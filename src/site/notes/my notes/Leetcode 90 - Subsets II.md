---
{"dg-publish":true,"permalink":"/my-notes/leetcode-90-subsets-ii/","created":"2024-10-12T21:35:26.317-05:00","updated":"2024-10-12T21:36:04.909-05:00"}
---


tags:: 
type:: Leetcode_Solution
in:: [[Algorithms MOC\|Algorithms MOC]]


Key idea:
- dfs + backtracking
	- [[backtracking algorithm\|backtracking algorithm]]
	- [[Depth First Search (DFS)\|Depth First Search (DFS)]]

the dfs function does the following
- base case: if reached the end of the array, you have created a subset
- to create a subset, there are two choices
	- part 1: include (one or more) of the current number x. 
		- If the array still has x's available, you have the choice to include them too
	- part 2: choose to include 0 of the current number x, and move on to the next number y
		- this is how we exclude elements from a subset.
