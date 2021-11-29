
# Installation and Software

*You can complete all exercises in this textbook without having to install
any software on your own computer.* All you will need is a web-browser.
The exercises are hosted on a free cloud-based service called **Binder**, 
which allows you to access Jupyter notebooks running on a remote server 
with all required software pre-installed. You can find links to these 
notebooks in each chapter, and all links are also listed at the end of 
each chapter in the table of contents.

As an example, this link will connect you to a notebook from the 
Python bootcamp for learning how to use Jupyter:
[(:material-book:notebook-1.1-TODO)](...).


## Software used in this textbook

- Easy to install w/ conda.

- Simple/minimalist and stable. Example, we will not use custom class
objects from BioPython to parse a fasta file, but instead prefer basic
Python types to represent data in Dictionaries or arrays.

- Examples use Python to demonstrate algorithms using easy to read code. We
also show how to optimize many of these functions for speed. However, in most
cases published software tools have been optimized over many years and include
many more complex speed improvements. The code shown here is primarily for 
didactic purposes. We demonstrate examples using state-of-the-art software
as well, using fixed stable software versions updated periodically.



### Python
This textbook includes exercises in Python. Whenever possible we strive to 
use as few dependencies as possible, and to develop examples using the most
common libraries for scientific programing in Python. 

- Python Data Science:  
    - [Numpy](...): arrays, tensors, and numeric processing.  
    - [Pandas](...): tabular dataframes, statistical processing.  
    - [Scipy](...): statistical distributions.  
    - [Numba](...): just-in-time compilation for speed-optimized functions.  

- Visualization:  
    - [Toyplot](...): minimalist interactive vector-based plotting.

- Tree objects:  
    - [Toytree](...): tree-based operations and tree plotting using toyplot.  

- Coalescent simulations:  
    - [Ipcoal](...): coalescent simulation library integrated with toytree visualization.  
        - [Msprime](...): coalescent simulation backend for ipcoal.  
        - [Tskit](...): tree sequence class backend for msprime.  

- Machine learning:  
    - [scikit-learn](...): simple and well documented ...  
    - [Tensorflow](...):   
    - [Keras](...):  

### External binaries

In addition to custom Python code established external software tools are
also demonstrated in many exercises. When multiple options are available we
tend to select the tools that are easiest to install (e.g., using conda) 
and to use, and which do not require a graphical user interface.

- raxml
- iqtree
- mrbayes
- bpp
- ...


## Local Installation Instructions

If you want to follow along with the exercises in this textbook on your 
own computer, rather than use the cloud-based binder notebooks, you can do
so by installing the necessary software into a conda environment. This is 
easiest to do by first cloning the repository, and then installing from the
`environment.yml` file, like below.

To start you need a `conda`, a tool that is used for installing 
software from the command line. I recommend installing miniconda if you 
don't already have conda installed:

=== "Linux"
    ```bash
    # download the installation binary
    wget ...

    # call the binary in batch mode (installs miniconda/ to your $HOME)
    bash -b Miniconda...

    # call the init script
    ~/miniconda/condabin/conda-init
    ```
=== "OSX"
    ```bash
    # download the installation binary
    curl ...

    # call the binary in batch mode (installs miniconda/ to your $HOME)
    ...

    # call the init script
    ~/miniconda/condabin/conda-init    
    ```

??? tip "Tips on Miniconda"
    
    After running the commands above you will likely see a small change to
    the text that is shown before your cursor in your terminal. Perhaps it 
    shows something like `(base)`. This is telling you the name of the conda
    environment that you currently have loaded. An environment is simply a 
    subfolder within your `miniconda/` directory where software is stored.
    You can create multiple environments with different sets of software for
    different projects. If you just installed `conda` then your base environment
    will hardly have any software in it. Basically just the latest version of
    Python.

    Below we will create a new environment called `phylodatascience`....


Once you have conda installed, you can then use `git` to clone the repository
for this textbook which includes an `environment.yml` file with instructions 
for conda to install a new `phylodatascience` environment that will include 
all software and dependencies for this textbook.

```bash
# clone the repository and cd into it.
git clone https://github.com/eaton-lab/phylogenetic-data-science
cd phylogenetic-data-science/

# create new env and install all dependencies into it.
conda env create -f environment.yml

# you can now activate this software environment from any terminal w/
conda activate phylodatascience
```

