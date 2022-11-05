Databases store data.  Solutions for storing data are often called database management systems, or DBMS. 

In general, picking the correct database is a process of understanding the most common workloads for the application.  Some applications may have very high read volumes, but few writes.  A database that has a good story for [[Replica sets]] or [[sharding]] may be a good choice in this instance.  Other applications may need to accomodate high write volumes; some [[No-SQL]] or even [[in-memory]] options may be a good choice.

Historically, by far the most important consideration in database performance has been minimizing disk access, since database seek times may be hundreds of thousands of times slower than memory access.  

C.f:https://en.wikipedia.org/wiki/Column-oriented_DBMS
[[online analytical processing (OLAP)]]
[[online transaction processing (OLTP)]]
[[columnar database]]
[[row-oriented database]]