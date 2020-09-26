# Reading Python Documentation
If you're taking CS 41, we still have a few weeks left in the course, which will cover the Python Standard Library and Third-Party Libraries in more detail and culminate in the final project presentations (get hype!! 🥳🚀). As far as course notes are concerned, though, we wanted to leave you with a tutorial on how to teach yourself things within the Python ecosystem.

Here, we'll walk through reading documentation from the Python standard library because most third-party documentation has a similar format.


## Table of Contents
This is the link to the Python 3 standard library table of contents: <https://docs.python.org/3/library/index.html>. We've reproduced some of the table of contents below to walk through how it's structured:

> *   [Built-in Functions](https://docs.python.org/3/library/functions.html)
> *   [Built-in Types](https://docs.python.org/3/library/stdtypes.html)
>     *   [Sequence Types — `list`, `tuple`, `range`](https://docs.python.org/3/library/stdtypes.html#sequence-types-list-tuple-range)
>     *   [Text Sequence Type — `str`](https://docs.python.org/3/library/stdtypes.html#text-sequence-type-str)
> *   [Built-in Exceptions](https://docs.python.org/3/library/exceptions.html)
> *   [Text Processing Services](https://docs.python.org/3/library/text.html)
>     *   [`string` — Common string operations](https://docs.python.org/3/library/string.html)
>     *   [`re` — Regular expression operations](https://docs.python.org/3/library/re.html)
> *   [Data Types](https://docs.python.org/3/library/datatypes.html)
>     *   [`datetime` — Basic date and time types](https://docs.python.org/3/library/datetime.html)
>     *   [`heapq` — Heap queue algorithm](https://docs.python.org/3/library/heapq.html)
>     *   [`pprint` — Data pretty printer](https://docs.python.org/3/library/pprint.html)
> *   [File and Directory Access](https://docs.python.org/3/library/filesys.html)
>     *   [`pathlib` — Object-oriented filesystem paths](https://docs.python.org/3/library/pathlib.html)
> *   [Data Persistence](https://docs.python.org/3/library/persistence.html)
>     *   [`pickle` — Python object serialization](https://docs.python.org/3/library/pickle.html)
> *   [Concurrent Execution](https://docs.python.org/3/library/concurrency.html)
>     *   [`threading` — Thread-based parallelism](https://docs.python.org/3/library/threading.html)
>     *   [`multiprocessing` — Process-based parallelism](https://docs.python.org/3/library/multiprocessing.html)
> *   [Internet Data Handling](https://docs.python.org/3/library/netdata.html)
>     *   [`json` — JSON encoder and decoder](https://docs.python.org/3/library/json.html)

At the top-level of the above list, you can find categories like "Data Persistence." Within those categories are Python libraries about that topic. For example, under "Data Persistence" is the library `pickle`, which allows you to store many Python objects onto your computer's hard drive.

## The `pickle` Module
Let's take a closer look at the `pickle` module, whose documentation is hosted at <https://docs.python.org/3/library/pickle.html>.

If you're reading about this module for the first time, you should start with the introduction which usually describes the module at a high level. In this case, the introduction is:

> The pickle module implements binary protocols for serializing and de-serializing a Python object structure. "Pickling" is the process whereby a Python object hierarchy is converted into a byte stream, and "unpickling" is the inverse operation, whereby a byte stream (from a binary file or bytes-like object) is converted back into an object hierarchy. Pickling (and unpickling) is alternatively known as "serialization", "marshalling," or "flattening"; however, to avoid confusion, the terms used here are "pickling" and "unpickling".

Then, you should glance at the table of contents for this module, which lives in the left-hand collapsible bar. In this case, it looks like this: 

> *   [`pickle` — Python object serialization](https://docs.python.org/3/library/pickle.html#)
>     *   [Relationship to other Python modules](https://docs.python.org/3/library/pickle.html#relationship-to-other-python-modules)
>         *   [Comparison with `marshal`](https://docs.python.org/3/library/pickle.html#comparison-with-marshal)
>         *   [Comparison with `json`](https://docs.python.org/3/library/pickle.html#comparison-with-json)
>     *   [Data stream format](https://docs.python.org/3/library/pickle.html#data-stream-format)
>     *   [Module Interface](https://docs.python.org/3/library/pickle.html#module-interface)
>     *   [What can be pickled and unpickled?](https://docs.python.org/3/library/pickle.html#what-can-be-pickled-and-unpickled)
>     *   [Pickling Class Instances](https://docs.python.org/3/library/pickle.html#pickling-class-instances)
>         *   [Persistence of External Objects](https://docs.python.org/3/library/pickle.html#persistence-of-external-objects)
>         *   [Dispatch Tables](https://docs.python.org/3/library/pickle.html#dispatch-tables)
>         *   [Handling Stateful Objects](https://docs.python.org/3/library/pickle.html#handling-stateful-objects)
>     *   [Custom Reduction for Types, Functions, and Other Objects](https://docs.python.org/3/library/pickle.html#custom-reduction-for-types-functions-and-other-objects)
>     *   [Out-of-band Buffers](https://docs.python.org/3/library/pickle.html#out-of-band-buffers)
>         *   [Provider API](https://docs.python.org/3/library/pickle.html#provider-api)
>         *   [Consumer API](https://docs.python.org/3/library/pickle.html#consumer-api)
>         *   [Example](https://docs.python.org/3/library/pickle.html#example)
>     *   [Restricting Globals](https://docs.python.org/3/library/pickle.html#restricting-globals)
>     *   [Performance](https://docs.python.org/3/library/pickle.html#performance)
>     *   [Examples](https://docs.python.org/3/library/pickle.html#examples)

Many of these sections are unique to `pickle`, which is a fairly sophisticated library. Let's jump to the "Module Interface" section which describes the exports of this module in the standard format.

This section (and most Python documentation) is ordered by indentation. The module exports are aligned to the left of the page, and indentation levels are used to nest descriptions. For example, this is the documentation for `pickle.dumps`:

<blockquote>
<code>pickle.<b>dumps</b>(<i>obj, protocol=None, *, fix_imports=True, buffer_callback=None</i>)</code>
<div style="margin-left: 30px;">
Return the pickled representation of the object <i>obj</i> as a <a href="https://docs.python.org/3/library/stdtypes.html#bytes">bytes</a> object, instead of writing it to a file.

Arguments <i>protocol</i>, <i>fix_imports</i> and <i>buffer_callback</i> have the same meaning as in the <a href="https://docs.python.org/3/library/pickle.html#pickle.Pickler">Pickler</a> constructor.

<i>Changed in version 3.8</i>: The <i>buffer_callback</i> argument was added.
</div>
</blockquote>

The name of the function is depicted in bold, and the function signature is reproduced in detail to show which arguments are required/optional and positional/keyword. In the above example, `obj` is the only required argument.

Then, there's an indented description of the function which describes what the function does. This description will refer to parameters in italics and should explicitly say when the function returns something and what the type of that object will be.

Finally, for objects that have their own attributes (like classes and instances), the documentation will typically display these with additional levels of indentation. As a template:

<blockquote>
<code>library.<b>ClassName</b>(<i>...parameters...</i>)</code>
<div style="margin-left: 30px;">
A description of the class and parameters, at a high level.
<br /><br />
<code><b>method_name</b>(self, <i>...parameters...</i>)</code>
<div style="margin-left: 30px;">
A description of the method and its parameters.
</div>
</div>
</blockquote>

If a class has an attribute that has its own attributes, the indentation can continue further.

# List of Useful Third Party Packages

Below, we've compiled a list of third party packages that we've found useful, along with a brief description of each and the link to the documentation. Hopefully you'll find these packages helpful in your Python projects!

## Numerical Computing, Machine Learning
* `numpy` ([documentation](https://numpy.org/doc/)) - `numpy` provides a series of numerical computing tools. `numpy` provides an n-dimensional array object, as well as (fast) linear-algebraic operations on `numpy` arrays, statistical operations, and random simulation.
* `scipy` ([documentation](https://docs.scipy.org/doc/scipy/reference/)) - `scipy` also provides numerical computing tools, specifically, it contains function implementations for numerical integration, interpolation, optimization, linear algebra, and statistics.
* `matplotlib` ([documentation](https://matplotlib.org/contents.html)) - `matplotlib` provides tools for the easy creation of data plots in Python.
* `tensorflow` ([documentation](https://www.tensorflow.org/guide)) - `tensorflow` is Google's open-source machine learning package. It contains tools to easily create, train, and test machine learning models.
* `pytorch` ([documentation](https://pytorch.org/docs/stable/index.html)) - `pytorch` is another open-source machine learning package, primarily designed for deep learning. It's similar to `tenosrflow` in that it provides tools to create, train, and test machine learning models.
* `scikit-learn` ([documentation](https://scikit-learn.org/stable/user_guide.html)) - `scikit-learn` is (yet another) machine learning package. It provides out-of-the-box implementations of classical machine learning models (KNN, SVM, random forest, etc.) as well as a multi-layered perceptron for regression and classification tasks.
* `keras` ([documentation](https://keras.io/api/)) - `keras` is a deep learning package built on top of `tensorflow`, that makes it easier to design and train deep learning models.
* `nltk` ([documentation](https://www.nltk.org)) - `nltk` is a natural language processing package, which provides access to lexicons and corpora, as well as libraries for classification, tokenization, parsing, and other tasks.
* `cvxpy` ([documentation](https://www.cvxpy.org)) - `cvxpy` is the Boyd Lab's convex optimization package, which implements standard optimization algorithms to automatically optimize convex problems.
* `pandas` ([documentation](https://pandas.pydata.org/docs/)) - `pandas` is a data manipulation library. Through its `DataFrame` class, it allows for the easy processing, reading/writing, and transformation of various types of data.

## Python & The Web
* `django` ([documentation](https://docs.djangoproject.com/en/3.1/)) - `django` is an industrial-strength framework in Python for building web applications.
* `beautifulsoup` ([documentation](https://www.crummy.com/software/BeautifulSoup/bs4/doc/)) - `BeautifulSoup` is an HTML-parsing library in Python for web scraping.

## Cryptography
* `pyca`/`cryptography` ([documentation](https://cryptography.io/en/latest/)) - `pyca`/`cryptography` is a package which provides an interface to cryptographic function implementations, such as symmetric ciphers, message digests, and key derivation functions.

## Game Programming
* `pygame` ([documentation](https://www.pygame.org/docs/)) - `pygame` is a collection of modules which enable developers to write video games in Python.


> With love, 🦄s, and 🐘s by the CS41 Staff