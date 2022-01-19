---
# template: 
icon: material/plus-circle
---

# Installation and Software


:material-star: ***You can complete all exercises in this textbook without installing
anything.***

That's right, all you really need is a web-browser. 
The exercises are hosted on a free cloud-based service called **MyBinder**, 
which allows you to access Jupyter notebooks running on a remote server 
with all required software pre-installed. You can find links to these 
notebooks in each chapter, and all links are also listed at the end of 
each chapter in the table of contents. As an example, the following link
connects you to a notebook from the Coding bootcamp on learning to 
use Jupyter: [(:material-notebook: jupyter-exercise.ipynb)](https://mybinder.org/v2/gh/eaton-lab/phylogenetic-data-science/HEAD?filepath=docs%2Fbootcamp%2Fnotebooks%2Fjupyter-intro.ipynb).

Nevertheless, you may wish to install the software dependencies 
and run code from the textbook exercises locally on your computer, which 
can provide a much greater opportunity for you to explore, modify, 
and learn about the code. Below I provide a brief summary of what 
this involves, and a link to our installation instructions.

## Software used in this textbook
This textbook aims to teach basic and advanced Python coding skills 
alongside lessons on phylogenetics with the goal of making complex
algorithms more easily understandable as a set of simpler step-by-step 
routines. This is a relatively difficult task, and obviously we cannot
cover all aspects of Python coding, phylogenetic theory, and phylogenetic 
software in this book. In general, decisions about which subjects to focus
on, how to write code, and which existing tools to highlight, uses the 
following guidelines:

- Coding style follows the ['Zen of Python'], which includes such 
enlightened ideas as "*Beautiful is better than ugly*", *"Simple is better 
than complex*", and "*Readability counts*".

  ['Zen of Python']: https://www.python.org/dev/peps/pep-0020/#id2

- All software and package versions are clearly shown and updated frequently.

- All demonstrated software is easy to install (specifically, using `conda`).

- ...

## Python libraries
Whenever possible we strive to use as few Python dependencies as possible, 
and to develop examples using the most common libraries for scientific 
programing in Python. Currently this includes the following:

- Python Data Science:  
    - [Numpy]: arrays, tensors, and numeric processing.  
    - [Pandas]: tabular dataframes, statistical processing.  
    - [Scipy]: statistical distributions.  
    - [Numba]: just-in-time compilation for speed-optimized functions.  
- Visualization:  
    - [Toyplot]: minimalist interactive vector-based plotting.
- Tree objects:  
    - [Toytree]: tree-based operations and tree plotting using toyplot.  
- Coalescent simulations:  
    - [Ipcoal]: coalescent simulation library integrated with toytree visualization.  
    - [Msprime]: coalescent simulation backend for ipcoal.  
    - [Tskit]: tree sequence class backend for msprime.  
- Machine learning:  
    - [scikit-learn]: simple and well documented machine learning code. 
    <!-- - [Tensorflow](...):    -->
    <!-- - [Keras](...):   -->

[Numpy]: https://numpy.org/
[Pandas]: https://pandas.pydata.org/
[Scipy]: https://scipy.org/
[Numba]: https://numba.pydata.org/
[Toyplot]: https://toyplot.readthedocs.io/en/stable/
[Toytree]: https://toytree.readthedocs.io/en/latest/
[Ipcoal]: https://ipcoal.readthedocs.io/en/latest/
[Msprime]: https://tskit.dev/msprime/docs/stable/intro.html
[Tskit]: https://tskit.dev/
[scikit-learn]: https://scikit-learn.org/stable/

## External binaries

In addition to learning to implement phylogenetic algorithms in Python, 
we also demonstrate usage of established external software tools in many
exercises. When multiple options are available we tend to select tools 
that are easiest to install (e.g., using conda), and which have a command
line interface (as opposed to graphical user interface). This includes 
the following software tools:

- Compiled software tools:
    - [RAxML]: Maximum likelihood tree inference software.
    - [MrBayes]: Bayesian tree inference software.
    - [BPP]: Multispecies coalescent species tree software.
    - ...

[RAxML]: https://cme.h-its.org/exelixis/software.html
[MrBayes]: ...
[BPP]: ...

## Optional Installation Instructions

If you want to follow along with the exercises in this textbook on your 
own computer, rather than use the cloud-based binder notebooks, you can do
so by installing the necessary software into a conda environment. You can
find detailed instructions for this in the [Coding bootcamp].

[Coding Bootcamp]: ../bootcamp/0.0-getting_started.md

