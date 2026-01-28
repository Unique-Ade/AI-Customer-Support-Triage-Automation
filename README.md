# AI Customer Support Ticket Triage & Routing Automation

## Overview

This project implements an **AI-powered customer support ticket triage and routing system** designed to reflect how modern US-based companies manage customer support operations at scale.

Incoming support tickets are automatically:
- Classified using AI
- Prioritized based on urgency and business impact
- Stored centrally for auditing and analytics
- Routed to appropriate operational queues
- Escalated immediately when high priority is detected

The workflow emphasizes **clean architecture, extensibility, and production-ready practices**.

---

## Key Features

### 🤖 AI Ticket Classification
Each support ticket is analyzed to extract structured insights:
- **Category**: Billing, Technical, Feature Request, General
- **Priority**: Low, Medium, High
- **Sentiment**: Positive, Neutral, Negative
- **Urgency flag**
- **Reasoning** for transparency and auditability

---

### 🚨 High-Priority Escalation
- Tickets marked as **High priority** trigger an **immediate email alert**
- Enables faster response to business-critical incidents
- Mimics real on-call and escalation workflows used in production systems

---

### 🔀 Category-Based Routing
Non-urgent tickets are routed using switch-based logic:

- **Billing** → Finance / Billing Queue  
- **Technical** → Engineering Support Queue  
- **Feature Request** → Product Backlog  
- **General** → General Support Queue  

Routing is implemented using named placeholder nodes to represent real enterprise systems.

---

### 🗄️ Centralized Storage (Supabase)
All tickets and AI classification outputs are stored in Supabase for:
- Auditing and compliance
- Analytics and reporting
- SLA measurement
- Historical trend analysis
- Future model improvements

Supabase serves as the **single source of truth**.

---

## Workflow Overview

![Workflow Overview](./workflow-overview.png)

> The workflow begins with a webhook trigger, followed by AI classification, database storage, routing logic, and conditional escalation.

---

## Example Test Request (PowerShell / curl)

```powershell
$body = @{
  ticket_id = "TCK-200001"
  customer_name = "Sarah Mitchell"
  customer_email = "sarah.mitchell@example.com"
  message = "Our production system is completely down and customers cannot place orders. This is impacting revenue."
  source = "support_form"
  submitted_at = "2026-01-27T09:15:00Z"
} | ConvertTo-Json -Depth 3

Invoke-WebRequest `
  -Uri "https://your-n8n-domain/webhook/customer-ticket-info" `
  -Method POST `
  -Headers @{ "Content-Type" = "application/json" } `
  -Body $body
```

---

## Workflow Architecture

1. **Webhook Trigger**
   - Receives incoming customer ticket data

2. **AI Classification (HTTP Request)**
   - Sends ticket details to an AI model
   - Receives structured classification output

3. **Data Normalization**
   - Parses and extracts AI response into usable fields

4. **Database Storage**
   - Stores tickets and AI outputs in Supabase

5. **Routing Logic**
   - Switch node routes tickets by category and priority

6. **Escalation Handling**
   - High-priority tickets trigger email notifications

---

## What I Learned

Through this project, I gained hands-on experience with:
- Designing production-grade automation workflows
- Structuring HTTP requests (headers, body, authentication)
- Handling API errors and conflict responses gracefully
- Parsing and normalizing AI outputs for downstream use
- Implementing centralized data storage for auditing and analytics
- Separating urgency handling from category-based routing
- Designing extensible systems that support future integrations

---

## Technologies Used

- **n8n** – Workflow orchestration
- **OpenAI API** – AI classification and sentiment analysis
- **Supabase** – Database and storage
- **Email Service** – Escalation alerts
- **HTTP Webhooks** – External integrations
- **PowerShell / curl** – Testing and validation

---

## Design Principles

- Single source of truth for all ticket data
- Clear separation of responsibilities
- Extensible and maintainable architecture
- Production-oriented error handling
- Human-in-the-loop escalation where required

---

## Future Enhancements

- Integration with ticketing systems (Zendesk, Jira, Linear)
- SLA timers and breach notifications
- Analytics dashboards
- Feedback loop for AI model improvement
- Role-based routing and access control

---

## Author

**Adeola Olagbenro**  
Automation & AI Workflow Engineer  
