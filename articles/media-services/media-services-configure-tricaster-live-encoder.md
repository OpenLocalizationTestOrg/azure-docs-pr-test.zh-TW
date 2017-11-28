---
title: "設定 NewTek TriCaster 編碼器來傳送單一位元速率的即時串流 | Microsoft Docs"
description: "本主題示範如何設定 Tricaster 即時編碼器，藉此將單一位元速率的串流傳送到已啟用即時編碼的 AMS 通道。"
services: media-services
documentationcenter: 
author: cenkdin
manager: cfowler
editor: 
ms.assetid: 8973181a-3059-471a-a6bb-ccda7d3ff297
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: ne
ms.topic: article
ms.date: 01/05/2017
ms.author: juliako;cenkd;anilmur
ms.openlocfilehash: 42b012fb98bd0504c931ce391d63aecca8c3d311
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="use-the-newtek-tricaster-encoder-to-send-a-single-bitrate-live-stream"></a><span data-ttu-id="618dc-103">使用 NewTek TriCaster 編碼器來傳送單一位元速率的即時串流</span><span class="sxs-lookup"><span data-stu-id="618dc-103">Use the NewTek TriCaster encoder to send a single bitrate live stream</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="618dc-104">Tricaster</span><span class="sxs-lookup"><span data-stu-id="618dc-104">Tricaster</span></span>](media-services-configure-tricaster-live-encoder.md)
> * [<span data-ttu-id="618dc-105">Elemental Live</span><span class="sxs-lookup"><span data-stu-id="618dc-105">Elemental Live</span></span>](media-services-configure-elemental-live-encoder.md)
> * [<span data-ttu-id="618dc-106">Wirecast</span><span class="sxs-lookup"><span data-stu-id="618dc-106">Wirecast</span></span>](media-services-configure-wirecast-live-encoder.md)
> * [<span data-ttu-id="618dc-107">FMLE</span><span class="sxs-lookup"><span data-stu-id="618dc-107">FMLE</span></span>](media-services-configure-fmle-live-encoder.md)
>
>

<span data-ttu-id="618dc-108">本主題示範如何設定 [NewTek TriCaster](http://newtek.com/products/tricaster-40.html) 即時編碼器，藉此將單一位元速率的即時串流傳送到已啟用即時編碼的 AMS 通道。</span><span class="sxs-lookup"><span data-stu-id="618dc-108">This topic shows how to configure the [NewTek TriCaster](http://newtek.com/products/tricaster-40.html) live encoder to send a single bitrate stream to AMS channels that are enabled for live encoding.</span></span> <span data-ttu-id="618dc-109">如需詳細資訊，請參閱 [使用啟用的通道以 Azure 媒體服務執行即時編碼](media-services-manage-live-encoder-enabled-channels.md)。</span><span class="sxs-lookup"><span data-stu-id="618dc-109">For more information, see [Working with Channels that are Enabled to Perform Live Encoding with Azure Media Services](media-services-manage-live-encoder-enabled-channels.md).</span></span>

<span data-ttu-id="618dc-110">本教學課程示範如何使用 Azure 媒體服務總管 (AMSE) 工具管理 Azure 媒體服務 (AMS)。</span><span class="sxs-lookup"><span data-stu-id="618dc-110">This tutorial shows how to manage Azure Media Services (AMS) with Azure Media Services Explorer (AMSE) tool.</span></span> <span data-ttu-id="618dc-111">此工具只會在 Windows 電腦上執行。</span><span class="sxs-lookup"><span data-stu-id="618dc-111">This tool only runs on Windows PC.</span></span> <span data-ttu-id="618dc-112">如果您是用 Mac 或 Linux，請使用 Azure 入口網站建立[通道](media-services-portal-creating-live-encoder-enabled-channel.md#create-a-channel)和[程式](media-services-portal-creating-live-encoder-enabled-channel.md)。</span><span class="sxs-lookup"><span data-stu-id="618dc-112">If you are on Mac or Linux, use the Azure portal to create [channels](media-services-portal-creating-live-encoder-enabled-channel.md#create-a-channel) and [programs](media-services-portal-creating-live-encoder-enabled-channel.md).</span></span>

> [!NOTE]
> <span data-ttu-id="618dc-113">使用 Tricaster 將分佈摘要傳送到針對即時編碼啟用的 AMS 通道時，如果您使用 Tricaster 的某些功能 (例如，在摘要之間快速切割或切換靜態圖像)，您的即時事件可能會出現視訊/音訊干擾。</span><span class="sxs-lookup"><span data-stu-id="618dc-113">When using Tricaster for sending in a contribution feed to AMS channels that are enabled for live encoding, there can be video/audio glitches in your live event if you use certain features of Tricaster, such as rapid cutting between feeds, or switching to/from slates.</span></span> <span data-ttu-id="618dc-114">AMS 小組正著手於修正這些問題，在解決之前，不建議使用這些功能。</span><span class="sxs-lookup"><span data-stu-id="618dc-114">The AMS team is working on fixing these issues, until then, it is not recommend to use these features.</span></span>
>
>

## <a name="prerequisites"></a><span data-ttu-id="618dc-115">必要條件</span><span class="sxs-lookup"><span data-stu-id="618dc-115">Prerequisites</span></span>
* [<span data-ttu-id="618dc-116">建立 Azure 媒體服務帳戶</span><span class="sxs-lookup"><span data-stu-id="618dc-116">Create an Azure Media Services account</span></span>](media-services-portal-create-account.md)
* <span data-ttu-id="618dc-117">確定有執行中的「串流端點」。</span><span class="sxs-lookup"><span data-stu-id="618dc-117">Ensure there is a Streaming Endpoint running.</span></span> <span data-ttu-id="618dc-118">如需詳細資訊，請參閱 [在媒體服務帳戶中管理串流端點](media-services-portal-manage-streaming-endpoints.md)</span><span class="sxs-lookup"><span data-stu-id="618dc-118">For more information, see [Manage Streaming Endpoints in a Media Services Account](media-services-portal-manage-streaming-endpoints.md)</span></span>
* <span data-ttu-id="618dc-119">安裝最新版的 [AMSE](https://github.com/Azure/Azure-Media-Services-Explorer) 工具。</span><span class="sxs-lookup"><span data-stu-id="618dc-119">Install the latest version of the [AMSE](https://github.com/Azure/Azure-Media-Services-Explorer) tool.</span></span>
* <span data-ttu-id="618dc-120">啟動工具並連接到您的 AMS 帳戶。</span><span class="sxs-lookup"><span data-stu-id="618dc-120">Launch the tool and connect to your AMS account.</span></span>

## <a name="tips"></a><span data-ttu-id="618dc-121">秘訣</span><span class="sxs-lookup"><span data-stu-id="618dc-121">Tips</span></span>
* <span data-ttu-id="618dc-122">請盡可能使用實體的有線網際網路連線。</span><span class="sxs-lookup"><span data-stu-id="618dc-122">Whenever possible, use a hardwired internet connection.</span></span>
* <span data-ttu-id="618dc-123">判斷頻寬需求的一項法則是將串流位元速率加倍。</span><span class="sxs-lookup"><span data-stu-id="618dc-123">A good rule of thumb when determining bandwidth requirements is to double the streaming bitrates.</span></span> <span data-ttu-id="618dc-124">雖然這不是強制性需求，卻有助於減輕網路阻塞的影響。</span><span class="sxs-lookup"><span data-stu-id="618dc-124">While this is not a mandatory requirement, it will help mitigate the impact of network congestion.</span></span>
* <span data-ttu-id="618dc-125">使用軟體型編碼器時，請關閉任何不必要的程式。</span><span class="sxs-lookup"><span data-stu-id="618dc-125">When using software based encoders, close out any unnecessary programs.</span></span>

## <a name="create-a-channel"></a><span data-ttu-id="618dc-126">建立通道</span><span class="sxs-lookup"><span data-stu-id="618dc-126">Create a channel</span></span>
1. <span data-ttu-id="618dc-127">在 AMSE 工具中，瀏覽至 [Live]  索引標籤，然後在通道區域內按一下滑鼠右鍵。</span><span class="sxs-lookup"><span data-stu-id="618dc-127">In the AMSE tool, navigate to the **Live** tab, and right click within the channel area.</span></span> <span data-ttu-id="618dc-128">從功能表選取 [建立通道...] </span><span class="sxs-lookup"><span data-stu-id="618dc-128">Select **Create channel…**</span></span> <span data-ttu-id="618dc-129">。</span><span class="sxs-lookup"><span data-stu-id="618dc-129">from the menu.</span></span>

    ![Tricaster](./media/media-services-tricaster-live-encoder/media-services-tricaster1.png)

2. <span data-ttu-id="618dc-131">指定通道名稱，描述欄位為選填。</span><span class="sxs-lookup"><span data-stu-id="618dc-131">Specify a channel name, the description field is optional.</span></span> <span data-ttu-id="618dc-132">在 [頻道設定] 下方，針對 [即時編碼] 選項選取 [標準]，並將 [輸入通訊協定] 設定為 [RTMP]。</span><span class="sxs-lookup"><span data-stu-id="618dc-132">Under Channel Settings, select **Standard** for the Live Encoding option, with the Input Protocol set to **RTMP**.</span></span> <span data-ttu-id="618dc-133">您可以將所有其他設定保留現狀。</span><span class="sxs-lookup"><span data-stu-id="618dc-133">You can leave all other settings as is.</span></span>

    <span data-ttu-id="618dc-134">請確認已選取 [ **立即啟動新頻道** ]。</span><span class="sxs-lookup"><span data-stu-id="618dc-134">Make sure the **Start the new channel now** is selected.</span></span>

3. <span data-ttu-id="618dc-135">按一下 [ **建立頻道**]。</span><span class="sxs-lookup"><span data-stu-id="618dc-135">Click **Create Channel**.</span></span>

   ![Tricaster](./media/media-services-tricaster-live-encoder/media-services-tricaster2.png)

> [!NOTE]
> <span data-ttu-id="618dc-137">通道約需 20 分鐘的時間即可啟動。</span><span class="sxs-lookup"><span data-stu-id="618dc-137">The channel can take as long as 20 minutes to start.</span></span>
>
>

<span data-ttu-id="618dc-138">當頻道啟動時，您可以 [設定編碼器](media-services-configure-tricaster-live-encoder.md#configure_tricaster_rtmp)。</span><span class="sxs-lookup"><span data-stu-id="618dc-138">While the channel is starting you can [configure the encoder](media-services-configure-tricaster-live-encoder.md#configure_tricaster_rtmp).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="618dc-139">請注意，只要通道進入就緒狀態，就會開始計費。</span><span class="sxs-lookup"><span data-stu-id="618dc-139">Note that billing starts as soon as Channel goes into a ready state.</span></span> <span data-ttu-id="618dc-140">如需詳細資訊，請參閱 [通道的狀態](media-services-manage-live-encoder-enabled-channels.md#states)。</span><span class="sxs-lookup"><span data-stu-id="618dc-140">For more information, see [Channel's states](media-services-manage-live-encoder-enabled-channels.md#states).</span></span>
>
>

## <span data-ttu-id="618dc-141"><a id=configure_tricaster_rtmp></a>設定 NewTek TriCaster 編碼器</span><span class="sxs-lookup"><span data-stu-id="618dc-141"><a id=configure_tricaster_rtmp></a>Configure the NewTek TriCaster encoder</span></span>
<span data-ttu-id="618dc-142">在本教學課程中會使用下列輸出設定。</span><span class="sxs-lookup"><span data-stu-id="618dc-142">In this tutorial the following output settings are used.</span></span> <span data-ttu-id="618dc-143">本章節的其餘部分將詳細說明組態步驟。</span><span class="sxs-lookup"><span data-stu-id="618dc-143">The rest of this section describes configuration steps in more detail.</span></span>

<span data-ttu-id="618dc-144">**視訊**：</span><span class="sxs-lookup"><span data-stu-id="618dc-144">**Video**:</span></span>

* <span data-ttu-id="618dc-145">轉碼器：H.264</span><span class="sxs-lookup"><span data-stu-id="618dc-145">Codec: H.264</span></span>
* <span data-ttu-id="618dc-146">設定檔：高 (層級 4.0)</span><span class="sxs-lookup"><span data-stu-id="618dc-146">Profile: High (Level 4.0)</span></span>
* <span data-ttu-id="618dc-147">位元速率：5000 kbps</span><span class="sxs-lookup"><span data-stu-id="618dc-147">Bitrate: 5000 kbps</span></span>
* <span data-ttu-id="618dc-148">主要畫面格：2 秒 (60 秒)</span><span class="sxs-lookup"><span data-stu-id="618dc-148">Keyframe: 2 seconds (60 seconds)</span></span>
* <span data-ttu-id="618dc-149">畫面播放速率：30</span><span class="sxs-lookup"><span data-stu-id="618dc-149">Frame Rate: 30</span></span>

<span data-ttu-id="618dc-150">**音訊**：</span><span class="sxs-lookup"><span data-stu-id="618dc-150">**Audio**:</span></span>

* <span data-ttu-id="618dc-151">轉碼器：AAC (LC)</span><span class="sxs-lookup"><span data-stu-id="618dc-151">Codec: AAC (LC)</span></span>
* <span data-ttu-id="618dc-152">位元速率：192 kbps</span><span class="sxs-lookup"><span data-stu-id="618dc-152">Bitrate: 192 kbps</span></span>
* <span data-ttu-id="618dc-153">取樣速率：44.1 kHz</span><span class="sxs-lookup"><span data-stu-id="618dc-153">Sample Rate: 44.1 kHz</span></span>

### <a name="configuration-steps"></a><span data-ttu-id="618dc-154">組態步驟</span><span class="sxs-lookup"><span data-stu-id="618dc-154">Configuration steps</span></span>
1. <span data-ttu-id="618dc-155">依據使用的視訊輸入來源建立新的 **NewTek TriCaster** 專案。</span><span class="sxs-lookup"><span data-stu-id="618dc-155">Create a new **NewTek TriCaster** project depending on what video input source is being used.</span></span>
2. <span data-ttu-id="618dc-156">進入該專案後，請尋找 [資料流]  按鈕，然後按一下該按鈕旁邊的齒輪圖示，以存取串流組態功能表。</span><span class="sxs-lookup"><span data-stu-id="618dc-156">Once within that project, find the **Stream** button, and click the gear icon next to it to access the stream configuration menu.</span></span>

    ![Tricaster](./media/media-services-tricaster-live-encoder/media-services-tricaster3.png)
3. <span data-ttu-id="618dc-158">開啟功能表後，按一下 [連接] 標題下的 [新增]  。</span><span class="sxs-lookup"><span data-stu-id="618dc-158">Once the menu has opened, click **New** under the Connection heading.</span></span> <span data-ttu-id="618dc-159">當系統提示您選取連接類型時，請選取 [Adobe Flash] 。</span><span class="sxs-lookup"><span data-stu-id="618dc-159">When prompted for the connection type, select **Adobe Flash**.</span></span>

    ![Tricaster](./media/media-services-tricaster-live-encoder/media-services-tricaster4.png)
4. <span data-ttu-id="618dc-161">按一下 [確定] 。</span><span class="sxs-lookup"><span data-stu-id="618dc-161">Click **OK**.</span></span>
5. <span data-ttu-id="618dc-162">現在按一下 [串流設定檔] 下方的下拉式清單箭頭，並瀏覽至 [瀏覽]，即可匯入 FMLE 設定檔。</span><span class="sxs-lookup"><span data-stu-id="618dc-162">An FMLE profile can now be imported by clicking the drop down arrow under **Streaming Profile** and navigating to **Browse**.</span></span>

    ![Tricaster](./media/media-services-tricaster-live-encoder/media-services-tricaster5.png)
6. <span data-ttu-id="618dc-164">瀏覽至儲存已設定之 FMLE 設定檔的位置。</span><span class="sxs-lookup"><span data-stu-id="618dc-164">Navigate to where the configured FMLE profile was saved.</span></span>
7. <span data-ttu-id="618dc-165">選取它，然後按下 [確定] 。</span><span class="sxs-lookup"><span data-stu-id="618dc-165">Select it, and press **OK**.</span></span>

    <span data-ttu-id="618dc-166">上傳設定檔後，請繼續進行下一個步驟。</span><span class="sxs-lookup"><span data-stu-id="618dc-166">Once the profile is uploaded, proceed to the next step.</span></span>
8. <span data-ttu-id="618dc-167">取得通道的輸入 URL，才能將它指派給 Tricaster 的 **RTMP 端點**。</span><span class="sxs-lookup"><span data-stu-id="618dc-167">Get the channel's input URL in order to assign it to the Tricaster **RTMP Endpoint**.</span></span>

    <span data-ttu-id="618dc-168">瀏覽回到 AMSE 工具，並檢查通道的完成狀態。</span><span class="sxs-lookup"><span data-stu-id="618dc-168">Navigate back to the AMSE tool, and check on the channel completion status.</span></span> <span data-ttu-id="618dc-169">狀態從 [啟動中] 變更為 [執行中] 後，您便可取得輸入 URL。</span><span class="sxs-lookup"><span data-stu-id="618dc-169">Once the State has changed from **Starting** to **Running**, you can get the input URL.</span></span>

    <span data-ttu-id="618dc-170">頻道執行時，以滑鼠右鍵按一下頻道名稱，向下瀏覽讓滑鼠游標停留在 [複製輸入 URL 到剪貼簿]，然後選取 [主要輸入 URL]。</span><span class="sxs-lookup"><span data-stu-id="618dc-170">When the channel is running, right click the channel name, navigate down to hover over **Copy Input URL to clipboard** and then select **Primary Input  URL**.</span></span>  

    ![Tricaster](./media/media-services-tricaster-live-encoder/media-services-tricaster6.png)
9. <span data-ttu-id="618dc-172">在 Tricaster 專案中，於 [Flash Server] 下的 [位置] 欄位貼上這項資訊。</span><span class="sxs-lookup"><span data-stu-id="618dc-172">Paste this information in the **Location** field under **Flash Server** within the Tricaster project.</span></span> <span data-ttu-id="618dc-173">此外也請在 [資料流 ID]  欄位中指派串流名稱。</span><span class="sxs-lookup"><span data-stu-id="618dc-173">Also assign a stream name in the **Stream ID** field.</span></span>

    <span data-ttu-id="618dc-174">如果串流資訊已新增至 FMLE 設定檔，您也可以按一下 [匯入設定]、瀏覽到已儲存的 FMLE 設定檔，並按一下 [確定]，來匯入至此區段。</span><span class="sxs-lookup"><span data-stu-id="618dc-174">If stream information was added to the FMLE profile, it can also be imported to this section by clicking **Import Settings**, navigating to the saved FMLE profile and clicking **OK**.</span></span> <span data-ttu-id="618dc-175">相關的 [Flash Server] 欄位應該填入 FMLE 的資訊。</span><span class="sxs-lookup"><span data-stu-id="618dc-175">The relevant Flash Server fields should populate with the information from FMLE.</span></span>

    ![Tricaster](./media/media-services-tricaster-live-encoder/media-services-tricaster7.png)
10. <span data-ttu-id="618dc-177">完成後，按一下畫面底部的 [確定]  。</span><span class="sxs-lookup"><span data-stu-id="618dc-177">When finished, click **OK** at the bottom of the screen.</span></span> <span data-ttu-id="618dc-178">輸入至 Tricaster 的視訊和音訊已就緒時，請按一下 [資料流]  按鈕，開始串流至 AMS。</span><span class="sxs-lookup"><span data-stu-id="618dc-178">When video and audio inputs into the Tricaster are ready, begin streaming to AMS by clicking the **Stream** button.</span></span>

     ![Tricaster](./media/media-services-tricaster-live-encoder/media-services-tricaster11.png)

> [!IMPORTANT]
> <span data-ttu-id="618dc-180">在您按一下 [資料流] 之前，**必須**確保通道已就緒。</span><span class="sxs-lookup"><span data-stu-id="618dc-180">Before you click **Stream**, you **must** ensure that the Channel is ready.</span></span>
> <span data-ttu-id="618dc-181">此外，請務必不要讓通道在沒有輸入比重摘要的情況下，處於就緒狀態超過 15 分鐘。</span><span class="sxs-lookup"><span data-stu-id="618dc-181">Also, make sure not to leave the Channel in a ready state without an input contribution feed for longer than > 15 minutes.</span></span>
>
>

## <a name="test-playback"></a><span data-ttu-id="618dc-182">測試播放</span><span class="sxs-lookup"><span data-stu-id="618dc-182">Test playback</span></span>
<span data-ttu-id="618dc-183">瀏覽至 AMSE 工具，然後以滑鼠右鍵按一下要測試的通道。</span><span class="sxs-lookup"><span data-stu-id="618dc-183">Navigate to the AMSE tool, and right click the channel to be tested.</span></span> <span data-ttu-id="618dc-184">在功能表中，將滑鼠游標停留在 [播放預覽]，並選取 [使用 Azure 媒體播放器]。</span><span class="sxs-lookup"><span data-stu-id="618dc-184">From the menu, hover over **Playback the Preview** and select **with Azure Media Player**.</span></span>  

    ![tricaster](./media/media-services-tricaster-live-encoder/media-services-tricaster8.png)

<span data-ttu-id="618dc-185">如果播放器中出現串流，則編碼器已妥善設定為連接到 AMS。</span><span class="sxs-lookup"><span data-stu-id="618dc-185">If the stream appears in the player, then the encoder has been properly configured to connect to AMS.</span></span>

<span data-ttu-id="618dc-186">如果收到錯誤，則必須重設通道，且編碼器設定需要調整。</span><span class="sxs-lookup"><span data-stu-id="618dc-186">If an error is received, the channel will need to be reset and encoder settings adjusted.</span></span> <span data-ttu-id="618dc-187">請參閱 [疑難排解](media-services-troubleshooting-live-streaming.md) 主題中的指引。</span><span class="sxs-lookup"><span data-stu-id="618dc-187">Please see the [troubleshooting](media-services-troubleshooting-live-streaming.md) topic for guidance.</span></span>  

## <a name="create-a-program"></a><span data-ttu-id="618dc-188">建立程式</span><span class="sxs-lookup"><span data-stu-id="618dc-188">Create a program</span></span>
1. <span data-ttu-id="618dc-189">一旦確認通道播放沒問題後，請建立程式。</span><span class="sxs-lookup"><span data-stu-id="618dc-189">Once channel playback is confirmed, create a program.</span></span> <span data-ttu-id="618dc-190">在 AMSE 工具的 [Live] 索引標籤下，於程式區域內按一下滑鼠右鍵，並選取 [建立新的程式]。</span><span class="sxs-lookup"><span data-stu-id="618dc-190">Under the **Live** tab in the AMSE tool, right click within the program area and select **Create New Program**.</span></span>  

    ![Tricaster](./media/media-services-tricaster-live-encoder/media-services-tricaster9.png)
2. <span data-ttu-id="618dc-192">為程式命名，並視需要調整 **封存時間長度** (預設為 4 小時)。</span><span class="sxs-lookup"><span data-stu-id="618dc-192">Name the program and, if needed, adjust the **Archive Window Length** (which defaults to 4 hours).</span></span> <span data-ttu-id="618dc-193">您也可以指定儲存體位置，或保留為預設值。</span><span class="sxs-lookup"><span data-stu-id="618dc-193">You can also specify a storage location or leave as the default.</span></span>  
3. <span data-ttu-id="618dc-194">勾選 [現在啟動程式]  方塊。</span><span class="sxs-lookup"><span data-stu-id="618dc-194">Check the **Start the Program now** box.</span></span>
4. <span data-ttu-id="618dc-195">按一下 [建立程式] 。</span><span class="sxs-lookup"><span data-stu-id="618dc-195">Click **Create Program**.</span></span>  

    >[!NOTE]
    ><span data-ttu-id="618dc-196">建立程式時所使用的時間會比建立通道時少。</span><span class="sxs-lookup"><span data-stu-id="618dc-196">Program creation takes less time than channel creation.</span></span>
        
5. <span data-ttu-id="618dc-197">一旦程式開始執行，請在程式上按一下滑鼠右鍵，並瀏覽至 [播放程式]，然後選取 [使用 Azure 媒體播放器] 確認播放。</span><span class="sxs-lookup"><span data-stu-id="618dc-197">Once the program is running, confirm playback by right clicking the program and navigating to **Playback the program(s)** and then selecting **with Azure Media Player**.</span></span>  
6. <span data-ttu-id="618dc-198">一經確認後，再次於該程式上按一下滑鼠右鍵，並選取 [複製輸出 URL 到剪貼簿] \(或從 [程式資訊和設定] 功能表選項擷取這項資訊)。</span><span class="sxs-lookup"><span data-stu-id="618dc-198">Once confirmed, right click the program again and select **Copy the Output URL to Clipboard** (or retrieve this information from the **Program information and settings** option from the menu).</span></span>

<span data-ttu-id="618dc-199">串流現在已經可以內嵌於播放程式中，或散發給某個對象，以供即時檢視。</span><span class="sxs-lookup"><span data-stu-id="618dc-199">The stream is now ready to be embedded in a player, or distributed to an audience for live viewing.</span></span>  

## <a name="troubleshooting"></a><span data-ttu-id="618dc-200">疑難排解</span><span class="sxs-lookup"><span data-stu-id="618dc-200">Troubleshooting</span></span>
<span data-ttu-id="618dc-201">請參閱 [疑難排解](media-services-troubleshooting-live-streaming.md) 主題中的指引。</span><span class="sxs-lookup"><span data-stu-id="618dc-201">Please see the [troubleshooting](media-services-troubleshooting-live-streaming.md) topic for guidance.</span></span>

## <a name="next-step"></a><span data-ttu-id="618dc-202">後續步驟</span><span class="sxs-lookup"><span data-stu-id="618dc-202">Next step</span></span>
<span data-ttu-id="618dc-203">檢閱媒體服務學習路徑。</span><span class="sxs-lookup"><span data-stu-id="618dc-203">Review Media Services learning paths.</span></span>

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="618dc-204">提供意見反應</span><span class="sxs-lookup"><span data-stu-id="618dc-204">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]
