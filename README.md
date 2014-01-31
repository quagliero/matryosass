# Matryosass

Derived from 'Matryoshka' (a Russian nesting doll), Matryosass is a micro Sass library that gives you a fractional, nestable, responsive, reversible, <em>n-</em>col layout system - with custom namespaced media queries. It's a lovechild of <a href="http://github.com/csswizardry/inuit.css">inuit.css</a>, <a href="http://css-tricks.com/dont-overthink-it-grids/">Don't Overthink It Grids</a>, <a href="http://css-tricks.com/naming-media-queries/">Naming Media Queries</a>, and Bootstrap.

You tell Matryosass how many fractional widths you want, how big of a gutter, and what breakpoints - if any - you need.  

Matryosass Grid works in fractions; no more using 'sixcol' or 'col-6' when you just mean one half. The idea being you give a column a default width value, and then use your custom named media queries to act as width modifiers. 

So if you wanted a three quarter width column you'd use `<div class="col-3-4">` and then if you wanted that to go down to 50% for medium screens and full width for very small screens, you'd use `<div class="col-3-4 md-1-2 xs-1-1">`.   


## Demo

* [View demo](http://quagliero.github.io/matryosass) (the pink is nested, the grey is reversed!)
* [View demo code](https://github.com/quagliero/matryosass/tree/gh-pages)

## Implementation

Getting a Matryosass Grid up and running is quick and easy. Download the Sass file, define your variables, `@import` it into your stylesheet and off you go. 

```scss
/* grid.scss */
$mg-fractions  : 12;
$mg-gutter     : 24px;
```
```scss
/* your .scss file */
[Your own CSS]

@import "path/to/matryosass-grid";

[More of your own CSS]

```

## Settings

### $mg-fractions
```scss
// @int
$mg-fractions: 12;
```
Straight out of the box you get 12 fractional widths to use. Whole, Halves, thirds, quarters, fifths, sixths, sevenths... you get the idea. But you can have as many (or few) as you want. Whatever number you assign to `$mg-fractions` will be the amount you get.

### $mg-gutter
```scss
// @int + unit
$mg-gutter: 24px;
```
Nothing crazy here, just the distance between each column. I'd recommend matching it to your base line height for some horizontal and vertical rhythm. Vertical rhythm? There are things like <a href="http://github.com/csswizardry/typecsset">Typcsset</a> which are great at this.

### $mg-border-box
```scss
// @bool
$mg-border-box: true;
```
Matryosass uses `box-sizing: border-box` to keep everything in proportion. If you've already got this defined globally, or with normalize.css, then feel free to set this to false.

### $mg-bp-_n_(-/width/name)
```scss
// @bool
$mg-bp-xs          : true;
// @int + unit
$mg-bp-xs-width    : 30em; /* ~480px */
// @string
$mg-bp-xs-name     : 'xs';
```
You can declare up to 5 breakpoints in Matryosass (4 max-width, 1 min-width), by default these are named `xs`,`sm`,`md`,`lg`,`xxl` for those familiar with Bootstrap - though I urge you to use naming conventions that work for _you_.

## Nesting, reversing, break-pointin'

To come...

Influenced by inuit.css, 'Don't Overthink It Grids' and Bootstrap. 
