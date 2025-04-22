---
title: The structure of the Gybernaty organization
description: 
published: true
date: 2025-04-22T01:37:47.450Z
tags: 
editor: markdown
dateCreated: 2025-04-22T01:37:47.450Z
---

# **The structure of the Gybernaty organization: a system of levels - UnitTypes, criteria for growth and motivation**  


---

## **1. General provisions**  
This document defines:  
1. The hierarchy of members of the Gybernaty community.  
2. Criteria for the transition between levels.  
3. Remuneration and management system.  
4. Mandatory quality control procedures.  


---

## **2. Levels of participants - Unit Types**

### **2.1. Unit (Beginner)**
**Description**: A basic level for new participants who master the fundamental skills of developing and operating principles of decentralized systems and other relevant technologies.

**Requirements**:
- Registration in the Gybernaty ID system
- Completion of required courses:
- "Fundamentals of Git and GitHub" (minimum 80% points)
- "Blockchain for beginners" (certification exam)
- "Fundamentals of the command line" (Linux/macOS/Windows)

**Responsibilities**:
- Performing 3+ training tasks monthly:
- Testing MVP projects
- Writing technical documentation
- Participating in a code review (observer)
- Attend 2+ training webinars per month

**Privileges**:
- Access to GyberUniversity (basic courses)
- Participation in a private chat for newbies
- The opportunity to apply for internships in projects
- Appointment of a mentor from among the Dev+

**Duration of stay**: 1-6 months (depending on entry level and progress)

---

### **2.2. Dev (Developer)**
**Description**: The main production staff performing key technical tasks in the field of specialization.

**Requirements**:
- Successful completion of the Unit level or the availability of Dev level skills
- 5+ approved PRS in the main repositories
- Protection of a Junior-level project:
  - Frontend: Development of the React/Next component.js
Backend: REST API on the selected stack
  - Blockchain: A simple smart contract with tests

**Responsibilities**:
- Implementation of 3+ tasks per month by specialization
- Participation in sprint planning
- Conducting a code review for the Unit
- Project documentation support

**Privileges**:
- Access to projects with a budget of up to 10 B Gbr
- Voting rights in the DAO (weight 1x)
- Access to GyberUniversity Pro intermediate courses
- The opportunity to become a mentor

**Specializations**:
1. Frontend (React/Next.js + Web3)
2. Backend (Python/Node.js/Go/Rust)
3. Blockchain (Solidity/Rust)
4. DevOps (Docker/K8s/CI-CD)

---

### **2.3. LeadDev (Lead Developer)**
**Description**: Technical leaders responsible for the implementation of complex projects and mentoring.

**Requirements**:
- 3-6 months in Dev status or 1 month with LeadDev level skills
- Successful completion of 1+ medium-level projects:
- Budget 10 B-30 B Gbr
- Implementation period 3+ months
### **Updated requirements for expertise in specializations**  

---

 **1. Frontend expertise**  
**Required skills:**  
- Optimization of Core Web Vitals:
- LCP < 1.2s via SSR/ISR (Next.js)
- CLS < 0.1 with dynamic layouts  
  - Integration of Web Workers for heavy computing  
- Advanced state management:
- Zustand + Immer for complex states  
  - Optimization of renderers via React Forget (expected in React 19)  
- Web3 stack:
- Wagmi+ Viem for interaction with the blockchain  
  - Adaptation to WalletConnect v2  

**Additional competencies:**  
- WebAssembly:
- Assembly of Rust modules in WASM for the frontend  
  - Optimization of WASM bundles (wasm-pack + wasm-opt)  
- Micro frontends:  
  - Module Federation (Webpack 5)
- Cross-front-end communication  

---

 **2. Backend expertise**  
**By stack:**  

 **Python (FastAPI/Starlette)**  
- Asynchronous databases:  
  - SQLAlchemy 2.0 + asyncpg
- Optimization of complex JOINS via Materialized Views  
- Highload patterns:
- Rate limiting at the Nginx + Lua level
- Caching via RedisJSON  

 **Node.js (NestJS)**  
- Microservice architecture:
- gRPC transport with protobuf serialization  
  - Saga is a pattern for distributed transactions  
- Security:
- JWT-authorization with OPA/Rego  

 **Golang**  
- Profiling:
- pprof + flamegraph  
  - Allocation of memory via sync.Pool  
- Cloud-Native:
- Auto-scaling via K8s Operators  

 **Rust**  
- Security:
- fuzzing-tests with cargo-fuzz
- Audit of unsafe blocks  
- Performance:
- SIMD optimization (std::simd)  

---

 **3. Blockchain Expertise**  
**Basic level:**  
- EVM-network nuances:
- Gas optimization (EIP-4844 for blobs)
- MEV-resistance (Flashbots Protect)  
- Tools:
- Foundry + Anvil for local testing  
  - Hardhat for complex deployments  

**Advanced level:**  
- ZK technologies:
- Circom for custom circuits  
  - Plonky2 for recursive proofs  
- Cross-chain:
- CCIP (Chainlink) for arbitration messaging
- IBC (Cosmos) for inter-hub communication  

**Contract audit:**  
- Static analysis:
- Slither with custom detectors  
  - Semgrep for finding template vulnerabilities  
- Dynamic analysis:
- Echidna for property-based tests  
  - Differential fuzzing  

---

 **4. DevOps/SRE expertise**  
**For the blockchain infrastructure:**  
- Nodes:
- Geth optimization (snapshots + state pruning)  
  - Monitoring via Prometheus + Grafana Loki  
- Security:
- Falco for anomaly detection  
  - Vault for managing private keys  

**Cloud solutions:**  
- GitOps:
- ArgoCD + Kustomize
- Crossplane for multicloud management  
- Cost optimization:
- Spot instances with graceful degradation  

---

### **Examination confirmation criteria**

 **1. Practical exam**
For each level and specialization:

**Frontend:**
- Implementation of an SSR application with:
- LCP < 1.2s on mobile devices (Lighthouse Audit)
- Integration of a Web3 wallet via WalletConnect v2
  - Optimization of bundles (size of the main.js < 150kb)

**Backend:**
- Development of a highly loaded API:
- Processing 10k+ RPS (test via k6)
- Implementation of graceful degradation at 90% load
  - JWT authorization with refresh tokens

**Blockchain:**
- Creation and audit of a smart contract:
- Gas optimization (saving ≥30% of baseline)
- Protection against reentrancy and frontrunning
  - Full Test coverage (Foundry)

 **2. Code review**
Analysis requirements:

- For Dev:
- Checking 3+ PRS of medium difficulty
  - Identification of at least 2 critical issues in each
- Suggestion of optimizations

- For LeadDev+:
  - Audit of architectural solutions
- Verification of security best practices
  - Performance analysis (profiling)

---

**Responsibilities**:
- Leadership of the 3-5 Dev/Unit team
- Design of solution architecture
- Technical interviewing of candidates
- Participation in strategic planning

**Privileges**:
- Access to projects with a budget of up to 50,000 Gbr
- Voice weight in DAO 3x
- Access to premium courses
- 2% of the budget of managed projects
- The right to initiate new projects

---

### **2.4. ArchDev (Architect)**
**Description**: The highest technical level that defines the development strategy of the entire ecosystem.

**Requirements**:
- Implementation of 1+ enterprise project:
- Budget 50 B+ Gbr
- Cross-functional team
- Integration with external systems
- Contribution to the core of Gybernaty:
- Standards development
  - System improvements

**Responsibilities**:
- System architecture design
- Technical leadership in the direction of
- Negotiations with key partners
- Formation of the technological stack
- Arbitration of technical disputes

**Privileges**:
- Unlimited access to all projects
- Voice weight in DAO 5x
- 5% of the income of the managed area
- The right to veto critical decisions
- Access to private meetings with investors

**Appointment procedure**:
1. Nomination of 2+ current ArchDev
2. Public portfolio protection
3. Secret ballot (70% approval)
4. Inauguration with the transfer of the NFT certificate

---

### **2.5. Special statuses**
**Research Fellow** (for all levels):
- Conducting fundamental research
- Access to the experimental budget
- Publication of the results is required

**Ecosystem Ambassador** (LeadDev+):
- Representation at conferences
- Maintenance of a technical blog
- 500 M Gbr/month bonus for activity

*(For the full criteria for special statuses, see Appendix 4)* 

---

## **3. Criteria for the transition between levels**  
### **3.1. Unit → Dev**  
1. Completion of courses:
- Git & CI/CD.  
   - Fundamentals of Solidity.  
2. Practical tasks:
- 5 successful PR (bugfixes, tests).  
3. Code review from LeadDev+.  

### **3.2. Dev → LeadDev**  
1. Implementation of 2+ projects of the "Medium" level.
2. Skills:
- Rust or Go (confirmed by the test).  
   - Audit of smart contracts.
3. Positive feedback from 5+ participants.  

*(For detailed conditions for all levels, see Appendix 2.)*  

---

## **4. The reward system**  
### **4.1. Accrual of Gbr tokens**  
| **Action**               | Unit | Dev  | LeadDev | ArchDev |  
|----------------------------|------|------|---------|---------|  
| Task Completion | 10 | 30 | 50 | – |  
| Project Management | – | 100 | 200 + 2 % of the budget | 500 + 5% of the budget |  

### **4.2. Additional mechanisms**  
- **Steaking**:
- LeadDev/ArchDev increase the weight of the voice up to 1.5x with a steak starting from 500 Gbr.  
- **Token Burning**:
- 10% of project revenue is burned quarterly.  

*(For the full economic model, see Appendix 3.)*  

---

## **5. Governance (DAO)**  
### **5.1. Types of solutions**  
1. **Operational** (LeadDev): Selection of tools, design.
2. **Strategic** (ArchDev): Budget, technology stack.  
3. **Ecosystem** (Core/Collective Solutions through DAO): Partnerships, token burning.  

### **5.2. Voting procedure**  
1. Initiative → Discussion (7 days) → Voting (3 days).  
2. Quorum:
- 30% for operational decisions.  
   - 50% for strategic purposes.  

---

## **6. Quality control**  
### **6.1. Activity and Reputation audit System**

#### **Multi-level monitoring system**
**1 . Weekly micro-audit:**
- Automatic tracking via:
- GitHub Activity Score (commits, PR, review)
- DAO Participation Index (votes, suggestions)
  - Mentorship Points (mentoring activity)
- **Threshold values:**
- Dev: ≥15 units. activities
  - LeadDev: ≥25 units. activities
  - ArchDev: ≥10 units. (but with a focus on strategic objectives)

**2. Quarterly comprehensive audit:**
- **Technical contribution:**
- Code Impact Score (according to GitPrime):
- Uniqueness of the code
- Criticality of changes
- Impact on architecture
- **Social capital:**
- Peer Review Rating (peer ratings)
- Community Help Score (help in chats)

#### **Dynamic sanctions system**
**Flexible response system:**
1. **The first violation:**
   - Automatic appointment of a supervisor
- Mandatory course "Time management in distributed teams"

2. **Repeated violation:**
- Temporary restriction of rights:
     - Dev: ban on participation in new projects (2 weeks)
- LeadDev: voice weight reduction to 1x
   - The requirement to pass a stress test (solving a difficult task in 48 hours)

3. **Chronic non-compliance:**
- Automatic demotion with "quarantine":
- LeadDev → Dev: at least 3 months before re-certification
     - Dev → Unit: complete qualification review

#### **The system of bonuses for stability**
- **Quarterly bonuses:**
- 100 Gbr for 12 weeks of 100% activity
  - NFT badge "Indestructible" (gives +5% to rewards)
- **Compensation mechanisms:**
- The possibility of "paying off" passes (1 day = 10 Gbr to the general fund)
- The system of "activity credit" (accumulation of excess)

#### **Technical implementation**
1. **Automated system:**
- Bot @GyberAuditor in Discord
   - Personal dashboard with:
     - Forecast of downgrade risk
     - Comparison with colleagues of the same level
     - Recommendations for improvement

2. **The human factor:**
   - Randomized verification of 5% of audits by the ArchDev committee
   - The possibility of appeal through the DAO (cost - 50 Gbr)

#### **Special conditions**
- **For ArchDev:**
- Alternative evaluation system:
- Impact on strategy (number of accepted proposals)
- Peer review of 3 random LeadDev
- **Grace periods:**
- Possibility to freeze the audit (maximum 2 weeks per year)
- Seasonal coefficients (summer = ×0.8 requirements)

*(For a complete mathematical model of calculations, see Appendix 7. Machine learning algorithms for contribution assessment)*

  

### **6.2. Arbitration**  
Conflicts are resolved by a committee of 3 ArchDev (rotating every 6 months).  

---

## **7. Final provisions**  
1. The document is valid until changes are made through the DAO.  
2. Participants are required to comply with the rules from the moment of registration.  

---