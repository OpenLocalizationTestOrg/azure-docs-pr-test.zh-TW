---
title: "Azure App Service 中的 API Apps aaaService 主體驗證 |Microsoft 文件"
description: "深入了解如何在 Azure App Service 中的服務對服務案例的 tooprotect API 應用程式。"
services: app-service\api
documentationcenter: .net
author: alexkarcher-msft
manager: erikre
editor: 
ms.assetid: 7ca0bab2-1d29-4d51-b779-dce0edd34f8b
ms.service: app-service-api
ms.workload: na
ms.tgt_pltfrm: dotnet
ms.devlang: na
ms.topic: article
ms.date: 06/30/2016
ms.author: alkarche
ms.openlocfilehash: 94d9ee11f38293df4a2fd815ef02c59cc6defed4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="service-principal-authentication-for-api-apps-in-azure-app-service"></a><span data-ttu-id="2c04f-103">在 Azure App Service 中 API Apps 的服務主體驗證</span><span class="sxs-lookup"><span data-stu-id="2c04f-103">Service principal authentication for API Apps in Azure App Service</span></span>
## <a name="overview"></a><span data-ttu-id="2c04f-104">概觀</span><span class="sxs-lookup"><span data-stu-id="2c04f-104">Overview</span></span>
<span data-ttu-id="2c04f-105">這篇文章說明如何 toouse 應用程式服務驗證*內部*存取 tooAPI 應用程式。</span><span class="sxs-lookup"><span data-stu-id="2c04f-105">This article explains how toouse App Service authentication for *internal* access tooAPI apps.</span></span> <span data-ttu-id="2c04f-106">內部的案例是您必須要 toobe 您可以使用自己的應用程式程式碼只能由 API 應用程式的位置。</span><span class="sxs-lookup"><span data-stu-id="2c04f-106">An internal scenario is where you have an API app that you want toobe consumable only by your own application code.</span></span> <span data-ttu-id="2c04f-107">hello 建議的方式 tooimplement 這種情況下在應用程式服務 toouse Azure AD tooprotect hello 稱為 API 應用程式。</span><span class="sxs-lookup"><span data-stu-id="2c04f-107">hello recommended way tooimplement this scenario in App Service is toouse Azure AD tooprotect hello called API app.</span></span> <span data-ttu-id="2c04f-108">您可以呼叫受保護的 hello API 應用程式，以從 Azure AD 取得藉由提供應用程式識別 （服務主體） 認證的承載權杖。</span><span class="sxs-lookup"><span data-stu-id="2c04f-108">You call hello protected API app with a bearer token that you get from Azure AD by providing application identity (service principal) credentials.</span></span> <span data-ttu-id="2c04f-109">替代項目 toousing Azure AD，請參閱 hello**服務對服務驗證**區段 hello [Azure 應用程式服務驗證概觀](../app-service/app-service-authentication-overview.md#service-to-service-authentication)。</span><span class="sxs-lookup"><span data-stu-id="2c04f-109">For alternatives toousing Azure AD, see hello **Service-to-service authentication** section of hello [Azure App Service authentication overview](../app-service/app-service-authentication-overview.md#service-to-service-authentication).</span></span>

<span data-ttu-id="2c04f-110">在本文中，您將了解：</span><span class="sxs-lookup"><span data-stu-id="2c04f-110">In this article, you'll learn:</span></span>

* <span data-ttu-id="2c04f-111">如何從 toouse Azure Active Directory (Azure AD) tooprotect API 應用程式未經驗證的存取。</span><span class="sxs-lookup"><span data-stu-id="2c04f-111">How toouse Azure Active Directory (Azure AD) tooprotect an API app from unauthenticated access.</span></span>
* <span data-ttu-id="2c04f-112">如何從應用程式開發介面應用程式、 web 應用程式或行動裝置應用程式使用 Azure AD 服務主體 （應用程式身分識別） 認證 tooconsume 受保護的應用程式開發介面應用程式。</span><span class="sxs-lookup"><span data-stu-id="2c04f-112">How tooconsume a protected API app from an API app, web app, or mobile app by using Azure AD service principal (app identity) credentials.</span></span> <span data-ttu-id="2c04f-113">如需有關資訊 tooconsume 從邏輯應用程式，請參閱[使用您裝載邏輯應用程式的 App Service 上的自訂 API](../logic-apps/logic-apps-custom-hosted-api.md)。</span><span class="sxs-lookup"><span data-stu-id="2c04f-113">For information about how tooconsume from a logic app, see [Using your custom API hosted on App Service with Logic apps](../logic-apps/logic-apps-custom-hosted-api.md).</span></span>
* <span data-ttu-id="2c04f-114">如何 toomake 確認該 hello 保護 API 應用程式無法從瀏覽器呼叫登入的使用者。</span><span class="sxs-lookup"><span data-stu-id="2c04f-114">How toomake sure that hello protected API app can't be called from a browser by logged on users.</span></span>
* <span data-ttu-id="2c04f-115">Toomake 確認該 hello 保護 API 應用程式只能由特定呼叫 Azure AD 服務主體。</span><span class="sxs-lookup"><span data-stu-id="2c04f-115">How toomake sure that hello protected API app can only be called by a specific Azure AD service principal.</span></span>

<span data-ttu-id="2c04f-116">hello 文章包含兩個區段：</span><span class="sxs-lookup"><span data-stu-id="2c04f-116">hello article contains two sections:</span></span>

* <span data-ttu-id="2c04f-117">hello [tooconfigure 服務主體驗證 Azure App Service 中的方式](#authconfig)章節將說明一般方式 tooconfigure 驗證的任何應用程式開發介面應用程式和 tooconsume hello 如何保護應用程式開發介面應用程式。</span><span class="sxs-lookup"><span data-stu-id="2c04f-117">hello [How tooconfigure service principal authentication in Azure App Service](#authconfig) section explains in general how tooconfigure authentication for any API app, and how tooconsume hello protected API app.</span></span> <span data-ttu-id="2c04f-118">本章節同樣適用於 tooall 架構應用程式服務，包括.NET、 Node.js 和 Java 支援。</span><span class="sxs-lookup"><span data-stu-id="2c04f-118">This section applies equally tooall frameworks supported by App Service, including .NET, Node.js, and Java.</span></span>
* <span data-ttu-id="2c04f-119">開頭為 hello[繼續 hello.NET 使用者入門教學課程](#tutorialstart) 區段中，hello 教學課程引導您設定 App Service 中執行的.NET 範例應用程式的 「 內部存取 」 案例。</span><span class="sxs-lookup"><span data-stu-id="2c04f-119">Starting with hello [Continuing hello .NET getting-started tutorials](#tutorialstart) section, hello tutorial guides you through configuring an "internal access" scenario for a .NET sample application running in App Service.</span></span> 

## <span data-ttu-id="2c04f-120"><a id="authconfig"></a>Tooconfigure 服務主體驗證 Azure App Service 中的方式</span><span class="sxs-lookup"><span data-stu-id="2c04f-120"><a id="authconfig"></a> How tooconfigure service principal authentication in Azure App Service</span></span>
<span data-ttu-id="2c04f-121">本節提供適用於 tooany API 應用程式的一般指示。</span><span class="sxs-lookup"><span data-stu-id="2c04f-121">This section provides general instructions that apply tooany API app.</span></span> <span data-ttu-id="2c04f-122">步驟特定 toohello tooDo 清單.NET 範例應用程式，跳過[繼續 hello.NET API 的應用程式的教學課程系列](#tutorialstart)。</span><span class="sxs-lookup"><span data-stu-id="2c04f-122">For steps specific toohello tooDo List .NET sample application, go too[Continuing hello .NET API Apps tutorial series](#tutorialstart).</span></span>

1. <span data-ttu-id="2c04f-123">在 hello [Azure 入口網站](https://portal.azure.com/)，瀏覽 toohello**設定**刀鋒視窗中的 hello API 應用程式，tooprotect，並找出 hello**功能**區段，然後按一下**驗證 / 授權**。</span><span class="sxs-lookup"><span data-stu-id="2c04f-123">In hello [Azure portal](https://portal.azure.com/), navigate toohello **Settings** blade of hello API app that you want tooprotect, and then find hello **Features** section and click **Authentication/ Authorization**.</span></span>
   
    ![Azure 入口網站中的驗證/授權](./media/app-service-api-dotnet-user-principal-auth/features.png)
2. <span data-ttu-id="2c04f-125">在 hello**驗證 / 授權**刀鋒視窗中，按一下 **上**。</span><span class="sxs-lookup"><span data-stu-id="2c04f-125">In hello **Authentication / Authorization** blade, click **On**.</span></span>
3. <span data-ttu-id="2c04f-126">在 hello**當要求未經驗證的動作 tootake**下拉式清單中，選取**登入 Azure Active Directory** 。</span><span class="sxs-lookup"><span data-stu-id="2c04f-126">In hello **Action tootake when request is not authenticated** drop-down list, select **Log in with Azure Active Directory** .</span></span>
4. <span data-ttu-id="2c04f-127">在 [驗證提供者] 底下，選取 [Azure Active Directory]。</span><span class="sxs-lookup"><span data-stu-id="2c04f-127">Under **Authentication Providers**, select **Azure Active Directory**.</span></span>
   
    ![Azure 入口網站中的驗證/授權刀鋒視窗](./media/app-service-api-dotnet-user-principal-auth/authblade.png)
5. <span data-ttu-id="2c04f-129">設定 hello **Azure Active Directory 設定**刀鋒視窗 toocreate 新的 Azure AD 應用程式或使用現有 Azure AD 的應用程式如果您已經有您想 toouse。</span><span class="sxs-lookup"><span data-stu-id="2c04f-129">Configure hello **Azure Active Directory Settings** blade toocreate a new Azure AD application, or use an existing Azure AD application if you already have one that you want toouse.</span></span>
   
    <span data-ttu-id="2c04f-130">內部案例通常涉及 API 應用程式呼叫 API 應用程式。</span><span class="sxs-lookup"><span data-stu-id="2c04f-130">Internal scenarios typically involve an API app calling an API app.</span></span> <span data-ttu-id="2c04f-131">您可以為每一個 API 應用程式使用個別的 Azure AD 應用程式，或是全都使用同一個 Azure AD 應用程式。</span><span class="sxs-lookup"><span data-stu-id="2c04f-131">You can use separate Azure AD applications for each API app or just one Azure AD application.</span></span>
   
    <span data-ttu-id="2c04f-132">如需此刀鋒視窗的詳細指示，請參閱[如何 tooconfigure 您 App Service 應用程式 toouse 的 Azure Active Directory 登入](../app-service-mobile/app-service-mobile-how-to-configure-active-directory-authentication.md)。</span><span class="sxs-lookup"><span data-stu-id="2c04f-132">For detailed instructions on this blade, see [How tooconfigure your App Service application toouse Azure Active Directory login](../app-service-mobile/app-service-mobile-how-to-configure-active-directory-authentication.md).</span></span>
6. <span data-ttu-id="2c04f-133">當您完成 hello 驗證提供者組態刀鋒視窗中時，按一下 **確定**。</span><span class="sxs-lookup"><span data-stu-id="2c04f-133">When you're done with hello authentication provider configuration blade, click **OK**.</span></span>
7. <span data-ttu-id="2c04f-134">在 hello**驗證 / 授權**刀鋒視窗中，按一下 **儲存**。</span><span class="sxs-lookup"><span data-stu-id="2c04f-134">In hello **Authentication / Authorization** blade, click **Save**.</span></span>
   
    ![按一下 [Save] \(儲存)。](./media/app-service-api-dotnet-service-principal-auth/authsave.png)

<span data-ttu-id="2c04f-136">完成此動作後，應用程式服務僅允許要求呼叫端在 hello 設定 Azure AD 租用戶。</span><span class="sxs-lookup"><span data-stu-id="2c04f-136">When this is done, App Service only allows requests from callers in hello configured Azure AD tenant.</span></span> <span data-ttu-id="2c04f-137">受保護的 hello API 應用程式中不需要任何驗證或授權的程式碼。</span><span class="sxs-lookup"><span data-stu-id="2c04f-137">No authentication or authorization code is required in hello protected API app.</span></span> <span data-ttu-id="2c04f-138">hello 持有人權杖會傳入 toohello API 應用程式，以及常用的宣告 HTTP 標頭，而且您可以讀取該要求是從特定的呼叫者，例如服務主體的程式碼 toovalidate 中的資訊。</span><span class="sxs-lookup"><span data-stu-id="2c04f-138">hello bearer token is passed toohello API app along with commonly used claims in HTTP headers, and you can read that information in code toovalidate that requests are from a particular caller, such as a service principal.</span></span>

<span data-ttu-id="2c04f-139">此驗證功能的運作方式 hello 一樣適用於所有語言的應用程式服務支援，包括.NET、 Node.js 和 Java。</span><span class="sxs-lookup"><span data-stu-id="2c04f-139">This authentication functionality works hello same way for all languages that App service supports, including .NET, Node.js, and Java.</span></span> 

#### <a name="how-tooconsume-hello-protected-api-app"></a><span data-ttu-id="2c04f-140">Tooconsume hello 如何保護應用程式開發介面應用程式</span><span class="sxs-lookup"><span data-stu-id="2c04f-140">How tooconsume hello protected API app</span></span>
<span data-ttu-id="2c04f-141">hello 呼叫者必須提供應用程式開發介面呼叫 Azure AD 持有人權杖。</span><span class="sxs-lookup"><span data-stu-id="2c04f-141">hello caller must provide an Azure AD bearer token with API calls.</span></span> <span data-ttu-id="2c04f-142">tooget 持有者權杖，使用服務主體認證，hello 呼叫端會使用 Active Directory Authentication Library (ADAL for [.NET](https://www.nuget.org/packages/Microsoft.IdentityModel.Clients.ActiveDirectory)， [Node.js](https://github.com/AzureAD/azure-activedirectory-library-for-nodejs)，或[Java](https://github.com/AzureAD/azure-activedirectory-library-for-java))。</span><span class="sxs-lookup"><span data-stu-id="2c04f-142">tooget a bearer token using service principal credentials, hello caller uses Active Directory Authentication Library (ADAL for [.NET](https://www.nuget.org/packages/Microsoft.IdentityModel.Clients.ActiveDirectory), [Node.js](https://github.com/AzureAD/azure-activedirectory-library-for-nodejs), or [Java](https://github.com/AzureAD/azure-activedirectory-library-for-java)).</span></span> <span data-ttu-id="2c04f-143">tooget 語彙基元，呼叫 ADAL 的 hello 程式碼提供下列資訊 tooADAL hello:</span><span class="sxs-lookup"><span data-stu-id="2c04f-143">tooget a token, hello code that calls ADAL provides tooADAL hello following information:</span></span>

* <span data-ttu-id="2c04f-144">hello Azure AD 租用戶名稱。</span><span class="sxs-lookup"><span data-stu-id="2c04f-144">hello name of your Azure AD tenant.</span></span>
* <span data-ttu-id="2c04f-145">hello 用戶端識別碼和用戶端 （應用程式金鑰） 的密碼與 hello 呼叫端相關聯的 hello Azure AD 應用程式。</span><span class="sxs-lookup"><span data-stu-id="2c04f-145">hello client ID and client secret (app key) of hello Azure AD app associated with hello caller.</span></span>
* <span data-ttu-id="2c04f-146">hello 用戶端識別碼 hello hello 與相關聯的 Azure AD 應用程式的受保護的應用程式開發介面應用程式。</span><span class="sxs-lookup"><span data-stu-id="2c04f-146">hello client ID of hello Azure AD application associated with hello protected API app.</span></span> <span data-ttu-id="2c04f-147">(如果使用只在一個 Azure AD 應用程式時，這是 hello 相同的用戶端識別碼為 hello 一個 hello 呼叫端。)</span><span class="sxs-lookup"><span data-stu-id="2c04f-147">(If just one Azure AD application is used, this is hello same client ID as hello one for hello caller.)</span></span>

<span data-ttu-id="2c04f-148">這些值為 hello 的 hello Azure AD 頁面中提供[Azure 傳統入口網站](https://manage.windowsazure.com/)。</span><span class="sxs-lookup"><span data-stu-id="2c04f-148">These values are available in hello Azure AD pages of hello [Azure classic portal](https://manage.windowsazure.com/).</span></span>

<span data-ttu-id="2c04f-149">一旦取得的 hello 語彙基元，hello 呼叫端會包含它與 hello 授權標頭中的 HTTP 要求。</span><span class="sxs-lookup"><span data-stu-id="2c04f-149">Once hello token has been acquired, hello caller includes it with HTTP requests in hello Authorization header.</span></span>  <span data-ttu-id="2c04f-150">應用程式服務會驗證 hello 語彙基元，並允許 hello 要求 tooreach hello 保護 API 應用程式。</span><span class="sxs-lookup"><span data-stu-id="2c04f-150">App Service validates hello token and allows hello requests tooreach hello protected API app.</span></span>

#### <a name="how-tooprotect-hello-api-app-from-access-by-users-in-hello-same-tenant"></a><span data-ttu-id="2c04f-151">如何從 hello 中的使用者存取 tooprotect hello API 應用程式相同租用戶</span><span class="sxs-lookup"><span data-stu-id="2c04f-151">How tooprotect hello API app from access by users in hello same tenant</span></span>
<span data-ttu-id="2c04f-152">持有者權杖供使用者在同一個租用戶會被視為有效的 hello hello 受保護的應用程式開發介面應用程式。</span><span class="sxs-lookup"><span data-stu-id="2c04f-152">Bearer tokens for users in hello same tenant are considered valid for hello protected API app.</span></span>  <span data-ttu-id="2c04f-153">如果您想要只服務主體可以呼叫的 tooensure hello 受保護的應用程式開發介面應用程式，新增 hello 中的程式碼保護應用程式開發介面應用程式 toovalidate hello 遵循 hello 語彙基元的宣告：</span><span class="sxs-lookup"><span data-stu-id="2c04f-153">If you want tooensure that only a service principal can call hello protected API app, add code in hello protected API app toovalidate hello following claims from hello token:</span></span>

* <span data-ttu-id="2c04f-154">`appid`應該 hello 與 hello 呼叫端相關聯的 hello Azure AD 應用程式的用戶端識別碼。</span><span class="sxs-lookup"><span data-stu-id="2c04f-154">`appid` should be hello client ID of hello Azure AD application that is associated with hello caller.</span></span> 
* <span data-ttu-id="2c04f-155">`oid`(`objectidentifier`) 應該是 hello hello 呼叫端的服務主體識別碼。</span><span class="sxs-lookup"><span data-stu-id="2c04f-155">`oid` (`objectidentifier`) should be hello service principal ID of hello caller.</span></span> 

<span data-ttu-id="2c04f-156">應用程式服務也提供 hello `objectidentifier` hello X MS-用戶端-主體識別碼標頭中的宣告。</span><span class="sxs-lookup"><span data-stu-id="2c04f-156">App Service also provides hello `objectidentifier` claim in hello X-MS-CLIENT-PRINCIPAL-ID header.</span></span>

### <a name="how-tooprotect-hello-api-app-from-browser-access"></a><span data-ttu-id="2c04f-157">如何 tooprotect hello 從瀏覽器存取的 API 應用程式</span><span class="sxs-lookup"><span data-stu-id="2c04f-157">How tooprotect hello API app from browser access</span></span>
<span data-ttu-id="2c04f-158">如果您不要驗證在 hello 受保護的應用程式開發介面應用程式中的程式碼中的宣告，如果您使用不同的 Azure AD 應用程式 hello 受保護的應用程式開發介面應用程式，請確定該 hello Azure AD 應用程式的回覆 URL 是不 hello 與 hello API 應用程式的基底 URL 相同。</span><span class="sxs-lookup"><span data-stu-id="2c04f-158">If you don't validate claims in code in hello protected API app, and if you use a separate Azure AD application for hello protected API app, make sure that hello Azure AD application's Reply URL is not hello same as hello API app's base URL.</span></span> <span data-ttu-id="2c04f-159">如果 hello 回覆 URL 直接點 toohello 受保護的應用程式開發介面應用程式、 hello 相同的 Azure AD 租用戶中的使用者無法瀏覽 toohello API 應用程式、 登入，並且成功呼叫 hello API。</span><span class="sxs-lookup"><span data-stu-id="2c04f-159">If hello Reply URL points directly toohello protected API app, a user in hello same Azure AD tenant could browse toohello API app, log on, and successfully call hello API.</span></span>

## <span data-ttu-id="2c04f-160"><a id="tutorialstart"></a>繼續 hello.NET API 的應用程式的教學課程</span><span class="sxs-lookup"><span data-stu-id="2c04f-160"><a id="tutorialstart"></a> Continuing hello .NET API Apps tutorial series</span></span>
<span data-ttu-id="2c04f-161">如果您要遵照 hello Node.js 或 Java 教學課程系列的 API 應用程式，請略過 toohello[後續步驟](#next-steps)> 一節。</span><span class="sxs-lookup"><span data-stu-id="2c04f-161">If you are following hello Node.js or Java tutorial series for API apps, skip toohello [Next steps](#next-steps) section.</span></span> 

<span data-ttu-id="2c04f-162">hello 本文其餘部分會繼續 hello.NET API 的應用程式的教學課程，而且假設您已經完成 hello[使用者驗證教學課程](app-service-api-dotnet-user-principal-auth.md)，而且有 hello 範例應用程式在 Azure 中執行的使用者驗證啟用。</span><span class="sxs-lookup"><span data-stu-id="2c04f-162">hello remainder of this article continues hello .NET API Apps tutorial series and assumes that you have completed hello [user authentication tutorial](app-service-api-dotnet-user-principal-auth.md) and have hello sample application running in Azure with user authentication enabled.</span></span>

## <a name="set-up-authentication-in-azure"></a><span data-ttu-id="2c04f-163">在 Azure 中設定驗證</span><span class="sxs-lookup"><span data-stu-id="2c04f-163">Set up authentication in Azure</span></span>
<span data-ttu-id="2c04f-164">本節中您設定應用程式服務因此它可讓 tooreach hello 資料層應用程式開發介面應用程式的只有 HTTP 要求該 hello hello 的有有效的 Azure AD 持有者權杖。</span><span class="sxs-lookup"><span data-stu-id="2c04f-164">In this section you configure App Service so that hello only HTTP requests it allows tooreach hello data tier API app are hello ones that have valid Azure AD bearer tokens.</span></span> 

<span data-ttu-id="2c04f-165">在下列章節的 hello，設定 hello 中介層應用程式開發介面應用程式 toosend 應用程式認證 tooAzure AD、 取回持有者權杖，並傳送 hello 持有人權杖 toohello 資料層應用程式開發介面應用程式。</span><span class="sxs-lookup"><span data-stu-id="2c04f-165">In hello following section, you configure hello middle tier API app toosend application credentials tooAzure AD, get back a bearer token, and send hello bearer token toohello data tier API app.</span></span> <span data-ttu-id="2c04f-166">此程序如下所示 hello 圖表。</span><span class="sxs-lookup"><span data-stu-id="2c04f-166">This process is illustrated in hello diagram.</span></span>

![服務驗證圖表](./media/app-service-api-dotnet-service-principal-auth/appdiagram.png)

<span data-ttu-id="2c04f-168">如果您執行下列 hello 教學課程指引時出現問題，請參閱 hello[疑難排解](#troubleshooting)hello 結尾 hello 教學課程 > 一節。</span><span class="sxs-lookup"><span data-stu-id="2c04f-168">If you run into problems while following hello tutorial directions, see hello [Troubleshooting](#troubleshooting) section at hello end of hello tutorial.</span></span> 

1. <span data-ttu-id="2c04f-169">在 hello [Azure 入口網站](https://portal.azure.com/)，瀏覽 toohello**設定**刀鋒視窗中的 hello API 應用程式，您建立 hello ToDoListDataAPI （資料層） API 應用程式，然後按一下**設定**。</span><span class="sxs-lookup"><span data-stu-id="2c04f-169">In hello [Azure portal](https://portal.azure.com/), navigate toohello **Settings** blade of hello API app that you created for hello ToDoListDataAPI (data tier) API app, and then click **Settings**.</span></span>
2. <span data-ttu-id="2c04f-170">在 hello**設定**刀鋒視窗中，尋找 hello**功能**區段，然後再按一下**驗證 / 授權**。</span><span class="sxs-lookup"><span data-stu-id="2c04f-170">In hello **Settings** blade, find hello **Features** section, and then click **Authentication / Authorization**.</span></span>
   
    ![Azure 入口網站中的驗證/授權](./media/app-service-api-dotnet-user-principal-auth/features.png)
3. <span data-ttu-id="2c04f-172">在 hello**驗證 / 授權**刀鋒視窗中，按一下 **上**。</span><span class="sxs-lookup"><span data-stu-id="2c04f-172">In hello **Authentication / Authorization** blade, click **On**.</span></span>
4. <span data-ttu-id="2c04f-173">在 hello**當要求未經驗證的動作 tootake**下拉式清單中，選取**登入 Azure Active Directory**。</span><span class="sxs-lookup"><span data-stu-id="2c04f-173">In hello **Action tootake when request is not authenticated** drop-down list, select **Log in with Azure Active Directory**.</span></span>
   
    <span data-ttu-id="2c04f-174">這是造成只有已驗證要求觸達 hello API 應用程式的應用程式服務 tooensure hello 設定。</span><span class="sxs-lookup"><span data-stu-id="2c04f-174">This is hello setting that causes App Service tooensure that only authenticated requests reach hello API app.</span></span> <span data-ttu-id="2c04f-175">具有有效的持有者權杖的要求，應用程式服務傳遞 hello 語彙基元沿著 toohello API 應用程式並於其中填入的 HTTP 標頭與常用的宣告 toomake 該資訊更易於使用 tooyour 程式碼。</span><span class="sxs-lookup"><span data-stu-id="2c04f-175">For requests that have valid bearer tokens, App Service passes hello tokens along toohello API app and populates HTTP headers with commonly used claims toomake that information more easily available tooyour code.</span></span>
5. <span data-ttu-id="2c04f-176">在 [驗證提供者] 底下，按一下 [Azure Active Directory]。</span><span class="sxs-lookup"><span data-stu-id="2c04f-176">Under **Authentication Providers**, click **Azure Active Directory**.</span></span>
   
    ![Azure 入口網站中的驗證/授權刀鋒視窗](./media/app-service-api-dotnet-user-principal-auth/authblade.png)
6. <span data-ttu-id="2c04f-178">在 hello **Azure Active Directory 設定**刀鋒視窗中，按一下  **Express**。</span><span class="sxs-lookup"><span data-stu-id="2c04f-178">In hello **Azure Active Directory Settings** blade, click **Express**.</span></span>
   
    <span data-ttu-id="2c04f-179">以 hello **Express**選項 Azure 可以自動建立 AAD 應用程式，您的 Azure AD 中[租用戶](https://msdn.microsoft.com/en-us/library/azure/jj573650.aspx#BKMK_WhatIsAnAzureADTenant)。</span><span class="sxs-lookup"><span data-stu-id="2c04f-179">With hello **Express** option Azure can automatically create an AAD application in your Azure AD [tenant](https://msdn.microsoft.com/en-us/library/azure/jj573650.aspx#BKMK_WhatIsAnAzureADTenant).</span></span> 
   
    <span data-ttu-id="2c04f-180">您不需要 toocreate 租用戶，因為每個 Azure 帳戶會自動擁有一個。</span><span class="sxs-lookup"><span data-stu-id="2c04f-180">You don't have toocreate a tenant, because every Azure account automatically has one.</span></span>
7. <span data-ttu-id="2c04f-181">在 [管理模式] 底下，按一下 [建立新的 AD 應用程式] \(若尚未選取)。</span><span class="sxs-lookup"><span data-stu-id="2c04f-181">Under **Management mode**, click **Create New AD App** if it isn't already selected.</span></span>
   
    <span data-ttu-id="2c04f-182">hello 入口網站外掛 hello**建立應用程式**輸入的方塊中，預設值。</span><span class="sxs-lookup"><span data-stu-id="2c04f-182">hello portal plugs hello **Create App** input box with a default value.</span></span> <span data-ttu-id="2c04f-183">根據預設，名為 hello Azure AD 應用程式相同 hello 與 hello API 應用程式。</span><span class="sxs-lookup"><span data-stu-id="2c04f-183">By default, hello Azure AD application is named hello same as hello API app.</span></span> <span data-ttu-id="2c04f-184">如有需要，也可以輸入不同名稱。</span><span class="sxs-lookup"><span data-stu-id="2c04f-184">If you prefer, you can enter a different name.</span></span>
   
    ![Azure AD 設定](./media/app-service-api-dotnet-service-principal-auth/aadsettings.png)
   
    <span data-ttu-id="2c04f-186">**請注意**： 或者，您可以使用單一的 Azure AD 應用程式的同時 hello 呼叫 API 的應用程式和 hello 保護 API 應用程式。</span><span class="sxs-lookup"><span data-stu-id="2c04f-186">**Note**: As an alternative, you could use a single Azure AD application for both hello calling API app and hello protected API app.</span></span> <span data-ttu-id="2c04f-187">如果您選擇其他的替代方法，您不需要 hello**建立新的 AD 應用程式**這裡選項，因為您稍早在 hello 使用者驗證教學課程中，已經建立 Azure AD 應用程式。</span><span class="sxs-lookup"><span data-stu-id="2c04f-187">If you chose that alternative, you would not need hello **Create New AD App** option here because you already created an Azure AD application earlier in hello user authentication tutorial.</span></span> <span data-ttu-id="2c04f-188">此教學課程中，您將使用不同 Azure AD 應用程式呼叫 API 應用程式和 hello hello 受保護的應用程式開發介面應用程式。</span><span class="sxs-lookup"><span data-stu-id="2c04f-188">For this tutorial, you'll use separate Azure AD applications for hello calling API app and hello protected API app.</span></span>
8. <span data-ttu-id="2c04f-189">請記下在 hello hello 值**建立應用程式**輸入的方塊中，您將此 AAD 應用程式中查閱 hello Azure 傳統入口網站更新版本。</span><span class="sxs-lookup"><span data-stu-id="2c04f-189">Make a note of hello value that is in hello **Create App** input box; you'll look up this AAD application in hello Azure classic portal later.</span></span>
9. <span data-ttu-id="2c04f-190">按一下 [確定] 。</span><span class="sxs-lookup"><span data-stu-id="2c04f-190">Click **OK**.</span></span>
10. <span data-ttu-id="2c04f-191">在 hello**驗證 / 授權**刀鋒視窗中，按一下 **儲存**。</span><span class="sxs-lookup"><span data-stu-id="2c04f-191">In hello **Authentication / Authorization** blade, click **Save**.</span></span>
    
    ![按一下 [Save] \(儲存)。](./media/app-service-api-dotnet-service-principal-auth/saveauth.png)
    
    <span data-ttu-id="2c04f-193">應用程式服務會建立 Azure Active Directory 應用程式與**登入 URL**和**回覆 URL**自動設定 toohello API 應用程式的 URL。</span><span class="sxs-lookup"><span data-stu-id="2c04f-193">App Service creates an Azure Active Directory application with **Sign-on URL** and **Reply URL** automatically set toohello URL of your API app.</span></span> <span data-ttu-id="2c04f-194">在您 AAD 租用戶 toolog 中的使用者和存取 hello API 應用程式，可讓 hello 第二個值。</span><span class="sxs-lookup"><span data-stu-id="2c04f-194">hello latter value enables users in your AAD tenant toolog in and access hello API app.</span></span>

### <a name="verify-that-hello-api-app-is-protected"></a><span data-ttu-id="2c04f-195">確認該 hello API 應用程式受到保護</span><span class="sxs-lookup"><span data-stu-id="2c04f-195">Verify that hello API app is protected</span></span>
1. <span data-ttu-id="2c04f-196">在瀏覽器中前往 toohello hello API 應用程式 URL: hello 中**API 應用程式**刀鋒視窗中 hello Azure 入口網站中，按一下底下的 hello 連結**URL**。</span><span class="sxs-lookup"><span data-stu-id="2c04f-196">In a browser go toohello URL of hello API app: in hello **API app** blade in hello Azure portal, click hello link under **URL**.</span></span> 
   
    <span data-ttu-id="2c04f-197">您是重新導向的 tooa 登入畫面，因為 tooreach hello API 應用程式不允許未經驗證的要求。</span><span class="sxs-lookup"><span data-stu-id="2c04f-197">You are redirected tooa login screen because unauthenticated requests are not allowed tooreach hello API app.</span></span> 
   
    <span data-ttu-id="2c04f-198">如果您的瀏覽器並移 toohello Swagger UI，您的瀏覽器可能已經登入--在此情況下，開啟 InPrivate 或 Incognito 視窗和移 toohello 的 UI Swagger URL。</span><span class="sxs-lookup"><span data-stu-id="2c04f-198">If your browser does go toohello Swagger UI, your browser might already be logged on -- in that case, open an InPrivate or Incognito window and go toohello Swagger UI URL.</span></span>
2. <span data-ttu-id="2c04f-199">使用 AAD 租用戶中使用者的認證進行登入。</span><span class="sxs-lookup"><span data-stu-id="2c04f-199">Log in with credentials of a user in your AAD tenant.</span></span>
   
   <span data-ttu-id="2c04f-200">當您登入時，hello"建立成功 」 的頁面會顯示 hello 瀏覽器中。</span><span class="sxs-lookup"><span data-stu-id="2c04f-200">When you're logged on, hello "successfully created" page appears in hello browser.</span></span>

## <a name="configure-hello-todolistapi-project-tooacquire-and-send-hello-azure-ad-token"></a><span data-ttu-id="2c04f-201">設定 hello ToDoListAPI 專案 tooacquire 和傳送 hello Azure AD 權杖</span><span class="sxs-lookup"><span data-stu-id="2c04f-201">Configure hello ToDoListAPI project tooacquire and send hello Azure AD token</span></span>
<span data-ttu-id="2c04f-202">本節中您不要 hello 下列工作：</span><span class="sxs-lookup"><span data-stu-id="2c04f-202">In this section you do hello following tasks:</span></span>

* <span data-ttu-id="2c04f-203">加入程式碼 hello 中介層應用程式開發介面應用程式中使用 Azure AD 應用程式認證 tooacquire 語彙基元，並傳送的 HTTP 要求 toohello 資料層應用程式開發介面應用程式。</span><span class="sxs-lookup"><span data-stu-id="2c04f-203">Add code in hello middle tier API app that uses Azure AD application credentials tooacquire a token and send it with HTTP requests toohello data tier API app.</span></span>
* <span data-ttu-id="2c04f-204">從 Azure AD 取得您需要的 hello 認證。</span><span class="sxs-lookup"><span data-stu-id="2c04f-204">Get hello credentials you need from Azure AD.</span></span>
* <span data-ttu-id="2c04f-205">Hello 認證輸入 hello 中介層應用程式開發介面應用程式中的 Azure 應用程式服務執行階段環境設定。</span><span class="sxs-lookup"><span data-stu-id="2c04f-205">Enter hello credentials into Azure App Service runtime environment settings in hello middle tier API app.</span></span> 

### <a name="configure-hello-todolistapi-project-tooacquire-and-send-hello-azure-ad-token"></a><span data-ttu-id="2c04f-206">設定 hello ToDoListAPI 專案 tooacquire 和傳送 hello Azure AD 權杖</span><span class="sxs-lookup"><span data-stu-id="2c04f-206">Configure hello ToDoListAPI project tooacquire and send hello Azure AD token</span></span>
<span data-ttu-id="2c04f-207">請遵循 Visual Studio 中的 hello ToDoListAPI 專案中的變更 hello。</span><span class="sxs-lookup"><span data-stu-id="2c04f-207">Make hello following changes in hello ToDoListAPI project in Visual Studio.</span></span>

1. <span data-ttu-id="2c04f-208">取消所有 hello hello 中的程式碼註解*ServicePrincipal.cs*檔案。</span><span class="sxs-lookup"><span data-stu-id="2c04f-208">Uncomment all of hello code in hello *ServicePrincipal.cs* file.</span></span>
   
    <span data-ttu-id="2c04f-209">這是.NET tooacquire hello Azure AD 持有人權杖中會使用 ADAL 的 hello 程式碼。</span><span class="sxs-lookup"><span data-stu-id="2c04f-209">This is hello code that uses ADAL for .NET tooacquire hello Azure AD bearer token.</span></span>  <span data-ttu-id="2c04f-210">它會使用幾個可在 hello Azure 執行階段環境中設定更新版本的組態值。</span><span class="sxs-lookup"><span data-stu-id="2c04f-210">It uses several configuration values that you'll set in hello Azure runtime environment later.</span></span> <span data-ttu-id="2c04f-211">Hello 程式碼如下：</span><span class="sxs-lookup"><span data-stu-id="2c04f-211">Here's hello code:</span></span> 
   
        public static class ServicePrincipal
        {
            static string authority = ConfigurationManager.AppSettings["ida:Authority"];
            static string clientId = ConfigurationManager.AppSettings["ida:ClientId"];
            static string clientSecret = ConfigurationManager.AppSettings["ida:ClientSecret"];
            static string resource = ConfigurationManager.AppSettings["ida:Resource"];
   
            public static AuthenticationResult GetS2SAccessTokenForProdMSA()
            {
                return GetS2SAccessToken(authority, resource, clientId, clientSecret);
            }
   
            static AuthenticationResult GetS2SAccessToken(string authority, string resource, string clientId, string clientSecret)
            {
                var clientCredential = new ClientCredential(clientId, clientSecret);
                AuthenticationContext context = new AuthenticationContext(authority, false);
                AuthenticationResult authenticationResult = context.AcquireToken(
                    resource,
                    clientCredential);
                return authenticationResult;
            }
        }
   
    <span data-ttu-id="2c04f-212">**注意：**此程式碼需要.NET NuGet 套件 (Microsoft.IdentityModel.Clients.ActiveDirectory)，已安裝在 hello 專案中的 hello ADAL。</span><span class="sxs-lookup"><span data-stu-id="2c04f-212">**Note:** This code requires hello ADAL for .NET NuGet package (Microsoft.IdentityModel.Clients.ActiveDirectory), which is already installed in hello project.</span></span> <span data-ttu-id="2c04f-213">如果您從頭開始建立這個專案，您必須 tooinstall 此封裝。</span><span class="sxs-lookup"><span data-stu-id="2c04f-213">If you were creating this project from scratch, you would have tooinstall this package.</span></span> <span data-ttu-id="2c04f-214">此套件不會自動安裝由 hello API 應用程式的新專案範本。</span><span class="sxs-lookup"><span data-stu-id="2c04f-214">This package is not automatically installed by hello API app new-project template.</span></span>
2. <span data-ttu-id="2c04f-215">在*控制器/ToDoListController*，請取消註解 hello hello 中的程式碼`NewDataAPIClient`將 hello 授權標頭中的 hello tooHTTP 權杖要求方法。</span><span class="sxs-lookup"><span data-stu-id="2c04f-215">In *Controllers/ToDoListController*, uncomment hello code in hello `NewDataAPIClient` method that adds hello token tooHTTP requests in hello authorization header.</span></span>
   
        client.HttpClient.DefaultRequestHeaders.Authorization =
            new AuthenticationHeaderValue("Bearer", ServicePrincipal.GetS2SAccessTokenForProdMSA().AccessToken);
3. <span data-ttu-id="2c04f-216">部署 hello ToDoListAPI 專案。</span><span class="sxs-lookup"><span data-stu-id="2c04f-216">Deploy hello ToDoListAPI project.</span></span> <span data-ttu-id="2c04f-217">(Hello 專案上按一下滑鼠右鍵，然後按一下 **發行 > 發行**。)</span><span class="sxs-lookup"><span data-stu-id="2c04f-217">(Right-click hello project, then click **Publish > Publish**.)</span></span>
   
    <span data-ttu-id="2c04f-218">Visual Studio 部署 hello 專案，並開啟瀏覽器 toohello web 應用程式的基底 URL。</span><span class="sxs-lookup"><span data-stu-id="2c04f-218">Visual Studio deploys hello project and opens a browser toohello web app's base URL.</span></span> <span data-ttu-id="2c04f-219">這會顯示 403 錯誤頁面上，也就是從瀏覽器嘗試 toogo tooa Web API 基底 URL 的一般。</span><span class="sxs-lookup"><span data-stu-id="2c04f-219">This will show a 403 error page, which is normal for an attempt toogo tooa Web API base URL from a browser.</span></span>
4. <span data-ttu-id="2c04f-220">關閉 hello 瀏覽器。</span><span class="sxs-lookup"><span data-stu-id="2c04f-220">Close hello browser.</span></span>

### <a name="get-azure-ad-configuration-values"></a><span data-ttu-id="2c04f-221">取得 Azure AD 設定值</span><span class="sxs-lookup"><span data-stu-id="2c04f-221">Get Azure AD configuration values</span></span>
1. <span data-ttu-id="2c04f-222">在 hello [Azure 傳統入口網站](https://manage.windowsazure.com/)，跳過**Azure Active Directory**。</span><span class="sxs-lookup"><span data-stu-id="2c04f-222">In hello [Azure classic portal](https://manage.windowsazure.com/), go too**Azure Active Directory**.</span></span>
2. <span data-ttu-id="2c04f-223">在 hello**目錄**索引標籤上，按一下您的 AAD 租用戶。</span><span class="sxs-lookup"><span data-stu-id="2c04f-223">On hello **Directory** tab, click your AAD tenant.</span></span>
3. <span data-ttu-id="2c04f-224">按一下**應用程式 > 我公司所擁有的應用程式**，然後按一下hello 核取記號。</span><span class="sxs-lookup"><span data-stu-id="2c04f-224">Click **Applications > Applications my company owns**, and then click hello check mark.</span></span>
4. <span data-ttu-id="2c04f-225">Hello 應用程式清單中按一下 hello hello 時啟用 hello ToDoListDataAPI （資料層） API 的應用程式的驗證為您建立 Azure 的其中一個名稱。</span><span class="sxs-lookup"><span data-stu-id="2c04f-225">In hello list of applications, click hello name of hello one that Azure created for you when you enabled authentication for hello ToDoListDataAPI (data tier) API app.</span></span>
5. <span data-ttu-id="2c04f-226">按一下 hello**設定** 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="2c04f-226">Click hello **Configure** tab.</span></span>
6. <span data-ttu-id="2c04f-227">複製 hello**用戶端識別碼**值，並將其儲存位置，就可以從更新版本。</span><span class="sxs-lookup"><span data-stu-id="2c04f-227">Copy hello **Client ID** value and save it someplace you can get it from later.</span></span> 
7. <span data-ttu-id="2c04f-228">在 hello Azure 傳統入口網站移回 toohello 清單**我公司所擁有的應用程式**，然後按一下您建立 hello 中介層 ToDoListAPI API 應用程式 (不在 hello 上一個教學課程中，建立一個 hello hello AAD 應用程式hello 本教學課程中建立)。</span><span class="sxs-lookup"><span data-stu-id="2c04f-228">In hello Azure classic portal go back toohello list of **Applications my company owns**, and click hello AAD application that you created for hello middle tier ToDoListAPI API app (hello one you created in hello previous tutorial, not hello one you created in this tutorial).</span></span>
8. <span data-ttu-id="2c04f-229">按一下 hello**設定** 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="2c04f-229">Click hello **Configure** tab.</span></span>
9. <span data-ttu-id="2c04f-230">複製 hello**用戶端識別碼**值，並將其儲存位置，就可以從更新版本。</span><span class="sxs-lookup"><span data-stu-id="2c04f-230">Copy hello **Client ID** value and save it someplace you can get it from later.</span></span>
10. <span data-ttu-id="2c04f-231">在下**金鑰**，選取**1 年**從 hello**選取持續時間**下拉式清單。</span><span class="sxs-lookup"><span data-stu-id="2c04f-231">Under **keys**, select **1 year** from hello **Select duration** drop-down list.</span></span>
11. <span data-ttu-id="2c04f-232">按一下 [儲存] 。</span><span class="sxs-lookup"><span data-stu-id="2c04f-232">Click **Save**.</span></span>
    
     ![產生應用程式金鑰](./media/app-service-api-dotnet-service-principal-auth/genkey.png)
12. <span data-ttu-id="2c04f-234">複製 hello 索引鍵值，並將其儲存位置，就可以從更新版本。</span><span class="sxs-lookup"><span data-stu-id="2c04f-234">Copy hello key value and save it someplace you can get it from later.</span></span>
    
     ![複製新的應用程式金鑰](./media/app-service-api-dotnet-service-principal-auth/genkeycopy.png)

### <a name="configure-azure-ad-settings-in-hello-middle-tier-api-apps-runtime-environment"></a><span data-ttu-id="2c04f-236">在 hello 中介層應用程式開發介面應用程式的執行階段環境中設定 Azure AD</span><span class="sxs-lookup"><span data-stu-id="2c04f-236">Configure Azure AD settings in hello middle tier API app's runtime environment</span></span>
1. <span data-ttu-id="2c04f-237">移 toohello [Azure 入口網站](https://portal.azure.com/)，然後瀏覽 toohello **API 應用程式**刀鋒視窗中的 hello API 應用程式裝載 hello TodoListAPI （中介層） 專案。</span><span class="sxs-lookup"><span data-stu-id="2c04f-237">Go toohello [Azure portal](https://portal.azure.com/), and then navigate toohello **API App** blade for hello API app that hosts hello TodoListAPI (middle tier) project.</span></span>
2. <span data-ttu-id="2c04f-238">按一下 [設定] > [應用程式設定]。</span><span class="sxs-lookup"><span data-stu-id="2c04f-238">Click **Settings > Application Settings**.</span></span>
3. <span data-ttu-id="2c04f-239">在 hello**應用程式設定**區段中，加入下列的 hello 索引鍵和值：</span><span class="sxs-lookup"><span data-stu-id="2c04f-239">In hello **App settings** section, add hello following keys and values:</span></span>
   
   | <span data-ttu-id="2c04f-240">**金鑰**</span><span class="sxs-lookup"><span data-stu-id="2c04f-240">**Key**</span></span> | <span data-ttu-id="2c04f-241">ida:Authority</span><span class="sxs-lookup"><span data-stu-id="2c04f-241">ida:Authority</span></span> |
   | --- | --- |
   | <span data-ttu-id="2c04f-242">**值**</span><span class="sxs-lookup"><span data-stu-id="2c04f-242">**Value**</span></span> |<span data-ttu-id="2c04f-243">https://login.microsoftonline.com/{您的 Azure AD 租用戶名稱}</span><span class="sxs-lookup"><span data-stu-id="2c04f-243">https://login.microsoftonline.com/{your Azure AD tenant name}</span></span> |
   | <span data-ttu-id="2c04f-244">**範例**</span><span class="sxs-lookup"><span data-stu-id="2c04f-244">**Example**</span></span> |<span data-ttu-id="2c04f-245">https://login.microsoftonline.com/contoso.onmicrosoft.com</span><span class="sxs-lookup"><span data-stu-id="2c04f-245">https://login.microsoftonline.com/contoso.onmicrosoft.com</span></span> |
   
   | <span data-ttu-id="2c04f-246">**Key**</span><span class="sxs-lookup"><span data-stu-id="2c04f-246">**Key**</span></span> | <span data-ttu-id="2c04f-247">ida:ClientId</span><span class="sxs-lookup"><span data-stu-id="2c04f-247">ida:ClientId</span></span> |
   | --- | --- |
   | <span data-ttu-id="2c04f-248">**值**</span><span class="sxs-lookup"><span data-stu-id="2c04f-248">**Value**</span></span> |<span data-ttu-id="2c04f-249">用戶端識別碼 hello 呼叫應用程式 （中介層-ToDoListAPI）</span><span class="sxs-lookup"><span data-stu-id="2c04f-249">Client ID of hello calling application (middle tier - ToDoListAPI)</span></span> |
   | <span data-ttu-id="2c04f-250">**範例**</span><span class="sxs-lookup"><span data-stu-id="2c04f-250">**Example**</span></span> |<span data-ttu-id="2c04f-251">960adec2-b74a-484a-960adec2-b74a-484a</span><span class="sxs-lookup"><span data-stu-id="2c04f-251">960adec2-b74a-484a-960adec2-b74a-484a</span></span> |
   
   | <span data-ttu-id="2c04f-252">**金鑰**</span><span class="sxs-lookup"><span data-stu-id="2c04f-252">**Key**</span></span> | <span data-ttu-id="2c04f-253">ida:ClientSecret</span><span class="sxs-lookup"><span data-stu-id="2c04f-253">ida:ClientSecret</span></span> |
   | --- | --- |
   | <span data-ttu-id="2c04f-254">**值**</span><span class="sxs-lookup"><span data-stu-id="2c04f-254">**Value**</span></span> |<span data-ttu-id="2c04f-255">Hello 呼叫應用程式 （中介層-ToDoListAPI） 的應用程式金鑰</span><span class="sxs-lookup"><span data-stu-id="2c04f-255">App key of hello calling application (middle tier - ToDoListAPI)</span></span> |
   | <span data-ttu-id="2c04f-256">**範例**</span><span class="sxs-lookup"><span data-stu-id="2c04f-256">**Example**</span></span> |<span data-ttu-id="2c04f-257">e65e8fc9-5f6b-48e8-e65e8fc9-5f6b-48e8</span><span class="sxs-lookup"><span data-stu-id="2c04f-257">e65e8fc9-5f6b-48e8-e65e8fc9-5f6b-48e8</span></span> |
   
   | <span data-ttu-id="2c04f-258">**金鑰**</span><span class="sxs-lookup"><span data-stu-id="2c04f-258">**Key**</span></span> | <span data-ttu-id="2c04f-259">ida:Resource</span><span class="sxs-lookup"><span data-stu-id="2c04f-259">ida:Resource</span></span> |
   | --- | --- |
   | <span data-ttu-id="2c04f-260">**值**</span><span class="sxs-lookup"><span data-stu-id="2c04f-260">**Value**</span></span> |<span data-ttu-id="2c04f-261">Hello 呼叫應用程式的用戶端識別碼 （資料層-ToDoListDataAPI）</span><span class="sxs-lookup"><span data-stu-id="2c04f-261">Client ID of hello called application (data tier - ToDoListDataAPI)</span></span> |
   | <span data-ttu-id="2c04f-262">**範例**</span><span class="sxs-lookup"><span data-stu-id="2c04f-262">**Example**</span></span> |<span data-ttu-id="2c04f-263">e65e8fc9-5f6b-48e8-e65e8fc9-5f6b-48e8</span><span class="sxs-lookup"><span data-stu-id="2c04f-263">e65e8fc9-5f6b-48e8-e65e8fc9-5f6b-48e8</span></span> |
   
    <span data-ttu-id="2c04f-264">**請注意**： 的`ida:Resource`，請確定您使用呼叫應用程式的 hello**用戶端識別碼**而非其**應用程式識別碼 URI**。</span><span class="sxs-lookup"><span data-stu-id="2c04f-264">**Note**: For `ida:Resource`, make sure you use hello called application's **client ID** and not its **App ID URI**.</span></span>
   
    <span data-ttu-id="2c04f-265">`ida:ClientId`和`ida:Resource`不同本教學課程中的值，因為您正在使用分隔 Azure AD applicaations hello 中介層和資料層。</span><span class="sxs-lookup"><span data-stu-id="2c04f-265">`ida:ClientId` and `ida:Resource` are different values for this tutorial because you're using separate Azure AD applicaations for hello middle tier and data tier.</span></span> <span data-ttu-id="2c04f-266">如果您使用單一 Azure AD 應用程式呼叫 API 應用程式和 hello hello 受保護的應用程式開發介面應用程式，您會使用相同的值中的 hello`ida:ClientId`和`ida:Resource`。</span><span class="sxs-lookup"><span data-stu-id="2c04f-266">If you were using a single Azure AD application for hello calling API app and hello protected API app, you would use hello same value in both `ida:ClientId` and `ida:Resource`.</span></span>
   
    <span data-ttu-id="2c04f-267">hello 程式碼會使用 ConfigurationManager tooget 這些值，因此它們無法在 hello 專案的 Web.config 檔案或 hello Azure 執行階段環境中儲存。</span><span class="sxs-lookup"><span data-stu-id="2c04f-267">hello code uses ConfigurationManager tooget these values, so they could be stored in hello project's Web.config file or in hello Azure runtime environment.</span></span> <span data-ttu-id="2c04f-268">當 ASP.NET 應用程式在 Azure App Service 中執行時，環境設定會自動覆寫 Web.config 的設定。環境設定通常是[更安全方式 toostore 機密資訊比較 tooa Web.config 檔案](http://www.asp.net/identity/overview/features-api/best-practices-for-deploying-passwords-and-other-sensitive-data-to-aspnet-and-azure)。</span><span class="sxs-lookup"><span data-stu-id="2c04f-268">While an ASP.NET application is running in Azure App Service, environment settings automatically override settings from Web.config. Environment settings are generally a [more secure way toostore sensitive information compared tooa Web.config file](http://www.asp.net/identity/overview/features-api/best-practices-for-deploying-passwords-and-other-sensitive-data-to-aspnet-and-azure).</span></span>
4. <span data-ttu-id="2c04f-269">按一下 [儲存] 。</span><span class="sxs-lookup"><span data-stu-id="2c04f-269">Click **Save**.</span></span>
   
    ![按一下 [Save] \(儲存)。](./media/app-service-api-dotnet-service-principal-auth/appsettings.png)

### <a name="test-hello-application"></a><span data-ttu-id="2c04f-271">測試 hello 應用程式</span><span class="sxs-lookup"><span data-stu-id="2c04f-271">Test hello application</span></span>
1. <span data-ttu-id="2c04f-272">在瀏覽器移 toohello hello AngularJS 前端 web 應用程式的 HTTPS URL。</span><span class="sxs-lookup"><span data-stu-id="2c04f-272">In a browser go toohello HTTPS URL of hello AngularJS front end web app.</span></span>
2. <span data-ttu-id="2c04f-273">按一下 hello **tooDo 清單** 索引標籤並登入 Azure AD 租用戶中使用者的認證。</span><span class="sxs-lookup"><span data-stu-id="2c04f-273">Click hello **tooDo List** tab and log in with credentials for a user in your Azure AD tenant.</span></span> 
3. <span data-ttu-id="2c04f-274">加入待辦項目 tooverify 正在 hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="2c04f-274">Add to-do items tooverify that hello application is working.</span></span>
   
    ![tooDo 清單頁面](./media/app-service-api-dotnet-service-principal-auth/mvchome.png)
   
    <span data-ttu-id="2c04f-276">如果 hello 應用程式不會在如預期般運作，請仔細檢查所有您輸入 hello Azure 入口網站中的 hello 設定。</span><span class="sxs-lookup"><span data-stu-id="2c04f-276">If hello application doesn't work as expected, double-check all of hello settings you entered in hello Azure portal.</span></span> <span data-ttu-id="2c04f-277">如果所有的 hello 設定出現 toobe 正確，請參閱 hello[疑難排解](#troubleshooting)稍後在本教學課程 > 一節。</span><span class="sxs-lookup"><span data-stu-id="2c04f-277">If all of hello settings appear toobe correct, see hello [Troubleshooting](#troubleshooting) section later in this tutorial.</span></span>

## <a name="protect-hello-api-app-from-browser-access"></a><span data-ttu-id="2c04f-278">防止瀏覽器存取的 hello API 應用程式</span><span class="sxs-lookup"><span data-stu-id="2c04f-278">Protect hello API app from browser access</span></span>
<span data-ttu-id="2c04f-279">在此教學課程中，您建立個別 hello ToDoListDataAPI （資料層） API 應用程式的 Azure AD 應用程式。</span><span class="sxs-lookup"><span data-stu-id="2c04f-279">For this tutorial you created a separate Azure AD application for hello ToDoListDataAPI (data tier) API app.</span></span> <span data-ttu-id="2c04f-280">如您所見，當應用程式服務建立 AAD 應用程式，它會設定 hello AAD 應用程式上啟用使用者 toogo toohello API 應用程式的 URL 在瀏覽器和記錄檔中的方式。</span><span class="sxs-lookup"><span data-stu-id="2c04f-280">As you've seen, when App Service creates an AAD application, it configures hello AAD application in a way that enables a user toogo toohello API app's URL in a browser and log on.</span></span> <span data-ttu-id="2c04f-281">這表示這是可能的 Azure AD 租用戶中，不只是服務主體使用者，tooaccess hello 應用程式開發介面。</span><span class="sxs-lookup"><span data-stu-id="2c04f-281">That means it's possible for an end user in your Azure AD tenant, not just a service principal, tooaccess hello API.</span></span> 

<span data-ttu-id="2c04f-282">如果您想 tooprevent 瀏覽器存取，且不受 hello 中撰寫任何程式碼保護 API 應用程式，您可以變更 hello**回覆 URL** hello AAD 應用程式中，讓它與 hello API 應用程式的不同基底 URL。</span><span class="sxs-lookup"><span data-stu-id="2c04f-282">If you want tooprevent browser access without writing any code in hello protected API app, you can change hello **Reply URL** in hello AAD application so that it's different from hello API app's base URL.</span></span> 

### <a name="disable-browser-access"></a><span data-ttu-id="2c04f-283">停用瀏覽器存取</span><span class="sxs-lookup"><span data-stu-id="2c04f-283">Disable browser access</span></span>
1. <span data-ttu-id="2c04f-284">Hello 傳統入口網站中的**設定**hello AAD 應用程式所建立的 hello TodoListService 索引標籤上，變更在 hello hello 值**回覆 URL**欄位，讓它是有效的 URL，但不是 hello API 的應用程式URL。</span><span class="sxs-lookup"><span data-stu-id="2c04f-284">In hello classic portal's **Configure** tab for hello AAD application that was created for hello TodoListService, change hello value in hello **Reply URL** field so that it is a valid URL but not hello API app's URL.</span></span>
2. <span data-ttu-id="2c04f-285">按一下 [儲存] 。</span><span class="sxs-lookup"><span data-stu-id="2c04f-285">Click **Save**.</span></span>

### <a name="verify-browser-access-no-longer-works"></a><span data-ttu-id="2c04f-286">確認瀏覽器存取無法再運作</span><span class="sxs-lookup"><span data-stu-id="2c04f-286">Verify browser access no longer works</span></span>
<span data-ttu-id="2c04f-287">您稍早驗證，您可以移 toohello API 應用程式 URL 從瀏覽器以個別使用者的認證登入。</span><span class="sxs-lookup"><span data-stu-id="2c04f-287">Earlier you verified that you can go toohello API app URL from a browser by logging on with an individual user's credentials.</span></span> <span data-ttu-id="2c04f-288">在本節中，您將要確認此動作已不可行。</span><span class="sxs-lookup"><span data-stu-id="2c04f-288">In this section, you verify that this is no longer possible.</span></span> 

1. <span data-ttu-id="2c04f-289">在新的瀏覽器視窗中，會再次 toohello hello API 應用程式 URL。</span><span class="sxs-lookup"><span data-stu-id="2c04f-289">In a new browser window, go toohello URL of hello API app again.</span></span>
2. <span data-ttu-id="2c04f-290">記錄檔中時，提示 toodo。</span><span class="sxs-lookup"><span data-stu-id="2c04f-290">Log in when prompted toodo so.</span></span>
3. <span data-ttu-id="2c04f-291">登入成功，但會導致 tooan 錯誤頁面。</span><span class="sxs-lookup"><span data-stu-id="2c04f-291">Login succeeds but leads tooan error page.</span></span>
   
    <span data-ttu-id="2c04f-292">您已設定 hello AAD 應用程式，所以 hello AAD 租用戶中的使用者無法登入，並從瀏覽器存取 hello API。</span><span class="sxs-lookup"><span data-stu-id="2c04f-292">You've configured hello AAD app so that users in hello AAD tenant cannot log in and access hello API from a browser.</span></span> <span data-ttu-id="2c04f-293">您仍然可以使用服務主體 token，您可以確認進入 toohello web 應用程式的 URL，並加入更多待辦項目，以存取 hello API 應用程式。</span><span class="sxs-lookup"><span data-stu-id="2c04f-293">You can still access hello API app by using a service principal token, which you can verify by going toohello web app's URL and adding more to-do items.</span></span>

## <a name="restrict-access-tooa-particular-service-principal"></a><span data-ttu-id="2c04f-294">限制存取 tooa 特定的服務主體</span><span class="sxs-lookup"><span data-stu-id="2c04f-294">Restrict access tooa particular service principal</span></span>
<span data-ttu-id="2c04f-295">以滑鼠右鍵，可以為使用者取得權杖的任何呼叫端，或在 Azure AD 租用戶中的服務主體可以呼叫 hello TodoListDataAPI （資料層） API 應用程式。</span><span class="sxs-lookup"><span data-stu-id="2c04f-295">Right now, any caller that can get a token for a user or service principal in your Azure AD tenant can call hello TodoListDataAPI (data tier) API app.</span></span> <span data-ttu-id="2c04f-296">您可能想 toomake 確定該 hello 資料層應用程式開發介面應用程式只接受呼叫從 hello TodoListAPI （中介層） 應用程式開發介面應用程式，而且是從特定的服務主體。</span><span class="sxs-lookup"><span data-stu-id="2c04f-296">You might want toomake sure that hello data tier API app only accepts calls from hello TodoListAPI (middle tier) API app, and only from a particular service principal.</span></span> 

<span data-ttu-id="2c04f-297">您可以加入程式碼 toovalidate hello，以便將這些限制`appid`和`objectidentifier`宣告上的連入呼叫。</span><span class="sxs-lookup"><span data-stu-id="2c04f-297">You can add these restrictions by adding code toovalidate hello `appid` and `objectidentifier` claims on incoming calls.</span></span>

<span data-ttu-id="2c04f-298">本教學課程中，您將會驗證應用程式識別碼，並直接在控制器動作中的服務主體 ID 的 hello 程式碼。</span><span class="sxs-lookup"><span data-stu-id="2c04f-298">For this tutorial you put hello code that validates app ID and service principal ID directly in your controller actions.</span></span>  <span data-ttu-id="2c04f-299">替代方式為 toouse 自訂`Authorize`屬性或 toodo 這項驗證在您啟動序列 （例如 OWIN 中介軟體）。</span><span class="sxs-lookup"><span data-stu-id="2c04f-299">Alternatives are toouse a custom `Authorize` attribute or toodo this validation in your startup sequences (e.g. OWIN middleware).</span></span> <span data-ttu-id="2c04f-300">如需 hello 後面的範例，請參閱[此範例應用程式](https://github.com/mohitsriv/EasyAuthMultiTierSample/blob/master/MyDashDataAPI/Startup.cs)。</span><span class="sxs-lookup"><span data-stu-id="2c04f-300">For an example of hello latter, see [this sample application](https://github.com/mohitsriv/EasyAuthMultiTierSample/blob/master/MyDashDataAPI/Startup.cs).</span></span> 

<span data-ttu-id="2c04f-301">請遵循變更 toohello TodoListDataAPI 專案 hello。</span><span class="sxs-lookup"><span data-stu-id="2c04f-301">Make hello following changes toohello TodoListDataAPI project.</span></span>

1. <span data-ttu-id="2c04f-302">開啟 hello *Controllers/TodoListController.cs*檔案。</span><span class="sxs-lookup"><span data-stu-id="2c04f-302">Open hello *Controllers/TodoListController.cs* file.</span></span>
2. <span data-ttu-id="2c04f-303">設定的 hello 行取消註解`trustedCallerClientId`和`trustedCallerServicePrincipalId`。</span><span class="sxs-lookup"><span data-stu-id="2c04f-303">Uncomment hello lines that set `trustedCallerClientId` and `trustedCallerServicePrincipalId`.</span></span>
   
        private static string trustedCallerClientId = ConfigurationManager.AppSettings["todo:TrustedCallerClientId"];
        private static string trustedCallerServicePrincipalId = ConfigurationManager.AppSettings["todo:TrustedCallerServicePrincipalId"];
3. <span data-ttu-id="2c04f-304">取消註解 hello hello CheckCallerId 方法中的程式碼。</span><span class="sxs-lookup"><span data-stu-id="2c04f-304">Uncomment hello code in hello CheckCallerId method.</span></span> <span data-ttu-id="2c04f-305">這個方法是在 hello 開始 hello 控制器中的每個動作方法的呼叫。</span><span class="sxs-lookup"><span data-stu-id="2c04f-305">This method is called at hello start of every action method in hello controller.</span></span> 
   
        private static void CheckCallerId()
        {
            string currentCallerClientId = ClaimsPrincipal.Current.FindFirst("appid").Value;
            string currentCallerServicePrincipalId = ClaimsPrincipal.Current.FindFirst("http://schemas.microsoft.com/identity/claims/objectidentifier").Value;
            if (currentCallerClientId != trustedCallerClientId || currentCallerServicePrincipalId != trustedCallerServicePrincipalId)
            {
                throw new HttpResponseException(new HttpResponseMessage { StatusCode = HttpStatusCode.Unauthorized, ReasonPhrase = "hello appID or service principal ID is not hello expected value." });
            }
        }
4. <span data-ttu-id="2c04f-306">重新部署 hello ToDoListDataAPI 專案 tooAzure 應用程式服務。</span><span class="sxs-lookup"><span data-stu-id="2c04f-306">Redeploy hello ToDoListDataAPI project tooAzure App Service.</span></span>
5. <span data-ttu-id="2c04f-307">在瀏覽器中前往 toohello AngularJS 前端 web 應用程式的 HTTPS URL，並在 hello 首頁上，按一下 [hello **tooDo 清單**] 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="2c04f-307">In your browser, go toohello AngularJS front end web app's HTTPS URL, and in hello home page click hello **tooDo List** tab.</span></span>
   
    <span data-ttu-id="2c04f-308">hello 應用程式不會運作，因為回 toohello 結尾的呼叫失敗。</span><span class="sxs-lookup"><span data-stu-id="2c04f-308">hello application doesn't work because calls toohello back end are failing.</span></span> <span data-ttu-id="2c04f-309">hello 新的程式碼會檢查實際 appid 和 objectidentifier，但它還沒有 hello 正確值 toocheck 針對它們。</span><span class="sxs-lookup"><span data-stu-id="2c04f-309">hello new code is checking actual appid and objectidentifier but it doesn't yet have hello correct values toocheck them against.</span></span> <span data-ttu-id="2c04f-310">hello 瀏覽器開發人員工具主控台會報告該 hello 伺服器傳回 HTTP 401 錯誤。</span><span class="sxs-lookup"><span data-stu-id="2c04f-310">hello browser Developer Tools Console reports that hello server is returning an HTTP 401 error.</span></span>
   
    ![開發人員工具主控台中發生錯誤](./media/app-service-api-dotnet-service-principal-auth/webapperror.png)
   
    <span data-ttu-id="2c04f-312">Hello 步驟中，您會設定 hello 預期的值。</span><span class="sxs-lookup"><span data-stu-id="2c04f-312">In hello following steps you configure hello expected values.</span></span>
6. <span data-ttu-id="2c04f-313">使用 Azure AD PowerShell 時，取得 hello 值 hello 服務主體的 hello hello TodoListWebApp 專案建立的 Azure AD 應用程式。</span><span class="sxs-lookup"><span data-stu-id="2c04f-313">Using Azure AD PowerShell, get hello value of hello service principal for hello Azure AD application that you created for hello TodoListWebApp project.</span></span>
   
    <span data-ttu-id="2c04f-314">a.</span><span class="sxs-lookup"><span data-stu-id="2c04f-314">a.</span></span> <span data-ttu-id="2c04f-315">如需有關指示 tooinstall Azure PowerShell 及連接 tooyour 訂用帳戶，請參閱[使用 Azure PowerShell 的 Azure Resource Manager](../powershell-azure-resource-manager.md)。</span><span class="sxs-lookup"><span data-stu-id="2c04f-315">For instructions on how tooinstall Azure PowerShell and connect tooyour subscription, see [Using Azure PowerShell with Azure Resource Manager](../powershell-azure-resource-manager.md).</span></span>
   
    <span data-ttu-id="2c04f-316">b.</span><span class="sxs-lookup"><span data-stu-id="2c04f-316">b.</span></span> <span data-ttu-id="2c04f-317">服務主體清單 tooget 執行 hello`Login-AzureRmAccount`命令，然後 hello`Get-AzureRmADServicePrincipal`命令。</span><span class="sxs-lookup"><span data-stu-id="2c04f-317">tooget a list of service principals, execute hello `Login-AzureRmAccount` command and then hello `Get-AzureRmADServicePrincipal` command.</span></span>
   
    <span data-ttu-id="2c04f-318">c.</span><span class="sxs-lookup"><span data-stu-id="2c04f-318">c.</span></span> <span data-ttu-id="2c04f-319">找到 hello objectid hello TodoListAPI 應用程式的服務主體，並將它儲存在您可以從複製稍後的位置。</span><span class="sxs-lookup"><span data-stu-id="2c04f-319">Find hello objectid for hello service principal of hello TodoListAPI application, and save it in a location you can copy from later.</span></span>
7. <span data-ttu-id="2c04f-320">在 hello Azure 入口網站，瀏覽 toohello hello API 應用程式部署至 hello ToDoListDataAPI 專案的應用程式開發介面應用程式刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="2c04f-320">In hello Azure portal, navigate toohello API app blade for hello API app that you deployed hello ToDoListDataAPI project to.</span></span>
8. <span data-ttu-id="2c04f-321">按一下 [設定] > [應用程式設定]。</span><span class="sxs-lookup"><span data-stu-id="2c04f-321">Click **Settings > Application settings**.</span></span>
9. <span data-ttu-id="2c04f-322">在 hello**應用程式設定**區段中，加入下列的 hello 索引鍵和值：</span><span class="sxs-lookup"><span data-stu-id="2c04f-322">In hello **App settings** section, add hello following keys and values:</span></span>
   
   | <span data-ttu-id="2c04f-323">**金鑰**</span><span class="sxs-lookup"><span data-stu-id="2c04f-323">**Key**</span></span> | <span data-ttu-id="2c04f-324">todo:TrustedCallerServicePrincipalId</span><span class="sxs-lookup"><span data-stu-id="2c04f-324">todo:TrustedCallerServicePrincipalId</span></span> |
   | --- | --- |
   | <span data-ttu-id="2c04f-325">**值**</span><span class="sxs-lookup"><span data-stu-id="2c04f-325">**Value**</span></span> |<span data-ttu-id="2c04f-326">呼叫端應用程式的服務主體識別碼</span><span class="sxs-lookup"><span data-stu-id="2c04f-326">Service principal id of calling application</span></span> |
   | <span data-ttu-id="2c04f-327">**範例**</span><span class="sxs-lookup"><span data-stu-id="2c04f-327">**Example**</span></span> |<span data-ttu-id="2c04f-328">4f4a94a4-6f0d-4072-4f4a94a4-6f0d-4072</span><span class="sxs-lookup"><span data-stu-id="2c04f-328">4f4a94a4-6f0d-4072-4f4a94a4-6f0d-4072</span></span> |
   
   | <span data-ttu-id="2c04f-329">**金鑰**</span><span class="sxs-lookup"><span data-stu-id="2c04f-329">**Key**</span></span> | <span data-ttu-id="2c04f-330">todo:TrustedCallerClientId</span><span class="sxs-lookup"><span data-stu-id="2c04f-330">todo:TrustedCallerClientId</span></span> |
   | --- | --- |
   | <span data-ttu-id="2c04f-331">**值**</span><span class="sxs-lookup"><span data-stu-id="2c04f-331">**Value**</span></span> |<span data-ttu-id="2c04f-332">呼叫應用程式-複製從 hello TodoListAPI Azure AD 應用程式的用戶端識別碼</span><span class="sxs-lookup"><span data-stu-id="2c04f-332">Client ID of calling application - copied from hello TodoListAPI Azure AD application</span></span> |
   | <span data-ttu-id="2c04f-333">**範例**</span><span class="sxs-lookup"><span data-stu-id="2c04f-333">**Example**</span></span> |<span data-ttu-id="2c04f-334">960adec2-b74a-484a-960adec2-b74a-484a</span><span class="sxs-lookup"><span data-stu-id="2c04f-334">960adec2-b74a-484a-960adec2-b74a-484a</span></span> |
10. <span data-ttu-id="2c04f-335">按一下 [儲存] 。</span><span class="sxs-lookup"><span data-stu-id="2c04f-335">Click **Save**.</span></span>
    
     ![按一下 [Save] \(儲存)。](./media/app-service-api-dotnet-service-principal-auth/trustedcaller.png)
11. <span data-ttu-id="2c04f-337">在瀏覽器中傳回 toohello web 應用程式的 URL，然後在 hello 首頁上，按一下 hello **tooDo 清單** 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="2c04f-337">In your browser, return toohello web app's URL, and in hello home page click hello **tooDo List** tab.</span></span>
    
     <span data-ttu-id="2c04f-338">此時間 hello 應用程式可以正常運作因為 hello 信任的呼叫端應用程式識別碼和服務主體識別碼 hello 預期的值。</span><span class="sxs-lookup"><span data-stu-id="2c04f-338">This time hello application works as expected because hello trusted caller app ID and service principal ID are hello expected values.</span></span>
    
     ![tooDo 清單頁面](./media/app-service-api-dotnet-service-principal-auth/mvchome.png)

## <a name="building-hello-projects-from-scratch"></a><span data-ttu-id="2c04f-340">建置從頭 hello 專案</span><span class="sxs-lookup"><span data-stu-id="2c04f-340">Building hello projects from scratch</span></span>
<span data-ttu-id="2c04f-341">hello 兩個 Web API 專案所建立的 hello **Azure API 應用程式**專案範本和取代 hello 預設值的控制站與 ToDoList 控制站。</span><span class="sxs-lookup"><span data-stu-id="2c04f-341">hello two Web API projects were created by using hello **Azure API App** project template and replacing hello default Values controller with a ToDoList controller.</span></span> <span data-ttu-id="2c04f-342">取得 Azure AD 服務主體語彙基元 hello ToDoListAPI 專案中的，hello [Active Directory 驗證程式庫 (ADAL) for.NET](https://www.nuget.org/packages/Microsoft.IdentityModel.Clients.ActiveDirectory/)已安裝 NuGet 套件。</span><span class="sxs-lookup"><span data-stu-id="2c04f-342">For acquiring Azure AD service principal tokens in hello ToDoListAPI project, hello [Active Directory Authentication Library (ADAL) for .NET](https://www.nuget.org/packages/Microsoft.IdentityModel.Clients.ActiveDirectory/) NuGet package was installed.</span></span>

<span data-ttu-id="2c04f-343">如需太建立 AngularJS 單一頁面應用程式類似 ToDoListAngular Web API 後端，請參閱[手上實驗室： 建置單一頁面應用程式 (SPA)，使用 ASP.NET Web API 和 Angular.js](http://www.asp.net/web-api/overview/getting-started-with-aspnet-web-api/build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs)。</span><span class="sxs-lookup"><span data-stu-id="2c04f-343">For information about how too create an AngularJS single-page application with a Web API back end like ToDoListAngular, see  [Hands On Lab: Build a Single Page Application (SPA) with ASP.NET Web API and Angular.js](http://www.asp.net/web-api/overview/getting-started-with-aspnet-web-api/build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs).</span></span> <span data-ttu-id="2c04f-344">如需有關資訊 tooadd Azure AD 驗證程式碼，請參閱[保護 AngularJS 單一頁面應用程式與 Azure AD](../active-directory/active-directory-devquickstarts-angular.md)。</span><span class="sxs-lookup"><span data-stu-id="2c04f-344">For information about how tooadd Azure AD authentication code, see [Securing AngularJS Single Page Apps with Azure AD](../active-directory/active-directory-devquickstarts-angular.md).</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="2c04f-345">疑難排解</span><span class="sxs-lookup"><span data-stu-id="2c04f-345">Troubleshooting</span></span>
[!INCLUDE [troubleshooting](../../includes/app-service-api-auth-troubleshooting.md)]

* <span data-ttu-id="2c04f-346">請確定不要混淆 ToDoListAPI (中介層) 和 ToDoListDataAPI (資料層)。</span><span class="sxs-lookup"><span data-stu-id="2c04f-346">Make sure that you don't confuse ToDoListAPI (middle tier) and ToDoListDataAPI (data tier).</span></span> <span data-ttu-id="2c04f-347">例如，本教學課程中您要加入驗證 toohello 資料層應用程式開發介面應用程式， **hello 應用程式金鑰必須來自 hello hello 中介層應用程式開發介面應用程式所建立的 Azure AD 應用程式，但**。</span><span class="sxs-lookup"><span data-stu-id="2c04f-347">For example, in this tutorial you add authentication toohello data tier API app, **but hello app key must come from hello Azure AD application that you created for hello middle tier API app**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="2c04f-348">後續步驟</span><span class="sxs-lookup"><span data-stu-id="2c04f-348">Next steps</span></span>
<span data-ttu-id="2c04f-349">這是 hello hello API Apps 數列中的最後一個教學課程。</span><span class="sxs-lookup"><span data-stu-id="2c04f-349">This is hello last tutorial in hello API Apps series.</span></span> 

<span data-ttu-id="2c04f-350">如需 Azure Active Directory 的詳細資訊，請參閱下列資源的 hello。</span><span class="sxs-lookup"><span data-stu-id="2c04f-350">For more information about Azure Active Directory, see hello following resources.</span></span>

* [<span data-ttu-id="2c04f-351">Azure AD 開發人員指南</span><span class="sxs-lookup"><span data-stu-id="2c04f-351">Azure AD developers' guide</span></span>](http://aka.ms/aaddev)
* [<span data-ttu-id="2c04f-352">Azure AD 案例</span><span class="sxs-lookup"><span data-stu-id="2c04f-352">Azure AD scenarios</span></span>](http://aka.ms/aadscenarios)
* [<span data-ttu-id="2c04f-353">Azure AD 範例</span><span class="sxs-lookup"><span data-stu-id="2c04f-353">Azure AD samples</span></span>](http://aka.ms/aadsamples)
  
    <span data-ttu-id="2c04f-354">hello [WebApp-WebAPI-OAuth2-[appidentity]-DotNet](http://github.com/AzureADSamples/WebApp-WebAPI-OAuth2-AppIdentity-DotNet)範例是類似 toowhat 會顯示在本教學課程中，但不會使用應用程式服務驗證。</span><span class="sxs-lookup"><span data-stu-id="2c04f-354">hello [WebApp-WebAPI-OAuth2-AppIdentity-DotNet](http://github.com/AzureADSamples/WebApp-WebAPI-OAuth2-AppIdentity-DotNet) sample is similar toowhat is shown in this tutorial, but without using App Service authentication.</span></span>

<span data-ttu-id="2c04f-355">如需其他方式 toodeploy Visual Studio 專案 tooAPI 應用程式，使用 Visual Studio 或[自動化部署](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/continuous-integration-and-continuous-delivery)從[原始檔控制系統](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/source-control)，請參閱[如何 toodeployAzure App Service 應用程式](../app-service-web/web-sites-deploy.md)。</span><span class="sxs-lookup"><span data-stu-id="2c04f-355">For information about other ways toodeploy Visual Studio projects tooAPI apps, by using Visual Studio or by [automating deployment](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/continuous-integration-and-continuous-delivery) from a [source control system](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/source-control), see [How toodeploy an Azure App Service app](../app-service-web/web-sites-deploy.md).</span></span>

