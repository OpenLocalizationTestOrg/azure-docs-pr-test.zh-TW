---
title: "發佈原生用戶端應用程式 - Azure AD | Microsoft Docs"
description: "涵蓋如何讓原生用戶端應用程式與 Azure AD 應用程式 Proxy 連接器通訊，為內部部署的應用程式提供安全的遠端存取。"
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
ms.openlocfilehash: bdaa5af6ff5331bc310499586615b48a864c3c5e
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="how-to-enable-native-client-apps-to-interact-with-proxy-applications"></a><span data-ttu-id="9d382-103">如何讓原生用戶端應用程式與 Proxy 應用程式互動</span><span class="sxs-lookup"><span data-stu-id="9d382-103">How to enable native client apps to interact with proxy Applications</span></span>

<span data-ttu-id="9d382-104">除了 Web 應用程式，Azure Active Directory 應用程式 Proxy 也可以用來發佈原生用戶端應用程式。</span><span class="sxs-lookup"><span data-stu-id="9d382-104">In addition to web applications, Azure Active Directory Application Proxy can also be used to publish native client apps.</span></span> <span data-ttu-id="9d382-105">原生用戶端應用程式與 Web 應用程式不同，因為這種應用程式會安裝在裝置上，而 Web 應用程式則是透過瀏覽器存取。</span><span class="sxs-lookup"><span data-stu-id="9d382-105">Native client apps differ from web apps because they are installed on a device, while web apps are accessed through a browser.</span></span> 

<span data-ttu-id="9d382-106">應用程式 Proxy 藉由接受在標準授權 HTTP 標頭中傳送的 Azure AD 發行權杖，來支援原生用戶端應用程式。</span><span class="sxs-lookup"><span data-stu-id="9d382-106">Application Proxy supports native client apps by accepting Azure AD issued tokens that are sent in standard Authorize HTTP headers.</span></span>

![使用者、Azure Active Directory 和已發佈應用程式之間的關係](./media/active-directory-application-proxy-native-client/richclientflow.png)

<span data-ttu-id="9d382-108">請使用 Azure AD 驗證程式庫來發佈原生應用程式，該程式庫會處理驗證並支援許多用戶端環境。</span><span class="sxs-lookup"><span data-stu-id="9d382-108">Use the Azure AD Authentication Library, which takes care of authentication and supports many client environments, to publish native applications.</span></span> <span data-ttu-id="9d382-109">應用程式 Proxy 融入 [原生應用程式到 Web API 案例](develop/active-directory-authentication-scenarios.md#native-application-to-web-api)。</span><span class="sxs-lookup"><span data-stu-id="9d382-109">Application Proxy fits into the [Native Application to Web API scenario](develop/active-directory-authentication-scenarios.md#native-application-to-web-api).</span></span> <span data-ttu-id="9d382-110">本文引導您完成使用應用程式 Proxy 和 Azure AD 驗證程式庫發佈原生應用程式的四個步驟。</span><span class="sxs-lookup"><span data-stu-id="9d382-110">This article walks you through the four steps to publish a native application with Application Proxy and the Azure AD Authentication Library.</span></span> 

## <a name="step-1-publish-your-application"></a><span data-ttu-id="9d382-111">步驟 1：發佈您的應用程式</span><span class="sxs-lookup"><span data-stu-id="9d382-111">Step 1: Publish your application</span></span>
<span data-ttu-id="9d382-112">如同任何其他應用程式一般，發佈您的 Proxy 應用程式，並指派使用者以存取您的應用程式。</span><span class="sxs-lookup"><span data-stu-id="9d382-112">Publish your proxy application as you would any other application and assign users to access your application.</span></span> <span data-ttu-id="9d382-113">如需詳細資訊，請參閱[使用應用程式 Proxy 發佈應用程式](active-directory-application-proxy-publish.md)。</span><span class="sxs-lookup"><span data-stu-id="9d382-113">For more information, see [Publish applications with Application Proxy](active-directory-application-proxy-publish.md).</span></span>

## <a name="step-2-configure-your-application"></a><span data-ttu-id="9d382-114">步驟 2：設定您的應用程式</span><span class="sxs-lookup"><span data-stu-id="9d382-114">Step 2: Configure your application</span></span>
<span data-ttu-id="9d382-115">以下列方式設定原生應用程式：</span><span class="sxs-lookup"><span data-stu-id="9d382-115">Configure your native application as follows:</span></span>

1. <span data-ttu-id="9d382-116">登入 [Azure 入口網站](https://portal.azure.com)。</span><span class="sxs-lookup"><span data-stu-id="9d382-116">Sign in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="9d382-117">巡覽至 [Azure Active Directory] > [應用程式註冊]。</span><span class="sxs-lookup"><span data-stu-id="9d382-117">Navigate to **Azure Active Directory** > **App registrations**.</span></span>
3. <span data-ttu-id="9d382-118">選取 [新增應用程式註冊]。</span><span class="sxs-lookup"><span data-stu-id="9d382-118">Select **New application registration**.</span></span>
4. <span data-ttu-id="9d382-119">指定應用程式的名稱，選取 [原生] 作為應用程式類型，並提供應用程式的重新導向 URI。</span><span class="sxs-lookup"><span data-stu-id="9d382-119">Specify a name for your application, select **Native** as the application type, and provide the Redirect URI for your application.</span></span> 

   ![建立新的應用程式註冊](./media/active-directory-application-proxy-native-client/create.png)
5. <span data-ttu-id="9d382-121">選取 [ **建立**]。</span><span class="sxs-lookup"><span data-stu-id="9d382-121">Select **Create**.</span></span>

<span data-ttu-id="9d382-122">如需建立新應用程式註冊的詳細資訊，請參閱[整合應用程式與 Azure Active Directory](.//develop/active-directory-integrating-applications.md)。</span><span class="sxs-lookup"><span data-stu-id="9d382-122">For more detailed information about creating a new app registration, see [Integrating applications with Azure Active Directory](.//develop/active-directory-integrating-applications.md).</span></span>


## <a name="step-3-grant-access-to-other-applications"></a><span data-ttu-id="9d382-123">步驟 3：授與其他應用程式存取權</span><span class="sxs-lookup"><span data-stu-id="9d382-123">Step 3: Grant access to other applications</span></span>
<span data-ttu-id="9d382-124">啟用要公開給您的目錄中的其他應用程式的原生應用程式：</span><span class="sxs-lookup"><span data-stu-id="9d382-124">Enable the native application to be exposed to other applications in your directory:</span></span>

1. <span data-ttu-id="9d382-125">仍在 [應用程式註冊] 中，選取您剛才建立的新原生應用程式。</span><span class="sxs-lookup"><span data-stu-id="9d382-125">Still in **App registrations**, select the new native application that you just created.</span></span>
2. <span data-ttu-id="9d382-126">選取 [必要權限]。</span><span class="sxs-lookup"><span data-stu-id="9d382-126">Select **Required permissions**.</span></span>
3. <span data-ttu-id="9d382-127">選取 [新增] 。</span><span class="sxs-lookup"><span data-stu-id="9d382-127">Select **Add**.</span></span>
4. <span data-ttu-id="9d382-128">開啟第一個步驟 [選取 API]。</span><span class="sxs-lookup"><span data-stu-id="9d382-128">Open the first step, **Select an API**.</span></span>
5. <span data-ttu-id="9d382-129">使用搜尋列，尋找您在第一節中發佈的「應用程式 Proxy」應用程式。</span><span class="sxs-lookup"><span data-stu-id="9d382-129">Use the search bar to find the Application Proxy app that you published in the first section.</span></span> <span data-ttu-id="9d382-130">選擇該應用程式，然後按一下 [選取]。</span><span class="sxs-lookup"><span data-stu-id="9d382-130">Choose that app, then click **Select**.</span></span> 

   ![搜尋 Proxy 應用程式](./media/active-directory-application-proxy-native-client/select_api.png)
6. <span data-ttu-id="9d382-132">開啟第二個步驟 [選取權限]。</span><span class="sxs-lookup"><span data-stu-id="9d382-132">Open the second step, **Select permissions**.</span></span>
7. <span data-ttu-id="9d382-133">使用核取方塊授與 Proxy 應用程式的原生應用程式存取權，然後按一下 [選取]。</span><span class="sxs-lookup"><span data-stu-id="9d382-133">Use the checkbox to grant your native application access to your proxy application, then click **Select**.</span></span>

   ![授與 Proxy 應用程式存取權](./media/active-directory-application-proxy-native-client/select_perms.png)
8. <span data-ttu-id="9d382-135">選取 [完成] 。</span><span class="sxs-lookup"><span data-stu-id="9d382-135">Select **Done**.</span></span>


## <a name="step-4-edit-the-active-directory-authentication-library"></a><span data-ttu-id="9d382-136">步驟 4：編輯 Active Directory 驗證程式庫</span><span class="sxs-lookup"><span data-stu-id="9d382-136">Step 4: Edit the Active Directory Authentication Library</span></span>
<span data-ttu-id="9d382-137">在 Active Directory 驗證程式庫 (ADAL) 的驗證內容中編輯原生應用程式程式碼，以包含下列文字：</span><span class="sxs-lookup"><span data-stu-id="9d382-137">Edit the native application code in the authentication context of the Active Directory Authentication Library (ADAL) to include the following text:</span></span>

```
// Acquire Access Token from AAD for Proxy Application
AuthenticationContext authContext = new AuthenticationContext("https://login.microsoftonline.com/<Tenant ID>");
AuthenticationResult result = authContext.AcquireToken("< External Url of Proxy App >",
        "<App ID of the Native app>",
        new Uri("<Redirect Uri of the Native App>"),
        PromptBehavior.Never);

//Use the Access Token to access the Proxy Application
HttpClient httpClient = new HttpClient();
httpClient.DefaultRequestHeaders.Authorization = new AuthenticationHeaderValue("Bearer", result.AccessToken);
HttpResponseMessage response = await httpClient.GetAsync("< Proxy App API Url >");
```

<span data-ttu-id="9d382-138">範例程式碼中的變數應取代如下：</span><span class="sxs-lookup"><span data-stu-id="9d382-138">The variables in the sample code should be replaced as follows:</span></span>

* <span data-ttu-id="9d382-139">**租用戶識別碼**可以在 Azure 入口網站中找到。</span><span class="sxs-lookup"><span data-stu-id="9d382-139">**Tenant ID** can be found in the Azure portal.</span></span> <span data-ttu-id="9d382-140">巡覽至 [Azure Active Directory] > [屬性]，然後複製目錄識別碼。</span><span class="sxs-lookup"><span data-stu-id="9d382-140">Navigate to **Azure Active Directory** > **Properties** and copy the Directory ID.</span></span> 
* <span data-ttu-id="9d382-141">[外部 URL] 是您在 Proxy 應用程式中輸入的前端 URL。</span><span class="sxs-lookup"><span data-stu-id="9d382-141">**External URL** is the front-end URL you entered in the Proxy Application.</span></span> <span data-ttu-id="9d382-142">若要尋找此值，請巡覽至 Proxy 應用程式的 [應用程式 Proxy] 區段。</span><span class="sxs-lookup"><span data-stu-id="9d382-142">To find this value, navigate to the **Application proxy** section of the proxy app.</span></span>
* <span data-ttu-id="9d382-143">原生應用程式的**應用程式識別碼**可以在原生應用程式的 [屬性] 頁面上找到。</span><span class="sxs-lookup"><span data-stu-id="9d382-143">**App ID** of the native app can be found on the **Properties** page of the native application.</span></span>
* <span data-ttu-id="9d382-144">**原生應用程式的重新導向 URI** 可以在原生應用程式的 [重新導向 URI] 頁面上找到。</span><span class="sxs-lookup"><span data-stu-id="9d382-144">**Redirect URI of the native app** can be found on the **Redirect URIs** page of the native application.</span></span>


## <a name="see-also"></a><span data-ttu-id="9d382-145">另請參閱</span><span class="sxs-lookup"><span data-stu-id="9d382-145">See also</span></span>

<span data-ttu-id="9d382-146">如需原生應用程式流程的詳細資訊，請參閱[原生應用程式到 Web API](develop/active-directory-authentication-scenarios.md#native-application-to-web-api)。</span><span class="sxs-lookup"><span data-stu-id="9d382-146">For more information about the native application flow, see [Native application to web API](develop/active-directory-authentication-scenarios.md#native-application-to-web-api)</span></span>

<span data-ttu-id="9d382-147">如需最新消息，請查閱 [應用程式 Proxy 部落格](http://blogs.technet.com/b/applicationproxyblog/)</span><span class="sxs-lookup"><span data-stu-id="9d382-147">For the latest news and updates, check out the [Application Proxy blog](http://blogs.technet.com/b/applicationproxyblog/)</span></span>
