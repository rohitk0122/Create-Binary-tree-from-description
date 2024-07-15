# Create-Binary-tree-from-description
/**
 * Definition for a binary tree node.
 * public class TreeNode {
 *     int val;
 *     TreeNode left;
 *     TreeNode right;
 *     TreeNode() {}
 *     TreeNode(int val) { this.val = val; }
 *     TreeNode(int val, TreeNode left, TreeNode right) {
 *         this.val = val;
 *         this.left = left;
 *         this.right = right;
 *     }
 * }
 */
class Solution {
    public TreeNode createBinaryTree(int[][] descriptions) {
        Map<Integer, TreeNode> nodeMap = new HashMap<>();
        Set<Integer> children = new HashSet<>();

        // Create nodes and build the tree structure
        for (int[] description : descriptions) {
            int parentVal = description[0];
            int childVal = description[1];
            boolean isLeft = description[2] == 1;

            // Get or create the parent node
            TreeNode parentNode = nodeMap.getOrDefault(parentVal, new TreeNode(parentVal));
            nodeMap.put(parentVal, parentNode);

            // Get or create the child node
            TreeNode childNode = nodeMap.getOrDefault(childVal, new TreeNode(childVal));
            nodeMap.put(childVal, childNode);

            // Set the child node to the correct position
            if (isLeft) {
                parentNode.left = childNode;
            } else {
                parentNode.right = childNode;
            }

            // Add the child value to the set of children
            children.add(childVal);
        }

        // Find the root (a node that is not any child)
        TreeNode root = null;
        for (int val : nodeMap.keySet()) {
            if (!children.contains(val)) {
                root = nodeMap.get(val);
                break;
            }
        }

        return root; 
    }
}
