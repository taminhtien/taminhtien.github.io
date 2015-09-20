---
layout:     post
title:      "Advanced CSS3"
subtitle:   "Notes of CSS3 Crosscontry at Codeschool.com"
date:       2015-09-18 12:00:00
author:     "tientm"
header-img: "img/css.png"
---

# Frost-proof Fundamentals
---

## Sloop Style
Adding CSS:

- Inline style attribute
- In the ```<head>```
- External ```<link>```

Inline style attribute:

~~~
<h1 style="color: #98c7d4;">CSS Cross Country</h1>
~~~

In the ```<head>```:

~~~
<head>
  <style>
    h1 { color: #98c7d4; }
  </style>
</head>
~~~

External ```<link>```:

~~~
<head>
  <title>CSS Cross Country</title>
  <link rel="stylesheet" href="styles.css" />
</head>
~~~

## Selectors

Primary DOM selectors

- Element selector
- Class selector
- ID selector

Element selector

~~~
<h1 class="intro" id="header">Nice and Toasty</h1>

h1 {
  color: #aba4ac;
  margin-bottom: 10px;
}
~~~

Class selector

~~~
<h1 class="intro" id="header">Nice and Toasty</h1>

.intro {
  color: #aba4ac;
  margin-bottom: 10px;
}
~~~

ID selector

~~~
<h1 class="intro" id="header">Nice and Toasty</h1>

#header {
  color: #aba4ac;
  margin-bottom: 10px;
}
~~~

Compound selectors

~~~
<h1 class="intro" id="header">Nice and Toasty</h1>

h1#header {
  color: #aba4ac;
  margin-bottom: 10px;
}
~~~

## Cascade Order

Style priority is determined by position in site:

- External
- In the <head>
- Inline style attribute
- Using ```!important```

From External to using ```!important``` is the increasing priority.

Priority is also dependant on position in document:

~~~
.intro {
  color: #444245;
}

.intro { // the second defination will override the first one.
 color: #dddadd;
}
~~~

Non-conflicting properties will be combined:

~~~
.intro {
  color: #dddadd;
}

.intro {
  margin-bottom: 5px;
  width: 900px;
}

-> Combine to:

.intro {
  color: #dddadd;
  margin-bottom: 5px;
  width: 900px;
}
~~~

## Floating Left & Right

Removes element from the document flow and moves them to a specified edge.
Other content within the parent element will wrap around floats.

~~~
float: left / right / none;
~~~

**Stacking order:**

- Floated elements stack up to the parent edge, then move down to the next available edge.
- Take care with elements that have differing heights - the first available edge isn't always below.

E.g: *<http://codepen.io/tientm/pen/dYMqoa>*

# Clear Carving
---

## Clearing Float

Clearing is necessary if:

- Floated items can be taller than non-floated content, e.g: *<http://codepen.io/tientm/pen/garBWG>*
- All children are floating, e.g: *<http://codepen.io/tientm/pen/avNRGd>*

Common float-clearing methods:

~~~
clear: left / right / both;
~~~

- Clear with subsequent element, e.g: *<http://codepen.io/tientm/pen/jbqeKd>*
  - Requires sequence to stay intact - breaks if things move
  - Background / border do not extend
- Manual clearing, e.g: *<http://codepen.io/tientm/pen/epZPaN/>*
  - Requires empty element
  - Might not be necessary later
- The clearfix, e.g: *<http://codepen.io/tientm/pen/EVKOYg>*
  - Originally developed by Tony Aslett
  - Redefined version by Nicholas Gallagher
  - When used on the parent, the children will be self-cleared

More details about clearfix: *<http://hocwebchuan.com/tutorial/tut_css_clearfix.php>*

## Inheritence & Specificity
---
Nested elements automatically inherit parent styles:

~~~
<article class="featured">
  <p>Dang, it's cold up here!</p>
</article>

.featured {
  color: #aba4ac; // The paragraph content above will inherit this color
}
~~~

Selectors can be nested to override parent properties:

~~~
<article class="featured">
  <p>Dang, it's cold up here!</p>
</article>

.featured {
  color: #aba4ac; // The paragraph content above will inherit this color
}

.featured p { // Nesting the element selector overrides the color on .featured
  color: #fff;
}
~~~

**Dealing with specificity:**

- ID has higher priority than Class, e.g: *<http://codepen.io/tientm/pen/bVpQvb>*

~~~
<div id="content" class="featured">
  <p>Break out the cocoa.</p>
</div>

#content {
  color: #555; // It will be adapted
}
.featured {
  color: #ccc; // It's not
}
~~~

- The priority of a selector (specificity):

~~~
0(inline styles?), 0(# of ID selectors), 0(# of class selectors), 0(# of element selectors)

p { color: #fff; }                      // 0, 0, 0, 1
.intro { color: #98c7d4; }              // 0, 0, 1, 0
#header { color: #444245; }             // 0, 1, 0, 0
<h1 style="color: #000;">Mogul</h1>     // 1, 0, 0, 0
p { color: #fff !important; }           // !!!
.intro p.article { color: #fff; }       // 0, 0, 2, 1
.intro ul li.active { color: #98c7d4; } // 0, 0, 2, 2
#header { color: #444245; }             // 0, 1, 0, 0
~~~

- ID and element selectors versus class, e.g: *<http://codepen.io/tientm/pen/avNQEL>*

~~~
<section id="content">
  <p class="featured">Free coffee with ski rental.</p>
  <p>Choose from 48 different ski colors.</p>
</section>

#content p { // 0, 1, 0, 1. It will affect both p elements
  color: #000;
}
.featured { // 0, 0, 1, 0.
  color: #777;
}
~~~

- ID and element selectors versus !important, e.g: <http://codepen.io/tientm/pen/xwVQMW>

~~~
<section id="content">
  <p class="featured">Free coffee with ski rental.</p>
  <p>Choose from 48 different ski colors.</p>
</section>

#content p { // It will affect both p elements again.
  color: #000;
}
.featured {
  color: #777 !important;
}
~~~

- ID and element selectors versus ID and class selectors, e.g: <http://codepen.io/tientm/pen/bVpQJd>

~~~
<section id="content">
  <p class="featured">Free coffee with ski rental.</p>
  <p>Choose from 48 different ski colors.</p>
</section>

#content p { // 0, 1, 0, 1
 color: #000;
}
#content .featured { // 0, 1, 1, 0
 color: #777;
}
~~~

# Box Bindings
---

## The Box Model

An imaginary diagram that outlines each DOM element:

{: .center}
![](/img/dom.png)

__Width:__

- Total calculated box width = content width + padding width + border width
- When adapting a design, you'll need to calculate the content width

__The overflow property:__

~~~
overflow: visible / auto / hidden / scroll;
~~~

- _visible:_ the default value, which allows element content extend beyond container boundaries, e.g: _<http://codepen.io/tientm/pen/bVpyPO>_
- _auto:_ adds a scrollbar as needed when content overflows, e.g: _<http://codepen.io/tientm/pen/dYMEBz>_
- _hidden:_ hides content that extends beyond the container, e.g: _<http://codepen.io/tientm/pen/KdzLjj>_
- _scroll:_ adds a scrollbar at all times, even if unneeded, e.g: _<http://codepen.io/tientm/pen/JYXqgE>_

## Positioning

__Elements have a position value of static by default:__

~~~
position: static / relative / absolute / fixed;
~~~

- Using a value other than static causes an object to become a _positioned element._
- Positioned elements may use the top, left, right, bottom properties for placement.

__Relative positioning:__

Renders in the normal fow, then shifted via positioning properties, e.g: _<http://codepen.io/tientm/pen/KdzLOj>_

__Absolute positioning:__

Takes an element out of the normal fow for manual positioning, e.g: _<http://codepen.io/tientm/pen/dYMBbz/>_

__Fixed positioning:__

Afxes an element to a specifc place in the window, where it will stay regardless of scrolling, e.g: _<http://codepen.io/tientm/pen/garNOj>_

## Z-Index

__Manually adjusting overlap:__

- No ```z-index``` or equal ```z-index``` = overlap determined by placement in DOM
- Higher values appear above lower values
- Elements must be positioned for ```z-index``` to take efect. Use relative if you're not interested in moving the object

E.g: _<http://codepen.io/tientm/pen/YyqoPY>_

# Grooming Your Code
---

## Staying DRY

__Selected CSS property shorthands:__

~~~
font: italic  bold    16px/18px         sans-serif;
/*    style   weight  size/line-height  family */

background: #000  url(image.jpg) no-repeat  center  top;
/*          color image          repeat     x-pos   y-pos */

list-style: disc  inside    none;
/*          style position  image */

margin or padding: 0   10px  0      10px / 0   10px       0      / 0          10px;
/*                 top right bottom left / top right&left bottom / top&bottom right&left */

border: 3px   solid #ccc;
/*      width style color */
~~~

## Display Types

__Display:__

~~~
display: none / block / inline / inline-block;
~~~

- Block element:
  - Stretch the full width of their container
  - Behave as though there is a line break before and after the element
  - Full box model can be manipulated
  - Tags that are block-level by default: ```<div>, <p>, <ul>, <ol>, <li> and <h1> through <h6>```
- Inline elements:
  - Typically found within block-level elements
  - Only take up the space of the content inside
  - Do not generate a line break before and after the content
  - Tags that are inline by default include ```<span>, <a>, <em>, <img>, and <strong>```
- Inline-block
  - Same fow as an inline element but behave as a block element

## Centering

__Centering a block-level element:__

- Defne a width, and the element width must be less than that of the parent container
- ```margin: 0 auto;```

__Centering inline and inline-block elements:__ ```text-align:center```

# CSS Safety
---

## Protecting Your Layout

Example of collapsing margins: _<http://codepen.io/tientm/pen/YyqoaO>_

Collapsing margins will not occur when one or more block element has:
- Padding or border
- Relative or absolute positioning
- A foat left or right

Example of Non-collapsing margins: _<http://codepen.io/tientm/pen/XmdLoa>_

## Specificity Problems

Resets & normalization:
- Eric Meyer's Reset CSS: _<http://meyerweb.com/eric/tools/css/reset/>_
- Normalize.css: _<http://necolas.github.io/normalize.css/>_

# Image Issues
---

## Image Use

- Content should be marked up as inline images, e.g: _<http://codepen.io/tientm/pen/wKWajj>_
- Layout elements should be defned as background images, e.g: _<http://codepen.io/tientm/pen/dYXoKN>_

## Image Cropping

- Resize images to a square < height and width of all of your images
- Resize them server-side
- Provide image-uploading instructions in your CMS

E.g: _<http://codepen.io/tientm/pen/NGrqOO>_

# Sprightly Slaloms
---

## Image Replacement

Add descriptive text to image-replaced elements:

~~~
<a href="#" class="logo">Sven's Snowshoe Emporium</a>
.logo {
  background: url(logo.png);
  display: block;
  height: 100px;
  width: 200px;
  text-indent: -9999px; // Move the text out of the view port
}
~~~

E.g: _<http://codepen.io/tientm/pen/XmKdMw>_

# Sprites

~~~
<a href="#" class="logo">Sven's Snowshoe Emporium</a>

.logo {
  background: url(logo.png);
  display: block;
  height: 100px;
  width: 200px;
  text-indent: -9999px;
}

.logo:hover, .logo:focus {
  background: url(hover.png); // Loading another image will add an extra HTTP request
}
~~~

E.g: _<http://codepen.io/tientm/pen/zvBqwg>_

__=> Sprites mean the combination images into one file and using `background-position` to get needed image.__

- `background-position` will allow us to change orientation of our image inside of the element.
- `background` property default is 0(x-axis) 0(y-axis).

Recipe:

~~~
background-position: <x-axis change> <y-axis change>

Note: Because background-position shifts image to (0, 0) location, therefore:
- y < 0, shift up
- y > 0, shift down
~~~

Advantages to the sprite approach:

- Reduces number of HTTP image requests
- Removes loading flash / need for pre-load

`base64` encoding:

- Direct embed images into your CSS
- IE8+

~~~
background-image: url(data:image/png;base64,iVBO...;
~~~

`base64` method encodes images directly into CSS, HTML or JS. That allows us to not need to use sprites or include separate images.

# Pseudo
---

## Pseudo Classes

Allow you to conditionally select an element based on state or position:

~~~
.twitter:hover, .twitter:focus {
  background-position: 0 -100px;
}
.github:hover, .github:focus {
  background-position: -100px -100px;
}
~~~

A selection of useful selectors:

~~~
:hover / :focus / :active / :visited
:first-child / :last-child / :only-child
:nth-child() / :nth-of-type()
~~~

E.g: _<http://codepen.io/tientm/pen/EVyKLa>_

## Pseudo Elements

Example:

~~~
<article>
  <p>Coffee? Hah! Our cocoa is far better.</p>
  <p>Visit from 4-5 for cocoa happy hour!</p>
</article>

article p:last-child:after {
  content: '\2744';
}
~~~

A selection of useful pseudo elements:

~~~
:before / :after IE8+
:first-letter / :first-line
~~~

:before and :after effectively add two additional places per element on the page for styling

Example of positioned elements: _<http://codepen.io/tientm/pen/qONZyN>_
