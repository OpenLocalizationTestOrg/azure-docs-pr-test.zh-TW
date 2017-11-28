---
title: "在 Azure Automation DSC aaaCompiling 組態 |Microsoft 文件"
description: "本文說明如何 toocompile 預期狀態設定 (DSC) 設定 Azure 自動化。"
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
ms.openlocfilehash: b195311318a2d7431c4d6b29f4b9a5f3a0a0a9a5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="compiling-configurations-in-azure-automation-dsc"></a><span data-ttu-id="b31f4-103">編譯 Azure 自動化 DSC 中的組態</span><span class="sxs-lookup"><span data-stu-id="b31f4-103">Compiling configurations in Azure Automation DSC</span></span>

<span data-ttu-id="b31f4-104">您可以編譯為預期狀態設定 (DSC) 設定與 Azure 自動化有兩種： hello Azure 入口網站，並使用 Windows PowerShell。</span><span class="sxs-lookup"><span data-stu-id="b31f4-104">You can compile Desired State Configuration (DSC) configurations in two ways with Azure Automation: in hello Azure portal, and with Windows PowerShell.</span></span> <span data-ttu-id="b31f4-105">hello 下列表格可協助您判斷何時 toouse 哪一種方法會根據每個 hello 特性：</span><span class="sxs-lookup"><span data-stu-id="b31f4-105">hello following table will help you determine when toouse which method based on hello characteristics of each:</span></span>

### <a name="azure-portal"></a><span data-ttu-id="b31f4-106">Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="b31f4-106">Azure portal</span></span>

* <span data-ttu-id="b31f4-107">互動式使用者介面的最簡單方法</span><span class="sxs-lookup"><span data-stu-id="b31f4-107">Simplest method with interactive user interface</span></span>
* <span data-ttu-id="b31f4-108">表單 tooprovide 簡單的參數值</span><span class="sxs-lookup"><span data-stu-id="b31f4-108">Form tooprovide simple parameter values</span></span>
* <span data-ttu-id="b31f4-109">輕鬆追蹤工作狀態</span><span class="sxs-lookup"><span data-stu-id="b31f4-109">Easily track job state</span></span>
* <span data-ttu-id="b31f4-110">使用 Azure 登入資訊驗證存取</span><span class="sxs-lookup"><span data-stu-id="b31f4-110">Access authenticated with Azure logon</span></span>

### <a name="windows-powershell"></a><span data-ttu-id="b31f4-111">Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="b31f4-111">Windows PowerShell</span></span>

* <span data-ttu-id="b31f4-112">使用 Windows PowerShell Cmdlet 從命令列呼叫</span><span class="sxs-lookup"><span data-stu-id="b31f4-112">Call from command line with Windows PowerShell cmdlets</span></span>
* <span data-ttu-id="b31f4-113">可以包含在具有多個步驟的自動化解決方案中</span><span class="sxs-lookup"><span data-stu-id="b31f4-113">Can be included in automated solution with multiple steps</span></span>
* <span data-ttu-id="b31f4-114">提供簡單和複雜的參數值</span><span class="sxs-lookup"><span data-stu-id="b31f4-114">Provide simple and complex parameter values</span></span>
* <span data-ttu-id="b31f4-115">追蹤工作狀態</span><span class="sxs-lookup"><span data-stu-id="b31f4-115">Track job state</span></span>
* <span data-ttu-id="b31f4-116">所需的用戶端 toosupport PowerShell cmdlet</span><span class="sxs-lookup"><span data-stu-id="b31f4-116">Client required toosupport PowerShell cmdlets</span></span>
* <span data-ttu-id="b31f4-117">傳遞 ConfigurationData</span><span class="sxs-lookup"><span data-stu-id="b31f4-117">Pass ConfigurationData</span></span>
* <span data-ttu-id="b31f4-118">編譯使用認證的組態</span><span class="sxs-lookup"><span data-stu-id="b31f4-118">Compile configurations that use credentials</span></span>

<span data-ttu-id="b31f4-119">一旦您決定編譯方法上，您可以依照以下 toostart 編譯 hello 個別的程序。</span><span class="sxs-lookup"><span data-stu-id="b31f4-119">Once you have decided on a compilation method, you can follow hello respective procedures below toostart compiling.</span></span>

## <a name="compiling-a-dsc-configuration-with-hello-azure-portal"></a><span data-ttu-id="b31f4-120">編譯 DSC 設定以 hello Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="b31f4-120">Compiling a DSC Configuration with hello Azure portal</span></span>

1. <span data-ttu-id="b31f4-121">從您的自動化帳戶中，按一下 [DSC 組態]。</span><span class="sxs-lookup"><span data-stu-id="b31f4-121">From your Automation account, click **DSC Configurations**.</span></span>
2. <span data-ttu-id="b31f4-122">按一下 設定 tooopen 其刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="b31f4-122">Click a configuration tooopen its blade.</span></span>
3. <span data-ttu-id="b31f4-123">按一下 [編譯] 。</span><span class="sxs-lookup"><span data-stu-id="b31f4-123">Click **Compile**.</span></span>
4. <span data-ttu-id="b31f4-124">如果 hello 設定沒有任何參數，則會提示的 tooconfirm 是否要將 toocompile 它。</span><span class="sxs-lookup"><span data-stu-id="b31f4-124">If hello configuration has no parameters, you will be prompted tooconfirm whether you want toocompile it.</span></span> <span data-ttu-id="b31f4-125">如果 hello 組態有參數，hello**編譯組態**刀鋒視窗會開啟，以便您可以提供參數值。</span><span class="sxs-lookup"><span data-stu-id="b31f4-125">If hello configuration has parameters, hello **Compile Configuration** blade will open so you can provide parameter values.</span></span> <span data-ttu-id="b31f4-126">請參閱 hello [**基本參數**](#basic-parameters)下面章節以取得參數的詳細資料。</span><span class="sxs-lookup"><span data-stu-id="b31f4-126">See hello [**Basic Parameters**](#basic-parameters) section below for further details on parameters.</span></span>
5. <span data-ttu-id="b31f4-127">hello**編譯工作**刀鋒視窗中開啟，讓您可以追蹤 hello 編譯作業的狀態，並 hello 節點組態 （MOF 設定文件） 則因為 toobe 置於 hello Azure Automation DSC 提取伺服器。</span><span class="sxs-lookup"><span data-stu-id="b31f4-127">hello **Compilation Job** blade is opened so that you can track hello compilation job's status, and hello node configurations (MOF configuration documents) it caused toobe placed on hello Azure Automation DSC Pull Server.</span></span>

## <a name="compiling-a-dsc-configuration-with-windows-powershell"></a><span data-ttu-id="b31f4-128">使用 Windows PowerShell 編譯 DSC 組態</span><span class="sxs-lookup"><span data-stu-id="b31f4-128">Compiling a DSC Configuration with Windows PowerShell</span></span>

<span data-ttu-id="b31f4-129">您可以使用[ `Start-AzureRmAutomationDscCompilationJob` ](/powershell/module/azurerm.automation/start-azurermautomationdsccompilationjob) toostart 編譯使用 Windows PowerShell。</span><span class="sxs-lookup"><span data-stu-id="b31f4-129">You can use [`Start-AzureRmAutomationDscCompilationJob`](/powershell/module/azurerm.automation/start-azurermautomationdsccompilationjob) toostart compiling with Windows PowerShell.</span></span> <span data-ttu-id="b31f4-130">下列範例程式碼的 hello 啟動編譯 DSC 設定，稱為**SampleConfig**。</span><span class="sxs-lookup"><span data-stu-id="b31f4-130">hello following sample code starts compilation of a DSC configuration called **SampleConfig**.</span></span>

```powershell
Start-AzureRmAutomationDscCompilationJob -ResourceGroupName "MyResourceGroup" -AutomationAccountName "MyAutomationAccount" -ConfigurationName "SampleConfig"
```

<span data-ttu-id="b31f4-131">`Start-AzureRmAutomationDscCompilationJob`傳回編譯作業，您可以使用 tootrack 其狀態的物件。</span><span class="sxs-lookup"><span data-stu-id="b31f4-131">`Start-AzureRmAutomationDscCompilationJob` returns a compilation job object that you can use tootrack its status.</span></span> <span data-ttu-id="b31f4-132">然後，您可以使用此編譯作業物件搭配[ `Get-AzureRmAutomationDscCompilationJob` ](/powershell/module/azurerm.automation/get-azurermautomationdsccompilationjob) hello 編譯工作，toodetermine hello 狀態和[ `Get-AzureRmAutomationDscCompilationJobOutput` ](/powershell/module/azurerm.automation/get-azurermautomationdsccompilationjoboutput) tooview 其資料流 （輸出）。</span><span class="sxs-lookup"><span data-stu-id="b31f4-132">You can then use this compilation job object with [`Get-AzureRmAutomationDscCompilationJob`](/powershell/module/azurerm.automation/get-azurermautomationdsccompilationjob) toodetermine hello status of hello compilation job, and [`Get-AzureRmAutomationDscCompilationJobOutput`](/powershell/module/azurerm.automation/get-azurermautomationdsccompilationjoboutput) tooview its streams (output).</span></span> <span data-ttu-id="b31f4-133">下列範例程式碼的 hello 啟動的 hello 編譯**SampleConfig**組態中，等候直到它已完成，並接著會顯示其資料流。</span><span class="sxs-lookup"><span data-stu-id="b31f4-133">hello following sample code starts compilation of hello **SampleConfig** configuration, waits until it has completed, and then displays its streams.</span></span>

```powershell
$CompilationJob = Start-AzureRmAutomationDscCompilationJob -ResourceGroupName "MyResourceGroup" -AutomationAccountName "MyAutomationAccount" -ConfigurationName "SampleConfig"

while($CompilationJob.EndTime –eq $null -and $CompilationJob.Exception –eq $null)
{
    $CompilationJob = $CompilationJob | Get-AzureRmAutomationDscCompilationJob
    Start-Sleep -Seconds 3
}

$CompilationJob | Get-AzureRmAutomationDscCompilationJobOutput –Stream Any
```

## <a name="basic-parameters"></a><span data-ttu-id="b31f4-134">基本參數</span><span class="sxs-lookup"><span data-stu-id="b31f4-134">Basic Parameters</span></span>
<span data-ttu-id="b31f4-135">在 DSC 設定，包含參數型別和運作的內容中的參數宣告 hello 相同如同 Azure 自動化 runbook。</span><span class="sxs-lookup"><span data-stu-id="b31f4-135">Parameter declaration in DSC configurations, including parameter types and properties, works hello same as in Azure Automation runbooks.</span></span> <span data-ttu-id="b31f4-136">請參閱[Azure 自動化中啟動 runbook](automation-starting-a-runbook.md) toolearn 深入了解 runbook 參數。</span><span class="sxs-lookup"><span data-stu-id="b31f4-136">See [Starting a runbook in Azure Automation](automation-starting-a-runbook.md) toolearn more about runbook parameters.</span></span>

<span data-ttu-id="b31f4-137">hello 下列範例會使用兩個參數呼叫**FeatureName**和**IsPresent**，toodetermine hello 中 hello 屬性值**ParametersExample.sample**節點設定中，在編譯期間產生。</span><span class="sxs-lookup"><span data-stu-id="b31f4-137">hello following example uses two parameters called **FeatureName** and **IsPresent**, toodetermine hello values of properties in hello **ParametersExample.sample** node configuration, generated during compilation.</span></span>

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

<span data-ttu-id="b31f4-138">您可以編譯 DSC 設定在 hello Azure Automation DSC 入口網站或 Azure PowerShell，使用基本參數：</span><span class="sxs-lookup"><span data-stu-id="b31f4-138">You can compile DSC Configurations that use basic parameters in hello Azure Automation DSC portal, or with Azure PowerShell:</span></span>

### <a name="portal"></a><span data-ttu-id="b31f4-139">入口網站</span><span class="sxs-lookup"><span data-stu-id="b31f4-139">Portal</span></span>

<span data-ttu-id="b31f4-140">在 hello 入口網站中，您可以輸入參數值之後按**編譯**。</span><span class="sxs-lookup"><span data-stu-id="b31f4-140">In hello portal, you can enter parameter values after clicking **Compile**.</span></span>

![替代文字](./media/automation-dsc-compile/DSC_compiling_1.png)

### <a name="powershell"></a><span data-ttu-id="b31f4-142">PowerShell</span><span class="sxs-lookup"><span data-stu-id="b31f4-142">PowerShell</span></span>

<span data-ttu-id="b31f4-143">PowerShell 要求中的參數[雜湊表](http://technet.microsoft.com/library/hh847780.aspx)hello 索引鍵符合 hello 參數名稱，而 hello 值等於 hello 參數值。</span><span class="sxs-lookup"><span data-stu-id="b31f4-143">PowerShell requires parameters in a [hashtable](http://technet.microsoft.com/library/hh847780.aspx) where hello key matches hello parameter name, and hello value equals hello parameter value.</span></span>

```powershell
$Parameters = @{
    "FeatureName" = "Web-Server"
    "IsPresent" = $False
}

Start-AzureRmAutomationDscCompilationJob -ResourceGroupName "MyResourceGroup" -AutomationAccountName "MyAutomationAccount" -ConfigurationName "ParametersExample" -Parameters $Parameters
```

<span data-ttu-id="b31f4-144">如需如何將 PSCredentials 傳入作為參數的相關資訊，請參閱下方的 <a href="#credential-assets">**認證資產**</a> 。</span><span class="sxs-lookup"><span data-stu-id="b31f4-144">For information about passing PSCredentials as parameters, see <a href="#credential-assets">**Credential Assets**</a> below.</span></span>

## <a name="configurationdata"></a><span data-ttu-id="b31f4-145">ConfigurationData</span><span class="sxs-lookup"><span data-stu-id="b31f4-145">ConfigurationData</span></span>
<span data-ttu-id="b31f4-146">**ConfigurationData**可讓您從任何環境的特定設定時使用的 PowerShell DSC tooseparate 結構化設定。</span><span class="sxs-lookup"><span data-stu-id="b31f4-146">**ConfigurationData** allows you tooseparate structural configuration from any environment specific configuration while using PowerShell DSC.</span></span> <span data-ttu-id="b31f4-147">請參閱[「 什麼 」 隔開"Where"PowerShell dsc](http://blogs.msdn.com/b/powershell/archive/2014/01/09/continuous-deployment-using-dsc-with-minimal-change.aspx) toolearn 更多關於**ConfigurationData**。</span><span class="sxs-lookup"><span data-stu-id="b31f4-147">See [Separating "What" from "Where" in PowerShell DSC](http://blogs.msdn.com/b/powershell/archive/2014/01/09/continuous-deployment-using-dsc-with-minimal-change.aspx) toolearn more about **ConfigurationData**.</span></span>

> [!NOTE]
> <span data-ttu-id="b31f4-148">您可以使用**ConfigurationData**編譯中使用 Azure PowerShell 的 Azure 自動化 DSC，但不是在 hello Azure 入口網站時。</span><span class="sxs-lookup"><span data-stu-id="b31f4-148">You can use **ConfigurationData** when compiling in Azure Automation DSC using Azure PowerShell, but not in hello Azure portal.</span></span>

<span data-ttu-id="b31f4-149">hello 下列範例 DSC 設定使用**ConfigurationData**透過 hello **$ConfigurationData**和**$AllNodes**關鍵字。</span><span class="sxs-lookup"><span data-stu-id="b31f4-149">hello following example DSC configuration uses **ConfigurationData** via hello **$ConfigurationData** and **$AllNodes** keywords.</span></span> <span data-ttu-id="b31f4-150">您還需要 hello [ **xWebAdministration**模組](https://www.powershellgallery.com/packages/xWebAdministration/)此範例中：</span><span class="sxs-lookup"><span data-stu-id="b31f4-150">You'll also need hello [**xWebAdministration** module](https://www.powershellgallery.com/packages/xWebAdministration/) for this example:</span></span>

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

<span data-ttu-id="b31f4-151">您可以編譯上述使用 PowerShell 的 hello DSC 設定。</span><span class="sxs-lookup"><span data-stu-id="b31f4-151">You can compile hello DSC configuration above with PowerShell.</span></span> <span data-ttu-id="b31f4-152">hello PowerShell 底下加入兩個節點組態 toohello Azure Automation DSC 提取伺服器： **ConfigurationDataSample.MyVM1**和**ConfigurationDataSample.MyVM3**:</span><span class="sxs-lookup"><span data-stu-id="b31f4-152">hello below PowerShell adds two node configurations toohello Azure Automation DSC Pull Server: **ConfigurationDataSample.MyVM1** and **ConfigurationDataSample.MyVM3**:</span></span>

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

## <a name="assets"></a><span data-ttu-id="b31f4-153">Assets</span><span class="sxs-lookup"><span data-stu-id="b31f4-153">Assets</span></span>

<span data-ttu-id="b31f4-154">資產的參考是 hello Azure 自動化 DSC 設定和 runbook 中相同。</span><span class="sxs-lookup"><span data-stu-id="b31f4-154">Asset references are hello same in Azure Automation DSC configurations and runbooks.</span></span> <span data-ttu-id="b31f4-155">Hello 下列如需詳細資訊，請參閱：</span><span class="sxs-lookup"><span data-stu-id="b31f4-155">See hello following for more information:</span></span>

* [<span data-ttu-id="b31f4-156">憑證</span><span class="sxs-lookup"><span data-stu-id="b31f4-156">Certificates</span></span>](automation-certificates.md)
* [<span data-ttu-id="b31f4-157">連線</span><span class="sxs-lookup"><span data-stu-id="b31f4-157">Connections</span></span>](automation-connections.md)
* [<span data-ttu-id="b31f4-158">認證</span><span class="sxs-lookup"><span data-stu-id="b31f4-158">Credentials</span></span>](automation-credentials.md)
* [<span data-ttu-id="b31f4-159">變數</span><span class="sxs-lookup"><span data-stu-id="b31f4-159">Variables</span></span>](automation-variables.md)

### <a name="credential-assets"></a><span data-ttu-id="b31f4-160">認證資產</span><span class="sxs-lookup"><span data-stu-id="b31f4-160">Credential Assets</span></span>

<span data-ttu-id="b31f4-161">雖然 Azure 自動化中的 DSC 組態可以使用 **Get-AzureRmAutomationCredential**參考認證資產，但如有需要，也可以透過參數傳入認證資產。</span><span class="sxs-lookup"><span data-stu-id="b31f4-161">While DSC configurations in Azure Automation can reference credential assets using **Get-AzureRmAutomationCredential**, credential assets can also be passed in via parameters, if desired.</span></span> <span data-ttu-id="b31f4-162">如果組態使用的參數**PSCredential**類型，則您需要 Azure 自動化認證資產 toopass hello 字串名稱做為該參數的值，而不是 PSCredential 物件。</span><span class="sxs-lookup"><span data-stu-id="b31f4-162">If a configuration takes a parameter of **PSCredential** type, then you need toopass hello string name of an Azure Automation credential asset as that parameter’s value, rather than a PSCredential object.</span></span> <span data-ttu-id="b31f4-163">Hello 幕後 hello Azure 自動化認證資產具有該名稱將會擷取和傳遞 toohello 組態。</span><span class="sxs-lookup"><span data-stu-id="b31f4-163">Behind hello scenes, hello Azure Automation credential asset with that name will be retrieved and passed toohello configuration.</span></span>

<span data-ttu-id="b31f4-164">保留認證安全節點組態 （MOF 設定文件） 需要加密 hello 節點設定 MOF 檔案中的 hello 認證。</span><span class="sxs-lookup"><span data-stu-id="b31f4-164">Keeping credentials secure in node configurations (MOF configuration documents) requires encrypting hello credentials in hello node configuration MOF file.</span></span> <span data-ttu-id="b31f4-165">Azure 自動化會進一步採用此步驟，並且加密 hello 整個 MOF 檔案。</span><span class="sxs-lookup"><span data-stu-id="b31f4-165">Azure Automation takes this one step further and encrypts hello entire MOF file.</span></span> <span data-ttu-id="b31f4-166">不過，目前必須告知 PowerShell DSC 沒有關係的節點設定 MOF 在產生期間，輸出以純文字認證 toobe 因為 PowerShell DSC 並不知道 Azure 自動化會加密後的 hello 整個 MOF 檔案及其產生透過編譯工作。</span><span class="sxs-lookup"><span data-stu-id="b31f4-166">However, currently you must tell PowerShell DSC it is okay for credentials toobe outputted in plain text during node configuration MOF generation, because PowerShell DSC doesn’t know that Azure Automation will be encrypting hello entire MOF file after its generation via a compilation job.</span></span>

<span data-ttu-id="b31f4-167">您可以告訴 PowerShell DSC 是否可以供輸出中產生的 hello 節點設定 Mof 內的純文字認證 toobe 使用[ **ConfigurationData**](#configurationdata)。</span><span class="sxs-lookup"><span data-stu-id="b31f4-167">You can tell PowerShell DSC that it is okay for credentials toobe outputted in plain text in hello generated node configuration MOFs using [**ConfigurationData**](#configurationdata).</span></span> <span data-ttu-id="b31f4-168">您應該傳遞`PSDscAllowPlainTextPassword = $true`透過**ConfigurationData** hello DSC 組態中會出現，並使用認證的每個節點區塊的名稱。</span><span class="sxs-lookup"><span data-stu-id="b31f4-168">You should pass `PSDscAllowPlainTextPassword = $true` via **ConfigurationData** for each node block’s name that appears in hello DSC configuration and uses credentials.</span></span>

<span data-ttu-id="b31f4-169">hello 下列範例顯示使用自動化認證資產的 DSC 設定。</span><span class="sxs-lookup"><span data-stu-id="b31f4-169">hello following example shows a DSC configuration that uses an Automation credential asset.</span></span>

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

<span data-ttu-id="b31f4-170">您可以編譯上述使用 PowerShell 的 hello DSC 設定。</span><span class="sxs-lookup"><span data-stu-id="b31f4-170">You can compile hello DSC configuration above with PowerShell.</span></span> <span data-ttu-id="b31f4-171">hello PowerShell 底下加入兩個節點組態 toohello Azure Automation DSC 提取伺服器： **CredentialSample.MyVM1**和**CredentialSample.MyVM2**。</span><span class="sxs-lookup"><span data-stu-id="b31f4-171">hello below PowerShell adds two node configurations toohello Azure Automation DSC Pull Server:  **CredentialSample.MyVM1** and **CredentialSample.MyVM2**.</span></span>

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

## <a name="importing-node-configurations"></a><span data-ttu-id="b31f4-172">匯入節點組態</span><span class="sxs-lookup"><span data-stu-id="b31f4-172">Importing node configurations</span></span>

<span data-ttu-id="b31f4-173">您也可以匯入在 Azure 外部完成編譯的節點組態 (MOF)。</span><span class="sxs-lookup"><span data-stu-id="b31f4-173">You can also import node configuratons (MOFs) that you have compiled outside of Azure.</span></span> <span data-ttu-id="b31f4-174">這樣做的優點之一就是可以簽署節點組態。</span><span class="sxs-lookup"><span data-stu-id="b31f4-174">One advantage of this is that node confiturations can be signed.</span></span>
<span data-ttu-id="b31f4-175">帶正負號的節點驗證的設定在本機上受管理的節點 hello DSC 代理程式，確保正在套用的 toohello 節點該 hello 組態來自授權來源。</span><span class="sxs-lookup"><span data-stu-id="b31f4-175">A signed node configuration is verified locally on a managed node by hello DSC agent, ensuring that hello configuration being applied toohello node comes from an authorized source.</span></span>

> [!NOTE]
> <span data-ttu-id="b31f4-176">您可以將簽署的組態匯入到您的 Azure 自動化帳戶，但 Azure 自動化目前不支援編譯簽署的組態。</span><span class="sxs-lookup"><span data-stu-id="b31f4-176">You can use import signed configurations into your Azure Automation account, but Azure Automation does not currently support compiling signed configurations.</span></span>

> [!NOTE]
> <span data-ttu-id="b31f4-177">節點組態檔必須是不能大於 1 MB tooallow 它 toobe 匯入到 Azure 自動化。</span><span class="sxs-lookup"><span data-stu-id="b31f4-177">A node configuration file must be no larger than 1 MB tooallow it toobe imported into Azure Automation.</span></span>

<span data-ttu-id="b31f4-178">您可以了解如何在 https://msdn.microsoft.com/en-us/powershell/wmf/5.1/dsc-improvements#how-to-sign-configuration-and-module toosign 節點設定。</span><span class="sxs-lookup"><span data-stu-id="b31f4-178">You can learn how toosign node configurations at https://msdn.microsoft.com/en-us/powershell/wmf/5.1/dsc-improvements#how-to-sign-configuration-and-module.</span></span>

### <a name="importing-a-node-configuration-in-hello-azure-portal"></a><span data-ttu-id="b31f4-179">匯入 hello Azure 入口網站中的節點設定</span><span class="sxs-lookup"><span data-stu-id="b31f4-179">Importing a node configuration in hello Azure portal</span></span>

1. <span data-ttu-id="b31f4-180">從您的自動化帳戶中，按一下 [DSC 節點組態]。</span><span class="sxs-lookup"><span data-stu-id="b31f4-180">From your Automation account, click **DSC node configurations**.</span></span>

    ![DSC 節點組態](./media/automation-dsc-compile/node-config.png)
2. <span data-ttu-id="b31f4-182">在 hello **DSC 節點組態**刀鋒視窗中，按一下 **新增 NodeConfiguration**。</span><span class="sxs-lookup"><span data-stu-id="b31f4-182">In hello **DSC node configurations** blade, click **Add a NodeConfiguration**.</span></span>
3. <span data-ttu-id="b31f4-183">在 hello**匯入**刀鋒視窗中，按一下 hello 資料夾圖示的 下一步 toohello**節點組態檔**節點組態檔 (MOF) 在本機電腦上的文字方塊中 toobrowse。</span><span class="sxs-lookup"><span data-stu-id="b31f4-183">In hello **Import** blade, click hello folder icon next toohello **Node Configuration File** textbox toobrowse for a node configuration file (MOF) on your local computer.</span></span>

    ![瀏覽本機檔案](./media/automation-dsc-compile/import-browse.png)
4. <span data-ttu-id="b31f4-185">輸入的名稱在 hello**組態名稱**文字方塊。</span><span class="sxs-lookup"><span data-stu-id="b31f4-185">Enter a name in hello **Configuration Name** textbox.</span></span> <span data-ttu-id="b31f4-186">此名稱必須符合 hello hello 組態從中編譯 hello 節點組態名稱。</span><span class="sxs-lookup"><span data-stu-id="b31f4-186">This name must match hello name of hello configuration from which hello node configuration was compiled.</span></span>
5. <span data-ttu-id="b31f4-187">按一下 [確定] 。</span><span class="sxs-lookup"><span data-stu-id="b31f4-187">Click **OK**.</span></span>

### <a name="importing-a-node-configuration-with-powershell"></a><span data-ttu-id="b31f4-188">使用 PowerShell 匯入節點組態</span><span class="sxs-lookup"><span data-stu-id="b31f4-188">Importing a node configuration with PowerShell</span></span>

<span data-ttu-id="b31f4-189">您可以使用 hello[匯入 AzureRmAutomationDscNodeConfiguration](/powershell/module/azurerm.automation/import-azurermautomationdscnodeconfiguration) cmdlet tooimport 到您的自動化帳戶的節點設定。</span><span class="sxs-lookup"><span data-stu-id="b31f4-189">You can use hello [Import-AzureRmAutomationDscNodeConfiguration](/powershell/module/azurerm.automation/import-azurermautomationdscnodeconfiguration) cmdlet tooimport a node configuration into your automation account.</span></span>

```powershell
Import-AzureRmAutomationDscNodeConfiguration -AutomationAccountName "MyAutomationAccount" -ResourceGroupName "MyResourceGroup" -ConfigurationName "MyNodeConfiguration" -Path "C:\MyConfigurations\TestVM1.mof"
```



