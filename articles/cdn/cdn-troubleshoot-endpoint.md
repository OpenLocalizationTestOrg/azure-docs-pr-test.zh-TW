---
title: "傳回 404 狀態 aaaTroubleshooting Azure CDN 端點 |Microsoft 文件"
description: "針對 Azure CDN 端點的 404 回應碼進行疑難排解。"
services: cdn
documentationcenter: 
author: zhangmanling
manager: erikre
editor: 
ms.assetid: b588a1eb-ab69-4fc7-ae4d-157c3e46f4a8
ms.service: cdn
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: mazha
ms.openlocfilehash: 450bfbd641c869cfd88169a12c4b69819eaa7c26
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-cdn-endpoints-returning-404-statuses"></a>針對傳回 404 狀態的 CDN 端點進行疑難排解
這篇文章可協助您針對 [CDN 端點](cdn-create-new-endpoint.md) 傳回 404 錯誤的問題進行疑難排解。

如果您需要更多說明，在本文中的任何時間點，您可以連絡上 hello Azure 專家[hello MSDN Azure 和 hello 堆疊溢位論壇](https://azure.microsoft.com/support/forums/)。 或者，您也可以提出 Azure 支援事件。 移 toohello [Azure 支援服務網站](https://azure.microsoft.com/support/options/)，然後按一下 **取得支援**。

## <a name="symptom"></a>徵狀
您已建立 CDN 設定檔和端點，但您的內容似乎不是用於 hello CDN toobe。  如果使用者嘗試 tooaccess hello CDN URL 透過內容接收 HTTP 404 狀態碼。 

## <a name="cause"></a>原因
有幾個可能的原因，包括︰

* hello 檔案的來源不可見 toohello CDN
* hello 端點設定不正確，導致 hello 錯誤的位置中的 hello CDN toolook
* hello 主機會拒絕從 hello CDN hello 主機標頭
* hello 端點尚未有時間 toopropagate 整個 hello CDN

## <a name="troubleshooting-steps"></a>疑難排解步驟
> [!IMPORTANT]
> 建立 CDN 端點之後, 它將不立即可供使用，因為它需要花費一些時間透過 hello CDN hello 註冊 toopropagate。  若為 <b>來自 Akamai 的 Azure CDN</b> 設定檔，通常會在一分鐘之內完成傳播。  若為<b>來自 Verizon 的 Azure CDN</b> 設定檔，則通常會在 90 分鐘之內完成傳播，但在某些情況下可能會更久。  如果您完成 hello 步驟在此文件，而且您仍然收到 404 回應，等待幾個小時 toocheck 再次開啟支援票證之前，請考慮。
> 
> 

### <a name="check-hello-origin-file"></a>核取 hello 來源檔案
首先，我們應該確認 hello 我們想要快取該 hello 檔案上我們來源可用，而且是可公開存取。  hello 是 tooopen 瀏覽器在私用或 Incognito 工作階段中的最快速方式 toodo 並直接瀏覽 toohello 檔案。  只輸入或貼入 hello 地址 方塊中的 hello URL，並查看是否，導致您預期的 hello 檔案。  針對此範例中，我們即將 toouse 我有 Azure 儲存體帳戶可存取的檔案`https://cdndocdemo.blob.core.windows.net/publicblob/lorem.txt`。  如您所見，它已順利通過 hello 測試。

![成功！](./media/cdn-troubleshoot-endpoint/cdn-origin-file.png)

> [!WARNING]
> 雖然這是最快的 hello 和最簡單的方式 tooverify 您檔案是公開使用，某些組織中的網路設定可以讓您 hello 這個檔案是公開可用時，事實上，只顯示 toousers 的網路 （假象即使它裝載在 Azure 中）。  如果您有外部的瀏覽器，您可以從此處測試，例如在不是行動裝置連線 tooyour 組織的網路或在 Azure 中虛擬機器，那就是最佳方法。
> 
> 

### <a name="check-hello-origin-settings"></a>請檢查 hello 原始設定
既然我們已經確認 hello 檔案位於可公開 hello 網際網路，我們應該確認我們原始設定。  在 hello [Azure 入口網站](https://portal.azure.com)、 瀏覽 tooyour 的 CDN 設定檔，然後按一下您正在進行疑難排解的 hello 端點。  在 hello 產生**端點**刀鋒視窗中，按一下 hello 原點。  

![來源反白的端點刀鋒視窗](./media/cdn-troubleshoot-endpoint/cdn-endpoint.png)

hello**原點**刀鋒視窗隨即出現。 

![原始刀鋒視窗](./media/cdn-troubleshoot-endpoint/cdn-origin-settings.png)

#### <a name="origin-type-and-hostname"></a>來源類型和主機名稱
確認 hello**來源類型**均正確無誤，請確認 hello**來源主機名稱**。  在範例中， `https://cdndocdemo.blob.core.windows.net/publicblob/lorem.txt`，URL 是的 hello hello hostname 部分`cdndocdemo.blob.core.windows.net`。  您可以看到 hello 螢幕擷取畫面中，這是正確的。  Azure 儲存體、 Web 應用程式和雲端服務的原始來源，hello**來源主機名稱**欄位是下拉式清單中，所以我們不需要 tooworry 有關拼寫正確。  不過，如果您使用的是自訂來源，則您的主機名稱的拼字正確便「十分重要」  ！

#### <a name="http-and-https-ports"></a>HTTP 和 HTTPS 連接埠
hello 其他的事情 toocheck 是您**HTTP**和**HTTPS 連接埠**。  在大部分情況下，80 和 443 皆正確，而且您不需要進行任何變更。  不過，如果 hello 原始伺服器正在接聽不同的通訊埠，將需要 toobe 表示。  如果您不確定，只查看 hello 來源檔案的 URL。  hello HTTP 和 HTTPS 規格指定連接埠 80 和 443 做為 hello 預設值。 在 URL 中， `https://cdndocdemo.blob.core.windows.net/publicblob/lorem.txt`，未指定連接埠，因此會假設 hello 預設值是 443，而且我的設定正確無誤。  

不過，在您稍早進行測試的來源檔案是說出 hello URL `http://www.contoso.com:8080/file.txt`。  請注意 hello `:8080` hello hello hostname 區段結尾處。  會告訴 hello 瀏覽器 toouse 連接埠`8080`tooconnect toohello web 伺服器`www.contoso.com`，因此您必須在 hello tooenter 8080 **HTTP 連接埠**欄位。  它是重要 toonote，這些連接埠設定只會影響哪些連接埠 hello 端點會使用從 hello 原點 tooretrieve 資訊。

> [!NOTE]
> **Azure CDN 從 Akamai**端點不允許 hello 完整 TCP 連接埠範圍的來源。  如需不允許的原始連接埠清單，請參閱 [來自 Akamai 的 Azure CDN 允許的原始連接埠](https://msdn.microsoft.com/library/mt757337.aspx)。  
> 
> 

### <a name="check-hello-endpoint-settings"></a>請檢查 hello 端點設定
在 [hello**端點**刀鋒視窗中，按一下 hello**設定**] 按鈕。

![以反白顯示設定按鈕的端點刀鋒視窗](./media/cdn-troubleshoot-endpoint/cdn-endpoint-configure-button.png)

hello 端點的**設定**刀鋒視窗隨即出現。

![設定刀鋒視窗](./media/cdn-troubleshoot-endpoint/cdn-configure.png)

#### <a name="protocols"></a>通訊協定
如**通訊協定**，確認已選取 hello hello 用戶端所使用的通訊協定。  hello hello 用戶端所使用的相同通訊協定會使用其中一種 tooaccess hello 原點，因此您很重要的 toohave hello 來源連接埠 hello 前一節中正確設定的 hello。  此外，hello 端點只會在 hello 預設 HTTP 和 HTTPS 連接埠 （80 和 443），不論 hello 來源連接埠上接聽。

讓我們回到 tooour 假設的範例與`http://www.contoso.com:8080/file.txt`。  您應該還記得之前 Contoso 指定 `44300` 做為其 HTTP 連接埠，但我們也假設其指定 `8080` 做為 HTTPS 連接埠。  如果他們建立名為 `contoso` 的端點，其 CDN 端點的主機名稱會是 `contoso.azureedge.net`。  要求`http://contoso.azureedge.net/file.txt`是 HTTP 要求，因此 hello 端點將會使用 HTTP 連接埠 8080 tooretrieve 上從 hello 原點。  會透過 HTTPS 的安全要求`https://contoso.azureedge.net/file.txt`，擷取 hello hello 的原始檔時，會導致 hello 端點 toouse HTTPS 連接埠 44300 上。

#### <a name="origin-host-header"></a>原始主機標頭
hello**原始主機標頭**hello 主機標頭值傳送 toohello 原點，隨著每項要求。  在大部分情況下，這應該是 hello 相同為 hello**來源主機名稱**我們稍早驗證。  不正確的值，這個欄位中通常不會造成 404 狀態，而可能 toocause 其他 4xx 狀態，根據需要哪些 hello 原點。

#### <a name="origin-path"></a>原始路徑
最後，我們應該確認 **原始路徑**。  依預設這會是空白。  如果您想 toonarrow hello 範圍，您應該只使用此欄位要 toomake hello CDN 上可用的 hello 原點裝載的資源。  

例如，在我的端點，我想要的所有資源上可用的我儲存體帳戶 toobe 讓我保持**原始路徑**空白。  這表示要求太`https://cdndocdemo.azureedge.net/publicblob/lorem.txt`太產生從我的端點連接`cdndocdemo.core.windows.net`要求`/publicblob/lorem.txt`。  同樣地，針對要求`https://cdndocdemo.azureedge.net/donotcache/status.png`hello 端點要求會導致`/donotcache/status.png`從 hello 原點。

但如果想 toouse hello CDN 每個路徑上我的來源？  假設我只是想 tooexpose hello`publicblob`路徑。  如果我輸入*/publicblob*在我**原始路徑**欄位中，將導致 hello 端點 tooinsert */publicblob*進行 toohello 原點每個要求之前。  這表示該 hello 要求`https://cdndocdemo.azureedge.net/publicblob/lorem.txt`現在實際上會 hello 要求一部分 hello URL `/publicblob/lorem.txt`，並附加`/publicblob`toohello 開頭。 這會導致的要求`/publicblob/publicblob/lorem.txt`從 hello 原點。  如果該路徑未解析 tooan 實際的檔案，請 hello 來源會傳回 404 狀態。  hello 正確 URL tooretrieve lorem.txt 在此範例實際上是`https://cdndocdemo.azureedge.net/lorem.txt`。  請注意，我們不包含 hello */publicblob*路徑，因為 hello 要求一部分 hello URL 是`/lorem.txt`並 hello 端點加入`/publicblob`，並產生`/publicblob/lorem.txt`hello 要求傳遞 toohello 來源.

