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
Calculate how many machines can be constructed using each resource (RAM, CPU, and Disk units). The maximum number of machines is determined by the most limiting resource:

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


