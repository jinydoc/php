---
layout: php
title: "PHP"
keyword: "jinyphp, php"
breadcrumb:
- "oop"
- "namespace"
---

# 네임스페이스
---
네임스페이스는 같은 유형의 클래스들을 그룹으로 묶어 관리할 수 있는 가상의 폴더와 같습니다. 다른 고급 언어에서는 네임스페이스 기능을 도입하여 클래스 패키지 방법을 제공했지만 PHP는 약간 늦게 지원된 감이 있습니다. 네임스페이스 기능은 PHP의 다양한 오픈소스 프로젝트를 통해 인기를 얻고 있는 기능입니다. 또한 PHP 패키지들을 만들 때 매우 중요하게 사용되는 개념이기도 합니다.

네임스페이스 기능은 PHP 5.3부터 지원됩니다.

<br>

### 15.6.1 네임스페이스의 개념
---
PHP를 포함한 프로그램 언어는 동일한 이름의 클래스명의 중복을 허용하지 않습니다. 즉, 실행 스크립트 안에 클래스명은 유일한 한 개의 이름만 사용 가능합니다. 중복해서 사용할 수 없습니다.

개발자에게 이름을 정의하는 것이란 쉽지 않습니다. 각각의 의미를 부여함과 동시에 실행 스크립트 안에서 동일한 이름이 중복되지 않아야 합니다. 이러한 이름의 규칙은 개발자 한 명일 때는 큰 영향이 없습니다. 만일 다수의 개발자들이 공동으로 대형 프로젝트를 제작할 때 클래스의 이름은 중복될 여지가 있습니다. 하지만 여러 개발자들이 함께 협업하여 만들거나, 공개된 소스들과 결합하기 위해서는 클래스 이름의 중복 문제가 자주 발생하곤 했습니다.

특히 오픈소스 등 다수의 개발자들이 협업하여 만들 때 동일한 클래스 이름 중복으로 충돌이 발생할 가능성이 매우 많습니다. 매번 수많은 개발자들이 클래스 이름을 실시간으로 중복 여부를 확인할 수는 없습니다. 이러한 문제점을 해결하기 위해서 도입된 기능이 가상의 클래스 폴더인 네임스페이스가 있습니다.

 

클래스들은 네임스페이스 형태로 그룹화되어 구분됩니다. 따라서 개발자 및 프로젝트별로 구분할 수 있는 네임스페이스를 각각 가지고 있습니다. 네임스페이스를 적용하면 같은 클래스 이름을 가지고 있다고 해도 서로 충돌하지 않습니다. 하지만 네임스페이스를 적용했다고 해서 실제적인 폴더를 가지거나 구분하지는 않습니다. 네임스페이스는 가상의 폴더 계층 형태로 나누어 관리하기 때문에 공동의 작업이나 소스가 공개된 오픈소스에 매우 유용한 클래스 관리 방법입니다.

<br>

### 15.6.2 네임스페이스 문법
---
네임스페이스를 적용하기 위해서는 PHP 스크립트 상단 `<?php` 다음에 작성합니다.

|문법|
```php
<?php
namespace 이름;
```
namespace 키워드 다음에 이름을 적으면 됩니다. namespace 키워드 다음의 문장은 해당 네임스페이스 경로를 적용받습니다.

네임스페이스는 여러 경로로 계층화할 수 있습니다. 마치 폴더 안에 또 다른 폴더를 만들 수 있는 것과 같습니다. 
서브 네임스페이스를 구분하는 방법은 백슬래시 `\`를 사용하면 됩니다.

하지만 통상적으로 네임스페이스를 계층적으로 사용할 때 첫 경로는 ‘벤더명’으로 사용하는 경우가 많습니다. 개발자 또는 소스를 개발한 회사의 이름을 벤더명으로 적을 때가 많습니다.

네임스페이스는 물리적인 폴더 구조로 나누어지지 않기 때문에 실제적으로 1:1 매칭이 되지 않습니다. 하지만 PSR-4 및 오토로딩 도입으로 네임스페이스 클래스를 폴더를 만들어 관리하고 있는 추세로 바뀌고 있습니다.

<br>

### 15.6.3 네임스페이스 적용
---
기존 함수 방식의 코딩을 할 때 두 개 이상의 동일함 함수 이름을 중복하여 사용할 수 없습니다. 이러한 함수명 중복 문제를 해결하기 위한 대안이 클래스라고 할 수 있습니다. 클래스도 선언할 때 PHP 실행 파일 안에서 두 개 이상의 동일한 클래스 이름을 중복하여 사용할 수 없습니다.

클래스의 중복 방지는 네임스페이스를 통해 할 수 있습니다. 네임스페이스가 적용된 클래스는 가상의 개념의 계층이 적용되어 동일한 클래스명도 서로 다르게 인식합니다. 하나의 PHP 실행 파일에서 네임스페이스로 구분된 동일한 클래스들을 동작시킬 수 있습니다.

<br>

### 15.6.3.1 전역 네임스페이스
---
네임스페이스를 적용하기 전에는 일반적으로 클래스를 작성할 때 클래스 키워드와 이름을 선언하고 바로 인스턴스를 생성하여 아래와 같이 사용했습니다.

예제 파일 namespace-01.php
```
<?php
	class members
	{
		public function setUsers($id)
		{
			echo "회원ID = $id";
		}
	}

	$obj = new members();
	$obj->setUsers(123);
?>
```

결과
```
회원ID = 123
```

이처럼 별도의 네임스페이스를 사용하지 않고 클래스(members)를 선언하여 사용하는 것을 전역 네임스페이스로 정의되었다고 표현합니다.

<br>

## 네임스페이스
---
다음 소스는 위의 예제 앞에 네임스페이스 키워드를 추가했습니다.

예제 파일 namespace-02.php
```php
<?php
	namespace jiny;

	class members
	{
		public function setUsers($id)
		{
			echo "회원ID = $id";
		}
	}

	// 네임스페이스 이름을 같이 적용
	$obj = new \jiny\members();
	$obj->setUsers(123);

	echo "<br>";
	// 현재 네임스페이스를 적용
	$obj2 = new members();
	$obj2->setUsers(123);

?>
```

결과
```
회원ID = 123
회원ID = 123
```

상단에 네임스페이스가 선언되면 네임스페이스명으로 하나의 가상 계층이 생성됩니다. 위 예에서 jiny라는 가상의 계층이 생성되고, 네임스페이스 가상 계층 안에 members 클래스가 선언한다는 것입니다.

동일한 네임스페이스 안에서 클래스 인스턴스를 생성하는 것은 기존 방법과 동일하게 사용할 수 있습니다.

```php
$obj = new members();
```

즉 네임스페이스를 넣지 않는 경우 PHP는 이를 현재의 네임스페이스에 의존한다고 간주하는 것입니다.

하지만 네임스페이스를 적용한 클래스에서 호출하기 위해서는 기존에 클래스명 앞에 네임스페이스명 도 같이 넣어야 합니다.

```php
$obj = new \jiny\members();
```

new 키워드와 클래스명 사이에 네임스페이스명을 넣어줍니다.  
만일 서브 네임스페이스를 가지고 있다고 하면 백슬래시(\)로 네임스페이스\클래스명으로 구분하면 됩니다.

또는 전역으로 클래스를 설정을 하고자 할 때는 다음과 같은 형태로 클래스명 앞에 \를 넣으면 됩니다.

```php
$obj = new \members();
```

즉 맨 앞에 \로 시작한다고 하면 루트 디렉터리처럼 전역을 선언하는 것과 같습니다.  

예전에 기존 네임스페이스가 도입되기 전에는 클래스명의 중복을 피하기 위해서 클래스명 앞에 접두사를 넣어서 쓰거나 밑줄(_)를 이용하여 구별하여 사용했습니다.


기본 방식 => 	jiny_shop_currency   
네임스페이스 => jiny/shop/currency 


네임스페이스 기능을 통하여 좀더 계층적이고 익숙한 디렉터리 구조로 소스를 계층화합니다. 마치 폴더를 관리하는 것과 같은 백슬래시(\)를 이용하여 구분할 수 있습니다.

예제 파일 namespace-03.php
```php
<?php
	namespace jiny\site;

	class members
	{
		public function setUsers($id)
		{
			echo "회원ID = $id";
		}
	}

	// 네임스페이스 이름을 같이 적용 
	$obj = new \jiny\site\members();
	$obj->setUsers(124);
?>
```

결과
```
회원ID = 123
```

예제 파일 namespace-04.php
```php
<?php
	namespace jiny\aaa;

	class members
	{
		public function setUsers($id)
		{
			echo "회원ID = $id";
		}
	}

	
	namespace jiny\bbb;

	class members
	{
		public function setUsers($id)
		{
			echo "회원ID = $id";
		}
	}


	// 네임스페이스 이름을 같이 적용 
	echo "네임스페이스 \jiny\aaa\<br>";
	$obj = new \jiny\aaa\members();
	$obj->setUsers(126);

	echo "<br>";

	// 네임스페이스 이름을 같이 적용
	echo "네임스페이스 \jiny\bbb\<br>";
	$obj2 = new \jiny\bbb\members();
	$obj2->setUsers(127);

?>
```

결과
```
네임스페이스 \jiny\aaa\
회원ID = 126
네임스페이스 \jiny\bbb\
회원ID = 127
```

위의 예를 보면 동일 members 클래스를 네임스페이스를 통해 두 번 선언되어 있습니다.  
또한 네임스페이스를 통해 클래스 인스턴스를 생성하여 호출합니다. 

<br>

### 15.6.3 클래스 이름 확인
---
PHP 5.5 이후 버전에서는 class 키워드를 통해 현재의 네임스페이스를 포함한 클래스 이름을 확인할 수 있습니다.

예제 파일 namespace-05.php
```
<?php
	namespace jinyPHP;
    
    class MyClass {
    }
    
    echo MyClass::class;
	
?>
```

결과
```
jinyPHP\MyClass
```

<br>

## 15.7 use 키워드
---
앞에서 학습한 네임스페이스를 이용했습니다. 만일 네임스페이스 명이 길다거나, 서브 네임스페이스명이 많을 때는 클래스 인스턴스 생성 시 길어진 이름으로 인하여 불편한 점이 있었습니다.    

<br>

### 15.7.1 use 개념
---
서브 네임스페이스로 인하여 길어진 이름은 매번 클래스의 인스턴스를 생성하는 데 많은 불편을 주었습니다. 또한 길어진 이름은 소스의 가독성을 떨어뜨리고, 오탈자를 많이 발생합니다. PHP 언어는 별칭 기능을 통해 길어진 네임스페이스명을 짧게 줄여서 사용할 수 있습니다. use 키워드는 길어진 네임스페이스를 별칭으로 치환하는 기능을 제공합니다.  

<br>

### 15.7.2 use 문법
---
use를 통해 네임스페이스 이름을 처리하는 방법으로 두 가지 형태를 제공합니다. 

첫째는 현재 적용되고 있는 네임스페이스의 경로를 변경합니다.

|문법|
```
use 네임스페이스경로;
```

use 명령은 클래스의 인스턴스 생성하기 전에 use 키워드를 통해 별칭을 선언 할 수 있습니다. 

use 네임스페이스경로; 를 적용하면 클래스 인스턴스 선언 시 기존 네임스페이스의 모든 경로를 다 넣지 않아도 클래스의 인스턴스를 간단하게 생성할 수 있습니다.

예제 파일 use-01.php
```php
<?php
	namespace jiny\aaa;

	class Members1
	{
		public function setUsers($id)
		{
			echo "aaa 회원ID = $id";
		}
	}


	namespace jiny2\bbb;

	class Members
	{
		public function setUsers($id)
		{
			echo "bbb 회원ID = $id";
		}
	}


	// 네임스페이스를 aaa로 변경
	echo "네임스페이스를 aaa 변경<br>";
	use jiny\aaa\Members1;

	// 네임스페이스 이름을 같이 적용 
	$obj = new Members1;
	$obj->setUsers(1);
?>
```

결과
```
네임스페이스를 aaa 변경
aaa 회원ID = 1
```

두 번째는 길어진 네임스페이스에 별명 명칭을 적어 사용하는 것입니다.

|문법|
```
use 네임스페이스경로 as 별칭;
```

as 별칭으로 짧은 이름을 새롭게 부여할 수 있습니다. 

 

as 키워드를 이용하면 개발자의 편의에 따라서 별칭을 사용자가 지정할 수 있다는 것이 매우 유용합니다.

예제 파일 use-02.php
```php
<?php
	namespace jiny\aaa;

	class members
	{
		public function setUsers($id)
		{
			echo "aaa 회원ID = $id";
		}
	}


	namespace jiny\bbb;

	class members
	{
		public function setUsers($id)
		{
			echo "bbb 회원ID = $id";
		}
	}

	use jiny\aaa as aaa;
	use jiny\bbb as bbb;

	// 네임스페이스 이름을 같이 적용 
	$obj = new aaa\members();
	$obj->setUsers(1);

	echo "<br>";

	// 네임스페이스 이름을 같이 적용 
	$obj = new bbb\members();
	$obj->setUsers(2);
?>
```

결과
```
aaa 회원ID = 1
bbb 회원ID = 2
```

위의 예제에서는 as 키워드를 통하여 jiny\aaa 를 aaa로 별칭을 변경합니다. 별칭으로 작성된 이름으로 클래스를 선언할 수 있습니다.

<br>

### 15.7.3 다중 use
---
여러 개의 네임스페이스를 한 번에 처리할 수 있습니다. 기본적으로 use 명령은 콤마(,)를 통해 다수의 네임스페이스를 하나의 use 명령을 처리할 수 있습니다. 

|문법|
```php
use 네임스페이스1,
 네임스페이스2,
 네임스페이스3;
```

하지만 콤마(,)를 이용한 다수의 처리는 코드의 가독성을 줄이고, 오류를 발행할 수 있는 상황을 만들 수 있습니다.

이를 방지하기 위해 use 명령 하나당 네임스페이스 한 개를 적어주는 스타일을 추천합니다. 

|문법|
```php
use 네임스페이스1;
use 네임스페이스2;
use 네임스페이스3;
```

<br>

### 15.7.3 use 그룹화
---
위와 같이 한 줄 단위로 use 별칭을 작성하는 것은 불편한 점이 있습니다. 네임스페이스의 클래스를 각각의 use 명령으로 재정의하는 것은 코드 작성에 있어 복잡한 부분이 있었습니다.

```php
<?php
// 이전 코드에서는 비슷한 use 명령을 여러 줄을 통해 작성했습니다.
	use some\namespace\ClassA;
	use some\namespace\ClassB;
	use some\namespace\ClassC as C;

	use function some\namespace\fn_a;
	use function some\namespace\fn_b;
	use function some\namespace\fn_c;

	use const some\namespace\ConstA;
	use const some\namespace\ConstB;
	use const some\namespace\ConstC;
?>
```

PHP 7.x로 업그레이드되면서 비슷한 유형끼리 그룹으로 설정할 수 있는 새로운 기능을 추가로 제공합니다.

|문법|
```
<?php
// PHP 7+ code
// PHP 7+ 버전에서는 같은 유형의 use 를 그룹화하여 처리를 할 수 있습니다.
<?php

	use some\namespace\{
		ClassA, 
		ClassB, 
		ClassC as C
	};
	
	use function some\namespace\{
		fn_a, 
		fn_b, 
		fn_c
	};
	
	use const some\namespace\{
		ConstA, 
		ConstB, 
		ConstC
	};
?>
```

같은 유형의 그룹은 위의 예처럼 중괄호를 이용하여 처리할 수 있습니다. 코드를 가독화하고 읽기 쉽게 만들어 사용할 수 있습니다.
