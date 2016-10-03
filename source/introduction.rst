Introduction
==============
A number of web sites provide people's reviews about various kinds of objects
such as products, stores and services. Those reviews have been considered as
important for both consumers and vendors to make decisions. For example,
consumers read product reviews on Amazon.com to buy the best products
and read movie reviews on a site like The Internet Movie Database
(`IMDb <http://www.imdb.com/>`_) to find interesting movies.
On the other hand, vendors obtain feedbacks about their products from review
sites for marketing.

Summaries of reviews are also useful for making decisions particularly
because summaries enable us to understand semantic orientations without reading
all reviews. In fact, most of review sites provide summaries of reviews.
A typical summary is average scores of reviews.
Several methodologies to summarize reviews have been proposed [#Liu:WWW05]_
[#Pera:WISE10]_.

To summarize reviews, treating all reviews equivalently is inappropriate
approach because there would be *anomalous reviewers*. Some of them are
malicious and sometimes called spam reviewers who would deliberately bring
biased views for their benefit. The others would provide too specialized
opinions for common people. One example of anomalous but not spam reviewer is an
expert of a product. Opinions of experts are often significantly useful for
another expert, although they can be inappropriate for common people.
For example, if a common person desires to buy a digital camera for daily use,
reviews from common people are more suitable than ones from experts because
usually experts recommend too expensive or too heavy camera for common people.
Therefore, detecting anomalous reviewers and their reviews is important to
summarize reviews.

The aim of this project is providing a framework to evaluate several algorithms
to detect anomalous reviewers and compare those algorithms in your problem.


.. rubric:: References

.. [#Liu:WWW05] B. Liu, M. Hu, and J. Cheng. Opinion Observer: Analyzing and
  Comparing Opinions on the Web. In Proc. of the 14th International Conference
  on World Wide Web, pages 342–351, Chiba, Japan, May 2005.
.. [#Pera:WISE10] M. S. Pera, R. Qumsiyeh, and Y.-K. Ng. An Unsupervised
  Sentiment Classifier on Summarized or Full Reviews. In Proc. of the 11th
  International Conference on Web Information Systems Engineering, pages 142–156,
  Hong Kong, China, Dec. 2010. Springer-Verlag.
