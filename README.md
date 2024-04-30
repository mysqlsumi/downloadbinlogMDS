## MDS_binarylog
How to download a binary log from MDS on Oracle Cloud

MDS 에서 바이너리 로그 OCI 배스천 서버에 다운로드 하는 법

### 1. OCI 베스천 서버에서 MySQL Shell로 접속 후 binary log 정보 확인 및 INSERT 쿼리 수행
- INSERT 쿼리 수행 


```
insert into t1 values (5), (6);
select * from t1;
```
![alt text](/img/image-2.png)

- binary log 정보 확인 


```
show binary logs;
```
![chek binary log file](/img/image-3.png)


### 2. OCI 베스천 서버에서 mysqlbinlog 명령어를 이용해서  binary log 다운받기


```
mysqlbinlog --read-from-remote-server --host=10.0.1.xxx --user admin -pWelcome1! --raw  binary-log.000xxx
```
![download binlog](/img/image-4.png)

### 3. 다운받은 binary log 읽기 가능한 형태로 변환
- mysqlbinlog 명령어를 이용해서 binary log 변환


```
mysqlbinlog -v --base64-output=DECODE-ROWS binary-log.000xxx> xxx.sql
```
![change to a readable format](/img/image-5.png)

- 변환된 log 확인


```
<!-- cat xxx.sql  또는 -->
vi xxx.sql 
```
![01log](/img/image-6.png)
![02log](/img/image-7.png)

### 4. 참고자료
[오라클 블로그 PITR part1](https://blogs.oracle.com/mysql/post/point-in-time-recovery-in-oci-mds-with-object-storage-part-1)


[오라클 블로그 PITR part2](https://blogs.oracle.com/mysql/post/point-in-time-recovery-in-oci-mds-with-object-storage-part-2)


[MySQL Reference 메뉴얼](https://dev.mysql.com/doc/refman/8.3/en/mysqlbinlog.html)