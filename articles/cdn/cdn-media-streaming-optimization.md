---
title: "aaaMedia 資料流最佳化透過 hello Azure 內容傳遞網路"
description: "將串流媒體檔案最佳化以便傳遞順暢"
services: cdn
documentationcenter: 
author: smcevoy
manager: erikre
editor: 
ms.assetid: 
ms.service: cdn
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/16/2017
ms.author: v-semcev
ms.openlocfilehash: a05a86204708c7ea7ef1f9be04323cdda6a2d403
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="media-streaming-optimization-via-hello-azure-content-delivery-network"></a>媒體串流處理透過 hello Azure 內容傳遞網路最佳化 
 
使用高畫質視訊會增加在 hello 網際網路，這會建立有效率的傳遞大型檔案的問題。 客戶即時視訊資產上各種網路和用戶端擁有 hello world，或視需要順暢地播放的視訊。 媒體串流處理檔案快速又有效率的傳遞機制是重大 tooensure 平滑且更有趣的取用者經驗。  

即時串流處理媒體為特別地困難 toodeliver 因為 hello 大型大小和並行的檢視器的數目。 長時間延遲會導致使用者 tooleave。 由於無法事先快取即時資料流，而大型延遲不是可接受 tooviewers，必須及時傳遞視訊片段。 

資料流處理的 hello 要求模式也會提供一些新的挑戰。 當受歡迎的即時資料流或新的序列所發行的千分位隨選視訊 toomillions 一個檢視器可能會要求在 hello hello 資料流相同的時間。 在此情況下，整合是重要的 toonot 智慧要求時 hello 資產不會快取尚未不勝負荷 hello 原始伺服器。
 
hello Azure 內容傳遞網路從 Akamai 現在提供傳遞串流處理媒體資產有效率地 toousers 跨大規模 hello 地球的功能。 hello 功能可降低延遲，因為它可以減少 hello hello 來源伺服器上的負載。 這項功能可與 hello Akamai 標準定價層。 

hello Verizon 從 Azure 內容傳遞網路直接在 hello 一般 web 傳遞最佳化類型中提供串流媒體。
 
## <a name="configure-an-endpoint-toooptimize-media-streaming-in-hello-azure-content-delivery-network-from-akamai"></a>Hello Akamai 從 Azure 內容傳遞網路資料流端點 toooptimize 媒體設定
 
您可以設定您內容傳遞網路 (CDN) 端點的 toooptimize 傳遞透過 hello Azure 入口網站的大型檔案。 您也可以使用我們的 REST Api，或任何 hello 用戶端 Sdk toodo 這。 hello 下列步驟顯示 hello 程序，透過 hello Azure 入口網站：

1. 新的端點，在 hello tooadd**的 CDN 設定檔**頁面上，選取**端點**。
  
    ![新增端點](./media/cdn-media-streaming-optimization/01_Adding.png)

2. 在 hello**適合**下拉式清單中，選取**要求媒體串流處理視訊**video-on-demand 資產。 如果您結合即時和點播視訊串流處理，請選取 [General media streaming] \(一般媒體串流處理)。

    ![選取的串流](./media/cdn-media-streaming-optimization/02_Creating.png) 
 
建立 hello 端點之後，它適用於符合特定準則的所有檔案的 hello 最佳化。 hello 之後 > 一節說明此程序。 
 
## <a name="media-streaming-optimizations-for-hello-azure-content-delivery-network-from-akamai"></a>媒體串流處理的 hello Akamai 從 Azure 內容傳遞網路最佳化
 
來自 Akamai 的媒體串流處理最佳化，適合使用媒體片段傳遞處理即時或點播視訊串流的媒體。 此程序不同於透過漸進式下載或使用位元組範圍要求的單一大型資產傳輸。 如需該樣式的媒體傳遞相關資訊，請查看[大型檔案最佳化](cdn-large-file-optimization.md)。


hello 一般媒體傳遞或 video-on-demand 媒體傳遞最佳化類型使用 CDN 與後端最佳化 toodeliver 媒體資產更快。 它們也會使用媒體資產組態，此組態是以經過一段時間學習的最佳作法為基礎。

### <a name="caching"></a>快取

如果 hello Azure 內容傳遞網路從 Akamai 偵測到該 hello 資產是串流資訊清單或片段，它會使用不同的快取的逾期時間，從一般 web 傳遞。 （請參閱 hello hello 下表中的完整清單）。如往常，請接受 cache-control 或 Expires 標頭傳送 hello 原點。 如果 hello 資產不是媒體資產，它會使用一般 web 傳遞 hello 逾期時間快取。

許多使用者要求片段還不存在時，適用於來源卸載 hello 簡短負快取的時間。 範例是即時資料流，其中 hello 封包無法使用從 hello 原點的第二個。 hello 再快取的時間間隔也有助於卸載 hello 的原始要求，因為通常不修改視訊內容。
 

|    | 一般<br> Web<br>偵錯 | 一般<br> 媒體<br> 串流 | 點播視訊 <br>媒體<br> 串流  
--- | --- | --- | ---
快取：正向 <br> HTTP 200、203、300、 <br> 301、302 和 410 | 7 天 |365 天 | 365 天   
快取：負向 <br> HTTP 204、305、404 <br> 和 405 | None | 1 秒 | 1 秒
 
### <a name="deal-with-origin-failure"></a>處理原始伺服器失敗  

一般媒體傳遞和點播視訊媒體傳遞也都有以典型要求模式的最佳做法為基礎的原始伺服器逾時和重試記錄。 例如，因為一般媒體傳遞即時是的它會使用較短的連線逾時到期 toohello 時間緊迫性質 video-on-demand 媒體傳遞，即時資料流。

當連線逾時時，hello CDN 重試數次傳送 「 504-閘道逾時 」 錯誤 toohello 用戶端之前。 

當檔案符合 hello 檔案類型和大小條件清單時，hello CDN 會使用媒體串流處理 hello 行為。 否則，會使用一般 Web 傳遞。
   
### <a name="conditions-for-media-streaming-optimization"></a>媒體串流最佳化的條件 

hello 下表列出用於媒體串流最佳化滿足的準則 toobe hello 組： 
 
支援的串流類型 | 副檔名  
--- | ---  
Apple HLS | m3u8、m3u、m3ub、key、ts、aac
Adobe HDS | f4m、f4x、drmmeta、bootstrap、f4f、<br>Seg-Frag URL 結構 <br> (matching regex: ^(/.*)Seq(\d+)-Frag(\d+)
DASH | mpd、dash、divx、ismv、m4s、m4v、mp4、mp4v、 <br> sidx、webm、mp4a、m4a、isma
Smooth Streaming | /manifest/,/QualityLevels/Fragments/
  

 
## <a name="media-streaming-optimizations-for-hello-azure-content-delivery-network-from-verizon"></a>媒體串流處理的 hello Verizon 從 Azure 內容傳遞網路最佳化

hello Azure 內容傳遞網路從 Verizon 傳遞串流處理媒體資產是直接使用 hello 一般 web 傳遞最佳化類型。 某些功能在 hello CDN 直接協助傳遞預設的媒體資產。

### <a name="partial-cache-sharing"></a>部分快取共用

部分快取共用，可讓 hello CDN tooserve 部分快取內容的 toonew 要求。 例如，如果第一個要求 toohello hello CDN 導致快取遺漏，hello 要求會傳送 toohello 原點。 雖然此內容不完整載入 hello CDN 快取時，其他要求 toohello CDN 可以開始取得這項資料。 

### <a name="cache-fill-wait-time"></a>快取填滿等候時間

 hello 快取填滿的等候時間功能強制 hello edge server toohold 的任何後續要求 hello 直到 HTTP 回應標頭傳來 hello 來源伺服器相同的資源。 如果 HTTP 回應標頭從 hello 原點抵達 hello 計時器終止之前，所有已暫停要求是從 hello 成長快取。 在 hello 相同時間、 hello hello 的原始資料會填入快取。 根據預設，hello 快取填滿的等候時間會設定 too3，000 毫秒為單位。 

