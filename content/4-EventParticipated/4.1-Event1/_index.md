---
title: "Event 1"
date: 2026-06-27
weight: 1
chapter: false
pre: " <b> 4.1. </b> "
---

# FC Community Day Event Report (Online)

### Event information

- **Event name:** FC Community Day
- **Format:** A community event hosted onsite and broadcast through YouTube
- **Date:** June 27, 2026
- **Role:** Online participant
- **Audience:** Students, technology engineers, and people interested in Cloud and AI

### Event objectives

- Present several ways AI is being applied in enterprise environments.
- Share practical career experiences from the Cloud Engineering field.
- Demonstrate how Voice AI can support Vietnamese customer-service workflows.
- Introduce DevOps AI Agents for incident investigation and response.
- Discuss security requirements when connecting AI assistants to internal services and data.

### Speakers

- **Steve Tran** - Cloud career journey and the Cloud Thinker platform
- **Hieu Nghi, Anh Kiet, and Anh Trung** - Voice AI for the Vietnamese language
- **Nguyen and Bao (Cloud Kinetics)** - DevOps AI Agent
- **Truong and Minh Anh (Noventis)** - AI applications in human resources
- **Toan Nguyen and Hieu Nghi** - Amazon Q and secure enterprise AI architecture

### Key content

#### Cloud Engineering career development and Cloud Thinker

- Steve's story showed that a Cloud career does not follow one fixed path. Self-study, experimentation, changing direction when necessary, and gaining project experience are more valuable than collecting certificates without practical application.
- AI can contribute to Cloud operations by collecting context, accelerating log analysis, supporting FinOps, and assisting security investigation rather than functioning as another general-purpose chatbot.
- For large operational domains, multiple specialist agents can separate responsibilities more clearly. Human approval remains necessary before any action that could affect production.
- A useful career lesson was to build depth in a small number of core skills and participate early in projects that resemble real enterprise environments.

#### Voice AI for Vietnamese users

- A common Voice AI pipeline is: audio input → Speech-to-Text (STT) → language model → Text-to-Speech (TTS).
- Vietnamese includes tones and significant regional pronunciation differences. Training data, sentence breaks, and conversational context therefore need dedicated optimization rather than directly reusing an English-oriented model.
- With controlled tool calling, a voice assistant can perform authorized operations instead of only answering frequently asked questions.
- A production system also requires streaming to reduce latency, version management, audit logs, handoff to a human operator, and real-time monitoring.

#### DevOps AI Agents for incident response

- Traditional debugging becomes difficult when logs are distributed across services and each team only understands one part of the overall context.
- An AI Agent can start from a monitoring alert, collect related signals, propose hypotheses, validate them against evidence, and recommend a mitigation plan.
- Every proposed change should include supporting evidence and require approval before modifying a live system. After the incident, the agent can also recommend improvements to alerts and runbooks.
- The cases presented during the event showed that automating information collection can substantially reduce detection and recovery time.

#### AI-assisted human-resources workflows

- Reading resumes and comparing candidates with job requirements requires significant time and can produce inconsistent evaluations when criteria are unclear.
- Enterprise assistants such as Amazon Q can summarize resumes, match skills, draft job descriptions, and create candidate comparison reports.
- AI output should remain advisory. A responsible person must review the context and make the final recruitment decision.
- From an applicant's perspective, a resume should be clearly structured, accurately represent experience, and explain how that experience relates to the position.

#### Secure connections between AI and internal systems

- Enterprises must avoid exposing sensitive data through the public Internet when an AI assistant accesses internal applications or data sources.
- VPC Interface Endpoints and AWS PrivateLink can provide private communication paths. Authentication may be handled through Amazon Cognito or another suitable identity system.
- MCP (Model Context Protocol) standardizes how agents obtain context and call tools, but every connector must still follow least-privilege access.
- In addition to encryption, the architecture needs tool-call monitoring, audit logs, and explicit restrictions on operations the agent may perform.

### Lessons learned

- **AI operations depend on good context:** logs, metrics, and system documentation strongly affect the quality of agent analysis.
- **Human-in-the-loop is essential:** AI can recommend quickly, but people must approve high-impact changes.
- **Language problems require localization:** Vietnamese Voice AI needs specialized handling of tones, regional accents, and conversational rhythm.
- **Security must be designed from the beginning:** private networking, IAM, encryption, and audit logging should not be added only after a product is complete.
- **Practical projects create career value:** a complete system that includes deployment and troubleshooting demonstrates ability more clearly than theory alone.

### Application to my work

- For the Spring Boot system deployed on EC2, I can organize CloudWatch Logs and CloudWatch Alarms by error category so incident investigations have sufficient context.
- The DevOps AI Agent workflow suggests a useful project runbook: receive alert → inspect service logs → compare EC2 and RDS metrics → determine the cause → obtain approval before mitigation.
- Access to S3, SES, and RDS should remain limited to the application's responsibilities. Any future AI tool should use a separate IAM role and produce an access trail.
- The human-in-the-loop approach also applies to AI-assisted coding: suggestions should only be accepted after review, testing, and checking their effect on deployment configuration.
- The Voice AI pipeline demonstrates how a complex capability can be separated into independent, observable, and replaceable processing stages.

### Event experience

FC Community Day provided a broad view of where Cloud and AI meet in enterprise use cases. The presentations went beyond language models and covered infrastructure operations, voice interaction, recruitment, and data protection.

My main impressions were:

- The opening career story was motivating because it emphasized learning from failed attempts and project experience instead of presenting an idealized path.
- The Voice AI session showed how much specialized engineering is required for a reliable Vietnamese conversational product, especially around data quality and latency.
- The DevOps AI Agent workflow was closely related to my workshop because it connects directly to CloudWatch, EC2, and RDS operations.
- The security session made it clear that a useful agent also requires controlled permissions, monitoring, and approval when it can call internal tools.

#### Event images

<!-- TODO: Add screenshots that you personally captured while attending the event. -->

> Overall, the event helped me understand that AI creates the most value when it is placed inside a process with trustworthy data, controlled permissions, and people who remain accountable for final decisions. These principles can be applied directly while completing and operating my AWS system.

#### Content reference

- [Reference group's Event 3 report](https://friskchara02.github.io/eam-workshop-report/vi/4-eventparticipated/4.3-event3/)

