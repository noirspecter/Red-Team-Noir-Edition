# Red Team: Noir Edition – Entry #001
**Title:** The Minute Root: How One Cron Job Handed Me the Keys  
**Date:** 27 March 2025  

---

They say time is money—but in this case, time was root.

While navigating a TryHackMe privilege escalation lab, I found a cron job running every minute as `root`, pointing to a script I could edit as a low-privileged user. What followed was a clean, elegant escalation:

- Inserted a reverse shell into `backup.sh`
- Set a Netcat listener on my attack box
- Waited for the clock to do the rest

One minute later, I had root. 🕶️

From there, I:
- Retrieved the final flag
- Discovered a lingering password hash in `/etc/shadow`
- Cracked it clean with `john` and `rockyou.txt`

This challenge was more than just root—it was a reminder that misconfigurations and poor cleanup are often the quietest doors into a system.

**Takeaway:** Always inspect cron jobs as part of your escalation routine. If it's writable, it's exploitable.

#PrivilegeEscalation #CronJobs #RedTeamNoir #TryHackMe #Linux #eJPTPrep #LearningInPublic
