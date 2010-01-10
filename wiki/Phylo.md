---
title: Phylo
permalink: wiki/Phylo
layout: wiki
---

This module provides classes, functions and I/O support for working with
phylogenetic trees.

This code is not yet part of Biopython, and therefore the documentation
has not been integrated into the Biopython Tutorial yet either.

Availability
------------

The source code for this module currently lives on
[Eric](User%3AEricTalevich "wikilink")'s [phyloxml
branch](http://github.com/etal/biopython/tree/phyloxml) in GitHub. If
you're interested in testing this code before it's been merged into
Biopython, follow the instructions there to create your own fork, or
just clone the phyloxml branch onto your machine.

Requirements:

-   Biopython 1.51 or newer (older may work, but hasn't been tested)
-   Python 2.4 or newer
-   ElementTree module

To draw trees (optional), you'll also need these packages:

-   [NetworkX](http://networkx.lanl.gov/index.html) 1.0rc1 (or 0.36 for
    snapshot at the end of GSoC 2009)
-   [PyGraphviz](http://networkx.lanl.gov/pygraphviz/) 0.99.1 or
    [pydot](http://dkbza.org/pydot.html)
-   [matplotlib](http://matplotlib.sourceforge.net/)

The I/O and tree-manipulation functionality will work without them;
they're imported on demand when the functions to\_networkx() and
draw\_graphviz() are called.

The XML parser used in the IO.PhyloXMLIO sub-module is ElementTree,
added to the Python standard library in Python 2.5. To use this module
in Python 2.4, you'll need to install a separate package that provides
the ElementTree interface. Two exist:

-   [lxml](http://codespeak.net/lxml/)
-   [elementtree](http://effbot.org/zone/element-index.htm)
    (or cElementTree)

PhyloXMLIO attempts to import each of these compatible ElementTree
implementations until it succeeds. The given XML file handle is then
parsed incrementally to instantiate an object hierarchy containing the
relevant phylogenetic information.

I/O functions
-------------

Wrappers for supported file formats are available from the top level of
the module:

``` python
from Bio import Phylo
```

Like SeqIO and AlignIO, this module provides four I/O functions:
parse(), read(), write() and convert(). Each function accepts either a
file name or an open file handle, so data can be also loaded from
compressed files, StringIO objects, and so on. If the file name is
passed as a string, the file is automatically closed when the function
finishes; otherwise, you're responsible for closing the handle yourself.

The second argument to each function is the target format. Currently,
the following formats are supported:

-   phyloxml
-   newick
-   nexus

See the [PhyloXML](PhyloXML "wikilink") page for more examples of using
tree objects.

### parse()

Incrementally parse each tree in the given file or handle, returning an
iterator of Tree objects (i.e. some subclass of the Bio.Phylo.BaseTree
Tree class, depending on the file format).

``` python
>>> trees = Phylo.parse('phyloxml_examples.xml', 'phyloxml')
>>> for tree in trees:
...     print tree.name
```

    example from Prof. Joe Felsenstein's book "Inferring Phylogenies"
    example from Prof. Joe Felsenstein's book "Inferring Phylogenies"
    same example, with support of type "bootstrap"
    same example, with species and sequence
    same example, with gene duplication information and sequence relationships
    similar example, with more detailed sequence data
    network, node B is connected to TWO nodes: AB and C
    ...

If there's only one tree, then the next() method on the resulting
generator will return it.

``` python
>>> tree = Phylo.parse('phyloxml_examples.xml', 'phyloxml').next()
>>> tree.name
'example from Prof. Joe Felsenstein\'s book "Inferring Phylogenies"'
```

Note that this doesn't immediately reveal whether there are any
remaining trees -- if you want to verify that, use read() instead.

### read()

Parse and return exactly one tree from the given file or handle. If the
file contains zero or multiple trees, a ValueError is raised. This is
useful if you know a file contains just one tree, to load that tree
object directly rather than through parse() and next(), and as a safety
check to ensure the input file does in fact contain exactly one
phylogenetic tree at the top level.

``` python
tree = Phylo.read('example.xml', 'phyloxml')
print tree
```

### write()

Write a sequence of Tree objects to the given file or handle. Passing a
single Tree object instead of a list or iterable will also work. (See,
TreeIO is friendly.)

``` python
tree1 = Phylo.read('example1.xml', 'phyloxml')
tree2 = Phylo.read('example2.xml', 'phyloxml')
Phylo.write([tree1, tree2], 'example-both.xml', 'phyloxml')
```

### convert()

Given two files (or handles) and two formats, both supported by
Bio.Phylo, convert the first file from the first format to the second
format, writing the output to the second file.

``` python
Phylo.convert('example.nhx', 'newick', 'example2.nex', 'nexus')
```

Tree and Subtree classes
------------------------

The basic objects are defined in Bio.Phylo.BaseTree.

### Format-specific extensions

To support additional information stored in specific file formats,
sub-modules within Tree offer additional classes that inherit from
BaseTree classes.

Each sub-class of BaseTree.Tree or Node has a class method to promote an
object from the basic type to the format-specific one. These sub-class
objects can generally be treated as instances of the basic type without
any explicit conversion.

**PhyloXML**: Support for the phyloXML format. See the
[PhyloXML](PhyloXML "wikilink") page for details.

**Newick**: The Newick module provides minor enhancements to the
BaseTree classes, plus several shims for compatibility with the existing
Bio.Nexus module. The API for this module is under development and
should not be relied on, other than the functionality already provided
by BaseTree.

Utilities
---------

Some additional tools are located in the Utils module under Bio.Phylo.
These functions are also loaded to the top level of the Phylo module on
import for easy access.

Where a third-party package is required, that package is imported when
the function itself is called, so these dependencies are not necessary
to install or use the rest of the Tree module.

### pretty\_print()

Produces a plain-text representation of the entire tree. Uses str() to
display nodes by default; for the longer repr() representation, add the
argument show\_all=True.

Strings are automatically truncated to ensure reasonable display.

    >>> phx = Phylo.read('phyloxml_examples.xml', 'phyloxml')
    >>> Phylo.pretty_print(phx)
    Phylogeny example from Prof. Joe Felsenstein's book "Inferring Phylogenies"
        Clade
            Clade
                Clade A
                Clade B
            Clade C
    ...

    >>> Phylo.pretty_print(phx, show_all=True)
    Phylogeny(description='phyloXML allows to use either a "branch_length"
    attribute or element to indicate branch lengths.', name='example from
    Prof. Joe Felsenstein's book "Inferring Phylogenies"')
        Clade()
            Clade(branch_length=0.06)
                Clade(branch_length=0.102, name='A')
                Clade(branch_length=0.23, name='B')
            Clade(branch_length=0.4, name='C')
    ...

### Graph export

Although any phylogenetic tree can reasonably be represented by a
directed acyclic graph, the Phylo module does not attempt to provide a
generally usable graph library. Instead, it provides two functions for
exporting Tree objects to the excellent
[NetworkX](http://networkx.lanl.gov/) library's graph objects and using
that library, along with
[matplotlib](http://matplotlib.sourceforge.net/) and/or
[PyGraphviz](http://networkx.lanl.gov/pygraphviz/), to display trees.

**to\_networkx** returns the given tree as a networkx LabeledDiGraph or
LabeledGraph object. You'll probably need to import networkx directly
for subsequent operations on the graph object. To display a (somewhat
haphazard-looking) dendrogram on the screen, for interactive work, use
matplotlib or pylab along with one of networkx's drawing functions.

``` python
import networkx, pylab
tree = Phylo.read('example.xml', 'phyloxml')
net = Phylo.to_networkx(tree)
networkx.draw(net)
pylab.show()
```

**draw\_graphviz** mimics the networkx function of the same name, with
some tweaks to improve the display of the graph. If a file name is
given, the graph is drawn directly to that file, and options such as
image format (default PDF) may be used.

``` python
tree = Phylo.read('example.xml', 'phyloxml')
# Draw it a few different ways
Phylo.draw_graphviz(tree, 'example.pdf')
Phylo.draw_graphviz(tree, 'example.png', format='png')
Phylo.draw_graphviz(tree)
```