---
section: Background
nav_order: 2
title: Gemini
topics: GEMINI, Graph Neural Networks
---

Throughout the rest of this workshop, we will be using the approach outlined within the seminal paper published by Xu et al (2018). The paper is available on [arxiv](https://arxiv.org/pdf/1708.06525) for download. The authors use a graph neural network method called Structure2Vec which has few up-to-date and working implementations. To overcome this, we are going to use an alternative GNN architecture 
using a simple 3-layer Graph Convolution Network (GCN) ([Kipf and Welling (2016)](https://arxiv.org/abs/1609.02907)).

{% include figure.html img="gemini_paper_screenshot.png" alt="A screenshot of the first page from the GEMINI paper titled Neural Network-based Graph Embedding for Cross-Platform Binary Code Similarity Detection" width="50%" %}

# Task at hand 

The task GEMINI is seeking to solve is cross-architecture function search which can be framed like the question below:

*Given an `arm32` implementation of `hello_world()`, are there any `hello_world()` like functions in this `mips32` binary?*

# Data Representation

One of the most interesting aspects of the GEMINI paper is the data representation they choose to use. Given that the task they are trying to solve is cross-architecture function search, they need
a suitable function level representation. They choose to use the [Control Flow Graph (CFG)](https://en.wikipedia.org/wiki/Control-flow_graph) of a function where each node within the graph is a basic block and the edges represent control transfer relationships.

{% include figure.html img="r2_cfg.png" alt="A screenshot of a simple 4 basic block control flow graph" width="50%" %}

In the screenshot above, green lines denote jumps when the jump condition is true and red lines denote jumps when the jump condition is false. Either have the concept of directionality - the code will jump from block A to block B if true or block C if false. This means that this graph is known as a *directed graph*. 

The question now is, "How to I change the contents of the basic block into something that is useable with a graph neural network?". This is something that is usually the most annoying and requires a fair
bit of thought. Formulating a high quality and flexible scheme is challenging! 

In GEMINI's case, they chose a very simple approach that performs surprisingly well! They process each basic blocks individually and generate a feature vector with 8 features - most of which are simply counts of features that perform particularly operations. 

{% include figure.html img="gemini_feature_vector_high_res.svg" alt="A picture of a feature vector containing eight features. Number of call instruction, number of transfer instructions, number of arithmetic instructions, total number of instructions, number of numeric constants, number of string constants, number of offspring and node between-ness" width="50%" %}

These categories of operations cover areas such as control flow operations (calls and transfers) as well as mathematical operations (arithmetic ops) which provide a rough idea of what the function does as well as higher level information such as how many string and numeric constants are used. These features provide a reasonable way of representing what happens *within* a basic block, but basic blocks do not operate in isolation! This is where the authors add two additional features to add information about where a basic block sits within the function as a whole. They achieve this by counting the number of offspring a basic block has as well as calculating the node between-ness. Between-ness is a graph theory metric which is usually used to identify criticality or bottlenecks within graphs (usually applied to computer networking tasks!). The authors use between-ness here to provide an indication of how important or critical a given basic block is within the function.

Once each of the basic for a given function has be processed, you end up with something that looks like the below CFG. (Whilst the structure of this CFG is the same as the screenshot, the values are 
completely made up!). Because we have now added what are known as feature vectors (lists of numbers) to the nodes, this can now be referred to as an *Attributed* Control Flow Graph or ACFG.

{% include figure.html img="acfg_example.svg" alt="A picture of a 4 node directed graph with feature vectors on each of the nodes - This is known as an Attributed Control Flow Graph (ACFG)" width="50%" %}
