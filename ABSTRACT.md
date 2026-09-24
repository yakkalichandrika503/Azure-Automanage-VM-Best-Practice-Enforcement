# Azure Automanage - VM Best Practice Enforcement

### 1. ABSTRACT
This project automates Azure VM management using PowerShell and Azure Policy. Since Azure Automanage is retired, we use Policy to enforce best practices like Backup, Monitoring, and Security. It reduces manual work and gives 100% compliance.

### 2. REQUIREMENTS
- Azure Subscription
- Resource Group: WednesdayTask-RG
- VM: Task5VM
- Managed Disk: WednesdayManagedDisk
- Azure Cloud Shell (PowerShell)
- Azure Policy

### 3. ARCHITECTURE
START 
  -> Create VM and Disk
  -> Apply Azure Policy
  -> Enable Backup, Monitor, Defender
  -> Check Compliance
  -> Monitor VM
END


### 4. USE CASES
1. Auto Onboarding: New VMs get best practices automatically.
2. Enterprise:100+ VMs managed with same rules.
3. Replacement:Works even after Automanage is retired.

### 5. BOTTLENECKS FACED
1. Automanage retired - Solved using Azure Policy
2. Permission error - Solved with Owner role
3. Compliance delay 15 min - Waited for evaluation
4. Command error in VS Code - Used Cloud Shell

### 6. CONCLUSION
Project completed successfully with 100% compliance. Azure Policy is the best replacement for retired Automanage. It is simple, scalable and cost-effective.
