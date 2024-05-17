---
# Leave the homepage title empty to use the site title
title: ''
date: 2022-10-24
type: landing

sections:
 
  - block: about.biography
    id: about
    content:
      title: Biography
      # Choose a user profile to display (a folder name within `content/authors/`)
      username: jpgoldberg

  - block: skills
    content:
      title: Skills
      text: ''
      # Choose a user to display skills from (a folder name within `content/authors/`)
      username: jpgoldberg
    design:
      columns: '1'

  - block: experience
    content:
      title: Experience
      # Date format for experience
      #   Refer to https://docs.hugoblox.com/customization/#date-format
      date_format: Jan 2006
      # Experiences.
      #   Add/remove as many `experience` items below as you like.
      #   Required fields are `title`, `company`, and `date_start`.
      #   Leave `date_end` empty if it's your current employer.
      #   Begin multi-line descriptions with YAML's `|2-` multi-line prefix.
      items:
        - title: Principal Security Architect, Chief Defender Against the Dark Arts, Support
          company: 1Password
          company_url: 'https://1password.com'
          # company_logo: org-gc
          location: Remote
          date_start: '2010-04-01'
          date_end: '2023-06-30'
          description: |2-

              * Assisted in Security design of OPVault format (introduced 2012)
              *  Assisted in Security design of 1Password service (introduced 2015)
              * Managed team responsible for all aspects of product and organization security (2013–2022)
              * Developed internal and external security documentation
              * Developed first security manual and incident response plan
              * Reviewed code (Rust, Go, Swift, Typescript, Kotlin, Java, Objective-C)
              * Primary developer of SRP and password generator modules 
        
        - title: Freelance system administration
          location: Riverside, California; Plano, Texas
          date_start: "2000-09-01"
          date_end: "2008-10-01"
          description: |2-

            * Installed and managed network services for small and medium sized enterprises
            * Linux and FreeBSD system setup, firewalls (m0n0wall, iptables), mail transport (exim, sendmail, UW imapd, spamassassin)
       
        - title:  Asst. Information Officer, Network Programmer
          company: Cranfield University Computing Centre
          location: Cranfield, Beds., UK
          date_start: '1994-04-01'
          date_end: '2000-06-15'
          description: |2-

             * Cranfield University (UK) was among the very first UK universities to enable staff and students to create personal web pages.
             * Taught Introduction to C Programing to Masters students in the Applied Mathematics and Computing Department (Autumn 1999)
             * Set up and managed email system (exim, uw-imapd)
             * Trained staff and students in web technology, PGP, and \LaTeX
             * Assisted information officer in developing and maintaining university website
             * Unix system (OSF, Linux) administration, DNS (bind), NTP, general scripting
  
        - title: Researcher
          company: Research Institute for Linguistics, Hungarian Academy of Science
          position: Researcher
          location: Budapest, Hungary
          date_start: "1988-09-01"
          date_end: "1993-11-01"
          description: |2-

            * Taught Syntax and Computing in Theoretical Linguistics Department
            * Unix system administration work
              
    design:
      columns: '2'

  - block: collection
    id: posts
    content:
      title: Recent Posts
      subtitle: ''
      text: ''
      # Choose how many pages you would like to display (0 = all pages)
      count: 5
      # Filter on criteria
      filters:
        folders:
          - post
        author: ""
        category: ""
        tag: ""
        exclude_featured: false
        exclude_future: false
        exclude_past: false
        publication_type: ""
      # Choose how many pages you would like to offset by
      offset: 0
      # Page order: descending (desc) or ascending (asc) date.
      order: desc
    design:
      # Choose a layout view
      view: compact
      columns: '2'

  - block: portfolio
    id: projects
    content:
      title: Projects
      filters:
        folders:
          - project
      # Default filter index (e.g. 0 corresponds to the first `filter_button` instance below).
      default_button_index: 0
      # Filter toolbar (optional).
      # Add or remove as many filters (`filter_button` instances) as you like.
      # To show all items, set `tag` to "*".
      # To filter by a specific tag, set `tag` to an existing tag name.
      # To remove the toolbar, delete the entire `filter_button` block.
      buttons:
        - name: All
          tag: '*'
        - name: Deep Learning
          tag: Deep Learning
        - name: Other
          tag: Demo
    design:
      # Choose how many columns the section has. Valid values: '1' or '2'.
      columns: '1'
      view: showcase
      # For Showcase view, flip alternate rows?
      flip_alt_rows: false

  - block: collection
    id: featured
    content:
      title: Featured Publications
      filters:
        folders:
          - publication
        featured_only: true
    design:
      columns: '2'
      view: card
      
  - block: collection
    content:
      title: Recent Publications
      text: |-
        {{% callout note %}}
        Quickly discover relevant content by [filtering publications](./publication/).
        {{% /callout %}}
      filters:
        folders:
          - publication
        exclude_featured: true
    design:
      columns: '2'
      view: citation

  - block: collection
    id: talks
    content:
      title: Recent & Upcoming Talks
      filters:
        folders:
          - event
    design:
      columns: '2'
      view: compact

  - block: contact
    id: contact
    content:
      title: Find me
      subtitle:
      email: jeffrey@example.org
      contact_links:
        - icon: mastodon
          icon_pack: fab
          name: 'jpgoldberg@ioc.exchange'
          link: 'https://ioc.exchange/@jpgoldberg'
        - icon: github
          icon_pack: fab
          link: 'https://github.com/jpgoldberg'
          name: jpgoldberg
  
      # Automatically link email and phone or display as text?
      autolink: true
      # Email form provider
    design:
      columns: '2'
---
