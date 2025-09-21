---
title: 2.02 Developing and Testing
---
Hi there! 

I know I've been promising to *actually* make the app work. And then we went there, went here, did this and that and still no mood logging is happening =\

But now, **now**, we'll definitely do it! Pinky promise!

**However,** before that, we need to talk about something important...

## The Multi-File Development Challenge

When you write functions in `.ipynb`, it's very easy to test them. You write a function, run it, re-write, re-run, re-write, re-run, re... etc

But when you build a Python application, your functions go to different `.py` files. If you've never written an app that consists of multiple `.py` files, it might not be exactly clear how you can make sure that the function you wrote is actually correct.

**The notebook :**
```python
# Cell 1
def calculate_something(x):
    return x * 2 + 1

# Cell 2
result = calculate_something(5)
print(result)  # Quick test!
```

**The multi-file:**
```
mood-tracker/
├── app.py              # Main program
├── src/
│   └── app_logic.py    # Function lives here
```

**How do you test that  `log_mood()` is correct if it's in `src/app_logic.py` but use it it in `app.py`?**

Here are some options you can use. Depending on the situation, you might prefer one or another:

### 1. **Write Direct + Run Whole App** (Brave Method )
- Write the function directly in the `.py` file
- Run the entire application to see if it works
- **Pros**: Forces you to think about integration early, less typing. When things are straightforward I use it often
- **Cons**: Slow feedback loop, hard to debug

### 2. **Prototype in Notebook + Copy Over** (Safe Method )
- Write and test the function in `.ipynb` first
- Once it works, copy it to the correct `.py` file
- **Pros**: Familiar workflow, confidence before committing
- **Cons**: Potential copy-paste errors

### 3. **Write Direct + Import to Notebook** (Hybrid Method )
- Write the function in the `.py` file
- Import it into an `.ipynb` for testing
- **Pros**: Best of both worlds - proper structure + easy testing
- **Cons**: Nothing I know of 
*Note*: with Option 3 when you import code to `.ipynb` you have to put in the very top cell the following magic functions -- they keep track of the changes in your files, so that when you edit your `.py` your notebook automatically reloads

```python
# simply dark magic
%load_ext autoreload
%autoreload 2

import src.app_logic as al

# call any function below with al.FUNCTION_NAME
```

You can use either option 2 or 3 in this lesson. To use it all you need to do is to create in VSCode `test.ipynb` in the root of your project and here you are -- in a familiar coding environment.

## Your MoodTracker Mission

We need to replace our placeholder `log_mood()` function with real functionality. Here's what our function should do:

**Requirements:**
1. **Accept two parameters**: `mood` (string) and `intensity` (integer 1-3)
2. **Create a data folder** if it doesn't exist
3. **Save to a file**: `data/mood_log.csv`
4. **File format**: One line per mood entry, like `2025-09-21,happy,2`
5. **User feedback**: Print a confirmation message

**Example usage:**
```python
log_mood("happy", 2)
# Should print: "Logged happy (intensity 2) at 2024-01-15 14:30"
# Should save: "2024-01-15 14:30,happy,2" to data/mood_log.csv
```

# Practice

### Step 1: Prototype in Notebook

<input type="checkbox"> **Create a test notebook** in your mood-tracker folder called `test.ipynb`
<br>&nbsp;&nbsp;<input type="checkbox"> Open it in VS Code (or Jupyter if you prefer)
<br>&nbsp;&nbsp;<input type="checkbox"> Write and test your `log_mood` function there first

**Here's a starter template to get you going:**
Feel free to peruse documents:
- [Time formatting/strftime](https://docs.python.org/3.6/library/datetime.html)
- [Changing case](https://docs.python.org/3.12/library/stdtypes.html#str.lower)
- [Pathlib is a good library to create a folder (pathlib.mkdir)](https://docs.python.org/3/library/pathlib.html)

```python
# Cell 1: Import what you need
from datetime import datetime
...

# Cell 2: Write your function
def log_mood(mood, intensity):
    # Get current timestamp
    timestamp = datetime.now().strftime("%Y-%m-%d %H:%M")
    
    # users only can enter 1 of 5 moods we allow
    # check if mood a correct one, if not tell them what they can enter
    # not that we should allow users to enter moods in any case, eg
    # "Happy", "happy" "HaPPy" etc
    ...
    
    # check that intensity is between 1 and 3
    ...

    # Create data directory if it doesn't exist
    ...

    # Format the log entry
    ...

    # Save to file
    ...

    # Print confirmation
    ...

# Cell 3: Test it!
log_mood("happy", 2)
log_mood("sad", 1)
```

<input type="checkbox"> **Test thoroughly** - try different moods and intensities
<br>&nbsp;&nbsp;<input type="checkbox"> Check that the `data/mood_log.csv` file is created correctly
<br>&nbsp;&nbsp;<input type="checkbox"> Make sure your function handles the file creation properly

### Step 2: Copy to the main app

<input type="checkbox"> **Once it works perfectly in your notebook:**
<br>&nbsp;&nbsp;<input type="checkbox"> Copy your function to `src/app_logic.py` (replace the placeholder)
<br>&nbsp;&nbsp;<input type="checkbox"> In `app.py`, temporarily modify the entrypoint to test with hardcoded values:
```python
if __name__ == "__main__":
    log_mood("happy", 2)  # temporary test
```
<br>&nbsp;&nbsp;<input type="checkbox"> Test by running `python app.py` - you should see "Logged ... at ..."
<br>&nbsp;&nbsp;<input type="checkbox"> Check that `data/mood_log.csv` was created with your test entry

### Question

**After implementing and testing your `log_mood` function in the notebook, what's the most important thing to verify before copying it to `src/app_logic.py`?**

- a) The function name matches exactly
- b) The function works with different mood/intensity combinations and creates the file correctly
- c) The indentation looks right
- d) The function has comments explaining every line

## Question 2

**You've successfully copied your function and added the hardcoded test `log_mood("happy", 2)` to your `app.py`. When you run `python app.py`, what actually happens behind the scenes?**

- a) Python runs only the `log_mood` function and ignores everything else
- b) Python executes the entire `app.py` file from top to bottom, including imports and the `if __name__` block
- c) Python checks if the function works first, then runs the `if __name__` block
- d) Python runs the function in a separate process to avoid conflicts

---

[Next: Command Line Arguments with Argparse](23_argparse.md)

---

<details>
<summary><b>Code Review - Reference Implementation</b></summary>

Here's a complete, working implementation of the log_mood function:

<pre><code class="language-python">
from datetime import datetime
from pathlib import Path

def log_mood(mood: str, intensity: int) -> None:
    """Log a mood with intensity to a CSV file.
    Args:
        mood (str): The emotion to log (happy, sad, angry, fearful, disgusted)
        intensity (int): Intensity level from 1-3 (1=low, 2=medium, 3=high)
    """
    # Define allowed moods (from Pixar's Inside Out)
    allowed_moods = ["happy", "sad", "angry", "fearful", "disgusted"]

    # Normalize mood input - convert to lowercase for case-insensitive comparison
    mood_lower = mood.lower()

    # Validate mood input
    if mood_lower not in allowed_moods:
        print(f"Invalid mood '{mood}'. Please choose from: {', '.join(allowed_moods)}")
        return

    # Validate intensity input
    if not isinstance(intensity, int) or intensity < 1 or intensity > 3:
        print("Intensity must be an integer between 1 and 3")
        return

    # Get current timestamp in YYYY-MM-DD HH:MM format
    timestamp = datetime.now().strftime("%Y-%m-%d %H:%M")

    # Create data directory if it doesn't exist
    # Path() creates a pathlib object, mkdir() creates the directory
    data_dir = Path("data")
    data_dir.mkdir(exist_ok=True)  # exist_ok=True means no error if dir already exists

    # Format the log entry as CSV: timestamp,mood,intensity
    log_entry = f"{timestamp},{mood_lower},{intensity}\n"

    # Save to file - append mode so we don't overwrite previous entries
    log_file = data_dir / "mood_log.csv"  # pathlib way to join paths
    with open(log_file, "a") as file:  # "a" = append mode
        file.write(log_entry)

    # Print confirmation message to user
    print(f"Logged {mood_lower} (intensity {intensity}) at {timestamp}")
</code></pre>

<b>Key implementation details:</b>
<ul>
<li><b>Input validation:</b> Checks both mood and intensity before processing</li>
<li><b>Case handling:</b> Accepts "Happy", "HAPPY", "happy" - all become "happy"</li>
<li><b>Pathlib usage:</b> Modern Python way to handle file paths</li>
<li><b>CSV format:</b> Simple comma-separated values for easy data analysis later</li>
<li><b>Append mode:</b> Preserves previous mood entries</li>
<li><b>Error handling:</b> Graceful feedback for invalid inputs</li>
</ul>

</details>

---

<details>
<summary><b>Answers to this lesson Practice</b></summary>

<b>Question 1 - Correct answer:</b> <p><b>b) The function works with different mood/intensity combinations and creates the file correctly</b></p>
<p>The most critical verification is that your function actually works as expected with various inputs and successfully creates/writes to the data file. While proper naming and code style matter, functionality is paramount. You want to be confident that when you move the function to production, it will behave exactly as tested in your notebook environment.</p>

<b>Question 2 - Correct answer:</b> <p><b>b) Python executes the entire `app.py` file from top to bottom, including imports and the `if __name__ == "__main__":` block</b></p>
<p>When you run `python app.py`, Python reads and executes the entire file sequentially. It processes the imports first (like `from src.app_logic import log_mood`), then any function definitions, and finally the `if __name__ == "__main__":` block. This is fundamentally different from notebooks where you can run cells in any order - Python applications always execute from top to bottom in a predictable sequence.</p>

</details>
<!-- end of answers section -->