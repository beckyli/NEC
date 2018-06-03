_How to install and start using the toolkit_

## Introduction

Here we describe how to install and start using the toolkit (it's pretty simple!)

## Download

Download the latest distribution; either (note: these distributions are suitable for all platforms):
 1. git repository -- by taking a `git clone` of this repo. This is the bleeding edge to stay right up to date. See [https://github.com/jlizier/jidt](https://github.com/jlizier/jidt) for repo details, and [AntScripts](AntScripts) for build instructions as you will have to build it yourself from the repo.
 1. [v1.4 full distribution](http://lizier.me/joseph/software/jidt/download.php?file=infodynamics-dist-1.4.zip) -- this is *recommended* for most users (includes jar file, javadocs, demonstrations, unit tests and build scripts); or
 1. [v1.4 jar](http://lizier.me/joseph/software/jidt/download.php?file=infodynamics-jar-1.4.zip) only (use only if you don't need much guidance on how to use the toolkit);

See all distributions and brief descriptions at [Downloads](Downloads).

## Dependencies

None! You don't need any other downloads to start using this code _in general_.

There are only dependencies if:
 1. You don't have java installed - [download the Java SE / JDK](http://www.oracle.com/technetwork/java/javase/overview/index.html). It's better to install the JDK (development kit) instead of [JRE](http://java.com/) (runtime environment), since this will allow you to make Java code changes instead of only running the java code;
 1. You wish to (re-)build the project (if you're changing the source files or using an svn checkout) using the `build.xml` script - this requires [ant](http://ant.apache.org/). See [AntScripts](AntScripts) for build instructions;
 1. You wish to run the JUnit test cases - this requires [JUnit](http://www.junit.org/) - for how to run JUnit with our ant script see [JUnitTestCases](JUnitTestCases) and [AntScripts](AntScipts);
 1. Additional preparation may be required to use JIDT in GNU Octave or Python; see [UseInOctaveMatlab](UseInOctaveMatlab) or [UseInPython](UseInPython) respectively.

## Install

If you have one of the distributions:
 1. Unzip the distribution to a location of your choice, and/or move the `infodynamics.jar` file to a relevant location. Ensure that `infodynamics.jar` is on the Java classpath when your code attempts to access it (see e.g. [SimpleJavaExamples](SimpleJavaExamples));
 1. To update to a new version, simply copy the new distribution over the top of the previous one.

Otherwise, if you are running with the source code via git, see [AntScripts](AntScripts) regarding running `ant` to generate `infodynamics.jar`.

That's it.

## Usage

See [Documentation](Documentation) and [Demos](Demos) for some guided examples on getting started and using the code.