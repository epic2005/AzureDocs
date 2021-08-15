# Azure Stack on Azure
为 Azure Stack Hub Development kit (ASDK) 在Azure上创建准备 POC验证环境

## Welcome to the Azure Stack Hub on Azure Step by Step Guide!
In this guide, we'll walk you experiencing a number of the amazing capabilities within Azure Stack Hub 2012.

## Description
Deploy-AzureStackonAzureVM.ps1 script prepares Storage Account and copy VHD file before you calling ARM Template

## Prepaire for the Deployment
* Gloabl Azure AD tenant with Gloabladmin permission


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

You can install PowerShell commands for Azure Stack through the PowerShell Gallery.

```powershell
Set-PSRepository -Name "PSGallery" -InstallationPolicy Trusted
```

After that, you can install the latest Azure Stack PowerShell module to the ASDK host by running the commands below.

```powershell
[Net.ServicePointManager]::SecurityProtocol = [Net.SecurityProtocolType]::Tls12
 
Install-Module -Name Az.BootStrapper -Force -AllowPrerelease
Install-AzProfile -Profile 2019-03-01-hybrid -Force
Install-Module -Name AzureStack -RequiredVersion 2.0.2-preview -AllowPrerelease

Get-Module -Name "Az*" -ListAvailable
Get-Module -Name "Azs*" -ListAvailable
```

We can now configure a GitHub repository hosting PowerShell modules in the ASDK Host VM to manage resources and deploying them to Azure Stack. 

```powershell
# Download the tools archive.
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

You can run the following commands to verify that your ASDK deployment is successful:

```powershell
Enter-PSSession -ComputerName AzS-ERCS01 -ConfigurationName PrivilegedEndpoint
Test-AzureStack
```

![GitHub Logo](/image01.png)

# Last Step
As the last step in our ASDK configuration, you need to register your ASDK environment with Azure. This will allow you to use both Azure marketplace items and full features of Azure Stack. You can run the command below to register. Make sure to define your Azure Subscription ID and a uniqe-registration-name before running the command.

Add-AzAccount -EnvironmentName "AzureCloud"
 
Register-AzResourceProvider -ProviderNamespace Microsoft.AzureStack
 
Import-Module C:\AzureStack-Tools-az\Registration\RegisterWithAzure.psm1
 
Get-AzSubscription -SubscriptionID "<strong><subscription ID></strong>" | Select-AzSubscription
 
```powershell
# Register Azure Stack
$AzureContext = Get-AzContext
$CloudAdminCred = Get-Credential -UserName AZURESTACK\CloudAdmin -Message "Enter the credentials to access the privileged endpoint."
$RegistrationName = "<strong><unique-registration-name></strong>"
Set-AzsRegistration `
-PrivilegedEndpointCredential $CloudAdminCred `
-PrivilegedEndpoint AzS-ERCS01 `
-BillingModel Development `
-RegistrationName $RegistrationName `
-UsageReportingEnabled:$true
 ```
