---
title: If name?
---



```python
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