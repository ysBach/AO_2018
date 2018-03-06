
# Python Basics

In this Note, you will learn how to use Python. I omitted some concepts of Python, not because they are not important, but because you may learn them gradually and we can do the things in simpler ways if we use NumPy, SciPy, or AstroPy related packages/classes/modules.

After you're finished looking at this material, I recommend you to go look at the [scipy lecture notes](https://www.scipy-lectures.org/) (chapter 1 will be enough), which although looks long but very concise and easy to understand. Then the books ["A Student's Guide to Python for Physical Modeling"](https://press.princeton.edu/titles/11349.html) and ["think python"](http://greenteapress.com/wp/think-python-2e/) (free book) are also good sources. The former is rather scince-oriented and the latter is rather general. For astronomers, there is a book called ["Statistics, Data Mining, and Machine Learning in Astronomy"](https://www.amazon.com/Statistics-Mining-Machine-Learning-Astronomy/dp/0691151687).



## Using Packages


Let me explain some of the useful packages of Python. This note is to explain basic notations of packages, and not a python tutorial. You can always come to this note when you are curious about a certain package that will be used in any of other notes.

### Importing

When you import a package, you can do

```python
import [package_name]
```

For example, say a package named `pkg`:

```python
import pkg
```

Each package may have `sub` packages. Say `pkg` has subpackage `sub`, and you want to load this `sub` only, because none of other subpackages of `pkg` will be used. Then you can do it as

```python
from pkg import sub
```
And if there is a *subsub* package named `ssub`, i.e., `ssub` $\in$ `sub` $\in$ `pkg`, then you can do

```python
from pkg.sub import ssub
```

That is, the `(larger).(smaller).(even_smaller)` style is used in Python to *locate* certain package.

To use some functions defined in the package (module), e.g., the function named `sum` which sums all the inputs, you can call this function by the aforementioned "locating" method:

```python
ssub.sum(1, 2, 3)
```

If you did `import pkg` only, you have to specify the location of `ssub` too:

```python
pkg.sub.ssub.sum(1, 2, 3)
```

Sometimes you may not like the package name, since even `ssub` feels too long for you. Then use **`as`**:

```python
from pkg.sub import ssub as S
S.sum(1, 2, 3)
```

### "Standard" Packages

First is the famous [**NumPy**](http://www.numpy.org/). Numpy is a package developed for faster numerical calculation in Python, and it is very widely used in almost all of python codes which contains any numerical calculation especially with larger data. It is customary to import it as **np**.

```python
import numpy as np
```
[**SciPy**](http://www.scipy.org/) is another widely used one. It mainly contains modules and functions that will be used if you want to do some scientific calculations, e.g., image processing, curve fitting and optimization, integration and derivatives, FFT and special functions, etc. There are too many different possible usages, so I cannot state "some widely used" packages. While you are using Python and want to do certain job and google it, then you may find some SciPy module/function which does the job very efficiently.

[**matplotlib**](http://matplotlib.org/) is also a very widely used plotting package. It resembles that of MATLAB style. As time goes, you may have a myriad of times to plot better graphs, and you will very frequently encounter matplotlib. I will not explain about much of this here. Just keep in mind that

```python
import matplotlib.pyplot as plt
```
is the most widely used convention than just "`import matplotlib`" or "`import matplotlib.pyplot`". Every time you see `plt. blahblah`, it usually means `pyplot` of `matplotlib`.


**astropy** contains enormous amount of tools that you may use as an astronomer (or even as a physicist or a scientist), and I will not explain about it in detail here. [Official website](http://docs.astropy.org/en/stable/getting_started.html). Some widely used ones are

```python
from astropy import constants as c
from astropy import units as u
from astropy.io import fits
from astropy.stats import sigma_clip
...
```



## Simple Grammar

In the following examples, I will assume you know very basics of programming languages, e.g., at least what `==`, `!=`, or `a[3]` mean. If you are not familliar with any of these and cannot understand what the following description means, please refer to some good textbooks for Python, or other programming languages.

### Data Types

As many other languages, we have **Data Types** in Python. The ones you will use for most of the time are `int` == integer, `float` == real numbers, and `str` == string (alphabets/letters). The type can be checked by the function `type(~~~)`. A lot of other types are there, but let me show you these first, and you will learn all others by yourselves very easily.

By the way, unlike many traditional languages, you don't have to specify the datatype when you declare a variable in Python.


```python
a = 3     # integer
b = 3.14  # float (real number)
c = 'cc'  # string

print(a)  # will print 3
print(b)  # will print 3.14
print(c)  # will print cc
print(type(a))   # the data types of a, b, c
print(type(b))
print(type(c))
# 3
# 3.14
# cc
# <class 'int'>
# <class 'float'>
# <class 'str'>
```


One very unusual thing for those who are familiar to other languages, even Python 2, is that the integer division now results in real number:


```python
a = 3/5    # In C/Python 2/ ..., this should be 0
b = 3./5.  # and this is 0.6
print(a)
print(b)
print(a==b) # "Is a equals b?" ==> answer will be either True OR False.
# 0.6
# 0.6
# True
```


Of course `True` and `False` have types, called `bool` == boolean:


```python
print(type(True))
print(type(False))
# <class 'bool'>
# <class 'bool'>
```


The indexing starts from 0 in Python. Let me make three new data types to show this clearly.


```python
import numpy as np

A = [0,1,2]            # classical Python "list"
B = (0,1,2)            # classical Python "tuple"
C = np.array((0,1,2))  # numpy n-dimensional array
print('A: ', A[0], A[1], A[2])
print('B: ', B[0], B[1], B[2])
print('C: ', C[0], C[1], C[2])
print('ABC: ', A, B, C)
print('type: ', type(A), type(B), type(C))
# A:  0 1 2
# B:  0 1 2
# C:  0 1 2
# ABC:  [0, 1, 2] (0, 1, 2) [0 1 2]
# type:  <class 'list'> <class 'tuple'> <class 'numpy.ndarray'>
```


You may ask why I used double parentheses for `C`. This is because `np.array` gets not only the elements (in this case the elements are 1, 2, 3), but also other optional arguments. In the following example, you may understand why numpy does not accept `np.array(0,1,2)`.


```python
C_obj = np.array([0,1,'test'], dtype='object')
print(C_obj)
print(C_obj[0], C_obj[1], C_obj[2])
print(type(C_obj[0]), type(C_obj[1]), type(C_obj[2]))
# [0 1 'test']
# 0 1 test
# <class 'int'> <class 'int'> <class 'str'>
```


In the above example, an option `dtype='object'` made it possible to save not only the same kind (e.g., three integers or three strings), but different mixed data types into one array. So now it's clear: If you use `np.array(0,1,2)`, Python understands `0` as the element (0-dimensional), but it cannot understands what are `1` and `2`, which are followed by commas. Thus, an error occurs (verify).


### Conditions/Loops

There are three main conditions/loops you may use frequently: `if`, `for`, and `while`. You can utilize `break` and `continue` too. I personally do not use `while` very much, but it's just my personal preference as a non-expert.


```python
x, y, z = 3, 3.14, 10-7
L1 = np.ones((10))  # 10 by 1 sized numpy array, filled with 1
L0 = np.zeros((10)) # 10 by 1 sized numpy array, filled with 0
L  = np.arange(0, 10, 1) # numpy array with elements [0, 10) with interval 1

if (x != y):
    print('Different!')

for i in range(0,10):
    if (L[i] == 9):
        print("\t'Oh it's NEIN!'")
        continue
    print(L[i], end=' ') # option "end" sets the ending part for each print; test many cases by yourself!
    print(L[i]==L1[i], end=' ')
        
print("\n")

j=0
while (1):  # identical to while(True)
    print(j, L1[j])
    j += 1
    if(j==5):
        print("j reached 5")
        break
# Different!
# 0 False 1 True 2 False 3 False 4 False 5 False 6 False 7 False 8 False 	'Oh it's NEIN!'
# 
# 0 1.0
# 1 1.0
# 2 1.0
# 3 1.0
# 4 1.0
# j reached 5
```


### Why Numpy Array?

Details: [Here](https://docs.scipy.org/doc/numpy/user/quickstart.html)

You may wonder why we need numpy array, while there is traditional Python list or tuple. The following examples will partially answer this question by showing how powerful numpy array is compared to that of usual list/tuple, when we want to perform scientific calculations. Unlike normal Python list, calculation time has already been optimized for NumPy, so it's much faster when there are much more data.


```python
num1 = np.arange(0, 11, 2) # generate numpy array [0, 11) with interval 2
num2 = np.random.rand(6) # generate six random numbers (0,1)

# Basics
print("num1:")
print(num1)
print("num2:")
print(num2)
print("\nnum1^2:") # "\n" means "new line".
print(num1**2)           # Square each element
print("\nnum1^(0.5):")
print(np.sqrt(num1))     # Square root of each element
print("\nnum1 in 2 x 3 form:")
print(num1.reshape(2,3)) # reshape the num1 into 2 by 3 form. 
# Identical to np.reshape(num1, (2,3))
num3 = np.reshape(num1, (2,3))
print("\nnum3's row 0:")
print(num3[0,:])         # row 0, column all (:)
print("\nnum3's min/max:")
print(num3.min(), num3.max())
# Identical to np.min(num3), np.max(num3)
print(np.where(num3 == num3.max())) # Show at which position the maximum occurs

# MASKING
tf   = np.array([False, True, False, True, True, False])
print("\nnum1's selected elements:")
print(num1[tf])

tf   = (num2*10 > 3)       # Select only elements larger than 3 from num2*10
# RHS is identical to just "num2*10>3"
print("\nnum2's selected elements:")
print(num2[tf])

# num1:
# [ 0  2  4  6  8 10]
# num2:
# [ 0.78143084  0.31859395  0.94417048  0.19161944  0.19672851  0.69199476]
# 
# num1^2:
# [  0   4  16  36  64 100]
# 
# num1^(0.5):
# [ 0.          1.41421356  2.          2.44948974  2.82842712  3.16227766]
# 
# num1 in 2 x 3 form:
# [[ 0  2  4]
#  [ 6  8 10]]
# 
# num3's row 0:
# [0 2 4]
# 
# num3's min/max:
# 0 10
# (array([1]), array([2]))
# 
# num1's selected elements:
# [2 6 8]
# 
# num2's selected elements:
# [ 0.78143084  0.31859395  0.94417048  0.69199476]
```


### Complicated Calculations

Some rather tedious/complicated calculations should be done from time to time. You may want to develop your own code/function and use it to effectively conduct certain tasks. I will briefly show you how you can define some functions.


```python
def function_f(x):
    return x**2

a=1
b=np.array([1,2,3])
print(function_f(a))
print(function_f(b))
# 1
# [1 4 9]
```


You can also set some optional arguments with giving them default values when defining:


```python
def function_g(x, mode='square'):
    if mode=='square':
        return x**2
    elif mode=='sqrt':
        return x**0.5
    else:
        raise ValueError("mode should be either 'square' or 'sqrt'!")

a=1
b=np.array([1,2,3])
print(function_g(a))               # will do square by defailt
print(function_g(b, mode='sqrt'))  # will do sqrt
print(function_g(b, mode='test'))  # will raise "ValueError"
#1
#[ 1.          1.41421356  1.73205081]
#
#---------------------------------------------------------------------------
#ValueError                                Traceback (most recent call last)
#<ipython-input-9-5c3820c2f2bc> in <module>()
#     11 print(function_g(a))               # will do square by defailt
#     12 print(function_g(b, mode='sqrt'))  # will do sqrt
#---> 13 print(function_g(b, mode='test'))  # will raise "ValueError"
#
#<ipython-input-9-5c3820c2f2bc> in function_g(x, mode)
#      5         return x**0.5
#      6     else:
#----> 7         raise ValueError("mode should be either 'square' or 'sqrt'!")
#      8 
#      9 a=1
#
#ValueError: mode should be either 'square' or 'sqrt'!
#
```

Read "The Zen of Python" in the last section. Errors should never pass silently!

## Finding Documentations

As you now can import any packages, you can use the default functions in the packages. Polynomial fitting, sigma clipping, ..., anything you need is most likely has already been constructed via NumPy/SciPy/AstroPy developers. If you want to use any of these, google the keywords like "python sigma clipping". Then you will see numpy or scipy documentation. **BUT BE CAREFUL THAT YOU ARE LOOKING AT THE DOCUMENTATION FOR THE CORRESPONDING VERSION OF THE PACKAGE!!!** If you are looking at Astropy version 0.2, while you're using v1.3, for instance, this may be a problematic situation.

Most of the documentation contains some core examples to let you understand things correctly, and you can see the source codes, if you want (there are always a '[source]' button, and you'll be redirected to GitHub repository).

Sometimes you may not be able to find comprehensive online documentation. Then use the **`docstring`**. For instance, if the function or module has the name `package.sub`, then it is most likely that it has its own docstring, and you can print it by using `__doc__`:

```python
from package import sub
print(sub.__doc__)
```





# Homework Questions

1. Read the following:

   > Python is a programming langauge. Most importantly, it is __object oriented__ and __interpreted__, __high-level language__. In short, it means **"Python is quite powerful, modern, intuitive, flexible, and easy to use."**
   >
   > The following is so-called __The Zen of Python__. As the name says, it consist of some *morals* that python keeps in mind. These are not only for the python developers, but also for any python users to code in __pythonic__ way.
   >
   > * Beautiful is better than ugly. 
   > * Explicit is better than implicit. 
   > * Simple is better than complex.  
   > * Complex is better than complicated. 
   > * Flat is better than nested. 
   > * Sparse is better than dense. 
   > * Readability counts. 
   > * Special cases aren't special enough to break the rules. 
   > * Although practicality beats purity. 
   > * Errors should never pass silently. 
   > * Unless explicitly silenced. 
   > * In the face of ambiguity, refuse the temptation to guess. 
   > * There should be one-- and preferably only one --obvious way to do it. 
   > * Although that way may not be obvious at first unless you're Dutch.
   > * *Unless you're Dutch*: See [Stack Exchange](http://ell.stackexchange.com/questions/85517/zen-of-python-meaning-of-unless-youre-dutch).
   > * *"The inventor of Python is a Dutch programmer named Guido van Rossum. It is probably a reference to the inventor of Perl, Larry Wall who is not Dutch and invented a language where there a at least 50 ways to do any one thing. – ColleenV♦ Mar 24 '16 at 22:29"*
   > * Now is better than never.
   > * Although never is often better than *right* now.
   > * If the implementation is hard to explain, it's a bad idea.
   > * If the implementation is easy to explain, it may be a good idea.
   > * Namespaces are one honking great idea -- let's do more of those!
   >
   > In Korean,
   >
   > * (아름다운 것이 못생긴(추한) 것 보다 낫다)
   > * (명시하는 것이 암시하는 것 보다 낫다)
   > * (간결한 것이 복잡한 것 보다 낫다)
   > * (복잡한 것이 난잡한 것 보다 낫다)
   > * (수평적인 것이 계층화된 것 보다 낫다)
   > * (성긴(듬성듬성한) 것이 밀집된 것 보다 낫다)
   > * (가독성은 중요하다)
   > * (특별한 경우(예외)들은 기존 규칙을 깰 만큼 특별한 게 아니다)
   > * (비록 실용성은 (규칙의) 순수성을 깰 정도로 중요하지만.)
   > * (오류는 절대 조용히 넘어가서는 안 된다)
   > * (명시적으로 그러라고 하기 전에는.)
   > * (모호함 앞에서, 추측하려는 유혹을 거절하라.)
   > * (무언가를 할 때 하나의 자명한 방식이 존재한다 -- 가장 좋은 것은 오직 하나 뿐일 것이다)
   > * (비록 그 방식이 단번에 떠오르지 않을지라도 말이다.)
   > * (지금이라도 하는 게 아예 안 하는 것 보다 낫다) 
   > * (비록 종종 아예 안 하는 게 *지금 당장* 하는 것 보다 나을지라도)
   > * (만약 구현 결과가 설명하기 어렵다면, 그것은 안 좋은 것이다.)
   > * (만약 구현 결과가 설명하기 쉽다면, 그것은 좋은 것일지도 모른다.)
   > * (네임스페이스는 엄청 좋은 것이다: 더 많이 쓰자!)
   >
   > If you want to see this __The Zen of Python__, you can type `import this`:
   >
   > ```python
   > import this
   > #The Zen of Python, by Tim Peters
   > #
   > #Beautiful is better than ugly.
   > #Explicit is better than implicit.
   > #Simple is better than complex.
   > #Complex is better than complicated.
   > #Flat is better than nested.
   > #Sparse is better than dense.
   > #Readability counts.
   > #Special cases aren't special enough to break the rules.
   > #Although practicality beats purity.
   > #Errors should never pass silently.
   > #Unless explicitly silenced.
   > #In the face of ambiguity, refuse the temptation to guess.
   > #There should be one-- and preferably only one --obvious way to do it.
   > #Although that way may not be obvious at first unless you're Dutch.
   > #Now is better than never.
   > #Although never is often better than *right* now.
   > #If the implementation is hard to explain, it's a bad idea.
   > #If the implementation is easy to explain, it may be a good idea.
   > #Namespaces are one honking great idea -- let's do more of those!
   > ```
