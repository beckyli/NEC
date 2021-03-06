_Demos to show how to compute local information dynamics profiles in cellular automata_

[Demos](Demos) > Cellular Automata demos

## Cellular Automata demos

This demonstration set shows how to compute local information dynamics profiles in (1D) [cellular automata](http://en.wikipedia.org/wiki/Cellular_automaton) (CAs).

It is written for Matlab or Octave.

This demonstration set is found at [demos/octave/CellularAutomata/](../blob/master/demos/octave/CellularAutomata) in the svn or full distribution.

## Code design

`plotLocalInfoMeasureForCA.m` is the main file, which you call supplying arguments specifying the CA, and which local information dynamics measure to profile:

```matlab
% function plotLocalInfoMeasureForCA(neighbourhood, base, rule, cells, timeSteps, measureId, measureParams, options)
%
% Plot one run of the given CA and compute and plot a local information dynamics profile for it
%
% Inputs:
% - neighbourhood - neighbourhood size for the rule (ECA has neighbourhood 3).
%     For an even size neighbourhood (meaning a different number of neighbours on each side of the cell),
%     we take an extra cell from the lower cell indices (i.e. from the left).
% - base - number of discrete states for each cell (for binary states this is 2)
% - rule - supplied as either:
%     a. an integer rule number if <= 2^31 - 1 (Wolfram style; e.g. 110, 54 are the complex ECA rules)
%     b. a HEX string, e.g. phi_par from Mitchell et al. is '0xfeedffdec1aaeec0eef000a0e1a020a0' (note: the leading 0x is not required)
% - cells - number of cells in the CA
% - timeSteps - number of rows to execute the CA for (including the random initial row)
% - measureId - which local info dynamics measure to plot - can be a string or an integer as follows:
%    - 'active', 0 - active information storage (requires measureParams.k)
%    - 'transfer', 1 - apparent transfer entropy (requires measureParams.k and j)
%    - 'transfercomplete', 2 - complete transfer entropy (requires measureParams.k and j)
%    - 'separable', 3 - separable information (requires measureParams.k)
%    - 'all', -1 - plot all measures
% - measureParams - a structure containing options as described for each measure above:
%    - measureParams.k - history length for information dynamics measures
%    - measureParams.j - we measure information transfer across j cells to the right per time step
% - options - a stucture containing a range of other options, i.e.:
%    - plotOptions - structure as defined for the plotRawCa function
%    - seed - state for the random number generator used to set the initial condition of the CA (use this
%       for reproducibility of plots, or to produce profiles for several different measures of the same CA raw states).
%       We set rand('state', options.seed) if options.seed is supplied, and restore the previous seed afterwards.
%    - plotRawCa - default true
%    - saveImages - whether to save the plots or not (default false)
%    - movingFrameSpeed - to investigate a moving frame of reference (default 0) (as in Lizier & Mahoney paper)
```

## Running

Several scripts are available demonstrating how to call `plotLocalInfoMeasureForCA.m` to generate the desired figures; see:
 * [demos/octave/CellularAutomata/GsoChapterDemo2013.m](../blob/master/demos/octave/CellularAutomata/GsoChapterDemo2013.m) to generate figures for: J.T. Lizier, M. Prokopenko and A.Y. Zomaya, "A framework for the local information dynamics of distributed computation in complex systems", in Guided Self-Organization: Inception, edited by M. Prokopenko, pp. 115-158, Springer, Berlin/Heidelberg, 2014;
 * [demos/octave/CellularAutomata/DirectedMeasuresChapterDemo2013.m](../blob/master/demos/octave/CellularAutomata/DirectedMeasuresChapterDemo2013.m) to generate figures for J.T. Lizier,"Measuring the dynamics of information processing on a local scale in time and space", in "Directed Information Measures in Neuroscience", ed. M. Wibral, R. Vicente, J.T. Lizier, Springer, to be published, 2013;
 * [demos/octave/CellularAutomata/TeBook2013.m](../blob/master/demos/octave/CellularAutomata/TeBook2013.m) to generate figures for chapter 5 of T. Bossomaier, L. Barnett, M. Harré and J.T. Lizier, "An Introduction to Transfer Entropy: Information Flow in Complex Systems", Springer, to be published, 2013.
 * [demos/octave/CellularAutomata/movingFrame.m](../blob/master/demos/octave/CellularAutomata/movingFrame.m) to generate figures for: J.T. Lizier, J.R. Mahoney, "Moving frames of reference, relativity and invariance in transfer entropy and information dynamics", Entropy, vol. *15*, no. 1, p. 177-197, 2013; doi: [10.3390/e15010177](http://dx.doi.org/10.3390/e15010177)

In brief, the steps that these scripts demonstrate are as follows:

Make sure that the jar location is entered correctly in `plotLocalInfoMeasureForCA.m`

Set up the `measureParams` and `options` structures, e.g.:

```matlab
measureParams.k = 16; % History length of 16 for info dynamics measures
options.plotOptions.plotRows = 100; % plot only 100 rows
options.plotOptions.plotCols = 100; % plot only 100 columns
options.plotOptions.plotStartRow = 100; % plot from row 100 onwards
options.plotOptions.plotStartCol = 100; % plot from column 100 onwards
```

Then call to plot a CA and a given local information dynamics profile, e.g. for ECA rule 54 and plotting local active information storage:

```matlab
plotLocalInfoMeasureForCA(3, 2, 54, 10000, 600, 'active', measureParams, options);
```

with sample results as follows:

<img src="http://lizier.me/joseph/images/jidt/rule54-rawStates.png" height="300"/> <img src="http://lizier.me/joseph/images/jidt/rule54-activeInfoStorage.png" height="300"/>

Or for the neighbourhood 7 rule \phi_par from Mitchell et al. (see this [paper](http://web.cecs.pdx.edu/~mm/evca-review.pdf)):

```matlab
measureParams.k = 10; % History length of 10 for info dynamics measures
options.plotOptions.plotRows = 100; % plot only 100 rows
options.plotOptions.plotCols = 100; % plot only 100 columns
options.plotOptions.plotStartRow = 10; % plot from row 100 onwards
options.plotOptions.plotStartCol = 100; % plot from column 100 onwards

plotLocalInfoMeasureForCA(7, 2, 'feedffdec1aaeec0eef000a0e1a020a0', 10000, 1000, 'active', measureParams, options);
```

with sample results as follows:

<img src="http://lizier.me/joseph/images/jidt/phiPar-rawStates.png" height="300"/> <img src="http://lizier.me/joseph/images/jidt/phiPar-activeInfoStorage.png" height="300"/>

To make several local information profiles for the one CA run (with the same initial CA state for each plot), set `options.seed` to a fixed value, and call `plotLocalInfoMeasureForCA` for each measure separately.

## References

The code can also be used to reproduce results from the following papers (these were originally produced with an earlier toolkit):
 * J.T. Lizier, M. Prokopenko and A.Y. Zomaya, "Local information transfer as a spatiotemporal filter for complex systems", _Physical Review E_, vol. *77*, 026110, 2008. doi: [10.1103/PhysRevE.77.026110](http://dx.doi.org/10.1103/PhysRevE.77.026110)
 * J.T. Lizier, M. Prokopenko and A.Y. Zomaya, "Information modification and particle collisions in distributed computation", _Chaos_, vol. *20*, no. 3, 037109, 2010; doi: [10.1063/1.3486801](http://dx.doi.org/10.1063/1.3486801)
 * J.T. Lizier, M. Prokopenko and A.Y. Zomaya, "Local measures of information storage in complex distributed computation", _Information Sciences_, vol. *208*, pp. 39-54, 2012; doi: [10.1016/j.ins.2012.04.016](http://dx.doi.org/10.1016/j.ins.2012.04.016)