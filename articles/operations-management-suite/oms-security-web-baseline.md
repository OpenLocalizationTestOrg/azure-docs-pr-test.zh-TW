---
title: "Operations Management Suite 安全性和稽核解決方案 Web 基準 | Microsoft Docs"
description: "本文件說明如何針對合規性和安全性目的，使用 OMS 安全性和稽核解決方案來執行所有受監視 Web 的 Web 基準評估。"
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
ms.openlocfilehash: 0d4707dc0c0ffbf40d0d10a6d12b9709a9655258
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="web-baseline-assessment-in-operations-management-suite-security-and-audit-solution"></a><span data-ttu-id="5ac2f-103">Operations Management Suite 安全性和稽核解決方案中的 Web 基準評估</span><span class="sxs-lookup"><span data-stu-id="5ac2f-103">Web Baseline Assessment in Operations Management Suite Security and Audit Solution</span></span>
<span data-ttu-id="5ac2f-104">本文件協助您使用 [Operations Management Suite (OMS) 安全性和稽核解決方案](operations-management-suite-overview.md)的 Web 基準評估功能，存取受監視資源的安全狀態。</span><span class="sxs-lookup"><span data-stu-id="5ac2f-104">This document helps you to use [Operations Management Suite (OMS) Security and Audit Solution](operations-management-suite-overview.md) web baseline assessment capabilities to access the secure state of your monitored resources.</span></span>

## <a name="what-is-web-baseline-assessment"></a><span data-ttu-id="5ac2f-105">什麼是 Web 基準評估？</span><span class="sxs-lookup"><span data-stu-id="5ac2f-105">What is Web Baseline Assessment?</span></span>
<span data-ttu-id="5ac2f-106">OMS 安全性目前會提供作業系統的安全性基準評估。</span><span class="sxs-lookup"><span data-stu-id="5ac2f-106">Currently OMS Security provides security baseline assessment for operating systems.</span></span> <span data-ttu-id="5ac2f-107">它會每隔 24 小時掃描您伺服器的作業系統設定，並可讓您檢視可能有弱點的設定。</span><span class="sxs-lookup"><span data-stu-id="5ac2f-107">It scans the operating system settings of your servers every 24 hours and provides a view into potentially vulnerable settings.</span></span> <span data-ttu-id="5ac2f-108">如需詳細資訊，請參閱 [Operations Management Suite 安全性和稽核解決方案中的基準評估](oms-security-baseline.md)。</span><span class="sxs-lookup"><span data-stu-id="5ac2f-108">Read [Baseline Assessment in Operations Management Suite Security and Audit Solution](oms-security-baseline.md) for more information on this.</span></span>

<span data-ttu-id="5ac2f-109">Web 基準評估的目的是尋找可能有弱點的 Web 伺服器設定。</span><span class="sxs-lookup"><span data-stu-id="5ac2f-109">The goal of the web baseline assessment is to find potentially vulnerable web server settings.</span></span> <span data-ttu-id="5ac2f-110">Web 基準組態的三個主要來源︰.NET、ASP.NET 和 IIS 組態。</span><span class="sxs-lookup"><span data-stu-id="5ac2f-110">The three primary sources for the web baseline configurations are: .NET, ASP.NET, and IIS configuration.</span></span>  <span data-ttu-id="5ac2f-111">如同作業系統基準評估，OMS 安全性將會每隔 24 小時掃描您的 Web 伺服器，並可讓您檢視其安全性狀態。</span><span class="sxs-lookup"><span data-stu-id="5ac2f-111">Just like the operating system baseline assessment, OMS Security is going to scan your web servers every 24hrs and provide a view into security state of them.</span></span>  <span data-ttu-id="5ac2f-112">在 Internet Information Service (IIS) 中，可以高度自訂組態，以便覆寫各種網站和應用程式層級。</span><span class="sxs-lookup"><span data-stu-id="5ac2f-112">In Internet Information Service (IIS), configurations are highly customizable, which allows various site and application levels to be overridden.</span></span> <span data-ttu-id="5ac2f-113">除了預設的根層級以外，掃描程式會檢查每個應用程式/網站層級的設定。</span><span class="sxs-lookup"><span data-stu-id="5ac2f-113">The scanner checks the settings at each application/site level in addition to the default root level.</span></span> <span data-ttu-id="5ac2f-114">這可協助您找出可能有弱點的設定和位置，並且快速修補。</span><span class="sxs-lookup"><span data-stu-id="5ac2f-114">This helps you to identify potential vulnerability settings locations and quickly remediate.</span></span>


## <a name="web-security-baseline-assessment"></a><span data-ttu-id="5ac2f-115">Web 安全性基準評估</span><span class="sxs-lookup"><span data-stu-id="5ac2f-115">Web Security Baseline Assessment</span></span>
<span data-ttu-id="5ac2f-116">在此預覽版本中，使用 OMS 搜尋選項將可存取這項功能。</span><span class="sxs-lookup"><span data-stu-id="5ac2f-116">For this preview this feature is going to be accessed using the OMS Search option.</span></span> <span data-ttu-id="5ac2f-117">請遵循下列步驟來執行適當的查詢︰</span><span class="sxs-lookup"><span data-stu-id="5ac2f-117">Follow the steps below to perform the appropriated query:</span></span>

1. <span data-ttu-id="5ac2f-118">在 [Microsoft Operations Management Suite] 主儀表板內按一下 [安全性和稽核] 圖格。</span><span class="sxs-lookup"><span data-stu-id="5ac2f-118">In the **Microsoft Operations Management Suite** main dashboard click **Security and Audit** tile.</span></span>
2. <span data-ttu-id="5ac2f-119">在 [安全性和稽核] 儀表板中，按一下 [記錄搜尋] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="5ac2f-119">In the **Security and Audit** dashboard, click **Log Search** button.</span></span>
3. <span data-ttu-id="5ac2f-120">您可以使用的第一個查詢是 **Web 基準評估摘要**。</span><span class="sxs-lookup"><span data-stu-id="5ac2f-120">The first query that you can use is the **Web Baseline Assessment Summary**.</span></span> <span data-ttu-id="5ac2f-121">在 [從這裡開始搜尋] 欄位中，輸入此查詢︰Type=SecurityBaselineSummary BaselineType=web。</span><span class="sxs-lookup"><span data-stu-id="5ac2f-121">In the **Begin search here** field, type this query: Type*=SecurityBaselineSummary BaselineType=web*.</span></span> <span data-ttu-id="5ac2f-122">以下畫面有輸出範例︰</span><span class="sxs-lookup"><span data-stu-id="5ac2f-122">The following screen has an output sample:</span></span>

![Web 基準評估摘要](./media/oms-security-web-baseline/oms-security-web-baseline-fig1-new.png)

> [!NOTE]
> <span data-ttu-id="5ac2f-124">在此查詢中，每筆記錄都會指出在單一伺服器上的評估摘要。</span><span class="sxs-lookup"><span data-stu-id="5ac2f-124">In this query, each record indicates assessment summary on a single server.</span></span>

<span data-ttu-id="5ac2f-125">當您在 [記錄搜尋] 中，您可以輸入不同的查詢，以取得有關 Web 基準評估的詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="5ac2f-125">Once you are in the **Log Search**, you can type different queries to obtain more information about the web baseline assessment.</span></span> <span data-ttu-id="5ac2f-126">除了上述查詢，您也可以在此預覽版本中使用下列查詢。</span><span class="sxs-lookup"><span data-stu-id="5ac2f-126">In addition to the previous query, you can also use the following ones in this preview.</span></span>

<span data-ttu-id="5ac2f-127">**Web 基準規則評估**︰每筆記錄均代表單一伺服器上的單一 Web 基準規則評估。</span><span class="sxs-lookup"><span data-stu-id="5ac2f-127">**Web Baseline Rule Assessment**: Each record represents a single web baseline rule evaluation on a single server.</span></span> <span data-ttu-id="5ac2f-128">它包含規則、位置、預期結果和實際結果的所有資料。</span><span class="sxs-lookup"><span data-stu-id="5ac2f-128">It includes all data for the rule, location, the expected result, and the actual result.</span></span>

<span data-ttu-id="5ac2f-129">**查詢**：Type=SecurityBaseline BaselineType=web</span><span class="sxs-lookup"><span data-stu-id="5ac2f-129">**Query**: Type*=SecurityBaseline BaselineType=web*</span></span>

![Web 基準規則評估](./media/oms-security-web-baseline/oms-security-web-baseline-fig2.png)

<span data-ttu-id="5ac2f-131">**顯示特定伺服器的所有結果**︰此查詢會顯示如何查看特定伺服器的結果。</span><span class="sxs-lookup"><span data-stu-id="5ac2f-131">**Show all results for a specific server**: This query shows how to see results of a specific server.</span></span>

<span data-ttu-id="5ac2f-132">**查詢**：Type=SecurityBaseline BaselineType=web Computer=BaselineTestVM1</span><span class="sxs-lookup"><span data-stu-id="5ac2f-132">**Query**: *Type=SecurityBaseline BaselineType=web Computer=BaselineTestVM1*</span></span>

![所有結果](./media/oms-security-web-baseline/oms-security-web-baseline-fig3.png)

<span data-ttu-id="5ac2f-134">您也可以使用這些記錄/查詢來建立自己的儀表板、報告或警示。</span><span class="sxs-lookup"><span data-stu-id="5ac2f-134">You can also use these records/queries to create your own dashboards, reports, or alerts.</span></span> <span data-ttu-id="5ac2f-135">下列畫面有您可以新增儀表板的範例 UI 控制項。</span><span class="sxs-lookup"><span data-stu-id="5ac2f-135">The screen below has a sample UI control that you can add to your dashboard.</span></span> <span data-ttu-id="5ac2f-136">您可以了解如何使用 [這裡](https://blogs.technet.microsoft.com/msoms/2016/06/30/oms-view-designer-visualize-your-data-your-way/)的 OMS 檢視表設計工具將您的資料視覺化。</span><span class="sxs-lookup"><span data-stu-id="5ac2f-136">You can learn how to visualize your data using OMS View Designer [here](https://blogs.technet.microsoft.com/msoms/2016/06/30/oms-view-designer-visualize-your-data-your-way/).</span></span> <span data-ttu-id="5ac2f-137">下列畫面是您進行此自訂後，圖格的外觀範例。</span><span class="sxs-lookup"><span data-stu-id="5ac2f-137">The screen below is an example of how the tile will look like once you make this customization.</span></span>

![範例 UI](./media/oms-security-web-baseline/oms-security-web-baseline-fig4.png)

> [!NOTE]
> <span data-ttu-id="5ac2f-139">如果您想要知道已針對基準評估進行檢查的設定，您可以下載[這份 Excel 試算表](https://gallery.technet.microsoft.com/OMS-Web-Baseline-1e811690)，其中包含這些設定。</span><span class="sxs-lookup"><span data-stu-id="5ac2f-139">If you would like to know the settings that are checked for the baseline assessment, you can download [this Excel spreadsheet](https://gallery.technet.microsoft.com/OMS-Web-Baseline-1e811690) that contains these settings.</span></span>

## <a name="see-also"></a><span data-ttu-id="5ac2f-140">另請參閱</span><span class="sxs-lookup"><span data-stu-id="5ac2f-140">See also</span></span>
<span data-ttu-id="5ac2f-141">在本文件中，您已了解 OMS 安全性和稽核 Web 基準評估。</span><span class="sxs-lookup"><span data-stu-id="5ac2f-141">In this document, you learned about OMS Security and Audit web baseline assessment.</span></span> <span data-ttu-id="5ac2f-142">若要深入了解 OMS 安全性，請參閱下列文章：</span><span class="sxs-lookup"><span data-stu-id="5ac2f-142">To learn more about OMS Security, see the following articles:</span></span>

* [<span data-ttu-id="5ac2f-143">Operations Management Suite (OMS) 概觀</span><span class="sxs-lookup"><span data-stu-id="5ac2f-143">Operations Management Suite (OMS) overview</span></span>](operations-management-suite-overview.md)
* [<span data-ttu-id="5ac2f-144">在 Operations Management Suite 安全性和稽核內監視及回應安全性警示</span><span class="sxs-lookup"><span data-stu-id="5ac2f-144">Monitoring and Responding to Security Alerts in Operations Management Suite Security and Audit Solution</span></span>](oms-security-responding-alerts.md)
* [<span data-ttu-id="5ac2f-145">在 Operations Management Suite 安全性和稽核解決方案內監視資源</span><span class="sxs-lookup"><span data-stu-id="5ac2f-145">Monitoring Resources in Operations Management Suite Security and Audit Solution</span></span>](oms-security-monitoring-resources.md)

