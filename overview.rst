Overview
========

Welcome to Multinet!

Multinet is a software suite consisting of a web API server, a web client
application, a TypeScript client library, and a collection of analysis and
visualization applications that are all designed to work with each other to host
*multivariate network data* and enable *discovery, analysis, and visualization*
for them.

Multinet is part of a larger `NSF research project
<https://vdl.sci.utah.edu/projects/2019-nsf-multinet/>`_ led by the
`Visualization Design Lab <https://vdl.sci.utah.edu/>`_ at the University of
Utah, with `Kitware Inc. <https://www.kitware.com/>`_ spearheading software
development efforts.

What is a Multivariate Network?
-------------------------------

Networks are an increasingly common and useful way to model many of the
phenomena in the natural, social, biological, and abstract worlds around us.
Common examples include social networks connecting individuals through their
acquaintanceships, neurons in the retina forming sensory-perceptual receiver
circuits, computers connected to each other comprising both local networks and
the Internet at large, and networks modeling the probabilistic transmission of
disease through a community, but there are countless other examples, spread
throughout many academic and industrial fields.

In general, networks are modeled as a collection of *nodes*, representing
entities such as people or computers, connected together via *links*
representing some type of relationship between a subset of pairs of nodes.
*Multivariate* networks are networks that carry extra data (also known as
*attributes*) on the nodes and edges. For instance, in a social network, the
nodes (representing individual people) might each carry data such as *name*,
*age*, *hometown*, etc. A network representing the retina could have scientific
measurements or assessments, such as cell types for the nodes, or voltage
measurements for the links, etc.

The Multinet research project's main goal is to develop data processing,
analysis, and visualization methods that take into account both the connectivity
features of networks, and their multivariate data as well. Doing so will unlock
a lot of the value of network datasets being collected by scientists, policy
makers, and laypeople alike.

For an overview of the state of the art in visualization techniques for
multivariate networks, see `Nobre et al.
<https://vdl.sci.utah.edu/publications/2019_eurovis_mvn/>`_

The Multinet Software Stack
---------------------------

The Multinet stack consists of the following components:

- `multinet-server <https://github.com/multinet-app/multinet-server>`_, an
  open-source Flask API server that provides the Multinet API, which we are
  developing as part of this project

- `multinet-client <https://github.com/multinet-app/multinet-client>`_, an
  open-source web application, using VueJS and Vuetify to present an easy to use
  interface to the Multinet API, including access to stored data, and ways to
  launch intensive visualization and analysis applications

- visualization applications, including `view-nodelink
  <https://github.com/multinet-app/view-nodelink>`_, an interactive node-link diagram that
  also displays node attributes in various forms, and `view-adjmatrix
  <https://github.com/multinet-app/view-adjmatrix>`_, an interactive adjacency
  matrix that also supports attribute display

- `ArangoDB <https://www.arangodb.com/>`_, a third-party open-source graph
  database system that Multinet uses to store data and perform queries

You can see how the client works by going to https://multinet.app and giving it
a try. To build your own development environment, either to host your own data
locally, or to work on the codebases, see :ref:`quickstart`.
