---
title: "透過 hello Azure 內容傳遞網路 aaaLarge 檔案下載最佳化"
description: "深度解說大型檔案下載最佳化"
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
ms.openlocfilehash: 2646979bfb38e997037bcff5b1cdda34e22c394a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="large-file-download-optimization-via-hello-azure-content-delivery-network"></a>透過 hello Azure 內容傳遞網路的大型檔案下載最佳化

傳送 hello 網際網路上的內容檔案大小繼續 toogrow 到期 tooenhanced 功能、 改善的圖形，以及豐富的媒體內容。 這種成長是由許多因素所驅動，包括：寬頻滲透、大型廉價存放裝置、高畫質影片普遍增加，以及連線至網際網路的裝置 (IoT) 等。 大型檔案快速又有效率的傳遞機制是重大 tooensure 平滑且更有趣的取用者經驗。

傳送大型檔案有幾項困難。 首先，hello 的平均時間 toodownload 大型檔案可能十分顯著因為應用程式可能會以循序方式下載所有資料。 在某些情況下，應用程式可能會下載 hello 最後一部分之前 hello 第一個部分的檔案。 當要求只有少量的檔案，或使用者暫停下載時，hello 下載可能會失敗。 hello 下載也可能會延遲直到 hello 後內容傳遞網路 (CDN) 會擷取 hello 整個檔案從 hello 原始伺服器。 

第二，使用者的電腦和 hello 檔案之間的 hello 延遲決定，他們可以檢視內容的 hello 速度。 此外，網路壅塞和容量問題也會影響輸送量。 大於伺服器與使用者之間的距離會建立其他封包遺失 toooccur 減少品質的機會。 hello 品質降低因有限輸送量並增加的封包遺失可能會增加檔案下載 toofinish hello 等候時間。 

第三，許多大型檔案不會完整傳遞。 使用者可能取消下載到一半，或觀賞只 hello 長 MP4 視訊前幾分鐘。 因此，軟體和媒體傳遞公司都想 toodeliver 唯一 hello 部分之要求的檔案。 散佈 hello 要求部分可以降低 hello 原始伺服器 hello 輸出流量。 Hello 記憶體和 I/O 壓力 hello 來源伺服器上的，也會減少有效率的通訊群組。 

hello Azure 內容傳遞網路從 Akamai 現在提供傳送大型檔案有效率地 toousers 跨大規模 hello 地球的功能。 hello 功能可降低延遲，因為它可以減少 hello hello 來源伺服器上的負載。 這項功能可與 hello Akamai 標準定價層。

## <a name="configure-a-cdn-endpoint-toooptimize-delivery-of-large-files"></a>將大型檔案的 CDN 端點 toooptimize 傳遞設定

您可以設定您的 CDN 端點 toooptimize 傳遞，如透過 hello Azure 入口網站的大型檔案。 您也可以使用我們的 REST Api，或任何 hello 用戶端 Sdk toodo 這。 hello 下列步驟顯示 hello 程序，透過 hello Azure 入口網站。

1. 新的端點，在 hello tooadd**的 CDN 設定檔**頁面上，選取**端點**。

    ![新增端點](./media/cdn-large-file-optimization/01_Adding.png)  
 
2. 在 hello**適合**下拉式清單中，選取**大型檔案的下載**。

    ![已選取大型檔案最佳化](./media/cdn-large-file-optimization/02_Creating.png)


建立 hello CDN 端點之後，它適用於符合特定準則的所有檔案的 hello 大型檔案最佳化。 hello 之後 > 一節說明此程序。

## <a name="optimize-for-delivery-of-large-files-with-hello-azure-content-delivery-network-from-akamai"></a>針對從 Akamai 以 hello Azure 內容傳遞網路的大型檔案傳遞最佳化

更快速且更 responsively hello 大型檔案最佳化類型功能開啟網路最佳化和組態 toodeliver 大型檔案。 Akamai 與一般 web 傳遞快取只下方 1.8 g b 的檔案，並可以通道 （而不是快取） 檔案組成 too150 GB。 大型的檔案最佳化功能會快取總 too150 GB 的檔案。

大型檔案最佳化在滿足特定條件下會生效。 條件包括 hello 原始伺服器的運作方式 hello 和大小的 hello 要求的檔案類型。 我們在這些主題的詳細資料之前，您應該了解 hello 最佳化的運作方式。 

### <a name="object-chunking"></a>物件區塊化 

hello Akamai 從 Azure 內容傳遞網路會使用稱為物件區塊的技術。 要求的大型檔案時，hello CDN 會從 hello 原點擷取 hello 檔案的較小的片段。 Hello CDN 邊緣/彈出伺服器收到完整或位元組範圍的檔案要求之後，它會檢查是否支援此最佳化的 hello 檔案類型。 它也會檢查 hello 檔案類型是否符合 hello 檔案大小需求。 如果 hello 檔案大小大於 10 MB，hello CDN 邊緣伺服器要求 hello 檔案從 2 MB 的區塊中的 hello 原點。 

Hello 區塊抵達 hello CDN 邊緣之後，它有快取，並立即提供 toohello 使用者。 hello CDN，然後以平行方式預先提取 hello 下一個區塊。 這個預先擷取可確保 hello 內容仍然 hello 使用者，可減少延遲，前面的一個區塊。 此程序會等到整個 hello 繼續下載檔案時 （如有要求），所有的位元組範圍 （如有要求），或 hello 用戶端會終止 hello 連線。 

如需有關 hello 位元組範圍要求的詳細資訊，請參閱[RFC 7233](https://tools.ietf.org/html/rfc7233)。

在收到 hello CDN 會快取任何區塊。 hello 整個檔案沒有 toobe hello CDN 快取上快取。 後續 hello 檔案或位元組範圍要求是從 hello CDN 快取。 如果並非所有的 hello 區塊會 hello CDN 快取，預先擷取是使用的 toorequest hello 原點的區塊。 此最佳化依賴 hello 能力 hello 原始伺服器 toosupport 位元組範圍要求。 _如果 hello 原始伺服器不支援位元組範圍要求，此最佳化並非有效的。_ 

### <a name="caching"></a>快取
大型檔案最佳化會使用不同的預設從一般 Web 傳遞快取逾期時間。 它會根據 HTTP 回應碼來區分正向快取與負向快取。 如果指定到期時間透過快取控制 hello 原始伺服器，或到期 hello 回應標頭，hello CDN 會接受該值。 當 hello 原點未指定，hello 檔符合此最佳化類型的 hello 類型和大小條件 hello CDN 使用大型的檔案最佳化功能 hello 預設值。 否則，hello CDN 會使用預設值進行一般 web 傳遞。


|    | 一般 Web | 大型檔案最佳化 
--- | --- | --- 
快取：正向 <br> HTTP 200、203、300、 <br> 301、302 和 410 | 7 天 |1 天  
快取：負向 <br> HTTP 204、305、404 <br> 和 405 | None | 1 秒 

### <a name="deal-with-origin-failure"></a>處理原始伺服器失敗

hello 原始讀取逾時長度會增加從 hello 大型檔案最佳化類型的一般 web 傳遞 tootwo 分鐘的兩秒。 這種增加量較大檔案大小 tooavoid hello 提早逾時連接的帳戶。

當連線逾時時，hello CDN 重試數次傳送 「 504-閘道逾時 」 錯誤 toohello 用戶端之前。 

### <a name="conditions-for-large-file-optimization"></a>大型檔案最佳化的條件

hello 下表列出 hello 整組準則 toobe 滿足大型檔案最佳化：

條件 | 值 
--- | --- 
支援的檔案類型 | 3g2、3gp、asf、avi、bz2、dmg、exe、f4v、flv、 <br> gz、hdp、iso、jxr、m4v、mkv、mov、mp4、 <br> mpeg、mpg、mts、pkg、qt、rm、swf、tar、 <br> tgz、wdp、webm、webp、wma、wmv、zip  
檔案大小下限 | 10 MB 
檔案大小上限 | 150 GB 
原始伺服器特性 | 必須支援位元組範圍要求 

## <a name="optimize-for-delivery-of-large-files-with-hello-azure-content-delivery-network-from-verizon"></a>針對從 Verizon 以 hello Azure 內容傳遞網路的大型檔案傳遞最佳化

hello Verizon 從 Azure 內容傳遞網路將傳遞沒有端點上的檔案大小的大型檔案。 其他功能會開啟預設 toomake 傳送大型檔案的速度。

### <a name="complete-cache-fill"></a>完成快取填滿

hello 預設完整快取填滿功能可讓您 hello CDN toopull 檔案到 hello 快取的初始要求是放棄或遺失。 

完成快取填滿最適合大型資產。 一般而言，使用者不會從下載開始 toofinish。 他們使用漸進式下載。 hello 預設行為會強制 hello edge server tooinitiate hello 資產的背景擷取從 hello 原始伺服器。 之後，hello 資產是 hello 邊緣伺服器的本機快取中。 Hello 完整物件位於 hello 快取之後，hello edge server，可滿足 hello 快取物件的位元組範圍要求 toohello CDN。

可以停用 hello 預設行為，透過 hello Verizon Premium 層中的 hello 規則引擎。

### <a name="peer-cache-fill-hot-filing"></a>對等快取填滿 Hotfiling

hello 預設對等快取填滿熱歸檔功能會使用複雜的專屬演算法。 它會使用其他的邊緣快取伺服器，根據頻寬，並彙總要求度量 toofulfill 用戶端要求的大型、 高度受歡迎的物件。 這項功能可防止大量的額外要求傳送 tooa 使用者的原始伺服器所在的情況。 

### <a name="conditions-for-large-file-optimization"></a>大型檔案最佳化的條件

依預設會開啟 Verizon 的 hello 最佳化功能。 檔案大小上限沒有任何限制。 

## <a name="additional-considerations"></a>其他考量

請考慮 hello 遵循此最佳化類型的其他層面。
 
### <a name="azure-content-delivery-network-from-akamai"></a>Akamai 的 Azure 內容傳遞網路

- hello 區塊處理程序會產生其他要求 toohello 原始伺服器。 不過，hello 整體 hello 的原始傳送的資料數量會小很多。 區塊處理的結果中有更佳在 hello CDN 快取的特性。

- 記憶體和 I/O 壓力會減少在 hello 原點因為傳送嗨檔案的較小的片段。

- 在 hello CDN 快取的區塊，如有任何其他要求 toohello 原點 hello 內容到期或收回從 hello 快取之前。

- 使用者可在建立範圍要求 toohello CDN，且它們視為一般的檔案。 只有當它是有效的檔案類型，而且 hello 位元組範圍是介於 10 MB 到 150 GB 之間，適用於最佳化。 如果 hello 要求的平均檔案大小小於 10 MB，您可能改用想 toouse 一般 web 傳遞。

### <a name="azure-content-delivery-network-from-verizon"></a>Verizon 的 Azure 內容傳遞網路

hello 一般 web 傳遞最佳化類型可以傳遞大型檔案。
