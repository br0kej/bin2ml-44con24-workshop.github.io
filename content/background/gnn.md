---
section_id: Background
nav_order: 2
title: GNNs at the speed of light
topics: Graph Neural Networks, Graphs
---

Graph Neural Networks (GNNs) are a powerful class of machine learning algorithm which operate exclusive on graphs represented as a collection of nodes and edges (aka vertices). This combination
of nodes and edges can represent a wide range of things whether that be nodes representing people and edges representing the relationships between those people or alternatively the nodes could 
represent basic blocks within a function-level control flow graph and nodes representing the jump and fallthrough paths between basic blocks. The possibilities are really limited by your imagination!

Formally, graphs come in a wide range of types such as undirected or directed as well as many variations of these depending on if extra information is added to the graph such as giving edges a single 
numerical value, usually referred to as a weight (resulting in a weighted undirected/directed graph) or a set of attributes/features to nodes (resulting in an attributed *insert other stuff* graph). 

Regardless of the type of graph used as the input to a graph neural network, the secret sauce is essentially to exploit the structure of the graph itself to create powerful *representations* for 
the task at hand. This means a graph neural network does not *change* the underlying graph structure (such as add or remove people to our social network graph or change the fall-through
target in the control flow graph) but instead uses its structure to aggregate information across the graph.

# Different GNN Tasks

For the purposes of this workshop, we are going to be focusing solely on what is known as *Whole Graph Embeddings* whereby we want to create a representation of a whole graph that is 
suitable for comparing it against many other graphs (which also have representations). I had included an additional reading page titled [Graph Neural Network Task Types](../additional-reading/gnn_task_types.html) 
that explores some other examples and should help with getting your own problems formulated into machine learning problems. 

# Message Passing Graph Neural Networks

The focus of this workshop is focused on GNN's but formally, only covers on what are known as Message Passing GNN's. Message passing GNN's are the probably the most popular way of doing ML on graphs 
with a large body of research. They work by passing messages between the nodes within the graph iteratively. The messages are usually either node features, edge features or both. To keep it simple,
we will only be using node features. The gif below demonstrates this for a very simple graph and one node feature update (If the gif is not playing, refresh the page!).

{% include figure.html img="msg_passing.gif" onclick="this.src='msg_passing.gif'" alt="A gif showing the message passing operation for a single node in a 3 node graph. The aggregation is done using a *SUM* aggregation function" width="75%" %}

As previously mentioned the gif above shows one update for a single node, node A. From watching the gif, you will have noticed that the floating point numbers from Nodes *B* and *C* are iteratively 
sent to Node *A*. Once all of them are received, the values are then combined using an aggregation function (denoted as *AGG* in the GIF). In this case, the *SUM* aggregation function is used 
to combine the original value of *A* with the messages (i.e values) from *B* and *C*. This results in the new value of -9.2 for the node. 

I hope this provides you with an intitution why this may be useful. By passing messages between nodes by using the structure of the graph, the idea is that the representation of any given node incorporates, and is aware of, it's neighboring nodes.

# Representation Learning
You are probably now wondering what the hell is a *representation*? It is also commonly referred to as an embedding. It's basically a list of floating point numbers whereby the *size* or *dimension* of the representation/embedding corresponds to the number of floating point numbers within the list. This list of floating point numbers represents the inputs position in high-dimensional space which is referred to as the *embedding space* or *latent space*. 

Luckily for us, we don't really need to visualise this Doctor Strange level wizardry but instead we can use mathematical distances to answer the question of *Is A graph similar to (close to) B graph?*.
Distance functions such as *L2 Distance* or *Cosine Distance* provide a means of comparing two representations against each other. The output of this operation is a value between 0 and 1 and gives 
you an idea if two things are similar or dissimilar. 



