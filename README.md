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

<br />
Enter the number of passes: <br/>
<img src="https://i.imgur.com/nCIbXbg.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
Confirm your selection:  <br/>
<img src="https://i.imgur.com/cdFHBiU.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
Wait for process to complete (may take some time):  <br/>
<img src="https://i.imgur.com/JL945Ga.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
Sanitization complete:  <br/>
<img src="https://i.imgur.com/K71yaM2.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
Observe the wiped disk:  <br/>
<img src="https://i.imgur.com/AeZkvFQ.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>

<!--
 ```diff
- text in red
+ text in green
! text in orange
# text in gray
@@ text in purple (and bold)@@
```
--!>
