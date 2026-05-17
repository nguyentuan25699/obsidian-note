| **Concept**       | **Keyword**            |
| ----------------- | ---------------------- |
| Azure Functions   | serverless compute     |
| Queue trigger     | message queue          |
| Blob trigger      | file upload            |
| Consumption plan  | pay per execution      |
| Premium plan      | no cold start          |
| Durable functions | workflow orchestration |

| **Scenario**           | **Service**         |
| ---------------------- | ------------------- |
| host web app           | App Service         |
| event-driven compute   | Azure Functions     |
| run container quickly  | Container Instances |
| orchestrate containers | AKS                 |
| full server control    | Virtual Machine     |

#  **1. Azure Functions Hosting Plans**

| **Plan**                     | **Đặc điểm**                                       | **Khi dùng**                        |
| ---------------------------- | -------------------------------------------------- | ----------------------------------- |
| Consumption                  | serverless, auto scale, pay per execution          | workload nhỏ, event-driven          |
| Premium                      | pre-warmed instance, **no cold start**, auto scale | API latency thấp                    |
| Dedicated (App Service plan) | chạy trên App Service plan                         | khi muốn share resource với web app |


| **Scenario**                           | **Đáp án**  |
| -------------------------------------- | ----------- |
| pay only when function runs            | Consumption |
| avoid cold start                       | Premium     |
| run function with existing App Service | Dedicated   |


# **2. Azure App Service Plans**
App Service **không phải hosting plan cho function**, mà là compute resource cho web apps.

| **Tier** | **Đặc điểm**     |
| -------- | ---------------- |
| Free     | testing          |
| Basic    | production nhỏ   |
| Standard | auto scale       |
| Premium  | high performance |
📌 AZ-204 thường hỏi:

> Multiple apps share the same App Service plan → **TRUE**

#  **3. Container Compute Options**
| **Service**         | **Dùng khi**         |
| ------------------- | -------------------- |
| Container Instances | chạy container nhanh |
| Container Apps      | microservices        |
| AKS                 | Kubernetes cluster   |
📌 Exam hay hỏi:

| **Scenario**                 | **Answer**          |
| ---------------------------- | ------------------- |
| run single container quickly | Container Instances |
| orchestrate many containers  | AKS                 |

# **4. Compute services overview (hay ra đề)**

| **Service**     | **Type**                |
| --------------- | ----------------------- |
| Virtual Machine | IaaS                    |
| App Service     | PaaS                    |
| Azure Functions | Serverless              |
| AKS             | Container orchestration |

# **5. Blob Storage Cheat Sheet (rất quan trọng)**
| **Scenario**          | **Answer**  |
| --------------------- | ----------- |
| store images/video    | Block Blob  |
| log append            | Append Blob |
| VM disk               | Page Blob   |
| temporary access      | SAS         |
| move old data cheaper | Lifecycle   |
| frequent access       | Hot         |
| rare access           | Cool        |
| long-term archive     | Archive     |

# 6. Microsoft identity platform

| **Scenario**                         | **Answer**       |
| ------------------------------------ | ---------------- |
| login with Azure AD                  | Entra ID         |
| register app                         | App registration |
| API authentication                   | OAuth            |
| access Azure resource without secret | Managed Identity |
| assign permissions                   | RBAC             |

# 7. Mesaging
Event Grid = something happened
Event Hub = data flowing
Service Bus = send message reliably

| **Thấy từ**                   | **Chọn**    |
| ----------------------------- | ----------- |
| trigger / event / blob upload | Event Grid  |
| telemetry / logs / streaming  | Event Hub   |
| queue / retry / delivery      | Service Bus |

# 8. Mornitoring
|**Keyword**|**Answer**|
|---|---|
|CPU / VM / resource|Azure Monitor|
|API / exception / app|App Insights|
|query / logs|Log Analytics|

# **Một bảng cực quan trọng cho AZ-204**

| **Situation**          | **Service**         |
| ---------------------- | ------------------- |
| Host web API           | App Service         |
| Event-driven code      | Azure Functions     |
| Process queue message  | Azure Functions     |
| Run container quickly  | Container Instances |
| Run Kubernetes cluster | AKS                 |

# **⚠️ 5 bẫy Microsoft hay dùng**

| **Bẫy**             | **Thực tế**           |
| ------------------- | --------------------- |
| Function = PaaS     | Function = Serverless |
| avoid cold start    | Premium plan          |
| cheap event compute | Consumption           |
| run container       | Container Instances   |
| web app hosting     | App Service           |

# **📌 Mẹo nhớ nhanh**
```
Web app → App Service
Event code → Functions
Container → Container Instances
Cluster → AKS
```




____
# AZ-204 – Complete System Note (Theory + Exam Patterns)

---

# 1. COMPUTE

## Azure App Service

### What
- PaaS để host web app/API
- Không cần quản lý server

### Key Features
- Deployment Slots → deploy không downtime
- Auto-scale → scale theo load
- Built-in authentication

### Scaling
- Scale up → tăng CPU/RAM
- Scale out → tăng instance

---

### WHEN TO USE
- Host REST API
- Host frontend (React, Angular)
- Web app production

---

### EXAM PATTERN

❓ "Deploy without downtime"  
→ Deployment Slots

❓ "Increase performance under load"  
→ Scale out

❓ "Need managed hosting"  
→ App Service

---

## Azure Functions

### What
- Serverless compute
- Chạy theo event

### Hosting Plans
- Consumption → rẻ, có cold start
- Premium → không cold start
- Dedicated → App Service plan

---

### WHEN TO USE
- Event-driven logic
- Background jobs
- Lightweight API

---

### EXAM PATTERN

❓ "Event-driven" → Functions  
❓ "Avoid cold start" → Premium  
❓ "Pay per execution" → Consumption  

---

# 2. STORAGE

## Blob Storage

### What
- Object storage cho file

---

### Blob Types
- Block Blob → file/image
- Append Blob → log
- Page Blob → VM disk

---

### Access Control
- RBAC → long-term access
- SAS → temporary access

---

### Lifecycle
- move data → Hot → Cool → Archive
- delete automatically

---

### WHEN TO USE
- Store file
- Static website hosting
- Media storage

---

### EXAM PATTERN

❓ "Temporary access to file" → SAS  
❓ "Store logs" → Append Blob  
❓ "Reduce cost over time" → Lifecycle  

---

# 3. COSMOS DB

## What
- NoSQL distributed database
- Low latency

---

## Partition Key (VERY IMPORTANT)

### What
- Chia data ra nhiều partition

### WHY
- quyết định performance

---

### EXAM PATTERN

❓ "Improve performance" → chọn partition key tốt  
❓ "Even distribution" → partition key  

---

## RU/s

- Throughput unit
- Scale performance

---

## Consistency Levels

### Overview

| Level | Meaning |
|------|--------|
Strong | strict consistency |
Session | default |
Eventual | fastest |
Bounded staleness | delay limited |
Consistent prefix | order guaranteed |

---

### WHEN TO USE

- Strong → banking / critical data  
- Session → app thông thường  
- Eventual → performance priority  

---

### EXAM PATTERN (VERY IMPORTANT)

❓ "Maximize throughput / minimize latency"  
→ Eventual  

❓ "Default consistency"  
→ Session  

❓ "Strict consistency required"  
→ Strong  

---

# 4. AUTHENTICATION

## Microsoft Entra ID

- Identity provider
- User login

---

## Token Types

| Token | Use |
|------|-----|
Access token | call API |
ID token | user info |
Refresh token | renew |

---

## Managed Identity

### What
- Azure service tự authenticate

### WHY
- không cần lưu secret

---

### EXAM PATTERN

❓ "Access Azure service securely"  
→ Managed Identity  

❓ "Avoid storing credentials"  
→ Managed Identity  

---

# 5. KEY VAULT

## What
- Store sensitive data

---

## Types

- Secret → password
- Key → encryption
- Certificate → SSL

---

### EXAM PATTERN

❓ "Store password securely" → Secret  
❓ "Encrypt data" → Key  
❓ "Use with App Service" → Managed Identity + Key Vault  

---

# 6. MESSAGING (CRITICAL)

---

## Azure Service Bus

### What
- Enterprise messaging

### Features
- Queue (point-to-point)
- Topic (pub/sub)
- Retry
- Dead-letter

---

### WHEN TO USE
- Reliable messaging
- Microservices communication

---

### EXAM PATTERN

❓ "Queue between services" → Service Bus  
❓ "Guaranteed delivery" → Service Bus  

---

## Event Grid

### What
- Event routing

---

### WHEN TO USE
- Trigger action
- Blob upload event

---

### EXAM PATTERN

❓ "Trigger when event happens" → Event Grid  
❓ "Blob upload trigger" → Event Grid  

---

## Event Hub

### What
- Streaming platform

---

### WHEN TO USE
- Telemetry
- IoT data
- Logs

---

### EXAM PATTERN

❓ "High throughput / streaming" → Event Hub  
❓ "Real-time analytics" → Event Hub  

---

# 7. MONITORING

---

## Azure Monitor

### What
- Monitor infrastructure

---

### Data
- Metrics
- Logs

---

### EXAM PATTERN

❓ "CPU / memory monitoring" → Azure Monitor  
❓ "Resource metrics" → Azure Monitor  

---

## Application Insights

### What
- Monitor application

---

### Track
- Requests
- Exceptions
- Performance

---

### EXAM PATTERN

❓ "Track API performance" → App Insights  
❓ "Track errors" → App Insights  

---

## Log Analytics

### What
- Query logs

---

### EXAM PATTERN

❓ "Query logs" → Log Analytics  
❓ "Analyze log data" → Log Analytics  

---

# 8. API MANAGEMENT

### What
- API Gateway

---

### Features
- Rate limiting
- Authentication
- Logging

---

### EXAM PATTERN

❓ "Manage API centrally" → API Management  
❓ "Apply rate limit" → API Management  

---

# 9. REDIS CACHE

### What
- In-memory cache

---

### WHY
- improve performance

---

### EXAM PATTERN

❓ "Reduce latency" → Redis  
❓ "Cache data" → Redis  

---

# 10. FINAL EXAM STRATEGY

---

## STEP 1
Scan keyword (không đọc hết câu)

---

## STEP 2
Map to service

---

## STEP 3
Eliminate wrong answers

---

## CORE MAPPING

trigger → Event Grid  
stream → Event Hub  
queue → Service Bus  

app → App Insights  
resource → Azure Monitor  
query → Log Analytics  

fastest → Eventual  
default → Session  
strict → Strong  

---