---
layout: php
title: "PHP"
keyword: "jinyphp, php"
---

14. 메일
====================

PHP의 내장 메일함수는 PHP를 이용하여 간단하게 메일을 전송할 수 있습니다. 메일을 발송을 하기 위해서는 메일 발송 SMTP 서버가 필요로 합니다.

14.1 SMTP
====================

SMTP는 (Simple Mail Transfer Protocol) 약자로 메일발송 역할을 하는 서버입니다. 보통 메일을 발송할려면 메일 전송 서버와 수신서버가 필요로 합니다. 

PHP 내부함수를 통하여 메일을 전송하기 위해서는 SMTP 발송 서버가 설치되어 있어야 합니다.

리눅스에서 대표적으로 사용하는 SMTP 서버로는 sendmail 데몬 서비스가 있습니다.

sendmail 데몬 서비스에 대한 설치 및 설정 정보는 리눅스 관련 서적을 참조해 주시길 바랍니다.


14.2 메일작성
====================

PHP 에서는 내장함수 mail()을 통하여 메일을 작성할 수 있습니다. 작성된 메일은 지정된 메일서버로 전달되고. 메일 서버를 통하여 상대방에게 전달이 됩니다.

|내부함수|
bool mail ( string $to , string $subject , string $message [, string $additional_headers [, string $additional_parameters ]] )

mail()함수는 메일 전송에 필요한 몇개의 인자를 필요로 합니다.

to : 메일 수신 이메일
subject : 메일의 제목
message : 메일의 본문
additional_headers : 메일해더 부분

예제) mail.php
<?php
	// 메일 메시지 본문
	$message = "내용1\r\n 내용2\r\n 내용3";

	// 메일 내용이 길어진 경우 wordwarp() 함수를 통하여 넘길 수 있습니다.
	$message = wordwrap($message, 70, "\r\n");

	$to = "infohojin@naver.com";
	$subject = "메일 테스트";

	$header = 'From: infohojin@naver.com' . "\r\n" .
    'Reply-To: infohojin@naver.com' . "\r\n" .
    'X-Mailer: PHP/' . phpversion();
	
	// Send
	mail($to, $subject, $message, $headers);
?>


<br><br>