---
title: "使用.NET aaaConnecting tooMedia 服務帳戶"
description: "本主題示範如何 tooconnect tooMedia 服務 uisng.NET。"
services: media-services
documentationcenter: 
author: juliako
manager: erikre
editor: 
ms.assetid: a8412a29-59dc-44a0-ace0-be79a97dab63
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 09/26/2016
ms.author: juliako
ms.openlocfilehash: a23bd285f7cae17ae5831e1e50e73947afbb9a3d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="connecting-toomedia-services-account-using-media-services-sdk-for-net"></a>連接 tooMedia 使用 Media Services SDK for.NET 的服務帳戶
> [!div class="op_single_selector"]
> * [REST](media-services-rest-connect-programmatically.md)
> * [.NET](media-services-dotnet-connect-programmatically.md)
> 
> 

本主題說明 Azure Media Services 以進行程式設計時的程式設計連線 tooMicrosoft tooobtain 如何 hello Media Services SDK for.NET。

## <a name="connecting-toomedia-services"></a>TooMedia 服務連線
tooconnect tooMedia 服務以程式設計的方式，您必須擁有先前設定的 Azure 帳戶，該帳戶，在設定媒體服務，然後設定使用 hello Media Services SDK for.NET 進行開發的 Visual Studio 專案。 如需詳細資訊，請參閱 < 開發的設定以 hello Media Services SDK for.NET。

您可以在 hello hello Media Services 帳戶設定程序結尾，取得 hello 下列必要的連線值。 使用這些 toomake 以程式設計方式連接 tooMedia 服務。

* 媒體服務帳戶名稱。
* 媒體服務帳戶金鑰。

toofind 這些值，請 toohello Azure 管理入口，選取您的媒體服務帳戶，然後按一下 hello"**管理金鑰**"hello hello 入口網站視窗底部的圖示。 按一下 hello 圖示下一步 tooeach 文字方塊複製 hello 值 toohello 系統剪貼簿。

## <a name="creating-a-cloudmediacontext-instance"></a>建立 CloudMediaContext 執行個體
針對媒體進行程式設計服務需要 toocreate toostart **CloudMediaContext**代表 hello 伺服器內容的執行個體。 hello **CloudMediaContext**包含參考 tooimportant 集合，包括工作、 資產、 檔案、 存取原則和定位器。

> [!NOTE]
> hello **CloudMediaContext**類別不是安全執行緒。 您應該為每個執行緒或每組作業建立新的 CloudMediaContext。
> 
> 

CloudMediaContext 有五個建構函式多載。 它是使用建議的 toouse 建構函式**MediaServicesCredentials**做為參數。 如需詳細資訊，請參閱 hello**重複使用存取控制服務權杖**一節。 

hello 下列範例會使用 hello 公用 CloudMediaContext(MediaServicesCredentials credentials) 建構函式：

    // _cachedCredentials and _context are class member variables. 
    _cachedCredentials = new MediaServicesCredentials(
                    _mediaServicesAccountName,
                    _mediaServicesAccountKey);

    _context = new CloudMediaContext(_cachedCredentials);


## <a name="reusing-access-control-service-tokens"></a>重複使用存取控制服務權杖
本節說明如何 tooreuse 存取控制服務權杖使用採用 MediaServicesCredentials 做為參數的 CloudMediaContext 建構函式。

[Azure Active Directory 存取控制](https://msdn.microsoft.com/library/hh147631.aspx)（也稱為存取控制服務或 ACS） 是提供讓您輕鬆地驗證並授權使用者 toogain 存取 tootheir web 應用程式的雲端服務。 Microsoft Azure Media Services 控制存取透過需要 ACS 權杖的 OAuth 通訊協定 tooits 服務。 媒體服務會接收來自授權伺服器 hello ACS 權杖。

當使用 hello Media Services SDK 進行開發，您就可以選擇 toonot 處理 hello 語彙基元，因為 hello SDK 程式碼管理員加以。 不過，讓 hello SDK 完全管理 hello ACS 權杖潛在客戶 toounnecessary 權杖要求。 要求語彙基元耗時，而且會耗用 hello 用戶端和伺服器資源。 此外，hello ACS server 會調整 hello 要求如果 hello 速率太高。 hello 限制是每秒 30 個要求，請參閱[ACS 服務限制](https://msdn.microsoft.com/library/gg185909.aspx)如需詳細資訊。

從 hello Media Services SDK 版本 3.0.0.0 開始，您可以重複使用 hello ACS 權杖。 hello **CloudMediaContext**使用建構函式**MediaServicesCredentials**做為參數啟用多個內容間共用的 hello ACS 權杖。 hello MediaServicesCredentials 類別封裝 hello 媒體服務認證。 如果可用的 ACS 權杖，而且知道其到期時間，您可以建立新的 MediaServicesCredentials 執行個體與 hello 語彙基元，並將它傳遞 CloudMediaContext toohello 建構函式。 每當在到期時，請注意，hello Media Services SDK 自動重新整理語彙基元。 有兩種方式 tooreuse ACS 權杖，如以下的 hello 範例所示。

* 您可以快取 hello **MediaServicesCredentials** （例如，在靜態類別變數） 的記憶體中的物件。 接著，將快取的 hello 物件 toohello CloudMediaContext 建構函式。 hello MediaServicesCredentials 物件包含可重複使用，如果仍然有效的 ACS 權杖。 如果 hello 語彙基元不是有效的它將會重新整理 hello 由 Media Services SDK 使用 hello 認證會提供 toohello MediaServicesCredentials 建構函式。
  
    請注意該 hello **MediaServicesCredentials**物件 RefreshToken 稱為的 hello 之後取得有效的語彙基元。 hello **CloudMediaContext**呼叫 hello **RefreshToken** hello 建構函式中的方法。 如果您計劃 toosave hello 語彙基元值 tooan 外部儲存體時，請確定 toocheck 是否儲存 hello 權杖資料前先 hello TokenExpiration 值是否有效。 如果無效，則請在快取前呼叫 RefreshToken。
  
        // Create and cache hello Media Services credentials in a static class variable.
        _cachedCredentials = new MediaServicesCredentials(_mediaServicesAccountName, _mediaServicesAccountKey);

        // Use hello cached credentials toocreate a new CloudMediaContext object.
        if(_cachedCredentials == null)
        {
            _cachedCredentials = new MediaServicesCredentials(_mediaServicesAccountName, _mediaServicesAccountKey);
        }

        CloudMediaContext context = new CloudMediaContext(_cachedCredentials);

* 您也可以快取 hello AccessToken 字串和 hello TokenExpiration 值。 hello 值稍後可以使用的 toocreate 新 MediaServicesCredentials 物件並快取的 hello 語彙基元資料。  這是其中 hello 語彙基元可以在多個處理程序或電腦間安全共用的案例特別有用。
  
    hello 下列程式碼片段會呼叫 hello SaveTokenDataToExternalStorage、 GetTokenDataFromExternalStorage 以及 updatetokendatainexternalstorageifneeded 等此範例中未定義的方法。 您可以在外部儲存體中定義這些方法 toostore、 擷取、 和更新權杖資料。 
  
        CloudMediaContext context1 = new CloudMediaContext(_mediaServicesAccountName, _mediaServicesAccountKey);
  
        // Get token values from hello context.
        var accessToken = context1.Credentials.AccessToken;
        var tokenExpiration = context1.Credentials.TokenExpiration;
  
        // Save token values for later use. 
        // hello SaveTokenDataToExternalStorage method should check 
        // whether hello TokenExpiration value is valid before saving hello token data. 
        // If it is not valid, call MediaServicesCredentials’s RefreshToken before caching.
        SaveTokenDataToExternalStorage(accessToken, tokenExpiration);
  
    使用儲存的語彙基元值 toocreate MediaServicesCredentials hello。

        var accessToken = "";
        var tokenExpiration = DateTime.UtcNow;

        // Retrieve saved token values.
        GetTokenDataFromExternalStorage(out accessToken, out tokenExpiration);

        // Create a new MediaServicesCredentials object using saved token values.
        MediaServicesCredentials credentials = new MediaServicesCredentials(_mediaServicesAccountName, _mediaServicesAccountKey)
        {
            AccessToken = accessToken,
            TokenExpiration = tokenExpiration
        };

        CloudMediaContext context2 = new CloudMediaContext(credentials);

    更新 hello 權杖副本，以防 hello 語彙基元已由 hello Media Services SDK 更新。 

        if(tokenExpiration != context2.Credentials.TokenExpiration)
        {
            UpdateTokenDataInExternalStorageIfNeeded(accessToken, context2.Credentials.TokenExpiration);
        }


* 如果您有多個 Media Services 帳戶 （例如，針對載入目的或地理分散） 您可以快取使用 hello System.Collections.Concurrent.ConcurrentDictionary 集合 (hello MediaServicesCredentials 物件ConcurrentDictionary 集合代表安全執行緒集合可由多個執行緒並行存取的索引鍵/值組）。 然後，您可以使用 hello GetOrAdd 方法 tooget hello 快取認證。 
  
        // Declare a static class variable of hello ConcurrentDictionary type in which hello Media Services credentials will be cached.  
        private static readonly ConcurrentDictionary<string, MediaServicesCredentials> mediaServicesCredentialsCache = 
            new ConcurrentDictionary<string, MediaServicesCredentials>();

        // Cache (or get already cached) Media Services credentials. Use these credentials toocreate a new CloudMediaContext object.
        static public CloudMediaContext CreateMediaServicesContext(string accountName, string accountKey)
        {
            CloudMediaContext cloudMediaContext;
            MediaServicesCredentials mediaServicesCredentials;

            mediaServicesCredentials = mediaServicesCredentialsCache.GetOrAdd(
                accountName,
                valueFactory => new MediaServicesCredentials(accountName, accountKey));

            cloudMediaContext = new CloudMediaContext(mediaServicesCredentials);

            return cloudMediaContext;
        }

## <a name="connecting-tooa-media-services-account-located-in-hello-north-china-region"></a>連接位於 hello 中國北部地區 tooa Media Services 帳戶
如果您的帳戶位於 hello 中國北部地區，請使用下列建構函式的 hello:

    public CloudMediaContext(Uri apiServer, string accountName, string accountKey, string scope, string acsBaseAddress)

例如：

    _context = new CloudMediaContext(
        new Uri("https://wamsbjbclus001rest-hs.chinacloudapp.cn/API/"),
        _mediaServicesAccountName,
        _mediaServicesAccountKey,
        "urn:WindowsAzureMediaServices",
        "https://wamsprodglobal001acs.accesscontrol.chinacloudapi.cn");


## <a name="storing-connection-values-in-configuration"></a>在組態中儲存連線值
強烈建議的作法 toostore 連接值，尤其是敏感值，例如您的帳戶名稱和密碼，在設定它。 此外，也是建議的作法 tooencrypt 敏感的組態資料。 您可以使用 hello Windows 加密檔案系統 (EFS) 加密 hello 整個組態檔案。 tooenable EFS 檔案，以滑鼠右鍵按一下 hello 檔案中，選取**屬性**，並啟用加密在 hello**進階**設定 索引標籤。或者，可以使用受保護的組態，建立將選擇之組態檔案內的部分加密的自訂解決方案。 請參閱 [使用受保護組態將組態資訊加密](https://msdn.microsoft.com/library/53tyfkaw.aspx)。

下列 App.config 檔的 hello 包含所需的 hello 連接值。 hello 中 hello 值<appSettings>項目是您 hello Media Services 帳戶設定程序中取得的所需的 hello 值。

    <configuration>
      <appSettings>
        <add key="MediaServicesAccountName" value="Media-Services-Account-Name" />
        <add key="MediaServicesAccountKey" value="Media-Services-Account-Key" />
      </appSettings>
    </configuration>


從組態 tooretrieve 連接值，您可以使用 hello **ConfigurationManager**類別，並將指定在程式碼中的 hello 值 toofields:

    private static readonly string _accountName = ConfigurationManager.AppSettings["MediaServicesAccountName"];
    private static readonly string _accountKey = ConfigurationManager.AppSettings["MediaServicesAccountKey"];



## <a name="media-services-learning-paths"></a>媒體服務學習路徑
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>提供意見反應
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

