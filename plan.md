# Experiment Plan for Summarization

## Problem

Transcripts aren't enough to get people to stay up-to-date on what is happening directly in council meetings. We have had transcripts for a long time. I don't read them that often unless I am specifically looking for something and I assume many others use them in the same way: only using them when looking for a specific thing.

## Potential Solution

We want to explore summarization techniques as a potential solution for making each council meeting (and more general) council activity more easily digestable.

This has been proposed by others (and ourselves) but we would like a method to measure the effectiveness of such an approach, and potentially a few different implementations.

### Potential Implementations

#### "Read the Abstract"

The "simpliest" form of summarization. Given all of the text of the meeting, create an abstractive summary of what happened. This can be a paragraph of two.

#### "The Axios Model"

At the moment, I read Axios most frequently. There model definitely hides a lot of detail and nuance from the reader but I like it to get the high level overview of something that if I am interested in further I can then go to AP or NPR or something else to get more details.

I view this model as much more challenging to create but we could start with a simplified version of it that goes something like the following:

* few sentence abstractive summary intro
* extractive summary and quote(s) about the topics mentioned in the abstract
* details:
    * pull from prior meeting summaries which reference the same legislative matters (or semantically similar?)

I think this may be possible because we can prompt the summarization model. I.e.:

* "Keep the abstractive summary shorter than 5 sentences."
* "Pull a few quotes from the meeting that are most representative of the topics mentioned."
* "Create a summary of how this prior meeting affected this current meetings discussion."

Even those prompts may be too simplistic. There is a possibility that we can provide a whole Axios article or at least the structure as laid out above in the prompt and have the model figure it out.

If the user wants more detail they can read the full transcript of this same meeting or of the prior referenced meetings.

#### All the Data

What I don't think we will explore right now is the "all the data" model that we talked to Matt and Dave about. This would include the voting records, minutes item text, and so on. We may pull in elements of those things but definitely not all of it due to the timeline of the quarter and how much time we have left.

## Background and Literature Review

### Original OpenAI Paper on Map-Reduce Summarization on Books

**[Paper](https://arxiv.org/pdf/2109.10862.pdf)**

* "recursive task decomposition"
* fine-tuned a model on the smaller tasks
    * i.e. given a page of text, ask a human to summarize it
    * fine-tune on these page-sized inputs and summary outputs
* eval method
    * take 40 most popular books published in 2020
    * assign two labelers to read each book and write a summary of the book
    * ask the labelers to rate summaries from various models and from the other labeler
    * measure agreement between labelers on the model-written summary quality
* results
    * distribution of likert scores on quality of summary
    * note that on average model-generated summaries are still worse than human-written summaries
    * likert scales decrease as you climb the levels of decomposition (garbage in, worse garbage out)
* also tested summaries for question answering -- comparing accuracy of results when asking the summary vs asking the whole document
* this method lacks coherence -- while they include a lot of important information, they slowly become a list of events.

### Other Map-Reduce Summarization

* [https://aclanthology.org/2022.creativesumm-1.3.pdf](https://aclanthology.org/2022.creativesumm-1.3.pdf)
* [https://aclanthology.org/2022.acl-long.118.pdf](https://aclanthology.org/2022.acl-long.118.pdf)
   * Fine-tuned SOTA model on government reports + meetings
   * Best model checkpoints are available

TODO:
* Read more into prompted summarization
* Try to find meeting summarization papers with user interviews
* Try to find any papers on city council meeting summarization
* Try to find any papers on Axios' writing style
* Look into reddit auto tldr bot
* Review the BOBA user interview study

## Experiment Setup

TODO:
* Find community members and journalists
    * Some community members should have very little engagement with city council
    * Some community members should have high engagement with city council

* Create two summary implementations for a specific meeting that some of the selected individuals will have attended, listened to, watched, etc.

* Interview:
    * Ask everyone first:
        * How do you stay up-to-date on council actions currently?

    * Then for each summary implementation ask the following (random order the implementations):
        * For the people who do follow city council / attended / watched:
            * "Is this a fair representation of what happened in meeting?"
        * For people who do not follow city council / didn't attend / watch:
            * "Do you feel more up-to-date on the city council meeting from today / yesterday?"
        * For everyone:
            * "What do you like about this summary?"
            * "What do you dislike about this summary?"

    * After both:
        * Which summary did you like more and why?
        * Would a tool that generates either of these summaries for every meeting be useful to you in staying up to date on council and if so, how would you like to find these summaries (i.e. notifications, website, etc.).
        * Any final comments?

* Analysis
    * Which summary do people like more?
    * For those that follow the council: was the summary a fair representation of what happened?
    * Would a tool for this be useful?
    * Qualitative reviews of interview responses?
       * Possible things to change?

## Timeline

Note: Roughly three to four hours of work a week

### April 23 - April 29

* **1 hour** - Discussion of this plan and resolving possible changes.
* **1 hour** - Start working on getting a small dataset created for testing. Twenty meetings just for testing purposes.
* **1 hour** - Getting setup for summarization, quickstart, and learning.

### April 30 - May 6

* **2.5 hours** - Function to generate a first summarization implementation and examples of summaries from the twenty meetings.
    * These examples are for us for debugging and reference purposes not for the interviews.
* **1.5 hours** - Starting plan for user interviews.

### May 7 - May 13

* **2.5 hours** - Function to generate a second summarization implementation and examples of summaries from the twenty meetings.
   * These examples are for us for debugging and reference purposes not for the interviews.
* **1.5 hours** - Completed draft of user interview plan. All structure, questions, and format decided.
* **0.5 hours** - Start contacting people for potential interviews.
   * Four community members
       * Activists okay
   * Four journalists
   * No requirement for individuals to be planning to attend the upcoming meeting.
       * Selection of individuals should include some that hopefully do end up going to / listening / watching the meeting.

### May 14 - May 20

* Eva on vacation
* **1 hour** - Schedule all interviews.

### May 21 - May 27

* Eva on vacation until May 23.
* **2.5 hours** - Further development of summarization implementations (fixes, features, etc.).
* **1.5 hours** - Final user interview plan.
    * Mock interview?

### May 28 - June 3

* **0.5 hours** - Generate meeting summaries for latest meeting.
* **4 hours** - User iterviews.

### June 4 - June 10

* **1 hour** - Summarize user interview notes.
* **3 hours** - Write up project into short paper.
    * Abstract
    * Introduction
    * Background and Lit Review
    * Method
    * Results
    * Conclusion
