# PRStar

## Description

PRStar is a work-in-progress implementation of `P(R*_{3, 0, 1})`, aka 3D Projective Geometric
Algebra. In contrast to other GA libraries, PRStar does not attempt to generalize the metric or
dimensionality of the space. In exchange for this loss of generality, PRStar implements the
algebraic operations using the full weight of SSE (Streaming SIMD Extensions) for maximum
throughput.

## Requirements

- Machine with a processor that supports SSE4.1 or later (has ~97% market penetration)
- C++17 compliant compiler

## Motivation

PGA fully streamlines traditionally used quaternions, and dual-quaternions in a single algebra.
Normally, the onus is on the user to perform appropriate casts and ensure signs and memory layout
are accounted for. Here, all types are unified within the geometric algebra,
and operations such as quaternion _ dual-quat (rotor _ motor) compositions make sense.

## Performance Considerations

It is known that a "better" way to vectorize computation in general is to arrange the data in an SoA
layout to avoid unnecessary cross-lane arithmetic or unnecessary shuffling. PGA is unique in that
a given PGA multivector has a natural decomposition into 4 blocks of 4 floating-point quantities.
For the even sub-algebra (isomorphic to the space of dual-quaternions) also known as the _motor
algebra_, the geometric product can be densely packed and implemented efficiently using SSE.

# sym_shell

A simple command line REPL (Read Eval Print Loop) is provided to perform
symbolic evaluation of GA expressions. This is a work-in-progress.

## TODO

- Conditionally support FMA (~75% market penetration)
- Provide a fallback for SSE2 in case SSE4.1 isn't available
- Sandwich operator
- Exterior product
- Reversion
- Norms
- Matrix conversion
