I often think about this Picasso art pice:
![](https://upload.wikimedia.org/wikipedia/en/e/ed/Pablo-Picasso-The-Bull.jpg)

I have some more extended thoughts and examples over in [Gerard Thomas and conceptual ideas](Gerard%20Thomas%20and%20conceptual%20ideas.md). 

Applying the same deconstruction logic to code yields some of the following:
```
val database = map[string, array[row]]

fun execute(structured_statement)
```

This should present as a SQL database. 

```
index = page_rank(internet)

fun search(query)
```

This is Google's search product. Now this requires you to know that Google search uses the PageRank algorithm... but doesn't the Picasso example require you to have seen a bull? Are those two comparable? 

I am leaning towards no, as PageRank is an internal thing of Google's tech (however famous it may be). As a layperson you see the search box, you don't really delve into the algorithm. Given Google's popularity, would it then be possible to just do:
```
fun search_internet(query)
```
to represent it? Would anyone seriously consider "Bing" or "DuckDuckGo" being the answer here?

In Gerard Thomas's examples, you need a certain amount of exposure to car culture to "get it". If you've never seen the car he's referring to, you cannot "get it". Picasso's example works similarly. So far we've operated under that assumption. The artist simplifies the object's [gestalt](https://en.wiktionary.org/wiki/gestalt), its concept or "entireness" if you will down to a simplified form that can impress upon you the idea of the whole. Notably, some research on that was done by Norbert Wiener, and you can read about it in Chapter 6 of my [Thoughts on reading Cybernetics](Thoughts%20on%20reading%20Cybernetics.md).

What if we broke that? What if I tried, through code, to make you envision a concept that you have not (necessarily) encountered before? A tech tool that doesn't exist and yet you can imagine it existing based on these few lines:

```
fun search(query)
	result = actual_search(query)
	if result == null
		return imagined_result(query)
	
	return result
```

*"In some ways the above is not far from an LLM"*, I can hear you cynically commenting, and yet, to be far, it's not quite one, is it? It's just a search engine that always finds a result, whether one exists or not. Is it useful? Probably not. Is it what you the concept you got in your head? Unclear to me!

```
person = population.random()
soulmate = population.random()
while match_quality(person, soulmate) < 0.9
	manipulate(person)
	manipulate(soulmate)
```

What do you get from this description? What's the idea of this "app"?

In my head, it's a dating app that works by manipulating its users, rather than matching them. Now that description, "a dating app that works by manipulating its users rather than matching them" is 76 characters. The example above is 145, nearly double the length. 

Are we showing that code is a poor abstraction choice because it's structured text, and unstructured text using the full power of language can carry far more signal per character? Probably, though if we're being honest, a more accurate description would be "A search app that selects random users, pairs them, then manipulates them until they are a good enough match" which is 108 characters to the 145. 

Abstraction is, in the end, just some variations of reversible lossy compression and we already know that [Ideas are uniquely expressed in mediums](Ideas%20are%20uniquely%20expressed%20in%20mediums.md). We are doing text->text abstracting here, right? 