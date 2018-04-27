---
layout: post
title:  "Replication as an abstract problem"
date:   2018-04-27 17:33:38 +0700
categories: jekyll update
---
### Paper source

[Understanding Replication in Database and Distributed Systems [ M. Wiesmann, F. Pedone, A. Schiper & B. Kemme, G. Alonso ]](https://pdfs.semanticscholar.org/d0b5/b68e0b7c60dda9de967b3c14937693d0e680.pdf)

##### Request Phase

During the request phase, a client submits an operation to the system. This can be done in two
ways: the client can directly send the operation to all replicas or the client can send the operation to one replica which will then send the operation to all others as part of the server coordination phase.

This distinction, although apparently simple, already introduces some signiﬁcant differences between databases and distributed systems. 

In databases, clients never contact all replicas, and always send the operation to one copy. The reason is very simple: replication should be transparent to the client. Being able to send an operation to all replicas will imply the client has knowledge about the data location, schema, and distribution which is not practical
for any database of average size. This is knowledge intrinsically tied to the database nodes, thus, client must always submit the operation to one node which will then send it to all others.

In distributed systems, however, a clear distinction is made between replication techniques depending on whether the client sends the operation directly to all copies (e.g. active replication) or to one copy (e.g. passive replication).

It could be argued that in both cases, the request mechanisms can be seen as contacting a proxy (a database node in one case, or a communication module in the other), in which case there are no signiﬁcant differences between the two approaches. 

Conceptually this is true. Practically, it is not a very helpful abstraction because of its implications as it will be discussed below when the different protocols are compared. For the moment being, note that distributed systems deal with processes while database deal with relational schemas. 

A list of processes is simpler to handle that a database schema, i.e., a communication module can be expected to be able to handle a list of processes but it is not realistic to assume it can handle a database schema. In particular, database replication requires to understand the operation that is going to be performed while in distributed systems, operation semantics usually play no role.

Finally, distributed systems distinguish between deterministic and non-deterministic replica behaviour. Deterministic replica behaviour assumes that when presented with the same operations in the same order, replicas will produce the same results. Such an assumption is very difﬁcult to make in a database. 

Thus, if the different replicas have to communicate anyway in order to agree on a result, they can as well exchange the actual operation. By shifting the burden of broadcast the request to the server, the logic necessary at the client side is greatly simpliﬁed at the price of (theoretically) reducing fault tolerance. If fault tolerance is necessary, a back up system can be used, but this is totally transparent to the client.