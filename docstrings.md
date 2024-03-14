### Docstring

_Sources:_

1. _Docstring (https://en.wikipedia.org/wiki/Docstring)_
2. _Python Docstrings (https://www.geeksforgeeks.org/python-docstrings/)_

***

<br>

**Docstrings**, short for documentation strings, provide a convenient way of associating documentation with Python modules, functions, classes, and methods. Docstrings are string literals specified in source code that are used, like a comment, to document a specific segment of code. Unlike conventional source code comments, the docstring should describe what the function does, not how. Docstrings are not stripped from the source tree when it is parsed and are retained throughout the runtime of the program. This allows the programmer to inspect these comments at runtime, for instance as an interactive help system, or as metadata. 

Common practice in Python is to document a code object at the head of its definition. The docstring of that code object, is the first statement of that code object, immediately following the definition (the `def` or `class` statement). The statement must be a bare string literal, not any other kind of expression. The docstring for the code object is available on that code object's `__doc__` attribute and through the `help` function. 

A first example: 


```python
"""The module's docstring"""
class MyClass: 
    """The class's docstring"""

    def my_method(self):
        """The method's docstring"""

def my_function():
    """The function's docstring"""
```

Assuming the above code was saved as `mymodule.py`, the following is an interactive session showing how the docstrings may be accessed: 


```python
# >>>import mymodule
# >>>help(mymodule)
# The module's docstring
# >>>help(mymodule.MyClass)
# The class's docstring
# >>>help(mymodule.MyClass.my_method)
# The method's docstring
# >>>help(mymodule.my_function)
# The function's docstring
```

**Declaring Docstrings.** 

The docstrings are declared using triple single quotes (''' ''') or triple double quotes (""" """) just below the class, method, or function declaration. _**All functions should have a docstring.**_

<br>

**Accessing Docstrings.** 
The docstrings can be accessed using the `__doc__` method of the object or using the help function. 

<br>

**Best Practices:**

* The docstring line should begin with a capital letter and end with a period.
* The first line should be a short description.
* If there are more lines in the documentation string, the second line should be blank, visually separating the summary from the rest of the description.
* The following lines should be one or more paragraphs describing the object's calling conventions, side effects. etc.

<br>

**Types of Docstrings:**

1. _**Triple-quoted strings:**_ the most common docstring format in Python. Triple-quoted strings can span multiple lines and are often placed immediately below the function, class, or module definition. 


```python
def add_numbers(a:int, b:int): 
    """ Adds two integers together. 

    Args: 
        a: First integer.
        b: Second integer.

    Returns: 
        Sum of the two integers. 
    """
    return a + b

add_numbers(3, 2)
```




    5



2. _**Google-style docstrings**_ place a new line after the initial triple single (or double) quotes and a new line after the final triple single (or double) quotes: 


```python
def multiply_numbers(a, b): 
    """
    Multiplies two numbers and returns the result. 

    Args: 
        a (int): The first number. 
        b (int): The second number. 

    Returns:
        int: The product of a and b
    """
    return a*b

print(multiply_numbers(3,5))
```

    15


3. _**Numpydoc-style docstrings**_ are widely used in the scientific and data analysis community, particularly for documenting functions and classes related to numerical computations and data manipulation. It is an extension of Google-style docstrings, with some additional conventions for documenting parameters and return values. 


```python
 def divide_numbers(a, b):
     """
     Divide two numbers. 

     Parameters
     ----------
     a : float
         The dividend.
     b : float
         The divisor.

     Returns
     -------
     float
         The quotient of the division.
     """
     if b == 0:
         raise ValueError("Division by zero is not allowed.")
     return a / b

print(divide_numbers(3,6))
```

    0.5


4. _**One-line docstrings**_ fit in one line. They are used in obvious cases. The closing quotes are on the same line as the opening quotes. 


```python
def power(a, b):
    '''Returns arg1 raised to power arg2.'''

    return a**b

print(power.__doc__)
```

    Returns arg1 raised to power arg2.


5. _**Multi-line docstrings**_ consist of a summary line just like a one-line docstring, followed by a blank line, followed by a more elaborate description. The summary line may be on the same line as the opening quotes or on the next line. 


```python
def subtract_numbers(a, b):
    """
    This function takes two numbers as input and returns their difference.

    Parameters:
    a (int): The first number. 
    b (int): The second number. 

    Returns: 
    int: The difference of a and b. 
    """
    return a - b

print(subtract_numbers(3, 5))
```

    -2


_**Indentation in Docstrings**_. 

The entire docstring is indented the same as the quotes in the first line. Docstring processing tools will strip a uniform amount of indentation from the second and further lines of the docstring, equal to the minimum indentation of all non-blank lines after the first line. Any indentation in the first line of the docstring (i.e., up to the first new line) is insignificant and removed. Relative indentation of later lines in the docstring is retained.  


```python
class Employee:
    """
    A class representing an employee.

    Attributes: 
        name (str): The name of the employee. 
        age (int): The age of the employee. 
        department (str): The department the employee works in. 
        salary (float): The salary of the employee. 
    """

    def __init__(self, name, age, department, salary): 
        """
        Initializes an Employee object. 

        Parameters: 
            name (str): The name of the employee. 
            age (int): The age of the employee. 
            department (str): The department the employee works in. 
            salary (float): The salary of the employee. 
        """
        self.name = name
        self.age = age
        self.department = department
        self.salary = salary

    def promote(self, raise_amount):
        """
        Promotes the employee and increases their salary. 

        Parameters: 
            raise_amount (float): The raise amount to increase their salary. 

        Returns: 
            str: A message indicating the promotion and new salary. 
        """
        self.salary += raise_amount
        return f"{self.name} has been promoted! New salary: ${self.salary:.2f}"

    def retire(self):
        """
        Marks the employee as retired. 

        Returns: 
            str: A message indicating the retirement status. 
        """
        # Some implementation for retiring an employee
        return f"{self.name} has retired. Thank you for your service!"

# Access the Class docstring using help()
help(Employee)
    
```

    Help on class Employee in module __main__:
    
    class Employee(builtins.object)
     |  Employee(name, age, department, salary)
     |  
     |  A class representing an employee.
     |  
     |  Attributes: 
     |      name (str): The name of the employee. 
     |      age (int): The age of the employee. 
     |      department (str): The department the employee works in. 
     |      salary (float): The salary of the employee.
     |  
     |  Methods defined here:
     |  
     |  __init__(self, name, age, department, salary)
     |      Initializes an Employee object. 
     |      
     |      Parameters: 
     |          name (str): The name of the employee. 
     |          age (int): The age of the employee. 
     |          department (str): The department the employee works in. 
     |          salary (float): The salary of the employee.
     |  
     |  promote(self, raise_amount)
     |      Promotes the employee and increases their salary. 
     |      
     |      Parameters: 
     |          raise_amount (float): The raise amount to increase their salary. 
     |      
     |      Returns: 
     |          str: A message indicating the promotion and new salary.
     |  
     |  retire(self)
     |      Marks the employee as retired. 
     |      
     |      Returns: 
     |          str: A message indicating the retirement status.
     |  
     |  ----------------------------------------------------------------------
     |  Data descriptors defined here:
     |  
     |  __dict__
     |      dictionary for instance variables (if defined)
     |  
     |  __weakref__
     |      list of weak references to the object (if defined)
    

