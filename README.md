# 0x19-postmortem

Sure, here's a postmortem for a fictional issue with the Spy-cam project:

## Issue Summary

**Duration**: The outage occurred from 2:00 AM to 6:30 AM UTC on May 14, 2024.

**Impact**: The Spy-cam video streaming service was completely down during this period. All users were unable to access live video feeds or recorded footage. Approximately 80% of our user base was affected.

**Root Cause**: A configuration change to the primary database server caused it to run out of disk space, leading to a cascading failure of the entire system.

## Timeline

- `2:00 AM` - A scheduled database maintenance job overwrote a critical configuration file, causing the database to start consuming disk space at an alarming rate.
- `2:30 AM` - A monitoring alert was triggered for high disk usage on the primary database server.
- `3:00 AM` - An on-call engineer investigated the alert and noticed the rapidly decreasing disk space but was unable to identify the root cause.
- `3:30 AM` - The primary database server ran out of disk space and became unresponsive, causing a complete outage of the Spy-cam service.
- `4:00 AM` - The incident was escalated to the database team, who began investigating the issue.
- `4:30 AM` - The team assumed it was a hardware failure and attempted to fail over to the secondary database server, but the failover process hung due to the primary server being unresponsive.
- `5:00 AM` - The team realized it was a configuration issue and reverted the changes made by the maintenance job.
- `5:30 AM` - The primary database server was brought back online, and services began recovering.
- `6:30 AM` - The Spy-cam service was fully restored and operational.

## Root Cause and Resolution

The root cause of the issue was a scheduled database maintenance job that overwrote a critical configuration file responsible for managing disk space usage. This caused the database to start consuming disk space at an alarming rate until it completely filled up the available disk space, rendering the primary database server unresponsive.

To resolve the issue, the team reverted the configuration changes made by the maintenance job, allowing the database to release the consumed disk space and return to normal operation.

## Corrective and Preventative Measures

**Areas for Improvement**:
- Better monitoring and alerting for critical configuration changes.
- Improved failover and recovery procedures for database servers.
- More robust testing of maintenance jobs before deployment.

**Tasks**:
- Implement file integrity monitoring for critical configuration files.
- Add disk space usage monitoring with stricter thresholds and better alerting.
- Review and update the database failover and recovery procedures.
- Implement a comprehensive testing framework for database maintenance jobs.
- Add manual approval steps for maintenance jobs that modify critical configurations.

Overall, this incident highlighted the need for better monitoring, testing, and failover procedures, especially for critical components like the database servers. By addressing these areas, we can improve the reliability and resilience of the Spy-cam service.
