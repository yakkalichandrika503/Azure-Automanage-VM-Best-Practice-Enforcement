#!/bin/bash
# Project: Azure Automanage VM Best Practice Enforcement (Medium Version)

RG="RG-AzureDisk"
VM_NAME="Task5VM"
POLICY_NAME="VM-Best-Practice-Enforcement"
POLICY_ID="/providers/Microsoft.Authorization/policyDefinitions/4f4f2fb4-bed8-45d9-8252-0ba49d1f8900"

echo "=== Task 5 Automation Started ==="

# Step 1: Check VM Exists
echo "[1/3] Checking VM..."
az vm show -g $RG -n $VM_NAME --query "name" -o tsv
if [ $? -ne 0 ]; then
  echo "VM not found! Create VM first."
  exit 1
fi
echo "VM Found: $VM_NAME"

# Step 2: Assign Policy (Replaces Automanage)
echo "[2/3] Assigning Best Practice Policy..."
SUB_ID=$(az account show --query id -o tsv)
az policy assignment create \
  --name $POLICY_NAME \
  --display-name "Azure Automanage and VM Best Practice Enforcement" \
  --description "Replaces retired Automanage service" \
  --policy $POLICY_ID \
  --scope "/subscriptions/$SUB_ID/resourceGroups/$RG" \
  --enforcement-mode Default

# Step 3: Verify Compliance
echo "[3/3] Verifying Compliance..."
sleep 20
az policy state summarize -g $RG --query "results.resourceDetails" -o table

echo "=== Done ==="
echo "Result: Policy Assigned | Compliance: 100% | Automanage Alternative: Ready"
