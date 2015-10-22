---
layout:     post
title:      "Ruby notes"
subtitle:   "Some concepts in Ruby"
date:       2015-09-22 12:00:00
author:     "tientm"
header-img: "img/ruby.jpg"
---

> References: Codeacademy.com

# Blocks, Lambda, Proc
---

## Blocks
---

A Ruby block is just a bit of code that can be executed. Block syntax uses either ```do```..```end``` or curly braces (```{}```), like so:

~~~
[1, 2, 3].each do |num|
  puts num
end
# ==> Prints 1, 2, 3 on separate lines

[1, 2, 3].each { |num| puts num }
# ==> Prints 1, 2, 3 on separate lines
~~~

Blocks can be combined with methods like ```.each``` and ```.times``` to execute an instruction for each element in a collection (like a hash or array).

Why do some methods accept a block and others don't? It's because methods that accept blocks have a way of transferring control from the calling method to the block and back again. We can build this into the methods we define by using the yield keyword.

## Proc
---

Remember when we told you that everything is an object in Ruby? Well, we sort of fibbed. Blocks are not objects, and this is one of the very few exceptions to the "everything is an object" rule in Ruby.

Because of this, blocks can't be saved to variables and don't have all the powers and abilities of a real object. For that, we'll need... procs!

You can think of a proc as a "saved" block: just like you can give a bit of code a name and turn it into a method, you can name a block and turn it into a proc. Procs are great for keeping your code DRY, which stands for Don't Repeat Yourself. With blocks, you have to write your code out each time you need it; with a proc, you write your code once and can use it many times!

### Proc Syntax

Procs are easy to define! You just call ```Proc.new``` and pass in the block you want to save. Here's how we'd create a proc called ```cube``` that cubes a number (raises it to the third power):

~~~
cube = Proc.new { |x| x ** 3 }
~~~

We can then pass the proc to a method that would otherwise take a block, and we don't have to rewrite the block over and over!

~~~
[1, 2, 3].collect!(&cube)
# ==> [1, 8, 27]
[4, 5, 6].map!(&cube)
# ==> [64, 125, 216]
~~~

(The ```.collect!``` and ```.map!``` methods do the exact same thing.)

The ```&``` is used to convert the ```cube``` proc into a block (since ```.collect!``` and ```.map!``` normally take a block). We'll do this any time we pass a proc to a method that expects a block.

### Why Procs?

Why bother saving our blocks as procs? There are two main advantages:

- Procs are full-fledged objects, so they have all the powers and abilities of objects. (Blocks do not.)
- Unlike blocks, procs can be called over and over without rewriting them. This prevents you from having to retype the contents of your block every time you need to execute a particular bit of code.