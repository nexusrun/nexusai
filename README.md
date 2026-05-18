# NEXUS AI

**Full-stack application platform. Deploy full-stack apps from a prompt, a repo, or a CLI. Your AI agent runs the rest.**

[![Website](https://img.shields.io/badge/Website-nexusai.run-0ea5e9?style=flat-square)](https://nexusai.run)
[![Pricing](https://img.shields.io/badge/Pricing-from%20%2429%2Fmo-38bdf8?style=flat-square)](https://nexusai.run/pricing)
[![Docs](https://img.shields.io/badge/Docs-nexusai.run%2Fdocs-64748b?style=flat-square)](https://nexusai.run/docs)
[![HIPAA](https://img.shields.io/badge/HIPAA-Aligned-10b981?style=flat-square)](https://nexusai.run/hipaa-compliance)
[![MCP Registry](https://img.shields.io/badge/MCP%20Registry-io.github.nexusrun%2Fnexus--ai-7c3aed?style=flat-square)](https://registry.modelcontextprotocol.io/v0.1/servers?search=io.github.nexusrun/nexus-ai)
[![LinkedIn](https://img.shields.io/badge/LinkedIn-nexusai--run-0077b5?style=flat-square&logo=linkedin)](https://linkedin.com/company/nexusai-run)

---

## What is NEXUS AI?

NEXUS AI is an **MCP-native application platform** that deploys full-stack containerized applications (app code, Postgres, MySQL, Mongo, Redis, S3-compatible buckets, persistent volumes, background workers, encrypted backups) in about 5 minutes. Every platform action is callable as a Model Context Protocol (MCP) tool, so Claude, Cursor, Codex, or any MCP-compatible agent can deploy, scale, back up, restore, query the database, and roll back without leaving the chat or IDE.

**The problem it solves.** AI tools like Claude Code, Cursor, v0, Bolt, Lovable, and Replit can generate working application code in minutes. Getting that code into production still requires the rest of a real stack: a database, a queue, storage, secrets, scaling, health checks, backups, rollbacks. NEXUS AI is the deploy layer that closes that gap and exposes every operation to the agent that wrote the code.

**In one sentence.** Describe what you want to build, ship to a public HTTPS URL with Postgres + Redis + S3 in 5 minutes, then let your AI agent operate the stack on your behalf.

---

## How It Works

Three equivalent ways to deploy the same app. Pick one or use all three.

```
PROMPT
  Tell Claude in chat: "Deploy this repo with Postgres, Redis,
  and a bucket called user-uploads."
  → The agent calls nexusai_deploy_source + nexusai_bucket_create
    + nexusai_bucket_attach + nexusai_deploy_redeploy.
  → Live URL in ~5 minutes.

REPO
  nexus deploy source \
    --repo https://github.com/you/my-app.git \
    --framework python \
    --services postgresql,redis \
    --bucket user-uploads --wait

DASHBOARD
  Click through the same operations at https://nexusai.run/app.
  Same engine, same result.
```

After deploy, the agent (or you) operates the running stack: stream logs, scale replicas, snapshot the database, restore from backup, run a sandboxed SQL query, apply an AI-proposed schema fix, roll back to a previous release. Every action is an MCP tool, a CLI command, and a dashboard button.

---

## Core Features

### Full-stack deploys in one command
Postgres, MySQL, Mongo, Redis, S3-compatible buckets, persistent volumes, background workers, and your app code. Wired together by one `nexus deploy` and live at a public HTTPS URL in 5 minutes. Framework detection covers FastAPI, Flask, Django, Express, Next.js, Rails, Laravel, Symfony, PHP, Ruby, Go, Java, and any container.

### Operated by your AI agent
59 MCP tools cover the full lifecycle. Connect the NEXUS AI MCP server (`https://api.zollo.live/mcp`) to Claude Desktop, Claude Code, Cursor, Codex, or any MCP client. The same agent that generated the code can deploy, scale, back up, restore, query the database, and roll back. Listed on the official MCP Registry at `io.github.nexusrun/nexus-ai`.

### Persistent storage with real IAM
Org-scoped volumes that survive container restarts, redeploys, and host reboots. Multi-attach S3-compatible buckets backed by MinIO, each with its own scoped IAM service account (not platform-wide root credentials). Per-bucket credential rotation, signed download URLs (30 seconds to 1 hour TTL), streaming uploads.

### Database intelligence layer
Connect external Postgres, MySQL, or Mongo databases. Inspect schemas (cached for 5 minutes). Preview queries with `EXPLAIN` + safety analysis. Execute sandboxed SELECT statements with statement timeouts and row caps. Apply AI-proposed DDL fixes generated from runtime error logs (with review and audit).

### Encrypted backups, signed downloads
Scheduled or on-demand backups for Postgres (`pg_dump`), MySQL (`mysqldump`), Mongo (`mongodump`), and Redis (`BGSAVE`). Encrypted at rest. Download via short-lived signed URLs (TTL 30s to 1h) or restore directly. Cross-deployment restore (seed staging from production) supported.

### Production-safe lifecycle
Soft stop preserves containers, networks, volumes, and the port reservation so the next start brings everything back. Boot reconciliation restarts deployments the host reboot did not bring back. Versioned rollback in seconds. Replica count preserved across restart.

### Three deploy paths, one engine
Dashboard, CLI (`nexus deploy`), or MCP tool call from your agent. Same engine, same result. Switch between them in the same project without anything getting out of sync.

### Multi-cloud single-container deploys
Full-stack deploys run on the NEXUS AI managed Container platform with org-level isolation. Single-container apps can also target AWS App Runner, Google Cloud Run, or Azure Container Apps from the same dashboard, CLI, or MCP call.

### Real-time observability
Streaming build and runtime logs over WebSocket. Health checks with configurable endpoints. Tail logs directly from your agent (`nexusai_deploy_logs`) to triage failures without leaving chat.

### Encrypted secrets vault
AES-256-GCM encryption. Injected at container start, never written to images, never returned over the API, never appear in logs. Scoped per organization and environment with full audit trail on every read, write, and deletion.

### Role-based access control and tenant isolation
Org-level roles (Owner, Admin, Developer). Per-org isolated runtime, networks, volumes, and S3 buckets. SAML / OIDC SSO available on Enterprise. Independently scoped and revocable API tokens with 23 fine-grained OAuth scopes (`deployments:read`, `db:admin`, `volumes:manage`, `buckets:manage`, etc.) plus four legacy broad scopes preserved for backward compatibility.

### HIPAA-aligned infrastructure
Tenant isolation, encrypted secrets, encrypted backups, scoped per-bucket IAM, full audit logs, customer-owned cloud deployments for Enterprise, BAA available for Healthcare Pro and Enterprise.

---

## Supported deploy targets

| Provider | Type | Plans |
|---|---|---|
| **NEXUS AI managed Container platform** | Full-stack (app + DB + storage + workers) | All plans |
| **AWS App Runner** | Single-container | Pro, Healthcare Pro, Enterprise |
| **Google Cloud Run** | Single-container | Starter+, all plans |
| **Azure Container Apps** | Single-container | Pro, Healthcare Pro, Enterprise |
| **Self-hosted / on-prem** | Customer-owned Docker hosts | Enterprise |

Full-stack deploys (app + databases + storage + workers + backups) run on the NEXUS AI managed Container platform. The cloud-provider targets are for single-container apps that do not need the full managed stack.

---

## Where NEXUS AI is listed

| Registry | URL |
|---|---|
| **Official MCP Registry** | [`io.github.nexusrun/nexus-ai`](https://registry.modelcontextprotocol.io/v0.1/servers?search=io.github.nexusrun/nexus-ai) |
| **mcp.so** | [mcp.so/server/nexusrun](https://mcp.so/server/nexusrun) |
| **Smithery** | [smithery.ai/server/saif-elyzal/NEXUSRUN](https://smithery.ai/server/saif-elyzal/NEXUSRUN) |

Install in any MCP client by searching "NEXUS AI" in the client's MCP marketplace, or via the registry URL above.

---

## Pricing

| Plan | Price | Best For |
|---|---|---|
| **Starter** | $29/month | Individual developers, early experiments |
| **Pro** | $149/month | Startups, SaaS teams, multi-cloud workloads |
| **Healthcare Starter** | $149/month | Regulated healthcare, HIPAA-aligned |
| **Healthcare Pro** | $299/month | Full audit logs, RBAC, compliance controls |
| **Enterprise** | Custom | On-prem, private runtime, SSO, dedicated SLA |

### Starter at $29/month
- Application Generation Engine
- NEXUS AI managed Container platform (shared runtime)
- 2 concurrent deployments
- Public HTTPS endpoint
- Google Cloud Run single-container deployment target
- Community support

### Pro at $149/month
- Everything in Starter
- Multi-cloud single-container deploys (AWS App Runner, Google Cloud Run, Azure Container Apps)
- 5 active deployments, up to 10 concurrent containers
- Versioned deployments + one-click rollback
- Real-time build and runtime observability
- Encrypted secrets vault
- Storage volumes + buckets
- Database backups
- Team access with RBAC
- Email support

### Enterprise (custom)
- Everything in Pro
- Deploy into customer-owned AWS, Google Cloud, or Azure accounts
- Private build and runtime isolation
- Unlimited deployments and versions
- Advanced audit logs (HIPAA / SOC-ready)
- SSO (SAML / OIDC)
- IP allowlisting and network controls
- Air-gapped and on-premises deployment support
- Dedicated support and SLA

[View full pricing](https://nexusai.run/pricing) · [Healthcare pricing](https://nexusai.run/pricing/healthcare)

---

## NEXUS AI vs alternatives

| Capability | NEXUS AI | Vercel | Render | Railway | Fly.io |
|---|:---:|:---:|:---:|:---:|:---:|
| Full-stack in one command (DB + Redis + storage + workers + code) | ✅ | partial | ✅ | ✅ | ✅ |
| Native MCP tools for AI agents (50+) | ✅ | — | — | — | — |
| AI-powered DB schema fixes from runtime logs | ✅ | — | — | — | — |
| Per-bucket IAM out of the box | ✅ | — | — | — | partial |
| Encrypted DB backups with signed download URLs | ✅ | — | ✅ | ✅ | partial |
| Single CLI command for full stack | ✅ | — | partial | partial | ✅ |
| Built for agent-driven workflows | ✅ | — | — | — | — |
| Multi-cloud single-container target | ✅ | — | — | — | — |
| Customer-owned cloud accounts (BYOC) | ✅ (Enterprise) | — | — | — | — |
| Production rollback | ✅ (one-click) | — | partial | partial | partial |
| AES-256-GCM secrets vault | ✅ | basic | basic | basic | basic |
| Real-time WebSocket logs | ✅ | basic | basic | basic | basic |
| HIPAA-aligned | ✅ | — | — | — | — |

---

## Who Uses NEXUS AI

### AI app builders
Ship apps generated by Claude Code, Cursor, v0, Bolt, Lovable, or Replit with a real database, real storage, and a real public URL in 5 minutes. Let the same agent that wrote the code operate the deploy.

### Teams building agent products
Expose your platform actions as MCP tools so end-user agents can deploy, operate, and scale on your customers' behalf.

### SaaS founders
Launch new ideas without spending a week on infrastructure. Stand up new apps with Postgres, Redis, and storage from one command.

### Platform and DevOps teams
Give every internal team a self-service deploy path with audit logs, RBAC, and rollback baked in. No tickets, no glue scripts.

### Regulated industries (Healthcare and Fintech)
Deploy into customer-owned cloud infrastructure with HIPAA-aligned controls, full audit trails, tenant isolation, and BAA support.

---

## Quick Start

### 1. Install the CLI

```bash
# macOS
curl -fsSL https://nexusai.run/install-mac.sh | bash

# Linux
curl -fsSL https://nexusai.run/install.sh | bash
```

Authenticate:

```bash
nexus auth login
nexus auth status
```

### 2. Deploy a full-stack app from a Git repo

```bash
nexus deploy source \
  --repo https://github.com/you/my-app.git \
  --name my-app \
  --provider docker \
  --framework python \
  --services postgresql,redis \
  --start-command "uvicorn app:app --host 0.0.0.0 --port 8000" \
  --wait
```

NEXUS AI builds the container, provisions Postgres + Redis with persistent volumes, opens a public HTTPS URL through Traefik, and starts streaming logs.

### 3. Attach a bucket for uploads

```bash
nexus bucket create user-uploads
nexus bucket attach <bucket-id> <deployment-id>
nexus deploy redeploy <deployment-id> --wait
```

Your app receives `S3_ENDPOINT`, `S3_BUCKET`, `S3_ACCESS_KEY`, `S3_SECRET_KEY` as environment variables. Use any S3 SDK against the scoped per-bucket service account.

### 4. Operate from your agent

Connect the NEXUS AI MCP server to Claude Desktop, Claude Code, Cursor, or Codex (`https://api.zollo.live/mcp`). The agent can then run commands like:

> "Take a Postgres backup of my-app, run the migration, and roll back if anything fails."

The agent calls `nexusai_db_services_list`, `nexusai_db_backup`, then conditionally `nexusai_db_restore` and `nexusai_deploy_rollback`, all without you opening a terminal.

[Full documentation](https://nexusai.run/docs) · [MCP Server Reference](https://nexusai.run/docs#mcp-overview)

---

## API and MCP Integration

NEXUS AI exposes a REST API and a full MCP server with **59 tools across 9 categories**:

| Category | Tools | Example |
|---|---:|---|
| Identity and discovery | 4 | `nexusai_whoami`, `nexusai_projects_list` |
| Deployments | 14 | `nexusai_deploy_create`, `nexusai_deploy_source`, `nexusai_deploy_scale`, `nexusai_deploy_rollback` |
| Secrets | 4 | `nexusai_secrets_create`, `nexusai_secrets_list` |
| Custom domains | 4 | `nexusai_domains_add`, `nexusai_domains_verify` |
| External database sources / DB intelligence | 8 | `nexusai_db_inspect_schema`, `nexusai_db_query_execute`, `nexusai_db_propose_fix` |
| Database backups | 7 | `nexusai_db_backup`, `nexusai_db_restore`, `nexusai_db_backup_download` |
| Persistent storage volumes | 5 | `nexusai_volume_create`, `nexusai_volume_attach` |
| S3-compatible buckets | 9 | `nexusai_bucket_create`, `nexusai_bucket_attach`, `nexusai_bucket_rotate_credentials`, `nexusai_bucket_file_download` |
| Support tickets | 4 | `nexusai_support_ticket_create`, `nexusai_support_ticket_reply` |

**OAuth scopes.** 23 scopes total: 4 legacy broad scopes (`deployments:{read,logs,create,delete}`) kept for backward compatibility, plus 18 fine-grained scopes (`secrets:{read,manage,delete}`, `domains:{read,manage,delete}`, `db:{read,query,admin,source:delete}`, `volumes:{read,manage,delete}`, `buckets:{read,manage,delete}`, `support:{read,write}`). Old tokens continue to satisfy fine-grained checks via `SCOPE_SUPERSETS`.

### Connect from Claude Desktop

Add to `~/Library/Application Support/Claude/claude_desktop_config.json` (macOS) or `%APPDATA%\Claude\claude_desktop_config.json` (Windows):

```json
{
  "mcpServers": {
    "nexus-ai": {
      "url": "https://api.zollo.live/mcp",
      "headers": { "Authorization": "Bearer <your-nexus-token>" }
    }
  }
}
```

### Connect from Claude Code

```bash
claude mcp add nexus-ai \
  --url https://api.zollo.live/mcp \
  --header "Authorization: Bearer <your-nexus-token>"
```

### Connect from Cursor

Cursor Settings, MCP, Add server with the same URL and Bearer token.

Generate tokens at [nexusai.run/app/tokens](https://nexusai.run/app/tokens). Full MCP reference at [nexusai.run/docs#mcp-overview](https://nexusai.run/docs#mcp-overview).

[API Documentation](https://nexusai.run/docs)

---

## Tech Stack

| Layer | Technology |
|---|---|
| Frontend | React 18, TypeScript, Vite 7, Tailwind CSS |
| Backend | Node.js, Express, TypeScript |
| ORM | Prisma |
| Database | PostgreSQL |
| Cache | Redis |
| Object storage (managed) | MinIO (S3-compatible, per-bucket IAM service accounts) |
| Ingress | Traefik (per-deployment networks, Let's Encrypt certificates) |
| Container runtime | Docker (Compose for full-stack deploys) |
| OAuth | PKCE + auth code, JWT access tokens, 23 scopes |
| Encryption | AES-256-GCM (secrets, bucket credentials), TLS 1.2+ (transit) |
| Auth | JWT + optional SAML / OIDC SSO |
| Cloud single-container targets | AWS App Runner, Google Cloud Run, Azure Container Apps |
| Process supervision | systemd (`nexus-backend.service` with `StateDirectory=nexus/deployments nexus/docker`) |

---

## Reliability

NEXUS AI is built to keep stateful apps alive across host reboots, backend restarts, and manual stop/start cycles. The reliability layer:

- **Persistent compose workdirs** at `/var/lib/nexus/deployments` so the orchestrator survives `PrivateTmp` and `tmpfs` wipes
- **Soft stop semantics**: `docker compose stop` (not `down`) preserves containers, networks, volumes, and the port reservation
- **Boot reconciliation** runs 5 seconds after backend startup, verifies every `RUNNING` deployment is actually running, and restarts any that are down
- **Replica preservation** across restart: scale state survives stop/start and reboot
- **`restart: unless-stopped`** on every container so Docker brings them back automatically

Deep dive: [How NEXUS AI keeps your Postgres alive across host reboots](https://nexusai.run/blog/how-nexus-ai-keeps-your-postgres-alive-across-host-reboots).

---

## Security

- **Encryption at rest**: AES-256-GCM for all secrets, bucket credentials, and sensitive configuration
- **Encryption in transit**: TLS 1.2+ enforced across all endpoints
- **Tenant isolation**: per-organization runtime, networks, volumes, and S3 buckets. No shared application runtime or storage between customer organizations.
- **Per-bucket IAM**: every S3 bucket ships with a scoped MinIO service account, not platform-wide root credentials. Rotatable via `nexusai_bucket_rotate_credentials`.
- **Zero plaintext credentials**: Secrets never appear in code, container images, build logs, or runtime logs
- **Audit logging**: Every action (deployment, secret access, scope use, backup, restore, config change) logged with timestamp, actor identity (user or agent token name), and result
- **RBAC + scoped tokens**: Role-based access at organization and deployment level, plus 23 fine-grained OAuth scopes for least-privilege automation
- **Private runtimes**: Enterprise customers run fully isolated build and runtime environments
- **IP allowlisting**: Network-level access controls for Enterprise deployments

[Security overview](https://nexusai.run/security)

---

## HIPAA and Compliance

NEXUS AI provides HIPAA-aligned technical safeguards for regulated healthcare environments:

- **Infrastructure isolation**: Container-level isolation per deployment. No shared runtime between tenants.
- **Audit trails**: Deployment history, execution logs, change tracking, agent attribution, and user activity visibility
- **Secrets management**: Runtime injection only. No plaintext credentials in code, images, or logs.
- **Customer-owned cloud**: Enterprise customers deploy entirely within their own AWS, Google Cloud, or Azure accounts
- **Data residency**: Choose specific cloud regions for all workloads
- **BAA**: Business Associate Agreements available for Enterprise and Healthcare Pro customers
- **SSO**: SAML / OIDC support for Enterprise (satisfies HIPAA workforce access requirements)
- **Network controls**: IP allowlisting, private networks, and air-gapped environments for Enterprise

> **Shared responsibility.** NEXUS AI provides HIPAA-aligned infrastructure controls and is designed to support customer HIPAA compliance programs. Customers retain responsibility for their overall compliance posture, application logic, data classification, internal policies, and HIPAA program governance.

[HIPAA and Compliance details](https://nexusai.run/hipaa-compliance)

---

## Frequently Asked Questions

**What is NEXUS AI?**
NEXUS AI is an MCP-native application platform that deploys full-stack containerized applications (Postgres, MySQL, Mongo, Redis, S3 buckets, persistent volumes, workers, encrypted backups) in 5 minutes. Every platform action is callable as an MCP tool, so Claude, Cursor, Codex, and any MCP-compatible agent can deploy, scale, back up, restore, query the database, and roll back without leaving the chat.

**Where can I install the NEXUS AI MCP server?**
The official MCP Registry lists it at `io.github.nexusrun/nexus-ai`. Also indexed at mcp.so and Smithery. Direct endpoint: `https://api.zollo.live/mcp`.

**Which AI tools generate apps that NEXUS AI deploys?**
NEXUS AI deploys from any Git repository. Apps generated by Claude Code, Cursor, v0, Bolt, Lovable, Replit, Windsurf, or any other tool work the same way: push the result to GitHub and run `nexus deploy source --repo <url>`.

**Where do full-stack deploys actually run?**
Full-stack deploys (app + databases + storage + workers) run on the NEXUS AI managed Container platform with org-level isolation. Single-container deploys can also target AWS App Runner, Google Cloud Run, or Azure Container Apps.

**Does NEXUS AI require a DevOps team?**
No. NEXUS AI is designed so individual developers and small teams can deploy production-grade containerized applications without dedicated DevOps expertise. The platform handles container builds, deployment orchestration, secrets management, health checks, observability, and the database / storage / backup layer.

**Can I deploy from a GitHub repository?**
Yes. NEXUS AI supports deployments from GitHub repositories, container images, local source code, or AI-generated code through the same unified workflow.

**Is NEXUS AI HIPAA compliant?**
NEXUS AI provides HIPAA-aligned technical safeguards including tenant isolation, AES-256-GCM encrypted secrets, encrypted backups, scoped per-bucket IAM, full audit logs, and customer-owned cloud deployments. BAAs are available for Enterprise and Healthcare Pro plans.

**Can I use my own cloud account?**
Yes. Enterprise customers can deploy NEXUS AI entirely within their own AWS, Google Cloud, Azure, or on-premises infrastructure with no data leaving their environment.

**How does rollback work?**
Every deployment is versioned and immutable. You can restore any previous version with a single click from the deployment dashboard, the CLI (`nexus deploy rollback`), or an MCP call (`nexusai_deploy_rollback`). No manual re-deployment or downtime required.

**What happens to my secrets?**
Secrets are encrypted with AES-256-GCM and injected at container runtime only. They are never stored in plaintext, never appear in container images, and never appear in build or runtime logs. A full access audit trail is maintained.

**What happens to my data if the host reboots?**
Persistent volumes survive container restarts and host reboots. Boot reconciliation restarts any deployments the reboot did not bring back. Postgres / MySQL / Mongo crash recovery happens via their own journaling on next start. Full deep dive: [How NEXUS AI keeps your Postgres alive across host reboots](https://nexusai.run/blog/how-nexus-ai-keeps-your-postgres-alive-across-host-reboots).

**How is NEXUS AI different from Vercel, Render, Railway, or Fly.io?**
NEXUS AI is the only platform that combines (1) full-stack deploys in one command, (2) 59 MCP tools for AI agents to operate the platform end-to-end, (3) AI-powered database schema fixes from runtime logs, (4) per-bucket IAM out of the box, (5) HIPAA-aligned controls with customer-owned cloud deployments. See the comparison table above.

---

## Reading list

Recent engineering and product posts:

- [Your AI app is generated. Now how do you deploy it?](https://nexusai.run/blog/your-ai-app-is-generated-now-how-do-you-deploy-it). The deploy gap for AI-generated apps and how NEXUS AI closes it.
- [MCP-driven deploys: 5 tasks your Claude agent should be running for you](https://nexusai.run/blog/mcp-driven-deploys-5-tasks-your-claude-agent-should-run). Concrete operations to hand to an agent today.
- [From v0 prototype to production database in 5 minutes](https://nexusai.run/blog/from-v0-prototype-to-production-database-in-5-minutes). Tutorial.
- [How NEXUS AI keeps your Postgres alive across host reboots](https://nexusai.run/blog/how-nexus-ai-keeps-your-postgres-alive-across-host-reboots). Reliability deep dive.
- [Deploy a full-stack Python app with Postgres, Redis, and workers in 5 minutes](https://nexusai.run/blog/deploy-full-stack-python-postgres-redis-workers-5-minutes). Hands-on FastAPI tutorial.
- [Database backup and restore on NEXUS AI](https://nexusai.run/blog/database-backup-restore-nexus-ai). Backup mechanics.

---

## Links

| | |
|---|---|
| Website | [nexusai.run](https://nexusai.run) |
| Documentation | [nexusai.run/docs](https://nexusai.run/docs) |
| MCP Reference | [nexusai.run/docs#mcp-overview](https://nexusai.run/docs#mcp-overview) |
| Pricing | [nexusai.run/pricing](https://nexusai.run/pricing) |
| Healthcare Pricing | [nexusai.run/pricing/healthcare](https://nexusai.run/pricing/healthcare) |
| HIPAA and Compliance | [nexusai.run/hipaa-compliance](https://nexusai.run/hipaa-compliance) |
| Security | [nexusai.run/security](https://nexusai.run/security) |
| Blog | [nexusai.run/blog](https://nexusai.run/blog) |
| About | [nexusai.run/about](https://nexusai.run/about) |
| Contact / Sales | [nexusai.run/contact](https://nexusai.run/contact) |
| Official MCP Registry | [registry.modelcontextprotocol.io](https://registry.modelcontextprotocol.io/v0.1/servers?search=io.github.nexusrun/nexus-ai) |
| mcp.so listing | [mcp.so/server/nexusrun](https://mcp.so/server/nexusrun) |
| Smithery listing | [smithery.ai/server/saif-elyzal/NEXUSRUN](https://smithery.ai/server/saif-elyzal/NEXUSRUN) |

---

## Contact

- **Support**: support@nexusai.run
- **Sales**: [nexusai.run/contact](https://nexusai.run/contact)
- **LinkedIn**: [linkedin.com/company/nexusai-run](https://linkedin.com/company/nexusai-run)

---

© 2026 NEXUS AI, Inc. Built for engineers who ship.
- [![smithery badge](https://smithery.ai/badge/saif-elyzal/NEXUSRUN)](https://smithery.ai/servers/saif-elyzal/NEXUSRUN)
- [![smithery badge](https://smithery.ai/badge/sali/nexusai)](https://smithery.ai/servers/sali/nexusai)

---

© 2026 NEXUS AI, Inc. — Built for engineers who ship.
