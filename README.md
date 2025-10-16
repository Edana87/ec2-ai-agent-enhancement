 🤖 EC2 AI Agent Enhancement System – ServiceNow Implementation

---

## 🏢 Company Context
Following the successful deployment of Netflix’s **WL2 Manual EC2 Remediation System**, DevOps engineers reported faster incident response times.  
However, during peak streaming hours, multiple EC2 failures still required **manual parsing of incident descriptions, instance identification, and UI navigation**, creating operational bottlenecks.

This project introduces an **AI Agent enhancement** to streamline remediation workflows while retaining manual fallback options.

---

## 🎯 Objective
Enhance the existing manual EC2 remediation system with capabilities that:
- Identify EC2 instance IDs from **natural language incident descriptions**  
- Provide **human-in-the-loop conversational remediation**  
- Execute the same **proven remediation scripts** via AI Agent  
- Maintain **identical logging** to the manual system  

**Outcome:** Faster, more scalable incident response while preserving operational oversight.

---

## 👩‍💻 Edana’s Role
As a **ServiceNow Administrator and Jr Developer**, Edana was responsible for:
- Designing the **AI Agent architecture**  
- Implementing a **Script Tool** that converts conversational input to API calls  
- Integrating the AI Agent with existing manual workflows and **AWS Integration Server**  
- Conducting **comparative testing** between manual and AI-enhanced remediation  

---

## 🛠️ Technologies Used
| Component | Purpose |
|-----------|---------|
| **ServiceNow PDI (Yokohama)** | AI Agent, Script Tool, Flow Designer, Update Set management |
| **AWS Integration Server** | EC2 instance remediation API execution |
| **Draw.io** | Architecture diagram creation |
| **RemediationHelper Script Include** | Existing remediation logic reused in AI Script Tool |
| **ServiceNow Tables** | `x_snc_ec2_instance`, `x_snc_remediation_log`, `sn_aia_agent`, `sn_aia_agent_tool_m2m` |

---

## 🧩 System Overview
The **Enhanced EC2 Remediation System** introduces a **conversational AI layer** while maintaining full compatibility with the manual WL2 system.

**Dual Mode Operation:**
1. **Manual UI Action** – Existing “Restart EC2 Instance” button  
2. **AI Agent Conversation** – Example: *“Restart instance i-09ae69f1cb71f622e”*  

**Shared Features:**
- Both use the **same AWS Integration Server API**  
- Both write to **Remediation Log** table  
- Both maintain **human approval workflows**  

---

## 📝 Implementation Steps

### ⚙️ Step 1: AI Agent Creation
- **Name:** EC2 Remediation Assistant  
- **Description:** Conversational assistant for DevOps to remediate EC2 incidents  
- **Role:** EC2 remediation specialist for DevOps operations  
- **Functions:**
  - Read incident descriptions  
  - Identify EC2 instance IDs  
  - Request human approval  
  - Execute remediation scripts via API  

---

### 🧮 Step 2: Script Tool Implementation
- **Purpose:** Translate natural language input → valid EC2 instance IDs → API calls  
- **Configuration:**
  - Input Schema: `instance_id` (LLM-friendly)  
  - Execution Mode: Supervised (human approval required)  
  - Logic: Adapts `RemediationHelper` Script Include  
- **Integration:** Maintains identical logging and API calls as manual remediation  

---

### 🔗 Step 3: Agent Tool Configuration
- Add Script Tool to **EC2 Remediation Assistant** in AI Agent Studio  
- Configure parameters to accept `instance_id` and provide **human-readable responses**  
- Validate **tool-agent linkage** via `sn_aia_agent_tool_m2m` table  

---

### 🧪 Step 4: Testing & Validation
**Scenarios:**
| Scenario | Expected Behavior |
|----------|------------------|
| Direct Instance ID Request | Extract ID, request approval, trigger API |
| Incident-Based Request | Read incident → identify instance ID → request approval |
| Invalid Input | Display error, no execution |
| Approval Flow | Wait for human confirmation before execution |

**Integration Verification:**
- Logs entries in **Remediation Log table**  
- Confirms identical API payloads and responses  
- Tests manual vs AI Agent execution on same instances  

---

### 🧾 Step 5: System Analysis
| Aspect | Manual WL2 | AI Agent |
|--------|------------|----------|
| Input Method | Button click | Natural language |
| Approval | Immediate | Conversational prompt |
| Execution Logic | Direct Script Include | Script Tool → RemediationHelper.js |
| Logging | Remediation Log | Same table |
| Efficiency | Manual lookup slows response | Auto-ID parsing accelerates response |

**Use Cases:**
- **Manual:** Debugging or controlled maintenance  
- **AI Agent:** Peak streaming hours, multi-incident remediation  

---

## 🗺️ Architecture Diagram
📁 *Diagram.png* (created in Draw.io)  

**Workflow Overview:**
AWS EC2 → AWS Integration Server → ServiceNow EC2 Table → Flow Designer Workflow
↘︎ Manual UI Action → RemediationHelper.js
↘︎ AI Agent Conversation → Script Tool → RemediationHelper.js → AWS API

yaml
Copy code

---

## 🧰 Update Set Components
Ensure your update set includes:
- **AI Agent Definition** (`sn_aia_agent`)  
- **Script Tool** (`sn_aia_agent_tool`)  
- **Agent-Tool Relationships** (`sn_aia_agent_tool_m2m`)  
- **Execution Plans** (`sn_aia_execution_plan`)  
- **Execution Plan Tasks** (`sn_aia_execution_plan_task`)  
- **AWS Connection & Credentials**  
- **EC2 Instance & Remediation Log records**  

---

## 📸 Screenshot Placeholders
- AI Agent conversation demo  
- Human approval flow  
- Successful remediation log entry  
- API response verification  

---

## 🚀 Optimization & Future Enhancements
- **Slack/Teams Integration:** Approve or trigger remediation from messaging platforms  
- **Enhanced NLP Parsing:** Handle multiple incident formats and edge cases  
- **Auto-Remediation Threshold:** Define safe conditions for auto-execution without approval  

---

## 🙏🏾 Thanks for Scrolling This Far
This project demonstrates how AI can **enhance human workflows** without replacing operational control.  
Built with precision, patience, and just a touch of caffeine ☕.  
