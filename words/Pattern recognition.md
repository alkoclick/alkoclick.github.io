Originally posted on [[2019-10-09]] as an email

#articles 

---

Hey cool kids!

This issue focuses on pattern recognition. "_Great"_, I hear the voice inside your head, "_finally he's gonna talk about all that fancy ML stuff, right?"_


Hahahahaha no. We're gonna talk about like, _actual_ development? ML is cool and all but I'm not the expert to talk about it. We may get such an expert in this very newsletter though, so stay tuned!  
  

Woah, all this misleading kinda starts to sound like fake news. But then again, [I don't think most people want to live in a world where you can only post things that tech companies judge to be 100 percent true](https://www.cnet.com/news/facebook-ceo-mark-zuckerberg-defends-decision-to-allow-politicians-to-lie-in-ads/)  

_Are you gonna be taking weekly stabs against Mark now? Stop_

No. But he just keeps on giving! Did you actually hear the Georgetown speech? It's almost like Steve Jobs' [inspirational graduation speech](https://www.youtube.com/results?search_query=steve+jobs+speech), only reversed and fucked up.  

_sudo stop_

Nope, not working

_sudo -u#-1 id -u OR sudo -u#4294967295 id -u stop_

Ok. [Holy shit that actually worked](https://thehackernews.com/2019/10/linux-sudo-run-as-root-flaw.html)! 

_Did you see the Joker yet? Great movie right?_ 

Yes! Apparently the co-founder at GitLab thought [his business too needed some chaos](https://www.theregister.co.uk/2019/10/16/gitlab_employees_gagged/), only to be [promptly thwarted the next day](https://www.theregister.co.uk/2019/10/17/gitlab_reverse_ferret/) by the chief marketing officer (which sounds like a really stressful job) and his trusty sidekick. Back to the Arkham with ya!

_So, about those patterns?_

Well, do you know what is GoF?

_Baby don't hurt me?_

No, GoF, (Gang of Four, not the [band](https://en.wikipedia.org/wiki/Gang_of_Four_(band)), not the [political exiles](https://en.wikipedia.org/wiki/Gang_of_Four), not one of the 1783 Pornhub search results) are the original authors of the "[Design Patterns](https://en.wikipedia.org/wiki/Design_Patterns)" book, quite possibly one of the most monumental books in the history of software.  

_What are design patterns and why should I use them?_

Design patterns help you tackle common problems, without your code base blowing out of control. They represent industry standards and often graduate to be built-in language features. Design patterns are mostly found in more mature languages, or those that deal with the enterprise, as that's where they have the most impact.

_Ok, I knew most of that already. So I should just use them everywhere, right?_

Absolutely not. These patterns are there to deal with problems. Over time you will start to discover more and more applications and how effective they really are. But it's important to first identify the problem, then the patterns which could address it, then understand if and how you would need to adapt them. Applying a "good practice" blindly is sure to turn it into a bad practice.

_Can you give me [some examples](https://stackoverflow.com/questions/1673841/examples-of-gof-design-patterns-in-javas-core-libraries)?_

Absolutely! Let's take a look at some of the patterns stated in that answer, with a bit more context and 10 years of hindsight. Examples are Java-like, but no real language.  

**Factory**

This pattern has a lot of sub patterns, but I will group their core functionality here. Factories deliver new instances of a ready-to-use object. This object may be precustomized in what is called an "opinionated default", but other than that, the factory doesn't offer much customization. The factory itself may often be a Singleton.

Example:

```java
Factory toyotaFactory = new ToyotaFactory()
Car toyota = toyotaFactory.newCar()  
```

**Builder**

The builder pattern is, on the other hand, about customization. You start with an "empty" object, then along the way you apply to it all the stuff you want. Very handy for when you need to support very different and customizable instances of the same object.  

Example:

```java
CarBuilder toyotaBuilder = new CarBuilder()

Car toyota = toyotaBuilder.color(Color.RED).windows(Windows.ELECTRIC).abs(true)

.gps(true).childSeat(false).build()
```

We could also have a CarBuilderFactory creating CarBuilder instances, as the CarBuilder class seems to require little customization itself (builders are often like that). Quite often btw the CarBuilder class and the Car class are different and you don't actually have a Car instance until you call "build()" itself.  

**Singleton**

Create a single instance of a particular object, for the entire program. This is one of the most used patterns out there, but over time has often been criticized as unsafe, bad design, and most implementations of it suffer by some sort of concurrency issue. Languages such as Kotlin, or C#, have the singleton pattern already implemented and even a keyword. However, this is usually the wrong pattern to use. It looks simple and you may even have an ok implem of it. But there is probably a better design option.

Example:

Yeah, no

**Facade**

This pattern is not so common, but I've opted to include it here, because my current project at work involves getting rid of a gigantic Facade/Gateway mess. When a pattern is abused (usually something that happens over time as the requirements evolve but the architecture doesn't), it ends up being an active hindrance to the developer. Some signs of a failing design pattern are:

- Confusing architecture
- Multiple layers that do very little actual work
- Code that exists only to maintain a similar structure to other code, not because it's ideal/useful

It's important to remember a pattern is supposed to deliver value. Panos Lantavos has elegantly put this as "Architecture over functionality", which is a plague in the enterprise world. This is not a choice you should have to make and if you are, you're using the wrong pattern. But do not underestimate the brains of the people who developed and implemented those. They were solving real world problems and sometimes they even had to choose between bad and worse. Assume they chose wisely, until you can reliably prove otherwise.

**Observer**

Hugely popular and the heart of many major frameworks/applications. Also called the [publisher/subscriber](https://en.wikipedia.org/wiki/Publish%E2%80%93subscribe_pattern) model, you will most commonly find it in what is called a "Message Queue" system. Message Queues (MQs) provide an asynchronous communications protocol, meaning that the sender and receiver of the message do not need to interact with the message queue at the same time. Messages placed onto the queue are stored until the recipient retrieves them. Message queues have implicit or explicit limits on the size of data that may be transmitted in a single message and the number of messages that may remain outstanding on the queue. That's totally copy/pasted from my article on MQs btw, coming out soon!

Examples:

RabbitMQ, Apache Kafka

**Circuit Breaker**

Not in the original GoF book, [this is a very interesting pattern](https://martinfowler.com/bliki/CircuitBreaker.html) (and a personal pet peeve). I hope you read that last link, because that's Martin Fowler. Use this pattern to safeguard against cascading failures in complex systems. Essentially the logic is "every time you get a minor (recoverable) failure, increment a counter. If there are no failures for a while reset the counter, When a counter limit is reached, shut down your system". Even defining the logic requirements for this pattern's application will be a very illuminating view into your system, what to expect and what are its conditions and possible states.

Example:

```
while (true) {
  circuit.reset()
  if (Network.isUnavalable()) 
    circuit.add(1)
  if (Drive.isInaccessible()) 
    circuit.add(1)
  if (System.isUnresponsive()) 
    circuit.add(1)  
  if (circuit.get() > 2) 
    throw new CircuitBreakerException("Failure threshold exceeded")
  sleep(100 ms)
}
```

_But I write in beautiful Haskell/Clojure/Lisp! I don't need these.. (scoffs)... patterns_

First of all, noone ever called Lisp beautiful, so don't start that shit here. 

Secondly, patterns are a tool that depends on the implementation. Your language may make some things easier, or even unnecessary. It may make others essential. Knowing well thought-out algorithms to tackle common problems can only be a benefit... _as long as you are also measured and careful in the way you apply them._

Final note: I'm evaluating whether I will stay longer in CERN, or search for something else. This section aims to give you some insight in how I search for work. As part of that effort, I've updated my CV across Europass, LinkedIn, StackOverflow careers and my [github profile website](https://alkoclick.github.io/). I also marked myself as "actively looking" in those platforms, who are, in my experience, the best starting (and ending) point in that search. Will probably update with more info next week!

That's all from me, and hope you had/have a great weekend!

Cheers,

Alexander P.