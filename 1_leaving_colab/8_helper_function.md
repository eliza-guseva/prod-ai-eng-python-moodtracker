---
title: 1.8 Helper Function
---
Okay, we ventured into terminal. That was good. Now let's get back to the familiar ground and let's write some Python!

## The Application Architecture

**In notebooks**, your code runs cell by cell, with shared state in memory. Each cell can access variables from previous cells, and you often restart the kernel when things get messy. 

**In applications**, your code must be self-contained and start fresh every time it runs. There's no "previous cell" to rely on - everything the program needs must be explicitly provided. This fundamental difference shapes how we organize our code.


Look at the code below. 
If you want to change the mood, you can go back to Cell 1 and change it. 
```python 
# Cell 1 
mood = "happy" intensity = 3 
# Cell 2 
store_mood(mood)
if mood == "happy": 
    print("Great day!")
```

But if we write an application for the users (even if it is just ourselves), we cannot expect them to go and edit the code. So instead, we will accept ??


---
# TODO

Our MoodTracker will demonstrate professional patterns:

- **Command-line argument processing** - like `pandas.read_csv(filename)`
- **Function organization** - modular, testable code
- **Error handling** - graceful failures instead of crashed notebooks
- **Data persistence** - files, not just variables in memory

## Professional Command-Line Design

**Good CLI applications follow conventions**:

```bash
# Standard pattern: program action arguments
python mood_logger.py log happy 3
python mood_logger.py stats
python mood_logger.py help

# Help is always available  
python mood_logger.py --help
python mood_logger.py help
```

This matches tools you already use: `pip install package`, `git add file`, `python -m module`.

## Building the Foundation

Open `mood_logger.py` in VS Code and let's build it step by step:

### Step 1: The Help System (Professional Documentation)

```python
def show_help():
    """Display usage information for MoodTracker.
    
    This function provides comprehensive help text following
    standard CLI application conventions.
    """
    print("MoodTracker - Track your daily emotions")
    print("Designed for AI Engineers transitioning from notebooks to applications")
    print()
    print("USAGE:")
    print("  python mood_logger.py <mood> <intensity>  - Log a mood")
    print("  python mood_logger.py stats              - Show statistics")
    print("  python mood_logger.py help               - Show this help")
    print()
    print("MOODS:")
    print("  happy, sad, angry, fearful, disgusted")
    print("  (Based on Pixar's Inside Out emotions)")
    print()
    print("INTENSITY:")
    print("  1 = low       (slightly happy)")
    print("  2 = medium    (pretty happy)")  
    print("  3 = high      (extremely happy)")
    print()
    print("EXAMPLES:")
    print("  python mood_logger.py happy 2")
    print("  python mood_logger.py angry 3")
    print("  python mood_logger.py fearful 1")
    print()
    print("DATA STORAGE:")
    print("  Moods are saved to: data/mood_log.txt")
    print("  Data persists between program runs (unlike notebook variables)")


# Application entry point - this is what runs when you execute the script
if __name__ == "__main__":
    show_help()
```

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