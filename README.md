# Session 8 - Functional Parameters
# EPAi Session8 Assignment

#### Objective of Assignment:

1. Write a closure that takes a function and then check whether the function passed has a docstring with more than 50 characters. 50 is stored as a free variable

2. Write a closure that gives you the next Fibonacci number

3. We wrote a closure that counts how many times a function was called. Write a new one that can keep a track of how many times add/mul/div functions were called, and update a global dictionary variable with the counts

4. Modify above such that now we can pass in different dictionary variables to update different dictionaries




## Functions Defined:

* check_doc_string_len:
    Check for the total number of characters present in the docstring. If the characters are more than 50 then results as True

    ```python
    def check_doc_string_len():
    """ Closure function to generate function to check doc string length > 50
    Returns:
        inner: function
    """
    doc_str_threshold = 50
    def doc_length_check(fn):
        fn_len = len(fn.__doc__.replace("\n",""))
        print('Docstring: {0}\nCharacter Count = {1}'.format(fn.__doc__,fn_len))
        return fn_len > doc_str_threshold
    return doc_length_check
    ```

* gen_next_fibonacci_num:
Generates a next Fibonacci number in a series

```python
def gen_next_fibonacci_num():
    """ Closure function to generate next fibonacci number
    Returns:
        fibonacci: function
    """
    num1 = 0
    num2 = 0
    def fibonacci():
        nonlocal num1, num2
        if num1 ==0 and num2 ==0:
            num2 = 1
        else:
            num2, num1 = num1+ num2, num2
        return num1
    return fibonacci
```

* add:
Adds a given two numbers 

* mul:
Multiplies a given two numbers

* div:
Divides a given two numbers

* counter: Counts the total number of times that the functions run in the background
```python
cnt={}
def counter(fn):
    """ Closure function to create a counter function 
    Counter will be saved as dictionary with key as function name
    Args:
        fn: function call to be counted
        cnt: is global counter
    Return:
        inner: function
    """
    key = ""
    def inner(*args, **kwargs):
        global cnt
        nonlocal key
        key = fn.__name__
        if key not in cnt:            
            cnt[key] = 0
        cnt[key] += 1
        print('{0} has been called {1} times'.format(fn.__name__, cnt[key]))
        return fn(*args, **kwargs)
    return inner
```

* cnt: Global dictionary to keep a count of any given function

* user_counter: Closure function to generate function with not only runs the function but also keep tracks of its count with user defined dicitionary

```python
def user_counter(fn,cnt):
    """ Closure function to create a counter function 
    Counter will be saved as dictionary with key as function name
    Args:
        fn: function call to be counted
        cnt: user defined counter for each user different
    Return:
        inner: function
    """
    key = ""
    def inner(*args, **kwargs):
        nonlocal key
        key = fn.__name__
        if key not in cnt:            
            cnt[key] = 0
        cnt[key] += 1
        print('{0} has been called {1} times'.format(fn.__name__, cnt[key]))
        return fn(*args, **kwargs)
    return inner
```

