---
title: "aaaHow tooconfigure Google 驗證您的應用程式服務應用程式"
description: "深入了解如何 tooconfigure Google 驗證您的應用程式服務應用程式。"
services: app-service
documentationcenter: 
author: mattchenderson
manager: syntaxc4
editor: 
ms.assetid: 2b2f9abf-9120-4aac-ac5b-4a268d9b6e2b
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: multiple
ms.topic: article
ms.date: 10/01/2016
ms.author: mahender
ms.openlocfilehash: 9175c40b78c859e9e191504c41cd0bb9a3380ccd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooconfigure-your-app-service-application-toouse-google-login"></a><span data-ttu-id="5e1b2-103">如何 tooconfigure 您 App Service 應用程式 toouse Google 登入</span><span class="sxs-lookup"><span data-stu-id="5e1b2-103">How tooconfigure your App Service application toouse Google login</span></span>
[!INCLUDE [app-service-mobile-selector-authentication](../../includes/app-service-mobile-selector-authentication.md)]

<span data-ttu-id="5e1b2-104">本主題說明如何 tooconfigure Azure App Service toouse Google 作為驗證提供者。</span><span class="sxs-lookup"><span data-stu-id="5e1b2-104">This topic shows you how tooconfigure Azure App Service toouse Google as an authentication provider.</span></span>

<span data-ttu-id="5e1b2-105">toocomplete hello 程序，本主題中的，您必須具有 已驗證的電子郵件地址的 Google 帳戶。</span><span class="sxs-lookup"><span data-stu-id="5e1b2-105">toocomplete hello procedure in this topic, you must have a Google account that has a verified email address.</span></span> <span data-ttu-id="5e1b2-106">toocreate 新 Google 帳戶，跳過[accounts.google.com](http://go.microsoft.com/fwlink/p/?LinkId=268302)。</span><span class="sxs-lookup"><span data-stu-id="5e1b2-106">toocreate a new Google account, go too[accounts.google.com](http://go.microsoft.com/fwlink/p/?LinkId=268302).</span></span>

## <span data-ttu-id="5e1b2-107"><a name="register"> </a>向 Google 註冊您的應用程式</span><span class="sxs-lookup"><span data-stu-id="5e1b2-107"><a name="register"> </a>Register your application with Google</span></span>
1. <span data-ttu-id="5e1b2-108">登入 toohello [Azure 入口網站]，並瀏覽 tooyour 應用程式。</span><span class="sxs-lookup"><span data-stu-id="5e1b2-108">Log on toohello [Azure portal], and navigate tooyour application.</span></span> <span data-ttu-id="5e1b2-109">複製您**URL**，而您使用稍後 tooconfigure Google 應用程式。</span><span class="sxs-lookup"><span data-stu-id="5e1b2-109">Copy your **URL**, which you use later tooconfigure your Google app.</span></span>
2. <span data-ttu-id="5e1b2-110">瀏覽 toohello [Google apis](http://go.microsoft.com/fwlink/p/?LinkId=268303)網站，使用您的 Google 帳戶認證登入。 按一下**建立專案**，提供**專案名稱**，然後按一下  **建立**。</span><span class="sxs-lookup"><span data-stu-id="5e1b2-110">Navigate toohello [Google apis](http://go.microsoft.com/fwlink/p/?LinkId=268303) website, sign in with your Google account credentials, click **Create Project**, provide a **Project name**, then click **Create**.</span></span>
3. <span data-ttu-id="5e1b2-111">在 [社交平台類 API] 下，按一下 [Google + API]，然後按一下 [啟用]。</span><span class="sxs-lookup"><span data-stu-id="5e1b2-111">Under **Social APIs** click **Google+ API** and then **Enable**.</span></span>
4. <span data-ttu-id="5e1b2-112">在左瀏覽，hello**認證** > **OAuth 同意畫面**，然後選取您**電子郵件地址**，輸入**產品名稱**，然後按一下**儲存**。</span><span class="sxs-lookup"><span data-stu-id="5e1b2-112">In hello left navigation, **Credentials** > **OAuth consent screen**, then select your **Email address**,  enter a **Product Name**, and click **Save**.</span></span>
5. <span data-ttu-id="5e1b2-113">在 hello**認證**索引標籤上，按一下 **建立認證** > **OAuth 用戶端識別碼**，然後選取**Web 應用程式**。</span><span class="sxs-lookup"><span data-stu-id="5e1b2-113">In hello **Credentials** tab, click **Create credentials** > **OAuth client ID**, then select **Web application**.</span></span>
6. <span data-ttu-id="5e1b2-114">貼上 hello App Service **URL**您先前複製到**授權 JavaScript Origins**，然後貼上您重新導向 URI 切割**授權重新導向 URI**。</span><span class="sxs-lookup"><span data-stu-id="5e1b2-114">Paste hello App Service **URL** you copied earlier into **Authorized JavaScript Origins**, then paste your redirect URI into **Authorized Redirect URI**.</span></span> <span data-ttu-id="5e1b2-115">hello 重新導向 URI 是應用程式加上 hello 路徑 hello URL */.auth/login/google/callback*。</span><span class="sxs-lookup"><span data-stu-id="5e1b2-115">hello redirect URI is hello URL of your application appended with hello path, */.auth/login/google/callback*.</span></span> <span data-ttu-id="5e1b2-116">例如： `https://contoso.azurewebsites.net/.auth/login/google/callback`。</span><span class="sxs-lookup"><span data-stu-id="5e1b2-116">For example, `https://contoso.azurewebsites.net/.auth/login/google/callback`.</span></span> <span data-ttu-id="5e1b2-117">請確定您使用 hello HTTPS 配置。</span><span class="sxs-lookup"><span data-stu-id="5e1b2-117">Make sure that you are using hello HTTPS scheme.</span></span> <span data-ttu-id="5e1b2-118">然後按一下 [ **建立**]。</span><span class="sxs-lookup"><span data-stu-id="5e1b2-118">Then click **Create**.</span></span>
7. <span data-ttu-id="5e1b2-119">Hello 下一個畫面中，記下的 hello 值 hello 用戶端識別碼和用戶端密碼。</span><span class="sxs-lookup"><span data-stu-id="5e1b2-119">On hello next screen, make a note of hello values of hello client ID and client secret.</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="5e1b2-120">hello 用戶端機密是重要的安全性認證。</span><span class="sxs-lookup"><span data-stu-id="5e1b2-120">hello client secret is an important security credential.</span></span> <span data-ttu-id="5e1b2-121">請勿與任何人共用此密碼，或在用戶端應用程式中加以散發。</span><span class="sxs-lookup"><span data-stu-id="5e1b2-121">Do not share this secret with anyone or distribute it within a client application.</span></span>


## <span data-ttu-id="5e1b2-122"><a name="secrets"></a>新增 Google 資訊 tooyour 應用程式</span><span class="sxs-lookup"><span data-stu-id="5e1b2-122"><a name="secrets"> </a>Add Google information tooyour application</span></span>
1. <span data-ttu-id="5e1b2-123">在 hello [Azure 入口網站]，瀏覽 tooyour 應用程式。</span><span class="sxs-lookup"><span data-stu-id="5e1b2-123">Back in hello [Azure portal], navigate tooyour application.</span></span> <span data-ttu-id="5e1b2-124">依序按一下 [設定] 及 [驗證/授權]。</span><span class="sxs-lookup"><span data-stu-id="5e1b2-124">Click **Settings**, and then **Authentication / Authorization**.</span></span>
2. <span data-ttu-id="5e1b2-125">如果 hello 驗證 / 授權功能未啟用，請開啟 hello 參數太**上**。</span><span class="sxs-lookup"><span data-stu-id="5e1b2-125">If hello Authentication / Authorization feature is not enabled, turn hello switch too**On**.</span></span>
3. <span data-ttu-id="5e1b2-126">按一下 [Google] 。</span><span class="sxs-lookup"><span data-stu-id="5e1b2-126">Click **Google**.</span></span> <span data-ttu-id="5e1b2-127">貼上您先前，取得 hello 應用程式識別碼和應用程式密碼值，並選擇性地啟用應用程式所需的任何範圍。</span><span class="sxs-lookup"><span data-stu-id="5e1b2-127">Paste in hello App ID and App Secret values which you obtained previously, and optionally enable any scopes your application requires.</span></span> <span data-ttu-id="5e1b2-128">然後按一下 [確定] 。</span><span class="sxs-lookup"><span data-stu-id="5e1b2-128">Then click **OK**.</span></span>
   
   ![][1]
   
   <span data-ttu-id="5e1b2-129">根據預設，應用程式服務提供驗證但不會限制授權的存取 tooyour 網站內容和應用程式開發介面。</span><span class="sxs-lookup"><span data-stu-id="5e1b2-129">By default, App Service provides authentication but does not restrict authorized access tooyour site content and APIs.</span></span> <span data-ttu-id="5e1b2-130">您必須在應用程式程式碼中授權使用者。</span><span class="sxs-lookup"><span data-stu-id="5e1b2-130">You must authorize users in your app code.</span></span>
4. <span data-ttu-id="5e1b2-131">（選擇性） toorestrict 存取 tooyour 網站 tooonly 使用者經過 Google、 設定**當要求未經驗證的動作 tootake**太**Google**。</span><span class="sxs-lookup"><span data-stu-id="5e1b2-131">(Optional) toorestrict access tooyour site tooonly users authenticated by Google, set **Action tootake when request is not authenticated** too**Google**.</span></span> <span data-ttu-id="5e1b2-132">這需要驗證的所有要求，而所有未經驗證的要求重新導向的 tooGoogle 進行驗證。</span><span class="sxs-lookup"><span data-stu-id="5e1b2-132">This requires that all requests be authenticated, and all unauthenticated requests are redirected tooGoogle for authentication.</span></span>
5. <span data-ttu-id="5e1b2-133">按一下 [儲存] 。</span><span class="sxs-lookup"><span data-stu-id="5e1b2-133">Click **Save**.</span></span>

<span data-ttu-id="5e1b2-134">現在您已準備好 toouse Google 驗證您的應用程式。</span><span class="sxs-lookup"><span data-stu-id="5e1b2-134">You are now ready toouse Google for authentication in your app.</span></span>

## <span data-ttu-id="5e1b2-135"><a name="related-content"> </a>相關內容</span><span class="sxs-lookup"><span data-stu-id="5e1b2-135"><a name="related-content"> </a>Related Content</span></span>
[!INCLUDE [app-service-mobile-related-content-get-started-users](../../includes/app-service-mobile-related-content-get-started-users.md)]

<!-- Anchors. -->

<!-- Images. -->

[0]: ./media/app-service-mobile-how-to-configure-google-authentication/mobile-app-google-redirect.png
[1]: ./media/app-service-mobile-how-to-configure-google-authentication/mobile-app-google-settings.png

<!-- URLs. -->

[Google apis]: http://go.microsoft.com/fwlink/p/?LinkId=268303

[Azure 入口網站]: https://portal.azure.com/

