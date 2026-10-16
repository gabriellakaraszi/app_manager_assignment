# Technical Assignment: Application Manager 

### Task 1: Data Quality, Security & Onboarding Review
Analyze the provided `users.yaml` and `repositories.yaml` files, paying close attention to user statuses, assigned roles, email domains, and dates.

1. **Security & Data Quality Anomalies:** Identify at least **3 risky, inconsistent, or suspicious records** in the existing files. Briefly explain why they represent a potential security risk, operational issue, or data anomaly.
•	Users file: id 103- last active 1 year ago – check if license/access still required (since project closed status). (unnecessary cost, security issue)
•	Users file: id 104 – if the status is “inactive” why is copilot enabled?
•	(Users file: id 106 – Dev access to billing?)
•	Users file: id 109 – User is on leave, hence the access and license should be put on hold/removed
•	Users file: id 110 – Test Account? Shared account??? Should not be supported for security reasons

2. **Onboarding Decisions:** Review the following five access requests for our GitLab environment. Choose one decision for each: **`[Proceed]`**, **`[Hold for approval]`**, or **`[Reject]`**. Explain your reasoning based on the Principle of Least Privilege, domain validity, repository status, or role compliance.
   * *New User A:* Mark Kovacs (`mark.kovacs@aldi-sued.com`), Role: Developer, Repo: `payment-gateway` [Hold for approval] – ask for reasoning, why dev should access finance’s repo and ask for Finance IT’s approval with the business reasoning
   * *New User B:* Stefan Müller (`stefan.mueller@adli-seud.com`), Role: Maintainer, Repos: `auth-service`, `core-api` [Reject] – mail domain! I would include a message with the rejection: Check if it was a typo within the email address and reasoning for 2 repo accesses should be included (separate requests must be opened)
   * *New User C:* Anna Schmidt (`anna.schmidt@aldi-sued.com`), Role: Owner, Repo: `billing-system` [Hold for approval] – Owner of what? I would ask for business reasoning and then for the approval of Finance IT’s approver
   * *New User D:* Thomas Weber (`thomas.weber@aldi-sued.com`), Role: Developer, Repo: `core-api` [Hold for approval]- I would ask for business reasoning and then for the approval of Platform team’s approver
   * *New User E:* Kevin Smith (`kevin.smith@aldi-sued.com`), Role: System-Admin-All, Repo: `frontend-ui` [Proceed] – based on role
3. **Configuration Update:** For all requests where your decision is **`[Proceed]`**, format them as valid objects and append them to your final `users.yaml` list.
My questions/concerns: 
How does the current approval process work, and is it integrated into the request process?
Is business justification required when requesting access?
Who typically submits requests for new joiners: repository owners or team leaders?
Are repository descriptions detailed enough to provide the information needed for effective access management?

---

### Task 2: Operational Support & License Management

**Scenario:** It is Thursday morning at 09:15 AM. You receive several urgent MS Teams messages from team leads reporting that their developers are suddenly losing access to their AI code-assistant plugin integrated with GitLab. In their IDEs, they see the error: *"License expired or quota exceeded"*. 

You check the global billing dashboard and see that **all allocated licenses are fully used**, and there are no free seats left to assign, leaving a queue of 40+ active developers blocked from their work.

Please answer the following questions:

1. **First Steps & Troubleshooting:** What are the first **3 practical actions** you would take in your first 15 minutes to mitigate the bottleneck? 
•	Ask TLs to give me a list of DEV in priority order, who needs access
•	I would pull user info and revoke license of users, who were not active for the last 3 months (2 if needed)
•	I would start to grant access to the DEVs based on priority list and send notification to all users about the access revoke (Including the information of requesting it again and letting me know if it was not revoked but not needed anymore.). 
(I would start to mentally prepare for the feedback of those who still need the license but were on long holiday/other tasks not requiring it for a period etc.)
2. **Prioritization:** You have a long queue of developers asking for a license immediately, but you cannot purchase new ones right away due to budget approval workflows. Based on the data in `users.yaml` and `repositories.yaml`, how would you prioritize who gets a seat, or whose license could be revoked to free up space?
As mentioned above, I would revoke access of those, who were not active for the longest time and ask business assistance with prioritizing license relocations (on my own I would consider roles).
3. **Escalation & Help:** Since you are new to the team, you cannot solve a budget shortage alone. Who within a standard IT organization would you contact for help, and what specific data would you prepare for them?
I would contact my supervisor for further information, but I also assume it is something I would clarify amongst the first topics upon joining the team. I would contact the application owner and/or the person responsible for license billing and provide the numbers, all licensed user, users waiting for license, I assume the team size increased so those details would help, too.
I would also opened the discussion how to avoid these scenarios in the future. I would set up (if there is no process in place yet) a process (preferably automated) for license clean-up – revoke licenses for users, who did not use it for 1-2-3 months. Set up notification once we are near to 80-90 % of license usage and investigate ramp-up plans. -Would we need extra manual clean-up or even more licenses?
4. **User Communication:** Write a short, friendly MS Teams broadcast message (max 80 words) to the affected developers. Inform them that you are working on the issue and let them know what to do next.
Dear Team,
All plugin licenses are currently in use, so we are unable to grant new access.
If you have a license that you no longer need, or will not use for an extended period, please let me know so it can be reassigned. 
If you are waiting for a license, please share your business justification to help us prioritize requests.
We are actively working on a solution and will keep you updated.
Thanks for your patience and understanding!

