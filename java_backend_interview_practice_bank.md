# Java Backend Interview Practice Bank

## Coding · Core Java · Concurrency · Spring Boot · SQL · Microservices · LLD · HLD

**Companion to:** *Java Backend Interview Preparation Curriculum*

**Purpose:** A practical problem bank aligned to the curriculum. It is
intentionally organised by topic rather than by week or date. The
prompts are original practice exercises informed by recurring topics in
public Java interview guides and candidate-reported interviews; they are
not claimed to be verbatim questions from any employer.

**Target level:** Experienced Java/backend engineer (roughly 3+ years).
DSA-heavy algorithm drills are excluded, except for basic data
structures needed to demonstrate Java fluency.

------------------------------------------------------------------------

## How to use each problem

For every coding or design prompt:

1.  Clarify assumptions and requirements before solving.
2.  State a straightforward approach first, then improve it if needed.
3.  Write working code or a clear design.
4.  Explain why you chose the API, data structure, abstraction or
    architecture.
5.  Discuss complexity, correctness, edge cases, failure modes and
    testing.
6.  Answer the follow-up questions without changing the subject.
7.  Summarise the solution in 60--120 seconds as if the interviewer
    asked, "Walk me through your approach."

### Completion checklist

-   [ ] I clarified assumptions.
-   [ ] I produced a working solution or coherent design.
-   [ ] I explained the key mechanism, not just the definition.
-   [ ] I justified the choices and compared an alternative.
-   [ ] I covered edge cases, failure modes and testing.
-   [ ] I answered follow-up questions.
-   [ ] I can repeat the explanation without notes.

------------------------------------------------------------------------

# 1. Core Java coding exercises

## 1.1 OOP, immutability and object contracts

### CJ-01 --- Implement an immutable `Money` value object

Create a `Money` class with amount and currency. Prevent invalid states,
support addition only for compatible currencies, and implement equality
correctly.

**Must demonstrate:** encapsulation, immutability, `BigDecimal`,
validation, `equals()` and `hashCode()`.

**Follow-ups** - Why use `BigDecimal` rather than `double`? - Should
currency conversion belong in this class? - How do you prevent callers
from changing internal state? - What should happen when currencies
differ? - How would you test rounding and scale behaviour?

### CJ-02 --- Fix a broken `HashMap` key

Given a class used as a map key whose equality-relevant field can
change, reproduce a failed lookup and refactor the design.

**Must demonstrate:** equality/hash contracts, mutability, collection
invariants.

**Follow-ups** - Does a hash collision mean two keys are equal? - What
if `equals()` is overridden without `hashCode()`? - Why is mutability
especially dangerous for keys in hash-based collections?

### CJ-03 --- Model payment providers with interfaces

Design a small API supporting multiple payment providers with different
request formats and response behaviours. Avoid a long conditional chain.

**Must demonstrate:** abstraction, composition, polymorphism, Strategy
and possibly Factory.

**Follow-ups** - Where should provider selection live? - How would you
add a new provider without modifying stable business logic? - What if
providers have different capabilities? - How do you prevent an
abstraction from becoming overengineered?

### CJ-04 --- Refactor a god class

A `PaymentService` validates requests, calculates fees, calls a
provider, writes database records, sends notifications and formats HTTP
responses. Refactor responsibilities.

**Must demonstrate:** SOLID, cohesion, dependency inversion, testing
boundaries.

**Follow-ups** - Which responsibilities should remain together? - How do
you avoid creating too many tiny classes? - Which operations need a
transaction? - Which actions should be asynchronous?

## 1.2 Collections and Java APIs

### CJ-05 --- Transaction frequency and aggregation

Given a list of transactions, calculate counts and total amounts per
currency. Ignore or reject invalid records according to a stated policy.

**Must demonstrate:** maps, loops or streams, `BigDecimal`, validation.

**Follow-ups** - How would you preserve deterministic output order? -
What happens if a currency is missing? - Would you choose streams or a
loop in production? Why?

### CJ-06 --- Implement an LRU cache

Implement a fixed-capacity least-recently-used cache with `get` and
`put` operations. Aim for O(1) average operations.

**Must demonstrate:** HashMap plus doubly linked list, invariants,
eviction.

**Follow-ups** - How would you make it thread-safe? - What happens at
capacity zero? - Would you use `LinkedHashMap` in production? When is a
custom implementation justified? - How would you add TTL expiration?

### CJ-07 --- Build a generic bounded queue

Implement a bounded queue with enqueue/dequeue operations and
well-defined behaviour when full or empty. First make it
single-threaded; then discuss a concurrent version.

**Must demonstrate:** generics, data structure invariants, API
contracts.

**Follow-ups** - Should enqueue block, fail immediately or time out? -
How do you prevent null elements if the API disallows them? - What
changes for a thread-safe queue?

### CJ-08 --- Sort with multiple criteria

Sort payments by status priority, then timestamp, then amount. Define
deterministic handling of null or missing fields.

**Must demonstrate:** `Comparator`, comparator composition, stable and
deterministic ordering.

**Follow-ups** - `Comparable` vs `Comparator`? - What can go wrong if a
comparator violates its contract? - How would you sort in reverse order
for only one field?

### CJ-09 --- Group and transform nested data

Given customers with lists of transactions, produce a flat list of
transaction summaries, grouped by customer and ordered by date.

**Must demonstrate:** `map`, `flatMap`, collectors, null/empty handling.

**Follow-ups** - Why is `flatMap` appropriate? - What if two records
have the same key in `Collectors.toMap()`? - When would a loop be
clearer than a stream pipeline?

### CJ-10 --- Implement a basic linked list and tree

Implement a singly linked list and a binary tree with insert/search or
traversal operations. Focus on correctness and readable Java, not
algorithm puzzle difficulty.

**Must demonstrate:** generics, references, encapsulation, edge cases,
iterative vs recursive traversal.

**Follow-ups** - What invariants must always hold? - How do you test
empty, one-node and deeply nested structures? - What is the
stack-overflow risk of recursive traversal?

------------------------------------------------------------------------

# 2. Java Streams and functional programming practice

For each problem, solve once with streams and once with a conventional
loop where useful. Be ready to defend which version you would ship.

### ST-01 --- Find the top three distinct transaction amounts

Given transactions, return the three largest distinct amounts,
descending. Define behaviour when fewer than three exist.

**Follow-ups:** Where should `distinct()` occur? How is ordering
guaranteed? What if amounts are `BigDecimal` values with different
scales?

### ST-02 --- Find the latest transaction per customer

Return one latest transaction per customer. Define a deterministic
tie-breaker when timestamps match.

**Follow-ups:** `groupingBy` vs `toMap`? How do you handle duplicate
timestamps? How would you do this efficiently in SQL instead?

### ST-03 --- Find duplicate values and their counts

Given a list of strings, return only values appearing more than once
with their counts.

**Follow-ups:** How do you normalise case? What is the time and space
complexity? Is a stream solution more readable here?

### ST-04 --- Partition valid and invalid records

Separate transaction records based on multiple validation rules and
report counts for each group.

**Follow-ups:** `partitioningBy` vs `groupingBy`? Should validation
throw or return a result? How would you preserve reasons for rejection?

### ST-05 --- Flatten nested collections

Convert `List<Customer>` where each customer has `List<Transaction>`
into a flat stream of transaction records enriched with customer
identifiers.

**Follow-ups:** `map` vs `flatMap`? How do you handle null lists? How do
you avoid losing parent context?

### ST-06 --- Aggregate with downstream collectors

Group transactions by currency and calculate count, total, minimum and
maximum in one pass.

**Follow-ups:** Can a collector be parallelised safely? What is the
difference between mutable reduction and `reduce`? How would you handle
empty groups?

### ST-07 --- Merge duplicate keys safely

Convert a list of provider records into a map keyed by provider ID, with
an explicit merge policy for duplicates.

**Follow-ups:** What happens if no merge function is provided? Which
duplicate should win? Is "last wins" deterministic for parallel streams?

### ST-08 --- Diagnose a broken stream pipeline

Review a pipeline that mutates a shared `ArrayList` inside
`parallelStream()` and occasionally loses or corrupts results. Explain
the failure and rewrite it.

**Follow-ups:** Why is shared mutable state unsafe? When are parallel
streams useful? Which executor does a parallel stream commonly use?

### ST-09 --- Use `Optional` appropriately

Refactor nested null checks for finding a customer's preferred payment
method, while preserving a clear distinction between "not found" and
"invalid request."

**Follow-ups:** `orElse` vs `orElseGet`? When should you not use
`Optional`? Should absence always be treated as an error?

### ST-10 --- Streams code review

Review a long stream pipeline with repeated traversals, side effects,
hidden exceptions and unclear collectors. Identify correctness and
readability issues and propose a clearer version.

**Follow-ups:** What is the biggest correctness risk? What would you
test? When is a loop the better engineering choice?

------------------------------------------------------------------------

# 3. Core Java and concurrency code-review drills

For each prompt, identify the bug, explain the execution interleaving or
contract violation, fix it, and write a test that would fail before the
fix.

### CC-01 --- Non-atomic counter

Several threads increment a shared integer. The final count is sometimes
too low.

**Cover:** race conditions, `synchronized`, atomics, visibility vs
atomicity.

**Follow-ups:** Is `volatile` sufficient? What are the trade-offs of a
lock vs `LongAdder` for high-contention statistics?

### CC-02 --- Broken double-checked locking

Review a lazy singleton implementation using a null check outside and
inside a synchronized block.

**Cover:** safe publication, `volatile`, class initialisation and
singleton alternatives.

**Follow-ups:** Why can instruction reordering matter? Is a DI-managed
singleton necessarily the same as the Singleton design pattern?

### CC-03 --- Deadlock in account transfers

Two threads transfer money between accounts while locking the source and
destination in opposite orders.

**Cover:** deadlock, lock ordering, atomicity and transaction
invariants.

**Follow-ups:** How would you reproduce it reliably? How would you
detect it in production? What are the trade-offs of globally ordering
locks?

### CC-04 --- Unsafe shared collection

Multiple threads write to a regular `HashMap`. Refactor it for
concurrent access and discuss compound operations.

**Cover:** `ConcurrentHashMap`, atomic map methods, external locking and
workflow-level atomicity.

**Follow-ups:** Does thread-safe `put()` make a read-modify-write
sequence atomic? When is a concurrent map not enough?

### CC-05 --- Executor overload

A service submits tasks to an executor with an unbounded queue. Latency
and memory usage grow during traffic spikes.

**Cover:** bounded queues, pool sizing, rejection policies, backpressure
and load shedding.

**Follow-ups:** What should the service do when saturated? How do you
size the pool? Why can simply increasing thread count make things worse?

### CC-06 --- `CompletableFuture` failure handling

Two independent downstream calls should run concurrently and their
results should be combined. One call can time out or fail.

**Cover:** composition, combining, exception handling, explicit
executors and timeouts.

**Follow-ups:** `thenApply` vs `thenCompose`? Which thread executes a
continuation? How do you avoid blocking the common pool?

### CC-07 --- Producer-consumer pipeline

Implement a producer-consumer workflow with a bounded `BlockingQueue`,
graceful shutdown and failure handling.

**Cover:** blocking, interruption, poison-pill or equivalent shutdown
strategy, queue capacity and backpressure.

**Follow-ups:** What if the consumer fails? How do you drain work during
shutdown? How many consumers can safely process items?

### CC-08 --- ThreadLocal leak

A request-scoped value is stored in a `ThreadLocal` in a pooled server
thread but is not removed.

**Cover:** thread reuse, stale context, cleanup and safer context
propagation.

**Follow-ups:** Why can one user's context appear in another request?
What changes with virtual threads or asynchronous execution?

### CC-09 --- Virtual-thread design review

A service creates a virtual thread per incoming request, but throughput
remains poor because all requests wait for a small database connection
pool.

**Cover:** virtual threads, bottlenecks, connection pools, admission
control and downstream limits.

**Follow-ups:** What did virtual threads improve? What is still the
bottleneck? How would you protect the database?

### CC-10 --- JVM incident diagnosis

A service has rising heap usage, long pauses and intermittent latency
spikes. Propose an investigation plan.

**Cover:** metrics, GC logs, heap dump, retained references, allocation
rate and correlation with traffic.

**Follow-ups:** How do you distinguish a leak from temporary allocation
pressure? What evidence would justify changing GC settings?

------------------------------------------------------------------------

# 4. Spring Framework and Spring Boot practice

## 4.1 Implementation tasks

### SB-01 --- Build a production-style REST endpoint

Implement `POST /payments` and `GET /payments/{id}` with DTOs,
validation, status codes and consistent error responses.

**Follow-ups** - Why separate DTOs from persistence entities? - How
should validation errors be represented? - What happens if the client
retries the POST? - Which tests belong at controller, service and
integration levels?

### SB-02 --- Resolve multiple beans

Create two implementations of a `PaymentGateway` interface and inject
the correct implementation based on configuration.

**Cover:** `@Qualifier`, `@Primary`, bean names, profiles and
constructor injection.

**Follow-ups:** What happens if both candidates are primary? How do you
choose a provider dynamically per request?

### SB-03 --- Explain a missing bean

A service fails at startup because a dependency cannot be injected.
Diagnose component scanning, configuration, conditions, profiles and
bean definitions.

**Follow-ups:** How does auto-configuration work? What is the difference
between `@Component` and `@Bean`? How would you avoid circular
dependencies?

### SB-04 --- Implement global exception handling

Create a consistent error response for validation failures, missing
resources, conflicts and unexpected exceptions.

**Cover:** `@RestControllerAdvice`, exception mapping, correlation IDs
and information leakage.

**Follow-ups:** Should every exception map to HTTP 500? How do you
preserve useful internal diagnostics without exposing stack traces?

### SB-05 --- Code review for `@Transactional`

Review a service where a transactional method is called from another
method in the same class and does not behave as expected.

**Cover:** proxy-based AOP, self-invocation, propagation, rollback rules
and transaction boundaries.

**Follow-ups:** Why can self-invocation bypass advice? What happens with
a checked exception? Why should a DB transaction not remain open during
a slow remote call?

### SB-06 --- Add validation and idempotency

Implement a payment endpoint that validates the request and accepts an
idempotency key to prevent duplicate processing.

**Cover:** request validation, database uniqueness, transaction
boundaries, replay semantics and error contracts.

**Follow-ups:** What if the first request times out after committing?
How long should keys be retained? What if the same key is reused with a
different payload?

### SB-07 --- Call an external HTTP service safely

Implement a client for a downstream service with connection/read
timeouts, error mapping, retry policy and metrics.

**Cover:** HTTP client configuration, timeout budgets, retryable errors,
circuit breakers and connection pooling.

**Follow-ups:** Which HTTP failures should be retried? How do you
prevent retry amplification? How do you propagate correlation IDs?

### SB-08 --- Write meaningful tests

Test a controller, service and repository integration path. Use mocks
only at appropriate boundaries and include failure cases.

**Cover:** JUnit, Mockito, Spring test slices, Testcontainers and
contract tests.

**Follow-ups:** What does a unit test prove that an integration test
does not? How do you avoid brittle tests tied to implementation details?

### SB-09 --- Diagnose N+1 queries

A list endpoint loads hundreds of records and issues one extra query per
row. Identify the cause and compare fetch joins, entity graphs,
projections and batching.

**Follow-ups:** Why not make every relationship eager? What are
pagination pitfalls with fetch joins? How would you confirm the fix?

### SB-10 --- Production readiness review

Review a Spring Boot service with secrets in source code, no timeouts,
excessive logging, no health checks and unbounded work queues.
Prioritise fixes.

**Follow-ups:** Which issues are security-critical? What belongs in
liveness vs readiness? How would you roll out changes safely?

## 4.2 Spring explanation and follow-up prompts

-   Walk through Spring Boot startup and bean creation.
-   Explain IoC and DI with a concrete example.
-   Compare filters, interceptors and AOP.
-   Explain JDK dynamic proxies vs class-based proxies.
-   Explain bean scopes and singleton thread safety.
-   Explain configuration precedence and profile-specific settings.
-   Explain authentication vs authorisation and the security filter
    chain.
-   Explain JWT validation, CORS and CSRF in a browser-facing API.
-   Explain persistence context, dirty checking, entity states and lazy
    loading.
-   Explain optimistic locking and how to handle a conflict.
-   Explain graceful shutdown and in-flight requests.
-   For each answer, prepare a practical example, a limitation and at
    least three follow-ups.

------------------------------------------------------------------------

# 5. SQL and database practice

Use a relational database such as PostgreSQL or MySQL. Create a small
schema and execute the queries; do not only read the answers.

## 5.1 Suggested practice schema

``` sql
CREATE TABLE customers (
    customer_id BIGINT PRIMARY KEY,
    name VARCHAR(200) NOT NULL,
    created_at TIMESTAMP NOT NULL
);

CREATE TABLE payments (
    payment_id BIGINT PRIMARY KEY,
    customer_id BIGINT NOT NULL REFERENCES customers(customer_id),
    amount DECIMAL(18, 2) NOT NULL,
    currency CHAR(3) NOT NULL,
    status VARCHAR(30) NOT NULL,
    created_at TIMESTAMP NOT NULL
);

CREATE TABLE payment_events (
    event_id BIGINT PRIMARY KEY,
    payment_id BIGINT NOT NULL REFERENCES payments(payment_id),
    event_type VARCHAR(50) NOT NULL,
    created_at TIMESTAMP NOT NULL
);
```

Create enough sample data to include customers with no payments,
duplicate amounts, multiple currencies, repeated statuses and timestamps
that tie.

## 5.2 Query exercises

### SQL-01 --- Aggregation by status

Return payment count and total amount for each status, filtering to
groups above a specified count.

**Follow-ups:** `WHERE` vs `HAVING`? How should multiple currencies be
handled? What happens with nulls?

### SQL-02 --- Customers with no payments

Return customers who have never made a payment.

**Follow-ups:** `LEFT JOIN ... IS NULL` vs `NOT EXISTS`? How might
indexes affect the plan?

### SQL-03 --- Latest payment per customer

Return the most recent payment for each customer, with deterministic
tie-breaking.

**Follow-ups:** Window functions vs correlated subqueries? What index
could help?

### SQL-04 --- Top customers by total successful payment amount

Aggregate successful payments by customer and return the top N.

**Follow-ups:** How do you handle currencies? Can an index remove the
need to aggregate all qualifying rows?

### SQL-05 --- Detect duplicate payment requests

Assume a request table stores an idempotency key, customer ID and
request payload hash. Find duplicate keys and keys reused with different
payloads.

**Follow-ups:** Should this be enforced in application code, the
database or both? What race condition can occur without a unique
constraint?

### SQL-06 --- Running total

For each customer, return payments in time order with a running total.
State how you handle ties and currency.

**Follow-ups:** How do window frames work? Why does ordering matter?

### SQL-07 --- Conditional aggregation

Return one row per customer with counts of successful, failed and
pending payments.

**Follow-ups:** Conditional aggregation vs multiple joins? How does the
query behave for customers with no payments?

### SQL-08 --- Pagination

Implement page-based and cursor-based pagination for a large payment
history.

**Follow-ups:** Why can offset pagination become slow? How do you make
cursor ordering stable? What if records arrive while the client is
paging?

### SQL-09 --- Index design

Given a query filtering by customer, status and date range, propose an
index and explain column ordering.

**Follow-ups:** What is a covering index? Why can too many indexes hurt
writes? How do you use an execution plan to validate the choice?

### SQL-10 --- Transaction race

Two concurrent requests attempt to update a payment from `PENDING` to
`SUCCESS`.

**Follow-ups:** How can conditional updates, optimistic locking or row
locks help? What does the caller see when the update loses the race?

### SQL-11 --- Data retention and housekeeping

Design a retention and archival strategy for a table with billions of
payment events.

**Follow-ups:** Partitioning vs sharding? How do you archive without
disrupting writes? How do you validate data integrity after migration?

### SQL-12 --- Replication and stale reads

A payment is written to the primary database but immediately read from a
lagging replica.

**Follow-ups:** What consistency does the user expect? How might you
route read-after-write requests? What are the availability and cost
trade-offs?

## 5.3 Database verbal drills

-   Explain ACID and a real example of each property.
-   Compare `READ COMMITTED`, `REPEATABLE READ` and `SERIALIZABLE` at
    the chosen database's actual semantics.
-   Explain dirty reads, non-repeatable reads, phantom reads and lost
    updates.
-   Explain optimistic vs pessimistic locking.
-   Explain normalisation and when denormalisation is useful.
-   Explain primary keys, unique constraints, foreign keys and check
    constraints.
-   Explain replication vs partitioning vs sharding.
-   Explain connection pools and why transactions should be short.
-   Explain how to investigate a slow query.
-   Explain why database-per-service complicates cross-service reporting
    and transactions.

------------------------------------------------------------------------

# 6. HTTP, networking, messaging and Kafka

## 6.1 HTTP/networking scenarios

### NW-01 --- Trace a request

Explain what happens from entering a URL to receiving an HTTP response,
including DNS, TCP, TLS, proxies, load balancing and server processing.

**Follow-ups:** What changes with connection reuse? Which parts may be
cached? Where can latency occur?

### NW-02 --- Diagnose a timeout

A caller times out, but the downstream service may have completed the
operation.

**Follow-ups:** Why is the result ambiguous? How should idempotency
work? Which timeout should be shorter---the client deadline or the
server's downstream timeout?

### NW-03 --- Choose status codes and API semantics

Design responses for invalid input, unauthenticated access, forbidden
access, missing resources, conflicts, throttling and unexpected
failures.

**Follow-ups:** When is 202 appropriate? What does 409 communicate?
Which methods are safe or idempotent?

### NW-04 --- Reverse proxy vs load balancer

Explain the roles and overlap between a reverse proxy, API gateway and
load balancer.

**Follow-ups:** Where should TLS terminate? Where should rate limiting
occur? What should not be trusted from arbitrary forwarded headers?

## 6.2 Messaging and Kafka scenarios

### MQ-01 --- Queue vs pub/sub

Choose between point-to-point work distribution and pub/sub event
distribution for order processing and notifications.

**Follow-ups:** Can multiple consumer groups independently receive the
same event? How do you handle slow consumers?

### MQ-02 --- Consumer commits DB, then crashes

A consumer writes to a database, crashes before acknowledging/committing
its message offset, and processes the message again.

**Follow-ups:** How do you make processing idempotent? Can the DB update
and broker offset commit be one atomic transaction? What does
effectively-once mean here?

### MQ-03 --- Preserve per-payment ordering

Events for the same payment must be processed in order, but unrelated
payments should process concurrently.

**Follow-ups:** How should the key be selected? What limits parallelism?
What happens when partitions are reassigned?

### MQ-04 --- Poison message

One malformed message repeatedly fails and blocks progress.

**Follow-ups:** Retry or dead-letter? How should retry delays work? How
do you preserve enough context for replay and debugging?

### MQ-05 --- Transactional outbox

A service updates its database and must publish an event without losing
the event if the process crashes between the two actions.

**Follow-ups:** How does the outbox relay work? Can it publish
duplicates? How do consumers deduplicate? How is old outbox data cleaned
up?

### MQ-06 --- Kafka lag and rebalance

Consumer lag increases after a deployment and consumers repeatedly
rebalance.

**Follow-ups:** What metrics would you inspect? How do processing time
and poll configuration matter? When is increasing partition count
useful?

------------------------------------------------------------------------

# 7. Microservices and resilience practice

### MS-01 --- Split a monolith

A payments application contains customer, payment, ledger, reporting and
notification modules. Propose service boundaries and a migration plan.

**Must cover:** domain boundaries, data ownership, API/event contracts,
deployment risks and when not to split.

**Follow-ups:** Which service owns payment state? How does reporting
query data? How would you migrate without a risky big-bang cutover?

### MS-02 --- Design a resilient downstream call

A service calls a provider that sometimes responds slowly and sometimes
returns errors.

**Must cover:** timeout budgets, retries with backoff/jitter, circuit
breaker, bulkhead, metrics and fallback semantics.

**Follow-ups:** Which errors are retryable? What if a payment outcome is
unknown? When is fallback unsafe?

### MS-03 --- Implement a saga

A workflow reserves funds, creates an order and schedules fulfilment.
Later steps may fail.

**Must cover:** choreography vs orchestration, durable state,
compensating actions, retries and reconciliation.

**Follow-ups:** Is compensation the same as rollback? What if
compensation fails? How do you make each step idempotent?

### MS-04 --- Avoid a distributed monolith

Several services must be deployed together because they share tables and
make synchronous calls in a cycle.

**Follow-ups:** Which coupling is most harmful? How would you introduce
clear ownership? Would a modular monolith be better?

### MS-05 --- Design a rate limiter

Design a per-user and per-client rate limiter for a horizontally scaled
API.

**Must cover:** token bucket or another algorithm, key design,
distributed state, latency, limits, failure mode and observability.

**Follow-ups:** What happens if Redis is unavailable? How do multiple
instances coordinate? How do you avoid a single hot key?

### MS-06 --- Safe deployment with schema changes

A service and its database schema must evolve without downtime while old
and new application versions may run simultaneously.

**Must cover:** expand-and-contract migrations, backward compatibility,
backfills, rollback limitations and deployment sequencing.

**Follow-ups:** Why can rolling back code be unsafe after a schema
migration? How do you prove both versions are compatible?

------------------------------------------------------------------------

# 8. Design pattern implementation exercises

### DP-01 --- Strategy: payment routing

Select a payment provider based on currency, amount, region and provider
health. Keep routing rules testable.

**Follow-ups:** Where should selection rules live? How do you handle no
eligible provider? When does Strategy become unnecessary?

### DP-02 --- Factory: provider construction

Create provider adapters from configuration while avoiding `new` calls
and conditionals throughout the business layer.

**Follow-ups:** Is a factory still needed if Spring can inject a map of
implementations? How should invalid configuration fail?

### DP-03 --- Adapter: external provider integration

Integrate two providers with incompatible request and response models
behind a stable internal interface.

**Follow-ups:** Where should provider-specific error codes be
translated? How do you prevent the adapter from leaking provider
details?

### DP-04 --- Decorator: instrumentation

Add timing, metrics and logging to a component without changing its core
business behaviour.

**Follow-ups:** Why use a decorator instead of inheritance? How do you
avoid logging sensitive payloads?

### DP-05 --- Chain of Responsibility: validation

Build an ordered validation pipeline for payment requests. Some checks
are cheap; others call external services.

**Follow-ups:** How do you control order? Which checks should
short-circuit? How should failures be represented?

### DP-06 --- State: payment lifecycle

Model transitions such as `CREATED`, `PENDING`, `SUCCESS`, `FAILED` and
`REVERSED`, including invalid transitions.

**Follow-ups:** Where are invariants enforced? How do you handle
duplicate or out-of-order events? When would a state machine library be
justified?

------------------------------------------------------------------------

# 9. LLD practice problems

For each design, first clarify requirements, then sketch classes and
interfaces, then write compilable Java for the core flows. Explain why
each abstraction exists.

## LLD-01 --- Parking lot

Support multiple vehicle types, parking spot sizes, entry/exit,
ticketing, fee calculation and availability.

**Must cover:** entities, spot allocation strategy, pricing strategy,
ticket lifecycle, concurrency and extensibility.

**Follow-ups:** How do you prevent two vehicles receiving the same spot?
How would reservations change the design? Where is persistence needed?

## LLD-02 --- Notification dispatcher

Support email, SMS and push providers, templates, user preferences,
retries and delivery status.

**Must cover:** Strategy, Factory/DI, queue-based asynchronous
execution, idempotency and provider failure.

**Follow-ups:** How do you add a channel? How do you avoid duplicate
notifications? How do you handle provider rate limits?

## LLD-03 --- In-memory cache

Support `get`, `put`, TTL and eviction policy; discuss concurrency and
capacity limits.

**Must cover:** interface design, cache entry lifecycle, LRU or another
eviction strategy, clock/testing strategy and thread safety.

**Follow-ups:** How do you avoid a global lock bottleneck? What happens
when many entries expire at once? How would you add metrics?

## LLD-04 --- Rate limiter library

Implement a reusable per-key token-bucket rate limiter with a defined
concurrency contract.

**Must cover:** time abstraction, token refill, concurrency, API
semantics and testability.

**Follow-ups:** How do you test without sleeping? What changes for
distributed enforcement? What is the memory-cleanup strategy for
inactive keys?

## LLD-05 --- Task scheduler

Support scheduling tasks, cancellation, execution status, retries and
bounded concurrency.

**Must cover:** state transitions, scheduling abstraction, executor
management, error handling and graceful shutdown.

**Follow-ups:** How do you prevent a task from running twice? What if
the process restarts? What belongs in durable storage?

## LLD-06 --- Payment routing engine

Route payments across provider adapters according to rules, capabilities
and health.

**Must cover:** Strategy, Factory, domain models, rule ordering,
observability and test seams.

**Follow-ups:** How do you avoid a provider outage causing cascading
failure? How do you version routing rules? What should happen when no
route qualifies?

## LLD-07 --- Audit event recorder

Record important domain actions with actor, timestamp, correlation ID
and immutable event details.

**Must cover:** append-only semantics, sensitive-data handling,
persistence boundary, asynchronous delivery and failure policy.

**Follow-ups:** Can audit writes be dropped? How do you handle ordering?
How do you prevent application logs from being mistaken for an audit
trail?

## LLD-08 --- Expense-sharing service

Support users, groups, expenses, split strategies, balances and
settlement records.

**Must cover:** domain invariants, Strategy for split calculations,
decimal arithmetic, validation and persistence.

**Follow-ups:** How do you handle rounding? How do you correct an
expense? How would concurrent updates affect balances?

------------------------------------------------------------------------

# 10. HLD and system-design practice problems

For each prompt, produce: requirements, rough sizing, APIs, data model,
architecture diagram, request flow, bottlenecks, failure handling,
security, observability and trade-offs.

## HLD-01 --- API rate limiter

Design a distributed rate limiter used by multiple API instances.

**Explore:** algorithms, keying, shared state, latency, hot keys,
failure policy and fairness.

**Follow-ups:** Local vs distributed limits? What if the state store
fails? How do you handle burst traffic?

## HLD-02 --- Notification platform

Design a service that sends email, SMS and push notifications to a large
user base.

**Explore:** API, queues, provider adapters, user preferences, retries,
DLQ, rate limits, templates and delivery tracking.

**Follow-ups:** How do you prevent duplicates? How do you prioritise
urgent messages? How do you handle provider outages?

## HLD-03 --- Payment processing platform

Design an API that accepts payment requests, calls external providers,
maintains payment state and emits events.

**Explore:** idempotency, state machine, database transaction, outbox,
provider timeout, reconciliation, auditability and security.

**Follow-ups:** What if the provider succeeds but the response is lost?
How do you prevent double charging? How do you reconcile unknown
outcomes?

## HLD-04 --- URL shortener

Design URL creation and redirection at high read volume.

**Explore:** key generation, collision handling, database/index choice,
cache, expiry, abuse prevention and analytics.

**Follow-ups:** How would you estimate storage? What if a URL becomes
extremely popular? How do you prevent malicious links?

## HLD-05 --- Order management

Design order creation, inventory reservation, payment and fulfilment
across services.

**Explore:** service boundaries, event flow, saga, outbox, idempotency,
consistency and compensations.

**Follow-ups:** What if payment succeeds but inventory reservation
fails? Which state is authoritative? How does the user see progress?

## HLD-06 --- Audit/event pipeline

Design a high-throughput pipeline that ingests events, stores them for
analysis and supports replay.

**Explore:** partitioning, ordering, retention, schema evolution,
consumer groups, backpressure and storage lifecycle.

**Follow-ups:** How do you handle late or duplicate events? What
ordering is actually required? How do you replay without repeating side
effects?

## HLD-07 --- File upload service

Design large file uploads with metadata, access control, resumability
and asynchronous processing.

**Explore:** object storage, pre-signed URLs, multipart uploads,
metadata database, scanning, events and lifecycle policies.

**Follow-ups:** How do you resume after failure? How do you prevent
unauthorised access? What if processing fails after upload?

## HLD-08 --- Read-heavy product catalogue

Design a catalogue with frequent reads, less frequent updates and
search/filter functionality.

**Explore:** caching, search index, database ownership, invalidation,
replication lag and consistency.

**Follow-ups:** How stale can the cache be? How are updates propagated?
What happens when the search index falls behind?

## HLD-09 --- Job processing platform

Design a system that accepts jobs, schedules them, executes workers,
retries failures and reports status.

**Explore:** queues, scheduling, leases, idempotency, worker scaling,
cancellation, poison jobs and observability.

**Follow-ups:** How do you recover jobs after worker death? How do you
prevent two workers executing the same job? What is the retry policy?

## HLD-10 --- Monolith-to-microservices migration

Design a staged migration of a business-critical monolith with no
planned downtime.

**Explore:** domain boundaries, strangler pattern, data ownership, dual
reads/writes risks, outbox, observability and rollback.

**Follow-ups:** How do you validate parity? How do you avoid two sources
of truth? What is the first module you would extract, and why?

## HLD-11 --- Financial transaction history

Design a queryable transaction history for customers with high write
volume, retention requirements and strict access controls.

**Explore:** write path, read models, indexing, partitioning, archival,
replicas, pagination and auditability.

**Follow-ups:** How do you ensure read-after-write behaviour? How do you
handle corrections? How do you enforce tenant/customer access?

## HLD-12 --- Capacity estimation drill

For any HLD above, estimate: - Requests per second and peak-to-average
ratio. - Average request/event size and daily data volume. -
Retention-based storage requirements. - Read/write ratio and cache
hit-rate implications. - Queue backlog and consumer capacity. -
Replication overhead and rough network bandwidth.

State assumptions explicitly. Exact arithmetic is less important than
making reasonable assumptions, checking units and using the estimates to
justify architecture choices.

------------------------------------------------------------------------

# 11. Cross-topic incident scenarios

These are especially useful for experienced-engineer interviews because
they require more than textbook definitions.

### INC-01 --- Duplicate payment after timeout

The client retries because it did not receive a response. The first
request may have completed successfully.

**Explain:** idempotency key, unique constraint, transaction boundaries,
provider idempotency and reconciliation.

### INC-02 --- Latency spike after deployment

The service's p95 latency rises, thread count grows and the database
connection pool is exhausted.

**Explain:** trace analysis, thread dumps, connection acquisition time,
downstream latency, deployment diff and mitigation.

### INC-03 --- Kafka consumer lag

The backlog grows even though all consumers are healthy.

**Explain:** processing time, partition count, hot partitions, batch
size, retries and downstream bottlenecks.

### INC-04 --- Memory growth over days

Heap usage rises slowly after every deployment and does not return to
its previous baseline.

**Explain:** retained objects, caches, static references, thread locals,
heap dumps and allocation profiling.

### INC-05 --- Database migration under load

A new index or schema change is required on a very large table.

**Explain:** lock impact, online/concurrent index creation where
supported, backfill, validation, rollback and deployment compatibility.

### INC-06 --- Downstream outage

A provider's latency increases, retries spike and the caller's own
requests begin timing out.

**Explain:** timeout budgets, retry amplification, circuit breaker,
bulkhead, rate limits and graceful degradation.

### INC-07 --- Incorrect concurrent state transition

Two requests both observe a payment as `PENDING` and attempt different
terminal transitions.

**Explain:** optimistic locking, conditional update, transaction
isolation, state-machine invariants and conflict response.

### INC-08 --- Bad deployment

A new service version is incompatible with existing messages or database
schema.

**Explain:** compatibility, expand-and-contract, consumer-driven
contracts, rollback constraints and replay strategy.

------------------------------------------------------------------------

# 12. Articulation and follow-up question bank

Use these prompts after solving any problem. Answer them aloud; do not
merely list keywords.

## Explain

-   What problem does your solution solve?
-   Walk through the execution from input to output.
-   Which invariants must always hold?
-   What is the most important implementation detail?

## Justify

-   Why did you choose this data structure, API, pattern or
    architecture?
-   What alternative did you consider?
-   What trade-off did you accept?
-   At what scale or complexity would your choice stop being
    appropriate?

## Probe correctness

-   What are the boundary cases?
-   What if the input is missing, duplicated, malformed or out of order?
-   What if two requests arrive concurrently?
-   What if a dependency fails halfway through?
-   What if the client retries after a timeout?

## Probe operations

-   How would you test it?
-   What metrics and logs would you add?
-   How would you diagnose a production failure?
-   How would you deploy this change safely?
-   How would you roll it back?

## Probe design quality

-   Which SOLID principles are relevant?
-   Is this abstraction necessary?
-   What would change if a new provider, database or message broker were
    added?
-   Which component owns the data and business invariant?
-   What would you deliberately not build yet?

## A strong answer structure

1.  State the requirement and assumptions.
2.  Describe the design or algorithm.
3.  Explain the key mechanism.
4.  Walk through a concrete example.
5.  Discuss trade-offs and failure modes.
6.  Explain testing and production observability.
7.  Summarise why the solution is appropriate.

------------------------------------------------------------------------

# 13. Suggested practice order

This is a dependency order, not a calendar: 1. Core Java implementation
and code review. 2. Streams and collections exercises. 3. Concurrency
bugs and executor exercises. 4. Spring Boot implementation and code
review. 5. SQL query writing and database reasoning. 6. HTTP, Kafka and
messaging scenarios. 7. Microservice resilience and consistency
scenarios. 8. Design patterns and LLD implementation. 9. HLD with sizing
and trade-offs. 10. Cross-topic incidents and timed mock interviews.

Do not try to solve every prompt in one sitting. For each topic, first
attempt without notes, then review gaps, revise the implementation and
repeat the explanation.

------------------------------------------------------------------------

# 14. Public references used to identify recurring practice areas

The problems in this document are original prompts aligned to the
curriculum. Public references below were used to check recurring subject
areas and interview formats; individual candidate experiences are
anecdotal and do not establish a universal company rubric.

-   Baeldung, Java Concurrency Interview Questions:
    https://www.baeldung.com/java-concurrency-interview-questions
-   Baeldung, Java Collections Interview Questions:
    https://www.baeldung.com/java-collections-interview-questions
-   Public Java interview question collection spanning Java, Spring
    Boot, SQL, Kafka and operations:
    https://github.com/ViacheslavChernyshov/java-interview-questions-and-answers
-   Java Streams coding practice collection:
    https://github.com/jeevankumardev18/Java8_Streams_Coding
-   JPMC candidate report discussing Java Streams, REST calls, SQL,
    Kafka, containers and CI/CD:
    https://www.jointaro.com/interviews/companies/jpmorgan-chase/experiences/senior-software-engineer-hyderabad-telangana-january-1-2020-no-offer-positive-1136219e/
-   JPMC SDE-2 candidate report describing code review and a
    rate-limiter HLD round:
    https://www.reddit.com/r/developersIndia/comments/1ogc3v2/jpmc_sde2_interview_experience_4_yoe_java_backend/
