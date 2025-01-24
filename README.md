# Leetcode---802
Find Eventual Safe States
// Code in java
import java.util.ArrayList;
import java.util.List;

public class Solution {
    public List<Integer> eventualSafeNodes(int[][] graph) {
        int n = graph.length;
        int[] color = new int[n];
        List<Integer> result = new ArrayList<>();

        for (int i = 0; i < n; i++) {
            if (dfs(graph, color, i)) {
                result.add(i);
            }
        }
        return result;
    }

    private boolean dfs(int[][] graph, int[] color, int node) {
        if (color[node] > 0) {
            return color[node] == 2;
        }
        color[node] = 1;
        for (int next : graph[node]) {
            if (color[next] == 2) {
                continue;
            }
            if (color[next] == 1 || !dfs(graph, color, next)) {
                return false;
            }
        }
        color[node] = 2;
        return true;
    }

    public static void main(String[] args) {
        Solution solution = new Solution();
        int[][] graph = {{1,2},{2,3},{5},{0},{5},{},{}};
        List<Integer> safeNodes = solution.eventualSafeNodes(graph);
        System.out.println("Safe nodes: " + safeNodes);
    }
}
