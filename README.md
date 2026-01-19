# Natural Language Processing (NLP) - an introduction<a name="top"/>
**A half day workshop on NLP with a non-expert, health domain focus.**

*Angus Roberts, King's College London Institute of Psychiatry, Psychology and Neuroscience*



## Contents

1. **Part 1 (1h30)**
    1. [Introduction](#introduction)
        - Motivation – why do we need NLP for health research and clinical care? 
        - What is NLP?
    1. [Representing language: documents](#representing-language-documents)
    1. [Representing words: vector semantics](#representing-words-vector-semantics)
1. **Part 2 (1h15)**
    1. [Playing with word embeddings](#playing-with-word-embeddings)
    1. [Supervised machine learning and classification](#classification)
    1. [Demo and real world use cases](#demo-and-real-world-use-cases)

## Introduction
[[back to top]](#top)

- This repository contains all the material you will need for the NLP half day
- The day will consist of six practicals to explore topics in NLP and neural networks
- Each practical will be introduced by short presentations of around 5 minutes each

**Python**

- Practicals will be in the Python programming language
- Don't worry if you don't know any Python, you do not need to write any code
- We will explain how to run the code, and talk you through each step
- We will run our Python code using Google Colaboratory (Colab), a cloud-based virtual compute service
- You will need a Gmail / Google account to use Colab
- If you do not have a Gmail account, [please create one now](https://support.google.com/mail/answer/56256?hl=en-GB) 

**Presentation**

- [Introductory presentation](./presentations/introduction.pdf) 

## Representing language: documents
[[back to top]](#top)

**Shakespeare's plays as vectors**
*Original idea from Jurafsky and Martin, [Speech and Language Processing](https://web.stanford.edu/~jurafsky/slp3/), Draft 3rd Edition.*

If we want to manipulate and analyse language computationally, we first need to find a way to represent language. We will start by looking at how we might represent documents. We are going to do a simple analysis of Shakespeare's plays, which are available in digital form from a USA library, the [Folger Shakespeare Library](https://www.folger.edu/explore/shakespeares-works/download/). We will look at the plain text of four plays:

- [As You Like It](https://flgr.sh/txtfssAYLtxt)
- [Twelfth Night](https://flgr.sh/txtfssTN_txt)
- [Julius Caesar](https://flgr.sh/txtfssJC_txt)
- [Henry V](https://flgr.sh/txtfssH5_txt)

**Practical**

- Each person will be allocated a play from the above list, and a word
- Count the number of times your word occurs in your play
- A simple way to do this is to use CTRL-F in your browser - this finds words in a page
- The dialog box in which you type the search word will tell you how many times that word occurs in the page
- Record your results in [this spreadsheet](https://docs.google.com/spreadsheets/d/1W-NI1-CAufuXTCHISsbwvnqY5krQVnsAxqX2IKpNcVg/edit?usp=sharing)

**Questions**

- *Wit* is also found in common words like *with* - how will you overcome this?
- Can we tell the difference between Shakespeare's comedies (e.g. As You Like It, Twelfth Night) and other plays?
- How might you represent a document?
- How might you visualise this?
- Can you think of any uses for this document representation?
- Can you think of a way to represent words?

**Presentation**

This presentation introduces a simple  model of documents based on the ideas from the above practical, called *Bag-of-Words*
- [Presentation: A simple model of documents: Bag-of-Words](./presentations/bag-of-words.pdf) 

## Representing words: vector semantics
[[back to top]](#top)

We've seen how to represent documents as vectors, but what about words themselves? 

**Presentation** 

This presentation introduces the idea of *distributional semantics*
- [Presentation: distributional semantics](./presentations/distributional-semantics.pdf) 

**Demonstration**

We will demonstrate the idea of using a word's context to create a vector representation of that word by using a linguistic search engine, [WebCorp](https://www.webcorp.org.uk/). WebCorp allows us to find and list all contexts on the web in which a word appears, and to count the number of times other words appear next to it. We call these the the word's collocates).
- [Demonstration: WebCorp](https://www.webcorp.org.uk/)

**Practical**

This practical builds word vectors using data from the [iWeb corpus](https://www.english-corpora.org/iweb/): a corpus of 14 billion words in 22 million systematically selected English language web pages. This can be searched and analysed using the tools at [English-Corpora.org](https://www.english-corpora.org/). We have used these tools to look at a few words, and to find what other words appear in their context. In this case, we define context as being on the same web page. We have saved the context counts in a spreadsheet, which has one sheet for each of our words:

- [Data: word contexts](./practicals/contexts.xlsx) (click the "View raw" button to download, tnen open on your computer)

You can use this spreadsheet with the Python notebook below to build and explore some word vectors:

- [Python notebook: vector semantics](https://githubtocolab.com/KCL-Health-NLP/nlp-half-day-workshop/blob/main/practicals/plot_contexts.ipynb)

## Playing with word embeddings
[[back to top]](#top)

The simple word and document vectors we built above can be used in NLP and information retrieval applications, but they have a few shortcomings, and better distributional semantics solutions exist: **word embeddings**. Whereas the vectors we have looked at so far are high dimensional with integer values, word embeddings are much lower dimensional (maybe a few hundred dimensions), with real number values. The most popular of these is Google's [Word2Vec](https://www.tensorflow.org/text/tutorials/word2vec) and Stanford University's [GloVe](https://nlp.stanford.edu/projects/glove/). We will use both of these in the practical below.

**Presentation**

This presentation gives a high level, intuitive overview of word embeddings. For more details, and information on how they are built, see the links above and Chapter 5 in [Jurafsky and Martin](https://web.stanford.edu/~jurafsky/slp3/)
- [Presentation: word embeddings](./presentations/word-embeddings.pdf) 

**Practical**

In this practical, you will create a word embedding from a small corpus and test it. It won't be very good! Then you will load an embedding that has been pre-trained on a much bigger corpus, to see the difference this makes.

- [Python notebook: word embeddings](https://githubtocolab.com/KCL-Health-NLP/nlp-half-day-workshop/blob/main/practicals/embeddings.ipynb)

## Classification
[[back to top]](#top)

Now that we have ways to represent language numerically, we can build models of our texts from these representations, and use the models when processing the texts. There are many NLP tasks we might carry out. For example, we might use the models to identify specific entites in the text, such as medications; we might use them to help answer questions put by a user; or to create summaries of the text.

We will look at one of the most widely used tasks, classification, in which we build models to assign one of several possible classes to a piece of text. This is a foundation of many other NLP techniques. Here are a few examples of how we might use classification:

- **Texts**: patient reviews of a service. **Classes**: the sentiment of the review, "positive" and "negative"
- **Texts**: sentences in a health record document. **Classes**: whether a sentence indicates that the patient is a smoker, "smoker", "non-smoker", "not stated".
- **Texts**: individual words in a health record document. **Classes**: whether the word is the name of a medication.

In each of these cases we can build a *supervised* model by providing training examples that have been pre-labelled with their classes (possibly by human labellers) to a classification algorithm. We can then apply this trained model to previously unseen texts, to predict the classes of those unseen texts.

**Presentation**

In this presentation, we will outline the basic idea of supervised machine learning for NLP.
- [Presentation: supervised machine learning for text classification](./presentations/classification.pdf) 

**Optional Demonstration Practical**

We will do a demo of this practoical if there is time and interest. In this practical, we will learn a model to assign medical specialties to health record documents. We will use texts from the publically available [MT Samples](https://mtsamples.com/) collection of medical transcriptions.
- [Python notebook: classification](https://githubtocolab.com/KCL-Health-NLP/nlp-half-day-workshop/blob/main/practicals/classification-short.ipynb)


## Demo and real world use cases
[[back to top]](#top)

We will finish with a demonstration of a medical NLP tool, and a presentation of some real world uses cases.

**Demonstration**

In this very simple demonstration we will take a look at a medical concept extraction tool, [MedCAT](https://github.com/CogStack/cogstack-nlp/blob/main/medcat-v2/README.md). MedCAT finds mentions of medical concepts in text and "annotates" i.e. labels them. It also links them to external medical terminologies.

The demo is a basic version of MedCAT using a publicly available model that links to a collection of medical terminologies curated by the USA National Library of Medicine, called the [Unified Medical Langusge System (UMLS)](https://www.nlm.nih.gov/research/umls/index.html). This includes ICD 10, as you will see in the demo. If you create a UMLS account, you can browse the identifiers that MedCAT assigns.

MedCAT is part of a larger health data extraction and transformation toolkit, [CogStack](https://github.com/CogStack/cogstack-nlp) whic is used by around 10 UK health service hospital services (NHS Trusts), and several others internationally. You can read more about MedCAT on the [website](https://github.com/CogStack/cogstack-nlp/blob/main/medcat-v2/README.md), and in this paper:

- *Kraljevic et al. Multi-domain clinical natural language processing with MedCAT: The Medical Concept Annotation Toolkit. Artif Intell Med. 2021 Jul;117:102083. doi: 10.1016/j.artmed.2021.102083. Epub 2021 May 1. PMID: 34127232.[https://doi.org/10.1016/j.artmed.2021.102083](https://doi.org/10.1016/j.artmed.2021.102083)*


- [Demonstration: MedCAT](https://medcat.sites.er.kcl.ac.uk/)


**Presentation**

This presentation gives just a few examples of NLP being developed and used at some London hospitals: [King's College Hospital](https://www.kch.nhs.uk/), [Guy's and St. Thomas'](https://www.guysandstthomas.nhs.uk/)

This is followed by a descriptin of an NLP service for mential health research, developed at the UK's [National Institute for Health Research's Maudsley Biomedical research Centre](https://www.maudsleybrc.nihr.ac.uk/) which is  hosted by a large psychiatric service, [South London and Maudsley NHS Foundation Trust](https://slam.nhs.uk/)

All of the applications have been developed by researchers at [King's College London](https://www.kcl.ac.uk/) in collaboration with clinical and informatics colleagues at these hospitals.

- [Presentation: some real world use cases](./presentations/use-cases.pdf)
