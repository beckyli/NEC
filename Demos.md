_List of demonstration code sets distributed with the toolkit_

## Demos

Several sets of demonstration code are distributed with the toolkit. Links to their wiki pages and their location in the distribution are given below:
  * [AutoAnalyser](AutoAnalyser) -- `demos/AutoAnalyser` -- a GUI tool to compute transfer entropy on a chosen data set with the toolkit, and also automatically generate code in Java, Python and Matlab to show how to do this calculation with the toolkit.
  * [SimpleJavaExamples](SimpleJavaExamples) -- `demos/java` -- a set of basic examples using the Java toolkit;
  * Several demo sets mirror the `SimpleJavaExamples` to demonstrate the use of the toolkit in non-Java environments:
   * [OctaveMatlabExamples](OctaveMatlabExamples) -- `demos/octave` -- basic examples on using the Java toolkit from Octave or Matlab environments;
   * [PythonExamples](PythonExamples) -- `demos/python` -- basic examples on using the Java toolkit from Python using the JPype interface;
   * [R_Examples](R_Examples) -- `demos/r` -- basic examples on using the Java toolkit from R using the rJava interface;
   * [JuliaExamples](JuliaExamples) -- `demos/julia` -- basic examples on using the Java toolkit from Julia;
   * [Clojure_Examples](Clojure_Examples) -- `demos/clojure/examples` -- basic examples on using the Java toolkit from Clojure;
  * [SchreiberTeDemos](SchreiberTeDemos) -- `demos/octave/SchreiberTransferEntropyExamples` -- using the toolkit to reproduce the transfer entropy examples originally included in Schreiber's 2000 paper introducing transfer entropy;
  * [CellularAutomataDemos](CellularAutomataDemos) -- `demos/octave/CellularAutomata` -- using the Java toolkit to plot local information dynamics profiles in cellular automata; the demo is run under Octave or Matlab;
  * [DetectingInteractionLags](DetectingInteractionLags) -- `demos/octave/DetectingInteractionLags` -- demonstration of using the transfer entropy with source-destination lags; the demo is run under Octave or Matlab;
  * [InterregionalTransfer](InterregionalTransfer) -- `demos/java/interregionalTransfer` -- higher level example using collective transfer entropy to infer effective connections between "regions" of data;
  * [NullDistributions](NullDistributions) -- `demos/octave/NullDistributions` -- investigating the correspondence between analytic and resampled distributions for TE and MI under null hypotheses of no relationship; the demo is run under Octave or Matlab;

You can also review the [JUnitTestCases](JUnitTestCases) -- the test cases for the Java toolkit included in the distribution -- these case also be browsed to see simple use cases for the toolkit.

## Extras

You may also be interested in several [extra](Extras) features that the toolkit has (in addition to the information dynamics calculators); e.g. Octave text file format reading and writing, matrix manipulation, mathematical functions, etc.