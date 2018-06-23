# ProjectTel

The purpose of this file is to create a design document for forwarding alarms from Netcool Servers to OMi Servers as SNMP traps.
EXECUTIVE SUMMARY
The USM LCM project is adding new distributed OMi solution deployment, two new USM Omi DPS Servers and six new Gateway Servers, along with hardware load balancer (one for user access and other one for data collectors). In this deployment process eight new servers for Omi have been introduced.  The database servers for Omi deployment are separate from these eight servers. We need to monitor OS and OMi application as part of standard monitoring. This document provides the changes to USM design to include the new Omi servers.
Note: OMi DB will be monitored as per standard USM Oracle monitoring. The FB monitoring is not in the scope of this design.
Server Details:
       Server FQDN	IP 	Hardware	OS	Type
lxapp6438.dc.corp.telstra.com	10.75.6.23	VM	RHEL 6.9	Gateway
lxapp6439.dc.corp.telstra.com	10.75.6.24	VM	RHEL6.9	Gateway
lxapp6436.dc.corp.telstra.com	10.75.6.20	VM	RHEL6.9	DPS
lxapp6437.dc.corp.telstra.com	10.75.6.22	VM	RHEL6.9	DPS
lxapp6515.dc.corp.telstra.com	10.75.6.29	VM	RHEL6.9	Gateway
lxapp6516.dc.corp.telstra.com	10.75.6.30	VM	RHEL6.9	Gateway
lxapp6517.dc.corp.telstra.com	10.75.6.31	VM	RHEL6.9	Gateway
lxapp6518.dc.corp.telstra.com	10.75.6.32	VM	RHEL 6.9	Gateway
	
Load Balancer VIP Details:
       VIP FQDN	IP 	Type
usmopsbridge.in.telstra.com.au	10.75.67.13	User access
usmopsbridgedc.in.telstra.com.au	10.75.6.24	Data collectors

•	The USMOpsBridge aspect contains templates for both OS and application monitoring. 
             Note: For template details, please refer section 2.5.
•	The OMi DPS server’s application and OS monitoring will be performed via USMOpsbridge OMi DPS monitoring templates.
•	The OMi GW server’s application and OS monitoring will be performed via USMOpsbridge OMi GW monitoring templates.
•	The USM Opsbridge OMi URL (user access and data collectors) will be monitored via EPIC Sitescope under URL sequence monitoring category. The robotic ID will be used from Sitescope to login to both the OMi application URL on every 10 minutes and dynamic content match will be enabled at step 2 of the URL sequence (i.e. POST Login page of OMi).
•	The F5 LB URL of OMI will be monitored via same Sitescope in EPIC and content will be matched. This will not be URL sequence, this will be single URL with Content Match.
•	The parent business CI will be USMOpsBridge in iTAM for all alarms.
•	L2 – AS&IT will be the alarm support group.

1.1.	RESOURCES
This section must be completed for all designs
Resource	Name	Telephone
USM Designer *	Subhasish G	
Delivery Consultant	Subhasish G	
Engineering SME	Kevin Ching	
Operations SME  	Kevin Ching	
Integration Lead		
Alarm Instructions  	Subhasish G	
Network Designer	N/A	N/A

NOTE: An * indicates that this information is MANDATORY.

1.2.	TIME TABLES
This section details when the entire solution must be delivered by and when hosts etc will be available for implementation to commence
Date hosts available for alarming	06/10/2018
Date OVIS targets available for alarming	NA
`Go live’ date 	06/30/2018

NOTE: An * indicates that this information is MANDATORY.




1.3.	OBSERVATION AND LEVEL 3 SUPPORT TEAMS
This section must be completed for all designs
Team	
Observation Team (O/S and H/W)	(L2 – AS&IT)
Observation Team (M/W and Application)	(L2 – AS&IT)
Level 3 Support (App)	

1.4.	 NETWORK TOPOLOGY 

This section is to detail which network or networks the hosts and/or devices are on as well which RPoP is to be used.  The specific details in regards to the RPoP are to be found in section 2.2
               
1.5.	WBS ELEMENTS

Role/Area	WBS Element
USM Design & Build tasks (by SMS group)	A.46027676.1.1.04.04.1
Operational Support Systems	A.46027676.1.1.04.04.2
Software Purchasing	A.46027676.1.1.04.04.1



1.6.	LICENSING
Software Description	Quantity of USM Software Required
ESX CO	0
OVIS Targets **	0
OVO / OVP agents	8
Sitescope Targets	1



1.7.	USM IMPLEMENTATION TASKS
Please indicate below (with a ) which of the following function areas are to be engaged to implement this design:
Function Area	Engagement Required
Agent Load	
Alarms (by OSS)	
Development	
Foundation	
Non-Standard Reporting	
Notification	
OVIS	
OVPI	
OVPM	
OVSN	
Reporter	
SIP	
SLA	




1.8.	ITAM DOCKETS
This section is to capture iTam docket numbers that the implementation is dependent on, for example Service Model and new/updated template QA’s as well as alarm instructions (in spreadsheet format)
     
           
Deliverable	Number/Name
Service Model	
Template/scripts  	
Alarm Instructions	
Quality Centre	










 
2.	OPENVIEW OPERATIONS
Use this section to document details for OMi Operations requirements.
2.1.	NODE(S) TO BE ADDED
Nodes that are to be added can be either controlled or managed. Please complete this table for each node that this design addresses. When completing the OS table please indicate if it is 32 or 64 bit where appropriate
2.1.1.	FOR NODE TYPE CONTROLLED


Hostname	FQDN	IP 	
NATTED IP	Hardware	OS
lxapp6438	lxapp6438.dc.corp.telstra.com	10.75.6.23		VM	RHEL 6.9
lxapp6439	lxapp6439.dc.corp.telstra.com	10.75.6.24		VM	RHEL6.9
lxapp6436	lxapp6436.dc.corp.telstra.com	10.75.6.20		VM	RHEL6.9
lxapp6437	lxapp6437.dc.corp.telstra.com	10.75.6.22		VM	RHEL6.9
lxapp6515	lxapp6515.dc.corp.telstra.com	10.75.6.29		VM	RHEL6.9
lxapp6516	lxapp6516.dc.corp.telstra.com	10.75.6.30		VM	RHEL6.9
lxapp6517	lxapp6517.dc.corp.telstra.com	10.75.6.31		VM	RHEL6.9
lxapp6518	lxapp6518.dc.corp.telstra.com	10.75.6.32		VM	RHEL 6.9







2.2.	USM COMMUNICATIONS
The following table details the USM Omi connectivity of Omi servers. The communication between Omi servers will be direct and will not pass through ant R-POP.
Omi VIP Connectivity Information
Short Name	usmopsbridgedc.in.telstra.com.au
Location	EPIC
VIP addr	10.75.67.14


FQDN	Management Server	Machine Type	console_par2 	console_par3
			RPOP name or NONE	Agent	POLLLED-A/B	TRAP	SYSLOG
lxapp6438.dc.corp.telstra.com	usmopsbridgedc	Linux Red Hat 6.9 2.6.32	none	ICMP  			
lxapp6439.dc.corp.telstra.com	usmopsbridgedc	Linux Red Hat 6.9 2.6.32	none	ICMP			
lxapp6436.dc.corp.telstra.com	usmopsbridgedc	Linux Red Hat 6.9 2.6.32	none	ICMP			
lxapp6437.dc.corp.telstra.com	usmopsbridgedc	Linux Red Hat 6.9 2.6.32	none	ICMP			
lxapp6515.dc.corp.telstra.com	usmopsbridgedc	Linux Red Hat 6.9 2.6.32	none	ICMP			
lxapp6516.dc.corp.telstra.com	usmopsbridgedc	Linux Red Hat 6.9 2.6.32	none	ICMP			
lxapp6517.dc.corp.telstra.com	usmopsbridgedc	Linux Red Hat 6.9 2.6.32	none	ICMP			
lxapp6518.dc.corp.telstra.com	usmopsbridgedc	Linux Red Hat 6.9 2.6.32	none	ICMP			
Note: ICMP is enabled from EPIC Sitescope server to all the OMI servers. 
2.3.	NEW VIEW NAME
                   Please use this section to define new view name
          
View Name	Description	Functional or Product
Omi Deployment  	This OOB view displays all Omi Servers (DPS and GWs)	
		
		
2.4.	PRODUCT NODE GROUP ASSIGNMENTS
Product node group assignments are basically metadata in USM. Please note that a node must never be assigned to more than one product node 
Add all nodes to be managed in this table placing a tick [] next to the node group(s) to which the node belongs.
Node	Product Node Group
	P: USMOpsBridge  															
lxapp6438																
lxapp6439																
lxapp6436																
lxapp6437																
lxapp6515																
lxapp6516																
lxapp6517																
lxapp6518																
usmopsbridge																
usmopsbridgedc																









2.5.	MANAGEMENT TEMPLATE AND ASPECT
Please use this table to detail the node to aspect assignments
Add all nodes to be managed in this table placing a tick [] next to the aspects to which the node belongs. 
Node		Functional Node Group
	F:OS Linux RH	F: USMOpsBridge  															
lxapp6438																	
lxapp6439																	
lxapp6436																	
lxapp6437																	
lxapp6515																	
lxapp6516																	
lxapp6517																	
lxapp6518																	

The management template and aspect resides at OMi under administration  Monitoring  Management Template & Aspect.


Alarm and template details for this design  :

Alarm	AIN	Template	Template Group
Failed to update live server after backup server took over  	79156	OMi Bus Logfile2.10	USMOpsbridge Self-Monitoring
Failed to set live server within 15 seconds	79157	OMi Bus Logfile2.10	USMOpsbridge Self-Monitoring
Could not execute CMDB query for TQL OMiAutoView	79158	OMi Scripting Host Logfile2.11	USMOpsbridge Self-Monitoring
All OMi server components started	79159	OMi Nanny Logfile2.10	USMOpsbridge Self-Monitoring
All OMi server components stopped	79160	OMi Nanny Logfile2.10	USMOpsbridge Self Monitoring
All OMi server components Launched	79161	OMi Nanny Logfile2.10	USMOpsbridge Self Monitoring
Script error reported on Gateway server.	79162	OMi Scripting Host Logfile2.11	USMOpsbridge Self Monitoring
Process OPR stopped	79163	OMi Nanny Logfile2.10	USMOpsbridge Self Monitoring
Process OPR Started	79164	OMi Nanny Logfile2.10	USMOpsbridge Self Monitoring
JMS Bus hang detected. Executing corrective action	79165	OMi_BusMonitor2.10	USMOpsbridge Self Monitoring
JMS Bus hang is free now	79166	OMi_BusMonitor2.10	USMOpsbridge Self Monitoring
The size of a JMS Bus Queue is greater the defined threshold	79167	OMi_BusMonitor2.10	USMOpsbridge Self Monitoring
Check JMS Bus Queue size – critical	79168	OMi_BusMonitor2.10	USMOpsbridge Self Monitoring
Remote  host closed connection during handshake	79169	Omi Event receiver Log file3.0	USMOpsbridge Self Monitoring
The OMi internal certificate Server Certificate expires in 30 days	79170	OMi_CertMonitor2.11	USMOpsbridge Self Monitoring
The Omi internal certificate is still 30 days valid	79171	OMi_CertMonitor2.11	USMOpsbridge Self Monitoring
The Omi Web server certificate Server Certificate expires in 30  days	79172	OMi_CertMonitor2.11	USMOpsbridge Self Monitoring
The OMi database certificate expires in <$VALUE> days	79174	OMi_CertMonitor2.11	USMOpsbridge Self Monitoring
FileSystem space utilization for /opt exceeded Threshold	79176	Sys_FileSystemUtilizationMonitor(1.203)
	USMOpsbridge Infrastructure Management Templates
EventSyncThread.logServerUnavailable(1691) - Server lxapp6438 appears to be unavailable. Event update forward request will be re-queued for later delivery:	79190	OMi Event Receiver Logfile3.0	USMOpsbridge Self Monitoring
ERROR EventSyncThread.sendUpdateList(582) - Server lxapp6438 appears to be unavailable. 1 event update requests will be re-queued for later delivery, first event ID:	79191	OMi Event Receiver Logfile3.0	USMOpsbridge Self Monitoring
ERROR EventOperationsSender.sendOperation(156) - Exception while trying to send operation.CMAUpdateOperation, Acknowledge: javax.net.ssl.SSLHandshakeException: Remote host closed connection during	79192	OMi Event Receiver Logfile30	USMOpsbridge Self Monitoring
ERROR EventOperationsSender.sendOperation(156) - Exception while trying to send operation.CMAUpdateOperation, Acknowledge: javax.net.ssl.SSLHandshakeException: Remote host closed connection during	79193	OMi Event Receiver Logfile3.0	USMOpsbridge Self Monitoring
ERROR JobExecutor.invoke0(?) - Job ( job ID: ) for node ‘ USMOpsBridge failed. Reason: Could not connect to the node.	79195	OMi Event Receiver Logfile3.0	USMOpsbridge Self Monitoring
OA  process  oacore  stopped on USMOpsBridge	79210	OMi Selfmon process Monitor1.0	USMOpsbridge Self Monitoring
OA  process oacore started on USMOpsBridge	79211	OMi Selfmon process Monitor1.0	USMOpsbridge Self Monitoring
OA  process  ovbbccb stopped on USMOpsBridge	79215	OMi Selfmon process Monitor1.0	USMOpsbridge Self Monitoring
OA  process  ovcd stopped on USMOpsBridge	79217	OMi Selfmon process Monitor1.0	USMOpsbridge Self Monitoring
OA  process  opcmsga stopped on USMOpsBridge	79214	OMi Selfmon process Monitor1.0	USMOpsbridge Self Monitoring



2.6.	OBSERVATION GROUPS
Please use this table to detail the node to Observation group assignments
Add all nodes to be managed in this table placing a tick [] next to the node group(s) to which the node belongs.
Node	Observation Group
	O:L2-ASIT-HW-OS	O:L2-ASIT-HW-App														
lxapp6438																
lxapp6439																
lxapp6436																
lxapp6437																
lxapp6515																
lxapp6516																
lxapp6517																
lxapp6518		  														
usmopsbridge		 														
usmopsbridgedc		 														


2.7.	PRODUCT GROUPS
2.7.1.	ITAM PROUDCT NODE GROUP

            This section is to detail the USM /iTAM Product group relationships

USM View	Itam Product Group
OMi Deployment	USMOpsBridge
	
	
2.7.2.	NEW USM PRODUCT NODE GROUPS

                This section is to detail any new USM product node group
  
Node Group Name	Node Group Label	Description
		
		
		
2.8.	ADD NODE SCRIPT

This section is where the add node script is to be added 
Please note this must be added as a zip file to prevent differing versions of Office causing issues 

 
2.9.	OPERATING SYSTEM PROCESS AND SERVICE MONITORING
Include OS process and service monitoring (i.e additional to standard OS template group) in this section (i.e. cron). For more information see “USM Monitoring Configuration Guide” (as listed in the References section).
2.9.1.	UNIX OS PROCESS / SERVICE MONITORING
Complete one table per application/severity grouping.
For Data Processing Server:
Node(s)	Application	Object	Msg Group	Severity	Service Name (OVSN)
lxapp6438
lxapp6439	OMi	<$MSG_OBJECT>	Application	Major	<$MSG_NODE_NAME>
Process	Operator	Count	Process Parameters*	Case Sensitive Parameters (Y/N)
hpbsm_bus	>=	1		
hpbsm_RTSM	>=	1		
Jboss	>=	1		
hpbsm_marble_supervisor	>=	1		
hpbsm_bizImpact	>=	1		
hpbsm_opr-scripting-host	>=	1		
hpbsm_opr-backend	>=	1		








For Gateway Servers:
Node(s)	Application	Object	Msg Group	Severity	Service Name (OVSN)
lxapp6436
lxapp6437
lxapp6515
lxapp6516
lxapp6517
lxapp6518	OMi	<$MSG_OBJECT>	Application	Major	<$MSG_NODE_NAME>
Process	Operator	Count	Process Parameters*	Case Sensitive Parameters (Y/N)
hpbsm_RTSM	>=	1		
Jboss	>=	1		
hpbsm_wde	>=	1		
hpbsm_opr-scripting-host	>=	1		
hpbsm_opr-backend	>=	1		








2.9.2.	WINDOWS OS PROCESS / SERVICE MONITORING
Node(s)	Windows Service Name	Msg Group	Object	Severity	Application
		NTService			
		NTService			
		NTService			

2.10.	MIDDLEWARE AND APPLICATION PROCESS AND SERVICE MONITORING
Include Middleware and application specific process monitoring in this section (e.g. Oracle, IIS).  The Service Name used must align to a corresponding Service Name in the Service Model.
2.10.1.	UNIX MIDDLEWARE / APPLICATIONS PROCESS (ES) AND SERVICE(S) WITHOUT AUTO-RESTART
Use one table per Application grouping.
Node(s)	Application	Object	Msg Group	Severity	Service Name (OVSN)
lxapp6436
lxapp6437
lxapp6515
lxapp6516
lxapp6517
lxapp6518
lxapp6438
lxapp6439	OMi	Internal	OpC	Critical	APP:OMi:<$MSG_NODE_NAME>
Process	Operator	Count	Process Parameters*	Case Sensitive Parameters (Y/N)
midaemon	>=	1		
ttd	>=	1		
perfalarm	>=	1		
perfd	>=	1		
hpsensor	>=	1		
oacore	>=	1		
ompolparm	>=	1		
opcacta	>=	1		
opcle	>=	1		
opcmona	>=	1		
opcmsga	>=	1		
opcmsgi	>=	1		
ovbbccb	>=	1		
ovcd	>=	1		
ovconfd	>=	1		


2.10.2.	UNIX MIDDLEWARE / APPLICATIONS PROCESS(ES) AND SERVICE(S) WITH AUTO-RESTART
OVO has the ability to restart applications if it detects that they have failed.  Use this section to include details of applications that need to be restarted if they fail.  For each application that requires auto restarting you also need to include:
-	the utility to test the running state of the application
-	the utility(s) to stop and/or start the application
Node(s)	Process	Operator	Count	Service Name (OVSN)	Severity	Msg Group	Object	Application	Parameters
									
									

2.10.3.	WINDOWS MIDDLEWARE / APPLICATIONS PROCESS(ES) AND SERVICE(S)
Node(s)	Windows Service Name	Service Name (OVSN)	Severity	Msg Group	Object	Application
				NTService		
				NTService		



2.11.	APPLICATION ACCESSIBILITY MONITORING

This application web console availability can be monitored via Sitescope. Please fill the following section for URL sequence monitoring with content match.

NOTE: A password must never be included in this document.


Probe Type	HTTPS
Reporting		Reporting is supplied by default.
Note: If Availability Alarming is also required, please  this box.
Availability Alarming		
Target	https://usmopsbridge.in.telstra.com.au/topaz/login.jsp

Hostname	usmopsbridge	Virtual Asset?	Yes
Service Name	usmopsbridge 
Timeout WARN	8s	Timeout ERROR	10s
Severity WARN	Major	Severity ERROR	Critical
BSA	NA
AIN	AIN#79301
Message Group	USM
Additional Information (Any UserID / Password requirements must be entered here.)	 n106974


Probe Type	HTTPS
Reporting		Reporting is supplied by default.
Note: If Availability Alarming is also required, please  this box.
Availability Alarming		
Target	https://usmopsbridge.in.telstra.com.au/opr-web/framework/app#/myWorkspace/

Hostname	usmopsbridge	Virtual Asset?	Yes
Service Name	usmopsbridge 
Timeout WARN	8s	Timeout ERROR	10s
Severity WARN	Major	Severity ERROR	Critical
BSA	NA
AIN	AIN#79301
Message Group	USM
Additional Information (Any UserID / Password requirements must be entered here.)	Content Match: /a href="?([:\/\w\s\d\.]*)"?/i



Probe Type	HTTPS
Reporting		Reporting is supplied by default.
Note: If Availability Alarming is also required, please  this box.
Availability Alarming		
Target	https://usmopsbridge.in.telstra.com.au:443/topaz/topaz_api/loadBalancerVerify_centers.jsp

Hostname	usmopsbridge	Virtual Asset?	Yes
Service Name	usmopsbridge 
Timeout WARN	8s	Timeout ERROR	10s
Severity WARN	Major	Severity ERROR	Critical
BSA	NA
AIN	AIN#79302
Message Group	USM
Additional Information (Any UserID / Password requirements must be entered here.)	Content Match: /(Success)/i

No Login Credentials required.




Probe Type	HTTPS
Reporting		Reporting is supplied by default.
Note: If Availability Alarming is also required, please  this box.
Availability Alarming		
Target	https://usmopsbridgedc.in.telstra.com.au:443/ext/mod_mdrv_wrap.dll?type=test

Hostname	usmopsbridge	Virtual Asset?	Yes
Service Name	usmopsbridge 
Timeout WARN	8s	Timeout ERROR	10s
Severity WARN	Major	Severity ERROR	Critical
BSA	NA
AIN	AIN#79303
Message Group	USM
Additional Information (Any UserID / Password requirements must be entered here.)	Content Match: /(Success)/i



Probe Type	ICMP
Reporting		Reporting is supplied by default.
Note: If Availability Alarming is also required, please  this box.
Availability Alarming		
Target	lxapp6438.dc.corp.telstra.com
lxapp6439.dc.corp.telstra.com
lxapp6436.dc.corp.telstra.com
lxapp6437.dc.corp.telstra.com
lxapp6515.dc.corp.telstra.com
lxapp6516.dc.corp.telstra.com
lxapp6517.dc.corp.telstra.com
lxapp6518.dc.corp.telstra.com
Hostname	<$MSG_NODE_NAME>	Virtual Asset?	Yes
Service Name	usmopsbridge 
Timeout WARN		Timeout ERROR	120s
Severity WARN		Severity ERROR	Critical
BSA	NA
AIN	79271
Message Group	USM
Additional Information (Any UserID / Password requirements must be entered here.)	NA
 
2.12.	CRON JOB MONITORING
This applies to Unix hosts only.  By default Cron jobs are not monitored .If a cron job is to be monitored please complete this tables.
Node(s)	Command	User	Return Code	Severity	Parameters
					
					
					
					
					

2.13.	ORACLE MONITORING
Note: Oracle process-monitoring requirements must be captured in Section Middleware and Application Process and Service Monitoring.
For each Oracle instance complete the following table:
Table Space monitoring for OMi Servers.  
Instance (SID)	NA
Oracle Version Number	
Oracle Home Directory	
Logfiles (including full path)	
Oracle RAC	False
Oracle ASM	False
Table space	Threshold %	Severity
		
		
		
		
		
		
		
		
		
		
		
		

2.13.1.	ORACLE PASSWORD 
Where appropriate please complete this table  
NOTE: A password must never be included in this document.
Who will supply Password	Telephone Number	Email Address
		
		
		
2.13.2.	OVO CONFIGURATION FILES

This section is for all the configuration files that are to be deployed. One line per node
Please add as zip 


Node	OS & Disk	Middleware	Application(s)
			
			
			
			
2.14.	POLLING AND TRAP COLLECTION

This section is for all the details on location from which devices are to be polled and the destination and source of any traps 
2.14.1.	POLLING DETAILS


Source Name  (Poller)	Source IP Address	Target Name	Target IP Address
			
			
			
			
2.14.2.	TRAP DESTINATIONS
Source Name 	Source IP Address	Destination Name	Destination IP Address
			
			
			
			
 
2.14.3.	UNIX FILESYSTEM / WINDOWS DISK UTILISATION ALARMING
Use one of the following tables to customise the default thresholds either globally or per Unix filesystem / Window disk. 
NOTE: You may use one table or the other, not both.
2.14.4.	GLOBAL THRESHOLDS FOR DISK UTILISATION 
Only complete this table if you want to have global utilisation thresholds for all Unix filesystems or all Windows disks.
Severity Level	Threshold (%)
(Please indicate below the Percentage (%) for each Severity Level.)
Warning	
Minor	85
Major	90
Critical  	95

2.14.5.	CUSTOMISED THRESHOLDS FOR UNIX BY FILESYSTEM OR WINDOWS DISK UTILISATION

Only complete the following table if you wish to customise the above Global thresholds for specific Unix file systems or Windows disk
Node(s)	Unix Filesystem / Windows Disk	Severity	Threshold (%)
lxapp6436	/var/opt/OV/	minor	85
lxapp6436	/var/opt/OV/	major	90
lxapp6436	/opt/app/OV/	minor	85
lxapp6436	/opt/app/OV/	major	90
lxapp6436	/opt/OV/	minor	85
lxapp6436	/opt/OV/	major	90
lxapp6437	/var/opt/OV/	minor	85
lxapp6437	/var/opt/OV/	major	90
lxapp6437	/opt/app/OV/	minor	85
lxapp6437	/opt/app/OV/	major	90
lxapp6437	/opt/OV/	minor	85
lxapp6437	/opt/OV/	major	90
lxapp6438	/var/opt/OV/	minor	85
lxapp6438	/var/opt/OV/	major	90
lxapp6438	/opt/app/OV/	minor	85
lxapp6438	/opt/app/OV/	major	90
lxapp6438	/opt/OV/	minor	85
lxapp6438	/opt/OV/	major	90
lxapp6439	/var/opt/OV/	minor	85
lxapp6439	/var/opt/OV/	major	90
lxapp6439	/opt/app/OV/	minor	85
lxapp6439	/opt/app/OV/	major	90
lxapp6439	/opt/OV/	minor	85
lxapp6439	/opt/OV/	major	90
lxapp6515	/var/opt/OV/	minor	85
lxapp6515	/var/opt/OV/	major	90
lxapp6515	/opt/app/OV/	minor	85
lxapp6515	/opt/app/OV/	major	90
lxapp6515	/opt/OV/	minor	85
lxapp6515	/opt/OV/	major	90
lxapp6516	/var/opt/OV/	minor	85
lxapp6516	/var/opt/OV/	major	90
lxapp6516	/opt/app/OV/	minor	85
lxapp6516	/opt/app/OV/	major	90
lxapp6516	/opt/OV/	minor	85
lxapp6516	/opt/OV/	major	90
lxapp6517	/var/opt/OV/	minor	85
lxapp6517	/var/opt/OV/	major	90
lxapp6517	/opt/app/OV/	minor	85
lxapp6517	/opt/app/OV/	major	90
lxapp6517	/opt/OV/	minor	85
lxapp6517	/opt/OV/	major	90
lxapp6518	/var/opt/OV/	minor	85
lxapp6518	/var/opt/OV/	major	90
lxapp6518	/opt/app/OV/	minor	85
lxapp6518	/opt/app/OV/	major	90
lxapp6518	/opt/OV/	minor	85
lxapp6518	/opt/OV/	major	90












3.	VMWARE MONITORING VIA NWORKS 

3.1.1.	VCENTER SERVER
               
          The function of this section is to establish if the VM farm is monitored with Cloud Optimizer.

	
VCenter v4,v5,v6
3.1.2.	ESX CLUSTER NAME AS IN VCENTER

Please specify the cluster to ESX host relationship in this table placing a tick [] next to the cluster name which the ESX node belongs 
ESX Node	Cluster Name
																
																
																
																
																
																
																
																
																
Note: The above cluster is listed as ‘Unmonitored cluster’ in the MainDB.xml.
3.1.3.	ESX HOSTS 
     PLEASE REFER TO SECTION 2.1.2 FOR DETAILS AND ADDNODE.









3.1.4.	 VM GUEST AND ESX HOST CUSTOM ATTRIBUTES 
                
Node	Custom Attribute
	
	
	
	
	
	
	
	
	
	

NOTE Veeam.ems_node custom attribute setting on VC must verified has been set for any node that is to be monitored by USM 
3.1.5.	CO SERVERS

	
	

3.1.6.	CO VMWARE ROOT


3.1.7.	REQUIRED USER ACCOUNTS

User Name	Role	Notes
TBD	Ssh access for COTS monitoring	This is required so we can connect to the ESX server via SSH to get the COTS information. Thsi is done via plink and runs a “df”
TBD	Read Only User to allow the collector to retrieve data from the VC server,	To add an read only user to VC: 

1. Create a user account either local or domain (eg rouser) 
2. Connect to your VC using the Virtual Infrastructure client 
3. Select Inventory – Hosts And Clusters 
4. Right Click on the top level container (“Host & Clusters”) and select “Add Permission” 
a. You can add permissions to any object, so you can be as detailed as you like with permissions 
5. The default screen will be to add a read only user. Click the Add button 
6. Search for the user you created, select that user, click the add button, and then click ok 
7. Then configure Collector to use that user to connect to the VC through the VICConfig
TBD	Domain robot account for VIC services	NWorks VIC to nMC service authentication

This allows the VIC services to be controlled by the NWorks management console

3.1.8.	VMWARE INFRASTRUCTURE CONTACT FOR PASSWORDS
NOTE: A password must never be included in this document.
Who will supply Passwords	Telephone Number	EMAIL ADDRESS
		

4.	OMI PERFORMANCE
Use this section to document design details for OMi Performance monitoring.
4.1.	APPLICATION GROUPING
This section is compulsory for applications running on shared platforms.  It is recommended for all other applications.
Data can be collected and reported on in a more detailed fashion by grouping data by application or user.
Application	User	Processes
		
		

4.2.	STANDARD OVP DATA COLLECTION
Will be deployed by default.  Complete Section Non-Standard OVP Alarming and/or Data Collection if non-standard alarming and data collection is required.

4.3.	NON-STANDARD ALARMING (OVP) AND/OR DATA COLLECTION
If non-standard data collection is required Section Non-Standard Reporting Requirements must be completed.
4.3.1.	ALARMING: NEW OR EXTENDED FOR EXISTING DATA COLLECTED
4.3.2.	DATA COLLECTION: ADDITIONAL REQUIREMENTS (USING OVP DATA SOURCE INTEGRATION)
DSI requirements would normally be documented by Capacity Management and delivered as an Attachment to the Design.
4.3.2.1.	UNIX DATA COLLECTION
Provide sample output of command to run highlighting what output needs to be collected.
4.3.2.2.	WINDOWS DATA COLLECTION
ECB – metrics to collect on, perfmon.
4.3.2.3.	ALARMING ON DSI DATA
Is data for reporting only or alarming + reporting?
4.3.3.	OVPA PARM FILE 

This section is for all the configuration files that are to be deployed. One line per node


Node	Parm File
	
	
	
	

5.	REPORTING
Only complete this section if you require Non-standard Reporting.
5.1.	NON-STANDARD REPORTING REQUIREMENTS
Please specify the non-standard reporting requirements by placing a tick [] beside the appropriate option.
	New Report(s) Required on Data currently Existing in USM
	New Report(s) Required on Data not currently Existing in USM

Please discuss the reporting requirements for this design with the Convergence and Planning group (Contact: Roy Partington on 08-8401 7316).





6.	INTERNET SERVICES PROBING
Use this table to define standard OVIS probing, use one table per target.
If OVIS probing of URLs is required then at least one generic (non-host specific) OVIS URL test of the service provided is mandatory to measure when service as a whole is unavailable.
Probe Type	
Reporting		Reporting is supplied by default.
Note: If Availability Alarming is also required, please  this box.
Availability Alarming		
Target	
Hostname		Physical or Virtual Host?	
Service Name	
Severity	
Scheduled Outage	
Additional Information (Any UserID / Password requirements must be entered here.)	

Note: All network connectivity requirements must be arranged prior to testing.
6.1.1.	PASSWORD AND CERTIFICATES
NOTE: A password must never be included in this document.
Where appropriate please complete this table  Who will supply Passwords and Certificates	Telephone Number	EMAIL ADDRESS
		
		
		
7.	SERVICE LEVEL AGREEMENTS
Indicate which services you require Service Level Reporting for, that is, the major services on which the customer is offered a SLA. Use one table per service, placing a tick [] next to the Reporting Frequency(s). Default items already have a tick beside.
Service Name	
SLA Offering (Please tick [] whichever is applicable.)		PLATINUM
		GOLD
		SILVER
		BRONZE
		Other, specify:
Reporting Frequency		Annual
		Quarterly
		Monthly
		Weekly
		Other, specify:

8.	SERVICE INFORMATION PORTAL (SIP) – CUSTOMER ACCESS

8.1.	NEW SIP USERS

Please specify any new Telstra internal customers, support staff, product managers that require access to the SIP view generated by this design. (
Name	Email Address
NA Alarms Optimisation Team	
	

These users will be advised of the SIP Login URL, the User Name and password to enable them to view SIP information referring to the service described in this design.
8.2.	SIP VIEW POINTS
                     This section is to detail the SIP Viewpoints that are to be used
9.	ALARM INSTRUCTIONS & NOTIFICATION
9.1.	ALARM INSTRUCTIONS
Any new or revised alarm instructions must be presented in spreadsheet format
9.2.	ALARM NOTIFCATION
9.2.1.	PURPOSE OF NOTIFICATION
What is the purpose of the notification?

9.2.2.	ALARMS FOR NOTIFICATION
Complete the following table for any alarm notification(s) required.  Use one table per user (i.e. person to be notified).
Name of Person to be Notified	
Person’s Email address 	
Company Name for the above person	
Notification Style (Tick [] whichever is required.)
SMS		Mobile Number	
Email		Email Address	
Pager		Pager Number	
SYMON		SYMON ID	
Message Group	Node	Severity	Application	Object
				
				

 
10.	REFERENCES
DOCUMENT NUMBER	TITLE
DME Reference numbers	Example SAD , RDD
TAF0001-345434	USM Network Connectivity for Monitored Servers and Devices (to get correct RPOP and USM Host details)
TAF0001-309395	Valid Machine types are defined in TAF0001-309395 
11.	DEFINITIONS
TERM	DEFINITION
	
	
	
12.	ATTACHMENTS
DOCUMENT NUMBER	TITLE
	Service Model (Visio  )
13.	DOCUMENT CONTROL SHEET
Contact for Enquiries and Proposed Changes
If you have any questions regarding this document contact:
NAME:	D209102

DESIGNATION:	TEAM LEADER USM SOLUTIONS
PHONE:	(03) 8661 1044
FAX:	

If you have a suggestion for improving this document, please contact the person listed above.
ISSUE NO.	ISSUE DATE	NATURE OF AMENDMENT
		
		
		



