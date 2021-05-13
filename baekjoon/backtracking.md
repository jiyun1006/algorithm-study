# 백준 백트래킹문제

1. 음수도 포함이라 일반적 방식이 아님.



```c++
#include <vector>
#include <string>
#include <regex>
#include <iostream>
#include <sstream>
#include <cmath>
#include <map>

using namespace std;

void subset(vector<int>& arr, int i, int sum, int n, int target, int& cnt)
{
    sum+=arr[i];
    
    if(i>=n)
        return;
    if(sum==target)
        cnt++;
    
    subset(arr, i+1, sum-arr[i], n, target, cnt);
    subset(arr, i+1, sum, n, target, cnt);
}

int main()
{
    int n, target;
    cin >> n >> target;
    vector<int> arr(n+1);
    vector<int> temp_arr(n);
    int total = 0;
    for (int i = 0; i < n; i++)
    {
        cin >> arr[i];
        total += arr[i];
    }

    int cnts = 0;
    subset(arr, 0, 0, n, target, cnts);

    cout << cnts;
}
```
