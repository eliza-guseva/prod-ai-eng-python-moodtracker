---
title: 1.01 MoodTracker
---

# Section 1. Leaving familiar places. Build command-line mood tracker
## Lesson 1.1 MoodTracker

Welcome to your journey from Jupyter notebooks to professional software development! If you've been living in the comfortable world of `.ipynb` files and Google Colab, this chapter will feel different - and that's exactly the point.

In this chapter, we'll build _MoodTracker_, a command-line application that is grounded in the deeply scientific methodology of Pixar's "Inside Out". It helps users (you) log and analyze their daily emotions. 

This is something that you probably can build easily in Colab or Jupyter. But here's what makes this different what we are going to do from the approach you know:

- **It runs as a standalone program** - just like any application
- **It can run locally on your computer** -- no need to connect to Google Colab
- **It processes command-line arguments** - like professional developer tools
- **It saves data to files** - persistent storage without cloud dependencies
- **It follows engineering patterns** - organized, testable, maintainable code

And! We're not just building a simple script. We're establishing the **engineering mindset** and **professional workflows** that separate research code from production-ready software development. Every choice we make, from how we organize files to how we run programs, follows patterns used by professional engineering teams.

**Why mood tracker specifically??**
1. **It is connecting your analytical background** (tracking and analyzing data) with engineering practices (building applications that others can use).
2. **Simple enough** to focus on tooling and workflow
3. **Complex enough** to demonstrate proper project organization 
4. **Relatable** - everyone has emotions that one can track and maybe even learn something from them
5. **Extensible** - we can grow it into something sophisticated

By the end of this chapter, you'll have a complete development environment and a working command-line application that you can actually use daily.

---
## The Notebook vs. Engineering Mindset

### What You Know: Data Science Workflow

```python
# In a Jupyter cell
import pandas as pd
data = pd.read_csv('emotions.csv')
data.groupby('mood').mean()
# Output appears below cell
```

### What We're Building: Engineering Workflow

```bash
# In the terminal
python mood_logger.py happy 3
python mood_logger.py stats
# Output appears in terminal, data persists between runs
```

**The key difference isn't complexity** - it's **reliability and reusability**. Your notebook experiments become applications that work consistently for anyone, anywhere.

---
# Practice

**What does "engineering mindset" mean in the context of this course?**

a) Writing more complex code with advanced algorithms  
b) Using only the most cutting-edge programming languages  
c) Establishing workflows that separate research code from production-ready software  
d) Working only on large-scale distributed systems

---
**For now we skip Python Installation and explanation how to work with VSCode** -- these will be added later

[Next Lesson](6_project_organization)


<details>
<summary><b>Answers to this lesson Practice</b></summary>
<b>Correct answer:</b>
<p>
c) Establishing workflows that separate research code from production-ready software
<p>
The engineering mindset focuses on creating maintainable, scalable, and production-ready code rather than just making things work. It emphasizes proper workflows, testing, documentation, and code organization. 
</details>
<!-- end of answers section -->
