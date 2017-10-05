---
title: "Azure 資訊安全中心和 Azure 中的 Linux 虛擬機器 | Microsoft Docs"
description: "了解如何使用 Azure 資訊安全中心來確保 Azure Linux 虛擬機器的安全性。"
services: virtual-machines-linux
documentationcenter: virtual-machines
author: neilpeterson
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 05/07/2017
ms.author: nepeters
ms.custom: mvc
ms.openlocfilehash: 7f76da8cd5f4299c64c6e99d0521829c454d8c6c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="monitor-virtual-machine-security-by-using-azure-security-center"></a><span data-ttu-id="b5afd-103">使用 Azure 資訊安全中心來監視虛擬機器</span><span class="sxs-lookup"><span data-stu-id="b5afd-103">Monitor virtual machine security by using Azure Security Center</span></span>

<span data-ttu-id="b5afd-104">Azure 資訊安全中心可協助您了解 Azure 資源的安全性作法。</span><span class="sxs-lookup"><span data-stu-id="b5afd-104">Azure Security Center can help you gain visibility into your Azure resource security practices.</span></span> <span data-ttu-id="b5afd-105">資訊安全中心提供了整合式的安全性監視功能。</span><span class="sxs-lookup"><span data-stu-id="b5afd-105">Security Center offers integrated security monitoring.</span></span> <span data-ttu-id="b5afd-106">它可以偵測到可能不會被察覺的威脅。</span><span class="sxs-lookup"><span data-stu-id="b5afd-106">It can detect threats that otherwise might go unnoticed.</span></span> <span data-ttu-id="b5afd-107">在本教學課程中，您將會了解 Azure 資訊安全中心，以及要如何︰</span><span class="sxs-lookup"><span data-stu-id="b5afd-107">In this tutorial, you learn about Azure Security Center, and how to:</span></span>
 
> [!div class="checklist"]
> * <span data-ttu-id="b5afd-108">設定資料收集功能</span><span class="sxs-lookup"><span data-stu-id="b5afd-108">Set up data collection</span></span>
> * <span data-ttu-id="b5afd-109">設定安全性原則</span><span class="sxs-lookup"><span data-stu-id="b5afd-109">Set up security policies</span></span>
> * <span data-ttu-id="b5afd-110">檢視及修正組態的健康狀態問題</span><span class="sxs-lookup"><span data-stu-id="b5afd-110">View and fix configuration health issues</span></span>
> * <span data-ttu-id="b5afd-111">檢閱所偵測到的威脅</span><span class="sxs-lookup"><span data-stu-id="b5afd-111">Review detected threats</span></span>  

## <a name="security-center-overview"></a><span data-ttu-id="b5afd-112">資訊安全中心概觀</span><span class="sxs-lookup"><span data-stu-id="b5afd-112">Security Center overview</span></span>

<span data-ttu-id="b5afd-113">資訊安全中心會找出潛在的虛擬機器 (VM) 組態問題和針對性的安全性威脅。</span><span class="sxs-lookup"><span data-stu-id="b5afd-113">Security Center identifies potential virtual machine (VM) configuration issues and targeted security threats.</span></span> <span data-ttu-id="b5afd-114">這些項目可能包括缺少網路安全性群組的 VM、磁碟未加密，以及遠端桌面通訊協定 (RDP) 暴力破解攻擊。</span><span class="sxs-lookup"><span data-stu-id="b5afd-114">These might include VMs that are missing network security groups, unencrypted disks, and brute-force Remote Desktop Protocol (RDP) attacks.</span></span> <span data-ttu-id="b5afd-115">此資訊會以容易看懂的圖表形式顯示在資訊安全中心儀表板上。</span><span class="sxs-lookup"><span data-stu-id="b5afd-115">The information is shown on the Security Center dashboard in easy-to-read graphs.</span></span>

<span data-ttu-id="b5afd-116">若要存取資訊安全中心儀表板，請在 Azure 入口網站的功能表上選取 [資訊安全中心]。</span><span class="sxs-lookup"><span data-stu-id="b5afd-116">To access the Security Center dashboard, in the Azure portal, on the menu, select  **Security Center**.</span></span> <span data-ttu-id="b5afd-117">在儀表板上，您可以看到 Azure 環境的安全性健康狀態、找到目前建議項目的計數，以及檢視目前的威脅警示狀態。</span><span class="sxs-lookup"><span data-stu-id="b5afd-117">On the dashboard, you can see the security health of your Azure environment, find a count of current recommendations, and view the current state of threat alerts.</span></span> <span data-ttu-id="b5afd-118">展開每個高階圖表就能查看更多詳細資料。</span><span class="sxs-lookup"><span data-stu-id="b5afd-118">You can expand each high-level chart to see more detail.</span></span>

![資訊安全中心儀表板](./media/tutorial-azure-security/asc-dash.png)

<span data-ttu-id="b5afd-120">資訊安全中心不只能探索資料，它還會提供建議以讓您解決所偵測到的問題。</span><span class="sxs-lookup"><span data-stu-id="b5afd-120">Security Center goes beyond data discovery to provide recommendations for issues that it detects.</span></span> <span data-ttu-id="b5afd-121">例如，如果 VM 在部署時未連結網路安全性群組，資訊安全中心便會顯示建議，並指出可供採取的補救步驟。</span><span class="sxs-lookup"><span data-stu-id="b5afd-121">For example, if a VM was deployed without an attached network security group, Security Center displays a recommendation, with remediation steps you can take.</span></span> <span data-ttu-id="b5afd-122">您不需要離開資訊安全中心便能自動補救。</span><span class="sxs-lookup"><span data-stu-id="b5afd-122">You get automated remediation without leaving the context of Security Center.</span></span>  

![建議](./media/tutorial-azure-security/recommendations.png)

## <a name="set-up-data-collection"></a><span data-ttu-id="b5afd-124">設定資料收集功能</span><span class="sxs-lookup"><span data-stu-id="b5afd-124">Set up data collection</span></span>

<span data-ttu-id="b5afd-125">您必須先設定資訊安全中心的資料收集功能，才能了解 VM 的安全性組態。</span><span class="sxs-lookup"><span data-stu-id="b5afd-125">Before you can get visibility into VM security configurations, you need to set up Security Center data collection.</span></span> <span data-ttu-id="b5afd-126">設定過程中，您會開啟資料收集功能，並建立 Azure 儲存體帳戶以保存收集到的資料。</span><span class="sxs-lookup"><span data-stu-id="b5afd-126">This involves turning on data collection and creating an Azure storage account to hold collected data.</span></span> 

1. <span data-ttu-id="b5afd-127">在資訊安全中心儀表板上，按一下 [安全性原則] 並選取您的訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="b5afd-127">On the Security Center dashboard, click **Security policy**, and then select your subscription.</span></span> 
2. <span data-ttu-id="b5afd-128">在 [資料收集] 中選取 [開啟]。</span><span class="sxs-lookup"><span data-stu-id="b5afd-128">For **Data collection**, select **On**.</span></span>
3. <span data-ttu-id="b5afd-129">若要建立儲存體帳戶，請選取 [選擇儲存體帳戶]。</span><span class="sxs-lookup"><span data-stu-id="b5afd-129">To create a storage account, select **Choose a storage account**.</span></span> <span data-ttu-id="b5afd-130">然後選取 [確定]。</span><span class="sxs-lookup"><span data-stu-id="b5afd-130">Then, select **OK**.</span></span>
4. <span data-ttu-id="b5afd-131">在 [安全性原則] 刀鋒視窗中，選取 [儲存]。</span><span class="sxs-lookup"><span data-stu-id="b5afd-131">On the **Security Policy** blade, select **Save**.</span></span> 

<span data-ttu-id="b5afd-132">系統隨即會在所有 VM 上安裝資訊安全中心的資料收集代理程式，並開始收集資料。</span><span class="sxs-lookup"><span data-stu-id="b5afd-132">The Security Center data collection agent is then installed on all VMs, and data collection begins.</span></span> 

## <a name="set-up-a-security-policy"></a><span data-ttu-id="b5afd-133">設定安全性原則</span><span class="sxs-lookup"><span data-stu-id="b5afd-133">Set up a security policy</span></span>

<span data-ttu-id="b5afd-134">安全性原則可用來定義原則項目，讓資訊安全中心收集其資料並提出建議。</span><span class="sxs-lookup"><span data-stu-id="b5afd-134">Security policies are used to define the items for which Security Center collects data and makes recommendations.</span></span> <span data-ttu-id="b5afd-135">您可以對不同的 Azure 資源集合套用不同的安全性原則。</span><span class="sxs-lookup"><span data-stu-id="b5afd-135">You can apply different security policies to different sets of Azure resources.</span></span> <span data-ttu-id="b5afd-136">雖然系統預設會根據所有原則項目來評估 Azure 資源，但您可以針對所有 Azure 資源或某個資源群組來關閉個別的原則項目。</span><span class="sxs-lookup"><span data-stu-id="b5afd-136">Although by default Azure resources are evaluated against all policy items, you can turn off individual policy items for all Azure resources or for a resource group.</span></span> <span data-ttu-id="b5afd-137">若要深入了解資訊安全中心的安全性原則，請參閱[在 Azure 資訊安全中心設定安全性原則](../../security-center/security-center-policies.md)。</span><span class="sxs-lookup"><span data-stu-id="b5afd-137">For in-depth information about Security Center security policies, see [Set security policies in Azure Security Center](../../security-center/security-center-policies.md).</span></span> 

<span data-ttu-id="b5afd-138">若要設定所有 Azure 資源的安全性原則：</span><span class="sxs-lookup"><span data-stu-id="b5afd-138">To set up a security policy for all Azure resources:</span></span>

1. <span data-ttu-id="b5afd-139">在資訊安全中心儀表板上，選取 [安全性原則] 並選取您的訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="b5afd-139">On the Security Center dashboard, select **Security policy**, and then select your subscription.</span></span>
2. <span data-ttu-id="b5afd-140">選取 [預防原則]。</span><span class="sxs-lookup"><span data-stu-id="b5afd-140">Select **Prevention policy**.</span></span>
3. <span data-ttu-id="b5afd-141">開啟您要對所有 Azure 資源套用的原則項目，或將項目關閉。</span><span class="sxs-lookup"><span data-stu-id="b5afd-141">Turn on or turn off policy items that you want to apply to all Azure resources.</span></span>
4. <span data-ttu-id="b5afd-142">當您選好設定時，請選取 [確定]。</span><span class="sxs-lookup"><span data-stu-id="b5afd-142">When you're finished selecting your settings, select **OK**.</span></span>
5. <span data-ttu-id="b5afd-143">在 [安全性原則] 刀鋒視窗中，選取 [儲存]。</span><span class="sxs-lookup"><span data-stu-id="b5afd-143">On the **Security policy** blade, select **Save**.</span></span> 

<span data-ttu-id="b5afd-144">若要設定特定資源群組的原則︰</span><span class="sxs-lookup"><span data-stu-id="b5afd-144">To set up a policy for a specific resource group:</span></span>

1. <span data-ttu-id="b5afd-145">在資訊安全中心儀表板上，選取 [安全性原則] 並選取資源群組。</span><span class="sxs-lookup"><span data-stu-id="b5afd-145">On the Security Center dashboard, select **Security policy**, and then select a resource group.</span></span>
2. <span data-ttu-id="b5afd-146">選取 [預防原則]。</span><span class="sxs-lookup"><span data-stu-id="b5afd-146">Select **Prevention policy**.</span></span>
3. <span data-ttu-id="b5afd-147">開啟您要對該資源群組套用的原則項目，或將項目關閉。</span><span class="sxs-lookup"><span data-stu-id="b5afd-147">Turn on or turn off policy items that you want to apply to the resource group.</span></span>
4. <span data-ttu-id="b5afd-148">在 [繼承] 底下選取 [唯一]。</span><span class="sxs-lookup"><span data-stu-id="b5afd-148">Under **INHERITANCE**, select **Unique**.</span></span>
5. <span data-ttu-id="b5afd-149">當您選好設定時，請選取 [確定]。</span><span class="sxs-lookup"><span data-stu-id="b5afd-149">When you're finished selecting your settings, select **OK**.</span></span>
6. <span data-ttu-id="b5afd-150">在 [安全性原則] 刀鋒視窗中，選取 [儲存]。</span><span class="sxs-lookup"><span data-stu-id="b5afd-150">On the **Security policy** blade, select **Save**.</span></span>  

<span data-ttu-id="b5afd-151">您也可以在此頁面關閉特定資源群組的資料收集功能。</span><span class="sxs-lookup"><span data-stu-id="b5afd-151">You also can turn off data collection for a specific resource group on this page.</span></span>

<span data-ttu-id="b5afd-152">下列範例已為名為 myResoureGroup 的資源群組建立唯一的原則。</span><span class="sxs-lookup"><span data-stu-id="b5afd-152">In the following example, a unique policy has been created for a resource group named *myResoureGroup*.</span></span> <span data-ttu-id="b5afd-153">此原則會關閉磁碟加密和 Web 應用程式防火牆的建議。</span><span class="sxs-lookup"><span data-stu-id="b5afd-153">In this policy, disk encryption and web application firewall recommendations are turned off.</span></span>

![唯一原則](./media/tutorial-azure-security/unique-policy.png)

## <a name="view-vm-configuration-health"></a><span data-ttu-id="b5afd-155">檢視 VM 組態健康狀態</span><span class="sxs-lookup"><span data-stu-id="b5afd-155">View VM configuration health</span></span>

<span data-ttu-id="b5afd-156">在開啟資料收集功能並設定好安全性原則後，資訊安全中心會開始提供警示和建議。</span><span class="sxs-lookup"><span data-stu-id="b5afd-156">After you've turned on data collection and set a security policy, Security Center begins to provide alerts and recommendations.</span></span> <span data-ttu-id="b5afd-157">VM 在部署時就已安裝好資料收集代理程式。</span><span class="sxs-lookup"><span data-stu-id="b5afd-157">As VMs are deployed, the data collection agent is installed.</span></span> <span data-ttu-id="b5afd-158">之後，系統就會在資訊安全中心內填入新 VM 的資料。</span><span class="sxs-lookup"><span data-stu-id="b5afd-158">Security Center is then populated with data for the new VMs.</span></span> <span data-ttu-id="b5afd-159">若要深入了解 VM 組態的健康狀態，請參閱[在資訊安全中心內保護您的 VM](../../security-center/security-center-virtual-machine-recommendations.md)。</span><span class="sxs-lookup"><span data-stu-id="b5afd-159">For in-depth information about VM configuration health, see [Protect your VMs in Security Center](../../security-center/security-center-virtual-machine-recommendations.md).</span></span> 

<span data-ttu-id="b5afd-160">隨著資料的收集，系統會彙總每個 VM 和相關 Azure 資源的資源健康狀態。</span><span class="sxs-lookup"><span data-stu-id="b5afd-160">As data is collected, the resource health for each VM and related Azure resource is aggregated.</span></span> <span data-ttu-id="b5afd-161">此資訊會以容易看懂的圖表形式來顯示。</span><span class="sxs-lookup"><span data-stu-id="b5afd-161">The information is shown in an easy-to-read chart.</span></span> 

<span data-ttu-id="b5afd-162">若要檢視資源健康狀態︰</span><span class="sxs-lookup"><span data-stu-id="b5afd-162">To view resource health:</span></span>

1.  <span data-ttu-id="b5afd-163">在資訊安全中心儀表板的 [資源安全性健康狀態] 底下，選取 [計算]。</span><span class="sxs-lookup"><span data-stu-id="b5afd-163">On the Security Center dashboard, under **Resource security health**, select **Compute**.</span></span> 
2.  <span data-ttu-id="b5afd-164">在 [計算] 刀鋒視窗中選取 [虛擬機器]。</span><span class="sxs-lookup"><span data-stu-id="b5afd-164">On the **Compute** blade, select **Virtual machines**.</span></span> <span data-ttu-id="b5afd-165">此檢視會提供所有 VM 組態的狀態摘要。</span><span class="sxs-lookup"><span data-stu-id="b5afd-165">This view provides a summary of the configuration status for all your VMs.</span></span>

![計算健康狀態](./media/tutorial-azure-security/compute-health.png)

<span data-ttu-id="b5afd-167">若要查看某個 VM 的所有建議，請選取該 VM。</span><span class="sxs-lookup"><span data-stu-id="b5afd-167">To see all recommendations for a VM, select the VM.</span></span> <span data-ttu-id="b5afd-168">本教學課程會在下一節詳述各項建議和補救步驟。</span><span class="sxs-lookup"><span data-stu-id="b5afd-168">Recommendations and remediation are covered in more detail in the next section of this tutorial.</span></span>

## <a name="remediate-configuration-issues"></a><span data-ttu-id="b5afd-169">補救組態問題：</span><span class="sxs-lookup"><span data-stu-id="b5afd-169">Remediate configuration issues</span></span>

<span data-ttu-id="b5afd-170">在資訊安全中心開始填入組態資料後，系統會根據您設定的安全性原則來提出建議。</span><span class="sxs-lookup"><span data-stu-id="b5afd-170">After Security Center begins to populate with configuration data, recommendations are made based on the security policy you set up.</span></span> <span data-ttu-id="b5afd-171">例如，如果 VM 在設置時沒有相關聯的網路安全性群組，系統會建議您建立一個安全性群組。</span><span class="sxs-lookup"><span data-stu-id="b5afd-171">For instance, if a VM was set up without an associated network security group, a recommendation is made to create one.</span></span> 

<span data-ttu-id="b5afd-172">若要查看所有建議項目的清單︰</span><span class="sxs-lookup"><span data-stu-id="b5afd-172">To see a list of all recommendations:</span></span> 

1. <span data-ttu-id="b5afd-173">在資訊安全中心儀表板上，選取 [建議]。</span><span class="sxs-lookup"><span data-stu-id="b5afd-173">On the Security Center dashboard, select **Recommendations**.</span></span>
2. <span data-ttu-id="b5afd-174">選取特定建議。</span><span class="sxs-lookup"><span data-stu-id="b5afd-174">Select a specific recommendation.</span></span> <span data-ttu-id="b5afd-175">適用該項建議的所有資源清單隨即會出現。</span><span class="sxs-lookup"><span data-stu-id="b5afd-175">A list of all resources for which the recommendation applies appears.</span></span>
3. <span data-ttu-id="b5afd-176">若要套用建議，請選取特定資源。</span><span class="sxs-lookup"><span data-stu-id="b5afd-176">To apply a recommendation, select a specific resource.</span></span> 
4. <span data-ttu-id="b5afd-177">遵循補救步驟的指示來進行。</span><span class="sxs-lookup"><span data-stu-id="b5afd-177">Follow the instructions for remediation steps.</span></span> 

<span data-ttu-id="b5afd-178">在許多情況下，資訊安全中心會提供可行步驟，供您執行建議卻又無須離開資訊安全中心。</span><span class="sxs-lookup"><span data-stu-id="b5afd-178">In many cases, Security Center provides actionable steps you can take to address a recommendation without leaving Security Center.</span></span> <span data-ttu-id="b5afd-179">在下列範例中，資訊安全中心會偵測到輸入規則未受限制的網路安全性群組。</span><span class="sxs-lookup"><span data-stu-id="b5afd-179">In the following example, Security Center detects a network security group that has an unrestricted inbound rule.</span></span> <span data-ttu-id="b5afd-180">在建議頁面中，您可以選取 [編輯輸入規則] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="b5afd-180">On the recommendation page, you can select the **Edit inbound rules** button.</span></span> <span data-ttu-id="b5afd-181">用以修改規則的 UI 會隨即出現。</span><span class="sxs-lookup"><span data-stu-id="b5afd-181">The UI that is needed to modify the rule appears.</span></span> 

![建議](./media/tutorial-azure-security/remediation.png)

<span data-ttu-id="b5afd-183">建議在執行補救後會標示為已解決。</span><span class="sxs-lookup"><span data-stu-id="b5afd-183">As recommendations are remediated, they are marked as resolved.</span></span> 

## <a name="view-detected-threats"></a><span data-ttu-id="b5afd-184">檢視偵測到的威脅</span><span class="sxs-lookup"><span data-stu-id="b5afd-184">View detected threats</span></span>

<span data-ttu-id="b5afd-185">除了資源組態建議外，資訊安全中心也會提供威脅偵測警示。</span><span class="sxs-lookup"><span data-stu-id="b5afd-185">In addition to resource configuration recommendations, Security Center displays threat detection alerts.</span></span> <span data-ttu-id="b5afd-186">安全性警示功能會彙總從每個 VM、Azure 網路記錄和連線合作夥伴解決方案所收集到的資料，以偵測不利於 Azure 資源的安全性威脅。</span><span class="sxs-lookup"><span data-stu-id="b5afd-186">The security alerts feature aggregates data collected from each VM, Azure networking logs, and connected partner solutions to detect security threats against Azure resources.</span></span> <span data-ttu-id="b5afd-187">若要深入了解資訊安全中心的威脅偵測功能，請參閱 [Azure 資訊安全中心的偵測功能](../../security-center/security-center-detection-capabilities.md)。</span><span class="sxs-lookup"><span data-stu-id="b5afd-187">For in-depth information about Security Center threat detection capabilities, see [Azure Security Center detection capabilities](../../security-center/security-center-detection-capabilities.md).</span></span>

<span data-ttu-id="b5afd-188">若要使用安全性警示功能，須將資訊安全中心的定價層從「免費」提升為「標準」。</span><span class="sxs-lookup"><span data-stu-id="b5afd-188">The security alerts feature requires the Security Center pricing tier to be increased from *Free* to *Standard*.</span></span> <span data-ttu-id="b5afd-189">當您改用這個較高的定價層時，您會有 30 天的**免費試用**期。</span><span class="sxs-lookup"><span data-stu-id="b5afd-189">A 30-day **free trial** is available when you move to this higher pricing tier.</span></span> 

<span data-ttu-id="b5afd-190">若要變更定價層：</span><span class="sxs-lookup"><span data-stu-id="b5afd-190">To change the pricing tier:</span></span>  

1. <span data-ttu-id="b5afd-191">在資訊安全中心儀表板上，按一下 [安全性原則] 並選取您的訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="b5afd-191">On the Security Center dashboard, click **Security policy**, and then select your subscription.</span></span>
2. <span data-ttu-id="b5afd-192">選取 [定價層]。</span><span class="sxs-lookup"><span data-stu-id="b5afd-192">Select **Pricing tier**.</span></span>
3. <span data-ttu-id="b5afd-193">選取新的定價層，然後選取 [選取]。</span><span class="sxs-lookup"><span data-stu-id="b5afd-193">Select the new tier, and then select **Select**.</span></span>
4. <span data-ttu-id="b5afd-194">在 [安全性原則] 刀鋒視窗中，選取 [儲存]。</span><span class="sxs-lookup"><span data-stu-id="b5afd-194">On the **Security policy** blade, select **Save**.</span></span> 

<span data-ttu-id="b5afd-195">在變更定價層後，一旦系統偵測到安全性威脅，安全性警示圖表就會開始填入資料。</span><span class="sxs-lookup"><span data-stu-id="b5afd-195">After you've changed the pricing tier, the security alerts graph begins to populate as security threats are detected.</span></span>

![安全性警示](./media/tutorial-azure-security/security-alerts.png)

<span data-ttu-id="b5afd-197">選取警示以檢視資訊。</span><span class="sxs-lookup"><span data-stu-id="b5afd-197">Select an alert to view information.</span></span> <span data-ttu-id="b5afd-198">例如，您可以看到威脅、偵測時間、所有威脅嘗試和建議補救步驟等項目的描述。</span><span class="sxs-lookup"><span data-stu-id="b5afd-198">For example, you can see a description of the threat, the detection time, all threat attempts, and the recommended remediation.</span></span> <span data-ttu-id="b5afd-199">在下列範例中，系統會偵測到 RDP 暴力破解攻擊，且這項 RDP 攻擊嘗試已失敗 294 次。</span><span class="sxs-lookup"><span data-stu-id="b5afd-199">In the following example, an RDP brute-force attack was detected, with 294 failed RDP attempts.</span></span> <span data-ttu-id="b5afd-200">資訊安全中心會提供建議的解決方案。</span><span class="sxs-lookup"><span data-stu-id="b5afd-200">A recommended resolution is provided.</span></span>

![RDP 攻擊](./media/tutorial-azure-security/rdp-attack.png)

## <a name="next-steps"></a><span data-ttu-id="b5afd-202">後續步驟</span><span class="sxs-lookup"><span data-stu-id="b5afd-202">Next steps</span></span>
<span data-ttu-id="b5afd-203">在本教學課程中，您已設定 Azure 資訊安全中心，然後在資訊安全中心檢閱了 VM。</span><span class="sxs-lookup"><span data-stu-id="b5afd-203">In this tutorial, you set up Azure Security Center, and then reviewed VMs in Security Center.</span></span> <span data-ttu-id="b5afd-204">您已了解如何︰</span><span class="sxs-lookup"><span data-stu-id="b5afd-204">You learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="b5afd-205">設定資料收集功能</span><span class="sxs-lookup"><span data-stu-id="b5afd-205">Set up data collection</span></span>
> * <span data-ttu-id="b5afd-206">設定安全性原則</span><span class="sxs-lookup"><span data-stu-id="b5afd-206">Set up security policies</span></span>
> * <span data-ttu-id="b5afd-207">檢視及修正組態的健康狀態問題</span><span class="sxs-lookup"><span data-stu-id="b5afd-207">View and fix configuration health issues</span></span>
> * <span data-ttu-id="b5afd-208">檢閱所偵測到的威脅</span><span class="sxs-lookup"><span data-stu-id="b5afd-208">Review detected threats</span></span>

<span data-ttu-id="b5afd-209">前進到下一個教學課程，深入了解如何利用 Jenkins、GitHub、Docker 建立 CI/CD 管線。</span><span class="sxs-lookup"><span data-stu-id="b5afd-209">Advance to the next tutorial to learn more about creating a CI/CD pipeline with Jenkins, GitHub, and Docker.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="b5afd-210">以 Jenkins、GitHub 及 Docker 建立 CI/CD 基礎結構</span><span class="sxs-lookup"><span data-stu-id="b5afd-210">Create CI/CD infrastructure with Jenkins, GitHub, and Docker</span></span>](tutorial-jenkins-github-docker-cicd.md)

