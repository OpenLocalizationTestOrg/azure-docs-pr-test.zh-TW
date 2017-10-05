---
title: "編譯 Azure 自動化 DSC 中的組態 | Microsoft Docs"
description: "此文章說明如何針對 Azure 自動化編譯期望狀態設定 (DSC) 組態。"
services: automation
documentationcenter: na
author: eslesar
manager: carmonm
ms.assetid: 49f20b31-4fa5-4712-b1c7-8f4409f1aecc
ms.service: automation
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: powershell
ms.workload: na
ms.date: 02/07/2017
ms.author: magoedte; eslesar
ms.openlocfilehash: 1aadd604e676659475f00760af3b0bdfb13a4792
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="compiling-configurations-in-azure-automation-dsc"></a><span data-ttu-id="2fc47-103">編譯 Azure 自動化 DSC 中的組態</span><span class="sxs-lookup"><span data-stu-id="2fc47-103">Compiling configurations in Azure Automation DSC</span></span>

<span data-ttu-id="2fc47-104">使用 Azure 自動化時有兩種方式可以編譯「期望狀態設定 (DSC)」組態：在 Azure 入口網站中，以及使用 Windows PowerShell。</span><span class="sxs-lookup"><span data-stu-id="2fc47-104">You can compile Desired State Configuration (DSC) configurations in two ways with Azure Automation: in the Azure portal, and with Windows PowerShell.</span></span> <span data-ttu-id="2fc47-105">下表將協助您根據方法的特性判斷何時應使用哪種方法：</span><span class="sxs-lookup"><span data-stu-id="2fc47-105">The following table will help you determine when to use which method based on the characteristics of each:</span></span>

### <a name="azure-portal"></a><span data-ttu-id="2fc47-106">Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="2fc47-106">Azure portal</span></span>

* <span data-ttu-id="2fc47-107">互動式使用者介面的最簡單方法</span><span class="sxs-lookup"><span data-stu-id="2fc47-107">Simplest method with interactive user interface</span></span>
* <span data-ttu-id="2fc47-108">提供簡單參數值的表單</span><span class="sxs-lookup"><span data-stu-id="2fc47-108">Form to provide simple parameter values</span></span>
* <span data-ttu-id="2fc47-109">輕鬆追蹤工作狀態</span><span class="sxs-lookup"><span data-stu-id="2fc47-109">Easily track job state</span></span>
* <span data-ttu-id="2fc47-110">使用 Azure 登入資訊驗證存取</span><span class="sxs-lookup"><span data-stu-id="2fc47-110">Access authenticated with Azure logon</span></span>

### <a name="windows-powershell"></a><span data-ttu-id="2fc47-111">Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="2fc47-111">Windows PowerShell</span></span>

* <span data-ttu-id="2fc47-112">使用 Windows PowerShell Cmdlet 從命令列呼叫</span><span class="sxs-lookup"><span data-stu-id="2fc47-112">Call from command line with Windows PowerShell cmdlets</span></span>
* <span data-ttu-id="2fc47-113">可以包含在具有多個步驟的自動化解決方案中</span><span class="sxs-lookup"><span data-stu-id="2fc47-113">Can be included in automated solution with multiple steps</span></span>
* <span data-ttu-id="2fc47-114">提供簡單和複雜的參數值</span><span class="sxs-lookup"><span data-stu-id="2fc47-114">Provide simple and complex parameter values</span></span>
* <span data-ttu-id="2fc47-115">追蹤工作狀態</span><span class="sxs-lookup"><span data-stu-id="2fc47-115">Track job state</span></span>
* <span data-ttu-id="2fc47-116">支援 PowerShell Cmdlet 所需的用戶端</span><span class="sxs-lookup"><span data-stu-id="2fc47-116">Client required to support PowerShell cmdlets</span></span>
* <span data-ttu-id="2fc47-117">傳遞 ConfigurationData</span><span class="sxs-lookup"><span data-stu-id="2fc47-117">Pass ConfigurationData</span></span>
* <span data-ttu-id="2fc47-118">編譯使用認證的組態</span><span class="sxs-lookup"><span data-stu-id="2fc47-118">Compile configurations that use credentials</span></span>

<span data-ttu-id="2fc47-119">在您決定編譯方法後，您可以依照下列個別的程序開始編譯。</span><span class="sxs-lookup"><span data-stu-id="2fc47-119">Once you have decided on a compilation method, you can follow the respective procedures below to start compiling.</span></span>

## <a name="compiling-a-dsc-configuration-with-the-azure-portal"></a><span data-ttu-id="2fc47-120">使用 Azure 入口網站編譯 DSC 組態</span><span class="sxs-lookup"><span data-stu-id="2fc47-120">Compiling a DSC Configuration with the Azure portal</span></span>

1. <span data-ttu-id="2fc47-121">從您的自動化帳戶中，按一下 [DSC 組態]。</span><span class="sxs-lookup"><span data-stu-id="2fc47-121">From your Automation account, click **DSC Configurations**.</span></span>
2. <span data-ttu-id="2fc47-122">按一下組態以開啟其刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="2fc47-122">Click a configuration to open its blade.</span></span>
3. <span data-ttu-id="2fc47-123">按一下 [編譯] 。</span><span class="sxs-lookup"><span data-stu-id="2fc47-123">Click **Compile**.</span></span>
4. <span data-ttu-id="2fc47-124">如果組態沒有參數，系統會提示您確認是否要加以編譯。</span><span class="sxs-lookup"><span data-stu-id="2fc47-124">If the configuration has no parameters, you will be prompted to confirm whether you want to compile it.</span></span> <span data-ttu-id="2fc47-125">如果組態有參數，即會開啟 [編譯組態] 刀鋒視窗，讓您可以提供參數值。</span><span class="sxs-lookup"><span data-stu-id="2fc47-125">If the configuration has parameters, the **Compile Configuration** blade will open so you can provide parameter values.</span></span> <span data-ttu-id="2fc47-126">如需參數的進一步詳細資訊，請參閱以下的[**基本參數**](#basic-parameters)一節。</span><span class="sxs-lookup"><span data-stu-id="2fc47-126">See the [**Basic Parameters**](#basic-parameters) section below for further details on parameters.</span></span>
5. <span data-ttu-id="2fc47-127">[編譯工作]  刀鋒視窗隨即開啟，供您追蹤編譯工作的狀態，以及因為此工作而放在 Azure 自動化 DSC 提取伺服器上的節點組態 (MOF 組態文件)。</span><span class="sxs-lookup"><span data-stu-id="2fc47-127">The **Compilation Job** blade is opened so that you can track the compilation job's status, and the node configurations (MOF configuration documents) it caused to be placed on the Azure Automation DSC Pull Server.</span></span>

## <a name="compiling-a-dsc-configuration-with-windows-powershell"></a><span data-ttu-id="2fc47-128">使用 Windows PowerShell 編譯 DSC 組態</span><span class="sxs-lookup"><span data-stu-id="2fc47-128">Compiling a DSC Configuration with Windows PowerShell</span></span>

<span data-ttu-id="2fc47-129">您可以在 Windows PowerShell 中使用 [`Start-AzureRmAutomationDscCompilationJob`](/powershell/module/azurerm.automation/start-azurermautomationdsccompilationjob) 開始編譯。</span><span class="sxs-lookup"><span data-stu-id="2fc47-129">You can use [`Start-AzureRmAutomationDscCompilationJob`](/powershell/module/azurerm.automation/start-azurermautomationdsccompilationjob) to start compiling with Windows PowerShell.</span></span> <span data-ttu-id="2fc47-130">下列範例程式碼會啟動 DSC 組態 **SampleConfig**的編譯。</span><span class="sxs-lookup"><span data-stu-id="2fc47-130">The following sample code starts compilation of a DSC configuration called **SampleConfig**.</span></span>

```powershell
Start-AzureRmAutomationDscCompilationJob -ResourceGroupName "MyResourceGroup" -AutomationAccountName "MyAutomationAccount" -ConfigurationName "SampleConfig"
```

<span data-ttu-id="2fc47-131">`Start-AzureRmAutomationDscCompilationJob` 會傳回可用來追蹤工作狀態的編譯工作物件。</span><span class="sxs-lookup"><span data-stu-id="2fc47-131">`Start-AzureRmAutomationDscCompilationJob` returns a compilation job object that you can use to track its status.</span></span> <span data-ttu-id="2fc47-132">接著，您可以使用此編譯工作物件與 [`Get-AzureRmAutomationDscCompilationJob`](/powershell/module/azurerm.automation/get-azurermautomationdsccompilationjob) 來判斷編譯工作的狀態，並使用 [`Get-AzureRmAutomationDscCompilationJobOutput`](/powershell/module/azurerm.automation/get-azurermautomationdsccompilationjoboutput) 來檢視其串流 (輸出)。</span><span class="sxs-lookup"><span data-stu-id="2fc47-132">You can then use this compilation job object with [`Get-AzureRmAutomationDscCompilationJob`](/powershell/module/azurerm.automation/get-azurermautomationdsccompilationjob) to determine the status of the compilation job, and [`Get-AzureRmAutomationDscCompilationJobOutput`](/powershell/module/azurerm.automation/get-azurermautomationdsccompilationjoboutput) to view its streams (output).</span></span> <span data-ttu-id="2fc47-133">下列範例程式碼會啟動 **SampleConfig** 組態的編譯，並在編譯完成後顯示其串流。</span><span class="sxs-lookup"><span data-stu-id="2fc47-133">The following sample code starts compilation of the **SampleConfig** configuration, waits until it has completed, and then displays its streams.</span></span>

```powershell
$CompilationJob = Start-AzureRmAutomationDscCompilationJob -ResourceGroupName "MyResourceGroup" -AutomationAccountName "MyAutomationAccount" -ConfigurationName "SampleConfig"

while($CompilationJob.EndTime –eq $null -and $CompilationJob.Exception –eq $null)
{
    $CompilationJob = $CompilationJob | Get-AzureRmAutomationDscCompilationJob
    Start-Sleep -Seconds 3
}

$CompilationJob | Get-AzureRmAutomationDscCompilationJobOutput –Stream Any
```

## <a name="basic-parameters"></a><span data-ttu-id="2fc47-134">基本參數</span><span class="sxs-lookup"><span data-stu-id="2fc47-134">Basic Parameters</span></span>
<span data-ttu-id="2fc47-135">DSC 組態中的參數宣告 (包括參數類型和屬性) 的運作方式與 Azure 自動化 Runbook 中相同。</span><span class="sxs-lookup"><span data-stu-id="2fc47-135">Parameter declaration in DSC configurations, including parameter types and properties, works the same as in Azure Automation runbooks.</span></span> <span data-ttu-id="2fc47-136">若要深入了解 Runbook 參數，請參閱 [在 Azure 自動化中啟動 Runbook](automation-starting-a-runbook.md) 。</span><span class="sxs-lookup"><span data-stu-id="2fc47-136">See [Starting a runbook in Azure Automation](automation-starting-a-runbook.md) to learn more about runbook parameters.</span></span>

<span data-ttu-id="2fc47-137">下列範例使用兩個名為 **FeatureName** 和 **IsPresent** 的參數，來判斷在編譯期間產生的 **ParametersExample.sample** 節點組態中的屬性值。</span><span class="sxs-lookup"><span data-stu-id="2fc47-137">The following example uses two parameters called **FeatureName** and **IsPresent**, to determine the values of properties in the **ParametersExample.sample** node configuration, generated during compilation.</span></span>

```powershell
Configuration ParametersExample
{
    param(
        [Parameter(Mandatory=$true)]

        [string] $FeatureName,

        [Parameter(Mandatory=$true)]
        [boolean] $IsPresent
    )

    $EnsureString = "Present"
    if($IsPresent -eq $false)
    {
        $EnsureString = "Absent"
    }

    Node "sample"
    {
        WindowsFeature ($FeatureName + "Feature")
        {
            Ensure = $EnsureString
            Name = $FeatureName
        }
    }
}
```

<span data-ttu-id="2fc47-138">您可以在 Azure Automation DSC 入口網站或 Azure PowerShell 中編譯使用基本參數的 DSC 組態：</span><span class="sxs-lookup"><span data-stu-id="2fc47-138">You can compile DSC Configurations that use basic parameters in the Azure Automation DSC portal, or with Azure PowerShell:</span></span>

### <a name="portal"></a><span data-ttu-id="2fc47-139">入口網站</span><span class="sxs-lookup"><span data-stu-id="2fc47-139">Portal</span></span>

<span data-ttu-id="2fc47-140">在入口網站中，您可以在按一下 [編譯] 後輸入參數值。</span><span class="sxs-lookup"><span data-stu-id="2fc47-140">In the portal, you can enter parameter values after clicking **Compile**.</span></span>

![替代文字](./media/automation-dsc-compile/DSC_compiling_1.png)

### <a name="powershell"></a><span data-ttu-id="2fc47-142">PowerShell</span><span class="sxs-lookup"><span data-stu-id="2fc47-142">PowerShell</span></span>

<span data-ttu-id="2fc47-143">PowerShell 會要求您將參數放入 [hashtable](http://technet.microsoft.com/library/hh847780.aspx) 中，且其中的索引鍵必須符合參數名稱，值等於參數值。</span><span class="sxs-lookup"><span data-stu-id="2fc47-143">PowerShell requires parameters in a [hashtable](http://technet.microsoft.com/library/hh847780.aspx) where the key matches the parameter name, and the value equals the parameter value.</span></span>

```powershell
$Parameters = @{
    "FeatureName" = "Web-Server"
    "IsPresent" = $False
}

Start-AzureRmAutomationDscCompilationJob -ResourceGroupName "MyResourceGroup" -AutomationAccountName "MyAutomationAccount" -ConfigurationName "ParametersExample" -Parameters $Parameters
```

<span data-ttu-id="2fc47-144">如需如何將 PSCredentials 傳入作為參數的相關資訊，請參閱下方的 <a href="#credential-assets">**認證資產**</a> 。</span><span class="sxs-lookup"><span data-stu-id="2fc47-144">For information about passing PSCredentials as parameters, see <a href="#credential-assets">**Credential Assets**</a> below.</span></span>

## <a name="configurationdata"></a><span data-ttu-id="2fc47-145">ConfigurationData</span><span class="sxs-lookup"><span data-stu-id="2fc47-145">ConfigurationData</span></span>
<span data-ttu-id="2fc47-146">**ConfigurationData** 可讓您在使用 PowerShell DSC 時區隔結構化組態與任何環境特定組態。</span><span class="sxs-lookup"><span data-stu-id="2fc47-146">**ConfigurationData** allows you to separate structural configuration from any environment specific configuration while using PowerShell DSC.</span></span> <span data-ttu-id="2fc47-147">請參閱 [區隔 PowerShell DSC 中的 "What" 與 "Where"](http://blogs.msdn.com/b/powershell/archive/2014/01/09/continuous-deployment-using-dsc-with-minimal-change.aspx) ，以深入了解 **ConfigurationData**。</span><span class="sxs-lookup"><span data-stu-id="2fc47-147">See [Separating "What" from "Where" in PowerShell DSC](http://blogs.msdn.com/b/powershell/archive/2014/01/09/continuous-deployment-using-dsc-with-minimal-change.aspx) to learn more about **ConfigurationData**.</span></span>

> [!NOTE]
> <span data-ttu-id="2fc47-148">使用 Azure PowerShell 在 Azure 自動化 DSC 中進行編譯時可以使用 **ConfigurationData** ，但使用 Azure 入口網站時則否。</span><span class="sxs-lookup"><span data-stu-id="2fc47-148">You can use **ConfigurationData** when compiling in Azure Automation DSC using Azure PowerShell, but not in the Azure portal.</span></span>

<span data-ttu-id="2fc47-149">下列範例 DSC 組態會透過 **$ConfigurationData** 和 **$AllNodes** 關鍵字來使用 **ConfigurationData**。</span><span class="sxs-lookup"><span data-stu-id="2fc47-149">The following example DSC configuration uses **ConfigurationData** via the **$ConfigurationData** and **$AllNodes** keywords.</span></span> <span data-ttu-id="2fc47-150">在此範例中也需要 [**xWebAdministration** 模組](https://www.powershellgallery.com/packages/xWebAdministration/)：</span><span class="sxs-lookup"><span data-stu-id="2fc47-150">You'll also need the [**xWebAdministration** module](https://www.powershellgallery.com/packages/xWebAdministration/) for this example:</span></span>

```powershell
Configuration ConfigurationDataSample
{
    Import-DscResource -ModuleName xWebAdministration -Name MSFT_xWebsite

    Write-Verbose $ConfigurationData.NonNodeData.SomeMessage

    Node $AllNodes.Where{$_.Role -eq "WebServer"}.NodeName
    {
        xWebsite Site
        {
            Name = $Node.SiteName
            PhysicalPath = $Node.SiteContents
            Ensure   = "Present"
        }
    }
}
```

<span data-ttu-id="2fc47-151">您可以使用 PowerShell 編譯上述 DSC 組態。</span><span class="sxs-lookup"><span data-stu-id="2fc47-151">You can compile the DSC configuration above with PowerShell.</span></span> <span data-ttu-id="2fc47-152">PowerShell 會將以下兩個節點組態新增至 Azure Automation DSC 提取伺服器：**ConfigurationDataSample.MyVM1** 和 **ConfigurationDataSample.MyVM3**：</span><span class="sxs-lookup"><span data-stu-id="2fc47-152">The below PowerShell adds two node configurations to the Azure Automation DSC Pull Server: **ConfigurationDataSample.MyVM1** and **ConfigurationDataSample.MyVM3**:</span></span>

```powershell
$ConfigData = @{
    AllNodes = @(
        @{
            NodeName = "MyVM1"
            Role = "WebServer"
        },
        @{
            NodeName = "MyVM2"
            Role = "SQLServer"
        },
        @{
            NodeName = "MyVM3"
            Role = "WebServer"
        }
    )

    NonNodeData = @{
        SomeMessage = "I love Azure Automation DSC!"
    }
}

Start-AzureRmAutomationDscCompilationJob -ResourceGroupName "MyResourceGroup" -AutomationAccountName "MyAutomationAccount" -ConfigurationName "ConfigurationDataSample" -ConfigurationData $ConfigData
```

## <a name="assets"></a><span data-ttu-id="2fc47-153">資產</span><span class="sxs-lookup"><span data-stu-id="2fc47-153">Assets</span></span>

<span data-ttu-id="2fc47-154">Azure 自動化 DSC 組態和 Runbook 中的資產參考是相同的。</span><span class="sxs-lookup"><span data-stu-id="2fc47-154">Asset references are the same in Azure Automation DSC configurations and runbooks.</span></span> <span data-ttu-id="2fc47-155">如需詳細資訊，請參閱下列主題：</span><span class="sxs-lookup"><span data-stu-id="2fc47-155">See the following for more information:</span></span>

* [<span data-ttu-id="2fc47-156">憑證</span><span class="sxs-lookup"><span data-stu-id="2fc47-156">Certificates</span></span>](automation-certificates.md)
* [<span data-ttu-id="2fc47-157">連線</span><span class="sxs-lookup"><span data-stu-id="2fc47-157">Connections</span></span>](automation-connections.md)
* [<span data-ttu-id="2fc47-158">認證</span><span class="sxs-lookup"><span data-stu-id="2fc47-158">Credentials</span></span>](automation-credentials.md)
* [<span data-ttu-id="2fc47-159">變數</span><span class="sxs-lookup"><span data-stu-id="2fc47-159">Variables</span></span>](automation-variables.md)

### <a name="credential-assets"></a><span data-ttu-id="2fc47-160">認證資產</span><span class="sxs-lookup"><span data-stu-id="2fc47-160">Credential Assets</span></span>

<span data-ttu-id="2fc47-161">雖然 Azure 自動化中的 DSC 組態可以使用 **Get-AzureRmAutomationCredential**參考認證資產，但如有需要，也可以透過參數傳入認證資產。</span><span class="sxs-lookup"><span data-stu-id="2fc47-161">While DSC configurations in Azure Automation can reference credential assets using **Get-AzureRmAutomationCredential**, credential assets can also be passed in via parameters, if desired.</span></span> <span data-ttu-id="2fc47-162">如果組態採用屬於 **PSCredential** 類型的參數，您必須將 Azure 自動化認證資產的字串名稱傳遞為該參數的值，而不是 PSCredential 物件。</span><span class="sxs-lookup"><span data-stu-id="2fc47-162">If a configuration takes a parameter of **PSCredential** type, then you need to pass the string name of an Azure Automation credential asset as that parameter’s value, rather than a PSCredential object.</span></span> <span data-ttu-id="2fc47-163">具有該名稱的 Azure 自動化認證資產會在背景中被擷取，並傳遞至組態。</span><span class="sxs-lookup"><span data-stu-id="2fc47-163">Behind the scenes, the Azure Automation credential asset with that name will be retrieved and passed to the configuration.</span></span>

<span data-ttu-id="2fc47-164">要在節點組態 (MOF 組態文件) 中保持認證的安全性，需要在節點組態 MOF 檔案中為認證加密。</span><span class="sxs-lookup"><span data-stu-id="2fc47-164">Keeping credentials secure in node configurations (MOF configuration documents) requires encrypting the credentials in the node configuration MOF file.</span></span> <span data-ttu-id="2fc47-165">Azure 自動化會進一步執行此步驟，而加密整個 MOF 檔案。</span><span class="sxs-lookup"><span data-stu-id="2fc47-165">Azure Automation takes this one step further and encrypts the entire MOF file.</span></span> <span data-ttu-id="2fc47-166">不過，目前您必須告知 PowerShell DSC 在節點組態 MOF 產生期間以純文字形式輸出認證是可行的，因為 PowerShell DSC 並不知道在透過編譯工作產生 MOF 檔案之後 Azure 自動化會加密整個檔案。</span><span class="sxs-lookup"><span data-stu-id="2fc47-166">However, currently you must tell PowerShell DSC it is okay for credentials to be outputted in plain text during node configuration MOF generation, because PowerShell DSC doesn’t know that Azure Automation will be encrypting the entire MOF file after its generation via a compilation job.</span></span>

<span data-ttu-id="2fc47-167">您可以告知 PowerShell DSC，使用 [**ConfigurationData**](#configurationdata)。</span><span class="sxs-lookup"><span data-stu-id="2fc47-167">You can tell PowerShell DSC that it is okay for credentials to be outputted in plain text in the generated node configuration MOFs using [**ConfigurationData**](#configurationdata).</span></span> <span data-ttu-id="2fc47-168">您應針對每個出現在 DSC 組態中且使用認證的節點區塊名稱，透過 **ConfigurationData** 傳遞 `PSDscAllowPlainTextPassword = $true`。</span><span class="sxs-lookup"><span data-stu-id="2fc47-168">You should pass `PSDscAllowPlainTextPassword = $true` via **ConfigurationData** for each node block’s name that appears in the DSC configuration and uses credentials.</span></span>

<span data-ttu-id="2fc47-169">下列範例說明使用自動化認證資產的 DSC 組態。</span><span class="sxs-lookup"><span data-stu-id="2fc47-169">The following example shows a DSC configuration that uses an Automation credential asset.</span></span>

```powershell
Configuration CredentialSample
{
    $Cred = Get-AzureRmAutomationCredential -ResourceGroupName "ResourceGroup01" -AutomationAccountName "AutomationAcct" -Name "SomeCredentialAsset"

    Node $AllNodes.NodeName
    {
        File ExampleFile
        {
            SourcePath = "\\Server\share\path\file.ext"
            DestinationPath = "C:\destinationPath"
            Credential = $Cred
        }
    }
}
```

<span data-ttu-id="2fc47-170">您可以使用 PowerShell 編譯上述 DSC 組態。</span><span class="sxs-lookup"><span data-stu-id="2fc47-170">You can compile the DSC configuration above with PowerShell.</span></span> <span data-ttu-id="2fc47-171">PowerShell 會將以下兩個節點組態新增至 Azure Automation DSC 提取伺服器：**CredentialSample.MyVM1** 和 **CredentialSample.MyVM2**。</span><span class="sxs-lookup"><span data-stu-id="2fc47-171">The below PowerShell adds two node configurations to the Azure Automation DSC Pull Server:  **CredentialSample.MyVM1** and **CredentialSample.MyVM2**.</span></span>

```powershell
$ConfigData = @{
    AllNodes = @(
        @{
            NodeName = "*"
            PSDscAllowPlainTextPassword = $True
        },
        @{
            NodeName = "MyVM1"
        },
        @{
            NodeName = "MyVM2"
        }
    )
}

Start-AzureRmAutomationDscCompilationJob -ResourceGroupName "MyResourceGroup" -AutomationAccountName "MyAutomationAccount" -ConfigurationName "CredentialSample" -ConfigurationData $ConfigData
```

## <a name="importing-node-configurations"></a><span data-ttu-id="2fc47-172">匯入節點組態</span><span class="sxs-lookup"><span data-stu-id="2fc47-172">Importing node configurations</span></span>

<span data-ttu-id="2fc47-173">您也可以匯入在 Azure 外部完成編譯的節點組態 (MOF)。</span><span class="sxs-lookup"><span data-stu-id="2fc47-173">You can also import node configuratons (MOFs) that you have compiled outside of Azure.</span></span> <span data-ttu-id="2fc47-174">這樣做的優點之一就是可以簽署節點組態。</span><span class="sxs-lookup"><span data-stu-id="2fc47-174">One advantage of this is that node confiturations can be signed.</span></span>
<span data-ttu-id="2fc47-175">DSC 代理程式會在受管理的節點上本機驗證簽署的節點組態，確保套用到節點的組態來自經授權之來源。</span><span class="sxs-lookup"><span data-stu-id="2fc47-175">A signed node configuration is verified locally on a managed node by the DSC agent, ensuring that the configuration being applied to the node comes from an authorized source.</span></span>

> [!NOTE]
> <span data-ttu-id="2fc47-176">您可以將簽署的組態匯入到您的 Azure 自動化帳戶，但 Azure 自動化目前不支援編譯簽署的組態。</span><span class="sxs-lookup"><span data-stu-id="2fc47-176">You can use import signed configurations into your Azure Automation account, but Azure Automation does not currently support compiling signed configurations.</span></span>

> [!NOTE]
> <span data-ttu-id="2fc47-177">節點組態檔不得大於 1 MB，才能匯入到 Azure 自動化。</span><span class="sxs-lookup"><span data-stu-id="2fc47-177">A node configuration file must be no larger than 1 MB to allow it to be imported into Azure Automation.</span></span>

<span data-ttu-id="2fc47-178">如需了解如何簽署節點組態，請參閱 https://msdn.microsoft.com/en-us/powershell/wmf/5.1/dsc-improvements#how-to-sign-configuration-and-module。</span><span class="sxs-lookup"><span data-stu-id="2fc47-178">You can learn how to sign node configurations at https://msdn.microsoft.com/en-us/powershell/wmf/5.1/dsc-improvements#how-to-sign-configuration-and-module.</span></span>

### <a name="importing-a-node-configuration-in-the-azure-portal"></a><span data-ttu-id="2fc47-179">在 Azure 入口網站中匯入節點組態</span><span class="sxs-lookup"><span data-stu-id="2fc47-179">Importing a node configuration in the Azure portal</span></span>

1. <span data-ttu-id="2fc47-180">從您的自動化帳戶中，按一下 [DSC 節點組態]。</span><span class="sxs-lookup"><span data-stu-id="2fc47-180">From your Automation account, click **DSC node configurations**.</span></span>

    ![DSC 節點組態](./media/automation-dsc-compile/node-config.png)
2. <span data-ttu-id="2fc47-182">在 [DSC 節點組態] 刀鋒視窗上，按一下 [新增節點組態]。</span><span class="sxs-lookup"><span data-stu-id="2fc47-182">In the **DSC node configurations** blade, click **Add a NodeConfiguration**.</span></span>
3. <span data-ttu-id="2fc47-183">在 [匯入] 刀鋒視窗中，按一下資料夾圖示旁的 [節點組態檔] 文字方塊，以瀏覽本機電腦上的節點組態檔 (MOF)。</span><span class="sxs-lookup"><span data-stu-id="2fc47-183">In the **Import** blade, click the folder icon next to the **Node Configuration File** textbox to browse for a node configuration file (MOF) on your local computer.</span></span>

    ![瀏覽本機檔案](./media/automation-dsc-compile/import-browse.png)
4. <span data-ttu-id="2fc47-185">在 [組態名稱]文字方塊中輸入名稱。</span><span class="sxs-lookup"><span data-stu-id="2fc47-185">Enter a name in the **Configuration Name** textbox.</span></span> <span data-ttu-id="2fc47-186">此名稱必須符合已編譯節點組態的組態名稱。</span><span class="sxs-lookup"><span data-stu-id="2fc47-186">This name must match the name of the configuration from which the node configuration was compiled.</span></span>
5. <span data-ttu-id="2fc47-187">按一下 [確定] 。</span><span class="sxs-lookup"><span data-stu-id="2fc47-187">Click **OK**.</span></span>

### <a name="importing-a-node-configuration-with-powershell"></a><span data-ttu-id="2fc47-188">使用 PowerShell 匯入節點組態</span><span class="sxs-lookup"><span data-stu-id="2fc47-188">Importing a node configuration with PowerShell</span></span>

<span data-ttu-id="2fc47-189">您可以使用 [Import-AzureRmAutomationDscNodeConfiguration](/powershell/module/azurerm.automation/import-azurermautomationdscnodeconfiguration) Cmdlet，將節點組態匯入到您的自動化帳戶。</span><span class="sxs-lookup"><span data-stu-id="2fc47-189">You can use the [Import-AzureRmAutomationDscNodeConfiguration](/powershell/module/azurerm.automation/import-azurermautomationdscnodeconfiguration) cmdlet to import a node configuration into your automation account.</span></span>

```powershell
Import-AzureRmAutomationDscNodeConfiguration -AutomationAccountName "MyAutomationAccount" -ResourceGroupName "MyResourceGroup" -ConfigurationName "MyNodeConfiguration" -Path "C:\MyConfigurations\TestVM1.mof"
```



