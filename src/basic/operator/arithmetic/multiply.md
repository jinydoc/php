---
layout: php
breadcrumb:
- "basic"
- "operator"
- "arithmetic"
---

# 곱하기
---
컴퓨터 언어의 곱셈 기호는 `*`를 사용합니다. 우리가 일반적으로 알고 있는 `×`를 사용하지 않습니다.  

<br>

## `*` 연산기호
---
`곱셈`은 좌우의 값을 곱한 값을 출력합니다.  
또한 곱한 결과값을 왼쪽에 대입 연산자를 통해 변수에 저장할 수 있습니다.  

|문법|
```php
$sum = $x * $y
$a = 5 * 3; // $a = 5 + 5 + 5;
```

<br>

## 연습문제1
---
곱셈은 왼쪽에 있는 값을 오른쪽의 값의 횟수만큼 `더한 값`과 같습니다.  
즉 세 번의 덧셈을 처리하는 것과 같습니다.  

예제 파일 mul-01.php
```php
<?php

	$x = 5;
	$y = 3;

	$sum = 0;
	for ($i=0;$i<$y;$i++) {
		$sum = $sum + $x;
	}

	echo "곱셈은 덧셈의 반복 = ". $sum ;
?>
```

결과
```
곱셈은 덧셈의 반복 = 15
```
