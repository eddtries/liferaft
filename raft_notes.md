# My Raft Notes

Raft is a consensus algorithm for managing a replicated log that has an unusual primary goal of being *understandable*. A consensus algorithm is a method of replicating state machines and keeping them in sync, while dealing with issues such as state machines going offline (including the leader!). Replicated state machines are usually built with a replicated log; each server stores a log containing a series of commands and excutes them in the same order. Because the state machines are deterministic, if two state machines run the same log they will end in the same state. The consensus alogirithms job is to keep this replicated log consistent. 

Practical consensus algorithms typically have the following properties:
* Termination
* Integrity
* Agreement

Raft implements consensus by first electing a distinguished *leader*, then giving the leader complete responsibility for managing the replicated log. The leader accepts log entires from clients, replicates them on other servers, and tells servers when it is safe to apply log entries to their state machines. A leader can fail or become disconnected from the other servers, in which case a new leader is elected.

