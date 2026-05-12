# Lab 1.3: Connect Your n8n Agent to Your Prototype

![banner](./assets/banner.png)

You've built two things. An AI agent that reads contracts and answers questions. And a web app that looks like a real product. Right now they have no idea the other exists.

This lab connects them.

By the end, you'll have one fully working product — a real contract review app where a user uploads a document, types a question, and gets an actual AI-generated answer back. Not a simulation. Not a dummy response. The real thing.

---

## The Big Idea: Every Product Has Two Sides

Before we start connecting anything, there's one idea worth understanding. It's the mental model behind this entire lab — and honestly, behind most products you've ever used.

Every product is made of two sides.

The **user-facing side** is everything the user sees and touches. The buttons, the layout, the chat panel, the upload area. It's what you built in Lab 1.2. It lives in the browser. It doesn't do the heavy thinking — it just collects what the user wants and passes it along.

The **intelligence side** is where the actual work happens. It never appears on screen. It receives the user's input, thinks about it, and sends an answer back. That's your n8n agent from Lab 1.1 — the thing that reads the contract, reasons over it, and writes a response.

Right now these two sides exist in complete isolation. Your web app has no way to reach your agent. Your agent has no idea your web app even exists.

This lab builds the bridge.

---

## Before You Start

This lab builds directly on both previous labs. Make sure you have:

✅ **Lab 1.1 complete** — your n8n contract review workflow is built and the AI agent responded correctly inside n8n's own chat interface

✅ **Lab 1.2 complete** — your Claude Code prototype is built, `index.html` opens in your browser, and the two-panel layout (contract viewer + chat) is working

If either of these isn't done, go back and complete them first. Both pieces need to be in place before this lab makes sense.

---

## Phase 1: Prepare the Agent to Receive Outside Messages

### Open the workflow from Lab 1.1

Log into your n8n account and open the contract review workflow you built in Lab 1.1. You are not creating a new one — this is the same workflow.

![flow](./assets/2.png)

> When you save a workflow in n8n, it stays on n8n's servers — not your computer. You can close the browser, come back days later, and everything is exactly as you left it.

---

### Delete the "When Chat Message Received" node

Find the node at the very beginning of your workflow labeled **"When Chat Message Received"**. Click it to select it, then press Delete.

This node only works inside n8n's own built-in chat. It listens for messages typed in n8n — and nowhere else. Your web app is outside of n8n, so this node can't hear it. We need to replace it with something that's open to the outside world.

![flow](./assets/3.png)

> Don't worry about breaking anything. Removing this node only disconnects the starting point. You'll reconnect everything in the next steps.

---

### Add the Webhook and Respond to Webhook nodes

Here's where the bridge gets built. And this is the right moment to understand what a webhook actually is.

A **webhook** is an address — like a phone number — that your agent publishes to the world. When your web app wants to ask the agent a question, it calls that number. The agent picks up, does its work, and calls back with the answer.

Right now your agent has no phone number. It only takes calls from inside n8n. Adding a webhook gives it a number that anyone — including your web app — can call.

Click the **(+)** button on the canvas, search for **"Webhook"**, and add it to the canvas. Then search for **"Respond to Webhook"** and add that one too.

You should now have both nodes sitting on the canvas, unconnected.

![flow](./assets/4.png)

These two always work together. Think of them as the front door and the reply:

| Node | What it does |
|---|---|
| **Webhook** | Answers the call. Receives the contract and the user's question from your web app. |
| **Respond to Webhook** | Sends the answer back. Returns the agent's response to your web app. |

![flow](./assets/5.png)

> Every question-and-answer interaction on the internet works this way. Something asks. Something else answers. Your web app will ask — the Webhook node receives it. Your agent will answer — the Respond to Webhook node delivers it. This is the same pattern behind every search, every login, every payment. You're building the same thing, just visually in n8n.

---

### Connect the Webhook node to the Extract from File node

Draw a connection from the **Webhook** node's output to the **Extract from File** node — the same node that was previously connected to the trigger you just deleted.

Your workflow now starts at the Webhook instead.

![flow](./assets/6.png)

> When a user uploads a contract in your web app, the file arrives at the webhook in a raw format that isn't readable text yet. The Extract from File node is what converts it into actual words the AI can read. Think of it like opening a sealed envelope — the file arrives sealed, this node opens it, and then the agent can read what's inside.

---

### Configure the Webhook node

Click the **Webhook** node to open its settings. Make these four changes in order:

**1. Set the HTTP Method to POST.**

There are two ways to use a webhook address — you can ask it for information, or you can send it information. We're sending it a contract and a question, so set this to **POST** (sending data). Think of it as the difference between checking a mailbox and dropping a letter in it. We're dropping a letter.

**2. Set the Response field to "Using 'Respond to Webhook' node".**

This tells n8n to wait until the agent finishes thinking before it sends a reply. Without this, n8n would send an empty response immediately — before the agent even reads the contract.

**3. Click "Add Option" and add: Field Name for Binary Data.**

This gives the uploaded contract a label so the rest of the workflow knows how to find it.

**4. Click "Add Option" again and add: Allowed Origins (CORS). Set the value to `*`.**

This one needs a small explanation. Browsers have a built-in safety rule: by default, your web app is only allowed to send information to the same place it was loaded from. Your prototype loads from your own computer, but the webhook lives on n8n's servers somewhere else. Without this setting, your browser will refuse to send anything — it'll block the request before n8n even gets a chance to receive it. Setting this to `*` is like telling the browser: "it's okay, you have permission to reach out to that address." Fine for building and testing.

![flow](./assets/7.png)

> If your app ever stops responding with no clear reason, and n8n shows no activity, this permission setting is almost always the cause. It's the most common invisible blocker when connecting a web app to an outside service.

After saving, you'll see your webhook address appear in the settings panel. It looks something like:

```
https://your-instance.app.n8n.cloud/webhook-test/your-unique-id
```

Copy this and keep it somewhere handy — you'll paste it into your web app in the next phase.

![flow](./assets/8.png)

---

### Connect the AI Agent to the Respond to Webhook node

Draw a connection from the **AI Agent** node's output to the **Respond to Webhook** node.

Your full workflow now follows this path:

**Webhook → Extract from File → AI Agent → Respond to Webhook**

![flow](./assets/9.png)

Before moving on, trace every connection visually. Every node in that chain must be linked. One missing connection and the whole thing stops.

> Your agent now has an address the outside world can reach. Once the workflow is running, any app — your prototype, a mobile app, anything — can send it a contract and a question and get a real AI answer back. This is exactly how real AI products work in production.

---

## Phase 2: Connect Your Web App to the Agent

### Go back to Claude Code — use the same conversation from Lab 1.2

Open the Claude desktop app and find the Claude Code session where you built the prototype in Lab 1.2. Use that exact same conversation — don't start a new one.

Claude Code's memory lives in the conversation. The session that built your prototype already knows what your app looks like, how it's structured, and where everything lives. If you open a new conversation, Claude starts fresh with no context — and you'd have to describe the whole project again before it can help.

> The conversation that built your prototype is the one that knows it best. Continue from there.

---

### Run the integration prompt

Copy the prompt below. Before running it, replace `<Your Webhook URL>` with the actual address you copied in the previous phase.

```
Now add this feature to the existing prototype:

A user uploads a contract file in the UI.
The user enters a message in the chat input.
When the user clicks the Send button:

1. Collect both:
   - The uploaded contract file
   - The user's chat message

2. Send both to this webhook URL:
   <Your Webhook URL>

3. After the webhook processes the request:
   - Capture the response returned by the webhook
   - Display that response inside the chat UI as the assistant reply

Replace the dummy hardcoded responses with this webhook integration.
```

Paste it into Claude Code and run it.

Claude will update only the part of the app that needs changing — the Send button behaviour. It won't touch the layout, the design, or anything else that's already working.

![flow](./assets/11.png)

---

## Phase 3: Test Everything

### Open the app in your browser

Go to your `contract-review-app` folder on your Desktop and open `index.html` the same way you have been since Lab 1.2.

---

### Activate the workflow in n8n, then send your first real message

Before testing in the browser, go back to n8n and click **"Execute Workflow"** first.

This is important. Your webhook address only works when the workflow is actively running. If you skip this step and go straight to testing, n8n won't receive anything and the app will appear to hang.

![flow](./assets/12.png)

With the workflow running, go to your browser. Upload the sample contract, type a question, and click Send.

You'll likely see an error. That's completely normal — and it's actually a good sign.

It means your web app successfully reached the agent. The error is coming from inside the workflow, not from a broken connection. The bridge is working. There's just one small configuration left.

> An error at this stage means your two sides are talking to each other. The connection is live. Now we just need to make sure the agent is reading the right message.

---

### Point the agent to the right input

Go back to n8n and open the **AI Agent** node.

Find the **user message** field. It's currently set to read from the old n8n chat — which no longer exists in this workflow. You need to update it to read from the webhook instead.

Replace whatever is in that field with this:

```
{{ $json.body.message }}
```

This tells the agent: "don't look for a hardcoded question — read whatever message the user just sent from the web app." The curly braces are n8n's way of saying "pull this value in live from what just arrived."

If that doesn't work, click on the Webhook node after a test run — you'll see exactly what arrived and can match the field name from there.

![flow](./assets/13.gif)

The contract file doesn't need updating — that part of the workflow is already reading it correctly. Only the user message field needs this change. Save the node.

> Not sure what field name to use? Go back to your Claude Code session and ask: "What field name are you sending the user message under?" You'll get the exact answer in one message.

---

### The final test

Go to n8n and click **"Execute Workflow"** again to put the agent back into listening mode.

Go to your browser. Upload the sample contract. Type this and click Send:

*"What is this contract about?"*

This time you'll get a real answer — pulled from the actual contract, reasoned over by your agent, and displayed right in your web app.

![flow](./assets/15.png)

Try a few more:

*"What are the payment terms?"*

*"What happens if either party wants to terminate early?"*

*"Are there any auto-renewal clauses?"*

Every answer comes from the actual document. Every response travels through your agent. The two sides of your product are now one.

---

## What You Built

![banner](./assets/17.png)

Take a moment to look at what you actually have.

A user opens a web app, uploads a contract, types a question, and gets a real AI answer back. One product. Two sides talking to each other through a single address — the webhook.

This is the same shape as every AI product in the market today. A user-facing experience on one side. An intelligence layer on the other. And a connection between them.

**The two sides of every product** — what users see and interact with on one side, what does the thinking on the other. Most products fail because these two sides don't talk well. Now you know how to connect them.

**Webhooks** — an address your agent publishes so the outside world can reach it. Your web app rings it, your agent answers, and the response comes back. That's the whole idea.

**Browser permissions (CORS)** — your browser needs explicit permission before it sends information from your app to an outside address. One setting in the webhook configuration handles this. If something stops working for no obvious reason, this is almost always why.

**Three labs, one product** — Lab 1.1 built the agent. Lab 1.2 built the interface. Lab 1.3 connected them. You now have something real.

---

[← Back to Week 1 Overview](../readme.md)
