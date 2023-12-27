# swift_study_2023

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

- 클로저는 함수나 클로저 표현식과 같은 독립적인 코드블록과 코드 블록 주변에 있는 하나 이상의 변수가 결합된 것을 말한다.
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

-----------------------------
------- 5(42), 8(69), 9(84), 11(106)



## Chapter 12. 스위프트 구조체와 열거형
--- 114
## Chapter 13. 스위프트 프로퍼티 래퍼
--- 121
## Chapter 14. 스위프트의 배열과 딕셔너리 컬렉션으로 작업하기
--- 132
## Chapter 15. 스위프트 5의 에러 핸들링 이해하기
--- 139

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
- 각각의 뷰는 View 프로토코을 따르는 독립적인 객체다.

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



---------------------------------------------------------------------------------------
---------------------------------------------------------------------------------------
---------------------------------------------------------------------------------------


--- 192
## Chapter 21. SwiftUI스택과 프레임
--- 204


## Chapter 22. SwiftUI상태 프로퍼티, Observable, State, Environment 객체
--- 214
## Chapter 23. SwiftUI예제 튜토리얼
--- 229

## Chapter 24. 스위프트 구조화된 동시성 개요
--- 248
## Chapter 25. 스위프트 액터 소개
--- 256
## Chapter 26. SwiftUI동시성 및 생명 주기 이벤트 수정자
--- 262
## Chapter 27. Observable 객체와 Environment 객체 튜토리얼
--- 270


## Chapter 28. AppStorage와 SceneStorage를 사용한 SwiftUI데이터 지속성
--- 280
## Chapter 29. SwiftUI스택 정렬과 정렬 가이드
--- 297


## Chapter 30. SwiftUI List와 내비게이션
--- 313
## Chapter 31. SwiftUI List와 NavigationStack 튜토리얼
--- 332


## Chapter 32. 분할 뷰 내비게이션 개요
--- 337
## Chapter 33. NavigrationSplitView 튜토리얼
--- 345
## Chapter 34. List, OutlineGroup, DisclosureGroup 개요
--- 353
## Chapter 35. SwiftUI List, OutLineGroup, DisclosureGroup 튜토리얼
--- 364


## Chapter 36. LazyVGrid 및 LazyHGrid로 SwiftUI 그리드 구축하기
--- 376
## Chapter 37. Grid와 GridRow를 사용하여 SwiftUI 그리드 구축하기
--- 388
## Chapter 38. SwiftUI에서 탭 그리고 페이지 뷰 구축하기
--- 393


## Chapter 39. SwiftUI에서 콘텍스트 메뉴 바인딩하기
--- 397
## Chapter 40. SwiftUI 그래픽 드로잉 기초
--- 406
## Chapter 41. SwiftUI 애니메이션과 전환
--- 420


## Chapter 42. SwiftUI에서 제스처 작업하기
--- 429
## Chapter 43. 사용자 정의 SwiftUI ProgressView 생성하기
--- 436
## Chapter 44. SwiftUI 차트로 데이터 표시하기
--- 444
## Chapter 45. SwiftUI 차트 튜토리얼
--- 449



## Chapter 46. SwiftUI DocumentGroup 개요
--- 460
## Chapter 47. SwiftUI DocumentGroup 튜토리얼
--- 467
## Chapter 48. 코어 데이터와 SwiftUI 소개
--- 476


## Chapter 49. SwiftUI 코어 데이터 튜토리얼
--- 492
## Chapter 50. SwiftUI 코어 데이터와 클라우드킷 저장소 개요
--- 498
## Chapter 51. SwiftUI 코어 데이터와 클라우드킷 튜토리얼
--- 510



## Chapter 52. 시리킷 소개
--- 518
## Chapter 53. SwiftUI 시리킷 메시징 익스텐션 튜토리얼
-- 526
## Chapter 54. 시리 단축어 앱 통합 개요
--- 533



## Chapter 55. SwiftUI 시리 단축어 튜토리얼
--- 555
## Chapter 56. SwiftUI와 위젯킷으로 위젯 빌드하기
--- 564


## Chapter 57. SwiftUI 위젯킷 튜토리얼
--- 579
## Chapter 58. 위젯킷 크기 지원
--- 585
## Chapter 59. SwiftUI 위젯키 딥링크 튜토리얼
--- 592
## Chapter 60. 위젯킷 위젯에 구성 옵션 추가하기
--- 600



## Chapter 61. UIView를 SwiftUI에 통합하기
--- 610
## Chapter 62. UIViewController를 SwiftUI와 통합하기
--- 618
## Chapter 63. SwiftUI를 UIKit에 통합하기
--- 631



## Chapter 64. 앱 스토어에 iOS 16 애플리케이션 등록을 위한 준비와 제출하기
--- 642

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
