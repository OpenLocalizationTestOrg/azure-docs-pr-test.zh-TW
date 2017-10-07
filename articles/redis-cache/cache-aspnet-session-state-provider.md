---
title: "ASP.NET 工作階段狀態提供者 aaaCache |Microsoft 文件"
description: "深入了解如何使用 Azure Redis 快取 toostore ASP.NET 工作階段狀態"
services: redis-cache
documentationcenter: na
author: steved0x
manager: douge
editor: tysonn
ms.assetid: 192f384c-836a-479a-bb65-8c3e6d6522bb
ms.service: cache
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: cache-redis
ms.workload: tbd
ms.date: 05/01/2017
ms.author: sdanie
ms.openlocfilehash: 9ea84cf67b9314b15dce696f596d399921194510
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="aspnet-session-state-provider-for-azure-redis-cache"></a>Azure Redis 快取的 ASP.NET 工作階段狀態提供者
Azure Redis 快取提供工作階段狀態提供者，您可以使用 toostore 快取，而不是記憶體中工作階段狀態，或在 SQL Server 資料庫中。 toouse hello 快取工作階段狀態提供者，先設定您的快取，然後設定 快取使用 hello Redis 快取工作階段狀態 NuGet 封裝您的 ASP.NET 應用程式。

通常不是實際在真實世界雲端應用程式 tooavoid 某種形式的狀態儲存使用者工作階段，但某些方法會影響效能和延展性比其他更多。 如果您有 toostore 狀態，hello 最佳解決方案是 tookeep hello 數量小狀態，並將它儲存在 cookie 中。 如果此方法不可行，hello 的下一個最佳解決方案是 toouse ASP.NET 工作階段狀態與分散式、 記憶體中快取提供者。 hello 效能和延展性的觀點而言最差的解決方式是 toouse 資料庫備份的工作階段狀態提供者。 本主題提供使用 Azure Redis 快取的 hello ASP.NET 工作階段狀態提供者的指引。 如需其他工作階段狀態選項的相關資訊，請參閱 [ASP.NET 工作階段狀態選項](#aspnet-session-state-options)。

## <a name="store-aspnet-session-state-in-hello-cache"></a>Hello 快取中儲存 ASP.NET 工作階段狀態
tooconfigure 用戶端應用程式，在 Visual Studio 中使用 hello Redis 快取工作階段狀態 NuGet 封裝，按一下**NuGet 套件管理員**， **Package Manager Console**從 hello**工具**功能表。

執行 hello 下列命令從 hello`Package Manager Console`視窗。
    
```
Install-Package Microsoft.Web.RedisSessionStateProvider
```

> [!IMPORTANT]
> 如果您使用 hello hello premium 層從叢集功能，您必須使用[RedisSessionStateProvider](https://www.nuget.org/packages/Microsoft.Web.RedisSessionStateProvider) 2.0.1 或更高版本，或例外狀況就會擲回。 移動 too2.0.1 或更高版本是中斷變更。如需詳細資訊，請參閱[v2.0.0 重大變更詳細資料](https://github.com/Azure/aspnet-redis-providers/wiki/v2.0.0-Breaking-Change-Details)。 Hello 這個更新的發行項時，此封裝的 hello 目前版本是 2.2.3。
> 
> 

hello Redis 工作階段狀態提供者 NuGet 封裝 hello StackExchange.Redis.StrongName 封裝上具有相依性。 如果 hello StackExchange.Redis.StrongName 封裝不存在專案中，它會安裝。

>[!NOTE]
>在加法 toohello 強式名稱 StackExchange.Redis.StrongName 封裝，還有 hello StackExchange.Redis 非強式命名版本。 如果您的專案使用 hello 非強式命名 StackExchange.Redis 版本必須先解除安裝，否則您發生命名衝突專案中。 如需這些封裝的相關詳細資訊，請參閱 [設定 .NET 快取用戶端](cache-dotnet-how-to-use-azure-redis-cache.md#configure-the-cache-clients)。
>
>

hello NuGet 封裝下載並新增 hello 需要組件參考，並新增下列區段到您的 web.config 檔案的 hello。 本節包含您 ASP.NET 應用程式 toouse hello Redis 的快取工作階段狀態提供者的 hello 必要的設定。

```xml
<sessionState mode="Custom" customProvider="MySessionStateStore">
    <providers>
    <!--
    <add name="MySessionStateStore"
           host = "127.0.0.1" [String]
        port = "" [number]
        accessKey = "" [String]
        ssl = "false" [true|false]
        throwOnError = "true" [true|false]
        retryTimeoutInMilliseconds = "0" [number]
        databaseId = "0" [number]
        applicationName = "" [String]
        connectionTimeoutInMilliseconds = "5000" [number]
        operationTimeoutInMilliseconds = "5000" [number]
    />
    -->
    <add name="MySessionStateStore" type="Microsoft.Web.Redis.RedisSessionStateProvider" host="127.0.0.1" accessKey="" ssl="false"/>
    </providers>
</sessionState>
```

hello 標記為註解 > 一節提供 hello 屬性和每個屬性的範例設定的範例。

設定您在 hello Microsoft Azure 入口網站的快取刀鋒伺服器中的 hello 值 hello 屬性並設定 hello 所需的其他值。 如需存取快取屬性的指示，請參閱 [設定 Redis 快取設定](cache-configure.md#configure-redis-cache-settings)。

* **主機** – 指定您的快取端點。
* **連接埠**– 使用非 SSL 連接埠或您的 SSL 連接埠，取決於 hello ssl 設定。
* **accessKey** – 用於您的快取中的任一 hello 主要或次要金鑰。
* **ssl** – 如果您想要以 ssl toosecure 快取/用戶端通訊，則為 true，否則為 false。 為確定 toospecify hello 正確的連接埠。
  * 新的快取預設為停用 hello 非 SSL 連接埠。 指定 true，此設定 toouse hello SSL 連接埠。 如需有關如何啟用 hello 非 SSL 連接埠的詳細資訊，請參閱 hello[存取連接埠](cache-configure.md#access-ports)> 一節中 hello[設定快取](cache-configure.md)主題。
* **throwOnError** – 如果您想是否有失敗或 false 如果您要以無訊息模式的 hello 作業 toofail 擲回例外狀況 toobe 則為 true。 您可以藉由檢查靜態 Microsoft.Web.Redis.RedisSessionStateProvider.LastException 屬性 hello 檢查失敗。 hello 預設值為 true。
* **retryTimeoutInMilliseconds** – 會在此間隔期間 (以毫秒指定) 重試失敗的作業。 hello 第一個重試發生之後 20 毫秒，並產生 hello retryTimeoutInMilliseconds 間隔到期之前的每秒然後重試作業。 緊接著此間隔，hello 作業會重試最後一個的一次。 如果 hello 作業仍失敗，hello 例外狀況擲回 toohello 呼叫者，根據 hello throwOnError 設定。 hello 預設值為 0，表示無重試。
* **databaseId** – 指定快取哪些資料庫 toouse 輸出資料。 如果未指定，會使用 hello 預設值為 0。
* **applicationName** – 金鑰在 redis 中會儲存為 `{<Application Name>_<Session ID>}_Data`。 這個命名配置可讓多個應用程式 tooshare hello 相同的 Redis 執行個體。 此參數是選擇性的，如果您未提供，將會使用預設值。
* **connectionTimeoutInMilliseconds** – 此設定可讓您 toooverride hello connectTimeout hello StackExchange.Redis 用戶端中設定。 如果未指定，會使用 hello 預設 connectTimeout 值為 5000。 如需詳細資訊，請參閱 [StackExchange.Redis 設定模型](http://go.microsoft.com/fwlink/?LinkId=398705)(英文)。
* **operationTimeoutInMilliseconds** – 此設定可讓您 toooverride hello syncTimeout hello StackExchange.Redis 用戶端中設定。 如果未指定，會使用 hello syncTimeout 預設為 1000年。 如需詳細資訊，請參閱 [StackExchange.Redis 設定模型](http://go.microsoft.com/fwlink/?LinkId=398705)(英文)。

如需有關這些屬性的詳細資訊，請參閱 hello 原始部落格文章公告在[宣佈適用於 ASP.NET 工作階段狀態提供者 Redis](http://blogs.msdn.com/b/webdev/archive/2014/05/12/announcing-asp-net-session-state-provider-for-redis-preview-release.aspx)。

別忘了 toocomment 出 hello 標準 InProc 工作階段狀態提供者區段在 web.config 中。

```xml
<!-- <sessionState mode="InProc"
     customProvider="DefaultSessionProvider">
     <providers>
        <add name="DefaultSessionProvider"
              type="System.Web.Providers.DefaultSessionStateProvider,
                    System.Web.Providers, Version=1.0.0.0, Culture=neutral,
                    PublicKeyToken=31bf3856ad364e35"
              connectionStringName="DefaultConnection" />
      </providers>
</sessionState> -->
```

一旦執行了這些步驟，您的應用程式是設定的 toouse hello Redis 的快取工作階段狀態提供者。 當您在應用程式中使用工作階段狀態時，會儲存在 Azure Redis 快取執行個體中。

> [!IMPORTANT]
> Hello 快取中儲存的資料必須是可序列化的與 hello 資料可以儲存在 hello 不同預設記憶體中 ASP.NET 工作階段狀態提供者。 使用 hello Redis 工作階段狀態提供者時，請務必儲存工作階段狀態中的 hello 資料型別都是可序列化。
> 
> 

## <a name="aspnet-session-state-options"></a>ASP.NET 工作階段狀態選項
* 在記憶體的工作階段狀態提供者-此提供者會儲存在記憶體中的 hello 工作階段狀態。 使用此提供者的 hello 優點是它既簡單又快速。 不過，您在使用記憶體中提供者時將無法調整 Web Apps，因為它不是分散式的。
* Sql Server 工作階段狀態提供者-此提供者會將 hello 工作階段狀態儲存在 Sql Server。 如果您想 toostore hello 工作階段狀態持續性儲存體中，請使用此提供者。 您可以調整您的 Web 應用程式，但將 SQL Server 用於工作階段，會對 Web 應用程式的效能造成影響。
* 分散式中記憶體的工作階段狀態提供者例如 Redis 快取工作階段狀態提供者-這個 hello 兩者之優點的提供者提供。 您的 Web 應用程式可擁有簡單、快速而可調整的工作階段狀態供應器。 因為此工作階段狀態快取中，您的應用程式的提供者存放區 hello tootake 考量所有 hello 與對話 tooa 分散式記憶體內部快取，例如暫時性網路失敗時，相關聯的特性。 如需使用快取的最佳作法，請參閱 Microsoft 模式和作法 [Azure 雲端應用程式設計和實作指引](https://github.com/mspnp/azure-guidance)中的[快取指引](../best-practices-caching.md)。

如需工作階段狀態和其他最佳作法的相關詳細資訊，請參閱 [Web 開發最佳作法 (使用 Azure 建置實際的雲端應用程式)](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/web-development-best-practices)(英文)。

## <a name="next-steps"></a>後續步驟
簽出 hello [Azure Redis 快取的 ASP.NET 輸出快取提供者](cache-aspnet-output-cache-provider.md)。

