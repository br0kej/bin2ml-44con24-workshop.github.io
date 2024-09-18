---
section: Data Processing
nav_order: 3
title: extract with bin2ml
topics: Data Processing, Raw to Intermediate
---
We have a pile of binaries ready to get processing! Before we do so, it's worth 
briefly explaining how `bin2ml` approaches data generation. 

# Design Decisions 

## Re-usable Data Stages

One of the fundamental design decisions of `bin2ml` was to make it possible to `extract` a certain type 
of data from a software binary and then re-use that `extract`'d data to generate multiple downstream data
types. 

In order to generate the ACFG's like the ones used in `Gemini`, we need to `extract` the `cfg` data. Under the hood,
this uses the `radare2` command `agfj` command.

## Data Parallelism

In addition to the re-usable data stages design decision, another design decision was to implement as much of the
data processing in a manner which could be parallelised using a thread pool (thank you `rayon`!) wherever possible. 
This applies to all `extract` and `generate` stages as well as most of the other functionality provided by `bin2ml`. 

# Extracting the `cfg` raw data from the binaries

{% capture text %}
If this stage takes a very long time on your hardware, this has already been extracted and can be found within `training/intermediate`. 
{% endcapture %}
{% include alert.html text=text color=secondary %}

Execute the following commands to start the `cfg` data extraction:

```
cd <path>/<to>/44con-workshop-materials
mkdir data/training/intermediate-extract
bin2ml extract -f data/training/binaries -o data/training/intermediate-extract -m cfg -n 4
```

# Tasks

Open up one of the (smaller) JSON files and think about:

- What information is provided for each function? 
- What information would be useful to construct a control flow graph?
- What other down-stream data types could you use this intermediate ata to create?
