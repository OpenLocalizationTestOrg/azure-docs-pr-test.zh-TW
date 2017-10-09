---
title: "aaaHow tooperform 即時資料流使用 Azure Media Services toocreate 多位元速率串流以 hello Azure 入口網站 |Microsoft 文件"
description: "此教學課程會逐步引導您完成建立通道的 hello 步驟接收單一位元速率即時串流，並將其編碼使用 hello Azure 入口網站的 toomulti 位元速率資料流。"
services: media-services
documentationcenter: 
author: anilmur
manager: cfowler
editor: 
ms.assetid: 504f74c2-3103-42a0-897b-9ff52f279e23
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 08/09/2017
ms.author: juliako
ms.openlocfilehash: 963a25b8ba4683a2ce34d9fb0e19499874b4707c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooperform-live-streaming-using-azure-media-services-toocreate-multi-bitrate-streams-with-hello-azure-portal"></a><span data-ttu-id="9b7c9-103">如何 tooperform 即時資料流使用 Azure Media Services toocreate 多位元速率串流以 hello Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="9b7c9-103">How tooperform live streaming using Azure Media Services toocreate multi-bitrate streams with hello Azure portal</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="9b7c9-104">入口網站</span><span class="sxs-lookup"><span data-stu-id="9b7c9-104">Portal</span></span>](media-services-portal-creating-live-encoder-enabled-channel.md)
> * [<span data-ttu-id="9b7c9-105">.NET</span><span class="sxs-lookup"><span data-stu-id="9b7c9-105">.NET</span></span>](media-services-dotnet-creating-live-encoder-enabled-channel.md)
> * [<span data-ttu-id="9b7c9-106">REST API</span><span class="sxs-lookup"><span data-stu-id="9b7c9-106">REST API</span></span>](https://docs.microsoft.com/rest/api/media/operations/channel)
> 
> 

<span data-ttu-id="9b7c9-107">本教學課程將引導您完成 hello 步驟建立的**通道**，接收單一位元速率即時串流，並將其編碼 toomulti 位元速率串流。</span><span class="sxs-lookup"><span data-stu-id="9b7c9-107">This tutorial walks you through hello steps of creating a **Channel** that receives a single-bitrate live stream and encodes it toomulti-bitrate stream.</span></span>

> [!NOTE]
> <span data-ttu-id="9b7c9-108">如需詳細的概念性資訊相關的 tooChannels 啟用即時編碼，請參閱[使用 Azure Media Services toocreate 多位元速率串流的即時串流](media-services-manage-live-encoder-enabled-channels.md)。</span><span class="sxs-lookup"><span data-stu-id="9b7c9-108">For more conceptual information related tooChannels that are enabled for live encoding, see [Live streaming using Azure Media Services toocreate multi-bitrate streams](media-services-manage-live-encoder-enabled-channels.md).</span></span>
> 
> 

## <a name="common-live-streaming-scenario"></a><span data-ttu-id="9b7c9-109">常見即時串流案例</span><span class="sxs-lookup"><span data-stu-id="9b7c9-109">Common Live Streaming Scenario</span></span>
<span data-ttu-id="9b7c9-110">hello 以下是建立通用的即時串流應用程式所需的一般步驟。</span><span class="sxs-lookup"><span data-stu-id="9b7c9-110">hello following are general steps involved in creating common live streaming applications.</span></span>

> [!NOTE]
> <span data-ttu-id="9b7c9-111">目前，最大的 hello 建議即時事件的持續時間是 8 小時。</span><span class="sxs-lookup"><span data-stu-id="9b7c9-111">Currently, hello max recommended duration of a live event is 8 hours.</span></span> <span data-ttu-id="9b7c9-112">請如果您需要 toorun 通道的時間較長的時間，連絡 amslived microsoft.com。</span><span class="sxs-lookup"><span data-stu-id="9b7c9-112">Please contact  amslived at Microsoft.com if you need toorun a Channel for longer periods of time.</span></span>
> 
> 

1. <span data-ttu-id="9b7c9-113">視訊攝影機 tooa 電腦連線。</span><span class="sxs-lookup"><span data-stu-id="9b7c9-113">Connect a video camera tooa computer.</span></span> <span data-ttu-id="9b7c9-114">啟動及設定內部部署即時編碼器可以輸出的其中一種 hello 下列通訊協定的單一位元速率資料流： RTMP、 Smooth Streaming 或 RTP (MPEG-TS)。</span><span class="sxs-lookup"><span data-stu-id="9b7c9-114">Launch and configure an on-premises live encoder that can output a single bitrate stream in one of hello following protocols: RTMP, Smooth Streaming, or RTP (MPEG-TS).</span></span> <span data-ttu-id="9b7c9-115">如需詳細資訊，請參閱 [Azure 媒體服務 RTMP 支援和即時編碼器](http://go.microsoft.com/fwlink/?LinkId=532824)。</span><span class="sxs-lookup"><span data-stu-id="9b7c9-115">For more information, see [Azure Media Services RTMP Support and Live Encoders](http://go.microsoft.com/fwlink/?LinkId=532824).</span></span>
   
    <span data-ttu-id="9b7c9-116">此步驟也可以在您建立通道之後執行。</span><span class="sxs-lookup"><span data-stu-id="9b7c9-116">This step could also be performed after you create your Channel.</span></span>
2. <span data-ttu-id="9b7c9-117">建立並啟動通道。</span><span class="sxs-lookup"><span data-stu-id="9b7c9-117">Create and start a Channel.</span></span> 
3. <span data-ttu-id="9b7c9-118">擷取 hello 通道的內嵌 URL。</span><span class="sxs-lookup"><span data-stu-id="9b7c9-118">Retrieve hello Channel ingest URL.</span></span> 
   
    <span data-ttu-id="9b7c9-119">hello 內嵌 URL 由 hello 即時編碼器 toosend hello 資料流 toohello 通道。</span><span class="sxs-lookup"><span data-stu-id="9b7c9-119">hello ingest URL is used by hello live encoder toosend hello stream toohello Channel.</span></span>
4. <span data-ttu-id="9b7c9-120">擷取 hello 通道預覽 URL。</span><span class="sxs-lookup"><span data-stu-id="9b7c9-120">Retrieve hello Channel preview URL.</span></span> 
   
    <span data-ttu-id="9b7c9-121">使用您的通道可正常接收即時資料流 hello 這個 URL tooverify。</span><span class="sxs-lookup"><span data-stu-id="9b7c9-121">Use this URL tooverify that your channel is properly receiving hello live stream.</span></span>
5. <span data-ttu-id="9b7c9-122">建立事件/程式，此程式也會建立資產。</span><span class="sxs-lookup"><span data-stu-id="9b7c9-122">Create an event/program (that will also create an asset).</span></span> 
6. <span data-ttu-id="9b7c9-123">發行 hello 事件 （會建立 OnDemand 定位器 hello 相關聯的資產）。</span><span class="sxs-lookup"><span data-stu-id="9b7c9-123">Publish hello event (that will create an  OnDemand locator for hello associated asset).</span></span>    
7. <span data-ttu-id="9b7c9-124">啟動 hello 事件，當您準備好 toostart 串流和封存時。</span><span class="sxs-lookup"><span data-stu-id="9b7c9-124">Start hello event when you are ready toostart streaming and archiving.</span></span>
8. <span data-ttu-id="9b7c9-125">（選擇性） hello 即時編碼器可以信號的 toostart 公告。</span><span class="sxs-lookup"><span data-stu-id="9b7c9-125">Optionally, hello live encoder can be signaled toostart an advertisement.</span></span> <span data-ttu-id="9b7c9-126">hello 公告 hello 輸出資料流中插入。</span><span class="sxs-lookup"><span data-stu-id="9b7c9-126">hello advertisement is inserted in hello output stream.</span></span>
9. <span data-ttu-id="9b7c9-127">停止 hello 事件時，您隨時 toostop 串流並封存 hello 事件。</span><span class="sxs-lookup"><span data-stu-id="9b7c9-127">Stop hello event whenever you want toostop streaming and archiving hello event.</span></span>
10. <span data-ttu-id="9b7c9-128">刪除 hello 事件 （並選擇性地刪除 hello 資產）。</span><span class="sxs-lookup"><span data-stu-id="9b7c9-128">Delete hello event (and optionally delete hello asset).</span></span>   

## <a name="in-this-tutorial"></a><span data-ttu-id="9b7c9-129">本教學課程內容</span><span class="sxs-lookup"><span data-stu-id="9b7c9-129">In this tutorial</span></span>
<span data-ttu-id="9b7c9-130">在本教學課程，hello Azure 入口網站是使用的 tooaccomplish hello 下列工作：</span><span class="sxs-lookup"><span data-stu-id="9b7c9-130">In this tutorial, hello Azure portal is used tooaccomplish hello following tasks:</span></span> 

1. <span data-ttu-id="9b7c9-131">建立通道也就啟用的 tooperform 即時編碼。</span><span class="sxs-lookup"><span data-stu-id="9b7c9-131">Create a channel that is enabled tooperform live encoding.</span></span>
2. <span data-ttu-id="9b7c9-132">取得在順序 toosupply hello 內嵌 URL 它 toolive 編碼器。</span><span class="sxs-lookup"><span data-stu-id="9b7c9-132">Get hello Ingest URL in order toosupply it toolive encoder.</span></span> <span data-ttu-id="9b7c9-133">hello 即時編碼器會使用這個 URL tooingest hello 資料流到 hello 通道。</span><span class="sxs-lookup"><span data-stu-id="9b7c9-133">hello live encoder will use this URL tooingest hello stream into hello Channel.</span></span>
3. <span data-ttu-id="9b7c9-134">建立事件/程式 (和資產)。</span><span class="sxs-lookup"><span data-stu-id="9b7c9-134">Create an event/program (and an asset).</span></span>
4. <span data-ttu-id="9b7c9-135">發行 hello 資產，並取得串流 Url。</span><span class="sxs-lookup"><span data-stu-id="9b7c9-135">Publish hello asset and get streaming URLs.</span></span>  
5. <span data-ttu-id="9b7c9-136">播放您的內容。</span><span class="sxs-lookup"><span data-stu-id="9b7c9-136">Play your content.</span></span>
6. <span data-ttu-id="9b7c9-137">清除。</span><span class="sxs-lookup"><span data-stu-id="9b7c9-137">Cleaning up.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="9b7c9-138">必要條件</span><span class="sxs-lookup"><span data-stu-id="9b7c9-138">Prerequisites</span></span>
<span data-ttu-id="9b7c9-139">hello 下面是必要的 toocomplete hello 教學課程。</span><span class="sxs-lookup"><span data-stu-id="9b7c9-139">hello following are required toocomplete hello tutorial.</span></span>

* <span data-ttu-id="9b7c9-140">toocomplete 本教學課程中，您需要 Azure 帳戶。</span><span class="sxs-lookup"><span data-stu-id="9b7c9-140">toocomplete this tutorial, you need an Azure account.</span></span> <span data-ttu-id="9b7c9-141">如果您沒有帳戶，只需要幾分鐘的時間就可以建立免費試用帳戶。</span><span class="sxs-lookup"><span data-stu-id="9b7c9-141">If you don't have an account, you can create a free trial account in just a couple of minutes.</span></span> 
  <span data-ttu-id="9b7c9-142">如需詳細資訊，請參閱 [Azure 免費試用](https://azure.microsoft.com/pricing/free-trial/)。</span><span class="sxs-lookup"><span data-stu-id="9b7c9-142">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="9b7c9-143">媒體服務帳戶。</span><span class="sxs-lookup"><span data-stu-id="9b7c9-143">A Media Services account.</span></span> <span data-ttu-id="9b7c9-144">toocreate Media Services 帳戶，請參閱[建立帳戶](media-services-portal-create-account.md)。</span><span class="sxs-lookup"><span data-stu-id="9b7c9-144">toocreate a Media Services account, see [Create Account](media-services-portal-create-account.md).</span></span>
* <span data-ttu-id="9b7c9-145">網路攝影機以及可以傳送單一位元速率即時串流的編碼器。</span><span class="sxs-lookup"><span data-stu-id="9b7c9-145">A webcam and an encoder that can send a single bitrate live stream.</span></span>

## <a name="create-a-channel"></a><span data-ttu-id="9b7c9-146">建立通道</span><span class="sxs-lookup"><span data-stu-id="9b7c9-146">Create a channel</span></span>
1. <span data-ttu-id="9b7c9-147">在 hello [Azure 入口網站](https://portal.azure.com/)選取 Media Services，然後按一下您的 Media Services 帳戶名稱。</span><span class="sxs-lookup"><span data-stu-id="9b7c9-147">In hello [Azure portal](https://portal.azure.com/), select Media Services and then click on your Media Services account name.</span></span>
2. <span data-ttu-id="9b7c9-148">選取 [即時串流] 。</span><span class="sxs-lookup"><span data-stu-id="9b7c9-148">Select **Live Streaming**.</span></span>
3. <span data-ttu-id="9b7c9-149">選取 [自訂建立] 。</span><span class="sxs-lookup"><span data-stu-id="9b7c9-149">Select **Custom create**.</span></span> <span data-ttu-id="9b7c9-150">此選項可讓您建立通道，而啟用通道即可進行即時編碼。</span><span class="sxs-lookup"><span data-stu-id="9b7c9-150">This option will let you create a channel that is enabled for live encoding.</span></span>
   
    ![建立通道](./media/media-services-portal-creating-live-encoder-enabled-channel/media-services-create-channel.png)
4. <span data-ttu-id="9b7c9-152">按一下 [設定] 。</span><span class="sxs-lookup"><span data-stu-id="9b7c9-152">Click on **Settings**.</span></span>
   
   1. <span data-ttu-id="9b7c9-153">選擇 hello**即時編碼**通道類型。</span><span class="sxs-lookup"><span data-stu-id="9b7c9-153">Choose hello **Live Encoding** channel type.</span></span> <span data-ttu-id="9b7c9-154">此類型指定您想要啟用通道 toocreate 即時編碼。</span><span class="sxs-lookup"><span data-stu-id="9b7c9-154">This type specifies that you want toocreate a Channel that is enabled for live encoding.</span></span> <span data-ttu-id="9b7c9-155">表示 hello 連入的單一位元速率串流會傳送 toohello 通道，並編碼為多位元速率串流，使用指定的即時編碼器設定。</span><span class="sxs-lookup"><span data-stu-id="9b7c9-155">That means hello incoming single bitrate stream is sent toohello Channel and encoded into a multi-bitrate stream using specified live encoder settings.</span></span> <span data-ttu-id="9b7c9-156">如需詳細資訊，請參閱[使用 Azure Media Services toocreate 多位元速率串流的即時串流](media-services-manage-live-encoder-enabled-channels.md)。</span><span class="sxs-lookup"><span data-stu-id="9b7c9-156">For more information, see [Live streaming using Azure Media Services toocreate multi-bitrate streams](media-services-manage-live-encoder-enabled-channels.md).</span></span> <span data-ttu-id="9b7c9-157">按一下 [確定]。</span><span class="sxs-lookup"><span data-stu-id="9b7c9-157">Click OK.</span></span>
   2. <span data-ttu-id="9b7c9-158">指定通道的名稱。</span><span class="sxs-lookup"><span data-stu-id="9b7c9-158">Specify a channel's name.</span></span>
   3. <span data-ttu-id="9b7c9-159">按一下 [確定] 在 hello 囉 」 畫面底部。</span><span class="sxs-lookup"><span data-stu-id="9b7c9-159">Click OK at hello bottom of hello screen.</span></span>
5. <span data-ttu-id="9b7c9-160">選取 hello**內嵌** 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="9b7c9-160">Select hello **Ingest** tab.</span></span>
   
   1. <span data-ttu-id="9b7c9-161">在這個頁面上，您可以選取串流通訊協定。</span><span class="sxs-lookup"><span data-stu-id="9b7c9-161">On this page, you can select a streaming protocol.</span></span> <span data-ttu-id="9b7c9-162">Hello**即時編碼**通道類型，有效的通訊協定選項為：</span><span class="sxs-lookup"><span data-stu-id="9b7c9-162">For hello **Live Encoding** channel type, valid protocol options are:</span></span>
      
      * <span data-ttu-id="9b7c9-163">單一位元速率的分散 MP4 (Smooth Streaming)</span><span class="sxs-lookup"><span data-stu-id="9b7c9-163">Single bitrate Fragmented MP4 (Smooth Streaming)</span></span>
      * <span data-ttu-id="9b7c9-164">單一位元速率 RTMP</span><span class="sxs-lookup"><span data-stu-id="9b7c9-164">Single bitrate RTMP</span></span>
      * <span data-ttu-id="9b7c9-165">RTP (MPEG-TS)：透過 RTP 的 MPEG-2 傳輸串流。</span><span class="sxs-lookup"><span data-stu-id="9b7c9-165">RTP (MPEG-TS): MPEG-2 Transport Stream over RTP.</span></span>
        
        <span data-ttu-id="9b7c9-166">如需有關每個通訊協定的詳細說明，請參閱[使用 Azure Media Services toocreate 多位元速率串流的即時串流](media-services-manage-live-encoder-enabled-channels.md)。</span><span class="sxs-lookup"><span data-stu-id="9b7c9-166">For detailed explanation about each protocol, see [Live streaming using Azure Media Services toocreate multi-bitrate streams](media-services-manage-live-encoder-enabled-channels.md).</span></span>
        
        <span data-ttu-id="9b7c9-167">您無法變更 hello hello 通道時的通訊協定選項，或其相關聯的事件/程式正在執行。</span><span class="sxs-lookup"><span data-stu-id="9b7c9-167">You cannot change hello protocol option while hello Channel or its associated events/programs are running.</span></span> <span data-ttu-id="9b7c9-168">如果您需要不同的通訊協定，則應該為每個串流通訊協定建立個別的通道。</span><span class="sxs-lookup"><span data-stu-id="9b7c9-168">If you require different protocols, you should create separate channels for each streaming protocol.</span></span>  
   2. <span data-ttu-id="9b7c9-169">您可以在 hello 套用 IP 限制內嵌。</span><span class="sxs-lookup"><span data-stu-id="9b7c9-169">You can apply IP restriction on hello ingest.</span></span> 
      
       <span data-ttu-id="9b7c9-170">您可以定義 hello IP 位址允許 tooingest 視訊 toothis 通道。</span><span class="sxs-lookup"><span data-stu-id="9b7c9-170">You can define hello IP addresses that are allowed tooingest a video toothis channel.</span></span> <span data-ttu-id="9b7c9-171">允許的 IP 位址可以指定為單一 IP 位址 (例如'10.0.0.1')、使用 IP 位址和 CIDR 子網路遮罩的 IP 範圍 (例如'10.0.0.1/22’)，或使用 IP 位址和以點分隔十進位子網路遮罩的 IP 範圍 (例如'10.0.0.1(255.255.252.0)')。</span><span class="sxs-lookup"><span data-stu-id="9b7c9-171">Allowed IP addresses can be specified as either a single IP address (e.g. '10.0.0.1'), an IP range using an IP address and a CIDR subnet mask (e.g. '10.0.0.1/22'), or an IP range using an IP address and a dotted decimal subnet mask (e.g. '10.0.0.1(255.255.252.0)').</span></span>
      
       <span data-ttu-id="9b7c9-172">如果未指定 IP 位址，而且沒有任何規則定義，則不允許任何 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="9b7c9-172">If no IP addresses are specified and there is no rule definition then no IP address will be allowed.</span></span> <span data-ttu-id="9b7c9-173">tooallow 任何 IP 位址，建立一個規則，並設定 0.0.0.0/0。</span><span class="sxs-lookup"><span data-stu-id="9b7c9-173">tooallow any IP address, create a rule and set 0.0.0.0/0.</span></span>
6. <span data-ttu-id="9b7c9-174">在 hello**預覽**索引標籤上，套用 hello preview 上的 IP 限制。</span><span class="sxs-lookup"><span data-stu-id="9b7c9-174">On hello **Preview** tab, apply IP restriction on hello preview.</span></span>
7. <span data-ttu-id="9b7c9-175">在 hello**編碼**索引標籤上，指定 hello 編碼預設。</span><span class="sxs-lookup"><span data-stu-id="9b7c9-175">On hello **Encoding** tab, specify hello encoding preset.</span></span> 
   
    <span data-ttu-id="9b7c9-176">目前，hello 只有系統是的預設您可以選取**預設 720p**。</span><span class="sxs-lookup"><span data-stu-id="9b7c9-176">Currently, hello only system preset you can select is **Default 720p**.</span></span> <span data-ttu-id="9b7c9-177">toospecify 自訂預設值，請開啟 Microsoft 支援票證。</span><span class="sxs-lookup"><span data-stu-id="9b7c9-177">toospecify a custom preset, open a Microsoft support ticket.</span></span> <span data-ttu-id="9b7c9-178">然後，輸入 hello hello 名稱為您建立的預設值。</span><span class="sxs-lookup"><span data-stu-id="9b7c9-178">Then, enter hello name of hello preset created for you.</span></span> 

> [!NOTE]
> <span data-ttu-id="9b7c9-179">目前，hello 通道開始可能會佔用 too30 分鐘。</span><span class="sxs-lookup"><span data-stu-id="9b7c9-179">Currently, hello Channel start can take up too30 minutes.</span></span> <span data-ttu-id="9b7c9-180">重設通道可能會佔用 too5 分鐘。</span><span class="sxs-lookup"><span data-stu-id="9b7c9-180">Channel reset can take up too5 minutes.</span></span>
> 
> 

<span data-ttu-id="9b7c9-181">一旦您建立 hello 通道時，您可以按一下 hello 通道，然後選取**設定**，您可以在其中檢視通道組態。</span><span class="sxs-lookup"><span data-stu-id="9b7c9-181">Once you created hello Channel, you can click on hello channel and select **Settings** where you can view your channels configurations.</span></span> 

<span data-ttu-id="9b7c9-182">如需詳細資訊，請參閱[使用 Azure Media Services toocreate 多位元速率串流的即時串流](media-services-manage-live-encoder-enabled-channels.md)。</span><span class="sxs-lookup"><span data-stu-id="9b7c9-182">For more information, see [Live streaming using Azure Media Services toocreate multi-bitrate streams](media-services-manage-live-encoder-enabled-channels.md).</span></span>

## <a name="get-ingest-urls"></a><span data-ttu-id="9b7c9-183">取得內嵌 URL</span><span class="sxs-lookup"><span data-stu-id="9b7c9-183">Get ingest URLs</span></span>
<span data-ttu-id="9b7c9-184">一旦建立 hello 通道之後，您可以取得內嵌您將會提供 toohello 即時編碼器的 Url。</span><span class="sxs-lookup"><span data-stu-id="9b7c9-184">Once hello channel is created, you can get ingest URLs that you will provide toohello live encoder.</span></span> <span data-ttu-id="9b7c9-185">hello 編碼器使用這些 Url tooinput 即時資料流。</span><span class="sxs-lookup"><span data-stu-id="9b7c9-185">hello encoder uses these URLs tooinput a live stream.</span></span>

![ingesturls](./media/media-services-portal-creating-live-encoder-enabled-channel/media-services-ingest-urls.png)

## <a name="create-and-manage-events"></a><span data-ttu-id="9b7c9-187">建立和管理事件</span><span class="sxs-lookup"><span data-stu-id="9b7c9-187">Create and manage events</span></span>
### <a name="overview"></a><span data-ttu-id="9b7c9-188">概觀</span><span class="sxs-lookup"><span data-stu-id="9b7c9-188">Overview</span></span>
<span data-ttu-id="9b7c9-189">通道是 toocontrol hello 發行和即時串流片段的儲存體可讓您的事件/程式相關聯。</span><span class="sxs-lookup"><span data-stu-id="9b7c9-189">A channel is associated with events/programs that enable you toocontrol hello publishing and storage of segments in a live stream.</span></span> <span data-ttu-id="9b7c9-190">通道會管理事件/程式。</span><span class="sxs-lookup"><span data-stu-id="9b7c9-190">Channels manage events/programs.</span></span> <span data-ttu-id="9b7c9-191">hello 通道和程式的關聯性是內容的非常類似 tootraditional 媒體其中通道具有常數資料流，而程式是內容的該頻道上的已設定領域的 toosome 逾時事件。</span><span class="sxs-lookup"><span data-stu-id="9b7c9-191">hello Channel and Program relationship is very similar tootraditional media where a channel has a constant stream of content and a program is scoped toosome timed event on that channel.</span></span>

<span data-ttu-id="9b7c9-192">您可以指定您想要 tooretain hello 記錄內容 hello 事件設定 hello 的 hello 數**封存時間長度**長度。</span><span class="sxs-lookup"><span data-stu-id="9b7c9-192">You can specify hello number of hours you want tooretain hello recorded content for hello event by setting hello **Archive Window** length.</span></span> <span data-ttu-id="9b7c9-193">這個值可以設定為 5 分鐘 tooa 最多 25 個小時的最小值。</span><span class="sxs-lookup"><span data-stu-id="9b7c9-193">This value can be set from a minimum of 5 minutes tooa maximum of 25 hours.</span></span> <span data-ttu-id="9b7c9-194">封存時間長度也會規定 hello 最大用戶端可以從 hello 目前即時位置搜尋的時間量。</span><span class="sxs-lookup"><span data-stu-id="9b7c9-194">Archive window length also dictates hello maximum amount of time clients can seek back in time from hello current live position.</span></span> <span data-ttu-id="9b7c9-195">事件可以透過 hello 指定時間內，執行但落後 hello 時間長度的內容會持續遭到捨棄。</span><span class="sxs-lookup"><span data-stu-id="9b7c9-195">Events can run over hello specified amount of time, but content that falls behind hello window length is continuously discarded.</span></span> <span data-ttu-id="9b7c9-196">這個屬性的值也會決定資訊清單所能成長的時間長度 hello 用戶端。</span><span class="sxs-lookup"><span data-stu-id="9b7c9-196">This value of this property also determines how long hello client manifests can grow.</span></span>

<span data-ttu-id="9b7c9-197">每個事件都是與資產相關聯。</span><span class="sxs-lookup"><span data-stu-id="9b7c9-197">Each event is associated with an Asset.</span></span> <span data-ttu-id="9b7c9-198">您必須建立 OnDemand 定位器 hello toopublish hello 事件相關聯的資產。</span><span class="sxs-lookup"><span data-stu-id="9b7c9-198">toopublish hello event you must create an OnDemand locator for hello associated asset.</span></span> <span data-ttu-id="9b7c9-199">擁有這個定位器，可讓您 toobuild 您可以提供 tooyour 用戶端的串流 URL。</span><span class="sxs-lookup"><span data-stu-id="9b7c9-199">Having this locator will enable you toobuild a streaming URL that you can provide tooyour clients.</span></span>

<span data-ttu-id="9b7c9-200">一個通道可支援同時執行的事件，因此您可以建立多個封存 hello toothree 註冊相同的傳入資料流。</span><span class="sxs-lookup"><span data-stu-id="9b7c9-200">A channel supports up toothree concurrently running events so you can create multiple archives of hello same incoming stream.</span></span> <span data-ttu-id="9b7c9-201">這可讓您 toopublish 和封存的事件所需的不同部分。</span><span class="sxs-lookup"><span data-stu-id="9b7c9-201">This allows you toopublish and archive different parts of an event as needed.</span></span> <span data-ttu-id="9b7c9-202">例如，您的商務需求是 tooarchive 6 小時的事件，但是 toobroadcast 最後的 10 分鐘。</span><span class="sxs-lookup"><span data-stu-id="9b7c9-202">For example, your business requirement is tooarchive 6 hours of an event, but toobroadcast only last 10 minutes.</span></span> <span data-ttu-id="9b7c9-203">tooaccomplish，您需要 toocreate 兩個同時執行事件。</span><span class="sxs-lookup"><span data-stu-id="9b7c9-203">tooaccomplish this, you need toocreate two concurrently running event.</span></span> <span data-ttu-id="9b7c9-204">一個事件設定 tooarchive 6 小時的 hello 事件但 hello 程式不會發行。</span><span class="sxs-lookup"><span data-stu-id="9b7c9-204">One event is set tooarchive 6 hours of hello event but hello program is not published.</span></span> <span data-ttu-id="9b7c9-205">hello 其他事件的集合 tooarchive 為 10 分鐘並發佈此程式。</span><span class="sxs-lookup"><span data-stu-id="9b7c9-205">hello other event is set tooarchive for 10 minutes and this program is published.</span></span>

<span data-ttu-id="9b7c9-206">您不應該將現有程式重複用於新的事件。</span><span class="sxs-lookup"><span data-stu-id="9b7c9-206">You should not reuse existing programs for new events.</span></span> <span data-ttu-id="9b7c9-207">而是針對每個事件建立並啟動新的程式。</span><span class="sxs-lookup"><span data-stu-id="9b7c9-207">Instead, create and start a new program for each event.</span></span>

<span data-ttu-id="9b7c9-208">當您準備好 toostart 串流和封存時啟動事件/程式。</span><span class="sxs-lookup"><span data-stu-id="9b7c9-208">Start an event/program when you are ready toostart streaming and archiving.</span></span> <span data-ttu-id="9b7c9-209">停止 hello 事件時，您隨時 toostop 串流並封存 hello 事件。</span><span class="sxs-lookup"><span data-stu-id="9b7c9-209">Stop hello event whenever you want toostop streaming and archiving hello event.</span></span> 

<span data-ttu-id="9b7c9-210">toodelete 封存內容時，會停止和刪除 hello 事件，然後再刪除 hello 相關聯的資產。</span><span class="sxs-lookup"><span data-stu-id="9b7c9-210">toodelete archived content, stop and delete hello event and then delete hello associated asset.</span></span> <span data-ttu-id="9b7c9-211">無法刪除資產，如果它由 hello 事件。必須先刪除 hello 事件。</span><span class="sxs-lookup"><span data-stu-id="9b7c9-211">An asset cannot be deleted if it is used by hello event; hello event must be deleted first.</span></span> 

<span data-ttu-id="9b7c9-212">即使您停止並刪除 hello 事件之後，hello 使用者是無法 toostream 封存的內容，視視訊，只要您不要刪除 hello 資產。</span><span class="sxs-lookup"><span data-stu-id="9b7c9-212">Even after you stop and delete hello event, hello users would be able toostream your archived content as a video on demand, for as long as you do not delete hello asset.</span></span>

<span data-ttu-id="9b7c9-213">若要封存的 tooretain hello 內容，而不是需要它提供給串流，刪除 hello 串流定位器。</span><span class="sxs-lookup"><span data-stu-id="9b7c9-213">If you do want tooretain hello archived content, but not have it available for streaming, delete hello streaming locator.</span></span>

### <a name="createstartstop-events"></a><span data-ttu-id="9b7c9-214">建立/啟動/停止事件</span><span class="sxs-lookup"><span data-stu-id="9b7c9-214">Create/start/stop events</span></span>
<span data-ttu-id="9b7c9-215">一旦您擁有 hello 資料流流入 hello 通道就可以開始建立資產、 程式和串流定位器串流處理事件的 hello。</span><span class="sxs-lookup"><span data-stu-id="9b7c9-215">Once you have hello stream flowing into hello Channel you can begin hello streaming event by creating an Asset, Program, and Streaming Locator.</span></span> <span data-ttu-id="9b7c9-216">這將會封存 hello 資料流，並讓它使用 tooviewers 透過 hello 串流端點。</span><span class="sxs-lookup"><span data-stu-id="9b7c9-216">This will archive hello stream and make it available tooviewers through hello Streaming Endpoint.</span></span> 

>[!NOTE]
><span data-ttu-id="9b7c9-217">AMS 帳戶建立時**預設**串流端點就會加入 tooyour 帳戶 hello**已停止**狀態。</span><span class="sxs-lookup"><span data-stu-id="9b7c9-217">When your AMS account is created a **default** streaming endpoint is added tooyour account in hello **Stopped** state.</span></span> <span data-ttu-id="9b7c9-218">串流處理您的內容，並採取利用動態封裝和動態加密，toostart hello 串流端點，您想要從中 toostream 內容已經在 hello toobe**執行**狀態。</span><span class="sxs-lookup"><span data-stu-id="9b7c9-218">toostart streaming your content and take advantage of dynamic packaging and dynamic encryption, hello streaming endpoint from which you want toostream content has toobe in hello **Running** state.</span></span> 

<span data-ttu-id="9b7c9-219">有兩種方式 toostart 事件：</span><span class="sxs-lookup"><span data-stu-id="9b7c9-219">There are two ways toostart event:</span></span> 

1. <span data-ttu-id="9b7c9-220">從 hello**通道**頁面上，按**即時事件**tooadd 新的事件。</span><span class="sxs-lookup"><span data-stu-id="9b7c9-220">From hello **Channel** page, press **Live Event** tooadd a new event.</span></span>
   
    <span data-ttu-id="9b7c9-221">指定：事件名稱、資產名稱、封存時間範圍和加密選項。</span><span class="sxs-lookup"><span data-stu-id="9b7c9-221">Specify: event name, asset name, archive window, and encryption option.</span></span>
   
    ![createprogram](./media/media-services-portal-creating-live-encoder-enabled-channel/media-services-create-program.png)
   
    <span data-ttu-id="9b7c9-223">如果您保留**立即發行這個即時事件**核取，hello 事件 hello 發行 Url 將會建立。</span><span class="sxs-lookup"><span data-stu-id="9b7c9-223">If you left **Publish this live event now** checked, hello event hello PUBLISHING URLs will get created.</span></span>
   
    <span data-ttu-id="9b7c9-224">您可以按**啟動**，當您準備好 toostream hello 事件。</span><span class="sxs-lookup"><span data-stu-id="9b7c9-224">You can press **Start**, whenever you are ready toostream hello event.</span></span>
   
    <span data-ttu-id="9b7c9-225">一旦您開始 hello 事件時，您可以按**監看式**toostart 播放 hello 內容。</span><span class="sxs-lookup"><span data-stu-id="9b7c9-225">Once you start hello event, you can press **Watch** toostart playing hello content.</span></span>
2. <span data-ttu-id="9b7c9-226">或者，您可以使用捷徑，並按**Go Live**按鈕 hello**通道**頁面。</span><span class="sxs-lookup"><span data-stu-id="9b7c9-226">Alternatively, you can use a shortcut and press **Go Live** button on hello **Channel** page.</span></span> <span data-ttu-id="9b7c9-227">這樣會建立預設「資產」、「程式」和「串流定位器」。</span><span class="sxs-lookup"><span data-stu-id="9b7c9-227">This will create a default Asset, Program, and Streaming Locator.</span></span>
   
    <span data-ttu-id="9b7c9-228">hello 事件命名為**預設**而且 hello 封存時間長度會設定 too8 小時。</span><span class="sxs-lookup"><span data-stu-id="9b7c9-228">hello event is named **default** and hello archive window is set too8 hours.</span></span>

<span data-ttu-id="9b7c9-229">您可以觀看 hello 已發行的事件從 hello**即時事件**頁面。</span><span class="sxs-lookup"><span data-stu-id="9b7c9-229">You can watch hello published event from hello **Live event** page.</span></span> 

<span data-ttu-id="9b7c9-230">如果您按一下 [停止播放] ，則會停止所有的即時事件。</span><span class="sxs-lookup"><span data-stu-id="9b7c9-230">If you click **Off Air**, it will stop all live events.</span></span> 

## <a name="watch-hello-event"></a><span data-ttu-id="9b7c9-231">監看式 hello 事件</span><span class="sxs-lookup"><span data-stu-id="9b7c9-231">Watch hello event</span></span>
<span data-ttu-id="9b7c9-232">toowatch hello 事件中，按一下 **監看式**在 hello Azure 入口網站 或 複製 hello 串流 URL，並使用您選擇的播放程式。</span><span class="sxs-lookup"><span data-stu-id="9b7c9-232">toowatch hello event, click **Watch** in hello Azure portal or copy hello streaming URL and use a player of your choice.</span></span> 

![建立時間](./media/media-services-portal-creating-live-encoder-enabled-channel/media-services-play-event.png)

<span data-ttu-id="9b7c9-234">實況事件會自動將事件 tooon 要求內容時停止。</span><span class="sxs-lookup"><span data-stu-id="9b7c9-234">Live event automatically converts events tooon-demand content when stopped.</span></span>

## <a name="clean-up"></a><span data-ttu-id="9b7c9-235">清除</span><span class="sxs-lookup"><span data-stu-id="9b7c9-235">Clean up</span></span>
<span data-ttu-id="9b7c9-236">如果您完成資料流的事件，而且想 tooclean hello 資源佈建之前，請依照下列程序的 hello。</span><span class="sxs-lookup"><span data-stu-id="9b7c9-236">If you are done streaming events and want tooclean up hello resources provisioned earlier, follow hello following procedure.</span></span>

* <span data-ttu-id="9b7c9-237">停止從 hello 編碼器發送 hello 資料流。</span><span class="sxs-lookup"><span data-stu-id="9b7c9-237">Stop pushing hello stream from hello encoder.</span></span>
* <span data-ttu-id="9b7c9-238">停止 hello 通道。</span><span class="sxs-lookup"><span data-stu-id="9b7c9-238">Stop hello channel.</span></span> <span data-ttu-id="9b7c9-239">一旦停止 hello 通道時，它將不會產生任何費用。</span><span class="sxs-lookup"><span data-stu-id="9b7c9-239">Once hello Channel is stopped, it will not incur any charges.</span></span> <span data-ttu-id="9b7c9-240">當您需要 toostart 同樣地，它會有 hello 相同內嵌 URL，您不需要 tooreconfigure 您的編碼器。</span><span class="sxs-lookup"><span data-stu-id="9b7c9-240">When you need toostart it again, it will have hello same ingest URL so you won't need tooreconfigure your encoder.</span></span>
* <span data-ttu-id="9b7c9-241">您可以停止串流端點，除非您想為點播串流即時事件的 toocontinue tooprovide hello 封存。</span><span class="sxs-lookup"><span data-stu-id="9b7c9-241">You can stop your Streaming Endpoint, unless you want toocontinue tooprovide hello archive of your live event as an on-demand stream.</span></span> <span data-ttu-id="9b7c9-242">如果 hello 通道處於停止狀態，它將不會產生任何費用。</span><span class="sxs-lookup"><span data-stu-id="9b7c9-242">If hello channel is in stopped state, it will not incur any charges.</span></span>

## <a name="view-archived-content"></a><span data-ttu-id="9b7c9-243">檢視封存的內容</span><span class="sxs-lookup"><span data-stu-id="9b7c9-243">View archived content</span></span>
<span data-ttu-id="9b7c9-244">即使您停止並刪除 hello 事件之後，hello 使用者是無法 toostream 封存的內容，視視訊，只要您不要刪除 hello 資產。</span><span class="sxs-lookup"><span data-stu-id="9b7c9-244">Even after you stop and delete hello event, hello users would be able toostream your archived content as a video on demand, for as long as you do not delete hello asset.</span></span> <span data-ttu-id="9b7c9-245">無法刪除資產，如果它由事件。必須先刪除 hello 事件。</span><span class="sxs-lookup"><span data-stu-id="9b7c9-245">An asset cannot be deleted if it is used by an event; hello event must be deleted first.</span></span> 

<span data-ttu-id="9b7c9-246">您的資產，選取 toomanage**設定**按一下**資產**。</span><span class="sxs-lookup"><span data-stu-id="9b7c9-246">toomanage your assets, select **Setting** and click **Assets**.</span></span>

![Assets](./media/media-services-portal-creating-live-encoder-enabled-channel/media-services-assets.png)

## <a name="considerations"></a><span data-ttu-id="9b7c9-248">考量</span><span class="sxs-lookup"><span data-stu-id="9b7c9-248">Considerations</span></span>
* <span data-ttu-id="9b7c9-249">目前，最大的 hello 建議即時事件的持續時間是 8 小時。</span><span class="sxs-lookup"><span data-stu-id="9b7c9-249">Currently, hello max recommended duration of a live event is 8 hours.</span></span> <span data-ttu-id="9b7c9-250">請如果您需要 toorun 通道的時間較長的時間，連絡 amslived microsoft.com。</span><span class="sxs-lookup"><span data-stu-id="9b7c9-250">Please contact amslived at Microsoft.com if you need toorun a Channel for longer periods of time.</span></span>
* <span data-ttu-id="9b7c9-251">請確定將內容串流的端點要從中 toostream hello 處於 hello**執行**狀態。</span><span class="sxs-lookup"><span data-stu-id="9b7c9-251">Make sure hello streaming endpoint from which you want toostream  your content is in hello **Running** state.</span></span>

## <a name="next-step"></a><span data-ttu-id="9b7c9-252">後續步驟</span><span class="sxs-lookup"><span data-stu-id="9b7c9-252">Next step</span></span>
<span data-ttu-id="9b7c9-253">檢閱媒體服務學習路徑。</span><span class="sxs-lookup"><span data-stu-id="9b7c9-253">Review Media Services learning paths.</span></span>

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="9b7c9-254">提供意見反應</span><span class="sxs-lookup"><span data-stu-id="9b7c9-254">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

