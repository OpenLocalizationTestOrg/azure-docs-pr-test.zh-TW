---
title: "在 Operations Management Suite 安全性和稽核解決方案基準基準評估 aaaWeb |Microsoft 文件"
description: "本文件說明如何 toouse web 基準評估 OMS 安全性和稽核解決方案 tooperform 基準評估相容性和安全性用途的所有受監視的 web 伺服器中。"
services: operations-management-suite
documentationcenter: na
author: YuriDio
manager: mbaldwin
editor: 
ms.assetid: 17837c8b-3e79-47c0-9b83-a51c6ca44ca6
ms.service: operations-management-suite
ms.custom: oms-security
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/18/2017
ms.author: yurid
ms.openlocfilehash: dafa9d3d93fae31748306b60ee40b285dd59c802
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="web-baseline-assessment-in-operations-management-suite-security-and-audit-solution"></a><span data-ttu-id="a2408-103">Operations Management Suite 安全性和稽核解決方案中的 Web 基準評估</span><span class="sxs-lookup"><span data-stu-id="a2408-103">Web Baseline Assessment in Operations Management Suite Security and Audit Solution</span></span>
<span data-ttu-id="a2408-104">這份文件可協助您使用 OMS 安全性和稽核 web 基準評估功能 tooaccess hello 受監視資源的安全的狀態。</span><span class="sxs-lookup"><span data-stu-id="a2408-104">This document helps you use OMS Security and Audit web baseline assessment capabilities tooaccess hello secure state of your monitored resources.</span></span>

## <a name="what-is-web-baseline-assessment"></a><span data-ttu-id="a2408-105">什麼是 Web 基準評估？</span><span class="sxs-lookup"><span data-stu-id="a2408-105">What is web baseline assessment?</span></span>
<span data-ttu-id="a2408-106">OMS 安全性目前會提供作業系統的安全性基準評估。</span><span class="sxs-lookup"><span data-stu-id="a2408-106">Currently OMS Security provides security baseline assessment for operating systems.</span></span> <span data-ttu-id="a2408-107">它會每 24 小時，會掃描您的伺服器 hello OS 設定，並提供讓您檢視可能有弱點的設定。</span><span class="sxs-lookup"><span data-stu-id="a2408-107">It scans hello OS settings of your servers every 24 hours, and provides a view into potentially vulnerable settings.</span></span> <span data-ttu-id="a2408-108">如需詳細資訊，請參閱 [Operations Management Suite 安全性和稽核解決方案中的基準評估](https://docs.microsoft.com/azure/operations-management-suite/oms-security-baseline)。</span><span class="sxs-lookup"><span data-stu-id="a2408-108">Read [Baseline Assessment in Operations Management Suite Security and Audit Solution](https://docs.microsoft.com/azure/operations-management-suite/oms-security-baseline) for more information on this.</span></span>

<span data-ttu-id="a2408-109">hello Web 基準評估 hello 目標是 toofind 可能有弱點的網頁伺服器設定。</span><span class="sxs-lookup"><span data-stu-id="a2408-109">hello goal of hello Web Baseline assessment is toofind potentially vulnerable web server settings.</span></span> <span data-ttu-id="a2408-110">hello web 基準設定為 hello 三個主要來源：.NET、 ASP.NET 和 IIS 組態。</span><span class="sxs-lookup"><span data-stu-id="a2408-110">hello three primary sources for hello web baseline configurations are: .NET, ASP.NET, and IIS configuration.</span></span>  <span data-ttu-id="a2408-111">就像 hello 作業系統基準評估，OMS 安全性即將 tooscan 您網頁伺服器每隔 24 小時制，並提供讓您檢視它們的安全性狀態。</span><span class="sxs-lookup"><span data-stu-id="a2408-111">Just like hello operating system baseline assessment, OMS Security is going tooscan your web servers every 24hrs and provide a view into security state of them.</span></span>  <span data-ttu-id="a2408-112">在 網際網路資訊服務 (IIS) 中，設定是高度可自訂，可讓覆寫的不同網站和應用程式層級 toobe。</span><span class="sxs-lookup"><span data-stu-id="a2408-112">In Internet Information Service (IIS), configurations are highly customizable, which allows various site and application levels toobe overridden.</span></span> <span data-ttu-id="a2408-113">hello 掃描器檢查 hello 加法 toohello 預設根層級中每個應用程式/網站層級的設定。</span><span class="sxs-lookup"><span data-stu-id="a2408-113">hello scanner checks hello settings at each application/site level in addition toohello default root level.</span></span> <span data-ttu-id="a2408-114">這有助於您 tooidentify 可能有弱點的設定，並快速修正，以及我們的建議的設定。</span><span class="sxs-lookup"><span data-stu-id="a2408-114">This helps you tooidentify potentially vulnerable settings and quickly remediate, along with our recommendations for those settings.</span></span>

>[!NOTE] 
><span data-ttu-id="a2408-115">您可以下載 hello 常見的組態識別碼與在此使用 OMS 安全性的基準規則[頁面](https://gallery.technet.microsoft.com/Azure-Security-Center-a789e335?redir=0)。</span><span class="sxs-lookup"><span data-stu-id="a2408-115">You can download hello Common Configuration Identifiers and Baseline Rules used by OMS Security in this [page](https://gallery.technet.microsoft.com/Azure-Security-Center-a789e335?redir=0).</span></span>


## <a name="web-security-baseline-assessment"></a><span data-ttu-id="a2408-116">Web 安全性基準評估</span><span class="sxs-lookup"><span data-stu-id="a2408-116">Web security baseline assessment</span></span>

<span data-ttu-id="a2408-117">此預覽 hello 功能可以透過 hello OMS 搜尋選項和 hello OMS 安全性和稽核儀表板。</span><span class="sxs-lookup"><span data-stu-id="a2408-117">For this preview hello feature can be accessed via hello OMS Search option, and hello OMS Security and Audit Dashboard.</span></span> <span data-ttu-id="a2408-118">請遵循以下 tooperform hello appropriated 查詢 hello 步驟：</span><span class="sxs-lookup"><span data-stu-id="a2408-118">Follow hello steps below tooperform hello appropriated query:</span></span>

1. <span data-ttu-id="a2408-119">在 hello **Microsoft Operations Management Suite**主要儀表板中，按一下**安全性和稽核**磚。</span><span class="sxs-lookup"><span data-stu-id="a2408-119">In hello **Microsoft Operations Management Suite** main dashboard, click **Security and Audit** tile.</span></span>
2. <span data-ttu-id="a2408-120">在 hello**安全性和稽核**儀表板，您可以看到 hello Web 基準檢視方塊 下一步 toohello OS 基準檢視方塊。</span><span class="sxs-lookup"><span data-stu-id="a2408-120">In hello **Security and Audit** dashboard, you can see hello Web Baseline perspective next toohello OS baseline perspective.</span></span>
   
    ![OMS 安全性和稽核 Web 安全幸基準評估](./media/oms-security-web-baseline/oms-security-web-baseline-fig5.png)

3. <span data-ttu-id="a2408-122">hello 左的窗格會顯示 hello 數目進行比較的網頁伺服器 toohello 基準，hello 平均百分比傳遞所有的 hello 評估伺服器的規則及 hello 所評估的伺服器清單。</span><span class="sxs-lookup"><span data-stu-id="a2408-122">hello left pane shows hello number of Web Servers compared toohello baseline, hello average percentage of rules that passed on all hello evaluated servers, and hello list of Servers that were assessed.</span></span>
4. <span data-ttu-id="a2408-123">右窗格會列出 hello 唯一 hello 規則失敗*嚴重性*，和*RuleType*。</span><span class="sxs-lookup"><span data-stu-id="a2408-123">hello right pane lists hello unique rules that failed by *Severity*, and *RuleType*.</span></span> <span data-ttu-id="a2408-124">按一下任一 hello 右窗格的規則將會顯示 hello 詳細資料，該規則。</span><span class="sxs-lookup"><span data-stu-id="a2408-124">Clicking on any of hello right pane rules will show hello details of that rule.</span></span> <span data-ttu-id="a2408-125">範例所示 hello 影像下方。</span><span class="sxs-lookup"><span data-stu-id="a2408-125">An example is shown in hello below image.</span></span> <span data-ttu-id="a2408-126">評估 hello 規則都會列在下*規則設定*。</span><span class="sxs-lookup"><span data-stu-id="a2408-126">hello rule that is evaluated is listed under *Rule Setting*.</span></span> <span data-ttu-id="a2408-127">hello *AzId*欄位，也就是 Microsoft 用於追蹤 hello 基準規則每個規則的唯一識別碼。</span><span class="sxs-lookup"><span data-stu-id="a2408-127">hello *AzId* field which is a unique identifier for each rule used by Microsoft for tracking hello baseline rules.</span></span> <span data-ttu-id="a2408-128">此外 toothat 使用者可以看到 hello*預期的結果*（Microsoft 的建議值），和其他詳細資料有關的 hello 規則 hello 安全性影響。</span><span class="sxs-lookup"><span data-stu-id="a2408-128">In addition toothat users can see hello *Expected Result* (Microsoft’s recommended value), and other details regarding hello security impact of hello rule.</span></span>
    
    ![查詢](./media/oms-security-web-baseline/oms-security-web-baseline-fig6.png)

5. <span data-ttu-id="a2408-130">您可以建立您自己的查詢 tooreview hello 結果。</span><span class="sxs-lookup"><span data-stu-id="a2408-130">You can create your own queries tooreview hello results.</span></span> 

<span data-ttu-id="a2408-131">hello 第一個查詢，您可以使用為 hello **Web 基準評估摘要**。</span><span class="sxs-lookup"><span data-stu-id="a2408-131">hello first query that you can use is hello **Web Baseline Assessment Summary**.</span></span> <span data-ttu-id="a2408-132">在 hello**這裡開始搜尋**欄位中，輸入此查詢：*類型 = SecurityBaselineSummary BaselineType = Web*。</span><span class="sxs-lookup"><span data-stu-id="a2408-132">In hello **Begin search here** field, type this query: *Type=SecurityBaselineSummary BaselineType=Web*.</span></span> <span data-ttu-id="a2408-133">hello 下面是輸出範例：</span><span class="sxs-lookup"><span data-stu-id="a2408-133">hello following is an output sample:</span></span>

![查詢結果](./media/oms-security-web-baseline/oms-security-web-baseline-fig7.png)

>[!NOTE] 
><span data-ttu-id="a2408-135">在此查詢中，每筆記錄都會指出在單一伺服器上的評估摘要。</span><span class="sxs-lookup"><span data-stu-id="a2408-135">In this query, each record indicates assessment summary on a single server.</span></span>

<span data-ttu-id="a2408-136">當您在 hello**記錄搜尋**，您可以輸入不同的查詢 tooobtain hello web 基準評估的詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="a2408-136">Once you are in hello **Log Search**, you can type different queries tooobtain more information about hello web baseline assessment.</span></span> <span data-ttu-id="a2408-137">此外 toohello 上述查詢中，您也可以使用下列是在此預覽中的 hello:</span><span class="sxs-lookup"><span data-stu-id="a2408-137">In addition toohello previous query, you can also use hello following ones in this preview:</span></span>

<span data-ttu-id="a2408-138">**Web 基準規則評估**︰每筆記錄均代表單一伺服器上的單一 Web 基準規則評估。</span><span class="sxs-lookup"><span data-stu-id="a2408-138">**Web Baseline Rule Assessment**: Each record represents a single web baseline rule evaluation on a single server.</span></span> <span data-ttu-id="a2408-139">它包含所有資料針對失敗的規則，hello *SitePath*上哪些 hello 規則評估，hello*預期的結果*，和 hello*實際結果*。</span><span class="sxs-lookup"><span data-stu-id="a2408-139">It includes all data for a failed rule, hello *SitePath* on which hello rule was evaluated, hello *Expected Result*, and hello *Actual Result*.</span></span>

<span data-ttu-id="a2408-140">查詢：*Type=SecurityBaseline BaselineType=Web AnalyzeResult=Failed*</span><span class="sxs-lookup"><span data-stu-id="a2408-140">Query: *Type=SecurityBaseline BaselineType=Web AnalyzeResult=Failed*</span></span>

![查詢結果 2](./media/oms-security-web-baseline/oms-security-web-baseline-fig8.png)

<span data-ttu-id="a2408-142">**顯示特定伺服器的所有結果**： 此查詢會顯示如何 toosee 結果的特定伺服器： 查詢：*類型 = SecurityBaseline BaselineType = Web 電腦 = BaselineTestVM1*</span><span class="sxs-lookup"><span data-stu-id="a2408-142">**Show all results for a specific server**: This query shows how toosee results of a specific server: Query: *Type=SecurityBaseline BaselineType=Web Computer=BaselineTestVM1*</span></span>

![查詢結果 3](./media/oms-security-web-baseline/oms-security-web-baseline-fig3.png)

<span data-ttu-id="a2408-144">您可以使用這些記錄/查詢 toocreate 您自己的儀表板、 報表或警示。</span><span class="sxs-lookup"><span data-stu-id="a2408-144">You can use these records/queries toocreate your own dashboards, reports, or alerts.</span></span> <span data-ttu-id="a2408-145">以下是範例 UI 控制項，您可以加入 tooyour 儀表板。</span><span class="sxs-lookup"><span data-stu-id="a2408-145">Here is a sample UI control that you can add tooyour dashboard.</span></span> <span data-ttu-id="a2408-146">您可以了解如何 toovisualize 資料，可使用 OMS 檢視表設計工具[這裡](https://blogs.technet.microsoft.com/msoms/2016/06/30/oms-view-designer-visualize-your-data-your-way/)。</span><span class="sxs-lookup"><span data-stu-id="a2408-146">You can learn how toovisualize your data using OMS View Designer [here](https://blogs.technet.microsoft.com/msoms/2016/06/30/oms-view-designer-visualize-your-data-your-way/).</span></span> <span data-ttu-id="a2408-147">囉 」 畫面下方是 hello 的並排顯示的範例看起來像一旦完成這項自訂。</span><span class="sxs-lookup"><span data-stu-id="a2408-147">hello screen below is an example of how hello tile will look like once you make this customization.</span></span>

![儀表板](./media/oms-security-web-baseline/oms-security-web-baseline-fig4.png)

## <a name="see-also"></a><span data-ttu-id="a2408-149">另請參閱</span><span class="sxs-lookup"><span data-stu-id="a2408-149">See also</span></span>
<span data-ttu-id="a2408-150">在本文件中，您已了解 OMS 安全性和稽核 Web 基準評估。</span><span class="sxs-lookup"><span data-stu-id="a2408-150">In this document, you learned about OMS Security and Audit Web Baseline assessment.</span></span> <span data-ttu-id="a2408-151">toolearn 進一步了解 OMS 安全性，請參閱下列文章 hello:</span><span class="sxs-lookup"><span data-stu-id="a2408-151">toolearn more about OMS Security, see hello following articles:</span></span>

* [<span data-ttu-id="a2408-152">Operations Management Suite (OMS) 概觀</span><span class="sxs-lookup"><span data-stu-id="a2408-152">Operations Management Suite (OMS) overview</span></span>](operations-management-suite-overview.md)
* [<span data-ttu-id="a2408-153">監視及回應 tooSecurity 警示在 Operations Management Suite 安全性和稽核解決方案</span><span class="sxs-lookup"><span data-stu-id="a2408-153">Monitoring and Responding tooSecurity Alerts in Operations Management Suite Security and Audit Solution</span></span>](oms-security-responding-alerts.md)
* [<span data-ttu-id="a2408-154">在 Operations Management Suite 安全性和稽核解決方案內監視資源</span><span class="sxs-lookup"><span data-stu-id="a2408-154">Monitoring Resources in Operations Management Suite Security and Audit Solution</span></span>](oms-security-monitoring-resources.md)

