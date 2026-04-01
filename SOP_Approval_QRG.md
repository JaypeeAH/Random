# Quick Reference Guide (QRG): SOP Document Approval Workflow

**Project:** SOP Repository – 2-Level Document Approval
**Platform:** SharePoint + Power Automate + Microsoft Teams + Outlook
**Date:** 2026-03-31

---

## Workflow Overview

```
[Submitter uploads document to SOP Repository]
              |
              v
    [Check In document]
     Major: Auto-triggers    Minor: Click Check-In button
              |
              v
  [LEVEL 1 APPROVAL – All approvers must approve]
    (via Microsoft Teams Approvals OR Outlook)
              |
         All Approved?
        /            \
      NO              YES
       |               |
  [REJECTED]           v
       |     [LEVEL 2 APPROVAL – Knowledge Assistant]
       |       (Anyone in KA team can approve)
       |              |
       |         Approved/Rejected?
       |        /              \
       |      NO               YES
       |       |                |
       v       v                v
[Submitter receives Email + Teams message from Workflow Bot]
```

---

## Role-Based Quick Steps

---

### 🟦 SUBMITTER

#### Step 1 – Upload Your Document
1. Go to the **SOP Repository** document library in SharePoint.
2. Click **Upload > Files** and select your Word (.docx), PowerPoint (.pptx), or Excel (.xlsx) file.
3. The document will appear as **Checked Out** to you.

#### Step 2 – Check In the Document

**Major Version (auto-triggers approval):**
1. Right-click the document > **Check In**.
2. Select **Major Version (Publish)**.
3. Add a version comment (optional) > Click **OK**.
4. ✅ The approval workflow starts automatically.

**Minor Version (manual trigger):**
1. Click the **Check In** button on the document toolbar.
2. Select **Minor Version**.
3. Click **OK**.
4. ✅ The approval workflow starts.

#### Step 3 – Wait for Notifications
You will receive a **Teams message** and **email** from the Workflow Bot when:
- ✅ Your document is **fully approved**
- ❌ Your document is **rejected** at any level (with rejection reason)

---

### 🟩 LEVEL 1 APPROVER

> ⚠️ **ALL Level 1 approvers must approve** before the document moves to Level 2.

#### Option A – Approve via Microsoft Teams
1. Open **Microsoft Teams**.
2. Go to **Approvals** app (left sidebar) or check your **Activity** feed.
3. Find the pending approval request for the document.
4. Review the document details.
5. Click **Approve** or **Reject**.
   - If rejecting, enter a **reason** in the comments field.
6. Click **Confirm**.

#### Option B – Approve via Outlook
1. Open your **Outlook** inbox.
2. Find the approval email from the Workflow Bot.
3. Click **Approve** or **Reject** directly in the email.
   - If rejecting, enter a reason when prompted.
4. Confirm your response.

> 📌 **Note:** The document will NOT proceed to Level 2 until ALL Level 1 approvers have responded.

---

### 🟨 LEVEL 2 APPROVER (Knowledge Assistant Team)

> ✅ **Anyone** on the Knowledge Assistant team can approve – only one approval needed.

#### Option A – Approve via Microsoft Teams
1. Open **Microsoft Teams**.
2. Go to the **Approvals** app or check your **Activity** feed.
3. Find the pending Level 2 approval request.
4. Review the document.
5. Click **Approve** or **Reject** (with reason if rejecting).
6. Click **Confirm**.

#### Option B – Approve via Outlook
1. Open your **Outlook** inbox.
2. Find the Level 2 approval email from the Workflow Bot.
3. Click **Approve** or **Reject**.
4. Confirm your response.

> 📌 **Note:** Once one KA member approves, the workflow completes and the submitter is notified.

---

## Notification Summary

| Event | Who Gets Notified | How |
|-------|------------------|-----|
| Document checked in | Level 1 Approvers | Teams Approval + Outlook Email |
| All Level 1 approved | Level 2 KA Approvers | Teams Approval + Outlook Email |
| Level 1 rejected | Submitter | Email + Teams message from Workflow Bot |
| Level 2 rejected | Submitter | Email + Teams message from Workflow Bot |
| Fully approved | Submitter | Email + Teams message from Workflow Bot |

---

## Approver Configuration (Admin Reference)

Approvers are managed in the **`approver_configuration`** SharePoint list.

| Column | Description |
|--------|-------------|
| Name | Approver's display name |
| Email | Approver's email address |
| Level | `1` = Level 1 (all must approve), `2` = Level 2 KA (anyone) |
| Active | Yes/No – controls if user receives approvals |

> To add/remove approvers: Navigate to the SharePoint site > **Site Contents** > `approver_configuration` list > Edit items as needed.

---

## Troubleshooting

| Issue | What to Check |
|-------|--------------|
| No approval notification received | Check `approver_configuration` list – is the approver listed and Active = Yes? |
| Workflow not triggering after check-in | Verify the Power Automate flow is turned ON and not in error state |
| Approval card not visible in Teams | Check Teams Approvals app; try refreshing or searching Activity feed |
| Submitter not receiving notifications | Verify submitter email in SharePoint profile; check spam/junk folder |
| Workflow stuck at Level 1 | One or more Level 1 approvers have not responded yet – all must approve |

---

## Support Contacts

| Role | Contact |
|------|---------|
| IT / Flow Owner | *(Insert contact)* |
| SharePoint Admin | *(Insert contact)* |
| Knowledge Assistant Team Lead | *(Insert contact)* |

---

*End of Quick Reference Guide*