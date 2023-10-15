# 목차
- [목차](#목차)
  - [로그인회원가입List로 만들기](#로그인회원가입list로-만들기)
  - [Set extends Collection](#set-extends-collection)
  - [Speed Test ArrayList VS HashSet](#speed-test-arraylist-vs-hashset)
## 로그인회원가입List로 만들기
- User Filed 구성
```java
public class User {
	private String name;
	private String id;
	private String password;
	private String phone;
	
	public User() {;}

	public String getName() {
		return name;
	}

	public void setName(String name) {
		this.name = name;
	}

	public String getId() {
		return id;
	}

	public void setId(String id) {
		this.id = id;
	}

	public String getPassword() {
		return password;
	}

	public void setPassword(String password) {
		this.password = password;
	}

	public String getPhone() {
		return phone;
	}

	public void setPhone(String phone) {
		this.phone = phone;
	}

	@Override
	public String toString() {
		return "User [name=" + name + ", id=" + id + ", password=" + password + ", phone=" + phone + "]";
	}

	@Override
	public int hashCode() {
		final int prime = 31;
		int result = 1;
		result = prime * result + ((id == null) ? 0 : id.hashCode());
		return result;
	}

	@Override
	public boolean equals(Object obj) {
		if (this == obj)
			return true;
		if (obj == null)
			return false;
		if (getClass() != obj.getClass())
			return false;
		User other = (User) obj;
		if (id == null) {
			if (other.id != null)
				return false;
		} else if (!id.equals(other.id))
			return false;
		return true;
	}
	
}
```
- DB 
```java
  public class DBConnecter {
	public static ArrayList<User> users = new ArrayList<User>();
}
```
- Method
```java
public class UserField {
	public static String userId;
	public ArrayList<User> users = DBConnecter.users;
	private final int KEY = 3;
	
//	아이디 중복검사
	public User checkId(String id) {
//		빠른 for문, 향상된 for문, forEach
		for(User user : users) {
			if(user.getId().equals(id)) {
				return user;
			}
		}
		return null;
	}
	
	
//	회원가입
	public void join(User user) {
		user.setPassword(encrypt(user.getPassword()));
		users.add(user);
	}
	
//	로그인
	public boolean login(User user) {
		User userInDb = checkId(user.getId());
		if(userInDb != null) {
			if(userInDb.getPassword().equals(encrypt(user.getPassword()))) {
				userId = user.getId();
				return true;
			}
		}
		return false;
		
	}
	
//	로그아웃
	public void logout() {
		userId = null;
	}
	
//	비밀번호 변경(마이페이지)
	public void update(User user) {
		User userInDb = checkId(user.getId());
		userInDb.setPassword(encrypt(user.getPassword()));
	}
	
//	비밀번호 변경(비밀번호 변경 페이지)
	public boolean update(String password, String newPassword) {
		User foundUser = checkId(userId);
		if(foundUser.getPassword().equals(encrypt(password))) {
			foundUser.setPassword(encrypt(newPassword));
			return true;
		}
		return false;
	}
	
//	인증번호 제작(6자리)
	public String makeNumber(int count) {
		Random random = new Random();
		String number = "";
		for (int i = 0; i < count; i++) {
			number += random.nextInt(10);
		}
		return number;
	}
	
//	인증번호 전송
	public String sendNumber(String phone) {
		String api_key = "";
	    String api_secret = "";
	    Message coolsms = new Message(api_key, api_secret);
	    String number = makeNumber(6);
	    // 4 params(to, from, type, text) are mandatory. must be filled
	    HashMap<String, String> params = new HashMap<String, String>();
	    params.put("to", phone);
	    params.put("from", "01000000000");
	    params.put("type", "SMS");
	    params.put("text", "[인증번호]" + number);
	    params.put("app_version", "test app 1.2"); // application name and version

	    try {
	      JSONObject obj = (JSONObject) coolsms.send(params);
	      System.out.println(obj.toString());
	    } catch (CoolsmsException e) {
	      System.out.println(e.getMessage());
	      System.out.println(e.getCode());
	    }
	    return number;
	}
	
//	암호화
	public String encrypt(String password) {
		String encryptedPassword = "";
		for (int i = 0; i < password.length(); i++) {
			encryptedPassword += (char)(password.charAt(i) * KEY);
		}
		
		return encryptedPassword;
	}
}
```
- Login Main
```java
public class Login {
	public static void main(String[] args) {
		UserField userField = new UserField();
		User user = new User();
//		User user2 = new User();
		
		user.setId("hds1234");
		user.setName("홍길동");
		user.setPassword("1234");
		user.setPhone("01012341234");
		
//		user2.setId("hds12345");
//		user2.setName("홍길석");
//		user2.setPassword("4444");
//		user2.setPhone("0108889999");
		
		if(userField.checkId(user.getId()) == null) {
			
//			인증번호 발송
//			String number = userField.sendNumber(user.getPhone());
			String number = userField.makeNumber(6);
			System.out.println(number);
//			인증번호 검사
			System.out.print("인증번호: ");
			if(number.equals(new Scanner(System.in).next())){
				userField.join(user);
				System.out.println(DBConnecter.users);
			}else{
				System.out.println("인증번호를 확인해주세요");
			}
		}else {
			System.out.println("중복된 아이디");
		}
		
//		if(userField.checkId(user2.getId()) == null) {
//			userField.join(user2);
//			System.out.println(DBConnecter.users);
//		}else {
//			System.out.println("중복된 아이디");
//		}

		
		User userForLogin = new User();
		userForLogin.setId("hds1234");
		userForLogin.setPassword("1234");
		
		if(userField.login(userForLogin)) {
			System.out.println("로그인 성공");
			
		}else {
			System.out.println("로그인 실패");
			
		}
		
////		마이페이지
//		User foundUser = userField.checkId(UserField.userId);
//		foundUser.setPassword("6666");
//		
////		비밀번호 변경
//		userField.update(foundUser);
		
//		비밀번호 변경 페이지(30일 넘게 비밀번호 사용함)
		if(userField.update("1234", "8888")) {
			System.out.println("비밀번호 변경 완료, 다시 로그인 해주세요.");
//		로그아웃
			userField.logout();
//		재로그인
			userForLogin = new User();
			userForLogin.setId("hds1234");
			userForLogin.setPassword("8888");
			
			if(userField.login(userForLogin)) {
				System.out.println("로그인 성공");
				
			}else {
				System.out.println("로그인 실패");
				
			}
		}else {
			System.out.println("비밀번호를 확인하세요.");
		}
		
		
		
	}
}
```
 
## Set extends Collection
- HashSet
-	집합에서는 중복되는 원소를 포함할 수 없는 것 처럼
-	HashSet이라는 자료구조는 중복되는 값을 무시한다.
-	저장된 값들은 인덱스가 없기 때문에 순서가 없다.
-	값의 유무 검사에 특화되어 있는 자료구조이고
-	해시코드로 유무 검사가 진행되기 때문에 속도가 상대적으로 좋다.
```java
public class HashSetTest {
	public static void main(String[] args) {
//		데이터를 가져오고 싶을 때 순서를 부여해야 한다.
//		iterator가 정답이다.
//		HashSet<String> bloodTypeSet = new HashSet<String>();
		
//		bloodTypeSet.add("A");
//		bloodTypeSet.add("B");
//		bloodTypeSet.add("O");
//		bloodTypeSet.add("AB");
//		
//		Iterator<String> iter = bloodTypeSet.iterator();
//		
//		while(iter.hasNext()) {
//			System.out.println(iter.next());
//		}
//		
		
//		중복제거할 때 써라!
//	DBMS의 기본 구조가 Set이다!
		ArrayList<Integer> datas = new ArrayList<Integer>(Arrays.asList(1, 2, 3, 4, 5, 6, 7, 8, 9, 9, 9, 1, 2));
		datas = new ArrayList<Integer>(new HashSet<Integer>(datas));
	
		System.out.println(datas);
		
		
		HashSet<String> bloodTypeSet = new HashSet<String>();
		bloodTypeSet.add("A");
	bloodTypeSet.add("B");
		bloodTypeSet.add("O");
		System.out.println(bloodTypeSet.add("AB"));
	System.out.println(bloodTypeSet.add("AB"));
		System.out.println(bloodTypeSet.add("AB"));
		System.out.println(bloodTypeSet.add("AB"));
		System.out.println(bloodTypeSet.add("AB"));
		System.out.println(bloodTypeSet.add("AB"));
		System.out.println(bloodTypeSet.add("AB"));
		System.out.println(bloodTypeSet.add("AB"));
		System.out.println(bloodTypeSet.add("AB"));
		System.out.println(bloodTypeSet.add("AB"));
		
		System.out.println(bloodTypeSet.size());
	}
}
```
## Speed Test ArrayList VS HashSet
```java
public class SpeedTest {
	public static void main(String[] args) {
		final int SIZE = 10_000_000;
        final List<Integer> arrayList = new ArrayList<>(SIZE);//용량 정하기
        final Set<Integer> hashSet = new HashSet<>(SIZE);
        final int data = 9_000_000;

        IntStream.range(0, SIZE).forEach(value -> {
            arrayList.add(value);
            hashSet.add(value);
        });

        Instant start = Instant.now();
        arrayList.contains(data);
        Instant end = Instant.now();
        long elapsedTime = Duration.between(start, end).toMillis();
        System.out.println("array list search time : " + elapsedTime * 0.001 + "초");

        start = Instant.now();
        hashSet.contains(data);
        end = Instant.now();
        elapsedTime = Duration.between(start, end).toMillis();
        System.out.println("hash set search time : " + elapsedTime * 0.001 + "초");
	}
}
```