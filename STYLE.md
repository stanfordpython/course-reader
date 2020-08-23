# Contribution Guide
## Explanations in Code
When possible, avoid writing commented explanations in code blocks and, instead, explain them in text and add the code block afterwards.

**BAD:**

```python
# Lists can contain elements of different types (even other lists!)
many_types = ["a", 2, 3, [4, 5]]
```

**GOOD:**

Lists can contain elements of different types (even other lists!). For example,

```python
many_types = ["a", 2, 3, [4, 5]]
```

## Code Output
The output of code should be denoted with the implication sign after a comment so that the code is valid Python. The hash sign should be separated from the end of the line with a single space unless the expression is part of a longer block in which case the hash signs for each line should be aligned so that the longest expression is separated from the hash sign by one space.

For example,

```python
expression # => return_val

expression             # => return_val
longer_expression      # => long_return_val
really_long_expression # => really_long_return_val
```

When an expression will result in printed terminal output, this should be written after the expression and a blank line. Each line of output should be commented out with the hash sign at the beginning of the line, a space, and then the terminal output. The implication sign should not be included.

For example

```python
expression_that_prints_something

# Line 1 of output
# Line 2 of output
# Line 3 of output
```

## Filenames

When indicating code that is written in a `.py` file, the following lines should appear at the top of the code block; the separating `-`s should reach exactly to the end of the `.py` extension in the filename, as below.
```python
# /usr/bin/env python3

'''
File: filename.py
-----------------
'''
```

## Images
All images should include alt text and be centered in the screen with a caption. The height should be specified and is generally 350. This can be done in Github with the following HTML code:

```md
<p align="center">
  <img height="350" alt="ALT TEXT" src="img/.../filename.png" /><br />
  <i>Caption</i>
</p>
```

## "You"
When possible, try to avoid addressing the reader using the "you" pronoun unless it significantly improves readability. 

One exception is that, because this is a course about Python, we're often suggesting best practices. In these cases it's okay to use language like "You'll rarely encounter this ..." but it's still generally better to rephrase these sentences like "This concept is rarely used in production ..."

## Terms and Definitions
When introducing new terms and definitions for the first time, they are to be written "in quotes" so that the student is aware that a new term is being introduced and defined.

## Philosophy
These notes are not a guide on how to use Python so they should generally avoid walking the reader through an implementation. That will happen in class. Instead, these notes will should explain Python's language design and philosophy.

Think "this is how Python does X" instead of "here's how to do X in Python."

## Accessibility
These notes should be written to be friendly to people using assistive technologies to access the website. In particular, make sure that the notes make sense read aloud. Introduce code blocks and images with signpost language like "The image below depicts..." or "In Python, it's valid to write...".

## Signature
All documents will be signed as
> With love, 🦄s, and 🐘s by the CS41 Staff
