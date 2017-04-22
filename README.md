# newick-tools

[![License](https://img.shields.io/badge/license-AGPL-blue.svg)](http://www.gnu.org/licenses/agpl-3.0.en.html)
[![Build Status](https://travis-ci.org/xflouris/newick-tools.svg?branch=master)](https://magnum.travis-ci.com/xflouris/newick-tools)

## Introduction

[RF fork primarily to manipulate fonts in svg.c]

The aim of this project is to implement a proper, multifunctional newick
manipulation toolkit called `newick-tools`. The toolkit should:

* correctly parse newick files, both binary rooted and binary unrooted.
* parse n-ary newick files and allow collapsing into binary rooted/unrooted.
* parse the [newick extended format](http://dmi.uib.es/~gcardona/BioInfo/enewick.html)
* create new topologies from existing one by pruning taxa, or inducing subtrees.
* generate topologies
* list taxa, or taxa of specific subtrees
* visualize the tree in terminal (ASCII), vector formats such as SVG and EPS, and raster format such as PNG.
* compare topologies
* root trees given outgroup taxon or outgroup subtree
* locate repeated substructures (subtree repeats)
* display tree info (rooting,number of taxa, max branch length, average branch length etc)
* generate a consensus tree from a collection of trees.
* perform all above functions on files that contain more than one tree, e.g. induce the subtrees of specific taxa in a collection of trees.


## Compilation instructions

Currently, `newick-tools` requires that [GNU Bison](http://www.gnu.org/software/bison/)
and [Flex](http://flex.sourceforge.net/) are installed on the target system. On
a Debian-based Linux systems, ... well you should know.

`newick-tools` also requires that a GNU system is available as it uses several
functions (e.g. `asprintf`) which are not present in the POSIX standard.
This, however may change in the future such that the code is more portable.

`newick-tools` can be compiled using the included Makefile:

`make`

## Command-line options

General options:

* `--help`
* `--version`
* `--quiet`
* `--precision`
* `--seed`

Options for binary trees:
* `--lca_left`
* `--lca_right`
* `--identical`
* `--extract_ltips`
* `--extract_rtips`
* `--svg`
* `--induce_subtree`
* `--subtree_short`
* `--svg_legend_ratio`

Options for unrooted trees:
* `--root`

Options for all tree types:
* `--extract_tips`
* `--prune_tips`
* `--prune_random`
* `--tree_show`
* `--make_binary`
* `--info`

Options for visualization:
* `--svg_width`
* `--svg_fontsize`
* `--svg_tipspacing`
* `--svg_legend_ratio`
* `--svg_nolegend`
* `--svg_marginleft`
* `--svg_marginright`
* `--svg_margintop`
* `--svg_marginbottom`
* `--svg_inner_radius`

Input and output options:
* `--tree_file`
* `--output_file`

## 

## License and third party licenses

The code is currently licensed under the [GNU Affero General Public License version 3](http://www.gnu.org/licenses/agpl-3.0.en.html).

## Code

    File           | Description
-------------------|----------------
**newick-tools.c** | Main file handling command-line parameters and executing corresponding parts.
**Makefile**       | Makefile.
**lex_rtree.l**    | Lexical analyzer parsing newick rooted trees.
**lex_utree.l**    | Lexical analyzer parsing newick unrooted trees.
**lex_ntree.l**    | Lexical analyzer parsing newick n-ary trees.
**util.c**         | Various common utility functions.
**arch.c**         | Architecture specific code (Mac/Linux).
**rtree.c**        | Rooted tree manipulation functions.
**utree.c**        | Unrooted tree manipulation functions.
**ntree.c**        | n-ary tree manipulation functions.
**parse_rtree.y**  | Functions for parsing rooted trees in newick format.
**parse_utree.y**  | Functions for parsing unrooted trees in newick format.
**parse_ntree.y**  | Functions for parsing n-ary trees in newick format.
**lca_utree.c**    | Naive LCA computation in unrooted trees.
**lca_tips.c**     | Compute tips leading to an LCA node.
**svg.c**          | SVG output routines.
**prune.c**        | Methods for pruning taxa and inducing subtrees.
**info.c**         | Functions for showing various tree-related  information.

## Examples:
Say you have two leaf-nodes labelled 371596Q and 337364Q, you can prune them as follows:
newick-tools --induce_subtree "371596Q,337364Q" --tree_file RAxML_bestTree.tre --output_file o.t
This example serves to clarify that the TAXA element referred to in the docs are comma-separated leaf-labels.

## Coding style
* High number of globals.
* The options are exclusively long.
* the --three-word-option standard is waived. In its stead, the underscore is used as the token separator
* Some impoliteness "go fix your tree" no doubt due to non-maternal-english of coders, not intentional one expects.
* However, program behaves well according to valgrind.

## Bugs

The source code in the master branch is thoroughly tested before commits.
However, mistakes may happen. All bug reports are highly appreciated.
- RF: segfaults with induce_subtree. This function seems to be partially built, explains version number (0.0.1).
    This is probably due to your giving it an unrooted tree. The induce_subtree seems to need a root, I think.

## The team

* Paschalia Kapli
* Sarah Lutteropp
* Tom&aacute;&scaron; Flouri
