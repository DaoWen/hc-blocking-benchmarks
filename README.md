# Habanero-C Benchmarks for Blocked Worker Contexts

This repository contains a set of benchmarks
for evaluating the overhead of different strategies
for handling blocked workers in Habanero-C.

## The Strategies

The strategies include the following:

- A performance baseline using a fixed worker thread pool
  with the global-helping optimization (sometimes called master/helper),
  which is not safe for general blocking constructs like promises.
- A compiler-based transformation using a form of continuation passing style
  that splits tasks at each possible blocking runtime API call.
  This strategy depends on the legacy Habanero-C language compiler toolchain.
- A manual re-write of HClib code to use only non-blocking constructs.
  A top-level <tt>finish</tt> construct is allowed in order to synchronize
  the Habanero-C program within the serial C <tt>main</tt> function.
- Automatic compensation of blocked workers via creation of new kernel threads.
  This strategy can also be augmented by the finish-helping optimization.
- Automatic compensation of blocked workers via creation of new fibers.
  This strategy can also be augmented by the finish-helping optimization.

## The Benchmarks

We include multiple versions of the following benchmarks,
each specialized for one or more of the aforementioned strategies:

- Cholesky factorization
- Cilksort
- Fibonacci
- Needleman-Wunsch
- N-Queens
- Quicksort
- Unbalanced Tree Search (UTS)

## Further Reading

An analysis of these blocking strategies in the context of these benchmarks
is included in the text of Nick Vrvilo's PhD dissertation:

<https://habanero.rice.edu/vrvilo-phd>
