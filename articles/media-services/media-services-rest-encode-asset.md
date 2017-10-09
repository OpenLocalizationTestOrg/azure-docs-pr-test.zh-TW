---
title: "aaaHow tooencode 使用標準的媒體編碼器 Azure 資產 |Microsoft 文件"
description: "了解如何 toouse 媒體編碼器標準 tooencode 媒體內容上 Azure Media Services。 程式碼範例會使用 REST API。"
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
ms.openlocfilehash: b766bafded7ee98eda3e6ef149c31d5d8fe406fc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooencode-an-asset-by-using-media-encoder-standard"></a><span data-ttu-id="fe00b-104">如何使用媒體編碼器標準資產 tooencode</span><span class="sxs-lookup"><span data-stu-id="fe00b-104">How tooencode an asset by using Media Encoder Standard</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="fe00b-105">.NET</span><span class="sxs-lookup"><span data-stu-id="fe00b-105">.NET</span></span>](media-services-dotnet-encode-with-media-encoder-standard.md)
> * [<span data-ttu-id="fe00b-106">REST</span><span class="sxs-lookup"><span data-stu-id="fe00b-106">REST</span></span>](media-services-rest-encode-asset.md)
> * [<span data-ttu-id="fe00b-107">入口網站</span><span class="sxs-lookup"><span data-stu-id="fe00b-107">Portal</span></span>](media-services-portal-encode.md)
>
>

## <a name="overview"></a><span data-ttu-id="fe00b-108">概觀</span><span class="sxs-lookup"><span data-stu-id="fe00b-108">Overview</span></span>
<span data-ttu-id="fe00b-109">toodeliver hello 網際網路上的數位視訊，您必須壓縮 hello 媒體。</span><span class="sxs-lookup"><span data-stu-id="fe00b-109">toodeliver digital video over hello Internet, you must compress hello media.</span></span> <span data-ttu-id="fe00b-110">數位視訊檔案很大，而且可能會太大 toodeliver 透過 hello 網際網路，或基於您的客戶裝置 toodisplay 正確。</span><span class="sxs-lookup"><span data-stu-id="fe00b-110">Digital video files are large and may be too big toodeliver over hello Internet, or for your customers’ devices toodisplay properly.</span></span> <span data-ttu-id="fe00b-111">編碼是壓縮視訊和音訊，使您的客戶可以檢視您的媒體 hello 程序。</span><span class="sxs-lookup"><span data-stu-id="fe00b-111">Encoding is hello process of compressing video and audio so your customers can view your media.</span></span>

<span data-ttu-id="fe00b-112">編碼工作是在 Azure Media Services hello 大多數處理作業。</span><span class="sxs-lookup"><span data-stu-id="fe00b-112">Encoding jobs are one of hello most common processing operations in Azure Media Services.</span></span> <span data-ttu-id="fe00b-113">您從一個編碼 tooanother 建立編碼工作 tooconvert 媒體檔案。</span><span class="sxs-lookup"><span data-stu-id="fe00b-113">You create encoding jobs tooconvert media files from one encoding tooanother.</span></span> <span data-ttu-id="fe00b-114">當編碼時，您可以使用 hello Media Services 內建編碼器 （媒體編碼器標準）。</span><span class="sxs-lookup"><span data-stu-id="fe00b-114">When you encode, you can use hello Media Services built-in encoder (Media Encoder Standard).</span></span> <span data-ttu-id="fe00b-115">您也可以使用媒體服務合作夥伴所提供的編碼器。</span><span class="sxs-lookup"><span data-stu-id="fe00b-115">You can also use an encoder provided by a Media Services partner.</span></span> <span data-ttu-id="fe00b-116">第三方編碼器皆可透過 hello Azure Marketplace。</span><span class="sxs-lookup"><span data-stu-id="fe00b-116">Third-party encoders are available through hello Azure Marketplace.</span></span> <span data-ttu-id="fe00b-117">您可以指定 hello 的編碼工作，使用針對您的編碼器定義的預設的字串，或使用預設的組態檔的詳細資料。</span><span class="sxs-lookup"><span data-stu-id="fe00b-117">You can specify hello details of encoding tasks by using preset strings defined for your encoder, or by using preset configuration files.</span></span> <span data-ttu-id="fe00b-118">toosee hello 類型的預設值可供使用，請參閱[的媒體編碼器標準工作預設](http://msdn.microsoft.com/library/mt269960)。</span><span class="sxs-lookup"><span data-stu-id="fe00b-118">toosee hello types of presets that are available, see [Task Presets for Media Encoder Standard](http://msdn.microsoft.com/library/mt269960).</span></span>

<span data-ttu-id="fe00b-119">每個工作可以有一個或更多的工作，根據 hello 類型處理您想 tooaccomplish。</span><span class="sxs-lookup"><span data-stu-id="fe00b-119">Each job can have one or more tasks depending on hello type of processing that you want tooaccomplish.</span></span> <span data-ttu-id="fe00b-120">透過 hello REST API，您可以建立工作和其相關的工作中有兩種：</span><span class="sxs-lookup"><span data-stu-id="fe00b-120">Through hello REST API, you can create jobs and their related tasks in one of two ways:</span></span>

* <span data-ttu-id="fe00b-121">工作可以透過工作項目上的 hello 工作導覽屬性的內嵌定義。</span><span class="sxs-lookup"><span data-stu-id="fe00b-121">Tasks can be defined inline through hello Tasks navigation property on Job entities.</span></span>
* <span data-ttu-id="fe00b-122">使用 OData 批次處理。</span><span class="sxs-lookup"><span data-stu-id="fe00b-122">Use OData batch processing.</span></span>

<span data-ttu-id="fe00b-123">我們建議您一律將原始程式檔編碼成彈性位元速率 MP4 集，並使用，以轉換 hello 集 toohello 所需的格式[動態封裝](media-services-dynamic-packaging-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="fe00b-123">We recommend that you always encode your source files into an adaptive bitrate MP4 set, and then convert hello set toohello desired format by using [dynamic packaging](media-services-dynamic-packaging-overview.md).</span></span>

<span data-ttu-id="fe00b-124">如果輸出資產是儲存體加密，您必須設定 hello 資產傳遞原則。</span><span class="sxs-lookup"><span data-stu-id="fe00b-124">If your output asset is storage encrypted, you must configure hello asset delivery policy.</span></span> <span data-ttu-id="fe00b-125">如需詳細資訊，請參閱[設定資產傳遞原則](media-services-rest-configure-asset-delivery-policy.md)。</span><span class="sxs-lookup"><span data-stu-id="fe00b-125">For more information, see [Configuring asset delivery policy](media-services-rest-configure-asset-delivery-policy.md).</span></span>

## <a name="considerations"></a><span data-ttu-id="fe00b-126">考量</span><span class="sxs-lookup"><span data-stu-id="fe00b-126">Considerations</span></span>

<span data-ttu-id="fe00b-127">在媒體服務中存取實體時，您必須在 HTTP 要求中設定特定的標頭欄位和值。</span><span class="sxs-lookup"><span data-stu-id="fe00b-127">When accessing entities in Media Services, you must set specific header fields and values in your HTTP requests.</span></span> <span data-ttu-id="fe00b-128">如需詳細資訊，請參閱 [媒體服務 REST API 開發設定](media-services-rest-how-to-use.md)。</span><span class="sxs-lookup"><span data-stu-id="fe00b-128">For more information, see [Setup for Media Services REST API Development](media-services-rest-how-to-use.md).</span></span>

<span data-ttu-id="fe00b-129">您可以啟動參考媒體處理器之前，請確認您擁有 hello 正確的媒體處理器的識別碼。</span><span class="sxs-lookup"><span data-stu-id="fe00b-129">Before you start referencing media processors, verify that you have hello correct media processor ID.</span></span> <span data-ttu-id="fe00b-130">如需詳細資訊，請參閱[取得媒體處理器](media-services-rest-get-media-processor.md)。</span><span class="sxs-lookup"><span data-stu-id="fe00b-130">For more information, see [Get media processors](media-services-rest-get-media-processor.md).</span></span>

## <a name="connect-toomedia-services"></a><span data-ttu-id="fe00b-131">TooMedia 服務連接</span><span class="sxs-lookup"><span data-stu-id="fe00b-131">Connect tooMedia Services</span></span>

<span data-ttu-id="fe00b-132">如需有關如何 tooconnect toohello AMS API，請參閱詳細[存取 hello Azure 媒體服務 API 與 Azure AD 驗證](media-services-use-aad-auth-to-access-ams-api.md)。</span><span class="sxs-lookup"><span data-stu-id="fe00b-132">For information on how tooconnect toohello AMS API, see [Access hello Azure Media Services API with Azure AD authentication](media-services-use-aad-auth-to-access-ams-api.md).</span></span> 

>[!NOTE]
><span data-ttu-id="fe00b-133">已成功連接之後 toohttps://media.windows.net，您會收到指定另一個媒體服務 URI 的 301 重新導向。</span><span class="sxs-lookup"><span data-stu-id="fe00b-133">After successfully connecting toohttps://media.windows.net, you will receive a 301 redirect specifying another Media Services URI.</span></span> <span data-ttu-id="fe00b-134">您必須進行的後續呼叫 toohello 新的 URI。</span><span class="sxs-lookup"><span data-stu-id="fe00b-134">You must make subsequent calls toohello new URI.</span></span>

## <a name="create-a-job-with-a-single-encoding-task"></a><span data-ttu-id="fe00b-135">建立具有單一編碼工作的工作</span><span class="sxs-lookup"><span data-stu-id="fe00b-135">Create a job with a single encoding task</span></span>
> [!NOTE]
> <span data-ttu-id="fe00b-136">當您使用以 hello 媒體服務 REST API 時，hello 適用下列考量：</span><span class="sxs-lookup"><span data-stu-id="fe00b-136">When you're working with hello Media Services REST API, hello following considerations apply:</span></span>
>
> <span data-ttu-id="fe00b-137">在媒體服務中存取實體時，您必須在 HTTP 要求中設定特定的標頭欄位和值。</span><span class="sxs-lookup"><span data-stu-id="fe00b-137">When accessing entities in Media Services, you must set specific header fields and values in your HTTP requests.</span></span> <span data-ttu-id="fe00b-138">如需詳細資訊，請參閱[媒體服務 REST API 開發設定](media-services-rest-how-to-use.md)。</span><span class="sxs-lookup"><span data-stu-id="fe00b-138">For more information, see [Setup for Media Services REST API development](media-services-rest-how-to-use.md).</span></span>
>
> <span data-ttu-id="fe00b-139">已成功連接之後 toohttps://media.windows.net，您會收到指定另一個媒體服務 URI 的 301 重新導向。</span><span class="sxs-lookup"><span data-stu-id="fe00b-139">After successfully connecting toohttps://media.windows.net, you will receive a 301 redirect specifying another Media Services URI.</span></span> <span data-ttu-id="fe00b-140">您必須進行的後續呼叫 toohello 新的 URI。</span><span class="sxs-lookup"><span data-stu-id="fe00b-140">You must make subsequent calls toohello new URI.</span></span> <span data-ttu-id="fe00b-141">如需有關如何 tooconnect toohello AMS API，請參閱詳細[存取 hello Azure 媒體服務 API 與 Azure AD 驗證](media-services-use-aad-auth-to-access-ams-api.md)。</span><span class="sxs-lookup"><span data-stu-id="fe00b-141">For information on how tooconnect toohello AMS API, see [Access hello Azure Media Services API with Azure AD authentication](media-services-use-aad-auth-to-access-ams-api.md).</span></span>
>
> <span data-ttu-id="fe00b-142">當使用 JSON，並指定 toouse hello **__metadata**關鍵字 hello 要求 (例如，tooreferences 連結物件)，您必須設定 hello**接受**標頭太[詳細資訊 JSON 格式](http://www.odata.org/documentation/odata-version-3-0/json-verbose-format/)： 接受： 應用程式/json; odata = 詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="fe00b-142">When using JSON and specifying toouse hello **__metadata** keyword in hello request (for example, tooreferences a linked object), you must set hello **Accept** header too[JSON Verbose format](http://www.odata.org/documentation/odata-version-3-0/json-verbose-format/): Accept: application/json;odata=verbose.</span></span>
>
>

<span data-ttu-id="fe00b-143">hello 下列範例會示範如何 toocreate 和 post 作業的一項工作設定 tooencode 視訊在特定的解析度與品質。</span><span class="sxs-lookup"><span data-stu-id="fe00b-143">hello following example shows you how toocreate and post a job with one task set tooencode a video at a specific resolution and quality.</span></span> <span data-ttu-id="fe00b-144">透過媒體編碼器標準進行編碼時，您可以使用 [這裡](http://msdn.microsoft.com/library/mt269960)指定的工作組態預設。</span><span class="sxs-lookup"><span data-stu-id="fe00b-144">When you encode with Media Encoder Standard, you can use task configuration presets specified [here](http://msdn.microsoft.com/library/mt269960).</span></span>

<span data-ttu-id="fe00b-145">要求：</span><span class="sxs-lookup"><span data-stu-id="fe00b-145">Request:</span></span>

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

<span data-ttu-id="fe00b-146">回應：</span><span class="sxs-lookup"><span data-stu-id="fe00b-146">Response:</span></span>

    HTTP/1.1 201 Created

    . . .

### <a name="set-hello-output-assets-name"></a><span data-ttu-id="fe00b-147">設定 hello 輸出資產的名稱</span><span class="sxs-lookup"><span data-stu-id="fe00b-147">Set hello output asset's name</span></span>
<span data-ttu-id="fe00b-148">hello 下列範例顯示如何 tooset hello assetName 屬性：</span><span class="sxs-lookup"><span data-stu-id="fe00b-148">hello following example shows how tooset hello assetName attribute:</span></span>

    { "TaskBody" : "<?xml version=\"1.0\" encoding=\"utf-8\"?><taskBody><inputAsset>JobInputAsset(0)</inputAsset><outputAsset assetName=\"CustomOutputAssetName\">JobOutputAsset(0)</outputAsset></taskBody>"}

## <a name="considerations"></a><span data-ttu-id="fe00b-149">考量</span><span class="sxs-lookup"><span data-stu-id="fe00b-149">Considerations</span></span>
* <span data-ttu-id="fe00b-150">TaskBody 屬性必須使用常值的輸入或輸出資產 hello 工作所使用 XML toodefine hello 數目。</span><span class="sxs-lookup"><span data-stu-id="fe00b-150">TaskBody properties must use literal XML toodefine hello number of input, or output assets that are used by hello task.</span></span> <span data-ttu-id="fe00b-151">hello 工作主題包含 XML hello XML 結構描述定義。</span><span class="sxs-lookup"><span data-stu-id="fe00b-151">hello task topic contains hello XML Schema Definition for hello XML.</span></span>
* <span data-ttu-id="fe00b-152">在 hello TaskBody 定義中，每個內部值<inputAsset>和<outputAsset>必須設定為 JobInputAsset(value) 或 JobOutputAsset(value)。</span><span class="sxs-lookup"><span data-stu-id="fe00b-152">In hello TaskBody definition, each inner value for <inputAsset> and <outputAsset> must be set as JobInputAsset(value) or JobOutputAsset(value).</span></span>
* <span data-ttu-id="fe00b-153">每個工作可以有多個輸出資產。</span><span class="sxs-lookup"><span data-stu-id="fe00b-153">A task can have multiple output assets.</span></span> <span data-ttu-id="fe00b-154">一個 JobOutputAsset(x) 只能使用一次做為工作中的工作輸出。</span><span class="sxs-lookup"><span data-stu-id="fe00b-154">One JobOutputAsset(x) can only be used once as an output of a task in a job.</span></span>
* <span data-ttu-id="fe00b-155">您可以指定 JobInputAsset 或 JobOutputAsset 做為工作的輸入資產。</span><span class="sxs-lookup"><span data-stu-id="fe00b-155">You can specify JobInputAsset or JobOutputAsset as an input asset of a task.</span></span>
* <span data-ttu-id="fe00b-156">工作不能形成循環。</span><span class="sxs-lookup"><span data-stu-id="fe00b-156">Tasks must not form a cycle.</span></span>
* <span data-ttu-id="fe00b-157">您傳遞 tooJobInputAsset 或 JobOutputAsset 的 hello value 參數代表資產 hello 索引值。</span><span class="sxs-lookup"><span data-stu-id="fe00b-157">hello value parameter that you pass tooJobInputAsset or JobOutputAsset represents hello index value for an asset.</span></span> <span data-ttu-id="fe00b-158">hello 實際的資產會定義在 hello Inputmediaasset 與 Outputmediaasset 導覽屬性上 hello 工作實體定義。</span><span class="sxs-lookup"><span data-stu-id="fe00b-158">hello actual assets are defined in hello InputMediaAssets and OutputMediaAssets navigation properties on hello job entity definition.</span></span>
* <span data-ttu-id="fe00b-159">因為 Media Services 內建於 OData v3，hello 個別資產 hello Inputmediaasset 與 Outputmediaasset 導覽屬性集合會透過參考"__metadata: uri"名稱 / 值組。</span><span class="sxs-lookup"><span data-stu-id="fe00b-159">Because Media Services is built on OData v3, hello individual assets in hello InputMediaAssets and OutputMediaAssets navigation property collections are referenced through a "__metadata : uri" name-value pair.</span></span>
* <span data-ttu-id="fe00b-160">Inputmediaasset 對應 tooone 或您建立 Media Services 中的多個資產。</span><span class="sxs-lookup"><span data-stu-id="fe00b-160">InputMediaAssets maps tooone or more assets that you created in Media Services.</span></span> <span data-ttu-id="fe00b-161">Outputmediaasset 由 hello 系統建立。</span><span class="sxs-lookup"><span data-stu-id="fe00b-161">OutputMediaAssets are created by hello system.</span></span> <span data-ttu-id="fe00b-162">它們不會參考現有的資產。</span><span class="sxs-lookup"><span data-stu-id="fe00b-162">They don't reference an existing asset.</span></span>
* <span data-ttu-id="fe00b-163">Outputmediaasset 可以使用 hello assetName 屬性命名。</span><span class="sxs-lookup"><span data-stu-id="fe00b-163">OutputMediaAssets can be named by using hello assetName attribute.</span></span> <span data-ttu-id="fe00b-164">如果這個屬性不存在，則 hello OutputMediaAsset hello 名稱是 hello 任何 hello 內部文字值<outputAsset>項目是與 hello 作業名稱值或 （在 hello hello Name 屬性不定義所在的情況下） 的 hello 作業識別碼值的尾碼。</span><span class="sxs-lookup"><span data-stu-id="fe00b-164">If this attribute is not present, then hello name of hello OutputMediaAsset is whatever hello inner text value of hello <outputAsset> element is with a suffix of either hello Job Name value, or hello Job Id value (in hello case where hello Name property isn't defined).</span></span> <span data-ttu-id="fe00b-165">例如，如果您設定 assetName 的值太 「 範例 」，然後 hello OutputMediaAsset Name 屬性設定太"Sample。"</span><span class="sxs-lookup"><span data-stu-id="fe00b-165">For example, if you set a value for assetName too"Sample," then hello OutputMediaAsset Name property is set too"Sample."</span></span> <span data-ttu-id="fe00b-166">不過，如果您未設定 assetName 的值，但是未設定 hello 工作名稱太"NewJob，"然後 hello OutputMediaAsset Name 將是"JobOutputAsset （值） _NewJob"。</span><span class="sxs-lookup"><span data-stu-id="fe00b-166">However, if you didn't set a value for assetName, but did set hello job name too"NewJob," then hello OutputMediaAsset Name would be "JobOutputAsset(value)_NewJob."</span></span>

## <a name="create-a-job-with-chained-tasks"></a><span data-ttu-id="fe00b-167">建立具有鏈結工作的工作</span><span class="sxs-lookup"><span data-stu-id="fe00b-167">Create a job with chained tasks</span></span>
<span data-ttu-id="fe00b-168">在許多應用程式案例中，開發人員會想 toocreate 一連串的處理工作。</span><span class="sxs-lookup"><span data-stu-id="fe00b-168">In many application scenarios, developers want toocreate a series of processing tasks.</span></span> <span data-ttu-id="fe00b-169">在媒體服務中，您可以建立一連串的鏈結工作。</span><span class="sxs-lookup"><span data-stu-id="fe00b-169">In Media Services, you can create a series of chained tasks.</span></span> <span data-ttu-id="fe00b-170">每一項工作會執行不同的處理步驟，而且可以使用不同的媒體處理器。</span><span class="sxs-lookup"><span data-stu-id="fe00b-170">Each task performs different processing steps and can use different media processors.</span></span> <span data-ttu-id="fe00b-171">hello 鏈結工作可以遞交資產，從一個工作 tooanother，hello 資產上執行一連串的工作。</span><span class="sxs-lookup"><span data-stu-id="fe00b-171">hello chained tasks can hand off an asset from one task tooanother, performing a linear sequence of tasks on hello asset.</span></span> <span data-ttu-id="fe00b-172">不過，執行作業中的 hello 工作就不需要的 toobe 序列中。</span><span class="sxs-lookup"><span data-stu-id="fe00b-172">However, hello tasks performed in a job are not required toobe in a sequence.</span></span> <span data-ttu-id="fe00b-173">當您建立鏈結的工作時，hello 鏈結**ITask**物件都會建立單一**IJob**物件。</span><span class="sxs-lookup"><span data-stu-id="fe00b-173">When you create a chained task, hello chained **ITask** objects are created in a single **IJob** object.</span></span>

> [!NOTE]
> <span data-ttu-id="fe00b-174">目前有每個工作裡 30 個工作的限制。</span><span class="sxs-lookup"><span data-stu-id="fe00b-174">There is currently a limit of 30 tasks per job.</span></span> <span data-ttu-id="fe00b-175">如果您需要 toochain 30 個以上的工作，建立多個作業 toocontain hello 工作。</span><span class="sxs-lookup"><span data-stu-id="fe00b-175">If you need toochain more than 30 tasks, create more than one job toocontain hello tasks.</span></span>
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


### <a name="considerations"></a><span data-ttu-id="fe00b-176">考量</span><span class="sxs-lookup"><span data-stu-id="fe00b-176">Considerations</span></span>
<span data-ttu-id="fe00b-177">tooenable 鏈結工作：</span><span class="sxs-lookup"><span data-stu-id="fe00b-177">tooenable task chaining:</span></span>

* <span data-ttu-id="fe00b-178">一個作業至少必須有 2 個工作。</span><span class="sxs-lookup"><span data-stu-id="fe00b-178">A job must have at least two tasks.</span></span>
* <span data-ttu-id="fe00b-179">必須有至少一個工作的輸入是 hello hello 工作中另一項工作的輸出。</span><span class="sxs-lookup"><span data-stu-id="fe00b-179">There must be at least one task whose input is hello output of another task in hello job.</span></span>

## <a name="use-odata-batch-processing"></a><span data-ttu-id="fe00b-180">使用 OData 批次處理</span><span class="sxs-lookup"><span data-stu-id="fe00b-180">Use OData batch processing</span></span>
<span data-ttu-id="fe00b-181">hello 下列範例顯示如何 toouse OData 批次處理 toocreate 工作和工作。</span><span class="sxs-lookup"><span data-stu-id="fe00b-181">hello following example shows how toouse OData batch processing toocreate a job and tasks.</span></span> <span data-ttu-id="fe00b-182">如需批次處理的資訊，請參閱 [開放式資料通訊協定 (OData) 批次處理](http://www.odata.org/documentation/odata-version-3-0/batch-processing/)。</span><span class="sxs-lookup"><span data-stu-id="fe00b-182">For information on batch processing, see [Open Data Protocol (OData) Batch Processing](http://www.odata.org/documentation/odata-version-3-0/batch-processing/).</span></span>

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



## <a name="create-a-job-by-using-a-jobtemplate"></a><span data-ttu-id="fe00b-183">使用 JobTemplate 建立作業</span><span class="sxs-lookup"><span data-stu-id="fe00b-183">Create a job by using a JobTemplate</span></span>
<span data-ttu-id="fe00b-184">當您使用一組常用的工作，則使用 JobTemplate toospecify hello 預設的工作預設設定或工作的 tooset hello 順序來處理多個資產。</span><span class="sxs-lookup"><span data-stu-id="fe00b-184">When you process multiple assets by using a common set of tasks, use a JobTemplate toospecify hello default task presets, or tooset hello order of tasks.</span></span>

<span data-ttu-id="fe00b-185">下列範例中的 hello 顯示 toocreate 是 TaskTemplate 使用 JobTemplate 定義內嵌的方式。</span><span class="sxs-lookup"><span data-stu-id="fe00b-185">hello following example shows how toocreate a JobTemplate with a TaskTemplate that is defined inline.</span></span> <span data-ttu-id="fe00b-186">hello TaskTemplate 使用 hello 媒體編碼器標準為 hello MediaProcessor tooencode hello 資產檔案。</span><span class="sxs-lookup"><span data-stu-id="fe00b-186">hello TaskTemplate uses hello Media Encoder Standard as hello MediaProcessor tooencode hello asset file.</span></span> <span data-ttu-id="fe00b-187">但是，也可以使用其他 MediaProcessor。</span><span class="sxs-lookup"><span data-stu-id="fe00b-187">However, other MediaProcessors can be used as well.</span></span>

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
> <span data-ttu-id="fe00b-188">不同於其他媒體服務實體，您必須為每個 TaskTemplate 定義新的 GUID 識別碼，並將它放在 hello taskTemplateId 與 Id 屬性中，要求主體中。</span><span class="sxs-lookup"><span data-stu-id="fe00b-188">Unlike other Media Services entities, you must define a new GUID identifier for each TaskTemplate and place it in hello taskTemplateId and Id property in your request body.</span></span> <span data-ttu-id="fe00b-189">hello 內容識別配置必須依照 hello 配置識別 Azure 媒體服務實體中所述。</span><span class="sxs-lookup"><span data-stu-id="fe00b-189">hello content identification scheme must follow hello scheme described in Identify Azure Media Services Entities.</span></span> <span data-ttu-id="fe00b-190">而且，不能更新 JobTemplate。</span><span class="sxs-lookup"><span data-stu-id="fe00b-190">Also, JobTemplates cannot be updated.</span></span> <span data-ttu-id="fe00b-191">相反地，您必須使用更新後的變更建立一個新的 JobTemplate。</span><span class="sxs-lookup"><span data-stu-id="fe00b-191">Instead, you must create a new one with your updated changes.</span></span>
>
>

<span data-ttu-id="fe00b-192">如果成功，則會傳回下列回應 hello:</span><span class="sxs-lookup"><span data-stu-id="fe00b-192">If successful, hello following response is returned:</span></span>

    HTTP/1.1 201 Created

    . . .


<span data-ttu-id="fe00b-193">下列範例會示範如何 hello toocreate 參考 JobTemplate 識別碼的工作：</span><span class="sxs-lookup"><span data-stu-id="fe00b-193">hello following example shows how toocreate a job that references a JobTemplate Id:</span></span>

    POST https://media.windows.net/API/Jobs HTTP/1.1
    Content-Type: application/json;odata=verbose
    Accept: application/json;odata=verbose
    DataServiceVersion: 3.0
    MaxDataServiceVersion: 3.0
    x-ms-version: 2.11
    Authorization: Bearer <token value>
    Host: media.windows.net


    {"Name" : "NewTestJob", "InputMediaAssets" : [{"__metadata" : {"uri" : "https://media.windows.net/api/Assets('nb%3Acid%3AUUID%3A3f1fe4a2-68f5-4190-9557-cd45beccef92')"}}], "TemplateId" : "nb:jtid:UUID:15e6e5e6-ac85-084e-9dc2-db3645fbf0aa"}


<span data-ttu-id="fe00b-194">如果成功，則會傳回下列回應 hello:</span><span class="sxs-lookup"><span data-stu-id="fe00b-194">If successful, hello following response is returned:</span></span>

    HTTP/1.1 201 Created

    . . .



## <a name="media-services-learning-paths"></a><span data-ttu-id="fe00b-195">媒體服務學習路徑</span><span class="sxs-lookup"><span data-stu-id="fe00b-195">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="fe00b-196">提供意見反應</span><span class="sxs-lookup"><span data-stu-id="fe00b-196">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="next-steps"></a><span data-ttu-id="fe00b-197">後續步驟</span><span class="sxs-lookup"><span data-stu-id="fe00b-197">Next steps</span></span>
<span data-ttu-id="fe00b-198">您現在知道如何 toocreate 作業 tooencode 資產，請參閱[toocheck 如何工作進度與 Media Services](media-services-rest-check-job-progress.md)。</span><span class="sxs-lookup"><span data-stu-id="fe00b-198">Now that you know how toocreate a job tooencode an asset, see [How toocheck job progress with Media Services](media-services-rest-check-job-progress.md).</span></span>

## <a name="see-also"></a><span data-ttu-id="fe00b-199">另請參閱</span><span class="sxs-lookup"><span data-stu-id="fe00b-199">See also</span></span>
[<span data-ttu-id="fe00b-200">取得媒體處理器</span><span class="sxs-lookup"><span data-stu-id="fe00b-200">Get Media Processors</span></span>](media-services-rest-get-media-processor.md)
