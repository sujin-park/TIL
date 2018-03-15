## Spring JPA

Spring data jpa는 스프링 프레임워크에서 JPA를 편리하게 사용할 수 있도록 제공해주어 반복되는 CRUD를 간단하게 사용할 수 있다.

Spring data jpa는 CRUD를 처리하기 위한 공통 인터페이스가 존재한다. 개발 시 인터페이스만 작성하면 실행 시점에서 JPA 구현 객체를 동적으로 생성해서 주입해준다.


### JPA Query Method


* method 이름만으로 쿼리를 생성하는 기능
* NamedQuery, @Query annotation 등

#### @Query Annotation

이 중 repository method에 쿼리를 직접 정의하려면 Spring에 있는 @Query 어노테이션을 사용하면 된다. method에 정적 쿼리를 직접 작성하므로 이름 없는 Named 쿼리라 할 수 있다. 또한 JPA Named 쿼리처럼 **애플리케이션 실행 시점에 문법 오류**를 발견 할 수 있는 장점이 있다.

~~~
@Repository 
interface 
MemberRepository : JpaRepository<Member, Int>{

    @Query("select u from member u where u.userNo = :userNo")
    fun findByUserNo(@Param("userNo") userNo: Int) : List<Member>
~~~

쿼리가 잘못 작성되었을 경우에 spring 로딩에 실패하면서 프로그램이 실행되지 않는다. 그러나 편집기 상에서의 유효성 분석은 해주지 않는다. 그래서 쿼리 어노테이션은 type safe 하지 않은 것으로 보고 잘 사용하지는 않는 편이다.


### 참고
[머루의 개발블로그](http://wonwoo.ml/index.php/post/1004)
