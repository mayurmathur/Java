Why do we need concurent collections when we already have collections?
-> Since if you do any structural modifications(like add, remove an element) while iterating through it, you will get concurrentModificationException
-> So Java introduced following as part of Java 1.5
   -> ConcurrentHashMap
   -> CopyOnWriteArrayList
   -> CopyOnWriteArraySet

Why is peformance improved in ConcurrentHashMap whereas decreased in HashTables/SynchronizedMap ?
-> Lock use to be taken on whole of HashTable, it will not allow people to read as well
-> In ConcurrentHashMap, we acquire lock on the segment only(which is calculated by concurreny level). There is a concept of Concurreny Level also here-> this allows how many threads can be allowed 
to access the ConcurrentHashMap
  -> Multiple threads can read on ConcurrentHashMap in other segments as well as same segment.
  -> Lock is on segment level.

Why nulls are not allowed in ConcurrentHashMap?
-> Because you can modify while reading, so if something is deleted while writing then we will get null. If we allow null we dont know if value is null or its missing.

Non Blocking Operations in ConcurrentHashMap
  -> Read read 

Blocking Operations in ConcurrentHashMap
  -> Write/*

Can ConcurrentModificationException happen in Single Threaded Environment?
-> Yes when we are iterating a list and removing something while iterating


How do we figure out modification Exception comes up ?
 -> In non concurrentDataStructures you have a concept of modCOunt
  -> modCount is transient variable

-> CopyOnWriteArrayList
   -> For every write a new cloned copy is created
   -> JVM snychronizes it at the end.

    **HashMap**	                                           **ConcurrentHashMap**
Fail-Fast Iterator	                             Fail-Safe (Weakly Consistent) Iterator
Very performant in single-threaded scenarios	   Slightly lower performance due to thread safety overhead
Not thread-safe	                                 Thread-safe
Allows nulls	                                   Does not allow nulls


  **ArrayList**	                                           **CopyOnWriteArrayList**
Fail-Fast Iterator	                              Fail-Safe Iterator (Snapshot-based)
Not thread-safe	                                  Thread-safe
Suitable for frequent modifications	              Suitable for read-heavy workloads
Iterator supports remove()	                      Iterator does not support remove(), set(), or add()


ShortCuts
1. Single machine → Locks / CAS
2. Database system → Transactions / Optimistic locking
3. Distributed system → Saga / 2PC
4. Event-driven system → Event sourcing



Problems
-> Check then act

if(a.length()>10){
a = a-1;
}
Solution: -> Lock/Synchronized

-> read-modify-write
  count++; -> its actually three steps -> read count, int k = count+1, count = k

Solution -> AtomicInteger

Update multiple rows then use locks instead of AtomicInteger


-> Asynchronus processing
BlockingQueue<> bq = new ArrayBlockingKey<>(100)

-> Limiting Concurrent Accesses to same resource
  Semaphores

-> For Objects of class
BlockingQueue<Connection> pool = ArrayBlockingQueue<>();

poll.put(new Connection());

Connection c = poll.take();
//doSomething
poll.put(c);
