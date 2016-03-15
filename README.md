# Webcomponents Foundations
In this HTML file you will see
- What is a custom element, and how to create one
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
## Working with templates
