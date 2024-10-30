# Min cost to connect all points
### https://leetcode.com/problems/min-cost-to-connect-all-points

You are given an array points representing integer coordinates of some points on a 2D-plane, where points[i] = [xi, yi].

The cost of connecting two points [xi, yi] and [xj, yj] is the manhattan distance between them: |xi - xj| + |yi - yj|, where |val| denotes the absolute value of val.

Return the minimum cost to make all points connected. All points are connected if there is exactly one simple path between any two points.

 
```
Example 1:


Input: points = [[0,0],[2,2],[3,10],[5,2],[7,0]]
Output: 20

Explanation: 

We can connect the points as shown above to get the minimum cost of 20.
Notice that there is a unique path between every pair of points.

Example 2:

Input: points = [[3,12],[-2,5],[-4,1]]
Output: 18
``` 

### Constraints:

1. 1 <= points.length <= 1000
2. -10^6 <= xi, yi <= 10^6
3. All pairs (xi, yi) are distinct.

# Implementation : Prim's Algorithm 
```java
class Solution {
    public int minCostConnectPoints(int[][] points) {
        int nodes = points.length;
        PriorityQueue<int[]> queue = new PriorityQueue<>((v1, v2) -> v1[1] - v2[1]);
        queue.add(new int[]{0,0});
        Set<Integer> visited = new HashSet<>();
        int minCost = 0;
        while(!queue.isEmpty()) {
            int[] node = queue.remove();
            if(visited.contains(node[0]))
              continue;
            visited.add(node[0]);
            minCost += node[1];
            for(int point = 0; point < nodes; point++) {
                if(!visited.contains(point)) {
                    int[] p1 = points[node[0]];
                    int[] p2 = points[point];
                    int distance = Math.abs(p1[0] - p2[0]) + Math.abs(p1[1] - p2[1]);
                    queue.add(new int[]{point, distance});
                }
            }

        }
        return minCost;
    }
}
```
