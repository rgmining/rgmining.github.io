:description: A framework of review data mining based on a graph model.

.. _top:

Review Graph Mining
=====================
.. raw:: html

   <div class="addthis_inline_share_toolbox"></div>

.. graphviz::

  digraph bipartite {
    graph [label="Review graph.", rankdir = LR];
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

A framework of review data mining based on a graph model.

It helps both data analysts who want to analyze their review data, and research
scientists who want to make other mining algorithms.

**For data analysts**, you can easily compare several algorithms:

* :ref:`Mutually Reinforcing Analysis (MRA) <ria:top>` [#DEXA2011]_
  (`rgmining-ria <https://pypi.python.org/pypi/rgmining-ria>`_),
* :ref:`Repeated Improvement Analysis (RIA) <ria:top>` [#DEIM2015]_
  (`rgmining-ria <https://pypi.python.org/pypi/rgmining-ria>`_),
* :ref:`Detecting Product Review Spammers Using Rating Behaviors <ria:top>` [#CIKM2010]_
  (`rgmining-ria <https://pypi.python.org/pypi/rgmining-ria>`_),
* :ref:`Review Spammer Detection <rsd:top>` [#ICDM2011]_
  (`rgmining-rsd <https://pypi.python.org/pypi/rgmining-rsd>`_),
* :ref:`Fraud Eagle <fraud-eagle:top>` [#ICWSM13]_
  (`rgmining-fraud-eagle <https://pypi.python.org/pypi/rgmining-fraud-eagle>`_),
* :ref:`FRAUDAR <fraudar:top>` [#KDD2016]_
  (`rgmining-fraudar <https://pypi.python.org/pypi/rgmining-fraudar>`_).

All packages are also available on `PyPI <https://pypi.python.org/pypi>`_ and you can
install them by ``pip install``.

To use one algorithm, you need to create a review graph object provided by
each package, create reviewers and products, add then run the algorithm.
For example, the following code shows a way to use MRA algorithm with the above
review graph:

.. code-block:: python

  # Construct a Review Graph instance.
  import ria
  graph = ria.mra_graph()

  # Create reviewers and products.
  reviewers = [graph.new_reviewer("reviewer-{0}".format(i)) for i in range(1,4)]
  products = [graph.new_product("product-{0}".format(i)) for i in range(1,3)]

  # Add reviews.
  graph.add_review(reviewers[0], products[0], 0.3)
  graph.add_review(reviewers[0], products[1], 0.9)
  graph.add_review(reviewers[1], products[1], 0.1)
  graph.add_review(reviewers[2], products[1], 0.5)

  # Start the algorithm.
  for i in range(10000):
    # Run one iteration.
    diff = graph.update()
    print("Iteration %d ends. (diff=%s)", i + 1, diff)
    # If the update becomes negligible, the algorithm ends.
    if diff < 10**-5:
      break

  # Print results.
  for r in graph.reviewers:
    print(r.name, r.anomalous_score)
  for p in graph.products:
    print(p.name, p.summary)

If you want to analyze a dataset given by this project or your review data are
formatted in :ref:`the JSON format <dataset-io:review-data>`, you can run
algorithms via ``analyze`` command provided by :ref:`script:top` package.

For example, the following command analyzes the synthetic dataset by the Fraud
Eagle algorithm with parameter :math:`\epsilon = 0.25`:

.. code-block:: sh

  $ analyze synthetic feagle --method-param epsilon=0.25

Or the following command analyze your review data file ``review.json`` by the
FRAUDAR algorithm with parameter blocks = 10:

.. code-block:: sh

  $ analyze file --dataset-param file=review.json fraudar --method-param blocks=10

**For research scientists**, you can evaluate your algorithms comparing with
other algorithms. This project also provides several dataset loaders:

* :ref:`A Synthetic Review Dataset Loader <synthetic:top>`
  (`rgmining-synthetic-dataset <https://pypi.python.org/pypi/rgmining-synthetic-dataset>`_),
* :ref:`amazon:top`
  (`rgmining-amazon-dataset <https://pypi.python.org/pypi/rgmining-amazon-dataset>`_),
* :ref:`tripadvisor:top`
  (`rgmining-tripadvisor-datast <https://pypi.python.org/pypi/rgmining-tripadvisor-dataset>`_).

To use these loaders, you need to make a review graph object which implements
the :ref:`dataset-io:graph-interface`.

For example, the following code shows a way to load the
Six Categories of Amazon Product Reviews Dataset
to a graph object ``graph``:

.. code-block:: python

  import amazon
  # `graph` must implement the graph interface.
  amazon.load(graph)


Contents
----------

.. toctree::
   :maxdepth: 2

   introduction
   tutorial
   libraries
   publications
   forum


Contribution
--------------
We welcome any contributions to this project such as issue reports, providing
mining algorithms, providing datasets, etc.

If you publish something using this project, please let us know any links to it.
We'd like to link any materials.

You can find contact information at the bottom of this page.


License
---------
All softwares in this project are released under The GNU General Public License Version 3,
see `COPYING <https://www.gnu.org/licenses/gpl-3.0.html>`_ for more detail.


References
------------
.. [#DEXA2011] Kazuki Tawaramoto, `Junpei Kawamoto`_, `Yasuhito Asano`_, and `Masatoshi Yoshikawa`_,
  "|springer| `A Bipartite Graph Model and Mutually Reinforcing Analysis for Review Sites
  <http://www.anrdoezrs.net/links/8186671/type/dlg/http://link.springer.com/chapter/10.1007%2F978-3-642-23088-2_25>`_,"
  Proc. of `the 22nd International Conference on Database and Expert Systems Applications <http://www.dexa.org/>`_ (DEXA 2011),
  pp.341-348, Toulouse, France, August 31, 2011.
.. [#DEIM2015] `川本 淳平`_, 俵本 一輝, `浅野 泰仁`_, `吉川 正俊`_,
  "|pdf| `初期レビューを用いた長期間評価推定 <http://db-event.jpn.org/deim2015/paper/253.pdf>`_,"
  `第7回データ工学と情報マネジメントに関するフォーラム <http://db-event.jpn.org/deim2015>`_,
  D3-6, 福島, 2015年3月2日～4日. |deim2015-slide|
.. [#CIKM2010] `Ee-Peng Lim <https://sites.google.com/site/aseplim/>`_,
  `Viet-An Nguyen <http://www.cs.umd.edu/~vietan/>`_,
  Nitin Jindal,
  `Bing Liu`_,
  `Hady Wirawan Lauw <http://www.smu.edu.sg/faculty/profile/9621/Hady-W-LAUW>`_,
  "`Detecting Product Review Spammers Using Rating Behaviors
  <http://dl.acm.org/citation.cfm?id=1871557>`_,"
  Proc. of the 19th ACM International Conference on Information and Knowledge Management,
  pp.939-948, 2010.
.. [#ICDM2011] `Guan Wang <https://www.cs.uic.edu/~gwang/>`_,
  `Sihong Xie <http://www.cse.lehigh.edu/~sxie/>`_, `Bing Liu`_,
  `Philip S. Yu <http://bdsc.lab.uic.edu/people.html>`_,
  "`Review Graph Based Online Store Review Spammer Detection
  <http://ieeexplore.ieee.org/document/6137345/?reload=true&arnumber=6137345>`_,"
  Proc. of the 11th IEEE International Conference on Data Mining (ICDM 2011),
  pp.1242-1247, 2011.
.. [#ICWSM13] `Leman Akoglu <http://www.andrew.cmu.edu/user/lakoglu/>`_,
  Rishi Chandy, and `Christos Faloutsos`_,
  "|pdf| `Opinion Fraud Detection in Online Reviews by Network Effects
  <https://www.aaai.org/ocs/index.php/ICWSM/ICWSM13/paper/viewFile/5981/6338>`_,"
  Proc. of `the 7th International AAAI Conference on WeblogsS and Social Media
  <http://www.icwsm.org/2013/>`_ (ICWSM 2013), Boston, MA, July, 2013.
.. [#KDD2016] `Bryan Hooi <https://www.andrew.cmu.edu/user/bhooi/index.html>`_,
  `Hyun Ah Song <http://www.cs.cmu.edu/~hyunahs/>`_,
  `Alex Beutel <http://alexbeutel.com/>`_,
  `Neil Shah <http://www.cs.cmu.edu/~neilshah/>`_,
  `Kijung Shin <http://www.cs.cmu.edu/~kijungs/>`_,
  `Christos Faloutsos`_,
  "|pdf| `FRAUDAR: Bounding Graph Fraud in the Face of Camouflage
  <http://www.andrew.cmu.edu/user/bhooi/papers/fraudar_kdd16.pdf>`_,"
  Proc. of the 22nd ACM SIGKDD International Conference on Knowledge Discovery and Data Mining (KDD 2016),
  pp.895-904, 2016.

.. _Junpei Kawamoto: https://www.jkawamoto.info
.. _Yasuhito Asano: http://www.iedu.i.kyoto-u.ac.jp/intro/member/asano
.. _Masatoshi Yoshikawa: http://www.db.soc.i.kyoto-u.ac.jp/~yoshikawa/
.. _川本 淳平: https://www.jkawamoto.info
.. _浅野 泰仁: http://www.iedu.i.kyoto-u.ac.jp/intro/member/asano
.. _吉川 正俊: http://www.db.soc.i.kyoto-u.ac.jp/~yoshikawa/
.. _Bing Liu: https://www.cs.uic.edu/~liub/
.. _Christos Faloutsos: http://www.cs.cmu.edu/afs/cs/usr/christos/www/


.. |springer| image:: img/springer.png

.. |pdf| raw:: html

  <i class="fa fa-file-pdf-o" aria-hidden="true"></i>

.. |deim2016-slide| raw:: html

  <a href="http://www.slideshare.net/jkawamoto/ss-59672505">
   <i class="fa fa-slideshare" aria-hidden="true"></i>
  </a>

.. |deim2015-slide| raw:: html

 <a href="http://www.slideshare.net/jkawamoto/deim2015-45470497">
  <i class="fa fa-slideshare" aria-hidden="true"></i>
 </a>
