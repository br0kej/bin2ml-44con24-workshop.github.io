---
section_id: Pre-Reqs
nav_order: 2
title: Workshop Materials
topics: Pre-reqs, Preperation
---

Now that we have gone over the necessary background for the workshop, it's now time to get all of the required *stuff* to actually do the workshop.

The workshop materials can be found on [GitHub here](https://github.com/br0kej/44con-bin2ml-workshop-material). 

# Local Setup steps
```
# Pull repository
git clone https://github.com/br0kej/44con-bin2ml-workshop-material.git

# Navigate into repo
cd 44con-bin2ml-workshop-material

# Execute setup.sh
./setup.sh

# Download data manually by clicking the link
# https://drive.google.com/file/d/1dtM10-UHaG9IIAJ6KrZL8lCyHH-saZlZ/view?usp=share_link

# Extract into data/
unzip data.zip -d data/
```

# Docker based setup

If you would rather run all of this within a Docker container, you can do this by first cloning the repository and manually downloading the data. Once both of these steps have been done,
you can then mount both of them into a *nix container such as Ubuntu. You will have to also installing the rust toolchain before then executing the `setup.sh` - It should work just fine!
