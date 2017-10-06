---
title: "aaaSession 狀態時，使用 Azure App Service 中的 Azure Redis 快取"
description: "了解如何 toouse hello Azure 快取服務 toosupport ASP.NET 工作階段狀態快取。"
services: app-service\web
documentationcenter: .net
author: Rick-Anderson
manager: erikre
editor: none
ms.assetid: 4f98d289-2698-464d-85cd-99ec40fad1f2
ms.service: app-service-web
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: get-started-article
ms.date: 06/27/2016
ms.author: riande
ms.openlocfilehash: f689b6754ea072aa195f822ab6482f4bf2748375
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="session-state-with-azure-redis-cache-in-azure-app-service"></a>在 Azure App Service 中使用 Azure Redis 快取的工作階段狀態
本主題說明如何 toouse hello Azure Redis 快取服務工作階段狀態。

如果您的 ASP.NET web 應用程式使用工作階段狀態，您將需要 tooconfigure 外部工作階段狀態提供者 （hello Redis 快取服務或 SQL Server 工作階段狀態提供者）。 如果您使用工作階段狀態，而未使用外部提供者，您將會限制的 tooone web 應用程式的執行個體。 hello Redis 快取服務是 hello 最快速且簡單 tooenable。

[!INCLUDE [app-service-web-to-api-and-mobile](../../includes/app-service-web-to-api-and-mobile.md)]

## <a id="createcache"></a>建立 hello 快取
請遵循[這些指示](../redis-cache/cache-dotnet-how-to-use-azure-redis-cache.md#create-cache)toocreate hello 快取。

## <a id="configureproject"></a>新增 hello RedisSessionStateProvider NuGet 封裝 tooyour web 應用程式
安裝 hello NuGet`RedisSessionStateProvider`封裝。  使用 hello 下列命令從 hello 封裝管理員主控台 tooinstall (**工具** > **NuGet 套件管理員** > **Package Manager Console**):

  `PM> Install-Package Microsoft.Web.RedisSessionStateProvider`

從 tooinstall**工具** > **NuGet 套件管理員** > **管理 NugGet Packages for Solution**，搜尋`RedisSessionStateProvider`。

如需詳細資訊，請參閱 hello [NuGet RedisSessionStateProvider 頁面](http://www.nuget.org/packages/Microsoft.Web.RedisSessionStateProvider/)和[設定 hello 快取用戶端](../redis-cache/cache-dotnet-how-to-use-azure-redis-cache.md#NuGet)。

## <a id="configurewebconfig"></a>修改 hello Web.Config 檔案
此外 toomaking 組件所參考的快取、 hello NuGet 封裝會新增虛設常式項目在 hello *web.config*檔案。 

1. 開啟 hello *web.config*並尋找 hello hello **sessionState**項目。
2. 輸入的值 hello `host`， `accessKey`， `port` （hello SSL 連接埠應為 6380），並設定`SSL`太`true`。 這些值可以取自 hello [Azure 入口網站](http://go.microsoft.com/fwlink/?LinkId=529715)刀鋒視窗中的快取執行個體。 如需詳細資訊，請參閱[連接 toohello 快取](../redis-cache/cache-dotnet-how-to-use-azure-redis-cache.md#connect-to-cache)。 請注意新的快取預設為停用 hello 非 SSL 連接埠。 如需有關如何啟用 hello 非 SSL 連接埠的詳細資訊，請參閱 hello[存取連接埠](https://msdn.microsoft.com/library/azure/dn793612.aspx#AccessPorts)> 一節中 hello [Azure Redis 快取中設定快取](https://msdn.microsoft.com/library/azure/dn793612.aspx)主題。 hello 下列標記會顯示 hello 變更 toohello *web.config*檔案，特別是 hello 變更太*連接埠*，*主機*，accessKey * 和*ssl*.
   
          <system.web>;
            <customErrors mode="Off" />;
            <authentication mode="None" />;
            <compilation debug="true" targetFramework="4.5" />;
            <httpRuntime targetFramework="4.5" />;
            <sessionState mode="Custom" customProvider="RedisSessionProvider">;
              <providers>;  
                  <!--<add name="RedisSessionProvider" 
                    host = "127.0.0.1" [String]
                    port = "" [number]
                    accessKey = "" [String]
                    ssl = "false" [true|false]
                    throwOnError = "true" [true|false]
                    retryTimeoutInMilliseconds = "0" [number]
                    databaseId = "0" [number]
                    applicationName = "" [String]
                  />;-->;
                 <add name="RedisSessionProvider" 
                      type="Microsoft.Web.Redis.RedisSessionStateProvider" 
                      port="6380"
                      host="movie2.redis.cache.windows.net" 
                      accessKey="m7PNV60CrvKpLqMUxosC3dSe6kx9nQ6jP5del8TmADk=" 
                      ssl="true" />;
              <!--<add name="MySessionStateStore" type="Microsoft.Web.Redis.RedisSessionStateProvider" host="127.0.0.1" accessKey="" ssl="false" />;-->;
              </providers>;
            </sessionState>;
          </system.web>;

## <a id="usesessionobject"></a>使用程式碼中的 hello 工作階段物件
hello 最後一個步驟是 toobegin 使用 ASP.NET 程式碼中的 hello 工作階段物件。 使用 hello 加入物件 toosession 狀態**Session.Add**方法。 這個方法會使用 hello 工作階段狀態快取中的索引鍵-值組 toostore 項目。

    string strValue = "yourvalue";
    Session.Add("yourkey", strValue);

下列程式碼的 hello 擷取此值從工作階段狀態。

    object objValue = Session["yourkey"];
    if (objValue != null)
       strValue = (string)objValue;    

您也可以使用 web 應用程式中的 hello Redis 快取 toocache 物件。 如需詳細資訊，請參閱 [15 分鐘學會包含 Azure Redis 快取的 MVC 影片應用程式](https://azure.microsoft.com/blog/2014/06/05/mvc-movie-app-with-azure-redis-cache-in-15-minutes/)。
如需有關如何 toouse ASP.NET 工作階段狀態，請參閱[ASP.NET 工作階段狀態概觀][ASP.NET Session State Overview]。

> [!NOTE]
> 如果您想 tooget 之前註冊 Azure 帳戶與 Azure 應用程式服務啟動時，請移至太[再試一次應用程式服務](https://azure.microsoft.com/try/app-service/)，可以立即存留較短的入門的 web 應用程式中建立應用程式服務。 不需要信用卡；沒有承諾。
> 
> 

## <a name="whats-changed"></a>變更的項目
* 從網站 tooApp 服務變更如指南 toohello: [Azure 應用程式服務和其對影響現有的 Azure 服務](http://go.microsoft.com/fwlink/?LinkId=529714)
  
  *作者：[Rick Anderson](https://twitter.com/RickAndMSFT)*

[installed hello latest]: http://www.windowsazure.com/downloads/?sdk=net  
[ASP.NET Session State Overview]: http://msdn.microsoft.com/library/ms178581.aspx

[NewIcon]: ./media/web-sites-dotnet-session-state-caching/CacheScreenshot_NewButton.png
[NewCacheDialog]: ./media/web-sites-dotnet-session-state-caching/CachingScreenshot_CreateOptions.png
[CacheIcon]: ./media/web-sites-dotnet-session-state-caching/CachingScreenshot_CacheIcon.png
[NuGetDialog]: ./media/web-sites-dotnet-session-state-caching/CachingScreenshot_NuGet.png
[OutputConfig]: ./media/web-sites-dotnet-session-state-caching/CachingScreenshot_OC_WebConfig.png
[CacheConfig]: ./media/web-sites-dotnet-session-state-caching/CachingScreenshot_CacheConfig.png
[EndpointURL]: ./media/web-sites-dotnet-session-state-caching/CachingScreenshot_EndpointURL.png
[ManageKeys]: ./media/web-sites-dotnet-session-state-caching/CachingScreenshot_ManageAccessKeys.png

