---
title: "aaaEnable Azure 資訊安全中心中的資料收集 |Microsoft 文件"
description: " 深入了解如何在 Azure 資訊安全中心 tooenable 資料收集。 "
services: security-center
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
editor: 
ms.assetid: 411d7bae-c9d4-4e83-be63-9f2f2312b075
ms.service: security-center
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/16/2017
ms.author: terrylan
ms.openlocfilehash: 78bbf9a3d852095e2a1387c1606ff4bbb778a0dd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="enable-data-collection-in-azure-security-center"></a><span data-ttu-id="ed9bb-103">在 Azure 資訊安全中心啟用資料收集</span><span class="sxs-lookup"><span data-stu-id="ed9bb-103">Enable data collection in Azure Security Center</span></span>

> [!NOTE]
> <span data-ttu-id="ed9bb-104">從開始早期年 6 月 2017年，資訊安全中心將會使用 hello Microsoft Monitoring Agent toocollect 及儲存資料。</span><span class="sxs-lookup"><span data-stu-id="ed9bb-104">Beginning in early June 2017, Security Center will use hello Microsoft Monitoring Agent toocollect and store data.</span></span> <span data-ttu-id="ed9bb-105">詳細資訊，請參閱 toolearn [Azure 安全性 Center 平台移轉](security-center-platform-migration.md)。</span><span class="sxs-lookup"><span data-stu-id="ed9bb-105">toolearn more, see [Azure Security Center Platform Migration](security-center-platform-migration.md).</span></span> <span data-ttu-id="ed9bb-106">本文章中的 hello 資訊表示資訊安全中心功能之後轉換 toohello Microsoft Monitoring Agent。</span><span class="sxs-lookup"><span data-stu-id="ed9bb-106">hello information in this article represents Security Center functionality after transition toohello Microsoft Monitoring Agent.</span></span>
>
>

<span data-ttu-id="ed9bb-107">資訊安全中心會收集從虛擬機器 (Vm) tooassess 其資訊安全狀態、 提供安全性建議事項，並警示您 toothreats。</span><span class="sxs-lookup"><span data-stu-id="ed9bb-107">Security Center collects data from your virtual machines (VMs) tooassess their security state, provide security recommendations, and alert you toothreats.</span></span> <span data-ttu-id="ed9bb-108">當您第一次存取資訊安全中心時，您的訂用帳戶中有 hello 選項 tooenable 資料收集的所有 vm。</span><span class="sxs-lookup"><span data-stu-id="ed9bb-108">When you first access Security Center, you have hello option tooenable data collection for all VMs in your subscription.</span></span> <span data-ttu-id="ed9bb-109">如果未啟用資料收集，資訊安全中心會建議您開啟 hello 該訂用帳戶的安全性原則中的資料收集。</span><span class="sxs-lookup"><span data-stu-id="ed9bb-109">If data collection is not enabled, Security Center recommends that you turn on data collection in hello security policy for that subscription.</span></span>

<span data-ttu-id="ed9bb-110">啟用資料收集時，對所有現有的資訊安全中心會佈建 hello Microsoft Monitoring Agent 支援 Azure 虛擬機器和建立任何新的。</span><span class="sxs-lookup"><span data-stu-id="ed9bb-110">When data collection is enabled, Security Center provisions hello Microsoft Monitoring Agent on all existing supported Azure virtual machines and any new ones that are created.</span></span> <span data-ttu-id="ed9bb-111">Microsoft Monitoring Agent hello 掃描的各種安全性相關設定。</span><span class="sxs-lookup"><span data-stu-id="ed9bb-111">hello Microsoft Monitoring Agent scans for various security-related configurations.</span></span> <span data-ttu-id="ed9bb-112">此外，hello 作業系統引發的事件記錄檔事件。</span><span class="sxs-lookup"><span data-stu-id="ed9bb-112">In addition, hello operating system raises event log events.</span></span> <span data-ttu-id="ed9bb-113">這類資料的範例包括︰作業系統類型和版本、作業系統記錄檔 (Windows 事件記錄檔)、執行中程序、電腦名稱、IP 位址、已登入的使用者和租用戶識別碼。</span><span class="sxs-lookup"><span data-stu-id="ed9bb-113">Examples of such data are: operating system type and version, operating system logs (Windows event logs), running processes, machine name, IP addresses, logged in user, and tenant ID.</span></span> <span data-ttu-id="ed9bb-114">hello Microsoft Monitoring Agent 會讀取事件記錄項目和組態，並將複製 hello 資料 tooyour 工作區中的進行分析。</span><span class="sxs-lookup"><span data-stu-id="ed9bb-114">hello Microsoft Monitoring Agent reads event log entries and configurations and copies hello data tooyour workspace for analysis.</span></span> <span data-ttu-id="ed9bb-115">hello Microsoft Monitoring Agent 也會複製損毀傾印檔案 tooyour 工作區。</span><span class="sxs-lookup"><span data-stu-id="ed9bb-115">hello Microsoft Monitoring Agent also copies crash dump files tooyour workspace.</span></span>

<span data-ttu-id="ed9bb-116">如果您使用 hello 免費層的資訊安全中心，您可以關閉 hello 安全性原則中的資料收集停用資料收集，從虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="ed9bb-116">If you are using hello Free tier of Security Center, you can disable data collection from virtual machines by turning off data collection in hello security policy.</span></span> <span data-ttu-id="ed9bb-117">停用資料收集會限制 VM 的安全性評估。</span><span class="sxs-lookup"><span data-stu-id="ed9bb-117">Disabling data collection limits security assessments for your VMs.</span></span> <span data-ttu-id="ed9bb-118">詳細資訊，請參閱 toolearn[停用資料收集](#disabling-data-collection)。</span><span class="sxs-lookup"><span data-stu-id="ed9bb-118">toolearn more, see [Disabling data collection](#disabling-data-collection).</span></span> <span data-ttu-id="ed9bb-119">即使已停用資料集合，仍然會啟用 VM 磁碟快照集和構件集合。</span><span class="sxs-lookup"><span data-stu-id="ed9bb-119">VM disk snapshots and artifact collection are enabled even if data collection has been disabled.</span></span> <span data-ttu-id="ed9bb-120">需要訂閱 hello 標準層的資訊安全中心上的資料收集。</span><span class="sxs-lookup"><span data-stu-id="ed9bb-120">Data collection is required for subscriptions on hello Standard tier of Security Center.</span></span>

> [!NOTE]
> <span data-ttu-id="ed9bb-121">深入了解資訊安全中心的免費和標準[定價層](security-center-pricing.md)。</span><span class="sxs-lookup"><span data-stu-id="ed9bb-121">Learn more about Security Center's Free and Standard [pricing tiers](security-center-pricing.md).</span></span>
>
>

## <a name="implement-hello-recommendation"></a><span data-ttu-id="ed9bb-122">實作 hello 建議</span><span class="sxs-lookup"><span data-stu-id="ed9bb-122">Implement hello recommendation</span></span>

> [!NOTE]
> <span data-ttu-id="ed9bb-123">本文件介紹 hello 服務使用的範例部署。</span><span class="sxs-lookup"><span data-stu-id="ed9bb-123">This document introduces hello service by using an example deployment.</span></span> <span data-ttu-id="ed9bb-124">本文件不是一份逐步解說指南。</span><span class="sxs-lookup"><span data-stu-id="ed9bb-124">This document is not a step-by-step guide.</span></span>
>
>

1. <span data-ttu-id="ed9bb-125">在 hello**建議**刀鋒視窗中，選取**啟用訂用帳戶的資料收集**。</span><span class="sxs-lookup"><span data-stu-id="ed9bb-125">In hello **Recommendations** blade, select **Enable data collection for subscriptions**.</span></span>  <span data-ttu-id="ed9bb-126">這會開啟 hello**開啟資料收集**刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="ed9bb-126">This opens hello **Turn on data collection** blade.</span></span>
   <span data-ttu-id="ed9bb-127">![建議刀鋒視窗][2]</span><span class="sxs-lookup"><span data-stu-id="ed9bb-127">![Recommendations blade][2]</span></span>
2. <span data-ttu-id="ed9bb-128">在 hello**開啟資料收集**刀鋒視窗中，選取您的訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="ed9bb-128">On hello **Turn on data collection** blade, select your subscription.</span></span> <span data-ttu-id="ed9bb-129">hello**安全性原則**該訂用帳戶 刀鋒視窗隨即開啟。</span><span class="sxs-lookup"><span data-stu-id="ed9bb-129">hello **Security policy** blade for that subscription opens.</span></span>
3. <span data-ttu-id="ed9bb-130">在 hello**安全性原則**刀鋒視窗中，選取**上**下**資料收集**tooautomatically 收集記錄檔。</span><span class="sxs-lookup"><span data-stu-id="ed9bb-130">On hello **Security policy** blade, select **On** under **Data collection** tooautomatically collect logs.</span></span> <span data-ttu-id="ed9bb-131">開啟所有目前和新的資料集合會佈建 hello 上監視功能延伸模組支援 hello 訂用帳戶中的 Vm。</span><span class="sxs-lookup"><span data-stu-id="ed9bb-131">Turning on data collection provisions hello monitoring extension on all current and new supported VMs in hello subscription.</span></span>
4. <span data-ttu-id="ed9bb-132">選取 [ **儲存**]。</span><span class="sxs-lookup"><span data-stu-id="ed9bb-132">Select **Save**.</span></span>
5. <span data-ttu-id="ed9bb-133">選取 [確定] 。</span><span class="sxs-lookup"><span data-stu-id="ed9bb-133">Select **OK**.</span></span>

## <a name="disabling-data-collection"></a><span data-ttu-id="ed9bb-134">停用資料收集</span><span class="sxs-lookup"><span data-stu-id="ed9bb-134">Disabling data collection</span></span>
<span data-ttu-id="ed9bb-135">如果您使用 hello 免費層的資訊安全中心，您可以關閉 hello 安全性原則中的資料收集停用在任何時間從虛擬機器的資料收集。</span><span class="sxs-lookup"><span data-stu-id="ed9bb-135">If you are using hello Free tier of Security Center, you can disable data collection from virtual machines at any time by turning off data collection in hello security policy.</span></span> <span data-ttu-id="ed9bb-136">需要訂閱 hello 標準層的資訊安全中心上的資料收集。</span><span class="sxs-lookup"><span data-stu-id="ed9bb-136">Data collection is required for subscriptions on hello Standard tier of Security Center.</span></span>

1. <span data-ttu-id="ed9bb-137">傳回 toohello**資訊安全中心**刀鋒視窗，然後選取 hello**原則**磚。</span><span class="sxs-lookup"><span data-stu-id="ed9bb-137">Return toohello **Security Center** blade and select hello **Policy** tile.</span></span> <span data-ttu-id="ed9bb-138">這會開啟 hello**安全性原則定義每個訂閱的原則**刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="ed9bb-138">This opens hello **Security policy-Define policy per subscription** blade.</span></span>
   <span data-ttu-id="ed9bb-139">![選取 hello 原則磚][5]</span><span class="sxs-lookup"><span data-stu-id="ed9bb-139">![Select hello policy tile][5]</span></span>
2. <span data-ttu-id="ed9bb-140">在 hello**安全性原則定義每個訂閱的原則**刀鋒視窗中，選取 hello 訂用帳戶，您會希望 toodisable 資料收集。</span><span class="sxs-lookup"><span data-stu-id="ed9bb-140">On hello **Security policy-Define policy per subscription** blade, select hello subscription that you wish toodisable data collection.</span></span>
3. <span data-ttu-id="ed9bb-141">hello**安全性原則**該訂用帳戶 刀鋒視窗隨即開啟。</span><span class="sxs-lookup"><span data-stu-id="ed9bb-141">hello **Security policy** blade for that subscription opens.</span></span>  <span data-ttu-id="ed9bb-142">選取 [資料收集] 底下的 [關閉]。</span><span class="sxs-lookup"><span data-stu-id="ed9bb-142">Select **Off** under Data collection.</span></span>
4. <span data-ttu-id="ed9bb-143">選取**儲存**hello 頂端功能區中。</span><span class="sxs-lookup"><span data-stu-id="ed9bb-143">Select **Save** in hello top ribbon.</span></span>

## <a name="next-steps"></a><span data-ttu-id="ed9bb-144">後續步驟</span><span class="sxs-lookup"><span data-stu-id="ed9bb-144">Next steps</span></span>
<span data-ttu-id="ed9bb-145">本文章向您說明如何 tooimplement 會 hello 資訊安全中心建議"啟用資料收集。 」</span><span class="sxs-lookup"><span data-stu-id="ed9bb-145">This article showed you how tooimplement hello Security Center recommendation "Enable data collection.”</span></span> <span data-ttu-id="ed9bb-146">toolearn 有關資訊安全中心的詳細資訊，請參閱 hello 下列資訊：</span><span class="sxs-lookup"><span data-stu-id="ed9bb-146">toolearn more about Security Center, see hello following:</span></span>

* <span data-ttu-id="ed9bb-147">[在 Azure 資訊安全中心中設定安全性原則](security-center-policies.md)-了解如何 tooconfigure 您的 Azure 訂用帳戶和資源群組的安全性原則。</span><span class="sxs-lookup"><span data-stu-id="ed9bb-147">[Setting security policies in Azure Security Center](security-center-policies.md) -- Learn how tooconfigure security policies for your Azure subscriptions and resource groups.</span></span>
* <span data-ttu-id="ed9bb-148">[管理 Azure 資訊安全中心的安全性建議](security-center-recommendations.md) -- 了解建議如何協助保護您的 Azure 資源。</span><span class="sxs-lookup"><span data-stu-id="ed9bb-148">[Managing security recommendations in Azure Security Center](security-center-recommendations.md) -- Learn how recommendations help you protect your Azure resources.</span></span>
* <span data-ttu-id="ed9bb-149">[在 Azure 資訊安全中心中的安全性健全狀況監視](security-center-monitoring.md)-了解如何 toomonitor hello 您的 Azure 資源的健全狀況。</span><span class="sxs-lookup"><span data-stu-id="ed9bb-149">[Security health monitoring in Azure Security Center](security-center-monitoring.md)--Learn how toomonitor hello health of your Azure resources.</span></span>
* <span data-ttu-id="ed9bb-150">[在 Azure 資訊安全中心警示管理，而且有回應 toosecurity](security-center-managing-and-responding-alerts.md)-了解如何 toomanage 和回應 toosecurity 警示。</span><span class="sxs-lookup"><span data-stu-id="ed9bb-150">[Managing and responding toosecurity alerts in Azure Security Center](security-center-managing-and-responding-alerts.md)--Learn how toomanage and respond toosecurity alerts.</span></span>
* <span data-ttu-id="ed9bb-151">[監視與 Azure 資訊安全中心的協力廠商解決方案](security-center-partner-solutions.md)-了解如何 toomonitor hello 的協力廠商解決方案的健全狀況狀態。</span><span class="sxs-lookup"><span data-stu-id="ed9bb-151">[Monitoring partner solutions with Azure Security Center](security-center-partner-solutions.md) -- Learn how toomonitor hello health status of your partner solutions.</span></span>
- <span data-ttu-id="ed9bb-152">[Azure 資訊安全中心資料安全性](security-center-data-security.md) - 了解資訊安全中心如何管理及保護其中的資料。</span><span class="sxs-lookup"><span data-stu-id="ed9bb-152">[Azure Security Center data security](security-center-data-security.md) - Learn how data is managed and safeguarded in Security Center.</span></span>
* <span data-ttu-id="ed9bb-153">[Azure 資訊安全中心常見問題集](security-center-faq.md)-尋找使用 hello 服務相關的常見問題集。</span><span class="sxs-lookup"><span data-stu-id="ed9bb-153">[Azure Security Center FAQ](security-center-faq.md)--Find frequently asked questions about using hello service.</span></span>
* <span data-ttu-id="ed9bb-154">[Azure 安全性部落格](http://blogs.msdn.com/b/azuresecurity/)-取得最新 Azure 安全性消息 hello 和資訊。</span><span class="sxs-lookup"><span data-stu-id="ed9bb-154">[Azure Security blog](http://blogs.msdn.com/b/azuresecurity/)--Get hello latest Azure security news and information.</span></span>

<!--Image references-->
[2]: ./media/security-center-enable-data-collection/recommendations.png
[3]: ./media/security-center-enable-data-collection/data-collection.png
[4]: ./media/security-center-enable-data-collection/storage-account.png
[5]: ./media/security-center-enable-data-collection/policy.png
[6]: ./media/security-center-enable-data-collection/disable-data-collection.png
