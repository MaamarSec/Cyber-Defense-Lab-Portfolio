# 08 - Detection Engineering & Alerting

This folder turns the searches built in [07-splunk-siem](../07-splunk-siem/) into scheduled Splunk alerts, with each detection documented: the logic, the alert settings as stored, the test that proved it fires, and the problems found while tuning it.

## Detection library

| ID | Detection | Event ID | MITRE ATT&CK | Status | Documentation |
|---|---|---|---|---|---|
| DET-001 | New user account created | 4720 | T1136 | Live | [DET-001](DET-001-new-account-created.md) |
| DET-002 | Excessive failed logons | 4625 | T1110.001 | Live | [DET-002](DET-002-excessive-failed-logons.md) |
| DET-003 | Account deleted | 4726 | T1531 | Live | [DET-003](DET-003-account-deleted.md) |

An authentication dashboard is also planned.

## Conventions

- **Naming:** DET-### followed by a plain-language description.
- **Scheduling:** scheduled searches with overlapping time windows, since a back-to-back window misses events that are indexed late (see the tuning journal in DET-001).
- **Triggering:** per-result triggers with a throttle on the relevant field, so each new object alerts once.
- **Testing:** results are checked against the source Windows log, not only against Splunk's own output (see the tuning journal in DET-002).
- **Documentation:** every detection records its logic, its configuration as stored, the test that proved it fires, and its known gaps.

## Environment

Splunk Enterprise 10.4.3 on splunk-siem, ingesting Windows Security events from the Domain Controller DC01 through a Universal Forwarder. Alerts use the built-in Triggered Alerts action, since the lab has no mail or webhook infrastructure. The Splunk Enterprise trial licence on this instance expires on Nov 11, 2026. Splunk Free does not include alerting, so the alerts run only while the trial is valid, and the SPL remains portable.

Related: [investigations/](../investigations/) holds worked investigations of alerts from these detections.
