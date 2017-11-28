---
title: "aaaConfigure hello 元素即時編碼器 toosend 單一位元速率即時資料流 |Microsoft 文件"
description: "本主題說明如何 tooconfigure 會 hello 元素即時編碼器 toosend 即時編碼啟用單一位元速率串流 tooAMS 通道。"
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
ms.openlocfilehash: 9a5de6189bfb123768a9da038b8c8db69cf85e91
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-elemental-live-encoder-toosend-a-single-bitrate-live-stream"></a><span data-ttu-id="82a0d-103">使用單一位元速率即時資料流，hello 元素即時編碼器 toosend</span><span class="sxs-lookup"><span data-stu-id="82a0d-103">Use hello Elemental Live encoder toosend a single bitrate live stream</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="82a0d-104">Elemental Live</span><span class="sxs-lookup"><span data-stu-id="82a0d-104">Elemental Live</span></span>](media-services-configure-elemental-live-encoder.md)
> * [<span data-ttu-id="82a0d-105">Tricaster</span><span class="sxs-lookup"><span data-stu-id="82a0d-105">Tricaster</span></span>](media-services-configure-tricaster-live-encoder.md)
> * [<span data-ttu-id="82a0d-106">Wirecast</span><span class="sxs-lookup"><span data-stu-id="82a0d-106">Wirecast</span></span>](media-services-configure-wirecast-live-encoder.md)
> * [<span data-ttu-id="82a0d-107">FMLE</span><span class="sxs-lookup"><span data-stu-id="82a0d-107">FMLE</span></span>](media-services-configure-fmle-live-encoder.md)
>
>

<span data-ttu-id="82a0d-108">本主題說明如何 tooconfigure hello[元素 Live](http://www.elementaltechnologies.com/products/elemental-live)編碼器 toosend 單一位元速率串流的即時編碼啟用 tooAMS 通道。</span><span class="sxs-lookup"><span data-stu-id="82a0d-108">This topic shows how tooconfigure hello [Elemental Live](http://www.elementaltechnologies.com/products/elemental-live) encoder toosend a single bitrate stream tooAMS channels that are enabled for live encoding.</span></span>  <span data-ttu-id="82a0d-109">如需詳細資訊，請參閱[使用通道，會啟用 tooPerform Live 使用 Azure 媒體服務編碼](media-services-manage-live-encoder-enabled-channels.md)。</span><span class="sxs-lookup"><span data-stu-id="82a0d-109">For more information, see [Working with Channels that are Enabled tooPerform Live Encoding with Azure Media Services](media-services-manage-live-encoder-enabled-channels.md).</span></span>

<span data-ttu-id="82a0d-110">本教學課程示範如何 toomanage Azure 媒體服務 (AMS) 中使用 Azure 媒體服務總管 (AMSE) 工具。</span><span class="sxs-lookup"><span data-stu-id="82a0d-110">This tutorial shows how toomanage Azure Media Services (AMS) with Azure Media Services Explorer (AMSE) tool.</span></span> <span data-ttu-id="82a0d-111">此工具只會在 Windows 電腦上執行。</span><span class="sxs-lookup"><span data-stu-id="82a0d-111">This tool only runs on Windows PC.</span></span> <span data-ttu-id="82a0d-112">如果您是在 Mac 或 Linux 上，使用 Azure 入口網站 toocreate hello[通道](media-services-portal-creating-live-encoder-enabled-channel.md#create-a-channel)和[程式](media-services-portal-creating-live-encoder-enabled-channel.md)。</span><span class="sxs-lookup"><span data-stu-id="82a0d-112">If you are on Mac or Linux, use hello Azure portal toocreate [channels](media-services-portal-creating-live-encoder-enabled-channel.md#create-a-channel) and [programs](media-services-portal-creating-live-encoder-enabled-channel.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="82a0d-113">必要條件</span><span class="sxs-lookup"><span data-stu-id="82a0d-113">Prerequisites</span></span>
* <span data-ttu-id="82a0d-114">必須使用元素即時 web 介面 toocreate 即時事件的實用知識。</span><span class="sxs-lookup"><span data-stu-id="82a0d-114">Must have a working knowledge of using Elemental Live web interface toocreate live events.</span></span>
* [<span data-ttu-id="82a0d-115">建立 Azure 媒體服務帳戶</span><span class="sxs-lookup"><span data-stu-id="82a0d-115">Create an Azure Media Services account</span></span>](media-services-portal-create-account.md)
* <span data-ttu-id="82a0d-116">確定有執行中的「串流端點」。</span><span class="sxs-lookup"><span data-stu-id="82a0d-116">Ensure there is a Streaming Endpoint running.</span></span> <span data-ttu-id="82a0d-117">如需詳細資訊，請參閱 [在媒體服務帳戶中管理串流端點](media-services-portal-manage-streaming-endpoints.md)。</span><span class="sxs-lookup"><span data-stu-id="82a0d-117">For more information, see [Manage Streaming Endpoints in a Media Services Account](media-services-portal-manage-streaming-endpoints.md).</span></span>
* <span data-ttu-id="82a0d-118">安裝 hello 最新版 hello [AMSE](https://github.com/Azure/Azure-Media-Services-Explorer)工具。</span><span class="sxs-lookup"><span data-stu-id="82a0d-118">Install hello latest version of hello [AMSE](https://github.com/Azure/Azure-Media-Services-Explorer) tool.</span></span>
* <span data-ttu-id="82a0d-119">啟動 hello 工具和 tooyour AMS 帳戶連接。</span><span class="sxs-lookup"><span data-stu-id="82a0d-119">Launch hello tool and connect tooyour AMS account.</span></span>

## <a name="tips"></a><span data-ttu-id="82a0d-120">祕訣</span><span class="sxs-lookup"><span data-stu-id="82a0d-120">Tips</span></span>
* <span data-ttu-id="82a0d-121">請盡可能使用實體的有線網際網路連線。</span><span class="sxs-lookup"><span data-stu-id="82a0d-121">Whenever possible, use a hardwired internet connection.</span></span>
* <span data-ttu-id="82a0d-122">最佳經驗法則時判斷頻寬需求為串流處理位元的 toodouble hello。</span><span class="sxs-lookup"><span data-stu-id="82a0d-122">A good rule of thumb when determining bandwidth requirements is toodouble hello streaming bitrates.</span></span> <span data-ttu-id="82a0d-123">雖然這不是強制性需求，有助於減少 hello 發生網路壅塞的影響。</span><span class="sxs-lookup"><span data-stu-id="82a0d-123">While this is not a mandatory requirement, it will help mitigate hello impact of network congestion.</span></span>
* <span data-ttu-id="82a0d-124">使用軟體型編碼器時，請關閉任何不必要的程式。</span><span class="sxs-lookup"><span data-stu-id="82a0d-124">When using software based encoders, close out any unnecessary programs.</span></span>

## <a name="elemental-live-with-rtp-ingest"></a><span data-ttu-id="82a0d-125">Elemental Live 與 RTP 嵌入</span><span class="sxs-lookup"><span data-stu-id="82a0d-125">Elemental Live with RTP ingest</span></span>
<span data-ttu-id="82a0d-126">本節說明如何 tooconfigure hello 元素即時編碼器會傳送單一位元速率透過 RTP 的即時資料流。</span><span class="sxs-lookup"><span data-stu-id="82a0d-126">This section shows how tooconfigure hello Elemental Live encoder that sends a single bitrate live stream over RTP.</span></span>  <span data-ttu-id="82a0d-127">如需詳細資訊，請參閱 [透過 RTP 的 MPEG-TS 串流](media-services-manage-live-encoder-enabled-channels.md#channel)。</span><span class="sxs-lookup"><span data-stu-id="82a0d-127">For more information, see [MPEG-TS stream over RTP](media-services-manage-live-encoder-enabled-channels.md#channel).</span></span>

### <a name="create-a-channel"></a><span data-ttu-id="82a0d-128">建立通道</span><span class="sxs-lookup"><span data-stu-id="82a0d-128">Create a channel</span></span>

1. <span data-ttu-id="82a0d-129">在 hello AMSE 工具中，瀏覽 toohello **Live**索引標籤，然後以滑鼠右鍵按一下 hello 通道區域內。</span><span class="sxs-lookup"><span data-stu-id="82a0d-129">In hello AMSE tool, navigate toohello **Live** tab, and right click within hello channel area.</span></span> <span data-ttu-id="82a0d-130">從功能表選取 [建立通道...] </span><span class="sxs-lookup"><span data-stu-id="82a0d-130">Select **Create channel…**</span></span> <span data-ttu-id="82a0d-131">從 [hello] 功能表中。</span><span class="sxs-lookup"><span data-stu-id="82a0d-131">from hello menu.</span></span>

    ![Elemental](./media/media-services-elemental-live-encoder/media-services-elemental1.png)

2. <span data-ttu-id="82a0d-133">指定通道名稱，hello 描述欄位是選擇性的。</span><span class="sxs-lookup"><span data-stu-id="82a0d-133">Specify a channel name, hello description field is optional.</span></span> <span data-ttu-id="82a0d-134">在 [通道設定] 下選取**標準**hello 即時編碼選項，以 hello 輸入通訊協定設定得**RTP (MPEG-TS)**。</span><span class="sxs-lookup"><span data-stu-id="82a0d-134">Under Channel Settings, select **Standard** for hello Live Encoding option, with hello Input Protocol set too**RTP (MPEG-TS)**.</span></span> <span data-ttu-id="82a0d-135">您可以將所有其他設定保留現狀。</span><span class="sxs-lookup"><span data-stu-id="82a0d-135">You can leave all other settings as is.</span></span>

    <span data-ttu-id="82a0d-136">請確定 hello**開始 hello 新通道現在**已選取。</span><span class="sxs-lookup"><span data-stu-id="82a0d-136">Make sure hello **Start hello new channel now** is selected.</span></span>

3. <span data-ttu-id="82a0d-137">按一下 [ **建立頻道**]。</span><span class="sxs-lookup"><span data-stu-id="82a0d-137">Click **Create Channel**.</span></span>

   ![Elemental](./media/media-services-elemental-live-encoder/media-services-elemental12.png)

> [!NOTE]
> <span data-ttu-id="82a0d-139">hello 通道花費 20 分鐘 toostart 一樣長。</span><span class="sxs-lookup"><span data-stu-id="82a0d-139">hello channel can take as long as 20 minutes toostart.</span></span>
>
>

<span data-ttu-id="82a0d-140">您可以啟動 hello 通道時[設定 hello 編碼器](media-services-configure-elemental-live-encoder.md#configure_elemental_rtp)。</span><span class="sxs-lookup"><span data-stu-id="82a0d-140">While hello channel is starting you can [configure hello encoder](media-services-configure-elemental-live-encoder.md#configure_elemental_rtp).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="82a0d-141">請注意，只要通道進入就緒狀態，就會開始計費。</span><span class="sxs-lookup"><span data-stu-id="82a0d-141">Note that billing starts as soon as Channel goes into a ready state.</span></span> <span data-ttu-id="82a0d-142">如需詳細資訊，請參閱 [通道的狀態](media-services-manage-live-encoder-enabled-channels.md#states)。</span><span class="sxs-lookup"><span data-stu-id="82a0d-142">For more information, see [Channel's states](media-services-manage-live-encoder-enabled-channels.md#states).</span></span>
>
>

### <span data-ttu-id="82a0d-143"><a id=configure_elemental_rtp></a>設定 hello 元素即時編碼器</span><span class="sxs-lookup"><span data-stu-id="82a0d-143"><a id=configure_elemental_rtp></a>Configure hello Elemental Live encoder</span></span>
<span data-ttu-id="82a0d-144">在此教學課程的 hello 會使用下列的輸出設定。</span><span class="sxs-lookup"><span data-stu-id="82a0d-144">In this tutorial hello following output settings are used.</span></span> <span data-ttu-id="82a0d-145">hello 本節其餘部分描述更詳細的組態步驟。</span><span class="sxs-lookup"><span data-stu-id="82a0d-145">hello rest of this section describes configuration steps in more detail.</span></span>

<span data-ttu-id="82a0d-146">**視訊**：</span><span class="sxs-lookup"><span data-stu-id="82a0d-146">**Video**:</span></span>

* <span data-ttu-id="82a0d-147">轉碼器：H.264</span><span class="sxs-lookup"><span data-stu-id="82a0d-147">Codec: H.264</span></span>
* <span data-ttu-id="82a0d-148">設定檔：高 (層級 4.0)</span><span class="sxs-lookup"><span data-stu-id="82a0d-148">Profile: High (Level 4.0)</span></span>
* <span data-ttu-id="82a0d-149">位元速率：5000 kbps</span><span class="sxs-lookup"><span data-stu-id="82a0d-149">Bitrate: 5000 kbps</span></span>
* <span data-ttu-id="82a0d-150">主要畫面格：2 秒 (60 秒)</span><span class="sxs-lookup"><span data-stu-id="82a0d-150">Keyframe: 2 seconds (60 seconds)</span></span>
* <span data-ttu-id="82a0d-151">畫面播放速率：30</span><span class="sxs-lookup"><span data-stu-id="82a0d-151">Frame Rate: 30</span></span>

<span data-ttu-id="82a0d-152">**音訊**：</span><span class="sxs-lookup"><span data-stu-id="82a0d-152">**Audio**:</span></span>

* <span data-ttu-id="82a0d-153">轉碼器：AAC (LC)</span><span class="sxs-lookup"><span data-stu-id="82a0d-153">Codec: AAC (LC)</span></span>
* <span data-ttu-id="82a0d-154">位元速率：192 kbps</span><span class="sxs-lookup"><span data-stu-id="82a0d-154">Bitrate: 192 kbps</span></span>
* <span data-ttu-id="82a0d-155">取樣速率：44.1 kHz</span><span class="sxs-lookup"><span data-stu-id="82a0d-155">Sample Rate: 44.1 kHz</span></span>

#### <a name="configuration-steps"></a><span data-ttu-id="82a0d-156">組態步驟</span><span class="sxs-lookup"><span data-stu-id="82a0d-156">Configuration steps</span></span>
1. <span data-ttu-id="82a0d-157">瀏覽 toohello**元素 Live** web 介面，並設定好的 hello 編碼器**UDP/TS**資料流。</span><span class="sxs-lookup"><span data-stu-id="82a0d-157">Navigate toohello **Elemental Live** web interface, and set up hello encoder for **UDP/TS** streaming.</span></span>
2. <span data-ttu-id="82a0d-158">一旦建立新的事件，向下 toohello 輸出群組捲動，並新增 hello **UDP/TS**輸出群組。</span><span class="sxs-lookup"><span data-stu-id="82a0d-158">Once a new event is created, scroll down toohello output groups and add hello **UDP/TS** output group.</span></span>
3. <span data-ttu-id="82a0d-159">選取 新增串流 然後按一下加入輸出 建立新的輸出。</span><span class="sxs-lookup"><span data-stu-id="82a0d-159">Create a new output by selecting **New Stream** and then clicking **Add Output**.</span></span>  

    ![Elemental](./media/media-services-elemental-live-encoder/media-services-elemental13.png)

   > [!NOTE]
   > <span data-ttu-id="82a0d-161">建議的 hello 元素事件有 hello 播放設定得 「 系統時鐘"toohelp hello 編碼器重新連線在 hello 案例中的資料流失敗。</span><span class="sxs-lookup"><span data-stu-id="82a0d-161">It is recommended that hello Elemental event has hello timecode set too"System Clock" toohelp hello encoder reconnect in hello case of a stream failure.</span></span>
   >
   >
4. <span data-ttu-id="82a0d-162">既然 hello 輸出建立之後，按一下**新增資料流**。</span><span class="sxs-lookup"><span data-stu-id="82a0d-162">Now that hello Output has been created, click **Add Stream**.</span></span> <span data-ttu-id="82a0d-163">現在可以設定 hello 輸出設定。</span><span class="sxs-lookup"><span data-stu-id="82a0d-163">hello output settings can now be configured.</span></span>
5. <span data-ttu-id="82a0d-164">捲動 toohello 」 資料流 1"已建立，請按一下 hello**視訊**hello 左側索引標籤，展開 hello**進階**設定 區段。</span><span class="sxs-lookup"><span data-stu-id="82a0d-164">Scroll down toohello "Stream 1" that was just created, click hello **Video** tab on hello left and expand hello **Advanced** settings section.</span></span>

    ![Elemental](./media/media-services-elemental-live-encoder/media-services-elemental4.png)

    <span data-ttu-id="82a0d-166">雖然元素 Live 有各種不同的可自訂，hello 下列設定建議的開始使用資料流 tooAMS。</span><span class="sxs-lookup"><span data-stu-id="82a0d-166">While Elemental Live has a wide range of available customizing, hello following settings are recommended for getting started with streaming tooAMS.</span></span>

   * <span data-ttu-id="82a0d-167">解析度：1280 x 720</span><span class="sxs-lookup"><span data-stu-id="82a0d-167">Resolution: 1280 x 720</span></span>
   * <span data-ttu-id="82a0d-168">畫面播放速率：30</span><span class="sxs-lookup"><span data-stu-id="82a0d-168">Framerate: 30</span></span>
   * <span data-ttu-id="82a0d-169">GOP 大小：60 個畫面格</span><span class="sxs-lookup"><span data-stu-id="82a0d-169">GOP Size: 60 frames</span></span>
   * <span data-ttu-id="82a0d-170">交錯式模式：漸進式</span><span class="sxs-lookup"><span data-stu-id="82a0d-170">Interlace Mode: Progressive</span></span>
   * <span data-ttu-id="82a0d-171">位元速率：5000000 位元/秒 (這可以根據網路限制調整)</span><span class="sxs-lookup"><span data-stu-id="82a0d-171">Bitrate: 5000000 bit/s (This can be adjusted based on network limitations)</span></span>

    ![Elemental](./media/media-services-elemental-live-encoder/media-services-elemental5.png)

1. <span data-ttu-id="82a0d-173">取得 hello 通道的輸入的 URL。</span><span class="sxs-lookup"><span data-stu-id="82a0d-173">Get hello channel's input URL.</span></span>

    <span data-ttu-id="82a0d-174">瀏覽後 toohello AMSE 工具，並檢查 hello 通道完成狀態。</span><span class="sxs-lookup"><span data-stu-id="82a0d-174">Navigate back toohello AMSE tool, and check on hello channel completion status.</span></span> <span data-ttu-id="82a0d-175">一旦 hello 狀態已從**起始**太**執行**，您可以取得 hello 輸入的 URL。</span><span class="sxs-lookup"><span data-stu-id="82a0d-175">Once hello State has changed from **Starting** too**Running**, you can get hello input URL.</span></span>

    <span data-ttu-id="82a0d-176">當執行 hello 通道時，hello 通道名稱上按一下滑鼠右鍵、 向下 toohover 巡覽**複製輸入 URL tooclipboard** ，然後選取 **主要輸入 URL**。</span><span class="sxs-lookup"><span data-stu-id="82a0d-176">When hello channel is running, right click hello channel name, navigate down toohover over **Copy Input URL tooclipboard** and then select **Primary Input  URL**.</span></span>  

    ![Elemental](./media/media-services-elemental-live-encoder/media-services-elemental6.png)
2. <span data-ttu-id="82a0d-178">此資訊貼在 hello**主要目的**hello Elemental 欄位。</span><span class="sxs-lookup"><span data-stu-id="82a0d-178">Paste this information in hello **Primary Destination** field of hello Elemental.</span></span> <span data-ttu-id="82a0d-179">所有其他設定可以維持 hello 預設值。</span><span class="sxs-lookup"><span data-stu-id="82a0d-179">All other settings can remain hello default.</span></span>

    ![Elemental](./media/media-services-elemental-live-encoder/media-services-elemental14.png)

    <span data-ttu-id="82a0d-181">如需額外的備援，重複這些步驟以 hello 次要輸入 URL UDP/TS 串流建立個別的 「 輸出 」 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="82a0d-181">For extra redundancy, repeat these steps with hello Secondary Input URL by creating a separate "Output" tab for UDP/TS Streaming.</span></span>
3. <span data-ttu-id="82a0d-182">按一下**建立**（如果已建立新事件） 或**更新**（如果正在編輯現有的事件），然後再繼續 toostart hello 編碼器。</span><span class="sxs-lookup"><span data-stu-id="82a0d-182">Click **Create** (if a new event was created) or **Update** (if editing a pre-existing event) and then proceed toostart hello encoder.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="82a0d-183">在您按一下之前**啟動**hello 元素即時 web 介面上，您**必須**確保 hello 通道已就緒。</span><span class="sxs-lookup"><span data-stu-id="82a0d-183">Before you click **Start** on hello Elemental Live web interface, you **must** ensure that hello Channel is ready.</span></span>
> <span data-ttu-id="82a0d-184">此外，請確定未 tooleave hello 通道處於就緒狀態，但不超過 > 15 分鐘的事件。</span><span class="sxs-lookup"><span data-stu-id="82a0d-184">Also, make sure not tooleave hello Channel in a ready state without an event for longer than > 15 minutes.</span></span>
>
>

<span data-ttu-id="82a0d-185">Hello 資料流已執行 30 秒後，瀏覽後 toohello AMSE 工具和測試播放。</span><span class="sxs-lookup"><span data-stu-id="82a0d-185">After hello stream has been running for 30 seconds, navigate back toohello AMSE tool and test playback.</span></span>  

### <a name="test-playback"></a><span data-ttu-id="82a0d-186">測試播放</span><span class="sxs-lookup"><span data-stu-id="82a0d-186">Test playback</span></span>

<span data-ttu-id="82a0d-187">瀏覽 toohello AMSE 工具，並以滑鼠右鍵按一下 hello 通道 toobe 測試。</span><span class="sxs-lookup"><span data-stu-id="82a0d-187">Navigate toohello AMSE tool, and right click hello channel toobe tested.</span></span> <span data-ttu-id="82a0d-188">從 [hello] 功能表中，將滑鼠停留在**播放 hello 預覽**選取**使用 Azure Media Player**。</span><span class="sxs-lookup"><span data-stu-id="82a0d-188">From hello menu, hover over **Playback hello Preview** and select **with Azure Media Player**.</span></span>  

    ![Elemental](./media/media-services-elemental-live-encoder/media-services-elemental8.png)

<span data-ttu-id="82a0d-189">Hello 資料流會顯示 hello 播放程式中，如果 hello 編碼器已經過正確設定的 tooconnect tooAMS。</span><span class="sxs-lookup"><span data-stu-id="82a0d-189">If hello stream appears in hello player, then hello encoder has been properly configured tooconnect tooAMS.</span></span>

<span data-ttu-id="82a0d-190">如果收到錯誤，hello 通道必須調整 toobe 重設和編碼器設定。</span><span class="sxs-lookup"><span data-stu-id="82a0d-190">If an error is received, hello channel will need toobe reset and encoder settings adjusted.</span></span> <span data-ttu-id="82a0d-191">請參閱 hello[疑難排解](media-services-troubleshooting-live-streaming.md)指引主題。</span><span class="sxs-lookup"><span data-stu-id="82a0d-191">Please see hello [troubleshooting](media-services-troubleshooting-live-streaming.md) topic for guidance.</span></span>   

### <a name="create-a-program"></a><span data-ttu-id="82a0d-192">建立程式</span><span class="sxs-lookup"><span data-stu-id="82a0d-192">Create a program</span></span>
1. <span data-ttu-id="82a0d-193">一旦確認通道播放沒問題後，請建立程式。</span><span class="sxs-lookup"><span data-stu-id="82a0d-193">Once channel playback is confirmed, create a program.</span></span> <span data-ttu-id="82a0d-194">在 hello **Live** hello AMSE 工具中索引標籤上，在 hello 程式區域按一下滑鼠右鍵並選取**建立新的程式**。</span><span class="sxs-lookup"><span data-stu-id="82a0d-194">Under hello **Live** tab in hello AMSE tool, right click within hello program area and select **Create New Program**.</span></span>  

    ![Elemental](./media/media-services-elemental-live-encoder/media-services-elemental9.png)
2. <span data-ttu-id="82a0d-196">Hello 程式，並有需要則調整 hello**封存時間長度**（預設值 too4 時段）。</span><span class="sxs-lookup"><span data-stu-id="82a0d-196">Name hello program and, if needed, adjust hello **Archive Window Length** (which defaults too4 hours).</span></span> <span data-ttu-id="82a0d-197">您也可以指定儲存體位置，或保留 hello 預設。</span><span class="sxs-lookup"><span data-stu-id="82a0d-197">You can also specify a storage location or leave as hello default.</span></span>  
3. <span data-ttu-id="82a0d-198">檢查 hello**開始 hello 程式現在**方塊。</span><span class="sxs-lookup"><span data-stu-id="82a0d-198">Check hello **Start hello Program now** box.</span></span>
4. <span data-ttu-id="82a0d-199">按一下 [建立程式] 。</span><span class="sxs-lookup"><span data-stu-id="82a0d-199">Click **Create Program**.</span></span>  

    >[!NOTE]
    > <span data-ttu-id="82a0d-200">建立程式時所使用的時間會比建立通道時少。</span><span class="sxs-lookup"><span data-stu-id="82a0d-200">Program creation takes less time than channel creation.</span></span>   
      
5. <span data-ttu-id="82a0d-201">Hello 程式開始執行之後，以確認播放 hello 程式上按一下滑鼠右鍵，瀏覽過**播放 hello （_r)** ，然後選取 **使用 Azure Media Player**。</span><span class="sxs-lookup"><span data-stu-id="82a0d-201">Once hello program is running, confirm playback by right clicking hello program and navigating too**Playback hello program(s)** and then selecting **with Azure Media Player**.</span></span>  
6. <span data-ttu-id="82a0d-202">確認，以滑鼠右鍵按一下 hello 程式，並選取**複製 hello 輸出 URL tooClipboard** (或擷取這項資訊從 hello**程式資訊和設定**hello 功能表選項)。</span><span class="sxs-lookup"><span data-stu-id="82a0d-202">Once confirmed, right click hello program again and select **Copy hello Output URL tooClipboard** (or retrieve this information from hello **Program information and settings** option from hello menu).</span></span>

<span data-ttu-id="82a0d-203">hello 資料流已準備好 toobe 內嵌在播放程式，或分散式的 tooan 對象的即時檢視。</span><span class="sxs-lookup"><span data-stu-id="82a0d-203">hello stream is now ready toobe embedded in a player, or distributed tooan audience for live viewing.</span></span>  

## <a name="troubleshooting"></a><span data-ttu-id="82a0d-204">疑難排解</span><span class="sxs-lookup"><span data-stu-id="82a0d-204">Troubleshooting</span></span>
<span data-ttu-id="82a0d-205">請參閱 hello[疑難排解](media-services-troubleshooting-live-streaming.md)指引主題。</span><span class="sxs-lookup"><span data-stu-id="82a0d-205">Please see hello [troubleshooting](media-services-troubleshooting-live-streaming.md) topic for guidance.</span></span>

## <a name="media-services-learning-paths"></a><span data-ttu-id="82a0d-206">媒體服務學習路徑</span><span class="sxs-lookup"><span data-stu-id="82a0d-206">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="82a0d-207">提供意見反應</span><span class="sxs-lookup"><span data-stu-id="82a0d-207">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]
