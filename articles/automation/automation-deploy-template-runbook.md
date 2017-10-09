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
# <a name="deploy-an-azure-resource-manager-template-in-an-azure-automation-powershell-runbook"></a><span data-ttu-id="1fc76-104">在 Azure 自動化 PowerShell Runbook 中部署 Azure Resource Manager 範本</span><span class="sxs-lookup"><span data-stu-id="1fc76-104">Deploy an Azure Resource Manager template in an Azure Automation PowerShell runbook</span></span>

<span data-ttu-id="1fc76-105">您可以使用 [Azure 資源管理範本](../azure-resource-manager/resource-manager-create-first-template.md)撰寫可部署 Azure 資源的 [Azure 自動化 PowerShell Runbook](automation-first-runbook-textual-powershell.md)。</span><span class="sxs-lookup"><span data-stu-id="1fc76-105">You can write an [Azure Automation PowerShell runbook](automation-first-runbook-textual-powershell.md) that deploys an Azure resource by using an [Azure Resource Management template](../azure-resource-manager/resource-manager-create-first-template.md).</span></span>

<span data-ttu-id="1fc76-106">如此一來，您就可以自動化部署 Azure 資源。</span><span class="sxs-lookup"><span data-stu-id="1fc76-106">By doing this, you can automate deployment of Azure resources.</span></span> <span data-ttu-id="1fc76-107">您可以在中央、安全的位置 (例如 Azure 儲存體) 中維護 Resource Manager 範本。</span><span class="sxs-lookup"><span data-stu-id="1fc76-107">You can maintain your Resource Manager templates in a central,secure location such as Azure Storage.</span></span>

<span data-ttu-id="1fc76-108">在本主題中，我們會建立使用儲存在資源管理員範本的 PowerShell runbook [Azure 儲存體](../storage/common/storage-introduction.md)toodeploy 新的 Azure 儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="1fc76-108">In this topic, we create a PowerShell runbook that uses an Resource Manager template stored in [Azure Storage](../storage/common/storage-introduction.md) toodeploy a new Azure Storage account.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="1fc76-109">必要條件</span><span class="sxs-lookup"><span data-stu-id="1fc76-109">Prerequisites</span></span>

<span data-ttu-id="1fc76-110">toocomplete 本教學課程中，您需要遵循的 hello:</span><span class="sxs-lookup"><span data-stu-id="1fc76-110">toocomplete this tutorial, you need hello following:</span></span>

* <span data-ttu-id="1fc76-111">Azure 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="1fc76-111">Azure subscription.</span></span> <span data-ttu-id="1fc76-112">如果您沒有這類帳戶，可以[啟用自己的 MSDN 訂戶權益<a href="/pricing/free-account/" target="_blank">或](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/)[註冊免費帳戶](https://azure.microsoft.com/free/)。</span><span class="sxs-lookup"><span data-stu-id="1fc76-112">If you don't have one yet, you can [activate your MSDN subscriber benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) or <a href="/pricing/free-account/" target="_blank">[sign up for a free account](https://azure.microsoft.com/free/).</span></span>
* <span data-ttu-id="1fc76-113">[自動化帳戶](automation-sec-configure-azure-runas-account.md)toohold hello runbook 並驗證 tooAzure 資源。</span><span class="sxs-lookup"><span data-stu-id="1fc76-113">[Automation account](automation-sec-configure-azure-runas-account.md) toohold hello runbook and authenticate tooAzure resources.</span></span>  <span data-ttu-id="1fc76-114">此帳戶必須具有權限 toostart，停止 hello 虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="1fc76-114">This account must have permission toostart and stop hello virtual machine.</span></span>
* <span data-ttu-id="1fc76-115">[Azure 儲存體帳戶](../storage/common/storage-create-storage-account.md)中哪些 toostore hello Resource Manager 範本</span><span class="sxs-lookup"><span data-stu-id="1fc76-115">[Azure Storage account](../storage/common/storage-create-storage-account.md) in which toostore hello Resource Manager template</span></span>
* <span data-ttu-id="1fc76-116">本機電腦上安裝的 Azure Powershell。</span><span class="sxs-lookup"><span data-stu-id="1fc76-116">Azure Powershell installed on a local machine.</span></span> <span data-ttu-id="1fc76-117">請參閱[安裝和設定 Azure Powershell](https://docs.microsoft.com/powershell/azure/install-azurerm-ps?view=azurermps-4.1.0)如需有關資訊 tooget Azure PowerShell。</span><span class="sxs-lookup"><span data-stu-id="1fc76-117">See [Install and configure Azure Powershell](https://docs.microsoft.com/powershell/azure/install-azurerm-ps?view=azurermps-4.1.0) for information about how tooget Azure PowerShell.</span></span>

## <a name="create-hello-resource-manager-template"></a><span data-ttu-id="1fc76-118">建立 hello Resource Manager 範本</span><span class="sxs-lookup"><span data-stu-id="1fc76-118">Create hello Resource Manager template</span></span>

<span data-ttu-id="1fc76-119">此範例中，我們使用 Resource Manager 範本來部署新的 Azure 儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="1fc76-119">For this example, we use an Resource Manager template that deploys a new Azure Storage account.</span></span>

<span data-ttu-id="1fc76-120">在文字編輯器中，複製下列文字的 hello:</span><span class="sxs-lookup"><span data-stu-id="1fc76-120">In a text editor, copy hello following text:</span></span>

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

<span data-ttu-id="1fc76-121">Hello 檔案儲存在本機為`TemplateTest.json`。</span><span class="sxs-lookup"><span data-stu-id="1fc76-121">Save hello file locally as `TemplateTest.json`.</span></span>

## <a name="save-hello-resource-manager-template-in-azure-storage"></a><span data-ttu-id="1fc76-122">Azure 儲存體中儲存 hello Resource Manager 範本</span><span class="sxs-lookup"><span data-stu-id="1fc76-122">Save hello Resource Manager template in Azure Storage</span></span>

<span data-ttu-id="1fc76-123">現在我們可以使用 PowerShell toocreate 對 Azure 儲存體檔案共用並上傳 hello`TemplateTest.json`檔案。</span><span class="sxs-lookup"><span data-stu-id="1fc76-123">Now we use PowerShell toocreate an Azure Storage file share and upload hello `TemplateTest.json` file.</span></span>
<span data-ttu-id="1fc76-124">如需有關如何 toocreate 檔案共用，並上傳 hello Azure 入口網站中的檔案的指示，請參閱[開始使用 Azure 檔案儲存在 Windows 上](../storage/files/storage-dotnet-how-to-use-files.md)。</span><span class="sxs-lookup"><span data-stu-id="1fc76-124">For instructions on how toocreate a file share and upload a file in hello Azure portal, see [Get started with Azure File storage on Windows](../storage/files/storage-dotnet-how-to-use-files.md).</span></span>

<span data-ttu-id="1fc76-125">在您的本機電腦上啟動 PowerShell 並執行下列命令 toocreate 檔案共用的 hello 及上傳 hello 資源管理員範本 toothat 檔案共用。</span><span class="sxs-lookup"><span data-stu-id="1fc76-125">Launch PowerShell on your local machine, and run hello following commands toocreate a file share and upload hello Resource Manager template toothat file share.</span></span>

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

## <a name="create-hello-powershell-runbook-script"></a><span data-ttu-id="1fc76-126">建立 hello PowerShell runbook 指令碼</span><span class="sxs-lookup"><span data-stu-id="1fc76-126">Create hello PowerShell runbook script</span></span>

<span data-ttu-id="1fc76-127">現在我們建立的 PowerShell 指令碼，取得 hello`TemplateTest.json`從 Azure 儲存體檔案，並將部署的 hello 範本 toocreate 新的 Azure 儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="1fc76-127">Now we create a PowerShell script that gets hello `TemplateTest.json` file from Azure Storage and deploys hello template toocreate a new Azure Storage account.</span></span>

<span data-ttu-id="1fc76-128">在文字編輯器中，貼上下列文字的 hello:</span><span class="sxs-lookup"><span data-stu-id="1fc76-128">In a text editor, paste hello following text:</span></span>

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

<span data-ttu-id="1fc76-129">Hello 檔案儲存在本機為`DeployTemplate.ps1`。</span><span class="sxs-lookup"><span data-stu-id="1fc76-129">Save hello file locally as `DeployTemplate.ps1`.</span></span>

## <a name="import-and-publish-hello-runbook-into-your-azure-automation-account"></a><span data-ttu-id="1fc76-130">匯入，並將 hello runbook 發佈至 Azure 自動化帳戶</span><span class="sxs-lookup"><span data-stu-id="1fc76-130">Import and publish hello runbook into your Azure Automation account</span></span>

<span data-ttu-id="1fc76-131">現在我們到您的 Azure 自動化帳戶，使用 PowerShell tooimport hello runbook，然後發行 hello runbook。</span><span class="sxs-lookup"><span data-stu-id="1fc76-131">Now we use PowerShell tooimport hello runbook into your Azure Automation account, and then publish hello runbook.</span></span>
<span data-ttu-id="1fc76-132">如需有關資訊 tooimport 和 hello Azure 入口網站中發佈 runbook，請參閱[建立或匯入 Azure 自動化中的 runbook](automation-creating-importing-runbook.md)。</span><span class="sxs-lookup"><span data-stu-id="1fc76-132">For information about how tooimport and publish a runbook in hello Azure portal, see [Creating or importing a runbook in Azure Automation](automation-creating-importing-runbook.md).</span></span>

<span data-ttu-id="1fc76-133">tooimport`DeployTemplate.ps1`到您的自動化帳戶作為 PowerShell runbook，請執行下列 PowerShell 命令的 hello:</span><span class="sxs-lookup"><span data-stu-id="1fc76-133">tooimport `DeployTemplate.ps1` into your Automation account as a PowerShell runbook, run hello following PowerShell commands:</span></span>

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

## <a name="start-hello-runbook"></a><span data-ttu-id="1fc76-134">啟動 hello runbook</span><span class="sxs-lookup"><span data-stu-id="1fc76-134">Start hello runbook</span></span>

<span data-ttu-id="1fc76-135">現在我們一開始呼叫 hello hello runbook[開始 AzureRmAutomationRunbook](https://docs.microsoft.com/powershell/module/azurerm.automation/start-azurermautomationrunbook?view=azurermps-4.1.0) cmdlet。</span><span class="sxs-lookup"><span data-stu-id="1fc76-135">Now we start hello runbook by calling hello [Start-AzureRmAutomationRunbook](https://docs.microsoft.com/powershell/module/azurerm.automation/start-azurermautomationrunbook?view=azurermps-4.1.0) cmdlet.</span></span>

<span data-ttu-id="1fc76-136">如需如何 toostart hello Azure 入口網站中的 runbook 參閱[Azure 自動化中啟動 runbook](automation-starting-a-runbook.md)。</span><span class="sxs-lookup"><span data-stu-id="1fc76-136">For information about how toostart a runbook in hello Azure portal, see [Starting a runbook in Azure Automation](automation-starting-a-runbook.md).</span></span>

<span data-ttu-id="1fc76-137">執行下列命令在 hello PowerShell 主控台中的 hello:</span><span class="sxs-lookup"><span data-stu-id="1fc76-137">Run hello following commands in hello PowerShell console:</span></span>

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

<span data-ttu-id="1fc76-138">hello runbook 執行時，以及您可以執行來檢查其狀態`$job.Status`。</span><span class="sxs-lookup"><span data-stu-id="1fc76-138">hello runbook runs, and you can check its status by running `$job.Status`.</span></span>

<span data-ttu-id="1fc76-139">hello runbook 取得 hello Resource Manager 範本，並使用該 toodeploy 新的 Azure 儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="1fc76-139">hello runbook gets hello Resource Manager template and uses it toodeploy a new Azure Storage account.</span></span>
<span data-ttu-id="1fc76-140">您可以看到 hello 新儲存體帳戶由執行下列命令的 hello:</span><span class="sxs-lookup"><span data-stu-id="1fc76-140">You can see that hello new storage account was created by running hello following command:</span></span>
```powershell
Get-AzureRmStorageAccount
```

## <a name="summary"></a><span data-ttu-id="1fc76-141">摘要</span><span class="sxs-lookup"><span data-stu-id="1fc76-141">Summary</span></span>

<span data-ttu-id="1fc76-142">就這麼簡單！</span><span class="sxs-lookup"><span data-stu-id="1fc76-142">That's it!</span></span> <span data-ttu-id="1fc76-143">現在您可以使用 Azure 自動化和 Azure 儲存體，資源管理員範本 toodeploy 您所有的 Azure 資源。</span><span class="sxs-lookup"><span data-stu-id="1fc76-143">Now you can use Azure Automation and Azure Storage, and Resource Manager templates toodeploy all your Azure resources.</span></span>

## <a name="next-steps"></a><span data-ttu-id="1fc76-144">後續步驟</span><span class="sxs-lookup"><span data-stu-id="1fc76-144">Next steps</span></span>

* <span data-ttu-id="1fc76-145">toolearn 進一步了解資源管理員範本，請參閱[Azure 資源管理員概觀](../azure-resource-manager/resource-group-overview.md)</span><span class="sxs-lookup"><span data-stu-id="1fc76-145">toolearn more about Resource Manager templates, see [Azure Resource Manager overview](../azure-resource-manager/resource-group-overview.md)</span></span>
* <span data-ttu-id="1fc76-146">tooget 開始使用 Azure 儲存體，請參閱[簡介 tooAzure 儲存體](../storage/common/storage-introduction.md)。</span><span class="sxs-lookup"><span data-stu-id="1fc76-146">tooget started with Azure Storage, see [Introduction tooAzure Storage](../storage/common/storage-introduction.md).</span></span>
* <span data-ttu-id="1fc76-147">toofind 其他有用的 Azure 自動化 runbook，請參閱[Azure 自動化 Runbook 和模組組件庫](automation-runbook-gallery.md)。</span><span class="sxs-lookup"><span data-stu-id="1fc76-147">toofind other useful Azure Automation runbooks, see [Runbook and module galleries for Azure Automation](automation-runbook-gallery.md).</span></span>
* <span data-ttu-id="1fc76-148">toofind 其他有用的資源管理員範本，請參閱[Azure 快速入門範本](https://azure.microsoft.com/resources/templates/)</span><span class="sxs-lookup"><span data-stu-id="1fc76-148">toofind other useful Resource Manager templates, see [Azure Quickstart Templates](https://azure.microsoft.com/resources/templates/)</span></span>

