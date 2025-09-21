---
title: 2.04 Adding Revert Functionality
---

Time for a mini-challenge!

We've been logging moods, but what if you make a mistake? What if you accidentally log "angry 3" when you meant "happy 3"? Right now, you'd have to manually edit the CSV file. Not very user-friendly!

Let's add a `revert` command that undoes the last mood entry:

```bash
python app.py happy 2
python app.py sad 1
python app.py revert    # Removes the "sad 1" entry
python app.py revert    # Removes the "happy 2" entry
```

## Your Mission

You need to:

1. **Add a new command-line option** for `revert` (check the previous lesson if you forgot how argparse works)
2. **Implement the revert function** in `src/app_logic.py`
3. **Wire it up** in your main application logic

## The Revert Function

Here's the function you need to add to `src/app_logic.py`. Copy this exactly:

```python
import csv
import os
from datetime import datetime
from pathlib import Path

def revert_last():
    """Remove the last mood entry from the log file."""
    data_dir = Path("data")
    filename = data_dir / "mood_log.csv"

    if not filename.exists():
        print("No mood log found!")
        return

    # Read all rows
    with open(filename, 'r') as file:
        rows = list(csv.reader(file))

    if len(rows) == 0:
        print("No mood entries to revert!")
        return

    # Remove last row and rewrite file
    last_entry = rows[-1]
    rows = rows[:-1]

    with open(filename, 'w', newline='') as file:
        writer = csv.writer(file)
        writer.writerows(rows)

    print(f"Reverted last entry: {last_entry[1]} (intensity {last_entry[2]}) from {last_entry[0]}")
```

## Your Challenge

Figure out how to:

1. **Modify your argparse setup** to handle three possible commands:
   - `python app.py happy 2` (mood + intensity)
   - `python app.py revert` (just the revert command)
   - `python app.py --help` (still works)

2. **Update your main logic** to call `revert_last()` when the user runs the revert command

**Hints:**
- You might need to make some arguments optional
- Think about when the user provides just one argument vs. two arguments
- The previous lesson showed you all the argparse tools you need

# Practice

<input type="checkbox"> **Step 1: Add the revert function**
<br>&nbsp;&nbsp;<input type="checkbox"> Copy the `revert_last()` function to `src/app_logic.py`
<br>&nbsp;&nbsp;<input type="checkbox"> Make sure you have the necessary imports at the top of the file

<input type="checkbox"> **Step 2: Modify your argparse setup**
<br>&nbsp;&nbsp;<input type="checkbox"> Figure out how to make your current arguments work with a new `revert` option
<br>&nbsp;&nbsp;<input type="checkbox"> Test that your old commands still work: `python app.py happy 2`

<input type="checkbox"> **Step 3: Wire up the logic**
<br>&nbsp;&nbsp;<input type="checkbox"> Import `revert_last` in your `app.py`
<br>&nbsp;&nbsp;<input type="checkbox"> Add logic to call `revert_last()` when appropriate

<input type="checkbox"> **Step 4: Test everything**
<br>&nbsp;&nbsp;<input type="checkbox"> Log a few moods: `python app.py happy 2`, `python app.py sad 1`
<br>&nbsp;&nbsp;<input type="checkbox"> Try reverting: `python app.py revert`
<br>&nbsp;&nbsp;<input type="checkbox"> Check your `data/mood_log.csv` file to see if the last entry was removed
<br>&nbsp;&nbsp;<input type="checkbox"> Try reverting when there are no entries

## Question 1

**What happens when you run `python app.py revert` on an empty mood log?**

- a) Python crashes with a file not found error
- b) The function prints "No mood entries to revert!" and exits gracefully
- c) It creates an empty CSV file
- d) It asks the user what to do

## Question 2

**The revert function reads all rows into memory before rewriting the file. For a mood tracker with thousands of entries, what might be a concern?**

- a) The CSV format can't handle that many rows
- b) Reading large files into memory could be slow or use too much RAM
- c) The timestamps will become corrupted
- d) Python can't handle more than 1000 CSV rows

## Question 3

**If your argparse setup is working correctly, what should happen when you run `python app.py revert 2`?**

- a) It should revert the last 2 entries
- b) It should show an error because revert doesn't take additional arguments
- c) It should log "revert" as a mood with intensity 2
- d) It should show the help message

---

[Next: Statistics and Data Analysis](25_statistics.md)

[Rest Stop: File I/O and CSV Handling](24a_csv_deep_dive.md)

---

<details>
<summary><b>Solutions and Approaches</b></summary>

<b>One possible argparse approach:</b>

<pre><code class="language-python">
def main():
    parser = argparse.ArgumentParser(
        description="MoodTracker - Track your daily emotions",
        epilog="Examples: python app.py happy 2, python app.py revert"
    )

    # Make mood and intensity optional
    parser.add_argument(
        "command_or_mood",
        help="Either 'revert' or a mood (happy, sad, angry, fearful, disgusted)"
    )
    parser.add_argument(
        "intensity",
        type=int,
        nargs='?',  # Optional - only required for mood logging
        choices=[1, 2, 3],
        help="Intensity level: 1=low, 2=medium, 3=high (required for mood logging)"
    )

    args = parser.parse_args()

    if args.command_or_mood == "revert":
        if args.intensity is not None:
            print("Error: revert command doesn't take intensity argument")
            sys.exit(1)
        revert_last()
    elif args.command_or_mood in ["happy", "sad", "angry", "fearful", "disgusted"]:
        if args.intensity is None:
            print("Error: mood logging requires intensity (1-3)")
            sys.exit(1)
        log_mood(args.command_or_mood, args.intensity)
    else:
        print("Error: Invalid command. Use 'revert' or a valid mood.")
        sys.exit(1)
</code></pre>

<b>Alternative approach using subparsers:</b>

<pre><code class="language-python">
def main():
    parser = argparse.ArgumentParser(description="MoodTracker")
    subparsers = parser.add_subparsers(dest="command", help="Available commands")

    # Log command
    log_parser = subparsers.add_parser("log", help="Log a mood")
    log_parser.add_argument("mood", choices=["happy", "sad", "angry", "fearful", "disgusted"])
    log_parser.add_argument("intensity", type=int, choices=[1, 2, 3])

    # Revert command
    revert_parser = subparsers.add_parser("revert", help="Remove the last mood entry")

    args = parser.parse_args()

    if args.command == "log":
        log_mood(args.mood, args.intensity)
    elif args.command == "revert":
        revert_last()
    else:
        parser.print_help()
</code></pre>

</details>

<details>
<summary><b>Answers to this lesson Practice</b></summary>

<b>Question 1 - Correct answer:</b> <p><b>b) The function prints "No mood entries to revert!" and exits gracefully</b></p>
<p>The `revert_last()` function includes proper error checking. It first checks if the file exists, then checks if there are any rows to remove. When there are no entries, it prints a helpful message and returns gracefully instead of crashing. This is an example of defensive programming - anticipating edge cases and handling them user-friendly way.</p>

<b>Question 2 - Correct answer:</b> <p><b>b) Reading large files into memory could be slow or use too much RAM</b></p>
<p>The current implementation uses `list(csv.reader(file))` which loads the entire file into memory at once. For small personal mood logs this is fine, but for very large files (thousands of entries), this approach could be slow and memory-intensive. In production applications, you'd typically use more efficient approaches like reading the file backwards or keeping track of line positions.</p>

<b>Question 3 - Correct answer:</b> <p><b>b) It should show an error because revert doesn't take additional arguments</b></p>
<p>If your argparse setup is correct, it should validate that the `revert` command doesn't expect additional arguments. The `2` in `python app.py revert 2` should either be rejected by your argument parser, or caught by your logic that checks whether the user provided the right combination of arguments for each command type.</p>

</details>
<!-- end of answers section -->