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

Git commit [8493536](https://github.com/dantrevino/html5-canvas-drawing-app/commit/8493536ec0f698842133ef63edcbd037a26fb612)

## HTML Setup ##

3. Break up page into display divs. Existing code should go into the 'app' div.
```
<div id="landing"></div>
<div id="app"></div>
```
4. Add a signin button to the landing section.   
5. Add an avatar and username to the existing header bar.
6. Add a signout button
7. Add a save button
8. Add save as image functionality (https://www.html5canvastutorials.com/advanced/html5-canvas-save-drawing-as-an-image/)

## JS Setup ##
7. Check for user login.  If user is logged in show "app" div.  If user is not logged in show "landing" div
by using jQuery: $('#app').toggle(isUserLoggedIn), $('#landing').toggle(!isUserLoggedIn)
8. Populate avatar and username
9. Add click handler to signout button
10. Add save functionality

## Profit ##
11. set up netlify to deploy from tutorial branch

