# 목차
- [목차](#목차)
  - [파일 입출력](#파일-입출력)
  - [Writer(출력)](#writer출력)
  - [Reader(입력)](#reader입력)
  - [파일입출력 예제](#파일입출력-예제)
  - [File(파일 정보)](#file파일-정보)
## 파일 입출력
	Stream이라는 연결통로를 통해 원본 데이터가 알맞는 인코딩 방식으로 전송된다.
	byte단위로 입출력되기 때문에 개별처리이며, 상세 연산이 필요하지 않다면
	Buffer를 사용한 입출력을 권장한다. Buffer를 사용하면 일괄처리가 가능해진다.

	※ 인코딩 방식
		인코딩 방식은 완성형과 조합형이 있다.
		- 완성형: 각, 간, 갇, 갈, 감, ... , 갛, ...
		- 조합형: ㄱ + ㅏ + ㄱ

		조합형이 효율적이며 byte단위로 데이터를 전송할 때 고정된 byte가
		아니기 때문에 가변형 인코딩 방식을 선호한다.
		조합형이면서 가변형인 인코딩 방식은 UTF-8이며, 전 세계에서 가장 많이
		사용되는 방식이다.


## 	Writer(출력)
		BufferedWriter: 버퍼를 사용한 출력 클래스
		FileWriter: 전달한 경로의 파일을 출력하기 위한 목적으로 열어준다.
			    전달한 경로에 파일이 없다면 새롭게 만든 후 열어준다.
---
##	Reader(입력)
		BufferedReader: 버퍼를 사용한 입력 클래스
		FileReader: 전달한 경로의 파일을 입력하기 위한 목적으로 열어준다.
			    전달한 경로에 파일이 없다면 FileNotFoundException이 발생한다.
```java
public class FileTest {
//	throws는 해당 메소드를 사용한 쪽으로 예외를 발생시킨다.
//	따라서 메소드 내에서는 throws에 작성한 예외가 발생하지 않는다.
	public static void main(String[] args) throws IOException{
//		절대 경로: 어디에서 작성해도 찾아갈 수 있는 경로, "대한민국 서울시 강남구 역삼동 123-22 빌딩 302호", "C:/a/b"
//		상대 경로: 현재 위치에 따라 변경되는 경로, "직진해서 우회전하세요", "../../a/b", "./a", "a"
		
//		BufferedWriter bufferedWriter = new BufferedWriter(new FileWriter("test.txt", true));
//		bufferedWriter.write("홍길동");
//		bufferedWriter.close();
		
		BufferedReader bufferedReader = null;
		
		try {
			bufferedReader = new BufferedReader(new FileReader("test.txt"));
		} catch (FileNotFoundException e) {
			// TODO Auto-generated catch block
			e.printStackTrace();
		}
		
		
	}
}
```
---
## 파일입출력 예제
```java
public class FileTask {
	public static void main(String[] args) throws IOException{
//		음식을 4개 출력
//		BufferedWriter bufferedWriter = new BufferedWriter(new FileWriter("food.txt"));
//		String[] foods = {"스테이크", "오마카세", "햄버거", "한우"};
////		
//		Arrays.asList(foods).stream().forEach(food -> {
//			try {
//				bufferedWriter.write(food + "\n");
////				bufferedWriter.newLine(); 비추!
//			} catch (IOException e) {
//				e.printStackTrace();
//			}
//		});
//		bufferedWriter.close();
		
		
//		음식 모두 가져와서 콘솔에 출력
//		BufferedReader bufferedReader = new BufferedReader(new FileReader("food.txt"));
//		String line = null;
//		
//		while((line = bufferedReader.readLine()) != null) {
//			System.out.println(line);
//		}
//		bufferedReader.close();
//		
//		BufferedReader bufferedReader = new BufferedReader(new FileReader("food.txt"));
//		String line = null;
//		String temp = "";
//		
//		while((line = bufferedReader.readLine()) != null) {
//			if(line.equals("스테이크")) {
//				temp += "스파게티\n";
//				continue;
//			}
//			temp += line + "\n";
//		}
//		
//		bufferedReader.close();
//
//		BufferedWriter bufferedWriter = new BufferedWriter(new FileWriter("food.txt"));
//		bufferedWriter.write(temp);
//		
//		bufferedWriter.close();
		
//		햄버거 삭제
		BufferedReader bufferedReader = new BufferedReader(new FileReader("food.txt"));
		String line = null;
		String temp = "";
		
		while((line = bufferedReader.readLine()) != null) {
			if(line.equals("햄버거")) {
				continue;
			}
			temp += line + "\n";
		}
		
		bufferedReader.close();

		BufferedWriter bufferedWriter = new BufferedWriter(new FileWriter("food.txt"));
		bufferedWriter.write(temp);
		
		bufferedWriter.close();
		
	}
}
```



##	File(파일 정보)
		전달한 경로에 있는 파일의 정보를 담는 타입.
		디렉터리 생성, 해당 경로의 전체 파일 목록, 파일 삭제 등
---
