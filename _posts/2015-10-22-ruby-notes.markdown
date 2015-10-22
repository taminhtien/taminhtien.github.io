---
layout:     post
title:      "Ruby notes"
subtitle:   "Some concepts in Ruby"
date:       2015-10-22 12:00:00
author:     "tientm"
header-img: "img/ruby.jpg"
---

> References: Codeacademy.com

# Blocks, Lambda, Proc
---

## Blocks

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

## Lambda

Like procs, lambdas are objects. The similarities don't stop there: with the exception of a bit of syntax and a few behavioral quirks, lambdas are identical to procs.

Check out the code in the editor. See the ```lambda``` bit? Typing

~~~
lambda { puts "Hello!" }
~~~

Is just about the same as

~~~
Proc.new { puts "Hello!" }
~~~

### Lambda Syntax

Lambdas are defined using the following syntax:

~~~
lambda { |param| block }
~~~

Lambdas are useful in the same situations in which you'd use a proc. 

### Lambdas vs. Procs

If you're thinking that procs and lambdas look super similar, that's because they are! There are only two main differences.

First, a lambda checks the number of arguments passed to it, while a proc does not. This means that a lambda will throw an error if you pass it the wrong number of arguments, whereas a proc will ignore unexpected arguments and assign nil to any that are missing.

Second, when a lambda returns, it passes control back to the calling method; when a proc returns, it does so immediately, without going back to the calling method.

## Quick Review

All this talk of blocks, procs, and lambdas might have your head spinning. Let's take a minute to clarify exactly what each one is:

- A **block** is just a bit of code between do..end or {}. It's not an object on its own, but it can be passed to methods like .each or .select.
- A **proc** is a saved block we can use over and over.
- A **lambda** is just like a proc, only it cares about the number of arguments it gets and it returns to its calling method rather than returning immediately.

# Symbol
---

## What's a symbol?


You can think of a Ruby symbol as a sort of name. It's important to remember that symbols aren't strings:

~~~
"string" == :string # false
~~~

Above and beyond the different syntax, there's a key behavior of symbols that makes them different from strings: while there can be multiple different strings that all have the same value, there's only one copy of any particular symbol at a given time.

~~~
puts "string".object_id # => 15796720
puts "string".object_id # => 15796500

puts :symbol.object_id # => 319528
puts :symbol.object_id # => 319528
~~~

## What are Symbols Used For?

Symbols pop up in a lot of places in Ruby, but they're primarily used either as hash keys or for referencing method names. (We'll see how symbols can reference methods in a later lesson.)

~~~
sounds = {
  :cat => "meow",
  :dog => "woof",
  :computer => 10010110,
}
~~~

Symbols make good hash keys for a few reasons:

- They're immutable, meaning they can't be changed once they're created;
- Only one copy of any symbol exists at a given time, so they save memory;
- Symbol-as-keys are faster than strings-as-keys because of the above two reasons.
