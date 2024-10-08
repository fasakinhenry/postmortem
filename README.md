# Postmortem Template Repository

This is a postmortem template inspired by atlassian for document incident reports and taking actions. It is configured to work with GitHub Pages and Jekyll, so your postmortem can be viewed as a static webpage.

## How to Use

1. Fork this repository or create a new repository from this template.
2. Create a new postmortem inside the `_posts/` folder following the naming convention `YYYY-MM-DD-title.md`.
3. Customize the template to your needs.

## Template Structure

- **_layouts/default.html**: The default layout for all postmortem pages.
- **_posts/**: Store your postmortem Markdown files here.

## View Postmortem Online

Once you push your changes, the postmortem will be available at: `https://<your-username>.github.io/<repository-name>/`


> Check out a postmortem template written for [Consolve App](https://consolve.vercel.app) here: [Postmortem Template](/postmortem-example.md)

> [!TIP]
> Just copy and make use of the template and replace the values in the curly braces with their original values


```
Incident summary
Write a summary of the incident in a few sentences. Include what happened, why, the severity of the incident and how long the impact lasted.

EXAMPLE:
Between the hour of {time range of incident, e.g. 15:45 and 16:35} on {DATE}, {NUMBER} users encountered {EVENT SYMPTOMS}. 

The event was triggered by a {CHANGE} at {TIME OF CHANGE THAT CAUSED THE EVENT}. 

The {CHANGE} contained {DESCRIPTION OF OR REASON FOR THE CHANGE, such as a change in code to update a system}. 

A bug in this code caused {DESCRIPTION OF THE PROBLEM}. 

The event was detected by {MONITORING SYSTEM}. The team started working on the event by {RESOLUTION ACTIONS TAKEN}.

This {SEVERITY LEVEL} incident affected {X%} of users.

There was further impact as noted by {e.g. NUMBER OF SUPPORT TICKETS SUBMITTED, SOCIAL MEDIA MENTIONS, CALLS TO ACCOUNT MANAGERS} were raised in relation to this incident. 

Leadup
Describe the sequence of events that led to the incident, for example, previous changes that introduced bugs that had not yet been detected.

EXAMPLE:
At {16:00} on {MM/DD/YY}, ({AMOUNT OF TIME BEFORE CUSTOMER IMPACT, e.g. 10 days before the incident in question}), a change was introduced to {PRODUCT OR SERVICE}  in order to {THE CHANGES THAT LED TO THE INCIDENT}. 

This change resulted in  {DESCRIPTION OF THE IMPACT OF THE CHANGE}.

Fault
Describe how the change that was implemented didn't work as expected. If available, attach screenshots of relevant data visualizations that illustrate the fault.

EXAMPLE:
{NUMBER} responses were sent in error to {XX%} of requests. This went on for {TIME PERIOD}.

Impact
Describe how the incident impacted internal and external users during the incident. Include how many support cases were raised.

EXAMPLE:
For {XXhrs XX minutes} between {XX:XX UTC and XX:XX UTC} on {MM/DD/YY}, {SUMMARY OF INCIDENT} our users experienced this incident.

This incident affected {XX} customers (X% OF {SYSTEM OR SERVICE} USERS), who experienced {DESCRIPTION OF SYMPTOMS}.

{XX NUMBER OF SUPPORT TICKETS AND XX NUMBER OF SOCIAL MEDIA POSTS} were submitted.

Detection
When did the team detect the incident? How did they know it was happening? How could we improve time-to-detection? Consider: How would we have cut that time by half?

EXAMPLE:
This incident was detected when the {ALERT TYPE} was triggered and {TEAM/PERSON} were paged. 

Next, {SECONDARY PERSON} was paged, because {FIRST PERSON} didn't own the service writing to the disk, delaying the response by {XX MINUTES/HOURS}.

{DESCRIBE THE IMPROVEMENT} will be set up by {TEAM OWNER OF THE IMPROVEMENT} so that {EXPECTED IMPROVEMENT}.

Response
Who responded to the incident? When did they respond, and what did they do? Note any delays or obstacles to responding.

EXAMPLE:
After receiving a page at {XX:XX UTC}, {ON-CALL ENGINEER} came online at {XX:XX UTC} in {SYSTEM WHERE INCIDENT INFO IS CAPTURED}. 

This engineer did not have a background in the {AFFECTED SYSTEM} so a second alert was sent at {XX:XX UTC} to {ESCALATIONS ON-CALL ENGINEER} into the who came into the room at {XX:XX UTC}.

Recovery
Describe how the service was restored and the incident was deemed over. Detail how the service was successfully restored and you knew how what steps you needed to take to recovery. 

Depending on the scenario, consider these questions: How could you improve time to mitigation? How could you have cut that time by half?

EXAMPLE:
We used a three-pronged approach to the recovery of the system: 

{DESCRIBE THE ACTION THAT MITIGATED THE ISSUE, WHY IT WAS TAKEN, AND THE OUTCOME} 

Example: By Increasing the size of the BuildEng EC3 ASG to increase the number of nodes available to support the workload and reduce the likelihood of scheduling on oversubscribed nodes

Disabled the Escalator autoscaler to prevent the cluster from aggressively scaling-down
Reverting the Build Engineering scheduler to the previous version.
Timeline
Detail the incident timeline. We recommend using UTC to standardize for timezones.

Include any notable lead-up events, any starts of activity, the first known impact, and escalations. Note any decisions or changed made, and when the incident ended, along with any post-impact events of note. 

EXAMPLE:
All times are UTC.

11:48 - K8S 1.9 upgrade of control plane is finished 

12:46 - Upgrade to V1.9 completed, including cluster-auto scaler and the BuildEng scheduler instance 

14:20 - Build Engineering reports a problem to the KITT Disturbed

14:27 - KITT Disturbed starts investigating failures of a specific EC2 instance (ip-203-153-8-204) 

14:42 - KITT Disturbed cordons the node 

14:49 - BuildEng reports the problem as affecting more than just one node. 86 instances of the problem show failures are more systemic 

15:00 - KITT Disturbed suggests switching to the standard scheduler 

15:34 - BuildEng reports 200 pods failed 

16:00 - BuildEng kills all failed builds with OutOfCpu reports 

16:13 - BuildEng reports the failures are consistently recurring with new builds and were not just transient. 

16:30 - KITT recognize the failures as an incident and run it as an incident. 

16:36 - KITT disable the Escalator autoscaler to prevent the autoscaler from removing compute to alleviate the problem.

16:40 - KITT confirms ASG is stable, cluster load is normal and customer impact resolved.

TEMPLATE:

XX:XX UTC - INCIDENT ACTIVITY; ACTION TAKEN

XX:XX UTC - INCIDENT ACTIVITY; ACTION TAKEN

XX:XX UTC - INCIDENT ACTIVITY; ACTION TAKEN

Root cause identification: The Five Whys
The Five Whys is a root cause identification technique. Here’s how you can use it:

Begin with a description of the impact and ask why it occurred. 
Note the impact that it had.  
Ask why this happened, and why it had the resulting impact. 
Then, continue asking “why” until you arrive at a root cause.
List the "whys" in your postmortem documentation.

EXAMPLE:
The application had an outage because the database was locked
The database locked because there were too many writes to the database
Because we pushed a change to the service and didn’t expect the elevated writes
Because we don't have a development process established for load testing changes
Because we never felt load testing was necessary until we reached this level of scale.
Root cause
Note the final root cause of the incident, the thing identified that needs to change in order to prevent this class of incident from happening again.

EXAMPLE:
A bug in connection pool handling led to leaked connections under failure conditions, combined with lack of visibility into connection state.

Backlog check
Review your engineering backlog to find out if there was any unplanned work there that could have prevented this incident, or at least reduced its impact? 

A clear-eyed assessment of the backlog can shed light on past decisions around priority and risk.

EXAMPLE:
No specific items in the backlog that could have improved this service. There is a note about improvements to flow typing, and these were ongoing tasks with workflows in place.  

There have been tickets submitted for improving integration tests but so far they haven't been successful.

Recurrence
Now that you know the root cause, can you look back and see any other incidents that could have the same root cause? If yes, note what mitigation was attempted in those incidents and ask why this incident occurred again.

EXAMPLE:
This same root cause resulted in incidents HOT-13432, HOT-14932 and HOT-19452.

Lessons learned
Discuss what went well in the incident response, what could have been improved, and where there are opportunities for improvement.

EXAMPLE:
Need a unit test to verify the rate-limiter for work has been properly maintained
Bulk operation workloads which are atypical of normal operation should be reviewed
Bulk ops should start slowly and monitored, increasing when service metrics appear nominal
Corrective actions
Describe the corrective action ordered to prevent this class of incident in the future. Note who is responsible and when they have to complete the work and where that work is being tracked.

EXAMPLE:
Manual auto-scaling rate limit put in place temporarily to limit failures
Unit test and re-introduction of job rate limiting
Introduction of a secondary mechanism to collect distributed rate information across cluster to guide scaling effects
```
