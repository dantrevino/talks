---
title: Introduction to the Blockstack Identity and Storage APIs for Developers
theme: theme/blockstack.css
---

<img src="blockstack-logo-landscape-rev.svg" height="95%" style="border:none;box-shadow:none;background:transparent;">

<img src="blockstack-0308.svg" height="36px" width="36px" style="border:none;vertical-align:middle;"> dantrevino.id

<i class="mdi mdi-twitter"></i>@dantrevino

---

## Easily Decentralize your Apps with Blockstack ##
#### Introduction to the Blockstack Identity and Storage APIs for Developers ####

---

## Getting Started ##

* [Blockstack Browser](https://blockstack.org/install)
* [Atom](https://atom.io) / [VSCode](https://code.visualstudio.com/)
* [Live Server](https://github.com/tapio/live-server) or any lightweight web server, preferably one with hot-reload

`npm install -g live-server`

Note:
Blockstack's identity and storage APIs let developers get started developing applications for the new decentralized Internet, quickly and easily.  This is a short demonstration of how easy it is to adapt existing applications and immediately gain the benefits of strong identity and encrypted storage for your users.

---

## Dependencies and Setup ##

```
git clone https://gitlab.com/dantrevino/html5-canvas-drawing-app.git
git clone https://github.com/blockstack/blockstack.js
cd html5-canvas-drawing-app
cp ../blockstack.js/dist/blockstack.js ./

<script src="/blockstack.js"></script>
```

Note:

Get and install dependencies.  Update and add javascript dependencies
* Add blockstack.js

Next, add blockstack to your index.html

---

```
live-server --cors
```
Note:
One item to note.  CORS needs to be set on the development server since we're using a redirect for user authentication.  Start live-server with the CORS option in your project directory

---

## The HTML ##

```
<div id="landing">
  <button type="button">Sign In with Blockstack</button>
</div>
<div id="app">
  <div id="page">
    <div class="header">
      <a id="new" class="navbtn">New</a>
      <div style="float:right;vertical-align:top;">
        <a id="savebtn" class="navbtn">Save</a>&nbsp;
        <img id="avatar" src="https://via.placeholder.com/32x32" height="32px" width="32px">
      </div>
      <div class="title"><span id="username">Unknown User</span>'s Sketch Pad</div>
    </div>
    <div id="content"><p style="text-align:center">Loading Canvas...</p></div>
    <div class="footer">
      <div style="float:right;vertical-align:top;">
        <a id="signout" class="navbtn">Sign Out</a>&nbsp;
      </div>
      <div class="palette-case">
      ...
```
Note:

In order to lay the foundation for the authentication and functionality we will:
1. Break up page into display divs. Existing code should go into the 'app' div.
1. Add a signin button to the landing section.   
1. Add an avatar and username to the existing header bar.
1. Add a signout button
1. Add a save button

---

## Manifest ##

```
{
  "name": "Sketch",
  "start_url": "/",
  "description": "Sketch. Save. Repeat.",
  "icons": [{
    "src": "http://dant.org/sketch.png",
    "sizes": "400x400",
    "type": "image/png"
  }]
}
```
Note:

We're also going to need a manifest file.  Create `manifest.json` in the root of the directory with the following content

---

## The Javascript ##

```
const blockstack = window.blockstack
var user = null
const STORAGE_FILE = 'sketch.png'
```

Note:
First we'll do some basic housekeeping ... initialize blockstack, set up a user object and a filename constant

---

## Key Blockstack functions ##

* __blockstack.redirectToSignIn()__
* __blockstack.isUserSignedIn()__
* __blockstack.handlePendingSignIn()__
* __blockstack.loadUserData()__
* __blockstack.signUserOut()__  

Note:
* __blockstack.redirectToSignIn()__: Generates an authentication request and redirects the user to the Blockstack browser to approve the sign in request.
* __blockstack.isUserSignedIn()__: Check if a user is currently signed in.
* __blockstack.handlePendingSignIn()__:  Tries to process any pending sign in request by returning a Promise that resolves to the user data object if the sign in succeeds.
* __blockstack.loadUserData()__:  Retrieves the user data object. The user's profile is stored in the key profile.
* __blockstack.signUserOut()__:  Sign the user out and optionally redirect to given location.

Now lets get started with fun parts... Blockstack authentication/authorization.  We'll check for user login.  If user is logged in show "app" div.  If user is not logged in show "landing" div.  This is a routine pattern.  We want to hide the application content until the user is logged in.  The landing page $('#landing') will include only a 'Sign-In with Blockstack' button.  The application $('#app') will house the primary application content.

---

## Authentication ##

```
$('#signinbtn').click(function(e) {
  var origin = window.location.origin + '/'
  console.log(origin)
  var manifest = origin + 'manifest.json'
  console.log(manifest)
  blockstack.redirectToSignIn(origin,manifest,['store_write','publish_data'])
})

$('#signoutbtn').click(function(e){
  blockstack.signUserOut(window.location.href)
})
```
Note:
First, we'll look at the Blockstack sign-in and sign-out functions:

__blockstack.redirectToSignIn()__

__blockstack.signUserOut()__

Most single user applications will be able to use this function as highlighted above.  The default configuration will give your application access to read/write to Gaia storage.  In this case, we are specifying an additional permission request `('publish_data')`, so we specify the options passed.

The `('publish_data')` scope allows us to make our application data public.  For the purposes of this demonstration, we'll be using this permission to enable us to pull up our wonderful pictures, and view them later.

Again we see here that Blockstack makes some really simple primitives available for managing the authentication.

---

## Authorization ##

```
$('#landing').toggle(!blockstack.isUserSignedIn())
$('#app').toggle(blockstack.isUserSignedIn())

if (blockstack.isUserSignedIn()) {
  this.userData = blockstack.loadUserData()
  this.user = new blockstack.Person(this.userData.profile)
  this.user.username = this.userData.username

  /* avatar and username code go here */

} else if (blockstack.isSignInPending()) {
    blockstack.handlePendingSignIn()
    .then((userData) => {
      window.location = window.location.origin
  })
}
```
Note:
Next we'll set the conditions for displaying our login button or the app ... our authorization components. Then we'll check to see if the user is logged in.  Blockstack makes simple authorization easy.  Any complex logic will need to be managed by your application.  For our purposes, we'll just check for a valid login.

---

## Profile Attributes ##

```
$('#avatar').attr('src',this.user.avatarUrl())
$('#username').text(this.user.name())
```

Note:
Populate avatar and username using Blockstack's user profile functionality by adding the following to the blockstack.isUserSignedIn() block

---

## Storage ##

```
$('#savebtn').click(function(e) {
   var cnvs = $('#canvas')[0]
   var mypicture = cnvs.toDataURL()
   const encrypt = true
   blockstack.putFile(STORAGE_FILE,mypicture,encrypt)
})
```

Note:
Finally, we'll use Blockstack's GAIA functionality to save an ecrypted version of our data.  Huge note here.  We are passing `encrypt=true` to the Blockstack putFile function, however, previously our app requested `publish_data` scope.  So even though we're encrypting the file save, our app is making that data _**public**_.

Add save functionality

---

## Profit ##
```
blockstack.lookupProfile('dantrevino.id','https://core.blockstack.org/v1/names/')
```
Note:
Create an image, and save it.

Lets find our image and take a look.  

Copy or type the command below into the web developer console:

Copy the gaia.blockstack.org url for your development server.  In my case: 127.0.0.1:8080, and paste it into the browser address with our default file name 'sketch.png'.

---

## Win! ##

```
"https://gaia.blockstack.org/hub/1PcN47KKVeYEfuxokppB1Vm3yipsFMUnJd/sketch.png"
data:image/png;base64,iVBORw0KGgoA......=
```
Note:
Since we're saving this as base64 encoding, we can paste the result directly into the browser address bar.

Blockstack's easy-to-use APIs let you quickly and easily support strong, encrypted user identity and encrypted storage.  Blockstack's feature set makes is a stong contender in the upcoming wave of Decentralized Applications that will make up the New Internet.

---

## Find Us ##

* <i class="mdi mdi-forum"></i> forum.blockstack.org

* <i class="mdi mdi-twitter"></i> @Blockstack

* <i class="mdi mdi-github-circle"></i> github.com/blockstack/

* <i class="mdi mdi-forum"></i> meetup.com/blockstack-portland

Note:

---
