---
section_id: Extra Resources
nav_order: 6
title: Graph Neural Network Task Types
topics: Graph Neural Networks, Problem Formulation
---

# GNN Task Levels

There are three major level of GNN tasks; *Node-Level*, *Edge-Level* or *Graph-Level*. 

## Node-Level 

Node level tasks are usually either classification or representation generation. Both of these can be used to tackle the same problems but are subtly different. Let's demonstrate this different with the example of identifying whether function within a software binary is a Cryptographic operation. In the classification setup, the objective would be a binary classification problem (`IsCrypt` (1) or `NotCrypt` (0)) and would require a collection of labelled functions that are Cryptographic operations and those that are not. The output of such a model would again be binary - "I think this function
*is* a cryptographic operation" or "I think this function *is not* a cryptographic operation".

What happens if you want to answer a question which is subtly different such as "What functions are similar to this function?". This is where representation learning comes into play. Representation 
learning seeks to learn representations 

In representation generation, the aim of the task is to create a representation that provides a means of comparing 
a given node against many other nodes. An example of this would be the creation of a node representation for an individual within a social network
