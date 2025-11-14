# HVAC Business – Automated Lead Management & Sales Funnel (n8n)

This project is a complete lead management and sales funnel automation built for an HVAC and home-services company. The workflow runs inside n8n and connects four different lead sources, processes them through a standardized pipeline, scores each lead, and routes them into the right follow-up path.

The goal of this system is simple:  
**Capture every lead, score it accurately, respond fast, and keep the team focused on the right opportunities.**

---

## 📥 Lead Sources

The workflow collects leads from four channels:

### 1. Typeform Webhook
- Receives website form submissions in real time  
- Webhook endpoint: `/typeform-webhook`  
- Sends an immediate response back to Typeform

### 2. Clay API (Hourly Polling)
- Fetches enriched leads from the Clay API every hour  
- Uses Bearer token authentication  
- Converts Clay’s response into the unified lead format  

### 3. Facebook Lead Ads (Hourly Polling)
- Calls the Facebook Graph API once per hour  
- Pulls lead form submissions from active campaigns  
- Data is extracted from Facebook’s `field_data` structure  

### 4. Manual Phone Entries
- Manual trigger for call-in leads  
- Ensures offline inquiries are included in the flow  

---

## 🔄 Data Normalization

All leads are converted into one consistent structure.

### Common Schema
firstName
lastName
fullName
phone
email
serviceType
address
message
budget
urgency
source
timestamp


### Parsing Logic
- Typeform: Splits names, sanitizes phone numbers  
- Clay: Combines first/last names, maps API values to unified schema  
- Facebook: Extracts nested field data  
- Manual: Direct mapping  

### Merge Step
All parsed sources are combined into one unified pipeline.

---

## 🎯 Lead Scoring System

Each lead is scored on a 1–10 scale across four categories.

### Service Type
- AC Installation: 9  
- HVAC Repair: 8  
- Home Inspection / Maintenance: 7  
- Tune-Up: 6  

### Location
- San Diego City: 10  
- SD County + nearby cities (Chula Vista, La Mesa, El Cajon, Oceanside, Carlsbad): 8  
- California: 6  
- Other locations: 5  

### Budget
- 5K–10K+: 10  
- 3K–4K: 8  
- 1K–2K: 6  
- Not provided: 5  

### Urgency
- Emergency / ASAP / Urgent: 10  
- Today or This Week: 8  
- This Month: 6  
- Flexible: 4  

### Final Score Formula

### Lead Tiers
- **Hot:** 8–10  
- **Warm:** 6–7  
- **Cold:** 1–5  

---

## 🔀 Routing Logic

---

## 🔥 Hot Lead Path (Score 8+)

1. Send immediate email via Gmail  
2. Create job task in ClickUp  
3. Schedule Google Calendar appointment  
   - 2 days after lead  
   - Time: 10:00 AM–12:00 PM  
   - Location: customer address  
4. Send appointment confirmation email  

---

## ❄️ Warm / Cold Lead Path (Score ≤7)

1. Send initial acknowledgment email  
2. Wait 3 days  
3. Draft follow-up email  
4. ClickUp manual approval step  
   - Team member must comment **APPROVE EMAIL**  

---

## 📧 Email Templates

### Hot Lead – Immediate Response
- Personalized  
- Promises contact within 24 hours  

### Warm/Cold – Initial Email
- Simple thank-you  
- Sets slower response expectation  

### 3-Day Follow-Up
- Asks if customer wants to schedule a consultation  

### Appointment Confirmation
- Includes date, time window, and address  

---

## 🗂️ CRM Automation (ClickUp)

### Lead Task Format
**Name:**  

**Description Includes:**  
- Lead source  
- Score and tier  
- Contact details  
- Budget  
- Message  
- Urgency  

### Job Task Format (Hot Leads Only)
**Name:**  



Includes all customer and service details.

---

## 📅 Calendar Automation

Hot leads automatically receive a scheduled appointment:

- Date: 2 days from lead creation  
- Time: 10:00 AM – 12:00 PM  
- Location: Customer address  
- Customer added as calendar guest  
- Notifications enabled  

---

## 🔧 Required Credentials

- ClickUp OAuth  
- Gmail OAuth2  
- Google Calendar OAuth2  

### Replace These Placeholders

---

## 🧩 Key Nodes

### Trigger Nodes
- Manual Trigger  
- Typeform Webhook  
- Clay Polling  
- Facebook Polling  

### Data Processing
- Parse Typeform  
- Parse Clay  
- Parse Facebook  
- Parse Manual Lead  
- Merge Data  

### Lead Scoring & Routing
- Calculate Lead Score  
- Hot Lead Check  

### CRM
- Create ClickUp Tasks  
- Update Task Status  
- Job Task Creation  

### Hot Lead Actions
- Prepare Email  
- Send Email  
- Prepare Calendar Event  
- Create Calendar Event  
- Send Confirmation  

### Warm/Cold Actions
- Acknowledgment Email  
- Wait 3 Days  
- Prepare Follow-Up  
- Manual Approval  

---

## ⚙️ Workflow Settings

- Execution Mode: v1  
- Clay/Facebook Polling: Every 1 hour  
- Typeform Webhook: Instant  
- Wait Duration: 3 days  

---

## 💡 Summary

- Every lead enters a unified system  
- High-value leads receive fast follow-ups  
- Warm/cold leads follow a controlled sequence  
- Manual approval ensures quality control  
- The system reduces missed leads and improves response times  

---

If you need the workflow JSON or setup instructions, feel free to reach out.



