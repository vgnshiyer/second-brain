## Metadata
- Author: Kleppmann, Martin
- [Apple Books Link](ibooks://assetid/28AEDF62F12B289C88BD6659BD6E50CC)

## Highlights
If the database itself does not support joins, you have to emulate a join in application code by
making multiple queries to the database

---
When the underlying data changes, a materialized view needs to be updated, because it is a
denormalized copy of the data. The database can do that automatically, but such updates make writes
more expensive, which is why materialized views are not often used in OLTP databases. In read-heavy
data warehouses they can make more sense

---
RPC and REST APIs, where the client encodes a request, the server decodes the request and encodes
a response, and the client finally decodes the response

---
data is organized into relations (called tables in SQL), where each relation is an unordered collection
of tuples (rows in SQL).

---
SOAP is an XML-based protocol for making network API
requests

---
Another option is to simply force all atomic operations to be executed on a single thread.

---
Usually it is better to use percentiles. If you take your list of response times and sort it from
fastest to slowest, then the median is the halfway point

---
users of SOAP rely heavily on tool support, code generation, and IDEs


---
In 2PL, writers don’t just block other writers; they also block readers and vice
versa

---
transaction isolation is
primarily about avoiding race conditions due to concurrently executing transactions, whereas
distributed consistency is mostly about coordinating the state of replicas in the face of delays and
faults.

---
Operability

---
A network
request is much slower than a function call

---
The situation is more complicated if the new value is larger, as it probably needs to be moved to a
new location in the heap where there is enough space. In that case, either all indexes need to be
updated to point at the new heap location of the record, or a forwarding pointer is left behind in
the old heap location

---
This approach is called materializing conflicts, because it takes a phantom and turns it into a
lock conflict on a concrete set of rows that exist in the database

---
The blocking of readers and writers is implemented by a having a lock on each object in the
database. The lock can either be in shared mode or in exclusive mode. The lock is used as
follows:

---
When two processes are communicating over a bidirectional network connection, they can negotiate
the schema version on connection setup and then use that schema for the lifetime of the
connection

---
Each secondary
index is a separate data structure from the primary data—thus, if you modify some data, the
corresponding change needs to also be made in the secondary index. Atomicity ensures that the
secondary index stays consistent with the primary data

---
but each query is typically very demanding, requiring many millions of records to be
scanned in a short time

---
If your application requires linearizability, and some replicas are disconnected from the other
replicas due to a network problem, then some replicas cannot process requests while they are
disconnected: they must either wait until the network problem is fixed, or return an error (either
way, they become unavailable).


If your application does not require linearizability, then it can be written in a way that each
replica can process requests independently, even if it is disconnected from other replicas (e.g.,
multi-leader). In this case, the application can remain available in the face of a network
problem, but its behavior is not linearizable.

---
purely a collection of locks which is used
to prevent bookings on the same room and time range from being modified concurrently

---
but they
don’t support binary strings (sequences of bytes without a character encoding). Binary strings are a
useful feature, so people get around this limitation by encoding the binary data as text using
Base64

---
it protects against all the race conditions discussed earlier, including lost updates and write skew.

---
If you want synchronous conflict detection, you might as well just use
single-leader replication.

---
there is an implicit schema, but it is not
enforced by the database

---
background process that constantly looks for differences in
the data between replicas and copies any missing data from one replica to another

---
linearizability essentially means “behave as though there is only a single copy of the data,
and all operations on it are atomic

---
For workloads that consist of mostly reads and only a small percentage of writes
(a common pattern on the web), there is an attractive option: create many followers, and distribute
the read requests across those followers

---
A common special case of a materialized view is known as a data cube or OLAP cube

---
In general, atomic refers to something that cannot be broken down into smaller parts

---
For example, in Figure 7-2, the
user sees the new unread email but not the updated counter. This is a dirty read of the email.
Seeing the database in a partially updated state is confusing to users and may cause other
transactions to take incorrect decisions.

---
It logically decouples the sender from the recipient 

---
Preventing this kind of anomaly requires another type of guarantee: consistent prefix reads
[23]. This guarantee says that if a sequence of
writes happens in a certain order, then anyone reading those writes will see them appear in the same
order

---
Snapshot isolation has the mantra readers never block writers, and writers never block
readers

---
This is a particular problem in partitioned (sharded) databases

---
Each follower takes the log from the leader and updates its local copy of the
database accordingly,

---
SSI adds an algorithm for detecting serialization conflicts among writes and
determining which transactions to abort

---
network request is unpredictable: the request or response may be
lost due to a network problem, or the remote machine may be slow or unavailable, and such problems
are entirely outside of your control

---
By subtracting a follower’s current position from the leader’s
current position, you can measure the amount of replication lag.

---
A data warehouse, by contrast, is a separate database that analysts can query to their hearts’
content, without affecting OLTP operations
[48].
The data warehouse contains a read-only copy of the data in all the various OLTP systems in the
company. Data is extracted from OLTP databases (using either a periodic data dump or a continuous
stream of updates), transformed into an analysis-friendly schema, cleaned up, and then loaded into
the data warehouse. This process of getting data into the warehouse is known as
Extract–Transform–Load (ETL

---
Snapshot isolation is a boon for long-running, read-only queries such as backups and analytics. It
is very hard to reason about the meaning of a query if the data on which it operates is changing at
the same time as the query is executing. When a transaction can see a consistent snapshot of the
database, frozen at a particular point in time, it is much easier to understand.

---
An advantage of this approach is that databases can perform this check efficiently in conjunction
with snapshot isolation

---
ACID atomicity describes what happens if a client wants to make several writes, but a fault
occurs after some of the writes have been processed

---
Evolvability

---
The main arguments in favor of the document data model are schema flexibility, better performance
due to locality, and that for some applications it is closer to the data structures used by the
application

---
However, they have the
downside that data needs to be decoded before it is human-readable.

---
It turns out
that the indexing algorithms discussed in the first half of this chapter work well for OLTP, but are
not very good at answering analytic queries

---
Consequently, Avro doesn’t have optional and required markers

---
phantoms—that is, one transaction
changing the results of another transaction’s search query

---
When reading from the database, you will only see data that has been committed (no dirty
reads).

---
The map and reduce functions are somewhat restricted in what they are allowed to do. They must be
pure functions, which means they only use the data that is passed to them as input, they cannot
perform additional database queries

---
Isolation in the sense of ACID means that concurrently executing transactions are isolated from
each other: they cannot step on each other’s toes. The classic database textbooks formalize
isolation as serializability, which means that each transaction can pretend that it is the only
transaction running on the entire database.

---
you might find this query to be too slow if there are many emails, and decide to store the
number of unread messages in a separate field (a kind of denormalization

---
that is, any period of network
interruption lasts only for a finite duration and is then repaired

---
In this case, consensus is important to avoid a bad failover, resulting in a
split brain situation

---
if any other
transaction tries to concurrently read the same object, it is forced to wait until the first
read-modify-write cycle has completed.

---
the database must resolve the conflict in a convergent way, which means that all
replicas must arrive at the same final value when all changes have been replicated.

---
UDP is a good choice in situations where delayed data is worthless

---
This makes the median a good metric if you want to know how long users typically have to wait: half
of user requests are served in less than the median response time, and the other half take longer
than the median

---
This nondeterminism and possibility of partial failures is what makes distributed systems hard to
work with

---
Programming language–specific encodings are restricted to a single programming language and often
fail to provide forward and backward compatibility.

---
Splitting a big database into smaller subsets called partitions so that different
    partitions can be assigned to different nodes (also known as sharding).

---
2PC provides atomic commit in a distributed database, whereas 2PL provides
serializable isolation

---
This is because the customers with the slowest requests are often those who have
the most data on their accounts because they have made many purchases—that is, they’re the most
valuable customers
[19].
It’s important to keep those customers happy by ensuring the website is fast for them:

---
Because of this risk of skew and hot spots, many distributed datastores use a hash function to
determine the partition for a given key.

---
If the database
keeps track of each transaction’s activity in great detail, it can be precise about which
transactions need to abort, but the bookkeeping overhead can become significant. Less detailed
tracking is faster, but may lead to more transactions being aborted than strictly necessary.

---
On the other hand, in a leaderless configuration, failover does not exist

---
In a multi-leader configuration, there is no defined ordering of writes, so it’s not clear what the
final value should be

---
A multi-leader configuration with asynchronous replication can
usually tolerate network problems better: a temporary network interruption does not prevent writes
being processed

---
An alternative is to use different log formats for replication and for the storage engine, which
allows the replication log to be decoupled from the storage engine internals. This kind of
replication log is called a logical log

---
Some data storage systems take a different approach, abandoning the concept of a leader and
allowing any replica to directly accept writes from clients

---
By contrast, serializable snapshot isolation is an optimistic concurrency control technique.
Optimistic in this context means that instead of blocking if something potentially dangerous
happens, transactions continue anyway, in the hope that everything will turn out all right

---
WSDL enables code generation so that a client can access a remote
service using local classes and method calls

---
One way of electing a leader is to use a lock: every node that starts up
tries to acquire the lock, and the one that succeeds becomes the leader
[14]. No matter how this
lock is implemented, it must be linearizable: all nodes must agree which node owns the lock;
otherwise it is useless.

---
And once a transaction has been committed on one
node, it cannot be retracted again if it later turns out that it was aborted on another node

---
A
transaction is a way for an application to group several reads and writes together into a logical
unit. Conceptually, all the reads and writes in a transaction are executed as one operation: either
the entire transaction succeeds (commit) or it fails (abort, rollback). If it fails, the
application can safely retry

---
The application requests records using some kind of key, and the storage engine uses an
index to find the data for the requested key. Disk seek time is often the bottleneck here.

---
Table 3-1. Comparing characteristics of transaction processing versus analytic systems

---
Imagine a transaction has written some data to the database, but the transaction has not yet committed or aborted.
Can another transaction see that uncommitted data? If yes, that is called a
dirty read

---
However, the approach of requiring read locks does not work well in practice, because one
long-running write transaction can force many read-only transactions to wait until the long-running
transaction has completed

---
but the bigger the database gets, the more disk
bandwidth is required for compaction.

---
eventual consistency is a
liveness property

---
Real-time collaborative editing applications allow several people to edit a document
simultaneously

---
read-only queries can run on a consistent
snapshot without requiring any locks, which is very appealing for read-heavy workloads.

---
In practice, if you enable synchronous replication on a
database, it usually means that one of the followers is synchronous, and the others are
asynchronous. If the synchronous follower becomes unavailable or slow, one of the asynchronous
followers is made synchronous. This guarantees that you have an up-to-date copy of the data on at
least two nodes: the leader and one synchronous follower. This configuration is sometimes also
called semi-synchronous [7].

---
The idea behind column-oriented storage is simple: don’t store all the values from one row
together, but store all the values from each column together instead. 

---
When a
transaction wants to commit, the database checks whether anything bad happened (i.e., whether
isolation was violated); if so, the transaction is aborted and has to be retried. Only transactions
that executed serializably are allowed to commit.

---
When generating load artificially in order to test the scalability of a system, the load-generating
client needs to keep sending requests independently of the response time. If the client waits for
the previous request to complete before sending the next one, that behavior has the effect of
artificially keeping the queues shorter in the test than they would be in reality, which skews the
measurements

---
they often neglect the inconvenient problems of forward and backward
compatibility.

---
If one operation happened before another, the later
operation should overwrite the earlier operation, but if the operations are concurrent, we have a
conflict that needs to be resolved

---
map (also known as collect) and reduce (also
known as fold or inject

---
OLTP systems are typically user-facing, which means that they may see a huge volume of requests

---
It is impossible to reduce the probability of a fault to zero;
therefore it is usually best to design fault-tolerance mechanisms that prevent faults from causing
failures

---
Imperative code is very hard to parallelize across multiple cores and multiple machines, because it
specifies instructions that must be performed in a particular order. Declarative languages have a
better chance of getting faster in parallel execution because they specify only the pattern of the
results, not the algorithm that is used to determine the results. The database is free to use a
parallel implementation of the query language, if appropriate

---
Many programming languages come with built-in support for encoding in-memory objects into byte
sequences. For example, Java has java.io.Serializable
[1], Ruby has Marshal
[2], Python has pickle
[3],
and so on

---
Another approach is the shared-disk architecture, which uses several machines with
independent CPUs and RAM, but stores data on an array of disks that is shared between the machines,
which are connected via a fast network.ii This architecture is used
for some data warehousing workloads, but contention and the overhead of locking limit the
scalability of the shared-disk approach

---
Transactions running at the read
committed isolation level must prevent dirty writes, usually by delaying the second write until the
first write’s transaction has committed or aborted.



---
If the network between datacenters is interrupted in a single-leader setup, clients connected to
follower datacenters cannot contact the leader, so they cannot make any writes to the database, nor
any linearizable reads. They can still make reads from the follower, but they might be stale
(nonlinearizable)

---
The column-oriented storage layout relies on each column file containing the rows in the same order.
Thus, if you need to reassemble an entire row, you can take the 23rd entry from each of the
individual column files and put them together to form the 23rd row of the table.

---
B-tree implementations to
include an additional data structure on disk: a write-ahead log (WAL, also known as a redo log).
This is an append-only file to which every B-tree modification must be written before it can be
applied to the pages of the tree itself

---
storage become permanently inconsistent

---
There is a lot of ambiguity around the encoding of numbers

---
to
execute only one transaction at a time, in serial order, on a single thread. By doing so, we completely
sidestep the problem of detecting and preventing conflicts between transactions: the resulting
isolation is by definition serializable.

---
A B-tree index must write every piece of data at least twice: once to the write-ahead log, and once
to the tree page itself

---
Rather than each partition having its own secondary index (a local index), we can construct a
global index that covers data in all partitions.

---
When one part of the network is cut off from the rest due to a network fault, that is sometimes
called a network partition or netsplit

---
you
also need some way of keeping track of which keys are being split.

---
Rather than blindly relying on tools, we need to develop a good understanding of the kinds of
concurrency problems that exist, and how to prevent them. Then we can build applications that are
reliable and correct, using the tools at our disposal.

---
The API of a SOAP web service is described using an XML-based language called the Web Services
Description Language, or WSDL

---
if you decode a database value into model objects in the application

---
This is easy, using CSS

---
A secondary index usually doesn’t identify a record uniquely but
rather is a way of searching for occurrences of a particular value

---
Partitioning is usually combined with replication so that copies of each partition are stored on
multiple nodes. This means that, even though each record belongs to exactly one partition, it may
still be stored on several different nodes for fault tolerance

---
Our goal with partitioning is to spread the data and the query load evenly across nodes.

---
Monotonic Reads

---
Scalability is the term we use to describe a system’s ability to cope with increased load

---
Replication Lag

---
For example, in an application where a user can edit their own data, you can ensure that requests
from a particular user are always routed to the same datacenter and use the leader in that
datacenter for reading and writing

---
MapReduce is a programming model for processing large amounts of data in bulk across many
machines

---
It allows one message to be sent to several recipients.

---
moving backward in time.

---
A new HTTP request starts a new transaction.

---
Joins can be emulated in
application code by making multiple requests to the database, but that also moves complexity into
the application and is usually slower than a join performed by specialized code inside the
database

---
A software
project mired in complexity is sometimes described as a big ball of mud
[30].

---
Serializability is an isolation property of transactions, where every transaction may read and
write multiple objects (rows, documents, records)—see “Single-Object and Multi-Object Operations”. It
guarantees that transactions behave the same as if they had executed in some serial order (each
transaction running to completion before the next transaction starts)

---
It
may take just one slow transaction, or one transaction that accesses a lot of data and acquires many
locks, to cause the rest of the system to grind to a halt. This instability is problematic when
robust operation is required

---
Both Thrift and Protocol Buffers require a schema for any data that is encoded

---
Conceptually, the process looks like this:

---
The purpose of a database system is to provide a safe place where data can be stored without fear of
losing it. Durability is the promise that once a transaction has committed successfully, any data it
has written will not be forgotten, even if there is a hardware fault or the database crashes.



---
B-trees, partly because they
sometimes have lower write amplification

---
Moreover, LSM-trees are typically able to sustain higher write throughput than

---
and later reencode
those model objects, the unknown field might be lost in that translation process. Solving this is
not a hard problem; you just need to be aware of it.




---
We call this kind of index term-partitioned, because the term we’re looking for determines the partition
of the index

---
In Dynamo-style databases, the parameters n, w, and r are typically configurable. A common
choice is to make n an odd number (typically 3 or 5) and to set w = r =
(n + 1) / 2 (rounded up

---
if anything might possibly go wrong (as indicated by a lock held by another
transaction), it’s better to wait until the situation is safe again before doing anything. It is
like mutual exclusion, which is used to protect data structures in multi-threaded programming

---
Even though crashes, race conditions, and disk failures do occur, the transaction abstraction hides
those problems so that the application doesn’t need to worry about them.

---
Cassandra achieves a compromise between the two partitioning strategies
[11,
12,
13].
A table in Cassandra can be declared with a compound primary key consisting of several columns.
Only the first part of that key is hashed to determine the partition, but the other columns are used
as a concatenated index for sorting the data in Cassandra’s SSTables. A query therefore cannot
search for a range of values within the first column of a compound key, but if it specifies a fixed
value for the first column, it can perform an efficient range scan over the other columns of the
key.


The concatenated index approach enables an elegant data model for one-to-many relationships. For
example, on a social media site, one user may post many updates. If the primary key for updates is
chosen to be (user_id, update_timestamp), then you can efficiently retrieve all updates made by a
particular user within some time interval, sorted by timestamp. Different users may be stored on
different partitions, but within each user, the updates are stored ordered by timestamp on a single
partition.

---
raison d’être

---
In the case of a B-tree (see “B-Trees”), which overwrites individual disk blocks,
every modification is first written to a write-ahead log so that the index can be restored
to a consistent state after a crash.

---
Shared-nothing is not the only way of building systems, but it has become the dominant approach for
building internet services, for several reasons: it’s comparatively cheap because it
requires no special hardware, it can make use of commoditized cloud computing services, and it can
achieve high reliability through redundancy across multiple geographically distributed datacenters

---
In this setup, each leader simultaneously acts as a
follower to the other leaders.

---
by allowing an update to happen only if the value has not changed since you last
read it

---
This is where the name “two-phase” comes from: the first phase
(while the transaction is executing) is when the locks are acquired, and the second phase (at the
end of the transaction) is when all the locks are released.

---
but it unfortunately requires that the
clients do some extra work: if several operations happen concurrently, clients have to clean up
afterward by merging the concurrently written values

---
Several transactions
are allowed to concurrently read the same object as long as nobody is writing to it. But as soon as
anyone wants to write (modify or delete) an object, exclusive access is required:

---
the basic idea is to make a system appear as if there were only one copy of the data,
and all operations on it are atomic

---
The only safe way of using a database with LWW is to ensure that a key is only written once and
thereafter treated as immutable, thus avoiding any concurrent updates to the same key. For example,
a recommended way of using Cassandra is to use a UUID as the key, thus giving each write operation a
unique key

---
The fault handling must be part of the software design, and
you (as operator of the software) need to know what behavior to expect from the software in the case
of a fault.

---
the sender doesn’t wait for the message to be delivered, but simply sends it and
then forgets about it

---
On its local disk, each follower keeps a log of the data changes it has received from the leader. 

---
serializable isolation means that the database
guarantees that transactions have the same effect as if they ran serially (i.e., one at a time,
without any concurrency).

---
Write skew can occur if two
transactions read the same objects, and then update some of those objects

---
If the code
reading the data encounters a field that appears in the writer’s schema but not in the reader’s
schema, it is ignored. If the code reading the data expects some field, but the writer’s schema does
not contain a field of that name, it is filled in with a default value declared in the reader’s
schema

---
The client can remember the timestamp of its most recent write—then the system can ensure that the
replica serving any reads for that user reflects updates at least until that timestamp

---
Even in “noncritical” applications we have a responsibility to our users

---
Any kind of index usually slows down writes, because the index also needs
to be updated every time data is written.

---
instead, the
system must leave a marker with an appropriate version number to indicate that the item has been
removed when merging siblings.  Such a deletion marker is known as a tombstone

---
there is no
such thing as perfect reliability

---
One of the best tools we have for removing accidental complexity is abstraction. A good
abstraction can hide a great deal of implementation detail behind a clean, simple-to-understand
façade

---
Any statement that calls a nondeterministic function, such as NOW() to get the current date
and time or RAND() to get a random number, is likely to generate a different value on each
replica.

---
A system is Byzantine fault-tolerant if it continues to operate correctly even if some of the
nodes are malfunctioning and not obeying the protocol, or if malicious attackers are interfering
with the network

---
Asynchronous message passing (using message brokers or actors), where nodes communicate by sending
each other messages that are encoded by the sender and decoded by the recipient

---
they must be executed in exactly the same
order on each replica

---
Unicode character strings (i.e., human-readable text

---
There are many different types of objects, and it is not practical to put each type of object in
its own table.


The structure of the data is determined by external systems over which you have no control and
which may change at any time.

---
A key design goal of a service-oriented/microservices architecture is to make the application easier
to change and maintain by making services independently deployable and evolvable

---
But in cases where all records are expected to have the same
structure, schemas are a useful mechanism for documenting and enforcing that structure

---
Even if the input strings are very similar, their
hashes are evenly distributed across that range of numbers.

---
The biggest problem with multi-leader replication is that write conflicts can occur, which means
that conflict resolution is required

---
it is not important whether they literally overlap in time. Because of problems with clocks
in distributed systems, it is actually quite difficult to tell whether two things happened
at exactly the same time

---
Making a system simpler does not necessarily mean reducing its functionality; it can also mean
removing accidental complexity. Moseley and Marks
[32] define complexity as accidental if
it is not inherent in the problem that the software solves (as seen by the users) but arises only
from the implementation

---
While distributing stateless services across multiple machines is fairly straightforward, taking
stateful data systems from a single node to a distributed setup can introduce a lot of additional
complexity. For this reason, common wisdom until recently was to keep your database on a single
node (scale up) until scaling cost or high-availability requirements forced you to make it
distributed

---
The best candidate for leadership is usually the replica with the most
up-to-date data changes from the old leader

---
Dirty reads

One client reads another client’s writes before they have been committed. The read committed
isolation level and stronger levels prevent dirty reads.

Dirty writes

One client overwrites data that another client has written, but not yet committed. Almost all
transaction implementations prevent dirty writes.

Read skew (nonrepeatable reads)




A client sees different parts of the database at different points in time. This issue is most
commonly prevented with snapshot isolation, which allows a transaction to read from a consistent
snapshot at one point in time. It is usually implemented with multi-version concurrency control
(MVCC).

Lost updates

Two clients concurrently perform a read-modify-write cycle. One overwrites the other’s write
without incorporating its changes, so data is lost. Some implementations of snapshot isolation
prevent this anomaly automatically, while others require a manual lock (SELECT FOR UPDATE).

Write skew

A transaction reads something, makes a decision based on the value it saw, and writes the decision
to the database. However, by the time the write is made, the premise of the decision is no longer
true. Only serializable isolation prevents this anomaly.

Phantom reads

A transaction reads objects that match some search condition. Another client makes a write that
affects the results of that search. Snapshot isolation prevents straightforward phantom reads, but
phantoms in the context of write skew require special treatment, such as index-range locks.



Weak isolation levels protect against some of those anomalies but leave you, the application
developer, to handle others manually (e.g., using explicit locking). Only serializable isolation
protects against all of these issues. We discussed three different approaches to implementing
serializable transactions:

Literally executing transactions in a serial order

If you can make each transaction very fast to execute, and the transaction throughput is low
enough to process on a single CPU core, this is a simple and effective option.

Two-phase locking

For decades this has been the standard way of implementing serializability, but many applications
avoid using it because of its performance characteristics.

Serializable snapshot isolation (SSI)

A fairly new algorithm that avoids most of the downsides of the previous approaches. It uses an
optimistic approach, allowing transactions to proceed without blocking. When a transaction wants
to commit, it is checked, and it is aborted if the execution was not serializable.

---
It can act as a buffer if the recipient is unavailable or overloaded

---
It is
possible (though computationally expensive) to test whether a system’s behavior is linearizable by
recording the timings of all requests and responses, and checking whether they can be arranged into
a valid sequential order [11].

---
They are similar to RPC in that a client’s request (usually
called a message) is delivered to another process with low latency. They are similar to databases
in that the message is not sent via a direct network connection, but goes via an intermediary called
a message broker

---
This is why the
coordinator must write its commit or abort decision to a transaction log on disk before sending
commit or abort requests to participants: when the coordinator recovers, it determines the status of
all in-doubt transactions by reading its transaction log

---
One common reason for degradation is increased load

---
so most systems simply use a timeout: nodes frequently bounce messages back and
forth between each other, and if a node doesn’t respond for some period of time—say, 30
seconds—it is assumed to be dead

---
you can create several
secondary indexes on the same table using the CREATE INDEX command, and they are often crucial
for performing joins efficiently.

---
At times when the network is working correctly, a system can provide both consistency
(linearizability) and total availability. When a network fault occurs, you have to choose between
either linearizability or total availability

---
By avoiding unnecessary aborts, SSI preserves snapshot
isolation’s support for long-running reads from a consistent snapshot.

---
Since so many locks are in use, it can happen quite easily that transaction A is stuck waiting for
transaction B to release its lock, and vice versa. This situation is called deadlock. The database
automatically detects deadlocks between transactions and aborts one of them so that the others can
make progress. The aborted transaction needs to be retried by the application.

---
Simplicity

---
The usual way of handling this issue is a timeout: after some time you give up waiting and assume that
the response is not going to arrive

---
When reading something that the user may have modified, read it from the leader; otherwise, read it
from a follower

---
The safety guarantees provided by transactions are often described by the well-known acronym ACID,
which stands for Atomicity, Consistency, Isolation, and Durability

---
If your application has mostly one-to-many relationships (tree-structured
data) or no relationships between records, the document model is appropriate.

---
A compromise between a clustered index (storing all row data within the index) and a nonclustered
index (storing only references to the data within the index

---
If an error occurs halfway through a sequence of writes, the transaction should be aborted, and
the writes made up to that point should be discarded

---
Custom RPC protocols with a binary encoding format can achieve better performance than something
generic like JSON over REST

---
Although this approach
is popular, it is dangerously prone to data loss
[35].

---
This is an important trade-off in storage systems: well-chosen indexes speed up read queries, but
every index slows down writes. For this reason, databases don’t usually index everything by default,
but require you—the application developer or database administrator—to choose indexes
manually, using your knowledge of the application’s typical query patterns

---
The parameters w and r allow you to adjust the probability of stale values
being read, but it’s wise to not take them as absolute guarantees.

---
If the data in your application has a document-like structure (i.e., a tree of one-to-many
relationships, where typically the entire tree is loaded at once), then it’s probably a good idea to
use a document model

---
Often, leader-based replication is configured to be completely asynchronous. In this case, if the
leader fails and is not recoverable, any writes that have not yet been replicated to followers are
lost. This means that a write is not guaranteed to be durable, even if it has been confirmed to the
client. However, a fully asynchronous configuration has the advantage that the leader can continue
processing writes, even if all of its followers have fallen behind.

---
In the example of Figure 5-2, the replication to follower 1 is
synchronous: the leader waits until follower 1 has confirmed that it received the write before
reporting success to the user, and before making the write visible to other clients. The replication
to follower 2 is asynchronous:

---
The main focus of RPC
frameworks is on requests between services owned by the same organization, typically within the same
datacenter.

---
JSON distinguishes strings and numbers, but it doesn’t distinguish integers and
floating-point numbers

---
but from any one user’s point of view the
configuration is essentially single-leader.

---
The key idea with Avro is that the writer’s schema and the reader’s schema don’t have to be the
same—they only need to be compatible. When data is decoded (read), the Avro library resolves the
differences by looking at the writer’s schema and the reader’s schema side by side and translating
the data from the writer’s schema into the reader’s schema

---
The simplest
solution is to include a version number at the beginning of every encoded record, and to keep a
list of schema versions in your database

---
Document databases reverted back to the hierarchical model in one aspect: storing nested records

---
The process of
moving load from one node in the cluster to another is called rebalancing

---
it also sends the
data change to all of its followers as part of a  replication log or
change stream

---
If a node is removed from the cluster, the same happens in
reverse.

Only entire partitions are moved between nodes. The number of partitions does not change, nor does
the assignment of keys to partitions

---
If a participant has crashed in the meantime, the
transaction will be committed when it recovers—since the participant voted “yes,” it cannot
refuse to commit when it recovers

---
LSM-trees are typically faster for writes, whereas B-trees are thought to be faster for reads


---
Safety is often informally defined as nothing bad happens, and liveness as something good
eventually happens

---
We need an approach that doesn’t move data around more than necessary

---
if the application can ensure
that all writes for a particular record go through the same leader, then conflicts cannot occur.

---
 On the one hand, we
have implementations of serializability that don’t perform well (two-phase locking) or don’t scale
well (serial execution). On the other hand, we have weak isolation levels that have good
performance, but are prone to various race conditions (lost updates, write skew, phantoms, etc.

---
monotonic reads
only means that if one user makes several reads in sequence, they will not see time go
backward—i.e., they will not read older data after having previously read newer data.

One way of achieving monotonic reads is to make sure that each user always makes their reads from
the same replica (different users can read from different replicas). For example, the replica can be
chosen based on a hash of the user ID

---
The lost update problem can occur if an application reads some value from the database, modifies it,
and writes back the modified value (a read-modify-write cycle). If two transactions do this
concurrently, one of the modifications can be lost, because the second write does not include the
first modification

---
With the example of a shopping cart, a reasonable approach to merging siblings is to just take the
union

---
The requirement of linearizability is that the lines joining up the operation markers always move
forward in time (from left to right), never backward

---
First of all, notice that there are no tag numbers in the schema. If we encode our example record
(Example 4-1) using this schema, the Avro binary encoding is just 32 bytes long—the
most compact of all the encodings we have seen

---
one key for every few kilobytes of segment file is sufficient

---
if you run the same query on the leader and a follower at the same time, you may get
different results, because not all writes have been reflected in the follower

---
In a database with single-leader replication, all nodes need to agree on which node is the leader

---
However, they have the downside of making writes more difficult.

An update-in-place approach, like B-trees use, is not possible with compressed columns. If you
wanted to insert a row in the middle of a sorted table, you would most likely have to rewrite all
the column files. As rows are identified by their position within a column, the insertion has to
update all columns consistently.

---
Synchronous Versus Asynchronous Replication

---
The client sees that replica 3 has a stale
value and writes the newer value back to that replica. This approach works well for values that are
frequently read.

---
There is also overhead from having
to write an entire page at a time, even if only a few bytes in that page changed

---
other users’ updates may not be
visible until some later time. However, it reassures the user that their own input has been saved
correctly.

---
These constraints all require there to
be a single up-to-date value (the account balance, the stock level, the seat occupancy) that all
nodes agree on.

---
read-your-writes consistency
[24].
This is a guarantee that if the user reloads the page, they will always see any updates they
submitted themselves.

---
the database prevents all possible race conditions.

---
In dynamically typed programming languages such as JavaScript, Ruby, or Python, there is not much
point in generating code, since there is no compile-time type checker to satisfy. Code generation is
often frowned upon in these languages, since they otherwise avoid an explicit compilation step

---
all-or-nothing guarantee.

---
However, for faster collaboration, you may want to make the unit of change very small (e.g., a single
keystroke) and avoid locking. This approach allows multiple users to edit simultaneously, but it also brings
all the challenges of multi-leader replication, including requiring conflict resolution

---
Thus, applications that don’t require linearizability can be more tolerant of network problems

---
Analyzing whether people are more inclined to buy fresh fruit or candy, depending on the day of the week

---
For that reason, it is impractical for all followers to be synchronous: any one node outage would
cause the whole system to grind to a halt

---
To implement snapshot isolation, databases use a generalization of the mechanism we saw for
preventing dirty reads

---
Most database vendors recommend that you structure
your partitioning scheme so that secondary index queries can be served from a single partition

---
Similarly to what db_set does, many databases
internally use a log, which is an append-only data file

---
The data model of a data warehouse is most commonly relational, because SQL is generally a good fit
for analytic queries

---
When you want to write data to a file or send it over the network, you have to encode it as some
kind of self-contained sequence of bytes

---
The encoding is often tied to a particular programming language

---
This is a realistic model of many
systems: most of the time, networks and processes are quite well behaved—otherwise we would never
be able to get anything done—but we have to reckon with the fact that any timing assumptions
may be shattered occasionally

---
most databases with 2PL
actually implement index-range locking (also known as next-key locking), which is a simplified
approximation of predicate locking

---
it’s ugly to let a concurrency control
mechanism leak into the application data model. For those reasons, materializing conflicts should be
considered a last resort if no alternative is possible

---
In this situation, it’s likely that fewer than w or r
reachable nodes remain, so the client can no longer reach a quorum.

---
One thing that document and graph databases have in common is that they typically don’t enforce a
schema for the data they store, which can make it easier to adapt applications to changing
requirements

---
In order to figure out how bad your outliers are, you can look at higher percentiles: the 95th,
99th, and 99.9th percentiles are common (abbreviated p95, p99, and p999). They are the
response time thresholds at which 95%, 99%, or 99.9% of requests are faster than that particular
threshold. For example, if the 95th percentile response time is 1.5 seconds, that means 95 out of
100 requests take less than 1.5 seconds, and 5 out of 100 requests take 1.5 seconds or more. This is
illustrated in Figure 1-4.





---
As multi-leader replication is a somewhat retrofitted feature in many databases, there are often
subtle configuration pitfalls and surprising interactions with other database features. For example,
autoincrementing keys, triggers, and integrity constraints can be problematic. For this reason,
multi-leader replication is often considered dangerous territory that should be avoided if possible

---
You could also monitor the replication lag on followers and
prevent queries on any follower that is more than one minute behind the leader.

---
The things that can go wrong are called faults, and systems that anticipate faults and can cope
with them are called fault-tolerant or resilient

---
When a participant receives the prepare request, it makes sure that it can definitely commit
the transaction under all circumstances

---
a common approach in such replicated
databases is to allow concurrent writes to create several conflicting versions of a value (also
known as siblings), and to use application code or special data structures to resolve and merge
these versions after the fact.

---
Consistent Prefix Reads

---
epoch: midnight UTC on January 1, 1970

---
Some in-memory key-value stores, such as Memcached, are intended for caching use only, where it’s
acceptable for data to be lost if a machine is restarted

---
Normally, partitions are defined in such a way that each piece of data (each record, row, or
document) belongs to exactly one partition

---
One of the replicas is designated the leader (also known as master or primary). When
clients want to write to the database, they must send their requests to the leader, which first
writes the new data to its local storage.









The other replicas are known as followers

---
RESTful APIs tend to favor simpler approaches, typically involving less code generation and
automated tooling

---
Thus, the inter-datacenter network delay is hidden from
users, which means the perceived performance may be better

---
Thus, if you want to search for red cars, you need to
send the query to all partitions, and combine all the results you get back

---
Systems that do not meet the ACID criteria are sometimes called BASE, which stands for
Basically Available, Soft state, and Eventual consistency
[9].
This is even more vague than the definition of ACID. It seems that the only sensible definition of
BASE is “not ACID”; i.e., it can mean almost anything you want.

---
We also say that B is causally dependent on A.

---
The main reason for wanting to partition data is scalability. Different partitions can be placed
on different nodes in a shared-nothing cluster

---
But what if many-to-many relationships are very common in your data? The relational model can handle
simple cases of many-to-many relationships, but as the connections within your data become more
complex, it becomes more natural to start modeling your data as a graph.

---
It avoids the sender needing to know the IP address and port number of the recipient

---
It can automatically redeliver messages to a process that has crashed, and thus prevent messages from
being lost.

---
transaction throughput and response times of queries are significantly worse
under two-phase locking than under weak isolation.

---
the decoding process needs to be able to
instantiate arbitrary classes

---
efficient
encoding with clearly defined forward and backward compatibility semantics

---
A network request has another possible
outcome: it may return without a result, due to a timeout

---
The final twist of the Twitter anecdote: now that approach 2 is robustly implemented, Twitter is
moving to a hybrid of both approaches. Most users’ tweets continue to be fanned out to home
timelines at the time when they are posted, but a small number of users with a very large number of
followers (i.e., celebrities) are excepted from this fan-out

---
each index just references a location
in the heap file, and the actual data is kept in one place.

---
The simplest
way of handling such faults is to simply let the entire service fail, and show the user an error
message

---
However, with liveness properties we are allowed to make caveats: for example, we could say that a
request needs to receive a response only if a majority of nodes have not crashed, and only if the
network eventually recovers from an outage

---
it is
unwise for a service to assume that its clients will always be well behaved, because the clients are
often run by people whose priorities are very different from the priorities of the people running
the service

---
However, if you want to allow people to also remove things from their carts, and not just add
things, then taking the union of siblings may not yield the right result: if you merge two sibling
carts and an item has been removed in only one of them, then the removed item will reappear in the
union of the siblings

---
you cannot refer directly to a nested item

---
A logical log format is also easier for external applications to parse. This aspect is useful if you want
to send the contents of a database to an external system

---
The advantage of a global (term-partitioned) index over a document-partitioned index is that it can
make reads more efficient: rather than doing scatter/gather over all partitions, a client only needs
to make a request to the partition containing the term that it wants. However, the downside of a
global index is that writes are slower and more complicated, because a write to a single
document may now affect multiple partitions of the index

---
LSM-trees. All writes
first go to an in-memory store, where they are added to a sorted structure and prepared for writing
to disk. It doesn’t matter whether the in-memory store is row-oriented or column-oriented. When
enough writes have accumulated, they are merged with the column files on disk and written to new
files in bulk

---
If any of the participants replies “no,” the coordinator sends an abort request to all nodes in
phase 2

---
REST is not a protocol, but rather a design philosophy that builds upon the principles of HTTP


---
Concurrently running transactions shouldn’t interfere with each other.

---
If we want to maintain
transaction atomicity (in the sense of ACID; see “Atomicity”), we have to get
all nodes to agree on the outcome of the transaction: either they all abort/roll back (if anything
goes wrong) or they all commit (if nothing goes wrong)

---
Databases, where the process writing to the database encodes the data and the process reading
from the database decodes it

---
LSM-trees, which only append to files (and eventually delete obsolete files)

---
Executing all transactions serially makes concurrency control much simpler, but limits the
transaction throughput of the database to the speed of a single CPU core on a single machine.
Read-only transactions may execute elsewhere, using snapshot isolation, but for applications with
high write throughput, the single-threaded transaction processor can become a serious bottleneck

---
That is, even if all nodes crash, or
the entire network fails, the algorithm must nevertheless ensure that it does not return a wrong
result (i.e., that the safety properties remain satisfied

---
Compaction
means throwing away duplicate keys in the log, and keeping only the most recent update for each key.




---
maelstrom

---
you need linearizability.

---
This problem does not occur in a single-leader database

---
The presence of skew makes partitioning much less effective. In an extreme case, all the load
could end up on one partition, so 9 out of 10 nodes are idle and your bottleneck is the
single busy node. A partition with disproportionately high load is called a hot spot.

---
Note that the additional table
isn’t used to store information about the booking—it’s

---
The disadvantage is that if the synchronous
follower doesn’t respond (because it has crashed, or there is a network fault, or for any other
reason), the write cannot be processed. The leader must block all writes and wait until the
synchronous replica is available again.

---
The idea is that each transaction reads from a consistent snapshot of
the database—that is, the transaction sees all the data that was committed in the database at the
start of the transaction

---
read requests are also sent to several nodes in parallel.

---
This effect, where a write in one transaction changes the result of a search query in another
transaction, is called a phantom

---
When writing to the database, you will only overwrite data that has been committed (no dirty
writes).

---
Leader-based replication has one major downside: there is only one leader, and all writes must go
through it

---
Unfortunately however, by using the hash of the key for partitioning we lose a nice property of
key-range partitioning: the ability to do efficient range queries. Keys that were once adjacent are
now scattered across all the partitions, so their sort order is lost

---
By contrast, if you were using Thrift or Protocol Buffers for this purpose, the field tags would
likely have to be assigned by hand: every time the database schema changes, an administrator would
have to manually update the mapping from database column names to field tags. 

---
systems with stronger guarantees may have worse performance or be less
fault-tolerant than systems with weaker guarantees

---
An alternative is to allow them to execute in parallel and, if the
transaction manager detects a lost update, abort the transaction and force it to retry
its read-modify-write cycle.

---
greater scalability than relational databases

---
If one node
fails, a common solution is to simply stop the entire cluster workload. After the faulty node is
repaired, the computation is restarted from the last checkpoint
[7,
8].
Thus, a supercomputer is more like a single-node computer than a distributed system

---
Without hearing from the coordinator, the participant has no way of knowing whether to commit or
abort

---
In an early-stage startup or an unproven product it’s usually more important to
be able to iterate quickly on product features than it is to scale to some hypothetical future
load.

---
The RPC model tries to make a request to a remote network service look the same as calling a function or
method in your programming language, within the same process (this abstraction is called location
transparency

---
When you call a local function, you can efficiently pass it references (pointers) to objects in
local memory. When you make a network request, all those parameters need to be encoded into a
sequence of bytes that can be sent over the network

---
either Consistent or Available when Partitioned

---
In this case, when the resizer fetches the image (step 5), it might see an old version of
the image, or nothing at all

---
Range queries are not efficient

---
The
database typically needs to load the entire document, even if you access only a small portion of it,
which can be wasteful on large documents

---
hubris

---
If the current value does not match what you previously read, the update has no effect, and
the read-modify-write cycle must be retried.

---
Thrift has a dedicated list datatype, which is parameterized with the datatype of the list
elements. This does not allow the same evolution from single-valued to multi-valued as Protocol
Buffers does, but it has the advantage of supporting nested lists.

---
Each write from a client
is sent to all replicas, regardless of datacenter, but the client usually only waits for
acknowledgment from a quorum of nodes within its local datacenter so that it is unaffected by
delays and interruptions on the cross-datacenter link

---
Consistent hashing, as defined by Karger et al.
[7],
is a way of evenly distributing load across an internet-wide system of caches such as a content
delivery network (CDN). It uses randomly chosen partition boundaries to avoid the need for central
control or distributed consensus. Note that consistent here has nothing to do with replica
consistency (see Chapter 5) or ACID consistency (see Chapter 7), but rather
describes a particular approach to rebalancing.

---
one process sends a message to a named queue or topic, and the
broker ensures that the message is delivered to one or more consumers of or subscribers to that
queue or topic. There can be many producers and many consumers on the same topic.

---
for every
object that is written, the database remembers both the old committed value and the new value
set by the transaction that currently holds the write lock. While the transaction is ongoing, any
other transactions that read the object are simply given the old value.

---
Now, if a node is added to the cluster, the new node can steal a few partitions from every
existing node until partitions are fairly distributed once again

---
OLTP systems for analytics purposes, and to run the analytics on a separate
database instead. This separate database was called a data warehouse.

---
These
characteristics make databases with leaderless replication appealing for use cases that require
high availability and low latency, and that can tolerate occasional stale reads.

---
systems with single-threaded serial transaction processing don’t allow interactive
multi-statement transactions. Instead, the application must submit the entire transaction code to
the database ahead of time, as a stored procedure

---
This works better because the average
rate of published tweets is almost two orders of magnitude lower than the rate of home timeline
reads, and so in this case it’s preferable to do more work at write time and less at read time.

---
dirty writes and lost updates, two kinds of race conditions that
can occur when different transactions concurrently try to write to the same objects.

---
Serializable isolation is usually regarded as the strongest isolation level. It guarantees that even
though transactions may execute in parallel, the end result is the same as if they had executed one
at a time, serially, without any concurrency

---
The reason for this rule is that once data has been
committed, it becomes visible to other transactions, and thus other clients may start relying on
that data; this principle forms the basis of read committed isolation

---
SQL is a
declarative query language

---
The web works this way: clients (web browsers) make requests to web servers, making GET requests
to download HTML, CSS, JavaScript, images, etc., and making POST requests to submit data to the
server. The API consists of a standardized set of protocols and data formats (HTTP, URLs, SSL/TLS,
HTML, etc.). Because web browsers, web servers, and website authors mostly agree on these standards,
you can use any web browser to access any website

---
Serial execution is, in a sense, pessimistic to the extreme: it is essentially equivalent to each
transaction having an exclusive lock on the entire database (or one partition of the database) for
the duration of the transaction. We compensate for the pessimism by making each transaction very
fast to execute, so it only needs to hold the “lock” for a short time.

---
Every write to the database needs to be processed by every replica; otherwise, the replicas would no
longer contain the same data. The most common solution for this is called leader-based
replication (also known as active/passive or master–slave replication) and is illustrated

---
With Avro, forward compatibility means that you can have a new version of the schema as writer and
an old version of the schema as reader. Conversely, backward compatibility means that you can have a
new version of the schema as reader and an old version as writer.

---
when developing a prototype product for an unproven market

---
There are plenty of well-known tree data structures that you can use, such
as red-black trees or AVL trees [2]. With
these data structures, you can insert keys in any order and read them back in sorted order.

---
Concurrency bugs are hard to find by testing, because such bugs are only triggered when you get
unlucky with the timing. Such timing issues might occur very rarely, and are usually difficult to
reproduce

---
due to a network interruption or GC pause

---
downside of log-structured storage is that the compaction process can sometimes interfere with the
performance of ongoing reads and writes.

---
Just a two-digit decimal random number would split the writes to the key evenly across 100 different
keys, allowing those keys to be distributed to different partitions.

However, having split the writes across different keys, any reads now have to do additional work, as
they have to read the data from all 100 keys and combine it

---
If partitions are very large, rebalancing and recovery from
node failures become expensive. But if partitions are too small, they incur too much overhead. The
best performance is achieved when the size of partitions is “just right,” neither too big nor too
small, which can be hard to achieve if the number of partitions is fixed but the dataset size
varies.

---
Linearizability is a recency guarantee on reads and writes of a register (an individual object).
It doesn’t group operations together into transactions, so it does not prevent problems such as
write skew

---
This requirement ensures the recency guarantee we
discussed earlier: once a new value has been written or read, all subsequent reads see the value
that was written, until it is overwritten again

---
Specialized query operations that are not well supported by the relational model

---
application may
prompt the user or automatically resolve the conflict, and write the result back to the database.
CouchDB works this way, for example

---
problems in the network cannot reliably be distinguished from problems at a node.

---
Only one transaction can hold the
lock for any given object; if another transaction wants to write to the same object, it must wait
until the first transaction is committed or aborted before it can acquire the lock and continue.
This locking is done automatically by databases in read committed mode (or stronger isolation
levels).

---
For example, consider the calendar apps on your mobile phone, your laptop, and other devices. You
need to be able to see your meetings (make read requests) and enter new meetings (make write
requests) at any time, regardless of whether your device currently has an internet connection. If
you make any changes while you are offline, they need to be synced with a server and your other
devices when the device is next online.


In this case, every device has a local database that acts as a leader (it accepts write requests),
and there is an asynchronous multi-leader replication process (sync) between the replicas of your
calendar on all of your devices. The replication lag may be hours or even days, depending on when
you have internet access available.

---
If you want to enforce this constraint as the data is written

---
A global
index must also be partitioned, but it can be partitioned differently from the primary key index

---
better because it allows messages to travel
along different paths, avoiding a single point of failure.

---
there is enough spare capacity, and if contention between transactions is not too high,
optimistic concurrency control techniques tend to perform better than pessimistic ones

---
Two-phase commit is an algorithm for achieving atomic transaction commit across multiple
nodes—i.e., to ensure that either all nodes commit or all nodes abort.

---
 The retry happens at the human layer instead.
(“Could you repeat that please? The sound just cut out for a moment.”)

---
One solution is to make sure that any writes that are causally related to each other are written to
the same partition—but in some applications that cannot be done efficiently.

---
the coordinator begins phase 1: it sends a prepare request to each of the nodes,
asking them whether they are able to commit. The coordinator then tracks the responses from the
participants:

---
These formats are somewhat vague about datatypes, so you have to be careful with things
like numbers and binary strings.

---
Historically, data started out being represented as one big tree (the hierarchical model), but that
wasn’t good for representing many-to-many relationships, so the relational model was invented to
solve that problem. More recently, developers found that some applications don’t fit well in the
relational model either. New nonrelational “NoSQL” datastores have diverged in two main
directions:


Document databases target use cases where data comes in self-contained documents and
relationships between one document and another are rare.


Graph databases go in the opposite direction, targeting use cases where anything is potentially
related to everything.

---
For modeling real systems, the partially synchronous model with crash-recovery faults is generally
the most useful model

---
In a web browser, using declarative CSS styling is much better than manipulating styles imperatively in
JavaScript. Similarly, in databases, declarative query languages like SQL turned out to be much
better than imperative query APIs

---
Keeping a copy of the same data on several different nodes, potentially in different
    locations

---
profusion

---
When a client wants to read from the database, it can query either the leader or any of the
followers. However, writes are only accepted on the leader

---
is up to the database
system’s query optimizer to decide which indexes and which join methods to use, and in which order
to execute various parts of the query.

---
If a database only needed to provide read committed isolation, but not snapshot isolation, it would
be sufficient to keep two versions of an object: the committed version and the
overwritten-but-not-yet-committed version. However, storage engines that support snapshot isolation
typically use MVCC for their read committed isolation level as well. A typical approach is that read
committed uses a separate snapshot for each query, while snapshot isolation uses the same snapshot
for an entire transaction

---
the second-best option in this case is probably
to explicitly lock the rows that the transaction depends on

---
Atomic operations are usually implemented by taking an exclusive lock on the object when it is read
so that no other transaction can read it until the update has been applied

---
A long timeout means a long wait until a node is declared dead (and during this time, users may have
to wait or see error messages). A short timeout detects faults faster, but carries a higher risk of
incorrectly declaring a node dead when in fact it has only suffered a temporary slowdown

---
The problem with a shared-memory approach is that the cost grows faster than linearly

---
more dynamic and
expressive data model 

---
Now, if the database schema changes (for example, a table has one column added and one column
removed), you can just generate a new Avro schema from the updated database schema and export data in
the new Avro schema. The data export process does not need to pay any attention to the schema
change

---
The client and the service may be implemented in different programming languages, so the RPC
framework must translate datatypes from one language into another

---
does not copy writes in
any particular order

---
The difference between the two values tells you how much time
elapsed between the two checks

---
A simple
approach is to just pick one of the values based on a version number or timestamp (last write wins),
but that implies losing data

---
Thus, if one
client’s read returns the new value 1, all subsequent reads must also return the new value, even if
the write operation has not yet completed.

---
They are usually reluctant to let business analysts
run ad hoc analytic queries on an OLTP database

---
Atomicity prevents failed transactions from littering the database with half-finished results and
half-updated state

---
If you want to guarantee that there will be no editing conflicts, the application must obtain a lock
on the document before a user can edit it. If another user wants to edit the same document, they
first have to wait until the first user has committed their changes and released the lock. This
collaboration model is equivalent to single-leader replication with transactions on the leader.

---
plethora

---
The collection of version numbers from all the replicas is called a version vector

---
use a lot of space

---
If all participants reply “yes,” indicating they are ready to commit, then the coordinator sends
out a commit request in phase 2, and the commit actually takes place.

---
One way of creating such a cache is a materialized view. In a relational data model, it is often
defined like a standard (virtual) view: a table-like object whose contents are the results of some
query

---
Many data warehouses are used in a fairly formulaic
style, known as a star schema

---
That includes decisions about declaring nodes dead. If a quorum of nodes declares another node
dead, then it must be considered dead, even if that node still very much feels alive. The individual
node must abide by the quorum decision and step down

---
Why not abort transaction 43 immediately when the stale read is detected?
Well, if transaction 43 was a read-only transaction, it wouldn’t need to be aborted, because there
is no risk of write skew

---
Systems with multi-leader replication are generally not linearizable, because they concurrently
process writes on multiple nodes and asynchronously replicate them to other nodes

---
database must
discard or undo any writes it has made so far in that transaction.

---
For RESTful APIs, common approaches are to use a version
number in the URL or in the HTTP Accept header

---
To parse the binary data, you go through the fields in the order that they appear in the schema and
use the schema to tell you the datatype of each field. This means that the binary data can only be
decoded correctly if the code reading the data is using the exact same schema as the code that
wrote the data. Any mismatch in the schema between the reader and the writer would mean incorrectly
decoded data.