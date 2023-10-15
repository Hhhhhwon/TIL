### *목록*

---

# 1. 개발환경 만들기

1. [Oracle.com/kr](http://Oracle.com/kr) 접속→ 제품 → (하드웨어) Java 클릭 → 17 버전 다움
    1. 17이 LTS ⇒ 유지보수 지속적으로 해주는 버전
    2. window x64 Installer 설치
        - mac 에서는 ARM 기반(M1칩) Installer 다운 받기
2. Eclipse IDE(통합 개발 환경) → 3개월마다 최신 버전 배포
    1. Eclipse 는 사용 언어에 따른(C++, JS) 버전 설치
    2. 해당 수업은 BE / FE 모두 다루기 때문에 Web Developer 버전 다운
    3. 설치(PATH 설정하기 - Eclipse 설치하는 폴더나 workspace DIR 설정)

---

# 2. Eclipse 파일 실행

1. Window → preferences에서 encoding 검색하면 인코딩 관련 설정할 수 있음
    - Workspce 오른쪽 아래 보면 Text file encoding에서 UTF-8로 사용하기
        - 문자를 저장하는 방식
        - 맥이나 윈도우 모두 문자를 UTF-8로 사용하기 때문
    - Web - CSS files에서 Encoding 방식으로 Korean, EUC-KR(윈도우에서만 사용 가능) 가 되어 있는데 이를 UTF-8로 변경
        - HTML과 JSP도 마찬가지로 UTF-8로 변경하기
        - XML은 UTF-8로 설정되어 있음 → XML 파일은 UTF-8로만 작성할 수 있음
2. Space 검색 (공백 관련 설정)
    - Insert spaces for tabs : 탭 키를 사용해서 공백 입력
    - Formatter
        - 자동으로 줄맞춤 해주는 Eclips built-in ⇒ 타입 지정에 문제 있을 수 있믐
        - New로 Profile name을  My Style로 하고 확인
        - Indentation : tab 사용이 기본으로 설정되어 있는데 `space only`로 변경하기
            - Client-Side JavaScript도 똑같이 만들어주시
    - CSS: Editor
        - Indent using tabs
        - Indent using spaces
            - 스페이스 사용하는 걸로 설정하고 사이즈는 4로 설정
            - HTML, XML Editor도 동일하게 설정
3. JAVA 프로젝트 시작
    - Create a Project
    - Module 내에 있는 체크 없애기
4. 프로젝트, 패키지 폴더 생성
    - 이후 클래스 생성
        - Name : AppMain
        - psvm 지닌 채로 생성하기 체크
        - 클래스 파일 클릭하면 소스 코드로 열리고 만약 글씨 너무 작으면 Preferences → Colors and Font에 있는 글씨 크기

---

# 3. 자바 구조

- Eclipse 프로젝트를 만들면 자동으로 .settings, bin, src 폴더와 .classpath, .project파일을 생성해준다.
- 실제로 eclipse에서 위 경로의 폴더를 열 src 파일만 확인할 수 있다.
- workspace > lab_java > lab01_intro > src > com > itwill > intro
    - lab01_intro : 프로젝트명으로 설정했던 이름
    - 패키지를 만들때 `com.itwill.intro` 의 이름으로 만들었는데, `.`을 기준으로 오른쪽에 있는 문자가 하위 폴더로 생성되는 구조

## -1. 자바 프로그램 구조

- Class를 만들어서 작성한 것을 코드라고 함 (`.java` 확장자)
- code를 `.class` 라는 확장자의 컴퓨터에서 실행할 수 있는 바이트 코드로 구성된 파일로 컴파일하는 과정을 거쳐야 실행할 수 있음
- 이클립스에서 Run을 하면 자동으로 컴파일하여 실행해주는 것
- 개발자가 작성한 소스 코드는 `src` 폴더에 생성하고, 컴파일된 바이트 파일은 `bin` 폴더 내에 저장

---

# 4. 가장 간단한 자바 프로그램 만들기!

- 프로젝트 → 패키지 → 클래스 순으로 생성
    - 실제 패키지 이름과 해당 패키지 내 클래스 생성 시 위에 명시된 패키지 명은 일치해야 함.
- 클래스는 .java 확장자로 생성됨
- 수업 중 첫 클래스 파일
    
    ```java
    package com.itwil.introl; // (1)
    
    public class AppMain { // (2)
    
    	public static void main(String[] args) {	// (3)
    //		주석 (Comment) (5)-a inline comment
    /*
     * (5)-b block 주석(Comment) 
    */
    		System.out.println("안녕하세요.!");
    		System.out.println("Hello, Java!");
    	}
    
    } // (4)
    ```
    
    <aside>
    💡 소스 코드 수정 후 저장은 필수… `cntl + S`
    
    - 저장하지 않았다면 파일 탭에 별표가 있어
    - 중괄호로 시작을 했으면 꼭 닫아주어야 함!
    </aside>
    
    1. 패키지 선언문 
    : 자바의 실행문은 항상 패키지 선언문으로 시작하여야 한다. (주석이 먼저 나오는 것은 상관 X)
        1. 패키지는 `src` 폴더 하위에 생성한다.
        
        <aside>
        💡 패키지 명에 숫자를 붙이지 않아요!
        
        </aside>
        
    2. 클래스 선언 
    : 패키지 선언문 다음에 항상 나오는 클래스 선언.
        1. 자바의 모든 것은 클래스로 되어 있다.
    3. 메인 메서드 
        1. 프로그램의 시작 부분
        2. 항상 `public static void main(String[] args)`로 작성되어야 함.
        3. 메인 메서드의 종료는 자바 프로그램의 종료와 동일한 의미
    4. 클래스 선언 끝
        1. 닫는 중괄호는 끝난다는 의미가 있기 때문에 세미콜론을 안써도 된다.
    5. 주석 
    : 프로그램 설명 (내가 작성하는 코드들이 어떤 의미가 있는 코드인지 설명을 담아줄 때 사용. 자바 프로그램 실행 시 제외됨)
        1. 인라인 커맨트 (`// 요 모양 주석`)
            - 프로그램 내 한줄 한줄의 코드에 대한 설명을 작성할 때
        2. 블럭 주석(`/* … … **/*`) *:* 앞의 `/*` 치고 엔터 누르면 이클립스가 자동으로 닫는 부분을 만들어준다. 
            - 문서화 주석(documentation comment) : 클래스나 메서드에 대한 설명을 적을 때 사용

## 5 - 1. 프린트 프로그램 (문자열과 수)

```java
package com.itwill.print;

public class PrintMain {
//		메인 메서드 - 프로그램 시작
	public static void main(String[] args) {
		
		System.out.println("한 줄 출력");	// print line
		System.out.println("1 + 2"); // (1)
		System.out.println(1+2); // (2)
		
	}
}
```

1. `“”` : 문자열을 출력, 큰따옴표 내에 있는 그대로 출력
    1. 문자를 출력할 때는 반드시 따옴표가 있어야 한다
    2. `“”` 외부에 있거나 예약어, 변수명 등이 아닌 문자를 문자열로 표현해야 한다.
2. 1+2 를 계산한 값을 출력

### 위 프로그램에서 마지막 줄에 `1 + 2 = 3` 을 출력하고 싶다면?

 

```java
System.out.println("1 + 2 = 3"); // 1 + 2 = 3
System.out.println("1 + 2 = " + (1+2)); // 1 + 2 = 3
System.out.println("1 + 2 = " + 1+2); // 1 + 2 = 12
```

- 만약 소괄호가 없다면 `1 + 2 = 12`로 츨력됨
    - 문자열에 1과 2가 차례대로 더해지기 때문에 발생하는 문제
    - `1 + 2`를 우선 계산하고 싶다면 소괄호 필수

### print와 println의 차이

```java
System.out.print("Hello");
System.out.print("안녕");
```

- 위의 출력 결과 : `Hello안녕`
    - print`ln`은 ln(line)과 같이 출력 후 자동으로 줄바꿈을 해줌

- 만약 다음과 같다면 출력 결과는?
    
    ```java
    System.out.print("Hello");
    System.out.print("안녕");
    		
    System.out.println("jAVA");
    ```
    
    - `Hello안녕jAVA` : println의 경우 앞 뒤로 줄바꿈을 하는 것이 아니라 현재 커서 위치에서 출력 후에 줄바꿈을 하므로, $`JAVA`$가 우선 출력된 후 줄바꿈됨다.

 

### printf

```java
System.out.printf("문자열 포맷 : %d, %f, %s\n", 100, 3.14, "hello");
```

- %d : 해당 자리에 정수를 출력해라
    - digit
- %f : 해당 자리에 실수를 출력해라
    - float-point number
- %s : 해당 자리에 문자열을 출력해라
    - stirng
- %b : 해당 자리에 논리값(Boolean)을 출력하라.
    - 대소문자 모두 표현할 수 있다.
    - 만약 %b로 작성하면 true/false, %B로 작성하면 TRUE / FALSE로 출력된다.
- 만약 `%d`라고 써놓고 double인 100 대신 3.182379 등을 쓰면 에러가 난다.
- printf는 print와 마찬가지로 자동 줄바꿈이 제공되지 않는다.
- 문자열 내에 `\n` 으로 줄바꿈을 직접 표현해주어야 한다.
    - `\n`은 new line에서 온 표현이다.

```java
System.out.printf("%d + %d = %d", 1, 2, 1+2);
System.out.printf("%d + %d = %d", 1, 2, (1+2));
```

- Argument로 들어간 `1+2`는 소괄호가 필수는 아니지만 소괄호 쓰면 더 깔끔해 보이겠쥬?
- 다른 기호와 다르게 `%`를 문자열 안에 표시하고 싶다면 `%%`라고 쓰여야 한다.
    
    ```java
    System.out.printf("%d %% %d = %d\n", num1 , num2, num1 % num2);
    ```
    

---

<aside>
💡 JDK는 .java 확장자를 `.class` 확장자의 파일로 컴파일해준다.
컴파일은 사람이 작성한 프로그래밍 언어를 컴퓨터가 이해할 수 있는 바이트 코드로 변환시켜주는 과정이다.

JRE 또한 가지고 있는데, Java Runtime Environment의 약어로 자바 실행 환경을 의미한다.

</aside>