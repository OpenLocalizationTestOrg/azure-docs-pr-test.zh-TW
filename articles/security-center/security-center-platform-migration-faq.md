---
title: "資訊安全中心平台移轉常見問題集 | Microsoft Docs"
description: "本常見問題集回答 Azure 資訊安全中心平台移轉的相關問題。"
services: security-center
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
editor: 
ms.assetid: 4d1364cd-7847-425a-bb3a-722cb0779f78
ms.service: security-center
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/15/2017
ms.author: terrylan
ms.openlocfilehash: 2ffbaca614d667db565197f3c13b1658fffc2a7c
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/18/2017
---
# <a name="security-center-platform-migration-faq"></a><span data-ttu-id="7b991-103">資訊安全中心平台移轉常見問題集</span><span class="sxs-lookup"><span data-stu-id="7b991-103">Security Center platform migration FAQ</span></span>
<span data-ttu-id="7b991-104">在 2017 年 6 月初，Azure 資訊安全中心開始使用 Microsoft Monitoring Agent 來收集與儲存資料。</span><span class="sxs-lookup"><span data-stu-id="7b991-104">In early June 2017, Azure Security Center began using the Microsoft Monitoring Agent to collect and store data.</span></span> <span data-ttu-id="7b991-105">如需詳細資訊，請參閱 [Azure 資訊安全中心平台移轉](security-center-platform-migration.md)。</span><span class="sxs-lookup"><span data-stu-id="7b991-105">To learn more, see [Azure Security Center Platform Migration](security-center-platform-migration.md).</span></span> <span data-ttu-id="7b991-106">本常見問題集回答平台移轉的相關問題。</span><span class="sxs-lookup"><span data-stu-id="7b991-106">This FAQ answers questions about the platform migration.</span></span>

## <a name="data-collection-agents-and-workspaces"></a><span data-ttu-id="7b991-107">資料收集、代理程式及工作區</span><span class="sxs-lookup"><span data-stu-id="7b991-107">Data collection, agents, and workspaces</span></span>

### <a name="how-is-data-collected"></a><span data-ttu-id="7b991-108">資料如何收集？</span><span class="sxs-lookup"><span data-stu-id="7b991-108">How is data collected?</span></span>
<span data-ttu-id="7b991-109">資訊安全中心使用 Microsoft Monitoring Agent 從您的虛擬機器收集安全性資料。</span><span class="sxs-lookup"><span data-stu-id="7b991-109">Security Center uses the Microsoft Monitoring Agent to collect security data from your VMs.</span></span> <span data-ttu-id="7b991-110">這些安全性資料包括用來識別弱點之安全性設定，以及用來偵測威脅之安全性事件的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="7b991-110">The security data includes information about security configurations, which are used to identify vulnerabilities, and security events, which are used to detect threats.</span></span> <span data-ttu-id="7b991-111">代理程式所收集的資料會儲存在連線到虛擬機器的既存 Log Analytics 工作區，或是在資訊安全中心建立的新工作區。</span><span class="sxs-lookup"><span data-stu-id="7b991-111">Data collected by the agent is stored in either an existing Log Analytics workspace connected to the VM or a new workspace created by Security Center.</span></span> <span data-ttu-id="7b991-112">資訊安全中心建立新工作區時，會將虛擬機器的地理位置納入考量。</span><span class="sxs-lookup"><span data-stu-id="7b991-112">When Security Center creates a new workspace, the geolocation of the VM is taken into account.</span></span>

> [!NOTE]
> <span data-ttu-id="7b991-113">Microsoft Monitoring Agent 是 Operations Management Suite (OMS)、Log Analytics 服務及 System Center Operations Manager (SCOM) 所使用的代理程式。</span><span class="sxs-lookup"><span data-stu-id="7b991-113">The Microsoft Monitoring Agent is the same agent used by the Operations Management Suite (OMS), Log Analytics service and System Center Operations Manager (SCOM).</span></span>
>
>

<span data-ttu-id="7b991-114">初次啟用資料收集或訂用帳戶移轉後，資訊安全中心會確認 Microsoft Monitoring Agent 是否已經以 Azure 擴充功能的形式安裝在您的虛擬機器上。</span><span class="sxs-lookup"><span data-stu-id="7b991-114">When data collection is enabled for the first time or when your subscriptions are migrated, Security Center checks to see if the Microsoft Monitoring Agent is already installed as an Azure extension on each of your VMs.</span></span> <span data-ttu-id="7b991-115">如果未安裝 Microsoft Monitoring Agent，資訊安全中心將：</span><span class="sxs-lookup"><span data-stu-id="7b991-115">If the Microsoft Monitoring Agent is not installed, then Security Center will:</span></span>

- <span data-ttu-id="7b991-116">在虛擬機器上安裝 Microsoft Monitoring Agent</span><span class="sxs-lookup"><span data-stu-id="7b991-116">install the Microsoft Monitoring agent on the VM</span></span>
   - <span data-ttu-id="7b991-117">若資訊安全中心已經建立了與虛擬機器存在於相同地理位置的工作區，代理程式即會連線到此工作區</span><span class="sxs-lookup"><span data-stu-id="7b991-117">if a workspace created by Security Center already exists in the same geolocation as the VM, the agent is connected to this workspace</span></span>
   - <span data-ttu-id="7b991-118">如果沒有這樣的工作區，資訊安全中心會在此地理位置建立新的資源群組和預設工作區，並將代理程式連線到該工作區。</span><span class="sxs-lookup"><span data-stu-id="7b991-118">if a workspace does not exist, Security Center creates a new resource group and default workspace in that geolocation, and connect the agent to that workspace.</span></span> <span data-ttu-id="7b991-119">工作區和資源群組的命名慣例如下：</span><span class="sxs-lookup"><span data-stu-id="7b991-119">The naming convention for the workspace and resource group are:</span></span>

       <span data-ttu-id="7b991-120">工作區：DefaultWorkspace-[subscription-ID]-[geo]</span><span class="sxs-lookup"><span data-stu-id="7b991-120">Workspace: DefaultWorkspace-[subscription-ID]-[geo]</span></span>

       <span data-ttu-id="7b991-121">資源群組：DefaultResouceGroup-[geo]</span><span class="sxs-lookup"><span data-stu-id="7b991-121">Resource Group: DefaultResouceGroup-[geo]</span></span>
- <span data-ttu-id="7b991-122">在工作區上安裝資訊安全中心解決方案</span><span class="sxs-lookup"><span data-stu-id="7b991-122">install a Security Center solution on the workspace</span></span>

<span data-ttu-id="7b991-123">工作區的位置取決於虛擬機器的位置。</span><span class="sxs-lookup"><span data-stu-id="7b991-123">The location of the workspace is based on the location of the VM.</span></span> <span data-ttu-id="7b991-124">若要深入了解，請參閱[資料安全性](security-center-data-security.md)。</span><span class="sxs-lookup"><span data-stu-id="7b991-124">To learn more, see [Data Security](security-center-data-security.md).</span></span>

> [!NOTE]
> <span data-ttu-id="7b991-125">平台移轉之前，資訊安全中心已使用 Azure Monitoring Agent 從您的虛擬機器收集安全性資料，並將資料儲存到您的儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="7b991-125">Prior to platform migration, Security Center collected security data from your VMs using the Azure Monitoring Agent, and data was stored in your storage account.</span></span> <span data-ttu-id="7b991-126">平台移轉之後，資訊安全中心會使用 Microsoft Monitoring Agent 及工作區來與儲存該資料。</span><span class="sxs-lookup"><span data-stu-id="7b991-126">After the platform migration, Security Center uses the Microsoft Monitoring Agent and workspace to collect and store the same data.</span></span> <span data-ttu-id="7b991-127">移轉之後就可以移除儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="7b991-127">The storage account can be removed after the migration.</span></span>
>
>

### <a name="am-i-billed-for-log-analytics-or-oms-on-the-workspaces-created-by-security-center"></a><span data-ttu-id="7b991-128">資訊安全中心建立之工作區的 Log Analytics 或 OMS 是否需要付費？</span><span class="sxs-lookup"><span data-stu-id="7b991-128">Am I billed for Log Analytics or OMS on the workspaces created by Security Center?</span></span>
<span data-ttu-id="7b991-129">否。</span><span class="sxs-lookup"><span data-stu-id="7b991-129">No.</span></span> <span data-ttu-id="7b991-130">資訊安全中心所建立的工作區雖然設定以每節點之 OMS 計費，但實際上不會產生 OMS 費用。</span><span class="sxs-lookup"><span data-stu-id="7b991-130">Workspaces created by Security Center, while configured for OMS per node billing, do not incur OMS charges.</span></span> <span data-ttu-id="7b991-131">資訊安全中心的計費一律根據您的資訊安全中心的安全性原則，以及工作區安裝的解決方案：</span><span class="sxs-lookup"><span data-stu-id="7b991-131">Security Center billing is always based on your Security Center security policy and the solutions installed on a workspace:</span></span>

- <span data-ttu-id="7b991-132">**免費層** – 資訊安全中心在預設工作區安裝 SecurityCenterFree 解決方案。</span><span class="sxs-lookup"><span data-stu-id="7b991-132">**Free tier** – Security Center installs the 'SecurityCenterFree' solution on the default workspace.</span></span> <span data-ttu-id="7b991-133">免費層不須付費。</span><span class="sxs-lookup"><span data-stu-id="7b991-133">You are not billed for the Free tier.</span></span>
- <span data-ttu-id="7b991-134">**標準層** – 資訊安全中心在預設工作區安裝 SecurityCenterFree 及 Security 解決方案。</span><span class="sxs-lookup"><span data-stu-id="7b991-134">**Standard tier** – Security Center installs the 'SecurityCenterFree' and 'Security’ solutions on the default workspace.</span></span>

<span data-ttu-id="7b991-135">如需詳細資訊，請參閱[資訊安全中心價格](https://azure.microsoft.com/pricing/details/security-center/)。</span><span class="sxs-lookup"><span data-stu-id="7b991-135">For more information on pricing, see [Security Center pricing](https://azure.microsoft.com/pricing/details/security-center/).</span></span> <span data-ttu-id="7b991-136">價格頁面反映了自 2017 年起 6 月起安全性資料儲存體及依比例計費的改變。</span><span class="sxs-lookup"><span data-stu-id="7b991-136">The pricing page addresses changes to security data storage and prorated billing starting in June 2017.</span></span>

> [!NOTE]
> <span data-ttu-id="7b991-137">資訊安全中心所建立之工作區的 OMS 定價層不會影響資訊安全中心的收費。</span><span class="sxs-lookup"><span data-stu-id="7b991-137">The OMS pricing tier of workspaces created by Security Center does not affect Security Center billing.</span></span>
>
>

### <a name="can-i-delete-the-default-workspaces-created-by-security-center"></a><span data-ttu-id="7b991-138">我可以刪除資訊安全中心所建立的預設工作區嗎？</span><span class="sxs-lookup"><span data-stu-id="7b991-138">Can I delete the default workspaces created by Security Center?</span></span>
<span data-ttu-id="7b991-139">**建議您不要刪除預設工作區。**</span><span class="sxs-lookup"><span data-stu-id="7b991-139">**Deleting the default workspace is not recommended.**</span></span> <span data-ttu-id="7b991-140">資訊安全中心會使用預設工作區儲存您虛擬機器傳來的安全性資料。</span><span class="sxs-lookup"><span data-stu-id="7b991-140">Security Center uses the default workspaces to store security data from your VMs.</span></span>  <span data-ttu-id="7b991-141">如果您刪除了工作區，資訊安全中心無法收集此資料，特定安全性建議及警示就無法使用</span><span class="sxs-lookup"><span data-stu-id="7b991-141">If you delete a workspace, Security Center is unable to collect this data and some security recommendations and alerts are unavailable</span></span>

<span data-ttu-id="7b991-142">若要復原，請將連線到刪除工作區之虛擬機器上的 Microsoft Monitoring Agent 移除。</span><span class="sxs-lookup"><span data-stu-id="7b991-142">To recover, remove the Microsoft Monitoring Agent on the VMs connected to the deleted workspace.</span></span> <span data-ttu-id="7b991-143">資訊安全中心會重新安裝代理程式，並建立新的預設工作區。</span><span class="sxs-lookup"><span data-stu-id="7b991-143">Security Center reinstalls the agent and creates new default workspaces.</span></span>

### <a name="what-if-the-microsoft-monitoring-agent-was-already-installed-as-an-extension-on-the-vm"></a><span data-ttu-id="7b991-144">如果虛擬機器上 Microsoft Monitoring Agent 已經以擴充功能的形式安裝了呢？</span><span class="sxs-lookup"><span data-stu-id="7b991-144">What if the Microsoft Monitoring Agent was already installed as an extension on the VM?</span></span>
<span data-ttu-id="7b991-145">資訊安全中心不會覆寫既存的使用者工作區連線。</span><span class="sxs-lookup"><span data-stu-id="7b991-145">Security Center does not override existing connections to user workspaces.</span></span> <span data-ttu-id="7b991-146">資訊安全中心會將虛擬機器送出的資料儲存到已經連線的工作區。</span><span class="sxs-lookup"><span data-stu-id="7b991-146">Security Center stores security data from the VM in the workspace already connected.</span></span>

### <a name="what-if-i-had-a-microsoft-monitoring-agent-installed-on-the-machine-but-not-as-an-extension"></a><span data-ttu-id="7b991-147">如果我已經在機器上安裝了 Microsoft Monitoring Agent，但不是以擴充功能的形式呢？</span><span class="sxs-lookup"><span data-stu-id="7b991-147">What if I had a Microsoft Monitoring Agent installed on the machine but not as an extension?</span></span>
<span data-ttu-id="7b991-148">如果 Microsoft Monitoring Agent 已經直接安裝在虛擬機器上 (而非作為 Azure 擴充功能)，資訊安全中心不會再安裝 Microsoft Monitoring Agent，且資訊安全監控的功能會受到限制。</span><span class="sxs-lookup"><span data-stu-id="7b991-148">If the Microsoft Monitoring Agent is installed directly on the VM (not as an Azure extension), Security Center will not install the Microsoft Monitoring Agent and security monitoring will be limited.</span></span>

### <a name="what-is-the-impact-of-removing-these-extensions"></a><span data-ttu-id="7b991-149">移除這些擴充功能會有什麼影響？</span><span class="sxs-lookup"><span data-stu-id="7b991-149">What is the impact of removing these extensions?</span></span>
<span data-ttu-id="7b991-150">如果您移除了 Microsoft Monitoring 擴充功能，資訊安全中心會無法收集虛擬機器送出的安全性資料，且特定安全性建議及警示將無法使用。</span><span class="sxs-lookup"><span data-stu-id="7b991-150">If you remove the Microsoft Monitoring Extension, Security Center is not able to collect security data from the VM and some security recommendations and alerts are unavailable.</span></span> <span data-ttu-id="7b991-151">24 小時內，資訊安全中心會判定虛擬機器缺少了擴充功能，並重新安裝。</span><span class="sxs-lookup"><span data-stu-id="7b991-151">Within 24 hours, Security Center determines that the VM is missing the extension and reinstalls the extension.</span></span>

### <a name="how-do-i-stop-the-automatic-agent-installation-and-workspace-creation"></a><span data-ttu-id="7b991-152">我要如何避免自動安裝代理程式和建立工作區？</span><span class="sxs-lookup"><span data-stu-id="7b991-152">How do I stop the automatic agent installation and workspace creation?</span></span>
<span data-ttu-id="7b991-153">您可以在安全性原則中停用訂用帳戶的資料收集，但不建議您這麼做。</span><span class="sxs-lookup"><span data-stu-id="7b991-153">You can turn off data collection for your subscriptions in the security policy but this is not recommended.</span></span> <span data-ttu-id="7b991-154">關閉資料收集會限制資訊安全中心的建議和警示。</span><span class="sxs-lookup"><span data-stu-id="7b991-154">Turning off data collection limits Security Center recommendations and alerts.</span></span> <span data-ttu-id="7b991-155">標準層上的訂用帳戶需要進行資料收集。</span><span class="sxs-lookup"><span data-stu-id="7b991-155">Data collection is required for subscriptions on the Standard pricing tier.</span></span> <span data-ttu-id="7b991-156">若要停用資料收集：</span><span class="sxs-lookup"><span data-stu-id="7b991-156">To disable data collection:</span></span>

1. <span data-ttu-id="7b991-157">如果您的訂用帳戶設定為標準層，請開啟該訂用帳戶的安全性原則，並選取**免費**層。</span><span class="sxs-lookup"><span data-stu-id="7b991-157">If your subscription is configured for the Standard tier, open the security policy for that subscription and select the **Free** tier.</span></span>

   ![定價層 ][1]

2. <span data-ttu-id="7b991-159">接下來請選取 [安全性原則 – 資料收集] 刀鋒視窗上的 [關閉]，來停用資料收集。</span><span class="sxs-lookup"><span data-stu-id="7b991-159">Next, turn off data collection by selecting **Off** on the **Security policy – Data collection** blade.</span></span>

   ![資料收集][2]

### <a name="how-do-i-remove-oms-extensions-installed-by-security-center"></a><span data-ttu-id="7b991-161">我要如何移除資訊安全中心安裝的 OMS 擴充功能？</span><span class="sxs-lookup"><span data-stu-id="7b991-161">How do I remove OMS extensions installed by Security Center?</span></span>
<span data-ttu-id="7b991-162">您可以手動移除 Microsoft Monitoring Agent。</span><span class="sxs-lookup"><span data-stu-id="7b991-162">You can manually remove the Microsoft Monitoring Agent.</span></span> <span data-ttu-id="7b991-163">關閉資料收集會限制資訊安全中心的建議和警示，所以不建議您這麼做。</span><span class="sxs-lookup"><span data-stu-id="7b991-163">This is not recommended as it limits Security Center recommendations and alerts.</span></span>

> [!NOTE]
> <span data-ttu-id="7b991-164">如果已啟用資料收集，資訊安全中心將會在您移除代理程式後重新安裝程式。</span><span class="sxs-lookup"><span data-stu-id="7b991-164">If data collection is enabled, Security Center will reinstall the agent after you remove it.</span></span>  <span data-ttu-id="7b991-165">您必須停用資料收集，再手動移除代理程式。</span><span class="sxs-lookup"><span data-stu-id="7b991-165">You need to disable data collection before manually removing the agent.</span></span> <span data-ttu-id="7b991-166">若要了解如何停用資料收集，請參閱[我要如何避免自動安裝代理程式和建立工作區？](#how-do-i-stop-the-automatic-agent-installation-and-workspace-creation?)</span><span class="sxs-lookup"><span data-stu-id="7b991-166">See [How do I stop the automatic agent installation and workspace creation?](#how-do-i-stop-the-automatic-agent-installation-and-workspace-creation?) for instructions on disabling data collection.</span></span>
>
>

<span data-ttu-id="7b991-167">若要手動移除代理程式：</span><span class="sxs-lookup"><span data-stu-id="7b991-167">To manually remove the agent:</span></span>

1.  <span data-ttu-id="7b991-168">在入口網站中，開啟**Log Analytics**。</span><span class="sxs-lookup"><span data-stu-id="7b991-168">In the portal, open **Log Analytics**.</span></span>
2.  <span data-ttu-id="7b991-169">在 [Log Analytics] 刀鋒視窗中，選取工作區：</span><span class="sxs-lookup"><span data-stu-id="7b991-169">On the Log Analytics blade, select a workspace:</span></span>
3.  <span data-ttu-id="7b991-170">選取您不想監控的虛擬機器，並選取 [中斷連線]。</span><span class="sxs-lookup"><span data-stu-id="7b991-170">Select each VM that you don’t want to monitor and select **Disconnect**.</span></span>

   ![移除代理程式][3]

> [!NOTE]
> <span data-ttu-id="7b991-172">如果 Linux VM 已經有非擴充功能的 OMS 代理程式，移除功能的同時也會移除代理程式，客戶必須要重新安裝。</span><span class="sxs-lookup"><span data-stu-id="7b991-172">If a Linux VM already has a non-extension OMS agent, removing the extension removes the agent as well and the customer has to reinstall it.</span></span>
>
>

## <a name="existing-oms-customers"></a><span data-ttu-id="7b991-173">現有的 OMS 客戶</span><span class="sxs-lookup"><span data-stu-id="7b991-173">Existing OMS customers</span></span>

### <a name="does-security-center-override-any-existing-connections-between-vms-and-workspaces"></a><span data-ttu-id="7b991-174">資訊安全中心是否會覆寫任何虛擬機器及工作區之間現有的連線？</span><span class="sxs-lookup"><span data-stu-id="7b991-174">Does Security Center override any existing connections between VMs and workspaces?</span></span>
<span data-ttu-id="7b991-175">如果虛擬機器已經以擴充功能的形式安裝 Microsoft Monitoring Agent，資訊安全中心不會覆寫既存的工作區連線。</span><span class="sxs-lookup"><span data-stu-id="7b991-175">If a VM already has the Microsoft Monitoring Agent installed as an Azure extension, Security Center does not override the existing workspace connection.</span></span> <span data-ttu-id="7b991-176">相反地，資訊安全中心會使用現有的工作區。</span><span class="sxs-lookup"><span data-stu-id="7b991-176">Instead, Security Center uses the existing workspace.</span></span>

<span data-ttu-id="7b991-177">資訊安全中心解決方案若尚未安裝，此時會安裝至工作區，且此解決方案只會套用至相關的虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="7b991-177">A Security Center solution is installed on the workspace if not present already, and the solution is applied only to the relevant VMs.</span></span> <span data-ttu-id="7b991-178">當您新增解決方案時，依預設會該解決方案會自動部署到與您 Log Analytics 工作區連線的所有 Windows 與 Linux 代理程式。</span><span class="sxs-lookup"><span data-stu-id="7b991-178">When you add a solution, it's automatically deployed by default to all Windows and Linux agents connected to your Log Analytics workspace.</span></span> <span data-ttu-id="7b991-179">[解決方案目標設定](../operations-management-suite/operations-management-suite-solution-targeting.md)是 OMS 的功能，讓您能將範圍套用至解決方案。</span><span class="sxs-lookup"><span data-stu-id="7b991-179">[Solution Targeting](../operations-management-suite/operations-management-suite-solution-targeting.md), which is an OMS feature, allows you to apply a scope to your solutions.</span></span>

<span data-ttu-id="7b991-180">如果 Microsoft Monitoring Agent 已經直接安裝在虛擬機器上 (而非作為 Azure 擴充功能)，資訊安全中心不會再安裝 Microsoft Monitoring Agent，且資訊安全監控的功能會受到限制。</span><span class="sxs-lookup"><span data-stu-id="7b991-180">If the Microsoft Monitoring Agent is installed directly on the VM (not as an Azure extension), Security Center will not install the Microsoft Monitoring Agent and security monitoring is limited.</span></span>

### <a name="what-should-i-do-if-i-suspect-that-the-data-platform-migration-broke-the-connection-between-one-of-my-vms-and-my-workspace"></a><span data-ttu-id="7b991-181">如果我懷疑資料平台移轉中斷了我的工作區及虛擬機器之一的連線，我該怎麼做？</span><span class="sxs-lookup"><span data-stu-id="7b991-181">What should I do if I suspect that the data platform migration broke the connection between one of my VMs and my workspace?</span></span>
<span data-ttu-id="7b991-182">這種情況不應發生。</span><span class="sxs-lookup"><span data-stu-id="7b991-182">This should not happen.</span></span> <span data-ttu-id="7b991-183">如果連線真的中斷了，請[建立一個 Azure 支援要求](../azure-supportability/how-to-create-azure-support-request.md)，並隨附下列詳細資料：</span><span class="sxs-lookup"><span data-stu-id="7b991-183">If it does happen, then [Create an Azure support request](../azure-supportability/how-to-create-azure-support-request.md) and include the following details:</span></span>

- <span data-ttu-id="7b991-184">受影響虛擬機器的 Azure 資源識別碼</span><span class="sxs-lookup"><span data-stu-id="7b991-184">The Azure resource ID of the impacted VM</span></span>
- <span data-ttu-id="7b991-185">工作區連線中斷前，擴充功能所設定之工作區的 Azure 資源識別碼</span><span class="sxs-lookup"><span data-stu-id="7b991-185">The Azure resource ID of the workspace configured on the extension before the connection was broken</span></span>
- <span data-ttu-id="7b991-186">代理程式和先前已安裝的版本</span><span class="sxs-lookup"><span data-stu-id="7b991-186">The agent and version that was previously installed</span></span>

### <a name="does-security-center-install-solutions-on-my-existing-oms-workspaces-what-are-the-billing-implications"></a><span data-ttu-id="7b991-187">資訊安全中心是否會在我現有的 OMS 工作區上安裝解決方案？</span><span class="sxs-lookup"><span data-stu-id="7b991-187">Does Security Center install solutions on my existing OMS workspaces?</span></span> <span data-ttu-id="7b991-188">這會對計費造成什麼影響？</span><span class="sxs-lookup"><span data-stu-id="7b991-188">What are the billing implications?</span></span>
<span data-ttu-id="7b991-189">當資訊安全中心發現已經有虛擬機器連線到您建立的工作區時，資訊安全中心會根據您的定價層啟用此工作區上的解決方案。</span><span class="sxs-lookup"><span data-stu-id="7b991-189">When Security Center identifies that a VM is already connected to a workspace you created, Security Center enables solutions on this workspace according to your pricing tier.</span></span> <span data-ttu-id="7b991-190">這些解決方案會透過[方案目標設定](https://docs.microsoft.com/azure/operations-management-suite/operations-management-suite-solution-targeting)，只套用至相關的 Azure 虛擬機器，所以收費不會改變。</span><span class="sxs-lookup"><span data-stu-id="7b991-190">The solutions are applied only to the relevant Azure VMs, via [solution targeting](https://docs.microsoft.com/azure/operations-management-suite/operations-management-suite-solution-targeting), so the billing remains the same.</span></span>

- <span data-ttu-id="7b991-191">**免費層** – 資訊安全中心在工作區安裝 SecurityCenterFree 解決方案。</span><span class="sxs-lookup"><span data-stu-id="7b991-191">**Free tier** – Security Center installs the 'SecurityCenterFree' solution on the workspace.</span></span> <span data-ttu-id="7b991-192">免費層不須付費。</span><span class="sxs-lookup"><span data-stu-id="7b991-192">You are not billed for the Free tier.</span></span>
- <span data-ttu-id="7b991-193">**標準層** – 資訊安全中心在工作區安裝 SecurityCenterFree 及 Security 解決方案。</span><span class="sxs-lookup"><span data-stu-id="7b991-193">**Standard tier** – Security Center installs the 'SecurityCenterFree' and 'Security' solutions on the workspace.</span></span>

   ![預設工作區的解決方案][4]

> [!NOTE]
> <span data-ttu-id="7b991-195">Log Analytics 中的 Security 解決方案即為 OMS 中的 Security & Audit 解決方案。</span><span class="sxs-lookup"><span data-stu-id="7b991-195">The ‘Security’ solution in Log Analytics is the Security & Audit solution in OMS.</span></span>
>
>

### <a name="i-already-have-workspaces-in-my-environment-can-i-use-them-to-collect-security-data"></a><span data-ttu-id="7b991-196">我的環境中已經有工作區，我是否能使用這些工作區來收集安全性資料？</span><span class="sxs-lookup"><span data-stu-id="7b991-196">I already have workspaces in my environment, can I use them to collect security data?</span></span>
<span data-ttu-id="7b991-197">如果虛擬機器已經以擴充套件的形式安裝 Microsoft Monitoring Agent，資訊安全中心會使用現有已連線的工作區。</span><span class="sxs-lookup"><span data-stu-id="7b991-197">If a VM already has the Microsoft Monitoring Agent installed as an Azure extension, Security Center uses the existing connected workspace.</span></span> <span data-ttu-id="7b991-198">資訊安全中心解決方案若尚未安裝，此時會安裝至工作區，且透過[解決方案目標設定](https://docs.microsoft.com/azure/operations-management-suite/operations-management-suite-solution-targeting)，此解決方案只會套用至相關的虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="7b991-198">A Security Center solution is installed on the workspace if not present already, and the solution is applied only to the relevant VMs via [solution targeting](https://docs.microsoft.com/azure/operations-management-suite/operations-management-suite-solution-targeting).</span></span>

<span data-ttu-id="7b991-199">資訊安全中心在虛擬機器上安裝 Microsoft Monitoring Agent 時，會使用資訊安全中心建立的預設工作區。</span><span class="sxs-lookup"><span data-stu-id="7b991-199">When Security Center installs the Microsoft Monitoring Agent on VMs, it uses the default workspace(s) created by Security Center.</span></span> <span data-ttu-id="7b991-200">不久之後客戶將能自行設定要使用那些工作區。</span><span class="sxs-lookup"><span data-stu-id="7b991-200">Soon customers will be able to configure which workspace(s) are used.</span></span>

### <a name="i-already-have-security-solution-on-my-workspaces-what-are-the-billing-implications"></a><span data-ttu-id="7b991-201">我的工作區上已經有安全性解決方案。</span><span class="sxs-lookup"><span data-stu-id="7b991-201">I already have security solution on my workspaces.</span></span> <span data-ttu-id="7b991-202">這會對計費造成什麼影響？</span><span class="sxs-lookup"><span data-stu-id="7b991-202">What are the billing implications?</span></span>
<span data-ttu-id="7b991-203">Security & Audit 解決方案會用來啟用 Azure 虛擬機器上資訊安全中心標準層的功能。</span><span class="sxs-lookup"><span data-stu-id="7b991-203">The Security & Audit solution is used to enable Security Center Standard tier features for Azure VMs.</span></span> <span data-ttu-id="7b991-204">如果工作區已經安裝有 Security & Audit 解決方案，資訊安全中心會使用現有的解決方案。</span><span class="sxs-lookup"><span data-stu-id="7b991-204">If the Security & Audit solution is already installed on a workspace, Security Center uses the existing solution.</span></span> <span data-ttu-id="7b991-205">收費不會改變。</span><span class="sxs-lookup"><span data-stu-id="7b991-205">There is no change in billing.</span></span>

## <a name="next-steps"></a><span data-ttu-id="7b991-206">後續步驟</span><span class="sxs-lookup"><span data-stu-id="7b991-206">Next steps</span></span>
<span data-ttu-id="7b991-207">若要深入了解資訊安全中心平台移轉，請參閱</span><span class="sxs-lookup"><span data-stu-id="7b991-207">To learn more about the Security Center platform migration, see</span></span>

- [<span data-ttu-id="7b991-208">Azure 資訊安全中心平台移轉</span><span class="sxs-lookup"><span data-stu-id="7b991-208">Azure Security Center Platform Migration</span></span>](security-center-platform-migration.md)
- [<span data-ttu-id="7b991-209">Azure 資訊安全中心疑難排解指南</span><span class="sxs-lookup"><span data-stu-id="7b991-209">Azure Security Center Troubleshooting Guide</span></span>](security-center-troubleshooting-guide.md)

<!--Image references-->
[1]: ./media/security-center-platform-migration-faq/pricing-tier.png
[2]: ./media/security-center-platform-migration-faq/data-collection.png
[3]: ./media/security-center-platform-migration-faq/remove-the-agent.png
[4]: ./media/security-center-platform-migration-faq/solutions.png
