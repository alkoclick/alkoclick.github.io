[[2021-02-22]]

As the endless pandemic drags on, the words of a loving parent come to mind: “Life sucks. And then you die”.

![](https://cdn-images-1.medium.com/max/800/0*A-1XN3x7WxXXaty9)

Photo by [Sarah Ardin](https://unsplash.com/@ardentlysarah?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

My mother is definitely a lot of things, cynical being one of them. But I definitely see the point in some of the philosophy she radiated, whether I misrepresent it here or not — the world at large does not quite care about your plight, but you can and should. Your primary agent and scope of change is yourself, so if you don’t like something in your situation, you’re the main one who can address it. You can usually succeed too! I’m probably extrapolating and rose-tinting it a bit, but hey, gotta try and keep spirits up, amirite?

Can’t complain, as far as pandemic experiences go, writing an article at 23:42 (now 01:32) and listening to Muse is not far from how I’d want to be spending my Sunday night. Whether you’re pouring a coffee or a drink though, you probably wanna pour a good one, cause we’re gonna have a strong session today!

![](https://cdn-images-1.medium.com/max/800/0*wO8i6tayWSbNJUvV)

Photo by [Michael Parulava](https://unsplash.com/@parulava?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

“[Government censors traffic to our website. Workarounds?](https://serverfault.com/questions/1050958/government-censors-https-traffic-to-our-website-workarounds)” As simple as it sounds, a pretty thought provoking question with a lot of standards-based and creative answers. Definitely recommend taking a peek through the plausible solutions — you never know when you may be on the wrong side of your government.

But then in episode 5… the [(Netherlands) government strikes back](https://raidforums.com/Thread-Message-from-the-Netherlands-Police)! Looks like not only did they take down emotet, a pretty major botnet, but they went to brag about it on hacker’s faces. Don’t scroll too far, that shit’s toxic as hell, but do click [on their YouTube link](https://raidforums.com/misc.php?action=safelinks&url=https%3A%2F%2Fyoutu.be%2F24srTBcbslo) because why the fuck not, I’m sorry, this is just too good!

![](https://cdn-images-1.medium.com/max/800/0*2DDN11Bzsn7ckFaT)

Photo by [Mark König](https://unsplash.com/@markkoenig?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

Speaking of hackers and toxic shit, someone hacked the… [water supply](https://twitter.com/Bing_Chris/status/1358873543623274499)? Half funny and half serious — having seen some of the infrastructure holding together public services, that stuff’s not built for security. If someone wanted the average town poisoned, it’s quite doable and that’s concerning. We’ve had this year’s noteworthy Solarwinds breaches, but did you know about the teenager who once found and reported a vulnerability in the website of Los Alamos nuclear facility? He goes by Ed, but you probably have heard about him as Edward.   
Snowden.

And staying on the vulnerabilities side, this [creative (ab)use of Google Maps](https://twitter.com/simon_deliver/status/1223569659645112320) is definitely going to be used offensively against someone, we just don’t know who yet. But on the other hand, if you’re Amazon, [you don’t care about bending the traffic rules, you just make them](https://twitter.com/GrimKim/status/1361820493079339008) up as you go.

Okay, let’s take a breather here. I mean, I’m starting to sound pretty doomsayish, even for me. So let’s talk about something else, life! In fact, [Conway’s game of life](https://en.wikipedia.org/wiki/Conway%27s_Game_of_Life), a game that requires 0 players, plays itself, is Turing-complete, answers and asks a bunch of mathematics questions and simulates a living organism’s growth patterns across a complex system. I’ve had a lot of fun reading through various strategies and patterns in the game!

Fun fact, some years ago, knowing nothing of this, I actually [built a similar thing](https://github.com/alkoclick/miniLifeSim) from scratch in C# and Unity game engine. The core concept is that you have a 2d map with a bunch of nutrients containing energy of random types (A-D) and randomly moving organisms that move around ingesting one kind of nutrient and egesting another, e.g they eat A and poop C. If the organisms get to 0 energy they die. Moving costs them energy, and if they get to 150% of their original energy, they actually split into 2 organisms, with a chance X that the new organism actually ingests and egests different nutrients. Through experimentation I discovered some really cool facts:  
- My random organisms largely clustered together in “towns”, which were occupied by diverse organisms that basically “traded” resources with each other  
- Apparently the evolutionary chance X is a pretty important thing. If it’s too low, the organisms consume all their primary nutrient and die out. If it’s too high, organisms basically evolved equally, with near 0 natural selection at play, and the entire ecosystem died out. In numbers, 30–50% was an ideal rate in my system. Turns out I had actually stumbled on one of the fundamental facts of evoutionary biology, lol.

Ever played any videogames where you had a cheatcode with some weird or funny combination of moves? Disappointed that irl there’s not such thing? [DO I HAVE NEWS FOR YOU](https://stackoverflow.com/questions/7580508/getting-chrome-to-accept-self-signed-localhost-certificate/47646463#47646463). Basically you can type “thisisunsafe” in any chrome-based browser to turn off security controls for the page you are in. Found it out while localhost testing some self signed certificates.

Ever had to use a system that seems to mess up your name? That’s no rare occurence especially if, like me, your name is over the default SQL varchar column count of 30 characters, or it has non-english characters. The programmers who built this system implicitly or explicitly made a series of assumptions. [Here’s a list about such failed assumptions about names](https://www.kalzumeus.com/2010/06/17/falsehoods-programmers-believe-about-names/).

That initial article back in 2010 spawned a cascade of “falsehoods programmers believe about X”. I spent hours reading through multiple such lists — [here’s the motherload](https://github.com/kdeldycke/awesome-falsehood).

Another series of articles and repos are the “Awesome X” genre. You may stumble on them from time to time, especially in Github. Here’s “[Awesome roadmaps](https://github.com/liuchong/awesome-roadmaps)”, offering roadmaps for different programming languages and tech stacks.

![](https://cdn-images-1.medium.com/max/800/0*7m13T1NOpQu3K4_6)

Photo by [JJ Ying](https://unsplash.com/@jjying?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

Now, living in Amsterdam, I can’t help but think about the tech capital across the channel — London. I do not currently envy [the island whose ham sandwiches are now illegal](https://www.bbc.com/news/world-europe-55622331) in the EU, though I do [respect their vaccination numbers](https://www.statista.com/statistics/1196071/covid-19-vaccination-rate-in-europe-by-country/). They are going to be adding an interesting notch under their belt though: Uber just [lost a case in the Supreme Court](https://www.wired.co.uk/article/uber-loses-gig-economy-case) and is forced to recognize its gig workers as actual human employees. Uber, a company whose tagline could possibly be “[We’re the biggest money losing company you know](https://news.crunchbase.com/news/understanding-uber-loses-money/)” has long used the low rates to fund its explosive growth. What’s that growth for? If I knew I’d tell you, but at this point I’m beginning to wonder if we’re looking at the next WeWork.

On another note, with the latest updates to the WhatsApp security policy, many folks have been talking about secure messaging mobile apps. But how does the landscape look like from a security perspective? [Ola Bini has a very interesting thread comparing options, compiled here](https://threader.app/thread/1351198565230632962).

It’s been about 45 days since I last spoke about [Facebook’s role in the Myanmar genocide](https://time.com/5880118/myanmar-rohingya-genocide-facebook-gambia/). Time to reset the counter I guess. The platform staunchly refused either to allow external investigations, or to take any meaningful action. But hey, when Australia decided to start charging platforms for the news content hosted on their sites, [Facebook went nuclear](https://twitter.com/mathewi/status/1362109514141556740) and… [caught itself in the aftermath](https://twitter.com/AndrewBrownAU/status/1362173723151798276)?

![](https://cdn-images-1.medium.com/max/800/0*jRzrAvHy2zT56ds5)

Photo by [Wicked Monday](https://unsplash.com/@wickedmonday?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

Now, you’ve probably already heard the news: [Jeff is stepping down as Amazon CEO](https://www.cnbc.com/2021/02/02/jeff-bezos-to-step-down-as-amazon-ceo-andy-jassy-to-take-over-in-q3.html). His successor, whose name you probably wish you won’t have to know for another couple years, [has an interesting view on machine learning and neural networks](https://twitter.com/alfredwkng/status/1356717392961937413). By interesting I mean “wholly uninformed or ignoring of the usage of facial recognition against Hong Kong protesters and even BLM protesters on US soil with generally disasterous results that we’ve already discussed about in this newsletter”, so holy fuck.

I don’t know what note to close this on, so I’m going to leave you with one of the headline songs of the album I was just listening to: “[The Algorithm — Muse](https://www.youtube.com/watch?v=X8f5RgwY8CI)”. Oddly fitting, I find.

P.S Wanna work for a pretty cool employer, writing open source code and developing a product that gives people control over their data? Check out Memri.io and [their job postings](https://memri.cloud/jobs), a former colleague let me know about them and I’m now assisting in their DevOps hiring process, so hit me up for a possible referral!