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
redirect_document_id: TRUE
ms.openlocfilehash: 8f27962d097bffc2a03de80244ae41d6573a4bf3
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="azure-machine-learning-recommendations---javascript-integration"></a><span data-ttu-id="7a3dc-103">Azure Machine Learning Recommendations - JavaScript 整合</span><span class="sxs-lookup"><span data-stu-id="7a3dc-103">Azure Machine Learning Recommendations - JavaScript Integration</span></span>
> [!NOTE]
> <span data-ttu-id="7a3dc-104">您應該開始使用 Recommendations API 的 Cognitive Service，而不是此版本。</span><span class="sxs-lookup"><span data-stu-id="7a3dc-104">You should start using the Recommendations API Cognitive Service instead of this version.</span></span> <span data-ttu-id="7a3dc-105">Recommendations 的 Cognitive Service 將會取代這個服務，而所有的新特徵都會在其中進行開發。</span><span class="sxs-lookup"><span data-stu-id="7a3dc-105">The Recommendations Cognitive Service will be replacing this service, and all the new features will be developed there.</span></span> <span data-ttu-id="7a3dc-106">它會提供新功能，例如，批次支援、更好的 API 總管、更簡潔的 API 介面、更一致的註冊/計費體驗等。</span><span class="sxs-lookup"><span data-stu-id="7a3dc-106">It has new capabilities like batching support, a better API Explorer, a cleaner API surface, more consistent signup/billing experience, etc.</span></span>
> <span data-ttu-id="7a3dc-107">深入了解 [移轉到新的 Cognitive Service](http://aka.ms/recomigrate)</span><span class="sxs-lookup"><span data-stu-id="7a3dc-107">Learn more about [Migrating to the new Cognitive Service](http://aka.ms/recomigrate)</span></span>
> 
> 

<span data-ttu-id="7a3dc-108">本文件說明如何使用 JavaScript 整合您的網站。</span><span class="sxs-lookup"><span data-stu-id="7a3dc-108">This document depict how to integrate your site using JavaScript.</span></span> <span data-ttu-id="7a3dc-109">JavaScript 可讓您傳送資料擷取事件，並在建立建議模型之後取用建議。</span><span class="sxs-lookup"><span data-stu-id="7a3dc-109">The JavaScript enables you to send Data Acquisition events and to consume recommendations once you build a recommendation model.</span></span> <span data-ttu-id="7a3dc-110">透過 JS 完成的所有操作也能從伺服器端完成。</span><span class="sxs-lookup"><span data-stu-id="7a3dc-110">All operations done via JS can be also done from server side.</span></span>

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

## <a name="1-general-overview"></a><span data-ttu-id="7a3dc-111">1.一般概觀</span><span class="sxs-lookup"><span data-stu-id="7a3dc-111">1. General Overview</span></span>
<span data-ttu-id="7a3dc-112">利用 2 階段所包含的 Azure ML Recommendations 來整合您的網站：</span><span class="sxs-lookup"><span data-stu-id="7a3dc-112">Integrating your site with Azure ML Recommendations consist on 2 Phases:</span></span>

1. <span data-ttu-id="7a3dc-113">將事件傳送到 Azure ML Recommendations。</span><span class="sxs-lookup"><span data-stu-id="7a3dc-113">Send Events into Azure ML Recommendations.</span></span> <span data-ttu-id="7a3dc-114">這樣做將能建立建議模型。</span><span class="sxs-lookup"><span data-stu-id="7a3dc-114">This will enable to build a recommendation model.</span></span>
2. <span data-ttu-id="7a3dc-115">取用建議。</span><span class="sxs-lookup"><span data-stu-id="7a3dc-115">Consume the recommendations.</span></span> <span data-ttu-id="7a3dc-116">建立模型之後，您就可以取用建議。</span><span class="sxs-lookup"><span data-stu-id="7a3dc-116">After the model is built you can consume the recommendations.</span></span> <span data-ttu-id="7a3dc-117">(本文件並未說明如何建立模型，請閱讀快速入門指南以取得做法的詳細資訊)。</span><span class="sxs-lookup"><span data-stu-id="7a3dc-117">(This document does not explain how to build a model, read the quick start guide to get more information on how).</span></span>

<span data-ttu-id="7a3dc-118"><ins>第一階段</ins></span><span class="sxs-lookup"><span data-stu-id="7a3dc-118"><ins>Phase I</ins></span></span>

<span data-ttu-id="7a3dc-119">在第一階段中，您會將一個小型 JavaScript 程式庫插入 HTML 網頁，讓該頁面可在事件於 HTML 網頁上發生時將其傳送到 Azure ML Recommendations 伺服器 (透過資料市場)：</span><span class="sxs-lookup"><span data-stu-id="7a3dc-119">In the first phase you insert into your html pages a small JavaScript library that enables the page to send events as they occur on the html page into Azure ML Recommendations servers (via Data Market):</span></span>

![繪圖 1][1]

<span data-ttu-id="7a3dc-121"><ins>第二階段</ins></span><span class="sxs-lookup"><span data-stu-id="7a3dc-121"><ins>Phase II</ins></span></span>

<span data-ttu-id="7a3dc-122">在第二階段中，當您想要在頁面上顯示建議時，請選取下列其中一個選項：</span><span class="sxs-lookup"><span data-stu-id="7a3dc-122">In the second phase when you want to show the recommendations on the page you select one of the following options:</span></span>

<span data-ttu-id="7a3dc-123">1. 您的伺服器 (在頁面轉譯階段) 呼叫 Azure ML Recommendations 伺服器 (透過資料市場) 以取得建議。</span><span class="sxs-lookup"><span data-stu-id="7a3dc-123">1.Your server (on the phase of page rendering) calls Azure ML Recommendations Server (via Data Market) to get recommendations.</span></span> <span data-ttu-id="7a3dc-124">結果會包含項目識別碼的清單。</span><span class="sxs-lookup"><span data-stu-id="7a3dc-124">The results include a list of items id.</span></span> <span data-ttu-id="7a3dc-125">您的伺服器需要利用「中繼資料」 (例如影像、描述) 項目擴充結果，以及將建立的頁面傳送給瀏覽器。</span><span class="sxs-lookup"><span data-stu-id="7a3dc-125">Your server needs to enrich the results with the items Meta data (e.g. images, description) and send the created page to the browser.</span></span>

![繪圖 2][2]

<span data-ttu-id="7a3dc-127">2. 另一個選擇是使用第一階段中的小型 JavaScript 檔案，以取得簡單的建議項目清單。</span><span class="sxs-lookup"><span data-stu-id="7a3dc-127">2.The other option is to use the small JavaScript file from phase one to get a simple list of recommended items.</span></span> <span data-ttu-id="7a3dc-128">這裡收到的資料會比第一個選擇還要精簡。</span><span class="sxs-lookup"><span data-stu-id="7a3dc-128">The data received here is leaner than the one in the first option.</span></span>

![繪圖 3][3]

## <a name="2-prerequisites"></a><span data-ttu-id="7a3dc-130">2.必要條件</span><span class="sxs-lookup"><span data-stu-id="7a3dc-130">2. Prerequisites</span></span>
1. <span data-ttu-id="7a3dc-131">使用 API 建立新的模型。</span><span class="sxs-lookup"><span data-stu-id="7a3dc-131">Create a new model using the APIs.</span></span> <span data-ttu-id="7a3dc-132">如需如何執行此操作，請參閱快速入門指南。</span><span class="sxs-lookup"><span data-stu-id="7a3dc-132">See the Quick start guide on how to do it.</span></span>
2. <span data-ttu-id="7a3dc-133">使用 base64 將 &lt;dataMarketUser&gt;:&lt;dataMarketKey&gt; 編碼。</span><span class="sxs-lookup"><span data-stu-id="7a3dc-133">Encode your &lt;dataMarketUser&gt;:&lt;dataMarketKey&gt; with base64.</span></span> <span data-ttu-id="7a3dc-134">(這將會用於基本驗證，讓 JS 程式碼能夠呼叫 API)。</span><span class="sxs-lookup"><span data-stu-id="7a3dc-134">(This will be used for the basic authentication to enable the JS code to call the APIs).</span></span>

## <a name="3-send-data-acquisition-events-using-javascript"></a><span data-ttu-id="7a3dc-135">3.使用 JavaScript 傳送資料擷取事件</span><span class="sxs-lookup"><span data-stu-id="7a3dc-135">3. Send Data Acquisition events using JavaScript</span></span>
<span data-ttu-id="7a3dc-136">下列步驟可加入傳送事件的速度：</span><span class="sxs-lookup"><span data-stu-id="7a3dc-136">The following steps facilitate sending events:</span></span>

1. <span data-ttu-id="7a3dc-137">在程式碼中納入 JQuery 程式庫。</span><span class="sxs-lookup"><span data-stu-id="7a3dc-137">Include JQuery library in your code.</span></span> <span data-ttu-id="7a3dc-138">您可以利用下列 URL 來從 nuget 下載。</span><span class="sxs-lookup"><span data-stu-id="7a3dc-138">You can download it from nuget in the following URL.</span></span>
   
     <span data-ttu-id="7a3dc-139">http://www.nuget.org/packages/jQuery/1.8.2</span><span class="sxs-lookup"><span data-stu-id="7a3dc-139">http://www.nuget.org/packages/jQuery/1.8.2</span></span>
2. <span data-ttu-id="7a3dc-140">從下列 URL 納入 Recommendations Java Script 程式庫：http://aka.ms/RecoJSLib1</span><span class="sxs-lookup"><span data-stu-id="7a3dc-140">Include the Recommendations Java Script library from the following URL: http://aka.ms/RecoJSLib1</span></span>
3. <span data-ttu-id="7a3dc-141">使用適當參數初始化 Azure ML Recommendations 程式庫。</span><span class="sxs-lookup"><span data-stu-id="7a3dc-141">Initialize Azure ML Recommendations library with the appropriate parameters.</span></span>
   
     <span data-ttu-id="7a3dc-142"><script> AzureMLRecommendationsStart("<base64encoding of username:key>", "<model_id>"); </script>
4. 傳送適當的事件。</span><span class="sxs-lookup"><span data-stu-id="7a3dc-142"><script> AzureMLRecommendationsStart("<base64encoding of username:key>", "<model_id>"); </script>
4. Send the appropriate event.</span></span> <span data-ttu-id="7a3dc-143">有關所有型別事件的詳細說明 (Click 事件範例)，請參閱下節  <script> 如果 (typeof AzureMLRecommendationsEvent=="undefined") {</span><span class="sxs-lookup"><span data-stu-id="7a3dc-143">See detailed section below on all type of events (example of click event)  <script> if (typeof AzureMLRecommendationsEvent=="undefined") {</span></span>         
                     <span data-ttu-id="7a3dc-144">AzureMLRecommendationsEvent = []; } AzureMLRecommendationsEvent.push({ event: "click", item: "18321116" }); </script></span><span class="sxs-lookup"><span data-stu-id="7a3dc-144">AzureMLRecommendationsEvent = []; } AzureMLRecommendationsEvent.push({ event: "click", item: "18321116" }); </script></span></span>

### <a name="31----limitations-and-browser-support"></a><span data-ttu-id="7a3dc-145">3.1.</span><span class="sxs-lookup"><span data-stu-id="7a3dc-145">3.1.</span></span>    <span data-ttu-id="7a3dc-146">限制和瀏覽器支援</span><span class="sxs-lookup"><span data-stu-id="7a3dc-146">Limitations and Browser Support</span></span>
<span data-ttu-id="7a3dc-147">這是參考實作並依現況提供。</span><span class="sxs-lookup"><span data-stu-id="7a3dc-147">This is a reference implementation and it is given as is.</span></span> <span data-ttu-id="7a3dc-148">其應該支援所有主要瀏覽器。</span><span class="sxs-lookup"><span data-stu-id="7a3dc-148">It should support all major browsers.</span></span>

### <a name="32----type-of-events"></a><span data-ttu-id="7a3dc-149">3.2.</span><span class="sxs-lookup"><span data-stu-id="7a3dc-149">3.2.</span></span>    <span data-ttu-id="7a3dc-150">事件類型</span><span class="sxs-lookup"><span data-stu-id="7a3dc-150">Type of Events</span></span>
<span data-ttu-id="7a3dc-151">程式庫一共支援 5 種類型的事件：點選 (Click)、建議點選 (Recommendation Click)、加入購物車 (Add to Shop Cart)、從購物車移除 (Remove from Shop Cart) 以及購買 (Purchase)。</span><span class="sxs-lookup"><span data-stu-id="7a3dc-151">There are 5 types of event that the library supports: Click, Recommendation Click, Add to Shop Cart, Remove from Shop Cart and Purchase.</span></span> <span data-ttu-id="7a3dc-152">另外還有一種用來設定使用者內容的事件，稱為登入 (Login)。</span><span class="sxs-lookup"><span data-stu-id="7a3dc-152">There is an additional event that is used to set the user context called Login.</span></span>

#### <a name="321-click-event"></a><span data-ttu-id="7a3dc-153">3.2.1.</span><span class="sxs-lookup"><span data-stu-id="7a3dc-153">3.2.1.</span></span> <span data-ttu-id="7a3dc-154">點選事件</span><span class="sxs-lookup"><span data-stu-id="7a3dc-154">Click Event</span></span>
<span data-ttu-id="7a3dc-155">每當使用者點選項目時，都應該會使用這個事件。</span><span class="sxs-lookup"><span data-stu-id="7a3dc-155">This event should be used any time a user clicked on an item.</span></span> <span data-ttu-id="7a3dc-156">當使用者點選項目時，通常會開啟含有該項目詳細資料的新頁面。在這個頁面中，應該會觸發此事件。</span><span class="sxs-lookup"><span data-stu-id="7a3dc-156">Usually when user clicks on an item a new page is opened with the item details; in this page this event should be triggered.</span></span>

<span data-ttu-id="7a3dc-157">參數：</span><span class="sxs-lookup"><span data-stu-id="7a3dc-157">Parameters:</span></span>

* <span data-ttu-id="7a3dc-158">event (字串, 強制) - “click”</span><span class="sxs-lookup"><span data-stu-id="7a3dc-158">event (string, mandatory) - “click”</span></span>
* <span data-ttu-id="7a3dc-159">item (字串, 強制) - 項目的唯一識別碼</span><span class="sxs-lookup"><span data-stu-id="7a3dc-159">item (string, mandatory) - Unique identifier of the item</span></span>
* <span data-ttu-id="7a3dc-160">itemName (字串, 選擇性) - 項目的名稱</span><span class="sxs-lookup"><span data-stu-id="7a3dc-160">itemName (string, optional) - the name of the item</span></span>
* <span data-ttu-id="7a3dc-161">itemDescription (字串, 選擇性) - 項目的描述</span><span class="sxs-lookup"><span data-stu-id="7a3dc-161">itemDescription (string, optional) - the description of the item</span></span>
* <span data-ttu-id="7a3dc-162">itemCategory (字串, 選擇性) - 項目的類別</span><span class="sxs-lookup"><span data-stu-id="7a3dc-162">itemCategory (string, optional) - the category of the item</span></span>
  
        <script>
            if (typeof AzureMLRecommendationsEvent == "undefined") { AzureMLRecommendationsEvent = []; }
            AzureMLRecommendationsEvent.push({ event: "click", item: "3111718" });
        </script>

<span data-ttu-id="7a3dc-163">或使用選擇性資料：</span><span class="sxs-lookup"><span data-stu-id="7a3dc-163">Or with optional data:</span></span>

        <script>
            if (typeof AzureMLRecommendationsEvent === "undefined") { AzureMLRecommendationsEvent = []; }
            AzureMLRecommendationsEvent.push({event: "click", item: "3111718", itemName: "Plane", itemDescription: "It is a big plane", itemCategory: "Aviation"});
        </script>


#### <a name="322-recommendation-click-event"></a><span data-ttu-id="7a3dc-164">3.2.2.</span><span class="sxs-lookup"><span data-stu-id="7a3dc-164">3.2.2.</span></span> <span data-ttu-id="7a3dc-165">建議點選事件</span><span class="sxs-lookup"><span data-stu-id="7a3dc-165">Recommendation Click Event</span></span>
<span data-ttu-id="7a3dc-166">每當使用者點選項目 (從 Azure ML Recommendations 接收當成建議的項目) 時，都應該會使用這個事件。</span><span class="sxs-lookup"><span data-stu-id="7a3dc-166">This event should be used any time a user clicked on an item that was received from Azure ML Recommendations as a recommended item.</span></span> <span data-ttu-id="7a3dc-167">當使用者點選項目時，通常會開啟含有該項目詳細資料的新頁面。在這個頁面中，應該會觸發此事件。</span><span class="sxs-lookup"><span data-stu-id="7a3dc-167">Usually when user clicks on an item a new page is opened with the item details; in this page this event should be triggered.</span></span>

<span data-ttu-id="7a3dc-168">參數：</span><span class="sxs-lookup"><span data-stu-id="7a3dc-168">Parameters:</span></span>

* <span data-ttu-id="7a3dc-169">event (字串, 強制) - “recommendationclick”</span><span class="sxs-lookup"><span data-stu-id="7a3dc-169">event (string, mandatory) - “recommendationclick”</span></span>
* <span data-ttu-id="7a3dc-170">item (字串, 強制) - 項目的唯一識別碼</span><span class="sxs-lookup"><span data-stu-id="7a3dc-170">item (string, mandatory) - Unique identifier of the item</span></span>
* <span data-ttu-id="7a3dc-171">itemName (字串, 選擇性) - 項目的名稱</span><span class="sxs-lookup"><span data-stu-id="7a3dc-171">itemName (string, optional) - the name of the item</span></span>
* <span data-ttu-id="7a3dc-172">itemDescription (字串, 選擇性) - 項目的描述</span><span class="sxs-lookup"><span data-stu-id="7a3dc-172">itemDescription (string, optional) - the description of the item</span></span>
* <span data-ttu-id="7a3dc-173">itemCategory (字串, 選擇性) - 項目的類別</span><span class="sxs-lookup"><span data-stu-id="7a3dc-173">itemCategory (string, optional) - the category of the item</span></span>
* <span data-ttu-id="7a3dc-174">seeds (字串陣列, 選擇性) - 產生建議查詢的種子。</span><span class="sxs-lookup"><span data-stu-id="7a3dc-174">seeds (string array, optional) - the seeds that generated the recommendation query.</span></span>
* <span data-ttu-id="7a3dc-175">recoList (字串陣列, 選擇性) - 產生被按一下之項目的建議要求的結果。</span><span class="sxs-lookup"><span data-stu-id="7a3dc-175">recoList (string array, optional) - the result of the recommendation request that generated the item that was clicked.</span></span>
  
        <script>
            if (typeof AzureMLRecommendationsEvent=="undefined") { AzureMLRecommendationsEvent = []; }
            AzureMLRecommendationsEvent.push({event: "recommendationclick", item: "18899918" });
        </script>

<span data-ttu-id="7a3dc-176">或使用選擇性資料：</span><span class="sxs-lookup"><span data-stu-id="7a3dc-176">Or with optional data:</span></span>

        <script>
            if (typeof AzureMLRecommendationsEvent == "undefined") { AzureMLRecommendationsEvent = []; }
            AzureMLRecommendationsEvent.push({ event: eventName, item: "198", itemName: "Plane2", itemDescription: "It is a big plane2", itemCategory: "Default2", seeds: ["Seed1", "Seed2"], recoList: ["199", "198", "197"]                 });
        </script>


#### <a name="323-add-shopping-cart-event"></a><span data-ttu-id="7a3dc-177">3.2.3.</span><span class="sxs-lookup"><span data-stu-id="7a3dc-177">3.2.3.</span></span> <span data-ttu-id="7a3dc-178">加入購物車事件</span><span class="sxs-lookup"><span data-stu-id="7a3dc-178">Add Shopping Cart Event</span></span>
<span data-ttu-id="7a3dc-179">當使用者將項目加入購物車時，應該會使用這個事件。</span><span class="sxs-lookup"><span data-stu-id="7a3dc-179">This event should be used when the user add an item to the shopping cart.</span></span>
<span data-ttu-id="7a3dc-180">參數：</span><span class="sxs-lookup"><span data-stu-id="7a3dc-180">Parameters:</span></span>

* <span data-ttu-id="7a3dc-181">event (字串, 強制) - “addshopcart”</span><span class="sxs-lookup"><span data-stu-id="7a3dc-181">event (string, mandatory) - “addshopcart”</span></span>
* <span data-ttu-id="7a3dc-182">item (字串, 強制) - 項目的唯一識別碼</span><span class="sxs-lookup"><span data-stu-id="7a3dc-182">item (string, mandatory) - Unique identifier of the item</span></span>
* <span data-ttu-id="7a3dc-183">itemName (字串, 選擇性) - 項目的名稱</span><span class="sxs-lookup"><span data-stu-id="7a3dc-183">itemName (string, optional) - the name of the item</span></span>
* <span data-ttu-id="7a3dc-184">itemDescription (字串, 選擇性) - 項目的描述</span><span class="sxs-lookup"><span data-stu-id="7a3dc-184">itemDescription (string, optional) - the description of the item</span></span>
* <span data-ttu-id="7a3dc-185">itemCategory (字串, 選擇性) - 項目的類別</span><span class="sxs-lookup"><span data-stu-id="7a3dc-185">itemCategory (string, optional) - the category of the item</span></span>
  
        <script>
            if (typeof AzureMLRecommendationsEvent == "undefined") { AzureMLRecommendationsEvent = []; }
            AzureMLRecommendationsEvent.push({event: "addshopcart", item: "13221118" });
        </script>

#### <a name="324-remove-shopping-cart-event"></a><span data-ttu-id="7a3dc-186">3.2.4.</span><span class="sxs-lookup"><span data-stu-id="7a3dc-186">3.2.4.</span></span> <span data-ttu-id="7a3dc-187">移除購物車事件</span><span class="sxs-lookup"><span data-stu-id="7a3dc-187">Remove Shopping Cart Event</span></span>
<span data-ttu-id="7a3dc-188">當使用者移除購物車中的項目時，應該會使用這個事件。</span><span class="sxs-lookup"><span data-stu-id="7a3dc-188">This event should be used when the user removes an item to the shopping cart.</span></span>

<span data-ttu-id="7a3dc-189">參數：</span><span class="sxs-lookup"><span data-stu-id="7a3dc-189">Parameters:</span></span>

* <span data-ttu-id="7a3dc-190">event (字串, 強制) - “removeshopcart”</span><span class="sxs-lookup"><span data-stu-id="7a3dc-190">event (string, mandatory) - “removeshopcart”</span></span>
* <span data-ttu-id="7a3dc-191">item (字串, 強制) - 項目的唯一識別碼</span><span class="sxs-lookup"><span data-stu-id="7a3dc-191">item (string, mandatory) - Unique identifier of the item</span></span>
* <span data-ttu-id="7a3dc-192">itemName (字串, 選擇性) - 項目的名稱</span><span class="sxs-lookup"><span data-stu-id="7a3dc-192">itemName (string, optional) - the name of the item</span></span>
* <span data-ttu-id="7a3dc-193">itemDescription (字串, 選擇性) - 項目的描述</span><span class="sxs-lookup"><span data-stu-id="7a3dc-193">itemDescription (string, optional) - the description of the item</span></span>
* <span data-ttu-id="7a3dc-194">itemCategory (字串, 選擇性) - 項目的類別</span><span class="sxs-lookup"><span data-stu-id="7a3dc-194">itemCategory (string, optional) - the category of the item</span></span>
  
        <script>
            if (typeof AzureMLRecommendationsEvent=="undefined") { AzureMLRecommendationsEvent = []; }
            AzureMLRecommendationsEvent.push({ event: "removeshopcart", item: "111118" });
        </script>

#### <a name="325-purchase-event"></a><span data-ttu-id="7a3dc-195">3.2.5.</span><span class="sxs-lookup"><span data-stu-id="7a3dc-195">3.2.5.</span></span> <span data-ttu-id="7a3dc-196">購買事件</span><span class="sxs-lookup"><span data-stu-id="7a3dc-196">Purchase Event</span></span>
<span data-ttu-id="7a3dc-197">當使用者購買購物車中的項目時，應該會使用這個事件。</span><span class="sxs-lookup"><span data-stu-id="7a3dc-197">This event should be used when the user purchased his shopping cart.</span></span>

<span data-ttu-id="7a3dc-198">參數：</span><span class="sxs-lookup"><span data-stu-id="7a3dc-198">Parameters:</span></span>

* <span data-ttu-id="7a3dc-199">event (字串) - “purchase”</span><span class="sxs-lookup"><span data-stu-id="7a3dc-199">event (string) - “purchase”</span></span>
* <span data-ttu-id="7a3dc-200">items (Purchased[]) - 陣列會為購買的每個項目保留一個項目。</span><span class="sxs-lookup"><span data-stu-id="7a3dc-200">items ( Purchased[] ) - Array holding an entry for each item purchased.</span></span><br><br>
  <span data-ttu-id="7a3dc-201">已購買項目的格式︰</span><span class="sxs-lookup"><span data-stu-id="7a3dc-201">Purchased format:</span></span>
  * <span data-ttu-id="7a3dc-202">item (字串) – 項目的唯一識別碼。</span><span class="sxs-lookup"><span data-stu-id="7a3dc-202">item (string) - Unique identifier of the item.</span></span>
  * <span data-ttu-id="7a3dc-203">count (整數或字串) - 已購買的項目數。</span><span class="sxs-lookup"><span data-stu-id="7a3dc-203">count (int or string) - number of items that were purchased.</span></span>
  * <span data-ttu-id="7a3dc-204">price (浮點數或字串) - 選擇性欄位 - 項目的價格。</span><span class="sxs-lookup"><span data-stu-id="7a3dc-204">price (float or string) - optional field - the price of the item.</span></span>

<span data-ttu-id="7a3dc-205">以下範例顯示總共購買 3 個項目 (33, 34, 35)，已填入其中兩個的所有欄位 (item, count, price)，還有一個 (item 34) 沒有價格。</span><span class="sxs-lookup"><span data-stu-id="7a3dc-205">The example below shows purchase of 3 items (33, 34, 35), two with all fields populated (item, count, price) and one (item 34) without a price.</span></span>

        <script>
            if ( typeof AzureMLRecommendationsEvent == "undefined"){ AzureMLRecommendationsEvent = []; }
            AzureMLRecommendationsEvent.push({ event: "purchase", items: [{ item: "33", count: "1", price: "10" }, { item: "34", count: "2" }, { item: "35", count: "1", price: "210" }] });
        </script>

#### <a name="326-user-login-event"></a><span data-ttu-id="7a3dc-206">3.2.6.</span><span class="sxs-lookup"><span data-stu-id="7a3dc-206">3.2.6.</span></span> <span data-ttu-id="7a3dc-207">使用者登入事件</span><span class="sxs-lookup"><span data-stu-id="7a3dc-207">User Login Event</span></span>
<span data-ttu-id="7a3dc-208">Azure ML Recommendations 事件程式庫會建立並使用 Cookie，以識別來自相同瀏覽器的事件。</span><span class="sxs-lookup"><span data-stu-id="7a3dc-208">Azure ML Recommendations Event library creates and use a cookie in order to identify events that came from the same browser.</span></span> <span data-ttu-id="7a3dc-209">為了改善模型結果，Azure ML Recommendations 能夠為使用者設定將覆寫 Cookie 使用的唯一識別。</span><span class="sxs-lookup"><span data-stu-id="7a3dc-209">In order to improve the model results Azure ML Recommendations enables to set a user unique identification that will override the cookie usage.</span></span>

<span data-ttu-id="7a3dc-210">在使用者登入您的網站後，應該會使用這個事件。</span><span class="sxs-lookup"><span data-stu-id="7a3dc-210">This event should be used after the user login to your site.</span></span>

<span data-ttu-id="7a3dc-211">參數：</span><span class="sxs-lookup"><span data-stu-id="7a3dc-211">Parameters:</span></span>

* <span data-ttu-id="7a3dc-212">event (字串) - “userlogin”</span><span class="sxs-lookup"><span data-stu-id="7a3dc-212">event (string) - “userlogin”</span></span>
* <span data-ttu-id="7a3dc-213">user (字串) - 使用者的唯一識別。</span><span class="sxs-lookup"><span data-stu-id="7a3dc-213">user (string) - unique identification of the user.</span></span>
  
        <script>
            if (typeof AzureMLRecommendationsEvent=="undefined") { AzureMLRecommendationsEvent = []; }
            AzureMLRecommendationsEvent.push({event: "userlogin", user: “ABCD10AA” });
        </script>

## <a name="4-consume-recommendations-via-javascript"></a><span data-ttu-id="7a3dc-214">4.透過 JavaScript 取用建議</span><span class="sxs-lookup"><span data-stu-id="7a3dc-214">4. Consume Recommendations via JavaScript</span></span>
<span data-ttu-id="7a3dc-215">取用建議的程式碼是由用戶端網頁的某些 JavaScript 事件所觸發。</span><span class="sxs-lookup"><span data-stu-id="7a3dc-215">The code that consumes the recommendation is triggered by some JavaScript event by the client’s webpage.</span></span> <span data-ttu-id="7a3dc-216">建議回應包含建議項目識別碼、其名稱及評等。</span><span class="sxs-lookup"><span data-stu-id="7a3dc-216">The recommendation response includes the recommended items Ids, their names and their ratings.</span></span> <span data-ttu-id="7a3dc-217">最好只有在以清單顯示建議的項目時，才使用這個選項 - 較複雜的處理 (例如，新增項目的中繼資料) 應該在伺服器端整合完成。</span><span class="sxs-lookup"><span data-stu-id="7a3dc-217">It’s best to use this option only for a list display of the recommended items - more complex handling (such as adding the item’s metadata) should be done on the server side integration.</span></span>

### <a name="41-consume-recommendations"></a><span data-ttu-id="7a3dc-218">4.1 取用建議</span><span class="sxs-lookup"><span data-stu-id="7a3dc-218">4.1 Consume Recommendations</span></span>
<span data-ttu-id="7a3dc-219">若要取用建議，您必須將必要的 JavaScript 程式碼納入頁面中，然後呼叫 AzureMLRecommendationsStart。</span><span class="sxs-lookup"><span data-stu-id="7a3dc-219">To consume recommendations you need to include the required JavaScript libraries in your page and to call AzureMLRecommendationsStart.</span></span> <span data-ttu-id="7a3dc-220">請參閱第 2 節。</span><span class="sxs-lookup"><span data-stu-id="7a3dc-220">See section 2.</span></span>

<span data-ttu-id="7a3dc-221">若要取用一或多個項目的建議，您必須呼叫以下方法： AzureMLRecommendationsGetI2IRecommendation。</span><span class="sxs-lookup"><span data-stu-id="7a3dc-221">To consume recommendations for one or more items you need to call a method called: AzureMLRecommendationsGetI2IRecommendation.</span></span>

<span data-ttu-id="7a3dc-222">參數：</span><span class="sxs-lookup"><span data-stu-id="7a3dc-222">Parameters:</span></span>

* <span data-ttu-id="7a3dc-223">items (字串的陣列) - 要取得建議的一或多個項目。</span><span class="sxs-lookup"><span data-stu-id="7a3dc-223">items (array of strings) - One or more items to get recommendations for.</span></span> <span data-ttu-id="7a3dc-224">如果您取用 Fbt 組建，則您在這裡只能設定一個項目。</span><span class="sxs-lookup"><span data-stu-id="7a3dc-224">If you consume an Fbt build then you can set here only one item.</span></span>
* <span data-ttu-id="7a3dc-225">numberOfResults (整數) - 所需結果的數目。</span><span class="sxs-lookup"><span data-stu-id="7a3dc-225">numberOfResults (int) - number of required results.</span></span>
* <span data-ttu-id="7a3dc-226">includeMetadata (布林值, 選擇性) - 如果設為 'true' 表示必須在結果中填入中繼資料欄位。</span><span class="sxs-lookup"><span data-stu-id="7a3dc-226">includeMetadata (boolean, optional) - if set to ‘true’ indicates that the metadata field must be populated in the result.</span></span>
* <span data-ttu-id="7a3dc-227">處理函式 - 將處理所傳回建議的函式。</span><span class="sxs-lookup"><span data-stu-id="7a3dc-227">Processing function - a function that will handle the recommendations returned.</span></span> <span data-ttu-id="7a3dc-228">資料會以下列陣列的方式傳回︰</span><span class="sxs-lookup"><span data-stu-id="7a3dc-228">The data is returned as an array of:</span></span>
  * <span data-ttu-id="7a3dc-229">項目 - 項目唯一識別碼</span><span class="sxs-lookup"><span data-stu-id="7a3dc-229">Item - item unique id</span></span>
  * <span data-ttu-id="7a3dc-230">名稱 - 項目名稱 (如果存在於目錄中)</span><span class="sxs-lookup"><span data-stu-id="7a3dc-230">name - item name (if exist in catalog)</span></span>
  * <span data-ttu-id="7a3dc-231">評等 - 建議評等</span><span class="sxs-lookup"><span data-stu-id="7a3dc-231">rating - recommendation rating</span></span>
  * <span data-ttu-id="7a3dc-232">中繼資料 - 代表項目中繼資料的字串</span><span class="sxs-lookup"><span data-stu-id="7a3dc-232">metadata - a string that represents the metadata of the item</span></span>

<span data-ttu-id="7a3dc-233">範例：下列程式碼要求項目 "64f6eb0d-947a-4c18-a16c-888da9e228ba" (而不指定 includeMetadata - 即暗示不需要任何中繼資料) 提供 8 個建議，然後將結果串連到緩衝區。</span><span class="sxs-lookup"><span data-stu-id="7a3dc-233">Example: The following code requests 8 recommendations for item "64f6eb0d-947a-4c18-a16c-888da9e228ba" (and by not specifying includeMetadata - it implicitly says that no metadata is required), it then concatenate the results into a buffer.</span></span>

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
