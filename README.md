# Azure Stack on Azure
为 Azure Stack Hub Development kit (ASDK) 在Azure上创建准备 POC验证环境

## Version Compatibility

## Description
Deploy-AzureStackonAzureVM.ps1 script prepares Storage Account and copy VHD file before you calling ARM Template

## Step by Step Guidance
Step 1 - Download the Deploy-AzureStackonAzureVM.ps1 script

Run the following PowerShell command to install the new installation script. This will also downloads required modules from powershell gallery.

```powershell
Find-Script Deploy-AzureStackonAzureVM | Install-Module -Force
```


