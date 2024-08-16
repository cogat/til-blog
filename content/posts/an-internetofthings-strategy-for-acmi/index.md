---
title: "An Internet-of-things strategy for ACMI"
author: "Greg Turner"
date: 2020-06-23T04:46:18.393Z
lastmod: 2024-04-07T14:21:13+10:00

description: ""

subtitle: "One of the guiding principles of the renewed ACMI is “curation by humans, enabled by technology”. Here’s how we make that happen."

featured_image: "/posts/an-internetofthings-strategy-for-acmi/images/9.jpeg"

---

![image](/posts/an-internetofthings-strategy-for-acmi/images/1.jpeg#layoutTextWidth)
Artist’s impression of technology doing its thing in our new exhibition

As Lead Engineer and project CTO, I have headed up the multi-year technology design and implementation for ACMI’s $40m [Re/newal](https://www.renew.acmi.net.au/). One of the guiding principles of the renewed ACMI is “curation by humans, enabled by technology” (sigh, I guess my top secret _curate-o-bot_ AI can wait for another day). We wanted to build a system that curators can use to choose and rapidly deploy playlists of content around ACMI’s galleries, whether the media comes from ACMI’s Collection, edit suite, special exhibition videos or elsewhere.

With Second Story and Swinburne’s Centre for Design Innovation, we also created the Lens, a hybrid physical/digital device and service, which lets visitors dive deeper, discover new favourites and inspire curiosity beyond the museum experience. We’ll have way more to say about video and the Lens in future posts, but for now I wanted to talk about the philosophical approach we have taken at ACMI to choosing, managing and deploying custom Internet-of-Things devices. I’ve tried to summarise our journey and the reasons behind our technology decisions, in the hope that there may be useful insights for other institutions on similar journeys.

In our new exhibition, which is designed to run for 10 years, we need 350 or so computers that carry out related jobs — playing videos, displaying labels, and interacting with visitors’ Lenses. These all have displays, projectors, speakers and sensors attached — somewhere north of 800–1000 ‘smart’ devices in all, depending on how you count them. As you might imagine, it’s quite a technology challenge to synchronise content and custom behaviour across these devices, whilst also making sure they start up happily in the morning, run smoothly throughout the day 364 days per year, and shut down safely each night when they’re supposed to.

If these devices weren’t centrally managed, monitored and controlled, then our technical services team would spend all day racing round doing those jobs manually. And if even 1% of these devices fail over any given period, then that’s 8–10 devices to isolate and troubleshoot out of 800–1000. And can you imagine deploying software updates by hand in the middle of a public exhibition?

**What did you do up until now?**

When I arrived at ACMI in 2017 as the Renewal project’s Chief Technology Officer, we were in the habit of using hand-deployed ruggedised hardware like [BrightSigns](https://www.brightsign.biz/) for simplicity, stability and their professional features. Rugged hardware is really good — it is built to take the kinds of enthusiastic (ab)use that an excited group of school kids might throw at it; it has longer mean time between failures and longer service life; it often has remote power control and security features that make it a good fit for public deployment at scale. But the main downsides are price — you pay a lot extra for all that metal — and the proprietary, enterprise-y nature of the feature set. That’s not universally a bad thing, but when you’re creating something new in an agile environment, it can be frustrating to come up against proprietary (or pay-walled) limitations that are less prevalent in an open-source ecosystem. It also has meant that, over time, we end up with a broad variation of devices, as companies continually upgrade their product lines. That makes it difficult to standardise and streamline deployments, which all adds up in design and installation time.

We also tended as much as possible to deploy our player hardware in one of ACMI’s network of comms rooms. This had several advantages: it keeps expensive hardware away from heat, fingers, spilled water bottles, etc, and allows easy access for commissioning, maintenance and troubleshooting. The main disadvantages were that we needed to spend a _lot_ on display and USB signal boosters to bring the signals out to the exhibition floor, and that troubleshooting and maintenance requires a lot of walking between exhibition floor and comms room. And for bonus fun times, ACMI is built right on top of a major railway hub— the electromagnetic interference coming from passing trains can be strong enough to knock out long signal runs, unless we convert those signals into an optical format.

**What are the technology opportunities in ACMI’s Re/newal?**

The first, biggest opportunity, was to create a smart network of devices that would elevate the new ACMI visitor experience. We wanted to improve the accessibility of the moving image, amplify visitor engagement, integrate with online, and also use technology to solve some of the physical and logistical challenges that we face as a real-world museum. We couldn’t find a system on the market that did everything (or even half) of what we aspired to do, and the outcome of this opportunity was important to us, so we knew we had to develop a new suite of products. At the centre of this new suite is XOS, ACMI’s eXperience Operating System, that coordinates much of the standardised moving image content and user interactions across the museum.

It seemed to the team that we could reduce our reliance (and therefore expenditure) on a wide variety of rugged, centralised industrial products if we had better monitoring and control across a smaller variety of less-rugged, more flexible devices. In other words, if a ruggedised video player costs $500+ and fails zero times, but a standardised single-board computer costs $100 and fails twice, then, for ACMI, it’s a better deal — ultimately reaching well into a six-figures saving over our entire deployment footprint. (It needs to be said that these economics only make sense if you have a qualified tech crew on staff, as we do. If we had to risk waiting days for a repair call-out, or had a smaller number of devices then $500 might be the better deal.)

If we could create a smart device that is identical to all other devices, but gets its configuration and content from a central service, then that means that time spent in commissioning and repairs should also drop. Rather than commission every new device by hand, content and configuration across the board can be managed from XOS, based on a predetermined device name. And rather than manually troubleshoot faulty devices on the floor, it becomes quicker to yank the device and plug in one of a number of identical replacement devices, and to expect the replacement to pick up where the faulty one left off.
![image](/posts/an-internetofthings-strategy-for-acmi/images/2.jpeg#layoutTextWidth)
Lens Reader assemblies ready to be deployed. These are all identical except for name, and so can be easily swapped out in the event of failure.

**Why wouldn’t you just use some commercial video player hardware or software?**

The exact reasons are subtle and it’s too early to share all the details, but you will probably get the idea if I say that video in the context of a public museum has different measures of success, and standard video player hardware and software — and much traditional video in a museum — isn’t created with these successes in mind.

People bring different contexts to a museum: their ages, tastes, language and access needs, and time budgets all differ. It’s impossible for one video screen to meet more than a privileged subset of these needs, and so we need to look for ways to augment what is happening on screen with deeper digital and non-digital experiences elsewhere and elsewhen. We’re launching the first round of these experiences around our re/opening, and having a video player that talks and responds to the network unlocks massive ongoing potential for augmented video experiences.

Also, we didn’t re-invent video-playing — our software uses [VLC](https://www.videolan.org/vlc/index.html) under the hood, with a simple Python-based network wrapper (we explored Raspberry Pi’s standard _omxplayer_ but it was too bare-bones feature-wise and didn’t run on x86 architecture)

We pondered using an off-the-shelf video looper (such as [Lūpa](https://lupaplayer.com/), which is a single-purpose Raspberry Pi that runs proprietary software). Unfortunately we couldn’t modify these products to add the features we needed in a way that was easier than building our own.

**What hardware options did you have?**

We needed to adopt a standard hardware footprint that was:

1. commoditised open standard (so we could customise, and so that single-supplier risk was reduced over a 10-year span)
2. low-cost but serviceable quality (shifting investment from ruggedness to monitoring and flexibility)
3. low in variety (to economise on scale, software development time, and to minimise spares, maintenance and training barriers)
4. small form factor, for deployment on the exhibition floor rather than in comms rooms
5. minimum of moving parts (dust is a thing, noise is a thing)
6. widely available in Australia (waiting weeks for replacements is not an option)
7. ethernet-enabled, and ideally power-over-ethernet ready (too much happening to rely on Wifi)

In short, we tried a lot of experiments, and landed on a combination of official Raspberry Pi 4s and Dell Optiplex Micros. We use the Raspberry Pis for basic tasks like 1080p video, Lens interaction and simple displays, and the Dells when we need more oomph, like for 4k, multi-screen synced playback and low-latency interaction. In all, we’ve purchased about 300 Raspberry Pis and 50 Dell Micros. We enhanced the Raspberry Pis with power-over-ethernet boards and temperature sensors to improve reliability and to simplify installation.

![image](/posts/an-internetofthings-strategy-for-acmi/images/3.jpeg#layoutTextWidth)
Some Raspberry Pis

![image](/posts/an-internetofthings-strategy-for-acmi/images/4.jpeg#layoutTextWidth)
And some more

Before settling on Pis and Dells, we trialed using BrightScript to have our existing Brightsign media players share information about their status, so that other systems could respond. This _just about_ worked, but turned out to be a bit hacky, very difficult to deploy and maintain at scale (without at least subscribing to BrightSign’s commercial fleet management tool) and would have meant huge dependency on BrightSign’s ecosystem. Whilst we could have improved the situation, ACMI really wanted to invest elsewhere and not put all our eggs in someone else’s basket.

Alongside Brightsigns, we started looking at small form-factor PCs. When we started the project, Raspberry Pi 4s hadn’t been released, so we prototyped with Raspberry Pi 3s. These would play 1080p video, integrate with XOS and the Lens hardware well enough, and we were all set to use them if the new Pi 4s hadn’t been reliable enough. Happily the Pi 4s do meet our reliability standards and so we are deploying them across the board.

The Pi 4s did struggle with some of our more demanding cases — 4k video, multi-device synchronised playback, animated interactives and in-browser video, which we use for some of our labels. For these, we needed something a bit more hefty. We initially tried some Intel NUC small-form-factor PCs. These worked great for the more demanding cases, and have been well-proven by our colleagues at Museum Victoria/Melbourne Museum. We could happily have used IntelNUCs or Dells, and in the end opted for Dells for technology-adjacent advantages.

(We briefly considered other hardware approaches: specialised, higher-powered single-board computers, like NVidia Jetsons, and industrial small form factor PCs — however, none of these pass the “can we envisage cheaply being able to replace these for 10 years?” test as well as the standard models did).

**But aren’t Raspberry Pis unreliable?**

No-one expects a Raspberry Pi to last as long as a ruggedised device like a BrightSign, but if they’re [reliable enough to go into space](https://www.raspberrypi.org/blog/raspberry-pi-in-space/), they should be more than reliable enough for our needs. As outlined earlier, the cost-benefit of a couple of replacements over the lifespan of an exhibition works well in our favour.

Our prior experience tells us that the least reliable part of a Raspberry Pi hardware deployment is the SD card. If a Pi has a power crash while the SD card is in use then the lifespan of the card is quickly reduced. We minimised that risk by:

* avoiding SD card use in software where possible (certainly with no irreplaceable data stored there),
* planning to safely shut down before scheduled power-off,
* choosing industrial-quality SD cards,
* continuous monitoring (using [Prometheus](https://prometheus.io/) and [Grafana](https://grafana.com/)) to ensure everything is behaving as it should.

However, we also wanted to remove any lingering doubts. As other areas of ACMI’s renewal project continued to develop, we had the luxury of time to conduct a long-term test (now even more long-term due to COVID-19). We deployed a full bank of Pis and Dells on our Demo desk playing every variation of media and other tasks 24/7 for several months. While we did get some initial crashes, they were all to do with software issues, which we had plenty of time to iron out.

Our further concern is how Raspberry Pis perform when deployed in the field, compared with our demo desk. Most of all we anticipate additional heat challenges, as Pis have no active cooling by default, [reported issues with heat](https://www.theregister.co.uk/2019/07/22/raspberry_pi_4_too_hot_to_handle/), and they are going to be deployed in close quarters with other heat-generating equipment. To mitigate this, we have a couple of approaches: their enclosures will all have passive and active ventilation where needed, but most interestingly, we are attaching an external temperature and humidity sensor to every Pi. This helps us monitor the ambient temperature around each Pi, but also gives us a way of deploying cheap, high-quality smart temperature sensors around the museum which, as every conservator knows, is important to monitor to help safeguard fragile objects on display. The temperature data, alongside all the other data, is sent to Prometheus for visualisation in a Grafana dashboard.
![image](/posts/an-internetofthings-strategy-for-acmi/images/5.png#layoutTextWidth)
Grafana dashboard for a media player

**What about Internet-of-displays-and-projectors? Audio?**

We are absolutely still going for rugged and industrial displays and projectors. We can’t hide them away for protection, we don’t want to spend hours each day manually turning them on and off or wondering if they’re working, and we want them to look fantastic for as long as possible. Plus we don’t need to innovate on display hardware as much as we do with playback and interaction devices. So for these reasons we’re very pleased to be partnering with Panasonic, who make the professional 24/7-rated [displays and projectors](https://business.panasonic.com.au/visual-system/products-and-accessories/professional-displays-range) that made the Tea Party in our Alice exhibition look so amazing.

For audio, we are going networked by streaming most of our audio over a Dante network for mixing and balancing. This is mainly to allow us holistic control over sound to avoid the cacophony that unbalanced audio can produce, but also allows us to integrate the audio into responsive soundscapes, and down the track to respond better to different audience needs.

**How do you manage configuration of a fleet of 300+ devices and media?**

We use a system called [Balena](https://www.balena.io/) to manage the entire fleet of standardised devices. Balena takes care of the process of securely deploying software to fleets of internet-of-things devices, and essential remote monitoring and control of each device. To set up, we install a custom flavour of Linux on each device, which then contacts Balena to be issued its individual name and configuration. When we want to deploy changes to our software, we push it up to BalenaCloud, which seamlessly and safely rolls it out to each applicable device, using a blue/green-style deployment.

![image](/posts/an-internetofthings-strategy-for-acmi/images/6.jpeg#layoutTextWidth)
Industrial SD cards waiting to have software installed

![image](/posts/an-internetofthings-strategy-for-acmi/images/7.jpeg#layoutTextWidth)
Our homebrew SD card duplicator in action

Using Balena allows us to ignore individual differences between devices; we install identical software on every device, with all of the configuration managed by Balena. XOS then only needs to communicate with BalenaCloud via its API to roll out content and configuration to each device. This massively streamlines development and deployment — a one-time install process consists mainly of burning identical install images to SD cards and allocating a name for each device; from there we can sidestep manual per-device configuration or upgrades for the entire life of the device.

While there’s a risk in relying on any 3rd-party service for a 10-year lifespan, we’re comforted by the knowledge that, should anything untoward happen to the BalenaCloud service, we can run our own OpenBalena service if need be.

If you’re interested in reading more about our team’s experiences with Balena, take a look at this this [detailed post from Benjamin](https://labs.acmi.net.au/working-remotely-with-internet-of-things-hardware-devices-969c53923e1f).

![image](/posts/an-internetofthings-strategy-for-acmi/images/8.jpeg#layoutTextWidth)
Four Dells (stacked two high) having Balena installed onto them.

Although Balena can take care of devices running BalenaOS, we need a more general system to take care of monitoring and control of all hardware across the building. For this, we are using an open-source platform called [Nodel](http://nodel.io/), which originated with our friends at Museums Victoria. The Nodel ecosystem has extensible recipes for all our displays and projectors, and provides a powerful central control and dashboard that allows us to start up and shut down the entire exhibition with a single tap, or in response to scheduled calendar events. Happily, our expert tech integrators [Lumicom](https://lumicom.com.au/) are Nodel experts, and are setting it up for us, as well as installing our Internet-of-Things devices and other hardware.
![image](/posts/an-internetofthings-strategy-for-acmi/images/9.jpeg#layoutTextWidth)
Peek under the hood of a nearly-assembled Raspberry-Pi-based Lens Reader. Hardware nerds, speculate away!

**What about custom interactives?**

We have a lot of video to play and need a lot of identically-behaving Lens readers and digital labels, but we always knew that one or two choices of standard hardware wouldn’t serve every need we would face. For example, often a complex artwork will be delivered with the specific hardware and software it must use, and in those cases we have to deploy the work exactly as it comes. That’s fine in the name of art, and we’ve long been geared up for those particular challenges, but it’s not an approach that can scale.

Instead, our strategy is to standardise 90% of ACMI’s deployment cases and handle the remaining 10% on a case-by-case basis. Currently we’re on track to exceed that, taking on more use cases as it becomes increasingly cost-effective. Now in the new exhibition, only about 15 AV installations don’t run on our standardised Raspberry Pis and Dells, due to their advanced or one-off needs. However, we’ve been surprised at how many of these custom installations can actually leverage some part of the XOS infrastructure. To take one example, we’ve commissioned an interactive that takes apart a video frame by frame in response to user input. That frame-by-frame interaction isn’t a feature of our standard software, but the interactive can still use XOS to fetch the source video it needs, rather than us needing to manage content in a separate pipeline. Another major art commission incorporates more than 50(!) of our standard video players which massively simplifies installation and spares management.

**Will you be open-sourcing your Internet-of-Things software?**

Yep! ACMI [recently announced](https://labs.acmi.net.au/our-open-source-media-player-for-displaying-fleets-of-video-8d518c0c97dc?source=collection_home---2------0-----------------------) the open-sourcing of our [RaspberryPi/x86-based Media Player](https://github.com/acmilabs/media-player) under an MPL license. We’re announcing the next few projects very soon — follow us on [Twitter](https://twitter.com/acmilabs) or [Medium](https://labs.acmi.net.au/) to be the first to hear.

**Where could this go in the future?**

We’re really excited to see how this strategy plays out in real-world conditions with real public once we open our new building. We’re also keen to share this technology with other institutions so we can benefit together. No doubt we’ll learn a lot and uncover opportunities to make further technology shifts. In particular, we might want to standardise more kinds of media and experience over time, ranging from HTML-based signage that responds to realtime data, to more advanced media such as mixed reality or real-time interactive streaming.

We also have an opportunity to deepen the network integration — more interoperation between screens and visitor devices, perhaps even generative or personalised content (a tricky thing to pull off in a multi-visitor context).

Much longer-term, using standard approaches should simplify the often-challenging task of preservation of digital artefacts — it would be amazing to develop museum standards that can be adopted as part of a work’s inception, and to extend the technology pipeline to shepherd moving image media from exhibition through to conservation.

_XOS and ACMI’s internet of things ecosystem would be nowhere near as smart and robust as it is without the dedication and inspiration of our amazing team of creative technologists at ACMI:_ [_Ali Haberfield_](https://labs.acmi.net.au/@alihaberfield)_,_ [_Benjamin Laird_](https://labs.acmi.net.au/@benjaminlaird)_,_ [_David Amores_](https://medium.com/@davidamores3)_,_ [_Simon Loffler_](https://labs.acmi.net.au/@simon.loffler) _and Scrum master_ [_Francesco Ramigni_](https://labs.acmi.net.au/@f.ramigni) _(and thanks to Lumicom for the photos of work in progress, and to the entire ICT department for laying down the infrastructure it lives on)._
