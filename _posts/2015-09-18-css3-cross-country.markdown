---
layout:     post
title:      "Advanced CSS3"
subtitle:   "Notes of CSS3 Crosscontry at Codeschool.com"
date:       2015-09-18 12:00:00
author:     "tientm"
header-img: "img/css3.jpg"
---

# Frost-proof Fundamentals

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

Example: <http://codepen.io/tientm/pen/dYMqoa>