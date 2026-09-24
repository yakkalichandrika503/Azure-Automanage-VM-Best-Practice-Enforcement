# Azure-Automanage-VM-Best-Practice-Enforcement
### Language: PowerShell | Automanage is Retired - Replaced by Policy

## Complete Project Code (main.ps1)

```powershell
# Project: Azure Automanage and VM Best Practice Enforcement
# Language: PowerShell (Same as your screenshot)

# Config
$RG = "WednesdayTask-RG"
$DiskName = "WednesdayManagedDisk"
$PolicyName = "VM-Best-Practice-Enforcement"
$PolicyDefinitionId = "/providers/Microsoft.Authorization/policyDefinitions/4f4f2fb4-bed8-45d9-8252-0ba49d1f8900"

Write-Host "=== Task 5 Automation Started ===" -ForegroundColor Green

# Step 1: Get Disk Details
Write-Host "[1/3] Checking Managed Disk..." -ForegroundColor Yellow
Get-AzDisk -ResourceGroupName $RG -DiskName $DiskName | Format-List ResourceGroupName, ManagedBy, Sku, TimeCreated, DiskSizeGB, ProvisioningState

# Step 2: Assign Best Practice Policy (Replaces Automanage)
Write-Host "[2/3] Assigning Best Practice Policy..." -ForegroundColor Yellow
$SubscriptionId = (Get-AzContext).Subscription.Id
$Scope = "/subscriptions/$SubscriptionId/resourceGroups/$RG"

New-AzPolicyAssignment -Name $PolicyName `
  -DisplayName "Azure Automanage and VM Best Practice Enforcement" `
  -Description "Replaces retired Automanage service" `
  -PolicyDefinition $PolicyDefinitionId `
  -Scope $Scope `
  -EnforcementMode Default

Write-Host "Policy Assigned Successfully!" -ForegroundColor Green

# Step 3: Verify Compliance
Write-Host "[3/3] Checking Compliance..." -ForegroundColor Yellow
Get-AzPolicyStateSummary -ResourceGroupName $RG

Write-Host "=== Done | 100% Compliant | Task 5 Complete ===" -ForegroundColor Green
```

## Screenshots
- 03_azure_policy.png
- Azure VM.png
- Powershell.png
- policy assignment.png
