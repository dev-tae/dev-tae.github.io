# Daily Question 1/10/2024

## [🏠 Back to Home](https://dev-tae.github.io)

## [Amount of Time for Binary Tree to Be Infected](https://leetcode.com/problems/amount-of-time-for-binary-tree-to-be-infected/description/?envType=daily-question&envId=2024-01-10) (Link to Leetcode)

# Intuition
This problem, although initially appearing as a tree question, can actually be approached as a graph problem. The time required for all nodes to be infected can be calculated level by level. Thus, it can be solved using a mix of graph theory and BFS approach.

There is a recursive (DFS) solution as well, but it is more complex, and I couldn't come up with the solution by myself. I would stick with the BFS solution for now.

# Approach 1: Iteration (BFS)
We understand this to be a graph problem. An adjacent list is needed, which is slightly different from a common adjacency list since we are dealing with a tree, not an undirected graph. We need one pass to create an adjacency list using a BFS approach. Additionally, we're going to track the length of the tree for later use.

```
q = deque([root])
adj_list = defaultdict(list)
tree_len = 0
```

We build an adjacency list with a deque. However, it's important to append adjacent lists to each other, as shown below:

![image.png](https://assets.leetcode.com/users/images/7bb09898-12bc-48a9-9a28-b75f2842ab8b_1704922861.4277818.png)

For node 1, the adjacency list would look like this:

adj_list[1] = [5, 3]

But then, we need to add node 1 to the adjacency lists of nodes 5 and 3 as well, since infection can spread from any of these nodes.

adj_list[5] = [1, ...]
adj_list[3] = [1, ...]

Now, we iterate through our queue and build our adjacency list, using only values rather than tree nodes for convenience. We also track the length of the tree during this process.

```
while q:
    for _ in range(len(q)):
        ndoe = q.popleft()
        tree_len += 1
        if node.left:
            adj_list[node.val].append(node.left.val)
            adj_list[node.left.val].append(node.val)
            q.append(node.left)
        if node.right:
            adj_list[node.val].append(node.right.val)
            adj_list[node.right.val].append(node.val)
            q.append(node.right)
```

Having completed our adjacency list, we now require a few more variables for our second iteration. Since we're treating this as a graph problem, we want to keep track of the infected nodes using a set. We start minutes at -1 because we'll increment it in a level-order manner.

```
infected = set()
minutes = -1
```

We can simply add the start value (an integer) to our now-empty queue.

```
q.append(start)
```

We iterate until every node is infected. As mentioned earlier, we increment minutes in level order, thus we start at -1. Nodes that are popped from the queue become infected. Then, we append adjacent nodes to the queue, provided they have not yet been infected.

```
        while len(infected) < tree_len:
            minutes += 1
            for _ in range(len(q)):
                node = q.popleft()
                infected.add(node)                
                for adj_node in adj_list[node]:
                    if adj_node not in infected:
                        q.append(adj_node)
        
        return minutes
```


# Complexity
- Time complexity: O(N)
<!-- Add your time complexity here, e.g. $$O(n)$$ -->

- Space complexity: O(N)
<!-- Add your space complexity here, e.g. $$O(n)$$ -->

# Code
```
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution:
    def amountOfTime(self, root: Optional[TreeNode], start: int) -> int:
        q = deque([root])
        adj_list = defaultdict(list)
        infected = set()
        minutes = -1
        tree_len = 0
        # Build adj_list with a queue
        while q:
            for _ in range(len(q)):
                node = q.popleft()
                tree_len += 1
                if node.left:
                    adj_list[node.val].append(node.left.val)
                    adj_list[node.left.val].append(node.val)
                    q.append(node.left)
                if node.right:
                    adj_list[node.val].append(node.right.val)
                    adj_list[node.right.val].append(node.val)
                    q.append(node.right)
        
        q.append(start)

        while len(infected) < tree_len:
            minutes += 1
            for _ in range(len(q)):
                node = q.popleft()
                infected.add(node)                
                for adj_node in adj_list[node]:
                    if adj_node not in infected:
                        q.append(adj_node)
        
        return minutes
                    
```