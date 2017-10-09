---
title: "aaaAzure 資訊安全中心快速入門指南 |Microsoft 文件"
description: "這篇文章可協助您快速開始使用 Azure 資訊安全中心帶領您完成 hello 安全性監視和原則管理元件，並將您連結 toonext 步驟。"
services: security-center
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
editor: 
ms.assetid: 61e95a87-39c5-48f5-aee6-6f90ddcd336e
ms.service: security-center
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/16/2017
ms.author: terrylan
ms.openlocfilehash: 23b2444ba1ba30d0a1bd1a1afbc4fd0abfd0827c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-security-center-quick-start-guide"></a><span data-ttu-id="17407-103">Azure 資訊安全中心快速入門指南</span><span class="sxs-lookup"><span data-stu-id="17407-103">Azure Security Center quick start guide</span></span>
<span data-ttu-id="17407-104">這篇文章可協助您快速地開始使用 Azure 資訊安全中心透過帶領您完成 hello 安全性監視和原則管理元件的資訊安全中心。</span><span class="sxs-lookup"><span data-stu-id="17407-104">This article helps you quickly get started with Azure Security Center by guiding you through hello security monitoring and policy management components of Security Center.</span></span>

> [!NOTE]
> <span data-ttu-id="17407-105">從開始早期年 6 月 2017年，資訊安全中心將會使用 hello Microsoft Monitoring Agent toocollect 及儲存資料。</span><span class="sxs-lookup"><span data-stu-id="17407-105">Beginning in early June 2017, Security Center will use hello Microsoft Monitoring Agent toocollect and store data.</span></span> <span data-ttu-id="17407-106">請參閱[Azure 安全性 Center 平台移轉](security-center-platform-migration.md)toolearn 更多。</span><span class="sxs-lookup"><span data-stu-id="17407-106">See [Azure Security Center Platform Migration](security-center-platform-migration.md) toolearn more.</span></span> <span data-ttu-id="17407-107">本文章中的 hello 資訊表示資訊安全中心功能之後轉換 toohello Microsoft Monitoring Agent。</span><span class="sxs-lookup"><span data-stu-id="17407-107">hello information in this article represents Security Center functionality after transition toohello Microsoft Monitoring Agent.</span></span>
>
>

## <a name="prerequisites"></a><span data-ttu-id="17407-108">必要條件</span><span class="sxs-lookup"><span data-stu-id="17407-108">Prerequisites</span></span>
<span data-ttu-id="17407-109">tooget 啟動與資訊安全中心，您必須擁有 Azure 的訂用帳戶 tooMicrosoft。</span><span class="sxs-lookup"><span data-stu-id="17407-109">tooget started with Security Center, you must have a subscription tooMicrosoft Azure.</span></span> <span data-ttu-id="17407-110">如果您沒有訂用帳戶，可以註冊[免費帳戶](https://azure.microsoft.com/pricing/free-trial/)。</span><span class="sxs-lookup"><span data-stu-id="17407-110">If you do not have a subscription, you can sign up for a [free account](https://azure.microsoft.com/pricing/free-trial/).</span></span>

<span data-ttu-id="17407-111">hello 免費層的資訊安全中心與您的訂用帳戶會自動啟用，並提供您的 Azure 資源 hello 安全性狀態的可視性。</span><span class="sxs-lookup"><span data-stu-id="17407-111">hello Free tier of Security Center is automatically enabled with your subscription and provides visibility into hello security state of your Azure resources.</span></span> <span data-ttu-id="17407-112">它提供基本的安全性原則管理、安全性建議並整合 Azure 合作夥伴的安全性產品和服務。</span><span class="sxs-lookup"><span data-stu-id="17407-112">It provides basic security policy management, security recommendations, and integration with security products and services from Azure partners.</span></span>

<span data-ttu-id="17407-113">您可以存取的資訊安全中心從 hello [Azure 入口網站](https://azure.microsoft.com/features/azure-portal/)。</span><span class="sxs-lookup"><span data-stu-id="17407-113">You access Security Center from hello [Azure portal](https://azure.microsoft.com/features/azure-portal/).</span></span> <span data-ttu-id="17407-114">toolearn 深入了解 hello Azure 入口網站，請參閱 hello[入口網站的文件](https://azure.microsoft.com/documentation/services/azure-portal/)。</span><span class="sxs-lookup"><span data-stu-id="17407-114">toolearn more about hello Azure portal, see hello [portal documentation](https://azure.microsoft.com/documentation/services/azure-portal/).</span></span>

## <a name="permissions"></a><span data-ttu-id="17407-115">權限</span><span class="sxs-lookup"><span data-stu-id="17407-115">Permissions</span></span>
<span data-ttu-id="17407-116">資訊安全中心，因此您只看到相關的資訊 tooan 指派資源所屬的 hello 訂用帳戶或資源群組的擁有者、 參與者或讀取器 hello 角色時的 Azure 資源。</span><span class="sxs-lookup"><span data-stu-id="17407-116">In Security Center, you only see information related tooan Azure resource when you are assigned hello role of Owner, Contributor, or Reader for hello subscription or resource group that a resource belongs to.</span></span> <span data-ttu-id="17407-117">請參閱[Azure 資訊安全中心中的權限](security-center-permissions.md)toolearn 深入了解角色與資訊安全中心所允許的動作。</span><span class="sxs-lookup"><span data-stu-id="17407-117">See [Permissions in Azure Security Center](security-center-permissions.md) toolearn more about roles and allowed actions in Security Center.</span></span>

## <a name="data-collection"></a><span data-ttu-id="17407-118">資料收集</span><span class="sxs-lookup"><span data-stu-id="17407-118">Data collection</span></span>
<span data-ttu-id="17407-119">資訊安全中心會收集從虛擬機器 (Vm) tooassess 其資訊安全狀態、 提供安全性建議事項，並警示您 toothreats。</span><span class="sxs-lookup"><span data-stu-id="17407-119">Security Center collects data from your virtual machines (VMs) tooassess their security state, provide security recommendations, and alert you toothreats.</span></span> <span data-ttu-id="17407-120">當您第一次存取資訊安全中心時，訂用帳戶中的所有 VM 都會啟用資料收集。</span><span class="sxs-lookup"><span data-stu-id="17407-120">When you first access Security Center, data collection is enabled on all VMs in your subscription.</span></span> <span data-ttu-id="17407-121">對所有現有的資訊安全中心會佈建 hello Microsoft Monitoring Agent 支援的 Azure Vm 和建立任何新的。</span><span class="sxs-lookup"><span data-stu-id="17407-121">Security Center provisions hello Microsoft Monitoring Agent on all existing supported Azure VMs and any new ones that are created.</span></span> <span data-ttu-id="17407-122">請參閱[啟用資料收集](security-center-enable-data-collection.md)toolearn 更多關於資料收集的運作方式。</span><span class="sxs-lookup"><span data-stu-id="17407-122">See [Enable data collection](security-center-enable-data-collection.md) toolearn more about how data collection works.</span></span>

<span data-ttu-id="17407-123">建議您啟用資料收集。</span><span class="sxs-lookup"><span data-stu-id="17407-123">Data collection is recommended.</span></span> <span data-ttu-id="17407-124">如果您使用 hello 免費層的資訊安全中心，您可以關閉資料收集 hello 安全性原則中停用的 Vm 所傳來的資料收集。</span><span class="sxs-lookup"><span data-stu-id="17407-124">If you are using hello Free tier of Security Center, you can disable data collection from VMs by turning off data collection in hello security policy.</span></span> <span data-ttu-id="17407-125">需要訂閱 hello 標準層的資訊安全中心上的資料收集。</span><span class="sxs-lookup"><span data-stu-id="17407-125">Data collection is required for subscriptions on hello Standard tier of Security Center.</span></span> <span data-ttu-id="17407-126">請參閱[資訊安全中心定價](security-center-pricing.md)toolearn 深入了解 hello 免費及標準定價層。</span><span class="sxs-lookup"><span data-stu-id="17407-126">See [Security Center pricing](security-center-pricing.md) toolearn more about hello Free and Standard pricing tiers.</span></span>

<span data-ttu-id="17407-127">hello 下列步驟說明 tooaccess 並用 hello 資訊安全中心的元件。</span><span class="sxs-lookup"><span data-stu-id="17407-127">hello following steps describe how tooaccess and use hello components of Security Center.</span></span> <span data-ttu-id="17407-128">在這些步驟中，我們會示範如何關閉資料收集，如果您選擇出 tooopt tooturn。</span><span class="sxs-lookup"><span data-stu-id="17407-128">In these steps, we show you how tooturn off data collection if you choose tooopt out.</span></span>

> [!NOTE]
> <span data-ttu-id="17407-129">本文介紹 hello 服務使用的範例部署。</span><span class="sxs-lookup"><span data-stu-id="17407-129">This article introduces hello service by using an example deployment.</span></span> <span data-ttu-id="17407-130">此文章不是逐步指南。</span><span class="sxs-lookup"><span data-stu-id="17407-130">This article is not a step-by-step guide.</span></span>
>
>

## <a name="access-security-center"></a><span data-ttu-id="17407-131">存取資訊安全中心</span><span class="sxs-lookup"><span data-stu-id="17407-131">Access Security Center</span></span>
<span data-ttu-id="17407-132">在 hello 入口網站，請遵循這些步驟 tooaccess 資訊安全中心：</span><span class="sxs-lookup"><span data-stu-id="17407-132">In hello portal, follow these steps tooaccess Security Center:</span></span>

1. <span data-ttu-id="17407-133">在 hello **Microsoft Azure**功能表上，選取**資訊安全中心**。</span><span class="sxs-lookup"><span data-stu-id="17407-133">On hello **Microsoft Azure** menu, select **Security Center**.</span></span>

   ![Azure 功能表][1]
2. <span data-ttu-id="17407-135">如果您要存取的資訊安全中心 hello 第一次，hello ** 褖畫惎**刀鋒視窗隨即開啟。</span><span class="sxs-lookup"><span data-stu-id="17407-135">If you are accessing Security Center for hello first time, hello **Welcome** blade opens.</span></span> <span data-ttu-id="17407-136">選取**啟動資訊安全中心**tooopen hello**資訊安全中心**刀鋒視窗，然後 tooenable 資料收集。</span><span class="sxs-lookup"><span data-stu-id="17407-136">Select **Launch Security Center** tooopen hello **Security Center** blade and tooenable data collection.</span></span>
   <span data-ttu-id="17407-137">![歡迎使用畫面][10]</span><span class="sxs-lookup"><span data-stu-id="17407-137">![Welcome screen][10]</span></span>
3. <span data-ttu-id="17407-138">啟動資訊安全中心的 hello  褖畫惎] 刀鋒視窗，或從 hello Microsoft Azure 功能表選取 [資訊安全中心之後，hello**資訊安全中心**刀鋒視窗隨即開啟。</span><span class="sxs-lookup"><span data-stu-id="17407-138">After you launch Security Center from hello Welcome blade or select Security Center from hello Microsoft Azure menu, hello **Security Center** blade opens.</span></span> <span data-ttu-id="17407-139">針對輕鬆存取 toohello**資訊安全中心**刀鋒視窗中 hello 未來，選取 hello **Pin 刀鋒視窗 toodashboard**選項 （右上方）。</span><span class="sxs-lookup"><span data-stu-id="17407-139">For easy access toohello **Security Center** blade in hello future, select hello **Pin blade toodashboard** option (upper right).</span></span>
   <span data-ttu-id="17407-140">![Pin 刀鋒視窗 toodashboard 選項][2]</span><span class="sxs-lookup"><span data-stu-id="17407-140">![Pin blade toodashboard option][2]</span></span>

## <a name="use-security-center"></a><span data-ttu-id="17407-141">使用資訊安全中心</span><span class="sxs-lookup"><span data-stu-id="17407-141">Use Security Center</span></span>
<span data-ttu-id="17407-142">您可以設定 Azure 訂用帳戶和資源群組的安全性原則。</span><span class="sxs-lookup"><span data-stu-id="17407-142">You can configure security policies for your Azure subscriptions and resource groups.</span></span> <span data-ttu-id="17407-143">一同設定您訂用帳戶的安全性原則：</span><span class="sxs-lookup"><span data-stu-id="17407-143">Let's configure a security policy for your subscription:</span></span>

1. <span data-ttu-id="17407-144">在 hello**資訊安全中心**刀鋒視窗中，選取 hello**原則**磚。</span><span class="sxs-lookup"><span data-stu-id="17407-144">On hello **Security Center** blade, select hello **Policy** tile.</span></span>
2. <span data-ttu-id="17407-145">在 hello**安全性原則-定義每個訂閱的原則**刀鋒視窗中，選取的訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="17407-145">On hello **Security policy - Define policy per subscription** blade, select a subscription.</span></span>
3. <span data-ttu-id="17407-146">在 hello**安全性原則**刀鋒視窗中，**資料收集**是啟用的 tooautomatically 收集記錄檔。</span><span class="sxs-lookup"><span data-stu-id="17407-146">On hello **Security policy** blade, **Data collection** is enabled tooautomatically collect logs.</span></span> <span data-ttu-id="17407-147">hello 監視功能延伸模組的 hello 訂用帳戶中的所有目前和新 Vm 上佈建。</span><span class="sxs-lookup"><span data-stu-id="17407-147">hello monitoring extension is provisioned on all current and new VMs in hello subscription.</span></span> <span data-ttu-id="17407-148">(在 hello 免費層上的資訊安全中心，您可以退出資料收集設定**資料收集**太**關閉**。</span><span class="sxs-lookup"><span data-stu-id="17407-148">(On hello Free tier of Security Center, you can opt out of data collection by setting **Data collection** too**Off**.</span></span> <span data-ttu-id="17407-149">設定**資料收集**太**關閉**防止資訊安全中心提供安全性警示和建議。)</span><span class="sxs-lookup"><span data-stu-id="17407-149">Setting **Data Collection** too**Off** prevents Security Center from giving you security alerts and recommendations.)</span></span>
4. <span data-ttu-id="17407-150">在 hello**安全性原則**刀鋒視窗中，選取**防止原則**。</span><span class="sxs-lookup"><span data-stu-id="17407-150">On hello **Security policy** blade, select **Prevention policy**.</span></span> <span data-ttu-id="17407-151">這會開啟 hello**防止原則**刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="17407-151">This opens hello **Prevention policy** blade.</span></span>
5. <span data-ttu-id="17407-152">在 hello**防止原則**刀鋒視窗中，開啟 hello 建議的 toosee 做為您的安全性原則的一部分。</span><span class="sxs-lookup"><span data-stu-id="17407-152">On hello **Prevention policy** blade, turn on hello recommendations that you want toosee as part of your security policy.</span></span> <span data-ttu-id="17407-153">範例：</span><span class="sxs-lookup"><span data-stu-id="17407-153">Examples:</span></span>

   * <span data-ttu-id="17407-154">設定**系統更新**太**上**掃描所有遺漏的 OS 更新支援的 Vm。</span><span class="sxs-lookup"><span data-stu-id="17407-154">Setting **System updates** too**On** scans all supported VMs for missing OS updates.</span></span>
   * <span data-ttu-id="17407-155">設定**作業系統弱點**太**上**掃描所有支援的 Vm tooidentify 可能會使任何 OS 設定 hello VM 更容易遭受 tooattack。</span><span class="sxs-lookup"><span data-stu-id="17407-155">Setting **OS vulnerabilities** too**On** scans all supported VMs tooidentify any OS configurations that might make hello VM more vulnerable tooattack.</span></span>

### <a name="view-recommendations"></a><span data-ttu-id="17407-156">檢視建議</span><span class="sxs-lookup"><span data-stu-id="17407-156">View recommendations</span></span>
1. <span data-ttu-id="17407-157">傳回 toohello**資訊安全中心**刀鋒視窗，然後選取 hello**建議**磚。</span><span class="sxs-lookup"><span data-stu-id="17407-157">Return toohello **Security Center** blade and select hello **Recommendations** tile.</span></span> <span data-ttu-id="17407-158">資訊安全中心定期分析您的 Azure 資源 hello 安全性狀態。</span><span class="sxs-lookup"><span data-stu-id="17407-158">Security Center periodically analyzes hello security state of your Azure resources.</span></span> <span data-ttu-id="17407-159">當資訊安全中心識別潛在的安全性漏洞時，它會顯示建議的 hello**建議**刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="17407-159">When Security Center identifies potential security vulnerabilities, it shows recommendations on hello **Recommendations** blade.</span></span>
   <span data-ttu-id="17407-160">![Azure 資訊安全中心的建議][5]</span><span class="sxs-lookup"><span data-stu-id="17407-160">![Recommendations in Azure Security Center][5]</span></span>
2. <span data-ttu-id="17407-161">選取在 hello 建議**建議**刀鋒視窗 tooview 詳細的資訊和/或 tootake 動作 tooresolve hello 發出。</span><span class="sxs-lookup"><span data-stu-id="17407-161">Select a recommendation on hello **Recommendations** blade tooview more information and/or tootake action tooresolve hello issue.</span></span>

### <a name="view-hello-security-state-of-your-resources"></a><span data-ttu-id="17407-162">檢視您資源的 hello 安全性狀態</span><span class="sxs-lookup"><span data-stu-id="17407-162">View hello security state of your resources</span></span>
1. <span data-ttu-id="17407-163">傳回 toohello**資訊安全中心**刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="17407-163">Return toohello **Security Center** blade.</span></span> <span data-ttu-id="17407-164">hello**防止**hello 儀表板 區段包含 hello 安全性狀態的指標，這對於資料和應用程式網路的 Vm。</span><span class="sxs-lookup"><span data-stu-id="17407-164">hello **Prevention** section of hello dashboard contains indicators of hello security state for VMs, networking, data, and applications.</span></span>
2. <span data-ttu-id="17407-165">選取**計算**tooview 的詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="17407-165">Select **Compute** tooview more information.</span></span> <span data-ttu-id="17407-166">hello**計算**刀鋒視窗會開啟顯示三個索引標籤：</span><span class="sxs-lookup"><span data-stu-id="17407-166">hello **Compute** blade opens showing three tabs:</span></span>

  - <span data-ttu-id="17407-167">**概觀** - 包含監視和 VM 的建議。</span><span class="sxs-lookup"><span data-stu-id="17407-167">**Overview** - Contains monitoring and VM recommendations.</span></span>
  - <span data-ttu-id="17407-168">**虛擬機器** - 列出所有 VM 及其目前的安全性狀態。</span><span class="sxs-lookup"><span data-stu-id="17407-168">**Virtual machines** - Lists all VMs and current security states.</span></span>
  - <span data-ttu-id="17407-169">**雲端服務** - 列出資訊安全中心監視的 Web 和背景工作角色清單。</span><span class="sxs-lookup"><span data-stu-id="17407-169">**Cloud services** - Lists web and worker roles monitored by Security Center.</span></span>

    ![Azure 資訊安全中心中的 hello 資源健全狀況圖格][6]

3. <span data-ttu-id="17407-171">在 hello**概觀**索引標籤上，選取下方的建議**虛擬機器建議**tooview 詳細資訊和/或採取動作 tooconfigure 必要的控制項。</span><span class="sxs-lookup"><span data-stu-id="17407-171">On hello **Overview** tab, select a recommendation under **VIRTUAL MACHINES RECOMMENDATIONS** tooview more information and/or take action tooconfigure necessary controls.</span></span>
4. <span data-ttu-id="17407-172">在 hello**虛擬機器**索引標籤上，選取 VM tooview 其他詳細資料。</span><span class="sxs-lookup"><span data-stu-id="17407-172">On hello **Virtual machines** tab, select a VM tooview additional details.</span></span>

### <a name="view-security-alerts"></a><span data-ttu-id="17407-173">檢視安全性警示</span><span class="sxs-lookup"><span data-stu-id="17407-173">View security alerts</span></span>
1. <span data-ttu-id="17407-174">傳回 toohello**資訊安全中心**刀鋒視窗，然後選取 hello**安全性警示**磚。</span><span class="sxs-lookup"><span data-stu-id="17407-174">Return toohello **Security Center** blade and select hello **Security alerts** tile.</span></span> <span data-ttu-id="17407-175">hello**安全性警示**刀鋒視窗會開啟並顯示警示的清單。</span><span class="sxs-lookup"><span data-stu-id="17407-175">hello **Security alerts** blade opens and displays a list of alerts.</span></span> <span data-ttu-id="17407-176">hello 資訊安全中心分析您的安全性記錄檔和網路活動會產生這些警示。</span><span class="sxs-lookup"><span data-stu-id="17407-176">hello Security Center analysis of your security logs and network activity generates these alerts.</span></span> <span data-ttu-id="17407-177">包含來自整合式合作夥伴解決方案的警示。</span><span class="sxs-lookup"><span data-stu-id="17407-177">Alerts from integrated partner solutions are included.</span></span>
   <span data-ttu-id="17407-178">![Azure 資訊安全中心的安全性警示][7]</span><span class="sxs-lookup"><span data-stu-id="17407-178">![Security alerts in Azure Security Center][7]</span></span>

   > [!NOTE]
   > <span data-ttu-id="17407-179">安全性警示才可使用的資訊安全中心 hello 標準層啟用。</span><span class="sxs-lookup"><span data-stu-id="17407-179">Security alerts are only available if hello Standard tier of Security Center is enabled.</span></span> <span data-ttu-id="17407-180">使用 60 天免費試用版的 hello Standard 價格區間。</span><span class="sxs-lookup"><span data-stu-id="17407-180">A 60 day free trial of hello Standard tier is available.</span></span> <span data-ttu-id="17407-181">請參閱[後續步驟](#next-steps)如需如何 tooget hello 標準層。</span><span class="sxs-lookup"><span data-stu-id="17407-181">See [Next steps](#next-steps) for information on how tooget hello Standard tier.</span></span>
   >
   >
2. <span data-ttu-id="17407-182">選取警示 tooview 其他資訊。</span><span class="sxs-lookup"><span data-stu-id="17407-182">Select an alert tooview additional information.</span></span> <span data-ttu-id="17407-183">在此範例中，請選取 [探索到修改過的系統二進位檔]。</span><span class="sxs-lookup"><span data-stu-id="17407-183">In this example, let's select **Modified system binary discovered**.</span></span> <span data-ttu-id="17407-184">這會開啟刀鋒視窗，提供有關 hello 警示的其他詳細資料。</span><span class="sxs-lookup"><span data-stu-id="17407-184">This opens blades that provide additional details about hello alert.</span></span>
   <span data-ttu-id="17407-185">![Azure 資訊安全中心的安全性警示詳細資料][8]</span><span class="sxs-lookup"><span data-stu-id="17407-185">![Security alert details in Azure Security Center][8]</span></span>

### <a name="view-hello-health-of-your-partner-solutions"></a><span data-ttu-id="17407-186">檢視 hello 健康情況的協力廠商解決方案</span><span class="sxs-lookup"><span data-stu-id="17407-186">View hello health of your partner solutions</span></span>
1. <span data-ttu-id="17407-187">傳回 toohello**資訊安全中心**刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="17407-187">Return toohello **Security Center** blade.</span></span> <span data-ttu-id="17407-188">hello**合作夥伴解決方案**磚可讓您監視您一眼 hello 與您 Azure 訂用帳戶整合協力廠商方案的健全狀況狀態。</span><span class="sxs-lookup"><span data-stu-id="17407-188">hello **Partner solutions** tile lets you monitor, at a glance, hello health status of your partner solutions integrated with your Azure subscription.</span></span>
2. <span data-ttu-id="17407-189">選取 hello**合作夥伴解決方案**磚。</span><span class="sxs-lookup"><span data-stu-id="17407-189">Select hello **Partner solutions** tile.</span></span> <span data-ttu-id="17407-190">刀鋒視窗會開啟，並顯示的協力廠商解決方案清單連接 tooSecurity 中心。</span><span class="sxs-lookup"><span data-stu-id="17407-190">A blade opens and displays a list of your partner solutions connected tooSecurity Center.</span></span>
   <span data-ttu-id="17407-191">![][9]</span><span class="sxs-lookup"><span data-stu-id="17407-191">![Partner solutions][9]</span></span>
3. <span data-ttu-id="17407-192">選取合作夥伴解決方案。</span><span class="sxs-lookup"><span data-stu-id="17407-192">Select a partner solution.</span></span> <span data-ttu-id="17407-193">在此範例中，我們選取 hello **QualysVa1**方案。</span><span class="sxs-lookup"><span data-stu-id="17407-193">In this example, let's select hello **QualysVa1** solution.</span></span>  <span data-ttu-id="17407-194">刀鋒視窗會開啟並顯示 hello 夥伴方案和 hello 方案 hello 狀態相關聯的資源。</span><span class="sxs-lookup"><span data-stu-id="17407-194">A blade opens and shows you hello status of hello partner solution and hello solution's associated resources.</span></span> <span data-ttu-id="17407-195">選取**方案主控台**tooopen hello 夥伴管理體驗此解決方案。</span><span class="sxs-lookup"><span data-stu-id="17407-195">Select **Solution console** tooopen hello partner management experience for this solution.</span></span>

## <a name="next-steps"></a><span data-ttu-id="17407-196">後續步驟</span><span class="sxs-lookup"><span data-stu-id="17407-196">Next steps</span></span>
<span data-ttu-id="17407-197">這篇文章會引進 toohello 安全性監視和原則管理元件的資訊安全中心。</span><span class="sxs-lookup"><span data-stu-id="17407-197">This article introduced you toohello security monitoring and policy management components of Security Center.</span></span> <span data-ttu-id="17407-198">既然您已熟悉的資訊安全中心，請嘗試下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="17407-198">Now that you're familiar with Security Center, try hello following steps:</span></span>

* <span data-ttu-id="17407-199">為您的 Azure 訂用帳戶設定安全性原則。</span><span class="sxs-lookup"><span data-stu-id="17407-199">Configure a security policy for your Azure subscription.</span></span> <span data-ttu-id="17407-200">詳細資訊，請參閱 toolearn [Azure 資訊安全中心中設定安全性原則](security-center-policies.md)。</span><span class="sxs-lookup"><span data-stu-id="17407-200">toolearn more, see [Setting security policies in Azure Security Center](security-center-policies.md).</span></span>
* <span data-ttu-id="17407-201">您可以使用 hello 建議的資訊安全中心 toohelp 保護您的 Azure 資源。</span><span class="sxs-lookup"><span data-stu-id="17407-201">Use hello recommendations in Security Center toohelp you protect your Azure resources.</span></span> <span data-ttu-id="17407-202">詳細資訊，請參閱 toolearn[管理 Azure 資訊安全中心中的安全性建議](security-center-recommendations.md)。</span><span class="sxs-lookup"><span data-stu-id="17407-202">toolearn more, see [Managing security recommendations in Azure Security Center](security-center-recommendations.md).</span></span>
* <span data-ttu-id="17407-203">檢閱並管理目前的安全性警示。</span><span class="sxs-lookup"><span data-stu-id="17407-203">Review and manage your current security alerts.</span></span> <span data-ttu-id="17407-204">詳細資訊，請參閱 toolearn[中 Azure 資訊安全中心警示管理，而且有回應 toosecurity](security-center-managing-and-responding-alerts.md)。</span><span class="sxs-lookup"><span data-stu-id="17407-204">toolearn more, see [Managing and responding toosecurity alerts in Azure Security Center](security-center-managing-and-responding-alerts.md).</span></span>
- <span data-ttu-id="17407-205">[Azure 資訊安全中心資料安全性](security-center-data-security.md) - 了解資訊安全中心如何管理及保護其中的資料。</span><span class="sxs-lookup"><span data-stu-id="17407-205">[Azure Security Center data security](security-center-data-security.md) - Learn how data is managed and safeguarded in Security Center.</span></span>
* <span data-ttu-id="17407-206">深入了解 hello[進階威脅偵測功能](security-center-detection-capabilities.md)隨附的 hello[標準層](security-center-pricing.md)的資訊安全中心。</span><span class="sxs-lookup"><span data-stu-id="17407-206">Learn more about hello [advanced threat detection features](security-center-detection-capabilities.md) that come with hello [Standard tier](security-center-pricing.md) of Security Center.</span></span> <span data-ttu-id="17407-207">hello 標準層是免費提供 hello 前 60 天。</span><span class="sxs-lookup"><span data-stu-id="17407-207">hello Standard tier is offered free for hello first 60 days.</span></span>
* <span data-ttu-id="17407-208">如果您有關於使用資訊安全中心的問題，請參閱 hello [Azure 安全性中心常見問題集](security-center-faq.md)。</span><span class="sxs-lookup"><span data-stu-id="17407-208">If you have questions about using Security Center, see hello [Azure Security Center FAQ](security-center-faq.md).</span></span>

<!--Image references-->
[1]: ./media/security-center-get-started/azure-menu.png
[2]: ./media/security-center-get-started/security-center-pin.png
[3]: ./media/security-center-get-started/security-policy.png
[4]: ./media/security-center-get-started/prevention-policy.png
[5]: ./media/security-center-get-started/recommendations.png
[6]: ./media/security-center-get-started/resources-health.png
[7]: ./media/security-center-get-started/security-alert.png
[8]: ./media/security-center-get-started/security-alert-detail.png
[9]: ./media/security-center-get-started/partner-solutions.png
[10]: ./media/security-center-get-started/welcome.png
