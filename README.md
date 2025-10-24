🤖 EC2 Remediation Assistant — Bringing AI Into Netflix’s Cloud Ops

When I first started experimenting with ServiceNow’s AI Agent Studio, I wanted to see how far I could push automation without losing the human touch. Netflix’s existing WL2 EC2 Remediation System was already doing a great job, but it still relied heavily on manual effort during peak hours.

Scenario proposed: What if DevOps engineers could just tell an AI, “Restart the instance that failed,” and it would handle the rest — cleanly, safely, and with full audit control?

That’s how this project started.

🧠 The Idea

During Netflix’s busiest streaming hours, EC2 incidents pile up fast. Engineers had to open the incident, copy the instance ID, run the remediation, then verify logs.

I built an AI-powered extension for the WL2 system that could:

Understand natural language descriptions like “Restart the EC2 instance for stream-node-09.”

Translate that into a valid EC2 instance ID.

Ask for human approval before running the same API remediation scripts the manual system used.

🛠️ How I Built It

This project lives inside ServiceNow, with a mix of familiar tools and a few new ones I learned on the fly.

Key pieces I worked on:

Built the AI Agent architecture in ServiceNow’s AI Agent Studio.

Created a Script Tool that bridges conversational input with the AWS Integration Server API.

Reused the existing RemediationHelper logic so the new system mirrors the manual one exactly (same logs, same API payloads).

Tested both approaches side-by-side to make sure the AI version never skipped a safety step.

I learned a lot about how to keep human-in-the-loop design functional. 

💬 What It Feels Like to Use

You can interact with the system two ways:

Manual Mode: The old-school button that says “Restart EC2 Instance.”

AI Mode: You literally type, “Restart instance i-09ae69f1cb71f622e,” and the agent walks you through the process — confirming the instance, requesting approval, executing the script, and logging everything.

Both paths end up in the same Remediation Log table, so it’s fully traceable.

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

- AI Agent conversation demo/ Succesful remediation log entry
<img width="1868" height="893" alt="image" src="https://github.com/user-attachments/assets/4bd5fab2-b26e-4120-b8da-59fcacfffa9f" />


The agent identifies the EC2 ID, asks for approval, runs the same API call, and logs it automatically.

🧩 The Architecture 

Here’s how everything connects:

AWS EC2 → AWS Integration Server → ServiceNow Tables → Flow Designer Workflow → AI Agent Conversation Interface
<img width="1024" height="1024" alt="Diagram" src="https://github.com/user-attachments/assets/e52e7812-bb66-4b21-9ddd-341a65648d4a" />

The AI layer doesn’t replace anything, it just adds a smarter entry point for existing scripts.

🔍 What I Learned

This project was my deep dive into human-approved automation. 

🚀 What’s Next

If I had more time (and maybe a few more cups of coffee ☕), I’d love to:

Add Slack or Teams integration, so approvals can happen directly in chat.

Set smart auto-remediation thresholds, where the system knows when it’s safe to fix something instantly.

💡 Try It Yourself

If you’re exploring ServiceNow’s AI Agent Studio or AWS integrations, this is a great project to experiment with. 





