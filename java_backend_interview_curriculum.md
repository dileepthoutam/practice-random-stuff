# Java Backend Interview Preparation

## Core Java · Concurrency · Spring Boot · Microservices · Design Practices

**Purpose:** A topic-first curriculum for experienced Java/backend
engineering interviews. This document is intentionally not divided by
weeks or dates. Work through topics in order, prioritising the must-have
areas and practising with code.

**Target outcome:** Be able to explain concepts clearly, demonstrate
them in code, justify design choices, identify limitations, and handle
follow-up questions. Knowing a definition is not enough.

------------------------------------------------------------------------

## How to use this curriculum

For each topic, prepare these layers:

1.  **Explain it simply:** Give a concise definition without relying on
    jargon.
2.  **Explain how it works:** Describe the mechanism or internals at the
    level expected of an experienced engineer.
3.  **Demonstrate it:** Write a small example, trace execution, or
    reproduce a failure.
4.  **Justify choices:** Explain when you would use it, alternatives,
    and trade-offs.
5.  **Handle follow-ups:** Explore edge cases, failure modes,
    concurrency, performance, testing, and production implications.
6.  **Connect it to experience:** Where possible, relate it to a real
    service, incident, code review, or project.

For each major concept, try to answer: - What problem does this solve? -
How does it work? - Why is it designed this way? - When would I choose
it over an alternative? - What can go wrong? - How would I test, debug,
or observe it in production? - What changes under load, failure, or
concurrent access?

Use the checklist to track confidence: - \[ \] Can explain without
notes - \[ \] Can implement or demonstrate - \[ \] Can justify
trade-offs - \[ \] Can answer at least three follow-up questions - \[ \]
Can identify common mistakes and failure modes

------------------------------------------------------------------------

# 1. Core Java

## 1.1 Java execution and language fundamentals --- Must-have

-   JDK vs JRE vs JVM; source code, bytecode, class loading,
    interpretation and JIT compilation.
-   Compilation errors vs runtime exceptions vs linkage errors.
-   Primitive types vs reference types; default values and numeric
    conversions.
-   Java is pass-by-value: understand primitive values and copied object
    references.
-   `static`, instance members, initialization order, constructors,
    `this` and `super`.
-   Access modifiers, package visibility, `final`
    variables/methods/classes.
-   `==` vs logical equality; reference identity vs value equality.
-   Autoboxing/unboxing, wrapper types, `null`, and
    `NullPointerException`.
-   Integer caching and why boxed values should not generally be
    compared with `==`.
-   Varargs, enums, nested classes, records and annotations at a
    practical level.

**Practise:** Trace initialization order; demonstrate pass-by-value with
object references; compare identity and equality; explain a class from
source code through JVM execution.

**Likely follow-ups:** Does Java pass objects by reference? What does
`final` guarantee? When does class initialization happen? What work does
the JIT do?

## 1.2 OOP and object modelling --- Must-have

-   Encapsulation, abstraction, inheritance and polymorphism.
-   Overloading vs overriding; compile-time vs runtime method selection.
-   Interfaces vs abstract classes; default and static interface
    methods.
-   Composition vs inheritance; favouring composition where it reduces
    coupling.
-   Upcasting, downcasting, `instanceof`, covariant return types.
-   Constructors, constructor chaining, dynamic dispatch and pitfalls in
    calling overridable methods from constructors.
-   Cohesion, coupling, information hiding and programming to
    interfaces.
-   Immutable objects, defensive copying and value objects.
-   Records and sealed classes: use cases and limitations.

**Practise:** Model payments using interfaces and composition; refactor
a deep inheritance hierarchy; implement an immutable value object.

**Likely follow-ups:** When is inheritance appropriate? Can an interface
have implementation? How do you make a class immutable if it contains a
mutable collection? What makes an abstraction good?

## 1.3 `equals()`, `hashCode()` and object contracts --- Must-have

-   The `equals()` contract: reflexive, symmetric, transitive,
    consistent and false for `null`.
-   The `hashCode()` contract and why equal objects must have equal hash
    codes.
-   Why unequal objects may share a hash code.
-   Correctly implementing equality for value objects and inheritance
    hierarchies.
-   Mutable fields in equality and hashing; consequences for map/set
    keys.
-   `toString()`, `getClass()` and the purpose and pitfalls of
    `clone()`.
-   Records and generated equality semantics.

**Practise:** Implement equality for a `Payment` or `Money` class;
reproduce a failed `HashMap` lookup after mutating a key.

**Likely follow-ups:** What if `equals()` is overridden but `hashCode()`
is not? Does `HashMap` use only the hash code? How can inheritance
violate symmetry?

## 1.4 Strings, arrays, dates and core APIs --- Must-have

-   `String` immutability, string pool, literals and `intern()`
    conceptually.
-   `String` vs `StringBuilder` vs `StringBuffer`.
-   Concatenation costs; avoiding repeated string concatenation in
    loops.
-   Array creation, copying, equality, sorting and utility methods.
-   `Objects`, `Arrays`, `Collections` and `Comparator` utilities.
-   `BigDecimal`: scale, rounding modes, comparison and financial
    calculations.
-   `java.time`: `Instant`, `LocalDate`, `LocalDateTime`,
    `ZonedDateTime`, `Duration`, `Period`, `ZoneId`.
-   UTC, time zones, daylight-saving transitions and why timestamps
    should not be confused with local date-times.
-   `Optional`: intended use, `map`, `flatMap`, `orElse`, `orElseGet`,
    `orElseThrow`; avoid using it indiscriminately in fields and
    parameters.

**Practise:** Compare `BigDecimal` values safely; parse and format
dates; convert between instants and time zones; process strings
efficiently.

**Likely follow-ups:** Why is `String` immutable? Why can
`new BigDecimal(0.1)` surprise you? What is the difference between
`orElse()` and `orElseGet()`? How should a service store timestamps?

## 1.5 Collections framework --- Must-have

-   `Iterable`, `Collection`, `List`, `Set`, `Queue`, `Deque` and `Map`.
-   `ArrayList` vs `LinkedList`; `ArrayDeque` vs `Stack`.
-   `HashMap`, `LinkedHashMap`, `TreeMap`; `HashSet`, `LinkedHashSet`,
    `TreeSet`.
-   `PriorityQueue` and heap behaviour.
-   `Comparable` vs `Comparator`; stable ordering and custom sorting.
-   Iterator contracts, fail-fast behaviour and
    `ConcurrentModificationException`.
-   Immutable collections vs unmodifiable views.
-   Choosing collections based on access patterns, ordering, uniqueness,
    concurrency and complexity.
-   Big-O costs and the assumptions behind average-case complexity.

### HashMap and HashSet internals --- Must-have

-   Hashing, bucket selection, collisions, equality checks and lookup
    flow.
-   Capacity, load factor, resizing and rehashing.
-   Collision handling and tree bins in modern OpenJDK implementations.
-   How poor or mutable keys can damage correctness or performance.
-   Why `HashSet` is backed by a map.
-   Why `HashMap` is not thread-safe.
-   `null` handling and implementation-specific details that are useful
    in interviews.

**Practise:** Implement a frequency counter; group transactions by
customer; deduplicate value objects; choose a collection for a given
access pattern.

**Likely follow-ups:** How does `HashMap` find a key? What happens
during resize? Why do equal keys need equal hash codes? When is a
`TreeMap` preferable? What does fail-fast mean---and does it guarantee
thread safety?

## 1.6 Generics --- Must-have

-   Generic classes, interfaces and methods.
-   Type parameters and bounded type parameters.
-   Wildcards: `?`, `? extends T`, `? super T`; PECS.
-   Invariance: why `List<Integer>` is not a `List<Number>`.
-   Type erasure and its consequences.
-   Raw types, unchecked casts, heap pollution and generic arrays.
-   Generic methods vs overloads; type inference.

**Practise:** Write a generic repository/helper; create a method that
copies from a producer to a consumer; explain why a given generic
assignment does not compile.

**Likely follow-ups:** Why are generics invariant? What is type erasure?
When do you use `extends` vs `super`? Why are generic arrays restricted?

## 1.7 Lambdas, functional interfaces and streams --- Must-have

-   Functional interfaces and `@FunctionalInterface`.
-   Lambdas, method references and effectively-final captured variables.
-   `Predicate`, `Function`, `Consumer`, `Supplier`, `UnaryOperator`,
    `BinaryOperator`.
-   Stream lifecycle; intermediate vs terminal operations; lazy
    evaluation.
-   `map`, `flatMap`, `filter`, `distinct`, `sorted`, `reduce`,
    `collect`.
-   Collectors: `groupingBy`, `partitioningBy`, `mapping`, `toMap`,
    downstream collectors.
-   Encounter order, stateful operations, short-circuiting and stream
    reuse.
-   Side effects and why they make pipelines harder to reason about.
-   Parallel streams, common ForkJoinPool, splitting/combining costs and
    when parallelism is counterproductive.
-   `Optional` with streams and nested transformations.

**Practise:** Group payments by currency; find the latest transaction
per customer; calculate aggregates; convert nested collections with
`flatMap`; handle duplicate keys in `toMap`.

**Likely follow-ups:** `map()` vs `flatMap()`? Why are streams lazy?
When should parallel streams be avoided? What happens if a collector
receives duplicate keys? Why should stream lambdas avoid shared mutable
state?

## 1.8 Exceptions and resource management --- Must-have

-   `Throwable`, `Error`, `Exception` and `RuntimeException`.
-   Checked vs unchecked exceptions and the trade-offs of each.
-   `try`, `catch`, `finally`, try-with-resources and `AutoCloseable`.
-   Exception propagation, wrapping, causes and stack traces.
-   Custom exception design; preserving useful context.
-   Multi-catch, rethrowing and exception translation at application
    boundaries.
-   Avoiding swallowed exceptions and overly broad catches.
-   Recoverable vs unrecoverable errors; retry only when appropriate.
-   Resource cleanup and suppressed exceptions.
-   API error contracts vs internal diagnostic details.

**Practise:** Implement a service exception hierarchy; wrap a
lower-level exception without losing its cause; handle a resource that
can fail during both work and close.

**Likely follow-ups:** When should an exception be checked? Is catching
`Exception` always wrong? What happens if `finally` throws? When should
a failed operation be retried?

## 1.9 SOLID and good Java design --- Must-have

-   Single Responsibility, Open/Closed, Liskov Substitution, Interface
    Segregation and Dependency Inversion.
-   Cohesion, coupling, encapsulation and separation of concerns.
-   Composition over inheritance.
-   Dependency injection and programming to interfaces.
-   Tell-don't-ask and keeping business rules near the relevant domain
    behaviour.
-   Avoiding god classes, primitive obsession, unnecessary abstractions
    and speculative generality.
-   Refactoring toward testable code without overengineering.

**Practise:** Refactor a large payment service; separate validation,
business rules and persistence; explain which SOLID principle is
improved and what trade-off the refactor introduces.

**Likely follow-ups:** Can applying SOLID make code worse? What does
Liskov Substitution mean in practical terms? When is an interface
unnecessary? How do you balance extensibility with simplicity?

------------------------------------------------------------------------

# 2. Concurrency and JVM

## 2.1 Concurrency fundamentals --- Must-have

-   Process vs thread; concurrency vs parallelism.
-   CPU-bound vs I/O-bound tasks.
-   Thread lifecycle and states.
-   `Thread`, `Runnable`, `Callable`; `start()` vs `run()`.
-   `sleep()`, `join()`, interruption, daemon threads.
-   Shared mutable state, race conditions, atomicity, visibility and
    ordering.
-   Thread confinement and immutable data as ways to reduce
    coordination.
-   Why `count++` is not atomic.

**Practise:** Reproduce a race condition with a shared counter; explain
the interleaving that causes the wrong result; fix it in more than one
way.

**Likely follow-ups:** Is concurrency the same as parallelism? What
happens when a thread is interrupted? Why can code work locally but fail
under load?

## 2.2 Java Memory Model and synchronization --- Must-have

-   Heap and per-thread stacks at a conceptual level.
-   Visibility, atomicity and ordering as distinct concerns.
-   `synchronized` blocks/methods, monitor ownership and reentrancy.
-   `volatile`: visibility and ordering guarantees; what it does not
    make atomic.
-   Happens-before relationships: monitor unlock/lock, volatile
    write/read, thread start/join and safe publication.
-   Atomic classes and compare-and-set (CAS).
-   Safe publication, final-field guarantees and object construction.
-   Double-checked locking and correct use of `volatile`.
-   Lock granularity, critical sections and contention.
-   Why unsafely shared state creates bugs even when individual
    operations look simple.

**Practise:** Compare a plain field, a `volatile` field and an
`AtomicInteger`; implement a thread-safe counter; safely publish a
configuration object.

**Likely follow-ups:** Is `volatile` enough for incrementing a counter?
What does happens-before guarantee? Why is double-checked locking
subtle? What is the difference between visibility and atomicity?

## 2.3 Locks, deadlocks and coordination --- Must-have

-   Intrinsic locks vs `ReentrantLock`.
-   `tryLock`, timed locking, interruptible locking and `Condition`.
-   Deadlock, livelock, starvation and priority inversion conceptually.
-   Lock ordering and avoiding nested locks.
-   `ReadWriteLock` and `StampedLock` at a high level.
-   `Semaphore`, `CountDownLatch`, `CyclicBarrier` and their use cases.
-   `ThreadLocal`, appropriate use cases and cleanup in pooled threads.
-   Minimising lock scope without exposing inconsistent state.

**Practise:** Build a two-account transfer example; reproduce a
deadlock; resolve it with a consistent lock order; coordinate multiple
workers with a latch.

**Likely follow-ups:** How would you diagnose a deadlock? When is
`ReentrantLock` useful over `synchronized`? What happens if a
`ThreadLocal` is not cleared in a thread pool?

## 2.4 Executors and asynchronous programming --- Must-have

-   Why use executors instead of creating threads per task.
-   `Executor`, `ExecutorService`, scheduled executors and shutdown
    semantics.
-   Fixed, cached and scheduled thread pools; queues and rejection
    policies.
-   `Future`, cancellation, timeouts and exception propagation.
-   `CompletableFuture`: `thenApply`, `thenCompose`, `thenCombine`,
    `allOf`, `anyOf`, exceptional recovery and timeouts.
-   Synchronous vs asynchronous continuations; choosing an executor
    explicitly.
-   Blocking operations inside asynchronous pipelines.
-   Backpressure, bounded queues and overload protection.
-   Thread-pool sizing for CPU-bound vs I/O-bound work.
-   Graceful shutdown and draining work.

**Practise:** Build a bounded task executor; aggregate results from
independent calls; implement timeout and failure handling; demonstrate
why an unbounded queue can be dangerous.

**Likely follow-ups:** `thenApply()` vs `thenCompose()`? `Future` vs
`CompletableFuture`? What happens if a task throws? Which thread runs a
continuation? How would you prevent overload?

## 2.5 Concurrent collections and concurrent algorithms --- Must-have

-   `ConcurrentHashMap` vs `HashMap` vs synchronized maps.
-   Atomic compound operations such as `computeIfAbsent`, `merge` and
    `putIfAbsent`.
-   `CopyOnWriteArrayList` use cases and write costs.
-   `BlockingQueue` and producer-consumer patterns.
-   Atomic variables, CAS and contention.
-   ForkJoinPool and work stealing conceptually.
-   Why thread-safe individual operations do not automatically make a
    multi-step workflow atomic.

**Practise:** Implement producer-consumer with a bounded queue; maintain
concurrent counts; compare a synchronized map with a concurrent map.

**Likely follow-ups:** Why doesn't `ConcurrentHashMap` make every
sequence of operations atomic? When is copy-on-write suitable? How do
you handle backpressure in a producer-consumer pipeline?

## 2.6 Virtual threads and modern concurrency --- Must-have awareness

-   Platform threads vs virtual threads.
-   Virtual-thread creation and executors; where virtual threads help.
-   Blocking I/O and scalability; why virtual threads do not accelerate
    CPU-bound work.
-   Thread-local implications and resource limits.
-   Pinning and version-specific behaviour; avoid memorising obsolete
    limitations without checking the Java version.
-   Structured concurrency and scoped values as
    evolving/version-dependent features; distinguish preview from
    finalised features.

**Practise:** Compare platform and virtual threads for a blocking I/O
workload; identify what still limits throughput (database connections,
remote APIs, CPU and rate limits).

**Likely follow-ups:** Do virtual threads replace thread pools? Can
millions of virtual threads mean millions of database connections? What
kinds of work benefit most?

## 2.7 JVM memory and garbage collection --- Must-have

-   Heap, stacks, metaspace, code cache and direct/native memory at a
    high level.
-   Object allocation, reachability and GC roots.
-   Strong, soft, weak and phantom references conceptually.
-   Generational collection and collector trade-offs.
-   G1 GC fundamentals; ZGC at a high level.
-   Stop-the-world pauses, throughput vs latency trade-offs.
-   Memory leaks caused by retained references, static collections,
    listeners, caches and thread locals.
-   `OutOfMemoryError` vs `StackOverflowError`.
-   Class loading, linking, initialization, JIT compilation and warm-up.
-   Diagnostics: heap dumps, thread dumps, GC logs, Java Flight Recorder
    and basic profiling.

**Practise:** Create a retained-object leak; interpret a thread dump;
explain a GC log or memory graph; identify whether a symptom suggests
heap pressure, thread blockage or CPU saturation.

**Likely follow-ups:** How can Java leak memory? What causes long GC
pauses? How would you investigate rising heap usage? What is the
difference between stack and heap memory?

## 2.8 Modern Java features and version awareness

-   Java 17: records, sealed classes, pattern matching for `instanceof`,
    switch expressions and text blocks.
-   Java 21: virtual threads, record patterns and pattern matching for
    `switch`.
-   Java 25: understand the permanent language/platform additions and
    distinguish them from preview features.
-   Know the Java version used by the target team and the application's
    compatibility constraints.
-   Use new features when they improve clarity, correctness or
    maintainability---not merely because they are new.

**Practise:** Refactor a DTO to a record where appropriate; model a
closed hierarchy with sealed classes; explain migration risks between
Java versions.

**Likely follow-ups:** When should you not use a record? What is a
preview feature? What should be checked before upgrading a production
service?

------------------------------------------------------------------------

# 3. Spring Framework and Spring Boot

## 3.1 Spring fundamentals and IoC --- Must-have

-   Why Spring exists: dependency management, modularity, testability
    and infrastructure abstractions.
-   Inversion of Control (IoC) and Dependency Injection (DI).
-   `ApplicationContext` vs `BeanFactory`.
-   Component scanning and bean registration.
-   `@Component`, `@Service`, `@Repository`, `@Controller`,
    `@RestController`, `@Configuration` and `@Bean`.
-   Constructor injection vs field/setter injection.
-   Bean naming, `@Primary`, `@Qualifier` and multiple beans of the same
    type.
-   Bean scopes: singleton, prototype and web scopes.
-   Singleton bean vs singleton design pattern.
-   Bean lifecycle, initialization and destruction callbacks.
-   Circular dependencies and why they are usually a design smell.
-   Configuration properties, profiles and externalised configuration.

**Practise:** Build a small application with multiple implementations of
one interface; select one with `@Qualifier`; write a configuration class
and explain the bean lifecycle.

**Likely follow-ups:** How does Spring create and inject beans? Why
prefer constructor injection? What happens if two beans match? Does
singleton scope make a bean thread-safe?

## 3.2 Spring Boot internals and configuration --- Must-have

-   Spring Boot vs Spring Framework.
-   Auto-configuration and conditional configuration.
-   Starter dependencies and dependency management.
-   `@SpringBootApplication` and its constituent annotations.
-   Application startup at a high level.
-   Configuration precedence, profiles and `@ConfigurationProperties`.
-   Embedded servlet containers and deployment modes.
-   Actuator, health checks and metrics.
-   Logging configuration and environment-specific settings.
-   Diagnosing startup failures, bean conflicts and configuration
    mistakes.

**Practise:** Explain why a bean was or was not created; add a custom
auto-configuration condition; externalise configuration safely.

**Likely follow-ups:** How does auto-configuration decide what to
create? How would you debug a missing bean? How should secrets be
supplied in different environments?

## 3.3 Spring AOP and proxies --- Must-have

-   Cross-cutting concerns: transactions, security, logging and metrics.
-   Aspect, advice, pointcut and join point.
-   JDK dynamic proxies vs class-based proxies.
-   Proxy invocation and interception.
-   Self-invocation and why it can bypass proxy-based advice.
-   Proxy limitations, final methods/classes where relevant, and
    framework-specific behaviour.
-   Choosing AOP vs explicit composition.

**Practise:** Create a simple logging aspect; explain why an annotated
method might not be intercepted; trace a call through a proxy.

**Likely follow-ups:** How does `@Transactional` use proxies? What is
self-invocation? When would explicit code be clearer than an aspect?

## 3.4 REST APIs and HTTP services --- Must-have

-   Controllers, request mappings and request/response DTOs.
-   HTTP methods, status codes, headers and content negotiation.
-   Path variables vs query parameters vs request bodies.
-   Validation with Bean Validation annotations and `@Valid`.
-   Global exception handling with `@ControllerAdvice` /
    `@RestControllerAdvice`.
-   Consistent error response structures; avoiding sensitive error
    leakage.
-   Pagination, sorting, filtering and API versioning.
-   Idempotent API design and safe retries.
-   Authentication vs authorisation; Spring Security basics and JWT
    concepts.
-   CORS, CSRF and input validation at an appropriate level.
-   API documentation and contract testing.
-   Interceptors vs servlet filters vs AOP: responsibilities and
    execution boundaries.

**Practise:** Build a CRUD REST API; add validation, pagination and
global error handling; design an idempotent payment endpoint.

**Likely follow-ups:** Where should validation live? Filter vs
interceptor vs AOP? Which HTTP methods are idempotent? How would you
handle duplicate client requests?

## 3.5 Transactions and persistence --- Must-have

-   `@Transactional` and proxy-based transaction boundaries.
-   Propagation and isolation levels.
-   Rollback rules and checked vs unchecked exceptions.
-   Self-invocation limitations.
-   Transaction boundaries in service-layer design.
-   JDBC vs JPA/Hibernate at a conceptual level.
-   Entity lifecycle, persistence context and dirty checking.
-   Lazy vs eager loading; N+1 query problem.
-   Optimistic vs pessimistic locking.
-   Database transactions vs distributed transactions.
-   Why not to hold database transactions open across slow network
    calls.

**Practise:** Demonstrate rollback behaviour; diagnose an N+1 query;
model a payment update with optimistic locking.

**Likely follow-ups:** Why might `@Transactional` not work? What happens
if an exception is caught inside the transaction? How do isolation
levels affect concurrent updates? Can one transaction span two
microservices?

## 3.6 Testing Spring applications --- Must-have

-   Unit tests vs integration tests vs end-to-end tests.
-   JUnit and Mockito fundamentals.
-   Testing services, controllers, validation and exception handlers.
-   `@SpringBootTest`, MVC test support and test slices.
-   Testcontainers and integration testing with real dependencies.
-   Mocking boundaries rather than internal implementation details.
-   Testing transactions, asynchronous work and failure paths.
-   Contract tests and compatibility between services.
-   Reliable test data and avoiding brittle tests.

**Practise:** Test a service with mocks; test an HTTP endpoint; add an
integration test for persistence; verify error and retry behaviour.

**Likely follow-ups:** When should a dependency be mocked? What does a
test slice exclude? How do you test Kafka or database integration
reliably?

## 3.7 Spring production readiness --- Must-have

-   Structured logging and correlation/trace IDs.
-   Metrics, health checks and readiness vs liveness.
-   Configuration and secrets management.
-   Timeouts, retries, circuit breakers and bulkheads.
-   Graceful shutdown and in-flight request handling.
-   Thread pools, connection pools and resource exhaustion.
-   API security, least privilege and dependency updates.
-   Docker packaging, environment parity and deployment configuration.
-   Debugging latency, errors, memory and thread saturation.

**Likely follow-ups:** Why can retries make an outage worse? What should
a readiness check verify? How do you trace a request across services?

------------------------------------------------------------------------

# 4. Microservices and distributed systems

## 4.1 Microservices fundamentals --- Must-have

-   Monolith, modular monolith and microservices: trade-offs.
-   Service boundaries and bounded contexts.
-   Domain-driven design basics: entities, value objects, aggregates and
    bounded contexts.
-   Database-per-service principle and data ownership.
-   Synchronous vs asynchronous communication.
-   Service discovery, API gateways and edge routing.
-   Configuration management and secrets.
-   Distributed failure modes: partial failure, latency, timeouts and
    network partitions.
-   Eventual consistency and duplicated messages.
-   Avoiding distributed monoliths and excessive service decomposition.
-   When a modular monolith is a better choice.

**Practise:** Split a hypothetical payment platform into service
boundaries; justify what belongs together; identify cross-service
dependencies and operational costs.

**Likely follow-ups:** When would you not use microservices? Why should
services own their data? How do you change a shared business workflow
without creating tight coupling?

## 4.2 Inter-service communication --- Must-have

-   HTTP/REST and synchronous request-response.
-   RPC and gRPC at a conceptual level.
-   Message brokers and asynchronous events.
-   Service discovery and internal DNS.
-   Connection pooling, deadlines, timeouts and cancellation.
-   Retry policies, exponential backoff and jitter.
-   Circuit breakers, bulkheads and fallbacks.
-   Idempotency keys and deduplication.
-   API compatibility, schema evolution and versioning.
-   Correlation IDs, tracing and propagation of context.
-   Authentication and authorisation between services.

**Practise:** Design a service call with timeouts and bounded retries;
identify which errors are retryable; define a compatible API change.

**Likely follow-ups:** Why are timeouts essential? Which failures should
not be retried? How can retries create duplicate payments? How do you
propagate trace context?

## 4.3 Message queues and event-driven architecture --- Must-have

-   Queue vs topic; point-to-point vs publish-subscribe.
-   Producer, consumer, broker, acknowledgement and consumer groups.
-   Competing consumers and work distribution.
-   Delivery semantics: at-most-once, at-least-once and effectively-once
    application behaviour.
-   Ordering guarantees and partitioning.
-   Consumer acknowledgements, redelivery and poison messages.
-   Retry topics/queues and dead-letter queues.
-   Backpressure, lag and consumer scaling.
-   Event schema evolution and compatibility.
-   Event notification vs event-carried state transfer.
-   Commands vs events; choreography vs orchestration.

**Practise:** Design an asynchronous notification flow; handle poison
messages; explain how a consumer resumes after failure; prevent
duplicate side effects.

**Likely follow-ups:** Can a queue guarantee exactly-once business
processing? What happens if a consumer commits its database transaction
but fails before acknowledging the message? How do you preserve
ordering?

## 4.4 Kafka --- Must-have for Java backend roles using messaging

-   Topics, partitions, offsets, brokers and replication.
-   Producers, keys, partition selection and ordering.
-   Consumer groups and partition assignment.
-   Consumer offsets and commit strategies.
-   Consumer lag and throughput.
-   Replication, leaders and fault tolerance.
-   Delivery semantics and idempotent producers.
-   Transactions and Kafka's exactly-once capabilities---understand
    their scope and limitations.
-   Rebalances and duplicate processing.
-   Retry and dead-letter patterns.
-   Schema Registry and Avro/Protobuf/JSON compatibility at a conceptual
    level.
-   Kafka vs traditional message queues: log-based retention, replay and
    consumer model.
-   Kafka operations: partition count, retention, monitoring and
    capacity planning.

**Practise:** Design an order/payment event pipeline; choose a message
key; handle duplicate events; reason through a consumer crash around
offset commits.

**Likely follow-ups:** What determines ordering? Can multiple consumers
in a group read one partition concurrently? What is consumer lag? Why
doesn't Kafka alone guarantee that an external database side effect
happens exactly once?

## 4.5 Microservice design patterns --- Must-have

### Reliability patterns

-   Timeout and deadline propagation.
-   Retry with exponential backoff and jitter.
-   Circuit breaker.
-   Bulkhead isolation.
-   Rate limiting and load shedding.
-   Health checks and graceful degradation.

### Data and consistency patterns

-   Saga: choreography vs orchestration.
-   Transactional outbox.
-   Idempotent consumer and deduplication.
-   CQRS: when read/write models should differ.
-   Event sourcing: benefits, costs and when not to use it.
-   Distributed transaction and two-phase commit concepts.
-   Eventual consistency and reconciliation workflows.

### Integration and architecture patterns

-   API Gateway.
-   Backend for Frontend (BFF).
-   Strangler Fig migration.
-   Anti-corruption layer.
-   Service discovery.
-   Sidecar pattern at a conceptual level.
-   Consumer-driven contract testing.
-   Database-per-service and shared-database risks.

**Practise:** Design a payment workflow involving payment, ledger and
notification services; show where an outbox, idempotency key, retry and
reconciliation process belong.

**Likely follow-ups:** Why is the outbox useful? How do saga
compensations differ from database rollback? When does CQRS add
unnecessary complexity? What if a compensation action fails?

## 4.6 Distributed systems fundamentals --- Must-have

-   Latency, throughput, availability, reliability and scalability.
-   Partial failure and why networks cannot be treated like local method
    calls.
-   Consistency models and eventual consistency.
-   CAP theorem, with its practical interpretation during network
    partitions.
-   Replication, leader/follower models and failover.
-   Read-after-write consistency and stale reads.
-   Partitioning and sharding.
-   Clock skew, ordering and timestamps.
-   At-least-once delivery, duplicate requests and idempotency.
-   Coordination, leases and distributed locking at a conceptual level.
-   Backpressure, queues and overload propagation.
-   Resilience vs redundancy; graceful degradation.

**Practise:** Trace a request across services during a partial outage;
explain stale reads after replica lag; decide how a workflow recovers
after a timeout with an unknown outcome.

**Likely follow-ups:** What does CAP actually say? Why is a timeout an
ambiguous result? How do you handle an operation that may have succeeded
remotely but whose response was lost?

## 4.7 Observability and production debugging --- Must-have

-   Logs, metrics and distributed traces: what each reveals.
-   Correlation IDs and trace/span context.
-   RED metrics (rate, errors, duration) and USE metrics (utilisation,
    saturation, errors).
-   Latency percentiles vs averages.
-   Service-level indicators and objectives (SLIs/SLOs); error budgets
    conceptually.
-   Dashboards, alerts and alert fatigue.
-   Diagnosing high latency, error spikes, CPU saturation, memory
    pressure, thread-pool exhaustion and connection-pool exhaustion.
-   Incident response, mitigation, root-cause analysis and postmortems.
-   Avoiding sensitive data in logs.

**Practise:** Investigate a hypothetical latency spike; distinguish
application, database, network and downstream causes; propose evidence
to collect before changing code.

**Likely follow-ups:** Why can average latency hide problems? What is
the difference between monitoring and observability? What should be
logged for a failed payment without leaking sensitive information?

------------------------------------------------------------------------

# 5. Good design practices and design patterns

## 5.1 SOLID, clean code and maintainability --- Must-have

-   SOLID principles applied to real service code.
-   Separation of concerns and clear module boundaries.
-   Dependency inversion and constructor injection.
-   Domain logic vs infrastructure logic.
-   Cohesion, coupling and encapsulation.
-   Naming, method size, explicit contracts and useful error handling.
-   Immutability and reducing shared state.
-   Composition over inheritance.
-   Refactoring safely with tests.
-   Avoiding premature abstraction, overengineering and unnecessary
    design patterns.
-   Designing for change while keeping today's solution simple.

**Practise:** Refactor a controller containing business logic; separate
orchestration from domain rules; explain why each abstraction exists.

## 5.2 Common design patterns --- Must-have

### Creational

-   Singleton: lifecycle, thread safety, global state risks; compare
    with dependency-injection-managed singleton scope.
-   Factory Method / Simple Factory: hiding construction and selecting
    implementations.
-   Abstract Factory: families of related objects; when it is justified.
-   Builder: readable construction of complex objects and validation of
    invariants.

### Structural

-   Adapter: bridging incompatible interfaces.
-   Decorator: adding behaviour without changing the wrapped type.
-   Facade: simplifying a subsystem.
-   Proxy: controlling access or adding behaviour; connection to Spring
    AOP.

### Behavioural

-   Strategy: interchangeable algorithms or business rules.
-   Observer / publish-subscribe: notification and coupling trade-offs.
-   Template Method: fixed algorithm skeleton with customisable steps.
-   Chain of Responsibility: ordered processing and middleware-style
    pipelines.
-   State: behaviour that changes with explicit state transitions.
-   Command: representing an operation as an object.

**Practise:** Implement Strategy for payment routing; Factory for
provider selection; Builder for a validated request; Adapter for an
external provider; Chain of Responsibility for validation.

**Likely follow-ups:** Why this pattern instead of a conditional? What
complexity does the pattern introduce? How would you test it? Does
Spring already provide a similar mechanism?

## 5.3 API and domain design --- Must-have

-   Explicit contracts, preconditions, postconditions and invariants.
-   DTOs vs persistence entities vs domain objects.
-   Validation at boundaries and enforcement of domain invariants.
-   Avoiding leaking database models through public APIs.
-   Nullability and optional values.
-   Error taxonomy and stable error responses.
-   Backward compatibility and additive API evolution.
-   Idempotency and safe retry semantics.
-   State machines for workflows.
-   Clear separation of commands, queries and events where appropriate.

## 5.4 LLD readiness --- Must-have

-   Clarifying functional requirements, non-functional requirements and
    assumptions.
-   Identifying entities, value objects, services, repositories and
    interfaces.
-   Defining responsibilities and object relationships.
-   Modelling states, transitions, invariants and invalid operations.
-   Applying SOLID and patterns only when justified.
-   Writing working Java code, not just drawing UML.
-   Designing for extensibility, testability and concurrency where
    relevant.
-   Discussing persistence, errors and external dependencies.
-   Explaining alternatives and trade-offs.
-   Testing normal paths, edge cases and failure conditions.

**Practice designs:** parking lot, rate limiter, notification
dispatcher, payment routing engine, task scheduler, in-memory cache and
expense-sharing service.

## 5.5 HLD readiness --- Must-have

-   Functional and non-functional requirements.
-   Capacity estimation and back-of-the-envelope calculations.
-   API design, data model and service boundaries.
-   Architecture diagrams and request/data flows.
-   Load balancers, reverse proxies, API gateways and service discovery.
-   Database selection, indexing, replication, partitioning and
    sharding.
-   Caching strategy and invalidation.
-   Queues, event-driven workflows and asynchronous processing.
-   Availability, resilience, consistency and recovery.
-   Authentication, authorisation and data protection.
-   Observability, deployment, scaling and operational cost.
-   Bottleneck identification and iterative design.
-   Explicit trade-offs rather than a single supposedly perfect
    architecture.

**Practice designs:** URL shortener, notification system, payment
processing platform, order management, rate limiter, file upload service
and audit/event pipeline.

------------------------------------------------------------------------

# 6. Supporting backend knowledge

These topics are essential to explaining how a Spring Boot microservice
behaves in production.

## 6.1 HTTP and networking --- Must-have

-   Client-server model; request/response lifecycle.
-   DNS lookup, IP routing, TCP connection establishment and TLS
    handshake at a high level.
-   HTTP/1.1 vs HTTP/2 vs HTTP/3 conceptually.
-   Methods, status codes, headers, cookies and content negotiation.
-   Safe and idempotent methods; caching semantics.
-   TCP reliability, retransmission, congestion control and connection
    reuse.
-   TLS and certificate validation.
-   Timeouts, keep-alive, connection pools and cancellation.
-   Forward proxy vs reverse proxy; load balancers.
-   Latency sources and the cost of remote calls.

**Practise:** Explain what happens from entering a URL to receiving a
response; trace a slow HTTP request; distinguish DNS, connection, TLS,
server processing and response time.

## 6.2 SQL and database fundamentals --- Must-have

-   Relational modelling, keys, constraints and normalisation.
-   Joins, aggregation, `GROUP BY`, `HAVING`, subqueries and window
    functions.
-   `INSERT`, `UPDATE`, `DELETE`, schema changes and safe migrations.
-   Indexes, composite-index ordering and execution plans.
-   ACID, isolation levels, locks and transaction anomalies.
-   Optimistic vs pessimistic locking.
-   Offset vs cursor pagination.
-   Replication, replica lag, partitioning and sharding.
-   Connection pools, transaction duration and query performance.
-   Large-table housekeeping, archival, retention and batch processing.

**Practise:** Write representative SQL queries; inspect a query plan;
diagnose a slow query; design a schema for payments and ledger entries.

## 6.3 Caching, load balancing and traffic management --- Must-have

-   Cache-aside, read-through and write-through concepts.
-   TTL, eviction, invalidation and stale data.
-   Cache stampede, penetration and hot keys.
-   Local cache vs distributed cache.
-   Redis fundamentals and common data structures.
-   Load-balancing algorithms and health checks.
-   Rate limiting: token bucket, leaky bucket and fixed/sliding windows.
-   Throttling, quotas, admission control and load shedding.
-   Latency, throughput, saturation and queueing effects.

**Practise:** Choose a caching strategy for read-heavy data; design a
per-user rate limiter; explain how a service should behave when the
cache is unavailable.

## 6.4 Delivery and operations --- Must-have awareness

-   Git workflow, code review and build pipelines.
-   Maven/Gradle dependency management and reproducible builds.
-   Unit, integration, contract and end-to-end tests.
-   CI/CD stages, artefact promotion and environment configuration.
-   Docker images, containers, ports, environment variables and secrets.
-   Kubernetes basics: pods, deployments, services, config maps,
    secrets, probes, autoscaling and rolling updates.
-   Cloud basics, especially AWS regions, availability zones, IAM,
    networking, compute, databases, object storage and monitoring.
-   Rolling, blue-green and canary deployments.
-   Health checks, graceful shutdown, rollback and database migration
    safety.

**Practise:** Explain how a code change reaches production; containerise
a Spring Boot service; outline how you would deploy it safely and roll
back a bad release.

------------------------------------------------------------------------

# 7. Cross-topic interview practice

The strongest answers connect concepts instead of treating them as
separate facts. Use scenarios like these to test that understanding.

1.  **Duplicate payment request:** HTTP idempotency, database
    uniqueness, transaction boundaries, retries and distributed failure.
2.  **Slow Spring Boot endpoint:** tracing, thread pools, connection
    pools, query plans, downstream latency and timeouts.
3.  **Kafka consumer processes an event twice:** delivery semantics,
    idempotency, database transactions, offsets and outbox/inbox
    patterns.
4.  **Heap usage grows continuously:** object retention, caches, static
    collections, thread locals, heap dumps and GC logs.
5.  **A new payment provider must be added:** Strategy, Factory,
    interfaces, SOLID, validation and provider-specific failure
    handling.
6.  **One downstream service is unavailable:** timeouts, retries,
    circuit breakers, bulkheads, fallbacks and user-visible consistency.
7.  **A database update races with another request:** isolation,
    optimistic/pessimistic locking, constraints and retry semantics.
8.  **A service needs to scale:** statelessness, load balancing,
    bottlenecks, caching, horizontal scaling and database capacity.

For each scenario, prepare to: - State assumptions and clarify
requirements. - Explain the simplest correct solution. - Describe
failure modes and edge cases. - Compare at least one alternative. -
Defend the selected trade-offs. - Explain how you would test and observe
the solution in production.

------------------------------------------------------------------------

# 8. Completion standard

A topic is ready for interview use when you can do all of the following
without relying on memorised wording:

-   [ ] Explain the concept clearly in about one to two minutes.
-   [ ] Go deeper into its mechanism when asked.
-   [ ] Write or trace a relevant code example.
-   [ ] Compare it with the closest alternative.
-   [ ] Explain trade-offs and situations where it is a poor fit.
-   [ ] Answer follow-ups about concurrency, failures, performance or
    testing where relevant.
-   [ ] Connect it to a realistic production scenario.

**Guiding principle:** Prioritise depth over checklist completion. A
smaller set of concepts understood deeply---with clear explanations,
working examples and defensible choices---is more valuable than
superficial familiarity with every topic.
