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
# <a name="connecting-toomedia-services-account-using-media-services-sdk-for-net"></a><span data-ttu-id="5499c-103">連接 tooMedia 使用 Media Services SDK for.NET 的服務帳戶</span><span class="sxs-lookup"><span data-stu-id="5499c-103">Connecting tooMedia Services Account using Media Services SDK for .NET</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="5499c-104">REST</span><span class="sxs-lookup"><span data-stu-id="5499c-104">REST</span></span>](media-services-rest-connect-programmatically.md)
> * [<span data-ttu-id="5499c-105">.NET</span><span class="sxs-lookup"><span data-stu-id="5499c-105">.NET</span></span>](media-services-dotnet-connect-programmatically.md)
> 
> 

<span data-ttu-id="5499c-106">本主題說明 Azure Media Services 以進行程式設計時的程式設計連線 tooMicrosoft tooobtain 如何 hello Media Services SDK for.NET。</span><span class="sxs-lookup"><span data-stu-id="5499c-106">This topic describes how tooobtain a programmatic connection tooMicrosoft Azure Media Services when you are programming with hello Media Services SDK for .NET.</span></span>

## <a name="connecting-toomedia-services"></a><span data-ttu-id="5499c-107">TooMedia 服務連線</span><span class="sxs-lookup"><span data-stu-id="5499c-107">Connecting tooMedia Services</span></span>
<span data-ttu-id="5499c-108">tooconnect tooMedia 服務以程式設計的方式，您必須擁有先前設定的 Azure 帳戶，該帳戶，在設定媒體服務，然後設定使用 hello Media Services SDK for.NET 進行開發的 Visual Studio 專案。</span><span class="sxs-lookup"><span data-stu-id="5499c-108">tooconnect tooMedia Services programmatically, you must have previously set up an Azure account, configured Media Services on that account, and then set up a Visual Studio project for development with hello Media Services SDK for .NET.</span></span> <span data-ttu-id="5499c-109">如需詳細資訊，請參閱 < 開發的設定以 hello Media Services SDK for.NET。</span><span class="sxs-lookup"><span data-stu-id="5499c-109">For more information, see Setup for Development with hello Media Services SDK for .NET.</span></span>

<span data-ttu-id="5499c-110">您可以在 hello hello Media Services 帳戶設定程序結尾，取得 hello 下列必要的連線值。</span><span class="sxs-lookup"><span data-stu-id="5499c-110">At hello end of hello Media Services account setup process, you obtained hello following required connection values.</span></span> <span data-ttu-id="5499c-111">使用這些 toomake 以程式設計方式連接 tooMedia 服務。</span><span class="sxs-lookup"><span data-stu-id="5499c-111">Use these toomake programmatic connections tooMedia Services.</span></span>

* <span data-ttu-id="5499c-112">媒體服務帳戶名稱。</span><span class="sxs-lookup"><span data-stu-id="5499c-112">Your Media Services account name.</span></span>
* <span data-ttu-id="5499c-113">媒體服務帳戶金鑰。</span><span class="sxs-lookup"><span data-stu-id="5499c-113">Your Media Services account key.</span></span>

<span data-ttu-id="5499c-114">toofind 這些值，請 toohello Azure 管理入口，選取您的媒體服務帳戶，然後按一下 hello"**管理金鑰**"hello hello 入口網站視窗底部的圖示。</span><span class="sxs-lookup"><span data-stu-id="5499c-114">toofind these values, go toohello Azure Managment Portal, select your Media Service account, and click on hello “**MANAGE KEYS**” icon on hello bottom of hello portal window.</span></span> <span data-ttu-id="5499c-115">按一下 hello 圖示下一步 tooeach 文字方塊複製 hello 值 toohello 系統剪貼簿。</span><span class="sxs-lookup"><span data-stu-id="5499c-115">Clicking on hello icon next tooeach text box copies hello value toohello system clipboard.</span></span>

## <a name="creating-a-cloudmediacontext-instance"></a><span data-ttu-id="5499c-116">建立 CloudMediaContext 執行個體</span><span class="sxs-lookup"><span data-stu-id="5499c-116">Creating a CloudMediaContext Instance</span></span>
<span data-ttu-id="5499c-117">針對媒體進行程式設計服務需要 toocreate toostart **CloudMediaContext**代表 hello 伺服器內容的執行個體。</span><span class="sxs-lookup"><span data-stu-id="5499c-117">toostart programming against Media Services you need toocreate a **CloudMediaContext** instance that represents hello server context.</span></span> <span data-ttu-id="5499c-118">hello **CloudMediaContext**包含參考 tooimportant 集合，包括工作、 資產、 檔案、 存取原則和定位器。</span><span class="sxs-lookup"><span data-stu-id="5499c-118">hello **CloudMediaContext** includes references tooimportant collections including jobs, assets, files, access policies, and locators.</span></span>

> [!NOTE]
> <span data-ttu-id="5499c-119">hello **CloudMediaContext**類別不是安全執行緒。</span><span class="sxs-lookup"><span data-stu-id="5499c-119">hello **CloudMediaContext** class is not thread safe.</span></span> <span data-ttu-id="5499c-120">您應該為每個執行緒或每組作業建立新的 CloudMediaContext。</span><span class="sxs-lookup"><span data-stu-id="5499c-120">You should create a new CloudMediaContext per thread or per set of operations.</span></span>
> 
> 

<span data-ttu-id="5499c-121">CloudMediaContext 有五個建構函式多載。</span><span class="sxs-lookup"><span data-stu-id="5499c-121">CloudMediaContext has five constructor overloads.</span></span> <span data-ttu-id="5499c-122">它是使用建議的 toouse 建構函式**MediaServicesCredentials**做為參數。</span><span class="sxs-lookup"><span data-stu-id="5499c-122">It is recommended toouse constructors that take **MediaServicesCredentials** as a parameter.</span></span> <span data-ttu-id="5499c-123">如需詳細資訊，請參閱 hello**重複使用存取控制服務權杖**一節。</span><span class="sxs-lookup"><span data-stu-id="5499c-123">For more information, see hello **Reusing Access Control Service Tokens** that follows.</span></span> 

<span data-ttu-id="5499c-124">hello 下列範例會使用 hello 公用 CloudMediaContext(MediaServicesCredentials credentials) 建構函式：</span><span class="sxs-lookup"><span data-stu-id="5499c-124">hello following example uses hello public CloudMediaContext(MediaServicesCredentials credentials) constructor:</span></span>

    // _cachedCredentials and _context are class member variables. 
    _cachedCredentials = new MediaServicesCredentials(
                    _mediaServicesAccountName,
                    _mediaServicesAccountKey);

    _context = new CloudMediaContext(_cachedCredentials);


## <a name="reusing-access-control-service-tokens"></a><span data-ttu-id="5499c-125">重複使用存取控制服務權杖</span><span class="sxs-lookup"><span data-stu-id="5499c-125">Reusing Access Control Service Tokens</span></span>
<span data-ttu-id="5499c-126">本節說明如何 tooreuse 存取控制服務權杖使用採用 MediaServicesCredentials 做為參數的 CloudMediaContext 建構函式。</span><span class="sxs-lookup"><span data-stu-id="5499c-126">This section shows how tooreuse Access Control Service tokens by using CloudMediaContext constructors that take MediaServicesCredentials as a parameter.</span></span>

<span data-ttu-id="5499c-127">[Azure Active Directory 存取控制](https://msdn.microsoft.com/library/hh147631.aspx)（也稱為存取控制服務或 ACS） 是提供讓您輕鬆地驗證並授權使用者 toogain 存取 tootheir web 應用程式的雲端服務。</span><span class="sxs-lookup"><span data-stu-id="5499c-127">[Azure Active Directory Access Control](https://msdn.microsoft.com/library/hh147631.aspx) (also known as Access Control Service or ACS) is a cloud-based service that provides an easy way of authenticating and authorizing users toogain access tootheir web applications.</span></span> <span data-ttu-id="5499c-128">Microsoft Azure Media Services 控制存取透過需要 ACS 權杖的 OAuth 通訊協定 tooits 服務。</span><span class="sxs-lookup"><span data-stu-id="5499c-128">Microsoft Azure Media Services controls access tooits services though OAuth protocol that requires an ACS token.</span></span> <span data-ttu-id="5499c-129">媒體服務會接收來自授權伺服器 hello ACS 權杖。</span><span class="sxs-lookup"><span data-stu-id="5499c-129">Media Services receives hello ACS tokens from an authorization server.</span></span>

<span data-ttu-id="5499c-130">當使用 hello Media Services SDK 進行開發，您就可以選擇 toonot 處理 hello 語彙基元，因為 hello SDK 程式碼管理員加以。</span><span class="sxs-lookup"><span data-stu-id="5499c-130">When developing with hello Media Services SDK, you can choose toonot deal with hello tokens because hello SDK code managers them for you.</span></span> <span data-ttu-id="5499c-131">不過，讓 hello SDK 完全管理 hello ACS 權杖潛在客戶 toounnecessary 權杖要求。</span><span class="sxs-lookup"><span data-stu-id="5499c-131">However, letting hello SDK fully manage hello ACS tokens leads toounnecessary token requests.</span></span> <span data-ttu-id="5499c-132">要求語彙基元耗時，而且會耗用 hello 用戶端和伺服器資源。</span><span class="sxs-lookup"><span data-stu-id="5499c-132">Requesting tokens takes time and consumes hello client and server resources.</span></span> <span data-ttu-id="5499c-133">此外，hello ACS server 會調整 hello 要求如果 hello 速率太高。</span><span class="sxs-lookup"><span data-stu-id="5499c-133">Also, hello ACS server throttles hello requests if hello rate is too high.</span></span> <span data-ttu-id="5499c-134">hello 限制是每秒 30 個要求，請參閱[ACS 服務限制](https://msdn.microsoft.com/library/gg185909.aspx)如需詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="5499c-134">hello limit is 30 requests per second, see [ACS Service Limitations](https://msdn.microsoft.com/library/gg185909.aspx) for more details.</span></span>

<span data-ttu-id="5499c-135">從 hello Media Services SDK 版本 3.0.0.0 開始，您可以重複使用 hello ACS 權杖。</span><span class="sxs-lookup"><span data-stu-id="5499c-135">Starting with hello Media Services SDK version 3.0.0.0, you can reuse hello ACS tokens.</span></span> <span data-ttu-id="5499c-136">hello **CloudMediaContext**使用建構函式**MediaServicesCredentials**做為參數啟用多個內容間共用的 hello ACS 權杖。</span><span class="sxs-lookup"><span data-stu-id="5499c-136">hello **CloudMediaContext** constructors that take **MediaServicesCredentials** as a parameter enable sharing hello ACS tokens between multiple contexts.</span></span> <span data-ttu-id="5499c-137">hello MediaServicesCredentials 類別封裝 hello 媒體服務認證。</span><span class="sxs-lookup"><span data-stu-id="5499c-137">hello MediaServicesCredentials class encapsulates hello Media Services credentials.</span></span> <span data-ttu-id="5499c-138">如果可用的 ACS 權杖，而且知道其到期時間，您可以建立新的 MediaServicesCredentials 執行個體與 hello 語彙基元，並將它傳遞 CloudMediaContext toohello 建構函式。</span><span class="sxs-lookup"><span data-stu-id="5499c-138">If an ACS token is available and its expiration time is known, you can create a new MediaServicesCredentials instance with hello token and pass it toohello constructor of CloudMediaContext.</span></span> <span data-ttu-id="5499c-139">每當在到期時，請注意，hello Media Services SDK 自動重新整理語彙基元。</span><span class="sxs-lookup"><span data-stu-id="5499c-139">Note that hello Media Services SDK automatically refreshes tokens whenever they expire.</span></span> <span data-ttu-id="5499c-140">有兩種方式 tooreuse ACS 權杖，如以下的 hello 範例所示。</span><span class="sxs-lookup"><span data-stu-id="5499c-140">There are two ways tooreuse ACS tokens, as shown in hello examples below.</span></span>

* <span data-ttu-id="5499c-141">您可以快取 hello **MediaServicesCredentials** （例如，在靜態類別變數） 的記憶體中的物件。</span><span class="sxs-lookup"><span data-stu-id="5499c-141">You can cache hello **MediaServicesCredentials** object in memory (for example, in a static class variable).</span></span> <span data-ttu-id="5499c-142">接著，將快取的 hello 物件 toohello CloudMediaContext 建構函式。</span><span class="sxs-lookup"><span data-stu-id="5499c-142">Then, pass hello cached object toohello CloudMediaContext constructor.</span></span> <span data-ttu-id="5499c-143">hello MediaServicesCredentials 物件包含可重複使用，如果仍然有效的 ACS 權杖。</span><span class="sxs-lookup"><span data-stu-id="5499c-143">hello MediaServicesCredentials object contains an ACS token that can be reused if it is still valid.</span></span> <span data-ttu-id="5499c-144">如果 hello 語彙基元不是有效的它將會重新整理 hello 由 Media Services SDK 使用 hello 認證會提供 toohello MediaServicesCredentials 建構函式。</span><span class="sxs-lookup"><span data-stu-id="5499c-144">If hello token is not valid, it will be refreshed by hello Media Services SDK using hello credentials given toohello MediaServicesCredentials constructor.</span></span>
  
    <span data-ttu-id="5499c-145">請注意該 hello **MediaServicesCredentials**物件 RefreshToken 稱為的 hello 之後取得有效的語彙基元。</span><span class="sxs-lookup"><span data-stu-id="5499c-145">Note that hello **MediaServicesCredentials** object gets a valid token after hello RefreshToken is called.</span></span> <span data-ttu-id="5499c-146">hello **CloudMediaContext**呼叫 hello **RefreshToken** hello 建構函式中的方法。</span><span class="sxs-lookup"><span data-stu-id="5499c-146">hello **CloudMediaContext** calls hello **RefreshToken** method in hello constructor.</span></span> <span data-ttu-id="5499c-147">如果您計劃 toosave hello 語彙基元值 tooan 外部儲存體時，請確定 toocheck 是否儲存 hello 權杖資料前先 hello TokenExpiration 值是否有效。</span><span class="sxs-lookup"><span data-stu-id="5499c-147">If you are planning toosave hello token values tooan external storage, make sure toocheck whether hello TokenExpiration value is valid before saving hello token data.</span></span> <span data-ttu-id="5499c-148">如果無效，則請在快取前呼叫 RefreshToken。</span><span class="sxs-lookup"><span data-stu-id="5499c-148">If it is not valid, call RefreshToken before caching.</span></span>
  
        // Create and cache hello Media Services credentials in a static class variable.
        _cachedCredentials = new MediaServicesCredentials(_mediaServicesAccountName, _mediaServicesAccountKey);

        // Use hello cached credentials toocreate a new CloudMediaContext object.
        if(_cachedCredentials == null)
        {
            _cachedCredentials = new MediaServicesCredentials(_mediaServicesAccountName, _mediaServicesAccountKey);
        }

        CloudMediaContext context = new CloudMediaContext(_cachedCredentials);

* <span data-ttu-id="5499c-149">您也可以快取 hello AccessToken 字串和 hello TokenExpiration 值。</span><span class="sxs-lookup"><span data-stu-id="5499c-149">You can also cache hello AccessToken string and hello TokenExpiration values.</span></span> <span data-ttu-id="5499c-150">hello 值稍後可以使用的 toocreate 新 MediaServicesCredentials 物件並快取的 hello 語彙基元資料。</span><span class="sxs-lookup"><span data-stu-id="5499c-150">hello values could later be used toocreate a new MediaServicesCredentials object with hello cached token data.</span></span>  <span data-ttu-id="5499c-151">這是其中 hello 語彙基元可以在多個處理程序或電腦間安全共用的案例特別有用。</span><span class="sxs-lookup"><span data-stu-id="5499c-151">This is especially useful for scenarios where hello token can be securely shared among multiple processes or computers.</span></span>
  
    <span data-ttu-id="5499c-152">hello 下列程式碼片段會呼叫 hello SaveTokenDataToExternalStorage、 GetTokenDataFromExternalStorage 以及 updatetokendatainexternalstorageifneeded 等此範例中未定義的方法。</span><span class="sxs-lookup"><span data-stu-id="5499c-152">hello following code snippets call hello SaveTokenDataToExternalStorage, GetTokenDataFromExternalStorage, and UpdateTokenDataInExternalStorageIfNeeded methods that are not defined in this example.</span></span> <span data-ttu-id="5499c-153">您可以在外部儲存體中定義這些方法 toostore、 擷取、 和更新權杖資料。</span><span class="sxs-lookup"><span data-stu-id="5499c-153">You could define these methods toostore, retrieve, and update token data in an external storage.</span></span> 
  
        CloudMediaContext context1 = new CloudMediaContext(_mediaServicesAccountName, _mediaServicesAccountKey);
  
        // Get token values from hello context.
        var accessToken = context1.Credentials.AccessToken;
        var tokenExpiration = context1.Credentials.TokenExpiration;
  
        // Save token values for later use. 
        // hello SaveTokenDataToExternalStorage method should check 
        // whether hello TokenExpiration value is valid before saving hello token data. 
        // If it is not valid, call MediaServicesCredentials’s RefreshToken before caching.
        SaveTokenDataToExternalStorage(accessToken, tokenExpiration);
  
    <span data-ttu-id="5499c-154">使用儲存的語彙基元值 toocreate MediaServicesCredentials hello。</span><span class="sxs-lookup"><span data-stu-id="5499c-154">Use hello saved token values toocreate MediaServicesCredentials.</span></span>

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

    <span data-ttu-id="5499c-155">更新 hello 權杖副本，以防 hello 語彙基元已由 hello Media Services SDK 更新。</span><span class="sxs-lookup"><span data-stu-id="5499c-155">Update hello token copy in case hello token was updated by hello Media Services SDK.</span></span> 

        if(tokenExpiration != context2.Credentials.TokenExpiration)
        {
            UpdateTokenDataInExternalStorageIfNeeded(accessToken, context2.Credentials.TokenExpiration);
        }


* <span data-ttu-id="5499c-156">如果您有多個 Media Services 帳戶 （例如，針對載入目的或地理分散） 您可以快取使用 hello System.Collections.Concurrent.ConcurrentDictionary 集合 (hello MediaServicesCredentials 物件ConcurrentDictionary 集合代表安全執行緒集合可由多個執行緒並行存取的索引鍵/值組）。</span><span class="sxs-lookup"><span data-stu-id="5499c-156">If you have multiple Media Services accounts (for example, for load sharing purposes or Geo-distribution) you can cache MediaServicesCredentials objects using hello System.Collections.Concurrent.ConcurrentDictionary collection (hello ConcurrentDictionary collection represents a thread-safe collection of key/value pairs that can be accessed by multiple threads concurrently).</span></span> <span data-ttu-id="5499c-157">然後，您可以使用 hello GetOrAdd 方法 tooget hello 快取認證。</span><span class="sxs-lookup"><span data-stu-id="5499c-157">You can then use hello GetOrAdd method tooget hello cached credentials.</span></span> 
  
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

## <a name="connecting-tooa-media-services-account-located-in-hello-north-china-region"></a><span data-ttu-id="5499c-158">連接位於 hello 中國北部地區 tooa Media Services 帳戶</span><span class="sxs-lookup"><span data-stu-id="5499c-158">Connecting tooa Media Services account located in hello North China region</span></span>
<span data-ttu-id="5499c-159">如果您的帳戶位於 hello 中國北部地區，請使用下列建構函式的 hello:</span><span class="sxs-lookup"><span data-stu-id="5499c-159">If your account is located in hello North China region, use hello following constructor:</span></span>

    public CloudMediaContext(Uri apiServer, string accountName, string accountKey, string scope, string acsBaseAddress)

<span data-ttu-id="5499c-160">例如：</span><span class="sxs-lookup"><span data-stu-id="5499c-160">For example:</span></span>

    _context = new CloudMediaContext(
        new Uri("https://wamsbjbclus001rest-hs.chinacloudapp.cn/API/"),
        _mediaServicesAccountName,
        _mediaServicesAccountKey,
        "urn:WindowsAzureMediaServices",
        "https://wamsprodglobal001acs.accesscontrol.chinacloudapi.cn");


## <a name="storing-connection-values-in-configuration"></a><span data-ttu-id="5499c-161">在組態中儲存連線值</span><span class="sxs-lookup"><span data-stu-id="5499c-161">Storing Connection Values in Configuration</span></span>
<span data-ttu-id="5499c-162">強烈建議的作法 toostore 連接值，尤其是敏感值，例如您的帳戶名稱和密碼，在設定它。</span><span class="sxs-lookup"><span data-stu-id="5499c-162">It is a highly recommended practice toostore connection values, especially sensitive values such as your account name and password, in configuration.</span></span> <span data-ttu-id="5499c-163">此外，也是建議的作法 tooencrypt 敏感的組態資料。</span><span class="sxs-lookup"><span data-stu-id="5499c-163">Also, it is a recommended practice tooencrypt sensitive configuration data.</span></span> <span data-ttu-id="5499c-164">您可以使用 hello Windows 加密檔案系統 (EFS) 加密 hello 整個組態檔案。</span><span class="sxs-lookup"><span data-stu-id="5499c-164">You can encrypt hello entire configuration file by using hello Windows Encrypting File System (EFS).</span></span> <span data-ttu-id="5499c-165">tooenable EFS 檔案，以滑鼠右鍵按一下 hello 檔案中，選取**屬性**，並啟用加密在 hello**進階**設定 索引標籤。或者，可以使用受保護的組態，建立將選擇之組態檔案內的部分加密的自訂解決方案。</span><span class="sxs-lookup"><span data-stu-id="5499c-165">tooenable EFS on a file, right-click hello file, select **Properties**, and enable encryption in hello **Advanced** settings tab. Or you can create a custom solution for encrypting selected portions of a configuration file by using protected configuration.</span></span> <span data-ttu-id="5499c-166">請參閱 [使用受保護組態將組態資訊加密](https://msdn.microsoft.com/library/53tyfkaw.aspx)。</span><span class="sxs-lookup"><span data-stu-id="5499c-166">See [Encrypting Configuration Information Using Protected Configuration](https://msdn.microsoft.com/library/53tyfkaw.aspx).</span></span>

<span data-ttu-id="5499c-167">下列 App.config 檔的 hello 包含所需的 hello 連接值。</span><span class="sxs-lookup"><span data-stu-id="5499c-167">hello following App.config file contains hello required connection values.</span></span> <span data-ttu-id="5499c-168">hello 中 hello 值<appSettings>項目是您 hello Media Services 帳戶設定程序中取得的所需的 hello 值。</span><span class="sxs-lookup"><span data-stu-id="5499c-168">hello values in hello <appSettings> element are hello required values that you got from hello Media Services account setup process.</span></span>

    <configuration>
      <appSettings>
        <add key="MediaServicesAccountName" value="Media-Services-Account-Name" />
        <add key="MediaServicesAccountKey" value="Media-Services-Account-Key" />
      </appSettings>
    </configuration>


<span data-ttu-id="5499c-169">從組態 tooretrieve 連接值，您可以使用 hello **ConfigurationManager**類別，並將指定在程式碼中的 hello 值 toofields:</span><span class="sxs-lookup"><span data-stu-id="5499c-169">tooretrieve connection values from configuration, you can use hello **ConfigurationManager** class and then assign hello values toofields in your code:</span></span>

    private static readonly string _accountName = ConfigurationManager.AppSettings["MediaServicesAccountName"];
    private static readonly string _accountKey = ConfigurationManager.AppSettings["MediaServicesAccountKey"];



## <a name="media-services-learning-paths"></a><span data-ttu-id="5499c-170">媒體服務學習路徑</span><span class="sxs-lookup"><span data-stu-id="5499c-170">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="5499c-171">提供意見反應</span><span class="sxs-lookup"><span data-stu-id="5499c-171">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

