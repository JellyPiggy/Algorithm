#### [662. 二叉树最大宽度](https://leetcode-cn.com/problems/maximum-width-of-binary-tree/)

```java
class Solution {

    class NodeGreater {
        TreeNode node;
        int id;

        public NodeGreater(TreeNode node, int id) {
            this.node = node;
            this.id = id;
        }
    }

    public int widthOfBinaryTree(TreeNode root) {
        if (root == null) return 0;
        int res = 0;
        LinkedList<NodeGreater> list = new LinkedList<>();
        list.add(new NodeGreater(root, 1));
        while (!list.isEmpty()) {
            int size = list.size();
            int first = 0, last = 0;
            for (int i = 0; i < size; i++) {
                NodeGreater nodeGreater = list.poll();
                TreeNode tNode = nodeGreater.node;
                if (i == 0) first = nodeGreater.id;
                if (i == size - 1) last = nodeGreater.id;
                if (tNode.left != null) {
                    list.add(new NodeGreater(tNode.left,nodeGreater.id * 2));
                }
                if (tNode.right != null) {
                    list.add(new NodeGreater(tNode.right,nodeGreater.id * 2 + 1));
                }
            }
            res = Math.max(res, last - first + 1);
        }
        return res;
    }
}
```

