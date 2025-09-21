---
title: 2.01 Import functions
---
## Section 2. Log the moods

Okay, we created a nice helper function, but our application doesn't deliver on the promise the helper function does.

Let's write actual logic! Let's write `log_mood` function.

We are going to write this function in `src/app_logic.py`. Technically our app is small enough, that we can write all the logic in `app.py`. And generally, we should do so -- it is a good practice not to create extra complexity unless necessary.

However, real-life applications with which you'll be working, usually grow big enough to justify multiple files, directories and subdirectories. So, we are going to practice working with them.

So, let's imagine, that we wrote our `log_mood` function, put it into `src/app_logic.py`. The question is: **how do we use it from `app.py`?**

```
mood-tracker/        
├── README.md        
├── app.py
├── src/   
	├── app_logic.py          
```

## Python Import System
When we want to use code from another file, we use Python's **import system**. This is the same mechanism you use when you write `import pandas` or `import requests` - except now we're importing our own code.

### Basic Import Syntax
In our `app.py` we can write something like this:
```python
# Import a function from our own module
from src.app_logic import log_mood

# Now we can use log_mood() in this file
log_mood()
```

**This tells Python**: "Go look in the `src` folder, find the file `app_logic.py`, and bring me the `log_mood` function from it."

Notice that `src.app_logic` is a local path - Python looks for folders and files **relative to where your main script is located. **

**Watch out for these issues**:
- `from app_logic import log_mood` (missing the `src` part) - Python won't find the file
- `from src/app_logic import log_mood` (using `/` instead of `.`) - Python uses dots, not slashes
- `from ./src.app_logic import log_mood` (adding `./`) - Don't use file system notation

### Other ways to import

There are several ways to import code in Python. Each has its place depending on what you're trying to do:

**0. Import only what you need (what we do)**
```python
from src.app_logic import log_mood

# Use it like this:
log_mood()
```

**1. Import the entire module (often too verbose):**
```python
import src.app_logic

# Use it like this:
src.app_logic.log_mood()
```

**2. Import with an alias (shorter name -- easy on the eyes):**
```python
import src.app_logic as al

# Use it like this:
al.log_mood()
```

**3. Import everything (not the best  -- makes it harder to  understand the origin of a function -> harder to debug):**
```python
from src.app_logic import *
from src.something_else import *

# Use it like this:
log_mood()
# But do you know if this function came from `something_else` or from `app_logic`?
```

**Generally options 0 and 2 are preferred ones**. You'll see either of them pretty frequently.

In many teams I worked people preferred option 0. And there are good reasons for it:
- **Clear and explicit** - you can see exactly which functions come from where
- **No namespace pollution** - only brings in what you need
- **Easy to use** - `log_mood()` instead of `src.app_logic.log_mood()`

When you work in a team -- do like the team does. But for this course just do whichever version you prefer. 

# Practice
<input type="checkbox"> **Go ahead and create a file `src/app_logic.py`**
<br>&nbsp;&nbsp;<input type="checkbox"> In it let's create a stub of a function so far -- we'll fill it later. Now we just want to make sure, that we can import the function. Add the following function to the file
```
def log_mood():
	print("Logging moods. Coming soon...")
```
<input type="checkbox"> **Now in you `app.py` import this function**
<br>&nbsp;&nbsp;<input type="checkbox"> Remove `show_help()` from the entrypoint block and replace it with `log_mood()`
<br>&nbsp;&nbsp;<input type="checkbox"> Ensure that you are in your project directory and run the program

### Question 1
**What do you see?**

a) An error: "ModuleNotFoundError: No module named 'src'"
b) The text "Logging moods. Coming soon..."
c) An error: "ImportError: cannot import name 'log_mood'"
d) Nothing - the program hangs
### Question 2
<input type="checkbox"> **In your terminal go to one directory up**
<br>&nbsp;&nbsp;<input type="checkbox"> Run your app from there.
<br>&nbsp;&nbsp;*Don't forget that when you change a directory up you have to provide to python a correct path to your app*

**What do you see?**

a) An error: "ModuleNotFoundError: No module named 'src'"
b) The same "Logging moods. Coming soon..." message
c) An error: "FileNotFoundError: can't open file 'app.py'"
d) An error: "ImportError: attempted relative import with no known parent package"

---

[Next: Developing and Testing](22_test_and_dev.md)

---

<details>
<summary><b>Answers to this lesson Practice</b></summary>

<b>Question 1 - Correct answer:</b> <p><b>b) The text "Logging moods. Coming soon..."</b></p>
<p>When you run `python app.py` from your project directory, Python successfully imports the `log_mood` function from `src/app_logic.py` and executes it, displaying the placeholder message. This confirms that your import system is working correctly and Python can find your custom module.</p>

<b>Question 2 - Correct answer:</b> <p><b>b) The same "Logging moods. Coming soon..." message</b></p>
<p>When you run the script from a directory above your project (e.g., `python mood-tracker/app.py`), Python still successfully finds and imports the `src.app_logic` module <b>because the import path is relative to where the script file (`app.py`) is located</b>, not where you're running the command from. Since `app.py` and the `src` folder are in the same directory, Python can resolve the import correctly and the program runs normally, displaying the same message.</p>

</details>
<!-- end of answers section -->