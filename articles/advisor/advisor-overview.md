---
title: "Azure 建議程式簡介 | Microsoft Docs"
description: "使用 Azure 建議程式將 Azure 部署最佳化。"
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
ms.openlocfilehash: 35678142550f9f887562f311a5e7d9516495cf53
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="introduction-to-azure-advisor"></a><span data-ttu-id="18a33-103">Azure 建議程式簡介</span><span class="sxs-lookup"><span data-stu-id="18a33-103">Introduction to Azure Advisor</span></span>

<span data-ttu-id="18a33-104">了解 Azure Advisor 和其主要功能，並獲得常見問題的解答。</span><span class="sxs-lookup"><span data-stu-id="18a33-104">Learn about Azure Advisor and its key capabilities, and get answers to frequently asked questions.</span></span>

## <a name="what-is-advisor"></a><span data-ttu-id="18a33-105">何謂 Advisor？</span><span class="sxs-lookup"><span data-stu-id="18a33-105">What is Advisor?</span></span>
<span data-ttu-id="18a33-106">Advisor 是個人化的雲端顧問，可協助您依最佳做法來最佳化您的 Azure 部署。</span><span class="sxs-lookup"><span data-stu-id="18a33-106">Advisor is a personalized cloud consultant that helps you follow best practices to optimize your Azure deployments.</span></span> <span data-ttu-id="18a33-107">它可分析您的資源組態和使用量遙測，然後建議可協助您改善 Azure 資源的成本效益、效能、高可用性和安全性的解決方案。</span><span class="sxs-lookup"><span data-stu-id="18a33-107">It analyzes your resource configuration and usage telemetry and then recommends solutions that can help you improve the cost effectiveness, performance, high availability, and security of your Azure resources.</span></span>

<span data-ttu-id="18a33-108">使用 Advisor，您可以：</span><span class="sxs-lookup"><span data-stu-id="18a33-108">With Advisor, you can:</span></span>
* <span data-ttu-id="18a33-109">取得主動式、可採取動作且個人化的最佳做法建議。</span><span class="sxs-lookup"><span data-stu-id="18a33-109">Get proactive, actionable, and personalized best practices recommendations.</span></span> 
* <span data-ttu-id="18a33-110">改善資源的效能、安全性及高可用性，同時尋找降低整體 Azure 費用的機會。</span><span class="sxs-lookup"><span data-stu-id="18a33-110">Improve the performance, security, and high availability of your resources, as you identify opportunities to reduce your overall Azure spend.</span></span>
* <span data-ttu-id="18a33-111">取得內嵌了提議動作的建議。</span><span class="sxs-lookup"><span data-stu-id="18a33-111">Get recommendations with proposed actions inline.</span></span>

<span data-ttu-id="18a33-112">您可以透過 [Azure 入口網站](https://aka.ms/azureadvisordashboard)存取建議程式。</span><span class="sxs-lookup"><span data-stu-id="18a33-112">You can access Advisor through the [Azure portal](https://aka.ms/azureadvisordashboard).</span></span> <span data-ttu-id="18a33-113">登入[入口網站](https://portal.azure.com)，選取 [瀏覽]，然後捲動至 [Azure Advisor]。</span><span class="sxs-lookup"><span data-stu-id="18a33-113">Sign in to the [portal](https://portal.azure.com), select **Browse**, and then scroll to **Azure Advisor**.</span></span> <span data-ttu-id="18a33-114">[建議程式] 儀表板會顯示所選訂用帳戶的個人化建議。</span><span class="sxs-lookup"><span data-stu-id="18a33-114">The Advisor dashboard displays personalized recommendations for a selected subscription.</span></span> 

<span data-ttu-id="18a33-115">建議分為四個類別：</span><span class="sxs-lookup"><span data-stu-id="18a33-115">The recommendations are divided into four categories:</span></span> 

* <span data-ttu-id="18a33-116">**高可用性**：確保和改善業務關鍵應用程式的持續性。</span><span class="sxs-lookup"><span data-stu-id="18a33-116">**High Availability**: To ensure and improve the continuity of your business-critical applications.</span></span> <span data-ttu-id="18a33-117">如需詳細資訊，請參閱[建議程式高可用性的建議](advisor-high-availability-recommendations.md)。</span><span class="sxs-lookup"><span data-stu-id="18a33-117">For more information, see [Advisor High Availability recommendations](advisor-high-availability-recommendations.md).</span></span>

* <span data-ttu-id="18a33-118">**安全性**偵測可能導致安全性漏洞的威脅和弱點。</span><span class="sxs-lookup"><span data-stu-id="18a33-118">**Security**: To detect threats and vulnerabilities that might lead to security breaches.</span></span> <span data-ttu-id="18a33-119">如需詳細資訊，請參閱[建議程式安全性建議](advisor-security-recommendations.md)。</span><span class="sxs-lookup"><span data-stu-id="18a33-119">For more information, see [Advisor Security recommendations](advisor-security-recommendations.md).</span></span>

* <span data-ttu-id="18a33-120">**效能**提升應用程式的速度。</span><span class="sxs-lookup"><span data-stu-id="18a33-120">**Performance**: To improve the speed of your applications.</span></span> <span data-ttu-id="18a33-121">如需詳細資訊，請參閱[建議程式效能建議](advisor-performance-recommendations.md)。</span><span class="sxs-lookup"><span data-stu-id="18a33-121">For more information, see [Advisor Performance recommendations](advisor-performance-recommendations.md).</span></span>

* <span data-ttu-id="18a33-122">**成本**：最佳化並減少整體 Azure 費用。</span><span class="sxs-lookup"><span data-stu-id="18a33-122">**Cost**: To optimize and reduce your overall Azure spend.</span></span> <span data-ttu-id="18a33-123">如需詳細資訊，請參閱[建議程式成本建議](advisor-cost-recommendations.md)。</span><span class="sxs-lookup"><span data-stu-id="18a33-123">For more information, see [Advisor Cost recommendations](advisor-cost-recommendations.md).</span></span>

  ![建議程式建議類型](./media/advisor-overview/advisor-all-tab-examples.png)

> [!NOTE]
> <span data-ttu-id="18a33-125">若要存取 Advisor 建議，您必須先向 Advisor「註冊您的訂用帳戶」。</span><span class="sxs-lookup"><span data-stu-id="18a33-125">To access Advisor recommendations, you must first *register your subscription* with Advisor.</span></span> <span data-ttu-id="18a33-126">當「訂用帳戶擁有者」啟動 Advisor 儀表板，然後按一下 [取得建議] 按鈕時，便會註冊訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="18a33-126">A subscription is registered when a *subscription Owner* launches the Advisor dashboard and clicks the **Get recommendations** button.</span></span> <span data-ttu-id="18a33-127">此作業「只需要執行一次」。</span><span class="sxs-lookup"><span data-stu-id="18a33-127">This is a *one-time operation*.</span></span> <span data-ttu-id="18a33-128">註冊訂用帳戶之後，您能以訂用帳戶、資源群組或特定資源的 [擁有者]、[參與者] 或 [讀取者] 身分存取 Advisor 建議。</span><span class="sxs-lookup"><span data-stu-id="18a33-128">After the subscription is registered, you can access Advisor recommendations as *Owner*, *Contributor*, or *Reader* for a subscription, a resource group, or a specific resource.</span></span>

<span data-ttu-id="18a33-129">您可以按一下建議，以對其進行深入了解。</span><span class="sxs-lookup"><span data-stu-id="18a33-129">You can click a recommendation to learn more about it.</span></span> <span data-ttu-id="18a33-130">您也可以了解您可以執行的動作，以便利用機會或解決問題。</span><span class="sxs-lookup"><span data-stu-id="18a33-130">You can also learn about actions that you can perform to take advantage of an opportunity or resolve an issue.</span></span> 

<span data-ttu-id="18a33-131">建議程式可透過內嵌動作或文件連結提供建議。</span><span class="sxs-lookup"><span data-stu-id="18a33-131">Advisor offers recommendations with inline actions or documentation links.</span></span> <span data-ttu-id="18a33-132">按一下內嵌動作，可帶領您完成「引導式使用者旅程圖」以進行實作。</span><span class="sxs-lookup"><span data-stu-id="18a33-132">Clicking an inline action takes you through a “guided user journey” to implement it.</span></span> <span data-ttu-id="18a33-133">按一下文件連結，可將您指向說明如何以手動方式實作動作的文件。</span><span class="sxs-lookup"><span data-stu-id="18a33-133">Clicking a documentation link points you to documentation that describes how to manually implement the action.</span></span> 

<span data-ttu-id="18a33-134">Advisor 會每小時更新建議。</span><span class="sxs-lookup"><span data-stu-id="18a33-134">Advisor updates recommendations hourly.</span></span> <span data-ttu-id="18a33-135">如果您不想立即對建議採取行動，您可以將它延遲一段時間或加以關閉。</span><span class="sxs-lookup"><span data-stu-id="18a33-135">If you don’t intend to take immediate action on a recommendation, you can snooze it for a specified time period or dismiss it.</span></span> 

## <a name="frequently-asked-questions"></a><span data-ttu-id="18a33-136">常見問題集</span><span class="sxs-lookup"><span data-stu-id="18a33-136">Frequently asked questions</span></span>

### <a name="how-do-i-access-advisor"></a><span data-ttu-id="18a33-137">如何存取建議程式？</span><span class="sxs-lookup"><span data-stu-id="18a33-137">How do I access Advisor?</span></span>
<span data-ttu-id="18a33-138">您可以透過 [Azure 入口網站](https://aka.ms/azureadvisordashboard)存取建議程式。</span><span class="sxs-lookup"><span data-stu-id="18a33-138">You can access Advisor through the [Azure portal](https://aka.ms/azureadvisordashboard).</span></span> <span data-ttu-id="18a33-139">登入[入口網站](https://portal.azure.com)，選取 [瀏覽]，然後捲動至 [Azure Advisor]。</span><span class="sxs-lookup"><span data-stu-id="18a33-139">Sign in to the [portal](https://portal.azure.com), select **Browse**, and then scroll to **Azure Advisor**.</span></span> <span data-ttu-id="18a33-140">[建議程式] 儀表板會顯示所選訂用帳戶的個人化建議。</span><span class="sxs-lookup"><span data-stu-id="18a33-140">The Advisor dashboard displays personalized recommendations for a selected subscription.</span></span> 

<span data-ttu-id="18a33-141">您也可以透過虛擬機器資源刀鋒視窗檢視建議程式建議。</span><span class="sxs-lookup"><span data-stu-id="18a33-141">You can also view Advisor recommendations through the virtual machine resource blade.</span></span> <span data-ttu-id="18a33-142">選擇虛擬機器，然後捲動至功能表中的建議程式建議。</span><span class="sxs-lookup"><span data-stu-id="18a33-142">Choose a virtual machine, and then scroll to Advisor recommendations in the menu.</span></span> 

### <a name="what-permissions-do-i-need-to-access-advisor"></a><span data-ttu-id="18a33-143">我需要哪些權限才能存取建議程式？</span><span class="sxs-lookup"><span data-stu-id="18a33-143">What permissions do I need to access Advisor?</span></span>

<span data-ttu-id="18a33-144">若要存取 Advisor 建議，您必須先向 Advisor「註冊您的訂用帳戶」。</span><span class="sxs-lookup"><span data-stu-id="18a33-144">To access Advisor recommendations, you must first *register your subscription* with Advisor.</span></span> <span data-ttu-id="18a33-145">當「訂用帳戶擁有者」啟動 Advisor 儀表板，然後按一下 [取得建議] 按鈕時，便會註冊訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="18a33-145">A subscription is registered when a *subscription Owner* launches the Advisor dashboard and clicks the **Get recommendations** button.</span></span> <span data-ttu-id="18a33-146">此作業「只需要執行一次」。</span><span class="sxs-lookup"><span data-stu-id="18a33-146">This is a *one-time operation*.</span></span> <span data-ttu-id="18a33-147">註冊訂用帳戶之後，您能以訂用帳戶、資源群組或特定資源的 [擁有者]、[參與者] 或 [讀取者] 身分存取 Advisor 建議。</span><span class="sxs-lookup"><span data-stu-id="18a33-147">After the subscription is registered, you can access Advisor recommendations as *Owner*, *Contributor*, or *Reader* for a subscription, a resource group, or a specific resource.</span></span>

### <a name="how-often-are-advisor-recommendations-updated"></a><span data-ttu-id="18a33-148">建議程式建議的頻率為何？</span><span class="sxs-lookup"><span data-stu-id="18a33-148">How often are Advisor recommendations updated?</span></span>

<span data-ttu-id="18a33-149">Advisor 建議會每小時進行更新。</span><span class="sxs-lookup"><span data-stu-id="18a33-149">Advisor recommendations are updated hourly.</span></span>

### <a name="what-resources-does-advisor-provide-recommendations-for"></a><span data-ttu-id="18a33-150">建議程式可提供哪些資源的建議？</span><span class="sxs-lookup"><span data-stu-id="18a33-150">What resources does Advisor provide recommendations for?</span></span>

<span data-ttu-id="18a33-151">Advisor 可提供虛擬機器、可用性設定組、應用程式閘道、應用程式服務、SQL Server、SQL Database 和 Redis 快取的建議。</span><span class="sxs-lookup"><span data-stu-id="18a33-151">Advisor provides recommendations for virtual machines, availability sets, application gateways, App Services, SQL servers, SQL databases, and Redis Cache.</span></span>

### <a name="can-i-snooze-or-dismiss-a-recommendation"></a><span data-ttu-id="18a33-152">是否可以延遲或解除建議？</span><span class="sxs-lookup"><span data-stu-id="18a33-152">Can I snooze or dismiss a recommendation?</span></span>

<span data-ttu-id="18a33-153">若要延遲或解除建議，請按一下 [延遲] 按鈕或連結。</span><span class="sxs-lookup"><span data-stu-id="18a33-153">To snooze or dismiss a recommendation, click the **Snooze** button or link.</span></span> <span data-ttu-id="18a33-154">您可以指定延遲時間週期，或選取 [永不] 來解除建議。</span><span class="sxs-lookup"><span data-stu-id="18a33-154">You can specify a snooze time period or select **Never** to dismiss the recommendation.</span></span>

## <a name="next-steps"></a><span data-ttu-id="18a33-155">後續步驟</span><span class="sxs-lookup"><span data-stu-id="18a33-155">Next steps</span></span>

<span data-ttu-id="18a33-156">若要深入了解 Advisor 建議，請參閱：</span><span class="sxs-lookup"><span data-stu-id="18a33-156">To learn more about Advisor recommendations, see:</span></span>

* [<span data-ttu-id="18a33-157">開始使用建議程式</span><span class="sxs-lookup"><span data-stu-id="18a33-157">Get started with Advisor</span></span>](advisor-get-started.md)
* [<span data-ttu-id="18a33-158">建議程式高可用性建議</span><span class="sxs-lookup"><span data-stu-id="18a33-158">Advisor High Availability recommendations</span></span>](advisor-high-availability-recommendations.md)
* [<span data-ttu-id="18a33-159">建議程式安全性建議</span><span class="sxs-lookup"><span data-stu-id="18a33-159">Advisor Security recommendations</span></span>](advisor-security-recommendations.md)
* [<span data-ttu-id="18a33-160">建議程式效能建議</span><span class="sxs-lookup"><span data-stu-id="18a33-160">Advisor Performance recommendations</span></span>](advisor-performance-recommendations.md)
* [<span data-ttu-id="18a33-161">建議程式成本建議</span><span class="sxs-lookup"><span data-stu-id="18a33-161">Advisor Cost recommendations</span></span>](advisor-cost-recommendations.md)
