---
title: 2.22a Rest Stop - The `with` Statement
---

Hey! Welcome to the next rest stop!

You might have noticed in our MoodTracker code we wrote something like this:

```python
with open(log_file, "a") as file:
    file.write(log_entry)
```

And you might be thinking: "What's this `with` thing? Why not just `file = open(log_file, "a")`?"

Great question! The `with` statement is one of Python's most helpful features, but it's not immediately obvious why you need it if you're coming from notebooks where things "just work."

## The Problem: Files That Stay Open

**In notebooks**, if you forget to close a file, it's usually not a big deal. You restart the kernel, everything resets, problem solved.

**In applications**, forgetting to close files can cause real problems:

```python
# The "oops I forgot" way
file = open("data/mood_log.csv", "a")
file.write("2024-01-15,happy,2\n")
# Oops! Forgot to call file.close()
# File stays open in memory
# Do this 1000 times = 1000 open files = your program crashes
```

**What happens?** Your operating system limits how many files a program can have open simultaneously. Forget to close enough files, and your program will crash with "Too many open files" error.

## The Manual Solution (Annoying)

```python
# The "I'll remember to close it" way
file = open("data/mood_log.csv", "a")
file.write("2024-01-15,happy,2\n")
file.close()  # Don't forget this!

# But what if an error happens?
file = open("data/mood_log.csv", "a")
file.write("2024-01-15,happy,2\n")
# ERROR OCCURS HERE - file.close() never runs!
some_function_that_crashes()
file.close()  # This line never executes
```

**The problem:** If an error occurs between `open()` and `close()`, the file stays open forever.

## The `with` Statement Solution (Automatic)

```python
# The "Python handles it for me" way
with open("data/mood_log.csv", "a") as file:
    file.write("2024-01-15,happy,2\n")
    # Even if an error happens here...
    some_function_that_might_crash()
# Python AUTOMATICALLY closes the file when we exit this block
# No matter what happens - error or success
```

**What `with` does:**
1. **Opens the file** and assigns it to `file`
2. **Executes everything indented** under the `with` block
3. **Automatically closes the file** when done
4. **Closes the file even if an error occurs**

## How `with` Actually Works

The `with` statement follows a pattern called "context management." Here's what happens step by step:

```python
with open("mood_log.csv", "a") as file:
    # 1. Python calls open() and stores result in 'file'
    # 2. Python remembers "I need to close this when done"
    file.write("happy,2\n")
    # 3. More code runs...
# 4. Python exits the 'with' block
# 5. Python automatically calls file.close()
# 6. This happens EVEN if there was an error inside the block
```

**Think of it like:** Python puts a reminder in its calendar: "No matter what happens, close this file when I'm done with this block."

## Real-World Example

Let's say you're logging moods for 1000 users:

```python
# Without 'with' - DANGEROUS
def log_many_moods():
    for i in range(1000):
        file = open(f"user_{i}_moods.csv", "a")
        file.write("happy,2\n")
        # Forgot file.close() - now we have 1000 open files!
    # Program crashes: "Too many open files"

# With 'with' - SAFE
def log_many_moods():
    for i in range(1000):
        with open(f"user_{i}_moods.csv", "a") as file:
            file.write("happy,2\n")
        # Python automatically closed each file
    # Program runs perfectly
```

## `with` Works with More Than Files

The `with` statement isn't just for files. It works with anything that needs "setup" and "cleanup":

```python
# Database connections
with database.connect() as conn:
    conn.execute("INSERT INTO moods ...")
# Connection automatically closed

# Network requests
with requests.session() as session:
    response = session.get("https://api.example.com")
# Session automatically cleaned up

# Even simple things like timing
with Timer() as timer:
    slow_function()
# Timer automatically stops and reports duration
```

## Multiple Files at Once

You can open multiple files in one `with` statement:

```python
with open("input.csv", "r") as input_file, \
     open("output.csv", "w") as output_file:
    data = input_file.read()
    processed_data = process(data)
    output_file.write(processed_data)
# Both files automatically closed
```

# Practice

<input type="checkbox"> **Let's see the difference yourself**
<br>&nbsp;&nbsp;<input type="checkbox"> Create a test notebook `test_with.ipynb` in your project
<br>&nbsp;&nbsp;<input type="checkbox"> Try this code that demonstrates the problem:

```python
# Cell 1: The problematic way (Note: this might not work on all systems)
def open_files_demo():
    files = []
    print("Opening files without closing...")
    for i in range(5):
        file = open(f"test_{i}.txt", "w")
        files.append(file)
        print(f"Opened file {i}")

    print("Files are still open in memory!")

    # Clean up manually
    for file in files:
        file.close()
    print("Now closed them all")

open_files_demo()
```

<input type="checkbox"> **Now try the safe way:**

```python
# Cell 2: The 'with' way
def safe_files_demo():
    print("Using 'with' statements...")
    for i in range(5):
        with open(f"test_safe_{i}.txt", "w") as file:
            file.write("Hello from file!")
            print(f"Processed file {i}, automatically closed")

safe_files_demo()
```

<input type="checkbox"> **Test error handling:**

```python
# Cell 3: What happens when errors occur?
def test_error_handling():
    try:
        with open("error_test.txt", "w") as file:
            file.write("Starting...")
            print("About to cause an error...")
            raise Exception("Something went wrong!")
            file.write("This never executes")
    except Exception as e:
        print(f"Error occurred: {e}")

    # Check if file was closed despite the error
    try:
        with open("error_test.txt", "r") as file:
            content = file.read()
            print(f"File contents: '{content}'")
            print("File was properly closed and can be read!")
    except Exception as e:
        print(f"Problem reading file: {e}")

test_error_handling()
```

## Question 1

**You're processing 100 CSV files in a loop. Without `with` statements, what's the most likely problem you'll encounter?**

- a) The files will be processed in the wrong order
- b) Your program will crash with "Too many open files" error
- c) The CSV data will be corrupted
- d) Python will run out of memory storing the file contents

## Question 2

**What happens if an error occurs inside a `with` block?**

- a) The file stays open and you have to restart Python
- b) Python automatically closes the file, then raises the error
- c) The error is automatically caught and ignored
- d) Python asks you what to do with the open file

## Question 3

**In notebooks, why might you not notice file-closing problems as much as in applications?**

- a) Jupyter automatically closes all files every 5 minutes
- b) Notebooks can have unlimited open files
- c) You often restart the kernel, which closes everything
- d) Files in notebooks don't actually open

---

[Continue to Main Course: Command Line Arguments](23_argparse.md)

[Back to Main Course: Developing and Testing](22_test_and_dev.md)

---

<details>
<summary><b>Answers to this lesson Practice</b></summary>

<b>Question 1 - Correct answer:</b> <p><b>b) Your program will crash with "Too many open files" error</b></p>
<p>Operating systems limit how many files a process can have open simultaneously (usually around 1000-4000). Without `with` statements, each `open()` call consumes one of these slots. Process 100 files without closing them, and you'll quickly hit this limit, causing your program to crash. The `with` statement prevents this by automatically closing each file when done.</p>

<b>Question 2 - Correct answer:</b> <p><b>b) Python automatically closes the file, then raises the error</b></p>
<p>This is the key benefit of `with` statements - they guarantee cleanup even when errors occur. Python first executes the cleanup code (closing the file), then re-raises the error for you to handle. This prevents resource leaks while still allowing proper error handling in your application.</p>

<b>Question 3 - Correct answer:</b> <p><b>c) You often restart the kernel, which closes everything</b></p>
<p>In notebooks, when you restart the kernel (which happens frequently during development), all open files, variables, and resources are automatically cleaned up. This masks the file-closing problem because the restart essentially "fixes" it. In applications that run continuously, you don't have this safety net, making proper resource management critical.</p>

</details>
<!-- end of answers section -->