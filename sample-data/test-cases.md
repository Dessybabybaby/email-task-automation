#Test Cases - Email-to-Task Automation

## Test Case 1: Normal Priority Email
**Input:**
- Subject: "Password reset request"
- From: user@company.com
- Body: "Please reset my password"

**Expected Output:**
- Notion task created with Priority: Medium
- Email archived
- No Slack alert

**Status:**  PASS

---

## Test Case 2: Urgent Email
**Input:**
- Subject: "[URGENT] Server down"
- From: admin@company.com
- Body: "Production server not responding"

**Expected Output:**
- Notion task created with Priority: High
- Email archived
- No Slack alert

**Status:**  PASS

---

## Test Case 3: Email with HTML Body
**Input:**
- Subject: "Feature request"
- From: product@company.com
- Body: HTML formatted email with <tags>

**Expected Output:**
- Notion task created with clean text (HTML stripped)
- Priority: Medium
- Email archived

**Status:**  PASS

---

## Test Case 4: Notion API Failure
**Input:**
- Subject: "Test email"
- From: test@company.com
- Notion API unavailable (simulate by invalid database ID)

**Expected Output:**
- Workflow continues (Continue on Fail enabled)
- Slack alert sent with error details
- Email NOT archived

**Status:**  PASS

---

## Test Case 5: Empty Email Body
**Input:**
- Subject: "Subject only"
- From: user@company.com
- Body: (empty)

**Expected Output:**
- Notion task created with Description: "No content"
- Email archived

**Status:**  PASS
