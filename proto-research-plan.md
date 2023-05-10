# Prototype Research Plan

## Definitions

* "paragraph" summary

What we typically refer to as the output of a summarization task. Sequences of sentences joined together into a single or multiple paragraphs. Typically, this is produced from an abstractive summarization model.

* "structured" summary

A document with multiple distinct but related parts. Produced with potentially many models but includes both abstractive and extractive portions and combines sequences of sentences and bullet point items.

## Hypotheses

H1. Readers will rate a summary's accuracy to the source document equal for both "paragraph" and "structured" text summaries.

H2. Readers will rate a summary's usefullness to the source document equal for both "paragraph" and "structured" text summaries.

H3. Readers will have the same rates of information retention for both "paragraph" and "structured" text summaries.

## General Assumptions and Reasoning

My general assumption here is simply on how I (and I assume many others) take notes for themselves.

I try to keep things in bullet point lists of different topics mentioned, with a descending tree of items if need be. And if I need to elaborate on something further, I write out more -- in the "abstractive" style of summarization models.

### H1 Accuracy

Aim: measure how "the structure / formatting of a summary" may affect a readers perceived accuracy of that summary compared to the source document.

### H2 Usefullness

Aim: measure how "the structure / formatting of a summary" may affect a readers perceive the usefullness of that summary.

This is a bit harder to do in an "experiment" -- as in many situations, the data we would be testing users with isn't directly related to what they themselves work on or care about. "Usefullness" is partly dependent on how much attention the user gives to this general research area (or the test documents we select).

That said, this is the question I am really interested in because it looks at whether the summaries that models are typically trained on are "useful" in the first place.

### H3 Retention

Aim: measure how "the structure / formatting of a summary" may affect a readers retention of that information.

A follow up for H1 and H2, if the "structured" summaries are more accuract and more useful (on initial viewing), do the readers retain more information? less information? etc.

## Lit Review

### Summarization Evaluation

Benchmarks are great and important but application matters.

#### [SummEval](https://arxiv.org/pdf/2007.12626.pdf)

* Large scale re-evaluation of summarization evaluation metrics
* Found multiple models (both extractive and abstract)
* Produced a list of "automatic" evaluation metrics
* Used the CNN/DailyMail dataset
* And further did human annotation of:
   * Coherence -- collective quality of all sentences

     "The summary should be well-structured and well-organized. The summary should not just be a heap of related information, but should build from sentence to sentence to a coherent body of information about a topic."

   * Consistency -- factual alignment between summary and source

     "A factually consistent summary contains only statements that are entailed by the source document. Annotators were also asked to penalize summaries that contained hallucinated facts."
    
   * Fluency -- quality of individual sentences

     "should have no formatting problems, capitalization errors or obviously ungrammatical sentences (e.g., fragments, missing components) that make the text difficult to read."
    
   * Relevance -- selection of important content from source

     "The summary should include only important information from the source document. Annotators were instructed to penalize summaries which contained redundancies and excess information"

* Pre-trained models scored highest on consistency and fluency while obtaining lower scores for relevance and coherence.
* Worth noting is also the fact that reference summaries did not score well on consistency, coherence, and relevance.
    * Upon examination of the annotations, we found that the reference summaries often contained extraneous information, such as hyperlinks and click-bait descriptions of other articles.
* Additionally, many reference summaries in the CNN/DailyMail dataset were constructed by naively concatenating bullet-point summaries into contiguous sequences. Such processing steps negatively affected the coherence of examples.

General comments:

* Really interesting work but I think this backs up what I am potentially interested in.
    * Why are summary datasets being concattenated in the first place. If the grouth truth / reference summaries are bullet points, leave them as bullet points. Structure matters.
    * Reference summaries include formatting more generally.

#### [Revisiting the Gold Standard](https://www.semanticscholar.org/reader/2bff7efafc7a07cc6c8402c595cb469bb90fea3d)

* Human eval is the gold standard BUT current benchmarks exhibit low rater agreement
* Introduce a new protocol called: "Atomic Content Units" (ACUs)
* With ACU's, annotator agreement increases
* Focused on: Salience -- a desired summary quality that requires the summary to include all and only important information of the input article.
* "The main goal of our ACU protocol is to reduce the subjectivity of reference-based summarization human evaluation"
* "More concretely, with the ACU protocol, the evaluation process is decomposed into two steps: (1) extracting facts from one text sequence, and (2) checking for the presence of the extracted facts in
another sequence."
* Generally, turning evaluation into a binary task

### Structured Summarization

#### [ECTSum](https://www.semanticscholar.org/reader/9c1f2985d9f2cc03f78c813b61641318bc794d0d)

* New dataset for "bullet point summarization" of long finacial call transcripts
* "What makes ECTSum truly different from others is the way summaries are written. Instead of containing well-formed sentences, the articles contain telegram-style bullet-points precisely capturing the important metrics discussed in the earnings calls."
* "Second, existing long document summarization datasets such as Arxiv/PubMed, BigPatent, FNS, and GovReport, have fixed document layouts. ECTs, on the other hand, are free-form documents with salient
information spread throughout the text (please refer Section 3.3). Hence, models can no longer take advantage of learning any stylistic signal."
* ECT-BPS consists of an extractive summarization module followed by a paraphrasing module.
* "While, the former is trained to identify salient sentences from the source ECT, the latter is trained to paraphrase ECT sentences to short abstractive telegram-style bullet-points that precisely capture the numerical values and facts discussed in the calls."
* "Hire a team of financial experts to manually assess and compare the summaries generated by ECT-BPS, and those of our strongest baseline. Overall, both automatic and manual evaluation results show ECT-BPS to outperform strong state-of-the-art baselines, which demonstrates the advantage of a simple approach."
* "All the unsupervised methods perform poorly, thereby highlighting the domain-specific nature of the ECT summarization task, and hence the need for supervised training."
* Human Eval:
    * Factual Correctness: For each summary sentence, the task was to asses if it can be supported by the source ECT.
    * Relevance: For each summary sentence, the task was to asses if it captures pertinent information relative to the ECT.
    * Coverage, the participants were instructed to assign a score to the overall summary (on a Likert scale of 1-5) based upon their impression about the amount/coverage of relevant content present in it.

General comments:

* This is REALLY close to what I am interested in. But from what I can tell, it is passing the extractive output into a paraphrasing module and not concattenating the two modules.
* They are targeting pure bullet point summaries rather than mixed formatting summaries.



## Design Tasks

Big piece to control is "how much text is generated", controlling for summary length to better understand how structure is directly affecting reader comprehension rather than just "long summaries".

## Measurement