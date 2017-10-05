---
title: "Azure CDN 中的 HTTP/2 支援 | Microsoft Docs"
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
ms.openlocfilehash: 4f8dd685c3ae89535217d7a17a01c5129ca7e6e4
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="http2-support-in-azure-cdn"></a>Azure CDN 中的 HTTP/2 支援

HTTP/2 是主要 HTTP/1.1\ 有所修訂。 它會提供更快速 web 效能、 降低的回應時間，以及改善的使用者體驗，同時維持類似的 HTTP 方法，狀態碼和語意。 雖然 HTTP/2 是設計來搭配 HTTP 和 HTTPS，但許多用戶端 Web 瀏覽器僅支援透過 TLS 使用 HTTP/2。

###<a name="http2-benefits"></a>HTTP/2 的優點

HTTP/2 的優點包括︰

*   **多工和並行**

    使用 HTTP 1.1 時，多方提出多個資源要求需要多個 TCP 連線，每個連線都有其相關聯的效能負荷。 HTTP/2 允許在單一 TCP 連線上要求多個資源。

*   **標頭壓縮**

    將提供的資源壓縮 HTTP 標頭，可大幅縮短網路上的時間。

*   **資料流相依性**

    資料流相依性可讓用戶端向伺服器表示哪個資源最優先。


##<a name="http2-browser-support"></a>HTTP/2 瀏覽器支援

所有主要瀏覽器都已在其目前的版本中實作 HTTP/2 支援。 不支援的瀏覽器會自動降回 HTTP/1.1。

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

若要了解 HTTP/2 在實務上的優點，請參閱 [Akamai 的這個示範](https://http2.akamai.com/demo)。

若要深入了解 HTTP/2，請瀏覽下列資源：

*   [HTTP/2 規格首頁](https://http2.github.io/)
*   [官方 HTTP/2 常見問題集](https://http2.github.io/faq/)
*   [Akamai HTTP/2 資訊](https://http2.akamai.com/)

若要深入了解 Azure CDN 提供的功能，請參閱 [Azure CDN 概觀](https://azure.microsoft.com/documentation/articles/cdn-overview/)。