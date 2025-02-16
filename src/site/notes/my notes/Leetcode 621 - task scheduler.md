---
{"dg-publish":true,"permalink":"/my-notes/leetcode-621-task-scheduler/","created":"2024-10-12T21:37:08.310-05:00","updated":"2024-10-12T22:01:35.472-05:00"}
---


tags:: 
type:: Leetcode_Solution
in:: [[Home/Algorithms MOC\|Algorithms MOC]]


### approach 1 - brute force with heap
- simulate the cpu
- make a timer, make a cooldown deque, make a heap of tasks to perform

### approach 2 - greedy
- the time it task to complete the tasks is `len(tasks) + idle`.
- the optimal approach is to cycle tasks based on the gap, using the most frequent task (A) as the decider
	- Eg: A---A---A---A
- and then insert other tasks as evenly as possible as well:
	- ABCDAB-DAB--A
	- since every other task has a lower frequency of A, you can put 1 task per gap
- if you still have spaces, you have idle time. if not, then you have no idle time