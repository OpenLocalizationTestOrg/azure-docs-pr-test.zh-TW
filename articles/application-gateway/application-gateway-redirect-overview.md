---
title: "Azure 應用程式閘道的重新導向概觀 | Microsoft Docs"
description: "了解 Azure 應用程式閘道的重新導向功能"
services: application-gateway
documentationcenter: na
author: amsriva
manager: timlt
editor: 
tags: azure-resource-manager
ms.service: application-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/18/2017
ms.author: amsriva
ms.openlocfilehash: ea9ae8373ff67bf9557b06bbc8a4b0d82a03e2d0
ms.sourcegitcommit: 6699c77dcbd5f8a1a2f21fba3d0a0005ac9ed6b7
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/11/2017
---
# <a name="application-gateway-redirect-overview"></a>應用程式閘道重新導向概觀

許多 Web 應用程式的常見案例是支援自動 HTTP 至 HTTPS 的重新導向，以確保應用程式與其使用者之間的通訊會透過加密的路徑進行。 在過去，客戶會使用一些技巧 (例如建立專屬後端集區)，其唯一目的是要將其在 HTTP 上接收的要求重新導向至 HTTPS。  應用程式閘道現在支援應用程式閘道上重新導向流量的功能。 這可簡化應用程式組態、將資源使用量最佳化，並支援新的重新導向案例，包括全域和路徑式重新導向。 應用程式閘道重新導向支援不只限於 HTTP -> HTTPS 重新導向。 這是泛型重新導向機制，可將在一個接聽程式接收的流量重新導向至應用程式閘道上的另一個接聽程式。 它也支援重新導向至外部網站。 應用程式閘道重新導向提供下列功能：

1. 從閘道上的一個接聽程式到另一個接聽程式的全域重新導向。 這允許在網站上進行 HTTP 至 HTTPS 重新導向。
2. 路徑式重新導向。 這類型的重新導向只允許在特定網站區域上進行 HTTP 至 HTTPS 重新導向，例如以 /cart/* 表示的購物車區域。
3. 重新導向至外部網站。

![重新導向](./media/application-gateway-redirect-overview/redirect.png)

有了這項變更，客戶必須建立新的重新導向組態物件，以指定重新導向所需的目標接聽程式或外部網站。 此組態元素也支援能將 URI 路徑和查詢字串附加至重新導向之 URL 的選項。 客戶也可以選擇重新導向為暫時 (HTTP 狀態碼 302) 或永久重新導向 (HTTP 狀態碼 301)。 一旦建立，此重新導向組態會透過新規則附加至來源接聽程式。 若使用時基本規則，重新導向組態會與來源接聽程式相關聯並為全域重新導向。 若使用路徑式規則，重新導向組態會定義於 URL 路徑圖上，因此僅適用於網站的特定路徑區域。

### <a name="next-steps"></a>後續步驟

[在應用程式閘道上設定 URL 重新導向](application-gateway-configure-redirect-powershell.md)
