---
title: "設定 Telestream Wirecast 編碼器來傳送單一位元速率的即時串流 | Microsoft Docs"
description: "本主題示範如何設定 Wirecast 即時編碼器，藉此將單一位元速率的即時串流傳送到已啟用即時編碼的 AMS 通道。 "
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: 0d2f1e81-51a6-4ca9-894a-6dfa51ce4c70
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: ne
ms.topic: article
ms.date: 01/05/2017
ms.author: juliako;cenkdin;anilmur
ms.openlocfilehash: c4df14f24650ce431dfb31cc774cab6d3cf3aef0
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="use-the-wirecast-encoder-to-send-a-single-bitrate-live-stream"></a><span data-ttu-id="8fc98-103">使用 Wirecast 編碼器來傳送單一位元速率的即時串流</span><span class="sxs-lookup"><span data-stu-id="8fc98-103">Use the Wirecast encoder to send a single bitrate live stream</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="8fc98-104">Wirecast</span><span class="sxs-lookup"><span data-stu-id="8fc98-104">Wirecast</span></span>](media-services-configure-wirecast-live-encoder.md)
> * [<span data-ttu-id="8fc98-105">Elemental Live</span><span class="sxs-lookup"><span data-stu-id="8fc98-105">Elemental Live</span></span>](media-services-configure-elemental-live-encoder.md)
> * [<span data-ttu-id="8fc98-106">Tricaster</span><span class="sxs-lookup"><span data-stu-id="8fc98-106">Tricaster</span></span>](media-services-configure-tricaster-live-encoder.md)
> * [<span data-ttu-id="8fc98-107">FMLE</span><span class="sxs-lookup"><span data-stu-id="8fc98-107">FMLE</span></span>](media-services-configure-fmle-live-encoder.md)
>
>

<span data-ttu-id="8fc98-108">本主題示範如何設定 [Telestream Wirecast](http://www.telestream.net/wirecast/overview.htm) 即時編碼器，藉此將單一位元速率的即時串流傳送到已啟用即時編碼的 AMS 通道。</span><span class="sxs-lookup"><span data-stu-id="8fc98-108">This topic shows how to configure the [Telestream Wirecast](http://www.telestream.net/wirecast/overview.htm) live encoder to send a single bitrate stream to AMS channels that are enabled for live encoding.</span></span>  <span data-ttu-id="8fc98-109">如需詳細資訊，請參閱 [使用啟用的通道來以 Azure 媒體服務執行即時編碼](media-services-manage-live-encoder-enabled-channels.md)。</span><span class="sxs-lookup"><span data-stu-id="8fc98-109">For more information, see [Working with Channels that are Enabled to Perform Live Encoding with Azure Media Services](media-services-manage-live-encoder-enabled-channels.md).</span></span>

<span data-ttu-id="8fc98-110">本教學課程示範如何使用 Azure 媒體服務總管 (AMSE) 工具管理 Azure 媒體服務 (AMS)。</span><span class="sxs-lookup"><span data-stu-id="8fc98-110">This tutorial shows how to manage Azure Media Services (AMS) with Azure Media Services Explorer (AMSE) tool.</span></span> <span data-ttu-id="8fc98-111">此工具只會在 Windows 電腦上執行。</span><span class="sxs-lookup"><span data-stu-id="8fc98-111">This tool only runs on Windows PC.</span></span> <span data-ttu-id="8fc98-112">如果您是用 Mac 或 Linux，請使用 Azure 入口網站建立[通道](media-services-portal-creating-live-encoder-enabled-channel.md#create-a-channel)和[程式](media-services-portal-creating-live-encoder-enabled-channel.md)。</span><span class="sxs-lookup"><span data-stu-id="8fc98-112">If you are on Mac or Linux, use the Azure portal to create [channels](media-services-portal-creating-live-encoder-enabled-channel.md#create-a-channel) and [programs](media-services-portal-creating-live-encoder-enabled-channel.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="8fc98-113">必要條件</span><span class="sxs-lookup"><span data-stu-id="8fc98-113">Prerequisites</span></span>
* [<span data-ttu-id="8fc98-114">建立 Azure 媒體服務帳戶</span><span class="sxs-lookup"><span data-stu-id="8fc98-114">Create an Azure Media Services account</span></span>](media-services-portal-create-account.md)
* <span data-ttu-id="8fc98-115">確定有執行中的「串流端點」。</span><span class="sxs-lookup"><span data-stu-id="8fc98-115">Ensure there is a Streaming Endpoint running.</span></span> <span data-ttu-id="8fc98-116">如需詳細資訊，請參閱 [在媒體服務帳戶中管理串流端點](media-services-portal-manage-streaming-endpoints.md)</span><span class="sxs-lookup"><span data-stu-id="8fc98-116">For more information, see [Manage Streaming Endpoints in a Media Services Account](media-services-portal-manage-streaming-endpoints.md)</span></span>
* <span data-ttu-id="8fc98-117">安裝最新版的 [AMSE](https://github.com/Azure/Azure-Media-Services-Explorer) 工具。</span><span class="sxs-lookup"><span data-stu-id="8fc98-117">Install the latest version of the [AMSE](https://github.com/Azure/Azure-Media-Services-Explorer) tool.</span></span>
* <span data-ttu-id="8fc98-118">啟動工具並連接到您的 AMS 帳戶。</span><span class="sxs-lookup"><span data-stu-id="8fc98-118">Launch the tool and connect to your AMS account.</span></span>

## <a name="tips"></a><span data-ttu-id="8fc98-119">秘訣</span><span class="sxs-lookup"><span data-stu-id="8fc98-119">Tips</span></span>
* <span data-ttu-id="8fc98-120">請盡可能使用實體的有線網際網路連線。</span><span class="sxs-lookup"><span data-stu-id="8fc98-120">Whenever possible, use a hardwired internet connection.</span></span>
* <span data-ttu-id="8fc98-121">判斷頻寬需求的一項法則是將串流位元速率加倍。</span><span class="sxs-lookup"><span data-stu-id="8fc98-121">A good rule of thumb when determining bandwidth requirements is to double the streaming bitrates.</span></span> <span data-ttu-id="8fc98-122">雖然這不是強制性需求，卻有助於減輕網路阻塞的影響。</span><span class="sxs-lookup"><span data-stu-id="8fc98-122">While this is not a mandatory requirement, it will help mitigate the impact of network congestion.</span></span>
* <span data-ttu-id="8fc98-123">使用軟體型編碼器時，請關閉任何不必要的程式。</span><span class="sxs-lookup"><span data-stu-id="8fc98-123">When using software based encoders, close out any unnecessary programs.</span></span>

## <a name="create-a-channel"></a><span data-ttu-id="8fc98-124">建立通道</span><span class="sxs-lookup"><span data-stu-id="8fc98-124">Create a channel</span></span>
1. <span data-ttu-id="8fc98-125">在 AMSE 工具中，瀏覽至 [Live]  索引標籤，然後在通道區域內按一下滑鼠右鍵。</span><span class="sxs-lookup"><span data-stu-id="8fc98-125">In the AMSE tool, navigate to the **Live** tab, and right click within the channel area.</span></span> <span data-ttu-id="8fc98-126">從功能表選取 [建立通道...] </span><span class="sxs-lookup"><span data-stu-id="8fc98-126">Select **Create channel…**</span></span> <span data-ttu-id="8fc98-127">。</span><span class="sxs-lookup"><span data-stu-id="8fc98-127">from the menu.</span></span>

    ![Wirecast](./media/media-services-wirecast-live-encoder/media-services-wirecast1.png)

2. <span data-ttu-id="8fc98-129">指定通道名稱，描述欄位為選填。</span><span class="sxs-lookup"><span data-stu-id="8fc98-129">Specify a channel name, the description field is optional.</span></span> <span data-ttu-id="8fc98-130">在 [頻道設定] 下方，針對 [即時編碼] 選項選取 [標準]，並將 [輸入通訊協定] 設定為 [RTMP]。</span><span class="sxs-lookup"><span data-stu-id="8fc98-130">Under Channel Settings, select **Standard** for the Live Encoding option, with the Input Protocol set to **RTMP**.</span></span> <span data-ttu-id="8fc98-131">您可以將所有其他設定保留現狀。</span><span class="sxs-lookup"><span data-stu-id="8fc98-131">You can leave all other settings as is.</span></span>

    <span data-ttu-id="8fc98-132">請確認已選取 [ **立即啟動新頻道** ]。</span><span class="sxs-lookup"><span data-stu-id="8fc98-132">Make sure the **Start the new channel now** is selected.</span></span>

3. <span data-ttu-id="8fc98-133">按一下 [ **建立頻道**]。</span><span class="sxs-lookup"><span data-stu-id="8fc98-133">Click **Create Channel**.</span></span>

   ![Wirecast](./media/media-services-wirecast-live-encoder/media-services-wirecast2.png)

> [!NOTE]
> <span data-ttu-id="8fc98-135">通道約需 20 分鐘的時間即可啟動。</span><span class="sxs-lookup"><span data-stu-id="8fc98-135">The channel can take as long as 20 minutes to start.</span></span>
>
>

<span data-ttu-id="8fc98-136">當頻道啟動時，您可以 [設定編碼器](media-services-configure-wirecast-live-encoder.md#configure_wirecast_rtmp)。</span><span class="sxs-lookup"><span data-stu-id="8fc98-136">While the channel is starting you can [configure the encoder](media-services-configure-wirecast-live-encoder.md#configure_wirecast_rtmp).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="8fc98-137">請注意，只要通道進入就緒狀態，就會開始計費。</span><span class="sxs-lookup"><span data-stu-id="8fc98-137">Note that billing starts as soon as Channel goes into a ready state.</span></span> <span data-ttu-id="8fc98-138">如需詳細資訊，請參閱 [通道的狀態](media-services-manage-live-encoder-enabled-channels.md#states)。</span><span class="sxs-lookup"><span data-stu-id="8fc98-138">For more information, see [Channel's states](media-services-manage-live-encoder-enabled-channels.md#states).</span></span>
>
>

## <span data-ttu-id="8fc98-139"><a id=configure_wirecast_rtmp></a>設定 Telestream Wirecast 編碼器</span><span class="sxs-lookup"><span data-stu-id="8fc98-139"><a id=configure_wirecast_rtmp></a>Configure the Telestream Wirecast encoder</span></span>
<span data-ttu-id="8fc98-140">在本教學課程中，我們會使用下列輸出設定。</span><span class="sxs-lookup"><span data-stu-id="8fc98-140">In this tutorial the following output settings are used.</span></span> <span data-ttu-id="8fc98-141">本章節的其餘部分將詳細說明組態步驟。</span><span class="sxs-lookup"><span data-stu-id="8fc98-141">The rest of this section describes configuration steps in more detail.</span></span>

<span data-ttu-id="8fc98-142">**視訊**：</span><span class="sxs-lookup"><span data-stu-id="8fc98-142">**Video**:</span></span>

* <span data-ttu-id="8fc98-143">轉碼器：H.264</span><span class="sxs-lookup"><span data-stu-id="8fc98-143">Codec: H.264</span></span>
* <span data-ttu-id="8fc98-144">設定檔：高 (層級 4.0)</span><span class="sxs-lookup"><span data-stu-id="8fc98-144">Profile: High (Level 4.0)</span></span>
* <span data-ttu-id="8fc98-145">位元速率：5000 kbps</span><span class="sxs-lookup"><span data-stu-id="8fc98-145">Bitrate: 5000 kbps</span></span>
* <span data-ttu-id="8fc98-146">主要畫面格：2 秒 (60 秒)</span><span class="sxs-lookup"><span data-stu-id="8fc98-146">Keyframe: 2 seconds (60 seconds)</span></span>
* <span data-ttu-id="8fc98-147">畫面播放速率：30</span><span class="sxs-lookup"><span data-stu-id="8fc98-147">Frame Rate: 30</span></span>

<span data-ttu-id="8fc98-148">**音訊**：</span><span class="sxs-lookup"><span data-stu-id="8fc98-148">**Audio**:</span></span>

* <span data-ttu-id="8fc98-149">轉碼器：AAC (LC)</span><span class="sxs-lookup"><span data-stu-id="8fc98-149">Codec: AAC (LC)</span></span>
* <span data-ttu-id="8fc98-150">位元速率：192 kbps</span><span class="sxs-lookup"><span data-stu-id="8fc98-150">Bitrate: 192 kbps</span></span>
* <span data-ttu-id="8fc98-151">取樣速率：44.1 kHz</span><span class="sxs-lookup"><span data-stu-id="8fc98-151">Sample Rate: 44.1 kHz</span></span>

### <a name="configuration-steps"></a><span data-ttu-id="8fc98-152">組態步驟</span><span class="sxs-lookup"><span data-stu-id="8fc98-152">Configuration steps</span></span>
1. <span data-ttu-id="8fc98-153">在使用的機器上開啟 Telestream Wirecast 應用程式，並設定 RTMP 串流。</span><span class="sxs-lookup"><span data-stu-id="8fc98-153">Open the Telestream Wirecast application on the machine being used, and set up for RTMP streaming.</span></span>
2. <span data-ttu-id="8fc98-154">瀏覽至 [輸出] 索引標籤，並選取 [輸出設定...] 以設定輸出。</span><span class="sxs-lookup"><span data-stu-id="8fc98-154">Configure the output by navigating to the **Output** tab and selecting **Output Settings…**.</span></span>

    <span data-ttu-id="8fc98-155">請確定 [輸出目的地] 已設為 [RTMP Server]。</span><span class="sxs-lookup"><span data-stu-id="8fc98-155">Make sure the **Output Destination** is set to **RTMP Server**.</span></span>
3. <span data-ttu-id="8fc98-156">按一下 [確定] 。</span><span class="sxs-lookup"><span data-stu-id="8fc98-156">Click **OK**.</span></span>
4. <span data-ttu-id="8fc98-157">在 [設定] 頁面上，將 [目的地] 欄位設為 [Azure 媒體服務]。</span><span class="sxs-lookup"><span data-stu-id="8fc98-157">On the settings page, set the **Destination** field to be **Azure Media Services**.</span></span>

    <span data-ttu-id="8fc98-158">編碼設定檔已預先選取為 [Azure H.264 720p 16:9 (1280x720)] 。</span><span class="sxs-lookup"><span data-stu-id="8fc98-158">The Encoding profile is pre-selected to **Azure H.264 720p 16:9 (1280x720)**.</span></span> <span data-ttu-id="8fc98-159">若要自訂這些設定，請選取下拉式清單右邊的齒輪圖示，然後選擇 [新增預設] 。</span><span class="sxs-lookup"><span data-stu-id="8fc98-159">To customize these settings, select the gear icon to the right of the drop down, and then choose **New Preset**.</span></span>

    ![Wirecast](./media/media-services-wirecast-live-encoder/media-services-wirecast3.png)
5. <span data-ttu-id="8fc98-161">設定編碼器預設。</span><span class="sxs-lookup"><span data-stu-id="8fc98-161">Configure encoder presets.</span></span>

    <span data-ttu-id="8fc98-162">為預設命名，並檢查下列建議的設定：</span><span class="sxs-lookup"><span data-stu-id="8fc98-162">Name the preset, and check for the following recommended settings:</span></span>

    <span data-ttu-id="8fc98-163">**影片**</span><span class="sxs-lookup"><span data-stu-id="8fc98-163">**Video**</span></span>

   * <span data-ttu-id="8fc98-164">編碼器：MainConcept H.264</span><span class="sxs-lookup"><span data-stu-id="8fc98-164">Encoder: MainConcept H.264</span></span>
   * <span data-ttu-id="8fc98-165">每秒畫面格數：30</span><span class="sxs-lookup"><span data-stu-id="8fc98-165">Frames per Second: 30</span></span>
   * <span data-ttu-id="8fc98-166">平均位元速率：5000 kbit/秒 (可視網路限制加以調整)</span><span class="sxs-lookup"><span data-stu-id="8fc98-166">Average bit rate: 5000 kbits/sec (Can be adjusted based on network limitations)</span></span>
   * <span data-ttu-id="8fc98-167">設定檔：主要</span><span class="sxs-lookup"><span data-stu-id="8fc98-167">Profile: Main</span></span>
   * <span data-ttu-id="8fc98-168">畫面間隔：60 個畫面</span><span class="sxs-lookup"><span data-stu-id="8fc98-168">Key frame every: 60 frames</span></span>

    <span data-ttu-id="8fc98-169">**音訊**</span><span class="sxs-lookup"><span data-stu-id="8fc98-169">**Audio**</span></span>

   * <span data-ttu-id="8fc98-170">目標位元速率：192 kbit/秒</span><span class="sxs-lookup"><span data-stu-id="8fc98-170">Target bit rate: 192 kbits/sec</span></span>
   * <span data-ttu-id="8fc98-171">取樣速率：44.100 kHz</span><span class="sxs-lookup"><span data-stu-id="8fc98-171">Sample Rate: 44.100 kHz</span></span>

     ![Wirecast](./media/media-services-wirecast-live-encoder/media-services-wirecast4.png)
6. <span data-ttu-id="8fc98-173">按下 [儲存] 。</span><span class="sxs-lookup"><span data-stu-id="8fc98-173">Press **Save**.</span></span>

    <span data-ttu-id="8fc98-174">[編碼] 欄位現在會有可供選取的新建立設定檔。</span><span class="sxs-lookup"><span data-stu-id="8fc98-174">The Encoding field now has the newly created profile available for selection.</span></span>

    <span data-ttu-id="8fc98-175">請確定已選取新的設定檔。</span><span class="sxs-lookup"><span data-stu-id="8fc98-175">Make sure the new profile is selected.</span></span>
7. <span data-ttu-id="8fc98-176">取得通道的輸入 URL，才能將它指派給 Wirecast 的 **RTMP 端點**。</span><span class="sxs-lookup"><span data-stu-id="8fc98-176">Get the channel's input URL in order to assign it to the Wirecast **RTMP Endpoint**.</span></span>

    <span data-ttu-id="8fc98-177">瀏覽回到 AMSE 工具，並檢查通道的完成狀態。</span><span class="sxs-lookup"><span data-stu-id="8fc98-177">Navigate back to the AMSE tool, and check on the channel completion status.</span></span> <span data-ttu-id="8fc98-178">狀態從 [啟動中] 變更為 [執行中] 後，您便可取得輸入 URL。</span><span class="sxs-lookup"><span data-stu-id="8fc98-178">Once the State has changed from **Starting** to **Running**, you can get the input URL.</span></span>

    <span data-ttu-id="8fc98-179">頻道執行時，以滑鼠右鍵按一下頻道名稱，向下瀏覽讓滑鼠游標停留在 [複製輸入 URL 到剪貼簿]，然後選取 [主要輸入 URL]。</span><span class="sxs-lookup"><span data-stu-id="8fc98-179">When the channel is running, right click the channel name, navigate down to hover over **Copy Input URL to clipboard** and then select **Primary Input  URL**.</span></span>  

    ![Wirecast](./media/media-services-wirecast-live-encoder/media-services-wirecast6.png)
8. <span data-ttu-id="8fc98-181">在 Wirecast [輸出設定] 視窗中，於輸出區段的 [位址] 欄位中貼上這項資訊，並指派串流名稱。</span><span class="sxs-lookup"><span data-stu-id="8fc98-181">In the Wirecast **Output Settings** window, paste this information in the **Address** field of the output section, and assign a stream name.</span></span>

    ![Wirecast](./media/media-services-wirecast-live-encoder/media-services-wirecast5.png)

1. <span data-ttu-id="8fc98-183">選取 [確定] 。</span><span class="sxs-lookup"><span data-stu-id="8fc98-183">Select **OK**.</span></span>
2. <span data-ttu-id="8fc98-184">在 **Wirecast** 主畫面上，確認視訊和音訊的輸入來源已就緒，然後按下左上角的 [資料流]。</span><span class="sxs-lookup"><span data-stu-id="8fc98-184">On the main **Wirecast** screen, confirm input sources for video and audio are ready and then hit **Stream** in the top left hand corner.</span></span>

   ![Wirecast](./media/media-services-wirecast-live-encoder/media-services-wirecast7.png)

> [!IMPORTANT]
> <span data-ttu-id="8fc98-186">在您按一下 [資料流] 之前，**必須**確保通道已就緒。</span><span class="sxs-lookup"><span data-stu-id="8fc98-186">Before you click **Stream**, you **must** ensure that the Channel is ready.</span></span>
> <span data-ttu-id="8fc98-187">此外，請務必不要讓通道在沒有輸入比重摘要的情況下，處於就緒狀態超過 15 分鐘。</span><span class="sxs-lookup"><span data-stu-id="8fc98-187">Also, make sure not to leave the Channel in a ready state without an input contribution feed for longer than > 15 minutes.</span></span>
>
>

## <a name="test-playback"></a><span data-ttu-id="8fc98-188">測試播放</span><span class="sxs-lookup"><span data-stu-id="8fc98-188">Test playback</span></span>

<span data-ttu-id="8fc98-189">瀏覽至 AMSE 工具，然後以滑鼠右鍵按一下要測試的通道。</span><span class="sxs-lookup"><span data-stu-id="8fc98-189">Navigate to the AMSE tool, and right click the channel to be tested.</span></span> <span data-ttu-id="8fc98-190">在功能表中，將滑鼠游標停留在 [播放預覽]，並選取 [使用 Azure 媒體播放器]。</span><span class="sxs-lookup"><span data-stu-id="8fc98-190">From the menu, hover over **Playback the Preview** and select **with Azure Media Player**.</span></span>  

    ![wirecast](./media/media-services-wirecast-live-encoder/media-services-wirecast8.png)

<span data-ttu-id="8fc98-191">如果播放器中出現串流，則編碼器已妥善設定為連接到 AMS。</span><span class="sxs-lookup"><span data-stu-id="8fc98-191">If the stream appears in the player, then the encoder has been properly configured to connect to AMS.</span></span>

<span data-ttu-id="8fc98-192">如果收到錯誤，則必須重設通道，且編碼器設定需要調整。</span><span class="sxs-lookup"><span data-stu-id="8fc98-192">If an error is received, the channel will need to be reset and encoder settings adjusted.</span></span> <span data-ttu-id="8fc98-193">請參閱 [疑難排解](media-services-troubleshooting-live-streaming.md) 主題中的指引。</span><span class="sxs-lookup"><span data-stu-id="8fc98-193">Please see the [troubleshooting](media-services-troubleshooting-live-streaming.md) topic for guidance.</span></span>  

## <a name="create-a-program"></a><span data-ttu-id="8fc98-194">建立程式</span><span class="sxs-lookup"><span data-stu-id="8fc98-194">Create a program</span></span>
1. <span data-ttu-id="8fc98-195">一旦確認通道播放沒問題後，請建立程式。</span><span class="sxs-lookup"><span data-stu-id="8fc98-195">Once channel playback is confirmed, create a program.</span></span> <span data-ttu-id="8fc98-196">在 AMSE 工具的 [Live] 索引標籤下，於程式區域內按一下滑鼠右鍵，並選取 [建立新的程式]。</span><span class="sxs-lookup"><span data-stu-id="8fc98-196">Under the **Live** tab in the AMSE tool, right click within the program area and select **Create New Program**.</span></span>  

    ![Wirecast](./media/media-services-wirecast-live-encoder/media-services-wirecast9.png)
2. <span data-ttu-id="8fc98-198">為程式命名，並視需要調整 **封存時間長度** (預設為 4 小時)。</span><span class="sxs-lookup"><span data-stu-id="8fc98-198">Name the program and, if needed, adjust the **Archive Window Length** (which defaults to 4 hours).</span></span> <span data-ttu-id="8fc98-199">您也可以指定儲存體位置，或保留為預設值。</span><span class="sxs-lookup"><span data-stu-id="8fc98-199">You can also specify a storage location or leave as the default.</span></span>  
3. <span data-ttu-id="8fc98-200">勾選 [現在啟動程式]  方塊。</span><span class="sxs-lookup"><span data-stu-id="8fc98-200">Check the **Start the Program now** box.</span></span>
4. <span data-ttu-id="8fc98-201">按一下 [建立程式] 。</span><span class="sxs-lookup"><span data-stu-id="8fc98-201">Click **Create Program**.</span></span>  

   >[!NOTE]
   ><span data-ttu-id="8fc98-202">建立程式時所使用的時間會比建立通道時少。</span><span class="sxs-lookup"><span data-stu-id="8fc98-202">Program creation takes less time than channel creation.</span></span>
       
5. <span data-ttu-id="8fc98-203">一旦程式開始執行，請在程式上按一下滑鼠右鍵，並瀏覽至 [播放程式]，然後選取 [使用 Azure 媒體播放器] 確認播放。</span><span class="sxs-lookup"><span data-stu-id="8fc98-203">Once the program is running, confirm playback by right clicking the program and navigating to **Playback the program(s)** and then selecting **with Azure Media Player**.</span></span>  
6. <span data-ttu-id="8fc98-204">一經確認後，再次於該程式上按一下滑鼠右鍵，並選取 [複製輸出 URL 到剪貼簿] \(或從 [程式資訊和設定] 功能表選項擷取這項資訊)。</span><span class="sxs-lookup"><span data-stu-id="8fc98-204">Once confirmed, right click the program again and select **Copy the Output URL to Clipboard** (or retrieve this information from the **Program information and settings** option from the menu).</span></span>

<span data-ttu-id="8fc98-205">串流現在已經可以內嵌於播放程式中，或散發給某個對象，以供即時檢視。</span><span class="sxs-lookup"><span data-stu-id="8fc98-205">The stream is now ready to be embedded in a player, or distributed to an audience for live viewing.</span></span>  

## <a name="troubleshooting"></a><span data-ttu-id="8fc98-206">疑難排解</span><span class="sxs-lookup"><span data-stu-id="8fc98-206">Troubleshooting</span></span>
<span data-ttu-id="8fc98-207">請參閱 [疑難排解](media-services-troubleshooting-live-streaming.md) 主題中的指引。</span><span class="sxs-lookup"><span data-stu-id="8fc98-207">Please see the [troubleshooting](media-services-troubleshooting-live-streaming.md) topic for guidance.</span></span>

## <a name="media-services-learning-paths"></a><span data-ttu-id="8fc98-208">媒體服務學習路徑</span><span class="sxs-lookup"><span data-stu-id="8fc98-208">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="8fc98-209">提供意見反應</span><span class="sxs-lookup"><span data-stu-id="8fc98-209">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]
