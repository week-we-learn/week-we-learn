## 소프트웨어 디자인패턴

### 소프트웨어 개발 방법
과거의 소프트웨어 개발 과정에서 발견된 설계의 노하우를 축적하여 그 방법에 이름을 붙여서 이후에 재사용하기 좋은 형태로 특정 규약을 만들어서 정리한 것

"효율적인 코드를 만들기 위한 방법론 (구조)"

<br>

## Delegate 패턴
In software engineering, the delegation pattern is an ***object-oriented design pattern*** that allows object composition to achieve the same code reuse as inheritance.

Delegate 패턴은 객체 구성이 상속과 동일한 코드 재사용을 달성할 수 있도록 하는 **객체지향 디자인 패턴**입니다.

<br>

## 예시로 알아보는 Delegate 패턴

#### Swift 예시)

**파티를 준비하기 위해서 할 일**
```
protocol PrepareParty: class {
  func prepareFood()
  func prepareSong()
}
```

**파티 준비자**
```
class PartyDirector {
  weak var delegate: PrepareParty?

  func order() {
    self.delegate?.prepareFood()
    self.delegate?.prepareSong()
  }
}
```

```
class FirstPartyWorker: PrepareParty {
  init(director: PartyDirector) {
    direct.delegate = self
  }

  func prepareFood() {
    print("첫번째 파티준비자는 피자를 준비합니다.")
  }

  func prepareSong() {
    print("첫번째 파티준비자는 BTS 노래를 준비합니다.")
  }
}


class SecondPartyWorker: PrepareParty {
  init(director: PartyDirector) {
    direct.delegate = self
  }

  func prepareFood() {
    print("두번째 파티준비자는 치킨을 준비합니다.")
  }

  func prepareSong() {
    print("두번째 파티준비자는 오마이걸 노래를 준비합니다.")
  }
}
```


#### Java 예시)

**[Delegate 패턴을 사용하지 않았을 때]**
```
public class Worker {
    private String name;

    Person(String name) {
        this.name = name;
    }

    void 본업() {
        수없이 많은일~~~~~
        수없이 많은일~~~~~
        수없이 많은일~~~~~
        수없이 많은일~~~~~
        수없이 많은일~~~~~
        수없이 많은일~~~~~
        수없이 많은일~~~~~
        수없이 많은일~~~~~
    }

    void 전세 대출() {
        대출되는 은행 탐방~~
        ...
    };
    void 부동산 돌기() {
        부동산 10곳 찾기
        ...
    };
    void 계약 하기() {
        계약서 꼼꼼히 검토
        ...
    };
}
```

<br>

**[Delegate 선언 - 인터페이스]**
```
public interface RoomGetter {
    void 전세 대출();
    void 부동산 돌기();
    void 계약하기();
}
```

**[코드에 Delegate 변수 생성]**
```
public class Worker {
    private String name;
    private RoomGetter delegate;

    Person(String name) {
        this.name = name;
    }

    void 본업() {
        수없이 많은일~~~~~
        수없이 많은일~~~~~
        수없이 많은일~~~~~
        수없이 많은일~~~~~
        수없이 많은일~~~~~
        수없이 많은일~~~~~
        수없이 많은일~~~~~
        수없이 많은일~~~~~
    }

    void 방 계약() {
        delegate.전세 대출();
        delegate.부동산 돌기();
        delegate.계약하기();
    }
}
```


**[Delegate 타입을 구현하는 클래스]**
```
public class FirstRoomGetter implements RoomGetter {
    FirstRoomGetter(Worker: worker) {
        worker.delegate = this;
    }

    void 전세 대출() {
        대출되는 은행 탐방~~
        ...
    };
    void 부동산 돌기() {
        부동산 10곳 찾기
        ...
    };
    void 계약 하기() {
        계약서 꼼꼼히 검토
        ...
    };
}
```

  
#### 참조
[velog](https://velog.io/@zooneon/Delegate-%ED%8C%A8%ED%84%B4%EC%9D%B4%EB%9E%80-%EB%AC%B4%EC%97%87%EC%9D%BC%EA%B9%8C)  
[tistory](https://week-year.tistory.com/219)  
[tistory](https://wiserloner.tistory.com/461)  
[wiki](https://en.wikipedia.org/wiki/Delegation_pattern)
