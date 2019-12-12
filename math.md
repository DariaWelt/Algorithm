# Math
+ [Fibonacci Number](#fibonacci-number)
+ [Count Primes](#count-primes)

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

## Count Primes
https://leetcode.com/problems/count-primes/

```C++
int countPrimes(int n) {
    if (n < 2)
        return 0;
    vector<int> prime(n, 1);
    prime[0] = prime[1] = 0;
    for (int i = 0; i < sqrt(n); ++i) {
        if (prime[i]) {
            for (int j = i * i; j < n; j += i)
                prime[j] = 0;
        }
    }
    int res = 0;
    for (int i = 0; i < n; res += prime[i++]);
    return res;
}
```
