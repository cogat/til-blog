---
title: "Our open-source media player for displaying fleets of video"
author: "Greg Turner"
date: 2020-06-10T01:46:37.771Z
lastmod: 2024-04-07T14:21:09+10:00


subtitle: "We made an exhibition-scale internet-of-things media player, and we’re open-sourcing it so you can use it too."

featured_image: "/posts/our-opensource-media-player-for-displaying-fleets-of-video/images/1.jpeg"


aliases:
    - "/our-open-source-media-player-for-displaying-fleets-of-video-8d518c0c97dc"

---

This is just a quick post to say hello, we made an exhibition-scale internet-of-things media player, and [we’ve open-sourced it](https://github.com/ACMILabs/media-player) so you can use it too.
![image](/posts/our-opensource-media-player-for-displaying-fleets-of-video/images/1.jpeg#layoutTextWidth)
XOS media players playing through various kinds of demo content on various screens as part of our long-term testing — thanks to [sighmon](https://medium.com/u/b3aae533f7e6) for the photo

**Why did we roll our own media player?**

As the world’s most-visited museum of the moving image, ACMI has a lot of, well, moving image to show. We also know that it’s really hard to present the moving image in a way that invites a deeper experience than you might get from simply watching the media there and then in a distracting environment. Some of the challenges we face are:

* Not everyone can see and hear the media clearly. Sometimes because of a disability, but also everyone finds it kinda hard to focus on one video in a gallery brimming with amazing moving image. How might we provide some sensory breathing room?
* Not all of our visitors share the same language. So how do we make other languages available?
* Not everyone has time or willingness to linger on a moving image piece of unknown length or interest. How can we help them decide?
* We don’t have unlimited wall space and sometimes it is useful to put a playlist of several videos on one screen. How can we add interpretive material that updates in sync with the playlist?
* If a visitor wants to learn more about what’s on screen, how can they ‘bookmark’ it for further exploration later?
* Sometimes we want a number of screens to play in exact sync. How can we do this reliably?
* We need hundreds of these things. How do we get value-for money? How do we coordinate management and maintenance?
* We want to micro-curate videos with rapid turnaround. How can we speed up the deployment pipeline?
* We want to send these out on tour without worrying about configuration or network uptime

To address these challenges, we realised we needed a robust network-connected media player, that could take a playlist and content via API, and then play that playlist stably for years and years if need be. At frequent intervals it should publish its playback status so that other nearby technology can respond in realtime.

That’s why we made the [XOS Media Player](https://github.com/acmilabs/media-player). At its core it’s pretty simple — a Python wrapper around VLC that fetches content and reports playback status to a message broker over the network. But it’s designed for scale and robustness and has been running for months on end in our prototype exhibitions. It’s delivered as a Docker image that is designed to be deployed on a fleet of Raspberry Pi 4s and x86 machines (we use [Balena](https://labs.acmi.net.au/working-remotely-with-internet-of-things-hardware-devices-969c53923e1f) to manage our fleet of IoT devices).

We’ve open sourced the code under the [Mozilla Public License](https://www.mozilla.org/en-US/MPL/2.0/), meaning you can use it for free (with attribution)—you need to BYO media API for now, unless you want to become an XOS partner/collaborator.

**How does the XOS media player help us with our challenges?**

With a media player that connects to a network, we can:

* Collect videos onto ACMI’s [Lens](https://www.theage.com.au/culture/movies/acmi-mixes-hi-tech-with-retro-charm-in-40m-renewal-20191128-p53f6k.html), for watching or deeper investigation later. This also allows some needed “sensory breathing room” away from the exhibition context.
* Rapidly deploy and transcode content from a central service.
* Show synchronised content on nearby devices that people can use to discover more about each video.
* Indicate with a separate countdown clock or progress bar how long is remaining on a video.
* Synchronise playback on visitors’ own devices, allowing them to see captions or hear audio in a preferred language.
* Connect several players together to play synchronised video (we’ve achieved sub-1-frame accuracy)

And in future, we want to add:

* Not just video, but HTML views.
* On-screen interactivity — a jukebox, interactive kiosk, language choice, etc.
* Remote playback control.
* Realtime content deployment (rather than fetching on startup).

**Key Features:**

* Downloads a playlist of videos (with optional subtitles) from an API and saves these locally so that playback can take place after reboot without an internet connection
* Plays the downloaded playlist fullscreen in an endless loop through the first HDMI output
* Supports content and captions playable by VLC on the given hardware
* Posts playback &amp; volume information to a broker to allow integration with synchronised systems
* Synchronises playback with additional media players if configured
* Deployable and configurable at scale via Docker and Balena
* Runs on Raspberry Pi 4 and Intel/Dell small-form-factor PCs.
* If no network is available, continue to play the last-downloaded playlist

If this sounds like it would be useful for your organisation, give it a try and let us know how you get on via [GitHub issues](https://github.com/acmilabs/media-player/issues).

_If you do use it, tell us!_ It helps us build a stronger case for the open sourcing of other software we make like 2016’s [open source mobile media guide](https://labs.acmi.net.au/an-open-source-static-museum-audio-guide-4c5cd83dbdcb) which got forked and used by museums and cultural organisations on several continents!
