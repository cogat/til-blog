---
title: "ACMI’s Standards for exhibition technology"
author: "Greg Turner"
date: 2020-08-13T01:20:52.900Z
lastmod: 2024-04-07T14:21:17+10:00

description: ""

subtitle: "How does a museum set standards for technology when its footprint is so varied? Here’s our attempt, and we’ve made it remixable."

featured_image: '/posts/acmis-standards-for-exhibition-technology/images/1.jpeg'

---

When I arrived at ACMI three years ago, I had a relatively naïve understanding of how much museums invest in the quality and robustness of their digital technology. Obviously, no-one wants their technology to fail, but museums — especially technology-rich ones like ACMI — face challenges of robustness, demand and scale that are unlike any other industry sector:

* How can we plan for no accessible cabling but easy maintainability?
* An artist has made a work with technology we’ve never encountered before. How can we look after it for an exhibition?
* How can we provide security when we literally let the public in through our front door?
* What if there’s a software crash when an exhibition’s on tour, on the other side of the world?
* How can anyone keep track of all these kids? _(ok, that last one may not be strictly a hardware question)_
![image](/posts/acmis-standards-for-exhibition-technology/images/1.jpeg#layoutTextWidth)
The Tea Party from our Wonderland exhibition. How do you apply standards to something like this?

Happily, my colleagues at ACMI have decades of experience preparing and installing technology for major exhibitions, and are always generous in sharing their knowledge. In addition, we’d been running _Screenworlds_, our permanent exhibition, for coming up to ten years and knew what we wanted to do differently next time round. In particular [Sean Doyle](https://medium.com/u/2a58c737dea8) had captured 14 years of eye-opening knowledge in a long-form document “Advice for Developers”.

As we prepared to procure all the technology for ACMI’s _Re/newal_, we have collated all the conversations with our in-house experts, Sean, Travis Geldard, Paul Cuthbert, Chris Harris, Glenn Willey and the team of developers into **“**[**ACMI’s standards for exhibition technology**](https://github.com/ACMILabs/tech-standards/wiki)**”**, which we are releasing today in Creative Commons wiki form on Github so that our colleagues can hopefully re-use, remix and improve. Excerpts from the front page are below; [follow the link to access the whole thing](https://github.com/ACMILabs/tech-standards/wiki).

_ACMI often provides advice and consulting to other museums and cultural institutions, helping them design and build better exhibitions and experiences. These standards are part of that sector advice —_[_if you’d like to chat to our experts then get in touch_](https://www.acmi.net.au/contact/)_!_### Common Standards for Exhibition Technology

This document sets out a supplier-facing set of guidelines, grouped by technology area. At ACMI we are using these standards as a procurement tool and sign-off checklist, and we thought it would be useful to publish them here so that our colleagues can benefit. We would love to see forks, remixes, extensions and contributions to this work — particularly to incorporate COVID-safe guidelines!

![image](/posts/acmis-standards-for-exhibition-technology/images/2.jpeg#layoutTextWidth)
We have to keep these weird things running. Not pictured: heaps more weird things.

### Usage

This work is licensed under [CC BY-SA 4.0](https://github.com/ACMILabs/tech-standards/wiki/LICENSE.md), particularly the bit where no warranties are given.

A further note: these are not engineering standards or to be relied upon for building infrastructure, safety or compliance. For power, networking, cooling, lighting and audio, we got the experts in, and you should too.

### Context and environment

In short, design and deliver technology for groups of smart, raucous schoolchildren. They will be curious, engaged, inspired, experimental and will admire the beauty of things. But they will also hit, lean, yank, climb, run into, shake, hide gum, unplug cables, plug in phones, attempt to break, hack, etc.

Consider that many of our visitors have accessibility needs. Our exhibitions are required to be DDA compliant, but we want to exceed that. Choose and design technology that allows access by people with the widest range of needs.

Also consider that our exhibitions generally contain a great deal of technology, all of which generates heat which needs ventilating away in order to protect the technology and fragile objects, and to keep visitors comfortable on hot days.

While we deploy staff to be generally available in galleries, in general we do not want to deploy staff or volunteers to invigilate specific installations or to train visitors to use specific pieces of technology. Therefore, each technology installation needs to, as much as possible, instruct visitors in its own proper use.

We want to be able to remotely monitor the status of our technology, for troubleshooting and analytics purposes.

When we close (at varying hours), we want this technology to turn off automatically so as to prolong life and reduce electricity and cooling costs.

As if that wasn’t enough, ACMI is situated next to a major train station, which generates large amounts of EMF as trains pass. For that reason, we need to avoid signals that are susceptible to that level of electromagnetic interference.

### General responsibilities

Unless otherwise specified in requirements documentation, suppliers of exhibition technology systems are expected to:

* Provide a plan and program of works
* Carry out design of the system, including production of prototypes and user testing
* Supply, deliver, install, configure and demonstrate all hardware, software and cabling necessary to operate, maintain and modify the fully working system
* Integrate the system into specified furniture/joinery
* Integrate the system into ACMI’s lighting, audio, AV control (Nodel, usually) and network infrastructure
* Train staff in the use of the system
* Support and warrant the system
* Project management and stakeholder liaison for the above

### Navigating the requirements

The exact requirements that are needed for each installation typically depend on user interface, technical complexity and networking needs. The following sections should be read after assessing the installation in question, as not all measures will be needed for some installations.

All technology suppliers should read the sections on [Delivery, Documentation and Support](https://github.com/ACMILabs/tech-standards/wiki/Delivery%2C-Documentation-and-Support), [Hardware](https://github.com/ACMILabs/tech-standards/wiki/Hardware), [Software and content](https://github.com/ACMILabs/tech-standards/wiki/Software-and-content), [Naming Conventions](https://github.com/ACMILabs/tech-standards/wiki/Naming-Conventions) and [Backups and Disaster Recovery](https://github.com/ACMILabs/tech-standards/wiki/Backups-and-disaster-recovery).

The following questions will help to determine which other parts of this document to read in depth. If your answer is _“No”_ to these questions, then ignore the related sections.

* Will computer/s or device/s need to be housed near the work on the gallery floor? If _“Yes”_ then read the [Case and cabinet design](https://github.com/ACMILabs/tech-standards/wiki/Case-and-cabinet-design) section.
* Does the work require network access including for power and show control? If _“Yes”_ then read the [Networking](https://github.com/ACMILabs/tech-standards/wiki/Networking) section.
* Does the user interface require the user to access keyboard or mouse? If _“Yes”_ then read the [User interface such as keyboards, mice, controllers, touch screens, cameras](https://github.com/ACMILabs/tech-standards/wiki/User-interface-such-as-keyboards%2C-mice%2C-controllers%2C-touch-screens%2C-cameras) section.

_You can view the_ [_entire set of standards on Github_](https://github.com/ACMILabs/tech-standards/wiki)_. Again, we would love to see suggestions, forks, remixes, extensions and contributions to this work — particularly to incorporate COVID-safe guidelines!_
