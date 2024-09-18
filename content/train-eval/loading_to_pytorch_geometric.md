---
section_id: Train and Eval
nav_order: 4
title: Data to PyTorch Geometric
topics: Data Loading, Training Prep
---
{% include figure.html img="have_a_break.jpeg" alt="A meme of Leonardo DiCaprio holding a drink with the text Have a break, you made it this far" width="75%" %}

# Back too it!

It's now time to open up the first lab within the `labs` folder called `01_prepare_data.ipynb`. The lab is in the format of a `jupyter notebook`. During the prerequisites, a python `venv` 
should have been created within the `44con-workshop-material/py` folder. Make sure this is activated and if it's not, activate it using the `source py/venv/bin/activate` command.

{% capture text %}
Most of the dependencies are fairly lightweight apart from `pytorch` and `pytorch_geometric` + it's associated
stuff. These are monsters!

Note: The `cpu` versions of each are installed as part of the `pyproject.toml` - The GPU versions will work with
the code provided but are not installed.
{% endcapture %}
{% include alert.html text=text color=secondary %}

# What is this lab?

This lab is focused on converting the `networkx` JSON objects outputted by `bin2ml` into `pytorch geometric` `Data` objects. A single `Data` object represents a single graph, in our case, a single
functions attributed CFG. The notebook (and the python module it imports) does this process for us before then saving it as a Python Pickle object ready to be loaded later for training. 

# Complete the lab
Open the notebook within Visual Studio Code, your choice of IDE or within jupyter lab and follow the steps within it.

# Tasks

Check out the code that is used within this notebook

