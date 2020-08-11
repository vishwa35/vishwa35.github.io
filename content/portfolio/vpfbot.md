---
title: "@vpfbot"
date: 2018-06-06T01:03:29-07:00
draft: false
description: Slackbot built to streamline processes I encountered as Vice President of Finance for gtakpsi
projTags: [slackbot, python]
link: https://github.com/vishwa35/vpfbot
---


- Streamlined some of my processes as Vice President of Finance for Alpha Kappa Psi by building a custom slackbot that reads from the extensive Google Sheets maintaining our financial information and logging for sponsorship efforts to deliver periodic updates on the status of the organization

[//]: <> (- Added support for notifications triggered on external events such as Google Form submissions, alert emails, budget shifts, etc. - Resolved common financial questions by adding an interactive layer to respond to trigger words in the workspace)


### Scheduled Messages
---

##### constructing a weekly update message based on a Google Sheet

CSPON Updates: [a week ago] - [yesterday]

**Sales Closed** - _HELL YEA! Congrats!_
- Company | @director | Date

**Wins** - _YAY! Good news :) Remember to see these all the way through!_
- Company | @director | Date

**Losses** - _It happens. Please remember to fill out insights from this contact in the sheet. Onwards!_
- Company | @director | Date

**In Progress** - _Company | @director | Last Contacted Date_ - _Good work. Remember to keep following up._
> Only those overdue for followup (5 days) are listed here. See the sheet for details

- Company | @director | Date

Total in progress emails: XX

**Calls Scheduled** - _Company | @director | Date_ - _Good Luck!_

- Company | @director | Date

Total calls scheduled: XX

##### weekly updates on our fund status

###### [TODO] add special projects fund status

Raza-Dhanani Fund Updates: [a week ago] - [yesterday]

Since last week: +/-X% | +/-$XX.XX

**Cash Value**: $XXX.XX

**Stock Value**: $XXX.XX

**Total Account Value**: $XXX.XX

See the pinned sheet for details!

### Externally Triggered Messages
---

###### [TODO] for new applications for special projects funding

### Internally Triggered Messages
---

###### [TODO] @vpf budget
Returns a link to the current budget

###### [TODO] @vpf dues
Responds in DM with how much your current A/R is based on chapterspot (feasible?)

###### [TODO] @vpf venmo request @handle
Adds row to venmo request sheet with handle and name