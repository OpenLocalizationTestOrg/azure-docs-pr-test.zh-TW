---
title: "aaaHow tooconfigure Facebook 驗證您的應用程式服務應用程式"
description: "深入了解如何 tooconfigure Facebook 驗證您的應用程式服務應用程式。"
services: app-service
documentationcenter: 
author: mattchenderson
manager: syntaxc4
editor: 
ms.assetid: b6b4f062-fcb4-47b3-b75a-ec4cb51a62fd
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: multiple
ms.topic: article
ms.date: 10/01/2016
ms.author: mahender
ms.openlocfilehash: 53d03445a2ad17de1d2f69f5e770d14385b48ad4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooconfigure-your-app-service-application-toouse-facebook-login"></a><span data-ttu-id="d20fc-103">如何 tooconfigure 您 App Service 應用程式 toouse Facebook 登入</span><span class="sxs-lookup"><span data-stu-id="d20fc-103">How tooconfigure your App Service application toouse Facebook login</span></span>
[!INCLUDE [app-service-mobile-selector-authentication](../../includes/app-service-mobile-selector-authentication.md)]

<span data-ttu-id="d20fc-104">本主題說明如何 tooconfigure Azure App Service toouse Facebook 做為驗證提供者。</span><span class="sxs-lookup"><span data-stu-id="d20fc-104">This topic shows you how tooconfigure Azure App Service toouse Facebook as an authentication provider.</span></span>

<span data-ttu-id="d20fc-105">toocomplete hello 程序，本主題中的，您必須擁有已驗證的電子郵件地址和行動電話號碼的 Facebook 帳戶。</span><span class="sxs-lookup"><span data-stu-id="d20fc-105">toocomplete hello procedure in this topic, you must have a Facebook account that has a verified email address and a mobile phone number.</span></span> <span data-ttu-id="d20fc-106">新的 Facebook 帳戶，toocreate 太移[facebook.com]。</span><span class="sxs-lookup"><span data-stu-id="d20fc-106">toocreate a new Facebook account, go too[facebook.com].</span></span>

## <span data-ttu-id="d20fc-107"><a name="register"> </a>向 Facebook 註冊您的應用程式</span><span class="sxs-lookup"><span data-stu-id="d20fc-107"><a name="register"> </a>Register your application with Facebook</span></span>
1. <span data-ttu-id="d20fc-108">登入 toohello [Azure 入口網站]，並瀏覽 tooyour 應用程式。</span><span class="sxs-lookup"><span data-stu-id="d20fc-108">Log on toohello [Azure portal], and navigate tooyour application.</span></span> <span data-ttu-id="d20fc-109">複製您的 **URL**。</span><span class="sxs-lookup"><span data-stu-id="d20fc-109">Copy your **URL**.</span></span> <span data-ttu-id="d20fc-110">您將使用此 tooconfigure Facebook 應用程式。</span><span class="sxs-lookup"><span data-stu-id="d20fc-110">You will use this tooconfigure your Facebook app.</span></span>
2. <span data-ttu-id="d20fc-111">在另一個瀏覽器視窗中，瀏覽 toohello [Facebook 開發人員]網站，並使用您的 Facebook 登入帳戶的認證。</span><span class="sxs-lookup"><span data-stu-id="d20fc-111">In another browser window, navigate toohello [Facebook Developers] website and sign-in with your Facebook account credentials.</span></span>
3. <span data-ttu-id="d20fc-112">（選擇性）如果您具有尚未註冊，請按一下**應用程式** > **身為開發人員註冊**，然後接受 hello 原則，並遵循 hello 註冊步驟。</span><span class="sxs-lookup"><span data-stu-id="d20fc-112">(Optional) If you have not already registered, click **Apps** > **Register as a Developer**, then accept hello policy and follow hello registration steps.</span></span>
4. <span data-ttu-id="d20fc-113">按一下 [我的應用程式] > [新增應用程式] > [網站] > [略過並建立應用程式識別碼]。</span><span class="sxs-lookup"><span data-stu-id="d20fc-113">Click **My Apps** > **Add a New App** > **Website** > **Skip and Create App ID**.</span></span> 
5. <span data-ttu-id="d20fc-114">在**顯示名稱**，輸入您的應用程式類型的唯一名稱您**Contact Email**，選擇**類別**應用程式，然後按一下**建立應用程式識別碼**並完成 hello 安全性檢查。</span><span class="sxs-lookup"><span data-stu-id="d20fc-114">In **Display Name**, type a unique name for your app, type your **Contact Email**, choose a **Category** for your app, then click **Create App ID** and complete hello security check.</span></span> <span data-ttu-id="d20fc-115">這會帶您 toohello 新的 Facebook 應用程式的開發人員儀表板。</span><span class="sxs-lookup"><span data-stu-id="d20fc-115">This takes you toohello developer dashboard for your new Facebook app.</span></span>
6. <span data-ttu-id="d20fc-116">在 [Facebook 登入] 下，按一下 [開始使用]。</span><span class="sxs-lookup"><span data-stu-id="d20fc-116">Under "Facebook Login," click **Get Started**.</span></span> <span data-ttu-id="d20fc-117">新增您的應用程式**重新導向 URI**太**有效的 OAuth 重新導向 Uri**，然後按一下 **儲存變更**。</span><span class="sxs-lookup"><span data-stu-id="d20fc-117">Add your application's **Redirect URI** too**Valid OAuth redirect URIs**, then click **Save Changes**.</span></span> 
   
   > [!NOTE]
   > <span data-ttu-id="d20fc-118">您重新導向 URI 是應用程式加上 hello 路徑 hello URL */.auth/login/facebook/callback*。</span><span class="sxs-lookup"><span data-stu-id="d20fc-118">Your redirect URI is hello URL of your application appended with hello path, */.auth/login/facebook/callback*.</span></span> <span data-ttu-id="d20fc-119">例如： `https://contoso.azurewebsites.net/.auth/login/facebook/callback`。</span><span class="sxs-lookup"><span data-stu-id="d20fc-119">For example, `https://contoso.azurewebsites.net/.auth/login/facebook/callback`.</span></span> <span data-ttu-id="d20fc-120">請確定您使用 hello HTTPS 配置。</span><span class="sxs-lookup"><span data-stu-id="d20fc-120">Make sure that you are using hello HTTPS scheme.</span></span>
   > 
   > 
7. <span data-ttu-id="d20fc-121">在 hello 左側導覽中，按一下 **設定**。</span><span class="sxs-lookup"><span data-stu-id="d20fc-121">In hello left-hand navigation, click **Settings**.</span></span> <span data-ttu-id="d20fc-122">在 hello**應用程式秘鑰**欄位中，按一下**顯示**，提供您的密碼，如果要求，然後記下的 hello 值**應用程式識別碼**和**應用程式秘鑰**.</span><span class="sxs-lookup"><span data-stu-id="d20fc-122">On hello **App Secret** field, click **Show**, provide your password if requested, then make a note of hello values of **App ID** and **App Secret**.</span></span> <span data-ttu-id="d20fc-123">您使用這些更新 tooconfigure 您的應用程式在 Azure 中。</span><span class="sxs-lookup"><span data-stu-id="d20fc-123">You use these later tooconfigure your application in Azure.</span></span>
   
   > [!IMPORTANT]
   > <span data-ttu-id="d20fc-124">hello 應用程式密碼是重要的安全性認證。</span><span class="sxs-lookup"><span data-stu-id="d20fc-124">hello app secret is an important security credential.</span></span> <span data-ttu-id="d20fc-125">請勿與任何人共用此密碼，或在用戶端應用程式中加以散發。</span><span class="sxs-lookup"><span data-stu-id="d20fc-125">Do not share this secret with anyone or distribute it within a client application.</span></span>
   > 
   > 
8. <span data-ttu-id="d20fc-126">hello 已使用的 tooregister hello 應用程式的 Facebook 帳戶是 hello 應用程式的系統管理員。</span><span class="sxs-lookup"><span data-stu-id="d20fc-126">hello Facebook account which was used tooregister hello application is an administrator of hello app.</span></span> <span data-ttu-id="d20fc-127">此時，只有系統管理員可以登入此應用程式。</span><span class="sxs-lookup"><span data-stu-id="d20fc-127">At this point, only administrators can sign into this application.</span></span> <span data-ttu-id="d20fc-128">tooauthenticate 其他 Facebook 帳戶，按一下**應用程式檢閱**並啟用**< 您的應用程式名稱 > 請公用**tooenable 使用 Facebook 驗證一般公用存取。</span><span class="sxs-lookup"><span data-stu-id="d20fc-128">tooauthenticate other Facebook accounts, click **App Review** and enable **Make <your-app-name> public** tooenable general public access using Facebook authentication.</span></span>

## <span data-ttu-id="d20fc-129"><a name="secrets"></a>新增 Facebook 資訊 tooyour 應用程式</span><span class="sxs-lookup"><span data-stu-id="d20fc-129"><a name="secrets"> </a>Add Facebook information tooyour application</span></span>
1. <span data-ttu-id="d20fc-130">在 hello [Azure 入口網站]，瀏覽 tooyour 應用程式。</span><span class="sxs-lookup"><span data-stu-id="d20fc-130">Back in hello [Azure portal], navigate tooyour application.</span></span> <span data-ttu-id="d20fc-131">按一下 [設定] > [驗證/授權]，並確定 [App Service 驗證] 為 [開啟]。</span><span class="sxs-lookup"><span data-stu-id="d20fc-131">Click **Settings** > **Authentication / Authorization**, and make sure that **App Service Authentication** is **On**.</span></span>
2. <span data-ttu-id="d20fc-132">按一下**Facebook**，貼上您先前取得 hello 應用程式識別碼和應用程式密碼值，選擇性地啟用應用程式所需的任何範圍然後按一下**確定**。</span><span class="sxs-lookup"><span data-stu-id="d20fc-132">Click **Facebook**, paste in hello App ID and App Secret values which you obtained previously, optionally enable any scopes needed by your application, then click **OK**.</span></span>
   
    ![][0]
   
    <span data-ttu-id="d20fc-133">根據預設，應用程式服務提供驗證但不會限制授權的存取 tooyour 網站內容和應用程式開發介面。</span><span class="sxs-lookup"><span data-stu-id="d20fc-133">By default, App Service provides authentication but does not restrict authorized access tooyour site content and APIs.</span></span> <span data-ttu-id="d20fc-134">您必須在應用程式程式碼中授權使用者。</span><span class="sxs-lookup"><span data-stu-id="d20fc-134">You must authorize users in your app code.</span></span>
3. <span data-ttu-id="d20fc-135">（選擇性） toorestrict 存取 tooyour 網站 tooonly 使用者驗證 Facebook、 設定**當要求未經驗證的動作 tootake**太**Facebook**。</span><span class="sxs-lookup"><span data-stu-id="d20fc-135">(Optional) toorestrict access tooyour site tooonly users authenticated by Facebook, set **Action tootake when request is not authenticated** too**Facebook**.</span></span> <span data-ttu-id="d20fc-136">這需要驗證的所有要求，而所有未經驗證的要求重新導向的 tooFacebook 進行驗證。</span><span class="sxs-lookup"><span data-stu-id="d20fc-136">This requires that all requests be authenticated, and all unauthenticated requests are redirected tooFacebook for authentication.</span></span>
4. <span data-ttu-id="d20fc-137">設定驗證完成時，按一下 [儲存] 。</span><span class="sxs-lookup"><span data-stu-id="d20fc-137">When done configuring authentication, click **Save**.</span></span>

<span data-ttu-id="d20fc-138">現在您已準備好 toouse Facebook 驗證您的應用程式。</span><span class="sxs-lookup"><span data-stu-id="d20fc-138">You are now ready toouse Facebook for authentication in your app.</span></span>

## <span data-ttu-id="d20fc-139"><a name="related-content"> </a>相關內容</span><span class="sxs-lookup"><span data-stu-id="d20fc-139"><a name="related-content"> </a>Related Content</span></span>
[!INCLUDE [app-service-mobile-related-content-get-started-users](../../includes/app-service-mobile-related-content-get-started-users.md)]

<!-- Images. -->
[0]: ./media/app-service-mobile-how-to-configure-facebook-authentication/mobile-app-facebook-settings.png

<!-- URLs. -->
[Facebook 開發人員]: http://go.microsoft.com/fwlink/p/?LinkId=268286
[facebook.com]: http://go.microsoft.com/fwlink/p/?LinkId=268285
[Get started with authentication]: /en-us/develop/mobile/tutorials/get-started-with-users-dotnet/
[Azure 入口網站]: https://portal.azure.com/
