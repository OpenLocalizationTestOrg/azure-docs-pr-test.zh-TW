---
title: "在 Azure CDN aaaTroubleshooting 檔案壓縮 |Microsoft 文件"
description: "針對 Azure CDN 檔案壓縮的問題進行疑難排解。"
services: cdn
documentationcenter: 
author: zhangmanling
manager: erikre
editor: 
ms.assetid: a6624e65-1a77-4486-b473-8d720ce28f8b
ms.service: cdn
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: mazha
ms.openlocfilehash: f00b98beaf6b3b3cd30108ece65a8191edc06ff5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-cdn-file-compression"></a>CDN 檔案壓縮疑難排解
這篇文章可協助您針對 [CDN 檔案壓縮](cdn-improve-performance.md)的問題進行疑難排解。

如果您需要更多說明，在本文中的任何時間點，您可以連絡上 hello Azure 專家[hello MSDN Azure 和 hello 堆疊溢位論壇](https://azure.microsoft.com/support/forums/)。 或者，您也可以提出 Azure 支援事件。 移 toohello [Azure 支援服務網站](https://azure.microsoft.com/support/options/)按一下**取得支援**。

## <a name="symptom"></a>徵狀
已為您的端點啟用壓縮，但會傳回未壓縮的檔案。

> [!TIP]
> toocheck 檔案會被傳回壓縮，是否需要一種工具要的 toouse [Fiddler](http://www.telerik.com/fiddler)或您的瀏覽器[開發人員工具](https://developer.microsoft.com/microsoft-edge/platform/documentation/f12-devtools-guide/)。  核取 hello HTTP 回應標頭傳回您的快取 CDN 內容。  如果名為 `Content-Encoding` 的標頭有 **gzip**、**bzip2** 或 **deflate** 值，內容會進行壓縮。
> 
> ![Content-Encoding 標頭](./media/cdn-troubleshoot-compression/cdn-content-header.png)
> 
> 

## <a name="cause"></a>原因
有幾個可能的原因，包括︰

* hello 要求內容不符合資格的壓縮。
* 無法啟用壓縮 hello 要求的檔案類型。
* hello HTTP 要求不包含標頭要求有效的壓縮類型。

## <a name="troubleshooting-steps"></a>疑難排解步驟
> [!TIP]
> 與部署新的端點，CDN 的設定變更都會透過 hello 網路某些時間 toopropagate。  變更通常會在 90 分鐘內套用。  如果這是 hello 您為您的 CDN 端點設定壓縮的第一次，您應該考慮等候 1-2 小時 toobe 確定 hello 壓縮設定都已傳播 toohello 快顯。 
> 
> 

### <a name="verify-hello-request"></a>確認 hello 要求
首先，我們應該進行 hello 要求快速例行性檢查。  您可以使用您的瀏覽器[開發人員工具](https://developer.microsoft.com/microsoft-edge/platform/documentation/f12-devtools-guide/)tooview hello 提出的要求。

* 請確認正在傳送嗨要求 tooyour 端點 URL， `<endpointname>.azureedge.net`，並不是您的原點。
* 請確認 hello 要求包含**Accept-encoding**該標頭包含標頭和 hello 值**gzip**， **deflate**，或**bzip2**.

> [!NOTE]
> **來自 Akamai 的 Azure CDN** 設定檔只支援 **gzip** 編碼。
> 
> 

![CDN 要求標頭](./media/cdn-troubleshoot-compression/cdn-request-headers.png)

### <a name="verify-compression-settings-standard-cdn-profile"></a>驗證壓縮設定 (標準 CDN 設定檔)
> [!NOTE]
> 如果您的 CDN 設定檔是**來自 Akamai 的 Azure CDN 標準**或**來自 Verizon 的 Azure CDN 標準**設定檔，才能套用此步驟。 
> 
> 

瀏覽在 hello tooyour 端點[Azure 入口網站](https://portal.azure.com)按一下 hello**設定** 按鈕。

* 驗證已啟用壓縮。
* 請確認 hello 內容 toobe 壓縮隨附的壓縮格式的 hello 清單中的 hello MIME 類型。

![CDN 壓縮設定](./media/cdn-troubleshoot-compression/cdn-compression-settings.png)

### <a name="verify-compression-settings-premium-cdn-profile"></a>驗證壓縮設定 (進階 CDN 設定檔)
> [!NOTE]
> 如果您的 CDN 設定檔是 **來自 Verizon 的 Azure CDN 進階** 設定檔，才能套用此步驟。
> 
> 

瀏覽在 hello tooyour 端點[Azure 入口網站](https://portal.azure.com)按一下 hello**管理** 按鈕。  hello 補充入口網站將會開啟。  暫留在 hello **HTTP 大型** 索引標籤，然後暫留在 hello**快取設定**彈出式視窗。  按一下 [壓縮]。 

* 驗證已啟用壓縮。
* 確認 hello**檔案類型**清單包含以逗號分隔清單 （無空格） 的 MIME 類型。
* 請確認 hello 內容 toobe 壓縮隨附的壓縮格式的 hello 清單中的 hello MIME 類型。

![CDN 進階壓縮設定](./media/cdn-troubleshoot-compression/cdn-compression-settings-premium.png)

### <a name="verify-hello-content-is-cached"></a>確認 hello 內容會快取
> [!NOTE]
> 如果您的 CDN 設定檔是 **來自 Verizon 的 Azure CDN** 設定檔 (標準或進階)，才能套用此步驟。
> 
> 

使用瀏覽器的開發人員工具，請檢查 hello 回應標頭 tooensure hello 檔案會快取，它所要求的 hello 區域中。

* 檢查 hello**伺服器**回應標頭。  hello 標頭應該具有 hello 格式**平台 (POP/伺服器 ID)**、 hello 下列範例所示。
* 檢查 hello **X 快取**回應標頭。  hello 標頭應該閱讀**叫用**。  

![CDN 回應標頭](./media/cdn-troubleshoot-compression/cdn-response-headers.png)

### <a name="verify-hello-file-meets-hello-size-requirements"></a>確認 hello 檔案符合 hello 大小需求
> [!NOTE]
> 如果您的 CDN 設定檔是 **來自 Verizon 的 Azure CDN** 設定檔 (標準或進階)，才能套用此步驟。
> 
> 

toobe 能夠壓縮，檔案必須符合下列大小需求的 hello:

* 超過 128 個位元組。
* 小於 1 MB。

### <a name="check-hello-request-at-hello-origin-server-for-a-via-header"></a>檢查 hello 要求在原始伺服器 hello**透過**標頭
hello**透過**HTTP 標頭顯示由 proxy 伺服器傳遞 toohello hello 要求的網頁伺服器。  Microsoft IIS web 伺服器，預設不會壓縮回應 hello 要求包含當**透過**標頭。  toooverride 這種行為，執行下列 hello:

* **IIS 6**:[設定 HcNoCompressionForProxies ="FALSE"hello IIS Metabase 內容中](https://msdn.microsoft.com/library/ms525390.aspx)
* **IIS 7 版與**:[同時設定**noCompressionForHttp10**和**noCompressionForProxies** tooFalse hello 伺服器設定中](http://www.iis.net/configreference/system.webserver/httpcompression)

