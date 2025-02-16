---
{"dg-publish":true,"permalink":"/my-notes/leetcode-198-house-robber/","created":"2024-10-14T22:58:30.527-05:00","updated":"2024-10-14T22:58:35.393-05:00"}
---


tags:: 
type:: Leetcode_Solution
in:: [[Algorithms MOC\|Algorithms MOC]]

[[q-Leetcode 198 - house robber\|q-Leetcode 198 - house robber]]

### Leetcode 198 - house robber
- determine what is more profitable:
	- robbery of current house + loot before the previous house (val + rob(i-2))
	- loot from the previous house and before (rob(i-1))
- use a memoization array

[[Dynamic Programming\|Dynamic Programming]]

