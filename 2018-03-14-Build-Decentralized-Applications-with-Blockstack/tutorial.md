# Introduction to the Blockstack Identity and Storage APIs


Blockstack's identity and storage APIs let developers get started developing applications for the new decentralized Internet, quickly and easily.  This is a short demonstration of how easy it to adapt existing applications.

## Getting Started

* [Blockstack Browser](https://blockstack.org/install)
* [Atom](https://atom.io)
* [Atom Live Server](https://atom.io/packages/atom-live-server)

## Dependencies and file/folder setup ##

1. Clone repos needed
```
git clone https://github.com/dantrevino/html5-canvas-drawing-app
git clone https://github.com/blockstack/blockstack.js
cd html5-canvas-drawing-app
```
2. Update and add javascript dependencies
* Add blockstack.js
* Update jquery to current version.  Download from [here](https://jquery.com/download/)

```
mkdir js
cp ../blockstack.js/dist/blockstack.js ./js
edit index_jQuery.html ... update jquery and add blockstack.js
mv index.html index.html.orig
mv index_jQuery.html index.html
```
Next, copy jquery-3.3.1-min.js from your Downloads directory to your new js directory.  Next, modify index.html so that jQuery and Blockstack are referenced properly.

```
<script src="js/jquery-3.3.1.min.js"></script>
<script src="js/blockstack.js"></script>
```

One more item to note.  CORS needs to be set on the development server since we're using a redirect for user authentication.  Create a file in the root directory called ".atom-live-server.json" ...note the leading period.  The contents should be:
```
{"cors": true}
```

## The HTML ##

3. Break up page into display divs. Existing code should go into the 'app' div.
```
<div id="landing"></div>
<div id="app"></div>
```
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

## The Javascript ##
9. Initialize blockstack, a login indicator, and a user object in `$(document).ready()`

```
const blockstack = window.blockstack
var user = null
```

10. Check for user login.  If user is logged in show "app" div.  If user is not logged in show "landing" div

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
  var mypicture = $('#content').toDataURL()
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
