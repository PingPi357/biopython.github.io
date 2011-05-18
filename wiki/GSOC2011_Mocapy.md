---
title: GSOC2011 Mocapy
permalink: wiki/GSOC2011_Mocapy
layout: wiki
---

'''Mocapy++Biopython: from data to probabilistic models of biomolecules
'''

Mocapy++ is a machine learning toolkit for training and using Bayesian
networks. It has been used to develop probabilistic models of
biomolecular structures. The goal of this project is to develop a Python
interface to Mocapy++ and integrate it with Biopython. This will allow
the training of a probabilistic model using data extracted from a
database. The integration of Mocapy++ with Biopython will provide a
strong support for the field of protein structure prediction, design and
simulation.

Discovering the structure of biomolecules is one of the biggest problems
in biology. Given an amino acid or base sequence, what is the three
dimensional structure? One approach to biomolecular structure prediction
is the construction of probabilistic models. A Bayesian network is a
probabilistic model composed of a set of variables and their joint
probability distribution, represented as a directed acyclic graph. A
dynamic Bayesian network is a Bayesian network that represents sequences
of variables. These sequences can be time-series or sequences of
symbols, such as protein sequences. Directional statistics is concerned
mainly with observations which are unit vectors in the plane or in
three-dimensional space. The sample space is typically a circle or a
sphere. There must be special directional methods which take into
account the structure of the sample spaces. The union of graphical
models and directional statistics allows the development of
probabilistic models of biomolecular structures. Through the use of
dynamic Bayesian networks with directional output it becomes possible to
construct a joint probability distribution over sequence and structure.
Biomolecular structures can be represented in a geometrically natural,
continuous space. Mocapy++ is an open source toolkit for inference and
learning using dynamic Bayesian networks that provides support for
directional statistics. Mocapy++ is excellent for constructing
probabilistic models of biomolecular structures; it has been used to
develop models of protein and RNA structure in atomic detail. Mocapy++
is used in several high-impact publications, and will form the core of
the molecular modeling package Phaistos, which will be released soon.
The goal of this project is to develop a highly useful Python interface
to Mocapy++, and to integrate that interface with the Biopython project.
Through the Bio.PDB module, Biopython provides excellent functionality
for data mining biomolecular structure databases. Integrating Mocapy++
and Biopython will allow training a probabilistic model using data
extracted from a database. Integrating Mocapy++ with Biopython will
create a powerful toolkit for researchers to quickly implement and test
new ideas, try a variety of approaches and refine their methods. It will
provide strong support for the field of biomolecular structure
prediction, design, and simulation.

'''Work Plan '''

'''Gain understanding of SEM and directional statistics '''

-   Review the theory behind machine learning for bioinformatics, Markov
    chain Monte Carlo and dynamic Bayesian networks.

<!-- -->

-   Build the theoretical background on the algorithms used in Mocapy++,
    such as parameter learning of Bayesian networks using Stochastic
    Expectation Maximization (SEM).

'''Study Mocapy++'s use cases '''

-   Read several papers and attempt to replicate part of the experiments
    described using Mocapy++.

<!-- -->

-   Get a better understanding of biological sequence analysis done
    through probabilistic models of proteins and nucleic acids.

'''Work with Mocapy++ '''

-   Understand Mocapy++'s internal architecture and algorithms by
    exploring its source code and running its test cases.

<!-- -->

-   Research other applications of Mocapy++ in Bioinformatics.

'''Design Mocapy++'s Python interface '''

-   Explore the source code of Biopython to understand its design
    and implementation. The Mocapy++ interface to be included in
    Biopython must be made compatible with the methods of solving
    problems in Biopython.

<!-- -->

-   Design a Python interface for Mocapy++, based on its data structures
    and algorithms. Examine Mocapy++'s use cases and existing test cases
    to provide guidance for the interface design.

'''Implement Python bindings '''

-   Implement test cases in Python using the new interface to Mocapy++.

<!-- -->

-   Implement python bindings for the defined interface.

'''Explore Mocapy++'s applications '''

-   Develop example applications that involve data mining of
    biomolecular structure databases using Biopython.

<!-- -->

-   Formulate probabilistic models using Python-Mocapy++. Apply the
    models to solve biological problems. Examples of problems that can
    be solved using dynamic Bayesian networks include deciding if a pair
    of sequences is evolutionarily related, finding sequences which are
    homologous to a known evolutionary family and predicting RNA
    secondary structure.

**Timeline**

''Before April 25 ''

-   Get involved with the Biopython project and community.

<!-- -->

-   Learn the statistical methods used in Mocapy++ and relevant concepts
    in structural biology.

Community bonding period

''April 25 - May 22 (4 weeks) ''

-   Familiarize myself with Mocapy++'s functionality and architecture.

<!-- -->

-   Configure a development environment and explore the Mocapy++ and
    Bio.PDB source code more thoroughly. Document the code
    during exploration.

<!-- -->

-   Study Mocapy++ and Bio.PDB test cases in order to understand the
    Mocapy++ interface requirements.

<!-- -->

-   Compare options to create python bindings to C++ code (Boost Python,
    Cython, Swig). Perform the necessary assesments and gathering of
    requirements to determine the best library to create the
    Python bindings.

<!-- -->

-   Try fixing bugs in Biopython in order to get familiar with the
    development cycle.

Begin of coding phase

''May 23 - June 5 (2 weeks) ''

-   Design and implement test cases for the Mocapy++ Python interface.
    The tests must include data structures such as the Multi-Dimentional
    array; and statistic models such as the hidden Markov Models, a
    special case of dynamic Bayesian networks.

<!-- -->

-   Identify functions and data structures which impose challenges for
    the creation of Python bindings.

<!-- -->

-   Implement Python bindings for the core functions and data
    structures, especially the ones which are straightforward to wrap.

''June 6 - June 19 (2 weeks) ''

-   Implement Python bindings for the remaining Mocapy++ functionality
    that composes its interface.

<!-- -->

-   Run and improve the previously designed test cases. Make sure the
    newly designed interface meets the requirements of the use cases.

<!-- -->

-   Do performance analysis (code profiling) in order to make sure the
    Python interface of Mocapy++ is fast enough to be usable.

<!-- -->

-   Try other options to create Python bindings to C++ code, in case the
    implementation doesn't meet the speed requirements.

''June 20 - July 3 (2 weeks) ''

-   Integrate the Mocapy++ Python interface with Biopython.

<!-- -->

-   Implement integration tests for Mocapy++ Biopython.

<!-- -->

-   Test the operation of each module of the modified source code.

''June 4 - July 10 (1 week) ''

-   Make further changes in the code to improve robustness
    and functionality.

<!-- -->

-   Gather, organize, and improve the documentation written during the
    previous weeks.

Mid-term evaluations (July 11)

''July 11 - July 24 (2 weeks) ''

-   Design probabilistic models for biological problems. Solve them
    using Mocapy++ Biopython.

<!-- -->

-   Offer the code to the community for testing and suggestions for
    further functionality.

''July 25 - August 7 (2 weeks) ''

-   Create applications which use the data mining provided by Bio.PDB
    together with the machine learning features of Mocapy++.

<!-- -->

-   Profile the code and work on speed and robustness improvements.

''August 8 - August 14 (1 week) ''

-   Perform last review and improvements on code and documentation.

''August 15 - August 21 (1 week) ''

-   A buffer for any unpredictable delay.

Firm pencils down (August 22)

'''External References: '''

\[<https://docs.google.com/document/d/1E72Qysp3pMd69hSYfIXJKgBLdeSMbzSol9RYD2rKHlI/edit?hl=pt_BR&authkey=CPmFxK0H>:
Mocapy++Biopython - Box of ideas\]

\[<https://docs.google.com/document/d/1JPkCbvJ9Gk3b6LmQ68__UUt4Yz2P1-c286p6FVEqyXs/edit?hl=pt_BR&authkey=CJTCpZgL>:
Mocapy++ Bindings Prototype\]