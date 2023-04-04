The Google technical writing course is avaible [here](https://developers.google.com/tech-writing/overview). I took it during March '23 while working at [Miro](Miro.md)

## Notes on Technical Writing One

#### Summary

Technical Writing One covers the following basic lessons of technical writing:

-   Use terms consistently.
-   Avoid ambiguous pronouns.
-   Prefer active voice to passive voice.
-   Pick specific verbs over vague ones.
-   Focus each sentence on a single idea.
-   Convert some long sentences to lists.
-   Eliminate unneeded words.
-   Use a numbered list when ordering is important and a bulleted list when ordering is irrelevant.
-   Keep list items parallel.
-   Start numbered list items with imperative words.
-   Introduce lists and tables appropriately.
-   Create great opening sentences that establish a paragraph's central point.
-   Focus each paragraph on a single topic.
-   Determine what your audience needs to learn.
-   Fit documentation to your audience.
-   Establish your document's key points at the start of the document.

#### Words
> When writing or editing, learn to recognize terms that might be unfamiliar to some or all of your target audience. When you spot such a term, take one of the following two tactics:
> 
> -   If the term already exists, link to a good existing explanation. (Don't reinvent the wheel.)
> -   If your document is introducing the term, define the term. If your document is introducing many terms, collect the definitions into a glossary.

Fair

> ## Use terms consistently
> 
> If you change the name of a variable midway through a method, your code won’t compile. Similarly, if you rename a term in the middle of a document, your ideas won’t compile (in your users’ heads).

That's actually a pretty nice way of putting it

Use acronyms like this: The **Confusing Project Network (CPN)**... 
*(they also recommend using bold on the term you are defining)*

Pronoun guidelines:

-   Only use a pronoun _after_ you've introduced the noun; never use the pronoun before you've introduced the noun.
-   Place the pronoun as close as possible to the referring noun. In general, if more than five words separate your noun from your pronoun, consider repeating the noun instead of using the pronoun.
-   If you introduce a second noun between your noun and your pronoun, reuse your noun instead of using a pronoun.

Avoid using these common misunderstanding machines:
* this/that
* it
* they/them/their

#### Prefer active voice to passive voice

> Use the active voice most of the time. Use the passive voice sparingly. Active voice provides the following advantages:
>
> -   Most readers mentally convert passive voice to active voice. Why subject your readers to extra processing time? By sticking to active voice, you enable readers to skip the preprocessor stage and go straight to compilation.
> -   Passive voice obfuscates your ideas, turning sentences on their head. Passive voice reports action indirectly.
> -   Some passive voice sentences omit an actor altogether, which forces the reader to guess the actor's identity.
> -   Active voice is generally shorter than passive voice.

Be bold—be active.


#### Sentence clarity

>Comedy writers seek the funniest results, horror writers strive for the scariest, and technical writers aim for the clearest. In technical writing, clarity takes precedence over all other rules. This unit suggests a few ways to make your sentences beautifully clear.

These following verbs are weak! You should reduce them! (Their words, not mine):

>-   forms of _be_: is, are, am, was, were, etc.
> -   occur
> -   happen


> Reduce there is / there are. In the best-case scenario, you may simply delete **There is** or **There are** (and possibly another word or two later in the sentence).
> 
> There is a variable called `met_trick` that stores the current accuracy. -> The `met_trick` variable stores the current accuracy.

> **Note:** Don't confuse educating your readers (technical writing) with publicizing or selling a product (marketing writing). When your readers expect education, provide education; don't intersperse publicity or sales material inside educational material.

Avoid adjectives and prefer to use factual data such as numbers. Using concrete data will help you come across as technical documents and not marketing.


#### Short sentences

You should want to have short sentences for the same reason you strive to have fewer lines of code.

> Focus each sentence on a single idea, thought, or concept. Just as statements in a program execute a single task, sentences should execute a single idea.

That's a pretty neat way of putting it.

**Subordinate clauses** are subsentences adding context or definitions to a sentence. Avoid them when possible. Stick to one idea per sentence.

#### Lists & Tables
Lists are great! Readers love them! 

3 types of lists:
* Numbered
* Bulleted
* Embedded

Numbered and bulleted lists are different. Does the list's meaning change if you reorder the items? Then use a numbered list. Otherwise, use a bulleted list.

An **embedded list** (sometimes called a **run-in** list) contains items stuffed within a sentence. That's usually a bad idea.

> What separates effective lists from defective lists? Effective lists are parallel; defective lists tend to be nonparallel. All items in a **parallel** list look like they "belong" together. That is, all items in a parallel list match along the following parameters:
> 
> -   grammar
> -   logical category
> -   capitalization
> -   punctuation

> The first item in a list establishes a pattern that readers expect to see repeated in subsequent items.

> Consider starting all items in a numbered list with an imperative verb. For example:
> 1.  Download the Frambus app from Google Play or iTunes.
> 2.  Configure the Frambus app's settings.
> 3.  Start the Frambus app.

> If the list item is a sentence, use sentence capitalization and punctuation. Otherwise, do not use sentence capitalization and punctuation.

> Consider the following guidelines when creating tables:
> -   Label each column with a meaningful header. Don't make readers guess what each column holds.
> -   Avoid putting too much text into a table cell. If a table cell holds more than two sentences, ask yourself whether that information belongs in some other format.
> -   Although different columns can hold different types of data, strive for parallelism _within_ individual columns. For instance, the cells within a particular table column should not be a mixture of numerical data and famous circus performers.

> We recommend introducing each list and table with a sentence that tells readers what the list or table represents. In other words, give the list or table context. Terminate the introductory sentence with a colon rather than a period.

Introduce your lists and tables!


#### Paragraphs
>The work of writing is _simply_ this: untangling the dependencies among the parts of a topic, and presenting those parts in a logical stream that enables the reader to understand you.

>The opening sentence is the most important sentence of any paragraph.

>A paragraph should represent an independent unit of logic. Restrict each paragraph to the current topic. Don't describe what will happen in a future topic or what happened in a past topic. When revising, ruthlessly delete (or move to another paragraph) any sentence that doesn't directly relate to the current topic.

> Readers generally welcome paragraphs containing three to five sentences, but will avoid paragraphs containing more than about seven sentences.

Wonder if they have data on that :/

> Good paragraphs answer the following three questions:
> 1.  **What** are you trying to tell your reader?
> 2.  **Why** is it important for the reader to know this?
> 3.  **How** should the reader use this knowledge? Alternatively, how should the reader know your point to be true?


#### Audience
They actually link to [this video](https://www.youtube.com/watch?v=eFtXIrmsMwI) lol

It is important to define your audience, so you can tune your message to their missing knowledge.

1. Begin by identifying your audience's **role**(s).
	1. People within the same role _generally_ share certain base skills and knowledge
	2. Some people will be closer to a project or idea than their peers
2. Determine what your audience needs to learn
3. Fit documentation to your audience
4. Prefer simple words and avoid keep your writing culturally neutral


#### Documents

Once you know how to make words and sentences, we hope you can put them together in a coherent document. Emphasis on hope.

Begin by defining the scope. These are the things you will cover. It's also a great idea to define the non-scope. These are things you will explicitly not cover.

State your audience. This may be based on role, or knowledge prerequisites.

Summarize your key points. Busy readers may not read more than your opening paragraph, so put important information there. Revise this part ruthlessly to increase conversions.

Use comparisons to existing ideas and concepts your audience knows.

Understand your audience's needs, and use them to structure your document.

> -   Who is your target audience?
> -   What is your target audience's goal? Why are they reading this document?
> -   What do your readers already know _before_ they read your document?
> -   What should your readers know or be able to do _after_ they read your document?


#### Punctuation

Avoid using commas to splice together distinct sentences into one.

Semicolons connect highly related thoughts. Before using a semicolon, ask yourself whether the sentence would still make sense if you flipped the thoughts to opposite sides of the semicolon.

> Use parentheses to hold minor points and digressions. Parentheses inform readers that the enclosed text isn't critical. Because the enclosed text isn't critical, some editors feel that text that deserves parentheses doesn't deserve to be in the document. As a compromise, keep parentheses to a minimum in technical writing.
> 
> The rules regarding periods and parentheses aren't always clear. Here are the standard rules:
>
> -   If a pair of parentheses holds an entire sentence, the period goes inside the closing parenthesis.
> -   If a pair of parentheses ends a sentence but does not hold the entire sentence, the period goes just outside the closing parenthesis.
