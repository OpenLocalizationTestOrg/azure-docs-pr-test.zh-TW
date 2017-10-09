---
title: "aaaConfigure hello Telestream Wirecast 編碼程式 toosend 單一位元速率即時資料流 |Microsoft 文件"
description: "本主題說明如何 tooconfigure hello Wirecast 會即時編碼器 toosend 即時編碼啟用單一位元速率串流 tooAMS 通道。 "
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
ms.openlocfilehash: e373f6c08232c652e65db584ded409c405d8cffe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-wirecast-encoder-toosend-a-single-bitrate-live-stream"></a><span data-ttu-id="9e5c1-103">使用 hello Wirecast 編碼程式 toosend 單一位元速率即時資料流</span><span class="sxs-lookup"><span data-stu-id="9e5c1-103">Use hello Wirecast encoder toosend a single bitrate live stream</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="9e5c1-104">Wirecast</span><span class="sxs-lookup"><span data-stu-id="9e5c1-104">Wirecast</span></span>](media-services-configure-wirecast-live-encoder.md)
> * [<span data-ttu-id="9e5c1-105">Elemental Live</span><span class="sxs-lookup"><span data-stu-id="9e5c1-105">Elemental Live</span></span>](media-services-configure-elemental-live-encoder.md)
> * [<span data-ttu-id="9e5c1-106">Tricaster</span><span class="sxs-lookup"><span data-stu-id="9e5c1-106">Tricaster</span></span>](media-services-configure-tricaster-live-encoder.md)
> * [<span data-ttu-id="9e5c1-107">FMLE</span><span class="sxs-lookup"><span data-stu-id="9e5c1-107">FMLE</span></span>](media-services-configure-fmle-live-encoder.md)
>
>

<span data-ttu-id="9e5c1-108">本主題說明如何 tooconfigure hello [Telestream wirecast 編碼](http://www.telestream.net/wirecast/overview.htm)即時編碼器 toosend 即時編碼啟用單一位元速率串流 tooAMS 通道。</span><span class="sxs-lookup"><span data-stu-id="9e5c1-108">This topic shows how tooconfigure hello [Telestream Wirecast](http://www.telestream.net/wirecast/overview.htm) live encoder toosend a single bitrate stream tooAMS channels that are enabled for live encoding.</span></span>  <span data-ttu-id="9e5c1-109">如需詳細資訊，請參閱[使用通道，會啟用 tooPerform Live 使用 Azure 媒體服務編碼](media-services-manage-live-encoder-enabled-channels.md)。</span><span class="sxs-lookup"><span data-stu-id="9e5c1-109">For more information, see [Working with Channels that are Enabled tooPerform Live Encoding with Azure Media Services](media-services-manage-live-encoder-enabled-channels.md).</span></span>

<span data-ttu-id="9e5c1-110">本教學課程示範如何 toomanage Azure 媒體服務 (AMS) 中使用 Azure 媒體服務總管 (AMSE) 工具。</span><span class="sxs-lookup"><span data-stu-id="9e5c1-110">This tutorial shows how toomanage Azure Media Services (AMS) with Azure Media Services Explorer (AMSE) tool.</span></span> <span data-ttu-id="9e5c1-111">此工具只會在 Windows 電腦上執行。</span><span class="sxs-lookup"><span data-stu-id="9e5c1-111">This tool only runs on Windows PC.</span></span> <span data-ttu-id="9e5c1-112">如果您是在 Mac 或 Linux 上，使用 Azure 入口網站 toocreate hello[通道](media-services-portal-creating-live-encoder-enabled-channel.md#create-a-channel)和[程式](media-services-portal-creating-live-encoder-enabled-channel.md)。</span><span class="sxs-lookup"><span data-stu-id="9e5c1-112">If you are on Mac or Linux, use hello Azure portal toocreate [channels](media-services-portal-creating-live-encoder-enabled-channel.md#create-a-channel) and [programs](media-services-portal-creating-live-encoder-enabled-channel.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="9e5c1-113">必要條件</span><span class="sxs-lookup"><span data-stu-id="9e5c1-113">Prerequisites</span></span>
* [<span data-ttu-id="9e5c1-114">建立 Azure 媒體服務帳戶</span><span class="sxs-lookup"><span data-stu-id="9e5c1-114">Create an Azure Media Services account</span></span>](media-services-portal-create-account.md)
* <span data-ttu-id="9e5c1-115">確定有執行中的「串流端點」。</span><span class="sxs-lookup"><span data-stu-id="9e5c1-115">Ensure there is a Streaming Endpoint running.</span></span> <span data-ttu-id="9e5c1-116">如需詳細資訊，請參閱 [在媒體服務帳戶中管理串流端點](media-services-portal-manage-streaming-endpoints.md)</span><span class="sxs-lookup"><span data-stu-id="9e5c1-116">For more information, see [Manage Streaming Endpoints in a Media Services Account](media-services-portal-manage-streaming-endpoints.md)</span></span>
* <span data-ttu-id="9e5c1-117">安裝 hello 最新版 hello [AMSE](https://github.com/Azure/Azure-Media-Services-Explorer)工具。</span><span class="sxs-lookup"><span data-stu-id="9e5c1-117">Install hello latest version of hello [AMSE](https://github.com/Azure/Azure-Media-Services-Explorer) tool.</span></span>
* <span data-ttu-id="9e5c1-118">啟動 hello 工具和 tooyour AMS 帳戶連接。</span><span class="sxs-lookup"><span data-stu-id="9e5c1-118">Launch hello tool and connect tooyour AMS account.</span></span>

## <a name="tips"></a><span data-ttu-id="9e5c1-119">祕訣</span><span class="sxs-lookup"><span data-stu-id="9e5c1-119">Tips</span></span>
* <span data-ttu-id="9e5c1-120">請盡可能使用實體的有線網際網路連線。</span><span class="sxs-lookup"><span data-stu-id="9e5c1-120">Whenever possible, use a hardwired internet connection.</span></span>
* <span data-ttu-id="9e5c1-121">最佳經驗法則時判斷頻寬需求為串流處理位元的 toodouble hello。</span><span class="sxs-lookup"><span data-stu-id="9e5c1-121">A good rule of thumb when determining bandwidth requirements is toodouble hello streaming bitrates.</span></span> <span data-ttu-id="9e5c1-122">雖然這不是強制性需求，有助於減少 hello 發生網路壅塞的影響。</span><span class="sxs-lookup"><span data-stu-id="9e5c1-122">While this is not a mandatory requirement, it will help mitigate hello impact of network congestion.</span></span>
* <span data-ttu-id="9e5c1-123">使用軟體型編碼器時，請關閉任何不必要的程式。</span><span class="sxs-lookup"><span data-stu-id="9e5c1-123">When using software based encoders, close out any unnecessary programs.</span></span>

## <a name="create-a-channel"></a><span data-ttu-id="9e5c1-124">建立通道</span><span class="sxs-lookup"><span data-stu-id="9e5c1-124">Create a channel</span></span>
1. <span data-ttu-id="9e5c1-125">在 hello AMSE 工具中，瀏覽 toohello **Live**索引標籤，然後以滑鼠右鍵按一下 hello 通道區域內。</span><span class="sxs-lookup"><span data-stu-id="9e5c1-125">In hello AMSE tool, navigate toohello **Live** tab, and right click within hello channel area.</span></span> <span data-ttu-id="9e5c1-126">從功能表選取 [建立通道...] </span><span class="sxs-lookup"><span data-stu-id="9e5c1-126">Select **Create channel…**</span></span> <span data-ttu-id="9e5c1-127">從 [hello] 功能表中。</span><span class="sxs-lookup"><span data-stu-id="9e5c1-127">from hello menu.</span></span>

    ![Wirecast](./media/media-services-wirecast-live-encoder/media-services-wirecast1.png)

2. <span data-ttu-id="9e5c1-129">指定通道名稱，hello 描述欄位是選擇性的。</span><span class="sxs-lookup"><span data-stu-id="9e5c1-129">Specify a channel name, hello description field is optional.</span></span> <span data-ttu-id="9e5c1-130">在 [通道設定] 下選取**標準**hello 即時編碼選項，以 hello 輸入通訊協定設定得**RTMP**。</span><span class="sxs-lookup"><span data-stu-id="9e5c1-130">Under Channel Settings, select **Standard** for hello Live Encoding option, with hello Input Protocol set too**RTMP**.</span></span> <span data-ttu-id="9e5c1-131">您可以將所有其他設定保留現狀。</span><span class="sxs-lookup"><span data-stu-id="9e5c1-131">You can leave all other settings as is.</span></span>

    <span data-ttu-id="9e5c1-132">請確定 hello**開始 hello 新通道現在**已選取。</span><span class="sxs-lookup"><span data-stu-id="9e5c1-132">Make sure hello **Start hello new channel now** is selected.</span></span>

3. <span data-ttu-id="9e5c1-133">按一下 [ **建立頻道**]。</span><span class="sxs-lookup"><span data-stu-id="9e5c1-133">Click **Create Channel**.</span></span>

   ![Wirecast](./media/media-services-wirecast-live-encoder/media-services-wirecast2.png)

> [!NOTE]
> <span data-ttu-id="9e5c1-135">hello 通道花費 20 分鐘 toostart 一樣長。</span><span class="sxs-lookup"><span data-stu-id="9e5c1-135">hello channel can take as long as 20 minutes toostart.</span></span>
>
>

<span data-ttu-id="9e5c1-136">您可以啟動 hello 通道時[設定 hello 編碼器](media-services-configure-wirecast-live-encoder.md#configure_wirecast_rtmp)。</span><span class="sxs-lookup"><span data-stu-id="9e5c1-136">While hello channel is starting you can [configure hello encoder](media-services-configure-wirecast-live-encoder.md#configure_wirecast_rtmp).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="9e5c1-137">請注意，只要通道進入就緒狀態，就會開始計費。</span><span class="sxs-lookup"><span data-stu-id="9e5c1-137">Note that billing starts as soon as Channel goes into a ready state.</span></span> <span data-ttu-id="9e5c1-138">如需詳細資訊，請參閱 [通道的狀態](media-services-manage-live-encoder-enabled-channels.md#states)。</span><span class="sxs-lookup"><span data-stu-id="9e5c1-138">For more information, see [Channel's states](media-services-manage-live-encoder-enabled-channels.md#states).</span></span>
>
>

## <span data-ttu-id="9e5c1-139"><a id=configure_wirecast_rtmp></a>設定 Telestream wirecast 編碼程式 hello</span><span class="sxs-lookup"><span data-stu-id="9e5c1-139"><a id=configure_wirecast_rtmp></a>Configure hello Telestream Wirecast encoder</span></span>
<span data-ttu-id="9e5c1-140">在此教學課程的 hello 會使用下列的輸出設定。</span><span class="sxs-lookup"><span data-stu-id="9e5c1-140">In this tutorial hello following output settings are used.</span></span> <span data-ttu-id="9e5c1-141">hello 本節其餘部分描述更詳細的組態步驟。</span><span class="sxs-lookup"><span data-stu-id="9e5c1-141">hello rest of this section describes configuration steps in more detail.</span></span>

<span data-ttu-id="9e5c1-142">**視訊**：</span><span class="sxs-lookup"><span data-stu-id="9e5c1-142">**Video**:</span></span>

* <span data-ttu-id="9e5c1-143">轉碼器：H.264</span><span class="sxs-lookup"><span data-stu-id="9e5c1-143">Codec: H.264</span></span>
* <span data-ttu-id="9e5c1-144">設定檔：高 (層級 4.0)</span><span class="sxs-lookup"><span data-stu-id="9e5c1-144">Profile: High (Level 4.0)</span></span>
* <span data-ttu-id="9e5c1-145">位元速率：5000 kbps</span><span class="sxs-lookup"><span data-stu-id="9e5c1-145">Bitrate: 5000 kbps</span></span>
* <span data-ttu-id="9e5c1-146">主要畫面格：2 秒 (60 秒)</span><span class="sxs-lookup"><span data-stu-id="9e5c1-146">Keyframe: 2 seconds (60 seconds)</span></span>
* <span data-ttu-id="9e5c1-147">畫面播放速率：30</span><span class="sxs-lookup"><span data-stu-id="9e5c1-147">Frame Rate: 30</span></span>

<span data-ttu-id="9e5c1-148">**音訊**：</span><span class="sxs-lookup"><span data-stu-id="9e5c1-148">**Audio**:</span></span>

* <span data-ttu-id="9e5c1-149">轉碼器：AAC (LC)</span><span class="sxs-lookup"><span data-stu-id="9e5c1-149">Codec: AAC (LC)</span></span>
* <span data-ttu-id="9e5c1-150">位元速率：192 kbps</span><span class="sxs-lookup"><span data-stu-id="9e5c1-150">Bitrate: 192 kbps</span></span>
* <span data-ttu-id="9e5c1-151">取樣速率：44.1 kHz</span><span class="sxs-lookup"><span data-stu-id="9e5c1-151">Sample Rate: 44.1 kHz</span></span>

### <a name="configuration-steps"></a><span data-ttu-id="9e5c1-152">組態步驟</span><span class="sxs-lookup"><span data-stu-id="9e5c1-152">Configuration steps</span></span>
1. <span data-ttu-id="9e5c1-153">使用，而且 RTMP 資料流的設定，請開啟 hello 機器必須 hello Telestream wirecast 編碼應用程式。</span><span class="sxs-lookup"><span data-stu-id="9e5c1-153">Open hello Telestream Wirecast application on hello machine being used, and set up for RTMP streaming.</span></span>
2. <span data-ttu-id="9e5c1-154">瀏覽 toohello 設定 hello 輸出**輸出** 索引標籤，然後選取**輸出設定...**.</span><span class="sxs-lookup"><span data-stu-id="9e5c1-154">Configure hello output by navigating toohello **Output** tab and selecting **Output Settings…**.</span></span>

    <span data-ttu-id="9e5c1-155">請確定 hello**輸出目的地**設定得**RTMP 伺服器**。</span><span class="sxs-lookup"><span data-stu-id="9e5c1-155">Make sure hello **Output Destination** is set too**RTMP Server**.</span></span>
3. <span data-ttu-id="9e5c1-156">按一下 [確定] 。</span><span class="sxs-lookup"><span data-stu-id="9e5c1-156">Click **OK**.</span></span>
4. <span data-ttu-id="9e5c1-157">在 [hello] 設定頁面上，設定 hello**目的地**欄位 toobe **Azure Media Services**。</span><span class="sxs-lookup"><span data-stu-id="9e5c1-157">On hello settings page, set hello **Destination** field toobe **Azure Media Services**.</span></span>

    <span data-ttu-id="9e5c1-158">hello 編碼設定檔預先選取太**Azure H.264 720 p 16:9 (1280 x 720)**。</span><span class="sxs-lookup"><span data-stu-id="9e5c1-158">hello Encoding profile is pre-selected too**Azure H.264 720p 16:9 (1280x720)**.</span></span> <span data-ttu-id="9e5c1-159">toocustomize 下拉式清單，這些設定，請選取 hello 齒輪圖示 toohello 方 hello，然後選擇**新增預設**。</span><span class="sxs-lookup"><span data-stu-id="9e5c1-159">toocustomize these settings, select hello gear icon toohello right of hello drop down, and then choose **New Preset**.</span></span>

    ![Wirecast](./media/media-services-wirecast-live-encoder/media-services-wirecast3.png)
5. <span data-ttu-id="9e5c1-161">設定編碼器預設。</span><span class="sxs-lookup"><span data-stu-id="9e5c1-161">Configure encoder presets.</span></span>

    <span data-ttu-id="9e5c1-162">名稱 hello 預先設定，並檢查 hello 下列建議的設定：</span><span class="sxs-lookup"><span data-stu-id="9e5c1-162">Name hello preset, and check for hello following recommended settings:</span></span>

    <span data-ttu-id="9e5c1-163">**影片**</span><span class="sxs-lookup"><span data-stu-id="9e5c1-163">**Video**</span></span>

   * <span data-ttu-id="9e5c1-164">編碼器：MainConcept H.264</span><span class="sxs-lookup"><span data-stu-id="9e5c1-164">Encoder: MainConcept H.264</span></span>
   * <span data-ttu-id="9e5c1-165">每秒畫面格數：30</span><span class="sxs-lookup"><span data-stu-id="9e5c1-165">Frames per Second: 30</span></span>
   * <span data-ttu-id="9e5c1-166">平均位元速率：5000 kbit/秒 (可視網路限制加以調整)</span><span class="sxs-lookup"><span data-stu-id="9e5c1-166">Average bit rate: 5000 kbits/sec (Can be adjusted based on network limitations)</span></span>
   * <span data-ttu-id="9e5c1-167">設定檔：主要</span><span class="sxs-lookup"><span data-stu-id="9e5c1-167">Profile: Main</span></span>
   * <span data-ttu-id="9e5c1-168">畫面間隔：60 個畫面</span><span class="sxs-lookup"><span data-stu-id="9e5c1-168">Key frame every: 60 frames</span></span>

    <span data-ttu-id="9e5c1-169">**音訊**</span><span class="sxs-lookup"><span data-stu-id="9e5c1-169">**Audio**</span></span>

   * <span data-ttu-id="9e5c1-170">目標位元速率：192 kbit/秒</span><span class="sxs-lookup"><span data-stu-id="9e5c1-170">Target bit rate: 192 kbits/sec</span></span>
   * <span data-ttu-id="9e5c1-171">取樣速率：44.100 kHz</span><span class="sxs-lookup"><span data-stu-id="9e5c1-171">Sample Rate: 44.100 kHz</span></span>

     ![Wirecast](./media/media-services-wirecast-live-encoder/media-services-wirecast4.png)
6. <span data-ttu-id="9e5c1-173">按下 [儲存] 。</span><span class="sxs-lookup"><span data-stu-id="9e5c1-173">Press **Save**.</span></span>

    <span data-ttu-id="9e5c1-174">hello Encoding 欄位現在有新建立的 hello 設定檔可讓您選取。</span><span class="sxs-lookup"><span data-stu-id="9e5c1-174">hello Encoding field now has hello newly created profile available for selection.</span></span>

    <span data-ttu-id="9e5c1-175">請確定已選取 hello 新設定檔。</span><span class="sxs-lookup"><span data-stu-id="9e5c1-175">Make sure hello new profile is selected.</span></span>
7. <span data-ttu-id="9e5c1-176">取得順序 tooassign hello 通道的輸入的 URL 它 toohello Wirecast **RTMP 端點**。</span><span class="sxs-lookup"><span data-stu-id="9e5c1-176">Get hello channel's input URL in order tooassign it toohello Wirecast **RTMP Endpoint**.</span></span>

    <span data-ttu-id="9e5c1-177">瀏覽後 toohello AMSE 工具，並檢查 hello 通道完成狀態。</span><span class="sxs-lookup"><span data-stu-id="9e5c1-177">Navigate back toohello AMSE tool, and check on hello channel completion status.</span></span> <span data-ttu-id="9e5c1-178">一旦 hello 狀態已從**起始**太**執行**，您可以取得 hello 輸入的 URL。</span><span class="sxs-lookup"><span data-stu-id="9e5c1-178">Once hello State has changed from **Starting** too**Running**, you can get hello input URL.</span></span>

    <span data-ttu-id="9e5c1-179">當執行 hello 通道時，hello 通道名稱上按一下滑鼠右鍵、 向下 toohover 巡覽**複製輸入 URL tooclipboard** ，然後選取 **主要輸入 URL**。</span><span class="sxs-lookup"><span data-stu-id="9e5c1-179">When hello channel is running, right click hello channel name, navigate down toohover over **Copy Input URL tooclipboard** and then select **Primary Input  URL**.</span></span>  

    ![Wirecast](./media/media-services-wirecast-live-encoder/media-services-wirecast6.png)
8. <span data-ttu-id="9e5c1-181">Hello Wirecast 中**輸出設定**視窗中，貼上這個資訊中 hello**位址**hello 輸出區段中，並指派資料流名稱的欄位。</span><span class="sxs-lookup"><span data-stu-id="9e5c1-181">In hello Wirecast **Output Settings** window, paste this information in hello **Address** field of hello output section, and assign a stream name.</span></span>

    ![Wirecast](./media/media-services-wirecast-live-encoder/media-services-wirecast5.png)

1. <span data-ttu-id="9e5c1-183">選取 [確定] 。</span><span class="sxs-lookup"><span data-stu-id="9e5c1-183">Select **OK**.</span></span>
2. <span data-ttu-id="9e5c1-184">在 hello 主要**Wirecast**畫面上，確認輸入的來源視訊和音訊的準備，然後按下**資料流**hello 最上層的左下角中。</span><span class="sxs-lookup"><span data-stu-id="9e5c1-184">On hello main **Wirecast** screen, confirm input sources for video and audio are ready and then hit **Stream** in hello top left hand corner.</span></span>

   ![Wirecast](./media/media-services-wirecast-live-encoder/media-services-wirecast7.png)

> [!IMPORTANT]
> <span data-ttu-id="9e5c1-186">在您按一下之前**資料流**，您**必須**確保 hello 通道已就緒。</span><span class="sxs-lookup"><span data-stu-id="9e5c1-186">Before you click **Stream**, you **must** ensure that hello Channel is ready.</span></span>
> <span data-ttu-id="9e5c1-187">此外，請確定未 tooleave hello 通道處於就緒狀態，而輸入的比重不摘要超過 > 15 分鐘。</span><span class="sxs-lookup"><span data-stu-id="9e5c1-187">Also, make sure not tooleave hello Channel in a ready state without an input contribution feed for longer than > 15 minutes.</span></span>
>
>

## <a name="test-playback"></a><span data-ttu-id="9e5c1-188">測試播放</span><span class="sxs-lookup"><span data-stu-id="9e5c1-188">Test playback</span></span>

<span data-ttu-id="9e5c1-189">瀏覽 toohello AMSE 工具，並以滑鼠右鍵按一下 hello 通道 toobe 測試。</span><span class="sxs-lookup"><span data-stu-id="9e5c1-189">Navigate toohello AMSE tool, and right click hello channel toobe tested.</span></span> <span data-ttu-id="9e5c1-190">從 [hello] 功能表中，將滑鼠停留在**播放 hello 預覽**選取**使用 Azure Media Player**。</span><span class="sxs-lookup"><span data-stu-id="9e5c1-190">From hello menu, hover over **Playback hello Preview** and select **with Azure Media Player**.</span></span>  

    ![wirecast](./media/media-services-wirecast-live-encoder/media-services-wirecast8.png)

<span data-ttu-id="9e5c1-191">Hello 資料流會顯示 hello 播放程式中，如果 hello 編碼器已經過正確設定的 tooconnect tooAMS。</span><span class="sxs-lookup"><span data-stu-id="9e5c1-191">If hello stream appears in hello player, then hello encoder has been properly configured tooconnect tooAMS.</span></span>

<span data-ttu-id="9e5c1-192">如果收到錯誤，hello 通道必須調整 toobe 重設和編碼器設定。</span><span class="sxs-lookup"><span data-stu-id="9e5c1-192">If an error is received, hello channel will need toobe reset and encoder settings adjusted.</span></span> <span data-ttu-id="9e5c1-193">請參閱 hello[疑難排解](media-services-troubleshooting-live-streaming.md)指引主題。</span><span class="sxs-lookup"><span data-stu-id="9e5c1-193">Please see hello [troubleshooting](media-services-troubleshooting-live-streaming.md) topic for guidance.</span></span>  

## <a name="create-a-program"></a><span data-ttu-id="9e5c1-194">建立程式</span><span class="sxs-lookup"><span data-stu-id="9e5c1-194">Create a program</span></span>
1. <span data-ttu-id="9e5c1-195">一旦確認通道播放沒問題後，請建立程式。</span><span class="sxs-lookup"><span data-stu-id="9e5c1-195">Once channel playback is confirmed, create a program.</span></span> <span data-ttu-id="9e5c1-196">在 hello **Live** hello AMSE 工具中索引標籤上，在 hello 程式區域按一下滑鼠右鍵並選取**建立新的程式**。</span><span class="sxs-lookup"><span data-stu-id="9e5c1-196">Under hello **Live** tab in hello AMSE tool, right click within hello program area and select **Create New Program**.</span></span>  

    ![Wirecast](./media/media-services-wirecast-live-encoder/media-services-wirecast9.png)
2. <span data-ttu-id="9e5c1-198">Hello 程式，並有需要則調整 hello**封存時間長度**（預設值 too4 時段）。</span><span class="sxs-lookup"><span data-stu-id="9e5c1-198">Name hello program and, if needed, adjust hello **Archive Window Length** (which defaults too4 hours).</span></span> <span data-ttu-id="9e5c1-199">您也可以指定儲存體位置，或保留 hello 預設。</span><span class="sxs-lookup"><span data-stu-id="9e5c1-199">You can also specify a storage location or leave as hello default.</span></span>  
3. <span data-ttu-id="9e5c1-200">檢查 hello**開始 hello 程式現在**方塊。</span><span class="sxs-lookup"><span data-stu-id="9e5c1-200">Check hello **Start hello Program now** box.</span></span>
4. <span data-ttu-id="9e5c1-201">按一下 [建立程式] 。</span><span class="sxs-lookup"><span data-stu-id="9e5c1-201">Click **Create Program**.</span></span>  

   >[!NOTE]
   ><span data-ttu-id="9e5c1-202">建立程式時所使用的時間會比建立通道時少。</span><span class="sxs-lookup"><span data-stu-id="9e5c1-202">Program creation takes less time than channel creation.</span></span>
       
5. <span data-ttu-id="9e5c1-203">Hello 程式開始執行之後，以確認播放 hello 程式上按一下滑鼠右鍵，瀏覽過**播放 hello （_r)** ，然後選取 **使用 Azure Media Player**。</span><span class="sxs-lookup"><span data-stu-id="9e5c1-203">Once hello program is running, confirm playback by right clicking hello program and navigating too**Playback hello program(s)** and then selecting **with Azure Media Player**.</span></span>  
6. <span data-ttu-id="9e5c1-204">確認，以滑鼠右鍵按一下 hello 程式，並選取**複製 hello 輸出 URL tooClipboard** (或擷取這項資訊從 hello**程式資訊和設定**hello 功能表選項)。</span><span class="sxs-lookup"><span data-stu-id="9e5c1-204">Once confirmed, right click hello program again and select **Copy hello Output URL tooClipboard** (or retrieve this information from hello **Program information and settings** option from hello menu).</span></span>

<span data-ttu-id="9e5c1-205">hello 資料流已準備好 toobe 內嵌在播放程式，或分散式的 tooan 對象的即時檢視。</span><span class="sxs-lookup"><span data-stu-id="9e5c1-205">hello stream is now ready toobe embedded in a player, or distributed tooan audience for live viewing.</span></span>  

## <a name="troubleshooting"></a><span data-ttu-id="9e5c1-206">疑難排解</span><span class="sxs-lookup"><span data-stu-id="9e5c1-206">Troubleshooting</span></span>
<span data-ttu-id="9e5c1-207">請參閱 hello[疑難排解](media-services-troubleshooting-live-streaming.md)指引主題。</span><span class="sxs-lookup"><span data-stu-id="9e5c1-207">Please see hello [troubleshooting](media-services-troubleshooting-live-streaming.md) topic for guidance.</span></span>

## <a name="media-services-learning-paths"></a><span data-ttu-id="9e5c1-208">媒體服務學習路徑</span><span class="sxs-lookup"><span data-stu-id="9e5c1-208">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="9e5c1-209">提供意見反應</span><span class="sxs-lookup"><span data-stu-id="9e5c1-209">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]
