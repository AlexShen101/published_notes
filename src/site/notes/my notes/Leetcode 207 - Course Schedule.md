---
{"dg-publish":true,"permalink":"/my-notes/leetcode-207-course-schedule/","created":"2024-10-15T18:54:48.591-05:00","updated":"2024-10-15T18:55:01.086-05:00"}
---


tags:: 
type:: Leetcode_Solution
in:: [[Home/Algorithms MOC\|Algorithms MOC]]

### Leetcode 207 - Course Schedule
- make a prereq map that does crs -> array of all prereqs
- create a visiting set for loop detection
- create a method to memoize previous results (visited set)
- dfs + backtracking with visiting set (to detect loops) + memoization

**Recursive Definition: returns true if course can be taken, false if not**
- if memoized, return memoized result
- if currently visiting - you found a loop, memoize and return False
- add to visiting set, and recurse for all prereqs
	- if any prereq returns False, return False
- if no prereqs returned False (all prereqs can be taken), return True

