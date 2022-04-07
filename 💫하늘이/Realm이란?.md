# Realm

> 모바일에 특화된 오픈소스 객체 데이터베이스 관리 시스템

> 모바일용으로 제작되었으며 가볍고, 메모리, 디스크 공간 및 배터리 수명을 효율적으로 사용합니다.

##### 홈페이지에 보면 Java, Swift, .NET, Node.js, React Native, Kotlin, Web, Flutter 등 다양하게 지원하는 것을 알 수 있습니다.

<br>

### Realm 특징

1. Realm은 `NoSQL` 입니다.
<details> 
<summary> NoSQL </summary>
<div markdown="1">
- Not Only SQL 의 약자로 데이터베이스 관리시스템을 지칭합니다.
- 여러 유형의 DB를 사용합니다.
- SQL 외에 데이터를 저장하는 방식이 있습니다.
</div>
</details>

2. Realm은 `객체 중심 데이터베이스` 입니다.
    
    → ORM 이 필요하지 않고 개발자에게 직관적입니다.
    
3. iOS와 Android 간 DB 공유가 가능합니다.
   
4. `코드로 작업`할 수 있습니다.

    → SQL과 같은 중간 쿼리 언어를 사용하지 않습니다.
   
5. `메인 스레드`에서 읽기/ 쓰기를 할 수 있습니다.
    
    → 다중 쓰레드에서의 Realm 객체 관리가 어렵습니다. (쓰레드별 객체 관리 필요함)
    
6. 객체를 `직접 디스크에 유지`합니다.  
    
    → 서드파티 스토리지 엔진을 사용하지 않습니다.  
    → 디스크에서 데이터를 읽거나 쓸 때 데이터를 상호 변환하지 않아도 됩니다.
   
7. SQLite와 CoreData보다 `작업 속도가 빠릅니다.`
   
8. 다양한 쿼리를 지원하지 않습니다.
   
9.  iOS 8 이상부터 사용이 가능합니다.

<br><br>

## 객체 선언

```swift
import Foundation
import RealmSwift

class Dog: Object {
	@Persisted var name: String
	@Persisted var age: Int
}

class Person: Object {
	@Persisted(primaryKey: true) var _id: String
	@Persisted var name: String
  @Persisted var age: Int

  @Persisted var dogs: List<Dog>
}
```

<br>

## Create

```swift
import UIKit
import RealmSwift

class ViewController: UIViewController {
    
	let realm = try! Realm()

	let dog = Dog()
	dog.name = "MAX"

	try! realm.write {
		realm.add(dog)
	}
}
```

<br>

## Read

```swift
realm.objects(Dog.self)  // 반환값: Results<Repository>
```

<br>

## Update

```swift
try! realm.write {
	dog.name = "Wolfie"
}
```

<br>

## listener & observe object notifications

```swift
token = dog.observe { change in
    switch change {
    case .change(let properties):
        for property in properties {
            print("Property '\(property.name)' changed to '\(property.newValue!)'");
        }
    case .error(let error):
        print("An error occurred: (error)")
    case .deleted:
        print("The object was deleted.")
    }
}
```

<br>

## 자동 갱신되는 객체와 쿼리

```
let puppies = realm.objects(Dog).filter("age < 2")
puppies.count // => 아직 개가 Realm에 추가되지 않았기 때문에 0

let myDog = Dog()
myDog.name = "Rex"
myDog.age = 1

try! realm.write {
    realm.add(myDog)
}

puppies.count // => 실시간으로 1로 갱신됩니다.

// 다른 질의에서 개에 접근합니다
let puppy = realm.objects(Dog).filter("age == 1").first
try! realm.write {
    puppy.age = 3
}

// 원래 개 객체는 자동 갱신됩니다.
myDog.age // => 3
puppies.count // => 0
```

<br><br>

#### 참고

[Realm 스레드 깊게 들여보기](https://academy.realm.io/kr/posts/threading-deep-dive/)