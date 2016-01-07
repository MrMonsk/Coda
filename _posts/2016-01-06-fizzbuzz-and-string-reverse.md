---
layout:     post
title:      "Fizzbuzz and String Reversal"
subtitle:   "trying to be more concise"
date:       2016-01-06
author:     "Yowon Yoon"
header-img: "img/post-bg-02.jpg"
---

Having been told my countless friends and mentors that the same coding challenges will appear again and again, I thought it best to go through the most common ones and practice them as much as possible.

### FizzBuzz:
>Write a program that prints the numbers from 1 to 100. But for multiples of three print `Fizz` instead of the number and for the multiples of five print `Buzz`. For numbers which are multiples of both three and five print `FizzBuzz`.

Apparently this is a very common interviewing problem, and after speaking with my mentor about it, the takeaway is to prove one's ability to utilize the modulo operator. Here is my solution:

{% highlight ruby %}
(1..100).each do |n|
	if n % 15 == 0
		puts "FizzBuzz"
	elsif n % 5 == 0
		puts "Buzz"
	elsif n % 3 == 0
		puts "Fizz"
	else
		puts n
	end
end
{% endhighlight %}

At first I did `n % 5 && n % 3 == 0` until my mentor pointed out to me that this could be combined down to simply `n % 15`. Doh! 

### String Reversal:
>Write a method that takes in an input of a string value and returns the reversed string. So for example, transform `hello` into `olleh`.

The first thought that popped into my head was the *reverse* method already built into the ruby string class, but this challenge likely wants me to reverse the string not using the *reverse* method. After scratching my head for a bit, I decided to push the input string into an array, and then reverse the order of array using a while loop:

{% highlight ruby %}
def reverse(input)
	ary = input.chars

	i = 0
	j = ary.length - 1
	while i < j
		last = ary[j]
		first = ary[i]

		ary[i] = last
		ary[j] = first

		i += 1
		j -= 1

	end

	return ary.join
end
{% endhighlight %}

However, ruby's string class actually has indices as well, so I refactored my code:

{% highlight ruby %}
def reverse2(x)
	rstring = ""
	(x.length-1).downto(0) do |i|
		rstring += x[i]
	end
	
	return rstring
{% endhighlight %}

Hooray! I have two solutions to this problem: one that utilizes arrays and one that does not, and the second solution is much cleaner. 

