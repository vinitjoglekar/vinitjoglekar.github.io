---
layout: default
title: About me
---

# About me

> Experience is what you get, when you don't get what you want &mdash; Socrates

After graduating in late 90's I joined my family's business. About the same time, 
I happened to buy a book titled [Artificial Intelligence](https://www.amazon.in/dp/0070087709) 
authored by Elaine Rich & Kevin Knight. The whole book was a fascinating 
read, but it was the passing reference to Prolog programming language that captured my attention. 
So I got hold of a Prolog compiler and taught myself a little bit of the
language. That was the first programming language I studied for my own curiosity &mdash; 
without any necessity for academic courses or work. But before I went to any serious depth in it, something else 
caught my attention - in some weblog, someone claimed that a toy library
accompanying an online book titled [The Art of Assembly Language 
Programming](https://www.randallhyde.com/AssemblyLanguage/www.artofasm.com/index.html)
had awesome pattern matching capabilities (behold the tenuous thread with 
Prolog). Whoever it was, he was talking about [this
](https://www.randallhyde.com/AssemblyLanguage/www.artofasm.com/AoAExtra/Patterns.html).

_The Art of Assembly Language Programming_ (AOA) mesmerized me. After a while, 
for no good reason, I decided to develop a business accounting software 
in assembly language! Obviously I did not know what I was taking on. To 
begin with, I developed a good fraction of `stdio.h` equivalent 
functionality as the foundation for my work &mdash; I was bootstrapping, 
and console IO was the first pre-requisite. Once this was achieved, I 
turned my attention to development of the core accounting engine. And 
here, I stumbled. AOA had taught me about integers but not about floating 
point numbers (I see that AOA linked above does discuss them at length, 
but my impression is that it did not, back in the 90's / early 2000s &mdash; or maybe I missed 
it back then). Anyway, after some research on internet, I found a wonderful 
tutorial about FPUs &mdash; [Simply FPU](http://www.ray.masmcode.com/tutorial/).
And in I went in to that rabbit hole, and studied the basics of [IEEE 754 
specification](https://en.wikipedia.org/wiki/IEEE_754). It was a revelation.
It is so easy to declare a `float` and an `int` variable in C, and use 
them together. But that simple syntax masks the gulf between 
the two types. And after having studied the basics, it was obvious that one 
must not use floating point numbers to represent amounts in an accounting 
package. Instead, one should just use integers!

All this was happening in slow motion &mdash; because I would work on this
in my free time. And being in business does not give you much
free time really. So by the time I achieved that realization, we had already
started using a commercial accounting software, and there was no point in 
pursuing this any further.

But still, I pursued this topic for some more time. FPUs provide you with 80-bit
floating point numbers. What if we want a superior precision and broader dynamic range?
So instead of the accounting software, I started to develop a library for floating
point numbers of arbitrarily defined precision and range in C, and managed to implement basic 
arithmetic operations. And in that process, got some first-hand experience of 
pitfalls of dealing with floating point numbers.

By this time, it was clear to me that I enjoy technical things more than business. 
So I moved to pursue a diploma in computing, and eventually a career
in software engineering.


