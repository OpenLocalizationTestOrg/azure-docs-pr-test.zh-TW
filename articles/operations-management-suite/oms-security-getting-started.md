---
title: "aaaGetting 開始使用 Operations Management Suite 安全性和稽核解決方案 |Microsoft 文件"
description: "此文件將協助您 tooget 入門 Operations Management Suite 安全性和稽核解決方案功能 toomonitor 混合式雲端。"
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
ms.openlocfilehash: 5cb3e5dbb3e60f9702a34c9413ddc1bf2b14b411
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="getting-started-with-operations-management-suite-security-and-audit-solution"></a><span data-ttu-id="5aa12-103">開始使用 Operations Management Suite 安全性和稽核解決方案</span><span class="sxs-lookup"><span data-stu-id="5aa12-103">Getting started with Operations Management Suite Security and Audit Solution</span></span>
<span data-ttu-id="5aa12-104">本文帶領您認識每個選項，協助您快速開始使用 Operations Management Suite (OMS) 安全性和稽核解決方案功能。</span><span class="sxs-lookup"><span data-stu-id="5aa12-104">This document helps you get started quickly with Operations Management Suite (OMS) Security and Audit solution capabilities by guiding you through each option.</span></span>

## <a name="what-is-oms"></a><span data-ttu-id="5aa12-105">何謂 OMS？</span><span class="sxs-lookup"><span data-stu-id="5aa12-105">What is OMS?</span></span>
<span data-ttu-id="5aa12-106">Microsoft Operations Management Suite (OMS) 是 Microsoft 的雲端型 IT 管理解決方案，可協助您管理並保護內部部署和雲端基礎結構。</span><span class="sxs-lookup"><span data-stu-id="5aa12-106">Microsoft Operations Management Suite (OMS) is Microsoft's cloud-based IT management solution that helps you manage and protect your on-premises and cloud infrastructure.</span></span> <span data-ttu-id="5aa12-107">關於 OMS 的詳細資訊，請參閱 hello 文章[Operations Management Suite](https://technet.microsoft.com/library/mt484091.aspx)。</span><span class="sxs-lookup"><span data-stu-id="5aa12-107">For more information about OMS, read hello article [Operations Management Suite](https://technet.microsoft.com/library/mt484091.aspx).</span></span>

## <a name="oms-security-and-audit-dashboard"></a><span data-ttu-id="5aa12-108">OMS 安全性和稽核儀表板</span><span class="sxs-lookup"><span data-stu-id="5aa12-108">OMS Security and Audit dashboard</span></span>
<span data-ttu-id="5aa12-109">hello OMS 安全性和稽核 」 解決方案可讓您完整檢視組織的 IT 安全性狀況，針對值得您注意的問題使用內建的搜尋查詢。</span><span class="sxs-lookup"><span data-stu-id="5aa12-109">hello OMS Security and Audit solution provides a comprehensive view into your organization’s IT security posture with built-in search queries for notable issues that require your attention.</span></span> <span data-ttu-id="5aa12-110">hello**安全性和稽核**儀表板是所有項目 hello 主畫面相關 toosecurity 在 OMS 中的。</span><span class="sxs-lookup"><span data-stu-id="5aa12-110">hello **Security and Audit** dashboard is hello home screen for everything related toosecurity in OMS.</span></span> <span data-ttu-id="5aa12-111">會提供在電腦的 hello 安全性狀態的高層級深入。</span><span class="sxs-lookup"><span data-stu-id="5aa12-111">It provides high-level insight into hello security state of your computers.</span></span> <span data-ttu-id="5aa12-112">它也包含 hello 能力 tooview hello 過去 24 小時、 7 天的所有事件或任何其他自訂的時間範圍。</span><span class="sxs-lookup"><span data-stu-id="5aa12-112">It also includes hello ability tooview all events from hello past 24 hours, 7 days, or any other custom time frame.</span></span> <span data-ttu-id="5aa12-113">tooaccess hello**安全性和稽核**儀表板，請遵循下列步驟：</span><span class="sxs-lookup"><span data-stu-id="5aa12-113">tooaccess hello **Security and Audit** dashboard, follow these steps:</span></span>

1. <span data-ttu-id="5aa12-114">在 hello **Microsoft Operations Management Suite**主要儀表板按一下**設定**hello 方的磚。</span><span class="sxs-lookup"><span data-stu-id="5aa12-114">In hello **Microsoft Operations Management Suite** main dashboard click **Settings** tile in hello left.</span></span>
2. <span data-ttu-id="5aa12-115">在 hello**設定**刀鋒視窗底下**解決方案**按一下**安全性和稽核**選項。</span><span class="sxs-lookup"><span data-stu-id="5aa12-115">In hello **Settings** blade, under **Solutions** click **Security and Audit** option.</span></span>
3. <span data-ttu-id="5aa12-116">hello**安全性和稽核**儀表板會顯示：</span><span class="sxs-lookup"><span data-stu-id="5aa12-116">hello **Security and Audit** dashboard appears:</span></span>
   
    ![OMS 安全性和稽核儀表板](./media/oms-security-getting-started/oms-getting-started-fig1-ga.png)

<span data-ttu-id="5aa12-118">如果您要存取此儀表板 hello 第一次，您不需要 OMS 監視的裝置 hello 磚將不會填入取自 hello 代理程式的資料。</span><span class="sxs-lookup"><span data-stu-id="5aa12-118">If you are accessing this dashboard for hello first time and you don’t have devices monitored by OMS, hello tiles will not be populated with data obtained from hello agent.</span></span> <span data-ttu-id="5aa12-119">一旦您安裝 hello 代理程式時，可能需要一些時間 toopopulate，因此您看到一開始可能會遺失某些資料因為它們仍在上傳 toohello 雲端。</span><span class="sxs-lookup"><span data-stu-id="5aa12-119">Once you install hello agent, it can take some time toopopulate, therefore what you see initially may be missing some data as they are still uploading toohello cloud.</span></span>  <span data-ttu-id="5aa12-120">在此情況下，它是一般 toosee 某些磚沒有具體的資訊。</span><span class="sxs-lookup"><span data-stu-id="5aa12-120">In this case, it is normal toosee some tiles without tangible information.</span></span> <span data-ttu-id="5aa12-121">讀取[連接的 Windows 電腦直接 tooOMS](https://technet.microsoft.com/library/mt484108.aspx)如需有關如何 tooinstall OMS 代理程式在 Windows 系統和[連線 Linux 電腦 tooOMS](https://technet.microsoft.com/library/mt622052.aspx)如需有關如何 tooperform 這項工作在 Linux 系統中。</span><span class="sxs-lookup"><span data-stu-id="5aa12-121">Read [Connect Windows computers directly tooOMS](https://technet.microsoft.com/library/mt484108.aspx) for more information on how tooinstall OMS agent in a Windows system and [Connect Linux computers tooOMS](https://technet.microsoft.com/library/mt622052.aspx) for more information on how tooperform this task in a Linux system.</span></span>

> [!NOTE]
> <span data-ttu-id="5aa12-122">hello 代理程式會收集 hello 資訊根據 hello 目前事件已啟用，例如電腦名稱、 IP 位址和使用者名稱。</span><span class="sxs-lookup"><span data-stu-id="5aa12-122">hello agent collects hello information based on hello current events that are enabled, for instance computer name, IP address and user name.</span></span> <span data-ttu-id="5aa12-123">但不會收集任何文件/檔案、資料庫名稱或私人資料。</span><span class="sxs-lookup"><span data-stu-id="5aa12-123">However no document/files, database name or private data are collected.</span></span>   
> 
> 

<span data-ttu-id="5aa12-124">解決方案是邏輯、視覺效果和資料擷取規則的集合，可解決客戶所面臨的重要挑戰。</span><span class="sxs-lookup"><span data-stu-id="5aa12-124">Solutions are a collection of logic, visualization, and data acquisition rules that address key customer challenges.</span></span> <span data-ttu-id="5aa12-125">「安全性和稽核」是其他人可以個別新增的一種解決方案。</span><span class="sxs-lookup"><span data-stu-id="5aa12-125">Security and Audit is one solution, others can be added separately.</span></span> <span data-ttu-id="5aa12-126">閱讀文章 hello[新增解決方案](https://technet.microsoft.com/library/mt674635.aspx)如需有關如何 tooadd 新方案。</span><span class="sxs-lookup"><span data-stu-id="5aa12-126">Read hello article [Add solutions](https://technet.microsoft.com/library/mt674635.aspx) for more information on how tooadd a new solution.</span></span>

<span data-ttu-id="5aa12-127">hello OMS 安全性和稽核儀表板分為四個主要類別：</span><span class="sxs-lookup"><span data-stu-id="5aa12-127">hello OMS Security and Audit dashboard is organized in four major categories:</span></span>

* <span data-ttu-id="5aa12-128">**安全性網域**： 在此區域中，您將無法能 toofurther 探索安全性記錄一段時間，存取惡意程式碼評估、 更新評估、 網路安全性、 身分識別和存取資訊、 電腦與安全性事件並能快速地存取 tooAzure 資訊安全中心儀表板。</span><span class="sxs-lookup"><span data-stu-id="5aa12-128">**Security Domains**: in this area you will be able toofurther explore security records over time, access malware assessment, update assessment, network security, identity and access information, computers with security events and quickly have access tooAzure Security Center dashboard.</span></span>
* <span data-ttu-id="5aa12-129">**值得注意的問題**： 此選項可讓您 tooquickly 識別作用中問題的 hello 數目和 hello 這些問題的嚴重性。</span><span class="sxs-lookup"><span data-stu-id="5aa12-129">**Notable Issues**: this option will allow you tooquickly identify hello number of active issues and hello severity of these issues.</span></span>
* <span data-ttu-id="5aa12-130">**偵測 （預覽）**： 可讓您透過視覺化安全性警示，因為它們對您的資源進行的 tooidentify 攻擊的模式。</span><span class="sxs-lookup"><span data-stu-id="5aa12-130">**Detections (Preview)**: enables you tooidentify attack patterns by visualizing security alerts as they take place against your resources.</span></span>
* <span data-ttu-id="5aa12-131">**威脅情報**： 可讓您所視覺化的具有惡意連出 IP 流量、 hello 惡意之威脅類型和顯示來自這些 Ip 其中的對應伺服器 hello 總數的 tooidentify 攻擊的模式。</span><span class="sxs-lookup"><span data-stu-id="5aa12-131">**Threat Intelligence**: enables you tooidentify attack patterns by visualizing hello total number of servers with outbound malicious IP traffic, hello malicious threat type and a map that shows where these IPs are coming from.</span></span> 
* <span data-ttu-id="5aa12-132">**常見安全性查詢**： 這個選項提供您一份 hello 最常見安全性查詢，您可以使用 toomonitor 您的環境。</span><span class="sxs-lookup"><span data-stu-id="5aa12-132">**Common security queries**: this option provides you a list of hello most common security queries that you can use toomonitor your environment.</span></span> <span data-ttu-id="5aa12-133">當您按一下其中一個這些查詢中時，它會開啟 hello**搜尋**hello 結果該查詢的刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="5aa12-133">When you click in one of those queries, it opens hello **Search** blade with hello results for that query.</span></span>

> [!NOTE]
> <span data-ttu-id="5aa12-134">如需 OMS 如何保留您的資料安全的詳細資訊，請閱讀「OMS 如何保護您的資料」。</span><span class="sxs-lookup"><span data-stu-id="5aa12-134">for more information on how OMS keeps your data secure, read How OMS secures your data.</span></span>
> 
> 

## <a name="security-domains"></a><span data-ttu-id="5aa12-135">安全性網域</span><span class="sxs-lookup"><span data-stu-id="5aa12-135">Security domains</span></span>
<span data-ttu-id="5aa12-136">監視資源時，重要 toobe 無法 tooquickly 存取 hello 目前狀態的環境。</span><span class="sxs-lookup"><span data-stu-id="5aa12-136">When monitoring resources, it is important toobe able tooquickly access hello current state of your environment.</span></span> <span data-ttu-id="5aa12-137">不過也很重要的 toobe 無法 tootrack 後發生的事件，hello 過去可能導致 tooa 進一步了解這為什麼在特定時間點您環境中的時間。</span><span class="sxs-lookup"><span data-stu-id="5aa12-137">However it is also important toobe able tootrack back events that occurred in hello past that can lead tooa better understanding of what’s happening in your environment at certain point in time.</span></span> 

> [!NOTE]
> <span data-ttu-id="5aa12-138">資料保留根據 toohello OMS 定價方案。</span><span class="sxs-lookup"><span data-stu-id="5aa12-138">data retention is according toohello OMS pricing plan.</span></span> <span data-ttu-id="5aa12-139">如需詳細資訊，請造訪 hello [Microsoft Operations Management Suite](https://www.microsoft.com/server-cloud/operations-management-suite/pricing.aspx)定價頁面。</span><span class="sxs-lookup"><span data-stu-id="5aa12-139">For more information visit hello [Microsoft Operations Management Suite](https://www.microsoft.com/server-cloud/operations-management-suite/pricing.aspx) pricing page.</span></span>
> 
> 

<span data-ttu-id="5aa12-140">事件的回應和鑑識調查情況直接將從中獲益 hello 結果會提供在 hello**經過一段時間的安全性記錄**磚。</span><span class="sxs-lookup"><span data-stu-id="5aa12-140">Incident response and forensics investigation scenarios will directly benefit from hello results available in hello **Security Records over Time** tile.</span></span>

![一段時間的安全性記錄](./media/oms-security-getting-started/oms-getting-started-fig2.JPG)

<span data-ttu-id="5aa12-142">當您按一下這個磚時，hello**搜尋**隨即會開啟刀鋒視窗，顯示查詢結果**安全性事件**(類型 = SecurityEvents) 與資料是根據 hello 過去七天，如下所示：</span><span class="sxs-lookup"><span data-stu-id="5aa12-142">When you click on this tile, hello **Search** blade will open, showing a query result for **Security Events** (Type=SecurityEvents) with data based on hello last seven days, as shown below:</span></span>

[!include[log-analytics-log-search-nextgeneration](../../includes/log-analytics-log-search-nextgeneration.md)]

![一段時間的安全性記錄](./media/oms-security-getting-started/oms-getting-started-fig3.JPG)

<span data-ttu-id="5aa12-144">hello 搜尋結果會分割成兩個窗格： hello 的左的窗格可讓您找不到，hello 電腦中的這些事件找不到，帳戶所探索到這些電腦中的 hello 數目和 hello 類型的安全性事件的 hello 數目的細目活動。</span><span class="sxs-lookup"><span data-stu-id="5aa12-144">hello search result is divided in two panes: hello left pane gives you a breakdown of hello number of security events that were found, hello computers in which these events were found, hello number of accounts that were discovered in these computers and hello types of activities.</span></span> <span data-ttu-id="5aa12-145">hello 右窗格會提供您 hello 總結果和 hello 電腦的名稱和事件的活動與 hello 安全性事件的時間檢視。</span><span class="sxs-lookup"><span data-stu-id="5aa12-145">hello right pane provides you hello total results and a chronological view of hello security events with hello computer’s name and event activity.</span></span> <span data-ttu-id="5aa12-146">您也可以按一下**顯示更多**tooview 更詳細說明有關此事件，例如 hello 事件資料、 hello 事件識別碼和 hello 事件來源。</span><span class="sxs-lookup"><span data-stu-id="5aa12-146">You can also click **Show More** tooview more details about this event, such as hello event data, hello event ID and hello event source.</span></span>

> [!NOTE]
> <span data-ttu-id="5aa12-147">如需 OMS 搜尋查詢的詳細資訊，請參閱 [OMS 搜尋參考](https://technet.microsoft.com/library/mt450427.aspx)。</span><span class="sxs-lookup"><span data-stu-id="5aa12-147">for more information about OMS search query, read [OMS search reference](https://technet.microsoft.com/library/mt450427.aspx).</span></span>
> 
> 

### <a name="antimalware-assessment"></a><span data-ttu-id="5aa12-148">反惡意程式碼評估</span><span class="sxs-lookup"><span data-stu-id="5aa12-148">Antimalware assessment</span></span>
<span data-ttu-id="5aa12-149">此選項會啟用您 tooquickly 識別電腦和保護不足和都遭到惡意軟體的電腦。</span><span class="sxs-lookup"><span data-stu-id="5aa12-149">This option enables you tooquickly identify computers with insufficient protection and computers that are compromised by a piece of malware.</span></span> <span data-ttu-id="5aa12-150">惡意程式碼評估狀態 hello 監視伺服器上偵測到的威脅閱讀，並再 hello 資料會傳送 toohello OMS 服務進行處理的 hello 雲端中。</span><span class="sxs-lookup"><span data-stu-id="5aa12-150">Malware assessment status and detected threats on hello monitored servers are read, and then hello data is sent toohello OMS service in hello cloud for processing.</span></span> <span data-ttu-id="5aa12-151">偵測到威脅及保護效力不足的伺服器會顯示 hello 惡意程式碼評定儀表板中，也就是可存取在 hello 按一下後**反惡意程式碼評定**磚。</span><span class="sxs-lookup"><span data-stu-id="5aa12-151">Servers with detected threats and servers with insufficient protection are shown in hello malware assessment dashboard, which is accessible after you click in hello **Antimalware Assessment** tile.</span></span> 

![惡意程式碼評估](./media/oms-security-getting-started/oms-getting-started-fig4-ga.png)

<span data-ttu-id="5aa12-153">就像任何其他動態磚提供 OMS 儀表板中，當您按一下它，hello**搜尋**hello 查詢結果將會開啟刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="5aa12-153">Just like any other live tile available in OMS Dashboard, when you click on it, hello **Search** blade will open with hello query result.</span></span> <span data-ttu-id="5aa12-154">針對這個選項，如果您按一下 hello**未回報**選項在**保護狀態**，您必須 hello 查詢結果會顯示包含 hello 電腦的名稱和其陣序規範，與此單一項目如下所示：</span><span class="sxs-lookup"><span data-stu-id="5aa12-154">For this option, if you click in hello **Not Reporting** option under **Protection Status**, you will have hello query result that shows this single entry that contains hello computer’s name and its rank, as shown below:</span></span>

![搜尋結果](./media/oms-security-getting-started/oms-getting-started-fig5.png)

> [!NOTE]
> <span data-ttu-id="5aa12-156">*順位*是提供 tooreflect hello 狀態的 hello 保護等級 （on、 off、 更新，等等） 以及發現的威脅。</span><span class="sxs-lookup"><span data-stu-id="5aa12-156">*rank* is a grade giving tooreflect hello status of hello protection (on, off, updated, etc.) and threats that are found.</span></span> <span data-ttu-id="5aa12-157">讓，成為數字的協助 toomake 彙總。</span><span class="sxs-lookup"><span data-stu-id="5aa12-157">Having that as a number helps toomake aggregations.</span></span>
> 
> 

<span data-ttu-id="5aa12-158">如果您按一下 hello 電腦名稱中，您必須 hello hello 保護狀態，此電腦的時間檢視。</span><span class="sxs-lookup"><span data-stu-id="5aa12-158">If you click in hello computer’s name, you will have hello chronological view of hello protection status for this computer.</span></span> <span data-ttu-id="5aa12-159">這是非常有用的案例，您需要 toounderstand 如果 hello 反惡意程式碼曾安裝，以及在某個時間點已移除。</span><span class="sxs-lookup"><span data-stu-id="5aa12-159">This is very useful for scenarios in which you need toounderstand if hello antimalware was once installed and at some point it was removed.</span></span>   

### <a name="update-assessment"></a><span data-ttu-id="5aa12-160">更新評估</span><span class="sxs-lookup"><span data-stu-id="5aa12-160">Update assessment</span></span>
<span data-ttu-id="5aa12-161">此選項可讓您 tooquickly 判斷 hello 整體曝光 toopotential 安全性問題，以及是否或重要性這些更新適用於您的環境。</span><span class="sxs-lookup"><span data-stu-id="5aa12-161">This option enables you tooquickly determine hello overall exposure toopotential security problems, and whether or how critical these updates are for your environment.</span></span> <span data-ttu-id="5aa12-162">OMS 安全性和稽核解決方案只提供這些更新的 hello 視覺效果、 hello 實際資料是來自[更新管理解決方案](oms-solution-update-management.md)，這是在不同的模組，在 OMS 中。</span><span class="sxs-lookup"><span data-stu-id="5aa12-162">OMS Security and Audit solution only provide hello visualization of these updates, hello real data comes from [Update Management Solutions](oms-solution-update-management.md), which is a different module within OMS.</span></span> <span data-ttu-id="5aa12-163">這裡 hello 更新的範例：</span><span class="sxs-lookup"><span data-stu-id="5aa12-163">Here an example of hello updates:</span></span>

![系統更新](./media/oms-security-getting-started/oms-getting-started-fig6-new.png)

> [!NOTE]
> <span data-ttu-id="5aa12-165">如需更新管理解決方案的詳細資訊，請參閱[在 OMS 中更新管理解決方案](oms-solution-update-management.md)。</span><span class="sxs-lookup"><span data-stu-id="5aa12-165">For more information about Update Management solution, read [Update Management solution in OMS](oms-solution-update-management.md).</span></span>
> 
> 

### <a name="identity-and-access"></a><span data-ttu-id="5aa12-166">身分識別與存取</span><span class="sxs-lookup"><span data-stu-id="5aa12-166">Identity and Access</span></span>
<span data-ttu-id="5aa12-167">識別應與 hello 控制您的企業，保護您的身分識別的平面應為您的優先考量。</span><span class="sxs-lookup"><span data-stu-id="5aa12-167">Identity should be hello control plane for your enterprise, protecting your identity should be your top priority.</span></span> <span data-ttu-id="5aa12-168">雖然在 hello 過去發生周圍組織的周邊和這些周邊是其中一個 hello 主要防禦界限，screen 鍵移動 toohello 雲端的更多應用程式詳細資料與 hello 身分識別會變得 hello 新周邊。</span><span class="sxs-lookup"><span data-stu-id="5aa12-168">While in hello past there were perimeters around organizations and those perimeters were one of hello primary defensive boundaries, nowadays with more data and more apps moving toohello cloud hello identity becomes hello new perimeter.</span></span> 

> [!NOTE]
> <span data-ttu-id="5aa12-169">目前 hello 資料只會根據在 hello 未來 Office365 登入的安全性事件登入資料 （事件識別碼 4624），Azure AD 資料也會包含在內。</span><span class="sxs-lookup"><span data-stu-id="5aa12-169">currently hello data is based only on Security Events login data (event ID 4624) in hello future Office365 logins and Azure AD data will also be included.</span></span>
> 
> 

<span data-ttu-id="5aa12-170">監視您的身分識別活動您會無法 tootake 預防措施事件之前或反應動作 toostop 攻擊。</span><span class="sxs-lookup"><span data-stu-id="5aa12-170">By monitoring your identity activities you will be able tootake proactive actions before an incident takes place or reactive actions toostop an attack attempt.</span></span> <span data-ttu-id="5aa12-171">hello**身分識別和存取**儀表板會提供您的身分識別狀態，包括 hello 期間每次嘗試後，帳戶已鎖定，所使用的 hello 使用者帳戶上的失敗的嘗試 toolog 數目的概觀具有帳戶變更或重設密碼和目前的登入的帳戶數目。</span><span class="sxs-lookup"><span data-stu-id="5aa12-171">hello **Identity and Access** dashboard provides you an overview of your identity state, including hello number of failed attempts toolog on, hello user’s account that were used during those attempts, accounts that were locked out, accounts with changed or reset password and currently number of accounts that are logged in.</span></span> 

<span data-ttu-id="5aa12-172">當您按一下在 hello**身分識別和存取**您會看到 hello 下列儀表板的磚：</span><span class="sxs-lookup"><span data-stu-id="5aa12-172">When you click in hello **Identity and Access** tile you will see hello following dashboard:</span></span>

![身分識別與存取](./media/oms-security-getting-started/oms-getting-started-fig7-ga.png)

<span data-ttu-id="5aa12-174">此儀表板中可用的 hello 資訊可以立即協助 tooidentify 潛在可疑的活動。</span><span class="sxs-lookup"><span data-stu-id="5aa12-174">hello information available in this dashboard can immediately assist you tooidentify a potential suspicious activity.</span></span> <span data-ttu-id="5aa12-175">例如，有 338 嘗試 toolog 上做為**管理員**和 100%的這些嘗試失敗。</span><span class="sxs-lookup"><span data-stu-id="5aa12-175">For example, there are 338 attempts toolog on as **Administrator** and 100% of these attempts failed.</span></span> <span data-ttu-id="5aa12-176">這可能是由暴力密碼破解攻擊這個帳戶所造成。</span><span class="sxs-lookup"><span data-stu-id="5aa12-176">This can be caused by a brute force attack against this account.</span></span> <span data-ttu-id="5aa12-177">如果您按一下此帳戶將會取得詳細的資訊可協助您 toodetermine hello 目標資源的潛在攻擊：</span><span class="sxs-lookup"><span data-stu-id="5aa12-177">If you click on this account you will obtain more information that can assist you toodetermine hello target resource for this potential attack:</span></span>

![搜尋結果](./media/oms-security-getting-started/oms-getting-started-fig8.JPG)

<span data-ttu-id="5aa12-179">hello 詳細資料報表提供關於這個事件中，重要的資訊包括： hello 目標電腦、 hello 類型 （在此案例的網路登入） 的登入]、 [hello 活動 （在此案例事件 4625） 以及每次嘗試的完整時間軸。</span><span class="sxs-lookup"><span data-stu-id="5aa12-179">hello detailed report provides important information about this event, including: hello target computer, hello type of logon (in this case Network logon), hello activity (in this case event 4625) and a comprehensive timeline of each attempt.</span></span> 

### <a name="computers"></a><span data-ttu-id="5aa12-180">電腦</span><span class="sxs-lookup"><span data-stu-id="5aa12-180">Computers</span></span>
<span data-ttu-id="5aa12-181">這張牌可以是使用的 tooaccess 主動具有安全性事件的所有電腦。</span><span class="sxs-lookup"><span data-stu-id="5aa12-181">This tile can be used tooaccess all computers that actively have security events.</span></span> <span data-ttu-id="5aa12-182">當您按一下此磚中您會看到每一部電腦上的 hello 與安全性事件和事件的 hello 數目的電腦清單：</span><span class="sxs-lookup"><span data-stu-id="5aa12-182">When you click in this tile you will see hello list of computers with security events and hello number of events on each computer:</span></span>

![電腦](./media/oms-security-getting-started/oms-getting-started-fig9.JPG)

<span data-ttu-id="5aa12-184">您可以在每一部電腦上，即可繼續調查程式，並檢閱已加上旗標的 hello 安全性事件。</span><span class="sxs-lookup"><span data-stu-id="5aa12-184">You can continue your investigation by clicking on each computer and review hello security events that were flagged.</span></span>

### <a name="threat-intelligence"></a><span data-ttu-id="5aa12-185">威脅情報</span><span class="sxs-lookup"><span data-stu-id="5aa12-185">Threat Intelligence</span></span>

<span data-ttu-id="5aa12-186">藉由使用 hello 威脅情報選項可以在 OMS 安全性和稽核，IT 系統管理員可以識別針對 hello 環境的安全性威脅，例如，必須識別特定的電腦是否殭屍網路的一部分。</span><span class="sxs-lookup"><span data-stu-id="5aa12-186">By using hello Threat Intelligence option available in OMS Security and Audit, IT administrators can identify security threats against hello environment, for example, identify if a particular computer is part of a botnet.</span></span> <span data-ttu-id="5aa12-187">當攻擊者非法地安裝惡意軟體偷偷地連接此電腦 toohello 命令和控制項時，電腦可能會變成殭屍網路中的節點。</span><span class="sxs-lookup"><span data-stu-id="5aa12-187">Computers can become nodes in a botnet when attackers illicitly install malware that secretly connects this computer toohello command and control.</span></span> <span data-ttu-id="5aa12-188">它也可以識別來自地下通訊通道 (例如暗網) 的潛在威脅。</span><span class="sxs-lookup"><span data-stu-id="5aa12-188">It can also identify potential threats coming from underground communication channels, such as darknet.</span></span> <span data-ttu-id="5aa12-189">深入了解威脅情報閱讀[Operations Management Suite 安全性和稽核解決方案中的監視和回應 toosecurity 警示](oms-security-responding-alerts.md)發行項。</span><span class="sxs-lookup"><span data-stu-id="5aa12-189">Learn more about Threat Intelligence by reading [Monitoring and responding toosecurity alerts in Operations Management Suite Security and Audit Solution](oms-security-responding-alerts.md) article.</span></span>

<span data-ttu-id="5aa12-190">在某些情況下，您可能會發現已從一部受監視的電腦存取潛在惡意 IP：</span><span class="sxs-lookup"><span data-stu-id="5aa12-190">In some scenarios, you may notice a potential malicious IP that was accessed from one monitored computer:</span></span>

![威脅情報對應](./media/oms-security-responding-alerts/oms-security-responding-alerts-fig6.png)

<span data-ttu-id="5aa12-192">此警示和其他人在 hello 相同類別目錄，利用透過 OMS 安全性會產生[Microsoft 威脅情報](https://youtu.be/O4WtxgUrDc8)。</span><span class="sxs-lookup"><span data-stu-id="5aa12-192">This alert and others within hello same category, are generated via OMS Security by leveraging [Microsoft Threat Intelligence](https://youtu.be/O4WtxgUrDc8).</span></span> <span data-ttu-id="5aa12-193">hello 威脅情報資料是 Microsoft 所收集，以及主要威脅情報提供者購買。</span><span class="sxs-lookup"><span data-stu-id="5aa12-193">hello Threat Intelligence data is collected by Microsoft as well as purchased from leading threat intelligence providers.</span></span> <span data-ttu-id="5aa12-194">這項資料會經常更新，並調整 toofast 移動的威脅。</span><span class="sxs-lookup"><span data-stu-id="5aa12-194">This data is updated frequently and adapted toofast-moving threats.</span></span> <span data-ttu-id="5aa12-195">Tooits 本質，因為它應與結合其他來源的安全性資訊時[調查](https://blogs.technet.microsoft.com/msoms/2016/12/08/investigating-suspicious-activity-in-a-hybrid-cloud-with-oms-security/)安全性警示。</span><span class="sxs-lookup"><span data-stu-id="5aa12-195">Due tooits nature, it should be combined with other sources of security information while [investigating](https://blogs.technet.microsoft.com/msoms/2016/12/08/investigating-suspicious-activity-in-a-hybrid-cloud-with-oms-security/) a security alert.</span></span> 

### <a name="baseline-assessment"></a><span data-ttu-id="5aa12-196">基準評估</span><span class="sxs-lookup"><span data-stu-id="5aa12-196">Baseline Assessment</span></span>

<span data-ttu-id="5aa12-197">Microsoft 與全球產業和政府組織共同定義可代表高度安全伺服器部署的 Windows 組態。</span><span class="sxs-lookup"><span data-stu-id="5aa12-197">Microsoft, together with industry and government organizations worldwide, defines a Windows configuration that represents highly secure server deployments.</span></span> <span data-ttu-id="5aa12-198">此組態是一組登錄機碼、稽核原則設定和安全性原則設定，以及 Microsoft 對於這些設定的建議值。</span><span class="sxs-lookup"><span data-stu-id="5aa12-198">This configuration is a set of registry keys, audit policy settings, and security policy settings along with Microsoft’s recommended values for these settings.</span></span> <span data-ttu-id="5aa12-199">這組規則也稱為安全性基準。</span><span class="sxs-lookup"><span data-stu-id="5aa12-199">This set of rules is known as Security baseline.</span></span> <span data-ttu-id="5aa12-200">如需此選項的詳細資訊，請參閱 [Operations Management Suite 安全性和稽核解決方案中的基準評估](oms-security-baseline.md)。</span><span class="sxs-lookup"><span data-stu-id="5aa12-200">Read [Baseline Assessment in Operations Management Suite Security and Audit Solution](oms-security-baseline.md) for more information about this option.</span></span>

### <a name="azure-security-center"></a><span data-ttu-id="5aa12-201">Azure 資訊安全中心</span><span class="sxs-lookup"><span data-stu-id="5aa12-201">Azure Security Center</span></span>
<span data-ttu-id="5aa12-202">此磚基本上是快顯 tooaccess Azure 資訊安全中心儀表板。</span><span class="sxs-lookup"><span data-stu-id="5aa12-202">This tile is basically a shortcut tooaccess Azure Security Center dashboard.</span></span> <span data-ttu-id="5aa12-203">如需此解決方案的詳細資訊，請閱讀 [開始使用 Azure 資訊安全中心](../security-center/security-center-get-started.md) 。</span><span class="sxs-lookup"><span data-stu-id="5aa12-203">Read [Getting started with Azure Security Center](../security-center/security-center-get-started.md) for more information about this solution.</span></span>

## <a name="notable-issues"></a><span data-ttu-id="5aa12-204">值得注意的問題</span><span class="sxs-lookup"><span data-stu-id="5aa12-204">Notable issues</span></span>
<span data-ttu-id="5aa12-205">此群組的選項 hello 主要目的是 tooprovide 您尚未在環境中，分類，以進行重大、 警告及資訊中的 hello 問題的快速檢視。</span><span class="sxs-lookup"><span data-stu-id="5aa12-205">hello main intent of this group of options is tooprovide a quick view of hello issues that you have in your environment, by categorizing them in Critical, Warning and Informational.</span></span> <span data-ttu-id="5aa12-206">hello 作用中的問題類型的磚是視覺效果的這些問題，但它並不允許的 tooexplore 更多詳細資料，您必須具有 hello 名稱多少物件有此項動作 （計數） 的 hello 問題 （名稱），此磚的 toouse hello 下半部，重要性是 （嚴重性）。</span><span class="sxs-lookup"><span data-stu-id="5aa12-206">hello Active issue type tile it’s a visualization of these issues, but it doesn’t allow you tooexplore more details about them, for that you need toouse hello lower part of this tile that has hello name of hello issue (NAME), how many objects had this happen (COUNT) and how critical it is (SEVERITY).</span></span>

![值得注意的問題](./media/oms-security-getting-started/oms-getting-started-fig10.JPG)

<span data-ttu-id="5aa12-208">您可以看到這些問題已已經涵蓋 hello 的不同領域中**安全性網域**群組，這可加強 hello 意圖，此檢視： 以視覺化方式檢視您的環境，從單一位置中的 hello 最重要問題。</span><span class="sxs-lookup"><span data-stu-id="5aa12-208">You can see that these issues were already covered in different areas of hello **Security Domains** group, which reinforces hello intent of this view: visualize hello most important issues in your environment from a single place.</span></span>

## <a name="detections-preview"></a><span data-ttu-id="5aa12-209">偵測 (預覽)</span><span class="sxs-lookup"><span data-stu-id="5aa12-209">Detections (Preview)</span></span>
<span data-ttu-id="5aa12-210">hello 這個選項的主要目的是 tooallow IT tooquickly 識別潛在威脅 tootheir 環境中的透過和 hello 的這項威脅的嚴重性。</span><span class="sxs-lookup"><span data-stu-id="5aa12-210">hello main intent of this option is tooallow IT tooquickly identify potential threats tootheir environment via and hello severity of this threat.</span></span>

![威脅情報](./media/oms-security-getting-started/oms-getting-started-fig12.png)

<span data-ttu-id="5aa12-212">此選項也可用在[事件回應調查](https://blogs.msdn.microsoft.com/azuresecurity/2016/11/30/investigating-suspicious-activity-in-a-hybrid-cloud-with-oms-security/)tooperform hello 評估，並取得更多有關 hello 攻擊。</span><span class="sxs-lookup"><span data-stu-id="5aa12-212">This option can also be used during an [incident response investigation](https://blogs.msdn.microsoft.com/azuresecurity/2016/11/30/investigating-suspicious-activity-in-a-hybrid-cloud-with-oms-security/) tooperform hello assessment and obtain more information about hello attack.</span></span>

> [!NOTE]
> <span data-ttu-id="5aa12-213">如需有關如何 toouse 事件回應 OMS 觀看這段影片： [tooLeverage 如何 hello Azure 資訊安全中心 & Microsoft Operations Management Suite 事件回應](https://channel9.msdn.com/Blogs/Taste-of-Premier/ToP1703)。</span><span class="sxs-lookup"><span data-stu-id="5aa12-213">For more information on how toouse OMS for Incident Response, watch this video: [How tooLeverage hello Azure Security Center & Microsoft Operations Management Suite for an Incident Response](https://channel9.msdn.com/Blogs/Taste-of-Premier/ToP1703).</span></span>
> 
> 

## <a name="threat-intelligence"></a><span data-ttu-id="5aa12-214">威脅情報</span><span class="sxs-lookup"><span data-stu-id="5aa12-214">Threat Intelligence</span></span>
<span data-ttu-id="5aa12-215">hello 新威脅智慧一節的 hello 安全性和稽核 」 解決方案會視覺化 hello 可能的攻擊模式幾種： hello 的具有惡意連出 IP 流量的伺服器總數、 hello 惡意之威脅類型及顯示在哪裡對應這些 Ip來自。</span><span class="sxs-lookup"><span data-stu-id="5aa12-215">hello new threat intelligence section of hello Security and Audit solution visualizes hello possible attack patterns in several ways: hello total number of servers with outbound malicious IP traffic, hello malicious threat type and a map that shows where these IPs are coming from.</span></span> <span data-ttu-id="5aa12-216">您可以互動 hello 對應，然後按一下 hello Ip 如需詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="5aa12-216">You can interact with hello map and click on hello IPs for more information.</span></span>

<span data-ttu-id="5aa12-217">黃色圖釘 hello 地圖上的指出惡意 Ip 的連入流量。</span><span class="sxs-lookup"><span data-stu-id="5aa12-217">Yellow pushpins on hello map indicate incoming traffic from malicious IPs.</span></span> <span data-ttu-id="5aa12-218">是很常見的伺服器公開 toohello 網際網路 toosee 連入惡意流量，但我們建議您檢閱這些嘗試 toomake 確定沒有任何已順利完成。</span><span class="sxs-lookup"><span data-stu-id="5aa12-218">It is not uncommon for servers that are exposed toohello internet toosee incoming malicious traffic, but we recommend reviewing these attempts toomake sure none of them was successful.</span></span> <span data-ttu-id="5aa12-219">這些指標是以 IIS 記錄、WireData 和 Windows 防火牆記錄為基礎。</span><span class="sxs-lookup"><span data-stu-id="5aa12-219">These indicators are based on IIS logs, WireData and Windows Firewall logs.</span></span>  

![威脅情報](./media/oms-security-getting-started/oms-getting-started-fig11-ga.png)

## <a name="common-security-queries"></a><span data-ttu-id="5aa12-221">常見安全性查詢</span><span class="sxs-lookup"><span data-stu-id="5aa12-221">Common security queries</span></span>
<span data-ttu-id="5aa12-222">可用的常見安全性查詢 hello 清單可以用於您 toorapidly 存取資源的資訊，並根據您的環境需求加以自訂。</span><span class="sxs-lookup"><span data-stu-id="5aa12-222">hello list of common security queries available can be useful for you toorapidly access resource’s information and customize it based on your environment’s needs.</span></span> <span data-ttu-id="5aa12-223">這些常用查詢如下︰</span><span class="sxs-lookup"><span data-stu-id="5aa12-223">These common queries are:</span></span>

* <span data-ttu-id="5aa12-224">所有安全性活動</span><span class="sxs-lookup"><span data-stu-id="5aa12-224">All Security Activities</span></span>
* <span data-ttu-id="5aa12-225">Hello 電腦"computer01.contoso.com"（取代為您自己的電腦名稱） 的安全性活動</span><span class="sxs-lookup"><span data-stu-id="5aa12-225">Security Activities on hello computer "computer01.contoso.com" (replace with your own computer name)</span></span>
* <span data-ttu-id="5aa12-226">Hello 電腦"computer01.contoso.com"帳戶"Administrator"（以您自己的電腦和帳戶名稱取代） 的安全性活動</span><span class="sxs-lookup"><span data-stu-id="5aa12-226">Security Activities on hello computer "computer01.contoso.com" for account "Administrator" (replace with your own computer and account names)</span></span>
* <span data-ttu-id="5aa12-227">依電腦的登入活動</span><span class="sxs-lookup"><span data-stu-id="5aa12-227">Log on Activity by Computer</span></span>
* <span data-ttu-id="5aa12-228">在任何電腦上終止 Microsoft 反惡意程式碼的帳戶</span><span class="sxs-lookup"><span data-stu-id="5aa12-228">Accounts who terminated Microsoft antimalware on any computer</span></span>
* <span data-ttu-id="5aa12-229">Hello Microsoft 反惡意程式碼處理序已終止的電腦</span><span class="sxs-lookup"><span data-stu-id="5aa12-229">Computers where hello Microsoft antimalware process was terminated</span></span>
* <span data-ttu-id="5aa12-230">已執行 "hash.exe" 的電腦 (以不同的處理序名稱取代)</span><span class="sxs-lookup"><span data-stu-id="5aa12-230">Computers where "hash.exe" was executed (replace with different process name)</span></span>
* <span data-ttu-id="5aa12-231">已執行的所有處理序名稱</span><span class="sxs-lookup"><span data-stu-id="5aa12-231">All Process names that were executed</span></span>
* <span data-ttu-id="5aa12-232">依帳戶的登入活動</span><span class="sxs-lookup"><span data-stu-id="5aa12-232">Log on Activity by Account</span></span>
* <span data-ttu-id="5aa12-233">從遠端登入帳戶 hello 電腦"computer01.contoso.com"（以您自己的電腦名稱取代）</span><span class="sxs-lookup"><span data-stu-id="5aa12-233">Accounts who remotely logged on hello computer "computer01.contoso.com" (replace with your own computer name)</span></span>

## <a name="see-also"></a><span data-ttu-id="5aa12-234">另請參閱</span><span class="sxs-lookup"><span data-stu-id="5aa12-234">See also</span></span>
<span data-ttu-id="5aa12-235">在本文件中，您所導入了的 tooOMS 安全性和稽核 」 解決方案。</span><span class="sxs-lookup"><span data-stu-id="5aa12-235">In this document, you were introduced tooOMS Security and Audit solution.</span></span> <span data-ttu-id="5aa12-236">toolearn 進一步了解 OMS 安全性，請參閱下列文章 hello:</span><span class="sxs-lookup"><span data-stu-id="5aa12-236">toolearn more about OMS Security, see hello following articles:</span></span>

* [<span data-ttu-id="5aa12-237">Operations Management Suite (OMS) 概觀</span><span class="sxs-lookup"><span data-stu-id="5aa12-237">Operations Management Suite (OMS) overview</span></span>](operations-management-suite-overview.md)
* [<span data-ttu-id="5aa12-238">監視及回應 tooSecurity 警示在 Operations Management Suite 安全性和稽核解決方案</span><span class="sxs-lookup"><span data-stu-id="5aa12-238">Monitoring and Responding tooSecurity Alerts in Operations Management Suite Security and Audit Solution</span></span>](oms-security-responding-alerts.md)
* [<span data-ttu-id="5aa12-239">在 Operations Management Suite 安全性和稽核解決方案內監視資源</span><span class="sxs-lookup"><span data-stu-id="5aa12-239">Monitoring Resources in Operations Management Suite Security and Audit Solution</span></span>](oms-security-monitoring-resources.md)

