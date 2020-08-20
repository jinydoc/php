---
layout: php
---

# 콘솔 실행
---
PHP는 클라이언트 웹 브라우저를 통해 실행 및 결과를 확인하는 것 이외에 서버, 터미널 콘솔 창에서 실행 결과를 확인할 수 있습니다.

실행 방법)
```
# php 실행 파일.php
```

위와 같이 콘솔 창에서 실행하면 바로 결과를 콘솔 창에서 확인할 수 있습니다.  

콘솔 창과 웹 브라우저로 결과를 확인하는 것은 약간의 차이점이 있을 수 있습니다. 콘솔 창에서 출력의 다음 줄은 ‘\n’으로 표기하지만 웹 브라우저는 다음 줄을 `<br>` 태그로 처리합니다.  

대부분의 소스들은 웹 브라우저에서 확인하는 것을 기준으로 다음 줄 표시를 `<br>` 태그를 사용합니다. `<br>` 태그는 다음 줄을 의미한다고 생각하면 됩니다.  

PHP 콘솔을 이용하면 몇 가지 장점이 있습니다. 
* PHP 스크립트 실행 파일을 백그라운드로 실행할 수도 있습니다. 
* 스케줄링 기능을 통해 주기적으로 PHP를 실행할 수도 있습니다. 

<br><br>