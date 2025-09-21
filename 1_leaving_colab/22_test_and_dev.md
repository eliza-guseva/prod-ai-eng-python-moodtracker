---
title: 2.02 Developing and Testing
---

Alright, I know I've been promising to *actually* make the app work. But now, **now**, it will definitely happen! 🎯

Let's write a real `log_mood` function that actually logs moods to a file. But first, we need to talk about something important...

## The Multi-File Development Challenge

When you write functions in `.ipynb`, it's very easy to test them. You write a function, run it, re-write, re-run, re-write, re-run... you know the drill!

But when you build a Python application, your functions go to different `.py` files. If you've never written an app that consists of multiple `.py` files, it might not be exactly clear how you can make sure that the function you wrote is actually correct.

**The notebook comfort zone:**
```python
# Cell 1
def calculate_something(x):
    return x * 2 + 1

# Cell 2
result = calculate_something(5)
print(result)  # Quick test!
```

**The multi-file reality:**
```
mood-tracker/
├── app.py              # Main program
├── src/
│   └── app_logic.py    # Function lives here
└── test_data.txt       # Sample data
```

**How do you test `calculate_something()` if it's in `src/app_logic.py` but you need it in `app.py`?**

## Three Development Strategies

Here are 3 options I use in real projects. Depending on the situation, you might prefer one or another:

### 1. **Write Direct + Run Whole App** (Brave Method 💪)
- Write the function directly in the `.py` file
- Run the entire application to see if it works
- **Pros**: Forces you to think about integration early
- **Cons**: Slow feedback loop, hard to debug

### 2. **Write Direct + Import to Notebook** (Hybrid Method 🔄)
- Write the function in the `.py` file
- Import it into an `.ipynb` for testing
- **Pros**: Best of both worlds - proper structure + easy testing
- **Cons**: Need to restart notebook kernel when you change the `.py` file

### 3. **Prototype in Notebook + Copy Over** (Safe Method 🛡️)
- Write and test the function in `.ipynb` first
- Once it works, copy it to the correct `.py` file
- **Pros**: Familiar workflow, confidence before committing
- **Cons**: Extra step, potential copy-paste errors

**Today we're going with Method 3** because it feels most comfortable coming from notebooks! 🤝

## Your MoodTracker Mission

We need to replace our placeholder `log_mood()` function with real functionality. Here's what our function should do:

**Requirements:**
1. **Accept two parameters**: `mood` (string) and `intensity` (integer 1-3)
2. **Create a data folder** if it doesn't exist
3. **Save to a file**: `data/mood_log.txt`
4. **File format**: One line per mood entry, like `2024-01-15,happy,3`
5. **User feedback**: Print a confirmation message

**Example usage:**
```python
log_mood("happy", 2)
# Should print: "Logged happy (intensity 2) at 2024-01-15 14:30"
# Should save: "2024-01-15 14:30,happy,2" to data/mood_log.txt
```

# Practice

### Step 1: Prototype in Notebook

<input type="checkbox"> **Create a test notebook** in your mood-tracker folder called `test.ipynb`
<br>&nbsp;&nbsp;<input type="checkbox"> Open it in VS Code (or Jupyter if you prefer)
<br>&nbsp;&nbsp;<input type="checkbox"> Write and test your `log_mood` function there first

**Here's a starter template to get you going:**

```python
# Cell 1: Import what you need
from datetime import datetime
import os

# Cell 2: Write your function
def log_mood(mood, intensity):
    # Get current timestamp
    timestamp = datetime.now().strftime("%Y-%m-%d %H:%M")

    # Create data directory if it doesn't exist
    # Your code here...

    # Format the log entry
    # Your code here...

    # Save to file
    # Your code here...

    # Print confirmation
    print(f"Logged {mood} (intensity {intensity}) at {timestamp}")

# Cell 3: Test it!
log_mood("happy", 2)
log_mood("sad", 1)
```

<input type="checkbox"> **Test thoroughly** - try different moods and intensities
<br>&nbsp;&nbsp;<input type="checkbox"> Check that the `data/mood_log.txt` file is created correctly
<br>&nbsp;&nbsp;<input type="checkbox"> Make sure your function handles the file creation properly

### Step 2: Copy to Production

<input type="checkbox"> **Once it works perfectly in your notebook:**
<br>&nbsp;&nbsp;<input type="checkbox"> Copy your function to `src/app_logic.py` (replace the placeholder)
<br>&nbsp;&nbsp;<input type="checkbox"> Test by running `python app.py` - you should see "Logged ... at ..."
<br>&nbsp;&nbsp;<input type="checkbox"> Check that `data/mood_log.txt` was created with your test entry

## Question 1

**After implementing and testing your `log_mood` function in the notebook, what's the most important thing to verify before copying it to `src/app_logic.py`?**

a) The function name matches exactly
b) The function works with different mood/intensity combinations and creates the file correctly
c) The indentation looks right
d) The function has comments explaining every line

## Question 2

**You've copied your function to `src/app_logic.py` and run `python app.py`, but no `data/mood_log.txt` file is created. What's the most likely issue?**

a) Python doesn't have permission to create files
b) The function is working but you're looking in the wrong directory
c) You forgot to import the `os` module in `src/app_logic.py`
d) VS Code is blocking file creation

---

[Next: Command Line Arguments with Argparse](23_argparse.md)

---

<details>
<summary><b>Answers to this lesson Practice</b></summary>

<b>Question 1 - Correct answer:</b> <p><b>b) The function works with different mood/intensity combinations and creates the file correctly</b></p>
<p>The most critical verification is that your function actually works as expected with various inputs and successfully creates/writes to the data file. While proper naming and code style matter, functionality is paramount. You want to be confident that when you move the function to production, it will behave exactly as tested in your notebook environment.</p>

<b>Question 2 - Correct answer:</b> <p><b>c) You forgot to import the `os` module in `src/app_logic.py`</b></p>
<p>When you copy a function from a notebook to a `.py` file, you need to include all the imports that the function depends on. In notebooks, you might have imported `os` and `datetime` in earlier cells, but your `.py` file needs its own import statements at the top. This is a common gotcha when transitioning from notebook development to application development - forgetting to copy the dependencies along with the function.</p>

</details>
<!-- end of answers section -->