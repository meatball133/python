## Scopes

In programming languages, a scope is a area of a program where you can access a **name** such as a variable, object, or function. In Python, there are two types of scopes: global, local, enclosing scope, and built-in scope.

Scopes are important because it separates names in different areas of a program so that names in one area do not conflict with names in another area.
Which gives the benefit of making the code easier to debug and understand.

If you can access a name in your current scope, it is called a **in scope**.
If you can't, it is called a **out of scope**.

Python follows the **LEGB rule** to determine the scope of a name.
It stands for **L**ocal, **E**nclosing, **G**lobal, and **B**uilt-in.
Which means that python looks up a name in that order.
If it can't find the name, it will throw a `NameError`.

### Global Scope

A variable defined in the main body of a Python file is a global variable and belongs to the global scope. This means that global variables can be accessed inside or outside of functions.

```python
>>> message = "I am global"

>>> message
"I am global"

>>> def greet():
...     print(message)

>>> greet()
"I am global"
```

### Local Scope

A name defined inside a function or [`lambda`][lambda] belongs to the **local scope** of that function, and can only be accessed inside that function.

```python
>>> def greet():
...     message = "I am local"
...     print(message)

>>> greet()
"I am local"
```

If you try to access a local variable in the global scope, you will get an error:

```python

>>> def greet():
...     message = "I am local"

>>> message
NameError: name 'message' is not defined
```

That is because when a function returns, the local scope is destroyed, and with it the local variables.

### Enclosing scope (nonlocal)

Enclosing scope is a scope that exists for nested functions.
If the inner function is the local scope then the enclosing scope is the scope of the outer function.

```python
>>> def outer():
...     message = "I am enclosing"
...     def inner():
...         print(message)
...     inner()

>>> outer()
"I am enclosing"
```

### Built-in scope

The built-in scope is a special scope that Python creates when it starts up.
It contains names such as [`print`][print], [`len`][len], and [`input`][input].

## Modifying behavior of scopes

Python allows you to modify the behavior of scopes by using the [`global`][global] and [`nonlocal`][nonlocal] keywords.

### Global

The [`global`][global] keyword allows you to modify a global variable from within a function.
To do this, you must use the [`global`][global] keyword before the variable name.

```python
>>> message = "I am global"

>>> def greet():
...     global message
...     message = "I am global, but modified"

>>> greet()

>>> message
"I am global, but modified"
```

### Nonlocal

Nonlocal works very similarly to global, but for enclosing scopes instead of the global scope.
The [`nonlocal`][nonlocal] keyword allows you to modify a variable in the enclosing scope from within a nested function.
To do this, you must use the [`nonlocal`][nonlocal] keyword before the variable name.

```python
>>> def outer():
...     message = "I am enclosing"
...     def inner():
...         nonlocal message
...         message = "I am enclosing, but modified"
...     inner()
...     print(message)

>>> outer()
"I am enclosing, but modified"
```

## Return statement

All functions in python returns a value or object.
To specify what value or object a function should return to the caller, you use the [`return`][return] statement.
Since everything is an object in python, you can return anything from a function.
To use the `return` statement, you simply write `return` followed by the value or object you want to return.
The `return` can only be used inside a function.

```python
>>> def greet():
...     return "Hello, World!"

>>> greet()
"Hello, World!"
```

### Explicit return

An explicit return statement is a when you use the [`return`][return] statement and give an optional return value.
Using an explicit return statement will terminate the function and return the value to the caller.

```python
>>> def greet():
...     print("Hello, World!")
...     return
...     print("This will never be printed")

>>> greet()
"Hello, World!"
```

You can use this behavior of `return` to be able to do early returns.

```python
>>> def greet(input = None):
...     if input == None:
...         return "Hello, World!"
...     return "Hello, " + input + "!"

>>> greet()
"Hello, World!"
>>> greet("Python")
"Hello, Python!"
```

You can also return a another function call.

```python
>>> def greet():
...     return len("Hello, World!")

>>> greet()
13
```

### Implicit return

An implicit return statement is a when you don't use the [`return`][return] statement.
In this case, the function will return `None`.

```python
>>> def greet():
...     equation = 1 + 1

>>> greet()
None
```
