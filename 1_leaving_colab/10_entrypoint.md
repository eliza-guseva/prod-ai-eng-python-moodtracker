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

### Step 2: Test Your Application

**Save the file** and run it from your terminal:

```bash
# Make sure you're in the mood-tracker directory
pwd

# Run your application
python mood_logger.py
```

**You should see comprehensive help output.** If not:

- **Check you're in the right directory**: `pwd` should show mood-tracker
- **Check Python works**: `python --version` should show 3.12+
- **Check the filename**: Make sure you saved as `mood_logger.py`

**Congratulations!** You just built your first standalone Python application with professional help documentation.