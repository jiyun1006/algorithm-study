1. compare 기반 sorting은 최대 성능이 O(NlogN)이다.
2. key index를 기반으로 하는 radix sort가 사용 가능한 경우 최대의 성능을 뽑을 수 있다.
3. O(N+R) time안에 가능하다. N array 길이 R 키 index의 범위




```c++


int main()
{
	vector<pair<string, int>> r;
	r.push_back({ "Anderson", 2 });
	r.push_back({ "Brown", 3 });
	r.push_back({ "Davies", 3 });
	r.push_back({ "Garcia", 4 });
	r.push_back({ "Harris", 1 });
	r.push_back({ "Jackson", 3 });
	r.push_back({ "Jonhson", 4 });
	r.push_back({ "Jones", 3 });
	r.push_back({ "Martin", 1 });
	r.push_back({ "Martinez", 2 });
	r.push_back({ "Miller", 2 });
	r.push_back({ "Moore", 1 });
	r.push_back({ "Robinson", 2 });
	r.push_back({ "Smith", 4 });
	r.push_back({ "Taylor", 3 });
	r.push_back({ "Thomas", 4 });
	r.push_back({ "Thompson", 4 });
	r.push_back({ "White", 2 });
	r.push_back({ "Wilson", 4 });
	r.push_back({ "Williamson", 3 });

	int val = max_element(r.begin(), r.end(), [](auto e, auto k) {return e.second < k.second; })->second; // 최대 index 값
	cout << val << endl;
	int len = r.size();

	vector<pair<string, int>> res(len); // 값과 key index
	vector<int> cnt(val + 2); // 맨 처음 맨 끝 여유분으로 원래 범위에 2개를 더 추가해야함.

	for (auto i : r)
		cout << i.first << " " << i.second << endl;



	for (auto i : r)
		cnt[i.second + 1]++;
	for (int i = 0; i < val; i++)
		cnt[i + 1] += cnt[i]; // index 누적 누적 값을 경계로 그 개수만 갖는걸 파악이 가능하다.

	for (int i = 0; i < len; i++)
		res[cnt[r[i].second]++] = r[i];
	cout << "hi" << endl;
	for (int i = 0; i < len; i++)
		r[i] = res[i];

	for (auto i : r)
		cout << i.first << " " << i.second << endl;



}



```
