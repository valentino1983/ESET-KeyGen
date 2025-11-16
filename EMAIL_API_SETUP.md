# Email API Setup Guide

This document explains how to set up and use the different email providers with ESET-KeyGen.

## Available Email APIs

### Free/Public Email Services (No API Key Required)

1. **1secmail** - https://www.1secmail.com
   - Free temporary email service
   - REST API
   - Usage: `python main.py --key --email-api 1secmail`

2. **Guerrillamail** - https://www.guerrillamail.com
   - Free temporary email service
   - Browser-based
   - Usage: `python main.py --auto-detect-browser --key --email-api guerrillamail`

3. **Mailticking** - https://www.mailticking.com
   - Free temporary email service
   - Browser-based
   - Usage: `python main.py --auto-detect-browser --key --email-api mailticking`

4. **Fakemail** - https://www.fakemail.net
   - Free temporary email service
   - Browser-based
   - Usage: `python main.py --auto-detect-browser --key --email-api fakemail`

5. **Inboxes** - https://inboxes.com
   - Free temporary email service
   - Browser-based
   - Usage: `python main.py --auto-detect-browser --key --email-api inboxes`

6. **Incognitomail** - https://incognitomail.co
   - Free temporary email service
   - Browser-based
   - Usage: `python main.py --auto-detect-browser --key --email-api incognitomail`

7. **EmailFake** - https://emailfake.com
   - Free temporary email service
   - Browser-based
   - Usage: `python main.py --auto-detect-browser --key --email-api emailfake`

### Professional Email Testing Services (API Key Required)

These are designed for automated testing and CI/CD pipelines, offering more reliability and custom domain support.

#### MailSlurp

**Website:** https://www.mailslurp.com

**Features:**
- Powerful REST API
- Create unlimited private inboxes on demand
- Support for custom domains
- Free tier available for personal projects
- SDKs in multiple languages

**Setup:**
1. Sign up at https://www.mailslurp.com
2. Get your API key from the dashboard
3. Set the environment variable:
   ```bash
   # Windows PowerShell
   $env:MAILSLURP_API_KEY="your-api-key-here"
   
   # Windows Command Prompt
   set MAILSLURP_API_KEY=your-api-key-here
   
   # Linux/macOS
   export MAILSLURP_API_KEY="your-api-key-here"
   ```
4. Run ESET-KeyGen:
   ```bash
   python main.py --key --email-api mailslurp
   ```

#### Mailsac

**Website:** https://mailsac.com

**Features:**
- REST API for all features
- Bring Your Own Domain (BYOD) support
- SMTP capture capability
- Free plan with public inboxes
- Strong CI/CD integration

**Setup:**
1. Sign up at https://mailsac.com
2. Get your API key from the dashboard
3. Set the environment variable:
   ```bash
   # Windows PowerShell
   $env:MAILSAC_API_KEY="your-api-key-here"
   
   # Windows Command Prompt
   set MAILSAC_API_KEY=your-api-key-here
   
   # Linux/macOS
   export MAILSAC_API_KEY="your-api-key-here"
   ```
4. Run ESET-KeyGen:
   ```bash
   python main.py --key --email-api mailsac
   ```

## Troubleshooting

### Token Retrieval Error

If you encounter a "Token retrieval error" message:
1. Try a different email API provider
2. For web-based services, ensure you have Chrome installed and browser auto-detection enabled (`--auto-detect-browser`)
3. For API-based services, verify your API key is set correctly

### MailSlurp/Mailsac Not Working

- Verify the API key is set: `echo $env:MAILSLURP_API_KEY` (PowerShell) or `echo $MAILSLURP_API_KEY` (Linux/macOS)
- Check your service plan doesn't have API rate limits exceeded
- Ensure your account has remaining API credits

### ESET Website Blocking

ESET may periodically block known temporary email providers. If you encounter blocks:
1. Try switching to a different provider
2. Consider using MailSlurp or Mailsac with custom domains (BYOD feature)
3. Use a VPN with the `--use-vpn` flag (GitHub Actions only)

## Recommended Setup for CI/CD

For GitHub Actions or other CI/CD pipelines:
1. **Primary:** Use `mailslurp` with API key stored as a secret
2. **Fallback:** Use `mailsac` as a secondary option
3. **Last resort:** Use `developermail` (no API key required)

Set secrets in your GitHub repository:
- `MAILSLURP_API_KEY` for MailSlurp
- `MAILSAC_API_KEY` for Mailsac (optional)

Then use them in your workflow:
```yaml
env:
  MAILSLURP_API_KEY: ${{ secrets.MAILSLURP_API_KEY }}
  MAILSAC_API_KEY: ${{ secrets.MAILSAC_API_KEY }}
```
