---
title: "aaaTroubleshoot 您本機的 Service Fabric 叢集設定 |Microsoft 文件"
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
ms.openlocfilehash: ce36f62a4bc69d2cd5b6c3df4abda6ca88fa84f0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-your-local-development-cluster-setup"></a><span data-ttu-id="b9e9c-103">疑難排解本機開發叢集設定</span><span class="sxs-lookup"><span data-stu-id="b9e9c-103">Troubleshoot your local development cluster setup</span></span>
<span data-ttu-id="b9e9c-104">如果您的本機 Azure Service Fabric 開發叢集進行互動時遇到問題，請檢閱下列可能的解決方案的建議 hello。</span><span class="sxs-lookup"><span data-stu-id="b9e9c-104">If you run into an issue while interacting with your local Azure Service Fabric development cluster, review hello following suggestions for potential solutions.</span></span>

## <a name="cluster-setup-failures"></a><span data-ttu-id="b9e9c-105">叢集設定失敗</span><span class="sxs-lookup"><span data-stu-id="b9e9c-105">Cluster setup failures</span></span>
### <a name="cannot-clean-up-service-fabric-logs"></a><span data-ttu-id="b9e9c-106">無法清除 Service Fabric 記錄檔</span><span class="sxs-lookup"><span data-stu-id="b9e9c-106">Cannot clean up Service Fabric logs</span></span>
#### <a name="problem"></a><span data-ttu-id="b9e9c-107">問題</span><span class="sxs-lookup"><span data-stu-id="b9e9c-107">Problem</span></span>
<span data-ttu-id="b9e9c-108">在執行 hello DevClusterSetup 指令碼時，您會看到類似錯誤：</span><span class="sxs-lookup"><span data-stu-id="b9e9c-108">While running hello DevClusterSetup script, you see an error like this:</span></span>

    Cannot clean up C:\SfDevCluster\Log fully as references are likely being held tooitems in it. Please remove those and run this script again.
    At line:1 char:1 + .\DevClusterSetup.ps1
    + ~~~~~~~~~~~~~~~~~~~~~
    + CategoryInfo : NotSpecified: (:) [Write-Error], WriteErrorException
    + FullyQualifiedErrorId : Microsoft.PowerShell.Commands.WriteErrorException,DevClusterSetup.ps1


#### <a name="solution"></a><span data-ttu-id="b9e9c-109">方案</span><span class="sxs-lookup"><span data-stu-id="b9e9c-109">Solution</span></span>
<span data-ttu-id="b9e9c-110">關閉 hello 目前的 PowerShell 視窗，並開啟新的 PowerShell 視窗，以系統管理員。</span><span class="sxs-lookup"><span data-stu-id="b9e9c-110">Close hello current PowerShell window and open a new PowerShell window as an administrator.</span></span> <span data-ttu-id="b9e9c-111">您現在應該能夠 toosuccessfully 執行 hello 指令碼。</span><span class="sxs-lookup"><span data-stu-id="b9e9c-111">You should now be able toosuccessfully run hello script.</span></span>

## <a name="cluster-connection-failures"></a><span data-ttu-id="b9e9c-112">叢集連接失敗</span><span class="sxs-lookup"><span data-stu-id="b9e9c-112">Cluster connection failures</span></span>
### <a name="service-fabric-powershell-cmdlets-are-not-recognized-in-azure-powershell"></a><span data-ttu-id="b9e9c-113">在 Azure PowerShell 中無法辨識 Service Fabric PowerShell Cmdlet</span><span class="sxs-lookup"><span data-stu-id="b9e9c-113">Service Fabric PowerShell cmdlets are not recognized in Azure PowerShell</span></span>
#### <a name="problem"></a><span data-ttu-id="b9e9c-114">問題</span><span class="sxs-lookup"><span data-stu-id="b9e9c-114">Problem</span></span>
<span data-ttu-id="b9e9c-115">如果您嘗試 toorun 任何 hello Service Fabric PowerShell cmdlet，例如`Connect-ServiceFabricCluster`在 Azure PowerShell 視窗中，失敗，指出無法辨識該 hello 指令程式。</span><span class="sxs-lookup"><span data-stu-id="b9e9c-115">If you try toorun any of hello Service Fabric PowerShell cmdlets, such as `Connect-ServiceFabricCluster` in an Azure PowerShell window, it fails, saying that hello cmdlet is not recognized.</span></span> <span data-ttu-id="b9e9c-116">hello 這個錯誤的原因是，Azure PowerShell，將會使用 hello 32 位元版本的 Windows PowerShell （即使在 64 位元作業系統的版本），而 hello Service Fabric cmdlet 只能在 64 位元環境中運作。</span><span class="sxs-lookup"><span data-stu-id="b9e9c-116">hello reason for this is that Azure PowerShell uses hello 32-bit version of Windows PowerShell (even on 64-bit OS versions), whereas hello Service Fabric cmdlets only work in 64-bit environments.</span></span>

#### <a name="solution"></a><span data-ttu-id="b9e9c-117">方案</span><span class="sxs-lookup"><span data-stu-id="b9e9c-117">Solution</span></span>
<span data-ttu-id="b9e9c-118">一律直接從 Windows PowerShell 執行 Service Fabric Cmdlet。</span><span class="sxs-lookup"><span data-stu-id="b9e9c-118">Always run Service Fabric cmdlets directly from Windows PowerShell.</span></span>

> [!NOTE]
> <span data-ttu-id="b9e9c-119">hello 最新版本的 Azure PowerShell 不會建立特殊的捷徑，因此這不會再出現。</span><span class="sxs-lookup"><span data-stu-id="b9e9c-119">hello latest version of Azure PowerShell does not create a special shortcut, so this should no longer occur.</span></span>
> 
> 

### <a name="type-initialization-exception"></a><span data-ttu-id="b9e9c-120">類型初始化例外狀況</span><span class="sxs-lookup"><span data-stu-id="b9e9c-120">Type Initialization exception</span></span>
#### <a name="problem"></a><span data-ttu-id="b9e9c-121">問題</span><span class="sxs-lookup"><span data-stu-id="b9e9c-121">Problem</span></span>
<span data-ttu-id="b9e9c-122">當您要連接 toohello 叢集在 PowerShell 中的時，您會看到如 System.Fabric.Common.AppTrace hello 錯誤 TypeInitializationException。</span><span class="sxs-lookup"><span data-stu-id="b9e9c-122">When you are connecting toohello cluster in PowerShell, you see hello error TypeInitializationException for System.Fabric.Common.AppTrace.</span></span>

#### <a name="solution"></a><span data-ttu-id="b9e9c-123">方案</span><span class="sxs-lookup"><span data-stu-id="b9e9c-123">Solution</span></span>
<span data-ttu-id="b9e9c-124">在安裝期間未正確設定路徑變數。</span><span class="sxs-lookup"><span data-stu-id="b9e9c-124">Your path variable was not correctly set during installation.</span></span> <span data-ttu-id="b9e9c-125">登出 Windows，再重新登入。</span><span class="sxs-lookup"><span data-stu-id="b9e9c-125">Sign out of Windows and sign back in.</span></span> <span data-ttu-id="b9e9c-126">這會重新整理您的路徑。</span><span class="sxs-lookup"><span data-stu-id="b9e9c-126">This refreshes your path.</span></span>

### <a name="cluster-connection-fails-with-object-is-closed"></a><span data-ttu-id="b9e9c-127">叢集連接失敗，且出現「物件已關閉」</span><span class="sxs-lookup"><span data-stu-id="b9e9c-127">Cluster connection fails with "Object is closed"</span></span>
#### <a name="problem"></a><span data-ttu-id="b9e9c-128">問題</span><span class="sxs-lookup"><span data-stu-id="b9e9c-128">Problem</span></span>
<span data-ttu-id="b9e9c-129">呼叫 tooConnect ServiceFabricCluster 失敗，錯誤如下：</span><span class="sxs-lookup"><span data-stu-id="b9e9c-129">A call tooConnect-ServiceFabricCluster fails with an error like this:</span></span>

    Connect-ServiceFabricCluster : hello object is closed.
    At line:1 char:1
    + Connect-ServiceFabricCluster
    + ~~~~~~~~~~~~~~~~~~~~~~~~~~~~
    + CategoryInfo : InvalidOperation: (:) [Connect-ServiceFabricCluster], FabricObjectClosedException
    + FullyQualifiedErrorId : CreateClusterConnectionErrorId,Microsoft.ServiceFabric.Powershell.ConnectCluster

#### <a name="solution"></a><span data-ttu-id="b9e9c-130">方案</span><span class="sxs-lookup"><span data-stu-id="b9e9c-130">Solution</span></span>
<span data-ttu-id="b9e9c-131">關閉 hello 目前的 PowerShell 視窗，並開啟新的 PowerShell 視窗，以系統管理員。</span><span class="sxs-lookup"><span data-stu-id="b9e9c-131">Close hello current PowerShell window and open a new PowerShell window as an administrator.</span></span> <span data-ttu-id="b9e9c-132">您現在應該可以 toosuccessfully 連接。</span><span class="sxs-lookup"><span data-stu-id="b9e9c-132">You should now be able toosuccessfully connect.</span></span>

### <a name="fabric-connection-denied-exception"></a><span data-ttu-id="b9e9c-133">拒絕網狀架構連線例外狀況</span><span class="sxs-lookup"><span data-stu-id="b9e9c-133">Fabric Connection Denied exception</span></span>
#### <a name="problem"></a><span data-ttu-id="b9e9c-134">問題</span><span class="sxs-lookup"><span data-stu-id="b9e9c-134">Problem</span></span>
<span data-ttu-id="b9e9c-135">從 Visual Studio 進行偵錯時，看見 FabricConnectionDeniedException 錯誤。</span><span class="sxs-lookup"><span data-stu-id="b9e9c-135">When debugging from Visual Studio, you get a FabricConnectionDeniedException error.</span></span>

#### <a name="solution"></a><span data-ttu-id="b9e9c-136">方案</span><span class="sxs-lookup"><span data-stu-id="b9e9c-136">Solution</span></span>
<span data-ttu-id="b9e9c-137">當您嘗試 toostart 服務主機處理序以手動方式，而不是允許 hello Service Fabric 執行階段 toostart，通常會發生此錯誤會針對您。</span><span class="sxs-lookup"><span data-stu-id="b9e9c-137">This error usually occurs when you try toostart a service host process manually, rather than allowing hello Service Fabric runtime toostart it for you.</span></span>

<span data-ttu-id="b9e9c-138">請確定您的解決方法中沒有任何設定為啟始專案的服務專案。</span><span class="sxs-lookup"><span data-stu-id="b9e9c-138">Ensure that you do not have any service projects set as startup projects in your solution.</span></span> <span data-ttu-id="b9e9c-139">只有 Service Fabric 應用程式專案才可設為啟始專案。</span><span class="sxs-lookup"><span data-stu-id="b9e9c-139">Only Service Fabric application projects should be set as startup projects.</span></span>

> [!TIP]
> <span data-ttu-id="b9e9c-140">如果安裝程式，您的本機叢集開始 toobehave 異常，您可以重設使用 hello 本機叢集管理員 」 系統匣應用程式。</span><span class="sxs-lookup"><span data-stu-id="b9e9c-140">If, following setup, your local cluster begins toobehave abnormally, you can reset it using hello local cluster manager system tray application.</span></span> <span data-ttu-id="b9e9c-141">此移除 hello 現有的叢集，並設定新的。</span><span class="sxs-lookup"><span data-stu-id="b9e9c-141">This removes hello existing cluster and set up a new one.</span></span> <span data-ttu-id="b9e9c-142">請注意，所有已部署的應用程式和相關聯的資料都會被移除。</span><span class="sxs-lookup"><span data-stu-id="b9e9c-142">Note that all deployed applications and associated data is removed.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="b9e9c-143">後續步驟</span><span class="sxs-lookup"><span data-stu-id="b9e9c-143">Next steps</span></span>
* [<span data-ttu-id="b9e9c-144">透過系統健康情況報告了解及疑難排解您的叢集</span><span class="sxs-lookup"><span data-stu-id="b9e9c-144">Understand and troubleshoot your cluster with system health reports</span></span>](service-fabric-understand-and-troubleshoot-with-system-health-reports.md)
* [<span data-ttu-id="b9e9c-145">使用 Service Fabric 總管視覺化叢集</span><span class="sxs-lookup"><span data-stu-id="b9e9c-145">Visualize your cluster with Service Fabric Explorer</span></span>](service-fabric-visualizing-your-cluster.md)

