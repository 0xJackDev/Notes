

Now, if you're on **Windows** then export `FLASK_APP` and `FLASK_ENV` variables on _Command Prompt_ like this:

```
C:\path\to\app>set FLASK_APP=app.py
C:\path\to\app>set FLASK_ENV=development
```


then run

```
python -m flask run
```


```

from flask import Flask

app = Flask(__name__)


Then you can make app routes with functions under for example

@app.route("/")
def Hello_world():
	return "Hello World!"
```


to make an app route to serve html you can do this.

```
@app.route("/fancy")

def hello_world_fancy():

    greetings = """

    <html>

    <body>

  

    <h1> Greetings </h1>

    <p>Hello world</p>

    </body>

    </html

    """

    return greetings
```
no if you go to /fancy on the webserver it says Greetings, hello world.


## Render HTML Pages

### [#](https://python-web.teclado.com/section07/lectures/02_render_template_to_send_longer_strings/#create-the-static-files)Create the Static Files

Let's create a folder named `templates` inside your project folder. Create two empty HTML files called `first_page.html` and `second_page.html` in the `templates` folder. Your project folder should have the following structure:

```
.
├── app.py
└── templates
    ├── first_page.html
    └── second_page.html
```

Now, go ahead and add the following contents to your static files.

**First page:**

```
<!-- first_page.html -->

<!DOCTYPE html>
<html>

<body>

    <h1>First Page</h1>
    <p>This is the first page of your static content</p>

</body>

</html>
```

**Second Page:**

```
<!-- second_page.html -->

<!DOCTYPE html>
<html>

<body>

    <h1>Second Page</h1>
    <p>This is the second page of your static content</p>

</body>

</html>
```

The above static files are kept simple for demonstration purposes. In real life, you'll be dealing with much larger and more complex static files.

### [#](https://python-web.teclado.com/section07/lectures/02_render_template_to_send_longer_strings/#render-the-files-via-render-template)Render the Files via render_template

Now that you've created the necessary HTML static files, let's see how you can use `render_template` to send the files to the browser. Here, the following code snippet should be familiar to you. Here, we'll be exposing two API endpoints for accessing the static files from your browser:

```
# app.py

from flask import Flask
from flask import render_template

app = Flask(__name__)


@app.route("/first-page")
def render_first_page():
    return render_template("first_page.html")


@app.route("/second-page")
def render_second_page():
    return render_template("second_page.html")
```

In the above code snippet, we've imported the `render_template` method from Flask and used that to send the static contents to the browser. Using the route decorator we've created two different endpoints to send the pages. Notice we didn't mention the full path of the HTML files inside the `render_template()` method; Flask automatically looks for static files in the `templates` folder.

Now run the application (refer to the previous lesson[[2]](https://python-web.teclado.com/section07/lectures/02_render_template_to_send_longer_strings/#fn2) if you don't know how to run Flask applications) and go to following URL to view the `first_page.html`: