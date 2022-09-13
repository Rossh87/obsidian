# Sorted string table (SS table)

A sorted string table is just a file that is filled with binary blobs of key-value pairs, sorted by key.  The structure is very simple: duplicate keys are fine, there is no special padding, etc.  It is a simple and effective structure for exchanging large segments of sorted data.

The fact that the info is already sorted makes building an index very easy: simply read the file into memory and create an index table by pairing each key with the appropriate byte offset of its value in the file.

The file itself is immutable, since inserting or deleting would require very IO-intensive rewriting.