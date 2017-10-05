---
title: "Azure 建議程式安全性建議 | Microsoft Docs"
description: "使用 Azure 建議程式協助改善 Azure 部署的安全性。"
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
ms.openlocfilehash: 53be05593c3733ccb27979a3a026414013125779
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="advisor-security-recommendations"></a><span data-ttu-id="38c6a-103">建議程式安全性建議</span><span class="sxs-lookup"><span data-stu-id="38c6a-103">Advisor Security recommendations</span></span>

<span data-ttu-id="38c6a-104">Azure Advisor 可針對所有的 Azure 資源提供一致的合併建議檢視。</span><span class="sxs-lookup"><span data-stu-id="38c6a-104">Azure Advisor provides you with a consistent, consolidated view of recommendations for all your Azure resources.</span></span> <span data-ttu-id="38c6a-105">它與 Azure 資訊安全中心整合，可為您提供安全性建議。</span><span class="sxs-lookup"><span data-stu-id="38c6a-105">It integrates with Azure Security Center to bring you security recommendations.</span></span> <span data-ttu-id="38c6a-106">您可以從 Advisor 儀表板上的 [安全性] 索引標籤取得安全性建議。</span><span class="sxs-lookup"><span data-stu-id="38c6a-106">You can get security recommendations from the **Security** tab on the Advisor dashboard.</span></span>

![Advisor [安全性] 按鈕](./media/advisor-security-recommendations/advisor-security-tab.png)

<span data-ttu-id="38c6a-108">資訊安全中心利用加強對您 Azure 資源的能見度及安全性控制權，來協助您預防、偵測及回應威脅。</span><span class="sxs-lookup"><span data-stu-id="38c6a-108">Security Center helps you prevent, detect, and respond to threats with increased visibility into and control over the security of your Azure resources.</span></span> <span data-ttu-id="38c6a-109">它會定期分析 Azure 資源的安全性狀態。</span><span class="sxs-lookup"><span data-stu-id="38c6a-109">It periodically analyzes the security state of your Azure resources.</span></span> <span data-ttu-id="38c6a-110">當資訊安全中心識別潛在的安全性弱點時，它會建立建議。</span><span class="sxs-lookup"><span data-stu-id="38c6a-110">When Security Center identifies potential security vulnerabilities, it creates recommendations.</span></span> <span data-ttu-id="38c6a-111">這些建議會引導您完成設定所需控制項的程序。</span><span class="sxs-lookup"><span data-stu-id="38c6a-111">The recommendations guide you through the process of configuring the controls you need.</span></span> 

![Advisor [安全性] 索引標籤](./media/advisor-security-recommendations/advisor-security-recommendations.png)

<span data-ttu-id="38c6a-113">如需安全性建議的詳細資訊，請參閱[管理 Azure 資訊安全中心的安全性建議](https://azure.microsoft.com/en-us/documentation/articles/security-center-recommendations/)。</span><span class="sxs-lookup"><span data-stu-id="38c6a-113">For more information about security recommendations, see [Managing security recommendations in Azure Security Center](https://azure.microsoft.com/en-us/documentation/articles/security-center-recommendations/).</span></span>

## <a name="how-to-access-security-recommendations-in-azure-advisor"></a><span data-ttu-id="38c6a-114">如何存取 Azure Advisor 中的安全性建議</span><span class="sxs-lookup"><span data-stu-id="38c6a-114">How to access Security recommendations in Azure Advisor</span></span>

1. <span data-ttu-id="38c6a-115">登入 [Azure 入口網站](https://portal.azure.com)。</span><span class="sxs-lookup"><span data-stu-id="38c6a-115">Sign in to the [Azure portal](https://portal.azure.com).</span></span>

2. <span data-ttu-id="38c6a-116">在左側窗格中，按一下 [更多服務]。</span><span class="sxs-lookup"><span data-stu-id="38c6a-116">In the left pane, click **More services**.</span></span>

3. <span data-ttu-id="38c6a-117">在服務功能表窗格中，於 [監視和管理] 底下，按一下 [Azure Advisor]。</span><span class="sxs-lookup"><span data-stu-id="38c6a-117">In the service menu pane, under **Monitoring and Management**, click **Azure Advisor**.</span></span>  
 <span data-ttu-id="38c6a-118">隨即會顯示 Advisor 儀表板。</span><span class="sxs-lookup"><span data-stu-id="38c6a-118">The Advisor dashboard is displayed.</span></span>

4. <span data-ttu-id="38c6a-119">在 Advisor 儀表板上，按一下 [安全性] 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="38c6a-119">On the Advisor dashboard, click the **Security** tab.</span></span>

5. <span data-ttu-id="38c6a-120">選取您想要接收建議的訂用帳戶，然後按一下 [取得建議]。</span><span class="sxs-lookup"><span data-stu-id="38c6a-120">Select the subscription for which you want to receive recommendations, and then click **Get recommendations**.</span></span>

> [!NOTE]
> <span data-ttu-id="38c6a-121">若要存取 Advisor 建議，您必須先向 Advisor「註冊您的訂用帳戶」。</span><span class="sxs-lookup"><span data-stu-id="38c6a-121">To access Advisor recommendations, you must first *register your subscription* with Advisor.</span></span> <span data-ttu-id="38c6a-122">當「訂用帳戶擁有者」啟動 Advisor 儀表板，然後按一下 [取得建議] 按鈕時，便會註冊訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="38c6a-122">A subscription is registered when a *subscription Owner* launches the Advisor dashboard and clicks the **Get recommendations** button.</span></span> <span data-ttu-id="38c6a-123">此作業「只需要執行一次」。</span><span class="sxs-lookup"><span data-stu-id="38c6a-123">This is a *one-time operation*.</span></span> <span data-ttu-id="38c6a-124">註冊訂用帳戶之後，您能以訂用帳戶、資源群組或特定資源的 [擁有者]、[參與者] 或 [讀取者] 身分存取 Advisor 建議。</span><span class="sxs-lookup"><span data-stu-id="38c6a-124">After the subscription is registered, you can access Advisor recommendations as *Owner*, *Contributor*, or *Reader* for a subscription, a resource group, or a specific resource.</span></span>

## <a name="next-steps"></a><span data-ttu-id="38c6a-125">後續步驟</span><span class="sxs-lookup"><span data-stu-id="38c6a-125">Next steps</span></span>

<span data-ttu-id="38c6a-126">若要深入了解 Advisor 建議，請參閱：</span><span class="sxs-lookup"><span data-stu-id="38c6a-126">To learn more about Advisor recommendations, see:</span></span>
* [<span data-ttu-id="38c6a-127">建議程式簡介</span><span class="sxs-lookup"><span data-stu-id="38c6a-127">Introduction to Advisor</span></span>](advisor-overview.md)
* [<span data-ttu-id="38c6a-128">開始使用建議程式</span><span class="sxs-lookup"><span data-stu-id="38c6a-128">Get started with Advisor</span></span>](advisor-get-started.md)
* [<span data-ttu-id="38c6a-129">建議程式成本建議</span><span class="sxs-lookup"><span data-stu-id="38c6a-129">Advisor Cost recommendations</span></span>](advisor-performance-recommendations.md)
* [<span data-ttu-id="38c6a-130">建議程式效能建議</span><span class="sxs-lookup"><span data-stu-id="38c6a-130">Advisor Performance recommendations</span></span>](advisor-performance-recommendations.md)
* [<span data-ttu-id="38c6a-131">建議程式高可用性建議</span><span class="sxs-lookup"><span data-stu-id="38c6a-131">Advisor High Availability recommendations</span></span>](advisor-high-availability-recommendations.md)


 
