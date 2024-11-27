<p align="center">

<img src="https://mlfk3cv5yvnx.i.optimole.com/cb:bn-b.2fe21/w:930/h:485/q:mauto/f:best/https://www.ninjaone.com/wp-content/uploads/elementor/thumbs/N1-0921-Group-Policy-Management-Console-blog-image1-1-1-qvjtaq0fhxhzkuuel3xr3mwst5thvoor3jjybjtboy.png"  height="60%" width="60%" alt="Group Policy Management Console"/>
 
 <h1>Group Policy Management and Account Management</h1>
This tutorial outlines the use of the Group Policy Management Console in Active Directory. We will use the console to configure security settings on accounts within our orgnaizational units.
<br />


<h2>Environments and Technologies</h2>

- <b>Microsoft Azure</b> 
- <b>Remote Desktop</b>
- <b>PowerShell</b>

<h2>Operating Systems</h2>

- <b>Windows 10</b> (22H2)
- <b>Windows Server</b> (2022)
  <br />

<h2>Group Policy Management Console</h2>
Log into DC-1 as jane_admin. Click Start, and type gpmc.msc in the search box, then press Enter. This opens the Group Policy Management Console.
  <br>
  <br>
<img src="https://i.imgur.com/nkgStpO.png" height="50%" width="50%" alt="login as Jane Admin"/>
<br />
<br />

In the GPMC, navigate to the Group Policy Objects section. 
Right-click Group Policy Objects and select New to create a new GPO, or right-click an existing GPO and select Edit to modify it. *Name it "Account Lockout Policy"*.


<img src="https://i.imgur.com/1qfdarI.png" height="80%" width="80%" alt="Select Remote Desktop"/><br />
<br />
<br />

Set the <b>Account Lockout Duration</b> to 30 minutes. This is the time in minutes that an account remains locked before it is automatically unlocked.

<img src="https://i.imgur.com/6QKa3lc.png" height="80%" width="80%" alt="Account Lockout Policy"/>

<br />
<br />

Configure the <b>Account Lockout Threshold</b> to 5 invalid logon attempts and the <B>Reset Account Lockout Counter After" to 10 minutes.
 <br/>

<img src="https://i.imgur.com/k50oqGq.png" height="80%" width="80%" alt="Additional lockout settings."/>
<br />
<br />

Update Group Policy:</b>  you can force an update immediately. On a client machine or server, open Command Prompt and type gpupdate /force, then press Enter. <br>
<br />
<img src="https://i.imgur.com/EwSy255.png" height="80%" width="80%" alt="Force gpudate"/>

<br />
<br />

<b>Verify the Policy</b>: To verify the policy, you can use the "rsop.msc" tool on a client machine to see the applied settings.
  <br>
<br/>
<img src="https://i.imgur.com/kJ48CN6.png" height="80%" width="80%" alt="rsop.msc"/>
<br />
<br />
<h2>Dealing with Account Lockouts</h2>
Get logged into DC-1. Pick a random user account you created previously. Attempt to login to it 6 times with a bad password. Note the account lockout message.<br/>
<img src="https://i.imgur.com/QNjZBI4.png" height="80%" width="80%" alt="login failed"/>
<br />
<img src="https://i.imgur.com/VfLAMDD.png" height="60%" width="60%" alt="account locked"/>
<br />
<br />

Log into DC-1 as jane_admin. Unlock the account from within ADUC. See the image below to see how to navigate to the  <br/>

<img src="https://i.imgur.com/BEaJ8st.png" height="80%" width="80%" alt="unlock account"/>
<br />
<br />

Reset the account password. <br/>

<img src="https://i.imgur.com/bW1495K.png" height="80%" width="80%" alt="reset password"/>
<br />
<br />
Try to log back in with the new password. Success! <br/>

<h2>Enabling/Disabling Accounts</h2>
As a foreword, when working Help Desk or support, it is important to check in with Supervisors or Managers when contacted about account disablement. There are many reasons why an account would be disabled, including but not limited to: termination, fraud, or technical issues. 
<br />
<br />
Disable the same account in Active Directory <br/>

<img src="https://i.imgur.com/9MmxFOZ.png" height="80%" width="80%" alt="Disable bigfat"/>
<br />
<br />

Try to login to the client account. Note the message that appears. <br/>

<img src="https://i.imgur.com/3ZwRvja.png" height="60%" width="60%" alt="observe account disabled."/>
<br />
<br />

Enable the account. Note the icon for the client user had changed when we disabled the account. <br/>

<img src="https://i.imgur.com/22QYIZb.png" height="80%" width="80%" alt="Enable the account"/>
<br />
<br />

<h2>Observing Logs</h2>
Observe the logs in the Domain Controller. Open eventvwr.msc in the start menu. Run as administrator.<br/>

<img src="https://i.imgur.com/AG8aHfM.png" height="70%" width="70%" alt="eventvwr.msc"/>
<br />
<br />

Locate the client account and continue. <br/>

<img src="https://i.imgur.com/JWmpQD0.png" height="80%" width="80%" alt="use eventvwr.msc to locate the client account"/>
<br />
<br />

View event logs. In the image, we can see our failed login attempt generated an event log. <br/>

<img src="https://i.imgur.com/eBgEnKC.png" height="80%" width="80%" alt="view event logs"/>
<br />
<br />

Now, view those same logs from the Domain controller.
<img src="https://i.imgur.com/shYz6sd.png" height="80%" width="80%" alt="reset password"/>
<br />
<br />

Finish the lab, but do not delete the VMs in Azure. We will use them for upcoming labs.
If you are done for the day and want to save money, simply “Stop”/turn off the VMs within the Azure Portal
<br/>
