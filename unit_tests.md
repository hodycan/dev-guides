# Cheatsheet

`import unittest`

`class TestCaseName(unittest.TestCase): pass`
`python -m unittest test_module.TestClass`
`python -m unittest test_module.TestClass.test_method`
`python -m unittest MODULE_NAME`

# Functions should be small

Before coding new features, 
break it down into as many functions as you can.

A rule of thumb is that each function should only do one thing.

Benefits:

- Quickly locate errors when something breaks
- More often than not, functions will eventually be
    reused, reducing the amount of duplicate code.
- You can test each function one by one

# Unit testing

Unit testing is a method of testing individual units of code so that
you can:

- frequently verify results and be on "stable ground"
- reduce wasted time coding too many things, 
    only to see it break when you run it for the first time

Ideally, before you write a new function, you'd first 
write a unit test that uses your function the way you'd imagine.

You may not always write tests before you write your function though,
especially for super simple and small functions.

It might sound like you'd write more code and code more slowly, 
but the amount of frustrations it saves will save you more time in 
the long run, as well as result in cleaner code.

Writing tests as you write your code is called 
Test-driven Development.

# How to unit-test with python

Python provides a built-in library called `unittest`, which provides the
`TestCase` class.

Each `TestCase` can include multiple tests.
e.g. testing multiple functions that are related, 
usually a group of functions that support an overall major feature.

Each test in a `TestCase` usually includes `assert` statements.

Assert statements do nothing if they pass, 
but raise an error if they fail.

For each thing you test:

1. Write a method in your TestCase class. 
The name should start with "test", followed by what you're testing
2. Inside, call the functions that you're testing
4. Write assert statements.


# Example

Let's say we want to write a function called `foo` that 
takes a number and returns the number squared.

Let's assume we already wrote that function in another module.

Let's write the tests:

```
import unittest
from other_module import foo

class TestFoo(unittest.TestCase):
    
    def test_big_number(self):
        # Fail test if foo(5) doesn't return 25
        self.assertEqual(foo(5), 25)

    def test_zero():
        self.assertEqual(foo(5), 25)

```



Use python's unittest library to do this.

`import unittest`

Create a test class for each group of tests.