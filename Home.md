# Java Information Dynamics Toolkit (JIDT)

Copyright (C) 2012-2014 [Joseph T. Lizier](http://lizier.me/joseph/); 2014-2016 [Joseph T. Lizier](http://lizier.me/joseph/) and Ipek Özdemir; 2017- [Joseph T. Lizier](http://lizier.me/joseph/), Ipek Özdemir and [Pedro Mediano](https://www.doc.ic.ac.uk/~pam213/)

*JIDT* provides a stand-alone, open-source code Java implementation (also usable in [Matlab, Octave](UseInOctaveMatlab), [Python](UseInPython), [R](UseInR), [Julia](UseInJulia) and [Clojure](UseInClojure)) of information-theoretic measures of distributed computation in complex systems: i.e. information storage, transfer and modification.

JIDT includes implementations:
 * principally for the measures **transfer entropy**, **mutual information**, and their conditional variants, as well as **active information storage**, entropy, etc;
 * for both _discrete_ and _continuous_-valued data;
 * using various types of estimators (e.g. _Kraskov-Stögbauer-Grassberger estimators_, _box-kernel estimation_, _linear-Gaussian_),
as described in full at ImplementedMeasures.

JIDT is distributed under the [GNU GPL v3 license](http://www.gnu.org/licenses/gpl.html) (or later).

# Getting started

 1. [Download](Downloads) and [Installation](Installation) is very easy!
   1. _Quick start_: download the latest [v1.4 full distribution](http://lizier.me/joseph/software/jidt/download.php?file=infodynamics-dist-1.4.zip) (suitable for all platforms) and see the readme.txt file therein.
 1. [Documentation](Documentation) including: the paper describing JIDT at [arXiv:1408.3270](http://arxiv.org/abs/1408.3270) (distributed with the toolkit), a [Tutorial](Tutorial), and [Javadocs (v1.4 here)](http://lizier.me/joseph/software/jidt/javadocs/v1.4/);
 1. [Demos](Demos) are included with the full distribution, including a [GUI app](AutoAnalyser) for automatic analysis and code generation (see picture below), [simple java demos](SimpleJavaExamples) and [cellular automata (CA) demos](CellularAutomataDemos).
  1. These Java tools can easily be used in [Matlab/Octave](OctaveMatlabExamples), [Python](PythonExamples), [R](R_Examples), [Julia](JuliaExamples) and [Clojure](Clojure_Examples)! (click on each language here for examples)

![Computing in the GUI app image](https://raw.githubusercontent.com/jlizier/jidt/master/web/AutoAnalyserGUI-2-Compute.png)

For further information or announcements:
 * Join our discussion group: http://groups.google.com/d/forum/jidt-discuss
 * See also the [FAQs](FAQs)
 * Follow [@infodynamicstkt](http://twitter.com/infodynamicstkt) on twitter

# Citation

Please **cite** your use of this toolkit as:

Joseph T. Lizier, "JIDT: An information-theoretic toolkit for studying the dynamics of complex systems", _Frontiers in Robotics and AI_ 1:11, 2014; doi:[10.3389/frobt.2014.00011](http://dx.doi.org/10.3389/frobt.2014.00011) (pre-print: [arXiv:1408.3270](http://arxiv.org/abs/1408.3270))

And please [let me know](mailto:joseph.lizier_AT_gmail.com) about any publications resulting from its use!

See other PublicationsUsingThisToolkit.

# News

_26/11/2017_ - New jar and full distribution files available for **release v1.4**; Changes for v1.4 include:
Major expansion of functionality for AutoAnalysers: adding Launcher applet and capability to double click jar to launch, added Entropy, CMI, CTE and AIS AutoAnalysers, also added binned estimator type, added all variables/pairs analysis, added statistical significance analysis, and ensured functionality of generated Python code with Python3;
Added GPU (cuda) capability for KSG Mutual Information calculator (proper documentation and wiki page to come), including unit tests;
Added fast neighbour search implementations for mixed discrete-continuous KSG MI estimators;
Expanded Gaussian estimator for multi-information (integration);
Made all demo/data files readable by Matlab.

_17/12/2016_ - New book out from J. Lizier et al., ["An Introduction to Transfer Entropy: Information Flow in Complex Systems"](http://bit.ly/te-book-2016) published by Springer, which contains various examples using JIDT (distributed in our releases)

_21/10/2016_ - New jar and full distribution files available for **release v1.3.1**; Changes for v1.3.1 include:
Major update to TransferEntropyCalculatorDiscrete so as to implement arbitrary source and dest embeddings and source-dest delay;
Conditional TE calculators (continuous) handle empty conditional variables;
Added new auto-embedding method for AIS and TE which maximises bias corrected AIS;
Added getNumSeparateObservations() method to TE calculators to make reconstructing/separating local values easier after multiple addObservations() calls;
Fixed kernel estimator classes to return proper densities, not probabilities;
Bug fix in mixed discrete-continuous MI (Kraskov) implementation;
Added simple interface for adding joint observations for MultiInfoCalculatorDiscrete
Including compiled class files for the AutoAnalyser demo in distribution;
Updated Python demo 1 to show use of numpy arrays with ints;
Added Python demo 7 and 9 for TE Kraskov with ensemble method and auto-embedding respectively;
Added Matlab/Octave example 10 for conditional TE via Kraskov (KSG) algorithm;
Added utilities to prepare for enhancing surrogate calculations with fast nearest neighbour search;
Minor bug patch to Python readFloatsFile utility.

_19/7/2015_ - New jar and full distribution files available for **release v1.3**; Changes for v1.3 include:
Added AutoAnalyser (Code Generator) GUI demo for MI and TE;
Added auto-embedding capability via Ragwitz criteria for AIS and TE calculators (KSG estimators);
Added Java demo 9 for showcasing use of Ragwitz auto-embedding;
Adding small amount of noise to data in all KSG estimators now by default (may be disabled via setProperty());
Added getProperty() methods for all conditional MI and TE calculators;
Upgraded Python demos for Python 3 compatibility;
Fixed bias correction on mixed discrete-continuous KSG calculators;
Updated the tutorial slides to those in use for ECAL 2015 JIDT tutorial.

_12/2/2015_ - New jar and full distribution files available for **release v1.2.1**; Changes for v1.2.1 include:
Added tutorial slides, description of exercises and sample exercise solutions;
Made jar target Java 1.6;
Added Schreiber TE heart-breath rate with KSG estimator demo code for Python.

_28/1/2015_ - New jar and full distribution files available for **release v1.2**; Changes for v1.2 include:
Dynamic correlation exclusion, or Theiler window, added to all Kraskov estimators;
Added univariate MI calculation to simple demo 6;
Added Java code for Schreiber TE heart-breath rate with KSG estimator, ready for use as a template in Tutorial;
Patch for crashes in KSG conditional MI algorithm 2.

_20/11/2014_ - New jar and full distribution files available for **release v1.1**; Changes for v1.1 include:
Implemented Fast Nearest Neighbour Search for Kraskov-Stögbauer-Grassberger (KSG) estimators for MI, conditional MI, TE, conditional TE, AIS, Predictive info, and multi-information. This includes a general (multivariate) k-d tree implementation;
Added multi-threading (using all available processors by default) for the KSG estimators -- code contributed by Ipek Özdemir;
Added Predictive information / Excess entropy implementations for KSG, kernel and Gaussian estimators;
Added R, Julia, and Clojure demos;
Added Windows batch files for the Simple Java Demos;
Added property for adding a small amount of noise to data in all KSG estimators;

_15/8/2014_ JIDT paper finalised and uploaded to the website and [arXiv:1408.3270](http://arxiv.org/abs/1408.3270)

_14/8/2014_ - New jar and full distribution files available for our **first official release, v1.0**; Changes for v1.0 include: Added the draft of the paper on the toolkit to the release;
Javadocs made ready for release;
Switched source->destination arguments for discrete TE calculators to be with source first in line with continuous calculators;
Renamed all discrete calculators to have Discrete suffix -- TE and conditional TE calculators also renamed to remove "Apparent" prefix and change "Complete" to "Conditional";
Kraskov estimators now using 4 nearest neighbours by default;
Unit test for Gaussian TE against ChaLearn Granger causality measurement;
Added Schreiber TE demos; Interregional transfer demos; documentation for Interaction lag demos; added examples 7 and 8 to Simple Java demos;
Added property to add noise to data for Kraskov MI;
Added derivation of Apache Commons Math code for chi square distribution, and included relevant notices in our release;
Inserted translation class for arrays between Octave and Java;
Added analytic statistical significance calculation to Gaussian calculators and discrete TE;
Corrected Kraskov algorithm 2 for conditional MI to follow equation in Wibral et al. 2014.

_20/4/2014_ - New jar and full distribution files available for v0.2.0; Moved downloads to http://lizier.me/joseph/ since google code has stopped the download facility here :(. Changes for v0.2.0 include: Rearchitected (most) Transfer Entropy and Multivariate TE calculators to use an underlying conditional mutual information calculator, and have arbitrary embedding delay, source-dest delay; this includes moving Kraskov-Grassberger Transfer Entropy calculator to use a single conditional mutual information estimator instead of two mutual information estimators; Rearchitected (most) Active Information Storage calculators to use an underlying mutual information calculator; Added Conditional Transfer Entropy calculators using underlying conditional mutual information calculators; Moved mixed discrete-continuous calculators to a new "mixed" package; bug fixes.

_11/9/2013_ - New jar and full distribution files available for v0.1.4; added scripts to generate CA figures for 2013 book chapters; added general Java demo code; added Python demo code; made Octave/Matlab demos and CA demos properly compatible for Matlab; added extra Octave/Matlab general demos; added more unit tests for MI and conditional MI calculators, including against results from Wibral's TRENTOOL; bug fixes.

_11/9/2013_ - New CA demo scripts for several review book chapters we're preparing in 2013 have been uploaded - see [CellularAutomataDemos](CellularAutomataDemos).

_4/6/2013_ - Added instructions on how to [use in python](UseInPython) and several [PythonExamples](PythonExamples).

_13/01/2013_ - New jar and full distribution files available for v0.1.3; existing Octave/Matlab demo code made compatible with Matlab; several bug fixes, including using max norm by default in Kraskov calculator (instead of requiring this to be set explicitly); more unit tests (including against results from Kraskov's own MI implementation)

_19/11/2012_ - New jar and full distribution files available for v0.1.2, including demo code for two newly submitted papers

_31/10/2012_ - Jar and full distribution files available for v0.1.1 (first distribution)

_7/5/2012_ - JIDT project created and code uploaded
