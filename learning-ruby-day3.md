## Table of Contents
- [Table of Contents](#table-of-contents)
- [Introduction](#introduction)
- [Take user input](#take-user-input)
- [Convert](#convert)
- [Pass multiple arguments](#pass-multiple-arguments)
- [Default arguments](#default-arguments)
- [Keyword arguments](#keyword-arguments)
- [Block](#block)
- [Proc](#proc)
- [Conclusion](#conclusion)

## Introduction

Hey guys, welcome to my blog recording my ruby self-taught process

I decided to learn this amazing language while I was trying to solving some ruby challenges to get my tenth badge in HackerRank

At the first two days, We have learned about some common collections such as array and hash in ruby. We have also gotten to know with string.

Today, we will learn more about methods and arguments 

<hr>

## Take user input
```ruby
str = gets

p str
```
**Output**
```powershell
"hi\n"
```
I typed `hi` and hit Enter

As you can see, it also gets the NEWLINE character, which we don't want to.

So use the chomp method we have learned before to delete that last character at every `gets`

_One more problem here_

`gets` just gets input as raw type, we need to convert it to other type to use it

```ruby
i = gets.to_i

p i
```
**Output**
```powershell
4
```
We converted the input to integer, if you type a non-digit character, `i` will be `0`

## Convert
Convert variable types in Ruby is pretty simple.
```ruby
# String to integer
i = str.to_i
# String to float
f = str.to_f
# Anything to string
str = ob.to_str

# or if you want to catch error unless user type digit
# String to integer
i = Integer(str)
# String to float
f = Float(str)
```
## Pass multiple arguments
```ruby
def append(*rest)
    str = ""
    rest.each do |x|
        str << x
    end
    str
end

print append("the", " ", "end")
```
**Output**
```powershell
the end
```
`*rest` is a array of all arguments passed
## Default arguments
```ruby
def increase(num1, num2 = 1)
    num1 + num2
end
n = 5
puts increase(n)
puts increase(n, 5)
```
**Output**
```powershell
6
10
```
## Keyword arguments
Convert Temperature program using keyword arguments input_scale and output_scale as default arguments
```ruby
def celsius_kelvin(num)
    return num + 273.15
end

def kelvin_celsius(num)
    return num - 273.15
end

def celsius_fahrenheit(num)
    return num * 1.8 + 32
end

def fahrenheit_celsius(num)
    return (num - 32) / 1.8
end

def kelvin_fahrenheit(num)
    return (num - 273.15) * 1.8
end

def fahrenheit_kelvin(num)
    return ((num - 32) / 1.8) + 273.15
end
    
def convert_temp(num, input_scale: 'celsius', output_scale: 'celsius')
    return num if input_scale == output_scale
    cmd = input_scale << "_" << output_scale << "(#{num})"
    return eval cmd
end

puts convert_temp(0, input_scale: 'kelvin', output_scale: 'celsius')

puts convert_temp(393, input_scale: 'kelvin', output_scale: 'celsius')

puts convert_temp(400, input_scale: 'fahrenheit', output_scale: 'celsius')

puts convert_temp(333, input_scale: 'fahrenheit', output_scale: 'kelvin')
```
**Output**
```vim
-273.15
119.85000000000002
204.44444444444443
440.3722222222222
```
We could also set a hash parameter `**` that helps user pass a key argument
```ruby
def foo(str: "foo", num: 424242, **options)
    options.each_pair do |key, val|
        puts key
        puts options[key]
    end
end

foo(key: "val", key2: "val2")
```
**Output**
```vim
key
val
key2
val2
```

## Block
Blocks are nameless methods that can be passed to another method as a parameter
```ruby
def call_block
    puts "Start"
    yield
    puts "End"
end 

# Pass a block {puts "I'm in"} to call_block method
# We can pass with do..end
call_block do 
    puts "I'm in"
end
# or
call_block { puts "I'm in" }
```
**Output**
```shell
Start
I'm in
End
```
We can also pass a block to a method that takes parameters
```ruby
def call_block(a, b)
    puts "Start"
    yield(a, b)
    puts "End"
end 

call_block(12, 23) {|a, b| puts a - b}
```
**Output**
```shell
Start
-11
End
```
## Proc
"_A Proc object is an encapsulation of a block of code, which can be stored in a local variable, passed to a method or another Proc, and can be called._"

If Block is a nameless method that can be passed to another method right after the method name

Proc is now the object that holding block, we can pass it as a normal variable to another method
```ruby
def square_of_sum (arr_, proc_sum, proc_square)
    sum = proc_sum.call(arr_)
    proc_square.call(sum)
end

proc_sum_arr       = proc {|arr| arr.sum}
proc_square_number = proc {|x| x**2}

puts square_of_sum([1, 2], proc_sum_arr, proc_square_number)
```
If Block codes are called by `yield` key word

Proc codes are called by call() method

<hr>

## Conclusion
Today we have learned how to take user input, convert variables in ruby

We also have learned some advanced ways to create methods and pass arguments

Knowledged a closure object called Proc, and a nameless method called Block

<hr>

I'd like to thank HackerRank for giving me a chance to acknowledge and be interesting in this cool language

If guys found Ruby is fascinating, please come to the link below and solve some Ruby challenges with me 

<https://www.hackerrank.com/domains/ruby>

If you have any question or suggestion, please let me know at the comment section below.

OK I'm going to wrap this up here

`Thanks for reading my blog`