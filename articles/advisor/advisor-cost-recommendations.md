---
title: "Azure 建議程式成本建議 | Microsoft Docs"
description: "使用 Azure 建議程式將 Azure 部署的成本最佳化。"
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
ms.openlocfilehash: 5eef2116f238b477fa8de46ce7b25728c393739c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="advisor-cost-recommendations"></a><span data-ttu-id="e4d58-103">建議程式成本建議</span><span class="sxs-lookup"><span data-stu-id="e4d58-103">Advisor Cost recommendations</span></span>

<span data-ttu-id="e4d58-104">建議程式可找出閒置和未充分利用的資源，協助您最佳化並減少 Azure 整體費用。</span><span class="sxs-lookup"><span data-stu-id="e4d58-104">Advisor helps you optimize and reduce your overall Azure spend by identifying idle and underutilized resources.</span></span> <span data-ttu-id="e4d58-105">您可以從 Advisor 儀表板上的 [成本] 索引標籤取得成本建議。</span><span class="sxs-lookup"><span data-stu-id="e4d58-105">You can get cost recommendations from the **Cost** tab on the Advisor dashboard.</span></span>

![Advisor [成本] 索引標籤](./media/advisor-cost-recommendations/advisor-cost-tab2.png)

## <a name="optimize-virtual-machine-spend-by-resizing-underutilized-instances"></a><span data-ttu-id="e4d58-107">將未充分利用的執行個體調整大小以最佳化虛擬機器費用</span><span class="sxs-lookup"><span data-stu-id="e4d58-107">Optimize virtual machine spend by resizing underutilized instances</span></span> 
<span data-ttu-id="e4d58-108">雖然特定應用程式案例的設計可能導致低使用率，但您通常可藉由管理虛擬機器的大小和數目來節省金錢。</span><span class="sxs-lookup"><span data-stu-id="e4d58-108">Although certain application scenarios can result in low utilization by design, you can often save money by managing the size and number of your virtual machines.</span></span> <span data-ttu-id="e4d58-109">Advisor 可監視 14 天的虛擬機器使用量，然後找出低使用率的虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="e4d58-109">Advisor monitors your virtual machine usage for 14 days and then identifies low-utilization virtual machines.</span></span> <span data-ttu-id="e4d58-110">CPU 使用率等於或低於 5% 且網路使用量等於或低於 7 MB 長達 4 天 (含) 以上的虛擬機器，會被視為低使用率虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="e4d58-110">Virtual machines whose CPU utilization is 5 percent or less and network usage is 7 MB or less for four or more days are considered low-utilization virtual machines.</span></span>

<span data-ttu-id="e4d58-111">Advisor 會顯示繼續執行虛擬機器的預估成本，以便您可以選擇將它關閉或調整其大小。</span><span class="sxs-lookup"><span data-stu-id="e4d58-111">Advisor shows you the estimated cost of continuing to run your virtual machine, so that you can choose to shut it down or resize it.</span></span>  

![調整虛擬機器大小的建議程式成本建議](./media/advisor-cost-recommendations/advisor-cost-resizevms.png)

## <a name="use-a-cost-effective-solution-to-manage-performance-goals-of-multiple-sql-databases"></a><span data-ttu-id="e4d58-113">使用符合成本效益的解決方案來管理多個 SQL Database 的效能目標</span><span class="sxs-lookup"><span data-stu-id="e4d58-113">Use a cost effective solution to manage performance goals of multiple SQL databases</span></span>
<span data-ttu-id="e4d58-114">建議程式會找出可受益於建立彈性資料庫集區的 SQL Server 執行個體。</span><span class="sxs-lookup"><span data-stu-id="e4d58-114">Advisor identifies SQL server instances that can benefit from creating elastic database pools.</span></span> <span data-ttu-id="e4d58-115">彈性資料庫集區提供符合成本效益的簡單解決方案，以管理多個具有不同使用模式之資料庫的效能目標。</span><span class="sxs-lookup"><span data-stu-id="e4d58-115">Elastic database pools provide a simple, cost-effective solution to manage the performance goals of multiple databases that have varying usage patterns.</span></span> <span data-ttu-id="e4d58-116">如需 Azure 彈性集區的詳細資訊，請參閱[什麼是 Azure 彈性集區？](https://azure.microsoft.com/en-us/documentation/articles/sql-database-elastic-pool/)。</span><span class="sxs-lookup"><span data-stu-id="e4d58-116">For more information about Azure elastic pools, see [What is an Azure Elastic pool?](https://azure.microsoft.com/en-us/documentation/articles/sql-database-elastic-pool/).</span></span>

![彈性資料庫集區的建議程式成本建議](./media/advisor-cost-recommendations/advisor-cost-elasticdbpools.png)

## <a name="how-to-access-cost-recommendations-in-azure-advisor"></a><span data-ttu-id="e4d58-118">如何在 Azure 建議程式中存取成本建議</span><span class="sxs-lookup"><span data-stu-id="e4d58-118">How to access cost recommendations in Azure Advisor</span></span>

1. <span data-ttu-id="e4d58-119">登入 [Azure 入口網站](https://portal.azure.com)。</span><span class="sxs-lookup"><span data-stu-id="e4d58-119">Sign in to the [Azure portal](https://portal.azure.com).</span></span>

2. <span data-ttu-id="e4d58-120">在左側窗格中，按一下 [更多服務]。</span><span class="sxs-lookup"><span data-stu-id="e4d58-120">In the left pane, click **More services**.</span></span>

3. <span data-ttu-id="e4d58-121">在服務功能表窗格中，於 [監視和管理] 底下，按一下 [Azure Advisor]。</span><span class="sxs-lookup"><span data-stu-id="e4d58-121">In the service menu pane, under **Monitoring and Management**, click **Azure Advisor**.</span></span>  
 <span data-ttu-id="e4d58-122">隨即會顯示 Advisor 儀表板。</span><span class="sxs-lookup"><span data-stu-id="e4d58-122">The Advisor dashboard is displayed.</span></span>

4. <span data-ttu-id="e4d58-123">在 Advisor 儀表板上，按一下 [成本] 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="e4d58-123">On the Advisor dashboard, click the **Cost** tab.</span></span>

5. <span data-ttu-id="e4d58-124">選取您想要接收建議的訂用帳戶，然後按一下 [取得建議]。</span><span class="sxs-lookup"><span data-stu-id="e4d58-124">Select the subscription for which you want to receive recommendations, and then click **Get recommendations**.</span></span>

> [!NOTE]
> <span data-ttu-id="e4d58-125">若要存取 Advisor 建議，您必須先向 Advisor「註冊您的訂用帳戶」。</span><span class="sxs-lookup"><span data-stu-id="e4d58-125">To access Advisor recommendations, you must first *register your subscription* with Advisor.</span></span> <span data-ttu-id="e4d58-126">當「訂用帳戶擁有者」啟動 Advisor 儀表板，然後按一下 [取得建議] 按鈕時，便會註冊訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="e4d58-126">A subscription is registered when a *subscription Owner* launches the Advisor dashboard and clicks the **Get recommendations** button.</span></span> <span data-ttu-id="e4d58-127">此作業「只需要執行一次」。</span><span class="sxs-lookup"><span data-stu-id="e4d58-127">This is a *one-time operation*.</span></span> <span data-ttu-id="e4d58-128">註冊訂用帳戶之後，您能以訂用帳戶、資源群組或特定資源的 [擁有者]、[參與者] 或 [讀取者] 身分存取 Advisor 建議。</span><span class="sxs-lookup"><span data-stu-id="e4d58-128">After the subscription is registered, you can access Advisor recommendations as *Owner*, *Contributor*, or *Reader* for a subscription, a resource group, or a specific resource.</span></span>

## <a name="next-steps"></a><span data-ttu-id="e4d58-129">後續步驟</span><span class="sxs-lookup"><span data-stu-id="e4d58-129">Next steps</span></span>

<span data-ttu-id="e4d58-130">若要深入了解 Advisor 建議，請參閱：</span><span class="sxs-lookup"><span data-stu-id="e4d58-130">To learn more about Advisor recommendations, see:</span></span>
* [<span data-ttu-id="e4d58-131">建議程式簡介</span><span class="sxs-lookup"><span data-stu-id="e4d58-131">Introduction to Advisor</span></span>](advisor-overview.md)
* [<span data-ttu-id="e4d58-132">快速入門</span><span class="sxs-lookup"><span data-stu-id="e4d58-132">Get Started</span></span>](advisor-get-started.md)
* [<span data-ttu-id="e4d58-133">建議程式效能建議</span><span class="sxs-lookup"><span data-stu-id="e4d58-133">Advisor Performance recommendations</span></span>](advisor-cost-recommendations.md)
* [<span data-ttu-id="e4d58-134">建議程式高可用性建議</span><span class="sxs-lookup"><span data-stu-id="e4d58-134">Advisor High Availability recommendations</span></span>](advisor-cost-recommendations.md)
* [<span data-ttu-id="e4d58-135">建議程式安全性建議</span><span class="sxs-lookup"><span data-stu-id="e4d58-135">Advisor Security recommendations</span></span>](advisor-cost-recommendations.md)
