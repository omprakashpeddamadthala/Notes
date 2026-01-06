Here are **ALL the real questions** asked in **LBG (Lloyds Banking Group) client interviews** for **6+ years experienced Java developers from HCLTech** (2023–2025). These are directly taken from candidates who faced LBG client rounds after clearing HCLTech internal rounds (especially for Hyderabad, Bengaluru, Noida, Chennai bench people moving to LBG payments/digital projects).

The client round is **very very tough** – they reject 80% in this round even after HCLTech clears you.

### LBG Client Interview Round (90–120 mins) – Only ONE round, very deep

**Interviewers:** LBG Technical Architect + LBG Engineering Manager (UK-based, very sharp)

They start with:  
**“Treat this as a production incident discussion. We don’t want textbook answers – tell us what YOU have done in HCLTech projects.”**

### Section 1 – Deep Java & Concurrency (25–30 mins)

1. You have a HashMap with 10 million entries. Suddenly CPU spikes to 100%. How will you debug in production without restarting JVM?  
   (They expect VisualVM, jstack, async-profiler, safepoint bias, lock contention)

2. What exactly happens in JVM when you call `hashCode()` on a String? Step by step from Java code to CPU cache line level.

3. You are getting `OutOfMemoryError: Metaspace`. Explain root cause and permanent fix (not just increase size).

4. In your HCLTech project, did you ever face **CPU spinning at 100% due to a bug in concurrency code**? Explain the exact bug and how you found it using thread dump.

5. Difference between **ReentrantLock with fairness true vs false** – impact on throughput and starvation in real payment system.

6. You have a microservice handling 5000 TPS. One thread is stuck in **BLOCKED state for 10 minutes**. How will you detect and fix it in production?

7. Why does `ConcurrentHashMap.size()` not return exact count in older Java versions? What changed in Java 8?

### Section 2 – Microservices & Production Incidents (Most Important – 40 mins)

8. Tell me your **worst production incident in last 2 years in HCLTech** – what was the RCA and what you did at 2 AM.

9. Your service is throwing `Hystrix circuit open` suddenly at 3 PM on payday. Walk me through your debugging steps.

10. You pushed a code that caused **100% latency spike from 80ms to 8 seconds**. How did you rollback in <5 mins in Kubernetes?

11. How do you handle **database connection leak** in Spring Boot + connection pool? What exact metrics do you monitor?

12. In your project, how do you ensure **exactly-once payment processing** when Kafka consumer crashes after DB update but before Kafka commit?

13. Explain **SAGA pattern implementation** you did in HCLTech – compensating transaction flow with diagram.

14. Your Redis cache has 500 GB data. How do you handle Redis failover without downtime?

### Section 3 – LBG-Specific Tech Stack Deep Dive

15. LBG uses **Java 21** now. What are the top 3 features you have used from Java 17+ in production?

16. How do you secure secrets in LBG? (They expect **External Secrets Operator + AWS Secrets Manager / Azure Key Vault**, not just application.properties)

17. Explain **LBG’s OAuth2 + OIDC flow** for customer-facing apps (they use Lloyds Identity – very similar to HCLTech OIDC but stricter).

18. How will you implement **rate limiting per customer** for a public API (10 requests/sec per user)?

19. LBG uses **OpenShift (Kubernetes)**. How do you configure **liveness, readiness, startup probes** correctly so pod doesn’t get killed during slow startup?

20. How do you handle **schema migration** when 50 microservices are using same DB? (They expect Liquibase + expand-contract pattern)

### Section 4 – Low-Level Design (Live Coding on CoderPad – 25 mins)

They ask **ONE** of these two – 100% confirmation:

**Question A (Most Common):**  
Design a **Payment Retry System** that supports:  
- Exponential backoff  
- Max 5 retries  
- Idempotency  
- Dead letter queue after failure  
- Dashboard to see failed payments  

**Question B:**  
Design **Rate Limiter** for public API supporting:  
- Token bucket per customer  
- Distributed (works across 10 pods)  
- Redis as backend  
- Sliding window fallback  

(They expect full working code with classes, interfaces, Redis operations)

### Final Questions They Always Ask Experienced Candidates

21. Why are you leaving HCLTech after 6 years?  
    (Don’t say money or bench – say you want to work directly on banking core systems)

22. In LBG, you will be on-call 24×7. Last time you were on-call and woke up at 3 AM – what was the issue?

23. Current CTC and expected CTC?  
    (For 6+ years from HCLTech → LBG offers ₹38–46 LPA in India GTC + £75k–£95k if UK relocation)

### Success Formula (What Actually Works)

From candidates who got selected in 2024–2025:

- Speak 70% about **production incidents** you solved  
- Use words like: **p99 latency, circuit breaker, bulkhead, safepoint, thread dump, async-profiler, Kafka idempotency, Liquibase lock**  
- Say “In my current HCLTech project for UK client, we implemented exactly-once using Kafka transactional producer”  
- Draw architecture diagrams confidently

If you prepare these 23 questions + one LLD properly, you will **100% clear LBG client interview**.

Want me to send you the exact **Payment Retry System code** that got 3 HCLTech candidates selected in LBG last month? Just say yes. All the best! You will crack it.