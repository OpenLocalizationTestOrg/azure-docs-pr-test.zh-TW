---
title: "aaaEnabling 結束 tooend Azure 應用程式閘道上的 SSL |Microsoft 文件"
description: "此頁面提供 SSL 支援 hello 應用程式閘道結束 tooend 的概觀。"
documentationcenter: na
services: application-gateway
author: amsriva
manager: rossort
editor: amsriva
ms.assetid: 3976399b-25ad-45eb-8eb3-fdb736a598c5
ms.service: application-gateway
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.custom: H1Hack27Feb2017
ms.workload: infrastructure-services
ms.date: 07/19/2017
ms.author: amsriva
ms.openlocfilehash: c5cb398a1e7d9a08662a3120baad98edb5575917
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="overview-of-end-tooend-ssl-with-application-gateway"></a>結束 tooend SSL 與應用程式閘道的概觀

應用程式閘道支援在 hello 閘道進行 SSL 終止後通常流動的流量加密 toohello 後端伺服器。 這項功能可讓 web 伺服器 toobe unburdened 從昂貴加密和解密的額外負荷。 但是對某些客戶未加密的通訊 toohello 後端伺服器不是可接受的選項。 此未加密的通訊可能是因為 toosecurity 需求，相容性需求，或 hello 應用程式可能只接受安全的連線。 針對這類應用程式，應用程式閘道支援結束 tooend SSL 加密。

## <a name="overview"></a>概觀

結束 tooend SSL 可讓您 toosecurely 傳輸時仍利用 hello 7 層負載平衡功能的優點的應用程式閘道提供加密的敏感性資料 toohello 後端。 這其中部分功能會以 cookie 為基礎的工作階段親和性、 URL 為基礎的路由、 支援路由根據站台或能力 tooinject 轉寄-X * 標頭。

設定為結束 tooend SSL 通訊模式時，應用程式閘道會終止在 hello 閘道 hello SSL 工作階段，並解密使用者流量。 然後再套用設定的 hello 規則 tooselect 適當的後端集區執行個體 tooroute 流量。 應用程式閘道會起始新的 SSL 連接 toohello 後端伺服器，然後重新加密資料前傳送嗨要求 toohello 後端使用 hello 後端伺服器的公開金鑰憑證。 結束 tooend BackendHTTPSetting tooHTTPS，接著在將通訊協定設定啟用 SSL 套用 tooa 後端集區。 Hello 與結束 tooend 啟用 SSL 的後端集區中每個後端伺服器必須設定憑證 tooallow 安全通訊。

![結束 tooend ssl 案例][1]

在此範例中，使用 TLS1.2 的要求使用 SSL 的結束 tooend Pool1 中的路由的 toobackend 伺服器。

## <a name="end-tooend-ssl-and-whitelisting-of-certificates"></a>結束 tooend SSL 和憑證的允許清單

應用程式閘道只會與 hello 應用程式閘道使用其憑證有在允許清單中的已知的後端執行個體通訊。 tooenable 允許清單的憑證，您必須上傳 hello 公開金鑰的後端伺服器憑證 toohello 應用程式閘道 （不 hello 根憑證）。 然後允許只有連線 tooknown 和白名單後端。 hello 剩餘後端會導致閘道時發生錯誤。 自我簽署憑證僅供測試之用，並不建議用於生產工作負載。 這類憑證有 toobe 在允許清單與 hello 應用程式閘道 hello 才可以使用先前步驟中所述。

## <a name="next-steps"></a>後續步驟

在了解結束 tooend SSL 之後, 請繼續太[啟用應用程式閘道結束 tooend SSL](application-gateway-end-to-end-ssl-powershell.md) toocreate 應用程式閘道使用結束 tooend SSL。

<!--Image references-->

[1]: ./media/application-gateway-backend-ssl/scenario.png
