---
section: Data Processing
nav_order: 3
title: generate with bin2ml
topics: Data Processing, Intermediate to Processed
---
Phew, we've done all of the heavy lifting as part of the `extract` command and now it's time to move 
onto generating some real data from this pile of intermediate JSON.

When generating Attributed Control Flow Graphs, `bin2ml` loads the intermediate JSON, creates the graph
structure, processes the node features and then merges the two together into a `networkx` compatible
JSON object.

{% capture text %}
If you are thinking "WTF is `networkx`?" - It's the most popular graph library for python. It has 
the ability to load and save graphs to/from JSON. In addition, due to its popularity, lots of 
other libraries such as `pytorch_geometric` (the GNN library we are going to use), provide functionality
to convert networkx `Graph` python objects into the format the library expects. 
{% endcapture %}
{% include alert.html text=text color=secondary %}

# `generate` graphs with Gemini nodes features

The following command can be used to generate the graphs:

```
bin2ml generate graphs \
    -p data/training/intermediate-extract/ \
    -o data/training/processed-output \
    -f gemini \
    -n 2 \
    --data-type cfg
```

This should be fairly rapid at generating the control flow graphs. Once complete, within the `data-processed` directory,
you will have a directory for each of the binaries processed. The binary specific directories will contain a networkx compitable
JSON file containing the ACFG for each of the functions within the binary.

## Example Graph

`x86-gcc-9-Os_minigzip_cfg-sym.gzfread.json`

```
{
   "adjacency":[
      [
         {
            "id":2,
            "weight":2
         },
         {
            "id":1,
            "weight":1
         }
      ],
      [
         
      ],
      [
         {
            "id":3,
            "weight":2
         },
         {
            "id":1,
            "weight":1
         }
      ],
      [
         {
            "id":5,
            "weight":2
         },
         {
            "id":4,
            "weight":1
         }
      ],
      [
         {
            "id":6,
            "weight":2
         },
         {
            "id":1,
            "weight":1
         }
      ],
      [
         {
            "id":4,
            "weight":2
         },
         {
            "id":1,
            "weight":1
         }
      ],
      [
         {
            "id":8,
            "weight":2
         },
         {
            "id":7,
            "weight":1
         }
      ],
      [
         {
            "id":9,
            "weight":2
         },
         {
            "id":1,
            "weight":1
         }
      ],
      [
         {
            "id":1,
            "weight":1
         }
      ],
      [
         {
            "id":1,
            "weight":1
         }
      ]
   ],
   "directed":"True",
   "graph":[
      
   ],
   "multigraph":false,
   "nodes":[
      {
         "id":0,
         "numCalls":1.0,
         "numTransfer":7.0,
         "numArith":2.0,
         "numIns":13.0,
         "numericConsts":2.0,
         "stringConsts":0.0,
         "numOffspring":2.0
      },
      {
         "id":1,
         "numCalls":0.0,
         "numTransfer":2.0,
         "numArith":0.0,
         "numIns":7.0,
         "numericConsts":0.0,
         "stringConsts":0.0,
         "numOffspring":2.0
      },
      {
         "id":2,
         "numCalls":0.0,
         "numTransfer":0.0,
         "numArith":0.0,
         "numIns":2.0,
         "numericConsts":1.0,
         "stringConsts":0.0,
         "numOffspring":2.0
      },
      {
         "id":3,
         "numCalls":0.0,
         "numTransfer":1.0,
         "numArith":0.0,
         "numIns":3.0,
         "numericConsts":0.0,
         "stringConsts":0.0,
         "numOffspring":2.0
      },
      {
         "id":4,
         "numCalls":0.0,
         "numTransfer":0.0,
         "numArith":0.0,
         "numIns":3.0,
         "numericConsts":0.0,
         "stringConsts":0.0,
         "numOffspring":2.0
      },
      {
         "id":5,
         "numCalls":0.0,
         "numTransfer":2.0,
         "numArith":2.0,
         "numIns":7.0,
         "numericConsts":0.0,
         "stringConsts":0.0,
         "numOffspring":2.0
      },
      {
         "id":6,
         "numCalls":0.0,
         "numTransfer":0.0,
         "numArith":0.0,
         "numIns":2.0,
         "numericConsts":0.0,
         "stringConsts":0.0,
         "numOffspring":2.0
      },
      {
         "id":7,
         "numCalls":1.0,
         "numTransfer":3.0,
         "numArith":1.0,
         "numIns":6.0,
         "numericConsts":0.0,
         "stringConsts":0.0,
         "numOffspring":2.0
      },
      {
         "id":8,
         "numCalls":1.0,
         "numTransfer":5.0,
         "numArith":1.0,
         "numIns":9.0,
         "numericConsts":1.0,
         "stringConsts":0.0,
         "numOffspring":2.0
      },
      {
         "id":9,
         "numCalls":0.0,
         "numTransfer":0.0,
         "numArith":0.0,
         "numIns":2.0,
         "numericConsts":1.0,
         "stringConsts":0.0,
         "numOffspring":2.0
      }
   ]
}
```

The eagle eyed of you may have noticed that the nodes do not have `between-ness`, one of the eight GEMINI features. We'll resolve this
using the `networkx` in-built `node betweenness` function when preparing the data before loading it into `pytorch geometric` soon!

# Tasks

If you attended the presentation earlier, you would have noticed that the `cfg` data type we extracted in the previous stage can be used 
for a lot more than just generating ACFG's. Experiment with the different `bin2ml` options!