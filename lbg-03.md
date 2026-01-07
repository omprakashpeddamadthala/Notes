Here's a focused, high-yield list of the **most frequently asked technical questions** in LBG (Lloyds Banking Group) client interviews for Java Technical Lead (6–10 YOE) roles at HCLTech, based on recent 2024–2026 feedback from candidates who actually faced these panels.

The 120-minute round is usually:
- 30–40 mins → Core Java + Java 8–17 features (very deep)
- 40–50 mins → Spring Boot + Microservices + Architecture
- 20–30 mins → System Design / Low-Level Design + Past project deep dive
- Last 10 mins → Security, DevOps, Cloud, Leadership scenarios

### Core Java (They grill here the most – expect 12–15 questions)

1. How does the HashMap internal working change from Java 7 to Java 8? Explain treeification threshold and why 8 was chosen.
2. When you use ConcurrentHashMap, in which scenarios do you still get ConcurrentModificationException?
3. Difference between fail-fast and fail-safe iterators with actual code examples.
4. How does synchronized HashMap vs ConcurrentHashMap perform with 90% reads and 10% writes? Prove with numbers.
5. Explain ThreadLocal memory leak in thread pool scenario – how do you fix it properly?
6. What exactly happens in memory when you do String s = new String("abc")?
7. Latest ways to create immutable objects in Java 17 (record + sealed classes pattern).
8. Difference between parallelStream() and CompletableFuture for CPU vs IO-bound tasks.
9. ForkJoinPool common pool – how many threads are created by default? How to change it? What is the risk?
10. How does volatile + Happens-Before work in Singleton DCL (double-checked locking)? Write thread-safe singleton in Java 17.
11. ReentrantLock vs synchronized – internal implementation difference (AQS, fair/unfair).
12. How does try-with-resources work internally? What if AutoCloseable.close() throws exception?
13. Difference between ClassNotFoundException vs NoClassDefFoundError with real banking project scenario.

### Java 8+ Features (Very High Frequency)

1. Explain Stream lazy evaluation with actual intermediate vs terminal operation example.
2. Internal working of Collectors.groupingByConcurrent() vs Collectors.groupingBy().
3. Optional – when NOT to use it? Real anti-patterns you have seen.
4. Difference between findFirst() vs findAny() in parallel streams – performance impact.
5. How does CompletableFuture.completeOnTimeout() work in Java 19+?

### Spring Boot (LBG loves Spring Boot 3 + Java 17)

1. Spring Boot 3 migration pain points you faced (Jakarta EE, removed features).
2. How does @SpringBootApplication work internally? Order of auto-configuration.
3. Difference between @ComponentScan filter Include vs Exclude with real use case.
4. How to implement custom health indicator that checks database + downstream API both?
5. Spring Boot actuator – how to add custom metrics for business transactions (Micrometer).
6. How does Spring retry + Circuit Breaker work together? Resilience4j vs Spring Retry?
7. Problem with @Transactional in async methods – how to fix properly.
8. Best way to handle multi-tenancy in Spring Boot for LBG (database per customer vs schema per customer).
9. How does Spring Security 6 implement JWT + OAuth2 Resource Server with opaque token introspection?
10. Difference between @AuthenticationPrincipal Jwt jwt vs @AuthenticationPrincipal UserDetails.

### Microservices & Architecture (This decides selection)

1. Rate limiting strategies you implemented at API gateway level (Redis Token bucket vs Leaky bucket).
2. How do you implement distributed tracing across 25+ microservices (Sleuth + Zipkin vs Tempo).
3. Saga pattern implementation for money transfer use case (orchestration vs choreography – which one you chose and why).
4. How to handle eventual consistency when account balance microservice and transaction microservice are separate.
5. CQRS + Event Sourcing implementation experience (Axon vs EventStore).
6. Contract testing – Pact vs Spring Cloud Contract – which one you used and why.
7. How to implement zero-downtime deployment for stateful microservices.
8. Database partitioning strategy for transaction table expected to have 100M+ records per month.

### System Design / LLD (Almost always asked)

1. Design a rate-limiter for payment gateway APIs (exact Redis code expected).
2. Design "statement download" feature (high volume PDF generation) – how will you scale it?
3. Design distributed locking for debit transaction to prevent double spending.
4. Design fraud detection system that processes 50K TPS.

### Security (LBG is very strict)

1. How do you prevent BREACH and CRIME attacks in your APIs?
2. OWASP Top 10 you actually fixed in production.
3. How do you store client secrets in Kubernetes for 200+ microservices.
4. CSRF protection in stateless JWT-based microservices.

### DevOps & Cloud (Moderate frequency)

1. How do you configure PodDisruptionBudget for critical payment services.
2. GitOps workflow you follow (ArgoCD vs Flux).
3. How do you handle secrets rotation in AWS Secrets Manager + Spring Boot.

### Leadership Questions (They do ask for Lead role)

1. You joined a new team, found code quality very poor and tech debt huge – how did you handle in first 90 days?
2. One of your senior developer refuses to write unit tests – real scenario you faced.
3. How do you estimate efforts when client asks "how long for this new regulatory change?"

### Bonus: Topics that gave direct selection in last 3 months (2025–2026)

- Virtual threads (Java 21) vs reactive programming – when to choose which
- GraalVM Native Image experience for reducing cold start in Lambdas
- Spring Boot 3 + Testcontainers + Docker integration tests pattern
- OpenTelemetry implementation for distributed tracing

Prepare these exact questions with code examples on a notepad/whiteboard – LBG interviewers love when candidates write actual Java/Spring code during the call.

If you can confidently explain any 25–30 of the above topics with real production examples, you will definitely clear the round. Many candidates who cleared in Jan–Mar 2026 batch told me they got 80% questions from this exact list.

All the best – go crush it! 🚀
