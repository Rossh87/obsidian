c.f. https://www.youtube.com/watch?v=4rLW7zg21gI,
https://go.dev/blog/waza-talk

A [[Program]] is just a set of instructions that a computer can run, either directly (compiled binary), or through an interpreter (JS, Python).  A program becomes a [[Process]] when the instructions are loaded into memory and the CPU begins executing them.

Processes operate in their own memory address range, in general they do not share memory with other processes, helping to prevent corruption/cross-contamination.

A thread is a context of execution for a process.  It is all the program's state, plus system resources needed for executing the program.  Every process has a least one thread, the **main** thread, and may have more than one.  Threads allow the CPU and kernel resources to pause one task and switch to another, even on a single-processor system.  This prevents any one long-running process from grinding all other processes to a halt.  However, changing threads, or [[Context Switching]], is expensive: the state of one program must be loaded into [[Register]]s, and another loaded into memory before the CPU can resume work.

Programming languages/runtimes offer various constructs to get concurrent behavior with less overhead than preemptive OS threads.  E.g. [[Concurrency]].  C.f.  https://softwareengineering.stackexchange.com/questions/254140/is-there-a-difference-between-fibers-coroutines-and-green-threads-and-if-that-i