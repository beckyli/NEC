_How to use the toolkit in Clojure_

# Use in Clojure

The Java code from this toolkit can easily be used in [Clojure](http://clojure.org/) -- the project jar has been deployed to maven as [me.lizier/jidt](https://clojars.org/me.lizier/jidt) for automated inclusion in clojure projects (see further details below).

Here we give only a brief overview of calling Java code from [Clojure](http://clojure.org/); several longer examples of using the JIDT toolkit in Clojure can be viewed at [Clojure_Examples](Clojure_Examples).

# Using Java objects in Clojure

No special installations are required to begin using Java objects in Clojure, these are supported natively as described [here](http://clojure.org/java_interop).

You can run your Java code in Clojure as follows:
 1. Add the `["LATEST"](me.lizier/jidt)` for the latest version (or name a specific version) to the `:dependencies` vector of your `project.clj` file (this automatically references the JIDT jar from the leiningen repository and pulls it in). See our sample [project.clj](../blob/master/demos/clojure/examples/project.clj) file in our [Clojure_Examples](Clojure_Examples).
 1. Import the classes you wish to use, e.g. `(import infodynamics.measures.discrete.TransferEntropyCalculatorDiscrete)`.
 1. Create an instance of the calculator you wish to use, e.g. `(def teCalc (TransferEntropyCalculatorDiscrete. 2 1))`
 1. Call methods on the object, e.g. `(.addObservations teCalc sourceArray destArray)`.

*Array conversion* -- is generally straightforward -- see some details at the [Clojure-Java interoperability documentation](http://clojure.org/java_interop#Java%20Interop-Arrays), and the use of `int-array`, `into-array` and `map` in our [Clojure_Examples](Clojure_Examples).

# Acknowledgements

A big thank you to Matthew Chadwick for showing me how to do this and getting things up and running with clojure and leiningen.