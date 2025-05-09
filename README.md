# OPERA 5.6 PMS Cheatsheet
**Author:** _Lung Ho_ \
**Copyright:** _May - 2024_

## I. Initial 
Micro Fidelio Opera Print Control 
Opera jinitCheck Control 
Opera Register Terminal 
Oracle JInitiator 1.3.3.25
To Install Opera components

Http://appservername/installadobe.exe

Http://appservername/installregterm.exe

Http://appservername/opera_jinit_1012_25.exe

https://www.oracle.com/technetwork/java/javase/downloads/jre8-downloads-2133155.htm

Http://appservername/installoperaprintctrl.exe

## II. Unable to Communicate with Oracle DBMS
_Get remote access to the database server> sqlplus> (username/pw generic)_

Open a command window (CMD)

Start SQLPlus using a command:


    sqlplus


   _Username:_

     sys as sysdba

     or

     sys@opera as sysdba

   _Password:_

     opera10g 
     
     Opera10g

     opera11g
     
     Opera11g 

   If idle:
   
      startup;

  To restart: 

    shutdown immediate;
    startup;


## III. IE Cannot Display Webpage when accessing Opera
HTTP Server Service is down.

Bounce Services in Oappcfged

## IV. Unable to Start HTTP Server service
Check for World Wide Web Publishing service.

If running, Stop service and then bounce HTTP server service in Oappcfged

## V. Low D Drive Space
   Files in the following directories can be safely deleted:

     D:\MICROS\opera\operaias\webtemp\Opera

     D:\oracle\10gappr2\Apache\Apache\logs(all files not create today)

     D:\oracle\10gappr2\reports\cache

     D:\oracle\admin\OPERA\bdump\(all files except the alert_opera.log)

     _UNDER NO CIRCUMSTANCES DO WE DELETE ARCHIVE FILES_

## VI. Unable to Open PMS from Login page and other Workstation- related issues
### 6.1 Crashes when launching opera application
         Check opera compatibility.
     
         Jinitiator installed
     
         JVM
         
         Popup blocker
         
         Internet explorer settings
         
### 6.2 Replace JVM.DLL
         
   Open my computer: 
   
      C:\Program Files (x86)\Oracle\JInitiator 1.3.1.25\bin\hotspot
      
   Rename the jvm.dll file already there "OLD JVM.DLL"

   Paste the new jvm.dll file there
   
       New file size = 1585kb
       
   If that doesn't work - rename Jinitiator 1.3.1.25 folder to JInitiator 1.3.1.25.old and uninstall/reinstall Oracle Jinitiator program
   
   Add Opera URL to Trusted Sites
   
   Custom Level set all ActiveX controls and plug-ins as Enable
   
   Allow script-initiated windows without size or position constraints
   
   Manage Add Ons - Disabled
   
   Popup Blocker - Off
   
 ### 6.3  Java Configuration
   Start -> Configure Java
   
   Advanced Tab
   
   Show Console
   
   Perform TLS Certificate Revocation Checks on - Do Not Check
   
   Perform Signed Code Certificate Revocation Checks on - Do Not Check
   
   Use TLS 1.0 / 1.1 / 1.2
   
   Security Tab
   
   Add the URL OPERA to the Exception Site List
   
   
Manage Certificates - Add the Root CRTS
Turn off DEP settings for Windows XP
Right click on My Computer select properties.
Click the Advanced tab, and in the Startup and Recovery area, click Settings.
In the SystemStartup area, click Edit.
In Notepad, click Edit and then click Find.
In the Find what field, type /noexecute and then click Find Next.
In the Find dialog box click Cancel.
Replace the policy_level (for example, "OptIn" default) with "AlwaysOff" (without the quotes).
WARNING: Be sure to enter the text carefully.
Your boot.ini file switch should now read: /noexecute=AlwaysOff
In Notepad, click File and then click Save.
Click OK to close Startup and Recovery.
Click OK to close System Properties and then restart your computer
Turn off DEP settings for Windows 7
Start->Run->CMD
Type: wmic OS Get DataExecutionPrevention_SupportPolicy
0-AlwaysOff
1-AlwaysOn
2-OptIn
3-OptOut
If result is anything except for 0, run below:
bcdedit /set nx AlwaysOff
Reboot
Turn off DEP settings for Windows 10
Start->CMD
Type: BCDEDIT /SET {CURRENT} NX ALWAYSOFF
Reboot
Java refresh issue with windows 7
You may not be able to see the delay through windows

Go into control panel >launch jinit 1.3.1.25 and paste the whole thing into parameters(including the - )
-Dsun.java2d.noddraw=true
Registered Terminal Undefined / Registered Terminal keeps changing
Navigate to my computer > SEARCH for termreg file.
Should be saved at C:\Windows > if it is saved anywhere else, cut and copy to the correct location. Test if issue still exists. If issue still exists.
Check if issue is non reproducible under user ADMINISTRATOR. If not, refer to IT to make sure users have the permissions to the file location in windows.
IE Trusted Sites Custom Settings
All of the below need to be marked as Enable:
.NET Framework-reliant components
Run components not signed with Authenticode
Run components signed with Authenticode
ActiveX Controls and plug-ins
Allow previously unused ActiveX control to run without prompt
Allow scriptlets
Automatic prompting for ActiveX controls
Binary and Script behaviors
Run ActiveX controls as plugins
Script ActiveX controls marked safe for scripting
Miscellaneous
Allow script-initiated windows without size or position constraints
The following need to be marked as Prompt:
ActiveX Controls and plug-ins
Download signed ActiveX controls
Download unsigned ActiveX controls
The following need to be marked as Disabled:
ActiveX Controls and plug-ins
Display video and animation on a webpage that does use external media player
Initialize and script ActiveX controls not marked as safe for scripting
Unlock Supervisor and Change Supervisor Password

Connect to the application server
Start>run>cmd
From the command prompt, log into sqlplus
Username: username
Password: (password for independent sites)
For training hotel:
Username: username@schema
Password: Password
Unlock supervisor
Once logged in run the following:
update application$_user set lockout_date=null where app_user='SUPERVISOR';
It should say 1 row updated.
Then commit:
commit;
The supervisor account will now be unlocked
## Change Supervisor Password
Log in to sqlplus as username@schema and run
    
        UPDATE APPLICATION$_USER SET APP_PASSWORD='BETTERTHANV6', INACTIVE_DATE=NULL, DISABLED_UNTIL=NULL, ACCOUNT_LOCKED_OUT_YN='N', LOCKOUT_DATE=NULL WHERE APP_USER = 'SUPERVISOR';

Then run

       commit;

Password will now be 'BETTERTHANV6 '

    
Printing Issues
PRINTER SETUP
It is the IT responsibility to add the printer to the workstation in Windows. Make sure that printing in windows works correctly before troubleshooting Opera. (test printing from notepad/word)
Configuration>Setup>printers>new>select dropdown>choose printer
Printer must have the EXACT same name in Opera as in windows.
If choosing the dropdown freezes Opera, you must manually add in the printer by typing it into the Physical Device field

Printers on Print Servers are added in a different format:
In Windows, if printer is named Canon BW on print server. In Opera, the format should be: \\PRINTSERVER\CANON BW

PRINTER TASK
PMS>Miscellaneous>Print Tasks OR Configuration>Setup>Workstations>Print Tasks
Make sure that the printer has the EXACT same name in Opera as it does in Windows and that printers on print servers have the correct formatting.
For Latin American sites> folio printer check box on printer setup controls which print task will be available
REP 51002 Bind to Report Server when printing from all workstations
Connect to application server>bounce ReportsServer service in OAPPCFGED
Not able to print from 1 workstation
Check that IE version is correct.
Check ALL IE settings are setting correctly
Check that the print tasks are set to the exact printer name as what is in windows
Expand printing in progress window to see if you are able to view pdf in the window.
Adobe>edit>preferences>internet>make sure all boxes are check
OXI
OXI Conversion Code Setup
OXI>interface configuration>conversion codes>site should put in what conversions between opera and external interfaces are for rate code/ room types/categories/memberships types/etc.

If you do not see an active conversion, click inactive to check for it

Resync OXI
OXI>utilities>resync>check the XML in OXI message status> messages to external> confirm opera is sending correct information (by reading the xml)>refer to vendor

Common How - to's
Install License Code
Configuration>Setup>License>PMS license
How to change default folio style
Application setting to change default folio style /default AR folio style
How to change folio style on individual reservation
From billing screen> Folio>Folio Styles>select folio style site wishes to change it to. Check F1 help for descriptions of each folio style.
Restart OXI Processors/IFC
Check if processors are still running.
OXI>interface status>processors (you can stop or start from here)
Connect to OXI server. start>run>type services.msc>stop and start the service for the interface
usually called 'Opera interface for XXXX'
'Please swipe again' error when swiping card on one workstation.
Configuration>setup>workstations> (workstation highlighted in blue is the workstation you are working on)>edit
Check swipe reader attached check box
Grant user permission
Configuration>setup>user configuration>users>edit>permission.
Make sure to have a letter from general manager on company letter head/ via email with general manager signature in the email.
If user granting the permission does not have the permission themselves, they may not grant it. If user granting the user group does not have the user group they are trying to assign, they will not be able to do so.
Inventory Imbalance
Compare the control panel, house status, and detailed availability screens. (miscellaneous>show quick keys)
Utilities>synchronize utilities>synchronize inventory, physical rooms, block occupancies, stay records
Check that forecast processor is running: Utilities>processors>forecast processor. Make sure it is running, no failed/pending events.
Changing application settings
Configuration>setup>application settings.
Remember to log out of opera and log back in after making an app setting change
Record in use by another user/workstation
Utilities>tools>session statistics> highlight users session>kill

Creating table space
See creating datafiles doc.
Make sure you have supervision when creating datafiles.
Use script if you do not see enterprise manager console (it is not there for sites using oracle 11g)
Change room type for a room number
There are (5) requirements prior to being able to Change a room type. In order to change the room type of a room, you must make sure that none of the following apply:

The room is currently checked in.
If getting an error that the room is checked in go to reservations>update reservations>click advanced>search all reservations with that room type to find any that are checked in.
The room was checked out today.
If getting an error go to reservations>update reservations>click advanced>search all reservations with that room type to find any that checked out on today's date. If it has checked out today, the end of day must be rolled before making the change.
The room is set to Out of Order/Out of Service now or in the future.
If getting an error go to PMS>rooms management>out of order/service>search with blank date>delete entries for that room number.
The room is listed on a task assignment sheet now or in the future.
If getting an error go to PMS>rooms management>housekeeping>task assignment>search for completed and pending task assignment sheets>click expanded>search for the room in the list. If the room is there, delete the task sheet that it is on. If unable to delete advise the site to let audit roll and do not put on sheet for next day.
The room is pre-blocked on a future reservation.
have site go to the reservation and remove the room number
Log into Opera Utilities

Select Utilities

Select Property Config

Change Room

Change Room Type for room number.

Some sites will want to change all rooms in one room type to another room type. The above still applies but when making the change, navigate to:

Log into Opera Utilities

Select Utilities

Select Property Config

Change Room

Change Room Type for another room type

when getting here, opera will require a password. It changes every day. The formula for the password is:

Current day * Current month * 5 + 11

ex: October 9, 2015 = 461

Room Status Discrepancy in Housekeeping
Rooms management>housekeeping>housekeeping management>place cursor in from field. Press Shift+F7 on keyboard.
SQL for unlock an external locked block
If a block is being externally controlled it means that one of their OXI interfaces is controlling it
BEFORE RUNNING THIS, REFER TO EXTERNAL VENDOR FIRST TO UNLOCK!!!
Navigate to UTILTIIES>TOOLS>OPERA SQL.

Script to unlock:

update allotment_header set external_locked=null where allotment_header_id= blockid

Credit Cards not processing
Error message? All workstations? All reservations/credit cards? Recent network/server/opera changes? When did this begin happening? Try heartbeat test (configuration>setup>property interfaces>interface configuration>double click cc interface (CCW/EFT)>click test button)

Pass or Fail?

Pass → refer to cc processor

Fail → take note of number next to failure>log>search transaction>open log scroll to bottom.

Search error in MOS KM

Trial Balance vs Ledger Imbalance
Confirm imbalance>attach reports to Service Request>run imbalance analysis in utilities>6 month increments> find live date via script>run imbalance until live and escalate. Do not paste imbalance into Service Request, paste into notepad and attach to the Service Request.
How to manually add commissions
Commissions>Payment Processing>By Agent or Acct>Select the Account or agent needed>If the reservation in question is displayed in the lower section of the Commission Processing, you can right click & select "Manual Commission Adjustment" and enter an amount. If not, follow the below steps:
Commissions>Payment Processing>By Agent or Acct>Select the Account or agent needed>On the "Commission Processing" screen select "Search">Select criteria for your search (Checked out, reservation, etc) >Select the reservation needed (If the Travel Agent was not attached it will ask if you wish to attach it, say Yes) >it will then try to process the commission. The reservation will then display in the lower section of the Commission Processing. You can then highlight it & right click. Next select "Manual Commission Adjustment" and enter an amount.
SET NIGHT AUDIT TO COMPLETE
Select * from night_audit_jurnal where bus iness_date = 'DD-MMM-YYYY'

Find the sys_job_id #

Update night_audit_jurnal set status = 'COMPLETED' where sys_job_id ='XXXXXX'

"No credit" from POS
Uncheck no post from pm reservation for payment type

Adobe ? When Printing
Windows theme should be basic

POP-UPS ON RESERVATION SCREENS
Configuration>setup>screen design>popup blockers

SET FIELD DEFAULTS
Configuration>setup>screen design>field and button defaults

HOW TO IDENTIFY EACH SERVER
Check services on the server to determine:

Application Server will have service: Oracle10gappr2ProcessManager

DB Server will have service: OracleServiceOpera

Interface Server will have service: Opera IFC Controller

OXI server will have service: "Opera Interface for (whatever the name is for the OXI interface)"

RESTART EXAMPLES (WHAT IS RESOLVED BY A SERVER REBOOT)
Opera Down (after other basic attempts at troubleshooting)

Opera Slowness

Recommend Server reboot every 30 days.

Opera Freezing/hanging

How to check system up time:

Start>Run>CMD> type systeminfo

find system "up time" or "boot time"

SERVER TROUBLESHOOTING (when you need to connect to server)
Issues on all workstations.

If issue is reproducible on the server and not just one or a couple of workstations.

WORKSTATION TROUBLESHOOTING
Issue is not reproducible on the server.

Issue is not happening on all workstations

QUESTIONS TO ASK ON CALL/ADD TO Service Request NOTES
Service Request Stamp

Please make sure names are correct in the Service Request.

If Service Request is opened from Night Auditor, try to get a daytime point of contact for the issue.

Full Opera Version (ex:5.0.03.03/17)

Clear Description of the issue

Keep in mind that a lot of times, the site does not know exactly what the issue is/is not completely honest. Get connected and have the Reproduce the issue for you. If you do not understand them still, have them repeat it.

Steps to reproduce. Very important!

While connected, take note of the steps the caller is taking to reproduce the issue. Put them in your Service Request notes so that if the Service Request is escalated/dispatched the issue does not have to be repeated.

Example: Connected to workstation. PMS>reservations>update reservation>searched reservation confirmation number 123456>edit reservation>swipe card in payment field. Received error message: "please swipe again"

Work Performed

What Steps did you take to resolve the issue: Also take note of similar Service Request numbers found in MOS or Knowledge Documents found/attempted.

Plan of action

If you are researching a Service Request and find something you would like to try to resolve it, add it to your notes as a plan of action.

If you call a site with intentions on doing something, leave a plan of action for the next tech to attempt when the site calls back.

Alfredo Aguirre
Powered by Webnode
This website was made with Webnode. Create your own for free today!
Get started
