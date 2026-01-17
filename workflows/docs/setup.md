# Setup Guide - Email-to-Task Automation

## Prerequisites Checklist

- [ ] n8n instance running (cloud or self-hosted)
- [ ] Gmail account
- [ ] Notion workspace (free tier sufficient)
- [ ] Slack workspace (optional, for error alerts)

---

## Step 1: Gmail Setup (5 minutes)

1. **Create Gmail label:**
   - Go to Gmail Settings → Labels
   - Create new label: `support-inbox`

2. **Enable Gmail API:**
   - Already handled by n8n OAuth2 flow
   - No additional configuration needed

---

## Step 2: Notion Setup (10 minutes)

1. **Create Notion Integration:**
   - Go to: https://www.notion.so/my-integrations
   - Click "+ New integration"
   - Name: `n8n Email Automation`
   - Select your workspace
   - Copy "Internal Integration Token" (save for Step 4)

2. **Create Notion Database:**
   - In Notion, create new page
   - Type `/database` → Select "Table - Inline"
   - Name: `Support Tasks`
   
3. **Add Required Columns:**
   - Title (default - rename if needed)
   - Requester (type: Text)
   - Priority (type: Select)
     - Add options: High, Medium, Low
   - Description (type: Text)
   - Status (type: Select)
     - Add options: To Do, In Progress, Done
   - Created At (type: Date)

4. **Share Database with Integration:**
   - Click "..." (top right of database)
   - "Add connections"
   - Select "n8n Email Automation"
   
5. **Copy Database ID:**
   - From URL: `https://notion.so/workspace/ABC123?v=...`
   - Database ID = `ABC123`

---

## Step 3: n8n Setup (5 minutes)

1. **Import Workflow:**
   - Download: `workflows/email-task-workflow.json`
   - n8n UI → Workflows → Import from File
   - Select downloaded file

2. **Set Gmail Credentials:**
   - Click "Gmail Trigger" node
   - Credentials dropdown → "Create New"
   - Type: OAuth2
   - Click "Connect my account"
   - Authorize Gmail access

3. **Set Notion Credentials:**
   - Click "Create Task in Notion" node
   - Credentials dropdown → "Create New"
   - Paste Integration Token from Step 2
   - Save

4. **Configure Notion Database ID:**
   - Still in "Create Task in Notion" node
   - Database ID field → Paste your database ID
   - Save
     
---

## Step 4: Slack Setup (Optional, 5 minutes)

1. **Set Slack Credentials:**
   - Click "Send Error Alert" node
   - Credentials dropdown → "Create New"
   - Type: OAuth2
   - Click "Connect my account"
   - Authorize Slack workspace

2. **Select Channel:**
   - Channel dropdown → Select #general or create #automation-alerts

---

## Step 5: Test Workflow (10 minutes)

1. **Activate Workflow:**
   - Toggle switch (top right) to "Active"

2. **Send Test Email:**
   - Email yourself
   - Subject: [URGENT] Test Email
   - Body: This is a test
   - Add label: support-inbox

3. **Wait & Verify:**
   - Wait 5 minutes (or manually trigger)
   - Check Notion database for new task
   - Verify email archived in Gmail

---

## Troubleshooting

1. **Workflow doesn't trigger:**
   - Ensure workflow is Active (toggle on)
   - Check Gmail label spelling matches exactly
   - Verify at least one email has the label

2. **Notion task creation fails:**
   - Verify database shared with integration
   - Check database ID is correct
   - Ensure all required properties exist in database

3. **Need help?**
   - Open issue: https://github.com/Dessybabybaby/email-task-automation/issues
   - DM me: https://linkedin.com/in/achusi-desmond
