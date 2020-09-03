# Functional Programming

## What is Functional Programming?

Functional Programming is a programming paradigm, much like the Object-Oriented Programming with which many of you are familiar from CS 106B. The Functional paradigm is based on the philosophy of expressing program control flow through a series of (often nested) function calls, rather than through loops, variables, or classes.

Functional Programming is one of many programming paradigms: other paradigms include,
* Declarative Programming: in Declarative Programming, the programmer specifies the desired result and leaves it up to the computer to figure out how to obtain it.
* Object-Oriented Programming: under the Object-Oriented paradigm, the programmer defines a series of objects, and control flow is defined as a series of operations on these objects.
* Structured Programming: under the Structured paradigm, the programmer defines control flow through a series of `if/else` conditions and `while/for` loops.

The Functional programming paradigm revolves around defining control flow as a series of function calls. Functional programming, in general, avoids the idea of "state" (defined variables that change over the course of program execution), and prefers the use of "expressions" (pieces of code which may be evaluated to return a value) over "statements" (operations like `for/while`, `if/else`, etc.).

Let's quickly walk through an example of Functional programming to get a feel for the type of code which this paradigm produces. Below, we have written a Python function which takes in a list of numbers. It then finds the elements of the list which, when squared, are divisible by both 2 and 9, and returns a list consisting of those elements, each cubed.

We first write this code using the Declarative and Structured paradigms with which we are familiar:
```python
def squared_divisible_by_2_9(lst):
    ret_lst = []
    for elem in lst:
        if elem**2 % 2 == 0 and elem**2 % 9 == 0:
            ret_lst.append(elem**3)
    return ret_lst
```
Observe in the above function how we rely on state (we've set this variable `ret_list` at the start of our function, which we then build up over the course of function execution), and on statements (we use both a `for` loop and an `if` block). Below, we've rewritten the Python function to align more closely with the Functional programming paradigm:
```python
def squared_divisible_by_2_9(lst):
    return list(map(
        lambda x: x**3, 
        filter(
            lambda x: x**2 % 2 == 0 and x**2 % 9 == 0, 
            lst
        )
    ))
```
Don't panic if the code above looks unfamiliar to you - by the end of this section, writing this second version of this function should feel (almost) as natural as writing the first version. Take a moment, though, to observe the architecture of the second function: it does not use any stored function state, nor any `for` or `if` statements.

Before we dive in to discuss Python's Functional programming features, let's step back and conclude our discussion of programming paradigms. If you're interested in learning more about programming paradigms, there's a fantastic guide [here](https://cs.lmu.edu/~ray/notes/paradigms/) which provides a high-level overview of many of the most common paradigms.

It is likely the case that, in your daily programming life, you will use many different paradigms: some problems you may choose to approach with an Object-Oriented minset, while you find that other problems lend themselves more easily to a Declarative paradigm. It is also the case that programming languages tend to incline themselves more toward some paradigms than others. Query languages like SQL were designed with the Declarative paradigm in mind: specifying a SQL query is indicating to the computer the desired result (such as which data to select from a database), and the language determines how to make the appropriate data selection. As another example, C would be a poor choice of programming language for Object-Oriented programming, since it does not natively support classes: a programmer seeking to do Object-Oriented programming would be better served by a language such as Python or C++.

Python is what is called a "multi-paradigm language," meaning that it natively supports several different programming paradigms. In our discussion of Object-Oriented programming in Python, we have already seen Python's `class` objects supporting Object-Oriented programming. Similarly, Python's `if/else` and `while/for` operators support the structured programming paradigm. In this set of notes, we will explore Python's `map/filter/reduce` functions, among others, to showcase the support that Python provides for the Functonal paradigm.

## First-Class Functions - Functions are Objects!

The term "First-Class Function" refers to a function which is given the same privileges as any other object in a programming language. In Python, all functions objects, which means that all functions are first-class. Python functions, therefore, possess a type, identity, and value. In the below example, we create a sample function, then explore some of its properties.

```python
def f(x):
    return 5

id(f)      # => 4405959984
type(f)    # => <class 'function'>
print(f)   # => <function f at 0x1069d9d30>

isinstance(f, object) # => True
```

This raises some exciting questions, namely, if functions are objects, what can be done with these objects? 

Can they be operated on? Passed into other functions as arguments? _Returned_ from functions? In Python, the answer to all of these questions is _yes_, which has beautiful implications for the way in which Python supports the Functional paradigm.

## Lambda - Inline, Anonymous Functions

We will start by presenting the concept of the `lambda`. In Python, a `lambda` is an anonymous, inline function. In Python, a `lambda` is defined using the following syntax:
```python
lambda params : expression
```
Recall that an "expression" refers to a piece of code which is evaluated to return a value: the result of this expression is the return value of the `lambda`. Below, we give a simple example of defining a `lambda` function which accepts two arguments and returns the sum of their squares. 
```python
lambda x, y : x**2 + y**2
```
If we wanted to write a lambda function and immediately call it, we can do so using the standard Python syntax in which arguments are placed in parentheses after the `lambda` definition. You'll observe, however, that an extra set of parentheses are required to contain the `lambda` definition; without them, it would be ambiguous whether the `(3, 5)` were arguments to the `lambda`, or were a part of the `lambda` return expression.
```python
(lambda x, y : x**2 + y**2)(3, 5)      # => 34
```
## Iterators and Generators - Representing Infinity

One of the strengths of the Functional programming paradigm is that it allows for concrete representations of infinite-length objects. Functional programming is uniquely capable of representing infinite-length objects (in comparison with the other paradigms we have briefly discussed) due to its lack of reliance on state: in the Functional paradigm, we do not need to store every element of an infinite-dimentional list over the course of our program.

This is rather profound, so let's take a step back to evaluate what this looks like.

### Iterables - More than Just Lists!

In Python, we have seen collections of objects. Among them, we have seen lists, tuples, and dictionaries:
```python
lst = ["Parth", "Unicorns", "❤️"]
tup = ("CS41", "🦄", "🐘")
dctnry = {1 : 1, 2 : 2, 3 : "why did I think this was a useful dictionary?"}
```

All of these objects fall under the category of "iterables", which, as the name implies, are objects over which we can iterate. In its simplest form, an iterable is defined by its capability to return its elements one at a time. This means that we can apply a `for` or `while` loop over elements of these objects, and we will obtain something useful.

At a higher level of sophistication, an object of a given type is an iterable if either:
* The `__iter__()` method is defined for the type. (By "method", I am referring to a function bound to an instance of a class - for a refresher on classes and object oriented programming, check out our notes on OOP). We will discuss the behaviour of the `__iter__()` method in the following segment.
* The `__getitem__()` method and `__len__()` method are defined for the type. The `__getitem__()` method takes an integer and returns the item at that index, while the `__len__()` method returns the length of the object. For example,
  ```python
    lst.__getitem__(1) # => "Unicorns"
    tup.__getitem__(0) # => "CS41"
    lst.__len__()      # => 3
  ```

### Iterators - One Step Further

An iterator generalizes the concept of an iterable that we have seen in the previous section. Rather than representing a discrete collection of objects, such as the iterables with which we are familiar, an "iterator" represents a continuous stream of data which may be finite or infinite.

As a starting example, let's examine the `__iter__()` method which we introduced in the previous section. Let's see what happens when we call the `__iter__()` method on the `lst` we saw earlier:
```python
lst.__iter__() # => <list_iterator object at 0x104807d00>
```
Here, we see that we've created a new object of type `list_iterator`. We can create other types of iterator objects by calling the `__iter__()` method on other iterables:
```python
tup.__iter__()    # => <tuple_iterator object at 0x104807d00>
dctnry.__iter__() # => <dict_keyiterator object at 0x104887360>
```
To specifiy our earlier definition, then, an iterator enables iteration through the `__next__()` method, which must be defined for every type of iterable. The `__next__()` method, as the name implies, yields the subsequent object as we progress through our iteration. As a brief example, below, we create an iterator object, and call `__next__()` to iterate through its data stream:
```python
lst_iter = lst.__iter__()
lst_iter.__next__()       # => "Parth"
lst_iter.__next__()       # => "Unicorn"
lst_iter.__next__()       # => "❤️"
lst_iter.__next__()       # => StopIteration
```
Once we reach the end of the data from the iterator, Python raises a `StopIteration` exception to indicate that there is no more data available in the stream.

Python's builtin `next()` function is a wrapper function for the `__next__()` method: the next function takes in an object, so calling `next(obj)` is equivalent to `obj.__next__()`. Either is a perfectly acceptable way to progress through elements from an iterator's data stream.

The behaviour of an iterator is similar to that which we observe had we constructed a `for` loop over our `lst` object. In fact, we can write our own version of a `for` loop using iterators, as follows. This for loop,
```python
for elem in iterable:
    print(elem)
```
Is functionally equivalent to the following:
```python
it = iterable.__iter__()
while True:
    try:
        print(it.__next__())
    except StopIteration:
        break
```

As a subtlety, and an aside, the reader will recall that earlier, when we called `__iter__()` on a dictionary, we obtained a `dict_keyiterator`. We can then make the connectin between this name, `dict_keyiterator`, and the behaviour of a `for` loop when called on a dictionary; namely, looping over a dictionary iterates over only the keys (hence the name `dict_keyiterator`), and not the values. This is a direct result of the way in which `dict_keyiterator` is defined differently from its `list_iterator` and `tuple_iterator` counterparts.

### Generators

Until this point, we have seen iterators constructed from iterables of finite size: iterables over lists, dictionaries, and tuples. The problem with these iterables is that they require a data structure to be defined, and stored in memory, beforehand: a list is required for a `list_iterator`, for example. This poses a problem shoudl we wish to represent an unbounded stream of data.

In Python, a "generator" is a function which behaves like an iterator. Rather than a standard function, which returns a single value (or multiple values) once it is called, a generator is constructed so that, when called, it yields _the next_ term in the sequence defined by the generator.

In the abstract, this can be somewhat confusing, so let's walk through a brief example. Below, we present a generator function to produce the Fibonacci sequence:
```python
def generate_fib():
    a = 0
    b = 1
    while True:
        yield a
        a = b
        b = a + b
```
Here, we've introduced a new keyword: `yield`. We will define the `yield` keyword in the context of how a generator function is called and evaluated.

When a generator is called for the first time, say, `generate_fib()`, it returns a generator object.
```python
generator = generate_fib()
print(generator)           # => <generator object generate_fib at 0x10487e350>
```
At this point, we can treat the generator object just as we would treat any other iterator object: crucially, this generator object is defined with a `__next__()` method. When the `__next__()` method of the generator object is called, execution of the `generate_fib()` function will commence, until a `yield` statement is reached, at which point the value referenced by the `yield` will be returned to the caller, and execution of the `generate_fib()` function will pause. The next time that the `__next__()` method is called, execution of the `generate_fib()` function will resume, until a `yield` statement is reached - at that point, again, execution will pause and the value referenced by the `yield` will be returned to the caller. Reaching a `return` statement during execution of a generator function will raise a `StopIteration` exception.

This also answers the question of why our generator function contains a `while True` loop: given that the Fibonacci sequence is infinite, we would like this generator function to never return, instead preferring that it continuously yield values to the caller each time the `__next__()` method is called.

Note that the term "pause execution" genuinely does imply a pause: local variables relevant to this generator object are saved for the subsequent call. And as with any other type of object, we can have multiple generator objects based on the same generator function, and since they are separate instances of the same object, they will not interfere with one another.


Let us observe the behaviour of our generator in action:
```python
generator.__next__() # => 0
generator.__next__() # => 1
generator.__next__() # => 1
generator.__next__() # => 2
generator.__next__() # => 3
generator.__next__() # => 5
```

As we can see, this generator function produces the Fibonacci sequence, _ad infinitum_, resuming execution and generating the subsequent element with each call to the `__next__()` method.

We can loop through generators using the loop statements with which we are familiar. Using a `while` loop, we can loop through a generator in a similar manner to looping through an iterator (as in our earlier example):
```python
while True:
    try:
        print(generator.__next__())
    except StopIteration:
        break
```
Using a `for` loop, we can simplify this looping somewhat, as a `for` loop will automatically `break` when it encounters a `StopIteration` exception:
```python
for elem in generator:
    print(elem)
```

We can convert generator objects to other data structures, by calling a constructor function such as `list()` or `tuple()` on a generator object. Calling the `list()` constructor (this is without loss of generality - we could equivalently be discussing the `tuple()` constructor) on a generator object abides by something akin to the following procedure:
```python
def list(generator_object):
    lst = []
    for value in generator_object:
        lst.append(value)
    return lst
```

This works great when `generator_object` generates a sequence of finite size; if not, your computer's in for a bit of a bad day. (It will infinitely loop until the operating system ends the program since your program will have eaten all the available RAM).

## `map` and `filter` - Functional Programming Foundations

Three concepts which are fundamental to functional programming are `map` and `filter`: these functions support the transformation of arrays without relying on state.


### The `map` Function
In Python, the map function takes in two parameters, a function and an iterable, and it applies each the function to each element of that iterable. The basic syntax is:
```python
map(fn, iterable)
```

As an introductory example, let's suppose that we wish to square every element in a list. We could do so using the `map` function (and a `lambda`!) as follows:
```python
lst = [1, 2, 3]
map(lambda x : x**2, lst) # => <map object at 0x104885310>
```

Oops! What's this weird `map` object we've got going on? Where did it come from?

It turns out that `map` accepts either a finite data structure as an interable (`list`, `tuple`, etc.), or a generator object. And since Python cannot guarantee the generator object to produce a stream of data that is finite in size, the `map` function is similarly unable to guarantee return of a data structure of finite size. Instead, the `map` function circumvents this issue by returning a "map object," a generator, which yields elements of the mapped data structure through a call to the `__next__()` method. Therefore,

```python
map_obj = map(lambda x : x**2, lst)
map_obj.__next__()                  # => 1
map_obj.__next__()                  # => 4
map_obj.__next__()                  # => 9
map_obj.__next__()                  # => StopIteration
```

Of course, we can also apply the `list()` constructor (or another similar constructor) so that the output of our call to the `map` function is the same type as our input iterable, as follows:
```python
map_obj = map(lambda x : x**2, lst)
list(map_obj)                       # => [1, 4, 9]
```

### The `filter` Function
The `filter` function behaves similarly to the `map` function: it takes in two arguments, a predicate, and an iterable, and it returns only the elements of the iterable for which the predicate is `True`. The syntax is as follows:
```python
filter(predicate, iterable)
```

Here, the term "predicate" refers to an function which evaluates to either `True` or `False`.

As an introductory example, let's call the `filter` function on a list which returns only the elements of the list which are perfect squares. (As a caveat for those familiar with the CS107 material about floating point arithmetic - here, we're assuming that the floating point arithmetic works out, such that `math.sqrt(49)` always evaluates to `7.0` and not `6.9999999999`. Due to the stability of Python's `math` library, this is a pretty safe assumption, but isn't something we should always take for granted).
```python
import math
lst = [1, 3, 5, 7, 9]
filter(lambda x : math.sqrt(x) % 1 == 0, lst) # => <filter object at 0x1048853d0>

```
Above, observe that the expression `math.sqrt(x) % 1 == 0` simply checks whether the square root of the input to the lambda is a whole number. If so, the lambda will return `True`; if not, it will return `False`. The lambda we have defined, therefore, is a valid predicate.

Just like the `map` function, the `filter` function returns a filter object. As above, we can either read out the elements one-by-one, or we can cast it to a list, as below.
```python
list(
    filter(lambda x : math.sqrt(x) % 1 == 0, lst)
)                                                 # => [1, 9]
```
Observe that the elements in the list have been _filtered_ from our prior input: the only elements remaining within this new list are those which are perfect squares, as desired.

## Decorators

So far, we've done some pretty fancy things with functions! We've learned that functions are objects, and therefore, that they have identity, type, and value. Since functions are objects, we've also passed them as parameters into other functions, as we saw when we used lambdas (which are just smaller, cuter functions) to call the `map` and `filter` functions.

Now, we're going to explore one of Python's fanciest topics: decorators. A "decorator," in brief, is when we pass a function into a function to return a function.

No, the above was not a typo. But fear not - though decorators sound complicated (and they are - they're often the most difficult topic for students of CS41), this section will build up to them slowly, providing examples at each step of the way, to clearly illustrate what decorators are, how they work, and the situations in which they can be useful.

### Functions as Arguments

Let's take a quick step back, for a moment, and recall that functions can be passed as parameters to other functions. It's here that we wish to explicitly blur the line between lambdas and functions, if it was not already sufficiently blurred: lambdas _are_ functions. Any place in which we can use a lambda in Python is a place in which we can use a function defined with the standard `def` notation.

To illustrate this, below, we implement a toy version of `map`: we call it a toy version since it, unlike the standard `map` function, assumes that the input to the function is a list, and returns a list (instead of a map object).
```python
def cs41_map(fn, lst):
    return [fn(x) for x in lst]
```
Below, we define our own function operation (called `fun_polynomial`), and we call our `cs41_map` function using the function that we've just defined as an argument:
```python
def fun_polynomial(x):
    return x**2 - 3*x + 12 

cs41_map(fun_polynomial, [1, 2, 3, 4]) # => [10, 10, 12, 16]
```

So Python functions, by virtue of being objects, can be passed into functions just as if they were any other type of object. Though this shouldn't come as much of a surprise (we've been doing it with lambdas for most of this notes section), it's a core foundation on which decorators a built.

### Functions as Return Values



### Decorators

By this point, there should be two core takeaways about what it means to say the Python functions are objects:
1. Python functions can be passed into other functions as arguments.
2. Python functions can return other functions.

It shouldn't be too much of a stretch, at least conceptually, to say that in Python, we can define a function which (1) takes in another function as an argument, and which (2) returns a function. This is the essence of the Python decorator.

A "decorator" in Python is defined as any function which is used to modify a function or a class. For the purposes of these notes, we will stick to modifying functions, but it may be useful to understand that these same principles can be applied to decorate classes as well.

Let's take a look at our first decorator. This decorator is going to take in a function (denoted `fn`), and will return a function (denoted `fn_prime`). The function `fn_prime` will be identical to `fn`, with the exception that it will print out all the arguments passed into it whenever it is called. Below is the decorator for this scenario:
```python
def print_arguments(fn):
    def fn_prime(*args, **kwargs):
        print("Arguments: {}, {}".format(args, kwargs))
        fn(*args, **kwargs)
    return fn_prime
```
Let us walk through the above function step by step. We start by defining a function, `print_arguments`, which takes an arbitrary function, `fn`, as input. Within this function, we then use the standard `def` notation to construct another function, `fn_prime`. The arguments of `fn_prime` are specified by `*args` and `**kwargs` here, since we do not make any assumptions about the types of arguments that `fn` accepts. Our function `fn_prime` then does two things: first, it prints out `args` and `kwargs`, the inputs to our function `fn_prime`, then it calls `fn` with those same arguments (recall that calling `fn(*args, **kwargs)` just _unpacks_ the `args` and `kwargs` into our call of `fn`).

Finally, having constructed this new function with the desired behaviour we return it to the caller.

Feel free to re-read the above section another time: it's admittedly dense, and it combines several different concepts from the class (functions, positional arguments, keyword arguments, variadic arcuments...) in a novel, unique way.

Let's walk through a brief example of our decorator in action. Below, we define the function `foo`, decorate it with our decorator, and call it.
```python
def foo(a, b, c=1):
   return (a + b) * c

foo = print_arguments(foo)
foo(2, 1, c=3)

# Arguments: (2, 3) {'c': 1}
# 9
```

Here, the line `foo = print_arguments(foo)` redefines `foo` as the function returned from our `print_arguments` decorator. Then, calling our decorated version of `foo` both prints out the arguments passed into it, and returns the correct value.

Rather than using the line `foo = print_arguments(foo)`, we can write some Python shorthand to automatically decorate a function once it is created. To do so, we use the syntax `@decorator_name`, the line immediately before the function signature in our definition. For example, we might write,
```python
@print_arguments
def foo(a, b, c=1):
   return (a + b) * c
```
Which would have the same effect as the line assigning `foo` to its decorated version in our code above.

### Memoization - Decorators in Action!

Let's walk through one more example of decorators in action. Until this point, the example of decorators we have seen has been somewhat contrived: though printing the arguments of a function as it is called is certainly useful for debugging purposes, there are more common uses of decorators which also warrant our attention. One such example is memoization.

Let us start by defining a recursive function which, when passed in an integer `n`, returns the nth element of the Fibonacci sequence. Our function may be defined as follows:
```python
def recursive_fib(n):
    if n == 0 or n == 1:
        return n
    return recursive_fib(n-1) + recursive_fib(n-2)
```

Calling `recursive_fib(5)` is fine: any modern computer can easily resolve the stackframes required to compute such a function. Calling `recursive_fib(50)`? That's a different story - my computer _eventually_ got there, but it needed to take its time and do some serious thinking to resolve all the stackframes demanded by this function call.

The solution, as you may recall from CS106B, is to memoize the function: to store any result we have seen previously in a dictionary, and, if `recursive_fib(n)` is called on an `n` which exists as a key in our dictionary, to return its corresponding value rather than diving into the recursive function calls.

It turns out that Python decorators can be used to memoize a recursive function. Below, we present a Python decorator which takes in a function and returns a memoized version of that function (an aside: here, we assume there are no keyword arguments passed into `fn`).
```python
def memoize(fn):
    cache = {}
    def fn_prime(*args):
        if args not in cache:
            cache[args] = fn(*args)
        return cache[args]
    
    return fn_prime
```

This decorator starts by defining a cache in which to store inputs as keys, and outputs as values, for the function `fn`. We then define a new function, `fn_prime`, which performs memoization on the `fn` function: it first checks to see if the input argument is in the cache, and if so, returns it from the cache, avoiding the expensive computation which comes with evaluating many stackframes. Our decorator then returns `fn_prime`, and in so doing, our decorator returns a function which behaves akin to `fn`, except that it memoizes its output.

We can test our memoized decorator: previously, the below computations would have taken an unthinkably long time to run, but with our decorator, they can be computed in a matter of seconds.
```python
recursive_fib = memoize(recursive_fib)
recursive_fib(100)                      # => 354224848179261915075
recursive_fib(500)                      # => 139423224561697880139...
recursive_fib(1000)                     # => 434665576869374564356...
```

## Acknowledgements

The Loyola Marymount University [notes on programming paradigms](https://cs.lmu.edu/~ray/notes/paradigms/), and (as always) the [Python Language Reference](https://docs.python.org/3/reference/).

> With love, 🦄s, and 🐘s by the CS41 Staff
