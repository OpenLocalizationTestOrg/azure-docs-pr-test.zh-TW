---
title: "將 Azure 搜尋服務新增至 Blob 儲存體 | Microsoft Docs"
description: "使用 Azure 搜尋服務 HTTP REST API 在程式碼中建立索引。"
services: search
documentationcenter: 
author: ashmaka
manager: jhubbard
ms.service: search
ms.topic: article
ms.date: 05/04/2017
ms.author: ashmaka
ms.openlocfilehash: 0cd0cbb05c465d32a9ef02f9350ebdf9ccea36c5
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="searching-blob-storage-with-azure-search"></a><span data-ttu-id="88a7e-103">使用 Azure 搜尋服務搜尋 Blob 儲存體</span><span class="sxs-lookup"><span data-stu-id="88a7e-103">Searching Blob storage with Azure Search</span></span>

<span data-ttu-id="88a7e-104">搜尋 Azure Blob 儲存體中儲存的各種內容類型可能是難以解決的問題。</span><span class="sxs-lookup"><span data-stu-id="88a7e-104">Searching across the variety of content types stored in Azure Blob storage can be a difficult problem to solve.</span></span> <span data-ttu-id="88a7e-105">不過，使用 Azure 搜尋服務，您只要按幾下，即可編製索引並搜尋 Blob 內容。</span><span class="sxs-lookup"><span data-stu-id="88a7e-105">However, you can index and search the content of your Blobs in just a few clicks by using Azure Search.</span></span> <span data-ttu-id="88a7e-106">在 Blob 儲存體上搜尋需要佈建 Azure 搜尋服務。</span><span class="sxs-lookup"><span data-stu-id="88a7e-106">Searching over Blob storage requires provisioning an Azure Search service.</span></span> <span data-ttu-id="88a7e-107">在[價格頁面](https://aka.ms/azspricing)可以找到 Azure 搜尋服務的各種服務限制和定價層。</span><span class="sxs-lookup"><span data-stu-id="88a7e-107">The various service limits and pricing tiers of Azure Search can be found on the [pricing page](https://aka.ms/azspricing).</span></span>

## <a name="what-is-azure-search"></a><span data-ttu-id="88a7e-108">何謂 Azure 搜尋服務？</span><span class="sxs-lookup"><span data-stu-id="88a7e-108">What is Azure Search?</span></span>
<span data-ttu-id="88a7e-109">[Azure 搜尋服務](https://aka.ms/whatisazsearch)是一個搜尋解決方案，可讓開發人員輕鬆新增 Web 和行動應用程式的強大全文檢索搜尋體驗。</span><span class="sxs-lookup"><span data-stu-id="88a7e-109">[Azure Search](https://aka.ms/whatisazsearch) is a search solution that makes it easy for developers to add robust full-text search  experiences to web and mobile applications.</span></span> <span data-ttu-id="88a7e-110">Azure 搜尋服務不需要管理任何搜尋基礎結構，同時可提供 [99.9% 的運作時間 SLA](https://aka.ms/azuresearchsla)。</span><span class="sxs-lookup"><span data-stu-id="88a7e-110">As service, Azure Search removes the need to manage any search infrastructure while offering a [99.9% uptime SLA](https://aka.ms/azuresearchsla).</span></span>

<span data-ttu-id="88a7e-111">透過 56 種語言的進階支援，Azure 搜尋服務可以分析您的內容，並以智慧方式處理特定語言結構建構。</span><span class="sxs-lookup"><span data-stu-id="88a7e-111">With advanced support for 56 languages, Azure Search can analyze your content and intelligently handle language-specific constructs.</span></span> <span data-ttu-id="88a7e-112">Azure 搜尋服務也提供各種工具來打造豐富的搜尋使用者經驗。</span><span class="sxs-lookup"><span data-stu-id="88a7e-112">Azure Search also provides the tools to build a rich search user experience.</span></span> <span data-ttu-id="88a7e-113">使用 Azure 搜尋服務新增功能很簡單，例如多面向導覽、自動提示搜尋建議，以及使用者介面的結果醒目提示。</span><span class="sxs-lookup"><span data-stu-id="88a7e-113">It is simple to add features such as faceted navigation, typeahead search suggestions, and hit highlighting to user interfaces using Azure Search.</span></span> <span data-ttu-id="88a7e-114">若要了解 Azure 搜尋服務的功能，您可以閱讀服務的[文件](https://aka.ms/azsearchdocs)。</span><span class="sxs-lookup"><span data-stu-id="88a7e-114">To learn about Azure Search’s features, you can read the service's [documentation](https://aka.ms/azsearchdocs).</span></span>

## <a name="crack-open-and-search-through-the-content-of-enterprise-document-formats"></a><span data-ttu-id="88a7e-115">直接開啟並搜尋企業文件格式的內容</span><span class="sxs-lookup"><span data-stu-id="88a7e-115">Crack open and search through the content of enterprise document formats</span></span>
<span data-ttu-id="88a7e-116">透過 Azure Blob 儲存體中的[文件擷取](https://aka.ms/azsblobindexer)支援，Azure 搜尋服務可以為 Blob 中儲存的各種檔案類型內容編製索引︰</span><span class="sxs-lookup"><span data-stu-id="88a7e-116">With support for [document extraction](https://aka.ms/azsblobindexer) in Azure Blob storage, Azure Search can index the content of a variety of file types stored in blobs:</span></span>
- <span data-ttu-id="88a7e-117">PDF</span><span class="sxs-lookup"><span data-stu-id="88a7e-117">PDF</span></span>
- <span data-ttu-id="88a7e-118">Microsoft Office：DOCX/DOC、XLSX/XLS、PPTX/PPT、MSG (Outlook 電子郵件)</span><span class="sxs-lookup"><span data-stu-id="88a7e-118">Microsoft Office: DOCX/DOC, XLSX/XLS, PPTX/PPT, MSG (Outlook emails)</span></span>
- <span data-ttu-id="88a7e-119">HTML</span><span class="sxs-lookup"><span data-stu-id="88a7e-119">HTML</span></span>
- <span data-ttu-id="88a7e-120">純文字檔案</span><span class="sxs-lookup"><span data-stu-id="88a7e-120">Plain text files</span></span>

<span data-ttu-id="88a7e-121">擷取這些檔案類型的文字和中繼資料，即可利用單一查詢輕鬆搜尋多個檔案格式，以找出最相關的文件 (無論何種類型)。</span><span class="sxs-lookup"><span data-stu-id="88a7e-121">By extracting text and metadata of these file types, it is easy to search across multiple file formats with a single query to find the most relevant documents regardless of type.</span></span> <span data-ttu-id="88a7e-122">藉由為 Microsoft Office 文件、PDF 和電子郵件的內容和中繼資料編製索引，可以使用 Blob 儲存體和 Azure 搜尋服務建置強大的企業容管理解決方案。</span><span class="sxs-lookup"><span data-stu-id="88a7e-122">By indexing the content and the metadata of Microsoft Office documents, PDFs, and emails, it’s possible to build a robust enterprise content management solution using Blob storage and Azure Search.</span></span>

## <a name="search-through-your-blob-metadata"></a><span data-ttu-id="88a7e-123">搜尋您的 Blob 中繼資料</span><span class="sxs-lookup"><span data-stu-id="88a7e-123">Search through your blob metadata</span></span>
<span data-ttu-id="88a7e-124">若要簡化任何內容類型的 Blob 排序，常見案例是為每個 Blob 的自訂、使用者定義 Blob 中繼資料以及系統屬性編製索引。</span><span class="sxs-lookup"><span data-stu-id="88a7e-124">A common scenario that makes it easy to sort through blobs of any content type is to index the custom, user-defined blob metadata as well as the system properties for each of your blobs.</span></span> <span data-ttu-id="88a7e-125">如此一來，每個 Blob 的資訊都會在 Blob 中編製索引 (無論何種文件類型)，因此您可以輕鬆地將所有的 Blob 儲存體內容排序和進行層面分類。</span><span class="sxs-lookup"><span data-stu-id="88a7e-125">In this way, information for each and every  blob is indexed regardless of the type of document in the blob so you can easily sort and facet across all of your Blob storage content.</span></span>

[<span data-ttu-id="88a7e-126">深入了解如何編製 Blob 中繼資料的索引。</span><span class="sxs-lookup"><span data-stu-id="88a7e-126">Learn more about indexing blob metadata.</span></span>](https://aka.ms/azsblobmetadataindexing)

## <a name="image-search"></a><span data-ttu-id="88a7e-127">影像搜尋</span><span class="sxs-lookup"><span data-stu-id="88a7e-127">Image search</span></span>
<span data-ttu-id="88a7e-128">Azure 搜尋服務的全文檢索搜尋、多面向導覽和排序功能現在可套用至 Blob 中儲存的影像中繼資料。</span><span class="sxs-lookup"><span data-stu-id="88a7e-128">Azure Search’s full-text search, faceted navigation, and sorting capabilities can now be applied to the metadata of images stored in blobs.</span></span>

<span data-ttu-id="88a7e-129">如果從 Microsoft 辨識服務使用[電腦視覺 API](https://www.microsoft.com/cognitive-services/computer-vision-api) 預先處理這些影像，則可以為在每個影像中找到的視覺內容 (包括 OCR 和手寫辨識) 編製索引。</span><span class="sxs-lookup"><span data-stu-id="88a7e-129">If these images are pre-processed using the [Computer Vision API](https://www.microsoft.com/cognitive-services/computer-vision-api) from Microsoft’s Cognitive Services, then it is possible to index the visual content found in each image including OCR and handwriting recognition.</span></span> <span data-ttu-id="88a7e-130">我們正努力將 OCR 和其他影像處理功能直接新增到 Azure 搜尋服務，如果您對這些功能有興趣，請在我們的 [UserVoice](https://aka.ms/azsuv) 上提出要求或[傳送電子郵件給我們](mailto:azscustquestions@microsoft.com)。</span><span class="sxs-lookup"><span data-stu-id="88a7e-130">We are working on adding OCR and other image processing capabilities directly to Azure Search, if you are interested in these capabilities please submit a request on our [UserVoice](https://aka.ms/azsuv) or [email us](mailto:azscustquestions@microsoft.com).</span></span>

## <a name="index-and-search-through-json-blobs"></a><span data-ttu-id="88a7e-131">檢索和搜尋 JSON Blob</span><span class="sxs-lookup"><span data-stu-id="88a7e-131">Index and search through JSON blobs</span></span>
<span data-ttu-id="88a7e-132">可以將 Azure 搜尋服務設定為擷取在包含 JSON 的 Blob 中找到的結構化內容。</span><span class="sxs-lookup"><span data-stu-id="88a7e-132">Azure Search can be configured to extract structured content found in blobs that contain JSON.</span></span> <span data-ttu-id="88a7e-133">Azure 搜尋服務可以讀取 JSON Blob，並將結構化內容剖析成 Azure 搜尋服務文件的適當欄位。</span><span class="sxs-lookup"><span data-stu-id="88a7e-133">Azure Search can read JSON blobs and parse the structured content into the appropriate fields of an Azure Search document.</span></span> <span data-ttu-id="88a7e-134">Azure 搜尋服務也會採用包含 JSON 物件陣列的 Blob，並將每個元素對應至不同的 Azure 搜尋服務文件。</span><span class="sxs-lookup"><span data-stu-id="88a7e-134">Azure Search can also take blobs that contain an array of JSON objects and map each element to a separate Azure Search document.</span></span>

<span data-ttu-id="88a7e-135">請注意，JSON 剖析目前無法透過入口網站設定。</span><span class="sxs-lookup"><span data-stu-id="88a7e-135">Note that JSON parsing is not currently configurable through the portal.</span></span> [<span data-ttu-id="88a7e-136">深入了解 Azure 搜尋服務中的 JSON 剖析。</span><span class="sxs-lookup"><span data-stu-id="88a7e-136">Learn more about JSON parsing in Azure Search.</span></span>](https://aka.ms/azsjsonblobindexing)

## <a name="quick-start"></a><span data-ttu-id="88a7e-137">快速入門</span><span class="sxs-lookup"><span data-stu-id="88a7e-137">Quick start</span></span>
<span data-ttu-id="88a7e-138">您可以直接從 Blob 儲存體入口網站刀鋒視窗將 Azure 搜尋服務新增至 Blob。</span><span class="sxs-lookup"><span data-stu-id="88a7e-138">Azure Search can be added to blobs directly from the Blob storage portal blade.</span></span>

![](./media/search-blob-storage-integration/blob-blade.png)

<span data-ttu-id="88a7e-139">按一下 [新增 Azure 搜尋服務] 選項會啟動一個流程，您可以在其中選取現有的 Azure 搜尋服務或建立新的服務。</span><span class="sxs-lookup"><span data-stu-id="88a7e-139">Clicking on the "Add Azure Search" option launches a flow where you can select an existing Azure Search service or create a new service.</span></span> <span data-ttu-id="88a7e-140">如果您建立新的服務，您將會跳脫儲存體帳戶的入口網站經驗。</span><span class="sxs-lookup"><span data-stu-id="88a7e-140">If you create a new service, you will be navigated out of your Storage account's portal experience.</span></span> <span data-ttu-id="88a7e-141">您必須重新瀏覽至儲存體入口網站刀鋒視窗，然後重新選取 [新增 Azure 搜尋服務] 選項，便可在其中選取現有的服務。</span><span class="sxs-lookup"><span data-stu-id="88a7e-141">You will need to re-navigate to the Storage portal blade and re-select the "Add Azure Search" option, where you can select the existing service.</span></span>

### <a name="next-steps"></a><span data-ttu-id="88a7e-142">後續步驟</span><span class="sxs-lookup"><span data-stu-id="88a7e-142">Next Steps</span></span>
<span data-ttu-id="88a7e-143">閱讀完整的[文件](https://aka.ms/azsblobindexer)以深入了解 Azure 搜尋服務 Blob 索引子。</span><span class="sxs-lookup"><span data-stu-id="88a7e-143">Learn more about the Azure Search Blob Indexer in the full [documentation](https://aka.ms/azsblobindexer).</span></span>
