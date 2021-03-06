_Description of how to build the project_

## Introduction

Users may wish to build the code, perhaps if they are directly accessing the source files via svn or modifying the files. The source code may be compiled manually of course, or in your favourite IDE (Integrated Development
Environment), however JIDT provides an `ant` build script at the top level of the distribution, [build.xml](../blob/master/build.xml), to streamline this process.

Apache ant (see http://ant.apache.org for description and downloads) is a command-line tool to build various interdependent targets in software projects, much like the older style Makefile for C/C++.

## Running ant

To build any of the following targets using [build.xml](../blob/master/build.xml), run `ant <targetName>` in the top-level directory of the distribution, where `<targetName>` may be any of the following:
 * `build` or `jar` (this is the default if no `<targetName>` is supplied) -- creates a jar file for the JIDT library;
 * `compile` -- compiles the JIDT library and unit tests;
 * `junit` -- runs the unit tests as decsribed at [JUnitTestCases](JUnitTestCases) (note that some dependencies are described there);
 * `javadocs` -- generates automated Javadocs from the formatted comments in the source code;
 * `jardist` -- packages the JIDT jar file in a distributable form, as per the jar-only distributions of the project;
 * `dist` -- runs unit tests, and packages the JIDT jar file, Javadocs, demos, etc in a distributable form, as per the full distributions of the project;
 * `clean` -- delete all compiled code etc built by the above commands.