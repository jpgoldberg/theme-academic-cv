---
# Documentation: https://docs.hugoblox.com/managing-content/

title: "Telling (La)TeX what you mean"
subtitle: ""
summary: "LaTeX is a 'what you get is what you mean' system, which on the whole allows for both better output and appropriate focus on content when writing. This does, however, place some additional burden on the user to be clear about meanings."
authors: [jpgoldberg]
tags: []
categories: []
date: 2024-07-02T10:48:41-05:00
lastmod: 2024-07-02T10:48:41-05:00
featured: false
draft: true

# Featured image
# To use, add an image named `featured.jpg/png` to your page's folder.
# Focal points: Smart, Center, TopLeft, Top, TopRight, Left, Right, BottomLeft, Bottom, BottomRight.
image:
  caption: ""
  focal_point: ""
  preview_only: false

# Projects (optional).
#   Associate this post with one or more of your projects.
#   Simply enter your project's folder or file name without extension.
#   E.g. `projects = ["internal-project"]` references `content/project/deep-learning/index.md`.
#   Otherwise, set `projects = []`.
projects: []
---

This article should be interesting to anyone with a concern for high quality document preparation,
but it is primarily addressed to people with some familiarity with [LaTeX].
I have observed that a number of people who use [LaTeX] fail to understand an extremely important feature of it which makes it so superior to many other systems.
As a result, they can produce results that are inferior to common word processing systems.

## What you see and what you get

I believe that it was Richard Kinch who (in the 1990s) characterized word-processing systems as “what you see is all you get”,
which I will call
All You Get ({{< abbr "AYG" "All You Get" >}})
systems.
This is in contrast to semantic markup systems, like LaTeX, which are better characterized as “what you get is what you mean”,
and I will call
What You Mean ({{< abbr "WYM" "What You Mean" >}})
systems.[^ayg]

[^ayg]: Styles have since been introduced in common word processors, substantially mitigating that problem. Likewise, LaTeX is far from a purely semantic markup system, but it will be easier for me to initially present a distilled and exaggerated form of the distinction.


A simple example is to contrast what you would need to do for a document section heading in a purely
{{< abbr "AYG" "All You Get" >}} system
to what you need to to in LaTeX.

In LaTeX you might write something like

```latex
... and this analysis takes us to our conclusions. 

\section{Conclusions}

We can conclude from what has been presented above
that my extrodinary and revolutionary work
should be more than sufficient to
convince the Tenure and Promotions Committee at my university
that I should be granted tenure without the need for external reviews.
Furthermore, ...
```

In a _purely_ {{< abbr "AYG" "All You Get" >}} system
you would need to specify exactly how you would like the line
with the text “Conclusions” to appear in terms of
font choices (perhaps boldface),
text size,
distance between the line and preceding paragraph,
distance between the line and the following paragraph,
manually inserting a copy of the section header into a table of contents,
Perhaps taking steps to prevent a page break after the section header.
And most importantly you would need to do this for every section heading
and ensure consistency throughout.

Of course modern word processors are not purely
{{< abbr "AYG" "All You Get" >}} systems,
and so they do provide styles for sections,
but my goal is to illustrating contrasting approaches to document preparation.

With LaTeX you can take control of all of those choices about how section headers should be typeset,
but it is something you do elsewhere.
When you are writing your content, you just say what you mean.

## Responsibility to say what you mean

Standard LaTeX document styles provide you with the ability to say that you mean something to be a header for a new section.
So it is easy to say what you mean when you do mean something to
be a header of a new section of your document.
But now let me move to some examples where the responsibility tell LateX what you mean takes a bit more work.

### The dot-space (‘`. `') sequence

Consider text like 

```text
Dr. Smith wondered whether she should contact the F.B.I. about
what she had discoverd. It kept her up at night,
but eventually she did call the F.B.I. That act changed her life
and the lives of thousands of others.
```

In that text we have four different instances of a dot-space, '`. `' sequence.

1. `Dr. Smith`
2. `F.B.I. about`
3. `discovered. It`
4. `F.B.I. That`

Those four instances of a dot-space sequence have different meanings,
and those different meaning affect how the text should be typeset.
Before desktop computers, people prepared manuscripts on typewriters 
or even handwritten documents.
A professional compositor would read something like
our sample text above and know how
to interpret each of the four cases
and use that knowledge in their typesetting.
The person who wrote the text may have some tacit knowledge of
the distinct cases,
but is unlikely to be explicitly aware of that knowledge.

Let's start with the clearest difference,
which is between case 1 and case 3.
We know that the dot-space sequence is in case 3 marks the separation of sentences
while the dot-space sequence in case 1 is part of a persons name and title.
The effect on typesetting here is also the starkest.
English language typesetting often puts a little bit more horizontal space between sentences than it does between words within a sentence.
We want that extra space in case 3,
but output will look wrong if we have that extra space in case 1.
Other things being equal,
line breaks between sentences are better than line break between words within a sentence.
A line break in case 1, however, would be terrible.

The underlying algorithm that TeX uses to break paragraphs into lines knows how to encourage line breaks between sentences and to put a little bit of extra space between sentences.
It is this kind of optimization that makes TeX output so good.[^horrid]
But for TeX to do its job it needs to be told
that the dot-space sequence in case 1 is not a sentence break.
This puts a responsibility on the user to tell TeX that the dot-space sequence in 1 has a different meaning.
For this we would write ‘`Dr.~Smith`’ in our input.
Failing to help LaTeX know what you mean in such cases can really
produce very bad output.

[^horrid]: When TeX finds a solution that it is happy with, it is almost always better than what other systems produce. But when it fails to find a solution that it is happy with, it will report an error and produce terrible output for that paragraph. In other words, when it is good it is very very good, but when it is bad it is horrid.

The difference between cases 2 and 4 is more subtle.
Fortunately it doesn't come up that often,
particularly as people tend to write “FBI” instead of ”F.B.I.”
In case 2 the space has the meaning of a space between words within a sentence.
The space should be treated exactly as any other inter-word space
with respect to line breaking and amount of horizontal space.
In case 4, the space is between sentences,
and so it ought to be a better place for a line break
than the space in case 2,
and it should have the extra horizontal space that is used between sentences.

The underlying TeX algorithm will treat both 2 and 4 as not
marking a sentence boundary.
So LaTeX's output will be less optimal in in case 4, but it won't be horrid.
Still, you can help LaTeX know that you mean a sentence break in case 4
by writing '`F.B.I.\@ That`'.
This is not nearly as important as using '`Dr.~Smith`', but it does help illustrate why LaTeX is so good at setting paragraphs when given the information it needs.


[LaTeX]: https://www.latex-project.org/ "The LaTeX Project"
