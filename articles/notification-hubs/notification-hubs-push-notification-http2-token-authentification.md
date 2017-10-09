---
title: "aaaToken 基礎 APNS Azure 通知中心中的 (HTTP/2) 驗證 |Microsoft 文件"
description: "本主題說明如何 tooleverage hello 新適用於 APNS 的權杖驗證"
services: notification-hubs
documentationcenter: .net
author: kpiteira
manager: erikre
editor: 
ms.service: notification-hubs
ms.workload: mobile
ms.tgt_pltfrm: mobile-multiple
ms.devlang: dotnet
ms.topic: article
ms.date: 05/17/2017
ms.author: kapiteir
ms.openlocfilehash: 3353d7f16033ce0b68edec9ee9aeb98f47faa1fa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="token-based-http2-authentication-for-apns"></a><span data-ttu-id="79ca5-103">適用於 APNS 的權杖型 (HTTP/2) 驗證</span><span class="sxs-lookup"><span data-stu-id="79ca5-103">Token-based (HTTP/2) Authentication for APNS</span></span>
## <a name="overview"></a><span data-ttu-id="79ca5-104">概觀</span><span class="sxs-lookup"><span data-stu-id="79ca5-104">Overview</span></span>
<span data-ttu-id="79ca5-105">這篇文章說明如何 toouse hello 新 APNS HTTP/2 的通訊協定與權杖型驗證。</span><span class="sxs-lookup"><span data-stu-id="79ca5-105">This article details how toouse hello new APNS HTTP/2 protocol with token based authentication.</span></span>

<span data-ttu-id="79ca5-106">使用新通訊協定 hello hello 主要優點包括：</span><span class="sxs-lookup"><span data-stu-id="79ca5-106">hello key benefits of using hello new protocol include:</span></span>
-   <span data-ttu-id="79ca5-107">語彙基元的產生是相當麻煩可用 (比較的 toocertificates)</span><span class="sxs-lookup"><span data-stu-id="79ca5-107">Token generation is relatively hassle free (compared toocertificates)</span></span>
-   <span data-ttu-id="79ca5-108">不再需要顧慮到期日 – 您可以控制驗證權杖及其撤銷</span><span class="sxs-lookup"><span data-stu-id="79ca5-108">No more expiry dates – you are in control of your authentication tokens and their revocation</span></span>
-   <span data-ttu-id="79ca5-109">裝載現在可以註冊 too4 KB</span><span class="sxs-lookup"><span data-stu-id="79ca5-109">Payloads can now be up too4 KB</span></span>
- <span data-ttu-id="79ca5-110">同步的意見反應</span><span class="sxs-lookup"><span data-stu-id="79ca5-110">Synchronous feedback</span></span>
-   <span data-ttu-id="79ca5-111">您在 Apple 的最新的通訊協定 – 憑證仍然使用 hello 二進位通訊協定，可標示為已被取代</span><span class="sxs-lookup"><span data-stu-id="79ca5-111">You’re on Apple’s latest protocol – certificates still use hello binary protocol, which is marked for deprecation</span></span>

<span data-ttu-id="79ca5-112">在幾分鐘內透過兩個步驟完成使用此新機制的動作：</span><span class="sxs-lookup"><span data-stu-id="79ca5-112">Using this new mechanism can be done in two steps in a few minutes:</span></span>
1.  <span data-ttu-id="79ca5-113">從 hello Apple 開發人員帳戶入口網站取得 hello 所需的資訊</span><span class="sxs-lookup"><span data-stu-id="79ca5-113">Obtain hello necessary information from hello Apple Developer Account portal</span></span>
2.  <span data-ttu-id="79ca5-114">使用 hello 新資訊來設定您的通知中樞</span><span class="sxs-lookup"><span data-stu-id="79ca5-114">Configure your notification hub with hello new information</span></span>

<span data-ttu-id="79ca5-115">通知中樞現在是所有集合 toouse hello 新驗證系統使用 APNS。</span><span class="sxs-lookup"><span data-stu-id="79ca5-115">Notification Hubs is now all set toouse hello new authentication system with APNS.</span></span> 

<span data-ttu-id="79ca5-116">請注意，如果您從使用適用於 APNS 的憑證認證進行移轉：</span><span class="sxs-lookup"><span data-stu-id="79ca5-116">Note that if you migrated from using certificate credentials for APNS:</span></span>
- <span data-ttu-id="79ca5-117">您的憑證覆寫在我們的系統，hello 權杖屬性</span><span class="sxs-lookup"><span data-stu-id="79ca5-117">hello token properties overwrite your certificate in our system,</span></span>
- <span data-ttu-id="79ca5-118">但您的應用程式會順暢地繼續 tooreceive 通知。</span><span class="sxs-lookup"><span data-stu-id="79ca5-118">but your application continues tooreceive notifications seamlessly.</span></span>

## <a name="obtaining-authentication-information-from-apple"></a><span data-ttu-id="79ca5-119">從 Apple 取得驗證資訊</span><span class="sxs-lookup"><span data-stu-id="79ca5-119">Obtaining authentication information from Apple</span></span>
<span data-ttu-id="79ca5-120">tooenable 權杖型驗證，您需要 hello Apple 開發人員帳戶中的下列屬性：</span><span class="sxs-lookup"><span data-stu-id="79ca5-120">tooenable token-based authentication, you need hello following properties from your Apple Developer Account:</span></span>
### <a name="key-identifier"></a><span data-ttu-id="79ca5-121">金鑰識別碼</span><span class="sxs-lookup"><span data-stu-id="79ca5-121">Key Identifier</span></span>
<span data-ttu-id="79ca5-122">您可以從 hello Apple 開發人員帳戶中的 「 金鑰 」 頁面取得 hello 金鑰識別碼</span><span class="sxs-lookup"><span data-stu-id="79ca5-122">hello key identifier can be obtained from hello "Keys" page in your Apple Developer Account</span></span>

![](./media/notification-hubs-push-notification-http2-token-authentification/obtaining-auth-information-from-apple.png)

### <a name="application-identifier--application-name"></a><span data-ttu-id="79ca5-123">應用程式識別碼和應用程式名稱</span><span class="sxs-lookup"><span data-stu-id="79ca5-123">Application Identifier & Application Name</span></span>
<span data-ttu-id="79ca5-124">透過在 hello 開發人員帳戶中的 hello 應用程式識別碼頁面可使用 hello 應用程式名稱。</span><span class="sxs-lookup"><span data-stu-id="79ca5-124">hello application name is available via hello App IDs page in hello Developer Account.</span></span> 
![](./media/notification-hubs-push-notification-http2-token-authentification/app-name.png)

<span data-ttu-id="79ca5-125">hello 應用程式識別碼是可透過 hello 開發人員帳戶中的 hello 成員資格詳細資料頁面。</span><span class="sxs-lookup"><span data-stu-id="79ca5-125">hello application identifier is available via hello membership details page in hello Developer Account.</span></span>
![](./media/notification-hubs-push-notification-http2-token-authentification/app-id.png)


### <a name="authentication-token"></a><span data-ttu-id="79ca5-126">驗證權杖</span><span class="sxs-lookup"><span data-stu-id="79ca5-126">Authentication token</span></span>
<span data-ttu-id="79ca5-127">則產生權杖，應用程式之後，您可以下載 hello 驗證權杖。</span><span class="sxs-lookup"><span data-stu-id="79ca5-127">hello authentication token can be downloaded after you generate a token for your application.</span></span> <span data-ttu-id="79ca5-128">如如何 toogenerate 這權杖的詳細資訊，請參閱太[Apple 開發人員文件](http://help.apple.com/xcode/mac/current/#/dev11b059073?sub=dev1eb5dfe65)。</span><span class="sxs-lookup"><span data-stu-id="79ca5-128">For details on how toogenerate this token, refer too[Apple’s Developer documentation](http://help.apple.com/xcode/mac/current/#/dev11b059073?sub=dev1eb5dfe65).</span></span>

## <a name="configuring-your-notification-hub-toouse-token-based-authentication"></a><span data-ttu-id="79ca5-129">設定通知中樞 toouse 權杖型驗證</span><span class="sxs-lookup"><span data-stu-id="79ca5-129">Configuring your notification hub toouse token-based authentication</span></span>
### <a name="configure-via-hello-azure-portal"></a><span data-ttu-id="79ca5-130">透過 hello Azure 入口網站設定</span><span class="sxs-lookup"><span data-stu-id="79ca5-130">Configure via hello Azure portal</span></span>
<span data-ttu-id="79ca5-131">tooenable 權杖型驗證在 hello 入口網站登入 toohello Azure 入口網站，並移 tooyour 通知中樞 > Notification Services > APNS 面板。</span><span class="sxs-lookup"><span data-stu-id="79ca5-131">tooenable token based authentication in hello portal, log in toohello Azure portal and go tooyour Notification Hub > Notification Services > APNS panel.</span></span> 

<span data-ttu-id="79ca5-132">我們已提供新屬性 – 驗證模式。</span><span class="sxs-lookup"><span data-stu-id="79ca5-132">There is a new property – *Authentication Mode*.</span></span> <span data-ttu-id="79ca5-133">選取語彙基元可讓您 tooupdate 您與所有相關語彙基元屬性 hello 的中樞。</span><span class="sxs-lookup"><span data-stu-id="79ca5-133">Selecting Token allows you tooupdate your hub with all hello relevant token properties.</span></span>

![](./media/notification-hubs-push-notification-http2-token-authentification/azure-portal-apns-settings.png)

- <span data-ttu-id="79ca5-134">輸入您從 Apple 開發人員帳戶，擷取 hello 屬性</span><span class="sxs-lookup"><span data-stu-id="79ca5-134">Enter hello properties you retrieved from your Apple developer account,</span></span> 
- <span data-ttu-id="79ca5-135">選擇您的應用程式模式 (「生產」或「沙箱」)</span><span class="sxs-lookup"><span data-stu-id="79ca5-135">choose your application mode (Production or Sandbox)</span></span> 
- <span data-ttu-id="79ca5-136">按一下 儲存 tooupdate APNS 憑證。</span><span class="sxs-lookup"><span data-stu-id="79ca5-136">click Save tooupdate your APNS credentials.</span></span> 

### <a name="configure-via-management-api-rest"></a><span data-ttu-id="79ca5-137">透過管理 API (REST) 進行設定</span><span class="sxs-lookup"><span data-stu-id="79ca5-137">Configure via Management API (REST)</span></span>

<span data-ttu-id="79ca5-138">您可以使用我們[管理 Api](https://msdn.microsoft.com/library/azure/dn495827.aspx) tooupdate 通知中樞 toouse 權杖型驗證。</span><span class="sxs-lookup"><span data-stu-id="79ca5-138">You can use our [management APIs](https://msdn.microsoft.com/library/azure/dn495827.aspx) tooupdate your notification hub toouse token-based authentication.</span></span>
<span data-ttu-id="79ca5-139">根據您設定的 hello 應用程式是否 （Apple 開發人員帳戶中指定） 的沙箱或實際執行應用程式，使用其中一種 hello 對應的端點：</span><span class="sxs-lookup"><span data-stu-id="79ca5-139">Depending on whether hello application you’re configuring is a Sandbox or Production app (specified in your Apple Developer Account), use one of hello corresponding endpoints:</span></span>

- <span data-ttu-id="79ca5-140">沙箱端點：[https://api.development.push.apple.com:443/3/device](https://api.development.push.apple.com:443/3/device)</span><span class="sxs-lookup"><span data-stu-id="79ca5-140">Sandbox Endpoint: [https://api.development.push.apple.com:443/3/device](https://api.development.push.apple.com:443/3/device)</span></span>
- <span data-ttu-id="79ca5-141">生產端點：[https://api.push.apple.com:443/3/device](https://api.push.apple.com:443/3/device)</span><span class="sxs-lookup"><span data-stu-id="79ca5-141">Production Endpoint: [https://api.push.apple.com:443/3/device](https://api.push.apple.com:443/3/device)</span></span>

> [!IMPORTANT]
> <span data-ttu-id="79ca5-142">權杖型驗證所需的 API 版本：**2017-04 或更新版本**。</span><span class="sxs-lookup"><span data-stu-id="79ca5-142">Token-based authentication requires an API version of: **2017-04 or later**.</span></span>
> 
> 

<span data-ttu-id="79ca5-143">PUT 要求 tooupdate 集線器使用權杖型驗證的範例如下：</span><span class="sxs-lookup"><span data-stu-id="79ca5-143">Here’s an example of a PUT request tooupdate a hub with token-based authentication:</span></span>


        PUT https://{namespace}.servicebus.windows.net/{Notification Hub}?api-version=2017-04
          "Properties": {
            "ApnsCredential": {
              "Properties": {
                "KeyId": "<Your Key Id>",
                "Token": "<Your Authentication Token>",
                "AppName": "<Your Application Name>",
                "AppId": "<Your Application Id>",
                "Endpoint":"<Sandbox/Production Endpoint>"
              }
            }
          }
        

### <a name="configure-via-hello-net-sdk"></a><span data-ttu-id="79ca5-144">設定透過 hello.NET SDK</span><span class="sxs-lookup"><span data-stu-id="79ca5-144">Configure via hello .NET SDK</span></span>
<span data-ttu-id="79ca5-145">您可以設定程式中樞 toouse 權杖型的驗證，請使用我們[最新的用戶端 SDK](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/1.0.8)。</span><span class="sxs-lookup"><span data-stu-id="79ca5-145">You can configure your hub toouse token based authentication using our [latest client SDK](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/1.0.8).</span></span> 

<span data-ttu-id="79ca5-146">以下是程式碼範例說明 hello 正確使用方式：</span><span class="sxs-lookup"><span data-stu-id="79ca5-146">Here’s a code sample illustrating hello correct usage:</span></span>


        NamespaceManager nm = NamespaceManager.CreateFromConnectionString(_endpoint);
        string token = "YOUR TOKEN HERE";
        string keyId = "YOUR KEY ID HERE";
        string appName = "YOUR APP NAME HERE";
        string appId = "YOUR APP ID HERE";
        NotificationHubDescription desc = new NotificationHubDescription("PATH tooYOUR HUB");
        desc.ApnsCredential = new ApnsCredential(token, keyId, appId, appName);
        desc.ApnsCredential.Endpoint = @"https://api.development.push.apple.com:443/3/device";
        nm.UpdateNotificationHubAsync(desc);

## <a name="reverting-toousing-certificate-based-authentication"></a><span data-ttu-id="79ca5-147">還原 toousing 憑證式驗證</span><span class="sxs-lookup"><span data-stu-id="79ca5-147">Reverting toousing certificate-based authentication</span></span>
<span data-ttu-id="79ca5-148">您可以使用任何上述的方法，並將 hello 憑證而非 hello 語彙基元屬性還原在任何時間 toousing 憑證式驗證。</span><span class="sxs-lookup"><span data-stu-id="79ca5-148">You can revert at any time toousing certificate-based authentication by using any preceding method and passing hello certificate instead of hello token properties.</span></span> <span data-ttu-id="79ca5-149">動作會覆寫 hello 先前預存認證。</span><span class="sxs-lookup"><span data-stu-id="79ca5-149">That action overwrites hello previously stored credentials.</span></span>
