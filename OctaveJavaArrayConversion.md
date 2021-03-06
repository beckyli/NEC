_Issues and workarounds for converting arrays between Octave and Java format_

## Octave-Java array conversion

Conversion between native octave array types and java arrays is not straightforward (particularly for multidimensional arrays, or int arrays).

On this page, we describe these [issues](#issues), and then describe the [scripts](#scripts-to-workaround-the-issue) provided to perform the array conversion for you. Some [links](#links) about the issues are provided as well.

## Issues

One can generally call java methods which require a single dimensional `double[]()` array by passing in a native octave single dimensional array (e.g. see [OctaveMatlabExamples-Example_1](OctaveMatlabExamples#example-1---transfer-entropy-on-binary-data)).

This does not work however for multidimensional arrays, or int arrays: octave often reports that a method is not found when one tries to call a method requiring one of these types as an argument with a simple octave array as the argument.

One could create arrays of the required Java type inside octave (e.g. `jDoubleMatrix = javaArray('java.lang.Double', 2, 3);`) and then convert each element in an octave array into this java array. However, a. this can be time consuming, and b. this can't be done with integer arrays anyway.

## Scripts to workaround the issue

We have supplied scripts to make these conversions simple for the user, and indeed to make them as efficiently as possible.

These scripts are available at [demos/octave](../blob/master/demos/octave) in the svn or main distributions, and are the following files:
 * [octaveToJavaDoubleArray.m](../blob/master/demos/octave/octaveToJavaDoubleArray.m) - convert native octave vector to a java `double[]`
 * [octaveToJavaDoubleMatrix.m](../blob/master/demos/octave/octaveToJavaDoubleMatrix.m) - convert native octave matrix to a java `double[][]` matrix
 * [octaveToJavaIntArray.m](../blob/master/demos/octave/octaveToJavaIntArray.m) - convert native octave vector to a java `int[]` array
 * [octaveToJavaIntMatrix.m](../blob/master/demos/octave/octaveToJavaIntMatrix.m) - convert native octave matrix to a java `int[][]` matrix
 * [javaMatrixToOctave.m](../blob/master/demos/octave/javaMatrixToOctave.m) - convert a java array or matrix (either `int` or `double`) to a native octave matrix

See example use in [OctaveMatlabExamples-Example_2](OctaveMatlabExamples#example-2---transfer-entropy-on-multidimensional-binary-data) for octave-to-java conversion, and [OctaveMatlabExamples-Example_4](OctaveMatlabExamples#example-4---transfer-entropy-on-continuous-data-using-kraskov-estimators) for java-to-octave conversion.

The conversion is performed using the `infodynamics.utils.OctaveMatrix` class (which extends the `org.octave.Matrix` class that is distributed and installed with the `octave-java` package).
We extended `org.octave.Matrix` so that we had access to new conversion routines for `int` data.
If you examine the source code of [octaveToJavaDoubleArray.m](../blob/master/demos/octave/octaveToJavaDoubleArray.m) or [octaveToJavaDoubleMatrix.m](../blob/master/demos/octave/octaveToJavaDoubleMatrix.m) you will see that we simply create a `infodynamics.utils.OctaveMatrix` object from the octave matrix, telling it the dimensions of that matrix, then extract the Java array object of the required type.

The _reverse_ conversion is performed with the `javaMatrixToOctave` script, which uses the `java_convert_matrix` feature (to automatically convert `org.octave.Matrix` to octave native types).

In Matlab, matrices are converted back and forth to java format automatically. To ensure that your code can be used in either Matlab or Octave, you can call our conversion scripts - they will work in either Matlab or Octave: in Matlab, they simply return the matrix that was passed in.

## Caveats

Note that there are still some arrays that Octave will not recognise even with this conversion, e.g. see `sourceArray=(rand(100,1)>0.5)*1;` in [OctaveMatlabExamples - Example 1](OctaveMatlabExamples#example-1---transfer-entropy-on-binary-data). This line contains a `*1` to convert the `Boolean` array into something that Octave will recognise as an integer array -- without the `*1` the line will not work, even if we wrap it in a `octaveToJavaIntArray` conversion.
More information is provided by looking at the output of:

```matlab
javaMethod('get', 'java.lang.reflect.Array', (rand(100,1)>0.5), 1);
```

which gives the error `java.lang.IllegalArgumentException: Argument is not an array`, whereas if one adds the `*1` then this error does not occur. It seems that Octave simply does not recognise `rand(100,1)>0.5)` as any type of array, though it is unclear why.

## Links

Some helpful links if you want to know more:
 * [https://mailman.cae.wisc.edu/pipermail/help-octave/2012-February/050306.html](https://mailman.cae.wisc.edu/pipermail/help-octave/2012-February/050306.html)
 * [http://sourceforge.net/mailarchive/message.php?msg_id=27308769](http://sourceforge.net/mailarchive/message.php?msg_id=27308769)