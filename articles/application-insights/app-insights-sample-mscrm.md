---
title: "aaaMicrosoft Dynamics CRM 和 Azure Application Insights |Microsoft 文件"
description: "使用 Application Insights 取得 Microsoft Dynamics CRM Online 遙測。 設定、取得資料、視覺化與匯出的逐步解說。"
services: application-insights
documentationcenter: 
author: mazharmicrosoft
manager: carmonm
ms.assetid: 04c66338-687e-49e5-9975-be935f98f156
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 04/16/2017
ms.author: bwren
ms.openlocfilehash: a39398060d6553fb18a26c101f085b7d87443636
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="walkthrough-enabling-telemetry-for-microsoft-dynamics-crm-online-using-application-insights"></a><span data-ttu-id="e369c-104">逐步解說：使用 Application Insights 啟用Microsoft Dynamics CRM Online 遙測</span><span class="sxs-lookup"><span data-stu-id="e369c-104">Walkthrough: Enabling Telemetry for Microsoft Dynamics CRM Online using Application Insights</span></span>
<span data-ttu-id="e369c-105">本文章將示範如何從 tooget 遙測資料[Microsoft Dynamics CRM Online](https://www.dynamics.com/)使用[Azure Application Insights](https://azure.microsoft.com/services/application-insights/)。</span><span class="sxs-lookup"><span data-stu-id="e369c-105">This article shows you how tooget telemetry data from [Microsoft Dynamics CRM Online](https://www.dynamics.com/) using [Azure Application Insights](https://azure.microsoft.com/services/application-insights/).</span></span> <span data-ttu-id="e369c-106">我們將逐步 hello 加入 Application Insights 指令碼 tooyour 應用程式、 擷取資料和資料視覺效果的完整程序。</span><span class="sxs-lookup"><span data-stu-id="e369c-106">We’ll walk through hello complete process of adding Application Insights script tooyour application, capturing data, and data visualization.</span></span>

> [!NOTE]
> <span data-ttu-id="e369c-107">[瀏覽 hello 範例方案](https://dynamicsandappinsights.codeplex.com/)。</span><span class="sxs-lookup"><span data-stu-id="e369c-107">[Browse hello sample solution](https://dynamicsandappinsights.codeplex.com/).</span></span>
> 
> 

## <a name="add-application-insights-toonew-or-existing-crm-online-instance"></a><span data-ttu-id="e369c-108">加入 Application Insights toonew 或現有的 CRM Online 執行個體</span><span class="sxs-lookup"><span data-stu-id="e369c-108">Add Application Insights toonew or existing CRM Online instance</span></span>
<span data-ttu-id="e369c-109">toomonitor 應用程式新增 Application Insights SDK tooyour 應用程式。</span><span class="sxs-lookup"><span data-stu-id="e369c-109">toomonitor your application, you add an Application Insights SDK tooyour application.</span></span> <span data-ttu-id="e369c-110">hello SDK 傳送遙測 toohello [Application Insights 入口網站](https://portal.azure.com)，其中您可以使用我們的功能強大的分析與診斷工具，或匯出 hello 資料 toostorage。</span><span class="sxs-lookup"><span data-stu-id="e369c-110">hello SDK sends telemetry toohello [Application Insights portal](https://portal.azure.com), where you can use our powerful analysis and diagnostic tools, or export hello data toostorage.</span></span>

### <a name="create-an-application-insights-resource-in-azure"></a><span data-ttu-id="e369c-111">在 Azure 中建立 Application Insights 資源</span><span class="sxs-lookup"><span data-stu-id="e369c-111">Create an Application Insights resource in Azure</span></span>
1. <span data-ttu-id="e369c-112">取得 [Microsoft Azure 帳戶](http://azure.com/pricing)。</span><span class="sxs-lookup"><span data-stu-id="e369c-112">Get [an account in Microsoft Azure](http://azure.com/pricing).</span></span> 
2. <span data-ttu-id="e369c-113">登入 hello [Azure 入口網站](https://portal.azure.com)並加入新的 Application Insights 資源。</span><span class="sxs-lookup"><span data-stu-id="e369c-113">Sign into hello [Azure portal](https://portal.azure.com) and add a new Application Insights resource.</span></span> <span data-ttu-id="e369c-114">這是處理與顯示您資料的位置。</span><span class="sxs-lookup"><span data-stu-id="e369c-114">This is where your data will be processed and displayed.</span></span>
   
    ![按一下 [+]、[開發人員服務]、[Application Insights]。](./media/app-insights-sample-mscrm/01.png)
   
    <span data-ttu-id="e369c-116">選擇 ASP.NET 做為 hello 應用程式類型。</span><span class="sxs-lookup"><span data-stu-id="e369c-116">Choose ASP.NET as hello application type.</span></span>
3. <span data-ttu-id="e369c-117">開啟 hello 開始使用 頁面，並開啟 「 監視及診斷用戶端 」。</span><span class="sxs-lookup"><span data-stu-id="e369c-117">Open hello Getting Started page and open "Monitor and diagnose client side".</span></span>
   
    ![可在您網頁中進行插入的程式碼片段](./media/app-insights-sample-mscrm/03.png)

<span data-ttu-id="e369c-119">**保持開啟 hello 字碼頁**而您不要 hello 另一個瀏覽器視窗中的下一個步驟。</span><span class="sxs-lookup"><span data-stu-id="e369c-119">**Keep hello code page open** while you do hello next step in another browser window.</span></span> <span data-ttu-id="e369c-120">您將很快就需要 hello 程式碼。</span><span class="sxs-lookup"><span data-stu-id="e369c-120">You'll need hello code soon.</span></span> 

### <a name="create-a-javascript-web-resource-in-microsoft-dynamics-crm"></a><span data-ttu-id="e369c-121">在 Microsoft Dynamics CRM 中建立 JavaScript Web 資源</span><span class="sxs-lookup"><span data-stu-id="e369c-121">Create a JavaScript web resource in Microsoft Dynamics CRM</span></span>
1. <span data-ttu-id="e369c-122">開啟您的 CRM Online 執行個體並使用系統管理員權限登入。</span><span class="sxs-lookup"><span data-stu-id="e369c-122">Open your CRM Online instance and login with administrator privileges.</span></span>
2. <span data-ttu-id="e369c-123">開啟 [Microsoft Dynamics CRM 設定] 自訂項目，自訂 hello 系統</span><span class="sxs-lookup"><span data-stu-id="e369c-123">Open Microsoft Dynamics CRM Settings, Customizations, Customize hello System</span></span>
   
    ![Microsoft Dynamics CRM 設定](./media/app-insights-sample-mscrm/04.png)
   
    ![[設定] > [自訂]](./media/app-insights-sample-mscrm/05.png)

    ![自訂 hello 系統選項](./media/app-insights-sample-mscrm/06.png)

1. <span data-ttu-id="e369c-127">建立 JavaScript 資源。</span><span class="sxs-lookup"><span data-stu-id="e369c-127">Create a JavaScript resource.</span></span>
   
    ![新增 Web 資源對話方塊](./media/app-insights-sample-mscrm/07.png)
   
    <span data-ttu-id="e369c-129">指定它的名稱，選取**指令碼 (JScript)**和開啟 hello 文字編輯器。</span><span class="sxs-lookup"><span data-stu-id="e369c-129">Give it a name, select **Script (JScript)** and open hello text editor.</span></span>
   
    ![開啟的 hello 文字編輯器](./media/app-insights-sample-mscrm/08.png)
2. <span data-ttu-id="e369c-131">從 Application Insights 複製 hello 程式碼。</span><span class="sxs-lookup"><span data-stu-id="e369c-131">Copy hello code from Application Insights.</span></span> <span data-ttu-id="e369c-132">複製時請確定 tooignore 指令碼標記。</span><span class="sxs-lookup"><span data-stu-id="e369c-132">While copying make sure tooignore script tags.</span></span> <span data-ttu-id="e369c-133">請參閱以下螢幕擷取畫面：</span><span class="sxs-lookup"><span data-stu-id="e369c-133">Refer below screenshot:</span></span>
   
    ![設定您的檢測金鑰](./media/app-insights-sample-mscrm/09.png)
   
    <span data-ttu-id="e369c-135">hello 程式碼包含 hello 識別您的 Application insights 資源的檢測金鑰。</span><span class="sxs-lookup"><span data-stu-id="e369c-135">hello code includes hello instrumentation key that identifies your Application insights resource.</span></span>
3. <span data-ttu-id="e369c-136">儲存並發佈。</span><span class="sxs-lookup"><span data-stu-id="e369c-136">Save and publish.</span></span>
   
    ![儲存並發佈](./media/app-insights-sample-mscrm/10.png)

### <a name="instrument-forms"></a><span data-ttu-id="e369c-138">檢測表單</span><span class="sxs-lookup"><span data-stu-id="e369c-138">Instrument Forms</span></span>
1. <span data-ttu-id="e369c-139">在 Microsoft CRM Online 中，開啟 hello 帳戶表單</span><span class="sxs-lookup"><span data-stu-id="e369c-139">In Microsoft CRM Online, open hello Account form</span></span>
   
    ![帳戶表單](./media/app-insights-sample-mscrm/11.png)
2. <span data-ttu-id="e369c-141">開啟 hello 表單屬性</span><span class="sxs-lookup"><span data-stu-id="e369c-141">Open hello form Properties</span></span>
   
    ![表單屬性](./media/app-insights-sample-mscrm/12.png)
3. <span data-ttu-id="e369c-143">新增 hello JavaScript 所建立的 web 資源</span><span class="sxs-lookup"><span data-stu-id="e369c-143">Add hello JavaScript web resource that you created</span></span>
   
    ![[新增] 功能表](./media/app-insights-sample-mscrm/13.png)
   
    ![新增 hello web 資源](./media/app-insights-sample-mscrm/14.png)
4. <span data-ttu-id="e369c-146">儲存並發佈您的表單自訂內容。</span><span class="sxs-lookup"><span data-stu-id="e369c-146">Save and publish your form customizations.</span></span>

## <a name="metrics-captured"></a><span data-ttu-id="e369c-147">擷取的度量</span><span class="sxs-lookup"><span data-stu-id="e369c-147">Metrics captured</span></span>
<span data-ttu-id="e369c-148">您現在已設定遙測擷取 hello 表單。</span><span class="sxs-lookup"><span data-stu-id="e369c-148">You have now set up telemetry capture for hello form.</span></span> <span data-ttu-id="e369c-149">只要使用時，資料將傳送 tooyour Application Insights 資源。</span><span class="sxs-lookup"><span data-stu-id="e369c-149">Whenever it is used, data will be sent tooyour Application Insights resource.</span></span>

<span data-ttu-id="e369c-150">以下是您會看到的 hello 資料的範例。</span><span class="sxs-lookup"><span data-stu-id="e369c-150">Here are samples of hello data that you'll see.</span></span>

#### <a name="application-health"></a><span data-ttu-id="e369c-151">應用程式健全狀況</span><span class="sxs-lookup"><span data-stu-id="e369c-151">Application health</span></span>
![範例頁面載入時間](./media/app-insights-sample-mscrm/15.png)

![範例頁面檢視圖表](./media/app-insights-sample-mscrm/16.png)

<span data-ttu-id="e369c-154">瀏覽器例外狀況：</span><span class="sxs-lookup"><span data-stu-id="e369c-154">Browser exceptions:</span></span>

![瀏覽器例外狀況圖表](./media/app-insights-sample-mscrm/17.png)

<span data-ttu-id="e369c-156">按一下 hello 圖表 tooget 更多詳細資料：</span><span class="sxs-lookup"><span data-stu-id="e369c-156">Click hello chart tooget more detail:</span></span>

![例外狀況清單](./media/app-insights-sample-mscrm/18.png)

#### <a name="usage"></a><span data-ttu-id="e369c-158">使用量</span><span class="sxs-lookup"><span data-stu-id="e369c-158">Usage</span></span>
![使用者數、工作階段數及頁面檢視數](./media/app-insights-sample-mscrm/19.png)

![工作階段圖表](./media/app-insights-sample-mscrm/20.png)

![瀏覽器版本](./media/app-insights-sample-mscrm/21.png)

#### <a name="browsers"></a><span data-ttu-id="e369c-162">瀏覽器</span><span class="sxs-lookup"><span data-stu-id="e369c-162">Browsers</span></span>
![頁面載入時間明細](./media/app-insights-sample-mscrm/22.png)

![依瀏覽器版本區分的工作階段計數](./media/app-insights-sample-mscrm/23.png)

#### <a name="geolocation"></a><span data-ttu-id="e369c-165">地理位置</span><span class="sxs-lookup"><span data-stu-id="e369c-165">Geolocation</span></span>
![依國家/地區區分的工作階段計數](./media/app-insights-sample-mscrm/24.png)

![依國家/地區區分的工作階段數和使用者數](./media/app-insights-sample-mscrm/25.png)

#### <a name="inside-page-view-request"></a><span data-ttu-id="e369c-168">深入了解頁面檢視要求</span><span class="sxs-lookup"><span data-stu-id="e369c-168">Inside page view request</span></span>
![頁面檢視摘要](./media/app-insights-sample-mscrm/26.png)

![依頁面檢視事件進行搜尋](./media/app-insights-sample-mscrm/27.png)

![相似頁面檢視數](./media/app-insights-sample-mscrm/28.png)

![頁面檢視屬性](./media/app-insights-sample-mscrm/29.png)

![每個工作階段的頁面數](./media/app-insights-sample-mscrm/30.png)

## <a name="sample-code"></a><span data-ttu-id="e369c-174">範例程式碼</span><span class="sxs-lookup"><span data-stu-id="e369c-174">Sample code</span></span>
<span data-ttu-id="e369c-175">[瀏覽 hello 範例程式碼](https://dynamicsandappinsights.codeplex.com/)。</span><span class="sxs-lookup"><span data-stu-id="e369c-175">[Browse hello sample code](https://dynamicsandappinsights.codeplex.com/).</span></span>

## <a name="power-bi"></a><span data-ttu-id="e369c-176">Power BI</span><span class="sxs-lookup"><span data-stu-id="e369c-176">Power BI</span></span>
<span data-ttu-id="e369c-177">您可以執行甚至更深入分析，如果您[匯出 hello 資料 tooMicrosoft Power BI](app-insights-export-power-bi.md)。</span><span class="sxs-lookup"><span data-stu-id="e369c-177">You can do even deeper analysis if you [export hello data tooMicrosoft Power BI](app-insights-export-power-bi.md).</span></span>

## <a name="sample-microsoft-dynamics-crm-solution"></a><span data-ttu-id="e369c-178">Microsoft Dynamics CRM 解決方案範例</span><span class="sxs-lookup"><span data-stu-id="e369c-178">Sample Microsoft Dynamics CRM Solution</span></span>
<span data-ttu-id="e369c-179">[以下是在 Microsoft Dynamics CRM 中實作的 hello 範例方案](https://dynamicsandappinsights.codeplex.com/)。</span><span class="sxs-lookup"><span data-stu-id="e369c-179">[Here is hello sample solution implemented in Microsoft Dynamics CRM](https://dynamicsandappinsights.codeplex.com/).</span></span>

## <a name="learn-more"></a><span data-ttu-id="e369c-180">詳細資訊</span><span class="sxs-lookup"><span data-stu-id="e369c-180">Learn more</span></span>
* [<span data-ttu-id="e369c-181">什麼是 Application Insights？</span><span class="sxs-lookup"><span data-stu-id="e369c-181">What is Application Insights?</span></span>](app-insights-overview.md)
* [<span data-ttu-id="e369c-182">適用於網頁的 Application Insights</span><span class="sxs-lookup"><span data-stu-id="e369c-182">Application Insights for web pages</span></span>](app-insights-javascript.md)
* [<span data-ttu-id="e369c-183">更多範例和逐步解說</span><span class="sxs-lookup"><span data-stu-id="e369c-183">More samples and walkthroughs</span></span>](app-insights-code-samples.md)
