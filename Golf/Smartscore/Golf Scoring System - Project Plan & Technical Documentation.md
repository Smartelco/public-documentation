# 🏌️ Golf Scoring System - Project Plan & Technical Documentation

**Project Name:** Integrated Golf Scoring & Membership Platform  
**Target Market:** Golf Courses in Indonesia  
**Version:** 1.0 - MVP Proposal  
**Date:** October 2025  
**Prepared for:** Business & Technical Stakeholders

---

## 📋 Table of Contents

1. [Executive Summary](#executive-summary)
2. [Business Overview](#business-overview)
3. [System Architecture](#system-architecture)
4. [Database Design](#database-design)
5. [User Flows & Features](#user-flows--features)
6. [Technical Stack Recommendations](#technical-stack-recommendations)
7. [MVP Development Phases](#mvp-development-phases)
8. [Infrastructure Requirements](#infrastructure-requirements)
9. [Implementation Timeline](#implementation-timeline)
10. [Budget Estimation](#budget-estimation)
11. [Risk Management & Mitigation](#risk-management--mitigation)

---

## 🎯 Executive Summary

### Problem Statement

Golf courses di Indonesia saat ini menghadapi tantangan dalam pengelolaan scoring dan membership:
- ❌ Manual scorekeeping yang rawan error
- ❌ Tidak ada real-time leaderboard untuk tournament
- ❌ Sulit tracking performance history member
- ❌ Koordinasi antar Golfer, Caddy, dan Marshall tidak efisien
- ❌ Data terfragmentasi antara sistem scoring dan membership

### Proposed Solution

**Integrated Golf Scoring & Membership Platform** - sistem on-premise yang menyediakan:

✅ **Real-time scoring** dengan validasi Marshall  
✅ **Integrated membership tracking** dengan handicap management  
✅ **Live tournament leaderboard** yang dapat dilihat semua pemain  
✅ **Multi-role access** (Golfer, Caddy, Marshall, Admin, Tournament Organizer)  
✅ **Mobile-first approach** untuk kemudahan penggunaan di lapangan  
✅ **Comprehensive analytics** untuk management decision

### Key Benefits by Stakeholder

| Stakeholder | Key Benefits |
|------------|--------------|
| **Golf Course Management** | • Digitalisasi operasional<br>• Data analytics untuk business decision<br>• Meningkatkan member satisfaction<br>• Professional tournament hosting |
| **Golfer** | • Real-time score tracking<br>• Performance history & statistics<br>• Easy tournament participation<br>• Handicap tracking otomatis |
| **Tournament Organizer** | • Automated leaderboard updates<br>• Simplified tournament management<br>• Professional presentation<br>• Reduce manual work 80% |
| **Admin Staff** | • Centralized member management<br>• Automated reporting<br>• Easy user role management<br>• Audit trail untuk semua transaksi |
| **Caddy** | • Simplified score recording<br>• Player statistics access<br>• Better service capability |

### Success Metrics (MVP Target)

- **User Adoption:** 80% active members dalam 3 bulan
- **Score Accuracy:** 95% validasi tanpa error
- **Real-time Performance:** Leaderboard update < 3 detik
- **System Uptime:** 99.5% availability
- **User Satisfaction:** NPS Score > 8.0

---

## 💼 Business Overview

### Target Market

**Primary Target:** 1-2 Golf Courses untuk MVP Phase

**Target Segments:**
1. **Premium Golf Courses** dengan 200-500+ members
2. **Tournament-Active Courses** yang sering host kompetisi
3. **Technology-Forward Management** yang open untuk digitalisasi

### Market Opportunity

**Indonesia Golf Market Facts:**
- 150+ golf courses di Indonesia
- Growing middle-upper class dengan disposable income
- Increasing tournament activity post-pandemic
- Digital transformation trend di hospitality sector

**Pain Points yang Kami Solve:**
1. **Operational Efficiency:** Reduce manual work 70-80%
2. **Member Experience:** Modern, seamless scoring experience
3. **Data Insights:** Analytics yang tidak tersedia di sistem manual
4. **Tournament Capability:** Professional tournament management

### Competitive Advantage

| Feature | Manual System | Competitor Apps | Our Solution |
|---------|--------------|-----------------|--------------|
| **On-Premise** | ✅ | ❌ Cloud only | ✅ Customizable |
| **Local Support** | ✅ | ❌ Limited | ✅ Full support |
| **Integration** | ❌ | ⚠️ Partial | ✅ Full integration |
| **Indonesia Focus** | ✅ | ❌ Global | ✅ Local needs |
| **Cost Structure** | Low | $$$$ subscription | $$ one-time + maintenance |
| **Customization** | ❌ | ❌ | ✅ Flexible |

### Revenue Model (Future Consideration)

1. **License Model:** Per golf course license fee
2. **Implementation Fee:** Setup & training services
3. **Maintenance Contract:** Annual support & updates
4. **Additional Modules:** Advanced analytics, integrations

---

## 🏗️ System Architecture

### High-Level Architecture Overview

```mermaid
graph TB
    subgraph "Client Layer"
        A[Mobile App - Golfer]
        B[Mobile App - Caddy]
        C[Web Dashboard - Admin]
        D[Web Dashboard - Tournament Organizer]
        E[Tablet - Marshall]
    end
    
    subgraph "API Gateway Layer"
        F[Load Balancer]
        G[API Gateway<br/>Authentication & Rate Limiting]
    end
    
    subgraph "Application Layer - On-Premise Server"
        H[Auth Service<br/>JWT/Session]
        I[Scoring Service<br/>Real-time Processing]
        J[Tournament Service]
        K[Membership Service]
        L[Notification Service<br/>WebSocket/SSE]
        M[Leaderboard Service<br/>Real-time Updates]
    end
    
    subgraph "Data Layer"
        N[(PostgreSQL<br/>Primary DB)]
        O[(Redis Cache<br/>Sessions & Leaderboards)]
        P[File Storage<br/>Profile Photos, Documents]
    end
    
    subgraph "Background Jobs"
        Q[Task Queue<br/>Handicap Calculation]
        R[Scheduled Jobs<br/>Stats Aggregation]
    end
    
    A --> F
    B --> F
    C --> F
    D --> F
    E --> F
    
    F --> G
    
    G --> H
    G --> I
    G --> J
    G --> K
    G --> L
    G --> M
    
    H --> N
    I --> N
    I --> O
    J --> N
    K --> N
    L --> O
    M --> O
    M --> N
    
    I --> Q
    M --> Q
    Q --> R
    
    H --> P
    
    style A fill:#e1f5ff
    style B fill:#e1f5ff
    style C fill:#fff4e1
    style D fill:#fff4e1
    style E fill:#e1ffe1
```

### Architecture Components Explained

#### 1. Client Layer
- **Mobile Apps (React Native/Flutter):** For golfers and caddies to enter scores in real-time
- **Web Dashboard (React/Vue.js):** For admin and tournament organizer management
- **Tablet Interface:** For marshalls to validate scores on the course

#### 2. API Gateway Layer
- **Load Balancer:** NGINX for distributing traffic
- **API Gateway:** Centralized authentication, rate limiting, request routing

#### 3. Application Layer (Microservices)
- **Auth Service:** User authentication, JWT token management, role-based access
- **Scoring Service:** Core scoring logic, real-time score processing
- **Tournament Service:** Tournament setup, participant management, results
- **Membership Service:** Member profiles, handicap tracking, history
- **Notification Service:** WebSocket/SSE for real-time updates
- **Leaderboard Service:** Real-time ranking calculations and caching

#### 4. Data Layer
- **PostgreSQL:** Primary relational database for all persistent data
- **Redis:** In-memory cache for sessions, leaderboards, real-time data
- **File Storage:** Local storage for user uploads (photos, documents)

#### 5. Background Jobs
- **Task Queue (Bull/Celery):** Async processing for heavy computations
- **Scheduled Jobs:** Daily handicap recalculation, statistics aggregation

### Security Architecture

```mermaid
graph LR
    A[User Login] --> B{Authentication}
    B -->|Valid| C[JWT Token Issued]
    B -->|Invalid| D[Login Failed]
    
    C --> E[API Request with Token]
    E --> F{Token Validation}
    F -->|Valid| G{Role Check}
    F -->|Invalid| H[401 Unauthorized]
    
    G -->|Authorized| I[Process Request]
    G -->|Not Authorized| J[403 Forbidden]
    
    I --> K[Audit Log]
    K --> L[Response]
    
    style B fill:#FFE5B4
    style F fill:#FFE5B4
    style G fill:#FFE5B4
```

**Security Features:**
- ✅ JWT-based authentication with refresh tokens
- ✅ Role-based access control (RBAC)
- ✅ Input validation & sanitization
- ✅ SQL injection prevention (parameterized queries)
- ✅ XSS protection
- ✅ Rate limiting to prevent abuse
- ✅ Audit logging for all critical operations
- ✅ Encrypted password storage (bcrypt)
- ✅ HTTPS/TLS for all communications

---

## 🗄️ Database Design

### Entity Relationship Diagram (ERD)

**Access full interactive ERD at:** <https://dbdocs.io/aditira.jamhuri/Smart-Score-Golf?view=relationships>

**DBML Schema:**

![](assets/Smart-Score-Golf-ERD.png)

### Key Database Tables Explained

#### Core Tables

**1. users**
- Central user table untuk semua roles
- Single table untuk golfer, caddy, marshall, admin, tournament_organizer
- Status field untuk manage active/inactive users

**2. golf_courses**
- Master data lapangan golf
- Menyimpan course rating & slope rating untuk handicap calculation
- Support multiple courses dalam satu installation

**3. holes**
- Detail setiap hole di course
- Par value, distance, handicap index
- Foreign key ke golf_courses

**4. memberships**
- Link antara user dan golf course
- Menyimpan handicap index member
- Support multiple membership types (regular, premium, corporate)

**5. rounds**
- Setiap sesi bermain golf
- Bisa tournament round atau casual round
- Track player, caddy, start/end time, statistics

**6. scores**
- Detail score per hole per round
- Menyimpan strokes, putts, fairway hit, GIR
- recorded_by untuk audit trail

**7. tournaments**
- Master tournament data
- Support multiple tournament types (stroke play, match play, stableford)
- Status tracking (upcoming, ongoing, completed, cancelled)

**8. leaderboards**
- Real-time tournament rankings
- Cached calculation untuk performance
- Updated setiap ada score submission

#### Supporting Tables

**9. tournament_participants**
- Many-to-many relationship antara tournaments dan users
- Menyimpan handicap snapshot saat registration

**10. score_history**
- Audit trail untuk score modifications
- Track who changed what and when
- Important untuk tournament integrity

**11. notifications**
- Push notification management
- Support multiple notification types
- Read/unread tracking

### Database Optimization Strategy

**Indexing:**
- Composite indexes pada frequently queried combinations
- Unique constraints untuk data integrity
- Foreign key indexes untuk join performance

**Caching Strategy:**
- Redis cache untuk leaderboards (TTL: 5 minutes)
- Session cache (TTL: 24 hours)
- Query result cache untuk static data (course info, holes)

**Partitioning (Future):**
- Partition `scores` table by date (monthly)
- Partition `rounds` table by date
- Archive old tournaments (> 1 year)

---

## 🔄 User Flows & Features

### 1. Golfer Playing Round Flow

```mermaid
sequenceDiagram
    participant G as Golfer
    participant A as Mobile App
    participant API as API Gateway
    participant SS as Scoring Service
    participant LS as Leaderboard Service
    participant DB as Database
    participant WS as WebSocket
    
    G->>A: Login & Select Course
    A->>API: Authenticate
    API->>DB: Verify Credentials
    DB-->>API: User Data + Membership
    API-->>A: JWT Token
    
    G->>A: Start New Round
    A->>API: POST /rounds/create
    API->>SS: Create Round
    SS->>DB: Insert Round Record
    DB-->>SS: Round ID
    SS-->>A: Round Created
    
    G->>A: Submit Score for Hole 1
    A->>API: POST /scores/submit
    API->>SS: Process Score
    SS->>DB: Save Score
    
    alt Tournament Round
        SS->>LS: Update Leaderboard
        LS->>DB: Calculate Position
        LS->>WS: Broadcast Update
        WS-->>A: Real-time Leaderboard
    end
    
    SS-->>A: Score Confirmed
    
    loop For Each Hole
        G->>A: Submit Next Hole Score
        A->>API: POST /scores/submit
        API->>SS: Process Score
        SS->>DB: Save Score
        SS->>LS: Update Stats
        LS->>WS: Broadcast
    end
    
    G->>A: Complete Round
    A->>API: POST /rounds/complete
    API->>SS: Finalize Round
    SS->>DB: Update Round Status
    SS->>LS: Final Calculations
    LS-->>A: Final Scorecard
```

**Key Features:**
- ✅ Quick round start dengan preset course selection
- ✅ Hole-by-hole score entry dengan intuitive UI
- ✅ Real-time sync ke server (offline capability future phase)
- ✅ View current stats (total score, putts, fairways hit)
- ✅ Live leaderboard untuk tournament rounds
- ✅ Scorecard sharing capability

### 2. Tournament Organizer Setup Flow

```mermaid
flowchart TD
    A[Login as Tournament Organizer] --> B[Access Tournament Dashboard]
    B --> C[Create New Tournament]
    C --> D[Fill Tournament Details]
    D --> E{Select Tournament Type}
    
    E -->|Stroke Play| F[Configure Stroke Play Rules]
    E -->|Match Play| G[Configure Match Play]
    E -->|Stableford| H[Configure Stableford Points]
    
    F --> I[Set Participant Limit]
    G --> I
    H --> I
    
    I --> J[Set Registration Deadline]
    J --> K[Publish Tournament]
    K --> L[Monitor Registrations]
    
    L --> M{Tournament Day}
    M --> N[Start Tournament]
    N --> O[Monitor Live Scoring]
    O --> P[View Real-time Leaderboard]
    
    P --> Q{Scoring Issues?}
    Q -->|Yes| R[Review & Adjust Scores]
    Q -->|No| S[Continue Monitoring]
    
    R --> T[Add Score Adjustment Note]
    T --> S
    S --> U{Tournament Complete?}
    U -->|No| O
    U -->|Yes| V[Finalize Results]
    V --> W[Generate Tournament Report]
```

**Key Features:**
- ✅ Wizard-based tournament creation
- ✅ Multiple tournament format support
- ✅ Participant management (invite, approve, waitlist)
- ✅ Live monitoring dashboard dengan real-time updates
- ✅ Score adjustment capability dengan audit trail
- ✅ Automated result calculation
- ✅ Report generation (PDF/Excel export)

### 3. Admin Dashboard Flow

```mermaid
flowchart TD
    A[Admin Login] --> B[Dashboard Overview]
    B --> C{Select Action}
    
    C --> D[User Management]
    C --> E[Course Management]
    C --> F[Membership Management]
    C --> G[System Settings]
    
    D --> D1[Add/Edit Users]
    D --> D2[Assign Roles]
    D --> D3[View User Activity]
    
    E --> E1[Manage Course Details]
    E --> E2[Configure Holes]
    E --> E3[Update Par & Ratings]
    
    F --> F1[Approve Memberships]
    F --> F2[Track Membership Status]
    F --> F3[Generate Reports]
    
    G --> G1[System Configuration]
    G --> G2[Backup Management]
    G --> G3[Audit Logs]
```

**Key Features:**
- ✅ Centralized user management
- ✅ Role assignment dan permission control
- ✅ Course configuration (holes, par, ratings)
- ✅ Membership approval workflow
- ✅ System health monitoring
- ✅ Audit log viewer
- ✅ Database backup management

### 4. Real-time Scoring with Marshall Validation Flow

```mermaid
sequenceDiagram
    participant P as Player/Caddy
    participant M as Marshall (Validator)
    participant App as Mobile App
    participant API as API
    participant Cache as Redis Cache
    participant DB as PostgreSQL
    participant WS as WebSocket Server
    participant L as Live Viewers
    
    P->>App: Enter Score for Hole
    App->>API: Submit Score (Pending)
    API->>DB: Save Score (status: pending)
    API->>Cache: Update Round Cache
    API-->>App: Score Submitted
    
    Note over API,M: Score Validation Flow
    API->>M: Notify for Validation
    M->>App: Review Score
    
    alt Score Approved
        M->>API: Approve Score
        API->>DB: Update Score (status: approved)
        API->>Cache: Update Leaderboard Cache
        API->>WS: Trigger Update
        WS-->>L: Broadcast Score Update
        WS-->>App: Confirm to Player
    else Score Rejected
        M->>API: Reject with Reason
        API->>DB: Update Score (status: rejected)
        API->>P: Request Re-entry
    end
    
    Note over Cache,L: Leaderboard Calculation
    Cache->>Cache: Calculate Position
    Cache->>WS: Send Updated Rankings
    WS-->>L: Real-time Leaderboard
```

**Key Features:**
- ✅ Instant score submission
- ✅ Marshall validation untuk tournament integrity
- ✅ Real-time leaderboard updates
- ✅ Score correction workflow
- ✅ Audit trail untuk semua perubahan
- ✅ WebSocket untuk push updates

### 5. Complete Feature List by Role

#### Golfer Features
| Feature | Priority | Description |
|---------|----------|-------------|
| Profile Management | P0 | Edit profile, view handicap, statistics |
| Start Round | P0 | Quick start casual atau tournament round |
| Score Entry | P0 | Input strokes, putts, fairway hit, GIR |
| View Leaderboard | P0 | Live tournament standings |
| Round History | P1 | View past rounds, statistics, trends |
| Score Sharing | P2 | Share scorecard via social media |
| Performance Analytics | P2 | Charts, graphs, handicap trends |

#### Caddy Features
| Feature | Priority | Description |
|---------|----------|-------------|
| Score Entry for Player | P0 | Input scores on behalf of golfer |
| View Player Stats | P1 | Quick access to player's history |
| Multiple Player Support | P2 | Switch between players easily |

#### Marshall Features
| Feature | Priority | Description |
|---------|----------|-------------|
| Score Validation Queue | P0 | Review pending scores |
| Approve/Reject Scores | P0 | Validate accuracy with notes |
| Live Monitoring | P1 | See all active rounds on course |
| Issue Reporting | P2 | Report pace of play, issues |

#### Tournament Organizer Features
| Feature | Priority | Description |
|---------|----------|-------------|
| Create Tournament | P0 | Setup tournament details, rules |
| Participant Management | P0 | Invite, approve, organize players |
| Live Dashboard | P0 | Real-time monitoring semua rounds |
| Leaderboard Management | P0 | View, adjust, finalize standings |
| Score Adjustment | P1 | Correct errors dengan audit trail |
| Report Generation | P1 | PDF/Excel tournament results |
| Tournament Templates | P2 | Reusable tournament configs |

#### Admin Features
| Feature | Priority | Description |
|---------|----------|-------------|
| User Management | P0 | CRUD operations untuk users |
| Role Assignment | P0 | Assign roles, manage permissions |
| Course Configuration | P0 | Setup course details, holes |
| Membership Management | P0 | Approve, track memberships |
| System Settings | P1 | Configure system parameters |
| Audit Logs | P1 | View system activity logs |
| Backup/Restore | P1 | Database backup management |
| Analytics Dashboard | P2 | Business intelligence reports |

---

## 💻 Technical Stack Recommendations

### On-Premise Infrastructure Stack

```mermaid
graph TB
    subgraph "Client Applications"
        A1[Mobile App<br/>React Native/Flutter]
        A2[Web Dashboard<br/>React/Vue.js]
    end
    
    subgraph "Application Server"
        B1[Backend API<br/>Node.js/Python]
        B2[WebSocket Server<br/>Socket.io/uWS]
        B3[Task Queue<br/>Bull/Celery]
    end
    
    subgraph "Data Services"
        C1[(PostgreSQL 15+<br/>Primary Database)]
        C2[(Redis 7+<br/>Cache & Queue)]
        C3[File Storage<br/>MinIO/Local FS]
    end
    
    subgraph "Infrastructure"
        D1[NGINX<br/>Load Balancer]
        D2[Docker Containers]
        D3[Monitoring<br/>Prometheus+Grafana]
    end
    
    A1 --> D1
    A2 --> D1
    D1 --> B1
    D1 --> B2
    
    B1 --> C1
    B1 --> C2
    B1 --> C3
    B2 --> C2
    B3 --> C1
    B3 --> C2
    
    D2 -.-> B1
    D2 -.-> B2
    D2 -.-> B3
    D2 -.-> C1
    D2 -.-> C2
    
    D3 -.-> D2
```

### Recommended Technology Stack

#### Frontend Stack

**Mobile Application:**
```
Option 1 (Recommended): React Native
├── State Management: Redux Toolkit / Zustand
├── API Client: Axios / React Query
├── UI Components: React Native Paper / Native Base
├── Navigation: React Navigation
├── Real-time: Socket.io-client
└── Charts: Victory Native / React Native Chart Kit

Option 2: Flutter
├── State Management: Riverpod / Bloc
├── API Client: Dio
├── UI: Material Design / Cupertino
├── Navigation: GoRouter
├── Real-time: socket_io_client
└── Charts: FL Chart
```

**Web Dashboard:**
```
Framework: React 18+ / Vue 3+
├── UI Library: Ant Design / Material-UI / Tailwind CSS
├── State Management: Redux Toolkit / Pinia (Vue)
├── API Client: Axios / React Query
├── Real-time: Socket.io-client
├── Charts: Recharts / Chart.js / Apache ECharts
├── Tables: TanStack Table (React Table v8)
├── Forms: React Hook Form / Formik
└── Build Tool: Vite / Next.js
```

#### Backend Stack

**Option 1: Node.js (Recommended untuk MVP)**
```
Runtime: Node.js 20 LTS
├── Framework: Express.js / Fastify / NestJS
├── ORM: Prisma / TypeORM / Sequelize
├── Validation: Joi / Zod
├── Authentication: Passport.js / jsonwebtoken
├── WebSocket: Socket.io / ws
├── Task Queue: Bull / BullMQ
├── Testing: Jest / Supertest
├── Documentation: Swagger / OpenAPI
└── Language: TypeScript
```

**Option 2: Python**
```
Runtime: Python 3.11+
├── Framework: FastAPI / Django REST Framework
├── ORM: SQLAlchemy / Django ORM
├── Validation: Pydantic
├── Authentication: PyJWT / Django Auth
├── WebSocket: FastAPI WebSocket / Channels
├── Task Queue: Celery + Redis
├── Testing: Pytest
└── Documentation: FastAPI auto-docs / drf-spectacular
```

#### Database & Caching

**Primary Database:**
```
PostgreSQL 15+
├── Connection Pool: PgBouncer
├── Backup: pg_dump + cron jobs
├── Replication: Streaming Replication (future)
└── Extensions: pg_trgm (text search), pgcrypto
```

**Caching Layer:**
```
Redis 7+
├── Use Cases: 
│   ├── Session storage
│   ├── Leaderboard cache
│   ├── Real-time data buffer
│   └── Task queue backend
├── Persistence: RDB + AOF
└── Cluster: Single instance for MVP, Redis Cluster future
```

**File Storage:**
```
Option 1: Local File System (MVP)
└── Structure: /uploads/{user_id}/{type}/{filename}

Option 2: MinIO (Recommended future)
└── S3-compatible object storage for scalability
```

#### Infrastructure & DevOps

**Containerization:**
```
Docker + Docker Compose
├── Application containers
├── Database containers
├── Redis container
├── NGINX container
└── Volume mounts for persistence
```

**Web Server & Load Balancer:**
```
NGINX
├── Reverse proxy
├── Load balancing (future multi-instance)
├── SSL/TLS termination
├── Static file serving
└── WebSocket proxy
```

**Monitoring & Logging:**
```
Monitoring Stack:
├── Prometheus: Metrics collection
├── Grafana: Visualization dashboards
├── Node Exporter: System metrics
└── cAdvisor: Container metrics

Logging Stack:
├── Winston / Pino: Application logging
├── Logrotate: Log rotation
└── Optional: ELK Stack (Elasticsearch, Logstash, Kibana)
```

**Backup Strategy:**
```
Database Backup:
├── Daily full backup (pg_dump)
├── WAL archiving for point-in-time recovery
├── Retention: 30 days
└── Automated via cron jobs

Application Backup:
├── Weekly full server snapshot
├── Daily incremental file backups
└── Off-site backup recommended
```

### Why This Stack?

| Component | Reasoning |
|-----------|-----------|
| **React Native** | Single codebase untuk iOS & Android, large community, mature ecosystem |
| **Node.js + TypeScript** | JavaScript full-stack, excellent async I/O untuk real-time, type safety |
| **PostgreSQL** | Robust RDBMS, excellent JSON support, proven reliability, free |
| **Redis** | Best-in-class caching, pub/sub untuk real-time, task queue backend |
| **Docker** | Easy deployment, consistent environments, simplified scaling |
| **NGINX** | Industry standard, high performance, easy SSL setup |

### Development Tools

```
Version Control: Git + GitHub/GitLab
IDE: VS Code / WebStorm / IntelliJ
API Testing: Postman / Insomnia
Database Client: DBeaver / pgAdmin
Container Management: Docker Desktop / Portainer
CI/CD: GitHub Actions / GitLab CI (future)
```

---

## 🚀 MVP Development Phases

### Phase 1: Core MVP (Month 1-2) - CRITICAL

```mermaid
gantt
    title Phase 1 - Core MVP Development
    dateFormat  YYYY-MM-DD
    section Backend
    Database Setup & Schema      :2025-11-01, 3d
    Auth Service Implementation  :2025-11-04, 5d
    Course & Hole Management API :2025-11-09, 4d
    Scoring Service Core         :2025-11-13, 7d
    Basic Leaderboard Logic      :2025-11-20, 4d
    section Frontend
    Mobile App Setup             :2025-11-01, 3d
    Login & Profile Screens      :2025-11-04, 5d
    Round Start Flow             :2025-11-09, 4d
    Score Entry Interface        :2025-11-13, 7d
    Basic Leaderboard View       :2025-11-20, 4d
    section Testing
    Integration Testing          :2025-11-24, 5d
    User Acceptance Testing      :2025-11-29, 3d
```

**Deliverables:**

✅ **Backend:**
- User authentication & authorization (JWT)
- Course and hole management
- Round creation and management
- Score submission and retrieval
- Basic leaderboard calculation
- RESTful API documentation

✅ **Mobile App:**
- User login/logout
- Profile view
- Course selection
- Round start workflow
- Hole-by-hole score entry
- View current round statistics
- Basic leaderboard view

✅ **Infrastructure:**
- PostgreSQL database setup
- Redis cache setup
- Docker containerization
- NGINX reverse proxy
- Basic monitoring

**Success Criteria:**
- ✅ Golfer dapat login dan mulai round
- ✅ Score entry working untuk 18 holes
- ✅ Leaderboard update dalam < 5 detik
- ✅ System stable untuk 10 concurrent users

---

### Phase 2: Enhanced Features (Month 3)

```mermaid
gantt
    title Phase 2 - Enhanced Features
    dateFormat  YYYY-MM-DD
    section Backend
    Membership Service           :2025-12-01, 5d
    WebSocket Implementation     :2025-12-06, 7d
    Tournament Service Basic     :2025-12-13, 7d
    Marshall Validation Flow     :2025-12-20, 5d
    section Frontend
    Membership Management UI     :2025-12-01, 5d
    Real-time Updates (WS)       :2025-12-06, 7d
    Tournament Creation Flow     :2025-12-13, 7d
    Marshall Validation App      :2025-12-20, 5d
    section Testing
    Real-time Testing            :2025-12-25, 3d
    Load Testing                 :2025-12-28, 2d
```

**Deliverables:**

✅ **Backend:**
- Membership management service
- WebSocket server for real-time updates
- Tournament creation and management
- Marshall validation workflow
- Real-time leaderboard updates

✅ **Frontend:**
- Membership registration flow
- Real-time score updates via WebSocket
- Tournament organizer dashboard
- Marshall validation interface
- Enhanced leaderboard with live updates

✅ **Infrastructure:**
- WebSocket load balancing
- Redis pub/sub configuration
- Performance optimization

**Success Criteria:**
- ✅ Real-time updates < 3 second latency
- ✅ Support 50+ concurrent users
- ✅ Tournament creation and management working
- ✅ Marshall validation workflow complete

---

### Phase 3: Advanced Features (Month 4-5)

```mermaid
gantt
    title Phase 3 - Advanced Features
    dateFormat  YYYY-MM-DD
    section Backend
    Handicap Calculation Engine  :2026-01-01, 7d
    Statistics Aggregation       :2026-01-08, 7d
    Advanced Tournament Types    :2026-01-15, 7d
    Notification Service         :2026-01-22, 5d
    Reporting Engine             :2026-01-27, 6d
    section Frontend
    Statistics Dashboard         :2026-01-01, 7d
    Performance Analytics        :2026-01-08, 7d
    Advanced Tournament UI       :2026-01-15, 7d
    Push Notifications           :2026-01-22, 5d
    Report Generation UI         :2026-01-27, 6d
    section Polish
    UI/UX Refinement             :2026-02-02, 5d
    Performance Optimization     :2026-02-07, 5d
    Documentation                :2026-02-12, 3d
```

**Deliverables:**

✅ **Backend:**
- Handicap calculation (USGA system)
- Statistics aggregation (daily, weekly, monthly)
- Match play & Stableford tournament support
- Push notification service
- Report generation (PDF, Excel)

✅ **Frontend:**
- Comprehensive statistics dashboard
- Performance analytics charts
- Advanced tournament management
- Push notification handling
- Report viewer and download

✅ **Polish:**
- UI/UX improvements based on feedback
- Performance optimization
- Complete user documentation
- Admin training materials

**Success Criteria:**
- ✅ Accurate handicap calculation
- ✅ Rich analytics available
- ✅ Multiple tournament formats supported
- ✅ System ready for production launch

---

### Feature Priority Matrix

```mermaid
graph LR
    subgraph "Must Have - Phase 1"
        A1[User Auth]
        A2[Score Entry]
        A3[Round Management]
        A4[Basic Leaderboard]
        A5[Course Setup]
    end
    
    subgraph "Should Have - Phase 2"
        B1[Membership System]
        B2[Real-time Updates]
        B3[Tournament Basic]
        B4[Marshall Validation]
        B5[Mobile App Polish]
    end
    
    subgraph "Nice to Have - Phase 3"
        C1[Handicap Calc]
        C2[Statistics]
        C3[Advanced Tournaments]
        C4[Notifications]
        C5[Reports]
    end
    
    subgraph "Future Enhancements"
        D1[Offline Mode]
        D2[AI Insights]
        D3[Social Features]
        D4[Integrations]
    end
    
    A1 --> A2
    A2 --> A3
    A3 --> A4
    A4 --> A5
    
    A5 --> B1
    B1 --> B2
    B2 --> B3
    B3 --> B4
    B4 --> B5
    
    B5 --> C1
    C1 --> C2
    C2 --> C3
    C3 --> C4
    C4 --> C5
    
    C5 -.-> D1
    C5 -.-> D2
    C5 -.-> D3
    C5 -.-> D4
    
    style A1 fill:#4CAF50
    style A2 fill:#4CAF50
    style A3 fill:#4CAF50
    style A4 fill:#4CAF50
    style A5 fill:#4CAF50
    
    style B1 fill:#2196F3
    style B2 fill:#2196F3
    style B3 fill:#2196F3
    style B4 fill:#2196F3
    style B5 fill:#2196F3
    
    style C1 fill:#FF9800
    style C2 fill:#FF9800
    style C3 fill:#FF9800
    style C4 fill:#FF9800
    style C5 fill:#FF9800
    
    style D1 fill:#9E9E9E
    style D2 fill:#9E9E9E
    style D3 fill:#9E9E9E
    style D4 fill:#9E9E9E
```

---

## 🖥️ Infrastructure Requirements

### On-Premise Server Specifications

#### Minimum Requirements (MVP - Single Server)

**Hardware Specifications:**
```
Processor:
├── CPU: Intel Xeon / AMD EPYC
├── Cores: 8 cores / 16 threads minimum
├── Clock: 2.5 GHz base frequency
└── Recommended: Intel Xeon E-2288G or equivalent

Memory (RAM):
├── Minimum: 32 GB DDR4
├── Recommended: 64 GB DDR4
└── Type: ECC memory preferred

Storage:
├── System Drive: 256 GB NVMe SSD (OS + Applications)
├── Data Drive: 1 TB NVMe SSD (Database + Files)
├── Backup Drive: 2 TB HDD (Backups)
└── RAID 1 recommended for data protection

Network:
├── Network Card: 1 Gbps ethernet (minimum)
├── Recommended: 10 Gbps for future growth
└── Dual NIC for redundancy (recommended)

Power:
└── UPS: 1500VA minimum for power backup
```

**Software Requirements:**
```
Operating System:
└── Ubuntu Server 22.04 LTS (recommended)
    OR CentOS Stream 9
    OR Debian 12

Required Software:
├── Docker Engine 24+
├── Docker Compose 2.20+
├── Git 2.40+
└── OpenSSH Server

Optional but Recommended:
├── Fail2ban (security)
├── UFW / iptables (firewall)
└── Automated backup tool (rsync, borg)
```

#### Recommended Setup (Production Scale)

**For 500+ Active Users:**
```
Application Server:
├── CPU: 16 cores / 32 threads
├── RAM: 128 GB
├── Storage: 2 TB NVMe SSD (RAID 10)
└── Network: 10 Gbps

Database Server (Separate):
├── CPU: 12 cores / 24 threads
├── RAM: 64 GB (dedicated to PostgreSQL)
├── Storage: 1 TB NVMe SSD (RAID 1)
└── Backup: Automated daily backups

Load Balancer (Optional):
├── CPU: 4 cores
├── RAM: 16 GB
└── Network: 10 Gbps dual NIC
```

### Network Architecture

```mermaid
graph TB
    subgraph "External Network"
        A[Internet]
        B[Golf Course WiFi Network]
    end
    
    subgraph "DMZ - Perimeter"
        C[Firewall]
        D[Load Balancer / NGINX]
    end
    
    subgraph "Application Tier"
        E[App Server 1<br/>Docker Containers]
        F[App Server 2<br/>Failover - Future]
    end
    
    subgraph "Data Tier"
        G[(PostgreSQL<br/>Primary DB)]
        H[(Redis Cache)]
        I[File Storage]
    end
    
    subgraph "Management & Monitoring"
        J[Monitoring Server<br/>Prometheus/Grafana]
        K[Backup Server]
    end
    
    A --> C
    B --> C
    C --> D
    D --> E
    D --> F
    
    E --> G
    E --> H
    E --> I
    F --> G
    F --> H
    F --> I
    
    J -.-> E
    J -.-> F
    J -.-> G
    
    K -.-> G
    K -.-> I
    
    style C fill:#FF6B6B
    style D fill:#4ECDC4
    style E fill:#45B7D1
    style F fill:#45B7D1
    style G fill:#96CEB4
    style H fill:#FFEAA7
```

**Network Requirements:**
- **Internet Bandwidth:** 100 Mbps minimum (1 Gbps recommended)
- **Internal Network:** Gigabit ethernet minimum
- **WiFi Coverage:** Full course coverage untuk mobile app usage
- **Firewall Rules:**
  - Allow HTTP/HTTPS (80, 443)
  - Allow WebSocket (443 or dedicated port)
  - Allow SSH (22) from admin IPs only
  - Block all other inbound traffic

### Security Configuration

**Firewall Rules (UFW Example):**
```bash
# Allow SSH (from admin network only)
ufw allow from 192.168.1.0/24 to any port 22

# Allow HTTP/HTTPS
ufw allow 80/tcp
ufw allow 443/tcp

# Allow WebSocket (if different port)
ufw allow 8080/tcp

# Allow PostgreSQL (internal only)
ufw allow from 10.0.0.0/8 to any port 5432

# Allow Redis (internal only)
ufw allow from 10.0.0.0/8 to any port 6379

# Default deny incoming
ufw default deny incoming
ufw default allow outgoing

# Enable firewall
ufw enable
```

**SSL/TLS Certificate:**
- Let's Encrypt (free, auto-renewal)
- OR Commercial SSL certificate
- HTTPS only (force redirect from HTTP)
- TLS 1.2+ only

**Backup Strategy:**
```
Daily Backups:
├── Time: 2:00 AM (low traffic period)
├── PostgreSQL: Full database dump
├── Files: Incremental backup of uploads
└── Retention: 30 days

Weekly Backups:
├── Time: Sunday 2:00 AM
├── Type: Full system snapshot
└── Retention: 12 weeks (3 months)

Monthly Backups:
├── Time: 1st of month
├── Type: Complete system backup
├── Storage: Off-site / external drive
└── Retention: 12 months

Backup Verification:
└── Monthly restore test to verify backup integrity
```

### Docker Compose Setup Example

```yaml
version: '3.8'

services:
  postgres:
    image: postgres:15-alpine
    container_name: golf_db
    environment:
      POSTGRES_DB: golf_scoring
      POSTGRES_USER: golf_admin
      POSTGRES_PASSWORD: ${DB_PASSWORD}
    volumes:
      - postgres_data:/var/lib/postgresql/data
      - ./backups:/backups
    ports:
      - "5432:5432"
    restart: unless-stopped
    healthcheck:
      test: ["CMD-SHELL", "pg_isready -U golf_admin"]
      interval: 10s
      timeout: 5s
      retries: 5

  redis:
    image: redis:7-alpine
    container_name: golf_cache
    command: redis-server --appendonly yes --requirepass ${REDIS_PASSWORD}
    volumes:
      - redis_data:/data
    ports:
      - "6379:6379"
    restart: unless-stopped
    healthcheck:
      test: ["CMD", "redis-cli", "ping"]
      interval: 10s
      timeout: 3s
      retries: 5

  backend:
    build: ./backend
    container_name: golf_api
    environment:
      NODE_ENV: production
      DATABASE_URL: postgresql://golf_admin:${DB_PASSWORD}@postgres:5432/golf_scoring
      REDIS_URL: redis://:${REDIS_PASSWORD}@redis:6379
      JWT_SECRET: ${JWT_SECRET}
    ports:
      - "3000:3000"
    depends_on:
      postgres:
        condition: service_healthy
      redis:
        condition: service_healthy
    volumes:
      - ./uploads:/app/uploads
    restart: unless-stopped

  nginx:
    image: nginx:alpine
    container_name: golf_nginx
    ports:
      - "80:80"
      - "443:443"
    volumes:
      - ./nginx.conf:/etc/nginx/nginx.conf:ro
      - ./ssl:/etc/nginx/ssl:ro
      - ./static:/usr/share/nginx/html:ro
    depends_on:
      - backend
    restart: unless-stopped

  prometheus:
    image: prom/prometheus:latest
    container_name: golf_prometheus
    volumes:
      - ./prometheus.yml:/etc/prometheus/prometheus.yml
      - prometheus_data:/prometheus
    ports:
      - "9090:9090"
    restart: unless-stopped

  grafana:
    image: grafana/grafana:latest
    container_name: golf_grafana
    environment:
      GF_SECURITY_ADMIN_PASSWORD: ${GRAFANA_PASSWORD}
    volumes:
      - grafana_data:/var/lib/grafana
    ports:
      - "3001:3000"
    depends_on:
      - prometheus
    restart: unless-stopped

volumes:
  postgres_data:
  redis_data:
  prometheus_data:
  grafana_data:
```

### Monitoring & Alerts

**Key Metrics to Monitor:**
```
System Health:
├── CPU Usage (alert if > 80%)
├── Memory Usage (alert if > 85%)
├── Disk Usage (alert if > 90%)
├── Network Traffic
└── Disk I/O

Application Metrics:
├── API Response Time (P95 < 500ms)
├── WebSocket Connection Count
├── Active User Sessions
├── Database Connection Pool
└── Error Rate (alert if > 1%)

Database Metrics:
├── Query Performance
├── Connection Count
├── Cache Hit Ratio (target > 95%)
├── Database Size Growth
└── Replication Lag (if applicable)

Business Metrics:
├── Active Rounds
├── Scores Submitted per Hour
├── Tournament Participation
└── User Engagement
```

---

## 📅 Implementation Timeline

### Complete Project Timeline (5 Months MVP)

```mermaid
gantt
    title Golf Scoring System - Complete Implementation Timeline
    dateFormat  YYYY-MM-DD
    
    section Phase 1 - Foundation
    Project Setup & Planning     :2025-11-01, 5d
    Infrastructure Setup         :2025-11-06, 5d
    Database Design & Setup      :2025-11-11, 4d
    Backend Core Development     :2025-11-15, 15d
    Mobile App Foundation        :2025-11-20, 10d
    Integration & Testing        :2025-11-30, 7d
    
    section Phase 2 - Core Features
    Membership Service           :2025-12-07, 7d
    Real-time Infrastructure     :2025-12-14, 7d
    Tournament Management        :2025-12-21, 7d
    Marshall Workflows           :2025-12-28, 7d
    Testing & Bug Fixes          :2026-01-04, 7d
    
    section Phase 3 - Advanced
    Handicap System              :2026-01-11, 7d
    Analytics & Reporting        :2026-01-18, 7d
    Advanced Tournaments         :2026-01-25, 7d
    Notifications                :2026-02-01, 5d
    Polish & Optimization        :2026-02-06, 10d
    
    section Deployment
    UAT Preparation              :2026-02-16, 5d
    Pilot Golf Course Deployment :2026-02-21, 3d
    Training & Support           :2026-02-24, 5d
    Go-Live                      :2026-03-01, 1d
```

### Detailed Weekly Breakdown

#### Month 1: Foundation (Weeks 1-4)

| Week | Focus Area | Key Deliverables | Team Size |
|------|-----------|------------------|-----------|
| **Week 1** | Project Setup | • Project repo setup<br>• Development environment<br>• Team onboarding<br>• Requirements finalization | 3 developers |
| **Week 2** | Infrastructure | • Server provisioning<br>• Docker setup<br>• Database installation<br>• Network configuration | 2 backend, 1 DevOps |
| **Week 3** | Core Backend | • Auth service<br>• Course management API<br>• User management<br>• API documentation | 2 backend |
| **Week 4** | Mobile App Start | • React Native setup<br>• Login screens<br>• Navigation structure<br>• API integration layer | 2 mobile |

**Week 1 Checklist:**
- ✅ GitHub/GitLab repository created
- ✅ Development branch strategy defined
- ✅ Local development environment documented
- ✅ Code style guide established
- ✅ Initial project documentation
- ✅ Team communication channels setup

**Week 2 Checklist:**
- ✅ Server OS installed and configured
- ✅ Docker and Docker Compose installed
- ✅ PostgreSQL container running
- ✅ Redis container running
- ✅ NGINX configured as reverse proxy
- ✅ SSL certificate obtained and installed
- ✅ Firewall rules configured
- ✅ Backup system configured

**Week 3 Checklist:**
- ✅ User registration/login API working
- ✅ JWT authentication implemented
- ✅ Course CRUD operations complete
- ✅ Hole management API complete
- ✅ Basic API documentation available
- ✅ Unit tests for core functions
- ✅ Postman collection created

**Week 4 Checklist:**
- ✅ Mobile app builds successfully (iOS & Android)
- ✅ Login/logout flow working
- ✅ Profile screen implemented
- ✅ Course selection working
- ✅ API integration layer complete
- ✅ Basic error handling

#### Month 2: Core Scoring Features (Weeks 5-8)

| Week | Focus Area | Key Deliverables | Milestone |
|------|-----------|------------------|-----------|
| **Week 5** | Scoring Engine | • Round management<br>• Score submission API<br>• Validation logic | Core scoring ready |
| **Week 6** | Mobile Scoring | • Score entry UI<br>• Round progress tracking<br>• Statistics display | Scoring UI complete |
| **Week 7** | Leaderboard | • Leaderboard calculation<br>• Ranking algorithm<br>• Display logic | Leaderboards working |
| **Week 8** | Integration | • End-to-end testing<br>• Bug fixing<br>• Performance tuning | **Phase 1 Complete** |

#### Month 3: Real-time & Tournaments (Weeks 9-12)

| Week | Focus Area | Key Deliverables | Milestone |
|------|-----------|------------------|-----------|
| **Week 9** | Membership | • Membership service<br>• Handicap tracking<br>• Member profiles | Membership system ready |
| **Week 10** | WebSocket | • WebSocket server<br>• Real-time updates<br>• Client integration | Real-time working |
| **Week 11** | Tournaments | • Tournament creation<br>• Participant management<br>• Organizer dashboard | Basic tournaments ready |
| **Week 12** | Marshall | • Validation workflow<br>• Marshall interface<br>• Score approval | **Phase 2 Complete** |

#### Month 4-5: Advanced Features & Polish (Weeks 13-20)

| Week | Focus Area | Key Deliverables |
|------|-----------|------------------|
| **Week 13-14** | Handicap System | • USGA handicap calculation<br>• Automated updates<br>• Historical tracking |
| **Week 15-16** | Analytics | • Statistics dashboard<br>• Performance charts<br>• Report generation |
| **Week 17** | Advanced Tournaments | • Match play support<br>• Stableford scoring<br>• Team events |
| **Week 18** | Notifications | • Push notification service<br>• Email notifications<br>• In-app alerts |
| **Week 19-20** | Polish & UAT | • UI/UX refinement<br>• Performance optimization<br>• User testing |

### Deployment & Training Schedule

```mermaid
gantt
    title Deployment & Training Phase
    dateFormat  YYYY-MM-DD
    
    section Preparation
    UAT Environment Setup        :2026-02-16, 2d
    UAT Testing with Pilot Users :2026-02-18, 3d
    Bug Fixes & Adjustments      :2026-02-21, 3d
    
    section Training
    Admin Training Session       :2026-02-24, 1d
    Organizer Training           :2026-02-25, 1d
    Marshall Training            :2026-02-26, 1d
    Member Onboarding Materials  :2026-02-27, 2d
    
    section Go-Live
    Production Deployment        :2026-03-01, 1d
    Monitoring & Support         :2026-03-02, 7d
    Post-Launch Review           :2026-03-09, 1d
```

**Training Plan:**

1. **Admin Training (1 day)**
   - System overview
   - User management
   - Course configuration
   - Membership management
   - Backup/restore procedures
   - Troubleshooting basics

2. **Tournament Organizer Training (1 day)**
   - Tournament creation
   - Participant management
   - Live monitoring
   - Score adjustments
   - Report generation

3. **Marshall Training (1 day)**
   - Score validation process
   - Mobile tablet usage
   - Issue reporting
   - Communication protocols

4. **Member Onboarding (Self-service)**
   - Video tutorials
   - Quick start guide
   - FAQ documentation
   - Support contact info

### Post-Launch Support Plan

**Week 1-2 (Intensive Support):**
- Daily check-ins with golf course management
- On-site support available
- Real-time bug fixes
- User feedback collection

**Week 3-4 (Standard Support):**
- Every-other-day check-ins
- Remote support
- Bug fix releases
- Feature request collection

**Month 2+ (Ongoing Support):**
- Weekly status meetings
- Monthly feature updates
- Quarterly system reviews
- Annual major updates

---

## 💰 Budget Estimation

### Development Cost Breakdown

#### Team Composition & Cost (5 Months MVP)

| Role | Headcount | Monthly Rate (IDR) | Total Cost (5 months) |
|------|-----------|-------------------|---------------------|
| **Project Manager** | 1 | Rp 20,000,000 | Rp 100,000,000 |
| **Backend Developer (Senior)** | 1 | Rp 25,000,000 | Rp 125,000,000 |
| **Backend Developer (Mid)** | 1 | Rp 18,000,000 | Rp 90,000,000 |
| **Mobile Developer (React Native)** | 2 | Rp 22,000,000 | Rp 220,000,000 |
| **Frontend Developer (Web)** | 1 | Rp 20,000,000 | Rp 100,000,000 |
| **DevOps Engineer** | 1 (part-time) | Rp 12,000,000 | Rp 60,000,000 |
| **UI/UX Designer** | 1 (part-time) | Rp 10,000,000 | Rp 50,000,000 |
| **QA Engineer** | 1 | Rp 15,000,000 | Rp 75,000,000 |
| **Technical Writer** | 1 (part-time) | Rp 8,000,000 | Rp 40,000,000 |
| **Total Personnel** | **~7 FTE** | | **Rp 860,000,000** |

**Note:** Rates are indicative for Indonesian market (2025)

### Infrastructure Cost (On-Premise)

#### One-Time Hardware Investment

| Item | Specification | Unit Price (IDR) | Quantity | Total |
|------|--------------|-----------------|----------|-------|
| **Server (Dell PowerEdge R450)** | 16C/128GB/2TB SSD | Rp 80,000,000 | 1 | Rp 80,000,000 |
| **UPS (APC Smart-UPS 1500VA)** | 1500VA / 900W | Rp 8,000,000 | 1 | Rp 8,000,000 |
| **Network Switch (Managed)** | 24-port Gigabit | Rp 5,000,000 | 1 | Rp 5,000,000 |
| **Backup Storage (NAS)** | 4-bay, 8TB | Rp 12,000,000 | 1 | Rp 12,000,000 |
| **Firewall (Optional)** | Hardware firewall | Rp 15,000,000 | 1 | Rp 15,000,000 |
| **Installation & Setup** | - | Rp 10,000,000 | - | Rp 10,000,000 |
| **Total Hardware** | | | | **Rp 130,000,000** |

**Alternative Budget Option:**
- **Mid-Range Server:** Rp 40,000,000 (sufficient for MVP)
- **Total Hardware (Budget):** **Rp 75,000,000**

#### Ongoing Operational Costs (Yearly)

| Item | Monthly Cost (IDR) | Yearly Cost (IDR) |
|------|-------------------|------------------|
| Internet (100 Mbps dedicated) | Rp 5,000,000 | Rp 60,000,000 |
| Electricity (server + cooling) | Rp 3,000,000 | Rp 36,000,000 |
| SSL Certificate (commercial) | - | Rp 2,000,000 |
| Domain Name | - | Rp 500,000 |
| Server Room/Rack Rental | Rp 4,000,000 | Rp 48,000,000 |
| **Total Operational** | **Rp 12,000,000** | **Rp 146,500,000** |

### Software Licenses (All Open Source - $0)

✅ **No licensing costs for:**
- Operating System (Ubuntu Server - Free)
- Database (PostgreSQL - Free)
- Cache (Redis - Free)
- Web Server (NGINX - Free)
- Application Framework (Node.js/React Native - Free)
- Monitoring (Prometheus/Grafana - Free)

### Other Costs

| Category | Description | Cost (IDR) |
|----------|-------------|-----------|
| **Design Assets** | Icons, illustrations, branding | Rp 15,000,000 |
| **Testing Devices** | iOS/Android test devices | Rp 20,000,000 |
| **Subscriptions** | GitHub, monitoring tools | Rp 5,000,000 |
| **Contingency (10%)** | Unexpected expenses | Rp 100,000,000 |
| **Total Other Costs** | | **Rp 140,000,000** |

### Total Project Budget Summary

| Category | Amount (IDR) | Percentage |
|----------|-------------|-----------|
| **Development Team (5 months)** | Rp 860,000,000 | 73.5% |
| **Hardware (One-time)** | Rp 130,000,000 | 11.1% |
| **Other Costs** | Rp 140,000,000 | 12.0% |
| **First Year Operations** | Rp 40,000,000 | 3.4% |
| **TOTAL PROJECT COST** | **Rp 1,170,000,000** | **100%** |

**Approximate:** **~USD $75,000** (at 1 USD = 15,600 IDR)

### Budget Breakdown by Phase

```mermaid
pie title Budget Allocation by Phase
    "Development Team" : 860
    "Hardware Infrastructure" : 130
    "Operations (3 months)" : 40
    "Design & Testing" : 35
    "Contingency" : 105
```

### Cost Comparison: On-Premise vs Cloud

| Aspect | On-Premise (Our Solution) | Cloud-Based (AWS/GCP) |
|--------|--------------------------|---------------------|
| **Initial Investment** | Rp 130M (hardware) | Rp 0 (pay-as-you-go) |
| **Monthly Operational** | Rp 12M (fixed) | Rp 20-30M (variable) |
| **Year 1 Total** | Rp 274M | Rp 240-360M |
| **Year 2 Total** | Rp 144M | Rp 240-360M |
| **Year 3 Total** | Rp 144M | Rp 240-360M |
| **3-Year Total** | **Rp 562M** | **Rp 720-1,080M** |
| **Data Control** | ✅ Full control | ❌ Vendor dependent |
| **Customization** | ✅ Unlimited | ⚠️ Limited |

**ROI Analysis:**
- Break-even point: **~18 months** vs cloud
- Year 3 savings: **~Rp 200-500M** vs cloud
- Long-term: On-premise **30-50% cheaper**

### Maintenance & Support Cost (Post-Launch)

**Annual Maintenance Contract:**

| Service | Description | Annual Cost (IDR) |
|---------|-------------|------------------|
| **Technical Support** | 1 developer part-time | Rp 120,000,000 |
| **Server Maintenance** | Monitoring, updates, backups | Rp 36,000,000 |
| **Feature Updates** | Minor enhancements | Rp 60,000,000 |
| **Bug Fixes** | Priority bug resolution | Included |
| **Total Annual Maintenance** | | **Rp 216,000,000** |

---

## ⚠️ Risk Management & Mitigation

### Identified Risks & Mitigation Strategies

#### 1. Technical Risks

| Risk | Impact | Probability | Mitigation Strategy |
|------|--------|------------|-------------------|
| **Database Performance Issues** | High | Medium | • Proper indexing<br>• Query optimization<br>• Redis caching<br>• Regular performance testing |
| **Real-time Latency** | High | Medium | • WebSocket optimization<br>• Redis pub/sub<br>• Load testing<br>• CDN for static assets |
| **Mobile App Crashes** | High | Low | • Comprehensive error handling<br>• Crash reporting (Sentry)<br>• Thorough QA testing<br>• Beta testing phase |
| **Data Loss** | Critical | Low | • Daily automated backups<br>• RAID configuration<br>• Off-site backup storage<br>• Regular restore testing |
| **Server Hardware Failure** | High | Low | • UPS for power backup<br>• Regular hardware monitoring<br>• Spare parts availability<br>• Vendor support contract |
| **Security Breach** | Critical | Low | • Regular security audits<br>• Penetration testing<br>• Security updates<br>• Access logging |

#### 2. Operational Risks

| Risk | Impact | Probability | Mitigation Strategy |
|------|--------|------------|-------------------|
| **Poor User Adoption** | High | Medium | • User-friendly design<br>• Comprehensive training<br>• On-site support<br>• Gradual rollout |
| **Resistance to Change** | Medium | High | • Change management plan<br>• Executive sponsorship<br>• Quick wins demonstration<br>• Member champions program |
| **Inadequate Training** | Medium | Medium | • Multi-format training<br>• Video tutorials<br>• Hands-on workshops<br>• Support documentation |
| **Staff Turnover** | Medium | Low | • Comprehensive documentation<br>• Knowledge transfer sessions<br>• Code documentation<br>• Admin training |

#### 3. Business Risks

| Risk | Impact | Probability | Mitigation Strategy |
|------|--------|------------|-------------------|
| **Budget Overrun** | High | Medium | • 10% contingency buffer<br>• Regular budget reviews<br>• Scope control<br>• Phased approach |
| **Timeline Delays** | Medium | Medium | • Realistic estimates<br>• Buffer time in schedule<br>• Regular progress tracking<br>• Agile methodology |
| **Scope Creep** | Medium | High | • Clear requirements doc<br>• Change control process<br>• Regular stakeholder reviews<br>• MVP focus |
| **Golf Course Bankruptcy** | Medium | Low | • Multiple pilot courses<br>• Contract guarantees<br>• Transferable licenses |

#### 4. External Risks

| Risk | Impact | Probability | Mitigation Strategy |
|------|--------|------------|-------------------|
| **Internet Outage** | High | Low | • Offline mode (future)<br>• Mobile data backup<br>• Clear downtime procedures<br>• Data sync on reconnect |
| **Power Outage** | High | Low | • UPS backup (4-6 hours)<br>• Generator (if available)<br>• Graceful shutdown scripts |
| **Natural Disasters** | Critical | Very Low | • Off-site backups<br>• Disaster recovery plan<br>• Insurance coverage<br>• Cloud backup option |
| **Regulatory Changes** | Medium | Low | • Stay informed on regulations<br>• Legal consultation<br>• Flexible architecture<br>• Compliance documentation |

### Risk Priority Matrix

```mermaid
quadrantChart
    title Risk Assessment Matrix
    x-axis Low Impact --> High Impact
    y-axis Low Probability --> High Probability
    quadrant-1 Monitor Closely
    quadrant-2 High Priority Action
    quadrant-3 Low Priority
    quadrant-4 Mitigation Plan Required
    Database Performance: [0.7, 0.5]
    Real-time Latency: [0.7, 0.5]
    Data Loss: [0.9, 0.2]
    Security Breach: [0.9, 0.2]
    Poor Adoption: [0.7, 0.5]
    Resistance to Change: [0.5, 0.7]
    Budget Overrun: [0.7, 0.5]
    Scope Creep: [0.5, 0.7]
    Internet Outage: [0.7, 0.2]
```

### Contingency Plans

#### Plan A: Major Technical Failure
**Trigger:** System down for > 4 hours

**Actions:**
1. Activate disaster recovery plan
2. Switch to backup server (if available)
3. Communicate with all stakeholders
4. Restore from most recent backup
5. Root cause analysis post-incident

#### Plan B: Poor User Adoption (<50% target)
**Trigger:** < 40% active users after 1 month

**Actions:**
1. Conduct user surveys
2. Identify pain points
3. Organize additional training sessions
4. Simplify UI based on feedback
5. Launch incentive program
6. One-on-one support sessions

#### Plan C: Budget Exhaustion
**Trigger:** 80% budget used at 60% completion

**Actions:**
1. Re-prioritize features (cut nice-to-haves)
2. Seek additional funding
3. Reduce team size (if possible)
4. Extend timeline
5. Launch MVP with reduced scope

### Quality Assurance Strategy

**Testing Levels:**

1. **Unit Testing**
   - Backend: Jest (target 80% coverage)
   - Frontend: React Testing Library
   - Automated via CI/CD

2. **Integration Testing**
   - API endpoint testing
   - Database integration tests
   - WebSocket connection tests

3. **System Testing**
   - End-to-end user flows
   - Performance testing
   - Load testing (50+ concurrent users)
   - Security testing

4. **User Acceptance Testing (UAT)**
   - 2-week pilot with golf course staff
   - Real-world scenario testing
   - Feedback collection
   - Bug reporting

**Quality Gates:**
- ✅ No critical bugs in production
- ✅ < 5 high-priority bugs
- ✅ 90% test coverage for core features
- ✅ P95 API response time < 500ms
- ✅ 99.5% uptime during UAT

---

## 📊 Success Metrics & KPIs

### Key Performance Indicators (KPIs)

#### Technical KPIs

| Metric | Target | Measurement Method |
|--------|--------|-------------------|
| **System Uptime** | > 99.5% | Monitoring tools (Prometheus) |
| **API Response Time (P95)** | < 500ms | Application Performance Monitoring |
| **WebSocket Latency** | < 3 seconds | Real-time monitoring |
| **Database Query Time (P95)** | < 100ms | PostgreSQL slow query log |
| **Error Rate** | < 0.5% | Application logs analysis |
| **Page Load Time** | < 2 seconds | Lighthouse / WebPageTest |
| **Mobile App Crash Rate** | < 0.1% | Crashlytics / Sentry |

#### User Adoption KPIs

| Metric | Month 1 Target | Month 3 Target | Month 6 Target |
|--------|---------------|---------------|---------------|
| **Active Users (MAU)** | 50% members | 80% members | 90% members |
| **Daily Active Users (DAU)** | 20% members | 30% members | 40% members |
| **Rounds Recorded Digitally** | 60% | 85% | 95% |
| **Tournament Participation** | 70% digital | 90% digital | 100% digital |
| **Mobile App Installs** | 70% members | 85% members | 95% members |

#### Business KPIs

| Metric | Target | Description |
|--------|--------|-------------|
| **Time Saved per Tournament** | 80% reduction | vs manual scoring |
| **Score Accuracy** | > 95% | Validated scores |
| **Member Satisfaction (NPS)** | > 8.0 | Net Promoter Score |
| **Staff Efficiency Gain** | 70% time saved | Admin/organizer tasks |
| **Support Ticket Volume** | < 5 per week | After month 2 |

### Monitoring Dashboard

**Real-time Metrics to Display:**

```
System Health Dashboard:
├── Server CPU/Memory Usage
├── Database Connections
├── Redis Cache Hit Rate
├── Active WebSocket Connections
├── Current API Request Rate
└── Error Logs (last 24 hours)

Business Metrics Dashboard:
├── Active Rounds (right now)
├── Scores Submitted (today)
├── Active Users (today)
├── Tournament Status
├── Leaderboard Updates (last hour)
└── New Member Registrations

User Engagement:
├── Daily/Weekly/Monthly Active Users
├── Average Session Duration
├── Feature Usage Statistics
├── Most Active Features
└── User Retention Rate
```

### Post-Launch Review Checklist

**Week 1 Review:**
- ✅ System stability assessment
- ✅ Critical bug count
- ✅ User feedback collection
- ✅ Performance metrics review
- ✅ Support ticket analysis

**Month 1 Review:**
- ✅ User adoption rate
- ✅ Feature usage analysis
- ✅ Performance optimization needs
- ✅ Training effectiveness
- ✅ ROI preliminary assessment

**Month 3 Review:**
- ✅ Full KPI dashboard review
- ✅ User satisfaction survey
- ✅ System scalability assessment
- ✅ Feature roadmap adjustment
- ✅ Phase 2 planning

---

## 🚀 Next Steps & Recommendations

### Immediate Actions (Week 1)

1. **Stakeholder Alignment**
   - ✅ Present this plan to golf course management
   - ✅ Get budget approval
   - ✅ Identify pilot golf course(s)
   - ✅ Establish project governance

2. **Team Formation**
   - ✅ Recruit development team
   - ✅ Assign roles and responsibilities
   - ✅ Setup communication channels
   - ✅ Schedule kickoff meeting

3. **Infrastructure Preparation**
   - ✅ Procure server hardware
   - ✅ Setup development environment
   - ✅ Create project repository
   - ✅ Establish development standards

### Decision Points

**Key Decisions Needed:**

| Decision | Options | Recommendation |
|----------|---------|---------------|
| **Tech Stack** | Node.js vs Python | Node.js (better for real-time) |
| **Mobile Framework** | React Native vs Flutter | React Native (larger community) |
| **Database** | PostgreSQL vs MySQL | PostgreSQL (better JSON support) |
| **Deployment** | Docker vs Kubernetes | Docker Compose (simpler for MVP) |
| **Monitoring** | Prometheus vs Datadog | Prometheus (free, powerful) |

### Future Enhancements (Post-MVP)

**Phase 4 & Beyond:**

1. **Advanced Features**
   - AI-powered performance insights
   - Social features (challenges, clubs)
   - Integration with golf GPS watches
   - Weather integration
   - Offline mode support

2. **Scalability**
   - Multi-golf course platform
   - White-label solution for other courses
   - Regional tournaments support
   - National ranking system

3. **Business Expansion**
   - Membership marketplace
   - Pro shop integration
   - Tee time booking integration
   - E-commerce for golf equipment
   - Advertising platform

### Contact & Support

**Project Team:**
- **Project Lead:** [Name]
- **Technical Architect:** [Name]
- **Email:** project@golfscoring.id
- **Phone:** +62 XXX XXXX XXXX

**Documentation Links:**
- 📘 Technical Documentation: [URL]
- 🎨 Design Files: [URL]
- 💻 Code Repository: [URL]
- 📊 Project Dashboard: [URL]

---

## 📎 Appendices

### Appendix A: API Endpoint Specification (Sample)

```
Authentication Endpoints:
POST   /api/auth/register          - Register new user
POST   /api/auth/login             - User login
POST   /api/auth/logout            - User logout
POST   /api/auth/refresh-token     - Refresh JWT token
GET    /api/auth/me                - Get current user info

User Endpoints:
GET    /api/users/:id              - Get user by ID
PUT    /api/users/:id              - Update user profile
GET    /api/users/:id/stats        - Get user statistics
GET    /api/users/:id/rounds       - Get user round history

Course Endpoints:
GET    /api/courses                - List all courses
GET    /api/courses/:id            - Get course details
GET    /api/courses/:id/holes      - Get course holes
POST   /api/courses                - Create course (admin)
PUT    /api/courses/:id            - Update course (admin)

Round Endpoints:
POST   /api/rounds                 - Start new round
GET    /api/rounds/:id             - Get round details
PUT    /api/rounds/:id             - Update round
POST   /api/rounds/:id/complete    - Complete round
GET    /api/rounds/active          - Get active rounds

Score Endpoints:
POST   /api/scores                 - Submit score
PUT    /api/scores/:id             - Update score
GET    /api/scores/round/:roundId  - Get all scores for round
POST   /api/scores/:id/validate    - Validate score (marshall)

Tournament Endpoints:
GET    /api/tournaments            - List tournaments
POST   /api/tournaments            - Create tournament
GET    /api/tournaments/:id        - Get tournament details
PUT    /api/tournaments/:id        - Update tournament
POST   /api/tournaments/:id/register - Register for tournament
GET    /api/tournaments/:id/leaderboard - Get leaderboard

Leaderboard Endpoints:
GET    /api/leaderboards/:tournamentId - Get live leaderboard
WS     /ws/leaderboard/:tournamentId  - WebSocket subscribe
```

### Appendix B: Database Indexes Strategy

```sql
-- Critical Indexes for Performance

-- Users table
CREATE INDEX idx_users_email ON users(email);
CREATE INDEX idx_users_role ON users(role);
CREATE INDEX idx_users_status ON users(status);

-- Rounds table
CREATE INDEX idx_rounds_player_date ON rounds(player_id, round_date DESC);
CREATE INDEX idx_rounds_tournament ON rounds(tournament_id) WHERE tournament_id IS NOT NULL;
CREATE INDEX idx_rounds_status ON rounds(status);
CREATE INDEX idx_rounds_course_date ON rounds(course_id, round_date DESC);

-- Scores table
CREATE UNIQUE INDEX idx_scores_round_hole ON scores(round_id, hole_id);
CREATE INDEX idx_scores_recorded_at ON scores(recorded_at DESC);

-- Leaderboards table
CREATE UNIQUE INDEX idx_leaderboard_tournament_player ON leaderboards(tournament_id, player_id);
CREATE INDEX idx_leaderboard_tournament_position ON leaderboards(tournament_id, position);

-- Memberships table
CREATE UNIQUE INDEX idx_membership_user_course ON memberships(user_id, course_id);
CREATE INDEX idx_membership_number ON memberships(membership_number);
CREATE INDEX idx_membership_status ON memberships(status);

-- Tournament participants
CREATE UNIQUE INDEX idx_participant_tournament_user ON tournament_participants(tournament_id, user_id);
```

### Appendix C: Environment Variables Template

```bash
# .env.example

# Application
NODE_ENV=production
PORT=3000
API_VERSION=v1

# Database
DATABASE_HOST=localhost
DATABASE_PORT=5432
DATABASE_NAME=golf_scoring
DATABASE_USER=golf_admin
DATABASE_PASSWORD=<strong_password>
DATABASE_SSL=false
DATABASE_POOL_MIN=2
DATABASE_POOL_MAX=10

# Redis
REDIS_HOST=localhost
REDIS_PORT=6379
REDIS_PASSWORD=<redis_password>
REDIS_DB=0

# JWT
JWT_SECRET=<random_secret_key>
JWT_EXPIRES_IN=24h
JWT_REFRESH_EXPIRES_IN=7d

# WebSocket
WS_PORT=8080
WS_PATH=/ws

# File Upload
UPLOAD_DIR=./uploads
MAX_FILE_SIZE=5242880  # 5MB

# CORS
CORS_ORIGIN=https://yourdomain.com

# Email (optional)
SMTP_HOST=smtp.gmail.com
SMTP_PORT=587
SMTP_USER=your-email@gmail.com
SMTP_PASSWORD=<app_password>

# Monitoring
SENTRY_DSN=<sentry_dsn>  # optional

# Backup
BACKUP_DIR=/backups
BACKUP_RETENTION_DAYS=30
```

### Appendix D: Glossary

| Term | Definition |
|------|------------|
| **Handicap** | A numerical measure of a golfer's potential ability |
| **Par** | The number of strokes a scratch golfer should take to complete a hole or course |
| **GIR (Green in Regulation)** | Reaching the green in the expected number of strokes |
| **Stroke Play** | Tournament format where total strokes determine the winner |
| **Match Play** | Tournament format where holes won/lost determine the winner |
| **Stableford** | Scoring system based on points rather than strokes |
| **Marshall** | Course official who ensures pace of play and rules compliance |
| **Caddy** | Person who carries a player's clubs and provides assistance |
| **Round** | Complete play of all holes (typically 18) |
| **Tee Time** | Scheduled start time for a round |

---

## 📝 Document Version Control

| Version | Date | Author | Changes |
|---------|------|--------|---------|
| 1.0 | 2025-10-22 | Claude | Initial comprehensive plan document |

---

## ✅ Approval Signatures

**Prepared by:**  
Name: ___________________  
Title: Project Lead  
Date: ___________________  

**Reviewed by:**  
Name: ___________________  
Title: Technical Architect  
Date: ___________________  

**Approved by:**  
Name: ___________________  
Title: Golf Course Management  
Date: ___________________  

---

**END OF DOCUMENT**

*This document is confidential and intended for stakeholders of the Golf Scoring System project only.*