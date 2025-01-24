

Jinja is a python template engine often used to create HTML, XML, and other markup formats that are returned to the users via a HTTP response. In our case we will be creating HTML files from the templates.

*Jinja templates are just .html files with the added jinja code. By convention they live in the /templates directory in a Flask project*




Jinja2 Syntax can contain variables as well as some programming logic, which when eval or rendered are replaced with actual values.

The variables and or logic are placed between tags or delimiters. Jinja uses {%.....%} syntax to interpolate values to a string. If you already have Flask in your envinorment Jinja2 should be installed.




So jinja can be used with html to put things like variable to be rendered inside a HTML element. Case and point. 

But jinja must be used alongside a HTTP server like flask. Flask handles all the requests, and jinja can handle dynamic portions of the response.

Remember to always set your flask app with
set FLASK_APP=app.py
set FLASK_ENV=development


then you can 
python -m flask run


app.py
```
from flask import *

from jinja2 import *

  

app = Flask(__name__) #Initalize Flask app

  
  

#Create app route to render jinja page.

@app.route("/jinja")

def jinja():

    return render_template('jinja.html', name='John', template_name="Jinja2")
```

notice how we pass through key values name and template_name
then 
jinja.html

```
<!DOCTYPE html>

<html lang="en">

<head>

    <meta charset="UTF-8">

    <meta name="viewport" content="width=device-width, initial-scale=1.0">

    <title>Document</title>

</head>

<body>

    <h1>Hi, {{ name }}!</h1>

    <p>This is your introduction to {{ template_name }} template!</p>

</body>

</html>
```


https://jinja.palletsprojects.com/en/2.11.x/

## What is an Expression?

A Python expression[[2]](https://python-web.teclado.com/section07/lectures/04_jinja2_expressions_and_data_structures/#fn2) is any piece of code—like a number, a string, or a class instance—that evaluates down to a single value.

> An expression is an instruction that combines values and operators and always evaluates down to a single value.

For example, `>>> foo = 2 + 2` is an expression because it evaluates to a single value `4`. In contrast, a Python instruction that doesn't evaluate down to a single value is generally known as a statement (i.e. an `if-else` statement).

## [#](https://python-web.teclado.com/section07/lectures/04_jinja2_expressions_and_data_structures/#expressions-in-jinja2)Expressions in Jinja2

This section explains how you can evaluate Python expressions in Jinja2 and render them via the `render_template` method.

Let's perform some basic operations like **addition**, **subtraction** and **string concatenation** via Jinja template. To follow along, create a new HTML template file named `expressions.html` in the `/templates` folder of your Flask project's directory. The content of the file should look like this:

Now we'll evaluate these expression operations and render the results using the `render_template` method. Let's create a new endpoint in our `app.py` file named `/expressions/` and perform rendering there.

```
# app.py

from flask import Flask
from flask import render_template

app = Flask(__name__)


@app.route("/expressions/")
def render_expressions():

    # interpolation
    color = "brown"
    animal_one = "fox"
    animal_two = "dog"

    # addition and subtraction
    orange_amount = 10
    apple_amount = 20
    donate_amount = 15

    # string concatenation
    first_name = "Captain"
    last_name = "Marvel"

    kwargs = {
        "color": color,
        "animal_one": animal_one,
        "animal_two": animal_two,
        "orange_amount": orange_amount,
        "apple_amount": apple_amount,
        "donate_amount": donate_amount,
        "first_name": first_name,
        "last_name": last_name,
    }

    return render_template("expressions.html", **kwargs)
```

In the above file, we just have to define the placeholder variables and the evaluation part will be taken care by the Jinja2 template engine.

In line **26**, we've taken advantage of Python dictionary to pass keyworded arguments to the `render_template` method. Instead of supplying all the arguments directly, you can use dictionary unpacking operator `**` (in line **37**) to pass the arguments implicitly while keeping the `render_template` method clean.



# Data Structures in Jinja2


You can also use list interations in Jinja

```
<!-- templates/data_structures.html -->

<h2>Data Structures in Jinja2</h2>

<h3>List Operations</h3>

<p>
    Jina said her top three favorite movies were {{ movies[0] }},
    {{ movies[1] }} and  {{ movies[2]}}.
</p>

<h3>Dictionary Operations</h3>

<p>
    This is a {{ car["brand"] }} {{ car["model"] }}, built
    in {{ car["year"] }}.
</p>

<h3>Custom Data Structure Operations</h3>

<p>
    The four Galilean moons of Jupiter are {{ moons.first }},
    {{ moons.second }}, {{ moons.third }} and {{ moons.fourth }}.
</p>
```


