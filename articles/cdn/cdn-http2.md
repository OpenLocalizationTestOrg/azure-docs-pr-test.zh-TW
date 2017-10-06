---
title: "在 Azure CDN 的 aaaHTTP/2 支援 |Microsoft 文件"
description: "了解 HTTP/2 和 CDN 支援。"
services: cdn
documentationcenter: 
author: lichard
manager: erikre
editor: 
ms.service: cdn
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 5/04/2017
ms.author: rli
ms.openlocfilehash: 2e5e5345e8cf5c40e080ebf18b4f13a239a5aac5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="http2-support-in-azure-cdn"></a>Azure CDN 中的 HTTP/2 支援

HTTP/2 是重大修訂 tooHTTP/1.1\。 它會提供更快速 web 效能、 降低的回應時間，以及改善的使用者體驗，同時維持 hello 熟悉的 HTTP 方法，狀態碼和語意。 雖然 HTTP/2 是設計的 toowork HTTP 及 HTTPS，許多用戶端 web 瀏覽器僅支援 HTTP/2 5060，TLS。

###<a name="http2-benefits"></a>HTTP/2 的優點

HTTP/2 hello 優點包括：

*   **多工和並行**

    使用 HTTP 1.1 時，多方提出多個資源要求需要多個 TCP 連線，每個連線都有其相關聯的效能負荷。 HTTP/2 可讓多個資源 toobe 在單一 TCP 連接要求。

*   **標頭壓縮**

    藉由壓縮提供資源的 hello HTTP 標頭，已大幅降低 hello 網路上的時間。

*   **資料流相依性**

    資料流的相依性允許 hello 用戶端 tooindicate toohello 伺服器資源的優先順序。


##<a name="http2-browser-support"></a>HTTP/2 瀏覽器支援

所有主要瀏覽器 hello 未實作 HTTP/2 支援在其目前的版本。 不支援的瀏覽器將會自動後援 tooHTTP/1.1。

|[瀏覽器]|最低版本|
|-------------|------------|
|Microsoft Edge| 12|
|Google Chrome| 43|
|Mozilla Firefox| 38|
|Opera| 32|
|Safari| 9|

##<a name="enabling-http2-support-in-azure-cdn"></a>啟用 Azure CDN 中的 HTTP/2 支援

目前，**Akamai 的 Azure CDN** 和 **Verizon 的 Azure CDN** 設定檔已支援 HTTP/2。 客戶不需要採取任何動作。

##<a name="next-steps"></a>後續步驟

toosee hello 優點 HTTP/2 的動作，請參閱[Akamai 從這個示範](https://http2.akamai.com/demo)。

toolearn 深入了解 HTTP/2，請造訪 hello 下列資源：

*   [HTTP/2 規格首頁](https://http2.github.io/)
*   [官方 HTTP/2 常見問題集](https://http2.github.io/faq/)
*   [Akamai HTTP/2 資訊](https://http2.akamai.com/)

toolearn 進一步了解 Azure CDN 提供的功能，請參閱 hello [Azure CDN 概觀](https://azure.microsoft.com/documentation/articles/cdn-overview/)。
