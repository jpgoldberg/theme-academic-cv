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
url_slides: pwcon22-with-notes.pdf

url_code:
url_pdf:
url_video: https://www.infosecurity.us/blog/2022/10/21/bsideslv-2022-lucky13-passwordscon-jeffrey-p-goldbergs-can-a-password-management-service-safely-learn-about-users-passwords

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

Many services,
and particularly 1Password,
where I worked at the time this talk was presented,
simultaneously have a need to understand how users are using the client applications
while also providing strong and demonstrable privacy guarantees to those same users.

This talk, as part of PasswordsCon (US) 2022, described the problem
by first pointing out that mere removal of
{{< abbr PII "Personally Identifying Information">}}
is insufficient
and by using an extreme example.
If a solution could be found for the extremely sensitive user data
than such a solution could be applied to all data.

I then went on to discuss historical approaches used in the Social Sciences,
leading up to concepts of differential privacy.


