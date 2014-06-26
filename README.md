# Matryo

Derived from 'Matryoshka' (a Russian nesting doll), Matryo is a focused Sass library that gives you a fractional, nestable, responsive, reversible, <em>n-</em>col layout system - with custom namespaced media queries. It's a lovechild of [inuit.css](http://github.com/csswizardry/inuit.css), [Don't Overthink It Grids](http://css-tricks.com/dont-overthink-it-grids), [Naming Media Queries](http://css-tricks.com/naming-media-queries/), and Bootstrap.

MatryoSass can be as scaled back or as expressive as you need it to be; Static thirds, or responsive sixteenths.

You tell it how many columns you want, how big of a gutter, and what breakpoints - if any - you need.  

Matryo works in fractions; no more using 'sixcol', 'span6, or 'col-6' when you just mean one half. The idea being you give a column a default width value, and then use your custom named media queries to act as width modifiers. 

So if you wanted a three quarter width column you'd use `<div class="grid__col 3/4">` and then if you wanted that to go down to 50% for medium screens and full width for very small screens, you'd use `<div class="grid__col 3/4 md-1/2 xs-1">`.   


## Demo

* [View demo](http://quagliero.github.io/matryosass)
* [View demo code](https://github.com/quagliero/matryosass/tree/gh-pages)

_Matryosass is for IE8 and above._

## Implementation

Getting Matryo up and running is quick and easy. Download the Sass file, define your variables, `@import` it into your stylesheet and off you go.

Since we're converting fractions to percentages I recommend you use the `--precision 10` flag when you compile your stylesheet. This will give much more consistency across browsers and devices.

```scss
/* Your _vars or _settings .scss file */
$matryo-fractions  : 12; // this can also be a list, e.g. 1,2,4,8
$matryo-gutter     : 30px;
```
```scss
/* your main .scss file */
[Your own CSS]

@import "path/to/matryosass";

[More of your own CSS]

```

## Settings

### $matryo-fractions
Straight out of the box you get 12 fractional widths to use. Whole, halves, thirds, quarters, fifths, sixths, sevenths... you get the idea. But you can have as many (or few) as you want. Whatever number you assign to `$matryo-fractions` will be the amount you get.
```scss
// @int
$matryo-fractions: 12;
```
####Update: You can now pass in a list! Don't need a full 12 column fractions? Then only declare what you need.
```scss
$matryo-fractions: 1,2,4,8
```
<hr>
### $matryo-gutter
Nothing crazy here, just the distance between each column. I'd recommend matching it to your base line height for some horizontal and vertical rhythm. Vertical rhythm? There are things like [Typcsset](http://github.com/csswizardry/typecsset) which are great at this.
```scss
// @int + unit
$matryo-gutter: 24px;
```
<hr>
### $matryo-border-box
Matryo uses `box-sizing: border-box` to keep everything in proportion. If you've already got this defined globally, or with normalize.css, then feel free to set this to false.
```scss
// @bool
$matryo-border-box: true;
```
<hr>
### $matryo-grid-class
Matryo uses BEM (Block__Element--Modifier) syntax by default, but you can change this to suit your personal preferences or team code style.
```scss
// @string
$matryo-grid-class: 'grid';
```
<hr>
### $matryo-col-class
Matryo uses BEM (Block__Element--Modifier) syntax by default, but you can change this to suit your personal preferences or team code style.
```scss
// @string
$matryo-col-class: 'grid__col';
```
<hr>
### $matryo-bp-*
There are 5 breakpoints in Matryosass (4 max-width, 1 min-width). They work from smallest to largest.

For each of these breakpoints you get three options: on/off, width, and name.
#### $matryo-bp-_n_
The first option is to enable/disable the breakpoint. If you don't need one, switch it to `false` to get a filesize reward.
```scss
// @bool
$matryo-bp-xs          : true;
```
#### $matryo-bp-_n_-width
Aptly named: define the width for the breakpoint.
```scss
// @int + unit
$matryo-bp-xs-width    : 30em; /* ~480px */
```
#### $matryo-bp-_n_-name
These will be the names you prefix to your column with modifiers, and also when you use the `@include media` mixin. By default these are named `xs`,`sm`,`md`,`lg`,`xl` for those familiar with Bootstrap - though I urge you to use naming conventions that work for __you__. 
```scss
// @string
$matryo-bp-xs-name     : 'xs';
```

## Grids: nesting, --rev, --flush

To start with you'll need to wrap your grid in a class of `.grid`, this has a negative left margin (the same width as the column gutter) so you don't need to worry about any `.last` or `:last-of-type` shenanigans. 

It is imperative you do not add any margins, widths or padding to the `.col` items themselves. They form the structure of your site, and you add content within them. To paraphrase Harry Roberts, "the grid and it's columns are the shelves on which you place your things."

A simple two-column layout with a 40%:60% split, which collapses to full width at the smallest breakpoint:
```html
<div class="grid">
  <div class="grid__col 2/5 xs-1">
    <!-- archive -->
  </div>
  <div class="grid__col 3/5 xs-1">
     <!-- blog post -->
  </div>
</div>
```
### Nesting
Now on a mobile device we probably want that display order to be reversed, so we'd use the `.grid--rev` class instead of `.grid`, which will float our `.col-` items to the right:
```html
<div class="grid--rev">
  <div class="grid__col 2/5 xs-1">
    <!-- archive -->
  </div>
  <div class="grid__col 3/5 xs-1">
     <!-- I'm down here, but I will appear above the archive! -->
  </div>
</div>
```

### Reversing
So what if we want a block of modules underneath the blog post, but within the same column? We nest within a new `.grid`. This is when fractional widths become so awesome, because we still have access to our whole range of percentages - but within a new container! So let's have 3 evenly spaced out modules that are 1/3 of the width of the blog post column:
```html
...
  <div class="grid__col 3/5">
     <!-- blog post -->
     
     <div class="grid">
      <!-- modules -->
      <div class="grid__col 1/3">
        <!-- module 1 -->
      </div>
      <div class="grid__col 1/3">
        <!-- module 1 -->
      </div>
      <div class="grid__col 1/3">
        <!-- module 1 -->
      </div>
     </div>
  </div>
...
```
### Flush
But what if we don't want the modules to have any space between them? We make things flush. Using `.grid--flush` instead of `.grid` removes all spacing between `.grid__col`s.

## Cols: widths, media-queries, -hide
All grid columns require the `col-` class as this gives it the default styles it needs to behave like a column. We then suffix it with its default width, e.g. `<div class="grid__col 1/3">`. 

You can then manipulate the widths of columns across all five breakpoints by prefixing the fractional width with the namespace you gave to the media-query. `<div class="grid__col 3/4 lg-2/3 md-3/5 sm-1/2 xs-1/1">`.

And depending on your defined widths and names, this will behave something like:
```css
/* The [~=] attribute selector is used so we don't have to 
	escape the fraction slash in the CSS */
[class~='3/4'] {
  width: 75%;
}
@media (max-width: 1024px) {
  [class~='lg-2/3'] {
    width: 66.6666%; 
  }
}
@media (max-width: 800px) {
  [class~='md-3/5'] {
    width: 60%; 
  }
}
@media (max-width: 640px) {
  [class~='sm-1/2'] {
    width: 50%; 
  }
}
@media (max-width: 640px) {
  .xs-1 {
    width: 100%; 
  }
}

```


You can do some pretty powerful stuff with columns and media queries. This is a snippet taken from the [demo](http://quagliero.github.io/matryosass), specifically the light pink row. 
```html
<div class="grid__col 1/10 xl-1/12 lg-1/2 md-1/3 sm-1/2">
	<div class="demo-block"></div>
</div>
<!-- only show these on biig screens,
	kinda like firebox.com end menu items -->
<div class="grid__col 1/12 lg-hide">
	<div class="demo-block"></div>
</div>
<div class="grid__col 1/12 lg-hide">
	<div class="demo-block"></div>
</div>
```
We set the width of the last two items to one-twelfth, and hide them on our `lg` breakpoint (the largest max-width one we set). So as soon we go past this point these are now visible. Anything past our `lg` breakpoint is in our `xl` media-query territory, where you'll see the columns above are set to `.xl-1/12`. This allows you to create layouts that show and hide columns across the whole range of breakpoints! 

## Using your media queries for content
So you've now got total control of your grid layout with your fractional widths and your custom namespaced modifiers - but what if you want to style content differently at these breakpoints as well? Layout and content changes tend to go hand in hand. This is where the `@include media()` mixin comes in to play.

The `media` mixin takes one argument, `$namespace`, which it will try to match against the names of the media queries you defined at the beginning. So to target something at the `md` breakpoint, you would use `@include media(md)`. And if you're doing lots of changes, it might look like:

```scss
.lede {
	font-size: 2em;
	
	@include media(xl) {
		font-size: 2.2em;
	}
	@include media(md) {
		font-size: 1.6em
	}
	@include media(sm) {
		font-size: 1.3em;
	}
	@include media(xs) {
		font-size: 1.1em;
	}
}
```
If the `media` mixin can't match your argument to one of your defined breakpoints, it will trigger the `@else` case, which is a wildcard. So you can pass through whatever you want to make a custom media query.

```scss
.lede {
...
	@include media('(min-width: 80em)') {
		font-size: 3em;
	}
}
```
## Contributing
If you can improve Matryo (and that includes the documentation!), amazing, send some pull requests this way!

## In the wild
I'd love to hear if you use Matryo in any of your projects. Happy nesting.
 
