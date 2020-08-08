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

## Philosophy
These notes are not a guide on how to use Python so they should generally avoid walking the reader through an implementation. That will happen in class. Instead, these notes will should explain Python's language design and philosophy.

Think "this is how Python does X" instead of "here's how to do X in Python."

## Accessibility
These notes should be written to be friendly to people using assistive technologies to access the website. In particular, make sure that the notes make sense read aloud. Introduce code blocks and images with signpost language like "The image below depicts..." or "In Python, it's valid to write...".

