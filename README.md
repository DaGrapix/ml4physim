# Bi-Transformer & Packed-Ensemble Surrogate Models for Flow Estimation Arround Airfoil Geometries

This repository shows a different model strategies, based on Packed-Ensembles or Transformers for solving the RANS equations, based on the LIPS framework and the Airfrans Dataset.

The study provided here is part of the ML4physim challenge hosted by IRT-Systemx (see [Codabench page](https://www.codabench.org/competitions/1534/)).
CFD simulations being very costly, the use of data-driven surrogate models can be useful to optimize the shape of airfoils without paying the cost of expensive simulations.

Two families of models were implemented and tested here. 
- **Packed-ensemble models**, which are generalizations of Deep-ensembles that allow to lower the number of an Ensemble Method's parameters small. For Packed-Ensembles, two frameworks are proposed in the `packed_ensembles` folder:
    - A complete and independent framework developped in `ml4science.ipynb` with a custom training function and a cross validation selection implementation.
    - An implementation of the Packed-Ensemble model within the LIPS framework in `packed_lips.ipynb`. All the configurations that were tried are developed in the `config.ini` file.
- **Transformer models**, which have created a revolution in the sequence-to-sequence ML field (mainly in NLP). A modified version of transformer networks is proposed here, where for each simulations, the query tokens are only attended to a subsampled number of value tokens that have been sampled in the pointcloud of the simulation which we call the skeleton of the mesh. For Transformers, a bunch of architectures have been developed and reside in the `subsampled_bi_transformers` folder, and can be run using the `run.py` file.

The `megatron` bi-transformer model got us the best score and the $4^{\text{th}}$ place in the challenge!

---

## Installation

### Install the LIPS framework

#### Setup an Environment

```commandline
conda create --name ml4science python=3.9
```

##### Create a virtual environment

##### Enter virtual environment
```commandline
conda activate ml4science
```

#### Install from source
Download the LIPS repository in the `src` folder
```commandline
cd src
git clone https://github.com/IRT-SystemX/LIPS.git
```
Then remove the `numpy` and `scipy` requirement from the `setup.py` file to avoid conflicts.

```commandline
cd LIPS
pip install -U .
cd ..
```

### Install pytorch
Checkout https://pytorch.org/get-started/locally/

### Install the Airfrans library and install the datasets

#### Install the library
```sh
pip install airfrans
```

#### Download the dataset
```sh
import os
import airfrans as af

directory_name='Dataset'
if not os.path.isdir(directory_name):
    af.dataset.download(root = ".", file_name = directory_name, unzip = True, OpenFOAM = False)
```

### Install torch-uncertainty
```sh
pip install torch-uncertainty
```
