# Contribution Guide
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