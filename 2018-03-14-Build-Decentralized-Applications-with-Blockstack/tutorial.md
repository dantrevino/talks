# How to Easily Decentralize your Apps with Blockstack #
## Introduction to the Blockstack Identity and Storage APIs for Developers ##


Blockstack's identity and storage APIs let developers get started developing applications for the new decentralized Internet, quickly and easily.  This is a short demonstration of how easy it to adapt existing applications.

### Getting Started ###

* [Blockstack Browser](https://blockstack.org/install)
* [Atom](https://atom.io) / [VSCode](https://code.visualstudio.com/)
* [Live Server](https://github.com/tapio/live-server) or any lightweight web server, preferably one with hot-reload

`npm install -g live-server`

### Dependencies and file/folder setup ###

1. Get and install dependencies
```
git clone https://github.com/dantrevino/html5-canvas-drawing-app
git clone https://github.com/blockstack/blockstack.js
cd html5-canvas-drawing-app
```
2. Update and add javascript dependencies
* Add blockstack.js

```
cp ../blockstack.js/dist/blockstack.js ./
```
Next, add blockstack to your index.html

```
<script src="/blockstack.js"></script>
```

One item to note.  CORS needs to be set on the development server since we're using a redirect for user authentication.  Start live-server with the CORS option in your project directory
```
live-server --cors
```

### The HTML ###

3. Break up page into display divs. Existing code should go into the 'app' div.
4. Add a signin button to the landing section.   
5. Add an avatar and username to the existing header bar.
6. Add a signout button
7. Add a save button

```
<body>
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

8. We're also going to need a manifest file.  Create `manifest.json` in the root of the directory with the following content

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

### The Javascript ###
9. Initialize blockstack, set up a user object and a filename constant

```
const blockstack = window.blockstack
var user = null
const STORAGE_FILE = 'sketch.png'
```
This is self explanatory.  We want variable handlers to access Blockstack functionality.


10. Now lets get started with authentication.  We'll check for user login.  If user is logged in show "app" div.  If user is not logged in show "landing" div.  This is a routine pattern.  We want to hide the application content until the user is logged in.  The landing page $('#landing') will include only a 'Sign-In with Blockstack' button.  The application $('#app') will house the primary application content.

Key Blockstack functions:
* __blockstack.redirectToSignIn()__: Generates an authentication request and redirects the user to the Blockstack browser to approve the sign in request.
* __blockstack.isUserSignedIn()__: Check if a user is currently signed in.
* __blockstack.handlePendingSignIn()__:  Tries to process any pending sign in request by returning a Promise that resolves to the user data object if the sign in succeeds.
* __blockstack.loadUserData()__:  Retrieves the user data object. The user's profile is stored in the key profile.
* __blockstack.Person()__

First, the sign-in button:
 <span style="color:red">blockstack.redirectToSignIn()</span>
```
$('#signinbtn').click(function(e) {
  var origin = window.location.origin + '/'
  console.log(origin)
  var manifest = origin + 'manifest.json'
  console.log(manifest)
  blockstack.redirectToSignIn(origin,manifest,['store_write','publish_data'])
})
```
Most single user applications will be able to use this function as highlighted.  The default configuration will give your application access to read/write to Gaia storage.  In this case, we are specifying an additional permission request `('publish_data')`, so we specify the options passed.

The `('publish_data')` scope will allow us to make our creations public to the world and allow us to pull them up and view them later.


```
$('#landing').toggle(!blockstack.isUserSignedIn())
$('#app').toggle(blockstack.isUserSignedIn())

if (blockstack.isUserSignedIn()) {
  this.userData = blockstack.loadUserData()
  this.user = new blockstack.Person(this.userData.profile)
  this.user.username = this.userData.username
} else if (blockstack.isSignInPending()) {
    blockstack.handlePendingSignIn()
    .then((userData) => {
      window.location = window.location.origin
  })
}

```

11. Populate avatar and username

```
$('#avatar').attr('src',this.user.avatarUrl())
$('#username').text(this.user.name())
```

12. Add click handler and signout functionality to signout button

```
$('#signoutbtn').click(function(e){
  blockstack.signUserOut(window.location.href)
})
```

13. Add save functionality
```
$('#savebtn').click(function(e) {
   var cnvs = $('#canvas')[0]
   var mypicture = cnvs.toDataURL()
   const encrypt = true
   blockstack.putFile(STORAGE_FILE,mypicture,encrypt)
})
```



## Profit ##
14. Create an image, and save it.
15. Lets find an our image.  Copy or type the command below into the web developer console:

```
blockstack.lookupProfile('dantrevino.id','https://core.blockstack.org/v1/names/')
```
16. Copy the gaia.blockstack.org url for your development server.  In my case: 127.0.0.1:37697, and paste it into the browser address with our default file name 'sketch.png'.
```
"https://gaia.blockstack.org/hub/1PcN47KKVeYEfuxokppB1Vm3yipsFMUnJd/sketch.png"
```
17. Since we're saving this as base64 encoding, we can paste the result directly into the browser address bar:
```
data:image/png;base64,iVBORw0KGgoA......=
```

## Win! ##
