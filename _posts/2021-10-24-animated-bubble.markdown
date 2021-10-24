---
layout: post
title:  "Animated Bubble / SVG"
date:   2021-10-24 18:00:00 +0300
categories: frontend
---

Today we're going to learn how to create things like this without javascript or canvas:

![Animated Bubble](https://img-host.ru/8UKPW.gif "Animated Bubble")

**Drawing the bubble**.

- Go to [figma.com](figma.com) and create a new file;
- Select Pen or press P.

![pen](https://img-host.ru/dSxyy.jpg "pen")

Draw a rectangle - press Done.

![Close first and last line](https://img-host.ru/e0rM8.jpg "Close first and last line")

Let's remove the stroke and fill the rectangle with a fun color.

![Click on minus to remove stroke, add color to fill](https://img-host.ru/pBu2r.jpg "Click on minus to remove stroke, add color to fill")

Let's finally make what we want out of the square.

Let's press the Edit Object button.

![rectangle](https://img-host.ru/l5220.jpg "rectangle")

Next, click on Bend Tool

![Bend Tool](https://img-host.ru/W9Eso.jpg "Bend Tool")

Click on the side of the square. You should see points like this:

![start transform](https://img-host.ru/1n5i6.jpg "start transform")

Pull one of them up:

![pull](https://img-host.ru/czn85.jpg "pull")

As you can see, the shape curves. This is where my deep knowledge of figma and vector graphics comes to an end. So we just do the same trick for all four points.

![This is what I got](https://miro.medium.com/max/700/0*PqeA-pIzxB8pMKFO.jpg "This is what I got")

Great, the bubble is ready. It will be our "starting" position.
Let's copy it and put it next to it.

![I also recommend renaming them for convenience](https://img-host.ru/2mJmD.jpg "I also recommend renaming them for convenience")

Again press Edit Object - Bend Tool and change the bubble on the right side a bit.

![almost done](https://img-host.ru/XjE2u.jpg "almost done")

> What you get is the state of the shape that the original one will aspire to:

> start → finish → start → finish → ∞

Let's download what we've got:

- Select vectors;
- Choose svg as an extension;
- Click Export.

![Download and unpack the archive](https://miro.medium.com/max/700/0*flt4HIeWYH8eQPH6.jpg "Download and unpack the archive")

## Combine two SVGs into one animated one

Open the downloaded svg and create a new one:

![](https://img-host.ru/cdLwm.jpg)

Copy the contents of start into result:

![](https://img-host.ru/PPyo7.jpg)

In result.svg make the path tag paired:

![](https://img-host.ru/1Dr98.jpg)

I'll remove the width and height attributes so they don't get in the way.

In the viewBox I set the maximum possible height and width:

- In start.svg width = 363, and in finish.svg width = 364. I take 364;
- in start.svg height = 302, and in finish.svg = 311. I take 311.

![](https://img-host.ru/546Re.jpg)

Key point: we'll use the [animate tag](https://developer.mozilla.org/en-US/docs/Web/SVG/Element/animate) to animate.

> Pay attention to browser support!

Put it inside the path:

![](https://img-host.ru/cU2r8.jpg)

Briefly on the attributes:

- repeatCount - how many times the animation will happen. Set indefinite to set an infinite number of iterations;
- attributeName - the name of the attribute, which will be animated. In our example it is d, where the coordinates of the figure are kept;
- dur - animation duration.

Let's add another one - values. Let's copy into it the value of attribute d from the current path tag:

![These are the same coordinates we drew in the first bubble](https://img-host.ru/GyB61.jpg)

Add to it the value of the d attribute from the file finish.svg:

![Don't forget a semicolon after each coordinate](https://img-host.ru/2OE0w.jpg)

The third line is copied from the first in order to close the animation:

```html
<animate repeatCount="indefinite" attributeName="d" dur="10s"
  values="M314 46.0001C253 0 137 -28 52.9999 46.0001C-31.0001 120 -1.0002 202 52.9999 248C107 294 247 340 314 248C381 156 375 92.0001 314 46.0001Z;
  M302.348 71.5969C209 -48 69.1956 6.19389 41.3478 71.5969C13.5 137 -35.5 223 41.3478 273.597C118.196 324.194 233.195 322.694 302.348 273.597C371.5 224.5 395.695 191.194 302.348 71.5969Z;
  M314 46.0001C253 0 137 -28 52.9999 46.0001C-31.0001 120 -1.0002 202 52.9999 248C107 294 247 340 314 248C381 156 375 92.0001 314 46.0001Z;"></animate>
```

## Result:

You can see what it looks like at the beginning of the article.

I'm also going to put the svg itself here:

```html
<svg viewBox="0 0 364 311" fill="none" xmlns="http://www.w3.org/2000/svg">
  <path d="M314 46.0001C253 0 137 -28 52.9999 46.0001C-31.0001 120 -1.0002 202 52.9999 248C107 294 247 340 314 248C381 156 375 92.0001 314 46.0001Z" fill="#FFCC00">
    <animate repeatCount="indefinite" attributeName="d" dur="10s"
      values="M314 46.0001C253 0 137 -28 52.9999 46.0001C-31.0001 120 -1.0002 202 52.9999 248C107 294 247 340 314 248C381 156 375 92.0001 314 46.0001Z;
        M302.348 71.5969C209 -48 69.1956 6.19389 41.3478 71.5969C13.5 137 -35.5 223 41.3478 273.597C118.196 324.194 233.195 322.694 302.348 273.597C371.5 224.5 395.695 191.194 302.348 71.5969Z;
        M314 46.0001C253 0 137 -28 52.9999 46.0001C-31.0001 120 -1.0002 202 52.9999 248C107 294 247 340 314 248C381 156 375 92.0001 314 46.0001Z;"></animate>
  </path>
</svg>
```

And [codepen](https://codepen.io/vadimfilimonov/pen/OJydRLL), where you can get a better look at it.
