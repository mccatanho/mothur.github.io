---
title: 'collect.shared'
tags: 'commands'
redirect_from: '/wiki/Collect.shared.html'
---
The **collect.shared** command generates
collector's curves for [calculators](calculators), which
describe the similarity between communities or their shared richness.
Collector's curves describe how richness or diversity change as you
sample additional individuals. If a collector's curve becomes parallel
to the x-axis, you can be reasonably confident that you have done a good
job of sampling and can trust the last value in the curve. Otherwise,
you need to keep sampling. mothur has the ability to generate data for
collector's curves much the same way that sons did; however, sons
presented the data in the sons file, which was virtually impossible for
novices to parse. mothur fixes many of these issues by generating
separate files for each estimator. For this tutorial you should download
and decompress [ patient70data.zip](https://mothur.s3.us-east-2.amazonaws.com/wiki/patient70data.zip)

## Default settings

To execute the collect.shared() command you first need to have run the
[make.shared](make.shared) command with the list and group
options. For example:

    mothur > make.shared(list=patient70.fn.list, group=patient70.tissue_stool.groups)

By default, the collect.shared() command will randomize the order in
which the individuals are sampled. So if you run collect.shared()
multiple times, you will get slightly different results. The
collector's curve data for several
[calculators](calculators) is generated by default with the
following command:

    mothur > collect.shared(shared=patient70.fn.shared)

This will result in output to the screen looking like:

    unique 1
    0.00   2
    0.01   3
    0.02   4
    0.03   5
    0.04   6
    0.05   7
    0.06   8
    0.07   9
    0.08   10
    0.09   11
    0.10   12

The left column indicates the label for each line in the data set and
the right column indicates the row number in the data set. Execution of
collect.shared() will generate 11 files, one for each of the
calculators. If you look at patient70.fn.shared.sobs you will see
something like:

    sampled    uniquetissuestool   0.00tissuestool 0.01tissuestool 0.02tissuestool 0.03tissuestool
    1  1           1       1       1       1
    100    90          78      56      35      31
    200    173         123     75      58      46
    300    250         163     93      66      57
    400    324         203     106     74      61
    500    395         233     124     80      68
    600    463         263     131     89      70
    ...

In this file the first column tells you how many sequences have been
sampled; this would typically be plotted on the x-axis of a graph. Each
subsequent column has a heading, which indicates the label for the line
being analyzed from your OTU data file concatenate to the names of the
two groups being compared. The data in the column provides the estimator
value as indicated by the name of the file. For example, in the above
examples, after sampling 600 sequences there were 463 OTUs shared
between the tissue and stool samples when an OTU was defined as a group
of identical sequences. By default, collect.shared() prints output every
100 sequences.

## Options

### calc

If you are not interested in producing collector's curves for all of
the calculators, it is possible to select the calculators you want using
the calc option:

    mothur > collect.shared(shared=patient70.fn.shared, calc=sharedsobs-sharedchao)

This command would only generate the files patient70.fn.shared.sobs and
patient70.fn.shared.chao.

### label

There may only be a couple of lines in your OTU data that you are
interested in generating collector's curves for. There are two options.
You could: (i) manually delete the lines you aren't interested in from
your list file; (ii) or use the label option. To use the label option
with the collect.shared() command you need to know the labels you are
interested in. If you want the collector's curve data for the lines
labeled unique, 0.03, 0.05 and 0.10 you would enter:

    mothur > collect.shared(shared=patient70.fn.shared, label=unique-0.03-0.05-0.10)

In the file patient70.fn.shared.sobs you would see something like:

    sampled    uniquetissuestool   0.03tissuestool 0.05tissuestool 0.10tissuestool 
    1  1           1       1       1
    100    92          26      24      16
    200    179         39      34      24
    300    258         51      38      27
    400    332         57      47      29
    500    404         64      49      29
    600    473         67      51      31

### freq

For larger datasets you might not be interested in obtaining all of the
data for the number of sequences sampled. For instance, if you have
100,000 sequences, you may only want to output the data every 100
sequences. Alternatively, if you only have 100 sequences, you may only
want to output all of the data. The default setting is to output data
every 100 sequences. By altering the freq option you can set the
frequency that the analysis is performed:

    mothur > collect.shared(shared=patient70.fn.shared, freq=1)

or

    mothur > collect.shared(shared=patient70.fn.shared, freq=1000)

or you set set the frequency as a percentage of the number of sequences.
For example to output after 25%:

     mothur > collect.shared(shared=patient70.fn.shared, freq=0.25)

The second command would generate data such as this in the
patient70.fn.shared.sobs file:

    sampled    uniquetissuestool   0.00tissuestool 0.01tissuestool 0.02tissuestool 0.03tissuestool 0.04tissuestool 0.05tissuestool     
    1  1           1       1       1       1       1       1
    1000   711         361     167     102     80      69      60
    2000   1351            506     205     119     94      80      74
    3000   1976            619     237     129     99      88      83
    4000   2519            688     255     138     107     91      84
    4392   2742            713     257     138     111     94      84

### groups

If you had started this tutorial with the following comamnds:

    mothur > make.shared(list=patient70.fn.list, group=patient70.sites.groups)
    mothur > get.group(shared=patient70.fn.shared)

You would have seen that there were 7 groups here: 70A-70F and 70S. The
sequences from 70S were collected from Patient 70's stool sample those
from samples 70A-70F were from their mucosa. These 7 groups would yield
21 pairwise comparisons if you ran the **collect.shared** command; however,
if you were only interested in the comparisons between each mucosa site
and the stool sample you could use the group option:

    mothur > collect.shared(shared=patient70.fn.shared, calc=sharedsobs, groups=70A-70S)
    mothur > collect.shared(shared=patient70.fn.shared, calc=sharedsobs, groups=70B-70S)
    mothur > collect.shared(shared=patient70.fn.shared, calc=sharedsobs, groups=70C-70S)
    mothur > collect.shared(shared=patient70.fn.shared, calc=sharedsobs, groups=70D-70S)

Alternatively, if you want all of the pairwise comparisons you can
either not include the group option or set it equal to "all".

    mothur > collect.shared(shared=patient70.fn.shared, calc=sharedsobs, groups=all)

### all

The sharedsobs and sharedchao calculators not only do the pairwise
estimates, but also estimate the shared richness of all the groups in
your file. This calculation is RAM intensive. If your RAM is limited and
you have a large number of groups this may result in a crash, so by
default the all parameter is set to false. To calculate the shared
richness of all your groups, set the all parameter to true.

    mothur > collect.shared(shared=patient70.fn.shared, calc=sharedsobs-sharedchao, all=true)

## Revisions

-   1.40.0 - Speed and memory improvements for shared files.
    [\#357](https://github.com/mothur/mothur/issues/357) ,
    [\#347](https://github.com/mothur/mothur/issues/347)
-   1.41.0 - Bug Fix "\[error\]: requesting groups not present in
    files, aborting." error
    [\#497](https://github.com/mothur/mothur/issues/497)

