---
title: "管理套件的安全性和稽核解決方案 Web 基準 aaaOperations |Microsoft 文件"
description: "本文件說明如何 toouse OMS 安全性和稽核解決方案 tooperform web 基準評估相容性和安全性用途的所有受監視的 web 伺服器。"
services: operations-management-suite
documentationcenter: na
author: YuriDio
manager: mbaldwin
editor: 
ROBOTS: NOINDEX
redirect_url: https://www.microsoft.com/cloud-platform/security-and-compliance
ms.assetid: 17837c8b-3e79-47c0-9b83-a51c6ca44ca6
ms.service: operations-management-suite
ms.custom: oms-security
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 04/27/2017
ms.author: yurid
ms.openlocfilehash: 8aa87fa404ff97ab549dda3f9bebb75766055963
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="web-baseline-assessment-in-operations-management-suite-security-and-audit-solution"></a><span data-ttu-id="e1f10-103">Operations Management Suite 安全性和稽核解決方案中的 Web 基準評估</span><span class="sxs-lookup"><span data-stu-id="e1f10-103">Web Baseline Assessment in Operations Management Suite Security and Audit Solution</span></span>
<span data-ttu-id="e1f10-104">這份文件可協助您 toouse [Operations Management Suite (OMS) 的安全性和稽核解決方案](operations-management-suite-overview.md)web 基準評估功能 tooaccess hello 受監視資源的安全的狀態。</span><span class="sxs-lookup"><span data-stu-id="e1f10-104">This document helps you toouse [Operations Management Suite (OMS) Security and Audit Solution](operations-management-suite-overview.md) web baseline assessment capabilities tooaccess hello secure state of your monitored resources.</span></span>

## <a name="what-is-web-baseline-assessment"></a><span data-ttu-id="e1f10-105">什麼是 Web 基準評估？</span><span class="sxs-lookup"><span data-stu-id="e1f10-105">What is Web Baseline Assessment?</span></span>
<span data-ttu-id="e1f10-106">OMS 安全性目前會提供作業系統的安全性基準評估。</span><span class="sxs-lookup"><span data-stu-id="e1f10-106">Currently OMS Security provides security baseline assessment for operating systems.</span></span> <span data-ttu-id="e1f10-107">它會掃描每隔 24 小時的 hello 作業系統設定的伺服器，然後可讓您檢視可能有弱點的設定。</span><span class="sxs-lookup"><span data-stu-id="e1f10-107">It scans hello operating system settings of your servers every 24 hours and provides a view into potentially vulnerable settings.</span></span> <span data-ttu-id="e1f10-108">如需詳細資訊，請參閱 [Operations Management Suite 安全性和稽核解決方案中的基準評估](oms-security-baseline.md)。</span><span class="sxs-lookup"><span data-stu-id="e1f10-108">Read [Baseline Assessment in Operations Management Suite Security and Audit Solution](oms-security-baseline.md) for more information on this.</span></span>

<span data-ttu-id="e1f10-109">hello web 基準評估 hello 目標是 toofind 可能有弱點的網頁伺服器設定。</span><span class="sxs-lookup"><span data-stu-id="e1f10-109">hello goal of hello web baseline assessment is toofind potentially vulnerable web server settings.</span></span> <span data-ttu-id="e1f10-110">hello web 基準設定為 hello 三個主要來源：.NET、 ASP.NET 和 IIS 組態。</span><span class="sxs-lookup"><span data-stu-id="e1f10-110">hello three primary sources for hello web baseline configurations are: .NET, ASP.NET, and IIS configuration.</span></span>  <span data-ttu-id="e1f10-111">就像 hello 作業系統基準評估，OMS 安全性即將 tooscan 您網頁伺服器每隔 24 小時制，並提供讓您檢視它們的安全性狀態。</span><span class="sxs-lookup"><span data-stu-id="e1f10-111">Just like hello operating system baseline assessment, OMS Security is going tooscan your web servers every 24hrs and provide a view into security state of them.</span></span>  <span data-ttu-id="e1f10-112">在 網際網路資訊服務 (IIS) 中，設定是高度可自訂，可讓覆寫的不同網站和應用程式層級 toobe。</span><span class="sxs-lookup"><span data-stu-id="e1f10-112">In Internet Information Service (IIS), configurations are highly customizable, which allows various site and application levels toobe overridden.</span></span> <span data-ttu-id="e1f10-113">hello 掃描器檢查 hello 加法 toohello 預設根層級中每個應用程式/網站層級的設定。</span><span class="sxs-lookup"><span data-stu-id="e1f10-113">hello scanner checks hello settings at each application/site level in addition toohello default root level.</span></span> <span data-ttu-id="e1f10-114">這有助於您 tooidentify 潛在的弱點可能會設定位置，並快速修正。</span><span class="sxs-lookup"><span data-stu-id="e1f10-114">This helps you tooidentify potential vulnerability settings locations and quickly remediate.</span></span>


## <a name="web-security-baseline-assessment"></a><span data-ttu-id="e1f10-115">Web 安全性基準評估</span><span class="sxs-lookup"><span data-stu-id="e1f10-115">Web Security Baseline Assessment</span></span>
<span data-ttu-id="e1f10-116">此預覽這項功能即將 toobe 使用 hello OMS 搜尋選項來存取。</span><span class="sxs-lookup"><span data-stu-id="e1f10-116">For this preview this feature is going toobe accessed using hello OMS Search option.</span></span> <span data-ttu-id="e1f10-117">請遵循以下 tooperform hello appropriated 查詢 hello 步驟：</span><span class="sxs-lookup"><span data-stu-id="e1f10-117">Follow hello steps below tooperform hello appropriated query:</span></span>

1. <span data-ttu-id="e1f10-118">在 hello **Microsoft Operations Management Suite**主要儀表板按一下**安全性和稽核**磚。</span><span class="sxs-lookup"><span data-stu-id="e1f10-118">In hello **Microsoft Operations Management Suite** main dashboard click **Security and Audit** tile.</span></span>
2. <span data-ttu-id="e1f10-119">在 hello**安全性和稽核**儀表板，按一下 **記錄搜尋** 按鈕。</span><span class="sxs-lookup"><span data-stu-id="e1f10-119">In hello **Security and Audit** dashboard, click **Log Search** button.</span></span>
3. <span data-ttu-id="e1f10-120">hello 第一個查詢，您可以使用為 hello **Web 基準評估摘要**。</span><span class="sxs-lookup"><span data-stu-id="e1f10-120">hello first query that you can use is hello **Web Baseline Assessment Summary**.</span></span> <span data-ttu-id="e1f10-121">在 hello**這裡開始搜尋**欄位中，輸入此查詢： 型別*= SecurityBaselineSummary BaselineType = web*。</span><span class="sxs-lookup"><span data-stu-id="e1f10-121">In hello **Begin search here** field, type this query: Type*=SecurityBaselineSummary BaselineType=web*.</span></span> <span data-ttu-id="e1f10-122">下列畫面 hello 具有輸出範例：</span><span class="sxs-lookup"><span data-stu-id="e1f10-122">hello following screen has an output sample:</span></span>

![Web 基準評估摘要](./media/oms-security-web-baseline/oms-security-web-baseline-fig1-new.png)

> [!NOTE]
> <span data-ttu-id="e1f10-124">在此查詢中，每筆記錄都會指出在單一伺服器上的評估摘要。</span><span class="sxs-lookup"><span data-stu-id="e1f10-124">In this query, each record indicates assessment summary on a single server.</span></span>

<span data-ttu-id="e1f10-125">當您在 hello**記錄搜尋**，您可以輸入不同的查詢 tooobtain hello web 基準評估的詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="e1f10-125">Once you are in hello **Log Search**, you can type different queries tooobtain more information about hello web baseline assessment.</span></span> <span data-ttu-id="e1f10-126">此外 toohello 上述查詢中，您也可以使用下列是在此預覽中的 hello。</span><span class="sxs-lookup"><span data-stu-id="e1f10-126">In addition toohello previous query, you can also use hello following ones in this preview.</span></span>

<span data-ttu-id="e1f10-127">**Web 基準規則評估**︰每筆記錄均代表單一伺服器上的單一 Web 基準規則評估。</span><span class="sxs-lookup"><span data-stu-id="e1f10-127">**Web Baseline Rule Assessment**: Each record represents a single web baseline rule evaluation on a single server.</span></span> <span data-ttu-id="e1f10-128">它包含 hello 規則、 位置、 hello 預期的結果，以及 hello 實際結果的所有資料。</span><span class="sxs-lookup"><span data-stu-id="e1f10-128">It includes all data for hello rule, location, hello expected result, and hello actual result.</span></span>

<span data-ttu-id="e1f10-129">**查詢**：Type=SecurityBaseline BaselineType=web</span><span class="sxs-lookup"><span data-stu-id="e1f10-129">**Query**: Type*=SecurityBaseline BaselineType=web*</span></span>

![Web 基準規則評估](./media/oms-security-web-baseline/oms-security-web-baseline-fig2.png)

<span data-ttu-id="e1f10-131">**顯示特定伺服器的所有結果**： 此查詢會顯示如何 toosee 結果的特定伺服器。</span><span class="sxs-lookup"><span data-stu-id="e1f10-131">**Show all results for a specific server**: This query shows how toosee results of a specific server.</span></span>

<span data-ttu-id="e1f10-132">**查詢**：Type=SecurityBaseline BaselineType=web Computer=BaselineTestVM1</span><span class="sxs-lookup"><span data-stu-id="e1f10-132">**Query**: *Type=SecurityBaseline BaselineType=web Computer=BaselineTestVM1*</span></span>

![所有結果](./media/oms-security-web-baseline/oms-security-web-baseline-fig3.png)

<span data-ttu-id="e1f10-134">您也可以使用這些記錄/查詢 toocreate 您自己的儀表板、 報表或警示。</span><span class="sxs-lookup"><span data-stu-id="e1f10-134">You can also use these records/queries toocreate your own dashboards, reports, or alerts.</span></span> <span data-ttu-id="e1f10-135">囉 」 畫面下方有範例 UI 控制項，您可以加入 tooyour 儀表板。</span><span class="sxs-lookup"><span data-stu-id="e1f10-135">hello screen below has a sample UI control that you can add tooyour dashboard.</span></span> <span data-ttu-id="e1f10-136">您可以了解如何 toovisualize 資料，可使用 OMS 檢視表設計工具[這裡](https://blogs.technet.microsoft.com/msoms/2016/06/30/oms-view-designer-visualize-your-data-your-way/)。</span><span class="sxs-lookup"><span data-stu-id="e1f10-136">You can learn how toovisualize your data using OMS View Designer [here](https://blogs.technet.microsoft.com/msoms/2016/06/30/oms-view-designer-visualize-your-data-your-way/).</span></span> <span data-ttu-id="e1f10-137">囉 」 畫面下方是 hello 的並排顯示的範例看起來像一旦完成這項自訂。</span><span class="sxs-lookup"><span data-stu-id="e1f10-137">hello screen below is an example of how hello tile will look like once you make this customization.</span></span>

![範例 UI](./media/oms-security-web-baseline/oms-security-web-baseline-fig4.png)

> [!NOTE]
> <span data-ttu-id="e1f10-139">如果您想要檢查 hello 基準評估 tooknow hello 設定，您可以下載[這個 Excel 試算表](https://gallery.technet.microsoft.com/OMS-Web-Baseline-1e811690)，其中包含這些設定。</span><span class="sxs-lookup"><span data-stu-id="e1f10-139">If you would like tooknow hello settings that are checked for hello baseline assessment, you can download [this Excel spreadsheet](https://gallery.technet.microsoft.com/OMS-Web-Baseline-1e811690) that contains these settings.</span></span>

## <a name="see-also"></a><span data-ttu-id="e1f10-140">另請參閱</span><span class="sxs-lookup"><span data-stu-id="e1f10-140">See also</span></span>
<span data-ttu-id="e1f10-141">在本文件中，您已了解 OMS 安全性和稽核 Web 基準評估。</span><span class="sxs-lookup"><span data-stu-id="e1f10-141">In this document, you learned about OMS Security and Audit web baseline assessment.</span></span> <span data-ttu-id="e1f10-142">toolearn 進一步了解 OMS 安全性，請參閱下列文章 hello:</span><span class="sxs-lookup"><span data-stu-id="e1f10-142">toolearn more about OMS Security, see hello following articles:</span></span>

* [<span data-ttu-id="e1f10-143">Operations Management Suite (OMS) 概觀</span><span class="sxs-lookup"><span data-stu-id="e1f10-143">Operations Management Suite (OMS) overview</span></span>](operations-management-suite-overview.md)
* [<span data-ttu-id="e1f10-144">監視及回應 tooSecurity 警示在 Operations Management Suite 安全性和稽核解決方案</span><span class="sxs-lookup"><span data-stu-id="e1f10-144">Monitoring and Responding tooSecurity Alerts in Operations Management Suite Security and Audit Solution</span></span>](oms-security-responding-alerts.md)
* [<span data-ttu-id="e1f10-145">在 Operations Management Suite 安全性和稽核解決方案內監視資源</span><span class="sxs-lookup"><span data-stu-id="e1f10-145">Monitoring Resources in Operations Management Suite Security and Audit Solution</span></span>](oms-security-monitoring-resources.md)

