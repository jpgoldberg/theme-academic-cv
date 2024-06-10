---
# Documentation: https://docs.hugoblox.com/managing-content/

title: "Can a password management service safely learn about users' passwords?"
event: "PasswordsCon BSidesLV 2022"
event_url: https://archive.bsideslv.org/2022/schedule#PASS
location: Tuscany Suites and Casino, Las Vegas, Nevada
address:
  street: 255 E Flamingo Rd
  city: Paradise
  region: Nevada
  postcode: 89169-4708
  country: Unitied States
summary: Discussion of privacy preserving ways to gather analytic data of potentially highly sensitive user before. 
abstract:

# Talk start and end times.
#   End time can optionally be hidden by prefixing the line with `#`.
date: 2022-08-09T11:00:00-07:00
date_end: 2022-08-09T12:00:00-07:00
all_day: false

# Schedule page publish date (NOT event date).
publishDate: 2022-07-15

authors: [jpgoldberg]
tags: []

# Is this a featured event? (true/false)
featured: true

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

# Optional filename of your slides within your event's folder or a URL.
url_slides: totp-talk.pdf

url_code:
url_pdf:
url_video: 

# Markdown Slides (optional).
#   Associate this event with Markdown slides.
#   Simply enter your slide deck's filename without extension.
#   E.g. `slides = "example-slides"` references `content/slides/example-slides.md`.
#   Otherwise, set `slides = ""`.
slides: ""

# Projects (optional).
#   Associate this post with one or more of your projects.
#   Simply enter your project's folder or file name without extension.
#   E.g. `projects = ["internal-project"]` references `content/project/deep-learning/index.md`.
#   Otherwise, set `projects = []`.
projects: []
---

Google's introduction of the `otpauth` URI scheme made it easy 
for people and organization to deploy
and for individuals to enroll in
{{<abbr TOTP "Time-based One Time Password">}} authentication.
However, the initial implementations and description of the scheme left a number of ambiguities in and inconsistences in place.

This 2019 PasswordsCon talk discussed those ambiguities and contradictions along with some of the consequences I had observed.
I agrue that in general we need more well-constructed standards and complience with those standards, even though I don't offer a clear path for fixed TOTP.

## Context for these slides

This talk was presented when I worked for 1Password.
I have updated contact information in the slides and switched to typefaces which have freer licenses.

PasswordCon has a tradition of including pictures of cats on slides that present background that most audience members are already familiar with.
I had also been challenged to include something from my visit to the [Vasa Museum](https://www.vasamuseet.se/en)
