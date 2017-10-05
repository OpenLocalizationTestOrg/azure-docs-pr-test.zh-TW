---
title: "在 Azure 自動化混合式 Runbook 背景工作角色上執行 Runbook | Microsoft Docs"
description: "本文章提供在您的本機資料中心的電腦上執行 Runbook，或使用混合式 Runbook 背景工作角色之雲端提供者的相關資訊。"
services: automation
documentationcenter: 
author: mgoedtel
manager: carmonm
editor: tysonn
ms.assetid: 06227cda-f3d1-47fe-b3f8-436d2b9d81ee
ms.service: automation
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/22/2017
ms.author: magoedte
ms.openlocfilehash: 993bc3ea480a329541ca4ae825189cdb5a2b4a8b
ms.sourcegitcommit: 422efcbac5b6b68295064bd545132fcc98349d01
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/29/2017
---
# <a name="running-runbooks-on-a-hybrid-runbook-worker"></a><span data-ttu-id="dad3f-103">在混合式 Runbook 背景工作角色上執行 Runbook</span><span class="sxs-lookup"><span data-stu-id="dad3f-103">Running runbooks on a Hybrid Runbook Worker</span></span> 
<span data-ttu-id="dad3f-104">在 Azure 自動化和混合式 Runbook 背景工作上執行的 Runbook 結構中沒有任何差異。</span><span class="sxs-lookup"><span data-stu-id="dad3f-104">There is no difference in the structure of runbooks that run in Azure Automation and those that run on a Hybrid Runbook Worker.</span></span> <span data-ttu-id="dad3f-105">您對兩者使用的 Runbook 可能會有顯著差異，因為目標為混合式 Runbook 背景工作角色的 Runbook 通常會自行管理本機電腦上的資源，或針對其所部署之本機環境中的資源，而 Azure 自動化中的 Runbook 通常是管理 Azure 雲端中的資源。</span><span class="sxs-lookup"><span data-stu-id="dad3f-105">Runbooks that you use with each most likely differ significantly though since runbooks targeting a Hybrid Runbook Worker typically manage resources on the local computer itself or against resources in the local environment where it is deployed, while runbooks in Azure Automation typically manage resources in the Azure cloud.</span></span>

<span data-ttu-id="dad3f-106">您可以在 Azure 自動化中編輯混合式 Runbook 背景工作的 Runbook，但如果您嘗試在編輯器中測試 Runbook，可能會遇到困難。</span><span class="sxs-lookup"><span data-stu-id="dad3f-106">You can edit a runbook for Hybrid Runbook Worker in Azure Automation, but you may have difficulties if you try to test the runbook in the editor.</span></span>  <span data-ttu-id="dad3f-107">存取本機資源的 PowerShell 模組可能未安裝在 Azure 自動化環境中，在此情況下，測試就會失敗。</span><span class="sxs-lookup"><span data-stu-id="dad3f-107">The PowerShell modules that access the local resources may not be installed in your Azure Automation environment in which case, the test would fail.</span></span>  <span data-ttu-id="dad3f-108">如果您已安裝所需的模組，就會執行 Runbook，但它不能存取本機資源以進行完整測試。</span><span class="sxs-lookup"><span data-stu-id="dad3f-108">If you do install the required modules, then the runbook will run, but it will not be able to access local resources for a complete test.</span></span>

## <a name="starting-a-runbook-on-hybrid-runbook-worker"></a><span data-ttu-id="dad3f-109">在混合式 Runbook 背景工作角色上啟動 Runbook</span><span class="sxs-lookup"><span data-stu-id="dad3f-109">Starting a runbook on Hybrid Runbook Worker</span></span>
<span data-ttu-id="dad3f-110">[在 Azure 自動化中啟動 Runbook](automation-starting-a-runbook.md) 描述啟動 Runbook 的不同方法。</span><span class="sxs-lookup"><span data-stu-id="dad3f-110">[Starting a Runbook in Azure Automation](automation-starting-a-runbook.md) describes different methods for starting a runbook.</span></span>  <span data-ttu-id="dad3f-111">混合式 Runbook 背景工作加入了 **RunOn** 選項，您可以在其中指定混合式 Runbook 背景工作群組的名稱。</span><span class="sxs-lookup"><span data-stu-id="dad3f-111">Hybrid Runbook Worker adds a **RunOn** option where you can specify the name of a Hybrid Runbook Worker Group.</span></span>  <span data-ttu-id="dad3f-112">如果未指定群組，則會擷取 Runbook，且由該群組中的背景工作執行。</span><span class="sxs-lookup"><span data-stu-id="dad3f-112">If a group is specified, then the runbook is retrieved and run by of the workers in that group.</span></span>  <span data-ttu-id="dad3f-113">如果未指定此選項，則會正常在 Azure 自動化中執行。</span><span class="sxs-lookup"><span data-stu-id="dad3f-113">If this option is not specified, then it is run in Azure Automation as normal.</span></span>

<span data-ttu-id="dad3f-114">在 Azure 入口網站中啟動 Runbook 時，您會看到 [執行於] 選項，您可以在此選取 [Azure] 或 [Hybrid Worker]。</span><span class="sxs-lookup"><span data-stu-id="dad3f-114">When you start a runbook in the Azure portal, you are presented with a **Run on** option where you can select **Azure** or **Hybrid Worker**.</span></span>  <span data-ttu-id="dad3f-115">如果選取 [Hybrid 背景工作角色]，則您可以從下拉式清單中選取群組。</span><span class="sxs-lookup"><span data-stu-id="dad3f-115">If you select **Hybrid Worker**, then you can select the group from a dropdown.</span></span>

<span data-ttu-id="dad3f-116">使用 **RunOn** 參數。</span><span class="sxs-lookup"><span data-stu-id="dad3f-116">Use the **RunOn** parameter.</span></span>  <span data-ttu-id="dad3f-117">您可以使用 Windows PowerShell 以下列命令在 Hybrid Runbook Worker 群組上啟動名為 Test-Runbook 的 Runbook。</span><span class="sxs-lookup"><span data-stu-id="dad3f-117">You can use the following command to start a runbook named Test-Runbook on a Hybrid Runbook Worker Group named MyHybridGroup using Windows PowerShell.</span></span>

    Start-AzureRmAutomationRunbook –AutomationAccountName "MyAutomationAccount" –Name "Test-Runbook" -RunOn "MyHybridGroup"

> [!NOTE]
> <span data-ttu-id="dad3f-118">0.9.1 版 Microsoft Azure PowerShell 的 **Start-AzureAutomationRunbook** Cmdlet 已新增 **RunOn** 參數。</span><span class="sxs-lookup"><span data-stu-id="dad3f-118">The **RunOn** parameter was added to the **Start-AzureAutomationRunbook** cmdlet in version 0.9.1 of Microsoft Azure PowerShell.</span></span>  <span data-ttu-id="dad3f-119">如果您安裝較早的版本，您應該 [下載最新版本](https://azure.microsoft.com/downloads/) 。</span><span class="sxs-lookup"><span data-stu-id="dad3f-119">You should [download the latest version](https://azure.microsoft.com/downloads/) if you have an earlier one installed.</span></span>  <span data-ttu-id="dad3f-120">您只需要在從 Windows PowerShell 啟動 Runbook 的工作站上安裝此版本。</span><span class="sxs-lookup"><span data-stu-id="dad3f-120">You only need to install this version on a workstation where you are starting the runbook from Windows PowerShell.</span></span>  <span data-ttu-id="dad3f-121">您不需要將它安裝在背景工作電腦上，除非您想要從該電腦啟動 Runbook。</span><span class="sxs-lookup"><span data-stu-id="dad3f-121">You do not need to install it on the worker computer unless you intend to start runbooks from that computer.</span></span>  <span data-ttu-id="dad3f-122">您目前無法在混合式 Runbook 背景工作上從另一個 Runbook 啟動 Runbook，因為這項作業需要在您的自動化帳戶中安裝最新版本的 Azure PowerShell。</span><span class="sxs-lookup"><span data-stu-id="dad3f-122">You cannot currently start a runbook on a Hybrid Runbook Worker from another runbook since this would require the latest version of Azure Powershell to be installed in your Automation account.</span></span>  <span data-ttu-id="dad3f-123">Azure 自動化中會自動更新為最新版本，並且很快將其自動往下推送到背景工作角色。</span><span class="sxs-lookup"><span data-stu-id="dad3f-123">The latest version is automatically updated in Azure Automation and automatically pushed down to the workers soon.</span></span>
>
>

## <a name="runbook-permissions"></a><span data-ttu-id="dad3f-124">Runbook 權限</span><span class="sxs-lookup"><span data-stu-id="dad3f-124">Runbook permissions</span></span>
<span data-ttu-id="dad3f-125">在 Hybrid Runbook Worker 上執行的 Runbook 不能使用通常用於 Runbook 對 Azure 資源進行驗證的相同方法，因為它們會存取 Azure 外部的資源。</span><span class="sxs-lookup"><span data-stu-id="dad3f-125">Runbooks running on a Hybrid Runbook Worker cannot use the same method that is typically used for runbooks authenticating to Azure resources, since they are accessing resources outside of Azure.</span></span>  <span data-ttu-id="dad3f-126">Runbook 可以提供自己的驗證給本機資源，或者您可以指定 RunAs 帳戶以對所有 Runbook 提供使用者內容。</span><span class="sxs-lookup"><span data-stu-id="dad3f-126">The runbook can either provide its own authentication to local resources, or you can specify a RunAs account to provide a user context for all runbooks.</span></span>

### <a name="runbook-authentication"></a><span data-ttu-id="dad3f-127">Runbook 驗證</span><span class="sxs-lookup"><span data-stu-id="dad3f-127">Runbook authentication</span></span>
<span data-ttu-id="dad3f-128">根據預設，Runbook 將在內部部署機器上的本機系統帳戶內容中執行，因此，它們必須對將會存取的資源提供自己的驗證。</span><span class="sxs-lookup"><span data-stu-id="dad3f-128">By default, runbooks will run in the context of the local System account on the on-premises computer, so they must provide their own authentication to resources that they will access.</span></span>  

<span data-ttu-id="dad3f-129">您可以在您的 Runbook 中使用[認證](http://msdn.microsoft.com/library/dn940015.aspx)和[憑證](http://msdn.microsoft.com/library/dn940013.aspx)資產，搭配可讓您指定認證的 Cmdlet，您就能夠向不同的資源驗證。</span><span class="sxs-lookup"><span data-stu-id="dad3f-129">You can use [Credential](http://msdn.microsoft.com/library/dn940015.aspx) and [Certificate](http://msdn.microsoft.com/library/dn940013.aspx) assets in your runbook with cmdlets that allow you to specify credentials so you can authenticate to different resources.</span></span>  <span data-ttu-id="dad3f-130">下列範例顯示會重新啟動電腦的 Runbook 的一部分。</span><span class="sxs-lookup"><span data-stu-id="dad3f-130">The following example shows a portion of a runbook that restarts a computer.</span></span>  <span data-ttu-id="dad3f-131">它會從認證資產擷取認證和從變數資產擷取電腦的名稱，然後使用這些值搭配 Restart-Computer Cmdlet。</span><span class="sxs-lookup"><span data-stu-id="dad3f-131">It retrieves credentials from a credential asset and the name of the computer from a variable asset and then uses these values with the Restart-Computer cmdlet.</span></span>

    $Cred = Get-AzureRmAutomationCredential -ResourceGroupName "ResourceGroup01" -Name "MyCredential"
    $Computer = Get-AzureRmAutomationVariable -ResourceGroupName "ResourceGroup01" -Name  "ComputerName"

    Restart-Computer -ComputerName $Computer -Credential $Cred

<span data-ttu-id="dad3f-132">您也可以運用 [InlineScript](automation-powershell-workflow.md#inlinescript)，它可讓您利用 [PSCredential 一般參數](http://technet.microsoft.com/library/jj129719.aspx)指定的認證在另一部電腦上執行程式碼區塊。</span><span class="sxs-lookup"><span data-stu-id="dad3f-132">You can also leverage [InlineScript](automation-powershell-workflow.md#inlinescript), which  allows you to run blocks of code on another computer with credentials specified by the [PSCredential common parameter](http://technet.microsoft.com/library/jj129719.aspx).</span></span>

### <a name="runas-account"></a><span data-ttu-id="dad3f-133">RunAs 帳戶</span><span class="sxs-lookup"><span data-stu-id="dad3f-133">RunAs account</span></span>
<span data-ttu-id="dad3f-134">您不需要讓 Runbook 提供自己的驗證給本機資源，您可以針對混合式背景工作角色群組指定 **RunAs** 帳戶。</span><span class="sxs-lookup"><span data-stu-id="dad3f-134">Instead of having runbooks provide their own authentication to local resources, you can specify a **RunAs** account for a Hybrid worker group.</span></span>  <span data-ttu-id="dad3f-135">您指定具有本機資源存取權的 [認證資產](automation-credentials.md)，在群組中的 Hybrid Runbook Worker 執行時，所有 Runbook 會在這些認證下執行。</span><span class="sxs-lookup"><span data-stu-id="dad3f-135">You specify a [credential asset](automation-credentials.md) that has access to local resources, and all runbooks run under these credentials when running on a Hybrid Runbook Worker in the group.</span></span>  

<span data-ttu-id="dad3f-136">認證的使用者名稱必須是下列格式之一：</span><span class="sxs-lookup"><span data-stu-id="dad3f-136">The user name for the credential must be in one of the following formats:</span></span>

* <span data-ttu-id="dad3f-137">網域\使用者名稱</span><span class="sxs-lookup"><span data-stu-id="dad3f-137">domain\username</span></span>
* username@domain
* <span data-ttu-id="dad3f-138">使用者名稱 (適用於內部部署機器的本機帳戶)</span><span class="sxs-lookup"><span data-stu-id="dad3f-138">username (for accounts local to the on-premises computer)</span></span>

<span data-ttu-id="dad3f-139">使用下列程序以針對混合式背景工作角色群組指定 RunAs 帳戶：</span><span class="sxs-lookup"><span data-stu-id="dad3f-139">Use the following procedure to specify a RunAs account for a Hybrid worker group:</span></span>

1. <span data-ttu-id="dad3f-140">建立具有本機資源存取權的 [認證資產](automation-credentials.md) 。</span><span class="sxs-lookup"><span data-stu-id="dad3f-140">Create a [credential asset](automation-credentials.md) with access to local resources.</span></span>
2. <span data-ttu-id="dad3f-141">在 Azure 入口網站中，開啟自動化帳戶。</span><span class="sxs-lookup"><span data-stu-id="dad3f-141">Open the Automation account in the Azure portal.</span></span>
3. <span data-ttu-id="dad3f-142">選取 [Hybrid Worker 群組]  圖格，然後選取群組。</span><span class="sxs-lookup"><span data-stu-id="dad3f-142">Select the **Hybrid Worker Groups** tile, and then select the group.</span></span>
4. <span data-ttu-id="dad3f-143">選取 [所有設定]，然後選取 [Hybrid 背景工作角色群組設定]。</span><span class="sxs-lookup"><span data-stu-id="dad3f-143">Select **All settings** and then **Hybrid worker group settings**.</span></span>
5. <span data-ttu-id="dad3f-144">將 [執行身分] 從 [預設] 變更為 [自訂]。</span><span class="sxs-lookup"><span data-stu-id="dad3f-144">Change **Run As** from **Default** to **Custom**.</span></span>
6. <span data-ttu-id="dad3f-145">選取認證，然後按一下 [儲存] 。</span><span class="sxs-lookup"><span data-stu-id="dad3f-145">Select the credential and click **Save**.</span></span>

### <a name="automation-run-as-account"></a><span data-ttu-id="dad3f-146">自動化執行身分帳戶</span><span class="sxs-lookup"><span data-stu-id="dad3f-146">Automation Run As account</span></span>
<span data-ttu-id="dad3f-147">在 Azure 中部署資源的自動化建置流程中，您可能需要存取內部部署系統來支援部署序列中的工作或一組步驟。</span><span class="sxs-lookup"><span data-stu-id="dad3f-147">As part of your automated build process for deploying resources in Azure, you may require access to on-premise systems to support a task or set of steps in your deployment sequence.</span></span>  <span data-ttu-id="dad3f-148">若要支援使用「執行身分」帳戶向 Azure 驗證，您需要安裝「執行身分」帳戶憑證。</span><span class="sxs-lookup"><span data-stu-id="dad3f-148">To support authentication against Azure using the Run As account, you need to install the Run As account certificate.</span></span>  

<span data-ttu-id="dad3f-149">下列 PowerShell Runbook *Export-RunAsCertificateToHybridWorker* 會從 Azure 自動化帳戶匯出執行身分憑證，並將它下載和匯入 Hybird 背景工作角色 (連線至相同帳戶) 的本機憑證存放區。</span><span class="sxs-lookup"><span data-stu-id="dad3f-149">The following PowerShell runbook, *Export-RunAsCertificateToHybridWorker*, exports the Run As certificate from your Azure Automation account and downloads and imports it into the local machine certificate store on a Hybrid worker connected to the same account.</span></span>  <span data-ttu-id="dad3f-150">完成該步驟後，它會確認背景工作角色可以使用執行身分帳戶成功向 Azure 驗證。</span><span class="sxs-lookup"><span data-stu-id="dad3f-150">Once that step is completed, it verifies the worker can successfully authenticate to Azure using the Run As account.</span></span>

    <#PSScriptInfo
    .VERSION 1.0
    .GUID 3a796b9a-623d-499d-86c8-c249f10a6986
    .AUTHOR Azure Automation Team
    .COMPANYNAME Microsoft
    .COPYRIGHT 
    .TAGS Azure Automation 
    .LICENSEURI 
    .PROJECTURI 
    .ICONURI 
    .EXTERNALMODULEDEPENDENCIES 
    .REQUIREDSCRIPTS 
    .EXTERNALSCRIPTDEPENDENCIES 
    .RELEASENOTES
    #>

    <#  
    .SYNOPSIS  
    Exports the Run As certificate from an Azure Automation account to a hybrid worker in that account. 
  
    .DESCRIPTION  
    This runbook exports the Run As certificate from an Azure Automation account to a hybrid worker in that account.
    Run this runbook in the hybrid worker where you want the certificate installed.
    This allows the use of the AzureRunAsConnection to authenticate to Azure and manage Azure resources from runbooks running in the hybrid worker.

    .EXAMPLE
    .\Export-RunAsCertificateToHybridWorker

    .NOTES
    AUTHOR: Azure Automation Team 
    LASTEDIT: 2016.10.13
    #>

    [OutputType([string])] 

    # Set the password used for this certificate
    $Password = "YourStrongPasswordForTheCert"

    # Stop on errors
    $ErrorActionPreference = 'stop'

    # Get the management certificate that will be used to make calls into Azure Service Management resources
    $RunAsCert = Get-AutomationCertificate -Name "AzureRunAsCertificate"
       
    # location to store temporary certificate in the Automation service host
    $CertPath = Join-Path $env:temp  "AzureRunAsCertificate.pfx"
   
    # Save the certificate
    $Cert = $RunAsCert.Export("pfx",$Password)
    Set-Content -Value $Cert -Path $CertPath -Force -Encoding Byte | Write-Verbose 

    Write-Output ("Importing certificate into $env:computername local machine root store from " + $CertPath)
    $SecurePassword = ConvertTo-SecureString $Password -AsPlainText -Force
    Import-PfxCertificate -FilePath $CertPath -CertStoreLocation Cert:\LocalMachine\My -Password $SecurePassword -Exportable | Write-Verbose

    # Test that authentication to Azure Resource Manager is working
    $RunAsConnection = Get-AutomationConnection -Name "AzureRunAsConnection" 
    
    Add-AzureRmAccount `
      -ServicePrincipal `
      -TenantId $RunAsConnection.TenantId `
      -ApplicationId $RunAsConnection.ApplicationId `
      -CertificateThumbprint $RunAsConnection.CertificateThumbprint | Write-Verbose

    Set-AzureRmContext -SubscriptionId $RunAsConnection.SubscriptionID | Write-Verbose

    # List automation accounts to confirm Azure Resource Manager calls are working
    Get-AzureRmAutomationAccount | Select AutomationAccountName

<span data-ttu-id="dad3f-151">將 *Export-RunAsCertificateToHybridWorker* Runbook 以 `.ps1` 副檔名儲存至您的電腦。</span><span class="sxs-lookup"><span data-stu-id="dad3f-151">Save the *Export-RunAsCertificateToHybridWorker* runbook to your computer with a `.ps1` extension.</span></span>  <span data-ttu-id="dad3f-152">將它匯入您的自動化帳戶，並編輯 Runbook，將變數 `$Password` 的值變更為您自己的密碼。</span><span class="sxs-lookup"><span data-stu-id="dad3f-152">Import it into your Automation account and edit the runbook, changing the value of the variable `$Password` with your own password.</span></span>  <span data-ttu-id="dad3f-153">發佈 Runbook，然後以使用「執行身分」帳戶執行和驗證 Runbook 的 Hybrid Worker 群組為對象，執行 Runbook。</span><span class="sxs-lookup"><span data-stu-id="dad3f-153">Publish and then run the runbook targeting the Hybrid Worker group that run and authenticate runbooks using the Run As account.</span></span>  <span data-ttu-id="dad3f-154">作業資料流會報告將憑證匯入本機電腦存放區的嘗試，後面還會出現幾行，根據訂用帳戶中定義多少自動化帳戶和驗證是否成功而定。</span><span class="sxs-lookup"><span data-stu-id="dad3f-154">The job stream reports the attempt to import the certificate into the local machine store, and follows with multiple lines depending on how many Automation accounts are defined in your subscription and if authentication is successful.</span></span>  

## <a name="troubleshooting-runbooks-on-hybrid-runbook-worker"></a><span data-ttu-id="dad3f-155">在 Hybrid Runbook Worker 上進行 Runbook 疑難排解</span><span class="sxs-lookup"><span data-stu-id="dad3f-155">Troubleshooting runbooks on Hybrid Runbook Worker</span></span>
<span data-ttu-id="dad3f-156">記錄檔儲存每一個混合式背景工作角色本機的 C:\ProgramData\Microsoft\System Center\Orchestrator\7.2\SMA\Sandboxes 中。</span><span class="sxs-lookup"><span data-stu-id="dad3f-156">Logs are stored locally on each hybrid worker at C:\ProgramData\Microsoft\System Center\Orchestrator\7.2\SMA\Sandboxes.</span></span>  <span data-ttu-id="dad3f-157">混合式背景工作角色也會將錯誤和事件記錄在 Windows 事件記錄的 **Application and Services Logs\Microsoft-SMA\Operational** 底下。</span><span class="sxs-lookup"><span data-stu-id="dad3f-157">Hybrid worker also records errors and events in the Windows event log under **Application and Services Logs\Microsoft-SMA\Operational**.</span></span>  <span data-ttu-id="dad3f-158">背景工作上執行的 Runbook 相關事件會寫入 **Application and Services Logs\Microsoft-Automation\Operational** 底下。</span><span class="sxs-lookup"><span data-stu-id="dad3f-158">Events related to runbooks executed on the worker are written to **Application and Services Logs\Microsoft-Automation\Operational**.</span></span>  <span data-ttu-id="dad3f-159">**Microsoft SMA** 記錄中包含的許多事件，是與推送至背景工作和處理 Runbook 的 Runbook 作業相關。</span><span class="sxs-lookup"><span data-stu-id="dad3f-159">The **Microsoft-SMA** log includes many more events related to the runbook job pushed to the worker and the processing of the runbook.</span></span>  <span data-ttu-id="dad3f-160">雖然 **Microsoft 自動化**事件記錄並沒有許多事件具有可協助針對 Runbook 執行進行疑難排解的詳細資料，您至少會找到 Runbook 作業的結果。</span><span class="sxs-lookup"><span data-stu-id="dad3f-160">While the **Microsoft-Automation** event log does not have many events with details assisting with the troubleshooting of runbook execution, you will at least find the results of the runbook job.</span></span>  

<span data-ttu-id="dad3f-161">[Runbook 輸出和訊息](automation-runbook-output-and-messages.md) 會從混合式背景工作角色傳送到 Azure 自動化，就像雲端中執行的 Runbook 工作一樣。</span><span class="sxs-lookup"><span data-stu-id="dad3f-161">[Runbook output and messages](automation-runbook-output-and-messages.md) are sent to Azure Automation from hybrid workers just like runbook jobs run in the cloud.</span></span>  <span data-ttu-id="dad3f-162">您也可以啟用詳細資訊和進度資料流，就像您在其他 Runbook 中的作法一樣。</span><span class="sxs-lookup"><span data-stu-id="dad3f-162">You can also enable the Verbose and Progress streams the same way you would for other runbooks.</span></span>  

<span data-ttu-id="dad3f-163">如果您的 Runbook 未成功完成，但作業摘要顯示 [暫止]  狀態，請檢閱疑難排解文章 [Hybrid Runbook Worker：Runbook 作業在暫止狀態下終止](automation-troubleshooting-hybrid-runbook-worker.md#a-runbook-job-terminates-with-a-status-of-suspended)。</span><span class="sxs-lookup"><span data-stu-id="dad3f-163">If your runbooks are not completing successfully and the job summary shows a status of **Suspended**, please review the troubleshooting article [Hybrid Runbook Worker: A runbook job terminates with a status of Suspended](automation-troubleshooting-hybrid-runbook-worker.md#a-runbook-job-terminates-with-a-status-of-suspended).</span></span>   

## <a name="next-steps"></a><span data-ttu-id="dad3f-164">後續步驟</span><span class="sxs-lookup"><span data-stu-id="dad3f-164">Next steps</span></span>
* <span data-ttu-id="dad3f-165">若要深入了解可用來啟動 Runbook 的不同方法，請參閱[在 Azure 自動化中啟動 Runbook](automation-starting-a-runbook.md)。</span><span class="sxs-lookup"><span data-stu-id="dad3f-165">To learn more about the different methods that can be used to start a runbook, see [Starting a Runbook in Azure Automation](automation-starting-a-runbook.md).</span></span>  
* <span data-ttu-id="dad3f-166">若要了解使用文字式編輯器在 Azure 自動化中使用 PowerShell 和 PowerShell 工作流程 Runbook 的不同程序，請參閱 [在 Azure 自動化中編輯 Runbook](automation-edit-textual-runbook.md)</span><span class="sxs-lookup"><span data-stu-id="dad3f-166">To understand the different procedures for working with PowerShell and PowerShell Workflow runbooks in Azure Automation using the textual editor, see [Editing a Runbook in Azure Automation](automation-edit-textual-runbook.md)</span></span>