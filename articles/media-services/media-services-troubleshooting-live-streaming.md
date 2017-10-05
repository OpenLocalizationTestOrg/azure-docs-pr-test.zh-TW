---
title: "為即時串流而設的疑難排解指南 | Microsoft Docs"
description: "本主題提供有關如何疑難排解即時資料流問題的建議。"
services: media-services
documentationcenter: 
author: juliako
manager: cfowler
editor: 
ms.assetid: 3a7f6c1d-ce57-4fa4-a7a6-edb526b3ffbf
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/20/2017
ms.author: juliako
ms.openlocfilehash: fa91baf7c494941fccf0e6ca38b930f3c2a521ce
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="troubleshooting-guide-for-live-streaming"></a><span data-ttu-id="606d0-103">為即時串流而設的疑難排解指南</span><span class="sxs-lookup"><span data-stu-id="606d0-103">Troubleshooting guide for live streaming</span></span>
<span data-ttu-id="606d0-104">本主題提供有關如何疑難排解某些即時資料流問題的建議。</span><span class="sxs-lookup"><span data-stu-id="606d0-104">This topic gives suggestions on how to troubleshoot some live streaming problems.</span></span>

## <a name="issues-related-to-on-premises-encoders"></a><span data-ttu-id="606d0-105">內部部署編碼器的相關問題</span><span class="sxs-lookup"><span data-stu-id="606d0-105">Issues related to on-premises encoders</span></span>
<span data-ttu-id="606d0-106">本節提供如何疑難排解內部部署編碼器相關問題的建議，而編碼器的設定是傳送單一位元速率資料流到啟用即時編碼的 AMS 通道。</span><span class="sxs-lookup"><span data-stu-id="606d0-106">This section gives suggestions on how to troubleshoot problems related to on-premises encoders that are configured to send a single bitrate stream to AMS channels that are enabled for live encoding.</span></span>

### <a name="problem-would-like-to-see-logs"></a><span data-ttu-id="606d0-107">問題：想要查看記錄檔</span><span class="sxs-lookup"><span data-stu-id="606d0-107">Problem: Would like to see logs</span></span>
* <span data-ttu-id="606d0-108">潛在問題：找不到可能有助於偵錯問題的編碼器記錄檔。</span><span class="sxs-lookup"><span data-stu-id="606d0-108">**Potential issue**: Can't find encoder logs that might help in debugging issues.</span></span>
  
  * <span data-ttu-id="606d0-109">**Telestream Wirecas**：您通常可以在 C:\Users\{使用者名稱}\AppData\Roaming\Wirecast\ 下找到記錄檔</span><span class="sxs-lookup"><span data-stu-id="606d0-109">**Telestream Wirecast**: You can usually find logs under C:\Users\{username}\AppData\Roaming\Wirecast\\</span></span> 
  * <span data-ttu-id="606d0-110">︰您可在管理入口網站上找到記錄檔連結。</span><span class="sxs-lookup"><span data-stu-id="606d0-110">**Elemental Live**: You can find has links to logs on the management portal.</span></span> <span data-ttu-id="606d0-111">依序按一下 [統計] 及 [記錄檔]。</span><span class="sxs-lookup"><span data-stu-id="606d0-111">Click on **Stats**, then **Logs**.</span></span> <span data-ttu-id="606d0-112">在 [記錄檔]  頁面上，您會看到一份所有 LiveEvent 項目的記錄檔清單，請選取符合您目前工作階段的項目。</span><span class="sxs-lookup"><span data-stu-id="606d0-112">On the **Log Files** page, you will see a list of logs for all the LiveEvent items; select the one matching your current session.</span></span> 
  * <span data-ttu-id="606d0-113">**Flash Media Live Encoder**︰瀏覽至 [編碼記錄檔] 索引標籤即可找到 [記錄檔目錄...]。</span><span class="sxs-lookup"><span data-stu-id="606d0-113">**Flash Media Live Encoder**: You can find the **Log Directory...** by navigating to the **Encoding Log** tab.</span></span>

### <a name="problem-there-is-no-option-for-outputting-a-progressive-stream"></a><span data-ttu-id="606d0-114">問題：沒有輸出漸進式資料流的選項</span><span class="sxs-lookup"><span data-stu-id="606d0-114">Problem: There is no option for outputting a progressive stream</span></span>
* <span data-ttu-id="606d0-115">**可能的問題**：使用的編碼器不會自動進行非交錯處理。</span><span class="sxs-lookup"><span data-stu-id="606d0-115">**Potential issue**: The encoder being used doesn't automatically deinterlace.</span></span> 
  
    <span data-ttu-id="606d0-116">**疑難排解步驟**：尋找編碼器介面中的非交錯處理選項。</span><span class="sxs-lookup"><span data-stu-id="606d0-116">**Troubleshooting steps**: Look for a de-interlacing option within the encoder interface.</span></span> <span data-ttu-id="606d0-117">一旦啟用非交錯處理，請再次檢查漸進式的輸出設定。</span><span class="sxs-lookup"><span data-stu-id="606d0-117">Once de-interlacing is enabled, check again for progressive output settings.</span></span> 

### <a name="problem-tried-several-encoder-output-settings-and-still-unable-to-connect"></a><span data-ttu-id="606d0-118">問題：已嘗試數種編碼器輸出設定，但仍然無法連線。</span><span class="sxs-lookup"><span data-stu-id="606d0-118">Problem: Tried several encoder output settings and still unable to connect.</span></span>
* <span data-ttu-id="606d0-119">**可能的問題**：未正確重設 Azure 編碼通道。</span><span class="sxs-lookup"><span data-stu-id="606d0-119">**Potential issue**: Azure encoding channel was not properly reset.</span></span> 
  
    <span data-ttu-id="606d0-120">**疑難排解步驟**：確定編碼器不再推播至 AMS，停止並重設通道。</span><span class="sxs-lookup"><span data-stu-id="606d0-120">**Troubleshooting steps**: Make sure the encoder is no longer pushing to AMS, stop and reset the channel.</span></span> <span data-ttu-id="606d0-121">再次執行後，請嘗試使用新的設定連線至您的編碼器。</span><span class="sxs-lookup"><span data-stu-id="606d0-121">Once running again, try connecting your encoder with the new settings.</span></span> <span data-ttu-id="606d0-122">有時候，通道在經過幾次失敗的嘗試後可能會損毀，如果這樣仍無法更正問題，請嘗試建立新通道。</span><span class="sxs-lookup"><span data-stu-id="606d0-122">If this still does not correct the issue, try creating a new channel entirely, sometimes channels can become corrupt after several failed attempts.</span></span>  
* <span data-ttu-id="606d0-123">**可能的問題**：GOP 大小或主要畫面設定不佳。</span><span class="sxs-lookup"><span data-stu-id="606d0-123">**Potential issue**: The GOP size or key frame settings are not optimal.</span></span> 
  
    <span data-ttu-id="606d0-124">**疑難排解步驟**：建議的 GOP 大小或主要畫面間隔為 2 秒。</span><span class="sxs-lookup"><span data-stu-id="606d0-124">**Troubleshooting steps**: Recommended GOP size or keyframe interval is 2 seconds.</span></span> <span data-ttu-id="606d0-125">某些編碼器以畫面數目計算此設定，某些則使用秒。</span><span class="sxs-lookup"><span data-stu-id="606d0-125">Some encoders calculate this setting in number of frames, while others use seconds.</span></span> <span data-ttu-id="606d0-126">例如：輸出 30fps 時，GOP 大小會是 60 個畫面，相當於 2 秒。</span><span class="sxs-lookup"><span data-stu-id="606d0-126">For example: When outputting 30fps, the GOP size would be 60 frames, which is equivalent to 2 seconds.</span></span>  
* <span data-ttu-id="606d0-127">**可能的問題**：關閉的連接埠封鎖資料流。</span><span class="sxs-lookup"><span data-stu-id="606d0-127">**Potential issue**: Closed ports are blocking the stream.</span></span> 
  
    <span data-ttu-id="606d0-128">**疑難排解步驟**：透過 RTMP 串流處理時，請檢查防火牆和/或 Proxy 設定，確認輸出連接埠 1935 和 1936 已開啟。</span><span class="sxs-lookup"><span data-stu-id="606d0-128">**Troubleshooting steps**: When streaming via RTMP, check firewall and/or proxy settings to confirm that outbound ports 1935 and 1936 are open.</span></span> <span data-ttu-id="606d0-129">使用 RTP 資料流時，請確認輸出連接埠 2010 已開啟。</span><span class="sxs-lookup"><span data-stu-id="606d0-129">When using RTP streaming, confirm that outbound port 2010 is open.</span></span> 

### <a name="problem-when-configuring-the-encoder-to-stream-with-the-rtp-protocol-there-is-no-place-to-enter-a-host-name"></a><span data-ttu-id="606d0-130">問題：設定編碼器使用 RTP 通訊協定串流處理時，沒有輸入主機名稱的位置。</span><span class="sxs-lookup"><span data-stu-id="606d0-130">Problem: When configuring the encoder to stream with the RTP protocol, there is no place to enter a host name.</span></span>
* <span data-ttu-id="606d0-131">**可能的問題**：許多 RTP 編碼器未考慮到主機名稱，必須取得 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="606d0-131">**Potential issue**: Many RTP encoders do not allow for host names, and an IP address will need to be acquired.</span></span>  
  
    <span data-ttu-id="606d0-132">**疑難排解步驟**：若要尋找 IP 位址，請在任一電腦上開啟命令提示字元。</span><span class="sxs-lookup"><span data-stu-id="606d0-132">**Troubleshooting steps**: To find the IP address, open a command prompt on any computer.</span></span> <span data-ttu-id="606d0-133">若要在 Windows 中執行此操作，請開啟「執行」啟動程式 (WIN + R) 並輸入 "cmd" 來開啟。</span><span class="sxs-lookup"><span data-stu-id="606d0-133">To do this in Windows, open the Run launcher (WIN + R) and type “cmd” to open.</span></span>  
  
    <span data-ttu-id="606d0-134">命令提示字元開啟後，輸入 "Ping [AMS 主機名稱]"。</span><span class="sxs-lookup"><span data-stu-id="606d0-134">Once the command prompt is open, type "Ping [AMS Host Name]".</span></span> 
  
    <span data-ttu-id="606d0-135">藉由省略 Azure 內嵌 URL 中的連接埠號碼，即可衍生主機名稱，如以下範例中反白的部分所示：</span><span class="sxs-lookup"><span data-stu-id="606d0-135">The host name can be derived by omitting the port number from the Azure Ingest URL, as highlighted in the following example:</span></span> 
  
    <span data-ttu-id="606d0-136">rtp://test2-amstest009.rtp.channel.mediaservices.windows.net:2010/</span><span class="sxs-lookup"><span data-stu-id="606d0-136">rtp://test2-amstest009.rtp.channel.mediaservices.windows.net:2010/</span></span> 
  
    ![fmle](./media/media-services-fmle-live-encoder/media-services-fmle10.png)

> [!NOTE]
> <span data-ttu-id="606d0-138">如果依循下列疑難排解步驟後仍無法順利串流處理，請使用 Azure 入口網站提交支援票證。</span><span class="sxs-lookup"><span data-stu-id="606d0-138">If after following the troubleshooting steps you still cannot successfully stream, submit a support ticket using the Azure portal.</span></span>
> 
> 

## <a name="media-services-learning-paths"></a><span data-ttu-id="606d0-139">媒體服務學習路徑</span><span class="sxs-lookup"><span data-stu-id="606d0-139">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="606d0-140">提供意見反應</span><span class="sxs-lookup"><span data-stu-id="606d0-140">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

