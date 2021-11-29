

### Classes

- 1.1: introduction
	- Learning objectives
	- What is computational phylogenetics?
	- What is a phylogenetic tree?
	- What does a tree represent: Many possible things.
		- Examples
	- What do we learn from phylogenetic trees:
		- Biodiversity Systematics
		- Epidemiology and forensics
		- Function and homology
	- What do we learn from collections of trees:
		- Biogeography
		- Demography and rates of change
		- ...
	- Trees as data, and data science.


- 1.2 Tree thinking
	- What does tree thinking mean
	- Terminology in trees
	- Reading from the tips
	- Rotations
	- Rooting
		- unrooted versus rooted
		- what is a root node or edge
		- changing the rooting changes the relationships
	- Units
		- ...
	- Tree shapes
		- topology
	- Meta data
		- edge lengths
		- support values
	- Trees as data:
		- a visualization
		- a model (depends on units and model of change)
		- a variance-covariance matrix
		- a relational object
	- Saving trees
		- newick format
		- nexus format
		- xml format
		- other formats
			- tree sequence table
			- json
	- Tree databases
		- treebase
	- Interpreting trees


- 1.3: Tree visualizations
	- A history of visualizations
	- Drawing (plotting) a tree 
	- The toytree Python library
		- go to docs page
	- Tree I/O
	- Random trees
	- Tree layout
	- Edge lengths
		- transform, show scale, ...
	- Rooting, reroot
	- Transform
		- drop tips, 
	- Example:
		- Load the mammal tree
		- Prune a subclade
		- Relabel, color, style, annotate.
	- Exercises: 
		nb-1.3: tree thinking, toytree, upham tree.
	- reading: Felsenstein 34


- 1.4. Genealogy
	- Wright-Fisher Process
		- 1.4.1: Visualize the WF process
	- Kingman coalescent
		- 1.4.2: Infer Ne based on coalescent reps
	- Coalescent simulations (msprime)
		- 1.4.3: Simulate coalescent histories for a single pop
	- Demographic models
		- 1.4.4: 
	- Species Tree simulations (ipcoal)
		- 1.4.5: 
    - Reading and Exercises
    	- 1.4


5. Mutations
 	- 4.0 - 'infinite-sites' mutations: 4.0-mutations.md
 	- 4.1 - Markov substitution models: 4.1-substituions.md
 	- 4.2 - Statistical properties of Markov models: 4.2-markov-models.md
 	- Reading and Exercises: 1-reading-list.md      