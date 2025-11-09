# Email Signature Sending Setup Guide with n8n

## 📋 Table of Contents

1. [Prerequisites](#prerequisites)
2. [Installing n8n on Your Server](#installing-n8n-on-your-server)
3. [Setting Up Email Service](#setting-up-email-service)
4. [Creating the n8n Workflow](#creating-the-n8n-workflow)
5. [Securing Your Webhook](#securing-your-webhook)
6. [Updating Your Astro Application](#updating-your-astro-application)
7. [Testing the Integration](#testing-the-integration)
8. [Troubleshooting](#troubleshooting)

---

## 1. Prerequisites

Before starting, ensure you have:

- ✅ A server (VPS) with root/sudo access (Ubuntu 20.04+ recommended)
- ✅ Node.js 18+ installed
- ✅ A domain name (optional but recommended)
- ✅ An email service account (Gmail, SendGrid, or SMTP server)
- ✅ Basic knowledge of SSH and command line

---

## 2. Installing n8n on Your Server

### Option A: Using npm (Recommended for Development)

```bash
# SSH into your server
ssh user@your-server-ip

# Install n8n globally
npm install n8n -g

# Start n8n
n8n start
```

n8n will be available at `http://your-server-ip:5678`

### Option B: Using Docker (Recommended for Production)

```bash
# Install Docker if not already installed
curl -fsSL https://get.docker.com -o get-docker.sh
sudo sh get-docker.sh

# Create a directory for n8n data
mkdir -p ~/.n8n

# Run n8n with Docker
docker run -it --rm \
  --name n8n \
  -p 5678:5678 \
  -v ~/.n8n:/home/node/.n8n \
  n8nio/n8n
```

### Option C: Using PM2 for Production (Keeps n8n Running)

```bash
# Install PM2
npm install pm2 -g

# Install n8n
npm install n8n -g

# Start n8n with PM2
pm2 start n8n

# Save PM2 configuration
pm2 save

# Set PM2 to start on server reboot
pm2 startup
```

### Setting Up Nginx Reverse Proxy (Optional but Recommended)

```bash
# Install Nginx
sudo apt update
sudo apt install nginx -y

# Create Nginx configuration
sudo nano /etc/nginx/sites-available/n8n
```

Add this configuration:

```nginx
server {
    listen 80;
    server_name n8n.yourdomain.com;  # Change this to your domain

    location / {
        proxy_pass http://localhost:5678;
        proxy_http_version 1.1;
        proxy_set_header Upgrade $http_upgrade;
        proxy_set_header Connection 'upgrade';
        proxy_set_header Host $host;
        proxy_cache_bypass $http_upgrade;
    }
}
```

```bash
# Enable the site
sudo ln -s /etc/nginx/sites-available/n8n /etc/nginx/sites-enabled/
sudo nginx -t
sudo systemctl restart nginx
```

### Setting Up SSL with Let's Encrypt (Highly Recommended)

```bash
# Install Certbot
sudo apt install certbot python3-certbot-nginx -y

# Get SSL certificate
sudo certbot --nginx -d n8n.yourdomain.com

# Certbot will automatically configure Nginx for HTTPS
```

---

## 3. Setting Up Email Service

### Option A: Using Gmail (Easiest for Testing)

1. **Enable 2-Step Verification** on your Gmail account
2. **Create an App Password**:
   - Go to Google Account → Security
   - Under "Signing in to Google", click "App passwords"
   - Generate a new app password for "Mail"
   - Save this password (you'll need it in n8n)

### Option B: Using SendGrid (Recommended for Production)

1. Sign up at [SendGrid](https://sendgrid.com/)
2. Create an API key:
   - Go to Settings → API Keys
   - Create API Key with "Full Access"
   - Save the API key

### Option C: Using Your Own SMTP Server

You'll need:

- SMTP Host (e.g., `mail.yourdomain.com`)
- SMTP Port (usually 587 for TLS or 465 for SSL)
- Username
- Password

---

## 4. Creating the n8n Workflow

### Step 1: Access n8n

1. Open your browser and go to `http://your-server-ip:5678` or `https://n8n.yourdomain.com`
2. Create an account (first user becomes the admin)

### Step 2: Create New Workflow

1. Click **"New Workflow"**
2. Name it: `Email Signature Sender`

### Step 3: Add Webhook Node

1. Click the **"+"** button
2. Search for **"Webhook"**
3. Configure the webhook:

   - **HTTP Method**: `POST`
   - **Path**: `email-signature`
   - **Response Mode**: `Respond Immediately`
   - **Response Code**: `200`
   - **Response Data**: `First Entry JSON`

4. Click **"Execute Node"** to get your webhook URL (save this!)
   - Example: `https://n8n.yourdomain.com/webhook/email-signature`

### Step 4: Add Code Node (to Process Image Data)

1. Add a new node → Search for **"Code"**
2. Rename it to: `Process Image Data`
3. Add this code:

```javascript
// Get data from webhook
const email = $input.first().json.email;
const userName = $input.first().json.userName;
const imageData = $input.first().json.imageData;

// Remove data URL prefix if present
const base64Data = imageData.replace(/^data:image\/\w+;base64,/, "");

// Convert base64 to buffer for attachment
const buffer = Buffer.from(base64Data, "base64");

return {
  json: {
    email: email,
    userName: userName,
    subject: `Your Email Signature - ${userName}`,
    emailBody: `
      <html>
        <body style="font-family: Arial, sans-serif; padding: 20px; background-color: #f5f5f5;">
          <div style="max-width: 600px; margin: 0 auto; background: white; padding: 30px; border-radius: 10px; box-shadow: 0 2px 10px rgba(0,0,0,0.1);">
            <h2 style="color: #333;">Your Email Signature is Ready! 🎉</h2>
            <p style="color: #666; line-height: 1.6;">
              Hi ${userName},<br><br>
              Thank you for creating your email signature with us! Your personalized signature is attached to this email.
            </p>
            <h3 style="color: #333; margin-top: 30px;">How to Use Your Signature:</h3>
            <ol style="color: #666; line-height: 1.8;">
              <li>Download the attached PNG image</li>
              <li>Open Gmail Settings (gear icon → "See all settings")</li>
              <li>Go to the "General" tab</li>
              <li>Scroll down to "Signature" section</li>
              <li>Click "Create new" and name it "Romega Solutions"</li>
              <li>Click the image icon and upload your downloaded signature</li>
              <li>Set as default for new emails and replies</li>
              <li>Click "Save Changes" at the bottom</li>
            </ol>
            <div style="margin-top: 30px; padding: 20px; background: #f8f9fa; border-left: 4px solid #007bff; border-radius: 5px;">
              <p style="color: #666; margin: 0;">
                <strong>💡 Tip:</strong> Make sure to insert the image at its original size for best quality!
              </p>
            </div>
            <p style="color: #999; font-size: 12px; margin-top: 30px; border-top: 1px solid #eee; padding-top: 20px;">
              If you have any questions, feel free to reach out to our IT or HR team.
            </p>
          </div>
        </body>
      </html>
    `,
    fileName: `${userName
      .toLowerCase()
      .replace(/\s+/g, "_")}_email_signature.png`,
  },
  binary: {
    data: {
      data: buffer.toString("base64"),
      mimeType: "image/png",
      fileName: `${userName
        .toLowerCase()
        .replace(/\s+/g, "_")}_email_signature.png`,
    },
  },
};
```

### Step 5: Add Send Email Node

#### For Gmail:

1. Add new node → Search for **"Gmail"**
2. Click **"Create Credential"**
3. Follow OAuth2 flow to connect your Gmail account
4. Configure email:
   - **Resource**: `Message`
   - **Operation**: `Send`
   - **To**: `={{ $json.email }}`
   - **Subject**: `={{ $json.subject }}`
   - **Email Type**: `HTML`
   - **Message**: `={{ $json.emailBody }}`
   - **Attachments**:
     - Property Name: `data`
     - Add Options → Enable **Binary Property**

#### For SendGrid:

1. Add new node → Search for **"SendGrid"**
2. Create credential with your API key
3. Configure:
   - **Resource**: `Mail`
   - **Operation**: `Send`
   - **From Email**: `noreply@yourdomain.com`
   - **To Email**: `={{ $json.email }}`
   - **Subject**: `={{ $json.subject }}`
   - **Content**: `={{ $json.emailBody }}`
   - **Content Type**: `text/html`
   - **Attachments**:
     - Content: `={{ $binary.data.data }}`
     - Filename: `={{ $json.fileName }}`
     - Type: `image/png`

#### For Custom SMTP:

1. Add new node → Search for **"Send Email"**
2. Create SMTP credential:
   - **Host**: Your SMTP server
   - **Port**: 587 (TLS) or 465 (SSL)
   - **Username**: Your email
   - **Password**: Your password
3. Configure email (same as Gmail above)

### Step 6: Connect the Nodes

Connect them in this order:

```
Webhook → Process Image Data → Send Email
```

### Step 7: Activate the Workflow

1. Click **"Save"** (top right)
2. Toggle the **"Active"** switch to ON

---

## 5. Securing Your Webhook

### Add Authentication Header

1. Go back to the **Webhook** node
2. Under **"Options"**, add:
   - **Header Authentication**
   - Name: `Authorization`
   - Value: Create a secure token (e.g., `Bearer your-secret-token-here-12345`)

### Generate a Strong Secret Token

```bash
# On your server, generate a random token
node -e "console.log(require('crypto').randomBytes(32).toString('hex'))"
```

Save this token - you'll need it in your Astro app!

---

## 6. Updating Your Astro Application

### Create Environment Variables

Create a `.env` file in your Astro project:

```bash
# .env
PUBLIC_N8N_WEBHOOK_URL=https://n8n.yourdomain.com/webhook/email-signature
PUBLIC_N8N_AUTH_TOKEN=your-secret-token-here-12345
```

**Important**: Add `.env` to your `.gitignore` file!

### Update DownloadButtons.astro

Replace the "Send to Email" button handler with this code:

```typescript
// Send to Email Button Handler (UPDATED)
if (sendEmailBtn) {
  sendEmailBtn.addEventListener("click", async () => {
    const dataUrl = await generateSignatureImage(sendEmailBtn);

    if (!dataUrl) return;

    // Get the user's email and name from the form
    const emailElement = document.querySelector(
      '[data-field="email"]'
    ) as HTMLElement | null;
    const userEmail = emailElement?.textContent?.trim() || "";

    const nameElement = document.querySelector(
      '[data-field="name"]'
    ) as HTMLElement | null;
    const userName = nameElement?.textContent?.trim() || "User";

    if (!userEmail) {
      alert("Please enter an email address in the form.");
      return;
    }

    // Show loading state
    const originalHTML = sendEmailBtn.innerHTML;
    sendEmailBtn.innerHTML =
      '<i data-lucide="loader" class="w-5 h-5 animate-spin"></i> Sending...';
    sendEmailBtn.disabled = true;

    try {
      // Send to n8n webhook
      const response = await fetch(import.meta.env.PUBLIC_N8N_WEBHOOK_URL, {
        method: "POST",
        headers: {
          "Content-Type": "application/json",
          Authorization: `Bearer ${import.meta.env.PUBLIC_N8N_AUTH_TOKEN}`,
        },
        body: JSON.stringify({
          email: userEmail,
          userName: userName,
          imageData: dataUrl,
        }),
      });

      if (!response.ok) {
        throw new Error("Failed to send email");
      }

      // Show success message
      sendEmailBtn.innerHTML =
        '<i data-lucide="check" class="w-5 h-5"></i> Sent!';

      // Update dialog with email and show it
      if (sentToEmailSpan) {
        sentToEmailSpan.textContent = userEmail;
      }

      if (emailDialog) {
        emailDialog.style.display = "flex";

        // Re-initialize lucide icons in the dialog
        if (window.lucide) {
          window.lucide.createIcons();
        }
      }

      // Reset button after a delay
      setTimeout(() => {
        sendEmailBtn.innerHTML = originalHTML;
        sendEmailBtn.disabled = false;
        if (window.lucide) {
          window.lucide.createIcons();
        }
      }, 3000);
    } catch (error) {
      console.error("Error sending email:", error);
      alert(
        "Failed to send email. Please try again or download the image instead."
      );
      sendEmailBtn.innerHTML = originalHTML;
      sendEmailBtn.disabled = false;
      if (window.lucide) {
        window.lucide.createIcons();
      }
    }
  });
}
```

---

## 7. Testing the Integration

### Step 1: Test n8n Workflow Directly

1. In n8n, click **"Execute Workflow"** button
2. Use this test payload in the Webhook node:

```json
{
  "email": "test@example.com",
  "userName": "Test User",
  "imageData": "data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAAAEAAAABCAYAAAAfFcSJAAAADUlEQVR42mNk+M9QDwADhgGAWjR9awAAAABJRU5ErkJggg=="
}
```

3. Check if the email is received

### Step 2: Test from Your Application

1. Run your Astro app: `npm run dev`
2. Fill out the email signature form
3. Click "Send to Email"
4. Check your inbox (including spam folder)

### Step 3: Monitor n8n Executions

1. In n8n, go to **"Executions"** tab
2. Check the execution logs for any errors
3. Click on each execution to see detailed logs

---

## 8. Troubleshooting

### Common Issues and Solutions

#### ❌ "Webhook not found" Error

**Solution**: Make sure the workflow is active (toggle switch is ON)

#### ❌ Email not received

**Solutions**:

- Check spam/junk folder
- Verify email credentials in n8n
- Check n8n execution logs for errors
- For Gmail: Ensure app password is correct
- For SendGrid: Verify API key has sending permissions

#### ❌ CORS Error in Browser

**Solution**: Add CORS headers to your webhook response:

In the Webhook node, under "Options" → "Response Headers":

```json
{
  "Access-Control-Allow-Origin": "*",
  "Access-Control-Allow-Methods": "POST, OPTIONS",
  "Access-Control-Allow-Headers": "Content-Type, Authorization"
}
```

#### ❌ Image too large (413 Payload Too Large)

**Solution**: Increase Nginx body size limit:

```bash
sudo nano /etc/nginx/nginx.conf
```

Add inside `http` block:

```nginx
client_max_body_size 10M;
```

```bash
sudo systemctl restart nginx
```

#### ❌ Environment variables not working

**Solutions**:

- Restart your dev server after adding `.env`
- Ensure variables start with `PUBLIC_` prefix
- Check `.env` is in the project root
- Verify `.env` syntax (no spaces around `=`)

#### ❌ n8n not accessible from internet

**Solutions**:

- Check firewall rules: `sudo ufw allow 5678`
- If using Nginx, ensure it's running: `sudo systemctl status nginx`
- Check domain DNS settings point to your server IP

#### ❌ 401 Unauthorized Error

**Solutions**:

- Verify the auth token matches in both n8n and `.env`
- Check the Authorization header format: `Bearer your-token`
- Ensure the token has no extra spaces or quotes

---

## 🎉 Congratulations!

You've successfully set up an automated email signature sending system using n8n!

### Next Steps:

- [ ] Set up monitoring/alerts for failed executions
- [ ] Add rate limiting to prevent abuse
- [ ] Create backup workflows
- [ ] Customize email templates
- [ ] Add email tracking/analytics

### Useful n8n Resources:

- [n8n Documentation](https://docs.n8n.io/)
- [n8n Community Forum](https://community.n8n.io/)
- [n8n YouTube Channel](https://www.youtube.com/c/n8n-io)
- [n8n Templates](https://n8n.io/workflows)

### Security Best Practices:

- ✅ Always use HTTPS (SSL/TLS)
- ✅ Use strong authentication tokens
- ✅ Keep n8n updated to latest version
- ✅ Regularly rotate API keys and passwords
- ✅ Monitor execution logs for suspicious activity
- ✅ Never commit `.env` files to version control

---

**Need Help?** Check the n8n execution logs and browser console for detailed error messages.
