🤖 EC2 Remediation Assistant — Bringing AI Into Netflix’s Cloud Ops

When I first started experimenting with ServiceNow’s AI Agent Studio, I wanted to see how far I could push automation without losing the human touch. Netflix’s existing WL2 EC2 Remediation System was already doing a great job, but it still relied heavily on manual effort during peak hours.

Scenario proposed: What if DevOps engineers could just tell an AI, “Restart the instance that failed,” and it would handle the rest — cleanly, safely, and with full audit control?

That’s how this project started.

🧠 The Idea

During Netflix’s busiest streaming hours, EC2 incidents pile up fast. Engineers had to open the incident, copy the instance ID, run the remediation, then verify logs — all under pressure.

I built an AI-powered extension for the WL2 system that could:

Understand natural language descriptions like “Restart the EC2 instance for stream-node-09.”

Translate that into a valid EC2 instance ID.

Ask for human approval before running the same API remediation scripts the manual system used.

It’s not about replacing engineers — it’s about helping them breathe easier during chaos.

🛠️ How I Built It

This project lives inside ServiceNow, with a mix of familiar tools and a few new ones I learned on the fly.

Key pieces I worked on:

Built the AI Agent architecture in ServiceNow’s AI Agent Studio.

Created a Script Tool that bridges conversational input with the AWS Integration Server API.

Reused the existing RemediationHelper logic so the new system mirrors the manual one exactly — same logs, same API payloads.

Tested both approaches side-by-side to make sure the AI version never skipped a safety step.

I learned a lot about how to keep human-in-the-loop design functional — especially how to balance automation with operational trust.

💬 What It Feels Like to Use

You can interact with the system two ways:

Manual Mode: The old-school button that says “Restart EC2 Instance.”

AI Mode: You literally type, “Restart instance i-09ae69f1cb71f622e,” and the agent walks you through the process — confirming the instance, requesting approval, executing the script, and logging everything.

Both paths end up in the same Remediation Log table, so it’s fully traceable.

It’s surprisingly satisfying to watch the agent interpret a sentence, call the right API, and show you the same confirmation screen you’d get manually.

🧑‍💻 DevOps Usage

A quick guide for Netflix engineers on how to use both remediation modes effectively.

1️⃣ Manual Mode – “When you need control”
Use the traditional Restart EC2 Instance button when troubleshooting or verifying logs manually.

Best for: controlled maintenance windows, debugging, or non-urgent fixes.

Steps: Open the incident → click the UI Action → confirm execution → check the Remediation Log table for results.

2️⃣ AI Agent Mode – “When you need speed”
Use the EC2 Remediation Assistant when you want to handle incidents conversationally.

Example command:

Restart instance i-09ae69f1cb71f622e


Or let the agent find it:

Restart the instance for stream-node-23 that failed overnight


The agent identifies the EC2 ID, asks for approval, runs the same API call, and logs it automatically.

🧩 The Architecture (In Plain English)

Here’s how everything connects:

AWS EC2 → AWS Integration Server → ServiceNow Tables → Flow Designer Workflow → AI Agent Conversation Interface

It’s like giving the WL2 system a voice. The AI layer doesn’t replace anything — it just adds a smarter entry point for existing scripts.

🔍 What I Learned

This project was my deep dive into human-approved automation. I realized that the real challenge isn’t building the workflow — it’s making people trust the workflow.

Here are a few takeaways:

Natural language is powerful — but structure and context are everything.

Approval flows matter. Engineers want automation, not surprises.

Reusability beats reinvention. Adapting RemediationHelper.js saved time and reduced risk.

🚀 What’s Next

If I had more time (and maybe a few more cups of coffee ☕), I’d love to:

Add Slack or Teams integration, so approvals can happen directly in chat.

Set smart auto-remediation thresholds, where the system knows when it’s safe to fix something instantly.

💡 Try It Yourself

If you’re exploring ServiceNow’s AI Agent Studio or AWS integrations, this is a great project to experiment with. You can replicate it in a Yokohama PDI, reuse your own Script Include, and see how AI can sit naturally inside existing operations — not on top of them.

## 📸 Screenshot Placeholders
- AI Agent conversation demo
-  <img width="1899" height="919" alt="ec2 remediation agent success" src="https://github.com/user-attachments/assets/10e77161-17dd-4919-a1af-e32cb59825cd" />
 
- Successful remediation log entry
- <img width="913" height="535" alt="image" src="https://github.com/user-attachments/assets/bc5a6434-aab2-48a7-b4eb-a62e926e72ed" />

---



