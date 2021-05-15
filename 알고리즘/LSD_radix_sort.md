# LSD Radix Sort
1. counting sort 알고리즘을 이용한다.
2. 정수의 경우 최대 값의 길이를 구한후 길이를 padding 후 counting sort를 한다.
3. 최대 길이를 d라고 했을때 Time Complexity는 O(d*N) N은 배열의 길이
4. Space Complexity는 O(N)


```c++

#include <vector>
#include <string>
#include <regex>
#include <iostream>
#include <sstream>
#include <algorithm>
#include <numeric>
#include <cmath>
#include <map>

using namespace std;

void radix_sort(vector<int>& arr)
{
	int len = arr.size();
	int maxval = 0;
	// 가장 큰 value를 찾는다.
	if (len != 0)
		for (auto i : arr)
			maxval = max(i, maxval);

	// 가장 큰 value가 몇자리인지 찾기
	int digits = 0;
	while (maxval > 0)
	{
		digits++;
		maxval /= 10;
	}

	// 가장 큰 자리수에 맞게 padding하기

	for (int i = 0; i < digits; i++)
	{
		int power = pow(10, i);

		vector<int> new_arr(len); // update할 array

		// counting sort를 위한 array
		vector<int> counting(10); // 0~9 digits

		// Calculate frequency 
		
		for (int j = 0; j < len; j++)
		{
			int num = (arr[j] / power) % 10;

			counting[num]++;
		}

		// frequency 누적합
		for (int j = 1; j < 10; j++)
			counting[j] += counting[j-1];

		for (int j = len - 1; j >= 0; j--)
		{
			int num = (arr[j] / power) % 10;

			new_arr[counting[num] - 1] = arr[j];
			counting[num]--;
		}

		for (int j = 0; j < len; j++)
			arr[j] = new_arr[j]; // copy to original
	}


}

int main()
{

	vector<int> arr = { 15,120,53,36,167,81,75,32,9,60 };

	cout << "원본 배열\n";
	for (auto i : arr)
		cout << i << " ";
	cout << endl;

	radix_sort(arr);

	cout << "After Radix sort\n";
	for (auto i : arr)
		cout << i << " ";
	cout << endl;



}


```


```
원본 배열
15 120 53 36 167 81 75 32 9 60
After Radix sort
9 15 32 36 53 60 75 81 120 167

```
