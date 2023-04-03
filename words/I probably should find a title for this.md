Originally posted on [[2019-11-21]] at CodiMD

#articles 

---

Hey cool kids!

I’m happy to report that the planning for the first Cool Kid Conference is well under way! We have secured a date and a location and are bootstrapping the rest of the thing together. Are you excited? I am excited! How excited?

**Y E S**

More details will come up in the next issues! For now I can say that it will happen in Thessaloniki, the place that some amongst you have chosen to call an EasyJet destination. The North remembers…

Now let’s get down to business and we’re starting off easy:

### [Mom, why do we have 0 and -0?](https://stackoverflow.com/questions/58691512/why-do-we-have-0-0-and-0-0-in-ruby)

As a personal anecdote here, a sidebuddy of this problem, floating point precision, is a famous weak point for systems, destroying anything [from rockets](https://www.theinquirer.net/inquirer/news/1047844/floating-point-bugs-explode) (_playing a part at least_), to your test flows. JUnit, the most popular testing framework in the JVM which has been a core part of much of the modern software testing lifecycle, defines a family of methods like this:

```
assertEquals(int expected, int actual)
```

```
assertEquals(String expected, String actual)
```

```
assertEquals(Object expected, Object actual)
```

The concept is that you define what you would expect as the result as the first argument, and in the second argument you pass the results from your code. Use like this:

```
assertEquals(4, myPowFun(2,2));
```

_But Alex, why are you bringing this up?_

The educated reader may see this one coming. One of the methods in that family is different…

```
assertEquals(double expected, double actual, double delta)
```

What’s that last argument? The maximum acceptable delta between the values for them to be considered equal! You’d usually pass something like `0.01` or smaller, if you need more precision.

### News to me

[X] Weekly tech drama  
[X] Sexism  
[X] Cameo by Uncle Bob, telling everyone that his gasoline covered, match-wielding pal, is being wrongfully denied entry to a couple of cool barbecues. _Yes, that is metaphorical and an oversimplification._  
[X] [Medium article](https://medium.com/@cherp/propaganda-other-lies-we-tell-4325240379f7).

There’s but one reply.

_Ok boomer_

Millenials, amirite? Such a bunch of sensitive snowflakes, getting offended by everything. My generation fought in Normandy! Some of us were even on the Allies’ side!

_Ok boomer_

[_LISTEN HERE YOU LITTLE SHIT!_](https://twitter.com/rrpre/status/1192862490348179456/photo/1)

### Bitten

I’ll try to avoid getting too philosophical this week, as I feel last week was more than enough.

However, there’s been a string of very interesting cases regarding neural networks and perpetuating social biases. Have you ever considered that we teach computers to learn in the same way humans do, and humans have some problematic lines of thinking, and what does that mean for AI? Some, such as Amazon, chose to scrap their project altogether after it was deemed unsalvageable. What was wrong? Well, to put it mildly, it was [slightly more sexist than my old Greek boss.](https://www.reuters.com/article/us-amazon-com-jobs-automation-insight/amazon-scraps-secret-ai-recruiting-tool-that-showed-bias-against-women-idUSKCN1MK08G) You can probably imagine that’s a high bar, but let me tell you, some tech companies aren’t discouraged by that.

According to some religions, Eva, representing all women, bit off the apple in heaven once upon a time.

In 2019, Apple remembers too, and thinks [it’s about time she got some capital punishment.](https://www.bloomberg.com/news/articles/2019-11-10/apple-co-founder-says-goldman-s-apple-card-algo-discriminates)

Ever made a product so messed up, your actual co-founder publicly called it out? Yeah that’s exactly what happened. The original reporter here btw, DHH, seems like [a pretty cool guy.](https://dhh.dk/)

### Little big words

> _Αυτός  
> ο κόσμος ο μικρός, ο μέγας!_

> _This  
> world the small, the great!  

_[_Odysseas Elytis_](https://en.wikipedia.org/wiki/Odysseas_Elytis)_, in his nobel winning poem, Axion Esti_

I looked up for a good English translation, but this guy is famously difficult to translate. What did I want to refer to? One of the most [impressive grids I’ve seen recently.](https://twitter.com/simonbrown/status/1191285130926678016)

---

We’ll definitely discuss more about microservices in one of the future letters, but for now I really need some rest. It’s been a long week and I hope you’re doing great!

Wishes and stuff,  
Alexander P.

P.S [This Amazon posting might fit or interest some of you](https://www.amazon.jobs/en/jobs/966885/techu-graduate-solutions-architect)