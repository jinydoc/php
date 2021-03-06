---
layout: php
title: "PHP"
keyword: "jinyphp, php"
breadcrumb:
- "oop"
- "interface"
---

# 인터페이스
---
클래스가 상속될 때 부모의 메서드나 프로퍼티는 자식 클래스에 전달됩니다. 또한 메서드가 변경된 경우 오버라이딩되어 다시 재정의 사용할 수 있었습니다.

만일 어떤 메서드는 꼭 필요하지만 상속받은 자식 클래스마다 서로 달라 다르게 매번 오버라이딩을 해야 한다면 어떻게 해야 될까요? 이런 경우에 부모의 메서드를 만들어 놓는 것은 의미가 없을 수 있습니다.

<br>

### 15.3.1 인터페이스 개념
---
인터페이스는 다수의 사람들의 클래스를 설계할 때 서로 약속한 규약과 같습니다. 자신이 만든 클래스를 다른 사람들과 협업하여 개발을 할 때 클래스의 규칙을 정의하는 것입니다. 인터페이스는 이 클래스는 어떻게 만들어야 한다는 지시와 같습니다.

이러한 클래스의 규칙들은 인터페이스 기능을 이용하여 매우 유용하게 사용할 수 있습니다. 

인터페이스로 정의된 클래스의 메서드들은 부모에서 미리 선언을 합니다. 인터페이스를 적용한 자식 클래스에서는 부모에서 지시한 인터페이스 규칙을 따라 만들라고 지시하는 것과 같습니다.

 

오픈소스 및 큰 규모의 프로젝트를 여러 사람이 함께 개발할 때 인터페이스는 매우 유용합니다. 또한 개발된 소스를 다수의 개발자들에게 배포할 경우 인터페이스 정의 기능은 불특정한 클래스의 오동작을 방지할 수 있습니다.

인터페이스로 상속받으면 자식 클래스는 인터페이스 규약에 따라서 메서드와 프로퍼티를 반드시 만들어야 합니다. 만들지 않으면 오류를 발생합니다.

<br>

### 15.3.2 인터페이스 문법
---
인터페이스는 class 키워드 대신에 interface 키워드를 사용하면 됩니다. 그 외의 사용법은 클래스를 선언하는 것과 매우 비슷합니다.
  
인터페이스 문법
```php
interface pages 
{
  public function index();
}
```

위의 인터페이스 사용 문법예서 interface 키워드와 안에는 메서드 이름과 매개변수, 반환값 등만 정의된 것을 확인할 수 있습니다. 메서드 들의 실제적인 코드의 몸체 { }는 작성하지 않습니다. 인터페이스에서 정의된 코드의 몸체는 인터페이스를 적용한 자식 클래스에서 작성합니다.

인터페이스 내부의 메서드는 반드시 public으로 속성을 설정합니다. public 속성을 지정하는 것은 interface 선언 및 방법에 대한 특성입니다. 

<br>

### 15.3.3 클래스 사용
---
이렇게 미리 설계된 인터페이스 규약은 클래스 상속과 유사한 문법으로 사용할 수 있습니다. 단지 클래스 생성 시 상속 키워드 extends 대신에 인터페이스 키워드 implements 를 사용하면 됩니다.

예제 파일 interface-01.php
```php
<?php
	interface pages
	{

		public function index();

	}

	class intro implements pages
	{
		public function index()
		{
			echo "인터페이스 소개 <br>";
		}
	}

	$obj = new intro();
	$obj->index();
	
?>
```

결과
```
인터페이스 소개 
```

위의 예제는 클래스의 인터페이스에 대한 예입니다. 먼저 pages 라는 이름의 인터페이스 규약을 정의합니다. intro라는 클래스를 생성할 때 이전에 정의한 pages라는 인터페이스 규약을 따릅니다.

pages 인터페이스를 따르는 클래스를 생성할 때 index()라는 메서드를 꼭 만들어 쓰라는 의미입니다. 

예제 파일 interface-02.php
```php
<?php
	interface pages
	{

		public function index();

	}

	class intro implements pages
	{

	}

	$obj = new intro();
	
?>
```

결과
```
[Fri May 12 15:43:33 2017] ::1:51820 [500]: /jinyphp/interface-02.php - Class intro contains 1 abstract method and must therefore be declared abstract or implement the remaining methods (pages::index) in C:\php-7.1.4-Win32-VC14-x86\jinyphp\interface-02.php on line 9
```

두 번째 예제는 선언된 인터페이스를 구현하지 않은 경우입니다. 인터페이스를 적용하면서 인터페이스에서 규약한 방식대로 사용하지 않을 때 PHP는 에러를 출력하고 실행을 중단합니다. 

<br>

### 15.3.4 인터페이스 확장
---
인터페이스도 extends 키워드를 통해 상속 확장이 가능합니다. 다음 예는 인터페이스의 확장입니다.

예제 파일 interface-03.php
```php
<?php
	interface a
	{
    	public function foo();
	}

	// a 인터페이스를 상속 받습니다.
	interface b extends a
	{
    	public function bar();
	}

	// 상속받은 b 인터페이스로 구현합니다.
	class c implements b
	{
    	public function foo()
    	{
    		echo "method is foo <br>";
    	}

    	public function bar()
    	{
    		echo "method is bar <br>";
    	}
    	
	}

	$obj = new c;

	// 인터페이스 a의 메서드입니다.
	$obj->foo();

	// 인터페이스 b의 메서드입니다.
	$obj->bar();

?>
```

결과
```
method is foo 
method is bar
```

위의 예는 인터페이스 상속에 대한 실험입니다. 인터페이스 b는 인터페이스 a를 상속을 받습니다.

<br>

### 15.3.5 인터페이스 다중 상속
---
다수의 인터페이스를 콤마(,)로 구분하여 한 번에 인터페이스를 상속받을 수 있습니다.

예제 파일 interface-04.php
```php
<?php
    interface a
    {
        public function foo();
    }

    interface b
    {
        public function bar();
    }

    interface c extends a, b
    {
        public function baz();
    }

    class d implements c
    {
        public function foo()
        {
            echo "method is foo <br>";
        }

        public function bar()
        {
            echo "method is bar <br>";
        }

        public function baz()
        {
            echo "method is baz <br>";
        }
    }

    $obj = new d;

    // 인터페이스 a의 메서드입니다.
    $obj->foo();

    // 인터페이스 b의 메서드입니다.
    $obj->bar();

    // 인터페이스 c의 메서드입니다.
    $obj->baz();

?>
```

결과
```
method is foo 
method is bar 
method is baz
```

위의 예제는 인터페이스 상속에 대한 예입니다.  
인터페이스 c는 인터페이스 a와 b를 직접 상속을 받습니다.

<br>

### 15.3.6 인터페이스 와 상속
---
기존 클래스의 상속과 인터페이스를 동시에 적용하여 새로운 클래스를 생성할 수 있습니다. 먼저 상속을 받고자 하는 클래스를 extends 키워드를 사용하여 상속을 합니다. 계속 같은 줄에서 이어서 implements 키워드를 통하여 적용하고자 하는 인터페이스를 지정할 수 있습니다.

예제 파일 interface-05.php
```php
<?php
	interface a
	{
    	public function foo();
	}

	// a 인터페이스를 상속 받습니다.
	interface b extends a
	{
    	public function bar();
	}

	class Bird {
		public function info() {
			echo "I am a {$this->name} <br>";
			echo "I am an bird <br>";
		}
	}

	class Penguin extends Bird implements b {
		var $name = "Penguin";
		
		public function foo()
    	{
    		echo "method is foo <br>";
    	}

    	public function bar()
    	{
    		echo "method is bar <br>";
    	}

	}

	$obj = new Penguin;

	// 상속 메서드입니다.
	$obj->info();

	// 인터페이스 a의 메서드입니다.
	$obj->foo();

	// 인터페이스 b의 메서드입니다.
	$obj->bar();

?>
```

결과
```
I am a Penguin 
I am an bird 
method is foo 
method is bar
```

위의 예는 인터페이스 상속에 대한 실험입니다.  
인터페이스 적용과 클래스를 동시에 상속을 받아 클래스를 생성을 합니다.

예제 파일 interface-06.php
```php
<?php
	interface a
	{
    	public function foo();
	}

	interface b 
	{
    	public function bar();
	}

	class Bird {
		public function info() {
			echo "I am a {$this->name} <br>";
			echo "I am an bird <br>";
		}
	}

	class Penguin extends Bird implements a, b {
		var $name = "Penguin";
		
		public function foo()
    	{
    		echo "method is foo <br>";
    	}

    	public function bar()
    	{
    		echo "method is bar <br>";
    	}

	}

	$obj = new Penguin;

	// 상속 메서드 입니다.
	$obj->info();

	// 인터페이스 a의 메서드 입니다.
	$obj->foo();

	// 인터페이스 b의 메서드 입니다.
	$obj->bar();

?>
```

결과
```
I am a Penguin 
I am an bird 
method is foo 
method is bar
```

위의 예제는 인터페이스 상속에 대한 예입니다.  
위의 예제는 앞의 interface-05.php와 동일한 동작을 합니다. 
인터페이스 a와 b를 콤마(,)로 구분하여 다중 적용하여 동작합니다.

<br>

### 15.3.7 인터페이스 상수
---
인터페이스 에서도 상수를 선언하여 사용할 수 있습니다.

예제 파일 interface-07.php
```php
<?php

	interface a{

    	const name = "interface a const";
	}

	echo a::name;
	echo "<br>";

	class b implements a
	{

	}

	class c extends b
	{
    	const age = 'Class c constant';
	}

	echo c::age;

?>
```

결과
```
interface a const
Class c constant
```

## 15.4 추상화
---
클래스의 상속과 오버라이딩, 인터페이스를 세 가지의 클래스 확장 기능을 배웠습니다. 하지만 이중 상속과 인터페이스 두 개는 함께 사용할 수 없습니다. 즉, 상속과 인터페이스 규약을 혼합하여 사용할 수 없습니다. 

이 두 개를 서로 같이 사용할 수 없는 이유는 상속과 인터페이스는 문법이 서로 매우 비슷합니다. 클래스명과 키워드 그리고 상속, 인터페이스명입니다. 

```
class 클래스명 extends 상속 클래스
{
}
```

```
class 클래스명 implements 인터페이스
{
}
```

두 개의 기능을 콤마(,)등을 이용하여 구분하거나 연장해서 사용할 수 없다는 것입니다.

 

추상화는 이러한 문법적 유사점과 두 가지 기능을 유지하면서 두 개의 기능을 같이 사용하기 위한 것이 방법입니다.  
즉, 추상화 = 상속 + 인터페이스 기능을 동시에 하고 싶을 때 사용되는 OOP 개념입니다.

<br>

### 15.4.1 추상화 문법
---
클래스에 추상화 사용법 또한 매우 간단합니다. 추상화 설정은  클래스명 또는 메서드 앞에 새로운 추상화 키워드 abstract를 같이 선언만 해주면 됩니다.

|문법|
```
abstract class 추상화 클래스
{
    // 추상화: 인터페이스
    abstract public function 메서드();

    // 공통 메서드
    public function copyright() {
        echo "copyright all Right JinyPHP";
    }
}

class 클래스명 extends 추상화 클래스
{
    public function 메서드() {
        return "abstract Method";
    }
}
```

클래스를 정의할 때 abstract 키워드를 이용하여 추상화 클래스와 메서드 등을 생성합니다.  
추상화로 선언한 메서드들은 인터페이스와 같이 자식 클래스에서 반드시 선언해야 합니다.

추상화 클래스를 적용하는 방법은 상속과 같이 `extends` 키워드로 사용합니다.

<br>

### 15.4.2 추상화 예제

예제 파일 abstract-01.php
```
<?php

    // 추상화 클래스를 선언합니다.
    abstract class a
    {
        // 확장 시 구현부가 필요한 메서드 정의
        abstract public function isAdult($age);
        
        public function copyright ()
        {
            // 본 메서드 함수는 대체되지 않습니다.
            echo "copyright all Right JinyPHP";
        }
    }

    // 추상화 적용
    class b extends a
    {
        // 추상화 인터페이스를 구현
        public function isAdult($age)
        {
            if ($age>=18) return true; else return false;
        }
    }

    $obj = new b();

    // 추상화에 선언된 일반 메서드를 상속, 호출 가능합니다.
    $obj->copyright();

    if ($obj->isAdult(18)){
        echo "성인입니다.";
    } else {
        echo "미성년입니다.";
    }

?>
```

결과
```
copyright all Right JinyPHP 성인입니다.
```

위의 예제를 보면 추상화 클래스는 일반 클래스처럼 프로퍼티와 메서드 등을 구현할 수 있습니다. 
또한 자식 클래스에서 다시 구현 처리해야 하는 인터페이스는 abstract 키워드를 추가하여 함께 선언합니다.

추상화 클래스를 상속받은 자식 클래스는 부모의 메서드 기능도 같이 상속받아 호출 사용 가능합니다. 
또한 abstract로 선언한 인터페이스 메서드를 같이 구현해야 합니다.

추상화에서 선언된 인터페이스를 구현하지 않은 경우 PHP는 에러를 출력하고 PHP 코드를 더 이상 실행하지 않습니다. 
이것은 인터페이스 규약을 따르지 않는 동작과 유사합니다.
