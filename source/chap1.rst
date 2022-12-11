
Chapter 3: Python
====================================

This chapter further develops  skills you learned in your first
CS course and adds to your bag of tricks by teaching you how to use
efficient algorithms for dealing with large amounts of data. Without the proper
understanding of efficiency, it is possible to bring even the fastest computers
to a grinding halt when working with large data sets. This has happened before,
and soon you will understand just how easy it can happen. But first, we'll
review some patterns for programming and look at the Python programming language
to make sure you understand the basic structure and syntax of the language.

There are some general concepts about Python that you should know. Python is an
interpreted language. That means that you don't have to go through any extra
steps after writing Python code before you can run it. Typing
`python <progname>` will run your program. Python is also dynamically typed.
This means that you will not get any type errors before you run your program as
you would with some programming languages. It is especially important for you to
understand the types of data you are using in your program. More on this in just
a bit. Finally, your Python programs are interpreted by the Python interpreter.
The REPL (i.e. Read, Evaluate, Print Loop) is another name for the interactive
Python intepreter command line and VS Code gives you access to a terminal window
where you can run a Python REPL within the IDE itself. You can type Python
statements and expressions to quickly try out a snippet of code before you put
it in a program.

To motivate learning or reviewing Python, the chapter will develop
a simple drawing application using turtle graphics and a Graphical User
Interface (GUI) framework called Tkinter. Along the way, you'll discover some
patterns for programming including the accumulator pattern and the loop and a
half pattern for reading records from a file. You'll also see functions in
Python and begin to learn how to implement your own datatypes by designing and
writing a class definition.

Chapter Goals
++++++++++++++++

By the end of this chapter, you should be able to answer these questions.

   * What two parts are needed for the accumulator pattern?
   * When do you need to use the loop and a half pattern for reading from a file?
   * What is the purpose of a class definition?
   * What is an object and how do we create one?
   * What is a mutator method?
   * What is an acessor method?
   * What is a widget and how does one use widgets in GUI programming?


Creating Objects
++++++++++++++++++

Python is an object-oriented language. All data items in Python are objects. In
Python, data items that could be thought of as similar are named by a type or
class. The term *type* and *class* in Python are synonymous: they are two names
for the same thing. So when you read about *types* in Python you can think of
*classes* or vice versa.

There are several built-in types of data in Python including *int*, *float*,
*str*, *list*, and *dict* which is short for dictionary. These types of data and
their associated operations are included in the appendices at the end of the
text so you have a quick reference if you need to refer to it while programming.
You can also get help for any type by typing *help(typename)* in the Python
shell, where *typename* is a type or class in Python.


Literal Values
----------------

There are two ways to create objects in Python. In a few cases, you can use a
literal value to create an object. Literal values are used when we want to set
some variable to a specific value within our program. For example, the literal 6
denotes any object with the integer value of 6. ::

  x = 6

This creates an *int* object containing the value 6. It also points the
reference called *x* at this object as pictured in :numref:`xreffig`. All
assignments in Python point references at objects. Any time you see an
assignment statement, you should remember that the thing on the left side of the
equals sign is a reference and the thing on the right side is either another
reference or a newly created object. In this case, writing *x = 6* makes a new
object and then points *x* at this object.

.. container:: figboxright

	.. _xreffig:

	.. figure:: images/xref.png

		A Reference and Object

Other literal values may be written in Python as well. Here are some literal
values that are possible in Python.

  * *int* literals : 6, 3, 10, -2, etc.
  * *float* literals : 6.0, -3.2, 4.5E10
  * *str* literals : 'hi there', "how are you"
  * *list* literals : [], [6, 'hi there']
  * *dict* literals : {}, {'hi there':6, 'how are you':4}

Python lets you specify *float* literals with an exponent. So, *4.5E10*
represents the *float* 45000000000.0. Any number written with a decimal point is
a *float*, whether there is a 0 or some other value after the decimal point. If
you write a number using the *E* or exponent notation, it is a float as well.
Any number without a decimal point is an *int*, unless it is written in *E*
notation. String literals are surrounded by either single or double quotes. List
literals are surrounded by [ and ]. The [] literal represents the empty list.
The {} literal is the empty dictionary.

You may not have done a lot with dictionaries previvously. A dictionary is a
mapping of keys to values. In the dictionary literal, the key 'hi there' is
mapped to the value 6, and the key 'how are you' is mapped to 4. More
information can be found
`here <https://docs.python.org/3/tutorial/datastructures.html>`_.

Non-Literal Object Creation
-----------------------------

Most of the time, when an object is created, it is not created from a literal
value. Of course, we need literal values in programming languages, but most of
the time we have an object already and want to create another object by using
one or more existing objects. For instance, if we have a string in Python, like
'6' and want to create an *int* object from that string, we can do something
like the following.

.. code-block:: python

	y = '6'
	x = int(y)
	print(x)

In this short piece of code, *y* is a reference to the *str* object created from
the string literal. The variable *x* is a reference to an object that is created
by using the object that *y* refers to. In general, when we want to create an
object based on other object values we write the following:

.. code-block:: python

	variable = type(other_object_values)

The *type* is any type or class name in Python, like *int*, *float*, *str* or
any other type. The *other_object_values* is a comma-separated sequence of
references to other objects that are needed by the class or type to create an
instance (i.e an object) of that type. Here are some examples of creating
objects from non-literal values.

.. code-block:: python

	z = float('6.3')
	w = str(z)
	u = list(w) # this results in the list ['6', '.', '3']

.. _callingmethods:

Calling Methods on Objects
++++++++++++++++++++++++++++

Objects are useful because they allow us to collect related information and
group them with behavior that act on this data. These behaviors are are called
*methods* in Python. There are two kinds of methods in any object-oriented
language: *mutator* and *accessor* methods. *Accessor* methods access the
current state of an object but don't change the object. *Accessor* methods
return new object references when called. ::

	x = 'how are you'
	y = x.upper()
	print(y)

Here, the method *upper* is called on the object that *x* refers to. The *upper*
accessor method returns a new object, a *str* object, that is an upper-cased
version of the original string. Note that *x* is not changed by calling the
*upper* method on it. The *upper* method is an accessor method. There are many
accessor methods available on the *str* type which you can learn about in the
appendices.

Some methods are mutator methods. These methods actually change the existing
object. One good example of this is the *reverse* method on the *list* type. ::

	myList = [1, 2, 3]
	myList.reverse()
	print(myList) # This prints [3, 2, 1] to the screen

The *reverse* method mutates the existing object, in this case the list that
*myList* refers to. Once called, a mutator method can't be undone. The change or
mutation is permanent until mutated again by some other mutator method.

All classes contain accessor methods. Without accessor methods, the class would
be pretty uninteresting. We use accessor methods to retrieve a value that is
stored in an object or to retrieve a value that depends on the value stored in
an object. If a class had no accessor methods we could put values in the object
but we could never retrieve them.

Some classes have mutator methods and some don't. For instance, the *list* class
has mutator methods, including the *reverse* method. There are some classes that
don't have any mutator methods. For instance, the *str* class does not have any
mutator methods. When a class does not contain any mutator methods, we say that
the class is *immutable*. We can form new values from the data in an *immutable*
class, but once an immutable object is created, it cannot be changed. Other
immutable classes include *int* and *float*.

Implementing a Class
+++++++++++++++++++++

Programming in an object-oriented language usually means implementing classes
that describe objects which hold information that is needed by the program you
are writing. Objects contain data and methods operate on that data. A *class* is
the definition of the *data* and *methods* for a specific type of *object*.

Every class contains one special method called a constructor. The constructor's
job is to create an instance of an object by placing references to data within
the object itself. For example, consider a class called Dog. A dog has a name, a
birthday, and a sound it makes when it barks. When we create a Dog object, we
would write something like the code appearing in :ref:`creatingcalling`.

.. _creatingcalling:

Creating Objects and Calling Methods
--------------------------------------

.. code-block:: python
	:linenos:

	boyDog = Dog("Mesa", 5, 15, 2004, "WOOOF")
	girlDog = Dog("Sequoia", 5, 6, 2004, "barkbark")
	print(boyDog.speak())
	print(girlDog.speak())
	print(boyDog.birthDate())
	print(girlDog.birthDate())
	boyDog.changeBark("woofywoofy")
	print(boyDog.speak())

.. container:: figboxright

	.. _dogobjects:

	.. figure:: images/dogobjects.png

		A Couple of Dog Objects

Once created, the dog objects would look like :numref:`dogobjects` in the memory
of the computer. Each object is referenced by the variable reference assigned to
it, either *girlDog* or *boyDog* in this case. The objects themselves are a
collection of references that point to the information that is stored in the
object. Each object has a name, month, day, year, and speakText references that
point to the associated data that make up a Dog object.

To be able to create *Dog* objects like these two objects we need a *Dog* class
to define these objects. In addition, we'll need to define *speak*, *birthDate*,
and *changeBark* methods. We can do this by writing a class as shown in
:ref:`dogclass`. Comments about each part of the class appear in the code. The
special variable *self* always points at the current object and must be the
first parameter to each method in the class. Python takes care of passing the
*self* argument to the methods. The other arguments are passed by the programmer
when the method is called (see the example of calling each method in
:ref:`creatingcalling`).

.. _dogclass:

The Dog Class
-----------------

.. code-block:: python
	:linenos:

	class Dog:
	    # This is the constructor for the class. It is called whenever a Dog
	    # object is created. The reference called "self" is created by Python
	    # and made to point to the space for the newly created object. Python
	    # does this automatically for us but we have to have "self" as the first
	    # parameter to the __init__ method (i.e. the constructor).
	    def __init__(self, name, month, day, year, speakText):
	        self.name = name
	        self.month = month
	        self.day = day
	        self.year = year
	        self.speakText = speakText

	    # This is an accessor method that returns the speakText stored in the
	    # object. Notice that "self" is a parameter. Every method has "self" as its
	    # first parameter. The "self" parameter is a reference to the current
	    # object. The current object appears on the left hand side of the dot (i.e.
	    # the .) when the method is called.
	    def speak(self):
	        return self.speakText

	    # Here is an accessor method to get the name
	    def getName(self):
	        return self.name

	    # This is another accessor method that uses the birthday information to
	    # return a string representing the date.
	    def birthDate(self):
	        return str(self.month) + "/" + str(self.day) + "/" + str(self.year)

	    # This is a mutator method that changes the speakText of the Dog object.
	    def changeBark(self,bark):
	        self.speakText = bark

Operator Overloading
++++++++++++++++++++++

Python provides operator overloading, which is a nice feature of programming
languages because it makes it possible for the programmer to interact with
objects in a very natural way. Operator overloading is already implemented for a
variety of the built-in classes or types in Python. For instance, integers (i.e.
the *int* type) understand how they can be added together to form a new integer
object. Addition is implemented by a special method in Python called the
*__add__* method. When two integers are added together, this method is called to
create a new integer object. If you look in the appendices, you'll see examples
of these special methods and how they are called. For example, the *__add__*
method is called by writing *x+y* where *x* is an integer. The methods that
begin and end with two underscores are methods that Python associates with a
corresponding operator.

When we say that Python supports operator *overloading* we mean that if you
define a method for your class with a name that is operator overloaded, your
class will support that operator as well. Python figures out which method to
call based on the types of the operands involved. For instance, writing *x+y*
calls the *int* class *__add__* method when *x* is an integer, but it calls the
*float* type's *__add__* method when *x* is a *float*. This is because in the
case of the *__add__* method, the object on the left hand side of the *+*
operator corresponds to the object on the left hand side of the dot (i.e. the
period) in the equivalent method call *x.__add__(y)*. The object on the left
side of the dot determines which add method is called. The *+* operator is
overloaded.

If we wanted to define addition for our *Dog* class, we would include an
*__add__* method in the class definition. It might be natural to write *boyDog +
girlDog* to create a new puppy object. If we wished to do that we would extend
our Dog class as shown in :ref:`dogoperator`.

.. _dogoperator:

The Dog Class with Overloaded Addition
----------------------------------------

.. code-block:: python
	:linenos:

	class Dog:
	    # This is the constructor for the class. It is called whenever a Dog
	    # object is created. The reference called "self" is created by Python
	    # and made to point to the space for the newly created object. Python
	    # does this automatically for us but we have to have "self" as the first
	    # parameter to the __init__ method (i.e. the constructor).
	    def __init__(self, name, month, day, year, speakText):
	        self.name = name
	        self.month = month
	        self.day = day
	        self.year = year
	        self.speakText = speakText

	    # This is an accessor method that returns the speakText stored in the
	    # object. Notice that "self" is a parameter. Every method has "self" as its
	    # first parameter. The "self" parameter is a reference to the current
	    # object. The current object appears on the left hand side of the dot (i.e.
	    # the .) when the method is called.
	    def speak(self):
	        return self.speakText

	    # Here is an accessor method to get the name
	    def getName(self):
	        return self.name

	    # This is another accessor method that uses the birthday information to
	    # return a string representing the date.
	    def birthDate(self):
	        return str(self.month) + "/" + str(self.day) + "/" + str(self.year)

	    # This is a mutator method that changes the speakText of the Dog object.
	    def changeBark(self,bark):
	        self.speakText = bark

	    # When creating the new puppy we don't know it's birthday. Pick the
	    # first dog's birthday plus one year. The speakText will be the
	    # concatenation of both dog's text. The dog on the left side of the +
	    # operator is the object referenced by the "self" parameter. The
	    # "otherDog" parameter is the dog on the right side of the + operator.
	    def __add__(self,otherDog):
	        return Dog("Puppy of " + self.name + " and " + otherDog.name, \
	                   self.month, self.day, self.year + 1, \
	                   self.speakText + otherDog.speakText)

	def main():
	    boyDog = Dog("Mesa", 5, 15, 2004, "WOOOOF")
	    girlDog = Dog("Sequoia", 5, 6, 2004, "barkbark")
	    print(boyDog.speak())
	    print(girlDog.speak())
	    print(boyDog.birthDate())
	    print(girlDog.birthDate())
	    boyDog.changeBark("woofywoofy")
	    print(boyDog.speak())
	    puppy = boyDog + girlDog
	    print(puppy.speak())
	    print(puppy.getName())
	    print(puppy.birthDate())

	if __name__ == "__main__":
	    main()

This text uses operator overloading fairly extensively. There are many operators
that are defined in Python. Python programmers often call these operators *Magic
Methods* because a method automatically gets called when an operator is used in
an expression. Many of the common operators are given in the table in
:ref:`magicmethods` for your convenience. For each operator the magic method is
given, how to call the operator is given, and a short description of it as well.
In the table, *self* and *x* refer to the same object. The type of *x*
determines which operator method is called in each case in the table.

.. _magicmethods:

Python Operator Magic Methods
--------------------------------

+-------------------------+-------------+--------------------------------------------------------------------------------+
| Method Defintion        | Operator    | Description                                                                    |
+=========================+=============+================================================================================+
| __add__(self,y)         | x + y       |  The addition of two objects. The type of *x* determines                       |
|                         |             |  which add operator is called.                                                 |
+-------------------------+-------------+--------------------------------------------------------------------------------+
| __contains__(self,y)    | y in x      | When *x* is a collection you can test to see if *y* is in it.                  |
+-------------------------+-------------+--------------------------------------------------------------------------------+
| __eq__(self,y)          | x == y      | Returns *True* or *False* depending on the values of *x* and *y*.              |
+-------------------------+-------------+--------------------------------------------------------------------------------+
| __ge__(self,y)          | x >= y      | Returns *True* or *False* depending on the values of *x* and *y*.              |
+-------------------------+-------------+--------------------------------------------------------------------------------+
| __getitem__(self,y)     | x[y]        | Returns the item at the y\ :sup:`th` position in x.                            |
+-------------------------+-------------+--------------------------------------------------------------------------------+
| __gt__(self,y)          | x > y       | Returns *True* or *False* depending on the values of *x* and *y*.              |
+-------------------------+-------------+--------------------------------------------------------------------------------+
| __hash__(self)          | hash(x)     | Returns an integral value for *x*.                                             |
+-------------------------+-------------+--------------------------------------------------------------------------------+
| __int__(self)           | int(x)      | Returns an integer representation of *x*.                                      |
+-------------------------+-------------+--------------------------------------------------------------------------------+
| __iter__(self)          | for v in x  | Returns an iterator object for the sequence *x*.                               |
+-------------------------+-------------+--------------------------------------------------------------------------------+
| __le__(self,y)          | x <= y      | Returns *True* or *False* depending on the values of *x* and *y*.              |
+-------------------------+-------------+--------------------------------------------------------------------------------+
| __len__(self)           | len(x)      | Returns the size of *x* where *x* has some length attribute.                   |
+-------------------------+-------------+--------------------------------------------------------------------------------+
| __lt__(self,y)          | x < y       | Returns *True* or *False* depending on the values of *x* and *y*.              |
+-------------------------+-------------+--------------------------------------------------------------------------------+
| __mod__(self,y)         | x % y       | Returns the value of *x* modulo *y*. This is the remainder of *x/y*.           |
+-------------------------+-------------+--------------------------------------------------------------------------------+
| __mul__(self,y)         | x * y       | Returns the product of *x* and *y*.                                            |
+-------------------------+-------------+--------------------------------------------------------------------------------+
| __ne__(self,y)          | x != y      | Returns *True* or *False* depending on the values of *x* and *y*.              |
+-------------------------+-------------+--------------------------------------------------------------------------------+
| __neg__(self)           | -x          | Returns the unary negation of *x*.                                             |
+-------------------------+-------------+--------------------------------------------------------------------------------+
| __repr__(self)          | repr(x)     | Returns a string version of x suitable to be evaluated by the *eval* function. |
+-------------------------+-------------+--------------------------------------------------------------------------------+
| __setitem__(self,i,y)   | x[i] = y    | Sets the item at the i\ :sup:`th` position in *x* to *y*.                      |
+-------------------------+-------------+--------------------------------------------------------------------------------+
| __str__(self)           | str(x)      | Return a string representation of *x* suitable for user-level interaction.     |
+-------------------------+-------------+--------------------------------------------------------------------------------+
| __sub__(self,y)         | x - y       | The difference of two objects.                                                 |
+-------------------------+-------------+--------------------------------------------------------------------------------+


The *repr(x)* and the *str(x)* operators deserve a little more explanation. Both
operators return a string represenation of *x*. The difference is that the *str*
operator should return a string that is suitable for human interaction while the
*repr* operator is called when a string representation is needed that can be
evaluated. For instance, if we wanted to define these two operators on the *Dog*
class, the *repr* method would return the string "Dog('Mesa',5,15,2004,'WOOOF')"
while the *str* operator might return just the dog's name. The *repr*
opererator, when called, will treat the string as an expression that could later
be evaluated by the *eval* function in Python whereas the *str* operator simply
returns a string for an object.



Importing Modules
++++++++++++++++++++

In Python, programs can be broken up into modules. Typically, when you write a
program in Python you are going to use code that someone else wrote. Code that
others wrote is usually provided in a module. To use a module, you import it.
There are two ways to import a module. For the drawing program we are developing
in this chapter, we want to use turtle graphics. Turtle graphics was first
developed a long time ago for a programming language called Logo. Logo was
created around 1967 so the basis for turtle graphics is pretty ancient in terms
of Computer Science. It still remains a useful way of thinking about Computer
Graphics. The idea is that a turtle is wandering a beach and as it walks around
it drags its tail in the sand leaving a trail behind it.
`All that you can do with a turtle is discussed here <https://docs.python.org/3/library/turtle.html>`_.

There are two ways to import a module in Python: the *convenient* way and the
*safe* way. Which way you choose to import code may be a personal preference,
but there are some implications about using the *convenient* method of importing
code. The convenient way to import the turtle module would be to write the
following. ::

	from turtle import *
	t = Turtle()

This is convenient, because whenever you want to use the *Turtle* class, you can
just write *Turtle* which is convenient, but not completely safe because you
then have to make sure you never use the identifier *Turtle* for anything else
in your code. In fact, there may be other identifiers that the turtle module
defines that you are unaware of that would also be identifiers you should not
use in your code. The safe way to import the turtle module would be as follows.
::

	import turtle
	t = turtle.Turtle()

While this is not quite as *convenient*, because you must precede *Turtle* with
*"turtle."*, it is *safe* because the *namespace* of your module and the turtle
module are kept separate. All identifiers in the turtle module are in the
*turtle namespace*, while the local identifiers are in the *local namespace*.
This idea of *namespaces* is an important feature of most programming languages.
It helps programmers keep from stepping on each others' toes. The rest of this
text will stick to using the safe method of importing modules.

Indentation in Python Programs
+++++++++++++++++++++++++++++++++

Indentation plays an important role in Python programs. An indented line belongs
to the line it is indented under. The *body* of a function is indented under its
function definition line. The *then* part of an *if* statement is indented under
the *if*. A *while* loop's body is indented under it. The methods of a class are
all indented under the class defintion line. All statements that are indented
the same amount and grouped together are called a *block*. It is important that
all statements within a *block* are indented exactly the same amount. If they
are not, then Python will complain about inconsistent indentation.

.. container:: figboxcenter

	.. _blockindent:

	.. figure:: images/blockindent.png

		Adjusting Indentation in Wing IDE 101

Because indentation is so important to Python, the Wing IDE 101 lets you select
a series of lines and adjust their indentation as a group, as shown in
:numref:`blockindent`. You first select the lines of the block and then press
the *tab* key to increase their indentation. To decrease the indentation of a
block you select the lines of the block and press *Shift-tab*. As you write
Python code this is a common chore and being able to adjust the indentation of a
whole block at a time is a real timesaver.


The *main* Function
++++++++++++++++++++++

Programs are typically written with many function definitions and function
calls. One function definition is written by convention in Python, usually
called the *main* function. This function contains code the program typically
executes when it is first started. The general outline of a Python program is
given in :ref:`mainfunction`.

.. _mainfunction:

Python Program Structure
----------------------------

.. code-block:: python
	:linenos:

	# Imports at the top.
	import turtle

	# other function definitions followed by the main function definition
	def main():
	    # The main code of the program goes here
	    t = turtle.Turtle()

	# this code calls the main function to get everything started. The condition in this
	# if statement evaluates to True when the module is executed by the interpreter, but
	# not when it is imported into another module.
	if __name__ == "__main__":
	    main()

The *if* statement at the end of the code in :ref:`mainfunction` is the first
code executed after the import statements. The *if* statement's condition
evaluates to *True* when the program is run as a stand-alone program. Sometimes
we write modules that we may want to import into another module. Writing this
*if* statement to call the main function makes the module execute its own main
function when it is run as a stand-alone program. When the module is imported
into another module it will not execute its main function. Later you will have
the opportunity to write a module to be imported into another module so it is a
good habit to form to always call the *main* function in this way.

Reading From a File
+++++++++++++++++++++

To begin our drawing program, let's assume that a picture is stored in a file
and we wish to read this file when the program is started. We'll assume that
each line of the file contains a drawing command and its associated data. We'll
keep it simple and stick to drawing commands that look like this in the input
file:

  * goto, x, y, width, color
  * circle, radius, width, color
  * beginfill, color
  * endfill
  * penup
  * pendown

Each line of the file will contain a record with the needed information. We can
draw a picture by providing a file with the right sequence of these commands.
The file in :ref:`singlelinerecs` contains records that describe a pickup truck.

.. _singlelinerecs:

A Text File with Single Line Records
---------------------------------------

.. code-block:: text

	beginfill, black
	circle, 20, 1, black
	endfill
	penup
	goto, 120, 0, 1, black
	pendown
	beginfill, black
	circle, 20, 1, black
	endfill
	penup
	goto, 150, 40, 1, black
	pendown
	beginfill, yellow
	goto, -30, 40, 1, black
	goto, -30, 70, 1, black
	goto, 60, 70, 1, black
	goto, 60, 100, 1, black
	goto, 90, 100, 1, black
	goto, 115, 70, 1, black
	goto, 150, 70, 1, black
	goto, 150, 40, 1, black
	endfill

To process the records in the file in :ref:`singlelinerecs`, we can write a
Python program that reads the lines of this file and does the appropriate turtle
graphics commands for each record in the file. Since each record (i.e. drawing
command) is on its own line in the file format described in
:ref:`singlelinerecs`, we can read the file by using a *for* loop to read the
lines of the file. The code of :ref:`graphicsprograma` is a program that reads
these commands and processes each record in the file, drawing the picture that
it contains.

.. _graphicsprograma:

Reading and Processing Single Line Records
--------------------------------------------

.. code-block:: python
	:linenos:

	# This imports the turtle graphics module.
	import turtle

	# The main function is where the main code of the program is written.
	def main():
	    # This line reads a line of input from the user.
	    filename = input("Please enter drawing filename: ")

	    # Create a Turtle Graphics window to draw in.
	    t = turtle.Turtle()
	    # The screen is used at the end of the program.
	    screen = t.getscreen()

	    # The next line opens the file for "r" or reading. "w" would open it for
	    # writing, and "a" would open the file to append to it (i.e. add to the
	    # end). In this program we are only interested in reading the file.
	    file = open(filename, "r")

	    # The following for loop reads the lines of the file, one at a time
	    # and executes the body of the loop once for each line of the file.
	    for line in file:

	        # The strip method strips off the newline character at the end of the line
	        # and any blanks that might be at the beginning or end of the line.
	        text = line.strip()

	        # The following line splits the text variable into its pieces.
	        # For instance, if text contained "goto, 10, 20, 1, black" then
	        # commandList will be equal to ["goto", "10", "20", "1", "black"] after
	        # splitting text.
	        commandList = text.split(",")

	        # get the drawing command
	        command = commandList[0]

	        if command == "goto":
	            # Writing float(commandList[1]) makes a float object out of the
	            # string found in commandList[1]. You can do similar conversion
	            # between types for int objects.
	            x = float(commandList[1])
	            y = float(commandList[2])
	            width = float(commandList[3])
	            color = commandList[4].strip()
	            t.width(width)
	            t.pencolor(color)
	            t.goto(x,y)
	        elif command == "circle":
	            radius = float(commandList[1])
	            width = float(commandList[2])
	            color = commandList[3].strip()
	            t.width(width)
	            t.pencolor(color)
	            t.circle(radius)
	        elif command == "beginfill":
	            color = commandList[1].strip()
	            t.fillcolor(color)
	            t.begin_fill()
	        elif command == "endfill":
	            t.end_fill()
	        elif command == "penup":
	            t.penup()
	        elif command == "pendown":
	            t.pendown()
	        else:
	            print("Unknown command found in file:",command)

	    #close the file
	    file.close()

	    #hide the turtle that we used to draw the picture.
	    t.ht()

	    # This causes the program to hold the turtle graphics window open
	    # until the mouse is clicked.
	    screen.exitonclick()
	    print("Program Execution Completed.")


	# This code calls the main function to get everything started.
	if __name__ == "__main__":
	    main()

When you have a data file where each line of the file is its own separate
record, you can process those records as we did in :ref:`graphicsprograma`. The
general pattern is to open the file, use a for loop to iterate through the file,
and have the body of the for loop process each record. The pseudo-code in
:ref:`filereadingpattern` is the abstract pattern for reading one-line records
from a file.

.. _filereadingpattern:

Pattern for Reading Single Line Records from a File
------------------------------------------------------

.. code-block:: python

	# First the file must be opened.
	file = open(filename,"r")

	# The body of the for loop is executed once for each line in the file.
	for line in file:
	    # Process each record of the file. Each record must be exactly one line of the input file.
	    # What processing a record means will be determined by the program you are writing.
	    print(line)

	# Closing the file is always a good idea, but it will be closed when your program terminates
	# if you do not close it explicitly.
	file.close()


Reading Multi-line Records from a File
++++++++++++++++++++++++++++++++++++++++

Sometimes records of a file are not one per line. Records of a file may cross
multiple lines. In that case, you can't use a *for* loop to read the file. You
need a *while* loop instead. When you use a while loop, you need to be able to
check a condition to see if you are done reading the file. But, to check the
condition you must first try to read at least a little of a record. This is a
kind of chicken and egg problem. Which came first, the chicken or the egg?
Computer programmers have a name for this problem as it relates to reading from
files. It is called the *Loop and a Half Pattern*. To use a while loop to read
from a file, we need a loop and a half. The half comes before the while loop.

Consider the program we are writing in this chapter. Let's assume that the
records of the file cross multiple lines. In fact, let's assume that we have
variable length records. That is, the records of our file consist of one to five
lines. The drawing commands will be exactly as they were before. But, instead of
all the data for a record appearing on one line, we'll put each piece of data on
its own separate line as shown in :ref:`multilinerecs`.


.. _multilinerecs:

A Text File with Multiple Line Records
----------------------------------------

.. code-block:: text

	beginfill
	black
	circle
	20
	1
	black
	endfill
	penup
	goto
	120
	0
	1
	black
	pendown
	beginfill
	black
	circle
	20
	1
	black
	endfill
	penup
	goto
	150
	40
	1
	black
	pendown
	beginfill
	yellow
	goto
	-30
	40
	1
	black
	goto
	-30
	70
	1
	black
	goto
	60
	70
	1
	black
	goto
	60
	100
	1
	black
	goto
	90
	100
	1
	black
	goto
	115
	70
	1
	black
	goto
	150
	70
	1
	black
	goto
	150
	40
	1
	black
	endfill

To read a file as shown in :ref:`multilinerecs` we write our loop and a half to
read the first line of each record and then check that line (i.e. the graphics
command) so we know how many more lines to read. The code in :ref:`recordcode`
uses a while loop to read these variable length records.

.. _recordcode:

Reading and Processing Multi-Line Records
-------------------------------------------

.. code-block:: python
	:linenos:

	import turtle

	def main():
	    filename = input("Please enter drawing filename: ")

	    t = turtle.Turtle()
	    screen = t.getscreen()

	    file = open(filename, "r")

	    # Here we have the half a loop to get things started. Reading our first
	    # graphics command here lets us determine if the file is empty or not.
	    command = file.readline().strip()

	    # If the command is empty, then there are no more commands left in the file.
	    while command != "":

	        # Now we must read the rest of the record and then process it. Because
	        # records are variable length, we'll use an if-elif to determine which
	        # type of record it is and then we'll read and process the record.

	        if command == "goto":
	            x = float(file.readline())
	            y = float(file.readline())
	            width = float(file.readline())
	            color = file.readline().strip()
	            t.width(width)
	            t.pencolor(color)
	            t.goto(x,y)
	        elif command == "circle":
	            radius = float(file.readline())
	            width = int(file.readline())
	            color = file.readline().strip()
	            t.width(width)
	            t.pencolor(color)
	            t.circle(radius)
	        elif command == "beginfill":
	            color = file.readline().strip()
	            t.fillcolor(color)
	            t.begin_fill()
	        elif command == "endfill":
	            t.end_fill()
	        elif command == "penup":
	            t.penup()
	        elif command == "pendown":
	            t.pendown()
	        else:
	            print("Unknown command found in file:",command)

	        # This is still inside the while loop. We must (attempt to) read
	        # the next command from the file. If the read succeeds, then command
	        # will not be the empty string and the loop will be repeated. If
	        # command is empty it is because there were no more commands in the
	        # file and the while loop will terminate.
	        command = file.readline().strip()


	    # close the file
	    file.close()

	    t.ht()
	    screen.exitonclick()
	    print("Program Execution Completed.")

	if __name__ == "__main__":
	    main()

When reading a file with multi-line records, a while loop is needed. Notice that
on line 13 the first line of the first record is read prior to the while loop.
For the body of the while loop to execute, the condition must be tested prior to
executing the loop. Reading a line prior to the while loop is necessary so we
can check to see if the file is empty or not. The first line of every other
record is read at the end of the while loop on line 55. This is the loop and a
half pattern. The first line of the first record is read before the while loop
while the first line of every other record is read inside the while loop. When
the condition becomes false, the while loop terminates.

The abstract pattern for reading multi-line records from a file is shown in
:ref:`multilinepattern`. There are certainly other forms of this pattern that
can be used, but memorizing this pattern is worth-while since the pattern will
work using pretty much any programming language.

.. _multilinepattern:

Pattern for Reading Multi-line Records from a File
----------------------------------------------------

.. code-block:: python
	:linenos:


	# First the file must be opened
	file = open(filename, "r")

	# Read the first line of the first record in the file. Of course, firstLine should be called
	# something that makes sense in your program.
	firstLine = file.readline().strip()

	while firstLine != "":
		# Read the rest of the record
		secondLine = file.readline().strip()
		thirdLine = file.readline().strip()
		# ...

		# Then process the record. This will be determined by the program you are writing.
		print(firstLine, secondLine, thirdLine)

		# Finally, finish the loop by reading the first line of the next record to set up for
		# the next iteration of the loop.
		firstLine = file.readline().strip()

	# It's a good idea to close the file, but it will be automatically closed when your
	# program terminates.
	file.close()


A Container Class
+++++++++++++++++++

To further enhance our drawing program we will first create a data structure to
hold all of our drawing commands. This is our first example of defining our own
class in this text so we'll go slow and provide a lot of detail about what is
happening and why. To begin let's figure out what we want to do with this
container class.

Our program will begin by creating an empty container. To do this, we'll write a
line like this. ::

	graphicsCommands = PyList()

Then, we will want to add graphics commands to our list using an append method
like this. ::

	command = GotoCommand(x, y, width, color)
	graphicsCommands.append(command)

We would also like to be able to iterate over the commands in our list. ::

	for command in graphicsCommands:
	    # draw each command on the screen using the turtle called t.
	    command.draw(t)

At this point, our container class looks a lot like a list. We are defining our
own list class to illustrate a first data structure and to motivate discussion
of how lists can be implemented efficiently in this and the next chapter.

Polymorphism
+++++++++++++++

One important concept in Object-Oriented Programming is called polymorphism. The
word *polymorphic* literally means *many forms*. As this concept is applied to
computer programming, the idea is that there can be many ways that a particular
behavior might be implemented. In relationship to our PyList container class
that we are building, the idea is that each type of graphics command will know
how to draw itself correctly. For instance, one type of graphics command is the
*GoToCommand*. When a *GoToCommand* is drawn it draws a line on the screen from
the current point to some new *(x,y)* coordinate. But, when a *CircleCommand* is
drawn, it draws a circle on the screen with a particular radius. This
*polymorphic* behavior can be defined by creating a class and draw method for
each different type of behavior. The code in :ref:`graphicscommands` is a
collection of classes that define the polymorophic behavior of the different
graphics *draw* methods. There is one class for each drawing command that will
be processed by the program.

.. _graphicscommands:

Graphics Command Classes
-------------------------

.. code-block:: python
	:linenos:

	# Each of the command classes below hold information for one of the
	# types of commands found in a graphics file. For each command there must
	# be a draw method that is given a turtle and uses the turtle to draw
	# the object. By having a draw method for each class, we can
	# polymorphically call the right draw method when traversing a sequence of
	# these commands. Polymorphism occurs when the "right" draw method gets
	# called without having to know which graphics command it is being called on.
	class GoToCommand:
	    # Here the constructor is defined with default values for width and color.
	    # This means we can construct a GoToCommand objects as GoToCommand(10,20),
	    # or GoToCommand(10,20,5), or GoToCommand(10,20,5,"yellow").
	    def __init__(self,x,y,width=1,color="black"):
	        self.x = x
	        self.y = y
	        self.color = color
	        self.width = width

	    def draw(self,turtle):
	        turtle.width(self.width)
	        turtle.pencolor(self.color)
	        turtle.goto(self.x,self.y)

	class CircleCommand:
	    def __init__(self,radius, width=1,color="black"):
	        self.radius = radius
	        self.width = width
	        self.color = color

	    def draw(self,turtle):
	        turtle.width(self.width)
	        turtle.pencolor(self.color)
	        turtle.circle(self.radius)

	class BeginFillCommand:
	    def __init__(self,color):
	        self.color = color

	    def draw(self,turtle):
	        turtle.fillcolor(self.color)
	        turtle.begin_fill()

	class EndFillCommand:
	    def __init__(self):
	        # pass is a statement placeholder and does nothing. We have nothing
	        # to initialize in this class because all we want is the polymorphic
	        # behavior of the draw method.
	        pass

	    def draw(self,turtle):
	        turtle.end_fill()

	class PenUpCommand:
	    def __init__(self):
	        pass

	    def draw(self,turtle):
	        turtle.penup()

	class PenDownCommand:
	    def __init__(self):
	        pass

	    def draw(self,turtle):
	        turtle.pendown()




The Accumulator Pattern
++++++++++++++++++++++++++

To use the different command classes that we have just defined, our program will
read the variable length records from the file as it did before using the *Loop
and a Half* pattern that we have already seen. Patterns of programming,
sometimes called *idioms*, are important in Computer Science. Once we have
learned an idiom we can apply it over and over in our programs. This is useful
to us because as we solve problems its nice to say, "Oh, yes, I can solve this
problem using that idiom". Having idioms at our fingertips frees our minds to
deal with the tougher problems we encounter while programming.

One important pattern in programming is the *Accumulator Pattern*. This pattern
is used in nearly every program we write. When using this pattern you initialize
an accumulator before a loop and then inside the loop you add to the
accumulator. For instance, the code in :ref:`sumsquares` uses the accumulator
pattern to compute the sum of the squares of 1 to 10.

.. _sumsquares:

Sum of Squares
-----------------

.. code-block:: python
	:linenos:

	# initialize the accumulator, in this case a list
	accumulator = []

	# write some kind of for loop or while loop
	for i in range(10):
	    # add to the accumulator, in this case add to the list
	    accumulator = accumulator + [i ** 2]

To complete our graphics program, we'll use the loop and a half pattern to read
the records from a file and the accumulator pattern to add a command object to
our PyList container for each record we find in the file. The code is given in
:ref:`completedgraphicsprog`.

.. _completedgraphicsprog:

A Graphics Program
---------------------

.. code-block:: python
	:linenos:

	import turtle

	# Command classes would be inserted here but are left out because they
	# were defined earlier in the chapter.

	# This is our PyList class. It holds a list of our graphics
	# commands.

	class PyList:
	    def __init__(self):
	        self.items = []

	    def append(self,item):
	        self.items = self.items + [item]

	    # if we want to iterate over this sequence, we define the special method
	    # called __iter__(self). Without this we'll get "builtins.TypeError:
	    # 'PyList' object is not iterable" if we try to write
	    # for cmd in seq:
	    # where seq is one of these sequences. The yield below will yield an
	    # element of the sequence and will suspend the execution of the for
	    # loop in the method below until the next element is needed. The ability
	    # to yield each element of the sequence as needed is called "lazy" evaluation
	    # and is very powerful. It means that we only need to provide access to as
	    # many of elements of the sequence as are necessary and no more.
	    def __iter__(self):
	        for c in self.items:
	            yield c

	def main():
	    filename = input("Please enter drawing filename: ")

	    t = turtle.Turtle()
	    screen = t.getscreen()
	    file = open(filename, "r")

	    # Create a PyList to hold the graphics commands that are
	    # read from the file.
	    graphicsCommands = PyList()

	    command = file.readline().strip()

	    while command != "":

	        # Now we must read the rest of the record and then process it. Because
	        # records are variable length, we'll use an if-elif to determine which
	        # type of record it is and then we'll read and process the record.
	        # In this program, processing the record means creating a command object
	        # using one of the classes above and then adding that object to our
	        # graphicsCommands PyList object.

	        if command == "goto":
	            x = float(file.readline())
	            y = float(file.readline())
	            width = float(file.readline())
	            color = file.readline().strip()
	            cmd = GoToCommand(x,y,width,color)

	        elif command == "circle":
	            radius = float(file.readline())
	            width = float(file.readline())
	            color = file.readline().strip()
	            cmd = CircleCommand(radius,width,color)

	        elif command == "beginfill":
	            color = file.readline().strip()
	            cmd = BeginFillCommand(color)

	        elif command == "endfill":
	            cmd = EndFillCommand()

	        elif command == "penup":
	            cmd = PenUpCommand()

	        elif command == "pendown":
	            cmd = PenDownCommand()
	        else:
	            # raising an exception will terminate the program immediately
	            # which is what we want to happen if we encounter an unknown
	            # command. The RuntimeError exception is a common exception
	            # to raise. The string will be printed when the exception is
	            # printed.
	            raise RuntimeError("Unknown Command: " + command)

	        # Finish processing the record by adding the command to the sequence.
	        graphicsCommands.append(cmd)

	        # Read one more line to set up for the next time through the loop.
	        command = file.readline().strip()

	    # This code iterates through the commands to do the drawing and
	    # demonstrates the use of the __iter(self)__ method in the
	    # PyList class above.
	    for cmd in graphicsCommands:
	        cmd.draw(t)

	    file.close()
	    t.ht()
	    screen.exitonclick()
	    print("Program Execution Completed.")

	if __name__ == "__main__":
	    main()


Implementing a GUI with Tkinter
++++++++++++++++++++++++++++++++

The word GUI means Graphical User Interface. Implementing a Graphical User
Interface in Python is very easy using a module called tkinter. The Tcl/Tk
language and toolkit was designed as a cross-platform method of creating GUI
interfaces. Python provides an interface to this toolkit via the tkinter module.

A GUI is an event-driven program. This means that you write your code to respond
to events that occur in the program. The events occur as a result of mouse
clicks, dragging the mouse, button presses, and menu items being selected.

.. container:: figboxcenter

	.. _drawpic:

	.. figure:: images/Draw800wide.png

		The Draw Program

To build a GUI you place widgets in a window. Widgets are any element of a GUI
like labels, buttons, entry boxes, and sometimes invisible widgets called
frames. A frame is a widget that can hold other widgets. The drawing application
you see in :numref:`drawpic` is one such GUI built with tkinter. In this section
we'll develop a drawing application so you learn how to create your own GUI
applications using tkinter and to improve your Python programming skills.

To construct a GUI you need to create a window. It is really very simple to do
this using tkinter. ::

	root = tkinter.Tk()

This creates an empty window on the screen, but of course does not put anything
in it. We need to place widgets in it so it looks like the window in
:numref:`drawpic` (without the nice picture that Denise drew for us; thanks
Denise!). We also need to create event handlers to handle events in the drawing
application.

Putting widgets in a window is called *layout*. Laying out a window relies on a
layout manager of some sort. Windowing toolkits support some kind of layout. In
tkinter you either *pack*, *grid*, or *place* widgets within a window. When you
*pack* widgets it's like packing a suitcase and each widget is stacked either
beside or below the previous widget packed in the GUI. Packing widgets will give
you the desired layout in most situations, but at times a *grid* may be useful
for laying out a window. The *place* layout manager lets you place widgets at a
particular location within a window. In this text, we'll use the *pack* layout
manager to layout our drawing application.

.. container:: figboxcenter

	.. _thegui:

	.. figure:: images/labelledGUI.png

		The Draw Program Layout

When packing widgets, to get the proper layout, sometimes you need to create a
Frame widget. Frame widgets hold other widgets. In :numref:`thegui` two frame
widgets have been created. The DrawingApplication frame is the size of the whole
window and holds just two widgets that are placed side by side within it: the
canvas and the sideBar frame. A canvas is a widget on which a turtle can draw.
The sideBar widget holds all the buttons, entry boxes, and labels.

The DrawingApplication frame *inherits* from Frame. When programming in an
object-oriented language, sometimes you want to implement a class, but it is
almost like another class. In this case, the *DrawingApplication* is a *Frame*.
This means there are two parts to DrawingApplication objects, the Frame part of
the DrawingApplication and the rest of it, which in this case is the *PyList*
sequence of graphics commands. Our frame will keep track of the graphics
commands that are used to draw the picture on the canvas. Portions of the code
appear in :ref:`guiapp`. The code in :ref:`guiapp` shows you all the widgets
that are created and how they are packed within the window.

The *canvas* and the *sideBar* widgets are added side by side to the
DrawingApplication frame. Then all the entry, label, and button widgets are
added to the *sideBar* frame.

In addition, there is a menu with the *Draw* application. The menu is another
widget that is added to the window (called *self.master* in the code in
:ref:`guiapp`). The *fileMenu* is what appears on the menu bar. The menu items
"New", "Load...", "Load Into...", "Save As...", and "Exit" are all added to this
menu. Each menu item is linked to an event handler that is executed when it is
selected.

When *theTurtle* object is created in :ref:`guiapp`, it is created as a
*RawTurtle*. A *RawTurtle* is just like a turtle except that a *RawTurtle* can
be provided a canvas to draw on. A *Turtle* object creates its own canvas when
the first turtle is created. Since we already have a canvas for the turtle, we
create a *RawTurtle* object.

In addition to the event handlers for the widgets, there are three other event
handlers. The *onclick* event occurs when you click the mouse button on the
canvas. The *ondrag* event handler occurs when the turtle is dragged around the
canvas. Finally, the *undoHandler* is called when the *u* key is pressed on the
keyboard.

.. _guiapp:

A GUI Drawing Application
---------------------------

.. code-block:: python
	:linenos:

	# This class defines the drawing application. The following line says that
	# the DrawingApplication class inherits from the Frame class. This means that
	# a DrawingApplication object is a Frame object with some extra information
	# and methods.
	class DrawingApplication(tkinter.Frame):
	    def __init__(self, master=None):
	        super().__init__(master)
	        self.pack()
	        self.buildWindow()
	        self.graphicsCommands = PyList()

	    # This method is called to create all the widgets, place them in the GUI,
	    # and define the event handlers for the application.
	    def buildWindow(self):

	        # The master is the root window. The title is set as below.
	        self.master.title("Draw")

	        # Here is how to create a menu bar. The tearoff=0 means that menus
	        # can't be separated from the window which is a feature of tkinter.
	        bar = tkinter.Menu(self.master)
	        fileMenu = tkinter.Menu(bar,tearoff=0)

	        # This code is called by the "New" menu item below when it is selected.
	        # The same applies for loadFile, addToFile, and saveFile below. The
	        # "Exit" menu item below calls quit on the "master" or root window.
	        def newWindow():
	            # This sets up the turtle to be ready for a new picture to be
	            # drawn. It also sets the sequence back to empty. It is necessary
	            # for the graphicsCommands sequence to be in the object (i.e.
	            # self.graphicsCommands) because otherwise the statement:
	            # graphicsCommands = PyList()
	            # would make this variable a local variable in the newWindow
	            # method. If it were local, it would not be set anymore once the
	            # newWindow method returned.
	            theTurtle.clear()
	            theTurtle.penup()
	            theTurtle.goto(0,0)
	            theTurtle.pendown()
	            screen.update()
	            screen.listen()
	            self.graphicsCommands = PyList()

	        fileMenu.add_command(label="New",command=newWindow)

	        def loadFile():

	            filename = tkinter.filedialog.askopenfilename(title="Select a Graphics File")

	            newWindow()

	            # This re-initializes the sequence for the new picture.
	            self.graphicsCommands = PyList()

	            # calling parse will read the graphics commands from the file.
	            self.graphicsCommands.parse(filename)

	            for cmd in self.graphicsCommands:
	                cmd.draw(theTurtle)

	            # This line is necessary to update the window after the picture is drawn.
	            screen.update()


	        fileMenu.add_command(label="Load...",command=loadFile)

	        def addToFile():
	            filename = tkinter.filedialog.askopenfilename(title="Select a Graphics File")

	            theTurtle.penup()
	            theTurtle.goto(0,0)
	            theTurtle.pendown()
	            theTurtle.pencolor("#000000")
	            theTurtle.fillcolor("#000000")
	            cmd = PenUpCommand()
	            self.graphicsCommands.append(cmd)
	            cmd = GoToCommand(0,0,1,"#000000")
	            self.graphicsCommands.append(cmd)
	            cmd = PenDownCommand()
	            self.graphicsCommands.append(cmd)
	            screen.update()
	            self.graphicsCommands.parse(filename)

	            for cmd in self.graphicsCommands:
	                cmd.draw(theTurtle)

	            screen.update()

	        fileMenu.add_command(label="Load Into...",command=addToFile)

	        def saveFile():
	            filename = tkinter.filedialog.asksaveasfilename(title="Save Picture As...")
	            self.graphicsCommands.write(filename)

	        fileMenu.add_command(label="Save As...",command=saveFile)


	        fileMenu.add_command(label="Exit",command=self.master.quit)

	        bar.add_cascade(label="File",menu=fileMenu)

	        # This tells the root window to display the newly created menu bar.
	        self.master.config(menu=bar)

	        # Here several widgets are created. The canvas is the drawing area on
	        # the left side of the window.
	        canvas = tkinter.Canvas(self,width=600,height=600)
	        canvas.pack(side=tkinter.LEFT)

	        # By creating a RawTurtle, we can have the turtle draw on this canvas.
	        # Otherwise, a RawTurtle and a Turtle are exactly the same.
	        theTurtle = turtle.RawTurtle(canvas)

	        # This makes the shape of the turtle a circle.
	        theTurtle.shape("circle")
	        screen = theTurtle.getscreen()

	        # This causes the application to not update the screen unless
	        # screen.update() is called. This is necessary for the ondrag event
	        # handler below. Without it, the program bombs after dragging the
	        # turtle around for a while.
	        screen.tracer(0)

	        # This is the area on the right side of the window where all the
	        # buttons, labels, and entry boxes are located. The pad creates some empty
	        # space around the side. The side puts the sideBar on the right side of the
	        # this frame. The fill tells it to fill in all space available on the right
	        # side.
	        sideBar = tkinter.Frame(self,padx=5,pady=5)
	        sideBar.pack(side=tkinter.RIGHT, fill=tkinter.BOTH)

	        # This is a label widget. Packing it puts it at the top of the sidebar.
	        widthLabel = tkinter.Label(sideBar,text="Width")
	        widthLabel.pack()

	        # This entry widget allows the user to pick a width for their lines.
	        # With the widthSize variable below you can write widthSize.get() to get
	        # the contents of the entry widget and widthSize.set(val) to set the value
	        # of the entry widget to val. Initially the widthSize is set to 1. str(1) is needed
	        # because the entry widget must be given a string.
	        widthSize = tkinter.StringVar()
	        widthEntry = tkinter.Entry(sideBar,textvariable=widthSize)
	        widthEntry.pack()
	        widthSize.set(str(1))

	        radiusLabel = tkinter.Label(sideBar,text="Radius")
	        radiusLabel.pack()
	        radiusSize = tkinter.StringVar()
	        radiusEntry = tkinter.Entry(sideBar,textvariable=radiusSize)
	        radiusSize.set(str(10))
	        radiusEntry.pack()

	        # A button widget calls an event handler when it is pressed. The circleHandler
	        # function below is the event handler when the Draw Circle button is pressed.
	        def circleHandler():
	            # When drawing, a command is created and then the command is drawn by calling
	            # the draw method. Adding the command to the graphicsCommands sequence means the
	            # application will remember the picture.
	            cmd = CircleCommand(int(radiusSize.get()), int(widthSize.get()), penColor.get())
	            cmd.draw(theTurtle)
	            self.graphicsCommands.append(cmd)

	            # These two lines are needed to update the screen and to put the focus back
	            # in the drawing canvas. This is necessary because when pressing "u" to undo,
	            # the screen must have focus to receive the key press.
	            screen.update()
	            screen.listen()

	        # This creates the button widget in the sideBar. The fill=tkinter.BOTH causes the
	        # button to expand to fill the entire width of the sideBar.
	        circleButton = tkinter.Button(sideBar, text = "Draw Circle", command=circleHandler)
	        circleButton.pack(fill=tkinter.BOTH)

	        # The color mode 255 below allows colors to be specified in RGB form (i.e. Red/
	        # Green/Blue). The mode allows the Red value to be set by a two digit hexadecimal
	        # number ranging from 00-FF. The same applies for Blue and Green values. The
	        # color choosers below return a string representing the selected color and a slice
	        # is taken to extract the #RRGGBB hexadecimal string that the color choosers return.
	        screen.colormode(255)
	        penLabel = tkinter.Label(sideBar,text="Pen Color")
	        penLabel.pack()
	        penColor = tkinter.StringVar()
	        penEntry = tkinter.Entry(sideBar,textvariable=penColor)
	        penEntry.pack()
	        # This is the color black.
	        penColor.set("#000000")

	        def getPenColor():
	            color = tkinter.colorchooser.askcolor()
	            if color != None:
	                penColor.set(str(color)[-9:-2])

	        penColorButton = tkinter.Button(sideBar, text = "Pick Pen Color", command=getPenColor)
	        penColorButton.pack(fill=tkinter.BOTH)

	        fillLabel = tkinter.Label(sideBar,text="Fill Color")
	        fillLabel.pack()
	        fillColor = tkinter.StringVar()
	        fillEntry = tkinter.Entry(sideBar,textvariable=fillColor)
	        fillEntry.pack()
	        fillColor.set("#000000")

	        def getFillColor():
	            color = tkinter.colorchooser.askcolor()
	            if color != None:
	                fillColor.set(str(color)[-9:-2])

	        fillColorButton = \
	            tkinter.Button(sideBar, text = "Pick Fill Color", command=getFillColor)
	        fillColorButton.pack(fill=tkinter.BOTH)


	        def beginFillHandler():
	            cmd = BeginFillCommand(fillColor.get())
	            cmd.draw(theTurtle)
	            self.graphicsCommands.append(cmd)

	        beginFillButton = tkinter.Button(sideBar, text = "Begin Fill", \
	                          command=beginFillHandler)
	        beginFillButton.pack(fill=tkinter.BOTH)

	        def endFillHandler():
	            cmd = EndFillCommand()
	            cmd.draw(theTurtle)
	            self.graphicsCommands.append(cmd)

	        endFillButton = tkinter.Button(sideBar, text = "End Fill", command=endFillHandler)
	        endFillButton.pack(fill=tkinter.BOTH)

	        penLabel = tkinter.Label(sideBar,text="Pen Is Down")
	        penLabel.pack()

	        def penUpHandler():
	            cmd = PenUpCommand()
	            cmd.draw(theTurtle)
	            penLabel.configure(text="Pen Is Up")
	            self.graphicsCommands.append(cmd)

	        penUpButton = tkinter.Button(sideBar, text = "Pen Up", command=penUpHandler)
	        penUpButton.pack(fill=tkinter.BOTH)

	        def penDownHandler():
	            cmd = PenDownCommand()
	            cmd.draw(theTurtle)
	            penLabel.configure(text="Pen Is Down")
	            self.graphicsCommands.append(cmd)

	        penDownButton = tkinter.Button(sideBar, text = "Pen Down", command=penDownHandler)
	        penDownButton.pack(fill=tkinter.BOTH)

	        # Here is another event handler. This one handles mouse clicks on the screen.
	        def clickHandler(x,y):
	            # When a mouse click occurs, get the widthSize entry value and set the width of the
	            # pen to the widthSize value. The int(widthSize.get()) is needed because
	            # the width is an integer, but the entry widget stores it as a string.
	            cmd = GoToCommand(x,y,int(widthSize.get()),penColor.get())
	            cmd.draw(theTurtle)
	            self.graphicsCommands.append(cmd)
	            screen.update()
	            screen.listen()

	        # Here is how we tie the clickHandler to mouse clicks.
	        screen.onclick(clickHandler)

	        def dragHandler(x,y):
	            cmd = GoToCommand(x,y,int(widthSize.get()),penColor.get())
	            cmd.draw(theTurtle)
	            self.graphicsCommands.append(cmd)
	            screen.update()
	            screen.listen()

	        theTurtle.ondrag(dragHandler)

	        # the undoHandler undoes the last command by removing it from the
	        # sequence and then redrawing the entire picture.
	        def undoHandler():
	            if len(self.graphicsCommands) > 0:
	                self.graphicsCommands.removeLast()
	                theTurtle.clear()
	                theTurtle.penup()
	                theTurtle.goto(0,0)
	                theTurtle.pendown()
	                for cmd in self.graphicsCommands:
	                    cmd.draw(theTurtle)
	                screen.update()
	                screen.listen()

	        screen.onkeypress(undoHandler, "u")
	        screen.listen()

	# The main function in our GUI program is very simple. It creates the
	# root window. Then it creates the DrawingApplication frame which creates
	# all the widgets and has the logic for the event handlers. Calling mainloop
	# on the frames makes it start listening for events. The mainloop function will
	# return when the application is exited.
	def main():
	    root = tkinter.Tk()
	    drawingApp = DrawingApplication(root)

	    drawingApp.mainloop()
	    print("Program Execution Completed.")

	if __name__ == "__main__":
	    main()


XML Files
++++++++++++

Reading a standard text file, like the graphics commands file we read using the
loop and a half pattern in :ref:`completedgraphicsprog`, is a common task in
computer programs. The only problem is that the program must be written to read
the specific format of the input file. If we later wish to change the format of
the input file to include, for example, a new option like fill color for a
circle, then we are stuck updating the program and updating all the files it
once read. The input file format and the program must always be synchronized.
This means that all old formatted input files must be converted to the new
format or they must be thrown away. That is simply not acceptable to most
businesses because data is valuable.

To deal with this problem, computer programmers designed a language for
describing data input files called XML which stands for eXtensible Markup
Language. XML is a meta-language for data description. A meta-language is a
language for describing other languages. The XML meta-language is universally
accepted. In fact, the XML format is governed by a standards committee, which
means that we can count on the XML format remaining very stable and backwards
compatible forever. Any additions to XML will have to be compatible with what
has already been defined.

An XML document begins with a special line to identify it as an XML file. This
line looks like this.

.. code-block:: xml

	<?xml version="1.0" encoding="UTF-8" standalone="no" ?>

The rest of an XML file consists of elements or nodes. Each node is identified
by a tag or a pair of beginning and ending tags. Each tag is delimited (i.e.
surrounded) by angle brackets. For instance, here is one such tag.

.. code-block:: xml

	<GraphicsCommands>

Most XML elements are delimited by a opening tag and a closing tag. The tag
above is an opening tag. Its matching closing tag looks like this.

.. code-block:: xml

	</GraphicsCommands>

The slash just before the tag name means that it is a closing tag. An opening
and closing tag may have text or other XML elements in between the two tags so
XML documents may contain XML elements nested as deeply as necessary depending
on the data you are trying to encode.

Each XML element may have attributes associated with it. For instance, consider
an XML element that encapsulates the information needed to do a *GoTo* graphics
command. To complete a *GoTo* command we need the *x* and *y* coordinates, the
*width* of the line, and the pen *color*. Here is an example of encoding that
information in XML format.

.. code-block:: xml

	<Command x="1.0" y="1.0" width="1.0" color="#000000">GoTo</Command>

In this example the attributes are *x*, *y*, *width*, and *color*. Each
attribute is mapped to its value as shown above. The *GoTo* text is the text
that appears between the opening and closing tags. That text is sometimes called
the child data.

By encoding an entire graphics commands input file in XML format we eliminate
some of the dependence between the Draw *program* and its *data*. Except for the
XML format (i.e. the grammar) the contents of the XML file are completely up to
the programmer or programmers using the data. The file in :ref:`truckxml` is an
example of the truck picture's XML input file.

.. _truckxml:

The Truck XML File
--------------------

.. code-block:: xml
	:linenos:

	<?xml version="1.0" encoding="UTF-8" standalone="no" ?>
	<GraphicsCommands>
	    <Command color="black">BeginFill</Command>
	    <Command radius="20.0" width="1" color="black">Circle</Command>
	    <Command>EndFill</Command>
	    <Command>PenUp</Command>
	    <Command x="120.0" y="0.0" width="1.0" color="black">GoTo</Command>
	    <Command>PenDown</Command>
	    <Command color="black">BeginFill</Command>
	    <Command radius="20.0" width="1" color="black">Circle</Command>
	    <Command>EndFill</Command>
	    <Command>PenUp</Command>
	    <Command x="150.0" y="40.0" width="1.0" color="black">GoTo</Command>
	    <Command>PenDown</Command>
	    <Command color="yellow">BeginFill</Command>
	    <Command x="-30.0" y="40.0" width="1.0" color="black">GoTo</Command>
	    <Command x="-30.0" y="70.0" width="1.0" color="black">GoTo</Command>
	    <Command x="60.0" y="70.0" width="1.0" color="black">GoTo</Command>
	    <Command x="60.0" y="100.0" width="1.0" color="black">GoTo</Command>
	    <Command x="90.0" y="100.0" width="1.0" color="black">GoTo</Command>
	    <Command x="115.0" y="70.0" width="1.0" color="black">GoTo</Command>
	    <Command x="150.0" y="70.0" width="1.0" color="black">GoTo</Command>
	    <Command x="150.0" y="40.0" width="1.0" color="black">GoTo</Command>
	    <Command>EndFill</Command>
	</GraphicsCommands>

XML files are text files. They just contain extra XML formatted data to help
standardize how XML files are read. Writing an XML file is as simple as writing
a text file. While indentation is not necessary in XML files, it is often used
to highlight the format of the file. In :ref:`truckxml` the *GraphicsCommands*
element contains one *Command* element for each drawing command in the picture.
Each drawing command contains the command type as its text. The command types
are *GoTo*, *Circle*, *BeginFill*, *EndFill*, *PenUp*, and *PenDown*. The
attributes of a command are data like *x*, *y*, *width*, *radius*, and *color*
that are used by the various types of commands.

To write the commands to a file, each of the Command classes can be modified to
produce an XML element when converted to a string using the special *__str__*
method. For instance, :ref:`gotoxml` contains the modified GoToCommand class
supporting the creation of an XML element.

.. _gotoxml:

The GoToCommand with XML Creation Code
-----------------------------------------

.. code-block:: python
	:linenos:

	# The following classes define the different commands that
	# are supported by the drawing application.
	class GoToCommand:
	    def __init__(self,x,y,width=1,color="black"):
	        self.x = x
	        self.y = y
	        self.width = width
	        self.color = color

	    # The draw method for each command draws the command
	    # using the given turtle
	    def draw(self,turtle):
	        turtle.width(self.width)
	        turtle.pencolor(self.color)
	        turtle.goto(self.x,self.y)

	    # The __str__ method is a special method that is called
	    # when a command is converted to a string. The string
	    # version of the command is how it appears in the graphics
	    # file format.
	    def __str__(self):
	        return '<Command x="' + str(self.x) + '" y="' + str(self.y) + '" width="' +  \
	               str(self.width) + '" color="' + self.color + '">GoTo</Command>'

By returning a string like this from each of the command objects, the code to
write the draw program's data to a file is very simple. All that is needed is
some code that writes the *xml* line as the first line, followed by the
*<GraphicsCommands>* tag and the command elements. Finally, the
*</GraphicsCommands>* tag must be written. The code in :ref:`writingxml`
accomplishes this.

.. _writingxml:

Writing Graphics Commands to an XML File
-------------------------------------------

.. code-block:: python
	:linenos:

	file = open(filename, "w")
	file.write('<?xml version="1.0" encoding="UTF-8" standalone="no" ?>\n')
	file.write('<GraphicsCommands>\n')
	for cmd in self.graphicsCommands:
	    file.write('    '+str(cmd)+"\n")

	file.write('</GraphicsCommands>\n')
	file.close()

Writing an XML file is like writing any text file except that the text file must
conform to the XML grammar specification. There are certainly ways to create XML
files that differ from how it was presented in :ref:`writingxml`. In the next
section we'll learn about XML parsers and a very simple way to read XML
documents. It turns out there are at least some XML frameworks that make writing
an XML document just as simple.

Reading XML Files
++++++++++++++++++++

XML files would be difficult to read if we had to read them like we read a
regular text file. This is especially true because XML files are not
line-oriented. They conform to the XML grammar, but the grammar does not specify
anything about the lines in the file. Instead of reading an XML file by reading
lines of the file, we use a special tool called a *parser*. A *parser* is
written according to the rules of a *grammar*, in this case the XML grammar.
There are many XML parsers that have been written and different parsers have
different features. The one we will use in this text is one of the simpler
parsers called *minidom*. The *minidom* parser reads an entire XML file by
calling the *parse* method on it. It places the entire contents of an XML file
into an sequence of *Element* objects. An *Element* object contains the child
data and attributes of an XML element along with any other elements that might
be defined inside this element.

To use the minidom parser, you must first import the module where the minidom
parser is defined. ::

	import xml.dom.minidom

Then, you can read an entire XML file by calling the *parse* method on an XML
document as follows. ::

	xmldoc = xml.dom.minidom.parse(filename)

Once you have done that, you can read a specific type of element from the XML
file by calling the method *getElementsByTagName* on it. For instance, to get
the *GraphicsCommands* element from the graphics commands XML file, you would
write this. ::

	graphicsCommands = xmldoc.getElementsByTagName("GraphicsCommands")[0]

The XML document contains the GraphicsCommands element. Calling
*getElementsByTagName* on *GraphicsCommands* returns a list of all tags that
match this tag name. Since we know there is only one of these tags in the file,
we can write *[0]* to get the first element from the list. Then, the
*graphicsCommands* element contains just the one element from the file and all
the *Command* elements of the file are located within it. If we want to go
through all these elements we can use a for loop as in the code in
:ref:`usingxmlparser`.

.. _usingxmlparser:

Using an XML Parser
----------------------

.. code-block:: python
	:linenos:

	for commandElement in graphicsCommands:
	    print(type(commandElement))
	    command = commandElement.firstChild.data.strip()
	    attr = commandElement.attributes
	    if command == "GoTo":
	        x = float(attr["x"].value)
	        y = float(attr["y"].value)
	        width = float(attr["width"].value)
	        color = attr["color"].value.strip()
	        cmd = GoToCommand(x,y,width,color)

	    elif command == "Circle":
	        radius = float(attr["radius"].value)
	        width = int(attr["width"].value)
	        color = attr["color"].value.strip()
	        cmd = CircleCommand(radius,width,color)

	    elif command == "BeginFill":
	        color = attr["color"].value.strip()
	        cmd = BeginFillCommand(color)

	    elif command == "EndFill":
	        cmd = EndFillCommand()

	    elif command == "PenUp":
	        cmd = PenUpCommand()

	    elif command == "PenDown":
	        cmd = PenDownCommand()
	    else:
	        raise RuntimeError("Unknown Command: " + command)

	    self.append(cmd)

In the code in :ref:`usingxmlparser` the *attr* variable is a dictionary mapping
the attribute *names* (i.e. keys) to their associated *values*. The child data
of a *Command* node can be found by looking at the *firstChild.data* for the
node. The *strip* method is used to strip away any unwanted blanks, tabs, or
newline characters that might appear in the string.

Chapter Summary
+++++++++++++++++

In this first chapter we have covered a large amount of material which should be
mostly review but probably covered some things that are new to you as well.
Don't be too overwhelmed by it all. The purpose of this chapter is to get you
asking questions about the things you don't understand. If you don't understand
something, you should ask your teacher or someone who knows more about
programming in Python. They can likely help you. Asking questions is a great way
to learn and Computer Science is all about a lifetime of learning.

Here is a list of the important concepts you should have learned in this chapter. You should:

 * know how to use the *Wing IDE* or a similar IDE to run and debug a program.
   If you haven't taken the time yet, watch an online video on how to use the
   Wing IDE. It will be a valuable tool for you while reading this text.

 * know how to create an *object*, both from a literal value and by calling the
   object's constructor explicitly.

 * understand the concept of a *reference* pointing at a value (i.e. an object)
   in Python.

 * know how to call a *method* on an object.

 * how to *import* a module.

 * understand the importance of *indentation* in Python programs.

 * know why you write a *main* function in Python program's and how to call the
   main function.

 * know how to read records from a file whether they be multi-line, single line,
   fixed length, or variable length records.
	
 * know how to define a *container* class like PyList defined in this chapter.

 * understand the concept of *polymporphism* and how that means an object will
   do the right thing when a method is called.

 * understand the *Accumulator* pattern and how to use it in a program.

 * know how to implement a simple GUI using tkinter in Python. Entry boxes,
   labels, buttons, frames, and event handlers should all be concepts that are
   understood and can be programmed by looking back at the examples in this
   chapter.

 * and finally you should know how to read and write XML files in your programs.

There is a lot of example code in this chapter and the final version of the
*Draw* program is
`provided here <https://kentdlee.github.io/CS2Plus/build/html/chap1/chap1.html#the-final-xml-draw-program>`_.
While it is doubtful you will be able to memorize each line of the code you
found in this chapter, you should make sure you know how things work when you
look at it and you should remember that you can use this chapter as a resource.
Come back to it often when you need to see how to do something in later
chapters. Using this example code as a reference will help to answer a lot of
your questions in future chapters.

Review Questions
++++++++++++++++++

Answer these short answer, multiple choice, and true/false questions to test
your mastery of the chapter.


 #. What does IDE stand for and why is it a good idea to use an IDE?

 #. What code would you write to create a string containing the words *Happy
    Birthday!*? Write some code to point a reference called *text* at that newly
    created object.
	
 #. What code would you write to take the string you created in the last
    question and split it into a list containing two strings? Point the reference
    *lst* at this newly created list.
	
 #. What code would you write to upper-case the string created in the second
    question. Point the reference named *bDayWish* at this upper-cased string.
	
 #. If you were to execute the code you wrote for answering the last three
    questions, what would the string referenced by *text* contain after executing
    these three lines of code?
	
 #. How would you create a dictionary that maps "Kent" to "Denise" and maps
    "Steve" to "Lindy"? In these two cases "Kent" and "Steve" are the keys and
    "Denise" and "Lindy" are the values.
	
 #. Consult
    `the dictionary reference <https://docs.python.org/3/tutorial/datastructures.html#dictionaries>`_.
    How would you map a key to a value as in the previous problem when the
    dictionary was first created as an empty dictionary? HINT: This would be called
    setting an item in the documentation in the appendix. Write a short piece of
    code to create an empty dictionary and then map "Kent" to "Denise" and "Steve"
    to "Lindy".
	
 #. What method is called when *x<y* is written? In which class is the method a
    member? In other words, if you were presented with *x<y* in a program, how
    would you figure out which class you needed to examine to understand exactly
    what *x<y* meant?
	
 #. What method is called when *x<<y* is written?
	
 #. What is the loop and a half problem and how is it solved?
	
 #. Do you need to use the solution to the loop and a half problem to read an
    XML file? Why or why not?
	
 #. Polymorphism and Operator Overloading are closely related concepts. Can you
    briefly explain how the two concepts are similar and how Python supports them?
    HINT: No is not a valid answer.
	
 #. What would you write so that a program asks the user to enter an integer and
    then adds up all the even integers from 2 to the integer entered by the user.
    HINT: You might want to review how to use the *range* function to accomplish
    this and decide on what pattern of programming you might use.
	
 #. How do you create a window using tkinter?
	
 #. What is the purpose of a Frame object in a tkinter program?
	
 #. What are three types of widgets in the tkinter framework?
	
 #. When reading an XML file, how many lines of code does it take to read the
    file?
	
 #. How do you get a single element from an XML document? What line(s) of code
    do you have to write? Provide an example.
	
 #. When traversing an XML document, how do you get a list of elements from it?
    What line(s) of code do you have to write? Provide an example.
	
 #. What is an attribute in an XML document and how do you access an attribute's
    value? Provide an example from the text or from another example you find
    online.


Programming Problems
+++++++++++++++++++++

These programming problems will give you a chance to try out the code found in this chapter and expand on those examples in one way or another.

 #. Starting with the version of the *Draw* program that reads an input file
    with variable length records, add a new graphics command of your choice to the
    program. Consider how it would be written to a file, create a test file, write
    your code, and test it. You must design two files: a sample test file, and the
    program itself. Some examples might be a graphics command to draw a star with
    some number of points, a rectangle with a height and width, etc.
	
 #. Starting with the *Draw* program
    `provided here <https://kentdlee.github.io/CS2Plus/build/html/chap1/chap1.html#the-final-xml-draw-program>`_,
    extend the program to include a new button to draw a new shape for the *Draw*
    program. For instance, have the draw program draw a star on the screen or a
    smiley face or something of your choosing. HINT: If you use forward, and back
    to draw your shape, you can scale it by multiplying each forward and back
    amount by a scale value. Then, you can let the user pick a scale for it (or use
    the radius amount as your scale) and draw your shape in whatever size you like.
    To complete this exercise you must extend your XML format to include a new
    graphics command to store the relative information for drawing your new shape.
    You must also define a new graphicsCommand class for your new shape.
	
 #. Add the ability to draw a text string on a *Draw* picture. You'll need to
    let the user pick a point size. For a real challenge, let the user pick the
    font type from a drop-down list of font types. Draw a string that you have the
    user enter in an entry box.
	
 #. Find an XML document of your choice on the internet, write code to parse
    through the data and plot something from that data whether it be some value
    over time or something else. Use turtle graphics to plot the data that you
    find.
	
 #. Add a new button to the drawing program
    `presented here <https://kentdlee.github.io/CS2Plus/build/html/chap1/chap1.html#the-final-xml-draw-program>`_
    that draws a rainbow centered above the current location of the turtle. This
    can be done quite easily by using *sin* and *cos* (i.e. sine and cosine). The
    *sin* and *cos* functions take radians as a parameter. To draw a rainbow, the
    radians would range from 0 to *math.pi* from the math module. You must import
    the *math* module to get access to *math.cos* and *math.sin* as well as
    *math.pi*. To draw values in an arc, you can use a *for loop* and let a
    variable, *i*, range from 0 to 100. Then *radius \* math.cos(i/100.0 *
    math.pi)*, *radius \* math.sin(i/100.0 * math.pi)* is the next *x,y* coordinate
    of the rainbow's arc. By varying the radius you will get several stripes for
    your rainbow. Each stripe should have a different color. To vary the color, you
    might convert a 24-bit number to hex. To convert a number to hexadecimal in
    Python you can use the *hex* function. You must make sure that your color
    string is 6 digits long and starts with a pound sign (i.e. #) for it to be a
    valid color string in Python.
