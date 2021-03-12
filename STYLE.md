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

When an expression will result in printed terminal output, this should be written using the syntax above, with the console (`>`) sign in place of the implication sign. If output takes place over multiple lines, the console sign should appear _on the first line only_, and spacing should indicate that subsequent lines are printed from the same expression, as below:

```python
exp_multiline_output()  # > Line 1 of output
                        #   Line 2 of output
                        #   Line 3 of output
```

When code is provided that interacts with the user, typed user input should be bolded and italicized. If possible, the input should indicate what the user types but, where necessary, it may be appropriate to type actions that the user performed (like "Presses Control-C"). This can be created in Markdown by using `<pre>`, `<b>`, and `<i>` tags.

For example,

<pre>
How old are you? <i><b>None of your business!</b></i>
That's not a valid age: invalid literal for int() with base 10: 'None of your business!'
How old are you? <i><b>20</b></i>
</pre>

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

