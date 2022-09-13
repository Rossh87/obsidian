# Bloom filter

A Bloom filter is a probabilistic data structure for determining whether or not a given element is a member of a set.  It is probabilistic in the sense that a 'no' is definitive, but a 'yes' has a quantifiable chance of being wrong; that is, the algorithm will occasionally say 'yes' when the answer is in fact 'no'.

The advantage of this structure is that is requires much less memory space than storing the set items themselves.  https://en.wikipedia.org/wiki/Bloom_filter provides a good example use case.