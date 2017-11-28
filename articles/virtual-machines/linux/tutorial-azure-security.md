---
title: "在 Azure 中的 aaaAzure 資訊安全中心和 Linux 虛擬機器 |Microsoft 文件"
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
ms.openlocfilehash: 7aa0de35fb311457e769f152c8575ec43e41c39c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-virtual-machine-security-by-using-azure-security-center"></a><span data-ttu-id="fdb0f-103">使用 Azure 資訊安全中心來監視虛擬機器</span><span class="sxs-lookup"><span data-stu-id="fdb0f-103">Monitor virtual machine security by using Azure Security Center</span></span>

<span data-ttu-id="fdb0f-104">Azure 資訊安全中心可協助您了解 Azure 資源的安全性作法。</span><span class="sxs-lookup"><span data-stu-id="fdb0f-104">Azure Security Center can help you gain visibility into your Azure resource security practices.</span></span> <span data-ttu-id="fdb0f-105">資訊安全中心提供了整合式的安全性監視功能。</span><span class="sxs-lookup"><span data-stu-id="fdb0f-105">Security Center offers integrated security monitoring.</span></span> <span data-ttu-id="fdb0f-106">它可以偵測到可能不會被察覺的威脅。</span><span class="sxs-lookup"><span data-stu-id="fdb0f-106">It can detect threats that otherwise might go unnoticed.</span></span> <span data-ttu-id="fdb0f-107">在本教學課程中，您將會了解 Azure 資訊安全中心，以及要如何︰</span><span class="sxs-lookup"><span data-stu-id="fdb0f-107">In this tutorial, you learn about Azure Security Center, and how to:</span></span>
 
> [!div class="checklist"]
> * <span data-ttu-id="fdb0f-108">設定資料收集功能</span><span class="sxs-lookup"><span data-stu-id="fdb0f-108">Set up data collection</span></span>
> * <span data-ttu-id="fdb0f-109">設定安全性原則</span><span class="sxs-lookup"><span data-stu-id="fdb0f-109">Set up security policies</span></span>
> * <span data-ttu-id="fdb0f-110">檢視及修正組態的健康狀態問題</span><span class="sxs-lookup"><span data-stu-id="fdb0f-110">View and fix configuration health issues</span></span>
> * <span data-ttu-id="fdb0f-111">檢閱所偵測到的威脅</span><span class="sxs-lookup"><span data-stu-id="fdb0f-111">Review detected threats</span></span>  

## <a name="security-center-overview"></a><span data-ttu-id="fdb0f-112">資訊安全中心概觀</span><span class="sxs-lookup"><span data-stu-id="fdb0f-112">Security Center overview</span></span>

<span data-ttu-id="fdb0f-113">資訊安全中心會找出潛在的虛擬機器 (VM) 組態問題和針對性的安全性威脅。</span><span class="sxs-lookup"><span data-stu-id="fdb0f-113">Security Center identifies potential virtual machine (VM) configuration issues and targeted security threats.</span></span> <span data-ttu-id="fdb0f-114">這些項目可能包括缺少網路安全性群組的 VM、磁碟未加密，以及遠端桌面通訊協定 (RDP) 暴力破解攻擊。</span><span class="sxs-lookup"><span data-stu-id="fdb0f-114">These might include VMs that are missing network security groups, unencrypted disks, and brute-force Remote Desktop Protocol (RDP) attacks.</span></span> <span data-ttu-id="fdb0f-115">hello 資訊安全中心儀表板中容易閱讀圖表會顯示 hello 資訊。</span><span class="sxs-lookup"><span data-stu-id="fdb0f-115">hello information is shown on hello Security Center dashboard in easy-to-read graphs.</span></span>

<span data-ttu-id="fdb0f-116">tooaccess hello 資訊安全中心儀表板，在 Azure 入口網站，在 hello 功能表上，選取 hello**資訊安全中心**。</span><span class="sxs-lookup"><span data-stu-id="fdb0f-116">tooaccess hello Security Center dashboard, in hello Azure portal, on hello menu, select  **Security Center**.</span></span> <span data-ttu-id="fdb0f-117">Hello 儀表板，您可以查看 Azure 環境的 hello 安全性健全狀況、 尋找目前的建議的計數和檢視 hello 的威脅警示的目前狀態。</span><span class="sxs-lookup"><span data-stu-id="fdb0f-117">On hello dashboard, you can see hello security health of your Azure environment, find a count of current recommendations, and view hello current state of threat alerts.</span></span> <span data-ttu-id="fdb0f-118">您可以展開每個高層級圖表 toosee 更多詳細資料。</span><span class="sxs-lookup"><span data-stu-id="fdb0f-118">You can expand each high-level chart toosee more detail.</span></span>

![資訊安全中心儀表板](./media/tutorial-azure-security/asc-dash.png)

<span data-ttu-id="fdb0f-120">資訊安全中心超出資料探索 tooprovide 建議針對它偵測到的問題。</span><span class="sxs-lookup"><span data-stu-id="fdb0f-120">Security Center goes beyond data discovery tooprovide recommendations for issues that it detects.</span></span> <span data-ttu-id="fdb0f-121">例如，如果 VM 在部署時未連結網路安全性群組，資訊安全中心便會顯示建議，並指出可供採取的補救步驟。</span><span class="sxs-lookup"><span data-stu-id="fdb0f-121">For example, if a VM was deployed without an attached network security group, Security Center displays a recommendation, with remediation steps you can take.</span></span> <span data-ttu-id="fdb0f-122">您不需要離開 hello 內容的資訊安全中心取得自動的補救。</span><span class="sxs-lookup"><span data-stu-id="fdb0f-122">You get automated remediation without leaving hello context of Security Center.</span></span>  

![建議](./media/tutorial-azure-security/recommendations.png)

## <a name="set-up-data-collection"></a><span data-ttu-id="fdb0f-124">設定資料收集功能</span><span class="sxs-lookup"><span data-stu-id="fdb0f-124">Set up data collection</span></span>

<span data-ttu-id="fdb0f-125">您可以查看 VM 安全性組態之前，您會需要 tooset 資訊安全中心資料收集。</span><span class="sxs-lookup"><span data-stu-id="fdb0f-125">Before you can get visibility into VM security configurations, you need tooset up Security Center data collection.</span></span> <span data-ttu-id="fdb0f-126">這包括開啟資料收集和 Azure 儲存體帳戶 toohold 收集資料。</span><span class="sxs-lookup"><span data-stu-id="fdb0f-126">This involves turning on data collection and creating an Azure storage account toohold collected data.</span></span> 

1. <span data-ttu-id="fdb0f-127">在 hello 資訊安全中心儀表板上按一下**安全性原則**，然後選取您的訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="fdb0f-127">On hello Security Center dashboard, click **Security policy**, and then select your subscription.</span></span> 
2. <span data-ttu-id="fdb0f-128">在 [資料收集] 中選取 [開啟]。</span><span class="sxs-lookup"><span data-stu-id="fdb0f-128">For **Data collection**, select **On**.</span></span>
3. <span data-ttu-id="fdb0f-129">toocreate 儲存體帳戶中，選取**選擇儲存體帳戶**。</span><span class="sxs-lookup"><span data-stu-id="fdb0f-129">toocreate a storage account, select **Choose a storage account**.</span></span> <span data-ttu-id="fdb0f-130">然後選取 [確定]。</span><span class="sxs-lookup"><span data-stu-id="fdb0f-130">Then, select **OK**.</span></span>
4. <span data-ttu-id="fdb0f-131">在 hello**安全性原則**刀鋒視窗中，選取**儲存**。</span><span class="sxs-lookup"><span data-stu-id="fdb0f-131">On hello **Security Policy** blade, select **Save**.</span></span> 

<span data-ttu-id="fdb0f-132">hello 資訊安全中心資料收集代理程式就會安裝在所有的 Vm，並開始資料收集。</span><span class="sxs-lookup"><span data-stu-id="fdb0f-132">hello Security Center data collection agent is then installed on all VMs, and data collection begins.</span></span> 

## <a name="set-up-a-security-policy"></a><span data-ttu-id="fdb0f-133">設定安全性原則</span><span class="sxs-lookup"><span data-stu-id="fdb0f-133">Set up a security policy</span></span>

<span data-ttu-id="fdb0f-134">使用的 toodefine hello 項目為其資訊安全中心會收集資料，並提出建議的安全性原則。</span><span class="sxs-lookup"><span data-stu-id="fdb0f-134">Security policies are used toodefine hello items for which Security Center collects data and makes recommendations.</span></span> <span data-ttu-id="fdb0f-135">您可以套用不同的安全性原則 toodifferent 組的 Azure 資源。</span><span class="sxs-lookup"><span data-stu-id="fdb0f-135">You can apply different security policies toodifferent sets of Azure resources.</span></span> <span data-ttu-id="fdb0f-136">雖然系統預設會根據所有原則項目來評估 Azure 資源，但您可以針對所有 Azure 資源或某個資源群組來關閉個別的原則項目。</span><span class="sxs-lookup"><span data-stu-id="fdb0f-136">Although by default Azure resources are evaluated against all policy items, you can turn off individual policy items for all Azure resources or for a resource group.</span></span> <span data-ttu-id="fdb0f-137">若要深入了解資訊安全中心的安全性原則，請參閱[在 Azure 資訊安全中心設定安全性原則](../../security-center/security-center-policies.md)。</span><span class="sxs-lookup"><span data-stu-id="fdb0f-137">For in-depth information about Security Center security policies, see [Set security policies in Azure Security Center](../../security-center/security-center-policies.md).</span></span> 

<span data-ttu-id="fdb0f-138">所有的 Azure 資源的安全性原則 tooset:</span><span class="sxs-lookup"><span data-stu-id="fdb0f-138">tooset up a security policy for all Azure resources:</span></span>

1. <span data-ttu-id="fdb0f-139">Hello 資訊安全中心儀表板上選取**安全性原則**，然後選取您的訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="fdb0f-139">On hello Security Center dashboard, select **Security policy**, and then select your subscription.</span></span>
2. <span data-ttu-id="fdb0f-140">選取 [預防原則]。</span><span class="sxs-lookup"><span data-stu-id="fdb0f-140">Select **Prevention policy**.</span></span>
3. <span data-ttu-id="fdb0f-141">開啟或關閉原則項目，您會想 tooapply tooall Azure 資源。</span><span class="sxs-lookup"><span data-stu-id="fdb0f-141">Turn on or turn off policy items that you want tooapply tooall Azure resources.</span></span>
4. <span data-ttu-id="fdb0f-142">當您選好設定時，請選取 [確定]。</span><span class="sxs-lookup"><span data-stu-id="fdb0f-142">When you're finished selecting your settings, select **OK**.</span></span>
5. <span data-ttu-id="fdb0f-143">在 hello**安全性原則**刀鋒視窗中，選取**儲存**。</span><span class="sxs-lookup"><span data-stu-id="fdb0f-143">On hello **Security policy** blade, select **Save**.</span></span> 

<span data-ttu-id="fdb0f-144">tooset 特定資源群組的原則：</span><span class="sxs-lookup"><span data-stu-id="fdb0f-144">tooset up a policy for a specific resource group:</span></span>

1. <span data-ttu-id="fdb0f-145">Hello 資訊安全中心儀表板上選取**安全性原則**，然後選取 資源群組。</span><span class="sxs-lookup"><span data-stu-id="fdb0f-145">On hello Security Center dashboard, select **Security policy**, and then select a resource group.</span></span>
2. <span data-ttu-id="fdb0f-146">選取 [預防原則]。</span><span class="sxs-lookup"><span data-stu-id="fdb0f-146">Select **Prevention policy**.</span></span>
3. <span data-ttu-id="fdb0f-147">開啟或關閉您要讓 tooapply toohello 資源群組的原則項目。</span><span class="sxs-lookup"><span data-stu-id="fdb0f-147">Turn on or turn off policy items that you want tooapply toohello resource group.</span></span>
4. <span data-ttu-id="fdb0f-148">在 [繼承] 底下選取 [唯一]。</span><span class="sxs-lookup"><span data-stu-id="fdb0f-148">Under **INHERITANCE**, select **Unique**.</span></span>
5. <span data-ttu-id="fdb0f-149">當您選好設定時，請選取 [確定]。</span><span class="sxs-lookup"><span data-stu-id="fdb0f-149">When you're finished selecting your settings, select **OK**.</span></span>
6. <span data-ttu-id="fdb0f-150">在 hello**安全性原則**刀鋒視窗中，選取**儲存**。</span><span class="sxs-lookup"><span data-stu-id="fdb0f-150">On hello **Security policy** blade, select **Save**.</span></span>  

<span data-ttu-id="fdb0f-151">您也可以在此頁面關閉特定資源群組的資料收集功能。</span><span class="sxs-lookup"><span data-stu-id="fdb0f-151">You also can turn off data collection for a specific resource group on this page.</span></span>

<span data-ttu-id="fdb0f-152">在下列範例的 hello，唯一的原則已建立名為資源群組的*myResoureGroup*。</span><span class="sxs-lookup"><span data-stu-id="fdb0f-152">In hello following example, a unique policy has been created for a resource group named *myResoureGroup*.</span></span> <span data-ttu-id="fdb0f-153">此原則會關閉磁碟加密和 Web 應用程式防火牆的建議。</span><span class="sxs-lookup"><span data-stu-id="fdb0f-153">In this policy, disk encryption and web application firewall recommendations are turned off.</span></span>

![唯一原則](./media/tutorial-azure-security/unique-policy.png)

## <a name="view-vm-configuration-health"></a><span data-ttu-id="fdb0f-155">檢視 VM 組態健康狀態</span><span class="sxs-lookup"><span data-stu-id="fdb0f-155">View VM configuration health</span></span>

<span data-ttu-id="fdb0f-156">在您開啟 資料收集，並設定安全性原則之後，資訊安全中心會開始 tooprovide 警示和建議。</span><span class="sxs-lookup"><span data-stu-id="fdb0f-156">After you've turned on data collection and set a security policy, Security Center begins tooprovide alerts and recommendations.</span></span> <span data-ttu-id="fdb0f-157">部署 Vm，則會安裝 hello 資料收集代理程式。</span><span class="sxs-lookup"><span data-stu-id="fdb0f-157">As VMs are deployed, hello data collection agent is installed.</span></span> <span data-ttu-id="fdb0f-158">資訊安全中心接著會填入資料 hello 新 Vm。</span><span class="sxs-lookup"><span data-stu-id="fdb0f-158">Security Center is then populated with data for hello new VMs.</span></span> <span data-ttu-id="fdb0f-159">若要深入了解 VM 組態的健康狀態，請參閱[在資訊安全中心內保護您的 VM](../../security-center/security-center-virtual-machine-recommendations.md)。</span><span class="sxs-lookup"><span data-stu-id="fdb0f-159">For in-depth information about VM configuration health, see [Protect your VMs in Security Center](../../security-center/security-center-virtual-machine-recommendations.md).</span></span> 

<span data-ttu-id="fdb0f-160">隨著收集資料，每個 VM 和相關的 Azure 資源的 hello 資源健全狀況彙總。</span><span class="sxs-lookup"><span data-stu-id="fdb0f-160">As data is collected, hello resource health for each VM and related Azure resource is aggregated.</span></span> <span data-ttu-id="fdb0f-161">容易閱讀圖表中會顯示 hello 資訊。</span><span class="sxs-lookup"><span data-stu-id="fdb0f-161">hello information is shown in an easy-to-read chart.</span></span> 

<span data-ttu-id="fdb0f-162">tooview 資源健全狀況：</span><span class="sxs-lookup"><span data-stu-id="fdb0f-162">tooview resource health:</span></span>

1.  <span data-ttu-id="fdb0f-163">Hello 資訊安全中心儀表板上底下**資源安全性健全狀況**，選取**計算**。</span><span class="sxs-lookup"><span data-stu-id="fdb0f-163">On hello Security Center dashboard, under **Resource security health**, select **Compute**.</span></span> 
2.  <span data-ttu-id="fdb0f-164">在 hello**計算**刀鋒視窗中，選取**虛擬機器**。</span><span class="sxs-lookup"><span data-stu-id="fdb0f-164">On hello **Compute** blade, select **Virtual machines**.</span></span> <span data-ttu-id="fdb0f-165">此檢視會為您的 Vm 提供 hello 設定狀態的摘要。</span><span class="sxs-lookup"><span data-stu-id="fdb0f-165">This view provides a summary of hello configuration status for all your VMs.</span></span>

![計算健康狀態](./media/tutorial-azure-security/compute-health.png)

<span data-ttu-id="fdb0f-167">toosee 所有 VM，建議都選取 hello VM。</span><span class="sxs-lookup"><span data-stu-id="fdb0f-167">toosee all recommendations for a VM, select hello VM.</span></span> <span data-ttu-id="fdb0f-168">建議和補救涵蓋 hello 這個教學課程的下一節中詳細說明。</span><span class="sxs-lookup"><span data-stu-id="fdb0f-168">Recommendations and remediation are covered in more detail in hello next section of this tutorial.</span></span>

## <a name="remediate-configuration-issues"></a><span data-ttu-id="fdb0f-169">補救組態問題：</span><span class="sxs-lookup"><span data-stu-id="fdb0f-169">Remediate configuration issues</span></span>

<span data-ttu-id="fdb0f-170">資訊安全中心開始 toopopulate 與設定資料之後，建議都是對根據您設定的 hello 安全性原則。</span><span class="sxs-lookup"><span data-stu-id="fdb0f-170">After Security Center begins toopopulate with configuration data, recommendations are made based on hello security policy you set up.</span></span> <span data-ttu-id="fdb0f-171">比方說，如果 VM 設定不含相關聯的網路安全性的群組，提出該項建議的 toocreate 其中一個。</span><span class="sxs-lookup"><span data-stu-id="fdb0f-171">For instance, if a VM was set up without an associated network security group, a recommendation is made toocreate one.</span></span> 

<span data-ttu-id="fdb0f-172">toosee 所有建議的清單：</span><span class="sxs-lookup"><span data-stu-id="fdb0f-172">toosee a list of all recommendations:</span></span> 

1. <span data-ttu-id="fdb0f-173">Hello 資訊安全中心儀表板上選取**建議**。</span><span class="sxs-lookup"><span data-stu-id="fdb0f-173">On hello Security Center dashboard, select **Recommendations**.</span></span>
2. <span data-ttu-id="fdb0f-174">選取特定建議。</span><span class="sxs-lookup"><span data-stu-id="fdb0f-174">Select a specific recommendation.</span></span> <span data-ttu-id="fdb0f-175">所有資源的 hello 項建議適用於清單隨即出現。</span><span class="sxs-lookup"><span data-stu-id="fdb0f-175">A list of all resources for which hello recommendation applies appears.</span></span>
3. <span data-ttu-id="fdb0f-176">tooapply 建議中，選取特定的資源。</span><span class="sxs-lookup"><span data-stu-id="fdb0f-176">tooapply a recommendation, select a specific resource.</span></span> 
4. <span data-ttu-id="fdb0f-177">請依照 hello 補救步驟的指示。</span><span class="sxs-lookup"><span data-stu-id="fdb0f-177">Follow hello instructions for remediation steps.</span></span> 

<span data-ttu-id="fdb0f-178">在許多情況下，資訊安全中心提供可採取動作的步驟可能不需要離開資訊安全中心需要 tooaddress 建議。</span><span class="sxs-lookup"><span data-stu-id="fdb0f-178">In many cases, Security Center provides actionable steps you can take tooaddress a recommendation without leaving Security Center.</span></span> <span data-ttu-id="fdb0f-179">在下列範例的 hello，資訊安全中心會偵測具有不受限制的輸入的規則的網路安全性群組。</span><span class="sxs-lookup"><span data-stu-id="fdb0f-179">In hello following example, Security Center detects a network security group that has an unrestricted inbound rule.</span></span> <span data-ttu-id="fdb0f-180">您可以在 hello 建議頁面上，選取 hello**編輯輸入的規則** 按鈕。</span><span class="sxs-lookup"><span data-stu-id="fdb0f-180">On hello recommendation page, you can select hello **Edit inbound rules** button.</span></span> <span data-ttu-id="fdb0f-181">hello 需要的 toomodify hello 規則的 UI 會出現。</span><span class="sxs-lookup"><span data-stu-id="fdb0f-181">hello UI that is needed toomodify hello rule appears.</span></span> 

![建議](./media/tutorial-azure-security/remediation.png)

<span data-ttu-id="fdb0f-183">建議在執行補救後會標示為已解決。</span><span class="sxs-lookup"><span data-stu-id="fdb0f-183">As recommendations are remediated, they are marked as resolved.</span></span> 

## <a name="view-detected-threats"></a><span data-ttu-id="fdb0f-184">檢視偵測到的威脅</span><span class="sxs-lookup"><span data-stu-id="fdb0f-184">View detected threats</span></span>

<span data-ttu-id="fdb0f-185">此外 tooresource 設定建議，資訊安全中心會顯示威脅偵測警示。</span><span class="sxs-lookup"><span data-stu-id="fdb0f-185">In addition tooresource configuration recommendations, Security Center displays threat detection alerts.</span></span> <span data-ttu-id="fdb0f-186">hello 安全性警示功能彙總從每個 VM、 Azure 網路的記錄檔和連線的交易夥伴方案 toodetect 對 Azure 資源的安全性威脅所收集的資料。</span><span class="sxs-lookup"><span data-stu-id="fdb0f-186">hello security alerts feature aggregates data collected from each VM, Azure networking logs, and connected partner solutions toodetect security threats against Azure resources.</span></span> <span data-ttu-id="fdb0f-187">若要深入了解資訊安全中心的威脅偵測功能，請參閱 [Azure 資訊安全中心的偵測功能](../../security-center/security-center-detection-capabilities.md)。</span><span class="sxs-lookup"><span data-stu-id="fdb0f-187">For in-depth information about Security Center threat detection capabilities, see [Azure Security Center detection capabilities](../../security-center/security-center-detection-capabilities.md).</span></span>

<span data-ttu-id="fdb0f-188">hello 安全性警示功能需要 hello 資訊安全中心定價層 toobe 從增加*免費*太*標準*。</span><span class="sxs-lookup"><span data-stu-id="fdb0f-188">hello security alerts feature requires hello Security Center pricing tier toobe increased from *Free* too*Standard*.</span></span> <span data-ttu-id="fdb0f-189">30 天**免費試用版**時才能使用移動 toothis 較高的定價層。</span><span class="sxs-lookup"><span data-stu-id="fdb0f-189">A 30-day **free trial** is available when you move toothis higher pricing tier.</span></span> 

<span data-ttu-id="fdb0f-190">toochange hello 定價層：</span><span class="sxs-lookup"><span data-stu-id="fdb0f-190">toochange hello pricing tier:</span></span>  

1. <span data-ttu-id="fdb0f-191">在 hello 資訊安全中心儀表板上按一下**安全性原則**，然後選取您的訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="fdb0f-191">On hello Security Center dashboard, click **Security policy**, and then select your subscription.</span></span>
2. <span data-ttu-id="fdb0f-192">選取 [定價層]。</span><span class="sxs-lookup"><span data-stu-id="fdb0f-192">Select **Pricing tier**.</span></span>
3. <span data-ttu-id="fdb0f-193">選取 hello 新的層，然後選取**選取**。</span><span class="sxs-lookup"><span data-stu-id="fdb0f-193">Select hello new tier, and then select **Select**.</span></span>
4. <span data-ttu-id="fdb0f-194">在 hello**安全性原則**刀鋒視窗中，選取**儲存**。</span><span class="sxs-lookup"><span data-stu-id="fdb0f-194">On hello **Security policy** blade, select **Save**.</span></span> 

<span data-ttu-id="fdb0f-195">您已變更定價層的 hello 之後，hello 安全性警示圖形開始 toopopulate 會偵測到安全性威脅。</span><span class="sxs-lookup"><span data-stu-id="fdb0f-195">After you've changed hello pricing tier, hello security alerts graph begins toopopulate as security threats are detected.</span></span>

![安全性警示](./media/tutorial-azure-security/security-alerts.png)

<span data-ttu-id="fdb0f-197">選取警示 tooview 資訊。</span><span class="sxs-lookup"><span data-stu-id="fdb0f-197">Select an alert tooview information.</span></span> <span data-ttu-id="fdb0f-198">例如，您可以看到說明 hello 威脅、 hello 偵測時間、 所有潛在威脅的嘗試，並 hello 建議的補救。</span><span class="sxs-lookup"><span data-stu-id="fdb0f-198">For example, you can see a description of hello threat, hello detection time, all threat attempts, and hello recommended remediation.</span></span> <span data-ttu-id="fdb0f-199">在下列範例的 hello，RDP 暴力攻擊偵測到，與超出 294 嘗試失敗 RDP。</span><span class="sxs-lookup"><span data-stu-id="fdb0f-199">In hello following example, an RDP brute-force attack was detected, with 294 failed RDP attempts.</span></span> <span data-ttu-id="fdb0f-200">資訊安全中心會提供建議的解決方案。</span><span class="sxs-lookup"><span data-stu-id="fdb0f-200">A recommended resolution is provided.</span></span>

![RDP 攻擊](./media/tutorial-azure-security/rdp-attack.png)

## <a name="next-steps"></a><span data-ttu-id="fdb0f-202">後續步驟</span><span class="sxs-lookup"><span data-stu-id="fdb0f-202">Next steps</span></span>
<span data-ttu-id="fdb0f-203">在本教學課程中，您已設定 Azure 資訊安全中心，然後在資訊安全中心檢閱了 VM。</span><span class="sxs-lookup"><span data-stu-id="fdb0f-203">In this tutorial, you set up Azure Security Center, and then reviewed VMs in Security Center.</span></span> <span data-ttu-id="fdb0f-204">您已了解如何︰</span><span class="sxs-lookup"><span data-stu-id="fdb0f-204">You learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="fdb0f-205">設定資料收集功能</span><span class="sxs-lookup"><span data-stu-id="fdb0f-205">Set up data collection</span></span>
> * <span data-ttu-id="fdb0f-206">設定安全性原則</span><span class="sxs-lookup"><span data-stu-id="fdb0f-206">Set up security policies</span></span>
> * <span data-ttu-id="fdb0f-207">檢視及修正組態的健康狀態問題</span><span class="sxs-lookup"><span data-stu-id="fdb0f-207">View and fix configuration health issues</span></span>
> * <span data-ttu-id="fdb0f-208">檢閱所偵測到的威脅</span><span class="sxs-lookup"><span data-stu-id="fdb0f-208">Review detected threats</span></span>

<span data-ttu-id="fdb0f-209">前進 toohello 下一個教學課程 toolearn 有關使用 Jenkins、 GitHub 和 Docker 建立 CI/CD 管線的詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="fdb0f-209">Advance toohello next tutorial toolearn more about creating a CI/CD pipeline with Jenkins, GitHub, and Docker.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="fdb0f-210">以 Jenkins、GitHub 及 Docker 建立 CI/CD 基礎結構</span><span class="sxs-lookup"><span data-stu-id="fdb0f-210">Create CI/CD infrastructure with Jenkins, GitHub, and Docker</span></span>](tutorial-jenkins-github-docker-cicd.md)

