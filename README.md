# Webcomponents Foundations
In this HTML file you will see
- What is a custom element, and how to create one
- Extend HTML elements
- Working with templates
- How to create Shadow DOM and its advantages

## What is a custom element, and how to create one
First at all, what is a custom element? A custom element in other words is a custom tag, HTML has its tags, for example h1, p, and div.
We can also create our custom elements.
In order to create a custom element, we need to do 3 simple steps:
- Create a new HTML Element
- Create the callback, there are 4 callbacks (createdCallback, attachedCallback, detachedCallback and attributeChangeCallback)
- We must register the element

```javascript
var myComponent = Object.create(HTMLElement.prototype);
myComponent.createdCallback = function(){
  this.innerHTML = "<p>Example</p>"
}
document.registerElement("my-component",{
  prototype: myComponent
});
```

## Extend HTML elements
We can extend HTML elements using the attribute "is". Basically we need to follow the same steps than creating a custom element, with the difference that now we need to create the object with the element we will extend, for example if we´ll to extend a button we need to extend HTMLButtonElement, see the next example:

```javascript
var protoButton = Object.create(HTMLButtonElement.prototype);
protoButton.createdCallback = function (){
	this.innerHTML = "button";
	this.style.color = "blue"
}

var superButton = document.registerElement("super-button",{
	prototype: protoButton,
	extends: 'button'
});
```
```html
<button is="super-button"></button>
```

## Working with templates
A template is an HTML5 tag that allows us to create content that won´t render into the page until we call the respective javascript function. A nice feature with the templates is that we can add styles just to that template and it won´t affect other parts of the page, even if we have the same selector.
In order to create a template we need to follow 4 steps:
- Create the tag and put the content inside it
- Select the template using Javascript
- Import the node
- Append the content

```html
<template id="test">
	<div>
		<p>Hello <span class="person"></span></p>
	</div>
</template>
```

```javascript
var template = document.querySelector("#test");
var clone = document.importNode(template.content,true);
clone.querySelector(".person").innerHTML="Marvin Solano Eduarte";
document.body.appendChild(clone);
```

## How to create Shadow DOM and its advantages
Shadow DOM is DOM that we are not able to see, for example when we use the video tag it contains a lot of buttons, of course we did not create those buttons, the shadow dom did it.
We need to follow 3 steps to create a shadow dom:
- Create a host, this is where is going to live our shadow dom
- Create the shadow root by Javascript
- Create the content inside shadow root

```html
<div id="host"></div>
```

```javascript
var host = document.querySelector("#host");
var root = host.createShadowRoot();
root.innerHTML = "<h1>Hello world from Shadow DOM</h1>";
```

Of course we can insert templates inside a Shadow DOM, just like this
```html
<div id="host2">
		
</div>
<template id="shadow">
	<style>
		h1{
			color: blue;
		}
	</style>
	<h1>Hello world from Shadow DOM inside a template</h1>
</template>
```

```javascript
var host2 = document.querySelector("#host2");
var templateshadow = document.querySelector("#shadow");
var cloneshadow = document.importNode(templateshadow.content,true);
var root2 = host2.createShadowRoot();
root2.appendChild(cloneshadow);
```
You can now go to [Webcomponents Foundations 2](https://github.com/marvinse/webcomponents/tree/webcomponentsfoundations2).
