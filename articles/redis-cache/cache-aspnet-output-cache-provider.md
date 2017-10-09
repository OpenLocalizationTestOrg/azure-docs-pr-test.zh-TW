---
title: "aaaCache ASP.NET 輸出快取提供者"
description: "深入了解如何使用 Azure Redis 快取 toocache ASP.NET 頁面輸出"
services: redis-cache
documentationcenter: na
author: steved0x
manager: douge
editor: tysonn
ms.assetid: 78469a66-0829-484f-8660-b2598ec60fbf
ms.service: cache
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: cache-redis
ms.workload: tbd
ms.date: 02/14/2017
ms.author: sdanie
ms.openlocfilehash: fc38cc657604b351f55ad8febac383783ac29700
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="aspnet-output-cache-provider-for-azure-redis-cache"></a>Azure Redis 快取的 ASP.NET 輸出快取提供者
hello Redis 輸出快取提供者是輸出快取資料的跨處理序儲存機制。 此資料特別適用於完整 HTTP 回應 (頁面輸出快取)。 hello 提供者插入 hello 新輸出快取提供者擴充性點 ASP.NET 4 中導入。

toouse hello Redis 的輸出快取提供者，先設定您的快取，然後再設定您的 ASP.NET 應用程式使用 hello Redis 輸出快取提供者 NuGet 封裝。 本主題提供指引，設定您的應用程式 toouse hello Redis 輸出快取提供者。 如需建立和設定 Azure Redis 快取執行個體的相關詳細資訊，請參閱 [建立快取](cache-dotnet-how-to-use-azure-redis-cache.md#create-a-cache)。

## <a name="store-aspnet-page-output-in-hello-cache"></a>Hello 快取中儲存 ASP.NET 頁面輸出
tooconfigure 用戶端應用程式，在 Visual Studio 中使用 hello Redis 快取工作階段狀態 NuGet 封裝，按一下**NuGet 套件管理員**， **Package Manager Console**從 hello**工具**功能表。

執行 hello 下列命令從 hello`Package Manager Console`視窗。
    
```
Install-Package Microsoft.Web.RedisOutputCacheProvider
```

hello Redis 輸出快取提供者 NuGet 封裝 hello StackExchange.Redis.StrongName 封裝上具有相依性。 如果 hello StackExchange.Redis.StrongName 封裝不存在專案中，它會安裝。 如需 hello Redis 輸出快取提供者 NuGet 封裝的詳細資訊，請參閱 hello [RedisOutputCacheProvider](https://www.nuget.org/packages/Microsoft.Web.RedisOutputCacheProvider/) NuGet 頁面。

>[!NOTE]
>在加法 toohello 強式名稱 StackExchange.Redis.StrongName 封裝，還有 hello StackExchange.Redis 非強式命名版本。 如果您的專案使用 hello 非強式命名 StackExchange.Redis 版本必須先解除安裝，否則您發生命名衝突專案中。 如需這些封裝的相關詳細資訊，請參閱 [設定 .NET 快取用戶端](cache-dotnet-how-to-use-azure-redis-cache.md#configure-the-cache-clients)。
>
>

hello NuGet 封裝下載並新增 hello 需要組件參考，並新增下列區段到您的 web.config 檔案的 hello。 本節包含您 ASP.NET 應用程式 toouse hello Redis 輸出快取提供者的 hello 必要的設定。

```xml
<caching>
  <outputCachedefault Provider="MyRedisOutputCache">
    <providers>
      <!--
      <add name="MyRedisOutputCache"
        host = "127.0.0.1" [String]
        port = "" [number]
        accessKey = "" [String]
        ssl = "false" [true|false]
        databaseId = "0" [number]
        applicationName = "" [String]
        connectionTimeoutInMilliseconds = "5000" [number]
        operationTimeoutInMilliseconds = "5000" [number]
      />
      -->
      <add name="MyRedisOutputCache" type="Microsoft.Web.Redis.RedisOutputCacheProvider" host="127.0.0.1" accessKey="" ssl="false"/>
    </providers>
  </outputCache>
</caching>
```

hello 標記為註解 > 一節提供 hello 屬性和每個屬性的範例設定的範例。

設定您在 hello Microsoft Azure 入口網站的快取刀鋒伺服器中的 hello 值 hello 屬性並設定 hello 所需的其他值。 如需存取快取屬性的指示，請參閱 [設定 Redis 快取設定](cache-configure.md#configure-redis-cache-settings)。

* **主機** – 指定您的快取端點。
* **連接埠**– 使用非 SSL 連接埠或您的 SSL 連接埠，取決於 hello ssl 設定。
* **accessKey** – 用於您的快取中的任一 hello 主要或次要金鑰。
* **ssl** – 如果您想要以 ssl toosecure 快取/用戶端通訊，則為 true，否則為 false。 為確定 toospecify hello 正確的連接埠。
  * 新的快取預設為停用 hello 非 SSL 連接埠。 指定 true，此設定 toouse hello SSL 連接埠。 如需有關如何啟用 hello 非 SSL 連接埠的詳細資訊，請參閱 hello[存取連接埠](cache-configure.md#access-ports)> 一節中 hello[設定快取](cache-configure.md)主題。
* **databaseId** – 指定快取哪些資料庫 toouse 輸出資料。 如果未指定，會使用 hello 預設值為 0。
* **applicationName** – 金鑰在 redis 中會儲存為 `<AppName>_<SessionId>_Data`。 這個命名配置可讓多個應用程式 tooshare hello 相同索引鍵。 此參數是選擇性的，如果您未提供，將會使用預設值。
* **connectionTimeoutInMilliseconds** – 此設定可讓您 toooverride hello connectTimeout hello StackExchange.Redis 用戶端中設定。 如果未指定，會使用 hello 預設 connectTimeout 值為 5000。 如需詳細資訊，請參閱 [StackExchange.Redis 設定模型](http://go.microsoft.com/fwlink/?LinkId=398705)(英文)。
* **operationTimeoutInMilliseconds** – 此設定可讓您 toooverride hello syncTimeout hello StackExchange.Redis 用戶端中設定。 如果未指定，會使用 hello syncTimeout 預設為 1000年。 如需詳細資訊，請參閱 [StackExchange.Redis 設定模型](http://go.microsoft.com/fwlink/?LinkId=398705)(英文)。

新增您想 toocache hello 輸出 OutputCache 指示詞 tooeach 頁面。

```
<%@ OutputCache Duration="60" VaryByParam="*" %>
```

Hello 上述範例中，在 hello 快取頁面 hello 快取中的資料仍會保留 60 秒，而每一個參數組合快取不同版本的 hello 頁面。 如需 hello OutputCache 指示詞的詳細資訊，請參閱[ @OutputCache ](http://go.microsoft.com/fwlink/?linkid=320837)。

一旦執行了這些步驟，您的應用程式是設定的 toouse hello Redis 輸出快取提供者。

## <a name="next-steps"></a>後續步驟
簽出 hello [Azure Redis 快取的 ASP.NET 工作階段狀態提供者](cache-aspnet-session-state-provider.md)。

