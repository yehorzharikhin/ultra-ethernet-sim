# Future Research Directions

While this simulator establishes a baseline for comparing routing algorithms in lossy networks, several paths remain for extending this work to match the full complexity of the Ultra Ethernet Consortium (UEC) goals.

### 1. Lossless Ethernet (RoCEv2 & PFC)
Currently, the simulator drops packets when buffers overflow. In RDMA environments, **Priority Flow Control (PFC)** is used to pause traffic before drops occur.
* **Proposed Implementation:** Implement "Pause Frames" that propagate backpressure from switch to sender.
* **Hypothesis:** PFC will eliminate drops but introduce **Congestion Spreading** and **Victim Flow Blocking**, potentially causing deadlocks in the Fat-Tree.

### 2. Incast Workloads
The current "Permutation" traffic creates *path* congestion. "Incast" (Many-to-One) traffic creates *destination* congestion.
* **Proposed Implementation:** Simulate MapReduce-style shuffle phases where 100+ servers target a single receiver simultaneously.
* **Hypothesis:** Adaptive Routing will fail to solve Incast (as the bottleneck is the last mile). Only aggressive, receiver-driven Congestion Control (like Homa or NDP) will suffice.

### 3. Advanced CC Algorithms
* **Timely / DCQCN:** Implement RTT-based gradient congestion control rather than simple ECN step-marking.
* **Multipath Transport:** Allow a single flow to utilize multiple sub-flows with reordering resilience (MPTCP style logic for Datacenters).