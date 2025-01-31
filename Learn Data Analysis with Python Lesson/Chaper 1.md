# How to Use This Book

If you are already using Python for data analysis, just browse this book’s table of contents.  
You will probably find a bunch of things that you wish you knew how to do in Python.  
If so, feel free to turn directly to that chapter and get to work.  
Each lesson is, as much as possible, self-contained.

> **Be warned!** This book is more a workbook than a textbook.

If you aren’t using Python for data analysis, begin at the beginning.  
If you work your way through the whole workbook, you should have a better idea of how to use Python for data analysis when you are done.

If you know nothing at all about data analysis, this workbook might not be the place to start.  
However, give it a try and see how it works for you.

---

## Installing Jupyter Notebook

The fastest way to install and use Python is to do what you already know how to do—use your browser.  
Why not use **Jupyter Notebook**?

---

## What Is Jupyter Notebook?

**Jupyter Notebook** is an interactive Python shell that runs in your browser.  
When installed through **Anaconda**, it is easy to quickly set up a Python development environment.  
Since it’s easy to set up and easy to run, it will be easy to learn Python.

Jupyter Notebook turns your browser into a Python development environment.  
The only thing you have to install is **Anaconda**.  
Essentially, it allows you to enter a few lines of Python code, press `CTRL+Enter`, and execute the code.  
You enter the code in **cells** and then run the currently selected cell.  
There are also options to **run all the cells** in your notebook, which is useful for developing larger programs.

---

## What Is Anaconda?

**Anaconda** is the easiest way to ensure that you don’t spend all day installing Jupyter.  
Simply **download the Anaconda package** and run the installer.  

The **Anaconda software package** contains everything you need to create a Python development environment.  
Anaconda comes in **two versions**:
- Python **2.7**
- Python **3.x**  

For the purposes of this guide, **install the version for Python 2.7**.

Anaconda is an **open-source data science platform**.  
It contains over **100 packages** for use with Python, R, and Scala.  
You can download and install Anaconda **quickly** with minimal effort.  

Once installed, you can:
- **Update** the packages
- **Upgrade** the Python version
- **Create environments** for different projects

---

## Getting Started

Follow these steps to set up your Jupyter Notebook:

1. **Download and install Anaconda** at [Anaconda.com](https://www.anaconda.com/download).
2. **Run the Jupyter Notebook application** that was installed as part of Anaconda.
3. Your browser will open at: `http://localhost:8888`.  
   - If you’re using **Internet Explorer**, close it.  
   - Use **Firefox** or **Chrome** for the best results.
4. **Start a new notebook**:
   - On the right-hand side of the browser, click the drop-down button labeled **"New"**.
   - Select **Python** or **Python 2**.
5. This will open a **new iPython notebook** in another browser tab.  
   - You can have **multiple notebooks open** in different tabs.
6. Jupyter Notebook contains **cells** where you can type Python code.  
   - To get started (for Python 2.7), type:
     ```python
     print "Hello, World!"
     ```
     - Then press `CTRL+Enter`.  
   - If you are using **Python 3.5**, use:
     ```python
     print("Hello, World!")
     ```

---

## Getting the Datasets for the Workbook’s Exercises

1. **Download the dataset files** from:  
   [http://www.ajhenley.com/dwnld](http://www.ajhenley.com/dwnld).
2. **Upload the file** `datasets.zip` to **Anaconda** in the same folder as your notebook.
3. **Run the Python code** below to unzip the datasets:

   ```python
   path_to_zip_file = "datasets.zip"
   directory_to_extract_to = ""

   import zipfile

   zip_ref = zipfile.ZipFile(path_to_zip_file, 'r')
   zip_ref.extractall(directory_to_extract_to)
   zip_ref.close()
