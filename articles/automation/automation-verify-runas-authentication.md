---
title: "驗證 Azure 自動化帳戶組態 | Microsoft Docs"
description: "本文說明如何確認已正確設定您的自動化帳戶組態。"
services: automation
documentationcenter: 
author: mgoedtel
manager: carmonm
editor: 
ms.assetid: 
ms.service: automation
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 08/07/2017
ms.author: magoedte
ms.openlocfilehash: 804e05f596e1d6d5f650e4c94a18eff6b7c3ba4e
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/18/2017
---
# <a name="test-azure-automation-run-as-account-authentication"></a><span data-ttu-id="dc78c-103">測試 Azure 自動化執行身分帳戶驗證</span><span class="sxs-lookup"><span data-stu-id="dc78c-103">Test Azure Automation Run As account authentication</span></span>
<span data-ttu-id="dc78c-104">成功建立自動化帳戶之後，您可以執行簡單的測試，確認您能夠在 Azure Resource Manager 或 Azure 傳統部署中使用新建立或已更新的自動化執行身分帳戶成功進行驗證。</span><span class="sxs-lookup"><span data-stu-id="dc78c-104">After an Automation account is successfully created, you can perform a simple test to confirm you are able to successfully authenticate in Azure Resource Manager or Azure classic deployment using your newly created or updated Automation Run As account.</span></span>    

## <a name="automation-run-as-authentication"></a><span data-ttu-id="dc78c-105">自動化執行身分驗證</span><span class="sxs-lookup"><span data-stu-id="dc78c-105">Automation Run As authentication</span></span>
<span data-ttu-id="dc78c-106">使用下面範例程式碼來[建立 PowerShell Runbook](automation-creating-importing-runbook.md)，以使用執行身分帳戶進行驗證，並且同時在自訂 Runbook 中使用您的自動化帳戶驗證及管理 Resource Manage 資源。</span><span class="sxs-lookup"><span data-stu-id="dc78c-106">Use the sample code below to [create a PowerShell runbook](automation-creating-importing-runbook.md) to verify authentication using the Run As account and also in your custom runbooks to authenticate and manage Resource Manager resources with your Automation account.</span></span>   

    $connectionName = "AzureRunAsConnection"
    try
    {
        # Get the connection "AzureRunAsConnection "
        $servicePrincipalConnection=Get-AutomationConnection -Name $connectionName         

        "Logging in to Azure..."
        Add-AzureRmAccount `
           -ServicePrincipal `
           -TenantId $servicePrincipalConnection.TenantId `
           -ApplicationId $servicePrincipalConnection.ApplicationId `
           -CertificateThumbprint $servicePrincipalConnection.CertificateThumbprint 
    }
    catch {
       if (!$servicePrincipalConnection)
       {
          $ErrorMessage = "Connection $connectionName not found."
          throw $ErrorMessage
      } else{
          Write-Error -Message $_.Exception
          throw $_.Exception
      }
    }

    #Get all ARM resources from all resource groups
    $ResourceGroups = Get-AzureRmResourceGroup 

    foreach ($ResourceGroup in $ResourceGroups)
    {    
       Write-Output ("Showing resources in resource group " + $ResourceGroup.ResourceGroupName)
       $Resources = Find-AzureRmResource -ResourceGroupNameContains $ResourceGroup.ResourceGroupName | Select ResourceName, ResourceType
       ForEach ($Resource in $Resources)
       {
          Write-Output ($Resource.ResourceName + " of type " +  $Resource.ResourceType)
       }
       Write-Output ("")
    } 

<span data-ttu-id="dc78c-107">請注意，Runbook 中用來驗證的 Cmdlet (**Add-AzureRmAccount**) 會使用 ServicePrincipalCertificate 參數集。</span><span class="sxs-lookup"><span data-stu-id="dc78c-107">Notice the cmdlet used for authenticating in the runbook - **Add-AzureRmAccount**, uses the *ServicePrincipalCertificate* parameter set.</span></span>  <span data-ttu-id="dc78c-108">它藉由使用服務主體憑證 (而非認證) 進行驗證。</span><span class="sxs-lookup"><span data-stu-id="dc78c-108">It authenticates by using service principal certificate, not credentials.</span></span>  

<span data-ttu-id="dc78c-109">當您**執行 Runbook** 來驗證您的執行身分帳戶時，已建立 [Runbook 作業](automation-starting-a-runbook.md#starting-a-runbook-with-the-azure-portal)、顯示 [作業] 刀鋒視窗，而作業狀態會顯示在 [作業摘要][](automation-runbook-execution.md) 圖格中。</span><span class="sxs-lookup"><span data-stu-id="dc78c-109">When you [run the runbook](automation-starting-a-runbook.md#starting-a-runbook-with-the-azure-portal) to validate your Run As account, a [runbook job](automation-runbook-execution.md) is created, the Job blade is displayed, and the job status displayed in the **Job Summary** tile.</span></span> <span data-ttu-id="dc78c-110">作業狀態一開始會顯示為 [已排入佇列]  ，表示其正在等候雲端中的 Runbook 背景工作變為可用狀態。</span><span class="sxs-lookup"><span data-stu-id="dc78c-110">The job status will start as *Queued* indicating that it is waiting for a runbook worker in the cloud to become available.</span></span> <span data-ttu-id="dc78c-111">然後當背景工作宣告該工作時，狀態將變更為 [正在開始]，然後 Runbook 實際開始執行時再變更為 [執行中]。</span><span class="sxs-lookup"><span data-stu-id="dc78c-111">It will then move to *Starting* when a worker claims the job, and then *Running* when the runbook actually starts running.</span></span>  <span data-ttu-id="dc78c-112">Runbook 作業完成時，我們應該會看到 [完成] 狀態。</span><span class="sxs-lookup"><span data-stu-id="dc78c-112">When the runbook job completes, we should see a status of **Completed**.</span></span>

<span data-ttu-id="dc78c-113">若要查看 Runbook 的詳細結果，請按一下 [輸出]  圖格。</span><span class="sxs-lookup"><span data-stu-id="dc78c-113">To see the detailed results of the runbook, click on the **Output** tile.</span></span>  <span data-ttu-id="dc78c-114">在 [輸出] 刀鋒視窗上，您應會看到它已成功驗證並傳回您的訂用帳戶中所有資源群組中的所有資源清單。</span><span class="sxs-lookup"><span data-stu-id="dc78c-114">On the **Output** blade, you should see it has successfully authenticated and returns a list of all resources in all resource groups in your subscription.</span></span>  

<span data-ttu-id="dc78c-115">當您對 Runbook 重複使用程式碼時，請記得移除以 `#Get all ARM resources from all resource groups` 註解開頭的程式碼區塊。</span><span class="sxs-lookup"><span data-stu-id="dc78c-115">Just remember to remove the block of code starting with the comment `#Get all ARM resources from all resource groups` when you reuse the code for your runbooks.</span></span>

## <a name="classic-run-as-authentication"></a><span data-ttu-id="dc78c-116">傳統執行身分驗證</span><span class="sxs-lookup"><span data-stu-id="dc78c-116">Classic Run As authentication</span></span>
<span data-ttu-id="dc78c-117">使用下面範例程式碼來[建立 PowerShell Runbook](automation-creating-importing-runbook.md)，以使用傳統執行身分帳戶進行驗證，並且同時在自訂 Runbook 中驗證及管理傳統部署模型中的資源。</span><span class="sxs-lookup"><span data-stu-id="dc78c-117">Use the sample code below to [create a PowerShell runbook](automation-creating-importing-runbook.md) to verify authentication using the Classic Run As account and also in your custom runbooks to authenticate and manage resources in the classic deployment model.</span></span>  

    $ConnectionAssetName = "AzureClassicRunAsConnection"
    # Get the connection
    $connection = Get-AutomationConnection -Name $connectionAssetName        

    # Authenticate to Azure with certificate
    Write-Verbose "Get connection asset: $ConnectionAssetName" -Verbose
    $Conn = Get-AutomationConnection -Name $ConnectionAssetName
    if ($Conn -eq $null)
    {
       throw "Could not retrieve connection asset: $ConnectionAssetName. Assure that this asset exists in the Automation account."
    }

    $CertificateAssetName = $Conn.CertificateAssetName
    Write-Verbose "Getting the certificate: $CertificateAssetName" -Verbose
    $AzureCert = Get-AutomationCertificate -Name $CertificateAssetName
    if ($AzureCert -eq $null)
    {
       throw "Could not retrieve certificate asset: $CertificateAssetName. Assure that this asset exists in the Automation account."
    }

    Write-Verbose "Authenticating to Azure with certificate." -Verbose
    Set-AzureSubscription -SubscriptionName $Conn.SubscriptionName -SubscriptionId $Conn.SubscriptionID -Certificate $AzureCert
    Select-AzureSubscription -SubscriptionId $Conn.SubscriptionID
    
    #Get all VMs in the subscription and return list with name of each
    Get-AzureVM | ft Name

<span data-ttu-id="dc78c-118">當您**執行 Runbook** 來驗證您的執行身分帳戶時，已建立 [Runbook 作業](automation-starting-a-runbook.md#starting-a-runbook-with-the-azure-portal)、顯示 [作業] 刀鋒視窗，而作業狀態會顯示在 [作業摘要][](automation-runbook-execution.md) 圖格中。</span><span class="sxs-lookup"><span data-stu-id="dc78c-118">When you [run the runbook](automation-starting-a-runbook.md#starting-a-runbook-with-the-azure-portal) to validate your Run As account, a [runbook job](automation-runbook-execution.md) is created, the Job blade is displayed, and the job status displayed in the **Job Summary** tile.</span></span> <span data-ttu-id="dc78c-119">作業狀態一開始會顯示為 [已排入佇列]  ，表示其正在等候雲端中的 Runbook 背景工作變為可用狀態。</span><span class="sxs-lookup"><span data-stu-id="dc78c-119">The job status will start as *Queued* indicating that it is waiting for a runbook worker in the cloud to become available.</span></span> <span data-ttu-id="dc78c-120">然後當背景工作宣告該工作時，狀態將變更為 [正在開始]，然後 Runbook 實際開始執行時再變更為 [執行中]。</span><span class="sxs-lookup"><span data-stu-id="dc78c-120">It will then move to *Starting* when a worker claims the job, and then *Running* when the runbook actually starts running.</span></span>  <span data-ttu-id="dc78c-121">Runbook 作業完成時，我們應該會看到 [完成] 狀態。</span><span class="sxs-lookup"><span data-stu-id="dc78c-121">When the runbook job completes, we should see a status of **Completed**.</span></span>

<span data-ttu-id="dc78c-122">若要查看 Runbook 的詳細結果，請按一下 [輸出]  圖格。</span><span class="sxs-lookup"><span data-stu-id="dc78c-122">To see the detailed results of the runbook, click on the **Output** tile.</span></span>  <span data-ttu-id="dc78c-123">在 [輸出] 刀鋒視窗上，您應會看到它已驗證成功並傳回您訂用帳戶中部署的所有 Azure VM 清單 (依 VMName 列出)。</span><span class="sxs-lookup"><span data-stu-id="dc78c-123">On the **Output** blade, you should see it has successfully authenticated and returns a list of all Azure VMs by VMName that are deployed in your subscription.</span></span>  

<span data-ttu-id="dc78c-124">當您對 Runbook 重複使用程式碼時，請記得移除 **Get-AzureVM** Cmdlet。</span><span class="sxs-lookup"><span data-stu-id="dc78c-124">Just remember to remove the cmdlet **Get-AzureVM** when you reuse the code for your runbooks.</span></span>

## <a name="next-steps"></a><span data-ttu-id="dc78c-125">後續步驟</span><span class="sxs-lookup"><span data-stu-id="dc78c-125">Next steps</span></span>
* <span data-ttu-id="dc78c-126">若要開始使用 PowerShell Runbook，請參閱[我的第一個 PowerShell Runbook](automation-first-runbook-textual-powershell.md)。</span><span class="sxs-lookup"><span data-stu-id="dc78c-126">To get started with PowerShell runbooks, see [My first PowerShell runbook](automation-first-runbook-textual-powershell.md).</span></span>
* <span data-ttu-id="dc78c-127">若要深入了解圖形化編寫，請參閱 [Azure 自動化中的圖形化編寫](automation-graphical-authoring-intro.md)。</span><span class="sxs-lookup"><span data-stu-id="dc78c-127">To learn more about Graphical Authoring, see [Graphical authoring in Azure Automation](automation-graphical-authoring-intro.md).</span></span>
