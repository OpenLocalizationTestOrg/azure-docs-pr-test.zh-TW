---
title: "在 Operations Management Suite 安全性和稽核解決方案內監視及回應安全性警示 | Microsoft Docs"
description: "這份文件可協助您使用 OMS 安全性和稽核中可用的 [威脅情報] 選項來監視及回應安全性警示。"
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
ms.openlocfilehash: 0cf9b83d7023641ec445a59a5e61d3da038695fa
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="monitoring-and-responding-to-security-alerts-in-operations-management-suite-security-and-audit-solution"></a><span data-ttu-id="17a85-103">在 Operations Management Suite 安全性和稽核解決方案內監視及回應安全性警示</span><span class="sxs-lookup"><span data-stu-id="17a85-103">Monitoring and responding to security alerts in Operations Management Suite Security and Audit Solution</span></span>
<span data-ttu-id="17a85-104">這份文件可協助您使用 OMS 安全性和稽核中可用的威脅情報選項來監視及回應安全性警示。</span><span class="sxs-lookup"><span data-stu-id="17a85-104">This document helps you use the threat intelligence option available in OMS Security and Audit to monitor and respond to security alerts.</span></span>

## <a name="what-is-oms"></a><span data-ttu-id="17a85-105">何謂 OMS？</span><span class="sxs-lookup"><span data-stu-id="17a85-105">What is OMS?</span></span>
<span data-ttu-id="17a85-106">Microsoft Operations Management Suite (OMS) 是 Microsoft 的雲端型 IT 管理解決方案，可協助您管理並保護內部部署和雲端基礎結構。</span><span class="sxs-lookup"><span data-stu-id="17a85-106">Microsoft Operations Management Suite (OMS) is Microsoft's cloud based IT management solution that helps you manage and protect your on-premises and cloud infrastructure.</span></span> <span data-ttu-id="17a85-107">如需 OMS 的詳細資訊，請閱讀 [Operations Management Suite](https://technet.microsoft.com/library/mt484091.aspx)一文。</span><span class="sxs-lookup"><span data-stu-id="17a85-107">For more information about OMS, read the article [Operations Management Suite](https://technet.microsoft.com/library/mt484091.aspx).</span></span>

## <a name="threat-intelligence"></a><span data-ttu-id="17a85-108">威脅情報</span><span class="sxs-lookup"><span data-stu-id="17a85-108">Threat intelligence</span></span>
<span data-ttu-id="17a85-109">在使用者可廣泛存取網路且使用各種裝置連接到公司資料的企業環境中，請確定您可以主動監視資源，並快速地回應安全性事件。</span><span class="sxs-lookup"><span data-stu-id="17a85-109">In an enterprise environment where users have broad access to the network and use a variety of devices to connect to corporate data, it is imperative that you can actively monitor your resources and quickly respond to security incidents.</span></span> <span data-ttu-id="17a85-110">從安全性生命週期觀點來看，這點特別重要，因為有些網路安全性威脅可能不會引發可透過傳統安全性技術控制項識別的警示或可疑活動。</span><span class="sxs-lookup"><span data-stu-id="17a85-110">This is particular important from the security lifecycle perspective because some cybersecurity threats may not raise alerts or suspicious activities that can be identified by traditional security technical controls.</span></span> 

<span data-ttu-id="17a85-111">使用 OMS 安全性和稽核中可用的 [威脅情報]  選項，IT 系統管理員可以識別對環境的安全性威脅 (例如，識別特定的電腦是否屬於 [殭屍網路](https://www.microsoft.com/security/sir/story/default.aspx#!botnetsection))。</span><span class="sxs-lookup"><span data-stu-id="17a85-111">By using the **Threat Intelligence** option available in OMS Security and Audit, IT administrators can identify security threats against the environment, for example, identify if a particular computer is part of a [botnet](https://www.microsoft.com/security/sir/story/default.aspx#!botnetsection).</span></span> <span data-ttu-id="17a85-112">如果攻擊者偷偷地安裝惡意程式碼，暗中將此電腦連接到命令和控制項，則電腦可能會成為殭屍網路中的節點。</span><span class="sxs-lookup"><span data-stu-id="17a85-112">Computers can become nodes in a botnet when attackers illicitly install malware that secretly connects this computer to the command and control.</span></span> <span data-ttu-id="17a85-113">它也可以識別來自地下通訊通道 (例如 [暗網](https://www.microsoft.com/security/sir/story/default.aspx#!botnetsection_honeypots_darkents)) 的潛在威脅。</span><span class="sxs-lookup"><span data-stu-id="17a85-113">It can also identify potential threats coming from underground communication channels, such as [darknet](https://www.microsoft.com/security/sir/story/default.aspx#!botnetsection_honeypots_darkents).</span></span> 

<span data-ttu-id="17a85-114">為了建置此威脅情報，OMS 安全性和稽核會使用來自 Microsoft 內多個來源的資料。</span><span class="sxs-lookup"><span data-stu-id="17a85-114">In order to build this threat intelligence, OMS Security and Audit use data coming from multiple sources within Microsoft.</span></span> <span data-ttu-id="17a85-115">OMS 安全性和稽核將會利用這項資料來識別您環境的潛在威脅。</span><span class="sxs-lookup"><span data-stu-id="17a85-115">OMS Security and Audit will leverage this data to identify potential threats against your environment.</span></span>

<span data-ttu-id="17a85-116">[威脅情報] 窗格是由三個主要選項所組成︰</span><span class="sxs-lookup"><span data-stu-id="17a85-116">The Threat Intelligence pane is composed by three major options:</span></span>

* <span data-ttu-id="17a85-117">具有輸出惡意流量的伺服器</span><span class="sxs-lookup"><span data-stu-id="17a85-117">Servers with outbound malicious traffic</span></span>
* <span data-ttu-id="17a85-118">偵測到的威脅類型</span><span class="sxs-lookup"><span data-stu-id="17a85-118">Detected threats types</span></span>
* <span data-ttu-id="17a85-119">威脅情報對應</span><span class="sxs-lookup"><span data-stu-id="17a85-119">Threat intelligence map</span></span>

> [!NOTE]
> <span data-ttu-id="17a85-120">如需所有這些選項的概觀，請參閱 [開始使用 Operations Management Suite 安全性和稽核解決方案](oms-security-getting-started.md)。</span><span class="sxs-lookup"><span data-stu-id="17a85-120">for an overview of all these options, read [Getting started with Operations Management Suite Security and Audit Solution](oms-security-getting-started.md).</span></span>
> 
> 

### <a name="responding-to-security-alerts"></a><span data-ttu-id="17a85-121">回應安全性警示</span><span class="sxs-lookup"><span data-stu-id="17a85-121">Responding to security alerts</span></span>
<span data-ttu-id="17a85-122">[安全性事件回應](https://technet.microsoft.com/library/cc512623.aspx) 程序的其中一個步驟是識別危害系統的嚴重性。</span><span class="sxs-lookup"><span data-stu-id="17a85-122">One of the steps of a [security incident response](https://technet.microsoft.com/library/cc512623.aspx) process is to identify the severity of the compromise system(s).</span></span> <span data-ttu-id="17a85-123">在這個階段，您應該執行下列工作︰</span><span class="sxs-lookup"><span data-stu-id="17a85-123">In this phase you should perform the following tasks:</span></span>

* <span data-ttu-id="17a85-124">判斷攻擊本質</span><span class="sxs-lookup"><span data-stu-id="17a85-124">Determine the nature of the attack</span></span>
* <span data-ttu-id="17a85-125">判斷攻擊源點</span><span class="sxs-lookup"><span data-stu-id="17a85-125">Determine the attack point of origin</span></span>
* <span data-ttu-id="17a85-126">判斷攻擊意圖。</span><span class="sxs-lookup"><span data-stu-id="17a85-126">Determine the intent of the attack.</span></span> <span data-ttu-id="17a85-127">在組織中特別指示還是隨機指示攻擊取得特定資訊？</span><span class="sxs-lookup"><span data-stu-id="17a85-127">Was the attack specifically directed at your organization to acquire specific information, or was it random?</span></span>
* <span data-ttu-id="17a85-128">識別已遭入侵的系統</span><span class="sxs-lookup"><span data-stu-id="17a85-128">Identify the systems that have been compromised</span></span>
* <span data-ttu-id="17a85-129">識別已存取的檔案，並判斷這些檔案的敏感度</span><span class="sxs-lookup"><span data-stu-id="17a85-129">Identify the files that have been accessed and determine the sensitivity of those files</span></span>

<span data-ttu-id="17a85-130">您可以利用 OMS 安全性和稽核解決方案中的 [威脅情報]  資訊，協助進行這些工作。</span><span class="sxs-lookup"><span data-stu-id="17a85-130">You can leverage **Threat Intelligence** information in OMS Security and Audit solution to help with these tasks.</span></span> <span data-ttu-id="17a85-131">請遵循下列步驟來存取這個 [威脅情報]  選項：</span><span class="sxs-lookup"><span data-stu-id="17a85-131">Follow the steps below to access this **Threat Intelligence** options:</span></span>

1. <span data-ttu-id="17a85-132">在 [Microsoft Operations Management Suite] 主儀表板內按一下 [安全性和稽核] 圖格。</span><span class="sxs-lookup"><span data-stu-id="17a85-132">In the **Microsoft Operations Management Suite** main dashboard click **Security and Audit** tile.</span></span>
   
    ![安全性和稽核](./media/oms-security-responding-alerts/oms-security-responding-alerts-fig1.png)
2. <span data-ttu-id="17a85-134">在 [安全性和稽核] 儀表板中，您會在右側看到 [威脅情報] 選項，如下所示︰</span><span class="sxs-lookup"><span data-stu-id="17a85-134">In the **Security and Audit** dashboard, you will see the **Threat Intelligence** options in the right, as shown below:</span></span>
   
    ![威脅情報](./media/oms-security-responding-alerts/oms-security-responding-alerts-fig2-ga.png)

<span data-ttu-id="17a85-136">這三個圖格會提供目前威脅的概觀。</span><span class="sxs-lookup"><span data-stu-id="17a85-136">These three tiles will give you an overview of the current threats.</span></span> <span data-ttu-id="17a85-137">在 [具有輸出惡意流量的伺服器]  中，可以找出是否有任何您監視的電腦 (網路內部或外部) 正在將惡意流量傳送到網際網路。</span><span class="sxs-lookup"><span data-stu-id="17a85-137">In the **Server with outbound malicious traffic** you will be able to identify if there is any computer that you are monitoring (inside or outside of your network) that is sending malicious traffic to the Internet.</span></span> 

<span data-ttu-id="17a85-138">[偵測到的威脅類型]  圖格會顯示目前偵測到的威脅摘要，如果您按一下此圖格，會看到這些威脅的詳細資訊，如下所示︰</span><span class="sxs-lookup"><span data-stu-id="17a85-138">The **Detected threat types** tile shows a summary of the threats that are current “in the wild”, if you click on this tile you will see more details about these threats as show below:</span></span>

![偵測到的威脅類型](./media/oms-security-responding-alerts/oms-security-responding-alerts-fig3.png)

<span data-ttu-id="17a85-140">您可以按一下每個威脅，以擷取其詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="17a85-140">You can extract more information about each threat by clicking on it.</span></span> <span data-ttu-id="17a85-141">下列範例顯示殭屍網路的詳細資訊：</span><span class="sxs-lookup"><span data-stu-id="17a85-141">The example below shows more details about Botnet:</span></span>

![威脅的詳細資料](./media/oms-security-responding-alerts/oms-security-responding-alerts-fig4.png)

<span data-ttu-id="17a85-143">如本節開頭所述，此資訊在事件回應案例期間可能會很有幫助。</span><span class="sxs-lookup"><span data-stu-id="17a85-143">As described in the beginning of this section, this information can be very useful during an incident response case.</span></span> <span data-ttu-id="17a85-144">在需要找出攻擊來源、遭入侵系統和時間表的鑑識調查期間，這項資訊也十分重要。</span><span class="sxs-lookup"><span data-stu-id="17a85-144">It can also be important during a forensic investigation, where you need to find the source of the attack, which system was compromised and the timeline.</span></span> <span data-ttu-id="17a85-145">在這份報告中，您可以輕鬆地識別攻擊的一些重要詳細資料，例如︰攻擊來源、遭入侵的本機 IP，以及連接的目前工作階段狀態。</span><span class="sxs-lookup"><span data-stu-id="17a85-145">In this report you can easily identify some key details about the attack, such as: the source of the attack, the local IP that was compromised and the current session state of the connection.</span></span> 

<span data-ttu-id="17a85-146">**威脅情報對應** 將協助您識別全球各地目前有惡意流量的位置。</span><span class="sxs-lookup"><span data-stu-id="17a85-146">The **threat intelligence map** will help you to identify the current locations around the globe that have malicious traffic.</span></span> <span data-ttu-id="17a85-147">這個對應中的橙色 (內送) 和紅色 (外寄) 箭號識別流量方向，如果您按一下其中一個箭號，則會顯示威脅類型和流量方向，如下所示︰</span><span class="sxs-lookup"><span data-stu-id="17a85-147">There are orange (incoming) and red (outgoing) arrows in this map that identify the traffic direction, if you click in one of these arrows, it will show the type of threat and the traffic direction as shown below:</span></span>

![威脅情報對應](./media/oms-security-responding-alerts/oms-security-responding-alerts-fig5.png)

> [!NOTE]
> <span data-ttu-id="17a85-149">您可以觀看 Microsoft Ignite 所提供的簡報[使用 Operations Management Suite 以引導式調查減輕資料中心的安全性威脅](https://myignite.microsoft.com/videos/5000)，查看如何在事件回應程序期間使用這項功能的示範。</span><span class="sxs-lookup"><span data-stu-id="17a85-149">You can see a demonstration on how to use this capability during an incident response process by watching the presentation [Mitigate datacenter security threats with guided investigation using Operations Management Suite](https://myignite.microsoft.com/videos/5000) delivered at Microsoft Ignite.</span></span>
> 

### <a name="responding-to-distinct-malicious-ip-accessed"></a><span data-ttu-id="17a85-150">回應存取的相異惡意 IP</span><span class="sxs-lookup"><span data-stu-id="17a85-150">Responding to distinct malicious IP accessed</span></span>
<span data-ttu-id="17a85-151">在某些情況下，您可能會發現已從一部受監視的電腦存取潛在惡意 IP：</span><span class="sxs-lookup"><span data-stu-id="17a85-151">In some scenarios, you may notice a potential malicious IP that was accessed from one monitored computer:</span></span>

![威脅情報對應](./media/oms-security-responding-alerts/oms-security-responding-alerts-fig6.png)

<span data-ttu-id="17a85-153">會透過 OMS 安全性產生此警示以及其他相同類別中的警示，方法是運用 [Microsoft 威脅情報](https://youtu.be/O4WtxgUrDc8)。</span><span class="sxs-lookup"><span data-stu-id="17a85-153">This alert and others within the same category, are generated via OMS Security by leveraging [Microsoft Threat Intelligence](https://youtu.be/O4WtxgUrDc8).</span></span> <span data-ttu-id="17a85-154">威脅情報資料是由 Microsoft 向主要威脅情報提供者所收集及購買。</span><span class="sxs-lookup"><span data-stu-id="17a85-154">The Threat Intelligence data is collected by Microsoft as well as purchased from leading threat intelligence providers.</span></span> <span data-ttu-id="17a85-155">這項資料會經常更新，且適用於快速移動威脅。</span><span class="sxs-lookup"><span data-stu-id="17a85-155">This data is updated frequently and adapted to fast-moving threats.</span></span> <span data-ttu-id="17a85-156">本質上，在[調查](https://blogs.technet.microsoft.com/msoms/2016/12/08/investigating-suspicious-activity-in-a-hybrid-cloud-with-oms-security/)安全性警示時，應將它與其他安全性資訊的來源進行結合。</span><span class="sxs-lookup"><span data-stu-id="17a85-156">Due to its nature, it should be combined with other sources of security information while [investigating](https://blogs.technet.microsoft.com/msoms/2016/12/08/investigating-suspicious-activity-in-a-hybrid-cloud-with-oms-security/) a security alert.</span></span> 

## <a name="customize-alerts-received-via-e-mail"></a><span data-ttu-id="17a85-157">自訂透過電子郵件接收的警示</span><span class="sxs-lookup"><span data-stu-id="17a85-157">Customize alerts received via e-mail</span></span>

<span data-ttu-id="17a85-158">您可以自訂在 OMS 安全性觸發安全性警示時，組織內的哪些使用者會收到通知。</span><span class="sxs-lookup"><span data-stu-id="17a85-158">You can customize which users in your organization will be notified when security alerts are triggered by OMS Security.</span></span> <span data-ttu-id="17a85-159">此選項可在 OMS 儀表板的 [概觀 / 設定] 下找到：</span><span class="sxs-lookup"><span data-stu-id="17a85-159">This option is available under Overview / Settings at the OMS dashboard:</span></span>

![電子郵件](./media/oms-security-responding-alerts/oms-security-responding-alerts-fig7.png)

## <a name="see-also"></a><span data-ttu-id="17a85-161">另請參閱</span><span class="sxs-lookup"><span data-stu-id="17a85-161">See also</span></span>
<span data-ttu-id="17a85-162">在這份文件中，您了解到如何使用 OMS 安全性和稽核解決方案中的 [威脅情報]  選項來回應安全性警示。</span><span class="sxs-lookup"><span data-stu-id="17a85-162">In this document, you learned how to use the **Threat Intelligence** option in OMS Security and Audit solution to respond to security alerts.</span></span> <span data-ttu-id="17a85-163">若要深入了解 OMS 安全性，請參閱下列文章：</span><span class="sxs-lookup"><span data-stu-id="17a85-163">To learn more about OMS Security, see the following articles:</span></span>

* [<span data-ttu-id="17a85-164">Operations Management Suite (OMS) 概觀</span><span class="sxs-lookup"><span data-stu-id="17a85-164">Operations Management Suite (OMS) overview</span></span>](operations-management-suite-overview.md)
* [<span data-ttu-id="17a85-165">開始使用 Operations Management Suite 安全性和稽核解決方案</span><span class="sxs-lookup"><span data-stu-id="17a85-165">Getting started with Operations Management Suite Security and Audit Solution</span></span>](oms-security-getting-started.md)
* [<span data-ttu-id="17a85-166">在 Operations Management Suite 安全性和稽核解決方案內監視資源</span><span class="sxs-lookup"><span data-stu-id="17a85-166">Monitoring Resources in Operations Management Suite Security and Audit Solution</span></span>](oms-security-monitoring-resources.md)

