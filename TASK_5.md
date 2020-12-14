## Task 5 <small>[[Try Now]](http://pentesteracademylab.appspot.com/lab/webapp/jfp/5)</small>

Objectives:

1. Remove the Form and add a notification "Website is Down! Please visit SecurityTube.net"

Ah, this is pretty easy. If you would see we have to overwrite the exisiting form and add the text.

This can be achieved by setting [HTMLElement.innerText](https://developer.mozilla.org/en-US/docs/Web/API/HTMLElement/innerText) of form element.

```js
document.forms[0].innerText = "Website is Down! Please visit SecurityTube.net";
```

The naive approach would be delete the form using [Node.removeChild](https://developer.mozilla.org/en-US/docs/Web/API/Node/removeChild), creating an element and appending the chiild

Just in case you want to add HTML instead of text, see [Element.innerHTML](https://developer.mozilla.org/en-US/docs/Web/API/Element/innerHTML)

For POC, [Click Here](http://pentesteracademylab.appspot.com/lab/webapp/jfp/5?url=%3Cscript%3Edocument.forms%5B0%5D.innerText%20%3D%20%27Website%20is%20Down%21%20Please%20visit%20SecurityTube.net%27%3C%2Fscript%3E)
