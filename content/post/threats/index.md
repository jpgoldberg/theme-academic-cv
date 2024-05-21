---
# Documentation: https://docs.hugoblox.com/managing-content/

title: "Rationalizing threat models"
subtitle: ""
summary: "Threat models are often tacitly defined in terms of what we can or can't defend against. This practice should be made explicit instead of creating bogus rationales for excluding the threats we can't defend against."
authors: []
tags: []
categories: []
date: 2024-05-21T11:57:11-05:00
lastmod: 2024-05-21T11:57:11-05:00
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

So you have hit upon one of my biggest gripes about how threat modeling is conceived. It is often tacitly focused on "what we can defend against".


## All that's green does not glitter

Let's consider a threat model lived for about a quarter of a century.

{{< quote source="Ramasamy et al (2011)"
    src="https://www.usenix.org/legacy/event/hotice11/tech/full_papers/Ramasamy.pdf" >}}
The intranet is a trusted network environment for hosting systems, services, and data internal to the enterprise.
The opennet is an untrusted network environment (e.g., the Internet) that includes all systems external to the enterprise.
{{< /quote >}}

In what follows, I will be referring to these as the “green zone” and the ”red zone” respectively.
I am ignoring yellow zones (DMZ) and other zones security zones that may have been put in place. 

The relevant portion of the accompanying threat model was that network traffic originating inside the green zone was benign,
while traffic originating from the red zone may be malicious.

Consider the old days of network topology which had a physical organization network with a gateway to out to be the big bad world. Often the servers within the network were hard to upgrade, both as security patches were less commonly available, and any software or system upgrade could easily break things.

In those days, we operated under the assumption that traffic originating from outside of the organization's network (red zone) might be hostile, while traffic from instead the network (green zone) was trustworthy. This was the basis of the threat model that put all of our defenses on the perimeter firewall.

But the green zone assumption was always bogus. And I don't think that anyone genuinely believed it, but the defensive tools that we had gave us the ability to control traffic from the red zone and not from the green zone. So we ended up calling the green zone, green.

So your example of threats to worms. It's fine if we say (A).

(A) We can't defend against rain, so we will exclude that threat from our model.

The practicalities may demand such things as (A). But what I often hear is

(B) We exclude rain from our threat model because an attacker who can manipulate the weather can already defeat everything else we do.

Rationales like (B) may or may not be true, but they are not the real reasons for excluding something from the threat model. It is far better to think about things in terms of (A) because it means that you are both more aware of the risks you face and you have a smoother way of updating your model as new defenses become available. Back to my green/red zone example, I suspect that thinking like that delayed the deployment of zero-trust mechanisms within an organization.
