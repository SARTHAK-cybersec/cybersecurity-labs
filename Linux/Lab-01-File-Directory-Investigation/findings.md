# Investigation Findings — Lab 01

## Finding 01 — Authentication Activity

### Evidence

File:

```text
logs/auth.log

###Observation

The authentication log contained four login-related events.

Successful login: eminem
Failed login: unknown_user
Failed login: unknown_user
Successful login: eminem
Analysis

#The log contained:

2 successful login attempts
2 failed login attempts

The failed attempts were associated with:

unknown_user
Interpretation

The failed login attempts are security-relevant events that would require further investigation in a real environment.

However, the presence of failed login attempts alone does not establish that an attack or compromise occurred.

### Finding 02 — Suspicious File
Evidence

File:

suspicious/temp_data.txt
Observation

A non-empty file was identified inside the suspicious directory.

File Type:-
ASCII text

Content:-
unknown process data

File Size:-
21 bytes


### Analysis

The file was flagged for investigation because it was located inside a directory specifically designated as suspicious within the lab environment.

Its contents alone are not sufficient to establish malicious activity.

Finding 03 — Evidence Correlation

The authentication log and suspicious file were examined as separate pieces of evidence.



### Observed information:

Authentication events
        +
Suspicious file
        ↓
Further investigation required

There was not enough evidence in this lab to establish a relationship between the failed authentication attempts and the suspicious file.

### Final Assessment

### The investigation identified:

2 successful login events

2 failed login events

1 non-empty suspicious file


The evidence demonstrates how Linux command-line tools can be used to locate files, inspect logs, search text, and identify potentially relevant artifacts.

No conclusion of system compromise was made because the available evidence was insufficient.

### Lessons Learned

This lab helped develop the following investigation habits:

Collect evidence before reaching conclusions.

Use command-line tools to search large amounts of data.

Separate observations from assumptions.

Treat suspicious activity as something requiring investigation rather than automatically assuming compromise.

Document findings so another analyst can reproduce the investigation.
