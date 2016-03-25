# Webcomponents Foundations 2
In this HTML file you will see
- What is an insertion point and its advantages
- Creating multiples shadow dom
- Working with events in Shadow DOM

## What is an insertion point and its advantages
Combining templates with custom element we can control where to put the content, even it will allow us to hide the content that doesn´t match with our insertion points.
In order to create an insertion point, we need to follow 3 simple steps:
- Create a template
- Use the content tag with the corresponding select attribute
- Create the custom element

```html
<template>
	<fieldset>
		<legend>
			<content select="h1"></content><!--the h1 will be here, in this insertion point -->
		</legend>
		<content select="p.instructions"></content>
		<textarea cols="30" rows="10"></textarea>
		<input type="submit" value="Submit">
		<content select=".footer"></content>
		<content></content><!--any content that doesn´t match with content selectors above-->
	</fieldset>
</template>
```

```javascript
var proto = Object.create(HTMLElement.prototype);
proto.createdCallback = function(){
	var template = document.querySelector("template");
	var shadow = this.createShadowRoot();
	shadow.appendChild(document.importNode(template.content,true));
}

document.registerElement("comment-form",{
	prototype: proto
})
```

Now we are able to use the new tag with insertion points, so note that even if we put the h1 tag down, at the time it renders, it will be at the top, as we defined in our insertion point
```html
<comment-form>
	<p class="instructions">Please fill this form</p>
	<h3>It is a pleasure to serve you</h3>
	<p class="footer">Suscribe now</p>
	<h1>Form</h1>
</comment-form/>
```

## Creating multiples shadow dom
We can create shadow dom inside other shadow dom. We need to take into consideration that just the last shadow dom will be rendered on the page, so we need to use the shadow tag to make an insertion point of the before shadow dom, look at the example:

```html
<div id="shadowhost">
	<h1>shadow inside shadow</h1>
</div>
```

```javascript
var host = document.querySelector("#shadowhost");
var root1 = host.createShadowRoot();
var root2 = host.createShadowRoot();//just the last shadow root is rendered
root1.innerHTML = "<p>Root1</p>";
root2.innerHTML = "<p>Root2</p><shadow></shadow>";//to render the previous shadow dom we need to use the shadow tag, content tag can be used if it´s needed
```

## Working with events in Shadow DOM
The difference between events in light dom and shadow dom is that in Shadow Dom who receives the event is the host, not the element itself, like normally happens on Light Dom

```html
<button id="light-dom-btn">Light Dom Btn</button>
<div id="event-host">
	
</div>

<template id="event-template">
	<button id="shadow-dom-btn">Shadow Dom Btn</button>
	<select name="" id="shadowselect">
		<option value="option">Option</option>
		<option value="option">Option</option>
		<option value="option">Option</option>
	</select>
</template>
```

```javascript
var hostevent = document.querySelector("#event-host");
var rootevent = hostevent.createShadowRoot();
var templateevent = document.querySelector("#event-template");
rootevent.appendChild(document.importNode(templateevent.content,true));

document.addEventListener("click",function(e){
	console.log(e.target.id);//On Shadow Dom who receives the event is the container, not the element
});

document.addEventListener("change",function(e){
	console.log(e.target.id);
});
```

Note that change event is treated like a click on shadow dom.

You can now go to [Webcomponents Intermediate] (https://github.com/marvinse/webcomponents/tree/webcomponentsintermediate).
