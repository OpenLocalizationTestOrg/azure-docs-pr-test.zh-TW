---
title: "建議程式的安全性建議 aaaAzure |Microsoft 文件"
description: "使用 Azure Advisor toohelp 改善您的 Azure 部署的 hello 安全性。"
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
ms.openlocfilehash: e01ac29eb6e02bff0b1e846e320e7c36f85c7343
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="advisor-security-recommendations"></a><span data-ttu-id="5e85f-103">建議程式安全性建議</span><span class="sxs-lookup"><span data-stu-id="5e85f-103">Advisor Security recommendations</span></span>

<span data-ttu-id="5e85f-104">Azure Advisor 可針對所有的 Azure 資源提供一致的合併建議檢視。</span><span class="sxs-lookup"><span data-stu-id="5e85f-104">Azure Advisor provides you with a consistent, consolidated view of recommendations for all your Azure resources.</span></span> <span data-ttu-id="5e85f-105">它可以整合 Azure 資訊安全中心 toobring 與您的安全性建議。</span><span class="sxs-lookup"><span data-stu-id="5e85f-105">It integrates with Azure Security Center toobring you security recommendations.</span></span> <span data-ttu-id="5e85f-106">您可以從 hello 取得的安全性建議**安全性**hello Advisor 儀表板上的索引標籤。</span><span class="sxs-lookup"><span data-stu-id="5e85f-106">You can get security recommendations from hello **Security** tab on hello Advisor dashboard.</span></span>

![hello Advisor 安全性] 按鈕](./media/advisor-security-recommendations/advisor-security-tab.png)

<span data-ttu-id="5e85f-108">資訊安全中心可協助您防止、 偵測，並回應 toothreats 增加的可見性與您的 Azure 資源的 hello 安全性控制。</span><span class="sxs-lookup"><span data-stu-id="5e85f-108">Security Center helps you prevent, detect, and respond toothreats with increased visibility into and control over hello security of your Azure resources.</span></span> <span data-ttu-id="5e85f-109">定期分析您的 Azure 資源 hello 安全性狀態。</span><span class="sxs-lookup"><span data-stu-id="5e85f-109">It periodically analyzes hello security state of your Azure resources.</span></span> <span data-ttu-id="5e85f-110">當資訊安全中心識別潛在的安全性弱點時，它會建立建議。</span><span class="sxs-lookup"><span data-stu-id="5e85f-110">When Security Center identifies potential security vulnerabilities, it creates recommendations.</span></span> <span data-ttu-id="5e85f-111">hello 建議會引導您完成設定您需要的 hello 控制項的 hello 程序。</span><span class="sxs-lookup"><span data-stu-id="5e85f-111">hello recommendations guide you through hello process of configuring hello controls you need.</span></span> 

![hello Advisor 安全性] 索引標籤](./media/advisor-security-recommendations/advisor-security-recommendations.png)

<span data-ttu-id="5e85f-113">如需安全性建議的詳細資訊，請參閱[管理 Azure 資訊安全中心的安全性建議](https://azure.microsoft.com/en-us/documentation/articles/security-center-recommendations/)。</span><span class="sxs-lookup"><span data-stu-id="5e85f-113">For more information about security recommendations, see [Managing security recommendations in Azure Security Center](https://azure.microsoft.com/en-us/documentation/articles/security-center-recommendations/).</span></span>

## <a name="how-tooaccess-security-recommendations-in-azure-advisor"></a><span data-ttu-id="5e85f-114">如何 tooaccess Azure Advisor 中的安全性建議</span><span class="sxs-lookup"><span data-stu-id="5e85f-114">How tooaccess Security recommendations in Azure Advisor</span></span>

1. <span data-ttu-id="5e85f-115">登入 toohello [Azure 入口網站](https://portal.azure.com)。</span><span class="sxs-lookup"><span data-stu-id="5e85f-115">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>

2. <span data-ttu-id="5e85f-116">在 [hello] 左窗格中，按一下 [**更多服務**。</span><span class="sxs-lookup"><span data-stu-id="5e85f-116">In hello left pane, click **More services**.</span></span>

3. <span data-ttu-id="5e85f-117">在 [hello 服務功能表窗格底下**監視及管理**，按一下 [ **Azure Advisor**。</span><span class="sxs-lookup"><span data-stu-id="5e85f-117">In hello service menu pane, under **Monitoring and Management**, click **Azure Advisor**.</span></span>  
 <span data-ttu-id="5e85f-118">hello Advisor 儀表板會顯示。</span><span class="sxs-lookup"><span data-stu-id="5e85f-118">hello Advisor dashboard is displayed.</span></span>

4. <span data-ttu-id="5e85f-119">在 [hello Advisor 儀表板上按一下 [hello**安全性**] 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="5e85f-119">On hello Advisor dashboard, click hello **Security** tab.</span></span>

5. <span data-ttu-id="5e85f-120">選取 hello 訂用帳戶，您想 tooreceive 建議，然後按一下**取得建議**。</span><span class="sxs-lookup"><span data-stu-id="5e85f-120">Select hello subscription for which you want tooreceive recommendations, and then click **Get recommendations**.</span></span>

> [!NOTE]
> <span data-ttu-id="5e85f-121">tooaccess Advisor 的建議，您必須先*註冊您的訂閱*與 Advisor。</span><span class="sxs-lookup"><span data-stu-id="5e85f-121">tooaccess Advisor recommendations, you must first *register your subscription* with Advisor.</span></span> <span data-ttu-id="5e85f-122">已經註冊訂閱時*訂用帳戶擁有者*啟動 hello Advisor 儀表板，並按一下 hello**取得建議**] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="5e85f-122">A subscription is registered when a *subscription Owner* launches hello Advisor dashboard and clicks hello **Get recommendations** button.</span></span> <span data-ttu-id="5e85f-123">此作業「只需要執行一次」。</span><span class="sxs-lookup"><span data-stu-id="5e85f-123">This is a *one-time operation*.</span></span> <span data-ttu-id="5e85f-124">Hello 訂用帳戶註冊之後，您可以存取 Advisor 的建議做為*擁有者*，*參與者*，或*讀取器*訂用帳戶，資源群組，或特定的資源。</span><span class="sxs-lookup"><span data-stu-id="5e85f-124">After hello subscription is registered, you can access Advisor recommendations as *Owner*, *Contributor*, or *Reader* for a subscription, a resource group, or a specific resource.</span></span>

## <a name="next-steps"></a><span data-ttu-id="5e85f-125">後續步驟</span><span class="sxs-lookup"><span data-stu-id="5e85f-125">Next steps</span></span>

<span data-ttu-id="5e85f-126">toolearn 深入了解 Advisor 的建議，請參閱：</span><span class="sxs-lookup"><span data-stu-id="5e85f-126">toolearn more about Advisor recommendations, see:</span></span>
* [<span data-ttu-id="5e85f-127">簡介 tooAdvisor</span><span class="sxs-lookup"><span data-stu-id="5e85f-127">Introduction tooAdvisor</span></span>](advisor-overview.md)
* [<span data-ttu-id="5e85f-128">開始使用建議程式</span><span class="sxs-lookup"><span data-stu-id="5e85f-128">Get started with Advisor</span></span>](advisor-get-started.md)
* [<span data-ttu-id="5e85f-129">建議程式成本建議</span><span class="sxs-lookup"><span data-stu-id="5e85f-129">Advisor Cost recommendations</span></span>](advisor-performance-recommendations.md)
* [<span data-ttu-id="5e85f-130">建議程式效能建議</span><span class="sxs-lookup"><span data-stu-id="5e85f-130">Advisor Performance recommendations</span></span>](advisor-performance-recommendations.md)
* [<span data-ttu-id="5e85f-131">建議程式高可用性建議</span><span class="sxs-lookup"><span data-stu-id="5e85f-131">Advisor High Availability recommendations</span></span>](advisor-high-availability-recommendations.md)


 
