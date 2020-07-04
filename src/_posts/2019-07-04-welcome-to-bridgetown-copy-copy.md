---
layout: post
title:  "Another blog post"
date:   2019-12-23 00:44:39 -0400
categories:
  - Ruby
---

If you’re new to React, and [just installed React through Webpacker in your Ruby on Rails application](https://jasoncharnes.com/installing-react-in-ruby-on-rails), you might have some questions.

Let’s answer those questions by walking through the React component Rails and Webpacker auto-generated for us.

# Hello React

Rails auto generates a React component in `app/javascript/packs` named `hello_react.jsx`. Cute name, right?

The file looks like this:

```javascript
import React from "react";
import ReactDOM from "react-dom";
import PropTypes from "prop-types";

const Hello = props => <div>Hello {props.name}!</div>;

Hello.defaultProps = {
  name: "David"
};

Hello.propTypes = {
  name: PropTypes.string
};

document.addEventListener("DOMContentLoaded", () => {
  ReactDOM.render(
    <Hello name="React" />,
    document.body.appendChild(document.createElement("div"))
  );
});
```

Let’s break down the different pieces of this file.

# The file type

If you haven’t worked with React, JSX may be an unknown file type to you. Don’t worry; we’re going to start there.

JSX is a ["syntax extension to JavaScript"](https://reactjs.org/docs/introducing-jsx.html). Essentially, this means JSX is a regular JavaScript file with the ability to do some templating. The React team recommends the JSX file type, and it’s the one I use when I write React code, even in Ruby on Rails.

All you need to know, at this point, is that JSX files render React components. We’ll create these React components out of JavaScript and HTML.

There’s an example further down, so let’s move on for now.

# Imports

The top of the file starts with "import" statements. What are these imports?

ES6 brought the ability to import functionality from JavaScript modules easily. Using modules allows us to wrap JavaScript functionality inside a module and use it elsewhere throughout our application.

In this file, we’re importing three libraries from our "node_modules" directory. These libraries are brought in by Yarn as declared in package.json

```javascript
import React from "react";
import ReactDOM from "react-dom";
import PropTypes from "prop-types";
```

1. __React__ is used for, well, React.
2. __ReactDOM__ is used to render our React component(s) onto the DOM.
3. __PropTypes__ is used to declare "props" in our components. We’ll talk more about this below.

If you’d like to know more, I go further in-depth on ES6 modules in my free course on [ES6 Essentials](https://jasoncharnes.podia.com/es6-essentials-for-react).

# Constants and arrow functions oh my!

If you’ve not worked with ES6 or JSX, this line of JavaScript is going to look funny.

```jsx
const Hello = props => <div>Hello {props.name}!</div>;
```

This small line of code is a potent line of JavaScript. Let’s break it down by keyword.

### Constants

`const` is a keyword short for constant. Once’s a constant is declared, it cannot be re-declared or re-assigned- it becomes a read-only property.

### Hello

It should come as no shock that `Hello` is the constant’s name. However, it might be odd to you that it’s capitalized. React components are camel-cased and start with capital letters. And that’s what we’re declaring, a React component.

### Arrow functions

Okay, so let’s dissect `props => ...`

We’re assigning an arrow function to the `Hello` constant. The first keyword, `props`, is the argument to the arrow function.

The code after the arrow is the code we want to execute when we invoke this constant (or render this component).

__But, this code has no brackets or return keyword!__ Because this is a single expression, we can inline the code and get an implicit return.

__But, this code is just HTML!__ Aha, welcome to JSX, which I said we talk about more. This line begins the power of JSX. We’ve defined our component to render an HTML div. JSX knows how to convert that to a div for the DOM.

__But, there are curly brackets inside the div!__ How about that? So this further shows the power of JSX. If we want to execute a JavaScript expression in HTML, we can wrap it in curly brackets. In this case, props.name is a value, so the value name is rendered inside this HTML. Neat, huh?

So, let’s recap what we learned about this line of code.

```jsx
const
// 👆A constant

Hello =
// 👆The constant's name

props =>
// 👆The function's argument and declaration

<div>Hello {props.name}!</div>;
// 👆The HTML implicitly returned by the function, with evaluated (and rendered) JavaScript
```

I swear this article isn’t a promotion for my mini-course, but it is relevant again. (And at least it’s free!) If you’d like to know more about constants and arrow functions, I cover those in my free course on [ES6 Essentials](https://jasoncharnes.podia.com/es6-essentials-for-react).

# Props

Now is an appropriate time to talk about "props." Props are simple to understand, very powerful, and require more explanation than this article can provide. We’ll cover at a high-level what props are and how they fit into this component.

Props are arguments to React components. Skipping ahead (just a little bit) to the bottom of the file, you’ll find the following line of code:

```jsx
<Hello name="React" />
```

This line is rendering our React component. There is an argument awkwardly named name. The argument, here, is taking the value "React". This prop is then available in the component.

Remember The line of code returned by our Component `<div>Hello {props.name}!</div>`? This snippet is how we access props passed into our component. props is an argument into our function (given to us by React), and then the name is accessed via props.name.

See, that’s not so bad?

One significant caveat also outside the scope of this article: Props are read-only. You can’t mutate props. For simplicity’s sake, think of props as constants.

# Prop types

With your abounding knowledge of props, we can continue down the file.

```javascript
Hello.defaultProps = {
  name: "David"
};

Hello.propTypes = {
  name: PropTypes.string
};
```

Our component can have two properties assigned to it:

1. Default props
2. Prop types

These are just as they sound.

### Default props

Default props are default arguments. If someone renders the component without passing the prop, it falls back to the default value.

### Prop types

You can set the expected type of the prop using the PropTypes library we imported earlier. If I give this component an integer for the name prop instead of a string, the application won’t blow up. (Unless you try to do some string-specific logic to the integer.) It will, though, log an error in the console telling you it expected a string, and you gave it an integer.

This functionality is handy as your components grow in size and complexity. However, both of these prop properties are _optional_.

# The grand finale

It’s time to get our React component onto the DOM.

```javascript
document.addEventListener("DOMContentLoaded", () => {
  ReactDOM.render(
    <Hello name="React" />,
    document.body.appendChild(document.createElement("div"))
  );
});
```

We start by adding an everyday event listener to the DOM. Once the content is loaded, the anonymous arrow function is invoked.

ReactDom (the library we imported earlier) has a render method we call with two arguments:

The rendered React component (with our props)
The DOM element the component is rendered inside

### Rendered React components

To render a React component, we wrap it in self-closing brackets, just as we would any other HTML element.

### The DOM element

In this example, we’re creating a div and appending it to the body. The React component is rendered inside the div and displayed in the DOM.

The second argument (the DOM element) can be any DOM node JavaScript knows about. For example, we could re-write the code to use an existing DOM node:

```javascript
document.addEventListener("DOMContentLoaded", () => {
  ReactDOM.render(
    <Hello name="React" />,
    document.getElementById("#fancy-react-element")
  );
});
```

# Look at you, React expert

We covered much ground, but I hope this helps you understand the random React component that Webpacker generated for you in your Ruby on Rails application.

So, what did we learn today?

- ES6 imports
- Constants
- Arrow functions
- Basic React components
- Props
- PropTypes
- ReactDOM rendering

I hope this piques your interest just enough to keep learning React. I think it makes a great addition to Ruby on Rails applications, and I’m excited to see what you build with it.
