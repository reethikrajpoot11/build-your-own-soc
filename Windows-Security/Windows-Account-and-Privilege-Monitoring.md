# Windows Account and Privilege Monitoring

## 1. Objective

The objective of this investigation was to monitor Windows account management activities, account lockouts, and privileged logon sessions using Windows Security Event Logs and Splunk.

## 2. Event IDs Investigated

| Event ID | Description |
|---|---|
| 4720 | A user account was created |
| 4726 | A user account was deleted |
| 4740 | A user account was locked out |
| 4672 | Special privileges were assigned to a new logon session |

## 3. Event ID 4720 – User Account Created

### Practical Investigation

Created a test account named `SOC_TestUser` using Windows Command Prompt.

Command used:

`net user SOC_TestUser Test@12345 /add`

### Event Viewer Findings

- Subject Account: `ritik`
- Target Account: `SOC_TestUser`

The Subject identifies the account that performed the action. The Target identifies the account that was created.

### Splunk Investigation

Search:

`index=* sourcetype="WinEventLog:Security" EventCode=4720`

Used Splunk table commands to examine the event timestamp and account-related fields.

## 4. Event ID 4726 – User Account Deleted

### Practical Investigation

Deleted the test account `SOC_TestUser` using Command Prompt.

### Event Viewer Findings

- Subject Account: `ritik`
- Target Account: `SOC_TestUser`

This event records which account performed the deletion and which account was deleted.

### Splunk Investigation

Search:

`index=* sourcetype="WinEventLog:Security" EventCode=4726`

Found one matching event and examined its timestamp, EventCode, and Account_Name fields.

## 5. Event ID 4740 – User Account Locked Out

### Practical Investigation

Created a separate local test account named `ritik1`.

Checked the Windows account lockout policy:

- Lockout Threshold: 10 attempts
- Lockout Duration: 10 minutes
- Lockout Observation Window: 10 minutes

Entered an incorrect password ten times for the test account, triggering an account lockout.

### Event Viewer Findings

- Locked Account: `ritik1`
- Caller Computer Name: `RAJPOOT`
- Subject Account: `RAJPOOT$`

The `$` suffix identifies a computer account.

### SOC Analyst Perspective

An account lockout can result from repeated incorrect passwords, brute-force attempts, password spraying, or legitimate user mistakes.

A lockout alone does not confirm an attack. Further investigation is required.

## 6. Event ID 4672 – Special Privileges Assigned

### Practical Investigation

Investigated Event ID 4672 in Windows Security logs.

### Event Viewer Findings

Two different account examples were examined:

**SYSTEM account**

The event contained privileges such as:

- SeDebugPrivilege
- SeBackupPrivilege
- SeRestorePrivilege
- SeTakeOwnershipPrivilege
- SeLoadDriverPrivilege

**Administrator account**

The account `ritikbhanot141@gmail.com` also received special privileges.

Checked Windows account settings and confirmed that this account has Administrator status.

### SOC Analyst Perspective

Event ID 4672 is not automatically suspicious. SYSTEM and administrator accounts commonly receive special privileges.

Analysts should investigate unexpected privileged logons and verify whether the account is authorized.

## 7. Splunk Investigation

Investigated all four Event IDs using Splunk Enterprise.

The searches used the Windows Security event sourcetype:

`WinEventLog:Security`

Created tables to examine available event fields and timestamps.

## 8. Learning Outcomes

Through this practical investigation, I learned:

- How to identify Windows account creation and deletion events.
- How to investigate account lockouts.
- How to understand Subject and Target account information.
- How to identify privileged logon sessions.
- How to investigate Windows Security events using Splunk.
- Why security events must be interpreted in context rather than automatically treated as attacks.

## 9. Conclusion

This investigation demonstrated how Windows Security logs can help SOC analysts monitor account management, detect account lockouts, and investigate privileged access.

Event IDs 4720, 4726, 4740, and 4672 provide useful security information when combined with proper investigation and analysis.
