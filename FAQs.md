_Frequently asked questions about the toolkit_

On this page, we list several **frequently asked questions** about the toolkit (these are mostly excerpts from emails):
 * [What do I do about java.lang.OutOfMemoryError?](#what-do-i-do-about-javalangoutofmemoryerror)
 * [How can I build JIDT from the latest SVN sources?](#how-can-i-build-jidt-from-the-latest-svn-sources)
 * [How fast is the toolkit, e.g. for transfer entropy estimation?](#how-fast-is-the-toolkit-eg-for-transfer-entropy-estimation)
 * [What does it mean if I get negative results from a Kraskov-Stoegbauer-Grassberger estimator?](#what-does-it-mean-if-i-get-negative-results-from-a-kraskov-stoegbauer-grassberger-estimator)
 * [Can the Kraskov-Stoegbauer-Grassberger estimator add noise to the data?](#can-the-kraskov-stoegbauer-grassberger-estimator-add-noise-to-the-data)
 * [Why are my results from a Kraskov-Stoegbauer-Grassberger estimator stochastic?](#why-are-my-results-from-a-kraskov-stoegbauer-grassberger-estimator-stochastic)
 * [How do I set the Kraskov-Stoegbauer-Grassberger estimator for transfer entropy to use algorithm 2?](#how-do-i-set-the-kraskov-stoegbauer-grassberger-estimator-for-transfer-entropy-to-use-algorithm-2)

### What do I do about `java.lang.OutOfMemoryError`?

Getting `java.lang.OutOfMemoryError` errors means that the heap space allocated to your JVM instance is not large enough for your program.

If you are running Java directly, then you can increase the maximum heap space by adding an argument to the `java` command such as `-Xmx512M` to request 512 MB heap space, for example.

When running Java from other environments, e.g. in an IDE, in Matlab, GNU Octave, Python etc, you will need to specify this parameter in a manner dependent on that environment:
 * Matlab often gives this error because the heap space is usually set to a rather low value. Increasing the heap space allocated by Matlab to the JVM is described e.g. [here](http://www.mathworks.com.au/help/matlab/matlab_env/preferences.html#bsemees-1).
 * For Python via JPype, you can specify this parameter when calling the `startJVM()` function; see comments in the PythonExamples.
 * For Julia, you can specify this parameter when calling the `JavaCall.init()` method; see comments in the JuliaExamples.

### How can I build JIDT from the latest SVN sources?

If you need one of the latest features that are only available via SVN (or you want to grab the source code and make some changes), you can grab the source and build `infodynamics.jar` as follows:

1. Make an SVN checkout, e.g.:

```
svn checkout http://information-dynamics-toolkit.googlecode.com/svn/trunk/ information-dynamics-toolkit-read-only
```

or update an existing SVN checkout:

```
svn update
```

2. Compile the code and build your own `infodynamics.jar`:

```
ant jar
```

### How fast is the toolkit, e.g. for transfer entropy estimation?

I've had some enquiries regarding how long the toolkit will take to compute transfer entropy on large data sets, say 100 000 samples.
The answer depends mostly on the type of data that you are calculating transfer entropy on:
 1. *Is it discrete or discretized data?* [infodynamics.discrete.ApparentTransferEntropyCalculator](http://code.google.com/p/information-dynamics-toolkit/source/browse/trunk/java/source/infodynamics/measures/discrete/ApparentTransferEntropyCalculator.java) is very fast, on the order of 1 sec or less for this sized data.
 1. *Is it continuous data (that you would prefer not to discretize)?* This is generally slower, using techniques such as a Kraskov-Grassberger estimator (this is the best of breed for continuous valued data), i.e. [infodynamics.measures.continuous.kraskov.TransferEntropyCalculatorKraskov](http://code.google.com/p/information-dynamics-toolkit/source/browse/trunk/java/source/infodynamics/measures/continuous/kraskov/TransferEntropyCalculatorKraskov.java), but not too far behind. At v1.0, a 100 000 time step calculation would take almost an hour with this estimator; however with the recent implementation of a fast-neighbour search algorithm (from v1.1 onwards) this has dropped to (sub?) seconds. If you want the calculation to run faster than that, then you could discretize your data (at the expense of accuracy), or subsample (say into 10 data sets of 10 000 time steps, and average over these. This will be a little less accurate, but you will get a standard error measurement from this approach as well). You can test out how long the code takes to run e.g. with [example4](SimpleJavaExamples#Example_4_-_Transfer_entropy_on_continuous_data_using_Kraskov_es) in the simple java demos (mirrored in the simple octave/matlab demos [here](OctaveMatlabExamples#Example_4_-_Transfer_entropy_on_continuous_data_using_Kraskov_es) and the python demos [here](PythonExamples#Example_4_-_Transfer_entropy_on_continuous_data_using_Kraskov_es)), by altering the length of the random data that is used.

### What does it mean if I get negative results from a Kraskov-Stoegbauer-Grassberger estimator?

You need to think about the output of the KSG algorithm (for mutual information, conditional MI or transfer entropy) as an estimation from a finite amount of empirical data. All estimators have a bias and variance w.r.t. the true value from underlying generating PDF. The KSG estimator seeks to eliminate the bias (under some broad assumptions), but will still have variance. So, when the true value from the underlying generating PDF would have been zero (or close to zero) MI or TE, then the bias correction in the KSG estimator should deliver an expected result around zero, and the variance around that value will mean that you will see a lot of negative results.

So, getting a negative value simply means that the relationship you've measured is less than the expected value if the variables were not related. Taking the variance into account, it would be likely that the result was consistent with no relationship between the variables. (It's possible also that your results can be more strongly skewed negative if your variable don't have a directed relationship the MI or TE is measuring for, but also don't satisfy the KSG estimators broad assumptions.)

### Can the Kraskov-Stoegbauer-Grassberger estimator add noise to the data?

The [original publication](http://dx.doi.org/10.1103/PhysRevE.69.066138) of the KSG estimator recommends the addition of a very small amount of noise to the data (e.g 1e-8) to address the situation where multiple data points share the same value in (at least) one dimension.

This can be done for each KSG estimator in JIDT (for MI basec calculators from v1.0, for conditional MI based calculators from v1.1) as shown below for the transfer entropy estimator:

```
// The following is Java code; change it to your own language if required
TransferEntropyCalculatorKraskov teCalc =
		new TransferEntropyCalculatorKraskov();
teCalc.setProperty("NORMALISE", "true"); // Normalise the individual variables (default)
// Set up to add noise with standard deviation of 0.00000001 normalised units
teCalc.setProperty("NOISE_LEVEL_TO_ADD", "0.00000001");
// Then use the calculator as normal ...
```

*Please note*: as of release v1.3 the addition of noise using the KSG estimator is switched on by default.

Importantly -- the addition of noise means that the results of the KSG estimators become (slightly) stochastic. If you need to produce repeatable results, then you can simply turn off the noise addition by setting property `NOISE_LEVEL_TO_ADD` to `0`. (If you still need noise added, but want this to be repeatable, then I suggest you do this yourself before calling JIDT, using a fixed random number seed).

More details are shown in the [Javadocs](Documentation) for the `setProperty(String, String)` method for each relevant calculator.

### Why are my results from a Kraskov-Stoegbauer-Grassberger estimator stochastic?

See the FAQ [Can the Kraskov-Stoegbauer-Grassberger estimator add noise to the data?](#can-the-kraskov-stoegbauer-grassberger-estimator-add-noise-to-the-data), including the suggestion on how to turn this feature off if you need to.

### How do I set the Kraskov-Stoegbauer-Grassberger estimator for transfer entropy to use algorithm 2?

The MI and conditional MI estimators using the KSG algorithms have separate classes for each of the KSG algorithms (1 and 2), being e.g. `MutualInfoCalculatorMultiVariateKraskov1` and `MutualInfoCalculatorMultiVariateKraskov2`. However, for Transfer Entropy there is only one available class `TransferEntropyCalculatorKraskov` which uses algorithm 1 by default.

To use algorithm 2 here, one should set the property "ALG_NUM" to have value "2", i.e. have a statement:

```
teCalcKSG2.setProperty("ALG_NUM", "2");
```

before the calculator is initialised. One can switch the calculator back to algorithm 1 by setting this property to have value "1".