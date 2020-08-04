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