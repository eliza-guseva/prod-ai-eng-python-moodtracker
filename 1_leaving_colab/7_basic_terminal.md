---
title: 1.7 Basic Terminal
---

What we would like to build is a CLI tool.
CLI stands for **Command Line Interface**, which is sort of opposite of what you got used -- GUI, which stands for Graphical User Interface.

The reason we're even bothering with this is because so many professional development tool you'll encounter - from Docker to Git to cloud deployment - run primarily through the command line. And the reason for it is **AUTOMATION** 🎀👏🏻📣🎉🤸🏼‍♀️🎊 (As engineers we just **love** *AUTOMATION* 🎀👏🏻📣🎉🤸🏼‍♀️🎊)

And it's *very hard* to automate clicking buttons, but you can easily automate terminal commands. So, a lot of engineering, including AI/ML ones go to terminal when they need to process thousands of files or run the same workflow repeatedly.

There are engineers who largely manage to avoid it, but we're trying to go a different path here - not the path of avoiding difficulty but the path of learning engineering and understanding how to use tools efficiently. 

And the terminal is one of those tools that feels awkward in the beginning but in fact is really powerful.

**So, let's do it**

## System-Specific Terminal Access

### Windows: Git Bash (Your New Best Friend)

**Launch Git Bash** (not Command Prompt):
- **From Start Menu**: Search "Git Bash"
- **From File Explorer**: Right-click in any folder → "Git Bash Here"

### macOS: Terminal

**Launch Terminal**:
- **Spotlight**: Cmd+Space → type "Terminal"
- **Applications**: Applications → Utilities → Terminal

### Linux: Terminal

**Launch Terminal**:
- **Keyboard**: Usually Ctrl+Alt+T
- **Applications**: Search for "Terminal"

# Practice

- [ ] Let's first make sure that we aren't going to forget the most important terminal commands.
	- [ ] In your project create `CMD.md` and copy the code snippet below into it.
	- [ ] Don't forget the 3 backquotes symbols in the beginning and in the end of the snippet -- that is how `.md` files signify code block

I capitalized some letters in the explanation -- these are the letters that gave the name to the command
```bash
# Navigation
pwd                    # Show current directory (Print Working Directory)
ls                     # List files (LiSt)
ls -la                 # List files with details
cd folder_name         # Enter directory (Change Directory)
cd ..                  # Go to the parent directory (current directory is just .)
cd ~                   # Go to home folder (the tilde points to your Home Folder)

# File operations
touch filename         # Create empty file
mkdir folder_name      # Create directory (MaKe DIRertory)
cp file1 file2         # Copy file (CoPy)
cp -r folder1 folder2  # Copy folder Recursively
mv old_name new_name   # Rename/move file (MoVe)

# Python operations
python script.py       # Run Python script 
python --version       # Check Python version
````

## Question 1
Open your terminal (On Windows: GitBash -- we will always be working with GitBash)
**Which directory are you in?** Use the reference with the command.

a) `/c/Program Files/` or `/Applications/` 
b) `/c/Users/YourName/` or `/Users/yourname/` 
c) `/c/Windows/` or `/System/`

## Question 2
Now run the command to list files in your current directory. **What do you see?**

a) A long list with file permissions, dates, and sizes 
b) Just the names of files and folders like Desktop, Documents, Downloads 
c) Nothing - the directory is completely empty

## Question 3

Now try the command that lists files WITH detailed information (hint: check the reference for the option that shows details). **What's different from your previous result?**

a) You see the same simple list as before 
b) You see many more files that were hidden before, plus detailed information like dates and file sizes 
c) You only see Python files now