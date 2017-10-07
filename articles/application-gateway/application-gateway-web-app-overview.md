---
title: "aaaOverview 多租用戶備份的結尾是 Azure 應用程式閘道 |Microsoft 文件"
description: "此頁面會提供多租用戶後結束 hello 應用程式閘道支援的概觀。"
documentationcenter: na
services: application-gateway
author: georgewallace
manager: timlt
editor: 
ms.service: application-gateway
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/26/2017
ms.author: gwallace
ms.openlocfilehash: b7da8c9c68e34bd83ad2b828fab62c00caea354a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="application-gateway-support-for-multi-tenant-back-ends"></a>多租用戶後端的應用程式閘道支援

Azure 應用程式閘道支援以虛擬機器擴展集、網路介面、公用/私人 IP 或完整的網域名稱 (FQDN) 作為其後端集區的一部分。 根據預設，應用程式閘道 hello 用戶端不會變更 hello 連入 HTTP 主機標頭，並傳送 hello 標頭未改變的 toohello 後端。 有許多服務，例如[Azure Web Apps](../app-service-web/app-service-web-overview.md)和[API 管理](../api-management/api-management-key-concepts.md)，為多租用戶的本質，且依賴特定主機標頭或 SNI 延伸 tooresolve toohello 正確的端點。 應用程式閘道現在支援使用者 toooverwrite hello 連入 HTTP 主機標頭以 hello 後端 HTTP 設定為基礎的 hello 功能。 這項功能可支援多租用戶後端進行 Azure Web 應用程式和 API 管理。 這項功能是適用於標準 hello 和 WAF SKU。 多租用戶後端也支援使用 SSL 終止和結束 tooend SSL 案例。

![Web 應用程式案例](./media/application-gateway-web-app-overview/scenario.png)

主機覆寫定義於 hello 能力 toospecify hello HTTP 設定，可以是回套用的 tooany 終止集區規則建立期間。 多租用戶回結束下列兩種方式的覆寫主機標頭和 SNI 延伸模組支援 hello。

1. hello 能力 tooset hello 主機名稱 tooa 固定 hello 中的值的 HTTP 設定。 這項功能可確保該 hello 主機標頭會覆寫 toothis 值的所有流量 toohello 後端集區套用 hello HTTP 設定的位置。 使用時結束 tooend SSL，這個覆寫的主機名稱將用於 hello SNI 延伸模組。 這項功能可讓後端集區伺服器陣列，必須要有 hello 傳入客戶主機標頭與不同的主機標頭的案例。

2. hello 能力 tooderive hello 主機名稱從 hello IP 或 FQDN 的 hello 後端集區成員。 HTTP 設定也會提供選項 toopick hello 主機名稱從後端集區成員的 FQDN，如果設定為使用 hello 選項 tooderive 從個別的後端集區成員的主機名稱。 當使用結束 tooend SSL 時，這個主機名稱就會衍生自 hello FQDN，而且會用於 hello SNI 延伸模組。 這項功能可讓後端集區可以有兩個或多個多租用戶 PaaS 服務，例如 Azure web 應用程式，而 hello 要求的主機標頭 tooeach 成員包含衍生自其 FQDN hello 主機名稱。

> [!NOTE]
> 在這兩個先前案例的 hello hello 設定只會影響 hello 即時流量行為和不 hello 健全狀況探查的行為。 自訂探查已經支援 hello 能力 toospecify hello 探查組態中的主機標頭。 自訂探查時，現在也支援 hello 能力 tooderive hello 主機標頭的行為 hello 目前設定的 HTTP 設定。 這項設定可以指定使用 hello `PickHostNameFromback endAddress` hello 探查組態中的參數。 結束 tooend 功能 toowork，hello 探查和 hello HTTP 設定必須是已修改的 tooreflect hello 正確的組態。

使用這項功能，客戶會指定 hello 選項在 hello HTTP 設定和自訂探查 toohello 適當的組態。 這項設定會接著繫結 tooa 接聽程式和備份集區使用結束的規則。

## <a name="next-steps"></a>後續步驟

深入了解如何 tooset 註冊應用程式閘道與 web 應用程式做為備份結束造訪的集區成員：[設定 App Service web 應用程式與應用程式閘道](application-gateway-web-app-powershell.md)
