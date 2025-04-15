---
layout: post
title: "Evaluating React.js and Flask"
date: 2015-08-05 10:39
comments: true
published: true
categories: Software Javascript React Python Flask
---

> Update: Udemy has generously granted a free coupon for the readers of this blog for their [React JS and Flux](https://www.udemy.com/learn-and-understand-reactjs/learn/) course. Use the code `avidasreactjs` and the first 50 readers will get free access to the course!

As a connoisseur of the web, front-end frameworks have been been a fertile area of late. React.js from Facebook has taken much fanfare, and this post evaluates key ideas on react, and digs into why you could be interested in React. Staying true to single responsibility principle, React is a highly useful tool if you are doing web programming.

In this post, we will dive into building a Frontend using React.js and Backend built using the Python framework Flask. Flask is a minimalistic framework, and excellent when your backend becomes more and more of an API. Moreover, this facilitates the microservices architecture, where the decoupling of your your app into small unit of services can make it more maintainable and scalable.

We will cover some of the key ideas of React and Flask here, but it would be worth referring to the official documentation for [React](https://facebook.github.io/react/) and [Flask](http://flask.pocoo.org/) for getting started and understanding the philosophies of each framework.

###Key Ideas of React
The core idea of React is the developers are better of leaving manipulating the DOM to battle tested framework code. Since the DOM has a tree structure, finding elements and manipulating them would need many traversals of a potentially very large tree.  Instead, what you modify is a virtual DOM, and React runs its intelligent diffing algorithm to directly update the DOM. 

#####React 
React itself is the UI library that will manage all the DOM updates as data changes. It's takes the V of MVC frameworks, hence it can be used with other MVC frameworks such as Angular, Backbone or Meteor. It is quite easy to use React to manage specific areas of your application's UI, rather than the entire app.

#####Virtual Dom
The virtual Dom is an abstraction layer between nodes in the real DOM and the view of the code you are modifying. When React selectively renders subtrees of the nodes in DOM based upon state changes, it achieves the following

     1. Ensures that your DOM is always up to date with current state
     2. Reduces the need to re-render the DOM every time there is change in state
     3. Updating only the individual components on state change ensures high performance

#####JSX
JSX is a JavaScript syntax extension and it brings in a HTML/XML like familiar syntax for defining a tree structure with attributes. This is the syntax you can use to declare the changes in layout code and React will update the UI. It's a bold approach, since developers are conditioned to keep layout code separate from Javascript. We will explain more React terminology later as we dive into some code.

###Key Ideas of Flask
Flask is a microframework, which means that it trades a short learning curve for fewer out of the box functionalities, compared to heavier frameworks such as Django or Rails. It gives developers more freedom to use their preferable tools and libraries. However, it does have a list of officially supported [extensions](http://flask.pocoo.org/extensions/) which when plugged in provide a wide breath of functionalities for a standard web app. Extensions behave as if they are native flask code.

We strongly recommend that you set up a [virtualenv](http://www.virtualenv.org/) for this project, and you may also want to check out [virtualenvwrapper](http://virtualenvwrapper.readthedocs.org/) for convenience. This is to provide your app with a sandboxed environment.

#####Getting up and running with Flask

Lets first install Flask

```bash
pip install Flask

# For viewing and reusing app dependencies
pip freeze > requirements.txt
```
Set up the following directory structure in your app. 

```bash

├── README.md
├── app.py
├── requirements.txt
└── templates
    └── index.html
```

Modify your app.py code to include the following

```python
from flask import Flask, render_template

app = Flask(__name__)

@app.route("/")

def index():
    return render_template('index.html')

if __name__ == "__main__":
    app.run()
```

We start by importing Flask and creating a new instance of a flask application. In flask, app.route is used to describe the behavior when users hit particular endpoints in the application. Here when user hits the index route, we render a template called hello world. By default Flask uses the Jinja2 templating language, but you can use any other templating language. In fact, we will not be covering Jinja2 in this blog post. Finally we tell python to call the run method of the app when invoked as a main function.

Let's populate index.html with the following basic HTML boilerplate

```html

<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Flask React Tutorial</title>
</head>
<body>
     <div id="mount-point">
         <p1>Hello world.</p1>
     </div>
</body>
</html>
```

Now run the app with

```bash
python app.py
// * Running on http://127.0.0.0:5000/
// * Restarting with reloader
```
By default it runs on port 5000. Navigate to the endpoint and you should see the html page you just created. You are now up and running with Flask!

#####Integrate React
Easiest way to include React would be to just include them from a cdn. Let's update the index.html to include React and and port our existing html to React. index.html will now look like

```html

<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Flask React Tutorial</title>
    <script src="https://cdnjs.cloudflare.com/ajax/libs/react/0.13.2/react.min.js"></script>
    <script src="https://cdnjs.cloudflare.com/ajax/libs/react/0.13.2/JSXTransformer.js">
</head>
<body>
     <div id="mount-point"></div>
</body>

  <script type="text/jsx">
     /*** @jsx React.DOM */
    var FirstComponent = React.createClass({
        render: function() {
            return (<p1>Hello world.</p1>);
        }
    });
    React.render(<FirstComponent />, document.getElementById('mount-point') );
     </script>

</html>
```

<!-- more -->

Let's go over the code. We first include the react and jsx libraries via the script tags and remove the earlier p tags. We set up a jsx script by specifying type="text/jsx". Then we call createClass method of React which creates a React component. React components are reusable units that you can use to compose your UI. The component must have at least the render method, which returns the virtual representation of a native DOM element or another component.
Next we call React.render with the first element and pass it the id of the div element on which we want the result of the render function to be. Run the app again to navigate to the same path to see the app again.

#####Data binding with React
For a more practical example, as well to demonstrate multiple components, let's produce a type along data binding example. You can replace your script tag with the following

```html
<script type="text/jsx">
    /** @jsx React.DOM */
    var Input = React.createClass({
        updateLabel: function(event){
            this.setState({value: event.target.value});
        },
        getInitialState: function(){
            return {
                value: ''
            }
        },
        componentWillMount: function(){
            this.setState({value: this.state.value})
        },
        render: function(){
            return (
                <div className="update-label">
                      <input type="text" placeholder="Enter text" onChange={this.updateLabel}/>
                    <Label value={this.state.value}/>
                </div>
        )
    }
});

var Label = React.createClass({
    render: function(){
        return (
        <div class="my-label">
        <h2>{this.props.value}</h2>
        </div>
        )
    }
});

React.render(<Input/>, document.getElementById('mount-point'));
</script>
```

As before, React.render is called at the very end on a component called Input and it is bound to the element with id mount-point. Inside the Input component a few other lifecycle functions are introduced. 

The method getInitialState is called once before the component mounts and  responsible for setting for the initial state of a component. 
componentWillMount is called directly before a react component is initially rendered. Inside componentWillMount, we invoke setState.

setState can trigger UI updates from event handlers and server request callbacks. It will always cause a re-render to happen. Once render is called, it returns a div with a input box and a React component called label. We attach the method updateLabel which gets invoked when the text inside the input box changes. It updates this.state.value. 

State attributes are mutable within a component and are used to represent the interaction changes changes within a component. On the other hand, props are immutable and used to pass data from a parent component to a child. In this case Label is a child component of Input, and this.state.value for Input is passed to Label, which can access it by this.props.value. Thus Input passes the data entered into the input box to Label and causes it to re-render and display the text.

Fire up the server again and type something into the input box and the content gets updated in the h2 element underneath.

#####Why React
As it turns out, the selling points of React are not super hard to get and clear use cases became obvious.

1. React is very efficient in the way it handles DOM updates. It is important however, to isolate that heavy rendering or interactions are the bottlenecks so that you are not optimizing prematurely and likely already have optimized database interactions and network calls.

2. SEO management overhead can be less with React compared to Angular/Ember since it can be rendered server side. The benefit comes from not having the overhead of rendering your page server side with something like PhantomJS and serving the HTML.

3. Reusable components make the code more reusable and testable, and the short terminology keeps the learning curve managable.

4. Since React can be rendered Server Side, you might completely get rid of your server side templating, further reducing the number of tools necessary to run your app.


#####React and Flask
With their focus on SRP, React and Flask could be dependable and efficient parts of your stack. This is specially handy if you want to leverage the Numpy/Scipy stack for doing data analysis in near realtime and serve up a frontend with heavy user interaction. In a later post, we will look at exploring interactive applications and introduce Socket.io.