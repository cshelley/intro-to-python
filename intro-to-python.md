### Introduction to Python

#### Getting started
1. Download and install Python
2. Download and install a text editor. I chose Brackets.
3. In Brackets, begin a new file. Type: 
print('Hello world')
4. Save the file to your home directory.* Name the file "hello.py". Once saved with the `.py` file extension, your computer knows its a Python script. 

\* NOTE: I could only save to my Desktop so used some command-line to move it to \~

5. Open a Terminal window. Navigate to where the file is stored, if necessary.
6. Type: 
python3 hello.py
7. After hitting `<return>`, `Hello world` will print on the next line(!)

#### Interactive Python: The Chevron Prompt

Typing python3 and <return> at the command-line will enter interactive mode, where Python awaits your command with `>>>`:  
% python3      # enter interactive command line
>>> x = 1
x = 1
>>>print(x)
1
>>>x = x + 1
2
>>>exit()      # exit interactive session and return to command line
Note that Python only uses `=` for left to right assignment and does not support `<-`. 

### Reserved Words

Reserved words have special meaning within Python and cannot be used for variable or function names. 
False    await      else      import    pass     
None     break      except    in        raise    
True     class      finally   is        return   
and      continue   for       lambda    try      
as       def        from      nonlocal  while    
assert   del        global    not       with     
async    elif       if        or        yield    
### `if` Syntax


```python
if x < 10:
    print('small')
```

    small


### `while` Loop


```python
n = 1
while n < 6:
    print(n)
    n = n + 1
```

    1
    2
    3
    4
    5


### Expressions

* **Constants** are fixed values such as numbers, letters, and strings. String constants use single quotes or double quotes.

* A **variable** is a named place in memory where a programmer can store data and later retrieve the data using the variable "name". You can assign the name in one statement and then change the variable's contents in a later statement.

    * _Naming rules\:_: Must start with a letter or underscore (but avoid this), remainder of name must consist of letters, numbers, and underscores. Names are case-sensitive, but all lower-case is preferred.
 
* **Numeric expressions:** Because of the lack of mathematical symbols on computer keyboards, we repurpose available keys:

| Operator |     Operation    |
|:--------:|:----------------:|
|    +     | Addition         |
|    -     | Subtraction      |
|    *     | Multiplication   |
|    /     | Division         |
|    **    | Exponent/Power   |
|    %     | Modulo/Remainder |




In Python, variables, literals, and constants have a "type". For example, `+` means "addition" if something is a number and "concatenate" if something is a string. 


```python
ddd = 1 + 4
print(ddd)
```

    5



```python
eee = 'hello ' + 'there'
print(eee)
```

    hello there


To see type: 


```python
type(eee)
```




    str



Numbers have two main types, "integer" and "float". `int()` and `float()` will coerce an object.  

### User Input


```python
nam = input('Who are you?')  # the input requires user input and returns a STRING
print('Welcome,', nam)
```

    Who are you? Quentin


    Welcome, Quentin


Comments are indicated by `#`. 

### A First Working Program. 

Write this program in your text editor and save as elevator.py. Then run from the command line. 


```python
# convert elevator floors
inp = input('Europe floor?')
usf = int(inp) + 1     # remember to convert from string for addition
print('US floor', usf)
```

    Europe floor? 0


    US floor 1


### An IDE Environment

Working with Brackets is a bit kludgy. A great IDE to use instead is Spyder. To install Spyder, navigate to https://www.spyder-ide.org/ and follow installation instructions. 

Within Spyder, you can type your program in one panel, highlight, and hit 'play', then interact if necessary in a separate console panel. 

### Conditional Statements


```python
x = 5
if x < 10:
    print('smaller')
if x > 20: 
    print('bigger')
print('finis')
```

    smaller
    finis


Anything within the indentation of the `if` statement will be evaluated within the `if` statement. 

#### Comparison Operators

| Python |          Meaning         |
|:------:|:------------------------:|
|   <    | Less than                |
|   <=   | Less than or equal to    |
|   ==   | Equal to                 |
|   >=   | Greater than or equal to |
|   >    | Greater than             |
|   !=   | Not equal                |


**NOTE**: Since Python doesn't use curly brackets in `if` statement like R does, the identing is required! Use **four spaces**, not **tab**!

### `if/else`


```python
if x > 2:
    print('bigger')
else:
    print('smaller')
print('All done')
```

    bigger
    All done


### `elif:`


```python
if x < 2:
    print('small')
elif x < 10:         # elif stays within the original if and continues evaluating
    print('medium')
else:                # else exits the if statement
    print('large')
print('All done')
```

    medium
    All done


### `try/except` Structure: 

To debug, you can surround a dangerous section of code with a `try` and `except`. If the code in the `try` works then the `except` is skipped. If the code in the `try` fails, the program jumps to the `except` section. 


```python
astr = 'Hello Bob'
instr = int(astr)
print('First', istr)
astr = '123'
istr = int(astr)
print('Second', istr)
```


    ---------------------------------------------------------------------------

    ValueError                                Traceback (most recent call last)

    Cell In[17], line 2
          1 astr = 'Hello Bob'
    ----> 2 instr = int(astr)
          3 print('First', istr)
          4 astr = '123'


    ValueError: invalid literal for int() with base 10: 'Hello Bob'



```python
# returns a traceback error @line 2 and not evaluate further
```

With `try/except`: 


```python
astr = 'Hello Bob'
try:                  # when the first conversion fails it just drops into the except clause and the program continues
    istr = int(astr)
except:
    istr = -1
print('First', istr)
```

    First -1



```python
astr = '123'
try:
    istr = int(astr)
except:                # when the second conversion succeeds it just skips the except clause and the program continues
    istr = -1
print('Second', istr)
```

    Second 123


`try/except` will not return a traceback error, so write your `except` smartly to help find the error. 

Here's a more useful example: 


```python
rawstr = input('Enter a number:')  # Execute: 
try:                               #    Enter a number: 42
    ival = int(rawstr)             #    Nice work
except:
    ival = -1                      #    Enter a number: forty-two
                                   #    Not a number
if ival > 0:
    print('Nice work')
else:
    print('Not a number')
```

### Functions

Functions are steps that are stored and reused. They take the basic form: 
def function_name():
    <do ....>

```python
def plus_one(x):
    y = x + 1 
    return y

plus_one(10)
```




    11



Python can nest returns within `if` statements: 


```python
def greet(lang):
    if lang == 'es':
        return 'Hola'
    elif lang == 'fr':
        return 'Bonjour'
    else:
        return 'Hello'

print(greet('en'), 'Glenn')
```

    Hello Glenn


### Repeated (Indefinite) Loops, `while` Construct


```python
n = 5
while n > 0:
    print(n)
    n = n - 1
print('Blastoff!')
print(n)
```

    5
    4
    3
    2
    1
    Blastoff!
    0


Breaking out of a loop: 
while True:
    line = input('> ')
    if line == 'done':  # here the loop will execute forever until input exactly matches 'done'
        break
    print(line)
print('Done!')while True:
    line = input('> ')
    if line[0] == '#':
        continue        # continue abandons the current iteration and goes to the next thing
    if line == 'done':
        break
    print(line)
print('Done!')
### Definite Loops: `for` construct


```python
for i in [5, 4, 3, 2, 1]:
    print(i)
print('Blastoff!')
```

    5
    4
    3
    2
    1
    Blastoff!



```python

```
