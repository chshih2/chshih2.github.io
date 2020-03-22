---
layout: post
title: "Markdown Template"
description: "Markdown features for the posts"
categories: [website]
tags: [markdown]
redirect_from:
  - /2020/03/22/
---
<script type="text/javascript" async
  src="https://cdn.mathjax.org/mathjax/latest/MathJax.js?config=TeX-MML-AM_CHTML">
</script>


Here are all the most important features I need for my post template and their
markdown formats.

This [markdown][1] article gave a nice introduction of markdown file.
I got the formats to create [**sections**](#sections),
[**lists**](#lists), [**links**](#links), and [**separation lines**](#horizontals).
To import [**images**](#images), I used HTML syntax like how [kushdilip][2] did.
For [**bookmarks**](#bookmarks), I got the answer from [Steve][3].
For [**equations**](#equations), I used [MathJax][4].

---

# <a name="sections"></a>Section
```
# This gives me titles
```
The format of sentences and paragraphs follows LaTex. Use `` ` `` ... `` ` `` for [escaping][5].
# This gives me titles

---

# <a name="lists"></a>List
```
*  List
    * Item
```
Use indents to create nested items. The symbols will be different at each level automatically.
*  List
    * Item

```
1.  List 1
    1. Item 1
    2. Item 2
2.  List 2
    1. Item 1
    2. Item 2
```

1.  List 1
    1. Item 1
    2. Item 2
2.  List 2
    1. Item 1
    2. Item 2

---

# <a name="links"></a>Link
```
go [there][1]
[1]:https:...
```

---

# <a name="horizontals"></a>Separation Lines
```
---
```

---

# <a name="images"></a>Image
```
<img src="turtle.jpg" alt="drawing" width="200"/>
<img src="https://images.unsplash.com/photo-1518467166778-b88f373ffec7?ixlib=rb-1.2.1&ixid=eyJhcHBfaWQiOjEyMDd9&auto=format&fit=crop&w=1778&q=80" alt="turtle1" width="200"/>
```
<img src="turtle.jpg" alt="turtle2" width="200"/>
<img src="https://images.unsplash.com/photo-1518467166778-b88f373ffec7?ixlib=rb-1.2.1&ixid=eyJhcHBfaWQiOjEyMDd9&auto=format&fit=crop&w=1778&q=80" alt="drawing" width="200"/>

I used HTML instead of another common approach [`![]()`][1] because it's easier to scale the image under my theme template.

---

# <a name="bookmarks"></a>Bookmark
```
Take me [here](#bookmark)
Put anchor point <a name="bookmark"></a>
```

---

# <a name="equations"></a>Equation
```
$$x_{1,2} = \frac{-b \pm \sqrt{b^2-4ac}}{2b}.$$
or
\begin{equation}x_{1,2} = \frac{-b \pm \sqrt{b^2-4ac}}{2b}\end{equation}
```

$$x_{1,2} = \frac{-b \pm \sqrt{b^2-4ac}}{2b}.$$

I use MathJax instead of generating images directly from LaTex because it makes searching easier.

To enable MathJax, do this in your script:
```
<script type="text/javascript" async
  src="https://cdn.mathjax.org/mathjax/latest/MathJax.js?config=TeX-MML-AM_CHTML">
</script>
```

[1]:https://programminghistorian.org/en/lessons/getting-started-with-markdown
[2]:https://stackoverflow.com/questions/14675913/changing-image-size-in-markdown
[3]:https://stackoverflow.com/questions/5319754/cross-reference-named-anchor-in-markdown
[4]:https://www.mathjax.org/
[5]:https://www.markdownguide.org/basic-syntax/
