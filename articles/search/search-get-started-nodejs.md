---
title: "開始在 Node.js 中使用 Azure 搜尋服務 | Microsoft Docs"
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
ms.openlocfilehash: 32865ed986f5eea961ef2c3813dcc6531498c90a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-azure-search-in-nodejs"></a><span data-ttu-id="65307-103">開始在 Node.js 中使用 Azure 搜尋服務</span><span class="sxs-lookup"><span data-stu-id="65307-103">Get started with Azure Search in Node.js</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="65307-104">入口網站</span><span class="sxs-lookup"><span data-stu-id="65307-104">Portal</span></span>](search-get-started-portal.md)
> * [<span data-ttu-id="65307-105">.NET</span><span class="sxs-lookup"><span data-stu-id="65307-105">.NET</span></span>](search-howto-dotnet-sdk.md)
> 
> 

<span data-ttu-id="65307-106">瞭解如何建置使用 Azure 搜尋服務提供搜尋體驗的自訂 Node.js 搜尋應用程式。</span><span class="sxs-lookup"><span data-stu-id="65307-106">Learn how to build a custom Node.js search application that uses Azure Search for its search experience.</span></span> <span data-ttu-id="65307-107">本教學課程利用 [Azure 搜尋服務 REST API](https://msdn.microsoft.com/library/dn798935.aspx) 來建構在此練習中所使用的物件和作業。</span><span class="sxs-lookup"><span data-stu-id="65307-107">This tutorial uses the [Azure Search Service REST API](https://msdn.microsoft.com/library/dn798935.aspx) to construct the objects and operations used in this exercise.</span></span>

<span data-ttu-id="65307-108">我們使用 [Node.js](https://Nodejs.org)NPM、[Sublime Text 3](http://www.sublimetext.com/3) 及 Windows 8.1 上的 Windows PowerShell 來開發和測試此代碼。</span><span class="sxs-lookup"><span data-stu-id="65307-108">We used [Node.js](https://Nodejs.org) and NPM, [Sublime Text 3](http://www.sublimetext.com/3), and Windows PowerShell on Windows 8.1 to develop and test this code.</span></span>

<span data-ttu-id="65307-109">若要執行此範例，必須要有 Azure 搜尋服務，您可以在 [Azure 入口網站](https://portal.azure.com)註冊此服務。</span><span class="sxs-lookup"><span data-stu-id="65307-109">To run this sample, you must have an Azure Search service, which you can sign up for in the [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="65307-110">如需逐步指示，請參閱 [在入口網站中建立 Azure 搜尋服務](search-create-service-portal.md) 。</span><span class="sxs-lookup"><span data-stu-id="65307-110">See [Create an Azure Search service in the portal](search-create-service-portal.md) for step-by-step instructions.</span></span>

## <a name="about-the-data"></a><span data-ttu-id="65307-111">關於資料</span><span class="sxs-lookup"><span data-stu-id="65307-111">About the data</span></span>
<span data-ttu-id="65307-112">此範例應用程式使用的 [美國地理服務中心 (USGS)](http://geonames.usgs.gov/domestic/download_data.htm)資料已依據羅德島州進行篩選，藉此減少資料集的大小。</span><span class="sxs-lookup"><span data-stu-id="65307-112">This sample application uses data from the [United States Geological Services (USGS)](http://geonames.usgs.gov/domestic/download_data.htm), filtered on the state of Rhode Island to reduce the dataset size.</span></span> <span data-ttu-id="65307-113">我們將使用此資料，建置可傳回地標建築物 (例如醫院和學校) 及地理特徵 (例如河流、湖泊和山峰) 等相關資料的搜尋應用程式。</span><span class="sxs-lookup"><span data-stu-id="65307-113">We'll use this data to build a search application that returns landmark buildings such as hospitals and schools, as well as geological features like streams, lakes, and summits.</span></span>

<span data-ttu-id="65307-114">在此應用程式中， **DataIndexer** 程式會使用 [索引子](https://msdn.microsoft.com/library/azure/dn798918.aspx) 建構來建置及載入索引，以從公用 Azure SQL Database 擷取篩選過的 USGS 資料集。</span><span class="sxs-lookup"><span data-stu-id="65307-114">In this application, the **DataIndexer** program builds and loads the index using an [Indexer](https://msdn.microsoft.com/library/azure/dn798918.aspx) construct, retrieving the filtered USGS dataset from a public Azure SQL Database.</span></span> <span data-ttu-id="65307-115">程式碼中提供線上資料來源的認證和連接資訊。</span><span class="sxs-lookup"><span data-stu-id="65307-115">Credentials and connection information to the online data source is provided in the program code.</span></span> <span data-ttu-id="65307-116">不需要進一步設定。</span><span class="sxs-lookup"><span data-stu-id="65307-116">No further configuration is necessary.</span></span>

> [!NOTE]
> <span data-ttu-id="65307-117">我們在此資料集套用了一個篩選，以維持不超過免費版定價層的 10,000 個文件的數量上限。</span><span class="sxs-lookup"><span data-stu-id="65307-117">We applied a filter on this dataset to stay under the 10,000 document limit of the free pricing tier.</span></span> <span data-ttu-id="65307-118">如果使用標準版定價層，就不會套用此限制。</span><span class="sxs-lookup"><span data-stu-id="65307-118">If you use the standard tier, this limit does not apply.</span></span> <span data-ttu-id="65307-119">如需各個定價層的容量詳細資料，請參閱 [搜尋服務限制](search-limits-quotas-capacity.md)。</span><span class="sxs-lookup"><span data-stu-id="65307-119">For details about capacity for each pricing tier, see [Search service limits](search-limits-quotas-capacity.md).</span></span>
> 
> 

<a id="sub-2"></a>

## <a name="find-the-service-name-and-api-key-of-your-azure-search-service"></a><span data-ttu-id="65307-120">尋找 Azure 搜尋服務的服務名稱和 API 金鑰</span><span class="sxs-lookup"><span data-stu-id="65307-120">Find the service name and api-key of your Azure Search service</span></span>
<span data-ttu-id="65307-121">建立服務之後，請返回入口網站取得 URL 或 `api-key`。</span><span class="sxs-lookup"><span data-stu-id="65307-121">After you create the service, return to the portal to get the URL or `api-key`.</span></span> <span data-ttu-id="65307-122">如果想要連接至搜尋服務，您必須同時擁有 URL 和 `api-key` 才能驗證呼叫。</span><span class="sxs-lookup"><span data-stu-id="65307-122">Connections to your Search service require that you have both the URL and an `api-key` to authenticate the call.</span></span>

1. <span data-ttu-id="65307-123">登入 [Azure 入口網站](https://portal.azure.com)。</span><span class="sxs-lookup"><span data-stu-id="65307-123">Sign in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="65307-124">在導向列中，按一下 [搜尋服務]  列出為您的訂用帳戶佈建的所有 Azure 搜尋服務。</span><span class="sxs-lookup"><span data-stu-id="65307-124">In the jump bar, click **Search service** to list all Azure Search services provisioned for your subscription.</span></span>
3. <span data-ttu-id="65307-125">選取您要使用的服務。</span><span class="sxs-lookup"><span data-stu-id="65307-125">Select the service you want to use.</span></span>
4. <span data-ttu-id="65307-126">您應在服務儀表板上看到基本資訊磚，例如用於存取系統管理金鑰的鑰匙圖示。</span><span class="sxs-lookup"><span data-stu-id="65307-126">On the service dashboard, you should see tiles for essential information, such as the key icon for accessing the admin keys.</span></span>
5. <span data-ttu-id="65307-127">複製服務 URL、系統管理金鑰和查詢金鑰。</span><span class="sxs-lookup"><span data-stu-id="65307-127">Copy the service URL, an admin key, and a query key.</span></span> <span data-ttu-id="65307-128">稍後您需要將這三個項目加到 config.js 檔案中。</span><span class="sxs-lookup"><span data-stu-id="65307-128">You need all three later when you add them to the config.js file.</span></span>

## <a name="download-the-sample-files"></a><span data-ttu-id="65307-129">下載範例檔案</span><span class="sxs-lookup"><span data-stu-id="65307-129">Download the sample files</span></span>
<span data-ttu-id="65307-130">使用以下其中一種方法下載範例。</span><span class="sxs-lookup"><span data-stu-id="65307-130">Use either one of the following approaches to download the sample.</span></span>

1. <span data-ttu-id="65307-131">移至 [AzureSearchNodeJSIndexerDemo](https://github.com/AzureSearch/AzureSearchNodejsIndexerDemo)。</span><span class="sxs-lookup"><span data-stu-id="65307-131">Go to [AzureSearchNodeJSIndexerDemo](https://github.com/AzureSearch/AzureSearchNodejsIndexerDemo).</span></span>
2. <span data-ttu-id="65307-132">按一下 [下載 ZIP] ，儲存 .zip 檔案，然後解壓縮其中所含的所有檔案。</span><span class="sxs-lookup"><span data-stu-id="65307-132">Click **Download ZIP**, save the .zip file, and then extract all the files it contains.</span></span>

<span data-ttu-id="65307-133">所有後續的檔案修改及執行陳述式都會用到此資料夾中的檔案。</span><span class="sxs-lookup"><span data-stu-id="65307-133">All subsequent file modifications and run statements are made against files in this folder.</span></span>

## <a name="update-the-configjs-with-your-search-service-url-and-api-key"></a><span data-ttu-id="65307-134">更新 config.js，</span><span class="sxs-lookup"><span data-stu-id="65307-134">Update the config.js.</span></span> <span data-ttu-id="65307-135">方法為使用您的搜尋服務 URL 及 API 金鑰</span><span class="sxs-lookup"><span data-stu-id="65307-135">with your Search service URL and api-key</span></span>
<span data-ttu-id="65307-136">使用先前複製的 URL 和 API 金鑰，在組態檔案中指定 URL、系統管理金鑰和查詢金鑰。</span><span class="sxs-lookup"><span data-stu-id="65307-136">Using the URL and api-key that you copied earlier, specify the URL, admin-key, and query-key in configuration file.</span></span>

<span data-ttu-id="65307-137">系統管理金鑰可將服務作業的完整控制權限授與給您，包括建立或刪除索引，以及載入文件。</span><span class="sxs-lookup"><span data-stu-id="65307-137">Admin keys grant full control over service operations, including creating or deleting an index and loading documents.</span></span> <span data-ttu-id="65307-138">相較之下，查詢金鑰僅用於唯讀作業，通常由連接到 Azure 搜尋服務的用戶端應用程式所用。</span><span class="sxs-lookup"><span data-stu-id="65307-138">In contrast, query keys are for read-only operations, typically used by client applications that connect to Azure Search.</span></span>

<span data-ttu-id="65307-139">在此範例中，我們包含查詢金鑰，協助您在客戶端應用程式中確實熟悉使用查詢金鑰的最佳做法。</span><span class="sxs-lookup"><span data-stu-id="65307-139">In this sample, we include the query key to help reinforce the best practice of using the query key in client applications.</span></span>

<span data-ttu-id="65307-140">下面的螢幕擷取畫面顯示在文字編輯器中開啟 **config.js** 的畫面，並與相關項目區分，讓您得知哪些位置可以使用對搜尋服務有效的值更新檔案。</span><span class="sxs-lookup"><span data-stu-id="65307-140">The following screenshot shows **config.js** open in a text editor, with the relevant entries demarcated so that you can see where to update the file with the values that are valid for your search service.</span></span>

![][5]

## <a name="host-a-runtime-environment-for-the-sample"></a><span data-ttu-id="65307-141">為範例託管執行階段環境</span><span class="sxs-lookup"><span data-stu-id="65307-141">Host a runtime environment for the sample</span></span>
<span data-ttu-id="65307-142">此範例需要 HTTP 伺服器，讓您安裝全球使用的 NPM。</span><span class="sxs-lookup"><span data-stu-id="65307-142">The sample requires an HTTP server, which you can install globally using npm.</span></span>

<span data-ttu-id="65307-143">使用 PowerShell 視窗以執行以下命令。</span><span class="sxs-lookup"><span data-stu-id="65307-143">Use a PowerShell window for the following commands.</span></span>

1. <span data-ttu-id="65307-144">瀏覽至內含 **package.json** 檔案的資料夾。</span><span class="sxs-lookup"><span data-stu-id="65307-144">Navigate to the folder that contains the **package.json** file.</span></span>
2. <span data-ttu-id="65307-145">輸入 `npm install`。</span><span class="sxs-lookup"><span data-stu-id="65307-145">Type `npm install`.</span></span>
3. <span data-ttu-id="65307-146">輸入 `npm install -g http-server`。</span><span class="sxs-lookup"><span data-stu-id="65307-146">Type `npm install -g http-server`.</span></span>

## <a name="build-the-index-and-run-the-application"></a><span data-ttu-id="65307-147">建置索引並執行應用程式</span><span class="sxs-lookup"><span data-stu-id="65307-147">Build the index and run the application</span></span>
1. <span data-ttu-id="65307-148">輸入 `npm run indexDocuments`。</span><span class="sxs-lookup"><span data-stu-id="65307-148">Type `npm run indexDocuments`.</span></span>
2. <span data-ttu-id="65307-149">輸入 `npm run build`。</span><span class="sxs-lookup"><span data-stu-id="65307-149">Type `npm run build`.</span></span>
3. <span data-ttu-id="65307-150">輸入 `npm run start_server`。</span><span class="sxs-lookup"><span data-stu-id="65307-150">Type `npm run start_server`.</span></span>
4. <span data-ttu-id="65307-151">將您的瀏覽器導向至 `http://localhost:8080/index.html`</span><span class="sxs-lookup"><span data-stu-id="65307-151">Direct your browser at `http://localhost:8080/index.html`</span></span>

## <a name="search-on-usgs-data"></a><span data-ttu-id="65307-152">搜尋 USGS 資料</span><span class="sxs-lookup"><span data-stu-id="65307-152">Search on USGS data</span></span>
<span data-ttu-id="65307-153">USGS 資料集包含與羅德島州相關的記錄。</span><span class="sxs-lookup"><span data-stu-id="65307-153">The USGS data set includes records that are relevant to the state of Rhode Island.</span></span> <span data-ttu-id="65307-154">如果您在空白的搜尋方塊中按一下 [搜尋] ，預設會出現前 50 個項目。</span><span class="sxs-lookup"><span data-stu-id="65307-154">If you click **Search** on an empty search box, you get the top 50 entries, which is the default.</span></span>

<span data-ttu-id="65307-155">輸入搜尋詞彙，讓搜尋引擎運作一下。</span><span class="sxs-lookup"><span data-stu-id="65307-155">Entering a search term gives the search engine something to go on.</span></span> <span data-ttu-id="65307-156">試著輸入區域名稱。</span><span class="sxs-lookup"><span data-stu-id="65307-156">Try entering a regional name.</span></span> <span data-ttu-id="65307-157">"Roger Williams" 是羅德島州的第一任州長。</span><span class="sxs-lookup"><span data-stu-id="65307-157">"Roger Williams" was the first governor of Rhode Island.</span></span> <span data-ttu-id="65307-158">許多公園、建築物和學校都是以他的姓名命名。</span><span class="sxs-lookup"><span data-stu-id="65307-158">Numerous parks, buildings, and schools are named after him.</span></span>

![][9]

<span data-ttu-id="65307-159">此外，您也可以試著使用這些字詞：</span><span class="sxs-lookup"><span data-stu-id="65307-159">You could also try any of these terms:</span></span>

* <span data-ttu-id="65307-160">Pawtucket</span><span class="sxs-lookup"><span data-stu-id="65307-160">Pawtucket</span></span>
* <span data-ttu-id="65307-161">Pembroke</span><span class="sxs-lookup"><span data-stu-id="65307-161">Pembroke</span></span>
* <span data-ttu-id="65307-162">goose +cape</span><span class="sxs-lookup"><span data-stu-id="65307-162">goose +cape</span></span>

## <a name="next-steps"></a><span data-ttu-id="65307-163">後續步驟</span><span class="sxs-lookup"><span data-stu-id="65307-163">Next steps</span></span>
<span data-ttu-id="65307-164">這是第一個以 Node.js 和 USGS 資料集為基礎的 Azure 搜尋服務教學課程。</span><span class="sxs-lookup"><span data-stu-id="65307-164">This is the first Azure Search tutorial based on Node.js and the USGS dataset.</span></span> <span data-ttu-id="65307-165">我們會漸漸擴充本教學課程，以示範其他您可能會想用在自訂方案中的搜尋功能。</span><span class="sxs-lookup"><span data-stu-id="65307-165">Over time, we'll extend this tutorial to demonstrate additional search features you might want to use in your custom solutions.</span></span>

<span data-ttu-id="65307-166">如果您已有一些 Azure 搜尋服務的背景知識，可以利用此範例做為試用建議工具 (預先輸入或自動完成查詢)、篩選及多面向導覽的跳板。</span><span class="sxs-lookup"><span data-stu-id="65307-166">If you already have some background in Azure Search, you can use this sample as a springboard for trying suggesters (type-ahead or autocomplete queries), filters, and faceted navigation.</span></span> <span data-ttu-id="65307-167">您也可以新增計數和批次處理文件，讓使用者可以逐頁查看結果，藉此改進搜尋結果頁面。</span><span class="sxs-lookup"><span data-stu-id="65307-167">You can also improve upon the search results page by adding counts and batching documents so that users can page through the results.</span></span>

<span data-ttu-id="65307-168">不熟悉 Azure 搜尋服務嗎？</span><span class="sxs-lookup"><span data-stu-id="65307-168">New to Azure Search?</span></span> <span data-ttu-id="65307-169">建議您嘗試學習其他教學課程，深入了解您還可以建立哪些東西。</span><span class="sxs-lookup"><span data-stu-id="65307-169">We recommend trying other tutorials to develop an understanding of what you can create.</span></span> <span data-ttu-id="65307-170">請瀏覽我們的 [文件頁面](https://azure.microsoft.com/documentation/services/search/) 以尋找更多資源。</span><span class="sxs-lookup"><span data-stu-id="65307-170">Visit our [documentation page](https://azure.microsoft.com/documentation/services/search/) to find more resources.</span></span> <span data-ttu-id="65307-171">您也可以查看我們 [影片和教學課程清單](search-video-demo-tutorial-list.md) 中的連結，以存取更多資訊。</span><span class="sxs-lookup"><span data-stu-id="65307-171">You can also view the links in our [Video and Tutorial list](search-video-demo-tutorial-list.md) to access more information.</span></span>

<!--Image references-->
[1]: ./media/search-get-started-Nodejs/create-search-portal-1.PNG
[2]: ./media/search-get-started-Nodejs/create-search-portal-2.PNG
[3]: ./media/search-get-started-Nodejs/create-search-portal-3.PNG
[5]: ./media/search-get-started-Nodejs/AzSearch-Nodejs-configjs.png
[9]: ./media/search-get-started-Nodejs/rogerwilliamsschool.png
