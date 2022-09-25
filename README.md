# ConcurrencyIssues_Stock
Study of solving concurrency issues
Race condition: 
The race condition occurs both in multithreaded applications and in the databases in which they work. And it is not limited to web applications only. For example, this is a common criterion for privilege escalation in operating systems. 

From <https://lab.wallarm.com/race-condition-in-web-applications/>
<br>
• Locks.
The operation blocks the access to the locked object in the DBMS until it is unlocked. Others stand and wait on the sidelines. It is necessary to work with locks correctly, not to lock anything extra.
<br>
• Isolations.
Serializable transactions ensure strictly sequential execution. This, however, can impact performance.
<br>
• Mutual exclusions.
We use a tool like etcd to create an entry with a key at each function call. If it is not possible to create an entry, then it already exists and the request is interrupted. At the end of request processing, the entry is deleted.
<br>
From <https://lab.wallarm.com/race-condition-in-web-applications/> 

<br>
@Transactional annotation
<br>
The annotation supports further configuration as well:
	<br>
  • the Propagation Type of the transaction
  <br>
	• the Isolation Level of the transaction
  <br>
	• a Timeout for the operation wrapped by the transaction
  <br>
	• a readOnly flag – a hint for the persistence provider that the transaction should be read only
  <br>
	• the Rollback rules for the transaction
Note that by default, rollback happens for runtime, unchecked exceptions only. The checked exception does not trigger a rollback of the transaction. We can, of course, configure this behavior with the rollbackFor and noRollbackFor annotation parameters.
  <br>
From <https://www.baeldung.com/transaction-configuration-with-jpa-and-spring> 

Solution

1. Use Synchronized
<br>
@Tranasactional 어노테이션은 스프링 클래스릉 Wrapping 하는 클래스를 매번 생성함
-> @Transactional 삭제
<br>
문제점: 하나의 프로세스 안에서만 보장. 서버가 2대 이상에서는 사용불가. (동시에 접근). 거의 사용 불가

<br>
2. Using Database Locks
  <br>
	• Pessimistic Lock

![image](https://user-images.githubusercontent.com/31177070/192123467-11503d54-3109-40cf-9963-54efff21a1bb.png)
