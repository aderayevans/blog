## Table of Contents
1. [Introduction](#Introduction)
2. [Content](#Content)
3. [Conclusion](#Conclusion)

<h2 id='Introduction'></h2>

## Introduction

Hey guys, welcome to my blog recording my ruby self-taught process

I decided to learn this amazing language while I was trying to solving some ruby challenges to get my tenth badge in HackerRank

Ok let's do it

<h2 id='Content'></h2>

<hr>

## Create my first program in ruby
```ruby
print "Hello World!!!"
```
**Output**
```powershell
PS D:\Workplace> ruby hello-world.rb
Hello World!!!
```

> print "\n" equals puts

```ruby
print "First line "
print "still first line\n"
puts "Second line"
puts "Thirld line"
```
**Output**
```powershell
First line still first line
Second line
Thirld line
```
<hr>

## Everything is object
```ruby
print else
```
**Output**
```powershell
main
```
<hr>

## Call Object Method

> check whether the num is even or odd

```ruby
num = 2
print num.even?
```
**Output**
```powershell
true
```
<hr>

## Call Object Method Parameters

>print the quotient of num and 2

```ruby
num = 2
num.div 2
print num
```
**Output**
```powershell
1
```
<hr>

## First loop

>print the value of each member in array to the power of 2

```ruby
array = [1, 2, 3, 4, 5]
array.each do |num|
    puts num.pow 2
end
```
**Output**
```powershell
1
4
9
16
25
```
<hr>

## First function

>print ASCII chars of any decimal number in array if number is not odd

```ruby
def print_char(array)
    array.each do |num|
        puts num.chr unless num.odd?
    end
end
array = [65, 66, 67, 68, 69, 70, 71]
print_char(array)
```
**Output**
```powershell
B
D
F
```
<hr>

## Array
**Working on single element**

> Delete last element

```ruby
arr.pop
```

> Delete first element

```ruby
arr.shift
```

> Delete element at position a given position

```ruby
arr.delete_at(2)
```
**Working on multiple elements**

> Delete all occurrences of a given element

```ruby
arr.delete(5)
```

> Delete elements if

```ruby
arr.delete_if {|a| a < 2}
```

> Delete elements unless

```ruby
arr.keep_if {|a| a < 4}  
```
**Create subarray**

> Select elements from array to subarray

```ruby
arr2 = arr.select {|a| a > 2}
print arr2
```

> Reject elements from array to subarray

```ruby
arr2 = arr.reject {|a| a > 2}
```

> Reject elements from array till returns false for the first time

```ruby
arr2 = arr.drop_while {|a| a > 1}
```
<hr>

## Hash, a dictionary-like data structures
```ruby
# initialize and set default value
empty_hash = Hash.new 
empty_hash.default = 1
# or
default_hash = Hash.new(1)
```
**Set value**
```ruby
new_hash = {"key1" => 12, "key2" => 50}
# or
new_hash = Hash.new
new_hash["key1"] = 12
new_hash["key2"] = 50
# or
new_hash.store("key1", 12)
new_hash.store(1512032, 50)
```
**Loop with hash**
```ruby
hash.each do |key, value|
    puts key
    puts value
end
# or
hash.each do |array|
    # now key is array[0], value is array[1]
    puts array[0]
    puts array[1]
end
```
**Delete pair**
```ruby
# Delete specific key
hash.delete("key1")
# Delete if
hash.keep_if {|key, value| key.is_a? Integer} 
# or 
hash.delete_if {|key, value|key.even? }
```
<hr>

## Infinite Loop
```ruby
i = 0
loop do
    puts i
    i += 1
    break if i == 10
end
```
**Output**
```powershell
1
2
3
4
5
6
7
8
9
10
```

<h2 id='Conclusion'></h2>

<hr>

## Conclusion
We have learned how to print output

How to do some basic loop and function

Learned some common methods of array and a dictionary-like data structures called hash

I'd like to thank HackerRank for giving me a chance to acknowledge and be interesting in this cool language

If guys found Ruby is fascinating, please come to the link below and solve some Ruby challenges with me 

<https://www.hackerrank.com/domains/ruby>

If you have any question or suggestion, please let me know at the comment section below.

OK I'm going to wrap this up here

`Thanks for reading my blog`