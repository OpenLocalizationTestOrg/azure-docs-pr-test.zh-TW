---
title: "aaaValidate Azure 自動化帳戶組態 |Microsoft 文件"
description: "本文說明如何 tooconfirm hello 設定您的自動化帳戶已正確設定。"
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
ms.openlocfilehash: 3a990dcc6661cf67c4b62592ce03d55a3791053a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="test-azure-automation-run-as-account-authentication"></a><span data-ttu-id="4a28c-103">測試 Azure 自動化執行身分帳戶驗證</span><span class="sxs-lookup"><span data-stu-id="4a28c-103">Test Azure Automation Run As account authentication</span></span>
<span data-ttu-id="4a28c-104">已成功建立自動化帳戶之後，您可以執行，就可以簡單測試 tooconfirm toosuccessfully 驗證 Azure 資源管理員或使用您新建立或更新自動化執行身分帳戶的 Azure 傳統部署。</span><span class="sxs-lookup"><span data-stu-id="4a28c-104">After an Automation account is successfully created, you can perform a simple test tooconfirm you are able toosuccessfully authenticate in Azure Resource Manager or Azure classic deployment using your newly created or updated Automation Run As account.</span></span>    

## <a name="automation-run-as-authentication"></a><span data-ttu-id="4a28c-105">自動化執行身分驗證</span><span class="sxs-lookup"><span data-stu-id="4a28c-105">Automation Run As authentication</span></span>
<span data-ttu-id="4a28c-106">使用下列的 hello 範例程式碼太[建立 PowerShell runbook](automation-creating-importing-runbook.md)使用 hello tooverify 驗證執行身分帳戶以及您自訂 runbook tooauthenticate 和管理與您的自動化帳戶的資源管理員資源。</span><span class="sxs-lookup"><span data-stu-id="4a28c-106">Use hello sample code below too[create a PowerShell runbook](automation-creating-importing-runbook.md) tooverify authentication using hello Run As account and also in your custom runbooks tooauthenticate and manage Resource Manager resources with your Automation account.</span></span>   

    $connectionName = "AzureRunAsConnection"
    try
    {
        # Get hello connection "AzureRunAsConnection "
        $servicePrincipalConnection=Get-AutomationConnection -Name $connectionName         

        "Logging in tooAzure..."
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

<span data-ttu-id="4a28c-107">請注意 hello cmdlet 用來驗證在 hello runbook-**新增 AzureRmAccount**，使用 hello *ServicePrincipalCertificate*參數集。</span><span class="sxs-lookup"><span data-stu-id="4a28c-107">Notice hello cmdlet used for authenticating in hello runbook - **Add-AzureRmAccount**, uses hello *ServicePrincipalCertificate* parameter set.</span></span>  <span data-ttu-id="4a28c-108">它藉由使用服務主體憑證 (而非認證) 進行驗證。</span><span class="sxs-lookup"><span data-stu-id="4a28c-108">It authenticates by using service principal certificate, not credentials.</span></span>  

<span data-ttu-id="4a28c-109">當您[執行 hello runbook](automation-starting-a-runbook.md#starting-a-runbook-with-the-azure-portal) toovalidate 您執行身分帳戶， [runbook 工作](automation-runbook-execution.md)是建立，會顯示 hello 作業刀鋒視窗，而 hello 作業狀態顯示在 hello**工作摘要**磚。</span><span class="sxs-lookup"><span data-stu-id="4a28c-109">When you [run hello runbook](automation-starting-a-runbook.md#starting-a-runbook-with-the-azure-portal) toovalidate your Run As account, a [runbook job](automation-runbook-execution.md) is created, hello Job blade is displayed, and hello job status displayed in hello **Job Summary** tile.</span></span> <span data-ttu-id="4a28c-110">hello 工作狀態會做為啟動*排入佇列*表示它正在等待在 hello 雲端 toobecome 可用的 runbook worker。</span><span class="sxs-lookup"><span data-stu-id="4a28c-110">hello job status will start as *Queued* indicating that it is waiting for a runbook worker in hello cloud toobecome available.</span></span> <span data-ttu-id="4a28c-111">它會接著進入太*起始*背景工作宣告 hello 作業時，然後*執行*hello runbook 實際開始執行時。</span><span class="sxs-lookup"><span data-stu-id="4a28c-111">It will then move too*Starting* when a worker claims hello job, and then *Running* when hello runbook actually starts running.</span></span>  <span data-ttu-id="4a28c-112">Hello runbook 工作完成時，我們應該會看到狀態為**已完成**。</span><span class="sxs-lookup"><span data-stu-id="4a28c-112">When hello runbook job completes, we should see a status of **Completed**.</span></span>

<span data-ttu-id="4a28c-113">toosee hello hello runbook 的詳細的結果，請按一下 hello**輸出**磚。</span><span class="sxs-lookup"><span data-stu-id="4a28c-113">toosee hello detailed results of hello runbook, click on hello **Output** tile.</span></span>  <span data-ttu-id="4a28c-114">在 hello**輸出**刀鋒視窗中，您應該會看到已成功地驗證並傳回您的訂用帳戶中的所有資源群組中的所有資源的清單。</span><span class="sxs-lookup"><span data-stu-id="4a28c-114">On hello **Output** blade, you should see it has successfully authenticated and returns a list of all resources in all resource groups in your subscription.</span></span>  

<span data-ttu-id="4a28c-115">請記得 tooremove hello 開頭 hello 註解的程式碼區塊`#Get all ARM resources from all resource groups`重複 hello 程式碼使用您的 runbook。</span><span class="sxs-lookup"><span data-stu-id="4a28c-115">Just remember tooremove hello block of code starting with hello comment `#Get all ARM resources from all resource groups` when you reuse hello code for your runbooks.</span></span>

## <a name="classic-run-as-authentication"></a><span data-ttu-id="4a28c-116">傳統執行身分驗證</span><span class="sxs-lookup"><span data-stu-id="4a28c-116">Classic Run As authentication</span></span>
<span data-ttu-id="4a28c-117">使用下列的 hello 範例程式碼太[建立 PowerShell runbook](automation-creating-importing-runbook.md) tooverify 驗證使用 hello 傳統執行身分帳戶以及您自訂 runbook tooauthenticate 和管理 hello 傳統部署模型中的資源。</span><span class="sxs-lookup"><span data-stu-id="4a28c-117">Use hello sample code below too[create a PowerShell runbook](automation-creating-importing-runbook.md) tooverify authentication using hello Classic Run As account and also in your custom runbooks tooauthenticate and manage resources in hello classic deployment model.</span></span>  

    $ConnectionAssetName = "AzureClassicRunAsConnection"
    # Get hello connection
    $connection = Get-AutomationConnection -Name $connectionAssetName        

    # Authenticate tooAzure with certificate
    Write-Verbose "Get connection asset: $ConnectionAssetName" -Verbose
    $Conn = Get-AutomationConnection -Name $ConnectionAssetName
    if ($Conn -eq $null)
    {
       throw "Could not retrieve connection asset: $ConnectionAssetName. Assure that this asset exists in hello Automation account."
    }

    $CertificateAssetName = $Conn.CertificateAssetName
    Write-Verbose "Getting hello certificate: $CertificateAssetName" -Verbose
    $AzureCert = Get-AutomationCertificate -Name $CertificateAssetName
    if ($AzureCert -eq $null)
    {
       throw "Could not retrieve certificate asset: $CertificateAssetName. Assure that this asset exists in hello Automation account."
    }

    Write-Verbose "Authenticating tooAzure with certificate." -Verbose
    Set-AzureSubscription -SubscriptionName $Conn.SubscriptionName -SubscriptionId $Conn.SubscriptionID -Certificate $AzureCert
    Select-AzureSubscription -SubscriptionId $Conn.SubscriptionID
    
    #Get all VMs in hello subscription and return list with name of each
    Get-AzureVM | ft Name

<span data-ttu-id="4a28c-118">當您[執行 hello runbook](automation-starting-a-runbook.md#starting-a-runbook-with-the-azure-portal) toovalidate 您執行身分帳戶， [runbook 工作](automation-runbook-execution.md)是建立，會顯示 hello 作業刀鋒視窗，而 hello 作業狀態顯示在 hello**工作摘要**磚。</span><span class="sxs-lookup"><span data-stu-id="4a28c-118">When you [run hello runbook](automation-starting-a-runbook.md#starting-a-runbook-with-the-azure-portal) toovalidate your Run As account, a [runbook job](automation-runbook-execution.md) is created, hello Job blade is displayed, and hello job status displayed in hello **Job Summary** tile.</span></span> <span data-ttu-id="4a28c-119">hello 工作狀態會做為啟動*排入佇列*表示它正在等待在 hello 雲端 toobecome 可用的 runbook worker。</span><span class="sxs-lookup"><span data-stu-id="4a28c-119">hello job status will start as *Queued* indicating that it is waiting for a runbook worker in hello cloud toobecome available.</span></span> <span data-ttu-id="4a28c-120">它會接著進入太*起始*背景工作宣告 hello 作業時，然後*執行*hello runbook 實際開始執行時。</span><span class="sxs-lookup"><span data-stu-id="4a28c-120">It will then move too*Starting* when a worker claims hello job, and then *Running* when hello runbook actually starts running.</span></span>  <span data-ttu-id="4a28c-121">Hello runbook 工作完成時，我們應該會看到狀態為**已完成**。</span><span class="sxs-lookup"><span data-stu-id="4a28c-121">When hello runbook job completes, we should see a status of **Completed**.</span></span>

<span data-ttu-id="4a28c-122">toosee hello hello runbook 的詳細的結果，請按一下 hello**輸出**磚。</span><span class="sxs-lookup"><span data-stu-id="4a28c-122">toosee hello detailed results of hello runbook, click on hello **Output** tile.</span></span>  <span data-ttu-id="4a28c-123">在 hello**輸出**刀鋒視窗中，您應該會看到已成功地驗證並傳回 VMName 部署您的訂用帳戶中所有的 Azure Vm 的清單。</span><span class="sxs-lookup"><span data-stu-id="4a28c-123">On hello **Output** blade, you should see it has successfully authenticated and returns a list of all Azure VMs by VMName that are deployed in your subscription.</span></span>  

<span data-ttu-id="4a28c-124">請記得 tooremove hello cmdlet **Get-azurevm**重複 hello 程式碼使用您的 runbook。</span><span class="sxs-lookup"><span data-stu-id="4a28c-124">Just remember tooremove hello cmdlet **Get-AzureVM** when you reuse hello code for your runbooks.</span></span>

## <a name="next-steps"></a><span data-ttu-id="4a28c-125">後續步驟</span><span class="sxs-lookup"><span data-stu-id="4a28c-125">Next steps</span></span>
* <span data-ttu-id="4a28c-126">請參閱 < 開始使用 PowerShell runbook tooget[我的第一個 PowerShell runbook](automation-first-runbook-textual-powershell.md)。</span><span class="sxs-lookup"><span data-stu-id="4a28c-126">tooget started with PowerShell runbooks, see [My first PowerShell runbook](automation-first-runbook-textual-powershell.md).</span></span>
* <span data-ttu-id="4a28c-127">toolearn 詳細資料圖形化撰寫，請參閱[Azure 自動化中的圖形化撰寫](automation-graphical-authoring-intro.md)。</span><span class="sxs-lookup"><span data-stu-id="4a28c-127">toolearn more about Graphical Authoring, see [Graphical authoring in Azure Automation](automation-graphical-authoring-intro.md).</span></span>
