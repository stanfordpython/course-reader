# Python Basics
Welcome to CS 41! In the first two weeks of CS 41, we're going to learn how to "translate" basic programming concepts into Python and learn a bit about Python's philosophy along the way. You should already know words like "variable", "string", and "function" so we won't explain what they are in these notes — instead, we'll focus on how those concepts are represented in Python. 

## Interactive Interpreter
The interactive interpreter is one way to execute Python code. Once you've installed Python, you can start the interactive interpreter in a few ways.

### Accessing the Interactive Interpreter
<ol>
<li> Open the Terminal and start the interactive interpreter in it. On Windows, you can access this by clicking Start, typing "cmd" into the search box, and clicking on "Command Prompt". On Mac, the Terminal application is in Applications > Utilities > Terminal. You should be greeted with a blinking cursor in front of a dollar sign. Type <code>py</code> if you're on Windows or <code>python3</code> if you're on Mac. The screen should look like:

<p align="center">
  <img height="300" alt="A terminal screen with text that appears from starting the interactive interpreter." src="img/1/mac-interpreter.png" /><br />
  <i>The interactive interpreter in a terminal on my Mac computer.</i>
</p>
</li>
<li> We can also run the interactive interpreter through VS Code. Open VS Code and go to the menu. On Windows, click View > Terminal and on Mac click Terminal > New Terminal. A terminal should appear at the bottom of the screen. Type in <code>py</code> on Windows or <code>python3</code> on Mac.

<p align="center">
  <img height="300" alt="A VS Code with a terminal at the bottom containing text that appears from starting the interactive interpreter." src="img/1/vscode-interpreter.png" /><br />
  <i>The interactive interpreter in VS Code on my Mac computer.</i>
</p>
</li>
</ol>

In both of these methods, notice that just below the line where I typed <code>python3</code> starts with "Python 3.8.1 (default, ..." — it's important that you're running Python 3. If you see Python 2 on that line, you should revisit the install instructions to make sure that you have access to the latest version of Python.

For the rest of this course, we'll use screenshots from the terminal version of the intereactive interpreter, but the content should be the same as the VS Code version. 

### What is the Interactive Interpreter?
You can type any Python code into the interactive interpreter and it will execute in realtime. This is actually a big deal! If you wanted to execute code in C++, you'd have to write it, compile it, and then execute all of the commands at once. The interactive interpreter lets you execute small portions of Python code more quickly. This is especially beneficial when you're introducing a new feature to a large project and don't want to compile the entire project to test the new feature.

After the `>>>` sign, you can type any Python code, press enter, and it'll get executed. The interpreter will display the result of the code on the line below where you typed it in. For example,

<p align="center">
  <img height="300" alt="The interactive interpreter showing that 33 + 8 is 41." src="img/1/mac-interpreter-add.png" /><br />
  <i>You can add numbers in Python and in the interactive interpreter!</i>
</p>

## Variables and Types
In other languages like Java and C++, you need to tell the language a variable's type when it's declared.

```cpp
int x = 41;
```

The keyword `int` in the above line tells the compiler that `x` will hold an integer. It would be illegal to try to assign `x = "Hello world"` because `x` can only hold an integer for its entire lifetime.

That's not true in Python. Variables are just references to objects and the type information is stored on the object. In practical terms, this means that a variable can be reassigned from one object to another even if those objects have different types. Consequently, you don't need to say what the type of a variable will be when its declared in Python.

```python
x = 41
x = "Unicorns rock!"
```

The `type` function will return information about the type of an object.

```python
type(41)              # => int
type("Unicorns rock") # => str
```

You'll rarely use `type` in production Python code, but it's useful in the interactive interpreter if you need to check what the type of some object is.

## Numbers and Booleans
### Numbers
There are three numeric types in Python: `int`, `float`, and `complex`. Let's talk about the first two. Integers are whole numbers without decimal places, just like in other languages. Floating point numbers can have decimal places.

Python supports many math operations. You'll probably use all of these at some point in your Python journey:

```python
5.  # => 5 (int)
5.0 # => 5.0 (float)

1 + 8   # => 9 (int)
8 + 5.1 # => 13.1 (float)
1 - 8   # => -7 (int)

2 * 4   # => 8 (int)
2 / 3   # => 0.666666 (float)
7 // 3  # => 2 (int; integer division)

7 % 3  # => 1 (int; modulo/remainder operator)
3 ** 3 # => 27 (int; exponential operator)
```

If you have a variable `x = 40` and want to add one to the value of that variable, there are two main ways to do that.

```python
x = x + 1
```

The line `x = x + 1` might seem strange. If you read this line like it's a mathematical equation, it seems like a contradiction. The Python interpreter, though, reads this differently: Python will execute the right hand side of this expression first (`x + 1` is `40 + 1` which is `41`) and then reassign `x` to be equal to that value. Altogether, this adds one to the value of `x`.

There's a shorter way to do this in Python:

```python
x += 1
```

In fact, you can combine any mathematical operator with the equals sign, and Python will update the variable accordingly.

```python
x += 5 # => x = x + 5
x -= 3 # => x = x – 3

x *= 2  # => x = x * 2
x /= 2  # => x = x / 2
x //= 4 # => x = x // 4

x %= 3  # => x = x % 3
x **= 3 # => x = x ** 3
```

### Booleans
A boolean object is either `True` or `False`. Python uses the words `True` and `False` to represent these concepts and, under the hood, they are secretly the numbers `1` and `0` respectively.

The `not` keyword will flip a boolean from `True` to `False` or vice versa. The `and` and `or` keywords can be placed between two boolean expressions and work like you'd expect from other languages. Here's an example of how these work:

```python
not True # => False

True and False # => False
True and True  # => True

True or False  # => True
False or False # => False
```

Finally, you can compare two objects in several ways.

* `a == b` if `a` is equal to `b`.
* `a != b` if `a` is not equal to `b`.
* `a > b` if `a` is strictly greater than `b`.
* `a >= b` if `a` is greater than or equal to `b`.

You can also chain multiple comparators together and they are combined using `and`. For example,

* `a == b > c != d` means `(a == b) and (b > c) and (c != d)`

Here are some examples of comparing numbers in Python:

```python
5 == 5    # => True
1 != 100  # => True
3 > 6     # => False
4 >= 9    # => False
3 > 2 > 1 # => True (3 > 2 and 2 > 1)
```

## Strings and Lists
## String Formatting
## Control Flow
## Loops
## Functions
> With 🦄s by @psarin and @coopermj