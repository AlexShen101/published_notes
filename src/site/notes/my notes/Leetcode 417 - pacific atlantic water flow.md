---
{"dg-publish":true,"permalink":"/my-notes/leetcode-417-pacific-atlantic-water-flow/","created":"2024-10-15T18:58:14.716-05:00","updated":"2024-10-15T18:58:25.786-05:00"}
---


tags:: 
type:: Leetcode_Solution
in:: [[Home/Algorithms MOC\|Algorithms MOC]]


# Leetcode 417 - pacific atlantic water flow

- make two sets containing coords
- one of them will contain all tiles which can reach the pacific
- one of them will contain all tiles which can reach the atlantic
- use graph DFS traversal to find all tiles that are added to each set
- return the set intersection
