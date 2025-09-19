# Troubleshooting Guide: Converting Epoch Timestamps in SQL Server

## Overview

When working with applications or logs that store timestamps in Unix epoch format, you may need to convert them into a human-readable datetime in SQL Server. This guide explains common issues, provides working solutions, and highlights pitfalls to avoid.

**Audience:** Database administrators, support engineers, and developers.  
**Skill Level:** Intermediate  

---

## Problem

You have a column storing epoch timestamps (e.g., `1694467200`) but queries return unreadable numbers instead of dates.

**Example:**

```sql
SELECT EventTimeEpoch FROM Logs;
-- Output: 1694467200
```

## Root Cause

SQL Server does not natively store or interpret Unix epoch timestamps. Conversion requires explicit handling.

---

## Solutions

### Convert Epoch to DateTime

```sql
SELECT DATEADD(SECOND, EventTimeEpoch, '1970-01-01') AS EventTime FROM Logs;
```

### Handling Milliseconds Epoch

If your data stores epoch in milliseconds:

```sql
 SELECT DATEADD(SECOND, EventTimeEpoch / 1000, '1970-01-01') AS EventTime FROM Logs;
```

---

## Common Pitfalls

* Forgetting to divide milliseconds by 1000 | results in incorrect dates.
* Not accounting for UTC vs local timezone differences.
* Using `DATETIME` instaed of `DATETIME2` | potential precision issues.

---

## Verification

Run this query to confirm conversion works:

```sql
SELECT TOP 5
  EventTimeEpoch,
  DATEADD(SECOND, EventTimeEpoch, '1970-01-01') AS ConvertedTime
FROM Logs;
```

Expected output should match known event timestamps.
