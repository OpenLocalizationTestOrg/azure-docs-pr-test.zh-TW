---
title: "Machine Learning 建議：JavaScript 整合 | Microsoft Docs"
description: "Azure Machine Learning Recommendations - JavaScript 整合 - 文件"
services: machine-learning
documentationcenter: 
author: LuisCabrer
manager: jhubbard
editor: cgronlun
ms.assetid: bbbb5bb6-489d-4a62-a2ae-f36237e9e2e1
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: javascript
ms.topic: article
ms.date: 03/31/2017
ms.author: luisca
ROBOTS: NOINDEX
redirect_url: machine-learning-datamarket-deprecation
redirect_document_id: True
ms.openlocfilehash: 4c5f0eee4aa04ce823321d52985374c52850f0d6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-machine-learning-recommendations---javascript-integration"></a><span data-ttu-id="06b64-103">Azure Machine Learning Recommendations - JavaScript 整合</span><span class="sxs-lookup"><span data-stu-id="06b64-103">Azure Machine Learning Recommendations - JavaScript Integration</span></span>
> [!NOTE]
> <span data-ttu-id="06b64-104">您應該開始使用 hello 建議 API 認知服務，而不此版本。</span><span class="sxs-lookup"><span data-stu-id="06b64-104">You should start using hello Recommendations API Cognitive Service instead of this version.</span></span> <span data-ttu-id="06b64-105">hello 建議認知服務將會取代此服務，並將那里開發所有 hello 新功能。</span><span class="sxs-lookup"><span data-stu-id="06b64-105">hello Recommendations Cognitive Service will be replacing this service, and all hello new features will be developed there.</span></span> <span data-ttu-id="06b64-106">它會提供新功能，例如，批次支援、更好的 API 總管、更簡潔的 API 介面、更一致的註冊/計費體驗等。</span><span class="sxs-lookup"><span data-stu-id="06b64-106">It has new capabilities like batching support, a better API Explorer, a cleaner API surface, more consistent signup/billing experience, etc.</span></span>
> <span data-ttu-id="06b64-107">深入了解[移轉 toohello 新認知的服務](http://aka.ms/recomigrate)</span><span class="sxs-lookup"><span data-stu-id="06b64-107">Learn more about [Migrating toohello new Cognitive Service](http://aka.ms/recomigrate)</span></span>
> 
> 

<span data-ttu-id="06b64-108">本文件描述如何 toointegrate 您使用 JavaScript 的網站。</span><span class="sxs-lookup"><span data-stu-id="06b64-108">This document depict how toointegrate your site using JavaScript.</span></span> <span data-ttu-id="06b64-109">hello JavaScript 可讓您 toosend 資料擷取的事件和 tooconsume 建議一旦建置推薦模型。</span><span class="sxs-lookup"><span data-stu-id="06b64-109">hello JavaScript enables you toosend Data Acquisition events and tooconsume recommendations once you build a recommendation model.</span></span> <span data-ttu-id="06b64-110">透過 JS 完成的所有操作也能從伺服器端完成。</span><span class="sxs-lookup"><span data-stu-id="06b64-110">All operations done via JS can be also done from server side.</span></span>

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

## <a name="1-general-overview"></a><span data-ttu-id="06b64-111">1.一般概觀</span><span class="sxs-lookup"><span data-stu-id="06b64-111">1. General Overview</span></span>
<span data-ttu-id="06b64-112">利用 2 階段所包含的 Azure ML Recommendations 來整合您的網站：</span><span class="sxs-lookup"><span data-stu-id="06b64-112">Integrating your site with Azure ML Recommendations consist on 2 Phases:</span></span>

1. <span data-ttu-id="06b64-113">將事件傳送到 Azure ML Recommendations。</span><span class="sxs-lookup"><span data-stu-id="06b64-113">Send Events into Azure ML Recommendations.</span></span> <span data-ttu-id="06b64-114">這會讓 toobuild 推薦模型。</span><span class="sxs-lookup"><span data-stu-id="06b64-114">This will enable toobuild a recommendation model.</span></span>
2. <span data-ttu-id="06b64-115">耗用 hello 建議。</span><span class="sxs-lookup"><span data-stu-id="06b64-115">Consume hello recommendations.</span></span> <span data-ttu-id="06b64-116">建立 hello 模型之後，您可以使用 hello 建議。</span><span class="sxs-lookup"><span data-stu-id="06b64-116">After hello model is built you can consume hello recommendations.</span></span> <span data-ttu-id="06b64-117">（此文件並未說明如何讀取 toobuild 模型時，會 hello 快速入門指南 tooget 詳細資訊）。</span><span class="sxs-lookup"><span data-stu-id="06b64-117">(This document does not explain how toobuild a model, read hello quick start guide tooget more information on how).</span></span>

<span data-ttu-id="06b64-118"><ins>第一階段</ins></span><span class="sxs-lookup"><span data-stu-id="06b64-118"><ins>Phase I</ins></span></span>

<span data-ttu-id="06b64-119">Hello 中第一個階段，您將插入至 html 頁面小型的 JavaScript 程式庫，可讓 hello 頁面 toosend 事件 hello html 網頁上發生時於 Azure ML 建議伺服器 （透過資料市場）：</span><span class="sxs-lookup"><span data-stu-id="06b64-119">In hello first phase you insert into your html pages a small JavaScript library that enables hello page toosend events as they occur on hello html page into Azure ML Recommendations servers (via Data Market):</span></span>

![繪圖 1][1]

<span data-ttu-id="06b64-121"><ins>第二階段</ins></span><span class="sxs-lookup"><span data-stu-id="06b64-121"><ins>Phase II</ins></span></span>

<span data-ttu-id="06b64-122">在 [hello 第二個階段，當您想在 hello] 頁面上的 tooshow hello 建議您選取其中一個 hello 下列選項：</span><span class="sxs-lookup"><span data-stu-id="06b64-122">In hello second phase when you want tooshow hello recommendations on hello page you select one of hello following options:</span></span>

<span data-ttu-id="06b64-123">1.您的伺服器 （在頁面上轉譯的 hello 階段） 會呼叫 Azure ML 建議伺服器 （透過資料市場） tooget 建議。</span><span class="sxs-lookup"><span data-stu-id="06b64-123">1.Your server (on hello phase of page rendering) calls Azure ML Recommendations Server (via Data Market) tooget recommendations.</span></span> <span data-ttu-id="06b64-124">hello 結果會包含項目 id 的清單。您的伺服器需要 tooenrich hello 結果與 hello 項目中繼資料 （例如影像、 描述），並傳送 hello 建立頁面 toohello 瀏覽器。</span><span class="sxs-lookup"><span data-stu-id="06b64-124">hello results include a list of items id. Your server needs tooenrich hello results with hello items Meta data (e.g. images, description) and send hello created page toohello browser.</span></span>

![繪圖 2][2]

<span data-ttu-id="06b64-126">2.hello 另一個選項是 toouse hello 小 JavaScript 檔案從階段一個 tooget 建議項目的簡單清單。</span><span class="sxs-lookup"><span data-stu-id="06b64-126">2.hello other option is toouse hello small JavaScript file from phase one tooget a simple list of recommended items.</span></span> <span data-ttu-id="06b64-127">比 hello 第一個選項 hello 一款這裡收到 hello 資料。</span><span class="sxs-lookup"><span data-stu-id="06b64-127">hello data received here is leaner than hello one in hello first option.</span></span>

![繪圖 3][3]

## <a name="2-prerequisites"></a><span data-ttu-id="06b64-129">2.必要條件</span><span class="sxs-lookup"><span data-stu-id="06b64-129">2. Prerequisites</span></span>
1. <span data-ttu-id="06b64-130">建立新的模型使用 hello 應用程式開發介面。</span><span class="sxs-lookup"><span data-stu-id="06b64-130">Create a new model using hello APIs.</span></span> <span data-ttu-id="06b64-131">請參閱 hello 快速入門指南 toodo 它。</span><span class="sxs-lookup"><span data-stu-id="06b64-131">See hello Quick start guide on how toodo it.</span></span>
2. <span data-ttu-id="06b64-132">使用 base64 將 &lt;dataMarketUser&gt;:&lt;dataMarketKey&gt; 編碼。</span><span class="sxs-lookup"><span data-stu-id="06b64-132">Encode your &lt;dataMarketUser&gt;:&lt;dataMarketKey&gt; with base64.</span></span> <span data-ttu-id="06b64-133">（這將用於 hello 基本驗證 tooenable hello JS 程式碼 toocall hello 應用程式開發介面）。</span><span class="sxs-lookup"><span data-stu-id="06b64-133">(This will be used for hello basic authentication tooenable hello JS code toocall hello APIs).</span></span>

## <a name="3-send-data-acquisition-events-using-javascript"></a><span data-ttu-id="06b64-134">3.使用 JavaScript 傳送資料擷取事件</span><span class="sxs-lookup"><span data-stu-id="06b64-134">3. Send Data Acquisition events using JavaScript</span></span>
<span data-ttu-id="06b64-135">下列步驟的 hello 促進傳送事件：</span><span class="sxs-lookup"><span data-stu-id="06b64-135">hello following steps facilitate sending events:</span></span>

1. <span data-ttu-id="06b64-136">在程式碼中納入 JQuery 程式庫。</span><span class="sxs-lookup"><span data-stu-id="06b64-136">Include JQuery library in your code.</span></span> <span data-ttu-id="06b64-137">您可以從下列 URL 的 hello 中的 nuget 下載它。</span><span class="sxs-lookup"><span data-stu-id="06b64-137">You can download it from nuget in hello following URL.</span></span>
   
     <span data-ttu-id="06b64-138">http://www.nuget.org/packages/jQuery/1.8.2</span><span class="sxs-lookup"><span data-stu-id="06b64-138">http://www.nuget.org/packages/jQuery/1.8.2</span></span>
2. <span data-ttu-id="06b64-139">將從下列 URL 的 hello hello 建議 Java 指令碼程式庫包括： http://aka.ms/RecoJSLib1</span><span class="sxs-lookup"><span data-stu-id="06b64-139">Include hello Recommendations Java Script library from hello following URL: http://aka.ms/RecoJSLib1</span></span>
3. <span data-ttu-id="06b64-140">初始化 Azure ML 建議程式庫與 hello 適當的參數。</span><span class="sxs-lookup"><span data-stu-id="06b64-140">Initialize Azure ML Recommendations library with hello appropriate parameters.</span></span>
   
     <span data-ttu-id="06b64-141"><script>AzureMLRecommendationsStart (「<base64encoding of username:key>"，"< model_id >");</script> 
4.傳送嗨適當的事件。</span><span class="sxs-lookup"><span data-stu-id="06b64-141"><script> AzureMLRecommendationsStart("<base64encoding of username:key>", "<model_id>"); </script>
4. Send hello appropriate event.</span></span> <span data-ttu-id="06b64-142">有關所有型別事件的詳細說明 (Click 事件範例)，請參閱下節  <script> 如果 (typeof AzureMLRecommendationsEvent=="undefined") {</span><span class="sxs-lookup"><span data-stu-id="06b64-142">See detailed section below on all type of events (example of click event)  <script> if (typeof AzureMLRecommendationsEvent=="undefined") {</span></span>         
                     <span data-ttu-id="06b64-143">AzureMLRecommendationsEvent = []; } AzureMLRecommendationsEvent.push({ event: "click", item: "18321116" }); </script></span><span class="sxs-lookup"><span data-stu-id="06b64-143">AzureMLRecommendationsEvent = []; } AzureMLRecommendationsEvent.push({ event: "click", item: "18321116" }); </script></span></span>

### <a name="31----limitations-and-browser-support"></a><span data-ttu-id="06b64-144">3.1.</span><span class="sxs-lookup"><span data-stu-id="06b64-144">3.1.</span></span>    <span data-ttu-id="06b64-145">限制和瀏覽器支援</span><span class="sxs-lookup"><span data-stu-id="06b64-145">Limitations and Browser Support</span></span>
<span data-ttu-id="06b64-146">這是參考實作並依現況提供。</span><span class="sxs-lookup"><span data-stu-id="06b64-146">This is a reference implementation and it is given as is.</span></span> <span data-ttu-id="06b64-147">其應該支援所有主要瀏覽器。</span><span class="sxs-lookup"><span data-stu-id="06b64-147">It should support all major browsers.</span></span>

### <a name="32----type-of-events"></a><span data-ttu-id="06b64-148">3.2.</span><span class="sxs-lookup"><span data-stu-id="06b64-148">3.2.</span></span>    <span data-ttu-id="06b64-149">事件類型</span><span class="sxs-lookup"><span data-stu-id="06b64-149">Type of Events</span></span>
<span data-ttu-id="06b64-150">事件的 5 hello 程式庫支援的類型有： 按一下 []，按一下建議，新增 tooShop 購物車，移除購物車及購買。</span><span class="sxs-lookup"><span data-stu-id="06b64-150">There are 5 types of event that hello library supports: Click, Recommendation Click, Add tooShop Cart, Remove from Shop Cart and Purchase.</span></span> <span data-ttu-id="06b64-151">沒有使用的 tooset hello 使用者內容呼叫登入的其他事件。</span><span class="sxs-lookup"><span data-stu-id="06b64-151">There is an additional event that is used tooset hello user context called Login.</span></span>

#### <a name="321-click-event"></a><span data-ttu-id="06b64-152">3.2.1.</span><span class="sxs-lookup"><span data-stu-id="06b64-152">3.2.1.</span></span> <span data-ttu-id="06b64-153">點選事件</span><span class="sxs-lookup"><span data-stu-id="06b64-153">Click Event</span></span>
<span data-ttu-id="06b64-154">每當使用者點選項目時，都應該會使用這個事件。</span><span class="sxs-lookup"><span data-stu-id="06b64-154">This event should be used any time a user clicked on an item.</span></span> <span data-ttu-id="06b64-155">只有當使用者按一下項目時，通常以 hello 項目詳細資料; 開啟新的頁面在此頁面應觸發這個事件。</span><span class="sxs-lookup"><span data-stu-id="06b64-155">Usually when user clicks on an item a new page is opened with hello item details; in this page this event should be triggered.</span></span>

<span data-ttu-id="06b64-156">參數：</span><span class="sxs-lookup"><span data-stu-id="06b64-156">Parameters:</span></span>

* <span data-ttu-id="06b64-157">event (字串, 強制) - “click”</span><span class="sxs-lookup"><span data-stu-id="06b64-157">event (string, mandatory) - “click”</span></span>
* <span data-ttu-id="06b64-158">項目 (string，強制)-hello 項目的唯一識別碼</span><span class="sxs-lookup"><span data-stu-id="06b64-158">item (string, mandatory) - Unique identifier of hello item</span></span>
* <span data-ttu-id="06b64-159">itemName (string，選用)-hello hello 項目名稱</span><span class="sxs-lookup"><span data-stu-id="06b64-159">itemName (string, optional) - hello name of hello item</span></span>
* <span data-ttu-id="06b64-160">itemDescription (string，選用)-hello 項目的 hello 描述</span><span class="sxs-lookup"><span data-stu-id="06b64-160">itemDescription (string, optional) - hello description of hello item</span></span>
* <span data-ttu-id="06b64-161">itemCategory (string，選用)-hello hello 項目分類的</span><span class="sxs-lookup"><span data-stu-id="06b64-161">itemCategory (string, optional) - hello category of hello item</span></span>
  
        <script>
            if (typeof AzureMLRecommendationsEvent == "undefined") { AzureMLRecommendationsEvent = []; }
            AzureMLRecommendationsEvent.push({ event: "click", item: "3111718" });
        </script>

<span data-ttu-id="06b64-162">或使用選擇性資料：</span><span class="sxs-lookup"><span data-stu-id="06b64-162">Or with optional data:</span></span>

        <script>
            if (typeof AzureMLRecommendationsEvent === "undefined") { AzureMLRecommendationsEvent = []; }
            AzureMLRecommendationsEvent.push({event: "click", item: "3111718", itemName: "Plane", itemDescription: "It is a big plane", itemCategory: "Aviation"});
        </script>


#### <a name="322-recommendation-click-event"></a><span data-ttu-id="06b64-163">3.2.2.</span><span class="sxs-lookup"><span data-stu-id="06b64-163">3.2.2.</span></span> <span data-ttu-id="06b64-164">建議點選事件</span><span class="sxs-lookup"><span data-stu-id="06b64-164">Recommendation Click Event</span></span>
<span data-ttu-id="06b64-165">每當使用者點選項目 (從 Azure ML Recommendations 接收當成建議的項目) 時，都應該會使用這個事件。</span><span class="sxs-lookup"><span data-stu-id="06b64-165">This event should be used any time a user clicked on an item that was received from Azure ML Recommendations as a recommended item.</span></span> <span data-ttu-id="06b64-166">只有當使用者按一下項目時，通常以 hello 項目詳細資料; 開啟新的頁面在此頁面應觸發這個事件。</span><span class="sxs-lookup"><span data-stu-id="06b64-166">Usually when user clicks on an item a new page is opened with hello item details; in this page this event should be triggered.</span></span>

<span data-ttu-id="06b64-167">參數：</span><span class="sxs-lookup"><span data-stu-id="06b64-167">Parameters:</span></span>

* <span data-ttu-id="06b64-168">event (字串, 強制) - “recommendationclick”</span><span class="sxs-lookup"><span data-stu-id="06b64-168">event (string, mandatory) - “recommendationclick”</span></span>
* <span data-ttu-id="06b64-169">項目 (string，強制)-hello 項目的唯一識別碼</span><span class="sxs-lookup"><span data-stu-id="06b64-169">item (string, mandatory) - Unique identifier of hello item</span></span>
* <span data-ttu-id="06b64-170">itemName (string，選用)-hello hello 項目名稱</span><span class="sxs-lookup"><span data-stu-id="06b64-170">itemName (string, optional) - hello name of hello item</span></span>
* <span data-ttu-id="06b64-171">itemDescription (string，選用)-hello 項目的 hello 描述</span><span class="sxs-lookup"><span data-stu-id="06b64-171">itemDescription (string, optional) - hello description of hello item</span></span>
* <span data-ttu-id="06b64-172">itemCategory (string，選用)-hello hello 項目分類的</span><span class="sxs-lookup"><span data-stu-id="06b64-172">itemCategory (string, optional) - hello category of hello item</span></span>
* <span data-ttu-id="06b64-173">種子 （字串陣列，選用）-hello 產生 hello 建議查詢的種子。</span><span class="sxs-lookup"><span data-stu-id="06b64-173">seeds (string array, optional) - hello seeds that generated hello recommendation query.</span></span>
* <span data-ttu-id="06b64-174">（字串陣列，選用）-recoList hello hello 建議要求產生已按下的 hello 項的結果。</span><span class="sxs-lookup"><span data-stu-id="06b64-174">recoList (string array, optional) - hello result of hello recommendation request that generated hello item that was clicked.</span></span>
  
        <script>
            if (typeof AzureMLRecommendationsEvent=="undefined") { AzureMLRecommendationsEvent = []; }
            AzureMLRecommendationsEvent.push({event: "recommendationclick", item: "18899918" });
        </script>

<span data-ttu-id="06b64-175">或使用選擇性資料：</span><span class="sxs-lookup"><span data-stu-id="06b64-175">Or with optional data:</span></span>

        <script>
            if (typeof AzureMLRecommendationsEvent == "undefined") { AzureMLRecommendationsEvent = []; }
            AzureMLRecommendationsEvent.push({ event: eventName, item: "198", itemName: "Plane2", itemDescription: "It is a big plane2", itemCategory: "Default2", seeds: ["Seed1", "Seed2"], recoList: ["199", "198", "197"]                 });
        </script>


#### <a name="323-add-shopping-cart-event"></a><span data-ttu-id="06b64-176">3.2.3.</span><span class="sxs-lookup"><span data-stu-id="06b64-176">3.2.3.</span></span> <span data-ttu-id="06b64-177">加入購物車事件</span><span class="sxs-lookup"><span data-stu-id="06b64-177">Add Shopping Cart Event</span></span>
<span data-ttu-id="06b64-178">此事件應該用於當 hello 使用者加入購物車的項目 toohello。</span><span class="sxs-lookup"><span data-stu-id="06b64-178">This event should be used when hello user add an item toohello shopping cart.</span></span>
<span data-ttu-id="06b64-179">參數：</span><span class="sxs-lookup"><span data-stu-id="06b64-179">Parameters:</span></span>

* <span data-ttu-id="06b64-180">event (字串, 強制) - “addshopcart”</span><span class="sxs-lookup"><span data-stu-id="06b64-180">event (string, mandatory) - “addshopcart”</span></span>
* <span data-ttu-id="06b64-181">項目 (string，強制)-hello 項目的唯一識別碼</span><span class="sxs-lookup"><span data-stu-id="06b64-181">item (string, mandatory) - Unique identifier of hello item</span></span>
* <span data-ttu-id="06b64-182">itemName (string，選用)-hello hello 項目名稱</span><span class="sxs-lookup"><span data-stu-id="06b64-182">itemName (string, optional) - hello name of hello item</span></span>
* <span data-ttu-id="06b64-183">itemDescription (string，選用)-hello 項目的 hello 描述</span><span class="sxs-lookup"><span data-stu-id="06b64-183">itemDescription (string, optional) - hello description of hello item</span></span>
* <span data-ttu-id="06b64-184">itemCategory (string，選用)-hello hello 項目分類的</span><span class="sxs-lookup"><span data-stu-id="06b64-184">itemCategory (string, optional) - hello category of hello item</span></span>
  
        <script>
            if (typeof AzureMLRecommendationsEvent == "undefined") { AzureMLRecommendationsEvent = []; }
            AzureMLRecommendationsEvent.push({event: "addshopcart", item: "13221118" });
        </script>

#### <a name="324-remove-shopping-cart-event"></a><span data-ttu-id="06b64-185">3.2.4.</span><span class="sxs-lookup"><span data-stu-id="06b64-185">3.2.4.</span></span> <span data-ttu-id="06b64-186">移除購物車事件</span><span class="sxs-lookup"><span data-stu-id="06b64-186">Remove Shopping Cart Event</span></span>
<span data-ttu-id="06b64-187">Hello 使用者移除項目 toohello 購物車時，應該使用這個事件。</span><span class="sxs-lookup"><span data-stu-id="06b64-187">This event should be used when hello user removes an item toohello shopping cart.</span></span>

<span data-ttu-id="06b64-188">參數：</span><span class="sxs-lookup"><span data-stu-id="06b64-188">Parameters:</span></span>

* <span data-ttu-id="06b64-189">event (字串, 強制) - “removeshopcart”</span><span class="sxs-lookup"><span data-stu-id="06b64-189">event (string, mandatory) - “removeshopcart”</span></span>
* <span data-ttu-id="06b64-190">項目 (string，強制)-hello 項目的唯一識別碼</span><span class="sxs-lookup"><span data-stu-id="06b64-190">item (string, mandatory) - Unique identifier of hello item</span></span>
* <span data-ttu-id="06b64-191">itemName (string，選用)-hello hello 項目名稱</span><span class="sxs-lookup"><span data-stu-id="06b64-191">itemName (string, optional) - hello name of hello item</span></span>
* <span data-ttu-id="06b64-192">itemDescription (string，選用)-hello 項目的 hello 描述</span><span class="sxs-lookup"><span data-stu-id="06b64-192">itemDescription (string, optional) - hello description of hello item</span></span>
* <span data-ttu-id="06b64-193">itemCategory (string，選用)-hello hello 項目分類的</span><span class="sxs-lookup"><span data-stu-id="06b64-193">itemCategory (string, optional) - hello category of hello item</span></span>
  
        <script>
            if (typeof AzureMLRecommendationsEvent=="undefined") { AzureMLRecommendationsEvent = []; }
            AzureMLRecommendationsEvent.push({ event: "removeshopcart", item: "111118" });
        </script>

#### <a name="325-purchase-event"></a><span data-ttu-id="06b64-194">3.2.5.</span><span class="sxs-lookup"><span data-stu-id="06b64-194">3.2.5.</span></span> <span data-ttu-id="06b64-195">購買事件</span><span class="sxs-lookup"><span data-stu-id="06b64-195">Purchase Event</span></span>
<span data-ttu-id="06b64-196">Hello 使用者購買他購物車時，應該使用這個事件。</span><span class="sxs-lookup"><span data-stu-id="06b64-196">This event should be used when hello user purchased his shopping cart.</span></span>

<span data-ttu-id="06b64-197">參數：</span><span class="sxs-lookup"><span data-stu-id="06b64-197">Parameters:</span></span>

* <span data-ttu-id="06b64-198">event (字串) - “purchase”</span><span class="sxs-lookup"><span data-stu-id="06b64-198">event (string) - “purchase”</span></span>
* <span data-ttu-id="06b64-199">items (Purchased[]) - 陣列會為購買的每個項目保留一個項目。</span><span class="sxs-lookup"><span data-stu-id="06b64-199">items ( Purchased[] ) - Array holding an entry for each item purchased.</span></span><br><br>
  <span data-ttu-id="06b64-200">已購買項目的格式︰</span><span class="sxs-lookup"><span data-stu-id="06b64-200">Purchased format:</span></span>
  * <span data-ttu-id="06b64-201">項目 （字串）-hello 項目的唯一識別碼。</span><span class="sxs-lookup"><span data-stu-id="06b64-201">item (string) - Unique identifier of hello item.</span></span>
  * <span data-ttu-id="06b64-202">count (整數或字串) - 已購買的項目數。</span><span class="sxs-lookup"><span data-stu-id="06b64-202">count (int or string) - number of items that were purchased.</span></span>
  * <span data-ttu-id="06b64-203">價格 （float 或字串） 為選擇性欄位-hello 價格 hello 項目。</span><span class="sxs-lookup"><span data-stu-id="06b64-203">price (float or string) - optional field - hello price of hello item.</span></span>

<span data-ttu-id="06b64-204">hello 下面範例 3 購買項目 （33、 34、 35），其中包含所有已填入欄位項目、 計數 （價格） 和一個 （項目 34） 沒有價格的兩個。</span><span class="sxs-lookup"><span data-stu-id="06b64-204">hello example below shows purchase of 3 items (33, 34, 35), two with all fields populated (item, count, price) and one (item 34) without a price.</span></span>

        <script>
            if ( typeof AzureMLRecommendationsEvent == "undefined"){ AzureMLRecommendationsEvent = []; }
            AzureMLRecommendationsEvent.push({ event: "purchase", items: [{ item: "33", count: "1", price: "10" }, { item: "34", count: "2" }, { item: "35", count: "1", price: "210" }] });
        </script>

#### <a name="326-user-login-event"></a><span data-ttu-id="06b64-205">3.2.6.</span><span class="sxs-lookup"><span data-stu-id="06b64-205">3.2.6.</span></span> <span data-ttu-id="06b64-206">使用者登入事件</span><span class="sxs-lookup"><span data-stu-id="06b64-206">User Login Event</span></span>
<span data-ttu-id="06b64-207">Azure ML 建議事件程式庫會建立並使用來自順序 tooidentify 事件中的 cookie hello 相同的瀏覽器。</span><span class="sxs-lookup"><span data-stu-id="06b64-207">Azure ML Recommendations Event library creates and use a cookie in order tooidentify events that came from hello same browser.</span></span> <span data-ttu-id="06b64-208">在訂單 tooimprove hello 模型結果 Azure ML 建議可讓 tooset 使用者的唯一識別碼，將會覆寫 hello cookie 使用方式。</span><span class="sxs-lookup"><span data-stu-id="06b64-208">In order tooimprove hello model results Azure ML Recommendations enables tooset a user unique identification that will override hello cookie usage.</span></span>

<span data-ttu-id="06b64-209">Hello 使用者登入 tooyour 網站之後，就應該使用此事件。</span><span class="sxs-lookup"><span data-stu-id="06b64-209">This event should be used after hello user login tooyour site.</span></span>

<span data-ttu-id="06b64-210">參數：</span><span class="sxs-lookup"><span data-stu-id="06b64-210">Parameters:</span></span>

* <span data-ttu-id="06b64-211">event (字串) - “userlogin”</span><span class="sxs-lookup"><span data-stu-id="06b64-211">event (string) - “userlogin”</span></span>
* <span data-ttu-id="06b64-212">使用者 （字串）-hello 使用者的唯一識別碼。</span><span class="sxs-lookup"><span data-stu-id="06b64-212">user (string) - unique identification of hello user.</span></span>
  
        <script>
            if (typeof AzureMLRecommendationsEvent=="undefined") { AzureMLRecommendationsEvent = []; }
            AzureMLRecommendationsEvent.push({event: "userlogin", user: “ABCD10AA” });
        </script>

## <a name="4-consume-recommendations-via-javascript"></a><span data-ttu-id="06b64-213">4.透過 JavaScript 取用建議</span><span class="sxs-lookup"><span data-stu-id="06b64-213">4. Consume Recommendations via JavaScript</span></span>
<span data-ttu-id="06b64-214">利用 hello 建議的 hello 程式碼是由用戶端 hello 網頁觸發某些 JavaScript 事件。</span><span class="sxs-lookup"><span data-stu-id="06b64-214">hello code that consumes hello recommendation is triggered by some JavaScript event by hello client’s webpage.</span></span> <span data-ttu-id="06b64-215">hello 建議回應會包含 hello 的建議項目 Id、 其名稱和其分級。</span><span class="sxs-lookup"><span data-stu-id="06b64-215">hello recommendation response includes hello recommended items Ids, their names and their ratings.</span></span> <span data-ttu-id="06b64-216">這個選項，只讓清單顯示的建議項目-更複雜處理 （例如將 hello 項目中繼資料） 的 hello 應該在 hello 伺服器端整合的最佳 toouse 它。</span><span class="sxs-lookup"><span data-stu-id="06b64-216">It’s best toouse this option only for a list display of hello recommended items - more complex handling (such as adding hello item’s metadata) should be done on hello server side integration.</span></span>

### <a name="41-consume-recommendations"></a><span data-ttu-id="06b64-217">4.1 取用建議</span><span class="sxs-lookup"><span data-stu-id="06b64-217">4.1 Consume Recommendations</span></span>
<span data-ttu-id="06b64-218">您需要 tooinclude hello tooconsume 建議需要在頁面和 toocall AzureMLRecommendationsStart 中的 JavaScript 程式庫。</span><span class="sxs-lookup"><span data-stu-id="06b64-218">tooconsume recommendations you need tooinclude hello required JavaScript libraries in your page and toocall AzureMLRecommendationsStart.</span></span> <span data-ttu-id="06b64-219">請參閱第 2 節。</span><span class="sxs-lookup"><span data-stu-id="06b64-219">See section 2.</span></span>

<span data-ttu-id="06b64-220">一或多個項目的 tooconsume 建議需要的 toocall 呼叫的方法： AzureMLRecommendationsGetI2IRecommendation。</span><span class="sxs-lookup"><span data-stu-id="06b64-220">tooconsume recommendations for one or more items you need toocall a method called: AzureMLRecommendationsGetI2IRecommendation.</span></span>

<span data-ttu-id="06b64-221">參數：</span><span class="sxs-lookup"><span data-stu-id="06b64-221">Parameters:</span></span>

* <span data-ttu-id="06b64-222">一或多個項目 tooget 建議的項目 （陣列的字串-）。</span><span class="sxs-lookup"><span data-stu-id="06b64-222">items (array of strings) - One or more items tooget recommendations for.</span></span> <span data-ttu-id="06b64-223">如果您取用 Fbt 組建，則您在這裡只能設定一個項目。</span><span class="sxs-lookup"><span data-stu-id="06b64-223">If you consume an Fbt build then you can set here only one item.</span></span>
* <span data-ttu-id="06b64-224">numberOfResults (整數) - 所需結果的數目。</span><span class="sxs-lookup"><span data-stu-id="06b64-224">numberOfResults (int) - number of required results.</span></span>
* <span data-ttu-id="06b64-225">includeMetadata （布林值，選用）-如果設定 too'true' 表示該 hello 中繼資料必須先填入欄位 hello 結果中。</span><span class="sxs-lookup"><span data-stu-id="06b64-225">includeMetadata (boolean, optional) - if set too‘true’ indicates that hello metadata field must be populated in hello result.</span></span>
* <span data-ttu-id="06b64-226">處理函式-處理 hello 建議函式傳回。</span><span class="sxs-lookup"><span data-stu-id="06b64-226">Processing function - a function that will handle hello recommendations returned.</span></span> <span data-ttu-id="06b64-227">hello 資料是以陣列傳回：</span><span class="sxs-lookup"><span data-stu-id="06b64-227">hello data is returned as an array of:</span></span>
  * <span data-ttu-id="06b64-228">項目 - 項目唯一識別碼</span><span class="sxs-lookup"><span data-stu-id="06b64-228">Item - item unique id</span></span>
  * <span data-ttu-id="06b64-229">名稱 - 項目名稱 (如果存在於目錄中)</span><span class="sxs-lookup"><span data-stu-id="06b64-229">name - item name (if exist in catalog)</span></span>
  * <span data-ttu-id="06b64-230">評等 - 建議評等</span><span class="sxs-lookup"><span data-stu-id="06b64-230">rating - recommendation rating</span></span>
  * <span data-ttu-id="06b64-231">中繼資料的字串，代表 hello hello 項目中繼資料</span><span class="sxs-lookup"><span data-stu-id="06b64-231">metadata - a string that represents hello metadata of hello item</span></span>

<span data-ttu-id="06b64-232">範例： hello 下列程式碼要求 8 建議項目 」 64f6eb0d-947a-4c18-a16c-888da9e228ba 」 (並不指定 includeMetadata-它隱含地說，無中繼資料，就需要)，它必須接著 hello 結果串連成一個緩衝區。</span><span class="sxs-lookup"><span data-stu-id="06b64-232">Example: hello following code requests 8 recommendations for item "64f6eb0d-947a-4c18-a16c-888da9e228ba" (and by not specifying includeMetadata - it implicitly says that no metadata is required), it then concatenate hello results into a buffer.</span></span>

        <script>
             var reco = AzureMLRecommendationsGetI2IRecommendation(["64f6eb0d-947a-4c18-a16c-888da9e228ba"], 8, false, function (reco) {
                 var buff = "";
                 for (var ii = 0; ii < reco.length; ii++) {
                       buff += reco[ii].item + "," + reco[ii].name + "," + reco[ii].rating + "\n";
                 }
                 alert(buff);
            });
        </script>


[1]: ./media/machine-learning-recommendation-api-javascript-integration/Drawing1.png
[2]: ./media/machine-learning-recommendation-api-javascript-integration/Drawing2.png
[3]: ./media/machine-learning-recommendation-api-javascript-integration/Drawing3.png
