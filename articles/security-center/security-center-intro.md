---
title: "Azure 資訊安全中心簡介 | Microsoft Docs"
description: "了解 Azure 資訊安全中心、其主要功能及運作方式。"
services: security-center
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
editor: 
ms.assetid: 45b9756b-6449-49ec-950b-5ed1e7c56daa
ms.service: security-center
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/16/2017
ms.author: terrylan
ms.openlocfilehash: 8951167213da6ab5341c1ca420353ec625ef5424
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="introduction-to-azure-security-center"></a><span data-ttu-id="cada6-103">Azure 資訊安全中心簡介</span><span class="sxs-lookup"><span data-stu-id="cada6-103">Introduction to Azure Security Center</span></span>
<span data-ttu-id="cada6-104">了解 Azure 資訊安全中心、其主要功能及運作方式。</span><span class="sxs-lookup"><span data-stu-id="cada6-104">Learn about Azure Security Center, its key capabilities, and how it works.</span></span>

> [!NOTE]
> <span data-ttu-id="cada6-105">從 2017 年 6 月初開始，資訊安全中心會使用 Microsoft Monitoring Agent 來收集和儲存資料。</span><span class="sxs-lookup"><span data-stu-id="cada6-105">Beginning in early June 2017, Security Center will use the Microsoft Monitoring Agent to collect and store data.</span></span> <span data-ttu-id="cada6-106">若要深入了解，請參閱 [Azure 資訊安全中心平台移轉](security-center-platform-migration.md)。</span><span class="sxs-lookup"><span data-stu-id="cada6-106">See [Azure Security Center Platform Migration](security-center-platform-migration.md) to learn more.</span></span> <span data-ttu-id="cada6-107">本文中的資訊說明轉換至 Microsoft Monitoring Agent 後的資訊安全中心功能。</span><span class="sxs-lookup"><span data-stu-id="cada6-107">The information in this article represents Security Center functionality after transition to the Microsoft Monitoring Agent.</span></span>
>
>

## <a name="what-is-azure-security-center"></a><span data-ttu-id="cada6-108">什麼是 Azure 資訊安全中心？</span><span class="sxs-lookup"><span data-stu-id="cada6-108">What is Azure Security Center?</span></span>
 <span data-ttu-id="cada6-109">資訊安全中心利用加強對您 Azure 資源的能見度及安全性控制權，來協助您預防、偵測及回應威脅。</span><span class="sxs-lookup"><span data-stu-id="cada6-109">Security Center helps you prevent, detect, and respond to threats with increased visibility into and control over the security of your Azure resources.</span></span> <span data-ttu-id="cada6-110">它提供您 Azure 訂用帳戶之間的整合式安全性監視和原則管理，協助您偵測可能會忽略的威脅，且適用於廣泛的安全性解決方案生態系統。</span><span class="sxs-lookup"><span data-stu-id="cada6-110">It provides integrated security monitoring and policy management across your Azure subscriptions, helps detect threats that might otherwise go unnoticed, and works with a broad ecosystem of security solutions.</span></span>

## <a name="key-capabilities"></a><span data-ttu-id="cada6-111">主要功能</span><span class="sxs-lookup"><span data-stu-id="cada6-111">Key capabilities</span></span>
 <span data-ttu-id="cada6-112">資訊安全中心，提供 Azure 內建的威脅預防、偵測及回應功能，簡單易用又有效。</span><span class="sxs-lookup"><span data-stu-id="cada6-112">Security Center delivers easy-to-use and effective threat prevention, detection, and response capabilities that are built in to Azure.</span></span> <span data-ttu-id="cada6-113">主要功能：</span><span class="sxs-lookup"><span data-stu-id="cada6-113">Key capabilities are:</span></span>

| <span data-ttu-id="cada6-114">階段</span><span class="sxs-lookup"><span data-stu-id="cada6-114">Stage</span></span> | <span data-ttu-id="cada6-115">功能</span><span class="sxs-lookup"><span data-stu-id="cada6-115">Capability</span></span> |
| --- | --- |
| <span data-ttu-id="cada6-116">防止</span><span class="sxs-lookup"><span data-stu-id="cada6-116">Prevent</span></span> |<span data-ttu-id="cada6-117">監視 Azure 資源的安全性狀態</span><span class="sxs-lookup"><span data-stu-id="cada6-117">Monitors the security state of your Azure resources</span></span> |
| <span data-ttu-id="cada6-118">防止</span><span class="sxs-lookup"><span data-stu-id="cada6-118">Prevent</span></span> | <span data-ttu-id="cada6-119">根據您的公司安全性需求、您使用的應用程式類型和資料的機密性，定義您的 Azure 訂用帳戶原則</span><span class="sxs-lookup"><span data-stu-id="cada6-119">Defines policies for your Azure subscriptions based on your company’s security requirements, the types of applications that you use, and the sensitivity of your data</span></span> |
| <span data-ttu-id="cada6-120">防止</span><span class="sxs-lookup"><span data-stu-id="cada6-120">Prevent</span></span> | <span data-ttu-id="cada6-121">使用原則導向的安全性建議，引導服務擁有者完成需要控制項的實作程序</span><span class="sxs-lookup"><span data-stu-id="cada6-121">Uses policy-driven security recommendations to guide service owners through the process of implementing needed controls</span></span> |
| <span data-ttu-id="cada6-122">防止</span><span class="sxs-lookup"><span data-stu-id="cada6-122">Prevent</span></span> | <span data-ttu-id="cada6-123">快速部署 Microsoft 和第三方的安全性服務和應用裝置</span><span class="sxs-lookup"><span data-stu-id="cada6-123">Rapidly deploys security services and appliances from Microsoft and partners</span></span> |
| <span data-ttu-id="cada6-124">偵測</span><span class="sxs-lookup"><span data-stu-id="cada6-124">Detect</span></span> |<span data-ttu-id="cada6-125">自動收集和分析下列來源的安全性資料：Azure 資源、網路，以及反惡意程式碼程式和防火牆等夥伴解決方案</span><span class="sxs-lookup"><span data-stu-id="cada6-125">Automatically collects and analyzes security data from your Azure resources, the network, and partner solutions like antimalware programs and firewalls</span></span> |
| <span data-ttu-id="cada6-126">偵測</span><span class="sxs-lookup"><span data-stu-id="cada6-126">Detect</span></span> | <span data-ttu-id="cada6-127">使用來自 Microsoft 產品與服務、Microsoft 數位犯罪防治中心 (DCU)、Microsoft 安全性回應中心 (MSRC) 以及外部摘要的全球威脅情報</span><span class="sxs-lookup"><span data-stu-id="cada6-127">Uses global threat intelligence from Microsoft products and services, the Microsoft Digital Crimes Unit (DCU), the Microsoft Security Response Center (MSRC), and external feeds</span></span> |
| <span data-ttu-id="cada6-128">偵測</span><span class="sxs-lookup"><span data-stu-id="cada6-128">Detect</span></span> | <span data-ttu-id="cada6-129">套用進階分析，包括機器學習服務和行為分析</span><span class="sxs-lookup"><span data-stu-id="cada6-129">Applies advanced analytics, including machine learning and behavioral analysis</span></span> |
| <span data-ttu-id="cada6-130">回應</span><span class="sxs-lookup"><span data-stu-id="cada6-130">Respond</span></span> |<span data-ttu-id="cada6-131">依優先順序提供安全性事件/警示</span><span class="sxs-lookup"><span data-stu-id="cada6-131">Provides prioritized security incidents/alerts</span></span> |
| <span data-ttu-id="cada6-132">回應</span><span class="sxs-lookup"><span data-stu-id="cada6-132">Respond</span></span> | <span data-ttu-id="cada6-133">提供對攻擊和受影響資源來源的深入見解</span><span class="sxs-lookup"><span data-stu-id="cada6-133">Offers insights into the source of the attack and impacted resources</span></span> |
| <span data-ttu-id="cada6-134">回應</span><span class="sxs-lookup"><span data-stu-id="cada6-134">Respond</span></span> | <span data-ttu-id="cada6-135">建議停止目前攻擊及協助避免未來攻擊的方法</span><span class="sxs-lookup"><span data-stu-id="cada6-135">Suggests ways to stop the current attack and help prevent future attacks</span></span> |

## <a name="introductory-walkthrough"></a><span data-ttu-id="cada6-136">逐步解說介紹</span><span class="sxs-lookup"><span data-stu-id="cada6-136">Introductory walkthrough</span></span>

> [!NOTE]
> <span data-ttu-id="cada6-137">本文件將使用範例部署來介紹服務。</span><span class="sxs-lookup"><span data-stu-id="cada6-137">This document introduces the service by using an example deployment.</span></span> <span data-ttu-id="cada6-138">本文件不是一份逐步解說指南。</span><span class="sxs-lookup"><span data-stu-id="cada6-138">This document is not a step-by-step guide.</span></span>
>
>

 <span data-ttu-id="cada6-139">您可以從 [Azure 入口網站](https://azure.microsoft.com/features/azure-portal/)存取資訊安全中心。</span><span class="sxs-lookup"><span data-stu-id="cada6-139">You access Security Center from the [Azure portal](https://azure.microsoft.com/features/azure-portal/).</span></span> <span data-ttu-id="cada6-140">[登入入口網站](https://portal.azure.com)。</span><span class="sxs-lookup"><span data-stu-id="cada6-140">[Sign in to the portal](https://portal.azure.com).</span></span> <span data-ttu-id="cada6-141">在主要入口網站功能表下，捲動至 [資訊安全中心] 選項，或選取之前釘選到入口網站儀表板的 [資訊安全中心] 圖格。</span><span class="sxs-lookup"><span data-stu-id="cada6-141">Under the main portal menu, scroll to the **Security Center** option or select the **Security Center** tile that you previously pinned to the portal dashboard.</span></span>

![Azure 入口網站中的安全性磚][1]

<span data-ttu-id="cada6-143">從資訊安全中心，您可以設定安全性原則、監視安全性組態，並檢視安全性警示。</span><span class="sxs-lookup"><span data-stu-id="cada6-143">From Security Center, you can set security policies, monitor security configurations, and view security alerts.</span></span>

### <a name="security-policies"></a><span data-ttu-id="cada6-144">安全性原則</span><span class="sxs-lookup"><span data-stu-id="cada6-144">Security policies</span></span>
<span data-ttu-id="cada6-145">您可以根據公司的安全性需求來定義 Azure 訂用帳戶的原則。</span><span class="sxs-lookup"><span data-stu-id="cada6-145">You can define policies for your Azure subscriptions according to your company's security requirements.</span></span> <span data-ttu-id="cada6-146">您也可以根據您使用的應用程式類型或每個訂用帳戶中的資料機密性來修改這些原則。</span><span class="sxs-lookup"><span data-stu-id="cada6-146">You can also tailor them to the types of applications you're using or to the sensitivity of the data in each subscription.</span></span> <span data-ttu-id="cada6-147">例如，用於開發或測試的資源與用於實際執行應用程式的資源，兩者的安全性需求可能不同。</span><span class="sxs-lookup"><span data-stu-id="cada6-147">For example, resources used for development or testing may have different security requirements than those used for production applications.</span></span> <span data-ttu-id="cada6-148">同樣地，具有規範資料 (例如 PII) 的應用程式可能需要較高層級的安全性。</span><span class="sxs-lookup"><span data-stu-id="cada6-148">Likewise, applications with regulated data like PII may require a higher level of security.</span></span>

> [!NOTE]
> <span data-ttu-id="cada6-149">若要修改安全性原則，您必須是安全性系統管理員或是訂用帳戶的擁有者或參與者。</span><span class="sxs-lookup"><span data-stu-id="cada6-149">To modify a security policy, you must be a Security Administrator or the subscription's Owner or Contributor.</span></span> <span data-ttu-id="cada6-150">如需角色與資訊安全中心所允許動作的詳細資訊，請參閱 [Azure 資訊安全中心的權限](security-center-permissions.md)。</span><span class="sxs-lookup"><span data-stu-id="cada6-150">To learn more about roles and allowed actions in Security Center, see [Permissions in Azure Security Center](security-center-permissions.md).</span></span>
>
>

<span data-ttu-id="cada6-151">在 [資訊安全中心] 刀鋒視窗上，選取 [原則] 圖格來取得訂用帳戶和資源群組清單。</span><span class="sxs-lookup"><span data-stu-id="cada6-151">On the **Security Center** blade, select the **Policy** tile for a list of your subscriptions and resource groups.</span></span>   

![[資訊安全中心] 刀鋒視窗][2]

<span data-ttu-id="cada6-153">在 [安全性原則] 刀鋒視窗上，選取訂用帳戶來檢視原則詳細資料。</span><span class="sxs-lookup"><span data-stu-id="cada6-153">On the **Security policy** blade, select a subscription to view the policy details.</span></span>

<span data-ttu-id="cada6-154">**資料收集**啟用安全性原則的資料收集。</span><span class="sxs-lookup"><span data-stu-id="cada6-154">**Data collection** enables data collection for a security policy.</span></span> <span data-ttu-id="cada6-155">若加以啟用可以：</span><span class="sxs-lookup"><span data-stu-id="cada6-155">Enabling provides:</span></span>

* <span data-ttu-id="cada6-156">每日掃描所有支援的虛擬機器 (VM)，取得安全性監視和建議。</span><span class="sxs-lookup"><span data-stu-id="cada6-156">Daily scanning of all supported virtual machines (VMs) for security monitoring and recommendations.</span></span>
* <span data-ttu-id="cada6-157">收集安全性事件，供分析和偵測威脅所用。</span><span class="sxs-lookup"><span data-stu-id="cada6-157">Collection of security events for analysis and threat detection.</span></span>

> [!NOTE]
> <span data-ttu-id="cada6-158">資料收集是在訂用帳戶等級設定。</span><span class="sxs-lookup"><span data-stu-id="cada6-158">Data collection is configured at the subscription level.</span></span>
>
>

<span data-ttu-id="cada6-159">選取 [防護原則] 以開啟 [防護原則] 刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="cada6-159">Select **Prevention policy** to open the **Prevention policy** blade.</span></span> <span data-ttu-id="cada6-160">[顯示建議] 可讓您選擇想要監視的安全性控制項，以及您想要根據訂用帳戶內的資源安全性需求而看見的建議。</span><span class="sxs-lookup"><span data-stu-id="cada6-160">**Show recommendations for** lets you choose the security controls that you want to monitor and the recommendations that you want to see based on the security needs of the resources within the subscription.</span></span>

### <a name="security-recommendations"></a><span data-ttu-id="cada6-161">安全性建議</span><span class="sxs-lookup"><span data-stu-id="cada6-161">Security recommendations</span></span>
 <span data-ttu-id="cada6-162">資訊安全中心會分析 Azure 資源的安全性狀態，以識別潛在的安全性弱點。</span><span class="sxs-lookup"><span data-stu-id="cada6-162">Security Center analyzes the security state of your Azure resources to identify potential security vulnerabilities.</span></span> <span data-ttu-id="cada6-163">建議清單會引導您完成設定所需控制項的程序。</span><span class="sxs-lookup"><span data-stu-id="cada6-163">A list of recommendations guides you through the process of configuring needed controls.</span></span> <span data-ttu-id="cada6-164">範例包括：</span><span class="sxs-lookup"><span data-stu-id="cada6-164">Examples include:</span></span>

* <span data-ttu-id="cada6-165">佈建反惡意程式碼，以協助識別及移除惡意軟體</span><span class="sxs-lookup"><span data-stu-id="cada6-165">Provisioning antimalware to help identify and remove malicious software</span></span>
* <span data-ttu-id="cada6-166">設定網路安全性群組和規則，以控制對 VM 的流量</span><span class="sxs-lookup"><span data-stu-id="cada6-166">Configuring network security groups and rules to control traffic to VMs</span></span>
* <span data-ttu-id="cada6-167">佈建 Web 應用程式防火牆，以協助抵禦以 Web 應用程式為目標的攻擊</span><span class="sxs-lookup"><span data-stu-id="cada6-167">Provisioning of web application firewalls to help defend against attacks that target your web applications</span></span>
* <span data-ttu-id="cada6-168">部署遺漏的系統更新</span><span class="sxs-lookup"><span data-stu-id="cada6-168">Deploying missing system updates</span></span>
* <span data-ttu-id="cada6-169">處理不符合建議基準的作業系統組態</span><span class="sxs-lookup"><span data-stu-id="cada6-169">Addressing OS configurations that do not match the recommended baselines</span></span>

<span data-ttu-id="cada6-170">按一下 [建議] 圖格以取得建議清單。</span><span class="sxs-lookup"><span data-stu-id="cada6-170">Click the **Recommendations** tile for a list of recommendations.</span></span> <span data-ttu-id="cada6-171">按一下每個建議，檢視其他資訊或採取行動以解決問題。</span><span class="sxs-lookup"><span data-stu-id="cada6-171">Click each recommendation to view additional information or to take action to resolve the issue.</span></span>

![Azure 資訊安全中心的安全性建議][5]

### <a name="security-state-of-azure-resources"></a><span data-ttu-id="cada6-173">Azure 資源的安全性狀態</span><span class="sxs-lookup"><span data-stu-id="cada6-173">Security state of Azure resources</span></span>
<span data-ttu-id="cada6-174">儀表板的 [保護] 區段會依資源類型顯示環境的整體安全性狀態，包括 VM、Web 應用程式和其他資源。</span><span class="sxs-lookup"><span data-stu-id="cada6-174">The **Prevention** section of the dashboard shows the overall security posture of the environment by resource type, including VMs, web applications, and other resources.</span></span>   

<span data-ttu-id="cada6-175">選取 [保護] 之下的資源類型來檢視詳細資訊，包括一份任何已識別潛在安全性弱點的清單。</span><span class="sxs-lookup"><span data-stu-id="cada6-175">Select a resource type under **Prevention** to view more information, including a list of any potential security vulnerabilities that have been identified.</span></span> <span data-ttu-id="cada6-176">(下面的範例已選取 [計算])。</span><span class="sxs-lookup"><span data-stu-id="cada6-176">(**Compute** is selected in the example below.)</span></span>

![資源健康狀態磚][6]

### <a name="security-alerts"></a><span data-ttu-id="cada6-178">安全性警示</span><span class="sxs-lookup"><span data-stu-id="cada6-178">Security alerts</span></span>
 <span data-ttu-id="cada6-179">資訊安全中心會自動收集、分析和整合下列來源的記錄檔資料：Azure 資源、網路，以及反惡意程式碼程式和防火牆等夥伴解決方案。</span><span class="sxs-lookup"><span data-stu-id="cada6-179">Security Center automatically collects, analyzes, and integrates log data from your Azure resources, the network, and partner solutions like antimalware programs and firewalls.</span></span> <span data-ttu-id="cada6-180">偵測到威脅時，會建立安全性警示。</span><span class="sxs-lookup"><span data-stu-id="cada6-180">When threats are detected, a security alert is created.</span></span> <span data-ttu-id="cada6-181">偵測範例包括：</span><span class="sxs-lookup"><span data-stu-id="cada6-181">Examples include detection of:</span></span>

* <span data-ttu-id="cada6-182">已受到危害的 VM 與已知的惡意 IP 位址進行通訊</span><span class="sxs-lookup"><span data-stu-id="cada6-182">Compromised VMs communicating with known malicious IP addresses</span></span>
* <span data-ttu-id="cada6-183">使用 Windows 錯誤報告偵測到進階的惡意程式碼</span><span class="sxs-lookup"><span data-stu-id="cada6-183">Advanced malware detected by using Windows error reporting</span></span>
* <span data-ttu-id="cada6-184">針對 VM 的暴力密碼破解攻擊</span><span class="sxs-lookup"><span data-stu-id="cada6-184">Brute force attacks against VMs</span></span>
* <span data-ttu-id="cada6-185">來自整合式反惡意程式碼程式和防火牆的安全性警示</span><span class="sxs-lookup"><span data-stu-id="cada6-185">Security alerts from integrated antimalware programs and firewalls</span></span>

<span data-ttu-id="cada6-186">按一下 [安全性警示]  圖格會顯示已排定優先順序的警示清單。</span><span class="sxs-lookup"><span data-stu-id="cada6-186">Clicking the **Security alerts** tile displays a list of prioritized alerts.</span></span>

![安全性警示][7]

<span data-ttu-id="cada6-188">選取警示可顯示攻擊的詳細資訊以及矯正方法建議。</span><span class="sxs-lookup"><span data-stu-id="cada6-188">Selecting an alert shows more information about the attack and suggestions for how to remediate it.</span></span>

![安全性警示詳細資料][8]

### <a name="partner-solutions"></a><span data-ttu-id="cada6-190">合作夥伴解決方案</span><span class="sxs-lookup"><span data-stu-id="cada6-190">Partner solutions</span></span>
<span data-ttu-id="cada6-191">[合作夥伴解決方案] 圖格可監視與 Azure 訂用帳戶整合之合作夥伴解決方案的安全性狀態，讓您一目了然。</span><span class="sxs-lookup"><span data-stu-id="cada6-191">The **Partner solutions** tile lets you monitor at a glance the security state of your partner solutions integrated with your Azure subscription.</span></span> <span data-ttu-id="cada6-192">資訊安全中心會顯示來自解決方案的警示。</span><span class="sxs-lookup"><span data-stu-id="cada6-192">Security Center displays alerts coming from the solutions.</span></span>

<span data-ttu-id="cada6-193">選取 [合作夥伴解決方案] 圖格。</span><span class="sxs-lookup"><span data-stu-id="cada6-193">Select the **Partner solutions** tile.</span></span> <span data-ttu-id="cada6-194">隨即開啟一個刀鋒視窗，其中顯示所有已連接的合作夥伴解決方案清單。</span><span class="sxs-lookup"><span data-stu-id="cada6-194">A blade opens displaying a list of all connected partner solutions.</span></span>

![合作夥伴解決方案][9]

## <a name="get-started"></a><span data-ttu-id="cada6-196">開始使用</span><span class="sxs-lookup"><span data-stu-id="cada6-196">Get started</span></span>
<span data-ttu-id="cada6-197">若要開始使用資訊安全中心，您需要 Microsoft Azure 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="cada6-197">To get started with Security Center, you need a subscription to Microsoft Azure.</span></span> <span data-ttu-id="cada6-198">資訊安全中心已經由 Azure 訂用帳戶啟用。</span><span class="sxs-lookup"><span data-stu-id="cada6-198">Security Center is enabled with your Azure subscription.</span></span> <span data-ttu-id="cada6-199">如果您沒有訂用帳戶，可以註冊[免費試用](https://azure.microsoft.com/pricing/free-trial/)。</span><span class="sxs-lookup"><span data-stu-id="cada6-199">If you do not have a subscription, you can sign up for a [free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

 <span data-ttu-id="cada6-200">您可以從 [Azure 入口網站](https://azure.microsoft.com/features/azure-portal/)存取資訊安全中心。</span><span class="sxs-lookup"><span data-stu-id="cada6-200">You access Security Center from the [Azure portal](https://azure.microsoft.com/features/azure-portal/).</span></span> <span data-ttu-id="cada6-201">如需詳細資訊，請參閱 [入口網站文件](https://azure.microsoft.com/documentation/services/azure-portal/) 。</span><span class="sxs-lookup"><span data-stu-id="cada6-201">See the [portal documentation](https://azure.microsoft.com/documentation/services/azure-portal/) to learn more.</span></span>

<span data-ttu-id="cada6-202">[開始使用 Azure 資訊安全中心](security-center-get-started.md) 會快速引導您認識資訊安全中心的安全性監視和原則管理元件。</span><span class="sxs-lookup"><span data-stu-id="cada6-202">[Getting started with Azure Security Center](security-center-get-started.md) quickly guides you through the security-monitoring and policy-management components of Security Center.</span></span>

## <a name="next-steps"></a><span data-ttu-id="cada6-203">後續步驟</span><span class="sxs-lookup"><span data-stu-id="cada6-203">Next steps</span></span>
<span data-ttu-id="cada6-204">本文介紹了資訊安全中心、其重要功能和如何開始進行。</span><span class="sxs-lookup"><span data-stu-id="cada6-204">In this document, you were introduced to Security Center, its key capabilities, and how to get started.</span></span> <span data-ttu-id="cada6-205">若要深入了解，請參閱下列資源：</span><span class="sxs-lookup"><span data-stu-id="cada6-205">To learn more, see the following resources:</span></span>

* <span data-ttu-id="cada6-206">[在 Azure 資訊安全中心設定安全性原則](security-center-policies.md) — 了解如何為您的 Azure 訂用帳戶及資源群組設定安全性原則。</span><span class="sxs-lookup"><span data-stu-id="cada6-206">[Setting security policies in Azure Security Center](security-center-policies.md) — Learn how to configure security policies for your Azure subscriptions and resource groups.</span></span>
* <span data-ttu-id="cada6-207">[管理 Azure 資訊安全中心的安全性建議](security-center-recommendations.md) — 了解建議如何協助保護您的 Azure 資源。</span><span class="sxs-lookup"><span data-stu-id="cada6-207">[Managing security recommendations in Azure Security Center](security-center-recommendations.md) — Learn how recommendations help you protect your Azure resources.</span></span>
* <span data-ttu-id="cada6-208">[Azure 資訊安全中心的安全性健全狀況監視](security-center-monitoring.md) — 了解如何監視 Azure 資源的健全狀況。</span><span class="sxs-lookup"><span data-stu-id="cada6-208">[Security health monitoring in Azure Security Center](security-center-monitoring.md) — Learn how to monitor the health of your Azure resources.</span></span>
* <span data-ttu-id="cada6-209">[管理與回應 Azure 資訊安全中心的安全性警示](security-center-managing-and-responding-alerts.md) — 了解如何管理與回應安全性警示。</span><span class="sxs-lookup"><span data-stu-id="cada6-209">[Managing and responding to security alerts in Azure Security Center](security-center-managing-and-responding-alerts.md) — Learn how to manage and respond to security alerts.</span></span>
* <span data-ttu-id="cada6-210">[使用 Azure 資訊安全中心監視合作夥伴解決方案](security-center-partner-solutions.md) — 了解如何監視合作夥伴解決方案的健全狀況。</span><span class="sxs-lookup"><span data-stu-id="cada6-210">[Monitoring partner solutions with Azure Security Center](security-center-partner-solutions.md) — Learn how to monitor the health status of your partner solutions.</span></span>
- <span data-ttu-id="cada6-211">[Azure 資訊安全中心資料安全性](security-center-data-security.md) - 了解資訊安全中心如何管理及保護其中的資料。</span><span class="sxs-lookup"><span data-stu-id="cada6-211">[Azure Security Center data security](security-center-data-security.md) - Learn how data is managed and safeguarded in Security Center.</span></span>
* <span data-ttu-id="cada6-212">[Azure 資訊安全中心常見問題集](security-center-faq.md) — 尋找有關使用服務的常見問題。</span><span class="sxs-lookup"><span data-stu-id="cada6-212">[Azure Security Center FAQ](security-center-faq.md) — Find frequently asked questions about using the service.</span></span>
* <span data-ttu-id="cada6-213">[Azure 安全性部落格](http://blogs.msdn.com/b/azuresecurity/) — 取得最新的 Azure 安全性新聞和資訊。</span><span class="sxs-lookup"><span data-stu-id="cada6-213">[Azure Security blog](http://blogs.msdn.com/b/azuresecurity/) — Get the latest Azure security news and information.</span></span>

<!--Image references-->
[1]: ./media/security-center-intro/security-tile.png
[2]: ./media/security-center-intro/security-center.png
[3]: ./media/security-center-intro/security-policy.png
[4]: ./media/security-center-intro/security-policy-blade.png
[5]: ./media/security-center-intro/recommendations.png
[6]: ./media/security-center-intro/resources-health.png
[7]: ./media/security-center-intro/security-alert.png
[8]: ./media/security-center-intro/security-alert-detail.png
[9]: ./media/security-center-intro/partner-solutions.png
