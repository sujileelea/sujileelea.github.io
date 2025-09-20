### 매개변수가 없는 함수 (Functions without Parameters)

함수는 기본적으로 매개변수 정의를 요구하지 않는다. 인자를 받지 않아도 동작할 수 있음.
```swift
func sayHelloWorld() -> String {
	return "hello, world"
}

print(sayHelloWorld())
```

### 반환값이 없는 함수 (Functions without Return Values)

반환값은 Void(빈 튜플)
```swift
func greet(person: Sring) {
	print("Welcome, \(person)!")
}

greet(person: "Lea")
```

### 옵셔널 튜플 반환 타입 (Optional Tuple Return Types)

함수에서 반환되는 튜플 타입이 전체 튜플에 대해 '**값이 없을' 가능성**이 있는 경우, **옵셔널 튜플** 반환 타입을 사용해 전체 튜플이 `nil` 일 수 있다는 사실을 반영할 수 있음.
```swift
fucn minMax(array: [Int]) -> (min: Int, max: Int)? {
	if array.isEmpty { return nil }
	var currentMin = array[0]
	var currentMax = array[0]
	for value in array[1..<array.count] {
		if value < currentMin {
			currentMin = value
		} else if value > currentMax {
			currentMax = value	
		}
	}
	return (currentMin, currentMax)
}
```
옵셔널 바인딩을 통해 `minMax(array:)` 함수가 실제 튜플 값을 반환하는지, `nil`을 반환하는지 확인 할 수 있다.
```swift
if lt bounds = minMax(array: [1, 2, 3, 4, 5]) {
	print("min is \(bounds.min) and max is \(bound.max)")
}
```

### 임시적 반환을 가진 함수 (Functions with an Implicit Return)
함수의 전체 본문이 **한 줄**로 표현되면, 함수는 해당 표현식을 암시적으로 반환한다. 아래 두 함수는 같은 동작을 함.
```swift
func greeting(for person: String) -> String {
	"Hello, \(person)"	
}

func anotherGreeting(for person: String) -> String {
	"Hello, \(person)"
}
```

### 인자 레이블 지정 (Specifying Argument Labels)
매개변수 이름 앞에 인자 레이블을 작성한다. 함수를 마치 문장처럼 표현력 있게 호출할 수 있고, 동시에 함수 본문은 읽기 쉽고 의도를 명확히 유지한다.
```swift
func someFuntion(argumentLabel parameterName: Int) {

}

func greet(person: String, from hometown: String) -> String {
	return "Hello \(person). Glad you coult visit from \(hometown)"
}

print(greet(person: "Lea", from: "Misa"))
```

### 인자 레이블 생략 (Omitting Argument Labels)
매개변수에 인자 레이블을 원치 않으면 명시적으로 인자 레이블 대신에 언더바 `(_)`를 작성.
```swift
func someFuntion(_ firstParameterName: Int, secondParameterName: Int) {
	//body
}

someFunction(1, secondParameterName: 2)
```

### 매개변수 기본값 (Default Prarameter Values)
기본값이 정의되어 있다면 함수 호출 시 매개변수를 생략할 수 있다. 기본값이 있는 매개변수는 함수 매개변수 목록의 뒤 쪽에 배치(중요도가 상대적으로 떨어지기 때문)
```swift
func somFunction(firstParameter: Int, secondParameter: Int = 1206) {
	//body
}

someFunction(firstParameter: 1994) //secondParameter is 1206
```

### 함수 타입 (Funtion Types)
함수의 매개변수 타입과 바환 타입이 곧 함수의 타입을 정의한다.
```swift
func addTwoInts(_a: Int, _b: Int) -> Int {
	return a + b
}

func multiplyTwoInts(_ a:Int, _ b:Int) -> Int {
	return a * b
}

var matchFuntion: (Int, Int) -> Int = addTwoInts
print("resutlt : \(matchFuntion(3, 4))")
//result : 7

matchFunction = multiplyTwoInts
print("result : \(matchFunction(3, 4))")
//result : 12
```
swfit가 함수 타입을 추론하도록 맡길 수도 있다.
```swift
let anotherMatchFunction = addTwoInts
```

### 매개변수 타입으로의 함수 타입 (Function Types as Parameter Types)

`(Int, Int) -> Int`와 같은 함수 타입을 다른 함수의 매개변수로 사용할 수 있다. 이렇게 하면 함수의 일부를 호출하는 함수 쪽에서 구현할 수도 있음
```swift
func printMathResult(_ matchFuntion: (Int, Int) -> Int, _ a: Int, _ b: Int) {
	print("result : \(matchFunction(a, b)))
}

printMathResult(addTwoInts, 3, 4)
//result : 7
```
위 예시는 3개의 매개변수를 가지는 `printMathResult(_:_:_:)`라는 함수를 정의한다. 첫번째 매개변수인 함수의 구현 내용은 중요하지 않으며, 중요한 것은 오직 함수가 올바른 타입을 가지는지 아닌지임. 이렇게 하면 `printMathResult(_:_:_:)`는 타입 안전성을 유짛하면서 자신의 일부 기능을 함수 호출자에게 넘길 수 있다.


### 반환 타입으로써의 함수 타입 (Function Types as Return Types)

함수의 반환 타입으로 다른 함수 타입을 사용할 수 있다. 
```swift
func stepFoward(_ input: Int) -> Int {
	return input + 1
}

func stepBackward(_ intput: Int) -> Int {
	return input - 1
}

//반환 타입이 (Int) -> Int인 함수
func chooseStepFunction(backward: Bool) -> (Int) -> Int {
	return backward ? stepBackward : stepFoward
}

var currentValue = 3
let moveNearerToZero = chooseStepFuntion(backward: currentValue > 0)

while currentValue != 0 {
	print("\(currentValue)")
	currentValue = moveNearerToZero(currentValue)
}
print("zero!")
// 3
// 2
// 1
// zero!
```

### 중첩 함수 (Nested Functions)
이 챕터에서 접한 모든 함수는 전역 범위에서 정의된 **전역 함수(global functions)** 의 예시였다. 함수 내부에도 함수를 정의할 수 있고, 이를 중첩 **함수(nested fucntions)** 라고 함.
```swift
func choosStepFunction(backward: Bool) -> (Int) -> Int {
	func stepFoward(input: Int) -> Int { return input + 1}
	func stepBackward(intput: Int) -> Int { return input - 1}
	return backward ? stepBackward : stepFoward
}

var currentValue = -4
let moveNearerToZero = chooseStepFunction(backward: currentValue > 0)
while currentValue != 0 {
	print("\(currentValue)")
	currentValue = moveNearerToZero(currentValue)
}
print("zero!")
// -4
// -3
// -2
// -1
// 0
```


