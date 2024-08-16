---
title: "I trained an A.I. to imagine movie titles from ACMI’s collection"
author: "Greg Turner"
date: 2017-08-31T02:35:18.466Z
lastmod: 2024-04-07T14:21:00+10:00

description: ""

subtitle: "My first few weeks at ACMI have been a whirlwind of discovery, exploration, planning and excitement around its forthcoming renewal. One of…"

featured_image: "/posts/i-trained-an-a.i.-to-imagine-movie-titles-from-acmis-collection/images/1.jpeg"

---

My first few weeks at ACMI have been a whirlwind of discovery, exploration, planning and excitement around its forthcoming renewal. One of my projects is to continue to flesh out explorations of machine learning and related AI techniques to ACMI’s collection of Australian moving image works.

This is not that project.

Or if it is, then it’s more of a fun steam-letting-off part of that project. Drawing from [Dan Hon](https://medium.com/u/a3934ce98c61)’s [experiment in generating British place names](https://medium.com/@hondanhon/i-trained-a-neural-net-to-generate-british-placenames-9460e907e4e9), I trained a Recurrent Neural Network (RNN) on titles from ACMI’s collection, and asked it to generate some more.

![image](/posts/i-trained-an-a.i.-to-imagine-movie-titles-from-acmis-collection/images/1.jpeg#layoutTextWidth)

### Method

I used [Jeff Thompson’s OS X instructions](http://www.jeffreythompson.org/blog/2016/03/25/torch-rnn-mac-install/) to get [torch-rnn](https://github.com/jcjohnson/torch-rnn) running, trained, and predicting new titles on my Mac. A good way to tell you’re working with bleeding-edge tech is that it is painful to install. I didn’t have to do _much_ textfile editing to get it working, and it didn’t break _many_ other things, but next time round I would definitely try the [Docker version](https://github.com/crisbal/docker-torch-rnn) first. The moral is: keep your AIs safely contained!

The next step was to get a list of titles to train the AI with. I grabbed the [Objects file from ACMI’s Collection Data Starter Kit](https://github.com/ACMILabs/collection-data-starterkit/tree/master/dist/json), and wrote a quick Python script to write the titles to a text file. [Here’s the complete list](https://gist.github.com/cogat/96c5ae9c8ddfb91378b6acb2656e6b40), if you’re interested.

Training the titles took an hour or so on my laptop — I didn’t stick around to find out exactly how long. Interestingly, the training process generates ‘checkpoint’ files, which you can use to generate titles based on a less-experienced network before the training has completed. I’ll give some example titles from these checkpoints below.

Once the training had finished, it was a simple matter to generate titles. It’s also possible to provide different ‘Temperature’ values, which change the amount of ‘novelty’ in the system. In the examples below, I explore the effects of more training and less novelty. The results I’ve highlighted are (because I chose them) an improvement on the average quality of results. In the most entertaining scenarios I’ve linked to longer lists of results.

### The effect of more training

These generation commands vary by checkpoint. A higher number means the network is more trained, and the highest number is 17150.
`th sample.lua -checkpoint cv/acmititles_**1000**.t7`

_This is pretty rudimentary —nearly ‘lorem ipsum’-ish, but clearly better than random characters, and I give it extra points for inventing “Australiation”. It has also adopted ACMI’s protocols for marking Captions and DVDs in titles. I like that it seems to generate nonsense that evokes a particular language — English, German, French, Latin. (N.B. ACMI uses ‘=’ to indicate translated titles. The transformation of ‘No.’ to ‘№’ is Medium’s.)_

* Dishorl (Coption. Volucu (Captioned)
* Brainou dinawawd Spiture conzer
* Fing, calle the well
* France Fogral 2000 = Cray
* The River sufits
* Taby’s wildisifs Issoder wald. №1. [Inpact. — 0t = Clactione (A)
* Mamson of the Cames Afrerzand of three pirm ant mathation of the A Blad york &amp; ukou [DVD]
* Eye
* Australiation en
* Cellle que dreacuat: the Truciona Schore [CVCA)
* Chaples of the sundy
* Stucter the Zittrest
* Ut lenzunes Zreal stire touran
* …etc.`th sample.lua -checkpoint cv/acmititles_**5000**.t7`

_Now it’s beginning to look like some thought has gone into it. It may help to imagine some of these being said in an Auld Scots dialect:_

* Black Australia
* Play shork
* The tron’s celeve: Christ to Tomorrow
* Frin’ of Guitz dous
* War caries
* dream view
* The Buildren a languard King dill the swain. Come Reader from Bering
* South of Bends
* Kuman wenting: The Poopes with Don at Viglembority
* The Cundrals City
* Fackumo
* Cat Critics: thrawd unges, the changlosia comafrico: sents in actories
* The Alphont
* Oration
* Don’t time (D)
* Lonster = the West of Tave
* Chysids: a ginution in the fould to lugar
* …etc.`th sample.lua -checkpoint cv/acmititles_**10000**.t7`

_This model seems to have more sustained moments of being on the verge of making sense. I think the_ `_temperature_` _value may still be too high to be interesting — too much randomness can be as uninspiring as none._

* The Craining
* Gromastard of Apprets (Captione)
* Beach Germany
* Dogged with Fine. [№381
* Mirror of Fire to gavey by Histry Vasie Miroh valuley [B&amp;W]
* The Tenny is is early white of marming [DVD]
* Sky people
* Wonderland Tada: fight of Glater sabute vitoriom
* Muse and people and experiel: project of the babi
* The Quoubed film!
* Les Fluik Steagh: Prenstactic Rives for shong upon lifes
* The New de city. Part 1. Spedite Nortan vook
* Mumbler sama
* …etc. [More results here](https://gist.github.com/cogat/5924b247154283a4e50f92722557eed1).`th sample.lua -checkpoint cv/acmititles_**17150**.t7`

_This is the final model, after the training has finished. It’s pretty inventive — if only we knew what all those new words meant. I call this “young adult scifi novel mode”._

* Making ackerous
* The Zookboy
* Sound of a parens
* The Vision Island
* The Nemplatage by speeng: a sea Ennital’s sense [Dabb)
* Sourtelf asimation
* Space ourth
* Bangosia story in Australian eterness
* Modern princes, the labon and lace
* Zive and the didgent
* Reductional priving’s Anumie
* The Metrectival descreecces voice = monkey: Episodes
* …etc. The [full list is here](https://gist.github.com/cogat/66e1a9374b0f172d89244553d18617c1).

### The effect of novelty

Remember, this neural network has no knowledge of English words, grammar or punctuation. It has only ever been shown these titles, not any other text, and we haven’t told it that these are necessarily titles, or even words.

Given how little we have told this AI about what it’s supposed to do (just ‘make more of this sort of thing’), it’s doing an admirable job. It’s also being quite brave about taking things in new directions. Perhaps a little _too_ brave.

Luckily there’s a `temperature` control, that allows us to cool down the novelty (and maybe to dial back any sentience that occurs). The default `temperature` value is 1.0, i.e.most novel, which is what we’ve used until now. Dialling the `temperature` back will result in more words and word patterns that are already found in the training list. Check it out:
`th sample.lua -checkpoint cv/acmititles_17150.t7 **-temperature 0.2**`

_Very low novelty — the patterns used are the most common ones in the collection. We have lots of ‘stories of’ works, it seems._

* The Children of the school (TEFC)
* The Community and the story
* The Little the world of the story
* The Beginning the school (TEFC)
* The Sea and the search of the sea
* The Story of the story
* The Story of the search of the search of the search of the search of the world
* The Story of the story
* …etc.`th sample.lua -checkpoint cv/acmititles_17150.t7 **-temperature 0.5**`

_Adding more novelty. In these results, most words are recognisably English and it is easier to select titles that are grammatically correct. I call this “bad concept album titles mode”. We’re close to being intriguingly novel, but the word patterns are a bit too repetitive (“The x in/of/and/to the y”) to be intriguing for long._

* The Life of the office
* The Plant community
* Breaking the earth = The Great growth [DVD]
* The Body in the clother sea = The Story of the electronical resease
* Parning the resigners of the Seven (Captioned)
* The Conside of the Beat
* The Australian diary. №097 = Deutschland Spiegel
* The Design to the commander
* The Art in the lung
* The Demonstre
* The Children of the monder and the discoveries
* Music panstraction
* The Master of the Flemination
* The Machination and peace for the spirit of the communication
* The Strance panorama. [№70/12]
* … etc. [Here are 359 more](https://gist.github.com/cogat/9640927c81298e7fd7d04353bf63a812).`th sample.lua -checkpoint cv/acmititles_17150.t7 **-temperature 0.6**`

_‘Undergraduate artist mode’. At this point, changing_ `_temperature_` _is a tradeoff between wanting perhaps_ **_more_** _novel word_ **_patterns_**_, but_ **_fewer_** _novel_ **_words_**_. If we were doing this seriously, we’d perhaps choose a model that knows more about (Australian) English._

* A Compilation of the poses
* The Mazures of Survival (K)
* Cities of the Grand Pictures of the father = The Allial change
* The Cup Anternation
* The Rose in the world
* New parts of the cat
* Challenge de Billy
* How the sheep bun
* Getters of the story
* Fattle to three smars
* Bean story
* Saga: the killer at you and the learning
* The Water in industrial program
* The History of Heart
* The Words of the babber South
* Faminations 1990 &amp; 2
* A New life in the red show
* Angel of the wind
* Making out
* The Interview of the self and compile
* Blood moves
* Mirror of Australia
* … etc. [Here are 374 more](https://gist.github.com/cogat/12d0b9a4749021bbcd4f4443752831b7).

That’s about all. I’ll be exploring these concepts further in my new album, _The Conside of the Beat,_ available in absolutely no good record stores.
