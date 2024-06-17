---
{"dg-publish":true,"permalink":"/blog/understanding-algorithm-efficiency-with-priori-analysis-and-posteriori-testing/","created":"2024-06-17T17:58:46.707-04:00","updated":"2024-06-17T18:01:32.009-04:00"}
---


To assess the running time of an algorithm, there are 2 approaches:
1. [[notes/posteriori testing\|posteriori testing]]: Creating an executable program of the algorithm, and running it with a series of tests
2. [[notes/priori analysis\|priori analysis]]: Analyzing a theoretical pseudocode of the algorithm using an ideal computer model

## Priori Analysis
Priori analysis is a method of determining the running time and space requirements of an algorithm by analyzing its theoretical behavior. This analysis is performed with respect to a theoretical computer model, such as the [[random access machine model\|random access machine model]]. Since priori analysis is based on a theoretical algorithm, it is both language-independent and hardware-independent.

The goal of priori analysis is to determine a time function and a space function that represent how much time and space the algorithm uses with respect to an input size n.

## Posteriori Testing
Posteriori testing, on the other hand, involves running a program that implements the algorithm. This approach is language-dependent, as different programming languages may have different performance characteristics for the same operations. It is also hardware-dependent, as the hardware used to run the program affects its execution time and memory usage.

The purpose of posteriori testing is to determine the actual running time and memory usage of the algorithm in practice.

## Running Time Functions for Algorithms
In priori analysis, we derive a function that represents the running time of an algorithm. This function is the running time of the algorithm, and is expressed as $T(a, b, c)$ where a, b and c are typically the inputs or factors related to hte input.

While the exact form of this function can be complex, it provides a precise mathematical description of how the running time grows as the input size increases.

## Asymptotic Notation
Asymptotic notation is used to describe the theoretical time and space complexity of an algorithm in terms of its input size. This notation helps provide a high-level understanding of the algorithm's efficiency by describing its behavior as the input size approaches infinity.

Algorithms can have complex time and space functions that are difficult to understand. Thus, we simplify them using asymptotic bounds to make them easier to classify and understand. 

Here are the 5 types of asymptotic bounds:
- [[Big O notation\|Big O notation]]: Describes the upper bound of the function
- [[Big Omega notation\|Big Omega notation]]: Describes the lower bound of the function
- [[Big Theta notation\|Big Theta notation]]: Describes both the upper and lower bound of the function (provides a tight bound)
- [[small o notation\|small o notation]]: Describes the strict upper bound of the function
- [[small omega notation\|small omega notation]]: Describes the strict lower bound of the function
