---
title: "aaaPublish 原生用戶端應用程式的 Azure AD |Microsoft 文件"
description: "涵蓋如何與 Azure AD 應用程式 Proxy 連接器 tooprovide 安全遠端存取 tooyour tooenable 原生用戶端應用程式 toocommunicate 內部部署應用程式。"
services: active-directory
documentationcenter: 
author: kgremban
manager: femila
ms.assetid: f0cae145-e346-4126-948f-3f699747b96e
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/17/2017
ms.author: kgremban
ms.reviewer: harshja
ms.custom: it-pro
ms.openlocfilehash: 0ed2be217bf992f034d8321d5e66569b4cace24f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooenable-native-client-apps-toointeract-with-proxy-applications"></a><span data-ttu-id="399c7-103">如何使用應用程式 proxy tooenable 原生用戶端應用程式 toointeract</span><span class="sxs-lookup"><span data-stu-id="399c7-103">How tooenable native client apps toointeract with proxy Applications</span></span>

<span data-ttu-id="399c7-104">加法 tooweb 應用程式中，Azure Active Directory 應用程式 Proxy 也可以使用的 toopublish 原生用戶端應用程式。</span><span class="sxs-lookup"><span data-stu-id="399c7-104">In addition tooweb applications, Azure Active Directory Application Proxy can also be used toopublish native client apps.</span></span> <span data-ttu-id="399c7-105">原生用戶端應用程式與 Web 應用程式不同，因為這種應用程式會安裝在裝置上，而 Web 應用程式則是透過瀏覽器存取。</span><span class="sxs-lookup"><span data-stu-id="399c7-105">Native client apps differ from web apps because they are installed on a device, while web apps are accessed through a browser.</span></span> 

<span data-ttu-id="399c7-106">應用程式 Proxy 藉由接受在標準授權 HTTP 標頭中傳送的 Azure AD 發行權杖，來支援原生用戶端應用程式。</span><span class="sxs-lookup"><span data-stu-id="399c7-106">Application Proxy supports native client apps by accepting Azure AD issued tokens that are sent in standard Authorize HTTP headers.</span></span>

![使用者、Azure Active Directory 和已發佈應用程式之間的關係](./media/active-directory-application-proxy-native-client/richclientflow.png)

<span data-ttu-id="399c7-108">使用 hello Azure AD 驗證程式庫，它會負責驗證並支援許多用戶端環境、 toopublish 原生應用程式。</span><span class="sxs-lookup"><span data-stu-id="399c7-108">Use hello Azure AD Authentication Library, which takes care of authentication and supports many client environments, toopublish native applications.</span></span> <span data-ttu-id="399c7-109">應用程式 Proxy 納入 hello [tooWeb API 的原生應用程式案例](develop/active-directory-authentication-scenarios.md#native-application-to-web-api)。</span><span class="sxs-lookup"><span data-stu-id="399c7-109">Application Proxy fits into hello [Native Application tooWeb API scenario](develop/active-directory-authentication-scenarios.md#native-application-to-web-api).</span></span> <span data-ttu-id="399c7-110">這篇文章會引導您 hello 四個步驟 toopublish hello Azure AD 驗證程式庫與應用程式 Proxy 的原生應用程式。</span><span class="sxs-lookup"><span data-stu-id="399c7-110">This article walks you through hello four steps toopublish a native application with Application Proxy and hello Azure AD Authentication Library.</span></span> 

## <a name="step-1-publish-your-application"></a><span data-ttu-id="399c7-111">步驟 1：發佈您的應用程式</span><span class="sxs-lookup"><span data-stu-id="399c7-111">Step 1: Publish your application</span></span>
<span data-ttu-id="399c7-112">發行應用程式 proxy，如同任何其他應用程式，並指派使用者 tooaccess 您的應用程式。</span><span class="sxs-lookup"><span data-stu-id="399c7-112">Publish your proxy application as you would any other application and assign users tooaccess your application.</span></span> <span data-ttu-id="399c7-113">如需詳細資訊，請參閱[使用應用程式 Proxy 發佈應用程式](active-directory-application-proxy-publish.md)。</span><span class="sxs-lookup"><span data-stu-id="399c7-113">For more information, see [Publish applications with Application Proxy](active-directory-application-proxy-publish.md).</span></span>

## <a name="step-2-configure-your-application"></a><span data-ttu-id="399c7-114">步驟 2：設定您的應用程式</span><span class="sxs-lookup"><span data-stu-id="399c7-114">Step 2: Configure your application</span></span>
<span data-ttu-id="399c7-115">以下列方式設定原生應用程式：</span><span class="sxs-lookup"><span data-stu-id="399c7-115">Configure your native application as follows:</span></span>

1. <span data-ttu-id="399c7-116">登入 toohello [Azure 入口網站](https://portal.azure.com)。</span><span class="sxs-lookup"><span data-stu-id="399c7-116">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="399c7-117">瀏覽過**Azure Active Directory** > **應用程式註冊**。</span><span class="sxs-lookup"><span data-stu-id="399c7-117">Navigate too**Azure Active Directory** > **App registrations**.</span></span>
3. <span data-ttu-id="399c7-118">選取 [新增應用程式註冊]。</span><span class="sxs-lookup"><span data-stu-id="399c7-118">Select **New application registration**.</span></span>
4. <span data-ttu-id="399c7-119">指定應用程式的名稱，選取**原生**hello 應用程式類型，並提供您的應用程式中的 hello 重新導向 URI。</span><span class="sxs-lookup"><span data-stu-id="399c7-119">Specify a name for your application, select **Native** as hello application type, and provide hello Redirect URI for your application.</span></span> 

   ![建立新的應用程式註冊](./media/active-directory-application-proxy-native-client/create.png)
5. <span data-ttu-id="399c7-121">選取 [ **建立**]。</span><span class="sxs-lookup"><span data-stu-id="399c7-121">Select **Create**.</span></span>

<span data-ttu-id="399c7-122">如需建立新應用程式註冊的詳細資訊，請參閱[整合應用程式與 Azure Active Directory](.//develop/active-directory-integrating-applications.md)。</span><span class="sxs-lookup"><span data-stu-id="399c7-122">For more detailed information about creating a new app registration, see [Integrating applications with Azure Active Directory](.//develop/active-directory-integrating-applications.md).</span></span>


## <a name="step-3-grant-access-tooother-applications"></a><span data-ttu-id="399c7-123">步驟 3： 授與存取 tooother 應用程式</span><span class="sxs-lookup"><span data-stu-id="399c7-123">Step 3: Grant access tooother applications</span></span>
<span data-ttu-id="399c7-124">啟用 hello 原生應用程式公開的 toobe tooother 應用程式目錄中：</span><span class="sxs-lookup"><span data-stu-id="399c7-124">Enable hello native application toobe exposed tooother applications in your directory:</span></span>

1. <span data-ttu-id="399c7-125">仍在**應用程式註冊**，選取 hello 您剛才建立的新原生應用程式。</span><span class="sxs-lookup"><span data-stu-id="399c7-125">Still in **App registrations**, select hello new native application that you just created.</span></span>
2. <span data-ttu-id="399c7-126">選取 [必要權限]。</span><span class="sxs-lookup"><span data-stu-id="399c7-126">Select **Required permissions**.</span></span>
3. <span data-ttu-id="399c7-127">選取 [新增] 。</span><span class="sxs-lookup"><span data-stu-id="399c7-127">Select **Add**.</span></span>
4. <span data-ttu-id="399c7-128">開啟 hello 第一個步驟中，**選取應用程式開發介面**。</span><span class="sxs-lookup"><span data-stu-id="399c7-128">Open hello first step, **Select an API**.</span></span>
5. <span data-ttu-id="399c7-129">使用 hello 搜尋列 toofind hello 應用程式 Proxy 應用程式發佈 hello 第一個區段中。</span><span class="sxs-lookup"><span data-stu-id="399c7-129">Use hello search bar toofind hello Application Proxy app that you published in hello first section.</span></span> <span data-ttu-id="399c7-130">選擇該應用程式，然後按一下 [選取]。</span><span class="sxs-lookup"><span data-stu-id="399c7-130">Choose that app, then click **Select**.</span></span> 

   ![搜尋 hello proxy 應用程式](./media/active-directory-application-proxy-native-client/select_api.png)
6. <span data-ttu-id="399c7-132">開啟 hello 第二個步驟中，**選取權限**。</span><span class="sxs-lookup"><span data-stu-id="399c7-132">Open hello second step, **Select permissions**.</span></span>
7. <span data-ttu-id="399c7-133">使用 hello 核取方塊 toogrant 原生應用程式存取 tooyour proxy 應用程式，然後按一下**選取**。</span><span class="sxs-lookup"><span data-stu-id="399c7-133">Use hello checkbox toogrant your native application access tooyour proxy application, then click **Select**.</span></span>

   ![授與存取 tooproxy 應用程式](./media/active-directory-application-proxy-native-client/select_perms.png)
8. <span data-ttu-id="399c7-135">選取 [完成] 。</span><span class="sxs-lookup"><span data-stu-id="399c7-135">Select **Done**.</span></span>


## <a name="step-4-edit-hello-active-directory-authentication-library"></a><span data-ttu-id="399c7-136">步驟 4： 編輯 hello Active Directory Authentication Library</span><span class="sxs-lookup"><span data-stu-id="399c7-136">Step 4: Edit hello Active Directory Authentication Library</span></span>
<span data-ttu-id="399c7-137">編輯下列文字的 hello Active Directory 驗證程式庫 (ADAL) tooinclude hello hello 驗證內容中的 hello 原生應用程式程式碼：</span><span class="sxs-lookup"><span data-stu-id="399c7-137">Edit hello native application code in hello authentication context of hello Active Directory Authentication Library (ADAL) tooinclude hello following text:</span></span>

```
// Acquire Access Token from AAD for Proxy Application
AuthenticationContext authContext = new AuthenticationContext("https://login.microsoftonline.com/<Tenant ID>");
AuthenticationResult result = authContext.AcquireToken("< External Url of Proxy App >",
        "<App ID of hello Native app>",
        new Uri("<Redirect Uri of hello Native App>"),
        PromptBehavior.Never);

//Use hello Access Token tooaccess hello Proxy Application
HttpClient httpClient = new HttpClient();
httpClient.DefaultRequestHeaders.Authorization = new AuthenticationHeaderValue("Bearer", result.AccessToken);
HttpResponseMessage response = await httpClient.GetAsync("< Proxy App API Url >");
```

<span data-ttu-id="399c7-138">hello 變數 hello 範例程式碼中的應該被取代，如下所示：</span><span class="sxs-lookup"><span data-stu-id="399c7-138">hello variables in hello sample code should be replaced as follows:</span></span>

* <span data-ttu-id="399c7-139">**租用戶識別碼**可以在 hello Azure 入口網站中找到。</span><span class="sxs-lookup"><span data-stu-id="399c7-139">**Tenant ID** can be found in hello Azure portal.</span></span> <span data-ttu-id="399c7-140">瀏覽過**Azure Active Directory** > **屬性**和複製 hello 目錄識別碼。</span><span class="sxs-lookup"><span data-stu-id="399c7-140">Navigate too**Azure Active Directory** > **Properties** and copy hello Directory ID.</span></span> 
* <span data-ttu-id="399c7-141">**外部 URL**是 hello 前端在 hello Proxy 應用程式中所輸入的 URL。</span><span class="sxs-lookup"><span data-stu-id="399c7-141">**External URL** is hello front-end URL you entered in hello Proxy Application.</span></span> <span data-ttu-id="399c7-142">這個值 toofind，瀏覽 toohello**應用程式 proxy** hello proxy 應用程式的區段。</span><span class="sxs-lookup"><span data-stu-id="399c7-142">toofind this value, navigate toohello **Application proxy** section of hello proxy app.</span></span>
* <span data-ttu-id="399c7-143">**應用程式識別碼**hello 的原生應用程式可以找到上 hello**屬性**hello 原生應用程式頁面。</span><span class="sxs-lookup"><span data-stu-id="399c7-143">**App ID** of hello native app can be found on hello **Properties** page of hello native application.</span></span>
* <span data-ttu-id="399c7-144">**重新導向的 hello 原生應用程式 URI**可以找到上 hello**重新導向 Uri** hello 原生應用程式頁面。</span><span class="sxs-lookup"><span data-stu-id="399c7-144">**Redirect URI of hello native app** can be found on hello **Redirect URIs** page of hello native application.</span></span>


## <a name="see-also"></a><span data-ttu-id="399c7-145">另請參閱</span><span class="sxs-lookup"><span data-stu-id="399c7-145">See also</span></span>

<span data-ttu-id="399c7-146">如需 hello 原生應用程式流程的詳細資訊，請參閱[原生應用程式 tooweb 應用程式開發介面](develop/active-directory-authentication-scenarios.md#native-application-to-web-api)</span><span class="sxs-lookup"><span data-stu-id="399c7-146">For more information about hello native application flow, see [Native application tooweb API](develop/active-directory-authentication-scenarios.md#native-application-to-web-api)</span></span>

<span data-ttu-id="399c7-147">如 hello 最新消息和更新，請參閱 hello[應用程式 Proxy 部落格](http://blogs.technet.com/b/applicationproxyblog/)</span><span class="sxs-lookup"><span data-stu-id="399c7-147">For hello latest news and updates, check out hello [Application Proxy blog](http://blogs.technet.com/b/applicationproxyblog/)</span></span>
