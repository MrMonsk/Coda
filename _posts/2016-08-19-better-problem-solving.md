---
layout:     post
title:      "Better Problem Solving"
subtitle:   "Think better."
date:       2016-08-19
author:     "Yowon Yoon"
header-img: "img/bag-and-hands.jpg"
---
I came across [this](https://www.codewars.com/kata/next-bigger-number-with-the-same-digits/ruby) problem recently, and it was a fascinating introduction to start thinking a bit more critically about how to approach solving algorithmic challenges.

Subroutines, subroutines, and subroutines. The number of times I’ve heard this term used by _vastly_ superior programmers is staggering. To me, the longer I’ve spent working at writing algorithms and ‘thinking’ like a programmer, I’ve started to see how far into this subroutine mantra one can go. 

There are a couple things that pop up in my head when I read a problem statement now. Let’s talk generally about my thought processes in the context of the problem:

1. Read the problem and understand clearly what my _input_ vs. _desired output_ is
   - I need to take an _input_ of type _integer_ and return another _integer_ comprised of the same digits which is not only LARGER than the original input, but also the smallest of any combination of digits that is larger the original.
2. Think of the laziest way (brute-force) that I could solve this
   - Ruby’s Array class has a `permutation` method, so if I convert the _input_ _integer_ into a digits array, I can get all the different permutations that exist that are larger than the original input and store it as a new array of numbers larger than the original!
   - Find the minimum value in this new array of numbers that I know are larger than the original, and that would give me my next biggest number! Here it is in code:

{% highlight ruby %}
def next_bigger(n)
  bigger = []
  n.to_s.chars.permutation do |p|
    if (p.join.to_i > n)
      bigger << p.join.to_i
    end
  end
  bigger.min
end
{% endhighlight %}
  - Unfortunately, this solution is really poor in terms of both space complexity O((n!/(n-k)!)) and time complexity O(n*n!) since it still needs to find every permutation and compare that permutation with the original, and then find the minimum O(n), so yeah this solution is already looking really bad for large numbers.  
3. Now let’s take the subroutine algorithmic approach:  
  1. For me, this is where most of my time is spent. 
  2. Really look at what needs to change for a given number to find the next larger number comprised of the same digits.
    - The first thing I noticed was that a number in descending order (in terms of digits) is the largest possible permutation of those digits (e.g. 7654321).
    - The second thing I noticed was that if all the digits are in descending order EXCEPT the last two, then I merely need to swap the last two digits to get the next bigger number (e.g. 54312 → 54321)
    - The third thing I noticed was that there really were two ‘halves’ of the number, a `left` side and a `right` side, with only the digits on the `right` side needing to be swapped or reordered since we’re only concerned with the _next largest_.
    - Finally I realized that there is a digit that splits the left and right parts (i.e. first occurrence where the left digit is smaller than the right digit)
    - I can then swap the smallest digit to the right of this ‘pivot’ digit larger than the pivot with the pivot, and then sort the right half to get the next larger number! Here’s the code:
{% highlight ruby %}
def next_bigger(n)
  d = n.to_s.chars.map(&:to_i)
  pivot_index = d.length - 1
  while pivot_index > 0
    d[pivot_index] <= d[pivot_index - 1] ? pivot_index -= 1 : break
  end
  pivot_index = pivot_index - 1
  if pivot_index == -1
    -1
  else
    swap = d[pivot_index]
    left = d[0...pivot_index]
    right = d[pivot_index+1..-1]
    smallest = 10
    right.each do |e|
      if e < smallest && e > swap
        smallest = e
      end
    end
    right_index = right.find_index(smallest)
    right[right_index] = swap
    (left.join.to_s + smallest.to_s + right.sort.join.to_s).to_i
  end    
end
{% endhighlight %}

Not the prettiest code, but it works pretty well, and more importantly decreases our time complexity to O(n)!