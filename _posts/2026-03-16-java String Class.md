---
layout: single
title:  "Java String Class"
categories: coding
tag: [Java]

---

# 자바 String 클래스
자바(Java)에서 String 클래스는 문자열을 다루기 위해 가장 빈번하게 사용되는 클래스입니다. 하지만 단순히 글자를 저장하는 용도를 넘어, 내부적으로는 메모리 효율과 보안을 위해 아주 독특한 방식으로 설계되어 있습니다.
핵심적인 특징들을 알기 쉽게 정리해 드릴게요.

# 1\. 불변성 (Immutability)
String 객체는 한 번 생성되면 그 값을 **변경할 수 없습니다.**
* 예를 들어, str + " world"와 같이 문자열을 합치는 연산을 하면 기존 문자열이 변하는 것이 아니라, 새로운 String 객체가 메모리에 생성됩니다.
* **장점:** 멀티쓰레드 환경에서 안전(Thread-safe)하며, 보안상 유리합니다.

⠀2. String Constant Pool
자바는 메모리 효율을 위해 JVM의 힙(Heap) 영역 안에 **String Constant Pool**이라는 특별한 저장소를 관리합니다.
* **리터럴 방식 ("abc"):** 같은 내용의 문자열이 이미 풀에 있다면 재사용합니다.
* **생성자 방식 (new String("abc")):** 풀과 상관없이 항상 새로운 객체를 힙 메모리에 생성합니다.

⠀
# 3\. 주요 메서드 활용법
자주 사용하는 메서드들을 표로 정리했습니다.
이전 문장과 표 사이에 반드시 빈 줄을 하나 만드세요.

| 메서드 | 설명 | 예시 |
|:---|:---|:---|
| `length()` | 문자열의 길이를 반환 | `"Hi".length()` → 2 |
| `charAt(int i)` | 특정 인덱스의 문자를 반환 | `"Java".charAt(0)` → 'J' |
| `substring(int start, int end)` | 부분 문자열 추출 | `"Hello".substring(0, 2)` → "He" |
| `equals(Object obj)` | **내용**이 같은지 비교 | `str1.equals(str2)` |
| `indexOf(String str)` | 특정 문자열의 위치를 찾음 | `"abc".indexOf("b") → 1` |
| `replace(old, new)` | 문자열 치환 | `"apple".replace("p", "b")` → "abble" |

다음 문장 시작 전에도 빈 줄을 두는 것이 좋습니다.

# 4\. 효율적인 문자열 관리: StringBuilder
String은 불변성 때문에 반복문에서 문자열을 계속 더하면 성능이 급격히 떨어집니다. 이때는 가변(Mutable) 객체인 StringBuilder를 사용하는 것이 좋습니다.
Java

StringBuilder sb = new StringBuilder();
sb.append("Hello");
sb.append(" World");
System.out.println(sb.toString()); // 하나의 객체 안에서 편집됨

**💡 팁:** 문자열 비교 시 ==은 메모리 주소를 비교하고, equals()는 실제 문자열 내용을 비교합니다. 자바에서는 **무조건 equals()를 쓰는 습관**을 들이는 것이 안전합니다!

# String 클래스 - 비교
자바에서 String을 비교할 때 가장 많이 하는 실수가 바로 **== 연산자**와 **equals() 메서드**를 혼동하는 것입니다. 이 둘은 비교하는 '대상' 자체가 완전히 다릅니다.

# 1\. == (주소값 비교) vs equals() (데이터 비교)
자바에서 문자열 비교의 핵심은 "주소(Reference)를 보느냐, 값(Value)을 보느냐"입니다.
* **== 연산자:** 두 객체가 메모리상의 **같은 주소**를 가리키고 있는지 확인합니다.
* **equals() 메서드:** 객체의 주소와 상관없이 실제 저장된 **문자열의 내용**이 같은지 확인합니다.

⠀비교 예시 코드

``` java
String str1 = "Java";
String str2 = "Java";
String str3 = new String("Java");

System.out.println(str1 == str2);      // true (상수 풀에 있는 같은 객체 공유)
System.out.println(str1 == str3);      // false (new로 생성 시 힙에 새로운 객체 생성)
System.out.println(str1.equals(str3)); // true (내용물은 "Java"로 동일)

``` 

# 2\. 문자열 비교의 다양한 방법들
상황에 따라 더 정밀한 비교가 필요할 때 사용할 수 있는 메서드들입니다.
이전 문장과 표 사이에 반드시 빈 줄을 하나 만드세요.

| 메서드 | 설명 | 비고 |
|:---|:---|:---|
| `equals()` | 대소문자를 구분하여 비교 | 가장 기본 |
| `equalsIgnoreCase()` | **대소문자를 무시**하고 비교 | `Admin` vs `admin` → `true` |
| `compareTo()` | 사전 순서(Unicode)로 비교 | 결과가 `0`이면 같음, 양수/음수면 순서 차이 |
| `startsWith()` | 특정 문자열로 시작하는지 확인 | 파일 확장자나 접두사 체크 시 유용 |
| `endsWith()` | 특정 문자열로 끝나는지 확인 | `filename.endsWith(".pdf")` |
| `contains()` | 특정 문자열이 포함되어 있는지 확인 | 부분 일치 검색 |

다음 문장 시작 전에도 빈 줄을 두는 것이 좋습니다.

# 3\. 주의해야 할 점: NullPointerException
equals()를 호출할 때 변수가 null이면 프로그램이 강제 종료될 수 있습니다. 이를 방지하기 위한 두 가지 팁이 있습니다.
**1** **리터럴을 앞에 두기:** "abc".equals(str) (추천)
**2** **Objects 클래스 활용:** Objects.equals(str1, str2) (null 체크를 알아서 해줌)

⠀
**결론:** 자바에서 문자열의 '값'을 비교하고 싶다면 고민하지 말고 **equals()**를 사용하세요!

# String 클래스 불변객체
자바의 String 클래스가 **불변 객체(Immutable Object)**라는 것은, 한 번 생성된 문자열의 내부 상태(데이터)를 절대 변경할 수 없다는 뜻입니다.
왜 자바 설계자들이 String을 이렇게 깐깐하게 만들었는지, 그 이유와 내부 동작 원리를 핵심만 짚어드릴게요.

# 1\. 불변성의 동작 원리
우리가 문자열을 수정하는 것처럼 보이는 코드를 작성해도, 실제로는 기존 객체가 변하는 것이 아니라 **새로운 객체**가 만들어지는 것입니다.
Java

String str = "Java";
str = str + " Script"; 
위 코드가 실행되면 메모리에서는 다음과 같은 일이 벌어집니다.
1 처음엔 "Java" 객체가 생성됩니다.
2 + 연산 시 "Java Script"라는 **완전히 새로운 객체**가 생성됩니다.
3 변수 str은 이제 새 객체의 주소를 가리키고, 기존 "Java" 객체는 참조를 잃고 나중에 가비지 컬렉터(GC)에 의해 정리됩니다.

⠀
# 2\. 왜 불변으로 만들었을까? (장점)
### ① 보안 (Security)
자바에서는 네트워크 연결, 파일 경로, 데이터베이스 연결 문자열 등을 모두 String으로 다룹니다. 만약 String이 가변적이라면, 메서드 인자로 전달된 경로가 중간에 해커에 의해 변조될 위험이 있습니다. 불변이기 때문에 전달받은 값을 믿고 사용할 수 있습니다.
### ② String Constant Pool (메모리 효율)
불변이기 때문에 동일한 문자열 리터럴을 공유해서 사용할 수 있습니다. 만약 값이 변할 수 있다면, 한 곳에서 값을 바꿨을 때 해당 문자열을 공유하던 모든 변수의 값이 의도치 않게 바뀌는 대참사가 일어날 것입니다.
### ③ 멀티쓰레드 안전 (Thread-Safe)
여러 쓰레드가 동시에 같은 문자열 객체에 접근해도 값이 변할 리 없으므로 별도의 동기화 처리가 필요 없습니다.
### ④ 캐싱을 통한 성능 향상
String은 불변이기 때문에 자신의 **해시코드(HashCode)**를 계산해서 내부에 캐싱해둡니다. 덕분에 HashMap의 키(Key)로 사용할 때 매번 계산할 필요가 없어 매우 빠릅니다.

# 3\. 불변성의 단점과 해결책
문자열을 수천 번, 수만 번 더하는 루프 문이 있다면 매번 새로운 객체가 생성되어 메모리가 낭비되고 성능이 떨어집니다.
* **해결책:** StringBuilder(비동기 최적화) 또는 StringBuffer(멀티쓰레드 안전)를 사용하세요. 이들은 내부 저장 공간을 가변적으로 관리하여 객체 생성 없이 문자열을 수정할 수 있습니다.

⠀
### 요약: String vs StringBuilder

| 구분 | String | StringBuilder |
|:---:|:---|:---|
| **가변성** | 불변 (Immutable) | 가변 (Mutable) |
| **연산** | 새로운 객체 생성 (메모리 낭비 가능성) | 기존 객체 수정 (효율적) |
| **권장 상황** | 문자열 공유, 단순 조회, 멀티스레드 안전 | 빈번한 문자열 추가/삭제 (`append` 등) |

다음 문장 시작 전에도 빈 줄을 두는 것이 좋습니다.

# String 클래스 - 주요 메서드
자바의 String 클래스는 문자열을 생성하고 조작하는 데 필요한 수백 개의 메서드를 제공합니다. 그중 실무에서 가장 많이 쓰이는 핵심 메서드들을 기능별로 분류해 정리해 드릴게요.

## 1\. 문자열 정보 조회
문자열의 길이나 특정 위치의 문자를 확인할 때 사용합니다.
* length(): 문자열의 길이를 반환합니다.
* isEmpty(): 길이가 0이면 true를 반환합니다.
* isBlank(): (Java 11+) 공백 문자만 있거나 비어있으면 true를 반환합니다.
* charAt(int index): 지정된 인덱스의 문자를 반환합니다. (0부터 시작)

⠀
## 2\. 문자열 비교 (중요!)
앞서 배운 것처럼 == 대신 다음 메서드들을 사용해야 합니다.
* equals(Object obj): 문자열의 내용이 같은지 비교합니다.
* equalsIgnoreCase(String str): 대소문자를 무시하고 내용이 같은지 비교합니다.
* contains(CharSequence s): 특정 문자열이 포함되어 있는지 확인합니다.
* startsWith(String prefix) **/** endsWith(String suffix): 특정 문자열로 시작하거나 끝나는지 확인합니다.

⠀
## 3\. 문자열 조작 및 변환
### String은 불변이므로, 아래 메서드들은 모두 **새로운 String 객체**를 반환합니다.
* substring(int begin, int end): 시작 인덱스부터 끝 인덱스 **전**까지의 문자열을 잘라냅니다.
* replace(target, replacement): 특정 문자를 찾아 다른 문자로 바꿉니다.
* toLowerCase() **/** toUpperCase(): 소문자 또는 대문자로 변환합니다.
* trim() **/** strip(): 문자열 앞뒤의 공백을 제거합니다. (strip()은 Java 11부터 지원하며 유니코드 공백까지 처리 가능)

⠀
## 4\. 문자열 분리 및 결합
데이터를 파싱하거나 합칠 때 필수적입니다.
* split(String regex): 정규 표현식을 기준으로 문자열을 나누어 **배열(String[])**로 반환합니다.
* join(CharSequence delimiter, CharSequence... elements): (Java 8+) 구분자를 넣어 여러 문자열을 하나로 합칩니다.
* valueOf(Object obj): 다양한 타입(int, double, boolean 등)을 문자열로 변환합니다.

⠀
## 5\. 실무 활용 예시 (Method Chaining)
메서드를 연속적으로 호출하여 코드를 간결하게 작성할 수 있습니다.
Java
``` java
String phone = "  010-1234-5678  ";
String cleanPhone = phone.trim().replace("-", ""); 

System.out.println(cleanPhone); // "01012345678"

```
### 
# StringBuilder - 가변 String
String이 "읽기 전용"의 단단한 성벽이라면, **StringBuilder**는 자유롭게 늘였다 줄였다 할 수 있는 "찰흙"과 같습니다.
왜 StringBuilder가 필요한지, 그리고 어떻게 사용하는지 핵심을 짚어드릴게요.

## 1\. 왜 StringBuilder를 쓰는가? (성능의 차이)
앞서 배운 것처럼 String은 **불변(Immutable)**입니다. 문자열을 더할 때마다 새로운 객체를 메모리에 생성하죠.
* **String 연산:** String a = "A" + "B" + "C"; -> 메모리에 "A", "B", "AB", "ABC" 객체가 모두 생성됨 (낭비 발생)
* **StringBuilder 연산:** 내부의 가변 버퍼(Buffer)에 문자를 추가함 -> **객체 생성이 단 한 번**만 일어남

⠀
## 2\. 주요 메서드 활용법
StringBuilder는 문자열을 조작하는 아주 강력한 도구들을 가지고 있습니다.
StringBuilder는 내부의 값을 직접 변경할 수 있는 가변(Mutable) 객체입니다.

| 메서드 | 설명 | 예시 |
|:---|:---|:---|
| `append()` | 문자열을 끝에 추가 (가장 많이 사용) | `sb.append("Java")` |
| `insert(int offset, String str)` | 특정 위치에 문자열 삽입 | `sb.insert(0, "Hi ")` |
| `delete(int start, int end)` | 특정 범위의 문자열 삭제 | `sb.delete(1, 3)` |
| `reverse()` | 문자열 순서를 뒤집음 | `"abc"` → `"cba"` |
| `toString()` | 완성된 결과를 **String으로 변환** | `String result = sb.toString()` |

작업이 끝나면 반드시 `toString()`을 호출해야 일반 String 변수에 담을 수 있습니다.
### 코드 예시: Method Chaining
StringBuilder의 메서드들은 자기 자신을 반환하기 때문에 마침표(.)로 계속 연결해서 쓸 수 있습니다. 이를 **메서드 체이닝**이라고 합니다.
``` java
StringBuilder sb = new StringBuilder("Hello");
String result = sb.append(" Java")
                  .insert(0, "🔥 ")
                  .reverse()
                  .toString();

System.out.println(result); // "avaJ olleH 🔥"

```
## 3\. StringBuilder vs StringBuffer
둘은 사용법이 거의 똑같지만, 딱 하나의 결정적인 차이가 있습니다.
* **StringBuilder**: 속도가 매우 빠릅니다. 하지만 멀티쓰레드 환경에서 안전하지 않습니다 (Thread-safe X). **보통의 경우 이걸 사용합니다.**
* **StringBuffer**: 조금 느리지만, 여러 쓰레드가 동시에 접근해도 안전합니다 (Thread-safe O).

⠀
## 💡 요약 및 권장 사항
**1** **단순한 문자열 결합** (2~3개): 그냥 String의 + 연산을 쓰셔도 무방합니다. (자바 컴파일러가 어느 정도 최적화를 해줍니다.)
**2** **반복문 안에서 결합**: **무조건 StringBuilder를 쓰세요.** 성능 차이가 수백 배 이상 날 수 있습니다.
**3** **최종 결과**: 조작이 끝났다면 반드시 .toString()을 호출해 다시 String으로 변환해서 사용하세요.

# String builder
StringBuilder는 자바에서 **"변경 가능한 문자열"**을 처리하기 위한 핵심 클래스입니다. String 객체가 가진 불변성(Immutability)의 한계를 극복하기 위해 설계되었죠.
핵심 내용을 작동 원리와 사용법 위주로 정리해 드릴게요.

# 1\. 왜 StringBuilder를 써야 할까?
자바의 String은 불변이라서 문자열을 더할 때마다 새로운 객체를 계속 생성합니다. 1만 번의 문자열 합치기를 한다면 1만 개의 쓰레기 객체가 메모리에 쌓이게 되죠.
**StringBuilder는 내부적으로 가변 버퍼(Buffer)**를 가지고 있어, 새로운 객체를 만들지 않고 그 안에서 문자를 추가, 삭제, 수정합니다.

# 2\. 주요 메서드 (조작의 달인)
StringBuilder는 문자열을 자유자재로 변형할 수 있는 강력한 기능들을 제공합니다.

| 메서드 | 기능 설명 | 코드 예시 |
|:---|:---|:---|
| `append()` | 문자열을 뒤에 추가 | `sb.append("!")` |
| `insert()` | 특정 위치에 삽입 | `sb.insert(0, "Start: ")` |
| `delete()` | 범위 지정 삭제 | `sb.delete(2, 5)` |
| `replace()` | 특정 범위 교체 | `sb.replace(0, 2, "Hi")` |
| `reverse()` | 문자열 뒤집기 | `sb.reverse()` |
| `toString()` | **String으로 변환** | `String s = sb.toString()` |

이 메서드들은 실행 후 자기 자신(this)을 반환하기 때문에 마침표(.)로 이어서 사용하는 '메서드 체이닝'이 가능합니다.

## 3\. 실무 활용 패턴: Method Chaining
StringBuilder의 메서드들은 수정된 자기 자신(this)을 반환합니다. 덕분에 여러 명령을 한 줄로 이어서 쓸 수 있어 코드가 매우 깔끔해집니다.
```  java
public class Main {
    public static void main(String[] args) {
        StringBuilder sb = new StringBuilder("Hello");

        // 메서드 체이닝 활용
        String result = sb.append(" Java")
                          .replace(0, 5, "Welcome")
                          .insert(7, " to")
                          .reverse()
                          .toString();

        System.out.println(result); // "avaJ ot emocleW"
    }
}
```
## 4\. StringBuilder vs StringBuffer
두 클래스는 사용법이 100% 동일하지만, 딱 한 가지 차이가 있습니다.
* **StringBuilder (추천):** 동기화를 지원하지 않아 **속도가 매우 빠릅니다.** 일반적인 단일 쓰레드 환경에서 사용합니다.
* **StringBuffer:** 동기화를 지원하여 멀티쓰레드 환경에서 안전(Thread-safe)하지만, 속도가 상대적으로 느립니다.

⠀
## 💡 요약하자면
**1** **조회 위주**거나 짧은 결합 → String 사용
**2** **반복문 안에서** 문자열을 계속 수정/결합 → StringBuilder 사용
3 마지막엔 반드시 **.toString()**으로 변환하여 사용

# String 최적화
자바 컴파일러와 JVM은 String이 불변 객체라는 점을 이용해 다양한 최적화 기법을 사용합니다. 우리가 무심코 쓰는 + 연산이나 리터럴 선언 뒤에는 성능을 위한 영리한 장치들이 숨어 있습니다.
주요 최적화 방식 3가지를 정리해 드릴게요.

# 1\. 컴파일 타임 최적화 (Literal Combination)
자바 컴파일러는 소스 코드를 바이트코드로 변환할 때, 변하지 않는 문자열 리터럴 결합을 미리 계산해 버립니다.
* **원래 코드:** String str = "Hello, " + "World";
* **최적화된 코드:** String str = "Hello, World";

⠀실행 시점에 더하기 연산을 수행하지 않기 때문에 런타임 오버헤드가 전혀 없습니다.

# 2\. 런타임 최적화 (String Concatenation)
변수가 포함된 문자열 결합(str1 + str2)은 컴파일 타임에 계산할 수 없습니다. 자바 버전이 올라감에 따라 이 부분의 최적화 방식이 진화해 왔습니다.
* **Java 8 이전:** 내부적으로 StringBuilder를 생성하여 append()를 호출한 뒤 toString()으로 변환합니다.
* **Java 9 이후:** StringConcatFactory와 invokedynamic을 사용하여 더 효율적이고 유연하게 문자열을 결합합니다. (매번 StringBuilder 객체를 생성하는 오버헤드를 줄임)

⠀
# 3\. String Interning (메모리 최적화)
### String.intern() 메서드는 해당 문자열이 **String Constant Pool**에 있는지 확인하고, 있으면 그 주소를 반환하며 없으면 풀에 등록합니다.
* **효과:** 동일한 내용의 문자열이 수만 개 생성될 상황에서 메모리를 획기적으로 절약할 수 있습니다.
* **주의:** 인턴 풀도 메모리 공간을 차지하므로, 무분별하게 사용하면 오히려 성능이 저하될 수 있습니다.

⠀
# 4\. 실무에서 놓치기 쉬운 최적화 팁
### ❌ 나쁜 예: 반복문 안에서의 결합
Java
``` java
String res = "";
for (int i = 0; i < 10000; i++) {
res += i; // 매 루프마다 새로운 String 객체 생성 (성능 최악)
}
```

### ✅ 좋은 예: StringBuilder 사용

``` java
StringBuilder sb = new StringBuilder();
or (int i = 0; i < 10000; i++) {
sb.append(i); // 기존 버퍼에 추가 (매우 빠름)
 }
String res = sb.toString();

```

# 5\. Java 11+strip() vs trim()
최신 자바에서는 공백 제거 시 trim()보다 strip() 사용을 권장합니다. strip()은 유니코드 공백까지 인식하며, 내부적으로 더 세밀하게 최적화되어 있습니다.

**요약하자면:** 단순한 결합은 자바가 알아서 최적화해주니 편하게 +를 쓰셔도 되지만, **반복문 내에서의 결합은 반드시** StringBuilder**를 직접 사용**하는 것이 성능 최적화의 핵심입니다.


# Method Chaining
**메서드 체이닝(Method Chaining)**은 여러 메서드 호출을 마침표(.)로 연결하여 한 줄의 문장처럼 실행하는 코딩 기법입니다. 자바의 StringBuilder나 Stream API에서 아주 흔하게 볼 수 있는 패턴이죠.
이 방식은 코드를 더 읽기 쉽고 간결하게 만들어줍니다.

## 1\. 메서드 체이닝의 핵심 원리
메서드 체이닝이 가능한 이유는 각 메서드가 실행을 마친 뒤 **자기 자신(객체의 주소값,** **this****)을 반환**하기 때문입니다.
* **일반적인 방식:** 메서드 호출 후 반환값을 변수에 저장하고, 그 변수로 다시 메서드 호출.
* **체이닝 방식:** 반환값이 곧 객체 자신이므로, 변수 없이 바로 다음 메서드를 연결.

⠀
## 2\. 코드 비교:StringBuilder 예시
### ❌ 체이닝을 사용하지 않을 때
객체의 참조 변수를 매번 써줘야 하므로 코드가 길어지고 중복이 발생합니다.
Java
``` java
StringBuilder sb = new StringBuilder("Hello");
sb.append(" Java");
sb.insert(0, "Hi, ");
sb.reverse();
String result = sb.toString();
```

### ✅ 체이닝을 사용할 때
마치 문장을 읽듯 자연스럽게 연결됩니다.

``` java
String result = new StringBuilder("Hello")
                    .append(" Java")
                    .insert(0, "Hi, ")
                    .reverse()
                    .toString();

```

## 3\. 직접 구현해보기 (커스텀 클래스)
자신만의 클래스에서도 메서드 마지막에 return this;를 추가하면 체이닝을 구현할 수 있습니다.

``` java
class Calculator {
    private int value = 0;

    public Calculator add(int n) {
        this.value += n;
        return this; // 자기 자신을 반환!
    }

    public Calculator subtract(int n) {
        this.value -= n;
        return this; // 자기 자신을 반환!
    }

    public void print() {
        System.out.println("Result: " + value);
    }
}

// 사용 예시
new Calculator().add(10).subtract(5).add(20).print(); // Result: 25
```


## 4\. 장점과 주의할 점
### 👍 장점
* **가독성 증가:** 코드가 간결해지고 의도가 명확해집니다.
* **불필요한 변수 감소:** 중간 단계의 임시 변수를 만들 필요가 없습니다.

⠀⚠️ 주의할 점
* **디버깅의 어려움:** 한 줄에서 여러 작업이 일어나므로, 에러 발생 시 정확히 어느 지점에서 문제가 생겼는지 파악하기 까다로울 수 있습니다. (줄 바꿈을 적절히 섞어주는 것이 좋습니다.)
* **반환 타입 확인:** 체이닝 중간에 다른 타입(예: void나 String)을 반환하는 메서드가 섞여 있으면 체인이 끊깁니다.