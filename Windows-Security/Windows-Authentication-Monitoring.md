# Windows Authentication Monitoring

## 1. Objective

Monitor Windows authentication activities using Windows Event Viewer and Splunk.

The objective is to identify successful and failed login attempts and understand how a SOC Analyst investigates authentication events.

## 2. Windows Authentication Event IDs

We focused on two important Windows Security Event IDs.

### Event ID 4624 – An Account Was Successfully Logged On

Event ID 4624 is generated when a user successfully logs into a Windows system.

### Event ID 4625 – An Account Failed to Log On

Event ID 4625 is generated when a login attempt fails.

These events help SOC Analysts monitor authentication activities and identify potentially suspicious login behaviour.

## 3. Event Viewer Investigation

Navigated to:

`Event Viewer → Windows Logs → Security`

Investigated the following Event IDs:

- `4624` – Successful Logon
- `4625` – Failed Logon

### Important Event Details

During the investigation, we examined:

- Account Name
- Logon Type
- Source Network Address
- Event ID
- Time of the event

### Observations

**Successful Login (4624)**

- Account Name: `Rajpoot$`
- Logon Type: `11`
- Source Network Address: `127.0.0.1`

**Failed Login (4625)**

- Account Name: `RAJPOOT$`
- Logon Type: `2`
- Source Network Address: `127.0.0.1`

The failed login event contained the message:

`An Error occurred during Logon`

## 4. Splunk Investigation

Configured Splunk Enterprise to collect Windows Security events using the Local Event Logs input.

Used the following sourcetype:

`WinEventLog:Security`

### Searching Successful Login Events

```spl
index=* sourcetype="WinEventLog:Security" EventCode=4624
```

### Searching Failed Login Events

```spl
index=* sourcetype="WinEventLog:Security" EventCode=4625
```

### Counting Successful and Failed Logins

Used the `stats` command to count authentication events.

```spl
index=* sourcetype="WinEventLog:Security" (EventCode=4624 OR EventCode=4625)
| stats count by EventCode
```

### Displaying Authentication Details

```spl
index=* sourcetype="WinEventLog:Security" EventCode=4625
| table _time Account_Name Logon_Type
```

### Monitoring Failed Login Activity Over Time

```spl
index=* sourcetype="WinEventLog:Security" EventCode=4625
| timechart span=1m count
```

### Investigation Findings

During our investigation, we observed:

- 203 successful login events.
- 1 failed login event.
- No repeated failed login attempts indicating a brute-force pattern.

## 5. SOC Login Monitoring Dashboard

Created a Splunk dashboard named:

`SOC Login Monitoring`

The dashboard included visualisations to monitor authentication activities.

### Dashboard Components

- Successful vs Failed Login Events.
- Failed Login Activity Over Time.

The dashboard helps provide a quick overview of Windows authentication activities.

## 6. SOC Analyst Perspective

A SOC Analyst should monitor both successful and failed authentication events.

Important investigation questions include:

- Which account attempted to log in?
- Was the login successful or unsuccessful?
- When did the event occur?
- What was the Logon Type?
- Where did the login attempt originate?
- Were there repeated failed login attempts?

A single failed login does not automatically indicate a brute-force attack.

In our lab, we observed only one failed login event. Therefore, there was insufficient evidence to identify a brute-force attack.

## 7. Learning Outcomes

- Learned about Windows Event ID 4624.
- Learned about Windows Event ID 4625.
- Investigated Windows Security logs using Event Viewer.
- Configured Splunk to collect Windows Security events.
- Searched for successful and failed login events.
- Practised SPL commands such as `stats`, `table` and `timechart`.
- Analysed authentication event details.
- Created a Splunk authentication monitoring dashboard.
- Learned how SOC Analysts investigate login activities.

**Status:** Windows Authentication Monitoring investigation completed.
