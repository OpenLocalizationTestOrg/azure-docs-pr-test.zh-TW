---
title: "在 Azure 自動化 runbook 中的 Azure Resource Manager 範本 aaaDeploy |Microsoft 文件"
description: "如何 toodeploy Azure Resource Manager 範本儲存在 Azure 儲存體從 runbook"
services: automation
documentationcenter: dev-center-name
author: eslesar
manager: carmonm
keywords: "powershell, runbook, json, azure 自動化"
ms.service: automation
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: powershell
ms.workload: TBD
ms.date: 07/09/2017
ms.author: eslesar
ms.openlocfilehash: f489a8e8635a48f5a6a2f1a88e1c803f56f01832
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-an-azure-resource-manager-template-in-an-azure-automation-powershell-runbook"></a>在 Azure 自動化 PowerShell Runbook 中部署 Azure Resource Manager 範本

您可以使用 [Azure 資源管理範本](../azure-resource-manager/resource-manager-create-first-template.md)撰寫可部署 Azure 資源的 [Azure 自動化 PowerShell Runbook](automation-first-runbook-textual-powershell.md)。

如此一來，您就可以自動化部署 Azure 資源。 您可以在中央、安全的位置 (例如 Azure 儲存體) 中維護 Resource Manager 範本。

在本主題中，我們會建立使用儲存在資源管理員範本的 PowerShell runbook [Azure 儲存體](../storage/common/storage-introduction.md)toodeploy 新的 Azure 儲存體帳戶。

## <a name="prerequisites"></a>必要條件

toocomplete 本教學課程中，您需要遵循的 hello:

* Azure 訂用帳戶。 如果您沒有這類帳戶，可以[啟用自己的 MSDN 訂戶權益<a href="/pricing/free-account/" target="_blank">或](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/)[註冊免費帳戶](https://azure.microsoft.com/free/)。
* [自動化帳戶](automation-sec-configure-azure-runas-account.md)toohold hello runbook 並驗證 tooAzure 資源。  此帳戶必須具有權限 toostart，停止 hello 虛擬機器。
* [Azure 儲存體帳戶](../storage/common/storage-create-storage-account.md)中哪些 toostore hello Resource Manager 範本
* 本機電腦上安裝的 Azure Powershell。 請參閱[安裝和設定 Azure Powershell](https://docs.microsoft.com/powershell/azure/install-azurerm-ps?view=azurermps-4.1.0)如需有關資訊 tooget Azure PowerShell。

## <a name="create-hello-resource-manager-template"></a>建立 hello Resource Manager 範本

此範例中，我們使用 Resource Manager 範本來部署新的 Azure 儲存體帳戶。

在文字編輯器中，複製下列文字的 hello:

```json
{
  "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
  "contentVersion": "1.0.0.0",
  "parameters": {
    "storageAccountType": {
      "type": "string",
      "defaultValue": "Standard_LRS",
      "allowedValues": [
        "Standard_LRS",
        "Standard_GRS",
        "Standard_ZRS",
        "Premium_LRS"
      ],
      "metadata": {
        "description": "Storage Account type"
      }
    }
  },
  "variables": {
    "storageAccountName": "[concat(uniquestring(resourceGroup().id), 'standardsa')]"
  },
  "resources": [
    {
      "type": "Microsoft.Storage/storageAccounts",
      "name": "[variables('storageAccountName')]",
      "apiVersion": "2016-01-01",
      "location": "[resourceGroup().location]",
      "sku": {
          "name": "[parameters('storageAccountType')]"
      },
      "kind": "Storage", 
      "properties": {
      }
    }
  ],
  "outputs": {
      "storageAccountName": {
          "type": "string",
          "value": "[variables('storageAccountName')]"
      }
  }
}
```

Hello 檔案儲存在本機為`TemplateTest.json`。

## <a name="save-hello-resource-manager-template-in-azure-storage"></a>Azure 儲存體中儲存 hello Resource Manager 範本

現在我們可以使用 PowerShell toocreate 對 Azure 儲存體檔案共用並上傳 hello`TemplateTest.json`檔案。
如需有關如何 toocreate 檔案共用，並上傳 hello Azure 入口網站中的檔案的指示，請參閱[開始使用 Azure 檔案儲存在 Windows 上](../storage/files/storage-dotnet-how-to-use-files.md)。

在您的本機電腦上啟動 PowerShell 並執行下列命令 toocreate 檔案共用的 hello 及上傳 hello 資源管理員範本 toothat 檔案共用。

```powershell
# Login tooAzure
Login-AzureRmAccount

# Get hello access key for your storage account
$key = Get-AzureRmStorageAccountKey -ResourceGroupName 'MyAzureAccount' -Name 'MyStorageAccount'

# Create an Azure Storage context using hello first access key
$context = New-AzureStorageContext -StorageAccountName 'MyStorageAccount' -StorageAccountKey $key[0].value

# Create a file share named 'resource-templates' in your Azure Storage account
$fileShare = New-AzureStorageShare -Name 'resource-templates' -Context $context

# Add hello TemplateTest.json file toohello new file share
# "TemplatePath" is hello path where you saved hello TemplateTest.json file
$templateFile = 'C:\TemplatePath'
Set-AzureStorageFileContent -ShareName $fileShare.Name -Context $context -Source $templateFile
```

## <a name="create-hello-powershell-runbook-script"></a>建立 hello PowerShell runbook 指令碼

現在我們建立的 PowerShell 指令碼，取得 hello`TemplateTest.json`從 Azure 儲存體檔案，並將部署的 hello 範本 toocreate 新的 Azure 儲存體帳戶。

在文字編輯器中，貼上下列文字的 hello:

```powershell
param (
    [Parameter(Mandatory=$true)]
    [string]
    $ResourceGroupName,

    [Parameter(Mandatory=$true)]
    [string]
    $StorageAccountName,

    [Parameter(Mandatory=$true)]
    [string]
    $StorageAccountKey,

    [Parameter(Mandatory=$true)]
    [string]
    $StorageFileName
)



# Authenticate tooAzure if running from Azure Automation
$ServicePrincipalConnection = Get-AutomationConnection -Name "AzureRunAsConnection"
Add-AzureRmAccount `
    -ServicePrincipal `
    -TenantId $ServicePrincipalConnection.TenantId `
    -ApplicationId $ServicePrincipalConnection.ApplicationId `
    -CertificateThumbprint $ServicePrincipalConnection.CertificateThumbprint | Write-Verbose

#Set hello parameter values for hello Resource Manager template
$Parameters = @{
    "storageAccountType"="Standard_LRS"
    }

# Create a new context
$Context = New-AzureStorageContext -StorageAccountKey $StorageAccountKey

Get-AzureStorageFileContent -ShareName 'resource-templates' -Context $Context -path 'TemplateTest.json' -Destination 'C:\Temp'

$TemplateFile = Join-Path -Path 'C:\Temp' -ChildPath $StorageFileName

# Deploy hello storage account
New-AzureRmResourceGroupDeployment -ResourceGroupName $ResourceGroupName -TemplateFile $TemplateFile -TemplateParameterObject $Parameters 
``` 

Hello 檔案儲存在本機為`DeployTemplate.ps1`。

## <a name="import-and-publish-hello-runbook-into-your-azure-automation-account"></a>匯入，並將 hello runbook 發佈至 Azure 自動化帳戶

現在我們到您的 Azure 自動化帳戶，使用 PowerShell tooimport hello runbook，然後發行 hello runbook。
如需有關資訊 tooimport 和 hello Azure 入口網站中發佈 runbook，請參閱[建立或匯入 Azure 自動化中的 runbook](automation-creating-importing-runbook.md)。

tooimport`DeployTemplate.ps1`到您的自動化帳戶作為 PowerShell runbook，請執行下列 PowerShell 命令的 hello:

```powershell
# MyPath is hello path where you saved DeployTemplate.ps1
# MyResourceGroup is hello name of hello Azure ResourceGroup that contains your Azure Automation account
# MyAutomationAccount is hello name of your Automation account
$importParams = @{
    Path = 'C:\MyPath\DeployTemplate.ps1'
    ResourceGroupName = 'MyResourceGroup'
    AutomationAccountName = 'MyAutomationAccount'
    Type = 'PowerShell'
}
Import-AzureRmAutomationRunbook @

# Publish hello runbook
$publishParams = @{
    ResourceGroupName = 'MyResourceGroup'
    AutomationAccountName = 'MyAutomationAccount'
    Name = 'DeployTemplate'
}
Publish-AzureRmAutomationRunbook @publishParams
```

## <a name="start-hello-runbook"></a>啟動 hello runbook

現在我們一開始呼叫 hello hello runbook[開始 AzureRmAutomationRunbook](https://docs.microsoft.com/powershell/module/azurerm.automation/start-azurermautomationrunbook?view=azurermps-4.1.0) cmdlet。

如需如何 toostart hello Azure 入口網站中的 runbook 參閱[Azure 自動化中啟動 runbook](automation-starting-a-runbook.md)。

執行下列命令在 hello PowerShell 主控台中的 hello:

```powershell
# Set up hello parameters for hello runbook
$runbookParams = @{
    ResourceGroupName = 'MyResourceGroup'
    StorageAccountName = 'MyStorageAccount'
    StorageAccountKey = $key[0].Value # We got this key earlier
    StorageFileName = 'TemplateTest.json' 
}

# Set up parameters for hello Start-AzureRmAutomationRunbook cmdlet
$startParams = @{
    ResourceGroupName = 'MyResourceGroup'
    AutomationAccountName = 'MyAutomationAccount'
    Name = 'DeployTemplate'
    Parameters = $runbookParams
}

# Start hello runbook
$job = Start-AzureRmAutomationRunbook @startParams
```

hello runbook 執行時，以及您可以執行來檢查其狀態`$job.Status`。

hello runbook 取得 hello Resource Manager 範本，並使用該 toodeploy 新的 Azure 儲存體帳戶。
您可以看到 hello 新儲存體帳戶由執行下列命令的 hello:
```powershell
Get-AzureRmStorageAccount
```

## <a name="summary"></a>摘要

就這麼簡單！ 現在您可以使用 Azure 自動化和 Azure 儲存體，資源管理員範本 toodeploy 您所有的 Azure 資源。

## <a name="next-steps"></a>後續步驟

* toolearn 進一步了解資源管理員範本，請參閱[Azure 資源管理員概觀](../azure-resource-manager/resource-group-overview.md)
* tooget 開始使用 Azure 儲存體，請參閱[簡介 tooAzure 儲存體](../storage/common/storage-introduction.md)。
* toofind 其他有用的 Azure 自動化 runbook，請參閱[Azure 自動化 Runbook 和模組組件庫](automation-runbook-gallery.md)。
* toofind 其他有用的資源管理員範本，請參閱[Azure 快速入門範本](https://azure.microsoft.com/resources/templates/)

