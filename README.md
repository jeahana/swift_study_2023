# 핵심만 골라배우는 Swift(2023)

## swift 정보

- swift.org: https://www.swift.org/
- apple swift resources : https://developer.apple.com/kr/swift/resources/
- The Swift Programming Language (영어) : https://docs.swift.org/swift-book/documentation/the-swift-programming-language/
   . 한글번역:  https://bbiguduk.gitbook.io/swift/
- Swift Standard Library: https://developer.apple.com/documentation/swift/swift-standard-library
- Apple 디자인 리소스 : https://developer.apple.com/kr/design/resources/
 . Sample Apps Tutorials :https://developer.apple.com/tutorials/sample-apps
 . Swift UI 샘플 앱 : https://developer.apple.com/tutorials/app-dev-training
 . iOS용 앱 개발하기 (14시간15분) : https://developer.apple.com/tutorials/app-dev-training
 . SwiftUI 소개 (4시간25분) : https://developer.apple.com/tutorials/swiftui
 . Mac Catalyst로 Mac에 iPad앱 구현하기 (3시간25분) : https://developer.apple.com/tutorials/mac-catalyst/

## Chapter 01. 시작하기

1.3 소스코드 : https://bit/ly/jpub_swiftui

## Chapter 02. 애플 개발자 프로그램 가입하기

- 앱 배포를 위해서는 프로그램에 가입해야한다.
- 프로그램에 가입해야 icloud, 앱내결제, apple pay 같은 고급 기능을 사용할 수 있다.
- url: https://developer.apple.com

## Chapter 03. Xcode 14와 iOS 15 SDK 설치하기

1. XCode 실행 후, Account 와 인증서를 생성한다.
- 메뉴 Xcode > Settings > Accounts 에서 Account 추가.
- Accounts 화면에서, 아래에 "Manage Certificates..."에서 개발 인증서 생성한다.
  + 인증서를 생성해야, 디바이스에 앱을 빌드하고 테스트할 수 있다.
- 앱 스토어에 업로드할 준비가 되었다면, 배포 인증서도 생성해야 한다. **배포 인증서는 애플 개발자 프로그램의 멤버십이 필요한다.**

## Chapter 04. Xcode 14 플레이그라운드

- 플레이그라운드는 스위프트 코드를 입력하면 실시간으로 결과가 실행되는 인터랙티프 환경이다.
  + 플레이그라운드는 Xcode 프로젝트를 생성하고 코드를 반복적으로 편집, 컴파일 및 실행할 필요 없이 iOS SDK에 포함된 많은 클래스 및 API를 실험하고 스위프트 프로그래밍 언어를 학습할 수 있게 해준다.
- 메뉴: File > New > Playground
- Markup : https://developer.apple.com/library/archive/documentation/Xcode/Reference/xcode_markup_formatting_ref/index.html

- 단축키
 + live view: alt + cmd + enter
 + run playground: shift + cmd + enter

``` swift
import SwiftUI
import PlaygroundSupport

struct ExampleView: View {
    
    @State private var rotation: Double  = 0
    
    var body: some View {
        VStack {
            Rectangle()
                .fill(Color.blue)
                .frame(width: 200, height: 200)
                .rotationEffect(.degrees(rotation))
                .animation(.linear(duration: 2), value: rotation)            
            Button(action: {
                rotation = (rotation < 360 ? rotation + 60:0)
            }) {
                Text("Rotate")
            }
        }
        .padding(10)
    }
}

PlaygroundPage.current.setLiveView(ExampleView()
    .padding(100))

```

## Chapter 5. 스위프트 데이터 타입, 상수 그리고 변수

``` swift
print("Int32 Min = \(Int32.min) Int32 Max= \(Int32.max)")

var multiline = """
   123
   가나다라
   abc
"""

print(multiline)

// 상수정의는 let 사용. 값을 할당해야 한다.
let maxUserCount = 0

var isSwiftBook = true

// 다만, 상수에 tupe annotation을 사용하면 정의 후 할당이 가능하고, 한 번 할당후에는 변경이 불가함.
let bookTitle: String
if isSwiftBook {
    bookTitle = "Swift UI Book"
} else {
    bookTitle = "Java Book"
}
print(bookTitle)

// type annotation. 상수 이름 뒤에 콜론(:)쓰고 타입을 적는다.
var userCount: Int = 10
print(userCount)

// 튜플. 함수에서 사용하면 반환할 때 여러 값을 반환할 수 있다.
let myTuple = (10, 3.14, "Swift Book")
let myStr = myTuple.2
print(myStr)

// 옵션널 타입
var index: Int?
index = 3
var treeArray = ["Oak", "Pine", "Yew", "Birch"]
if let myValue = index {
    print(treeArray[myValue])
} else {
    print("index does not contain a value")
}

// if-let 구문
if let index {
    print(treeArray[index])
} else {
    print("index does not contain a value")
}
```

## Chapter 6. 스위프트 연산자와 표현식

### 6.7 범위 연산자
``` swift
// 닫힌 범위 연산자(closed range operator)
x...y
5..8 // 5,6,7,8 을 지칭
// 반 개방 범위 연산자(half-open range operator)
x..<y
5..<8 // 5,6,7 지칭, 8 제외
// 단방향 범위 연산자(one-sided range operator)
x...
...y
// 문자열 index 범위를 적용할 때
2...
...6
```

### 6.9 nil 병합 연산자

- nil 병합 연산자(nil coalescing operator(??))를 사용하면 옵셔널에 nil값이 있는 경우 디폴트 값을 사용할 수 있다.
``` swift
let customerName: String? = nil
print("Welcom back, \(costomerName ?? "customer")")
```

## Chapter 7. 스위프트의 제어 흐름 (control flow)

``` swift
// for-in
for index in 1...5 {    

}

// while
var myCount = 0
while myCount < 100 {    
    myCount += 1
}

// repeat...while
var i = 10
repeat {
    i -= 1
} while (i > 0)

// break
var j = 10
for _ in 0..< 100 {
    j += 1
    if j > 100 {
        break
    } else {
        continue
    }
}

// if .. else if ...
let x = 9
if x == 10 {
    
} else if x == 9 {

} else if x == 8 {

}

// guard 구문. validation 체크 같은 기능이 듯. 
// guard 구문이 true 이면 다음 블럭이 실행되고, false 이면 guard else 블록이 실행된다.
// guard else 블록내에 흐름을 빠져나가는 구문을 포함해야한다.(return, break, continue)
func multiplyByTen(value: Int?) {
    guard let number = value, number < 10 else {
        print("Number is too high")
        return
    }
    
    // 일반적으로 if구문 내에서 언래핑된 변수는 if구분 밖에서는 유효하지 않으나,
    // guard 구문에서 언래핑된 number변수는 guard 구문밖에서도 유효하다.!!!
    let result = number * 10
    print(result)
}
```


## Chapter 8. 스위프트의 switch 구문

- 스위프트는 case 조건이 일치하면 자동으로 구문 밖으로 빠져나간다.(break 기본처리된다.)
- fallthrough 구문을 사용하면 swift 구현부에서 예외상황 효과를 주어, 실행 흐름이 그 다음 case 구문으로 진행하게 할 수 있다.
``` swift
let temperature = 24
swift (temperature) {
    case 0 :
        print("zero")
    case 1...20:
        print("Cold")
    case 20...28:
        print("Warm")
    case 29...40:
        print("Hot")
    case 41...50 where temperature % 2 == 0: // where 구문을 활용한 부가적인 조건 추가
        print("So Hot and even")
        fallthrough // 다음 구문으로 진행하도록 fall through 처리한다.
    default:
        print("Temperature out of range")
}
```

## Chapter 9. 스위프트의 함수, 메서드, 클로저

``` swift
// 함수 예제
// name, count 는 함수내의 지역 매개변수이자, 호출할 때 사용하는 외부 매개변수가 된다.
// String은 반환 타입이다.
func buildMessgeFor(name: String, count: Int) -> String {
    return "\(name), you are customer number \(count)"
}

let messge = buildMessageFor(name: "John", count: 100)

// 아래에서 callName, callCount는 외부 매개변수로 재정의한다.
func buildMessgeFor(callName name: String, callCount count: Int) -> String {
    return "\(name), you are customer number \(count)"
}

let messge = buildMessageFor(callName: "John", callCount: 100)

// 외부 매개변수명을 생략한다.
func buildMessgeFor(_ name: String, _ count: Int) -> String {
    return "\(name), you are customer number \(count)"
}

let messge = buildMessageFor("John", 100)

// 디폴트 변수를 선언한다.
func buildMessgeFor(_ name: String = "Customer", count: Int) -> String {
    return "\(name), you are customer number \(count)"
}

let messge = buildMessageFor(count: 100)

// 여러 결과값(튜플) 반환하기
func sizeConverter(_ length: Float) -> (yardd: Float, centimeters: Float, meters: Float) {
    let yard = length * 0.0277778
    let centimeters = length * 2.54
    let meters = length * 0.0254
    return (yards, centimeters, meters)
}

// 가변 매개변수
func displayStrins(_ strings: String...) {
    for string in strings {
        print(string)
    }
}

// 변수인 매개변수
func calcurateArea(length: Float, width: Float) -> Float {
    // 함수의 매개변수는 상수로 값을 변경할 수 없다. 값을 변경하려면 새도우 복사본(shadow copy)을 반드시 생성해야한다.
    var length = length
    var width = width

    length = length * 2.54
    width = width * 2.54
    return length * width
}

// 입출력 매개변수 사용하기
// inout 키워드를 추가하고, 새도우 복사본을 사용하지 않는다.
func doubleValue(_ value: inout Int) -> Int {
    value += value
    return value
}
let myValue = 10
let afterValue = doubleValue(&myValue)
// 외부 변수 myValue가  20 값을 가짐.

// 매개변수인 함수
func inchesToFeet(_ inches: Float) -> Float {
    return inches * 0.0833333
}

func inchesToYards(_ inches: Float) -> Float {
    return inches * 0.0277778
}

let toFeet = inchesToFeet // 함수를 상수에 할당할 수 있다
let toYard = inchesToYards

func outputConversion(_ converterFunc: (Float) -> Float, value: Float) { // (Float) -> Float 함수를 매개변수로 받음. (Float)는 함수 매변변수, 뒤는 반환 타입의 함수라는 의미.
    let result = converterFunc(value)
    print("Result of converstion is \(result)")
}
```
### 9.14 클로저 표현식

- 클로저 표현식은 독립적인 코드 블록이다. 클로저 표현식을 선언하고 그것을 상수에 할당한 다음 상수 참조를 통해 함수를 호출한다.

``` swift
let sayHello = { print("Hello") }
sayHello()

let multiply = {(_ val1: Int, _ var2: Int) -> Int in // 클로저 표현식 코드의 시작을 가르키기 위해서 in 키워드를 사용한다. 사실, 함수는 이름이 있는 클로저 표현식이다.
    return val1 * val2
}
let result = multiply(10, 20)
```

### 9.15 약식 인수 이름

- 매개 변수 이름과 in 키워드를 생략할 수 있게하며, 인수를 $0, $1, $2 등으로 참조할 수 있다.
``` swift
let join = { (string1: String, string2: String) -> String in 
    string1 + string2 // 함수내에서 단일 문장이면 return 을 생략할 수 있다.
}

// 클러저 표현식이 더 이상 인수 또는 반환 유형을 정의하지 않기 때문에 타입 애너테이션((String, String) -> String)이 할당 연산자(=)의 왼쪽으로 이동되었다.
let join : (String, String) -> String = {
    $0 + $1
}
```

### 9.16 스위프트의 클로저

- **클로저(함수)**는 함수나 클로저 표현식과 같은 독립적인 코드블록과 코드 블록 주변에 있는 하나 이상의 변수가 결합된 것을 말한다.
  + **이 함수(클로저)에서 외부에 있는 변수를 가두고 있으며(closed over). 외부 변수를 처리할 수 있다.**

``` swift
func functionA() () -> Int {
    var counter = 0
    func functionB() -> Int {
        return counter + 10
    }
    return functionB
}

let myClosure = functionA() // 함수 functionB()를 반환한다. functionB()를 클로저라 한다. counter 변수를 잡고있다(captured), 또는 가두고 있다(closed over)고 말할 수 있어 클로저로 간주한다.
let resutl = myClosure() // 클로저를 호출한다.
```


## Chapter 10. 스위프트의 객체지향 프로그래밍 기초

### 10.7 클래스 인스턴스 초기화하기와 소멸하기
``` swift
class BankAccount {
    var accountNumber: Int = 0
    var accountBalance: Float = 0

    init(number: Int, balance: Float) {   // 초기화. 생성자로 사용됨
        accountNumber: number
        accountBalance: balance
    }

    deinit {                              // 소멸자(deinitializer)
        // 필요한 정리 작업을 수행한다.
    }

    func displayBalance() {               // 인스턴스 메서드
        print("Number \(accountNumber)")
        print("Current balance is \(accountBalance)")
    }

    class func getMaxBalance() -> Float { // 타입 메서드
        return 100000.00
    }
}

var account1 = BankAccount(number: 12312312, balnce: 123.45)
account1.displayBalance() // 인스턴스 메서더 호출. 인스턴스.메서드()

var maxAllowed = BankAccount.getMaxBalance() // 타입메서드 호출. 클래스.메서드()
```

### 10.9 저장 프로퍼티와 연산 프로퍼티

- 연산 프로퍼티는 게터를 생성하고, 선택적으로 세터 메서드를 생성하며, 연산을 수행할 코드가 포함된다.
``` swift
class BankAccount {
    // 중략
    var balanceLessFees: Float {
        get {
            return accountBalance - fees
        }

        set(newBalance) {
            accountBalance = newBalance - fees
        }
    }
}

var valance1 = account.balanceLessFees
account.balanceLessFees = 123.45
```

### 10.10 지연 저장 프로프터

- 프로프티를 lazy로 선언하면 프로퍼티가 최초로 접근될 때만 초기화된다.
- 지연 프로퍼티는 반드시 변수(var)로 선언되어야 한다.
  
``` swift
class MyClass {
    lazy var myProperty: String = {
        var result = resourceIntensiveTask()
        result = processData(data: result)
        return result
    }()
}
```
### 10.11 스위프트에서 self 사용하기

- 대부분의 경우는 스위프트에서 selft는 선택적으로 사용된다.
- self를 사용해야 하는 상황은 프로프티나 메서드를 클로저 표현식 내에서 참조할 경우다.
``` swift
    document?.opernWithCompletionHandler({(success: Bool) -> Void in 
        if success {
            self.ubiquityURL = resultURL
        }
    })
```

### 10.12 스위프트 프로토콜 이해하기

- 클래스가 충족해야하는 최소한의 요구사항을 정의하는 규칙들의 집합을 프로토콜이라고 한다. (java 인터페이스 같은 역할)
- 프로토콜은 protocol 키워드를 이용하여 선언되며, 클래스가 반드시 포함해야 하는 메서드와 프로퍼티를 정의한다.
- 어떤 클래스가 프로토콜을 채택했으나 모든 프로토콜의 요구사항을 충족하지 않으면 에러가 발생한다.

``` swift
protocol MessageBuilder {
    var name: String {get}
    func buildMessage() -> String    
}

class MyClass: MessageBuilder {
    var name: STring
    init(name: String) {
        self.name = name
    }

    func buildMessage() -> String {
        "Hello " + name
    }
}
```
### 10.13 불투명 반환 타입(opaque return type)

- 특정 반환 타입(구체화된 타입(concrete type))을 지정하는 대신, 불투명 반환 유형을 사용하면 지정된 프로토콜을 따르는 모든 타입이 반환될 수 있게 한다.
- 불투명 반환 타입은 프로토콜 이름 앞에 some 키워드를 붙여 선언된다.
- 
``` swift
func doubleFunc1(value: Int) -> some Equatable {
    value * 2
}
```

## Chapter 11. 스위프트의 서브클래싱과 익스텐션 개요

- 스위프트의 하위 클래스는 반드시 단 한 개의 부모 클래스만 둘 수 있다. (단일 상속(single inheritance))

### 11.4 상속받은 메서드 오버라이딩 하기

- 오버라이딩할 때는 메서드의 1) 매개변수 개수와 타입이 일치하고, 2) 반환 타입이 일치해야 한다. 그리고, override 키워드를 붙인다.
- 하위 클래스에서 오버라이드된 상위 클래스의 메서드를 호출할 수도 있다. (super.메서드())

### 11.5 하위 클래스 초기화 하기

- 초기화 과정에서 발생할 수 있는 잠재적인 문제를 피하기 위해서 상위 클래스의 init 메서드는 항상 하위 클래스의 초기화 작업이 완료된 후에 호출한다.

``` swift
class SavingsAccount: BankAccount {
    var interestRatge : Float
    init(number: Int, balance: Float, rate: Float) {
        initerestRate = rate
        super.init(number: number, balance: balence)
    }
}
```

### 11.7 스위프트 클래스 익스텐션

- 익스텐션은 하위 클래스를 생성하거나 참조하지 않고 기존 클래스에 메서드, 생성자, 연산 프로퍼티, 서브스크립트 등의 기능을 추가하여 사용할 수 있다.

``` swift
extension 클래스명 {
    // 새로운 기능을 여기에 추가한다.
}

extension Double {
    var squared: Double {
        return self * self
    }

    var cubed: Double {
        return self * self * self
    }
}

let myValue: Double = 3.0
print(myValue.squared)
```

## Chapter 12. 스위프트 구조체와 열거형

### 12.2 값 타입 vs. 참조 타입

1. 구조체 인스턴스의 타입은 값 타입이고, 클래스의 인스턴스의 타입은 참조 타입이다.
- 구조체 인스턴스가 복사되거나 메서드에 전달될 때 인스턴스의 실제 복사본이 생성되면서 원본 객체가 가지고 있던 모든 데이터를 그대로 복사해서 갖게 된다.
- 각각의 복사본은 자신만의 데이터를 가질 수 있다. 구조체로 된 인스턴스는 어떤 하나의 인스턴스를 변경해도 다른 복사본에 영향을 미치지 않는다.
```swift
struct SampleStruct {
    var name: String
    init(name: String) {
        self.name = name
    }
}

let myStruct1 = SampleStruct(name: "Mark")
var myStruct2 = myStruct1
myStuct2.name = "David"

print(myStruct1.name) // Mark
print(myStruct2.name) // David
```

2. 구조체 특징
- 상속이나 하위 클래스를 지원하지 않는다.
- 클래스와 다른게 소멸자 메서드(deinit)를 포함할 수 없다.
- 런타임에서 인스턴스의 유형을 식별할 수 없다.
```swift
print(latte is Coffee) // is: 타입 확인 연산자
```

### 12.3 구조체와 클래스는 언제 사용하는가?

- 일반적으로 구조체가 클래스보다 효율적이고 멀티 스레드 코드를 사용하는 데 더 안정적이기 때문에 가능하다면 구조체를 권한다.
- 하지만, 상속이 필요하거나 데이터가 캡슐화된 하나의 인스턴스가 필요할 때는 클래스를 사용해야 한다. (익스텐션 기능은 사용이 가능함.)
- 또는, 인스턴스가 소멸될 때 리소스를 확보하기 위한 작업이 필요할 때도 클래스를 사용해야 한다.

### 12.4 열거형 개요

- 일반적으로 enum이라고 하는 열거형(enumeration)은 미리 정의된 값 집합으로 구성된 사용자 지정 데이터 유형을 만드는 데 사용된다.
- 열거형 내의 개별 케이스에는 연결된 값이 있을 수도 있다.
```swift
enum Temperature {
    case hot
    case warn
    case cold(centigrade: Int)
}

func displayTemp(temp: Temperature) {
    swith temp {
        case .hot:
            print("It is hot.")
        case .warn:
            print("It is warn.")
        case .cold(let centigrade) where centigrade <= 0:
            print("Ice waring: \(centigrade) degrees.")
        case .cold:
            print("It is cold but not freezing.")
    }
}
```

## Chapter 13. 스위프트 프로퍼티 래퍼

- 프로퍼티 래퍼는 클래스와 구조체 구현부에 게터, 세터, 연산 프로퍼티(computed property) 코드의 중복을 줄이는 방법을 제공한다.

```swift
// struct
struct Address {
    private var cityname: String = ""
    var city: String {
        get {cityname}
        set {cityname = newValue.uppercased() }
    }
}

var address = Address()
address.city = "London"
print(address.city) // output: LONDON
```

```swift
// propertyWrapper - example
@propertyWrapper // 1. 선언. propertyWrapper
struct FixCase {
    private(set) var value: String = ""

    var wrappedValue: String {  // 2. wrappedValue 가져야 함.
        get { value }
        set { value = newValue.uppercased() }
    }

    init(wrappedValue initialValue: String) { // 3. 초기값이 전달되는 초기화 메서드. (선택 사항)
        self.wrapedValue = initialValue
    }
}

struct Contact {
    @FixCase var name: String
    @FixCase var city: String
    @FixCase var country: String
}
```

```swift
@propertyWrapper
struct MinMaxVal {
    var value: Int
    let min : Int
    let max: Int

    init(wrappedValue: Int, min: Int, max: Int) {
        value = wrappedValue
        self.min = min
        self.max = max
    }

    var wrappedValue: Int {
        get { value }
        set { 
            if newValue > max {
                value = max
            } else if newValue < min {
                value = min
            } else {
                value = newValue 
            }
        }
    }
}

struct Demo {
    @MinMaxVal(min: 100, max: 200) var value: Int = 100
}

var demo = Demo()
demo.value = 250
print(demo.value)
```

```swift
// using comparable protocal for any Type(String, Charater, Int, Date, DateInterval, ... etc)
@propertyWrapper
struct MinMaxVal<V: Comparable> {
    var value: V
    let min : V
    let max: V

    init(wrappedValue: V, min: V, max: V) {
        value = wrappedValue
        self.min = min
        self.max = max
    }

    var wrappedValue: V {
        get { value }
        set { 
            if newValue > max {
                value = max
            } else if newValue < min {
                value = min
            } else {
                value = newValue 
            }
        }
    }
}

```

## Chapter 14. 스위프트의 배열과 딕셔너리 컬렉션으로 작업하기

- 스위프트에서의 컬렉션은 가변형(mutable)과 불변형(immutable)이 있다.
- 불편형 컬렉션을 만들고 싶다면 컬렉션을 생성할 때 상수에 할당한다. 반면, 변수에 할당했다면 가변형이 된다.
```swift
let treeArray = ["Pine", "Oak", "Yew"] // immatable
var treeArray1 = ["Pine", "Oak", "Yew"] // matable
var treeArray2: [String] = ["Pine", "Oak", "Yew"] // matable
var treeArray3: [String]() // 빈배열
var nameArray = [String](repeating: "My String", count: 10) // 10개항목을 "My String"으로 초기화된 배열 생성

let firstArray = ["Red", "Green", "Blue"]
let secondArray = ["Indigo", "Violet"]
let mergeArray = firstArray + secondArray
```

```swift
// 섞기
let shuffedTrees = treeArray.shuffled()
// 무작위로 가져오기
let randomTree = treeArray.randomElement()

// 항목추가(append)
treeArray.append("Redwood")
treeArray += ["Redwood"]
treeArray += ["Redwood", "Maple", "Birch"]

// insert
treeArray.insert("Maple", at: 0)

// remove
treeArray.remove(at: 2)

// remove at Last
treeArray.removeLast()
```

```swift
// 배열 반복하기
let treeArray = ["Pine", "Oak", "Yew", "Maple", "Birch", "Myrtle"]
for tree in treeArray {
    print(tree)
}

treeArray.forEach { tree in
    print(tree)
}

treeArray.forEach {
    print($0)
}
```

### 14.4 타입이 혼한된 배열 생성하기

- 스위프트의 Any는 특별한 타입으로, 지정된 클래스 타입이 아닌 객체를 참조하는 데 사용된다. 따라서 Any 객체 타입 배열은 여러 타입의 항목을 담을 수 있다.
```swift
let mixedArray: [Any] = ["A String", 432, 3.14]

for object in mixedArray {
    print(object as! Int * 10) // downcast 처리하면, 컴파일 오류는 잡히지만* 연산에서 String 경우는 Runtime 오류가 발생한다.
}
```

### 14.5 스위프트 딕셔너리 컬렉션

- 딕셔너리는 키-값 쌍의 형태로 데이터를 저장하고 관리한다.
- 현재(15.x 버전) 딕셔너리 키는 String, Int, Double, Bool 데이터 타입만 사용할 수 있다.
```swift
var 변수명: [키 타입: 값 타입] = [키1: 값1, 키2: 값2 ...]
```

```swift
var sampleDic = ["1": "val_1", 
                 "2": "val_2"]
// 빈 dictionary
var emptyDic: [Int: String]()
```

### 14.7 시퀀스 기반의 딕셔너리 초기화
```swift
let keys = ["1", "2"]
let values = ["val_1", "val_2"]
let sampleDic = Dictionary(uniqueKeysWithValues: zip(keys, values))

// 1 부터 시작하는 키로 지정
let sampleDic = Dictionary(uniqueKeysWithValues: zip(1..., values))
```

```swift
print(bookDict.count) // get count
print(bookDict["key1"]) // get Value
print(bookDict["key1", default: "Book not found"]) // default value

bookDict["key1"] = "new Value" // update value
bookDict.updateValue("new Value", forKey: "key1") // update value

// add new key, value
bookDict["new_key"] = "new value"

// remove key, value
bookDict["key1"] = nil
bookDict.removeValue(forKey: "key1")

// loop
for (bookId, title) in bookDict {
    print("Book ID: \(bookId) Title: \(title)")
}
```

## Chapter 15. 스위프트 5의 에러 핸들링 이해하기

1. 에러를 처리하는 두 단계
- 1) 에러를 발생(throwing) 하는 것.
- 2) 메서드가 던지(throwing) 에러를 잡아서 처리하는 것.

```swift
let connectionOK = true
let connectionSpeed = 30.00
let fileFound = false
enum FileTransferError: Error { // using Error protocal
    case noConnection
    case lowBandwith
    case fileNotFound
}

func transferFile() throws -> Bool {
    // guard 구문은 각 조건이 참인지 거짓인지 검사한다. 만약 거짓이라면 else 구분에 포함된 코드가 실행된다.
    guard connectionOk else {
        throw FileTransferError.noConnection
    }

    guard connectionSpeed else {
        throw FileTransferError.lowBandwidth
    }

    guard fileFound else {
        throw FileTransferError.fileNotFound
    }

    return true
}
```

### 15.4 스로잉 메서드와 함수 호출하기

- 메서드가 에러를 던지도록 선언했다면 일반적인 방법으로 호출할 수 없다. try 구분을 붙여야 한다.
```swift
func sendFile() -> String {
    do {
        try fileTransfer()
    } catch FileTransferError.noConnection {
        return ("No Network Connection")
    } catch FileTransferError.lowBandwidth {
        return ("File Transfer Speed too Low")
    } catch FileTransferError.fileNotFound {
        return ("File not Found")
    } catch { // catch all
        return ("Unknown error")
    }

    return("Successful transfer")
}

func sendFile2() -> String {
    do {
        try fileTransfer()
    } catch FileTransferError.noConnection, FileTransferError.lowBandwidth {
        return ("Connection problem")
    } catch FileTransferError.fileNotFound {
        return ("File not Found")
    } catch { // catch all
        return ("Unknown error")
    }

    return("Successful transfer")
}
```

```swift
// 에러 객체에 접근하기
do {
    try filemgr.createDirectory(atPath: newDir, withIntermediateDirectories: true, attributes: nil)
} catch let error {
    print("Error: \(error.localizedDescription)")
}
```

### 15.6 에러 캐칭 비활성화 하기

- try! 구분을 사용하면 do-catch 구문 내에서 메서드가 호출되도록 감싸지 않아도 스로잉 메서드가 강제로 실행된다.
- 이 방법은 런타임 에러가 발생할 수 있으므로 권장하지 않는다.
```swift
try! fileTransfer
```

### 15.7 defer 구분 사용하기

- defer 구문은 메서드가 결과를 반환하기 직전에 실행되어야 하는 일련의 코드를 지정한다. 리턴 전에 defer 구문이 수행된다.
```swift
func sendFile() -> String {    
    defer {
        removeTmpFiles()
        closeConnection()
    }

    do {
        try fileTransfer()
    } catch FileTransferError.noConnection, FileTransferError.lowBandwidth {
        return ("Connection problem")
    } catch FileTransferError.fileNotFound {
        return ("File not Found")
    } catch { // catch all
        return ("Unknown error")
    }

    return("Successful transfer")
}
```


## Chapter 16. SwiftUI 개요

### 16.1 UIKit와 인터페이스 빌더

1. Swift 이전 개발 방식.
- UIKit, 인터페이스 빌더(스토리보드 포함).
- 컴포넌트 이벤트 처리.
- 시뮬레이션.

### 16.2 SwiftUI의 선언적 구문

1. 구문을 이용하여 화면을 기술. (컴포넌트, 레이아웃매니저, 속성)
  - -> 레이아웃의 위치, 컨스트레인트, 레더링은 SwiftUI가 자동 처리.
2. 프리뷰 캔버스, 라이브 프리뷰 코드 지원.  

## Chapter 17. SwiftUI모드로 Xcode 이용하기

### 17.17 요약

- 앱의 사용자 인터페이스를 만들 때 UIKit 스토리보드를 이용할 것인지, 아니면 SwiftUI를 이용할 것이지 결정할 수 있는 옵션을 준다.(?)
- SwiftUI모드에서 앱 개발과 관련된 대부분의 작업은 코드 에디터와 프리뷰 캔버스에서 이뤄진다.
- 새로운 뷰에 사용자 인터페이스 레이아웃을 추가하고 구성하는 방법으로 코드 에디터에 직접 타이핑하거나, 라이브러리에서 원하는 항목을 에디터나 프리뷰 캔버스로 드래그 앤 드롭하는 방법이 있다.


## Chapter 18. SwiftUI 아키텍처

- 완성된 SwiftUI 앱은 계층적 방식으로 조합된 여러 컴포넌트로 구성된다.
- Scene은 WindowGroup과 같은 SwiftUI 기본 Scense 타입 중 하나에서 파생되거나 사용자 정의로 구축될 수 있다.
- iOS 또는 watchOS에서 애플리케이션은 일반적으로 전체 디스플레이를 차지하는 창 형태를 취하는 단일 Scene을 포함한다.
  + 하지만, maxOS 또는 iPadOS 시스템에서 응용 프로그램은 여러 Scene 인터스턴스로 구성될 수 있으며, 
  + 종종 동시에 표시되거나 탭 인터페이스와 함께 그룹화될 수 있는 별도의 창으로 표시된다.

``` java
App                 // SwiftUI 내 최상위 요소. 1) 각 인스턴스의 시작 및 생명 주기를 처리한다. 2) Scense 관리.
    .Scene          // 각 SwiftUI는 하나 이상의 Scene 포함. Scense은 UI의 섹션 또는 영역을 나타낸다.
        .View       // View는 버튼, 레이블, 텍스트 필드와 같은 UI의 시각적 요소를 구성하는 기본적인 빌딩 블록이다.
        .View(VStack)
            .View(Button)
            .View(TextView)
    .Scene
        .View
        .View

```

## Chapter 19. 기본 SwiftUI 프로젝트 분석

- Xcode 프로젝트 구조의 각 요소에 대해서 분석 (Multiplatform App 템플릿으로 생성한 DemoProject 샘플)

1. 프로젝트App.swift와 ContextView.swift
```swift
// DemoProjectApp.swift
import SwiftUI

@main                        // main 선언 
struct DemoProjectApp: App { // - App
    var body: some Scene {   //   + Scene 
        WindowGroup {        //     + WindowGroup
            ContentView()    //       + View
        }
    }
}
```

```swift
// ContentView.swift
import SwiftUI

struct ContentView: View {               // - View
    var body: some View {                //   + View
        VStack {                         //     + VStack
            Image(systemName: "globe")   //       + Image
                .imageScale(.large)
                .foregroundColor(.accentColor)
            Text("Hello, world!")         //      + Text
        }
        .padding()
    }
}

struct ContentView_Previews: PreviewProvider {
    static var previews: some View {
        ContentView()
    }
}
```

2. Assets.xcassets
 -  Assets.xcassets 폴더에는 이미지, 아이콘 및 색상과 같은 앱에서 사용하는 리소스를 저장하는 데 사용하는 애셋 카탈로그 포함.

3. DemoProject.entitlements
- entitlements 파일은 앱 내에서 특정 iOS 기능에 대한 지원을 활성화하는 데 사용된다.
  + 앱에서 iCloud 저장소 또는 디바이스 마이크에 접근해야 하거나 시리를 통해 음성 제어를 통합하려는 경우 이 파일 내에서 권한을 먼저 활성화해야 한다.

4. Preview Content
- 프리뷰 애셋 폴더에는 개발 중에 앱을 미리 볼 때 필요하지만 완성된 앱에서는 필요하지 않은 자산 및 데이터가 포함되어 있다.
- 앱 스토어에 제출하기 위해 앱을 패키징할 준비가 되면 Xcode는 불필요한 공각을 차지하지 않도록 이러 자산을 배달 아카이브에서 제거한다.


## Chapter 20. SwiftUI로 커스텀 뷰 생성하기

SwiftUI를 이용하여 앱 개발을 배우는 과정 중에서 중요한 한 가지는 내장된 SwiftUI 뷰를 사용함과 동시에 자신만의 커스텀 뷰를 만들어 자신이 원하는 UI 레이아웃을 어떻게 선언하는지를 배우는 것이다.

### 20.1 SwiftUI 뷰

- 사용자 인터페이스(UI) 레이아웃은 뷰의 사용과 생성, 그리고 결합을 통해서 SwiftUI로 구성된다.
- SwiftUI에서 뷰는 View 프로토콜을 따른 구조체로 선언된다.
  + View 프로토콜을 따르도록 하기 위해서 구조체는 body 프로퍼티를 가지고 있어야 하며, 이 body 프로퍼티 안에 뷰가 선언되어야 한다.
- 각각의 뷰는 View 프로토콜을 따르는 독립적인 객체다.
- SwiftUI는 UI 레이아웃을 설계하는 데 사용되는 내장 컴포넌트들의 라이브러리를 제공한다.
- 뷰의 모양과 동작은 수정자를 적용하여 구성할 수 있으며, 커스텀 뷰와 하위 뷰를 생성하기 위하여 수정되거나 그루핑될 수 있다.
- 커스텀 컨테이너 뷰는 ViewBuilder 클로저 프로퍼티를 이용하여 생성될 수 있다.

### 20.6 뷰 변경하기

- 모든 SwiftUI 뷰에는 뷰의 모양과 동작을 변경하는 데 사용될 수 있는 수정자(modifier)들이 있다.

### 20.7 텍스트 스타일로 작업하기

- 뷰에 텍스트를 표시하기 위해 내장된 텍스트 스타일을 사용할 수있다.
- 만약 내장된 텍스트 스타일을 이용하여 뷰의 폰트를 선언했다면 텍스트 크기를 사용자기 지정한 폰트 크기에 따라 동적으로 맞춰진다. (iOS 설정 > 디스플레이 및 밝기 > 텍스트 크기) (앱플 권장 사항)
- 텍스트 스타일
  + Large Title, Title, Title2, Title3
  + Headline, Subheadline
  + Body
  + Callout   // iMessage 메시지
  + Caption, Caption2
  + Footnote

### 20.8 수정자 순서

- 수정자들을 연결할 때 수정자들이 **적용되는 순서에 따라 모양이 달라진다.**

### 20.9 커스텀 수정자

- 같은 수정자를 적용할 때 커스텀 수정자를 묶어서 참조하게 한다. 커스텀 수정자는 ViewModifier 프로토콜을 따르는 구조체로 선언한다.
- 커스텀 수정자가 필요한 곳에서 각 View에서 modifier() 메서드를 호출하여, 커스텀 수정자를 전달하여 적용한다.

```swift
Text("Text 1")
  .font(.largeTitle)
  .backgroud(Color.white)
  .border(Color.gray, width: 0.2)
  .shadow(co.lr: Color.black, radius: 5, x: 0, y: 5)

// =====> 커스텀 뷰 적용
struct StandardTitle: ViewModifier {
    func body(content: Content) -> some View {
        content
            .font(.largeTitle)
            .backgroud(Color.white)
            .border(Color.gray, width: 0.2)
            .shadow(co.lr: Color.black, radius: 5, x: 0, y: 5)
    }
}

Text("Text 1")
    .modifier(StandardTitle())
Text("Text 2")
    .modifier(StandardTitle())
```

### 20.10 기본적인 이벤트 처리

``` swift
struct ContentView: View {
    var body: some View {
        Button(action: buttonPressed) {
            Text("Click Me")
        }
    }

    func buttonPressed() {
        // 동작할 코드 기술
    }
}

// 위 코드에서, 버튼 클릭되었을 때 실행될 코드를 클로저로 처리할 수 있다.
struct ContentView: View {
    var body: some View {
        Button(action: {
            // 동작할 코드 기술
        }) {
            Text("Click Me")
        }
    }
}
```

### 20.11 커스텀 컨테이너 뷰 만들기

- 하위 뷰의 한 가지 한계는 컨테이너 뷰의 콘텐트가 정적 이라는 점이다. 하위 뷰가 레이아웃에 포함되는 시점에 하위 뷰에 포함될 뷰를 동적으로 지정할 수 없다.
- 커스텀 컨테이너 뷰를 생성할 때 SwiftUI의 `ViewBuilder` 클로저 속성을 이용하면, 콘텐트 뷰들을 받아서 동적으로 단일 뷰를 만들 수 있다.

```swift
struct MyVStack<Content: View>: View {
    let content: () -> Content
    init(@ViewBuilder content: @escaping () -> Content) {
        self.content = content
    }

    var body: some View {
        VStack(space: 10) {
            content()
        }
        .font(.largeTitle)
    }
}

MyVStack {
    Text("Text 1")
    Text("Text 2")
    HStack {
        Image(systemName: "star.fill")
        Image(systemName: "star.fill")
        Image(systemName: "star")
    }
}
```

### 20.12 레이블 뷰로 작업하기

- 레이블 뷰는 아이콘과 텍스트가 나란히 배치된 형태의 두 요소로 구성된다.
- 이미지는 모든 이미지 애셋이나, SwiftUI 쉐이프 렌더링, 또는 SF 심볼의 형태를 취할 수 있다. (SF 심볼: 라이브러리 맨 우측에 심볼 탭 참조.)
```swift
Label("Welcom to SwiftUI", systemImage: "person.circle.fill") // SF 심볼 사용
    .font(.largeTitle)

Label("Welcom to SwiftUI", image: "myimage") // 앱 애셋 카탈로그의 이미지 사용한 경우

Label( // 별도의 뷰를 사용하여, 레이블 선어. 제목에 Text 뷰 사용하고, 아이콘은 원 그림 사용해서 표기
    title: {
        Text("Welcom to SwiftUI")
            .font(.largeTitle)
    },
    icon: {
        Circle()
            .fill(Color.blue)
            .frame(width: 25, height: 25)
    }
)
```


## Chapter 21. SwiftUI스택과 프레임

- UI 설계를 크게 보면, 인터페이스 컴포넌트를 선택하고 뷰를 어떻게 배치할지 결정한 후 
- 서로 다른 화면과 뷰들 간의 이동을 구현하는 것이다.
- SwfitUI는 UI의 구성 방법과 화면의 방향과 크기에 따라 대응하는 방법을 정의하는 **레이아웃** View를 제공한다.

### 21.1 SwiftUI 스택

- SwiftUI는 VStack(수직), HStack(수평), ZStack(중첩되게 배치) 형태의 3개의 스택 레이아웃 View를 제공한다.

### 21.3 컨테이너의 자식 뷰 제한

- 컨테이너 뷰(Stack)는 직접적인 하위 뷰를 10개로 제한한다. 뷰가 10개를 넘어야 한다면, 여러 컨테이너로 나눠서 담는다.
  + **Xcode15.1 / Any iOS 에서는 50개 넘어도 오류 안남.**
- Group뷰를 이용하여 뷰를 나눈다. 필요시 해당 그룹을 하나의 명령으로  숨길 수 있다.
```swift
VStack {
    Group {
        Text("Sample Text")
        Text("Sample Text")
        Text("Sample Text")
        Text("Sample Text")
        Text("Sample Text")
        Text("Sample Text")
    }

    Group {
        Text("Sample Text")
        Text("Sample Text")
        Text("Sample Text")
        Text("Sample Text")
        Text("Sample Text")
        Text("Sample Text")
    }
}
```

### 21.4 동적 HStack과 VStack 변환

- AnyLayout 인스턴스를 생성하고, HStackLayout 또는 VStackLayout 컨테이너에 할당하여 동적으로 변경할 수 있다.

```swift
struct DynamicStackView: View {
    @State var myLayout: AnyLayout = AnyLayout(VStackLayout())
    
    var body: some View {
        VStack {
            myLayout {
                Image(systemName: "goforward.10")
                    .resizable()
                    .aspectRatio(contentMode: .fit)
                Image(systemName: "goforward.15")
                    .resizable()
                    .aspectRatio(contentMode: .fit)
            }
            
            HStack {
                Button(action: {
                    myLayout = AnyLayout(HStackLayout()) // 클로저함수
                }) {
                    Text("HStack")
                }
                Button(action: {
                    myLayout = AnyLayout(VStackLayout())
                }) {
                    Text("VStack")
                }
            }
        }
    }
}
```

### 21. 텍스트 줄 제한과 레이아웃 우선순위

- 스택의 크기가 제한되거나 다른 뷰과 공간을 나눠사용하면 뷰 텍스트는 여러 줄로 표시된다.
- 텍스트 줄을 몇 줄로 표현할지는 `.lineLimit()` 수정자(줄제한)로 조정한다.
- 우선수위(priority)에 대한 가이드를 주면 높은 숫자가 우선이 되어 텍스트가 잘리는 현상이 사라진다. (`.layoutPriority(1)`)

```swift
    HStack {
        Image(systemName: "airplane")
        Text("Flight time: ")
        Text("London")
            .layoutPriority(1)
    }
    .font(.largeTitle)
    .lineLimit(1) // (1..4) 범위로 지정 가능
```
### 21.6 전통적 스택 vs. 지연(lazy) 스택

- 기존 HStack, VStack 뷰는 사용할 때 시스템은 포함된 하위 뷰들이 모두 생성된다. 만약 하위뷰가 수천 개가 있다면 성능 저하로 이어질 수 있다.
- 이 문제를 해결하기 위해서 SwiftUI는 LazyVStack, LazyHStack 뷰도 제공한다. 이 뷰는 필요할 때만 뷰를 생성하고, 화면 밖 뷰는 생성하지 않으며 화면을 벗어나면 뷰를 해제한다.

### 21.7 SwiftUI 프레임

- 기본적으로 뷰는 자신의 콘텐트와 자신이 속한 레이아웃에 따라 **자동으로 크기가 조절된다.**
- 뷰 자체가 특정 크기나 영역에 맞아야 한다면 frame 수정자를 사용한다.
- 디폴트로, frame은 화면을 채울 때 안전 영역(safe area)을 준수한다. 안전 영역 밖에까지 확장되도록 frame을 구성하려면 `.edgesIgnoringSafeArea(.all)` 수정자를 사용한다.

```swift
    Text("Hello World, how ary you?")
        .font(.largeTitle)
        .frame(minWidth: 100, maxWidth: 300, minHeight: 100,
                maxHeight: 100, alignment: .center)
        .border(Color.blue, width: 5)
```

### 21.8 frame과 GeometryReader

- 프레임은 뷰들을 담고 있는 컨테이너의 크기에 따라 조절되도록 구현할 수도 있다.
- GeometryReader로 뷰를 감싸고 컨테이너의 크기를 식별하기 위한 리더를 이용할 수 있다.

```swift
    var body: some View {
        GeometryReader { geometry in
            VStack(alignment: .center) {
                Text("Hello World, how are you?")
                    .font(.largeTitle)
                    .frame(width: geometry.size.width / 2,
                           height: (geometry.size.height / 4) * 2)
                    .border(Color.blue)
                Text("Goodbye World")
                    .font(.largeTitle)
                    .frame(width: geometry.size.width / 3,
                           height: geometry.size.height / 4)
                    .border(Color.blue)
            }
            .border(Color.red)
        }
```

## Chapter 22. SwiftUI상태 프로퍼티, Observable, State, Environment 객체

- UI 내의 뷰들은 기본 데이터의 변경에 따른 처리 코드를 작성하지 않아도 뷰가 업데이트된다. 이것은 데이터와 UI 내의 뷰사이에 게시자(publisher)와 구독자(subscriber)를 구축하여 할 수 있다.
- 이를 위하여 SwiftUI는 1) State 프로퍼티, 2) Obserable 객체(iOS13), 3) State 객체(iOS14), 4) Environment 객체를 제공하며, 이들 모두 UI 의 모양과 동작을 결정하는 상태를 제공한다.

### 22.1 상태 프로퍼티

- 상태 프로퍼티는 String 이나 Int 값처럼 간단한 데이터 타입을 저장하기 위해 사용되며, `@State` 프로퍼티 래퍼를 사용하여 선언된다.
- **상태 프로퍼티 값이 변경되었다는 것은 그 프로퍼티가 선언된 뷰 계층 구조를 다시 렌더링해야 한다는 SwiftUI 신호다.**
  + 결국, 그 프로퍼티에 의존하는 모든 뷰는 어떤 식으로든 최신 값이 반영되도록 업데이트된다.

### 22.2 State 바인딩

- 하위뷰에 상위 State 값을 `@Binding` 프로퍼티 래버를 이용하여 프로퍼티를 선언하여 연결한다.

```swift
struct ContentView: View {
    @State private var wifiEnabled = true
    @State private var userName = ""
    
    var body: some View {
        VStack {
            Toggle(isOn: $wifiEnabled) {
                Text("Enable Wi-Fi")
            }
            TextField("Enter user name", text: $userName)
            WifiImageView(wifiEnabled: $wifiEnabled) // <-- 하위에 State 연결.
        }
        .padding()
    }
}

struct WifiImageView: View {
    @Binding var wifiEnabled: Bool // <-- 상위의 State 연결.
    var body: some View {
        Image(systemName: wifiEnabled ? "wifi" : "wifi.slash")
    }
}
```

### 22.3 Observable 객체

- 상태 프로퍼티는 뷰의 상태를 저장하는 방법을 제공하여 해당 뷰와 하위 뷰에만 사용할 수 있다. 상태 프로퍼티는 일시적인 것이어서 부모 뷰가 사라지면 그 상태로 사라진다.
- 반면, Observable 객체는 여러 다른 뷰들이 외부에서 접근할 수 있는 지속적인 데이터를 표현하기 위해 사용된다.

- Observable 객체는 ObservableObject 프로토콜을 따르는 클래스나 구조체 형태를 취한다.
- Observable 객체는 게시된 프로퍼티(published property)로서 데이터 값을 **게시한다.**
  그런 다음, Observer 객체는 게시자를 **구독하여** 게시된 프로퍼티가 변경될 때마다 업데이트를 받는다.
- Combine 프레임워크에 포함되어 있는 Observable 객체는 게시자와 구독자 간의 관계를 쉽게 구축할 수 있도록 iOS 13에 도입되었다.

### 22.4 State 객체

- iOS14에 도입된 상태 객체(State Object) 프로퍼티 래퍼는 @ObservedObject 래퍼의 대안이다.
- @ObservedObject 는 선언한 뷰가 참조를 소유하지 않아 SwfitUI 시스템에 의해서 파괴될 수 있고, @StateObject 는 참조를 소유하여 파괴되지 않는다.
- **@ObservedObject 보다는 @StateObject를 사용하도록 한다.**

```swift
import Foundation
import Combine

class DemoData: ObservableObject {
    @Published var userCount = 0      // 1) publish
    @Published var currentUser = ""

    init() {
        // 데이터를 초기화하기 위한 코드가 여기 온다.
        updateData()
    }

    func updateData() {
        // Code here to keep data up to date
        // 데이터를 최산 상태로 유지하기 위한 코드가 여기 온다.
    }
}
```

```swift
import SwfitUI

struct ContentView: View {
    @StateObject var demoData : DemoData = DemoData() // 2) 구독
    var body: some View {
        Text("\(demoData.currentUser), you are user number \(demoDta.userCount)")   
    }
}
```

### 22. Environment 객체

- Environment 객체는 Observable 객체와 같는 방식으로 선언된다. 중용한 차이점은 이 객체는 SwiftUI 환경에 저장되며, 뷰에서 뷰로 전달할 필요 없이 모든 자식 뷰가 접근할 수 있다.
- 뷰의 상위 Stack에서 `.environmentObject()` 수정자를 이용하여, **Observable 객체 인스턴스를 전달한다.**

```swift
struct EnvironmentObjectView: View {
    let speedsetting = SpeedSetting()
    
    var body: some View {
        VStack {
            SpeedControlView()
            SpeedDisplayView()
        }
        .environmentObject(speedsetting) // 뷰에 Observable 객체 인스턴스를 전달한다
        .padding()
    }
}

class SpeedSetting: ObservableObject{
    @Published var speed = 0.0
}

struct SpeedControlView: View {
    @EnvironmentObject var speedsetting: SpeedSetting // 부모로 부터 environmemtObject를 받는다.
    var body: some View {
        Slider(value: $speedsetting.speed, in: 0...100)
    }
}

struct SpeedDisplayView: View {
    @EnvironmentObject var speedsetting: SpeedSetting
    var body: some View {
        Text("Speed = \(speedsetting.speed)")
    }
}
```

## Chapter 23. SwiftUI예제 튜토리얼

-- 예제 skip

## Chapter 24. 스위프트 구조화된 동시성 개요

- 동시어(concurrency)은 여러 작업을 병렬로 수행하는 소프트웨어 기능으로 정의할 수 있다.
- 스위프트 프로그래밍 언어의 구조화된 동시성(structured concurrency) 기능을 살펴보고, 앱 프로젝트에 멀티태스킹 지원을 추가하는 방법을 설명한다.
- 구조화된 동시성이 백그라운드에서 스레드를 사용하지만 모든 복잡성을 처리하므로 직접적인 상호작용할 필요가 없다.

### 24.2 애플리케이션 메인 스레드

- 앱이 처음 시작될 때 런타임 시스템은 보통 앱이 기본적으로 실행되는 단일 스레드를 생성한다. 이 스레드를 일반적으로 메인 스레드라 한다.
 메인 스레드의 주요 역할은 UI 레이아웃 렌더링, 이벤트 처리 및 사용자 인터페이스에서 뷰와 사용자 상호작용 측면에서 UI를 처리한다.
- 메인 스레드를 사용하여 시간 소모적인 작업을 하면 전체 애플리케이션이 멈춘 것 처럼 보이게 된다. 메인 스레드의 작업을 방해받지 않도록 별도로 작업을 수행할 스레드를 시작할 수 있다.

### 24.3 완료 핸들러

- 9장 '스위프트의 함수, 메서드, 클로저'에서 설명한 것 처럼, 스위프트는 **완료 핸들러(completion handler)** 를 사용하여 비동기 코드 실행을 구현한다.

### 24.4 구조화된 동시성

- 구조화된 동시성은 스위프트 버전 5.5와 함께 스위프트 언어에 도입되어 앱 개발자가 동시 실행을 보다 쉽고 논리적으로 작성하고, 이해하기 쉬운 방식으로 안전하게 구현할 수 있도록 한다.

### 24.8 동기 함수에서 비동기 함수 호출

- 구조화된 동시성의 규첵은 비동기 함수가 비동기 콘텍스트 내에서만 호출될 수 있을을 나타낸다.
- 동기함수에서 비동기함수를 호출하려면 **Task** 객체를 사용하여 비동기 함수를 시작한다.

```swift
    Button(action: {
        Task {
            await doSomethingAsyncLet()
        }
    }, label: {
        Text("Do Something(AsyncLet)")
    })
```
### 24.9 await 키워드

- await 키워드는 비동기 함수를 호출할 때 필요하며 일반적으로 다른 비동기 함수 범위 내에서만 사용할 수 있다.
- 비동기 호출을 허용하는 것 이외에도 await 키워드는 일시적인 중단점을 정의한다. 시스템은 우선 순위가 더 높은 작업에 리소스를 할당할 수 있다.

### 24.10 async-let 바인딩 사용하기

- awit 는 호출된 함수가 반환될 때까지 기다린다.
- 그러나, 더 일반적인 요구사항은 비동기 함수가 백그라운드에서 실행되는 동안 호출하는 함수 내에서 코드를 계속 실행하는 것이다. 
 async-let 바인딩을 사용하여 해당 코드에서 나중까지 결과를 기다리는 것을 지연시킬 수 있다.
 
### 24.11 오류 핸들링

 - throw / do / try / catch 매커니즘을 사용한다.

### 24.12 Task 이해

- 비동기적으로 실행되는 모든 작업은 스위프트의 Task 클래스의 인스턴스 내에서 실행된다. 앱은 여러 작업을 동시에 실행할 수 있으며 이러한 작업을 계층적으로 구성할 수 있다.
- 자식 작업은 부모로부터 우선순위와 같은 속성을 상속하며 계층 구조는 모든 하위 작업이 완료될 때까지 부모 작업이 종료되지 않도록 한다.
- 작업을 그룹화 하여 여러 비동기 작업을 동적으로 시작할 수도 있다.

### 24.13 구조화되지 않은 동시성

- 구조화되지 않은 동시성(unstructed concurrency) 은 Task객체를 사용하여 만들 수 있다. 구조화 되지 않은 작업의 일반적인 용도는 동기 함수 내에서 비동기 함수를 호출하는 것이다.
  + 결국은 동기에서 비동기 함수를 호출하는 Task 생성을 얘기하는 듯함.
- Task(구조화되지 않은 작업)는 외부에서 취소할 수 있다.

```swift
let task = Task(priorty: .high) {
    await doSomething()
}

// 중략

if(!task.isCancelled) {
    task.cancel()
}
```

### 24.13 분리된 작업

- 분리된 작업(detached task)은 구조화되지 않은 동시성의 또 다른 형태로 호출하는 부모로부터 속성을 상속하지 않는다.
- ??? 속성을 상속하지 않으면, 어떤 경우에 사용하는 것인지???
```swift
Task.detached {
    await doSomething()
}
```

### 24.15 작업 관리

```swift
// 작업 취소
Task.cancel()

// 1. 취소여부 확인
if Task.isCancelled {

}

// 2. 취소여부 확인
do {
    try Task.checkCancellation() // 작업이 취소된 경우, CancellationError 오류가 발생한다.
} catch {
    // 작업 정리 수행
}

// 작업코드 내에서, 일시 중단할 경우.
Task.yield() 
```

### 24.16 작업 그룹

- `withThrowingTaskGroup()` 또는 `withTaskGroup()` 함수를 사용하여 작업그룹을 구현할 수 있다.
- **그룹내 Task는 시작된 순서대로 완료되지 않는다.**
- 작업 그룹에 접근할 수 있는 몇가지 메서드와 속성을 제공한다.
  + addTask() 그룹에 작업을 추가한다.
  + cancelAll() 그룹의 모든 작업을 취소한다.
  + isCancelled 작업 그룹이 미미 취소되었는지 여부
  + isEmpty 작업 그룹내에 작업이 남아 있는지 여부

```swift
func doSomethingAsyncByGroup() async {
    print("--- Start \(Date())")
    await withTaskGroup(of: Void.self) { group in
        for i in 1...5 {
            group.addTask {
                async let result = takesTooLongAsyncLet()
                print("Complted Task \(i) = \(await result)")
            }
        }
    }
    print("--- End \(Date())")
}

func takesTooLongAsyncLet() async -> Date {
    sleep(5) // seconds
    return Date()
}
```
### 24.17 데이터 경쟁 피하기

- 데이터에 동시에 접근할 경우 데이터 경쟁(data race)조건이 발생할 위험이 있다. 데이터가 손상될 수 있으므로 컴파일러에서 오류가 표시된다.
- 이 경우 처리방안은 1) 데이터를 저장할 액터를 만들거나(25장), 2) withTaskGroup() 함수에서 결과 반환을 받아, for await에서 결과를 처리한다. 

### 24.18 for await 루프

- for await 표현식을 사용하면 비동기적을 반환되는 값의 수신을 기다릴 수 있다.
```swift
func doSomethingAsyncByGroupForAwait() async {
    var timeStamps: [Int: Date] = [:]
    await withTaskGroup(of: (Int, Date).self) { group in
        for i in 1...5 {
            group.addTask {
                return (i, await takesTooLongAsyncLet())
            }
        }
        
        for await (task, date) in group {
            timeStamps[task] = date
        }
    }
    
    for (task, date) in timeStamps {
        print("Task = \(task), Date = \(date)")
    }
}
```

### 24.19 비동기 속성

- 스위프트는 클래스와 구조체 타입 내에서 비동기 함수 뿐만아니라 **비동기 속성도 지원한다.** 현재는 읽기 전용 속성만 비동기가 될 수 있다.  


## Chapter 25. 스위프트 액터 소개

### 25.1 액터 개요
- 액터는 한 번에 하나의 작업만 데이터에 접근할 수 있도록 내부 변경 가능 상태에 대ㄴ 비동기 접근을 제어하는 스위프트 타입이다.
- 액터는 **참조 타입이고** 속성, 생성자 및 메서드를 포함한다는 점에서 클래스와 매우 유사하다.
- 액터를 선언할 때의 가장 큰 차이점은 `class`대신 `actor`라는 단어가 사용된다.

### 25.2 액터 선언하기

- 액터는 비동기 함수 또는 Task 클로저 내와 같은 비동기 콘텍스트 내에서만 생성 및 액세스할 수 있다.
- 액터 메서드를 호출하거나 속성에 접근할 때 await 키워드를 받드시 사용해야 한다.

```swift
actor BuildMessage {
    var message: String = ""
    let greeting = "Hello"

    func setName(name: String) {
        self.message = "\(greeting) \(name)"
    }
}

func someFunction() async {
    let builder = BuildMessge() // actor
    await build.setName(name: "Jane Smith")
    let message = await build.messge
    print(message)
}
```

### 25.3 데이터 격리 이해하기

- 액터 내의 모든 메서드와 가변적인 속성은 격리된 것으로 간주되며 await 키워드를 통해서만 호출할 수 있다.
- 가변적인 속성에 접근하지 않는 액터 메서드는 nonisolated 키워드를 사용하여 격리에서 제외시킬 수 있다.

### 25.4 스위프트 액터 예제
```swift

import SwiftUI

struct ContentView: View {
    var body: some View {
        VStack {
            Button(action: {
                Task {
                    await doSomethging()
                }
            }, label: {
                Text("Do something")
            })
            .padding()
        }
        .padding()
    }
    
    func doSomethging() async {
        print("--- Start \(Date())")
        let store = TimeStore()
        await withTaskGroup(of: Void.self) { group in
            for i in 1...5 {
                group.addTask {
                    await store.addStamp(task: i, date: await takesTooLong())
                }
            }
        }
        
        for (task, date) in await store.timeStamps {
            print("Task = \(task), Date = \(date)")
        }
        print("--- End \(Date())")
    }
    
    func takesTooLong() async -> Date {
        sleep(2)
        return Date()
    }
}

actor TimeStore {
    var timeStamps: [Int: Date] = [:]
    func addStamp(task: Int, date: Date) {
        timeStamps[task] = date
    }
}
#Preview {
    ContentView()
}
```

### 25.5 MainActor 소개

- 메인 스레드에서만 UI 업데이트를 수행된다.
- 스위프트에서 메인 스레드는 메인 액터로 표현된다. 이것을 전역 액터(global actor)라고 한다.
- 앱을 개발할 때, 메인 액터에서 실행하길 원하는 코드가 있을 수 있다. 특히 해당 코드가 어떤 식으로든 UI를 업데이트해야하는 경우다.
   이런 경우 @MainActor 속성을 사용하여 코드를 표시할 수 있다.
```swift
@MainActor
class TimeStore {
    var timeStamps: [Int: Date] = [:]
    func addStamp(task: Int, date: Date) {
        timeStamps[task] = date
    }
}
```

- 다른 방법으로 단일 값이나 속성을 메인 스레드 종속으로 표시할 수 있다.
```swift
class TimeStore {
    @MainActor var timeStamps: [Int: Date] = [:]
    @MainActor func addStamp(task: Int, date: Date) { // timeStamps 에 접근하기 위해 @MainActor 선언
        timeStamps[task] = date
    }
}
```

- MainActor의 메소드는 메인 스레드에서 작업을 수행하도록 비동기 코드 내에서 직접 호출 될 수 도 있다.
```swift
func runExample() async {
    await MainActor.run {
        // 메인 스레드에서 작업 수행
    }
}
```

## Chapter 26. SwiftUI동시성 및 생명 주기 이벤트 수정자

1. 이벤트 수정자
이벤트 수정자는 일반적인 UI 언어에서 이벤트 메소드 일부이다.

- onAppear() : 
- onDisapper() : 
- onChange() : 

### 26.5 ScenePhase와 onChange 수정자

- ScenePhase는 현재 화면의 상태를 저장하기 위해 SwiftUI에서 사용하는 `@Environment` 속성이다.
- ScenePhase 환경 프로퍼티를 onChange()와 함계 사용하면 앱의 화면 상태가 변경되는 시기를 식별할 수 있다.
  화면이 포그라운드나 백그라운드로 전환되거나 활성화 또는 비활성화 될 때 앱은 작얼을 실행한다.
- 앱 선언부에 적용할 때 유용하고, 선언부에서 개발 뷰만 적용도 가능하다.

```swift
@main
struct Demo26LifecycleApp: App {
    @Environment(\.scenePhase) private var scenePhase
    
    var body: some Scene {
        WindowGroup {
            ContentView()
        }
        .onChange(of: scenePhase, perform: { phase in
            switch phase {
                case .active: // 화면이 포그라운드에 있으며, 사용자에 표시되며, 사용자 인터랙션에 반응한다.
                    print("Active")
                case .inactive: // 화면이 포그라운드에 있고, 사용자에게 표시되지만 사용자 인터랙션에 반응하지 않는다.
                    print("Inactive")
                case .background:
                    print("Background") // 사용자에게 화면(앱)이 표시되지 않는다.
                default:
                    print("Unknown scenephase")
            }
        })
    }
}
```

### 26.6 동시 작업 시작하기

- task() 수정자를 사용하여 뷰를 만들 때 비동기 작업을 처리할 수 있다.

```swift
struct FirstTabView: View {
    @State var title = "View One"
    
    var body: some View {
        Text(title)
            .task(priority: .background) { // task modifier 를 통해서, 비동기 호출 함.
                title = await changeTitleAsync()
            }
    }
    
    func changeTitleAsync() async -> String {
        sleep(3)
        return "Aync task complete \(Date())"
    }
}
```

## Chapter 27. Observable 객체와 Environment 객체 튜토리얼

1. Observable 객체와 Environment 객체 사용 예제
- Observable 객체 구현, 프로퍼터 게시 정의
- Observable 객체를 이용한 구독 방법
- Environment 객체를 이용한 구독 방법

## Chapter 28. AppStorage와 SceneStorage를 사용한 SwiftUI데이터 지속성

- SwiftUI는 소량의 앱 데이터를 지속적으로 저장하기 위한 특별한 목적을 위해 두 개의 프로퍼티 래퍼(@AppStorage, @SceneStorage)를 제공한다.

### 28.1 @SceneStorage 프로퍼티 래퍼

- @SceneStorage 프로퍼티 래퍼는 개별 앱 화면 인스턴스의 범위 내에서 소량의 데이터를 저장할 때사용하고, 앱이 실행되는 사이에 화면 상태를 저장하고 복원하는 데 이상적이다.
- 화면 저장소(Scene Storage)는 관련된 값을 저장하기 위해 키 문자열과 함께 @SceneStorage 프로프터 래퍼를 사용하여 선언된다.
- 화면 저장소로 작업할 때, 화면의 각 인스턴스에는 다른 화면과 완전히 분리된 자체 저장소가 있다.!!!

```swift
@SceneStorage("city") var city: String = "" // key : "city"

var body: some View {
    TextEditor(text: $city)
        .padding()
}
```

### 28.2 @AppStorage 프로퍼티 래퍼

- @AppStorage 프로퍼티 래퍼는 앱 전체를 통하여 접근하고 사용할 수 있는 데이터를 저장하는 데 사용된다.
- 앱 저장소(app storage)는 수년 동안 iOS에서 사용할 수  있었던 기능인 UserDefaults를 기반으로 구축되었다.
```swift
@AppStorage("mystore") var myText: String = "" // key : mystore
```

- 데이터는 디폴트로 표준 UserDefaults 저장소에 저장된다. 하지만 데이터를 저장할 커스텀 앱 그룹(app group)을 지정할 수도 있다.
  앱 그룹은 앱이 동일한 그룹 내의 다른 앱 또는 타깃과 데이터를 공유할 수 있게 한다.
  앱 그룹에는 이름(일반적으로 group.com.mydomain.myappname)이 할당되며, **Xcode 프로젝트의 Signing & Capabilities 화면** 내에서 활성화되고 구성된다.
- iPad에서 멀티 인스턴스를 실행하면, 같은 app storage를 사용하는 인스턴스는 같이 UI가 업데이트 되며, scene storage는 각 인스턴스별로 분리되어 각각 상태를 유지한다.
- @State 프로퍼티 래퍼와 마찬가지로 저장된 값을 변경하면 새로운 데이터가 반영하도록 사용자 인터페이스가 새로고침 된다.
```swift
@AppStorage("mystore",
            store: UserDefaults(suiteName: "group.com.mydomain.userdefaults")
           ) var mytext: String = ""

```

### 28.6 커스텀 타입 저장하기

- 기본 타입외에 다른 타입을 저장해야 한다면 스위프트의 Data 객체로 인코딩해서 저장하고, 가져올 때 디코딩한다.

```swift
// custom data - struct
@AppStorage("username") var namestore: Data = Data()
var username = UserName(firstName: "Mark", secondName: "Wilson")
// save
let encoder = JSONEncoder()
if let data = try? encoder.encode(username) {
    namestore = data
}

// read
let decoder = JSONDecoder()
if let name = try? decoder.decode(UserName.self, from: namestore) {
    username = name
}

// struct
struct UserName: Encodable, Decodable {
    var firstName: String
    var secondName: String
}
```

```swift
// custom data - image
@AppStorage("myimage") var imagestore: Data = Data()
var image = UIImage(named: "profilephoto")

// encoding to save
if let data = image!.pngData() {
    imagestore = data
}

// decoding to read
if let decodedImage: UIImage = UIImage(data: imagestore) {
    image = decodedImage
}
```

## Chapter 29. SwiftUI스택 정렬과 정렬 가이드

- 컨테이너 정렬, 정렬 가이드, 커스텀 정렬, 서로 다른 스택들 간의 정렬 구현에 대해서 설명함.

### 29.1 컨테이너 정렬

- 기본 정렬 방법은 컨테이너 정렬이며, 스택에 포함된 하위 뷰들이 스택 내에서 정렬되는 방식을 정의한다.
  스택에 포함된 각각의 뷰에 지정된 정렬이 따로 없다면, 스택에 적용한 정렬이 하위 뷰에 적용된다.
- 이렇게 개별적으로 적용된 정렬이 없는 하위 뷰에 상위 뷰의 정렬 방법이 적용된는 것을 암묵적으로 정렬(implicitly aligned) 되었다고 한다.
- VStack, HStack은 중앙 정렬(.center)을 디폴트로 한다.
```swift
    VStack(alignment: .trailing) {
        Text("This is some text.")
        Text("This is some longer text.")
        Text("This is short.")
    }

    HStack(spacing: 20) {
        Text("This is some text.")
            .font(.largeTitle)
        Text("This is some longer text.")
            .font(.body)
        Text("This is short.")
            .font(.headline)
    }

    HStack(alignment: .lastTextBaseline,  spacing: 20) {
        Text("This is some text.")
            .font(.largeTitle)
        Text("This is some longer text.")
            .font(.body)
        Text("This is short.")
            .font(.headline)
    }
```

### 29.2 정렬 가이드

- 정렬 가이드(alignment guide)는 뷰가 스택에 포함된 다른 뷰와 정렬해야 할 때 사용되는 커스텀 포지션을 정의하는 데 사용된다.
  이것은 표준 정렬 타입보다 더 복잡한 정렬을 구현할 수 있게 해준다.
  예를 들어 ,정렬 가이드는 길이의 2/3 위치 또는 상단에서 20 포인트를 기준으로 뷰를 정렬할 때 사용할 수 있다.
- 정렬 가이드내의 ViewDemensions 객체는 뷰의 HorizontalAlignment와 VerticalAlignment 프로퍼티에 대한 접근을 제공한다.

```swift
    VStack(alignment: .leading) {
        Rectangle()
            .foregroundColor(Color.green)
            .frame(width: 120, height: 50)
        Rectangle()
            .foregroundColor(.red)
            .frame(width: 200, height: 50)
        Rectangle()
            .foregroundColor(.blue)
            .frame(width: 180, height: 50)
    }
    
    // alignmentGuide를 이용해서 offset을 조정한 예.
    VStack(alignment: .leading) {
        Rectangle()
            .foregroundColor(Color.green)
            .frame(width: 120, height: 50)
        Rectangle()
            .foregroundColor(.red)
            .alignmentGuide(.leading, computeValue: { d in 120.0 }) // 부모 스택의 정렬과 일치해 함.
            .frame(width: 200, height: 50)
        Rectangle()
            .foregroundColor(.blue)
            .frame(width: 180, height: 50)
    }
    
    // alignmentGuide를 이용해서 offset을 조정한 예.
    VStack(alignment: .leading) {
        Rectangle()
            .foregroundColor(Color.green)
            .frame(width: 120, height: 50)
        Rectangle()
            .foregroundColor(.red)
            .alignmentGuide(.leading, computeValue: { d in d.width / 3 }) // 부모 스택의 정렬과 일치해 함.
            .frame(width: 200, height: 50)
        Rectangle()
            .foregroundColor(.blue)
            .alignmentGuide(.leading, computeValue: { d in d[HorizontalAlignment.trailing] + 20}) // 부모 스택의 정렬과 일치해 함.
            .frame(width: 180, height: 50)
    }
```

### 29.4 커스텀 정렬 타입

- SsiftUI는 커스텀 정렬 타입을 선언하여 표준 타입들이 확장될 수 있게 해준다.
- 이 extension은 AlignmentID 프로토콜을 따르는 열거형(enum)을 포함해야 하며, defaultValue() 라는 이름의 함수가 구현되도록 지시한다.

```swift
struct CustomAlignmentView: View {
    var body: some View {
        HStack(alignment: .center) {
            Rectangle()
                .foregroundColor(.green)
                .frame(width: 50, height: 200)
            Rectangle()
                .foregroundColor(.red)
                .frame(width: 50, height: 200)
            Rectangle()
                .foregroundColor(.blue)
                .frame(width: 50, height: 200)
            Rectangle()
                .foregroundColor(.orange)
                .frame(width: 50, height: 200)
        }
        
        HStack(alignment: .oneThird) {
            Rectangle()
                .foregroundColor(.green)
                .frame(width: 50, height: 200)
            Rectangle()
                .foregroundColor(.red)
                .alignmentGuide(.oneThird, computeValue: { d in d[VerticalAlignment.top] })
                .frame(width: 50, height: 200)
            Rectangle()
                .foregroundColor(.blue)
                .frame(width: 50, height: 200)
            Rectangle()
                .foregroundColor(.orange)
                .alignmentGuide(.oneThird, computeValue: { d in d[VerticalAlignment.bottom] })
                .frame(width: 50, height: 200)
        }
    }
}

extension VerticalAlignment {
    private enum OneThird: AlignmentID {
        static func defaultValue(in context: ViewDimensions) -> CGFloat {
            return context.height / 3
        }
    }
    
    static let oneThird = VerticalAlignment(OneThird.self)
}
```

### 29.5 스택 정렬 교차하기

- 일반적으로 UI는 여러 스택이 중첩된다. 표준 정렬 타입의 단점은 스택 내의 뷰가 다른 스택에 있는 뷰와 정렬되도록 하는 방법을 제공하지 않는다.
- 커스텀 정렬을 생성하여 특정 뷰를 기준으로 정렬할 수 있다.

```swift
struct StackCrossAlignView: View {
    var body: some View {
        HStack(alignment: .center) {
            Circle()
                .foregroundColor(.purple)
                .frame(width: 70, height: 70)
            VStack(alignment: .center) {
                Rectangle()
                    .foregroundColor(.green)
                    .frame(width: 70, height: 70)
                Rectangle()
                    .foregroundColor(.red)
                    .frame(width: 70, height: 70)
                Rectangle()
                    .foregroundColor(.blue)
                    .frame(width: 70, height: 70)
                Rectangle()
                    .foregroundColor(.orange)
                    .frame(width: 70, height: 70)
            }
        }
        .padding()

        // 원을 3번 째 박스와 정렬한다.
        // 커스텀 정렬을 이용해서, alignmentGuide 에서, dimension 값을 이용해서 위치를 조정한다.
        HStack(alignment: .crossAlignment) {
            Circle()
                .foregroundColor(.purple)
                .alignmentGuide(.crossAlignment, computeValue: { d in d[VerticalAlignment.center] }) // dimension = bottom ~ circle.center
                .frame(width: 70, height: 70)
            VStack(alignment: .center) {
                Rectangle()
                    .foregroundColor(.green)
                    .frame(width: 70, height: 70)
                Rectangle()
                    .foregroundColor(.red)
                    .frame(width: 70, height: 70)
                Rectangle()
                    .foregroundColor(.blue)
                    .alignmentGuide(.crossAlignment, computeValue: { d in d[VerticalAlignment.center] }) // dimension = bottom ~ rectangle.center
                    .frame(width: 70, height: 70)
                Rectangle()
                    .foregroundColor(.orange)
                    .frame(width: 70, height: 70)
            }
        }
        .padding()
    }
}

extension VerticalAlignment {
    private enum CrossAlignment : AlignmentID {
        static func defaultValue(in context: ViewDimensions) -> CGFloat {
            return context[.bottom]
        }
    }
    
    static let crossAlignment = VerticalAlignment(CrossAlignment.self)
}
```

### 29.6 ZStack 커스텀 정렬

- 기본적으로 ZStack의 하위 뷰는 중앙 정렬된 상태로 위로 겹치게 쌓이게 된다.
- ZStack의 하위 뷰에 대한 커스텀 정렬은 수평 정렬 가이드와 수직 정렬 가이드 모두 필요하다.

```swift
struct ZStackCustomAlignmentView: View {
    var body: some View {
        ZStack(alignment: .myAlignment) {
            Rectangle()
                .foregroundColor(.green)
                .alignmentGuide(HorizontalAlignment.myAlignment, computeValue: { d in d[.trailing] })
                .alignmentGuide(VerticalAlignment.myAlignment, computeValue: { d in d[.bottom] })
                .frame(width: 100, height: 100)
            Rectangle()
                .foregroundColor(.red)
                .alignmentGuide(HorizontalAlignment.myAlignment, computeValue: { d in d[HorizontalAlignment.center] })
                .alignmentGuide(VerticalAlignment.myAlignment, computeValue: { d in d[.top] })
                .frame(width: 100, height: 100)
            Circle()
                .foregroundColor(.orange)
                .alignmentGuide(HorizontalAlignment.myAlignment, computeValue: { d in d[HorizontalAlignment.leading] })
                .alignmentGuide(VerticalAlignment.myAlignment, computeValue: { d in d[.bottom] })
                .frame(width: 100, height: 100)
        }
    }
}

extension HorizontalAlignment {
    enum MyHorizontal: AlignmentID {
        static func defaultValue(in context: ViewDimensions) -> CGFloat {
            return context[HorizontalAlignment.center]
        }
    }
    static let myAlignment = HorizontalAlignment(MyHorizontal.self)
}

extension VerticalAlignment {
    enum MyVertical: AlignmentID {
        static func defaultValue(in context: ViewDimensions) -> CGFloat {
            return context[HorizontalAlignment.center]
        }
    }
    static let myAlignment = VerticalAlignment(MyVertical.self)
}

extension Alignment {
    static let myAlignment = Alignment(horizontal: .myAlignment, vertical: .myAlignment)
}
```

## Chapter 30. SwiftUI List와 내비게이션

- List 뷰는 수직 방향의 목로 형태로 사용자에게 정보를 제공하고, 사용자가 터치 했을 때 다른 영역으로 이동한다.
  이때 NavigationStack 과 NavigationLink 컴포넌트를 사용하여 구현된다.
- `NavigationStack` navigation stack 설정 (iOS 16.0+). 다른 뷰로 이동할 때 원래의 뷰에 대한 참조가 스택에 푸시되고, 네비게이션 바에 뒤로 가는 화살표가 표시된다.
- `NavigationLink` navigation link 영역과 전달 값 설정 (iOS 13.0+)
- `NavigationPath` navigation 을 관리한다. (iOS 16.0+)
- `.navigationDestination` navigation to destination 설정. (iOS 16.0+)
- 리스트는 제목 있는 섹션으로 나눌 수 있으며,
  제목과 버튼을 가지는 내비게이션 바를 가질 수 있다.
  또한, 행의 추가, 삭제, 이동이 가능하도록 리스트를 구성할 수 있다.

### 30.5 NavigationStack과 NavigationLink
```swift
struct ToDoItemView: View {
    @State private var toggleStatus = true
    @State var listData: [ToDoItem] = [
        ToDoItem(task: "Take out trash", imageName: "trash.circle.fill"),
        ToDoItem(task: "Pick up the kids", imageName: "person.2.fill"),
        ToDoItem(task: "Wash the car", imageName: "car.fill")
    ]
    
    var body: some View {
        NavigationStack {
            List {
                Section(header: Text("Settings")) {
                    Toggle(isOn: $toggleStatus) {
                        Text("Allow Notifications")
                    }
                    NavigationLink(value: listData.count) {
                        Text("View Task Count")
                    }
                }
                
                Section(header: Text("To Do Tasks")) {
                    ForEach(listData) { item in
                        NavigationLink(value: item.task) {
                            HStack {
                                Image(systemName: item.imageName)
                                Text(item.task)
                            }
                        }
                    }
                    .onDelete(perform: deleteItem) // delete 버튼 추가
                    .onMove(perform: moveItem) // move 기능 추가
                }
            }
            .navigationTitle("To Do List")
            .navigationBarItems(trailing: Button(action: addTask) {
                Text("Add")
            })
            .navigationBarItems(trailing: EditButton()) // list 편집 버튼 추가. 삭제, 이동 가능.
            .navigationDestination(for: String.self) { task in // navi - String 타입 처리
                Text("Selected task : \(task)")
            }
            .navigationDestination(for: Int.self) { count in // nvgi - Int 타입 처리
                Text("Number of tasks = \(count)")
            }
            .refreshable {
                let tempList: [ToDoItem] = [
                    ToDoItem(task: "Order coffe \(listData.count)", imageName: "cup.and.saucer.fill"),
                ]
                
                listData = listData + tempList // 같은 타입 배열 merge
            }
        }
        
//        List(listData) { item in
//            HStack {
//                Image(systemName: item.imageName)
//                Text(item.task)
//            }
//        }
    }
    
    func addTask() {
        // Add Task 작업 구현
    }
    
    func deleteItem(at offsets: IndexSet) {
        // 데이터 소스에서 항목을 삭제하는 코드
    }
    
    func moveItem(from source: IndexSet, to destination: Int) {
        // 항목을 재배열하는 코드
    }
}


struct ToDoItem : Identifiable {
    var id = UUID()
    var task: String
    var imageName: String
}
```

### 30.7 네비게이션 경로로 작업하기

- 사용자가 이동하는 뷰를 내비게이션 경로(navigation path)라고 한다.
  우리가 만든 경로를 사용하는 NavigationStack을 사용하면, 스택의 여러 내비게이션 레벨을 건너 뛰어 되돌아 갈 수 있도록 대상들을 수동을 제거(pop)하는 등의 작업을 할 수 있다.
- 스택에 있는 내비게이션 대상을 수를 식별하여 인스턴의의 `removeLast()`로 스택을 제거할 수 있다.
- 내비게이션 경로의 `append()` 메서드를 호출하고 대상과 관련된 내비게이션 값을 전달하여 프로그램적으로 특정 대상 뷰로 이동할 수 있다.
```swift
    @State private var stackPath = NavigationPath()

    var stackCount = stackPath.count
    stackPath.removeLast(stackCount)
    // 중략
    stackPath.append(value)
```

### 30.8 내비게이션 바 커스터마이징

- NavigationStack 에 타이틀 바를 설정하고, 부가적인 작업을 수행하는 버튼도 추가할 수 있다.

```swift
    .navigationTitle("To Do List") // title 설정
    .navigationBarItems(trailing: Button(action: addTask) { // Add 버튼 추가
        Text("Add")
    })
```

### 30.10 계층적 목록
-- "34장 List, OutlineGroup, DisclosureGroup 개요" 참조.

### 30.11 멀티컬럼 내비게이션
-- NavigationStack은 각 대상이 전체 디바이스 화면을 차지하는 뷰들 간 이동을 제공한다.
   SwiftUI는 대상이 화면에 표시되면서 별도의 열에 각 대상을 나타내는 멀티컬럼 내비게이션을 지원한다.
   멀티컬럼 내비게이션은 NavigationSplitView 구성 요소에 의해 제공되며 "32장 분할 뷰 내비게이션 개요"를 참조한다.

## Chapter 31. SwiftUI List와 NavigationStack 튜토리얼
-- 예제 프로그램

## Chapter 32. 분할 뷰 내비게이션 개요

- 더 넓은 디스플레이를 활용하기 위해 SwiftUI에서는 멀티컬럼 기반의 내비게이션을 제공하도록 설계된 NavigationSplitView 컴포넌트가 있다. (iOS 16.0+)
- NavigationSplitView는 1) 사이드바, 2) 콘텐트 그리고 3) 데테일 열로 구성된 최대 3개의 열을 지원한다.
- 분할 네비기션의 열 너비와 스타일은 `navigationSplitViewColumnWidht()`와 `navigationSplitViewStyle()` 수정자를 사용하여 구성할 수 있다.
- `NavigationSplitView`의 `columnVisibility` 초기화 매개변수를 사용하여 프로그램적으로 열 가시성을 여러 조합을 구성할 수 있다.

```swift
// 사이드바, 세부사항 뷰
NavigationSplitView {
    // 사이드바 목록
} detail: {
    // 세부사항 뷰
}

// 사이트바, 콘텐트 목록, 디테일 뷰
NavigationSplitView {
    // 사이드바 목록
} content: {
    // 콘텐트 목록
} detail: {
    // 디테일 뷰
}
```

## Chapter 33. NavigrationSplitView 튜토리얼
-- NavigationSplitview 예제 프로그램

```swift
struct ContentView: View {
    @State private var categories = [
        IconCategory(categoryName: "Folders", images: ["questionmark.folder.ar",
                                                       "questionmark.folder",
                                                       "questionmark.folder.fill.ar",
                                                       "folder.fill.badge.gear",
                                                       "questionmark.folder.fill"
                                                      ]),
        IconCategory(categoryName: "Circles", images: ["book.circle",
                                                       "books.vertical.circle",
                                                       "books.vertical.circle.fill",
                                                       "book.circle.fill",
                                                       "book.closed.circle"
                                                      ]),
        IconCategory(categoryName: "Clouds", images: ["cloud.rain",
                                                      "cloud",
                                                      "cloud.drizzle.fill",
                                                      "cloud.fill",
                                                      "cloud.drizzle"
                                                     ])
    ]
    
    @State private var selectedCategory: IconCategory?
    @State private var selectedImage: String?
    @State private var columnVisibility = NavigationSplitViewVisibility.all
    
    var body: some View {
        NavigationSplitView(columnVisibility: $columnVisibility) {
            List(categories, selection: $selectedCategory) { Category in
                Text(Category.categoryName).tag(Category)
            }
        } content: {
            if let selectedCategory {
                List(selectedCategory.images, id: \.self,
                     selection: $selectedImage) { image in
                    HStack {
                        Image(systemName: image)
                        Text(image)
                    }.tag(image)
                }
            } else {
                Text("Select a category")
            }
        } detail: {
            if let selectedImage {
                Image(systemName: selectedImage)
                    .resizable()
                    .aspectRatio(contentMode: .fit)
                    .padding()
            } else {
                Text("Select an image")
            }
        }
        .navigationSplitViewStyle(.balanced)
    }
}
```

## Chapter 34. List, OutlineGroup, DisclosureGroup 개요

- List 생성에 `children` 파라미터를 정의하면 계층 데이터를 표시할 수 있다. 
- Section과 OutLineGroup 뷰를 사용하여 각각 **섹션** 헤더가 있는 그룹으로 나눈다.
  + OutLineGroup에서 Section 하위의 계측 데이터를 표시한다.
- DisclosureGroup 컨트롤을 사용하여 그룹내의 뷰를 확장/축소 할 수 있다.

## Chapter 35. SwiftUI List, OutLineGroup, DisclosureGroup 튜토리얼
-- 예제 프로그램

## Chapter 36. LazyVGrid 및 LazyHGrid로 SwiftUI 그리드 구축하기

- SwiftUI는 UI 레이아웃에서 멀티컬럼 그리드(multi-column grid)를 표시할 수 있는 LazyVGrid, LazyHGrid, GridItem 세 가지 뷰를 제공한다.

### 36.2 GridItem

- GridItem 인스턴스는 각 행이나 열을 나타낸다. GridItem 뷰는 크기조정, 가격, 정렬 측면에서 행 또는 열의 속성을 정의한다.
  또한 그리드 내에 표시되는 행 또는 열의 수와 이러한 제약 조건을 충족하기 위해 항목을 축소할 수 있는 최소 크기에 대한 제어도 제공한다.
- `GridItem(sizing, spacing: CGFloat?, alignment: <alignment>)`
  + sizing:
    + flexible() : 그리드의 행 또는 열 수는 그리드 뷰에 배열 형태로 전달된 GridItem 인스턴스 수에 따라 결정된다.
    + adaptive(minnum: CGFloat): 사용 가능한 공간에 가능한 많은 항목을 맞도록 조정된다. 축소될 수 있는 최소크기 minimum 인수를 선택사항으로 사용.
    + fixed(size: CGFloat): 고정된 크기를 지정한다. 행 또는 열 수는 배열 행태로 전달될 GridItem 인스턴스 수에 따라 결정된다.

### 36.6 적응형 GridItem으로 작업하기

- 적응형(adaptive) 설정은 뷰가 차지하는 공간에 맞출 수 있는 한 많은 행이나 열이 자동으로 표시되도록 그리드 뷰를 구성한다.
- 적응형 크기 조정을 사용하려면 아래와 같이 단일 적응형 항목을 포함하도록 gridItems 배열을 수정한다.
```swift
private var gridItems = [GridItem(.adaptive(minimum: 50))]
```

- LazyVGrid Demo
```swift
struct ContentView: View {
    private var colors: [Color] = [.blue, .yellow, .green]
    // flexible. 유연한 GridItem 크기를 위한 그리드 뷰
//    private var gridItems = [GridItem(.flexible()), GridItem(.flexible()), GridItem(.flexible())]

    // adaptive
//    private var gridItems = [GridItem(.adaptive(minimum: 50))]
    
    // fixed
//    private var gridItems = [GridItem(.fixed(75)), GridItem(.fixed(125)), GridItem(.fixed(175))]

    // mixed
//    private var gridItems = [GridItem(.fixed(75)), GridItem(), GridItem()]
    private var gridItems = [GridItem(.fixed(100)), GridItem(.adaptive(minimum: 50))]

    var body: some View {
        ScrollView {
            LazyVGrid(columns: gridItems, spacing: 5) {
                ForEach((0...99), id: \.self) { index in
                    CellContent(index: index, color: colors[index % colors.count])
                }
            }
            .padding()
        }
    }
}

struct CellContent: View {
    var index: Int
    var color: Color
    
    var body: some View {
        Text("\(index)")
            .frame(minWidth: 50, maxWidth: .infinity, minHeight: 100)
            .background(color)
            .cornerRadius(8)
            .font(.system(.largeTitle))
    }
}
```

- LazyHGrid Demo
```swift
struct HGridView: View {
    private var colors: [Color] = [.blue, .yellow, .green]
    // mixed
//    private var gridItems = [GridItem(.fixed(75)), GridItem(), GridItem()]
//    private var gridItems = [GridItem(.fixed(150)), GridItem(.adaptive(minimum: 50)), GridItem(.fixed(150))]
    private var gridItems = [GridItem(.fixed(150)), GridItem(.flexible(minimum: 50)), GridItem(.fixed(150))]

    var body: some View {
        ScrollView(.horizontal) {
            LazyHGrid(rows: gridItems, spacing: 5) {
                ForEach((0...99), id: \.self) { index in
                    HCellContent(index: index, color: colors[index % colors.count])
                }
            }
            .padding()
        }
    }
}

struct HCellContent: View {
    var index: Int
    var color: Color
    
    var body: some View {
        Text("\(index)")
            .frame(minWidth: 75, minHeight: 50, maxHeight: .infinity)
            .background(color)
            .cornerRadius(8)
            .font(.system(.largeTitle))
    }
}
```

## Chapter 37. Grid와 GridRow를 사용하여 SwiftUI 그리드 구축하기

- iOS 16에 도입된 `Grid`와 `GridRow`는 많은 수의 뷰를 포함하는 스크롤 그리드를 표시하는데 적합하지 않지만,
   열을 단일 셀에 두는 기능, 빈 셀 지원, 그리드행 정렬, 개별 셀 정렬 기능이 있다.

```swift
struct ContentView: View {
    var body: some View {
        Grid(horizontalSpacing: 10, verticalSpacing: 10) {
            GridRow {
                ForEach(1...5, id: \.self) { index in
                    if (index % 2 == 1) {
                        CellContent(index: index, color: .red)
                    } else {
                        Color.clear.gridCellUnsizedAxes([.horizontal, .vertical]) //  빈셀 Color.clear 뷰 설정. gridCellUnsizedAxes 는 높이, 너비 설정.
                    }
                }
            }
            
            GridRow {
                ForEach(6...8, id: \.self) { index in
                    CellContent(index: index, color: .blue)
                }
            }
            
            GridRow {
                ForEach(11...12, id: \.self) { index in
                    CellContent(index: index, color: .green)
                }
            }
            
            CellContent(index:16, color: .blue)
            GridRow {
                CellContent(index: 17, color: .orange)
                    .gridCellColumns(2)
                CellContent(index: 18, color: .indigo)
                    .gridCellColumns(3)
            }
        }
        .padding()
    }
}

struct CellContent: View {
    var index: Int
    var color: Color
    
    var body: some View {
        Text("\(index)")
            .frame(minWidth: 50, maxWidth: .infinity, minHeight: 100)
            .background(color)
            .cornerRadius(8)
            .font(.largeTitle)
    }
}
```

-- 정렬 샘플
```swift
struct AlignmentView: View {
    var body: some View {
        Grid(alignment: .topLeading) {
            GridRow(alignment: .bottom) {
                CellContent(index: 0, color: .orange)
                Image(systemName: "record.circle.fill")
                    .gridColumnAlignment(.trailing) // 열의 정렬 설정. 전체 열에 적용됨.
                Image(systemName: "record.circle.fill")
                    .gridCellAnchor(.center) // 개별 셀에 적용됨.
                Image(systemName: "record.circle.fill")
                    .gridCellAnchor(.top)
                CellContent(index: 0, color: .yellow)
            }
            .font(.largeTitle)

            GridRow {
                CellContent(index: 0, color: .orange)
                Image(systemName: "record.circle.fill")
                Image(systemName: "record.circle.fill")
                Image(systemName: "record.circle.fill")
                CellContent(index: 0, color: .yellow)
            }
            .font(.largeTitle)

            GridRow {
                ForEach(1...5, id: \.self) { index in
                    CellContent(index: index, color: .red)
                }
            }
        }
        .padding()
    }
}
```
### 37.7 열 확장하기

- grid와 GridRow 의 주용 기능은 단일 셀이 지정된 수의 열에 놓일 수 있게 한다.(**열을 병합한다.**) `gridCellColumns()` 수정자 사용.

## Chapter 38. SwiftUI에서 탭 그리고 페이지 뷰 구축하기

### 38.1 SwiftUI TabView 개요

- 디폴트로 TabView는 하위 뷰들 사이를 이동하는데 사용될 탭 아이템을 가진 탭 바를 레이아웃 하단에 표시한다.
- 탭 아이템은 수정자를 사용하여 각각의 콘텐트 뷰에 적용되며, Text 뷰와 Image 뷰로 구성할 수 있다.
- 탭 아이템에 태그를 추가하면 프로그램적으로 현재 선택된 탭을 제어할 수 있다.

```swift
struct ContentView: View {
    @State private var selection = 1
    
    var body: some View {
        TabView(selection: $selection) {
            Text("First Content View : \(selection)")
                .tabItem {
                    Image(systemName: "1.circle")
                    Text("Screen One")
                }.tag(1)
            Text("Second Content View : \(selection)")
                .tabItem {
                    Image(systemName: "2.circle")
                    Text("Screen Two")
                }.tag(2)
            Text("Third Content View : \(selection)")
                .tabItem {
                    Image(systemName: "3.circle")
                    Text("Screen Three")
                }.tag(3)
        }
        .font(.largeTitle)
//        .tabViewStyle(PageTabViewStyle()) // PageTabViewStyle() : 뷰를 왼쪽/오른쪽을 스와이프하며 이동한다.
    }
}
```

## Chapter 39. SwiftUI에서 콘텍스트 메뉴 바인딩하기

- SwiftUI에서 콘텍스트 메뉴(context menu)는 사용자가 뷰를 롱 프레스를 했을 때 나타나는 메뉴다. (mac은 마우스 우측 클릭)
  각 메뉴 항목은 일반적으로 Text 뷰 그리고 선택사항인 Image 뷰와 함께, 선택했을 때 동작을 수행하도록 구성된 button 뷰를 포함한다.

```swift
struct ContentView: View {
    @State private var foregroundColor: Color = Color.black
    @State private var backgroundColor: Color = Color.white
    
    var body: some View {
        Text("Hello, world!")
            .padding()
            .font(.largeTitle)
            .foregroundColor(foregroundColor)
            .background(backgroundColor)
            .contextMenu{
                Button(action:  {
                    self.foregroundColor = .black
                    self.backgroundColor = .white
                }) {
                    Text("Normal Colors")
                    Image(systemName: "paintbrush")
                }
                
                Button(action: {
                    self.foregroundColor = .white
                    self.backgroundColor = .black
                }) {
                    Text("Inverted Colors")
                    Image(systemName: "paintbrush.fill")
                }
            }
    }
}
```

## Chapter 40. SwiftUI 그래픽 드로잉 기초

- SwiftUI는 내장된 도형과 그레이디언트 드로잉 뿐만 아니라, Shape 프로토콜과 Path 프로토콜을 따르는 완전히 새로운 뷰를 생성하여 커스텀 드로잉을 할 수 있게도 한다.

### 40.2 SwiftUI 도형

- 기본적으로 도형은 도형이 속한 뷰에서 사용할 수 있는 모든 공간을 차지하고, 부모 뷰의 포그라운드 색상으로 채운다.
- 도형의 색상과 크기는 `fill()` 수정자와 `frame()` 수정자로 설정한다.
- `stroke()` 는 색을 채우지 않고 테두리만 설정한다.
- fill 수정자와 stroke 수정자를 결합할 수 없다. 하지만, overlay()를 이용하여 색을 채운 도형위에, 외곽선 도형을 그릴 수 있다.

```swift
struct ContentView: View {
    var body: some View {
        Capsule()
            .stroke(lineWidth: 10)
            .fill(.red)
            .frame(width: 200, height: 100)
        
        RoundedRectangle(cornerRadius: 20)
            .stroke(style: StrokeStyle(lineWidth: 8, dash: [10]))
            .foregroundColor(.blue)
            .frame(width: 200, height: 100)
        
        Ellipse()
            .stroke(style: StrokeStyle(lineWidth: 20,
                                       dash: [10,5,2],
                                      dashPhase: 10))
            .foregroundColor(.blue)
            .frame(width: 200, height: 150)

        Ellipse()
            .fill()
            .overlay(Ellipse() // overlay를 이용해서 색을 채원 도형위에, stroke 도형을 올린다.
                .stroke(.blue, lineWidth: 10))
            .frame(width: 200, height: 150)
        
        MyShape()
            .fill(.green)
            .frame(width: 200, height: 150)
    }
}

struct MyShape: Shape {
    func path(in rect: CGRect) -> Path {
        var path = Path()
        path.move(to: CGPoint(x: rect.minX, y: rect.minY))
        path.addQuadCurve(to: CGPoint(x: rect.minX, y: rect.maxY),
                          control: CGPoint(x: rect.midX, y: rect.midY))
        path.addLine(to: CGPoint(x: rect.minX, y: rect.maxY))
        path.addLine(to: CGPoint(x: rect.maxX, y: rect.maxY))
        path.closeSubpath()
        return path
    }
}
```
### 40.4 커스텀 경로와 도형 그리기

- 지금까지 사용된 도형은 기본적으로 `Shape` 프로토콜을 따르는 구조체 객체다.
  Shape 프로토콜을 따르기 위해 구조체는 `CGRect` 형태의 사각형을 받아 그 사각형에 그려질 것을 정의하는 `Path` 객체를 반환하는 `path()` 함수를 구현해야 한다.
- `path` 인스턴스는 포인트 간의 좌표를 지정하고 그려질 선을 정의하여 2 차원 도형을 제공한다.
   포인트 간의 선은 직선, 3차 및 2차 베지어 곡선, 호, 타원 그리고 사각형을 사용하여 그릴 수 있다.
- path정보: https://developer.apple.com/documentation/swiftui/path

```swift
struct GradientView: View {
    let colors = Gradient(colors: [Color.red,
                                   Color.yellow,
                                   Color.green,
                                   Color.blue,
                                   Color.purple])
    var body: some View {
        Grid {
            GridRow {
                Circle()
                    .fill(.blue.gradient)
                    .frame(width: 120, height: 120)
                Circle()
                    .fill(.blue.shadow(.drop(color: .black, radius: 10))) // drop shadow
                    .frame(width: 120, height: 120)
            }
            GridRow {
                Circle()
                    .fill(.blue.shadow(.inner(color: .white, radius: 15))) // inner shadow
                    .frame(width: 120, height: 120)
            }
            GridRow {
                Circle()
                    .fill(RadialGradient(gradient: colors,
                                         center: .center,
                                         startRadius: 0,
                                         endRadius: 60))
                    .frame(width: 120, height: 120)
                Circle()
                    .fill(AngularGradient(gradient: colors, center: /*@START_MENU_TOKEN@*/.center/*@END_MENU_TOKEN@*/))
                    .frame(width: 120, height: 120)
            }
            GridRow {
                Rectangle()
                    .fill(LinearGradient(gradient: colors, startPoint: .topLeading, endPoint: .bottomTrailing))
                    .frame(width: 120, height: 120)
                MyShape()
                    .fill(RadialGradient(gradient: colors,
                                         center: .center,
                                         startRadius: 0,
                                         endRadius: 60))
                    .background(LinearGradient(gradient: Gradient(colors: [Color.yellow, Color.brown]), // background 추가
                                               startPoint: .topLeading,
                                               endPoint: .bottomTrailing))
                    .frame(width: 120, height: 120)
            }
        }
    }
}
```

## Chapter 41. SwiftUI 애니메이션과 전환

- 이번 장은 **뷰를 애니메이션**하는 것과 SwiftUI 앱 내에서 **전환**에 대해서 설명한다.
- 애니메이션은 화면상의 뷰 회전, 확대 그리고 동작 등의 다양한 형태를 취한다.
- 전환은 레이아웃에서 뷰가 추가되거나 제거될 때 뷰가 어떻게 나타나고 사라질지를 정의한다.

### 41.2 암묵적 애니메이션 (implicit animation)

1. `animation()` 수정자를 사용하여, 애니메이션 수정자 앞에 있는 모든 수정자를 암묵적으로 애니메이션되도록 한다.
2. animation 커브
- .linear : 지정된 시간 동안 일정한 속도로 애니메이션을 수행한다.
- .easeOut : 빠른 속도로 시작하여 끝에 다다를수록 점점 느려진다.
- .easeIn : 느린 속도로 시작하여 끝에 다다를수록 점점 빨라진다.
- .easeInOut: 느린 속도록 시작하여 점점속도를 올리다가 끝에 다시 느려진다.

```swift
struct ContentView: View {
    @State private var rotation: Double = 0
    @State private var scale: CGFloat = 1
    
    var body: some View {
        Button(action: {
            self.rotation = (self.rotation < 360 ? self.rotation + 60: 0)
            self.scale = (self.scale < 2.8 ? self.scale + 0.3 : 1)
        }, label: {
            Text("Click to animate")
                .rotationEffect(.degrees(rotation))
                .scaleEffect(scale)
                .animation(.easeInOut(duration: 1), value: rotation)
//                .animation(.spring(response: 1, dampingFraction: 0.2, blendDuration: 0), value: rotation) // 스프링 효과
//                .animation(Animation.linear(duration: 0.2).repeatCount(2, autoreverses: false), value: rotation) // 애니메이션 반복
//                .animation(Animation.linear(duration: 1).repeatForever(autoreverses: true), value: rotation) // 애니메이션 무한 반복
//                .scaleEffect(scale) // scaleEffect을 애니메이션 뒤에 정의하면 회전에는 animation 이 적용되지 않는다.
        })
    }
}
```

### 41.4 명시적 애니메이션 (explicit animation)

- SwiftUI는 withAnimation() 클로저를 사용하여 구현되는 명시적 애니메이션 방법도 제공한다.
- `withAnimation()` 클로저 내에서 변경된 프로퍼티만 애니메이션 된다. 
   명시적 애니메이션을 사용하면 수정자(회전효과, 등)의 순서에 무관하게 지정 프로퍼티에 애니메이션이 적용된다.  
```swift
    @State private var redCircle = false

    Circle()
        .fill(redCircle ? .red : .blue)
        .frame(width: 200, height: 200)
        .onTapGesture {
            withAnimation {
                redCircle.toggle() // 변경에 애니메이션 효과 설정
            }
        }
```
### 41.5 애니메이션과 상태 바인딩

- 상태 값 변경의 결과로 인한 뷰의 변화가 애니메이션되도록 상태 프로퍼티 바인딩에 애니메이션을 적용할 수도 있다.
```swift
    @State private var visibility = false

    VStack {
        Toggle(isOn: $visibility.animation(.linear(duration: 1))) { // 상태에 애니메이션 바인딩 설정
            Text("Toggle Text View")
        }
        .padding()
        
        if visibility {
            Text("Hello World")
                .font(.largeTitle)
        } else {
            Text("Goodbye World")
                .font(.largeTitle)
        }
    }
```

### 41.6 자동으로 애니메이션 시작하기

```swift
struct StartAnimationView: View {
    @State private var rotation: Double = 0
    @State private var isSpinning: Bool = true
    
    var body: some View {
        ZStack {
            Circle()
                .stroke(lineWidth: 2)
                .foregroundColor(.blue)
                .frame(width: 360, height: 360)
            
            Image(systemName: "forward.fill")
                .font(.largeTitle)
                .offset(y:-180)
                .rotationEffect(.degrees(rotation))
                .animation(Animation.linear(duration: 5).repeatForever(autoreverses: false), value: rotation)
        }
        .onAppear() {
            self.isSpinning.toggle()
            rotation = isSpinning ? 0 : 360
        }
    }
}
```

### 41.7 SwiftUI 전환

1. `transition()` 수정자 효과
- .slide - 뷰가 옆으로 슬라이딩 하면 나가거나 들어온다.
- .scale - 뷰가 작아지면서 사라지고 커지면서 나타난다.
- .move(edge: edge) - 지정 방향으로 추가/제거된다.
- .opacity - 기본 전환 효과로 페이드 되는 동안 크기와 위치를 유지한다.

### 41.8 전환 결합하기

- `AnyTransition` 의 인스턴스를 `combined(with:)` 메서드와 함께 사용하면 전환을 결합할 수 있다.
```swift
struct TransitionView: View {
    @State private var isButtonVisible: Bool = true
    
    var body: some View {
        VStack {
            Toggle(isOn: $isButtonVisible.animation(.linear(duration: 2))) {
                Text("Show/Hide Button")
            }
            .padding()
            
            if isButtonVisible {
                Button(action: {}) {
                    Text("Example Button")
                }
                .font(.largeTitle)
//                .transition(.slide) // 정의하지 않으면 .opacity 기본 효과가 적용된다.
//                .transition(AnyTransition.opacity.combined(with: .move(edge: .top))) // 전환결합하기
//                .transition(.fadeAndMove) // 익스텐션 전환 사용하기
                .transition(.asymmetric(insertion: .scale, removal: .fadeAndMove)) // 비대칭 전환
            }
        }
        Spacer()
    }
}

extension AnyTransition {
    static var fadeAndMove: AnyTransition { // 익스텐션으로 전환 추가하기
        AnyTransition.opacity.combined(with: .move(edge: .bottom))
    }
}
```

## Chapter 42. SwiftUI에서 제스처 작업하기

### 42.2 기본 제스처
- 제스터라는 용어는 터치 스크린과 사용자 간의 인터랙션을 설명하는 데 사용되며, 앱 내에서 이를 감지하여 이벤트를 실행한다.
- 드래그, 탭, 더블 탭, 핀칭, 로테이션, 롱 프레스 등은 모두 SwiftUI에서 제스처로 분류한다.
- `gesture()` 수정자에 `nil` 값을 전달하면 제스처 인식기를 뷰에서 제거할 수 있다.

```swift
struct ContentView: View {
    var body: some View {
        let tap = TapGesture(count: 2) // 인식 탭수 설정
                    .onEnded { _ in
                        print("Tapped")
                    }
        let longPress = LongPressGesture(minimumDuration: 5, maximumDistance: 25) // 시간 및 접촉유효거리 설정
            .onEnded { _ in
                print("Long Press")
            }

        Image(systemName: "hand.point.right.fill")
            .gesture(tap)
            .gesture(longPress)
        
    }
}
```

### 42.3 onChanged 액션 콜백

- TapGesture 를 제외한 다른 제스처 인식기는 `onChanged` 액션 콜백을 지원한다.
  onChnaged 콜백은 제스처가 처음 인식되었을 때 호출되며, 제스처가 끝날 때까지 제스처의 값이 변할 때마다 호출된다.

### 42.4 updating 콜백 액션

1. updaing 콜백 액션은 onChanged 와 거의 비슷하나, @GestureState 라는 특별한 프로퍼티 래퍼를 사용한다.
2. @GestureState 는 표준 @State 프로퍼티와 유사하지만, 제스처와 함께 사용되도록 설계됐다.
   @GestureState 는 제스처가 끝나면 자동으로 원래 상태값이 리셋된다. updating 콜백은 제스처를 하는 동안에만 필요한 임시 상태를 저장하는 데 최적이다.
3. updating 액션이 호출 될 때 아래 세가지 인자가 전달된다.
- 제스처 정보가 담겨 있는 DragGesture.Value 인스턴스
- 제스처가 바인딩되어 있는 @GestureState 프로퍼티 참조체
- 제스처에 해다하는 애니메이션의 현재 상태를 담고 있는 Transaction 객체
4. DragGesture.Value 프로퍼티
- .locaton (CGPoint) : 드레그 제스처 현재 위치
- .predictedEndLocation (CGPoint) : 현재 드래그 속도를 바탕으로 드래그를 멈추게 되다면 예상되는 최종 위치
- .predictedEndTranslation (CGSize) : 현재의 드래그 속도를 바탕으로 드래그를 멈추게 된다면 예상되는 최종 오프셋
- .startLocation (CGPoint) : 드래그 제스처가 시작된 위치
- .time (Date) : 현재 드래그 이벤트가 발생한 타임 스탬프
- .translation (CGSize) : 드래그 제스처를 시작한 위치부터 현재 위치까지의 총 오프셋

```swift
struct ContentView: View {
    @State private var magnification: CGFloat = 1.0
    @GestureState private var offset: CGSize = .zero
    
    var body: some View {
        let tap = TapGesture(count: 2) // 1) 탭. 인식 탭수 설정
                    .onEnded { _ in
                        print("Tapped")
                    }
        let longPress = LongPressGesture(minimumDuration: 3, maximumDistance: 25) // 2) 롱프레스. 시간 및 접촉유효거리 설정
            .onEnded { _ in
                print("Long Press")
            }
        
        let magnificationGesture = MagnifyGesture(minimumScaleDelta: 0) // 3) 핀칭(pinching).
            .onChanged{ value in
                if value.magnification < 1.0 {
                    self.magnification = 1.0
                } else if value.magnification > 5.0 {
                    self.magnification = 5.0
                } else {
                    self.magnification = value.magnification
                }
            }
            .onEnded { _ in
                print("Gesture Ended")
            }
        
        let drag = DragGesture() // 4) 드래그. 4분위에서, 좌측(-X), 우측(+X), 위(-Y), 아래(+Y)
            .updating($offset) { dragValue, state, Transaction in
                state = dragValue.translation
                //.location, .predictedEndLocation, .predictedEndTranslation, .startLocation, .time, .translation
            }
        

        Image(systemName: "hand.point.right.fill")
            .resizable()
            .font(.largeTitle)
            .offset(offset) // drag offset 전달하여, 드래그되게 한다.
            .scaleEffect(magnification)
            .frame(width: 100, height: 100)
            .gesture(tap)                  // 1) 탭
            .gesture(drag)                 // 4) 드레그
            .gesture(longPress)            // 2) 롱프레스
            .gesture(magnificationGesture) // 3) 핀칭
    }
}
```

### 42.5 제스처 구성하기

- 하나의 뷰에 여러 개의 제스처를 결합하여 적용할 수 있다.
- `simultaneously` 수정자를 사용하면 구성되면 두 개의 제스처가 동시에 수행된다.
- `sequenced` 수정자를 사용하면 두 번째 제스처가 감지되기 전에 첫 번째 제스처가 완료되어야 한다.
- `exclusively` 수정자를 사용하면 둘 중 하나의 제스처가 감지되면 감지된 것으로 간주한다.

```swift
// 두가지 제스처를 동시에 처리
struct GestureMixedView: View {
    @GestureState private var offset: CGSize = .zero
    @GestureState private var longPress: Bool = false
    
    var body: some View {
        let longPressAndDrag = LongPressGesture(minimumDuration: 2.0)
            .updating($longPress) { value, state, transition in
                state = value
                print("long press \(longPress)")
            }
            .simultaneously(with: DragGesture())
            .updating($offset) { value, state, transaction in
                state = value.second? .translation ?? .zero
            }
        
        Image(systemName: "hand.point.right.fill")
            .foregroundColor(longPress ?  .red : .blue)
            .font(.largeTitle)
            .offset(offset)
            .gesture(longPressAndDrag)
    }
}
```

```swift
// long press 2 초 후에, 드래그 가능
struct SequencedGestureView: View {
    @GestureState private var offset: CGSize = .zero
    @State private var dragEnabled: Bool = false
    
    var body: some View {
        let longPressBeforeDrag = LongPressGesture(minimumDuration: 2.0)
            .onEnded({ _ in
                self.dragEnabled = true
            })
            .sequenced(before: DragGesture())
            .updating($offset) { value, state, transaction in
                switch value {
                case .first(true):
                    print("Long press is progress")
                case .second(true, let drag):
                    state = drag? .translation ?? .zero
                default: break
                }
            }
            .onEnded { value in
                self.dragEnabled = false
            }
        
        Image(systemName: "hand.point.right.fill")
            .foregroundColor(dragEnabled ? .green : .blue)
            .font(.largeTitle)
            .offset(offset)
            .gesture(longPressBeforeDrag)
    }
}
```

## Chapter 43. 사용자 정의 SwiftUI ProgressView 생성하기

- 이번 장은 사용자 정의 프로그레스 뷰를 생성하여 선형, 원형, 불확정적인 스타일을 포함하여 ProgressView 기반의 인터페이스 구현한다.

### 43.1 ProgressView 스타일

- ProgressView 는 세 가지 스타일로 표시할 수 있다. 수평선, 원형, 회전 애니메이션.
- 회전 애니메이션(불확정적인 스타일)은 얼만큼 완료되었는지 퍼센트를 알 수 없는 경우에 작업이 진행되고 있음을 표시하는데 유용하다.
- ProgressViewStyle 프로토콜을 채택함으로써 복잡한 사용자 정의 프로그레스 뷰를 구현할 수 있다.

```swift
struct ContentView: View {
    @State private var progress: Double = 1.0
    
    var body: some View {
        VStack {
            
            ProgressView("Task 1 Progress", value: progress, total: 100)
                .progressViewStyle(LinearProgressViewStyle(tint: .red)) // 선형
            
            ProgressView("Task 2 Progress", value: progress, total: 100)
                .progressViewStyle(CircularProgressViewStyle()) // 원형

            ProgressView()             // 불확정적인 ProcessView
            ProgressView("Working...") // 불확정적인 ProcessView + Text

            ProgressView("Task 5 Progress", value: progress, total: 100)
                .progressViewStyle(MyCustomProgressViewStyle())     // 커스텀스타일1

            ProgressView("Task 6 Progress", value: progress, total: 100)
                .progressViewStyle(MyCustomProgressTextViewStyle()) // 커스텀스타일2

            ProgressView("Task 5 Progress", value: progress, total: 100)
                .progressViewStyle(MyCustomProgressCircleViewStyle()) // 커스텀스타일3

            Slider(value: $progress, in:1...100, step: 0.1)
        }
        .padding()

        VStack {
            ProgressView("Task 1 Progress", value: progress, total: 100)
            ProgressView("Task 2 Progress", value: progress, total: 100)
            ProgressView("Task 3 Progress", value: progress, total: 100)
        }
        .progressViewStyle(CircularProgressViewStyle()) // 뷰 컨테이너에 적용해, 자식 ProgressView에 모두 적용
        .padding()
    }
}

struct MyCustomProgressViewStyle: ProgressViewStyle {
    func makeBody(configuration: Configuration) -> some View {
        ProgressView(configuration)
            .accentColor(.red)
            .shadow(color: Color(red: 0, green: 0.7, blue: 0), radius: 5.0, x: 2.0, y: 2.0)
            .progressViewStyle(LinearProgressViewStyle())
    }
}

struct MyCustomProgressTextViewStyle: ProgressViewStyle {
    func makeBody(configuration: Configuration) -> some View {
        let percent = Int(configuration.fractionCompleted! * 100)
        return Text("Task \(percent)% Completed")
    }
}

struct MyCustomProgressCircleViewStyle: ProgressViewStyle {
    func makeBody(configuration: Configuration) -> some View {
        let degress = configuration.fractionCompleted! * 360
        let percent = Int(configuration.fractionCompleted! * 100)
        return VStack {
            MyCircle(startAngle: .degrees(1), endAngle: .degrees(degress))
                .frame(width: 100, height: 100)
                .padding(50)
            Text("Task \(percent)% Completed")
        }
    }
}

struct MyCircle: Shape {
    var startAngle: Angle
    var endAngle: Angle
    
    func path(in rect: CGRect) -> Path {
        var path = Path()
        path.addArc(center: CGPoint(x: rect.midX, y: rect.midY),
                    radius: rect.width / 2,
                    startAngle: endAngle,
                    endAngle: startAngle,
                    clockwise: true)
        return path.strokedPath(.init(lineWidth: 100, dash: [5, 3], dashPhase: 10))
    }
}
```
## Chapter 44. SwiftUI 차트로 데이터 표시하기

1. SwiftUI Charts 는 데이터를 시각적으로 표시할 수 있게 하는 뷰와 수정자로 구성된다.
2. API는 area, line, point, rectangle, bar, stacked bar 그래프 형태를 지원한다.
3. Chart 내 각 데이터 포인트는 Mark 뷰의 형태를 취한다. 아래는 지원 Mark 뷰 목록.
- AreaMark
- LineMark
- RectangleMark
- BarMark
- PointMark
- RuleMark
4. 각 값은 PlottableValue 클래스의 인스턴스로 표현된다.

### 44.6 보간법 변경하기

1. 보간법(interpolation)은 그래프에서 데이터 포인트를 연결하기 위햇 선을 그리는 방법을 말한다.
2. 보간법은 `interpolationMethod()` 수정자에 마크 선언을 적용하여 변경할 수 있다. 아래를 보간 옵션.
- linear : 기본 보간법
- cardinal : 곡선
- catmullRom : 곡선
- monotone : 곡선
- stepStart : 마크 위/아래에서 옆으로 연결
- stepEnd : 마크 옆에서 위/아래로 연결
- stepCenter: 마크 옆에서 옆으로 연결

```swift
import SwiftUI
import Charts // Charts 라이브러리를 import 한다.

struct ContentView: View {
    let tempData: [MonthlyTemp] = [
        MonthlyTemp(month: "Jan", degrees: 50, year: "2021"),
        MonthlyTemp(month: "Feb", degrees: 43, year: "2021"),
        MonthlyTemp(month: "mar", degrees: 61, year: "2021"),
        MonthlyTemp(month: "Jan", degrees: 30, year: "2022"),
        MonthlyTemp(month: "Feb", degrees: 38, year: "2022"),
        MonthlyTemp(month: "mar", degrees: 29, year: "2022"),
    ]
    
    var body: some View {
//        Chart {
//            AreaMark(x: PlottableValue.value("Month", "Jan"), y: PlottableValue.value("Temp", 50))
//            AreaMark(x: .value("Month", "Feb"), y: .value("Temp", 43)) // PlottableValue 생략가능
//            AreaMark(x: .value("Month", "Mar"), y: .value("Temp", 61))
//        }
                
//        Chart {
//            ForEach(tempData) { data in // ForEach 문을 이용한 표현
//                AreaMark(x: .value("Month", data.month), y: .value("Temp", data.degrees))
//            }
//        }
        
        Chart(tempData) { data in
            AreaMark(x: .value("Month", data.month), y: .value("Temp", data.degrees))
                .foregroundStyle(by: .value("Year", data.year))
        }
        .padding()

        Chart(tempData) { data in // Mark 결합하기. Rectangle + Line
            RectangleMark(x: .value("Month", data.month), y: .value("Temp", data.degrees))
                .foregroundStyle(by: .value("Year", data.year)) // 필터링. 연도별로 데이터를 구분하도록 함.
            LineMark(x: .value("Month", data.month), y: .value("Temp", data.degrees))
                .interpolationMethod(.catmullRom)
                .foregroundStyle(by: .value("Year", data.year))
        }
        .chartPlotStyle { plotArea in
            plotArea
                .background(.gray.opacity(0.3))
        }
        .padding()
    }
}

struct MonthlyTemp: Identifiable {
    var id = UUID()
    var month: String
    var degrees: Int
    var year: String
}
```

## Chapter 45. SwiftUI 차트 튜토리얼

-- 예제 프로그램 작성
```swift
import SwiftUI
import Charts

struct ContentView: View {
    let sales = [(channel: "Retail", data: retailSales),
                 (channel: "Online", data: onlineSales)]
    
    var body: some View {
        Chart {
            ForEach(sales, id: \.channel) { channels in
                ForEach(channels.data) { sales in
                    PointMark(x: .value("Month", sales.month), y: .value("Total", sales.total))
                        .foregroundStyle(by: .value("Channel", channels.channel))
                }
            }
        }
        .frame(height: 250)
        .padding()
    }
}

struct SalesInfo: Identifiable {
    var id = UUID()
    var month: String
    var total: Int
}

var retailSales: [SalesInfo] = [
    .init(month: "Jan", total: 5),
    .init(month: "Feb", total: 7),
    .init(month: "March", total: 6),
    .init(month: "April", total: 5),
    .init(month: "May", total: 6),
    .init(month: "June", total: 3),
    .init(month: "July", total: 6)
]

var onlineSales: [SalesInfo] = [
    .init(month: "Jan", total: 2),
    .init(month: "Feb", total: 4),
    .init(month: "March", total: 5),
    .init(month: "April", total: 2),
    .init(month: "May", total: 4),
    .init(month: "June", total: 1),
    .init(month: "July", total: 4)
]
```

## Chapter 46. SwiftUI DocumentGroup 개요

- DocumentGroup 화면을 소개하고 SwiftUI에서 문서 기반 앱(document-based app)을 빌드하기 위하여 어떻게 사용할 수 있는지 설명한다.

### 46.1 앱내에서의 문서

- 내장 앱 파일(Files) 앱은 구글 드라이브와 써드-파티 프로바이더뿐만아니라 로컬 디바이스 파일 시스템 및 iCloud 저장소에 저장된 문서를 찾아보고, 선택하며 관리하는 방법을 제공한다.
- DocumentGroup 화면의 목적은 새로운 파일을 생성하는 기능 외에도 파일 앱이 제공하는 것과 같은 기능을 SwiftUI 앱에 구축할 수 있게한다.

### 46.3 DocumentGroup

- DocumentGroup 화면(scene)에는 앱 내에서 사용자가 파일과 폴더를 생성, 삭제, 이동, 이름 변경, 선택 등의 기능을 제공하는 데 필요한 대부분의 인프라가 포함된다.

### 46.4 파일 형식 지원 선언하기

- 문서 지원에 대한 구현의 핵심 단계는 앱이 지원하는 파일 형식을 선언하는 것이다.
  Document Group 사용자 인터페이스는 지원되는 형식의 파일만 선택할 수 있도록 하기 위해 이 정보를 사용한다.
- 형식이 다른 문서는 탐색 시 회식으로 표시된다.

1. 문서콘텐트 타입 식별자 (document content type identifier)
- 역방향 도메인 이름의 형식을 취하는 Uniform Type Identifier(UTI) 구문을 사용하여 선언된다.
- 예. 텍스트 파일 경우. `com.example.plain-text`

2. 핸들러 순위
- 이 값은 앱과 파일 형식의 관계를 시스템에 선언한다. 만약에 앱이 자체 커스텀 파일 형식을 사용한다면, Owner로 설정해야 하낟.
  만약에 해당 형식의 파일이 지정된 디폴트 앱으로 열리도록 한다면 Default 로 설정해야 한다.
  반면에 이러한 형식의 파일을 디폴트 앱이 아니라 앱 내에서 처리할 수 있다면 Alternate 값을 사용해야 한다.
  마지막으로, 앱이 해당 파일 형시과 관련이 없다면 None을 사용해야한다.

3. 타입 식별자 (type identifier)
- 이 식별자는 일치하는 특정 데이터 타입들의 목록과 연결되어 있어야 한다.
- 이러한 타입 식별자는 **애플**에서 제공하는 확장된 내장 타입 목록에서 선택할 수 있으며, 일반적으로 public 이라는 접두사가 붙는다.
- 예를 들어, 일반 텍스트 문서의 UTI는 public.plain-text 이며 모든 타이븨 이미지는 public.image다.
- 내장된 각 UTI 타입은 프로그램적으로 타입에 대한 작업을 할 때 사용할 수 있는 UTType에 해당하는 항목이 연결된다.
  예를 들어, public.plain-text UTI는 plainText라는 UTTyp 인스턴스가 있으며, public.mpeg4move에 대한 UTType인스턴스의 이름은 mpeg4Movie다.
- 지원하는 UTType 선언의 전체 목록은 URL을 참조한다. https://developer.apple.com/documentation/uniformtypeidentifiers/uttype

4. 파일명 확장자
- 많은 내장 타입 긱별자는 관련된 파일 타입을 지원하도록 이미 구성되어 있다. 예를 들어 public.png 타입은 .png 파일확장자를 인식한다.
- 여기에 선언된 확장자는 앱에서 생성된 모든 새로운 문서의 파일명에도 추가된다.

5. 커스텀 타입 문서 콘텐트 식별자
- 독자적인 데이터 형식으로 작업할 때, 새로운 문서 콘텐트 식별자를 선언할 수 있다.
  따라서 커스텀 타입에 대한 문서 타입 식별자는 다음과 같이 선언될 수 있다. `com.example.mydata`

6. 익스포트된 타입 식별자 vs 임포트된 타입 식별자
- 내장 타입(예. plain.image)이 사용되면, 이것을 임포트된 타입 식별자(imported type identifier)라 한다.
- 반면에 커스텀 타입 식별자는 익스포트된 타입 식별자(exported type identifier)라고 한다.
  이것은 브라우저가 해당 타입의 파일이 해당 앱과 연결된 것으로 인식할 수 있도록 앱 내에서 생성되어 시스템으로 보내지기(export) 때문이다.

### 46.5 Xcode 에서 파일 타입 지원 구성하기
- 46.4의 모든 설정은 프로젝트의 Info.plist 파일 내에서 구성된다. 프로젝트 > Tragets별 > info 탭에서 설졍을 변경할 수 있다.

### 46.6 문서 구조
- *Document.swift 라를 파일이 생성되며, 파일에 대한 파일목록 읽기가능한 파일 목록, 파일내용 읽기, 쓰기를 정의하고, 파일 생성 초기 값을 설정한다.

## Chapter 47. SwiftUI DocumentGroup 튜토리얼
- 예제 프로그램 작성

```swift
// Demo47ImageDocApp.swfit
import SwiftUI

@main
struct Demo47ImageDocApp: App {
    var body: some Scene {
        DocumentGroup(newDocument: Demo47ImageDocDocument()) { file in
            ContentView(document: file.$document)
        }
    }
}

// Demo47ImageDocDocument.swift
import SwiftUI
import UniformTypeIdentifiers

extension UTType {
    static var exampleImage: UTType {
        UTType(importedAs: "com.tistory.lunadaddy.image")
    }
}

struct Demo47ImageDocDocument: FileDocument {
    var image: UIImage = UIImage()

    init() {
        if let image = UIImage(named: "cascadefalls") {
            self.image = image
        }
    }

    static var readableContentTypes: [UTType] { [.exampleImage] }

    init(configuration: ReadConfiguration) throws {
        guard let data = configuration.file.regularFileContents,
              let decodedImage: UIImage = UIImage(data: data)
        else {
            throw CocoaError(.fileReadCorruptFile)
        }
        image = decodedImage
    }
    
    func fileWrapper(configuration: WriteConfiguration) throws -> FileWrapper {
        let data = image.pngData()!
        return .init(regularFileWithContents: data)
    }
}
```

```swift
// ContentView.swift
import SwiftUI
import CoreImage
import CoreImage.CIFilterBuiltins

struct ContentView: View {
    @Binding var document: Demo47ImageDocDocument
    @State private var ciFilter = CIFilter.sepiaTone()
    let context = CIContext()

    var body: some View {
        VStack {
            Image(uiImage: document.image)
                .resizable()
                .aspectRatio(contentMode: .fit)
                .padding()
            Button(action: {
                filterImage()
            }, label: {
                Text("Filter Image")
            })
            .padding()
        }
    }
    
    func filterImage() {
        ciFilter.intensity = Float(1.0)
        let ciImage = CIImage(image: document.image)
        ciFilter.setValue(ciImage, forKey: kCIInputImageKey)
        guard let outputImage = ciFilter.outputImage else { return }
        if let cgImage = context.createCGImage(outputImage, from: outputImage.extent) {
            document.image = UIImage(cgImage: cgImage)
        }
    }
}
```
## Chapter 48. 코어 데이터와 SwiftUI 소개

- 코어 데이터(Core Data)는 스위프트 객체로 데이터 작업을 할 수 있도록 SQLite 데이터베이스(또는 비슷한 환경)에 래퍼(wrapper)를 두는 프레임워크다.

### 48.1 코어 데이터 스택

(SwiftUI앱  )
(영구 컨테이너 )
(관리 객체 콘텍스트 / 관리 객체) -> (관리 객체 모델 / 엔티티 디스크립션)
(영구 저장소 코디테이터)
(영구 저장소 객체)
  ⬇️  ⬆️
(  데이터베이스 )

### 48.2 영구 컨테이이너
- 영구 컨테이너는 코어 데이터 스택의 생성을 처리하고, 기본적인 데이터 기능에 추가적인 애플리케이션 메서드를 쉽게 추가할 수 있도록 서브클래싱하게 설계되었다.
- 초기화가 되면, 영구 컨테이너 인스턴스는 관리 객체 콘텍스에 대한 액세스를 제공한다.

### 48.3 관리 객체
- 관리 객체는 데이터를 저장하기 위해 애플리케이션 코드에서 생성되는 객체다.
- 관리 객체는 관계형 데이터베이스 테이블의 행 또는 레코드로 생각할 수 있다.
- 관리 객체는 NSManagedObject 클래스 또는 그 하위 클래스의 인스턴스다.
- 관리 객체는 관리 객체 콘텍스트에 포함되고 유지된다.

### 48.4 관리 객체 콘텍스트
- 코어 데이터 기반의 애플리케이션은 영구 저장소와 직업 상호작용하지 않는다.
- 대신 애플리케이션 코드는 코어 데이터 스택의 관리 객체 콘텍스트 계층에 포함된 관리 객체와 상호작용한다.
- 이 콘텍스트는 기본 데이터 저장소와 관련하여 객체의 상태를 유지하고 관리 객체 모델에 의해 정의된 관리 객체 간의 관계를 관리한다.
  기본 데이터베이스와의 모든 상호작용은 콘텍스트가 변경 사항을 저장하라는 지시를 받을 때까지 콘텍스트 내에서 일시적으로 유지되며,
  이 시점에서 변경 사항은 코어 데이터 스택을 통해 전달되며 영구 저장소에 기록된다.

### 48.5 관리 객체 모델

1. 엔티티라고 하는 개념을 정의하는 관리 객체 모델의 작업으로 데이터 모델을 정의한다.
2. 엔티티는 속성(이름,주소,전화번화...), 관계, 영구저장소, 가져온 속성, 가져오기 요청이 포함될 수 있다.
- 관계(relationship)
- 가져온 속성(fetched property) 이것은 관계를 정의하는 것에 대한 대안을 제공한다.
- 자져오기 요청(fetch request) 정의된 조건(predicate)을 기반으로 데이터 객체를 검색하기 위해 참조할 수 있게 미리 정의된 쿼리다.

### 48.6 영구 저장소 코디네이터
- 영구 저장소 코디네이터(persistent store coordinator)는 여러 영구 객체 저장소에 대한 액세스를 조정하는 역할을 한다.
- 개발자가 영구 저장소와 직접 상호작용하지 않으며, 여러 장소가 필요한 경우 코디네이터는 이러한 저장소를 코어 데이터 스택의 상위 계측에 단일 저장소로 제공한다.

### 48.7 영구 객체 저장소
1. 영구 객체 저장소(persistent object store)는 코어 데이터를 사용할 때 데이터가 저장되는 기본 저장소 환경을 나타낸다.
2. 코어 데이터는 3개의 디스크 기반 영구 저장소와 한 개의 메모리 기반 영구 저장소를 지원한다.
- 디스크 기반 옵션: SQLite(default), XML, 바이너리
3. 코드는 동일한 Core Data API를 동일하게 호출하여 애플리케이션에 필요한 데이터 객체를 관리한다.

### 48.8 엔티티 디스크립션 정의하기
- 코어 데이터를 포함하기 위한 옵션으로 새로운 프로젝트를 생성하며, <엔티티이름>.xcdatamodeld 라는 템플릿 파일이 생성된다.
- Xcode 프로젝트 내비게이터 패널에서 이 파일을 선택하면 엔티티 편집 환경에 모델이 로드된다.
  Xcode 엔티티 에디터를 사용하면 엔티티 간에 관계를 설정할 수도 있다.

### 48.9 영구 컨테이너 초기화하기
- 영구 컨테이너는 새로운 NSPersistentContainer 인스턴스를 생성하고, 사용될 모델의 이름을 전달 한 다음, 해당 객체의 `loadPersistentStores()` 메서드를 호출하여 초기화된다.
```swift
let persistentContainer: NSPersistentContainer

persistentContainer NSPersistentContainer(name: "DemoData")
persistentContainer.loadPersistentStores { (storeDescription, error) in 
    if let error = error as NSError? {
        fatalError("Container load failded: \(error)")
    }
}
```

### 48.10 관리 객체 콘텍스트 얻기
- 많은 코어 데이터 메서드들은 인수로 관리 객체 콘텍스트를 필요로 하므로, 엔티티 디스크립션을 정의한 후의 다음 단계는 콘텍스트에 대한 참조를 얻는 것과 관련된 작업니다.
```swift
let managedObjectContext = persistentContainer.viewContext
```

### 48.12 관리 객체 저장하기
- 관리 객체 인스턴스가 생성되고 저장될 데이터로 구성되면, 관리 객체 콘텍스트의 `save()` 메서드를 사용하여 저장소에 저장할 수 있다.
```swift
do {
    try viewContext.save()
} catch {
    let error = error as NSError
    fatalError("An error occured: \(error))
}
```

### 48.13 관리 객체 가져오기
- 코어 데이터 저장소에 데이터를 가져오는 한 가지 방법은 데이터를 저장할 변수를 선언할 때 `@FetchRequest` 프로퍼티 래버를 사용하는 것이다.
```swift
@FetchRequest(entity: Customer.entity(),
              sortDescriptors: [NSSortDescriptor(key: "name", ascending: true)])
private var customers: FetchedResults<Customer>
```

### 48.14 조건에 따라 관리 객체 검색하기
- 조건(predicate)을 정의하여 관리 객체를 검색할 수 있다.
```swift
@FetchRequest(entity: Customer.entity(),
              sortDescriptors: [],
              predicate: NSPredicate(format: "name like %@", "John Smith"))
private var customers: FetchedResults<Customer>
```

- 일회성 가져오기(fetch) 작업. 
  1) NSFetchRequest 인스턴스를 생성하고, 
  2) 엔티터와 3) 조건 설정으로 인스턴스를 구성한 다음, 4) 관리 객체 콘텍스트의 fetch() 메서드에 전달하여 일회성 가져오기 작업을 수행할 수 있다.
```swift
@State var matches: [Customer]?

let fetchRequest: NSFetchRequest<Product> = Product.fetchRequest()
fetchRequest.entity = Customer.entity()
fetchRequest.predicate = NSPredicate(
    format: "name LIKE %@", "John Smith"
)
matches = try? viewContext.fetch(fetchRequst)
```

## Chapter 49. SwiftUI 코어 데이터 튜토리얼
- 예제 프로그램
```swift
// (mainapp) Demo49CoreDataApp.swift
import SwiftUI

@main
struct Demo49CoreDataApp: App {
    let persistenceController = PersistenceController.shared
    
    var body: some Scene {
        WindowGroup {
            ContentView()
                .environment(\.managedObjectContext, persistenceController.container.viewContext)
        }
    }
}
```

```swift
// Persistence.view
import CoreData

struct PersistenceController {
    static let shared = PersistenceController()
    
    let container: NSPersistentContainer
    
    init() {
        container = NSPersistentContainer(name: "Products")
        container.loadPersistentStores { storeDescription, error in
            if let error = error as NSError? {
                fatalError("Container load failed: \(error)")
            }
        }
    }
}
```

```swift
import SwiftUI
import CoreData

struct ContentView: View {
    @State var name: String = ""
    @State var quantity: String = ""
    @Environment(\.managedObjectContext) private var viewContext
    @FetchRequest(entity: Product.entity(), 
                  sortDescriptors: [NSSortDescriptor(key: "name", ascending: true)])
    private var products: FetchedResults<Product>
    
    var body: some View {
        NavigationView {
            VStack {
                TextField("Product name", text: $name)
                TextField("Product quantity", text: $quantity)
                
                HStack {
                    Spacer()
                    Button("Add") {
                        addProduct()
                    }
                    Spacer()
                    
                    NavigationLink(destination: ResultView(name: name, viewContext: viewContext)) {
                        Text("Find")
                    }
                    Spacer()

                    Button("Clear") {
                        name = ""
                        quantity = ""
                    }
                    Spacer()
                }
                .padding()
                .frame(maxWidth: .infinity)
                
                List {
                    ForEach(products) { product in
                        HStack {
                            Text(product.name ?? "Not Found")
                            Spacer()
                            Text(product.quantity ?? "Not Found")
                        }
                    }
                    .onDelete(perform: deleteProducts)
                }
                .navigationTitle("Product Database")
            }
            .padding()
            .textFieldStyle(RoundedBorderTextFieldStyle())
        }
    }
    
    private func addProduct() {
        withAnimation {
            let product = Product(context: viewContext)
            product.name = name
            product.quantity = quantity
            saveContext()
            name = ""
            quantity = ""
        }
    }
    
    private func deleteProducts(offsets: IndexSet) {
        withAnimation {
            offsets.map {products[$0] }.forEach(viewContext.delete)
            saveContext()
        }
    }
    
    private func saveContext() {
        do {
            try viewContext.save()
        } catch {
            let error = error as NSError
            fatalError("An error occurred: \(error)")
        }
    }
}

struct ResultView: View {
    var name: String
    var viewContext: NSManagedObjectContext
    
    @State var matches: [Product]?
    
    var body: some View {
        return VStack {
            List {
                ForEach(matches ?? []) { match in
                    HStack {
                        Text(match.name ?? "Not found")
                        Spacer()
                        Text(match.quantity ?? "Not found")
                    }
                }
            }
            .navigationTitle("Results")
            .task {
                let fetchRequest: NSFetchRequest<Product> = Product.fetchRequest()
                fetchRequest.entity = Product.entity()
                fetchRequest.predicate = NSPredicate(format: "name CONTAINS %@", name)
                matches = try? viewContext.fetch(fetchRequest)
            }
        }
    }
}
```

## Chapter 50. SwiftUI 코어 데이터와 클라우드킷 저장소 개요

- 클라우드킷(CloudKit)은 iCloud 저장소를 사용하여 클라우드 기반의 데이터베이스를 저장하는 방법을 제공하며, 여러 디바이스와 사용자 그리고 앱에 접근할 수 있게 한다.
- 초기에는 iCloud 기반 데이터베이스를 직접 생성하고, 관리하며 접근하기 위한 코드를 작성할 수 있는 전용 프레임워크로 제공되었지만,
  요즘 권장하는 방법은 코어 데이터와 함께 클라우드킷을 사용하는 것이다.

### 50.1 클라우드킷 개요

- CloudKit 프레임워크는 애플에서 호스팅하는 iCloud 서버에 대한 접근 권한을 애플리케이션에 제공하고 
  구조화된 방식으로 데이터와 기타 애셋 타입(비디오, 이미지, 파일, ...)을 저장, 관리 및 검색하기 위한 쉬운 방법을 제공한다.
- 이것은 사용자가 개인 데이터를 저장하고 여러 디바이스에서 접근할 수 있는 플랫폼을 제공하며, 
  애플리케이션의 모든 사용자가 공개적으로 사용할 수 있는 데이터를 개발자가 제공할 수도 있게 한다.

### 50.2 클라우드킷 컨테이너
- 클라우드킷이 활성화된 애플리케이션에는 하나 이상의 컨테이너가 iCloud에 있다.
- 애플리케이션의 컨테이너는 CKContainer 클래스에 의해 클라우드킷에 표현되며 데이터베이스는 이들 컨테이너 내에 있게 된다.

### 50.3 클라우드킷 공용 데이터베이스
- 각 클라우드 컨테이너에는 하나의 공용 데이터베이스(public database)가 포함되어 있다.
- 이것은 애플리케이션의 모든 사용자에게 필요한 데이터가 저장된 데이터베이스다. 
  예를 들어 지동 앱에는 앱의 모든 사용자게 적용되는 위치 및 경로에 대한 데이터 세트가 있다. (전체 사용자 공유정보)
  이러한 데이터는 애플리케이션의 클라우드 컨테이너 공용 데이터베이스에 저장된다.

### 50.4 클라우드킷 개인 데이터베이스
- 개인 데이터베이스(private database)는 각 개발 사용자에게만 공개되는 데이터를 저장하는 데 사용된다.
- 각 클라우드 컨테이너에는 애플리케이션의 각 사용자에 대한 하나의 개인 데이터베이스가 포함된다.

### 50.5 데이터 저장소 할당량
- 앱의 공용 클라우드 데이터베이스에 저장된 데이터와 애셋은 앱의 저장소 할당량(storage quota)에 포함된다.
- 반면, 개인 데이터베이스에 저장된 모든 항목은 해당 사용자의 iCloud 할당량에 포함된다.
- 애플은 프리 티어(free tier)에 포함되는 초당 쿼리 수와 데이터 전송량에 제한을 둔다. 일반적인 프로젝트에서는 이러한 제한이 발생하지는 않는다.

### 50.6 클라우드킷 레코드
- 데이터는 레코드 형식으로 공용 데이터베이스와 개인 데이터베이스 모두에 저장된다.
- 레코드는 CKRecord 클래스로 표현되며 기본적으로 키가 레코드에 저장된 데이터 값을 참조하는 데 사용되는 키-값 쌍의 딕셔너리다.
- 코어 데이터를 사용하여 클라우드킷을 통해 데이터가 저장되면, 이러한 레코드는 코어 데이터 관리 객체로 표현된다.

### 50.7 클라우드킷 레코드ID
- 각 클라우드킷 레코드는 CKRecordID 클래스로 표현되는 고유한 레코드 ID가 연결되어 있다.
- 레코드가 처음 생성될 때 레코드 ID를 지정하지 않으면 클라우드킷 프레임워크에서 자동으로 하나를 제공한다.

### 50.8 클라우드킷 참조
- 클라우드킷 참조(CloudKit reference)는 CKReference 클래스를 사용하여 구현되며 데이터베이스의 서로 다른 레코드 간의 관계를 구축하는 방법을 제공한다.

### 50.9 레코드 존
- 클라우드킷 레코드 존(CKRecordZone)은 개인 데이터베이스 내의 레코드 그룹을 연결하기 위한 메커니즘을 제공한다.
- 레코드를 클라우드에 저장할 때 레코드 존을 지정하지 않으면 대상 데이터베이스의 디폴트 존에 배치된다.
- 커스텀 존은 개인 데이터베이스에 추가될 수 있으며 관련 레코드를 구성하고 **단일 트랜잭션에서 동시에 여러 레코드에 쓰는 것과 같은 작업**을 수행하는 데 사용될 수 있다.
- 각 레코드 존은 새로운 레코드를 존에 추가할 때 참조되어야 하는 고유한 레코드존 ID가 연결된다.
- 공용 데이터베이스 내의 모든 레코드는 공용 디폴트 존에 있는 것으로 간주된다.
- 클라우드킷 레코드 존은 코어 데이터 영구 컨테이너로 변환된다. 이 때 NSPersistentCloudKitContainer 클래스를 사용한다. (No Cloud는 NSPersistentContainer 클래스)

### 50.10 클라우드킷 콘솔
- 클라우드킷 콘솔(CloudKit Console)은 클라우드킷 옵션과 애플리케이션 저장소를 관리하기 위한 인터페이스를 제공하는 웹 기반의 포털이다.
  URL: https://icloud.developer.apple.com/dashboard/
- 클라우드킷 콘솔을 통해 데이터를 접근할 경우, 개인 사용자 데이터는 대시보드 인터페이스를 사용하여 접근할 수 없다.
  공용 데이터베이스에 저장된 데이터와 콘솔에 로그인하는 데 사용된 개발자 계정에 속한 개인 데이터베이스만 조회하고 수정할 수 있다.

### 50.11 클라우드킷 공유
- **앱의 공용 데이터베이스에 포함된 클라우드킷 레코드는 해당 앱의 모든 사용자가 접근할 수 있다.**
- 그러나 사용자가 개인 데이터베이스에 포함된 특정 레코드를 다른 사용자와 공유하려는 상황이 발생할 수 있다.
  이것은 클라우드킷 공유(Cloudkit Sharing)의 도입으로 가능해 졌다.

### 50.12 클라우드킷 구독
- **클라우드킷 구독(CloudKit subscription)을 사용하면 설치된 앱에 속한 클라우드 데이터베이스 내에서 변경이 발생할 때 사용자에게 알려줄 수 있다.**
- 구독은 표준 iOS 푸시 알림 인프라를 사용하며 레콛가 추가, 업데이트 또는 삭제될 때와 같은 다양한 조건에 따라 발송될 수 있다.
  특정 조건과 일치하는 레코드의 데이터를 기반으로 알림이 발송하도록 조건을 사용하면 알림을 추가로 세분화할 수 도 있다.


## Chapter 51. SwiftUI 코어 데이터와 클라우드킷 튜토리얼

- Xcode SwiftUI 프로젝트에 클라우드킷 지원을 추가하는 첫 번째 단계는 iCloud 기능을 추가하여 클라우드킷 서비스와 원격 알림을 모두 활성화하고,
  앱과 연결된 데이터베이스를 저장하도록 컨테이너를 구성하는 것이다.
- 코어 데이터에서 클라우드킷으로는 마이그레이션은 NSPersistentContainer 대신 NSPersistentCloudKitContainer를 사용핟록 코드를 변경하고 프로젝트를 다시 빌드하기만 하면 된다.
- 클라우드킷 데이터베이스는 클라우드킷 콘솔 내에서 쿼리, 수정, 관리 및 모니터링할 수 있다.

## Chapter 52. 시리킷 소개

-- 시리킷의 목적은 시리 인터페이스를 통해 음성 명령으로 애플리케이션 기능의 핵심 영역에 접근할 수 있도록 하는 것이다.

### 52.1 시리와 시리킷
- 시리는 사용자의 요청을 인텐트(intent)로 패키징하여 iOS앱에 전달한다. 
- 인텐트에 필요한 모든 데이터가 포함되면 앱은 요청된 작업을 수행하고 결과를 시리에게 알린다.
  이러한 결과는 시리 또는 iOS 앱 자체 내에서 표시된다.

### 52.2 시리킷 도메인
1. 시리는 다음 도메인 중 하나 이상에 해당하는 작업을 수행할 때만 앱에서 사용할 수 있다.
- 메시징
- 메모 및 목록
- 결제
- 비주얼 코드
- 사진
- 운동
- 승차 예약
- 카플레이
- 자동차 제어
- VoIP 통화
- 레스토랑 예약
- 미디어
2. 만약 앱에 일치하는 도메인이 없다면, 커스텀 시리 단축어(Siri shortcut)를 사용하여 시리킷을 통합할 수 있다.

### 52.3 시리 단축어
- 시리 단축어는 앱 내에서 자주 수행되는 활동을 단축어로 저장하고 미리 정의된 구문을 사용하여 시리를 통해 트리거되게 할 수 있다.
- 사용자 행동 패턴을 기반으로 시리는 사용자가 디바이스 홈 화면에서 아래쪽으로 스와이핑 동작을 할 때 나타나는 시리 제안(siri suggestion)과 검색 패털에서 사용자에게 단축어를 제안한다.

### 52.4 시리킷 인텐트
- 각 도메인은 미리 정의된 작업, 즉 인텐트 세트가 앱에 의해 수행되도록 사용자가 요청하게 한다.
- '인텐트'는 시리가 인식하고 시리킷이 통합된 iOS 앱에 의해 수행될 수 있는 '특정 작업'을 나타낸다.
- 시리 단축어의 경우, 시리킷 통합은 앱이 시리와 어떻게 상호작용하는지를 설명하는 인텐트 정의 파일과 결된 커스텀 인텐트를 사용하여 구현된다.

### 52.5 시리킷 통합의 작동 방식
- 시리 통합은 iOS 익스텐션 메커니즘을 통해 수행된다.
1. 시리킷은 두 가지 유형의 익스텐션을 제공하면 그 중 핵심은 인텐트 익스텍션이다.
-  이 익스텐션에는 Intents 프레임워크의 INExtension 클래스로 부터 서브클래싱된 인텐트 핸들러가 있으며,
  사용자와 통신하는 과정에서 시리가 호출하는 메서드가 포함되어 있다.
- 시리가 사용자로부터 필요한 모든 정보를 수집했는지 확인하고 인테트에 정의된 작업을 실행하는 것은 **인텐트 핸들러**가 담당한다.

2. 두 번째 익스텐션 유형은 UI 익스텐션이다. 이 익스텐션은 선택 사항이며 스토리보드 파일과 IntentViewController 클래스의 하위 클래스로 구성된다.
- 이 익스텐션이 제공되었다면 사용자에게 정보를 표시할 때 시리는 이 UI를 사용한다.

3. 사용자가 시리를 통해 앱을 요청할 때 가장 먼저 호출하는 메소드는 인텐트 익스텐션에 포함된 인텐트 핸들러 클래스의 `handler(forIntent:)` 메소드다.
- 이 메서드는 현재 인텐트 객체에 전달되고 인테트 핸들러로 사용할 객체에 대한 참조를 반환한다.
- 인텐트 핸들러는 처리할 수 있는 인텐트 타입을 선언하고, 이러한 특정 인텐트 타입을 지워하는 데 필요한 모든 프로토콜 메서드를 구현해야 한다.

```
시리 => 인텐트 핸들러
    -> 1. 매개변수 확인
    -> 2. 인텐트 확인
    -> 3. 인텐트 처리
```

### 52.6 인텐트 매개변수 확인하기
- 각 인텐트 도메인 타입에는 앱에서 수행할 작업에 대한 세부 정보를 제공하는 데 사용되는 매개변수 그룹이 연결되어 있다.
  많은 매개 변수가 필수지만 일부는 선택사항이다.
- 시리가 이미 매개변수를 가지고 있다면 매개변수가 유효한지를 확인하도록 인텐트 핸들러에게 요청한다.
  시리에 매개변수 값이 아직 없다면, 인텐트 핸들러에게 매개변수가 필요한지 묻는다. 
  만약 매개변수가 필요하다면 시리는 사용자에게 정보 제공을 요청한다.

 ### 52.7 확인 메서드
- 확인(confirm) 메서드는 익스텐션 핸들러 내에서 구현되며 모든 인텐트 매개변수가 확인되면 시리에 의해 호출된다.
- 이 메서드는 인텐트 핸들러가 인텐트를 처리할 준비가 되었는지 확인할 수 있는 기회를 제공한다.
  확인 메서드가 준비가 된 상태라고 보고하면 시리는 핸들 메서드를 호출한다.

### 52.8 핸들 메서드
- 핸들(handle) 메서드는 인텐트와 관련된 활동이 수행되는 곳이다. 작업이 완료되면 응답이 시리에 전달되다.
  응답형식은 수행된 활동 타입에 따라 다르다.
- 핸들 메서드는 continueInApp 응답을 반환할 수 도 있다. 이것은 작업의 나머지 부분이 메인 앱 내에서 수행될 것임을 시리에게 알려준다.
  이 응답을 받으면 시리는 NSUserActivity 객체를 전달하여 앱을 시작한다.
- NSUserActivity는 앱의 상태를 저장하고 복원할 수 있게 해주는 클래스다. 
  iOS 10 이상에서 NSUserActivity 클래스에는 앱 상태와 함께 NSInteraction 객체를 저장할 수 있는 추가 속성이 있다.
  시리는 이 interaction 속성을 사용하여 세션에 대한 NSInteraction 객체를 저장하고 메인 iOS 앱에 전달한다.
- 그러면 interaction 객체에는 활동을 계속 처리하기 위해 앱이 추출할 수 있는 인텐트 객체의 복사본이 포함된다.
  커스텀 NSUserActivity 객체는 익스텐션으로 생성되며 iOS앱에 전달될 수 있다. 커스텀 객체가 지정되지 않았다면 시리킷은 디폴토르 하나를 생성한다.
- 인텐트 핸들러 클래스는 서로 다른 인텐트 타입을 처리하기 위해 하나 이상의 핸들 메서드를 포함할 수 있다.
  예를 들어, 메시징 앱은 메시지 보내기 및 메시지 검색 인텐트에 대해 서로 다른 핸들러 메서드를 갖는다.

### 52.9 커스텀 어휘
1. 시리는 다양한 언어의 어휘를 폭 넓게 알고 있다. 하지만 앱 또는 앱 사용자가 의미나 맥락인 없는 특정 단어 또는 용어를 시리에 사용할 수도 있다.
  이러한 용어를 시리가 인식하도록 앱에 추가할 수 있다. 이런 커스텀 어휘용어(custom vocabulary term)는 사용자별이나 전역으로 분류된다.
2. 사용자별 용어(User specific term)는 개별 사용자에게만 적용되는 용어다.
  사용자별 용처는 `NSVocabulary` 클래스의 `setVocabularyStrings(oftype:)` 메서드를 사용하여 애플리케이션 런타임 시 메인 iOS 앱 내에서 시리에 등록되며,
  먼저 나열된 가장 일반적으로 사용되는 용어가 포함된 정렬된 목록 형식으로 제공되어야 한다.
3. 사용자별 커스텀 용어는 연락처 및 연락처 그룹 이름, 사진 태그 및 앨범 이름, 운동 이름, CarPaly 자동차 프로핌 이름에 대해서만 지정할 수 있다.
   순서가 지정된 목록과 함께 `setVocabularyString(oftype:)` 메서드를 호출할 때 지정된 카테고리 타입은 다음 주 하나여야 한다.
- contactName
- contactGroupName
- photoTag
- photoAlbumName
- workoutActivityName
- carProfileName
4. 전역 어휘 용어(global vocabulary term)는 앱에 따라 다르지만 모든 앱 사용자에게 적용된다.
   이러한 용어는 AppInventoryVocabulary.plist 라는 속성 목록 파일 형식으로 앱 번들과 함께 제공된다.
   이들 용어는 운동 및 차량 공유 이름에만 적용된다.

### 52.10 시리 사용자 인터페이스
- 각 시리킷 도메인에는 사용자에게 정보를 전달하는 데 디폴트로 사용되는 표준 사용자 인터페이스 레이아웃이 있다.
- 이 주제는 60.5 '구성 인텐트 UI 커스터마이징하기'에서 다룬다.
- 시리 단축어의 경우 단축어가 사용될 때 시리 내에 나타나는 사용자 인터페이스를 커스텀하기 위해 동일한 기술이 사용될 수 있다.

## Chapter 53. SwiftUI 시리킷 메시징 익스텐션 튜토리얼
- 예제 프로그램

--- 526

## Chapter 54. 시리 단축어 앱 통합 개요
--- 533

## Chapter 55. SwiftUI 시리 단축어 튜토리얼
--- 555

-- 01/28(일) --


## Chapter 56. SwiftUI와 위젯킷으로 위젯 빌드하기
--- 564
--- 01/29 ---

## Chapter 57. SwiftUI 위젯킷 튜토리얼
--- 579
--- 01/30 ---

## Chapter 58. 위젯킷 크기 지원
--- 585

## Chapter 59. SwiftUI 위젯키 딥링크 튜토리얼
--- 592
--- 01/31 ---

## Chapter 60. 위젯킷 위젯에 구성 옵션 추가하기
--- 600

## Chapter 61. UIView를 SwiftUI에 통합하기
--- 610
--- 2/1 ---

## Chapter 62. UIViewController를 SwiftUI와 통합하기
--- 618
--- 2/2 ---

## Chapter 63. SwiftUI를 UIKit에 통합하기
--- 631

## Chapter 64. 앱 스토어에 iOS 16 애플리케이션 등록을 위한 준비와 제출하기
--- 642

--- 02/3(토) ---

-- 2/4(일) --
-- 만들 앱 / 선정
-- 일단 쉬운 걸로

end.

------------------------

핵심만골라배우는Swift(2023)


Swift 프로그래밍을 배우기 위한 몇 가지 추천 사이트는 다음과 같습니다:

1. **Swift Playgrounds**¹: 이 앱은 iPad 및 Mac용으로 제공되며, Swift로 코딩을 배우고 앱을 빌드하는 데 도움이 됩니다¹. 흥미로운 레슨과 안내를 통해 대화식 환경에서 실제 Swift 코드를 작성하며 코딩 및 앱 빌드의 핵심 개념을 확인할 수 있습니다¹.

2. **인프런**²: 'iOS 개발을 위한 swift5 완벽 가이드'라는 강의가 있습니다². 이 강의는 Swift 기초 문법과 Swift Standard Library 활용 방법을 모두 공부하며, 100% 라이브 코딩으로 최신 문법을 함께 공부하다보면 자연스럽게 Swift를 정복할 수 있습니다².

3. **100 Days of Swift**³: 이 사이트는 100일 동안 매일 스위프트 공부할 수 있는 커리큘럼을 제공합니다³. 스위프트 문법부터 시작해서 예제 프로젝트까지 다양하게 할 수 있습니다³.

4. **Lets Build That App**³: 유튜브 채널로, 페이스북, 인스타그램 등 다양한 앱들을 만들어보는 프로젝트 시리즈로 만들어 유튜브 채널에 올립니다³.

이러한 사이트들을 통해 Swift 프로그래밍을 배우는 데 도움이 될 것입니다. 학습에 성공하길 바랍니다!.

출처: Bing과의 대화, 2023. 11. 26.
(1) Swift Playgrounds - Apple Developer. https://developer.apple.com/kr/swift-playgrounds/.
(2) iOS 개발을 위한 swift5 완벽 가이드 - 인프런 | 강의. https://www.inflearn.com/course/Swift-KXcoding.
(3) 개인적으로 추천하는 도움이 되는 iOS 공부 자료 | Joohee Kim's Blog. https://bing.com/search?q=Swift+%ed%94%84%eb%a1%9c%ea%b7%b8%eb%9e%98%eb%b0%8d+%ed%95%99%ec%8a%b5+%ec%82%ac%ec%9d%b4%ed%8a%b8+%ec%b6%94%ec%b2%9c.
(4) [Site] 코딩테스트 준비, 알고리즘 공부 추천사이트 - ‍ .... https://lxxyeon.tistory.com/80.
(5) ko.wikipedia.org. https://ko.wikipedia.org/wiki/%EC%8A%A4%EC%9C%84%ED%94%84%ED%8A%B8_(%ED%94%84%EB%A1%9C%EA%B7%B8%EB%9E%98%EB%B0%8D_%EC%96%B8%EC%96%B4).


