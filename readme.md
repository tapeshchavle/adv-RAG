<![CDATA[<div align="center">

# 🏗️ Enterprise AI Platform — Architecture Reference

### *A Principal/Staff Engineer's Complete System Design*

[![Architecture](https://img.shields.io/badge/Architecture-Enterprise_Grade-blue?style=for-the-badge&logo=blueprint&logoColor=white)](#)
[![Microservices](https://img.shields.io/badge/Microservices-50+-green?style=for-the-badge&logo=spring&logoColor=white)](#)
[![Components](https://img.shields.io/badge/Components-100+-orange?style=for-the-badge&logo=kubernetes&logoColor=white)](#)
[![Diagrams](https://img.shields.io/badge/Diagrams-10_Volumes-purple?style=for-the-badge&logo=mermaid&logoColor=white)](#)

> **Production-grade architecture for an Enterprise AI Platform featuring Hybrid RAG, Agentic AI (LangGraph), Spring Boot Microservices, Kubernetes, Kafka Event Sourcing, Multi-Tenant Security, and Full Observability.**

---

</div>

## 📋 Table of Contents

| Volume | Title | Focus Area |
|--------|-------|------------|
| [Volume 1](#volume-1--executive-architecture-level-0) | Executive Architecture (Level 0) | High-level system overview |
| [Volume 2](#volume-2--kubernetes--infrastructure) | Kubernetes & Infrastructure | Cluster topology, service mesh, observability infra |
| [Volume 3](#volume-3--spring-boot-microservice-architecture) | Spring Boot Microservice Architecture | 25+ microservices with REST + Kafka |
| [Volume 4](#volume-4--kafka-event-flow) | Kafka Event Flow | Document ingestion & query event streams |
| [Volume 5](#volume-5--hybrid-rag-pipeline) | Hybrid RAG Pipeline | End-to-end retrieval-augmented generation |
| [Volume 6](#volume-6--agentic-ai-platform-langgraph) | Agentic AI Platform (LangGraph) | Multi-agent orchestration with state graphs |
| [Volume 7](#volume-7--memory-architecture) | Memory Architecture | Short-term, semantic, episodic & long-term memory |
| [Volume 8](#volume-8--multi-tenant-security) | Multi-Tenant Security | OAuth, RBAC, ABAC, RLS, OPA, Vault |
| [Volume 9](#volume-9--monitoring--evaluation) | Monitoring & Evaluation | Prometheus, Grafana, RAGAS, DeepEval, LLM Judge |
| [Volume 10](#volume-10--cicd--mlops) | CI/CD & MLOps | GitHub Actions, ArgoCD, model versioning, A/B testing |

---

<br/>

<div align="center">

## Volume 1 — Executive Architecture (Level 0)

*High-level view of the entire Enterprise AI Platform*

</div>

```mermaid
---
title: "Volume 1 — Executive Architecture (Level 0)"
---
%%{init: {'theme': 'dark', 'themeVariables': { 'primaryColor': '#1a1a2e', 'primaryTextColor': '#e0e0e0', 'primaryBorderColor': '#4fc3f7', 'lineColor': '#4fc3f7', 'secondaryColor': '#16213e', 'tertiaryColor': '#0f3460', 'fontFamily': 'Inter, sans-serif'}}}%%

flowchart TB

    %% ============================================
    %% CLIENT LAYER
    %% ============================================

    subgraph CLIENTS["🌐 Client Layer"]
        direction LR
        WEB["🖥️ Web App<br/><i>React / Next.js</i>"]
        MOBILE["📱 Mobile App<br/><i>React Native / Flutter</i>"]
        SLACK_CLIENT["💬 Slack Bot<br/><i>Bolt SDK</i>"]
        TEAMS_CLIENT["🟦 Teams Bot<br/><i>Bot Framework</i>"]
        SDK["⚙️ REST / gRPC SDK<br/><i>Python / Java / Go</i>"]
        WEBHOOK["🔗 Webhook<br/><i>Inbound Events</i>"]
    end

    %% ============================================
    %% EDGE LAYER
    %% ============================================

    subgraph EDGE["🛡️ Edge Layer"]
        direction LR
        CDN["🌍 CDN<br/><i>CloudFront / Fastly</i>"]
        WAF["🔥 WAF<br/><i>AWS WAF / Cloudflare</i>"]
        DDOS["🛡️ DDoS Protection<br/><i>Shield Advanced</i>"]
    end

    %% ============================================
    %% API GATEWAY
    %% ============================================

    subgraph GATEWAY["🚪 API Gateway Layer"]
        direction LR
        KONG["🦍 API Gateway<br/><i>Kong / Spring Cloud Gateway</i>"]
        RATELIMIT["⏱️ Rate Limiter<br/><i>Token Bucket / Sliding Window</i>"]
        LOADBALANCE["⚖️ Load Balancer<br/><i>L7 / Weighted Round Robin</i>"]
        CIRCUIT["🔌 Circuit Breaker<br/><i>Resilience4j</i>"]
    end

    %% ============================================
    %% AUTH LAYER
    %% ============================================

    subgraph AUTHLAYER["🔐 Authentication & Authorization"]
        direction LR
        AUTH_SVC["🔑 Auth Service<br/><i>Keycloak / Auth0</i>"]
        JWT_VALID["📜 JWT Validator<br/><i>RS256 / ES256</i>"]
        RBAC_ENGINE["👤 RBAC Engine<br/><i>Role-Based Access</i>"]
        ABAC_ENGINE["🏷️ ABAC Engine<br/><i>Attribute-Based Access</i>"]
        TENANT_VALID["🏢 Tenant Validator<br/><i>Multi-Tenant Isolation</i>"]
    end

    %% ============================================
    %% CORE PLATFORM
    %% ============================================

    subgraph PLATFORM["🧠 Core AI Platform"]
        direction TB

        subgraph CONVERSATION["💬 Conversation Layer"]
            CONV_MGR["🗣️ Conversation Manager<br/><i>Session + Context</i>"]
            MEMORY["🧩 Memory System<br/><i>STM / LTM / Semantic</i>"]
        end

        subgraph ROUTING["🔀 Intelligent Routing"]
            GUARDRAIL_IN["🛡️ Input Guardrails<br/><i>Prompt Injection Detection</i>"]
            ROUTER["🔀 Conditional Router<br/><i>Intent Classification</i>"]
            SMALL_LLM["⚡ Small LLM<br/><i>Greetings / Simple QA</i>"]
            CALC_TOOL["🧮 Calculator Tool<br/><i>Math Queries</i>"]
            SQL_TOOL["🗃️ SQL Tool<br/><i>Database Queries</i>"]
        end

        subgraph AGENTIC["🤖 Agentic AI Engine"]
            PLANNER["📋 Planner<br/><i>Task Decomposition</i>"]
            TOOL_SELECT["🔧 Tool Selector<br/><i>Dynamic Routing</i>"]
            AGENT_COORD["🎯 Agent Coordinator<br/><i>Multi-Agent DAG</i>"]
            AGENTS["🤖 AI Agents<br/><i>Research / Finance / Email /<br/>Report / Risk / SQL</i>"]
        end

        subgraph RAG["📚 Hybrid RAG Engine"]
            META_FILTER["🏷️ Metadata Filter<br/><i>Tenant / ACL / Version</i>"]
            HYBRID_SEARCH["🔍 Hybrid Search<br/><i>BM25 + Vector</i>"]
            RERANKER["📊 Cross-Encoder Reranker<br/><i>Cohere / BGE / ColBERT</i>"]
            CONTEXT_COMP["📦 Context Compression<br/><i>LLMLingua / Selective</i>"]
            PROMPT_BUILD["📝 Prompt Builder<br/><i>Dynamic Template Engine</i>"]
            CITATION_GEN["📌 Citation Generator<br/><i>Source Attribution</i>"]
        end

        subgraph LLM_LAYER["🧠 LLM Layer"]
            LLM_GATEWAY["🌐 LLM Gateway<br/><i>Unified API</i>"]
            GPT["OpenAI<br/><i>GPT-4o / GPT-4 Turbo</i>"]
            CLAUDE["Anthropic<br/><i>Claude 3.5 Sonnet</i>"]
            GEMINI["Google<br/><i>Gemini 1.5 Pro</i>"]
            LLAMA["Meta<br/><i>Llama 3.1 70B</i>"]
            MISTRAL["Mistral<br/><i>Mixtral 8x22B</i>"]
        end

        subgraph SELFCORRECT["🔄 Self-Correcting Evaluation"]
            GROUND_CHECK["✅ Grounding Check"]
            FAITH_CHECK["🎯 Faithfulness"]
            HALLU_DETECT["🚨 Hallucination Detection"]
            QUERY_REWRITE["✏️ Query Rewrite"]
        end

        subgraph RISK_ENGINE["⚠️ Risk Engine"]
            RISK_CLASSIFY["🎲 Risk Classifier"]
            AUTO_EXEC["⚡ Auto Execute<br/><i>Low Risk</i>"]
            HUMAN_APPROVE["👨‍💼 Human Approval<br/><i>High Risk</i>"]
        end
    end

    %% ============================================
    %% ENTERPRISE TOOLS
    %% ============================================

    subgraph TOOLS["🔧 Enterprise Tool Integrations"]
        direction LR
        T_EMAIL["📧 Email<br/><i>SendGrid / SES</i>"]
        T_JIRA["📋 Jira<br/><i>Atlassian API</i>"]
        T_SLACK["💬 Slack<br/><i>Web API</i>"]
        T_SQL["🗃️ Database<br/><i>SQL Executor</i>"]
        T_AWS["☁️ AWS<br/><i>SDK / CLI</i>"]
        T_K8S["☸️ Kubernetes<br/><i>kubectl API</i>"]
        T_CRM["👥 CRM<br/><i>Salesforce / HubSpot</i>"]
        T_ERP["🏭 ERP<br/><i>SAP / Oracle</i>"]
        T_GITHUB["🐙 GitHub<br/><i>REST / GraphQL</i>"]
        T_CONFLUENCE["📖 Confluence<br/><i>Atlassian API</i>"]
    end

    %% ============================================
    %% DATA LAYER
    %% ============================================

    subgraph STORAGE["💾 Data Layer"]
        direction LR
        PG["🐘 PostgreSQL HA<br/><i>Primary + Read Replicas</i>"]
        REDIS_STORE["⚡ Redis Cluster<br/><i>Cache + Sessions</i>"]
        VECTOR_DB["🧬 Vector Database<br/><i>Qdrant / Milvus / Pinecone</i>"]
        ELASTIC["🔍 Elasticsearch<br/><i>Full-Text Index</i>"]
        S3_STORE["📦 Object Storage<br/><i>S3 / MinIO</i>"]
        KAFKA_STORE["📨 Kafka Cluster<br/><i>Event Streaming</i>"]
    end

    %% ============================================
    %% INGESTION PIPELINE
    %% ============================================

    subgraph INGESTION["📥 Document Ingestion Pipeline"]
        direction LR
        DOC_UPLOAD["📄 Document Upload<br/><i>PDF / DOCX / PPT / XLSX</i>"]
        DOC_PARSE["🔧 Document Parser<br/><i>Apache Tika / Unstructured</i>"]
        DOC_OCR["👁️ OCR Engine<br/><i>Tesseract / AWS Textract</i>"]
        DOC_STRUCTURE["🏗️ Structure Detection<br/><i>Tables / Headers / Lists</i>"]
        DOC_CHUNK["✂️ Semantic Chunking<br/><i>Recursive / Sentence / Agentic</i>"]
        DOC_EMBED["🧬 Embedding Model<br/><i>text-embedding-3-large /<br/>BGE-M3 / E5</i>"]
        DOC_INDEX["📇 Index Builder<br/><i>Multi-Index Write</i>"]
    end

    %% ============================================
    %% OBSERVABILITY
    %% ============================================

    subgraph OBSERVE["📊 Observability & Evaluation"]
        direction LR
        OBS_METRICS["📈 Metrics<br/><i>Prometheus</i>"]
        OBS_LOGS["📝 Logs<br/><i>Loki / ELK</i>"]
        OBS_TRACE["🔗 Traces<br/><i>Jaeger / Tempo</i>"]
        OBS_DASH["📊 Dashboards<br/><i>Grafana</i>"]
        EVAL_ENGINE["🎯 Evaluation Engine<br/><i>RAGAS / DeepEval / TruLens</i>"]
        LLM_JUDGE["⚖️ LLM Judge<br/><i>GPT-4 Evaluator</i>"]
        AUDIT_LOG["📋 Audit Trail<br/><i>Immutable Logs</i>"]
    end

    %% ============================================
    %% SECURITY
    %% ============================================

    subgraph SECURITY["🔒 Security Layer"]
        direction LR
        SEC_INJECT["💉 Prompt Injection<br/><i>Detection</i>"]
        SEC_JAIL["🔓 Jailbreak<br/><i>Detection</i>"]
        SEC_LEAK["🕵️ Info Leakage<br/><i>Prevention</i>"]
        SEC_BIAS["⚖️ Bias Testing<br/><i>Fairness Checks</i>"]
        SEC_PII["🔐 PII Redaction<br/><i>Presidio / Phileas</i>"]
        SEC_GUARDRAILS["🛡️ Guardrails<br/><i>NeMo / Guardrails AI</i>"]
    end

    %% ============================================
    %% CONNECTIONS
    %% ============================================

    CLIENTS --> EDGE
    EDGE --> GATEWAY
    GATEWAY --> AUTHLAYER
    AUTHLAYER --> PLATFORM
    PLATFORM --> TOOLS
    PLATFORM --> STORAGE
    INGESTION --> STORAGE
    PLATFORM --> OBSERVE
    SECURITY --> PLATFORM

    %% ============================================
    %% STYLES
    %% ============================================

    classDef clientStyle fill:#1e3a5f,stroke:#4fc3f7,stroke-width:2px,color:#e0e0e0
    classDef edgeStyle fill:#1a237e,stroke:#7c4dff,stroke-width:2px,color:#e0e0e0
    classDef gatewayStyle fill:#004d40,stroke:#00e5ff,stroke-width:2px,color:#e0e0e0
    classDef authStyle fill:#4a148c,stroke:#ea80fc,stroke-width:2px,color:#e0e0e0
    classDef platformStyle fill:#1b1b2f,stroke:#e94560,stroke-width:2px,color:#e0e0e0
    classDef toolStyle fill:#33691e,stroke:#76ff03,stroke-width:2px,color:#e0e0e0
    classDef storageStyle fill:#bf360c,stroke:#ff6e40,stroke-width:2px,color:#e0e0e0
    classDef ingestStyle fill:#006064,stroke:#00e5ff,stroke-width:2px,color:#e0e0e0
    classDef observeStyle fill:#263238,stroke:#80cbc4,stroke-width:2px,color:#e0e0e0
    classDef securityStyle fill:#880e4f,stroke:#f50057,stroke-width:2px,color:#e0e0e0

    class WEB,MOBILE,SLACK_CLIENT,TEAMS_CLIENT,SDK,WEBHOOK clientStyle
    class CDN,WAF,DDOS edgeStyle
    class KONG,RATELIMIT,LOADBALANCE,CIRCUIT gatewayStyle
    class AUTH_SVC,JWT_VALID,RBAC_ENGINE,ABAC_ENGINE,TENANT_VALID authStyle
    class CONV_MGR,MEMORY,GUARDRAIL_IN,ROUTER,SMALL_LLM,CALC_TOOL,SQL_TOOL platformStyle
    class PLANNER,TOOL_SELECT,AGENT_COORD,AGENTS platformStyle
    class META_FILTER,HYBRID_SEARCH,RERANKER,CONTEXT_COMP,PROMPT_BUILD,CITATION_GEN platformStyle
    class LLM_GATEWAY,GPT,CLAUDE,GEMINI,LLAMA,MISTRAL platformStyle
    class GROUND_CHECK,FAITH_CHECK,HALLU_DETECT,QUERY_REWRITE platformStyle
    class RISK_CLASSIFY,AUTO_EXEC,HUMAN_APPROVE platformStyle
    class T_EMAIL,T_JIRA,T_SLACK,T_SQL,T_AWS,T_K8S,T_CRM,T_ERP,T_GITHUB,T_CONFLUENCE toolStyle
    class PG,REDIS_STORE,VECTOR_DB,ELASTIC,S3_STORE,KAFKA_STORE storageStyle
    class DOC_UPLOAD,DOC_PARSE,DOC_OCR,DOC_STRUCTURE,DOC_CHUNK,DOC_EMBED,DOC_INDEX ingestStyle
    class OBS_METRICS,OBS_LOGS,OBS_TRACE,OBS_DASH,EVAL_ENGINE,LLM_JUDGE,AUDIT_LOG observeStyle
    class SEC_INJECT,SEC_JAIL,SEC_LEAK,SEC_BIAS,SEC_PII,SEC_GUARDRAILS securityStyle
```

---

<br/>

<div align="center">

## Volume 2 — Kubernetes & Infrastructure

*Production Kubernetes cluster topology, service mesh, and infrastructure components*

</div>

```mermaid
---
title: "Volume 2 — Kubernetes & Infrastructure"
---
%%{init: {'theme': 'dark', 'themeVariables': { 'primaryColor': '#1a1a2e', 'primaryTextColor': '#e0e0e0', 'primaryBorderColor': '#00bcd4', 'lineColor': '#00bcd4', 'secondaryColor': '#16213e', 'tertiaryColor': '#0f3460', 'fontFamily': 'Inter, sans-serif'}}}%%

flowchart TB

    %% ============================================
    %% EXTERNAL TRAFFIC
    %% ============================================

    INTERNET["🌐 Internet<br/><i>External Traffic</i>"]
    DNS["🌍 Route53 / CloudDNS<br/><i>DNS Resolution</i>"]
    CERTMGR["🔒 Cert Manager<br/><i>Let's Encrypt / ACM</i>"]

    INTERNET --> DNS
    DNS --> CERTMGR

    %% ============================================
    %% KUBERNETES CLUSTER
    %% ============================================

    subgraph K8S_CLUSTER["☸️ Kubernetes Cluster (EKS / GKE / AKS)"]
        direction TB

        %% ---- INGRESS ----
        subgraph INGRESS_NS["📥 Ingress Namespace"]
            direction LR
            NGINX_ING["🔀 Nginx Ingress Controller<br/><i>TLS Termination</i>"]
            RATE_LIMIT_ING["⏱️ Rate Limiting<br/><i>Global Rate Limits</i>"]
            CORS_ING["🔗 CORS Handler<br/><i>Cross-Origin Policies</i>"]
        end

        %% ---- SERVICE MESH ----
        subgraph MESH_NS["🕸️ Service Mesh (Istio)"]
            direction LR
            ISTIOD["🧭 Istiod<br/><i>Control Plane</i>"]
            ENVOY["📡 Envoy Sidecar Proxies<br/><i>mTLS / Traffic Mgmt</i>"]
            VIRTUAL_SVC["🔀 Virtual Services<br/><i>Traffic Routing Rules</i>"]
            DEST_RULES["📋 Destination Rules<br/><i>Load Balancing Policies</i>"]
            PEER_AUTH["🔐 PeerAuthentication<br/><i>mTLS Strict Mode</i>"]
            AUTH_POLICY["📜 Authorization Policies<br/><i>L7 Access Control</i>"]
        end

        %% ---- API GATEWAY NAMESPACE ----
        subgraph GW_NS["🚪 Gateway Namespace"]
            direction LR
            SPRING_GW["🌱 Spring Cloud Gateway<br/><i>API Routing</i><br/>Replicas: 3"]
            KONG_GW["🦍 Kong Gateway<br/><i>Plugin Ecosystem</i><br/>Replicas: 3"]
        end

        %% ---- SERVICE DISCOVERY ----
        subgraph DISCOVERY_NS["🔍 Service Discovery"]
            direction LR
            EUREKA["📡 Eureka Server<br/><i>Service Registry</i><br/>Replicas: 3"]
            CONFIG_SVR["⚙️ Config Server<br/><i>Spring Cloud Config</i><br/>Replicas: 2"]
            CONSUL["🏛️ Consul<br/><i>Service Mesh + KV Store</i>"]
        end

        %% ---- APPLICATION NAMESPACE ----
        subgraph APP_NS["🧠 Application Namespace"]
            direction TB

            subgraph AUTH_PODS["🔐 Auth Pods"]
                AUTH_DEPLOY["Auth Service<br/><i>Deployment</i><br/>Replicas: 3<br/>CPU: 500m / Mem: 512Mi"]
            end

            subgraph CORE_PODS["🏗️ Core AI Pods"]
                CONV_DEPLOY["Conversation Service<br/><i>Deployment</i><br/>Replicas: 5<br/>CPU: 1 / Mem: 1Gi"]
                PLANNER_DEPLOY["Planner Service<br/><i>Deployment</i><br/>Replicas: 3<br/>CPU: 2 / Mem: 2Gi"]
                AGENT_DEPLOY["Agent Service<br/><i>Deployment</i><br/>Replicas: 5<br/>CPU: 2 / Mem: 4Gi"]
                RETRIEVAL_DEPLOY["Retrieval Service<br/><i>Deployment</i><br/>Replicas: 5<br/>CPU: 1 / Mem: 2Gi"]
                RERANK_DEPLOY["Reranker Service<br/><i>Deployment</i><br/>Replicas: 3<br/>CPU: 4 / Mem: 8Gi<br/><i>GPU: 1x T4</i>"]
            end

            subgraph LLM_PODS["🧠 LLM Gateway Pods"]
                LLM_GW_DEPLOY["LLM Gateway<br/><i>Deployment</i><br/>Replicas: 5<br/>CPU: 1 / Mem: 2Gi"]
            end

            subgraph INGESTION_PODS["📥 Ingestion Pods"]
                EMBED_DEPLOY["Embedding Service<br/><i>Deployment</i><br/>Replicas: 3<br/>CPU: 4 / Mem: 8Gi<br/><i>GPU: 1x A10</i>"]
                CHUNK_DEPLOY["Chunking Service<br/><i>Deployment</i><br/>Replicas: 3<br/>CPU: 1 / Mem: 2Gi"]
                PARSE_DEPLOY["Parser Service<br/><i>Deployment</i><br/>Replicas: 3<br/>CPU: 2 / Mem: 4Gi"]
            end

            subgraph EVAL_PODS["📊 Evaluation Pods"]
                EVAL_DEPLOY["Evaluation Service<br/><i>Deployment</i><br/>Replicas: 2<br/>CPU: 1 / Mem: 2Gi"]
                AUDIT_DEPLOY["Audit Service<br/><i>Deployment</i><br/>Replicas: 2<br/>CPU: 500m / Mem: 512Mi"]
            end
        end

        %% ---- AUTOSCALING ----
        subgraph HPA_NS["📈 Autoscaling"]
            direction LR
            HPA["⚖️ Horizontal Pod Autoscaler<br/><i>CPU / Memory / Custom Metrics</i>"]
            VPA["📊 Vertical Pod Autoscaler<br/><i>Resource Recommendations</i>"]
            KEDA["⚡ KEDA<br/><i>Event-Driven Autoscaling<br/>Kafka Consumer Lag</i>"]
            CLUSTER_AUTO["☁️ Cluster Autoscaler<br/><i>Node Pool Scaling</i>"]
        end

        %% ---- SECRETS ----
        subgraph SECRETS_NS["🔐 Secrets Management"]
            direction LR
            K8S_SECRETS["🗝️ Kubernetes Secrets<br/><i>Encrypted at Rest</i>"]
            VAULT["🏦 HashiCorp Vault<br/><i>Dynamic Secrets</i>"]
            EXTERNAL_SECRETS["🔄 External Secrets Operator<br/><i>AWS Secrets Manager Sync</i>"]
            SEALED_SECRETS["🔒 Sealed Secrets<br/><i>GitOps Compatible</i>"]
        end

        %% ---- DATA NAMESPACE ----
        subgraph DATA_NS["💾 Data Namespace"]
            direction TB

            subgraph PG_CLUSTER["🐘 PostgreSQL HA"]
                PG_PRIMARY["Primary<br/><i>Write Node</i><br/>PVC: 500Gi"]
                PG_REPLICA1["Replica 1<br/><i>Read Node</i><br/>PVC: 500Gi"]
                PG_REPLICA2["Replica 2<br/><i>Read Node</i><br/>PVC: 500Gi"]
                PG_PGBOUNCER["PgBouncer<br/><i>Connection Pooler</i>"]
            end

            subgraph REDIS_CLUSTER["⚡ Redis Cluster"]
                REDIS_M1["Master 1<br/><i>Shard 1</i>"]
                REDIS_M2["Master 2<br/><i>Shard 2</i>"]
                REDIS_M3["Master 3<br/><i>Shard 3</i>"]
                REDIS_SENTINEL["Sentinel<br/><i>HA Manager</i>"]
            end

            subgraph ES_CLUSTER["🔍 Elasticsearch Cluster"]
                ES_MASTER["Master Nodes<br/><i>x3</i>"]
                ES_DATA["Data Nodes<br/><i>x5</i><br/>PVC: 1Ti each"]
                ES_COORD["Coordinating Nodes<br/><i>x2</i>"]
            end

            subgraph VECTOR_CLUSTER["🧬 Vector DB Cluster"]
                QDRANT_LEADER["Qdrant Leader<br/><i>Write Path</i>"]
                QDRANT_FOLLOWER1["Qdrant Follower 1<br/><i>Read Path</i>"]
                QDRANT_FOLLOWER2["Qdrant Follower 2<br/><i>Read Path</i>"]
            end

            subgraph KAFKA_CLUSTER["📨 Kafka Cluster"]
                KAFKA_B1["Broker 1<br/><i>Partition Leader</i>"]
                KAFKA_B2["Broker 2<br/><i>ISR</i>"]
                KAFKA_B3["Broker 3<br/><i>ISR</i>"]
                ZOOKEEPER["ZooKeeper<br/><i>Cluster Coordination</i>"]
                SCHEMA_REG["Schema Registry<br/><i>Avro / Protobuf</i>"]
            end
        end

        %% ---- OBSERVABILITY NAMESPACE ----
        subgraph OBS_NS["📊 Observability Namespace"]
            direction LR
            PROMETHEUS["📈 Prometheus<br/><i>Metrics Collection</i><br/>PVC: 200Gi"]
            GRAFANA["📊 Grafana<br/><i>Dashboards</i>"]
            LOKI["📝 Loki<br/><i>Log Aggregation</i>"]
            TEMPO["🔗 Tempo<br/><i>Distributed Tracing</i>"]
            JAEGER["🔍 Jaeger<br/><i>Trace Visualization</i>"]
            OTEL_COLLECTOR["📡 OpenTelemetry Collector<br/><i>Unified Pipeline</i>"]
            ALERTMANAGER["🚨 Alertmanager<br/><i>PagerDuty / Slack</i>"]
        end
    end

    %% ============================================
    %% EXTERNAL SERVICES
    %% ============================================

    subgraph EXTERNAL["☁️ External Cloud Services"]
        direction LR
        S3_EXT["📦 S3 / MinIO<br/><i>Object Storage</i>"]
        SES_EXT["📧 SES / SendGrid<br/><i>Email Service</i>"]
        LLM_APIS["🧠 LLM APIs<br/><i>OpenAI / Anthropic / Google</i>"]
        SENTRY["🐛 Sentry<br/><i>Error Tracking</i>"]
    end

    %% ============================================
    %% CI/CD
    %% ============================================

    subgraph CICD["🔄 CI/CD Pipeline"]
        direction LR
        GITHUB_REPO["🐙 GitHub<br/><i>Source Code</i>"]
        GH_ACTIONS["⚙️ GitHub Actions<br/><i>CI Pipeline</i>"]
        ECR["📦 ECR / GCR<br/><i>Container Registry</i>"]
        ARGOCD["🔄 ArgoCD<br/><i>GitOps Deployment</i>"]
    end

    %% ============================================
    %% CONNECTIONS
    %% ============================================

    CERTMGR --> NGINX_ING
    NGINX_ING --> RATE_LIMIT_ING
    RATE_LIMIT_ING --> CORS_ING
    CORS_ING --> SPRING_GW
    CORS_ING --> KONG_GW

    SPRING_GW --> ENVOY
    KONG_GW --> ENVOY

    ENVOY --> AUTH_DEPLOY
    ENVOY --> CONV_DEPLOY
    ENVOY --> PLANNER_DEPLOY
    ENVOY --> AGENT_DEPLOY
    ENVOY --> RETRIEVAL_DEPLOY
    ENVOY --> RERANK_DEPLOY
    ENVOY --> LLM_GW_DEPLOY
    ENVOY --> EMBED_DEPLOY
    ENVOY --> CHUNK_DEPLOY
    ENVOY --> PARSE_DEPLOY
    ENVOY --> EVAL_DEPLOY
    ENVOY --> AUDIT_DEPLOY

    AUTH_DEPLOY --> EUREKA
    CONV_DEPLOY --> EUREKA
    PLANNER_DEPLOY --> EUREKA

    CONFIG_SVR --> AUTH_DEPLOY
    CONFIG_SVR --> CONV_DEPLOY
    CONFIG_SVR --> PLANNER_DEPLOY

    HPA --> CONV_DEPLOY
    HPA --> AGENT_DEPLOY
    HPA --> RETRIEVAL_DEPLOY
    KEDA --> EMBED_DEPLOY
    KEDA --> CHUNK_DEPLOY
    CLUSTER_AUTO --> K8S_CLUSTER

    VAULT --> K8S_SECRETS
    EXTERNAL_SECRETS --> K8S_SECRETS

    PG_PGBOUNCER --> PG_PRIMARY
    PG_PRIMARY --> PG_REPLICA1
    PG_PRIMARY --> PG_REPLICA2

    REDIS_SENTINEL --> REDIS_M1
    REDIS_SENTINEL --> REDIS_M2
    REDIS_SENTINEL --> REDIS_M3

    ES_COORD --> ES_DATA
    ES_MASTER --> ES_DATA

    KAFKA_B1 --> ZOOKEEPER
    KAFKA_B2 --> ZOOKEEPER
    KAFKA_B3 --> ZOOKEEPER
    SCHEMA_REG --> KAFKA_B1

    OTEL_COLLECTOR --> PROMETHEUS
    OTEL_COLLECTOR --> LOKI
    OTEL_COLLECTOR --> TEMPO
    PROMETHEUS --> GRAFANA
    LOKI --> GRAFANA
    TEMPO --> JAEGER
    PROMETHEUS --> ALERTMANAGER

    LLM_GW_DEPLOY --> LLM_APIS
    AUDIT_DEPLOY --> S3_EXT

    GITHUB_REPO --> GH_ACTIONS
    GH_ACTIONS --> ECR
    ECR --> ARGOCD
    ARGOCD --> K8S_CLUSTER

    %% ============================================
    %% STYLES
    %% ============================================

    classDef ingressStyle fill:#0d47a1,stroke:#42a5f5,stroke-width:2px,color:#e0e0e0
    classDef meshStyle fill:#1a237e,stroke:#7c4dff,stroke-width:2px,color:#e0e0e0
    classDef gwStyle fill:#004d40,stroke:#00e5ff,stroke-width:2px,color:#e0e0e0
    classDef appStyle fill:#1b1b2f,stroke:#e94560,stroke-width:2px,color:#e0e0e0
    classDef dataStyle fill:#bf360c,stroke:#ff6e40,stroke-width:2px,color:#e0e0e0
    classDef obsStyle fill:#263238,stroke:#80cbc4,stroke-width:2px,color:#e0e0e0
    classDef cicdStyle fill:#33691e,stroke:#76ff03,stroke-width:2px,color:#e0e0e0
    classDef extStyle fill:#311b92,stroke:#b388ff,stroke-width:2px,color:#e0e0e0
    classDef scaleStyle fill:#e65100,stroke:#ff9100,stroke-width:2px,color:#e0e0e0
    classDef secretStyle fill:#880e4f,stroke:#f50057,stroke-width:2px,color:#e0e0e0

    class NGINX_ING,RATE_LIMIT_ING,CORS_ING ingressStyle
    class ISTIOD,ENVOY,VIRTUAL_SVC,DEST_RULES,PEER_AUTH,AUTH_POLICY meshStyle
    class SPRING_GW,KONG_GW gwStyle
    class EUREKA,CONFIG_SVR,CONSUL gwStyle
    class AUTH_DEPLOY appStyle
    class CONV_DEPLOY,PLANNER_DEPLOY,AGENT_DEPLOY,RETRIEVAL_DEPLOY,RERANK_DEPLOY appStyle
    class LLM_GW_DEPLOY appStyle
    class EMBED_DEPLOY,CHUNK_DEPLOY,PARSE_DEPLOY appStyle
    class EVAL_DEPLOY,AUDIT_DEPLOY appStyle
    class PG_PRIMARY,PG_REPLICA1,PG_REPLICA2,PG_PGBOUNCER dataStyle
    class REDIS_M1,REDIS_M2,REDIS_M3,REDIS_SENTINEL dataStyle
    class ES_MASTER,ES_DATA,ES_COORD dataStyle
    class QDRANT_LEADER,QDRANT_FOLLOWER1,QDRANT_FOLLOWER2 dataStyle
    class KAFKA_B1,KAFKA_B2,KAFKA_B3,ZOOKEEPER,SCHEMA_REG dataStyle
    class PROMETHEUS,GRAFANA,LOKI,TEMPO,JAEGER,OTEL_COLLECTOR,ALERTMANAGER obsStyle
    class HPA,VPA,KEDA,CLUSTER_AUTO scaleStyle
    class K8S_SECRETS,VAULT,EXTERNAL_SECRETS,SEALED_SECRETS secretStyle
    class GITHUB_REPO,GH_ACTIONS,ECR,ARGOCD cicdStyle
    class S3_EXT,SES_EXT,LLM_APIS,SENTRY extStyle
    class INTERNET,DNS,CERTMGR ingressStyle
```

---

<br/>

<div align="center">

## Volume 3 — Spring Boot Microservice Architecture

*25+ Spring Boot microservices with REST and Kafka event communication*

</div>

```mermaid
---
title: "Volume 3 — Spring Boot Microservice Architecture"
---
%%{init: {'theme': 'dark', 'themeVariables': { 'primaryColor': '#1a1a2e', 'primaryTextColor': '#e0e0e0', 'primaryBorderColor': '#66bb6a', 'lineColor': '#66bb6a', 'secondaryColor': '#16213e', 'tertiaryColor': '#0f3460', 'fontFamily': 'Inter, sans-serif'}}}%%

flowchart TB

    %% ============================================
    %% SPRING CLOUD INFRASTRUCTURE
    %% ============================================

    subgraph SPRING_INFRA["🌱 Spring Cloud Infrastructure"]
        direction LR
        CONFIG["⚙️ Config Server<br/><i>Spring Cloud Config<br/>Git-backed / Vault</i>"]
        EUREKA_SVR["📡 Eureka Server<br/><i>Service Registry<br/>Heartbeat: 30s</i>"]
        GATEWAY["🚪 API Gateway<br/><i>Spring Cloud Gateway<br/>Route Predicates + Filters</i>"]
        ADMIN["🖥️ Spring Boot Admin<br/><i>Health + Metrics Dashboard</i>"]
    end

    %% ============================================
    %% AUTH & TENANT SERVICES
    %% ============================================

    subgraph AUTH_SERVICES["🔐 Auth & Tenant Services"]
        direction TB

        AUTH_SVC["🔑 Auth Service<br/><i>POST /api/v1/auth/login<br/>POST /api/v1/auth/refresh<br/>POST /api/v1/auth/logout<br/>POST /api/v1/auth/sso<br/>—<br/>Keycloak Integration<br/>JWT RS256 Signing<br/>MFA Support</i>"]

        USER_SVC["👤 User Service<br/><i>GET /api/v1/users<br/>POST /api/v1/users<br/>PUT /api/v1/users/:id<br/>GET /api/v1/users/:id/roles<br/>—<br/>Profile Management<br/>Role Assignment<br/>Preferences</i>"]

        TENANT_SVC["🏢 Tenant Service<br/><i>POST /api/v1/tenants<br/>GET /api/v1/tenants/:id<br/>PUT /api/v1/tenants/:id/config<br/>GET /api/v1/tenants/:id/usage<br/>—<br/>Tenant Provisioning<br/>Quota Management<br/>Feature Flags</i>"]

        POLICY_SVC["📜 Policy Service<br/><i>POST /api/v1/policies<br/>GET /api/v1/policies/evaluate<br/>PUT /api/v1/policies/:id<br/>—<br/>OPA Integration<br/>RBAC + ABAC Rules<br/>Document ACL</i>"]
    end

    %% ============================================
    %% CONVERSATION & MEMORY SERVICES
    %% ============================================

    subgraph CONV_SERVICES["💬 Conversation & Memory"]
        direction TB

        CONV_SVC["🗣️ Conversation Service<br/><i>POST /api/v1/conversations<br/>GET /api/v1/conversations/:id<br/>POST /api/v1/conversations/:id/messages<br/>GET /api/v1/conversations/:id/history<br/>DELETE /api/v1/conversations/:id<br/>—<br/>Session Management<br/>Context Window<br/>Streaming SSE</i>"]

        MEMORY_SVC["🧩 Memory Service<br/><i>POST /api/v1/memory/store<br/>GET /api/v1/memory/recall<br/>POST /api/v1/memory/consolidate<br/>DELETE /api/v1/memory/forget<br/>—<br/>STM Redis Cache<br/>LTM PostgreSQL<br/>Semantic Vector Memory<br/>Episodic Memory</i>"]

        PROMPT_SVC["📝 Prompt Service<br/><i>POST /api/v1/prompts/build<br/>GET /api/v1/prompts/templates<br/>PUT /api/v1/prompts/templates/:id<br/>POST /api/v1/prompts/version<br/>—<br/>Template Engine<br/>Variable Injection<br/>Prompt Versioning<br/>A/B Testing</i>"]
    end

    %% ============================================
    %% RAG SERVICES
    %% ============================================

    subgraph RAG_SERVICES["📚 RAG Pipeline Services"]
        direction TB

        RETRIEVAL_SVC["🔍 Retrieval Service<br/><i>POST /api/v1/retrieve<br/>POST /api/v1/retrieve/hybrid<br/>GET /api/v1/retrieve/metadata-filter<br/>—<br/>BM25 + Vector Fusion<br/>Metadata Pre-filter<br/>Tenant Isolation<br/>ACL Enforcement</i>"]

        SEARCH_SVC["🔎 Search Service<br/><i>POST /api/v1/search/fulltext<br/>POST /api/v1/search/semantic<br/>POST /api/v1/search/hybrid<br/>—<br/>Elasticsearch BM25<br/>Qdrant ANN Search<br/>RRF Merge Strategy</i>"]

        RERANK_SVC["📊 Reranking Service<br/><i>POST /api/v1/rerank<br/>—<br/>Cross-Encoder Model<br/>Cohere Rerank API<br/>BGE Reranker<br/>ColBERTv2<br/>Top-K Selection</i>"]

        CITATION_SVC["📌 Citation Service<br/><i>POST /api/v1/citations/generate<br/>GET /api/v1/citations/:id<br/>—<br/>Source Attribution<br/>Chunk-to-Document Mapping<br/>Confidence Scores</i>"]
    end

    %% ============================================
    %% INGESTION SERVICES
    %% ============================================

    subgraph INGEST_SERVICES["📥 Document Ingestion Services"]
        direction TB

        UPLOAD_SVC["📄 Upload Service<br/><i>POST /api/v1/documents/upload<br/>POST /api/v1/documents/bulk-upload<br/>GET /api/v1/documents/:id/status<br/>—<br/>Multi-part Upload<br/>S3 Pre-signed URLs<br/>File Validation<br/>Virus Scanning</i>"]

        PARSER_SVC["🔧 Parser Service<br/><i>Kafka Consumer<br/>—<br/>Apache Tika Integration<br/>Unstructured.io<br/>PDF / DOCX / PPT / XLSX<br/>Table Extraction<br/>Image Extraction</i>"]

        OCR_SVC["👁️ OCR Service<br/><i>Kafka Consumer<br/>—<br/>Tesseract OCR<br/>AWS Textract<br/>Azure Document Intelligence<br/>Handwriting Recognition</i>"]

        CHUNKING_SVC["✂️ Chunking Service<br/><i>Kafka Consumer<br/>—<br/>Recursive Character Splitting<br/>Sentence-based Chunking<br/>Semantic Chunking<br/>Agentic Chunking<br/>Overlap: 200 tokens</i>"]

        EMBEDDING_SVC["🧬 Embedding Service<br/><i>POST /api/v1/embeddings/generate<br/>Kafka Consumer<br/>—<br/>text-embedding-3-large<br/>BGE-M3<br/>E5-Mistral<br/>Batch Processing<br/>GPU Accelerated</i>"]

        METADATA_SVC["🏷️ Metadata Service<br/><i>Kafka Consumer<br/>—<br/>Auto-tagging<br/>Entity Extraction<br/>Language Detection<br/>Department Classification<br/>Version Tracking</i>"]

        INDEX_SVC["📇 Index Service<br/><i>Kafka Consumer<br/>—<br/>Vector DB Write<br/>Elasticsearch Write<br/>PostgreSQL Write<br/>Multi-Index Consistency</i>"]
    end

    %% ============================================
    %% AI ENGINE SERVICES
    %% ============================================

    subgraph AI_SERVICES["🧠 AI Engine Services"]
        direction TB

        LLM_GATEWAY_SVC["🌐 LLM Gateway Service<br/><i>POST /api/v1/llm/complete<br/>POST /api/v1/llm/stream<br/>POST /api/v1/llm/batch<br/>—<br/>Multi-Provider Router<br/>OpenAI / Anthropic / Google / Meta<br/>Fallback Chain<br/>Token Counting<br/>Cost Tracking<br/>Response Caching</i>"]

        PLANNER_SVC["📋 Planner Service<br/><i>POST /api/v1/plan<br/>GET /api/v1/plan/:id/status<br/>—<br/>Task Decomposition<br/>Dependency Graph<br/>Tool Selection<br/>Complexity Estimation</i>"]

        AGENT_SVC["🤖 Agent Service<br/><i>POST /api/v1/agents/execute<br/>GET /api/v1/agents/:id/status<br/>POST /api/v1/agents/coordinate<br/>—<br/>LangGraph Integration<br/>State Machine<br/>Research Agent<br/>Finance Agent<br/>Email Agent<br/>Report Agent<br/>SQL Agent<br/>Risk Agent</i>"]

        GUARDRAIL_SVC["🛡️ Guardrail Service<br/><i>POST /api/v1/guardrails/check<br/>—<br/>Prompt Injection Detection<br/>Jailbreak Detection<br/>PII Redaction<br/>Content Moderation<br/>NeMo Guardrails</i>"]
    end

    %% ============================================
    %% EVALUATION & AUDIT SERVICES
    %% ============================================

    subgraph EVAL_SERVICES["📊 Evaluation & Audit"]
        direction TB

        EVAL_SVC["🎯 Evaluation Service<br/><i>POST /api/v1/evaluate<br/>GET /api/v1/evaluate/reports<br/>—<br/>RAGAS Metrics<br/>DeepEval<br/>TruLens<br/>Faithfulness Score<br/>Relevance Score<br/>Hallucination Rate</i>"]

        AUDIT_SVC["📋 Audit Service<br/><i>Kafka Consumer<br/>GET /api/v1/audit/logs<br/>GET /api/v1/audit/trails/:id<br/>—<br/>Immutable Audit Trail<br/>Event Sourcing<br/>Compliance Reporting<br/>GDPR Data Requests</i>"]

        FEEDBACK_SVC["👍 Feedback Service<br/><i>POST /api/v1/feedback<br/>GET /api/v1/feedback/analytics<br/>—<br/>User Ratings<br/>Thumbs Up/Down<br/>Free-text Comments<br/>RLHF Signal</i>"]

        ANALYTICS_SVC["📈 Analytics Service<br/><i>GET /api/v1/analytics/usage<br/>GET /api/v1/analytics/costs<br/>GET /api/v1/analytics/performance<br/>—<br/>Token Usage Trends<br/>Cost per Query<br/>Latency Percentiles<br/>User Engagement</i>"]
    end

    %% ============================================
    %% OPERATIONS SERVICES
    %% ============================================

    subgraph OPS_SERVICES["⚙️ Operations Services"]
        direction TB

        NOTIFICATION_SVC["🔔 Notification Service<br/><i>Kafka Consumer<br/>—<br/>Email / Slack / Teams<br/>Push Notifications<br/>Webhook Delivery<br/>Template Engine</i>"]

        SCHEDULER_SVC["⏰ Scheduler Service<br/><i>POST /api/v1/schedules<br/>GET /api/v1/schedules<br/>—<br/>Cron Jobs<br/>Retry Policies<br/>Dead Letter Queue<br/>Quartz Integration</i>"]

        WORKFLOW_SVC["🔄 Workflow Service<br/><i>POST /api/v1/workflows<br/>GET /api/v1/workflows/:id/status<br/>—<br/>Multi-step Orchestration<br/>Approval Chains<br/>State Management<br/>Temporal Integration</i>"]

        BILLING_SVC["💰 Billing Service<br/><i>GET /api/v1/billing/usage<br/>GET /api/v1/billing/invoices<br/>POST /api/v1/billing/quotas<br/>—<br/>Token Metering<br/>Tiered Pricing<br/>Invoice Generation<br/>Stripe Integration</i>"]

        ADMIN_SVC["🖥️ Admin Service<br/><i>GET /api/v1/admin/dashboard<br/>POST /api/v1/admin/config<br/>GET /api/v1/admin/health<br/>—<br/>System Configuration<br/>Feature Toggles<br/>User Management<br/>Tenant Onboarding</i>"]
    end

    %% ============================================
    %% KAFKA EVENT BUS
    %% ============================================

    KAFKA_BUS{{"📨 Kafka Event Bus<br/><i>Async Communication</i>"}}

    %% ============================================
    %% DATA STORES
    %% ============================================

    subgraph DATASTORES["💾 Data Stores"]
        direction LR
        PG_DB[("🐘 PostgreSQL<br/><i>Primary Data Store</i>")]
        REDIS_DB[("⚡ Redis<br/><i>Cache + Sessions</i>")]
        VECTOR_STORE[("🧬 Qdrant<br/><i>Vector Embeddings</i>")]
        ES_DB[("🔍 Elasticsearch<br/><i>Full-Text Search</i>")]
        S3_DB[("📦 S3<br/><i>Object Storage</i>")]
    end

    %% ============================================
    %% REST CONNECTIONS (Synchronous)
    %% ============================================

    GATEWAY --> AUTH_SVC
    GATEWAY --> USER_SVC
    GATEWAY --> TENANT_SVC
    GATEWAY --> CONV_SVC
    GATEWAY --> RETRIEVAL_SVC
    GATEWAY --> UPLOAD_SVC
    GATEWAY --> LLM_GATEWAY_SVC
    GATEWAY --> PLANNER_SVC
    GATEWAY --> AGENT_SVC
    GATEWAY --> ADMIN_SVC
    GATEWAY --> ANALYTICS_SVC

    AUTH_SVC --> EUREKA_SVR
    USER_SVC --> EUREKA_SVR
    CONV_SVC --> EUREKA_SVR
    RETRIEVAL_SVC --> EUREKA_SVR
    LLM_GATEWAY_SVC --> EUREKA_SVR

    CONFIG --> AUTH_SVC
    CONFIG --> CONV_SVC
    CONFIG --> LLM_GATEWAY_SVC

    AUTH_SVC --> POLICY_SVC
    CONV_SVC --> MEMORY_SVC
    CONV_SVC --> PROMPT_SVC
    RETRIEVAL_SVC --> SEARCH_SVC
    RETRIEVAL_SVC --> RERANK_SVC
    RETRIEVAL_SVC --> CITATION_SVC
    PLANNER_SVC --> AGENT_SVC
    AGENT_SVC --> LLM_GATEWAY_SVC
    AGENT_SVC --> RETRIEVAL_SVC
    GUARDRAIL_SVC --> LLM_GATEWAY_SVC
    PROMPT_SVC --> LLM_GATEWAY_SVC
    LLM_GATEWAY_SVC --> EVAL_SVC
    WORKFLOW_SVC --> AGENT_SVC

    %% ============================================
    %% KAFKA CONNECTIONS (Asynchronous)
    %% ============================================

    UPLOAD_SVC --> KAFKA_BUS
    KAFKA_BUS --> PARSER_SVC
    KAFKA_BUS --> OCR_SVC
    KAFKA_BUS --> CHUNKING_SVC
    KAFKA_BUS --> EMBEDDING_SVC
    KAFKA_BUS --> METADATA_SVC
    KAFKA_BUS --> INDEX_SVC
    KAFKA_BUS --> AUDIT_SVC
    KAFKA_BUS --> NOTIFICATION_SVC
    KAFKA_BUS --> BILLING_SVC

    EVAL_SVC --> KAFKA_BUS
    FEEDBACK_SVC --> KAFKA_BUS
    CONV_SVC --> KAFKA_BUS

    %% ============================================
    %% DATA STORE CONNECTIONS
    %% ============================================

    AUTH_SVC --> PG_DB
    USER_SVC --> PG_DB
    TENANT_SVC --> PG_DB
    CONV_SVC --> PG_DB
    MEMORY_SVC --> PG_DB
    AUDIT_SVC --> PG_DB
    BILLING_SVC --> PG_DB
    FEEDBACK_SVC --> PG_DB
    ANALYTICS_SVC --> PG_DB

    CONV_SVC --> REDIS_DB
    MEMORY_SVC --> REDIS_DB
    LLM_GATEWAY_SVC --> REDIS_DB
    AUTH_SVC --> REDIS_DB

    SEARCH_SVC --> VECTOR_STORE
    EMBEDDING_SVC --> VECTOR_STORE
    INDEX_SVC --> VECTOR_STORE
    MEMORY_SVC --> VECTOR_STORE

    SEARCH_SVC --> ES_DB
    INDEX_SVC --> ES_DB

    UPLOAD_SVC --> S3_DB
    PARSER_SVC --> S3_DB

    %% ============================================
    %% STYLES
    %% ============================================

    classDef infraStyle fill:#1b5e20,stroke:#66bb6a,stroke-width:2px,color:#e0e0e0
    classDef authSvcStyle fill:#4a148c,stroke:#ce93d8,stroke-width:2px,color:#e0e0e0
    classDef convSvcStyle fill:#0d47a1,stroke:#64b5f6,stroke-width:2px,color:#e0e0e0
    classDef ragSvcStyle fill:#004d40,stroke:#4db6ac,stroke-width:2px,color:#e0e0e0
    classDef ingestSvcStyle fill:#e65100,stroke:#ffb74d,stroke-width:2px,color:#e0e0e0
    classDef aiSvcStyle fill:#b71c1c,stroke:#ef5350,stroke-width:2px,color:#e0e0e0
    classDef evalSvcStyle fill:#1a237e,stroke:#7986cb,stroke-width:2px,color:#e0e0e0
    classDef opsSvcStyle fill:#263238,stroke:#90a4ae,stroke-width:2px,color:#e0e0e0
    classDef kafkaStyle fill:#ff6f00,stroke:#ffa726,stroke-width:3px,color:#e0e0e0
    classDef dataStyle fill:#3e2723,stroke:#a1887f,stroke-width:2px,color:#e0e0e0

    class CONFIG,EUREKA_SVR,GATEWAY,ADMIN infraStyle
    class AUTH_SVC,USER_SVC,TENANT_SVC,POLICY_SVC authSvcStyle
    class CONV_SVC,MEMORY_SVC,PROMPT_SVC convSvcStyle
    class RETRIEVAL_SVC,SEARCH_SVC,RERANK_SVC,CITATION_SVC ragSvcStyle
    class UPLOAD_SVC,PARSER_SVC,OCR_SVC,CHUNKING_SVC,EMBEDDING_SVC,METADATA_SVC,INDEX_SVC ingestSvcStyle
    class LLM_GATEWAY_SVC,PLANNER_SVC,AGENT_SVC,GUARDRAIL_SVC aiSvcStyle
    class EVAL_SVC,AUDIT_SVC,FEEDBACK_SVC,ANALYTICS_SVC evalSvcStyle
    class NOTIFICATION_SVC,SCHEDULER_SVC,WORKFLOW_SVC,BILLING_SVC,ADMIN_SVC opsSvcStyle
    class KAFKA_BUS kafkaStyle
    class PG_DB,REDIS_DB,VECTOR_STORE,ES_DB,S3_DB dataStyle
```

---

<br/>

<div align="center">

## Volume 4 — Kafka Event Flow

*Complete event-driven architecture with document ingestion and query processing streams*

</div>

```mermaid
---
title: "Volume 4A — Document Ingestion Event Flow"
---
%%{init: {'theme': 'dark', 'themeVariables': { 'primaryColor': '#1a1a2e', 'primaryTextColor': '#e0e0e0', 'primaryBorderColor': '#ff9800', 'lineColor': '#ff9800', 'secondaryColor': '#16213e', 'tertiaryColor': '#0f3460', 'fontFamily': 'Inter, sans-serif'}}}%%

flowchart TB

    %% ============================================
    %% DOCUMENT UPLOAD TRIGGER
    %% ============================================

    USER_UPLOAD["📄 User Uploads Document<br/><i>PDF / DOCX / PPT / XLSX / CSV</i>"]

    %% ============================================
    %% UPLOAD SERVICE
    %% ============================================

    subgraph UPLOAD_PHASE["📤 Upload Phase"]
        VALIDATE_FILE["✅ Validate File<br/><i>Size / Type / Virus Scan</i>"]
        STORE_S3["📦 Store in S3<br/><i>Pre-signed URL<br/>Multipart Upload</i>"]
        CREATE_DOC_RECORD["🗃️ Create Document Record<br/><i>PostgreSQL<br/>Status: UPLOADED</i>"]
    end

    USER_UPLOAD --> VALIDATE_FILE
    VALIDATE_FILE --> STORE_S3
    STORE_S3 --> CREATE_DOC_RECORD

    %% ============================================
    %% EVENT: DocumentUploaded
    %% ============================================

    EVT_UPLOADED{{"📨 Kafka Topic<br/><b>document.uploaded</b><br/><i>Key: tenantId-docId<br/>Partition: by tenantId</i>"}}

    CREATE_DOC_RECORD --> EVT_UPLOADED

    %% ============================================
    %% PARSING PHASE
    %% ============================================

    subgraph PARSE_PHASE["🔧 Parsing Phase"]
        TIKA_PARSE["🔧 Apache Tika Parser<br/><i>Extract raw text<br/>Extract metadata<br/>Detect encoding</i>"]
        TABLE_EXTRACT["📊 Table Extractor<br/><i>Camelot / Tabula<br/>CSV conversion</i>"]
        IMAGE_EXTRACT["🖼️ Image Extractor<br/><i>Extract embedded images<br/>Store to S3</i>"]
        UPDATE_PARSED["🗃️ Update Status<br/><i>Status: PARSED</i>"]
    end

    EVT_UPLOADED --> TIKA_PARSE
    TIKA_PARSE --> TABLE_EXTRACT
    TIKA_PARSE --> IMAGE_EXTRACT
    TABLE_EXTRACT --> UPDATE_PARSED
    IMAGE_EXTRACT --> UPDATE_PARSED

    EVT_PARSED{{"📨 Kafka Topic<br/><b>document.parsed</b><br/><i>Payload: rawText + tables<br/>+ extracted images</i>"}}

    UPDATE_PARSED --> EVT_PARSED

    %% ============================================
    %% OCR PHASE
    %% ============================================

    subgraph OCR_PHASE["👁️ OCR Phase"]
        DETECT_SCAN["🔍 Detect Scanned Pages<br/><i>Image-based PDF detection</i>"]
        RUN_OCR["👁️ Run OCR<br/><i>Tesseract / AWS Textract<br/>Confidence scoring</i>"]
        MERGE_TEXT["🔗 Merge OCR + Text<br/><i>Page-level merge<br/>Layout preservation</i>"]
        UPDATE_OCR["🗃️ Update Status<br/><i>Status: OCR_COMPLETED</i>"]
    end

    EVT_PARSED --> DETECT_SCAN
    DETECT_SCAN --> RUN_OCR
    RUN_OCR --> MERGE_TEXT
    MERGE_TEXT --> UPDATE_OCR

    EVT_OCR{{"📨 Kafka Topic<br/><b>document.ocr.completed</b><br/><i>Payload: mergedText<br/>+ ocrConfidence</i>"}}

    UPDATE_OCR --> EVT_OCR

    %% ============================================
    %% STRUCTURE DETECTION
    %% ============================================

    subgraph STRUCTURE_PHASE["🏗️ Structure Detection Phase"]
        DETECT_HEADERS["📑 Detect Headers<br/><i>H1 / H2 / H3 hierarchy</i>"]
        DETECT_LISTS["📋 Detect Lists<br/><i>Bullet / Numbered</i>"]
        DETECT_CODE["💻 Detect Code Blocks<br/><i>Language identification</i>"]
        DETECT_TABLES_S["📊 Detect Tables<br/><i>Row / Column structure</i>"]
        BUILD_TREE["🌳 Build Document Tree<br/><i>Hierarchical structure</i>"]
        UPDATE_STRUCTURE["🗃️ Update Status<br/><i>Status: STRUCTURED</i>"]
    end

    EVT_OCR --> DETECT_HEADERS
    DETECT_HEADERS --> DETECT_LISTS
    DETECT_LISTS --> DETECT_CODE
    DETECT_CODE --> DETECT_TABLES_S
    DETECT_TABLES_S --> BUILD_TREE
    BUILD_TREE --> UPDATE_STRUCTURE

    EVT_STRUCTURED{{"📨 Kafka Topic<br/><b>document.structured</b><br/><i>Payload: documentTree<br/>+ sectionMap</i>"}}

    UPDATE_STRUCTURE --> EVT_STRUCTURED

    %% ============================================
    %% CHUNKING PHASE
    %% ============================================

    subgraph CHUNK_PHASE["✂️ Chunking Phase"]
        SELECT_STRATEGY["🎯 Select Strategy<br/><i>Based on document type</i>"]
        RECURSIVE_CHUNK["📄 Recursive Splitting<br/><i>Max: 512 tokens<br/>Overlap: 128 tokens</i>"]
        SEMANTIC_CHUNK["🧠 Semantic Chunking<br/><i>Embedding similarity<br/>Breakpoint detection</i>"]
        AGENTIC_CHUNK["🤖 Agentic Chunking<br/><i>LLM-guided splitting<br/>Proposition-based</i>"]
        PARENT_CHILD["🔗 Parent-Child Linking<br/><i>Hierarchical chunks<br/>Context preservation</i>"]
        UPDATE_CHUNKED["🗃️ Update Status<br/><i>Status: CHUNKED<br/>Chunk count stored</i>"]
    end

    EVT_STRUCTURED --> SELECT_STRATEGY
    SELECT_STRATEGY --> RECURSIVE_CHUNK
    SELECT_STRATEGY --> SEMANTIC_CHUNK
    SELECT_STRATEGY --> AGENTIC_CHUNK
    RECURSIVE_CHUNK --> PARENT_CHILD
    SEMANTIC_CHUNK --> PARENT_CHILD
    AGENTIC_CHUNK --> PARENT_CHILD
    PARENT_CHILD --> UPDATE_CHUNKED

    EVT_CHUNKED{{"📨 Kafka Topic<br/><b>document.chunked</b><br/><i>Payload: chunks[]<br/>+ parentChunkMap</i>"}}

    UPDATE_CHUNKED --> EVT_CHUNKED

    %% ============================================
    %% METADATA GENERATION
    %% ============================================

    subgraph META_PHASE["🏷️ Metadata Generation Phase"]
        AUTO_TAG["🏷️ Auto-Tagging<br/><i>LLM-based classification</i>"]
        ENTITY_EXTRACT["🔍 Entity Extraction<br/><i>NER: People / Orgs /<br/>Dates / Amounts</i>"]
        LANG_DETECT["🌐 Language Detection<br/><i>fastText / langdetect</i>"]
        DEPT_CLASSIFY["🏢 Department Classification<br/><i>HR / Finance / Engineering /<br/>Legal / Marketing</i>"]
        ACL_ASSIGN["🔐 ACL Assignment<br/><i>Based on folder / uploader<br/>/ document type</i>"]
        VERSION_TRACK["📊 Version Tracking<br/><i>Content hash comparison<br/>Diff generation</i>"]
        UPDATE_META["🗃️ Update Status<br/><i>Status: METADATA_READY</i>"]
    end

    EVT_CHUNKED --> AUTO_TAG
    AUTO_TAG --> ENTITY_EXTRACT
    ENTITY_EXTRACT --> LANG_DETECT
    LANG_DETECT --> DEPT_CLASSIFY
    DEPT_CLASSIFY --> ACL_ASSIGN
    ACL_ASSIGN --> VERSION_TRACK
    VERSION_TRACK --> UPDATE_META

    EVT_META{{"📨 Kafka Topic<br/><b>document.metadata.generated</b><br/><i>Payload: metadata{}<br/>+ entities[] + acl{}</i>"}}

    UPDATE_META --> EVT_META

    %% ============================================
    %% EMBEDDING PHASE
    %% ============================================

    subgraph EMBED_PHASE["🧬 Embedding Phase"]
        BATCH_CHUNKS["📦 Batch Chunks<br/><i>Batch size: 64<br/>GPU Optimized</i>"]
        GENERATE_EMBED["🧬 Generate Embeddings<br/><i>text-embedding-3-large<br/>Dimension: 3072</i>"]
        LATE_INTERACT["🔄 Late Interaction Vectors<br/><i>ColBERTv2<br/>Token-level embeddings</i>"]
        SPARSE_EMBED["📊 Sparse Embeddings<br/><i>SPLADE / BM25 weights</i>"]
        QUALITY_CHECK["✅ Quality Check<br/><i>Embedding norm validation<br/>Dimension verification</i>"]
        UPDATE_EMBED["🗃️ Update Status<br/><i>Status: EMBEDDED</i>"]
    end

    EVT_META --> BATCH_CHUNKS
    BATCH_CHUNKS --> GENERATE_EMBED
    BATCH_CHUNKS --> LATE_INTERACT
    BATCH_CHUNKS --> SPARSE_EMBED
    GENERATE_EMBED --> QUALITY_CHECK
    LATE_INTERACT --> QUALITY_CHECK
    SPARSE_EMBED --> QUALITY_CHECK
    QUALITY_CHECK --> UPDATE_EMBED

    EVT_EMBED{{"📨 Kafka Topic<br/><b>document.embedded</b><br/><i>Payload: embeddings[]<br/>+ sparseVectors[]</i>"}}

    UPDATE_EMBED --> EVT_EMBED

    %% ============================================
    %% INDEXING PHASE
    %% ============================================

    subgraph INDEX_PHASE["📇 Multi-Index Phase"]
        direction TB
        WRITE_VECTOR["🧬 Write to Vector DB<br/><i>Qdrant / Milvus<br/>Collection: tenant_docs<br/>Payload: metadata</i>"]
        WRITE_ELASTIC["🔍 Write to Elasticsearch<br/><i>Index: tenant_documents<br/>BM25 analyzers<br/>Custom tokenizers</i>"]
        WRITE_PG["🐘 Write to PostgreSQL<br/><i>chunks table<br/>document_metadata table<br/>Full-text tsvector</i>"]
        UPDATE_INDEXED["🗃️ Update Status<br/><i>Status: INDEXED</i>"]
    end

    EVT_EMBED --> WRITE_VECTOR
    EVT_EMBED --> WRITE_ELASTIC
    EVT_EMBED --> WRITE_PG
    WRITE_VECTOR --> UPDATE_INDEXED
    WRITE_ELASTIC --> UPDATE_INDEXED
    WRITE_PG --> UPDATE_INDEXED

    EVT_INDEXED{{"📨 Kafka Topic<br/><b>document.indexed</b><br/><i>Payload: indexStats{}<br/>+ vectorCount + esDocCount</i>"}}

    UPDATE_INDEXED --> EVT_INDEXED

    %% ============================================
    %% CACHE & NOTIFICATION
    %% ============================================

    subgraph FINALIZE_PHASE["✅ Finalization Phase"]
        INVALIDATE_CACHE["⚡ Invalidate Cache<br/><i>Redis cache bust<br/>Related queries</i>"]
        SEND_NOTIFICATION["🔔 Send Notification<br/><i>Email / Slack / Webhook<br/>Processing complete</i>"]
        UPDATE_ANALYTICS["📈 Update Analytics<br/><i>Document count<br/>Processing time<br/>Token usage</i>"]
        FINAL_STATUS["🗃️ Final Status<br/><i>Status: READY<br/>searchable: true</i>"]
    end

    EVT_INDEXED --> INVALIDATE_CACHE
    EVT_INDEXED --> SEND_NOTIFICATION
    EVT_INDEXED --> UPDATE_ANALYTICS
    INVALIDATE_CACHE --> FINAL_STATUS
    SEND_NOTIFICATION --> FINAL_STATUS

    EVT_READY{{"📨 Kafka Topic<br/><b>document.ready</b><br/><i>Payload: documentId<br/>+ processingStats{}</i>"}}

    FINAL_STATUS --> EVT_READY

    %% ============================================
    %% ERROR HANDLING
    %% ============================================

    subgraph ERROR_HANDLING["❌ Error Handling"]
        DLQ["☠️ Dead Letter Queue<br/><i>Kafka DLQ Topic<br/>Max retries: 3</i>"]
        RETRY_POLICY["🔄 Retry Policy<br/><i>Exponential Backoff<br/>1s → 2s → 4s</i>"]
        ALERT_OPS["🚨 Alert Operations<br/><i>PagerDuty / Slack Alert</i>"]
        MANUAL_REVIEW["👨‍💼 Manual Review Queue<br/><i>Admin Dashboard</i>"]
    end

    EVT_UPLOADED -.->|Failure| DLQ
    EVT_PARSED -.->|Failure| DLQ
    EVT_OCR -.->|Failure| DLQ
    EVT_CHUNKED -.->|Failure| DLQ
    EVT_EMBED -.->|Failure| DLQ
    DLQ --> RETRY_POLICY
    RETRY_POLICY -->|Max Retries| ALERT_OPS
    ALERT_OPS --> MANUAL_REVIEW

    %% ============================================
    %% STYLES
    %% ============================================

    classDef uploadStyle fill:#1565c0,stroke:#42a5f5,stroke-width:2px,color:#e0e0e0
    classDef parseStyle fill:#6a1b9a,stroke:#ce93d8,stroke-width:2px,color:#e0e0e0
    classDef ocrStyle fill:#00695c,stroke:#4db6ac,stroke-width:2px,color:#e0e0e0
    classDef structStyle fill:#4e342e,stroke:#a1887f,stroke-width:2px,color:#e0e0e0
    classDef chunkStyle fill:#283593,stroke:#7986cb,stroke-width:2px,color:#e0e0e0
    classDef metaStyle fill:#ad1457,stroke:#f06292,stroke-width:2px,color:#e0e0e0
    classDef embedStyle fill:#1b5e20,stroke:#66bb6a,stroke-width:2px,color:#e0e0e0
    classDef indexStyle fill:#e65100,stroke:#ff9100,stroke-width:2px,color:#e0e0e0
    classDef kafkaStyle fill:#ff6f00,stroke:#ffa726,stroke-width:3px,color:#000000
    classDef errorStyle fill:#b71c1c,stroke:#ef5350,stroke-width:2px,color:#e0e0e0
    classDef finalStyle fill:#004d40,stroke:#26a69a,stroke-width:2px,color:#e0e0e0

    class VALIDATE_FILE,STORE_S3,CREATE_DOC_RECORD uploadStyle
    class TIKA_PARSE,TABLE_EXTRACT,IMAGE_EXTRACT,UPDATE_PARSED parseStyle
    class DETECT_SCAN,RUN_OCR,MERGE_TEXT,UPDATE_OCR ocrStyle
    class DETECT_HEADERS,DETECT_LISTS,DETECT_CODE,DETECT_TABLES_S,BUILD_TREE,UPDATE_STRUCTURE structStyle
    class SELECT_STRATEGY,RECURSIVE_CHUNK,SEMANTIC_CHUNK,AGENTIC_CHUNK,PARENT_CHILD,UPDATE_CHUNKED chunkStyle
    class AUTO_TAG,ENTITY_EXTRACT,LANG_DETECT,DEPT_CLASSIFY,ACL_ASSIGN,VERSION_TRACK,UPDATE_META metaStyle
    class BATCH_CHUNKS,GENERATE_EMBED,LATE_INTERACT,SPARSE_EMBED,QUALITY_CHECK,UPDATE_EMBED embedStyle
    class WRITE_VECTOR,WRITE_ELASTIC,WRITE_PG,UPDATE_INDEXED indexStyle
    class EVT_UPLOADED,EVT_PARSED,EVT_OCR,EVT_STRUCTURED,EVT_CHUNKED,EVT_META,EVT_EMBED,EVT_INDEXED,EVT_READY kafkaStyle
    class DLQ,RETRY_POLICY,ALERT_OPS,MANUAL_REVIEW errorStyle
    class INVALIDATE_CACHE,SEND_NOTIFICATION,UPDATE_ANALYTICS,FINAL_STATUS finalStyle
    class USER_UPLOAD uploadStyle
```

<br/>

```mermaid
---
title: "Volume 4B — Query Processing Event Flow"
---
%%{init: {'theme': 'dark', 'themeVariables': { 'primaryColor': '#1a1a2e', 'primaryTextColor': '#e0e0e0', 'primaryBorderColor': '#ff9800', 'lineColor': '#ff9800', 'secondaryColor': '#16213e', 'tertiaryColor': '#0f3460', 'fontFamily': 'Inter, sans-serif'}}}%%

flowchart TB

    %% ============================================
    %% USER QUERY
    %% ============================================

    USER_QUERY["💬 User Sends Query<br/><i>Natural Language Question</i>"]

    %% ============================================
    %% CONVERSATION SERVICE
    %% ============================================

    subgraph CONV_PHASE["🗣️ Conversation Phase"]
        LOAD_SESSION["📋 Load Session<br/><i>Redis: conversation context<br/>Last N messages</i>"]
        LOAD_MEMORY["🧩 Recall Memory<br/><i>Short-term + Long-term<br/>Relevant memories</i>"]
        GUARDRAIL_CHECK["🛡️ Input Guardrails<br/><i>Prompt injection scan<br/>PII detection<br/>Jailbreak check</i>"]
    end

    USER_QUERY --> LOAD_SESSION
    LOAD_SESSION --> LOAD_MEMORY
    LOAD_MEMORY --> GUARDRAIL_CHECK

    EVT_QUESTION{{"📨 Kafka Topic<br/><b>query.asked</b><br/><i>Key: sessionId<br/>Payload: query + context</i>"}}

    GUARDRAIL_CHECK --> EVT_QUESTION

    %% ============================================
    %% ROUTING PHASE
    %% ============================================

    subgraph ROUTE_PHASE["🔀 Routing Phase"]
        CLASSIFY_INTENT["🎯 Classify Intent<br/><i>Small LLM classifier<br/>Greeting / Math / SQL /<br/>Knowledge / Complex</i>"]
        ROUTE_DECISION{"🔀 Route Decision"}
        GREETING_RESP["👋 Greeting Response<br/><i>Small LLM / Template</i>"]
        CALC_RESP["🧮 Calculator<br/><i>Direct computation</i>"]
        SQL_RESP["🗃️ SQL Executor<br/><i>Query database</i>"]
    end

    EVT_QUESTION --> CLASSIFY_INTENT
    CLASSIFY_INTENT --> ROUTE_DECISION
    ROUTE_DECISION -->|Greeting| GREETING_RESP
    ROUTE_DECISION -->|Math| CALC_RESP
    ROUTE_DECISION -->|SQL| SQL_RESP
    ROUTE_DECISION -->|Knowledge / Complex| PLANNER_PHASE

    %% ============================================
    %% PLANNER PHASE
    %% ============================================

    subgraph PLANNER_PHASE["📋 Planning Phase"]
        DECOMPOSE["🧩 Task Decomposition<br/><i>Break into sub-tasks<br/>Identify dependencies</i>"]
        SELECT_TOOLS["🔧 Tool Selection<br/><i>Retrieval / API / Calculator<br/>/ Database / External</i>"]
        BUILD_DAG["📊 Build Execution DAG<br/><i>Dependency graph<br/>Parallel paths</i>"]
    end

    EVT_PLAN{{"📨 Kafka Topic<br/><b>query.plan.created</b><br/><i>Payload: plan{} + dag{}<br/>+ selectedTools[]</i>"}}

    DECOMPOSE --> SELECT_TOOLS
    SELECT_TOOLS --> BUILD_DAG
    BUILD_DAG --> EVT_PLAN

    %% ============================================
    %% RETRIEVAL PHASE
    %% ============================================

    subgraph RETRIEVAL_PHASE["🔍 Retrieval Phase"]
        QUERY_EXPAND["🔄 Query Expansion<br/><i>HyDE / Multi-query<br/>Synonym expansion</i>"]
        META_FILTER["🏷️ Metadata Pre-filter<br/><i>Tenant / Department<br/>ACL / Date range</i>"]
        BM25_SEARCH["📝 BM25 Search<br/><i>Elasticsearch<br/>TF-IDF scoring</i>"]
        VECTOR_SEARCH["🧬 Vector Search<br/><i>Qdrant ANN<br/>Cosine similarity</i>"]
        SPARSE_SEARCH["📊 Sparse Search<br/><i>SPLADE<br/>Learned sparse</i>"]
        RRF_MERGE["🔗 RRF Merge<br/><i>Reciprocal Rank Fusion<br/>k=60</i>"]
    end

    EVT_PLAN --> QUERY_EXPAND
    QUERY_EXPAND --> META_FILTER
    META_FILTER --> BM25_SEARCH
    META_FILTER --> VECTOR_SEARCH
    META_FILTER --> SPARSE_SEARCH
    BM25_SEARCH --> RRF_MERGE
    VECTOR_SEARCH --> RRF_MERGE
    SPARSE_SEARCH --> RRF_MERGE

    EVT_RETRIEVED{{"📨 Kafka Topic<br/><b>query.retrieval.completed</b><br/><i>Payload: candidates[]<br/>+ scores{}</i>"}}

    RRF_MERGE --> EVT_RETRIEVED

    %% ============================================
    %% RERANKING PHASE
    %% ============================================

    subgraph RERANK_PHASE["📊 Reranking Phase"]
        CROSS_ENCODE["🔄 Cross-Encoder Rerank<br/><i>BGE-Reranker-v2<br/>Query-Document pairs</i>"]
        DIVERSITY_FILTER["🌈 Diversity Filter<br/><i>MMR: Maximal Marginal<br/>Relevance, lambda=0.7</i>"]
        CONTEXT_COMPRESS["📦 Context Compression<br/><i>LLMLingua-2<br/>Remove redundancy</i>"]
        TOP_K["🏆 Top-K Selection<br/><i>K=5 chunks<br/>Confidence threshold: 0.7</i>"]
    end

    EVT_RETRIEVED --> CROSS_ENCODE
    CROSS_ENCODE --> DIVERSITY_FILTER
    DIVERSITY_FILTER --> CONTEXT_COMPRESS
    CONTEXT_COMPRESS --> TOP_K

    EVT_RERANKED{{"📨 Kafka Topic<br/><b>query.rerank.completed</b><br/><i>Payload: topChunks[]<br/>+ rerankScores{}</i>"}}

    TOP_K --> EVT_RERANKED

    %% ============================================
    %% GENERATION PHASE
    %% ============================================

    subgraph GEN_PHASE["🧠 Generation Phase"]
        BUILD_PROMPT["📝 Build Prompt<br/><i>System + Context + Memory<br/>+ Conversation History<br/>+ Retrieved Chunks<br/>+ Instructions</i>"]
        SELECT_MODEL["🎯 Select LLM<br/><i>Based on complexity<br/>/ cost / latency</i>"]
        STREAM_GEN["⚡ Stream Generation<br/><i>SSE streaming<br/>Token by token</i>"]
        GEN_CITATIONS["📌 Generate Citations<br/><i>Chunk → Source mapping<br/>Confidence scores</i>"]
    end

    EVT_RERANKED --> BUILD_PROMPT
    BUILD_PROMPT --> SELECT_MODEL
    SELECT_MODEL --> STREAM_GEN
    STREAM_GEN --> GEN_CITATIONS

    EVT_GENERATED{{"📨 Kafka Topic<br/><b>query.answer.generated</b><br/><i>Payload: answer + citations[]<br/>+ tokenUsage{}</i>"}}

    GEN_CITATIONS --> EVT_GENERATED

    %% ============================================
    %% EVALUATION PHASE
    %% ============================================

    subgraph EVAL_PHASE["🔄 Self-Correcting Evaluation"]
        CHECK_GROUND["✅ Grounding Check<br/><i>Is answer grounded<br/>in context?</i>"]
        CHECK_FAITH["🎯 Faithfulness Check<br/><i>Does answer align<br/>with sources?</i>"]
        CHECK_HALLU["🚨 Hallucination Check<br/><i>Detect fabricated<br/>claims</i>"]
        CONFIDENCE_SCORE["📊 Confidence Score<br/><i>Aggregate quality<br/>metric</i>"]
        EVAL_DECISION{"✅ Quality Gate<br/><i>Threshold: 0.85</i>"}
    end

    EVT_GENERATED --> CHECK_GROUND
    CHECK_GROUND --> CHECK_FAITH
    CHECK_FAITH --> CHECK_HALLU
    CHECK_HALLU --> CONFIDENCE_SCORE
    CONFIDENCE_SCORE --> EVAL_DECISION

    EVAL_DECISION -->|Pass| RESPONSE_PHASE
    EVAL_DECISION -->|Fail| RETRY_PHASE

    %% ============================================
    %% RETRY PHASE
    %% ============================================

    subgraph RETRY_PHASE["🔄 Query Rewrite & Retry"]
        REWRITE_QUERY["✏️ Rewrite Query<br/><i>LLM-based rewrite<br/>Add context clues</i>"]
        RETRY_COUNT{"🔢 Retry Count<br/><i>Max: 2 retries</i>"}
        FALLBACK["💬 Fallback Response<br/><i>I don't have enough<br/>information to answer</i>"]
    end

    REWRITE_QUERY --> RETRY_COUNT
    RETRY_COUNT -->|Retry| RETRIEVAL_PHASE
    RETRY_COUNT -->|Max Reached| FALLBACK

    %% ============================================
    %% RESPONSE PHASE
    %% ============================================

    subgraph RESPONSE_PHASE["📤 Response Phase"]
        FORMAT_RESP["📝 Format Response<br/><i>Markdown / JSON<br/>+ Citations</i>"]
        STORE_MEMORY["🧩 Store Memory<br/><i>Update conversation<br/>memory</i>"]
        GUARDRAIL_OUT["🛡️ Output Guardrails<br/><i>PII redaction<br/>Content safety</i>"]
        SEND_RESPONSE["📤 Send to User<br/><i>SSE Stream / REST<br/>/ WebSocket</i>"]
    end

    FORMAT_RESP --> STORE_MEMORY
    STORE_MEMORY --> GUARDRAIL_OUT
    GUARDRAIL_OUT --> SEND_RESPONSE

    EVT_COMPLETED{{"📨 Kafka Topic<br/><b>query.completed</b><br/><i>Payload: responseMetrics{}<br/>+ latency + tokenUsage</i>"}}

    SEND_RESPONSE --> EVT_COMPLETED

    %% ============================================
    %% POST-PROCESSING EVENTS
    %% ============================================

    subgraph POST_PROCESS["📊 Post-Processing"]
        SAVE_AUDIT["📋 Save Audit Log<br/><i>Full query trace<br/>Immutable record</i>"]
        UPDATE_USAGE["💰 Update Usage Metrics<br/><i>Token count<br/>Cost calculation</i>"]
        FEEDBACK_WAIT["👍 Await User Feedback<br/><i>Thumbs up/down<br/>Comments</i>"]
        EVAL_METRICS["📈 Record Eval Metrics<br/><i>RAGAS scores<br/>Latency breakdown</i>"]
    end

    EVT_COMPLETED --> SAVE_AUDIT
    EVT_COMPLETED --> UPDATE_USAGE
    EVT_COMPLETED --> FEEDBACK_WAIT
    EVT_COMPLETED --> EVAL_METRICS

    EVT_AUDIT{{"📨 Kafka Topic<br/><b>audit.saved</b>"}}

    SAVE_AUDIT --> EVT_AUDIT

    %% ============================================
    %% STYLES
    %% ============================================

    classDef convStyle fill:#1565c0,stroke:#42a5f5,stroke-width:2px,color:#e0e0e0
    classDef routeStyle fill:#6a1b9a,stroke:#ce93d8,stroke-width:2px,color:#e0e0e0
    classDef planStyle fill:#00695c,stroke:#4db6ac,stroke-width:2px,color:#e0e0e0
    classDef retrieveStyle fill:#283593,stroke:#7986cb,stroke-width:2px,color:#e0e0e0
    classDef rerankStyle fill:#4e342e,stroke:#a1887f,stroke-width:2px,color:#e0e0e0
    classDef genStyle fill:#b71c1c,stroke:#ef5350,stroke-width:2px,color:#e0e0e0
    classDef evalStyle fill:#1b5e20,stroke:#66bb6a,stroke-width:2px,color:#e0e0e0
    classDef retryStyle fill:#e65100,stroke:#ff9100,stroke-width:2px,color:#e0e0e0
    classDef respStyle fill:#004d40,stroke:#26a69a,stroke-width:2px,color:#e0e0e0
    classDef kafkaStyle fill:#ff6f00,stroke:#ffa726,stroke-width:3px,color:#000000
    classDef postStyle fill:#263238,stroke:#90a4ae,stroke-width:2px,color:#e0e0e0

    class LOAD_SESSION,LOAD_MEMORY,GUARDRAIL_CHECK convStyle
    class CLASSIFY_INTENT,ROUTE_DECISION,GREETING_RESP,CALC_RESP,SQL_RESP routeStyle
    class DECOMPOSE,SELECT_TOOLS,BUILD_DAG planStyle
    class QUERY_EXPAND,META_FILTER,BM25_SEARCH,VECTOR_SEARCH,SPARSE_SEARCH,RRF_MERGE retrieveStyle
    class CROSS_ENCODE,DIVERSITY_FILTER,CONTEXT_COMPRESS,TOP_K rerankStyle
    class BUILD_PROMPT,SELECT_MODEL,STREAM_GEN,GEN_CITATIONS genStyle
    class CHECK_GROUND,CHECK_FAITH,CHECK_HALLU,CONFIDENCE_SCORE,EVAL_DECISION evalStyle
    class REWRITE_QUERY,RETRY_COUNT,FALLBACK retryStyle
    class FORMAT_RESP,STORE_MEMORY,GUARDRAIL_OUT,SEND_RESPONSE respStyle
    class EVT_QUESTION,EVT_PLAN,EVT_RETRIEVED,EVT_RERANKED,EVT_GENERATED,EVT_COMPLETED,EVT_AUDIT kafkaStyle
    class SAVE_AUDIT,UPDATE_USAGE,FEEDBACK_WAIT,EVAL_METRICS postStyle
    class USER_QUERY convStyle
```

---

<br/>

<div align="center">

## Volume 5 — Hybrid RAG Pipeline

*Advanced retrieval-augmented generation with multi-stage processing*

</div>

```mermaid
---
title: "Volume 5 — Complete Hybrid RAG Pipeline"
---
%%{init: {'theme': 'dark', 'themeVariables': { 'primaryColor': '#1a1a2e', 'primaryTextColor': '#e0e0e0', 'primaryBorderColor': '#26c6da', 'lineColor': '#26c6da', 'secondaryColor': '#16213e', 'tertiaryColor': '#0f3460', 'fontFamily': 'Inter, sans-serif'}}}%%

flowchart TB

    %% ============================================
    %% INPUT
    %% ============================================

    INPUT["💬 User Query<br/><i>Natural Language Question</i>"]

    %% ============================================
    %% QUERY UNDERSTANDING
    %% ============================================

    subgraph QUERY_UNDERSTAND["🧠 Query Understanding Layer"]
        direction TB

        subgraph QUERY_ANALYSIS["🔍 Query Analysis"]
            INTENT_DETECT["🎯 Intent Detection<br/><i>Classification: Factual /<br/>Analytical / Comparative /<br/>Procedural / Creative</i>"]
            ENTITY_RECOG["🏷️ Named Entity Recognition<br/><i>People / Organizations /<br/>Products / Dates / Locations</i>"]
            COMPLEXITY_EST["📊 Complexity Estimation<br/><i>Simple lookup vs<br/>Multi-hop reasoning</i>"]
            LANG_ID["🌐 Language Identification<br/><i>Multilingual support<br/>Auto-translation</i>"]
        end

        subgraph QUERY_TRANSFORM["🔄 Query Transformation"]
            MULTI_QUERY["📝 Multi-Query Generation<br/><i>LLM generates 3-5<br/>diverse reformulations</i>"]
            HYDE["🎭 HyDE<br/><i>Hypothetical Document<br/>Embedding generation</i>"]
            STEP_BACK["🔙 Step-Back Prompting<br/><i>Abstract higher-level<br/>question</i>"]
            DECOMPOSE_Q["🧩 Query Decomposition<br/><i>Break complex query into<br/>atomic sub-questions</i>"]
        end
    end

    INPUT --> INTENT_DETECT
    INTENT_DETECT --> ENTITY_RECOG
    ENTITY_RECOG --> COMPLEXITY_EST
    COMPLEXITY_EST --> LANG_ID
    LANG_ID --> MULTI_QUERY
    MULTI_QUERY --> HYDE
    HYDE --> STEP_BACK
    STEP_BACK --> DECOMPOSE_Q

    %% ============================================
    %% PRE-RETRIEVAL FILTERING
    %% ============================================

    subgraph PRE_FILTER["🏷️ Pre-Retrieval Filtering"]
        direction TB

        TENANT_FILTER["🏢 Tenant Isolation<br/><i>PostgreSQL RLS<br/>tenant_id = current_tenant</i>"]
        DEPT_FILTER["🏛️ Department Filter<br/><i>department IN<br/>user.departments</i>"]
        ACL_FILTER["🔐 ACL Enforcement<br/><i>document.acl CONTAINS<br/>user.groups</i>"]
        VERSION_FILTER["📊 Version Filter<br/><i>doc.version = latest<br/>OR doc.version = specified</i>"]
        DATE_FILTER["📅 Date Range Filter<br/><i>created_at BETWEEN<br/>start AND end</i>"]
        COLLECTION_FILTER["📁 Collection Filter<br/><i>collection_id IN<br/>selected_collections</i>"]
        DOCTYPE_FILTER["📄 Document Type Filter<br/><i>type IN selected_types<br/>PDF / DOCX / etc.</i>"]
    end

    DECOMPOSE_Q --> TENANT_FILTER
    TENANT_FILTER --> DEPT_FILTER
    DEPT_FILTER --> ACL_FILTER
    ACL_FILTER --> VERSION_FILTER
    VERSION_FILTER --> DATE_FILTER
    DATE_FILTER --> COLLECTION_FILTER
    COLLECTION_FILTER --> DOCTYPE_FILTER

    %% ============================================
    %% HYBRID SEARCH
    %% ============================================

    subgraph HYBRID_SEARCH["🔍 Hybrid Search Engine"]
        direction TB

        subgraph DENSE_PATH["🧬 Dense Retrieval Path"]
            QUERY_EMBED["🧬 Query Embedding<br/><i>text-embedding-3-large<br/>Dim: 3072 / Matryoshka</i>"]
            ANN_SEARCH["⚡ ANN Search<br/><i>Qdrant HNSW<br/>ef=256 / M=16<br/>Top 50 candidates</i>"]
            MULTI_VEC["🔢 Multi-Vector Search<br/><i>ColBERTv2 late interaction<br/>Token-level matching</i>"]
        end

        subgraph SPARSE_PATH["📝 Sparse Retrieval Path"]
            BM25_QUERY["📝 BM25 Query<br/><i>Elasticsearch<br/>Custom analyzers<br/>Boost: title=2.0</i>"]
            SPLADE_QUERY["📊 SPLADE Search<br/><i>Learned Sparse<br/>Expansion terms<br/>Top 50 candidates</i>"]
        end

        subgraph KNOWLEDGE_GRAPH["🕸️ Knowledge Graph Path"]
            KG_QUERY["🕸️ Graph Traversal<br/><i>Neo4j / ArangoDB<br/>Entity relationships</i>"]
            KG_EXPAND["🔗 Relationship Expansion<br/><i>1-hop and 2-hop<br/>neighbors</i>"]
        end

        subgraph FUSION["🔗 Result Fusion"]
            RRF_FUSION["🔢 Reciprocal Rank Fusion<br/><i>k=60<br/>score = Σ 1/(k+rank)</i>"]
            WEIGHTED_FUSION["⚖️ Weighted Fusion<br/><i>Dense: 0.4<br/>Sparse: 0.3<br/>ColBERT: 0.2<br/>KG: 0.1</i>"]
            DEDUP["🔄 Deduplication<br/><i>Content hash matching<br/>Overlap detection</i>"]
        end
    end

    DOCTYPE_FILTER --> QUERY_EMBED
    DOCTYPE_FILTER --> BM25_QUERY
    DOCTYPE_FILTER --> SPLADE_QUERY
    DOCTYPE_FILTER --> KG_QUERY

    QUERY_EMBED --> ANN_SEARCH
    QUERY_EMBED --> MULTI_VEC
    KG_QUERY --> KG_EXPAND

    ANN_SEARCH --> RRF_FUSION
    MULTI_VEC --> RRF_FUSION
    BM25_QUERY --> RRF_FUSION
    SPLADE_QUERY --> RRF_FUSION
    KG_EXPAND --> RRF_FUSION

    RRF_FUSION --> WEIGHTED_FUSION
    WEIGHTED_FUSION --> DEDUP

    %% ============================================
    %% RERANKING PIPELINE
    %% ============================================

    subgraph RERANK_PIPELINE["📊 Multi-Stage Reranking"]
        direction TB

        CROSS_ENCODER["🔄 Cross-Encoder Reranking<br/><i>BGE-Reranker-v2-m3<br/>Query-Document pairs<br/>Batch size: 32</i>"]
        COLBERT_RERANK["🎯 ColBERT Reranking<br/><i>Late interaction scoring<br/>Token-level relevance</i>"]
        LLM_RERANK["🧠 LLM Reranking<br/><i>GPT-4 listwise ranking<br/>For complex queries only</i>"]
        MMR_DIVERSITY["🌈 MMR Diversity<br/><i>Maximal Marginal Relevance<br/>λ = 0.7<br/>Reduce redundancy</i>"]
        SCORE_NORMALIZE["📊 Score Normalization<br/><i>Min-max scaling<br/>Cross-model calibration</i>"]
    end

    DEDUP --> CROSS_ENCODER
    CROSS_ENCODER --> COLBERT_RERANK
    COLBERT_RERANK --> LLM_RERANK
    LLM_RERANK --> MMR_DIVERSITY
    MMR_DIVERSITY --> SCORE_NORMALIZE

    %% ============================================
    %% CONTEXT PROCESSING
    %% ============================================

    subgraph CONTEXT_PROC["📦 Context Processing"]
        direction TB

        PARENT_RETRIEVE["📑 Parent Chunk Retrieval<br/><i>Fetch parent documents<br/>for context expansion</i>"]
        CONTEXT_WINDOW["📐 Context Window Mgmt<br/><i>Max tokens: 128K<br/>Priority-based truncation</i>"]
        COMPRESS["📦 Context Compression<br/><i>LLMLingua-2<br/>2-5x compression<br/>Selective retention</i>"]
        CITE_MAP["📌 Citation Mapping<br/><i>Chunk → Source Document<br/>Page number / Section</i>"]
        TOP_K_SELECT["🏆 Top-K Selection<br/><i>K=5 final chunks<br/>Confidence > 0.7</i>"]
    end

    SCORE_NORMALIZE --> PARENT_RETRIEVE
    PARENT_RETRIEVE --> CONTEXT_WINDOW
    CONTEXT_WINDOW --> COMPRESS
    COMPRESS --> CITE_MAP
    CITE_MAP --> TOP_K_SELECT

    %% ============================================
    %% PROMPT ENGINEERING
    %% ============================================

    subgraph PROMPT_ENG["📝 Advanced Prompt Engineering"]
        direction TB

        SYSTEM_PROMPT["🖥️ System Prompt<br/><i>Role definition<br/>Behavioral constraints<br/>Output format</i>"]
        CONTEXT_INJECT["📚 Context Injection<br/><i>Retrieved chunks<br/>With source markers<br/>[Source 1] [Source 2]</i>"]
        MEMORY_INJECT["🧩 Memory Injection<br/><i>Relevant memories<br/>User preferences<br/>Past interactions</i>"]
        HISTORY_INJECT["💬 History Injection<br/><i>Last N turns<br/>Sliding window<br/>Summary of older turns</i>"]
        CHAIN_OF_THOUGHT["🔗 Chain-of-Thought<br/><i>Think step by step<br/>Show reasoning</i>"]
        FEW_SHOT["📋 Few-Shot Examples<br/><i>Dynamic example selection<br/>Based on query type</i>"]
        OUTPUT_FORMAT["📄 Output Schema<br/><i>JSON / Markdown / Table<br/>Structured output</i>"]
    end

    TOP_K_SELECT --> SYSTEM_PROMPT
    SYSTEM_PROMPT --> CONTEXT_INJECT
    CONTEXT_INJECT --> MEMORY_INJECT
    MEMORY_INJECT --> HISTORY_INJECT
    HISTORY_INJECT --> CHAIN_OF_THOUGHT
    CHAIN_OF_THOUGHT --> FEW_SHOT
    FEW_SHOT --> OUTPUT_FORMAT

    %% ============================================
    %% LLM GENERATION
    %% ============================================

    subgraph LLM_GEN["🧠 LLM Generation"]
        direction TB

        MODEL_SELECT["🎯 Dynamic Model Selection<br/><i>Simple → GPT-4o-mini<br/>Standard → GPT-4o<br/>Complex → Claude 3.5 Sonnet<br/>Code → Codestral</i>"]
        TOKEN_COUNT["🔢 Token Estimation<br/><i>Pre-flight check<br/>Budget validation</i>"]
        STREAM_RESPONSE["⚡ Streaming Response<br/><i>Server-Sent Events<br/>Token-by-token delivery</i>"]
        STRUCTURED_OUTPUT["📋 Structured Output<br/><i>JSON mode / Function calling<br/>Schema validation</i>"]
    end

    OUTPUT_FORMAT --> MODEL_SELECT
    MODEL_SELECT --> TOKEN_COUNT
    TOKEN_COUNT --> STREAM_RESPONSE
    STREAM_RESPONSE --> STRUCTURED_OUTPUT

    %% ============================================
    %% POST-GENERATION
    %% ============================================

    subgraph POST_GEN["✅ Post-Generation Processing"]
        direction TB

        CITE_ATTACH["📌 Attach Citations<br/><i>[1] Source Doc, Page 5<br/>[2] Source Doc, Section 3</i>"]
        CONFIDENCE["📊 Confidence Score<br/><i>Aggregate retrieval +<br/>generation confidence</i>"]
        FORMAT_OUT["📝 Format Output<br/><i>Markdown rendering<br/>Code highlighting<br/>Table formatting</i>"]
        CACHE_RESPONSE["⚡ Cache Response<br/><i>Redis cache<br/>TTL: 1 hour<br/>Key: query hash</i>"]
    end

    STRUCTURED_OUTPUT --> CITE_ATTACH
    CITE_ATTACH --> CONFIDENCE
    CONFIDENCE --> FORMAT_OUT
    FORMAT_OUT --> CACHE_RESPONSE

    FINAL_OUTPUT["📤 Final Response<br/><i>Answer + Citations +<br/>Confidence Score +<br/>Source Documents</i>"]

    CACHE_RESPONSE --> FINAL_OUTPUT

    %% ============================================
    %% DATA STORES
    %% ============================================

    QDRANT_DB[("🧬 Qdrant<br/><i>Vector Store</i>")]
    ES_DB[("🔍 Elasticsearch<br/><i>Full-Text Index</i>")]
    NEO4J_DB[("🕸️ Neo4j<br/><i>Knowledge Graph</i>")]
    PG_DB[("🐘 PostgreSQL<br/><i>Metadata + ACL</i>")]
    REDIS_DB[("⚡ Redis<br/><i>Response Cache</i>")]

    ANN_SEARCH --> QDRANT_DB
    MULTI_VEC --> QDRANT_DB
    BM25_QUERY --> ES_DB
    SPLADE_QUERY --> ES_DB
    KG_QUERY --> NEO4J_DB
    TENANT_FILTER --> PG_DB
    CACHE_RESPONSE --> REDIS_DB

    %% ============================================
    %% STYLES
    %% ============================================

    classDef inputStyle fill:#1565c0,stroke:#42a5f5,stroke-width:2px,color:#e0e0e0
    classDef queryStyle fill:#4a148c,stroke:#ce93d8,stroke-width:2px,color:#e0e0e0
    classDef filterStyle fill:#bf360c,stroke:#ff8a65,stroke-width:2px,color:#e0e0e0
    classDef searchStyle fill:#004d40,stroke:#4db6ac,stroke-width:2px,color:#e0e0e0
    classDef rerankStyle fill:#1a237e,stroke:#7986cb,stroke-width:2px,color:#e0e0e0
    classDef contextStyle fill:#4e342e,stroke:#a1887f,stroke-width:2px,color:#e0e0e0
    classDef promptStyle fill:#283593,stroke:#9fa8da,stroke-width:2px,color:#e0e0e0
    classDef llmStyle fill:#b71c1c,stroke:#ef5350,stroke-width:2px,color:#e0e0e0
    classDef postStyle fill:#1b5e20,stroke:#66bb6a,stroke-width:2px,color:#e0e0e0
    classDef dbStyle fill:#263238,stroke:#78909c,stroke-width:2px,color:#e0e0e0
    classDef outputStyle fill:#00695c,stroke:#26a69a,stroke-width:3px,color:#e0e0e0

    class INPUT inputStyle
    class INTENT_DETECT,ENTITY_RECOG,COMPLEXITY_EST,LANG_ID queryStyle
    class MULTI_QUERY,HYDE,STEP_BACK,DECOMPOSE_Q queryStyle
    class TENANT_FILTER,DEPT_FILTER,ACL_FILTER,VERSION_FILTER,DATE_FILTER,COLLECTION_FILTER,DOCTYPE_FILTER filterStyle
    class QUERY_EMBED,ANN_SEARCH,MULTI_VEC searchStyle
    class BM25_QUERY,SPLADE_QUERY searchStyle
    class KG_QUERY,KG_EXPAND searchStyle
    class RRF_FUSION,WEIGHTED_FUSION,DEDUP searchStyle
    class CROSS_ENCODER,COLBERT_RERANK,LLM_RERANK,MMR_DIVERSITY,SCORE_NORMALIZE rerankStyle
    class PARENT_RETRIEVE,CONTEXT_WINDOW,COMPRESS,CITE_MAP,TOP_K_SELECT contextStyle
    class SYSTEM_PROMPT,CONTEXT_INJECT,MEMORY_INJECT,HISTORY_INJECT,CHAIN_OF_THOUGHT,FEW_SHOT,OUTPUT_FORMAT promptStyle
    class MODEL_SELECT,TOKEN_COUNT,STREAM_RESPONSE,STRUCTURED_OUTPUT llmStyle
    class CITE_ATTACH,CONFIDENCE,FORMAT_OUT,CACHE_RESPONSE postStyle
    class QDRANT_DB,ES_DB,NEO4J_DB,PG_DB,REDIS_DB dbStyle
    class FINAL_OUTPUT outputStyle
```

---

<br/>

<div align="center">

## Volume 6 — Agentic AI Platform (LangGraph)

*Multi-agent orchestration with state graphs, tool use, and human-in-the-loop*

</div>

```mermaid
---
title: "Volume 6 — Agentic AI Platform (LangGraph)"
---
%%{init: {'theme': 'dark', 'themeVariables': { 'primaryColor': '#1a1a2e', 'primaryTextColor': '#e0e0e0', 'primaryBorderColor': '#ff7043', 'lineColor': '#ff7043', 'secondaryColor': '#16213e', 'tertiaryColor': '#0f3460', 'fontFamily': 'Inter, sans-serif'}}}%%

flowchart TB

    %% ============================================
    %% ENTRY POINT
    %% ============================================

    TASK_INPUT["📋 Task Input<br/><i>Complex multi-step task<br/>from user or system</i>"]

    %% ============================================
    %% STATE GRAPH INITIALIZATION
    %% ============================================

    subgraph STATE_INIT["🔄 LangGraph State Initialization"]
        direction TB
        INIT_STATE["📊 Initialize AgentState<br/><i>messages: []<br/>plan: null<br/>tools_used: []<br/>iteration: 0<br/>max_iterations: 10<br/>status: STARTED</i>"]
        CHECKPOINTER["💾 Checkpoint Manager<br/><i>PostgreSQL Checkpointer<br/>State persistence<br/>Resume from failure</i>"]
        THREAD_MGR["🧵 Thread Manager<br/><i>Conversation thread<br/>Parallel execution<br/>Concurrency control</i>"]
    end

    TASK_INPUT --> INIT_STATE
    INIT_STATE --> CHECKPOINTER
    CHECKPOINTER --> THREAD_MGR

    %% ============================================
    %% PLANNER NODE
    %% ============================================

    subgraph PLANNER_NODE["📋 Planner Node"]
        direction TB

        TASK_ANALYZE["🔍 Task Analysis<br/><i>Understand user intent<br/>Identify requirements<br/>Detect ambiguity</i>"]
        DECOMPOSE_TASK["🧩 Task Decomposition<br/><i>Break into sub-tasks<br/>Identify dependencies<br/>Estimate complexity</i>"]
        DEPENDENCY_GRAPH["📊 Build Dependency Graph<br/><i>DAG of sub-tasks<br/>Parallel paths<br/>Critical path analysis</i>"]
        TOOL_ASSIGNMENT["🔧 Tool Assignment<br/><i>Map sub-tasks to tools<br/>Agent selection<br/>Resource estimation</i>"]
        PLAN_VALIDATE["✅ Plan Validation<br/><i>Feasibility check<br/>Resource availability<br/>Permission verification</i>"]

        TASK_ANALYZE --> DECOMPOSE_TASK
        DECOMPOSE_TASK --> DEPENDENCY_GRAPH
        DEPENDENCY_GRAPH --> TOOL_ASSIGNMENT
        TOOL_ASSIGNMENT --> PLAN_VALIDATE
    end

    THREAD_MGR --> TASK_ANALYZE

    %% ============================================
    %% TOOL SELECTOR NODE
    %% ============================================

    subgraph TOOL_SELECTOR["🔧 Tool Selector Node"]
        direction TB

        TOOL_REGISTRY["📋 Tool Registry<br/><i>Available tools catalog<br/>Capabilities matrix<br/>Rate limits</i>"]
        TOOL_MATCH["🎯 Tool Matching<br/><i>Semantic matching<br/>Capability scoring<br/>Cost estimation</i>"]
        TOOL_VALIDATE["✅ Tool Validation<br/><i>Schema validation<br/>Input type checking<br/>Permission check</i>"]
        TOOL_PREPARE["📦 Tool Preparation<br/><i>Input formatting<br/>Context injection<br/>Timeout configuration</i>"]

        TOOL_REGISTRY --> TOOL_MATCH
        TOOL_MATCH --> TOOL_VALIDATE
        TOOL_VALIDATE --> TOOL_PREPARE
    end

    PLAN_VALIDATE --> TOOL_REGISTRY

    %% ============================================
    %% AGENT COORDINATOR NODE
    %% ============================================

    subgraph COORDINATOR["🎯 Multi-Agent Coordinator"]
        direction TB

        DISPATCH_ENGINE["🚀 Dispatch Engine<br/><i>Task assignment<br/>Load balancing<br/>Priority queuing</i>"]
        PARALLEL_EXEC["⚡ Parallel Executor<br/><i>Concurrent agent execution<br/>Dependency-aware scheduling<br/>Max parallelism: 5</i>"]
        RESULT_AGGREGATOR["📊 Result Aggregator<br/><i>Merge agent outputs<br/>Conflict resolution<br/>Consensus building</i>"]
        STATE_UPDATER["🔄 State Updater<br/><i>Update AgentState<br/>Checkpoint progress<br/>Emit events</i>"]

        DISPATCH_ENGINE --> PARALLEL_EXEC
        PARALLEL_EXEC --> RESULT_AGGREGATOR
        RESULT_AGGREGATOR --> STATE_UPDATER
    end

    TOOL_PREPARE --> DISPATCH_ENGINE

    %% ============================================
    %% SPECIALIZED AGENTS
    %% ============================================

    subgraph RESEARCH_AGENT["🔍 Research Agent"]
        direction TB
        RA_PLAN["📋 Research Plan<br/><i>Identify sources<br/>Search strategy</i>"]
        RA_SEARCH["🔍 Multi-Source Search<br/><i>Internal docs<br/>Web search<br/>Knowledge base</i>"]
        RA_SYNTHESIZE["📝 Synthesize Findings<br/><i>Cross-reference sources<br/>Extract key insights</i>"]
        RA_CITE["📌 Generate Citations<br/><i>Source attribution<br/>Confidence scores</i>"]

        RA_PLAN --> RA_SEARCH
        RA_SEARCH --> RA_SYNTHESIZE
        RA_SYNTHESIZE --> RA_CITE
    end

    subgraph FINANCE_AGENT["💰 Finance Agent"]
        direction TB
        FA_DATA["📊 Gather Financial Data<br/><i>Revenue / Expenses<br/>Budgets / Forecasts</i>"]
        FA_ANALYZE["📈 Financial Analysis<br/><i>Ratio analysis<br/>Trend detection<br/>Anomaly flagging</i>"]
        FA_MODEL["🧮 Financial Modeling<br/><i>Projections<br/>Scenario analysis<br/>Monte Carlo</i>"]
        FA_REPORT["📋 Generate Report<br/><i>Financial summary<br/>Charts + Tables</i>"]

        FA_DATA --> FA_ANALYZE
        FA_ANALYZE --> FA_MODEL
        FA_MODEL --> FA_REPORT
    end

    subgraph SQL_AGENT["🗃️ SQL Agent"]
        direction TB
        SA_UNDERSTAND["🔍 Understand Query<br/><i>NL to SQL intent<br/>Schema awareness</i>"]
        SA_GENERATE["💻 Generate SQL<br/><i>Text-to-SQL<br/>Schema-aware generation<br/>Join optimization</i>"]
        SA_VALIDATE["✅ Validate SQL<br/><i>Syntax check<br/>Injection prevention<br/>Permission check</i>"]
        SA_EXECUTE["⚡ Execute Query<br/><i>Read-only mode<br/>Timeout: 30s<br/>Row limit: 10000</i>"]
        SA_FORMAT["📊 Format Results<br/><i>Tables / Charts<br/>Natural language summary</i>"]

        SA_UNDERSTAND --> SA_GENERATE
        SA_GENERATE --> SA_VALIDATE
        SA_VALIDATE --> SA_EXECUTE
        SA_EXECUTE --> SA_FORMAT
    end

    subgraph EMAIL_AGENT["📧 Email Agent"]
        direction TB
        EA_COMPOSE["📝 Compose Email<br/><i>Template selection<br/>Content generation<br/>Personalization</i>"]
        EA_REVIEW["👁️ Review Content<br/><i>Tone analysis<br/>Grammar check<br/>PII detection</i>"]
        EA_RECIPIENTS["👥 Resolve Recipients<br/><i>Contact lookup<br/>Distribution lists<br/>CC/BCC logic</i>"]
        EA_SEND["📤 Send Email<br/><i>SMTP / SendGrid<br/>Delivery tracking<br/>Read receipts</i>"]

        EA_COMPOSE --> EA_REVIEW
        EA_REVIEW --> EA_RECIPIENTS
        EA_RECIPIENTS --> EA_SEND
    end

    subgraph REPORT_AGENT["📊 Report Agent"]
        direction TB
        REPA_GATHER["📥 Gather Data<br/><i>Multiple data sources<br/>API calls<br/>Database queries</i>"]
        REPA_ANALYZE["🔍 Analyze Data<br/><i>Statistical analysis<br/>Pattern detection<br/>Outlier identification</i>"]
        REPA_VISUALIZE["📊 Create Visualizations<br/><i>Charts / Graphs<br/>Matplotlib / Plotly<br/>Interactive dashboards</i>"]
        REPA_GENERATE["📄 Generate Report<br/><i>PDF / DOCX / PPT<br/>Executive summary<br/>Detailed appendix</i>"]

        REPA_GATHER --> REPA_ANALYZE
        REPA_ANALYZE --> REPA_VISUALIZE
        REPA_VISUALIZE --> REPA_GENERATE
    end

    subgraph RISK_AGENT["⚠️ Risk Agent"]
        direction TB
        RISKA_ASSESS["🔍 Risk Assessment<br/><i>Identify potential risks<br/>Historical patterns</i>"]
        RISKA_SCORE["📊 Risk Scoring<br/><i>Probability × Impact<br/>Risk matrix</i>"]
        RISKA_MITIGATE["🛡️ Mitigation Plans<br/><i>Suggested controls<br/>Contingency plans</i>"]
        RISKA_MONITOR["📡 Monitoring Rules<br/><i>Alert thresholds<br/>Continuous monitoring</i>"]

        RISKA_ASSESS --> RISKA_SCORE
        RISKA_SCORE --> RISKA_MITIGATE
        RISKA_MITIGATE --> RISKA_MONITOR
    end

    %% ============================================
    %% COORDINATOR → AGENTS
    %% ============================================

    PARALLEL_EXEC --> RA_PLAN
    PARALLEL_EXEC --> FA_DATA
    PARALLEL_EXEC --> SA_UNDERSTAND
    PARALLEL_EXEC --> EA_COMPOSE
    PARALLEL_EXEC --> REPA_GATHER
    PARALLEL_EXEC --> RISKA_ASSESS

    RA_CITE --> RESULT_AGGREGATOR
    FA_REPORT --> RESULT_AGGREGATOR
    SA_FORMAT --> RESULT_AGGREGATOR
    EA_SEND --> RESULT_AGGREGATOR
    REPA_GENERATE --> RESULT_AGGREGATOR
    RISKA_MONITOR --> RESULT_AGGREGATOR

    %% ============================================
    %% REFLECTION & SELF-CORRECTION
    %% ============================================

    subgraph REFLECTION["🔄 Reflection & Self-Correction"]
        direction TB

        QUALITY_CHECK["✅ Quality Assessment<br/><i>Completeness check<br/>Accuracy validation<br/>Consistency check</i>"]
        CRITIC_AGENT["🧐 Critic Agent<br/><i>LLM-based review<br/>Identify gaps<br/>Suggest improvements</i>"]
        SHOULD_CONTINUE{"🔀 Continue?<br/><i>Quality threshold<br/>met?</i>"}
        REPLAN["📋 Re-Plan<br/><i>Adjust strategy<br/>Add missing steps<br/>Fix errors</i>"]
        ITERATION_CHECK{"🔢 Iteration Check<br/><i>iteration < max?</i>"}

        QUALITY_CHECK --> CRITIC_AGENT
        CRITIC_AGENT --> SHOULD_CONTINUE
    end

    STATE_UPDATER --> QUALITY_CHECK
    SHOULD_CONTINUE -->|"No — Quality < 0.85"| REPLAN
    REPLAN --> ITERATION_CHECK
    ITERATION_CHECK -->|"Yes — Continue"| TASK_ANALYZE
    ITERATION_CHECK -->|"No — Max Reached"| FORCE_OUTPUT
    SHOULD_CONTINUE -->|"Yes — Quality ≥ 0.85"| RISK_ASSESS

    FORCE_OUTPUT["⚠️ Force Output<br/><i>Best effort response<br/>With disclaimers</i>"]

    %% ============================================
    %% RISK ASSESSMENT & HUMAN-IN-THE-LOOP
    %% ============================================

    subgraph RISK_ASSESS["⚠️ Risk Assessment & Approval"]
        direction TB

        RISK_CLASSIFIER["🎲 Risk Classifier<br/><i>Action classification<br/>Read vs Write vs Delete<br/>Internal vs External</i>"]
        RISK_SCORING["📊 Risk Scoring<br/><i>Impact assessment<br/>Reversibility check<br/>Blast radius</i>"]
        RISK_DECISION{"⚠️ Risk Level?"}

        LOW_RISK["✅ Low Risk<br/><i>Auto-approve<br/>Log action</i>"]
        MEDIUM_RISK["⚡ Medium Risk<br/><i>Auto-approve<br/>with notification</i>"]
        HIGH_RISK["🛑 High Risk<br/><i>Human approval required<br/>Slack / Email notification<br/>Timeout: 24h</i>"]

        RISK_CLASSIFIER --> RISK_SCORING
        RISK_SCORING --> RISK_DECISION
        RISK_DECISION -->|Low| LOW_RISK
        RISK_DECISION -->|Medium| MEDIUM_RISK
        RISK_DECISION -->|High| HIGH_RISK

        APPROVAL_WAIT["⏳ Await Approval<br/><i>Human review<br/>Approve / Reject / Modify</i>"]
        APPROVAL_DECISION{"👨‍💼 Decision?"}

        HIGH_RISK --> APPROVAL_WAIT
        APPROVAL_WAIT --> APPROVAL_DECISION
    end

    %% ============================================
    %% TOOL EXECUTION
    %% ============================================

    subgraph TOOL_EXEC["⚡ Tool Execution Engine"]
        direction TB

        SANDBOX["🏗️ Sandbox Environment<br/><i>Isolated execution<br/>Resource limits<br/>Network policies</i>"]
        EXEC_ENGINE["⚙️ Execution Engine<br/><i>Tool invocation<br/>Timeout management<br/>Error handling</i>"]
        RESULT_VALIDATE["✅ Result Validation<br/><i>Output schema check<br/>Sanity validation<br/>Error detection</i>"]
        ROLLBACK["↩️ Rollback Handler<br/><i>Undo operations<br/>Compensating transactions<br/>State recovery</i>"]

        SANDBOX --> EXEC_ENGINE
        EXEC_ENGINE --> RESULT_VALIDATE
        RESULT_VALIDATE -->|Error| ROLLBACK
    end

    LOW_RISK --> SANDBOX
    MEDIUM_RISK --> SANDBOX
    APPROVAL_DECISION -->|Approved| SANDBOX
    APPROVAL_DECISION -->|Rejected| REJECTION_RESPONSE
    APPROVAL_DECISION -->|Modified| REPLAN

    REJECTION_RESPONSE["❌ Task Rejected<br/><i>Notify user<br/>Log decision</i>"]

    %% ============================================
    %% FINAL OUTPUT
    %% ============================================

    subgraph FINAL_NODE["📤 Final Output Assembly"]
        direction TB

        MERGE_RESULTS["🔗 Merge All Results<br/><i>Agent outputs<br/>Tool results<br/>Execution logs</i>"]
        FORMAT_RESPONSE["📝 Format Response<br/><i>Natural language summary<br/>Structured data<br/>Visualizations</i>"]
        ATTACH_ARTIFACTS["📎 Attach Artifacts<br/><i>Generated files<br/>Reports / Charts<br/>Execution logs</i>"]
        FINAL_STATE["📊 Final AgentState<br/><i>status: COMPLETED<br/>Checkpoint saved</i>"]

        MERGE_RESULTS --> FORMAT_RESPONSE
        FORMAT_RESPONSE --> ATTACH_ARTIFACTS
        ATTACH_ARTIFACTS --> FINAL_STATE
    end

    RESULT_VALIDATE -->|Success| MERGE_RESULTS
    FORCE_OUTPUT --> MERGE_RESULTS

    AGENT_OUTPUT["📤 Agent Response<br/><i>Answer + Artifacts +<br/>Execution Trace +<br/>Confidence Score</i>"]

    FINAL_STATE --> AGENT_OUTPUT

    %% ============================================
    %% STYLES
    %% ============================================

    classDef inputStyle fill:#1565c0,stroke:#42a5f5,stroke-width:2px,color:#e0e0e0
    classDef stateStyle fill:#4a148c,stroke:#ce93d8,stroke-width:2px,color:#e0e0e0
    classDef planStyle fill:#00695c,stroke:#4db6ac,stroke-width:2px,color:#e0e0e0
    classDef toolStyle fill:#283593,stroke:#7986cb,stroke-width:2px,color:#e0e0e0
    classDef coordStyle fill:#bf360c,stroke:#ff8a65,stroke-width:2px,color:#e0e0e0
    classDef agentStyle fill:#1b5e20,stroke:#66bb6a,stroke-width:2px,color:#e0e0e0
    classDef reflectStyle fill:#e65100,stroke:#ff9100,stroke-width:2px,color:#e0e0e0
    classDef riskStyle fill:#880e4f,stroke:#f06292,stroke-width:2px,color:#e0e0e0
    classDef execStyle fill:#311b92,stroke:#b388ff,stroke-width:2px,color:#e0e0e0
    classDef outputStyle fill:#004d40,stroke:#26a69a,stroke-width:3px,color:#e0e0e0

    class TASK_INPUT inputStyle
    class INIT_STATE,CHECKPOINTER,THREAD_MGR stateStyle
    class TASK_ANALYZE,DECOMPOSE_TASK,DEPENDENCY_GRAPH,TOOL_ASSIGNMENT,PLAN_VALIDATE planStyle
    class TOOL_REGISTRY,TOOL_MATCH,TOOL_VALIDATE,TOOL_PREPARE toolStyle
    class DISPATCH_ENGINE,PARALLEL_EXEC,RESULT_AGGREGATOR,STATE_UPDATER coordStyle
    class RA_PLAN,RA_SEARCH,RA_SYNTHESIZE,RA_CITE agentStyle
    class FA_DATA,FA_ANALYZE,FA_MODEL,FA_REPORT agentStyle
    class SA_UNDERSTAND,SA_GENERATE,SA_VALIDATE,SA_EXECUTE,SA_FORMAT agentStyle
    class EA_COMPOSE,EA_REVIEW,EA_RECIPIENTS,EA_SEND agentStyle
    class REPA_GATHER,REPA_ANALYZE,REPA_VISUALIZE,REPA_GENERATE agentStyle
    class RISKA_ASSESS,RISKA_SCORE,RISKA_MITIGATE,RISKA_MONITOR agentStyle
    class QUALITY_CHECK,CRITIC_AGENT,SHOULD_CONTINUE,REPLAN,ITERATION_CHECK reflectStyle
    class RISK_CLASSIFIER,RISK_SCORING,RISK_DECISION,LOW_RISK,MEDIUM_RISK,HIGH_RISK riskStyle
    class APPROVAL_WAIT,APPROVAL_DECISION riskStyle
    class SANDBOX,EXEC_ENGINE,RESULT_VALIDATE,ROLLBACK execStyle
    class MERGE_RESULTS,FORMAT_RESPONSE,ATTACH_ARTIFACTS,FINAL_STATE outputStyle
    class AGENT_OUTPUT,FORCE_OUTPUT,REJECTION_RESPONSE outputStyle
```

---

<br/>

<div align="center">

## Volume 7 — Memory Architecture

*Complete memory system: short-term, semantic, episodic, and long-term memory*

</div>

```mermaid
---
title: "Volume 7 — Memory Architecture"
---
%%{init: {'theme': 'dark', 'themeVariables': { 'primaryColor': '#1a1a2e', 'primaryTextColor': '#e0e0e0', 'primaryBorderColor': '#ab47bc', 'lineColor': '#ab47bc', 'secondaryColor': '#16213e', 'tertiaryColor': '#0f3460', 'fontFamily': 'Inter, sans-serif'}}}%%

flowchart TB

    %% ============================================
    %% MEMORY CONTROLLER
    %% ============================================

    INTERACTION["💬 User Interaction<br/><i>Query + Response pair</i>"]

    subgraph MEMORY_CONTROLLER["🧠 Memory Controller"]
        direction TB

        STORE_DECIDE["📋 Storage Decision Engine<br/><i>What to remember?<br/>Importance scoring<br/>Redundancy check</i>"]
        RECALL_DECIDE["🔍 Recall Decision Engine<br/><i>What to retrieve?<br/>Relevance scoring<br/>Recency weighting</i>"]
        CONSOLIDATE["🔄 Memory Consolidation<br/><i>Periodic consolidation<br/>Short-term → Long-term<br/>Importance-based promotion</i>"]
        FORGET_ENGINE["🗑️ Forgetting Engine<br/><i>Decay function<br/>Privacy-based deletion<br/>GDPR compliance</i>"]

        STORE_DECIDE --> RECALL_DECIDE
        RECALL_DECIDE --> CONSOLIDATE
        CONSOLIDATE --> FORGET_ENGINE
    end

    INTERACTION --> STORE_DECIDE

    %% ============================================
    %% SHORT-TERM MEMORY (STM)
    %% ============================================

    subgraph STM["⚡ Short-Term Memory (STM)"]
        direction TB

        subgraph STM_BUFFER["📋 Conversation Buffer"]
            SLIDING_WINDOW["📐 Sliding Window<br/><i>Last N messages<br/>N = 20 turns<br/>FIFO eviction</i>"]
            TOKEN_BUFFER["🔢 Token Buffer<br/><i>Max 8K tokens<br/>Truncate oldest<br/>Priority retention</i>"]
            SUMMARY_BUFFER["📝 Summary Buffer<br/><i>LLM-generated summary<br/>of evicted messages<br/>Compressed history</i>"]
        end

        subgraph STM_CONTEXT["🎯 Active Context"]
            CURRENT_QUERY["💬 Current Query<br/><i>Active user question</i>"]
            WORKING_MEMORY["🧩 Working Memory<br/><i>Intermediate results<br/>Reasoning steps<br/>Tool outputs</i>"]
            ATTENTION_FOCUS["🎯 Attention Focus<br/><i>Key entities mentioned<br/>Active topics<br/>User intent</i>"]
        end

        STM_STORE[("⚡ Redis<br/><i>TTL: 2 hours<br/>Key: session:{id}:stm<br/>Serialization: MessagePack</i>")]

        SLIDING_WINDOW --> SUMMARY_BUFFER
        TOKEN_BUFFER --> SUMMARY_BUFFER
        CURRENT_QUERY --> WORKING_MEMORY
        WORKING_MEMORY --> ATTENTION_FOCUS
    end

    STORE_DECIDE --> SLIDING_WINDOW
    STORE_DECIDE --> CURRENT_QUERY

    %% ============================================
    %% CONVERSATION MEMORY
    %% ============================================

    subgraph CONV_MEMORY["💬 Conversation Memory"]
        direction TB

        subgraph CONV_STORE_LAYER["📋 Conversation Store"]
            FULL_HISTORY["📜 Full Conversation History<br/><i>All messages stored<br/>User + Assistant + System<br/>Tool calls + Results</i>"]
            METADATA_STORE["🏷️ Conversation Metadata<br/><i>Start time / Duration<br/>Topic classification<br/>Participant info<br/>Satisfaction score</i>"]
            BRANCH_STORE["🔀 Conversation Branches<br/><i>Fork points<br/>Alternative paths<br/>Rollback support</i>"]
        end

        subgraph CONV_INDEX["🔍 Conversation Index"]
            TOPIC_INDEX["📑 Topic Index<br/><i>Topic → Conversation<br/>mapping for fast recall</i>"]
            ENTITY_INDEX["🏷️ Entity Index<br/><i>Mentioned entities<br/>→ Conversation mapping</i>"]
            TEMPORAL_INDEX["📅 Temporal Index<br/><i>Time-based retrieval<br/>Recent conversations first</i>"]
        end

        CONV_DB[("🐘 PostgreSQL<br/><i>Table: conversations<br/>Table: messages<br/>Table: conv_metadata<br/>Partitioned by tenant</i>")]

        FULL_HISTORY --> TOPIC_INDEX
        METADATA_STORE --> ENTITY_INDEX
        BRANCH_STORE --> TEMPORAL_INDEX
    end

    STORE_DECIDE --> FULL_HISTORY

    %% ============================================
    %% SEMANTIC MEMORY
    %% ============================================

    subgraph SEMANTIC_MEM["🧬 Semantic Memory"]
        direction TB

        subgraph KNOWLEDGE_STORE["📚 Knowledge Store"]
            FACTS["📋 Learned Facts<br/><i>User preferences<br/>Domain knowledge<br/>Extracted insights</i>"]
            BELIEFS["💡 Beliefs & Opinions<br/><i>User stated preferences<br/>Company policies<br/>Team conventions</i>"]
            SKILLS["🔧 Procedural Knowledge<br/><i>How to perform tasks<br/>Workflow patterns<br/>Best practices</i>"]
        end

        subgraph KNOWLEDGE_OPS["🔄 Knowledge Operations"]
            EXTRACT_KNOWLEDGE["🔍 Knowledge Extraction<br/><i>LLM extracts facts<br/>from conversations<br/>Importance: 0-1 score</i>"]
            EMBED_KNOWLEDGE["🧬 Embed Knowledge<br/><i>Generate embeddings<br/>for semantic search</i>"]
            UPDATE_KNOWLEDGE["🔄 Knowledge Update<br/><i>Merge with existing<br/>Resolve conflicts<br/>Version tracking</i>"]
            DECAY_KNOWLEDGE["📉 Knowledge Decay<br/><i>Reduce importance<br/>over time if not<br/>reinforced</i>"]
        end

        SEMANTIC_DB[("🧬 Qdrant<br/><i>Collection: semantic_memory<br/>Payload: {fact, importance,<br/>timestamp, source}</i>")]

        FACTS --> EXTRACT_KNOWLEDGE
        BELIEFS --> EXTRACT_KNOWLEDGE
        SKILLS --> EXTRACT_KNOWLEDGE
        EXTRACT_KNOWLEDGE --> EMBED_KNOWLEDGE
        EMBED_KNOWLEDGE --> UPDATE_KNOWLEDGE
        UPDATE_KNOWLEDGE --> DECAY_KNOWLEDGE
    end

    CONSOLIDATE --> EXTRACT_KNOWLEDGE

    %% ============================================
    %% EPISODIC MEMORY
    %% ============================================

    subgraph EPISODIC_MEM["📸 Episodic Memory"]
        direction TB

        subgraph EPISODE_STORE["📋 Episode Store"]
            EPISODES["📸 Episodes<br/><i>Discrete interaction events<br/>Task completions<br/>Key decisions made</i>"]
            OUTCOMES["📊 Outcomes<br/><i>Success / Failure<br/>User satisfaction<br/>Lessons learned</i>"]
            EMOTIONAL_CTX["💭 Emotional Context<br/><i>User sentiment<br/>Frustration detection<br/>Satisfaction indicators</i>"]
        end

        subgraph EPISODE_OPS["🔄 Episode Operations"]
            BOUNDARY_DETECT["🔍 Episode Boundary Detection<br/><i>Topic change detection<br/>Task completion signals<br/>Time gap detection</i>"]
            EPISODE_EMBED["🧬 Episode Embedding<br/><i>Summarize episode<br/>Generate embedding<br/>for future recall</i>"]
            SIMILAR_EPISODES["🔗 Find Similar Episodes<br/><i>Vector similarity search<br/>for relevant past<br/>experiences</i>"]
            LEARN_FROM["📚 Learn from Episodes<br/><i>Extract patterns<br/>Update preferences<br/>Improve responses</i>"]
        end

        EPISODIC_DB[("🧬 Qdrant<br/><i>Collection: episodic_memory<br/>Payload: {summary, outcome,<br/>sentiment, entities}</i>")]

        EPISODES --> BOUNDARY_DETECT
        OUTCOMES --> BOUNDARY_DETECT
        EMOTIONAL_CTX --> BOUNDARY_DETECT
        BOUNDARY_DETECT --> EPISODE_EMBED
        EPISODE_EMBED --> SIMILAR_EPISODES
        SIMILAR_EPISODES --> LEARN_FROM
    end

    CONSOLIDATE --> BOUNDARY_DETECT

    %% ============================================
    %% LONG-TERM MEMORY (LTM)
    %% ============================================

    subgraph LTM["🏛️ Long-Term Memory (LTM)"]
        direction TB

        subgraph LTM_STORE["📚 Long-Term Store"]
            USER_PROFILE["👤 User Profile Memory<br/><i>Communication style<br/>Technical level<br/>Role / Department<br/>Language preferences</i>"]
            DOMAIN_KNOWLEDGE["📖 Domain Knowledge<br/><i>Industry-specific facts<br/>Company terminology<br/>Product knowledge</i>"]
            INTERACTION_PATTERNS["📊 Interaction Patterns<br/><i>Common query types<br/>Peak usage times<br/>Preferred output format</i>"]
            RELATIONSHIP_MAP["🔗 Relationship Map<br/><i>Entity relationships<br/>Team structure<br/>Project associations</i>"]
        end

        subgraph LTM_OPS["🔄 LTM Operations"]
            IMPORTANCE_SCORE["📊 Importance Scoring<br/><i>Recency × Frequency ×<br/>Relevance × User Signal</i>"]
            SPACED_REPETITION["🔄 Spaced Repetition<br/><i>Reinforce important<br/>memories over time</i>"]
            MEMORY_MERGE["🔗 Memory Merging<br/><i>Combine similar memories<br/>Reduce redundancy<br/>Create abstractions</i>"]
            PRIVACY_FILTER["🔐 Privacy Filter<br/><i>PII redaction<br/>GDPR compliance<br/>Data retention policies</i>"]
        end

        LTM_PG[("🐘 PostgreSQL<br/><i>Table: user_memory<br/>Table: domain_knowledge<br/>Table: interaction_patterns<br/>RLS by tenant</i>")]

        LTM_VEC[("🧬 Qdrant<br/><i>Collection: long_term_memory<br/>Dense + Sparse vectors<br/>Filterable by user/tenant</i>")]

        USER_PROFILE --> IMPORTANCE_SCORE
        DOMAIN_KNOWLEDGE --> IMPORTANCE_SCORE
        INTERACTION_PATTERNS --> IMPORTANCE_SCORE
        RELATIONSHIP_MAP --> IMPORTANCE_SCORE
        IMPORTANCE_SCORE --> SPACED_REPETITION
        SPACED_REPETITION --> MEMORY_MERGE
        MEMORY_MERGE --> PRIVACY_FILTER
    end

    CONSOLIDATE --> IMPORTANCE_SCORE

    %% ============================================
    %% MEMORY RECALL PIPELINE
    %% ============================================

    subgraph RECALL_PIPELINE["🔍 Memory Recall Pipeline"]
        direction TB

        QUERY_ANALYZE["🔍 Analyze Query<br/><i>Extract entities<br/>Identify topics<br/>Detect temporal refs</i>"]
        PARALLEL_RECALL["⚡ Parallel Recall<br/><i>Search all memory<br/>stores simultaneously</i>"]
        STM_RECALL["⚡ STM Recall<br/><i>Recent context<br/>Active conversation</i>"]
        CONV_RECALL["💬 Conversation Recall<br/><i>Related past conversations<br/>Similar topics</i>"]
        SEMANTIC_RECALL["🧬 Semantic Recall<br/><i>Relevant facts<br/>Known preferences</i>"]
        EPISODIC_RECALL["📸 Episodic Recall<br/><i>Similar past experiences<br/>Relevant outcomes</i>"]
        LTM_RECALL["🏛️ LTM Recall<br/><i>User profile<br/>Domain knowledge</i>"]
        RANK_MEMORIES["📊 Rank & Fuse Memories<br/><i>Relevance scoring<br/>Recency weighting<br/>Importance weighting</i>"]
        CONTEXT_ASSEMBLE["📝 Assemble Context<br/><i>Structured memory context<br/>for prompt injection</i>"]
    end

    RECALL_DECIDE --> QUERY_ANALYZE
    QUERY_ANALYZE --> PARALLEL_RECALL
    PARALLEL_RECALL --> STM_RECALL
    PARALLEL_RECALL --> CONV_RECALL
    PARALLEL_RECALL --> SEMANTIC_RECALL
    PARALLEL_RECALL --> EPISODIC_RECALL
    PARALLEL_RECALL --> LTM_RECALL
    STM_RECALL --> RANK_MEMORIES
    CONV_RECALL --> RANK_MEMORIES
    SEMANTIC_RECALL --> RANK_MEMORIES
    EPISODIC_RECALL --> RANK_MEMORIES
    LTM_RECALL --> RANK_MEMORIES
    RANK_MEMORIES --> CONTEXT_ASSEMBLE

    MEMORY_OUTPUT["🧩 Memory Context<br/><i>Enriched context for<br/>prompt construction</i>"]

    CONTEXT_ASSEMBLE --> MEMORY_OUTPUT

    %% ============================================
    %% DATA STORE CONNECTIONS
    %% ============================================

    STM_RECALL --> STM_STORE
    CONV_RECALL --> CONV_DB
    SEMANTIC_RECALL --> SEMANTIC_DB
    EPISODIC_RECALL --> EPISODIC_DB
    LTM_RECALL --> LTM_PG
    LTM_RECALL --> LTM_VEC

    SLIDING_WINDOW --> STM_STORE
    FULL_HISTORY --> CONV_DB
    EMBED_KNOWLEDGE --> SEMANTIC_DB
    EPISODE_EMBED --> EPISODIC_DB
    PRIVACY_FILTER --> LTM_PG
    PRIVACY_FILTER --> LTM_VEC

    %% ============================================
    %% STYLES
    %% ============================================

    classDef controllerStyle fill:#4a148c,stroke:#ce93d8,stroke-width:2px,color:#e0e0e0
    classDef stmStyle fill:#1565c0,stroke:#42a5f5,stroke-width:2px,color:#e0e0e0
    classDef convStyle fill:#00695c,stroke:#4db6ac,stroke-width:2px,color:#e0e0e0
    classDef semanticStyle fill:#6a1b9a,stroke:#ab47bc,stroke-width:2px,color:#e0e0e0
    classDef episodicStyle fill:#283593,stroke:#5c6bc0,stroke-width:2px,color:#e0e0e0
    classDef ltmStyle fill:#bf360c,stroke:#ff8a65,stroke-width:2px,color:#e0e0e0
    classDef recallStyle fill:#1b5e20,stroke:#66bb6a,stroke-width:2px,color:#e0e0e0
    classDef dbStyle fill:#263238,stroke:#78909c,stroke-width:2px,color:#e0e0e0
    classDef outputStyle fill:#004d40,stroke:#26a69a,stroke-width:3px,color:#e0e0e0

    class STORE_DECIDE,RECALL_DECIDE,CONSOLIDATE,FORGET_ENGINE controllerStyle
    class SLIDING_WINDOW,TOKEN_BUFFER,SUMMARY_BUFFER,CURRENT_QUERY,WORKING_MEMORY,ATTENTION_FOCUS stmStyle
    class FULL_HISTORY,METADATA_STORE,BRANCH_STORE,TOPIC_INDEX,ENTITY_INDEX,TEMPORAL_INDEX convStyle
    class FACTS,BELIEFS,SKILLS,EXTRACT_KNOWLEDGE,EMBED_KNOWLEDGE,UPDATE_KNOWLEDGE,DECAY_KNOWLEDGE semanticStyle
    class EPISODES,OUTCOMES,EMOTIONAL_CTX,BOUNDARY_DETECT,EPISODE_EMBED,SIMILAR_EPISODES,LEARN_FROM episodicStyle
    class USER_PROFILE,DOMAIN_KNOWLEDGE,INTERACTION_PATTERNS,RELATIONSHIP_MAP ltmStyle
    class IMPORTANCE_SCORE,SPACED_REPETITION,MEMORY_MERGE,PRIVACY_FILTER ltmStyle
    class QUERY_ANALYZE,PARALLEL_RECALL,STM_RECALL,CONV_RECALL,SEMANTIC_RECALL,EPISODIC_RECALL,LTM_RECALL,RANK_MEMORIES,CONTEXT_ASSEMBLE recallStyle
    class STM_STORE,CONV_DB,SEMANTIC_DB,EPISODIC_DB,LTM_PG,LTM_VEC dbStyle
    class INTERACTION,MEMORY_OUTPUT outputStyle
```

---

<br/>

<div align="center">

## Volume 8 — Multi-Tenant Security

*Enterprise security architecture with OAuth, RBAC, ABAC, RLS, OPA, and Vault*

</div>

```mermaid
---
title: "Volume 8 — Multi-Tenant Security Architecture"
---
%%{init: {'theme': 'dark', 'themeVariables': { 'primaryColor': '#1a1a2e', 'primaryTextColor': '#e0e0e0', 'primaryBorderColor': '#ef5350', 'lineColor': '#ef5350', 'secondaryColor': '#16213e', 'tertiaryColor': '#0f3460', 'fontFamily': 'Inter, sans-serif'}}}%%

flowchart TB

    %% ============================================
    %% USER REQUEST
    %% ============================================

    REQUEST["🌐 Incoming Request<br/><i>API call from client<br/>Bearer token in header</i>"]

    %% ============================================
    %% AUTHENTICATION LAYER
    %% ============================================

    subgraph AUTH_LAYER["🔐 Authentication Layer"]
        direction TB

        subgraph OAUTH_FLOW["🔑 OAuth2 / OIDC Flow"]
            AUTH_CODE["📜 Authorization Code Flow<br/><i>Standard web apps<br/>PKCE for SPA / Mobile</i>"]
            CLIENT_CRED["🤖 Client Credentials Flow<br/><i>Service-to-service<br/>Machine accounts</i>"]
            DEVICE_CODE["📱 Device Code Flow<br/><i>CLI tools<br/>IoT devices</i>"]
            REFRESH_FLOW["🔄 Token Refresh Flow<br/><i>Rotating refresh tokens<br/>Absolute expiry: 7d</i>"]
        end

        subgraph SSO_PROVIDERS["🌐 SSO Providers"]
            KEYCLOAK["🔐 Keycloak<br/><i>Identity Provider<br/>Realm per Tenant<br/>User Federation</i>"]
            AZURE_AD["🟦 Azure AD / Entra<br/><i>Enterprise SSO<br/>SAML 2.0 + OIDC</i>"]
            OKTA["🟡 Okta<br/><i>Workforce Identity<br/>Universal Directory</i>"]
            GOOGLE_IDP["🔴 Google Workspace<br/><i>Google SSO<br/>Domain verification</i>"]
        end

        subgraph JWT_VALIDATION["📜 JWT Validation"]
            DECODE_JWT["🔍 Decode JWT<br/><i>Base64 decode<br/>Header / Payload / Signature</i>"]
            VERIFY_SIG["✅ Verify Signature<br/><i>RS256 / ES256<br/>JWKS endpoint rotation</i>"]
            CHECK_EXPIRY["⏰ Check Expiry<br/><i>exp claim validation<br/>Clock skew: 30s</i>"]
            CHECK_ISSUER["🏛️ Check Issuer<br/><i>iss claim validation<br/>Trusted issuers list</i>"]
            CHECK_AUDIENCE["🎯 Check Audience<br/><i>aud claim validation<br/>Service-specific audience</i>"]
            EXTRACT_CLAIMS["📋 Extract Claims<br/><i>sub / tenant_id / roles<br/>permissions / groups</i>"]
        end

        subgraph MFA_LAYER["🔒 Multi-Factor Authentication"]
            TOTP["📱 TOTP<br/><i>Google Authenticator<br/>Time-based OTP</i>"]
            WEBAUTHN["🔑 WebAuthn / FIDO2<br/><i>Hardware security keys<br/>Biometric authentication</i>"]
            PUSH_MFA["📲 Push Notification<br/><i>Mobile app approval<br/>Duo / Auth0 Guardian</i>"]
            SMS_MFA["📱 SMS OTP<br/><i>Fallback option<br/>Rate limited</i>"]
        end
    end

    REQUEST --> DECODE_JWT
    DECODE_JWT --> VERIFY_SIG
    VERIFY_SIG --> CHECK_EXPIRY
    CHECK_EXPIRY --> CHECK_ISSUER
    CHECK_ISSUER --> CHECK_AUDIENCE
    CHECK_AUDIENCE --> EXTRACT_CLAIMS

    AUTH_CODE --> KEYCLOAK
    CLIENT_CRED --> KEYCLOAK
    KEYCLOAK --> DECODE_JWT

    %% ============================================
    %% TENANT ISOLATION
    %% ============================================

    subgraph TENANT_ISOLATION["🏢 Tenant Isolation Layer"]
        direction TB

        TENANT_RESOLVE["🔍 Tenant Resolution<br/><i>From JWT: tenant_id claim<br/>From Header: X-Tenant-ID<br/>From subdomain: {tenant}.app.com</i>"]
        TENANT_VALIDATE["✅ Tenant Validation<br/><i>Active tenant check<br/>Subscription status<br/>Feature flags</i>"]
        TENANT_CONTEXT["📋 Set Tenant Context<br/><i>ThreadLocal: tenantId<br/>PostgreSQL: SET app.tenant_id<br/>Propagate to downstream</i>"]

        subgraph DB_ISOLATION["💾 Database Isolation"]
            RLS_PG["🐘 Row-Level Security<br/><i>PostgreSQL RLS Policies<br/>CREATE POLICY tenant_isolation<br/>ON documents<br/>USING tenant_id = current_setting<br/>app.tenant_id</i>"]
            SCHEMA_ISOLATION["📊 Schema Isolation<br/><i>Schema per tenant (optional)<br/>tenant_1.documents<br/>tenant_2.documents</i>"]
            CONNECTION_POOL["🔗 Connection Pooling<br/><i>PgBouncer per tenant<br/>Max connections per tenant<br/>Query timeout per tier</i>"]
        end

        subgraph VECTOR_ISOLATION["🧬 Vector DB Isolation"]
            COLLECTION_PER_TENANT["📁 Collection per Tenant<br/><i>Qdrant: tenant_{id}_docs<br/>Physical isolation<br/>Independent scaling</i>"]
            PAYLOAD_FILTER["🏷️ Payload Filtering<br/><i>Must filter: tenant_id<br/>Pre-filter before ANN<br/>Zero cross-contamination</i>"]
        end

        subgraph CACHE_ISOLATION["⚡ Cache Isolation"]
            REDIS_PREFIX["🔑 Key Prefixing<br/><i>tenant:{id}:session:{sid}<br/>Namespace isolation</i>"]
            REDIS_DB_NUM["🔢 Database Number<br/><i>Redis DB per tenant<br/>or key prefix</i>"]
        end

        TENANT_RESOLVE --> TENANT_VALIDATE
        TENANT_VALIDATE --> TENANT_CONTEXT
    end

    EXTRACT_CLAIMS --> TENANT_RESOLVE

    %% ============================================
    %% AUTHORIZATION ENGINE
    %% ============================================

    subgraph AUTHZ_ENGINE["👤 Authorization Engine"]
        direction TB

        subgraph RBAC_SYSTEM["👤 RBAC — Role-Based Access Control"]
            ROLE_HIERARCHY["📊 Role Hierarchy<br/><i>Super Admin<br/>├─ Tenant Admin<br/>│  ├─ Manager<br/>│  │  ├─ Editor<br/>│  │  │  └─ Viewer<br/>│  │  └─ Contributor<br/>│  └─ Auditor<br/>└─ System Service</i>"]
            ROLE_PERMISSIONS["🔧 Role → Permissions<br/><i>Admin: *.*.* (all)<br/>Manager: read.* + write.own<br/>Editor: read.* + write.assigned<br/>Viewer: read.allowed</i>"]
            ROLE_RESOLVE["🔍 Resolve User Roles<br/><i>From JWT claims<br/>From Keycloak realm roles<br/>From group membership</i>"]
        end

        subgraph ABAC_SYSTEM["🏷️ ABAC — Attribute-Based Access Control"]
            USER_ATTRS["👤 User Attributes<br/><i>department<br/>clearance_level<br/>location<br/>employment_type</i>"]
            RESOURCE_ATTRS["📋 Resource Attributes<br/><i>classification<br/>department<br/>created_by<br/>sensitivity_level</i>"]
            ENV_ATTRS["🌍 Environment Attributes<br/><i>time_of_day<br/>ip_address<br/>device_type<br/>network_zone</i>"]
            ABAC_EVAL["🔍 ABAC Evaluation<br/><i>IF user.dept == resource.dept<br/>AND user.clearance >= resource.level<br/>AND env.network == 'corporate'<br/>THEN allow</i>"]

            USER_ATTRS --> ABAC_EVAL
            RESOURCE_ATTRS --> ABAC_EVAL
            ENV_ATTRS --> ABAC_EVAL
        end

        subgraph DOC_ACL["📄 Document-Level ACL"]
            ACL_MATRIX["📊 ACL Matrix<br/><i>Document × User/Group<br/>Read / Write / Delete<br/>Share / Admin</i>"]
            INHERIT_ACL["🔗 ACL Inheritance<br/><i>Folder → Document<br/>Collection → Chunk<br/>Workspace → Collection</i>"]
            SHARE_MODEL["🤝 Sharing Model<br/><i>Private<br/>Team-shared<br/>Department-wide<br/>Organization-wide</i>"]
        end

        subgraph OPA_ENGINE["📜 OPA — Open Policy Agent"]
            REGO_POLICIES["📝 Rego Policies<br/><i>Declarative policy language<br/>Versioned in Git<br/>Hot-reloadable</i>"]
            POLICY_DECISION["⚖️ Policy Decision Point<br/><i>Evaluate all policies<br/>Return allow / deny<br/>+ reason</i>"]
            POLICY_DATA["📊 Policy Data<br/><i>External data bundles<br/>Periodic refresh<br/>Cached locally</i>"]

            REGO_POLICIES --> POLICY_DECISION
            POLICY_DATA --> POLICY_DECISION
        end
    end

    TENANT_CONTEXT --> ROLE_RESOLVE
    ROLE_RESOLVE --> ROLE_PERMISSIONS
    ROLE_PERMISSIONS --> ABAC_EVAL
    ABAC_EVAL --> POLICY_DECISION

    %% ============================================
    %% SECRETS MANAGEMENT
    %% ============================================

    subgraph SECRETS_MGR["🏦 Secrets Management"]
        direction TB

        VAULT_CORE["🏦 HashiCorp Vault<br/><i>KV v2 Secrets Engine<br/>Transit Engine (encryption)<br/>PKI Engine (certificates)</i>"]
        DYNAMIC_SECRETS["🔄 Dynamic Secrets<br/><i>Database credentials<br/>Lease: 1 hour<br/>Auto-rotation</i>"]
        TRANSIT_ENCRYPT["🔐 Transit Encryption<br/><i>Encrypt-as-a-Service<br/>AES-256-GCM<br/>Key rotation</i>"]
        SEAL_UNSEAL["🔒 Seal / Unseal<br/><i>Shamir's Secret Sharing<br/>Auto-unseal via KMS</i>"]
        AUDIT_VAULT["📋 Vault Audit Log<br/><i>All access logged<br/>File + Syslog backend<br/>Tamper-evident</i>"]

        VAULT_CORE --> DYNAMIC_SECRETS
        VAULT_CORE --> TRANSIT_ENCRYPT
        VAULT_CORE --> SEAL_UNSEAL
        VAULT_CORE --> AUDIT_VAULT
    end

    %% ============================================
    %% AI-SPECIFIC SECURITY
    %% ============================================

    subgraph AI_SECURITY["🤖 AI-Specific Security"]
        direction TB

        subgraph INPUT_GUARD["🛡️ Input Guardrails"]
            PROMPT_INJECT_DETECT["💉 Prompt Injection Detection<br/><i>Classifier model<br/>Pattern matching<br/>Semantic analysis</i>"]
            JAILBREAK_DETECT["🔓 Jailbreak Detection<br/><i>Known jailbreak patterns<br/>Adversarial input detection<br/>Red-team tested</i>"]
            PII_DETECT["🔍 PII Detection<br/><i>Microsoft Presidio<br/>Regex + NER<br/>SSN / CC / Email / Phone</i>"]
            PII_REDACT["🔐 PII Redaction<br/><i>Replace with tokens<br/>[REDACTED_SSN]<br/>Reversible for authorized</i>"]
        end

        subgraph OUTPUT_GUARD["🛡️ Output Guardrails"]
            CONTENT_FILTER["🚫 Content Filter<br/><i>Toxicity detection<br/>Harmful content blocking<br/>Bias detection</i>"]
            LEAK_PREVENT["🕵️ Data Leak Prevention<br/><i>Cross-tenant data check<br/>Sensitive data detection<br/>PII in output check</i>"]
            RESPONSE_SANITIZE["🧹 Response Sanitization<br/><i>Remove internal IDs<br/>Strip debug info<br/>Format validation</i>"]
        end

        subgraph RED_TEAM["🔴 Red Teaming"]
            ADVERSARIAL_TEST["⚔️ Adversarial Testing<br/><i>Automated attack simulation<br/>Fuzzing inputs<br/>Boundary testing</i>"]
            BIAS_AUDIT["⚖️ Bias Audit<br/><i>Fairness metrics<br/>Demographic parity<br/>Equal opportunity</i>"]
            SECURITY_SCAN["🔍 Security Scanning<br/><i>OWASP LLM Top 10<br/>Continuous scanning<br/>Vulnerability tracking</i>"]
        end
    end

    POLICY_DECISION --> PROMPT_INJECT_DETECT
    PROMPT_INJECT_DETECT --> JAILBREAK_DETECT
    JAILBREAK_DETECT --> PII_DETECT
    PII_DETECT --> PII_REDACT

    %% ============================================
    %% COMPLIANCE & AUDIT
    %% ============================================

    subgraph COMPLIANCE["📋 Compliance & Audit"]
        direction TB

        IMMUTABLE_LOG["📜 Immutable Audit Log<br/><i>Every access logged<br/>Append-only storage<br/>Cryptographic chaining</i>"]
        GDPR_MODULE["🇪🇺 GDPR Compliance<br/><i>Right to be forgotten<br/>Data portability<br/>Consent management</i>"]
        SOC2_MODULE["🏛️ SOC 2 Compliance<br/><i>Security controls<br/>Availability monitoring<br/>Processing integrity</i>"]
        DATA_RETENTION["📅 Data Retention<br/><i>Configurable per tenant<br/>Auto-purge policies<br/>Legal hold support</i>"]

        IMMUTABLE_LOG --> GDPR_MODULE
        GDPR_MODULE --> SOC2_MODULE
        SOC2_MODULE --> DATA_RETENTION
    end

    PII_REDACT --> IMMUTABLE_LOG
    AUDIT_VAULT --> IMMUTABLE_LOG

    %% ============================================
    %% FINAL SECURITY GATE
    %% ============================================

    AUTHORIZED["✅ Request Authorized<br/><i>Proceed to service<br/>with security context</i>"]

    POLICY_DECISION -->|Allow| AUTHORIZED
    POLICY_DECISION -->|Deny| DENIED

    DENIED["❌ Access Denied<br/><i>HTTP 403 Forbidden<br/>Audit log entry<br/>Security alert</i>"]

    %% ============================================
    %% STYLES
    %% ============================================

    classDef requestStyle fill:#1565c0,stroke:#42a5f5,stroke-width:2px,color:#e0e0e0
    classDef authStyle fill:#4a148c,stroke:#ce93d8,stroke-width:2px,color:#e0e0e0
    classDef tenantStyle fill:#bf360c,stroke:#ff8a65,stroke-width:2px,color:#e0e0e0
    classDef rbacStyle fill:#00695c,stroke:#4db6ac,stroke-width:2px,color:#e0e0e0
    classDef abacStyle fill:#283593,stroke:#7986cb,stroke-width:2px,color:#e0e0e0
    classDef opaStyle fill:#1b5e20,stroke:#66bb6a,stroke-width:2px,color:#e0e0e0
    classDef vaultStyle fill:#e65100,stroke:#ff9100,stroke-width:2px,color:#e0e0e0
    classDef aiSecStyle fill:#880e4f,stroke:#f06292,stroke-width:2px,color:#e0e0e0
    classDef complianceStyle fill:#263238,stroke:#90a4ae,stroke-width:2px,color:#e0e0e0
    classDef gateStyle fill:#004d40,stroke:#26a69a,stroke-width:3px,color:#e0e0e0
    classDef denyStyle fill:#b71c1c,stroke:#ef5350,stroke-width:3px,color:#e0e0e0

    class REQUEST requestStyle
    class AUTH_CODE,CLIENT_CRED,DEVICE_CODE,REFRESH_FLOW authStyle
    class KEYCLOAK,AZURE_AD,OKTA,GOOGLE_IDP authStyle
    class DECODE_JWT,VERIFY_SIG,CHECK_EXPIRY,CHECK_ISSUER,CHECK_AUDIENCE,EXTRACT_CLAIMS authStyle
    class TOTP,WEBAUTHN,PUSH_MFA,SMS_MFA authStyle
    class TENANT_RESOLVE,TENANT_VALIDATE,TENANT_CONTEXT tenantStyle
    class RLS_PG,SCHEMA_ISOLATION,CONNECTION_POOL tenantStyle
    class COLLECTION_PER_TENANT,PAYLOAD_FILTER tenantStyle
    class REDIS_PREFIX,REDIS_DB_NUM tenantStyle
    class ROLE_HIERARCHY,ROLE_PERMISSIONS,ROLE_RESOLVE rbacStyle
    class USER_ATTRS,RESOURCE_ATTRS,ENV_ATTRS,ABAC_EVAL abacStyle
    class ACL_MATRIX,INHERIT_ACL,SHARE_MODEL abacStyle
    class REGO_POLICIES,POLICY_DECISION,POLICY_DATA opaStyle
    class VAULT_CORE,DYNAMIC_SECRETS,TRANSIT_ENCRYPT,SEAL_UNSEAL,AUDIT_VAULT vaultStyle
    class PROMPT_INJECT_DETECT,JAILBREAK_DETECT,PII_DETECT,PII_REDACT aiSecStyle
    class CONTENT_FILTER,LEAK_PREVENT,RESPONSE_SANITIZE aiSecStyle
    class ADVERSARIAL_TEST,BIAS_AUDIT,SECURITY_SCAN aiSecStyle
    class IMMUTABLE_LOG,GDPR_MODULE,SOC2_MODULE,DATA_RETENTION complianceStyle
    class AUTHORIZED gateStyle
    class DENIED denyStyle
```

---

<br/>

<div align="center">

## Volume 9 — Monitoring & Evaluation

*Complete observability stack with Prometheus, Grafana, RAGAS, DeepEval, and LLM Judge*

</div>

```mermaid
---
title: "Volume 9 — Monitoring & Evaluation"
---
%%{init: {'theme': 'dark', 'themeVariables': { 'primaryColor': '#1a1a2e', 'primaryTextColor': '#e0e0e0', 'primaryBorderColor': '#26c6da', 'lineColor': '#26c6da', 'secondaryColor': '#16213e', 'tertiaryColor': '#0f3460', 'fontFamily': 'Inter, sans-serif'}}}%%

flowchart TB

    %% ============================================
    %% APPLICATION LAYER (Sources)
    %% ============================================

    subgraph APP_SOURCES["🧠 Application Sources"]
        direction LR
        MICROSERVICES["🌱 Spring Boot Microservices<br/><i>25+ services<br/>Micrometer metrics</i>"]
        KAFKA_SRC["📨 Kafka<br/><i>Consumer lag<br/>Throughput metrics</i>"]
        LLM_CALLS["🧠 LLM API Calls<br/><i>Latency / Tokens / Cost<br/>Error rates</i>"]
        RAG_PIPELINE["📚 RAG Pipeline<br/><i>Retrieval quality<br/>Reranking scores</i>"]
        AGENTS_SRC["🤖 AI Agents<br/><i>Execution traces<br/>Tool usage</i>"]
    end

    %% ============================================
    %% OPENTELEMETRY COLLECTION
    %% ============================================

    subgraph OTEL_LAYER["📡 OpenTelemetry Collection Layer"]
        direction TB

        subgraph INSTRUMENTATION["🔧 Auto-Instrumentation"]
            JAVA_AGENT["☕ Java Agent<br/><i>Spring Boot auto-instrumentation<br/>HTTP / gRPC / JDBC / Redis<br/>Kafka producer/consumer</i>"]
            PYTHON_SDK["🐍 Python SDK<br/><i>LangChain / LangGraph<br/>LLM call tracing<br/>Custom spans</i>"]
            CUSTOM_METRICS["📊 Custom Metrics<br/><i>token_usage_total<br/>retrieval_latency_seconds<br/>llm_request_duration<br/>rerank_score_histogram</i>"]
        end

        subgraph OTEL_COLLECTOR_CLUSTER["📡 OTel Collector Cluster"]
            RECEIVER["📥 Receivers<br/><i>OTLP gRPC :4317<br/>OTLP HTTP :4318<br/>Prometheus :9090<br/>Jaeger :14268</i>"]
            PROCESSOR["⚙️ Processors<br/><i>Batch processor<br/>Memory limiter<br/>Attribute processor<br/>Tail-based sampling</i>"]
            EXPORTER["📤 Exporters<br/><i>Prometheus remote write<br/>Loki push<br/>Tempo OTLP<br/>S3 archive</i>"]

            RECEIVER --> PROCESSOR
            PROCESSOR --> EXPORTER
        end
    end

    MICROSERVICES --> JAVA_AGENT
    LLM_CALLS --> PYTHON_SDK
    KAFKA_SRC --> JAVA_AGENT
    RAG_PIPELINE --> PYTHON_SDK
    AGENTS_SRC --> PYTHON_SDK
    JAVA_AGENT --> RECEIVER
    PYTHON_SDK --> RECEIVER
    CUSTOM_METRICS --> RECEIVER

    %% ============================================
    %% METRICS PIPELINE
    %% ============================================

    subgraph METRICS_PIPELINE["📈 Metrics Pipeline"]
        direction TB

        PROMETHEUS_SVR["📈 Prometheus<br/><i>TSDB storage: 90 days<br/>Scrape interval: 15s<br/>Remote write to Thanos</i>"]

        subgraph KEY_METRICS["📊 Key Metrics"]
            SYS_METRICS["🖥️ System Metrics<br/><i>cpu_usage_percent<br/>memory_usage_bytes<br/>disk_io_bytes<br/>network_bytes</i>"]
            APP_METRICS["🌱 Application Metrics<br/><i>http_request_duration_seconds<br/>http_requests_total<br/>active_connections<br/>thread_pool_size</i>"]
            AI_METRICS["🧠 AI-Specific Metrics<br/><i>llm_tokens_total{model,type}<br/>llm_latency_seconds{model}<br/>llm_cost_dollars{model}<br/>llm_errors_total{model,error}</i>"]
            RAG_METRICS["📚 RAG Metrics<br/><i>retrieval_precision<br/>retrieval_recall<br/>rerank_ndcg<br/>context_relevance_score</i>"]
            BIZ_METRICS["💼 Business Metrics<br/><i>queries_per_tenant<br/>cost_per_query<br/>user_satisfaction_score<br/>resolution_rate</i>"]
        end

        THANOS["🏔️ Thanos<br/><i>Long-term storage<br/>Global query view<br/>Downsampling</i>"]

        PROMETHEUS_SVR --> THANOS
    end

    EXPORTER --> PROMETHEUS_SVR

    %% ============================================
    %% LOGGING PIPELINE
    %% ============================================

    subgraph LOG_PIPELINE["📝 Logging Pipeline"]
        direction TB

        LOKI_SVR["📝 Loki<br/><i>Log aggregation<br/>Label-based indexing<br/>LogQL queries</i>"]

        subgraph LOG_TYPES["📋 Log Types"]
            ACCESS_LOGS["🔗 Access Logs<br/><i>HTTP method / path / status<br/>Response time / User-Agent<br/>Tenant ID / User ID</i>"]
            APP_LOGS["🌱 Application Logs<br/><i>Structured JSON logs<br/>Correlation IDs<br/>Error stack traces</i>"]
            AUDIT_LOGS["📋 Audit Logs<br/><i>Who did what, when<br/>Immutable records<br/>GDPR compliance</i>"]
            AI_LOGS["🧠 AI Logs<br/><i>Prompts sent / received<br/>Token counts<br/>Model selection reasoning</i>"]
            SECURITY_LOGS["🔒 Security Logs<br/><i>Auth failures<br/>Rate limit hits<br/>Suspicious patterns</i>"]
        end

        LOG_ARCHIVE["📦 Log Archive<br/><i>S3 cold storage<br/>Retention: 1 year<br/>Compressed Parquet</i>"]

        LOKI_SVR --> LOG_ARCHIVE
    end

    EXPORTER --> LOKI_SVR

    %% ============================================
    %% TRACING PIPELINE
    %% ============================================

    subgraph TRACE_PIPELINE["🔗 Distributed Tracing"]
        direction TB

        TEMPO_SVR["🔗 Tempo<br/><i>Trace storage<br/>TraceQL queries<br/>Exemplar linking</i>"]

        subgraph TRACE_TYPES["🔍 Trace Types"]
            E2E_TRACE["🔗 End-to-End Query Trace<br/><i>User → Gateway → Auth →<br/>Router → Retrieval → Rerank →<br/>LLM → Evaluation → Response</i>"]
            RAG_TRACE["📚 RAG Pipeline Trace<br/><i>Query → Filter → BM25 →<br/>Vector → Merge → Rerank →<br/>Compress → Prompt → Generate</i>"]
            AGENT_TRACE["🤖 Agent Execution Trace<br/><i>Plan → Tool Select →<br/>Execute → Reflect →<br/>Continue/Stop</i>"]
            INGESTION_TRACE["📥 Ingestion Trace<br/><i>Upload → Parse → OCR →<br/>Chunk → Embed → Index</i>"]
        end

        JAEGER_UI["🔍 Jaeger UI<br/><i>Trace visualization<br/>Service dependency map<br/>Latency analysis</i>"]

        TEMPO_SVR --> JAEGER_UI
    end

    EXPORTER --> TEMPO_SVR

    %% ============================================
    %% DASHBOARDS
    %% ============================================

    subgraph DASHBOARDS["📊 Grafana Dashboards"]
        direction TB

        GRAFANA_SVR["📊 Grafana<br/><i>Unified observability<br/>Data source federation</i>"]

        subgraph DASHBOARD_LIST["📋 Dashboard Gallery"]
            DASH_OVERVIEW["🏠 Platform Overview<br/><i>Total queries / Uptime<br/>Error rate / Active users<br/>Cost tracking</i>"]
            DASH_LLM["🧠 LLM Performance<br/><i>Latency P50/P95/P99<br/>Token throughput<br/>Cost per model<br/>Error rates by provider</i>"]
            DASH_RAG["📚 RAG Quality<br/><i>Retrieval precision/recall<br/>Reranking effectiveness<br/>Chunk utilization<br/>Cache hit rate</i>"]
            DASH_AGENT["🤖 Agent Monitoring<br/><i>Execution success rate<br/>Average iterations<br/>Tool usage frequency<br/>Human approval rate</i>"]
            DASH_TENANT["🏢 Tenant Analytics<br/><i>Usage per tenant<br/>Cost allocation<br/>Quota utilization<br/>SLA compliance</i>"]
            DASH_SECURITY["🔒 Security Dashboard<br/><i>Auth failures<br/>Injection attempts<br/>Rate limit triggers<br/>Anomaly detection</i>"]
            DASH_INFRA["☸️ Infrastructure<br/><i>K8s pod health<br/>Node utilization<br/>Kafka lag<br/>DB connections</i>"]
        end

        GRAFANA_SVR --> DASH_OVERVIEW
        GRAFANA_SVR --> DASH_LLM
        GRAFANA_SVR --> DASH_RAG
        GRAFANA_SVR --> DASH_AGENT
        GRAFANA_SVR --> DASH_TENANT
        GRAFANA_SVR --> DASH_SECURITY
        GRAFANA_SVR --> DASH_INFRA
    end

    PROMETHEUS_SVR --> GRAFANA_SVR
    LOKI_SVR --> GRAFANA_SVR
    TEMPO_SVR --> GRAFANA_SVR

    %% ============================================
    %% ALERTING
    %% ============================================

    subgraph ALERTING["🚨 Alerting System"]
        direction TB

        ALERTMANAGER_SVR["🚨 Alertmanager<br/><i>Alert routing<br/>Deduplication<br/>Silencing / Inhibition</i>"]

        subgraph ALERT_RULES["📋 Alert Rules"]
            ALERT_LLM["🧠 LLM Alerts<br/><i>P95 latency > 10s<br/>Error rate > 5%<br/>Token budget exceeded</i>"]
            ALERT_RAG["📚 RAG Alerts<br/><i>Retrieval precision < 0.7<br/>Hallucination rate > 10%<br/>Reranker timeout</i>"]
            ALERT_INFRA["☸️ Infra Alerts<br/><i>Pod CrashLoopBackOff<br/>CPU > 90%<br/>Disk > 85%</i>"]
            ALERT_SECURITY["🔒 Security Alerts<br/><i>Brute force detected<br/>Injection pattern<br/>Data exfiltration</i>"]
            ALERT_BUSINESS["💼 Business Alerts<br/><i>Query volume spike<br/>Cost anomaly<br/>Tenant quota 90%</i>"]
        end

        subgraph ALERT_CHANNELS["📣 Alert Channels"]
            PAGERDUTY["📟 PagerDuty<br/><i>P1/P2 incidents<br/>On-call rotation</i>"]
            SLACK_ALERT["💬 Slack<br/><i>#alerts-platform<br/>#alerts-security</i>"]
            EMAIL_ALERT["📧 Email<br/><i>Daily digest<br/>Critical immediate</i>"]
            WEBHOOK_ALERT["🔗 Webhook<br/><i>ServiceNow<br/>Custom integrations</i>"]
        end

        ALERTMANAGER_SVR --> PAGERDUTY
        ALERTMANAGER_SVR --> SLACK_ALERT
        ALERTMANAGER_SVR --> EMAIL_ALERT
        ALERTMANAGER_SVR --> WEBHOOK_ALERT
    end

    PROMETHEUS_SVR --> ALERTMANAGER_SVR

    %% ============================================
    %% AI EVALUATION ENGINE
    %% ============================================

    subgraph EVAL_ENGINE["🎯 AI Evaluation Engine"]
        direction TB

        subgraph RAGAS_EVAL["📊 RAGAS Framework"]
            FAITHFULNESS["🎯 Faithfulness<br/><i>Answer grounded in context?<br/>Claim decomposition<br/>NLI verification</i>"]
            ANSWER_RELEVANCE["📋 Answer Relevance<br/><i>Does answer address<br/>the question?<br/>Reverse question gen</i>"]
            CONTEXT_PRECISION["🎯 Context Precision<br/><i>Are retrieved chunks<br/>actually relevant?<br/>Weighted scoring</i>"]
            CONTEXT_RECALL["📊 Context Recall<br/><i>Were all needed chunks<br/>retrieved?<br/>Ground truth comparison</i>"]
            CONTEXT_RELEVANCE_M["🔍 Context Relevance<br/><i>Relevance of each<br/>retrieved sentence<br/>to the query</i>"]
        end

        subgraph DEEPEVAL_METRICS["📈 DeepEval Metrics"]
            G_EVAL["📊 G-Eval<br/><i>GPT-4 based evaluation<br/>Custom criteria<br/>Chain-of-thought scoring</i>"]
            BIAS_METRIC["⚖️ Bias Metric<br/><i>Gender / Race / Age<br/>bias detection<br/>Fairness scoring</i>"]
            TOXICITY_METRIC["🚫 Toxicity Metric<br/><i>Harmful content detection<br/>Severity scoring<br/>Category classification</i>"]
            HALLUCINATION_METRIC["🚨 Hallucination Metric<br/><i>Factual consistency<br/>Contradiction detection<br/>Source verification</i>"]
            SUMMARIZATION_METRIC["📝 Summarization Quality<br/><i>Coverage score<br/>Alignment score<br/>Coherence score</i>"]
        end

        subgraph LLM_JUDGE_SYSTEM["⚖️ LLM-as-Judge"]
            JUDGE_MODEL["🧠 Judge Model<br/><i>GPT-4 Turbo evaluator<br/>Custom rubric<br/>Structured output</i>"]
            PAIRWISE_COMPARE["🔄 Pairwise Comparison<br/><i>Compare responses<br/>from different models<br/>A/B evaluation</i>"]
            REFERENCE_EVAL["📋 Reference-Based Eval<br/><i>Compare against<br/>golden answers<br/>Semantic similarity</i>"]
            RUBRIC_SCORING["📊 Rubric Scoring<br/><i>1-5 scale on:<br/>Accuracy / Completeness /<br/>Clarity / Helpfulness</i>"]
        end

        subgraph CUSTOM_EVAL["🔧 Custom Evaluations"]
            LATENCY_EVAL["⏱️ Latency Budget<br/><i>E2E < 5s (P95)<br/>Retrieval < 500ms<br/>LLM < 3s</i>"]
            COST_EVAL["💰 Cost Efficiency<br/><i>Cost per query<br/>Token efficiency<br/>Cache savings</i>"]
            CITATION_EVAL["📌 Citation Accuracy<br/><i>Source link validity<br/>Page/section accuracy<br/>Chunk mapping correctness</i>"]
        end
    end

    AI_LOGS --> FAITHFULNESS
    AI_LOGS --> G_EVAL
    AI_LOGS --> JUDGE_MODEL

    %% ============================================
    %% FEEDBACK LOOP
    %% ============================================

    subgraph FEEDBACK_LOOP["🔄 Continuous Improvement Loop"]
        direction TB

        USER_FEEDBACK["👍 User Feedback<br/><i>Thumbs up/down<br/>Free-text comments<br/>Rating: 1-5</i>"]
        FEEDBACK_AGGREGATE["📊 Feedback Aggregation<br/><i>Per-model performance<br/>Per-topic accuracy<br/>User satisfaction trends</i>"]
        WEAK_SPOT_DETECT["🔍 Weak Spot Detection<br/><i>Low-performing queries<br/>High hallucination topics<br/>Frequent negative feedback</i>"]
        IMPROVEMENT_ACTIONS["🔧 Improvement Actions<br/><i>Prompt tuning<br/>Fine-tuning data collection<br/>Knowledge base updates<br/>Guardrail refinement</i>"]
        EXPERIMENT_TRACK["🧪 Experiment Tracking<br/><i>MLflow / Weights & Biases<br/>A/B test results<br/>Model comparison</i>"]

        USER_FEEDBACK --> FEEDBACK_AGGREGATE
        FEEDBACK_AGGREGATE --> WEAK_SPOT_DETECT
        WEAK_SPOT_DETECT --> IMPROVEMENT_ACTIONS
        IMPROVEMENT_ACTIONS --> EXPERIMENT_TRACK
    end

    RUBRIC_SCORING --> FEEDBACK_AGGREGATE

    %% ============================================
    %% STYLES
    %% ============================================

    classDef sourceStyle fill:#1565c0,stroke:#42a5f5,stroke-width:2px,color:#e0e0e0
    classDef otelStyle fill:#4a148c,stroke:#ce93d8,stroke-width:2px,color:#e0e0e0
    classDef metricStyle fill:#1b5e20,stroke:#66bb6a,stroke-width:2px,color:#e0e0e0
    classDef logStyle fill:#283593,stroke:#7986cb,stroke-width:2px,color:#e0e0e0
    classDef traceStyle fill:#00695c,stroke:#4db6ac,stroke-width:2px,color:#e0e0e0
    classDef dashStyle fill:#bf360c,stroke:#ff8a65,stroke-width:2px,color:#e0e0e0
    classDef alertStyle fill:#b71c1c,stroke:#ef5350,stroke-width:2px,color:#e0e0e0
    classDef evalStyle fill:#6a1b9a,stroke:#ab47bc,stroke-width:2px,color:#e0e0e0
    classDef feedbackStyle fill:#e65100,stroke:#ff9100,stroke-width:2px,color:#e0e0e0
    classDef serverStyle fill:#004d40,stroke:#26a69a,stroke-width:2px,color:#e0e0e0

    class MICROSERVICES,KAFKA_SRC,LLM_CALLS,RAG_PIPELINE,AGENTS_SRC sourceStyle
    class JAVA_AGENT,PYTHON_SDK,CUSTOM_METRICS otelStyle
    class RECEIVER,PROCESSOR,EXPORTER otelStyle
    class SYS_METRICS,APP_METRICS,AI_METRICS,RAG_METRICS,BIZ_METRICS metricStyle
    class PROMETHEUS_SVR,THANOS metricStyle
    class ACCESS_LOGS,APP_LOGS,AUDIT_LOGS,AI_LOGS,SECURITY_LOGS logStyle
    class LOKI_SVR,LOG_ARCHIVE logStyle
    class E2E_TRACE,RAG_TRACE,AGENT_TRACE,INGESTION_TRACE traceStyle
    class TEMPO_SVR,JAEGER_UI traceStyle
    class DASH_OVERVIEW,DASH_LLM,DASH_RAG,DASH_AGENT,DASH_TENANT,DASH_SECURITY,DASH_INFRA dashStyle
    class GRAFANA_SVR dashStyle
    class ALERT_LLM,ALERT_RAG,ALERT_INFRA,ALERT_SECURITY,ALERT_BUSINESS alertStyle
    class ALERTMANAGER_SVR,PAGERDUTY,SLACK_ALERT,EMAIL_ALERT,WEBHOOK_ALERT alertStyle
    class FAITHFULNESS,ANSWER_RELEVANCE,CONTEXT_PRECISION,CONTEXT_RECALL,CONTEXT_RELEVANCE_M evalStyle
    class G_EVAL,BIAS_METRIC,TOXICITY_METRIC,HALLUCINATION_METRIC,SUMMARIZATION_METRIC evalStyle
    class JUDGE_MODEL,PAIRWISE_COMPARE,REFERENCE_EVAL,RUBRIC_SCORING evalStyle
    class LATENCY_EVAL,COST_EVAL,CITATION_EVAL evalStyle
    class USER_FEEDBACK,FEEDBACK_AGGREGATE,WEAK_SPOT_DETECT,IMPROVEMENT_ACTIONS,EXPERIMENT_TRACK feedbackStyle
```

---

<br/>

<div align="center">

## Volume 10 — CI/CD & MLOps

*Complete CI/CD pipeline with GitHub Actions, ArgoCD, model versioning, and A/B testing*

</div>

```mermaid
---
title: "Volume 10A — CI/CD Pipeline"
---
%%{init: {'theme': 'dark', 'themeVariables': { 'primaryColor': '#1a1a2e', 'primaryTextColor': '#e0e0e0', 'primaryBorderColor': '#66bb6a', 'lineColor': '#66bb6a', 'secondaryColor': '#16213e', 'tertiaryColor': '#0f3460', 'fontFamily': 'Inter, sans-serif'}}}%%

flowchart TB

    %% ============================================
    %% SOURCE CONTROL
    %% ============================================

    DEV["👨‍💻 Developer<br/><i>Code change committed</i>"]

    subgraph SOURCE_CONTROL["🐙 Source Control"]
        direction TB

        GITHUB["🐙 GitHub Repository<br/><i>Monorepo structure<br/>Protected main branch<br/>Required reviews: 2</i>"]
        BRANCH_STRATEGY["🔀 Branching Strategy<br/><i>main → production<br/>develop → staging<br/>feature/* → development<br/>hotfix/* → emergency</i>"]
        PR_REVIEW["🔍 Pull Request<br/><i>Required reviewers<br/>CODEOWNERS file<br/>Auto-assign reviewers</i>"]
        MERGE_CHECKS["✅ Merge Checks<br/><i>All CI checks pass<br/>No merge conflicts<br/>Approved reviews</i>"]

        GITHUB --> BRANCH_STRATEGY
        BRANCH_STRATEGY --> PR_REVIEW
        PR_REVIEW --> MERGE_CHECKS
    end

    DEV --> GITHUB

    %% ============================================
    %% CI PIPELINE
    %% ============================================

    subgraph CI_PIPELINE["⚙️ CI Pipeline (GitHub Actions)"]
        direction TB

        subgraph BUILD_STAGE["🏗️ Build Stage"]
            CHECKOUT["📥 Checkout Code<br/><i>actions/checkout@v4<br/>Fetch depth: 0</i>"]
            CACHE_DEPS["⚡ Cache Dependencies<br/><i>Maven / Gradle cache<br/>npm cache<br/>Docker layer cache</i>"]
            BUILD_JAVA["☕ Build Java Services<br/><i>./gradlew build<br/>JDK 21<br/>GraalVM native (optional)</i>"]
            BUILD_PYTHON["🐍 Build Python Services<br/><i>Poetry install<br/>Python 3.12<br/>Type checking: mypy</i>"]
            BUILD_FRONTEND["⚛️ Build Frontend<br/><i>npm run build<br/>Next.js 14<br/>Static analysis</i>"]

            CHECKOUT --> CACHE_DEPS
            CACHE_DEPS --> BUILD_JAVA
            CACHE_DEPS --> BUILD_PYTHON
            CACHE_DEPS --> BUILD_FRONTEND
        end

        subgraph TEST_STAGE["🧪 Test Stage"]
            UNIT_TESTS["🧪 Unit Tests<br/><i>JUnit 5 / pytest<br/>Coverage > 80%<br/>Mutation testing</i>"]
            INTEGRATION_TESTS["🔗 Integration Tests<br/><i>Testcontainers<br/>PostgreSQL / Redis /<br/>Kafka / Elasticsearch</i>"]
            CONTRACT_TESTS["📜 Contract Tests<br/><i>Pact / Spring Cloud Contract<br/>Consumer-driven contracts<br/>API compatibility</i>"]
            E2E_TESTS["🌐 E2E Tests<br/><i>Playwright / Cypress<br/>Critical user flows<br/>Cross-browser testing</i>"]

            UNIT_TESTS --> INTEGRATION_TESTS
            INTEGRATION_TESTS --> CONTRACT_TESTS
            CONTRACT_TESTS --> E2E_TESTS
        end

        subgraph QUALITY_STAGE["📊 Quality Stage"]
            SONARQUBE["🔍 SonarQube Analysis<br/><i>Code smells<br/>Technical debt<br/>Duplications<br/>Quality gate: Pass</i>"]
            LINT_CHECK["📝 Linting<br/><i>Checkstyle / PMD (Java)<br/>Ruff / Black (Python)<br/>ESLint / Prettier (TS)</i>"]
            DEPENDENCY_CHECK["📦 Dependency Check<br/><i>OWASP Dependency Check<br/>Snyk vulnerability scan<br/>License compliance</i>"]
            API_SPEC_CHECK["📋 API Spec Validation<br/><i>OpenAPI 3.1 lint<br/>Breaking change detection<br/>Schema validation</i>"]

            SONARQUBE --> LINT_CHECK
            LINT_CHECK --> DEPENDENCY_CHECK
            DEPENDENCY_CHECK --> API_SPEC_CHECK
        end

        subgraph SECURITY_STAGE["🔒 Security Stage"]
            SAST["🔍 SAST<br/><i>Semgrep / CodeQL<br/>Static code analysis<br/>Custom rules</i>"]
            SCA["📦 SCA<br/><i>Software Composition Analysis<br/>Known vulnerabilities<br/>CVE database check</i>"]
            SECRETS_SCAN["🔑 Secrets Scanning<br/><i>Gitleaks / TruffleHog<br/>API keys / passwords<br/>Prevent leaks</i>"]
            CONTAINER_SCAN["🐳 Container Scanning<br/><i>Trivy / Grype<br/>Base image vulnerabilities<br/>Dockerfile best practices</i>"]
            DAST["🌐 DAST<br/><i>OWASP ZAP<br/>Runtime vulnerability scan<br/>Against staging</i>"]

            SAST --> SCA
            SCA --> SECRETS_SCAN
            SECRETS_SCAN --> CONTAINER_SCAN
            CONTAINER_SCAN --> DAST
        end

        BUILD_JAVA --> UNIT_TESTS
        BUILD_PYTHON --> UNIT_TESTS
        BUILD_FRONTEND --> UNIT_TESTS

        E2E_TESTS --> SONARQUBE
        API_SPEC_CHECK --> SAST
    end

    MERGE_CHECKS --> CHECKOUT

    %% ============================================
    %% ARTIFACT PUBLISHING
    %% ============================================

    subgraph ARTIFACT_PUB["📦 Artifact Publishing"]
        direction TB

        DOCKER_BUILD["🐳 Docker Build<br/><i>Multi-stage build<br/>Distroless base images<br/>Layer optimization</i>"]
        IMAGE_SIGN["🔏 Image Signing<br/><i>Cosign / Notary<br/>SBOM generation<br/>Provenance attestation</i>"]
        PUSH_ECR["📦 Push to ECR/GCR<br/><i>Tagged: git-sha + semver<br/>Multi-arch: amd64 + arm64</i>"]
        HELM_PACKAGE["📋 Helm Package<br/><i>Chart versioning<br/>Values per environment<br/>Push to Chart Museum</i>"]

        DOCKER_BUILD --> IMAGE_SIGN
        IMAGE_SIGN --> PUSH_ECR
        PUSH_ECR --> HELM_PACKAGE
    end

    DAST --> DOCKER_BUILD

    %% ============================================
    %% CD PIPELINE
    %% ============================================

    subgraph CD_PIPELINE["🚀 CD Pipeline (GitOps)"]
        direction TB

        subgraph ARGOCD_SYSTEM["🔄 ArgoCD"]
            ARGOCD_SVR["🔄 ArgoCD Server<br/><i>GitOps controller<br/>Auto-sync enabled<br/>Self-heal: true</i>"]
            APP_OF_APPS["📦 App-of-Apps Pattern<br/><i>Parent application<br/>manages child apps<br/>per microservice</i>"]
            SYNC_WAVES["🌊 Sync Waves<br/><i>Wave 0: CRDs + Namespaces<br/>Wave 1: Infrastructure<br/>Wave 2: Databases<br/>Wave 3: Services<br/>Wave 4: Ingress</i>"]
        end

        subgraph DEPLOYMENT_STRATEGIES["🎯 Deployment Strategies"]
            CANARY["🐤 Canary Deployment<br/><i>Argo Rollouts<br/>5% → 25% → 50% → 100%<br/>Auto-promote on success</i>"]
            BLUE_GREEN["🔵🟢 Blue-Green<br/><i>Instant switchover<br/>Full rollback capability<br/>Zero-downtime</i>"]
            PROGRESSIVE["📊 Progressive Delivery<br/><i>Flagger integration<br/>Metric-based promotion<br/>Automatic rollback</i>"]
        end

        subgraph ENVIRONMENTS["🌍 Environments"]
            DEV_ENV["🔧 Development<br/><i>Namespace: dev<br/>Auto-deploy on push<br/>Relaxed resources</i>"]
            STAGING_ENV["🧪 Staging<br/><i>Namespace: staging<br/>Production mirror<br/>Full test suite</i>"]
            PROD_ENV["🚀 Production<br/><i>Namespace: production<br/>Canary deployment<br/>Strict resource limits</i>"]
        end

        ARGOCD_SVR --> APP_OF_APPS
        APP_OF_APPS --> SYNC_WAVES
        SYNC_WAVES --> DEV_ENV
        SYNC_WAVES --> STAGING_ENV
        SYNC_WAVES --> PROD_ENV
    end

    HELM_PACKAGE --> ARGOCD_SVR
    CANARY --> PROD_ENV
    BLUE_GREEN --> PROD_ENV
    PROGRESSIVE --> PROD_ENV

    %% ============================================
    %% POST-DEPLOY VALIDATION
    %% ============================================

    subgraph POST_DEPLOY["✅ Post-Deploy Validation"]
        direction TB

        SMOKE_TESTS["💨 Smoke Tests<br/><i>Health check endpoints<br/>Critical path validation<br/>Database connectivity</i>"]
        CANARY_METRICS["📊 Canary Analysis<br/><i>Error rate comparison<br/>Latency comparison<br/>Business metric check</i>"]
        ROLLBACK_CHECK{"🔄 Healthy?"}
        AUTO_ROLLBACK["↩️ Auto Rollback<br/><i>Revert to previous<br/>Alert on-call team<br/>Incident created</i>"]
        PROMOTE["✅ Promote<br/><i>Full traffic shift<br/>Old version scaled down<br/>Success notification</i>"]

        SMOKE_TESTS --> CANARY_METRICS
        CANARY_METRICS --> ROLLBACK_CHECK
        ROLLBACK_CHECK -->|No| AUTO_ROLLBACK
        ROLLBACK_CHECK -->|Yes| PROMOTE
    end

    PROD_ENV --> SMOKE_TESTS

    %% ============================================
    %% STYLES
    %% ============================================

    classDef devStyle fill:#1565c0,stroke:#42a5f5,stroke-width:2px,color:#e0e0e0
    classDef scmStyle fill:#4a148c,stroke:#ce93d8,stroke-width:2px,color:#e0e0e0
    classDef buildStyle fill:#1b5e20,stroke:#66bb6a,stroke-width:2px,color:#e0e0e0
    classDef testStyle fill:#283593,stroke:#7986cb,stroke-width:2px,color:#e0e0e0
    classDef qualityStyle fill:#e65100,stroke:#ff9100,stroke-width:2px,color:#e0e0e0
    classDef secStyle fill:#b71c1c,stroke:#ef5350,stroke-width:2px,color:#e0e0e0
    classDef artifactStyle fill:#00695c,stroke:#4db6ac,stroke-width:2px,color:#e0e0e0
    classDef cdStyle fill:#6a1b9a,stroke:#ab47bc,stroke-width:2px,color:#e0e0e0
    classDef envStyle fill:#004d40,stroke:#26a69a,stroke-width:2px,color:#e0e0e0
    classDef postStyle fill:#bf360c,stroke:#ff8a65,stroke-width:2px,color:#e0e0e0

    class DEV devStyle
    class GITHUB,BRANCH_STRATEGY,PR_REVIEW,MERGE_CHECKS scmStyle
    class CHECKOUT,CACHE_DEPS,BUILD_JAVA,BUILD_PYTHON,BUILD_FRONTEND buildStyle
    class UNIT_TESTS,INTEGRATION_TESTS,CONTRACT_TESTS,E2E_TESTS testStyle
    class SONARQUBE,LINT_CHECK,DEPENDENCY_CHECK,API_SPEC_CHECK qualityStyle
    class SAST,SCA,SECRETS_SCAN,CONTAINER_SCAN,DAST secStyle
    class DOCKER_BUILD,IMAGE_SIGN,PUSH_ECR,HELM_PACKAGE artifactStyle
    class ARGOCD_SVR,APP_OF_APPS,SYNC_WAVES cdStyle
    class CANARY,BLUE_GREEN,PROGRESSIVE cdStyle
    class DEV_ENV,STAGING_ENV,PROD_ENV envStyle
    class SMOKE_TESTS,CANARY_METRICS,ROLLBACK_CHECK,AUTO_ROLLBACK,PROMOTE postStyle
```

<br/>

```mermaid
---
title: "Volume 10B — MLOps Pipeline"
---
%%{init: {'theme': 'dark', 'themeVariables': { 'primaryColor': '#1a1a2e', 'primaryTextColor': '#e0e0e0', 'primaryBorderColor': '#ff7043', 'lineColor': '#ff7043', 'secondaryColor': '#16213e', 'tertiaryColor': '#0f3460', 'fontFamily': 'Inter, sans-serif'}}}%%

flowchart TB

    %% ============================================
    %% MODEL LIFECYCLE
    %% ============================================

    subgraph MODEL_LIFECYCLE["🧠 Model Lifecycle Management"]
        direction TB

        subgraph MODEL_REGISTRY["📦 Model Registry"]
            MLFLOW["📊 MLflow Model Registry<br/><i>Model versioning<br/>Stage: Staging → Production<br/>Metadata tracking</i>"]
            MODEL_CARD["📋 Model Cards<br/><i>Model documentation<br/>Performance metrics<br/>Intended use / Limitations</i>"]
            MODEL_LINEAGE["🔗 Model Lineage<br/><i>Training data → Model<br/>→ Evaluation → Deployment<br/>Full provenance</i>"]
        end

        subgraph EMBEDDING_VERSIONING["🧬 Embedding Model Management"]
            EMBED_VERSIONS["📊 Embedding Versions<br/><i>v1: text-embedding-ada-002<br/>v2: text-embedding-3-small<br/>v3: text-embedding-3-large<br/>v4: BGE-M3</i>"]
            EMBED_MIGRATION["🔄 Migration Strategy<br/><i>Dual-write during migration<br/>Shadow scoring<br/>Gradual cutover</i>"]
            EMBED_BENCHMARK["📈 Benchmark Suite<br/><i>MTEB evaluation<br/>Domain-specific eval<br/>Latency comparison</i>"]
            REINDEX_PIPELINE["🔄 Re-indexing Pipeline<br/><i>Batch re-embedding<br/>Vector DB swap<br/>Zero-downtime migration</i>"]

            EMBED_VERSIONS --> EMBED_MIGRATION
            EMBED_MIGRATION --> EMBED_BENCHMARK
            EMBED_BENCHMARK --> REINDEX_PIPELINE
        end

        subgraph PROMPT_VERSIONING["📝 Prompt Version Management"]
            PROMPT_REPO["📁 Prompt Repository<br/><i>Git-backed prompt store<br/>Version control<br/>Branch per experiment</i>"]
            PROMPT_TEMPLATE["📋 Template Engine<br/><i>Jinja2 templates<br/>Variable injection<br/>Conditional sections</i>"]
            PROMPT_EVAL["📊 Prompt Evaluation<br/><i>Automated scoring<br/>Regression detection<br/>A/B comparison</i>"]
            PROMPT_DEPLOY["🚀 Prompt Deployment<br/><i>Feature flag controlled<br/>Gradual rollout<br/>Instant rollback</i>"]

            PROMPT_REPO --> PROMPT_TEMPLATE
            PROMPT_TEMPLATE --> PROMPT_EVAL
            PROMPT_EVAL --> PROMPT_DEPLOY
        end
    end

    %% ============================================
    %% FINE-TUNING PIPELINE
    %% ============================================

    subgraph FINETUNE_PIPELINE["🔧 Fine-Tuning Pipeline"]
        direction TB

        subgraph DATA_PIPELINE["📊 Training Data Pipeline"]
            DATA_COLLECT["📥 Data Collection<br/><i>User feedback signals<br/>Human annotations<br/>Synthetic data generation</i>"]
            DATA_CLEAN["🧹 Data Cleaning<br/><i>Deduplication<br/>Quality filtering<br/>PII removal</i>"]
            DATA_LABEL["🏷️ Data Labeling<br/><i>Human-in-the-loop<br/>Active learning<br/>Label Studio / Prodigy</i>"]
            DATA_VALIDATE["✅ Data Validation<br/><i>Schema validation<br/>Distribution checks<br/>Bias detection</i>"]
            DATA_VERSION["📊 Data Versioning<br/><i>DVC / LakeFS<br/>Snapshot management<br/>Lineage tracking</i>"]

            DATA_COLLECT --> DATA_CLEAN
            DATA_CLEAN --> DATA_LABEL
            DATA_LABEL --> DATA_VALIDATE
            DATA_VALIDATE --> DATA_VERSION
        end

        subgraph TRAINING["🏋️ Training Pipeline"]
            TRAIN_CONFIG["⚙️ Training Configuration<br/><i>Hyperparameters<br/>LoRA / QLoRA settings<br/>Learning rate schedule</i>"]
            TRAIN_EXECUTE["🔥 Training Execution<br/><i>GPU cluster: A100 / H100<br/>Distributed training<br/>Mixed precision (bf16)</i>"]
            TRAIN_MONITOR["📊 Training Monitoring<br/><i>Loss curves<br/>Gradient norms<br/>Learning rate tracking<br/>W&B / TensorBoard</i>"]
            CHECKPOINT_MGR["💾 Checkpoint Manager<br/><i>Periodic checkpointing<br/>Best model selection<br/>Storage optimization</i>"]

            TRAIN_CONFIG --> TRAIN_EXECUTE
            TRAIN_EXECUTE --> TRAIN_MONITOR
            TRAIN_MONITOR --> CHECKPOINT_MGR
        end

        subgraph EVAL_STAGE["📊 Model Evaluation"]
            AUTO_EVAL["🤖 Automated Evaluation<br/><i>RAGAS metrics<br/>DeepEval suite<br/>Custom benchmarks</i>"]
            HUMAN_EVAL["👨‍💼 Human Evaluation<br/><i>Blind comparison<br/>Expert review<br/>User study</i>"]
            REGRESSION_TEST["🔍 Regression Testing<br/><i>Golden test set<br/>Performance comparison<br/>No-regress validation</i>"]
            APPROVAL_GATE["✅ Approval Gate<br/><i>Metrics threshold<br/>Human sign-off<br/>Compliance check</i>"]

            AUTO_EVAL --> HUMAN_EVAL
            HUMAN_EVAL --> REGRESSION_TEST
            REGRESSION_TEST --> APPROVAL_GATE
        end

        DATA_VERSION --> TRAIN_CONFIG
        CHECKPOINT_MGR --> AUTO_EVAL
    end

    %% ============================================
    %% FEATURE STORE
    %% ============================================

    subgraph FEATURE_STORE["📦 Feature Store"]
        direction TB

        FEAST["📊 Feast<br/><i>Feature serving<br/>Online + Offline store<br/>Point-in-time joins</i>"]
        ONLINE_FEATURES["⚡ Online Features<br/><i>User preferences<br/>Recent interactions<br/>Real-time context</i>"]
        OFFLINE_FEATURES["📦 Offline Features<br/><i>User embeddings<br/>Historical patterns<br/>Aggregated statistics</i>"]
        FEATURE_PIPELINE["🔄 Feature Pipeline<br/><i>Spark / Flink<br/>Batch + Stream processing<br/>Feature freshness SLAs</i>"]

        FEAST --> ONLINE_FEATURES
        FEAST --> OFFLINE_FEATURES
        FEAST --> FEATURE_PIPELINE
    end

    %% ============================================
    %% A/B TESTING & EXPERIMENTATION
    %% ============================================

    subgraph AB_TESTING["🧪 A/B Testing & Experimentation"]
        direction TB

        subgraph EXPERIMENT_DESIGN["📋 Experiment Design"]
            HYPOTHESIS["📝 Hypothesis Definition<br/><i>Clear success criteria<br/>Primary + Secondary metrics<br/>Power analysis</i>"]
            TRAFFIC_SPLIT["🔀 Traffic Splitting<br/><i>Hash-based assignment<br/>Consistent bucketing<br/>Per-tenant experiments</i>"]
            EXPERIMENT_CONFIG["⚙️ Experiment Config<br/><i>Model A vs Model B<br/>Prompt v1 vs v2<br/>RAG config variants</i>"]
        end

        subgraph EXPERIMENT_RUN["🏃 Experiment Execution"]
            SHADOW_MODE["👻 Shadow Mode<br/><i>Run new model in parallel<br/>No impact on production<br/>Compare outputs offline</i>"]
            INTERLEAVING["🔀 Interleaving<br/><i>Mix results from A and B<br/>User preference signals<br/>Implicit feedback</i>"]
            MULTI_ARMED["🎰 Multi-Armed Bandit<br/><i>Thompson sampling<br/>Exploration vs Exploitation<br/>Auto-optimize allocation</i>"]
        end

        subgraph EXPERIMENT_ANALYSIS["📊 Experiment Analysis"]
            STAT_SIGNIFICANCE["📈 Statistical Significance<br/><i>p-value < 0.05<br/>Confidence intervals<br/>Bonferroni correction</i>"]
            EFFECT_SIZE["📊 Effect Size<br/><i>Cohen's d calculation<br/>Practical significance<br/>Minimum detectable effect</i>"]
            SEGMENT_ANALYSIS["🔍 Segment Analysis<br/><i>By tenant / user type<br/>By query complexity<br/>By domain area</i>"]
            EXPERIMENT_DECISION{"🔀 Decision"}
            ROLLOUT["✅ Roll Out Winner<br/><i>Gradual traffic increase<br/>Monitor for regressions<br/>Update baseline</i>"]
            ROLLBACK_EXP["↩️ Rollback<br/><i>Revert to baseline<br/>Document learnings<br/>Plan next iteration</i>"]

            STAT_SIGNIFICANCE --> EFFECT_SIZE
            EFFECT_SIZE --> SEGMENT_ANALYSIS
            SEGMENT_ANALYSIS --> EXPERIMENT_DECISION
            EXPERIMENT_DECISION -->|Winner| ROLLOUT
            EXPERIMENT_DECISION -->|No Winner| ROLLBACK_EXP
        end

        HYPOTHESIS --> TRAFFIC_SPLIT
        TRAFFIC_SPLIT --> EXPERIMENT_CONFIG
        EXPERIMENT_CONFIG --> SHADOW_MODE
        EXPERIMENT_CONFIG --> INTERLEAVING
        EXPERIMENT_CONFIG --> MULTI_ARMED
        SHADOW_MODE --> STAT_SIGNIFICANCE
        INTERLEAVING --> STAT_SIGNIFICANCE
        MULTI_ARMED --> STAT_SIGNIFICANCE
    end

    APPROVAL_GATE --> SHADOW_MODE

    %% ============================================
    %% INFRASTRUCTURE AS CODE
    %% ============================================

    subgraph IAC["🏗️ Infrastructure as Code"]
        direction TB

        TERRAFORM["🔧 Terraform<br/><i>Cloud infrastructure<br/>State management<br/>Module reuse</i>"]
        PULUMI["📦 Pulumi<br/><i>Programming language IaC<br/>Python / Go / TypeScript<br/>Type-safe configs</i>"]
        CROSSPLANE["☸️ Crossplane<br/><i>Kubernetes-native IaC<br/>Cloud resource management<br/>XRDs / Compositions</i>"]
        ATLANTIS["🌊 Atlantis<br/><i>Terraform PR automation<br/>Plan in PR comments<br/>Auto-apply on merge</i>"]

        TERRAFORM --> ATLANTIS
    end

    %% ============================================
    %% DISASTER RECOVERY
    %% ============================================

    subgraph DR["🛡️ Disaster Recovery"]
        direction TB

        BACKUP_STRATEGY["💾 Backup Strategy<br/><i>PostgreSQL: WAL streaming<br/>Vector DB: Snapshot + S3<br/>Redis: RDB + AOF<br/>Elasticsearch: Snapshots</i>"]
        MULTI_REGION["🌍 Multi-Region Setup<br/><i>Active-Passive<br/>Cross-region replication<br/>DNS failover</i>"]
        RTO_RPO["⏱️ RTO / RPO Targets<br/><i>RTO: 15 minutes<br/>RPO: 1 minute<br/>Automated failover</i>"]
        DR_TESTING["🧪 DR Testing<br/><i>Quarterly DR drills<br/>Chaos engineering<br/>Automated runbooks</i>"]

        BACKUP_STRATEGY --> MULTI_REGION
        MULTI_REGION --> RTO_RPO
        RTO_RPO --> DR_TESTING
    end

    %% ============================================
    %% STYLES
    %% ============================================

    classDef registryStyle fill:#4a148c,stroke:#ce93d8,stroke-width:2px,color:#e0e0e0
    classDef embedStyle fill:#1565c0,stroke:#42a5f5,stroke-width:2px,color:#e0e0e0
    classDef promptStyle fill:#283593,stroke:#7986cb,stroke-width:2px,color:#e0e0e0
    classDef dataStyle fill:#1b5e20,stroke:#66bb6a,stroke-width:2px,color:#e0e0e0
    classDef trainStyle fill:#b71c1c,stroke:#ef5350,stroke-width:2px,color:#e0e0e0
    classDef evalMLStyle fill:#e65100,stroke:#ff9100,stroke-width:2px,color:#e0e0e0
    classDef featureStyle fill:#00695c,stroke:#4db6ac,stroke-width:2px,color:#e0e0e0
    classDef abStyle fill:#6a1b9a,stroke:#ab47bc,stroke-width:2px,color:#e0e0e0
    classDef iacStyle fill:#bf360c,stroke:#ff8a65,stroke-width:2px,color:#e0e0e0
    classDef drStyle fill:#004d40,stroke:#26a69a,stroke-width:2px,color:#e0e0e0

    class MLFLOW,MODEL_CARD,MODEL_LINEAGE registryStyle
    class EMBED_VERSIONS,EMBED_MIGRATION,EMBED_BENCHMARK,REINDEX_PIPELINE embedStyle
    class PROMPT_REPO,PROMPT_TEMPLATE,PROMPT_EVAL,PROMPT_DEPLOY promptStyle
    class DATA_COLLECT,DATA_CLEAN,DATA_LABEL,DATA_VALIDATE,DATA_VERSION dataStyle
    class TRAIN_CONFIG,TRAIN_EXECUTE,TRAIN_MONITOR,CHECKPOINT_MGR trainStyle
    class AUTO_EVAL,HUMAN_EVAL,REGRESSION_TEST,APPROVAL_GATE evalMLStyle
    class FEAST,ONLINE_FEATURES,OFFLINE_FEATURES,FEATURE_PIPELINE featureStyle
    class HYPOTHESIS,TRAFFIC_SPLIT,EXPERIMENT_CONFIG abStyle
    class SHADOW_MODE,INTERLEAVING,MULTI_ARMED abStyle
    class STAT_SIGNIFICANCE,EFFECT_SIZE,SEGMENT_ANALYSIS,EXPERIMENT_DECISION,ROLLOUT,ROLLBACK_EXP abStyle
    class TERRAFORM,PULUMI,CROSSPLANE,ATLANTIS iacStyle
    class BACKUP_STRATEGY,MULTI_REGION,RTO_RPO,DR_TESTING drStyle
```

---

<br/>

<div align="center">

## 📊 Architecture Summary

</div>

| Metric | Count |
|--------|-------|
| **Total Diagrams** | 12 (across 10 volumes) |
| **Total Components** | 350+ |
| **Microservices** | 25+ |
| **Kafka Topics** | 20+ |
| **Database Systems** | 6 (PostgreSQL, Redis, Qdrant, Elasticsearch, Neo4j, S3) |
| **AI/ML Models** | 15+ (LLMs, Embedding, Reranker, Classifier) |
| **Security Layers** | 8+ (OAuth, JWT, RBAC, ABAC, OPA, RLS, Vault, Guardrails) |
| **Monitoring Tools** | 10+ (Prometheus, Grafana, Loki, Tempo, Jaeger, OpenTelemetry) |
| **Evaluation Frameworks** | 3 (RAGAS, DeepEval, LLM-as-Judge) |
| **Deployment Strategies** | 3 (Canary, Blue-Green, Progressive) |

---

<div align="center">

## 🏗️ Technology Stack

</div>

| Layer | Technologies |
|-------|-------------|
| **Frontend** | React, Next.js 14, React Native |
| **API Gateway** | Kong, Spring Cloud Gateway |
| **Backend** | Spring Boot 3.x, Java 21, Python 3.12 |
| **Service Mesh** | Istio, Envoy |
| **Message Broker** | Apache Kafka, Schema Registry |
| **Databases** | PostgreSQL 16, Redis 7, Qdrant, Elasticsearch 8, Neo4j |
| **Object Storage** | AWS S3, MinIO |
| **AI/LLM** | GPT-4o, Claude 3.5, Gemini 1.5, Llama 3.1, Mistral |
| **Embeddings** | text-embedding-3-large, BGE-M3, E5, ColBERTv2 |
| **Agentic Framework** | LangGraph, LangChain |
| **Auth** | Keycloak, OAuth2/OIDC, OPA |
| **Secrets** | HashiCorp Vault |
| **Container Orchestration** | Kubernetes (EKS/GKE/AKS), Helm |
| **CI/CD** | GitHub Actions, ArgoCD, Argo Rollouts |
| **Observability** | Prometheus, Grafana, Loki, Tempo, Jaeger, OpenTelemetry |
| **Evaluation** | RAGAS, DeepEval, TruLens, MLflow |
| **IaC** | Terraform, Crossplane |
| **Security Scanning** | SonarQube, Semgrep, Trivy, Snyk |

---

<div align="center">

### 🔗 Cross-Volume References

</div>

```mermaid
%%{init: {'theme': 'dark', 'themeVariables': { 'primaryColor': '#1a1a2e', 'primaryTextColor': '#e0e0e0', 'primaryBorderColor': '#4fc3f7', 'lineColor': '#4fc3f7'}}}%%

flowchart LR
    V1["📋 Vol 1<br/>Executive"] --> V2["☸️ Vol 2<br/>Infrastructure"]
    V1 --> V3["🌱 Vol 3<br/>Microservices"]
    V3 --> V4["📨 Vol 4<br/>Kafka Events"]
    V3 --> V5["📚 Vol 5<br/>Hybrid RAG"]
    V3 --> V6["🤖 Vol 6<br/>Agentic AI"]
    V5 --> V7["🧩 Vol 7<br/>Memory"]
    V6 --> V7
    V1 --> V8["🔐 Vol 8<br/>Security"]
    V2 --> V9["📊 Vol 9<br/>Monitoring"]
    V2 --> V10["🔄 Vol 10<br/>CI/CD & MLOps"]
    V9 --> V10

    classDef volStyle fill:#1b1b2f,stroke:#4fc3f7,stroke-width:2px,color:#e0e0e0
    class V1,V2,V3,V4,V5,V6,V7,V8,V9,V10 volStyle
```

---

<div align="center">

**Built with ❤️ by an Enterprise Architecture Team**

*This document follows C4-inspired notation for clarity and maintainability at scale.*

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg?style=flat-square)](https://opensource.org/licenses/MIT)

</div>
]]>
