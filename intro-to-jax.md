### INSTALLING JUPYTER

1. On the command line, install JupyterLab with `pip`:
pip install jupyterlab
2. Launch with
jupyter lab
This will open a locally-hosted browser page. Start a new project by selecting the Python 3 (pykernel) tile under "Notebook". 

_(Note: That's how to launch JupyterLab every time you want to use it.)_

#### `import`:

In Python, you use the `import` keyword to make code in one module availabine in another. 

Python code is organized into both **modules** and **packages**. 

> A **module** is an object that serves as an organizational unit of Python code. Modules have a **namespace** containing arbitrary Python objects. Modules are loaded into Python by the process of importing.

In practice, a module usually corresponds to one .py file containing Python code. The true power of modules is that they can be imported and reused in other code. 


```python
# Example: 
import math    # import math module
math.pi        # call the object pi within math
```




    3.141592653589793



In the first line, `import math`, you import the code in the `math` module and make it available to use. In the second line, you access the `pi` variable within the `math` module. `math` is part of Python's standard library, which means that it's always available to import when you're running Python. 

Note that you write `math.pi` and not just simply `pi`. In addition to being a module, `math` acts as a **namespace** that keeps all the attributes of the module together. Namespaces are useful for keeping your code readable and organized. 

You can test the contents of a namespace with `dir()`:


```python
import math
dir()        # using dir() without any arguments shows what's in the global namespace
```




    ['In',
     'Out',
     '_',
     '_4',
     '_5',
     '_6',
     '_8',
     '__',
     '___',
     '__builtin__',
     '__builtins__',
     '__doc__',
     '__loader__',
     '__name__',
     '__package__',
     '__spec__',
     '_dh',
     '_exit_code',
     '_i',
     '_i1',
     '_i2',
     '_i3',
     '_i4',
     '_i5',
     '_i6',
     '_i7',
     '_i8',
     '_i9',
     '_ih',
     '_ii',
     '_iii',
     '_oh',
     'exit',
     'get_ipython',
     'grad',
     'jit',
     'jnp',
     'key',
     'math',
     'open',
     'quit',
     'random',
     'vmap',
     'x']




```python
dir(math)
```




    ['__doc__',
     '__file__',
     '__loader__',
     '__name__',
     '__package__',
     '__spec__',
     'acos',
     'acosh',
     'asin',
     'asinh',
     'atan',
     'atan2',
     'atanh',
     'cbrt',
     'ceil',
     'comb',
     'copysign',
     'cos',
     'cosh',
     'degrees',
     'dist',
     'e',
     'erf',
     'erfc',
     'exp',
     'exp2',
     'expm1',
     'fabs',
     'factorial',
     'floor',
     'fmod',
     'frexp',
     'fsum',
     'gamma',
     'gcd',
     'hypot',
     'inf',
     'isclose',
     'isfinite',
     'isinf',
     'isnan',
     'isqrt',
     'lcm',
     'ldexp',
     'lgamma',
     'log',
     'log10',
     'log1p',
     'log2',
     'modf',
     'nan',
     'nextafter',
     'perm',
     'pi',
     'pow',
     'prod',
     'radians',
     'remainder',
     'sin',
     'sinh',
     'sqrt',
     'tan',
     'tanh',
     'tau',
     'trunc',
     'ulp']



The following code imports only the `pi` variable from the `math` module: 


```python
from math import pi
pi
```




    3.141592653589793


math.piNameError: name math is not defined
Note that this places `pi` in the global namespace and not within a `math` namespace. 

You can also rename modules and attributes as they're imported: 


```python
import math as m
m.pi
```




    3.141592653589793




```python
from math import pi as PI
PI
```




    3.141592653589793



You can use a **package** to further organize your modules. 

> A **package** is a Python module that can contain submodules or, recurseively, subpackages. 

Note that a package is still a module. In practice, a package typically corresponds to a file directory containing Python files and other directories. In general, submodules and subpackages aren't imported when you import a package. 


### INSTALLING JAX

In a Jupyter Notebook cell: 
!pip install jax
You only need to run that once, so after it runs successfully, switch the cell type to "raw" so that you still have it if you need to re-run in the future. 

### JAX Quickstart

_Source: JAX Quickstart: https://jax.readthedocs.io/en/latest/notebooks/quickstart.html_


```python
import jax.numpy as jnp
from jax import grad, jit, vmap
from jax import random
```

* jit() speeds up your code
* grad() takes derivatives
* vmap() for automatic vectorizatio or batching

#### Using JIT to speed up functions: 

If we have a sequence of operations, we can use the `@jit` decorator to compile multiple operations together using XLA. 

> **Decorators** in Python allow programmers to modify the behavior of a function or class.

> **XLA** (Accelerated Linear Algebra) is an open-source machine learning (ML) compiler for GPUs, CPUs, and ML accelerators. The XLA compiler takes models from popular ML frameworks such as PyTorch, TensorFlow, and JAX, and optimizes them for high-performance execution across different hardware platforms including GPUs, CPUs, and ML accelerators.


```python
def selu(x, alpha = 1.67, lmbda = 1.05):
    return lmbda * jnp.where(x > 0, x, alpha * jnp.exp(x) - alpha)

x = random.normal(key, (1000000, ))
%timeit selu(x).block_until_ready()
```

    8.92 ms ± 1.58 ms per loop (mean ± std. dev. of 7 runs, 100 loops each)


This can be sped up with `@jit`, which will jit-compile the first time `selu` is called and will be cached thereafter. 


```python
selu_jit = jit(selu)
%timeit selu_jit(x).block_until_ready()
```

    2.93 ms ± 109 µs per loop (mean ± std. dev. of 7 runs, 1,000 loops each)


#### Taking derivatives with `grad()`

Automatic differentiation (auto-differentiation, autodiff, or AD) is a set of techniques to evaluate the partial derivative of a function specified by a computer program. 

#### Multiplying Matrices


```python
key = random.PRNGKey(0)
x = random.normal(key, (10,))
print(x)
```

    [-0.3721109   0.26423115 -0.18252768 -0.7368197  -0.44030377 -0.1521442
     -0.67135346 -0.5908641   0.73168886  0.5673026 ]



```python
help(random.PRNGKey)  # to get help on any function
  # The zero input above was the set.seed
```

    Help on function PRNGKey in module jax._src.random:
    
    PRNGKey(seed: 'int | ArrayLike', *, impl: 'PRNGSpecDesc | None' = None) -> 'KeyArray'
        Create a pseudo-random number generator (PRNG) key given an integer seed.
        
        The resulting key carries the default PRNG implementation, as
        determined by the optional ``impl`` argument or, otherwise, by the
        ``jax_default_prng_impl`` config flag.
        
        Args:
          seed: a 64- or 32-bit integer used as the value of the key.
          impl: optional string specifying the PRNG implementation (e.g.
            ``'threefry2x32'``)
        
        Returns:
          A PRNG key, consumable by random functions as well as ``split``
          and ``fold_in``.
    


**Multiplying two big matrices:**


```python
size = 3000
x = random.normal(key, (size, size), dtype = jnp.float32)
```


```python
x
```




    Array([[-0.9290555 ,  0.85166323,  0.20667695, ...,  0.5367289 ,
             0.41531488,  1.2022016 ],
           [ 0.32031205, -0.15079641, -0.0241428 , ..., -0.82786137,
             1.5355531 , -1.2260039 ],
           [ 0.7273939 ,  1.2432809 ,  1.7800838 , ..., -0.34443098,
             1.0664394 , -1.1610765 ],
           ...,
           [-1.4628237 ,  1.0260845 ,  1.47854   , ..., -0.07614775,
            -1.6880821 ,  1.0994167 ],
           [-1.1308681 , -1.5304328 , -0.25091794, ...,  0.6202619 ,
            -1.5918293 , -0.7086028 ],
           [-0.03936769, -0.4169054 , -0.49644423, ...,  1.8154075 ,
            -0.12063057, -0.3610393 ]], dtype=float32)


