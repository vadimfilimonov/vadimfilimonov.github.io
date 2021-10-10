---
layout: post
title:  "Setting Aspect Ratio / HTML&CSS"
date:   2021-10-10 12:22:39 +0300
categories: frontend
---
## I. The way of the background image

- Create a div;
- Set it to zero height;
- Set the background image;
- Set the size of the background image to zero;
- Create a pseudo-element before;
- Inherit the background from the parent;
- Divide the height by the width and multiply the result by a hundred to get the value for padding-top;
- The result is the following styles:

{% highlight css %}
.image {
  background-size: 0 0;
}

.image:before {
  content: '';
  display: block;
  padding-top: 56.25%;
  background-image: inherit;
  background-repeat: no-repeat;
  background-size: cover;
}
{% endhighlight %}

Example on [codepen](https://codepen.io/vadimfilimonov/pen/KKKKrdB).

## II. The way of the object-fit's property.

If you are satisfied with the [browser support](https://caniuse.com/#feat=object-fit) and know the size of one of the sides of the images, then you can use the property:

{% highlight css %}
object-fit: cover;
{% endhighlight %}

If the width of the picture is 500px and the aspect ratio has to be 4:3, then all you have to do is this:

```
(3 / 4) * 500 = 375
```

In the end, the styles will look something like this:

{% highlight css %}
img {
  width: 500px;
  height: 375px;
  object-fit: cover;
}
{% endhighlight %}

## Additional materials

- [This article is in Russian](https://vk.com/@filimonovvadim-aspect-ratio-images)
