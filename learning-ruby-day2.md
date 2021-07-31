## Table of Contents
1. [Introduction](#Introduction)
2. [Content](#Content)
3. [Conclusion](#Conclusion)

<h2 id='Introduction'></h2>

## Introduction

Hey guys, welcome to my blog recording my ruby self-taught process

I decided to learn this amazing language while I was trying to solving some ruby challenges to get my tenth badge in HackerRank

At the first day, We have gotten to know Ruby. If you found it a little hard to understand then let me know immediately, otherwise I will keep writing this blog as a learning process recording

Today I will focus on more details what we have learned at the first day

<hr>

<h2 id='Content'></h2>

## Print output
Print value of variable and type of variable
```ruby
name = "Ade"
puts "Hello #{name}!"
puts "#{name.class.name}"
```
As we have discussed at the first day "Everything is Object", so we're now able to know that type of variable is a class name

**Output**
```powershell
PS D:\Workplace> ruby hello-world.rb
Hello Ade!
String
```
Print raw version of an object, use for debugging string. 

_P is a kernel method_
```ruby
a = " \n"
p a
```
**Output**
```powershell
" \n"
```
Pretty printting, use for print Hash object
```ruby
json = {
    "2019":[
       {
          "language":"Ruby",
          "edition":"seventh"
       },
       {
          "language":"Python",
          "edition":"sixth"
       },
       {
          "language":"Oracle",
          "edition":"second"
       }
    ],
    "2020":[
        {
          "language":"C++",
          "edition":"first"
       },
       {
          "language":"Java",
          "edition":"fourth"
       },
       {
          "language":"Mysql",
          "edition":"third"
       }
    ]
}
puts json
puts "----------------------------------------------------"
pp json
```
**Output**
```powershell
{:"2019"=>[{:language=>"Ruby", :edition=>"seventh"}, {:language=>"Python", :edition=>"sixth"}, {:language=>"Oracle", :edition=>"second"}], :"2020"=>[{:language=>"C++", :edition=>"first"}, {:language=>"Java", :edition=>"fourth"}, {:language=>"Mysql", :edition=>"third"}]}
----------------------------------------------------
{:"2019"=>
  [{:language=>"Ruby", :edition=>"seventh"},
   {:language=>"Python", :edition=>"sixth"},
   {:language=>"Oracle", :edition=>"second"}],
 :"2020"=>
  [{:language=>"C++", :edition=>"first"},
   {:language=>"Java", :edition=>"fourth"},
   {:language=>"Mysql", :edition=>"third"}]}
```
_As you can see, it looks pretty as it name_

<hr>

## Too much if - use Case instead
```ruby
if today == "Monday"
    puts "2, 30 July 2021"
elsif today == "Tuesday"
    puts "3, 30 July 2021"
#...
else
    puts "8, 30 July 2021"
end
```
```ruby
case today
when "Monday"
    puts "2, 30 July 2021"
when "Tuesday"
    puts "3, 30 July 2021"
#...
else
    puts "8, 30 July 2021"
end
```
**Output**
```powershell
6, 30 July 2021
```
<hr>

## Playing with array elements
```ruby
arr = [65, 66, 67, 68, 69, 70, 71, 72, 73, 74, 75, 76, 77, 78]
puts "Array: #{arr.inspect}"
puts "Array length = #{arr.length}"
puts "First element: #{arr[0]}"
puts "First element: #{arr.first}"
puts "Last element: #{arr[-1]}"
puts "Last element: #{arr.last}"
puts "Five first elements #{arr.take(5).inspect}"
puts "Ignores five first elements #{arr.drop(5).inspect}"
puts "Element at index 3 #{arr[3]}"
puts "Elements from index 3 to index 7 #{arr[3..7]}"
puts "Elements from index 3 to index 6 #{arr[3...7]}"
puts "8 Elements from index 3 #{arr[3, 8]}"
```
**Output**
```powershell
Array: [65, 66, 67, 68, 69, 70, 71, 72, 73, 74, 75, 76, 77, 78]
Array length = 14
First element: 65
First element: 65
Last element: 78
Last element: 78
Five first elements [65, 66, 67, 68, 69]
Ignores five first elements [70, 71, 72, 73, 74, 75, 76, 77, 78]
Element at index 3 68
Elements from index 3 to index 7 [68, 69, 70, 71, 72]
Elements from index 3 to index 6 [68, 69, 70, 71]
8 Elements from index 3 [68, 69, 70, 71, 72, 73, 74, 75]
```

>inspect help puts print all array elements in one line

<hr>

## Add elements to array

At the last blog, we have learned a bunch of ways to delete elements from array, let's look back a little
```ruby
arr = [65, 66, 67, 68, 69, 70, 71, 72, 73, 74, 75, 76, 77, 78]
puts "Array: \t\t\t#{arr.inspect}"
arr.shift
puts "Delete first element: \t#{arr.inspect}"
arr.pop.inspect
puts "Delete last element: \t#{arr.inspect}"
arr.delete_at(2).inspect
puts "Delete at index 2: \t#{arr.inspect}"
```
**Output**
```powershell
Array:                  [65, 66, 67, 68, 69, 70, 71, 72, 73, 74, 75, 76, 77, 78]
Delete first element:   [66, 67, 68, 69, 70, 71, 72, 73, 74, 75, 76, 77, 78]
Delete last element:    [66, 67, 68, 69, 70, 71, 72, 73, 74, 75, 76, 77]
Delete at index 2:      [66, 67, 69, 70, 71, 72, 73, 74, 75, 76, 77]
```
Now we're learning some ways to add elements to array
```ruby
arr = [65, 66, 67, 68, 69, 70]
puts "Array: \t\t\t#{arr.inspect}"
arr.unshift(97, 98)
puts "Add at first position: \t#{arr.inspect}"
arr.push(254, 255)
puts "Add at last position: \t#{arr.inspect}"
arr.insert(5, 128, 129)
puts "Add at index 5: \t#{arr.inspect}"
```
**Output**
```powershell
Array:                  [65, 66, 67, 68, 69, 70]
Add at first position:  [97, 98, 65, 66, 67, 68, 69, 70]
Add at last position:   [97, 98, 65, 66, 67, 68, 69, 70, 254, 255]
Add at index 5:         [97, 98, 65, 66, 67, 128, 129, 68, 69, 70, 254, 255]
```
As you can see we can add more than just one element
<hr>

## Here document
```ruby
puts 'Starting', '------------', <<HERE, 'Real Ending'
    1. Salad mix.
    2. Strawberries.
    3. Cereal.
    4. Milk.
HERE
```
**Output**
```powershell
Starting
------------
    1. Salad mix.
    2. Strawberries.
    3. Cereal.
    4. Milk.
Real Ending
```
This will print 'Starting' and '------------' normally as puts always do

The `<<HERE` here means the next occurrence of `HERE` will be the end of this document

`'Real Ending'` is lying right after the `<<HERE`, will be print out right after the end of the document

You can set multiple `<<` to exchange words in the document

`<<HERE` will be failed if there is any space or tab before the next occurrence `HERE`, `<<-HERE` is saying the next occurence can have some space, tab or `HERE`

Please check this link to learn more about this feature

<https://en.wikibooks.org/wiki/Ruby_Programming/Here_documents>
<hr>

## String
In this part, we're going to talk a little more about string in Ruby

String elements can be called in multiple ways

* Each char

```ruby
str.each_char {|x| p x}
```
**Output**
```shell
"W"
"h"
"a"
"t"
"'"
"s"
" "
"u"
"p"
"?"
```
* Each byte

```ruby
str.each_byte {|x| p x}
```

**Output**
```shell
87
104
97
116
39
115
32
117
112
63
```
* Each line

```ruby
"hello\nworld".each_line {|s| p s}
```
**Output**
```shell
"hello\n"
"world"
```
We can access elements of a string just like how we do with array

But we cannot delete or add elements to string like we do with array or hash

This is how we do it

_Remember these methods will just return a new string, it does not change the original string_
* Delete last char

```ruby
str = "Hi   \t\r\n"
p str.chop.chop
```
**Output**
```shell
"Hi   "
```
_You can see that we can chop multiple time, `\r`, `\n`, `\r\n` (exept `\n\r` though) will be treat as one char_

* Delete multiple last chars
  
```ruby
str = "Hi, My name is Ade\r\n\r"
p str = str.chomp
p str = str.chomp
p str.chomp "Ade"
```
**Output**
```shell
"Hi, My name is Ade\r\n"
"Hi, My name is Ade"
"Hi, My name is "
```
_Delete `\r` or `\n` or `\r\n` unless there is a parameter_

* Delete whitespaces

```ruby
str = "   \r\n\tHi     ,  Are you having fun?\t   \r    \n"
p str.strip
```
**Output**
```shell
"Hi     ,  Are you having fun?"
```
_Delete the leading and trailing `\t\n\r` and whitespaces_

* Append str

```ruby
str = ""
str += "Hello"
# or
str = ""
str << "Ruby is " << "pretty"
# How to append non-string
str << 3.14.to_s
```
* Add to the beginning

```ruby
str = "Gimme your wallet"
p str
p str.prepend("Please, ")
```
**Output**
```shell
"Gimme your wallet"
"Please, Gimme your wallet"
```
Check text occurs in str with include
```ruby
str.include? "wallet"
```
Replace text in str with gsub, first parameter can be RegExp or String, second parameter is string will replace the occurrence texts
```ruby
str.gsub(/wallet/, heart)
```
```ruby
str = "Please, Gimme your wallet"
if str.include? "wallet"
    puts str.gsub(/wallet/, "heart")
end
```
**Output**
```shell
Please, Gimme your heart
```

<hr>

<h2 id='Conclusion'></h2>

## Conclusion
We have learned more about printing object

Interesting feature called Here document to print multiple line strings

Acknowledged how to access, add and delete elements in array and string, or as i say "playing around with array and string"

<hr>

I'd like to thank HackerRank for giving me a chance to acknowledge and be interesting in this cool language

If guys found Ruby is fascinating, please come to the link below and solve some Ruby challenges with me 

<https://www.hackerrank.com/domains/ruby>

If you have any question or suggestion, please let me know at the comment section below.

OK I'm going to wrap this up here

`Thanks for reading my blog`