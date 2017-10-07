---
title: "即時資料流 aaaTroubleshooting 指南 |Microsoft 文件"
description: "本主題提供如何 tootroubleshoot 即時串流處理問題的建議。"
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
ms.openlocfilehash: 8549bae947ff3b225ce624220d1e48b63f90208c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-guide-for-live-streaming"></a><span data-ttu-id="c0300-103">為即時串流而設的疑難排解指南</span><span class="sxs-lookup"><span data-stu-id="c0300-103">Troubleshooting guide for live streaming</span></span>
<span data-ttu-id="c0300-104">本主題提供如何建議 tootroubleshoot 一些即時串流處理的問題。</span><span class="sxs-lookup"><span data-stu-id="c0300-104">This topic gives suggestions on how tootroubleshoot some live streaming problems.</span></span>

## <a name="issues-related-tooon-premises-encoders"></a><span data-ttu-id="c0300-105">問題相關的 tooon 內部編碼器</span><span class="sxs-lookup"><span data-stu-id="c0300-105">Issues related tooon-premises encoders</span></span>
<span data-ttu-id="c0300-106">本節提供如何 tootroubleshoot 問題相關的 tooon 內部編碼器，會設定 toosend 的建議為即時編碼啟用單一位元速率串流 tooAMS 通道。</span><span class="sxs-lookup"><span data-stu-id="c0300-106">This section gives suggestions on how tootroubleshoot problems related tooon-premises encoders that are configured toosend a single bitrate stream tooAMS channels that are enabled for live encoding.</span></span>

### <a name="problem-would-like-toosee-logs"></a><span data-ttu-id="c0300-107">問題： 希望 toosee 記錄檔</span><span class="sxs-lookup"><span data-stu-id="c0300-107">Problem: Would like toosee logs</span></span>
* <span data-ttu-id="c0300-108">潛在問題：找不到可能有助於偵錯問題的編碼器記錄檔。</span><span class="sxs-lookup"><span data-stu-id="c0300-108">**Potential issue**: Can't find encoder logs that might help in debugging issues.</span></span>
  
  * <span data-ttu-id="c0300-109">**Telestream Wirecas**：您通常可以在 C:\Users\{使用者名稱}\AppData\Roaming\Wirecast\ 下找到記錄檔</span><span class="sxs-lookup"><span data-stu-id="c0300-109">**Telestream Wirecast**: You can usually find logs under C:\Users\{username}\AppData\Roaming\Wirecast\\</span></span> 
  * <span data-ttu-id="c0300-110">**元素 Live**： 您可以尋找已連結 toologs hello 管理入口網站上。</span><span class="sxs-lookup"><span data-stu-id="c0300-110">**Elemental Live**: You can find has links toologs on hello management portal.</span></span> <span data-ttu-id="c0300-111">依序按一下 [統計] 及 [記錄檔]。</span><span class="sxs-lookup"><span data-stu-id="c0300-111">Click on **Stats**, then **Logs**.</span></span> <span data-ttu-id="c0300-112">在 [hello**記錄檔**] 頁面上，您會看到所有的記錄檔清單 hello LiveEvent 項目時，請選擇其中一個比對您目前的工作階段的 hello。</span><span class="sxs-lookup"><span data-stu-id="c0300-112">On hello **Log Files** page, you will see a list of logs for all hello LiveEvent items; select hello one matching your current session.</span></span> 
  * <span data-ttu-id="c0300-113">**快閃媒體即時編碼程式**： 您可以找到 hello**記錄檔目錄...**瀏覽 toohello**編碼方式記錄** 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="c0300-113">**Flash Media Live Encoder**: You can find hello **Log Directory...** by navigating toohello **Encoding Log** tab.</span></span>

### <a name="problem-there-is-no-option-for-outputting-a-progressive-stream"></a><span data-ttu-id="c0300-114">問題：沒有輸出漸進式資料流的選項</span><span class="sxs-lookup"><span data-stu-id="c0300-114">Problem: There is no option for outputting a progressive stream</span></span>
* <span data-ttu-id="c0300-115">**可能的問題**: hello 編碼器正在使用不會自動非交錯。</span><span class="sxs-lookup"><span data-stu-id="c0300-115">**Potential issue**: hello encoder being used doesn't automatically deinterlace.</span></span> 
  
    <span data-ttu-id="c0300-116">**疑難排解步驟**： 尋找 hello 編碼器介面中的取消交錯式選項。</span><span class="sxs-lookup"><span data-stu-id="c0300-116">**Troubleshooting steps**: Look for a de-interlacing option within hello encoder interface.</span></span> <span data-ttu-id="c0300-117">一旦啟用非交錯處理，請再次檢查漸進式的輸出設定。</span><span class="sxs-lookup"><span data-stu-id="c0300-117">Once de-interlacing is enabled, check again for progressive output settings.</span></span> 

### <a name="problem-tried-several-encoder-output-settings-and-still-unable-tooconnect"></a><span data-ttu-id="c0300-118">問題： 嘗試幾個編碼器輸出設定，並將仍然無法 tooconnect。</span><span class="sxs-lookup"><span data-stu-id="c0300-118">Problem: Tried several encoder output settings and still unable tooconnect.</span></span>
* <span data-ttu-id="c0300-119">**可能的問題**：未正確重設 Azure 編碼通道。</span><span class="sxs-lookup"><span data-stu-id="c0300-119">**Potential issue**: Azure encoding channel was not properly reset.</span></span> 
  
    <span data-ttu-id="c0300-120">**疑難排解步驟**： 請確定 hello 編碼器不會再推入 tooAMS、 停止及重設 hello 通道。</span><span class="sxs-lookup"><span data-stu-id="c0300-120">**Troubleshooting steps**: Make sure hello encoder is no longer pushing tooAMS, stop and reset hello channel.</span></span> <span data-ttu-id="c0300-121">執行一次之後, 再試一次您的編碼器連接的 hello 新設定。</span><span class="sxs-lookup"><span data-stu-id="c0300-121">Once running again, try connecting your encoder with hello new settings.</span></span> <span data-ttu-id="c0300-122">如果這仍無法更正 hello 問題，請嘗試完全建立新的通道，有時數次嘗試失敗之後通道可能會損毀。</span><span class="sxs-lookup"><span data-stu-id="c0300-122">If this still does not correct hello issue, try creating a new channel entirely, sometimes channels can become corrupt after several failed attempts.</span></span>  
* <span data-ttu-id="c0300-123">**可能的問題**: hello GOP 大小或主要畫面格設定不佳。</span><span class="sxs-lookup"><span data-stu-id="c0300-123">**Potential issue**: hello GOP size or key frame settings are not optimal.</span></span> 
  
    <span data-ttu-id="c0300-124">**疑難排解步驟**：建議的 GOP 大小或主要畫面間隔為 2 秒。</span><span class="sxs-lookup"><span data-stu-id="c0300-124">**Troubleshooting steps**: Recommended GOP size or keyframe interval is 2 seconds.</span></span> <span data-ttu-id="c0300-125">某些編碼器以畫面數目計算此設定，某些則使用秒。</span><span class="sxs-lookup"><span data-stu-id="c0300-125">Some encoders calculate this setting in number of frames, while others use seconds.</span></span> <span data-ttu-id="c0300-126">例如： 輸出 30fps 時, hello GOP 大小會是 60 框架，這是對等 too2 秒。</span><span class="sxs-lookup"><span data-stu-id="c0300-126">For example: When outputting 30fps, hello GOP size would be 60 frames, which is equivalent too2 seconds.</span></span>  
* <span data-ttu-id="c0300-127">**可能的問題**： 封鎖 hello 資料流已關閉的連接埠。</span><span class="sxs-lookup"><span data-stu-id="c0300-127">**Potential issue**: Closed ports are blocking hello stream.</span></span> 
  
    <span data-ttu-id="c0300-128">**疑難排解步驟**： 當 RTMP 透過串流處理，請檢查防火牆和/或 proxy 設定 tooconfirm 1935 和 1936年的輸出連接埠已開啟。</span><span class="sxs-lookup"><span data-stu-id="c0300-128">**Troubleshooting steps**: When streaming via RTMP, check firewall and/or proxy settings tooconfirm that outbound ports 1935 and 1936 are open.</span></span> <span data-ttu-id="c0300-129">使用 RTP 資料流時，請確認輸出連接埠 2010 已開啟。</span><span class="sxs-lookup"><span data-stu-id="c0300-129">When using RTP streaming, confirm that outbound port 2010 is open.</span></span> 

### <a name="problem-when-configuring-hello-encoder-toostream-with-hello-rtp-protocol-there-is-no-place-tooenter-a-host-name"></a><span data-ttu-id="c0300-130">問題： 在設定 hello 編碼器 toostream 以 hello RTP 通訊協定時，沒有無處 tooenter 主機名稱。</span><span class="sxs-lookup"><span data-stu-id="c0300-130">Problem: When configuring hello encoder toostream with hello RTP protocol, there is no place tooenter a host name.</span></span>
* <span data-ttu-id="c0300-131">**可能的問題**： 許多 RTP 編碼器不允許的主機名稱和 IP 位址必須 toobe 取得。</span><span class="sxs-lookup"><span data-stu-id="c0300-131">**Potential issue**: Many RTP encoders do not allow for host names, and an IP address will need toobe acquired.</span></span>  
  
    <span data-ttu-id="c0300-132">**疑難排解步驟**: toofind hello IP 位址，請開啟命令提示字元的任何電腦上。</span><span class="sxs-lookup"><span data-stu-id="c0300-132">**Troubleshooting steps**: toofind hello IP address, open a command prompt on any computer.</span></span> <span data-ttu-id="c0300-133">這在 Windows 中，開啟 toodo hello 執行啟動器 （WIN + R），並輸入"cmd"tooopen。</span><span class="sxs-lookup"><span data-stu-id="c0300-133">toodo this in Windows, open hello Run launcher (WIN + R) and type “cmd” tooopen.</span></span>  
  
    <span data-ttu-id="c0300-134">一旦開啟 hello 命令提示字元，輸入 「 Ping [AMS 主機名稱]"。</span><span class="sxs-lookup"><span data-stu-id="c0300-134">Once hello command prompt is open, type "Ping [AMS Host Name]".</span></span> 
  
    <span data-ttu-id="c0300-135">可以藉由略過從 hello Azure 內嵌 URL 以反白顯示 hello 下列範例中的 hello 連接埠號碼衍生 hello 主機名稱：</span><span class="sxs-lookup"><span data-stu-id="c0300-135">hello host name can be derived by omitting hello port number from hello Azure Ingest URL, as highlighted in hello following example:</span></span> 
  
    <span data-ttu-id="c0300-136">rtp://test2-amstest009.rtp.channel.mediaservices.windows.net:2010/</span><span class="sxs-lookup"><span data-stu-id="c0300-136">rtp://test2-amstest009.rtp.channel.mediaservices.windows.net:2010/</span></span> 
  
    ![FMLE](./media/media-services-fmle-live-encoder/media-services-fmle10.png)

> [!NOTE]
> <span data-ttu-id="c0300-138">如果後您仍無法成功地串流處理 hello 疑難排解步驟，提交支援票證使用 hello Azure 入口網站。</span><span class="sxs-lookup"><span data-stu-id="c0300-138">If after following hello troubleshooting steps you still cannot successfully stream, submit a support ticket using hello Azure portal.</span></span>
> 
> 

## <a name="media-services-learning-paths"></a><span data-ttu-id="c0300-139">媒體服務學習路徑</span><span class="sxs-lookup"><span data-stu-id="c0300-139">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="c0300-140">提供意見反應</span><span class="sxs-lookup"><span data-stu-id="c0300-140">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

