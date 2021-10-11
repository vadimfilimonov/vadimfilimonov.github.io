---
layout: post
title:  "Block rendering with JavaScript"
date:   2021-10-11 18:00:00 +0300
categories: frontend
---

## Task

There is an [API](https://private-531a0-vadimfilimonovblog.apiary-mock.com/frameworks), which in response to the request returns a json with a list of frameworks and their descriptions. We need to render cards based on it.

![Cards](https://sun9-86.userapi.com/impg/Gikuh5C_7CJjQWW6LXDVFu6GDzPGSP_eF-Go9w/GHtQ_aZJ5os.jpg?size=674x462&quality=96&sign=0e72025efff28459e34e6a4b8b1f7faf&type=album)

## Algorithm

1. Get list;
2. Process the list;
3. Render it into HTML.

### 1. Get list

I have prepared test data for this article, which can be obtained at:

```
https://private-531a0-vadimfilimonovblog.apiary-mock.com/frameworks
```

To make an HTTP request - use the method [fetch](https://developer.mozilla.org/en-US/docs/Web/API/Fetch_API/Using_Fetch):

{% highlight css %}
fetch("https://private-531a0-vadimfilimonovblog.apiary-mock.com/frameworks")
{% endhighlight %}

### 2. Process the list

This is what the json we get looks like:

{% highlight json %}
{
  "success": true,
  "list": [
    {
      "title": "React",
      "text": "React is an open-source...
{% endhighlight %}

Let's write a function `buildHTML` that will take JSON as input and output a string that we will use as HTML in the future:

{% highlight javascript %}
// HTTP request
fetch("https://private-531a0-vadimfilimonovblog.apiary-mock.com/frameworks")
  // convert the response to json
  .then(response => response.json())
  // convert to html
  .then(buildHTML)
{% endhighlight %}

Definition of function:

{% highlight javascript %}
const buildHTML = ({ list }) =>
  list.map(({ title, text }) => (`
    <div>
      <h2>${title}</h2>
      <p>${text}</p>
    </div>
  `)).join("");
{% endhighlight %}

### 3. Render it into HTML

{% highlight javascript %}
fetch("https://private-531a0-vadimfilimonovblog.apiary-mock.com/frameworks")
  .then(response => response.json())
  .then(buildHTML)
  // The result is sent to the render function
  .then(render);
{% endhighlight %}

In the HTML file create an empty container, where we will insert the cards:

{% highlight html %}
<div class="container"></div>
{% endhighlight %}

The work of the render function comes down to just using the property [innerHTML](https://developer.mozilla.org/en-US/docs/Web/API/Element/innerHTML):

{% highlight javascript %}
const render = (html) => {
  const container = document.querySelector('.container');
  container.innerHTML = html;
};
{% endhighlight %}

![Result](https://sun9-8.userapi.com/impg/YNDIxW64gsC2v3l2HzRqr9U8RgB82Os4vdYI3g/akmlzM5vrHA.jpg?size=693x531&quality=96&sign=a83c8b268137c0d35e4db9789fbf0446&type=album)

See the full version of the code at [codepen](https://codepen.io/vadimfilimonov/pen/QWEzLow).

## Additional materials

- [This article is in Russian](https://vk.com/@filimonovvadim-render-page-via-js)
