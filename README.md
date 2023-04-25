When I started learning to use Python four years ago, I had only ever used one other programming language, R. (Well, I also used Stata in grad school, but to be fair, I blocked out a lot of memories from those years.) I was familiar with how to use R, but didn't understand a lot of the concepts behind how it worked. So when it came time to learn Python, it frustrated me--I already *knew* how to program, so why does it feel like I'm learning how a computer works all over again? I just want to calculate the mean of this sample! This shouldn't be so hard!

Now that I've been programming almost exclusively in Python for a few years, I wanted to write the guide I wish I had had when I was first learning it. Something that would help me translate the R in my head to Python in the computer so I could get my code running without scouring the internet for how to decipher Python's quirks. Basically, this guide is a short R-to-Python dictionary for some of the less-intuitive features of Python to hopefully save R users time when they are first learning Python.

I want to note that I am an economist by training and a data scientist by trade. I have **no** compsci background and only know what I've picked up on the job, so please excuse and inform me of any inaccuracies or vagueness so that I can fix them!

# Summary
For more information on each row, check the corresponding section below.
**Note**: In the Python column of this table, assume `df` is a Pandas dataframe.
| Topic | R   | Python |
| ---   | --- | ---    |
| Importing packages | `library(package_name)` | `import package_name` **OR** <br /> `import package_name as alias` **OR** <br /> `from package import module` |
| Referring to dataframe columns | `df$col1` | `df.col1` |
| Data summaries | `mean(df)` | `df.col1.mean()` |

# Packages
To import a package in R, you use `library(package_name)`. The concept is the same for many Python packages: `import package_name`.

However, there are three differences with Python: aliasing, namespaces, and modules.
* **Aliasing**  
  * It is conventional to import some Python packages with a nickname. For example, 
    ```python
    import pandas as pd
    ```
  * When you refer to `pandas` in the code, you can just type `pd` instead and save a few keystrokes. This is helpful as these keystrokes add up, because of...
* **Namespaces** 
  * In R, you call the function from a package by its name. For example, `filter()` is a function in the `dplyr` package. Once you load `dplyr`, calling `filter()` invokes dplyr's `filter()` function.
    ```r
    library(dplyr)
    filter(df, col1 > 10)
    ```
  * In Python, if you want to call a package's function, you have to specify the package **every time** (unless you imported the function individually, as you'll see in the next bullet). 
    * For example,
      ```python
      import pandas as pd
      pd.read_csv('data.csv')
      ```
    * If you just call `read_csv()` by itself without importing it individually, Python won't know what you mean.
* **Modules** 
  * In R, loading a package generally loads all of its functions. Once you load `dplyr`, you can call all of its functions.
  * For some large Python packages, it's common to import subsets (modules) of the package, or even individual functions, specific to what you need without loading the entire package. 
    * For example, you might just want to use `scikit-learn`'s confusion matrix function without loading all of its myriad other features.
      ```python
      from sklearn.metrics import confusion_matrix
      confusion_matrix(df.col1, df.col2)
      ```
      This is equivalent to
      ```python
      from sklearn import metrics
      metrics.confusion_matrix(df.col1, df.col2)
      ```
      and **(DO NOT DO THIS, DEMONSTRATION PURPOSES ONLY)***
      ```python
      import sklearn
      sklearn.metrics.confusion_matrix(df.col1, df.col2)
      ```
    * To most closely emulate R's behavior, you can also import all packages from a package directly into your general namespace:
      ```python
      from sklearn.metrics import *
      confusion_matrix(df.col1, df.col2)
      ```
Did you notice anything odd about the Modules bullet above? When talking about the package, I called it `scikit-learn`, but in the code, I write `sklearn`. 

The reason for this escapes me to this day, but for some packages, when you import them, **you use a different name** than you used to install them. To install scikit-learn, you run `pip install scikit-learn`. And to load it, you run `from sklearn import ...`
Installing: some names differ, like sklearn/scikit-learn
