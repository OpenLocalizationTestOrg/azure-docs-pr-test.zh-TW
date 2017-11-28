---
title: "aaaConfigure hello FMLE 編碼器 toosend 單一位元速率即時資料流 |Microsoft 文件"
description: "本主題說明如何 tooconfigure 會 hello 快閃媒體即時編碼器 」 (FMLE) 編碼器 toosend 即時編碼啟用單一位元速率串流 tooAMS 通道。"
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: 3113f333-517a-47a1-a1b3-57e200c6b2a2
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: ne
ms.topic: article
ms.date: 01/05/2017
ms.author: juliako;cenkdin;anilmur
ms.openlocfilehash: 780d911c5186ec09c784264f9a0d0c3f8059d305
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-fmle-encoder-toosend-a-single-bitrate-live-stream"></a><span data-ttu-id="5986a-103">使用 hello FMLE 編碼器 toosend 單一位元速率即時資料流</span><span class="sxs-lookup"><span data-stu-id="5986a-103">Use hello FMLE encoder toosend a single bitrate live stream</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="5986a-104">FMLE</span><span class="sxs-lookup"><span data-stu-id="5986a-104">FMLE</span></span>](media-services-configure-fmle-live-encoder.md)
> * [<span data-ttu-id="5986a-105">Elemental Live</span><span class="sxs-lookup"><span data-stu-id="5986a-105">Elemental Live</span></span>](media-services-configure-elemental-live-encoder.md)
> * [<span data-ttu-id="5986a-106">Tricaster</span><span class="sxs-lookup"><span data-stu-id="5986a-106">Tricaster</span></span>](media-services-configure-tricaster-live-encoder.md)
> * [<span data-ttu-id="5986a-107">Wirecast</span><span class="sxs-lookup"><span data-stu-id="5986a-107">Wirecast</span></span>](media-services-configure-wirecast-live-encoder.md)
>
>

<span data-ttu-id="5986a-108">本主題說明如何 tooconfigure hello[快閃媒體即時編碼程式](http://www.adobe.com/products/flash-media-encoder.html)(FMLE) 編碼器 toosend 單一位元速率串流的即時編碼啟用 tooAMS 通道。</span><span class="sxs-lookup"><span data-stu-id="5986a-108">This topic shows how tooconfigure hello [Flash Media Live Encoder](http://www.adobe.com/products/flash-media-encoder.html) (FMLE) encoder toosend a single bitrate stream tooAMS channels that are enabled for live encoding.</span></span> <span data-ttu-id="5986a-109">如需詳細資訊，請參閱[使用通道，會啟用 tooPerform Live 使用 Azure 媒體服務編碼](media-services-manage-live-encoder-enabled-channels.md)。</span><span class="sxs-lookup"><span data-stu-id="5986a-109">For more information, see [Working with Channels that are Enabled tooPerform Live Encoding with Azure Media Services](media-services-manage-live-encoder-enabled-channels.md).</span></span>

<span data-ttu-id="5986a-110">本教學課程示範如何 toomanage Azure 媒體服務 (AMS) 中使用 Azure 媒體服務總管 (AMSE) 工具。</span><span class="sxs-lookup"><span data-stu-id="5986a-110">This tutorial shows how toomanage Azure Media Services (AMS) with Azure Media Services Explorer (AMSE) tool.</span></span> <span data-ttu-id="5986a-111">此工具只會在 Windows 電腦上執行。</span><span class="sxs-lookup"><span data-stu-id="5986a-111">This tool only runs on Windows PC.</span></span> <span data-ttu-id="5986a-112">如果您是在 Mac 或 Linux 上，使用 Azure 入口網站 toocreate hello[通道](media-services-portal-creating-live-encoder-enabled-channel.md#create-a-channel)和[程式](media-services-portal-creating-live-encoder-enabled-channel.md)。</span><span class="sxs-lookup"><span data-stu-id="5986a-112">If you are on Mac or Linux, use hello Azure portal toocreate [channels](media-services-portal-creating-live-encoder-enabled-channel.md#create-a-channel) and [programs](media-services-portal-creating-live-encoder-enabled-channel.md).</span></span>

<span data-ttu-id="5986a-113">請注意，本教學課程會說明如何使用 AAC。</span><span class="sxs-lookup"><span data-stu-id="5986a-113">Note that this tutorial describes using AAC.</span></span> <span data-ttu-id="5986a-114">不過，依預設 FMLE 不支援 AAC。</span><span class="sxs-lookup"><span data-stu-id="5986a-114">However, FMLE doesn’t supports AAC by default.</span></span> <span data-ttu-id="5986a-115">您需要 toopurchase AAC 編碼的外掛程式例如 MainConcept: [AAC 外掛程式](http://www.mainconcept.com/products/plug-ins/plug-ins-for-adobe/aac-encoder-fmle.html)</span><span class="sxs-lookup"><span data-stu-id="5986a-115">You would need toopurchase a plugin for AAC encoding such as from MainConcept: [AAC plugin](http://www.mainconcept.com/products/plug-ins/plug-ins-for-adobe/aac-encoder-fmle.html)</span></span>

## <a name="prerequisites"></a><span data-ttu-id="5986a-116">必要條件</span><span class="sxs-lookup"><span data-stu-id="5986a-116">Prerequisites</span></span>
* [<span data-ttu-id="5986a-117">建立 Azure 媒體服務帳戶</span><span class="sxs-lookup"><span data-stu-id="5986a-117">Create an Azure Media Services account</span></span>](media-services-portal-create-account.md)
* <span data-ttu-id="5986a-118">確定有執行中的「串流端點」。</span><span class="sxs-lookup"><span data-stu-id="5986a-118">Ensure there is a Streaming Endpoint running.</span></span> <span data-ttu-id="5986a-119">如需詳細資訊，請參閱 [在媒體服務帳戶中管理串流端點](media-services-portal-manage-streaming-endpoints.md)</span><span class="sxs-lookup"><span data-stu-id="5986a-119">For more information, see [Manage Streaming Endpoints in a Media Services Account](media-services-portal-manage-streaming-endpoints.md)</span></span>
* <span data-ttu-id="5986a-120">安裝 hello 最新版 hello [AMSE](https://github.com/Azure/Azure-Media-Services-Explorer)工具。</span><span class="sxs-lookup"><span data-stu-id="5986a-120">Install hello latest version of hello [AMSE](https://github.com/Azure/Azure-Media-Services-Explorer) tool.</span></span>
* <span data-ttu-id="5986a-121">啟動 hello 工具和 tooyour AMS 帳戶連接。</span><span class="sxs-lookup"><span data-stu-id="5986a-121">Launch hello tool and connect tooyour AMS account.</span></span>

## <a name="tips"></a><span data-ttu-id="5986a-122">祕訣</span><span class="sxs-lookup"><span data-stu-id="5986a-122">Tips</span></span>
* <span data-ttu-id="5986a-123">請盡可能使用實體的有線網際網路連線。</span><span class="sxs-lookup"><span data-stu-id="5986a-123">Whenever possible, use a hardwired internet connection.</span></span>
* <span data-ttu-id="5986a-124">最佳經驗法則時判斷頻寬需求為串流處理位元的 toodouble hello。</span><span class="sxs-lookup"><span data-stu-id="5986a-124">A good rule of thumb when determining bandwidth requirements is toodouble hello streaming bitrates.</span></span> <span data-ttu-id="5986a-125">雖然這不是強制性需求，有助於減少 hello 發生網路壅塞的影響。</span><span class="sxs-lookup"><span data-stu-id="5986a-125">While this is not a mandatory requirement, it will help mitigate hello impact of network congestion.</span></span>
* <span data-ttu-id="5986a-126">使用軟體型編碼器時，請關閉任何不必要的程式。</span><span class="sxs-lookup"><span data-stu-id="5986a-126">When using software based encoders, close out any unnecessary programs.</span></span>

## <a name="create-a-channel"></a><span data-ttu-id="5986a-127">建立通道</span><span class="sxs-lookup"><span data-stu-id="5986a-127">Create a channel</span></span>
1. <span data-ttu-id="5986a-128">在 hello AMSE 工具中，瀏覽 toohello **Live**索引標籤，然後以滑鼠右鍵按一下 hello 通道區域內。</span><span class="sxs-lookup"><span data-stu-id="5986a-128">In hello AMSE tool, navigate toohello **Live** tab, and right click within hello channel area.</span></span> <span data-ttu-id="5986a-129">從功能表選取 [建立通道...] </span><span class="sxs-lookup"><span data-stu-id="5986a-129">Select **Create channel…**</span></span> <span data-ttu-id="5986a-130">從 [hello] 功能表中。</span><span class="sxs-lookup"><span data-stu-id="5986a-130">from hello menu.</span></span>

    ![FMLE](./media/media-services-fmle-live-encoder/media-services-fmle1.png)

2. <span data-ttu-id="5986a-132">指定通道名稱，hello 描述欄位是選擇性的。</span><span class="sxs-lookup"><span data-stu-id="5986a-132">Specify a channel name, hello description field is optional.</span></span> <span data-ttu-id="5986a-133">在 [通道設定] 下選取**標準**hello 即時編碼選項，以 hello 輸入通訊協定設定得**RTMP**。</span><span class="sxs-lookup"><span data-stu-id="5986a-133">Under Channel Settings, select **Standard** for hello Live Encoding option, with hello Input Protocol set too**RTMP**.</span></span> <span data-ttu-id="5986a-134">您可以將所有其他設定保留現狀。</span><span class="sxs-lookup"><span data-stu-id="5986a-134">You can leave all other settings as is.</span></span>

    <span data-ttu-id="5986a-135">請確定 hello**開始 hello 新通道現在**已選取。</span><span class="sxs-lookup"><span data-stu-id="5986a-135">Make sure hello **Start hello new channel now** is selected.</span></span>

3. <span data-ttu-id="5986a-136">按一下 [ **建立頻道**]。</span><span class="sxs-lookup"><span data-stu-id="5986a-136">Click **Create Channel**.</span></span>

   ![FMLE](./media/media-services-fmle-live-encoder/media-services-fmle2.png)

> [!NOTE]
> <span data-ttu-id="5986a-138">hello 通道花費 20 分鐘 toostart 一樣長。</span><span class="sxs-lookup"><span data-stu-id="5986a-138">hello channel can take as long as 20 minutes toostart.</span></span>
>
>

<span data-ttu-id="5986a-139">您可以啟動 hello 通道時[設定 hello 編碼器](media-services-configure-fmle-live-encoder.md#configure_fmle_rtmp)。</span><span class="sxs-lookup"><span data-stu-id="5986a-139">While hello channel is starting you can [configure hello encoder](media-services-configure-fmle-live-encoder.md#configure_fmle_rtmp).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="5986a-140">請注意，只要通道進入就緒狀態，就會開始計費。</span><span class="sxs-lookup"><span data-stu-id="5986a-140">Note that billing starts as soon as Channel goes into a ready state.</span></span> <span data-ttu-id="5986a-141">如需詳細資訊，請參閱 [通道的狀態](media-services-manage-live-encoder-enabled-channels.md#states)。</span><span class="sxs-lookup"><span data-stu-id="5986a-141">For more information, see [Channel's states](media-services-manage-live-encoder-enabled-channels.md#states).</span></span>
>
>

## <span data-ttu-id="5986a-142"><a id=configure_fmle_rtmp></a>設定 hello FMLE 編碼器</span><span class="sxs-lookup"><span data-stu-id="5986a-142"><a id=configure_fmle_rtmp></a>Configure hello FMLE encoder</span></span>
<span data-ttu-id="5986a-143">在此教學課程的 hello 會使用下列的輸出設定。</span><span class="sxs-lookup"><span data-stu-id="5986a-143">In this tutorial hello following output settings are used.</span></span> <span data-ttu-id="5986a-144">hello 本節其餘部分描述更詳細的組態步驟。</span><span class="sxs-lookup"><span data-stu-id="5986a-144">hello rest of this section describes configuration steps in more detail.</span></span>

<span data-ttu-id="5986a-145">**視訊**：</span><span class="sxs-lookup"><span data-stu-id="5986a-145">**Video**:</span></span>

* <span data-ttu-id="5986a-146">轉碼器：H.264</span><span class="sxs-lookup"><span data-stu-id="5986a-146">Codec: H.264</span></span>
* <span data-ttu-id="5986a-147">設定檔：高 (層級 4.0)</span><span class="sxs-lookup"><span data-stu-id="5986a-147">Profile: High (Level 4.0)</span></span>
* <span data-ttu-id="5986a-148">位元速率：5000 kbps</span><span class="sxs-lookup"><span data-stu-id="5986a-148">Bitrate: 5000 kbps</span></span>
* <span data-ttu-id="5986a-149">主要畫面格：2 秒 (60 秒)</span><span class="sxs-lookup"><span data-stu-id="5986a-149">Keyframe: 2 seconds (60 seconds)</span></span>
* <span data-ttu-id="5986a-150">畫面播放速率：30</span><span class="sxs-lookup"><span data-stu-id="5986a-150">Frame Rate: 30</span></span>

<span data-ttu-id="5986a-151">**音訊**：</span><span class="sxs-lookup"><span data-stu-id="5986a-151">**Audio**:</span></span>

* <span data-ttu-id="5986a-152">轉碼器：AAC (LC)</span><span class="sxs-lookup"><span data-stu-id="5986a-152">Codec: AAC (LC)</span></span>
* <span data-ttu-id="5986a-153">位元速率：192 kbps</span><span class="sxs-lookup"><span data-stu-id="5986a-153">Bitrate: 192 kbps</span></span>
* <span data-ttu-id="5986a-154">取樣速率：44.1 kHz</span><span class="sxs-lookup"><span data-stu-id="5986a-154">Sample Rate: 44.1 kHz</span></span>

### <a name="configuration-steps"></a><span data-ttu-id="5986a-155">組態步驟</span><span class="sxs-lookup"><span data-stu-id="5986a-155">Configuration steps</span></span>
1. <span data-ttu-id="5986a-156">瀏覽的 toohello 快閃媒體即時編碼器的 (FMLE) 介面使用的 hello 機器。</span><span class="sxs-lookup"><span data-stu-id="5986a-156">Navigate toohello Flash Media Live Encoder’s (FMLE) interface on hello machine being used.</span></span>

    <span data-ttu-id="5986a-157">hello 介面是一個設定的主要頁面。</span><span class="sxs-lookup"><span data-stu-id="5986a-157">hello interface is one main page of settings.</span></span> <span data-ttu-id="5986a-158">請記下 hello 下列建議的設定 tooget 啟動與使用 FMLE 資料流。</span><span class="sxs-lookup"><span data-stu-id="5986a-158">Please take note of hello following recommended settings tooget started with streaming using FMLE.</span></span>

   * <span data-ttu-id="5986a-159">格式：H.264 畫面播放速率：30.00</span><span class="sxs-lookup"><span data-stu-id="5986a-159">Format: H.264 Frame Rate: 30.00</span></span>
   * <span data-ttu-id="5986a-160">輸入大小：1280 x 720</span><span class="sxs-lookup"><span data-stu-id="5986a-160">Input Size: 1280 x 720</span></span>
   * <span data-ttu-id="5986a-161">位元速率：5000 Kbps (可視網路限制加以調整)</span><span class="sxs-lookup"><span data-stu-id="5986a-161">Bit Rate: 5000 Kbps (Can be adjusted based on network limitations)</span></span>  

     ![FMLE](./media/media-services-fmle-live-encoder/media-services-fmle3.png)

     <span data-ttu-id="5986a-163">當使用交錯式來源時，請核取記號 hello"非交錯 」 選項</span><span class="sxs-lookup"><span data-stu-id="5986a-163">When using interlaced sources, please checkmark hello “Deinterlace” option</span></span>
2. <span data-ttu-id="5986a-164">選取 hello 扳手圖示下一步 tooFormat，這些額外的設定應該是：</span><span class="sxs-lookup"><span data-stu-id="5986a-164">Select hello wrench icon next tooFormat, these additional settings should be:</span></span>

   * <span data-ttu-id="5986a-165">設定檔：主要</span><span class="sxs-lookup"><span data-stu-id="5986a-165">Profile: Main</span></span>
   * <span data-ttu-id="5986a-166">層級：4.0</span><span class="sxs-lookup"><span data-stu-id="5986a-166">Level: 4.0</span></span>
   * <span data-ttu-id="5986a-167">主要畫面格頻率：2 秒</span><span class="sxs-lookup"><span data-stu-id="5986a-167">Keyframe Frequency: 2 seconds</span></span>

     ![FMLE](./media/media-services-fmle-live-encoder/media-services-fmle4.png)
3. <span data-ttu-id="5986a-169">設定下列重要的音訊設定 hello:</span><span class="sxs-lookup"><span data-stu-id="5986a-169">Set hello following important audio setting:</span></span>

   * <span data-ttu-id="5986a-170">格式：AAC</span><span class="sxs-lookup"><span data-stu-id="5986a-170">Format: AAC</span></span>
   * <span data-ttu-id="5986a-171">取樣速率：44100 Hz</span><span class="sxs-lookup"><span data-stu-id="5986a-171">Sample Rate: 44100 Hz</span></span>
   * <span data-ttu-id="5986a-172">位元速率：192 kbps</span><span class="sxs-lookup"><span data-stu-id="5986a-172">Bitrate: 192 Kbps</span></span>

     ![FMLE](./media/media-services-fmle-live-encoder/media-services-fmle5.png)
4. <span data-ttu-id="5986a-174">取得順序 tooassign hello 通道的輸入的 URL 它 toohello FMLE 的**RTMP 端點**。</span><span class="sxs-lookup"><span data-stu-id="5986a-174">Get hello channel's input URL in order tooassign it toohello FMLE's **RTMP Endpoint**.</span></span>

    <span data-ttu-id="5986a-175">瀏覽後 toohello AMSE 工具，並檢查 hello 通道完成狀態。</span><span class="sxs-lookup"><span data-stu-id="5986a-175">Navigate back toohello AMSE tool, and check on hello channel completion status.</span></span> <span data-ttu-id="5986a-176">一旦 hello 狀態已從**起始**太**執行**，您可以取得 hello 輸入的 URL。</span><span class="sxs-lookup"><span data-stu-id="5986a-176">Once hello State has changed from **Starting** too**Running**, you can get hello input URL.</span></span>

    <span data-ttu-id="5986a-177">當執行 hello 通道時，hello 通道名稱上按一下滑鼠右鍵、 向下 toohover 巡覽**複製輸入 URL tooclipboard** ，然後選取 **主要輸入 URL**。</span><span class="sxs-lookup"><span data-stu-id="5986a-177">When hello channel is running, right click hello channel name, navigate down toohover over **Copy Input URL tooclipboard** and then select **Primary Input  URL**.</span></span>  

    ![FMLE](./media/media-services-fmle-live-encoder/media-services-fmle6.png)
5. <span data-ttu-id="5986a-179">此資訊貼在 hello **FMS URL** hello 輸出區段中，並指派資料流名稱的欄位。</span><span class="sxs-lookup"><span data-stu-id="5986a-179">Paste this information in hello **FMS URL** field of hello output section, and assign a stream name.</span></span>

    ![FMLE](./media/media-services-fmle-live-encoder/media-services-fmle7.png)

    <span data-ttu-id="5986a-181">如需額外的備援，重複這些步驟以 hello 次要輸入 URL。</span><span class="sxs-lookup"><span data-stu-id="5986a-181">For extra redundancy, repeat these steps with hello Secondary Input URL.</span></span>
6. <span data-ttu-id="5986a-182">選取 [ **連接**]。</span><span class="sxs-lookup"><span data-stu-id="5986a-182">Select **Connect**.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="5986a-183">在您按一下之前**連接**，您**必須**確保 hello 通道已就緒。</span><span class="sxs-lookup"><span data-stu-id="5986a-183">Before you click **Connect**, you **must** ensure that hello Channel is ready.</span></span>
> <span data-ttu-id="5986a-184">此外，請確定未 tooleave hello 通道處於就緒狀態，而輸入的比重不摘要超過 > 15 分鐘。</span><span class="sxs-lookup"><span data-stu-id="5986a-184">Also, make sure not tooleave hello Channel in a ready state without an input contribution feed for longer than > 15 minutes.</span></span>
>
>

## <a name="test-playback"></a><span data-ttu-id="5986a-185">測試播放</span><span class="sxs-lookup"><span data-stu-id="5986a-185">Test playback</span></span>

<span data-ttu-id="5986a-186">瀏覽 toohello AMSE 工具，並以滑鼠右鍵按一下 hello 通道 toobe 測試。</span><span class="sxs-lookup"><span data-stu-id="5986a-186">Navigate toohello AMSE tool, and right click hello channel toobe tested.</span></span> <span data-ttu-id="5986a-187">從 [hello] 功能表中，將滑鼠停留在**播放 hello 預覽**選取**使用 Azure Media Player**。</span><span class="sxs-lookup"><span data-stu-id="5986a-187">From hello menu, hover over **Playback hello Preview** and select **with Azure Media Player**.</span></span>  

    ![fmle](./media/media-services-fmle-live-encoder/media-services-fmle8.png)

<span data-ttu-id="5986a-188">Hello 資料流會顯示 hello 播放程式中，如果 hello 編碼器已經過正確設定的 tooconnect tooAMS。</span><span class="sxs-lookup"><span data-stu-id="5986a-188">If hello stream appears in hello player, then hello encoder has been properly configured tooconnect tooAMS.</span></span>

<span data-ttu-id="5986a-189">如果收到錯誤，hello 通道必須調整 toobe 重設和編碼器設定。</span><span class="sxs-lookup"><span data-stu-id="5986a-189">If an error is received, hello channel will need toobe reset and encoder settings adjusted.</span></span> <span data-ttu-id="5986a-190">請參閱 hello[疑難排解](media-services-troubleshooting-live-streaming.md)指引主題。</span><span class="sxs-lookup"><span data-stu-id="5986a-190">Please see hello [troubleshooting](media-services-troubleshooting-live-streaming.md) topic for guidance.</span></span>  

## <a name="create-a-program"></a><span data-ttu-id="5986a-191">建立程式</span><span class="sxs-lookup"><span data-stu-id="5986a-191">Create a program</span></span>
1. <span data-ttu-id="5986a-192">一旦確認通道播放沒問題後，請建立程式。</span><span class="sxs-lookup"><span data-stu-id="5986a-192">Once channel playback is confirmed, create a program.</span></span> <span data-ttu-id="5986a-193">在 hello **Live** hello AMSE 工具中索引標籤上，在 hello 程式區域按一下滑鼠右鍵並選取**建立新的程式**。</span><span class="sxs-lookup"><span data-stu-id="5986a-193">Under hello **Live** tab in hello AMSE tool, right click within hello program area and select **Create New Program**.</span></span>  

    ![FMLE](./media/media-services-fmle-live-encoder/media-services-fmle9.png)
2. <span data-ttu-id="5986a-195">Hello 程式，並有需要則調整 hello**封存時間長度**（預設值 too4 時段）。</span><span class="sxs-lookup"><span data-stu-id="5986a-195">Name hello program and, if needed, adjust hello **Archive Window Length** (which defaults too4 hours).</span></span> <span data-ttu-id="5986a-196">您也可以指定儲存體位置，或保留 hello 預設。</span><span class="sxs-lookup"><span data-stu-id="5986a-196">You can also specify a storage location or leave as hello default.</span></span>  
3. <span data-ttu-id="5986a-197">檢查 hello**開始 hello 程式現在**方塊。</span><span class="sxs-lookup"><span data-stu-id="5986a-197">Check hello **Start hello Program now** box.</span></span>
4. <span data-ttu-id="5986a-198">按一下 [建立程式] 。</span><span class="sxs-lookup"><span data-stu-id="5986a-198">Click **Create Program**.</span></span>  

    >[!NOTE]
    ><span data-ttu-id="5986a-199">建立程式時所使用的時間會比建立通道時少。</span><span class="sxs-lookup"><span data-stu-id="5986a-199">Program creation takes less time than channel creation.</span></span>
        
5. <span data-ttu-id="5986a-200">Hello 程式開始執行之後，以確認播放 hello 程式上按一下滑鼠右鍵，瀏覽過**播放 hello （_r)** ，然後選取 **使用 Azure Media Player**。</span><span class="sxs-lookup"><span data-stu-id="5986a-200">Once hello program is running, confirm playback by right clicking hello program and navigating too**Playback hello program(s)** and then selecting **with Azure Media Player**.</span></span>  
6. <span data-ttu-id="5986a-201">確認，以滑鼠右鍵按一下 hello 程式，並選取**複製 hello 輸出 URL tooClipboard** (或擷取這項資訊從 hello**程式資訊和設定**hello 功能表選項)。</span><span class="sxs-lookup"><span data-stu-id="5986a-201">Once confirmed, right click hello program again and select **Copy hello Output URL tooClipboard** (or retrieve this information from hello **Program information and settings** option from hello menu).</span></span>

<span data-ttu-id="5986a-202">hello 資料流已準備好 toobe 內嵌在播放程式，或分散式的 tooan 對象的即時檢視。</span><span class="sxs-lookup"><span data-stu-id="5986a-202">hello stream is now ready toobe embedded in a player, or distributed tooan audience for live viewing.</span></span>  

## <a name="troubleshooting"></a><span data-ttu-id="5986a-203">疑難排解</span><span class="sxs-lookup"><span data-stu-id="5986a-203">Troubleshooting</span></span>
<span data-ttu-id="5986a-204">請參閱 hello[疑難排解](media-services-troubleshooting-live-streaming.md)指引主題。</span><span class="sxs-lookup"><span data-stu-id="5986a-204">Please see hello [troubleshooting](media-services-troubleshooting-live-streaming.md) topic for guidance.</span></span>

## <a name="media-services-learning-paths"></a><span data-ttu-id="5986a-205">媒體服務學習路徑</span><span class="sxs-lookup"><span data-stu-id="5986a-205">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="5986a-206">提供意見反應</span><span class="sxs-lookup"><span data-stu-id="5986a-206">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]
