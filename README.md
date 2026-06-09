<p align="center">
  <img src="https://github.com/gokulv197-crypto/readme-images/blob/main/expense-tracker/b1d1906722b334d8674254682068c0b9_fgraphic1.png">
</p>

Expense Tracker is a high-performance, asynchronous RESTful API backend designed to securely manage, track, and analyze personal financial data. Built as a scalable expense analytics platform, the system implements a modern microservices-adjacent architecture featuring decoupled storage layers, write-through caching pipelines, defensive security guardrails, and event-driven out-of-band communication systems.

## Technical Highlights & System Architecture
- __Asynchronous Enterprise Stack:__ Engineered entirely with __FastAPI__ utilizing Python's `asyncio` ecosystem to maximize concurrent throughput. It features persistent storage mapped through __SQLAlchemy ORM__ to a __MySQL__ relational database, optimized with explicit composite indexing and foreign key cascade deletion integrity.
- __Decoupled Multi-Instance Memory Tier:__ Implements three isolated Redis data pools to prevent cross-contamination of infrastructure memory:
    - __High-Speed Cache Engine:__ Reduces relational database load by executing an eviction/write-through cache pattern for persistent user transactions.
    - __Atomic Sliding Window Rate Limiter:__ Protects sensitive auth and account gateways against brute-force/DDoS requests using Redis Sorted Sets (`ZSET`) grouped within atomic pipeline round-trips.
    - __Time-Bound Ephemeral Key Store:__ Manages stateful lifecycle tracking for out-of-band security authentications.
- __Robust Identity Shield & Session Lifecycles:__ Features a robust dual-token security topology (__JWT-based Access & Refresh Token rotation__) transported safely via encrypted headers and `HttpOnly`, `SameSite=Strict` browser cookies to systematically insulate the application against XSS and CSRF ambient request attacks.
- __Defensive Cryptography & Security Controls:__ Enforces maximum security at the API gateway through memory-hard __Argon2id__ password hashing resistant to GPU parallel cracking, utilizing cryptographic constant-time string matching (`secrets.compare_digest`) to neutralize side-channel timing attacks.
- __Server-Side Data Aggregation & Analytical Engines:__ Minimizes API network overhead by offloading heavy arithmetic calculation onto the database engine. Leverages SQL data type casting and server-side mathematical aggregations (`SUM`, `AVG`, `MIN`, `MAX`, `COUNT`) to compile granular, date-bounded itemized financial metrics instantly.
- __Non-Blocking Out-of-Band (OOB) Communications:__ Handles secure workflow verification and account recovery routines through __Twilio SMS Gateway__ integration. To preserve zero-latency request processing times, communications are seamlessly offloaded to background execution worker pools using FastAPI BackgroundTasks.
- __Active Microservices Diagnostics & Telemetry:__ Outfitted with specialized administrative health telemetry endpoints monitoring live service-level connectivity status across all standalone relational, cache, rate-limiting, and external notification networks independently.

# Local Setup
## Prerequisites
- Python 3.9+
- MySQL database
- Dockerized Redis
- Twilio Messaging Account

## Clone the Repository
git clone https://github.com/gokulv197-crypto/expense-tracker
<br>
cd expense-tracker

## Create a Virtual Environment
python -m venv <venv_name>
- __Linux / Mac__: <venv_name>/bin/activate
- __Windows__: <venv_name>\Scripts\activate

## Install Dependencies
pip install -r requirements.txt

## Environment Configuration
Create a `.env` file in the root directory:
- __DATABASE_URL__=mysql+pymysql://[user]:[password]@localhost:3306/<db_name>
- __SECRET_KEY__=<secret_key>
- __REDIS_CACHE_URL__=redis://localhost:6379/<db_number_0-15>
- __REDIS_RATE_LIMITER_URL__=redis://localhost:6379/<db_number_0-15>
- __REDIS_OTP_STORAGE_URL__=redis://localhost:6379/<db_number_0-15>
- __TWILIO_ACCOUNT_SID__=<twilio_account_sid>
- __TWILIO_AUTH_TOKEN__=<twilio_auth_token>
- __TWILIO_PHONE__=<twilio_phone>
- __ADMIN__=[username]
- __PASSWORD__=<admin_password>
- __PHONE_NUMBER__=+[COUNTRY CODE][MOBILE NUMBER]

__Note 1__: Remove `SSL/CA` certificate arguments from the `create_engine` call in `database.py` file.
<br>
__Note 2__: Set `secure=False` within the `response.delete_cookie` call in `crud.py` file and `response.set_cookie` call in `main.py` file to allow the browser to process cookies over a HTTP connection.

## Run the application
uvicorn app.main:app --reload
<br>
<br>
API will be available at: `http://localhost:8000`
<br>
Access the interactive Swagger documentation at: `http://localhost:8000/docs`
