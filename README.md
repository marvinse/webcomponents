# Webcomponents Intermediate 2
In this HTML file you will see
- How to style an insertion point
- New CSS selector for shadow dom

## How to style an insertion point
We can style an insertion point using the :content pseudo-selector
```html
<div id="host">
	<button>My button</button>
</div>
<template id="content">
	<style>
		::content button{
			color: red;
		}
	</style>
	<content></content>
</template>
```
```javascript
var hostcontent = document.querySelector("#host");
var rootcontent = hostcontent.createShadowRoot();
var templatecontent = document.querySelector("#content");
rootcontent.appendChild(templatecontent.content);
```

## New CSS selector for shadow dom

### The :shadow pseudo-selector
It allows us to style the shadow dom itself, it will style just the first shadow dom, so if we want to give styles to shadow dom inside another shadow dom we will need to use another pseudo-selector


```html
<style>
li::shadow{ /*it won´t work because we need to define the custom element*/
	color: green;
}
developers-list::shadow li{
	color: red;
}
</style>
<template id="developers">
		<ul>
			<li>Developer 1</li>
			<li>Developer 2</li>
			<li>Developer 3</li>
			<li>Developer 4</li>
			<li>Developer 5</li>
		</ul>
</template>
<developers-list></developers-list>
```

```javascript
var developersList = Object.create(HTMLElement.prototype);
developersList.createdCallback = function(){
	var template = document.querySelector("#developers");
	var templateClone = document.importNode(template.content,true);
	this.createShadowRoot().appendChild(templateClone);
}

document.registerElement("developers-list",{
	prototype: developersList
});
```

### The /deep/ selector
This selector allow us to style the shadow dom, and the shadow dom inside a shadow dom

```html
<style>
developers-list /deep/ li{
	color: blue;
}
</style>
<template id="developers">
	<ul>
		<li>Developer 1</li>
		<li>Developer 2</li>
		<li>Developer 3</li>
		<li>Developer 4</li>
		<li>Developer 5</li>
	</ul>
	<shadow></shadow><!--we need to put this tag if not boss-list will not work-->
</template>
<template id="boss">
	<ul>
		<li>Boss 1</li>
		<li>Boss 2</li>
	</ul>
</template>
<developers-list>
	<boss-list></boss-list>
</developers-list>
```
```javascript
var bossList = Object.create(HTMLElement.prototype);
bossList.createdCallback = function(){
	var templateBoss = document.querySelector("#boss");
	var templateCloneBoss = document.importNode(templateBoss.content,true);
	this.createShadowRoot().appendChild(templateCloneBoss);
}

document.registerElement("boss-list",{
	prototype: bossList
});
```

### The :unresolved pseudo-selector
It allows ud to style the tags that are not properly resolved. A tag properly resolved must be register using `document.registerElement`

```html
<style>
custom-reallyunresolved:unresolved{
	color: red;
}
</style>
<custom-reallyunresolved>Im unresolved</custom-reallyunresolved>
```
