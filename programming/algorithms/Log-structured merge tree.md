# Log-structured merge tree (LSM tree)

LSMs are the data structure that back many [[No-SQL]] database products.  They are designed to tolerate high write volumes without performance loss by doing all initial writes on in-memory data structures. 

An LSM tree is the combination of an in-memory key value store and accompanying index (the 'frontend', often called a `MemTable`), and a set of [[Sorted string table]]s.  Writes will be performant regardless of the size of the total data structure because they are always initially performed on the in-memory frontend.  The frontend is periodically flushed to disk as the latest SST.

Reads are searched-for in the frontend first.  If the requested keys are not found, the keys must be searched-for somewhere in the on-disk SSTs.  To eliminate the random IO of searching through all these SSTs, the MemTable also stores a summary table that tracks the min-max data ranges of each disk block on every level.  This allows the search to skip some disk blocks upfront.  Naive requests for a non-existing key would trigger an IO-intensive search through every disk block with an appropriate range, so in addition to the summary table, [[Bloom filter]]s are maintained for each level that can give a definitive 'no' as to whether or not a given level contains a particular key, which eliminates futile searching.

Updates and deletes do not modify on-disk SSTs.  Instead they are added to the in-memory frontend (a `delete` is indicated by a special 'tombstone' record).  Because the indices are always searched in sequence, the most recent version of a given record will always be found and returned first.  

As records accumulate, the number of SSTs on disk will grow, eventually impacting performance and storage requirements.  To alleviate this issue, existing SSTs are periodically merged, or compacted, using a mechanism similar to [[Merge sort]].  Newer `update` or `delete` records will overwrite older entries at this point, freeing up disk space.  

The arrangement of on-disk SSTs is important for the specific compaction mechanism used.  In general SSTs are kept in a tiered structure, where the size of the SSTs in each tier increases exponentially from the preceding tier.  The smallest SSTs are those closest to the `MemTable`, i.e. they are the tier into which the `MemTable` is periodically flushed to disk.  These small tables are then periodically merged with the larger tables beneath, and so on.

Tuning the merging/compaction process is the most critical aspect of implementing the LSM tree.  Different compaction and leveling implementations can be used to achieve a different performance profile.  For example, Cassandra DB uses a compaction process designed to optimize write performance, while Rocks DB is optimized for reading.