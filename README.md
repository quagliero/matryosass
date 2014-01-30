# Matryosass

Derived from 'Matryoshka' (a Russian nesting doll), Matryosass is a micro Sass library that gives you a fractional, nestable, responsive, reversible, <em>n-</em>col grid with custom namespaced media queries.

You tell Matryosass how many fractional widths you want, how big of a gutter, and what breakpoints - if any - you need. 

## Demo

* [View demo](http://quagliero.github.io/matryosass-grid)
* [View demo code](https://github.com/quagliero/matryosass-grid/tree/gh-pages)

## Implementation

Getting a Matryosass Grid up and running is quick and easy. Download the Sass file, define your grid variables (or not, we have defaults for that), `@import` it into your stylesheet and off you go. 

```scss
/* grid.scss */
$mg-fractions  : 12 !default;
$mg-gutter     : 24px !default;
```
```scss
/* your .scss file */
[Your own CSS]

@import "path/to/matryosass-grid";

[More of your own CSS]

```

## Settings

To come...

## Nesting, reversing, break-pointin'

To come...

Influenced by inuit.css, 'Don't Overthink It Grids' and Bootstrap. 
