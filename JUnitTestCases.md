_How to find and run the JUnit test cases included in the full distribution_

## Introduction

The full distribution also includes the JUnit test cases used to test the java code. These test cases can be browsed to see simple use cases of the java toolkit. Attempting to run them is also a good way to check that the source code compiles and runs ok on your machine.

## Location

The java source code for the unit tests is at [java/unittests](../blob/master/java/unittests) in the distribution.

## Dependencies

To run the JUnit test cases, you will need to have a `junit.jar` file on your classpath, either:
  * in your IDE if you're running the junit test cases there; or
  * supplied to `ant` if you're running the junit test cases via our `build.xml` ant file as described at [AntScripts](AntScripts) -- see the [JUnit task](http://ant.apache.org/manual/Tasks/junit.html) in the ant documentation for more information on how the junit.jar could be supplied to ant. The `build.xml` file is currently implementing option 1 from that page - the required jar files are in `ANT_HOME/lib`. (I have the `ant` and `junit` packages installed on ubuntu 12.04, which already puts those jars in the location I am referencing).

I've been using ant 3.8.2; it does not appear to be compatible with later versions.

## Running via ant

Make sure that junit.jar is available to ant, as above. Then in the main distribution directory as described at [AntScripts](AntScripts) run: `ant junit`. This compiles and then runs the unit tests.