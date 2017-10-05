---
title: "針對本機 Service Fabric 叢集設定進行疑難排解 | Microsoft Azure"
description: "本文涵蓋了一組疑難排解本機開發叢集的建議"
services: service-fabric
documentationcenter: .net
author: mikkelhegn
manager: timlt
editor: 
ms.assetid: 97f4feaa-bba0-47af-8fdd-07f811fe2202
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/07/2017
ms.author: mikkelhegn
ms.openlocfilehash: aa393f884b564cee81fcf75cc2eff895efea9471
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="troubleshoot-your-local-development-cluster-setup"></a><span data-ttu-id="e7782-103">疑難排解本機開發叢集設定</span><span class="sxs-lookup"><span data-stu-id="e7782-103">Troubleshoot your local development cluster setup</span></span>
<span data-ttu-id="e7782-104">如果您在與本機 Azure Service Fabric 開發叢集互動時遇到問題，請檢閱下列建議，以尋求可能的解決方法。</span><span class="sxs-lookup"><span data-stu-id="e7782-104">If you run into an issue while interacting with your local Azure Service Fabric development cluster, review the following suggestions for potential solutions.</span></span>

## <a name="cluster-setup-failures"></a><span data-ttu-id="e7782-105">叢集設定失敗</span><span class="sxs-lookup"><span data-stu-id="e7782-105">Cluster setup failures</span></span>
### <a name="cannot-clean-up-service-fabric-logs"></a><span data-ttu-id="e7782-106">無法清除 Service Fabric 記錄檔</span><span class="sxs-lookup"><span data-stu-id="e7782-106">Cannot clean up Service Fabric logs</span></span>
#### <a name="problem"></a><span data-ttu-id="e7782-107">問題</span><span class="sxs-lookup"><span data-stu-id="e7782-107">Problem</span></span>
<span data-ttu-id="e7782-108">執行 DevClusterSetup 指令碼時，看到類似以下錯誤：</span><span class="sxs-lookup"><span data-stu-id="e7782-108">While running the DevClusterSetup script, you see an error like this:</span></span>

    Cannot clean up C:\SfDevCluster\Log fully as references are likely being held to items in it. Please remove those and run this script again.
    At line:1 char:1 + .\DevClusterSetup.ps1
    + ~~~~~~~~~~~~~~~~~~~~~
    + CategoryInfo : NotSpecified: (:) [Write-Error], WriteErrorException
    + FullyQualifiedErrorId : Microsoft.PowerShell.Commands.WriteErrorException,DevClusterSetup.ps1


#### <a name="solution"></a><span data-ttu-id="e7782-109">方案</span><span class="sxs-lookup"><span data-stu-id="e7782-109">Solution</span></span>
<span data-ttu-id="e7782-110">關閉目前的 Powershell 視窗，並以系統管理員身分開啟新的 Powershell 視窗。</span><span class="sxs-lookup"><span data-stu-id="e7782-110">Close the current PowerShell window and open a new PowerShell window as an administrator.</span></span> <span data-ttu-id="e7782-111">您現在應該能夠成功執行指令碼。</span><span class="sxs-lookup"><span data-stu-id="e7782-111">You should now be able to successfully run the script.</span></span>

## <a name="cluster-connection-failures"></a><span data-ttu-id="e7782-112">叢集連接失敗</span><span class="sxs-lookup"><span data-stu-id="e7782-112">Cluster connection failures</span></span>
### <a name="service-fabric-powershell-cmdlets-are-not-recognized-in-azure-powershell"></a><span data-ttu-id="e7782-113">在 Azure PowerShell 中無法辨識 Service Fabric PowerShell Cmdlet</span><span class="sxs-lookup"><span data-stu-id="e7782-113">Service Fabric PowerShell cmdlets are not recognized in Azure PowerShell</span></span>
#### <a name="problem"></a><span data-ttu-id="e7782-114">問題</span><span class="sxs-lookup"><span data-stu-id="e7782-114">Problem</span></span>
<span data-ttu-id="e7782-115">如果您嘗試執行任何 Service Fabric PowerShell Cmdlet (例如，在 Azure PowerShell 視窗中執行 `Connect-ServiceFabricCluster` )，它將會失敗，並指出無法辨識此 Cmdlet。</span><span class="sxs-lookup"><span data-stu-id="e7782-115">If you try to run any of the Service Fabric PowerShell cmdlets, such as `Connect-ServiceFabricCluster` in an Azure PowerShell window, it fails, saying that the cmdlet is not recognized.</span></span> <span data-ttu-id="e7782-116">這是因為 Azure PowerShell 使用 32 位元版本的 Windows PowerShell (即使是在 64 位元作業系統版本上)，而 Service Fabric Cmdlet 只能在 64 位元環境中運作。</span><span class="sxs-lookup"><span data-stu-id="e7782-116">The reason for this is that Azure PowerShell uses the 32-bit version of Windows PowerShell (even on 64-bit OS versions), whereas the Service Fabric cmdlets only work in 64-bit environments.</span></span>

#### <a name="solution"></a><span data-ttu-id="e7782-117">方案</span><span class="sxs-lookup"><span data-stu-id="e7782-117">Solution</span></span>
<span data-ttu-id="e7782-118">一律直接從 Windows PowerShell 執行 Service Fabric Cmdlet。</span><span class="sxs-lookup"><span data-stu-id="e7782-118">Always run Service Fabric cmdlets directly from Windows PowerShell.</span></span>

> [!NOTE]
> <span data-ttu-id="e7782-119">最新版的 Azure PowerShell 不會建立特殊捷徑，因此這不會再出現。</span><span class="sxs-lookup"><span data-stu-id="e7782-119">The latest version of Azure PowerShell does not create a special shortcut, so this should no longer occur.</span></span>
> 
> 

### <a name="type-initialization-exception"></a><span data-ttu-id="e7782-120">類型初始化例外狀況</span><span class="sxs-lookup"><span data-stu-id="e7782-120">Type Initialization exception</span></span>
#### <a name="problem"></a><span data-ttu-id="e7782-121">問題</span><span class="sxs-lookup"><span data-stu-id="e7782-121">Problem</span></span>
<span data-ttu-id="e7782-122">在 PowerShell 中連線到叢集時，看到 System.Fabric.Common.AppTrace 的 TypeInitializationException 錯誤。</span><span class="sxs-lookup"><span data-stu-id="e7782-122">When you are connecting to the cluster in PowerShell, you see the error TypeInitializationException for System.Fabric.Common.AppTrace.</span></span>

#### <a name="solution"></a><span data-ttu-id="e7782-123">方案</span><span class="sxs-lookup"><span data-stu-id="e7782-123">Solution</span></span>
<span data-ttu-id="e7782-124">在安裝期間未正確設定路徑變數。</span><span class="sxs-lookup"><span data-stu-id="e7782-124">Your path variable was not correctly set during installation.</span></span> <span data-ttu-id="e7782-125">登出 Windows，再重新登入。</span><span class="sxs-lookup"><span data-stu-id="e7782-125">Sign out of Windows and sign back in.</span></span> <span data-ttu-id="e7782-126">這會重新整理您的路徑。</span><span class="sxs-lookup"><span data-stu-id="e7782-126">This refreshes your path.</span></span>

### <a name="cluster-connection-fails-with-object-is-closed"></a><span data-ttu-id="e7782-127">叢集連接失敗，且出現「物件已關閉」</span><span class="sxs-lookup"><span data-stu-id="e7782-127">Cluster connection fails with "Object is closed"</span></span>
#### <a name="problem"></a><span data-ttu-id="e7782-128">問題</span><span class="sxs-lookup"><span data-stu-id="e7782-128">Problem</span></span>
<span data-ttu-id="e7782-129">呼叫 Connect-ServiceFabricCluster 失敗，且出現類似以下錯誤：</span><span class="sxs-lookup"><span data-stu-id="e7782-129">A call to Connect-ServiceFabricCluster fails with an error like this:</span></span>

    Connect-ServiceFabricCluster : The object is closed.
    At line:1 char:1
    + Connect-ServiceFabricCluster
    + ~~~~~~~~~~~~~~~~~~~~~~~~~~~~
    + CategoryInfo : InvalidOperation: (:) [Connect-ServiceFabricCluster], FabricObjectClosedException
    + FullyQualifiedErrorId : CreateClusterConnectionErrorId,Microsoft.ServiceFabric.Powershell.ConnectCluster

#### <a name="solution"></a><span data-ttu-id="e7782-130">方案</span><span class="sxs-lookup"><span data-stu-id="e7782-130">Solution</span></span>
<span data-ttu-id="e7782-131">關閉目前的 Powershell 視窗，並以系統管理員身分開啟新的 Powershell 視窗。</span><span class="sxs-lookup"><span data-stu-id="e7782-131">Close the current PowerShell window and open a new PowerShell window as an administrator.</span></span> <span data-ttu-id="e7782-132">您現在應該能夠成功連接。</span><span class="sxs-lookup"><span data-stu-id="e7782-132">You should now be able to successfully connect.</span></span>

### <a name="fabric-connection-denied-exception"></a><span data-ttu-id="e7782-133">拒絕網狀架構連線例外狀況</span><span class="sxs-lookup"><span data-stu-id="e7782-133">Fabric Connection Denied exception</span></span>
#### <a name="problem"></a><span data-ttu-id="e7782-134">問題</span><span class="sxs-lookup"><span data-stu-id="e7782-134">Problem</span></span>
<span data-ttu-id="e7782-135">從 Visual Studio 進行偵錯時，看見 FabricConnectionDeniedException 錯誤。</span><span class="sxs-lookup"><span data-stu-id="e7782-135">When debugging from Visual Studio, you get a FabricConnectionDeniedException error.</span></span>

#### <a name="solution"></a><span data-ttu-id="e7782-136">方案</span><span class="sxs-lookup"><span data-stu-id="e7782-136">Solution</span></span>
<span data-ttu-id="e7782-137">當您嘗試以手動方式啟動服務主機處理序，而非讓 Service Fabric 執行階段啟動時，通常會發生這個錯誤。</span><span class="sxs-lookup"><span data-stu-id="e7782-137">This error usually occurs when you try to start a service host process manually, rather than allowing the Service Fabric runtime to start it for you.</span></span>

<span data-ttu-id="e7782-138">請確定您的解決方法中沒有任何設定為啟始專案的服務專案。</span><span class="sxs-lookup"><span data-stu-id="e7782-138">Ensure that you do not have any service projects set as startup projects in your solution.</span></span> <span data-ttu-id="e7782-139">只有 Service Fabric 應用程式專案才可設為啟始專案。</span><span class="sxs-lookup"><span data-stu-id="e7782-139">Only Service Fabric application projects should be set as startup projects.</span></span>

> [!TIP]
> <span data-ttu-id="e7782-140">如果在安裝之後，您的本機叢集開始行為異常，您可以使用本機叢集管理員系統匣應用程式將其重設。</span><span class="sxs-lookup"><span data-stu-id="e7782-140">If, following setup, your local cluster begins to behave abnormally, you can reset it using the local cluster manager system tray application.</span></span> <span data-ttu-id="e7782-141">這麼做會移除現有叢集，並設定新的叢集。</span><span class="sxs-lookup"><span data-stu-id="e7782-141">This removes the existing cluster and set up a new one.</span></span> <span data-ttu-id="e7782-142">請注意，所有已部署的應用程式和相關聯的資料都會被移除。</span><span class="sxs-lookup"><span data-stu-id="e7782-142">Note that all deployed applications and associated data is removed.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="e7782-143">後續步驟</span><span class="sxs-lookup"><span data-stu-id="e7782-143">Next steps</span></span>
* [<span data-ttu-id="e7782-144">透過系統健康情況報告了解及疑難排解您的叢集</span><span class="sxs-lookup"><span data-stu-id="e7782-144">Understand and troubleshoot your cluster with system health reports</span></span>](service-fabric-understand-and-troubleshoot-with-system-health-reports.md)
* [<span data-ttu-id="e7782-145">使用 Service Fabric 總管視覺化叢集</span><span class="sxs-lookup"><span data-stu-id="e7782-145">Visualize your cluster with Service Fabric Explorer</span></span>](service-fabric-visualizing-your-cluster.md)

