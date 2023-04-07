This is a continuation of [Google Technical Writing Course](Google%20Technical%20Writing%20Course.md)


https://docs.google.com/document/d/1rsRqmlav7onIxMfXRTCO0ImyEBveck5QpOizTFUJIPs/edit#

#### Exercise 1
In the first exercise there were a couple of spaces where I wasn't sure whether "know" or "explain" was more applicable. E.g Software Engs know about "app", but they know about so many types that I feel it'd be a good idea to define it.


#### Exercise 2
This was about switching from passive to active voice. 

As we discussed the examples, we discovered that in example 2 the word "override" is kinda ambiguous. The third example was pretty interesting because it was the most complex. However, it feels like with a more realistic context (e.g what bugs and whether the method usage stopped) it'd be easier to convert.

> People who read documentation have a goal, which usually isn't "read documentation". It's "get something done".
> - Marco Spinello

#### Exercise 3
This was actually pretty fun! Writing a guide from scratch on how to put toothpaste on a toothbrush.

```
**

Okay, so let’s start with some definitions!

The blue thingie on the left is called a tube. We use tubes to contain semi-liquid substances and easily extract them. Tubes have a cap, the little white thing on the right end of it, which allows you to easily open and close the tub. This specific tube contains a substance called “toothpaste”. We can thus call this the “Toothpaste tube”, or “toothpaste” for short.

The green thing on the left is called a toothbrush. You hold it in your hand and you use the soft brush on the left to clean stuff.

Now, here’s a step-by-step guide to putting toothpaste on the toothbrush.

1.  Open the toothpaste tube by rotating the white cap clockwise
    
2.  Hold the toothbrush in your dominant hand
    
3.  Make sure the brush in the toothbrush is facing up
    
4.  Take the open toothpaste tube in your free hand and hold it near the toothbrush
    
5.  Use your fingers to squeeze the toothpaste tube
    
6.  Toothpaste will start to slowly come out - direct it over the brush of the toothbrush
    
7.  Stop squeezing the toothpaste tube once you have enough
    
8.  That’s it, you’re done!
    

Remember that once you are done using the toothpaste tube, you should close the cap again before storing it. You can do that by:

1.  Putting the cap back on
    
2.  Rotating the cap counterclockwise.
    

**
```

I asked Marco, our instructor on where we should possibly draw the line between text or other forms of content which could be a better fit. Marco pointed out that images or videos are much harder to maintain in the long term. Small changes require reshooting a whole video, or rebuilding a whole image. He also pointed out that different folks appreciate different mediums and may even have accessibility issues with some mediums.

How much are you trying to write? If it starts to feel like a post is too much, break it down into separate posts. This will make it easier to maintain, but also demonstrate any hidden relationships between components.

People tend not to click through to glossaries when they are placed in the end. However, if it's at the start, it's "in your face" and it's more possible for the audience to actually consume it. You can even consider adding a requirement such as "To move on, make sure you understand what X is"

#### Minimum viable documentation set
> What is the minimum amount of documentation I can write and still provide value?

Maintenance of docs costs energy, so make sure to be careful of how much you write. Optimise for efficiency.

---

Sorry, I run out of energy to collect further notes for Ex 4 and 5.

---

> I like to use simple words like "thing" to describe concepts. Is that a useful practice, or does it hinder communication?

* It's a good idea, unless the simple word removes an important piece of info about the concept (e.g a load balancing / proxy server should probably be called load balancer)
* "Thing Explainer" (book by Randall Munroe)

> How do you approach documentation maintenance?

* Tied to the tooling
* Content reuse is a big feature for docs maintainability