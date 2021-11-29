
# Python Style Guide

Python is a scripting language that is intended to be easy to read and write,
and this underlies much of its popularity and growth over the last few 
decades. 

- speed
- evolution
- interactivity
- jit-compilation
- data science revolution
- libraries 
- machine learning


### Black style
As with most languages, Python is flexible in allowing users to write code
in various ways to accomplish the same task. 



### Examples

```py
def get_num_nodes(tree: toytree.Toytree) -> int:
	"""Return the number of nodes in a tree.

	Example
	-------
	>>> tree = toytree.rtree.rtree(10)
	>>> print(get_num_nodes(tree))
	"""
    return len(tree.idx_dict)
```




*[syntax]: The set of rules for proper function of a coding language
