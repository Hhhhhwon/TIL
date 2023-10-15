# 목차
- [목차](#목차)
	- [접근 권한 제어자(접근자)](#접근-권한-제어자접근자)
	- [Casting](#casting)
	- [추상 클래스](#추상-클래스)
	- [추상 클래스 선언](#추상-클래스-선언)
	- [인터페이스(interface): 틀](#인터페이스interface-틀)

## 접근 권한 제어자(접근자)
	default: 다른 패키지에서 접근 불가
	public: 모든 곳에서 접근 가능, 해당 파일의 메인 클래스일 경우만 사용 가능
	protected: 다른 패키지에서 접근 불가, 자식은 가능
	private: 다른 클래스에서 접근 불가, 메소드(getter, setter)로만 접근하자!
---
※ 모든 자식은 부모 타입이다.

## Casting
	1. up casting: 자식 값을 부모 타입으로 형변환
	2. down casting: up casting된 객체를 자식 타입으로 형변환
	※ 부모 값을 자식 타입으로 형변환 시 오류
```java
	class Car {
	
	public Car() {;}
	
	void engineStart() {
		System.out.println("열쇠로 시동 킴");
	}
	
}

class SuperCar extends Car{
	@Override
	void engineStart() {
		System.out.println("음성으로 시동 킴");
	}
	
	void openRoof() {
		System.out.println("지붕 열기");
	}
}

public class CastingTest {
	public static void main(String[] args) {
		Car matiz = new Car();
		SuperCar ferrari = new SuperCar();
		
//		up casting
		Car noOptionFerrari = new SuperCar();
		noOptionFerrari.engineStart();
		
//		down casting
		SuperCar fullOptionFerrari = (SuperCar) noOptionFerrari;
		fullOptionFerrari.openRoof();
		
//		오류
//		SuperCar brokenFerrari = (SuperCar) new Car();
		
//		instanceof : 조건식
//		객체 instanceof 타입 : 참 또는 거짓
		
		System.out.println(matiz instanceof Car);
		System.out.println(matiz instanceof SuperCar);
		System.out.println(ferrari instanceof Car);
		System.out.println(ferrari instanceof SuperCar);
		System.out.println(noOptionFerrari instanceof Car);
		System.out.println(noOptionFerrari instanceof SuperCar);
		System.out.println(fullOptionFerrari instanceof Car);
		System.out.println(fullOptionFerrari instanceof SuperCar);
		
	}
}
```
---
## 추상 클래스
	필드 안에 구현이 안된 메소드가 선언되어 있는 클래스를 추상 클래스라고 한다.
	이 때 구현되지 않은 메소드를 추상 메소드라고 부른다.
	반드시 재정의를 통해 구현을 해야지만 메모리에 할당되기 때문에
	"강제성"을 부여하기 위해서 추상 메소드로 선언한다.

## 추상 클래스 선언
	abstract class 클래스명 {
		abstract 리턴타입 메소드명(매개변수, ...);
		일반 메소드도 선언 가능
	}
```java
	public abstract class Electronics {
	public abstract void on();
	public abstract void off();
	
	public final void safe() {
		System.out.println("안전 장치 작동");
	}
}

public class WashingMachine extends Electronics {

	@Override
	public void on() {
		System.out.println("밀어서");
	}

	@Override
	public void off() {
		System.out.println("댕겨서");
	}
	
}
```


---
## 인터페이스(interface): 틀
	추상 클래스를 고도화시킨 문법.
	상수와 추상메소드만 존재한다.
	구현은 지정한 클래스에서 진행하고, 인터페이스를
	다른 클래스에 지정할 때에는 implements 키워드를 사용한다.
```java
	package interfaceTest;

public interface Pet {
	final static String nation = "한국";
	
	public void sitDown();
	public void waitNow();
	public void poop();
}
```
	