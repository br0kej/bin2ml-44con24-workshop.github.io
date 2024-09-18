---
section_id: Data Processing
nav_order: 3
title: Getting binaries
topics: Compiled Binaries, Raw Data
---

Now that you have got all the pre-reqs (such as the supporting code and binaries), it is now time to get generating some training data using `bin2ml`! 

In our case, this means we need a collection of compiled software binaries *with* debug information to 
process with `bin2ml`. You may be wondering why we need debug information to be present - We are going to
use the function names as labels.

{% capture text %}
If you think that using function names from the compiler generated debug information as labels
might not be the *best* idea. You may be onto something! Can you think of an alternative?
{% endcapture %}
{% include alert.html text=text color=secondary %}

To make this practical in the time we have together, we are going to use a subset of
the `Dataset-1` from another very good paper by [Marcelli et al (2022) from Cisco Talos](https://www.usenix.org/conference/usenixsecurity22/presentation/marcelli).  This dataset is a very good starter dataset with a large body of 
research adopting it to evaluate their proposed approaches. It's cross-architecture, cross-compiler, 
cross-optimisation *AND* includes multiple bitness (32 + 64) - basically everything you want to do research in this area! 

I have subset this dataset to only include `x86` and `arm32` binaries as well as removing `nmap`, `clamav` and `z3` from the dataset to make it easier and less resource intensive to process the data on all kinds of hardware.

You should already have this as part of the download you did for the pre-reqs. If you want to check the data out, you can do this by looking in `data/training/binaries`.