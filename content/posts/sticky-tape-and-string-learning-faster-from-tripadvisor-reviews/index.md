---
title: "Sticky tape and string: Learning faster from TripAdvisor reviews"
author: "Greg Turner"
date: 2018-03-07T09:12:49.239Z
lastmod: 2024-04-07T14:21:06+10:00

description: ""

subtitle: "Last week the British Museum wrote about how they were making sense of their TripAdvisor reviews, using natural language processing…"

featured_image: "/posts/sticky-tape-and-string-learning-faster-from-tripadvisor-reviews/images/4.png"



aliases:
    - "/sticky-tape-and-string-learning-faster-from-tripadvisor-reviews-bc6db173d712"

---

Last week the [British Museum wrote](https://medium.com/mcnx-london/invisible-insights-learning-from-trip-advisor-reviews-b5c825fa4409) about how they were making sense of their TripAdvisor reviews, using natural language processing techniques and data visualisation — work they presented at MCNx. It was good-looking (if dense) stuff, which surfaced new insights into what visitors found important about their experience, and pointed towards some root causes. But I couldn’t help thinking that the approach suffered from throwing away the ratings data, and was very resource-intensive— the article concludes with plans for two PhD data science interns and a partnership with the Alan Turing Institute to continue the work. This makes it pretty daunting for other museums to join in the fun.

So, it being a Friday afternoon at ACMI, I decided to see how far I could get with a bit of computational sticky tape and string, in the form of a Python script to scrape our TripAdvisor reviews, and the simplest thing that could possibly work to visualise it. The results are interesting, but ugly and imperfect; in other words, a good start.

We’re also [open-sourcing the code](https://github.com/ACMILabs/tripadvisor-scraper), so that other museums can try it and perhaps contribute to more analysis tools.

The Python script uses `scrapy`, a library for building web scrapers. The scraper is 15 lines of code. The command to run the scraper and send the results to a CSV file is:
`scrapy runspider tripadvisorscraper.py -o reviews.csv`

Which, opened in Excel, gives us:

![image](/posts/sticky-tape-and-string-learning-faster-from-tripadvisor-reviews/images/1.png#layoutTextWidth)
reviews.csv. At this point I feel compelled to note that Arboria wasn’t actually an ACMI event ;)

From there, I pretty much just sorted the data by ‘rating’ in Excel, copied the `title` and `body` cells for each rating block, and pasted each block of text into [https://www.wordclouds.com/](https://www.wordclouds.com/).

Here’s what turned up (ignore the hideous font!):

![image](/posts/sticky-tape-and-string-learning-faster-from-tripadvisor-reviews/images/2.png#layoutTextWidth)
Wordcloud of ACMI’s 5-star ratings.

We can see from the 5-star word-cloud that people overwhelmingly love that we’re free, that they can see things (this is my surprised face). We can see some of our evolving brand values reflected, and also there’s great simplicity in the language. It also seems that people talk about themselves, their lives, and ACMI’s value to them. 59% of our reviews are 5-star.

There’s ambiguity in many of the words — are we good for all ‘ages’, or do people linger for ‘ages’? (this captures both). We could in future get some insight into this by doing the kinds of concept clustering that the British Museum are doing, or by analysing for topics, rather than words.

![image](/posts/sticky-tape-and-string-learning-faster-from-tripadvisor-reviews/images/3.png#layoutTextWidth)
Wordcloud of ACMI’s 4-star ratings

The 4-star words are more varied in nature. People are talking less about themselves and their lives, and more about ACMI’s specific offers, still using a lot of positive adjectives. This represents 32% of our total reviews.

![image](/posts/sticky-tape-and-string-learning-faster-from-tripadvisor-reviews/images/4.png#layoutTextWidth)
Wordcloud of ACMI’s 3-star ratings

The 3-star ratings are where people are ‘meh’ about us. Here the reviews really start talking about what is physically on offer, rather than strong feelings or values. The adjectives still skew positive, but we just didn’t grab them emotionally.

Note that there is a sharp drop-off in quantity between 4- and 3-stars — only 6% of our reviews are 3-star.

![image](/posts/sticky-tape-and-string-learning-faster-from-tripadvisor-reviews/images/5.png#layoutTextWidth)
Wordcloud of ACMI’s 2-star ratings

Less than 2% of our reviews are 2-star, so it’s unwise to draw much in the way of generalisation. Most of the words in this wordcloud are only used once. Here is where the British Museum’s clustering approach comes into its own, to draw together words like ‘crammed’ and ‘squeezed’.

But we should look more closely at specifics: for example, why people are bored — did we miss an opportunity to engage them, or did we accidentally engage them when they’re not our target audience?

![image](/posts/sticky-tape-and-string-learning-faster-from-tripadvisor-reviews/images/6.png#layoutTextWidth)
Wordcloud of ACMI’s 1-star ratings

The 1-star cloud are just here for completeness. We’ve only ever had 6 one-star reviews, all about very different things, so making a wordcloud doesn’t provide insight compared with just reading the reviews. Or maybe we’re ignoring the very real influence of the _David Bowie Is_ exhibition?

Anyway, this was a diverting way to spend an hour on Friday afternoon. Over time it would be good to elevate the level of interpretation to cluster and align feedback.

We’d love to see the code that the British Museum used, but in the interim, if you want to try this yourself, [here’s our code](https://github.com/ACMILabs/tripadvisor-scraper)— feel free to fork and improve it.
