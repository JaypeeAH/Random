# Test Script: Power Automate & SharePoint 2-Level Document Approval Process

**Project:** SOP Repository – 2-Level Document Approval Workflow  
**Platform:** Power Automate + SharePoint + Microsoft Teams + Outlook  
**Date:** 2026-04-01 12:21:18  
**Prepared by:** QA Team

---

## Scope

This test script covers the end-to-end validation of the 2-level document approval workflow integrated with SharePoint (SOP Repository document library), Power Automate, Microsoft Teams Approvals, and Outlook.

---

## Prerequisites

| Item | Details |
|------|---------|
| SharePoint Site | SOP Repository document library is accessible |
| Approver Configuration List | `approver_configuration` list is populated with Level 1 (all must approve) and Level 2 (Knowledge Assistant – anyone approves) approvers |
| Power Automate Flow | Deployed and turned ON |
| Test Users | Submitter, Level 1 Approver(s), Level 2 Knowledge Assistant Approver(s) |
| Teams & Outlook | All test users have access to Microsoft Teams and Outlook |

---

## Test Cases

---

### TC-001: Upload Document – Major Check-In (Auto-Start Approval)

**Objective:** Verify that uploading and performing a Major Check-In automatically triggers the approval workflow.

| Step | Action | Expected Result | Pass/Fail | Notes |
|------|--------|----------------|-----------|-------|
| 1 | Log in as Submitter | Successfully logged in | | |
| 2 | Navigate to the SOP Repository document library | Library is visible | | |
| 3 | Upload a Word (.docx), PowerPoint (.pptx), or Excel (.xlsx) document | Document appears in the library as checked out | | |
| 4 | Right-click the document > Check In | Check-In dialog appears | | |
| 5 | Select **Major Version** and add a comment, then click OK | Document is checked in as a major version | | |
| 6 | Verify Power Automate flow is triggered | Flow run appears in Power Automate run history | | |
| 7 | Verify Level 1 approvers receive a Teams Approval notification | All Level 1 approvers receive a Teams Approval card | | |
| 8 | Verify Level 1 approvers receive an Outlook approval email | All Level 1 approvers receive an approval email | | |

---

### TC-002: Upload Document – Minor Check-In (Manual Check-In Required)

**Objective:** Verify that a Minor Check-In requires the user to click the Check-In button to trigger the approval workflow.

| Step | Action | Expected Result | Pass/Fail | Notes |
|------|--------|----------------|-----------|-------|
| 1 | Log in as Submitter | Successfully logged in | | |
| 2 | Upload a document to the SOP Repository library | Document appears as checked out | | |
| 3 | Observe – do NOT manually check in yet | No approval workflow triggered | | |
| 4 | Click the **Check In** button on the document | Check-In dialog appears | | |
| 5 | Select **Minor Version** and click OK | Document is checked in as a minor version | | |
| 6 | Verify the approval workflow is triggered | Flow run appears in Power Automate run history | | |

---

### TC-003: Level 1 Approval – All Approvers Must Approve (via Teams)

**Objective:** Verify that ALL Level 1 approvers must approve via Teams before proceeding to Level 2.

| Step | Action | Expected Result | Pass/Fail | Notes |
|------|--------|----------------|-----------|-------|
| 1 | Trigger workflow (refer TC-001 or TC-002) | Level 1 approvers receive Teams Approval notification | | |
| 2 | Log in as Level 1 Approver 1 in Teams | Approval card is visible in Teams Approvals | | |
| 3 | Approve the document in Teams | Approval recorded for Approver 1 | | |
| 4 | Log in as Level 1 Approver 2 (if multiple) | Approval card still pending | | |
| 5 | Approve as Level 1 Approver 2 | Approval recorded | | |
| 6 | Repeat for all remaining Level 1 approvers | All approvals recorded | | |
| 7 | Verify Level 2 (Knowledge Assistant) approval request is triggered ONLY after ALL Level 1 approvers have approved | Level 2 approvers receive Teams & Outlook notifications | | |

---

### TC-004: Level 1 Approval – All Approvers Must Approve (via Outlook)

**Objective:** Verify that Level 1 approvers can approve via Outlook email.

| Step | Action | Expected Result | Pass/Fail | Notes |
|------|--------|----------------|-----------|-------|
| 1 | Trigger workflow | Level 1 approvers receive Outlook approval email | | |
| 2 | Open approval email in Outlook as Level 1 Approver | Approve/Reject options are visible | | |
| 3 | Click **Approve** in the email | Approval is recorded | | |
| 4 | Verify all Level 1 approvers have approved | Level 2 is triggered after all approvals | | |

---

### TC-005: Level 2 Approval – Knowledge Assistant (Anyone Can Approve) via Teams

**Objective:** Verify that any one Knowledge Assistant approver can approve at Level 2 via Teams.

| Step | Action | Expected Result | Pass/Fail | Notes |
|------|--------|----------------|-----------|-------|
| 1 | Complete all Level 1 approvals | Level 2 approval is triggered | | |
| 2 | Verify all Knowledge Assistant approvers receive a Teams notification | All listed KA approvers receive the Teams Approval card | | |
| 3 | Log in as any one Knowledge Assistant approver | Approval card is visible | | |
| 4 | Approve the document | Approval is recorded and workflow proceeds | | |
| 5 | Verify no further approvals are required from other KA approvers | Workflow completes without requiring other KA approvers | | |

---

### TC-006: Level 2 Approval – Knowledge Assistant (Anyone Can Approve) via Outlook

**Objective:** Verify Level 2 KA approver can approve via Outlook.

| Step | Action | Expected Result | Pass/Fail | Notes |
|------|--------|----------------|-----------|-------|
| 1 | Complete all Level 1 approvals | Level 2 KA approvers receive Outlook email | | |
| 2 | Open approval email in Outlook as a KA approver | Approve/Reject options visible | | |
| 3 | Click **Approve** | Approval recorded, workflow completes | | |

---

### TC-007: Level 1 Rejection – Submitter Notification

**Objective:** Verify the submitter receives an email AND a Teams message when a Level 1 approver rejects.

| Step | Action | Expected Result | Pass/Fail | Notes |
|------|--------|----------------|-----------|-------|
| 1 | Trigger approval workflow | Level 1 approvers receive notification | | |
| 2 | Log in as a Level 1 approver | Approval card visible | | |
| 3 | Click **Reject** (Teams or Outlook) and add a rejection reason | Rejection recorded | | |
| 4 | Log in as Submitter and check email | Rejection email received from workflow bot with rejection reason | | |
| 5 | Check Submitter's Teams messages | Teams message received from workflow bot with rejection details | | |

---

### TC-008: Level 2 Rejection – Submitter Notification

**Objective:** Verify the submitter receives an email AND a Teams message when a Level 2 KA approver rejects.

| Step | Action | Expected Result | Pass/Fail | Notes |
|------|--------|----------------|-----------|-------|
| 1 | Complete all Level 1 approvals | Level 2 KA notification triggered | | |
| 2 | Log in as a KA approver | Approval card visible | | |
| 3 | Click **Reject** and add a rejection reason | Rejection recorded | | |
| 4 | Log in as Submitter and check email | Rejection email received from workflow bot | | |
| 5 | Check Submitter's Teams messages | Teams message received from workflow bot | | |

---

### TC-009: Full Approval – Submitter Notification

**Objective:** Verify the submitter receives an email AND a Teams message when the document is fully approved.

| Step | Action | Expected Result | Pass/Fail | Notes |
|------|--------|----------------|-----------|-------|
| 1 | Complete all Level 1 approvals | Level 2 triggered | | |
| 2 | Complete Level 2 KA approval | Workflow marks document as approved | | |
| 3 | Log in as Submitter and check email | Approval confirmation email received from workflow bot | | |
| 4 | Check Submitter's Teams messages | Teams approval confirmation message received from workflow bot | | |

---

### TC-010: Approver Configuration List Validation

**Objective:** Verify the workflow correctly reads approvers from the `approver_configuration` SharePoint list.

| Step | Action | Expected Result | Pass/Fail | Notes |
|------|--------|----------------|-----------|-------|
| 1 | Open the `approver_configuration` SharePoint list | List shows Level 1 and Level 2 (KA) approvers | | |
| 2 | Trigger a new approval workflow | Only users listed in `approver_configuration` receive approval requests | | |
| 3 | Add a new Level 1 approver to the list | New approver receives approval request on next workflow run | | |
| 4 | Remove a Level 1 approver from the list | Removed approver does NOT receive request on next workflow run | | |

---

### TC-011: Unsupported File Type Upload

**Objective:** Verify behavior when an unsupported file type is uploaded (e.g., PDF, ZIP).

| Step | Action | Expected Result | Pass/Fail | Notes |
|------|--------|----------------|-----------|-------|
| 1 | Upload a file with an unsupported extension (e.g., .pdf, .zip) | Document uploads to library | | |
| 2 | Check in the document | Verify whether the workflow triggers or handles it gracefully (per business rule) | | |

---

### TC-012: Concurrent Document Submissions

**Objective:** Verify the workflow handles multiple simultaneous document submissions without conflict.

| Step | Action | Expected Result | Pass/Fail | Notes |
|------|--------|----------------|-----------|-------|
| 1 | Upload and check in 3 documents simultaneously from different submitters | All 3 workflows are triggered independently | | |
| 2 | Approve/Reject each independently | Each workflow completes independently without cross-contamination | | |

---

## Test Sign-Off

| Role | Name | Signature | Date |
|------|------|-----------|------|
| QA Lead | | | |
| Business Owner | | | |
| IT / Flow Owner | | | |

---

*End of Test Script*