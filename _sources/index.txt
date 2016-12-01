:description: A framework of review data mining based on a graph model.

Review Graph Mining
=====================
.. raw:: html

   <div class="addthis_inline_share_toolbox"></div>

A framework of review data mining based on a graph model.

.. graphviz::

  digraph bipartite {
    graph [label="Bipartite graph model.", rankdir = LR];
    "r1" [label="Reviewer 1 \n (anomalous: 0.1)"];
    "r2" [label="Reviewer 2 \n (anomalous: 0.9)"];
    "r3" [label="Reviewer 3 \n (anomalous: 0.5)"];
    "p1" [label="Product 1 \n (summary: 0.3)"];
    "p2" [label="Product 2 \n (summary: 0.8)"];
    "r1" -> "p1" [label="0.3"];
    "r1" -> "p2" [label="0.9"];
    "r2" -> "p2" [label="0.1"];
    "r3" -> "p2" [label="0.5"];
  }


Contents
----------

.. toctree::
   :maxdepth: 2

   introduction
   tutorial
   libraries
   publications
   forum
