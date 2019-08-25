# Database
</br>

## Outline
- [Indexing](#indexing)
- [DAO, DTO](#dao-dto)
- [SQL문법] (#SQL문법)
- [데이터베이스 CRUD] (#데이터베이스-CRUD)
- [Sharding] (#Sharding)

</br>

## Indexing

##### Index란?
  - 데이터에 빠르게 접근하기 위하여 (검색, 정렬 등) 
  - <키값, 포인터> 쌍으로 구성된 데이터 구조를 통하여 원하는 레코드에 접근
    - (인덱스의 키 값이 정렬되어 있으면, 원하는 레코드의 포인터를 더 빠르게 찾을 수 있다.)
##### 기본키값 말고 다른 속성을 인덱스의 키값으로 두면 무엇이 좋은가?
  - 기본키에 대해서는 항상 DBMS가 내부적으로 정렬된 목록을 관리하기에 특정 행을 가져올 때 빠르게 처리된다. 
  - 하지만, 다른 열의 내용을 검색하거나 정렬시에는 하나하나 대조를 해보기 때문에 시간이 오래걸린다. (이를 인덱스로 정의해두면 검색속도가 향상된다.)
##### 단점은?
  - DML에 취약
    데이터 삽입, 변경 등이 일어날 때 매번 인덱스가 변경되기 때문에 성능이 떨어질 수 있다.
  - (인덱스를 사용하면 데이터를 가져오는 작업의 성능은 향상시킬 수 있지만)
##### 그럼 언제 사용하면 좋을까?
  - DML가 얼마나 사용되는가를 고려해야한다.
  - JOIN이나 WHERE에 자주 사용되는 열의 경우.
  - 데이터의 중복도가 낮은 경우 (타입이 별로 없는 경우 X)
##### 자료구조?
- B+-Tree 인덱스
  - B+-Tree는 B-Tree와 다르게 중간에는 데이터가 아닌 인덱스만 저장이 되는 자료구조이다. 
  - B-Tree는 inner node에는 인덱스(키)값만 저장이 되고 leaf node에 인덱스와 데이터를 함께 저장한다.
  - leaf node에만 데이터가 저장되기 때문에, 포인터를 연결하여 B-Tree보다 쉽게 순회할 수 있다. 
- 해시 인덱스
  - 칼럼 값으로 Hash 값을 계산하여, 인덱스의 키값으로 사용한다.
- B+-Tree vs 해시 인덱스
  - 데이터에 접근하는 속도는 해시가 O(1)이기 때문에 더 빠를 것 같지만, SELECT 질의에는 부등호 연산이 주로 포함된다. 특정 범위에 속하는 데이터를 찾는 경우가 많으므로, B+-Tree가 대부분에 경우에 적합하다.

</br>

## DAO, DTO

##### DAO, DTO 정의
  - DAO : Data Access Object의 약자로써, 데이터 베이스에 접속, 명령 전송을 담당하는 객체이다. 비즈니스 로직과 분리하기 위해 사용된다.
    ~~~Java
    //DAO
    public class DEPT_DAO {
    DEPT_DAO(){}
    
    //insert
    public int insert(DEPT_DTO dto){
        
        return -1;
    }
    
    //select
    public ArrayList<DEPT_DTO> select() {
        
        return null;
    }
    
    //update
    public int update(DEPT_DTO dto) {
        
        return -1;
    }
    
    //delete
    public int delete(int deptno) {
        
        return -1;
    }
    }
    ~~~
    
  - DTO : Data Transfer Object의 약자로써, 하나의 클래스를 하나의 클래스에 매칭 시키기 위해 사용. VO 개념.
    ~~~Java
    public class DEPT_DTO {
    private int deptno;
    private String dname;
    private String loc;
    
    public int getDeptno() {
        return deptno;
    }
    
    public void setDeptno(int deptno) {
        this.deptno = deptno;
    }
    
    public String getDname() {
        return dname;
    }
    
    public void setDname(String dname) {
        this.dname = dname;
    }
    
    public String getLoc() {
        return loc;
    }
    
    public void setLoc(String loc) {
        this.loc = loc;
    }
    }
    ~~~
## SQL문법
##### DDL(데이터 정의어)
- 테이블과 같은 데이터 구조를 정의. 
- CREATE, ALTER, DROP, RENAME, TRUNCATE
##### DML (데이터 조작어)
- 데이터를 조회하거나 검색하기 위한 명령어
- SELECT, INSERT, DELETE, UPDATE
##### DCL (데이터 제어어)
- 데이터베이스에 접근하고 객체들을 사용하도록 권한을 주고 회수하는 명령어
- GRANT, REVOKE
##### TCL (트랜잭션 제어어)
- 논리적인 작업의 단위를 묶어서 DML에 의해 조작된 결과를 작업단위(트랜잭션) 별로 제어
- COMMIT, ROLLBACK, SAVEPOINT
    
</br>

## 데이터베이스 CRUD
- CRUD는 대부분의 컴퓨터 소프트웨어가 가지는 기본적인 데이터 처리 기능인 Create, Read, Update, Delete를 묶어서 일컫는 말 사용자 인터페이스가 갖추어야 할 기능을 가리키는 용어로서도 사용함
        
</br>

## Sharding
- RDBMS에서 대량의 데이터를 처리하기 위해 데이터를 파티셔닝하는 기술
- 데이터베이스 자체를 분할해야 하므로 어플리케이션 레벨에서 구현
- 참고 : https://genesis8.tistory.com/211



