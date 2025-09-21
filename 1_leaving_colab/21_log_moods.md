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

# Practice
- [ ] Go ahead and create a file `src/app_logic.py`
- [ ] In it let's create a stub of a function so far -- we'll fill it later. Now we just want to make sure, that we can import the function. Add the following function to the file
```
def log_mood():
	print("Logging moods. Coming soon...")
```
- [ ] Now in you `app.py` import this function 
- [ ] Remove `show_help()` from the entrypoint block and replace it with `log_mood()`
- [ ] Ensure that you are in your project directory and run the program

### Question 1
**What do you see?


### Question 2
- [ ] In your terminal go to one directory up
- [ ] Run your app from there.
*Don't forget that if you are one directory up you have to provide to python a correct path to your app*

**What do you see?**

- import errror
- still runs