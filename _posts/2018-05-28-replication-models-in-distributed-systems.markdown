---
layout: post
title:  "Replication models in distributed systems"
date:   2018-05-28 22:04:00 +0800
categories: Replication
---
TAG: `Replication` `Distributed System`

Fault tolerance is a very crucial property for distributed systems, because the network is not reliable, and expects to be likely to fail at any time. That means in order to make the distributed system to work properly, we have to replicate data into different nodes, so that any node fails, the data is not actually lost. Here in this post I am going to introduce the common and different strageties to implement replication in distributed systems.

#### Group Communication Primitives

The distributed systems are a set of processes running in different nodes. These services offer different endpoints for clients to invoke. Once the client sends in a invoking request, the services need to react with this request and make some internal changes. So each service maintains a local state, and the proper replication makes sure that the state change is a atomic operation, meaning the state of different services should be consistent. That is, either all the replicas are updated, either not for all nodes. The services can't be partially updated, otherwise the inconsistence will send out different results for clients. 

To cope with the complexity of replication, the notion of group and group communication primitives have been introduced. These primitives provide one-to-many communication with various powerful semantics. These semantics hide much of the complexity of maintaining the consistency of replicated servers. The two main are Atomic Broadcast (or ABCAST) and View Synchronous Broadcast (or VSCAST). 

**ABCAST.** Atomic Broadcast provides atomicity and total order. Let m and m' be two messages that are ABCAST to the same group g of servers. The atomicity property ensures that if one member of g delivers m (respt m') then all (not crashed) members of g eventually deliver m (respt. m). The order property ensures that if two members of g deliver both m and m', they deliver them in the same order.

**VSCAST.** The definition of View Synchronous Broadcast is more complex. It is defined in the context of a group g and is based on the notion of a sequence of views v0(g), v1(g),...,vi(g),...of group g. Each view vi(g) defines the composition of the group at same time t, i.e. the members of the group that are preceived as being correct at time t. Whenever a process p in some view vi(g) is suspected to have crashed, or some process q wants to join, a new view vi+1(g) is installed, which reflects the membership change.

Roughly speaking, VSCAST of message m by some member of the group g currently in view vi(g) ensures the following property: if one process p in vi(g) delivers m before installing view vi+1(g), than no process installs view vi+1(g) ebfore having first delivered m.

#### Active Replication

Active replication is a decentralized replication technique, whose core concept is that all replicas receive and process the same sequence of client requests. Consistency is guaranteed by assuming that when provided with the same input in the same order, replicas will produce the same output. This assumption implies that servers process requests in a deterministic way.

The main advantages of active replication is its simplicity, and failure transparency. Failures are fully hidden from the clients, since if a replica fails, the requests are still processed by the other replicas.

The determinism constraint is the major drawback of this approach. Someone will argue that the performance looks low. But processing a request at only one node and transmitting the state changes to the others in some cases, may be much more complex and expensive. So the performance actually is OK, not that bad.

![Active Replication](https://raw.githubusercontent.com/ywchang/ywchang.github.io/master/_imgs/active-replication.png)

Following steps are involved in active replication. 

* 1. The client sends the request to the servers using an Atomic Broadcast.
* 2. Server coordinate is given by the total order of property of the Atomic Broadcast.
* 3. All replicas execute the request in the order they are delivered. 
* 4. No coordination is necessary, as all replicas process the same request in the same order. Because replicas are deterministic, they all produce the same results.
* 5. All replica send back their result to the client, and the client typically only waits for the first answer(the others are ignored). 

#### Passive Replication