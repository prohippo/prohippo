ActiveWatch (AW) is a set of Java modules for finite indexing of text.
It represents text items as M-dimensional numerical vectors, where M is on
the order of 10⁴. AW notably employs a statistically scaled similarity
measure between pairs of vectors as an alternative to the cosine similarity
of Gerard Salton.

An AW index set consists of finitely many user-selected full words plus
finitely many high-frequency English word fragments. Fragmentary
indices allow an approximation of indexing by every word. For example,
if the word CONFABULATE is unknown as a full-word index key, we can still
recognize its overlapping fragments: CONF, NFA, FAB, ABU, ULAT, and LATE.

Indexing by fragments will be noisy, but can still be quite effective for
comparing the content of entire text items. Limiting an index set to one
or two thousand selected whole words, five or six thousand selected word
fragments, and about a thousand other indices gives us more manageable
descriptions of text content and simplifies statistical computations.

In particular, we can more reliably estimate the probability of a given
index key showing up in a text item and calculate the probability of a
particular inner product score occurring by chance for a pair of item
vectors. This will establish the parameters of a noise distribution for
scaling inner product similarity scores to make them easier to interpret.

AW will score similarity by the the number of standard deviations that a
raw inner product falls above or below the mean of a noise distribution.
This noise will be roughly Gaussian; an AW scaled similarity of 3 standard
deviations would be significant at about p = .003. With actual text data,
we usually will expect scaled similarity above 5 standard deviations.

Some index tuning is needed to achieve this kind of performance. This will
mainly involve adjustments of the whole-word index keys defined by a user
for particular target text data. We can also improve fragmentary indexing
in general by selecting the fragments more carefully so that they will
subsume occurrences of shorter fragments, which will tend to be noisier.

The first version of AW was written in C around 1982 and was employed for
information discovery in unfamiliar text data. The current Java version
dates back to around 1999, but has some recent tweaks in its linguistic
analysis and its inclusion of 4- and 5-letter word fragments for indexing,
along with the 2- and 3-letter fragments used previously. 

The modules included in the AW GitHub repository mainly provide support for
simple clustering of text items by content. These are organized functionally
by their Java package identifications. The Java code was originally written on
Apple home computers running versions 7.*, 8.*, or 9.* of the Macintosh OS.
This was when Java was still a somewhat new programming language.

Java AW eventually evolved to support many kinds of statistical natural
processing, but this GitHub repository includes only a small subset of modules
for automatic clustering of text items. This software should give you a good
overall idea of what you can do with AW finite indexing and statistically
scaled similarity between pairs of text items.

To build out a basic AW clustering capability, run the 'build' shell script
included with the AW GitHub download. The script is for macOS Darwin Unix and
should be edited for your computing platform. You will have to install a Java
JDK if you do not have one already. Everything in the AW demonstration will
have to run from a command line.

AW software is free for all uses and is released under BSD licensing.

Release History:

v0.1    16jun2021  Initial upload of original AW Java source code.

v0.2    10ju12021  Clean up and reorganize code for SEGMTR module
                   Add code to dump AW output files
                   Collect news data set for demonstration

v0.3    13jul2021  Clean up and debug code in AW table building modules
                   Add unit testing

v0.4    16jul2021  Clean up and reorganize code for INDEXR module
                   Add code to dump AW output files
                   Update to expect UTF-8 text input, not ASCII

v0.5    06aug2021  Clean up code for SEGMTR module
                   Fix problems in UTF-8 handling
                   Add diagnostic tools
                   Build initial versions of AW clustering modules to test

v0.6    12aug2021  Clean up SEGMTR, UPDATR, SEQNCR, SQUEZR, SUMRZR, KEYWDR modules
                   Fix problems in UTF-8 handling, subsegmenting long text items
                   Add and extend diagnostic tools
                   Clean up text data sample for clustering demonstration
                   Edit and update documentation

v0.6.1  14aug2021  Fix mishandling of multi-segment items in AW clustering

v0.7    21aug2021  add and extend diagnostic tools
                   remove phonetic indexing
                   add 4- and 5-gram indices
                   reorganize startup of n-gram analysis
                   clean up problems with deprecation and type casting

v0.7.1  25aug2021  fix bug in LexicalGram, improper breaking out of extraction loop
                   replace incorrect 4-gram and incorrect 5-gram in GramMap lists
                   clean up literal file to align with current 4- and 5-grams
                   fix inconsistent stemming rules in suffix filw
                   simply Updater command line arguments
                   update Dprb for v0.7 changes in n-gram initialization
                   update documentation
