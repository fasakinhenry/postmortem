**Incident Summary**

Between 10:00 UTC and 12:30 UTC on 2024-09-18, approximately 85% of Consolve users encountered service disruptions, including slow response times, failed login attempts, and errors while attempting to connect with service providers. The incident was triggered by high traffic on Consolve’s launch day, overwhelming the backend infrastructure. The root cause was database connection pool exhaustion, preventing the app from scaling effectively under load. The severity of the incident was classified as high, and the impact lasted for 2 hours and 30 minutes.

The event was detected by automated monitoring systems, which alerted the engineering team. Immediate actions were taken to restore service by scaling infrastructure and optimizing database performance. During the outage, over 150 support tickets were submitted, along with a spike in social media mentions.

---

**Leadup**

On 2024-09-18 at 09:45 UTC, Consolve officially launched. The team had anticipated increased traffic but underestimated the volume of concurrent users. The backend infrastructure was scaled based on pre-launch projections but was not stress-tested to match the traffic levels encountered.

At 10:00 UTC, over 10,000 requests per minute were sent to the backend, which triggered an overload in the system, leading to database connection pool exhaustion and service degradation. Initial attempts to handle the traffic increase failed, as the server was unable to allocate enough resources in time to accommodate the spike.

---

**Fault**

The backend connection pool was configured with a limit too low to handle the surge in requests, causing errors when attempting to establish new database connections. The web app returned 503 errors to users trying to log in or interact with service providers. This continued for approximately 2 hours until corrective action was taken. The lack of real-time monitoring of database performance metrics contributed to the delay in identifying the connection pool issue.

---

**Impact**

For 2 hours and 30 minutes between 10:00 UTC and 12:30 UTC on 2024-09-18, Consolve users experienced widespread disruption. 85% of all users (approximately 30,000) were unable to access key services, resulting in failed logins, slow page loads, and connection errors when attempting to interact with service providers. During this time, over 150 support tickets were submitted, and the issue was widely reported on social media, resulting in over 300 mentions of the outage.

---

**Detection**

The incident was detected at 10:05 UTC when the automated monitoring system triggered alerts for high latency and failed requests. The alert was sent to the on-call engineering team, who immediately began investigating the cause. However, there was a delay of 20 minutes in identifying the root cause due to insufficient real-time monitoring for database connection limits. To improve future detection, enhanced database monitoring with more granular alerts will be implemented.

---

**Response**

The on-call engineer received the alert at 10:05 UTC and started investigating by checking the server logs and application performance. The initial assumption was that the application servers were underperforming, and actions were taken to increase their capacity. At 10:45 UTC, the incident was escalated to the database administration team after noticing a bottleneck in connection handling. By 11:30 UTC, the database connection pool size was increased, and additional read replicas were provisioned to distribute the load. Service was fully restored by 12:30 UTC.

---

**Recovery**

The service was restored by increasing the database connection pool size and adding more read replicas to offload the demand from the primary database instance. Additionally, auto-scaling was configured for the backend servers to dynamically adjust capacity during traffic spikes. Database performance was continuously monitored, and by 12:30 UTC, all users were able to access the platform without issues. To reduce recovery time in the future, stress tests and automated scaling processes will be improved.

---

**Timeline**

- 10:00 UTC - Consolve launched; initial surge of traffic begins.
- 10:05 UTC - Automated monitoring system alerts for high latency and failed requests.
- 10:15 UTC - Initial investigation begins, assuming server performance issues.
- 10:45 UTC - Escalation to database team due to connection pool exhaustion.
- 11:30 UTC - Database connection pool increased; read replicas added.
- 12:30 UTC - Full recovery; system restored, traffic normalized.

---

**Root Cause Identification: The Five Whys**

1. The Consolve app had an outage because the database connection pool was exhausted.
2. The database connection pool was exhausted because the traffic exceeded pre-launch projections.
3. The traffic exceeded projections because the app was not adequately stress-tested for high user volumes.
4. The app was not stress-tested because the team underestimated peak traffic and relied on outdated traffic models.
5. Traffic models were outdated because real-time user behavior during launch was not incorporated into the projections.

---

**Root Cause**

The root cause of the incident was an under-configured database connection pool, combined with insufficient load-testing prior to launch. The app was unable to handle the number of concurrent requests, leading to degraded performance and eventual service unavailability.

---

**Backlog Check**

A review of the backlog indicated that while there were discussions around scaling, stress tests for the database connection pool size were not prioritized. Load testing and stress simulations were suggested but deprioritized due to time constraints leading up to launch.

---

**Recurrence**

This issue has not been previously observed at this scale, though smaller incidents related to connection pool limits have been logged in the past (INC-0021, INC-0087). The lack of proactive scaling led to this recurrence on a larger scale during launch day.

---

**Lessons Learned**

- Improved load testing is necessary to better anticipate user behavior under peak conditions.
- Database connection pool settings should be dynamically adjusted based on traffic.
- Real-time monitoring for database performance metrics would have reduced detection time.
- Stress testing for peak traffic should be scheduled ahead of major launches.

---

**Corrective Actions**

- Increase the default size of the database connection pool and enable auto-scaling for traffic spikes.
- Add real-time database performance monitoring with more granular alerts to detect future bottlenecks.
- Conduct full-scale load testing ahead of any major releases or launches.
- Review and update traffic projections regularly, especially in the lead-up to launches.
  
**Owners**: Backend Team and DevOps  
**Due Date**: 2024-09-30
