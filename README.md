# Webcomponents Training

This is a little training that show us how to use web components without any framework like Polymer.

Nowadays we have several problems with web development:

1. The markup is unclear, for example we have a div inside another div that at the same time has another div inside, etc
  ```html
  <div>
    <div>
      <div>
      </div>
    </div>
  </div>
  ```
2. We have conflict with styles, we are always afraid if someone adds some style and overwrites ours
  ```css
    h1{
      color:red;
    }
  ```
  ```css
    body h1{
      color:blue;  /* Uppps it overwrites the style above */
    }
  ```
3. We dont have any native template, for this reason exists a lot of templates libraries like handlebars
4. We are not able to bundle our code, I mean to package the CSS, the HTML and the JS in a single file

## Web components to the rescue

I created 4 branches, in each branch I teach some concepts about Web Components.

Before continue looking at this master branch I suggest you to follow this order:
- [Webcomponents Foundations](https://github.com/marvinse/webcomponents/tree/webcomponentsfoundations): In this branch I will show you the following concepts:
  - What is a custom element, and how to create one
  - Extend HTML elements
  - Working with templates
  - How to create Shadow DOM and its advantages
- [Webcomponents Foundations 2](https://github.com/marvinse/webcomponents/tree/webcomponentsfoundations2): Here I will explain:
  - What is an insertion point and its advantages
  - Creating multiples shadow dom
  - Working with events in Shadow DOM 
- [Webcomponents Intermediate](https://github.com/marvinse/webcomponents/tree/webcomponentsintermediate): This is one of the shorter classes, I will focus on showing you:
  - How to style shadow dom 
- [Webcomponents Intermediate 2](https://github.com/marvinse/webcomponents/tree/webcomponentsintermediate2): Finally in this branch I will be explaining:
  - How to style an insertion point
  - New CSS selector for shadow dom
