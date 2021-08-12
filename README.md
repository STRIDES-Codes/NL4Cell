# NL4Cell: Integrating NLP with single cell data analysis
[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/drive/1z0N8pN04WOuvCxl9lK2nArOafS6X6hpf?usp=sharing)

![NL4Cell](./images/banner.png)
## What is NL4Cell?
NL4Cell is a modified natural language processing model that has learned the language of genes. This pretrained model can be applied towards any number of tasks pertaining to single cell RNA expression data.

## Background
<details>
<summary>Click for information on why this project exists!</summary>
  

### Natural Language Processing
Natural language processing (NLP) has taken the world by storm. In NLP, the objective is to create artificial intelligence (AI) that is able to read and determine meaning behind language just as a human would. While this has led to some interesting linguistic applications, the technology behind language comprehension can be adapted to various domains including biological data.

Recently there has been a paradigm shift in how people train and use language models. Rather than creating and fully training a model for a singular task, large pretrained models have been created (e.g. BERT, GPT-3, etc.) that have a generalized fluency over language. Then individuals with specific aims can copy these pretrained models and "fine tune" them in order to make it more applicable to their specific tasks. For example, a team interested in medical record analysis can download a pretrained model which learned English from mining Wikipedia, and then they can fine tune the model on their smaller electronic health record database. The model's generalized knowledge of English gained from Wikipedia transfers over to a more specific task which helps combat overfitting and saves time on training. 

### Single Cell Sequencing
Single-cell cytometry allows us to view the protein expression profiles on an individual cellular basis. In short: we can look at *exactly* what proteins a cell is using an how much it is using them. This has revolutionized the way we can study biology by being able to describe the activities and inner-workings of cells in an extremely high-resolution.

There are too many applications of cytometry to enumerate here (futher complicated by how rapidly the field is developing), but there numerous tasks and applications which allow us to gain valueable insight into how both healthy and diseased cells operate spanning applications from embrology to cancer to diabetes.

### What do they have to do with each other?
So what does natural language processing have to do with single-cell data? 

Imagine you have a document. That document is comprised of words which have relationships to each other and together form the meaning for the document. There are combinations of words that make sense, and those that don't. For example we could say, "the mouse eats cheese," and the words come together in a way that makes sense syntactically and logically. On the contrary we can also say "the ladder eats cheese" which doesn't logically make sense-- a ladder and cheese don't typically go together. Language models are able to tell what makes sense and what doesn't by learning from example and gaining a general "understanding" of a language.

Now we can extend this concept to single cell data. Rather than a document comprised of words with lexical meaning, think about it in terms of a cell comprised of genes with biological meaning. We can reapply the same concepts from NLP to learn a new language, but rather than learning the meaning of words in a dictionary it learns the genes in a genome. Just as we could create a model that understands that "the mouse eats the cheese" makes more sense than "the ladder eats the cheese," we could create a model that can intuitively understand that a cell with `[CD4+, CD8-, CD20-]` makes a lot more sense than `[CD4+, CD8+, CD20+]`. This generalized understanding can then be applied towards any number of tasks just like one of the large pretrained models like GPT-3.

</details>

## Information

### Preprocessing

### Models
Several models, broadly divided into BERT-based and non-BERT-based models, were trained, with unique learning objectives and protocols for each model.
* BERT
    * Released by Google in 2018
    * Uses the original transformer architecture from "Attention is All You Need"
* ALBERT/DistillBERT
    * Released in 2019
    * A light/smaller version of BERT that retains much of the language understanding while increasing speed
* RoBERTa
    * Released in 2019 by Facebook
    * An extended version of BERT trained on 1000% more data, with modified learning objectives
* ELECTRA
    * Released in 2020 by Google and Stanford
    * Completely different learning objective, using corruption rather than masking
    * Improved performance with less computing resources by learning from all tokens, rather than a subset of masked tokens
All models were modified to remove positional embeddings, which are not needed for single cell data, as the sequence of gene tokens are not in any semantic order. In addition, the training objectives for BERT-based models were modified towards an ELECTRA-inspired adversarial model, randomly corrupting +/- values for a subset of gene markers to a neutral token, then predicting whether these tokens were + or -.


## How to use NL4Cell

### Installation

Before installing the project, we recommend you check out [the project on Google Collab](#Null)

Installing NL4Cell is very straightforward – the models used in NL4Cell can be installed as an extension of the HuggingFace ```transformers``` package using ```pip```, through the following command:
```
pip install git+https://github.com/justinphan3110/transformers.git
```

To use with Colab, include the following line of code before importing the various models:
```
!pip install git+https://github.com/justinphan3110/transformers.git
```

### Models and Classes
NL4Cell modifies the following model classes in the HuggingFace ```transformers``` package:
* ```BertModel```
* ```RobertaModel```
* ```AlbertModel```
* ```ElectraModel```

Along with these models, we recommend the use of our modified Tokenizer and Data Collaters, which can be imported with the following
```
from transformers.models.bert.tokenization_bert import CellBertTokenizer # This imports the custom tokenizer, which is an extension of the BERT Tokenizer
from transformers.data.data_collator import DataCollatorForNetutralCellModeling # This imports the custom Data Collater
```


### Example
```
This is where we will put a toy data example
```
For more examples of training and fine-tuning models included in NL4Cell, please reference the following notebooks
* [End-to-End Tutorial](https://github.com/STRIDES-Codes/NL4Cell/blob/main/tutorials/NL4Cell_Tutorial.ipynb)
* [Example: Training ALBERT](https://colab.research.google.com/drive/1N2hoGF6JqSN00tiYK7P3I8qqFuMNlkaK)
* [Example: Training ELECTRA](https://colab.research.google.com/drive/1tRtoqW6jof0z8rkCqV5gud54xSm7aocZ?usp=sharing)


## Team
**James Anibal** (Team Lead) \
Long Phan (Tech Lead) \
Runa Cheng \
Caitlin Corbin \
Caleb Grenko \
James Han \
Raina Kikani \
Zhichao Wu
