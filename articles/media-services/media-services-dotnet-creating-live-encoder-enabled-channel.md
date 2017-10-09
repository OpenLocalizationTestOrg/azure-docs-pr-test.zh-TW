---
title: "aaaHow tooperform 即時資料流搭配.NET 使用 Azure Media Services toocreate 多位元速率串流 |Microsoft 文件"
description: "此教學課程會逐步引導您完成建立通道的 hello 步驟接收單一位元速率即時串流，並將其編碼為使用.NET SDK toomulti 位元速率資料流。"
services: media-services
documentationcenter: 
author: anilmur
manager: cfowler
editor: 
ms.assetid: 4df5e690-ff63-47cc-879b-9c57cb8ec240
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/17/2017
ms.author: juliako;anilmur
ms.openlocfilehash: 22088e6a78a49bd839575614a7c17a411ae8081c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooperform-live-streaming-using-azure-media-services-toocreate-multi-bitrate-streams-with-net"></a><span data-ttu-id="12397-103">如何 tooperform 即時資料流使用 Azure Media Services toocreate 多位元速率串流的.NET</span><span class="sxs-lookup"><span data-stu-id="12397-103">How tooperform live streaming using Azure Media Services toocreate multi-bitrate streams with .NET</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="12397-104">入口網站</span><span class="sxs-lookup"><span data-stu-id="12397-104">Portal</span></span>](media-services-portal-creating-live-encoder-enabled-channel.md)
> * [<span data-ttu-id="12397-105">.NET</span><span class="sxs-lookup"><span data-stu-id="12397-105">.NET</span></span>](media-services-dotnet-creating-live-encoder-enabled-channel.md)
> * [<span data-ttu-id="12397-106">REST API</span><span class="sxs-lookup"><span data-stu-id="12397-106">REST API</span></span>](https://docs.microsoft.com/rest/api/media/operations/channel)
> 
> [!NOTE]
> <span data-ttu-id="12397-107">toocomplete 本教學課程中，您需要 Azure 帳戶。</span><span class="sxs-lookup"><span data-stu-id="12397-107">toocomplete this tutorial, you need an Azure account.</span></span> <span data-ttu-id="12397-108">如需詳細資料，請參閱 [Azure 免費試用](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F)。</span><span class="sxs-lookup"><span data-stu-id="12397-108">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F).</span></span>
> 
> 

## <a name="overview"></a><span data-ttu-id="12397-109">概觀</span><span class="sxs-lookup"><span data-stu-id="12397-109">Overview</span></span>
<span data-ttu-id="12397-110">本教學課程將引導您完成 hello 步驟建立的**通道**，接收單一位元速率即時串流，並將其編碼 toomulti 位元速率串流。</span><span class="sxs-lookup"><span data-stu-id="12397-110">This tutorial walks you through hello steps of creating a **Channel** that receives a single-bitrate live stream and encodes it toomulti-bitrate stream.</span></span>

<span data-ttu-id="12397-111">如需詳細的概念性資訊相關的 tooChannels 啟用即時編碼，請參閱[使用 Azure Media Services toocreate 多位元速率串流的即時串流](media-services-manage-live-encoder-enabled-channels.md)。</span><span class="sxs-lookup"><span data-stu-id="12397-111">For more conceptual information related tooChannels that are enabled for live encoding, see [Live streaming using Azure Media Services toocreate multi-bitrate streams](media-services-manage-live-encoder-enabled-channels.md).</span></span>

## <a name="common-live-streaming-scenario"></a><span data-ttu-id="12397-112">常見即時串流案例</span><span class="sxs-lookup"><span data-stu-id="12397-112">Common Live Streaming Scenario</span></span>
<span data-ttu-id="12397-113">hello 下列步驟說明建立通用的即時串流應用程式的相關工作。</span><span class="sxs-lookup"><span data-stu-id="12397-113">hello following steps describe tasks involved in creating common live streaming applications.</span></span>

> [!NOTE]
> <span data-ttu-id="12397-114">目前，最大的 hello 建議即時事件的持續時間是 8 小時。</span><span class="sxs-lookup"><span data-stu-id="12397-114">Currently, hello max recommended duration of a live event is 8 hours.</span></span> <span data-ttu-id="12397-115">請如果您需要 toorun 通道的時間較長的時間，連絡 amslived microsoft.com。</span><span class="sxs-lookup"><span data-stu-id="12397-115">Please contact amslived at Microsoft.com if you need toorun a Channel for longer periods of time.</span></span>
> 
> 

1. <span data-ttu-id="12397-116">視訊攝影機 tooa 電腦連線。</span><span class="sxs-lookup"><span data-stu-id="12397-116">Connect a video camera tooa computer.</span></span> <span data-ttu-id="12397-117">啟動及設定內部部署即時編碼器可以輸出的其中一種 hello 下列通訊協定的單一位元速率資料流： RTMP、 Smooth Streaming 或 RTP (MPEG-TS)。</span><span class="sxs-lookup"><span data-stu-id="12397-117">Launch and configure an on-premises live encoder that can output a single bitrate stream in one of hello following protocols: RTMP, Smooth Streaming, or RTP (MPEG-TS).</span></span> <span data-ttu-id="12397-118">如需詳細資訊，請參閱 [Azure 媒體服務 RTMP 支援和即時編碼器](http://go.microsoft.com/fwlink/?LinkId=532824)。</span><span class="sxs-lookup"><span data-stu-id="12397-118">For more information, see [Azure Media Services RTMP Support and Live Encoders](http://go.microsoft.com/fwlink/?LinkId=532824).</span></span>

    <span data-ttu-id="12397-119">此步驟也可以在您建立通道之後執行。</span><span class="sxs-lookup"><span data-stu-id="12397-119">This step could also be performed after you create your Channel.</span></span>

2. <span data-ttu-id="12397-120">建立並啟動通道。</span><span class="sxs-lookup"><span data-stu-id="12397-120">Create and start a Channel.</span></span>
3. <span data-ttu-id="12397-121">擷取 hello 通道的內嵌 URL。</span><span class="sxs-lookup"><span data-stu-id="12397-121">Retrieve hello Channel ingest URL.</span></span>

    <span data-ttu-id="12397-122">hello 內嵌 URL 由 hello 即時編碼器 toosend hello 資料流 toohello 通道。</span><span class="sxs-lookup"><span data-stu-id="12397-122">hello ingest URL is used by hello live encoder toosend hello stream toohello Channel.</span></span>

4. <span data-ttu-id="12397-123">擷取 hello 通道預覽 URL。</span><span class="sxs-lookup"><span data-stu-id="12397-123">Retrieve hello Channel preview URL.</span></span>

    <span data-ttu-id="12397-124">使用您的通道可正常接收即時資料流 hello 這個 URL tooverify。</span><span class="sxs-lookup"><span data-stu-id="12397-124">Use this URL tooverify that your channel is properly receiving hello live stream.</span></span>

5. <span data-ttu-id="12397-125">建立資產。</span><span class="sxs-lookup"><span data-stu-id="12397-125">Create an asset.</span></span>
6. <span data-ttu-id="12397-126">如果您想要在播放期間動態加密 hello 資產 toobe，請勿 hello 遵循：</span><span class="sxs-lookup"><span data-stu-id="12397-126">If you want for hello asset toobe dynamically encrypted during playback, do hello following:</span></span>
7. <span data-ttu-id="12397-127">建立內容金鑰。</span><span class="sxs-lookup"><span data-stu-id="12397-127">Create a content key.</span></span>
8. <span data-ttu-id="12397-128">設定 hello 內容金鑰授權原則。</span><span class="sxs-lookup"><span data-stu-id="12397-128">Configure hello content key's authorization policy.</span></span>
9. <span data-ttu-id="12397-129">設定資產傳遞原則 (供動態封裝和動態加密使用)。</span><span class="sxs-lookup"><span data-stu-id="12397-129">Configure asset delivery policy (used by dynamic packaging and dynamic encryption).</span></span>
10. <span data-ttu-id="12397-130">建立程式，並指定您所建立的 toouse hello 資產。</span><span class="sxs-lookup"><span data-stu-id="12397-130">Create a program and specify toouse hello asset that you created.</span></span>
11. <span data-ttu-id="12397-131">發佈 hello 資產建立 OnDemand 定位器與 hello 程式相關聯。</span><span class="sxs-lookup"><span data-stu-id="12397-131">Publish hello asset associated with hello program by creating an OnDemand locator.</span></span>

    >[!NOTE]
    ><span data-ttu-id="12397-132">AMS 帳戶建立時**預設**串流端點就會加入 tooyour 帳戶 hello**已停止**狀態。</span><span class="sxs-lookup"><span data-stu-id="12397-132">When your AMS account is created a **default** streaming endpoint is added tooyour account in hello **Stopped** state.</span></span> <span data-ttu-id="12397-133">hello 串流的端點要從中 toostream 內容已經在 hello toobe**執行**狀態。</span><span class="sxs-lookup"><span data-stu-id="12397-133">hello streaming endpoint from which you want toostream content has toobe in hello **Running** state.</span></span> 

12. <span data-ttu-id="12397-134">當您準備好 toostart 串流和封存時，請啟動 hello 程式。</span><span class="sxs-lookup"><span data-stu-id="12397-134">Start hello program when you are ready toostart streaming and archiving.</span></span>
13. <span data-ttu-id="12397-135">（選擇性） hello 即時編碼器可以信號的 toostart 公告。</span><span class="sxs-lookup"><span data-stu-id="12397-135">Optionally, hello live encoder can be signaled toostart an advertisement.</span></span> <span data-ttu-id="12397-136">hello 公告 hello 輸出資料流中插入。</span><span class="sxs-lookup"><span data-stu-id="12397-136">hello advertisement is inserted in hello output stream.</span></span>
14. <span data-ttu-id="12397-137">每當您想 toostop 串流並封存 hello 事件時，請停止 hello 程式。</span><span class="sxs-lookup"><span data-stu-id="12397-137">Stop hello program whenever you want toostop streaming and archiving hello event.</span></span>
15. <span data-ttu-id="12397-138">刪除 hello 程式 （並選擇性地刪除 hello 資產）。</span><span class="sxs-lookup"><span data-stu-id="12397-138">Delete hello Program (and optionally delete hello asset).</span></span>

## <a name="what-youll-learn"></a><span data-ttu-id="12397-139">您將學到什麼</span><span class="sxs-lookup"><span data-stu-id="12397-139">What you'll learn</span></span>
<span data-ttu-id="12397-140">本主題說明如何 tooexecute 通道和程式使用 Media Services.NET SDK 上不同的作業。</span><span class="sxs-lookup"><span data-stu-id="12397-140">This topic shows you how tooexecute different operations on channels and programs using Media Services .NET SDK.</span></span> <span data-ttu-id="12397-141">因為許多作業會長時間執行，所以會使用管理長時間執行作業的 .NET API。</span><span class="sxs-lookup"><span data-stu-id="12397-141">Because many operations are long-running .NET APIs that manage long running operations are used.</span></span>

<span data-ttu-id="12397-142">hello 主題顯示如何 toodo hello 下列：</span><span class="sxs-lookup"><span data-stu-id="12397-142">hello topic shows how toodo hello following:</span></span>

1. <span data-ttu-id="12397-143">建立並啟動通道。</span><span class="sxs-lookup"><span data-stu-id="12397-143">Create and start a channel.</span></span> <span data-ttu-id="12397-144">使用長時間執行的 API。</span><span class="sxs-lookup"><span data-stu-id="12397-144">Long-running APIs are used.</span></span>
2. <span data-ttu-id="12397-145">取得 hello 通道內嵌 （輸入） 端點。</span><span class="sxs-lookup"><span data-stu-id="12397-145">Get hello channels ingest (input) endpoint.</span></span> <span data-ttu-id="12397-146">此端點應提供 toohello 編碼器，可以傳送單一位元速率即時資料流。</span><span class="sxs-lookup"><span data-stu-id="12397-146">This endpoint should be provided toohello encoder that can send a single bitrate live stream.</span></span>
3. <span data-ttu-id="12397-147">收到 hello 預覽端點。</span><span class="sxs-lookup"><span data-stu-id="12397-147">Get hello preview endpoint.</span></span> <span data-ttu-id="12397-148">此端點是使用的 toopreview 您的資料流。</span><span class="sxs-lookup"><span data-stu-id="12397-148">This endpoint is used toopreview your stream.</span></span>
4. <span data-ttu-id="12397-149">建立資產將會使用的 toostore 您的內容。</span><span class="sxs-lookup"><span data-stu-id="12397-149">Create an asset that will be used toostore your content.</span></span> <span data-ttu-id="12397-150">應該也，如本範例所示設定 hello 資產傳遞原則。</span><span class="sxs-lookup"><span data-stu-id="12397-150">hello asset delivery policies should be configured as well, as shown in this example.</span></span>
5. <span data-ttu-id="12397-151">建立程式，並指定稍早建立的 toouse hello 資產。</span><span class="sxs-lookup"><span data-stu-id="12397-151">Create a program and specify toouse hello asset that was created earlier.</span></span> <span data-ttu-id="12397-152">啟動 hello 程式。</span><span class="sxs-lookup"><span data-stu-id="12397-152">Start hello program.</span></span> <span data-ttu-id="12397-153">使用長時間執行的 API。</span><span class="sxs-lookup"><span data-stu-id="12397-153">Long-running APIs are used.</span></span>
6. <span data-ttu-id="12397-154">建立 hello 資產的定位器，因此 hello 內容取得發行，且可以進行資料流處理的 tooyour 用戶端。</span><span class="sxs-lookup"><span data-stu-id="12397-154">Create a locator for hello asset, so hello content gets published and can be streamed tooyour clients.</span></span>
7. <span data-ttu-id="12397-155">顯示和隱藏 slate。</span><span class="sxs-lookup"><span data-stu-id="12397-155">Show and hide slates.</span></span> <span data-ttu-id="12397-156">啟動和停止公告。</span><span class="sxs-lookup"><span data-stu-id="12397-156">Start and stop advertisements.</span></span> <span data-ttu-id="12397-157">使用長時間執行的 API。</span><span class="sxs-lookup"><span data-stu-id="12397-157">Long-running APIs are used.</span></span>
8. <span data-ttu-id="12397-158">清除 您的通道，以及所有 hello 相關聯的資源。</span><span class="sxs-lookup"><span data-stu-id="12397-158">Clean up your channel and all hello associated resources.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="12397-159">必要條件</span><span class="sxs-lookup"><span data-stu-id="12397-159">Prerequisites</span></span>
<span data-ttu-id="12397-160">hello 下面是必要的 toocomplete hello 教學課程。</span><span class="sxs-lookup"><span data-stu-id="12397-160">hello following are required toocomplete hello tutorial.</span></span>

* <span data-ttu-id="12397-161">一個 Azure 帳戶。</span><span class="sxs-lookup"><span data-stu-id="12397-161">An Azure account.</span></span> <span data-ttu-id="12397-162">如果您沒有帳戶，只需要幾分鐘的時間就可以建立免費試用帳戶。</span><span class="sxs-lookup"><span data-stu-id="12397-162">If you don't have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="12397-163">如需詳細資料，請參閱 [Azure 免費試用](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F)。</span><span class="sxs-lookup"><span data-stu-id="12397-163">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F).</span></span> <span data-ttu-id="12397-164">就可以使用的 tootry 出支付 Azure 服務的信用額度。</span><span class="sxs-lookup"><span data-stu-id="12397-164">You get credits that can be used tootry out paid Azure services.</span></span> <span data-ttu-id="12397-165">即使 hello 信用額度用完之後，您可以讓 hello 的帳戶，並使用免費的 Azure 服務與功能，例如 Azure App Service 中的 hello Web 應用程式功能。</span><span class="sxs-lookup"><span data-stu-id="12397-165">Even after hello credits are used up, you can keep hello account and use free Azure services and features, such as hello Web Apps feature in Azure App Service.</span></span>
* <span data-ttu-id="12397-166">媒體服務帳戶。</span><span class="sxs-lookup"><span data-stu-id="12397-166">A Media Services account.</span></span> <span data-ttu-id="12397-167">toocreate Media Services 帳戶，請參閱[建立帳戶](media-services-portal-create-account.md)。</span><span class="sxs-lookup"><span data-stu-id="12397-167">toocreate a Media Services account, see [Create Account](media-services-portal-create-account.md).</span></span>
* <span data-ttu-id="12397-168">Visual Studio 2010 SP1 (Professional、Premium、Ultimate 或 Express) 或較新版本。</span><span class="sxs-lookup"><span data-stu-id="12397-168">Visual Studio 2010 SP1 (Professional, Premium, Ultimate, or Express) or later versions.</span></span>
* <span data-ttu-id="12397-169">您必須使用媒體服務 .NET SDK 3.2.0.0 版或更新版本。</span><span class="sxs-lookup"><span data-stu-id="12397-169">You must use Media Services .NET SDK version 3.2.0.0 or newer.</span></span>
* <span data-ttu-id="12397-170">網路攝影機以及可以傳送單一位元速率即時串流的編碼器。</span><span class="sxs-lookup"><span data-stu-id="12397-170">A webcam and an encoder that can send a single bitrate live stream.</span></span>

## <a name="considerations"></a><span data-ttu-id="12397-171">考量</span><span class="sxs-lookup"><span data-stu-id="12397-171">Considerations</span></span>
* <span data-ttu-id="12397-172">目前，最大的 hello 建議即時事件的持續時間是 8 小時。</span><span class="sxs-lookup"><span data-stu-id="12397-172">Currently, hello max recommended duration of a live event is 8 hours.</span></span> <span data-ttu-id="12397-173">請如果您需要 toorun 通道的時間較長的時間，連絡 amslived microsoft.com。</span><span class="sxs-lookup"><span data-stu-id="12397-173">Please contact amslived at Microsoft.com if you need toorun a Channel for longer periods of time.</span></span>
* <span data-ttu-id="12397-174">對於不同的 AMS 原則 (例如 Locator 原則或 ContentKeyAuthorizationPolicy) 有 1,000,000 個原則的限制。</span><span class="sxs-lookup"><span data-stu-id="12397-174">There is a limit of 1,000,000 policies for different AMS policies (for example, for Locator policy or ContentKeyAuthorizationPolicy).</span></span> <span data-ttu-id="12397-175">您應該使用 hello 如果一律使用相同的原則識別碼 hello 相同天 / 存取權限，例如，原則會就地預定的 tooremain 長時間 （非上載原則） 的定位器。</span><span class="sxs-lookup"><span data-stu-id="12397-175">You should use hello same policy ID if you are always using hello same days / access permissions, for example, policies for locators that are intended tooremain in place for a long time (non-upload policies).</span></span> <span data-ttu-id="12397-176">如需詳細資訊，請參閱 [這個](media-services-dotnet-manage-entities.md#limit-access-policies) 主題。</span><span class="sxs-lookup"><span data-stu-id="12397-176">For more information, see [this](media-services-dotnet-manage-entities.md#limit-access-policies) topic.</span></span>

## <a name="download-sample"></a><span data-ttu-id="12397-177">下載範例</span><span class="sxs-lookup"><span data-stu-id="12397-177">Download sample</span></span>

<span data-ttu-id="12397-178">您可以下載從本主題中所述的 hello 範例[這裡](https://azure.microsoft.com/documentation/samples/media-services-dotnet-encode-live-stream-with-ams-clear/)。</span><span class="sxs-lookup"><span data-stu-id="12397-178">You can download hello sample that is described in this topic from [here](https://azure.microsoft.com/documentation/samples/media-services-dotnet-encode-live-stream-with-ams-clear/).</span></span>

## <a name="set-up-for-development-with-media-services-sdk-for-net"></a><span data-ttu-id="12397-179">設定使用媒體服務 SDK for.NET 的開發</span><span class="sxs-lookup"><span data-stu-id="12397-179">Set up for development with Media Services SDK for .NET</span></span>

<span data-ttu-id="12397-180">設定您的開發環境，並填入 hello 與連接資訊的 app.config 檔案中所述[與.NET 的 Media Services 開發](media-services-dotnet-how-to-use.md)。</span><span class="sxs-lookup"><span data-stu-id="12397-180">Set up your development environment and populate hello app.config file with connection information, as described in [Media Services development with .NET](media-services-dotnet-how-to-use.md).</span></span> 

## <a name="code-example"></a><span data-ttu-id="12397-181">程式碼範例</span><span class="sxs-lookup"><span data-stu-id="12397-181">Code example</span></span>

    using System;
    using System.Collections.Generic;
    using System.Configuration;
    using System.IO;
    using System.Linq;
    using System.Net;
    using Microsoft.WindowsAzure.MediaServices.Client;
    using Microsoft.WindowsAzure.MediaServices.Client.DynamicEncryption;

    namespace EncodeLiveStreamWithAmsClear
    {
        class Program
        {
        private const string ChannelName = "channel001";
        private const string AssetlName = "asset001";
        private const string ProgramlName = "program001";

        // Read values from hello App.config file.
        private static readonly string _AADTenantDomain =
        ConfigurationManager.AppSettings["AADTenantDomain"];
        private static readonly string _RESTAPIEndpoint =
        ConfigurationManager.AppSettings["MediaServiceRESTAPIEndpoint"];

        private static CloudMediaContext _context = null;

        static void Main(string[] args)
        {
            var tokenCredentials = new AzureAdTokenCredentials(_AADTenantDomain, AzureEnvironments.AzureCloudEnvironment);
            var tokenProvider = new AzureAdTokenProvider(tokenCredentials);

            _context = new CloudMediaContext(new Uri(_RESTAPIEndpoint), tokenProvider);

            IChannel channel = CreateAndStartChannel();

            // hello channel's input endpoint:
            string ingestUrl = channel.Input.Endpoints.FirstOrDefault().Url.ToString();

            Console.WriteLine("Intest URL: {0}", ingestUrl);


            // Use hello previewEndpoint toopreview and verify 
            // that hello input from hello encoder is actually reaching hello Channel. 
            string previewEndpoint = channel.Preview.Endpoints.FirstOrDefault().Url.ToString();

            Console.WriteLine("Preview URL: {0}", previewEndpoint);

            // When Live Encoding is enabled, you can now get a preview of hello live feed as it reaches hello Channel. 
            // This can be a valuable tool toocheck whether your live feed is actually reaching hello Channel. 
            // hello thumbnail is exposed via hello same end-point as hello Channel Preview URL.
            string thumbnailUri = new UriBuilder
            {
            Scheme = Uri.UriSchemeHttps,
            Host = channel.Preview.Endpoints.FirstOrDefault().Url.Host,
            Path = "thumbnails/input.jpg"
            }.Uri.ToString();

            Console.WriteLine("Thumbain URL: {0}", thumbnailUri);

            // Once you previewed your stream and verified that it is flowing into your Channel, 
            // you can create an event by creating an Asset, Program, and Streaming Locator. 
            IAsset asset = CreateAndConfigureAsset();

            IProgram program = CreateAndStartProgram(channel, asset);

            ILocator locator = CreateLocatorForAsset(program.Asset, program.ArchiveWindowLength);

            // You can use slates and ads only if hello channel type is Standard.  
            StartStopAdsSlates(channel);

            // Once you are done streaming, clean up your resources.
            Cleanup(channel);
        }

        public static IChannel CreateAndStartChannel()
        {
            var channelInput = CreateChannelInput();
            var channePreview = CreateChannelPreview();
            var channelEncoding = CreateChannelEncoding();

            ChannelCreationOptions options = new ChannelCreationOptions
            {
            EncodingType = ChannelEncodingType.Standard,
            Name = ChannelName,
            Input = channelInput,
            Preview = channePreview,
            Encoding = channelEncoding
            };

            Log("Creating channel");
            IOperation channelCreateOperation = _context.Channels.SendCreateOperation(options);
            string channelId = TrackOperation(channelCreateOperation, "Channel create");

            IChannel channel = _context.Channels.Where(c => c.Id == channelId).FirstOrDefault();

            Log("Starting channel");
            var channelStartOperation = channel.SendStartOperation();
            TrackOperation(channelStartOperation, "Channel start");

            return channel;
        }

        /// <summary>
        /// Create channel input, used in channel creation options. 
        /// </summary>
        /// <returns></returns>
        private static ChannelInput CreateChannelInput()
        {
            return new ChannelInput
            {
            StreamingProtocol = StreamingProtocol.RTPMPEG2TS,
            AccessControl = new ChannelAccessControl
            {
                IPAllowList = new List<IPRange>
                {
                    new IPRange
                    {
                    Name = "TestChannelInput001",
                    Address = IPAddress.Parse("0.0.0.0"),
                    SubnetPrefixLength = 0
                    }
                }
            }
            };
        }

        /// <summary>
        /// Create channel preview, used in channel creation options. 
        /// </summary>
        /// <returns></returns>
        private static ChannelPreview CreateChannelPreview()
        {
            return new ChannelPreview
            {
            AccessControl = new ChannelAccessControl
            {
                IPAllowList = new List<IPRange>
                {
                    new IPRange
                    {
                    Name = "TestChannelPreview001",
                    Address = IPAddress.Parse("0.0.0.0"),
                    SubnetPrefixLength = 0
                    }
                }
            }
            };
        }

        /// <summary>
        /// Create channel encoding, used in channel creation options. 
        /// </summary>
        /// <returns></returns>
        private static ChannelEncoding CreateChannelEncoding()
        {
            return new ChannelEncoding
            {
            SystemPreset = "Default720p",
            IgnoreCea708ClosedCaptions = false,
            AdMarkerSource = AdMarkerSource.Api,
            // You can only set audio if streaming protocol is set tooStreamingProtocol.RTPMPEG2TS.
            AudioStreams = new List<AudioStream> { new AudioStream { Index = 103, Language = "eng" } }.AsReadOnly()
            };
        }

        /// <summary>
        /// Create an asset and configure asset delivery policies.
        /// </summary>
        /// <returns></returns>
        public static IAsset CreateAndConfigureAsset()
        {
            IAsset asset = _context.Assets.Create(AssetlName, AssetCreationOptions.None);

            IAssetDeliveryPolicy policy =
            _context.AssetDeliveryPolicies.Create("Clear Policy",
            AssetDeliveryPolicyType.NoDynamicEncryption,
            AssetDeliveryProtocol.HLS | AssetDeliveryProtocol.SmoothStreaming | AssetDeliveryProtocol.Dash, null);

            asset.DeliveryPolicies.Add(policy);

            return asset;
        }

        /// <summary>
        /// Create a Program on hello Channel. You can have multiple Programs that overlap or are sequential;
        /// however each Program must have a unique name within your Media Services account.
        /// </summary>
        /// <param name="channel"></param>
        /// <param name="asset"></param>
        /// <returns></returns>
        public static IProgram CreateAndStartProgram(IChannel channel, IAsset asset)
        {
            IProgram program = channel.Programs.Create(ProgramlName, TimeSpan.FromHours(3), asset.Id);
            Log("Program created", program.Id);

            Log("Starting program");
            var programStartOperation = program.SendStartOperation();
            TrackOperation(programStartOperation, "Program start");

            return program;
        }

        /// <summary>
        /// Create locators in order toobe able toopublish and stream hello video.
        /// </summary>
        /// <param name="asset"></param>
        /// <param name="ArchiveWindowLength"></param>
        /// <returns></returns>
        public static ILocator CreateLocatorForAsset(IAsset asset, TimeSpan ArchiveWindowLength)
        {
            // You cannot create a streaming locator using an AccessPolicy that includes write or delete permissions.            
            var locator = _context.Locators.CreateLocator
            (
                LocatorType.OnDemandOrigin,
                asset,
                _context.AccessPolicies.Create
                (
                    "Live Stream Policy",
                    ArchiveWindowLength,
                    AccessPermissions.Read
                )
            );

            return locator;
        }

        /// <summary>
        /// Perform operations on slates.
        /// </summary>
        /// <param name="channel"></param>
        public static void StartStopAdsSlates(IChannel channel)
        {
            int cueId = new Random().Next(int.MaxValue);
            var path = Path.GetFullPath(Path.Combine(AppDomain.CurrentDomain.BaseDirectory, @"..\\..\\SlateJPG\\DefaultAzurePortalSlate.jpg"));

            Log("Creating asset");
            var slateAsset = _context.Assets.Create("Slate test asset " + DateTime.Now.ToString("yyyy-MM-dd HH-mm"), AssetCreationOptions.None);
            Log("Slate asset created", slateAsset.Id);

            Log("Uploading file");
            var assetFile = slateAsset.AssetFiles.Create("DefaultAzurePortalSlate.jpg");
            assetFile.Upload(path);
            assetFile.IsPrimary = true;
            assetFile.Update();

            Log("Showing slate");
            var showSlateOpeartion = channel.SendShowSlateOperation(TimeSpan.FromMinutes(1), slateAsset.Id);
            TrackOperation(showSlateOpeartion, "Show slate");

            Log("Hiding slate");
            var hideSlateOperation = channel.SendHideSlateOperation();
            TrackOperation(hideSlateOperation, "Hide slate");

            Log("Starting ad");
            var startAdOperation = channel.SendStartAdvertisementOperation(TimeSpan.FromMinutes(1), cueId, false);
            TrackOperation(startAdOperation, "Start ad");

            Log("Ending ad");
            var endAdOperation = channel.SendEndAdvertisementOperation(cueId);
            TrackOperation(endAdOperation, "End ad");

            Log("Deleting slate asset");
            slateAsset.Delete();
        }

        /// <summary>
        /// Clean up resources associated with hello channel.
        /// </summary>
        /// <param name="channel"></param>
        public static void Cleanup(IChannel channel)
        {
            IAsset asset;
            if (channel != null)
            {
            foreach (var program in channel.Programs)
            {
                asset = _context.Assets.Where(se => se.Id == program.AssetId)
                            .FirstOrDefault();

                Log("Stopping program");
                var programStopOperation = program.SendStopOperation();
                TrackOperation(programStopOperation, "Program stop");

                program.Delete();

                if (asset != null)
                {
                Log("Deleting locators");
                foreach (var l in asset.Locators)
                    l.Delete();

                Log("Deleting asset");
                asset.Delete();
                }
            }

            Log("Stopping channel");
            var channelStopOperation = channel.SendStopOperation();
            TrackOperation(channelStopOperation, "Channel stop");

            Log("Deleting channel");
            var channelDeleteOperation = channel.SendDeleteOperation();
            TrackOperation(channelDeleteOperation, "Channel delete");
            }
        }

        /// <summary>
        /// Track long running operations.
        /// </summary>
        /// <param name="operation"></param>
        /// <param name="description"></param>
        /// <returns></returns>
        public static string TrackOperation(IOperation operation, string description)
        {
            string entityId = null;
            bool isCompleted = false;

            Log("starting tootrack ", null, operation.Id);
            while (isCompleted == false)
            {
            operation = _context.Operations.GetOperation(operation.Id);
            isCompleted = IsCompleted(operation, out entityId);
            System.Threading.Thread.Sleep(TimeSpan.FromSeconds(30));
            }
            // If we got here, hello operation succeeded.
            Log(description + " in completed", operation.TargetEntityId, operation.Id);

            return entityId;
        }

        /// <summary> 
        /// Checks if hello operation has been completed. 
        /// If hello operation succeeded, hello created entity Id is returned in hello out parameter.
        /// </summary> 
        /// <param name="operationId">hello operation Id.</param> 
        /// <param name="channel">
        /// If hello operation succeeded, 
        /// hello entity Id associated with hello sucessful operation is returned in hello out parameter.</param>
        /// <returns>Returns false if hello operation is still in progress; otherwise, true.</returns> 
        private static bool IsCompleted(IOperation operation, out string entityId)
        {
            bool completed = false;

            entityId = null;

            switch (operation.State)
            {
            case OperationState.Failed:
                // Handle hello failure. 
                // For example, throw an exception. 
                // Use hello following information in hello exception: operationId, operation.ErrorMessage.
                Log("operation failed", operation.TargetEntityId, operation.Id);
                break;
            case OperationState.Succeeded:
                completed = true;
                entityId = operation.TargetEntityId;
                break;
            case OperationState.InProgress:
                completed = false;
                Log("operation in progress", operation.TargetEntityId, operation.Id);
                break;
            }
            return completed;
        }

        private static void Log(string action, string entityId = null, string operationId = null)
        {
            Console.WriteLine(
            "{0,-21}{1,-51}{2,-51}{3,-51}",
            DateTime.Now.ToString("yyyy'-'MM'-'dd HH':'mm':'ss"),
            action,
            entityId ?? string.Empty,
            operationId ?? string.Empty);
        }
        }
    }

## <a name="next-step"></a><span data-ttu-id="12397-182">後續步驟</span><span class="sxs-lookup"><span data-stu-id="12397-182">Next step</span></span>
<span data-ttu-id="12397-183">檢閱媒體服務學習路徑。</span><span class="sxs-lookup"><span data-stu-id="12397-183">Review Media Services learning paths.</span></span>

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="12397-184">提供意見反應</span><span class="sxs-lookup"><span data-stu-id="12397-184">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]


