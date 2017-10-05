---
title: "設定 Elemental Live 編碼器來傳送單一位元速率的即時串流 | Microsoft Docs"
description: "本主題會示範如何設定 Elemental Live 編碼器，藉此將單一位元速率的即時串流傳送到 AMS 通道，其已針對即時編碼而啟用。"
services: media-services
documentationcenter: 
author: cenkdin
manager: cfowler
editor: 
ms.assetid: 9c6bf6a9-6273-4fdd-9477-f0e565280b5b
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: ne
ms.topic: article
ms.date: 01/05/2017
ms.author: cenkd;anilmur;juliako
ms.openlocfilehash: 668a3ab46a70c0ee25fa87031d27c0f4333ec89c
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="use-the-elemental-live-encoder-to-send-a-single-bitrate-live-stream"></a><span data-ttu-id="43e72-103">使用 Elemental Live 編碼器來傳送單一位元速率的即時串流</span><span class="sxs-lookup"><span data-stu-id="43e72-103">Use the Elemental Live encoder to send a single bitrate live stream</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="43e72-104">Elemental Live</span><span class="sxs-lookup"><span data-stu-id="43e72-104">Elemental Live</span></span>](media-services-configure-elemental-live-encoder.md)
> * [<span data-ttu-id="43e72-105">Tricaster</span><span class="sxs-lookup"><span data-stu-id="43e72-105">Tricaster</span></span>](media-services-configure-tricaster-live-encoder.md)
> * [<span data-ttu-id="43e72-106">Wirecast</span><span class="sxs-lookup"><span data-stu-id="43e72-106">Wirecast</span></span>](media-services-configure-wirecast-live-encoder.md)
> * [<span data-ttu-id="43e72-107">FMLE</span><span class="sxs-lookup"><span data-stu-id="43e72-107">FMLE</span></span>](media-services-configure-fmle-live-encoder.md)
>
>

<span data-ttu-id="43e72-108">本主題會示範如何設定 [Elemental Live](http://www.elementaltechnologies.com/products/elemental-live) 編碼器，藉此將單一位元速率的即時串流傳送到 AMS 通道，其已針對即時編碼而啟用。</span><span class="sxs-lookup"><span data-stu-id="43e72-108">This topic shows how to configure the [Elemental Live](http://www.elementaltechnologies.com/products/elemental-live) encoder to send a single bitrate stream to AMS channels that are enabled for live encoding.</span></span>  <span data-ttu-id="43e72-109">如需詳細資訊，請參閱 [使用啟用的通道來以 Azure 媒體服務執行即時編碼](media-services-manage-live-encoder-enabled-channels.md)。</span><span class="sxs-lookup"><span data-stu-id="43e72-109">For more information, see [Working with Channels that are Enabled to Perform Live Encoding with Azure Media Services](media-services-manage-live-encoder-enabled-channels.md).</span></span>

<span data-ttu-id="43e72-110">本教學課程示範如何使用 Azure 媒體服務總管 (AMSE) 工具管理 Azure 媒體服務 (AMS)。</span><span class="sxs-lookup"><span data-stu-id="43e72-110">This tutorial shows how to manage Azure Media Services (AMS) with Azure Media Services Explorer (AMSE) tool.</span></span> <span data-ttu-id="43e72-111">此工具只會在 Windows 電腦上執行。</span><span class="sxs-lookup"><span data-stu-id="43e72-111">This tool only runs on Windows PC.</span></span> <span data-ttu-id="43e72-112">如果您是用 Mac 或 Linux，請使用 Azure 入口網站建立[通道](media-services-portal-creating-live-encoder-enabled-channel.md#create-a-channel)和[程式](media-services-portal-creating-live-encoder-enabled-channel.md)。</span><span class="sxs-lookup"><span data-stu-id="43e72-112">If you are on Mac or Linux, use the Azure portal to create [channels](media-services-portal-creating-live-encoder-enabled-channel.md#create-a-channel) and [programs](media-services-portal-creating-live-encoder-enabled-channel.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="43e72-113">必要條件</span><span class="sxs-lookup"><span data-stu-id="43e72-113">Prerequisites</span></span>
* <span data-ttu-id="43e72-114">必須具備使用 Elemental Live Web 介面來建立即時事件的工作知識。</span><span class="sxs-lookup"><span data-stu-id="43e72-114">Must have a working knowledge of using Elemental Live web interface to create live events.</span></span>
* [<span data-ttu-id="43e72-115">建立 Azure 媒體服務帳戶</span><span class="sxs-lookup"><span data-stu-id="43e72-115">Create an Azure Media Services account</span></span>](media-services-portal-create-account.md)
* <span data-ttu-id="43e72-116">確定有執行中的「串流端點」。</span><span class="sxs-lookup"><span data-stu-id="43e72-116">Ensure there is a Streaming Endpoint running.</span></span> <span data-ttu-id="43e72-117">如需詳細資訊，請參閱 [在媒體服務帳戶中管理串流端點](media-services-portal-manage-streaming-endpoints.md)。</span><span class="sxs-lookup"><span data-stu-id="43e72-117">For more information, see [Manage Streaming Endpoints in a Media Services Account](media-services-portal-manage-streaming-endpoints.md).</span></span>
* <span data-ttu-id="43e72-118">安裝最新版的 [AMSE](https://github.com/Azure/Azure-Media-Services-Explorer) 工具。</span><span class="sxs-lookup"><span data-stu-id="43e72-118">Install the latest version of the [AMSE](https://github.com/Azure/Azure-Media-Services-Explorer) tool.</span></span>
* <span data-ttu-id="43e72-119">啟動工具並連接到您的 AMS 帳戶。</span><span class="sxs-lookup"><span data-stu-id="43e72-119">Launch the tool and connect to your AMS account.</span></span>

## <a name="tips"></a><span data-ttu-id="43e72-120">秘訣</span><span class="sxs-lookup"><span data-stu-id="43e72-120">Tips</span></span>
* <span data-ttu-id="43e72-121">請盡可能使用實體的有線網際網路連線。</span><span class="sxs-lookup"><span data-stu-id="43e72-121">Whenever possible, use a hardwired internet connection.</span></span>
* <span data-ttu-id="43e72-122">判斷頻寬需求的一項法則是將串流位元速率加倍。</span><span class="sxs-lookup"><span data-stu-id="43e72-122">A good rule of thumb when determining bandwidth requirements is to double the streaming bitrates.</span></span> <span data-ttu-id="43e72-123">雖然這不是強制性需求，卻有助於減輕網路阻塞的影響。</span><span class="sxs-lookup"><span data-stu-id="43e72-123">While this is not a mandatory requirement, it will help mitigate the impact of network congestion.</span></span>
* <span data-ttu-id="43e72-124">使用軟體式編碼器時，請關閉任何不必要的程式。</span><span class="sxs-lookup"><span data-stu-id="43e72-124">When using software based encoders, close out any unnecessary programs.</span></span>

## <a name="elemental-live-with-rtp-ingest"></a><span data-ttu-id="43e72-125">Elemental Live 與 RTP 嵌入</span><span class="sxs-lookup"><span data-stu-id="43e72-125">Elemental Live with RTP ingest</span></span>
<span data-ttu-id="43e72-126">本節說明如何設定可透過 RTP 傳送單一位元速率的即時串流 Elemental Live 編碼器。</span><span class="sxs-lookup"><span data-stu-id="43e72-126">This section shows how to configure the Elemental Live encoder that sends a single bitrate live stream over RTP.</span></span>  <span data-ttu-id="43e72-127">如需詳細資訊，請參閱 [透過 RTP 的 MPEG-TS 串流](media-services-manage-live-encoder-enabled-channels.md#channel)。</span><span class="sxs-lookup"><span data-stu-id="43e72-127">For more information, see [MPEG-TS stream over RTP](media-services-manage-live-encoder-enabled-channels.md#channel).</span></span>

### <a name="create-a-channel"></a><span data-ttu-id="43e72-128">建立通道</span><span class="sxs-lookup"><span data-stu-id="43e72-128">Create a channel</span></span>

1. <span data-ttu-id="43e72-129">在 AMSE 工具中，瀏覽至 [Live]  索引標籤，然後在通道區域內按一下滑鼠右鍵。</span><span class="sxs-lookup"><span data-stu-id="43e72-129">In the AMSE tool, navigate to the **Live** tab, and right click within the channel area.</span></span> <span data-ttu-id="43e72-130">從功能表選取 [建立通道...] </span><span class="sxs-lookup"><span data-stu-id="43e72-130">Select **Create channel…**</span></span> <span data-ttu-id="43e72-131">。</span><span class="sxs-lookup"><span data-stu-id="43e72-131">from the menu.</span></span>

    ![Elemental](./media/media-services-elemental-live-encoder/media-services-elemental1.png)

2. <span data-ttu-id="43e72-133">指定通道名稱，描述欄位為選填。</span><span class="sxs-lookup"><span data-stu-id="43e72-133">Specify a channel name, the description field is optional.</span></span> <span data-ttu-id="43e72-134">在 [頻道設定] 下方，針對 [即時編碼] 選項選取 [標準]，並將 [輸入通訊協定] 設為 [RTP (MPEG-TS)]。</span><span class="sxs-lookup"><span data-stu-id="43e72-134">Under Channel Settings, select **Standard** for the Live Encoding option, with the Input Protocol set to **RTP (MPEG-TS)**.</span></span> <span data-ttu-id="43e72-135">您可以將所有其他設定保留現狀。</span><span class="sxs-lookup"><span data-stu-id="43e72-135">You can leave all other settings as is.</span></span>

    <span data-ttu-id="43e72-136">請確認已選取 [ **立即啟動新頻道** ]。</span><span class="sxs-lookup"><span data-stu-id="43e72-136">Make sure the **Start the new channel now** is selected.</span></span>

3. <span data-ttu-id="43e72-137">按一下 [ **建立頻道**]。</span><span class="sxs-lookup"><span data-stu-id="43e72-137">Click **Create Channel**.</span></span>

   ![Elemental](./media/media-services-elemental-live-encoder/media-services-elemental12.png)

> [!NOTE]
> <span data-ttu-id="43e72-139">通道約需 20 分鐘的時間即可啟動。</span><span class="sxs-lookup"><span data-stu-id="43e72-139">The channel can take as long as 20 minutes to start.</span></span>
>
>

<span data-ttu-id="43e72-140">當頻道啟動時，您可以 [設定編碼器](media-services-configure-elemental-live-encoder.md#configure_elemental_rtp)。</span><span class="sxs-lookup"><span data-stu-id="43e72-140">While the channel is starting you can [configure the encoder](media-services-configure-elemental-live-encoder.md#configure_elemental_rtp).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="43e72-141">請注意，只要通道進入就緒狀態，就會開始計費。</span><span class="sxs-lookup"><span data-stu-id="43e72-141">Note that billing starts as soon as Channel goes into a ready state.</span></span> <span data-ttu-id="43e72-142">如需詳細資訊，請參閱 [頻道的狀態](media-services-manage-live-encoder-enabled-channels.md#states)。</span><span class="sxs-lookup"><span data-stu-id="43e72-142">For more information, see [Channel's states](media-services-manage-live-encoder-enabled-channels.md#states).</span></span>
>
>

### <span data-ttu-id="43e72-143"><a id=configure_elemental_rtp></a>設定 Elemental Live 編碼器</span><span class="sxs-lookup"><span data-stu-id="43e72-143"><a id=configure_elemental_rtp></a>Configure the Elemental Live encoder</span></span>
<span data-ttu-id="43e72-144">在本教學課程中會使用下列輸出設定。</span><span class="sxs-lookup"><span data-stu-id="43e72-144">In this tutorial the following output settings are used.</span></span> <span data-ttu-id="43e72-145">本章節的其餘部分將詳細說明組態步驟。</span><span class="sxs-lookup"><span data-stu-id="43e72-145">The rest of this section describes configuration steps in more detail.</span></span>

<span data-ttu-id="43e72-146">**視訊**：</span><span class="sxs-lookup"><span data-stu-id="43e72-146">**Video**:</span></span>

* <span data-ttu-id="43e72-147">轉碼器：H.264</span><span class="sxs-lookup"><span data-stu-id="43e72-147">Codec: H.264</span></span>
* <span data-ttu-id="43e72-148">設定檔：高 (層級 4.0)</span><span class="sxs-lookup"><span data-stu-id="43e72-148">Profile: High (Level 4.0)</span></span>
* <span data-ttu-id="43e72-149">位元速率：5000 kbps</span><span class="sxs-lookup"><span data-stu-id="43e72-149">Bitrate: 5000 kbps</span></span>
* <span data-ttu-id="43e72-150">主要畫面格：2 秒 (60 秒)</span><span class="sxs-lookup"><span data-stu-id="43e72-150">Keyframe: 2 seconds (60 seconds)</span></span>
* <span data-ttu-id="43e72-151">畫面播放速率：30</span><span class="sxs-lookup"><span data-stu-id="43e72-151">Frame Rate: 30</span></span>

<span data-ttu-id="43e72-152">**音訊**：</span><span class="sxs-lookup"><span data-stu-id="43e72-152">**Audio**:</span></span>

* <span data-ttu-id="43e72-153">轉碼器：AAC (LC)</span><span class="sxs-lookup"><span data-stu-id="43e72-153">Codec: AAC (LC)</span></span>
* <span data-ttu-id="43e72-154">位元速率：192 kbps</span><span class="sxs-lookup"><span data-stu-id="43e72-154">Bitrate: 192 kbps</span></span>
* <span data-ttu-id="43e72-155">取樣速率：44.1 kHz</span><span class="sxs-lookup"><span data-stu-id="43e72-155">Sample Rate: 44.1 kHz</span></span>

#### <a name="configuration-steps"></a><span data-ttu-id="43e72-156">組態步驟</span><span class="sxs-lookup"><span data-stu-id="43e72-156">Configuration steps</span></span>
1. <span data-ttu-id="43e72-157">瀏覽至 **Elemental Live** Web 介面，並設定用於 **UDP/TS** 串流的編碼器。</span><span class="sxs-lookup"><span data-stu-id="43e72-157">Navigate to the **Elemental Live** web interface, and set up the encoder for **UDP/TS** streaming.</span></span>
2. <span data-ttu-id="43e72-158">建立新事件後，請向下捲動至輸出群組並新增 **UDP/TS** 輸出群組。</span><span class="sxs-lookup"><span data-stu-id="43e72-158">Once a new event is created, scroll down to the output groups and add the **UDP/TS** output group.</span></span>
3. <span data-ttu-id="43e72-159">選取 [新增串流] 然後按一下 [加入輸出] 建立新的輸出。</span><span class="sxs-lookup"><span data-stu-id="43e72-159">Create a new output by selecting **New Stream** and then clicking **Add Output**.</span></span>  

    ![Elemental](./media/media-services-elemental-live-encoder/media-services-elemental13.png)

   > [!NOTE]
   > <span data-ttu-id="43e72-161">建議將 Elemental 事件的時間代碼設定為「系統時鐘」，以協助編碼器在串流失敗時重新連接。</span><span class="sxs-lookup"><span data-stu-id="43e72-161">It is recommended that the Elemental event has the timecode set to "System Clock" to help the encoder reconnect in the case of a stream failure.</span></span>
   >
   >
4. <span data-ttu-id="43e72-162">現在已建立好輸出，請按一下 [ **新增串流**]。</span><span class="sxs-lookup"><span data-stu-id="43e72-162">Now that the Output has been created, click **Add Stream**.</span></span> <span data-ttu-id="43e72-163">現在可以設定輸出設定。</span><span class="sxs-lookup"><span data-stu-id="43e72-163">The output settings can now be configured.</span></span>
5. <span data-ttu-id="43e72-164">向下捲動到剛剛建立的「串流 1」，按一下左側的 [視訊] 索引標籤並展開 [進階] 設定區段。</span><span class="sxs-lookup"><span data-stu-id="43e72-164">Scroll down to the "Stream 1" that was just created, click the **Video** tab on the left and expand the **Advanced** settings section.</span></span>

    ![Elemental](./media/media-services-elemental-live-encoder/media-services-elemental4.png)

    <span data-ttu-id="43e72-166">雖然 Elemental Live 有各種不同的可用自訂，建議對串流至 AMS 入門使用下列設定。</span><span class="sxs-lookup"><span data-stu-id="43e72-166">While Elemental Live has a wide range of available customizing, the following settings are recommended for getting started with streaming to AMS.</span></span>

   * <span data-ttu-id="43e72-167">解析度：1280 x 720</span><span class="sxs-lookup"><span data-stu-id="43e72-167">Resolution: 1280 x 720</span></span>
   * <span data-ttu-id="43e72-168">畫面播放速率：30</span><span class="sxs-lookup"><span data-stu-id="43e72-168">Framerate: 30</span></span>
   * <span data-ttu-id="43e72-169">GOP 大小：60 個畫面格</span><span class="sxs-lookup"><span data-stu-id="43e72-169">GOP Size: 60 frames</span></span>
   * <span data-ttu-id="43e72-170">交錯式模式：漸進式</span><span class="sxs-lookup"><span data-stu-id="43e72-170">Interlace Mode: Progressive</span></span>
   * <span data-ttu-id="43e72-171">位元速率：5000000 位元/秒 (這可以根據網路限制調整)</span><span class="sxs-lookup"><span data-stu-id="43e72-171">Bitrate: 5000000 bit/s (This can be adjusted based on network limitations)</span></span>

    ![Elemental](./media/media-services-elemental-live-encoder/media-services-elemental5.png)

1. <span data-ttu-id="43e72-173">取得通道的輸入 URL。</span><span class="sxs-lookup"><span data-stu-id="43e72-173">Get the channel's input URL.</span></span>

    <span data-ttu-id="43e72-174">瀏覽回到 AMSE 工具，並檢查通道的完成狀態。</span><span class="sxs-lookup"><span data-stu-id="43e72-174">Navigate back to the AMSE tool, and check on the channel completion status.</span></span> <span data-ttu-id="43e72-175">狀態從 [啟動中] 變更為 [執行中] 後，您便可取得輸入 URL。</span><span class="sxs-lookup"><span data-stu-id="43e72-175">Once the State has changed from **Starting** to **Running**, you can get the input URL.</span></span>

    <span data-ttu-id="43e72-176">頻道執行時，以滑鼠右鍵按一下頻道名稱，向下瀏覽讓滑鼠游標停留在 [複製輸入 URL 到剪貼簿]，然後選取 [主要輸入 URL]。</span><span class="sxs-lookup"><span data-stu-id="43e72-176">When the channel is running, right click the channel name, navigate down to hover over **Copy Input URL to clipboard** and then select **Primary Input  URL**.</span></span>  

    ![Elemental](./media/media-services-elemental-live-encoder/media-services-elemental6.png)
2. <span data-ttu-id="43e72-178">在 Elemental 的 [ **主要目的地** ] 欄位中貼上這項資訊。</span><span class="sxs-lookup"><span data-stu-id="43e72-178">Paste this information in the **Primary Destination** field of the Elemental.</span></span> <span data-ttu-id="43e72-179">所有其他設定可以保留預設值。</span><span class="sxs-lookup"><span data-stu-id="43e72-179">All other settings can remain the default.</span></span>

    ![Elemental](./media/media-services-elemental-live-encoder/media-services-elemental14.png)

    <span data-ttu-id="43e72-181">如需額外的備援，請對次要輸入 URL 重複這些步驟，方法是為 UDP/TS 串流建立個別的「輸出」索引標籤。</span><span class="sxs-lookup"><span data-stu-id="43e72-181">For extra redundancy, repeat these steps with the Secondary Input URL by creating a separate "Output" tab for UDP/TS Streaming.</span></span>
3. <span data-ttu-id="43e72-182">按一下 建立 \(如果已建立新事件) 或 更新 \(如果是編輯原有的事件)，然後繼續啟動編碼器。</span><span class="sxs-lookup"><span data-stu-id="43e72-182">Click **Create** (if a new event was created) or **Update** (if editing a pre-existing event) and then proceed to start the encoder.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="43e72-183">按一下 Elemental Live Web 介面上的 [開始] 之前，您**必須**確保頻道已就緒。</span><span class="sxs-lookup"><span data-stu-id="43e72-183">Before you click **Start** on the Elemental Live web interface, you **must** ensure that the Channel is ready.</span></span>
> <span data-ttu-id="43e72-184">此外，請確保不要讓通道處於就緒狀態而無任何事件超過 15 分鐘。</span><span class="sxs-lookup"><span data-stu-id="43e72-184">Also, make sure not to leave the Channel in a ready state without an event for longer than > 15 minutes.</span></span>
>
>

<span data-ttu-id="43e72-185">在串流已經執行了 30 秒後，導覽回 AMSE 工具和測試播放。</span><span class="sxs-lookup"><span data-stu-id="43e72-185">After the stream has been running for 30 seconds, navigate back to the AMSE tool and test playback.</span></span>  

### <a name="test-playback"></a><span data-ttu-id="43e72-186">測試播放</span><span class="sxs-lookup"><span data-stu-id="43e72-186">Test playback</span></span>

<span data-ttu-id="43e72-187">瀏覽至 AMSE 工具，然後以滑鼠右鍵按一下要測試的通道。</span><span class="sxs-lookup"><span data-stu-id="43e72-187">Navigate to the AMSE tool, and right click the channel to be tested.</span></span> <span data-ttu-id="43e72-188">在功能表中，將滑鼠游標停留在 [播放預覽]，並選取 [使用 Azure 媒體播放器]。</span><span class="sxs-lookup"><span data-stu-id="43e72-188">From the menu, hover over **Playback the Preview** and select **with Azure Media Player**.</span></span>  

    ![Elemental](./media/media-services-elemental-live-encoder/media-services-elemental8.png)

<span data-ttu-id="43e72-189">如果播放器中出現串流，則編碼器已妥善設定為連接到 AMS。</span><span class="sxs-lookup"><span data-stu-id="43e72-189">If the stream appears in the player, then the encoder has been properly configured to connect to AMS.</span></span>

<span data-ttu-id="43e72-190">如果收到錯誤，則必須重設通道，且編碼器設定需要調整。</span><span class="sxs-lookup"><span data-stu-id="43e72-190">If an error is received, the channel will need to be reset and encoder settings adjusted.</span></span> <span data-ttu-id="43e72-191">請參閱 [疑難排解](media-services-troubleshooting-live-streaming.md) 主題中的指引。</span><span class="sxs-lookup"><span data-stu-id="43e72-191">Please see the [troubleshooting](media-services-troubleshooting-live-streaming.md) topic for guidance.</span></span>   

### <a name="create-a-program"></a><span data-ttu-id="43e72-192">建立程式</span><span class="sxs-lookup"><span data-stu-id="43e72-192">Create a program</span></span>
1. <span data-ttu-id="43e72-193">一旦確認通道播放沒問題後，請建立程式。</span><span class="sxs-lookup"><span data-stu-id="43e72-193">Once channel playback is confirmed, create a program.</span></span> <span data-ttu-id="43e72-194">在 AMSE 工具的 [Live] 索引標籤下，於程式區域內按一下滑鼠右鍵，並選取 [建立新的程式]。</span><span class="sxs-lookup"><span data-stu-id="43e72-194">Under the **Live** tab in the AMSE tool, right click within the program area and select **Create New Program**.</span></span>  

    ![Elemental](./media/media-services-elemental-live-encoder/media-services-elemental9.png)
2. <span data-ttu-id="43e72-196">為程式命名，並視需要調整 **封存時間長度** (預設為 4 小時)。</span><span class="sxs-lookup"><span data-stu-id="43e72-196">Name the program and, if needed, adjust the **Archive Window Length** (which defaults to 4 hours).</span></span> <span data-ttu-id="43e72-197">您也可以指定儲存體位置，或保留為預設值。</span><span class="sxs-lookup"><span data-stu-id="43e72-197">You can also specify a storage location or leave as the default.</span></span>  
3. <span data-ttu-id="43e72-198">勾選 [現在啟動程式]  方塊。</span><span class="sxs-lookup"><span data-stu-id="43e72-198">Check the **Start the Program now** box.</span></span>
4. <span data-ttu-id="43e72-199">按一下 [建立程式] 。</span><span class="sxs-lookup"><span data-stu-id="43e72-199">Click **Create Program**.</span></span>  

    >[!NOTE]
    > <span data-ttu-id="43e72-200">建立程式時所使用的時間會比建立通道時少。</span><span class="sxs-lookup"><span data-stu-id="43e72-200">Program creation takes less time than channel creation.</span></span>   
      
5. <span data-ttu-id="43e72-201">一旦程式開始執行，請在程式上按一下滑鼠右鍵，並瀏覽至 [播放程式]，然後選取 [使用 Azure 媒體播放器] 確認播放。</span><span class="sxs-lookup"><span data-stu-id="43e72-201">Once the program is running, confirm playback by right clicking the program and navigating to **Playback the program(s)** and then selecting **with Azure Media Player**.</span></span>  
6. <span data-ttu-id="43e72-202">一經確認後，再次於該程式上按一下滑鼠右鍵，並選取 [複製輸出 URL 到剪貼簿] \(或從 [程式資訊和設定] 功能表選項擷取這項資訊)。</span><span class="sxs-lookup"><span data-stu-id="43e72-202">Once confirmed, right click the program again and select **Copy the Output URL to Clipboard** (or retrieve this information from the **Program information and settings** option from the menu).</span></span>

<span data-ttu-id="43e72-203">串流現在已經可以內嵌於播放程式中，或散發給某個對象，以供即時檢視。</span><span class="sxs-lookup"><span data-stu-id="43e72-203">The stream is now ready to be embedded in a player, or distributed to an audience for live viewing.</span></span>  

## <a name="troubleshooting"></a><span data-ttu-id="43e72-204">疑難排解</span><span class="sxs-lookup"><span data-stu-id="43e72-204">Troubleshooting</span></span>
<span data-ttu-id="43e72-205">請參閱 [疑難排解](media-services-troubleshooting-live-streaming.md) 主題中的指引。</span><span class="sxs-lookup"><span data-stu-id="43e72-205">Please see the [troubleshooting](media-services-troubleshooting-live-streaming.md) topic for guidance.</span></span>

## <a name="media-services-learning-paths"></a><span data-ttu-id="43e72-206">媒體服務學習路徑</span><span class="sxs-lookup"><span data-stu-id="43e72-206">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="43e72-207">提供意見反應</span><span class="sxs-lookup"><span data-stu-id="43e72-207">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]
