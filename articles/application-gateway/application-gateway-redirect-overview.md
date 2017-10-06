---
title: "Azure 應用程式閘道 aaaRedirect 概觀 |Microsoft 文件"
description: "深入了解 Azure 應用程式閘道中的 hello 重新導向功能"
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
ms.openlocfilehash: 7149e3bd000d336c51995fb0e90f971b4d9ba2be
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="application-gateway-redirect-overview"></a>應用程式閘道重新導向概觀

許多 web 應用程式的常見案例是 toosupport 自動 HTTP tooHTTPS 重新導向 tooensure 應用程式和其使用者之間的通訊會透過加密的路徑。 在 hello 過去，客戶使用的技術，例如建立專用的後端集區，其唯一目的是 tooredirect HTTP tooHTTPS 收到的要求。  應用程式閘道現在支援能力 tooredirect 流量上 hello 應用程式閘道。 這可簡化應用程式組態、 最佳化 hello 資源使用狀況，並支援新的重新導向案例，包括全域和路徑為基礎的重新導向。 應用程式閘道重新導向支援不限於 tooHTTP]-> [HTTPS 單獨的重新導向。 這是流量的泛型的重新導向的機制，可在應用程式閘道上的一個接聽程式 tooanother 接聽程式接收重新導向。 它也支援重新導向 tooan 外部站台。 應用程式閘道重新導向的支援會提供下列功能的 hello:

1. 從一個接聽程式 tooanother 接聽 hello 閘道的全域重新導向。 這可讓站台上的 HTTP tooHTTPS 重新導向。
2. 路徑式重新導向。 重新導向的這個類型可讓 HTTP tooHTTPS 重新導向只有在特定站台的區域中，例如購物車區域表示/車 / *。
3. 重新導向 tooexternal 站台。

![重新導向](./media/application-gateway-redirect-overview/redirect.png)

透過這項變更，客戶需要 toocreate 新重新導向設定物件，指定 hello 目標接聽程式，或想要使用外部網站 toowhich 重新導向。 hello 組態項目也支援選項 tooenable 附加 hello URI 的路徑和查詢字串 toohello 重新導向 URL。 客戶也可以選擇重新導向為暫時 (HTTP 狀態碼 302) 或永久重新導向 (HTTP 狀態碼 301)。 一旦建立此重新導向設定是透過新的規則附加的 toohello 來源接聽程式。 使用時的基本規則，hello 重新導向組態與來源的接聽程式相關聯，是通用的重新導向。 使用路徑規則時，定義上 hello URL 路徑對應 hello 重新導向設定，以及因此僅適用於 toohello 特定路徑區域中的站台。

### <a name="next-steps"></a>後續步驟

[在應用程式閘道上設定 URL 重新導向](application-gateway-configure-redirect-powershell.md)
