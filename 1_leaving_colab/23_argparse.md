---
title: 2.03 Command Line Arguments with Argparse
---

Alright! Time to make our MoodTracker work like a real command-line application!

Right now, we're hardcoding `log_mood("happy", 2)` in our app. But we want users to be able to run:

```bash
python app.py happy 2
python app.py sad 1
python app.py help
```

How do we get those `happy 2` arguments into our Python program? Enter **argparse** - Python's built-in solution for handling command-line arguments.

## The Problem: Getting User Input into Applications

**In notebooks**, you get user input by changing variables in cells:

```python
# Change this cell and re-run
mood = "happy"
intensity = 2
log_mood(mood, intensity)
```

**In applications**, users provide input when they run the program:

```bash
python app.py happy 2    # mood="happy", intensity=2
python app.py angry 3    # mood="angry", intensity=3
```

The question is: how does your Python code access those `happy 2` arguments?

## Meet `sys.argv` (The Raw Way)

Python gives you access to command-line arguments through `sys.argv`:

```python
import sys

print("Raw arguments:", sys.argv)
# Running: python app.py happy 2
# Output: ['app.py', 'happy', '2']
```

**What `sys.argv` contains:**
- `sys.argv[0]` = the script name (`"app.py"`)
- `sys.argv[1]` = first argument (`"happy"`)
- `sys.argv[2]` = second argument (`"2"`)

But handling `sys.argv` manually gets messy fast:

```python
# The painful manual way
import sys

if len(sys.argv) < 3:
    print("Error: Need mood and intensity")
    sys.exit(1)

mood = sys.argv[1]
try:
    intensity = int(sys.argv[2])  # Convert string to int
except ValueError:
    print("Error: Intensity must be a number")
    sys.exit(1)

if mood not in ["happy", "sad", "angry", "fearful", "disgusted"]:
    print("Error: Invalid mood")
    sys.exit(1)

if intensity < 1 or intensity > 3:
    print("Error: Intensity must be 1-3")
    sys.exit(1)

# Finally, we can use the arguments
log_mood(mood, intensity)
```

This works, but it's 20 lines just to handle two simple arguments! And we haven't even handled the `help` command yet.

## Enter Argparse (The Professional Way)

`argparse` is Python's built-in library that handles all this complexity for you:

```python
import argparse

# Create the argument parser
parser = argparse.ArgumentParser(description="MoodTracker - Track your daily emotions")

# Define what arguments we expect
parser.add_argument("mood", help="The emotion to log (happy, sad, angry, fearful, disgusted)")
parser.add_argument("intensity", type=int, help="Intensity level (1-3)")

# Parse the command line arguments
args = parser.parse_args()

# Use the arguments
log_mood(args.mood, args.intensity)
```

**What argparse does for free:**
- **Automatic help**: `python app.py --help` shows usage info
- **Type conversion**: Converts `"2"` string to `2` integer automatically
- **Error messages**: Shows helpful errors for invalid input
- **Validation**: You can add custom validation rules

## How Argparse Works

Here's the step-by-step process:

```python
import argparse

# 1. Create a parser object
parser = argparse.ArgumentParser(description="Your app description")

# 2. Tell it what arguments to expect
parser.add_argument("mood")          # Required positional argument
parser.add_argument("intensity", type=int)  # Required, converted to int

# 3. Parse whatever the user provided
args = parser.parse_args()
# This automatically reads sys.argv and processes it

# 4. Access the parsed arguments
print(f"User provided: {args.mood} and {args.intensity}")
```

**When you run `python app.py happy 2`:**
1. argparse sees `["app.py", "happy", "2"]`
2. It assigns `"happy"` to `args.mood`
3. It converts `"2"` to integer `2` and assigns to `args.intensity`
4. Your code gets clean, validated data

## Different Types of Arguments

### Positional Arguments (Required)
```python
parser.add_argument("mood")                    # Required
parser.add_argument("intensity", type=int)     # Required, converted to int
# Usage: python app.py happy 2
```

### Optional Arguments (Flags)
```python
parser.add_argument("--verbose", action="store_true")  # Flag (true/false)
parser.add_argument("--output", help="Output file")    # Optional value
# Usage: python app.py happy 2 --verbose --output results.txt
```

### Choices (Limited Options)
```python
parser.add_argument("mood", choices=["happy", "sad", "angry", "fearful", "disgusted"])
# argparse automatically validates the choice
```

## Subcommands (Advanced)

For our MoodTracker, we want multiple commands:
- `python app.py log happy 2` - log a mood
- `python app.py stats` - show statistics
- `python app.py help` - show help

```python
parser = argparse.ArgumentParser(description="MoodTracker")
subparsers = parser.add_subparsers(dest="command")

# 'log' command
log_parser = subparsers.add_parser("log", help="Log a mood")
log_parser.add_argument("mood", choices=["happy", "sad", "angry", "fearful", "disgusted"])
log_parser.add_argument("intensity", type=int, choices=[1, 2, 3])

# 'stats' command
stats_parser = subparsers.add_parser("stats", help="Show mood statistics")

# Parse and handle
args = parser.parse_args()
if args.command == "log":
    log_mood(args.mood, args.intensity)
elif args.command == "stats":
    show_stats()
```

But for now, let's keep it simple!

## Your Mission: Basic Argparse

For this lesson, we're going to implement a simpler version that handles:
- `python app.py happy 2` - log a mood
- `python app.py help` - show help (actually, argparse gives us `--help` for free!)

# Practice

<input type="checkbox"> **Step 1: Update your `app.py`**
<br>&nbsp;&nbsp;<input type="checkbox"> Remove the hardcoded `log_mood("happy", 2)` from your entrypoint
<br>&nbsp;&nbsp;<input type="checkbox"> Import argparse and implement argument parsing:

```python
import argparse
from src.app_logic import log_mood

def main():
    """Main application entry point with argument parsing."""
    # Create argument parser
    parser = argparse.ArgumentParser(
        description="MoodTracker - Track your daily emotions",
        epilog="Example: python app.py happy 2"
    )

    # Add arguments
    parser.add_argument(
        "mood",
        choices=["happy", "sad", "angry", "fearful", "disgusted"],
        help="The emotion to log"
    )
    parser.add_argument(
        "intensity",
        type=int,
        choices=[1, 2, 3],
        help="Intensity level: 1=low, 2=medium, 3=high"
    )

    # Parse arguments
    args = parser.parse_args()

    # Call our function with the parsed arguments
    log_mood(args.mood, args.intensity)

if __name__ == "__main__":
    main()
```

<input type="checkbox"> **Step 2: Test your argument parsing**
<br>&nbsp;&nbsp;<input type="checkbox"> Try: `python app.py happy 2`
<br>&nbsp;&nbsp;<input type="checkbox"> Try: `python app.py sad 1`
<br>&nbsp;&nbsp;<input type="checkbox"> Try: `python app.py angry 4` (should show error)
<br>&nbsp;&nbsp;<input type="checkbox"> Try: `python app.py excited 2` (should show error)
<br>&nbsp;&nbsp;<input type="checkbox"> Try: `python app.py --help` (should show usage info)

<input type="checkbox"> **Step 3: Handle edge cases**
<br>&nbsp;&nbsp;<input type="checkbox"> Try: `python app.py` (no arguments - should show error)
<br>&nbsp;&nbsp;<input type="checkbox"> Try: `python app.py happy` (missing intensity - should show error)
<br>&nbsp;&nbsp;<input type="checkbox"> Try: `python app.py happy two` (invalid intensity - should show error)

## Question 1

**When you run `python app.py happy 2`, what does `sys.argv` contain?**

- a) `["happy", "2"]`
- b) `["app.py", "happy", "2"]`
- c) `["python", "app.py", "happy", "2"]`
- d) `{"mood": "happy", "intensity": "2"}`

## Question 2

**What's the main advantage of using argparse instead of manually parsing `sys.argv`?**

- a) Argparse is faster than manual parsing
- b) Argparse automatically handles validation, type conversion, and help generation
- c) Argparse allows more command-line arguments than sys.argv
- d) Argparse works on more operating systems than sys.argv

## Question 3

**In your argparse setup, what happens when a user provides an invalid mood like "excited"?**

- a) Python crashes with an unhandled exception
- b) argparse shows an error message and exits gracefully
- c) The invalid mood gets passed to log_mood() anyway
- d) argparse asks the user to try again

## Question 4

**What does `type=int` do in `parser.add_argument("intensity", type=int)`?**

- a) It tells argparse that only integers are allowed
- b) It converts the string argument to an integer automatically
- c) It validates that the argument is between 1 and 3
- d) It makes the argument optional

---

[Next: Error Handling and Validation](24_error_handling.md)

[Rest Stop: Advanced Argparse Features](23a_advanced_argparse.md)

---

<details>
<summary><b>Answers to this lesson Practice</b></summary>

<b>Question 1 - Correct answer:</b> <p><b>b) `["app.py", "happy", "2"]`</b></p>
<p>`sys.argv` always contains the script name as the first element (`sys.argv[0]`), followed by all the command-line arguments. When you run `python app.py happy 2`, Python sees three things: the script name and two arguments. Note that all arguments in `sys.argv` are strings - "2" is a string, not an integer.</p>

<b>Question 2 - Correct answer:</b> <p><b>b) Argparse automatically handles validation, type conversion, and help generation</b></p>
<p>The power of argparse is that it eliminates boilerplate code. Instead of writing manual validation, type conversion, and error handling, argparse does it all for you. It converts "2" to integer 2, validates choices against your allowed list, generates helpful error messages, and even creates a `--help` option automatically.</p>

<b>Question 3 - Correct answer:</b> <p><b>b) argparse shows an error message and exits gracefully</b></p>
<p>When you specify `choices=["happy", "sad", "angry", "fearful", "disgusted"]`, argparse automatically validates the input. If someone provides "excited", argparse displays a clear error message like "argument mood: invalid choice: 'excited' (choose from 'happy', 'sad', 'angry', 'fearful', 'disgusted')" and exits with a non-zero status code.</p>

<b>Question 4 - Correct answer:</b> <p><b>b) It converts the string argument to an integer automatically</b></p>
<p>All command-line arguments start as strings. When you specify `type=int`, argparse takes the string argument (like "2") and converts it to an integer (2) before storing it in `args.intensity`. If the conversion fails (like "two"), argparse shows an error message. The `type=int` parameter handles the conversion, while `choices=[1, 2, 3]` handles the validation.</p>

</details>
<!-- end of answers section -->