_How to use the toolkit in Julia_

## Introduction

The Java code from this toolkit can easily be used in [Julia](http://julialang.org/).

Here we give only a brief overview of calling Java code from [Julia](http://julialang.org/); several longer examples of using the JIDT toolkit in Julia can be viewed at [JuliaExamples](JuliaExamples).

## Using Java objects in Julia

First, you need to install the [JavaCall](http://aviks.github.io/JavaCall.jl/) package in Julia; this is done inside a Julia session by calling: `Pkg.add("JavaCall")`.

You can then run your Java code in Julia as follows:
 1. Include the `JavaCall` package with command: `using JavaCall;`
 1. Initialise the `JavaCall` package and tell it where our `infodynamics.jar` file is, e.g.: `JavaCall.init(["-Djava.class.path=$(jarLocation)"]("-Xmx128M",));`
 1. Import the classes you wish to use, e.g. `teClass = @jimport infodynamics.measures.discrete.TransferEntropyCalculatorDiscrete;`.
 1. Create an instance of the calculator you wish to use, e.g. `teCalc = teClass((jint,jint,), 2, 1)`
 1. Call methods on the object, passing in the return type of the method and a tuple of argument types and the arguments themselves, e.g. or `jcall(teCalc, "getPastCount", int,(int,))`, or `jcall(teCalc, "initialise", Void,())` for a void return type and no arguments. See how to specify array types below.

**Array conversion** -- _single dimensional_ arrays can be passed directly back and forth. Take care to indicate their type correctly when passing into a Java method (see [JavaCall docs](http://aviks.github.io/JavaCall.jl/methods.html)), e.g. `jcall(teCalc, "addObservations", Void, (Array{jint,1}, Array{jint,1}), sourceArray, destArray);`. _Multi-dimensional_ arrays however are not yet supported in `JavaCall` (see [here](http://aviks.github.io/JavaCall.jl/)).
We're looking into whether we can make a conversion script to do this manually ...