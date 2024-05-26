# Instabug-internship-assessment
This repository contains solutions to the problems of Instabug internship assessment problem-solving section

## Problem 1: Easy Version

### Description
Sayed has a distributed system that consists of multiple machines. Each machine requires a specific amount of RAM, CPU, and Disk units to run. The cluster Sayed is working with has a maximum capacity of RAM, CPU, and Disk units. Help Sayed figure out the maximum number of machines he can run in his cluster.

### Input
- The first line of input contains an integer `T` (1 ≤ T ≤ 30), representing the number of test cases.
- For each test case:
  - The first line contains three integers `R`, `C`, `D` (1 ≤ R, C, D ≤ 100), representing the RAM, CPU, and Disk requirements for each machine.
  - The second line contains three integers `NR`, `NC`, `ND` (1 ≤ NR, NC, ND ≤ 100), representing the maximum capacities of RAM, CPU, and Disk units in the cluster.

### Output
- For each test case, print a single integer representing the maximum number of machines that Sayed can have in his cluster given the requirements.

### Example
#### Input
2
2 5 3
11 14 6
6 1 2
25 1 15

#### Output
2
1
### Solution
Calculate how many machines can be constructed using each (RAM, CPU, and Disk units).
for RAM the machines will be NR / R.
for CPU the machines will be NC / C.
for Disk units, the machines will be ND / D.
The answer will be a minimum of (NR / R, NC / C, ND / D).

```cpp
#include <iostream>
#include <algorithm>
using namespace std;

int main() {
    int T;
    cin >> T;
    while (T--) {
        int r, c, d;
        int nR, nC, nD;
        cin >> r >> c >> d >> nR >> nC >> nD;
        int ans = min(nR / r, min(nC / c, nD / d));
        cout << ans << endl;
    }
    return 0;
}
```cpp

## Problem Description

After solving the easy version, Sayed was able to find the maximum number of machines he can have based on the requirements and the cluster capacity. However, the numbers are not satisfactory. Sayed received approval from management to purchase extra RAM, CPU, and Disk resources to increase the number of machines.

Given the requirements for a machine, the current cluster capacity, the prices of RAM, CPU, and Disk units, and a total budget, help Sayed determine the maximum number of machines he can run in his cluster using the new budget.

## Input

- The first line of input contains an integer `T` (1 ≤ T ≤ 30), representing the number of test cases.
- Each test case consists of four lines:
  - The first line contains 3 integers `R`, `C`, `D` representing the requirements needed by each machine to run for RAM, CPU, and Disk units respectively, where (1 ≤ R, C, D ≤ 100).
  - The second line contains 3 integers `NR`, `NC`, `ND` representing the maximum capacity for RAM, CPU, and Disk units available in the cluster respectively, where (1 ≤ NR, NC, ND ≤ 100).
  - The third line contains 3 integers `PR`, `PC`, `PD` representing the price of a single RAM, CPU, or Disk unit respectively, where (1 ≤ PR, PC, PD ≤ 100).
  - The fourth line contains a single integer `N` representing the budget that Sayed has to buy extra resources, where (1 ≤ N ≤ 10^9).

## Output

For each test case, print a single integer representing the maximum number of machines that Sayed can have in his cluster given the requirements and the budget he has.

## Example

### Input
2
2 5 3
11 14 6
2 2 5
70
6 1 2
25 1 15
2 2 2
1

### Output
5
1

## Solution

As an easy version, calculate how many machines can be built using the current cluster capacity. 
After that, there might be some units of (RAM, CPU, and Disk space), it is optimal to use these units before paying for new ones, so while you have a capacity in the cluster calculate the remaining units needed to build it if you can afford it, otherwise break the loop (constraints are low 1 ≤ NR, NC, ND ≤ 100, so you will loop 100 times in the worst case, binary search can be used instead if the constraints were up to 1e9 or 1e18).
Finally, if there are still coins remaining with you, calculate how many machines you can afford (N / (R * PR + C * PC + D * PD)).

```cpp
long long r, c, d;
long long nR, nC, nD;
long long pR, pC, pD;
long long coins;
cin >> r >> c >> d >> nR >> nC >> nD >> pR >> pC >> pD >> coins;
long long ans = min(nR / r, min(nC / c, nD / d));
nR -= r * ans;
nC -= c * ans;
nD -= d * ans;
cout << ans << endl;
while (nR || nC || nD) {
    long long need = (r - min(nR, r)) * pR + (c - min(nC, c)) * pC + (d - min(nD, d)) * pD;
    if (need > coins)
        break;
    nR -= min(nR, r);
    nC -= min(nC, c);
    nD -= min(nD, d);
    coins -= need;
    ans++;
}
ans += coins / (r * pR + c * pC + d * pD);
cout << ans << endl;
