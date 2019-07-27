---
layout: post
title:      "Understanding Return Values for Ruby Iterators"
date:       2019-07-27 18:28:49 +0000
permalink:  understanding_return_values_for_ruby_iterators
---




In Ruby, a handy method tool to understand is iteration and its related return value. “The verb iterate means to do the same thing many times, you know, so an iterator is something that does the same thing many times. ” Ruby Docs.
In other words, the loop written within your method iterates over the collection of objects in either your array or hash. Iteration allows you to look at elements contained in the array or hash, and pull out a controlled return. In Ruby these methods will have an implicit return. so using the word ‘return’ at then end of your method is not necessary. Choosing the right method is important since it allows you to control the return value and gives you a desired result. As a quick guide, I will describe the more popularly used methods: .each, .map & .collect, .select, .find, and .delete_if.

**.each** will always *return the original array.* This method will do something with the elements in the array or hash, such as .reverse or in the example below adds  “ -- “  between each element. The array will always contain the same number of elements.

a = [ "a", "b", "c" ] a.each {|x| print x, " -- " } 
produces:
a -- b -- c --


.**map or .collect**  can be used interchangeably and have a *return of a new array*. This is a very versatile tool and you have a lot of flexibility on what gets returned to you within the block.

a = [ "a", "b", "c", "d" ] a.collect { |x| x + "!" }         #=> ["a!", "b!", "c!", "d!"] a.map.with_index { |x, i| x * i } #=> ["", "b", "cc", "ddd"] a                                 #=> ["a", "b", "c", "d"]



**.select** will find a specific element(s) and return *a new array containing the element(s*). The array will be shorter.

[1,2,3,4,5].select { |num|  num.even?  }   #=> [2, 4]  a = %w{ a b c d e f } a.select { |v| v =~ /[aeiou]/ }  #=> ["a", "e"]


**.find**  similarly to .detect,  is used to locate a specific number element(s), but it will *return the (1) element from the original array if a match is found true.* Ifnone is called if nothing is found in the block, and this will return nil.

(1..100).detect  #=> #<Enumerator: 1..100:detect>
(1..100).find    #=> #<Enumerator: 1..100:find>

(1..10).detect   { |i| i % 5 == 0 and i % 7 == 0 }   #=> nil
(1..10).find     { |i| i % 5 == 0 and i % 7 == 0 }   #=> nil
(1..100).detect  { |i| i % 5 == 0 and i % 7 == 0 }   #=> 35
(1..100).find    { |i| i % 5 == 0 and i % 7 == 0 }   #=> 35


**delete_if**  will find the first true result and delete that specific item, and then *return a new array without the element.* Notice that it stops iterating over the array once it finds the element. 

scores = [ 97, 42, 75 ] scores.delete_if {|score| score < 80 }   #=> [97]


