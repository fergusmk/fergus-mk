---
layout: post
title: Data-efficient Technical Text Classification
description: Classifying technical road maintenance texts with many classes using very few examples
---
A research project about using very few training examples to prepare a technical text classifier for a complex application.

Motivation
============
A very common issue facing machine learning practitionists is data scarcity. This is amplified in domain-specific applications like road maintenance, where general pre-training (as used in pre-trained models like LLMs) struggle to adapt to.

> There is not enough data -says everyone

Now, getting more data is one way of doing it. But let's face it, many domain-specific data are privately owned, and even if they are accessible, they are probably not well labelled for your task.

Instead, I decided to tackle it in a different angle, making the models more data-efficient.

Research activities
============
### Data Collection ###

I collected data from [New York City Open Data](https://opendata.cityofnewyork.us), using a database for [road code violations](https://data.cityofnewyork.us/Transportation/Street-Construction-Inspections-and-Corrective-Act/ydkf-mpxb/about_data). It comprises of inspection records produced by city inspectors on code violations during roadworks by non-government third parties. Each row has a violated code classification and a free text field detailing the violation.

The dataset was then cleaned:
    1. Many rows don't have textual descriptions or violation classification
    2. There were character encoding errors where instances of the same class would appear as separate classes
    3. Some classes contain duplicating contents which required manual merging
    4. Some classes have very few examples which might affect the interpretability of evaluation results, so those with fewer than 100 examples were removed.

The final dataset contained over 400,000 entries for 83 classes. Other than the technical nature of the texts used, the large number of classes pose a signifcant challenge to traditional instruction-tuning based LLMs.

Here are a some examples of the dataset:

I OBSERVED DEBRIS (COLD PATCH) BELONGING TO THE ABOVE RESPONDENT OBSTRUCTING ROADWAY GUTTERS. SITE UN ATTENDED. LOCATED OPPOSITE 265 23RD ST. If not admitting the charge, you MUST APPEAR IN PERSON. ----------> Debris/construction materials obstructing gutters/sidewalk, etc.   
          |
Bubbled pedestrian warning devise not install on ped ramp as required by DOT specs. ----------> Except as in NYC Administrative Code 19-152, failure to install pedestrian ramp as per DOT drawings


Novelty
============
Most LLM-based classifiers rely on instruction-tuning, where you use a chat-format to ask the model to output a classificaiton. However, this becomes impractical as the number of classes increases since you need to fit all class definitions and exmaples into a single prompt. With 83 classes in this case, the context length blows up. I decided not to do this...

An alternative is using an embedding-based model, more akin to traditional deep learning. However, instead of using a traditional classification head, I used cosine similarity to produce logits. But also unlike traditinal similarity-based fine-tuning, I used the cross entropy loss instead of contrastive loss, effectively linking the task with the classification function. 

A key characteristic of the proposed similarity-based classifier is that there is no uninitialized parameters, meaning that the model can in theory work without any training. Practically, it means that the model can adapt to a task much more quickly, thus combining the rapid adaptability of instruction-based models with the scalability of embedding-based models, all while being able to use Sentence Transformers which are up to around 70 times smaller than baseline SOTA LLMs like Llama3. 

This is an illustration of the classifier and fine-tuning regime:
![Proposed classifier and cross entropy fine-tuning](/assets/images/cross_entropy_tuning.jpg "Proposed classifier and cross entropy fine-tuning")


Results
============
The results show that the propsoed similarity-based classifier not only outperforms standard BERT models using classification heads, it also outperforms much bigger (30 times) LLMs!

![Proposed classifier vs 7B LLMs](/assets/images/baseline_comparison_llm.pdf "Proposed classifier vs 7B LLMs")


Here is a visualization of the embedding space (t-SNE down from 768 dimension), where each colour represents a class and the corresponding crosses represent the embedding of the textual class definitions:
![t-SNE plot of embedding space](/assets/images/bi-enc_tsne_plot_65.jpg "t-SNE plot of embedding space")


You can read more about this work [here](https://www.sciencedirect.com/science/article/pii/S1474034625004021).

