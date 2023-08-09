# Web Stack Outage Postmortem: Service Disruption on August 8, 2023

## Issue Summary

**Duration:** August 8, 2023, 09:00 AM - 11:30 AM (UTC-4)
**Impact:** The user authentication service experienced intermittent downtime during the specified duration. Users attempting to log in or register encountered delays and failed login attempts. Approximately 20% of users were affected.

**Root Cause:** A database connection pool overflow led to a bottleneck in the user authentication process.

## Timeline

- **09:00 AM:** The issue was detected when an engineer noticed an unusual increase in failed login attempts.
- **09:10 AM:** Monitoring alerts indicated a rise in response time for the authentication service.
- **09:20 AM:** Investigation began, focusing on backend servers and network latency.
- **09:45 AM:** Initial assumption: Network congestion might be causing the delays.
- **10:00 AM:** Further investigation revealed a spike in database connections.
- **10:15 AM:** Assumption: Database performance degradation might be causing the delays.
- **10:30 AM:** Debugging paths taken: Tweaking database configurations to handle more connections.
- **10:45 AM:** No significant improvement observed, and investigation shifted towards database query optimization.
- **11:00 AM:** Incident escalated to the database administration team.
- **11:15 AM:** Database administrators identified the connection pool overflow as the root cause.
- **11:30 AM:** The incident was resolved by increasing the connection pool size and optimizing query execution.

## Root Cause and Resolution

**Root Cause:** The connection pool for the database had a predefined limit that was exceeded due to sudden high user activity. As a result, new connection requests were being delayed, impacting the authentication process.

**Resolution:** The connection pool size was increased to accommodate higher traffic and prevent overflow. Additionally, database queries were optimized to reduce the load on the database server.

## Corrective and Preventative Measures

**Improvements/Fixes:**
- Implement automated monitoring for connection pool usage to detect overflows.
- Establish better communication channels between the engineering and database teams for quicker issue resolution.
- Implement rate limiting on the authentication service to prevent sudden spikes in user activity.

**Tasks to Address the Issue:**
1. **Database Optimization:** Identify and optimize slow-performing queries to reduce database load.
2. **Horizontal Scaling:** Evaluate the feasibility of horizontal scaling for the authentication service to distribute traffic effectively.
3. **Alerting Mechanism:** Set up proactive alerts for connection pool usage nearing predefined limits.
4. **Documentation Update:** Enhance documentation on connection pooling best practices to prevent similar incidents.
5. **User Communication Plan:** Develop a communication strategy to inform users about service disruptions and expected resolutions.

In conclusion, the service disruption on August 8, 2023, was caused by a database connection pool overflow, leading to delays in user authentication. The issue was promptly resolved by increasing the connection pool size and optimizing database queries. To prevent future occurrences, we will implement monitoring, optimize queries, and establish better collaboration between teams. This incident underscores the importance of proactive monitoring and continuous improvement in maintaining a reliable web service.

