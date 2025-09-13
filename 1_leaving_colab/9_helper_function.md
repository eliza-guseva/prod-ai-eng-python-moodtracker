---
title: 1.9 Helper Function
---
Okay, we ventured into terminal for some time. That was good! Now let's get back to the familiar ground and let's write some Python!

## The Application Architecture

**In notebooks**, your code runs cell by cell, with **shared state** in memory. 

**Shared state** means that each cell can access variables from other cells, and you often restart the kernel when things get messy. 

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

But if we write an application for the users (even if it is just ourselves), we cannot expect them to go and edit the code. So instead, we use **command line arguments** to get input from users. 

For our app it will look something like this:
```bash
python mood_logger.py log happy 3
```
You notice it's similar to the way how other commands operate (check your `CMD.md`): `cd folder` or `pip install package`. First we pass the command name (in our case it's a bit extended `python mood_logger.py`) and then we pass arguments like `log happy 3` or `showstats.`

Now, since we don't expect our users to go and check our code, we also need to tell them how to use our app. We need to tell them which arguments are possible -- or we need to show them `usage.`

That is why most of the CLI tools will also accept `help` or `--help` or `-h` arguments. Or often if  user didn't provide any arguments or provided wrong ones, they will show help as well. Just to be friendly. 

**Try it:** type in your terminal `pip -h` or `git help` -- you'll see that these tools will dump on your all the many arguments that you can give them.

So, let's begin with being friendly and create a help function that makes our MoodTracker as nice as the tools you use every day!

# Practice

<br><input type="checkbox"> Open `app.py` in VS Code. *Remember, don't just open a file with a double click -- first Open Folder with VS Code and then find `app.py` in the left side bar and double click it within the VS Code*
<br><input type="checkbox"> Your `app.py` is nice and empty. Copy the following function in there and save the file. This functions has nothing but a lot of print statements. Read through it -- it will show you which functionality we plan to add to our app.

```python
def show_help() -> None:
    """Display usage information for MoodTracker.
    
    This function provides comprehensive help text following
    standard CLI application conventions.
    """
    print("MoodTracker - Track your daily emotions")
    print("Designed for AI Engineers transitioning from notebooks to applications")
    print()
    print("USAGE:")
    print("  python mood_logger.py <mood> <intensity>  - Log a mood")
    print("  python mood_logger.py showstats           - Show statistics")
    print("  python mood_logger.py help                - Show this help")
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

```

<br><input type="checkbox"> Let's test it!
	<br><input type="checkbox"> In your terminal, the first thing we have to do is to navigate to your project? Do you remember where it is? type `cd path/to/your/folder`. *For example,* if you are in your home folder and your project is in the `Desktop/mood_tracker` type `cd Desktop/mood_tracker`
<br>&nbsp;&nbsp;<input type="checkbox"> run `python app.py` (type it in and hit enter)


## Question
**What do you see?**
- a) Nothing
- b) A lot of lines describing how to use 

### Issues?
<br><input type="checkbox"> If you have your terminal open and you don't know where you are, type `pwd`. If you want to go back to your home folder type `cd` (no arguments). From your home folder you can always navigate to your project (consult with your `CMD.md` if you forgot commands.)
<br><input type="checkbox"> `command not found: python`? try python3
<br><input type="checkbox"> On Window? make sure you are in `git bash` terminal.

---

[Next: Entrypoint](10_entrypoint.md)

---

<details> 
<summary><b>Answer to this lesson Practice</b></summary>
<b>Correct answer:</b> <p> a) Nothing </p> <p> When you run `python app.py`, you see nothing because the file only contains a function definition. In Python, defining a function doesn't automatically execute it - you need to explicitly call the function for it to run. The `show_help()` function exists in memory, but since there's no code that calls `show_help()`, nothing gets printed to the terminal.  </p>
</details>
