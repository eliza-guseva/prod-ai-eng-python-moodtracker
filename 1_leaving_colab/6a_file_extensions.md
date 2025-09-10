---
title: "1.6a Rest Stop: File Extensions"
---
## Lesson 1.6a File Extensions

**Notice how when we created files, we always had them end  with a dot and letters?** Those are called **file extensions** - they tell your computer (and you) what type of file it is.

**Common extensions you'll see:**
- `.py` - Python code files
- `.md` - Markdown files (documentation, or what I write this course in)
- `.txt` - Plain text files
- `.csv` - Data files (spreadsheets)
- `.jpg`, `.png` - Image files
- `.pdf` - Documents

**Nearly all files have extension**, but Windows and Mac by default hide them, so if you haven't worked with IDEs like VSCode before, extensions might not be something you think about. But they matter.

**Windows and Mac in their attempt to hide extensions might cause you problems.** For example, if you create a file called `app.py` with a built-in text editor, your computer might secretly saves it with an extra extension.

- **Windows:** Notepad saves it as `app.py.txt`
- **Mac:** TextEdit saves it as `app.py.rtf`

In your file browser, you only see `app.py` because both systems hide extensions by default.
Then when you try to run:
```bash
python app.py
```

You get: `python: can't open file 'app.py': [Errno 2] No such file or directory`

**Solution:**
- **Windows:** File Explorer → View → Show → File name extensions
- **Mac:** Finder → Preferences → Advanced → Show all filename extensions

**Or better: always create code files in VS Code (or terminal), not basic text editors** - it won't add surprise extensions.

# Practice

**Your friend sends you a file called `presentation` with no extension. What problem might this cause?**

a) The file will be corrupted 
b) You won't know what program to use to open it 
c) It will take up more storage space 
d) It can't be copied to other computers


**You see a file called `data.csv` in your project. What type of content would you expect to find inside?**

a) Python code 
b) A spreadsheet with rows and columns of data 
c) An image 
d) Documentation text

---
[Next Lesson](7_basic_terminal.md)

---

<details> <summary><b>Answers to this lesson Practice</b></summary> <b>Question 1 - Correct answer:</b> <p> b) You won't know what program to use to open it </p> <p> File extensions tell the operating system and users what type of file it is and which program should be used to open it. Without an extension, you have to guess the file type or try different programs until you find one that works. </p> <b>Question 2 - Correct answer:</b> <p> b) A spreadsheet with rows and columns of data </p> <p> The .csv extension stands for "Comma-Separated Values" - it's a plain text format used to store tabular data where each line represents a row and columns are separated by commas. CSV files are commonly used for data exchange between different programs. </p> </details> <!-- end of answers section -->