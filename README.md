# BFS-1
# Problem 1
Binary Tree Level Order Traversal (https://leetcode.com/problems/binary-tree-level-order-traversal/)
## Solution 1


## Using BFS
## Time complexity:O(n) Space Complexity:O(n/2)
class Solution {
    public List<List<Integer>> levelOrder(TreeNode root) {
       List<List<Integer>> result=new ArrayList<>();
       if(root==null) return result;
       Queue<TreeNode> q=new LinkedList<>();
       q.add(root);


       while(!q.isEmpty()){
        List<Integer> temp=new ArrayList<>();
        int size=q.size();
        for(int i=0;i<size;i++){
            TreeNode curr=q.poll();
            temp.add(curr.val);
            if(i==size-1)
            {  
                
                result.add(temp);
            }
            if(curr.left!=null)
            {
                q.add(curr.left);
            }
            if(curr.right!=null)
            {
                q.add(curr.right);
            }

        }
       }
       return result;
    }
}


## Using DFS
## Time Complexity:O(n) Space Complexity:O(h)
class Solution {
    List<List<Integer>> result;
    public List<List<Integer>> levelOrder(TreeNode root) {
       this.result =new ArrayList<>();
       if(root==null) return result;
       helper(root,0);
       return result;
    }
    public void helper(TreeNode root,int depth)
    {
        if(root==null) return;

        if(result.size()==depth)
        {
            result.add(new ArrayList<>());
        }

        result.get(depth).add(root.val);
        helper(root.left,depth+1);
        helper(root.right,depth+1);

    }
}



# Problem 2
Course Schedule (https://leetcode.com/problems/course-schedule/)
## Solution 2
## Time Complexity :O(v+e) Space Complexity:O(v+e)
class Solution {
    public boolean canFinish(int numCourses, int[][] prerequisites) {
        int[] indegrees=new int[numCourses];
        HashMap<Integer,List<Integer>>map=new HashMap<>();

        for(int[] pr:prerequisites){
            indegrees[pr[0]]++;

            if(!map.containsKey(pr[1])){
                map.put(pr[1],new ArrayList<>());

            }
            map.get(pr[1]).add(pr[0]);
            
            
        }
        int count=0;
        Queue<Integer> q=new LinkedList<>();

        for(int i=0;i<numCourses;i++)
        {
            if(indegrees[i]==0)
            {
                q.add(i);
                count++;
            }
        }

        if(count==numCourses) return true;
        if(q.isEmpty()) return false;
    
        while(!q.isEmpty())
        {
             int n=q.poll();
            List<Integer> depen=map.get(n);
           
            if(depen!=null){
            for(int i=0;i<depen.size();i++)
            {
                indegrees[depen.get(i)]--;
                if(indegrees[depen.get(i)]==0)
                {
                    q.add(depen.get(i));
                    count++;
                    if(count==numCourses) return true;
                }
                
                

            }
            }

        }
        return false;
    }
}
