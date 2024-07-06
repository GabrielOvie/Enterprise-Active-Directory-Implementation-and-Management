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
