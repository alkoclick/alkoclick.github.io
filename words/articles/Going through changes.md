The title reference to a song that Spotify keeps recommending to me

[[2021-12-21]]

---

### Going through changes

After 1.5 years at Zivver, I’ve decided to make the move to [VanMoof](https://vanmoof.com/), an e-bike company. If you’d like to find out how my interview process was like, I wrote about it in an article:

[**How I overthought every step of my interview process with VanMoof**  
_Every so often, we software engineers find ourselves looking for a new challenge. This was me, back in October 2021 …_alkoclick.medium.com](https://alkoclick.medium.com/how-i-overthought-every-step-of-my-interview-process-with-vanmoof-f527f386ff41 "https://alkoclick.medium.com/how-i-overthought-every-step-of-my-interview-process-with-vanmoof-f527f386ff41")[](https://alkoclick.medium.com/how-i-overthought-every-step-of-my-interview-process-with-vanmoof-f527f386ff41)

One of the most correct decisions I made was to leave not 2, but 6 weeks in between ending my position at Zivver and starting the next at VanMoof. I wanted [enough time to feel bored](https://www.youtube.com/watch?v=c73Q8oQmwzo), since that can [get your creativity juices flowing](https://www.youtube.com/watch?v=LKPwKFigF8U). But I also appreciated the generous rest at the end of what has been a couple of heavy pandemic years.

![](https://cdn-images-1.medium.com/max/800/0*nDQdfjBruO3WZbVz)

“Person sitting on bench” Photo by [Sid Leigh](https://unsplash.com/@sidbobs?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

Little did I know that thanks to that, I avoided being on-call during what has been called “one of the worst cyber security incidents of the decade”. Log4Shell is an exploit on log4j2, one of the most commonly used Java loggers. It functions in 2 parts: the first one is the fact that log4j2 can do arbitrary lookups to fetch classfiles or other data and the second is a specially crafted message that you input… anywhere it may get logged, such as search fields, URLs, anywhere. Minecraft was very heavily affected by these attacks. The whole story is further complicated by the fact that log4j2 is maintained just by 4 volunteers on their spare time, despite being used to power multiple billion-dollar corporations. Here’s a [more complete writeup](https://bgr.com/tech/internet-is-scrambling-to-fix-log4shell-the-worst-hack-in-history/)… and here’s the xkcd about it:

![“Now, turns out this is turing complete” says a character to another. The tag reads “This phrase means someone spent 6 months getting a dishwasher to play Mario cart, or you’re under attack by a nation state”](https://cdn-images-1.medium.com/max/800/1*sc1u2OE-PMfK_-J4menJ_A.png)

Here’s an excellent blogpost about [the state of open-source maintenance and paths forward](https://blog.filippo.io/professional-maintainers/).

And here are more memes about Log4j

[**log4j memes**  
_log4j memes dot com. If you don't know whether to laugh or cry. Curated by Intruder._log4jmemes.com](https://log4jmemes.com/ "https://log4jmemes.com/")[](https://log4jmemes.com/)

Okay, let’s switch topics. Ever had a great idea shot down by someone you respect? How about by multiple people, in public, by folks who are supposed to know their stuff? Here’s [Dropbox getting completely shot down on its HackerNews debut](https://news.ycombinator.com/item?id=8863), back in 2007.

When you see Chomsky’s name get brought up, you know shit’s about to get real. Do you know about the linguistics wars? Universal grammar? Feel free to look it up, it’s truly a fascinating topic with incredible depth and honestly the most fun linguists have been at parties in the last… forever years. But how is that related to computing? **Well, apparently learning computer languages is easier if you are good at learning languages, than it is if you are good at math or logic.** And there’s a journal article on it.

[**Relating Natural Language Aptitude to Individual Differences in Learning Programming Languages …**  
_This experiment employed an individual differences approach to test the hypothesis that learning modern programming…_www.nature.com](https://www.nature.com/articles/s41598-020-60661-8 "https://www.nature.com/articles/s41598-020-60661-8")[](https://www.nature.com/articles/s41598-020-60661-8)

Now that we’re at the topic of fascinating new knowledge, take a look at “[Abusing AWS to make a search engine](https://boyter.org/posts/abusing-aws-to-make-a-search-engine/)”. It delves into the guts of setting up a practical search engine, as well as taking things down to the absolute fundamentals. Turns out you can set up a completely serverless search engine that runs completely on demand on AWS Lambda? For me, it felt like a natural continuation of the “[Using Route53 (AWS DNS service) as a database)](https://www.lastweekinaws.com/blog/route-53-amazons-premier-database/)” though experiment, just more practical.

Okay, we’re still on the awesome-train, let’s keep going. You heard of Github CoPilot, an AI powered system for code completion, but here’s GPT-3 producing shell commands that are largely ready to execute from natural language input! Maybe we can finally have AI figure out the argument to untar a file 😅

More awesome! The EU parliament [blocks mass biometrics surveillance](https://www.yahoo.com/now/european-parliament-backs-ban-remote-111017178.html) across its member states.

And now that we’re in the domain of legal trouble, here’s a play-by-play commentary of the “Parler vs AWS” trial by the awesome Corey Quinn. It’s far more interesting than you expect it to be, mainly because of Corey’s humor.

If you’re into WiFi security, here’s a nice walkthrough and demonstration of some new vulnerabilities in the WEP and WPA (not to be confused with [WAP](https://www.youtube.com/watch?v=hsm4poTWjMs)). [Full article here](https://www.fragattacks.com/).

For your daily dose of dystopian tech, but at least with a sarcastic twist, here’s [an implementation of squid game](https://twitter.com/devdevcharlie/status/1457544591540830209) which you can play at home (no embed to avoid spoilers).

Since we brought up dystopia…

### About Facebook

Dear reader, this feels repetitive right? How can this article series have new content about how messed up FB is, in every issue? Trust me, it’s something that’s on my mind too. I genuinely don’t set out to search for cheap shots at them. I don’t wake up in the morning thinking “hmmm, how’s that company doing, what dirt do we have on them today?”. I even like several of the folks who work in software development at Facebook (well, Meta now).

So, Facebook renamed to Meta. I watched the presentation with morbid curiosity, just waiting for the moment when James Bond would break in and take down the Zucc on live feed. Didn’t quite happen, but after the line “If you die in Metaverse you die in real life” maybe this is a horror movie, not an action one. Vice news brought out the best title: “[Zuckeberg announces new world where Facebook is not a horrible company](https://www.vice.com/en/article/qjb485/zuckerberg-facebook-new-name-meta-metaverse-presentation)”. My personal favorite was the Iceland (yes, the country) parody tweet.

Facebook was fairly careful to show no actual product footage, only “artist visualizations” of what the metaverse will be like, commonly known as “trust me bro”. But hey, fear not, we already know there’s sexual harassment.

[**The metaverse has a groping problem already**  
_Skip to Content A woman was sexually harassed on Meta's VR social media platform. She's not the first-and won't be the…_www.technologyreview.com](https://www.technologyreview.com/2021/12/16/1042516/the-metaverse-has-a-groping-problem/ "https://www.technologyreview.com/2021/12/16/1042516/the-metaverse-has-a-groping-problem/")[](https://www.technologyreview.com/2021/12/16/1042516/the-metaverse-has-a-groping-problem/)

While “Meta” is too busy reinventing what the rest of us have been calling “Second Life” or “WoW” since 2001, but with VR and NFTs, some others have chosen to focus on minor concerns about questionable decisions, e.g the fact that Facebook opted to arbitrarily prioritize reacted content five times over simple likes, which led to a simple predictable outcome: Outrage spent five times faster:

Even that however is not as horrible as one of their shittiest moves to date: [**Knowing since 2019 that Instagram causes a significant percentage of people body image issues**](http://theguardian.com/technology/2021/sep/14/facebook-aware-instagram-harmful-effect-teenage-girls-leak-reveals)**, knowing that there are solutions and choosing to do nothing about it.** They did not share this research with the world. They chose to take 0 of the more than 30 actions that their own researchers suggested. Because… “the algorithm”. How do you live with yourself knowing the 13% of teenagers with suicidal thoughts trace them back to your fucking mobile app?

Oh and they had a [secret deal with Google](https://nymag.com/intelligencer/2021/10/inside-jedi-blue-facebooks-secret-deal-with-google.html) to unfairly buy ads with different conditions than all the competition, hide it from all anti-monopoly regulators, and deny it in court when it got there.

And let’s not talk about how Facebook’s own ad targeting allows companies like Exxon to [send the exact opposite message to different sides of the political spectrum](https://themarkup.org/news/2021/04/13/how-facebooks-ad-system-lets-companies-talk-out-of-both-sides-of-their-mouths) thanks to ultra-specific ad targeting. As a reminder, whenever different bodies such as [the Mozilla foundation](https://www.theverge.com/2021/8/5/22610898/facebook-bans-ad-privacy-misinformation-researchers-critics-warner-mozilla-klobuchar) or [Signal attempt to show Facebook users just how well Facebook can target them](https://slate.com/technology/2021/05/facebook-signal-ad-data-privacy.html), they either get banned from the platform or reported as violating the Code of Conduct.

The most positive thing I have to share about Facebook is that its red team folks are doing some pretty good cutting-edge work [when trying to ban porn](https://www.wired.com/story/facebooks-red-team-hacks-ai-programs/) from its platforms? Is that a good piece of news overall? I struggle to decide. Maybe they were just trying to get it to [stop blocking images one of the holiest sites of Islam as related to terrorism](https://www.buzzfeednews.com/amphtml/ryanmac/instagram-facebook-censored-al-aqsa-mosque)?

### On security

Yeah WiFi isn’t the only vulnerable thing I’m afraid. In fact, GPRS, the main standard for data over cellular networks for decades, seems to have a deliberate backdoor included in its design.

Of course, bad actors such as the [NSA adding backdoors into well-known and widely used encryption algorithms](https://www.theverge.com/2013/12/20/5231006/nsa-paid-10-million-for-a-back-door-into-rsa-encryption-according-to) is nothing new.

You know what is fairly new? Reverse engineering machine learning algorithms such as GPT2 to extract their raw data. I am not an expert in the field, but in my previous experience, the standard assumption was that training data used in a well-developed algorithm would either remain private or be fairly hard to extract. During my time at [Zivver](https://www.zivver.com/) I was first exposed to how you can account for anonymizing source data in your algorithmic design to protect privacy — hats off to them for being ahead of the curve on that one.

But hey, bigger hats off to the folks behind the recent explosion of anti-work manifestos plaguing receipt printers, I can honestly hardly imagine a more 2021 piece of news.

[**Hackers Are Spamming Businesses' Receipt Printers With 'Antiwork' Manifestos**  
_Hacking. Disinformation. Surveillance. CYBER is Motherboard's podcast and reporting on the dark underbelly of the…_www.vice.com](https://www.vice.com/en/article/qjbb9d/hackers-are-spamming-businesses-receipt-printers-with-antiwork-manifestos "https://www.vice.com/en/article/qjbb9d/hackers-are-spamming-businesses-receipt-printers-with-antiwork-manifestos")[](https://www.vice.com/en/article/qjbb9d/hackers-are-spamming-businesses-receipt-printers-with-antiwork-manifestos)

Or can I?

### On dickpics

As part of my “going completely unhinged due to plenty of time off” routine, I wrote about dickpics on Github recently:

### I can get no (education)

Not sure what to do in the holidays? Well, spend time with your loved ones. Got too much time still? Here’s some quick (15–60 minute) educational resources to get you up to speed with various fairly fundamental concepts across different sectors of software development:

[Common Vulnerability Scoring System](https://learning.first.org/courses/course-v1:FIRST+CVSSv3.1+2020/about)

[DNS (it’s always DNS)](https://www.cloudflare.com/learning/dns/what-is-dns/)

[Basic routing and lookup commands](https://academy.ripe.net/enrol/index.php?id=11)

[Kafka, but with cute beavers](http://www.gentlydownthe.stream/)

### Closing remarks

Last time I chose to close with a song from a movie. In honor of Matrix 4 being released this week I was considering choosing “White Rabbit” by Jefferson Airplane for this article, but instead I think I’ll go with Regina Spektor:

<iframe width="560" height="315" src="https://www.youtube-nocookie.com/embed/1eiXAUAe4GA" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

That’s all from me this (week/month/year) folks. I’ll probably see y’all again in 2022. Enjoy your holidays, if you have any!