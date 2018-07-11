## @Transactional


@Service 에서 class 또는 method 에  @Transactional(readOnly = true) 을 붙여 트랜잭션을 읽기 전용으로 설정할 수 있다.

```kotlin

@Service
class MemberService
{
    @Autowired
    private lateinit var memberRepository : MemberRepository

    @Transactional(readOnly = true)
    fun memberList() = memberRepository.findAll()

    fun memberCreate(member : Member) = memberRepository.save(member)

    @Transactional(readOnly = true)
    fun memberGet(id : Int) = memberRepository.findById(id)

}
```

### 사용 목적
- 성능을 최적화하기 위해 사용
- 특정 트랜잭션 작업 안에서 write를 의도적으로 방지하기 위해 사용
 

### 읽기 전용 속성이 Transaction Manager에게 전달되면 Transaction Manager가 적절한  그에 따라 Transaction Manager가 적절한 작업을 수행한다.  일반적으로 읽기 전용 트랜잭션이 시작된 이후 INSERT, UPDATE, DELETE 같은 쓰기 작업이 진행되면 예외가 발생한다. 


### 참고

- [Rednics Blog](http://springsource.tistory.com/136) 