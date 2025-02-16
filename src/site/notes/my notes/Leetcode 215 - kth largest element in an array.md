---
{"dg-publish":true,"permalink":"/my-notes/leetcode-215-kth-largest-element-in-an-array/","created":"2024-10-12T21:40:40.503-05:00","updated":"2024-10-12T22:01:31.572-05:00"}
---


tags:: 
type:: Leetcode_Solution
in:: [[Algorithms MOC\|Algorithms MOC]]


use a min heap storing k elements
- this is the k largest elements

if there are more than k elements, insert the rest in
the kth largest element will be the top of the min heap at the end

another option is sorting