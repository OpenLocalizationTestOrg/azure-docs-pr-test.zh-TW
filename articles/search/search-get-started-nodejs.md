---
title: "aaaGet 入門 node.js 的 Azure 搜尋 |Microsoft 文件"
description: "逐步了解如何使用 Node.js 作為程式設計語言，在 Azure 的雲端託管搜尋服務上建置搜尋應用程式。"
services: search
documentationcenter: 
author: EvanBoyle
manager: pablocas
editor: v-lincan
ms.assetid: 0625dc1b-9db6-40d5-ba9a-4738b75cbe19
ms.service: search
ms.devlang: na
ms.workload: search
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.date: 04/26/2017
ms.author: evboyle
ms.openlocfilehash: e9c7d756c2ea191ee2a285485c90439b96aa73b2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-search-in-nodejs"></a><span data-ttu-id="7a00a-103">開始在 Node.js 中使用 Azure 搜尋服務</span><span class="sxs-lookup"><span data-stu-id="7a00a-103">Get started with Azure Search in Node.js</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="7a00a-104">入口網站</span><span class="sxs-lookup"><span data-stu-id="7a00a-104">Portal</span></span>](search-get-started-portal.md)
> * [<span data-ttu-id="7a00a-105">.NET</span><span class="sxs-lookup"><span data-stu-id="7a00a-105">.NET</span></span>](search-howto-dotnet-sdk.md)
> 
> 

<span data-ttu-id="7a00a-106">了解如何自訂 Node.js toobuild 搜尋應用程式，使用 Azure 搜尋的搜尋經驗。</span><span class="sxs-lookup"><span data-stu-id="7a00a-106">Learn how toobuild a custom Node.js search application that uses Azure Search for its search experience.</span></span> <span data-ttu-id="7a00a-107">本教學課程使用 hello [Azure 搜尋服務 REST API](https://msdn.microsoft.com/library/dn798935.aspx) tooconstruct hello 物件和作業在此練習中使用。</span><span class="sxs-lookup"><span data-stu-id="7a00a-107">This tutorial uses hello [Azure Search Service REST API](https://msdn.microsoft.com/library/dn798935.aspx) tooconstruct hello objects and operations used in this exercise.</span></span>

<span data-ttu-id="7a00a-108">我們使用[Node.js](https://Nodejs.org)及 NPM，[適文字 3](http://www.sublimetext.com/3)，和 Windows 8.1 toodevelop 上的 Windows PowerShell 並測試這段程式碼。</span><span class="sxs-lookup"><span data-stu-id="7a00a-108">We used [Node.js](https://Nodejs.org) and NPM, [Sublime Text 3](http://www.sublimetext.com/3), and Windows PowerShell on Windows 8.1 toodevelop and test this code.</span></span>

<span data-ttu-id="7a00a-109">toorun 此範例中，您必須擁有 Azure 搜尋服務，您可以申請中 hello [Azure 入口網站](https://portal.azure.com)。</span><span class="sxs-lookup"><span data-stu-id="7a00a-109">toorun this sample, you must have an Azure Search service, which you can sign up for in hello [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="7a00a-110">請參閱[hello 入口網站中建立 Azure 搜尋服務](search-create-service-portal.md)如需逐步指示。</span><span class="sxs-lookup"><span data-stu-id="7a00a-110">See [Create an Azure Search service in hello portal](search-create-service-portal.md) for step-by-step instructions.</span></span>

## <a name="about-hello-data"></a><span data-ttu-id="7a00a-111">關於 hello 資料</span><span class="sxs-lookup"><span data-stu-id="7a00a-111">About hello data</span></span>
<span data-ttu-id="7a00a-112">此範例應用程式會使用資料 hello[美國地理服務 (USG)](http://geonames.usgs.gov/domestic/download_data.htm)、 篩選上 hello 羅德島狀態 tooreduce hello 資料集的大小。</span><span class="sxs-lookup"><span data-stu-id="7a00a-112">This sample application uses data from hello [United States Geological Services (USGS)](http://geonames.usgs.gov/domestic/download_data.htm), filtered on hello state of Rhode Island tooreduce hello dataset size.</span></span> <span data-ttu-id="7a00a-113">我們將使用此資料 toobuild 傳回例如醫院和學校，以及地理功能，例如資料流、 湖泊、 和 summits 地標建築物的搜尋應用程式。</span><span class="sxs-lookup"><span data-stu-id="7a00a-113">We'll use this data toobuild a search application that returns landmark buildings such as hospitals and schools, as well as geological features like streams, lakes, and summits.</span></span>

<span data-ttu-id="7a00a-114">在此應用程式，hello **DataIndexer**建置程式，並載入 hello 索引使用[索引子](https://msdn.microsoft.com/library/azure/dn798918.aspx)建構，擷取 hello 篩選 USG 從公開的 Azure SQL Database 的資料集。</span><span class="sxs-lookup"><span data-stu-id="7a00a-114">In this application, hello **DataIndexer** program builds and loads hello index using an [Indexer](https://msdn.microsoft.com/library/azure/dn798918.aspx) construct, retrieving hello filtered USGS dataset from a public Azure SQL Database.</span></span> <span data-ttu-id="7a00a-115">認證和連接資訊 toohello 線上資料來源提供 hello 程式碼中。</span><span class="sxs-lookup"><span data-stu-id="7a00a-115">Credentials and connection information toohello online data source is provided in hello program code.</span></span> <span data-ttu-id="7a00a-116">不需要進一步設定。</span><span class="sxs-lookup"><span data-stu-id="7a00a-116">No further configuration is necessary.</span></span>

> [!NOTE]
> <span data-ttu-id="7a00a-117">我們在 hello 免費定價層的 hello 10000 文件限制此資料集 toostay 套用篩選。</span><span class="sxs-lookup"><span data-stu-id="7a00a-117">We applied a filter on this dataset toostay under hello 10,000 document limit of hello free pricing tier.</span></span> <span data-ttu-id="7a00a-118">如果您使用 hello 標準層，這項限制不適用。</span><span class="sxs-lookup"><span data-stu-id="7a00a-118">If you use hello standard tier, this limit does not apply.</span></span> <span data-ttu-id="7a00a-119">如需各個定價層的容量詳細資料，請參閱 [搜尋服務限制](search-limits-quotas-capacity.md)。</span><span class="sxs-lookup"><span data-stu-id="7a00a-119">For details about capacity for each pricing tier, see [Search service limits](search-limits-quotas-capacity.md).</span></span>
> 
> 

<a id="sub-2"></a>

## <a name="find-hello-service-name-and-api-key-of-your-azure-search-service"></a><span data-ttu-id="7a00a-120">尋找 hello 服務名稱和您的 Azure 搜尋服務的 api 金鑰</span><span class="sxs-lookup"><span data-stu-id="7a00a-120">Find hello service name and api-key of your Azure Search service</span></span>
<span data-ttu-id="7a00a-121">建立 hello 服務之後，傳回 toohello 入口 tooget hello URL 或`api-key`。</span><span class="sxs-lookup"><span data-stu-id="7a00a-121">After you create hello service, return toohello portal tooget hello URL or `api-key`.</span></span> <span data-ttu-id="7a00a-122">連線 tooyour 搜尋服務需要您有兩個 hello 的 URL 和`api-key`tooauthenticate hello 呼叫。</span><span class="sxs-lookup"><span data-stu-id="7a00a-122">Connections tooyour Search service require that you have both hello URL and an `api-key` tooauthenticate hello call.</span></span>

1. <span data-ttu-id="7a00a-123">登入 toohello [Azure 入口網站](https://portal.azure.com)。</span><span class="sxs-lookup"><span data-stu-id="7a00a-123">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="7a00a-124">Hello 跳躍列中，按一下**搜尋服務**toolist 所有 Azure 搜尋服務佈都建您的訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="7a00a-124">In hello jump bar, click **Search service** toolist all Azure Search services provisioned for your subscription.</span></span>
3. <span data-ttu-id="7a00a-125">選取您想要 toouse hello 服務。</span><span class="sxs-lookup"><span data-stu-id="7a00a-125">Select hello service you want toouse.</span></span>
4. <span data-ttu-id="7a00a-126">Hello 服務儀表板，您應該會看到磚，以便於重要資訊，例如 hello 索引鍵圖示來存取 hello 系統管理金鑰。</span><span class="sxs-lookup"><span data-stu-id="7a00a-126">On hello service dashboard, you should see tiles for essential information, such as hello key icon for accessing hello admin keys.</span></span>
5. <span data-ttu-id="7a00a-127">將複製 hello 服務 URL、 管理金鑰和查詢索引鍵。</span><span class="sxs-lookup"><span data-stu-id="7a00a-127">Copy hello service URL, an admin key, and a query key.</span></span> <span data-ttu-id="7a00a-128">您所有的三個稍後需要時新增 toohello config.js 檔案。</span><span class="sxs-lookup"><span data-stu-id="7a00a-128">You need all three later when you add them toohello config.js file.</span></span>

## <a name="download-hello-sample-files"></a><span data-ttu-id="7a00a-129">下載檔案的 hello 範例</span><span class="sxs-lookup"><span data-stu-id="7a00a-129">Download hello sample files</span></span>
<span data-ttu-id="7a00a-130">使用下列方法 toodownload hello 範例 hello 的其中一個。</span><span class="sxs-lookup"><span data-stu-id="7a00a-130">Use either one of hello following approaches toodownload hello sample.</span></span>

1. <span data-ttu-id="7a00a-131">跳過[AzureSearchNodeJSIndexerDemo](https://github.com/AzureSearch/AzureSearchNodejsIndexerDemo)。</span><span class="sxs-lookup"><span data-stu-id="7a00a-131">Go too[AzureSearchNodeJSIndexerDemo](https://github.com/AzureSearch/AzureSearchNodejsIndexerDemo).</span></span>
2. <span data-ttu-id="7a00a-132">按一下**Download ZIP**，儲存 hello.zip 檔案，然後將它包含的所有 hello 檔案都解壓縮。</span><span class="sxs-lookup"><span data-stu-id="7a00a-132">Click **Download ZIP**, save hello .zip file, and then extract all hello files it contains.</span></span>

<span data-ttu-id="7a00a-133">所有後續的檔案修改及執行陳述式都會用到此資料夾中的檔案。</span><span class="sxs-lookup"><span data-stu-id="7a00a-133">All subsequent file modifications and run statements are made against files in this folder.</span></span>

## <a name="update-hello-configjs-with-your-search-service-url-and-api-key"></a><span data-ttu-id="7a00a-134">更新 hello config.js。</span><span class="sxs-lookup"><span data-stu-id="7a00a-134">Update hello config.js.</span></span> <span data-ttu-id="7a00a-135">方法為使用您的搜尋服務 URL 及 API 金鑰</span><span class="sxs-lookup"><span data-stu-id="7a00a-135">with your Search service URL and api-key</span></span>
<span data-ttu-id="7a00a-136">使用 hello URL 和更早版本，您所複製的 api 金鑰指定組態檔中的 hello URL、 管理金鑰，並查詢索引鍵。</span><span class="sxs-lookup"><span data-stu-id="7a00a-136">Using hello URL and api-key that you copied earlier, specify hello URL, admin-key, and query-key in configuration file.</span></span>

<span data-ttu-id="7a00a-137">系統管理金鑰可將服務作業的完整控制權限授與給您，包括建立或刪除索引，以及載入文件。</span><span class="sxs-lookup"><span data-stu-id="7a00a-137">Admin keys grant full control over service operations, including creating or deleting an index and loading documents.</span></span> <span data-ttu-id="7a00a-138">相較之下，查詢索引鍵是唯讀作業，通常是供連接 tooAzure 搜尋的用戶端應用程式。</span><span class="sxs-lookup"><span data-stu-id="7a00a-138">In contrast, query keys are for read-only operations, typically used by client applications that connect tooAzure Search.</span></span>

<span data-ttu-id="7a00a-139">在此範例中，我們可以包括 hello 查詢索引鍵 toohelp 強化 hello 最佳作法是在用戶端應用程式中使用 hello 查詢索引鍵。</span><span class="sxs-lookup"><span data-stu-id="7a00a-139">In this sample, we include hello query key toohelp reinforce hello best practice of using hello query key in client applications.</span></span>

<span data-ttu-id="7a00a-140">下列螢幕擷取畫面顯示 hello **config.js**開啟文字編輯器中，以 hello demarcated，讓您可以查看其中 tooupdate hello 檔案以 hello 值相關的項目都適用於您的搜尋服務。</span><span class="sxs-lookup"><span data-stu-id="7a00a-140">hello following screenshot shows **config.js** open in a text editor, with hello relevant entries demarcated so that you can see where tooupdate hello file with hello values that are valid for your search service.</span></span>

![][5]

## <a name="host-a-runtime-environment-for-hello-sample"></a><span data-ttu-id="7a00a-141">裝載執行階段環境的 hello 範例</span><span class="sxs-lookup"><span data-stu-id="7a00a-141">Host a runtime environment for hello sample</span></span>
<span data-ttu-id="7a00a-142">hello 範例需要 HTTP 伺服器，您可以安裝全域使用 npm。</span><span class="sxs-lookup"><span data-stu-id="7a00a-142">hello sample requires an HTTP server, which you can install globally using npm.</span></span>

<span data-ttu-id="7a00a-143">Hello，下列命令使用的 PowerShell 視窗。</span><span class="sxs-lookup"><span data-stu-id="7a00a-143">Use a PowerShell window for hello following commands.</span></span>

1. <span data-ttu-id="7a00a-144">瀏覽包含 hello toohello 資料夾**package.json**檔案。</span><span class="sxs-lookup"><span data-stu-id="7a00a-144">Navigate toohello folder that contains hello **package.json** file.</span></span>
2. <span data-ttu-id="7a00a-145">輸入 `npm install`。</span><span class="sxs-lookup"><span data-stu-id="7a00a-145">Type `npm install`.</span></span>
3. <span data-ttu-id="7a00a-146">輸入 `npm install -g http-server`。</span><span class="sxs-lookup"><span data-stu-id="7a00a-146">Type `npm install -g http-server`.</span></span>

## <a name="build-hello-index-and-run-hello-application"></a><span data-ttu-id="7a00a-147">建立 hello 索引並執行 hello 應用程式</span><span class="sxs-lookup"><span data-stu-id="7a00a-147">Build hello index and run hello application</span></span>
1. <span data-ttu-id="7a00a-148">輸入 `npm run indexDocuments`。</span><span class="sxs-lookup"><span data-stu-id="7a00a-148">Type `npm run indexDocuments`.</span></span>
2. <span data-ttu-id="7a00a-149">輸入 `npm run build`。</span><span class="sxs-lookup"><span data-stu-id="7a00a-149">Type `npm run build`.</span></span>
3. <span data-ttu-id="7a00a-150">輸入 `npm run start_server`。</span><span class="sxs-lookup"><span data-stu-id="7a00a-150">Type `npm run start_server`.</span></span>
4. <span data-ttu-id="7a00a-151">將您的瀏覽器導向至 `http://localhost:8080/index.html`</span><span class="sxs-lookup"><span data-stu-id="7a00a-151">Direct your browser at `http://localhost:8080/index.html`</span></span>

## <a name="search-on-usgs-data"></a><span data-ttu-id="7a00a-152">搜尋 USGS 資料</span><span class="sxs-lookup"><span data-stu-id="7a00a-152">Search on USGS data</span></span>
<span data-ttu-id="7a00a-153">hello USG 資料集包含相關 toohello 狀態的羅德島的記錄。</span><span class="sxs-lookup"><span data-stu-id="7a00a-153">hello USGS data set includes records that are relevant toohello state of Rhode Island.</span></span> <span data-ttu-id="7a00a-154">如果您按一下**搜尋**上是空的搜尋 方塊中，您取得 hello 排行前 50 名項目，hello 預設值。</span><span class="sxs-lookup"><span data-stu-id="7a00a-154">If you click **Search** on an empty search box, you get hello top 50 entries, which is hello default.</span></span>

<span data-ttu-id="7a00a-155">輸入的搜尋詞彙提供 hello 搜尋引擎一些 toogo 上。</span><span class="sxs-lookup"><span data-stu-id="7a00a-155">Entering a search term gives hello search engine something toogo on.</span></span> <span data-ttu-id="7a00a-156">試著輸入區域名稱。</span><span class="sxs-lookup"><span data-stu-id="7a00a-156">Try entering a regional name.</span></span> <span data-ttu-id="7a00a-157">「 Roger Williams 」 已羅德島 hello 第一個管理員。</span><span class="sxs-lookup"><span data-stu-id="7a00a-157">"Roger Williams" was hello first governor of Rhode Island.</span></span> <span data-ttu-id="7a00a-158">許多公園、建築物和學校都是以他的姓名命名。</span><span class="sxs-lookup"><span data-stu-id="7a00a-158">Numerous parks, buildings, and schools are named after him.</span></span>

![][9]

<span data-ttu-id="7a00a-159">此外，您也可以試著使用這些字詞：</span><span class="sxs-lookup"><span data-stu-id="7a00a-159">You could also try any of these terms:</span></span>

* <span data-ttu-id="7a00a-160">Pawtucket</span><span class="sxs-lookup"><span data-stu-id="7a00a-160">Pawtucket</span></span>
* <span data-ttu-id="7a00a-161">Pembroke</span><span class="sxs-lookup"><span data-stu-id="7a00a-161">Pembroke</span></span>
* <span data-ttu-id="7a00a-162">goose +cape</span><span class="sxs-lookup"><span data-stu-id="7a00a-162">goose +cape</span></span>

## <a name="next-steps"></a><span data-ttu-id="7a00a-163">後續步驟</span><span class="sxs-lookup"><span data-stu-id="7a00a-163">Next steps</span></span>
<span data-ttu-id="7a00a-164">這是根據 Node.js 和 hello USG 資料集 hello 第一個 Azure 搜尋教學課程。</span><span class="sxs-lookup"><span data-stu-id="7a00a-164">This is hello first Azure Search tutorial based on Node.js and hello USGS dataset.</span></span> <span data-ttu-id="7a00a-165">經過一段時間，我們將會延長此教學課程 toodemonstrate 您可能會想 toouse 自訂方案中的其他搜尋功能。</span><span class="sxs-lookup"><span data-stu-id="7a00a-165">Over time, we'll extend this tutorial toodemonstrate additional search features you might want toouse in your custom solutions.</span></span>

<span data-ttu-id="7a00a-166">如果您已有一些 Azure 搜尋服務的背景知識，可以利用此範例做為試用建議工具 (預先輸入或自動完成查詢)、篩選及多面向導覽的跳板。</span><span class="sxs-lookup"><span data-stu-id="7a00a-166">If you already have some background in Azure Search, you can use this sample as a springboard for trying suggesters (type-ahead or autocomplete queries), filters, and faceted navigation.</span></span> <span data-ttu-id="7a00a-167">您也可以藉由加入計數和批次的文件，以便使用者可以透過 hello 結果頁改善 hello 搜尋結果頁面時。</span><span class="sxs-lookup"><span data-stu-id="7a00a-167">You can also improve upon hello search results page by adding counts and batching documents so that users can page through hello results.</span></span>

<span data-ttu-id="7a00a-168">新 tooAzure 搜尋嗎？</span><span class="sxs-lookup"><span data-stu-id="7a00a-168">New tooAzure Search?</span></span> <span data-ttu-id="7a00a-169">我們建議您嘗試其他教學課程 toodevelop 了解您可以建立。</span><span class="sxs-lookup"><span data-stu-id="7a00a-169">We recommend trying other tutorials toodevelop an understanding of what you can create.</span></span> <span data-ttu-id="7a00a-170">請瀏覽我們[文件頁面](https://azure.microsoft.com/documentation/services/search/)toofind 更多資源。</span><span class="sxs-lookup"><span data-stu-id="7a00a-170">Visit our [documentation page](https://azure.microsoft.com/documentation/services/search/) toofind more resources.</span></span> <span data-ttu-id="7a00a-171">您也可以檢視中的 hello 連結我們[影片和教學課程清單](search-video-demo-tutorial-list.md)tooaccess 的詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="7a00a-171">You can also view hello links in our [Video and Tutorial list](search-video-demo-tutorial-list.md) tooaccess more information.</span></span>

<!--Image references-->
[1]: ./media/search-get-started-Nodejs/create-search-portal-1.PNG
[2]: ./media/search-get-started-Nodejs/create-search-portal-2.PNG
[3]: ./media/search-get-started-Nodejs/create-search-portal-3.PNG
[5]: ./media/search-get-started-Nodejs/AzSearch-Nodejs-configjs.png
[9]: ./media/search-get-started-Nodejs/rogerwilliamsschool.png
