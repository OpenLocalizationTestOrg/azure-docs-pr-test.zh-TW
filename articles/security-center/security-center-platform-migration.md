---
title: "aaaAzure 安全性 Center 平台移轉 |Microsoft 文件"
description: "本文件說明一些 Azure 資訊安全中心資料的變更 toohello 方式收集。"
services: security-center
documentationcenter: na
author: YuriDio
manager: mbaldwin
editor: 
ms.assetid: 80246b00-bdb8-4bbc-af54-06b7d12acf58
ms.service: security-center
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/24/2017
ms.author: yurid
ms.openlocfilehash: 28cb8d85912a3f62941cf113da51070081b5eda2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-security-center-platform-migration"></a><span data-ttu-id="92f23-103">Azure 資訊安全中心平台移轉</span><span class="sxs-lookup"><span data-stu-id="92f23-103">Azure Security Center platform migration</span></span>

<span data-ttu-id="92f23-104">從開始早期年 6 月 2017年，Azure 資訊安全中心中推出收集及儲存資料的變更 toohello 方式安全性很重要。</span><span class="sxs-lookup"><span data-stu-id="92f23-104">Beginning in early June 2017, Azure Security Center rolls out important changes toohello way security data is collected and stored.</span></span>  <span data-ttu-id="92f23-105">這些變更解除鎖定新功能，例如 hello 能力 tooeasily 搜尋安全性資料，並進一步對齊其他 Azure 管理和監視 windows 服務。</span><span class="sxs-lookup"><span data-stu-id="92f23-105">These changes unlock new capabilities like hello ability tooeasily search security data and better aligns with other Azure management and monitoring services.</span></span>

> [!NOTE]
> <span data-ttu-id="92f23-106">hello 平台移轉應該不會影響您實際執行的資源，並不不需要從您的側邊採取任何動作。</span><span class="sxs-lookup"><span data-stu-id="92f23-106">hello platform migration should not impact your production resources, and no action is necessary from your side.</span></span>


## <a name="whats-happening-during-this-platform-migration"></a><span data-ttu-id="92f23-107">在此平台移轉期間發生什麼事？</span><span class="sxs-lookup"><span data-stu-id="92f23-107">What’s happening during this platform migration?</span></span>

<span data-ttu-id="92f23-108">先前的資訊安全中心使用 hello Azure Monitoring Agent toocollect 安全性資料從您的 Vm。</span><span class="sxs-lookup"><span data-stu-id="92f23-108">Previously, Security Center used hello Azure Monitoring Agent toocollect security data from your VMs.</span></span> <span data-ttu-id="92f23-109">這包括安全性組態，也就是使用的 tooidentify 弱點和安全性事件，也就是使用的 toodetect 威脅的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="92f23-109">This includes information about security configurations, which are used tooidentify vulnerabilities, and security events, which are used toodetect threats.</span></span> <span data-ttu-id="92f23-110">此資料會儲存於 Azure 中您的儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="92f23-110">This data was stored in your Storage account(s) in Azure.</span></span>

<span data-ttu-id="92f23-111">這是使用相同的代理程式的 hello Operations Management Suite，記錄分析服務的 hello 接下來，資訊安全中心會使用 Microsoft Monitoring Agent – hello。</span><span class="sxs-lookup"><span data-stu-id="92f23-111">Going forward, Security Center uses hello Microsoft Monitoring Agent – this is hello same agent used by hello Operations Management Suite and Log Analytics service.</span></span> <span data-ttu-id="92f23-112">從這個代理程式收集的資料會儲存在現有*記錄分析*[工作區](../log-analytics/log-analytics-manage-access.md)納入的 hello VM 帳戶 hello 地理位置與您 Azure 訂用帳戶或新 workspace(s)，相關聯.</span><span class="sxs-lookup"><span data-stu-id="92f23-112">Data collected from this agent is stored in either an existing *Log Analytics* [workspace](../log-analytics/log-analytics-manage-access.md) associated with your Azure subscription or a new workspace(s), taking into account hello geolocation of hello VM.</span></span>

## <a name="agent"></a><span data-ttu-id="92f23-113">代理程式</span><span class="sxs-lookup"><span data-stu-id="92f23-113">Agent</span></span>

<span data-ttu-id="92f23-114">Hello 轉換的一部分，hello Microsoft Monitoring Agent (如[Windows](../log-analytics/log-analytics-windows-agents.md)或[Linux](../log-analytics/log-analytics-linux-agents.md)) 從中資料目前未收集所有的 Azure Vm 上已安裝。</span><span class="sxs-lookup"><span data-stu-id="92f23-114">As part of hello transition, hello Microsoft Monitoring Agent (for [Windows](../log-analytics/log-analytics-windows-agents.md) or [Linux](../log-analytics/log-analytics-linux-agents.md)) is installed on all Azure VMs from which data is currently being collected.</span></span>  <span data-ttu-id="92f23-115">如果 VM 已經有 Microsoft Monitoring Agent 安裝，hello hello 資訊安全中心運用 hello 目前安裝代理程式。</span><span class="sxs-lookup"><span data-stu-id="92f23-115">If hello VM already has hello Microsoft Monitoring Agent installed, Security Center leverages hello current installed agent.</span></span>

<span data-ttu-id="92f23-116">一段時間 （通常幾天），這兩個代理程式會執行並存 tooensure 照常平順地轉換資料。</span><span class="sxs-lookup"><span data-stu-id="92f23-116">For a period of time (typically a few days), both agents will run side by side tooensure a smooth transition without any loss of data.</span></span> <span data-ttu-id="92f23-117">這可讓 Microsoft hello 新的資料管線的 toovalidate 可運作之前停止使用 hello 目前的管線。</span><span class="sxs-lookup"><span data-stu-id="92f23-117">This will enable Microsoft toovalidate that hello new data pipeline is operational before discontinuing use of hello current pipeline.</span></span> <span data-ttu-id="92f23-118">一次驗證，hello Azure Monitoring Agent 會移除您的 Vm。</span><span class="sxs-lookup"><span data-stu-id="92f23-118">Once verified, hello Azure Monitoring Agent will be removed from your VMs.</span></span> <span data-ttu-id="92f23-119">您不需要執行任何工作。</span><span class="sxs-lookup"><span data-stu-id="92f23-119">No work is required on your part.</span></span> <span data-ttu-id="92f23-120">所有客戶都已移轉後，系統會以電子郵件通知您。</span><span class="sxs-lookup"><span data-stu-id="92f23-120">An email will notify you when all customers have been migrated.</span></span>
 
<span data-ttu-id="92f23-121">不建議您手動解除 hello Azure Monitoring Agent 安裝 hello 移轉期間因為可能會造成安全性資料中的間距。</span><span class="sxs-lookup"><span data-stu-id="92f23-121">It is not recommended that you manually uninstall hello Azure Monitoring Agent during hello migration as gaps in security data could result.</span></span> <span data-ttu-id="92f23-122">如果您需要進一步協助，請洽詢 [Microsoft 客戶服務與支援中心](https://support.microsoft.com/contactus/)。</span><span class="sxs-lookup"><span data-stu-id="92f23-122">Please consult [Microsoft Customer Service and Support](https://support.microsoft.com/contactus/) if you need further assistance.</span></span> 

<span data-ttu-id="92f23-123">Microsoft Monitoring Agent 的 Windows hello 需要使用 TCP 連接埠 443，讀取[Azure 安全性中心疑難排解指南](security-center-troubleshooting-guide.md)如需詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="92f23-123">hello Microsoft Monitoring Agent for Windows requires use TCP port 443, read [Azure Security Center Troubleshooting Guide](security-center-troubleshooting-guide.md) for more information.</span></span>


> [!NOTE] 
> <span data-ttu-id="92f23-124">Hello Microsoft Monitoring Agent 可能會由其他 Azure 管理和監視服務，hello 代理程式將不會自動解除安裝，因為當您關閉資訊安全中心中的資料收集。</span><span class="sxs-lookup"><span data-stu-id="92f23-124">Because hello Microsoft Monitoring Agent may be used by other Azure management and monitoring services, hello agent will not be uninstalled automatically when you turn off data collection in Security Center.</span></span> <span data-ttu-id="92f23-125">不過，您可以手動解除安裝 hello 代理程式所需。</span><span class="sxs-lookup"><span data-stu-id="92f23-125">However, you can manually uninstall hello agent if needed.</span></span>

## <a name="workspace"></a><span data-ttu-id="92f23-126">工作區</span><span class="sxs-lookup"><span data-stu-id="92f23-126">Workspace</span></span>

<span data-ttu-id="92f23-127">先前所述，從 Microsoft Monitoring Agent （代表 Security Center) 會儲存在現有記錄分析的 hello 收集的資料與您 Azure 訂用帳戶或新 workspace(s)，納入帳戶 hello workspace(s) 相關聯hello VM 的地理位置。</span><span class="sxs-lookup"><span data-stu-id="92f23-127">As described previously, data collected from hello Microsoft Monitoring Agent (on behalf of Security Center) are stored in either an existing Log Analytics workspace(s) associated with your Azure subscription or a new workspace(s), taking into account hello geolocation of hello VM.</span></span>

<span data-ttu-id="92f23-128">在 hello Azure 入口網站，您可以瀏覽 toosee 記錄分析工作區，包括任何資訊安全中心所建立的清單。</span><span class="sxs-lookup"><span data-stu-id="92f23-128">In hello Azure portal, you can browse toosee a list of your Log Analytics workspaces, including any created by Security Center.</span></span> <span data-ttu-id="92f23-129">將會針對新的工作區建立相關的資源群組。</span><span class="sxs-lookup"><span data-stu-id="92f23-129">A related resource group will be created for new workspaces.</span></span> <span data-ttu-id="92f23-130">兩者都會遵循此命名慣例：</span><span class="sxs-lookup"><span data-stu-id="92f23-130">Both follow this naming convention:</span></span>

- <span data-ttu-id="92f23-131">工作區：*DefaultWorkspace-[subscription-ID]-[geo]*</span><span class="sxs-lookup"><span data-stu-id="92f23-131">Workspace: *DefaultWorkspace-[subscription-ID]-[geo]*</span></span>
- <span data-ttu-id="92f23-132">資源群組：*DefaultResouceGroup-[geo]*</span><span class="sxs-lookup"><span data-stu-id="92f23-132">Resource Group: *DefaultResouceGroup-[geo]*</span></span> 
 
<span data-ttu-id="92f23-133">若為資訊安全中心所建立的工作區，資料會保留 30 天。</span><span class="sxs-lookup"><span data-stu-id="92f23-133">For workspaces created by Security Center, data is retained for 30 days.</span></span> <span data-ttu-id="92f23-134">保留現有的工作區，根據 hello 工作區的定價層。</span><span class="sxs-lookup"><span data-stu-id="92f23-134">For existing workspaces, retention is based on hello workspace pricing tier.</span></span>

> [!NOTE]
> <span data-ttu-id="92f23-135">資訊安全中心先前收集的資料會保留在儲存體帳戶中。</span><span class="sxs-lookup"><span data-stu-id="92f23-135">Data previously collected by Security Center remains in your Storage account(s).</span></span> <span data-ttu-id="92f23-136">Hello 移轉完成之後，您可以刪除這些儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="92f23-136">After hello migration is complete, you can delete these Storage accounts.</span></span>

### <a name="oms-security-solution"></a><span data-ttu-id="92f23-137">OMS 安全性解決方案</span><span class="sxs-lookup"><span data-stu-id="92f23-137">OMS Security Solution</span></span> 

<span data-ttu-id="92f23-138">對於未安裝 OMS 安全性解決方案的現有客戶，Microsoft 會安裝在其工作區上，但是僅以 Azure VM 為目標。</span><span class="sxs-lookup"><span data-stu-id="92f23-138">For existing customers that don’t have OMS Security solution installed, Microsoft is installing it on their workspace, but targeting only Azure VMs.</span></span> <span data-ttu-id="92f23-139">請勿解除安裝此解決方案，因為如果從 OMS 管理主控台進行此動作，就沒有任何自動補救方式。</span><span class="sxs-lookup"><span data-stu-id="92f23-139">Do not uninstall this solution, as there is no automatic remediation if this is done from OMS management console.</span></span>


## <a name="other-updates"></a><span data-ttu-id="92f23-140">其他更新</span><span class="sxs-lookup"><span data-stu-id="92f23-140">Other updates</span></span>

<span data-ttu-id="92f23-141">搭配 hello 平台移轉，我們會推出一些額外的次要更新：</span><span class="sxs-lookup"><span data-stu-id="92f23-141">In conjunction with hello platform migration, we are rolling out some additional minor updates:</span></span>

- <span data-ttu-id="92f23-142">將支援其他作業系統版本。</span><span class="sxs-lookup"><span data-stu-id="92f23-142">Additional OS versions will be supported.</span></span> <span data-ttu-id="92f23-143">請參閱 hello 清單[這裡](security-center-faq.md#virtual-machines)。</span><span class="sxs-lookup"><span data-stu-id="92f23-143">See hello list [here](security-center-faq.md#virtual-machines).</span></span>
- <span data-ttu-id="92f23-144">作業系統弱點的 hello 清單將會展開。</span><span class="sxs-lookup"><span data-stu-id="92f23-144">hello list of OS vulnerabilities will be expanded.</span></span> <span data-ttu-id="92f23-145">請參閱 hello 清單[這裡](https://gallery.technet.microsoft.com/Azure-Security-Center-a789e335)。</span><span class="sxs-lookup"><span data-stu-id="92f23-145">See hello list [here](https://gallery.technet.microsoft.com/Azure-Security-Center-a789e335).</span></span>
- <span data-ttu-id="92f23-146">[價格](https://azure.microsoft.com/pricing/details/security-center/)將會按小時 (先前按日) 計算，這可讓某些客戶節省成本。</span><span class="sxs-lookup"><span data-stu-id="92f23-146">[Pricing](https://azure.microsoft.com/pricing/details/security-center/) will be pro-rated hourly (previously it was daily), which will result in cost savings for some customers.</span></span>
- <span data-ttu-id="92f23-147">將所需資料收集，並自動啟用的客戶 hello 標準定價層。</span><span class="sxs-lookup"><span data-stu-id="92f23-147">Data Collection will be required and automatically enabled for customers on hello Standard pricing tier.</span></span>
- <span data-ttu-id="92f23-148">Azure 資訊安全中心將開始探索未透過 Azure 擴充功能部署的反惡意程式碼解決方案。</span><span class="sxs-lookup"><span data-stu-id="92f23-148">Azure Security Center will begin discovering antimalware solutions that were not deployed via Azure extensions.</span></span> <span data-ttu-id="92f23-149">將會首先探索 Symantec Endpoint Protection 和 Defender for Windows 2016。</span><span class="sxs-lookup"><span data-stu-id="92f23-149">Discovery of Symantec Endpoint Protection and Defender for Windows 2016 will be available first.</span></span>
- <span data-ttu-id="92f23-150">洩防護原則和通知只可在 hello 設定*訂用帳戶*層級，但定價仍然可以設定在 hello*資源群組*層級</span><span class="sxs-lookup"><span data-stu-id="92f23-150">Prevention policies and notifications are only configurable at hello *Subscription* level, but pricing can still be set at hello *Resource Group* level</span></span>

