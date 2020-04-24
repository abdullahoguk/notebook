# Python

## Basics

```python
print("Hello, world!")
name = "abdullah"

# formatted sting (~backticks in js)
print(f"Hello, {name}!")
```

- Indentation is important (loops, conditionals, functions), put `:` at the and of the line before indented line.

### Conditionals

```python
if x > 0:
	print("x is positive")
elif x < 0:
	print("x is negative")
else:
	print("x is zero")
```


### Data Types

- `int` : integer value
- `float` : floating point value
- `str` : text string
- `bool` : boolean value (`True` or `False`)
- `None` : empty value

### Sequences (String, Tuple, List, Set, Dict)

* **Strings**: Sequence of characters, and can be indexed as such.

	```python
  name = "Alice"
  print(name[0])
	```

- **Tuples**:  immutable collections of values under a single name, which can be indexed positionally.

	```python
  coordinates = (10.0, 20.0)
  print(coordinates[1])
	```

- **Lists**: mutable collections of values under a single name, which can be indexed positionally. It can contain any number of data types. Indexing out of range raises a Python ‘exception’. In this case, an `IndexError`, because there is no fourth value in `names` for Python to return.

	```python
  names = ["Alice", "Bob", "Charlie"]
  print(names[2])
	```

- **Sets**: Unordered collection of unique items. Because they are unordered, they cannot be indexed.

	```python
  s = set()
  s.add(1)
  s.add(3)
  s.add(5)
	```

- **Dictionaries**: Dictionaries (or dicts) are like lists, except that they are unordered and their `value`s are indexed by `keys`.	

	```python
  ages = {"Alice": 22, "Bob": 27}
  print(ages["Alice"])
  ages["Alice"] += 1
	```

### Loops

```python
for i in range(5):
    print(i)
```

- For-loops iterate over their bodies a limited number of times. In this case, the number of iterations is set by `range(5)`.

- `range(5)` returns the sequence of numbers starting at 0 through 4. Each value is passed to `i` once, resulting in the loop running a total of 5 times. `i` is normally referred to as an iterator variable.

- Lists can be iterable with for loop.

	```python
  for listItem in listName:
      print(listItem)
	```

### Functions 

```python
def square(x):
	return x * x
      
for i in range(10):
# old method to format strings
	print("{} squared is {}".format(i, square(i)))
```
- Python has built-in functions, such as `print()` and `input()`, but Python also allows for the creation of user-defined functions
- Trying to call a function that hasn’t been defined will raise a `NameError` exception.

### Modules

- Modules are separate `.py` files of code, often written by others, used in a new file without rewriting all the old code again. Using modules allows, for example, the use of functions across a program larger than a single file.

- Assuming the `square` function was saved in `functions.py`, adding this line atop a new module will allow for the use of `square` there as well.

  ```python
  # otherfile.py
  from functions import square
  square(4)
  ```

- When importing something, normal sequence of source file also be executed. To prevent that, add main sequence of source file to a function like main and add 

  ```python
  # functions.py
  if __name__ == "__main__":
        mainThingsToDo()
  ```

  - If you are running your module (the source file) as the main program like `python functions.py` , python sets `__name__` to `__main__`

### Classes 

- A Python `class` can be thought of as a way to define a new, custom Python data type, somewhat analagous to defining a custom function. 

- This creates a new `class` called `Point`:

  ```python
  class Point:
  	def __init__(self, x, y):
      	self.x = x
          self.y = y
          
  p = Point(3, 5)
  print(p.x)
  
  ```

- **`__init__`** (~constructor)function is a special function that defines the information needed when a new `Point` is created.

-  `**self**`(~this) is always required, which refers to the `Point` being created.

- By convention, `class` names tend to start with a capital letter.

- We can access the attributes with dot notation

## Flask

Flask a microframework written in Python that makes it easy to get a simple web application up and running with some features that can be useful in the development process.

- Flask code is generally stored inside `application.py` 
- set env var to application.py with `export FLASK_APP=application.py` , then run `flask run` on that directory



```python
from flask import Flask # Import the class `Flask` from the `flask` module
app = Flask(__name__) # Instantiate a new web application called `app`, with `__name__` representing the current file

@app.route("/") # A decorator; when the user goes to the route `/`, exceute the function immediately below
def index():
    return "Hello, world!"
    
@app.route("/<string:name>")
def hello(name):
    name = name.capitalize()
    return f"<h1>Hello, {name}!</h1>"
```

### **Using Html Template files** Jinja2

- `index.html` and any other template files should be stored in a directory named `templates`
- Variables can be defined as Python variables in `application.py` and used in HTML templates by passing them in as arguments to `render_template`. These templates are rendered using a separate templating language called Jinja2:

```python
#appication.py
from flask import Flask, render_template
app = Flask(__name__)

@app.route("/")
def index():
	headline = "Hello, world!"
    #send data to template
	return render_template("index.html", headline=headline) #render_template("index.html")

@app.route("/full")
def more():
	headline = "Hello, world!"
    #send data to template
	return render_template("more.html", headline=headline)
```

```html
#index.html
<h1>{{ headline }}</h1>

{% if new_year %}
    <h1>Yes! Happy New Year!</h1>
{% else %}
    <h1>No.</h1>
{% endif %}

{% for name in names %}
    <li>{{ name }}</li>
{% endfor %}

#go to route that more function associated ("full" in this case)
<a href="{{ url_for('more') }}">See more...</a>
```
- Template Inheritance

```html
#layout.html
<!DOCTYPE html>
<html>
    <head>
        <title>Flask PG</title>
    </head>
    <body>
        <h1>{% block heading %}This text is like default value to be placed if you dont use "heading" block in child. Using a block in child is overriding that block content. You can use "{{super()}}" in child templates if you also want to use original value{% endblock %}</h1>
        {% block body %} 
            {% for name in names %}<li>{{ name }}</li>{% endfor %}
        {% endblock %}    
    </body>
</html>

#more.html (super() to render content written inside block definiton in layout > for loop in names list in this case)
{% extends "layout.html" %}   

{% block heading %} All Content {% endblock %} 
{% block body %} 
    {{super()}}
    <a href="{{ url_for('index') }}">Ana Sayfa</a>
{% endblock %}    
```

### Forms

```python
# application.py
from flask import Flask, render_template, request, redirect, url_for
app = Flask(__name__)

@app.route("/new", methods=["GET", "POST"])
def newPerson():
    if request.method == "GET":
    	return "Please fill the form"
    else:
    	name = request.form.get("name") # on submit, access the form, and store `name` field in a python variable name
    	names.append(name)
    	return redirect(url_for('more')) #redirect to route that "more" function associated.
```

```html
# more.html
<form action="{{ url_for('newPerson') }}" method="post">
	<input type="text" name="name" placeholder="Enter Person Name">
    <button>Submit</button>
<form>
```

### Sessions

