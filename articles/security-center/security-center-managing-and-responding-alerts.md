---
title: "在 Azure 資訊安全中心 aaaManage 安全性警示 |Microsoft 文件"
description: "這份文件可協助您 toouse Azure 資訊安全中心功能 toomanage，以及回應 toosecurity 警示。"
services: security-center
documentationcenter: na
author: YuriDio
manager: mbaldwin
editor: 
ms.assetid: b88a8df7-6979-479b-8039-04da1b8737a7
ms.service: security-center
ms.topic: hero-article
ms.devlang: na
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/19/2017
ms.author: yurid
ms.openlocfilehash: f1cb7e4770776827b75ed15893914678c1f44216
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="managing-and-responding-toosecurity-alerts-in-azure-security-center"></a><span data-ttu-id="db7c0-103">管理及回應 toosecurity Azure 資訊安全中心警示</span><span class="sxs-lookup"><span data-stu-id="db7c0-103">Managing and responding toosecurity alerts in Azure Security Center</span></span>
<span data-ttu-id="db7c0-104">這份文件可協助您使用 Azure 資訊安全中心 toomanage 和回應 toosecurity 警示。</span><span class="sxs-lookup"><span data-stu-id="db7c0-104">This document helps you use Azure Security Center toomanage and respond toosecurity alerts.</span></span>

> [!NOTE]
> <span data-ttu-id="db7c0-105">升級 tooAzure 安全性 Center 標準 tooenable 進階偵測。</span><span class="sxs-lookup"><span data-stu-id="db7c0-105">tooenable advanced detections, upgrade tooAzure Security Center Standard.</span></span> <span data-ttu-id="db7c0-106">提供 60 天的免費試用。</span><span class="sxs-lookup"><span data-stu-id="db7c0-106">A free 60-day trial is available.</span></span> <span data-ttu-id="db7c0-107">tooupgrade，選取定價層 hello[安全性原則](security-center-policies.md)。</span><span class="sxs-lookup"><span data-stu-id="db7c0-107">tooupgrade, select Pricing Tier in hello [Security Policy](security-center-policies.md).</span></span> <span data-ttu-id="db7c0-108">請參閱[Azure 資訊安全中心定價](security-center-pricing.md)toolearn 更多。</span><span class="sxs-lookup"><span data-stu-id="db7c0-108">See [Azure Security Center pricing](security-center-pricing.md) toolearn more.</span></span>
>
>

## <a name="what-are-security-alerts"></a><span data-ttu-id="db7c0-109">什麼是安全性警示：</span><span class="sxs-lookup"><span data-stu-id="db7c0-109">What are security alerts?</span></span>
<span data-ttu-id="db7c0-110">資訊安全中心會自動收集、 分析時，整合記錄資料從您的 Azure 資源，hello 網路和連接協力廠商解決方案，例如防火牆和 endpoint protection 解決方案，toodetect 威脅，並且減少誤判。</span><span class="sxs-lookup"><span data-stu-id="db7c0-110">Security Center automatically collects, analyzes, and integrates log data from your Azure resources, hello network, and connected partner solutions, like firewall and endpoint protection solutions, toodetect real threats and reduce false positives.</span></span> <span data-ttu-id="db7c0-111">優先順序的安全性警示的清單會顯示在資訊安全中心，以及 hello 資訊需要 tooquickly 調查 hello 問題，並建議如何 tooremediate 攻擊。</span><span class="sxs-lookup"><span data-stu-id="db7c0-111">A list of prioritized security alerts is shown in Security Center along with hello information you need tooquickly investigate hello problem and recommendations for how tooremediate an attack.</span></span>


> [!NOTE]
> <span data-ttu-id="db7c0-112">如需資訊安全中心偵測功能運作方式的詳細資訊，請閱讀 [Azure 資訊安全中心的偵測功能](security-center-detection-capabilities.md)。</span><span class="sxs-lookup"><span data-stu-id="db7c0-112">For more information about how Security Center detection capabilities work, read [Azure Security Center Detection Capabilities](security-center-detection-capabilities.md).</span></span>
>
>

## <a name="managing-security-alerts"></a><span data-ttu-id="db7c0-113">管理安全性警示</span><span class="sxs-lookup"><span data-stu-id="db7c0-113">Managing security alerts</span></span>
<span data-ttu-id="db7c0-114">您可以檢閱您目前的警示，藉由查看 hello**安全性警示**磚。</span><span class="sxs-lookup"><span data-stu-id="db7c0-114">You can review your current alerts by looking at hello **Security alerts** tile.</span></span> <span data-ttu-id="db7c0-115">開啟 Azure 入口網站，並遵循下方 toosee hello 步驟有關每種警示的更多詳細資料：</span><span class="sxs-lookup"><span data-stu-id="db7c0-115">Open Azure Portal and follow hello steps below toosee more details about each alert:</span></span>

1. <span data-ttu-id="db7c0-116">在 hello 資訊安全中心儀表板中，您會看到 hello**安全性警示**磚。</span><span class="sxs-lookup"><span data-stu-id="db7c0-116">On hello Security Center dashboard, you will see hello **Security alerts** tile.</span></span>

    ![資訊安全中心的 [安全性警示] 圖格](./media/security-center-managing-and-responding-alerts/security-center-managing-and-responding-alerts-fig1-ga.png)

2. <span data-ttu-id="db7c0-118">按一下 hello 磚 tooopen hello**安全性警示**刀鋒視窗，其中包含更多詳細 hello 警示如下所示。</span><span class="sxs-lookup"><span data-stu-id="db7c0-118">Click hello tile tooopen hello **Security alerts** blade that contains more details about hello alerts as shown below.</span></span>

   ![hello 安全性警示 刀鋒視窗中的資訊安全中心](./media/security-center-managing-and-responding-alerts/security-center-managing-and-responding-alerts-fig2-ga.png)

<span data-ttu-id="db7c0-120">在 hello 此刀鋒視窗的下半部是 hello 每個警示的詳細資料。</span><span class="sxs-lookup"><span data-stu-id="db7c0-120">In hello bottom part of this blade are hello details for each alert.</span></span> <span data-ttu-id="db7c0-121">toosort，按一下您想要依 toosort hello 資料行。</span><span class="sxs-lookup"><span data-stu-id="db7c0-121">toosort, click hello column that you want toosort by.</span></span> <span data-ttu-id="db7c0-122">每個資料行的 hello 定義如下所示：</span><span class="sxs-lookup"><span data-stu-id="db7c0-122">hello definition for each column is given below:</span></span>

* <span data-ttu-id="db7c0-123">**描述**: hello 警示的簡短說明。</span><span class="sxs-lookup"><span data-stu-id="db7c0-123">**Description**: A brief explanation of hello alert.</span></span>
* <span data-ttu-id="db7c0-124">**計數**：在特定一天偵測到這個特定類型的所有警示清單。</span><span class="sxs-lookup"><span data-stu-id="db7c0-124">**Count**: A list of all alerts of this specific type that were detected on a specific day.</span></span>
* <span data-ttu-id="db7c0-125">**偵測到**: hello 負責觸發 hello 警示的服務。</span><span class="sxs-lookup"><span data-stu-id="db7c0-125">**Detected by**: hello service that was responsible for triggering hello alert.</span></span>
* <span data-ttu-id="db7c0-126">**日期**: hello 日期 hello 事件發生。</span><span class="sxs-lookup"><span data-stu-id="db7c0-126">**Date**: hello date that hello event occurred.</span></span>
* <span data-ttu-id="db7c0-127">**狀態**: hello 該警示的目前狀態。</span><span class="sxs-lookup"><span data-stu-id="db7c0-127">**State**: hello current state for that alert.</span></span> <span data-ttu-id="db7c0-128">狀態分為兩種：</span><span class="sxs-lookup"><span data-stu-id="db7c0-128">There are two types of states:</span></span>
  * <span data-ttu-id="db7c0-129">**Active**： 已偵測到 hello 安全性警示。</span><span class="sxs-lookup"><span data-stu-id="db7c0-129">**Active**: hello security alert has been detected.</span></span>
* <span data-ttu-id="db7c0-130">**嚴重性**: hello 嚴重性層級，它可以是高、 中或低。</span><span class="sxs-lookup"><span data-stu-id="db7c0-130">**Severity**: hello severity level, which can be high, medium or low.</span></span>

### <a name="filtering-alerts"></a><span data-ttu-id="db7c0-131">篩選警示</span><span class="sxs-lookup"><span data-stu-id="db7c0-131">Filtering alerts</span></span>
<span data-ttu-id="db7c0-132">您可以根據日期、狀態及嚴重性來篩選警示。</span><span class="sxs-lookup"><span data-stu-id="db7c0-132">You can filter alerts based on date, state, and severity.</span></span> <span data-ttu-id="db7c0-133">篩選警示可用於案例中您需要的安全性警示顯示 toonarrow hello 範圍。</span><span class="sxs-lookup"><span data-stu-id="db7c0-133">Filtering alerts can be useful for scenarios where you need toonarrow hello scope of security alerts show.</span></span> <span data-ttu-id="db7c0-134">例如，可能您想 tooaddress 就會發生在 hello 過去 24 小時您正在調查可能違反 hello 系統中的安全性警示。</span><span class="sxs-lookup"><span data-stu-id="db7c0-134">For example, you might you want tooaddress security alerts that occurred in hello last 24 hours because you are investigating a potential breach in hello system.</span></span>

1. <span data-ttu-id="db7c0-135">按一下**篩選**上 hello**安全性警示**刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="db7c0-135">Click **Filter** on hello **Security Alerts** blade.</span></span> <span data-ttu-id="db7c0-136">hello**篩選**刀鋒視窗會開啟，並選取您想 toosee hello 日期、 狀態和嚴重性值。</span><span class="sxs-lookup"><span data-stu-id="db7c0-136">hello **Filter** blade opens and you select hello date, state, and severity values you wish toosee.</span></span>

    ![篩選資訊安全中心的警示](./media/security-center-managing-and-responding-alerts/security-center-managing-and-responding-alerts-fig3-2017.png)

### <a name="respond-toosecurity-alerts"></a><span data-ttu-id="db7c0-138">回應 toosecurity 警示</span><span class="sxs-lookup"><span data-stu-id="db7c0-138">Respond toosecurity alerts</span></span>
<span data-ttu-id="db7c0-139">選取 安全性警示 toolearn hello 事件觸發 hello 警示，以及項目，如果有的話會引導您有關需要 tootake tooremediate 攻擊。</span><span class="sxs-lookup"><span data-stu-id="db7c0-139">Select a security alert toolearn more about hello event(s) that triggered hello alert and what, if any, steps you need tootake tooremediate an attack.</span></span> <span data-ttu-id="db7c0-140">安全性警示會依類型及日期區分。</span><span class="sxs-lookup"><span data-stu-id="db7c0-140">Security alerts are grouped by type and date.</span></span> <span data-ttu-id="db7c0-141">按一下 安全性警示，會開啟刀鋒視窗中包含的 hello 分組警示清單。</span><span class="sxs-lookup"><span data-stu-id="db7c0-141">Clicking a security alert will open a blade containing a list of hello grouped alerts.</span></span>

![回應 toosecurity Azure 資訊安全中心警示](./media/security-center-managing-and-responding-alerts/security-center-managing-and-responding-alerts-fig5-ga.png)

<span data-ttu-id="db7c0-143">在此情況下，所觸發的 hello 警示，請參閱 toosuspicious 遠端桌面通訊協定 (RDP) 活動。</span><span class="sxs-lookup"><span data-stu-id="db7c0-143">In this case, hello alerts that were triggered refer toosuspicious Remote Desktop Protocol (RDP) activity.</span></span> <span data-ttu-id="db7c0-144">hello 第一個資料行顯示的受攻擊的資源;hello 第二個顯示多少次 hello 資源遭到攻擊。hello 第三個 hello 時間顯示 hello 攻擊。hello 第四個顯示 hello 警示; 狀態並 hello 第五個顯示 hello 嚴重性 hello 攻擊。</span><span class="sxs-lookup"><span data-stu-id="db7c0-144">hello first column shows which resources were attacked; hello second shows how many times hello resource was attacked; hello third shows hello time of hello attack; hello fourth shows state of hello alert; and hello fifth shows hello severity of hello attack.</span></span> <span data-ttu-id="db7c0-145">檢閱此資訊之後，按一下 遭到攻擊的 hello 資源，並且會在開啟的新刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="db7c0-145">After reviewing this information, click hello resource that was attacked and a new blade will open.</span></span>

![Azure 資訊安全中心中的哪些 toodo 安全性的相關警示的建議](./media/security-center-managing-and-responding-alerts/security-center-managing-and-responding-alerts-fig6-ga.png)

<span data-ttu-id="db7c0-147">在 hello**描述**欄位的這個刀鋒視窗中您會發現此事件的詳細。</span><span class="sxs-lookup"><span data-stu-id="db7c0-147">In hello **Description** field of this blade you will find more details about this event.</span></span> <span data-ttu-id="db7c0-148">適用的 hello 來源 IP 位址，以及如何提出建議時，這些額外的詳細資料提供深入了解哪些 hello 觸發的安全性警示，hello 目標資源，tooremediate。</span><span class="sxs-lookup"><span data-stu-id="db7c0-148">These additional details offer insight into what triggered hello security alert, hello target resource, when applicable hello source IP address, and recommendations about how tooremediate.</span></span>  <span data-ttu-id="db7c0-149">在某些情況下，hello 來源 IP 位址會是空的 （不適用） 因為並非所有的 Windows 安全性事件記錄檔包含 hello IP 位址。</span><span class="sxs-lookup"><span data-stu-id="db7c0-149">In some instances, hello source IP address will be empty (not available) because not all Windows security events logs include hello IP address.</span></span>

<span data-ttu-id="db7c0-150">資訊安全中心所建議的 hello 補救異相應 toohello 安全性警示。</span><span class="sxs-lookup"><span data-stu-id="db7c0-150">hello remediation suggested by Security Center will vary according toohello security alert.</span></span> <span data-ttu-id="db7c0-151">在某些情況下，您可能會有 toouse 其他的 Azure 功能 tooimplement hello 建議補救。</span><span class="sxs-lookup"><span data-stu-id="db7c0-151">In some cases, you may have toouse other Azure capabilities tooimplement hello recommended remediation.</span></span> <span data-ttu-id="db7c0-152">這種攻擊是 tooblacklist hello IP 位址，使用產生這種攻擊，例如 hello 補救[網路 ACL](../virtual-network/virtual-networks-acl.md)或[網路安全性群組](../virtual-network/virtual-networks-nsg.md)規則。</span><span class="sxs-lookup"><span data-stu-id="db7c0-152">For example, hello remediation for this attack is tooblacklist hello IP address that is generating this attack by using a [network ACL](../virtual-network/virtual-networks-acl.md) or a [network security group](../virtual-network/virtual-networks-nsg.md) rule.</span></span>

> [!NOTE]
> <span data-ttu-id="db7c0-153">Hello 不同類型警示的詳細資訊，請參閱[Azure 資訊安全中心中的型別安全性警示](security-center-alerts-type.md)。</span><span class="sxs-lookup"><span data-stu-id="db7c0-153">For more information on hello different types of alerts, read [Security Alerts by Type in Azure Security Center](security-center-alerts-type.md).</span></span>
>
>

## <a name="see-also"></a><span data-ttu-id="db7c0-154">另請參閱</span><span class="sxs-lookup"><span data-stu-id="db7c0-154">See also</span></span>
<span data-ttu-id="db7c0-155">在本文件中，您學到如何 tooconfigure 資訊安全中心的安全性原則。</span><span class="sxs-lookup"><span data-stu-id="db7c0-155">In this document, you learned how tooconfigure security policies in Security Center.</span></span> <span data-ttu-id="db7c0-156">toolearn 有關資訊安全中心的詳細資訊，請參閱 hello 下列資訊：</span><span class="sxs-lookup"><span data-stu-id="db7c0-156">toolearn more about Security Center, see hello following:</span></span>

* [<span data-ttu-id="db7c0-157">在 Azure 資訊安全中心處理安全性事件</span><span class="sxs-lookup"><span data-stu-id="db7c0-157">Handling Security Incident in Azure Security Center</span></span>](security-center-incident.md)
* [<span data-ttu-id="db7c0-158">Azure 資訊安全中心的偵測功能</span><span class="sxs-lookup"><span data-stu-id="db7c0-158">Azure Security Center Detection Capabilities</span></span>](security-center-detection-capabilities.md)
* [<span data-ttu-id="db7c0-159">Azure 資訊安全中心規劃和操作指南</span><span class="sxs-lookup"><span data-stu-id="db7c0-159">Azure Security Center Planning and Operations Guide</span></span>](security-center-planning-and-operations-guide.md)
* <span data-ttu-id="db7c0-160">[Azure 資訊安全中心常見問題集](security-center-faq.md)— 尋找使用 hello 服務相關的常見問題集。</span><span class="sxs-lookup"><span data-stu-id="db7c0-160">[Azure Security Center FAQ](security-center-faq.md) — Find frequently asked questions about using hello service.</span></span>
* <span data-ttu-id="db7c0-161">[Azure 安全性部落格](http://blogs.msdn.com/b/azuresecurity/) — 尋找有關 Azure 安全性與相容性的部落格文章。</span><span class="sxs-lookup"><span data-stu-id="db7c0-161">[Azure Security blog](http://blogs.msdn.com/b/azuresecurity/) — Find blog posts about Azure security and compliance.</span></span>
