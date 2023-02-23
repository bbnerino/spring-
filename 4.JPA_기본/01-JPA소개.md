> 저번주에 JPA 활용을 통해 스프링을 이용해 프로젝트를 생성해 보았다.
> 후기 : 정말 .. 너무 어렵다 .. 하나도 모르겠다.
> 이 후기가 너무나도 당연한 결과다. 왜냐면 진짜 모르기 때문, 지금부터 그 코드들을 왜썼는지 깨닿게 되는 시간을 가지게 될 것이다.

# [JPA 기본] 1. JPA

JPA는 프로젝트에서 DB에 접근하기 위해 사용한다.
객체를 자바 컬렉션에 저장하듯이 DB에 저장할 수 있게 해준다.

- SQL 중심적인 개발에서 객체 중심으로 개발이 가능하다
- 생산성과 유지보수 능력이 올라간다.

백문이불여일타 : 코드로 직접 만들어보며 깨닿자

# 프로젝트 생성

DB : H2
MAVEN

### pom.xml

pom.xml을 통해 라이브러리를 추가해준다.

```xml
<?xml version="1.0" encoding="UTF-8"?>
<project
  xmlns="http://maven.apache.org/POM/4.0.0"
  xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
  xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd"
>
  <modelVersion>4.0.0</modelVersion>
  <groupId>jpa-basic</groupId>
  <artifactId>ex1-hello-jpa</artifactId>
  <version>1.0.0</version>
  <dependencies>
    <!-- JPA 하이버네이트 -->
    <dependency>
      <groupId>org.hibernate</groupId>
      <artifactId>hibernate-entitymanager</artifactId>
      <version>5.3.10.Final</version>
    </dependency>
    <!-- H2 데이터베이스 -->
    <dependency>
      <groupId>com.h2database</groupId>
      <artifactId>h2</artifactId>
      <version>1.4.199</version>
    </dependency>
  </dependencies>
</project>
```

하이버네이트와 h2 를 설치해준다.
### JPA 설정 

위치를 정확하게 `/META-INF/persistence.xml`에 만들어야한다.

```xml
<?xml version="1.0" encoding="UTF-8"?>
<persistence
  version="2.2"
  xmlns="http://xmlns.jcp.org/xml/ns/persistence"
  xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
  xsi:schemaLocation="http://xmlns.jcp.org/xml/ns/persistence http://xmlns.jcp.org/xml/ns/persistence/persistence_2_2.xsd"
>
  <persistence-unit name="hello">
    <properties>
      <!-- 필수 속성 -->
      <property name="javax.persistence.jdbc.driver" value="org.h2.Driver" />
      <property name="javax.persistence.jdbc.user" value="sa" />
      <property name="javax.persistence.jdbc.password" value="" />
      <property
        name="javax.persistence.jdbc.url"
        value="jdbc:h2:tcp://localhost/~/test"
      />
      <property
        name="hibernate.dialect"
        value="org.hibernate.dialect.H2Dialect"
      />
      <!-- 옵션 sql 코드들을 포맷에 따라 볼 수 있게 한다. -->
      <property name="hibernate.show_sql" value="true" /> 
      <property name="hibernate.format_sql" value="true" />
      <property name="hibernate.use_sql_comments" value="true" />
      <!--<property name="hibernate.hbm2ddl.auto" value="create" />-->
    </properties>
  </persistence-unit>
</persistence>
```

### 데이터 베이스 방언 
사용한는 DB에 따라 다른 설정값을 줘야한다.
`<property name="hibernate.dialect"value="org.hibernate.dialect.H2Dialect"/>` 
여기서는 H2 Dialect를 사용했다 MySQL, Oracle.. 에 따라 설정해주면 된다. 


# JPA 구동 방식

1. `persistence.xml` 을 토대로 Persistence를 만들어준다.

2. 그 Persistence에서 `EntityManagerFactory` (emf) 을 만들어준다.

3. 사용할 때마다 emf 에서 `EntityManger`를 만들어서 사용한다.


### 객체 만들기 
테스트를 위해 객체를 하나 만들어준다. 
```java
@Entity
public class Member {
  @Id
  private Long id;
  private String name;
}
```
- @Entity : JPA 가 관리할 객체를 등록한다.
- @Id : 데이터베이스 PK와 매핑한다.

그리고 DB에 직접 Table에 추가해준다.
```sql
create table Member{
  id bigint not null,
  name varchar(255),
  primary key (id)
}
```
--- 
# JPQL
검색 쿼리를 사용할때 사용한다.
테이블이 아닌 엔티티 객체를 대상으로 검색해야한다.
JPA는 SQL을 추상화한 JPQL이라는 객체 지향 쿼리 언어를 제공한다. 
JPQL은 엔티티 객체를 대상으로 쿼리 하고, SQL은 DB 테이블을 대상으로 쿼리한다.




# 코드

```java
public class JpaMain {
    public static void main(String[] args) {
        EntityManagerFactory emf = Persistence.createEntityManagerFactory("hello");
        EntityManager em = emf.createEntityManager();

        EntityTransaction tx = em.getTransaction();
        tx.begin();

        try{
            // 비영속 상태
            Member member = new Member(1L,"helloA");

            // 영속 상태
            // => 쿼리가 나가지 않는다.
            /** 저장*/
            em.persist(member);

            // 영속성 컨텐스트에서 지운다.
            em.detach(member);
            /** 객체를 삭제한다*/
//            em.remove(member1);
            /**조회*/
            Member member1 = em.find(Member.class, 1L); // 조회
            member1.setName("HelloB"); // 수정 => 딱히 아무거도 안해도 된다.
            tx.commit(); // 쿼리가 나가는 시점

        } catch (Exception e){
            tx.rollback();
        } finally {
            em.close();
        }

        emf.close();
    }
}
```
- Persistence를 통해 EntityManagerFactory 를 만든다.
- emf 를 통해 EmtityManager를 생성한다.
- EntityTransaction 을 begin() 시작해준다.

try 에서 원하는 코드를 작성하고, 마지막에 commit()을 통해 적용시켜준다 

자세한 내용은 다음장에서 소개한다. 