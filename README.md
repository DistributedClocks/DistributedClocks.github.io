## Welcome to DistributedClocks!

Making distributed systems make sense.

### Why?

Profiling and instrumenting distributed systems is tricky. The nature of failures in a distributed system makes them generally difficult to reproduce, and therefore analyze. DistributedClocks is a movement towards making this less painful.

### Supported Libraries

- [C](https://github.com/DistributedClocks/CVector)
- [C++](https://github.com/DistributedClocks/CppVector)
- [Java](https://github.com/DistributedClocks/JVector)
- [Golang](https://github.com/DistributedClocks/GoVector)

### VectorClocks

We expose a set of vector clock libraries, based on the concept of Leslie Lamport. 
Vector clocks are used to determine the partial ordering of events in a distributed system, enabling users to determine the flow of causality in a system. 

A vector clock is, for a distributed system executing N processes, a list of N logical clocks. Each logical clock is stored as a map of <ProcessID, Time> pairs. A process increments its time in a logical clock when a relevant event occurs. A process includes its vector clock in all messages that are sent between processes in the distributed system. Thus, when communication occurs between two processes in the system, the processes compare and consolidate vector clocks by taking an element-wise maximum. 

For more information about Vector Clocks: see the [Wikipedia page](https://en.wikipedia.org/wiki/Vector_clock). 

### How to use

As stated above, an essential part of the vector clock algorithm is that processes append their vector clocks to all messages sent between processes, and that they compare their vector clocks after doing so. DistributedClocks is a library that makes management of tis workflow easy.

Let's assume you already have a distributed system up and running. Naturally, these systems will be communicating with one other. Immediately before and after any communication-related calls, simply add a single line of code.

A typical workflow will look like this:
```
1. Have a data payload
2. buffer = PrepareSend(payload)
3. Send this buffer using the network call of your choice
```

And on the receiving side....
```
1. Receive the buffer
2. payload = UnpackReceive(buffer)
```
And that's it! The management and ordering of vector clocks will be handled accordingly. 

### Additional Tooling

We support other libraries that allow users to do more than just determining the ordering of events in a distributed system. 

#### Shiviz

[Shiviz](https://bestchai.bitbucket.io/shiviz/) is a tool which allows users to visualize the output of a DistributedClocks log. 

![](images/shiviz.png?raw=true)

#### Dinv

[Dinv](https://bitbucket.org/bestchai/dinv/) is a tool that helps users find data invariants in a distributed system. 
This is extremely helpful when trying to verify correctness in such a system. 

This page powered by Jekyll.

