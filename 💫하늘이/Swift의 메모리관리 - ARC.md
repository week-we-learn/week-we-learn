# ARC (Automatic Reference Counting)

### 값 형식 (value type) 과 참조 형식 (reference type)

| | value type | reference type |
|-|-           |-               |
| 메모리 저장 위치 | Stack  | Heap |
| 메모리 관리 방식 | 함수가 종료되면 스택프레임과 자동 제거 | RC(Reference Counting)을 통해 메모리를 관리
| 타입 | Int, String, ..., 튜플, 구조체, 열거형, 컬렉션 등 | 클래스, 클로저 |

> reference type은 메모리 관리가 필요하다.

<br>

```
Heap 영역에 할당된 데이터가 해제되지 않으면 메모리 누수 (Memory Leak) 현상이 발생한다.
왜? 쓰지 않는 데이터가 메모리 공간을 차지하고 있기 때문에 
```

<br>

### 그래서 언어마다 메모리 관리방법이 있다.

|Java|Swift|
|-|-|
|GC (Garbage Collector) | ARC (Automatic RC) |
|런타임에 메모리를 감시하는 기법| 자동으로 Reference를 카운팅 해주는 기법|

<br>

![](/💫하늘이/img/arc.jpeg)

<br>

자신을 참조하고 있는 갯수를 세어 갯수가 0 이되면 메모리에서 사라진다.