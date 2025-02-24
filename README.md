# TechNet Systems Cybersecurity Lab: Investigating and Securing Systems
(Ficticious Organization)

<h2> Overview </h2>

This lab focused on mitigating a simulated system breach by enhancing security controls and eliminating vulnerabilities. I conducted process monitoring, audited password security, and enforced strict access controls to protect system integrity.

<h2>Technical Skills</h2>
✅ Process Monitoring & Threat Detection<br />
✅ Password Auditing (John the Ripper)<br />
✅ Access Control & Privilege Management<br />
✅ User & Group Configuration Auditing<br />
✅ File Permission Hardening<br />
✅ Legacy Service Identification & Removal<br />


<h2>  Inventory of Active System Processes </h2>
I first executed a script file to compromise the system. Then, I ran the <b>top</b> command to generate a comprehensive list of all active processes. I carefully analyzed this list to identify any processes that appeared unfamiliar or suspicious. By comparing them against known safe processes and reviewing resource usage, I pinpointed potential anomalies that required further investigation or immediate action.
<br />
<br />
<p align="center">
<img src="https://i.imgur.com/A0kAc80.png" height="80%" width="90%" alt="Running processses"/>
 <br />
 <br />
<img src="https://i.imgur.com/tsho2du.png" height="80%" width="90%" alt="Running processses"/>

<h2>  Copying the Shadow Password File </h2>
I carefully copied the /etc/shadow file using secure file management commands such as <b>cp</b>, ensuring that appropriate permissions were maintained to prevent exposure of sensitive data. With the necessary root or administrative privileges, I accessed and copied the file securely. After executing the command, I verified the file’s integrity and confirmed its successful transfer to a secure location for further analysis. <br />
<br />
<p align="center">
<img src="https://i.imgur.com/EOaP3cs.png" height="80%" width="90%" alt="Copying shadow file"/>


<h2>  Editing the Shadow Copy File to Retain Only System Users </h2>
I edited the shadow_copy file using the <b>nano</b> text editor, carefully reviewing each line to identify and remove any unnecessary or irrelevant entries that did not pertain to actual system users. I ensured that only legitimate system users remained, eliminating any obsolete accounts or test entries to maintain accuracy and security. <br />
<br />
<p align="center">
<img src="https://i.imgur.com/RAKpJJi.png" height="80%" width="90%" alt="Editing Shadow_copy file"/>
 <br />
 <br />
<img src="https://i.imgur.com/22nOInc.png" height="80%" width="90%" alt="Editing Shadow_copy file"/>

<h2>  Running the Shadow File Through a Password Cracker </h2>
I used the <b>john</b> program to crack the passwords stored in the shadow_copy file. By leveraging a suitable wordlist and optimized cracking techniques, I systematically attempted to reveal user credentials. Once the process was complete, I reviewed the results to identify any successfully cracked passwords for further analysis. <br />
<br />
<p align="center">
<img src="https://i.imgur.com/E4vUAe5.png" height="80%" width="90%" alt="Cracking password"/>
 <br />
 <br />
<img src="https://i.imgur.com/5pfFUeD.png" height="80%" width="90%" alt="Cracking password"/>

<h2>  Checking Sudo Access of Users with Weak Passwords </h2>
I used the <b>sudo -lU</b> command to check which users had sudo privileges. By cross-referencing this information with previously cracked passwords, I identified accounts with weak credentials that also had elevated access. These high-risk accounts were flagged for immediate action, and I documented my findings to support the revocation of their sudo privileges. <br />
<br />
<p align="center">
<img src="https://i.imgur.com/PggkFNJ.png" height="80%" width="90%" alt="Checking sudo access"/>

<h2>  Removing Sudo Access from Users in the Sudoers File </h2>
I used <b>visudo</b> to securely edit the <b>/etc/sudoers</b> file, ensuring that any modifications would not introduce syntax errors. I carefully searched for user-specific entries granting sudo access and removed or commented out those associated with weak passwords. After making the necessary changes, I saved and exited the file, then verified the updates to confirm that unauthorized users no longer had elevated privileges. <br />
<br />
<p align="center">
<img src="https://i.imgur.com/OEMTu2O.png" height="80%" width="90%" alt="Removing sudo access"/>
 <br />
 <br />
<img src="https://i.imgur.com/MqXAGCa.png" height="80%" width="90%" alt="Removing sudo access"/>

<h2>  Removing Less Access from Users in the Sudoers File </h2>
I used the <b>visudo</b> command to securely edit the <b>/etc/sudoers</b> file, ensuring that any modifications were syntax-checked to prevent misconfigurations. I carefully reviewed the file for user-specific or group-specific entries that granted unnecessary or unauthorized access. Identifying such entries, I either commented them out or removed them entirely to restrict unauthorized privilege escalation. After making the changes, I verified the updates to confirm that only authorized users retained appropriate sudo access. <br />
<br />
<p align="center">
<img src="https://i.imgur.com/MqXAGCa.png" height="80%" width="90%" alt="Removing less access"/>

<h2>  Confirming Changes to the Sudoers File </h2>
After editing the <b>/etc/sudoers</b> file, I ran a syntax check using the <b>visudo</b> command to ensure that no errors were introduced, preventing potential misconfigurations that could lock out administrative access. I then manually reviewed the file to verify that only authorized users retained the necessary privileges. Finally, I confirmed the applied changes by checking user privileges with <b>sudo -l</b> for relevant accounts, ensuring that unauthorized access had been successfully revoked. <br />
<br />
<p align="center">
<img src="https://i.imgur.com/zC6YiY9.png" height="80%" width="90%" alt="Confirming changes"/>
 <br />
 <br />
<img src="https://i.imgur.com/COWsIh4.png" height="80%" width="90%" alt="Confirming changes"/>
 <br />
 <br />
<img src="https://i.imgur.com/1SNZRyS.png" height="80%" width="90%" alt="Confirming changes"/>

<h2>  Checking IDs for Every User on the System </h2>
I ran the <b>id 'user'</b> command to retrieve detailed user information, including UID (User ID) and GID (Group ID). By systematically reviewing each entry, I ensured that administrative accounts had the correct assignments and that no unauthorized users possessed elevated privileges. Any discrepancies were flagged for further investigation and corrective action. <br />
<br />
<p align="center">
<img src="https://i.imgur.com/Xar9Dua.png" height="80%" width="90%" alt="Checking userID"/>


<h2>  Checking Groups Users Belong to on the System </h2>
I ran the <b>groups</b> command for individual users to review all group memberships on the system. This allowed me to cross-check the groups each user belonged to and identify any unauthorized or suspicious group assignments. I paid special attention to privileged groups such as sudo or admin to ensure that only authorized accounts were included. <br />
<br />
<p align="center">
<img src="https://i.imgur.com/48pQP6r.png" height="80%" width="90%" alt="Checking groups"/>

<h2>  Removing Jack from the Sudo Group </h2>
I used the <b>usermod -G</b> command to remove Jack from the sudo group. After executing the command, I verified the change by running <b>groups jack</b> to confirm that Jack was no longer a member of the sudo group. <br />
<br />
<p align="center">
<img src="https://i.imgur.com/NfFVGA1.png" height="80%" width="90%" alt=""/>

<h2>  Removing Unauthorized Users and Groups from the System </h2>
I used the <b>deluser</b> and <b>delgroup</b> commands to remove unauthorized users and groups, ensuring that their associated files were also deleted to maintain system integrity. <br />
<br />
<p align="center">
<img src="https://i.imgur.com/JUCOsSw.png" height="80%" width="90%" alt="Removing users and groups"/>

<h2>  Adding Users to the Appropriate Group </h2>
I created any missing groups using the <b>addgroup</b> command. Then, I used the <b>usermod</b> command to add users to their designated groups. Specifically, I ensured that users like Adam, Billy, Sally, and Max were members of the developers group and their own primary groups only. <br />
<br />
<p align="center">
<img src="https://i.imgur.com/7MbeNee.png" height="80%" width="90%" alt="Adding users to group"/>

<h2>  Setting File Permissions </h2>
Guided by best practices, I adjusted file permissions for key system files to enhance their security using the <b>chmod</b> command. After applying these changes, I ran <b>ls -l</b> to verify the updated permissions and documented the adjustments for future reference.<br />
<br />
<p align="center">
<img src="https://i.imgur.com/mKHexpm.png" height="80%" width="90%" alt="Setting permissions"/>

<h2>  Checking for Vulnerabilities </h2>
I used vulnerability assessment tools, including <b>systemctl</b>, to scan the system for misconfigurations, outdated software, and potential security gaps. After completing the scans, I reviewed the output for any identified vulnerabilities or warnings. <br />
<br />
<p align="center">
<img src="https://i.imgur.com/4xQMcbA.png" height="80%" width="90%" alt="Checking for vulnerabilities"/>
 <br />
 <br />
<img src="https://i.imgur.com/RvXiEA1.png" height="80%" width="90%" alt="Checking for vulnerabilities"/>
 <br />
 <br />
<img src="https://i.imgur.com/OT6FCNq.png" height="80%" width="90%" alt="Checking for vulnerabilities"/>

<h2>  Stopping Vulnerable Services </h2>
After identifying vulnerable or unnecessary services during the audit, I took immediate steps to stop them. Using the <b>systemctl stop</b> command, I halted any flagged services. <br />
<br />
<p align="center">
<img src="https://i.imgur.com/m2TW6Uc.png" height="80%" width="90%" alt="Stopping vulnerable services"/>
 <br />
 <br />
<img src="https://i.imgur.com/qXZskVM.png" height="80%" width="90%" alt="Stopping vulnerable services"/>
 <br />
 <br />
<img src="https://i.imgur.com/v5xYq53.png" height="80%" width="90%" alt="Stopping vulnerable services"/>
 <br />
 <br />
<img src="https://i.imgur.com/FIXUSHP.png" height="80%" width="90%" alt="Stopping vulnerable services"/>

<h2>  Disabling Vulnerable Services </h2>
After stopping the flagged services, I disabled them to ensure they remained inactive. This was accomplished using the <b>systemctl disable</b> command. <br />
<br />
<p align="center">
<img src="https://i.imgur.com/5QAs4ue.png" height="80%" width="90%" alt="Disabling vulnerable services"/>
 <br />
 <br />
<img src="https://i.imgur.com/KeFYGM3.png" height="80%" width="90%" alt="Disabling vulnerable services"/>

<h2>  Removing Vulnerable Services from the System </h2>
After stopping and disabling the flagged services, I uninstalled them using the package management tools available on the system. This ensured that any unnecessary or vulnerable software was completely removed from the system. <br />
 <br />
<p align="center">
<img src="https://i.imgur.com/PtrInmB.png" height="80%" width="90%" alt="Removing services"/>
 <br />
 <br />
<img src="https://i.imgur.com/wCTSJ1r.png" height="80%" width="90%" alt="Removing services"/>
