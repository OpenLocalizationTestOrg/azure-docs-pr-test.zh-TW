---
title: "aaaIntroduction tooAzure Advisor |Microsoft 文件"
description: "使用 Azure Advisor toooptimize 您的 Azure 部署。"
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
ms.openlocfilehash: 5d796fc06366221efdb6f1bda39ab3fb676abfd2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-tooazure-advisor"></a><span data-ttu-id="e2e0b-103">簡介 tooAzure Advisor</span><span class="sxs-lookup"><span data-stu-id="e2e0b-103">Introduction tooAzure Advisor</span></span>

<span data-ttu-id="e2e0b-104">了解 Azure Advisor 和其索引鍵的功能，並取得常見問題的解答 toofrequently。</span><span class="sxs-lookup"><span data-stu-id="e2e0b-104">Learn about Azure Advisor and its key capabilities, and get answers toofrequently asked questions.</span></span>

## <a name="what-is-advisor"></a><span data-ttu-id="e2e0b-105">何謂 Advisor？</span><span class="sxs-lookup"><span data-stu-id="e2e0b-105">What is Advisor?</span></span>
<span data-ttu-id="e2e0b-106">Advisor 是個人化的雲端顧問，可協助您遵循最佳作法 toooptimize 您的 Azure 部署。</span><span class="sxs-lookup"><span data-stu-id="e2e0b-106">Advisor is a personalized cloud consultant that helps you follow best practices toooptimize your Azure deployments.</span></span> <span data-ttu-id="e2e0b-107">它會分析您的資源設定和使用遙測，並再建議解決方案，協助您改善 hello 成本效益、 效能、 高可用性和您的 Azure 資源的安全性。</span><span class="sxs-lookup"><span data-stu-id="e2e0b-107">It analyzes your resource configuration and usage telemetry and then recommends solutions that can help you improve hello cost effectiveness, performance, high availability, and security of your Azure resources.</span></span>

<span data-ttu-id="e2e0b-108">使用 Advisor，您可以：</span><span class="sxs-lookup"><span data-stu-id="e2e0b-108">With Advisor, you can:</span></span>
* <span data-ttu-id="e2e0b-109">取得主動式、可採取動作且個人化的最佳做法建議。</span><span class="sxs-lookup"><span data-stu-id="e2e0b-109">Get proactive, actionable, and personalized best practices recommendations.</span></span> 
* <span data-ttu-id="e2e0b-110">識別 Azure 整體支出的機會 tooreduce 提升 hello 效能、 安全性及您資源的高可用性。</span><span class="sxs-lookup"><span data-stu-id="e2e0b-110">Improve hello performance, security, and high availability of your resources, as you identify opportunities tooreduce your overall Azure spend.</span></span>
* <span data-ttu-id="e2e0b-111">取得內嵌了提議動作的建議。</span><span class="sxs-lookup"><span data-stu-id="e2e0b-111">Get recommendations with proposed actions inline.</span></span>

<span data-ttu-id="e2e0b-112">您可以透過 hello 存取 Advisor [Azure 入口網站](https://aka.ms/azureadvisordashboard)。</span><span class="sxs-lookup"><span data-stu-id="e2e0b-112">You can access Advisor through hello [Azure portal](https://aka.ms/azureadvisordashboard).</span></span> <span data-ttu-id="e2e0b-113">登入 toohello[入口網站](https://portal.azure.com)，選取**瀏覽**，然後捲動太**Azure Advisor**。</span><span class="sxs-lookup"><span data-stu-id="e2e0b-113">Sign in toohello [portal](https://portal.azure.com), select **Browse**, and then scroll too**Azure Advisor**.</span></span> <span data-ttu-id="e2e0b-114">hello Advisor 儀表板會顯示選取的訂用帳戶的個人化的建議。</span><span class="sxs-lookup"><span data-stu-id="e2e0b-114">hello Advisor dashboard displays personalized recommendations for a selected subscription.</span></span> 

<span data-ttu-id="e2e0b-115">hello 建議分為四種分類：</span><span class="sxs-lookup"><span data-stu-id="e2e0b-115">hello recommendations are divided into four categories:</span></span> 

* <span data-ttu-id="e2e0b-116">**高可用性**: tooensure 和改善的業務關鍵應用程式的 hello 持續性。</span><span class="sxs-lookup"><span data-stu-id="e2e0b-116">**High Availability**: tooensure and improve hello continuity of your business-critical applications.</span></span> <span data-ttu-id="e2e0b-117">如需詳細資訊，請參閱[建議程式高可用性的建議](advisor-high-availability-recommendations.md)。</span><span class="sxs-lookup"><span data-stu-id="e2e0b-117">For more information, see [Advisor High Availability recommendations](advisor-high-availability-recommendations.md).</span></span>

* <span data-ttu-id="e2e0b-118">**安全性**: toodetect 威脅與弱點可能會導致 toosecurity 漏洞。</span><span class="sxs-lookup"><span data-stu-id="e2e0b-118">**Security**: toodetect threats and vulnerabilities that might lead toosecurity breaches.</span></span> <span data-ttu-id="e2e0b-119">如需詳細資訊，請參閱[建議程式安全性建議](advisor-security-recommendations.md)。</span><span class="sxs-lookup"><span data-stu-id="e2e0b-119">For more information, see [Advisor Security recommendations](advisor-security-recommendations.md).</span></span>

* <span data-ttu-id="e2e0b-120">**效能**: tooimprove hello 速度的應用程式。</span><span class="sxs-lookup"><span data-stu-id="e2e0b-120">**Performance**: tooimprove hello speed of your applications.</span></span> <span data-ttu-id="e2e0b-121">如需詳細資訊，請參閱[建議程式效能建議](advisor-performance-recommendations.md)。</span><span class="sxs-lookup"><span data-stu-id="e2e0b-121">For more information, see [Advisor Performance recommendations](advisor-performance-recommendations.md).</span></span>

* <span data-ttu-id="e2e0b-122">**成本**: toooptimize 並減少整體 Azure 支出。</span><span class="sxs-lookup"><span data-stu-id="e2e0b-122">**Cost**: toooptimize and reduce your overall Azure spend.</span></span> <span data-ttu-id="e2e0b-123">如需詳細資訊，請參閱[建議程式成本建議](advisor-cost-recommendations.md)。</span><span class="sxs-lookup"><span data-stu-id="e2e0b-123">For more information, see [Advisor Cost recommendations](advisor-cost-recommendations.md).</span></span>

  ![建議程式建議類型](./media/advisor-overview/advisor-all-tab-examples.png)

> [!NOTE]
> <span data-ttu-id="e2e0b-125">tooaccess Advisor 的建議，您必須先*註冊您的訂閱*與 Advisor。</span><span class="sxs-lookup"><span data-stu-id="e2e0b-125">tooaccess Advisor recommendations, you must first *register your subscription* with Advisor.</span></span> <span data-ttu-id="e2e0b-126">已經註冊訂閱時*訂用帳戶擁有者*啟動 hello Advisor 儀表板，並按一下 hello**取得建議** 按鈕。</span><span class="sxs-lookup"><span data-stu-id="e2e0b-126">A subscription is registered when a *subscription Owner* launches hello Advisor dashboard and clicks hello **Get recommendations** button.</span></span> <span data-ttu-id="e2e0b-127">此作業「只需要執行一次」。</span><span class="sxs-lookup"><span data-stu-id="e2e0b-127">This is a *one-time operation*.</span></span> <span data-ttu-id="e2e0b-128">Hello 訂用帳戶註冊之後，您可以存取 Advisor 的建議做為*擁有者*，*參與者*，或*讀取器*訂用帳戶，資源群組，或特定的資源。</span><span class="sxs-lookup"><span data-stu-id="e2e0b-128">After hello subscription is registered, you can access Advisor recommendations as *Owner*, *Contributor*, or *Reader* for a subscription, a resource group, or a specific resource.</span></span>

<span data-ttu-id="e2e0b-129">您可以按一下建議 toolearn 詳細資訊，請參閱。</span><span class="sxs-lookup"><span data-stu-id="e2e0b-129">You can click a recommendation toolearn more about it.</span></span> <span data-ttu-id="e2e0b-130">您可以執行的機會 tootake 優點，或解決的問題，您也可以了解動作。</span><span class="sxs-lookup"><span data-stu-id="e2e0b-130">You can also learn about actions that you can perform tootake advantage of an opportunity or resolve an issue.</span></span> 

<span data-ttu-id="e2e0b-131">建議程式可透過內嵌動作或文件連結提供建議。</span><span class="sxs-lookup"><span data-stu-id="e2e0b-131">Advisor offers recommendations with inline actions or documentation links.</span></span> <span data-ttu-id="e2e0b-132">按一下內嵌動作會引導您完成 「 引導式的使用者之旅"tooimplement 它。</span><span class="sxs-lookup"><span data-stu-id="e2e0b-132">Clicking an inline action takes you through a “guided user journey” tooimplement it.</span></span> <span data-ttu-id="e2e0b-133">按一下文件的連結會指向 toodocumentation 描述 toomanually 實作 hello 動作的方式。</span><span class="sxs-lookup"><span data-stu-id="e2e0b-133">Clicking a documentation link points you toodocumentation that describes how toomanually implement hello action.</span></span> 

<span data-ttu-id="e2e0b-134">Advisor 會每小時更新建議。</span><span class="sxs-lookup"><span data-stu-id="e2e0b-134">Advisor updates recommendations hourly.</span></span> <span data-ttu-id="e2e0b-135">如果您不想 tootake 立即採取行動的建議，您可以延遲一段指定的時間，或關閉它。</span><span class="sxs-lookup"><span data-stu-id="e2e0b-135">If you don’t intend tootake immediate action on a recommendation, you can snooze it for a specified time period or dismiss it.</span></span> 

## <a name="frequently-asked-questions"></a><span data-ttu-id="e2e0b-136">常見問題集</span><span class="sxs-lookup"><span data-stu-id="e2e0b-136">Frequently asked questions</span></span>

### <a name="how-do-i-access-advisor"></a><span data-ttu-id="e2e0b-137">如何存取建議程式？</span><span class="sxs-lookup"><span data-stu-id="e2e0b-137">How do I access Advisor?</span></span>
<span data-ttu-id="e2e0b-138">您可以透過 hello 存取 Advisor [Azure 入口網站](https://aka.ms/azureadvisordashboard)。</span><span class="sxs-lookup"><span data-stu-id="e2e0b-138">You can access Advisor through hello [Azure portal](https://aka.ms/azureadvisordashboard).</span></span> <span data-ttu-id="e2e0b-139">登入 toohello[入口網站](https://portal.azure.com)，選取**瀏覽**，然後捲動太**Azure Advisor**。</span><span class="sxs-lookup"><span data-stu-id="e2e0b-139">Sign in toohello [portal](https://portal.azure.com), select **Browse**, and then scroll too**Azure Advisor**.</span></span> <span data-ttu-id="e2e0b-140">hello Advisor 儀表板會顯示選取的訂用帳戶的個人化的建議。</span><span class="sxs-lookup"><span data-stu-id="e2e0b-140">hello Advisor dashboard displays personalized recommendations for a selected subscription.</span></span> 

<span data-ttu-id="e2e0b-141">您也可以透過 hello 虛擬機器資源刀鋒視窗中檢視 Advisor 的建議。</span><span class="sxs-lookup"><span data-stu-id="e2e0b-141">You can also view Advisor recommendations through hello virtual machine resource blade.</span></span> <span data-ttu-id="e2e0b-142">選擇虛擬機器，，然後捲動 tooAdvisor hello 功能表中的建議。</span><span class="sxs-lookup"><span data-stu-id="e2e0b-142">Choose a virtual machine, and then scroll tooAdvisor recommendations in hello menu.</span></span> 

### <a name="what-permissions-do-i-need-tooaccess-advisor"></a><span data-ttu-id="e2e0b-143">權限的執行需要 tooaccess Advisor 嗎？</span><span class="sxs-lookup"><span data-stu-id="e2e0b-143">What permissions do I need tooaccess Advisor?</span></span>

<span data-ttu-id="e2e0b-144">tooaccess Advisor 的建議，您必須先*註冊您的訂閱*與 Advisor。</span><span class="sxs-lookup"><span data-stu-id="e2e0b-144">tooaccess Advisor recommendations, you must first *register your subscription* with Advisor.</span></span> <span data-ttu-id="e2e0b-145">已經註冊訂閱時*訂用帳戶擁有者*啟動 hello Advisor 儀表板，並按一下 hello**取得建議** 按鈕。</span><span class="sxs-lookup"><span data-stu-id="e2e0b-145">A subscription is registered when a *subscription Owner* launches hello Advisor dashboard and clicks hello **Get recommendations** button.</span></span> <span data-ttu-id="e2e0b-146">此作業「只需要執行一次」。</span><span class="sxs-lookup"><span data-stu-id="e2e0b-146">This is a *one-time operation*.</span></span> <span data-ttu-id="e2e0b-147">Hello 訂用帳戶註冊之後，您可以存取 Advisor 的建議做為*擁有者*，*參與者*，或*讀取器*訂用帳戶，資源群組，或特定的資源。</span><span class="sxs-lookup"><span data-stu-id="e2e0b-147">After hello subscription is registered, you can access Advisor recommendations as *Owner*, *Contributor*, or *Reader* for a subscription, a resource group, or a specific resource.</span></span>

### <a name="how-often-are-advisor-recommendations-updated"></a><span data-ttu-id="e2e0b-148">建議程式建議的頻率為何？</span><span class="sxs-lookup"><span data-stu-id="e2e0b-148">How often are Advisor recommendations updated?</span></span>

<span data-ttu-id="e2e0b-149">Advisor 建議會每小時進行更新。</span><span class="sxs-lookup"><span data-stu-id="e2e0b-149">Advisor recommendations are updated hourly.</span></span>

### <a name="what-resources-does-advisor-provide-recommendations-for"></a><span data-ttu-id="e2e0b-150">建議程式可提供哪些資源的建議？</span><span class="sxs-lookup"><span data-stu-id="e2e0b-150">What resources does Advisor provide recommendations for?</span></span>

<span data-ttu-id="e2e0b-151">Advisor 可提供虛擬機器、可用性設定組、應用程式閘道、應用程式服務、SQL Server、SQL Database 和 Redis 快取的建議。</span><span class="sxs-lookup"><span data-stu-id="e2e0b-151">Advisor provides recommendations for virtual machines, availability sets, application gateways, App Services, SQL servers, SQL databases, and Redis Cache.</span></span>

### <a name="can-i-snooze-or-dismiss-a-recommendation"></a><span data-ttu-id="e2e0b-152">是否可以延遲或解除建議？</span><span class="sxs-lookup"><span data-stu-id="e2e0b-152">Can I snooze or dismiss a recommendation?</span></span>

<span data-ttu-id="e2e0b-153">toosnooze 或關閉建議，請按一下 hello**延期**按鈕或連結。</span><span class="sxs-lookup"><span data-stu-id="e2e0b-153">toosnooze or dismiss a recommendation, click hello **Snooze** button or link.</span></span> <span data-ttu-id="e2e0b-154">您可以指定延遲時間週期或選取**永不**toodismiss hello 建議。</span><span class="sxs-lookup"><span data-stu-id="e2e0b-154">You can specify a snooze time period or select **Never** toodismiss hello recommendation.</span></span>

## <a name="next-steps"></a><span data-ttu-id="e2e0b-155">後續步驟</span><span class="sxs-lookup"><span data-stu-id="e2e0b-155">Next steps</span></span>

<span data-ttu-id="e2e0b-156">toolearn 深入了解 Advisor 的建議，請參閱：</span><span class="sxs-lookup"><span data-stu-id="e2e0b-156">toolearn more about Advisor recommendations, see:</span></span>

* [<span data-ttu-id="e2e0b-157">開始使用建議程式</span><span class="sxs-lookup"><span data-stu-id="e2e0b-157">Get started with Advisor</span></span>](advisor-get-started.md)
* [<span data-ttu-id="e2e0b-158">建議程式高可用性建議</span><span class="sxs-lookup"><span data-stu-id="e2e0b-158">Advisor High Availability recommendations</span></span>](advisor-high-availability-recommendations.md)
* [<span data-ttu-id="e2e0b-159">建議程式安全性建議</span><span class="sxs-lookup"><span data-stu-id="e2e0b-159">Advisor Security recommendations</span></span>](advisor-security-recommendations.md)
* [<span data-ttu-id="e2e0b-160">建議程式效能建議</span><span class="sxs-lookup"><span data-stu-id="e2e0b-160">Advisor Performance recommendations</span></span>](advisor-performance-recommendations.md)
* [<span data-ttu-id="e2e0b-161">建議程式成本建議</span><span class="sxs-lookup"><span data-stu-id="e2e0b-161">Advisor Cost recommendations</span></span>](advisor-cost-recommendations.md)
