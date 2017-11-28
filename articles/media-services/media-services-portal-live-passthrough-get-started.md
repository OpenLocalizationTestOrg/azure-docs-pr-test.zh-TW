---
title: "aaaLive 資料流，與在內部部署編碼器使用 hello Azure 入口網站 |Microsoft 文件"
description: "本教學課程會引導您建立設定為傳遞的傳遞通道的 hello 步驟。"
services: media-services
documentationcenter: 
author: juliako
manager: cfowler
editor: 
ms.assetid: 6f4acd95-cc64-4dd9-9e2d-8734707de326
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 08/09/2017
ms.author: juliako
ms.openlocfilehash: 1fb341e022f66f33903e13e07d3e84c0216cad77
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooperform-live-streaming-with-on-premises-encoders-using-hello-azure-portal"></a><span data-ttu-id="ed468-103">如何 tooperform 即時資料流與內部部署編碼器使用 hello Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="ed468-103">How tooperform live streaming with on-premises encoders using hello Azure portal</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="ed468-104">入口網站</span><span class="sxs-lookup"><span data-stu-id="ed468-104">Portal</span></span>](media-services-portal-live-passthrough-get-started.md)
> * [<span data-ttu-id="ed468-105">.NET</span><span class="sxs-lookup"><span data-stu-id="ed468-105">.NET</span></span>](media-services-dotnet-live-encode-with-onpremises-encoders.md)
> * [<span data-ttu-id="ed468-106">REST</span><span class="sxs-lookup"><span data-stu-id="ed468-106">REST</span></span>](https://docs.microsoft.com/rest/api/media/operations/channel)
> 
> 

<span data-ttu-id="ed468-107">本教學課程中引導您使用 Azure 入口網站 toocreate hello 的 hello 步驟**通道**針對傳遞的傳遞設定。</span><span class="sxs-lookup"><span data-stu-id="ed468-107">This tutorial walks you through hello steps of using hello Azure portal toocreate a **Channel** that is configured for a pass-through delivery.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="ed468-108">必要條件</span><span class="sxs-lookup"><span data-stu-id="ed468-108">Prerequisites</span></span>
<span data-ttu-id="ed468-109">hello 下面是必要的 toocomplete hello 教學課程：</span><span class="sxs-lookup"><span data-stu-id="ed468-109">hello following are required toocomplete hello tutorial:</span></span>

* <span data-ttu-id="ed468-110">一個 Azure 帳戶。</span><span class="sxs-lookup"><span data-stu-id="ed468-110">An Azure account.</span></span> <span data-ttu-id="ed468-111">如需詳細資訊，請參閱 [Azure 免費試用](https://azure.microsoft.com/pricing/free-trial/)。</span><span class="sxs-lookup"><span data-stu-id="ed468-111">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/).</span></span> 
* <span data-ttu-id="ed468-112">媒體服務帳戶。</span><span class="sxs-lookup"><span data-stu-id="ed468-112">A Media Services account.</span></span> <span data-ttu-id="ed468-113">toocreate Media Services 帳戶，請參閱[如何 tooCreate Media Services 帳戶](media-services-portal-create-account.md)。</span><span class="sxs-lookup"><span data-stu-id="ed468-113">toocreate a Media Services account, see [How tooCreate a Media Services Account](media-services-portal-create-account.md).</span></span>
* <span data-ttu-id="ed468-114">網路攝影機。</span><span class="sxs-lookup"><span data-stu-id="ed468-114">A webcam.</span></span> <span data-ttu-id="ed468-115">例如， [Telestream Wirecast 編碼器](http://www.telestream.net/wirecast/overview.htm)。</span><span class="sxs-lookup"><span data-stu-id="ed468-115">For example, [Telestream Wirecast encoder](http://www.telestream.net/wirecast/overview.htm).</span></span>

<span data-ttu-id="ed468-116">強烈建議 tooreview hello 下列文章：</span><span class="sxs-lookup"><span data-stu-id="ed468-116">It is highly recommended tooreview hello following articles:</span></span>

* [<span data-ttu-id="ed468-117">Azure 媒體服務 RTMP 支援和即時編碼器</span><span class="sxs-lookup"><span data-stu-id="ed468-117">Azure Media Services RTMP Support and Live Encoders</span></span>](https://azure.microsoft.com/blog/2014/09/18/azure-media-services-rtmp-support-and-live-encoders/)
* [<span data-ttu-id="ed468-118">使用 Azure 媒體服務之即時串流的概觀</span><span class="sxs-lookup"><span data-stu-id="ed468-118">Overview of Live Steaming using Azure Media Services</span></span>](media-services-manage-channels-overview.md)
* [<span data-ttu-id="ed468-119">使用會建立多位元速率串流的內部部署編碼器執行即時串流</span><span class="sxs-lookup"><span data-stu-id="ed468-119">Live streaming with on-premises encoders that create multi-bitrate streams</span></span>](media-services-live-streaming-with-onprem-encoders.md)

## <span data-ttu-id="ed468-120"><a id="scenario"></a>常見即時串流案例</span><span class="sxs-lookup"><span data-stu-id="ed468-120"><a id="scenario"></a>Common live streaming scenario</span></span>
<span data-ttu-id="ed468-121">hello 下列步驟說明建立常見即時資料流使用的應用程式所設定的通道傳遞傳遞所涉及的工作。</span><span class="sxs-lookup"><span data-stu-id="ed468-121">hello following steps describe tasks involved in creating common live streaming applications that use channels that are configured for pass-through delivery.</span></span> <span data-ttu-id="ed468-122">本教學課程示範如何 toocreate 及管理通過通道和即時事件。</span><span class="sxs-lookup"><span data-stu-id="ed468-122">This tutorial shows how toocreate and manage a pass-through channel and live events.</span></span>

>[!NOTE]
><span data-ttu-id="ed468-123">請確定 hello 串流的端點要從中 toostream 內容處於 hello**執行**狀態。</span><span class="sxs-lookup"><span data-stu-id="ed468-123">Make sure hello streaming endpoint from which you want toostream content is in hello **Running** state.</span></span> 
    
1. <span data-ttu-id="ed468-124">視訊攝影機 tooa 電腦連線。</span><span class="sxs-lookup"><span data-stu-id="ed468-124">Connect a video camera tooa computer.</span></span> <span data-ttu-id="ed468-125">啟動並設定內部部署即時編碼器，讓它輸出多位元速率 RTMP 或 Fragmented MP4 串流。</span><span class="sxs-lookup"><span data-stu-id="ed468-125">Launch and configure an on-premises live encoder that outputs a multi-bitrate RTMP or Fragmented MP4 stream.</span></span> <span data-ttu-id="ed468-126">如需詳細資訊，請參閱 [Azure 媒體服務 RTMP 支援和即時編碼器](http://go.microsoft.com/fwlink/?LinkId=532824)。</span><span class="sxs-lookup"><span data-stu-id="ed468-126">For more information, see [Azure Media Services RTMP Support and Live Encoders](http://go.microsoft.com/fwlink/?LinkId=532824).</span></span>
   
    <span data-ttu-id="ed468-127">此步驟也可以在您建立通道之後執行。</span><span class="sxs-lookup"><span data-stu-id="ed468-127">This step could also be performed after you create your Channel.</span></span>
2. <span data-ttu-id="ed468-128">建立並啟動即時通行通道。</span><span class="sxs-lookup"><span data-stu-id="ed468-128">Create and start a pass-through Channel.</span></span>
3. <span data-ttu-id="ed468-129">擷取 hello 通道的內嵌 URL。</span><span class="sxs-lookup"><span data-stu-id="ed468-129">Retrieve hello Channel ingest URL.</span></span> 
   
    <span data-ttu-id="ed468-130">hello 內嵌 URL 由 hello 即時編碼器 toosend hello 資料流 toohello 通道。</span><span class="sxs-lookup"><span data-stu-id="ed468-130">hello ingest URL is used by hello live encoder toosend hello stream toohello Channel.</span></span>
4. <span data-ttu-id="ed468-131">擷取 hello 通道預覽 URL。</span><span class="sxs-lookup"><span data-stu-id="ed468-131">Retrieve hello Channel preview URL.</span></span> 
   
    <span data-ttu-id="ed468-132">使用您的通道可正常接收即時資料流 hello 這個 URL tooverify。</span><span class="sxs-lookup"><span data-stu-id="ed468-132">Use this URL tooverify that your channel is properly receiving hello live stream.</span></span>
5. <span data-ttu-id="ed468-133">建立即時事件/程式。</span><span class="sxs-lookup"><span data-stu-id="ed468-133">Create a live event/program.</span></span> 
   
    <span data-ttu-id="ed468-134">當使用 hello Azure 入口網站時，建立即時事件也會建立資產。</span><span class="sxs-lookup"><span data-stu-id="ed468-134">When using hello Azure portal, creating a live event also creates an asset.</span></span> 

6. <span data-ttu-id="ed468-135">當您準備好 toostart 串流和封存時啟動 hello 事件/程式。</span><span class="sxs-lookup"><span data-stu-id="ed468-135">Start hello event/program when you are ready toostart streaming and archiving.</span></span>
7. <span data-ttu-id="ed468-136">（選擇性） hello 即時編碼器可以信號的 toostart 公告。</span><span class="sxs-lookup"><span data-stu-id="ed468-136">Optionally, hello live encoder can be signaled toostart an advertisement.</span></span> <span data-ttu-id="ed468-137">hello 公告 hello 輸出資料流中插入。</span><span class="sxs-lookup"><span data-stu-id="ed468-137">hello advertisement is inserted in hello output stream.</span></span>
8. <span data-ttu-id="ed468-138">每當您想 toostop 串流並封存 hello 事件時，請停止 hello 事件/程式。</span><span class="sxs-lookup"><span data-stu-id="ed468-138">Stop hello event/program whenever you want toostop streaming and archiving hello event.</span></span>
9. <span data-ttu-id="ed468-139">刪除 hello 事件/程式，並選擇性地刪除 hello 資產。</span><span class="sxs-lookup"><span data-stu-id="ed468-139">Delete hello event/program (and optionally delete hello asset).</span></span>     

> [!IMPORTANT]
> <span data-ttu-id="ed468-140">請檢閱[建立多位元速率串流的內部編碼器進行即時資料流處理](media-services-live-streaming-with-onprem-encoders.md)toolearn 概念和考量相關 toolive 內部編碼器和傳遞通道進行資料流處理。</span><span class="sxs-lookup"><span data-stu-id="ed468-140">Please review [Live streaming with on-premises encoders that create multi-bitrate streams](media-services-live-streaming-with-onprem-encoders.md) toolearn about concepts and considerations related toolive streaming with on-premises encoders and pass-through channels.</span></span>
> 
> 

## <a name="tooview-notifications-and-errors"></a><span data-ttu-id="ed468-141">tooview 通知和錯誤</span><span class="sxs-lookup"><span data-stu-id="ed468-141">tooview notifications and errors</span></span>
<span data-ttu-id="ed468-142">如果您希望 tooview 通知錯誤所產生的 hello Azure 入口網站，請按一下 hello 通知圖示。</span><span class="sxs-lookup"><span data-stu-id="ed468-142">If you want tooview notifications and errors produced by hello Azure portal, click on hello Notification icon.</span></span>

![通知](./media/media-services-portal-passthrough-get-started/media-services-notifications.png)

## <a name="create-and-start-pass-through-channels-and-events"></a><span data-ttu-id="ed468-144">建立並啟動即時通行通道和事件</span><span class="sxs-lookup"><span data-stu-id="ed468-144">Create and start pass-through channels and events</span></span>
<span data-ttu-id="ed468-145">通道是 toocontrol hello 發行和即時串流片段的儲存體可讓您的事件/程式相關聯。</span><span class="sxs-lookup"><span data-stu-id="ed468-145">A channel is associated with events/programs that enable you toocontrol hello publishing and storage of segments in a live stream.</span></span> <span data-ttu-id="ed468-146">通道會管理事件。</span><span class="sxs-lookup"><span data-stu-id="ed468-146">Channels manage events.</span></span> 

<span data-ttu-id="ed468-147">您可以指定您想要 tooretain hello 記錄內容 hello 程式設定 hello 的 hello 數**封存時間長度**長度。</span><span class="sxs-lookup"><span data-stu-id="ed468-147">You can specify hello number of hours you want tooretain hello recorded content for hello program by setting hello **Archive Window** length.</span></span> <span data-ttu-id="ed468-148">這個值可以設定為 5 分鐘 tooa 最多 25 個小時的最小值。</span><span class="sxs-lookup"><span data-stu-id="ed468-148">This value can be set from a minimum of 5 minutes tooa maximum of 25 hours.</span></span> <span data-ttu-id="ed468-149">封存時間長度也會規定 hello 最大用戶端可以從 hello 目前即時位置搜尋的時間量。</span><span class="sxs-lookup"><span data-stu-id="ed468-149">Archive window length also dictates hello maximum amount of time clients can seek back in time from hello current live position.</span></span> <span data-ttu-id="ed468-150">事件可以透過 hello 指定時間內，執行但落後 hello 時間長度的內容會持續遭到捨棄。</span><span class="sxs-lookup"><span data-stu-id="ed468-150">Events can run over hello specified amount of time, but content that falls behind hello window length is continuously discarded.</span></span> <span data-ttu-id="ed468-151">這個屬性的值也會決定資訊清單所能成長的時間長度 hello 用戶端。</span><span class="sxs-lookup"><span data-stu-id="ed468-151">This value of this property also determines how long hello client manifests can grow.</span></span>

<span data-ttu-id="ed468-152">每個事件都是與資產相關聯。</span><span class="sxs-lookup"><span data-stu-id="ed468-152">Each event is associated with an asset.</span></span> <span data-ttu-id="ed468-153">toopublish hello 事件，您必須建立 OnDemand 定位器 hello 相關聯的資產。</span><span class="sxs-lookup"><span data-stu-id="ed468-153">toopublish hello event, you must create an OnDemand locator for hello associated asset.</span></span> <span data-ttu-id="ed468-154">擁有這個定位器，可讓您 toobuild 您可以提供 tooyour 用戶端的串流 URL。</span><span class="sxs-lookup"><span data-stu-id="ed468-154">Having this locator enables you toobuild a streaming URL that you can provide tooyour clients.</span></span>

<span data-ttu-id="ed468-155">一個通道可支援同時執行的事件，因此您可以建立多個封存 hello toothree 註冊相同的傳入資料流。</span><span class="sxs-lookup"><span data-stu-id="ed468-155">A channel supports up toothree concurrently running events so you can create multiple archives of hello same incoming stream.</span></span> <span data-ttu-id="ed468-156">這可讓您 toopublish 和封存的事件所需的不同部分。</span><span class="sxs-lookup"><span data-stu-id="ed468-156">This allows you toopublish and archive different parts of an event as needed.</span></span> <span data-ttu-id="ed468-157">例如，您的商務需求是 tooarchive 6 小時的程式，但 toobroadcast 最後的 10 分鐘。</span><span class="sxs-lookup"><span data-stu-id="ed468-157">For example, your business requirement is tooarchive 6 hours of a program, but toobroadcast only last 10 minutes.</span></span> <span data-ttu-id="ed468-158">tooaccomplish，您需要 toocreate 兩個同時執行的程式。</span><span class="sxs-lookup"><span data-stu-id="ed468-158">tooaccomplish this, you need toocreate two concurrently running programs.</span></span> <span data-ttu-id="ed468-159">一個程式設 tooarchive 6 小時的 hello 事件，但 hello 程式不會發行。</span><span class="sxs-lookup"><span data-stu-id="ed468-159">One program is set tooarchive 6 hours of hello event but hello program is not published.</span></span> <span data-ttu-id="ed468-160">hello 其他程式的組 tooarchive 為 10 分鐘並發佈此程式。</span><span class="sxs-lookup"><span data-stu-id="ed468-160">hello other program is set tooarchive for 10 minutes and this program is published.</span></span>

<span data-ttu-id="ed468-161">您不應該重複使用現有的即時事件。</span><span class="sxs-lookup"><span data-stu-id="ed468-161">You should not reuse existing live events.</span></span> <span data-ttu-id="ed468-162">而是針對每個事件建立並啟動新事件。</span><span class="sxs-lookup"><span data-stu-id="ed468-162">Instead, create and start a new event for each event.</span></span>

<span data-ttu-id="ed468-163">啟動 hello 事件，當您準備好 toostart 串流和封存時。</span><span class="sxs-lookup"><span data-stu-id="ed468-163">Start hello event when you are ready toostart streaming and archiving.</span></span> <span data-ttu-id="ed468-164">每當您想 toostop 串流並封存 hello 事件時，請停止 hello 程式。</span><span class="sxs-lookup"><span data-stu-id="ed468-164">Stop hello program whenever you want toostop streaming and archiving hello event.</span></span> 

<span data-ttu-id="ed468-165">toodelete 封存內容時，會停止和刪除 hello 事件，然後再刪除 hello 相關聯的資產。</span><span class="sxs-lookup"><span data-stu-id="ed468-165">toodelete archived content, stop and delete hello event and then delete hello associated asset.</span></span> <span data-ttu-id="ed468-166">無法刪除資產，如果它由事件。必須先刪除 hello 事件。</span><span class="sxs-lookup"><span data-stu-id="ed468-166">An asset cannot be deleted if it is used by an event; hello event must be deleted first.</span></span> 

<span data-ttu-id="ed468-167">即使您停止並刪除 hello 事件之後，hello 使用者是無法 toostream 封存的內容，視視訊，只要您不要刪除 hello 資產。</span><span class="sxs-lookup"><span data-stu-id="ed468-167">Even after you stop and delete hello event, hello users would be able toostream your archived content as a video on demand, for as long as you do not delete hello asset.</span></span>

<span data-ttu-id="ed468-168">若要封存的 tooretain hello 內容，而不是需要它提供給串流，刪除 hello 串流定位器。</span><span class="sxs-lookup"><span data-stu-id="ed468-168">If you do want tooretain hello archived content, but not have it available for streaming, delete hello streaming locator.</span></span>

### <a name="toouse-hello-portal-toocreate-a-channel"></a><span data-ttu-id="ed468-169">toouse hello 入口 toocreate 通道</span><span class="sxs-lookup"><span data-stu-id="ed468-169">toouse hello portal toocreate a channel</span></span>
<span data-ttu-id="ed468-170">此區段會顯示如何 toouse hello**快速建立**選項 toocreate 通過通道。</span><span class="sxs-lookup"><span data-stu-id="ed468-170">This section shows how toouse hello **Quick Create** option toocreate a pass-through channel.</span></span>

<span data-ttu-id="ed468-171">如需傳遞通道的詳細資訊，請參閱[使用會從建立多位元速率串流的內部部署編碼器執行即時串流](media-services-live-streaming-with-onprem-encoders.md)。</span><span class="sxs-lookup"><span data-stu-id="ed468-171">For more details about pass-through channels, see [Live streaming with on-premises encoders that create multi-bitrate streams](media-services-live-streaming-with-onprem-encoders.md).</span></span>

1. <span data-ttu-id="ed468-172">在 hello [Azure 入口網站](https://portal.azure.com/)，選取您的 Azure Media Services 帳戶。</span><span class="sxs-lookup"><span data-stu-id="ed468-172">In hello [Azure portal](https://portal.azure.com/), select your Azure Media Services account.</span></span>
2. <span data-ttu-id="ed468-173">在 hello**設定**視窗中，按一下 **即時資料流**。</span><span class="sxs-lookup"><span data-stu-id="ed468-173">In hello **Settings** window, click **Live streaming**.</span></span> 
   
    ![開始使用](./media/media-services-portal-passthrough-get-started/media-services-getting-started.png)
   
    <span data-ttu-id="ed468-175">hello**即時資料流** 視窗隨即出現。</span><span class="sxs-lookup"><span data-stu-id="ed468-175">hello **Live streaming** window appears.</span></span>
3. <span data-ttu-id="ed468-176">按一下**快速建立**toocreate 通過通道以 hello RTMP 內嵌通訊協定。</span><span class="sxs-lookup"><span data-stu-id="ed468-176">Click **Quick Create** toocreate a pass-through channel with hello RTMP ingest protocol.</span></span>
   
    <span data-ttu-id="ed468-177">hello**建立新的通道** 視窗隨即出現。</span><span class="sxs-lookup"><span data-stu-id="ed468-177">hello **CREATE A NEW CHANNEL** window appears.</span></span>
4. <span data-ttu-id="ed468-178">提供 hello 新通道名稱，然後按一下 **建立**。</span><span class="sxs-lookup"><span data-stu-id="ed468-178">Give hello new channel a name and click **Create**.</span></span> 
   
    <span data-ttu-id="ed468-179">這會建立 hello 通過通道 RTMP 內嵌通訊協定。</span><span class="sxs-lookup"><span data-stu-id="ed468-179">This creates a pass-through channel with hello RTMP ingest protocol.</span></span>

## <a name="create-events"></a><span data-ttu-id="ed468-180">建立事件</span><span class="sxs-lookup"><span data-stu-id="ed468-180">Create events</span></span>
1. <span data-ttu-id="ed468-181">選取您想要 tooadd 事件通道 toowhich。</span><span class="sxs-lookup"><span data-stu-id="ed468-181">Select a channel toowhich you want tooadd an event.</span></span>
2. <span data-ttu-id="ed468-182">按下 [即時事件]  按鈕。</span><span class="sxs-lookup"><span data-stu-id="ed468-182">Press **Live Event** button.</span></span>

![Event](./media/media-services-portal-passthrough-get-started/media-services-create-events.png)

## <a name="get-ingest-urls"></a><span data-ttu-id="ed468-184">取得內嵌 URL</span><span class="sxs-lookup"><span data-stu-id="ed468-184">Get ingest URLs</span></span>
<span data-ttu-id="ed468-185">一旦建立 hello 通道之後，您可以取得內嵌您將會提供 toohello 即時編碼器的 Url。</span><span class="sxs-lookup"><span data-stu-id="ed468-185">Once hello channel is created, you can get ingest URLs that you will provide toohello live encoder.</span></span> <span data-ttu-id="ed468-186">hello 編碼器使用這些 Url tooinput 即時資料流。</span><span class="sxs-lookup"><span data-stu-id="ed468-186">hello encoder uses these URLs tooinput a live stream.</span></span>

![建立時間](./media/media-services-portal-passthrough-get-started/media-services-channel-created.png)

## <a name="watch-hello-event"></a><span data-ttu-id="ed468-188">監看式 hello 事件</span><span class="sxs-lookup"><span data-stu-id="ed468-188">Watch hello event</span></span>
<span data-ttu-id="ed468-189">toowatch hello 事件中，按一下 **監看式**在 hello Azure 入口網站 或 複製 hello 串流 URL，並使用您選擇的播放程式。</span><span class="sxs-lookup"><span data-stu-id="ed468-189">toowatch hello event, click **Watch** in hello Azure portal or copy hello streaming URL and use a player of your choice.</span></span> 

![建立時間](./media/media-services-portal-passthrough-get-started/media-services-default-event.png)

<span data-ttu-id="ed468-191">實況事件時會自動取得轉換的 tooon 要求內容時停止。</span><span class="sxs-lookup"><span data-stu-id="ed468-191">Live event automatically get converted tooon-demand content when stopped.</span></span>

## <a name="clean-up"></a><span data-ttu-id="ed468-192">清除</span><span class="sxs-lookup"><span data-stu-id="ed468-192">Clean up</span></span>
<span data-ttu-id="ed468-193">如需傳遞通道的詳細資訊，請參閱[使用會從建立多位元速率串流的內部部署編碼器執行即時串流](media-services-live-streaming-with-onprem-encoders.md)。</span><span class="sxs-lookup"><span data-stu-id="ed468-193">For more details about pass-through channels, see [Live streaming with on-premises encoders that create multi-bitrate streams](media-services-live-streaming-with-onprem-encoders.md).</span></span>

* <span data-ttu-id="ed468-194">所有事件/程式 hello 通道上都已都停止時，才可都停止通道。</span><span class="sxs-lookup"><span data-stu-id="ed468-194">A channel can be stopped only when all events/programs on hello channel have been stopped.</span></span>  <span data-ttu-id="ed468-195">一旦停止 hello 通道時，它不會不會產生任何費用。</span><span class="sxs-lookup"><span data-stu-id="ed468-195">Once hello Channel is stopped, it does not incur any charges.</span></span> <span data-ttu-id="ed468-196">當您需要 toostart 同樣地，它會有 hello 相同內嵌 URL，您不需要 tooreconfigure 您的編碼器。</span><span class="sxs-lookup"><span data-stu-id="ed468-196">When you need toostart it again, it will have hello same ingest URL so you won't need tooreconfigure your encoder.</span></span>
* <span data-ttu-id="ed468-197">已刪除 hello 通道上的所有即時事件時，才可以刪除通道。</span><span class="sxs-lookup"><span data-stu-id="ed468-197">A channel can be deleted only when all live events on hello channel have been deleted.</span></span>

## <a name="view-archived-content"></a><span data-ttu-id="ed468-198">檢視封存的內容</span><span class="sxs-lookup"><span data-stu-id="ed468-198">View archived content</span></span>
<span data-ttu-id="ed468-199">即使您停止並刪除 hello 事件之後，hello 使用者是無法 toostream 封存的內容，視視訊，只要您不要刪除 hello 資產。</span><span class="sxs-lookup"><span data-stu-id="ed468-199">Even after you stop and delete hello event, hello users would be able toostream your archived content as a video on demand, for as long as you do not delete hello asset.</span></span> <span data-ttu-id="ed468-200">無法刪除資產，如果它由事件。必須先刪除 hello 事件。</span><span class="sxs-lookup"><span data-stu-id="ed468-200">An asset cannot be deleted if it is used by an event; hello event must be deleted first.</span></span> 

<span data-ttu-id="ed468-201">您的資產，選取 toomanage**設定**按一下**資產**。</span><span class="sxs-lookup"><span data-stu-id="ed468-201">toomanage your assets, select **Setting** and click **Assets**.</span></span>

![Assets](./media/media-services-portal-passthrough-get-started/media-services-assets.png)

## <a name="next-step"></a><span data-ttu-id="ed468-203">後續步驟</span><span class="sxs-lookup"><span data-stu-id="ed468-203">Next step</span></span>
<span data-ttu-id="ed468-204">檢閱媒體服務學習路徑。</span><span class="sxs-lookup"><span data-stu-id="ed468-204">Review Media Services learning paths.</span></span>

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="ed468-205">提供意見反應</span><span class="sxs-lookup"><span data-stu-id="ed468-205">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

