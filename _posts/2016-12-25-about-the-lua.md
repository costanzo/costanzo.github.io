---
title:        "lua chapter 1"
description:  "The beginning for writing script for Dota2"
image:        "http://placehold.it/400x200"
author:       "Bryan"
toc: true
toc_label: "Table of Contents"
---

0 . The Beginning of Everything
=

Before writing my very first technical post, I think I have to say something about my blog.

I have been thinking about writing a diary a few years ago but I was too lazy to write something down. More importantly I think I am better at writing code than articles. Now I am in Japan for the winter program and get enough time  thinking what I really like to do. I feel that I cannot waste my time watching TV series or playing computer games. So I decide to set up my personal blog and write something. Actually my motivation for writing a blog is to record what I have learned in some areas that I am interested in.

As a fan of Dota2, it might be awesome to design an AI that can compete with human beings. The current robot in the game is too stupid to some extend. So I think I am going to study and design a model that can fight against human players. It sounds really ambitious but it is at least a target worth fighting for. So this blog is about some AI algorithms and details about writing a dota robot.

I think I am not a good geek because I am really struggling using [github page](https://pages.github.com/) and [jekyll](https://jekyllrb.com/) to set up my blog. Writing with [MarkDown](https://daringfireball.net/projects/markdown/) is also a challenging thing but I will get used to it in a few weeks.

1 . Where to start
=

There are some really useful websites that I recently find.

[VALVE Developer Community for Dota Bot Scripting](https://developer.valvesoftware.com/wiki/Dota_Bot_Scripting) is a very helpful website for developers. I did not think steam provide interfaces for us to develop robot so this is totally surprise for me. It provides a lot of information that I need. I have just look through the website and will read it in detail in the next few weeks.

[Dota2 Bot Scripting Forum](http://dev.dota2.com/forumdisplay.php?f=497) is a forum discussing the scripting writing which may be helpful.

In this website it is mentioned that the we must write the scripts in programming language lua, which is completely new to me. Then let's start learning lua.

2 . Start learning lua
=

lua is a popular language for computer game robot script and a lot of games like World of Warcraft and Star wars.

Since I use windows, [luaDist](http://luadist.org/) has the package that I have for my system. Just download it and put it somewhere. Then add this path to the system environment path and you can use it by cmd.

[ZeroBrane Studio](https://studio.zerobrane.com/) is an IDE for lua development.

For any questions in Lua, [Lua Reference Manual](https://www.lua.org/manual/5.3/) would be very helpful.

3 . Lua notes
=

1 . comment
-
	--[[content of comment --]]

2 . variables
-
* **Global variable**: default variable is global

		b = 10
* **Local variable**: must be explicitly specified

		local i j
* **Table fields**: can hold anything except nil

In single statement, multiple lvalues and rvalues are allowed

	g,l = 20,30

3 . Data types
-

Variables don't have types but value has

* **nil**: default value of variable
* **boolean**
* **number**: double floating point
* **string**
* **function**
* **userdata**: arbitrary C data
* **thread**:independent threads of execution and used to implement coroutines
* **talbe**: associative arrays, can hold any value except nil

4 . operator
-
Similar to C except

* ~= means not equal
* use *and*, *or* and *not* for logical operators

		a = true
		b = false
		not ( a and b)

* *..* concatenates two strings

		a = "hello "
		b = "wolrd"
		c = a..b

* *#* : return the length of string or table

		#"hello" will return 5

* precedence from high to low
	* not # -
	* ..
	* \* / %
	* \+ -
	* < > <= >= == ~=
	* == ~=
	* and
	* or

5 . Loops
-
* while loop

		while(condition)
		do
		    statements
		end

* for loop

		for init, max/min, increment --the increment is 1 by default
		do
			statements
		end

* repeat..until

		repeat
			statements
		while(condition)

* break as C

6 . if..else
-

	if(boolean expression1)
	then
		statement1
	elseif(boolean expression2)
	then
		statement2
	else
		statement3
	end

7 . function
-

* **define a function**

		(local) function functionName(arguments)
		function statements
		return results -- can be separated with commas
		end

* **assigning and passing functions**

		--assigning a function to a variable
		funcName = function(arg1, arg2)
		function statements
		end

		--define a function that accept a function as parameter
		function func(arg1, arg2, f)
		f(arg1, arg2)  --execute this function

		--execute the second function
		func(arg1, arg2, funcName)

* **variable arguments**

		function funcName(...)
		local args = {...}
		other processes
		end

8 . String
-

	--three ways to express strings
	s1 = "lua"
	s2 = 'lua'
	s3 = [[lua]]

useful string functions can be found in the [manual of string manipulation](https://www.lua.org/manual/5.3/manual.html#6.4)

9 . array
-

* one-Dimensional array

		array = {"str1", "str2"}  --an array with two elements, index start from 1
		array = {}
		for i=-2, 2 do
			array[i] = i*2
		end

		--basically one-dimensional array is pretty like a hashmap
		for i=-2, 2 do
			print(array[i])
		end

* multi-Dimensional array

		--intializing the array
		array = {}
		for i=1,3 do
			array[i] = {}
			for j =1,3 do
				array[i][j] = i*j
			end
		end

		--accessing the array
		for i=1,3 do
			for j=1,3 do
				print(array[i][j])
			end
		end

10 . [Iterators](https://www.tutorialspoint.com/lua/lua_iterators.htm)
-

* **generic iterator**

		array = {"lua","tutor"}
		for key,value in ipairs(array)
		do
			print(key, value)
		end

* **stateless iterators**: this iterator does not retain any state. Each time the function is called, it returns the next element of the collection based on a second variable sent to the function.

* **stateful iterators**: use closure to retain variables values across function calls.

11 . tables
-

Actually lua does not have arrays, it has table which can be called array

* usage

		maytable = {}
		--assignment
		mytable[1] = "lua"
		--removing reference
		mytable = nil

* [table manipulation](https://www.lua.org/manual/5.3/manual.html#6.6)
	* table.concat(table..)
	* table.insert(table..)
	* table.sort(table..)

12 . modules
-

use *require* to import module, there are several ways to *require* the module and use the function within it.

	--method 1
	require "printFormatter"
	printFormatter.simpleFormat("lua")

	--method 2
	local formatter = require "printFormatter"
	formatter.simpleFormat("lua")

	--method 3
	require "printFormatter"
	local formatterFunction = printFormatter.simpleFormat
	formatterFunction("lua")

creating a module

	local mymath = {}

	function mymath.add(a,b)
		print(a+b)
	end

	return mymath

**note**:

1. place both the modules and the file to run in the same directory
2. module name and its file name should be the same

13 . Object Oriented
-

OOP in lua is implemented by adding functions to a table

* creating a class

		-- meta class
		Rectangle = {area = 0, length = 0, breadth = 0}

		-- derived class method new
		function rectangle:new(o, length, breadth)
			o = o or {}
			setmetatable(o, self)
			self._index = self
			self.length = length or 0
			self.breadth = breadth or 0
			self.area = length*breadth
			return o
		end

		--derived class method printArea
		function Rectangle:printArea()
			print("rectangle",self.area)
		end

* creating an object

		r = Rectangle:new(nil, 10,20)

* accessing properties

		print(r.length)

* accessing member function

		r:printArea()

* inheritance

		--extend the rectangle class
		Square = Rectangle:new()
		--derived class method new
		function Square:new (o, side)
			o = o or Shape:new(o, side, side)
			setmetatable(o, self)
			self._index = self
			return o
		end

* overriding base functions

		--override printArea
		function Square:printArea()
			print("Square", self.area)
		end
