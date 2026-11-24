# Windows Account Creation Monitoring

## 1. Objective
Monitor Windows user account creation events using Windows Event Viewer and Splunk.

## 2. Event ID 4720 – A User Account Was Created

Event ID 4720 is generated when a new user account is created in Windows.

### Practical Lab

Created a test Windows account using Command Prompt (Run as Administrator):

```cmd
net user SOC_TestUser Test@12345 /add
```

**Result:** The command successfully created the test account.

> Note: The password was created specifically for this lab. Never reuse lab passwords for real accounts.

## 3. Event Viewer Investigation

Navigated to:

`Event Viewer → Windows Logs → Security`

Filtered the Security log using Event ID:

`4720`

### Important Event Details

| Field | Value |
|---|---|
| Event ID | 4720 |
| Subject Account | ritik |
| Target Account | SOC_TestUser |
| Subject Domain | RAJPOOT |
| Target Domain | Rajpoot |

### Understanding Subject and Target

- **Subject:** The account that performed the action.
- **Target:** The account affected by the action.

In this event:
- `ritik` created the account.
- `SOC_TestUser` was the newly created account.

## 4. Splunk Investigation
