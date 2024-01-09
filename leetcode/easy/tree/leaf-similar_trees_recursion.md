Daily Question 1/9/2024

# [🏠 Back to Home](https://dev-tae.github.io)

# [Leaf-Similar Trees](https://leetcode.com/problems/leaf-similar-trees/description/?envType=daily-question&envId=2024-01-09)

# Intuition
Most tree questions can be solved using either depth-first search (DFS) or breadth-first search (BFS), or both. Leaves of a tree can be easily accessed using a pre-order traversal approach, making recursion a fitting strategy for this problem.

![image.png](https://assets.leetcode.com/users/images/51535739-3f03-4e96-8705-0ca36ff39488_1704820092.3902779.png)

Sequence: (6 -> 7 -> 4 -> 9 -> 8)

*BFS makes code way too long since we have to take care of two trees. We would possibly have many if statements to take care of both trees. Hence, it's better to use a dfs for this question. I usually try to come up with both dfs and bfs solutions, but it was unnecessary this time.

# Approach
With recursion, determining the base case is crucial. For tree traversals, a common base case is when we've reached a null node, indicating the end of a path.


```
if not node:
   return None
```

Another base case is required for this question since we need to identify leaf nodes and store their values. A node is a leaf when it has no children.

```
if not node.left and not node.right:
   arr.append(node.val)
```

After handling the leaf case, we continue the DFS for left and right subtrees. Finally, we return the array containing the leaf values.
```
dfs(node.left, arr)
dfs(node.right, arr)

return arr
```

# Complexity
- Time complexity: O(N)


- Space complexity: O(N)

# Code
```
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution:
    def leafSimilar(self, root1: Optional[TreeNode], root2: Optional[TreeNode]) -> bool:
        def dfs(node, arr):
            if not node:
                return None
            if not node.left and not node.right:
                arr.append(node.val)
                
            dfs(node.left, arr)
            dfs(node.right, arr)

            return arr

        res1 = dfs(root1, [])
        res2 = dfs(root2, [])
        
        return res1 == res2 
```
