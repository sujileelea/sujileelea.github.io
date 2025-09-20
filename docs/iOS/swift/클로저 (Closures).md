> 코드에서 전달되고 사용할 수 있는 독립적인 기능 블록

클로저는 정의된 컨텐스트에서 상수나 변수에 대한 참조를 캡처라고 저장할 수 있다. 이걸 클로저가 포착한다(closeing over)라고 표현함. swift는 캡처에 대한 메모리 관리르 자동으로 처리한다.

- 전역 함수 : 이름을 가지고 어떠한 값도 캡처하지 않는 클로저
- 중첩 함수 : 이름을 가지고 외부 함수로부터 값을 캡처할 수 있는 클로저

보통 클로저는 이름이 없다.

## 클로저 표현식

간단한 구문으로 인라인 클로저를 작성하는 방법

### 정렬 메서드 (Tehe Sorted Method)
```swift
let names = ["Lea", "Suji", "adroa bodin]

func backward(_ s1: String,  _ s2: String) -> Bool {
	return s1 > s
}
```