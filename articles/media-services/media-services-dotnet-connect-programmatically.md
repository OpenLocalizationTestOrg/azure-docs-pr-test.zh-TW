---
title: "使用 .NET 連線到媒體服務帳戶"
description: "本主題示範如何使用 .NET 連線到媒體服務。"
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
ms.openlocfilehash: 892932116934952265a21ab17aac3434b5760136
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="connecting-to-media-services-account-using-media-services-sdk-for-net"></a><span data-ttu-id="2fa85-103">使用 Media Services SDK for .NET 連線到媒體服務帳戶</span><span class="sxs-lookup"><span data-stu-id="2fa85-103">Connecting to Media Services Account using Media Services SDK for .NET</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="2fa85-104">REST</span><span class="sxs-lookup"><span data-stu-id="2fa85-104">REST</span></span>](media-services-rest-connect-programmatically.md)
> * [<span data-ttu-id="2fa85-105">.NET</span><span class="sxs-lookup"><span data-stu-id="2fa85-105">.NET</span></span>](media-services-dotnet-connect-programmatically.md)
> 
> 

<span data-ttu-id="2fa85-106">本主題描述使用 Media Services SDK for .NET 進行程式設計時，如何取得與 Microsoft Azure 媒體服務的程式設計連線。</span><span class="sxs-lookup"><span data-stu-id="2fa85-106">This topic describes how to obtain a programmatic connection to Microsoft Azure Media Services when you are programming with the Media Services SDK for .NET.</span></span>

## <a name="connecting-to-media-services"></a><span data-ttu-id="2fa85-107">連線到媒體服務</span><span class="sxs-lookup"><span data-stu-id="2fa85-107">Connecting to Media Services</span></span>
<span data-ttu-id="2fa85-108">若要以程式設計方式連線到媒體服務，您必須先前已設定 Azure 帳戶，並在該帳戶上設定媒體服務，然後設定 Visual Studio 專案，才能使用 Media Services SDK for .NET 進行開發。</span><span class="sxs-lookup"><span data-stu-id="2fa85-108">To connect to Media Services programmatically, you must have previously set up an Azure account, configured Media Services on that account, and then set up a Visual Studio project for development with the Media Services SDK for .NET.</span></span> <span data-ttu-id="2fa85-109">如需詳細資訊，請參閱＜使用 Media Services SDK for .NET　進行開發的設定＞。</span><span class="sxs-lookup"><span data-stu-id="2fa85-109">For more information, see Setup for Development with the Media Services SDK for .NET.</span></span>

<span data-ttu-id="2fa85-110">媒體服務帳戶設定程序結束時，您會取得下列必要連線值。</span><span class="sxs-lookup"><span data-stu-id="2fa85-110">At the end of the Media Services account setup process, you obtained the following required connection values.</span></span> <span data-ttu-id="2fa85-111">使用這些值，即可進行與媒體服務的程式設計連線。</span><span class="sxs-lookup"><span data-stu-id="2fa85-111">Use these to make programmatic connections to Media Services.</span></span>

* <span data-ttu-id="2fa85-112">媒體服務帳戶名稱。</span><span class="sxs-lookup"><span data-stu-id="2fa85-112">Your Media Services account name.</span></span>
* <span data-ttu-id="2fa85-113">媒體服務帳戶金鑰。</span><span class="sxs-lookup"><span data-stu-id="2fa85-113">Your Media Services account key.</span></span>

<span data-ttu-id="2fa85-114">若要尋找這些值，請移至 Azure 管理入口網站，並選取您的媒體服務帳戶，然後按一下入口網站視窗底部的 [管理金鑰]圖示。</span><span class="sxs-lookup"><span data-stu-id="2fa85-114">To find these values, go to the Azure Managment Portal, select your Media Service account, and click on the “**MANAGE KEYS**” icon on the bottom of the portal window.</span></span> <span data-ttu-id="2fa85-115">按一下每個文字方塊旁邊的圖示，會將值複製到系統剪貼簿。</span><span class="sxs-lookup"><span data-stu-id="2fa85-115">Clicking on the icon next to each text box copies the value to the system clipboard.</span></span>

## <a name="creating-a-cloudmediacontext-instance"></a><span data-ttu-id="2fa85-116">建立 CloudMediaContext 執行個體</span><span class="sxs-lookup"><span data-stu-id="2fa85-116">Creating a CloudMediaContext Instance</span></span>
<span data-ttu-id="2fa85-117">若要開始針對媒體服務進行程式設計，您需要建立可呈現伺服器內容的 **CloudMediaContext** 執行個體。</span><span class="sxs-lookup"><span data-stu-id="2fa85-117">To start programming against Media Services you need to create a **CloudMediaContext** instance that represents the server context.</span></span> <span data-ttu-id="2fa85-118">**CloudMediaContext** 包含重要集合的參考，包括工作、資產、檔案、存取原則和定位器。</span><span class="sxs-lookup"><span data-stu-id="2fa85-118">The **CloudMediaContext** includes references to important collections including jobs, assets, files, access policies, and locators.</span></span>

> [!NOTE]
> <span data-ttu-id="2fa85-119">**CloudMediaContext** 類別不具備執行緒安全。</span><span class="sxs-lookup"><span data-stu-id="2fa85-119">The **CloudMediaContext** class is not thread safe.</span></span> <span data-ttu-id="2fa85-120">您應該為每個執行緒或每組作業建立新的 CloudMediaContext。</span><span class="sxs-lookup"><span data-stu-id="2fa85-120">You should create a new CloudMediaContext per thread or per set of operations.</span></span>
> 
> 

<span data-ttu-id="2fa85-121">CloudMediaContext 有五個建構函式多載。</span><span class="sxs-lookup"><span data-stu-id="2fa85-121">CloudMediaContext has five constructor overloads.</span></span> <span data-ttu-id="2fa85-122">建議使用採用 **MediaServicesCredentials** 做為參數的建構函式。</span><span class="sxs-lookup"><span data-stu-id="2fa85-122">It is recommended to use constructors that take **MediaServicesCredentials** as a parameter.</span></span> <span data-ttu-id="2fa85-123">如需詳細資訊，請參閱下面的 **重複使用存取控制服務權杖** 。</span><span class="sxs-lookup"><span data-stu-id="2fa85-123">For more information, see the **Reusing Access Control Service Tokens** that follows.</span></span> 

<span data-ttu-id="2fa85-124">下列範例會使用公用 CloudMediaContext(MediaServicesCredentials 認證) 建構函式：</span><span class="sxs-lookup"><span data-stu-id="2fa85-124">The following example uses the public CloudMediaContext(MediaServicesCredentials credentials) constructor:</span></span>

    // _cachedCredentials and _context are class member variables. 
    _cachedCredentials = new MediaServicesCredentials(
                    _mediaServicesAccountName,
                    _mediaServicesAccountKey);

    _context = new CloudMediaContext(_cachedCredentials);


## <a name="reusing-access-control-service-tokens"></a><span data-ttu-id="2fa85-125">重複使用存取控制服務權杖</span><span class="sxs-lookup"><span data-stu-id="2fa85-125">Reusing Access Control Service Tokens</span></span>
<span data-ttu-id="2fa85-126">本節顯示如何使用採用 MediaServicesCredentials 做為參數的 CloudMediaContext 建構函式，來重複使用存取控制服務權杖。</span><span class="sxs-lookup"><span data-stu-id="2fa85-126">This section shows how to reuse Access Control Service tokens by using CloudMediaContext constructors that take MediaServicesCredentials as a parameter.</span></span>

<span data-ttu-id="2fa85-127">[Azure Active Directory 存取控制](https://msdn.microsoft.com/library/hh147631.aspx) (也稱為存取控制服務或 ACS) 是一種雲端型服務，可提供簡單的方式來驗證和授權使用者存取其 Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="2fa85-127">[Azure Active Directory Access Control](https://msdn.microsoft.com/library/hh147631.aspx) (also known as Access Control Service or ACS) is a cloud-based service that provides an easy way of authenticating and authorizing users to gain access to their web applications.</span></span> <span data-ttu-id="2fa85-128">Microsoft Azure 媒體服務會透過需要 ACS 權杖的 OAuth 通訊協定來控制其服務的存取。</span><span class="sxs-lookup"><span data-stu-id="2fa85-128">Microsoft Azure Media Services controls access to its services though OAuth protocol that requires an ACS token.</span></span> <span data-ttu-id="2fa85-129">媒體服務會收到來自授權伺服器的 ACS 權杖。</span><span class="sxs-lookup"><span data-stu-id="2fa85-129">Media Services receives the ACS tokens from an authorization server.</span></span>

<span data-ttu-id="2fa85-130">使用 Media Services SDK 進行開發時，您可以選擇不處理權杖，因為 SDK 程式碼會進行管理。</span><span class="sxs-lookup"><span data-stu-id="2fa85-130">When developing with the Media Services SDK, you can choose to not deal with the tokens because the SDK code managers them for you.</span></span> <span data-ttu-id="2fa85-131">不過，讓 SDK 全權管理 ACS 權杖會導致不必要的權杖要求。</span><span class="sxs-lookup"><span data-stu-id="2fa85-131">However, letting the SDK fully manage the ACS tokens leads to unnecessary token requests.</span></span> <span data-ttu-id="2fa85-132">要求權杖十分耗時，並且會耗用用戶端和伺服器資源。</span><span class="sxs-lookup"><span data-stu-id="2fa85-132">Requesting tokens takes time and consumes the client and server resources.</span></span> <span data-ttu-id="2fa85-133">此外，如果速率太高，則 ACS 伺服器會節流處理要求。</span><span class="sxs-lookup"><span data-stu-id="2fa85-133">Also, the ACS server throttles the requests if the rate is too high.</span></span> <span data-ttu-id="2fa85-134">限制是每秒 30 個要求，如需詳細資料，請參閱 [ACS 服務限制](https://msdn.microsoft.com/library/gg185909.aspx) 。</span><span class="sxs-lookup"><span data-stu-id="2fa85-134">The limit is 30 requests per second, see [ACS Service Limitations](https://msdn.microsoft.com/library/gg185909.aspx) for more details.</span></span>

<span data-ttu-id="2fa85-135">從 Media Services SDK 3.0.0.0 版開始，您可以重複使用 ACS 權杖。</span><span class="sxs-lookup"><span data-stu-id="2fa85-135">Starting with the Media Services SDK version 3.0.0.0, you can reuse the ACS tokens.</span></span> <span data-ttu-id="2fa85-136">採用 **MediaServicesCredentials** 做為參數的 **CloudMediaContext** 建構函式會啟用多個內容之間的 ACS 權杖共用。</span><span class="sxs-lookup"><span data-stu-id="2fa85-136">The **CloudMediaContext** constructors that take **MediaServicesCredentials** as a parameter enable sharing the ACS tokens between multiple contexts.</span></span> <span data-ttu-id="2fa85-137">MediaServicesCredentials 類別會封裝媒體服務認證。</span><span class="sxs-lookup"><span data-stu-id="2fa85-137">The MediaServicesCredentials class encapsulates the Media Services credentials.</span></span> <span data-ttu-id="2fa85-138">如果有 ACS 權杖可用，並且知道其到期時間，則可以使用權杖建立新的 MediaServicesCredentials 執行個體，並將它傳遞給 CloudMediaContext 的建構函式。</span><span class="sxs-lookup"><span data-stu-id="2fa85-138">If an ACS token is available and its expiration time is known, you can create a new MediaServicesCredentials instance with the token and pass it to the constructor of CloudMediaContext.</span></span> <span data-ttu-id="2fa85-139">請注意，Media Services SDK 會在權杖到期時自動重新整理權杖。</span><span class="sxs-lookup"><span data-stu-id="2fa85-139">Note that the Media Services SDK automatically refreshes tokens whenever they expire.</span></span> <span data-ttu-id="2fa85-140">如下列範例所示，有兩種方式可以重複使用 ACS 權杖。</span><span class="sxs-lookup"><span data-stu-id="2fa85-140">There are two ways to reuse ACS tokens, as shown in the examples below.</span></span>

* <span data-ttu-id="2fa85-141">您可以快取記憶體中的 **MediaServicesCredentials** 物件 (例如，在靜態類別變數中)。</span><span class="sxs-lookup"><span data-stu-id="2fa85-141">You can cache the **MediaServicesCredentials** object in memory (for example, in a static class variable).</span></span> <span data-ttu-id="2fa85-142">然後，將快取的物件傳遞至 CloudMediaContext 建構函式。</span><span class="sxs-lookup"><span data-stu-id="2fa85-142">Then, pass the cached object to the CloudMediaContext constructor.</span></span> <span data-ttu-id="2fa85-143">MediaServicesCredentials 物件包含可重複使用的 ACS 權杖 (如果仍然有效)。</span><span class="sxs-lookup"><span data-stu-id="2fa85-143">The MediaServicesCredentials object contains an ACS token that can be reused if it is still valid.</span></span> <span data-ttu-id="2fa85-144">如果權杖無效，則 Media Services SDK 會使用提供給 MediaServicesCredentials 建構函式的認證來重新整理權杖。</span><span class="sxs-lookup"><span data-stu-id="2fa85-144">If the token is not valid, it will be refreshed by the Media Services SDK using the credentials given to the MediaServicesCredentials constructor.</span></span>
  
    <span data-ttu-id="2fa85-145">請注意，呼叫 RefreshToken 之後， **MediaServicesCredentials** 物件會取得有效的權杖。</span><span class="sxs-lookup"><span data-stu-id="2fa85-145">Note that the **MediaServicesCredentials** object gets a valid token after the RefreshToken is called.</span></span> <span data-ttu-id="2fa85-146">**CloudMediaContext** 會呼叫建構函式中的 **RefreshToken** 方法。</span><span class="sxs-lookup"><span data-stu-id="2fa85-146">The **CloudMediaContext** calls the **RefreshToken** method in the constructor.</span></span> <span data-ttu-id="2fa85-147">如果您想要將權杖值儲存到外接式儲存裝置，請一定要先檢查 TokenExpiration 值是否有效，再儲存權杖資料。</span><span class="sxs-lookup"><span data-stu-id="2fa85-147">If you are planning to save the token values to an external storage, make sure to check whether the TokenExpiration value is valid before saving the token data.</span></span> <span data-ttu-id="2fa85-148">如果無效，則請在快取前呼叫 RefreshToken。</span><span class="sxs-lookup"><span data-stu-id="2fa85-148">If it is not valid, call RefreshToken before caching.</span></span>
  
        // Create and cache the Media Services credentials in a static class variable.
        _cachedCredentials = new MediaServicesCredentials(_mediaServicesAccountName, _mediaServicesAccountKey);

        // Use the cached credentials to create a new CloudMediaContext object.
        if(_cachedCredentials == null)
        {
            _cachedCredentials = new MediaServicesCredentials(_mediaServicesAccountName, _mediaServicesAccountKey);
        }

        CloudMediaContext context = new CloudMediaContext(_cachedCredentials);

* <span data-ttu-id="2fa85-149">您也可以快取 AccessToken 字串和 TokenExpiration 值。</span><span class="sxs-lookup"><span data-stu-id="2fa85-149">You can also cache the AccessToken string and the TokenExpiration values.</span></span> <span data-ttu-id="2fa85-150">稍後可以使用這些值，來建立具有快取權杖資料的新 MediaServicesCredentials 物件。</span><span class="sxs-lookup"><span data-stu-id="2fa85-150">The values could later be used to create a new MediaServicesCredentials object with the cached token data.</span></span>  <span data-ttu-id="2fa85-151">這特別適用於權杖可以在多個處理程序或電腦之間安全共用的情況。</span><span class="sxs-lookup"><span data-stu-id="2fa85-151">This is especially useful for scenarios where the token can be securely shared among multiple processes or computers.</span></span>
  
    <span data-ttu-id="2fa85-152">下列程式碼片段會呼叫此範例中未定義的 SaveTokenDataToExternalStorage、GetTokenDataFromExternalStorage 和 UpdateTokenDataInExternalStorageIfNeeded 方法。</span><span class="sxs-lookup"><span data-stu-id="2fa85-152">The following code snippets call the SaveTokenDataToExternalStorage, GetTokenDataFromExternalStorage, and UpdateTokenDataInExternalStorageIfNeeded methods that are not defined in this example.</span></span> <span data-ttu-id="2fa85-153">您可以定義這些方法來儲存、擷取和更新外接式儲存裝置中的權杖資料。</span><span class="sxs-lookup"><span data-stu-id="2fa85-153">You could define these methods to store, retrieve, and update token data in an external storage.</span></span> 
  
        CloudMediaContext context1 = new CloudMediaContext(_mediaServicesAccountName, _mediaServicesAccountKey);
  
        // Get token values from the context.
        var accessToken = context1.Credentials.AccessToken;
        var tokenExpiration = context1.Credentials.TokenExpiration;
  
        // Save token values for later use. 
        // The SaveTokenDataToExternalStorage method should check 
        // whether the TokenExpiration value is valid before saving the token data. 
        // If it is not valid, call MediaServicesCredentials’s RefreshToken before caching.
        SaveTokenDataToExternalStorage(accessToken, tokenExpiration);
  
    <span data-ttu-id="2fa85-154">使用儲存的權杖值來建立 MediaServicesCredentials。</span><span class="sxs-lookup"><span data-stu-id="2fa85-154">Use the saved token values to create MediaServicesCredentials.</span></span>

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

    <span data-ttu-id="2fa85-155">更新權杖副本 (以免媒體服務 SDK 已更新權杖)。</span><span class="sxs-lookup"><span data-stu-id="2fa85-155">Update the token copy in case the token was updated by the Media Services SDK.</span></span> 

        if(tokenExpiration != context2.Credentials.TokenExpiration)
        {
            UpdateTokenDataInExternalStorageIfNeeded(accessToken, context2.Credentials.TokenExpiration);
        }


* <span data-ttu-id="2fa85-156">如果您有多個媒體服務帳戶 (例如，針對負載共用目的或地理分散)，則可以使用 System.Collections.Concurrent.ConcurrentDictionary 集合來快取 MediaServicesCredentials 物件 (ConcurrentDictionary 集合代表多個執行緒可以並行存取之金鑰/值組的執行緒安全集合)。</span><span class="sxs-lookup"><span data-stu-id="2fa85-156">If you have multiple Media Services accounts (for example, for load sharing purposes or Geo-distribution) you can cache MediaServicesCredentials objects using the System.Collections.Concurrent.ConcurrentDictionary collection (the ConcurrentDictionary collection represents a thread-safe collection of key/value pairs that can be accessed by multiple threads concurrently).</span></span> <span data-ttu-id="2fa85-157">您之後就可以使用 GetOrAdd 方法來取得快取的認證。</span><span class="sxs-lookup"><span data-stu-id="2fa85-157">You can then use the GetOrAdd method to get the cached credentials.</span></span> 
  
        // Declare a static class variable of the ConcurrentDictionary type in which the Media Services credentials will be cached.  
        private static readonly ConcurrentDictionary<string, MediaServicesCredentials> mediaServicesCredentialsCache = 
            new ConcurrentDictionary<string, MediaServicesCredentials>();

        // Cache (or get already cached) Media Services credentials. Use these credentials to create a new CloudMediaContext object.
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

## <a name="connecting-to-a-media-services-account-located-in-the-north-china-region"></a><span data-ttu-id="2fa85-158">連線到位於中國北部地區的媒體服務帳戶</span><span class="sxs-lookup"><span data-stu-id="2fa85-158">Connecting to a Media Services account located in the North China region</span></span>
<span data-ttu-id="2fa85-159">如果您的帳戶位於中國北部地區，請使用下列建構函式：</span><span class="sxs-lookup"><span data-stu-id="2fa85-159">If your account is located in the North China region, use the following constructor:</span></span>

    public CloudMediaContext(Uri apiServer, string accountName, string accountKey, string scope, string acsBaseAddress)

<span data-ttu-id="2fa85-160">例如：</span><span class="sxs-lookup"><span data-stu-id="2fa85-160">For example:</span></span>

    _context = new CloudMediaContext(
        new Uri("https://wamsbjbclus001rest-hs.chinacloudapp.cn/API/"),
        _mediaServicesAccountName,
        _mediaServicesAccountKey,
        "urn:WindowsAzureMediaServices",
        "https://wamsprodglobal001acs.accesscontrol.chinacloudapi.cn");


## <a name="storing-connection-values-in-configuration"></a><span data-ttu-id="2fa85-161">在組態中儲存連線值</span><span class="sxs-lookup"><span data-stu-id="2fa85-161">Storing Connection Values in Configuration</span></span>
<span data-ttu-id="2fa85-162">強烈建議使用這種作法將連線值儲存在組態中，尤其是敏感的值 (例如您的帳戶名稱與密碼)。</span><span class="sxs-lookup"><span data-stu-id="2fa85-162">It is a highly recommended practice to store connection values, especially sensitive values such as your account name and password, in configuration.</span></span> <span data-ttu-id="2fa85-163">另外，也建議將敏感的組態資料加密。</span><span class="sxs-lookup"><span data-stu-id="2fa85-163">Also, it is a recommended practice to encrypt sensitive configuration data.</span></span> <span data-ttu-id="2fa85-164">您可以使用 Windows 加密檔案系統 (EFS) 將整個組態檔加密。</span><span class="sxs-lookup"><span data-stu-id="2fa85-164">You can encrypt the entire configuration file by using the Windows Encrypting File System (EFS).</span></span> <span data-ttu-id="2fa85-165">若要在檔案上啟用 EFS，請在檔案上按一下滑鼠右鍵，並選取 [屬性]，然後在 [進階設定] 索引標籤中啟用加密。</span><span class="sxs-lookup"><span data-stu-id="2fa85-165">To enable EFS on a file, right-click the file, select **Properties**, and enable encryption in the **Advanced** settings tab.</span></span> <span data-ttu-id="2fa85-166">或者，可以使用受保護的組態，建立將選擇之組態檔案內的部分加密的自訂解決方案。</span><span class="sxs-lookup"><span data-stu-id="2fa85-166">Or you can create a custom solution for encrypting selected portions of a configuration file by using protected configuration.</span></span> <span data-ttu-id="2fa85-167">請參閱 [使用受保護組態將組態資訊加密](https://msdn.microsoft.com/library/53tyfkaw.aspx)。</span><span class="sxs-lookup"><span data-stu-id="2fa85-167">See [Encrypting Configuration Information Using Protected Configuration](https://msdn.microsoft.com/library/53tyfkaw.aspx).</span></span>

<span data-ttu-id="2fa85-168">下列 App.config 檔案包含必要的連線值。</span><span class="sxs-lookup"><span data-stu-id="2fa85-168">The following App.config file contains the required connection values.</span></span> <span data-ttu-id="2fa85-169"><appSettings> 元素中的值是您在媒體服務帳戶設定程序中取得的必要值。</span><span class="sxs-lookup"><span data-stu-id="2fa85-169">The values in the <appSettings> element are the required values that you got from the Media Services account setup process.</span></span>

    <configuration>
      <appSettings>
        <add key="MediaServicesAccountName" value="Media-Services-Account-Name" />
        <add key="MediaServicesAccountKey" value="Media-Services-Account-Key" />
      </appSettings>
    </configuration>


<span data-ttu-id="2fa85-170">若要從組態擷取連線值，可以使用 **ConfigurationManager** 類別，然後將值指派至程式碼中的欄位：</span><span class="sxs-lookup"><span data-stu-id="2fa85-170">To retrieve connection values from configuration, you can use the **ConfigurationManager** class and then assign the values to fields in your code:</span></span>

    private static readonly string _accountName = ConfigurationManager.AppSettings["MediaServicesAccountName"];
    private static readonly string _accountKey = ConfigurationManager.AppSettings["MediaServicesAccountKey"];



## <a name="media-services-learning-paths"></a><span data-ttu-id="2fa85-171">媒體服務學習路徑</span><span class="sxs-lookup"><span data-stu-id="2fa85-171">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="2fa85-172">提供意見反應</span><span class="sxs-lookup"><span data-stu-id="2fa85-172">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

