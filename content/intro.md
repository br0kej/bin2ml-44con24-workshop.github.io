---
nav_order: 1
title: Introduction
---
The focus of the workshop is to provide you with a guided walk-through on using `bin2ml`, an open source
tool that leverages `radare2` to generate machine learning ready data from software binaries.

## Overview

This workshop focuses on re-creating the seminal GEMINI model from raw binaries to trained model and will be structured as follows:

1. Background
    - Introduce the concept of what a graph neural network is and how they differ from other types of neural networks
    - Introduce the GEMINI approach, the data representation it uses and the features
    - Introduce `bin2ml` and it's general approach
2. Data Processing
   - Source Binaries
   - `extract` with `bin2ml`
   - `generate` with `bin2ml`
3. Data Loading and Training
   - Load data into `pytorch geometric` compatible objects
   - Initialise and Train the model
4. Evaluate the Model
   - What metrics to use?
   - Evaluate on Binary Code Similiarity Detection (BCSD) 
   - Evaluate on N-day vulnerability detection libcrypto from a TP-Link router
5. Where next?
6. Feedback and Close Down

## Main Objectives
- Provide attendees with hands on experience with bin2ml and demonstrate how easy it is to use
- Inspire machine learning (ML) people who may be skilled in ML but get stuck or do not understand how to transform raw data (in our case binaries) into data ready for ML to apply their skills to this area
- Lower the barrier of entry for non-ML people who may be interested in ML but need support with getting the data prepared to get training models and familiarise themselves with ML as a whole

## Requirements
You will need the following:

- a laptop
- docker installed
- rust tool chain 
- git
- about 50GB of space
- It would also be good to have an x86-64 SRE tool to check the binaries and explore how the binary ends up as a ml input.

{% capture text %}Note: If attending this workshop in person at 44con, we will have a bit of time at the start of the workshpp to set this stuff up!{% endcapture %}
{% include alert.html text=text color=secondary %}
