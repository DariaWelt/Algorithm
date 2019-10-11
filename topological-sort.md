# Topological Sort
+ [Course Schedule 1](#course-schedule-1)

## Course Schedule 1
https://leetcode.com/problems/course-schedule/submissions/

```C++
#define WHITE 0
#define GRAY 1
#define BLACK 2

class Solution {
public:
  bool cycle(int node, vector<vector<int>>& graph, vector<int>& color) {
    if (color[node] == GRAY)
      return true;
    if(graph[node].size() > 0)
      color[node] = GRAY;
    else {
      color[node] = BLACK;
      return false;
    }
    for (size_t i = 0; i < graph[node].size(); ++i) {
      switch (color[graph[node][i]])
      {
      case GRAY:
        return true;
      case BLACK:
        continue;
      case WHITE:
        if (cycle(graph[node][i], graph, color))
          return true;
        else
          color[graph[node][i]] = BLACK;
      }
    }
    color[node] = BLACK;
    return false;
  }
  bool canFinish(int numCourses, vector<vector<int>>& prerequisites) {
    vector<int> color(numCourses, 0);
    vector<vector<int>> graph(numCourses);
    for (size_t i = 0; i < prerequisites.size(); ++i) {
      graph[prerequisites[i][1]].push_back(prerequisites[i][0]);
    }
    for (size_t i = 0; i < numCourses; ++i) {
      if (color[i] == BLACK)
        continue;
      if (cycle(i, graph, color))
        return false;
    }
    return true;
  }
};
```
