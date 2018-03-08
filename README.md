# Blockstack Portland

Subdirectories contain notes and, if applicable, slides for each of the meetups.  Font awesome is included locally so that offline presentations will work.  Currently using version 5.06.

** As of March 2018 move to material design icons because fa

Align branding to blockstack.org ["Brands"](https://projects.invisionapp.com/boards/HE2VVROFSGB27/)

### Using the slides

Clone the repo
```
git clone https://github.com/dantrevino/blockstack-portland
```

Install reveal-md
```
npm install
```

Copy the tempate or create your own slides
```
cp -a template <presentation subdirectory>
```

Launch presentation from its subdirectory
```
reveal-md <presentation subdirectory>/slides.md --css <presentation subdirectory>/css/fontawesome-all.min.css
```
or after March 2018
```
reveal-md <presentation subdirectory>/slides.md --css <presentation subdirectory>/css/materialdesignicons.min.css
```

Point your browser to: [http://localhost:1948](http://localhost:1948)
