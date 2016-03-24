# Webcomponents Foundations
In this HTML file you will see
- What is an insertion point and its advantages
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

