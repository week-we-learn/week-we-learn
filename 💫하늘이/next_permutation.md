# next permutaion
###### C++의 algorithm STL에는 next_permutation, prev_permutation이 존재한다.
### Permutation 순열
1 2 3 4 -> 첫순열 (사전순으로 나열했을 때 첫번째)  
1 2 4 3  
1 3 2 4  
1 3 4 2  
1 4 2 3  
1 4 3 2  

...  

4 3 2 1 -> 끝순열 (사전순으로 나열했을 때 마지막)

<br>

<details> 
<summary> 1 2 3 4 5 6 7 의 다음 순열은? </summary>
<div markdown="1">
1 2 3 4 5 7 6
</div>
</details>
<br>
<details> 
<summary> 2 3 1 7 6 5 4 의 다음 순열은? </summary>
<div markdown="1">
2 3 4 1 5 6 7
</div>
</details>
<br>
<details> 
<summary> 1 6 7 4 5 3 2 의 다음 순열은? </summary>
<div markdown="1">
1 6 7 5 2 3 4
</div>
</details>
<br>

#### 규칙성

1 2 3 4 5 6 <u>7</u>  
1 2 3 4 5 <u>7</u> **6**

<br>

2 3 <u>1</u> **7 6 5 4**  
2 3 <u>4</u> **1 5 6 7**

- 1을 기준으로 7 6 5 4 내림차순
- 4를 기준으로 1 5 6 7 오름차순

<br>

1 6 7 <u>4</u> **5 3 2**  
1 6 7 <u>5</u> **2 3 4**

- 4를 기준으로 5 3 2 내림차순
- 5를 기준으로 2 3 4 오름차순

#### => 배열을 A라고 했을 때 A[i-1] < A[i]로 바뀌는 지점이 기준이 된다.

<br>

## 순서
<br>

#### 1. A[i-1] < A[i]로 바뀌는 지점 중 가장 큰 수를 찾는다.
> 왜? 사전순은 뒤에서부터 변화시키니까 

|2|3|7|6|5|4|
|-|-|-|-|-|-|
| |i-1|i| | | |

###### 시간복잡도: O(N)

#### 2. A[i-1]를 기준으로 오른쪽에서 A[i-1]보단 큰 가장 작은 수 A[j]를 찾는다.
> 왜? 다음에 그 숫자를 앞으로 땡겨야 하니까
 
|2|3|7|6|5|4|
|-|-|-|-|-|-|
| |i-1|i| | |j|

###### 시간복잡도: O(N)

#### 3. A[i-1]과 A[j]를 swap 한다.

|2|4|7|6|5|3|
|-|-|-|-|-|-|
| |j|i| | |i-1|

###### 시간복잡도: O(1)

#### 4. 바뀐 숫자를 기준으로 오른쪽을 오름차순으로 정렬한다. (= 뒤집는다)
> 다음 조합이 나왔다!

|2|4|3|5|6|7|
|-|-|-|-|-|-|

###### 시간복잡도: O(N)

### 시간복잡도 : *O(N)*

### 비교 (다음 순열을 구할 때)
|재귀|next_permutation|
|-|-|
|O(2^n)|O(n)|


<br><br><br>

#### 알고리즘 문제 추천
[백준 9081 단어 맞추기 실버1](https://www.acmicpc.net/problem/9081)  
[LeetCode 31. Next Permutation](https://leetcode.com/problems/next-permutation/)

<br>

#### 코드
<details> 
<summary> JAVA </summary>
<div markdown="1">

```
public void nextPermutation(int[] A) {
    if(A == null || A.length <= 1) return;
    int i = A.length - 2;
    while(i >= 0 && A[i] >= A[i + 1]) i--; // Find 1st id i that breaks descending order
    if(i >= 0) {                           // If not entirely descending
        int j = A.length - 1;              // Start from the end
        while(A[j] <= A[i]) j--;           // Find rightmost first larger id j
        swap(A, i, j);                     // Switch i and j
    }
    reverse(A, i + 1, A.length - 1);       // Reverse the descending sequence
}

public void swap(int[] A, int i, int j) {
    int tmp = A[i];
    A[i] = A[j];
    A[j] = tmp;
}

public void reverse(int[] A, int i, int j) {
    while(i < j) swap(A, i++, j--);
}
```

</div>
</details>

<details> 
<summary> Swift </summary>
<div markdown="1">

```
class Solution {
    func nextPermutation(_ nums: inout [Int]) {
        var l = -1, i = nums.count - 2
        while i >= 0 {
            if nums[i] < nums[i+1] { l = i; break }
            i -= 1
        }
        guard l != -1 else {
            nums = Array(nums.reversed())
            return
        }
        var r = -1
        i = nums.count - 1
        while i > l {
            if nums[i] > nums[l] { r = i; break }
            i -= 1
        }
        nums.swapAt(l, r)
        let arr: [Int] = Array(nums[l+1...nums.count - 1])
        nums.replaceSubrange(l + 1..<nums.count, with: Array(arr).reversed())
    }
}
```

</div>
</details>