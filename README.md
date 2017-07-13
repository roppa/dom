The <abbr title="Document Object Model">DOM</abbr> is a convention used for interacting with HTML elements. The DOM is made up of a core set if interfaces ([APIs](https://developer.mozilla.org/en-US/docs/Web/API/Document_Object_Model)), also a combination of an API and a tree data structure. It's an independent model, meaning it is up to the vendor to implement it.

HTML nodes are in a tree format, so using the Javascript API implementation of the DOM it is possible to create, update, delete HTML elements, add or trigger events, change css styles et al - all using the DOM API provided by the browser.

Lets start with some HTML elements.

## Element

Element is the general base class from which objects in a Document inherit.

## Finding an element

```javascript
document.getElementById(idOfElement);
```

Single elements that are returned by the DOM implement the HTMLElement, Element, Node, EventTarget, ParentNode, ChildNode interfaces.

## Nodelists and Live nodelists

A Nodelist is just that, a list (an Array-like object, but not an Array) of DOM nodes.

The difference between "live" and "not live" is "live" is a reference to the node, so changes are reflected in the list - live updates of DOM elements.

These selectors produce live node lists:

```javascript
element.querySelector(cssElement);
element.getElementsByClassName(cssClassName);
element.getElementsByTagName(tagName);
document.getElementById('elementId').childNodes;
```

Static list:

```javascript
element.querySelectorAll(cssSelector);
```

## HTMLElement

Every html element has a LOT of properties including the following:

 - classList
 - className
 - dataset
 - id
 - innerHTML
 - innerText
 - tagName
 - textContent

They also have these methods:

 - setAttribute
 - getAttribute
 - hasAttribute
 - removeAttribute
 - addEventListener
 - removeEventListener

You'll be using these ones a lot.

### Traversal

As the DOM is a tree structure, to traverse the tree you can use methods on any element:

 - parentNode
 - children
 - childNodes
 - firstElementChild
 - lastElementChild
 - nextElementSibling
 - previousElementSibling

### CRUD methods

As well as traversing, we can create nodes. You have to have a starting point, so that will be a node that you have selected.

 - removeChild
 - appendChild
 - insertBefore
 - insertAdjacentHTML

## Events

Events are sent to objects to signal that something has happened. Things such as clicks, blurs, network activity in the case of Ajax, as well as many others. These all implement the ```EventTarget``` interface which has the method ```addEventListener```. Event listeners can be removed by calling ```removeEventListener```.

Things can get a bit tricky with events. Say you have a list of messages. If you click a message we want you to visit a the individual message on its own page. And we want a button  in the list to reply to a message. The button sits inside the message, so how do we know the exact target of the click? Events have a flow. So when a click happens, the dom needs to work from top to bottom to get the element click. This is the capturing phase. Each one of those ancestors is checked to see if there is an event attached to itself, but only if the event is for capturing mode will it execute. When the actual target is arrived at, the at target phase is entered. This is achieved by setting to true the third boolean useCapture parameter.

## Event phases

There are [4 phases](https://developer.mozilla.org/en-US/docs/Web/API/Event/eventPhase), ```NONE```, ```CAPTURING_PHASE```, ```AT_TARGET```, ```BUBBLING_PHASE```.

- ```CAPTURING_PHASE```: trickles down from window to target's parent, executing handlers added with useCapture = true
- ```AT_TARGET``` or 'Target phase': on the target itself, executes handlers with useCapture = false
- ```BUBBLING_PHASE``` or 'Bubbling phase': Bubbles up from the target's parent to window, executing handlers with useCapture = false

## Events and EventTarget

We can add interactivity using the DOM methods addEventListener, removeEventListener, dispatchEvent. The event object has a type, target, currentTarget. The callback takes an event object - which is the event on the DOM element, hence event.target is the element that had the event triggered.

There are also methods on this event object such as preventDefault, stopPropagating, stopImmediatePropagation.

## References

- [Mozilla event phase](https://developer.mozilla.org/en-US/docs/Web/API/Event/eventPhase)
- [Nodelist](https://developer.mozilla.org/en-US/docs/Web/API/NodeList)
