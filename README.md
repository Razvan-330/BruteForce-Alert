<h1>Bruteforce Alert for Splunk</h1>

<h2>Description</h2>
This alert helps in combating and detecting brute-force attacks by identifying failed logins equal to or greater than 10 within a 2-minute time frame, thus quickly notifying the team and providing details about the source IP, the user, and the computer name where the attack is occurring, so it can be stopped as quickly as possible.

<b>This alert can help with:</b>

- Early detection of brute-force attacks by correlating failed authentication attempts.
- Prevention of unauthorized access by blocking attacked accounts.
- Protection of the IT infrastructure by identifying and blocking suspicious IP addresses.
<br />


<h2>Languages and Utilities Used</h2>

- <b>SPL-Search Processing Language</b>
- <b>BotsV2-[Dataset](https://github.com/splunk/botsv2)</b>
  
<h2>Environments Used </h2>

- <b>SIEM-Splunk</b>
- <b>OS-Kali Linux</b>

<h2>Alert Setup:</h2>

<b><p align="center">
SPL Query: <br/> 
</b>
```
index=botsv2 sourcetype=wineventlog source="wineventlog:security" EventCode=4625
| stats count by src_ip user ComputerName
| where count >= 10
| table ComputerName, user, src_ip, count
```
<b>The SPL query searches for Windows Security Event ID 4625, which indicates failed login attempts. It aggregates these events by source IP, user, and computer name, then filters the results to only show those with 10 or more failed attempts—potential signs of a brute-force attack. Finally, the output is displayed in a clear table format to aid in quick analysis and response.</b>


<br />
SPL Query Results in the Dataset:  <br/>
<img src="https://i.imgur.com/nSt07oR.png" height="80%" width="80%" alt="Dataset Query"/>
<br />

From the results, we can observe that the computer “mercury.frothly.local”, with the user “MERCURY$” from source IP 10.0.1.100, recorded a total of 3162 failed logon attempts.
Similarly, the user “Administrator” from IP 10.0.1.220 recorded a total of 189 failed login attempts.

<b><h3>Saving and Configuring the Alert:</h3></b>

To save and configure the alert, click on Save as > Alert.

<b>Title:</b> Assign a title to the alert (e.g., BruteForce Alert).

<b>Permissions:</b> Choose the alert's permission setting — either Private (personal use) or Shared in App (accessible to other users in the app). In a corporate context, it should be shared so that the response to such attacks can be as quick and coordinated as possible.

<b>Alert Type:</b>
Set to Scheduled - Run on Cron schedule (*/2 * * * *), so the alert runs every 2 minutes (Parameter 2).
Real-time is an option, but it might generate unnecessary traffic.

<b>Expires:</b> Set to 24 Hours. The alert will expire 24 hours after being triggered, which is appropriate for this type of attack, as it requires a fast response.

<b>Trigger Conditions:</b>
Set to Number of results is greater than 0 (Parameter 3).
Since the SPL query already filters to show results with 10 or more failed attempts, a single qualifying result is sufficient to trigger the alert. One failed login alone will not trigger the alert, allowing for normal human errors.

<b>Trigger Actions:</b>
Choose Add to Triggered Alerts (severity: High).
This alert will generate a high-severity notification to ensure it’s investigated as quickly as possible.

<br />
Save as Alert: <br/>
<img src="https://i.imgur.com/ku2yzRA.png" height="80%" width="80%" alt="Bruteforce alert"/>
<br />
<br />
Trigger Actions:  <br/>
<img src="https://i.imgur.com/3QsbsuI.png" height="80%" width="80%" alt="Bruteforce alert"/>
<br />

<!--
 ```diff
- text in red
+ text in green
! text in orange
# text in gray
@@ text in purple (and bold)@@
```
--!>
