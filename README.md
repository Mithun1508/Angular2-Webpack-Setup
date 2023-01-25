# This code sets up an Angular 2 project with Webpack is a simple way while also providing the configuration for unit testing.

![Screenshot (67)](https://user-images.githubusercontent.com/93249038/214496097-aabe6083-df02-4bfc-b561-043c6156a1bc.png)

![Screenshot (66)](https://user-images.githubusercontent.com/93249038/214496155-317c110e-cf5b-4667-983a-5420c611378b.png)

# What is Angular 2?
Angular 2 is a modern framework for developing JavaScript applications. It is the second major version of the extremely popular Angular framework by Google. It was written from the ground up using TypeScript to provide a modern, robust development experience.

Note that, although TypeScript is the preferred language for developing with Angular 2, it is possible to develop through ES5 and regular ES2015

#  Prerequisites 

An intermediate understanding of JavaScript, including concepts of CommonJS modules,

At least a rough understanding of Angular 1,

An understanding of ES6/ES2015 concepts, such as arrow functions, modules, classes and block-scoped variables,

Comprehension of using command line or terminal, such as Git Bash, iTerm, or your operating system’s built-in terminal, and

You have Node >= v4 and NPM >= v2 installed.


Differences from Angular 1
Within the Angular community, there is a well-known video (slides here) where Angular team members Igor Minar and Tobias Bosch announced the death of many concepts Angular developers were familiar with. These concepts were:

Controllers,

Directive Definition Objects,

$scope,

angular.module(...), and

jqLite.

# Using TypeScript
As mentioned above, Angular 2 can be developed without TypeScript, but the extra features that it provides on top of ES2015 make the development process richer. In this section, we’ll run through a quick primer on TypeScript.

TypeScript is a superset of Javascript. What does that mean? In short, it means that the JavaScript you know today is understood by TypeScript. You can take any JavaScript file you have, change the extension to .ts, run it through the TypeScript parser, and it will all be understood. What the compiler outputs is JavaScript code, which, many times, is as good or even better written than the original code.

One of the most prominent TypeScript features is its optional typing system. Note that this is optional. Utilizing types, however, makes it easier to reason about code. Many editors have support for TypeScript, which allows for features such as code completion to be utilized.

Another feature is the ability to define interfaces, which can then be used as types throughout your code. This helps when you need to ensure that a data structure is consistent throughout your code.

// note this code is available in the repo		
// at ./examples/introduction/types-and-interfaces.ts

// MyType is a custom interface
interface MyType {
    id: number;
    
   name: string;
   
   active?: boolean;       // the "?" makes this an optional field
}

// someFunction takes three parameters, the third of which is an
// optional callback
function someFunction(id: string, value: MyType, callback?: Function) {
    // ...
    
} 
Now, if you were to code and call someFunction, your editor (with TypeScript support) would give you a detailed definition of the parameters. Similarly, if you had a variable defined as MyType, code completion would show you the attributes available on MyType and the types of those attributes.

TypeScript does require a build process of some sort to run code through its compiler. In later sections we’ll set up the configuration for the TypeScript compiler.


# What is Webpack?
From the Webpack website, “webpack is a module loader” that “takes modules with dependencies and generates static assets”. Additionally, it provides a plugin system and methods for processing files.

# Module Loading
So, what does module loading mean? Let’s look at a very simple example. We have a project with 4 files: app.js, child1.js, child2.js, and grandchild.js.

app.js is dependent on child1.js and child2.js
child2.js depends on grandchild.js
We can then tell Webpack to run just on app.js, and it will compile a file that contains all files. It does this by finding all statements in app.js that indicate a dependency, such as an import or a require. In app.js, we have:

const child1 = require('./child1.js');

const child2 = require('./child2.js');          

Webpack knows it needs to find those files, read them, find any of their dependencies, and repeat until it hits a file with no dependencies. The file child1.js is such a file. In child2.js, though, we have:

const grandchild = require('./grandchild.js');

So, Webpack finds grandchild.js, reads it, sees no dependencies, and stops its processing. What we end up with is all 4 files, compiled together and usable in the browser. In a nutshell, this is what module loading does.

# File Processing
In addition to just loading modules based on dependencies, Webpack also provides a processing mechanism called loaders.

To see what loaders do, let’s use another example. Say we have a TypeScript file. As mentioned above, to compile a TypeScript file to JavaScript, it needs to be run through the TypeScript compiler.There are Webpack loaders that will do just that. We can tell Webpack that, as it encounters .ts files, it should run those files through the TypeScript compiler.

The same can be done for virtually any file type — SASS, LESS, HTML, Jade, not just JavaScript-like files. This concept is beneficial because it allows us to use Webpack as a sort of build system to do all the heavy lifting we need to get Angular 2 into the browser, or in our testing environment.

# Why Should We Unit Test?
When we develop applications the most important thing we can do is to ship code as fast and bug-free as possible. Testing helps us achieve those goals. The number one concern for developers who do not unit test is that it takes too long. When you’re first getting into utilizing unit testing in development, it may take longer than you’re used to. However, the long-term benefits far outweigh that initial investment, especially if we test before we write our application code. This is known as Test-driven Development (TDD).

# Test-driven Development
We need to write a JavaScript function called isPrimary. This function’s main purpose is to return true if a number is a primary number and false if it’s not.

In the past, we would just dive in head-first, probably hit Google to remember what a primary number is, or find a solid algorithm for it and code away, but let’s use TDD. We know our ultimate goal, i.e. to output a boolean of whether a number is a primary number or not, but there are a few other concerns we need to address to try to achieve a bug-free function:

What parameters does the function take? What happens if they’re not provided?
What happens if a user passes in a non-number value?
How do we handle non-integers?
When we approach a problem from a TDD perspective, our first step is to ask ourselves what could go wrong and figure out how to address it. Without this perspective, we may not think about these cases, and we might miss them. When these cases do arise, we may have to completely refactor our code to address them, potentially introducing new bugs.

One of the core tenets of TDD is writing just enough code to make a test pass. We use a process known as the red-green-refactor cycle to achieve this goal. The steps are:

Think about the test you need to move towards completion, 

Write a test, execute it, watch it fail (red),  

Write just enough code to watch it pass (green),   

Take a moment to look at the code for any smells.  If you find any, refactor the code. Run the tests with each change to the code to ensure you haven’t broken anything, and
Repeat.
Step number one is probably the hardest step for developers new to TDD and unit testing in general. Over time you’ll become more and more comfortable and recognize patterns of how to test.

Advantages of Unit Testing and TDD
We’ve seen a couple of the advantages of unit testing already, but there are more. Here are a few examples:

Reduces the level of bugs in code,  

Less application code because we write just enough code to achieve our goals,  

Makes it easier to refactor code, 

Provides sample code of how to use your functions, 


You get a low-level regression test suite, and
Speeds up code-writing.
Disadvantages of Unit Testing and TDD
Unit testing isn’t a silver bullet to writing perfect code. There are drawbacks to doing so. Here are a few of those drawbacks:

Could give a false sense of quality,  

Can be time consuming,

Adds complexity to codebase, 

Necessity to have mock objects and stubbed-out code, especially for things outside your control, i.e. third-party code, and     
 
For a large codebase, tweaking one part of your application, such as a data structure, could result in large changes to tests. 

While these disadvantages exist, if we are diligent and thoughtful in our testing approach, the benefits unit of testing and TDD outweigh these risks.

# Using NPM as a Task Runner
In a prior section, we saw that we could use Webpack to perform many of our build process functions, but not how to invoke them. You may be familiar with the plethora of task runners out there today, e.g. Grunt, Gulp, Broccoli, so why not use one of them? In short, NPM, which we already use to install our project dependencies, provides a simple system for running tasks.

As you may know, each project that uses NPM needs a package.json file. One of the sections package.json offers is a scripts section. This section is just a JSON object where the keys are the name of our task, and the values are the script that will run once the task is approved.

So, if we have the following in our package.json:

...
  "scripts": {
      "foo": "node ./scripts/foo.js",
      "bar": "node node_modules/bar",
      "baz": "baz some/config.file"
  }
...
# To run these tasks, 
all we need to do is say npm run [task name]. To run foo, we’d just do:

npm run foo
and the command node ./scripts/foo.js would be run. If we ran npm run baz it would look for the baz node module through node_modules/.bin, and then use some/config.file.

Because we already have this task-runner capability, it will be used to perform tasks such as running unit tests. To read more about using the scripts section, take a look at the official NPM documentation.

# Installing Dependencies
Now, we’ll move on to actually setting up the project. The first step is to get all the dependencies we need. We’ll be pulling in Angular, TypeScript, Webpack, and unit testing.

Creating the NPM Project
The first thing we need to do is create an NPM project. We’ll take the following steps:

Create a directory. The name doesn’t matter, but it’s useful to make it descriptive, e.g. ng2-webpack-test,
Change into that directory by doing cd ng2-webpack-test, or whatever you named your directory, and
Run npm init -f. This will generate a package.json file for your project.
The following commands should all be run from the directory you created in step 1 above.

# Angular Dependencies
Angular 2 is broken into a lot of packages under the @angular organization in NPM. We’ll need to install them and pull in RxJS, Zone.js, and some shims.

This can be accomplished through a single install operation:

npm i -S @angular/common @angular/compiler @angular/core @angular/platform-browser @angular/platform-browser-dynamic es6-shim reflect-metadata rxjs@5.0.0-beta.6 zone.js
i is an alias for install, -S is an alias for --save.

To see what each of these projects is for, take a look at the Angular 2 documentation.

Although some of these packages are not immediately necessary for performing unit testing, they will allow us to run our application in the browser when the time comes.

Note that this is for Angular 2 RC5.

TypeScript Dependencies
Since TypeScript is going to be used in this project, we’ll also need to pull it in as a dependency. To help our code have fewer mistakes and maintain a coding standard, we’ll be using code linting through the TypeScript linter, tslint.

npm i -D typescript tslint typings
-D is an alias for --save-dev.

The dependency typings is a way to pull in TypeScript definition files so that TypeScript can understand third-party libraries and provide code completion suggestions for those libraries. We’ll see how to use this later.

# Webpack Dependencies
We’ll also need to pull in all of the dependencies for using Webpack, too. This involves Webpack itself, as well as a list of loaders and plugins we’ll need for Angular, TypeScript, and unit testing.

Here’s the command we need to run:

npm i -D webpack webpack-dev-server html-webpack-plugin raw-loader ts-loader tslint-loader
The html-webpack-plugin and webpack-dev-server will benefit us when we run our application in a web browser. We’ll see what the raw-loader does as we develop our application.

# Unit Testing Dependencies
For unit testing, we’ll be using Karma as our test runner with Jasmine as the testing framework. There are a multitude of testing libraries out there that could be used, like Mocha and Chai, but by default Angular 2 uses Jasmine, and Karma works well with Webpack.

npm i -D karma karma-jasmine jasmine-core karma-chrome-launcher karma-phantomjs-launcher phantomjs-prebuilt karma-sourcemap-loader karma-webpack
The Chrome and Phantom launchers provide an environment for Karma to run the tests. Phantom is a “headless” browser, which basically means it doesn’t have a GUI. There are also launchers for Firefox, Internet Explorer, Safari, and others.

The karma-sourcemap-loader will take the sourcemaps that we produce in other steps and load them for use during testing. This will be useful when running tests in Chrome, so we can place breakpoints in the debugger to see where our code may have problems.

# Configurations
The following sections will show how set up our project to run tests and how to run our application in a browser. We’ll need to configure setups for:

TypeScript,
Unit Testing,
Webpack, and
NPM Scripts.
This may seem like a lot to undertake, but we’ll see that the developers of these libraries have established configurations that are easy to understand.

You can follow along with the example files located in examples/introduction/ng2-webpack-test. You will need to run npm i if you have cloned this repository to get all the Node modules installed.

# TypeScript Configuration
The pieces needed for utilizing TypeScript are type definitions, linting, and the actual configuration for the TypeScript compiler. Let’s look at the type definitions first.

Type Definitions
First, we’ll need to create the typings.json file by running the following command from the root of our project:

./node_modules/.bin/typings init
This will run Typings out of its node_modules directory and use its init command.

The typings.json file will be placed in the root of the project. It will contain the name of the project and an empty dependencies object. We’ll use the install command to fill that object.

There are three files to install, but we need two commands:

./node_modules/.bin/typings install dt~jasmine env~node --save --global
Again, we are using Typings to install type definitions for jasmine and node.

The second flag, --global, tells Typings that the definitions being installed are for libraries placed in the global scope, i.e. window.<var>. You’ll notice that each of the libraries is preceded by a ~ with some letters before it. Those letters correspond to different repositories to look for the type definition files. For information on those repositories, look at the “Sources” section of the Typings Github page.

We’ll run a second install command for the es6-promise shim, as it is not a window.<var> library. Notice that there is no prefix required.

./node_modules/.bin/typings install es6-promise --save
Your type definitions are now installed.

# Linting
We’ll also be instituting code linting for our project. This will help our code stay as error-free as possible, but be aware that it won’t completely prevent errors from happening.

As mentioned above, we’ll use the tslint library to achieve this goal. It uses the file tslint.json to describe the rules for how code linting should behave. Let’s take it one section at a time:

 timeout is used when we test asynchronous processes. If we don’t set this properly, some of our tests could hang forever.

With these two files, we’ve configured Karma to run. There’s a good chance we’ll never need to touch these files again.

# Configuring Webpack
Now, we’ll set up Webpack to perform its role. If we have a webpack.test.js, a webpack.dev.js, and a webpack.prod.js there is bound to be an overlap in functionality. Some projects will use the webpack-merge from SurviveJS which keeps us from duplicating parts of our configurations.

We won’t be using this approach in order to have a complete understanding of what the configuration files are providing us. For our purposes, we will have just a webpack.dev.js and a webpack.test.js. The .dev configuration will be used when spinning up the Webpack development server so that we can see our application in the browser.

In your project directory, create a sub-directory named webpack, which will house both of these files.

Setting up webpack.test.js
This file has been mentioned a couple of times. Now, we’ll finally see what it’s all about.

'use strict';


We’ve discussed loaders before, and here can we see them in action. We can also specify preLoaders which run before our regular loaders. We could put this loader with the other “regular” loaders, but as our application grows, having this separation of concerns will help prevent compilation from getting sluggish.

Our first “real” loader will take .css and .html files and pull them in raw, whithout doing any processing, but will pull them in as JavaScript modules. We’ll then load all .ts files with the ts-loader we installed before, which is going to run each file through the TypeScript compiler. The exclude attribute allows us to avoid compiling any third-party TypeScript files. In this case, it will avoid pulling in any TypeScript files from the node_modules directory.


# Setting Up webpack.dev.js
Note: if you are not interested in using the webpack-dev-server as you follow these tutorials, you can skip this section. Also, any portion of the configuration which is discussed in the webpack.test.js section will not be rehashed below.

'use strict';

const HtmlWebpack = require('html-webpack-plugin');
const path = require('path');
const webpack = require('webpack');
const ChunkWebpack = webpack.optimize.CommonsChunkPlugin;

const rootDir = path.resolve(__dirname, '..');
The two new Webpack dependencies here are the HtmlWebpack and ChunkWebpack plugins.

The last line of this snippet utilizes that path library so we can be sure that we’ll always be referencing files using our project directory as the starting point.

module.exports = {
    debug: true,
    devServer: {
        contentBase: path.resolve(rootDir, 'dist'),
        port: 9000
    },
    devtool: 'source-map',
The first attribute is debug which, when set to true, lets Webpack know it can switch all of our loaders into debug mode, which gives more information when things go wrong.

The devServer attribute describes how we want webpack-dev-server to be set up. This says that the location from which files are served will be the dist directory of our project and that we’ll be using port 9000.

Don’t worry about creating a dist directory, as the dev server is going to serve all of our files from memory. You will actually never see a physical dist directory be created, since it is served from memory. However, doing this tells the browser that the files are coming from another location.

    entry: { 
    
        app: [ path.resolve(rootDir, 'src', 'bootstrap') ], 
         
        vendor: [ path.resolve(rootDir, 'src', 'vendor') ]
        
    },
Here, we’re telling Webpack that there are two entry points for our code. One is going to be src/bootstrap.ts, and the other will be src/vendor.ts. The file vendor.ts will be our entry to load the third-party code, such as Angular, while bootstrap.ts is where our application code will begin.

You’ll notice that we don’t need to provide the .ts to the files. We’ll explain this in a moment. Also, we didn’t need this in webpack.test.js because the file karma.entry.js acted as a sort of faux entrypoint for that process.

    module: { 
    
        loaders: [ 
         
   
   { loader: 'raw', test: /\.(css|html)$/ },
             
             { exclude: /node_modules/, loader: 'ts', test: /\.ts$/ }
        ]
    },
    output: {  
          filename: '[name].bundle.js', 
        path: path.resolve(rootDir, 'dist')
    },
If you don’t remember how we used our loaders, you can take a look at the webpack.test.js section for more information.



# Manual linting,
Running the dev server,
In-browser (Chrome) testing, and
Headless browser (PhantomJS) testing.
Doing this is very simple — we’ll utilize our installed Node modules to perform any of the above actions. You can add the following to your scripts section of your package.json:

"lint": "tslint ./src/**/*.ts",
"start": "webpack-dev-server --config ./webpack/webpack.dev.js",
"test": "karma start ./karma/karma.conf.js",
"test:headless": "karma start ./karma/karma.conf.js --browsers PhantomJS"
Instead of saying node ./node_modules/tslint/bin/tslint.js, we can just use the name of a package, e.g. karma or tslint. This is because there is a symlink in ./node_modules/.bin to this file which NPM can utilize to run the package. The test task will run the unit tests in both Chrome and PhantomJS, while the test:headless task will run them just in PhantomJS, as specified by the browsers flag.

# How to Run and Test


To install all the dependencies run:

npm i
For single, headless tests use:

npm run test:headless
To run code in a browser user:

npm start
Setup for Angular 2 with Webpack
This is the code setup for the article Setting Up Angular 2 with Webpack

This code sets up an Angular 2 project with Webpack is a simple way while also providing the configuration for unit testing.

To install all the dependencies run:

npm i
For single, headless tests use:

npm run test:headless
To run code in a browser user:

npm start
