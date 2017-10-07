---
title: "aaaDynamic 網站加速透過 Azure CDN"
description: "動態站台加速深入探討"
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
ms.date: 08/02/2017
ms.author: v-semcev
ms.openlocfilehash: 37e6312ae5e83448f2d87c95ef48c387355748bb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="dynamic-site-acceleration-via-azure-cdn"></a>透過 Azure CDN 進行動態網站加速

社交媒體、 電子商務和 hello hyper-v 個人化 web hello 爆炸，快速增加的百分比表示 hello 內容提供 tooend 使用者即時產生。 使用者期望獲得的快速、可靠且個人化 web 體驗，無關乎瀏覽器、位置、裝置或網路。 不過，hello 非常創新，讓這些經驗也因此聘用緩慢頁面下載，而且 hello 經驗 hello 品質而面臨風險。 

標準的 CDN 功能包含 hello 能力 toocache 檔案接近 tooend 使用者 toospeed 向上傳遞靜態檔案。 不過，使用動態 web 應用程式，快取該內容中的邊緣位置無法 hello server 產生 hello 內容以回應 toouser 行為。 加速 hello 傳遞的這類內容比傳統的邊緣快取更為複雜，而且需要微調的每個項目從起始 toodelivery hello 整個資料路徑上的端對端解決方案。 使用 Azure CDN 動態網站加速 (DSA)，hello 搭配動態內容的 web 網頁會適當地改善效能。

從 Akamai 和 Verizon azure CDN 提供透過 hello 的 DSA 最佳化**適合**端點建立期間的功能表。

## <a name="configuring-cdn-endpoint-tooaccelerate-delivery-of-dynamic-files"></a>設定 CDN 端點 tooaccelerate 傳遞動態檔案

您可以設定您的 CDN 端點 toooptimize 傳遞的動態透過 Azure 入口網站的檔案選取 hello**動態站台加速**hello 下的選項**適合**時的屬性選項建立 hello 端點。 您也可以使用我們的 REST Api，或任何 hello 用戶端 Sdk toodo hello 以程式設計的方式相同。 

### <a name="probe-path"></a>探查路徑
探查路徑是功能特定 tooDynamic 網站加速，因此需要建立一份有效。 DSA 使用小型*探查路徑*檔案放在 hello 原點 toooptimize 網路的路由設定 hello CDN。 您可以下載和上傳我們的範例檔案 tooyour 網站，或使用現有的資產上您為約 10 KB hello 探查路徑改為 hello 資產存在的原點。

> [!Note]
> DSA 會產生額外費用。 如需詳細資訊，請參閱 hello[定價頁面](https://azure.microsoft.com/pricing/details/cdn/)如需詳細資訊。

下列螢幕擷取畫面的 hello 說明 hello 程序，透過 Azure 入口網站。
 
![新增新的 CDN 端點](./media/cdn-dynamic-site-acceleration/01_Endpoint_Profile.png) 

*圖 1： 從 hello 的 CDN 設定檔中加入新的 CDN 端點*
 
![使用 DSA 建立新的 CDN 端點](./media/cdn-dynamic-site-acceleration/02_Optimized_DSA.png)  

*圖 2：在已選取動態網站加速最佳化的情況下建立 CDN 端點*

一旦建立 hello CDN 端點時，它適用於符合特定準則的所有檔案的 hello DSA 最佳化。 下列章節的 hello 描述 DSA 最佳化，在詳細資料。

## <a name="dsa-optimization-using-azure-cdn"></a>使用 Azure CDN 將 DSA 最佳化

在 Azure CDN 的動態站台加速加速使用下列技巧 hello 動態資產的傳遞：

-   路由最佳化
-   TCP 最佳化
-   物件預先擷取 (僅限 Akamai)
-   行動映像壓縮 (僅限 Akamai)

### <a name="route-optimization"></a>路由最佳化

路線最佳化很重要的因為 hello 網際網路是動態的位置，其中流量並暫時中斷經常變更 hello 網路拓撲。 hello 邊界閘道通訊協定 (BGP) 路由 hello hello 網際網路，通訊協定，但可能更快的路由，透過中繼點的目前狀態 (PoP) 伺服器。 

Hello 最佳路徑 toohello 原點使站台會持續存取和動態內容傳遞 tooend 使用者透過 hello 最快速及最可靠的路由可能會選擇路線最佳化。 

hello Akamai 網路使用技術 toocollect 即時資料，以及比較 hello 開啟網際網路 toodetermine hello 最快速路由 hello 原點與 hello 之間的各種 hello Akamai 伺服器，以及 hello 預設 BGP 路由中的不同節點的路徑CDN 邊緣。 這些技術可避開網際網路壅塞點和長途路由。 

同樣地，任一傳播 DNS，高容量的組合支援快顯及健康情況檢查 toodetermine hello 最佳閘道 toobest 路由資料是從 hello Verizon 網路使用 hello 用戶端 toohello 原點。
 
如此一來，完全動態和交易式傳遞內容的更快速且更可靠地 tooend 使用者，即使它是不可快取。 

### <a name="tcp-optimizations"></a>TCP 最佳化

傳輸控制通訊協定 (TCP) 是 hello 標準 hello 網際網路通訊協定使用 toodeliver IP 網路上的應用程式之間的資訊。  根據預設，有數個後並提出要求所需 tooset 總 TCP 連線，以及限制 tooavoid 網路 congestions，這會導致在標尺的效率。 Akamai 中的 Azure CDN 會處理這個問題，方法是將下列三個方面最佳化： 

 - 排除慢速啟動
 - 利用持續連線
 - 調整 TCP 封包參數 (僅限 Akamai)

#### <a name="eliminating-slow-start"></a>排除慢速啟動

*緩慢開始*是限制 hello hello 網路上傳送的資料量，以防止網路壅塞的 hello TCP 通訊協定的一部分。 開始的寄件者與接收者之間的小壅塞視窗大小為止最大的 hello 或偵測到的封包遺失。

Akamai 和 Verizon 中的 Azure CDN 透過三個步驟來排除慢速啟動：

1.  Akamai 和 Verizon 的網路使用 「 狀況與監視 toomeasure hello 頻寬邊緣 PoP 伺服器之間的連線的頻寬。
2. hello 度量會邊緣 PoP 伺服器之間共用，使每一部伺服器所知的 hello 網路狀況和伺服器健全狀況的 hello 其他周圍的快顯。  
3. hello CDN 邊緣伺服器現在都能 toomake 假設某些傳輸參數，例如與它靠近其他 CDN 邊緣伺服器通訊時，應該是 hello 最佳的視窗大小。 此步驟中，表示是否能夠更高的封包資料傳輸 hello hello hello CDN 邊緣伺服器之間的連線健全狀況，可以增加 hello 初始的壅塞視窗大小。  

#### <a name="leveraging-persistent-connections"></a>利用持續連線

使用 CDN，較少的唯一機器連接 tooyour 原始伺服器直接相較於直接連線 tooyour 來源的使用者。 從 Akamai 和 Verizon azure CDN 也加入集區使用者的要求一起 tooestablish hello 原點使用較少的連線。

如先前所述，TCP 連線採取幾個要求來回交握 tooestablish 新的連接。 持續連線，也稱為 「 HTTP 保持運作，「 多個 HTTP 要求 toosave 來回行程時間的重複使用現有的 TCP 連線，並加速傳遞。 

hello Verizon 網路也會傳送定期保持運作封包透過 hello TCP 連線 tooprevent 從正在關閉開啟的連接。

#### <a name="tuning-tcp-packet-parameters"></a>調整 TCP 封包參數

Akamai 從 azure CDN 也微調 hello 參數，以管理伺服器對伺服器連線，並能減少 hello 使用下列技巧 hello hello 網站中內嵌的內容所需的往返 tooretrieve round 長時間牽引量：

1.  增加 hello 初始的壅塞視窗，以便能傳送多個封包，而不等候確認。
2.  以便在偵測到遺失時，並重新傳輸，就會發生更快速地減少 hello 初始重新傳輸逾時。
3.  遞減 hello 最小值和最大重新傳輸逾時 tooreduce hello 假設封包在傳輸中遺失之前的等待時間。

### <a name="object-prefetch-akamai-only"></a>物件預先擷取 (僅限 Akamai)

大多數網站是由參考諸如映像和指令碼等各種其他資源的 HTML 網頁所組成。 一般而言，當用戶端要求網頁，hello 瀏覽器會先下載並剖析 hello HTML 物件，並使 toolinked 資產之必要的 toofully hello 頁面載入的其他要求。 

*預先擷取*是一種技術 tooretrieve 映像和指令碼內嵌在 hello HTML 網頁 hello HTML 提供 toohello 瀏覽器中，而之前 hello 瀏覽器甚至使這些物件的要求。 

以 hello**預先擷取**次 hello hello CDN 服務 hello HTML 基礎頁面 toohello 用戶端的瀏覽器中，當 hello CDN 開啟選項剖析 hello HTML 檔案和提出其他要求的任何連結的資源並將它存放在其快取。 當 hello 戶端 hello 要求 hello 連結資產，hello CDN 邊緣伺服器已經有 hello 要求的物件，而且可以服務它們立即沒有往返 toohello 原點。 此最佳化有助於可快取和不可快取的內容。

### <a name="adaptive-image-compression-akamai-only"></a>調整映像壓縮 (僅限 Akamai)

某些裝置，特別是行動電腦遇到時間 tootime 從較低的網路速度。 在這些情況中，會更有幫助他們的網頁中的 hello 使用者 tooreceive 小影像更快速而不是等待長時間的完整解析度的影像。

這項功能會自動監視網路品質，並採用標準 JPEG 壓縮方法，當網路速度慢 tooimprove 傳遞時間。

調整映像壓縮 | 副檔名  
--- | ---  
JPEG 壓縮 | .jpg、.jpeg、.jpe、.jig、.jgig、.jgi

## <a name="caching"></a>快取

DSA，與快取已關閉預設會在 hello CDN，即使 hello 原點 hello 回應中包含快取控制項/到期的標頭。 因為 DSA 通常用於動態的資產，應該不會快取因為它是唯一的 tooeach 用戶端，關閉此預設值，並開啟預設的快取可能會中斷這種行為。

如果您有混合靜態和動態資產的網站時，它會是最佳 tootake 混合式方法 tooget hello 達到最佳效能。 

如果您使用和 Verizon premium，您可以開啟回上特定的情況下使用 hello 規則引擎的快取。  

替代方式是 toouse 兩個的 CDN 端點。 DSA toodeliver 動態資產的一個，另一個端點使用靜態的最佳化類型，例如一般 web 傳遞 toodelivery 可快取資產。 順序 tooaccomplish 此替代，在中，您將修改您的網頁 Url toolink 直接 toohello 資產上的 hello 您計劃 toouse 的 CDN 端點。 

例如：`mydynamic.azureedge.net/index.html`是動態，而且是從 hello DSA 端點載入。  hello html 頁面參考多個靜態資產，例如 JavaScript 程式庫，或從已載入的映像 hello 靜態 CDN 端點，例如`mystatic.azureedge.net/banner.jpg`和`mystatic.azureedge.net/scripts.js`。 

您可以找到範例[這裡](https://docs.microsoft.com/azure/cdn/cdn-cloud-service-with-cdn#controller)上 toouse 控制站，在 ASP.NET web 應用程式 tooserve 內容，透過特定的 CDN URL 的方式。




