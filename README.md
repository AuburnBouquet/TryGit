# Interesting Coding Questions

## Minimize costs for a product

### Description

Given a sequence of positive integers `A` with length `n` and a target product `B`, find the minimum cost to make the product of all the numbers equal to `B`. One "cost" is defined as incrementing or decrementing a number `A[i]` by one. Note that the resulting numbers should still be positive integers.

Input:
- A sequence of positive integers `A` with length `n`
- A positive integer `B`

Output:
- The minimum cost `c`

Constraints:

<img src="http://latex.codecogs.com/gif.latex?1\le{n}\le{10^3}" />, <img src="http://latex.codecogs.com/gif.latex?1\le{B}\le{10^5}" />, and <img src="http://latex.codecogs.com/gif.latex?1\le{A_i}\le{10^5}" />

### Examples
```
Input:
1 3 9 2 6
12
Output:
10
```


## Back to the starting point after k steps in a circle

### Description

Suppose we have a circle of `n` nodes, find how many ways we can go back to the starting point after `k` steps.

### Solution

```{c++}
// Dynamic Programming
// Time Complexity: O(kn)   Space Complexity: O(n)
int back_ways(int n, int k)
{
    if(n == 1)
        return 1;
    if(n == 2)
        return k % 2 ? 1 : 0;

    vector<vector<int>> memo(2, vector<int>(n, 0));

    int switcher = 1;
    memo[0][0] = 1;
    
    for(int j = 1; j <= k; ++j)
    {
        for(int i = 0; i < n; ++i)
            memo[switcher][i] = memo[!switcher][(i+n-1) % n] 
                              + memo[!switcher][(i+1) % n];
        
        switcher = !switcher;
    } // for

    return memo[!switcher][0];
}
```
