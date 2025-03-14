<div align="center">

# **Python**

![Python](./pic/python.gif)
</div>

# type conversion or type casting

## init

  int(): Converts a value to an integer.

    x = "10"
    x_int = int(x)  # converts string "10" to integer

## float

  float(): Converts a value to a floating-point number.
  
    x = "10.5"
    x_float = float(x)  # converts string "10.5" to float

## str

  str(): Converts a value to a string.

    x = 23
    x_str = str(x)  # converts integer 23 to string

## bool

  bool(): Converts a value to a boolean (True or False).

    x = 1
    x_bool = bool(x)  # converts integer 1 to True

# collection of elements.

## Dict, List, Tuple, Set

## List []

    list [] - an ordered, mutable (changeable) collection of elements.

    (my_list = [1,2,3,"apple",4.5])

##  Dictionary (dict) {}

    Dictionary - an unordered, mutable collection of key-value pairs.

    (my_dict = {"name": "Alice", "age": 25}).

## Tuple (tuple) ()

     tuple - an ordered, immutable (unchangeable) collection of elements.

     (my_tuple = (1, 2, 3, "apple", 4.5)).

## Set (set) {}

    set - an unordered, mutable collection of unique elements.

    (my_set = {1, 2, 3, 4, 5}).

# Built-in Functions

##  Mathematical Functions

  abs(x) – Returns the absolute value of x.
  
  round(x, n) – Rounds x to n decimal places.
  
  pow(x, y) – Returns x raised to the power of y (x ** y).
  
  min(iterable, *[, key, default]) – Returns the smallest item from an iterable.
  
  max(iterable, *[, key, default]) – Returns the largest item from an iterable.
  
  sum(iterable, /, start=0) – Returns the sum of the items in the iterable.

## Input/Output Functions

  print(*objects, sep=' ', end='\n', file=sys.stdout) – Prints objects to the console.
  
  input(prompt) – Reads a line of input from the user.
  
  open(file, mode='r') – Opens a file for reading or writing.

## Sequence Functions

  len(s) – Returns the length (number of items) of an object.
  
  sorted(iterable, *, key=None, reverse=False) – Returns a sorted list from the elements of any iterable.
  
  reversed(seq) – Returns an iterator that yields the elements of seq in reverse order.

## Miscellaneous Functions

  help([object]) – Displays help for an object or function.
  
  dir([object]) – Returns a list of attributes and methods of an object.
  
  callable(object) – Checks if an object appears callable (i.e., can be called like a function).
  
  eval(expression[, globals[, locals]]) – Evaluates a Python expression dynamically.
  
  exec(object[, globals[, locals]]) – Executes a Python code dynamically.
  
  slice(start, stop[, step]) – Returns a slice object (for slicing sequences).
  
  any(iterable) – Returns True if any item in the iterable is True.
  
  all(iterable) – Returns True if all items in the iterable are True.
  
## Exception Handling Functions

  raise – Used to raise an exception.
  
  try...except – Handles exceptions in code.

## Lambda

  lambda arguments: expression - one-line function that you can use when you need a simple function for a short period of time.

    #Lambda function to add two numbers
    
    add = lambda x, y: x + y
    
    #Calling the lambda function

    result = add(3, 5)
    
    print(result)  #Output: 8


  

# operation with numbers

## // (Floor Division)

   It divides two numbers and returns the integer part of the result, discarding the remainder.

   7 // 3  # Result: 2 (because 7 divided by 3 is 2.33, and we discard the decimal part)

## % (Modulo)

  get the remainder when one number is divided by another. 

  7 % 3  # Result: 1 (because 7 divided by 3 gives a remainder of 1)

## ** (Exponentiation)

  raises a number (the base) to the power of another number (the exponent).
  
  (2 ** 3  # Result: 8 (because 2 raised to the power of 3 is 8))

## continue

  continue - continue with the next iteration of the loop. It allows you to skip certain parts of the loop body and move on to the next cycle of the loop.

## pass

  pass - null operation or placeholder. It is used when you need to write a block of code that does nothing. 

# IF

  a = [1, 2]
  
  x = [1, 2]
  
  b = a

  if a == x # True
  
  if a is x # False
  
  if a is b # True

  if condition1:
  
      # code if condition1 is true
      
  elif condition2:
  
      # code if condition2 is true
      
  else:
  
      # code if both conditions are false
      

# for Loop

  for item in sequence:
  
    # Code to execute for each item

  for i in range(5):  # range(5) gives numbers from 0 to 4
  
    print(i)

# while Loop

  while condition:
  
    # Code to execute as long as the condition is true

  x = 0
  
  while x < 5:
  
    print(x)
    
    x += 1
    

# Functions

  block of code that performs a specific task and can be used to organize and reuse code.

  def function_name():
      # Do something
      return result

  x = function_name() # x will get result value.

# class

  class -  like a blueprint or template for creating objects (or instances). It defines what attributes (characteristics) and methods (functions) an object will have.

    #Define a class called Dog
    
    class Dog:
    
      #Constructor (method) to initialize attributes when creating an object
    
      def __init__(self, name, age):
    
        self.name = name  # Attribute: name of the dog
        
        self.age = age    # Attribute: age of the dog
        
      #Method: Function to make the dog bark
    
      def bark(self):
    
       return f"{self.name} says Woof!"

  #Creating objects (instances) from the Dog class
  
  dog1 = Dog("Buddy", 3)
  
  dog2 = Dog("Lucy", 5)

  
  #Calling the method on the objects
  
  print(dog1.bark())  # Output: Buddy says Woof!
  
  print(dog2.bark())  # Output: Lucy says Woof!
  

  * there are built-in class functions (example) set attribute for the class (like dog1.len()):

      def _ _str_ _(self):

        return f"unit {0} value {1}"

    def _ _len_ _(self):

      return int(self.variable)
    
## super()

  super() -  call methods from a parent class (or superclass) inside a child class. 

  super().method_name(arguments)




  
