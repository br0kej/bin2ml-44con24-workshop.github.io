---
section: Train and Eval
nav_order: 4
title: Ingredients for Training
topics: Model Training, Graph Neural Networks, Info
---

It's show time. We have done all of the leg work and now it's time to train your first Graph Neural Network (GNN). The type of graph neural network we are going to train is a 3-layer Graph Convolutional Network (GCN) from the ICLR paper by Kipf and Welling in 2017 titled ["Semi-Supervised Classification with Graph Convolutional Networks"](https://arxiv.org/abs/1609.02907). This is one of the seminal graph neural network approaches and is a great baseline approach!

{% include figure.html img="gcn_paper_screenshot.png" alt="A screenshot of the first page of Kipf and Welling 2017 titled Semi-Supervised Classification with Graph Convolutional Networks" width="75%" %}

Hold up though! A model and the training data is only part of the puzzle. We need a couple of other bits to make the magic happen.

## A way of telling our model if it's doing a good job 

As the model begins to process our training data, we need a method of calculating how well our model is doing. This is done by using what is known as a **loss function**. A loss function takes the outputs from our model alongside a label and then calculates the loss. An example of a loss function for a cat detection model could be 0 for a correct prediction and 1 for a negative prediction. Let's say 
the model predicts `[Cat, No Cat, No Cat]` when the true predictions should have been `[Cat, Cat, Cat]`, the loss function calculation would be `2`. If the model predicted `[Cat, No Cat, No Cat]`, the loss would be `0`.

The range of loss functions available is pretty daunting and something you can spend a lot of time experimenting with, but the fundamental idea shared by all loss function is that is provided a means of calculating how well the model is doing at a given time. If you do some further reading of this area, you will see "how well the model is doing" typically referred to as the models' error between predicted and true values - This is a bit more formal but to me at least, makes it a bit more difficult to conceptually understand.

## A way of updating the model using the loss

Knowing the model is doing terrible or well is not very useful unless it can be used to make the model better! This is where **optimizers** come into play. The role of the optimizer is to adjust the parameters (aka weights) of the neural network to *minimize* the loss function. Referring back to our cat detector example above - Adjusting the parameters of our model to get from `[Cat, Cat, Cat]` (a loss function value of 2) to `[Cat, No Cat, No Cat]` (a loss function value of 0). 

There are plenty of optimizers to experiment with and again this can be pretty daunting for folks. I personally have no explored and experimented with a large amount of optimizers but there are several go-to optimizers which show good general performance across a wide range of tasks. 

## What are we going to use?

### Circle Loss [(Sun et al 2020 - Paper)](https://arxiv.org/pdf/2002.10857)

For our loss function, we are going to use a loss function called `Circle Loss`. This loss function is what is known as a *Contrastive Loss* function which basically means we generate scores by comparing two examples together whereby the label is 1 for a pair of inputs that are *similar* and 0 for a pair of inputs that are *dissimilar*. The labels in our case are derived from the `<binary_name_function_name>` tuple.

{% capture text %}
To make this a bit more concrete, the function `hello_world` from `my_binary_O1` and `my_binary_O0` (the same binary but different optimisation level) would be labelled as `similiar` i.e `1`, but a pair made up of `hello_world` from `my_binary_O1` and `open_socket` from `foo_bar_O1` would be labelled as `dissimiliar` i.e `0`. 
{% endcapture %}
{% include alert.html text=text color=secondary %}

`Circle Loss` has been chosen because I have had good success with it during experimentation in the past. It does not mean it's the *best* choice, but it is definitely a *good* choice!

### Adam [(Kingma and Ba 2015 - Paper)](https://arxiv.org/pdf/1412.6980)

For our optimiser, we are going to use an optimizer called `Adam`. This optimizer is basically the defacto go-to optimizer and is used everywhere for loads of tasks! Rather than get bogged down in the details of Adam and optimisers as a whole, just remember, this is what changes our model using the output of our loss function!

