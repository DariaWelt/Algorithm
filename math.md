# Math
+ [Fibonacci Number] (#fibonacci-number)

## Fibonacci Number
https://leetcode.com/problems/fibonacci-number/

Reqursion
```C++
class Solution {
public:
  int fib(int N) {
    if (N <= 1)
      return N;
    return fib(N - 1) + fib(N - 2);
  }
};  
```

Reqursion + memoization
```C++
class Solution {
private:
  int mem[2] = {0, 1}; 
  bool i = 0;
public:
  int memoize (int N){
    if (N == 0)
      return mem[i];
    mem[i] = mem[i] + mem[!i];
    i = !i;
    return memoize(N-1);
  }
  int fib(int N) {
    if (N < 2)
      return N;
    return memoize(N);
  }
};  
```

Iteration
```C++
class Solution {
private:
  int mem[2] = {0, 1}; 
  bool i = 0;
public:
  int fib(int N) {
    if (N < 2)
      return N;
    for(int n = 0; n < N; ++n){
      mem[i] = mem[i] + mem[!i];
      i = !i;
    }
    return mem[i];
  }
};  
```
