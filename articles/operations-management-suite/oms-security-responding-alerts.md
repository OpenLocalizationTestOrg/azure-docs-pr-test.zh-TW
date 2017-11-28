---
title: "aaaMonitoring 及回應 tooSecurity 警示在 Operations Management Suite 安全性和稽核解決方案 |Microsoft 文件"
description: "這份文件可協助您 toouse hello 威脅情報選項可以在 OMS 安全性和稽核 toomonitor，以及回應 toosecurity 警示。"
services: operations-management-suite
documentationcenter: na
author: YuriDio
manager: mbaldwin
editor: 
ms.assetid: 7d45a32b-1341-4bb5-a436-1f42a8a2590a
ms.service: operations-management-suite
ms.custom: oms-security
ms.topic: article
ms.devlang: na
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/13/2017
ms.author: yurid
ms.openlocfilehash: 3d92b6809b7bd934c889afc119e5e34ff2b85f1b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="monitoring-and-responding-toosecurity-alerts-in-operations-management-suite-security-and-audit-solution"></a><span data-ttu-id="461a9-103">監視及回應 toosecurity Operations Management Suite 安全性和稽核 」 解決方案中的警示</span><span class="sxs-lookup"><span data-stu-id="461a9-103">Monitoring and responding toosecurity alerts in Operations Management Suite Security and Audit Solution</span></span>
<span data-ttu-id="461a9-104">這份文件可協助您使用 hello 威脅情報選項可以在 OMS 安全性和稽核 toomonitor 和回應 toosecurity 警示。</span><span class="sxs-lookup"><span data-stu-id="461a9-104">This document helps you use hello threat intelligence option available in OMS Security and Audit toomonitor and respond toosecurity alerts.</span></span>

## <a name="what-is-oms"></a><span data-ttu-id="461a9-105">何謂 OMS？</span><span class="sxs-lookup"><span data-stu-id="461a9-105">What is OMS?</span></span>
<span data-ttu-id="461a9-106">Microsoft Operations Management Suite (OMS) 是 Microsoft 的雲端型 IT 管理解決方案，可協助您管理並保護內部部署和雲端基礎結構。</span><span class="sxs-lookup"><span data-stu-id="461a9-106">Microsoft Operations Management Suite (OMS) is Microsoft's cloud based IT management solution that helps you manage and protect your on-premises and cloud infrastructure.</span></span> <span data-ttu-id="461a9-107">關於 OMS 的詳細資訊，請參閱 hello 文章[Operations Management Suite](https://technet.microsoft.com/library/mt484091.aspx)。</span><span class="sxs-lookup"><span data-stu-id="461a9-107">For more information about OMS, read hello article [Operations Management Suite](https://technet.microsoft.com/library/mt484091.aspx).</span></span>

## <a name="threat-intelligence"></a><span data-ttu-id="461a9-108">威脅情報</span><span class="sxs-lookup"><span data-stu-id="461a9-108">Threat intelligence</span></span>
<span data-ttu-id="461a9-109">在企業環境中使用者廣泛存取 toohello 網路，並使用各種裝置 tooconnect toocorporate 資料，請務必您可以主動監視您的資源和快速回應 toosecurity 事件。</span><span class="sxs-lookup"><span data-stu-id="461a9-109">In an enterprise environment where users have broad access toohello network and use a variety of devices tooconnect toocorporate data, it is imperative that you can actively monitor your resources and quickly respond toosecurity incidents.</span></span> <span data-ttu-id="461a9-110">這是重要的觀點 hello 安全性開發週期因為某些顧慮威脅可能不會引發警示的特定或傳統的安全性技術控制項可以識別的可疑活動。</span><span class="sxs-lookup"><span data-stu-id="461a9-110">This is particular important from hello security lifecycle perspective because some cybersecurity threats may not raise alerts or suspicious activities that can be identified by traditional security technical controls.</span></span> 

<span data-ttu-id="461a9-111">使用 hello**威脅情報**選項可在 OMS 安全性和稽核，IT 系統管理員可以識別針對 hello 環境的安全性威脅，例如，識別特定的電腦是否屬於[殭屍網路](https://www.microsoft.com/security/sir/story/default.aspx#!botnetsection)。</span><span class="sxs-lookup"><span data-stu-id="461a9-111">By using hello **Threat Intelligence** option available in OMS Security and Audit, IT administrators can identify security threats against hello environment, for example, identify if a particular computer is part of a [botnet](https://www.microsoft.com/security/sir/story/default.aspx#!botnetsection).</span></span> <span data-ttu-id="461a9-112">當攻擊者非法地安裝惡意軟體偷偷地連接此電腦 toohello 命令和控制項時，電腦可能會變成殭屍網路中的節點。</span><span class="sxs-lookup"><span data-stu-id="461a9-112">Computers can become nodes in a botnet when attackers illicitly install malware that secretly connects this computer toohello command and control.</span></span> <span data-ttu-id="461a9-113">它也可以識別來自地下通訊通道 (例如 [暗網](https://www.microsoft.com/security/sir/story/default.aspx#!botnetsection_honeypots_darkents)) 的潛在威脅。</span><span class="sxs-lookup"><span data-stu-id="461a9-113">It can also identify potential threats coming from underground communication channels, such as [darknet](https://www.microsoft.com/security/sir/story/default.aspx#!botnetsection_honeypots_darkents).</span></span> 

<span data-ttu-id="461a9-114">在順序 toobuild 這個威脅情報 OMS 安全性和稽核，請使用來自 Microsoft 內部的多個來源的資料。</span><span class="sxs-lookup"><span data-stu-id="461a9-114">In order toobuild this threat intelligence, OMS Security and Audit use data coming from multiple sources within Microsoft.</span></span> <span data-ttu-id="461a9-115">OMS 安全性和稽核將會利用這個資料 tooidentify 潛在的威脅攻擊的環境。</span><span class="sxs-lookup"><span data-stu-id="461a9-115">OMS Security and Audit will leverage this data tooidentify potential threats against your environment.</span></span>

<span data-ttu-id="461a9-116">hello 威脅情報窗格是由三個主要選項所組成：</span><span class="sxs-lookup"><span data-stu-id="461a9-116">hello Threat Intelligence pane is composed by three major options:</span></span>

* <span data-ttu-id="461a9-117">具有輸出惡意流量的伺服器</span><span class="sxs-lookup"><span data-stu-id="461a9-117">Servers with outbound malicious traffic</span></span>
* <span data-ttu-id="461a9-118">偵測到的威脅類型</span><span class="sxs-lookup"><span data-stu-id="461a9-118">Detected threats types</span></span>
* <span data-ttu-id="461a9-119">威脅情報對應</span><span class="sxs-lookup"><span data-stu-id="461a9-119">Threat intelligence map</span></span>

> [!NOTE]
> <span data-ttu-id="461a9-120">如需所有這些選項的概觀，請參閱 [開始使用 Operations Management Suite 安全性和稽核解決方案](oms-security-getting-started.md)。</span><span class="sxs-lookup"><span data-stu-id="461a9-120">for an overview of all these options, read [Getting started with Operations Management Suite Security and Audit Solution](oms-security-getting-started.md).</span></span>
> 
> 

### <a name="responding-toosecurity-alerts"></a><span data-ttu-id="461a9-121">回應 toosecurity 警示</span><span class="sxs-lookup"><span data-stu-id="461a9-121">Responding toosecurity alerts</span></span>
<span data-ttu-id="461a9-122">其中一個的 hello 步驟[安全性事件回應](https://technet.microsoft.com/library/cc512623.aspx)程序是 tooidentify hello 嚴重性 hello 危害系統。</span><span class="sxs-lookup"><span data-stu-id="461a9-122">One of hello steps of a [security incident response](https://technet.microsoft.com/library/cc512623.aspx) process is tooidentify hello severity of hello compromise system(s).</span></span> <span data-ttu-id="461a9-123">在這個階段您應該執行下列工作的 hello:</span><span class="sxs-lookup"><span data-stu-id="461a9-123">In this phase you should perform hello following tasks:</span></span>

* <span data-ttu-id="461a9-124">判斷 hello 攻擊的 hello 本質</span><span class="sxs-lookup"><span data-stu-id="461a9-124">Determine hello nature of hello attack</span></span>
* <span data-ttu-id="461a9-125">判斷 hello 的原點的攻擊點。</span><span class="sxs-lookup"><span data-stu-id="461a9-125">Determine hello attack point of origin</span></span>
* <span data-ttu-id="461a9-126">判斷 hello 攻擊的 hello 意圖。</span><span class="sxs-lookup"><span data-stu-id="461a9-126">Determine hello intent of hello attack.</span></span> <span data-ttu-id="461a9-127">Hello 攻擊是直接在您的組織 tooacquire 的特定資訊，或是它隨機嗎？</span><span class="sxs-lookup"><span data-stu-id="461a9-127">Was hello attack specifically directed at your organization tooacquire specific information, or was it random?</span></span>
* <span data-ttu-id="461a9-128">識別已受到危害的 hello 系統</span><span class="sxs-lookup"><span data-stu-id="461a9-128">Identify hello systems that have been compromised</span></span>
* <span data-ttu-id="461a9-129">識別已存取，並判斷那些檔案的 hello 敏感度的 hello 檔案</span><span class="sxs-lookup"><span data-stu-id="461a9-129">Identify hello files that have been accessed and determine hello sensitivity of those files</span></span>

<span data-ttu-id="461a9-130">您可以利用**威脅情報**OMS 安全性和稽核解決方案 toohelp 這些工作中的資訊。</span><span class="sxs-lookup"><span data-stu-id="461a9-130">You can leverage **Threat Intelligence** information in OMS Security and Audit solution toohelp with these tasks.</span></span> <span data-ttu-id="461a9-131">請遵循以下 tooaccess hello 步驟這**威脅情報**選項：</span><span class="sxs-lookup"><span data-stu-id="461a9-131">Follow hello steps below tooaccess this **Threat Intelligence** options:</span></span>

1. <span data-ttu-id="461a9-132">在 hello **Microsoft Operations Management Suite**主要儀表板按一下**安全性和稽核**磚。</span><span class="sxs-lookup"><span data-stu-id="461a9-132">In hello **Microsoft Operations Management Suite** main dashboard click **Security and Audit** tile.</span></span>
   
    ![安全性和稽核](./media/oms-security-responding-alerts/oms-security-responding-alerts-fig1.png)
2. <span data-ttu-id="461a9-134">在 hello**安全性和稽核**儀表板，您會看到 hello**威脅情報**hello 方選項，如下所示：</span><span class="sxs-lookup"><span data-stu-id="461a9-134">In hello **Security and Audit** dashboard, you will see hello **Threat Intelligence** options in hello right, as shown below:</span></span>
   
    ![威脅情報](./media/oms-security-responding-alerts/oms-security-responding-alerts-fig2-ga.png)

<span data-ttu-id="461a9-136">這些三個磚會提供您的 hello 潛在威脅的概觀。</span><span class="sxs-lookup"><span data-stu-id="461a9-136">These three tiles will give you an overview of hello current threats.</span></span> <span data-ttu-id="461a9-137">在 hello**具有惡意連出流量伺服器**（內部或外部網路），您要監視的任何電腦時，將會無法 tooidentify 也就是傳送惡意流量 toohello 網際網路。</span><span class="sxs-lookup"><span data-stu-id="461a9-137">In hello **Server with outbound malicious traffic** you will be able tooidentify if there is any computer that you are monitoring (inside or outside of your network) that is sending malicious traffic toohello Internet.</span></span> 

<span data-ttu-id="461a9-138">hello**偵測到威脅類型**磚會顯示為最新的 「 在 hello wild"hello 威脅的摘要時，如果您按一下這個磚會看見更多有關這些威脅的詳細資料如下所示：</span><span class="sxs-lookup"><span data-stu-id="461a9-138">hello **Detected threat types** tile shows a summary of hello threats that are current “in hello wild”, if you click on this tile you will see more details about these threats as show below:</span></span>

![偵測到的威脅類型](./media/oms-security-responding-alerts/oms-security-responding-alerts-fig3.png)

<span data-ttu-id="461a9-140">您可以按一下每個威脅，以擷取其詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="461a9-140">You can extract more information about each threat by clicking on it.</span></span> <span data-ttu-id="461a9-141">以下的 hello 範例顯示更多詳細殭屍網路：</span><span class="sxs-lookup"><span data-stu-id="461a9-141">hello example below shows more details about Botnet:</span></span>

![威脅的詳細資料](./media/oms-security-responding-alerts/oms-security-responding-alerts-fig4.png)

<span data-ttu-id="461a9-143">本章節的 hello 開頭所述，這項資訊可以是很有幫助期間事件回應案例。</span><span class="sxs-lookup"><span data-stu-id="461a9-143">As described in hello beginning of this section, this information can be very useful during an incident response case.</span></span> <span data-ttu-id="461a9-144">它也可以是重要期間鑑識偵查，您需要 toofind hello 來源 hello 攻擊，哪個系統已遭到洩露，而且 hello 時間軸的位置。</span><span class="sxs-lookup"><span data-stu-id="461a9-144">It can also be important during a forensic investigation, where you need toofind hello source of hello attack, which system was compromised and hello timeline.</span></span> <span data-ttu-id="461a9-145">例如，您可以輕鬆地識別 hello 攻擊的一些重要詳細這份報表中： hello hello 攻擊的來源、 hello 受到危害的本機 IP 和 hello hello 連接的目前工作階段狀態。</span><span class="sxs-lookup"><span data-stu-id="461a9-145">In this report you can easily identify some key details about hello attack, such as: hello source of hello attack, hello local IP that was compromised and hello current session state of hello connection.</span></span> 

<span data-ttu-id="461a9-146">hello**威脅情報對應**協助 tooidentify hello 目前位置周圍 hello 地球惡意流量。</span><span class="sxs-lookup"><span data-stu-id="461a9-146">hello **threat intelligence map** will help you tooidentify hello current locations around hello globe that have malicious traffic.</span></span> <span data-ttu-id="461a9-147">有 （內送） 的橙色和紅色 （外寄） 箭號在此對應中，找出 hello 流量的方向，如果您按一下的其中一個這些箭號，它會顯示 hello 類型的威脅和 hello 流量方向如下所示：</span><span class="sxs-lookup"><span data-stu-id="461a9-147">There are orange (incoming) and red (outgoing) arrows in this map that identify hello traffic direction, if you click in one of these arrows, it will show hello type of threat and hello traffic direction as shown below:</span></span>

![威脅情報對應](./media/oms-security-responding-alerts/oms-security-responding-alerts-fig5.png)

> [!NOTE]
> <span data-ttu-id="461a9-149">您可以觀看示範如何 toouse 這項功能，在事件回應程序藉由監看 hello 簡報[降低資料中心的安全性威脅與使用 Operations Management Suite 的引導式調查](https://myignite.microsoft.com/videos/5000)在 Microsoft Ignite 傳遞。</span><span class="sxs-lookup"><span data-stu-id="461a9-149">You can see a demonstration on how toouse this capability during an incident response process by watching hello presentation [Mitigate datacenter security threats with guided investigation using Operations Management Suite](https://myignite.microsoft.com/videos/5000) delivered at Microsoft Ignite.</span></span>
> 

### <a name="responding-toodistinct-malicious-ip-accessed"></a><span data-ttu-id="461a9-150">回應 toodistinct 惡意 IP 存取</span><span class="sxs-lookup"><span data-stu-id="461a9-150">Responding toodistinct malicious IP accessed</span></span>
<span data-ttu-id="461a9-151">在某些情況下，您可能會發現已從一部受監視的電腦存取潛在惡意 IP：</span><span class="sxs-lookup"><span data-stu-id="461a9-151">In some scenarios, you may notice a potential malicious IP that was accessed from one monitored computer:</span></span>

![威脅情報對應](./media/oms-security-responding-alerts/oms-security-responding-alerts-fig6.png)

<span data-ttu-id="461a9-153">此警示和其他人在 hello 相同類別目錄，利用透過 OMS 安全性會產生[Microsoft 威脅情報](https://youtu.be/O4WtxgUrDc8)。</span><span class="sxs-lookup"><span data-stu-id="461a9-153">This alert and others within hello same category, are generated via OMS Security by leveraging [Microsoft Threat Intelligence](https://youtu.be/O4WtxgUrDc8).</span></span> <span data-ttu-id="461a9-154">hello 威脅情報資料是 Microsoft 所收集，以及主要威脅情報提供者購買。</span><span class="sxs-lookup"><span data-stu-id="461a9-154">hello Threat Intelligence data is collected by Microsoft as well as purchased from leading threat intelligence providers.</span></span> <span data-ttu-id="461a9-155">這項資料會經常更新，並調整 toofast 移動的威脅。</span><span class="sxs-lookup"><span data-stu-id="461a9-155">This data is updated frequently and adapted toofast-moving threats.</span></span> <span data-ttu-id="461a9-156">Tooits 本質，因為它應與結合其他來源的安全性資訊時[調查](https://blogs.technet.microsoft.com/msoms/2016/12/08/investigating-suspicious-activity-in-a-hybrid-cloud-with-oms-security/)安全性警示。</span><span class="sxs-lookup"><span data-stu-id="461a9-156">Due tooits nature, it should be combined with other sources of security information while [investigating](https://blogs.technet.microsoft.com/msoms/2016/12/08/investigating-suspicious-activity-in-a-hybrid-cloud-with-oms-security/) a security alert.</span></span> 

## <a name="customize-alerts-received-via-e-mail"></a><span data-ttu-id="461a9-157">自訂透過電子郵件接收的警示</span><span class="sxs-lookup"><span data-stu-id="461a9-157">Customize alerts received via e-mail</span></span>

<span data-ttu-id="461a9-158">您可以自訂在 OMS 安全性觸發安全性警示時，組織內的哪些使用者會收到通知。</span><span class="sxs-lookup"><span data-stu-id="461a9-158">You can customize which users in your organization will be notified when security alerts are triggered by OMS Security.</span></span> <span data-ttu-id="461a9-159">這個選項才可以使用下概觀 / 設定在 hello OMS 儀表板：</span><span class="sxs-lookup"><span data-stu-id="461a9-159">This option is available under Overview / Settings at hello OMS dashboard:</span></span>

![電子郵件](./media/oms-security-responding-alerts/oms-security-responding-alerts-fig7.png)

## <a name="see-also"></a><span data-ttu-id="461a9-161">另請參閱</span><span class="sxs-lookup"><span data-stu-id="461a9-161">See also</span></span>
<span data-ttu-id="461a9-162">在本文件中，您學到如何 toouse hello**威脅情報**OMS 安全性和稽核解決方案 toorespond toosecurity 警示中的選項。</span><span class="sxs-lookup"><span data-stu-id="461a9-162">In this document, you learned how toouse hello **Threat Intelligence** option in OMS Security and Audit solution toorespond toosecurity alerts.</span></span> <span data-ttu-id="461a9-163">toolearn 進一步了解 OMS 安全性，請參閱下列文章 hello:</span><span class="sxs-lookup"><span data-stu-id="461a9-163">toolearn more about OMS Security, see hello following articles:</span></span>

* [<span data-ttu-id="461a9-164">Operations Management Suite (OMS) 概觀</span><span class="sxs-lookup"><span data-stu-id="461a9-164">Operations Management Suite (OMS) overview</span></span>](operations-management-suite-overview.md)
* [<span data-ttu-id="461a9-165">開始使用 Operations Management Suite 安全性和稽核解決方案</span><span class="sxs-lookup"><span data-stu-id="461a9-165">Getting started with Operations Management Suite Security and Audit Solution</span></span>](oms-security-getting-started.md)
* [<span data-ttu-id="461a9-166">在 Operations Management Suite 安全性和稽核解決方案內監視資源</span><span class="sxs-lookup"><span data-stu-id="461a9-166">Monitoring Resources in Operations Management Suite Security and Audit Solution</span></span>](oms-security-monitoring-resources.md)

