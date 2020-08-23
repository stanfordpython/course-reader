## The Python Data Model
The Python data model is built around the notion that everything in Python is an _object_, each of which possesses three attributes: identity, type, and value. We will explore these each in turn.

### Python Objects Have Identity
Each Python object has a unique identifier, which is generated once the object is created and does not change over the lifecycle of the object. In Python, the identity of each object is the memory address where it is stored. Using the `id()` function, we can obtain the identifier of the object passed into the function as an argument. For example,
```python
# Constructing some objects
>>> x = 4.5
>>> animal = "Elephant"
>>> arr = [1, 2, 3]

# Evaluating the identity of these objects using the id() function.
>>> id(x)
4520669840
>>> id(animal)
4521608048
>>> id(arr)
4521593920
```

### Python Objects Have Type
Each object in Python has a type, which determines the default operations which can be performed on the object. For example, we can obtain the length of an object of type `string` by using the `len()` function, whereas an object of type `int` would not support such an operation. We can obtain the type of an object using the `type()` function, which returns the type of the object passed in as an argument. Continuing with our example from before, we can write,
```python
>>> type(x)
<class 'float'>
>>> type(animal)
<class 'string'>
>>> type(arr)
<class 'list'>
```
### Python Objects Have Value
The _value_ of a Python object refers to the data which is contained within a particular object. In the case of an integer, the value may be `5`, in the case of a string, the value may be `"CS41"`, and in the case of a list, the value may be `["apples", "oranges", "pears"]`. The value of a Python object is most often referenced through the name of the Python object: if we have `x = 5`, and later in our code, we make reference to `x`, Python substitutes `x` in for its value in this context.

## Objects, Variables, and Namespaces

### Objects Are... Chunky?

One downside with Python's object model is that objects - even simple ones - need to store their identity, type, and value, which means that even "small" objects can take up a rather large amount of memory.

In C, an integer takes up 4 bytes. In Python, an integer takes up 28 bytes. We can check this by calling the `__sizeof__()` method on the object whose size we wish to check.
```python
>>> x = 5
>>> x.__sizeof__()
28
```

### Variables vs. Objects

Until this point, we have seen variables and objects used interchangeably. The previous code block, in fact, could equivalently have been written as follows.
```python
>>> (5).sizeof()
28
```
So what, then, is the relationship between variables and objects?

In Python, variables are _references to objects_. When an operation is performed on a variable, Python follows the reference to the object, and performs the operation on the object itself. 
