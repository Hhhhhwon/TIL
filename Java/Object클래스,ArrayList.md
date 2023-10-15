# 목차
- [목차](#목차)
  - [Object 클래스](#object-클래스)
    - [1. toString()](#1-tostring)
    - [2. equals()](#2-equals)
    - [3. hashCode()](#3-hashcode)
  - [알고리즘](#알고리즘)
  - [자료구조(저장공간)](#자료구조저장공간)
  - [컬렉션 프레임워크(Collection Framework)](#컬렉션-프레임워크collection-framework)
  - [List extends Collection](#list-extends-collection)
## Object 클래스
###	1. toString()
		항상 객체명을 출력할 때에는 toString()을 붙여서 출력해준다.
		따라서 객체명만 출력메소드에 전달하더라도 toString() 문자열 값이 출력된다.
		기본적으로 Object에서는 소속과 필드 주소를 문자열로 리턴해주지만,
		실사용에서는 불필요한 정보이기 때문에, 재정의한 뒤 필드의 정보를 확인하도록 구현한다.
		실무에서는 클래스 선언 시 각 필드의 초기화 여부를 확인하기 위해 toString()을 재정의하여 사용한다.
```java
class Sports {
	
	private String type;
	private int total;
	
	public Sports() {;}
	
	
	public Sports(String type, int total) {
		super();
		this.type = type;
		this.total = total;
	}

	public String getType() {
		return type;
	}

	public void setType(String type) {
		this.type = type;
	}

	public int getTotal() {
		return total;
	}

	public void setTotal(int total) {
		this.total = total;
	}


	@Override
	public String toString() {
		return "Sports [type=" + type + ", total=" + total + "]";
	}
	
	
	
	
}

public class ToStringTest {
	public static void main(String[] args) {
		Sports sports = new Sports("농구", 5);
		System.out.println(sports);
	}
}
```


###	2. equals()
		주소값 비교(==),
		객체 주소 비교가 아닌 특정 필드를 비교해야 할 경우 재정의한다.
```java
class Student {
	private int id;
	private String name;
	private int age;
	
	public Student() {;}

	public Student(int id, String name, int age) {
		super();
		this.id = id;
		this.name = name;
		this.age = age;
	}

	public int getId() {
		return id;
	}

	public void setId(int id) {
		this.id = id;
	}

	public String getName() {
		return name;
	}

	public void setName(String name) {
		this.name = name;
	}

	public int getAge() {
		return age;
	}

	public void setAge(int age) {
		this.age = age;
	}

	@Override
	public String toString() {
		return "Student [id=" + id + ", name=" + name + ", age=" + age + "]";
	}
	
	
	@Override
	public boolean equals(Object obj) {
		if(this == obj) {
			return true;
		}
		if(obj instanceof Student) {
			Student anotherStudent = (Student) obj;
			if(this.id == anotherStudent.getId()) {
				return true;
			}
		}
		return false;
	}
	
}
```
```java

public class EqualsTest {
	
	
	public static void main(String[] args) {
		Student student = new Student(1, "홍길동", 20);
		
		if(student.equals(new Student(1, "홍길동", 20))) {
			System.out.println("대여 완료");
			
		}else {
			System.out.println("도난 신고중");
		}
		
		
		
//		String data1 = "ABC";
//		String data2 = "ABC";
//		String data3 = new String("ABC");
//		String data4 = new String("ABC");
//		
//		System.out.println(data1 == data2);
//		System.out.println(data1.equals(data2));
//		System.out.println(data3 == data4);
//		System.out.println(data3.equals(data4));
	}
}
```
###	3. hashCode()
		JVM에서 관리하는 중복 없는 값. 실제 메모리에 할당되는 주소와 다르다.
		※ 컬렉션 프레임워크 챕터에서 재정의 목적을 이해하도록 한다.

```java
public class HashCodeTest {
	public static void main(String[] args) {
		Random random = new Random();
		System.out.println(random.hashCode());
	}
}
```

---
## 알고리즘
	어떤 문제가 발생되었을 때 해결할 수 있는 절차 혹은 순서

## 자료구조(저장공간)
	의미 없는 데이터를 하나의 정보로 만들어주는 알고리즘들의 집합.
	수집한 자료를 저장하는 방법.

## 컬렉션 프레임워크(Collection Framework)
	많은 데이터를 쉽고 효과적으로 관리할 수 있는 표준화된 방법을 제공하는 클래스들의 집합.
	

## List extends Collection
	- Vector: 용량 관리, 보안성 강화, 처리량 감소
	- LinkedList: FILO로 인해 넣을 때는 빨라도 원하는 위치의 데이터를 가져오는 것이 상대적으로 느리다.
	- ArrayList: 인덱스로 데이터를 관리한다. 컬렉션 클래스 중 실무에서 가장 많이 사용되는 클래스이다.
		     배열의 특징인 인덱스를 이용하여 값을 저장하고 관리한다.

	※ 배열과 ArrayList의 차이
		배열은 길이에 제한을 두어야할 때 자주 사용되고,
		ArrayList는 몇 개의 데이터가 들어올 지 알 수 없을 때 사용한다.
```java
public class ArrayListTest {

	public static void main(String[] args) {
//		<?>: 제네릭(이름이 없는)
//		객체화 시 타입을 지정하는 기법
//		설계할 때에는 타입을 지정할 수 없기 때문에 임시로 타입을 선언할 때 사용한다.
//		따로 다운 캐스팅을 할 필요가 없으며, 지정할 타입에 제한을 줄 수 있다.
		
		ArrayList<Integer> datas = new ArrayList<Integer>();
		System.out.println(datas.size());
		datas.add(10);
		datas.add(30);
		datas.add(50);
		datas.add(60);
		datas.add(20);
		datas.add(70);
		datas.add(80);
		datas.add(90);
		System.out.println(datas.size());
		
		try {
			System.out.println(datas.get(10));
		} catch (Exception e) {
			System.out.println("인덱스 똑바로!");
		}
		
		Collections.shuffle(datas);
		System.out.println(datas);
		Collections.sort(datas);
		Collections.reverse(datas);
		System.out.println(datas);
		
//		추가(삽입)
//		50 뒤에 500 삽입
		if(datas.contains(50)) {
			try {
				datas.add(datas.indexOf(50) + 1, 500);
			} catch (Exception e) {
				System.out.println("익덱스 똑바로!");
			}
		}else {
			System.out.println("찾으시는 값이 없습니다.");
		}
		
//		for (int i = 0; i < datas.size(); i++) {
//			System.out.println(datas.get(i));
//		}
		System.out.println(datas);
		
//		수정
//		90을 9로 수정
		if(datas.contains(90)) {
			int prev = datas.set(datas.indexOf(90), 9);
			System.out.println(prev + " 수정 완료");
		}
		
//		for (int i = 0; i < datas.size(); i++) {
//			System.out.println(datas.get(i));
//		}
		
		System.out.println(datas);
		
//		삭제
//		80 삭제
//		1. 인덱스로 삭제
//		if(datas.contains(80)) {
//			int deletedData = datas.remove(datas.indexOf(80));
//			System.out.println(deletedData + " 삭제 완료");
//			System.out.println(datas);
//		}
//		2. 값으로 삭제
		if(datas.remove(Integer.valueOf(80))) {
			System.out.println("삭제 성공");
			System.out.println(datas);
		}		
		
	}
}
```