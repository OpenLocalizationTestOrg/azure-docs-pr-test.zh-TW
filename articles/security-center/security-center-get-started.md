---
title: "Azure 資訊安全中心快速入門指南 | Microsoft Docs"
description: "此文章帶領您認識安全性監視和原則管理元件，並連結至下一個步驟，協助您快速開始使用 Azure 資訊安全中心。"
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
ms.openlocfilehash: 392c814b7d3ff6b4f0f7850a51960576775e0307
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="azure-security-center-quick-start-guide"></a><span data-ttu-id="c135e-103">Azure 資訊安全中心快速入門指南</span><span class="sxs-lookup"><span data-stu-id="c135e-103">Azure Security Center quick start guide</span></span>
<span data-ttu-id="c135e-104">此文章帶領您認識資訊安全中心的安全性監視和原則管理元件，協助您快速開始使用 Azure 資訊安全中心。</span><span class="sxs-lookup"><span data-stu-id="c135e-104">This article helps you quickly get started with Azure Security Center by guiding you through the security monitoring and policy management components of Security Center.</span></span>

> [!NOTE]
> <span data-ttu-id="c135e-105">從 2017 年 6 月初開始，資訊安全中心會使用 Microsoft Monitoring Agent 來收集和儲存資料。</span><span class="sxs-lookup"><span data-stu-id="c135e-105">Beginning in early June 2017, Security Center will use the Microsoft Monitoring Agent to collect and store data.</span></span> <span data-ttu-id="c135e-106">若要深入了解，請參閱 [Azure 資訊安全中心平台移轉](security-center-platform-migration.md)。</span><span class="sxs-lookup"><span data-stu-id="c135e-106">See [Azure Security Center Platform Migration](security-center-platform-migration.md) to learn more.</span></span> <span data-ttu-id="c135e-107">本文中的資訊說明轉換至 Microsoft Monitoring Agent 後的資訊安全中心功能。</span><span class="sxs-lookup"><span data-stu-id="c135e-107">The information in this article represents Security Center functionality after transition to the Microsoft Monitoring Agent.</span></span>
>
>

## <a name="prerequisites"></a><span data-ttu-id="c135e-108">必要條件</span><span class="sxs-lookup"><span data-stu-id="c135e-108">Prerequisites</span></span>
<span data-ttu-id="c135e-109">若要開始使用資訊安全中心，您必須有 Microsoft Azure 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="c135e-109">To get started with Security Center, you must have a subscription to Microsoft Azure.</span></span> <span data-ttu-id="c135e-110">如果您沒有訂用帳戶，可以註冊[免費帳戶](https://azure.microsoft.com/pricing/free-trial/)。</span><span class="sxs-lookup"><span data-stu-id="c135e-110">If you do not have a subscription, you can sign up for a [free account](https://azure.microsoft.com/pricing/free-trial/).</span></span>

<span data-ttu-id="c135e-111">資訊安全中心的免費層會在您訂用帳戶自動啟用，並提供 Azure 資源安全性狀態的可見度。</span><span class="sxs-lookup"><span data-stu-id="c135e-111">The Free tier of Security Center is automatically enabled with your subscription and provides visibility into the security state of your Azure resources.</span></span> <span data-ttu-id="c135e-112">它提供基本的安全性原則管理、安全性建議並整合 Azure 合作夥伴的安全性產品和服務。</span><span class="sxs-lookup"><span data-stu-id="c135e-112">It provides basic security policy management, security recommendations, and integration with security products and services from Azure partners.</span></span>

<span data-ttu-id="c135e-113">您可以從 [Azure 入口網站](https://azure.microsoft.com/features/azure-portal/)存取資訊安全中心。</span><span class="sxs-lookup"><span data-stu-id="c135e-113">You access Security Center from the [Azure portal](https://azure.microsoft.com/features/azure-portal/).</span></span> <span data-ttu-id="c135e-114">若要深入了解 Azure 入口網站，請參閱[入口網站文件](https://azure.microsoft.com/documentation/services/azure-portal/)。</span><span class="sxs-lookup"><span data-stu-id="c135e-114">To learn more about the Azure portal, see the [portal documentation](https://azure.microsoft.com/documentation/services/azure-portal/).</span></span>

## <a name="permissions"></a><span data-ttu-id="c135e-115">權限</span><span class="sxs-lookup"><span data-stu-id="c135e-115">Permissions</span></span>
<span data-ttu-id="c135e-116">在「資訊安全中心」中，當您獲指派為資源所屬的訂用帳戶或資源群組「擁有者」、「參與者」或「讀取者」角色時，您只會看到與 Azure 資源相關的項目。</span><span class="sxs-lookup"><span data-stu-id="c135e-116">In Security Center, you only see information related to an Azure resource when you are assigned the role of Owner, Contributor, or Reader for the subscription or resource group that a resource belongs to.</span></span> <span data-ttu-id="c135e-117">請參閱 [Azure 資訊安全中心的權限](security-center-permissions.md)以深入了解角色與資訊安全中心允許的動作。</span><span class="sxs-lookup"><span data-stu-id="c135e-117">See [Permissions in Azure Security Center](security-center-permissions.md) to learn more about roles and allowed actions in Security Center.</span></span>

## <a name="data-collection"></a><span data-ttu-id="c135e-118">資料收集</span><span class="sxs-lookup"><span data-stu-id="c135e-118">Data collection</span></span>
<span data-ttu-id="c135e-119">資訊安全中心會收集虛擬機器 (VM) 的資料，以便評估其安全性狀態、提供安全性建議，並對您發出威脅警示。</span><span class="sxs-lookup"><span data-stu-id="c135e-119">Security Center collects data from your virtual machines (VMs) to assess their security state, provide security recommendations, and alert you to threats.</span></span> <span data-ttu-id="c135e-120">當您第一次存取資訊安全中心時，訂用帳戶中的所有 VM 都會啟用資料收集。</span><span class="sxs-lookup"><span data-stu-id="c135e-120">When you first access Security Center, data collection is enabled on all VMs in your subscription.</span></span> <span data-ttu-id="c135e-121">資訊安全中心會在所有現有支援的 Azure 虛擬機器和任何新建立的 VM 上佈建 Microsoft Monitoring Agent。</span><span class="sxs-lookup"><span data-stu-id="c135e-121">Security Center provisions the Microsoft Monitoring Agent on all existing supported Azure VMs and any new ones that are created.</span></span> <span data-ttu-id="c135e-122">若要深入了解資料收集的運作方式，請參閱[啟用資料收集](security-center-enable-data-collection.md)。</span><span class="sxs-lookup"><span data-stu-id="c135e-122">See [Enable data collection](security-center-enable-data-collection.md) to learn more about how data collection works.</span></span>

<span data-ttu-id="c135e-123">建議您啟用資料收集。</span><span class="sxs-lookup"><span data-stu-id="c135e-123">Data collection is recommended.</span></span> <span data-ttu-id="c135e-124">如果您是使用免費層的資訊安全中心，可以在安全性原則中關閉資料收集，以停用 VM 的資料收集。</span><span class="sxs-lookup"><span data-stu-id="c135e-124">If you are using the Free tier of Security Center, you can disable data collection from VMs by turning off data collection in the security policy.</span></span> <span data-ttu-id="c135e-125">資訊安全中心標準層上的訂用帳戶需要資料收集。</span><span class="sxs-lookup"><span data-stu-id="c135e-125">Data collection is required for subscriptions on the Standard tier of Security Center.</span></span> <span data-ttu-id="c135e-126">如需免費和標準定價層的詳細資訊，請參閱[資訊安全中心定價](security-center-pricing.md)。</span><span class="sxs-lookup"><span data-stu-id="c135e-126">See [Security Center pricing](security-center-pricing.md) to learn more about the Free and Standard pricing tiers.</span></span>

<span data-ttu-id="c135e-127">下列步驟說明如何存取和使用安全中心的元件。</span><span class="sxs-lookup"><span data-stu-id="c135e-127">The following steps describe how to access and use the components of Security Center.</span></span> <span data-ttu-id="c135e-128">這些步驟會說明選擇退出時如何關閉資料收集。</span><span class="sxs-lookup"><span data-stu-id="c135e-128">In these steps, we show you how to turn off data collection if you choose to opt out.</span></span>

> [!NOTE]
> <span data-ttu-id="c135e-129">此文章將使用範例部署來介紹服務。</span><span class="sxs-lookup"><span data-stu-id="c135e-129">This article introduces the service by using an example deployment.</span></span> <span data-ttu-id="c135e-130">此文章不是逐步指南。</span><span class="sxs-lookup"><span data-stu-id="c135e-130">This article is not a step-by-step guide.</span></span>
>
>

## <a name="access-security-center"></a><span data-ttu-id="c135e-131">存取資訊安全中心</span><span class="sxs-lookup"><span data-stu-id="c135e-131">Access Security Center</span></span>
<span data-ttu-id="c135e-132">在入口網站中，執行下列步驟來存取資訊安全中心：</span><span class="sxs-lookup"><span data-stu-id="c135e-132">In the portal, follow these steps to access Security Center:</span></span>

1. <span data-ttu-id="c135e-133">在 [Microsoft Azure] 功能表中，選取 [資訊安全中心]。</span><span class="sxs-lookup"><span data-stu-id="c135e-133">On the **Microsoft Azure** menu, select **Security Center**.</span></span>

   ![Azure 功能表][1]
2. <span data-ttu-id="c135e-135">如果您是第一次存取資訊安全中心，[歡迎] 刀鋒視窗隨即開啟。</span><span class="sxs-lookup"><span data-stu-id="c135e-135">If you are accessing Security Center for the first time, the **Welcome** blade opens.</span></span> <span data-ttu-id="c135e-136">選取 [啟動資訊安全中心]，開啟 [資訊安全中心]刀鋒視窗並啟用資料收集。</span><span class="sxs-lookup"><span data-stu-id="c135e-136">Select **Launch Security Center** to open the **Security Center** blade and to enable data collection.</span></span>
   <span data-ttu-id="c135e-137">![歡迎使用畫面][10]</span><span class="sxs-lookup"><span data-stu-id="c135e-137">![Welcome screen][10]</span></span>
3. <span data-ttu-id="c135e-138">從 [歡迎使用] 刀鋒視窗啟動資訊安全中心，或從 [Microsoft Azure] 功能表中選取 [資訊安全中心] 之後，[資訊安全中心] 刀鋒視窗隨即開啟。</span><span class="sxs-lookup"><span data-stu-id="c135e-138">After you launch Security Center from the Welcome blade or select Security Center from the Microsoft Azure menu, the **Security Center** blade opens.</span></span> <span data-ttu-id="c135e-139">為方便日後快速存取 [資訊安全中心] 刀鋒視窗，請選取 [將刀鋒視窗釘選到儀表板] 選項 (右上方)。</span><span class="sxs-lookup"><span data-stu-id="c135e-139">For easy access to the **Security Center** blade in the future, select the **Pin blade to dashboard** option (upper right).</span></span>
   <span data-ttu-id="c135e-140">![將刀鋒視窗釘選到儀表板選項][2]</span><span class="sxs-lookup"><span data-stu-id="c135e-140">![Pin blade to dashboard option][2]</span></span>

## <a name="use-security-center"></a><span data-ttu-id="c135e-141">使用資訊安全中心</span><span class="sxs-lookup"><span data-stu-id="c135e-141">Use Security Center</span></span>
<span data-ttu-id="c135e-142">您可以設定 Azure 訂用帳戶和資源群組的安全性原則。</span><span class="sxs-lookup"><span data-stu-id="c135e-142">You can configure security policies for your Azure subscriptions and resource groups.</span></span> <span data-ttu-id="c135e-143">一同設定您訂用帳戶的安全性原則：</span><span class="sxs-lookup"><span data-stu-id="c135e-143">Let's configure a security policy for your subscription:</span></span>

1. <span data-ttu-id="c135e-144">選取 [資訊安全中心] 刀鋒視窗上的 [原則] 圖格。</span><span class="sxs-lookup"><span data-stu-id="c135e-144">On the **Security Center** blade, select the **Policy** tile.</span></span>
2. <span data-ttu-id="c135e-145">在 [安全性原則 - 定義每個訂用帳戶的原則] 刀鋒視窗上，選取訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="c135e-145">On the **Security policy - Define policy per subscription** blade, select a subscription.</span></span>
3. <span data-ttu-id="c135e-146">在 [安全性原則] 刀鋒視窗上，[資料收集] 已啟用以自動收集記錄檔。</span><span class="sxs-lookup"><span data-stu-id="c135e-146">On the **Security policy** blade, **Data collection** is enabled to automatically collect logs.</span></span> <span data-ttu-id="c135e-147">監視擴充功能會佈建在訂用帳戶的所有目前 VM 和新 VM 上。</span><span class="sxs-lookup"><span data-stu-id="c135e-147">The monitoring extension is provisioned on all current and new VMs in the subscription.</span></span> <span data-ttu-id="c135e-148">(在資訊安全中心的免費層上，您可以將 [資料收集] 設定為 [關閉]，以退出資料收集。</span><span class="sxs-lookup"><span data-stu-id="c135e-148">(On the Free tier of Security Center, you can opt out of data collection by setting **Data collection** to **Off**.</span></span> <span data-ttu-id="c135e-149">將 [資料收集] 設定為 [關閉] 會讓資訊安全中心無法為您提供安全性警示與建議。)</span><span class="sxs-lookup"><span data-stu-id="c135e-149">Setting **Data Collection** to **Off** prevents Security Center from giving you security alerts and recommendations.)</span></span>
4. <span data-ttu-id="c135e-150">選取 [安全性原則] 刀鋒視窗上的 [預防原則]。</span><span class="sxs-lookup"><span data-stu-id="c135e-150">On the **Security policy** blade, select **Prevention policy**.</span></span> <span data-ttu-id="c135e-151">這會開啟 [預防原則] 刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="c135e-151">This opens the **Prevention policy** blade.</span></span>
5. <span data-ttu-id="c135e-152">在 [預防原則] 刀鋒視窗上，開啟您想要作為安全性原則一部分的建議。</span><span class="sxs-lookup"><span data-stu-id="c135e-152">On the **Prevention policy** blade, turn on the recommendations that you want to see as part of your security policy.</span></span> <span data-ttu-id="c135e-153">範例：</span><span class="sxs-lookup"><span data-stu-id="c135e-153">Examples:</span></span>

   * <span data-ttu-id="c135e-154">將 [系統更新] 設定為 [開啟] 會掃描所有支援的 VM，尋找遺漏的 OS 更新。</span><span class="sxs-lookup"><span data-stu-id="c135e-154">Setting **System updates** to **On** scans all supported VMs for missing OS updates.</span></span>
   * <span data-ttu-id="c135e-155">將 [OS 弱點] 設定為 [開啟] 會掃描所有支援的 VM，以識別任何可能讓 VM 更容易受到攻擊的 OS 設定。</span><span class="sxs-lookup"><span data-stu-id="c135e-155">Setting **OS vulnerabilities** to **On** scans all supported VMs to identify any OS configurations that might make the VM more vulnerable to attack.</span></span>

### <a name="view-recommendations"></a><span data-ttu-id="c135e-156">檢視建議</span><span class="sxs-lookup"><span data-stu-id="c135e-156">View recommendations</span></span>
1. <span data-ttu-id="c135e-157">返回 [資訊安全中心] 刀鋒視窗，然後選取 [建議] 圖格。</span><span class="sxs-lookup"><span data-stu-id="c135e-157">Return to the **Security Center** blade and select the **Recommendations** tile.</span></span> <span data-ttu-id="c135e-158">資訊安全中心會定期分析 Azure 資源的安全性狀態。</span><span class="sxs-lookup"><span data-stu-id="c135e-158">Security Center periodically analyzes the security state of your Azure resources.</span></span> <span data-ttu-id="c135e-159">當資訊安全中心識別潛在的安全性弱點時，它會在 [建議] 刀鋒視窗上顯示建議。</span><span class="sxs-lookup"><span data-stu-id="c135e-159">When Security Center identifies potential security vulnerabilities, it shows recommendations on the **Recommendations** blade.</span></span>
   <span data-ttu-id="c135e-160">![Azure 資訊安全中心的建議][5]</span><span class="sxs-lookup"><span data-stu-id="c135e-160">![Recommendations in Azure Security Center][5]</span></span>
2. <span data-ttu-id="c135e-161">選取 [建議] 刀鋒視窗上的建議，檢視詳細資訊及/或採取行動以解決問題。</span><span class="sxs-lookup"><span data-stu-id="c135e-161">Select a recommendation on the **Recommendations** blade to view more information and/or to take action to resolve the issue.</span></span>

### <a name="view-the-security-state-of-your-resources"></a><span data-ttu-id="c135e-162">檢視資源的健康狀態</span><span class="sxs-lookup"><span data-stu-id="c135e-162">View the security state of your resources</span></span>
1. <span data-ttu-id="c135e-163">返回 [資訊安全中心] 刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="c135e-163">Return to the **Security Center** blade.</span></span> <span data-ttu-id="c135e-164">儀表板的 [防護] 區段包含 VM、網路、資料和應用程式的安全性狀態指標。</span><span class="sxs-lookup"><span data-stu-id="c135e-164">The **Prevention** section of the dashboard contains indicators of the security state for VMs, networking, data, and applications.</span></span>
2. <span data-ttu-id="c135e-165">選取 [計算] 以檢視更多資訊。</span><span class="sxs-lookup"><span data-stu-id="c135e-165">Select **Compute** to view more information.</span></span> <span data-ttu-id="c135e-166">[計算] 刀鋒視窗隨即開啟，並顯示三個索引標籤：</span><span class="sxs-lookup"><span data-stu-id="c135e-166">The **Compute** blade opens showing three tabs:</span></span>

  - <span data-ttu-id="c135e-167">**概觀** - 包含監視和 VM 的建議。</span><span class="sxs-lookup"><span data-stu-id="c135e-167">**Overview** - Contains monitoring and VM recommendations.</span></span>
  - <span data-ttu-id="c135e-168">**虛擬機器** - 列出所有 VM 及其目前的安全性狀態。</span><span class="sxs-lookup"><span data-stu-id="c135e-168">**Virtual machines** - Lists all VMs and current security states.</span></span>
  - <span data-ttu-id="c135e-169">**雲端服務** - 列出資訊安全中心監視的 Web 和背景工作角色清單。</span><span class="sxs-lookup"><span data-stu-id="c135e-169">**Cloud services** - Lists web and worker roles monitored by Security Center.</span></span>

    ![Azure 資訊安全中心的 [資源健康狀態] 磚][6]

3. <span data-ttu-id="c135e-171">在 [概觀] 索引標籤的 [虛擬機器建議] 下選取建議，以檢視詳細資訊及/或採取行動以設定必要的控制項。</span><span class="sxs-lookup"><span data-stu-id="c135e-171">On the **Overview** tab, select a recommendation under **VIRTUAL MACHINES RECOMMENDATIONS** to view more information and/or take action to configure necessary controls.</span></span>
4. <span data-ttu-id="c135e-172">在 [虛擬機器] 索引標籤中選取 VM，以檢視其他詳細資料。</span><span class="sxs-lookup"><span data-stu-id="c135e-172">On the **Virtual machines** tab, select a VM to view additional details.</span></span>

### <a name="view-security-alerts"></a><span data-ttu-id="c135e-173">檢視安全性警示</span><span class="sxs-lookup"><span data-stu-id="c135e-173">View security alerts</span></span>
1. <span data-ttu-id="c135e-174">返回 [資訊安全中心] 刀鋒視窗，然後選取 [安全性警示] 圖格。</span><span class="sxs-lookup"><span data-stu-id="c135e-174">Return to the **Security Center** blade and select the **Security alerts** tile.</span></span> <span data-ttu-id="c135e-175">[安全性警示] 刀鋒視窗會開啟並顯示警示清單。</span><span class="sxs-lookup"><span data-stu-id="c135e-175">The **Security alerts** blade opens and displays a list of alerts.</span></span> <span data-ttu-id="c135e-176">資訊安全中心透過對安全性記錄檔和網路活動的分析，產生警示。</span><span class="sxs-lookup"><span data-stu-id="c135e-176">The Security Center analysis of your security logs and network activity generates these alerts.</span></span> <span data-ttu-id="c135e-177">包含來自整合式合作夥伴解決方案的警示。</span><span class="sxs-lookup"><span data-stu-id="c135e-177">Alerts from integrated partner solutions are included.</span></span>
   <span data-ttu-id="c135e-178">![Azure 資訊安全中心的安全性警示][7]</span><span class="sxs-lookup"><span data-stu-id="c135e-178">![Security alerts in Azure Security Center][7]</span></span>

   > [!NOTE]
   > <span data-ttu-id="c135e-179">如果已啟用資訊安全中心的標準層，才會出現安全性警示。</span><span class="sxs-lookup"><span data-stu-id="c135e-179">Security alerts are only available if the Standard tier of Security Center is enabled.</span></span> <span data-ttu-id="c135e-180">標準層有 60 天的免費試用可供使用。</span><span class="sxs-lookup"><span data-stu-id="c135e-180">A 60 day free trial of the Standard tier is available.</span></span> <span data-ttu-id="c135e-181">如需有關如何取得標準層級資訊，請參閱[後續步驟](#next-steps)。</span><span class="sxs-lookup"><span data-stu-id="c135e-181">See [Next steps](#next-steps) for information on how to get the Standard tier.</span></span>
   >
   >
2. <span data-ttu-id="c135e-182">選取警示以檢視其他資訊。</span><span class="sxs-lookup"><span data-stu-id="c135e-182">Select an alert to view additional information.</span></span> <span data-ttu-id="c135e-183">在此範例中，請選取 [探索到修改過的系統二進位檔]。</span><span class="sxs-lookup"><span data-stu-id="c135e-183">In this example, let's select **Modified system binary discovered**.</span></span> <span data-ttu-id="c135e-184">這會開啟刀鋒視窗，提供有關警示的其他詳細資料。</span><span class="sxs-lookup"><span data-stu-id="c135e-184">This opens blades that provide additional details about the alert.</span></span>
   <span data-ttu-id="c135e-185">![Azure 資訊安全中心的安全性警示詳細資料][8]</span><span class="sxs-lookup"><span data-stu-id="c135e-185">![Security alert details in Azure Security Center][8]</span></span>

### <a name="view-the-health-of-your-partner-solutions"></a><span data-ttu-id="c135e-186">檢視合作夥伴解決方案的健全狀況</span><span class="sxs-lookup"><span data-stu-id="c135e-186">View the health of your partner solutions</span></span>
1. <span data-ttu-id="c135e-187">返回 [資訊安全中心]  刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="c135e-187">Return to the **Security Center** blade.</span></span> <span data-ttu-id="c135e-188">[合作夥伴解決方案] 圖格可讓您監視與您的 Azure 訂用帳戶整合之合作夥伴解決方案的健康狀態，一目了然。</span><span class="sxs-lookup"><span data-stu-id="c135e-188">The **Partner solutions** tile lets you monitor, at a glance, the health status of your partner solutions integrated with your Azure subscription.</span></span>
2. <span data-ttu-id="c135e-189">選取 [合作夥伴解決方案]  圖格。</span><span class="sxs-lookup"><span data-stu-id="c135e-189">Select the **Partner solutions** tile.</span></span> <span data-ttu-id="c135e-190">隨即開啟一個刀鋒視窗，並顯示已連接到資訊安全中心的合作夥伴解決方案清單。</span><span class="sxs-lookup"><span data-stu-id="c135e-190">A blade opens and displays a list of your partner solutions connected to Security Center.</span></span>
   <span data-ttu-id="c135e-191">![][9]</span><span class="sxs-lookup"><span data-stu-id="c135e-191">![Partner solutions][9]</span></span>
3. <span data-ttu-id="c135e-192">選取合作夥伴解決方案。</span><span class="sxs-lookup"><span data-stu-id="c135e-192">Select a partner solution.</span></span> <span data-ttu-id="c135e-193">在本範例中，我們會選取 **QualysVa1** 解決方案。</span><span class="sxs-lookup"><span data-stu-id="c135e-193">In this example, let's select the **QualysVa1** solution.</span></span>  <span data-ttu-id="c135e-194">隨即開啟一個刀鋒視窗，並顯示合作夥伴解決方案的狀態和解決方案相關聯的資源。</span><span class="sxs-lookup"><span data-stu-id="c135e-194">A blade opens and shows you the status of the partner solution and the solution's associated resources.</span></span> <span data-ttu-id="c135e-195">選取 [解決方案主控台]  以開啟此解決方案的合作夥伴管理體驗。</span><span class="sxs-lookup"><span data-stu-id="c135e-195">Select **Solution console** to open the partner management experience for this solution.</span></span>

## <a name="next-steps"></a><span data-ttu-id="c135e-196">後續步驟</span><span class="sxs-lookup"><span data-stu-id="c135e-196">Next steps</span></span>
<span data-ttu-id="c135e-197">此文章介紹了資訊安全中心的安全性監視和原則管理元件。</span><span class="sxs-lookup"><span data-stu-id="c135e-197">This article introduced you to the security monitoring and policy management components of Security Center.</span></span> <span data-ttu-id="c135e-198">現在，您已熟悉資訊安全中心，請嘗試下列步驟︰</span><span class="sxs-lookup"><span data-stu-id="c135e-198">Now that you're familiar with Security Center, try the following steps:</span></span>

* <span data-ttu-id="c135e-199">為您的 Azure 訂用帳戶設定安全性原則。</span><span class="sxs-lookup"><span data-stu-id="c135e-199">Configure a security policy for your Azure subscription.</span></span> <span data-ttu-id="c135e-200">若要深入了解，請參閱[在 Azure 資訊安全中心設定安全性原則](security-center-policies.md)。</span><span class="sxs-lookup"><span data-stu-id="c135e-200">To learn more, see [Setting security policies in Azure Security Center](security-center-policies.md).</span></span>
* <span data-ttu-id="c135e-201">使用資訊安全中心的建議來協助您保護 Azure 資源。</span><span class="sxs-lookup"><span data-stu-id="c135e-201">Use the recommendations in Security Center to help you protect your Azure resources.</span></span> <span data-ttu-id="c135e-202">若要深入了解，請參閱[管理 Azure 資訊安全中心的安全性建議](security-center-recommendations.md)。</span><span class="sxs-lookup"><span data-stu-id="c135e-202">To learn more, see [Managing security recommendations in Azure Security Center](security-center-recommendations.md).</span></span>
* <span data-ttu-id="c135e-203">檢閱並管理目前的安全性警示。</span><span class="sxs-lookup"><span data-stu-id="c135e-203">Review and manage your current security alerts.</span></span> <span data-ttu-id="c135e-204">若要深入了解，請參閱[管理及回應 Azure 資訊安全中心的安全性警示](security-center-managing-and-responding-alerts.md)。</span><span class="sxs-lookup"><span data-stu-id="c135e-204">To learn more, see [Managing and responding to security alerts in Azure Security Center](security-center-managing-and-responding-alerts.md).</span></span>
- <span data-ttu-id="c135e-205">[Azure 資訊安全中心資料安全性](security-center-data-security.md) - 了解資訊安全中心如何管理及保護其中的資料。</span><span class="sxs-lookup"><span data-stu-id="c135e-205">[Azure Security Center data security](security-center-data-security.md) - Learn how data is managed and safeguarded in Security Center.</span></span>
* <span data-ttu-id="c135e-206">深入了解 資訊安全中心[標準層](security-center-pricing.md)隨附的[進階威脅偵測功能](security-center-detection-capabilities.md)。</span><span class="sxs-lookup"><span data-stu-id="c135e-206">Learn more about the [advanced threat detection features](security-center-detection-capabilities.md) that come with the [Standard tier](security-center-pricing.md) of Security Center.</span></span> <span data-ttu-id="c135e-207">標準層的前 60 天免費。</span><span class="sxs-lookup"><span data-stu-id="c135e-207">The Standard tier is offered free for the first 60 days.</span></span>
* <span data-ttu-id="c135e-208">如果您對使用資訊安全中心有問題，請參閱 [Azure 資訊安全中心常見問題集](security-center-faq.md)。</span><span class="sxs-lookup"><span data-stu-id="c135e-208">If you have questions about using Security Center, see the [Azure Security Center FAQ](security-center-faq.md).</span></span>

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
