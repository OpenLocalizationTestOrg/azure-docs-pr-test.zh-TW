---
title: "aaaHow tooconfigure Microsoft 帳戶驗證您的應用程式服務應用程式"
description: "深入了解如何 tooconfigure Microsoft 帳戶驗證您的應用程式服務應用程式。"
author: mattchenderson
services: app-service
documentationcenter: 
manager: syntaxc4
editor: 
ms.assetid: ffbc6064-edf6-474d-971c-695598fd08bf
ms.service: app-service
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: multiple
ms.topic: article
ms.date: 10/01/2016
ms.author: mahender
ms.openlocfilehash: d86d8dab26a189f4454082fc18e44e3fb6e0a01d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooconfigure-your-app-service-application-toouse-microsoft-account-login"></a><span data-ttu-id="68b77-103">如何 tooconfigure 您 App Service 應用程式 toouse 的 Microsoft 帳戶登入</span><span class="sxs-lookup"><span data-stu-id="68b77-103">How tooconfigure your App Service application toouse Microsoft Account login</span></span>
[!INCLUDE [app-service-mobile-selector-authentication](../../includes/app-service-mobile-selector-authentication.md)]

<span data-ttu-id="68b77-104">本主題說明如何 tooconfigure Azure App Service toouse 作為驗證提供者的 Microsoft 帳戶。</span><span class="sxs-lookup"><span data-stu-id="68b77-104">This topic shows you how tooconfigure Azure App Service toouse Microsoft Account as an authentication provider.</span></span> 

## <span data-ttu-id="68b77-105"><a name="register-microsoft-account"> </a>使用 Microsoft 帳戶註冊應用程式</span><span class="sxs-lookup"><span data-stu-id="68b77-105"><a name="register-microsoft-account"> </a>Register your app with Microsoft Account</span></span>
1. <span data-ttu-id="68b77-106">登入 toohello [Azure 入口網站]，並瀏覽 tooyour 應用程式。</span><span class="sxs-lookup"><span data-stu-id="68b77-106">Log on toohello [Azure portal], and navigate tooyour application.</span></span> <span data-ttu-id="68b77-107">複製您**URL**，稍後您使用 tooconfigure 您的應用程式使用 Microsoft 帳戶。</span><span class="sxs-lookup"><span data-stu-id="68b77-107">Copy your **URL**, which later you use tooconfigure your app with Microsoft Account.</span></span>
2. <span data-ttu-id="68b77-108">瀏覽 toohello[我的應用程式]hello Microsoft 帳戶開發人員中心，在頁面上，並視需要使用您的 Microsoft 帳戶登入。</span><span class="sxs-lookup"><span data-stu-id="68b77-108">Navigate toohello [My Applications] page in hello Microsoft Account Developer Center, and log on with your Microsoft account, if required.</span></span>
3. <span data-ttu-id="68b77-109">按一下 [新增應用程式]，然後輸入應用程式名稱，再按一下 [建立應用程式]。</span><span class="sxs-lookup"><span data-stu-id="68b77-109">Click **Add an app**, then type an application name, and click **Create application**.</span></span>
4. <span data-ttu-id="68b77-110">請記下 hello**應用程式識別碼**，因為您稍後需要它。</span><span class="sxs-lookup"><span data-stu-id="68b77-110">Make a note of hello **Application ID**, as you will need it later.</span></span> 
5. <span data-ttu-id="68b77-111">在 [平台] 下，按一下 [新增平台]  ，然後選取 [網站]。</span><span class="sxs-lookup"><span data-stu-id="68b77-111">Under "Platforms," click **Add Platform** and select "Web".</span></span>
6. <span data-ttu-id="68b77-112">然後按一下 應用程式 」 重新導向 Uri"供應 hello 端點下,**儲存**。</span><span class="sxs-lookup"><span data-stu-id="68b77-112">Under "Redirect URIs" supply hello endpoint for your application, then click **Save**.</span></span> 
   
   > [!NOTE]
   > <span data-ttu-id="68b77-113">您重新導向 URI 是應用程式加上 hello 路徑 hello URL */.auth/login/microsoftaccount/callback*。</span><span class="sxs-lookup"><span data-stu-id="68b77-113">Your redirect URI is hello URL of your application appended with hello path, */.auth/login/microsoftaccount/callback*.</span></span> <span data-ttu-id="68b77-114">例如： `https://contoso.azurewebsites.net/.auth/login/microsoftaccount/callback`。</span><span class="sxs-lookup"><span data-stu-id="68b77-114">For example, `https://contoso.azurewebsites.net/.auth/login/microsoftaccount/callback`.</span></span>   
   > <span data-ttu-id="68b77-115">請確定您使用 hello HTTPS 配置。</span><span class="sxs-lookup"><span data-stu-id="68b77-115">Make sure that you are using hello HTTPS scheme.</span></span>
   
7. <span data-ttu-id="68b77-116">在 [應用程式密碼] 下，按一下 [產生新密碼] 。</span><span class="sxs-lookup"><span data-stu-id="68b77-116">Under "Application Secrets," click **Generate New Password**.</span></span> <span data-ttu-id="68b77-117">記下顯示 hello 值。</span><span class="sxs-lookup"><span data-stu-id="68b77-117">Make note of hello value that appears.</span></span> <span data-ttu-id="68b77-118">一旦您離開 hello 頁面，它就不會顯示一次。</span><span class="sxs-lookup"><span data-stu-id="68b77-118">Once you leave hello page, it will not be displayed again.</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="68b77-119">hello 密碼是重要的安全性認證。</span><span class="sxs-lookup"><span data-stu-id="68b77-119">hello password is an important security credential.</span></span> <span data-ttu-id="68b77-120">請勿與任何人共用 hello 密碼或分散在用戶端應用程式中。</span><span class="sxs-lookup"><span data-stu-id="68b77-120">Do not share hello password with anyone or distribute it within a client application.</span></span>

## <span data-ttu-id="68b77-121"><a name="secrets"></a>新增 Microsoft 帳戶資訊 tooyour App Service 應用程式</span><span class="sxs-lookup"><span data-stu-id="68b77-121"><a name="secrets"> </a>Add Microsoft Account information tooyour App Service application</span></span>
1. <span data-ttu-id="68b77-122">在 hello [Azure 入口網站]，瀏覽 tooyour 應用程式，按一下 **設定** > **驗證 / 授權**。</span><span class="sxs-lookup"><span data-stu-id="68b77-122">Back in hello [Azure portal], navigate tooyour application, click **Settings** > **Authentication / Authorization**.</span></span>
2. <span data-ttu-id="68b77-123">如果 hello 驗證 / 授權功能未啟用，請切換它**上**。</span><span class="sxs-lookup"><span data-stu-id="68b77-123">If hello Authentication / Authorization feature is not enabled, switch it **On**.</span></span>
3. <span data-ttu-id="68b77-124">按一下 [Microsoft 帳戶] 。</span><span class="sxs-lookup"><span data-stu-id="68b77-124">Click **Microsoft Account**.</span></span> <span data-ttu-id="68b77-125">貼上您先前，取得 hello 應用程式識別碼和密碼值，並選擇性地啟用應用程式所需的任何範圍。</span><span class="sxs-lookup"><span data-stu-id="68b77-125">Paste in hello Application ID and Password values which you obtained previously, and optionally enable any scopes your application requires.</span></span> <span data-ttu-id="68b77-126">然後按一下 [確定] 。</span><span class="sxs-lookup"><span data-stu-id="68b77-126">Then click **OK**.</span></span>
   
    ![][1]
   
    <span data-ttu-id="68b77-127">根據預設，應用程式服務提供驗證但不會限制授權的存取 tooyour 網站內容和應用程式開發介面。</span><span class="sxs-lookup"><span data-stu-id="68b77-127">By default, App Service provides authentication but does not restrict authorized access tooyour site content and APIs.</span></span> <span data-ttu-id="68b77-128">您必須在應用程式程式碼中授權使用者。</span><span class="sxs-lookup"><span data-stu-id="68b77-128">You must authorize users in your app code.</span></span>
4. <span data-ttu-id="68b77-129">（選擇性） toorestrict 存取 tooyour 網站 tooonly 使用者由 Microsoft 帳戶驗證設定**當要求未經驗證的動作 tootake**太**Microsoft 帳戶**。</span><span class="sxs-lookup"><span data-stu-id="68b77-129">(Optional) toorestrict access tooyour site tooonly users authenticated by Microsoft account, set **Action tootake when request is not authenticated** too**Microsoft Account**.</span></span> <span data-ttu-id="68b77-130">這需要驗證的所有要求，且所有未經驗證的要求會被重新導向 tooMicrosoft 帳戶進行驗證。</span><span class="sxs-lookup"><span data-stu-id="68b77-130">This requires that all requests be authenticated, and all unauthenticated requests are redirected tooMicrosoft account for authentication.</span></span>
5. <span data-ttu-id="68b77-131">按一下 [儲存] 。</span><span class="sxs-lookup"><span data-stu-id="68b77-131">Click **Save**.</span></span>

<span data-ttu-id="68b77-132">現在您已準備好 toouse Microsoft 帳戶進行驗證您的應用程式。</span><span class="sxs-lookup"><span data-stu-id="68b77-132">You are now ready toouse Microsoft Account for authentication in your app.</span></span>

## <span data-ttu-id="68b77-133"><a name="related-content"> </a>相關內容</span><span class="sxs-lookup"><span data-stu-id="68b77-133"><a name="related-content"> </a>Related content</span></span>
[!INCLUDE [app-service-mobile-related-content-get-started-users](../../includes/app-service-mobile-related-content-get-started-users.md)]

<!-- Images. -->

[0]: ./media/app-service-mobile-how-to-configure-microsoft-authentication/app-service-microsoftaccount-redirect.png
[1]: ./media/app-service-mobile-how-to-configure-microsoft-authentication/mobile-app-microsoftaccount-settings.png

<!-- URLs. -->

[我的應用程式]: http://go.microsoft.com/fwlink/p/?LinkId=262039
[Azure 入口網站]: https://portal.azure.com/
