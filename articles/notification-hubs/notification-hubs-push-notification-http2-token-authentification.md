---
title: "適用於 Azure 通知中樞 APNS 的權杖型 (HTTP/2) 驗證 | Microsoft Docs"
description: "本主題說明如何運用適用於 APNS 的新權杖驗證"
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
ms.openlocfilehash: 5a21bcd9f12fc3f96b17a556ba15526c35ababe2
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="token-based-http2-authentication-for-apns"></a><span data-ttu-id="81a6e-103">適用於 APNS 的權杖型 (HTTP/2) 驗證</span><span class="sxs-lookup"><span data-stu-id="81a6e-103">Token-based (HTTP/2) Authentication for APNS</span></span>
## <a name="overview"></a><span data-ttu-id="81a6e-104">概觀</span><span class="sxs-lookup"><span data-stu-id="81a6e-104">Overview</span></span>
<span data-ttu-id="81a6e-105">本文說明如何將新的 APNS HTTP/2 通訊協定與權杖型驗證搭配使用。</span><span class="sxs-lookup"><span data-stu-id="81a6e-105">This article details how to use the new APNS HTTP/2 protocol with token based authentication.</span></span>

<span data-ttu-id="81a6e-106">使用新通訊協定的主要優點包括：</span><span class="sxs-lookup"><span data-stu-id="81a6e-106">The key benefits of using the new protocol include:</span></span>
-   <span data-ttu-id="81a6e-107">產生權杖相對輕而易舉 (相較於憑證)</span><span class="sxs-lookup"><span data-stu-id="81a6e-107">Token generation is relatively hassle free (compared to certificates)</span></span>
-   <span data-ttu-id="81a6e-108">不再需要顧慮到期日 – 您可以控制驗證權杖及其撤銷</span><span class="sxs-lookup"><span data-stu-id="81a6e-108">No more expiry dates – you are in control of your authentication tokens and their revocation</span></span>
-   <span data-ttu-id="81a6e-109">目前的承載上限為 4 KB</span><span class="sxs-lookup"><span data-stu-id="81a6e-109">Payloads can now be up to 4 KB</span></span>
- <span data-ttu-id="81a6e-110">同步的意見反應</span><span class="sxs-lookup"><span data-stu-id="81a6e-110">Synchronous feedback</span></span>
-   <span data-ttu-id="81a6e-111">您會使用 Apple 的最新通訊協定 – 憑證仍使用已遭淘汰的二進位通訊協定</span><span class="sxs-lookup"><span data-stu-id="81a6e-111">You’re on Apple’s latest protocol – certificates still use the binary protocol, which is marked for deprecation</span></span>

<span data-ttu-id="81a6e-112">在幾分鐘內透過兩個步驟完成使用此新機制的動作：</span><span class="sxs-lookup"><span data-stu-id="81a6e-112">Using this new mechanism can be done in two steps in a few minutes:</span></span>
1.  <span data-ttu-id="81a6e-113">從 Apple 開發人員帳戶入口網站取得必要資訊</span><span class="sxs-lookup"><span data-stu-id="81a6e-113">Obtain the necessary information from the Apple Developer Account portal</span></span>
2.  <span data-ttu-id="81a6e-114">使用新資訊設定您的通知中樞</span><span class="sxs-lookup"><span data-stu-id="81a6e-114">Configure your notification hub with the new information</span></span>

<span data-ttu-id="81a6e-115">通知中樞目前已準備就緒，可將新驗證系統與 APNS 搭配使用。</span><span class="sxs-lookup"><span data-stu-id="81a6e-115">Notification Hubs is now all set to use the new authentication system with APNS.</span></span> 

<span data-ttu-id="81a6e-116">請注意，如果您從使用適用於 APNS 的憑證認證進行移轉：</span><span class="sxs-lookup"><span data-stu-id="81a6e-116">Note that if you migrated from using certificate credentials for APNS:</span></span>
- <span data-ttu-id="81a6e-117">權杖屬性會在我們的系統覆寫您的憑證，</span><span class="sxs-lookup"><span data-stu-id="81a6e-117">the token properties overwrite your certificate in our system,</span></span>
- <span data-ttu-id="81a6e-118">但您的應用程式仍可順利接收通知。</span><span class="sxs-lookup"><span data-stu-id="81a6e-118">but your application continues to receive notifications seamlessly.</span></span>

## <a name="obtaining-authentication-information-from-apple"></a><span data-ttu-id="81a6e-119">從 Apple 取得驗證資訊</span><span class="sxs-lookup"><span data-stu-id="81a6e-119">Obtaining authentication information from Apple</span></span>
<span data-ttu-id="81a6e-120">若要啟用權杖型驗證，您需要從 Apple 開發人員帳戶取得下列屬性：</span><span class="sxs-lookup"><span data-stu-id="81a6e-120">To enable token-based authentication, you need the following properties from your Apple Developer Account:</span></span>
### <a name="key-identifier"></a><span data-ttu-id="81a6e-121">金鑰識別碼</span><span class="sxs-lookup"><span data-stu-id="81a6e-121">Key Identifier</span></span>
<span data-ttu-id="81a6e-122">您可以從 Apple 開發人員帳戶中的 [Keys]\(金鑰\) 頁面取得金鑰識別碼</span><span class="sxs-lookup"><span data-stu-id="81a6e-122">The key identifier can be obtained from the "Keys" page in your Apple Developer Account</span></span>

![](./media/notification-hubs-push-notification-http2-token-authentification/obtaining-auth-information-from-apple.png)

### <a name="application-identifier--application-name"></a><span data-ttu-id="81a6e-123">應用程式識別碼和應用程式名稱</span><span class="sxs-lookup"><span data-stu-id="81a6e-123">Application Identifier & Application Name</span></span>
<span data-ttu-id="81a6e-124">您可以透過開發人員帳戶中的 [App IDs]\(應用程式識別碼\) 頁面取得應用程式名稱。</span><span class="sxs-lookup"><span data-stu-id="81a6e-124">The application name is available via the App IDs page in the Developer Account.</span></span> 
![](./media/notification-hubs-push-notification-http2-token-authentification/app-name.png)

<span data-ttu-id="81a6e-125">您可以透過開發人員帳戶中的成員資格詳細資料頁面取得應用程式識別碼。</span><span class="sxs-lookup"><span data-stu-id="81a6e-125">The application identifier is available via the membership details page in the Developer Account.</span></span>
![](./media/notification-hubs-push-notification-http2-token-authentification/app-id.png)


### <a name="authentication-token"></a><span data-ttu-id="81a6e-126">驗證權杖</span><span class="sxs-lookup"><span data-stu-id="81a6e-126">Authentication token</span></span>
<span data-ttu-id="81a6e-127">為應用程式產生權杖之後，您便可以下載該驗證權杖。</span><span class="sxs-lookup"><span data-stu-id="81a6e-127">The authentication token can be downloaded after you generate a token for your application.</span></span> <span data-ttu-id="81a6e-128">如需有關如何產生此權杖的詳細資訊，請參閱 [Apple 開發人員文件](http://help.apple.com/xcode/mac/current/#/dev11b059073?sub=dev1eb5dfe65) (英文)。</span><span class="sxs-lookup"><span data-stu-id="81a6e-128">For details on how to generate this token, refer to [Apple’s Developer documentation](http://help.apple.com/xcode/mac/current/#/dev11b059073?sub=dev1eb5dfe65).</span></span>

## <a name="configuring-your-notification-hub-to-use-token-based-authentication"></a><span data-ttu-id="81a6e-129">將您的通知中樞設定為使用權杖型驗證</span><span class="sxs-lookup"><span data-stu-id="81a6e-129">Configuring your notification hub to use token-based authentication</span></span>
### <a name="configure-via-the-azure-portal"></a><span data-ttu-id="81a6e-130">透過 Azure 入口網站進行設定</span><span class="sxs-lookup"><span data-stu-id="81a6e-130">Configure via the Azure portal</span></span>
<span data-ttu-id="81a6e-131">若要在入口網站中啟用權杖型驗證，請登入 Azure 入口網站，並移至 [通知中樞] > [Notification Services] > [APNS] 面板。</span><span class="sxs-lookup"><span data-stu-id="81a6e-131">To enable token based authentication in the portal, log in to the Azure portal and go to your Notification Hub > Notification Services > APNS panel.</span></span> 

<span data-ttu-id="81a6e-132">我們已提供新屬性 – 驗證模式。</span><span class="sxs-lookup"><span data-stu-id="81a6e-132">There is a new property – *Authentication Mode*.</span></span> <span data-ttu-id="81a6e-133">選取權杖可讓您透過所有相關的權杖屬性更新您的中樞。</span><span class="sxs-lookup"><span data-stu-id="81a6e-133">Selecting Token allows you to update your hub with all the relevant token properties.</span></span>

![](./media/notification-hubs-push-notification-http2-token-authentification/azure-portal-apns-settings.png)

- <span data-ttu-id="81a6e-134">輸入您從 Apple 開發人員帳戶擷取的屬性，</span><span class="sxs-lookup"><span data-stu-id="81a6e-134">Enter the properties you retrieved from your Apple developer account,</span></span> 
- <span data-ttu-id="81a6e-135">選擇您的應用程式模式 (「生產」或「沙箱」)</span><span class="sxs-lookup"><span data-stu-id="81a6e-135">choose your application mode (Production or Sandbox)</span></span> 
- <span data-ttu-id="81a6e-136">按一下 [儲存] 以更新 APNS 認證。</span><span class="sxs-lookup"><span data-stu-id="81a6e-136">click Save to update your APNS credentials.</span></span> 

### <a name="configure-via-management-api-rest"></a><span data-ttu-id="81a6e-137">透過管理 API (REST) 進行設定</span><span class="sxs-lookup"><span data-stu-id="81a6e-137">Configure via Management API (REST)</span></span>

<span data-ttu-id="81a6e-138">您可以使用我們的[管理 API](https://msdn.microsoft.com/library/azure/dn495827.aspx)，將您的通知中樞更新為使用權杖型驗證。</span><span class="sxs-lookup"><span data-stu-id="81a6e-138">You can use our [management APIs](https://msdn.microsoft.com/library/azure/dn495827.aspx) to update your notification hub to use token-based authentication.</span></span>
<span data-ttu-id="81a6e-139">根據您設定的是的「沙箱」或「生產」應用程式 (在 Apple 開發人員帳戶中指定)，使用其中一個對應端點：</span><span class="sxs-lookup"><span data-stu-id="81a6e-139">Depending on whether the application you’re configuring is a Sandbox or Production app (specified in your Apple Developer Account), use one of the corresponding endpoints:</span></span>

- <span data-ttu-id="81a6e-140">沙箱端點：[https://api.development.push.apple.com:443/3/device](https://api.development.push.apple.com:443/3/device)</span><span class="sxs-lookup"><span data-stu-id="81a6e-140">Sandbox Endpoint: [https://api.development.push.apple.com:443/3/device](https://api.development.push.apple.com:443/3/device)</span></span>
- <span data-ttu-id="81a6e-141">生產端點：[https://api.push.apple.com:443/3/device](https://api.push.apple.com:443/3/device)</span><span class="sxs-lookup"><span data-stu-id="81a6e-141">Production Endpoint: [https://api.push.apple.com:443/3/device](https://api.push.apple.com:443/3/device)</span></span>

> [!IMPORTANT]
> <span data-ttu-id="81a6e-142">權杖型驗證所需的 API 版本：**2017-04 或更新版本**。</span><span class="sxs-lookup"><span data-stu-id="81a6e-142">Token-based authentication requires an API version of: **2017-04 or later**.</span></span>
> 
> 

<span data-ttu-id="81a6e-143">透過權杖型驗證更新中樞的 PUT 要求範例如下：</span><span class="sxs-lookup"><span data-stu-id="81a6e-143">Here’s an example of a PUT request to update a hub with token-based authentication:</span></span>


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
        

### <a name="configure-via-the-net-sdk"></a><span data-ttu-id="81a6e-144">透過 .NET SDK 進行設定</span><span class="sxs-lookup"><span data-stu-id="81a6e-144">Configure via the .NET SDK</span></span>
<span data-ttu-id="81a6e-145">您可以使用我們的[最新用戶端 SDK](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/1.0.8)，將中樞設定為使用權杖型驗證。</span><span class="sxs-lookup"><span data-stu-id="81a6e-145">You can configure your hub to use token based authentication using our [latest client SDK](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/1.0.8).</span></span> 

<span data-ttu-id="81a6e-146">示範正確使用方式的程式碼範例如下：</span><span class="sxs-lookup"><span data-stu-id="81a6e-146">Here’s a code sample illustrating the correct usage:</span></span>


        NamespaceManager nm = NamespaceManager.CreateFromConnectionString(_endpoint);
        string token = "YOUR TOKEN HERE";
        string keyId = "YOUR KEY ID HERE";
        string appName = "YOUR APP NAME HERE";
        string appId = "YOUR APP ID HERE";
        NotificationHubDescription desc = new NotificationHubDescription("PATH TO YOUR HUB");
        desc.ApnsCredential = new ApnsCredential(token, keyId, appId, appName);
        desc.ApnsCredential.Endpoint = @"https://api.development.push.apple.com:443/3/device";
        nm.UpdateNotificationHubAsync(desc);

## <a name="reverting-to-using-certificate-based-authentication"></a><span data-ttu-id="81a6e-147">還原為使用憑證式驗證</span><span class="sxs-lookup"><span data-stu-id="81a6e-147">Reverting to using certificate-based authentication</span></span>
<span data-ttu-id="81a6e-148">您可以使用任何上述方法並傳遞憑證而不是權杖屬性，隨時還原為使用憑證式驗證。</span><span class="sxs-lookup"><span data-stu-id="81a6e-148">You can revert at any time to using certificate-based authentication by using any preceding method and passing the certificate instead of the token properties.</span></span> <span data-ttu-id="81a6e-149">該動作會覆寫先前儲存的認證。</span><span class="sxs-lookup"><span data-stu-id="81a6e-149">That action overwrites the previously stored credentials.</span></span>
