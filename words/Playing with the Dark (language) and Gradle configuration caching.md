Originally posted on [[2021-05-07]] at [Medium](https://medium.com/@alkoclick/playing-with-the-dark-language-and-gradle-configuration-caching-2da81138e2a9)

---

![](https://cdn-images-1.medium.com/max/800/0*RkcoUsrX-mFMJ8mZ)

Photo by [Jerry Wang](https://unsplash.com/@jerry_318?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

Hey everyone! This is a collection of notes for some things I’ve been toying with the last few days and how they went.

### Dark (Language)

[**darklang/dark**  
_This is the main repo for Dark, a combined language, editor, and infrastructure to make it easy to build backends. This…_github.com](https://github.com/darklang/dark "https://github.com/darklang/dark")[](https://github.com/darklang/dark)

I’ve been wanting to try Dark for actual years, I’ve had it in my drafts since early 2020, probably earlier. It’s merging a few very cool concepts: 0 infra (serverless), visual development, strong opinionated defaults leading to simple dev and ops cycles. Some of this was very well executed and I’m sure we’ll be seeing more adoptions of the idea in the years to come. Their concept of “Trace Driven Development” was also very fun, intuitive and effective. However, looks like the startup running Dark hit some hurdles back in June and fired 5 out of its 6 members, now only the founder/CTO remains and it’s all community driven, so evolution’s going veeeery slowly. It also felt like, because there’s so little integrations, it’s very difficult to do even the most basic things. I tried to fire up a POC that would scrape HackerNews, then post the headlines as linkable hrefs in a cleaner page because the HN UI is neolithic and also the comments are often a… special place. It was super easy to do the scraper, and super easy to produce the output HTML but it was nearly impossible to actually parse the HTML DOM that I received from HN in order to filter the tiles and repost them. If your language can’t do HTML parsing we probably have issues. Maybe I’ve missed something with the HTML parsing in particular, but overall, the language feels really lacking for anything you’d need in actual production workloads. I’d love to see them keep growing though!

### Kotlin multiplatform native executables

[**Get started with Kotlin/Native using Gradle - Help | Kotlin**  
_Gradle is a build system that is very commonly used in the Java, Android, and other ecosystems. It is the default…_kotlinlang.org](https://kotlinlang.org/docs/native-gradle.html "https://kotlinlang.org/docs/native-gradle.html")[](https://kotlinlang.org/docs/native-gradle.html)

This has also been in the back of my mind for years, there has been a backlog task in Thalatta’s Notion board since 2019. This was decently simple to set up by enabling the Gradle plugin (I was concerned it’d clash with the Kotlin JVM plugin) and it had plenty of interesting readup in their concurrency and immutability models (I skimmed most of it, but it was interesting). However, I realized that our integration path, even if I succeeded would be pretty complex. We have a lot of intra-project dependencies and produce a few (4) output artifacts (containers) via Google’s Jib Gradle plugin. We can’t get rid of JVM compilation completely, because our projects depend on each other and if I understand the Gradle project dependency flow correctly, this basically means that they are importing each other’s JARs, to build which, we need the JVM. Additionally, to trully take advantage of our native artifacts we’d need to switch the Docker base container to something much more barebones, which isn’t easy because we were using the GCR distroless java, which is decently small (80M) for a JVM container and is well, distroless. So we’d probably need to hunt for and test a new base image and figuring that out would take more time than I wanted to allocate.

### Kotlin beta JVM ‘IR’ backend

[**The New JVM IR Backend Is in Beta: Let's Make It Stable Together | The Kotlin Blog**  
_We'll make the new backend Stable soon, so we need each of you to adopt it, let's see how to do it. We have been…_blog.jetbrains.com](https://blog.jetbrains.com/kotlin/2021/02/the-jvm-backend-is-in-beta-let-s-make-it-stable-together/ "https://blog.jetbrains.com/kotlin/2021/02/the-jvm-backend-is-in-beta-let-s-make-it-stable-together/")[](https://blog.jetbrains.com/kotlin/2021/02/the-jvm-backend-is-in-beta-let-s-make-it-stable-together/)

This was super easy to turn on, because we were already on latest Kotlin lang version, you just need the following in your gradle buildscript:

```
compileKotlin {

    kotlinOptions.useIR = true

}
```

I run some test with the build time when using it or not. There was basically no significant difference. I obviously only verified time, there may have been other factors where it excels, but for us, build time is imo one of the most important things to optimize, and this didn’t really do it. Eventually this will become default in the Kotlin plugin, so we’ll be getting it anyway, but for now there seemed to be no reason to switch, given also the risk factor of a beta version. Sorry JetBrains, I really really love your stuff, but I don’t wanna test it in prod yet.

#### Gradle configuration caching

[**Configuration cache**  
_The following sections will go through some general guidelines on dealing with problems with the configuration cache…_docs.gradle.org](https://docs.gradle.org/current/userguide/configuration_cache.html "https://docs.gradle.org/current/userguide/configuration_cache.html")[](https://docs.gradle.org/current/userguide/configuration_cache.html)

This is an incubating feature of Gradle that premiered in 6.5 (we’re in 6.8 atm). Gradle has 2 stages, configuration and runtime. The configuration stage is when the gradle buildscripts are processed, linked and executed. In the runtime stage the actual tasks defined in the buildscripts are executed. So, for example, the module graph is drawn during the configuration stage and the execution plan is drawn, but the dependencies task to import a module’s output artifact is run during the runtime stage. As you probably already know, Gradle does pretty aggressive (and effective) testing in the runtime stage, which is why, when you change a block of code and run `gradle test` only that block of code and whatever is depending on it is recompiled and retested. This feature promises to bring a similar vision of caching to the configuration stage.

We care a lot about this in Thalatta, because we have a looot of modules (30+) and just making their graphs and configuring them takes up quite some time. However, a lot of the plugin ecosystem in Gradle does not yet support this feature. I run some tests in our build using `gradle --configuration-cache help` as a test command, but it appears something is defining a TaskExecutionListener or BuildListener, which blocks the config cache from running. I spent quite some time chasing that something, but could not find it. I suspect it's one of our plugin dependencies, because I could find no reference to any listener or hook in our code. According to the plugin docs, Java, Kotlin and Jacoco plugins are clear. I disabled Jib and semver, but the problem remained. It may be the application plugin, but I'd be honestly shocked if that's the case. Dunno about this one, should probably be put on hold for a while, then when it's stable we can try it again

Hope you enjoyed these random, subjective, opinionated scribbles and I’d love to know any thoughts or feedback you have!

#articles 