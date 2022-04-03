# 공부시작 설명

회사에서 하이브리드 앱을 사용하여 유지보수 개발을 해보았는데 앱개발을 해본적이 없어서 안드로이드 개발은 어떠한 것으로 많이 사용되는지 궁금하여 찾아보게 되었는데 현재는 구글에서 지원하는 코틀린으로 다들 넘어가는 추새라고 하여 이를 나도 경험하고 공부하기 위해 공부를 시작하였다.

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







