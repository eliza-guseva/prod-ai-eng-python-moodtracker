---
title: 1.10 Entrypoint
---
**Okay, let's make it actually run this time**

As we mentioned before, we need to call the `show_help` function. We of course can just type `show_help()` right below the function definition, but we aren't going to do it. Instead, we are going to type the following.

(Don't add it yet to your code)

```python
# Application entry point - this is what runs when you execute the script
if __name__ == "__main__":
    show_help()
```

Now, let's understand what we just added. To do so we have to dive briefly into Python's inner wiring.
## The wiring
When Python processes any `.py` file, it does two things:
1. **Sets built-in variables** - Python automatically creates several "magic" variables, including `__name__` that it needs for its own use.
2. **Executes all top-level code** - Any code not inside a function or class runs immediately

 Any `.py` file can be: 
 - executed  (`python app.py`)
 - imported (`import app`)
	 - Yes, you can import your own hand-written `.py` files just like you import `pandas`. You can even write better `pandas` :) 
 
`__name__` is a built-in variable that Python sets differently depending on how the file is being used.   
- **When run directly**: `python app.py` → `__name__ = "__main__"`
- **When imported**: `import app` → `__name__ = "app"` 

When we import files, we're just interested in the classes and functions inside these files. In other words, we want just the definitions, which we can then use. We **don't** want to run anything immediately.

So when we write `if __name__ == "__main__":` and put all the executable code inside that block, it will only run when we actually intend to execute the file directly.

Many languages create similar distinctions between **executable** and **importable** content. Some, like C and Go, force you to have a `main` function defined explicitly for executables. 

Python allows you to name your functions however you want, but as a tradeoff, we get to see some of the exposed inner language wiring -- all the variables and functions that begin with `__` are part of Python's internal wiring and should be handled with care.


# Practice

<br><input type="checkbox"> In your `app.py` at the end add the entrypoint block (type it in, don't copy -- it'll help you to notice the details -- really, it does)
<br><input type="checkbox"> In terminal run your app `python app.py` (make sure you are in the project directory)

### Question 1 
**What do you see?**
- a) An error message saying "module not found"
- b) The complete help text showing usage instructions, moods, intensity levels, and examples
- c) Just "MoodTracker - Track your daily emotions"
- d) Nothing - the terminal hangs

## Question 2
<br><input type="checkbox"> Let's try to follow the directions in the help: run `python app.py happy 3`
**What do you see?**
- a) An error message: "TypeError: show_help() takes 0 positional arguments but 2 were given"
- b) A confirmation message: "Logged happy with intensity 3"
- c) The same help menu again
- d) An error: "FileNotFoundError: data/mood_log.txt not found"

---

[Next: Log Moods](11_log_moods)

---
<details>
<summary><b>Answers to this lesson Practice</b></summary>

<b>Question 1 - Correct answer:</b> <p><b>b) The complete help text showing usage instructions, moods, intensity levels, and examples</b></p>
<p>When you run `python app.py`, the `if __name__ == "__main__":` block executes, which calls `show_help()`. This function prints the comprehensive help information including usage patterns, available moods, intensity levels, examples, and data storage information.</p>

<b>Question 2 - Correct answer:</b> <p><b>c) The same help menu again</b></p>
<p>When you run `python app.py happy 3`, the program still only calls `show_help()` because we haven't implemented command-line argument parsing yet. The `happy` and `3` arguments are passed to the script but ignored, so the same help menu displays. We need to add code to handle these command-line arguments to make the mood logging functionality work.</p>

</details>


