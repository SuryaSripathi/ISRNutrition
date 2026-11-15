# UIUC ISR Vegetarian Micronutrient Tracker & Daily Carrier Email-to-SMS/MMS Sender

Fetches the **exact daily ISR menu** from the official backend JSON API powering [https://web.housing.illinois.edu/diningmenus](https://web.housing.illinois.edu/diningmenus), filters strictly for **Vegetarian, Vegan, and Jain** dishes using the API's `Traits` metadata, grades each dish for **Iron**, **Vitamin C**, and **Vitamin D**, and sends a daily text summary at **8:00 AM Central Time (`America/Chicago`)** directly to **native iPhone Messages (SMS/MMS)** via **Carrier Email-to-SMS/MMS Gateways** (no third-party app required on the phone, and does not use your Apple ID).

## How Carrier Email-to-SMS/MMS Works

Mobile carriers run email-to-text gateways that convert an incoming email into a native SMS/MMS text message delivered straight to the recipient's iPhone **Messages** app:

| Carrier | Shorthand in `recipients.txt` / `.env` | Gateway Domain Used |
| :--- | :--- | :--- |
| **Verizon / Visible** | `2175550101:verizon` | `2175550101@vzwpix.com` |
| **AT&T** | `2175550102:att` | `2175550102@mms.att.net` |
| **T-Mobile / Mint Mobile** | `3125550199:tmobile` | `3125550199@tmomail.net` |
| **Cricket Wireless** | `2175550104:cricket` | `2175550104@mms.cricketwireless.net` |
| **US Cellular** | `2175550105:uscellular` | `2175550105@mms.uscc.net` |
| **Google Fi** | `2175550106:googlefi` | `2175550106@msg.fi.google.com` |
| **Boost Mobile** | `2175550107:boost` | `2175550107@myboostmobile.com` |

## Setup in 2 Minutes

### 1. Create a Free Google App Password (No Apple ID Used)
1. Using any Gmail account (or a dedicated Gmail account you create for this project), go to **[myaccount.google.com/apppasswords](https://myaccount.google.com/apppasswords)**.
2. Create an App Password named `UIUC ISR Bot` and copy the 16-character code.
3. Put it in `.env` (which is ignored by `.gitignore` so it is never uploaded to GitHub):
   ```ini
   SMTP_EMAIL="your.project.bot@gmail.com"
   SMTP_APP_PASSWORD="abcd efgh ijkl mnop"
   SMS_RECIPIENTS="2175550101:verizon,2175550102:att"
   ```
   *(Or list one `phone:carrier` per line inside `recipients.txt`.)*

### 2. Send a Live Test SMS/MMS Right Now
```bash
python3 isr_nutrition.py
```
*(Or test a specific recipient on the command line: `python3 isr_nutrition.py --to 2175550101:verizon`)*

### 3. Automated Daily 8:00 AM Central Time Delivery
- **Local Antigravity Automation:** Already enabled via **Daily UIUC ISR Micronutrient Digest** (`8:00 AM America/Chicago`).
- **GitHub Actions Cloud Schedule:** Add `SMTP_EMAIL`, `SMTP_APP_PASSWORD`, and `SMS_RECIPIENTS` under your GitHub repo's **Settings → Secrets and variables → Actions**.
