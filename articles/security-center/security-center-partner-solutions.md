---
title: "在 Azure 資訊安全中心 aaaManaging 協力廠商解決方案 |Microsoft 文件"
description: "這份文件會引導您如何 Azure 資訊安全中心可讓您監視在您與您 Azure 訂用帳戶整合的協力廠商解決方案概覽 hello 健全狀況狀態。"
services: security-center
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
editor: 
ms.assetid: 70c076ef-3ad4-4000-a0c1-0ac0c9796ff1
ms.service: security-center
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/17/2017
ms.author: terrylan
ms.openlocfilehash: fc97aedf709b9044bfd3d4ecae0b58d5fa716bbb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="monitoring-partner-solutions-with-azure-security-center"></a><span data-ttu-id="068ed-103">使用 Azure 資訊安全中心監視合作夥伴解決方案</span><span class="sxs-lookup"><span data-stu-id="068ed-103">Monitoring partner solutions with Azure Security Center</span></span>
<span data-ttu-id="068ed-104">這份文件會引導您如何 toomonitor hello Azure 資訊安全中心夥伴方案的健全狀況狀態。</span><span class="sxs-lookup"><span data-stu-id="068ed-104">This document walks you through how toomonitor hello health status of your partner solutions in Azure Security Center.</span></span>

> [!NOTE]
> <span data-ttu-id="068ed-105">本文件介紹 hello 服務使用的範例部署。</span><span class="sxs-lookup"><span data-stu-id="068ed-105">This document introduces hello service by using an example deployment.</span></span> <span data-ttu-id="068ed-106">本文件不是一份逐步解說指南。</span><span class="sxs-lookup"><span data-stu-id="068ed-106">This document is not a step-by-step guide.</span></span>
>
>

## <a name="monitoring-partner-solutions"></a><span data-ttu-id="068ed-107">監視合作夥伴解決方案</span><span class="sxs-lookup"><span data-stu-id="068ed-107">Monitoring partner solutions</span></span>
<span data-ttu-id="068ed-108">hello**合作夥伴解決方案**磚 hello**資訊安全中心**刀鋒視窗可讓您監視在您與您 Azure 訂用帳戶整合的協力廠商解決方案概覽 hello 健全狀況狀態。</span><span class="sxs-lookup"><span data-stu-id="068ed-108">hello **Partner solutions** tile on hello **Security Center** blade lets you monitor at a glance hello health status of your partner solutions that are integrated with your Azure subscription.</span></span>

![合作夥伴解決方案圖格][1]

<span data-ttu-id="068ed-110">hello**合作夥伴解決方案**磚會顯示 hello 數目與您的訂閱整合的協力廠商解決方案。</span><span class="sxs-lookup"><span data-stu-id="068ed-110">hello **Partner solutions** tile displays hello number of partner solutions integrated with your subscription.</span></span> <span data-ttu-id="068ed-111">如果沒有任何解決方案整合，hello 磚會顯示 hello 數字的零。</span><span class="sxs-lookup"><span data-stu-id="068ed-111">If there are no solutions integrated, hello tile displays hello number zero.</span></span>

<span data-ttu-id="068ed-112">協力廠商解決方案的 tooview hello 健康狀態：</span><span class="sxs-lookup"><span data-stu-id="068ed-112">tooview hello health of your partner solutions:</span></span>

1. <span data-ttu-id="068ed-113">選取 hello**合作夥伴解決方案**磚。</span><span class="sxs-lookup"><span data-stu-id="068ed-113">Select hello **Partner solutions** tile.</span></span> <span data-ttu-id="068ed-114">hello**合作夥伴解決方案**刀鋒視窗隨即開啟，顯示一份協力廠商解決方案連接 tooSecurity 中心。</span><span class="sxs-lookup"><span data-stu-id="068ed-114">hello **Partner solutions** blade opens displaying a list of your partner solutions connected tooSecurity Center.</span></span>

   ![合作夥伴解決方案][3]

   <span data-ttu-id="068ed-116">協力廠商解決方案的 hello 狀態可以是：</span><span class="sxs-lookup"><span data-stu-id="068ed-116">hello status of a partner solution can be:</span></span>

   * <span data-ttu-id="068ed-117">受保護 (綠色) - 沒有任何健康問題。</span><span class="sxs-lookup"><span data-stu-id="068ed-117">Protected (green) - there is no health issue.</span></span>
   * <span data-ttu-id="068ed-118">狀況不良 (紅色) - 有需要立即注意的健康狀態問題。</span><span class="sxs-lookup"><span data-stu-id="068ed-118">Unhealthy (red) - there is a health issue that requires immediate attention.</span></span>
   * <span data-ttu-id="068ed-119">停止報告 （橘色）-hello 方案已停止報告其健全狀況。</span><span class="sxs-lookup"><span data-stu-id="068ed-119">Stopped reporting (orange) - hello solution has stopped reporting its health.</span></span>
   * <span data-ttu-id="068ed-120">未知的保護狀態 （橘色）-hello 方案 hello 健全狀況是未知的到期 tooa 失敗的加入新的資源 toohello 現有方案的程序這一次。</span><span class="sxs-lookup"><span data-stu-id="068ed-120">Unknown protection status (orange) - hello health of hello solution is unknown at this time due tooa failed process of adding a new resource toohello existing solution.</span></span>
   * <span data-ttu-id="068ed-121">不會報告 （灰色）-hello 方案沒有回報任何項目，但如果最近已連線，而且仍將部署方案的狀態可能會回報。</span><span class="sxs-lookup"><span data-stu-id="068ed-121">Not reported (gray) - hello solution has not reported anything yet, a solution's status may be unreported if it has recently been connected and is still deploying.</span></span>

2. <span data-ttu-id="068ed-122">選取合作夥伴解決方案。</span><span class="sxs-lookup"><span data-stu-id="068ed-122">Select a partner solution.</span></span> <span data-ttu-id="068ed-123">在此範例中，可讓選取的 hello **Qualys**方案。</span><span class="sxs-lookup"><span data-stu-id="068ed-123">In this example, lets select hello **Qualys** solution.</span></span>  <span data-ttu-id="068ed-124">刀鋒視窗會開啟顯示 hello 夥伴方案和 hello 方案 hello 狀態相關聯的資源。</span><span class="sxs-lookup"><span data-stu-id="068ed-124">A blade opens showing you hello status of hello partner solution and hello solution's associated resources.</span></span> <span data-ttu-id="068ed-125">選取**方案主控台**tooopen hello 夥伴管理體驗此解決方案。</span><span class="sxs-lookup"><span data-stu-id="068ed-125">Select **Solution console** tooopen hello partner management experience for this solution.</span></span>

   ![合作夥伴解決方案詳細資料][4]
3. <span data-ttu-id="068ed-127">返回 toohello **Qualys**刀鋒視窗，然後選取**連結 VM**。</span><span class="sxs-lookup"><span data-stu-id="068ed-127">Go back toohello **Qualys** blade and select **Link VM**.</span></span> <span data-ttu-id="068ed-128">hello**連結應用程式**刀鋒視窗隨即開啟。</span><span class="sxs-lookup"><span data-stu-id="068ed-128">hello **Link Applications** blade opens.</span></span> <span data-ttu-id="068ed-129">您可以在這裡連接資源 toohello 協力廠商解決方案。</span><span class="sxs-lookup"><span data-stu-id="068ed-129">Here you can connect resources toohello partner solution.</span></span>

   ![連結資源 toopartner 方案][5]

## <a name="next-steps"></a><span data-ttu-id="068ed-131">後續步驟</span><span class="sxs-lookup"><span data-stu-id="068ed-131">Next steps</span></span>
<span data-ttu-id="068ed-132">在本文件中，您所導入了的 toohello**協力廠商解決方案**磚中的資訊安全中心。</span><span class="sxs-lookup"><span data-stu-id="068ed-132">In this document, you were introduced toohello **Partner Solutions** tile in Security Center.</span></span> <span data-ttu-id="068ed-133">toolearn 有關資訊安全中心的詳細資訊，請參閱下列文章 hello:</span><span class="sxs-lookup"><span data-stu-id="068ed-133">toolearn more about Security Center, see hello following articles:</span></span>

* <span data-ttu-id="068ed-134">[在 Azure 資訊安全中心中設定安全性原則](security-center-policies.md)— 了解如何 tooconfigure 您的 Azure 訂用帳戶和資源群組的安全性原則。</span><span class="sxs-lookup"><span data-stu-id="068ed-134">[Setting security policies in Azure Security Center](security-center-policies.md) — Learn how tooconfigure security policies for your Azure subscriptions and resource groups.</span></span>
* <span data-ttu-id="068ed-135">[管理 Azure 資訊安全中心的安全性建議](security-center-recommendations.md) — 了解建議如何協助保護您的 Azure 資源。</span><span class="sxs-lookup"><span data-stu-id="068ed-135">[Managing security recommendations in Azure Security Center](security-center-recommendations.md) — Learn how recommendations help you protect your Azure resources.</span></span>
* <span data-ttu-id="068ed-136">[在 Azure 資訊安全中心中的安全性健全狀況監視](security-center-monitoring.md)— 了解如何 toomonitor hello 您的 Azure 資源的健全狀況。</span><span class="sxs-lookup"><span data-stu-id="068ed-136">[Security health monitoring in Azure Security Center](security-center-monitoring.md) — Learn how toomonitor hello health of your Azure resources.</span></span>
* <span data-ttu-id="068ed-137">[Azure 資訊安全中心警示管理，而且有回應 toosecurity](security-center-managing-and-responding-alerts.md) — 了解如何 toomanage 和回應 toosecurity 警示。</span><span class="sxs-lookup"><span data-stu-id="068ed-137">[Managing and responding toosecurity alerts in Azure Security Center](security-center-managing-and-responding-alerts.md) — Learn how toomanage and respond toosecurity alerts.</span></span>
* <span data-ttu-id="068ed-138">[Azure 資訊安全中心常見問題集](security-center-faq.md)— 尋找使用 hello 服務相關的常見問題集。</span><span class="sxs-lookup"><span data-stu-id="068ed-138">[Azure Security Center FAQ](security-center-faq.md) — Find frequently asked questions about using hello service.</span></span>
* <span data-ttu-id="068ed-139">[Azure 安全性部落格](http://blogs.msdn.com/b/azuresecurity/)— 取得最新 Azure 安全性消息 hello 和資訊。</span><span class="sxs-lookup"><span data-stu-id="068ed-139">[Azure Security blog](http://blogs.msdn.com/b/azuresecurity/) — Get hello latest Azure security news and information.</span></span>

<!--Image references-->
[1]: ./media/security-center-partner-solutions/partner-solutions-tile.png
[3]: ./media/security-center-partner-solutions/partner-solutions.png
[4]: ./media/security-center-partner-solutions/partner-solutions-detail.png
[5]: ./media/security-center-partner-solutions/link-applications.png
