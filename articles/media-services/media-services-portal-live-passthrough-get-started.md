---
title: "使用 Azure 入口網站透過內部部署編碼器執行即時串流 | Microsoft Docs"
description: "本教學課程將逐步引導您建立針對即時通行傳遞設定的通道。"
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
ms.openlocfilehash: 6939e3b31c3c1b514df4c559c2d9408fce122a4e
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="how-to-perform-live-streaming-with-on-premises-encoders-using-the-azure-portal"></a><span data-ttu-id="13970-103">如何使用 Azure 入口網站透過內部部署編碼器執行即時串流</span><span class="sxs-lookup"><span data-stu-id="13970-103">How to perform live streaming with on-premises encoders using the Azure portal</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="13970-104">入口網站</span><span class="sxs-lookup"><span data-stu-id="13970-104">Portal</span></span>](media-services-portal-live-passthrough-get-started.md)
> * [<span data-ttu-id="13970-105">.NET</span><span class="sxs-lookup"><span data-stu-id="13970-105">.NET</span></span>](media-services-dotnet-live-encode-with-onpremises-encoders.md)
> * [<span data-ttu-id="13970-106">REST</span><span class="sxs-lookup"><span data-stu-id="13970-106">REST</span></span>](https://docs.microsoft.com/rest/api/media/operations/channel)
> 
> 

<span data-ttu-id="13970-107">本教學課程將逐步引導您使用 Azure 入口網站建立針對即時通行傳遞設定的 **通道** 。</span><span class="sxs-lookup"><span data-stu-id="13970-107">This tutorial walks you through the steps of using the Azure portal to create a **Channel** that is configured for a pass-through delivery.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="13970-108">必要條件</span><span class="sxs-lookup"><span data-stu-id="13970-108">Prerequisites</span></span>
<span data-ttu-id="13970-109">需要有下列項目，才能完成教學課程：</span><span class="sxs-lookup"><span data-stu-id="13970-109">The following are required to complete the tutorial:</span></span>

* <span data-ttu-id="13970-110">一個 Azure 帳戶。</span><span class="sxs-lookup"><span data-stu-id="13970-110">An Azure account.</span></span> <span data-ttu-id="13970-111">如需詳細資訊，請參閱 [Azure 免費試用](https://azure.microsoft.com/pricing/free-trial/)。</span><span class="sxs-lookup"><span data-stu-id="13970-111">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/).</span></span> 
* <span data-ttu-id="13970-112">媒體服務帳戶。</span><span class="sxs-lookup"><span data-stu-id="13970-112">A Media Services account.</span></span> <span data-ttu-id="13970-113">若要建立媒體服務帳戶，請參閱[如何建立媒體服務帳戶](media-services-portal-create-account.md)。</span><span class="sxs-lookup"><span data-stu-id="13970-113">To create a Media Services account, see [How to Create a Media Services Account](media-services-portal-create-account.md).</span></span>
* <span data-ttu-id="13970-114">網路攝影機。</span><span class="sxs-lookup"><span data-stu-id="13970-114">A webcam.</span></span> <span data-ttu-id="13970-115">例如， [Telestream Wirecast 編碼器](http://www.telestream.net/wirecast/overview.htm)。</span><span class="sxs-lookup"><span data-stu-id="13970-115">For example, [Telestream Wirecast encoder](http://www.telestream.net/wirecast/overview.htm).</span></span>

<span data-ttu-id="13970-116">強烈建議您先檢閱下列文章：</span><span class="sxs-lookup"><span data-stu-id="13970-116">It is highly recommended to review the following articles:</span></span>

* [<span data-ttu-id="13970-117">Azure 媒體服務 RTMP 支援和即時編碼器</span><span class="sxs-lookup"><span data-stu-id="13970-117">Azure Media Services RTMP Support and Live Encoders</span></span>](https://azure.microsoft.com/blog/2014/09/18/azure-media-services-rtmp-support-and-live-encoders/)
* [<span data-ttu-id="13970-118">使用 Azure 媒體服務之即時串流的概觀</span><span class="sxs-lookup"><span data-stu-id="13970-118">Overview of Live Steaming using Azure Media Services</span></span>](media-services-manage-channels-overview.md)
* [<span data-ttu-id="13970-119">使用會建立多位元速率串流的內部部署編碼器執行即時串流</span><span class="sxs-lookup"><span data-stu-id="13970-119">Live streaming with on-premises encoders that create multi-bitrate streams</span></span>](media-services-live-streaming-with-onprem-encoders.md)

## <span data-ttu-id="13970-120"><a id="scenario"></a>常見即時串流案例</span><span class="sxs-lookup"><span data-stu-id="13970-120"><a id="scenario"></a>Common live streaming scenario</span></span>
<span data-ttu-id="13970-121">下列步驟描述當我們建立一般即時串流應用程式 (其使用針對即時通行傳遞設定的通道) 時，會涉及到的各種工作。</span><span class="sxs-lookup"><span data-stu-id="13970-121">The following steps describe tasks involved in creating common live streaming applications that use channels that are configured for pass-through delivery.</span></span> <span data-ttu-id="13970-122">本教學課程示範如何建立及管理即時通行通道和即時事件。</span><span class="sxs-lookup"><span data-stu-id="13970-122">This tutorial shows how to create and manage a pass-through channel and live events.</span></span>

>[!NOTE]
><span data-ttu-id="13970-123">確定您想要串流內容的串流端點已處於 [執行中] 狀態。</span><span class="sxs-lookup"><span data-stu-id="13970-123">Make sure the streaming endpoint from which you want to stream content is in the **Running** state.</span></span> 
    
1. <span data-ttu-id="13970-124">將攝影機連接到電腦。</span><span class="sxs-lookup"><span data-stu-id="13970-124">Connect a video camera to a computer.</span></span> <span data-ttu-id="13970-125">啟動並設定內部部署即時編碼器，讓它輸出多位元速率 RTMP 或 Fragmented MP4 串流。</span><span class="sxs-lookup"><span data-stu-id="13970-125">Launch and configure an on-premises live encoder that outputs a multi-bitrate RTMP or Fragmented MP4 stream.</span></span> <span data-ttu-id="13970-126">如需詳細資訊，請參閱 [Azure 媒體服務 RTMP 支援和即時編碼器](http://go.microsoft.com/fwlink/?LinkId=532824)。</span><span class="sxs-lookup"><span data-stu-id="13970-126">For more information, see [Azure Media Services RTMP Support and Live Encoders](http://go.microsoft.com/fwlink/?LinkId=532824).</span></span>
   
    <span data-ttu-id="13970-127">此步驟也可以在您建立通道之後執行。</span><span class="sxs-lookup"><span data-stu-id="13970-127">This step could also be performed after you create your Channel.</span></span>
2. <span data-ttu-id="13970-128">建立並啟動即時通行通道。</span><span class="sxs-lookup"><span data-stu-id="13970-128">Create and start a pass-through Channel.</span></span>
3. <span data-ttu-id="13970-129">擷取通道內嵌 URL。</span><span class="sxs-lookup"><span data-stu-id="13970-129">Retrieve the Channel ingest URL.</span></span> 
   
    <span data-ttu-id="13970-130">內嵌 URL 可供即時編碼器用來傳送串流到通道。</span><span class="sxs-lookup"><span data-stu-id="13970-130">The ingest URL is used by the live encoder to send the stream to the Channel.</span></span>
4. <span data-ttu-id="13970-131">擷取通道預覽 URL。</span><span class="sxs-lookup"><span data-stu-id="13970-131">Retrieve the Channel preview URL.</span></span> 
   
    <span data-ttu-id="13970-132">使用此 URL 來確認您的通道會正確接收即時串流。</span><span class="sxs-lookup"><span data-stu-id="13970-132">Use this URL to verify that your channel is properly receiving the live stream.</span></span>
5. <span data-ttu-id="13970-133">建立即時事件/程式。</span><span class="sxs-lookup"><span data-stu-id="13970-133">Create a live event/program.</span></span> 
   
    <span data-ttu-id="13970-134">使用 Azure 入口網站時，建立即時事件也會建立資產。</span><span class="sxs-lookup"><span data-stu-id="13970-134">When using the Azure portal, creating a live event also creates an asset.</span></span> 

6. <span data-ttu-id="13970-135">當您準備好開始串流和封存時，請啟動事件/程式。</span><span class="sxs-lookup"><span data-stu-id="13970-135">Start the event/program when you are ready to start streaming and archiving.</span></span>
7. <span data-ttu-id="13970-136">即時編碼器會收到啟動公告的信號 (選擇性)。</span><span class="sxs-lookup"><span data-stu-id="13970-136">Optionally, the live encoder can be signaled to start an advertisement.</span></span> <span data-ttu-id="13970-137">公告會插入輸出串流中。</span><span class="sxs-lookup"><span data-stu-id="13970-137">The advertisement is inserted in the output stream.</span></span>
8. <span data-ttu-id="13970-138">每當您想要停止串流處理和封存事件時，請停止事件/程式。</span><span class="sxs-lookup"><span data-stu-id="13970-138">Stop the event/program whenever you want to stop streaming and archiving the event.</span></span>
9. <span data-ttu-id="13970-139">刪除事件/程式 (並選擇性地刪除資產)。</span><span class="sxs-lookup"><span data-stu-id="13970-139">Delete the event/program (and optionally delete the asset).</span></span>     

> [!IMPORTANT]
> <span data-ttu-id="13970-140">請檢閱[使用會建立多位元速率串流的內部部署編碼器執行即時串流](media-services-live-streaming-with-onprem-encoders.md)，以了解具有內部部署編碼器和傳遞通道之即時串流的相關概念和考量。</span><span class="sxs-lookup"><span data-stu-id="13970-140">Please review [Live streaming with on-premises encoders that create multi-bitrate streams](media-services-live-streaming-with-onprem-encoders.md) to learn about concepts and considerations related to live streaming with on-premises encoders and pass-through channels.</span></span>
> 
> 

## <a name="to-view-notifications-and-errors"></a><span data-ttu-id="13970-141">檢視通知和錯誤</span><span class="sxs-lookup"><span data-stu-id="13970-141">To view notifications and errors</span></span>
<span data-ttu-id="13970-142">如果您要檢視 Azure 入口網站所產生的通知和錯誤，請按一下 [通知] 圖示。</span><span class="sxs-lookup"><span data-stu-id="13970-142">If you want to view notifications and errors produced by the Azure portal, click on the Notification icon.</span></span>

![通知](./media/media-services-portal-passthrough-get-started/media-services-notifications.png)

## <a name="create-and-start-pass-through-channels-and-events"></a><span data-ttu-id="13970-144">建立並啟動即時通行通道和事件</span><span class="sxs-lookup"><span data-stu-id="13970-144">Create and start pass-through channels and events</span></span>
<span data-ttu-id="13970-145">通道是與事件/程式相關聯，而程式可讓您控制即時串流中區段的發佈和儲存。</span><span class="sxs-lookup"><span data-stu-id="13970-145">A channel is associated with events/programs that enable you to control the publishing and storage of segments in a live stream.</span></span> <span data-ttu-id="13970-146">通道會管理事件。</span><span class="sxs-lookup"><span data-stu-id="13970-146">Channels manage events.</span></span> 

<span data-ttu-id="13970-147">設定 **封存時間範圍** 長度，即可指定您想要保留程式之錄製內容的時數。</span><span class="sxs-lookup"><span data-stu-id="13970-147">You can specify the number of hours you want to retain the recorded content for the program by setting the **Archive Window** length.</span></span> <span data-ttu-id="13970-148">此值可以設為最少 5 分鐘到最多 25 個小時。</span><span class="sxs-lookup"><span data-stu-id="13970-148">This value can be set from a minimum of 5 minutes to a maximum of 25 hours.</span></span> <span data-ttu-id="13970-149">封存時間範圍長度也會指出用戶端可以從目前即時位置及時往回搜尋的最大時間量。</span><span class="sxs-lookup"><span data-stu-id="13970-149">Archive window length also dictates the maximum amount of time clients can seek back in time from the current live position.</span></span> <span data-ttu-id="13970-150">事件在超過指定的時間量後還是可以執行，但是會持續捨棄落後時間範圍長度的內容。</span><span class="sxs-lookup"><span data-stu-id="13970-150">Events can run over the specified amount of time, but content that falls behind the window length is continuously discarded.</span></span> <span data-ttu-id="13970-151">此屬性的這個值也會決定用戶端資訊清單可以成長多長的時間。</span><span class="sxs-lookup"><span data-stu-id="13970-151">This value of this property also determines how long the client manifests can grow.</span></span>

<span data-ttu-id="13970-152">每個事件都是與資產相關聯。</span><span class="sxs-lookup"><span data-stu-id="13970-152">Each event is associated with an asset.</span></span> <span data-ttu-id="13970-153">若要發佈事件，您必須建立相關聯資產的 OnDemand 定位器。</span><span class="sxs-lookup"><span data-stu-id="13970-153">To publish the event, you must create an OnDemand locator for the associated asset.</span></span> <span data-ttu-id="13970-154">擁有此定位器，可讓您建置可提供給用戶端的串流 URL。</span><span class="sxs-lookup"><span data-stu-id="13970-154">Having this locator enables you to build a streaming URL that you can provide to your clients.</span></span>

<span data-ttu-id="13970-155">通道支援最多三個同時執行的事件，因此您可以建立相同內送串流的多個封存。</span><span class="sxs-lookup"><span data-stu-id="13970-155">A channel supports up to three concurrently running events so you can create multiple archives of the same incoming stream.</span></span> <span data-ttu-id="13970-156">這可讓您視需要發行和封存事件的不同部分。</span><span class="sxs-lookup"><span data-stu-id="13970-156">This allows you to publish and archive different parts of an event as needed.</span></span> <span data-ttu-id="13970-157">例如，您的商務需求是封存 6 小時的程式，但只廣播最後 10 分鐘。</span><span class="sxs-lookup"><span data-stu-id="13970-157">For example, your business requirement is to archive 6 hours of a program, but to broadcast only last 10 minutes.</span></span> <span data-ttu-id="13970-158">為了達成此目的，您必須建立兩個同時執行的程式。</span><span class="sxs-lookup"><span data-stu-id="13970-158">To accomplish this, you need to create two concurrently running programs.</span></span> <span data-ttu-id="13970-159">其中一個程式設定為封存 6 小時的事件，但是未發行該程式。</span><span class="sxs-lookup"><span data-stu-id="13970-159">One program is set to archive 6 hours of the event but the program is not published.</span></span> <span data-ttu-id="13970-160">另一個程式則設定為封存 10 分鐘，並發行程式。</span><span class="sxs-lookup"><span data-stu-id="13970-160">The other program is set to archive for 10 minutes and this program is published.</span></span>

<span data-ttu-id="13970-161">您不應該重複使用現有的即時事件。</span><span class="sxs-lookup"><span data-stu-id="13970-161">You should not reuse existing live events.</span></span> <span data-ttu-id="13970-162">而是針對每個事件建立並啟動新事件。</span><span class="sxs-lookup"><span data-stu-id="13970-162">Instead, create and start a new event for each event.</span></span>

<span data-ttu-id="13970-163">當您準備好開始串流和封存時，請啟動事件。</span><span class="sxs-lookup"><span data-stu-id="13970-163">Start the event when you are ready to start streaming and archiving.</span></span> <span data-ttu-id="13970-164">每當您想要停止串流處理和封存事件時，請停止程式。</span><span class="sxs-lookup"><span data-stu-id="13970-164">Stop the program whenever you want to stop streaming and archiving the event.</span></span> 

<span data-ttu-id="13970-165">若要刪除封存的內容，請停止並刪除事件，然後刪除相關聯的資產。</span><span class="sxs-lookup"><span data-stu-id="13970-165">To delete archived content, stop and delete the event and then delete the associated asset.</span></span> <span data-ttu-id="13970-166">如果事件使用資產，則無法刪除資產；必須先刪除事件。</span><span class="sxs-lookup"><span data-stu-id="13970-166">An asset cannot be deleted if it is used by an event; the event must be deleted first.</span></span> 

<span data-ttu-id="13970-167">只要您未刪除資產，即使在停止並刪除事件之後，使用者還是可以視需求將封存的內容串流為視訊。</span><span class="sxs-lookup"><span data-stu-id="13970-167">Even after you stop and delete the event, the users would be able to stream your archived content as a video on demand, for as long as you do not delete the asset.</span></span>

<span data-ttu-id="13970-168">如果想要保留封存的內容，但不要讓它可進行串流，請刪除串流定位器。</span><span class="sxs-lookup"><span data-stu-id="13970-168">If you do want to retain the archived content, but not have it available for streaming, delete the streaming locator.</span></span>

### <a name="to-use-the-portal-to-create-a-channel"></a><span data-ttu-id="13970-169">使用 Azure 入口網站來建立通道</span><span class="sxs-lookup"><span data-stu-id="13970-169">To use the portal to create a channel</span></span>
<span data-ttu-id="13970-170">本節示範如何使用 [快速建立]  選項來建立即時通行通道。</span><span class="sxs-lookup"><span data-stu-id="13970-170">This section shows how to use the **Quick Create** option to create a pass-through channel.</span></span>

<span data-ttu-id="13970-171">如需傳遞通道的詳細資訊，請參閱[使用會從建立多位元速率串流的內部部署編碼器執行即時串流](media-services-live-streaming-with-onprem-encoders.md)。</span><span class="sxs-lookup"><span data-stu-id="13970-171">For more details about pass-through channels, see [Live streaming with on-premises encoders that create multi-bitrate streams](media-services-live-streaming-with-onprem-encoders.md).</span></span>

1. <span data-ttu-id="13970-172">在 [Azure 入口網站](https://portal.azure.com/)中，選取您的 Azure 媒體服務帳戶。</span><span class="sxs-lookup"><span data-stu-id="13970-172">In the [Azure portal](https://portal.azure.com/), select your Azure Media Services account.</span></span>
2. <span data-ttu-id="13970-173">在 [設定] 視窗中，按一下 [即時視訊串流]。</span><span class="sxs-lookup"><span data-stu-id="13970-173">In the **Settings** window, click **Live streaming**.</span></span> 
   
    ![開始使用](./media/media-services-portal-passthrough-get-started/media-services-getting-started.png)
   
    <span data-ttu-id="13970-175">[即時視訊串流]  視窗隨即出現。</span><span class="sxs-lookup"><span data-stu-id="13970-175">The **Live streaming** window appears.</span></span>
3. <span data-ttu-id="13970-176">按一下 [快速建立]  ，使用 RTMP 內嵌通訊協定建立即時通行通道。</span><span class="sxs-lookup"><span data-stu-id="13970-176">Click **Quick Create** to create a pass-through channel with the RTMP ingest protocol.</span></span>
   
    <span data-ttu-id="13970-177">[建立新的通道]  視窗隨即出現。</span><span class="sxs-lookup"><span data-stu-id="13970-177">The **CREATE A NEW CHANNEL** window appears.</span></span>
4. <span data-ttu-id="13970-178">提供新通道的名稱，然後按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="13970-178">Give the new channel a name and click **Create**.</span></span> 
   
    <span data-ttu-id="13970-179">這會使用 RTMP 內嵌通訊協定建立即時通行通道。</span><span class="sxs-lookup"><span data-stu-id="13970-179">This creates a pass-through channel with the RTMP ingest protocol.</span></span>

## <a name="create-events"></a><span data-ttu-id="13970-180">建立事件</span><span class="sxs-lookup"><span data-stu-id="13970-180">Create events</span></span>
1. <span data-ttu-id="13970-181">選取您要新增事件的通道。</span><span class="sxs-lookup"><span data-stu-id="13970-181">Select a channel to which you want to add an event.</span></span>
2. <span data-ttu-id="13970-182">按下 [即時事件]  按鈕。</span><span class="sxs-lookup"><span data-stu-id="13970-182">Press **Live Event** button.</span></span>

![Event](./media/media-services-portal-passthrough-get-started/media-services-create-events.png)

## <a name="get-ingest-urls"></a><span data-ttu-id="13970-184">取得內嵌 URL</span><span class="sxs-lookup"><span data-stu-id="13970-184">Get ingest URLs</span></span>
<span data-ttu-id="13970-185">建立通道之後，即可取得您提供給即時編碼器的內嵌 URL。</span><span class="sxs-lookup"><span data-stu-id="13970-185">Once the channel is created, you can get ingest URLs that you will provide to the live encoder.</span></span> <span data-ttu-id="13970-186">編碼器會使用這些 URL 來輸入即時串流。</span><span class="sxs-lookup"><span data-stu-id="13970-186">The encoder uses these URLs to input a live stream.</span></span>

![建立時間](./media/media-services-portal-passthrough-get-started/media-services-channel-created.png)

## <a name="watch-the-event"></a><span data-ttu-id="13970-188">監看事件</span><span class="sxs-lookup"><span data-stu-id="13970-188">Watch the event</span></span>
<span data-ttu-id="13970-189">若要監看事件，請按一下 Azure 入口網站中的 [監看]  ，或複製串流 URL 並使用您選擇的播放程式。</span><span class="sxs-lookup"><span data-stu-id="13970-189">To watch the event, click **Watch** in the Azure portal or copy the streaming URL and use a player of your choice.</span></span> 

![建立時間](./media/media-services-portal-passthrough-get-started/media-services-default-event.png)

<span data-ttu-id="13970-191">即時事件會在停止時自動轉換為點播內容。</span><span class="sxs-lookup"><span data-stu-id="13970-191">Live event automatically get converted to on-demand content when stopped.</span></span>

## <a name="clean-up"></a><span data-ttu-id="13970-192">清除</span><span class="sxs-lookup"><span data-stu-id="13970-192">Clean up</span></span>
<span data-ttu-id="13970-193">如需傳遞通道的詳細資訊，請參閱[使用會從建立多位元速率串流的內部部署編碼器執行即時串流](media-services-live-streaming-with-onprem-encoders.md)。</span><span class="sxs-lookup"><span data-stu-id="13970-193">For more details about pass-through channels, see [Live streaming with on-premises encoders that create multi-bitrate streams](media-services-live-streaming-with-onprem-encoders.md).</span></span>

* <span data-ttu-id="13970-194">只有當通道上的所有事件/程式都已停止時，才能停止通道。</span><span class="sxs-lookup"><span data-stu-id="13970-194">A channel can be stopped only when all events/programs on the channel have been stopped.</span></span>  <span data-ttu-id="13970-195">停止通道之後，就不會產生任何費用。</span><span class="sxs-lookup"><span data-stu-id="13970-195">Once the Channel is stopped, it does not incur any charges.</span></span> <span data-ttu-id="13970-196">當您需要重新啟動它時，它會具有相同的內嵌 URL，因此您不需要重新設定編碼器。</span><span class="sxs-lookup"><span data-stu-id="13970-196">When you need to start it again, it will have the same ingest URL so you won't need to reconfigure your encoder.</span></span>
* <span data-ttu-id="13970-197">只有當通道上的所有事件都已刪除時，才能刪除通道。</span><span class="sxs-lookup"><span data-stu-id="13970-197">A channel can be deleted only when all live events on the channel have been deleted.</span></span>

## <a name="view-archived-content"></a><span data-ttu-id="13970-198">檢視封存的內容</span><span class="sxs-lookup"><span data-stu-id="13970-198">View archived content</span></span>
<span data-ttu-id="13970-199">只要您未刪除資產，即使在停止並刪除事件之後，使用者還是可以視需求將封存的內容串流為視訊。</span><span class="sxs-lookup"><span data-stu-id="13970-199">Even after you stop and delete the event, the users would be able to stream your archived content as a video on demand, for as long as you do not delete the asset.</span></span> <span data-ttu-id="13970-200">如果事件使用資產，則無法刪除資產；必須先刪除事件。</span><span class="sxs-lookup"><span data-stu-id="13970-200">An asset cannot be deleted if it is used by an event; the event must be deleted first.</span></span> 

<span data-ttu-id="13970-201">若要管理您的資產，請選取 [設定]，然後按一下 [資產]。</span><span class="sxs-lookup"><span data-stu-id="13970-201">To manage your assets, select **Setting** and click **Assets**.</span></span>

![資產](./media/media-services-portal-passthrough-get-started/media-services-assets.png)

## <a name="next-step"></a><span data-ttu-id="13970-203">後續步驟</span><span class="sxs-lookup"><span data-stu-id="13970-203">Next step</span></span>
<span data-ttu-id="13970-204">檢閱媒體服務學習路徑。</span><span class="sxs-lookup"><span data-stu-id="13970-204">Review Media Services learning paths.</span></span>

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="13970-205">提供意見反應</span><span class="sxs-lookup"><span data-stu-id="13970-205">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

