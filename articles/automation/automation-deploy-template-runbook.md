---
title: "在 Azure 自動化 Runbook 中部署 Azure Resource Manager 範本 | Microsoft Docs"
description: "如何從 Runbook 部署儲存在 Azure 儲存體中的 Azure Resource Manager 範本"
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
ms.openlocfilehash: e511eee2f9eac3969b15ad3d45558dc7034f330a
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="deploy-an-azure-resource-manager-template-in-an-azure-automation-powershell-runbook"></a><span data-ttu-id="3c464-104">在 Azure 自動化 PowerShell Runbook 中部署 Azure Resource Manager 範本</span><span class="sxs-lookup"><span data-stu-id="3c464-104">Deploy an Azure Resource Manager template in an Azure Automation PowerShell runbook</span></span>

<span data-ttu-id="3c464-105">您可以使用 [Azure 資源管理範本](../azure-resource-manager/resource-manager-create-first-template.md)撰寫可部署 Azure 資源的 [Azure 自動化 PowerShell Runbook](automation-first-runbook-textual-powershell.md)。</span><span class="sxs-lookup"><span data-stu-id="3c464-105">You can write an [Azure Automation PowerShell runbook](automation-first-runbook-textual-powershell.md) that deploys an Azure resource by using an [Azure Resource Management template](../azure-resource-manager/resource-manager-create-first-template.md).</span></span>

<span data-ttu-id="3c464-106">如此一來，您就可以自動化部署 Azure 資源。</span><span class="sxs-lookup"><span data-stu-id="3c464-106">By doing this, you can automate deployment of Azure resources.</span></span> <span data-ttu-id="3c464-107">您可以在中央、安全的位置 (例如 Azure 儲存體) 中維護 Resource Manager 範本。</span><span class="sxs-lookup"><span data-stu-id="3c464-107">You can maintain your Resource Manager templates in a central,secure location such as Azure Storage.</span></span>

<span data-ttu-id="3c464-108">在本主題中，我們會建立使用儲存在 [Azure 儲存體](../storage/common/storage-introduction.md)中 Resource Manager 範本的 PowerShell Runbook，來部署新的 Azure 儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="3c464-108">In this topic, we create a PowerShell runbook that uses an Resource Manager template stored in [Azure Storage](../storage/common/storage-introduction.md) to deploy a new Azure Storage account.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="3c464-109">必要條件</span><span class="sxs-lookup"><span data-stu-id="3c464-109">Prerequisites</span></span>

<span data-ttu-id="3c464-110">若要完成此教學課程，您需要下列項目：</span><span class="sxs-lookup"><span data-stu-id="3c464-110">To complete this tutorial, you need the following:</span></span>

* <span data-ttu-id="3c464-111">Azure 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="3c464-111">Azure subscription.</span></span> <span data-ttu-id="3c464-112">如果您沒有這類帳戶，可以[啟用自己的 MSDN 訂戶權益<a href="/pricing/free-account/" target="_blank">或](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/)[註冊免費帳戶](https://azure.microsoft.com/free/)。</span><span class="sxs-lookup"><span data-stu-id="3c464-112">If you don't have one yet, you can [activate your MSDN subscriber benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) or <a href="/pricing/free-account/" target="_blank">[sign up for a free account](https://azure.microsoft.com/free/).</span></span>
* <span data-ttu-id="3c464-113">[自動化帳戶](automation-sec-configure-azure-runas-account.md) ，用來保存 Runbook 以及向 Azure 資源驗證。</span><span class="sxs-lookup"><span data-stu-id="3c464-113">[Automation account](automation-sec-configure-azure-runas-account.md) to hold the runbook and authenticate to Azure resources.</span></span>  <span data-ttu-id="3c464-114">此帳戶必須擁有啟動和停止虛擬機器的權限。</span><span class="sxs-lookup"><span data-stu-id="3c464-114">This account must have permission to start and stop the virtual machine.</span></span>
* <span data-ttu-id="3c464-115">用來儲存 Resource Manager 範本的 [Azure 儲存體帳戶](../storage/common/storage-create-storage-account.md)</span><span class="sxs-lookup"><span data-stu-id="3c464-115">[Azure Storage account](../storage/common/storage-create-storage-account.md) in which to store the Resource Manager template</span></span>
* <span data-ttu-id="3c464-116">本機電腦上安裝的 Azure Powershell。</span><span class="sxs-lookup"><span data-stu-id="3c464-116">Azure Powershell installed on a local machine.</span></span> <span data-ttu-id="3c464-117">如需如何取得 Azure PowerShell 的詳細資訊，請參閱[安裝和設定 Azure PowerShell](https://docs.microsoft.com/powershell/azure/install-azurerm-ps?view=azurermps-4.1.0)。</span><span class="sxs-lookup"><span data-stu-id="3c464-117">See [Install and configure Azure Powershell](https://docs.microsoft.com/powershell/azure/install-azurerm-ps?view=azurermps-4.1.0) for information about how to get Azure PowerShell.</span></span>

## <a name="create-the-resource-manager-template"></a><span data-ttu-id="3c464-118">建立 Resource Manager 範本</span><span class="sxs-lookup"><span data-stu-id="3c464-118">Create the Resource Manager template</span></span>

<span data-ttu-id="3c464-119">此範例中，我們使用 Resource Manager 範本來部署新的 Azure 儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="3c464-119">For this example, we use an Resource Manager template that deploys a new Azure Storage account.</span></span>

<span data-ttu-id="3c464-120">在文字編輯器中，複製下列文字：</span><span class="sxs-lookup"><span data-stu-id="3c464-120">In a text editor, copy the following text:</span></span>

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

<span data-ttu-id="3c464-121">將檔案本機儲存為 `TemplateTest.json`。</span><span class="sxs-lookup"><span data-stu-id="3c464-121">Save the file locally as `TemplateTest.json`.</span></span>

## <a name="save-the-resource-manager-template-in-azure-storage"></a><span data-ttu-id="3c464-122">在 Azure 儲存體中儲存 Resource Manager 範本</span><span class="sxs-lookup"><span data-stu-id="3c464-122">Save the Resource Manager template in Azure Storage</span></span>

<span data-ttu-id="3c464-123">現在我們可以使用 PowerShell 來建立 Azure 儲存體檔案共用，並上傳 `TemplateTest.json` 檔案。</span><span class="sxs-lookup"><span data-stu-id="3c464-123">Now we use PowerShell to create an Azure Storage file share and upload the `TemplateTest.json` file.</span></span>
<span data-ttu-id="3c464-124">如需如何在 Azure 入口網站建立檔案共用並上傳檔案的指示，請參閱[在 Windows 上開始使用 Azure 檔案儲存體](../storage/files/storage-dotnet-how-to-use-files.md)。</span><span class="sxs-lookup"><span data-stu-id="3c464-124">For instructions on how to create a file share and upload a file in the Azure portal, see [Get started with Azure File storage on Windows](../storage/files/storage-dotnet-how-to-use-files.md).</span></span>

<span data-ttu-id="3c464-125">在您的本機電腦上啟動 PowerShell 並執行下列命令，可建立檔案共用，並將 Resource Manager 範本上傳至該檔案共用。</span><span class="sxs-lookup"><span data-stu-id="3c464-125">Launch PowerShell on your local machine, and run the following commands to create a file share and upload the Resource Manager template to that file share.</span></span>

```powershell
# Login to Azure
Login-AzureRmAccount

# Get the access key for your storage account
$key = Get-AzureRmStorageAccountKey -ResourceGroupName 'MyAzureAccount' -Name 'MyStorageAccount'

# Create an Azure Storage context using the first access key
$context = New-AzureStorageContext -StorageAccountName 'MyStorageAccount' -StorageAccountKey $key[0].value

# Create a file share named 'resource-templates' in your Azure Storage account
$fileShare = New-AzureStorageShare -Name 'resource-templates' -Context $context

# Add the TemplateTest.json file to the new file share
# "TemplatePath" is the path where you saved the TemplateTest.json file
$templateFile = 'C:\TemplatePath'
Set-AzureStorageFileContent -ShareName $fileShare.Name -Context $context -Source $templateFile
```

## <a name="create-the-powershell-runbook-script"></a><span data-ttu-id="3c464-126">建立 PowerShell Runbook 指令碼</span><span class="sxs-lookup"><span data-stu-id="3c464-126">Create the PowerShell runbook script</span></span>

<span data-ttu-id="3c464-127">現在我們建立的 PowerShell 指令碼，會從 Azure 儲存體取得 `TemplateTest.json` 檔案，並部署範本來建立新的 Azure 儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="3c464-127">Now we create a PowerShell script that gets the `TemplateTest.json` file from Azure Storage and deploys the template to create a new Azure Storage account.</span></span>

<span data-ttu-id="3c464-128">在文字編輯器中，貼上下列文字：</span><span class="sxs-lookup"><span data-stu-id="3c464-128">In a text editor, paste the following text:</span></span>

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



# Authenticate to Azure if running from Azure Automation
$ServicePrincipalConnection = Get-AutomationConnection -Name "AzureRunAsConnection"
Add-AzureRmAccount `
    -ServicePrincipal `
    -TenantId $ServicePrincipalConnection.TenantId `
    -ApplicationId $ServicePrincipalConnection.ApplicationId `
    -CertificateThumbprint $ServicePrincipalConnection.CertificateThumbprint | Write-Verbose

#Set the parameter values for the Resource Manager template
$Parameters = @{
    "storageAccountType"="Standard_LRS"
    }

# Create a new context
$Context = New-AzureStorageContext -StorageAccountKey $StorageAccountKey

Get-AzureStorageFileContent -ShareName 'resource-templates' -Context $Context -path 'TemplateTest.json' -Destination 'C:\Temp'

$TemplateFile = Join-Path -Path 'C:\Temp' -ChildPath $StorageFileName

# Deploy the storage account
New-AzureRmResourceGroupDeployment -ResourceGroupName $ResourceGroupName -TemplateFile $TemplateFile -TemplateParameterObject $Parameters 
``` 

<span data-ttu-id="3c464-129">將檔案本機儲存為 `DeployTemplate.ps1`。</span><span class="sxs-lookup"><span data-stu-id="3c464-129">Save the file locally as `DeployTemplate.ps1`.</span></span>

## <a name="import-and-publish-the-runbook-into-your-azure-automation-account"></a><span data-ttu-id="3c464-130">將 Runbook 匯入您的 Azure 自動化帳戶並加以發佈</span><span class="sxs-lookup"><span data-stu-id="3c464-130">Import and publish the runbook into your Azure Automation account</span></span>

<span data-ttu-id="3c464-131">現在，我們會使用 PowerShell 將 Runbook 匯入您的 Azure 自動化帳戶，然後發佈 Runbook。</span><span class="sxs-lookup"><span data-stu-id="3c464-131">Now we use PowerShell to import the runbook into your Azure Automation account, and then publish the runbook.</span></span>
<span data-ttu-id="3c464-132">如需關於如何在 Azure 入口網站中匯入並發佈 Runbook 的資訊，請參閱[在 Azure 自動化中建立或匯入 Runbook](automation-creating-importing-runbook.md)。</span><span class="sxs-lookup"><span data-stu-id="3c464-132">For information about how to import and publish a runbook in the Azure portal, see [Creating or importing a runbook in Azure Automation](automation-creating-importing-runbook.md).</span></span>

<span data-ttu-id="3c464-133">若要將 `DeployTemplate.ps1` 匯入您的自動化帳戶中作為 PowerShell Runbook，請執行下列 PowerShell 命令：</span><span class="sxs-lookup"><span data-stu-id="3c464-133">To import `DeployTemplate.ps1` into your Automation account as a PowerShell runbook, run the following PowerShell commands:</span></span>

```powershell
# MyPath is the path where you saved DeployTemplate.ps1
# MyResourceGroup is the name of the Azure ResourceGroup that contains your Azure Automation account
# MyAutomationAccount is the name of your Automation account
$importParams = @{
    Path = 'C:\MyPath\DeployTemplate.ps1'
    ResourceGroupName = 'MyResourceGroup'
    AutomationAccountName = 'MyAutomationAccount'
    Type = 'PowerShell'
}
Import-AzureRmAutomationRunbook @

# Publish the runbook
$publishParams = @{
    ResourceGroupName = 'MyResourceGroup'
    AutomationAccountName = 'MyAutomationAccount'
    Name = 'DeployTemplate'
}
Publish-AzureRmAutomationRunbook @publishParams
```

## <a name="start-the-runbook"></a><span data-ttu-id="3c464-134">啟動 Runbook</span><span class="sxs-lookup"><span data-stu-id="3c464-134">Start the runbook</span></span>

<span data-ttu-id="3c464-135">現在我們會呼叫 [Start-AzureRmAutomationRunbook](https://docs.microsoft.com/powershell/module/azurerm.automation/start-azurermautomationrunbook?view=azurermps-4.1.0) Cmdlet 來啟動 Runbook。</span><span class="sxs-lookup"><span data-stu-id="3c464-135">Now we start the runbook by calling the [Start-AzureRmAutomationRunbook](https://docs.microsoft.com/powershell/module/azurerm.automation/start-azurermautomationrunbook?view=azurermps-4.1.0) cmdlet.</span></span>

<span data-ttu-id="3c464-136">如需關於如何在 Azure 入口網站中啟動 Runbook 的資訊，請參閱[在 Azure 自動化中啟動 Runbook](automation-starting-a-runbook.md)。</span><span class="sxs-lookup"><span data-stu-id="3c464-136">For information about how to start a runbook in the Azure portal, see [Starting a runbook in Azure Automation](automation-starting-a-runbook.md).</span></span>

<span data-ttu-id="3c464-137">在 PowerShell 主控台中執行下列命令：</span><span class="sxs-lookup"><span data-stu-id="3c464-137">Run the following commands in the PowerShell console:</span></span>

```powershell
# Set up the parameters for the runbook
$runbookParams = @{
    ResourceGroupName = 'MyResourceGroup'
    StorageAccountName = 'MyStorageAccount'
    StorageAccountKey = $key[0].Value # We got this key earlier
    StorageFileName = 'TemplateTest.json' 
}

# Set up parameters for the Start-AzureRmAutomationRunbook cmdlet
$startParams = @{
    ResourceGroupName = 'MyResourceGroup'
    AutomationAccountName = 'MyAutomationAccount'
    Name = 'DeployTemplate'
    Parameters = $runbookParams
}

# Start the runbook
$job = Start-AzureRmAutomationRunbook @startParams
```

<span data-ttu-id="3c464-138">Runbook 執行時，您可以執行 `$job.Status` 來檢查其狀態。</span><span class="sxs-lookup"><span data-stu-id="3c464-138">The runbook runs, and you can check its status by running `$job.Status`.</span></span>

<span data-ttu-id="3c464-139">Runbook 會取得 Resource Manager 範本，並使用它來部署新的 Azure 儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="3c464-139">The runbook gets the Resource Manager template and uses it to deploy a new Azure Storage account.</span></span>
<span data-ttu-id="3c464-140">您可以執行下列命令來看到建立的新儲存體帳戶：</span><span class="sxs-lookup"><span data-stu-id="3c464-140">You can see that the new storage account was created by running the following command:</span></span>
```powershell
Get-AzureRmStorageAccount
```

## <a name="summary"></a><span data-ttu-id="3c464-141">摘要</span><span class="sxs-lookup"><span data-stu-id="3c464-141">Summary</span></span>

<span data-ttu-id="3c464-142">就這麼簡單！</span><span class="sxs-lookup"><span data-stu-id="3c464-142">That's it!</span></span> <span data-ttu-id="3c464-143">現在您可以使用 Azure 自動化和 Azure 儲存體，以及 Resource Manager 範本來部署您所有的 Azure 資源。</span><span class="sxs-lookup"><span data-stu-id="3c464-143">Now you can use Azure Automation and Azure Storage, and Resource Manager templates to deploy all your Azure resources.</span></span>

## <a name="next-steps"></a><span data-ttu-id="3c464-144">後續步驟</span><span class="sxs-lookup"><span data-stu-id="3c464-144">Next steps</span></span>

* <span data-ttu-id="3c464-145">若要深入了解 Resource Manager 範本，請參閱 [Azure Resource Manager 概觀](../azure-resource-manager/resource-group-overview.md)</span><span class="sxs-lookup"><span data-stu-id="3c464-145">To learn more about Resource Manager templates, see [Azure Resource Manager overview](../azure-resource-manager/resource-group-overview.md)</span></span>
* <span data-ttu-id="3c464-146">若要開始使用 Azure 儲存體，請參閱 [Azure 儲存體簡介](../storage/common/storage-introduction.md)。</span><span class="sxs-lookup"><span data-stu-id="3c464-146">To get started with Azure Storage, see [Introduction to Azure Storage](../storage/common/storage-introduction.md).</span></span>
* <span data-ttu-id="3c464-147">若要尋找其他實用的 Azure 自動化 Runbook，請參閱 [Azure 自動化的 Runbook 和模組資源庫](automation-runbook-gallery.md)。</span><span class="sxs-lookup"><span data-stu-id="3c464-147">To find other useful Azure Automation runbooks, see [Runbook and module galleries for Azure Automation](automation-runbook-gallery.md).</span></span>
* <span data-ttu-id="3c464-148">若要尋找其他實用的 Resource Manager 範本，請參閱 [Azure 快速入門範本](https://azure.microsoft.com/resources/templates/)</span><span class="sxs-lookup"><span data-stu-id="3c464-148">To find other useful Resource Manager templates, see [Azure Quickstart Templates](https://azure.microsoft.com/resources/templates/)</span></span>

