---
title: 1.8 Terminal Navigation
---
Now that you know the basic commands, let's learn how to navigate efficiently to your projects. This is crucial because **an engineer you are likely expected to be able to navigate between different project folders**, and you need to be comfortable moving around your file system.

## Paths

In [Project Organization](6_project_organization) we were comparing your computer with a filing cabinet. We are going to continue with it. In this metaphor, navigating between folders, is like telling someone a direction to a specific location in our cabinet. Something like `Drawer 1 -> Section A -> Folder 13 -> Page 20`.

The way how we can provide these directions in a computer can be either with `absolute path` or `relative path`


### Absolute paths

**An absolute path is like giving someone your complete location** - the full route: `My Cabinet -> Drawer 1 -> Section A -> Folder 13 -> Page 20`

**On Windows (Git Bash):**
```bash
/c/Users/YourName/Documents/mood-tracker
```

**On Mac/Linux:**
```bash
/Users/yourname/Documents/mood-tracker
```

This means: "Start at the C: drive (the whole cabinet), go to Users drawer, find YourName folder, then Documents section, then mood-tracker"

**Absolute paths always start with `/`** (the root of your file system) and give the complete path from there.

### Relative Paths

**A relative path is like saying** something like "from where you're standing at the filing cabinet, go to the folder above, then to page 14 in that folder." 

Relative paths depend on our current location. When we provide relative paths we _assume_ we know where we are. If we assumed wrong, our navigation will result in an error.

**Examples of relative paths:**
```bash
cd Documents/mood-tracker           # Go into Documents, then mood-tracker
cd ../other-project                 # Go up one level, then into other-project
cd ./mood-tracker                   # Go into mood-tracker from current location
```

**Key symbols:**
- `.` means "current directory" (where you are now)
- `..` means "parent directory" (one level up)
- No leading `/` means "relative to where I am"

**We use relative paths often**:
- It's annoying to type the whole path every time
- You don't have to remember exact folder locations
- Projects can be moved around without breaking

**Example:** If you write `cd /c/Users/ME/Documents/mood-tracker` in your script, it won't work on your  colleague's computer. But `cd ./mood-tracker` works anywhere (or almost anywhere anyhow).
### FYI: Navigation Shortcuts
```bash
cd ~                    # Go to home directory (from anywhere)
cd                      # Also goes to home directory (shortcut)
cd -                    # Go back to previous directory
pwd                     # Show where you are (Print Working Directory)
```


# Practice

Let's practice navigating to your mood-tracker project using both types of paths.

## Question 1
### Step 1: Find your current location
- [ ] Open your terminal (if you don't have it open)
- [ ] Run `pwd` to see where you are
- [ ] Write down this path - this is an absolute path to your current location
### Step 2: Navigate using absolute path

- [ ] Look at the absolute path from Step 1
- [ ] Navigate to the root directory: `cd /`
- [ ] Run `ls` to see what's at the root level (Lotsa stuff, right?)
- [ ] Now navigate back to wherever you were using the absolute path you wrote down in Step 1
- [ ] Run `pwd`. Are you where you were?
### Step 3: Find your mood-tracker project

- [ ] Go to you home directory (Use the appropriate command, check `CMD.md` if you forgot)
- [ ] From your home directory, check the available folders 
- [ ] Navigate to *where* you created your mood-tracker project using relative path (probably `Desktop`)
- [ ] Confirm you can see your `mood_tracker` folder (check the available folders)
- [ ] Enter your `mood_tracker` and chock available files

### What do you see?
- a) `app.py		docs		README.md	src`
- b) `mood_trackre`
- c) `Documents    Desktop` and so on

## Question 2

**You're in `/c/Users/YourName/Documents` and want to go to `/c/Users/YourName/Desktop`. Which command uses a relative path?**

- a) `cd /c/Users/YourName/Desktop`
- b) `cd ../Desktop`
- c) `cd ~/Desktop`
- d) Both b and c

## Question 3

**You're in your mood-tracker project folder and run `pwd`. You see `/c/Users/Alice/Documents/mood-tracker`. What will `cd ..` do?**

- a) Take you to `/c/Users/Alice/Documents`
- b) Take you to `/c/Users/Alice`
- c) Take you to `/c/Users`
- d) Show an error

## Question 4

**Which of these is an absolute path?**

- a) `Documents/mood-tracker`
- b) `./mood-tracker`
- c) `../other-project`
- d) `/Users/yourname/Documents/mood-tracker`

---

[Next Lesson](9_helper_function.md)

---

<details> <summary><b>Answers to this lesson Practice</b></summary>
<b>Question 1 - Correct answer:</b>

<p> a) .Hopefully you didn't get lost. if you got lost, type `cd`, it will return you to you home folder. Try to find your `mood_tracker` again  </p>

<b>Question 2 - Correct answer:</b>

<p> d) Both b and c </p> <p> `cd ../Desktop` is relative (go up one level, then into Desktop). `cd ~/Desktop` is also technically relative (relative to your home directory). Option a is absolute because it starts with `/` and gives the full path. </p>

<b>Question 3 - Correct answer:</b>

<p> a) Take you to `/c/Users/Alice/Documents` </p> <p> The `..` means "go up one level" in the directory hierarchy. From `/c/Users/Alice/Documents/mood-tracker`, going up one level takes you to `/c/Users/Alice/Documents`. </p>

<b>Question 4 - Correct answer:</b>

<p> d) `/Users/yourname/Documents/mood-tracker` </p> <p> Absolute paths always start with `/` and give the complete path from the root of the file system. All the other options are relative paths because they don't start with `/`. </p> </details> <!-- end of answers section -->