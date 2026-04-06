# Setting Up OpenClaw on AWS

This guide walks you through launching an OpenClaw-ready EC2 instance on AWS using a pre-built AMI, connecting via SSH, and completing the OpenClaw installation.

---

## Prerequisites

- An AWS account ([sign up here](https://aws.amazon.com/))
- A terminal (Mac: `Cmd + Space` → type "Terminal" → Enter | Windows: `Win + R` → type "cmd" or use [Windows Terminal](https://aka.ms/terminal))
- An API key for your preferred AI model (OpenAI, Gemini, or Anthropic)

---

## Step 1 — Log In to AWS

Go to [https://aws.amazon.com/](https://aws.amazon.com/) and sign in to your account. You'll land on the AWS Management Console dashboard.

![alt text](./images/1.png)
---

## Step 2 — Find the AMI

1. In the top search bar, type **AMI** and select **AMIs** under EC2.
![alt text](./images/2.png)
2. You'll see the AMI Catalog dashboard. By default it shows **Owned by me** — click that tab and switch to **Public images**.
![alt text](./images/3.png)
3. In the search box, paste the AMI ID:

   ```
   ami-0bcfa8c91ee60d860
   ```
![alt text](./images/4.png)
4. You should see an AMI named **mahesh - all interview bootcamp**. Select it.
![alt text](./images/5.png)

---

## Step 3 — Launch an Instance from the AMI

1. With the AMI selected, click **Launch instance from AMI**.
![alt text](./images/6.png)
2. Fill in the instance configuration:
   - **Name:** Give your server a name (e.g., `openclaw-server`)
- ![alt text](./images/7.png)
   - **Instance type:** `m7i-flex.large`
  ![alt text](./images/8.png)

1. Under **Key pair**, click **Create new key pair**.
   - Enter a name for your key pair (e.g., `openclawkey`)
   - Click **Create key pair** — a `.pem` file will automatically download to your machine. **Keep this file safe.**
-  ![alt text](./images/9.png)
1. Click **Launch instance**.
   
![alt text](./images/10.png)

---

## Step 4 — Connect to Your Instance

1. In the EC2 console, click **Instances** in the left sidebar.
![alt text](./images/11.png)
2. Wait until your instance shows **Running** status, then click on it.
3. Click **Connect** (top right).
![alt text](./images/12.png)
4. Select the **SSH client** tab.
5. Copy the `chmod` command shown under step 3 — it looks like:

   ```bash
   chmod 400 "your-key-name.pem"
   ```

   Save this command — you'll need it shortly.

   ![alt text](./images/13.png)

6. Go back to the instance details and copy the **Public IPv4 address**.

   ![alt text](./images/14.png)

---

## Step 5 — Open a Terminal and Navigate to Your Key File

**Mac:** `Cmd + Space` → type "Terminal" → Enter  
**Windows:** `Win + R` → type `cmd` → Enter (or open Windows Terminal)

Navigate to the folder where your `.pem` key file was downloaded. For example, if it's in Downloads:

```bash
cd Downloads
```
![alt text](./images/15.png)


---

## Step 6 — Set Key Permissions

Run the `chmod` command you copied in Step 4:

```bash
chmod 400 "your-key-name.pem"
```

![alt text](./images/16.png)

---

## Step 7 — SSH into the Instance with Port Forwarding

Use the following SSH command template:

```bash
ssh -i "path/to/<key>.pem" -L 18789:localhost:18789 ubuntu@<Public-IP>
```

Replace:
- `path/to/<key>.pem` with the path to your downloaded key file
- `<Public-IP>` with the IPv4 address you copied in Step 4

**Example:**

```bash
ssh -i "/Users/sachin/Downloads/openclawkeydemo.pem" -L 18789:localhost:18789 ubuntu@18.222.180.213
```

![alt text](./images/17.png)

When prompted:

```
Are you sure you want to continue connecting (yes/no/[fingerprint])?
```

Type `yes` and press Enter.

![alt text](./images/18.png)

---

## Step 8 — Install OpenClaw

Run the install script:

```bash
curl -fsSL https://openclaw.ai/install.sh | bash

```

![alt text](./images/19.png)

When prompted:

```
◆  I understand this is personal-by-default and shared/multi-user use requires lock-down. Continue?
│  ○ Yes / ● No
```

Select **Yes** and press Enter.

![alt text](./images/20.png)

---

## Step 9 — Complete the OpenClaw Quickstart

Follow the interactive setup:

1. **Quickstart** — select `quickstart` to begin.

![alt text](./images/21.png)


2. **Select your AI model** — choose from OpenAI, Gemini, or Anthropic. Make sure you have an API key for the model you choose.
   > Need an API key? See: [OpenAI API Keys](https://platform.openai.com/api-keys) | [Anthropic API Keys](https://console.anthropic.com/) | [Google AI Studio](https://aistudio.google.com/)

![alt text](./images/22.png)

3. **Paste your API key** when prompted

![alt text](./images/23.png)

4. **Select a model** — for example: `gpt-4.1-mini`

![alt text](./images/24.png)

5. **Select channel** — you can skip this step for now.

![alt text](./images/25.png)

6. **Select provider** — you can skip this step for now.

![alt text](./images/26.png)

7. **Configure skills** — select **Yes** when asked.
   - Use **Space** to select/deselect skills
   - Use **Up/Down arrow keys** to navigate
   - Select all skills you want, then press Enter

![alt text](./images/27.png)

8. **Preferred Node package manager** — select `npm`.

   > You may see a warning that `camsnap` failed to install — this skill is not supported on all environments, so you can safely ignore it.

9.  **Optional API keys** — when asked for Google Places API, Notion API, OpenAI Whisper API, or ElevenLabs API keys, you can type **No** and skip for now.

10. **Hooks** — enable all hooks when prompted.

![alt text](./images/28.png)
---

## Step 10 — Open OpenClaw in Your Browser

1. Open a **new terminal window** and run the same SSH command from Step 7 again (keep the first terminal open).

![alt text](./images/29.png)

![alt text](./images/30.png)



2. From the **first terminal**, copy the local URL that OpenClaw printed (it will look like `http://localhost:18789`).


![alt text](./images/31.png)

3. Paste it into your browser.

OpenClaw is now installed and running successfully.

![alt text](./images/32.png)

---

## Troubleshooting

### Issue: `brew` version installed / `brew` not found

If the installer detects a Homebrew-installed version of a dependency or throws a `brew`-related error, first ensure Homebrew is properly installed and up to date.

**Install Homebrew (Mac only):**

```bash
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
```

After installation, add Homebrew to your PATH if prompted (copy and run the commands shown in the installer output), then verify:

```bash
brew --version
```

**Update Homebrew:**

```bash
brew update && brew upgrade
```

Once Homebrew is installed and up to date, re-run the OpenClaw install command from Step 8:

```bash
curl -fsSL https://openclaw.ai/install.sh | bash
```

---

### Issue: SSH connection refused

- Confirm your instance is in **Running** state in the EC2 console.
- Confirm the **Security Group** attached to your instance allows inbound SSH (port 22) from your IP.
- Double-check the Public IPv4 address — it changes if you stop and restart the instance.

---

### Issue: Port 18789 not accessible in browser

- Make sure your SSH command includes the `-L 18789:localhost:18789` flag.
- Confirm OpenClaw started successfully in the terminal (look for a URL printed to the console).
- Try refreshing after a few seconds — the server may still be starting up.