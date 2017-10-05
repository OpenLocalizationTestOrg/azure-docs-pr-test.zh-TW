---
title: "設定 FMLE 編碼器來傳送單一位元速率的即時串流 | Microsoft Docs"
description: "本主題示範如何設定 Flash Media Live Encoder (FMLE) 編碼器，藉此將單一位元速率的即時串流傳送到已啟用即時編碼的 AMS 通道。"
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
ms.openlocfilehash: e831048f34ecf6e89595adc4bfd58b5977e04bdb
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="use-the-fmle-encoder-to-send-a-single-bitrate-live-stream"></a><span data-ttu-id="63003-103">使用 FMLE 編碼器來傳送單一位元速率的即時串流</span><span class="sxs-lookup"><span data-stu-id="63003-103">Use the FMLE encoder to send a single bitrate live stream</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="63003-104">FMLE</span><span class="sxs-lookup"><span data-stu-id="63003-104">FMLE</span></span>](media-services-configure-fmle-live-encoder.md)
> * [<span data-ttu-id="63003-105">Elemental Live</span><span class="sxs-lookup"><span data-stu-id="63003-105">Elemental Live</span></span>](media-services-configure-elemental-live-encoder.md)
> * [<span data-ttu-id="63003-106">Tricaster</span><span class="sxs-lookup"><span data-stu-id="63003-106">Tricaster</span></span>](media-services-configure-tricaster-live-encoder.md)
> * [<span data-ttu-id="63003-107">Wirecast</span><span class="sxs-lookup"><span data-stu-id="63003-107">Wirecast</span></span>](media-services-configure-wirecast-live-encoder.md)
>
>

<span data-ttu-id="63003-108">本主題示範如何設定 [Flash Media Live Encoder](http://www.adobe.com/products/flash-media-encoder.html) (FMLE) 編碼器，藉此將單一位元速率的即時串流傳送到已啟用即時編碼的 AMS 通道。</span><span class="sxs-lookup"><span data-stu-id="63003-108">This topic shows how to configure the [Flash Media Live Encoder](http://www.adobe.com/products/flash-media-encoder.html) (FMLE) encoder to send a single bitrate stream to AMS channels that are enabled for live encoding.</span></span> <span data-ttu-id="63003-109">如需詳細資訊，請參閱 [使用啟用的通道來以 Azure 媒體服務執行即時編碼](media-services-manage-live-encoder-enabled-channels.md)。</span><span class="sxs-lookup"><span data-stu-id="63003-109">For more information, see [Working with Channels that are Enabled to Perform Live Encoding with Azure Media Services](media-services-manage-live-encoder-enabled-channels.md).</span></span>

<span data-ttu-id="63003-110">本教學課程示範如何使用 Azure 媒體服務總管 (AMSE) 工具管理 Azure 媒體服務 (AMS)。</span><span class="sxs-lookup"><span data-stu-id="63003-110">This tutorial shows how to manage Azure Media Services (AMS) with Azure Media Services Explorer (AMSE) tool.</span></span> <span data-ttu-id="63003-111">此工具只會在 Windows 電腦上執行。</span><span class="sxs-lookup"><span data-stu-id="63003-111">This tool only runs on Windows PC.</span></span> <span data-ttu-id="63003-112">如果您是用 Mac 或 Linux，請使用 Azure 入口網站建立[通道](media-services-portal-creating-live-encoder-enabled-channel.md#create-a-channel)和[程式](media-services-portal-creating-live-encoder-enabled-channel.md)。</span><span class="sxs-lookup"><span data-stu-id="63003-112">If you are on Mac or Linux, use the Azure portal to create [channels](media-services-portal-creating-live-encoder-enabled-channel.md#create-a-channel) and [programs](media-services-portal-creating-live-encoder-enabled-channel.md).</span></span>

<span data-ttu-id="63003-113">請注意，本教學課程會說明如何使用 AAC。</span><span class="sxs-lookup"><span data-stu-id="63003-113">Note that this tutorial describes using AAC.</span></span> <span data-ttu-id="63003-114">不過，依預設 FMLE 不支援 AAC。</span><span class="sxs-lookup"><span data-stu-id="63003-114">However, FMLE doesn’t supports AAC by default.</span></span> <span data-ttu-id="63003-115">您必須購買 AAC 編碼的外掛程式，例如從 MainConcept 購買 [AAC 外掛程式](http://www.mainconcept.com/products/plug-ins/plug-ins-for-adobe/aac-encoder-fmle.html)</span><span class="sxs-lookup"><span data-stu-id="63003-115">You would need to purchase a plugin for AAC encoding such as from MainConcept: [AAC plugin](http://www.mainconcept.com/products/plug-ins/plug-ins-for-adobe/aac-encoder-fmle.html)</span></span>

## <a name="prerequisites"></a><span data-ttu-id="63003-116">必要條件</span><span class="sxs-lookup"><span data-stu-id="63003-116">Prerequisites</span></span>
* [<span data-ttu-id="63003-117">建立 Azure 媒體服務帳戶</span><span class="sxs-lookup"><span data-stu-id="63003-117">Create an Azure Media Services account</span></span>](media-services-portal-create-account.md)
* <span data-ttu-id="63003-118">確定有執行中的「串流端點」。</span><span class="sxs-lookup"><span data-stu-id="63003-118">Ensure there is a Streaming Endpoint running.</span></span> <span data-ttu-id="63003-119">如需詳細資訊，請參閱 [在媒體服務帳戶中管理串流端點](media-services-portal-manage-streaming-endpoints.md)</span><span class="sxs-lookup"><span data-stu-id="63003-119">For more information, see [Manage Streaming Endpoints in a Media Services Account](media-services-portal-manage-streaming-endpoints.md)</span></span>
* <span data-ttu-id="63003-120">安裝最新版的 [AMSE](https://github.com/Azure/Azure-Media-Services-Explorer) 工具。</span><span class="sxs-lookup"><span data-stu-id="63003-120">Install the latest version of the [AMSE](https://github.com/Azure/Azure-Media-Services-Explorer) tool.</span></span>
* <span data-ttu-id="63003-121">啟動工具並連接到您的 AMS 帳戶。</span><span class="sxs-lookup"><span data-stu-id="63003-121">Launch the tool and connect to your AMS account.</span></span>

## <a name="tips"></a><span data-ttu-id="63003-122">秘訣</span><span class="sxs-lookup"><span data-stu-id="63003-122">Tips</span></span>
* <span data-ttu-id="63003-123">請盡可能使用實體的有線網際網路連線。</span><span class="sxs-lookup"><span data-stu-id="63003-123">Whenever possible, use a hardwired internet connection.</span></span>
* <span data-ttu-id="63003-124">判斷頻寬需求的一項法則是將串流位元速率加倍。</span><span class="sxs-lookup"><span data-stu-id="63003-124">A good rule of thumb when determining bandwidth requirements is to double the streaming bitrates.</span></span> <span data-ttu-id="63003-125">雖然這不是強制性需求，卻有助於減輕網路阻塞的影響。</span><span class="sxs-lookup"><span data-stu-id="63003-125">While this is not a mandatory requirement, it will help mitigate the impact of network congestion.</span></span>
* <span data-ttu-id="63003-126">使用軟體型編碼器時，請關閉任何不必要的程式。</span><span class="sxs-lookup"><span data-stu-id="63003-126">When using software based encoders, close out any unnecessary programs.</span></span>

## <a name="create-a-channel"></a><span data-ttu-id="63003-127">建立通道</span><span class="sxs-lookup"><span data-stu-id="63003-127">Create a channel</span></span>
1. <span data-ttu-id="63003-128">在 AMSE 工具中，瀏覽至 [Live]  索引標籤，然後在通道區域內按一下滑鼠右鍵。</span><span class="sxs-lookup"><span data-stu-id="63003-128">In the AMSE tool, navigate to the **Live** tab, and right click within the channel area.</span></span> <span data-ttu-id="63003-129">從功能表選取 [建立通道...] </span><span class="sxs-lookup"><span data-stu-id="63003-129">Select **Create channel…**</span></span> <span data-ttu-id="63003-130">。</span><span class="sxs-lookup"><span data-stu-id="63003-130">from the menu.</span></span>

    ![FMLE](./media/media-services-fmle-live-encoder/media-services-fmle1.png)

2. <span data-ttu-id="63003-132">指定通道名稱，描述欄位為選填。</span><span class="sxs-lookup"><span data-stu-id="63003-132">Specify a channel name, the description field is optional.</span></span> <span data-ttu-id="63003-133">在 [頻道設定] 下方，針對 [即時編碼] 選項選取 [標準]，並將 [輸入通訊協定] 設定為 [RTMP]。</span><span class="sxs-lookup"><span data-stu-id="63003-133">Under Channel Settings, select **Standard** for the Live Encoding option, with the Input Protocol set to **RTMP**.</span></span> <span data-ttu-id="63003-134">您可以將所有其他設定保留現狀。</span><span class="sxs-lookup"><span data-stu-id="63003-134">You can leave all other settings as is.</span></span>

    <span data-ttu-id="63003-135">請確認已選取 [ **立即啟動新頻道** ]。</span><span class="sxs-lookup"><span data-stu-id="63003-135">Make sure the **Start the new channel now** is selected.</span></span>

3. <span data-ttu-id="63003-136">按一下 [ **建立頻道**]。</span><span class="sxs-lookup"><span data-stu-id="63003-136">Click **Create Channel**.</span></span>

   ![FMLE](./media/media-services-fmle-live-encoder/media-services-fmle2.png)

> [!NOTE]
> <span data-ttu-id="63003-138">通道約需 20 分鐘的時間即可啟動。</span><span class="sxs-lookup"><span data-stu-id="63003-138">The channel can take as long as 20 minutes to start.</span></span>
>
>

<span data-ttu-id="63003-139">當頻道啟動時，您可以 [設定編碼器](media-services-configure-fmle-live-encoder.md#configure_fmle_rtmp)。</span><span class="sxs-lookup"><span data-stu-id="63003-139">While the channel is starting you can [configure the encoder](media-services-configure-fmle-live-encoder.md#configure_fmle_rtmp).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="63003-140">請注意，只要通道進入就緒狀態，就會開始計費。</span><span class="sxs-lookup"><span data-stu-id="63003-140">Note that billing starts as soon as Channel goes into a ready state.</span></span> <span data-ttu-id="63003-141">如需詳細資訊，請參閱 [頻道的狀態](media-services-manage-live-encoder-enabled-channels.md#states)。</span><span class="sxs-lookup"><span data-stu-id="63003-141">For more information, see [Channel's states](media-services-manage-live-encoder-enabled-channels.md#states).</span></span>
>
>

## <span data-ttu-id="63003-142"><a id=configure_fmle_rtmp></a>設定 FMLE 編碼器</span><span class="sxs-lookup"><span data-stu-id="63003-142"><a id=configure_fmle_rtmp></a>Configure the FMLE encoder</span></span>
<span data-ttu-id="63003-143">在本教學課程中會使用下列輸出設定。</span><span class="sxs-lookup"><span data-stu-id="63003-143">In this tutorial the following output settings are used.</span></span> <span data-ttu-id="63003-144">本章節的其餘部分將詳細說明組態步驟。</span><span class="sxs-lookup"><span data-stu-id="63003-144">The rest of this section describes configuration steps in more detail.</span></span>

<span data-ttu-id="63003-145">**視訊**：</span><span class="sxs-lookup"><span data-stu-id="63003-145">**Video**:</span></span>

* <span data-ttu-id="63003-146">轉碼器：H.264</span><span class="sxs-lookup"><span data-stu-id="63003-146">Codec: H.264</span></span>
* <span data-ttu-id="63003-147">設定檔：高 (層級 4.0)</span><span class="sxs-lookup"><span data-stu-id="63003-147">Profile: High (Level 4.0)</span></span>
* <span data-ttu-id="63003-148">位元速率：5000 kbps</span><span class="sxs-lookup"><span data-stu-id="63003-148">Bitrate: 5000 kbps</span></span>
* <span data-ttu-id="63003-149">主要畫面格：2 秒 (60 秒)</span><span class="sxs-lookup"><span data-stu-id="63003-149">Keyframe: 2 seconds (60 seconds)</span></span>
* <span data-ttu-id="63003-150">畫面播放速率：30</span><span class="sxs-lookup"><span data-stu-id="63003-150">Frame Rate: 30</span></span>

<span data-ttu-id="63003-151">**音訊**：</span><span class="sxs-lookup"><span data-stu-id="63003-151">**Audio**:</span></span>

* <span data-ttu-id="63003-152">轉碼器：AAC (LC)</span><span class="sxs-lookup"><span data-stu-id="63003-152">Codec: AAC (LC)</span></span>
* <span data-ttu-id="63003-153">位元速率：192 kbps</span><span class="sxs-lookup"><span data-stu-id="63003-153">Bitrate: 192 kbps</span></span>
* <span data-ttu-id="63003-154">取樣速率：44.1 kHz</span><span class="sxs-lookup"><span data-stu-id="63003-154">Sample Rate: 44.1 kHz</span></span>

### <a name="configuration-steps"></a><span data-ttu-id="63003-155">組態步驟</span><span class="sxs-lookup"><span data-stu-id="63003-155">Configuration steps</span></span>
1. <span data-ttu-id="63003-156">瀏覽至所使用之機器上 Flash Media Live Encoder (FMLE) 的介面。</span><span class="sxs-lookup"><span data-stu-id="63003-156">Navigate to the Flash Media Live Encoder’s (FMLE) interface on the machine being used.</span></span>

    <span data-ttu-id="63003-157">介面是各種設定的主頁面。</span><span class="sxs-lookup"><span data-stu-id="63003-157">The interface is one main page of settings.</span></span> <span data-ttu-id="63003-158">請記下以下的建議設定，以開始透過 FMLE 使用串流。</span><span class="sxs-lookup"><span data-stu-id="63003-158">Please take note of the following recommended settings to get started with streaming using FMLE.</span></span>

   * <span data-ttu-id="63003-159">格式：H.264 畫面播放速率：30.00</span><span class="sxs-lookup"><span data-stu-id="63003-159">Format: H.264 Frame Rate: 30.00</span></span>
   * <span data-ttu-id="63003-160">輸入大小：1280 x 720</span><span class="sxs-lookup"><span data-stu-id="63003-160">Input Size: 1280 x 720</span></span>
   * <span data-ttu-id="63003-161">位元速率：5000 Kbps (可視網路限制加以調整)</span><span class="sxs-lookup"><span data-stu-id="63003-161">Bit Rate: 5000 Kbps (Can be adjusted based on network limitations)</span></span>  

     ![FMLE](./media/media-services-fmle-live-encoder/media-services-fmle3.png)

     <span data-ttu-id="63003-163">當使用交錯式來源時，請勾選 [非交錯] 選項</span><span class="sxs-lookup"><span data-stu-id="63003-163">When using interlaced sources, please checkmark the “Deinterlace” option</span></span>
2. <span data-ttu-id="63003-164">選取 [格式] 旁邊的扳手圖示，這些額外的設定應該是：</span><span class="sxs-lookup"><span data-stu-id="63003-164">Select the wrench icon next to Format, these additional settings should be:</span></span>

   * <span data-ttu-id="63003-165">設定檔：主要</span><span class="sxs-lookup"><span data-stu-id="63003-165">Profile: Main</span></span>
   * <span data-ttu-id="63003-166">層級：4.0</span><span class="sxs-lookup"><span data-stu-id="63003-166">Level: 4.0</span></span>
   * <span data-ttu-id="63003-167">主要畫面格頻率：2 秒</span><span class="sxs-lookup"><span data-stu-id="63003-167">Keyframe Frequency: 2 seconds</span></span>

     ![FMLE](./media/media-services-fmle-live-encoder/media-services-fmle4.png)
3. <span data-ttu-id="63003-169">設定下列重要的音訊設定：</span><span class="sxs-lookup"><span data-stu-id="63003-169">Set the following important audio setting:</span></span>

   * <span data-ttu-id="63003-170">格式：AAC</span><span class="sxs-lookup"><span data-stu-id="63003-170">Format: AAC</span></span>
   * <span data-ttu-id="63003-171">取樣速率：44100 Hz</span><span class="sxs-lookup"><span data-stu-id="63003-171">Sample Rate: 44100 Hz</span></span>
   * <span data-ttu-id="63003-172">位元速率：192 kbps</span><span class="sxs-lookup"><span data-stu-id="63003-172">Bitrate: 192 Kbps</span></span>

     ![FMLE](./media/media-services-fmle-live-encoder/media-services-fmle5.png)
4. <span data-ttu-id="63003-174">取得頻道的輸入 URL，以將其指派給 FMLE 的 **RTMP 端點**。</span><span class="sxs-lookup"><span data-stu-id="63003-174">Get the channel's input URL in order to assign it to the FMLE's **RTMP Endpoint**.</span></span>

    <span data-ttu-id="63003-175">瀏覽回到 AMSE 工具，並檢查通道的完成狀態。</span><span class="sxs-lookup"><span data-stu-id="63003-175">Navigate back to the AMSE tool, and check on the channel completion status.</span></span> <span data-ttu-id="63003-176">狀態從 [啟動中] 變更為 [執行中] 後，您便可取得輸入 URL。</span><span class="sxs-lookup"><span data-stu-id="63003-176">Once the State has changed from **Starting** to **Running**, you can get the input URL.</span></span>

    <span data-ttu-id="63003-177">頻道執行時，以滑鼠右鍵按一下頻道名稱，向下瀏覽讓滑鼠游標停留在 [複製輸入 URL 到剪貼簿]，然後選取 [主要輸入 URL]。</span><span class="sxs-lookup"><span data-stu-id="63003-177">When the channel is running, right click the channel name, navigate down to hover over **Copy Input URL to clipboard** and then select **Primary Input  URL**.</span></span>  

    ![fmle](./media/media-services-fmle-live-encoder/media-services-fmle6.png)
5. <span data-ttu-id="63003-179">在輸出區段裡的 [ **FMS URL** ] 欄位中貼上這項資訊，並指派串流名稱。</span><span class="sxs-lookup"><span data-stu-id="63003-179">Paste this information in the **FMS URL** field of the output section, and assign a stream name.</span></span>

    ![FMLE](./media/media-services-fmle-live-encoder/media-services-fmle7.png)

    <span data-ttu-id="63003-181">如需額外的備援，請用次要輸入 URL 重複這些步驟。</span><span class="sxs-lookup"><span data-stu-id="63003-181">For extra redundancy, repeat these steps with the Secondary Input URL.</span></span>
6. <span data-ttu-id="63003-182">選取 [ **連接**]。</span><span class="sxs-lookup"><span data-stu-id="63003-182">Select **Connect**.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="63003-183">在您按一下 [連接] 之前，**必須**先確保頻道已就緒。</span><span class="sxs-lookup"><span data-stu-id="63003-183">Before you click **Connect**, you **must** ensure that the Channel is ready.</span></span>
> <span data-ttu-id="63003-184">此外，請務必不要讓通道在沒有輸入比重摘要的情況下，處於就緒狀態超過 15 分鐘。</span><span class="sxs-lookup"><span data-stu-id="63003-184">Also, make sure not to leave the Channel in a ready state without an input contribution feed for longer than > 15 minutes.</span></span>
>
>

## <a name="test-playback"></a><span data-ttu-id="63003-185">測試播放</span><span class="sxs-lookup"><span data-stu-id="63003-185">Test playback</span></span>

<span data-ttu-id="63003-186">瀏覽至 AMSE 工具，然後以滑鼠右鍵按一下要測試的通道。</span><span class="sxs-lookup"><span data-stu-id="63003-186">Navigate to the AMSE tool, and right click the channel to be tested.</span></span> <span data-ttu-id="63003-187">在功能表中，將滑鼠游標停留在 [播放預覽]，並選取 [使用 Azure 媒體播放器]。</span><span class="sxs-lookup"><span data-stu-id="63003-187">From the menu, hover over **Playback the Preview** and select **with Azure Media Player**.</span></span>  

    ![fmle](./media/media-services-fmle-live-encoder/media-services-fmle8.png)

<span data-ttu-id="63003-188">如果播放器中出現串流，則編碼器已妥善設定為連接到 AMS。</span><span class="sxs-lookup"><span data-stu-id="63003-188">If the stream appears in the player, then the encoder has been properly configured to connect to AMS.</span></span>

<span data-ttu-id="63003-189">如果收到錯誤，則必須重設通道，且編碼器設定需要調整。</span><span class="sxs-lookup"><span data-stu-id="63003-189">If an error is received, the channel will need to be reset and encoder settings adjusted.</span></span> <span data-ttu-id="63003-190">請參閱 [疑難排解](media-services-troubleshooting-live-streaming.md) 主題中的指引。</span><span class="sxs-lookup"><span data-stu-id="63003-190">Please see the [troubleshooting](media-services-troubleshooting-live-streaming.md) topic for guidance.</span></span>  

## <a name="create-a-program"></a><span data-ttu-id="63003-191">建立程式</span><span class="sxs-lookup"><span data-stu-id="63003-191">Create a program</span></span>
1. <span data-ttu-id="63003-192">一旦確認通道播放沒問題後，請建立程式。</span><span class="sxs-lookup"><span data-stu-id="63003-192">Once channel playback is confirmed, create a program.</span></span> <span data-ttu-id="63003-193">在 AMSE 工具的 [Live] 索引標籤下，於程式區域內按一下滑鼠右鍵，並選取 [建立新的程式]。</span><span class="sxs-lookup"><span data-stu-id="63003-193">Under the **Live** tab in the AMSE tool, right click within the program area and select **Create New Program**.</span></span>  

    ![fmle](./media/media-services-fmle-live-encoder/media-services-fmle9.png)
2. <span data-ttu-id="63003-195">為程式命名，並視需要調整 **封存時間長度** (預設為 4 小時)。</span><span class="sxs-lookup"><span data-stu-id="63003-195">Name the program and, if needed, adjust the **Archive Window Length** (which defaults to 4 hours).</span></span> <span data-ttu-id="63003-196">您也可以指定儲存體位置，或保留為預設值。</span><span class="sxs-lookup"><span data-stu-id="63003-196">You can also specify a storage location or leave as the default.</span></span>  
3. <span data-ttu-id="63003-197">勾選 [現在啟動程式]  方塊。</span><span class="sxs-lookup"><span data-stu-id="63003-197">Check the **Start the Program now** box.</span></span>
4. <span data-ttu-id="63003-198">按一下 [建立程式] 。</span><span class="sxs-lookup"><span data-stu-id="63003-198">Click **Create Program**.</span></span>  

    >[!NOTE]
    ><span data-ttu-id="63003-199">建立程式時所使用的時間會比建立通道時少。</span><span class="sxs-lookup"><span data-stu-id="63003-199">Program creation takes less time than channel creation.</span></span>
        
5. <span data-ttu-id="63003-200">一旦程式開始執行，請在程式上按一下滑鼠右鍵，並瀏覽至 [播放程式]，然後選取 [使用 Azure 媒體播放器] 確認播放。</span><span class="sxs-lookup"><span data-stu-id="63003-200">Once the program is running, confirm playback by right clicking the program and navigating to **Playback the program(s)** and then selecting **with Azure Media Player**.</span></span>  
6. <span data-ttu-id="63003-201">一經確認後，再次於該程式上按一下滑鼠右鍵，並選取 [複製輸出 URL 到剪貼簿] \(或從 [程式資訊和設定] 功能表選項擷取這項資訊)。</span><span class="sxs-lookup"><span data-stu-id="63003-201">Once confirmed, right click the program again and select **Copy the Output URL to Clipboard** (or retrieve this information from the **Program information and settings** option from the menu).</span></span>

<span data-ttu-id="63003-202">串流現在已經可以內嵌於播放程式中，或散發給某個對象，以供即時檢視。</span><span class="sxs-lookup"><span data-stu-id="63003-202">The stream is now ready to be embedded in a player, or distributed to an audience for live viewing.</span></span>  

## <a name="troubleshooting"></a><span data-ttu-id="63003-203">疑難排解</span><span class="sxs-lookup"><span data-stu-id="63003-203">Troubleshooting</span></span>
<span data-ttu-id="63003-204">請參閱 [疑難排解](media-services-troubleshooting-live-streaming.md) 主題中的指引。</span><span class="sxs-lookup"><span data-stu-id="63003-204">Please see the [troubleshooting](media-services-troubleshooting-live-streaming.md) topic for guidance.</span></span>

## <a name="media-services-learning-paths"></a><span data-ttu-id="63003-205">媒體服務學習路徑</span><span class="sxs-lookup"><span data-stu-id="63003-205">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="63003-206">提供意見反應</span><span class="sxs-lookup"><span data-stu-id="63003-206">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]
