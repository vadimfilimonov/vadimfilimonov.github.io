---
layout: post
title:  "Block rendering with JavaScript"
date:   2021-10-11 18:00:00 +0300
categories: frontend
---

## Задача

Есть [API](https://private-531a0-vadimfilimonovblog.apiary-mock.com/frameworks), который в ответ на запрос отдает json со списком фреймворков и их описанием. Необходимо на его основе отрендерить карточки.

![Cards](https://sun9-86.userapi.com/impg/Gikuh5C_7CJjQWW6LXDVFu6GDzPGSP_eF-Go9w/GHtQ_aZJ5os.jpg?size=674x462&quality=96&sign=0e72025efff28459e34e6a4b8b1f7faf&type=album)

## Алгоритм
1. Получить список;
2. Обработать список;
3. Отрендерить в HTML.

### 1. Получить список

Для данной статьи я подготовил тестовые данные, которые можно получить по адресу:

```
https://private-531a0-vadimfilimonovblog.apiary-mock.com/frameworks
```

Чтобы сделать HTTP запрос — используйте метод [fetch](https://developer.mozilla.org/en-US/docs/Web/API/Fetch_API/Using_Fetch):

{% highlight css %}
fetch("https://private-531a0-vadimfilimonovblog.apiary-mock.com/frameworks")
{% endhighlight %}

### 2. Обработать список

Вот как выглядит json, который мы получаем:

{% highlight json %}
{
  "success": true,
  "list": [
    {
      "title": "React",
      "text": "React is an open-source...
{% endhighlight %}

Напишем функцию `buildHTML`, которая на вход будет принимать JSON, а отдавать строку, которую мы в будущем используем как HTML:

{% highlight javascript %}
// HTTP запрос
fetch("https://private-531a0-vadimfilimonovblog.apiary-mock.com/frameworks")
  // переводим ответ в json
  .then(response => response.json())
  // конвертируем в html
  .then(buildHTML)
{% endhighlight %}

Определение функции:

{% highlight javascript %}
const buildHTML = ({ list }) =>
  list.map(({ title, text }) => (`
    <div>
      <h2>${title}</h2>
      <p>${text}</p>
    </div>
  `)).join("");
{% endhighlight %}

### 3. Отрендерить в HTML

{% highlight javascript %}
fetch("https://private-531a0-vadimfilimonovblog.apiary-mock.com/frameworks")
  .then(response => response.json())
  .then(buildHTML)
  // полученный результат передает в функцию render
  .then(render);
{% endhighlight %}

В файле HTML создадим пустой контейнер, куда будем вставлять карточки:

{% highlight html %}
<div class="container"></div>
{% endhighlight %}

Работа функции render сводится лишь к использованию свойства [innerHTML](https://developer.mozilla.org/en-US/docs/Web/API/Element/innerHTML):

{% highlight javascript %}
const render = (html) => {
  const container = document.querySelector('.container');
  container.innerHTML = html;
};
{% endhighlight %}

![Result](https://sun9-8.userapi.com/impg/YNDIxW64gsC2v3l2HzRqr9U8RgB82Os4vdYI3g/akmlzM5vrHA.jpg?size=693x531&quality=96&sign=a83c8b268137c0d35e4db9789fbf0446&type=album)

Полную версию кода смотрите на [codepen](https://codepen.io/vadimfilimonov/pen/QWEzLow).

## Additional materials

- [This article is in Russian](https://vk.com/@filimonovvadim-render-page-via-js)
