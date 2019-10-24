# Topological Sort
+ [Course Schedule I](#course-schedule-i)
+ [Course Schedule II](#course-schedule-ii)
+ [Alien Dictionary](#alien-dictionary)

## Course Schedule I
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
    if(color[node] == WHITE) {
        color[node] = GRAY;
        for (size_t i = 0; i < graph[node].size(); ++i) {
            switch (color[graph[node][i]]) {
                case GRAY:
                    return true;
                case WHITE:
                    if (cycle(graph[node][i], graph, color))
                        return true;
                    else
                        color[graph[node][i]] = BLACK;
            }
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
        if (color[i] != BLACK && cycle(i, graph, color))
            return false;
    }
    return true;
  }
};
```
## Course Schedule II
https://leetcode.com/problems/course-schedule-ii/solution/

```C++
#define WHITE 0
#define GRAY 1
#define BLACK 2

class Solution {
private:
  vector<int> orderSchedule;
public:
  bool cycle(int node, vector<vector<int>>& graph, vector<int>& color) {
    if (color[node] == GRAY)
        return true;
    if(color[node] == WHITE) {
        color[node] = GRAY;
        for (size_t i = 0; i < graph[node].size(); ++i) {
            switch (color[graph[node][i]]) {
                case GRAY:
                    return true;
                case WHITE:
                    if (cycle(graph[node][i], graph, color))
                        return true;
                    else
                        color[graph[node][i]] = BLACK;
            }
        }
    }
    orderSchedule.push_back(node);
    color[node] = BLACK;
    return false;
  }
  vector<int> findOrder(int numCourses, vector<vector<int>>& prerequisites) {
    vector<int> color(numCourses, 0);
    vector<vector<int>> graph(numCourses);
    for (size_t i = 0; i < prerequisites.size(); ++i) {
      graph[prerequisites[i][0]].push_back(prerequisites[i][1]);
    }
    for (size_t i = 0; i < numCourses; ++i) {
      if (color[i] != BLACK && cycle(i, graph, color))
        return vector<int>(0);
    }
    return orderSchedule;
  }
};
```

## Alien Dictionary
https://www.lintcode.com/problem/alien-dictionary/description

```C++
#define WHITE 0
#define GRAY 1
#define BLACK 2
#define NO -1

class Solution {
private:
  string orderLetters;
public:
  bool cycle(int node, vector<vector<char>>& graph, vector<int>& color) {
    if (color[node] == GRAY)
      return true;
    if (graph[node].size() > 0)
      color[node] = GRAY;
    else {
      orderLetters.push_back(node + 'a');
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

    orderLetters.push_back(node + 'a');
    return false;
  }
  string alienOrder(vector<string> &words) {
    vector<int> color('z' - 'a' + 1, NO);
    vector<vector<char>> graph('z' - 'a' + 1);
    for (size_t i = 0; i < words.size() - 1; ++i) {
      size_t j = 0;
      for (j; j < words[i].size() && j < words[i + 1].size() && words[i][j] == words[i + 1][j]; ++j){
          color[words[i][j] - 'a'] = WHITE;
      }
      graph[words[i + 1][j] - 'a'].push_back(words[i][j] - 'a');
      if (i == 0)
        for (size_t k = j; k < words[i].size(); ++k){
            color[words[i][k] - 'a'] = WHITE;
        }
      for (size_t k = j; k < words[i + 1].size(); ++k){
        color[words[i + 1][k] - 'a'] = WHITE;
      }
    }
    for (size_t i = 0; i < 'z' - 'a' + 1; ++i) {
      if (color[i] == BLACK || color[i] == NO)
        continue;
      if (cycle(i, graph, color))
        return "";
    }
    return orderLetters;
  }
};
```
