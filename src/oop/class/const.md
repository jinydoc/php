---
layout: php
title: "PHP"
keyword: "jinyphp, php"
breadcrumb:
- "oop"
- "class"
- "const"
---

# 클래스 상수
---
객체 클래스만의 상수를 선언할 수 있습니다. 객체 클래스 내에 상수를 선언하는 것은 프로그램 소스 전체에서 사용이 가능한 공용 상수가 아닙니다. 이 상수는 객체 클래스 안에서만 사용할 수 있는 상수 코드로 독립적인 효과가 있습니다.  
  
PHP 언어는 두 가지의 방식으로 상수를 설정할 수 있습니다. 하지만 이 두 가지 중에서 객체 클래스 안에서 상수 설정 가능한 방법은 const 명령만 사용 가능합니다. 즉, define() 함수는 사용하지 않습니다.  

클래스 상수
```php
class language {
	const ENGLISH = "en";
	const KOREAN = "ko";
}
```

객체 클래스 본문 중괄호 `{ }` 안에 `const`를 사용하여 상수를 선언하면 됩니다.  
상수를 선언하는 문법과 방식은 기존 PHP 상수 설정과 같지만 클래스 본문 안에 작성한다는 것이 차이점입니다.  

클래스 안에 상수를 쓸 때는 PSR-2 코딩 스타일 방식으로 들여쓰기를 하여 작성합니다.  
PSR-1 코딩 스타일에 따라서 상수는 대문자로 작성합니다. 상수명이 길어질 때는 밑줄(`_`)을 통해 구분하여 상수명을 작성할 수도 있습니다.

클래스 상수를 사용할 때는 객체변수 뒤에 이중콜론(`::`) 기호로 사용할 수 있습니다.  

|문법|
```php
$객체변수::상수명
```

클래스 내부적으로 사용을 할 때는 다음과 같은 형태로 사용 가능합니다.

|문법|
```php
self::상수명
```

예제 파일 class-01.php
```php
<?php
	class language {
		const ENGLISH = "en";
		const KOREAN = "ko";

		public function getEnglish()
		{
			return self::ENGLISH;
		}
	}

	$obj = new language();

	echo "클래스 상수 출력<br>";
	echo "KOREAN = " . $obj::KOREAN . "<br>";

	echo "메서드를 이용한 상수 출력<br>";
	echo "ENGLISH = " . $obj->getEnglish() . "<br>";
?>
```

결과
```
클래스 상수 출력
KOREAN = ko
메서드를 이용한 상수 출력
ENGLISH = en
```

위의 예제는 클래스 내부에 독립 상수를 설정하고, 이를 접근 출력하는 예입니다.  
language 클래스는 두 개의 상수를 가지고 있습니다. 첫 번째 출력에서는 직접 객체에 접근하여 사용했습니다.  
두 번째 출력에서는 매서드를 이용하여 내부 접근을 한 후에 상수값을 출력합니다.
