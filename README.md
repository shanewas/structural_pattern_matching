# How to use structural pattern matching in Python

The pattern-matching syntax introduced in Python 3.10 allows for powerful new programming techniques for decision-making in apps.

## Introducing Python structural pattern matching

Structural pattern matching introduces the `match/case` statement and the pattern syntax to Python. The `match/case` statement follows the same basic outline as `switch/case`. It takes an object, tests the object against one or more match patterns, and takes an action if it finds a match.

```python
match command:
    case "quit":
        quit()
    case "reset":
        reset()
    case unknown_command:
        print (f"Unknown command '{unknown_command}')
```

## Matching against variables with Python structural pattern matching

If you want to match against the contents of a variable, that variable must be expressed as a dotted name, like an enum. Here’s an example:

```python
from enum import Enum
class Command(Enum):
    QUIT = 0
    RESET = 1

match command:
    case Command.QUIT:
        quit()
    case Command.RESET:
        reset()
```

One doesn’t have to use an enum; any dotted-property name will do. That said, enums tend to be the most familiar and idiomatic way to do this in Python.

## Matching against multiple elements with Python structural pattern matching

The key to working most effectively with pattern matching is not just to use it as a substitute for a dictionary lookup. It’s to describe the structure of what you want to match. This way, you can perform matches based on the number of elements you’re matching against, or their combination.

```python
command = input()
match command.split():
    case ["quit"]:
        quit()
    case ["load", filename]:
        load_from(filename)
    case ["save", filename]:
        save_to(filename)
    case _:
        print (f"Command '{command}' not understood")
```

## Matching against objects with Python structural pattern matching

The most advanced feature of Python’s structural pattern matching system is the ability to match against objects with specific properties. Consider an application where we’re working with an object named media_object, which we want to convert into a .jpg file and return from the function.

```python
match media_object:
    case Image(type="jpg"):
        # Return as-is
        return media_object
    case Image(type="png") | Image(type="gif"):
        return render_as(media_object, "jpg")
    case Video():
        raise ValueError("Can't extract frames from video yet")
    case other_type:
        raise Exception(f"Media type {media_object} can't be handled yet")
```

###### You can also perform captures with object matches:

```python
match media_object:
    case Image(type=media_type):
        print (f"Image of type {media_type}")
```

###### Using Python structural pattern matching effectively

The key with Python structural pattern matching is to write matches that cover the structural cases you’re trying to match against. Simple tests against constants are fine, but if that’s all you’re doing, then a simple dictionary lookup might be a better option. The real value of structural pattern matching is being able to make matches against a pattern of objects, not just one particular object or even a selection of them.
