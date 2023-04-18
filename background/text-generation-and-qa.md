# Text Generation and Question Answering

This review pulls from:

* [HuggingFace Transformers Question Answering Notes](https://huggingface.co/course/chapter7/7)
* [Metrics to Evaluate a Question Answering System](https://www.deepset.ai/blog/metrics-to-evaluate-a-question-answering-system)
* [Papers from Papers With Code](https://paperswithcode.com/task/text-summarization)
* [Question Answering LangChain](https://python.langchain.com/en/latest/use_cases/question_answering.html)

Extracting an answer from given documents. Given "Context" (the documents you want to search) and a question.
The answer is NOT generated but extracted (usually -- there are other forms too similar to abstractive vs extractive summarization).

In recent times, it seems like many of these models are multi-modal -- i.e. "what is in this picture" which a visual question answering model that is more abstractive. I am assuming we will focus on document QA because most of our data is transcript data but it may be interesting to pull in other forms.

## Metrics

* Exact Match -- like the name, it looks for a literal exact match between prediction and true answer making it a binary (0 or 1 value).
* F1 Score -- word overlap between the labeled and the predicted answer (true pos = number of shared tokens between pred and true, false pos = number of tokens in the pred excluding the shared tokens, false neg = number of tokens in the correct answer, excluding shared).

## Of Interest

[Demonstrate - Search - Predict](https://arxiv.org/pdf/2212.14024v2.pdf)

Breakdown a single question into larger parts and have two models interact (language model and retrieval model)

"How many storeys are in the castle David Gregogy inherited?"

Language Model: "Which castle did David Gregory inherit?"
Retrieval Model: "David ... inherited Kinnairdy Castle..."
Language Model: "How many storeys does Kinnairdy Castle have?"
Retrieval Model: "Kinnairdy Castle is a .... has five storeys."
Language Model: "Kinnairdy Castle has five storeys."

This also goes down the thread of asking a language model to do something, take its output and then say: "find and correct any errors" or "refine" and the output is generally a bit better.

[Exporing the State of the Art in Legal QA Systems](https://arxiv.org/pdf/2304.06623v2.pdf)

Survey of benchmark datasets for question-answering in the legal field and comprehensive list of LegalQA DL models.

Generally, Legal answers must be of higher quality and reliability. Legal QA Models can be specialized to their field. Laws and regulations change, different from more general QA and LM models which focus on general understanding.

## LangChain

The "Demonstrate - Search - Predict" pattern also seems to me like one of the foundational abilities of LangChain. Can kind of see that in their [ConstitutionalChain](https://python.langchain.com/en/latest/modules/chains/examples/constitutional_chain.html) example and [Getting Started](https://python.langchain.com/en/latest/modules/chains/getting_started.html).

* Examples of question answering with LangChain and with sources (citation): https://python.langchain.com/en/latest/use_cases/question_answering.html

## More Generally

In some of the HuggingFace documentation and in some of the papers I read, the idea that training your own language model and then fine-tuning it to your specific task is the best strategy. I don't know if we want to do that but we could get "better" word embeddings by training our own masked LM.

Different path, is the idea of Teacher-Student training, where you use the inputs and outputs from a very large language model and train your own using those inputs and outputs.