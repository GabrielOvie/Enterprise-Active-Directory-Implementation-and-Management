# Enterprise Active-Directory Implementation and Management
Hands-on with Windows Server environments, Active Directory, and Group Policies.
## Objective
Design, implement, and manage a comprehensive Windows Server environment with Active Directory for a medium-sized business with 1000 employees across 3 locations.

## End Goals
- **Robust Active Directory Infrastructure**: Efficient and secure replication between all domain controllers; Scalable OU structure that accommodates future growth and organizational changes; Automated user provisioning and deprovisioning processes; Centralized management of user accounts, groups, and computers; Implemented fine-grained password policies and account security measures.
- **Comprehensive Group Policy Framework:** Implementing a set of well-documented, thoroughly tested Group Policies that enforce security baselines, manage user environments, and streamline software deployment, Implementing least-privilege access model across the organization, Automated application of security settings and software updates.
- **Enhanced Security Posture:** Multi-factor authentication implemented for all privileged accounts and remote access; BitLocker encryption deployed on all company devices; Privileged Access Management solution implementation to secure administrative access.
- **Efficient File and Print Services**: Centralized file storage with appropriate access controls and data deduplication; DFS namespaces and replication configured for seamless file access across all sites; Centralized print management with automated printer deployment.
- **Robust Backup and Disaster Recovery Solution**: Ability to recover the entire AD infrastructure within the defined RTO and RPO. Comprehensive backup strategy covering all critical servers and data.
- **Proactive Monitoring and Maintenance:** Centralized monitoring solution providing real-time insights into the health and performance of the AD infrastructure; Automated alerting system for critical events and performance thresholds; Scheduled maintenance tasks to ensure optimal system performance.
- **Compliance and Audit Readiness:** Implementing logging and auditing measures to track changes in the AD environment; generating reports for compliance audits (e.g., user access reviews, security policy enforcement).
- **Cost Optimization:** Reduced administrative overhead through automation and centralized management; Optimized storage utilization through data deduplication and efficient file management; Minimized security incidents and associated costs through proactive security measures.

## Lessons Learnt
- **Planning and Design**: Importance of thorough initial planning, and Flexibility in design.
- **Active Directory Implementation**: Setting up a test domain before full implementation helped identify and resolve issues early; Properly configured sites, DNS infrastructure and site links are crucial for efficient replication in a multi-site environment.
- **Group Policy Management**: Rigorous testing of Group Policies in a controlled environment before deployment is crucial to prevent widespread issues; correctly implementing loopback processing mode solved several user profile issues in shared computer scenarios; Regular review and consolidation of GPOs improved overall system performance and manageability.
- **Security Implementation**: Consistently applying this principle from the start prevented many potential security vulnerabilities; Implementing a robust monitoring solution was essential for maintaining security posture and quickly identifying potential threats.
- **Disaster Recovery**: Scheduled DR tests uncovered gaps in the recovery process that weren't apparent in the planning phase, Detailed, step-by-step recovery procedures proved invaluable during DR scenarios, Backup strategy diversification: Implementing both on-site and off-site backups; Having detailed rollback plans for each major change provided a safety net and increased confidence in implementations.
- **User Management:** PowerShell scripts for user management tasks significantly reduced administrative overhead and human errors; Implementing password reset self-service reduced help desk calls dramatically; Consistent naming conventions for users, computers, and groups greatly simplified management and troubleshooting.
- **Future-Proofing**: Stress testing the infrastructure beyond current needs helped identify potential scalability issues before they became problems.

## Tools Used:

- Windows Server 2019 Datacenter Edition
- Active Directory Domain Services
- Group Policy Management Console
- Windows Admin Center
- PowerShell for automation and scripting
- Hyper-V for virtualization
- Microsoft LAPS (Local Administrator Password Solution)
- Microsoft ADFS (Active Directory Federation Services)
- Veeam Backup & Replication for backup and disaster recovery
- PRTG Network Monitor for comprehensive monitoring
- Microsoft Visio for network diagramming
- Git for version control of scripts and configurations
- Microsoft Azure for hybrid cloud integration
- Wireshark for network troubleshooting
- Nmap for network discovery and security auditing
- Microsoft Baseline Security Analyzer (MBSA)
- Sysinternals Suite for advanced system utilities

## Detailed Project Steps 
Phase 1: Planning and Design (Duration: 2 weeks)
1.1 Organization Structure Analysis

Conduct interviews with simulated department heads
Document current and projected employee count per department
Identify special access requirements for each department
Map out physical office locations and remote work scenarios

1.2 Active Directory Design

Design forest structure (single forest for the organization)
Plan domain structure (single domain: contoso.local)
Design OU structure:

Location-based OUs (HQ, Branch1, Branch2)
Department-based OUs under each location (IT, HR, Finance, Sales, etc.)
Special OUs for servers, service accounts, and groups


Plan naming conventions:

Users: firstname.lastname
Computers: LOC-DEPT-TYPE-##  (e.g., HQ-IT-LT-01 for an IT laptop at HQ)
Groups: ROLE-DEPT-PERMISSION (e.g., ROLE-IT-AdminAccess)



1.3 Network Planning

Design IP addressing scheme:

HQ: 172.16.0.0/16
Branch1: 172.17.0.0/16
Branch2: 172.18.0.0/16


Plan subnets for each department within locations
Design DNS structure:

Internal DNS zones: contoso.local, subzones for each branch
External DNS requirements


Plan DHCP scope for each subnet

1.4 Server Infrastructure Planning

Determine number and placement of domain controllers

2 DCs at HQ, 1 each at Branch1 and Branch2


Plan for additional server roles:

File servers
Print servers
DHCP servers
Certificate Authority


Virtual machine resource allocation for each server role

1.5 Group Policy Strategy

Identify required Group Policies:

Security baseline policies
Software deployment policies
User environment policies


Plan GPO linking strategy
Design GPO naming convention

1.6 Security Planning

Define password policy requirements
Plan for implementation of least privilege access
Design multi-factor authentication strategy
Plan for data encryption (BitLocker) implementation

1.7 Backup and Disaster Recovery Planning

Define Recovery Point Objective (RPO) and Recovery Time Objective (RTO)
Design backup strategy for servers and Active Directory
Plan for site-to-site replication for disaster recovery

1.8 Project Timeline and Resource Allocation

Create a detailed Gantt chart for project phases
Assign responsibilities to team members (simulated)
Identify potential risks and mitigation strategies

Phase 2: Windows Server Environment Setup (Duration: 1 week)
2.1 Procurement and Setup (simulated)

"Order" necessary hardware:

4 physical servers for domain controllers
2 physical servers for Hyper-V hosts
Networking equipment (switches, routers)


Set up server racks and cable management

2.2 Hyper-V Host Configuration

Install Windows Server 2019 Datacenter Edition on physical hosts
Configure basic settings:

Hostname: HQ-HVHOST-01, HQ-HVHOST-02
IP addressing: 172.16.0.10, 172.16.0.11
Windows Updates


Install Hyper-V role
Configure virtual switches:

External switch for VM internet access
Internal switch for isolated VM communication


Set up Hyper-V Replica between hosts for VM high availability

2.3 Virtual Machine Creation

Create VMs for domain controllers:

HQ-DC-01, HQ-DC-02, BR1-DC-01, BR2-DC-01
Allocate 4 vCPUs, 8GB RAM, 100GB storage each


Create VMs for additional server roles:

HQ-FS-01 (File Server)
HQ-PRINT-01 (Print Server)
HQ-DHCP-01 (DHCP Server)
HQ-CA-01 (Certificate Authority)


Install Windows Server 2019 on all VMs
Configure basic settings for each VM (hostname, IP address, updates)

2.4 Network Configuration

Configure VLANs on physical switches
Set up routing between subnets
Configure firewall rules for inter-site communication

Phase 3: Active Directory Domain Services Implementation (Duration: 1 week)
3.1 Primary Domain Controller Setup

On HQ-DC-01:

Install AD DS role
Run dcpromo to create new forest and domain (contoso.local)
Configure DNS for AD DS
Set up AD-integrated DNS zones


Verify AD DS and DNS functionality

3.2 Additional Domain Controllers

On HQ-DC-02, BR1-DC-01, BR2-DC-01:

Install AD DS role
Join to existing domain
Promote to domain controller


Configure site links for efficient replication
Test replication between all DCs

3.3 Fine-tuning AD DS

Configure AD DS diagnostics, monitoring, and recovery tools
Set up AD Recycle Bin
Configure FSMO roles distribution

Phase 4: Active Directory Structure Implementation (Duration: 2 weeks)
4.1 Organizational Unit Creation

Create top-level OUs:

HQ, Branch1, Branch2
ServiceAccounts, Groups, Computers


Under each location OU, create department OUs:

IT, HR, Finance, Sales, Marketing, Operations


Create sub-OUs as needed (e.g., Servers under Computers)

4.2 User Account Creation

Develop PowerShell script for bulk user creation
Create test users for each department (at least 10 per department)
Set user properties:

Job titles
Department
Manager
Email address


Set up user home directories

4.3 Group Creation

Create Global Groups for each department
Create Universal Groups for cross-department teams
Create Domain Local Groups for resource access
Nest groups appropriately following best practices

4.4 Computer Account Management

Pre-create computer accounts for workstations and servers
Move computer accounts to appropriate OUs
Set up Group Policy to automate computer account creation

4.5 Service Account Management

Create service accounts for various applications
Implement Microsoft Local Administrator Password Solution (LAPS)

Phase 5: Group Policy Implementation (Duration: 2 weeks)
5.1 Group Policy Object Creation

Create and link the following GPOs:

Default Domain Policy (password policies, account lockout)
Default Domain Controllers Policy
Security Baseline Policy (based on Microsoft Security Baseline)
User Environment Policy (folder redirection, roaming profiles)
Software Deployment Policy
Windows Update Policy
BitLocker Policy
AppLocker Policy



5.2 Security Policies

Configure fine-grained password policies
Implement account lockout policy
Set up Kerberos policy
Configure User Rights Assignment

5.3 User Environment Policies

Set up folder redirection for Documents, Desktop, and Pictures
Configure roaming profiles
Implement desktop and Start menu standardization

5.4 Software Deployment

Package standard software (Office 365, Adobe Reader, etc.)
Create software deployment GPOs
Test and verify software installation via GPO

5.5 Windows Update Management

Configure WSUS server (HQ-WSUS-01)
Set up GPOs for update management:

Approval groups
Automatic updates schedule
Reboot management



5.6 BitLocker Implementation

Configure BitLocker GPOs
Set up BitLocker key backup to AD

5.7 AppLocker Configuration

Develop AppLocker policies for:

Executable rules
Windows Installer rules
Script rules


Test and enforce AppLocker policies

5.8 Group Policy Testing and Verification

Develop and execute test plans for each GPO
Use gpresult and RSOP.msc for troubleshooting
Document GPO settings and intended effects

Phase 6: File and Print Services (Duration: 1 week)
6.1 File Server Configuration

On HQ-FS-01:

Configure data volumes and shares
Set NTFS and share permissions
Implement access-based enumeration


Set up DFS namespaces and replication for branch office file access

6.2 Print Server Setup

On HQ-PRINT-01:

Add and share printers
Configure printer permissions
Set up printer deployment via Group Policy



6.3 Data Deduplication

Enable and configure data deduplication on file servers
Monitor and report on storage savings

Phase 7: Additional Services Configuration (Duration: 1 week)
7.1 DHCP Server Setup

On HQ-DHCP-01:

Install DHCP Server role
Configure DHCP scopes for each subnet
Set up DHCP failover with branch office servers



7.2 Certificate Authority Implementation

On HQ-CA-01:

Install AD Certificate Services role
Configure enterprise root CA
Set up certificate templates for various purposes (VPN, web servers, etc.)



7.3 Remote Access Configuration

Set up DirectAccess or Always On VPN for remote workers
Configure multi-factor authentication for VPN access

Phase 8: Monitoring and Maintenance Setup (Duration: 1 week)
8.1 Performance Monitoring

Set up Performance Monitor data collectors
Configure alerts for critical performance thresholds

8.2 Event Log Monitoring

Set up centralized event log collection
Configure alerts for critical events

8.3 Active Directory Health Monitoring

Implement AD replication monitoring
Set up DCDIAG scheduled tasks and alerts

8.4 Maintenance Tasks

Create scheduled tasks for:

Server restarts
Disk cleanup
Defragmentation


Implement automated patching schedule

Phase 9: Security Enhancements (Duration: 1 week)
9.1 Multi-Factor Authentication

Implement Azure MFA or third-party MFA solution
Configure MFA for privileged accounts

9.2 Advanced Threat Protection

Deploy Windows Defender ATP
Configure and test threat detection policies

9.3 Privileged Access Management

Implement Just-In-Time administration
Set up Privileged Access Workstations for admins

9.4 Security Information and Event Management (SIEM)

Set up centralized log collection
Configure alerting and reporting for security events

Phase 10: Backup and Disaster Recovery Implementation (Duration: 1 week)
10.1 Backup Configuration

Install and configure Veeam Backup & Replication
Set up backup jobs for all servers
Configure AD-specific backups

10.2 Disaster Recovery Planning

Develop step-by-step disaster recovery procedures
Set up site-to-site replication for critical servers
Configure Azure Site Recovery for cloud-based DR

10.3 Backup and DR Testing

Conduct full DR test
Document and optimize recovery procedures

Phase 11: Documentation and Knowledge Transfer (Duration: 2 weeks)
11.1 Technical Documentation

Create detailed network diagrams
Document AD structure, GPOs, and configurations
Develop standard operating procedures for common tasks

11.2 User Documentation

Create end-user guides for common tasks
Develop FAQ for IT self-service portal

11.3 Admin Knowledge Base

Document troubleshooting procedures
Create runbooks for critical processes
