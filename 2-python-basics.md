# Python Basics

## String Redux

### Special Characters

Python strings, as we have seen previously, are defined by either double quotes (`"`) or single quotes (`'`). If a string is defined by double quotes, single quotes may be used within the string without terminating the string; the converse also holds, that if the string is defined by single quotes, double quotes may be used without terminating the string.

```python
print("I'm dancing.")              # => I'm dancing.
print('"This is fun!" he cried.')  # => "This is fun!"
```
However, if a string is defined by single quotes, and it is desired to use single quotes within the string, the quotation character must be _escaped_ with a forward slash immediately prior to the character so that Python knows not to read the quotation character as a string terminator. The same applies to double quotes. Below, we've written some examples.

```python
print('I\'m dancing.')               # => I'm dancing.
print("\"This is fun!\" he cried.")  # => "This is fun!" he cried.
```

### Useful String Methods

Methods are functions which can be applied to an object of a given class. As it turns out, Python strings have a number of builtin methods which are useful for string processing operations. First, we examine a small collecton of functions built for case conversion:

```python
print("Elephants are the best.".lower())  # => elephants are the best.
print("Elephants are the best.".upper())  # => ELEPHANTS ARE THE BEST.
print("Elephants are the best.".title())  # => Elephants Are The Best.
```

Python also provides methods to check whether a string is written in a given case:
```python
print("elephants are the best.".islower())  # => True
print("ELEPHANTS ARE THE BEST.".isupper())  # => True
print("Elephants Are The Best.".istitle())  # => True
```

Python strings also contain a `strip` method - as an argument, it takes in a string of leading and trailing characters specifying the characters to be stripped from the string; if none are included, it defaults to stripping leading and trailing whitespace.

```python
print("   Elephant brains weigh up to 5.4kg.     ".strip())  # => Elephant brains weigh up to 5.4kg.
print("Elephant brains weigh up to 5.4kg.".strip("Eg.l"))    # => ephant brains weigh up to 5.4k

```

Python strings also include find/replace methods. The `find` method takes in a substring and returns the lowest index where the substring is found within the string on which the method was called. The `replace` method takes in an `old` string and a `new` string, and returns a string with all occurrences of the `old` argument replaced by the `new` argument.

```python
print("Elephants are the best.".find("are"))             # => 10
print("Mice are the best.".replace("Mice", "Elephants")) # => Elephants are the best.
```

### String Formatting

Though string formatting is often performed through the use of the `format` method, it deserves its own section since Python strings support a diverse array of formatting techniques.

At a basic level, string formatting can be completed using the `+` operator, since Python strings overload the `+` operator to perform string concatenation. (This method of string formatting generally more difficult to read, and significantly less fun to write; it also doesn't provide many of the more complex string formatting operations that may be desired - for this reason, using `+` for string formatting is generally to be avoided).

```python
score = 10
print("Parth is a " + str(score) + "/10 person.")  # => Parth is a 10/10 person.
```

Python also supports C-style string formatting - this is definitely an improvement from using the `+` operator for everything, but can get somewhat unwieldy, especially since, relative to most of the rest of Python, the C-string formatting operators are less human-readable, and less intuitive to many students.

```python
print("Parth is a %d/10 person" % (10))                   # => Parth is a 10/10 person.
print("Parth enjoys apple %.2f. (He does)." % (3.14159))  # => Parth enjoys apple 3.14. (He does).

```

But say, for example, that we wanted to print out the lecture schedule for Parth and Michael in CS 41. Since we're alternating lectures, we would need to print out something like, `"Parth, then Michael, then Parth...`, which, in C-style string formatting, reads as follows:

```python
print("%s then %s then %s then %s then %s." % ("Parth", "Michael", "Parth", "Michael", "Parth"))
```

Does it work? Sure. But is it _really_ any better than just writing out the string in standard form? Not much. This is where Python's `format` method shines: it presents complex string formatting techniques for a diverse array of cases.

In the basic case, the `format` method is run on a string where curly braces represent placeholders. Arguments passed into the `format` method are formatted into the string in the locations of the curly braces.

```python
score = 10
print("Parth is a {}/{} person.".format(score, score))  # => Parth is a 10/10 person.
```

In more advanced cases, arguments in the `format` method can be referenced by placing their location within the curly braces. To revisit our lecture schedule example, we can rewrite it as follows:

```python
print("{0} then {1} then {0} then {1} then {0}." % ("Parth", "Michael"))  # => Parth then Michael then Parth then Michael then Parth
```

The astute reader will also observe that, unlike the `+` operator, the `format` method automatically performs type conversion - we were able to pass in `10` as an integer to the `format` function, and Python automatically converted it to a string during formatting.

If we want to be extra fanct, we can also add names to our parameters, as follows:
```python
print("{taller} are taller than {shorter}.".format(taller="Elephants", shorter="ants"))  # => Elephants are taller than ants.
```

Beyond the `format` method, in Python 3.6, Python introduced f-strings, which bring the power of the `format` method into a more natural syntax. Rather than needing to pass in arguments as parameters to the `format` function, using an f-string (denoted by an `f` or `F` immediately preceding the string), one can instead place the argument name between the curly braces within the string, as below:

```python
name = "Parth"
adjective = "best"
print(f"{name} is the {adjective}!")  # => Parth is the best!
```

As with the `format` method, f-strings also perform automatic type conversion.
```python
score = 10
print(f"Parth is a {score}/{score} person.")  # => Parth is a 10/10 person.
```

Generally, `format` or f-strings are the most readable, convenient string formatting techniques in Python.

## Comments

In Python, a single-line comment is denoted with the hash symbol.

```python
# This is a single-line comment.
```

Multi-line comments are placed between three single-or-double quotation marks.

```python
"""
Multi-line comments
Lie between quotations marks
This is a haiku
"""
```

## Console I/O

Console I/O in Python is provided through the `input` function. The `input` function takes in a string as a parameter, which is a prompt which it will present to the user. The user is then prompted to type in a string as a response, which the `input` function will then return. Below, we provide an example of leveraging the input function to gather input about the user's favourite animal:
```python
favourite_animal = input("What is your favourite animal? ")
```
When run, this code will prompt the user, as follows:
```
What is your favourite animal?
```
At which point, the user can enter in a response at the prompt, as follows:
```
What is your favourite animal? Elephants.
```
After the user presses `return`, the `favourite_animal` variable will now be set to the string `"Elephants."`.
```python
favourite_animal == "Elephants."  # => True
```


## File I/O

Python's approach to File I/O revolves around the _file object_. In Python, a file object can be obtained through a call to the `open` function, as follows:
```python
f = open(filename, 'r')
```
The open function takes in a file name (a string representing a path, which can either be absolute or relative), and a mode in which to open the file (this can either be `'r'` for read, `'w'` for write, `b` for binary mode; and `+` can be used to open files in multiple modes, where `r+` and `w+` both indicate to open a file for reading and writing). It returns a file object, which can be read from and written to using the following methods.

### Reading from Files
Python files can be read from using any of the following methods - note that a _line_ refers to each string of text in the file, delimited by teh newline character `\n`.
```python
file_text = f.read(size) # Reads size bytes from the file; if size is omitted, the entire file is read.
first_line = f.readline() # Reads the file one line at a time.
all_lines = f.readlines() # Returns a list with all lines of the file.
```

Alternatively, Python file objects support looping, and so the following code is valid to loop over each line of the file in succession:
```python
for line in f:
    # Do something with each line.
```

### Writing to Files

To write to a file object, Python has implemented the `write` method. It takes in a string as an argument, writes the string to the file (overwriting any data which previously existed in the file), and returns an integer of the number of bytes which have been written to the file.
```python
f.write("Contrary to popular belief, elephants are not scared of mice.")
```

After opening a file and reading from or writing to it, it's important that the file be closed to free up system resources that the open file object is using. This can be done using the `close` method, as follows:
```python
f.close()
```

To check if a file is open or closed,`closed` method returns a boolean depending on whether the file object is open or closed.
```python
f.closed  # => True if file object is closed, False otherwise.
```

### Context Management

An alternative to the `open/close` file paradigm is using a _context manager_ - the advantage of using a context manager over the `open/close` paradigm is that, if an error is thrown during execution, the context manager will ensure that the file is automatically closed. (In contrast, in the `open/close` paradigm, an error thrown before execution reaches the call to `close` will cease execution and will exit the program, potentially leaving the file open). Though it is possible to obtain the same functionality with exception handlers, context managers provide a streamlined interface to safely ensure a file is closed if an error is thrown. Context managers are created using the `with` keyword, as follows:
```python
with open(filename, 'r'):
    # Do something with the file, like read its contents - but safely this time. :)
    file_text = f.read()
```

It's almost always a better idea to use the paradigm of the context manager when performing File I/O in Python. Cases where it is superior to use the `open/close` paradiem are significantly fewer - only use it if you have a clear, good reason to do so.

## Modules

Up until this point, we have seen Python code being run in the interactive interpreter - and though the interactive interpreter is great, it's less great for code reusability. If there's a Python function which we desire to use again and again and again, what is the most effective way to do so?

Python's answer to this question is the _module_. By default, every Python file is a module. A module, broadly, consists of two parts - depending on the use case, either may be omitted without consequence beyond losing the local functionality of the omitted segment. The structure of a Python file is as follows - going forward, let's assume this file is called `hello.py`. Python files can be written in any text editor of choice - I (Michael) personally am a fan of Sublime Text and Visual Studio Code as my go-to text editors for writing `.py` files.

```python
#!/usr/bin/env python3

def do_stuff():
    # A function which does some stuff.
    print("Hello!")
    return

if __name__ == "__main__":
    # __name__ == "__main__" when a function is executed as a script.
    do_stuff()
```

The first line is called a _shebang_, and it makes sure that the file can be executed as a script - we'll revisit this more shortly.

There are three ways, then, in which modules (saved as `.py` files) can be run.

### Running Modules in the Interactive Interpreter

We can run modules in the interactive interpreter using the `-i` flag when we enter the interactive interpreter from our command line, as follows (type the command after the `$` at the command prompt in our Terminal):
```
$ python3 -i hello.py
Python 3.8.0 (v3.8.0:fa919fdf25, Oct 14 2019, 10:23:27) 
[Clang 6.0 (clang-600.0.57)] on darwin
Type "help", "copyright", "credits" or "license" for more information.
>>> 
```
This has dropped us into an interactive interpreter in which we have access to the functions we have defined in the file `hello.py`. If, for example, we wish to call the `do_stuff()` function, we may do so without re-defining it in our interactive interpreter, as follows:
```
>>> do_stuff()
Hello!
```

### Running Modules as Scripts

Earlier, we saw the `if __name__ == "__main__":` condition statement (this is often called an _if main_); this code block is entered into if the module in question is run as a script. We can run a file as a script by marking it as executable through the `chmod +x <filename>` command, then, assuming the file has a properly-defined shebang (the fancy commented line we see at the top of the Python file we wrote in the prior section), the file will execute the code within the if main as a script on the command line.

```
$ chmod +x hello.py
$ ./hello.py
Hello!
$
```

Here, we see that once we executed the file `hello.py` as a script, `Hello!` was printed to the command line, since we call the `do_stuff()` function within the if main of our file.

### Importing Functions from Modules

Python files can also be _imported_ into other Python files, in much the same way as when running modules in the interactive interpreter. The `import` statement can be used to pull functionality from one Python file into another, and can be entered both within a Python file, or at the interactive interpreter. Below, we will go through one example of each.

First, we provide an example of importing functionality at the interactive interpreter - here, it is crucial to start the interactive interpreter from the same directory as that which contains the desired import file (or, alternatively, define the file path in the import statement as a relative path from the directory in which the interactive interpreter is being run).

```
$ python3
Python 3.8.0 (v3.8.0:fa919fdf25, Oct 14 2019, 10:23:27) 
[Clang 6.0 (clang-600.0.57)] on darwin
Type "help", "copyright", "credits" or "license" for more information.
>>> import hello
```
Here, we have _imported_ the file `hello.py` into our local environment - we therefore have access to all the functions defined in that file. Therefore, we can execute the following in our interactive interpreter:
```
>>> hello.do_stuff()
Hello!
```
Here, we reference the `do_stuff()` function by writing `hello.do_stuff()`, and the function `do_stuff()` will execute just as if we had defined it within our session in the interactive interpreter.

The same behaviour holds for imports in Python files. If we write a file `nice_day.py` (we assume here, that `nice_day.py` is in the same directory as `hello.py`), we could write it as follows:
```python
# /usr/bin/env python3
import hello

def nice_day():
    print("Have a nice day!")
    return

if __name__ == "__main__":
    hello.do_stuff()
    nice_day()
```

Then, running this file as a script would yield:
```
$ ./nice_day.py
Hello!
Have a nice day!
```
As we have _imported_ the functionality from `hello.py` into the file `nice_day.py`.

Additionally, since we only intend to use one function from `hello.py` in our file `nice_day.py`, we could have written,
```python
from hello import do_stuff
```
After which we could have called the `do_stuff()` function simply as `do_stuff()`, rather than `hello.do_stuff()`.

### Python's Modules

Python has a number of builtin modules which can be imported to provide enhanced functionality. As a brief example, we will provide an example of importing the `math` module and accessing some of the functions it defines.
```python
import math

math.gcd(45, 105)  # => 15
math.cos(3.14)     # => -0.9999987317275395
math.cos(math.pi)  # => -1.0
```

Here, observe that we use the same `import` statement as we used to import the `hello.py` file. Notably, unlike with the `hello.py` example, the directory in which we run this import statement is irrelevant - since the `math` module is built in to Python, Python will handle the file path automatically to bring us the `math` module when we import it.

> With ❤️ and 🐘s by @coopermj and @psarin
