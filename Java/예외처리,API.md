# 목차
- [목차](#목차)
  - [예외 처리](#예외-처리)
  - [예외 처리 문법](#예외-처리-문법)
  - [예외 발생](#예외-발생)
  - [사용자 정의 예외](#사용자-정의-예외)
  - [API(Application Programming Interface)](#apiapplication-programming-interface)
  - [JAR 파일로 배포하기](#jar-파일로-배포하기)
  - [JAR 파일을 프로젝트에 추가하기](#jar-파일을-프로젝트에-추가하기)
## 예외 처리
	컴파일 시, 빌드 시, 런타임 시 오류가 발생하면
	이를 제어문으로 막을 수 있으나, 제어문으로도 막을 수 없는
	오류들을 직접 처리할 수 있어야 한다.

## 예외 처리 문법
```java
	try {
		예외가 발생할 수 있는 문장
		예외가 없을 때 실행할 문장

	} catch(예외이름 객체명){
		예외 발생 시 실행할 문장

	} catch(예외이름 객체명){
		예외 발생 시 실행할 문장

	} ...

	} finally {
		예외 발생 여부에 상관없이 무조건 실행할 문장
		※ 외부 장치와 연결했을 경우 다시 닫을 때 주로 사용한다.
	}
```

## 예외 발생
	직접 예외를 발생시키기 위해서는 예외 던지기를 사용해야 하며, 이 때에는 생성자 호출 전 throw 키워드를 사용한다.
	예) throw new BadWordException();

## 사용자 정의 예외
	기본적으로 제공되는 예외가 아닌 특정 상황에서 직접 예외를 만들어야 한다면, Exception 혹은
	RuntimeException을 상속받아서 예외 클래스를 선언해야 한다.
	Exception은 컴파일러가 체크를 하기 때문에 예외처리를 강제로 해야하고,
	RuntimeException은 컴파일러가 체크하지 않기 때문에 예외처리를 선택할 수 있다.
```java
    // RuntimeException : 컴파일러가 검사하지 않음(강제 종료 시키고 싶을 때 사용)
// Exception : 컴파일러가 검사함(강제 종료가 아닌 해당 상황 처리를 원할 때 사용)
public class BadWordException extends RuntimeException{
	
	public BadWordException(String message) {
		super(message);
	}
```
```java
 

public class Chatting {
	public static void main(String[] args) {
		Scanner sc = new Scanner(System.in);
		String message = null;
		
		System.out.print("상대방에게 보내는 메세지: ");
		message = sc.nextLine();
		
		if(message.contains("바보")) {
//			try {
				throw new BadWordException("비속어 사용");
//			} catch (BadWordException e) {
//				System.out.println("비속어는 사용하지 말아주세요!");
//			}
		}else {
			System.out.println(message);
		}
		
		
		
	}
}
```
```java
public class ExceptionTest {
	public static void main(String[] args) {
		int[] arData = new int[5];
		
		try {
			System.out.println(arData[0]);
			System.out.println("성공!");
		} catch (ArrayIndexOutOfBoundsException e) {
			System.out.println("실패..");
		} catch (Exception e) {
			e.printStackTrace();
		}
	}
}
```
```java


public class ExceptionTask {
	public static void main(String[] args) {
//		5개의 정수만 입력받기
//		- 무한 입력 상태로 구현
//		- q 입력 시 나가기
//		- 각 정수는 배열에 담기
//		- if문은 딱 한 번 사용하기

//		alt + shift + z : 영역 단축키(영역을 잡고 사용해야 한다)
		
		Scanner sc = new Scanner(System.in);
		String message = "번째 정수: ";
		int count = 0;
		int[] arData = new int[5];
		String temp = null;
		
		while(true) {
			count++;
			System.out.print(count + message);
			temp = sc.next();
			if(temp.equals("q")) {
				break;
			}
			
			try {
				arData[count - 1] = Integer.parseInt(temp);
				
			} catch (NumberFormatException e) {
				System.out.println("정수를 입력해주세요.");
				count--;
			} catch (ArrayIndexOutOfBoundsException e) {
				System.out.println("5개의 정수까지만 입력할 수 있습니다.");
				for (int i = 0; i < arData.length; i++) {
					System.out.print(arData[i] + " ");
				}
				System.out.println();
				break;
			} catch (Exception e) {
				System.out.println("알 수 없는 오류.");
				count--;
			}
		}
	}
}
```

---

## API(Application Programming Interface)
	개발에 필요한 라이브러리들의 집합
	선배 개발자들이 만들어 놓은 소스코드

	- 내부 API
		JDK 설치 시 제공해주는 기본 API
		docs.oracle.com/javase

	- 외부 API
		선배 개발자들이 개발한 패키지 및 클래스들을 의미한다.
		보통 JAR 파일로 배포하며 자바 프로젝트의 build path에 추가하여 사용할 수 있다.

## JAR 파일로 배포하기
-	배포할 클래스 또는 패키지 우클릭
-	 Export > JAVA/JAR file 선택 > Next
-	 destination을 원하는 경로로 선택
-	 Export Java source files... 체크
-	 Finish

## JAR 파일을 프로젝트에 추가하기
-	배포된 JAR파일을 다운 받기
-	 프로젝트 우클릭 > Build Path > Configure Build Path
-	 Libraries 탭 클릭 > ClassPath(안되면 ModulePath) 클릭 > Add External JARs
-	 저장된 경로의 .jar파일을 더블 클릭으로 추가 > Apply 클릭
-	 Orders and Exports 탭 클릭
-	 Select All 클릭 > Apply and Close

 API 코드
```java


public class MailTest {
	public static void main(String[] args) {
	      // 메일 인코딩
	       final String bodyEncoding = "UTF-8"; //콘텐츠 인코딩
	       
	       //원하는 메일 제목 작성
	       String subject = "메일 발송 테스트";
	       
	       String fromEmail = "내 이메일 주소";
	       String fromUsername = "내 이름";
	       
	       String toEmail = "tedhan1204@gmail.com"; // 콤마(,)로 여러개 나열
	       
	       final String username = "구글 계정 이름";         
	       final String password = "구글 계정 비밀번호";
	       
	       // 메일에 출력할 텍스트
	       String html = null;
	       StringBuffer sb = new StringBuffer();
	       sb.append("<h3>안녕하세요</h3>\n");
	       sb.append("<h4>테스트입니다.</h4>\n");    
	       html = sb.toString();
	       
	       // 메일 옵션 설정
	       Properties props = new Properties();    
	       props.put("mail.smtp.starttls.enable", "true");
	       props.put("mail.smtp.host", "smtp.gmail.com");
	       props.put("mail.smtp.auth", "true");
	       props.put("mail.smtp.port", "587");
	       props.put("mail.smtp.ssl.trust", "smtp.gmail.com");
	       props.put("mail.smtp.ssl.protocols", "TLSv1.2");
	       
	       try {
	         // 메일 서버  인증 계정 설정
	         Authenticator auth = new Authenticator() {
	           protected PasswordAuthentication getPasswordAuthentication() {
	             return new PasswordAuthentication(username, password);
	           }
	         };
	         
	         // 메일 세션 생성
	         Session session = Session.getDefaultInstance(props, auth);
	         
	         // 메일 송/수신 옵션 설정
	         Message message = new MimeMessage(session);
	         message.setFrom(new InternetAddress(fromEmail, fromUsername));
	         message.setRecipients(RecipientType.TO, InternetAddress.parse(toEmail, false));
	         message.setSubject(subject);
	         message.setSentDate(new Date());
	         
//	         // 메일 콘텐츠 설정
	         Multipart mParts = new MimeMultipart();
	         MimeBodyPart mTextPart = new MimeBodyPart();
	         MimeBodyPart mFilePart = null;
	//    
//	         // 메일 콘텐츠 - 내용
	         mTextPart.setText(html, bodyEncoding, "html");
	         mParts.addBodyPart(mTextPart);
//	               
//	         // 메일 콘텐츠 설정
	         message.setContent(mParts);
	    
	         // 메일 발송
	         Transport.send( message );
	         
	       } catch ( Exception e ) {
	         e.printStackTrace();
	       }
	}
}
```
---




























