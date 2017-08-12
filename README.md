## Welcome to DistributedClocks!

Making distributed systems make sense.

### Why?

Profiling and instrumenting distributed systems is tricky. The nature of failures in a distributed system makes them generally difficult to reproduce, and therefore analyze. 

DistributedClocks is a movement towards making this less painful. We expose a set of vector clock libraries, based on a concept of Leslie Lamport, which allow users to determine a total ordering of events in a complicated and choatic environment.

### How to use

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

One the system execution is complete, we recommend visualizing it with [Shiviz](https://bestchai.bitbucket.io/shiviz/)

### Supported Libraries

- [C](https://github.com/DistributedClocks/CVector)
- [C++](https://github.com/DistributedClocks/CppVector)
- [Java](https://github.com/DistributedClocks/JVector)
- [Golang](https://github.com/DistributedClocks/GoVector)

This page powered by Jekyll.

