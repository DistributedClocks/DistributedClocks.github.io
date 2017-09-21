## Welcome to DistributedClocks

Profiling and instrumenting distributed systems is tricky. The nature of failures in a distributed system makes them difficult to reproduce, and analyze. This project maintains a suite of libraries for instrumenting systems in several different languages with logical distributed clock timestamps. An instrumented system produces logs that can be analyzed to deduce a variety of useful information regarding a system execution, such as whether an event e preceded or happened after some other event f. The current focus of the library is on [vector clock](https://en.wikipedia.org/wiki/Vector_clock) timestamps.

### Supported languages, with a library for each one:

- [C](https://github.com/DistributedClocks/CVector)
- [C++](https://github.com/DistributedClocks/CppVector)
- [Java](https://github.com/DistributedClocks/JVector)
- [Golang](https://github.com/DistributedClocks/GoVector)

### What are VectorClocks?

Vector clocks are used to establish the partial ordering of events in a distributed system, enabling users to determine the flow of potential causality in a system. 

For a distributed system executing N processes, a vector clock is a list of N logical clocks. Each logical clock is stored as a map of <ProcessID, Time> pairs. A process increments its time in a logical clock when a relevant event occurs. A process includes its vector clock in all messages that are sent between processes in the distributed system. Thus, when communication occurs between two processes in the system, the processes compare and consolidate vector clocks by taking an element-wise maximum. 

For more information about Vector Clocks: see the [wikipedia page](https://en.wikipedia.org/wiki/Vector_clock). 

### How do I use these libraries?

An essential part of the vector clock algorithm is that processes must append a vector clock timestamp on all messages they send. DistributedClocks libraries simplify this process.

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

### Log analysis tools

Logs produced by DistributedClocks libraries are compatible with several tools that make it easier to understand the execution of a distributed system.

#### Visualizing executions using ShiViz

[Shiviz](https://bestchai.bitbucket.io/shiviz/) allows users to visualize the output of a DistributedClocks log as a time-space diagram:

![](images/shiviz.png?raw=true)

#### Inferring distributed data invariants using Dinv

[Dinv](https://bitbucket.org/bestchai/dinv/) finds distributed data invariants for a distributed system. These can be helpful when trying to check that the system is correct.
