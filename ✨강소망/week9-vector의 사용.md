# C++ 다양한 함수

**vector의 최대값,최소값**

- max_element()
- min_element()

```cpp
#include <algorithm>
#include <vector>

vector<int> v;
int max = *max_element(v.begin(), v.end()); //최대값
int idx_max = max_element(v.begin(),v.end())-v.begin();

int min = *min_element(v.begin(), v.end()); //최소값
int idx_min = min_element(v.begin(),v.end())-v.begin();
```

[https://notepad96.tistory.com/entry/C-Vector-최대값-최소값-인덱스-구하기](https://notepad96.tistory.com/entry/C-Vector-%EC%B5%9C%EB%8C%80%EA%B0%92-%EC%B5%9C%EC%86%8C%EA%B0%92-%EC%9D%B8%EB%8D%B1%EC%8A%A4-%EA%B5%AC%ED%95%98%EA%B8%B0)

**해결못한질문**

```cpp
vector<int> v1;
vector<int> v2;

v1.push_back(1);
v1.push_back(2);

v2.push_back(1);
v2.push_back(2);
v2.push_back(3);

for(int i = 0;i<v2.size();i++){
	if(v1[i]==v2[i]){
		cout<<v1[i];
	}
}
```

과연 결과는?