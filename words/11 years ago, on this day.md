Originally posted on [[2019-12-06]] at CodiMD

#articles 

---

Hello cool kids!

Is it friday? It’s [friday, friday](https://www.youtube.com/watch?v=kfVsfOSbJY0) does anyone still remember Rebecca Black?

### This is turning out to be everyone’s fav segment

Hot out the gates! Not even time to scroll down to the typical twitter drama, it’s scrollin up to you instead!

-   [It’s 2019, are we still doing this?](https://2019.phpce.eu/en/)
-   [It’s 2019, are we really still doing this?](https://twitter.com/abbyfuller/status/1194397840287522816)
-   It’s 2019, are we really really… (not a link yet, I’ll update it as soon as the next one becomes a thing I promise)
-   [Codemopolitan is a thing I am well and trully into](https://www.codemopolitan.com/8-commit-messages/)
-   [This has been a pretty gold thread across tech](https://twitter.com/nipafx/status/1199636255132266496)
-   [Have some aggressive motivation to avoid overengineering your persistence/model layer](https://blog.jooq.org/2019/11/13/stop-mapping-stuff-in-your-middleware-use-sqls-xml-or-json-operators-instead/)
-   [I’m slowly developing a bromance with this man, he just doesn’t know it yet](https://twitter.com/dhh/status/1201870975228186624)

### How many letters does it take to spook Elon?

Now, I know a lot of cool kids are into this AI thing and I didn’t want to be insensitive to the tunes of the youth, lest I be greeted by the dreaded “Ok boomer” (it’s happened twice already ok?). So, [here’s some fancy schmancy AI paper for you](https://arxiv.org/abs/1911.11423)

### Supply-chain? I hardly knew ‘er!

And since we’re still in this Python thing, are you familiar with the series of supply-chain attacks that have been targetting developers recently?  
No?  
So, here’s how it goes:

-   I create a malicious program that does something evil, such as DDOS my enemies, or retweet Donald Trump
-   I set it up to run inside a library that looks innocent or misleading (e.g Pundaz or python-triange-math)
-   I push this library to a package repository (Maven central, NPM, or PyPi)
-   Unsuspecting devs include my library in their applications
-   As soon as their application is run (including testing), I do my damage, preferably in subtle or invisible ways

This attack is why it is important to have good controls in place for repository packages and to also only use trusted code as a dev. Honestly, both [NPM](https://www.synopsys.com/blogs/software-security/malicious-dependency-supply-chain/) and [PyPi](https://www.zdnet.com/article/two-malicious-python-libraries-removed-from-pypi/) are pretty open to anyone pushing packages with minimal effort. Friends dont let friends include unofficial, unvetted libraries, but then again, the Javascript attack was done using a product with millions of users. [Would it really be that hard to find another similar case?](https://twitter.com/fringetracker/status/991796881767436288/photo/1)

### Inter-views!

Good news! Or bad, depending on your outlook. I got through the fourth stage (!) of interviewing with a company and onwards to stage 5: On-Site interviews! With this opportunity, let’s take a quick look at what are the steps you would typically expect a tech interview process to have in the industry.

Stage 1: Vetting

-   With: General HR / recruitment person
-   Duration: 15–30 minutes
-   Key points: Have a good, clear, short explanation of your CV and skills
-   They would like to: Quickly figure out if you are a mismatch for the position, so they will drop keywords related to the tech, and also generally gauge the potential you are a psychopath / PR disaster waiting to happen / problematic employee.
-   Don’t: Ask long questions or speak long sentences.

Stage 2: Tech skills exercise

-   With: Yourself usually
-   Duration: 1–4 hours
-   Key points: Most companies check just algorithmic skill tbh. Read through [this masterpiece](https://epiportal.com/Ebooks/Cracking%20the%20Coding%20Interview%2C%204%20Edition%20-%20150%20Programming%20Interview%20Questions%20and%20Solutions.pdf) at least once. Practice. If you find a company that has an alternative/nontraditional way to do this stage, they’re usually good.
-   They would like to: Figure out your actual tech skill based on some BS exercise
-   Don’t: Spend too long on it or go unprepared

Stage 3: Tech skills debrief _(optional)_

-   With: Senior engineer(s)
-   Duration: 60–90 minutes
-   Key points: Explain your code and line of thinking. Be honest, admit mistakes. You are being checked both for your tech skill, as well as your communication and teamwork.
-   They would like to: Figure out if you can understand the code you write and how you react to being on the spotlight like Zucc on a Congress hearing
-   Don’t: Get defensive of your code or lie

Stage 4: Motivation review _(optional)_

-   With: Senior manager
-   Duration: 45–60 minutes
-   Key points: Explain more or less what you told them in stage 1, but also create a more personal connection to their business. Most companies look for people who would be excited and motivated in their new workplace, for whatever reason. Find the things they do that excite or impress you and make sure they come up.
-   They would like to: See if there is anything wrong with you that hasn’t been caught before, see what potential roles/teams you could fit into (it’s quite possible your job application can fit in multiple spots), before they spend the money to fly you over
-   Don’t: Be ignorant of their company, or an asshole

Stage 5: Onsite

-   With: Anyone they can fetch
-   Duration: 4–8 hours
-   Key points: They are expected to generally cover your expenses for getting there. You will be meeting the people you will be working with in the future, if it works out. Usually any single one of them can veto your application, so tread carefully.
-   They would like to: Get the final approvals from everyone on the team that you are a cool kid indeed
-   Don’t: Worry too much, if you got here with one company, you can do it with others too.

Side notes:

-   Each additional stage increases your hiring chances by about 20%, as the company is putting more and more resources into your application
-   It’s good to generally do some research into the company and use that in your cover letter. It’s also good to generally have a [cover letter](https://demo.codimd.org/s/rkfMyNPaS) at all. In this sample, I’ve bolded out the stuff I exchange per company.
-   Have a very clear expectation of your salary before you jump into the process with a company. They will probably ask for it in Stage 1, then again in 4 & 5. Don’t be afraid to share it, don’t be afraid to negotiate yourself up (they can always do something better)
-   While most companies follow hiring processes along these lines, obviously they will have variations. Pay attention when the process is explained to you, usually this will happen at the end of every step.
-   You are also vetting their company at each step. Don’t be afraid to walk away. Keep an eye out for red flags, whatever those may be to you. The IT market is definitely a worker’s market and you are pretty valuable even as a junior.

Stay awesome,  
Alexander P.