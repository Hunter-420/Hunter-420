# Nischal Khanal

Software engineer focused on high-performance systems, low-latency infrastructure, and market microstructure.

My work sits at the intersection of network programming, exchange architecture, and performance engineering. I build from scratch, measure everything, and treat bottleneck removal as the core discipline.

**Website:** [khanalnischal.com.np](https://khanalnischal.com.np) &nbsp;|&nbsp; **LinkedIn:** [nischalkhanal](https://linkedin.com/in/nischalkhanal) &nbsp;|&nbsp; **X:** [@NischalKha7180](https://x.com/NischalKha7180) &nbsp;|&nbsp; **Email:** khanalnischal2075@gmail.com

---

## Current Project

### [High-Performance TCP Order Matching Engine](https://www.khanalnischal.com.np/projects/high-performance-tcp-order-matching-engine)

A from-scratch, single-threaded electronic limit order book (LOB) built in C++ for correctness, determinism, and sub-microsecond latency. The design problem: process a high-volume, concurrent, stateful stream of sequential financial transactions without introducing latency fluctuations caused by OS kernel overhead, thread context-switching, lock contention, or heap fragmentation.

**Architecture decisions:**

**Order Book:** `std::map` price index over a custom doubly-linked list. Every node lives inside a pre-allocated flat memory arena — no heap allocation on the hot path, zero pointer-chasing from scattered allocations.

**Memory:** A `std::vector<OrderNode>` arena with 1,000,000 pre-allocated slots at boot. `borrow_node()` and `return_node()` replace `new`/`delete` entirely. Verified with `strace` to produce zero `brk`/`mmap` calls during execution.

**Networking:** Single-threaded `epoll` event loop, non-blocking sockets, thread pinned to a dedicated CPU core. Zero lock contention. No context-switching.

**Serialization:** Fixed-width binary protocol. Incoming network buffers are cast directly to a packed `OrderRequest` struct via `reinterpret_cast` — no string parsing, no tokenization.

**Latency suppression:** `TCP_NODELAY` set on all sockets to disable Nagle's algorithm and force immediate transmission of execution reports.

**Telemetry:** In-memory ring buffer logging `recv()` → `send()` timestamps using `std::chrono::high_resolution_clock`. No disk writes on the critical path. Target: p50 < 2µs, p99.9 < 10µs.

**Profiling:** `perf` for hardware cache-miss analysis, `strace` for syscall verification.

**Stack:** `C++17` `C++20` `g++` `clang++` `Linux epoll API` `POSIX Threads (pthread)` `Non-blocking Sockets` `Fixed-Width Binary Serialization` `Memory Arenas` `TCP_NODELAY` `strace` `perf` `Makefile` `Python`

---

## Writing

I write technical posts on systems I'm actively building or studying.

**Networking and communication between machines:** How data moves across systems, where latency originates in the network stack, and what the kernel does between `send()` and wire.

**Systems engineering fundamentals:** OS scheduling, memory behavior, concurrency models, and how low-level decisions propagate upward.

**Market infrastructure:** Order book design, matching engine architecture, market data distribution, and how infrastructure creates measurable advantages.

**Performance engineering:** Bottleneck identification, system measurement, tail-latency analysis, and the tradeoffs between throughput, reliability, and speed.

→ [All writing](https://www.khanalnischal.com.np/writing)

**Recent posts:**
- [Decoupled Vector-Map Data Layout for Allocation-Free Limit Order Book](https://www.khanalnischal.com.np/writing/decoupled-vector-map-data-layout-for-allocation-free-limit-order-book) *(Jun 2026)*
- [Python GIL Trap in Low-Latency Async Pipelines](https://www.khanalnischal.com.np/writing/python-gil-trap-in-low-latency-async-pipelines) *(Jun 2026)*
- [Stabilizing a High-Frequency Trading Gateway Under Extreme Market Volatility](https://www.khanalnischal.com.np/writing/stabilizing-a-high-frequency-trading-gateway-how-we-reclaimed-our-event-loop-under-extreme-market-volatility) *(Jun 2026)*

---

## Currently Exploring

**Networking and communication:** TCP/IP systems, sockets, latency, throughput

**Systems fundamentals:** Operating systems, concurrency, scheduling, memory behavior, distributed systems

**Market infrastructure:** Order books, matching engines, market data systems, exchange architecture, market microstructure

**Performance engineering:** Bottleneck analysis, system measurement, optimization, real-time systems

→ [Full exploration map](https://www.khanalnischal.com.np/exploring)

---

## Technical Stack

**Languages & Compilers:** `C++17` `C++20` `Python` `g++` `clang++`

**Systems & OS:** `Linux Kernel` `POSIX Threads (pthread)` `Linux epoll API` `Non-blocking Sockets` `Makefile`

**Performance & Networking:** `TCP_NODELAY` `Fixed-Width Binary Serialization` `Memory Arenas` `strace` `perf`

---

## Certifications

**AWS Certified Solutions Architect – Associate** · Amazon Web Services · Jun 2026

**Registered IT Engineer** · Nepal Engineering Council · Jan 2026 · [#97224](https://nec.gov.np/registration/97224)

**Mathematical Thinking in Computer Science** · Coursera · Mar 2022

**Programming for Everybody (Getting Started with Python)** · Coursera · Feb 2022

→ [All certifications](https://www.khanalnischal.com.np/certifications) &nbsp;|&nbsp; [Resume](https://www.khanalnischal.com.np/resume)
