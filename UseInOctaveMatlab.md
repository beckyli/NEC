_How to use the toolkit in Octave or Matlab_

## Introduction

The java code from this toolkit can easily be used in Octave or Matlab. This page contains basic information on how to get up and running with the toolkit:
  * [Matlab](#use-in-matlab) instructions
  * [Octave](#use-in-octave) instructions

Several longer examples of using the toolkit in Octave/Matlab can be viewed at [OctaveMatlabExamples](OctaveMatlabExamples).

## Use in Matlab

The ability to use Java from within Matlab comes with Matlab out of the box. Full info is available at:
  * http://au.mathworks.com/help/matlab/using-java-libraries-in-matlab.html
  * http://au.mathworks.com/help/matlab/matlab_external/product-overview.html

You can run your Java code inside Matlab fairly simply:
  1. Tell Matlab about your jar, e.g.: `javaaddpath('../Information Dynamics/infoDynamics.jar');`
  1. Create an instance of a class, e.g. by direct instantiation `miCalc = infodynamics.measures.continuous.kernel.MutualInfoCalculatorMultiVariateWithDiscreteKernel();` or using `miCalc = javaObject('infodynamics.measures.continuous.kernel.MutualInfoCalculatorMultiVariateWithDiscreteKernel')`
  1. Use the object: `miCalc.initialise(4, 2, 0.5);`
  1. Note that Matlab automatically makes conversion between its own and Java arrays.

For _static_ methods, note that you can simply call it on the class itself, or on  an object of the class - see http://www.mathworks.com.au/help/techdoc/matlab_external/f46719.html#f23705

If you get any `java.lang.OutOfMemoryError` errors, then you need to increase the heap space allocated by Matlab (it is usually set to a rather low value) -- doing this is described e.g. [here](http://au.mathworks.com/help/matlab/matlab_external/java-heap-memory-preferences.html).

Finally, sometimes Matlab can give warnings such as `Warning: Objects of infodynamics/measures/continuous/kraskovTransferEntropyCalculatorMultiVariateKraskov class exist - not clearing java`. To get rid of these errors, then you can clear the relevant Java variables in Matlab, e.g. `clear teCalc`, or clear all Java variables: `clear java`.

See longer code examples at [OctaveMatlabExamples](OctaveMatlabExamples).

## Use in Octave

Here I will describe material I found useful to get started with Java inside Octave, then how I installed octave-java, then how to run the code.

For octave 3.8 onwards, java functionality is natively available (this is the version carried for ubuntu 14.04, which I'm currently using).

_Otherwise_, material that I found useful regarding using Java code inside Octave:
  * http://sourceforge.net/mailarchive/forum.php?thread_name=128f38bd0911170856i2d9dc349x28e02b3fe3333011%40mail.gmail.com&forum_name=octave-dev
  * http://octave.1599824.n4.nabble.com/How-do-I-install-the-java-and-jhandles-packages-td1632116.html
  * http://www.octave.org/wiki/index.php?title=Java_package

Here is a list of how I got octave-java installed prior to octave 3.8 (i.e. on ubuntu 12.04 for me):
  1. Set-up steps:
    1. Set up an environment variable for JAVA_HOME - for me `/usr/lib/jvm/java-6-openjdk-amd64`
    1. Make sure that `$JAVA_HOME/jre/lib/<ARCH>/client/libjvm.so` exists - on 64-bit machines, the required file exists in `server` directory, not `client`. We can get around this by adding a symlink - I created the directory `client` and symlink from inside the `client` directory to the file in the `server` directory. I've been told that an alternative fix is to change the `_java_.cc` file as described [here](http://sourceforge.net/mailarchive/message.php?msg_id=28038447).
  1. Install [octave-java](http://octave.sourceforge.net/java/) from the [Octave-forge project](http://octave.sourceforge.net/) either:
    1. through your linux package manager (this didn't work properly for me on ubuntu 12.04), or
    1. via directly downloading the `.tar.gz` file from http://octave.sourceforge.net/java/ then starting octave in root mode (`sudo octave`), and inside octave run the installation, e.g.: `pkg install -verbose java-1.2.8.tar.gz`. To uninstall at a later date, you can run: `pkg uninstall java`. After running the installation in root mode, you will need to add read access for yourself to the `doc.info` file for running the `doc java` command.

Once all that is set up, you can run your java code just as simply as in Matlab:
  1. Tell octave-java about your jar, e.g.: `javaaddpath('../Information Dynamics/infoDynamics.jar');`
  1. Create an instance of a class, e.g.: `miCalc = javaObject("infodynamics.measures.continuous.kernel.MutualInfoCalculatorMultiVariateWithDiscreteKernel");`
  1. Use the object: `miCalc.initialise(4, 2, 0.5);`
  1. While Matlab automatically makes conversion between its own and Java arrays, Octave does not. To facilitate such conversion, scripts are provided for converting arrays back and forth between these environments in the `demos/octave` directory; see further discussion at OctaveJavaArrayConversion and example uses in [OctaveMatlabExamples](OctaveMatlabExamples).

For _static_ methods, you can call them on an object of the class itself, or using the javaMethod function - http://octave.sourceforge.net/java/function/javaMethod.html

See longer code examples at [OctaveMatlabExamples](OctaveMatlabExamples).