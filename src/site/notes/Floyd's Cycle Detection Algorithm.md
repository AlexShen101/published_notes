---
{"dg-publish":true,"permalink":"/floyd-s-cycle-detection-algorithm/","metatags":{"og:title":"Floyd's Cycle Detection Algorithm","og:image":"https://upload.wikimedia.org/wikipedia/commons/thumb/d/d7/Functional_graph.svg/1280px-Functional_graph.svg.png"},"created":"2024-06-10T23:45:02.512-04:00","updated":"2024-06-11T14:56:51.903-04:00"}
---


## Overview
Floyd's Cycle Detection Algorithm, also known as the Tortoise and Hare Algorithm, is used to identify cycles within a data structure such as a linked list. A cycle occurs when a node's next pointer points to a previous node, creating a loop.

The algorithm uses two pointers: a slow pointer and a fast pointer. The slow pointer moves one step at a time, while the fast pointer moves two steps at a time. If there is a cycle, the fast pointer will eventually catch up to the slow pointer. If the pointers meet, a cycle exists; otherwise, the sequence does not contain a cycle.

## General steps of the algorithm:
- Initialize two pointers, both starting at the head of the list.
- Move the slow pointer one step at a time.
- Move the fast pointer two steps at a time.
- If there is a cycle, the fast pointer will eventually meet the slow pointer.
- If the pointers meet, a cycle exists; otherwise, the sequence does not contain a cycle.

## Python Implementation
```python
def check_cycle(head): 
	if not head: 
		return False 
	
	slow = head 
	fast = head 
	
	while fast and fast.next: 
		slow = slow.next 
		fast = fast.next.next 
	
	if slow == fast: 
		return True 
	return False
```

## Complexity Analysis
#### Time Complexity
**Worst Case**: O(n). In the worst case, consider a list that forms a perfect loop. In such a scenario, the fast pointer will have to travel through the entire list to reach the slow pointer, which will take O(n) time.
**Best Case**: O(1). In the best case, consider a single node which points to itself. In such a scenario, the algorithm will terminate in O(1) time.

#### Space Complexity
The algorithm uses O(1) space since it only requires two pointers.

## Finding the Start of the Cycle
Floyd's Cycle Detection Algorithm can be modified to find the node where the cycle begins. This is achieved by determining the first intersection point of the slow and fast pointers within the cycle. The key idea behind this is that distance from the starting point of the list to the start of the cycle is equal to the distance from the intersection point to the start of the cycle. Here is an explanation of why this is true.

Consider a linked list with a cycle. Let:
- A be the start of the list.
- C be the start of the cycle.
- B be the first intersection point of the slow and fast pointers.
- x be the length of the cycle.

Thus, $AC$ represents the distance from the start of the list to the start of the cycle, and $BC$ represents the distance from the first intersection point to the start of the cycle.

The slow pointer travels a distance of $AC + CB$, while the fast pointer travels a distance of $AC + x + CB$. We also know that the fast pointer travels twice as fast as the slow pointer, so the fast pointer also travels a distance of $2(AC + CB)$. We can then set up the equation:
$$
\begin{align*}\\
2(AC + CB) &= AC + x + CB &&\\
2AC + 2CB &= AC + BC + CB + CB\\
2AC &= AC + BC\\
AC &= BC
\end{align*}$$
Thus, we see that the distance from the start of the list to the start of the cycle and the distance from the first intersection point to the start of the cycle are equal.

To find the start of the cycle, we just need to create 2 slow pointers: one at the start of the list and one at the intersection point. Then, we simply need to move each pointer until they intersection, which will be the start of the cycle in the linked list.

## Python Implementation
```python
def determine_cycle_start(head): 
	if not head: 
		return None 
	
	slow = head 
	fast = head 

	# Determine if a cycle exists. If a cycle exists, get the first intersection point of the two pointers
	while fast and fast.next: 
		slow = slow.next 
		fast = fast.next.next 
	
		if slow == fast: break 

	# If no cycle exists
	if not fast or not fast.next: 
		return None 
		
	# Find the start of the cycle 
	slow2 = head 
	while slow != slow2: 
		slow = slow.next 
		slow2 = slow2.next 
	return slow
```

