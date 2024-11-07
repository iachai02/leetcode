# 124. Binary Tree Maximum Path Sum

A path in a binary tree is a sequence of nodes where each pair of adjacent nodes in the sequence has an edge connecting them. A node can only appear in the sequence at most once. Note that the path does not need to pass through the root. The path sum of a path is the sum of the node's values in the path. Given the root of a binary tree, return the maximum path sum of any non-empty path.

## Solution

```python
def maxPathSum(self, root: TreeNode) -> int:
    res = float("-inf") # placeholder

    # return max path sum without splitting
    def dfs(root):
        nonlocal res
        if not root:
            return 0

        leftMax = dfs(root.left)
        rightMax = dfs(root.right)
        leftMax = max(leftMax, 0)
        rightMax = max(rightMax, 0)

        # compute max path sum WITH split
        res = max(res, root.val + leftMax + rightMax)

        return root.val + max(leftMax, rightMax)

    dfs(root)
    return res[0]
```

- Time: `O(n)`
- Space: `O(h)` where h is the height of the tree
