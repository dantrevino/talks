# Blockstack Portland

Subdirectories contain notes and, if applicable, slides for each of the meetups.  As of March 2018, CSS theme has been generated that includes material design icons.

Branding should be consistent with colors/fonts identified at blockstack.org branding site:  ["Brands"](https://projects.invisionapp.com/boards/HE2VVROFSGB27/)

### Using the slides

Clone the repo
```
git clone https://github.com/dantrevino/blockstack-portland
```

Install reveal-md
```
npm install reveal-md
```

Copy the tempate or create your own slides
```
cp -a template <presentation subdirectory>
```

Launch presentation from its subdirectory
```
cd <presentation subdirectory>
reveal-md ./slides.md
```
Note that the template includes a link to the theme that is relative to where you start the presentation (ie. wherever you run reveal-md)

Point your browser to: [http://localhost:1948](http://localhost:1948)

### Updating the Blockstack theme

Start with the reveal.js themeing instructions
`https://github.com/hakimel/reveal.js/blob/master/css/theme/README.md`

Copy blockstack.scss to the `reveal.js/css/theme/source/` directory.  Modify as needed.

In the root reveal.js directory:
`npm run build -- css-themes`
