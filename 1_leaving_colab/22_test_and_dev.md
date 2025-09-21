---
title: 2.02 Developing and Testing
---
Now, when you write functions in `ipynb`, it's very easy to test them. You write a function, run it, re-write, re-run, re-write, re-run re....

When you build a python application, your functions go to different `.py` files, and if you never written an app that consists of multiple `.py` files, it might not exactly clear how you can make sure that the function you wrote is actually correct.

There are multiple ways you can do it. Here are 3 options I use. Depending on a situation you might prefer one or another.

1. Write a function directly to `.py` file. Run the whole application see if it works
2. Write a function directly to `.py` file. Import it into `ipynb` and test it there
3. Write a function in `ipynb`, test like you normally test, then copy it to a corr