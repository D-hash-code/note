## Packages

Packages are just a special kind of module. Specifically, any module that contains a __path__ attribute is considered a package.

If you want to import/use code from a different directory in python there is a simple rule. The rule is that you don't include execute statements in the place you want to extract code from unless its nested in one of these

```python
if __name__ == "__main__.py":
    run_a_function()
```
If you want to mess around with this stuff a bit try run a file with this

```python
print(repr(__name__))
```

Going farther, if you have a file structure like this

```python
|--src    
    |--directoryone
        |--files.py
    |--directorytwo
        |--util.py
```

then as an experiment to understand the name main thing better, in utils place this code
```python
def does_nothing():
    return "insert unpopular opinion"

print(repr(__name__))
```
and in files place the following code

```python
from src.directorytwo.util import does_nothing
print(does_nothing)

```
and run files.py!

