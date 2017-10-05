---
title: "如何使用媒體編碼器標準為 Azure 資產編碼 | Microsoft Docs"
description: "了解如何使用媒體編碼器標準，為 Azure 媒體服務上的媒體內容編碼。 程式碼範例會使用 REST API。"
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: 2a7273c6-8a22-4f82-9bfe-4509ff32d4a4
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/10/2017
ms.author: juliako
ms.openlocfilehash: 796f3b5a4dd56a0160986600cbbcf38faf8add56
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="how-to-encode-an-asset-by-using-media-encoder-standard"></a><span data-ttu-id="fe2a7-104">如何使用媒體編碼器標準為資產編碼</span><span class="sxs-lookup"><span data-stu-id="fe2a7-104">How to encode an asset by using Media Encoder Standard</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="fe2a7-105">.NET</span><span class="sxs-lookup"><span data-stu-id="fe2a7-105">.NET</span></span>](media-services-dotnet-encode-with-media-encoder-standard.md)
> * [<span data-ttu-id="fe2a7-106">REST</span><span class="sxs-lookup"><span data-stu-id="fe2a7-106">REST</span></span>](media-services-rest-encode-asset.md)
> * [<span data-ttu-id="fe2a7-107">入口網站</span><span class="sxs-lookup"><span data-stu-id="fe2a7-107">Portal</span></span>](media-services-portal-encode.md)
>
>

## <a name="overview"></a><span data-ttu-id="fe2a7-108">概觀</span><span class="sxs-lookup"><span data-stu-id="fe2a7-108">Overview</span></span>
<span data-ttu-id="fe2a7-109">若要透過網際網路傳遞數位視訊，您必須壓縮媒體。</span><span class="sxs-lookup"><span data-stu-id="fe2a7-109">To deliver digital video over the Internet, you must compress the media.</span></span> <span data-ttu-id="fe2a7-110">數位視訊檔案十分龐大，而且可能太大而無法透過網際網路傳遞，或是太大而使您客戶的裝置無法正確顯示。</span><span class="sxs-lookup"><span data-stu-id="fe2a7-110">Digital video files are large and may be too big to deliver over the Internet, or for your customers’ devices to display properly.</span></span> <span data-ttu-id="fe2a7-111">編碼是壓縮視訊和音訊，好讓客戶能檢視您的媒體的程序。</span><span class="sxs-lookup"><span data-stu-id="fe2a7-111">Encoding is the process of compressing video and audio so your customers can view your media.</span></span>

<span data-ttu-id="fe2a7-112">編碼作業是 Azure 媒體服務中最常見的處理作業之一。</span><span class="sxs-lookup"><span data-stu-id="fe2a7-112">Encoding jobs are one of the most common processing operations in Azure Media Services.</span></span> <span data-ttu-id="fe2a7-113">您建立編碼工作以將媒體檔案從一種編碼轉換成另一種編碼。</span><span class="sxs-lookup"><span data-stu-id="fe2a7-113">You create encoding jobs to convert media files from one encoding to another.</span></span> <span data-ttu-id="fe2a7-114">編碼時，您可以使用媒體服務內建的編碼器 (媒體編碼器標準)。</span><span class="sxs-lookup"><span data-stu-id="fe2a7-114">When you encode, you can use the Media Services built-in encoder (Media Encoder Standard).</span></span> <span data-ttu-id="fe2a7-115">您也可以使用媒體服務合作夥伴所提供的編碼器。</span><span class="sxs-lookup"><span data-stu-id="fe2a7-115">You can also use an encoder provided by a Media Services partner.</span></span> <span data-ttu-id="fe2a7-116">第三方編碼器可透過 Azure Marketplace 取得。</span><span class="sxs-lookup"><span data-stu-id="fe2a7-116">Third-party encoders are available through the Azure Marketplace.</span></span> <span data-ttu-id="fe2a7-117">您可以使用針對您的編碼器定義的預設字串，或使用預設組態檔，指定編碼工作的詳細資料。</span><span class="sxs-lookup"><span data-stu-id="fe2a7-117">You can specify the details of encoding tasks by using preset strings defined for your encoder, or by using preset configuration files.</span></span> <span data-ttu-id="fe2a7-118">若要查看可用的預設類型，請參閱 [媒體編碼器標準的工作預設](http://msdn.microsoft.com/library/mt269960)。</span><span class="sxs-lookup"><span data-stu-id="fe2a7-118">To see the types of presets that are available, see [Task Presets for Media Encoder Standard](http://msdn.microsoft.com/library/mt269960).</span></span>

<span data-ttu-id="fe2a7-119">視您想要完成的處理類型而定。每個作業可以有一或多個工作。</span><span class="sxs-lookup"><span data-stu-id="fe2a7-119">Each job can have one or more tasks depending on the type of processing that you want to accomplish.</span></span> <span data-ttu-id="fe2a7-120">透過 REST API，您可以用下列其中一種方式來建立作業及其相關的工作：</span><span class="sxs-lookup"><span data-stu-id="fe2a7-120">Through the REST API, you can create jobs and their related tasks in one of two ways:</span></span>

* <span data-ttu-id="fe2a7-121">工作可透過 Job 實體上的 Tasks 導覽屬性，以內嵌方式定義。</span><span class="sxs-lookup"><span data-stu-id="fe2a7-121">Tasks can be defined inline through the Tasks navigation property on Job entities.</span></span>
* <span data-ttu-id="fe2a7-122">使用 OData 批次處理。</span><span class="sxs-lookup"><span data-stu-id="fe2a7-122">Use OData batch processing.</span></span>

<span data-ttu-id="fe2a7-123">我們建議一律將來源檔案編碼為調適型位元速率 MP4 集，然後使用[動態封裝](media-services-dynamic-packaging-overview.md)，將該集合轉換為所需的格式。</span><span class="sxs-lookup"><span data-stu-id="fe2a7-123">We recommend that you always encode your source files into an adaptive bitrate MP4 set, and then convert the set to the desired format by using [dynamic packaging](media-services-dynamic-packaging-overview.md).</span></span>

<span data-ttu-id="fe2a7-124">如果您的輸出資產是已加密的儲存體，就必須設定資產傳遞原則。</span><span class="sxs-lookup"><span data-stu-id="fe2a7-124">If your output asset is storage encrypted, you must configure the asset delivery policy.</span></span> <span data-ttu-id="fe2a7-125">如需詳細資訊，請參閱[設定資產傳遞原則](media-services-rest-configure-asset-delivery-policy.md)。</span><span class="sxs-lookup"><span data-stu-id="fe2a7-125">For more information, see [Configuring asset delivery policy](media-services-rest-configure-asset-delivery-policy.md).</span></span>

## <a name="considerations"></a><span data-ttu-id="fe2a7-126">考量</span><span class="sxs-lookup"><span data-stu-id="fe2a7-126">Considerations</span></span>

<span data-ttu-id="fe2a7-127">在媒體服務中存取實體時，您必須在 HTTP 要求中設定特定的標頭欄位和值。</span><span class="sxs-lookup"><span data-stu-id="fe2a7-127">When accessing entities in Media Services, you must set specific header fields and values in your HTTP requests.</span></span> <span data-ttu-id="fe2a7-128">如需詳細資訊，請參閱 [媒體服務 REST API 開發設定](media-services-rest-how-to-use.md)。</span><span class="sxs-lookup"><span data-stu-id="fe2a7-128">For more information, see [Setup for Media Services REST API Development](media-services-rest-how-to-use.md).</span></span>

<span data-ttu-id="fe2a7-129">開始參考媒體處理器之前，請確認您擁有正確的媒體處理器識別碼。</span><span class="sxs-lookup"><span data-stu-id="fe2a7-129">Before you start referencing media processors, verify that you have the correct media processor ID.</span></span> <span data-ttu-id="fe2a7-130">如需詳細資訊，請參閱[取得媒體處理器](media-services-rest-get-media-processor.md)。</span><span class="sxs-lookup"><span data-stu-id="fe2a7-130">For more information, see [Get media processors](media-services-rest-get-media-processor.md).</span></span>

## <a name="connect-to-media-services"></a><span data-ttu-id="fe2a7-131">連線到媒體服務</span><span class="sxs-lookup"><span data-stu-id="fe2a7-131">Connect to Media Services</span></span>

<span data-ttu-id="fe2a7-132">如需連線至 AMS API 的詳細資訊，請參閱[使用 Azure AD 驗證存取 Azure 媒體服務 API](media-services-use-aad-auth-to-access-ams-api.md)。</span><span class="sxs-lookup"><span data-stu-id="fe2a7-132">For information on how to connect to the AMS API, see [Access the Azure Media Services API with Azure AD authentication](media-services-use-aad-auth-to-access-ams-api.md).</span></span> 

>[!NOTE]
><span data-ttu-id="fe2a7-133">順利連接到 https://media.windows.net 之後，您會收到 301 重新導向，指定另一個媒體服務 URI。</span><span class="sxs-lookup"><span data-stu-id="fe2a7-133">After successfully connecting to https://media.windows.net, you will receive a 301 redirect specifying another Media Services URI.</span></span> <span data-ttu-id="fe2a7-134">後續的呼叫必須送到新的 URI。</span><span class="sxs-lookup"><span data-stu-id="fe2a7-134">You must make subsequent calls to the new URI.</span></span>

## <a name="create-a-job-with-a-single-encoding-task"></a><span data-ttu-id="fe2a7-135">建立具有單一編碼工作的工作</span><span class="sxs-lookup"><span data-stu-id="fe2a7-135">Create a job with a single encoding task</span></span>
> [!NOTE]
> <span data-ttu-id="fe2a7-136">使用媒體服務 REST API 時，適用下列考量事項：</span><span class="sxs-lookup"><span data-stu-id="fe2a7-136">When you're working with the Media Services REST API, the following considerations apply:</span></span>
>
> <span data-ttu-id="fe2a7-137">在媒體服務中存取實體時，您必須在 HTTP 要求中設定特定的標頭欄位和值。</span><span class="sxs-lookup"><span data-stu-id="fe2a7-137">When accessing entities in Media Services, you must set specific header fields and values in your HTTP requests.</span></span> <span data-ttu-id="fe2a7-138">如需詳細資訊，請參閱[媒體服務 REST API 開發設定](media-services-rest-how-to-use.md)。</span><span class="sxs-lookup"><span data-stu-id="fe2a7-138">For more information, see [Setup for Media Services REST API development](media-services-rest-how-to-use.md).</span></span>
>
> <span data-ttu-id="fe2a7-139">順利連接到 https://media.windows.net 之後，您會收到 301 重新導向，指定另一個媒體服務 URI。</span><span class="sxs-lookup"><span data-stu-id="fe2a7-139">After successfully connecting to https://media.windows.net, you will receive a 301 redirect specifying another Media Services URI.</span></span> <span data-ttu-id="fe2a7-140">後續的呼叫必須送到新的 URI。</span><span class="sxs-lookup"><span data-stu-id="fe2a7-140">You must make subsequent calls to the new URI.</span></span> <span data-ttu-id="fe2a7-141">如需連線至 AMS API 的詳細資訊，請參閱[使用 Azure AD 驗證存取 Azure 媒體服務 API](media-services-use-aad-auth-to-access-ams-api.md)。</span><span class="sxs-lookup"><span data-stu-id="fe2a7-141">For information on how to connect to the AMS API, see [Access the Azure Media Services API with Azure AD authentication](media-services-use-aad-auth-to-access-ams-api.md).</span></span>
>
> <span data-ttu-id="fe2a7-142">使用 JSON 並指定在要求中使用 **__metadata** 關鍵字時 (例如，為了參考連結的物件)，您必須將 **Accept** 標頭設為 [JSON Verbose 格式 (英文)](http://www.odata.org/documentation/odata-version-3-0/json-verbose-format/)：Accept: application/json;odata=verbose。</span><span class="sxs-lookup"><span data-stu-id="fe2a7-142">When using JSON and specifying to use the **__metadata** keyword in the request (for example, to references a linked object), you must set the **Accept** header to [JSON Verbose format](http://www.odata.org/documentation/odata-version-3-0/json-verbose-format/): Accept: application/json;odata=verbose.</span></span>
>
>

<span data-ttu-id="fe2a7-143">下列範例示範如何建立和張貼含有一個工作的作業，並將該工作設定為以特定的解析度與品質來為視訊編碼。</span><span class="sxs-lookup"><span data-stu-id="fe2a7-143">The following example shows you how to create and post a job with one task set to encode a video at a specific resolution and quality.</span></span> <span data-ttu-id="fe2a7-144">透過媒體編碼器標準進行編碼時，您可以使用 [這裡](http://msdn.microsoft.com/library/mt269960)指定的工作組態預設。</span><span class="sxs-lookup"><span data-stu-id="fe2a7-144">When you encode with Media Encoder Standard, you can use task configuration presets specified [here](http://msdn.microsoft.com/library/mt269960).</span></span>

<span data-ttu-id="fe2a7-145">要求：</span><span class="sxs-lookup"><span data-stu-id="fe2a7-145">Request:</span></span>

    POST https://media.windows.net/API/Jobs HTTP/1.1
    Content-Type: application/json;odata=verbose
    Accept: application/json;odata=verbose
    DataServiceVersion: 3.0
    MaxDataServiceVersion: 3.0
    x-ms-version: 2.11
    Authorization: Bearer <token value>
    x-ms-client-request-id: 00000000-0000-0000-0000-000000000000
    Host: media.windows.net

    {"Name" : "NewTestJob", "InputMediaAssets" : [{"__metadata" : {"uri" : "https://media.windows.net/api/Assets('nb%3Acid%3AUUID%3Aaab7f15b-3136-4ddf-9962-e9ecb28fb9d2')"}}],  "Tasks" : [{"Configuration" : "Adaptive Streaming", "MediaProcessorId" : "nb:mpid:UUID:ff4df607-d419-42f0-bc17-a481b1331e56",  "TaskBody" : "<?xml version=\"1.0\" encoding=\"utf-8\"?><taskBody><inputAsset>JobInputAsset(0)</inputAsset><outputAsset>JobOutputAsset(0)</outputAsset></taskBody>"}]}

<span data-ttu-id="fe2a7-146">回應：</span><span class="sxs-lookup"><span data-stu-id="fe2a7-146">Response:</span></span>

    HTTP/1.1 201 Created

    . . .

### <a name="set-the-output-assets-name"></a><span data-ttu-id="fe2a7-147">設定輸出資產的名稱</span><span class="sxs-lookup"><span data-stu-id="fe2a7-147">Set the output asset's name</span></span>
<span data-ttu-id="fe2a7-148">下列範例示範如何設定 assetName 屬性：</span><span class="sxs-lookup"><span data-stu-id="fe2a7-148">The following example shows how to set the assetName attribute:</span></span>

    { "TaskBody" : "<?xml version=\"1.0\" encoding=\"utf-8\"?><taskBody><inputAsset>JobInputAsset(0)</inputAsset><outputAsset assetName=\"CustomOutputAssetName\">JobOutputAsset(0)</outputAsset></taskBody>"}

## <a name="considerations"></a><span data-ttu-id="fe2a7-149">考量</span><span class="sxs-lookup"><span data-stu-id="fe2a7-149">Considerations</span></span>
* <span data-ttu-id="fe2a7-150">TaskBody 屬性必須使用 XML 常值，來定義工作所使用的輸入或輸出資產數目。</span><span class="sxs-lookup"><span data-stu-id="fe2a7-150">TaskBody properties must use literal XML to define the number of input, or output assets that are used by the task.</span></span> <span data-ttu-id="fe2a7-151">工作主題包含 XML 的 XML 結構描述定義。</span><span class="sxs-lookup"><span data-stu-id="fe2a7-151">The task topic contains the XML Schema Definition for the XML.</span></span>
* <span data-ttu-id="fe2a7-152">在 TaskBody 定義中，<inputAsset> 和 <outputAsset> 的每一個內部值必須設定為 JobInputAsset(value) 或 JobOutputAsset(value)。</span><span class="sxs-lookup"><span data-stu-id="fe2a7-152">In the TaskBody definition, each inner value for <inputAsset> and <outputAsset> must be set as JobInputAsset(value) or JobOutputAsset(value).</span></span>
* <span data-ttu-id="fe2a7-153">每個工作可以有多個輸出資產。</span><span class="sxs-lookup"><span data-stu-id="fe2a7-153">A task can have multiple output assets.</span></span> <span data-ttu-id="fe2a7-154">一個 JobOutputAsset(x) 只能使用一次做為工作中的工作輸出。</span><span class="sxs-lookup"><span data-stu-id="fe2a7-154">One JobOutputAsset(x) can only be used once as an output of a task in a job.</span></span>
* <span data-ttu-id="fe2a7-155">您可以指定 JobInputAsset 或 JobOutputAsset 做為工作的輸入資產。</span><span class="sxs-lookup"><span data-stu-id="fe2a7-155">You can specify JobInputAsset or JobOutputAsset as an input asset of a task.</span></span>
* <span data-ttu-id="fe2a7-156">工作不能形成循環。</span><span class="sxs-lookup"><span data-stu-id="fe2a7-156">Tasks must not form a cycle.</span></span>
* <span data-ttu-id="fe2a7-157">您傳遞至 JobInputAsset 或 JobOutputAsset 的 value 參數代表資產的索引值。</span><span class="sxs-lookup"><span data-stu-id="fe2a7-157">The value parameter that you pass to JobInputAsset or JobOutputAsset represents the index value for an asset.</span></span> <span data-ttu-id="fe2a7-158">實際的資產定義於作業實體定義上的 InputMediaAsset 與 OutputMediaAsset 導覽屬性中。</span><span class="sxs-lookup"><span data-stu-id="fe2a7-158">The actual assets are defined in the InputMediaAssets and OutputMediaAssets navigation properties on the job entity definition.</span></span>
* <span data-ttu-id="fe2a7-159">由於媒體服務建置在 OData v3 之上，因此，會透過 "__metadata : uri" 名稱/值組來參考 InputMediaAsset 與 OutputMediaAsset 導覽屬性集合中的個別資產。</span><span class="sxs-lookup"><span data-stu-id="fe2a7-159">Because Media Services is built on OData v3, the individual assets in the InputMediaAssets and OutputMediaAssets navigation property collections are referenced through a "__metadata : uri" name-value pair.</span></span>
* <span data-ttu-id="fe2a7-160">InputMediaAsset 對應至您在媒體服務中建立的一或多個資產。</span><span class="sxs-lookup"><span data-stu-id="fe2a7-160">InputMediaAssets maps to one or more assets that you created in Media Services.</span></span> <span data-ttu-id="fe2a7-161">OutputMediaAsset 由系統建立。</span><span class="sxs-lookup"><span data-stu-id="fe2a7-161">OutputMediaAssets are created by the system.</span></span> <span data-ttu-id="fe2a7-162">它們不會參考現有的資產。</span><span class="sxs-lookup"><span data-stu-id="fe2a7-162">They don't reference an existing asset.</span></span>
* <span data-ttu-id="fe2a7-163">OutputMediaAsset 可以使用 assetName 屬性來命名。</span><span class="sxs-lookup"><span data-stu-id="fe2a7-163">OutputMediaAssets can be named by using the assetName attribute.</span></span> <span data-ttu-id="fe2a7-164">如果這個屬性不存在，則 OutputMediaAsset 的名稱是 <outputAsset> 元素的任何內部文字值，並且尾碼為工作名稱值或工作識別碼值 (在未定義 Name 屬性的情況下)。</span><span class="sxs-lookup"><span data-stu-id="fe2a7-164">If this attribute is not present, then the name of the OutputMediaAsset is whatever the inner text value of the <outputAsset> element is with a suffix of either the Job Name value, or the Job Id value (in the case where the Name property isn't defined).</span></span> <span data-ttu-id="fe2a7-165">例如，如果您將 assetName 的值設為 "Sample"，則會將 OutputMediaAsset Name 屬性設為 "Sample"。</span><span class="sxs-lookup"><span data-stu-id="fe2a7-165">For example, if you set a value for assetName to "Sample," then the OutputMediaAsset Name property is set to "Sample."</span></span> <span data-ttu-id="fe2a7-166">不過，如果您未設定 assetName 的值，但已將作業名稱設為 "NewJob"，則 OutputMediaAsset Name 會是 "JobOutputAsset(value)_NewJob"。</span><span class="sxs-lookup"><span data-stu-id="fe2a7-166">However, if you didn't set a value for assetName, but did set the job name to "NewJob," then the OutputMediaAsset Name would be "JobOutputAsset(value)_NewJob."</span></span>

## <a name="create-a-job-with-chained-tasks"></a><span data-ttu-id="fe2a7-167">建立具有鏈結工作的工作</span><span class="sxs-lookup"><span data-stu-id="fe2a7-167">Create a job with chained tasks</span></span>
<span data-ttu-id="fe2a7-168">在許多應用程式案例中，開發人員想要建立一連串的處理工作。</span><span class="sxs-lookup"><span data-stu-id="fe2a7-168">In many application scenarios, developers want to create a series of processing tasks.</span></span> <span data-ttu-id="fe2a7-169">在媒體服務中，您可以建立一連串的鏈結工作。</span><span class="sxs-lookup"><span data-stu-id="fe2a7-169">In Media Services, you can create a series of chained tasks.</span></span> <span data-ttu-id="fe2a7-170">每一項工作會執行不同的處理步驟，而且可以使用不同的媒體處理器。</span><span class="sxs-lookup"><span data-stu-id="fe2a7-170">Each task performs different processing steps and can use different media processors.</span></span> <span data-ttu-id="fe2a7-171">鏈結工作可以將資產從一個工作遞交到另一個工作，對資產執行一連串的工作。</span><span class="sxs-lookup"><span data-stu-id="fe2a7-171">The chained tasks can hand off an asset from one task to another, performing a linear sequence of tasks on the asset.</span></span> <span data-ttu-id="fe2a7-172">不過，在工作中執行的工作不必按照順序。</span><span class="sxs-lookup"><span data-stu-id="fe2a7-172">However, the tasks performed in a job are not required to be in a sequence.</span></span> <span data-ttu-id="fe2a7-173">當您建立鏈結工作時，鏈結的 **ITask** 物件會建立在單一 **IJob** 物件中。</span><span class="sxs-lookup"><span data-stu-id="fe2a7-173">When you create a chained task, the chained **ITask** objects are created in a single **IJob** object.</span></span>

> [!NOTE]
> <span data-ttu-id="fe2a7-174">目前有每個工作裡 30 個工作的限制。</span><span class="sxs-lookup"><span data-stu-id="fe2a7-174">There is currently a limit of 30 tasks per job.</span></span> <span data-ttu-id="fe2a7-175">如果您需要鏈結超過 30 個工作，請建立多個工作來包含這些工作。</span><span class="sxs-lookup"><span data-stu-id="fe2a7-175">If you need to chain more than 30 tasks, create more than one job to contain the tasks.</span></span>
>
>

    POST https://media.windows.net/api/Jobs HTTP/1.1
    Content-Type: application/json;odata=verbose
    Accept: application/json;odata=verbose
    DataServiceVersion: 3.0
    MaxDataServiceVersion: 3.0
    x-ms-version: 2.11
    Authorization: Bearer <token value>
    x-ms-client-request-id: 00000000-0000-0000-0000-000000000000

    {  
       "Name":"NewTestJob",
       "InputMediaAssets":[  
          {  
             "__metadata":{  
                "uri":"https://testrest.cloudapp.net/api/Assets('nb%3Acid%3AUUID%3A910ffdc1-2e25-4b17-8a42-61ffd4b8914c')"
             }
          }
       ],
       "Tasks":[  
          {  
             "Configuration":"H264 Adaptive Bitrate MP4 Set 720p",
             "MediaProcessorId":"nb:mpid:UUID:ff4df607-d419-42f0-bc17-a481b1331e56",
             "TaskBody":"<?xml version=\"1.0\" encoding=\"utf-8\"?><taskBody><inputAsset>JobInputAsset(0)</inputAsset><outputAsset>JobOutputAsset(0)</outputAsset></taskBody>"
          },
          {  
             "Configuration":"H264 Smooth Streaming 720p",
             "MediaProcessorId":"nb:mpid:UUID:ff4df607-d419-42f0-bc17-a481b1331e56",
             "TaskBody":"<?xml version=\"1.0\" encoding=\"utf-16\"?><taskBody><inputAsset>JobOutputAsset(0)</inputAsset><outputAsset>JobOutputAsset(1)</outputAsset></taskBody>"
          }
       ]
    }


### <a name="considerations"></a><span data-ttu-id="fe2a7-176">考量</span><span class="sxs-lookup"><span data-stu-id="fe2a7-176">Considerations</span></span>
<span data-ttu-id="fe2a7-177">啟用工作鏈結：</span><span class="sxs-lookup"><span data-stu-id="fe2a7-177">To enable task chaining:</span></span>

* <span data-ttu-id="fe2a7-178">一個作業至少必須有 2 個工作。</span><span class="sxs-lookup"><span data-stu-id="fe2a7-178">A job must have at least two tasks.</span></span>
* <span data-ttu-id="fe2a7-179">至少必須有一個工作的輸入是作業中另一個工作的輸出。</span><span class="sxs-lookup"><span data-stu-id="fe2a7-179">There must be at least one task whose input is the output of another task in the job.</span></span>

## <a name="use-odata-batch-processing"></a><span data-ttu-id="fe2a7-180">使用 OData 批次處理</span><span class="sxs-lookup"><span data-stu-id="fe2a7-180">Use OData batch processing</span></span>
<span data-ttu-id="fe2a7-181">以下範例示範如何使用 OData 批次處理來建立工作和作業。</span><span class="sxs-lookup"><span data-stu-id="fe2a7-181">The following example shows how to use OData batch processing to create a job and tasks.</span></span> <span data-ttu-id="fe2a7-182">如需批次處理的資訊，請參閱 [開放式資料通訊協定 (OData) 批次處理](http://www.odata.org/documentation/odata-version-3-0/batch-processing/)。</span><span class="sxs-lookup"><span data-stu-id="fe2a7-182">For information on batch processing, see [Open Data Protocol (OData) Batch Processing](http://www.odata.org/documentation/odata-version-3-0/batch-processing/).</span></span>

    POST https://media.windows.net/api/$batch HTTP/1.1
    DataServiceVersion: 1.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Content-Type: multipart/mixed; boundary=batch_a01a5ec4-ba0f-4536-84b5-66c5a5a6d34e
    Accept: multipart/mixed
    Accept-Charset: UTF-8
    Authorization: Bearer <token>
    x-ms-version: 2.11
    x-ms-client-request-id: 00000000-0000-0000-0000-000000000000
    Host: media.windows.net


    --batch_a01a5ec4-ba0f-4536-84b5-66c5a5a6d34e
    Content-Type: multipart/mixed; boundary=changeset_122fb0a4-cd80-4958-820f-346309967e4d

    --changeset_122fb0a4-cd80-4958-820f-346309967e4d
    Content-Type: application/http
    Content-Transfer-Encoding: binary

    POST https://media.windows.net/api/Jobs HTTP/1.1
    Content-ID: 1
    Content-Type: application/json
    Accept: application/json
    DataServiceVersion: 3.0
    MaxDataServiceVersion: 3.0
    Accept-Charset: UTF-8
    Authorization: Bearer <token>
    x-ms-version: 2.11
    x-ms-client-request-id: 00000000-0000-0000-0000-000000000000

    {"Name" : "NewTestJob", "InputMediaAssets@odata.bind":["https://media.windows.net/api/Assets('nb%3Acid%3AUUID%3A2a22445d-1500-80c6-4b34-f1e5190d33c6')"]}

    --changeset_122fb0a4-cd80-4958-820f-346309967e4d
    Content-Type: application/http
    Content-Transfer-Encoding: binary

    POST https://media.windows.net/api/$1/Tasks HTTP/1.1
    Content-ID: 2
    Content-Type: application/json;odata=verbose
    Accept: application/json;odata=verbose
    DataServiceVersion: 3.0
    MaxDataServiceVersion: 3.0
    Accept-Charset: UTF-8
    Authorization: Bearer <token>
    x-ms-version: 2.11
    x-ms-client-request-id: 00000000-0000-0000-0000-000000000000

    {  
       "Configuration":"H264 Adaptive Bitrate MP4 Set 720p",
       "MediaProcessorId":"nb:mpid:UUID:ff4df607-d419-42f0-bc17-a481b1331e56",
       "TaskBody":"<?xml version=\"1.0\" encoding=\"utf-8\"?><taskBody><inputAsset>JobInputAsset(0)</inputAsset><outputAsset assetName=\"Custom output name\">JobOutputAsset(0)</outputAsset></taskBody>"
    }

    --changeset_122fb0a4-cd80-4958-820f-346309967e4d--
    --batch_a01a5ec4-ba0f-4536-84b5-66c5a5a6d34e--



## <a name="create-a-job-by-using-a-jobtemplate"></a><span data-ttu-id="fe2a7-183">使用 JobTemplate 建立作業</span><span class="sxs-lookup"><span data-stu-id="fe2a7-183">Create a job by using a JobTemplate</span></span>
<span data-ttu-id="fe2a7-184">使用一組常用的工作來處理多個資產時，請使用 JobTemplates 來指定預設的工作預設或設定工作順序。</span><span class="sxs-lookup"><span data-stu-id="fe2a7-184">When you process multiple assets by using a common set of tasks, use a JobTemplate to specify the default task presets, or to set the order of tasks.</span></span>

<span data-ttu-id="fe2a7-185">下列範例示範如何使用以內嵌方式定義的 TaskTemplate 來建立 JobTemplate。</span><span class="sxs-lookup"><span data-stu-id="fe2a7-185">The following example shows how to create a JobTemplate with a TaskTemplate that is defined inline.</span></span> <span data-ttu-id="fe2a7-186">TaskTemplate 使用媒體編碼器標準作為 MediaProcessor 來為資產檔案編碼。</span><span class="sxs-lookup"><span data-stu-id="fe2a7-186">The TaskTemplate uses the Media Encoder Standard as the MediaProcessor to encode the asset file.</span></span> <span data-ttu-id="fe2a7-187">但是，也可以使用其他 MediaProcessor。</span><span class="sxs-lookup"><span data-stu-id="fe2a7-187">However, other MediaProcessors can be used as well.</span></span>

    POST https://media.windows.net/API/JobTemplates HTTP/1.1
    Content-Type: application/json;odata=verbose
    Accept: application/json;odata=verbose
    DataServiceVersion: 3.0
    MaxDataServiceVersion: 3.0
    x-ms-version: 2.11
    Authorization: Bearer <token value>
    Host: media.windows.net


    {"Name" : "NewJobTemplate25", "JobTemplateBody" : "<?xml version=\"1.0\" encoding=\"utf-8\"?><jobTemplate><taskBody taskTemplateId=\"nb:ttid:UUID:071370A3-E63E-4E81-A099-AD66BCAC3789\"><inputAsset>JobInputAsset(0)</inputAsset><outputAsset>JobOutputAsset(0)</outputAsset></taskBody></jobTemplate>", "TaskTemplates" : [{"Id" : "nb:ttid:UUID:071370A3-E63E-4E81-A099-AD66BCAC3789", "Configuration" : "H264 Smooth Streaming 720p", "MediaProcessorId" : "nb:mpid:UUID:ff4df607-d419-42f0-bc17-a481b1331e56", "Name" : "SampleTaskTemplate2", "NumberofInputAssets" : 1, "NumberofOutputAssets" : 1}] }


> [!NOTE]
> <span data-ttu-id="fe2a7-188">與其他媒體服務實體不同的是，您必須為每個 TaskTemplate 定義新的 GUID 識別碼，並將它置入 taskTemplateId，以及在您的要求本文中置入識別碼屬性。</span><span class="sxs-lookup"><span data-stu-id="fe2a7-188">Unlike other Media Services entities, you must define a new GUID identifier for each TaskTemplate and place it in the taskTemplateId and Id property in your request body.</span></span> <span data-ttu-id="fe2a7-189">內容識別配置必須遵循「識別 Azure 媒體服務實體」中所述的配置。</span><span class="sxs-lookup"><span data-stu-id="fe2a7-189">The content identification scheme must follow the scheme described in Identify Azure Media Services Entities.</span></span> <span data-ttu-id="fe2a7-190">而且，不能更新 JobTemplate。</span><span class="sxs-lookup"><span data-stu-id="fe2a7-190">Also, JobTemplates cannot be updated.</span></span> <span data-ttu-id="fe2a7-191">相反地，您必須使用更新後的變更建立一個新的 JobTemplate。</span><span class="sxs-lookup"><span data-stu-id="fe2a7-191">Instead, you must create a new one with your updated changes.</span></span>
>
>

<span data-ttu-id="fe2a7-192">如果成功，則會傳回下列回應：</span><span class="sxs-lookup"><span data-stu-id="fe2a7-192">If successful, the following response is returned:</span></span>

    HTTP/1.1 201 Created

    . . .


<span data-ttu-id="fe2a7-193">下列範例示範如何建立參考 JobTemplate 識別碼的作業：</span><span class="sxs-lookup"><span data-stu-id="fe2a7-193">The following example shows how to create a job that references a JobTemplate Id:</span></span>

    POST https://media.windows.net/API/Jobs HTTP/1.1
    Content-Type: application/json;odata=verbose
    Accept: application/json;odata=verbose
    DataServiceVersion: 3.0
    MaxDataServiceVersion: 3.0
    x-ms-version: 2.11
    Authorization: Bearer <token value>
    Host: media.windows.net


    {"Name" : "NewTestJob", "InputMediaAssets" : [{"__metadata" : {"uri" : "https://media.windows.net/api/Assets('nb%3Acid%3AUUID%3A3f1fe4a2-68f5-4190-9557-cd45beccef92')"}}], "TemplateId" : "nb:jtid:UUID:15e6e5e6-ac85-084e-9dc2-db3645fbf0aa"}


<span data-ttu-id="fe2a7-194">如果成功，則會傳回下列回應：</span><span class="sxs-lookup"><span data-stu-id="fe2a7-194">If successful, the following response is returned:</span></span>

    HTTP/1.1 201 Created

    . . .



## <a name="media-services-learning-paths"></a><span data-ttu-id="fe2a7-195">媒體服務學習路徑</span><span class="sxs-lookup"><span data-stu-id="fe2a7-195">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="fe2a7-196">提供意見反應</span><span class="sxs-lookup"><span data-stu-id="fe2a7-196">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="next-steps"></a><span data-ttu-id="fe2a7-197">後續步驟</span><span class="sxs-lookup"><span data-stu-id="fe2a7-197">Next steps</span></span>
<span data-ttu-id="fe2a7-198">現在您已了解如何建立作業來為資產編碼，請參閱[如何使用媒體服務檢查作業進度](media-services-rest-check-job-progress.md)。</span><span class="sxs-lookup"><span data-stu-id="fe2a7-198">Now that you know how to create a job to encode an asset, see [How to check job progress with Media Services](media-services-rest-check-job-progress.md).</span></span>

## <a name="see-also"></a><span data-ttu-id="fe2a7-199">另請參閱</span><span class="sxs-lookup"><span data-stu-id="fe2a7-199">See also</span></span>
[<span data-ttu-id="fe2a7-200">取得媒體處理器</span><span class="sxs-lookup"><span data-stu-id="fe2a7-200">Get Media Processors</span></span>](media-services-rest-get-media-processor.md)
