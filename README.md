# Global V/S Nonlocal ![Python](https://img.shields.io/badge/python-3670A0?style=for-the-badge&logo=python&logoColor=ffdd54)
Today we'll deal with a topic that often causes headaches even for experienced developers - variable scopes and the keywords global and nonlocal.

## What's the point?
Imagine you're writing a function inside a function and you need to change a variable “outside”. Without special words, Python will say, “Nope, can't do that!”

## How does it work?
### Global:
```python
x = 5  # global variable

def change_x():
    global x 
    x = 10

change_x()
print(x)
```

### Nonlocal:
```python
def outer():
    counter = 0  # variable of the external function
    
    def inner():
        nonlocal counter  # want to change counter from outer
        counter += 1
    
    inner()
    print(counter) 

outer()
```

## Important points:

- Global can be used to create new variables
- Nonlocal only works with existing variables
- Python 3.13 fixed bugs with global in else and except blocks

## Typical bugs:
### Incorrect:
```python
def bad_function():
    print(x)    # error!
    global x    # global should be declared before using
    x = 10
```
### That's right
```python
def good_function():
    global x
    print(x)    # It's okay now.
    x = 10
```

## Useful tools:
### To check what variables you have:
```python
print(globals())  # all global variables
print(locals())   # all local variables
```
## Practical tips:

- Use global only when really necessary
- Nonlocal is great for counters and accumulators
- Always document the use of global and nonlocal in comments
- Try to minimize the use of global variables
