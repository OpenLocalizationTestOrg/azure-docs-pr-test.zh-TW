---
title: "開始使用 Operations Management Suite 安全性和稽核解決方案 | Microsoft Docs"
description: "本文協助您開始使用 Operations Management Suite 安全性和稽核解決方案功能來監視混合式雲端。"
services: operations-management-suite
documentationcenter: na
author: YuriDio
manager: mbaldwin
editor: 
ms.assetid: 754796ef-a43e-468a-86c9-04a2eda55b5b
ms.service: operations-management-suite
ms.custom: oms-security
ms.topic: get-started-article
ms.devlang: na
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/18/2017
ms.author: yurid
ms.openlocfilehash: eb5283c8f32fddaa8a20a565e4b877821de979a4
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="getting-started-with-operations-management-suite-security-and-audit-solution"></a><span data-ttu-id="60e84-103">開始使用 Operations Management Suite 安全性和稽核解決方案</span><span class="sxs-lookup"><span data-stu-id="60e84-103">Getting started with Operations Management Suite Security and Audit Solution</span></span>
<span data-ttu-id="60e84-104">本文帶領您認識每個選項，協助您快速開始使用 Operations Management Suite (OMS) 安全性和稽核解決方案功能。</span><span class="sxs-lookup"><span data-stu-id="60e84-104">This document helps you get started quickly with Operations Management Suite (OMS) Security and Audit solution capabilities by guiding you through each option.</span></span>

## <a name="what-is-oms"></a><span data-ttu-id="60e84-105">何謂 OMS？</span><span class="sxs-lookup"><span data-stu-id="60e84-105">What is OMS?</span></span>
<span data-ttu-id="60e84-106">Microsoft Operations Management Suite (OMS) 是 Microsoft 的雲端型 IT 管理解決方案，可協助您管理並保護內部部署和雲端基礎結構。</span><span class="sxs-lookup"><span data-stu-id="60e84-106">Microsoft Operations Management Suite (OMS) is Microsoft's cloud-based IT management solution that helps you manage and protect your on-premises and cloud infrastructure.</span></span> <span data-ttu-id="60e84-107">如需 OMS 的詳細資訊，請閱讀 [Operations Management Suite](https://technet.microsoft.com/library/mt484091.aspx)一文。</span><span class="sxs-lookup"><span data-stu-id="60e84-107">For more information about OMS, read the article [Operations Management Suite](https://technet.microsoft.com/library/mt484091.aspx).</span></span>

## <a name="oms-security-and-audit-dashboard"></a><span data-ttu-id="60e84-108">OMS 安全性和稽核儀表板</span><span class="sxs-lookup"><span data-stu-id="60e84-108">OMS Security and Audit dashboard</span></span>
<span data-ttu-id="60e84-109">「OMS 安全性和稽核」解決方案針對值得您注意的問題，使用內建的搜尋查詢，為您組織的 IT 安全性狀況提供全面性的檢視。</span><span class="sxs-lookup"><span data-stu-id="60e84-109">The OMS Security and Audit solution provides a comprehensive view into your organization’s IT security posture with built-in search queries for notable issues that require your attention.</span></span> <span data-ttu-id="60e84-110">[安全性和稽核] 儀表板是 OMS 中所有安全性相關項目的主畫面。</span><span class="sxs-lookup"><span data-stu-id="60e84-110">The **Security and Audit** dashboard is the home screen for everything related to security in OMS.</span></span> <span data-ttu-id="60e84-111">它可讓您深入了解您的電腦的安全性狀態。</span><span class="sxs-lookup"><span data-stu-id="60e84-111">It provides high-level insight into the security state of your computers.</span></span> <span data-ttu-id="60e84-112">它還能夠檢視過去 24 小時、7 天或任何其他自訂時間範圍內的所有事件。</span><span class="sxs-lookup"><span data-stu-id="60e84-112">It also includes the ability to view all events from the past 24 hours, 7 days, or any other custom time frame.</span></span> <span data-ttu-id="60e84-113">若要存取 [安全性和稽核] 儀表板，請遵循下列步驟︰</span><span class="sxs-lookup"><span data-stu-id="60e84-113">To access the **Security and Audit** dashboard, follow these steps:</span></span>

1. <span data-ttu-id="60e84-114">在 [Microsoft Operations Management Suite] 主要儀表板中，按一下左邊的 [設定] 圖格。</span><span class="sxs-lookup"><span data-stu-id="60e84-114">In the **Microsoft Operations Management Suite** main dashboard click **Settings** tile in the left.</span></span>
2. <span data-ttu-id="60e84-115">在 [設定] 刀鋒視窗的 [解決方案] 底下，按一下 [安全性和稽核] 選項。</span><span class="sxs-lookup"><span data-stu-id="60e84-115">In the **Settings** blade, under **Solutions** click **Security and Audit** option.</span></span>
3. <span data-ttu-id="60e84-116">[安全性和稽核] 儀表板隨即出現︰</span><span class="sxs-lookup"><span data-stu-id="60e84-116">The **Security and Audit** dashboard appears:</span></span>
   
    ![OMS 安全性和稽核儀表板](./media/oms-security-getting-started/oms-getting-started-fig1-ga.png)

<span data-ttu-id="60e84-118">如果您第一次存取此儀表板，而且沒有由 OMS 監視的裝置，則圖格中不會填入從代理程式取得的資料。</span><span class="sxs-lookup"><span data-stu-id="60e84-118">If you are accessing this dashboard for the first time and you don’t have devices monitored by OMS, the tiles will not be populated with data obtained from the agent.</span></span> <span data-ttu-id="60e84-119">一旦安裝此代理程式，則可能需要一些時間來填入資料，因此您一開始看到的儀表板可能會遺失一些資料，因為這些資料仍然在上傳至雲端。</span><span class="sxs-lookup"><span data-stu-id="60e84-119">Once you install the agent, it can take some time to populate, therefore what you see initially may be missing some data as they are still uploading to the cloud.</span></span>  <span data-ttu-id="60e84-120">在此情況下，看到一些沒有具體資訊的圖格是很正常的。</span><span class="sxs-lookup"><span data-stu-id="60e84-120">In this case, it is normal to see some tiles without tangible information.</span></span> <span data-ttu-id="60e84-121">請參閱[將 Windows 電腦直接連接到 OMS](https://technet.microsoft.com/library/mt484108.aspx) 以取得如何在 Windows 系統中安裝 OMS 代理程式的詳細資訊，並請參閱[將 Linux 電腦連接到 OMS](https://technet.microsoft.com/library/mt622052.aspx) 以取得如何在 Linux 系統中執行這項工作的詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="60e84-121">Read [Connect Windows computers directly to OMS](https://technet.microsoft.com/library/mt484108.aspx) for more information on how to install OMS agent in a Windows system and [Connect Linux computers to OMS](https://technet.microsoft.com/library/mt622052.aspx) for more information on how to perform this task in a Linux system.</span></span>

> [!NOTE]
> <span data-ttu-id="60e84-122">代理程式會根據目前啟用的事件來收集資訊，例如電腦名稱、IP 位址和使用者名稱。</span><span class="sxs-lookup"><span data-stu-id="60e84-122">The agent collects the information based on the current events that are enabled, for instance computer name, IP address and user name.</span></span> <span data-ttu-id="60e84-123">但不會收集任何文件/檔案、資料庫名稱或私人資料。</span><span class="sxs-lookup"><span data-stu-id="60e84-123">However no document/files, database name or private data are collected.</span></span>   
> 
> 

<span data-ttu-id="60e84-124">解決方案是邏輯、視覺效果和資料擷取規則的集合，可解決客戶所面臨的重要挑戰。</span><span class="sxs-lookup"><span data-stu-id="60e84-124">Solutions are a collection of logic, visualization, and data acquisition rules that address key customer challenges.</span></span> <span data-ttu-id="60e84-125">「安全性和稽核」是其他人可以個別新增的一種解決方案。</span><span class="sxs-lookup"><span data-stu-id="60e84-125">Security and Audit is one solution, others can be added separately.</span></span> <span data-ttu-id="60e84-126">如需有關如何新增解決方案的詳細資訊，請閱讀 [新增解決方案](https://technet.microsoft.com/library/mt674635.aspx) 一文。</span><span class="sxs-lookup"><span data-stu-id="60e84-126">Read the article [Add solutions](https://technet.microsoft.com/library/mt674635.aspx) for more information on how to add a new solution.</span></span>

<span data-ttu-id="60e84-127">OMS 安全性和稽核儀表板分為四個主要類別︰</span><span class="sxs-lookup"><span data-stu-id="60e84-127">The OMS Security and Audit dashboard is organized in four major categories:</span></span>

* <span data-ttu-id="60e84-128">**安全性網域**︰在此區域中，您將能夠進一步探索一段時間的安全性記錄、存取惡意程式碼評估、更新評估、網路安全性、身分識別和存取資訊、具有安全性事件的電腦，以及快速存取 Azure 資訊安全中心儀表板。</span><span class="sxs-lookup"><span data-stu-id="60e84-128">**Security Domains**: in this area you will be able to further explore security records over time, access malware assessment, update assessment, network security, identity and access information, computers with security events and quickly have access to Azure Security Center dashboard.</span></span>
* <span data-ttu-id="60e84-129">**值得注意的問題**︰此選項可讓您快速識別作用中問題數目和這些問題的嚴重性。</span><span class="sxs-lookup"><span data-stu-id="60e84-129">**Notable Issues**: this option will allow you to quickly identify the number of active issues and the severity of these issues.</span></span>
* <span data-ttu-id="60e84-130">**偵測 (預覽)**︰可讓您立即將資源的安全性警示視覺化，進而識別攻擊模式。</span><span class="sxs-lookup"><span data-stu-id="60e84-130">**Detections (Preview)**: enables you to identify attack patterns by visualizing security alerts as they take place against your resources.</span></span>
* <span data-ttu-id="60e84-131">**威脅情報**：可讓您藉由下列方式來識別攻擊模式：視覺化呈現具有惡意輸出 IP 流量的伺服器總數、惡意威脅類型，以及顯示這些 IP 出處的地圖。</span><span class="sxs-lookup"><span data-stu-id="60e84-131">**Threat Intelligence**: enables you to identify attack patterns by visualizing the total number of servers with outbound malicious IP traffic, the malicious threat type and a map that shows where these IPs are coming from.</span></span> 
* <span data-ttu-id="60e84-132">**常見安全性查詢**︰此選項提供最常見安全性查詢的清單，以便用來監視您的環境。</span><span class="sxs-lookup"><span data-stu-id="60e84-132">**Common security queries**: this option provides you a list of the most common security queries that you can use to monitor your environment.</span></span> <span data-ttu-id="60e84-133">當您按一下上述其中一個查詢時，[搜尋] 刀鋒視窗即會開啟，其中包含該查詢的結果。</span><span class="sxs-lookup"><span data-stu-id="60e84-133">When you click in one of those queries, it opens the **Search** blade with the results for that query.</span></span>

> [!NOTE]
> <span data-ttu-id="60e84-134">如需 OMS 如何保留您的資料安全的詳細資訊，請閱讀「OMS 如何保護您的資料」。</span><span class="sxs-lookup"><span data-stu-id="60e84-134">for more information on how OMS keeps your data secure, read How OMS secures your data.</span></span>
> 
> 

## <a name="security-domains"></a><span data-ttu-id="60e84-135">安全性網域</span><span class="sxs-lookup"><span data-stu-id="60e84-135">Security domains</span></span>
<span data-ttu-id="60e84-136">在監視資源時，務必要能夠快速存取您的環境的目前狀態。</span><span class="sxs-lookup"><span data-stu-id="60e84-136">When monitoring resources, it is important to be able to quickly access the current state of your environment.</span></span> <span data-ttu-id="60e84-137">不過，也務必要能夠往回追蹤過去發生的事件，以便進一步了解您的環境在特定時間點發生什麼事情。</span><span class="sxs-lookup"><span data-stu-id="60e84-137">However it is also important to be able to track back events that occurred in the past that can lead to a better understanding of what’s happening in your environment at certain point in time.</span></span> 

> [!NOTE]
> <span data-ttu-id="60e84-138">資料保留會根據 OMS 定價方案。</span><span class="sxs-lookup"><span data-stu-id="60e84-138">data retention is according to the OMS pricing plan.</span></span> <span data-ttu-id="60e84-139">如需詳細資訊，請造訪 [Microsoft Operations Management Suite](https://www.microsoft.com/server-cloud/operations-management-suite/pricing.aspx) 價格頁面。</span><span class="sxs-lookup"><span data-stu-id="60e84-139">For more information visit the [Microsoft Operations Management Suite](https://www.microsoft.com/server-cloud/operations-management-suite/pricing.aspx) pricing page.</span></span>
> 
> 

<span data-ttu-id="60e84-140">事件回應和鑑識調查案例將直接受惠於 [一段時間的安全性記錄]  圖格中可用的結果。</span><span class="sxs-lookup"><span data-stu-id="60e84-140">Incident response and forensics investigation scenarios will directly benefit from the results available in the **Security Records over Time** tile.</span></span>

![一段時間的安全性記錄](./media/oms-security-getting-started/oms-getting-started-fig2.JPG)

<span data-ttu-id="60e84-142">當您按一下此圖格時，[搜尋] 刀鋒視窗會開啟，並根據過去七天的資料顯示 [安全性事件] \(類型=SecurityEvents) 的查詢結果，如下所示︰</span><span class="sxs-lookup"><span data-stu-id="60e84-142">When you click on this tile, the **Search** blade will open, showing a query result for **Security Events** (Type=SecurityEvents) with data based on the last seven days, as shown below:</span></span>

[!include[log-analytics-log-search-nextgeneration](../../includes/log-analytics-log-search-nextgeneration.md)]

![一段時間的安全性記錄](./media/oms-security-getting-started/oms-getting-started-fig3.JPG)

<span data-ttu-id="60e84-144">搜尋結果會分成兩個窗格︰左窗格提供已找到的安全性事件數目細目、找到這些事件的電腦、在這些電腦中發現的帳戶數目及活動類型。</span><span class="sxs-lookup"><span data-stu-id="60e84-144">The search result is divided in two panes: the left pane gives you a breakdown of the number of security events that were found, the computers in which these events were found, the number of accounts that were discovered in these computers and the types of activities.</span></span> <span data-ttu-id="60e84-145">右窗格提供結果總數和安全性事件的時序檢視 (包含電腦的名稱和事件活動)。</span><span class="sxs-lookup"><span data-stu-id="60e84-145">The right pane provides you the total results and a chronological view of the security events with the computer’s name and event activity.</span></span> <span data-ttu-id="60e84-146">您也可以按一下 [顯示更多]  來檢視有關此事件的其他詳細資料，例如事件資料、事件識別碼和事件來源。</span><span class="sxs-lookup"><span data-stu-id="60e84-146">You can also click **Show More** to view more details about this event, such as the event data, the event ID and the event source.</span></span>

> [!NOTE]
> <span data-ttu-id="60e84-147">如需 OMS 搜尋查詢的詳細資訊，請參閱 [OMS 搜尋參考](https://technet.microsoft.com/library/mt450427.aspx)。</span><span class="sxs-lookup"><span data-stu-id="60e84-147">for more information about OMS search query, read [OMS search reference](https://technet.microsoft.com/library/mt450427.aspx).</span></span>
> 
> 

### <a name="antimalware-assessment"></a><span data-ttu-id="60e84-148">反惡意程式碼評估</span><span class="sxs-lookup"><span data-stu-id="60e84-148">Antimalware assessment</span></span>
<span data-ttu-id="60e84-149">此選項可讓您快速識別保護效力不足的電腦，以及遭到惡意程式碼入侵的電腦。</span><span class="sxs-lookup"><span data-stu-id="60e84-149">This option enables you to quickly identify computers with insufficient protection and computers that are compromised by a piece of malware.</span></span> <span data-ttu-id="60e84-150">系統會讀取受監視伺服器上的惡意程式碼評估狀態和偵測到的威脅，然後將資料傳送至雲端中的 OMS 服務，以便進行處理。</span><span class="sxs-lookup"><span data-stu-id="60e84-150">Malware assessment status and detected threats on the monitored servers are read, and then the data is sent to the OMS service in the cloud for processing.</span></span> <span data-ttu-id="60e84-151">偵測到威脅及保護效力不足的伺服器會顯示在惡意程式碼評估儀表板中，在您按一下 [反惡意程式碼評估] 圖格後即可存取該儀表板。</span><span class="sxs-lookup"><span data-stu-id="60e84-151">Servers with detected threats and servers with insufficient protection are shown in the malware assessment dashboard, which is accessible after you click in the **Antimalware Assessment** tile.</span></span> 

![惡意程式碼評估](./media/oms-security-getting-started/oms-getting-started-fig4-ga.png)

<span data-ttu-id="60e84-153">就如同 OMS 儀表板中可用的任何其他即時圖格，當您按一下圖格時，就會開啟包含查詢結果的 [搜尋] 刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="60e84-153">Just like any other live tile available in OMS Dashboard, when you click on it, the **Search** blade will open with the query result.</span></span> <span data-ttu-id="60e84-154">對於此選項，如果您按一下 [保護狀態] 之下的 [未回報] 選項，您的查詢結果會顯示此單一項目，其中包含電腦的名稱與其排名，如下所示︰</span><span class="sxs-lookup"><span data-stu-id="60e84-154">For this option, if you click in the **Not Reporting** option under **Protection Status**, you will have the query result that shows this single entry that contains the computer’s name and its rank, as shown below:</span></span>

![搜尋結果](./media/oms-security-getting-started/oms-getting-started-fig5.png)

> [!NOTE]
> <span data-ttu-id="60e84-156">「排名」是一個等級，可供反映保護的狀態 (開啟、關閉、已更新等) 以及發現的威脅。</span><span class="sxs-lookup"><span data-stu-id="60e84-156">*rank* is a grade giving to reflect the status of the protection (on, off, updated, etc.) and threats that are found.</span></span> <span data-ttu-id="60e84-157">以數字表示有助於進行彙總。</span><span class="sxs-lookup"><span data-stu-id="60e84-157">Having that as a number helps to make aggregations.</span></span>
> 
> 

<span data-ttu-id="60e84-158">如果您按一下電腦名稱，將會取得這部電腦依時間順序排列的保護狀態檢視。</span><span class="sxs-lookup"><span data-stu-id="60e84-158">If you click in the computer’s name, you will have the chronological view of the protection status for this computer.</span></span> <span data-ttu-id="60e84-159">對於需要了解反惡意程式碼是否曾經安裝並在某個時間點移除的情況，這非常實用。</span><span class="sxs-lookup"><span data-stu-id="60e84-159">This is very useful for scenarios in which you need to understand if the antimalware was once installed and at some point it was removed.</span></span>   

### <a name="update-assessment"></a><span data-ttu-id="60e84-160">更新評估</span><span class="sxs-lookup"><span data-stu-id="60e84-160">Update assessment</span></span>
<span data-ttu-id="60e84-161">此選項可讓您快速判斷潛在安全性問題的整體風險，以及或重要性這些更新適用於您的環境。</span><span class="sxs-lookup"><span data-stu-id="60e84-161">This option enables you to quickly determine the overall exposure to potential security problems, and whether or how critical these updates are for your environment.</span></span> <span data-ttu-id="60e84-162">OMS 安全性和稽核解決方案只提供這些更新的視覺效果，而實際資料來自[更新管理解決方案](oms-solution-update-management.md) (這是 OMS 內的不同模組)。</span><span class="sxs-lookup"><span data-stu-id="60e84-162">OMS Security and Audit solution only provide the visualization of these updates, the real data comes from [Update Management Solutions](oms-solution-update-management.md), which is a different module within OMS.</span></span> <span data-ttu-id="60e84-163">以下是更新範例：</span><span class="sxs-lookup"><span data-stu-id="60e84-163">Here an example of the updates:</span></span>

![系統更新](./media/oms-security-getting-started/oms-getting-started-fig6-new.png)

> [!NOTE]
> <span data-ttu-id="60e84-165">如需更新管理解決方案的詳細資訊，請參閱[在 OMS 中更新管理解決方案](oms-solution-update-management.md)。</span><span class="sxs-lookup"><span data-stu-id="60e84-165">For more information about Update Management solution, read [Update Management solution in OMS](oms-solution-update-management.md).</span></span>
> 
> 

### <a name="identity-and-access"></a><span data-ttu-id="60e84-166">身分識別與存取</span><span class="sxs-lookup"><span data-stu-id="60e84-166">Identity and Access</span></span>
<span data-ttu-id="60e84-167">身分識別應該是您的企業的控制台，保護您的身分識別應該是您的第一要務。</span><span class="sxs-lookup"><span data-stu-id="60e84-167">Identity should be the control plane for your enterprise, protecting your identity should be your top priority.</span></span> <span data-ttu-id="60e84-168">雖然過去組織周圍有一些周邊，而這些周邊是其中一個主要防禦界限，但時至今日有更多資料和更多應用程式移到雲端，身分識別便成為新的周邊。</span><span class="sxs-lookup"><span data-stu-id="60e84-168">While in the past there were perimeters around organizations and those perimeters were one of the primary defensive boundaries, nowadays with more data and more apps moving to the cloud the identity becomes the new perimeter.</span></span> 

> [!NOTE]
> <span data-ttu-id="60e84-169">資料目前是以未來 Office365 登入的安全性事件登入資料 (事件識別碼 4624) 為基礎，而 Azure AD 資料也會包含在內。</span><span class="sxs-lookup"><span data-stu-id="60e84-169">currently the data is based only on Security Events login data (event ID 4624) in the future Office365 logins and Azure AD data will also be included.</span></span>
> 
> 

<span data-ttu-id="60e84-170">監視您的身分識別活動，您就能夠在事件發生前採取主動式動作，或採取回應式動作以停止攻擊。</span><span class="sxs-lookup"><span data-stu-id="60e84-170">By monitoring your identity activities you will be able to take proactive actions before an incident takes place or reactive actions to stop an attack attempt.</span></span> <span data-ttu-id="60e84-171">[身分識別和存取] 儀表板會提供您的身分識別狀態概觀，包括嘗試登入失敗的數目、在這些嘗試期間使用的使用者帳戶、已鎖定的帳戶、已變更或重設密碼的帳戶，以及目前登入的帳戶數目。</span><span class="sxs-lookup"><span data-stu-id="60e84-171">The **Identity and Access** dashboard provides you an overview of your identity state, including the number of failed attempts to log on, the user’s account that were used during those attempts, accounts that were locked out, accounts with changed or reset password and currently number of accounts that are logged in.</span></span> 

<span data-ttu-id="60e84-172">當您按一下在 [身分識別和存取] 圖格時，您會看到下列儀表板︰</span><span class="sxs-lookup"><span data-stu-id="60e84-172">When you click in the **Identity and Access** tile you will see the following dashboard:</span></span>

![身分識別與存取](./media/oms-security-getting-started/oms-getting-started-fig7-ga.png)

<span data-ttu-id="60e84-174">此儀表板中可用的資訊可立即協助您識別潛在的可疑活動。</span><span class="sxs-lookup"><span data-stu-id="60e84-174">The information available in this dashboard can immediately assist you to identify a potential suspicious activity.</span></span> <span data-ttu-id="60e84-175">例如，有 338 次嘗試以**系統管理員**身分登入，而這些嘗試 100% 失敗。</span><span class="sxs-lookup"><span data-stu-id="60e84-175">For example, there are 338 attempts to log on as **Administrator** and 100% of these attempts failed.</span></span> <span data-ttu-id="60e84-176">這可能是由暴力密碼破解攻擊這個帳戶所造成。</span><span class="sxs-lookup"><span data-stu-id="60e84-176">This can be caused by a brute force attack against this account.</span></span> <span data-ttu-id="60e84-177">如果您按一下此帳戶，將會取得更多資訊，協助您判斷此潛在攻擊的目標資源︰</span><span class="sxs-lookup"><span data-stu-id="60e84-177">If you click on this account you will obtain more information that can assist you to determine the target resource for this potential attack:</span></span>

![搜尋結果](./media/oms-security-getting-started/oms-getting-started-fig8.JPG)

<span data-ttu-id="60e84-179">詳細報告會提供有關此事件的重要資訊，包括︰目標電腦、登入類型 (在此例中為「網路」登入)、活動 (在此例中為事件 4625) 和每次嘗試的完整時間軸。</span><span class="sxs-lookup"><span data-stu-id="60e84-179">The detailed report provides important information about this event, including: the target computer, the type of logon (in this case Network logon), the activity (in this case event 4625) and a comprehensive timeline of each attempt.</span></span> 

### <a name="computers"></a><span data-ttu-id="60e84-180">電腦</span><span class="sxs-lookup"><span data-stu-id="60e84-180">Computers</span></span>
<span data-ttu-id="60e84-181">此圖格可以用來存取目前有安全性事件的所有電腦。</span><span class="sxs-lookup"><span data-stu-id="60e84-181">This tile can be used to access all computers that actively have security events.</span></span> <span data-ttu-id="60e84-182">當您在此圖格中按一下時，您會看到一份具有安全性事件的電腦清單，以及每部電腦上的事件數目︰</span><span class="sxs-lookup"><span data-stu-id="60e84-182">When you click in this tile you will see the list of computers with security events and the number of events on each computer:</span></span>

![電腦](./media/oms-security-getting-started/oms-getting-started-fig9.JPG)

<span data-ttu-id="60e84-184">您可以按一下每部電腦以繼續調查，並檢閱已加上旗標的安全性事件。</span><span class="sxs-lookup"><span data-stu-id="60e84-184">You can continue your investigation by clicking on each computer and review the security events that were flagged.</span></span>

### <a name="threat-intelligence"></a><span data-ttu-id="60e84-185">威脅情報</span><span class="sxs-lookup"><span data-stu-id="60e84-185">Threat Intelligence</span></span>

<span data-ttu-id="60e84-186">使用 OMS 安全性和稽核中可用的 [威脅情報] 選項，IT 系統管理員可以識別對環境的安全性威脅 (例如，識別特定的電腦是否屬於殭屍網路)。</span><span class="sxs-lookup"><span data-stu-id="60e84-186">By using the Threat Intelligence option available in OMS Security and Audit, IT administrators can identify security threats against the environment, for example, identify if a particular computer is part of a botnet.</span></span> <span data-ttu-id="60e84-187">如果攻擊者偷偷地安裝惡意程式碼，暗中將此電腦連接到命令和控制項，則電腦可能會成為殭屍網路中的節點。</span><span class="sxs-lookup"><span data-stu-id="60e84-187">Computers can become nodes in a botnet when attackers illicitly install malware that secretly connects this computer to the command and control.</span></span> <span data-ttu-id="60e84-188">它也可以識別來自地下通訊通道 (例如暗網) 的潛在威脅。</span><span class="sxs-lookup"><span data-stu-id="60e84-188">It can also identify potential threats coming from underground communication channels, such as darknet.</span></span> <span data-ttu-id="60e84-189">請閱讀[在 Operations Management Suite 安全性和稽核解決方案內監視及回應安全性警示](oms-security-responding-alerts.md)一文，以深入了解威脅情報。</span><span class="sxs-lookup"><span data-stu-id="60e84-189">Learn more about Threat Intelligence by reading [Monitoring and responding to security alerts in Operations Management Suite Security and Audit Solution](oms-security-responding-alerts.md) article.</span></span>

<span data-ttu-id="60e84-190">在某些情況下，您可能會發現已從一部受監視的電腦存取潛在惡意 IP：</span><span class="sxs-lookup"><span data-stu-id="60e84-190">In some scenarios, you may notice a potential malicious IP that was accessed from one monitored computer:</span></span>

![威脅情報對應](./media/oms-security-responding-alerts/oms-security-responding-alerts-fig6.png)

<span data-ttu-id="60e84-192">會透過 OMS 安全性產生此警示以及其他相同類別中的警示，方法是運用 [Microsoft 威脅情報](https://youtu.be/O4WtxgUrDc8)。</span><span class="sxs-lookup"><span data-stu-id="60e84-192">This alert and others within the same category, are generated via OMS Security by leveraging [Microsoft Threat Intelligence](https://youtu.be/O4WtxgUrDc8).</span></span> <span data-ttu-id="60e84-193">威脅情報資料是由 Microsoft 向主要威脅情報提供者所收集及購買。</span><span class="sxs-lookup"><span data-stu-id="60e84-193">The Threat Intelligence data is collected by Microsoft as well as purchased from leading threat intelligence providers.</span></span> <span data-ttu-id="60e84-194">這項資料會經常更新，且適用於快速移動威脅。</span><span class="sxs-lookup"><span data-stu-id="60e84-194">This data is updated frequently and adapted to fast-moving threats.</span></span> <span data-ttu-id="60e84-195">本質上，在[調查](https://blogs.technet.microsoft.com/msoms/2016/12/08/investigating-suspicious-activity-in-a-hybrid-cloud-with-oms-security/)安全性警示時，應將它與其他安全性資訊的來源進行結合。</span><span class="sxs-lookup"><span data-stu-id="60e84-195">Due to its nature, it should be combined with other sources of security information while [investigating](https://blogs.technet.microsoft.com/msoms/2016/12/08/investigating-suspicious-activity-in-a-hybrid-cloud-with-oms-security/) a security alert.</span></span> 

### <a name="baseline-assessment"></a><span data-ttu-id="60e84-196">基準評估</span><span class="sxs-lookup"><span data-stu-id="60e84-196">Baseline Assessment</span></span>

<span data-ttu-id="60e84-197">Microsoft 與全球產業和政府組織共同定義可代表高度安全伺服器部署的 Windows 組態。</span><span class="sxs-lookup"><span data-stu-id="60e84-197">Microsoft, together with industry and government organizations worldwide, defines a Windows configuration that represents highly secure server deployments.</span></span> <span data-ttu-id="60e84-198">此組態是一組登錄機碼、稽核原則設定和安全性原則設定，以及 Microsoft 對於這些設定的建議值。</span><span class="sxs-lookup"><span data-stu-id="60e84-198">This configuration is a set of registry keys, audit policy settings, and security policy settings along with Microsoft’s recommended values for these settings.</span></span> <span data-ttu-id="60e84-199">這組規則也稱為安全性基準。</span><span class="sxs-lookup"><span data-stu-id="60e84-199">This set of rules is known as Security baseline.</span></span> <span data-ttu-id="60e84-200">如需此選項的詳細資訊，請參閱 [Operations Management Suite 安全性和稽核解決方案中的基準評估](oms-security-baseline.md)。</span><span class="sxs-lookup"><span data-stu-id="60e84-200">Read [Baseline Assessment in Operations Management Suite Security and Audit Solution](oms-security-baseline.md) for more information about this option.</span></span>

### <a name="azure-security-center"></a><span data-ttu-id="60e84-201">Azure 資訊安全中心</span><span class="sxs-lookup"><span data-stu-id="60e84-201">Azure Security Center</span></span>
<span data-ttu-id="60e84-202">此圖格基本上是存取 Azure 資訊安全中心儀表板的捷徑。</span><span class="sxs-lookup"><span data-stu-id="60e84-202">This tile is basically a shortcut to access Azure Security Center dashboard.</span></span> <span data-ttu-id="60e84-203">如需此解決方案的詳細資訊，請閱讀 [開始使用 Azure 資訊安全中心](../security-center/security-center-get-started.md) 。</span><span class="sxs-lookup"><span data-stu-id="60e84-203">Read [Getting started with Azure Security Center](../security-center/security-center-get-started.md) for more information about this solution.</span></span>

## <a name="notable-issues"></a><span data-ttu-id="60e84-204">值得注意的問題</span><span class="sxs-lookup"><span data-stu-id="60e84-204">Notable issues</span></span>
<span data-ttu-id="60e84-205">這一組選項的主要目的是提供您環境中問題的快速檢視，並將問題歸類為 [重大]、[警告] 和 [資訊]。</span><span class="sxs-lookup"><span data-stu-id="60e84-205">The main intent of this group of options is to provide a quick view of the issues that you have in your environment, by categorizing them in Critical, Warning and Informational.</span></span> <span data-ttu-id="60e84-206">[作用中問題類型] 圖格是這些問題的視覺呈現，但無法讓您進一步探索其詳細資訊，所以您需要使用此圖格的下半部，其中包含問題的名稱 (名稱)、已發生多少物件 (計數) 與其重要性 (嚴重性)。</span><span class="sxs-lookup"><span data-stu-id="60e84-206">The Active issue type tile it’s a visualization of these issues, but it doesn’t allow you to explore more details about them, for that you need to use the lower part of this tile that has the name of the issue (NAME), how many objects had this happen (COUNT) and how critical it is (SEVERITY).</span></span>

![值得注意的問題](./media/oms-security-getting-started/oms-getting-started-fig10.JPG)

<span data-ttu-id="60e84-208">您可以看到這些問題已涵蓋於 [安全性網域]  群組的不同領域中，以強調此檢視的用意︰從單一位置以視覺化方式呈現您的環境中最重要的問題。</span><span class="sxs-lookup"><span data-stu-id="60e84-208">You can see that these issues were already covered in different areas of the **Security Domains** group, which reinforces the intent of this view: visualize the most important issues in your environment from a single place.</span></span>

## <a name="detections-preview"></a><span data-ttu-id="60e84-209">偵測 (預覽)</span><span class="sxs-lookup"><span data-stu-id="60e84-209">Detections (Preview)</span></span>
<span data-ttu-id="60e84-210">這個選項的主要目的是讓 IT 能藉由威脅的嚴重性，快速識別其環境的潛在威脅。</span><span class="sxs-lookup"><span data-stu-id="60e84-210">The main intent of this option is to allow IT to quickly identify potential threats to their environment via and the severity of this threat.</span></span>

![威脅情報](./media/oms-security-getting-started/oms-getting-started-fig12.png)

<span data-ttu-id="60e84-212">在[事件回應調查](https://blogs.msdn.microsoft.com/azuresecurity/2016/11/30/investigating-suspicious-activity-in-a-hybrid-cloud-with-oms-security/)期間，這個選項也可以用來執行評估並取得有關攻擊的詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="60e84-212">This option can also be used during an [incident response investigation](https://blogs.msdn.microsoft.com/azuresecurity/2016/11/30/investigating-suspicious-activity-in-a-hybrid-cloud-with-oms-security/) to perform the assessment and obtain more information about the attack.</span></span>

> [!NOTE]
> <span data-ttu-id="60e84-213">如需有關如何使用 OMS 進行事件回應的詳細資訊，請觀看此影片：[如何利用 Azure 資訊安全中心和 Microsoft Operations Management Suite 進行事件回應](https://channel9.msdn.com/Blogs/Taste-of-Premier/ToP1703)。</span><span class="sxs-lookup"><span data-stu-id="60e84-213">For more information on how to use OMS for Incident Response, watch this video: [How to Leverage the Azure Security Center & Microsoft Operations Management Suite for an Incident Response](https://channel9.msdn.com/Blogs/Taste-of-Premier/ToP1703).</span></span>
> 
> 

## <a name="threat-intelligence"></a><span data-ttu-id="60e84-214">威脅情報</span><span class="sxs-lookup"><span data-stu-id="60e84-214">Threat Intelligence</span></span>
<span data-ttu-id="60e84-215">「安全性和稽核」解決方案的新威脅情報區段會以數種方式呈現可能的攻擊模式：具有惡意輸出 IP 流量的伺服器總數、惡意威脅類型，以及顯示這些 IP 出處的地圖。</span><span class="sxs-lookup"><span data-stu-id="60e84-215">The new threat intelligence section of the Security and Audit solution visualizes the possible attack patterns in several ways: the total number of servers with outbound malicious IP traffic, the malicious threat type and a map that shows where these IPs are coming from.</span></span> <span data-ttu-id="60e84-216">您可以與地圖互動並按一下 IP 以取得詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="60e84-216">You can interact with the map and click on the IPs for more information.</span></span>

<span data-ttu-id="60e84-217">地圖上的黃色圖釘表示來自惡意 IP 的傳入流量。</span><span class="sxs-lookup"><span data-stu-id="60e84-217">Yellow pushpins on the map indicate incoming traffic from malicious IPs.</span></span> <span data-ttu-id="60e84-218">對於暴露在網際網路中以查看傳入惡意流量的伺服器而言，這也很常見，但建議檢閱這些嘗試以確定全都順利完成。</span><span class="sxs-lookup"><span data-stu-id="60e84-218">It is not uncommon for servers that are exposed to the internet to see incoming malicious traffic, but we recommend reviewing these attempts to make sure none of them was successful.</span></span> <span data-ttu-id="60e84-219">這些指標是以 IIS 記錄、WireData 和 Windows 防火牆記錄為基礎。</span><span class="sxs-lookup"><span data-stu-id="60e84-219">These indicators are based on IIS logs, WireData and Windows Firewall logs.</span></span>  

![威脅情報](./media/oms-security-getting-started/oms-getting-started-fig11-ga.png)

## <a name="common-security-queries"></a><span data-ttu-id="60e84-221">常見安全性查詢</span><span class="sxs-lookup"><span data-stu-id="60e84-221">Common security queries</span></span>
<span data-ttu-id="60e84-222">可用的常用安全性查詢清單可讓您快速存取資源的資訊並根據您的環境需求加以自訂。</span><span class="sxs-lookup"><span data-stu-id="60e84-222">The list of common security queries available can be useful for you to rapidly access resource’s information and customize it based on your environment’s needs.</span></span> <span data-ttu-id="60e84-223">這些常用查詢如下︰</span><span class="sxs-lookup"><span data-stu-id="60e84-223">These common queries are:</span></span>

* <span data-ttu-id="60e84-224">所有安全性活動</span><span class="sxs-lookup"><span data-stu-id="60e84-224">All Security Activities</span></span>
* <span data-ttu-id="60e84-225">電腦 "computer01.contoso.com" (以您自己的電腦名稱取代) 上的安全性活動</span><span class="sxs-lookup"><span data-stu-id="60e84-225">Security Activities on the computer "computer01.contoso.com" (replace with your own computer name)</span></span>
* <span data-ttu-id="60e84-226">帳戶 "Administrator" (以您自己的電腦和帳戶名稱取代) 在電腦 "computer01.contoso.com" (以您自己的電腦名稱取代) 上的安全性活動</span><span class="sxs-lookup"><span data-stu-id="60e84-226">Security Activities on the computer "computer01.contoso.com" for account "Administrator" (replace with your own computer and account names)</span></span>
* <span data-ttu-id="60e84-227">依電腦的登入活動</span><span class="sxs-lookup"><span data-stu-id="60e84-227">Log on Activity by Computer</span></span>
* <span data-ttu-id="60e84-228">在任何電腦上終止 Microsoft 反惡意程式碼的帳戶</span><span class="sxs-lookup"><span data-stu-id="60e84-228">Accounts who terminated Microsoft antimalware on any computer</span></span>
* <span data-ttu-id="60e84-229">已終止 Microsoft 反惡意程式碼程序的電腦</span><span class="sxs-lookup"><span data-stu-id="60e84-229">Computers where the Microsoft antimalware process was terminated</span></span>
* <span data-ttu-id="60e84-230">已執行 "hash.exe" 的電腦 (以不同的處理序名稱取代)</span><span class="sxs-lookup"><span data-stu-id="60e84-230">Computers where "hash.exe" was executed (replace with different process name)</span></span>
* <span data-ttu-id="60e84-231">已執行的所有處理序名稱</span><span class="sxs-lookup"><span data-stu-id="60e84-231">All Process names that were executed</span></span>
* <span data-ttu-id="60e84-232">依帳戶的登入活動</span><span class="sxs-lookup"><span data-stu-id="60e84-232">Log on Activity by Account</span></span>
* <span data-ttu-id="60e84-233">從遠端登入電腦 "computer01.contoso.com" (以您自己的電腦名稱取代) 的帳戶</span><span class="sxs-lookup"><span data-stu-id="60e84-233">Accounts who remotely logged on the computer "computer01.contoso.com" (replace with your own computer name)</span></span>

## <a name="see-also"></a><span data-ttu-id="60e84-234">另請參閱</span><span class="sxs-lookup"><span data-stu-id="60e84-234">See also</span></span>
<span data-ttu-id="60e84-235">在本文件中，已向您介紹 OMS 安全性和稽核解決方案。</span><span class="sxs-lookup"><span data-stu-id="60e84-235">In this document, you were introduced to OMS Security and Audit solution.</span></span> <span data-ttu-id="60e84-236">若要深入了解 OMS 安全性，請參閱下列文章：</span><span class="sxs-lookup"><span data-stu-id="60e84-236">To learn more about OMS Security, see the following articles:</span></span>

* [<span data-ttu-id="60e84-237">Operations Management Suite (OMS) 概觀</span><span class="sxs-lookup"><span data-stu-id="60e84-237">Operations Management Suite (OMS) overview</span></span>](operations-management-suite-overview.md)
* [<span data-ttu-id="60e84-238">在 Operations Management Suite 安全性和稽核內監視及回應安全性警示</span><span class="sxs-lookup"><span data-stu-id="60e84-238">Monitoring and Responding to Security Alerts in Operations Management Suite Security and Audit Solution</span></span>](oms-security-responding-alerts.md)
* [<span data-ttu-id="60e84-239">在 Operations Management Suite 安全性和稽核解決方案內監視資源</span><span class="sxs-lookup"><span data-stu-id="60e84-239">Monitoring Resources in Operations Management Suite Security and Audit Solution</span></span>](oms-security-monitoring-resources.md)

