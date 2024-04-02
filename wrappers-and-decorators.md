## Wrappers and Decorators in Python

<br>

_Sources:_

> _Python String Formatting Best Practices [(realpython.com/python-string-formatting/#3-string-interpolation-f-strings-python-36)](https://realpython.com/python-string-formatting/#3-string-interpolation-f-strings-python-36)_
> 
>_Primer on Python Decorators [(realpython.com/primer-on-python-decorators/)](https://realpython.com/primer-on-python-decorators)_
>
> _Unwrapping the Power of Python: A Quick Guide to Wrappers and Decorators [(medium.com/codex/unwrapping-the-power-of-python-a-quick-guide-to-wrappers-and-decorators)](https://medium.com/codex/unwrapping-the-power-of-python-a-quick-guide-to-wrappers-and-decorators-db442dd89ae2#id_token=eyJhbGciOiJSUzI1NiIsImtpZCI6IjA5YmNmODAyOGUwNjUzN2Q0ZDNhZTRkODRmNWM1YmFiY2YyYzBmMGEiLCJ0eXAiOiJKV1QifQ.eyJpc3MiOiJodHRwczovL2FjY291bnRzLmdvb2dsZS5jb20iLCJhenAiOiIyMTYyOTYwMzU4MzQtazFrNnFlMDYwczJ0cDJhMmphbTRsamRjbXMwMHN0dGcuYXBwcy5nb29nbGV1c2VyY29udGVudC5jb20iLCJhdWQiOiIyMTYyOTYwMzU4MzQtazFrNnFlMDYwczJ0cDJhMmphbTRsamRjbXMwMHN0dGcuYXBwcy5nb29nbGV1c2VyY29udGVudC5jb20iLCJzdWIiOiIxMTUwMTMxMTQzODA4OTY4ODE3MjAiLCJlbWFpbCI6ImNvdXJ0bmV5LnNoZWxsZXlAZ21haWwuY29tIiwiZW1haWxfdmVyaWZpZWQiOnRydWUsIm5iZiI6MTcxMDgwMjA3MSwibmFtZSI6IkNvdXJ0bmV5IFNoZWxsZXkiLCJwaWN0dXJlIjoiaHR0cHM6Ly9saDMuZ29vZ2xldXNlcmNvbnRlbnQuY29tL2EvQUNnOG9jTHpzRWdlWWV5QkFHN2pNR3VpWVFBT090dkR6ZUpkS0lOanNnNkIzbThLREE9czk2LWMiLCJnaXZlbl9uYW1lIjoiQ291cnRuZXkiLCJmYW1pbHlfbmFtZSI6IlNoZWxsZXkiLCJpYXQiOjE3MTA4MDIzNzEsImV4cCI6MTcxMDgwNTk3MSwianRpIjoiM2U5MGZlMjZiM2FkNWVhMmNlNTQ3ZDY0MmM2OWJlMDQ1NTIyMTQwMCJ9.Fu_20TKFlR3hjqXtmjLVPf8W2CQQ7-ryPAk8_4596-0ePmlL0YLgmgWbOQ0VA-bHVFM5YimtRGMSBMTsL2Zee3IhGQeJnrJjG-jHgqDzLUdh0JcEjVAsVPsz2bXEate2wk21MIyu282q5VGncukTFtVvkk5x8uSx6qUCUGrGtVQOn080TIPDPx0Wup8Y_db0Q3M7DjjCYMbFnrj5PwvWkHTAmoJG_N26oj47c2w8QiZxw0MYSIaJnrigvDaXAYpVUE3RGwvNx8TNcWOsMrcQbRLqdi4DBj3-iy0XWdJiBc41TGUZU7MLKGPMdaM1GSUHEUkkttn2qAG_hERE_7AxyA)_
>
> _Python args and kwargs: Demystified [(realpython.com/python-kwargs-and-args/)](https://realpython.com/python-kwargs-and-args/)_

<br>
<br>

At the end of this section you will understand:

* f-Strings
* Functions
* Wrappers
* Decorators
* \*args and \**kwargs


<br> 

### f-Strings

Python 3.6 added a new string formatting approach called _formatted string literals_ or _**"f-strings"**_. f-Strings let you use embedded Python expressions inside string constants. 


```python
name = "Bob"
f'Hello, {name}!'
```




    'Hello, Bob!'




```python
a = 5
b = 10
f'Five plus ten is {a + b} and not {2 * (a + b)}.'
```




    'Five plus ten is 15 and not 30.'



<br>

### Python Functions

A **function** returns a value based on the given arguments. 



```python
def add_one(number):
    return number + 1

add_one(2)
```




    3



In general, functions in Python may also have side effects rather than just turning an input into an output. The `print()` function is an example of this: it returns `None` while having the side effect of outputting something to the console. 

<br>

**First-Class Objects**

In _functional programming_, you work almost entirely with pure functions that don't have side effects. While not a purely functional language, Python supports many functional programming concepts, including treating functions as **first-class objects**. 

>Python's functions are **first-class objects**. You can assign them to variables, store them in data structures, pass them as arguments to other functions, and even return them as values from other functions.

This means that functions can be passed around and used as arguments, just like any other object like `str`, `int`, `float`, `list`, and so on. Consider the following three functions: 


```python
def say_hello(name):
    return f"Hello {name}"

def be_awesome(name):
    return f"Yo {name}, together we're the awesomest!"

def greet_bob(greeter_func):
    return greeter_func("Bob")
```

Here `say_hello()` and `be_awesome()` are regular functions that expect a name given as a string. The `greet_bob()` function, however, expects a function as its argument. You can, for example, pass it the `say_hello()` or the `be_awesome()` function. 


```python
greet_bob(say_hello)
```




    'Hello Bob'




```python
greet_bob(be_awesome)
```




    "Yo Bob, together we're the awesomest!"



Note that `greet_bob(say_hello)` refers to two functions, but in different ways. The `say_hello` function is named without parentheses. This means that only a reference to the function is passed. The function isn't executed. The `greet_bob` function, on the other hand, is written with parentheses, so it will be called as usual. This is an important distinction that's crucial for how functions work as first-class objects. _**A function name without parentheses is a reference to a function, while a function name with trailing parentheses calls the function and refers to its return value.**_

<br>

_**Inner Functions**_

It's possible to define functions _inside other functions_. Such functions are called inner functions. Save the following into a file called `inner_functions.py`:


```python
# inner_functions.py
def parent():
    print("Printing from parent()")

    def first_child():
        print("Printing from first_child()")

    def second_child():
        print("Printing from second_child()")

    second_child()
    first_child()
```

On the command line, type: 
>>>python3 -i inner_functions.py
parent()Printing from parent()
Printing from second_child()
Printing from first_child()
The order in which the inner functions are defined does not matter. The printing only happens when the inner functions are executed. Furthermore, the inner functions aren't defined until the parent function is called. They're **locally scoped** to `parent()`, meaning they only exist inside the `parent()` function as local **variables**. In the example above, you cannot call `first_child()` directly. Whenever you call `parent()`, the inner functions `first_child()` and `second_child()` are also called. But because of their local scope, they aren't available outside of the `parent()` function. 

<br>

_**Functions as Return Variables**_

Python also allows you to return functions from functions. Update `inner_functions.py`:



```python
# Update inner_functions.py
def parent(num):
    def first_child():
        return "Hi, I'm Elias"

    def second_child():
        return "Call me Esther"

    if num == 1:
        return first_child
    else:
        return second_child
```

Note that you're returning `first_child` without the parentheses. Recall that this means that you're **returning a reference to the function** `first_child`. In contrast, `first_child()` with parentheses refers to the result of evaluating the function: 


```python
first = parent(1)
second = parent(2)

first
```




    <function __main__.parent.<locals>.second_child()>




```python
second
```




    <function __main__.parent.<locals>.second_child()>



This somewhat cryptic output means that the `first` variable refers to the local `first_child()` function inside of `parent()`, while `second` points to `second_child()`. You can now use `first` and `second` as if they're regular functions, even though you can't directly access the functions they point to: 


```python
first()
```




    "Hi, I'm Elias"




```python
second()
```




    'Call me Esther'



<br>

### Wrappers and Decorators in Python


#### Wrappers

We use *wrappers* in Python when we want to modify or extend the behavior of an existing function, method, or class without modifying its source code. **Wrappers** are functions or classes that encapsulate -- or "wrap" -- the behavior of another function. They provide a layer around the original functionality, allowing you to modify or extend behavior without altering the core implementation. 


```python
# hello_decorator.py
def hello_wrapper(func):
    def wrapper():
        print("Something is happening before the function is called.")
        func()
        print("Something is happening after the function is called.")
    return wrapper

def say_whee():
    print("Whee!")

say_whee = hello_wrapper(say_whee)
```

Here, we've defined two regular functions -- `hello_wrapper()` and `say_whee()` -- and one inner `wrapper()` function. Then we redefined `say_whee()` to apply `hello_wrapper()` to the original `say_whee()`:


```python
say_whee()
```

    Something is happening before the function is called.
    Whee!
    Something is happening after the function is called.


The wrapper happens at the following line:

`say_whee = hello_wrapper(say_whee)`

In effect, the name `say_whee` now points to the `wrapper()` inner function. Remember that you return `wrapper` as a function when you call `hello_wrapper(say_whee)`:


```python
say_whee
```




    <function __main__.hello_wrapper.<locals>.wrapper()>



However, wrapper() has a reference to the original `say_whee()` as `func`, and it calls that function between the two calls to `print()`. 

Because `wrapper()` is a regular Python function, the way it modifies a function can change dynamically: 


```python
# quiet_night.py
from datetime import datetime

def not_during_the_night(func):
    def wrapper():
        if 7 <= datetime.now().hour < 22:
            func()
        else:
            pass   # Hush, the neighbors are asleep
    return wrapper

def say_whee():
    print("Whee!")

say_whee = not_during_the_night(say_whee)

say_whee()
```

    Whee!


If you try to call `say_whee()` after bedtime, nothing will happen because the `if()` test failed so the `wrapper()` didn't call `func`, the original `say_whee`.

Typical use cases of wrappers are tasks such as logging, timing, or error-handling.  

In the below example, try to predict what order the print functions will occur before running: 
# A more complicated example:

def example_wrapper(func):
    print("'example_wrapper' has been called")

    def wrapper(*arg, **kwarg):
        print("'wrapper' before function execution")

        # Print arguments and keyword arguments of the wrapped function
        print('Arguments:', *arg)
        print('Keyword arguments:', **kwarg)

        # Calling the wrapper function
        func(*arg, **kwarg)

        print("'wrapper' after function execution")
    print("Moving to 'wrapper' now")
    return wrapper

# Defining a simple function to be called inside wrapper
def print_function(string):
    print("Inside 'print_function' now")
    print(string)

# Wrapping the `print_function` with the `example_wrapper`, 
#    creating a new wrapped function with extended functionality
wrapped_print_function = example_wrapper(print_function)

# Calling the wrapped print function
wrapped_print_function("Hello, World!")

```python
# A more complicated example:

def example_wrapper(func):
    print("'example_wrapper' has been called")

    def wrapper(*arg, **kwarg):
        print("'wrapper' before function execution")

        # Print arguments and keyword arguments of the wrapped function
        print('Arguments:', *arg)
        print('Keyword arguments:', **kwarg)

        # Calling the wrapper function
        func(*arg, **kwarg)

        print("'wrapper' after function execution")
    print("Moving to 'wrapper' now")
    return wrapper

# Defining a simple function to be called inside wrapper
def print_function(string):
    print("Inside 'print_function' now")
    print(string)

# Wrapping the `print_function` with the `example_wrapper`, 
#    creating a new wrapped function with extended functionality
wrapped_print_function = example_wrapper(print_function)

# Calling the wrapped print function
wrapped_print_function("Hello, World!")
```

    'example_wrapper' has been called
    Moving to 'wrapper' now
    'wrapper' before function execution
    Arguments: Hello, World!
    Keyword arguments:
    Inside 'print_function' now
    Hello, World!
    'wrapper' after function execution


The call `wrapped_print_function("Hello, World!")` has `arg` = `"Hello, World!"` and no `kwarg`s. 

This two-layer structure is common for wrappers: 

1. **Outer layer** (i.e., `example_wrapper`)
    - The actual wrapper function, takes another function (`func`) as its argument
    - Defines and returns the inner layer (`wrapper`) function
    - Can perform setup, configuration, or any other logic that needs to be done once when applying the decorator.
  

2. **Inner layer** (i.e., `wrapper`)

    - Wrapper function that is returned by the outer layer. It is the actual function that wraps around the original function (`func`).
    - Adds or modifies behavior before and/or after calling the original function
    - Often calls the original function (`func`) somewhere within its body.
    - Defining the inputs `*arg` and `**kwarg` enables accessing all arguments of the input function, which is possible because `wrapper` is contained in `example_wrapper`, which in turn has `func` as its input.
    - The layer can access the arguments and results of the original function and perform additional actions.
  
The actual wrapping was peformed by creating a new function via

`wrapped_print_function = example_wrapper(print_function)`

We could continue adding functionality via wrappers, but this can get messy and confusing

<br> 

#### Decorators

Creating explicit wrapped functions and calling them instead of the originals is often not ideal, especially when we're interested in increasing functionality for testing and development without extending that behavior into the production version. 

The `@decorator` syntax, sometimes called _pie syntax_, offers a clean and readable way to wrap functions to easily apply (and remove) a wrapper to a specific function 

Let's examine the previous example more deeply: 


```python
# Defining a wrapper function
def example_wrapper(func):
    print("'example_wrapper' has been called")

    def wrapper(*arg, **kwarg):
        print("'wrapper' before function exection")

        # Print arguments and keyword arguments of the wrapped function
        print('Arguments:', *arg)
        print('Keyword arguments:', **kwarg)

        # Calling the wrapper function
        func(*arg, **kwarg)

        print("'wrapper' after function execution")
        
    print("Moving to 'wrapper' now")
    return wrapper

# Defining a simple function to be called inside wrapper
def print_function(string):
    print("Inside 'print_function' now")
    print(string)

# Wrapping the "print_function" with the 'example wrapper', 
#  creating a new wrapped function with extended functionality
wrapped_print_function = example_wrapper(print_function)
```

    'example_wrapper' has been called
    Moving to 'wrapper' now


What do we expect to happen when we call this function? If we call: 

`wrapped_print_function("Hello, World!")`

1) `arg` = "Hello, World!", `kwarg` = <empty>
2) `wrapped_print_function = example_wrapper(print_function)` and `print_function("Hello, World!") =`
   > Inside 'print_function' now
   > 
   > Hello, World!
3) `wrapped_print_function("Hello, World!") = example_wrapper(print_function("Hello, World!") = example_wrapper(arg = "Hello, World!", func = print_function)`
4) Order of execution in example_wrapper:  1) print("`example_wrapper` has been called")

                                      2) wrapper: print("`wrapper` before function execution")
   
                                                  print("`Arguments:` "Hello, World!")
   
                                                  print("Keyword arguments:`)
   
                                                  func(*arg, **kwarg) = print_function("Hello, World!")
   
                                                  print("`wrapper` after function execution")

                                       3) print("Moving to `wrapper` now")

                                       4) return wrapper

5) `example_wrapper(arg = "Hello, World!", func = print_function)` will lead to the following output:

   > `example_wrapper` has been called    (first line in example_wrapper)
   > 
   > Moving to `wrapper` now              (skip output of wrapper until called)
   > 
   > `wrapper` before function execution  (NOW execute wrapper)
   > 
   > Arguments: Hello, World!
   > 
   > Keyword arguments:
   > 
   > Inside 'print_function' now
   > 
   > Hello, World!
   > 
   > `wrapper` after function execution   (Completion of wrapper output

   


```python
# Calling the wrapped print function
wrapped_print_function("Hello, World!")
```

    'wrapper' before function exection
    Arguments: Hello, World!
    Keyword arguments:
    Inside 'print_function' now
    Hello, World!
    'wrapper' after function execution


<br>

The same function using decorator syntax: 


```python
# Defining a wrapper function
def example_wrapper(func):
    print("'example_wrapper' has been called")

    def wrapper(*arg, **kwarg):
        print("'wrapper' before function execution")

        # Print arguments and keyword arguments of the wrapped function
        print('arguments:', *arg)
        print('keyword arguments:', **kwarg)

        # Calling the wrapper function
        func(*arg, **kwarg)

        print("'wrapper' after function execution")
    print("Moving to 'wrapper' now")
    return wrapper

# Defining a simple function, to be called inside wrapper
@example_wrapper        # Replaces wrapped_print_function = example_wrapper(print_function)
def print_function(string):
    print("inside 'print_function' now")
    print(string)

# Calling the wrapped print function
print_function("Hello, World!")
```

    'example_wrapper' has been called
    Moving to 'wrapper' now
    'wrapper' before function execution
    arguments: Hello, World!
    keyword arguments:
    inside 'print_function' now
    Hello, World!
    'wrapper' after function execution


We added `@example_wrapper` to decorate the original print function, replacing the original wrapping statement `wrapped_print_function = example_wrapper(print_function)` and need to call `wrapped_print_function("Hello, World!")`. Now `print_function("Hello, World!")` achieves the same outputs. _**If the wrapper ever loses its purpose, we can simply remove the decorator.**_

Note it is possible to **stack multiple decorators**: 
@log_wrapper
@timing_wrapper
def print_function(string)
    print(string)
When working with more extensive stacks of decorators, it is important to keep in mind the _**ordering of decorators, as well as potential interactions between them.**_

<br> 

**When do we use wrappers and decorators?**

We use wrappers in Python when we want to modify or extend the behavior of an existing function, method, or class without modifying its source code. There are several use cases for wrappers, including: 

_**Adding functionality:**_ Wrappers can be used to log input and output parameters:


```python
def log_wrapper(func):
    def wrapper(*args, **kwargs):
        result = func(*args, **kwargs)
        print(f"Function {func.__name__} called with arguments {args} and result {result}")
        return result
    return wrapper

@log_wrapper
def add(a, b):
    return a + b

result = add(3, 4)
```

    Function add called with arguments (3, 4) and result 7


<br>

A wrapper can also be used to measure time before and after running a function: 


```python
import time

def timing_wrapper(func):
    def wrapper(*args, **kwargs):
        start_time = time.time()
        result = func(*args, **kwargs)
        end_time = time.time()
        print(f"{func.__name__} took {end_time - start_time} seconds to execute")
        return result
    return wrapper

@timing_wrapper
def slow_function():
    time.sleep(2)
    print("Function executed")

slow_function()
```

    Function executed
    slow_function took 2.0005719661712646 seconds to execute


<br>

_**Modifying behavior:**_ A wrapper can transform output into a string: 


```python
def transform_output_wrapper(func):
    def wrapper(*args, **kwargs):
        result = func(*args, **kwargs)
        return str(result)    # Transforming the output to a string
    return wrapper

@transform_output_wrapper
def multiply(a, b):
    return a * b

result = multiply(3, 4)
type(result)
```




    str



_**Maintaining consistency:**_ Wrappers can be employed to ensure consistency across multiple functions by, for instance, standardizing input and output formats, applying uniform error handling, or employing validation logic. The example below _standardizes all input arguments as strings_. 


```python
def standardize_input_wrapper(func):
    def wrapper(*args, **kwargs):
        standardized_args = [str(arg) for arg in args]
        standardized_kwargs = {key: str(value) for key, value in kwargs.items()}
        return func(*standardized_args, **standardized_kwargs)
    return wrapper

@standardize_input_wrapper
def concatenate_strings(a, b):
    return a + b

concatenate_strings(3, 4)
```




    '34'



_**Controlling security:**_ Security features, such as access control or data encription, can be introduced using wrappers. For example, a wrapper may be designed to check user permissions before executing a function or encrypt sensitive data before passing it to a function. In the example below, the wrapper verifies whether the user has the "execute" permission: 
def secure_access_wrapper(func):
    def wrapper(user, *args, **kwargs):
        if user.has_permission("execute"):
            result = func(*args, **kwargs)
            return result
        else:
            raise PermissionError("User does not have permission to execute this function")
    return wrapper

class SecureCalculator:
    @secure_access_wrapper
    def add(self, a, b):
        return a + b

user = User("admin", ["execute"])
calculator = SecureCalculator()
result = calculator.add(user, 3, 4)
<br>

_**Reusing decorators:**_ Recall that a decorator is just a regular Python function. All the usual tools for reusability are available. Now we'll create a module to store decorators to use in many other functions. 


```python
# decorators.py
def do_twice(func):
    def wrapper_do_twice():
        func()
        func()
    return wrapper_do_twice
```

You can now use this new decorator in other files by doing a regular **import**:


```python
@do_twice
def say_whee():
    print("Whee")

say_whee()
```

    Whee
    Whee


<br>

### Decorating Functions with Arguments (*args and **kwargs)

*args and **kwargs allow decorators to take in unspecified numbers of inputs (including none). 

_**Returning Values from Decorated Functions:**_ 


```python
@do_twice
def return_greeting(name):
    print("Creating greeting")
    return f"Hi {name}"
```

This didn't output anything because `do_twice` does not explicitly return the return value of the decorated function. Let's modify `decorators.py` to utilize `*args` and `**kwargs`:


```python
# decorators.py
def do_twice(func):
    def wrapper_do_twice(*args, **kwargs):
        func(*args, **kwargs)
        return func(*args, **kwargs)
    return wrapper_do_twice
```

Now:


```python
@do_twice
def return_greeting(name):
    print("Creating greeting")
    return f"Hi {name}"

return_greeting("Adam")
```

    Creating greeting
    Creating greeting





    'Hi Adam'



_**`@functools.wraps` Decorator:**_ Will preserve information about the original function: 


```python
# decorators.py
import functools

def do_twice(func):
    @functools.wraps(func)
    def wrapper_do_twice(*args, **kwargs):
        func(*args, **kwargs)
        return func(*args, **kwargs)
    return wrapper_do_twice
```


```python
@do_twice
def say_whee():
    print("Whee!")
```


```python
say_whee
```




    <function __main__.say_whee()>




```python
say_whee.__name__
```




    'say_whee'




```python
help(say_whee)
```

    Help on function say_whee in module __main__:
    
    say_whee()
    


Now `say_whee()` is still itself after decoration

<br> 

### More About *args and **kwargs

*args and **kwargs allow you to pass multiple arguments or keyword arguments to be a function. 


```python
def my_sum(a, b):
    return a + b
```

One can pass a varying number of arguments to a function by passing a list or a set of all the arguments to your function:


```python
def my_sum(my_integers):
    result = 0
    for x in my_integers:
        result += x
    return result

list_of_integers = [1, 2, 3]
print(my_sum(list_of_integers))
```

    6


This implementation works but whenever you call this function you'll also need to create a list of arguments to pass to it. This is where `*args` can be really useful because it allows you to pass a varying number of positional arguments: 


```python
def my_sum(*args):
    result = 0
    #Iterating over the Python args tuple
    for x in args: 
        result += x
    return result

print(my_sum(1, 2, 3))
```

    6


`my_sum()` now takes all the parameters that are provided in the input and packs them into a single iterable object named `args`. 

Note that **`*args` is just a name.** You're not required to use the name `args`:


```python
def my_sum(*integers):
    result = 0
    for x in integers:
        result += x
    return result

print(my_sum(1, 2, 3))
```

    6


All that matters is that you use the **unpacking operator (*)**. The iterable object you'll get using the unpacking operator * is not a list but a tuple. A **tuple** is similar to a list in that they both support slicing and iteration. However, tuples are very different in at least one respect: lists are _mutable_ while tuples are not: 


```python
my_list = [1, 2, 3]  # lists are mutable
my_list[0] = 9
print(my_list)
```

    [9, 2, 3]



```python
my_tuple = (1, 2, 3)
#my_tuple[0] = 9        # tuples are not mutable. Will throw an error
#print(my_tuple)      
```

<br>

### Using the Python kwargs Variable in Function Definitions

`**kwargs` works just like `*args`, but instead of accepting positional arguments it accepts keyword (or _named_) arguments:


```python
def concatenate(**kwargs):
    result = ""
    #Iterating over the Python kwargs dictionary
    for arg in kwargs.values():
        result += arg
    return result

print(concatenate(a="Real", b="Python", c="Is", d="Great", e="!"))
```

    RealPythonIsGreat!


`concatenate()` iterates through the Python kwargs _**dictionary**_ and concatenate all the values it finds. 

Like `args`, `kwargs` is just a name that can be changed to whatever you want. Again, what is important here is the use of the **unpacking operator(\**).** So the previous example could be written as: 


```python
def concatenate(**words):
    result = ""
    for arg in words.values():
        result += arg
    return result

print(concatenate(a="Real", b="Python", c="Is", d="Great", e="!"))
```

    RealPythonIsGreat!


The `.values()` tag returns values when iterating over a standard `dict`. Without this, you will iterate through the **keys** of the Python kwargs dictionary instead, like below: 


```python
def concatenate(**kwargs):
    result = ""
    #Iterating over the keys of the Python kwargs dictionary
    for arg in kwargs:
        result += arg
    return result

print(concatenate(a="Real", b="Python", c="Is", d="Great", e="!"))
```

    abcde


<br>

### Ordering Arguments in a Function 

Ordering matters - `*args* must come before `**kwargs`. The correct order for your parameters is: 

1. Standard arguments
2. `*args` arguments
3. `**kwargs` arguments


```python
def my_function(a, b, *args, **kwargs):
    pass
```

Changing the order of these arguments will throw an error from the interpreter, such as a `SyntaxError`. 

<br>

### Unpacking with the Asterisk Operator: * & **

The unpacking operators are operators that unpack the values from iterable objects in Python. The single asterisk operator * can be used on any iterable that Python provides, while the double asterisk operator can only be used on dictionaries. 


```python
my_list = [1, 2, 3]
print(my_list)
```

    [1, 2, 3]


This code defines a list and then prints it to the standard output. Note how the list is printed, along with the corresponding brackets and commas. Now, try to prepend the unpacking operator * to the name of your list: 


```python
#print_unpacked_list.py
my_list = [1, 2, 3]
print(*my_list)
```

    1 2 3


Here, the * operator tells `print()` to unpack the list first. In this case, the output is no longer the list itself, but rather **the content** of the list. Another thing you'll notice is that in `print_unpacked_list.py`, you used the unpacking operator * to call a function, instead of in a function definition. In this case, `print()` takes all the items of a list as though they were single arguments. 

You can also use this method to call your own functions, but if your function requires a specific number of arguments. To test this behavior, consider this script: 


```python
def my_sum(a, b, c):
    print(a + b + c)

my_list = [1, 2, 3]
my_sum(*my_list)
```

    6


Here, `my_sum()` explicitly states that `a`, `b`, and `c` are required arguments. When run, you get the sum of the three numbers in `my_list`. The three elements in `my_list` match up perfectly with the required arguments in `my_sum()`. Now look at the following script, where `my_list` has four arguments instead of three: 


```python
def my_sum(a, b, c):
    print(a + b + c)

my_list = [1, 2, 3, 4]
#my_sum(*my_list)
```

This will return an error because `my_sum()` still expects just three arguments but the * operator gets four items from the list. When you use the * operator to unpack a list and pass arguments to a function, it's exactly as though you're passing every single argument alone. This means that you can use multiple unpacking operators to get values from several lists and pass them all to a single function. To test this behavior, consider the following example: 


```python
def my_sum(*args):
    result = 0
    for x in args:
        result += x 
    return result

list1 = [1, 2, 3]
list2 = [4, 5]
list3 = [6, 7, 8, 9]

print(my_sum(*list1, *list2, *list3))
```

    45


When run, all three lists are unpacked and each individual item is passed to `my_sum()`. 

As another example, say you need to split a list into three different parts. The output should show the first value, the last value, and all the values in between. With the unpacking operator, you can do this in just one line of code: 


```python
my_list = [1, 2, 3, 4, 5, 6]
a, *b, c = my_list

print(a)
```

    1



```python
print(b)
```

    [2, 3, 4, 5]



```python
print(c)
```

    6


In this example, `my_list` contains six items. The first variable is assigned to `a`, the last to `c`, and all other values are packed into a new list `b`. 

Another example: 


```python
my_first_list = [1, 2, 3]
my_second_list = [4, 5, 6]
my_merged_list = [*my_first_list, *my_second_list]

print(my_merged_list)
```

    [1, 2, 3, 4, 5, 6]


You can even merge two different dictionaries by using the unpacking operator **: 


```python
my_first_dict = {"A":1, "B":2}
my_second_dict = {"C":3, "D":4}
my_merged_dict = {**my_first_dict, **my_second_dict}

print(my_merged_dict)
```

    {'A': 1, 'B': 2, 'C': 3, 'D': 4}


Remember that the * operator works on _any_ iterable object. It can also be used to unpack a _string_: 


```python
a = [*"RealPython"]
print(a)
```

    ['R', 'e', 'a', 'l', 'P', 'y', 't', 'h', 'o', 'n']


In Python, strings are iterable objects, so * will unpack it and place all individual values in a list `a`. 


```python

```
