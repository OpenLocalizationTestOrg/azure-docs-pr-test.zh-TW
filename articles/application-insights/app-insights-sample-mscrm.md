---
title: "Microsoft Dynamics CRM 和 Azure Application Insights | Microsoft Docs"
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
ms.openlocfilehash: a9593d5f198e05db80451a599428a296ed02e781
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/18/2017
---
# <a name="walkthrough-enabling-telemetry-for-microsoft-dynamics-crm-online-using-application-insights"></a><span data-ttu-id="2bd80-104">逐步解說：使用 Application Insights 啟用Microsoft Dynamics CRM Online 遙測</span><span class="sxs-lookup"><span data-stu-id="2bd80-104">Walkthrough: Enabling Telemetry for Microsoft Dynamics CRM Online using Application Insights</span></span>
<span data-ttu-id="2bd80-105">本文說明如何使用 [Azure Application Insights](https://azure.microsoft.com/services/application-insights/) 從 [Microsoft Dynamics CRM Online](https://www.dynamics.com/) 取得遙測資料。</span><span class="sxs-lookup"><span data-stu-id="2bd80-105">This article shows you how to get telemetry data from [Microsoft Dynamics CRM Online](https://www.dynamics.com/) using [Azure Application Insights](https://azure.microsoft.com/services/application-insights/).</span></span> <span data-ttu-id="2bd80-106">我們會逐步解說將 Application Insights 指令碼加入至您的應用程式、擷取資料和資料視覺化的完整程序。</span><span class="sxs-lookup"><span data-stu-id="2bd80-106">We’ll walk through the complete process of adding Application Insights script to your application, capturing data, and data visualization.</span></span>

> [!NOTE]
> <span data-ttu-id="2bd80-107">[瀏覽範例解決方案](https://dynamicsandappinsights.codeplex.com/)。</span><span class="sxs-lookup"><span data-stu-id="2bd80-107">[Browse the sample solution](https://dynamicsandappinsights.codeplex.com/).</span></span>
> 
> 

## <a name="add-application-insights-to-new-or-existing-crm-online-instance"></a><span data-ttu-id="2bd80-108">將 Application Insights 加入至新的或現有的 CRM Online 執行個體</span><span class="sxs-lookup"><span data-stu-id="2bd80-108">Add Application Insights to new or existing CRM Online instance</span></span>
<span data-ttu-id="2bd80-109">若要監視您的應用程式，請將 Application Insights SDK 加入應用程式。</span><span class="sxs-lookup"><span data-stu-id="2bd80-109">To monitor your application, you add an Application Insights SDK to your application.</span></span> <span data-ttu-id="2bd80-110">所有 SDK 均會將遙測資料傳送至 [Application Insights 入口網站](https://portal.azure.com)，您可以在該入口網站中使用我們功能強大的分析與診斷工具，並將資料匯出至儲存體。</span><span class="sxs-lookup"><span data-stu-id="2bd80-110">The SDK sends telemetry to the [Application Insights portal](https://portal.azure.com), where you can use our powerful analysis and diagnostic tools, or export the data to storage.</span></span>

### <a name="create-an-application-insights-resource-in-azure"></a><span data-ttu-id="2bd80-111">在 Azure 中建立 Application Insights 資源</span><span class="sxs-lookup"><span data-stu-id="2bd80-111">Create an Application Insights resource in Azure</span></span>
1. <span data-ttu-id="2bd80-112">取得 [Microsoft Azure 帳戶](http://azure.com/pricing)。</span><span class="sxs-lookup"><span data-stu-id="2bd80-112">Get [an account in Microsoft Azure](http://azure.com/pricing).</span></span> 
2. <span data-ttu-id="2bd80-113">登入 [Azure 入口網站](https://portal.azure.com) 並加入新的 Application Insights 資源。</span><span class="sxs-lookup"><span data-stu-id="2bd80-113">Sign into the [Azure portal](https://portal.azure.com) and add a new Application Insights resource.</span></span> <span data-ttu-id="2bd80-114">這是處理與顯示您資料的位置。</span><span class="sxs-lookup"><span data-stu-id="2bd80-114">This is where your data will be processed and displayed.</span></span>
   
    ![按一下 [+]、[開發人員服務]、[Application Insights]。](./media/app-insights-sample-mscrm/01.png)
   
    <span data-ttu-id="2bd80-116">選擇 ASP.NET 做為應用程式類型。</span><span class="sxs-lookup"><span data-stu-id="2bd80-116">Choose ASP.NET as the application type.</span></span>
3. <span data-ttu-id="2bd80-117">開啟 [開始使用] 頁面，然後開啟 [監視及診斷用戶端]。</span><span class="sxs-lookup"><span data-stu-id="2bd80-117">Open the Getting Started page and open "Monitor and diagnose client side".</span></span>
   
    ![可在您網頁中進行插入的程式碼片段](./media/app-insights-sample-mscrm/03.png)

<span data-ttu-id="2bd80-119">**保持程式碼頁面開啟** 。</span><span class="sxs-lookup"><span data-stu-id="2bd80-119">**Keep the code page open** while you do the next step in another browser window.</span></span> <span data-ttu-id="2bd80-120">您很快就會需要程式碼。</span><span class="sxs-lookup"><span data-stu-id="2bd80-120">You'll need the code soon.</span></span> 

### <a name="create-a-javascript-web-resource-in-microsoft-dynamics-crm"></a><span data-ttu-id="2bd80-121">在 Microsoft Dynamics CRM 中建立 JavaScript Web 資源</span><span class="sxs-lookup"><span data-stu-id="2bd80-121">Create a JavaScript web resource in Microsoft Dynamics CRM</span></span>
1. <span data-ttu-id="2bd80-122">開啟您的 CRM Online 執行個體並使用系統管理員權限登入。</span><span class="sxs-lookup"><span data-stu-id="2bd80-122">Open your CRM Online instance and login with administrator privileges.</span></span>
2. <span data-ttu-id="2bd80-123">開啟 [Microsoft Dynamics CRM 設定]、[自訂]、[自訂系統]</span><span class="sxs-lookup"><span data-stu-id="2bd80-123">Open Microsoft Dynamics CRM Settings, Customizations, Customize the System</span></span>
   
    ![Microsoft Dynamics CRM 設定](./media/app-insights-sample-mscrm/04.png)
   
    ![[設定] > [自訂]](./media/app-insights-sample-mscrm/05.png)

    ![[自訂系統] 選項](./media/app-insights-sample-mscrm/06.png)

1. <span data-ttu-id="2bd80-127">建立 JavaScript 資源。</span><span class="sxs-lookup"><span data-stu-id="2bd80-127">Create a JavaScript resource.</span></span>
   
    ![新增 Web 資源對話方塊](./media/app-insights-sample-mscrm/07.png)
   
    <span data-ttu-id="2bd80-129">命名資源、選取 **指令碼 (JScript)** 並開啟文字編輯器。</span><span class="sxs-lookup"><span data-stu-id="2bd80-129">Give it a name, select **Script (JScript)** and open the text editor.</span></span>
   
    ![開啟文字編輯器](./media/app-insights-sample-mscrm/08.png)
2. <span data-ttu-id="2bd80-131">從 Application Insights 複製程式碼。</span><span class="sxs-lookup"><span data-stu-id="2bd80-131">Copy the code from Application Insights.</span></span> <span data-ttu-id="2bd80-132">在複製時請務必略過 script 標記。</span><span class="sxs-lookup"><span data-stu-id="2bd80-132">While copying make sure to ignore script tags.</span></span> <span data-ttu-id="2bd80-133">請參閱以下螢幕擷取畫面：</span><span class="sxs-lookup"><span data-stu-id="2bd80-133">Refer below screenshot:</span></span>
   
    ![設定您的檢測金鑰](./media/app-insights-sample-mscrm/09.png)
   
    <span data-ttu-id="2bd80-135">程式碼包含用來識別您 Application insights 資源的檢測金鑰。</span><span class="sxs-lookup"><span data-stu-id="2bd80-135">The code includes the instrumentation key that identifies your Application insights resource.</span></span>
3. <span data-ttu-id="2bd80-136">儲存並發佈。</span><span class="sxs-lookup"><span data-stu-id="2bd80-136">Save and publish.</span></span>
   
    ![儲存並發佈](./media/app-insights-sample-mscrm/10.png)

### <a name="instrument-forms"></a><span data-ttu-id="2bd80-138">檢測表單</span><span class="sxs-lookup"><span data-stu-id="2bd80-138">Instrument Forms</span></span>
1. <span data-ttu-id="2bd80-139">在 Microsoft CRM Online 中，開啟 [帳戶] 表單</span><span class="sxs-lookup"><span data-stu-id="2bd80-139">In Microsoft CRM Online, open the Account form</span></span>
   
    ![帳戶表單](./media/app-insights-sample-mscrm/11.png)
2. <span data-ttu-id="2bd80-141">開啟 [表單屬性]</span><span class="sxs-lookup"><span data-stu-id="2bd80-141">Open the form Properties</span></span>
   
    ![表單屬性](./media/app-insights-sample-mscrm/12.png)
3. <span data-ttu-id="2bd80-143">加入您建立的 JavaScript Web 資源</span><span class="sxs-lookup"><span data-stu-id="2bd80-143">Add the JavaScript web resource that you created</span></span>
   
    ![[新增] 功能表](./media/app-insights-sample-mscrm/13.png)
   
    ![新增 Web 資源](./media/app-insights-sample-mscrm/14.png)
4. <span data-ttu-id="2bd80-146">儲存並發佈您的表單自訂內容。</span><span class="sxs-lookup"><span data-stu-id="2bd80-146">Save and publish your form customizations.</span></span>

## <a name="metrics-captured"></a><span data-ttu-id="2bd80-147">擷取的度量</span><span class="sxs-lookup"><span data-stu-id="2bd80-147">Metrics captured</span></span>
<span data-ttu-id="2bd80-148">您現在已設定遙測擷取表單。</span><span class="sxs-lookup"><span data-stu-id="2bd80-148">You have now set up telemetry capture for the form.</span></span> <span data-ttu-id="2bd80-149">只要使用，資料就會傳送至 Application Insights 資源。</span><span class="sxs-lookup"><span data-stu-id="2bd80-149">Whenever it is used, data will be sent to your Application Insights resource.</span></span>

<span data-ttu-id="2bd80-150">以下是您會看到的資料範例。</span><span class="sxs-lookup"><span data-stu-id="2bd80-150">Here are samples of the data that you'll see.</span></span>

#### <a name="application-health"></a><span data-ttu-id="2bd80-151">應用程式健全狀況</span><span class="sxs-lookup"><span data-stu-id="2bd80-151">Application health</span></span>
![範例頁面載入時間](./media/app-insights-sample-mscrm/15.png)

![範例頁面檢視圖表](./media/app-insights-sample-mscrm/16.png)

<span data-ttu-id="2bd80-154">瀏覽器例外狀況：</span><span class="sxs-lookup"><span data-stu-id="2bd80-154">Browser exceptions:</span></span>

![瀏覽器例外狀況圖表](./media/app-insights-sample-mscrm/17.png)

<span data-ttu-id="2bd80-156">按一下圖表以取得詳細資料：</span><span class="sxs-lookup"><span data-stu-id="2bd80-156">Click the chart to get more detail:</span></span>

![例外狀況清單](./media/app-insights-sample-mscrm/18.png)

#### <a name="usage"></a><span data-ttu-id="2bd80-158">使用量</span><span class="sxs-lookup"><span data-stu-id="2bd80-158">Usage</span></span>
![使用者數、工作階段數及頁面檢視數](./media/app-insights-sample-mscrm/19.png)

![工作階段圖表](./media/app-insights-sample-mscrm/20.png)

![瀏覽器版本](./media/app-insights-sample-mscrm/21.png)

#### <a name="browsers"></a><span data-ttu-id="2bd80-162">瀏覽器</span><span class="sxs-lookup"><span data-stu-id="2bd80-162">Browsers</span></span>
![頁面載入時間明細](./media/app-insights-sample-mscrm/22.png)

![依瀏覽器版本區分的工作階段計數](./media/app-insights-sample-mscrm/23.png)

#### <a name="geolocation"></a><span data-ttu-id="2bd80-165">地理位置</span><span class="sxs-lookup"><span data-stu-id="2bd80-165">Geolocation</span></span>
![依國家/地區區分的工作階段計數](./media/app-insights-sample-mscrm/24.png)

![依國家/地區區分的工作階段數和使用者數](./media/app-insights-sample-mscrm/25.png)

#### <a name="inside-page-view-request"></a><span data-ttu-id="2bd80-168">深入了解頁面檢視要求</span><span class="sxs-lookup"><span data-stu-id="2bd80-168">Inside page view request</span></span>
![頁面檢視摘要](./media/app-insights-sample-mscrm/26.png)

![依頁面檢視事件進行搜尋](./media/app-insights-sample-mscrm/27.png)

![相似頁面檢視數](./media/app-insights-sample-mscrm/28.png)

![頁面檢視屬性](./media/app-insights-sample-mscrm/29.png)

![每個工作階段的頁面數](./media/app-insights-sample-mscrm/30.png)

## <a name="sample-code"></a><span data-ttu-id="2bd80-174">範例程式碼</span><span class="sxs-lookup"><span data-stu-id="2bd80-174">Sample code</span></span>
<span data-ttu-id="2bd80-175">[取得範例程式碼](https://dynamicsandappinsights.codeplex.com/)。</span><span class="sxs-lookup"><span data-stu-id="2bd80-175">[Browse the sample code](https://dynamicsandappinsights.codeplex.com/).</span></span>

## <a name="power-bi"></a><span data-ttu-id="2bd80-176">Power BI</span><span class="sxs-lookup"><span data-stu-id="2bd80-176">Power BI</span></span>
<span data-ttu-id="2bd80-177">如果您 [將資料匯出到 Microsoft Power BI](app-insights-export-power-bi.md)，則可以進行更深入的分析。</span><span class="sxs-lookup"><span data-stu-id="2bd80-177">You can do even deeper analysis if you [export the data to Microsoft Power BI](app-insights-export-power-bi.md).</span></span>

## <a name="sample-microsoft-dynamics-crm-solution"></a><span data-ttu-id="2bd80-178">Microsoft Dynamics CRM 解決方案範例</span><span class="sxs-lookup"><span data-stu-id="2bd80-178">Sample Microsoft Dynamics CRM Solution</span></span>
<span data-ttu-id="2bd80-179">[以下是在 Microsoft Dynamics CRM 中實作的解決方案範例](https://dynamicsandappinsights.codeplex.com/)。</span><span class="sxs-lookup"><span data-stu-id="2bd80-179">[Here is the sample solution implemented in Microsoft Dynamics CRM](https://dynamicsandappinsights.codeplex.com/).</span></span>

## <a name="learn-more"></a><span data-ttu-id="2bd80-180">詳細資訊</span><span class="sxs-lookup"><span data-stu-id="2bd80-180">Learn more</span></span>
* [<span data-ttu-id="2bd80-181">什麼是 Application Insights？</span><span class="sxs-lookup"><span data-stu-id="2bd80-181">What is Application Insights?</span></span>](app-insights-overview.md)
* [<span data-ttu-id="2bd80-182">適用於網頁的 Application Insights</span><span class="sxs-lookup"><span data-stu-id="2bd80-182">Application Insights for web pages</span></span>](app-insights-javascript.md)
* [<span data-ttu-id="2bd80-183">更多範例和逐步解說</span><span class="sxs-lookup"><span data-stu-id="2bd80-183">More samples and walkthroughs</span></span>](app-insights-code-samples.md)
