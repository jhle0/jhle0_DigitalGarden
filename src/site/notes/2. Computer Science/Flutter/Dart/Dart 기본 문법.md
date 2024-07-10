---
{"dg-publish":true,"permalink":"/2-computer-science/flutter/dart/dart/","tags":["dart","google","flutter"]}
---

``` table-of-contents

```
# [ Dart Overview   ]
---
- Google이 만든 언어
	=> UI에 최적화, 생상전인 개발환경, Fast on all platforms



## 2개의 Complier
#### Dart Web 
   => dart 코드 J.S 로 변환
#### Dart Native 
   => dart 코드를 여러 CPU 아키텍쳐에 맞게 변환
- IOS, Android, Windows, Linux, Mac 컴파일 가능 !



## JIT, AOT
- Just-In-Time -> dart VM 이 쓴 코드의 결과를 바로 화면에 보여줌 (개발 중일 때 사용)
- Ahead-In-Time -> 배포할 때 사용(빠름)



## Dart, Flutter
- 같은 Google에서 개발한 것이어서 => 상호 보완적이다!
- 따라서, Flutter에서 필요한 부분을 Dart 언어가 업그레이드 되면서 협력 관계가 된다.






# [ Variables ]
---
## Var
- 타입지정 X => var 사용
- 타입지정 O => String, int, ...

- 관습적으로 => 함수, 메소드 내부에 지역 변수 선언   =>  var
	-           => class에서 변수 , property 선언      =>  타입 지정



## Dynamic Type
- dynamic 키워드로 변수에 모든 데이터 타입이 들어가게 할 수 있다 -> 권장 X



## Null Safety
- 어떤 변수가 null 이 될 수 있음을 명시하는 것
	-  즉, 잘못된 상태의 변수를 참조하는 것을 막아준다
- ?를 붙여서 null값이 될 수도 있음을 표시함, ?가 없는 변수는 null 값이 들어갈 수 없다
```dart
void main() {
	String? name = 'leo';        // name에 null 값이 들어갈 수 있음을 표시
	name = null;
	
	if(name != null){              // name 이 null 이 아니라면 inNotEmpty 속성을 달라고 요청
		name.isNotEmpty;
	}
	
	name?.isNotEmpty;             // 위와 같은 기능!!!
}
```



## final
- 변수 수정 불가 (JS 에서 const 와 같음)
```dart
void main(){
	final name = "leo";
	name = 'fwfw'      // 오류 => 변수 수정 불가
}
```



## late
- 초기 데이터 없이 변수를 선언 하게 해준다    => Flutter에서 API 작업 할때 많이 사용
	- 즉, 아직은 어떤 데이터가 올지 모른다고 말해주는 것
```dart
void main() {
	late final String name;

	// do something...  ex) go to API

	name = "abc";       
}
```



## const
- compile-time constant를 만들어준다
- final 처럼 수정 불가 이지만 compile 하기 전에 알고 있어야 하는 값이다
	- 즉, final은 런타임 중에 만들어질 수 있음
	- const 는 앱스토어에 배포 하거나 사용자에 입력을 받기 전에 시스템이 알고 있어야 하는 값







  # [ Data Types ]
---
## Basic Data Types
- String, bool, int, double    => 모두 객체(Object)이다 !!!
	- 자료형에 들어가보면 class 인 것을 확인 가능
- int, double은 모두 num이라는 객체의 자식요소이다



## List
```dart
void main() {
	var numbers = [1, 2, 3, 4]
	List<int> numbers = [1, 2, 3, 4]     // 위와 같음 
}
```
- dart에서 리스트는 collection if 와 collection for 을 지원한다



## Collection If
```dart
void main() {
	var giveMeFive = true;
	var numbers = [
		1, 
		2, 
		3, 
		4, 
		if (giveMeFive) 5       // if 조건이 맞으면 리스트에 5 추가
	];

	print(numbers);    // [1, 2, 3, 4, 5]
}
```



## String Interpolation
- text에 변수를 추가하는 방법   =>   $ 사용
```dart
void main(){
	var name = 'leo';
	var age = 10;
	var greeting = "Hello my name is $name and I'm ${age + 2}."

	print(greeting)
}
```



## Collection For
```dart
void main(){
	var oldFriends = ['nico', 'lynn'];
	var newFriedns = [
		'lewis',
		'ralph',
		for (var firend in oldFriends) "❤️ $friend",
	];
	print(newFriends);    // ['lewis', 'ralph', '❤️ nico', '❤️ ralph']
}
```



## Maps
- 파이썬의 딕셔너리, JS의 객체와 같은 역할
- key: value 형태
```dart
void main() {
	var Players = {             // var은 Map<String, Object> 와 같은
		'name' = 'leo',
		'xp' = 123.4,
		'superPower' = true,
	};

	Map<int, bool> = {         // 이런식으로 명시적으롵 특정해서 정의 가능
		1: true,
		2: false,
		3: true,
	};
	
}

```



## Sets
- 중복된 값 X  => 모든 값들이 유니크한 값들
```dart
void main() {
	var numbers = {1, 2, 3, 4}
	numbers.add(1)
	numbers.add(1)

	print(numbers)       // {1, 2, 3, 4}	
}
```








# [ Functions ]
---
## Defining a Function
- '=>' 를 사용해서 하나의 표현식만 포함하는 함수는 더 간략화 가능(fat arrow syntax)
```dart
String sayHello(String name){
	return "Hello $name";
}

String sayHello(String name) => "Hello $name";     // 위와 같은 기능

num plus(num a, num b) => a + b;

void main(){
	print(sayHello('leo'))
}


```



## Named Parameters
- Positional parameters : 함수에 정의되어 있는 파라미터 순서대로 들어감
- named parameters : 순저 안지켜도 됨  =>   디폴트 값 or Required 사용
```dart
String sayHello({String name, int age, String country}){
	return "Hello $name, you are $age, and you come from $country";
}


void main(){          // named argument
	print(sayHello(
		age:  21,
		name: 'leo',
		country: 'Seoul'
	))       
}

```


- User가 parameter을 제공하지 않은 경우(Null 인 경우) => default value   or     required 사용
	- default value 즉 기본값을 정해주거나
	- required 를 사용하여 매개변수를 넘겨주지 않았을 때 동작하지 않게 한다
```dart
// defalut value
String sayHello({
  String name = 'anon',
  int age = 99,
  String country = '??',
}) {
  return "Hello $name, you are $age, and you come from $country";
}



// required 를 사용하면 사용자가 매개변수를 넘겨주지 않았을때 동작하지 않음
String sayHello({
  required String name,
  required int age,
  required String country,
}) {
  return "Hello $name, you are $age, and you come from $country";
}
```




## Optional Positional Parameters
- 몇개의 파라미터만 넘어오지 않았을때의 처리를 하고싶다면
	- [String? country = "?"]  이런 식으로 사용할 수 있다



## QQ Operator
- ?? 연산자는 왼쪽 값이 null 인지 체크해서 null이 아니면 왼쪽 값을 리턴하고 null이면 오른쪽 값을 리턴한다
```dart
String capitalizeName(String? name){
	if (name != null){
		return name.toUpperCase();
	}
	return 'ANON';
}


void main() {
	capitalizeName('leo');
	capitalizeName(null);
}
```
- 위 함수를 간단화 하면
```dart 
String capitalizeName(String? name) =>
	name != null ? name.toUpperCase() : 'ANON';

// 더 줄인다면
String capitalizeName(String? name) =>
	name?.toUpperCase() ?? 'ANON';
	
```




## Typedef
- 자료형에 사용자가 지정한 alias(별칭)을 지정할 수 있다
```dart
typedef ListOfInts = List<int>;

ListOfInts reverseList(ListOfInts list){
	var reversed = list.reversed;
	return reversed.toList();
}

void main() {
	print(reverseList([1, 2, 3]));
}

```









# [ Class ]
---
## Dart Class
```dart
class Player {
	final String name = 'leo';
	int xp = 1500;
	
	void sayHello(){
		print("Hi my name is $name")     // dart에서는 class method 내부에서 this를 쓰는 것을 권장하지 않는다
	}
}

void main() {
	var player = Player()   // new 키워드를 생략 가능하다
}

```





## Constructors
- 생성자는 어떤 객체가 생성과 동시에 유효함을 보장하는 역할을 합니다
	- 즉, 사용자가 지정한 인수를 class의 멤버 변수에 저장하기 위함이다
```dart
class Player {
	late final String name;    // 변수들의 값을 나중에 받을거라는 late 키워드 사용해야함
	late int xp;

	Player(String name, int xp){
		this.name = name;
		this.xp = xp;
	}
	
	void sayHello(){
		print("Hi my name is $name")    
	}
}

void main() {
	var player = Player('leo', 3000)
}
```

```dart
class Player {
	final String name;   // 밑 생성자에서 변수값이 즉시 초기화되므로 late 필요 없음
	int xp;

	Player(this.name, this.xp);   // 이런식으로 생성자 간략화 가능
	
	void sayHello(){
		print("Hi my name is $name")    
	}
}

void main() {
	var player = Player('leo', 3000)
	player.sayHello();
}
```



## Named Constructor Parameters
- 기본 생성자에서 파라미터를 넘기려면 순서를 기억해야한다
- 그리고 각 인자의 의미를 알  수가 없다 
	- 따라서, Named Constructor Parameters 사용 !
```dart
class Player {
	final String name;
	int xp;
	String team;
	int age;

	Player({
		required this.name, 
		required this.xp, 
		required this.team, 
		required this.age
	});
	
	void sayHello(){
		print("Hi my name is $name")    
	}
}

void main() {
	var player = Player(
		name: 'leo', 
		xp: 3000,
		team: blue,
		age: 10,
	);
	player.sayHello();
}
```




## Named Constructors
-  콜론( : ) 을 사용하여 특별한 생성자 함수를 만들 수 있다
```dart
class Player {
	final String name;
	int xp;
	String team;
	int age;

	Player({              // normal Constructor
		required this.name, 
		required this.xp, 
		required this.team, 
		required this.age
	});

	Player.createBluePlayer({     // named Constructor
		required String name,
		required int age,
	}) : this.age = age,    // 여기에 콜론을 넣음으로써 Dart에게 여기서 Player 객체를 초기화하겠다고 한것이다
		 this.name = name,
		 this.team = 'Blue',
		 this.xp = 0,
	
	void sayHello(){
		print("Hi my name is $name")    
	}
}

void main() {
	var player = Player.createBluePlayer(
		name: 'leo', 
		age: 10,
	);
	player.sayHello();
}
```




## Casecade Notation
- class의 변수를 바꿀때 사용할 수 있는 sugar syntax
```dart
void main() {
	var player = Player(name: 'aa', xp: 100, team: 'red')
	..name = 'bb'
	..xp = 200
	..team = 'blue';
}
```



## Enums
 - 개발자들의 실수를 줄여주는 역할 => 선택의 폽을 좁혀줌
```dart
enum Team{ red, blue }

void main() {
	var player = Player(name: 'aa', xp: 100, team: Team.red)
	..name = 'bb'
	..xp = 200
	..team = Team.blue;
}
```



## Abstract Classes
  - 추상클래스 - 다른 클래스들의 블루프린트 역할
	  - 매소드가 반환하는 값이 무엇인지만 결정
```

```

```dart
abstract class Human{
	void walk();
}
```


## Inheritance
- super 키워드 사용해서 부모 클래스의 요소 가져오기
```dart
class Human {
	final String name;

	Human(this.name);
	void sayHello() {
		print("Hi my name is $name")
	}
}

enum Team { blue, red }

class Player extends Human{
	final Team team;

	Player({
		required this.team, 
		required String name,
	}) : super(name);           // super을 사용해 부모클래스 name 할당하기

	@override
	void sayHello() {
		super.sayHello();        // super응 통해 부모클래스 method 가져오기
		print('and I play for ${team}');	
	}
}


```




## Mixins
- 생성자가 없는 class
- 상속할때 extends 필요 없음, with 사용
	- 플러그인 사용할 때 유용
```dart
class Strong {
	final double strengthLevel = 9999.9;
}

class QuickRunner {
	void runQuick() {
		print("ruuuuuuun!!")
	}
}



class Player with Strong, QuickRunner {}

class Horse with QuikRunner {}

class kid with Strong{}

```






