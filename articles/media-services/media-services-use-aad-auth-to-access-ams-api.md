---
title: "aaaAccess Azure 媒體服務 API 與 Azure Active Directory 驗證 |Microsoft 文件"
description: "深入了解概念及步驟 tootake toouse Azure Active Directory (Azure AD) tooauthenticate 存取 toohello Azure 媒體服務 API。"
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/17/2017
ms.author: juliako
ms.openlocfilehash: bb8f75f39100dc37098260c24ab4a199ef689d46
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="access-hello-azure-media-services-api-with-azure-ad-authentication"></a><span data-ttu-id="d784d-103">存取 hello Azure 媒體服務 API 與 Azure AD 驗證</span><span class="sxs-lookup"><span data-stu-id="d784d-103">Access hello Azure Media Services API with Azure AD authentication</span></span>
 
<span data-ttu-id="d784d-104">hello Azure Media Services API 是 Rest API。</span><span class="sxs-lookup"><span data-stu-id="d784d-104">hello Azure Media Services API is a RESTful API.</span></span> <span data-ttu-id="d784d-105">您可以使用它 tooperform 媒體資源的作業使用 REST API，或使用可用的用戶端 Sdk。</span><span class="sxs-lookup"><span data-stu-id="d784d-105">You can use it tooperform operations on media resources by using a REST API or by using available client SDKs.</span></span> <span data-ttu-id="d784d-106">Azure 媒體服務提供適用於 Microsoft .NET 的媒體服務用戶端 SDK。</span><span class="sxs-lookup"><span data-stu-id="d784d-106">Azure Media Services offers a Media Services client SDK for Microsoft .NET.</span></span> <span data-ttu-id="d784d-107">toobe 授權 tooaccess Media Services 資源和 hello Media Services API，您必須先通過驗證。</span><span class="sxs-lookup"><span data-stu-id="d784d-107">toobe authorized tooaccess Media Services resources and hello Media Services API, you must first be authenticated.</span></span> 

<span data-ttu-id="d784d-108">媒體服務支援 [Azure Active Directory (Azure AD) 型驗證](../active-directory/active-directory-whatis.md)。</span><span class="sxs-lookup"><span data-stu-id="d784d-108">Media Services supports [Azure Active Directory (Azure AD)-based authentication](../active-directory/active-directory-whatis.md).</span></span> <span data-ttu-id="d784d-109">hello Azure 媒體 REST 服務，必須具備 hello 使用者或應用程式可發出 hello REST API 要求的其中一個 hello**參與者**或**擁有者**角色 tooaccess hello 資源。</span><span class="sxs-lookup"><span data-stu-id="d784d-109">hello Azure Media REST service requires that hello user or application that makes hello REST API requests have either hello **Contributor** or **Owner** role tooaccess hello resources.</span></span> <span data-ttu-id="d784d-110">如需詳細資訊，請參閱[開始 hello Azure 入口網站中的 角色型存取控制使用](../active-directory/role-based-access-control-what-is.md)。</span><span class="sxs-lookup"><span data-stu-id="d784d-110">For more information, see [Get started with Role-Based Access Control in hello Azure portal](../active-directory/role-based-access-control-what-is.md).</span></span>  

> [!IMPORTANT]
> <span data-ttu-id="d784d-111">目前，Media Services 支援 hello Azure 存取控制服務驗證模型。</span><span class="sxs-lookup"><span data-stu-id="d784d-111">Currently, Media Services supports hello Azure Access Control service authentication model.</span></span> <span data-ttu-id="d784d-112">不過，存取控制授權將在 2018 年 6 月 1 日被取代。</span><span class="sxs-lookup"><span data-stu-id="d784d-112">However, Access Control authorization will be deprecated on June 1, 2018.</span></span> <span data-ttu-id="d784d-113">我們建議您儘速移轉 toohello Azure AD 驗證模型。</span><span class="sxs-lookup"><span data-stu-id="d784d-113">We recommend that you migrate toohello Azure AD authentication model as soon as possible.</span></span>

<span data-ttu-id="d784d-114">本文件概略 tooaccess hello Media Services API 使用 REST 或.NET 應用程式開發介面的方式。</span><span class="sxs-lookup"><span data-stu-id="d784d-114">This document gives an overview of how tooaccess hello Media Services API by using REST or .NET APIs.</span></span>

## <a name="access-control"></a><span data-ttu-id="d784d-115">存取控制</span><span class="sxs-lookup"><span data-stu-id="d784d-115">Access control</span></span>

<span data-ttu-id="d784d-116">Hello Azure 媒體 REST 要求 toosucceed，hello 呼叫使用者必須 hello 它嘗試 tooaccess Media Services 帳戶的參與者或擁有者角色。</span><span class="sxs-lookup"><span data-stu-id="d784d-116">For hello Azure Media REST request toosucceed, hello calling user must have a Contributor or Owner role for hello Media Services account it is trying tooaccess.</span></span>  
<span data-ttu-id="d784d-117">只有具備 hello 擁有者角色的使用者可以提供媒體資源 （帳戶） 存取 toonew 使用者或應用程式。</span><span class="sxs-lookup"><span data-stu-id="d784d-117">Only a user with hello Owner role can give media resource (account) access toonew users or apps.</span></span> <span data-ttu-id="d784d-118">hello 參與者角色可以存取 hello 媒體資源。</span><span class="sxs-lookup"><span data-stu-id="d784d-118">hello Contributor role can access only hello media resource.</span></span>
<span data-ttu-id="d784d-119">未經授權的要求會失敗，狀態碼為 401。</span><span class="sxs-lookup"><span data-stu-id="d784d-119">Unauthorized requests fail, with status code of 401.</span></span> <span data-ttu-id="d784d-120">如果您看到此錯誤的程式碼，請檢查您的使用者是否具有 hello 參與者或 hello 使用者 Media Services 帳戶指派的擁有者角色。</span><span class="sxs-lookup"><span data-stu-id="d784d-120">If you see this error code, check whether your user has hello Contributor or Owner role assigned for hello user's Media Services account.</span></span> <span data-ttu-id="d784d-121">您可以檢查這個 hello Azure 入口網站中。</span><span class="sxs-lookup"><span data-stu-id="d784d-121">You can check this in hello Azure portal.</span></span> <span data-ttu-id="d784d-122">搜尋您媒體的帳戶，然後再按一下 [hello**存取控制**] 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="d784d-122">Search for your media account, and then click hello **Access control** tab.</span></span> 

![[Access control] \(存取控制\) 索引標籤](./media/media-services-use-aad-auth-to-access-ams-api/media-services-access-control.png)

## <a name="types-of-authentication"></a><span data-ttu-id="d784d-124">驗證類型</span><span class="sxs-lookup"><span data-stu-id="d784d-124">Types of authentication</span></span> 
 
<span data-ttu-id="d784d-125">當您使用 Azure AD 驗證搭配 Azure 媒體服務 時，會有兩個驗證選項：</span><span class="sxs-lookup"><span data-stu-id="d784d-125">When you use Azure AD authentication with Azure Media Services, you have two authentication options:</span></span>

- <span data-ttu-id="d784d-126">**使用者驗證**。</span><span class="sxs-lookup"><span data-stu-id="d784d-126">**User authentication**.</span></span> <span data-ttu-id="d784d-127">驗證使用 hello 應用程式 toointeract 和媒體服務資源的人員。</span><span class="sxs-lookup"><span data-stu-id="d784d-127">Authenticate a person who is using hello app toointeract with Media Services resources.</span></span> <span data-ttu-id="d784d-128">hello 互動式應用程式應該會先提示 hello hello 使用者提供認證的使用者。</span><span class="sxs-lookup"><span data-stu-id="d784d-128">hello interactive application should first prompt hello user for hello user's credentials.</span></span> <span data-ttu-id="d784d-129">範例是由授權的使用者 toomonitor 編碼工作的主控台應用程式管理或即時資料流。</span><span class="sxs-lookup"><span data-stu-id="d784d-129">An example is a management console app used by authorized users toomonitor encoding jobs or live streaming.</span></span> 
- <span data-ttu-id="d784d-130">**服務主體驗證**。</span><span class="sxs-lookup"><span data-stu-id="d784d-130">**Service principal authentication**.</span></span> <span data-ttu-id="d784d-131">驗證服務。</span><span class="sxs-lookup"><span data-stu-id="d784d-131">Authenticate a service.</span></span> <span data-ttu-id="d784d-132">通常使用這種驗證方法的應用程式有執行精靈服務、中介層服務或排程的工作的應用程式。</span><span class="sxs-lookup"><span data-stu-id="d784d-132">Applications that commonly use this authentication method are apps that run daemon services, middle-tier services, or scheduled jobs.</span></span> <span data-ttu-id="d784d-133">例如，Web 應用程式、函數應用程式、邏輯應用程式、API 或微服務。</span><span class="sxs-lookup"><span data-stu-id="d784d-133">Examples are web apps, function apps, logic apps, API, and microservices.</span></span>

### <a name="user-authentication"></a><span data-ttu-id="d784d-134">使用者驗證</span><span class="sxs-lookup"><span data-stu-id="d784d-134">User authentication</span></span> 

<span data-ttu-id="d784d-135">管理或監視原生應用程式之應用程式應該使用 hello 使用者驗證方法： 行動裝置應用程式、 Windows 應用程式和主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="d784d-135">Applications that should use hello user authentication method are management or monitoring native apps: mobile apps, Windows apps, and Console applications.</span></span> <span data-ttu-id="d784d-136">您想與其中一個 hello 下列案例中的 hello 服務人為互動時，這種解決方案非常有用：</span><span class="sxs-lookup"><span data-stu-id="d784d-136">This type of solution is useful when you want human interaction with hello service in one of hello following scenarios:</span></span>

- <span data-ttu-id="d784d-137">編碼工作的監控儀表板。</span><span class="sxs-lookup"><span data-stu-id="d784d-137">Monitoring dashboard for your encoding jobs.</span></span>
- <span data-ttu-id="d784d-138">即時串流的監控儀表板。</span><span class="sxs-lookup"><span data-stu-id="d784d-138">Monitoring dashboard for your live streams.</span></span>
- <span data-ttu-id="d784d-139">Media Services 帳戶中的桌面或行動使用者 tooadminister 資源的管理應用程式。</span><span class="sxs-lookup"><span data-stu-id="d784d-139">Management application for desktop or mobile users tooadminister resources in a Media Services account.</span></span>

> [!NOTE]
> <span data-ttu-id="d784d-140">這種驗證方法不應用於消費者對向應用程式。</span><span class="sxs-lookup"><span data-stu-id="d784d-140">This authentication method should not be used for consumer-facing applications.</span></span> 

<span data-ttu-id="d784d-141">原生應用程式必須先取得 Azure ad 存取權杖，然後再使用它，當您進行 HTTP 要求 toohello 媒體服務 REST API。</span><span class="sxs-lookup"><span data-stu-id="d784d-141">A native application must first acquire an access token from Azure AD, and then use it when you make HTTP requests toohello Media Services REST API.</span></span> <span data-ttu-id="d784d-142">新增 hello 存取語彙基元 toohello 要求標頭。</span><span class="sxs-lookup"><span data-stu-id="d784d-142">Add hello access token toohello request header.</span></span> 

<span data-ttu-id="d784d-143">hello 下列圖表顯示一般的互動式應用程式的驗證流程：</span><span class="sxs-lookup"><span data-stu-id="d784d-143">hello following diagram shows a typical interactive application authentication flow:</span></span> 

![原生應用程式圖](./media/media-services-use-aad-auth-to-access-ams-api/media-services-native-aad-app1.png)

<span data-ttu-id="d784d-145">在之前圖表 hello，hello 數字代表 hello 資料流程的 hello 要求依時間先後順序。</span><span class="sxs-lookup"><span data-stu-id="d784d-145">In hello preceding diagram, hello numbers represent hello flow of hello requests in chronological order.</span></span>

> [!NOTE]
> <span data-ttu-id="d784d-146">當您使用 hello 使用者驗證方法時，所有的應用程式共用 hello 相同 （預設值） 的原生應用程式用戶端識別碼和原生應用程式重新導向 URI。</span><span class="sxs-lookup"><span data-stu-id="d784d-146">When you use hello user authentication method, all apps share hello same (default) native application client ID and native application redirect URI.</span></span> 

1. <span data-ttu-id="d784d-147">提示使用者輸入認證。</span><span class="sxs-lookup"><span data-stu-id="d784d-147">Prompt a user for credentials.</span></span>
2. <span data-ttu-id="d784d-148">以下列參數的 hello 要求 Azure AD 存取權杖：</span><span class="sxs-lookup"><span data-stu-id="d784d-148">Request an Azure AD access token with hello following parameters:</span></span>  

    * <span data-ttu-id="d784d-149">Azure AD 租用戶端點。</span><span class="sxs-lookup"><span data-stu-id="d784d-149">Azure AD tenant endpoint.</span></span>

        <span data-ttu-id="d784d-150">hello 租用戶資訊可以擷取從 hello Azure 入口網站。</span><span class="sxs-lookup"><span data-stu-id="d784d-150">hello tenant information can be retrieved from hello Azure portal.</span></span> <span data-ttu-id="d784d-151">Hello 右上角中，將游標放在 hello hello 登入的使用者名稱。</span><span class="sxs-lookup"><span data-stu-id="d784d-151">Place your cursor over hello name of hello signed-in user in hello top right corner.</span></span>
    * <span data-ttu-id="d784d-152">媒體服務資源 URI。</span><span class="sxs-lookup"><span data-stu-id="d784d-152">Media Services resource URI.</span></span> 

        <span data-ttu-id="d784d-153">這個 URI 是 hello 相同 hello 中的媒體服務帳戶相同的 Azure 環境 (例如，https://rest.media.azure.net)。</span><span class="sxs-lookup"><span data-stu-id="d784d-153">This URI is hello same for Media Services accounts that are in hello same Azure environment (for example, https://rest.media.azure.net).</span></span>

    * <span data-ttu-id="d784d-154">媒體服務 (原生) 應用程式用戶端識別碼。</span><span class="sxs-lookup"><span data-stu-id="d784d-154">Media Services (native) application client ID.</span></span>
    * <span data-ttu-id="d784d-155">媒體服務 (原生) 應用程式重新導向 URI。</span><span class="sxs-lookup"><span data-stu-id="d784d-155">Media Services (native) application redirect URI.</span></span>
    * <span data-ttu-id="d784d-156">REST 媒體服務的資源 URI。</span><span class="sxs-lookup"><span data-stu-id="d784d-156">Resource URI for REST Media Services.</span></span>
        
        <span data-ttu-id="d784d-157">hello URI 表示 hello REST API 端點 (例如，https://test03.restv2.westus.media.azure.net/api/)。</span><span class="sxs-lookup"><span data-stu-id="d784d-157">hello URI represents hello REST API endpoint (for example, https://test03.restv2.westus.media.azure.net/api/).</span></span>

    <span data-ttu-id="d784d-158">tooget 值，這些參數，請參閱[使用 hello Azure 入口網站 tooaccess Azure AD 驗證設定](media-services-portal-get-started-with-aad.md)使用 hello 使用者驗證 選項。</span><span class="sxs-lookup"><span data-stu-id="d784d-158">tooget values for these parameters, see [Use hello Azure portal tooaccess Azure AD authentication settings](media-services-portal-get-started-with-aad.md) using hello user authentication option.</span></span>

3. <span data-ttu-id="d784d-159">hello Azure AD 存取權杖會傳送 toohello 用戶端。</span><span class="sxs-lookup"><span data-stu-id="d784d-159">hello Azure AD access token is sent toohello client.</span></span>
4. <span data-ttu-id="d784d-160">hello 用戶端傳送 hello Azure AD 存取權杖的要求的 toohello Azure 媒體 REST API。</span><span class="sxs-lookup"><span data-stu-id="d784d-160">hello client sends a request toohello Azure Media REST API with hello Azure AD access token.</span></span>
5. <span data-ttu-id="d784d-161">hello 用戶端 hello 資料從取回 Media Services。</span><span class="sxs-lookup"><span data-stu-id="d784d-161">hello client gets back hello data from Media Services.</span></span>

<span data-ttu-id="d784d-162">如需如何使用 Media Services.NET 用戶端 hello SDK toouse Azure AD 驗證 toocommunicate 與其他要求資訊，請參閱[使用 Azure AD 驗證 tooaccess hello 與.NET 的 Media Services API](media-services-dotnet-get-started-with-aad.md)。</span><span class="sxs-lookup"><span data-stu-id="d784d-162">For information about how toouse Azure AD authentication toocommunicate with REST requests by using hello Media Services .NET client SDK, see [Use Azure AD authentication tooaccess hello Media Services API with .NET](media-services-dotnet-get-started-with-aad.md).</span></span> 

<span data-ttu-id="d784d-163">如果您未使用 Media Services.NET 用戶端 hello SDK，您必須手動建立的 Azure AD 存取權杖要求，使用步驟 2 中所述的 hello 參數。</span><span class="sxs-lookup"><span data-stu-id="d784d-163">If you are not using hello Media Services .NET client SDK, you must manually create an Azure AD access token request by using hello parameters described in step 2.</span></span> <span data-ttu-id="d784d-164">如需詳細資訊，請參閱[toouse hello Azure AD 驗證程式庫 tooget 如何 hello Azure AD 權杖](../active-directory/develop/active-directory-authentication-libraries.md)。</span><span class="sxs-lookup"><span data-stu-id="d784d-164">For more information, see [How toouse hello Azure AD Authentication Library tooget hello Azure AD token](../active-directory/develop/active-directory-authentication-libraries.md).</span></span>

### <a name="service-principal-authentication"></a><span data-ttu-id="d784d-165">服務主體驗證</span><span class="sxs-lookup"><span data-stu-id="d784d-165">Service principal authentication</span></span>

<span data-ttu-id="d784d-166">通常使用這種驗證方法的應用程式有執行中介層服務和排程的工作的應用程式：Web 應用程式、函數應用程式、邏輯應用程式、API 和微服務。</span><span class="sxs-lookup"><span data-stu-id="d784d-166">Applications that commonly use this authentication method are apps that run middle-tier services and scheduled jobs: web apps, function apps, logic apps, APIs, and microservices.</span></span> <span data-ttu-id="d784d-167">此驗證方法也會是適用於互動式應用程式，您可能會想 toouse 服務帳戶 toomanage 資源項目。</span><span class="sxs-lookup"><span data-stu-id="d784d-167">This authentication method also is suitable for interactive applications in which you might want toouse a service account toomanage resources.</span></span>

<span data-ttu-id="d784d-168">當您使用 hello 服務主體的驗證方法 toobuild 取用者案例時，驗證通常會處理在 hello 中介層 （透過某些應用程式開發介面），並不是直接在行動或桌面應用程式中。</span><span class="sxs-lookup"><span data-stu-id="d784d-168">When you use hello service principal authentication method toobuild consumer scenarios, authentication typically is handled in hello middle tier (through some API) and not directly in a mobile or desktop application.</span></span> 

<span data-ttu-id="d784d-169">toouse 這個方法建立的 Azure AD 應用程式和服務主體在它自己的租用戶中。</span><span class="sxs-lookup"><span data-stu-id="d784d-169">toouse this method, create an Azure AD application and service principal in its own tenant.</span></span> <span data-ttu-id="d784d-170">建立 hello 應用程式之後，授與 hello 應用程式參與者或擁有者角色存取 toohello Media Services 帳戶。</span><span class="sxs-lookup"><span data-stu-id="d784d-170">After you create hello application, give hello app Contributor or Owner role access toohello Media Services account.</span></span> <span data-ttu-id="d784d-171">您可以在 hello Azure 入口網站中使用 Azure CLI 或 PowerShell 指令碼。</span><span class="sxs-lookup"><span data-stu-id="d784d-171">You can do this in hello Azure portal, by using Azure CLI, or with a PowerShell script.</span></span> <span data-ttu-id="d784d-172">您也可以使用現有的 Azure AD 應用程式。</span><span class="sxs-lookup"><span data-stu-id="d784d-172">You also can use an existing Azure AD application.</span></span> <span data-ttu-id="d784d-173">您可以註冊及管理您的 Azure AD 應用程式和服務主體[hello Azure 入口網站中](media-services-portal-get-started-with-aad.md)。</span><span class="sxs-lookup"><span data-stu-id="d784d-173">You can register and manage your Azure AD app and service principal [in hello Azure portal](media-services-portal-get-started-with-aad.md).</span></span> <span data-ttu-id="d784d-174">您也可以使用 [Azure CLI 2.0](media-services-use-aad-auth-to-access-ams-api.md) 或 [PowerShell](media-services-powershell-create-and-configure-aad-app.md) 執行此動作。</span><span class="sxs-lookup"><span data-stu-id="d784d-174">You also can do this by using [Azure CLI 2.0](media-services-use-aad-auth-to-access-ams-api.md) or [PowerShell](media-services-powershell-create-and-configure-aad-app.md).</span></span> 

![中介層應用程式](./media/media-services-use-aad-auth-to-access-ams-api/media-services-principal-service-aad-app1.png)

<span data-ttu-id="d784d-176">建立您的 Azure AD 應用程式之後，您會取得 hello 下列設定的值。</span><span class="sxs-lookup"><span data-stu-id="d784d-176">After you create your Azure AD application, you get values for hello following settings.</span></span> <span data-ttu-id="d784d-177">您需要這些值以進行驗證：</span><span class="sxs-lookup"><span data-stu-id="d784d-177">You need these values for authentication:</span></span>

- <span data-ttu-id="d784d-178">用戶端識別碼</span><span class="sxs-lookup"><span data-stu-id="d784d-178">Client ID</span></span> 
- <span data-ttu-id="d784d-179">用戶端密碼</span><span class="sxs-lookup"><span data-stu-id="d784d-179">Client secret</span></span> 

<span data-ttu-id="d784d-180">在上述圖 hello，hello 數字代表 hello 流程依時間先後順序中的 hello 要求：</span><span class="sxs-lookup"><span data-stu-id="d784d-180">In hello preceding figure, hello numbers represent hello flow of hello requests in chronological order:</span></span>
    
1. <span data-ttu-id="d784d-181">中介層應用程式 （web API 或 web 應用程式） 會要求具有下列參數的 hello Azure AD 存取權杖：</span><span class="sxs-lookup"><span data-stu-id="d784d-181">A middle-tier app (web API or web application) requests an Azure AD access token that has hello following parameters:</span></span>  

    * <span data-ttu-id="d784d-182">Azure AD 租用戶端點。</span><span class="sxs-lookup"><span data-stu-id="d784d-182">Azure AD tenant endpoint.</span></span>

        <span data-ttu-id="d784d-183">hello 租用戶資訊可以擷取從 hello Azure 入口網站。</span><span class="sxs-lookup"><span data-stu-id="d784d-183">hello tenant information can be retrieved from hello Azure portal.</span></span> <span data-ttu-id="d784d-184">Hello 右上角中，將游標放在 hello hello 登入的使用者名稱。</span><span class="sxs-lookup"><span data-stu-id="d784d-184">Place your cursor over hello name of hello signed-in user in hello top right corner.</span></span>
    * <span data-ttu-id="d784d-185">媒體服務資源 URI。</span><span class="sxs-lookup"><span data-stu-id="d784d-185">Media Services resource URI.</span></span> 

        <span data-ttu-id="d784d-186">這個 URI 是 hello 相同位於 hello 的 Media Services 帳戶相同的 Azure 環境 (例如，https://rest.media.azure.net)。</span><span class="sxs-lookup"><span data-stu-id="d784d-186">This URI is hello same for Media Services accounts that are located in hello same Azure environment (for example, https://rest.media.azure.net).</span></span>

    * <span data-ttu-id="d784d-187">REST 媒體服務的資源 URI。</span><span class="sxs-lookup"><span data-stu-id="d784d-187">Resource URI for REST Media Services.</span></span>

        <span data-ttu-id="d784d-188">hello URI 表示 hello REST API 端點 (例如，https://test03.restv2.westus.media.azure.net/api/)。</span><span class="sxs-lookup"><span data-stu-id="d784d-188">hello URI represents hello REST API endpoint (for example, https://test03.restv2.westus.media.azure.net/api/).</span></span>

    * <span data-ttu-id="d784d-189">Azure AD 應用程式的值： hello 用戶端識別碼和用戶端密碼。</span><span class="sxs-lookup"><span data-stu-id="d784d-189">Azure AD application values: hello client ID and client secret.</span></span>
    
    <span data-ttu-id="d784d-190">tooget 值，這些參數，請參閱[使用 hello Azure 入口網站 tooaccess Azure AD 驗證設定](media-services-portal-get-started-with-aad.md)使用 hello 服務主體的驗證選項。</span><span class="sxs-lookup"><span data-stu-id="d784d-190">tooget values for these parameters, see [Use hello Azure portal tooaccess Azure AD authentication settings](media-services-portal-get-started-with-aad.md) by using hello service principal authentication option.</span></span>

2. <span data-ttu-id="d784d-191">hello Azure AD 存取權杖會傳送 toohello 中介層。</span><span class="sxs-lookup"><span data-stu-id="d784d-191">hello Azure AD access token is sent toohello middle tier.</span></span>
4. <span data-ttu-id="d784d-192">hello 中介層會傳送 hello Azure AD 權杖的要求 toohello Azure 媒體 REST API。</span><span class="sxs-lookup"><span data-stu-id="d784d-192">hello middle tier sends request toohello Azure Media REST API with hello Azure AD token.</span></span>
5. <span data-ttu-id="d784d-193">hello 中介層回取得 Media Services hello 資料。</span><span class="sxs-lookup"><span data-stu-id="d784d-193">hello middle tier gets back hello data from Media Services.</span></span>

<span data-ttu-id="d784d-194">如需有關如何使用 Media Services.NET 用戶端 hello SDK toouse Azure AD 驗證 toocommunicate 與其他要求的詳細資訊，請參閱[使用 Azure AD 驗證 tooaccess 與.NET 的 Azure 媒體服務 API](media-services-dotnet-get-started-with-aad.md)。</span><span class="sxs-lookup"><span data-stu-id="d784d-194">For more information about how toouse Azure AD authentication toocommunicate with REST requests by using hello Media Services .NET client SDK, see [Use Azure AD authentication tooaccess Azure Media Services API with .NET](media-services-dotnet-get-started-with-aad.md).</span></span> 

<span data-ttu-id="d784d-195">如果您未使用 Media Services.NET 用戶端 hello SDK，您必須手動建立的 Azure AD 的權杖要求，使用步驟 1 中所述的參數。</span><span class="sxs-lookup"><span data-stu-id="d784d-195">If you are not using hello Media Services .NET client SDK, you must manually create an Azure AD token request by using parameters described in step 1.</span></span> <span data-ttu-id="d784d-196">如需詳細資訊，請參閱[toouse hello Azure AD 驗證程式庫 tooget 如何 hello Azure AD 權杖](../active-directory/develop/active-directory-authentication-libraries.md)。</span><span class="sxs-lookup"><span data-stu-id="d784d-196">For more information, see [How toouse hello Azure AD Authentication Library tooget hello Azure AD token](../active-directory/develop/active-directory-authentication-libraries.md).</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="d784d-197">疑難排解</span><span class="sxs-lookup"><span data-stu-id="d784d-197">Troubleshooting</span></span>

<span data-ttu-id="d784d-198">例外狀況:"hello 遠端伺服器傳回錯誤: (401) 未授權。 」</span><span class="sxs-lookup"><span data-stu-id="d784d-198">Exception: "hello remote server returned an error: (401) Unauthorized."</span></span>

<span data-ttu-id="d784d-199">解決方案： Hello 媒體服務 REST 要求 toosucceed，hello 呼叫使用者必須 hello 它嘗試 tooaccess Media Services 帳戶中的參與者或擁有者角色。</span><span class="sxs-lookup"><span data-stu-id="d784d-199">Solution: For hello Media Services REST request toosucceed, hello calling user must be a Contributor or Owner role in hello Media Services account it is trying tooaccess.</span></span> <span data-ttu-id="d784d-200">如需詳細資訊，請參閱 hello[存取控制](media-services-use-aad-auth-to-access-ams-api.md#access-control)> 一節。</span><span class="sxs-lookup"><span data-stu-id="d784d-200">For more information, see hello [Access control](media-services-use-aad-auth-to-access-ams-api.md#access-control) section.</span></span>

## <a name="resources"></a><span data-ttu-id="d784d-201">資源</span><span class="sxs-lookup"><span data-stu-id="d784d-201">Resources</span></span>

<span data-ttu-id="d784d-202">下列文件的 hello 是 Azure AD 驗證概念的概觀：</span><span class="sxs-lookup"><span data-stu-id="d784d-202">hello following articles are overviews of Azure AD authentication concepts:</span></span> 

- [<span data-ttu-id="d784d-203">Azure AD 的驗證案例</span><span class="sxs-lookup"><span data-stu-id="d784d-203">Authentication scenarios addressed by Azure AD</span></span>](../active-directory/develop/active-directory-authentication-scenarios.md#basics-of-authentication-in-azure-ad)
- [<span data-ttu-id="d784d-204">在 Azure AD 新增、更新或移除應用程式</span><span class="sxs-lookup"><span data-stu-id="d784d-204">Add, update, or remove an application in Azure AD</span></span>](../active-directory/develop/active-directory-integrating-applications.md)
- [<span data-ttu-id="d784d-205">使用 PowerShell 設定及 管理角色型存取控制</span><span class="sxs-lookup"><span data-stu-id="d784d-205">Configure and manage Role-Based Access Control by using PowerShell</span></span>](../active-directory/role-based-access-control-manage-access-powershell.md)

## <a name="next-steps"></a><span data-ttu-id="d784d-206">後續步驟</span><span class="sxs-lookup"><span data-stu-id="d784d-206">Next steps</span></span>

* <span data-ttu-id="d784d-207">使用 Azure 入口網站 hello 太[存取 Azure AD 驗證 tooconsume Azure Media Services API](media-services-portal-get-started-with-aad.md)。</span><span class="sxs-lookup"><span data-stu-id="d784d-207">Use hello Azure portal too[access Azure AD authentication tooconsume Azure Media Services API](media-services-portal-get-started-with-aad.md).</span></span>
* <span data-ttu-id="d784d-208">使用 Azure AD 驗證太[存取 Azure Media Services API 的.NET](media-services-dotnet-get-started-with-aad.md)。</span><span class="sxs-lookup"><span data-stu-id="d784d-208">Use Azure AD authentication too[access Azure Media Services API with .NET](media-services-dotnet-get-started-with-aad.md).</span></span>

