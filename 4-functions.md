# Functions


## Namespaces and Scope

### Namespaces
Recall that a _namespace_ is the mechanism by which Python keeps track of which variable names correspond to which objects. Internally, Python keeps a mapping of which names correspond to which object identities (this is backed by a Python dictionary). Function execution creates a new _local symbol table_, a namespace which keeps track of local variables over the execution of the function.

Variable assignments within a function add to the local symbol table. The local symbol table is garbage collected at the conclusion of function execution, so local variables do not persist beyond the execution of a given function.

In Python, a variable reference consists of referencing a symbol table (which is backed by a dictionary) looking for a reference to the object in question. Therefore, if we have a variable `x`, taking `x + 5` would be the same as evaluating `symbol_table["x"] + 5`.

### Scope

Unlike a namespace, which is a binding of names to object references, scope refers to which namespaces, and the order in which namespaces, are referenced when a variable is requested.

Until this point, we've been rather relaxed about what constitutes a symbol tables. In Python, there are four different levels of symbol table, which are referenced in sequential order when a variable is to be referenced. If we are referencing a variable within a function, we check whether the variable name appears in any of the following namespaces, in the order below:

- Local Function Scope: is this variable local within the current function namespace?
- Enclosing Function Scope: if there is an enclosing function, does the variable exist within that namespace?
- Global Scope: does the name reference a global variable?
- Builtins: you shouldn't be naming variables that overwrite Python's builtins (`abs`, `len`, `list` - a full list is available [here](https://docs.python.org/3/library/functions.html)) in the first place, but in the event that you are, Python will check here anyways. 🙃

The first time in this sequence that Python obtains a valid namespace reference, it treats that variable as the one to be referenced. If the requested variable name lives within none of the above namespaces, Python throws a `NameError`.

Functions in Python create a new scope, because each function comes with a new local namespace. `if` statements, loops, and `try`/`catch` blocks do not create new scopes.

### Pass By Reference, or Pass By Value?

At this point, we raise the question: "does Python pass by value, or by reference?"

In fact, Python does neither - the best way to think of Python's treatment of function arguments is "pass by object-reference." Before diving into an example, we will first introduce the concept of _immutable_ and _mutable_ objects.

An object is _immutable_ if the object itself cannot be modified. Any change to the object requires the creation of a new object. Integers, for example, are immutable; so if `x` is an integer, taking `x + 1` creates a new integer object equal to `x + 1`. In Python, objects of type `int`, `float`, `long`, `complex`, `str`, and `tuple` are immutable.

A _mutable_ object, on the other hand, is an object which is modifiable. Changes to a mutable object do not require the creation of a new object. Lists, for example, are mutable; if `lst` is a list, taking `lst.append(5)` maintains the original list, but appends the element `5` to the end of the list. In Python, objects of type `list`, `set`, and `dict`, are mutable.

#### Immutable Objects as Parameters

Let's next examine how Python functions treat immutable objects when they are passed in as parameters. Consider the code block below:

```python
def increment(x):
    x = x + 1
    return

if __name__ == "__main__":
    x = 5
    increment(x)
    print(x)
```

What will get printed out? Will it be 6, or 5?

To answer this question, it helps to consider the various scopes at play, and the variables at play within each, during execution. 

On the first line of program execution (within the if main), we create a new variable `x` and set it equal to `5`. Therefore, our global symbol table is a dictionary containing `{"x" : 5}`.

On the second line of program execution, we call `increment(x)`. This process creates a new scope, which we will call the local symbol table, into which it copies a reference to `x`. In this case, our local symbol table and global symbol tables have bound the name `"x"` to the same object (which is valid), so the local symbol table contains `{"x" : 5}`, and the global symbol table also contains `{"x" : 5}`.

We then step inside the `increment` function, and evaluate the line `x = x + 1`. Here, since our parameter `x` is immutable, the evaluation of `x + 1` necessitates the creation of a new object, which in this case is equal to `6`. Then, since our expression within `increment` assigns this value equal to the name `x`, we bind `x` to that new object within the local namespace. Since this update was made inside the `increment` function, it is only reflected in the local symbol table; the global symbol table remains unchanged. By the time we return from `increment`, therefore, our local symbol table contains `{"x" : 6}`, while the global symbol table contains `{"x" : 5}`.

Then, when we subsequently call `print(x)`, since this function call is made in the global scope, we look at the `x` in the global symbol table, and we print `5`.

#### Mutable Objects as Parameters

In similar fashion, we next investigate how Python treats mutable objects when passed in as function parameters. Consider the code block below:

```python
def append_one(arr):
    arr.append(1)
    return

if __name__ == "__main__":
    arr = [3, 2]
    append_one(arr)
    print(arr)
```

This execution begins similarly to the previous example. By the end of the first line of execution, our global namespace includes `{"arr" : [3, 2]}`.

We then enter the `append_one` function, passing `arr` in as a parameter. As in the previous example, there are now two references to `arr`: one in the local namespace of the `append_one` function, and one from the global namespace. Then, since `arr` is an array (and therefore is mutable), calling the `append` operation does not create a new object as in the previous example; rather, the `append` function called on `arr` operates on the object to which `"arr"` is a reference in the local symbol table. Since there is only one list object, the _reference_ is updated, so the local symbol table reads `{"arr" : [3, 2, 1]}`, and the global symbol table reads `{"arr" : [3, 2, 1]}`, as we return from `append_one`.

Therefore, as we finish execution and print `arr`, we print `arr` as it is referenced from the global symbol table, so this code prints out `[3, 2, 1]`.

## Arguments

Python functions accept two broad categories of parameters:
- _Positional Arguments_ - when calling a function, positional arguments are referenced by their _position in the function definition_, and are arguments of the following form. When calling a function, the caller is required to provide all positional arguments to the function.

    As we see in the below example, by calling `euclidean_dist` with arguments in the order `5, 4, 3`, Python maps the arguments to the variables `x, y, z` in `euclidean_dist` definition based on the order of the arguments: so `x` becomes `5` because `5` is the first argument passed in, `y` becomes `4` because `4` is the second argument passed in, and `z` becomes `3` because `3` is the third argument passed in.
```python
def euclidean_dist(x, y, z):
    return math.sqrt(x**2 + y**2 + x**2)

if __name__ == "__main__":
    euclidean_dist(5, 4, 3)
```
- _Keyword Arguments_ - when calling a function, keyword arguments are referenced by _argument name_, and do not need to be provided in a specific order. 

    The below example presents a call to `euclidean_dist` in which we reference the arguments as keyword arguments, rather than positional arguments. You'll observe that we can call the arguments in any order.
```python
euclidean_dist(y=4, x=5, z=3)
```

When calling a function, Python enforces that positional arguments must appear in the function call before keyword arguments. In the below example, the first call to `euclidean_dist` is a valid one, whereas the second call is invalid because the keyword argument `x` appears before the positional arguments `y` and `z`. To rectify such a scenario, if we wish to reference `x` by keyword, we must also reference `y` and `z` by keyword, as in the third function call.

```python
euclidean_dist(3, 4, z=5)     # A valid call
euclidean_dist(x=5, 4, 3)     # An invalid call
euclidean_dist(x=5, y=4, z=3) # A valid call
```

### So, they're the same?

By looking at the example above, one may assume that positional and keyword arguments are the same - after all, the same function signature and definition was used for both examples. It turns out that there are two additional subcategories of Python arguments which allow for position and keyword arguments to be differentiated in the function definition:
- _Positional-Only Arguments_ - positional-pnly arguments are listed in the function signature before a `/`, and can only be referenced by their position at call-time. In the example below, we have updated `euclidean_dist` to accept two positional-only arguments, and one positional-or-keyword argument. Here, the first two calls to `euclidean_dist` are valid, whereas the third one is not since in the third call, we are attempting to use keywords to reference the positional-only arguments `x` and `y`.
```python
def euclidean_dist(x, y, /, z):
    return math.sqrt(x**2 + y**2 + x**2)

if __name__ == "__main__":
    euclidean_dist(5, 4, 3)       # A valid call
    euclidean_dist(5, 4, z=3)     # A valid call
    euclidean_dist(x=5, y=4, z=3) # Invalid call
```

- _Keyword-Only Arguments_ - in the function signature, keyword-only arguments are denoted by following a `*`, and can only be referenced by their name at call-time. We've updated the `euclidean_dist` function in the below example to accept two positional-or-keyword arguments, and one keyword-only argument. Here, the first two calls are valid, since we are referencing the argument `z` by name, rather than by position. The third call, however, is invalid, since when calling `euclidean_dist`, we are referencing `z` by its position in the function signature, rather than by the keyword to which it is bound.
```python
def euclidean_dist(x, y, *, z):
    return math.sqrt(x**2 + y**2 + x**2)

if __name__ == "__main__":
    euclidean_dist(5, 4, z=3)     # A valid call
    euclidean_dist(z=3, x=5, y=4) # A valid call
    euclidean_dist(5, 4, 3)       # Invalid call
```

## Variadic Arguments

Until this point, we have dealt only with functions that take in a fixed number of parameters. Sometimes, though, we may wish to deal with a variable number of parameters, so this section will cover Python's capabilities for doing so.

### Variadic Positional Arguments

A function can accept a variable number of positional arguments through an argument of the form `*args` (though to be clear, the name does not need to use the term "`args`" - the asterisk is what matters, so it could just as easily be `*elephants`). Assuming we're using `*args` though, this binds the name `args` in the function's local namespace to a tuple containing all the arguments passed into the function.

For example, below we have written a small function which takes in a variable number of names, then prints out a greeting for each name that was passed into the function. Below, we also include a sample function call, and indicate what it prints to the console.

```python
def greet_all(*names):
    for name in names:
        print("Hello {}!".format(name))

if __name__ == "__main__":
    greet_all("Parth", "Michael", "Sam")  # => Hello Parth!
                                          #    Hello Michael!
                                          #    Hello Sam!
```

### Variadic Keyword Arguments

A function can also accept a variable number of keyword arguments, through an argument of the form `**kwargs` (as before, the term "`kwargs`" is not required - we could just as easily use `**bananas`). An argument of this form binds the name `kwargs` in the function's local namespace to a dictionary containing a keyword-object mapping of the captured variadic keyword arguments.

```python
def favourite_animals(**kwargs):
    for name, animal in kwargs.items():
        print("{}'s favourite animal is the {}.".format(name, animal))

if __name__ == "__main__":
    favourite_animals(Michael="elephant", Parth="unicorn")  # => Michael's favourite animal is the elephant.
                                                            #    Parth's favourite animal is the unicorn.
```

## Argument Defaults
Python also permits the function author to set default argument values in the function definition. If an argument without a default value is not provided at call-time, Python will call the function using the argument's default value as the argument. (If the argument is provided, though, Python will call the function using the user-provided argument value).

In an argument signature, _arguments without default values must appear before arguments with default values_. In the below example, the function `euclidean_dist_valid` is a valid implementation of the euclidean distance operation using a default argument value, because arguments with default values follow arguments without default values in the function definition. On the other hand, the `euclidean_dist_invalid` function is not a valid implementation (it would raise a `SyntaxError`), since the arguments `x` and `y`, which do have default values, precede `z`, which does not.

```python
def euclidean_dist_valid(x, y=1, z=1):
    return math.sqrt(x**2, y**2, z**2)

def euclidean_dist_invalid(x=5, y=1, z):
    return math.sqrt(x**2, y**2, z**2)
```

## Parameter Ordering

We've spoken a lot about ordering in the prior sections - presenting rules such as how positional arguments must appear before keyword arguments, and arguments without default values must appear before arguments with default values - so this section will clarify the ordering of all argument types we have discussed in the prior sections. Below is a Python function signature for a monstrosity of a function which contains at least one of every type of argument we have discussed in the prior sections.

```python
def f(a, /, b, c=5, *d, e=2, **f)
```

Don't panic! Let's first review the arguments types that appear in this function - they're all argument types which we have previously discussed.
- `a` - since it appears before the `/`, `a` is a positional-only argument.
- `b` - since it appears after the `/`, `b` is a positional-or-keyword argument without a default value. If `a` had contained a default value (which is valid - positional-only arguments can have defaults), we would need to assign a default value to `b` as well to maintain the validity of the ordering.
- `c` - `c` is a positional-or-keyword argument with a default value.
- `d` - `d` captures excess positional arguments in a tuple.
- `e` - `e` is a keyword-only argument with a default value.
- `f` - `f` captures any additional keyword arguments in a dictionary.

## Argument Unpacking

We've already seen _argument packing_, in which, through the use of `*args` or `**kwargs`, multiple arguments are gathered together into a tuple or dictionary for the function to use. Similarly, we can perform _argument unpacking_, meaning that we can unpack a tuple or dictionary into a function as if it was a collection of argument or keyword arguments.

Unpacking a tuple into a function follows the convention of capturing positional arguments: the arguments are unpacked into the function call in the order that thy appear in the tuple. Additionally, the argument unpacking notation is the same as the positional argument packing notation (`*`), although we add this notation to the function call, rather than to the function definition. Below, we provide an example of unpacking a tuple into a function call:

```python
def product_sum(a, b, c):
    return a*(b+c)

if __name__ == "__main__":
    tup = (3, 4, 5)
    product_sum(*tup) # Equivalent to product_sum(3, 4, 5)
```

Unpacking a dictionary into a function follows the convention of capturing keyword arguments: inside the local symbol table, the key of each dictionary element becomes the argument name, and the value is the value of the argument. Dictionary unpacking uses the same `**` notation as that which is used to capture additional keyword arguments in the function signature. Below, we provide an example of unpacking a dictionary into a function call:

```python
def favourite_animals(name, animal):
    print("{}'s favourite animal is the {}.".format(name, animal))

if __name__ == "__main__":
    animals_names = {"name":"Michael", "animal":"elephant"}
    favourite_animals(**animals_names) # Equivalent to favourite_animals(name="Michael", annimal="elephant")
```
## First-Class Functions

In Python, the term _First-Class Functions_ refers to the idea that functions - like everything else in Python - are objects, possessing type, identity, and value. In the below example, we create a sample function, then explore some of its properties.

```python
def f(x):
    return 5

id(f)      # => 4405959984
type(f)    # => <class 'function'>
print(f)   # => <function f at 0x1069d9d30>

isinstance(f, object) # => True
```

This raises some exciting questions, namely, if functions are objects, what can be done with these objects?

Can they be operated on? Passed into other functions as arguments? _Returned_ from functions?

The next section of the notes - Functional Programming - will explore these questions in greater detail.

> With love, 🦄s, and 🐘s by the CS41 Staff