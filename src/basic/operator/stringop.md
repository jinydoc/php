---
layout: php
breadcrumb:
- "basic"
- "operator"
- "string"
---

# 문자열 연산
---
지금까지 많은 예제 중에서 화면 출력 시 점(`.`) 기호를 많이 봤을 것입니다.  
PHP에서는 두 개의 문자열을 결합할 수 있는 연산자를 지원합니다.  
다른 언어에서는 좀 더 직관적인 덧셈(`+`) 기호를 쓰기도 하지만 PHP에서는 점(`.`) 연산자를 사용합니다.  

|문법|
```php
$text = $txt1 . $txt2 
```

점은 두 개의 문자열을 연결하는 기능을 합니다.  

예제 파일 string-06.php
```php
<?php
	$a = "hello";
	$b = "world!";

	// 문자열을 바로 결합니다.
	echo "hello " . "world!";
	echo "<br>";

	// 변수와 문자열을 결합합니다.
	echo $a . " world!";
	echo "<br>";
	
	// 변수와 변수를 결합합니다.
	echo $a . $b;
	echo "<br>";
?>
```

결과
```
hello world!
hello world!
helloworld!
```

점 연산자는 문자열 데이터를 바로 연결할 수도 있으며, 변수와 같이 혼용하여 연결할 수도 있습니다.  

또한 이전에 복합 연산 방식과 비슷하게 `.=` 방식으로 기존의 문자열에 새로운 문자열을 결합할 수도 있습니다.  
새로운 문자열은 기존 문자열 맨 뒤에 추가로 연결됩니다.  

```php
$text .=  $txt2 
```

예제 파일 string-07.php
```php
<?php	
	$a = 'a';

	for($i=0;$i<10;$i++)
	{
		$string .= $a++;
		echo $string . "<br>";
	}
?>
```

결과
```
a
ab
abc
abcd
abcde
abcdef
abcdefg
abcdefgh
abcdefghi
abcdefghij
```

위의 예를 보면 $string 변수에 알파벳을 하나씩 늘려가면서 추가하는 예제입니다. 
`.=` 연산자를 통해 알파벳 한 글자 한 글자를 결합하면서 화면에 출력합니다.  

<br><br>