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
# <a name="use-hello-elemental-live-encoder-toosend-a-single-bitrate-live-stream"></a>使用單一位元速率即時資料流，hello 元素即時編碼器 toosend
> [!div class="op_single_selector"]
> * [Elemental Live](media-services-configure-elemental-live-encoder.md)
> * [Tricaster](media-services-configure-tricaster-live-encoder.md)
> * [Wirecast](media-services-configure-wirecast-live-encoder.md)
> * [FMLE](media-services-configure-fmle-live-encoder.md)
>
>

本主題說明如何 tooconfigure hello[元素 Live](http://www.elementaltechnologies.com/products/elemental-live)編碼器 toosend 單一位元速率串流的即時編碼啟用 tooAMS 通道。  如需詳細資訊，請參閱[使用通道，會啟用 tooPerform Live 使用 Azure 媒體服務編碼](media-services-manage-live-encoder-enabled-channels.md)。

本教學課程示範如何 toomanage Azure 媒體服務 (AMS) 中使用 Azure 媒體服務總管 (AMSE) 工具。 此工具只會在 Windows 電腦上執行。 如果您是在 Mac 或 Linux 上，使用 Azure 入口網站 toocreate hello[通道](media-services-portal-creating-live-encoder-enabled-channel.md#create-a-channel)和[程式](media-services-portal-creating-live-encoder-enabled-channel.md)。

## <a name="prerequisites"></a>必要條件
* 必須使用元素即時 web 介面 toocreate 即時事件的實用知識。
* [建立 Azure 媒體服務帳戶](media-services-portal-create-account.md)
* 確定有執行中的「串流端點」。 如需詳細資訊，請參閱 [在媒體服務帳戶中管理串流端點](media-services-portal-manage-streaming-endpoints.md)。
* 安裝 hello 最新版 hello [AMSE](https://github.com/Azure/Azure-Media-Services-Explorer)工具。
* 啟動 hello 工具和 tooyour AMS 帳戶連接。

## <a name="tips"></a>祕訣
* 請盡可能使用實體的有線網際網路連線。
* 最佳經驗法則時判斷頻寬需求為串流處理位元的 toodouble hello。 雖然這不是強制性需求，有助於減少 hello 發生網路壅塞的影響。
* 使用軟體型編碼器時，請關閉任何不必要的程式。

## <a name="elemental-live-with-rtp-ingest"></a>Elemental Live 與 RTP 嵌入
本節說明如何 tooconfigure hello 元素即時編碼器會傳送單一位元速率透過 RTP 的即時資料流。  如需詳細資訊，請參閱 [透過 RTP 的 MPEG-TS 串流](media-services-manage-live-encoder-enabled-channels.md#channel)。

### <a name="create-a-channel"></a>建立通道

1. 在 hello AMSE 工具中，瀏覽 toohello **Live**索引標籤，然後以滑鼠右鍵按一下 hello 通道區域內。 從功能表選取 [建立通道...]  從 [hello] 功能表中。

    ![Elemental](./media/media-services-elemental-live-encoder/media-services-elemental1.png)

2. 指定通道名稱，hello 描述欄位是選擇性的。 在 [通道設定] 下選取**標準**hello 即時編碼選項，以 hello 輸入通訊協定設定得**RTP (MPEG-TS)**。 您可以將所有其他設定保留現狀。

    請確定 hello**開始 hello 新通道現在**已選取。

3. 按一下 [ **建立頻道**]。

   ![Elemental](./media/media-services-elemental-live-encoder/media-services-elemental12.png)

> [!NOTE]
> hello 通道花費 20 分鐘 toostart 一樣長。
>
>

您可以啟動 hello 通道時[設定 hello 編碼器](media-services-configure-elemental-live-encoder.md#configure_elemental_rtp)。

> [!IMPORTANT]
> 請注意，只要通道進入就緒狀態，就會開始計費。 如需詳細資訊，請參閱 [通道的狀態](media-services-manage-live-encoder-enabled-channels.md#states)。
>
>

### <a id=configure_elemental_rtp></a>設定 hello 元素即時編碼器
在此教學課程的 hello 會使用下列的輸出設定。 hello 本節其餘部分描述更詳細的組態步驟。

**視訊**：

* 轉碼器：H.264
* 設定檔：高 (層級 4.0)
* 位元速率：5000 kbps
* 主要畫面格：2 秒 (60 秒)
* 畫面播放速率：30

**音訊**：

* 轉碼器：AAC (LC)
* 位元速率：192 kbps
* 取樣速率：44.1 kHz

#### <a name="configuration-steps"></a>組態步驟
1. 瀏覽 toohello**元素 Live** web 介面，並設定好的 hello 編碼器**UDP/TS**資料流。
2. 一旦建立新的事件，向下 toohello 輸出群組捲動，並新增 hello **UDP/TS**輸出群組。
3. 選取 新增串流 然後按一下加入輸出 建立新的輸出。  

    ![Elemental](./media/media-services-elemental-live-encoder/media-services-elemental13.png)

   > [!NOTE]
   > 建議的 hello 元素事件有 hello 播放設定得 「 系統時鐘"toohelp hello 編碼器重新連線在 hello 案例中的資料流失敗。
   >
   >
4. 既然 hello 輸出建立之後，按一下**新增資料流**。 現在可以設定 hello 輸出設定。
5. 捲動 toohello 」 資料流 1"已建立，請按一下 hello**視訊**hello 左側索引標籤，展開 hello**進階**設定 區段。

    ![Elemental](./media/media-services-elemental-live-encoder/media-services-elemental4.png)

    雖然元素 Live 有各種不同的可自訂，hello 下列設定建議的開始使用資料流 tooAMS。

   * 解析度：1280 x 720
   * 畫面播放速率：30
   * GOP 大小：60 個畫面格
   * 交錯式模式：漸進式
   * 位元速率：5000000 位元/秒 (這可以根據網路限制調整)

    ![Elemental](./media/media-services-elemental-live-encoder/media-services-elemental5.png)

1. 取得 hello 通道的輸入的 URL。

    瀏覽後 toohello AMSE 工具，並檢查 hello 通道完成狀態。 一旦 hello 狀態已從**起始**太**執行**，您可以取得 hello 輸入的 URL。

    當執行 hello 通道時，hello 通道名稱上按一下滑鼠右鍵、 向下 toohover 巡覽**複製輸入 URL tooclipboard** ，然後選取 **主要輸入 URL**。  

    ![Elemental](./media/media-services-elemental-live-encoder/media-services-elemental6.png)
2. 此資訊貼在 hello**主要目的**hello Elemental 欄位。 所有其他設定可以維持 hello 預設值。

    ![Elemental](./media/media-services-elemental-live-encoder/media-services-elemental14.png)

    如需額外的備援，重複這些步驟以 hello 次要輸入 URL UDP/TS 串流建立個別的 「 輸出 」 索引標籤。
3. 按一下**建立**（如果已建立新事件） 或**更新**（如果正在編輯現有的事件），然後再繼續 toostart hello 編碼器。

> [!IMPORTANT]
> 在您按一下之前**啟動**hello 元素即時 web 介面上，您**必須**確保 hello 通道已就緒。
> 此外，請確定未 tooleave hello 通道處於就緒狀態，但不超過 > 15 分鐘的事件。
>
>

Hello 資料流已執行 30 秒後，瀏覽後 toohello AMSE 工具和測試播放。  

### <a name="test-playback"></a>測試播放

瀏覽 toohello AMSE 工具，並以滑鼠右鍵按一下 hello 通道 toobe 測試。 從 [hello] 功能表中，將滑鼠停留在**播放 hello 預覽**選取**使用 Azure Media Player**。  

    ![Elemental](./media/media-services-elemental-live-encoder/media-services-elemental8.png)

Hello 資料流會顯示 hello 播放程式中，如果 hello 編碼器已經過正確設定的 tooconnect tooAMS。

如果收到錯誤，hello 通道必須調整 toobe 重設和編碼器設定。 請參閱 hello[疑難排解](media-services-troubleshooting-live-streaming.md)指引主題。   

### <a name="create-a-program"></a>建立程式
1. 一旦確認通道播放沒問題後，請建立程式。 在 hello **Live** hello AMSE 工具中索引標籤上，在 hello 程式區域按一下滑鼠右鍵並選取**建立新的程式**。  

    ![Elemental](./media/media-services-elemental-live-encoder/media-services-elemental9.png)
2. Hello 程式，並有需要則調整 hello**封存時間長度**（預設值 too4 時段）。 您也可以指定儲存體位置，或保留 hello 預設。  
3. 檢查 hello**開始 hello 程式現在**方塊。
4. 按一下 [建立程式] 。  

    >[!NOTE]
    > 建立程式時所使用的時間會比建立通道時少。   
      
5. Hello 程式開始執行之後，以確認播放 hello 程式上按一下滑鼠右鍵，瀏覽過**播放 hello （_r)** ，然後選取 **使用 Azure Media Player**。  
6. 確認，以滑鼠右鍵按一下 hello 程式，並選取**複製 hello 輸出 URL tooClipboard** (或擷取這項資訊從 hello**程式資訊和設定**hello 功能表選項)。

hello 資料流已準備好 toobe 內嵌在播放程式，或分散式的 tooan 對象的即時檢視。  

## <a name="troubleshooting"></a>疑難排解
請參閱 hello[疑難排解](media-services-troubleshooting-live-streaming.md)指引主題。

## <a name="media-services-learning-paths"></a>媒體服務學習路徑
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>提供意見反應
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]
