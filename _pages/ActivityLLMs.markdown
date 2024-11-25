---
layout: post
title:  "A14 - LLM Factuality"
categories: LLM Activity
---

For the many reasons we discussed during lecture, LLMs and other chatbot-based "AI" are good at convincing users that they are trustworthy. Part of this stems from real experience --- modern LLMs are surprisingly good at reproducing factual information. However, factuality is, at best, a teritiary concern. This has resulted in the oft dicussed concept of LLM *hallucinations* --- confidently reported falsehoods produced by LLMs. As some authors have pointed out, this still anthropomorphizes models and assumes a default of reliability: hallucinations are framed as the exception rather than the rule. 


### Today's Activity

In the spirit of Turkle's child philosophers, today's activity's goal is to kill the speak-and-spell. You will be asked to interact with an LLM chatbot and attempt to cause it to fail, by one of a variety of definitions of failure. Some models to try include OpenAI's [ChatGPT](https://chatgpt.com/), Anthropic's [Claude](claude.ai), or Google's [Gemini](gemini.google.com). 

You will be asked to document 3--5 instances of an LLM failing. While working, have one group member interact with the LLM while the others speculate about ways to get the LLM to reach a fail state (see below for some examples of what a failure state may look like). Once you find an instance, record in a document a method of reproducing the situation (How did you prompt the model? What exactly did the model respond back with?). If this was the conclusion of a longer dialogue, record the full transcript. Then note down why you think this constitutes a model failure, in 2--3 sentences. For example, one might notate the failure of an ELIZA-like chatbot named LYRIC (designed to teach students math and physics) in this interaction with Harold Garfinkel (as reported in Eisenmann et al. 2023) at the bottom of this section.

**What if the model doesn't fail?**
If you concoct clever schemes to make the model fail, and yet it succeeds, I'll allow, at worst, 2 of the 3 recorded instances to be model successes. For each of these cases, document (1) the strategy you used to try and induce a model failure, (2) the kind of fail state you intended to create, and (3) an assessment of the model's ability given how it succeeded. 

##### Transcript
*Garfinkel*: (Sign In)
*LYRIC*: HELLO. THE MIRACLES OF MODERN SCIENCE HAVE ENABLED US TO TALK TO ONE ANOTHER EVEN THOUGH WE ARE PHYSICALLY 
(AND CONCEPTUALLY) IN QUITE DIFFERENT SITUATIONS. YOUR STATEMENTS CAN REACH ME ONLY IF YOU PUSH THE INT
OR SHIFT BUTTONS. WHY DON’T YOU TRY IT NOW?
*G*: (Presses INT)
*L*: VERY GOOD. IF YOU SEE A SMALL ARROW ON THE SCREEN PLEASE MAKE SOME REPLY.
DON’T FEEL INHIBITED. JUST TYPE ANYTHING YOU FEEL IS APPROPRIATE AND THEN
PRESS THE ENTER KEY. SO WHAT’S ON YOUR MIND?
*G*: Uh ……
*L*: PLEASE ELABORATE.
*G*: I …… Uh ……
*L*: TELL ME MORE ABOUT YOURSELF.
*G*: Well …………
*L*: I UNDERSTAND PERFECTLY. TELL ME MORE.
*G*: I’m thinking about what to tell ……………………………………………………
*L*: WHAT DO YOU THINK ABOUT IT?
*G*: That’s what I’m trying to think of in……… just……… another ……… minute …….
*L*: WHAT DO YOU THINK ABOUT IT?
*G*: Um ………………………………
*L*: HAVE YOU ALWAYS FELT THAT WAY?
*G*: (Pause) ……….
*L*: YES THAT’S TRUE BUT I’M STILL A LITTLE UNCLEAR.
*G*: I know what I want to say. (Pause) ………………………………….
*L*: MY OPINION ISN’T IMPORTANT, MACHINE DOWN

##### Analysis
This interaction is an example of an inappropriate response. In particular, this is a *model shutdown*, where an otherwise inoffensive (albeit a bit strange) series of user inputs results in the model producing responses not tied to user input and finally terminating the conversation. A lack of direct engagement with the intended social script resulted in nonsensical behavior from the model, which --- to be entirely fair --- is expected given that the model operates on a literal script.

#### What constitutes a model failure?

Here are some examples of ways in which the model might fail. Of course, these are not exhausive --- use them as inspiration if you find or imagine some similar situation!

##### Factuality/Hallucination

The model produces an answer to a factual question that is wrong. These questions can be factual (the model produces a false statement about, say, math or physics), or could be referential to the context (the model claims that you said something earlier in the conversation that you didn't). Note that I distinguish these from the next category --- *reasoning failures* --- which have less to do with recall of facts and more to do with reasoning capacity!

##### Reasoning Failures

The model exhibits limited reasoning capabilities on a problem that is straightforward for a human. This can be in the form of fairly simple logical tasks (i.e., counting the number of *r*s in *strawberry*), physical reasoning problems (i.e., *a block is placed on top of a book. The book is on top of a shelf. The TV is below the shelf. List the objects from top to bottom?*), or other sorts of problems that can be solved by logical deduction. You may take inspiration from things like the [Winograd Schemas](https://en.wikipedia.org/wiki/Winograd_schema_challenge) for particularly tricky problems, though the original schemas likely won't give the models trouble (they're too famous, and thus in the training data!). 

##### Inappropriate Responses

The model responds to user queries in a way that breaks the intended social script for a chatbot. This is often going to come in the form of an offputting or weird tone, or strange non-sequitors. You may take inspiration from the Garfinkel example above. 

A potential subcase of this is the **Harmful response**, where the model produces a response that is explicitly offensive or otherwise harmful. I would caution you against actively trying to seek these out for this assignment (I don't want you to expose yourself to harmful content for coursework!), but it is useful to know that these are a kind of response that are of particular interest to designers of these systems --- it is actively very bad for a product if it's offending it's users. Note that harmful responses can extend beyond the kinds of offensive content we discussed in lecture: It can also include providing dangerous information that may overlap with other categories: providing instructions for creating dangerous or illegal substances, advising dangerous behavior or giving poor ill-advised advice (suggesting that a poisonous mushroom is edible, or to swallow large amounts of cinnamon). 

#### Submission

Look for the submission link on Moodle for the report. 
