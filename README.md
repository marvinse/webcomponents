# Webcomponents Intermediate
In this HTML file you will see
- How to style shadow dom

## How to style shadow dom
Styling shadow dom is a little different than styling light dom, we will se in this example the :host and the :host-context selectors:

```html
<body class="dark">
	<div id="host" class="error"><!--we can also put dark class here-->
		<p>Light DOM p</p>
	</div>
	<template>
		<style>
			p{
				color: blue;/*this rule won´t affect the p*/
			}
			:host{
				border: 1px solid black;
			}
			:host(.error){
				border: 1px solid red;
			}
			:host(.warning){
				border: 1px solid red;
			}
			:host(:hover){
				background: black;
			}
			:host-context(.dark){
				background-color: gray;
			}
			:host-context(.dark:hover){
				background-color: red;
			}
		</style>
		<content></content>
	</template>
</body>
```

```javascript
var host = document.querySelector("#host");
var root = host.createShadowRoot();
var template = document.querySelector("template");
root.appendChild(template.content);
```

The :host selector allow us to style the shadow host itself, and the :host-context is pretty similar, because allow us to style the shadow host, but we can put the host-context class in the host or in any host parent.

You can now go to [Webcomponents Intermediate 2] (https://github.com/marvinse/webcomponents/tree/webcomponentsintermediate2).
