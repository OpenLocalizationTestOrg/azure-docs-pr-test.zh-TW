---
title: "如何使用 Azure 媒體服務執行即時串流，以使用 .NET 建立多位元速率串流 | Microsoft Docs"
description: "本教學課程將逐步引導您使用 .NET SDK 建立通道，以接收單一位元速率即時串流，並將其編碼為多位元速率串流。"
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
ms.openlocfilehash: 22d63ff5e9fd33db8711b0c5125ab0882b9f6a74
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="how-to-perform-live-streaming-using-azure-media-services-to-create-multi-bitrate-streams-with-net"></a><span data-ttu-id="d6133-103">如何使用 Azure 媒體服務執行即時串流，以使用 .NET 建立多位元速率串流</span><span class="sxs-lookup"><span data-stu-id="d6133-103">How to perform live streaming using Azure Media Services to create multi-bitrate streams with .NET</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="d6133-104">入口網站</span><span class="sxs-lookup"><span data-stu-id="d6133-104">Portal</span></span>](media-services-portal-creating-live-encoder-enabled-channel.md)
> * [<span data-ttu-id="d6133-105">.NET</span><span class="sxs-lookup"><span data-stu-id="d6133-105">.NET</span></span>](media-services-dotnet-creating-live-encoder-enabled-channel.md)
> * [<span data-ttu-id="d6133-106">REST API</span><span class="sxs-lookup"><span data-stu-id="d6133-106">REST API</span></span>](https://docs.microsoft.com/rest/api/media/operations/channel)
> 
> [!NOTE]
> <span data-ttu-id="d6133-107">若要完成此教學課程，您需要 Azure 帳戶。</span><span class="sxs-lookup"><span data-stu-id="d6133-107">To complete this tutorial, you need an Azure account.</span></span> <span data-ttu-id="d6133-108">如需詳細資訊，請參閱 [Azure 免費試用](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F)。</span><span class="sxs-lookup"><span data-stu-id="d6133-108">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F).</span></span>
> 
> 

## <a name="overview"></a><span data-ttu-id="d6133-109">概觀</span><span class="sxs-lookup"><span data-stu-id="d6133-109">Overview</span></span>
<span data-ttu-id="d6133-110">本教學課程將逐步引導您建立 **通道** ，可接收單一位元速率的即時串流，並將其編碼為多位元速率串流。</span><span class="sxs-lookup"><span data-stu-id="d6133-110">This tutorial walks you through the steps of creating a **Channel** that receives a single-bitrate live stream and encodes it to multi-bitrate stream.</span></span>

<span data-ttu-id="d6133-111">如需為即時編碼啟用之通道相關的詳細概念資訊，請參閱 [使用 Azure 媒體服務的即時串流，以建立多位元速率串流](media-services-manage-live-encoder-enabled-channels.md)。</span><span class="sxs-lookup"><span data-stu-id="d6133-111">For more conceptual information related to Channels that are enabled for live encoding, see [Live streaming using Azure Media Services to create multi-bitrate streams](media-services-manage-live-encoder-enabled-channels.md).</span></span>

## <a name="common-live-streaming-scenario"></a><span data-ttu-id="d6133-112">常見即時串流案例</span><span class="sxs-lookup"><span data-stu-id="d6133-112">Common Live Streaming Scenario</span></span>
<span data-ttu-id="d6133-113">下列步驟描述當我們建立一般即時資料流應用程式時，會涉及到的各種工作。</span><span class="sxs-lookup"><span data-stu-id="d6133-113">The following steps describe tasks involved in creating common live streaming applications.</span></span>

> [!NOTE]
> <span data-ttu-id="d6133-114">目前，即時事件的最大建議持續時間是 8 小時。</span><span class="sxs-lookup"><span data-stu-id="d6133-114">Currently, the max recommended duration of a live event is 8 hours.</span></span> <span data-ttu-id="d6133-115">如果您需要較長的時間來執行通道，請連絡 amslived@Microsoft.com。</span><span class="sxs-lookup"><span data-stu-id="d6133-115">Please contact amslived at Microsoft.com if you need to run a Channel for longer periods of time.</span></span>
> 
> 

1. <span data-ttu-id="d6133-116">將攝影機連接到電腦。</span><span class="sxs-lookup"><span data-stu-id="d6133-116">Connect a video camera to a computer.</span></span> <span data-ttu-id="d6133-117">啟動和設定可使用下列其中一種通訊協定輸出單一位元速率串流的內部部署即時編碼器：RTMP、Smooth Streaming 或 RTP (MPEG-TS)。</span><span class="sxs-lookup"><span data-stu-id="d6133-117">Launch and configure an on-premises live encoder that can output a single bitrate stream in one of the following protocols: RTMP, Smooth Streaming, or RTP (MPEG-TS).</span></span> <span data-ttu-id="d6133-118">如需詳細資訊，請參閱 [Azure 媒體服務 RTMP 支援和即時編碼器](http://go.microsoft.com/fwlink/?LinkId=532824)。</span><span class="sxs-lookup"><span data-stu-id="d6133-118">For more information, see [Azure Media Services RTMP Support and Live Encoders](http://go.microsoft.com/fwlink/?LinkId=532824).</span></span>

    <span data-ttu-id="d6133-119">此步驟也可以在您建立通道之後執行。</span><span class="sxs-lookup"><span data-stu-id="d6133-119">This step could also be performed after you create your Channel.</span></span>

2. <span data-ttu-id="d6133-120">建立並啟動通道。</span><span class="sxs-lookup"><span data-stu-id="d6133-120">Create and start a Channel.</span></span>
3. <span data-ttu-id="d6133-121">擷取通道內嵌 URL。</span><span class="sxs-lookup"><span data-stu-id="d6133-121">Retrieve the Channel ingest URL.</span></span>

    <span data-ttu-id="d6133-122">內嵌 URL 可供即時編碼器用來傳送串流到通道。</span><span class="sxs-lookup"><span data-stu-id="d6133-122">The ingest URL is used by the live encoder to send the stream to the Channel.</span></span>

4. <span data-ttu-id="d6133-123">擷取通道預覽 URL。</span><span class="sxs-lookup"><span data-stu-id="d6133-123">Retrieve the Channel preview URL.</span></span>

    <span data-ttu-id="d6133-124">使用此 URL 來確認您的通道會正確接收即時串流。</span><span class="sxs-lookup"><span data-stu-id="d6133-124">Use this URL to verify that your channel is properly receiving the live stream.</span></span>

5. <span data-ttu-id="d6133-125">建立資產。</span><span class="sxs-lookup"><span data-stu-id="d6133-125">Create an asset.</span></span>
6. <span data-ttu-id="d6133-126">如果您想要在播放期間動態加密資產，請執行下列動作：</span><span class="sxs-lookup"><span data-stu-id="d6133-126">If you want for the asset to be dynamically encrypted during playback, do the following:</span></span>
7. <span data-ttu-id="d6133-127">建立內容金鑰。</span><span class="sxs-lookup"><span data-stu-id="d6133-127">Create a content key.</span></span>
8. <span data-ttu-id="d6133-128">設定內容金鑰的授權原則。</span><span class="sxs-lookup"><span data-stu-id="d6133-128">Configure the content key's authorization policy.</span></span>
9. <span data-ttu-id="d6133-129">設定資產傳遞原則 (供動態封裝和動態加密使用)。</span><span class="sxs-lookup"><span data-stu-id="d6133-129">Configure asset delivery policy (used by dynamic packaging and dynamic encryption).</span></span>
10. <span data-ttu-id="d6133-130">建立程式，並指定使用您所建立的資產。</span><span class="sxs-lookup"><span data-stu-id="d6133-130">Create a program and specify to use the asset that you created.</span></span>
11. <span data-ttu-id="d6133-131">藉由建立 OnDemand 定位器，發行與程式相關聯的資產。</span><span class="sxs-lookup"><span data-stu-id="d6133-131">Publish the asset associated with the program by creating an OnDemand locator.</span></span>

    >[!NOTE]
    ><span data-ttu-id="d6133-132">建立 AMS 帳戶時，**預設**串流端點會新增至 [已停止] 狀態的帳戶。</span><span class="sxs-lookup"><span data-stu-id="d6133-132">When your AMS account is created a **default** streaming endpoint is added to your account in the **Stopped** state.</span></span> <span data-ttu-id="d6133-133">您想要串流內容的串流端點必須處於 [執行中] 狀態。</span><span class="sxs-lookup"><span data-stu-id="d6133-133">The streaming endpoint from which you want to stream content has to be in the **Running** state.</span></span> 

12. <span data-ttu-id="d6133-134">當您準備好開始串流和封存時，請啟動程式。</span><span class="sxs-lookup"><span data-stu-id="d6133-134">Start the program when you are ready to start streaming and archiving.</span></span>
13. <span data-ttu-id="d6133-135">即時編碼器會收到啟動公告的信號 (選擇性)。</span><span class="sxs-lookup"><span data-stu-id="d6133-135">Optionally, the live encoder can be signaled to start an advertisement.</span></span> <span data-ttu-id="d6133-136">公告會插入輸出串流中。</span><span class="sxs-lookup"><span data-stu-id="d6133-136">The advertisement is inserted in the output stream.</span></span>
14. <span data-ttu-id="d6133-137">每當您想要停止串流處理和封存事件時，請停止程式。</span><span class="sxs-lookup"><span data-stu-id="d6133-137">Stop the program whenever you want to stop streaming and archiving the event.</span></span>
15. <span data-ttu-id="d6133-138">刪除程式 (並選擇性地刪除資產)。</span><span class="sxs-lookup"><span data-stu-id="d6133-138">Delete the Program (and optionally delete the asset).</span></span>

## <a name="what-youll-learn"></a><span data-ttu-id="d6133-139">您將學到什麼</span><span class="sxs-lookup"><span data-stu-id="d6133-139">What you'll learn</span></span>
<span data-ttu-id="d6133-140">本主題示範如何使用 Media Services.NET SDK 在通道上執行不同的作業和程式。</span><span class="sxs-lookup"><span data-stu-id="d6133-140">This topic shows you how to execute different operations on channels and programs using Media Services .NET SDK.</span></span> <span data-ttu-id="d6133-141">因為許多作業會長時間執行，所以會使用管理長時間執行作業的 .NET API。</span><span class="sxs-lookup"><span data-stu-id="d6133-141">Because many operations are long-running .NET APIs that manage long running operations are used.</span></span>

<span data-ttu-id="d6133-142">本主題示範如何執行下列動作：</span><span class="sxs-lookup"><span data-stu-id="d6133-142">The topic shows how to do the following:</span></span>

1. <span data-ttu-id="d6133-143">建立並啟動通道。</span><span class="sxs-lookup"><span data-stu-id="d6133-143">Create and start a channel.</span></span> <span data-ttu-id="d6133-144">使用長時間執行的 API。</span><span class="sxs-lookup"><span data-stu-id="d6133-144">Long-running APIs are used.</span></span>
2. <span data-ttu-id="d6133-145">取得通道內嵌 (輸入) 端點。</span><span class="sxs-lookup"><span data-stu-id="d6133-145">Get the channels ingest (input) endpoint.</span></span> <span data-ttu-id="d6133-146">此端點應該提供給可以傳送單一位元速率即時串流的編碼器。</span><span class="sxs-lookup"><span data-stu-id="d6133-146">This endpoint should be provided to the encoder that can send a single bitrate live stream.</span></span>
3. <span data-ttu-id="d6133-147">取得預覽端點。</span><span class="sxs-lookup"><span data-stu-id="d6133-147">Get the preview endpoint.</span></span> <span data-ttu-id="d6133-148">此端點可用來預覽您的串流。</span><span class="sxs-lookup"><span data-stu-id="d6133-148">This endpoint is used to preview your stream.</span></span>
4. <span data-ttu-id="d6133-149">建立將用來儲存內容的資產。</span><span class="sxs-lookup"><span data-stu-id="d6133-149">Create an asset that will be used to store your content.</span></span> <span data-ttu-id="d6133-150">資產傳遞原則也應該另外設定，如此範例中所示。</span><span class="sxs-lookup"><span data-stu-id="d6133-150">The asset delivery policies should be configured as well, as shown in this example.</span></span>
5. <span data-ttu-id="d6133-151">建立程式，並指定使用稍早建立的資產。</span><span class="sxs-lookup"><span data-stu-id="d6133-151">Create a program and specify to use the asset that was created earlier.</span></span> <span data-ttu-id="d6133-152">啟動程式。</span><span class="sxs-lookup"><span data-stu-id="d6133-152">Start the program.</span></span> <span data-ttu-id="d6133-153">使用長時間執行的 API。</span><span class="sxs-lookup"><span data-stu-id="d6133-153">Long-running APIs are used.</span></span>
6. <span data-ttu-id="d6133-154">建立資產的定位器，讓內容發行，並且可以串流至用戶端。</span><span class="sxs-lookup"><span data-stu-id="d6133-154">Create a locator for the asset, so the content gets published and can be streamed to your clients.</span></span>
7. <span data-ttu-id="d6133-155">顯示和隱藏 slate。</span><span class="sxs-lookup"><span data-stu-id="d6133-155">Show and hide slates.</span></span> <span data-ttu-id="d6133-156">啟動和停止公告。</span><span class="sxs-lookup"><span data-stu-id="d6133-156">Start and stop advertisements.</span></span> <span data-ttu-id="d6133-157">使用長時間執行的 API。</span><span class="sxs-lookup"><span data-stu-id="d6133-157">Long-running APIs are used.</span></span>
8. <span data-ttu-id="d6133-158">清除您的通道和所有相關聯的資源。</span><span class="sxs-lookup"><span data-stu-id="d6133-158">Clean up your channel and all the associated resources.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d6133-159">必要條件</span><span class="sxs-lookup"><span data-stu-id="d6133-159">Prerequisites</span></span>
<span data-ttu-id="d6133-160">需要有下列項目，才能完成教學課程。</span><span class="sxs-lookup"><span data-stu-id="d6133-160">The following are required to complete the tutorial.</span></span>

* <span data-ttu-id="d6133-161">一個 Azure 帳戶。</span><span class="sxs-lookup"><span data-stu-id="d6133-161">An Azure account.</span></span> <span data-ttu-id="d6133-162">如果您沒有帳戶，只需要幾分鐘的時間就可以建立免費試用帳戶。</span><span class="sxs-lookup"><span data-stu-id="d6133-162">If you don't have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="d6133-163">如需詳細資訊，請參閱 [Azure 免費試用](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F)。</span><span class="sxs-lookup"><span data-stu-id="d6133-163">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F).</span></span> <span data-ttu-id="d6133-164">您將獲得能用來試用 Azure 付費服務的額度。</span><span class="sxs-lookup"><span data-stu-id="d6133-164">You get credits that can be used to try out paid Azure services.</span></span> <span data-ttu-id="d6133-165">即使在額度用完後，您仍可保留帳戶，並使用免費的 Azure 服務和功能，例如 Azure App Service 中的 Web Apps 功能。</span><span class="sxs-lookup"><span data-stu-id="d6133-165">Even after the credits are used up, you can keep the account and use free Azure services and features, such as the Web Apps feature in Azure App Service.</span></span>
* <span data-ttu-id="d6133-166">媒體服務帳戶。</span><span class="sxs-lookup"><span data-stu-id="d6133-166">A Media Services account.</span></span> <span data-ttu-id="d6133-167">若要建立媒體服務帳戶，請參閱 [建立帳戶](media-services-portal-create-account.md)。</span><span class="sxs-lookup"><span data-stu-id="d6133-167">To create a Media Services account, see [Create Account](media-services-portal-create-account.md).</span></span>
* <span data-ttu-id="d6133-168">Visual Studio 2010 SP1 (Professional、Premium、Ultimate 或 Express) 或較新版本。</span><span class="sxs-lookup"><span data-stu-id="d6133-168">Visual Studio 2010 SP1 (Professional, Premium, Ultimate, or Express) or later versions.</span></span>
* <span data-ttu-id="d6133-169">您必須使用媒體服務 .NET SDK 3.2.0.0 版或更新版本。</span><span class="sxs-lookup"><span data-stu-id="d6133-169">You must use Media Services .NET SDK version 3.2.0.0 or newer.</span></span>
* <span data-ttu-id="d6133-170">網路攝影機以及可以傳送單一位元速率即時串流的編碼器。</span><span class="sxs-lookup"><span data-stu-id="d6133-170">A webcam and an encoder that can send a single bitrate live stream.</span></span>

## <a name="considerations"></a><span data-ttu-id="d6133-171">考量</span><span class="sxs-lookup"><span data-stu-id="d6133-171">Considerations</span></span>
* <span data-ttu-id="d6133-172">目前，即時事件的最大建議持續時間是 8 小時。</span><span class="sxs-lookup"><span data-stu-id="d6133-172">Currently, the max recommended duration of a live event is 8 hours.</span></span> <span data-ttu-id="d6133-173">如果您需要較長的時間來執行通道，請連絡 amslived@Microsoft.com。</span><span class="sxs-lookup"><span data-stu-id="d6133-173">Please contact amslived at Microsoft.com if you need to run a Channel for longer periods of time.</span></span>
* <span data-ttu-id="d6133-174">對於不同的 AMS 原則 (例如 Locator 原則或 ContentKeyAuthorizationPolicy) 有 1,000,000 個原則的限制。</span><span class="sxs-lookup"><span data-stu-id="d6133-174">There is a limit of 1,000,000 policies for different AMS policies (for example, for Locator policy or ContentKeyAuthorizationPolicy).</span></span> <span data-ttu-id="d6133-175">如果您一律使用相同的日期 / 存取權限，例如，要長時間維持就地 (非上載原則) 的定位器原則，您應該使用相同的原則識別碼。</span><span class="sxs-lookup"><span data-stu-id="d6133-175">You should use the same policy ID if you are always using the same days / access permissions, for example, policies for locators that are intended to remain in place for a long time (non-upload policies).</span></span> <span data-ttu-id="d6133-176">如需詳細資訊，請參閱 [這個](media-services-dotnet-manage-entities.md#limit-access-policies) 主題。</span><span class="sxs-lookup"><span data-stu-id="d6133-176">For more information, see [this](media-services-dotnet-manage-entities.md#limit-access-policies) topic.</span></span>

## <a name="download-sample"></a><span data-ttu-id="d6133-177">下載範例</span><span class="sxs-lookup"><span data-stu-id="d6133-177">Download sample</span></span>

<span data-ttu-id="d6133-178">您可以從[這裡](https://azure.microsoft.com/documentation/samples/media-services-dotnet-encode-live-stream-with-ams-clear/)下載本主題所述的範例。</span><span class="sxs-lookup"><span data-stu-id="d6133-178">You can download the sample that is described in this topic from [here](https://azure.microsoft.com/documentation/samples/media-services-dotnet-encode-live-stream-with-ams-clear/).</span></span>

## <a name="set-up-for-development-with-media-services-sdk-for-net"></a><span data-ttu-id="d6133-179">設定使用媒體服務 SDK for.NET 的開發</span><span class="sxs-lookup"><span data-stu-id="d6133-179">Set up for development with Media Services SDK for .NET</span></span>

<span data-ttu-id="d6133-180">設定您的開發環境並在 app.config 檔案中填入連線資訊，如[使用 .NET 進行 Media Services 開發](media-services-dotnet-how-to-use.md)所述。</span><span class="sxs-lookup"><span data-stu-id="d6133-180">Set up your development environment and populate the app.config file with connection information, as described in [Media Services development with .NET](media-services-dotnet-how-to-use.md).</span></span> 

## <a name="code-example"></a><span data-ttu-id="d6133-181">程式碼範例</span><span class="sxs-lookup"><span data-stu-id="d6133-181">Code example</span></span>

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

        // Read values from the App.config file.
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

            // The channel's input endpoint:
            string ingestUrl = channel.Input.Endpoints.FirstOrDefault().Url.ToString();

            Console.WriteLine("Intest URL: {0}", ingestUrl);


            // Use the previewEndpoint to preview and verify 
            // that the input from the encoder is actually reaching the Channel. 
            string previewEndpoint = channel.Preview.Endpoints.FirstOrDefault().Url.ToString();

            Console.WriteLine("Preview URL: {0}", previewEndpoint);

            // When Live Encoding is enabled, you can now get a preview of the live feed as it reaches the Channel. 
            // This can be a valuable tool to check whether your live feed is actually reaching the Channel. 
            // The thumbnail is exposed via the same end-point as the Channel Preview URL.
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

            // You can use slates and ads only if the channel type is Standard.  
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
            // You can only set audio if streaming protocol is set to StreamingProtocol.RTPMPEG2TS.
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
        /// Create a Program on the Channel. You can have multiple Programs that overlap or are sequential;
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
        /// Create locators in order to be able to publish and stream the video.
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
        /// Clean up resources associated with the channel.
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

            Log("starting to track ", null, operation.Id);
            while (isCompleted == false)
            {
            operation = _context.Operations.GetOperation(operation.Id);
            isCompleted = IsCompleted(operation, out entityId);
            System.Threading.Thread.Sleep(TimeSpan.FromSeconds(30));
            }
            // If we got here, the operation succeeded.
            Log(description + " in completed", operation.TargetEntityId, operation.Id);

            return entityId;
        }

        /// <summary> 
        /// Checks if the operation has been completed. 
        /// If the operation succeeded, the created entity Id is returned in the out parameter.
        /// </summary> 
        /// <param name="operationId">The operation Id.</param> 
        /// <param name="channel">
        /// If the operation succeeded, 
        /// the entity Id associated with the sucessful operation is returned in the out parameter.</param>
        /// <returns>Returns false if the operation is still in progress; otherwise, true.</returns> 
        private static bool IsCompleted(IOperation operation, out string entityId)
        {
            bool completed = false;

            entityId = null;

            switch (operation.State)
            {
            case OperationState.Failed:
                // Handle the failure. 
                // For example, throw an exception. 
                // Use the following information in the exception: operationId, operation.ErrorMessage.
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

## <a name="next-step"></a><span data-ttu-id="d6133-182">後續步驟</span><span class="sxs-lookup"><span data-stu-id="d6133-182">Next step</span></span>
<span data-ttu-id="d6133-183">檢閱媒體服務學習路徑。</span><span class="sxs-lookup"><span data-stu-id="d6133-183">Review Media Services learning paths.</span></span>

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="d6133-184">提供意見反應</span><span class="sxs-lookup"><span data-stu-id="d6133-184">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]


