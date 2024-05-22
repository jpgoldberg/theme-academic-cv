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
The intranet is a _trusted_ network environment for hosting systems, services, and data internal to the enterprise.
The opennet is an _untrusted_ network environment (e.g., the Internet) that includes all systems external to the enterprise. [Emphasis added]
{{< /quote >}}

In what follows, I will be referring to these as the “green zone” and the ”red zone” respectively.
I am ignoring yellow zones (DMZ) and other zones security zones that may have been put in place.

The relevant portion of the accompanying threat model was that network traffic originating inside the green zone was benign,
while traffic originating from the red zone may be malicious.
It is certainly fair to assume that traffic originating from outside the organization is more likely to be hostile than traffic originating internally,
but that hardly means that we shouldn't worry about threats from within the organizations network.

{{< figure
  src="ssl_added_and_removed.png"
  title="SSL added and removed here :-)"
  caption="Detail of 2103 leaked NSA slide: Source: Washington Post" >}}

### The Rationale

For those two young to recall the technological environment in which that threat model emerged,
there are two important things to note.

Organizations typically had their hosts on premise,
including both servers and user workstations.
This meant that there was a natural distinction between internal and external networks,
with a one or a small number of gateways between the two.
Firewalls could be incorporated into those gateways or immediately adjacent to them.
The network topology gave us a place to filter and block suspect network traffic.
We had a perimeter that could be defended with perimeter firewalls.

Another point about the technological environment is that IT managers and system administrators
were wary of updating or upgrading server systems and software.
Updates broke things.
Client systems often depended on undocumented service behavior.[^822]
Software and systems vendors were often slow to release security updates.
Responsible disclosure was not at widely accepted then and so vendors had less incentive to address security vulnerabilities.
The consequence of all this is that internal systems riddled with exploitable security vulnerabilities.

[^822]: This footnote is too small to contain my rant about systems encouraging the use of malformed data.
A large part of why things broke after an update is that malformed input was handled differently,
often subtly so, in new versions.
Such changes in behavior were often not intended behavior,
but a side effect of other changes.

In that environment, the practical way to protect servers within the organization was through perimeter firewalls.[^14]
In short, our practical defensive technologies drove our threat model.

[^14]: Endpoint management of user workstations was also a way to reduce the threat of malicious traffic originating from within the green zone.
Anti-virus and frequent re-imaging of user workstations was a regular practice,
illustrating that people did know that the green zone wasn't always trustworthy.

## Where things go wrong

I am absolutely support the practice of putting our defenses where we can.
There really isn't an alternative to that.
Relying on perimeter firewalls was a necessity.
The problem arises when we let that drive our threat model.
It is far better to explicitly acknowledge threats that we can't defend against
than to pretend that those threats don't exist or don't matter.

If we come to believe our rationales for excluding something from the threat model
we may find ourselves slower to adopt technologies that come along to address those threats.
After all, we aren't going to really notice solutions to problems we don't think we have.
I have no evidence to suggest that green zone thinking delayed transition from from `telnet` to `ssh`,
or from {{< abbr "POP3" "Post office protocol" >}} to
{{< abbr "POP3S" "POP3 over SSL" >}}.

Consider the old days of network topology which had a physical organization network with a gateway to out to be the big bad world. Often the servers within the network were hard to upgrade, both as security patches were less commonly available, and any software or system upgrade could easily break things.

In those days, we operated under the assumption that traffic originating from outside of the organization's network (red zone) might be hostile, while traffic from instead the network (green zone) was trustworthy. This was the basis of the threat model that put all of our defenses on the perimeter firewall.

But the green zone assumption was always bogus. And I don't think that anyone genuinely believed it, but the defensive tools that we had gave us the ability to control traffic from the red zone and not from the green zone. So we ended up calling the green zone, green.

So your example of threats to worms. It's fine if we say (A).

(A) We can't defend against rain, so we will exclude that threat from our model.

The practicalities may demand such things as (A). But what I often hear is

(B) We exclude rain from our threat model because an attacker who can manipulate the weather can already defeat everything else we do.

Rationales like (B) may or may not be true, but they are not the real reasons for excluding something from the threat model. It is far better to think about things in terms of (A) because it means that you are both more aware of the risks you face and you have a smoother way of updating your model as new defenses become available. Back to my green/red zone example, I suspect that thinking like that delayed the deployment of zero-trust mechanisms within an organization.
