---
title: "aaaAzure Advisor 成本建議 |Microsoft 文件"
description: "使用您的 Azure 部署的 Azure Advisor toooptimize hello 成本。"
services: advisor
documentationcenter: NA
author: kumudd
manager: carmonm
editor: 
ms.assetid: 
ms.service: advisor
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 11/16/2016
ms.author: kumud
ms.openlocfilehash: 50f70c33a17f550c8753795435cdfddd51e409f7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="advisor-cost-recommendations"></a><span data-ttu-id="dd00e-103">建議程式成本建議</span><span class="sxs-lookup"><span data-stu-id="dd00e-103">Advisor Cost recommendations</span></span>

<span data-ttu-id="dd00e-104">建議程式可找出閒置和未充分利用的資源，協助您最佳化並減少 Azure 整體費用。</span><span class="sxs-lookup"><span data-stu-id="dd00e-104">Advisor helps you optimize and reduce your overall Azure spend by identifying idle and underutilized resources.</span></span> <span data-ttu-id="dd00e-105">您可以取得成本建議 hello**成本**hello Advisor 儀表板上的索引標籤。</span><span class="sxs-lookup"><span data-stu-id="dd00e-105">You can get cost recommendations from hello **Cost** tab on hello Advisor dashboard.</span></span>

![Advisor [成本] 索引標籤](./media/advisor-cost-recommendations/advisor-cost-tab2.png)

## <a name="optimize-virtual-machine-spend-by-resizing-underutilized-instances"></a><span data-ttu-id="dd00e-107">將未充分利用的執行個體調整大小以最佳化虛擬機器費用</span><span class="sxs-lookup"><span data-stu-id="dd00e-107">Optimize virtual machine spend by resizing underutilized instances</span></span> 
<span data-ttu-id="dd00e-108">雖然某些應用程式的情況下可能會導致低使用率所設計，您通常可以藉由管理您的虛擬機器的 hello 大小與數目來節省成本。</span><span class="sxs-lookup"><span data-stu-id="dd00e-108">Although certain application scenarios can result in low utilization by design, you can often save money by managing hello size and number of your virtual machines.</span></span> <span data-ttu-id="dd00e-109">Advisor 可監視 14 天的虛擬機器使用量，然後找出低使用率的虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="dd00e-109">Advisor monitors your virtual machine usage for 14 days and then identifies low-utilization virtual machines.</span></span> <span data-ttu-id="dd00e-110">CPU 使用率等於或低於 5% 且網路使用量等於或低於 7 MB 長達 4 天 (含) 以上的虛擬機器，會被視為低使用率虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="dd00e-110">Virtual machines whose CPU utilization is 5 percent or less and network usage is 7 MB or less for four or more days are considered low-utilization virtual machines.</span></span>

<span data-ttu-id="dd00e-111">Advisor 顯示，讓您可以選擇的 tooshut 它向下或調整其大小，hello 再 toorun 繼續您的虛擬機器的估計的成本。</span><span class="sxs-lookup"><span data-stu-id="dd00e-111">Advisor shows you hello estimated cost of continuing toorun your virtual machine, so that you can choose tooshut it down or resize it.</span></span>  

![調整虛擬機器大小的建議程式成本建議](./media/advisor-cost-recommendations/advisor-cost-resizevms.png)

## <a name="use-a-cost-effective-solution-toomanage-performance-goals-of-multiple-sql-databases"></a><span data-ttu-id="dd00e-113">使用多個 SQL database 的成本效益的解決方案 toomanage 效能目標</span><span class="sxs-lookup"><span data-stu-id="dd00e-113">Use a cost effective solution toomanage performance goals of multiple SQL databases</span></span>
<span data-ttu-id="dd00e-114">建議程式會找出可受益於建立彈性資料庫集區的 SQL Server 執行個體。</span><span class="sxs-lookup"><span data-stu-id="dd00e-114">Advisor identifies SQL server instances that can benefit from creating elastic database pools.</span></span> <span data-ttu-id="dd00e-115">彈性資料庫集區提供簡單且符合成本效益的解決方案 toomanage hello 效能目標的多個具有不同的使用方式模式的資料庫。</span><span class="sxs-lookup"><span data-stu-id="dd00e-115">Elastic database pools provide a simple, cost-effective solution toomanage hello performance goals of multiple databases that have varying usage patterns.</span></span> <span data-ttu-id="dd00e-116">如需 Azure 彈性集區的詳細資訊，請參閱[什麼是 Azure 彈性集區？](https://azure.microsoft.com/en-us/documentation/articles/sql-database-elastic-pool/)。</span><span class="sxs-lookup"><span data-stu-id="dd00e-116">For more information about Azure elastic pools, see [What is an Azure Elastic pool?](https://azure.microsoft.com/en-us/documentation/articles/sql-database-elastic-pool/).</span></span>

![彈性資料庫集區的建議程式成本建議](./media/advisor-cost-recommendations/advisor-cost-elasticdbpools.png)

## <a name="how-tooaccess-cost-recommendations-in-azure-advisor"></a><span data-ttu-id="dd00e-118">Tooaccess 成本中 Azure Advisor 建議的方式</span><span class="sxs-lookup"><span data-stu-id="dd00e-118">How tooaccess cost recommendations in Azure Advisor</span></span>

1. <span data-ttu-id="dd00e-119">登入 toohello [Azure 入口網站](https://portal.azure.com)。</span><span class="sxs-lookup"><span data-stu-id="dd00e-119">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>

2. <span data-ttu-id="dd00e-120">在 hello 左窗格中，按一下 **更多服務**。</span><span class="sxs-lookup"><span data-stu-id="dd00e-120">In hello left pane, click **More services**.</span></span>

3. <span data-ttu-id="dd00e-121">在 hello 服務功能表窗格底下**監視及管理**，按一下  **Azure Advisor**。</span><span class="sxs-lookup"><span data-stu-id="dd00e-121">In hello service menu pane, under **Monitoring and Management**, click **Azure Advisor**.</span></span>  
 <span data-ttu-id="dd00e-122">hello Advisor 儀表板會顯示。</span><span class="sxs-lookup"><span data-stu-id="dd00e-122">hello Advisor dashboard is displayed.</span></span>

4. <span data-ttu-id="dd00e-123">在 hello Advisor 儀表板上按一下 hello**成本** 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="dd00e-123">On hello Advisor dashboard, click hello **Cost** tab.</span></span>

5. <span data-ttu-id="dd00e-124">選取 hello 訂用帳戶，您想 tooreceive 建議，然後按一下**取得建議**。</span><span class="sxs-lookup"><span data-stu-id="dd00e-124">Select hello subscription for which you want tooreceive recommendations, and then click **Get recommendations**.</span></span>

> [!NOTE]
> <span data-ttu-id="dd00e-125">tooaccess Advisor 的建議，您必須先*註冊您的訂閱*與 Advisor。</span><span class="sxs-lookup"><span data-stu-id="dd00e-125">tooaccess Advisor recommendations, you must first *register your subscription* with Advisor.</span></span> <span data-ttu-id="dd00e-126">已經註冊訂閱時*訂用帳戶擁有者*啟動 hello Advisor 儀表板，並按一下 hello**取得建議** 按鈕。</span><span class="sxs-lookup"><span data-stu-id="dd00e-126">A subscription is registered when a *subscription Owner* launches hello Advisor dashboard and clicks hello **Get recommendations** button.</span></span> <span data-ttu-id="dd00e-127">此作業「只需要執行一次」。</span><span class="sxs-lookup"><span data-stu-id="dd00e-127">This is a *one-time operation*.</span></span> <span data-ttu-id="dd00e-128">Hello 訂用帳戶註冊之後，您可以存取 Advisor 的建議做為*擁有者*，*參與者*，或*讀取器*訂用帳戶，資源群組，或特定的資源。</span><span class="sxs-lookup"><span data-stu-id="dd00e-128">After hello subscription is registered, you can access Advisor recommendations as *Owner*, *Contributor*, or *Reader* for a subscription, a resource group, or a specific resource.</span></span>

## <a name="next-steps"></a><span data-ttu-id="dd00e-129">後續步驟</span><span class="sxs-lookup"><span data-stu-id="dd00e-129">Next steps</span></span>

<span data-ttu-id="dd00e-130">toolearn 深入了解 Advisor 的建議，請參閱：</span><span class="sxs-lookup"><span data-stu-id="dd00e-130">toolearn more about Advisor recommendations, see:</span></span>
* [<span data-ttu-id="dd00e-131">簡介 tooAdvisor</span><span class="sxs-lookup"><span data-stu-id="dd00e-131">Introduction tooAdvisor</span></span>](advisor-overview.md)
* [<span data-ttu-id="dd00e-132">開始使用</span><span class="sxs-lookup"><span data-stu-id="dd00e-132">Get Started</span></span>](advisor-get-started.md)
* [<span data-ttu-id="dd00e-133">建議程式效能建議</span><span class="sxs-lookup"><span data-stu-id="dd00e-133">Advisor Performance recommendations</span></span>](advisor-cost-recommendations.md)
* [<span data-ttu-id="dd00e-134">建議程式高可用性建議</span><span class="sxs-lookup"><span data-stu-id="dd00e-134">Advisor High Availability recommendations</span></span>](advisor-cost-recommendations.md)
* [<span data-ttu-id="dd00e-135">建議程式安全性建議</span><span class="sxs-lookup"><span data-stu-id="dd00e-135">Advisor Security recommendations</span></span>](advisor-cost-recommendations.md)
