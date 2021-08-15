# Azure Stack on Azure
为 Azure Stack Hub Development kit (ASDK) 在Azure上创建准备 POC验证环境

## Welcome to the Azure Stack Hub on Azure Step by Step Guide!
In this guide, we'll walk you experiencing a number of the amazing capabilities within Azure Stack Hub 2012.

## Description
Deploy-AzureStackonAzureVM.ps1 script prepares Storage Account and copy VHD file before you calling ARM Template

## Prepaire for the Deployment
* 国际版 AAD租户 - 并且带有 Globaladmin权限


## Step by Step Guidance
### Step 1 - Download the Deploy-AzureStackonAzureVM.ps1 script

Run the following PowerShell command to install the new installation script. This will also downloads required modules from powershell gallery.

```powershell
Find-Script Deploy-AzureStackonAzureVM | Install-Module -Force
```

Can be run from Azure Cloudshell as well. :)

### Step 2 - Run the Deploy-AzureStackonAzureVM.ps1 script

Once script downloaded from PowerShell gallery, run the following command to locate some examples.

```powershell
Get-Help Deploy-AzureStackonAzureVM.ps1 -Examples
```

## Install PowerShell commands for Azure Stack hub

```powershell
Set-PSRepository -Name "PSGallery" -InstallationPolicy Trusted
```

```powershell
[Net.ServicePointManager]::SecurityProtocol = [Net.SecurityProtocolType]::Tls12
 
Install-Module -Name Az.BootStrapper -Force -AllowPrerelease
Install-AzProfile -Profile 2019-03-01-hybrid -Force
Install-Module -Name AzureStack -RequiredVersion 2.0.2-preview -AllowPrerelease

Get-Module -Name "Az*" -ListAvailable
Get-Module -Name "Azs*" -ListAvailable
```

```powershell
invoke-webrequest `
  https://github.com/Azure/AzureStack-Tools/archive/az.zip `
  -OutFile az.zip
 
# Expand the downloaded files.
expand-archive az.zip `
  -DestinationPath . `
  -Force
 
# Change to the tools directory.
cd AzureStack-Tools-az
```
