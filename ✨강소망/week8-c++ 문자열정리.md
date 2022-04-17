# C++ 문자열 정리

Tags: string

## stringstream

- 주어진 문자열에서 필요한 자료형에 맞는 정보를 꺼낼 때 사용

```cpp
#include <sstream> //header for stringstream

int num; 
string str = "123 456"; 
stringstream stream; 
stream.str(str); //현재 stream의 값을 문자열 str로 바꿈
while(stream >> num ) cout << num << endl;
stream.str("");//초기화
```

<aside>
💻 **출력**

123

456

</aside>

## getline

1. **cin.getline()**

```cpp
char test[10];

cin.getline(test,10);
cout << test << endl;
```

⇒ char형을 다룰 때 사용

이때, **마지막 칸은 '\n**'을 위해 남겨둔다.

예를들어 0,1,2,3,4,5,6,7,8,9를 입력했다면 0부터 8까지만 저장이 되고 마지막 test[9]에는 '\n'이 들어간다.

1. **getline()**
- cin.getline(cin, 문자열 변수);
    
    → 개행문자를 만나면 입력 중단
    
- cin.getline(cin, 문자열 변수, '문자');
    
    → ‘문자’를 만나면 입력 중단
    

```cpp
string str;
string str2;
getline(cin, str);
getline(cin,str2,'#');

cout<<str+str2;
```

ex)

입력 1 : Hi my name

입력 2 : is # somang

출력 : Hi my nameis

## substr

- string형 문자열 부분 문자열 추출, substr()

```cpp
string str = "A time for every purpose.";
 
cout << str.substr() << endl; //문자열 전체 추출
cout << str.substr(7) << endl; //index 7부터 추출
cout << str.substr(2, 4) << endl; //index 2 원소부터 4개 추출
cout << str.substr(str.find('f')) << endl; //f를 찾은 부분부터 추출
```

<aside>
💻 **출력**

A time for every purpose.
for every purpose.
time
for every purpose.

</aside>

Reference

[https://knowable.tistory.com/24](https://knowable.tistory.com/24)

[https://giantpark197cm.tistory.com/142](https://giantpark197cm.tistory.com/142)