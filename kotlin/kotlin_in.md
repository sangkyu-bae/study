# 01 코틀린이란 무엇이며 왜 필요한가 ?

코틀린은 자바 플랫폼에서 돌아가는 새로운 프로그래밍 언어다. 코틀린은 간결하고 실용적이며, 자바 코드와의 상호운용성을 중시한다. 현재 자바가 사용 중은 곳이라면 거의 대부분 코틀린을 활용할 수 있다. 코틀린은 주목적은 현재 자바가 사용되고 있는 모든 용도에 적합하면서도 더 간결하고 생상적이며 안전한 대체 언어를 제공하는 것이다.

## 정적 타입 지정 언어
코틀린도 정적 타입 지정 언어디. 정적 타입 지정이라는 말은 모든 프로그램 구성 요소의 타입을 컴파일 시점에서 알 수 있고 프로그램 안에서 객체 필드나 메서드를 사용할 때마다 컴파일러가 타입을 검증해준다는 뜻이다. 동적 타입 지정 언어에서는 타입과 관계 없이 모든 값을 변수에 넣을 수 있고, 메서드나 필드 접근에 대한 검증이 실행 시점에 일어나며, 그에 따라 코드가 더 짧아지고 데이터 구조를 더 유연하게 생성하고 사용할 수 있다. 하지만 컴파일 시 걸러내지 못하고 실행 시점에 오류가 발생한다.

한편 자바와 달리 코틀린에서는 모든 변수의 타입을 프로그래머가 직접 명시할 필요가 없다. 코틀린은 컴파일러가 문맥으로 부터 변수 타입을 자동으로 유추할 수 있기 때문이다.

## 안정성
코틀린은 자바보다 null 처리를 좀더 명확하게 한다. 그렇기에 NPE(NullPointerException)가 발생하는 빈도를 현저히 낮출 수 있다.

```kotlin
var s2: String? = null // null이 될 수 있음
var s2: String = "" // null이 될 수 없음
```
이러한 코드를 통해 ?가 없이 변수를 선언한다면 null이 될수 없도록 설정해 놓고 ?을 통해 null을 허용하는지 안하는지 확인이 가능하다.


# 02 코틀린 함수

## 02-1 코틀린 함수기초
### 함수 정의

```kotlin function
fun 함수 이름([변수 이름: 자료형, 변수 이름: 자료형..]  ): [반환값의 자료형] { 
    표현식...
    [return 반환값] 
}
```
코틀린에서 모든 함수는 fun 이라는 키워드로 시작 한다 . 매개변수는 콤마(,)와 함께 여러 개를 지정할 수 있고 반드시 콜론(:)과 함께 자료형을 명시해 주어야 합니다. 함수가 반환하는 값이 있다면 반환값의 자료형도 반드시 명시해야 한다.

### 함수 정의의 예

```kotlin function ex
fun sum(a: Int, b: Int): Int {
    return a + b
}
```
함수의 반환값을 생략될 수 있으며, 이는 return 문을 생략할 수 있다. 대신 반환값의 자료형을 Unit으로 지정하거나 생략한다.(java void 함수랑 비슷함) 

### 가변인자를 가진함수


함수 인자로 정해진 크기의 인자를 전달하는것이 아니라 매번 다른 크기의 인자를 전달한다면 가변 인자(variable arguments)를 사용하면 된다.

```kotlin variable arguments ex
fun main(args: Array<String>) {

    normalVarargs(1, 2, 3, 4) // 4개의 인자 구성
    normalVarargs(4, 5, 6)    // 3개의 인자 구성
}

fun normalVarargs(vararg counts: Int) {
    for (num in counts) {
        println("$num")
    }
    print("\n")
}
```

## 02-2 함수형 프로그래밍

### 코틀린에서 왜 람다식을 사용하나?

코틀린은 '함수형 프로그래밍'을 지원하는 언어이기 때문이다. 이는 순수 함수를 작성하여 프로그램의 부작용을 줄이는 프로그래밍 기법을 말하며 람다식과 고차함수를 사용, 그렇기에 코틀린에서 람다식을 사용하는 이유는 함수형 프로그래밍 규칙을 따르기 위함 이다.

### 순수함수

순수 함수가 되기 위해서는 두가지 조건을 충족해야한다
```
1. 같은 인자에 대해ㅏ여 항상 같은 값을 반환한다='부작용이 없는 함수'
2. 함수 외부의 어떤 상태도 바꾸지 않는다.
```

### 람다식

수학에서 말하는 람다 대수는 이름이 없는 함수로 2개 이상의 입력을 1개의 출력으로 단순화 한다는 개념입니다. 그런데 함수형 프로그래밍의 람다식은

```
1. 다른 함수의 인자로 넘기는 함수
2. 함수의 결과값으로 반환하는 함수
3. 변수에 저장하는 함수
```

### 매개변수가 없는 람다식

람다식 함수에 매개변수가 없으면 화살표 기호가 사용되지 않고 소괄호는 생략할 수 있다.
```
fun main() {
    // 매개변수 없는 람다식 함수
    noParam({ "Hello World!" })
    noParam { "Hello World!" } // 위와 동일 결과, 소괄호 생략 가능
}

// 매개변수가 없는 람다식 함수가 noParam 함수의 매개변수 out으로 지정됨
fun noParam(out: () -> String) = println(out())
```


### 매개변수가 한 개인 경우

람다식 함수에 매개변수가 한 개 있을 경우에는 람다식에 화살표 기호(->) 왼쪽에 필요한 변수를 써 줘야 한다. 하지만 이렇게 매개변수가 한 개인 경우에는 화살표 표기를 생략하고 it으로 대체할 수 있다.


# 03 프로그램 흐름 제어

## 기본적인 조건과 분기

기본적인 if~else 문은 주어진 조건이 참 혹은 거짓일 경우에 따라 실행된다
```kotlin
if (조건식) { 
    수행할 문장 // 조건식이 참인 경우에만 수행
} else { 
    수행할 문장 // 조건식이 거짓인 경우에 수행
}
```
기본적인 방법이나 수행 문장이 한줄로 간단한 경우
```kotlin
val max = if (a > b) a else b
```
으로 표현 할 수 있다.


## when문으로 다양한 조건 처리

주어진 인자에 대해 다양한 조건을 만들거나 인자 없이 여러개의 조건을 구성할수있다.

```kotlin
when (인자) {
  인자에 일치하는 값 혹은 표현식 -> 수행할 문장
  인자에 일치하는 범위 -> 수행할 문장
  ...
  else -> 문장
}
```
화살표 왼쪽에는 일치하는 값, 표현식, 범위 사용할수 있으며 오른쪽에는 수행할 문장을 사용한다 없을 경우 else문 다음에 작성한 문잦을 실행
```kotlin
when (x) {
    1 -> print("x == 1")
    2 -> print("x == 2")
    else -> { // 블록 구문 사용 가능
        print("x는 1, 2가 아닙니다.")
    }
}
```

## 흐름의 중단과 반환


인라인으로 선언되지 않은 람다식 함수에서 return을 사용할 때는 그냥 사용할 수 없다. return @lavel과 같이 라벨 표기와 함께 사용해야 한다
``` kotlin
fun inlineLambda(a: Int, b: Int, out: (Int, Int) -> Unit) { // inline이 제거됨
    out(a, b)
}

fun retFunc() {
    println("start of retFunc")
    inlineLambda(13, 3) lit@{ a, b ->  // ① 람다식 블록의 시작 부분에 라벨을 지정함
        val result = a + b
        if(result > 10) return@lit // ② 라벨을 사용한 블록의 끝부분으로 반환
        println("result: $result")
    } // ③ 이 부분으로 빠져나간다
    println("end of retFunc") //  ④ 이 부분이 실행됨 
}
```

# 04 코틀린의 표준함수 활용

## 고차함수

고차함수는 함수의 매개변수로 함수를 받거나 함수 자체를 반환할 수 있는 함수이다.

```kotlien
fun inc(x: Int): Int {
    return x + 1
}

fun high(name: String, body: (Int)->Int): Int {
    println("name: $name")
    val x = 0
    return body(x)
}
```

## 클로저

람다식 함수를 이용하다 보면 내부 함수에서 외부 변수를 사용 할때가 있다. 클로저란 람다식으로 표현된 내부 함수에서 외부 범우에 선언된 변수에 접근할 수 있는 개념이다. 이 때 람다식 안에 있는 외부 변수는 값을 유지하기 위해 람다가 포획한 변수라고 부른다. 

```kotilen
fun main() {

    val calc = Calc()
    var result = 0 // 외부의 변수
    calc.addNum(2,3) { x, y -> result = x + y }  // 클로저
    println(result) // 값을 유지하여 5가 출력
}

class Calc {
    fun addNum(a: Int, b: Int, add: (Int, Int) -> Unit) { // 람다식 add에는 반환값이 없음
        add(a, b)
    }
}
```
위코드와 같이 result는 람다식 내부에서 재할당 되어 사용되는데 이때 할당된 값은 유지되 출력문에서 사용 될수 있게 된다.

예제
```kotilen
// 길이가 일치하는 이름만 반환
fun filteredNames(length: Int) {
    val names = arrayListOf("Kim", "Hong", "Go", "Hwang", "Jeon")
    val filterResult = names.filter {
        it.length == length // 바깥의 length에 접근 
    }
    println(filterResult)
}
...
filteredNames(4)
```
이렇게 클로저 사용시 내부의 람다식 함수에서 외부 함수의 변수에 접근해 처리 효율성 상승 완전히 다른 함수에서 변수의 접근을 제한할 수 있다. 


## 코틀린의 표준 라이브러리

람다식을 사용하는 코틀린의 표준 라이브러리에서 let,apply,with,also,run 등 여러 가지 표준 함수를 활용해 코드의 효율을 높인다. 이러한 함수를 통해 기존의 복잡한 코드를 단순화 효율적으로 만든다.

### let()활용하기
let함수는 함수를 호출하는 객체 T를 이어지는 block의 인자로 넘기고 block의 결과값 R을 반환

```kotilen
// 표준 함수의 정의
public inline fun <T, R> T.let(block: (T) -> R): R { ... return block(this) }
```

T나 R은 let() 확장 함수를 사용하기 위해 어떤 자료형이더라도 사용할수 있도록 일반화한 문자, 형식 매개변수라고 한다. 예를 들어 정수형, 문자열, 특정 클래스의 객체등에 let()함수를 확장함수로 사용할수 있게 된다. 

```kotilen
    val score: Int? = 32
...
    // let을 사용해 null 검사를 제거
    fun checkScoreLet() {
        score?.let { println("Score: $it") } // ①
        val str = score.let { it.toString() } // ②
        println(str)
    }
```
 이 코드와 같이 let은 특정 선언 변수를 T요소로 받아 결정되는데 여기서 널 가능한 정수형 변수이다. 이변수는 Int의 객체라고 말할 수 있다. 

### null 가능성 있는 객체에서 let() 활용하기
let을 세이프 콜(?.)과 함께 사용하면 if(null!=obj)와 같은 null 검사 부분을 대체 할 수 있다.

```kotlin
obj?.let { // obj가 null이 아닐 경우 작업 수행 (Safe calls + let 사용)
    Toast.makeText(applicationContext, it, Toast.LENGTH_LONG).show()
}
```
따라서 이 코드는 obj가 널이 아닌 경우에만 let 블록 구문을 수행, 널이면 아무런 일도 하지 않게 된기에 NPE를 방지할 수 있다.

### 체이닝을 사용할 때 let() 활용하기
체이닝이란 여러 메서드 혹은 함수를 연속적으로 호출하는 기법 으로 let()함수를 체이닝 형태로 사용할 수 있다.
```kotlin
var a = 1
var b = 2

a = a.let { it + 2 }.let {
    val i = it + b
    i  // 마지막 식 반환
}
println(a) //5
```
코드에서처럼 첫 번쨰 a.let{...} 블록의 처리 결과를 다시한번 let{...}블록으로 넘겨서 처리할 수 있다.
코드의 가독성을 고려한다면 너무 많은 let을 사용하는 것은 권장되지 않는다.


## also()

also()는 함수를 호출하는 객체 T를 이어지는 block에 전달하고 객체 T 자체를 반환

```kotlin
// 표준 함수의 정의
public inline fun <T> T.also(block: (T) -> Unit): T { block(this); return this }
```
also는 let과 역할이 동일해 보이나, also는 블록 안의 코드 수행 결과와 상관없이 T인 객체 this를 반환
하게된다.

```kotlin
var m = 1
m = m.also { it + 3 }
println(m) // 원본 값 1
```
위 코드처럼 연산 결과인 4가 할당이 아니라 it의 값인 m의 본래값  1이 할당된다.

## apply()

apply()함수는 also()함수와 마찬가지로  객체 T를 이어지는 block에 전달하고 객체 T 자체를 반환 한다.

```kotlin
public inline fun <T> T.apply(block: T.() -> Unit): T { block(); return this }
```
apply()함수는 특정 객체를 생성하면서 함께 호출해야 하는 초기화 코드가 있는 경우 사용할 수 있다.


```kotlin
fun main() {
    data class Person(var name: String, var skills : String)
    var person = Person("Kildong", "Kotlin")

    // 여기서 this는 person 객체를 가리킴
    person.apply { this.skills = "Swift" }
    println(person)

    val retrunObj = person.apply { 
        name = "Sean" // ① this는 생략할 수 있음
        skills = "Java" // this 없이 객체의 멤버에 여러 번 접근
    }
    println(person)
    println(retrunObj)
}
```
apply는 확장 함수로서 person을 this로 받아온다 사실 클로저를 사용하는 방식과 같다. 따라서 객체의 프로퍼티를 변경하면 원본 객체에 반영되고 또한 이 객체는 this로 반환된다.

## run()

run()함수는 인자가 없는 익명 함수처럼 동작하는 형태로 단독 사용하거나 확장 함수 형태로 호출하는 형태
두 가지로 사용할 수 있다.

```kotlin
public inline fun <R> run(block: () -> R): R  = return block()
public inline fun <T, R> T.run(block: T.() -> R): R = return block()
```
독립적으로 사용할 때는 block에 처리할 내용을 넣어주며 마지막 식이 반환된다.

```kotlin
val a = 10
skills = run {
    val level = "Kotlin Level:" + a
    level // 마지막 표현식이 반환됨
}
```
할당 없이 사용할 때는 체이닝을 사용해 특정 결과에 대한 메서드 실행 할 수 있다.

```kotlin
  run {
        if (firstTimeView) introView else normalView
    }.show()
```

## with()
with() 함수는 인자로 받는 개체를 이어지는 block의 receiver로 전달하며 결과값을 반환, run()함수와 기능 거의 동일하며, run의 경우 receiver가 없지만 with에서는 receiver로 전달할 객체를 처리한다.

```kotlin
// 표준 함수의 정의
public inline fun <T, R> with(receiver: T, block: T.() -> R): R  = receiver.block()
```
with는 확장 함수 형태가 아니고 단독으로 사용되는 함수이다. with은 세이프 콜(?.)은 지원하지 않기에 let과 같이 사용기도 한다.

```kotlin
supportActionBar?.let {
    with(it) {
        setDisplayHomeAsUpEnabled(true)
        setHomeAsUpIndicator(R.drawable.ic_clear_white)    
    }
}
```
따라서 null의 경우를 조사하려면 run을 확장함수 형태로 사용하는 것이 좋다.

```kotlin
supportActionBar?.run {
    setDisplayHomeAsUpEnabled(true)
    setHomeAsUpIndicator(R.drawable.ic_clear_white)
}
```

## use()

보통 특정 객체가 사용된 후 닫아야 하는경우( ex) 파일받고 닫기)가 생기는데 use()를 사용하면 객체사용후 close()등을 자동적으로 호출해 닫아 줄 수 있다.

```kotlin
// 표준 함수의 정의
public inline fun <T : Closeable?, R> T.use(block: (T) -> R): R 
```
먼저 T의 제한된 자료형을 보면 Closeable?로 block은 닫힐 수 있는 객체를 지정해야 한다.

``` kotlin
fun main() {

    PrintWriter(FileOutputStream("d:\\test\\output.txt")).use {
        it.println("hello")
    }
}
```

PrintWirter은 파일을 열거나 새롭게 생성해 파일에 출력할 수 있다. 이때 use를 사용하는데 먼저 콘솔에 출력하듯 println을 통해 파일을 출력하고 이후 use는 열었던 파일을 닫아주는 작업을 내부에서 진행

## takeIf() 와 takeUnless()

takeIf()는 람다식이 true 이면 결과를 반환, takeUnIess()는 람다식이 false면 결과를 반환

```kotlin
// 표준 함수의 정의
public inline fun <T> T.takeIf(predicate: (T) -> Boolean): T?
  = if (predicate(this)) this else null
```

takeIf()함수의 정의에서 볼 수 있듯 predicate 는 T 객체를 매개변수로 받아오고, true이면 this 아니면 null을 반환 



# 05 클래스와 인터페이스 

## 추상클래스

추상 클래스 abstract라는 키워드와 함께 선언하며 추상 클래스로부터 일반적인 객체를 생성하는 방법으로 
인스턴스화 될 수 없다 

```kotlin
abstract class Vehicle
```

이 클래스를 설계할 때는 멤버인 프로퍼티나 메서드도 abstract로 선언될 수 있다.이때 추상프로퍼티나 추상 메서드로 부른다


```kotlin
// 추상 클래스, 주 생성자에는 비추상 프로퍼티 선언의 매개변수 3개가 있음
abstract class Vehicle(val name: String, val color: String, val weight: Double) {

    // 추상 프로퍼티 (반드시 하위 클래스에서 재정의해 초기화해야 함)
    abstract var maxSpeed: Double

    // 일반 프로퍼티 (초기 값인 상태를 저장할 수 있음)
    var year = "2018"

    // 추상 메서드 (반드시 하위 클래스에서 구현해야 함)
    abstract fun start()
    abstract fun stop()

    // 일반 메서드
    fun displaySpecs() {
        println("Name: $name, Color: $color, Weight: $weight, Year: $year, Max Speed: $maxSpeed")
    }
}
```

## 인터페이스

인터페이스는 클르사가 아니며 따라서 상속이라는 형태로 하위 클래스에 프로퍼티와 메서드를 전달하지 않는다. 그렇기 때문에 하위 클래스 보다는 구현 클래스라고 한다. 이런 구현 클래스는 인터페이스가 제시한 메서드들을 구체적으로 구현 한다는 것에 있으며 인터페이스는 구현 클래스들과 강한 연관을 가지지 않는다.

```kotlin
interface Pet {
    var category: String // abstract 키워드가 없어도 기본은 추상 프로퍼티
    fun feeding() // 마찬가지로 추상 메서드
    fun patting() { // 일반 메서드: 구현부를 포함하면 일반적인 메서드로 기본이 됨
        println("Keep patting!") // 구현부
    }
}
```

인터페이스에서 추상 클래스와 다르게 abstarct을 붙여 주지 않아도 기본적으로 추상 프로퍼티와 추상 메서드가 지정, 메서드에 기본 구현부가 있으면 일반 메서드로 기본 구현을 가지게 된다.


## 데이터 클래스

보통 데이터 전달을 위한 객체를 DTO라고 부른다. DTO는 구현 로직을 가지고 있지 않고 순수한 데이터 객체를 표현 하기 때문에 게터/세터 메서드를 가진다. 자바에서는 모두 정의하려면 소스 코드가 길어지나 코틀린에서는 간단하게 표현할 수 있다.

```kotlin
data class Customer(var name: String, var email: String)
```
데이터 클래스는 생성자는 최소한 하나의 매개변수를 가지며, 주 생성자의 모든 매개변수는 val, var로 지정된 프로퍼티여야하고, 데이터 클래스는 abstarac, open, sealed, inner 키워드를 사용할 수 없다.


## 중첩 클래스

코틀린에서 중첩 클래스는 기본적으로 정적 클래스처럼 다뤄진다. 중첩 클래스는 객체 생성 없이 접근할 수 있다.

```kotlin
class Outer {
    val ov = 5
    class Nested {
        val nv = 10
        fun greeting() = "[Nested] Hello ! $nv" // 외부의 ov에는 접근 불가
    }
    fun outside() {
        val msg = Nested().greeting() // 객체 생성 없이 중첩 클래스의 메서드 접근
        println("[Outer]: $msg, ${Nested().nv}") // 중첩 클래스의 프로퍼티 접근
    }
}

fun main() {
    // static 처럼 Outer의 객체 생성 없이 Nested객체를 생성 사용할 수 있음
    val output = Outer.Nested().greeting()
    println(output)

   // Outer.outside() // 에러! Outer 객체 생성 필요
    val outer = Outer()
    outer.outside()
}
```

Outer.Nested().greeting()과 같은 방법으로 중첩 클래스의 메서드가 객체 생성 없이 호출될 수 있다.

## 이너 클래스

이너 클래스는 클래스 안에 이너 클래스를 정의할 수 있다. 이때 이너 클래스는 바깥 클래스의 멤버들에 접근할 수 있다.

```kotlin
class Smartphone(val model: String) {

    private val cpu = "Exynos"

    inner class ExternalStorage(val size: Int) {
        fun getInfo() = "${model}: Installed on $cpu with ${size}Gb" // 바깥 클래스의 프로퍼티 접근
    }
}

fun main() {
    val mySdcard = Smartphone("S7").ExternalStorage(32)
    println(mySdcard.getInfo())
}
```

## 지역 클래스

지역 클래스는 특정 메서드의 블록이나 init 블록과 같이 블록 범위에서만 유효한 클래스, 블록 범위를 벗어나면 더이상 사용되지 않는다.

```kotlin
..
class Smartphone(val model: String) {

    private val cpu = "Exynos"
...
    fun powerOn(): String {
        class Led(val color: String) {  // 지역 클래스 선언
            fun blink(): String = "Blinking $color on $model"  // 외부의 프로퍼티는 접근 가능
        }
        val powerStatus = Led("Red") // 여기에서 지역 클래스가 사용됨
        return powerStatus.blink()
    } // powerOn() 블록 끝
}

fun main() {
...
    val myphone = Smartphone("Note9")
    myphone.ExternalStorage(128)
    println(myphone.powerOn())
}
```

## 익명 객체

자바에서는 익명 이너 클래스라는 것을 제공해 일회성으로 객체를 생성해 사용한다. 코틀린에서는 이와 같은 기능을 object 키워드를 사용하여 익명 객체로 같은 기능을 수행, 자바와 다른 점은 익명 객체 기법이 다중의 인터페이스를 구현할 수 있다는점이다.

```kotlin
interface Switcher { // ① 인터페이스의 선언
    fun on(): String
}

class Smartphone(val model: String) {
...
    fun powerOn(): String {
        class Led(val color: String) {  
            fun blink(): String = "Blinking $color on $model" 
        }
        val powerStatus = Led("Red")
        val powerSwitch = object : Switcher {  // ② 익명 객체를 사용해 Switcher의 on()을 구현
            override fun on(): String {
                return powerStatus.blink()
            }
        } // 익명(object) 객체 블록의 끝
        return powerSwitch.on() // 익명 객체의 메서드 사용
    }
}
...
```

## 실드 클래스

실드 클래스를 선언하려면 sealed 키워드를 class아 함께 사용한다. 실드 클래스는 그 자체로 추상 클래스와 같기 때문에 객체를 만들 수 없다. 또한 생성자도 기본적으로 private이고 private가 아닌 생서자는 허용되지 않는다. 실드 클래스는 같은 파일 안에서 상속이 가능하나 다른 파일에서는 상속이 불가능 하다. 블록 안에 선언되는 클래스는 상속이 필요한 경우 open 키워드로 선언될 수 있다.

```kotlin
sealed class Result {
    open class Success(val message: String): Result()
    class Error(val code: Int, val message: String): Result()
}
```

# 06 제네릭과 배열

## 제네릭

제네릭은 클래스 내부에서 사용할 자료형을 나중에 인스턴스로 생성할 때 확정한다. 제네릭이 나오게 된 배경은 자료형의 객체들을 다루는 메소드나 클래스에서 컴파일 시간에 자료형을 검사해 적당한 자료형을 선택할 수 있도록 하기 위해서 이다. 제네릭을 사용하면 객체의 자료형을 컴파일 시에 체크하기 때문에 객체 자료형의 안정성을 높이고 형 변환 번거로움이 줄어든다

```kotlin

class Box<T>(t: T) { // 제네릭을 사용해 형식 매개변수를 받아 name에 저장
    var name = t
}
fun main() {
    val box1: Box<Int> = Box<Int>(1)
    val box2: Box<String> = Box<String>("Hello")

    println(box1.name)
    println(box2.name)
}

```

## 가변성

가변성을 지정하는 두가지 방법이 있다. 선언 지점 변성이란 클래스를 선언하면서 클래스 자체에 가변성을 지정하는 방식으로 클래스에 in/out을 지정할 수 있다. 선언하면서 지정하면 클래스의 공변성을 전체적으로 지정하는 것이기에 클래스를 사용하는 장소에서는 따로 자료형을 지정해 줄 필요가 없음.

```kotlin
class Box<in T: Animal>(var item: T)
```

사용 지점 변성은 메서드 매개변수에서 제네릭 클래스를 생성할 때와 같이 사용 위치에서 가변성을 지정하는 방식이다. 이것은 형식 매개변수가 있는 자료형을 사용할 떄 마다 해당 형식 매개변수를 하위 자료형이나 상위 자료형 중 어떤 자료형으로 대체할 수 있는지 명시 해야함

```kotlin
class Box<T>(var item: T)

...

fun <T> printObj(box: Box<out Animal>) {
    val obj: Animal = box.item // item의 값을 얻음(get)
    println(obj)
}
```

## 코틀린 배열

배열은 동일한 자료형의 데이터를 연속적으로 나열한 형태이며, 기본적으로 배열은 1차원적으로 순서 번호에 해당하는 색인과 값이 들어있는 자료형에 따른 요소의 저장 공간을 가지고 있다. 코틀린에서는 여러가지 자료형을 혼합해 구성, 기본적인 배열을 생성하기 위해서는 arrayOf()나 Array()생성자를 사용해 배열을 만들며, 만일 빈 상태 배열을 지정하는 경우 arrayOfNulls()을 사용할 수 있다.

```kotlin
val numbers = arrayOf(4, 5, 7, 3) // 정수형으로 초기화된 배열
val animals = arrayOf("Cat", "Dog", "Lion") // 문자열형으로 초기화된 배열
...
for (element in numbers) { // 정수형으로 초기화된 배열 출력하기
    println(element)
}
```
  
## 배열에 요소 추가하고 잘라내기

배열이 일단 정의되면 고정되기 때문에 새로 할당하는 방법으로 추가하거나 잘라낼 수 있다.

```kotlin
val arr1 = intArrayOf(1, 2, 3, 4, 5) // 다섯개로 고정된 배열

// 하나의 요소를 추가한 새 배열 생성
val arr2 = arr.plus(6)
println("arr2: ${Arrays.toString(arr2)}")
```

first()나 last()를 이용하여 첫 번쨰나 마지막 요소를 확인 


# 07 컬렉션

## 컬렉션의 종류

코틀린의 커렉션은 자바 컬렉션의 구조를 확장 구현한 것으로 ,List, Set, Map 등이 있으며 자바와는 다르게 불변형 가변형으로 나누어 컬렉션을 다룬다. 가변형 컬렉션 타입은 객체의 데이터의 추가/변경이 가능 하며, 불변형은 한번 할당하면 읽기 전용으로 된다. 자바는 오로지 가변형 이기 때문에 자바와 상호작용하는 경우 주의해야 한다.

## 리스트

List는 순서에 따라 정렬된 요소를 가지는 컬렉션으로, 가장 많이 사용되는 컬렉션이다. 먼저 값을 변경할 수 없는 불변형 List를 만들기 위해 헬퍼 함수인 listOf()를 사용한다. 값을 변경할 수 있는 가변형을 표현하기 위해서는 mutableListOf()를 사용하며, 인자는 원하는 만큼 가변 인자를 가지도록 vararg로 선언할 수 있다.

```kotlin
fun main() {
    // 불변형 List의 사용
    var numbers: List<Int> = listOf(1, 2, 3, 4, 5)
    var names: List<String> = listOf("one", "two", "three")

    for (name in names) {
        println(name)
    }
    for (num in numbers) print(num)  // 한 줄에서 처리하기
    println() // 내용일 없을 때는 한 줄 내리는 개행
}
```

## setOf()

setOf()는 읽기전용인 불변형 Set자료형을 반환
```
fun main() {
    val mixedTypesSet = setOf("Hello", 5, "world", 3.14, 'c') // 자료형 혼합 초기화
    var intSet: Set<Int> = setOf<Int>(1, 5, 5)  // 정수형만 초기화

    println(mixedTypesSet)
    println(intSet)
}
```
자료형을 혼합하거나 특정 자료형을 지정해 사용할 수 있으며, 중복 요소를 허용하지 않기에 중복된 요소 5가 결과에서 하나만 나타난다.

##  mutableSetOf()

 mutableSetOf() 함수로 추가 및 삭제가 가능한 집합을 만들 수 있다.  mutableSetOf()는 MutableSet 인터페이스 자료형을 반환하며, 내부적으로 자바의 LinkedHashSet을 만들어 낸다.
 
## Set의 자료구조

### hashSetOf()

hashSetOf()헬퍼 함수를 통해 해시 테이블에 요소를 저장할 수 있는 자바의 HashSet컬렉션을 만든다.

### sortedSetOf()

sortedSetOf()함수는 자바의 TreeSet 컬렉션을 정렬된 상태로 반환하며, 사용시 패키지를 임포트 해야한다. TreeSet은 저장된 데이터의 값에 따라 정렬되며 일종의 개선된 이진 탐색 트리를 사용해 자료구조를 구성한다.

### linkedSetOf()

linkedSetOf()함수는 자바의 LinkedHashSEt 자료형을 반환하는 헬퍼 함수다. 이름에서 알 수 있듯이 자료구조중 하나인 링크드리스트를 이용해 구현된 해시 테이블에 요소를 저장한다.
  

## mapOf()

mapOf()함수는 불변형 Map 컬렉션을 만들며, 키와 값의 쌍으로 이루어진 목록을 만들기 위해 다음과 같이 사용한다.

```kotlin
val map: Map<키자료형, 값자료형> = mapOf(키 to 값[, ...])
```
<br>
키와 쌍은 '키 to 값' 형태로 나타낸다.

```kotlin
fun main() {
    // 불변형 Map의 선언 및 초기화
    val langMap: Map<Int, String> = mapOf(11 to "Java", 22 to "Kotlin", 33 to "C++")
    for ((key, value) in langMap) { // 키와 값의 쌍을 출력
        println("key=$key, value=$value")
    }
    println("langMap[22] = ${langMap[22]}") // 키 22에 대한 요소 출력
    println("langMap.get(22) = ${langMap.get(22)}") // 위와 동일한 표현
    println("langMap.keys = ${langMap.keys}") // 맵의 모든 키 출력
}
```

## mutableMapOf()

mutableMapOf() 함ㅅ누는 추가, 삭제가 가능한 Map을 정의한다.


 





































