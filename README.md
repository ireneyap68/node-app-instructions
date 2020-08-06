# node-app-instructions

### Setting up a Node Project
1. Create a new folder for your first node project.
```js
    mkdir my-first-node-proj
```
Open the folder in your favorite text editor.
2. Initialize Node inside the project folder.
```js   
    npm init
```
To skip this step in the future (and accept all default values at once), type 
```js
    npm init -y.
```
Take a look at the package.json file that was just created. This is where the values we just set up via npm init are stored. This is like your settings file. You can edit these values by changing them in this file (make sure to save).
3. Make your entry point.
 Create this file now.
```js
touch index.js
```
4. Run your program!
To run a file in node via the command line, type node [file name here].
```js
node index.js
```
# Node Module - Creating, Exporting, and Importing Modules
Node's module system allows code written in one file to be exported, and then imported into other files. By importing a module (i.e. a specified section of code), we can then use that code as if it actually were written in the file we imported it to.

1. Create your module.
In Node, module.exports is an object that will hold the code to be exported. We can use dot-notation to add the code we want to export to this object. Add the following code to your myModule.js file:
```js
    module.exports.beBasic = () => "That's so fetch!"
```

2. Import your module in index.js.
This is where the require function, specific to Node, comes into play. This function takes one argument: the path to the file that contains the module you are exporting.In the index.js file, write the following code:
```js
    const myModule = require('./myModule.js');

    console.log(myModule.beBasic());
```
Run index.js via the command line:
```js
    node index.js
```
Let's add some more code to our module. In myModule.js, add the following code:
```js
    module.exports.beBasic = () => "That's so fetch!"

    const count = () => {
        for (var i = 0; i <= 10; i++) {
            console.log(i);
        }
    }
```
Try running this code in the command line: node index.js

# Using Built-In Modules - Example: fs module
We will use the fs core module (it stands for "file system") to read a text file.
Create a story.txt text file inside your project directory and write a short story inside it.Core modules just need to be imported using the require function. Write the following code to your entry point file:
```js
    var fs = require('fs');

    fs.readFile('story.txt', 'utf8', function(err, data){
        if(err) {
            console.log("There was a problem reading the file.");
        } else {
            console.log(data);
        }
    });
```

# Git Ignore File 
Take a look at the node_modules folder that got generated when you used the npm install command. How big is this folder? How many files are in it? What's going on?
In general, we keep track of the version of the module that we are using in a file called package.json. This means we can just redownload the modules based on the version number on any new computer we want to put our code on - be that a fellow developer's computer or a production server. So, because we can just re-install the appropriate packages, we actually don't need to have the node_modules folder to be tracked by git at all! In fact, the node_modules folder can get so huge and unweildy that it's greatly preferred that you DO NOT push them up to github nor track them with version control! In fact, this can also cause serious errors during deployment!

How can we avoid this?!
We can specify directions to git about which files it should ignore by creating a file called .gitignore. Yes, the . at the front is necessary!
A .gitignore file will contain a list of files and folders that git should NOT be tracking. Go ahead and make a .gitignore file now and put node_modules into it as the first line. {.gitignore}
```js
    node_modules
```

# Intro to Express
Express is a light-weight, web application framework for writing RESTful APIs in Node.js.

## My first Express App
1. Create a new directory for your project.
```js
    mkdir hello-express
```
2. Initialize Node
```js
    cd hello-express
    npm init
```
3. Install Express
```js
    npm i express
```
4. Create your entry point file.
```js
    touch index.js
```
5. Import the Express module
```js
index.js
    const express = require('express');
```
6. Create an instance of an express app
```js
    index.js
    const express = require('express');
    const app = express();
```
7. Create a Home Route
```js
    index.js
    const express = require('express');
    const app = express();

    app.get('/', function(req, res) {
        res.send('Hello, World!');
    });

    app.listen(8000);
```
8. Run nodemon
```js
    nodemon
```
Now visit localhost:8000 in browser. This is my first express app.

# Routes
A route is a combination of a URL pattern and HTTP Verb.

### URL Pattern
The URL Patterns refer to everything that comes after the base URL (the slash and anything that follows). For example, let's look at a simple website - go to http://www.lemon-fol.io . You're looking at the home route. Now click on "projects" in the nav bar, or add /projects to the end of the URL in the URL bar. In this scenario, everything before /projects is the base URL. The base URL alone took you to the home route ("/") which served the home page. The URL pattern "/projects" served different files.

### HTTP Verb
There are 4 main HTTP verbs:
HTTP Verb | CRUD  | Example
GET       | READ  | Look at someone's profile on LinkedIn
POST      | CREATE | Post on LinkedIn
PUT       | UPDATE | Change your bio on LinkedIn
DELETE    | DELETE | Delete a photo from LinkedIn

### Backtrack: hello-express
The combination of the URL Pattern '/' and the HTTP verb 'get' ensures that this route will be reached when a GET request made by the client from the base URL.

### The Request and Response Objects
Our callback functions for our routes (which are sometimes referred to as Controllers) receive two very special objects from Express. They are provided to our function very much like the e object holding all the event data is passed into our event listeners, or like each item in an array is passed into our forEach() callback.

* request
The Request object, frequently abbreviated to req, contains all the data we would ever need about the actual request that came in. What are they requesting? What browser are they using? Bunches of other stuff. But mostly we will using three keys inside of it:
1. req.body - this is where any submitted form data will be stored for us.
2. req.params - this is where special route variables are stored for us.
3. req.query - this is where the query string data is stored.
As you can see, most of the time, if we are accessing the req object, its because we need to get at some data being sent to us from the user.

* response
The Response object, or res for short, is what we use to send something back to the user's browser, or more formally, send a response to the request. There are a number of functions we can use:
1. res.send() - sends back a simple string. Not really used in production. This is kind of like the console.log() for network requests. Good for testing if the route is working.
2. res.sendFile() - more sophisticated in that it can send an entire file back but file is static.
3. res.render() - used to render data into templates with the selected template engine. More on this later.
4. res.json() - used to send object data back as JSON. Very common when writing a backend API. Much more on this later.

## My 2nd Express App: Fun With Routes
Set up the project
1. Create a new directory called route-fun
```js
    mkdir route-fun
```
2. Initialize Node
```js
    cd route-fun
    npm init
```
3. Install Express
```js
    npm i express
```
4. Create entry point
```js
    touch index.js
```
5. Create an instance of express
```js 
    index.js
    const express = require('express');
    const app = express();
```
6. Establish the base URL
```js
    index.js
    const express = require('express');
    const app = express();

    app.listen(8000);
```
7. Write a home route
```js
    const express = require('express');
    const app = express();

    app.get('/', (req, res) => {
    res.send("You've reached the home route!");
    });

    app.listen(8000);
```
Run nodemon and visit localhost:8000 to make sure everything is working.

# Views
We're going to create a personal website with the following pages:
* Home
* About
* Blog

Objectives:
* Practice stubbing out routes
* Learn how to set up views
Prerequisites:
* Know how to write a GET route in Node/Express

## Part 1: Routes
We're going to stub out the routes for the home, about, and blog pages!
1. Set up your app Create a new Node/Express project.
2. Create the following routes:
* Home | GET | / | "This is the Home Page!"
* About | GET | /about | "Some stuff about me will go here."
* Blog | GET | /blog | "A directory of all my blog posts will go here."

## Part 2: Views
Writing text to a web page using res.send() gives us something to look at, but isn't very pretty. Instead of sending plain text, let's start serving HTML files. Since each page will display different HTML, we'll have several HTML files, or views.

1. Create a views folder inside your project directory. Inside this folder, create three HTML files:
* index.html (this is the standard filename for the view associated with the base URL)
* about.html
* blog-directory.html

2. Put some basic HTML in these files so you can test them.

3. In your routes, replace the res.send(<message>) with res.sendFile(<absolute file path>) (docs)

res.sendFile() takes an absolute path, so we can't just give it ./views/index.html. How do you get the absolute file path for each of these files? Don't know/don't care? You're in luck! __dirname is a Node keyword that gives us the absolute path of the current directory (docs), so we can just tack that on in front of the relative path
```js
    app.get('/', function(req, res) {
    res.sendFile(__dirname+'/views/index.html');
    });
```

# Templates
## Template Engines
Template engines allow us to inject values into the HTML, and even script logic into the HTML. This will be extremely useful for building in CRUD functionality and full stack apps in general. docs

## EJS: Embedded Javascript
There are several javascript template engines for express, one of the most popular of which, is EJS, available via npm. Let's update our express personal website views with EJS.

### Install EJS
Add EJS to your personal website project using npm:
```js
    npm install ejs
```
Set the view engine to EJS
Above your routes, add an app.set(name, value) statement docs where the name is the view engine property and the value is ejs.
```js
    app.set('view engine', 'ejs');
```
### Adapt your routes to ejs
1. Rename the .html files to .ejs files.
2. Replace your res.sendFile(<absolute path>) statements with res.render(<file name>) statements.
3. Ejs assumes a lot about the path to the template files, so as long as they are nested in a views folder and have .ejs extensions, you can simply pass the filename (no extension, though it wont break it if you include it) into res.render()
```js
    app.get('/', function(req, res) {
        res.render('index.ejs');
    });
```

## Templating with Variables
Templating with variables means we can pass in an object to res.render() and access the values stored in it as variables inside the ejs template.

We now have access to a name variable inside our index.ejs file! We can access this variable by embedding it into the html using this notation: <%= embedded js goes here %>.

index.js
```js
    app.get('/', function(req, res) {
    res.render('index', {name: "Sterling Archer", age: 35});
    });
```
For example: index.ejs
```html
    <!DOCTYPE html>
    <html>
    <head>
        <title>Home Page</title>
    </head>
    <body>
        <h1>Hello, <%= name %>!</h1>
    </body>
    </html>
```

## Partials
Partials can be used to modularize views and reduce repetition. A common pattern is to move the header and footer of a page into separate views, or partials, then render them on each page.

Create the partials
In the main directory of your project, create a partials folder that includes a header.ejs file.
partials/header.ejs
  <header>
    <img src="http://placekitten.com/500/500">
  </header>

Include my partial
index.ejs
<!DOCTYPE html>
<html>
  <head>
    <title>Home Page</title>
  </head>
  <body>

    <%- include('../partials/header.ejs') %>

    <h1>Hello, <%= name %>!</h1>

# Layouts and Controllers
## EJS Layouts
Adding partials can dry up the code a bit, but EJS Layouts can take this modularity even farther and make a big diffence with large applications.
EJS layouts is a node package that allows us to create a boilerplate (aka a layout) that we can inject content into based on which route is reached. Layouts normally include header and footer content that you want to display on every page (navbar, sitemap, logo, etc.).

nstall EJS Layouts
Step 1: Install EJS layouts
Install express-ejs-layouts via npm
```js 
    npm install express-ejs-layouts
```

Step 2: Set up EJS layouts
Require the module and add it to the app.
index.js
```js
    var express = require('express');
    var app = express();
    var ejsLayouts = require('express-ejs-layouts');

    app.set('view engine', 'ejs');
    app.use(ejsLayouts);

    app.listen(3000)
```

Step 3: Create a Layout
In the root of the views folder, add a layout called layout.ejs. It must be called layout.ejs, as mandated by express-ejs-layouts.
layout.ejs
```html
    <!DOCTYPE html>
    <html>
    <head>
    <title>Faves&Hates</title>
    </head>
    <body>
    <%- body %>
    </body>
    </html>
```
This layout will be used by all pages, and the content will be filled in where the <%- body %> tag is placed. <%- body %> is a special tag used by express-ejs-layouts that cannot be renamed.


Step 4: Use the Layout
In the views folder, create a home.ejs file:
home.ejs
```html
<h1>This is the home page!</h1>
```
Now create a home route in index.js below the middleware:
```js
    app.get('/', function(req, res) {
        res.render('home');
    });
```

Step 5: Set up a few more views/routes
index.js
```js
    app.get('/animals', function(req, res) {
        res.render('animals', {title: 'Favorite Animals', animals: ['sand crab', 'corny joke dog']})
    });
```
animals.ejs
```html
    <h1><%= title %></h1>
    <ul>
    <% animals.forEach(function(animal) { %>
        <li><%= animal %></li>
    <% }) %>
    </ul>
```

## Controllers & Express Router
Controllers become important organizational tools when you start making apps with several views, so let's create a few more views.
1. Inside the views folder, create a faves folder and move your foods.ejs and animals.ejs files into it.
2. Inside the views folder, create a hates folder that also contains a foods.ejs file and an animals.ejs file, but design these views to display your least favorite foods and animals.
We have been placing all routes into index.js when creating a Node/Express app, but this can get cumbersome when dealing with many routes. The solution is to group related routes and separate these groups into separate files. These files will go into a controllers folder.
3. Create a controllers folder inside the root directory that will contain all routes except for the home route.
4. Inside the controllers folder, create a file called faves.js with the following routes:
```js
    app.get('/foods', function(req, res) {
        res.render('faves/foods', {title: 'Favorite Foods', foods: ['coconut', 'avocado']});
    });

    app.get('/animals', function(req, res) {
        res.render('faves/animals', {title: 'Favorite Animals', animals: ['sand crab', 'corny joke dog']})
    });
```
5. Add these wrapper lines of code to faves.js, and replace app with router.
```js
    var express = require('express');
    var router = express.Router();

    router.get('/foods', function(req, res) {
        res.render('faves/foods', {title: 'Favorite Foods', foods: ['coconut', 'avocado']});
    });

    router.get('/animals', function(req, res) {
        res.render('faves/animals', {title: 'Favorite Animals', animals: ['sand crab', 'corny joke dog']})
    });

    module.exports = router;
```
6. Now back in index.js, we just need to add some middleware to get these routes working again!
index.js
```js
    app.use('/faves', require('./controllers/faves'));
```
Note that we defined the routes relative to the definition in app.use. In other words, take note that our URL patterns in faves.js don't inclued '/faves', because that is taken care of by the middleware.
Check that these routes are working by visiting http://localhost/faves/foods and http://localhost/faves/animals.

7. 'Hates page' set as 'Fave page'. Only change 'faves' to 'hates' in:
* index.js
* hates.js
* hates.ejs