---
title: "aaaConfigure hello NewTek tricaster 轉錄編碼器 toosend 單一位元速率即時資料流 |Microsoft 文件"
description: "本主題說明如何 tooconfigure hello tricaster 轉錄會即時編碼器 toosend 即時編碼啟用單一位元速率串流 tooAMS 通道。"
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
ms.openlocfilehash: 57dcf62a6a76b04e69f147a738be78ccb3c3ecdc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-newtek-tricaster-encoder-toosend-a-single-bitrate-live-stream"></a><span data-ttu-id="ecf5c-103">使用 hello NewTek tricaster 轉錄編碼器 toosend 單一位元速率即時資料流</span><span class="sxs-lookup"><span data-stu-id="ecf5c-103">Use hello NewTek TriCaster encoder toosend a single bitrate live stream</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="ecf5c-104">Tricaster</span><span class="sxs-lookup"><span data-stu-id="ecf5c-104">Tricaster</span></span>](media-services-configure-tricaster-live-encoder.md)
> * [<span data-ttu-id="ecf5c-105">Elemental Live</span><span class="sxs-lookup"><span data-stu-id="ecf5c-105">Elemental Live</span></span>](media-services-configure-elemental-live-encoder.md)
> * [<span data-ttu-id="ecf5c-106">Wirecast</span><span class="sxs-lookup"><span data-stu-id="ecf5c-106">Wirecast</span></span>](media-services-configure-wirecast-live-encoder.md)
> * [<span data-ttu-id="ecf5c-107">FMLE</span><span class="sxs-lookup"><span data-stu-id="ecf5c-107">FMLE</span></span>](media-services-configure-fmle-live-encoder.md)
>
>

<span data-ttu-id="ecf5c-108">本主題說明如何 tooconfigure hello [NewTek tricaster 轉錄](http://newtek.com/products/tricaster-40.html)即時編碼器 toosend 即時編碼啟用單一位元速率串流 tooAMS 通道。</span><span class="sxs-lookup"><span data-stu-id="ecf5c-108">This topic shows how tooconfigure hello [NewTek TriCaster](http://newtek.com/products/tricaster-40.html) live encoder toosend a single bitrate stream tooAMS channels that are enabled for live encoding.</span></span> <span data-ttu-id="ecf5c-109">如需詳細資訊，請參閱[使用通道，會啟用 tooPerform Live 使用 Azure 媒體服務編碼](media-services-manage-live-encoder-enabled-channels.md)。</span><span class="sxs-lookup"><span data-stu-id="ecf5c-109">For more information, see [Working with Channels that are Enabled tooPerform Live Encoding with Azure Media Services](media-services-manage-live-encoder-enabled-channels.md).</span></span>

<span data-ttu-id="ecf5c-110">本教學課程示範如何 toomanage Azure 媒體服務 (AMS) 中使用 Azure 媒體服務總管 (AMSE) 工具。</span><span class="sxs-lookup"><span data-stu-id="ecf5c-110">This tutorial shows how toomanage Azure Media Services (AMS) with Azure Media Services Explorer (AMSE) tool.</span></span> <span data-ttu-id="ecf5c-111">此工具只會在 Windows 電腦上執行。</span><span class="sxs-lookup"><span data-stu-id="ecf5c-111">This tool only runs on Windows PC.</span></span> <span data-ttu-id="ecf5c-112">如果您是在 Mac 或 Linux 上，使用 Azure 入口網站 toocreate hello[通道](media-services-portal-creating-live-encoder-enabled-channel.md#create-a-channel)和[程式](media-services-portal-creating-live-encoder-enabled-channel.md)。</span><span class="sxs-lookup"><span data-stu-id="ecf5c-112">If you are on Mac or Linux, use hello Azure portal toocreate [channels](media-services-portal-creating-live-encoder-enabled-channel.md#create-a-channel) and [programs](media-services-portal-creating-live-encoder-enabled-channel.md).</span></span>

> [!NOTE]
> <span data-ttu-id="ecf5c-113">使用 tricaster 轉錄比重中傳送的摘要為即時編碼啟用 tooAMS 通道時, 中可以有視訊/音訊問題即時事件如果您使用 tricaster 轉錄，例如快速摘要之間剪下或從情況切換的特定功能.</span><span class="sxs-lookup"><span data-stu-id="ecf5c-113">When using Tricaster for sending in a contribution feed tooAMS channels that are enabled for live encoding, there can be video/audio glitches in your live event if you use certain features of Tricaster, such as rapid cutting between feeds, or switching to/from slates.</span></span> <span data-ttu-id="ecf5c-114">hello AMS 團隊正在修正這些問題之前，它是不建議 toouse 這些功能。</span><span class="sxs-lookup"><span data-stu-id="ecf5c-114">hello AMS team is working on fixing these issues, until then, it is not recommend toouse these features.</span></span>
>
>

## <a name="prerequisites"></a><span data-ttu-id="ecf5c-115">必要條件</span><span class="sxs-lookup"><span data-stu-id="ecf5c-115">Prerequisites</span></span>
* [<span data-ttu-id="ecf5c-116">建立 Azure 媒體服務帳戶</span><span class="sxs-lookup"><span data-stu-id="ecf5c-116">Create an Azure Media Services account</span></span>](media-services-portal-create-account.md)
* <span data-ttu-id="ecf5c-117">確定有執行中的「串流端點」。</span><span class="sxs-lookup"><span data-stu-id="ecf5c-117">Ensure there is a Streaming Endpoint running.</span></span> <span data-ttu-id="ecf5c-118">如需詳細資訊，請參閱 [在媒體服務帳戶中管理串流端點](media-services-portal-manage-streaming-endpoints.md)</span><span class="sxs-lookup"><span data-stu-id="ecf5c-118">For more information, see [Manage Streaming Endpoints in a Media Services Account](media-services-portal-manage-streaming-endpoints.md)</span></span>
* <span data-ttu-id="ecf5c-119">安裝 hello 最新版 hello [AMSE](https://github.com/Azure/Azure-Media-Services-Explorer)工具。</span><span class="sxs-lookup"><span data-stu-id="ecf5c-119">Install hello latest version of hello [AMSE](https://github.com/Azure/Azure-Media-Services-Explorer) tool.</span></span>
* <span data-ttu-id="ecf5c-120">啟動 hello 工具和 tooyour AMS 帳戶連接。</span><span class="sxs-lookup"><span data-stu-id="ecf5c-120">Launch hello tool and connect tooyour AMS account.</span></span>

## <a name="tips"></a><span data-ttu-id="ecf5c-121">祕訣</span><span class="sxs-lookup"><span data-stu-id="ecf5c-121">Tips</span></span>
* <span data-ttu-id="ecf5c-122">請盡可能使用實體的有線網際網路連線。</span><span class="sxs-lookup"><span data-stu-id="ecf5c-122">Whenever possible, use a hardwired internet connection.</span></span>
* <span data-ttu-id="ecf5c-123">最佳經驗法則時判斷頻寬需求為串流處理位元的 toodouble hello。</span><span class="sxs-lookup"><span data-stu-id="ecf5c-123">A good rule of thumb when determining bandwidth requirements is toodouble hello streaming bitrates.</span></span> <span data-ttu-id="ecf5c-124">雖然這不是強制性需求，有助於減少 hello 發生網路壅塞的影響。</span><span class="sxs-lookup"><span data-stu-id="ecf5c-124">While this is not a mandatory requirement, it will help mitigate hello impact of network congestion.</span></span>
* <span data-ttu-id="ecf5c-125">使用軟體型編碼器時，請關閉任何不必要的程式。</span><span class="sxs-lookup"><span data-stu-id="ecf5c-125">When using software based encoders, close out any unnecessary programs.</span></span>

## <a name="create-a-channel"></a><span data-ttu-id="ecf5c-126">建立通道</span><span class="sxs-lookup"><span data-stu-id="ecf5c-126">Create a channel</span></span>
1. <span data-ttu-id="ecf5c-127">在 hello AMSE 工具中，瀏覽 toohello **Live**索引標籤，然後以滑鼠右鍵按一下 hello 通道區域內。</span><span class="sxs-lookup"><span data-stu-id="ecf5c-127">In hello AMSE tool, navigate toohello **Live** tab, and right click within hello channel area.</span></span> <span data-ttu-id="ecf5c-128">從功能表選取 [建立通道...] </span><span class="sxs-lookup"><span data-stu-id="ecf5c-128">Select **Create channel…**</span></span> <span data-ttu-id="ecf5c-129">從 [hello] 功能表中。</span><span class="sxs-lookup"><span data-stu-id="ecf5c-129">from hello menu.</span></span>

    ![Tricaster](./media/media-services-tricaster-live-encoder/media-services-tricaster1.png)

2. <span data-ttu-id="ecf5c-131">指定通道名稱，hello 描述欄位是選擇性的。</span><span class="sxs-lookup"><span data-stu-id="ecf5c-131">Specify a channel name, hello description field is optional.</span></span> <span data-ttu-id="ecf5c-132">在 [通道設定] 下選取**標準**hello 即時編碼選項，以 hello 輸入通訊協定設定得**RTMP**。</span><span class="sxs-lookup"><span data-stu-id="ecf5c-132">Under Channel Settings, select **Standard** for hello Live Encoding option, with hello Input Protocol set too**RTMP**.</span></span> <span data-ttu-id="ecf5c-133">您可以將所有其他設定保留現狀。</span><span class="sxs-lookup"><span data-stu-id="ecf5c-133">You can leave all other settings as is.</span></span>

    <span data-ttu-id="ecf5c-134">請確定 hello**開始 hello 新通道現在**已選取。</span><span class="sxs-lookup"><span data-stu-id="ecf5c-134">Make sure hello **Start hello new channel now** is selected.</span></span>

3. <span data-ttu-id="ecf5c-135">按一下 [ **建立頻道**]。</span><span class="sxs-lookup"><span data-stu-id="ecf5c-135">Click **Create Channel**.</span></span>

   ![Tricaster](./media/media-services-tricaster-live-encoder/media-services-tricaster2.png)

> [!NOTE]
> <span data-ttu-id="ecf5c-137">hello 通道花費 20 分鐘 toostart 一樣長。</span><span class="sxs-lookup"><span data-stu-id="ecf5c-137">hello channel can take as long as 20 minutes toostart.</span></span>
>
>

<span data-ttu-id="ecf5c-138">您可以啟動 hello 通道時[設定 hello 編碼器](media-services-configure-tricaster-live-encoder.md#configure_tricaster_rtmp)。</span><span class="sxs-lookup"><span data-stu-id="ecf5c-138">While hello channel is starting you can [configure hello encoder](media-services-configure-tricaster-live-encoder.md#configure_tricaster_rtmp).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="ecf5c-139">請注意，只要通道進入就緒狀態，就會開始計費。</span><span class="sxs-lookup"><span data-stu-id="ecf5c-139">Note that billing starts as soon as Channel goes into a ready state.</span></span> <span data-ttu-id="ecf5c-140">如需詳細資訊，請參閱 [通道的狀態](media-services-manage-live-encoder-enabled-channels.md#states)。</span><span class="sxs-lookup"><span data-stu-id="ecf5c-140">For more information, see [Channel's states](media-services-manage-live-encoder-enabled-channels.md#states).</span></span>
>
>

## <span data-ttu-id="ecf5c-141"><a id=configure_tricaster_rtmp></a>設定 hello NewTek tricaster 轉錄編碼器</span><span class="sxs-lookup"><span data-stu-id="ecf5c-141"><a id=configure_tricaster_rtmp></a>Configure hello NewTek TriCaster encoder</span></span>
<span data-ttu-id="ecf5c-142">在此教學課程的 hello 會使用下列的輸出設定。</span><span class="sxs-lookup"><span data-stu-id="ecf5c-142">In this tutorial hello following output settings are used.</span></span> <span data-ttu-id="ecf5c-143">hello 本節其餘部分描述更詳細的組態步驟。</span><span class="sxs-lookup"><span data-stu-id="ecf5c-143">hello rest of this section describes configuration steps in more detail.</span></span>

<span data-ttu-id="ecf5c-144">**視訊**：</span><span class="sxs-lookup"><span data-stu-id="ecf5c-144">**Video**:</span></span>

* <span data-ttu-id="ecf5c-145">轉碼器：H.264</span><span class="sxs-lookup"><span data-stu-id="ecf5c-145">Codec: H.264</span></span>
* <span data-ttu-id="ecf5c-146">設定檔：高 (層級 4.0)</span><span class="sxs-lookup"><span data-stu-id="ecf5c-146">Profile: High (Level 4.0)</span></span>
* <span data-ttu-id="ecf5c-147">位元速率：5000 kbps</span><span class="sxs-lookup"><span data-stu-id="ecf5c-147">Bitrate: 5000 kbps</span></span>
* <span data-ttu-id="ecf5c-148">主要畫面格：2 秒 (60 秒)</span><span class="sxs-lookup"><span data-stu-id="ecf5c-148">Keyframe: 2 seconds (60 seconds)</span></span>
* <span data-ttu-id="ecf5c-149">畫面播放速率：30</span><span class="sxs-lookup"><span data-stu-id="ecf5c-149">Frame Rate: 30</span></span>

<span data-ttu-id="ecf5c-150">**音訊**：</span><span class="sxs-lookup"><span data-stu-id="ecf5c-150">**Audio**:</span></span>

* <span data-ttu-id="ecf5c-151">轉碼器：AAC (LC)</span><span class="sxs-lookup"><span data-stu-id="ecf5c-151">Codec: AAC (LC)</span></span>
* <span data-ttu-id="ecf5c-152">位元速率：192 kbps</span><span class="sxs-lookup"><span data-stu-id="ecf5c-152">Bitrate: 192 kbps</span></span>
* <span data-ttu-id="ecf5c-153">取樣速率：44.1 kHz</span><span class="sxs-lookup"><span data-stu-id="ecf5c-153">Sample Rate: 44.1 kHz</span></span>

### <a name="configuration-steps"></a><span data-ttu-id="ecf5c-154">組態步驟</span><span class="sxs-lookup"><span data-stu-id="ecf5c-154">Configuration steps</span></span>
1. <span data-ttu-id="ecf5c-155">依據使用的視訊輸入來源建立新的 **NewTek TriCaster** 專案。</span><span class="sxs-lookup"><span data-stu-id="ecf5c-155">Create a new **NewTek TriCaster** project depending on what video input source is being used.</span></span>
2. <span data-ttu-id="ecf5c-156">一次在該專案中，找出 hello**資料流**按鈕，然後按一下 hello 齒輪圖示下一步 tooit tooaccess hello 資料流設定功能表。</span><span class="sxs-lookup"><span data-stu-id="ecf5c-156">Once within that project, find hello **Stream** button, and click hello gear icon next tooit tooaccess hello stream configuration menu.</span></span>

    ![Tricaster](./media/media-services-tricaster-live-encoder/media-services-tricaster3.png)
3. <span data-ttu-id="ecf5c-158">一旦已開啟 hello 功能表、 按一下**新增**hello 連接標題底下。</span><span class="sxs-lookup"><span data-stu-id="ecf5c-158">Once hello menu has opened, click **New** under hello Connection heading.</span></span> <span data-ttu-id="ecf5c-159">當提示 hello 連接類型，請選取**Adobe Flash**。</span><span class="sxs-lookup"><span data-stu-id="ecf5c-159">When prompted for hello connection type, select **Adobe Flash**.</span></span>

    ![Tricaster](./media/media-services-tricaster-live-encoder/media-services-tricaster4.png)
4. <span data-ttu-id="ecf5c-161">按一下 [確定] 。</span><span class="sxs-lookup"><span data-stu-id="ecf5c-161">Click **OK**.</span></span>
5. <span data-ttu-id="ecf5c-162">FMLE 設定檔現在 hello 下拉式底下的箭號，即可匯入**Streaming 設定檔**和瀏覽過**瀏覽**。</span><span class="sxs-lookup"><span data-stu-id="ecf5c-162">An FMLE profile can now be imported by clicking hello drop down arrow under **Streaming Profile** and navigating too**Browse**.</span></span>

    ![Tricaster](./media/media-services-tricaster-live-encoder/media-services-tricaster5.png)
6. <span data-ttu-id="ecf5c-164">瀏覽 toowhere 已儲存設定的 hello FMLE 設定檔。</span><span class="sxs-lookup"><span data-stu-id="ecf5c-164">Navigate toowhere hello configured FMLE profile was saved.</span></span>
7. <span data-ttu-id="ecf5c-165">選取它，然後按下 [確定] 。</span><span class="sxs-lookup"><span data-stu-id="ecf5c-165">Select it, and press **OK**.</span></span>

    <span data-ttu-id="ecf5c-166">一旦上傳 hello 設定檔時，可以繼續 toohello 下一個步驟。</span><span class="sxs-lookup"><span data-stu-id="ecf5c-166">Once hello profile is uploaded, proceed toohello next step.</span></span>
8. <span data-ttu-id="ecf5c-167">取得順序 tooassign hello 通道的輸入的 URL 它 toohello tricaster 轉錄**RTMP 端點**。</span><span class="sxs-lookup"><span data-stu-id="ecf5c-167">Get hello channel's input URL in order tooassign it toohello Tricaster **RTMP Endpoint**.</span></span>

    <span data-ttu-id="ecf5c-168">瀏覽後 toohello AMSE 工具，並檢查 hello 通道完成狀態。</span><span class="sxs-lookup"><span data-stu-id="ecf5c-168">Navigate back toohello AMSE tool, and check on hello channel completion status.</span></span> <span data-ttu-id="ecf5c-169">一旦 hello 狀態已從**起始**太**執行**，您可以取得 hello 輸入的 URL。</span><span class="sxs-lookup"><span data-stu-id="ecf5c-169">Once hello State has changed from **Starting** too**Running**, you can get hello input URL.</span></span>

    <span data-ttu-id="ecf5c-170">當執行 hello 通道時，hello 通道名稱上按一下滑鼠右鍵、 向下 toohover 巡覽**複製輸入 URL tooclipboard** ，然後選取 **主要輸入 URL**。</span><span class="sxs-lookup"><span data-stu-id="ecf5c-170">When hello channel is running, right click hello channel name, navigate down toohover over **Copy Input URL tooclipboard** and then select **Primary Input  URL**.</span></span>  

    ![Tricaster](./media/media-services-tricaster-live-encoder/media-services-tricaster6.png)
9. <span data-ttu-id="ecf5c-172">此資訊貼在 hello**位置**欄位底下**快閃伺服器**hello tricaster 轉錄專案內。</span><span class="sxs-lookup"><span data-stu-id="ecf5c-172">Paste this information in hello **Location** field under **Flash Server** within hello Tricaster project.</span></span> <span data-ttu-id="ecf5c-173">也將指定資料流中的名稱 hello**資料流識別碼**欄位。</span><span class="sxs-lookup"><span data-stu-id="ecf5c-173">Also assign a stream name in hello **Stream ID** field.</span></span>

    <span data-ttu-id="ecf5c-174">如果資料流資訊已新增 toohello FMLE 設定檔，它也可以匯 toothis 區段按一下**匯入設定**、 瀏覽儲存 toohello FMLE 設定檔，然後按一下**確定**。</span><span class="sxs-lookup"><span data-stu-id="ecf5c-174">If stream information was added toohello FMLE profile, it can also be imported toothis section by clicking **Import Settings**, navigating toohello saved FMLE profile and clicking **OK**.</span></span> <span data-ttu-id="ecf5c-175">hello 相關快閃伺服器欄位應該填入從 FMLE hello 資訊。</span><span class="sxs-lookup"><span data-stu-id="ecf5c-175">hello relevant Flash Server fields should populate with hello information from FMLE.</span></span>

    ![Tricaster](./media/media-services-tricaster-live-encoder/media-services-tricaster7.png)
10. <span data-ttu-id="ecf5c-177">完成後，請按一下**確定**在 hello 囉 」 畫面底部。</span><span class="sxs-lookup"><span data-stu-id="ecf5c-177">When finished, click **OK** at hello bottom of hello screen.</span></span> <span data-ttu-id="ecf5c-178">視訊和音訊的輸入內容 hello tricaster 轉錄準備好時，開始依序按一下 hello 串流 tooAMS**資料流** 按鈕。</span><span class="sxs-lookup"><span data-stu-id="ecf5c-178">When video and audio inputs into hello Tricaster are ready, begin streaming tooAMS by clicking hello **Stream** button.</span></span>

     ![Tricaster](./media/media-services-tricaster-live-encoder/media-services-tricaster11.png)

> [!IMPORTANT]
> <span data-ttu-id="ecf5c-180">在您按一下之前**資料流**，您**必須**確保 hello 通道已就緒。</span><span class="sxs-lookup"><span data-stu-id="ecf5c-180">Before you click **Stream**, you **must** ensure that hello Channel is ready.</span></span>
> <span data-ttu-id="ecf5c-181">此外，請確定未 tooleave hello 通道處於就緒狀態，而輸入的比重不摘要超過 > 15 分鐘。</span><span class="sxs-lookup"><span data-stu-id="ecf5c-181">Also, make sure not tooleave hello Channel in a ready state without an input contribution feed for longer than > 15 minutes.</span></span>
>
>

## <a name="test-playback"></a><span data-ttu-id="ecf5c-182">測試播放</span><span class="sxs-lookup"><span data-stu-id="ecf5c-182">Test playback</span></span>
<span data-ttu-id="ecf5c-183">瀏覽 toohello AMSE 工具，並以滑鼠右鍵按一下 hello 通道 toobe 測試。</span><span class="sxs-lookup"><span data-stu-id="ecf5c-183">Navigate toohello AMSE tool, and right click hello channel toobe tested.</span></span> <span data-ttu-id="ecf5c-184">從 [hello] 功能表中，將滑鼠停留在**播放 hello 預覽**選取**使用 Azure Media Player**。</span><span class="sxs-lookup"><span data-stu-id="ecf5c-184">From hello menu, hover over **Playback hello Preview** and select **with Azure Media Player**.</span></span>  

    ![tricaster](./media/media-services-tricaster-live-encoder/media-services-tricaster8.png)

<span data-ttu-id="ecf5c-185">Hello 資料流會顯示 hello 播放程式中，如果 hello 編碼器已經過正確設定的 tooconnect tooAMS。</span><span class="sxs-lookup"><span data-stu-id="ecf5c-185">If hello stream appears in hello player, then hello encoder has been properly configured tooconnect tooAMS.</span></span>

<span data-ttu-id="ecf5c-186">如果收到錯誤，hello 通道必須調整 toobe 重設和編碼器設定。</span><span class="sxs-lookup"><span data-stu-id="ecf5c-186">If an error is received, hello channel will need toobe reset and encoder settings adjusted.</span></span> <span data-ttu-id="ecf5c-187">請參閱 hello[疑難排解](media-services-troubleshooting-live-streaming.md)指引主題。</span><span class="sxs-lookup"><span data-stu-id="ecf5c-187">Please see hello [troubleshooting](media-services-troubleshooting-live-streaming.md) topic for guidance.</span></span>  

## <a name="create-a-program"></a><span data-ttu-id="ecf5c-188">建立程式</span><span class="sxs-lookup"><span data-stu-id="ecf5c-188">Create a program</span></span>
1. <span data-ttu-id="ecf5c-189">一旦確認通道播放沒問題後，請建立程式。</span><span class="sxs-lookup"><span data-stu-id="ecf5c-189">Once channel playback is confirmed, create a program.</span></span> <span data-ttu-id="ecf5c-190">在 hello **Live** hello AMSE 工具中索引標籤上，在 hello 程式區域按一下滑鼠右鍵並選取**建立新的程式**。</span><span class="sxs-lookup"><span data-stu-id="ecf5c-190">Under hello **Live** tab in hello AMSE tool, right click within hello program area and select **Create New Program**.</span></span>  

    ![Tricaster](./media/media-services-tricaster-live-encoder/media-services-tricaster9.png)
2. <span data-ttu-id="ecf5c-192">Hello 程式，並有需要則調整 hello**封存時間長度**（預設值 too4 時段）。</span><span class="sxs-lookup"><span data-stu-id="ecf5c-192">Name hello program and, if needed, adjust hello **Archive Window Length** (which defaults too4 hours).</span></span> <span data-ttu-id="ecf5c-193">您也可以指定儲存體位置，或保留 hello 預設。</span><span class="sxs-lookup"><span data-stu-id="ecf5c-193">You can also specify a storage location or leave as hello default.</span></span>  
3. <span data-ttu-id="ecf5c-194">檢查 hello**開始 hello 程式現在**方塊。</span><span class="sxs-lookup"><span data-stu-id="ecf5c-194">Check hello **Start hello Program now** box.</span></span>
4. <span data-ttu-id="ecf5c-195">按一下 [建立程式] 。</span><span class="sxs-lookup"><span data-stu-id="ecf5c-195">Click **Create Program**.</span></span>  

    >[!NOTE]
    ><span data-ttu-id="ecf5c-196">建立程式時所使用的時間會比建立通道時少。</span><span class="sxs-lookup"><span data-stu-id="ecf5c-196">Program creation takes less time than channel creation.</span></span>
        
5. <span data-ttu-id="ecf5c-197">Hello 程式開始執行之後，以確認播放 hello 程式上按一下滑鼠右鍵，瀏覽過**播放 hello （_r)** ，然後選取 **使用 Azure Media Player**。</span><span class="sxs-lookup"><span data-stu-id="ecf5c-197">Once hello program is running, confirm playback by right clicking hello program and navigating too**Playback hello program(s)** and then selecting **with Azure Media Player**.</span></span>  
6. <span data-ttu-id="ecf5c-198">確認，以滑鼠右鍵按一下 hello 程式，並選取**複製 hello 輸出 URL tooClipboard** (或擷取這項資訊從 hello**程式資訊和設定**hello 功能表選項)。</span><span class="sxs-lookup"><span data-stu-id="ecf5c-198">Once confirmed, right click hello program again and select **Copy hello Output URL tooClipboard** (or retrieve this information from hello **Program information and settings** option from hello menu).</span></span>

<span data-ttu-id="ecf5c-199">hello 資料流已準備好 toobe 內嵌在播放程式，或分散式的 tooan 對象的即時檢視。</span><span class="sxs-lookup"><span data-stu-id="ecf5c-199">hello stream is now ready toobe embedded in a player, or distributed tooan audience for live viewing.</span></span>  

## <a name="troubleshooting"></a><span data-ttu-id="ecf5c-200">疑難排解</span><span class="sxs-lookup"><span data-stu-id="ecf5c-200">Troubleshooting</span></span>
<span data-ttu-id="ecf5c-201">請參閱 hello[疑難排解](media-services-troubleshooting-live-streaming.md)指引主題。</span><span class="sxs-lookup"><span data-stu-id="ecf5c-201">Please see hello [troubleshooting](media-services-troubleshooting-live-streaming.md) topic for guidance.</span></span>

## <a name="next-step"></a><span data-ttu-id="ecf5c-202">後續步驟</span><span class="sxs-lookup"><span data-stu-id="ecf5c-202">Next step</span></span>
<span data-ttu-id="ecf5c-203">檢閱媒體服務學習路徑。</span><span class="sxs-lookup"><span data-stu-id="ecf5c-203">Review Media Services learning paths.</span></span>

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="ecf5c-204">提供意見反應</span><span class="sxs-lookup"><span data-stu-id="ecf5c-204">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]
