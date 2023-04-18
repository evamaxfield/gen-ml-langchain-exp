# Summarization

This review pulls from:

* [HuggingFace Transformers Summarization Notes](https://huggingface.co/course/chapter7/5)
* [Long Text Summarization](https://www.width.ai/post/4-long-text-summarization-methods)
* [Papers from Papers With Code](https://paperswithcode.com/task/text-summarization)

## Metrics

* ROUGE -- based on shared subsequent tokens between the produced sequence and the original document.
    * "Overlap between the produced sequence and the 'correct' sequence".
* BLEU (less common now) -- comes from translation. A number between 0 and 1 that measures the similarity of the machine-translated text to a set of high quality reference translations. In the case of summarization, this can mean: "similarity between machine-summarization text to a set of high quality reference summarizations."

## Abstractive Summarization

Generating short, consise summaries that capture the ideas of the source text. The summary can include new words and phrases that were not in the source.

## Extractive Summarization

Given a document, select the subset of words or sentences which best represents a summary of the document.

## Typical Datasets

Pairs of Input Text & "True" Summarization (potentially many)

### Of Interest

[Align and Attend: Multimodal Summarization with Dual Contrastive Losses](https://arxiv.org/pdf/2303.07284v1.pdf)

Multimodel model for video and text to produce a summarized video in addition to the summarized text (using features from both).

[MemSum: Extractive Summarization of Long Documents Using Multi-Step Episodic Markov Decision Processed](https://aclanthology.org/2022.acl-long.450.pdf)

Idea: iteratively select sentences into the summary, taking into account the text content of the sentence, the global context of the rest of the document, the extraction history. Use ROUGE (R-1, R-2, and R-L) to compare against both abstractive and extractive summarization models.

## LangChain

[LangChain](https://python.langchain.com/en/latest/use_cases/summarization.html) has a "summarization" chain.

It works with a map reduce mechanism: split the text into chunks that are max size for embedding, summarize each chunk, then summarize the summaries. Somewhat expensive compared to the MemSum idea from before but it works and can additionally add prompts.

This is also an approach taken by OpenAI with their [Summarizing Book with Human Feedback](https://openai.com/research/summarizing-books).

> Our best model is fine-tuned from GPT-3 and generates sensible summaries of entire books, sometimes even matching the average quality of human-written summaries: it achieves a 6/7 rating (similar to the average human-written summary) from humans who have read the book 5% of the time and a 5/7 rating 15% of the time. Our model also achieves state-of-the-art results on the BookSum dataset for book-length summarization. A zero-shot question-answering model can use our model’s summaries to obtain competitive results on the NarrativeQA dataset for book-length question answering.

## Potential Ideas

* Obvious: Full meeting transcript summarization
* Prompted summarization:
    * "Summarize public commenters input" -- will it ignore the rest of the meeting?
    * "Summarize each of the council bills in the meeting and their voting results"?
    * More generally, can we guide the summarization model to summarize subsections of interest.
    * Summarize this meeting but focus on disagreement.
    * Summarize this for X audience.