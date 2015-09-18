---
layout:     post
title:      "Advanced CSS3"
subtitle:   "Notes of CSS3 Crosscontry at Codeschool.com"
date:       2015-09-18 12:00:00
author:     "tientm"
header-img: "img/css3.jpg"
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

Demo: *<http://codepen.io/tientm/pen/dYMqoa>*

# Clear Carving
---
## Clearing Float

Clearing is necessary if:

- Floated items can be taller than non-floated content, demo: *<http://codepen.io/tientm/pen/garBWG>*
- All children are floating, demo: *<http://codepen.io/tientm/pen/avNRGd>*

Common float-clearing methods:

~~~
clear: left / right / both;
~~~

- Clear with subsequent element, demo: *<http://codepen.io/tientm/pen/jbqeKd>*
  - Requires sequence to stay intact - breaks if things move
  - Background / border do not extend
- Manual clearing, demo: *<http://codepen.io/tientm/pen/epZPaN/>*
  - Requires empty element
  - Might not be necessary later
- The clearfix, demo: *<http://codepen.io/tientm/pen/EVKOYg>*
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

- ID has higher priority than Class, demo: *<http://codepen.io/tientm/pen/bVpQvb>*

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

- ID and element selectors versus class, demo: *<http://codepen.io/tientm/pen/avNQEL>*

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

- ID and element selectors versus !important, demo: <http://codepen.io/tientm/pen/xwVQMW>

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

- ID and element selectors versus ID and class selectors, demo: <http://codepen.io/tientm/pen/bVpQJd>

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