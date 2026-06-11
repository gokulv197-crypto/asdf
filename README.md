Expense Tracker is a high-performance, asynchronous RESTful API backend designed to securely manage, track, and analyze personal financial data. Built as a scalable expense analytics platform, the system implements a modern microservices-adjacent architecture featuring decoupled storage layers, write-through caching pipelines, defensive security guardrails, and event-driven out-of-band communication systems.

## Built With

- __FastAPI & Asyncio__ – Asynchronous API gateway ecosystem maximizing concurrent throughput
- __Python__ – Core development language utilizing strict type hinting and robust security standard libraries
- __SQLAlchemy__ – Object-Relational Mapping (ORM) framework handling atomic persistent transactions
- __MySQL__ – Relational database infrastructure optimized for structured financial persistence
- __JWT (JSON Web Token)__ – Stateless security mechanism driving dual-token authentication lifecycles
- __Argon2id__ – Memory-hard password hashing standard protecting client credential stores
- __Docker__ – Containerization platform ensuring isolated service environments and deployment parity
- __Twilio API__ – Programmatic communications engine managing out-of-band SMS routing

## System Architecture

- __Asynchronous Enterprise Stack__: Engineered entirely with FastAPI utilizing Python's asyncio ecosystem to maximize concurrent throughput. It features persistent storage mapped through SQLAlchemy ORM to a MySQL relational database, optimized with explicit composite indexing and foreign key cascade deletion integrity.
- __Decoupled Multi-Instance Memory Tier__: Implements three isolated Redis data pools to prevent cross-contamination of infrastructure memory: 
    - __High-Speed Cache Engine__: Reduces relational database load by executing an eviction/write-through cache pattern for persistent user transactions.
    - __Atomic Sliding Window Rate Limiter__: Protects sensitive auth and account gateways against brute-force/DDoS requests using Redis Sorted Sets (ZSET) grouped within atomic pipeline round-trips.
    - __Time-Bound Ephemeral Key Store__: Manages stateful lifecycle tracking for out-of-band security authentications.
- __Robust Identity Shield & Session Lifecycles__: Features a robust dual-token security topology (JWT-based Access & Refresh Token rotation) transported safely via encrypted headers and HttpOnly, SameSite=Strict browser cookies to systematically insulate the application against XSS and CSRF ambient request attacks.
- __Defensive Cryptography & Security Controls__: Enforces maximum security at the API gateway through memory-hard Argon2id password hashing resistant to GPU parallel cracking, utilizing cryptographic constant-time string matching (secrets.compare_digest) to neutralize side-channel timing attacks.
- __Server-Side Data Aggregation & Analytical Engines__: Minimizes API network overhead by offloading heavy arithmetic calculation onto the database engine. Leverages SQL data type casting and server-side mathematical aggregations (SUM, AVG, MIN, MAX, COUNT) to compile granular, date-bounded itemized financial metrics instantly.
- __Non-Blocking Out-of-Band (OOB) Communications__: Handles secure workflow verification and account recovery routines through Twilio SMS Gateway integration. To preserve zero-latency request processing times, communications are seamlessly offloaded to background execution worker pools using FastAPI BackgroundTasks.
- __Active Microservices Diagnostics & Telemetry__: Outfitted with specialized administrative health telemetry endpoints monitoring live service-level connectivity status across all standalone relational, cache, rate-limiting, and external notification networks independently.
