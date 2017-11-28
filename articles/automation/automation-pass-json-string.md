---
title: "aaaPass JSON 物件 tooan Azure 自動化 runbook |Microsoft 文件"
description: "如何 toopass 參數 tooa runbook 以 JSON 物件"
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
ms.date: 06/15/2017
ms.author: eslesar
ms.openlocfilehash: 8229a16015d549927ead5496c70e9fb391d35498
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="pass-a-json-object-tooan-azure-automation-runbook"></a><span data-ttu-id="d273b-104">傳遞 JSON 物件 tooan Azure 自動化 runbook</span><span class="sxs-lookup"><span data-stu-id="d273b-104">Pass a JSON object tooan Azure Automation runbook</span></span>

<span data-ttu-id="d273b-105">它可以是您想要在 JSON 檔案中的 toopass tooa runbook 的實用 toostore 資料。</span><span class="sxs-lookup"><span data-stu-id="d273b-105">It can be useful toostore data that you want toopass tooa runbook in a JSON file.</span></span>
<span data-ttu-id="d273b-106">例如，您可能會建立包含所有 hello 參數的 JSON 檔案想 toopass tooa runbook。</span><span class="sxs-lookup"><span data-stu-id="d273b-106">For example, you might create a JSON file that contains all of hello parameters you want toopass tooa runbook.</span></span>
<span data-ttu-id="d273b-107">toodo，您有 tooconvert hello JSON tooa 字串，然後將傳遞其內容 toohello runbook 之前的轉換 hello 字串 tooa PowerShell 物件。</span><span class="sxs-lookup"><span data-stu-id="d273b-107">toodo this, you have tooconvert hello JSON tooa string and then convert hello string tooa PowerShell object before passing its contents toohello runbook.</span></span>

<span data-ttu-id="d273b-108">在此範例中，我們將建立 PowerShell 指令碼中呼叫[開始 AzureRmAutomationRunbook](https://msdn.microsoft.com/library/mt603661.aspx) toostart PowerShell runbook，傳遞 hello hello JSON toohello runbook 內容。</span><span class="sxs-lookup"><span data-stu-id="d273b-108">In this example, we'll create a PowerShell script that calls [Start-AzureRmAutomationRunbook](https://msdn.microsoft.com/library/mt603661.aspx) toostart a PowerShell runbook, passing hello contents of hello JSON toohello runbook.</span></span>
<span data-ttu-id="d273b-109">hello PowerShell runbook 啟動 Azure VM 中，從 hello 傳入的 JSON 取得 hello VM hello 參數。</span><span class="sxs-lookup"><span data-stu-id="d273b-109">hello PowerShell runbook starts an Azure VM, getting hello parameters for hello VM from hello JSON that was passed in.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d273b-110">必要條件</span><span class="sxs-lookup"><span data-stu-id="d273b-110">Prerequisites</span></span>
<span data-ttu-id="d273b-111">toocomplete 本教學課程中，您需要遵循的 hello:</span><span class="sxs-lookup"><span data-stu-id="d273b-111">toocomplete this tutorial, you need hello following:</span></span>

* <span data-ttu-id="d273b-112">Azure 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="d273b-112">Azure subscription.</span></span> <span data-ttu-id="d273b-113">如果您沒有這類帳戶，可以[啟用自己的 MSDN 訂戶權益<a href="/pricing/free-account/" target="_blank">或](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/)[註冊免費帳戶](https://azure.microsoft.com/free/)。</span><span class="sxs-lookup"><span data-stu-id="d273b-113">If you don't have one yet, you can [activate your MSDN subscriber benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) or <a href="/pricing/free-account/" target="_blank">[sign up for a free account](https://azure.microsoft.com/free/).</span></span>
* <span data-ttu-id="d273b-114">[自動化帳戶](automation-sec-configure-azure-runas-account.md)toohold hello runbook 並驗證 tooAzure 資源。</span><span class="sxs-lookup"><span data-stu-id="d273b-114">[Automation account](automation-sec-configure-azure-runas-account.md) toohold hello runbook and authenticate tooAzure resources.</span></span>  <span data-ttu-id="d273b-115">此帳戶必須具有權限 toostart，停止 hello 虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="d273b-115">This account must have permission toostart and stop hello virtual machine.</span></span>
* <span data-ttu-id="d273b-116">Azure 虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="d273b-116">An Azure virtual machine.</span></span> <span data-ttu-id="d273b-117">我們會停止並啟動這部電腦，因此它不該是生產 VM。</span><span class="sxs-lookup"><span data-stu-id="d273b-117">We stop and start this machine so it should not be a production VM.</span></span>
* <span data-ttu-id="d273b-118">本機電腦上安裝的 Azure Powershell。</span><span class="sxs-lookup"><span data-stu-id="d273b-118">Azure Powershell installed on a local machine.</span></span> <span data-ttu-id="d273b-119">請參閱[安裝和設定 Azure Powershell](https://docs.microsoft.com/powershell/azure/install-azurerm-ps?view=azurermps-4.1.0)如需有關資訊 tooget Azure PowerShell。</span><span class="sxs-lookup"><span data-stu-id="d273b-119">See [Install and configure Azure Powershell](https://docs.microsoft.com/powershell/azure/install-azurerm-ps?view=azurermps-4.1.0) for information about how tooget Azure PowerShell.</span></span>

## <a name="create-hello-json-file"></a><span data-ttu-id="d273b-120">建立 hello JSON 檔案</span><span class="sxs-lookup"><span data-stu-id="d273b-120">Create hello JSON file</span></span>

<span data-ttu-id="d273b-121">輸入 hello 下列測試在文字檔案，並將它儲存成`test.json`本機電腦上的某個地方。</span><span class="sxs-lookup"><span data-stu-id="d273b-121">Type hello following test in a text file, and save it as `test.json` somewhere on your local computer.</span></span>

```json
{
   "VmName" : "TestVM",
   "ResourceGroup" : "AzureAutomationTest"
}
```

## <a name="create-hello-runbook"></a><span data-ttu-id="d273b-122">建立 hello runbook</span><span class="sxs-lookup"><span data-stu-id="d273b-122">Create hello runbook</span></span>

<span data-ttu-id="d273b-123">在 Azure 自動化中建立名為 "Test-Json" 的新 PowerShell Runbook。</span><span class="sxs-lookup"><span data-stu-id="d273b-123">Create a new PowerShell runbook named "Test-Json" in Azure Automation.</span></span>
<span data-ttu-id="d273b-124">如何 toocreate 新的 PowerShell runbook，請參閱的 toolearn[我的第一個 PowerShell runbook](automation-first-runbook-textual-powershell.md)。</span><span class="sxs-lookup"><span data-stu-id="d273b-124">toolearn how toocreate a new PowerShell runbook, see [My first PowerShell runbook](automation-first-runbook-textual-powershell.md).</span></span>

<span data-ttu-id="d273b-125">tooaccept hello JSON 資料，hello runbook 必須採用物件作為輸入參數。</span><span class="sxs-lookup"><span data-stu-id="d273b-125">tooaccept hello JSON data, hello runbook must take an object as an input parameter.</span></span>

<span data-ttu-id="d273b-126">hello runbook 可以接著使用 hello hello JSON 中定義的屬性。</span><span class="sxs-lookup"><span data-stu-id="d273b-126">hello runbook can then use hello properties defined in hello JSON.</span></span>

```powershell
Param(
     [parameter(Mandatory=$true)]
     [object]$json
)

# Connect tooAzure account   
$Conn = Get-AutomationConnection -Name AzureRunAsConnection
Add-AzureRMAccount -ServicePrincipal -Tenant $Conn.TenantID `
    -ApplicationID $Conn.ApplicationID -CertificateThumbprint $Conn.CertificateThumbprint

# Convert object tooactual JSON
$json = $json | ConvertFrom-Json

# Use hello values from hello JSON object as hello parameters for your command
Start-AzureRmVM -Name $json.VMName -ResourceGroupName $json.ResourceGroup
 ```

 <span data-ttu-id="d273b-127">在您的自動化帳戶中儲存並發佈此 Runbook。</span><span class="sxs-lookup"><span data-stu-id="d273b-127">Save and publish this runbook in your Automation account.</span></span>

## <a name="call-hello-runbook-from-powershell"></a><span data-ttu-id="d273b-128">從 PowerShell 呼叫 hello runbook</span><span class="sxs-lookup"><span data-stu-id="d273b-128">Call hello runbook from PowerShell</span></span>

<span data-ttu-id="d273b-129">現在您可以使用 Azure PowerShell，從本機電腦呼叫 hello runbook。</span><span class="sxs-lookup"><span data-stu-id="d273b-129">Now you can call hello runbook from your local machine by using Azure PowerShell.</span></span>
<span data-ttu-id="d273b-130">執行下列 PowerShell 命令的 hello:</span><span class="sxs-lookup"><span data-stu-id="d273b-130">Run hello following PowerShell commands:</span></span>

1. <span data-ttu-id="d273b-131">登入 tooAzure:</span><span class="sxs-lookup"><span data-stu-id="d273b-131">Log in tooAzure:</span></span>
   ```powershell
   Login-AzureRmAccount
   ```
    <span data-ttu-id="d273b-132">您會提示的 tooenter 您的 Azure 認證。</span><span class="sxs-lookup"><span data-stu-id="d273b-132">You are prompted tooenter your Azure credentials.</span></span>
1. <span data-ttu-id="d273b-133">取得 hello hello JSON 檔案內容，並將它轉換 tooa 字串：</span><span class="sxs-lookup"><span data-stu-id="d273b-133">Get hello contents of hello JSON file and convert it tooa string:</span></span>
    ```powershell
    $json =  (Get-content -path 'JsonPath\test.json' -Raw) | Out-string
    ```
    <span data-ttu-id="d273b-134">`JsonPath`是 hello hello JSON 檔案的儲存位置的路徑。</span><span class="sxs-lookup"><span data-stu-id="d273b-134">`JsonPath` is hello path where you saved hello JSON file.</span></span>
1. <span data-ttu-id="d273b-135">轉換字串內容 hello `$json` tooa PowerShell 物件：</span><span class="sxs-lookup"><span data-stu-id="d273b-135">Convert hello string contents of `$json` tooa PowerShell object:</span></span>
   ```powershell
   $JsonParams = @{"json"=$json}
   ```
1. <span data-ttu-id="d273b-136">建立雜湊表 hello 參數`Start-AzureRmAutomstionRunbook`:</span><span class="sxs-lookup"><span data-stu-id="d273b-136">Create a hashtable for hello parameters for `Start-AzureRmAutomstionRunbook`:</span></span>
   ```powershell
   $RBParams = @{
        AutomationAccountName = 'AATest'
        ResourceGroupName = 'RGTest'
        Name = 'Test-Json'
        Parameters = $JsonParams
   }
   ```
   <span data-ttu-id="d273b-137">請注意，您要設定的 hello 值`Parameters`toohello PowerShell 物件，其中包含 hello JSON 檔案中的 hello 值。</span><span class="sxs-lookup"><span data-stu-id="d273b-137">Notice that you are setting hello value of `Parameters` toohello PowerShell object that contains hello values from hello JSON file.</span></span> 
1. <span data-ttu-id="d273b-138">啟動 hello runbook</span><span class="sxs-lookup"><span data-stu-id="d273b-138">Start hello runbook</span></span>
   ```powershell
   $job = Start-AzureRmAutomationRunbook @RBParams
   ```

<span data-ttu-id="d273b-139">hello runbook 會使用 hello JSON 檔案 toostart VM hello 值。</span><span class="sxs-lookup"><span data-stu-id="d273b-139">hello runbook uses hello values from hello JSON file toostart a VM.</span></span>

## <a name="next-steps"></a><span data-ttu-id="d273b-140">後續步驟</span><span class="sxs-lookup"><span data-stu-id="d273b-140">Next steps</span></span>

* <span data-ttu-id="d273b-141">進一步了解使用文字編輯器，編輯 PowerShell 和 PowerShell 工作流程 runbook toolearn 看到[編輯 Azure 自動化中的文字 runbook](automation-edit-textual-runbook.md)</span><span class="sxs-lookup"><span data-stu-id="d273b-141">toolearn more about editing PowerShell and PowerShell Workflow runbooks with a textual editor, see [Editing textual runbooks in Azure Automation](automation-edit-textual-runbook.md)</span></span> 
* <span data-ttu-id="d273b-142">toolearn 深入了解建立和匯入 runbook，請參閱[建立或匯入在 Azure 自動化 runbook](automation-creating-importing-runbook.md)</span><span class="sxs-lookup"><span data-stu-id="d273b-142">toolearn more about creating and importing runbooks, see [Creating or importing a runbook in Azure Automation](automation-creating-importing-runbook.md)</span></span>


