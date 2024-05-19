---
# Documentation: https://docs.hugoblox.com/managing-content/

title: "Learning Python"
summary: "I have been playing with Python recently."
authors: ["jpgoldberg"]
tags: ["python", "programming"]
categories: []
date: 2024-05-18T17:00:02-05:00

# Optional external URL for project (replaces project detail page).
external_link: ""

# Featured image
# To use, add an image named `featured.jpg/png` to your page's folder.
# Focal points: Smart, Center, TopLeft, Top, TopRight, Left, Right, BottomLeft, Bottom, BottomRight.
image:
  caption: ""
  focal_point: ""
  preview_only: false

# Custom links (optional).
#   Uncomment and edit lines below to show custom links.
# links:
# - name: Follow
#   url: https://twitter.com
#   icon_pack: fab
#   icon: twitter

url_code: ""
url_pdf: ""
url_slides: ""
url_video: ""

# Slides (optional).
#   Associate this project with Markdown slides.
#   Simply enter your slide deck's filename without extension.
#   E.g. `slides = "example-slides"` references `content/slides/example-slides.md`.
#   Otherwise, set `slides = ""`.
slides: ""
---

I've found myself playing with Python recently.
Although my first encounter with Python was in the 90s looking
through the code of the Mailman mailing list system, I had
entirely ignored the language ecosystem until recently.

I have been using it and Jupyter Notebooks to describe some
computations and algorithms as part of my
[security team training]({{< relref "/project/sec-training" >}}).
Python is more readable to most people than R,
and so I transitioned from RMarkdown to Jupyter Notebooks.

I still dislike Python's dynamic typing and referential unclarity,
but it is nice to be able to demonstrate concepts from cryptography
without having to explicitly use a Bigint library.
I am certainly not suggesting
that cryptographic or security focused applications be written in Python.
Quite the opposite.
But if I wish to walk through toy RSA examples for people with limited
programming backgrounds, Python is a good choice.

So here, I point to a few things I've been doing with Python.
They range in completeness and in the skill level that they exhibit.

## Powerset

I needed (well, wanted) to be able to create power sets,
and I was surprised by the lack of existing python packages that
met my needs.
So I took the opportunity to learn how to create a package for PyPi:
[powerset-generagor on PyPi](https://pypi.org/project/powerset-generator/).
The details of why I thought making a package for such a simple bit of code
[was a good idea](https://jpgoldberg.github.io/powerset-generator/yapp.html)
are included in the package [documentation](https://jpgoldberg.github.io/powerset-generator/).

The project itself is on GitHub: https://github.com/jpgoldberg/powerset-generator

## Hostname

I was surprised to learn that there was no standard's compliant
Python tool for validating whether a string is a valid Internet
hostname.
And so I developed [python-hostname](https://github.com/jpgoldberg/python-hostname),
which I have chosen not to publish on PyPi.
It is likely that other packages will introduce
good ways to syntactically validate hostnames,
and so there will be little need for my package.
Nonetheless, the extensive
[documentation](https://jpgoldberg.github.io/python-hostname/)
I have created for it
should help illustrate properly validating hostnames
is not as simple as a search of Stack Exchange might suggest.

## Toy Cryptography

It is probably best for me to just quote from the `README`,
of my toy-crypto-math [repository](https://github.com/jpgoldberg/toy-crypto-math)

> This is almost certainly not the package you are looking for.
>
> The material here is meant for learning purposes only, often my own learning.
> Do not use it for anything else. And if you do, understand that it focuses on what
> I am trying to illustrate or learn. It may not always be correct.
>
> - If you want to use cryptographic tools in Python use [pyca].
> - If you want to play with some of the mathematics of some things underlying Cryptography in
> a Python-like environment use [SageMath], [sympy], or [primefac].

[pyca]: https://cryptography.io
[SageMath]: https://doc.sagemath.org/
[sympy]: https://www.sympy.org/en/
[primefac]: https://pypi.org/project/primefac/

I do not foresee ever producing a package for distribution of this.
And if I do, I would certainly need to include more prominent warnings.


