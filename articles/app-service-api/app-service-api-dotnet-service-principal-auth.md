---
title: "Azure App Service 中 API Apps 的服務主體驗證 | Microsoft Docs"
description: "深入了解如何保護服務對服務案例的 Azure App Service 的 API 應用程式。"
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
ms.openlocfilehash: 95653287546bbe358111ed16af0c30a53caff2b5
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="service-principal-authentication-for-api-apps-in-azure-app-service"></a><span data-ttu-id="c2899-103">在 Azure App Service 中 API Apps 的服務主體驗證</span><span class="sxs-lookup"><span data-stu-id="c2899-103">Service principal authentication for API Apps in Azure App Service</span></span>
## <a name="overview"></a><span data-ttu-id="c2899-104">概觀</span><span class="sxs-lookup"><span data-stu-id="c2899-104">Overview</span></span>
<span data-ttu-id="c2899-105">這篇文章說明如何使用 App Service 驗證以「內部」  存取 API 應用程式。</span><span class="sxs-lookup"><span data-stu-id="c2899-105">This article explains how to use App Service authentication for *internal* access to API apps.</span></span> <span data-ttu-id="c2899-106">內部案例是您具有只想要讓您自己的應用程式程式碼使用的 API 應用程式。</span><span class="sxs-lookup"><span data-stu-id="c2899-106">An internal scenario is where you have an API app that you want to be consumable only by your own application code.</span></span> <span data-ttu-id="c2899-107">在 App Service 中實作這種案例的建議方法是使用 Azure AD 保護被呼叫的 API 應用程式。</span><span class="sxs-lookup"><span data-stu-id="c2899-107">The recommended way to implement this scenario in App Service is to use Azure AD to protect the called API app.</span></span> <span data-ttu-id="c2899-108">您可以藉由提供應用程式身分識別 (服務主體) 認證，使用您從 Azure AD 取得的持有人權杖，呼叫受保護的 API 應用程式。</span><span class="sxs-lookup"><span data-stu-id="c2899-108">You call the protected API app with a bearer token that you get from Azure AD by providing application identity (service principal) credentials.</span></span> <span data-ttu-id="c2899-109">如需使用 Azure AD 的替代方案，請參閱 **Azure App Service 驗證概觀** 的 [服務對服務驗證](../app-service/app-service-authentication-overview.md#service-to-service-authentication)一節。</span><span class="sxs-lookup"><span data-stu-id="c2899-109">For alternatives to using Azure AD, see the **Service-to-service authentication** section of the [Azure App Service authentication overview](../app-service/app-service-authentication-overview.md#service-to-service-authentication).</span></span>

<span data-ttu-id="c2899-110">在本文中，您將了解：</span><span class="sxs-lookup"><span data-stu-id="c2899-110">In this article, you'll learn:</span></span>

* <span data-ttu-id="c2899-111">如何使用 Azure Active Directory (Azure AD) 防止未經驗證存取 API 應用程式。</span><span class="sxs-lookup"><span data-stu-id="c2899-111">How to use Azure Active Directory (Azure AD) to protect an API app from unauthenticated access.</span></span>
* <span data-ttu-id="c2899-112">如何使用 Azure AD 服務主體 (應用程式身分識別) 認證，從 API 應用程式、Web 應用程式或行動應用程式取用受保護的 API 應用程式。</span><span class="sxs-lookup"><span data-stu-id="c2899-112">How to consume a protected API app from an API app, web app, or mobile app by using Azure AD service principal (app identity) credentials.</span></span> <span data-ttu-id="c2899-113">如需如何從邏輯應用程式取用的詳細資訊，請參閱 [將您裝載在 App Service 上的自訂 API 與邏輯應用程式一起使用](../logic-apps/logic-apps-custom-hosted-api.md)。</span><span class="sxs-lookup"><span data-stu-id="c2899-113">For information about how to consume from a logic app, see [Using your custom API hosted on App Service with Logic apps](../logic-apps/logic-apps-custom-hosted-api.md).</span></span>
* <span data-ttu-id="c2899-114">如何確保登入的使用者不能從瀏覽器呼叫受保護的 API 應用程式。</span><span class="sxs-lookup"><span data-stu-id="c2899-114">How to make sure that the protected API app can't be called from a browser by logged on users.</span></span>
* <span data-ttu-id="c2899-115">如何確保只能由特定 Azure AD 服務主體呼叫受保護的 API 應用程式。</span><span class="sxs-lookup"><span data-stu-id="c2899-115">How to make sure that the protected API app can only be called by a specific Azure AD service principal.</span></span>

<span data-ttu-id="c2899-116">本文包含兩個部分：</span><span class="sxs-lookup"><span data-stu-id="c2899-116">The article contains two sections:</span></span>

* <span data-ttu-id="c2899-117">[如何在 Azure App Service 中設定服務主體驗證](#authconfig) 一節大致說明如何為 API 應用程式設定驗證，以及如何取用受保護的 API 應用程式。</span><span class="sxs-lookup"><span data-stu-id="c2899-117">The [How to configure service principal authentication in Azure App Service](#authconfig) section explains in general how to configure authentication for any API app, and how to consume the protected API app.</span></span> <span data-ttu-id="c2899-118">本節一體適用於 App Service 支援的所有架構，包括 .NET、Node.js 和 Java。</span><span class="sxs-lookup"><span data-stu-id="c2899-118">This section applies equally to all frameworks supported by App Service, including .NET, Node.js, and Java.</span></span>
* <span data-ttu-id="c2899-119">從 [繼續進行 .NET 入門教學課程](#tutorialstart) 章節開始，教學課程會引導您針對 App Service 中執行的 .NET 範例應用程式設定「內部存取」案例。</span><span class="sxs-lookup"><span data-stu-id="c2899-119">Starting with the [Continuing the .NET getting-started tutorials](#tutorialstart) section, the tutorial guides you through configuring an "internal access" scenario for a .NET sample application running in App Service.</span></span> 

## <span data-ttu-id="c2899-120"><a id="authconfig"></a> 如何在 Azure App Service 中設定服務主體驗證</span><span class="sxs-lookup"><span data-stu-id="c2899-120"><a id="authconfig"></a> How to configure service principal authentication in Azure App Service</span></span>
<span data-ttu-id="c2899-121">本節提供適用於任何 API 應用程式的一般指示。</span><span class="sxs-lookup"><span data-stu-id="c2899-121">This section provides general instructions that apply to any API app.</span></span> <span data-ttu-id="c2899-122">如需「待辦事項清單」.NET 範例應用程式的專用步驟，請移至 [繼續進行 .NET API Apps 教學課程系列](#tutorialstart)。</span><span class="sxs-lookup"><span data-stu-id="c2899-122">For steps specific to the To Do List .NET sample application, go to [Continuing the .NET API Apps tutorial series](#tutorialstart).</span></span>

1. <span data-ttu-id="c2899-123">在 [Azure 入口網站](https://portal.azure.com/)中，瀏覽至您想要保護的 API 應用程式的 [設定] 刀鋒視窗，然後尋找 [功能] 區段，再按一下 [驗證/授權]。</span><span class="sxs-lookup"><span data-stu-id="c2899-123">In the [Azure portal](https://portal.azure.com/), navigate to the **Settings** blade of the API app that you want to protect, and then find the **Features** section and click **Authentication/ Authorization**.</span></span>
   
    ![Azure 入口網站中的驗證/授權](./media/app-service-api-dotnet-user-principal-auth/features.png)
2. <span data-ttu-id="c2899-125">在 [驗證/授權] 刀鋒視窗中，按一下 [開啟]。</span><span class="sxs-lookup"><span data-stu-id="c2899-125">In the **Authentication / Authorization** blade, click **On**.</span></span>
3. <span data-ttu-id="c2899-126">在 [要求未經驗證時所採取的動作] 下拉式清單中，選取 [使用 Azure Active Directory 登入]。</span><span class="sxs-lookup"><span data-stu-id="c2899-126">In the **Action to take when request is not authenticated** drop-down list, select **Log in with Azure Active Directory** .</span></span>
4. <span data-ttu-id="c2899-127">在 [驗證提供者] 底下，選取 [Azure Active Directory]。</span><span class="sxs-lookup"><span data-stu-id="c2899-127">Under **Authentication Providers**, select **Azure Active Directory**.</span></span>
   
    ![Azure 入口網站中的驗證/授權刀鋒視窗](./media/app-service-api-dotnet-user-principal-auth/authblade.png)
5. <span data-ttu-id="c2899-129">設定 [Azure Active Directory 設定]  刀鋒視窗以建立新的 Azure AD 應用程式，或者，如果您已有想要使用的現有 Azure AD 應用程式，則請使用該應用程式。</span><span class="sxs-lookup"><span data-stu-id="c2899-129">Configure the **Azure Active Directory Settings** blade to create a new Azure AD application, or use an existing Azure AD application if you already have one that you want to use.</span></span>
   
    <span data-ttu-id="c2899-130">內部案例通常涉及 API 應用程式呼叫 API 應用程式。</span><span class="sxs-lookup"><span data-stu-id="c2899-130">Internal scenarios typically involve an API app calling an API app.</span></span> <span data-ttu-id="c2899-131">您可以為每一個 API 應用程式使用個別的 Azure AD 應用程式，或是全都使用同一個 Azure AD 應用程式。</span><span class="sxs-lookup"><span data-stu-id="c2899-131">You can use separate Azure AD applications for each API app or just one Azure AD application.</span></span>
   
    <span data-ttu-id="c2899-132">如需關於此刀鋒視窗的詳細指示，請參閱 [如何設定 App Service 應用程式使用 Azure Active Directory 登入](../app-service-mobile/app-service-mobile-how-to-configure-active-directory-authentication.md)。</span><span class="sxs-lookup"><span data-stu-id="c2899-132">For detailed instructions on this blade, see [How to configure your App Service application to use Azure Active Directory login](../app-service-mobile/app-service-mobile-how-to-configure-active-directory-authentication.md).</span></span>
6. <span data-ttu-id="c2899-133">[驗證提供者設定] 刀鋒視窗使用完畢時，按一下 [確定] 。</span><span class="sxs-lookup"><span data-stu-id="c2899-133">When you're done with the authentication provider configuration blade, click **OK**.</span></span>
7. <span data-ttu-id="c2899-134">在 [驗證/授權] 刀鋒視窗中，按一下 [儲存]。</span><span class="sxs-lookup"><span data-stu-id="c2899-134">In the **Authentication / Authorization** blade, click **Save**.</span></span>
   
    ![按一下 [Save] (儲存)。](./media/app-service-api-dotnet-service-principal-auth/authsave.png)

<span data-ttu-id="c2899-136">完成時，App Service 只會允許來自已設定 Azure AD 租用戶的呼叫端的要求。</span><span class="sxs-lookup"><span data-stu-id="c2899-136">When this is done, App Service only allows requests from callers in the configured Azure AD tenant.</span></span> <span data-ttu-id="c2899-137">受保護的 API 應用程式則不需要有驗證或授權程式碼。</span><span class="sxs-lookup"><span data-stu-id="c2899-137">No authentication or authorization code is required in the protected API app.</span></span> <span data-ttu-id="c2899-138">持有人權杖會與 HTTP 標頭中的常用宣告一起傳遞至 API 應用程式，您可以在程式碼中閱讀該資訊，以驗證要求是來自特定的呼叫端，例如服務主體。</span><span class="sxs-lookup"><span data-stu-id="c2899-138">The bearer token is passed to the API app along with commonly used claims in HTTP headers, and you can read that information in code to validate that requests are from a particular caller, such as a service principal.</span></span>

<span data-ttu-id="c2899-139">凡是 App Service 所支援的語言 (包括 .NET、Node.js 和 Java)，此驗證功能的運作方式都相同。</span><span class="sxs-lookup"><span data-stu-id="c2899-139">This authentication functionality works the same way for all languages that App service supports, including .NET, Node.js, and Java.</span></span> 

#### <a name="how-to-consume-the-protected-api-app"></a><span data-ttu-id="c2899-140">如何取用受保護的 API 應用程式</span><span class="sxs-lookup"><span data-stu-id="c2899-140">How to consume the protected API app</span></span>
<span data-ttu-id="c2899-141">呼叫端必須在 API 呼叫中提供 Azure AD 持有人權杖。</span><span class="sxs-lookup"><span data-stu-id="c2899-141">The caller must provide an Azure AD bearer token with API calls.</span></span> <span data-ttu-id="c2899-142">若要取得使用服務主體認證的持有人權杖，呼叫端必須使用 Active Directory Authentication Library (適用於 [.NET](https://www.nuget.org/packages/Microsoft.IdentityModel.Clients.ActiveDirectory)、[Node.js](https://github.com/AzureAD/azure-activedirectory-library-for-nodejs) 或 [Java](https://github.com/AzureAD/azure-activedirectory-library-for-java) 的 ADAL)。</span><span class="sxs-lookup"><span data-stu-id="c2899-142">To get a bearer token using service principal credentials, the caller uses Active Directory Authentication Library (ADAL for [.NET](https://www.nuget.org/packages/Microsoft.IdentityModel.Clients.ActiveDirectory), [Node.js](https://github.com/AzureAD/azure-activedirectory-library-for-nodejs), or [Java](https://github.com/AzureAD/azure-activedirectory-library-for-java)).</span></span> <span data-ttu-id="c2899-143">為了取得權杖，呼叫 ADAL 的程式碼會對 ADAL 提供下列資訊：</span><span class="sxs-lookup"><span data-stu-id="c2899-143">To get a token, the code that calls ADAL provides to ADAL the following information:</span></span>

* <span data-ttu-id="c2899-144">Azure AD 租用戶的名稱。</span><span class="sxs-lookup"><span data-stu-id="c2899-144">The name of your Azure AD tenant.</span></span>
* <span data-ttu-id="c2899-145">與呼叫端相關聯之 Azure AD 應用程式的用戶端識別碼和用戶端密碼 (應用程式金鑰)。</span><span class="sxs-lookup"><span data-stu-id="c2899-145">The client ID and client secret (app key) of the Azure AD app associated with the caller.</span></span>
* <span data-ttu-id="c2899-146">與受保護 API 應用程式相關聯之 Azure AD 應用程式的用戶端識別碼 </span><span class="sxs-lookup"><span data-stu-id="c2899-146">The client ID of the Azure AD application associated with the protected API app.</span></span> <span data-ttu-id="c2899-147">(如果只有使用一個 Azure AD 應用程式，則此識別碼就是與呼叫端相同的用戶端識別碼)。</span><span class="sxs-lookup"><span data-stu-id="c2899-147">(If just one Azure AD application is used, this is the same client ID as the one for the caller.)</span></span>

<span data-ttu-id="c2899-148">這些值可在 [Azure 傳統入口網站](https://manage.windowsazure.com/)的 Azure AD 頁面中取得。</span><span class="sxs-lookup"><span data-stu-id="c2899-148">These values are available in the Azure AD pages of the [Azure classic portal](https://manage.windowsazure.com/).</span></span>

<span data-ttu-id="c2899-149">一旦取得權杖，呼叫端就會將它放入 HTTP 要求的 Authorization 標頭中。</span><span class="sxs-lookup"><span data-stu-id="c2899-149">Once the token has been acquired, the caller includes it with HTTP requests in the Authorization header.</span></span>  <span data-ttu-id="c2899-150">App Service 會驗證權杖，並允許要求觸達受保護的 API 應用程式。</span><span class="sxs-lookup"><span data-stu-id="c2899-150">App Service validates the token and allows the requests to reach the protected API app.</span></span>

#### <a name="how-to-protect-the-api-app-from-access-by-users-in-the-same-tenant"></a><span data-ttu-id="c2899-151">如何防止同一租用戶中的使用者存取 API 應用程式</span><span class="sxs-lookup"><span data-stu-id="c2899-151">How to protect the API app from access by users in the same tenant</span></span>
<span data-ttu-id="c2899-152">同一租用戶中的使用者所擁有的持有人權杖也會對受保護的 API 應用程式有效。</span><span class="sxs-lookup"><span data-stu-id="c2899-152">Bearer tokens for users in the same tenant are considered valid for the protected API app.</span></span>  <span data-ttu-id="c2899-153">如果您想要確保只有服務主體可以呼叫受保護的 API 應用程式，請在受保護的 API 應用程式中新增程式碼以驗證來自權杖的下列宣告：</span><span class="sxs-lookup"><span data-stu-id="c2899-153">If you want to ensure that only a service principal can call the protected API app, add code in the protected API app to validate the following claims from the token:</span></span>

* <span data-ttu-id="c2899-154">`appid` 應該是與呼叫端相關聯之 Azure AD 應用程式的用戶端識別碼。</span><span class="sxs-lookup"><span data-stu-id="c2899-154">`appid` should be the client ID of the Azure AD application that is associated with the caller.</span></span> 
* <span data-ttu-id="c2899-155">`oid` (`objectidentifier`) 應該是呼叫端的服務主體識別碼。</span><span class="sxs-lookup"><span data-stu-id="c2899-155">`oid` (`objectidentifier`) should be the service principal ID of the caller.</span></span> 

<span data-ttu-id="c2899-156">App Service 也在 X-MS-CLIENT-PRINCIPAL-ID 標頭中提供 `objectidentifier` 宣告。</span><span class="sxs-lookup"><span data-stu-id="c2899-156">App Service also provides the `objectidentifier` claim in the X-MS-CLIENT-PRINCIPAL-ID header.</span></span>

### <a name="how-to-protect-the-api-app-from-browser-access"></a><span data-ttu-id="c2899-157">如何防止瀏覽器存取 API 應用程式</span><span class="sxs-lookup"><span data-stu-id="c2899-157">How to protect the API app from browser access</span></span>
<span data-ttu-id="c2899-158">如果您並未驗證受保護 API 應用程式之程式碼中的宣告，而且您為受保護的 API 應用程式使用個別的 Azure AD 應用程式，請確定 Azure AD 應用程式的回覆 URL 與 API 應用程式的基底 URL 不同。</span><span class="sxs-lookup"><span data-stu-id="c2899-158">If you don't validate claims in code in the protected API app, and if you use a separate Azure AD application for the protected API app, make sure that the Azure AD application's Reply URL is not the same as the API app's base URL.</span></span> <span data-ttu-id="c2899-159">如果回覆 URL 直接指向受保護的 API 應用程式，同一 Azure AD 租用戶中的使用者將能夠瀏覽至 API 應用程式、進行登入，並成功呼叫 API。</span><span class="sxs-lookup"><span data-stu-id="c2899-159">If the Reply URL points directly to the protected API app, a user in the same Azure AD tenant could browse to the API app, log on, and successfully call the API.</span></span>

## <span data-ttu-id="c2899-160"><a id="tutorialstart"></a> 繼續進行 .NET API Apps 教學課程系列</span><span class="sxs-lookup"><span data-stu-id="c2899-160"><a id="tutorialstart"></a> Continuing the .NET API Apps tutorial series</span></span>
<span data-ttu-id="c2899-161">如果您要遵循適用於 API 應用程式的 Node.js 或 Java 教學課程系列，請跳至 [後續步驟](#next-steps) 一節。</span><span class="sxs-lookup"><span data-stu-id="c2899-161">If you are following the Node.js or Java tutorial series for API apps, skip to the [Next steps](#next-steps) section.</span></span> 

<span data-ttu-id="c2899-162">本文其餘部分將接續說明 .NET API Apps 教學課程系列，並且假設您已完成 [使用者驗證教學課程](app-service-api-dotnet-user-principal-auth.md) 而且擁有在 Azure 中執行、已啟用使用者驗證的範例應用程式。</span><span class="sxs-lookup"><span data-stu-id="c2899-162">The remainder of this article continues the .NET API Apps tutorial series and assumes that you have completed the [user authentication tutorial](app-service-api-dotnet-user-principal-auth.md) and have the sample application running in Azure with user authentication enabled.</span></span>

## <a name="set-up-authentication-in-azure"></a><span data-ttu-id="c2899-163">在 Azure 中設定驗證</span><span class="sxs-lookup"><span data-stu-id="c2899-163">Set up authentication in Azure</span></span>
<span data-ttu-id="c2899-164">在本節中，您將會設定 App Service，以便只有其允許觸達資料層 API 應用程式的 HTTP 要求，能擁有有效的 Azure AD 持有人權杖。</span><span class="sxs-lookup"><span data-stu-id="c2899-164">In this section you configure App Service so that the only HTTP requests it allows to reach the data tier API app are the ones that have valid Azure AD bearer tokens.</span></span> 

<span data-ttu-id="c2899-165">在下一節中，則會設定中介層 API 應用程式，以傳送應用程式認證至 Azure AD、取回持有人權杖，並將持有人權杖傳送至資料層 API 應用程式。</span><span class="sxs-lookup"><span data-stu-id="c2899-165">In the following section, you configure the middle tier API app to send application credentials to Azure AD, get back a bearer token, and send the bearer token to the data tier API app.</span></span> <span data-ttu-id="c2899-166">下圖可說明此程序。</span><span class="sxs-lookup"><span data-stu-id="c2899-166">This process is illustrated in the diagram.</span></span>

![服務驗證圖表](./media/app-service-api-dotnet-service-principal-auth/appdiagram.png)

<span data-ttu-id="c2899-168">如果您遵循教學課程指示進行時遇到問題，請參閱教學課程尾端的 [疑難排解](#troubleshooting) 一節。</span><span class="sxs-lookup"><span data-stu-id="c2899-168">If you run into problems while following the tutorial directions, see the [Troubleshooting](#troubleshooting) section at the end of the tutorial.</span></span> 

1. <span data-ttu-id="c2899-169">在 [Azure 入口網站](https://portal.azure.com/)中，瀏覽至您為 ToDoListDataAPI (資料層) API 應用程式建立之 API 應用程式的 [設定] 刀鋒視窗，然後按一下 [設定]。</span><span class="sxs-lookup"><span data-stu-id="c2899-169">In the [Azure portal](https://portal.azure.com/), navigate to the **Settings** blade of the API app that you created for the ToDoListDataAPI (data tier) API app, and then click **Settings**.</span></span>
2. <span data-ttu-id="c2899-170">在 [設定] 刀鋒視窗中，尋找 [功能] 區段，然後按一下 [驗證/授權]。</span><span class="sxs-lookup"><span data-stu-id="c2899-170">In the **Settings** blade, find the **Features** section, and then click **Authentication / Authorization**.</span></span>
   
    ![Azure 入口網站中的驗證/授權](./media/app-service-api-dotnet-user-principal-auth/features.png)
3. <span data-ttu-id="c2899-172">在 [驗證/授權] 刀鋒視窗中，按一下 [開啟]。</span><span class="sxs-lookup"><span data-stu-id="c2899-172">In the **Authentication / Authorization** blade, click **On**.</span></span>
4. <span data-ttu-id="c2899-173">在 [要求未經驗證時所採取的動作] 下拉式清單中，選取 [登入 Azure Active Directory]。</span><span class="sxs-lookup"><span data-stu-id="c2899-173">In the **Action to take when request is not authenticated** drop-down list, select **Log in with Azure Active Directory**.</span></span>
   
    <span data-ttu-id="c2899-174">這是能夠讓 App Service 確保唯有經過驗證的要求能觸達 API 應用程式的設定。</span><span class="sxs-lookup"><span data-stu-id="c2899-174">This is the setting that causes App Service to ensure that only authenticated requests reach the API app.</span></span> <span data-ttu-id="c2899-175">對於具有有效持有人權杖的要求，App Service 會將權杖傳遞至 API 應用程式，並於 HTTP 標頭中填入常用宣告，以讓程式碼更輕鬆地取得該資訊。</span><span class="sxs-lookup"><span data-stu-id="c2899-175">For requests that have valid bearer tokens, App Service passes the tokens along to the API app and populates HTTP headers with commonly used claims to make that information more easily available to your code.</span></span>
5. <span data-ttu-id="c2899-176">在 [驗證提供者] 底下，按一下 [Azure Active Directory]。</span><span class="sxs-lookup"><span data-stu-id="c2899-176">Under **Authentication Providers**, click **Azure Active Directory**.</span></span>
   
    ![Azure 入口網站中的驗證/授權刀鋒視窗](./media/app-service-api-dotnet-user-principal-auth/authblade.png)
6. <span data-ttu-id="c2899-178">在 [Azure Active Directory 設定] 刀鋒視窗中，按一下 [快速]。</span><span class="sxs-lookup"><span data-stu-id="c2899-178">In the **Azure Active Directory Settings** blade, click **Express**.</span></span>
   
    <span data-ttu-id="c2899-179">在使用 [快速] 選項時，Azure 可以自動在 Azure AD [租用戶](https://msdn.microsoft.com/en-us/library/azure/jj573650.aspx#BKMK_WhatIsAnAzureADTenant)中建立 AAD 應用程式。</span><span class="sxs-lookup"><span data-stu-id="c2899-179">With the **Express** option Azure can automatically create an AAD application in your Azure AD [tenant](https://msdn.microsoft.com/en-us/library/azure/jj573650.aspx#BKMK_WhatIsAnAzureADTenant).</span></span> 
   
    <span data-ttu-id="c2899-180">您不必建立租用戶，因為每個 Azure 帳戶都會自動擁有一個。</span><span class="sxs-lookup"><span data-stu-id="c2899-180">You don't have to create a tenant, because every Azure account automatically has one.</span></span>
7. <span data-ttu-id="c2899-181">在 [管理模式] 底下，按一下 [建立新的 AD 應用程式] \(若尚未選取)。</span><span class="sxs-lookup"><span data-stu-id="c2899-181">Under **Management mode**, click **Create New AD App** if it isn't already selected.</span></span>
   
    <span data-ttu-id="c2899-182">入口網站會在 [建立應用程式]  輸入方塊中填入預設值。</span><span class="sxs-lookup"><span data-stu-id="c2899-182">The portal plugs the **Create App** input box with a default value.</span></span> <span data-ttu-id="c2899-183">根據預設，Azure AD 應用程式的名稱會與 API 應用程式相同。</span><span class="sxs-lookup"><span data-stu-id="c2899-183">By default, the Azure AD application is named the same as the API app.</span></span> <span data-ttu-id="c2899-184">如有需要，也可以輸入不同名稱。</span><span class="sxs-lookup"><span data-stu-id="c2899-184">If you prefer, you can enter a different name.</span></span>
   
    ![Azure AD 設定](./media/app-service-api-dotnet-service-principal-auth/aadsettings.png)
   
    <span data-ttu-id="c2899-186">**附註**：或者，您可以讓呼叫端 API 應用程式和受保護的 API 應用程式使用同一個 Azure AD 應用程式。</span><span class="sxs-lookup"><span data-stu-id="c2899-186">**Note**: As an alternative, you could use a single Azure AD application for both the calling API app and the protected API app.</span></span> <span data-ttu-id="c2899-187">如果您選擇後者，則這邊不需要 [建立新的 AD 應用程式]  選項，因為您稍早已在使用者驗證教學課程中建立了 Azure AD 應用程式。</span><span class="sxs-lookup"><span data-stu-id="c2899-187">If you chose that alternative, you would not need the **Create New AD App** option here because you already created an Azure AD application earlier in the user authentication tutorial.</span></span> <span data-ttu-id="c2899-188">在本教學課程中，您會讓呼叫端 API 應用程式和受保護的 API 應用程式使用個別的 Azure AD 應用程式。</span><span class="sxs-lookup"><span data-stu-id="c2899-188">For this tutorial, you'll use separate Azure AD applications for the calling API app and the protected API app.</span></span>
8. <span data-ttu-id="c2899-189">記下 [建立應用程式]  輸入方塊中的值，您稍後將在 Azure 傳統入口網站中查詢此 AAD 應用程式。</span><span class="sxs-lookup"><span data-stu-id="c2899-189">Make a note of the value that is in the **Create App** input box; you'll look up this AAD application in the Azure classic portal later.</span></span>
9. <span data-ttu-id="c2899-190">按一下 [確定] 。</span><span class="sxs-lookup"><span data-stu-id="c2899-190">Click **OK**.</span></span>
10. <span data-ttu-id="c2899-191">在 [驗證/授權] 刀鋒視窗中，按一下 [儲存]。</span><span class="sxs-lookup"><span data-stu-id="c2899-191">In the **Authentication / Authorization** blade, click **Save**.</span></span>
    
    ![按一下 [Save] (儲存)。](./media/app-service-api-dotnet-service-principal-auth/saveauth.png)
    
    <span data-ttu-id="c2899-193">App Service 在建立 Azure Active Directory 應用程式時，會自動將 [登入 URL] 和 [回覆 URL] 設定為 API 應用程式的 URL。</span><span class="sxs-lookup"><span data-stu-id="c2899-193">App Service creates an Azure Active Directory application with **Sign-on URL** and **Reply URL** automatically set to the URL of your API app.</span></span> <span data-ttu-id="c2899-194">第二個值可讓 AAD 租用戶中的使用者登入和存取 API 應用程式。</span><span class="sxs-lookup"><span data-stu-id="c2899-194">The latter value enables users in your AAD tenant to log in and access the API app.</span></span>

### <a name="verify-that-the-api-app-is-protected"></a><span data-ttu-id="c2899-195">確認 API 應用程式已受到保護</span><span class="sxs-lookup"><span data-stu-id="c2899-195">Verify that the API app is protected</span></span>
1. <span data-ttu-id="c2899-196">在瀏覽器中，移至 API 應用程式的 URL：在 Azure 入口網站的 [API 應用程式] 刀鋒視窗中，按一下 [URL] 下方的連結。</span><span class="sxs-lookup"><span data-stu-id="c2899-196">In a browser go to the URL of the API app: in the **API app** blade in the Azure portal, click the link under **URL**.</span></span> 
   
    <span data-ttu-id="c2899-197">由於未經驗證的要求不得觸達 API 應用程式，因此系統會將您重新導向至登入畫面。</span><span class="sxs-lookup"><span data-stu-id="c2899-197">You are redirected to a login screen because unauthenticated requests are not allowed to reach the API app.</span></span> 
   
    <span data-ttu-id="c2899-198">如果瀏覽器的確移至 Swagger UI，則表示瀏覽器可能已登入，若是如此，請開啟 InPrivate 或 Incognito 視窗並移至 Swagger UI URL。</span><span class="sxs-lookup"><span data-stu-id="c2899-198">If your browser does go to the Swagger UI, your browser might already be logged on -- in that case, open an InPrivate or Incognito window and go to the Swagger UI URL.</span></span>
2. <span data-ttu-id="c2899-199">使用 AAD 租用戶中使用者的認證進行登入。</span><span class="sxs-lookup"><span data-stu-id="c2899-199">Log in with credentials of a user in your AAD tenant.</span></span>
   
   <span data-ttu-id="c2899-200">登入後，[已成功建立] 頁面隨即出現在瀏覽器中。</span><span class="sxs-lookup"><span data-stu-id="c2899-200">When you're logged on, the "successfully created" page appears in the browser.</span></span>

## <a name="configure-the-todolistapi-project-to-acquire-and-send-the-azure-ad-token"></a><span data-ttu-id="c2899-201">設定 ToDoListAPI 專案以取得和傳送 Azure AD 權杖</span><span class="sxs-lookup"><span data-stu-id="c2899-201">Configure the ToDoListAPI project to acquire and send the Azure AD token</span></span>
<span data-ttu-id="c2899-202">您將在本節執行下列工作：</span><span class="sxs-lookup"><span data-stu-id="c2899-202">In this section you do the following tasks:</span></span>

* <span data-ttu-id="c2899-203">在中介層 API 應用程式中新增使用 Azure AD 應用程式認證的程式碼，以取得權杖，然後透過 HTTP 要求將其傳送至資料層 API 應用程式。</span><span class="sxs-lookup"><span data-stu-id="c2899-203">Add code in the middle tier API app that uses Azure AD application credentials to acquire a token and send it with HTTP requests to the data tier API app.</span></span>
* <span data-ttu-id="c2899-204">從 Azure AD 取得您需要的認證。</span><span class="sxs-lookup"><span data-stu-id="c2899-204">Get the credentials you need from Azure AD.</span></span>
* <span data-ttu-id="c2899-205">在中介層 API 應用程式的 Azure App Service 執行階段環境設定中輸入認證。</span><span class="sxs-lookup"><span data-stu-id="c2899-205">Enter the credentials into Azure App Service runtime environment settings in the middle tier API app.</span></span> 

### <a name="configure-the-todolistapi-project-to-acquire-and-send-the-azure-ad-token"></a><span data-ttu-id="c2899-206">設定 ToDoListAPI 專案以取得和傳送 Azure AD 權杖</span><span class="sxs-lookup"><span data-stu-id="c2899-206">Configure the ToDoListAPI project to acquire and send the Azure AD token</span></span>
<span data-ttu-id="c2899-207">在 Visual Studio 中對 ToDoListAPI 專案進行下列變更。</span><span class="sxs-lookup"><span data-stu-id="c2899-207">Make the following changes in the ToDoListAPI project in Visual Studio.</span></span>

1. <span data-ttu-id="c2899-208">取消註解「ServicePrincipal.cs」  檔案中的所有程式碼。</span><span class="sxs-lookup"><span data-stu-id="c2899-208">Uncomment all of the code in the *ServicePrincipal.cs* file.</span></span>
   
    <span data-ttu-id="c2899-209">這便是使用適用於 .NET 的 ADAL 來取得 Azure AD 持有人權杖的程式碼。</span><span class="sxs-lookup"><span data-stu-id="c2899-209">This is the code that uses ADAL for .NET to acquire the Azure AD bearer token.</span></span>  <span data-ttu-id="c2899-210">此程式碼會使用數個設定值，而您稍後將會在 Azure 執行階段環境中設定這些值。</span><span class="sxs-lookup"><span data-stu-id="c2899-210">It uses several configuration values that you'll set in the Azure runtime environment later.</span></span> <span data-ttu-id="c2899-211">此程式碼如下：</span><span class="sxs-lookup"><span data-stu-id="c2899-211">Here's the code:</span></span> 
   
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
   
    <span data-ttu-id="c2899-212">**附註：** 此程式碼需要 .NET 適用之 ADAL 的 NuGet 封裝 (Microsoft.IdentityModel.Clients.ActiveDirectory)，其早已安裝於專案中。</span><span class="sxs-lookup"><span data-stu-id="c2899-212">**Note:** This code requires the ADAL for .NET NuGet package (Microsoft.IdentityModel.Clients.ActiveDirectory), which is already installed in the project.</span></span> <span data-ttu-id="c2899-213">如果您是從頭建立此專案，則必須安裝此封裝。</span><span class="sxs-lookup"><span data-stu-id="c2899-213">If you were creating this project from scratch, you would have to install this package.</span></span> <span data-ttu-id="c2899-214">API 應用程式的新專案範本不會自動安裝此封裝。</span><span class="sxs-lookup"><span data-stu-id="c2899-214">This package is not automatically installed by the API app new-project template.</span></span>
2. <span data-ttu-id="c2899-215">在 Controllers/ToDoListController 中，將 `NewDataAPIClient` 方法中會將權杖新增至 HTTP 要求之 authorization 標頭的程式碼取消註解。</span><span class="sxs-lookup"><span data-stu-id="c2899-215">In *Controllers/ToDoListController*, uncomment the code in the `NewDataAPIClient` method that adds the token to HTTP requests in the authorization header.</span></span>
   
        client.HttpClient.DefaultRequestHeaders.Authorization =
            new AuthenticationHeaderValue("Bearer", ServicePrincipal.GetS2SAccessTokenForProdMSA().AccessToken);
3. <span data-ttu-id="c2899-216">部署 ToDoListAPI 專案 </span><span class="sxs-lookup"><span data-stu-id="c2899-216">Deploy the ToDoListAPI project.</span></span> <span data-ttu-id="c2899-217">(以滑鼠右鍵按一下專案，然後按一下 [發佈] > [發佈])。</span><span class="sxs-lookup"><span data-stu-id="c2899-217">(Right-click the project, then click **Publish > Publish**.)</span></span>
   
    <span data-ttu-id="c2899-218">Visual Studio 會部署專案並將瀏覽器開啟至 Web 應用程式的基底 URL。</span><span class="sxs-lookup"><span data-stu-id="c2899-218">Visual Studio deploys the project and opens a browser to the web app's base URL.</span></span> <span data-ttu-id="c2899-219">這會顯示 403 錯誤頁面，這是嘗試從瀏覽器移至 Web API 基底 URL 時的正常現象。</span><span class="sxs-lookup"><span data-stu-id="c2899-219">This will show a 403 error page, which is normal for an attempt to go to a Web API base URL from a browser.</span></span>
4. <span data-ttu-id="c2899-220">關閉瀏覽器。</span><span class="sxs-lookup"><span data-stu-id="c2899-220">Close the browser.</span></span>

### <a name="get-azure-ad-configuration-values"></a><span data-ttu-id="c2899-221">取得 Azure AD 設定值</span><span class="sxs-lookup"><span data-stu-id="c2899-221">Get Azure AD configuration values</span></span>
1. <span data-ttu-id="c2899-222">在 [Azure 傳統入口網站](https://manage.windowsazure.com/)中，移至 [Azure Active Directory]。</span><span class="sxs-lookup"><span data-stu-id="c2899-222">In the [Azure classic portal](https://manage.windowsazure.com/), go to **Azure Active Directory**.</span></span>
2. <span data-ttu-id="c2899-223">在 [目錄]  索引標籤中，選取您的 AAD 租用戶。</span><span class="sxs-lookup"><span data-stu-id="c2899-223">On the **Directory** tab, click your AAD tenant.</span></span>
3. <span data-ttu-id="c2899-224">按一下 [應用程式] > [我的公司擁有的應用程式]，然後按一下核取記號。</span><span class="sxs-lookup"><span data-stu-id="c2899-224">Click **Applications > Applications my company owns**, and then click the check mark.</span></span>
4. <span data-ttu-id="c2899-225">在應用程式清單中，按一下當您針對 ToDoListDataAPI (資料層) API 應用程式啟用驗證時 Azure 為您建立的應用程式名稱。</span><span class="sxs-lookup"><span data-stu-id="c2899-225">In the list of applications, click the name of the one that Azure created for you when you enabled authentication for the ToDoListDataAPI (data tier) API app.</span></span>
5. <span data-ttu-id="c2899-226">按一下 [設定]  索引標籤。</span><span class="sxs-lookup"><span data-stu-id="c2899-226">Click the **Configure** tab.</span></span>
6. <span data-ttu-id="c2899-227">複製 [用戶端識別碼]  值，並將其儲存至可在稍後取得此值的位置。</span><span class="sxs-lookup"><span data-stu-id="c2899-227">Copy the **Client ID** value and save it someplace you can get it from later.</span></span> 
7. <span data-ttu-id="c2899-228">在 Azure 傳統入口網站中，返回 [我公司所擁有的應用程式] 清單，然後按一下您為中介層 ToDoListAPI API 應用程式 (您在先前的教學課程中所建立，不是您在本教學課程中建立) 建立的 AAD 應用程式。</span><span class="sxs-lookup"><span data-stu-id="c2899-228">In the Azure classic portal go back to the list of **Applications my company owns**, and click the AAD application that you created for the middle tier ToDoListAPI API app (the one you created in the previous tutorial, not the one you created in this tutorial).</span></span>
8. <span data-ttu-id="c2899-229">按一下 [設定]  索引標籤。</span><span class="sxs-lookup"><span data-stu-id="c2899-229">Click the **Configure** tab.</span></span>
9. <span data-ttu-id="c2899-230">複製 [用戶端識別碼]  值，並將其儲存至可在稍後取得此值的位置。</span><span class="sxs-lookup"><span data-stu-id="c2899-230">Copy the **Client ID** value and save it someplace you can get it from later.</span></span>
10. <span data-ttu-id="c2899-231">在 [金鑰] 中，從 [選取持續時間] 下拉式清單選取 [1 年]。</span><span class="sxs-lookup"><span data-stu-id="c2899-231">Under **keys**, select **1 year** from the **Select duration** drop-down list.</span></span>
11. <span data-ttu-id="c2899-232">按一下 [儲存] 。</span><span class="sxs-lookup"><span data-stu-id="c2899-232">Click **Save**.</span></span>
    
     ![產生應用程式金鑰](./media/app-service-api-dotnet-service-principal-auth/genkey.png)
12. <span data-ttu-id="c2899-234">複製金鑰值，並將其儲存至可在稍後取得此值的位置。</span><span class="sxs-lookup"><span data-stu-id="c2899-234">Copy the key value and save it someplace you can get it from later.</span></span>
    
     ![複製新的應用程式金鑰](./media/app-service-api-dotnet-service-principal-auth/genkeycopy.png)

### <a name="configure-azure-ad-settings-in-the-middle-tier-api-apps-runtime-environment"></a><span data-ttu-id="c2899-236">在中介層 API 應用程式的執行階段環境中設定 Azure AD 設定</span><span class="sxs-lookup"><span data-stu-id="c2899-236">Configure Azure AD settings in the middle tier API app's runtime environment</span></span>
1. <span data-ttu-id="c2899-237">移至 [Azure 入口網站](https://portal.azure.com/)，然後瀏覽至裝載 TodoListAPI (中介層) 專案之 API 應用程式的 [API 應用程式] 刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="c2899-237">Go to the [Azure portal](https://portal.azure.com/), and then navigate to the **API App** blade for the API app that hosts the TodoListAPI (middle tier) project.</span></span>
2. <span data-ttu-id="c2899-238">按一下 [設定] > [應用程式設定]。</span><span class="sxs-lookup"><span data-stu-id="c2899-238">Click **Settings > Application Settings**.</span></span>
3. <span data-ttu-id="c2899-239">在 [應用程式設定]  區段中，新增下列金鑰和值：</span><span class="sxs-lookup"><span data-stu-id="c2899-239">In the **App settings** section, add the following keys and values:</span></span>
   
   | <span data-ttu-id="c2899-240">**金鑰**</span><span class="sxs-lookup"><span data-stu-id="c2899-240">**Key**</span></span> | <span data-ttu-id="c2899-241">ida:Authority</span><span class="sxs-lookup"><span data-stu-id="c2899-241">ida:Authority</span></span> |
   | --- | --- |
   | <span data-ttu-id="c2899-242">**值**</span><span class="sxs-lookup"><span data-stu-id="c2899-242">**Value**</span></span> |<span data-ttu-id="c2899-243">https://login.microsoftonline.com/{您的 Azure AD 租用戶名稱}</span><span class="sxs-lookup"><span data-stu-id="c2899-243">https://login.microsoftonline.com/{your Azure AD tenant name}</span></span> |
   | <span data-ttu-id="c2899-244">**範例**</span><span class="sxs-lookup"><span data-stu-id="c2899-244">**Example**</span></span> |<span data-ttu-id="c2899-245">https://login.microsoftonline.com/contoso.onmicrosoft.com</span><span class="sxs-lookup"><span data-stu-id="c2899-245">https://login.microsoftonline.com/contoso.onmicrosoft.com</span></span> |
   
   | <span data-ttu-id="c2899-246">**Key**</span><span class="sxs-lookup"><span data-stu-id="c2899-246">**Key**</span></span> | <span data-ttu-id="c2899-247">ida:ClientId</span><span class="sxs-lookup"><span data-stu-id="c2899-247">ida:ClientId</span></span> |
   | --- | --- |
   | <span data-ttu-id="c2899-248">**值**</span><span class="sxs-lookup"><span data-stu-id="c2899-248">**Value**</span></span> |<span data-ttu-id="c2899-249">呼叫端應用程式 (中介層 - ToDoListAPI) 的用戶端識別碼</span><span class="sxs-lookup"><span data-stu-id="c2899-249">Client ID of the calling application (middle tier - ToDoListAPI)</span></span> |
   | <span data-ttu-id="c2899-250">**範例**</span><span class="sxs-lookup"><span data-stu-id="c2899-250">**Example**</span></span> |<span data-ttu-id="c2899-251">960adec2-b74a-484a-960adec2-b74a-484a</span><span class="sxs-lookup"><span data-stu-id="c2899-251">960adec2-b74a-484a-960adec2-b74a-484a</span></span> |
   
   | <span data-ttu-id="c2899-252">**金鑰**</span><span class="sxs-lookup"><span data-stu-id="c2899-252">**Key**</span></span> | <span data-ttu-id="c2899-253">ida:ClientSecret</span><span class="sxs-lookup"><span data-stu-id="c2899-253">ida:ClientSecret</span></span> |
   | --- | --- |
   | <span data-ttu-id="c2899-254">**值**</span><span class="sxs-lookup"><span data-stu-id="c2899-254">**Value**</span></span> |<span data-ttu-id="c2899-255">呼叫端應用程式 (中介層 - ToDoListAPI) 的應用程式金鑰</span><span class="sxs-lookup"><span data-stu-id="c2899-255">App key of the calling application (middle tier - ToDoListAPI)</span></span> |
   | <span data-ttu-id="c2899-256">**範例**</span><span class="sxs-lookup"><span data-stu-id="c2899-256">**Example**</span></span> |<span data-ttu-id="c2899-257">e65e8fc9-5f6b-48e8-e65e8fc9-5f6b-48e8</span><span class="sxs-lookup"><span data-stu-id="c2899-257">e65e8fc9-5f6b-48e8-e65e8fc9-5f6b-48e8</span></span> |
   
   | <span data-ttu-id="c2899-258">**金鑰**</span><span class="sxs-lookup"><span data-stu-id="c2899-258">**Key**</span></span> | <span data-ttu-id="c2899-259">ida:Resource</span><span class="sxs-lookup"><span data-stu-id="c2899-259">ida:Resource</span></span> |
   | --- | --- |
   | <span data-ttu-id="c2899-260">**值**</span><span class="sxs-lookup"><span data-stu-id="c2899-260">**Value**</span></span> |<span data-ttu-id="c2899-261">呼叫端應用程式 (資料層 - ToDoListAPI) 的用戶端識別碼</span><span class="sxs-lookup"><span data-stu-id="c2899-261">Client ID of the called application (data tier - ToDoListDataAPI)</span></span> |
   | <span data-ttu-id="c2899-262">**範例**</span><span class="sxs-lookup"><span data-stu-id="c2899-262">**Example**</span></span> |<span data-ttu-id="c2899-263">e65e8fc9-5f6b-48e8-e65e8fc9-5f6b-48e8</span><span class="sxs-lookup"><span data-stu-id="c2899-263">e65e8fc9-5f6b-48e8-e65e8fc9-5f6b-48e8</span></span> |
   
    <span data-ttu-id="c2899-264">**附註**︰針對 `ida:Resource`，請確定您使用呼叫之應用程式的**用戶端識別碼**，而非其**應用程式識別碼 URI**。</span><span class="sxs-lookup"><span data-stu-id="c2899-264">**Note**: For `ida:Resource`, make sure you use the called application's **client ID** and not its **App ID URI**.</span></span>
   
    <span data-ttu-id="c2899-265">`ida:ClientId` 和 `ida:Resource` 對本教學課程是不同的值，因為您正在為中介層和資料層使用個別的 Azure AD 應用程式。</span><span class="sxs-lookup"><span data-stu-id="c2899-265">`ida:ClientId` and `ida:Resource` are different values for this tutorial because you're using separate Azure AD applicaations for the middle tier and data tier.</span></span> <span data-ttu-id="c2899-266">如果您讓呼叫端 API 應用程式和受保護的 API 應用程式使用同一個 Azure AD 應用程式，則會在 `ida:ClientId` 和 `ida:Resource` 中使用相同的值。</span><span class="sxs-lookup"><span data-stu-id="c2899-266">If you were using a single Azure AD application for the calling API app and the protected API app, you would use the same value in both `ida:ClientId` and `ida:Resource`.</span></span>
   
    <span data-ttu-id="c2899-267">程式碼會使用 ConfigurationManager 來取得這些值，因此這些值可以儲存在專案的 Web.config 檔案或 Azure 執行階段環境中。</span><span class="sxs-lookup"><span data-stu-id="c2899-267">The code uses ConfigurationManager to get these values, so they could be stored in the project's Web.config file or in the Azure runtime environment.</span></span> <span data-ttu-id="c2899-268">當 ASP.NET 應用程式在 Azure App Service 中執行時，環境設定會自動覆寫 Web.config 的設定。</span><span class="sxs-lookup"><span data-stu-id="c2899-268">While an ASP.NET application is running in Azure App Service, environment settings automatically override settings from Web.config.</span></span> <span data-ttu-id="c2899-269">一般來說，環境設定是 [比 Web.config 檔案更安全的機密資訊儲存方式](http://www.asp.net/identity/overview/features-api/best-practices-for-deploying-passwords-and-other-sensitive-data-to-aspnet-and-azure)。</span><span class="sxs-lookup"><span data-stu-id="c2899-269">Environment settings are generally a [more secure way to store sensitive information compared to a Web.config file](http://www.asp.net/identity/overview/features-api/best-practices-for-deploying-passwords-and-other-sensitive-data-to-aspnet-and-azure).</span></span>
4. <span data-ttu-id="c2899-270">按一下 [儲存] 。</span><span class="sxs-lookup"><span data-stu-id="c2899-270">Click **Save**.</span></span>
   
    ![按一下 [Save] (儲存)。](./media/app-service-api-dotnet-service-principal-auth/appsettings.png)

### <a name="test-the-application"></a><span data-ttu-id="c2899-272">測試應用程式</span><span class="sxs-lookup"><span data-stu-id="c2899-272">Test the application</span></span>
1. <span data-ttu-id="c2899-273">在瀏覽器中，移至 AngularJS 前端 Web 應用程式的 HTTPS URL。</span><span class="sxs-lookup"><span data-stu-id="c2899-273">In a browser go to the HTTPS URL of the AngularJS front end web app.</span></span>
2. <span data-ttu-id="c2899-274">按一下 [待辦事項清單]  索引標籤，並以 Azure AD 租用戶中使用者的認證進行登入。</span><span class="sxs-lookup"><span data-stu-id="c2899-274">Click the **To Do List** tab and log in with credentials for a user in your Azure AD tenant.</span></span> 
3. <span data-ttu-id="c2899-275">新增待辦事項項目，以確認應用程式可以運作。</span><span class="sxs-lookup"><span data-stu-id="c2899-275">Add to-do items to verify that the application is working.</span></span>
   
    ![待辦事項清單頁面](./media/app-service-api-dotnet-service-principal-auth/mvchome.png)
   
    <span data-ttu-id="c2899-277">如果應用程式未如預期般運作，請仔細檢查所有您在 Azure 入口網站中輸入的設定。</span><span class="sxs-lookup"><span data-stu-id="c2899-277">If the application doesn't work as expected, double-check all of the settings you entered in the Azure portal.</span></span> <span data-ttu-id="c2899-278">如果所有設定看起來都沒問題，請參閱本教學課程稍後的 [疑難排解](#troubleshooting) 一節。</span><span class="sxs-lookup"><span data-stu-id="c2899-278">If all of the settings appear to be correct, see the [Troubleshooting](#troubleshooting) section later in this tutorial.</span></span>

## <a name="protect-the-api-app-from-browser-access"></a><span data-ttu-id="c2899-279">防止瀏覽器存取 API 應用程式</span><span class="sxs-lookup"><span data-stu-id="c2899-279">Protect the API app from browser access</span></span>
<span data-ttu-id="c2899-280">在本教學課程中，您已為 ToDoListDataAPI (資料層) API 應用程式建立了個別的 Azure AD 應用程式。</span><span class="sxs-lookup"><span data-stu-id="c2899-280">For this tutorial you created a separate Azure AD application for the ToDoListDataAPI (data tier) API app.</span></span> <span data-ttu-id="c2899-281">如您所見，App Service 在建立 AAD 應用程式時，會將 AAD 應用程式設定成可讓使用者在瀏覽器中移至 API 應用程式的 URL 來進行登入。</span><span class="sxs-lookup"><span data-stu-id="c2899-281">As you've seen, when App Service creates an AAD application, it configures the AAD application in a way that enables a user to go to the API app's URL in a browser and log on.</span></span> <span data-ttu-id="c2899-282">這表示不只是服務主體，連 Azure AD 租用戶中的使用者都有可能可以存取 API。</span><span class="sxs-lookup"><span data-stu-id="c2899-282">That means it's possible for an end user in your Azure AD tenant, not just a service principal, to access the API.</span></span> 

<span data-ttu-id="c2899-283">如果您想要防止瀏覽器存取，但不要在受保護的 API 應用程式中撰寫任何程式碼，您可以變更 AAD 應用程式中的 [回覆 URL]  ，使其不同於 API 應用程式的基底 URL。</span><span class="sxs-lookup"><span data-stu-id="c2899-283">If you want to prevent browser access without writing any code in the protected API app, you can change the **Reply URL** in the AAD application so that it's different from the API app's base URL.</span></span> 

### <a name="disable-browser-access"></a><span data-ttu-id="c2899-284">停用瀏覽器存取</span><span class="sxs-lookup"><span data-stu-id="c2899-284">Disable browser access</span></span>
1. <span data-ttu-id="c2899-285">在傳統入口網站的 [設定] 索引標籤中，針對為 TodoListService 所建立的 AAD 應用程式，變更 [回覆 URL] 欄位中的值，以讓它屬於有效 URL，但卻不是 API 應用程式的 URL。</span><span class="sxs-lookup"><span data-stu-id="c2899-285">In the classic portal's **Configure** tab for the AAD application that was created for the TodoListService, change the value in the **Reply URL** field so that it is a valid URL but not the API app's URL.</span></span>
2. <span data-ttu-id="c2899-286">按一下 [儲存] 。</span><span class="sxs-lookup"><span data-stu-id="c2899-286">Click **Save**.</span></span>

### <a name="verify-browser-access-no-longer-works"></a><span data-ttu-id="c2899-287">確認瀏覽器存取無法再運作</span><span class="sxs-lookup"><span data-stu-id="c2899-287">Verify browser access no longer works</span></span>
<span data-ttu-id="c2899-288">您稍早已確認過，您可以從瀏覽器以個別使用者的認證進行登入，藉此來移至 API 應用程式的 URL。</span><span class="sxs-lookup"><span data-stu-id="c2899-288">Earlier you verified that you can go to the API app URL from a browser by logging on with an individual user's credentials.</span></span> <span data-ttu-id="c2899-289">在本節中，您將要確認此動作已不可行。</span><span class="sxs-lookup"><span data-stu-id="c2899-289">In this section, you verify that this is no longer possible.</span></span> 

1. <span data-ttu-id="c2899-290">在新的瀏覽器視窗中，再次移至 API 應用程式的 URL。</span><span class="sxs-lookup"><span data-stu-id="c2899-290">In a new browser window, go to the URL of the API app again.</span></span>
2. <span data-ttu-id="c2899-291">在系統提示時進行登入。</span><span class="sxs-lookup"><span data-stu-id="c2899-291">Log in when prompted to do so.</span></span>
3. <span data-ttu-id="c2899-292">登入成功，但卻導致錯誤頁面。</span><span class="sxs-lookup"><span data-stu-id="c2899-292">Login succeeds but leads to an error page.</span></span>
   
    <span data-ttu-id="c2899-293">您已設定 AAD 應用程式，讓 AAD 租用戶中的使用者無法從瀏覽器登入和存取 API。</span><span class="sxs-lookup"><span data-stu-id="c2899-293">You've configured the AAD app so that users in the AAD tenant cannot log in and access the API from a browser.</span></span> <span data-ttu-id="c2899-294">您仍然可以使用服務主體權杖存取 API 應用程式，若要確認這一點，請移至 Web 應用程式的 URL，並新增更多待辦事項項目。</span><span class="sxs-lookup"><span data-stu-id="c2899-294">You can still access the API app by using a service principal token, which you can verify by going to the web app's URL and adding more to-do items.</span></span>

## <a name="restrict-access-to-a-particular-service-principal"></a><span data-ttu-id="c2899-295">限制對特定服務主體的存取</span><span class="sxs-lookup"><span data-stu-id="c2899-295">Restrict access to a particular service principal</span></span>
<span data-ttu-id="c2899-296">現在，Azure AD 租用戶中可以取得使用者或服務主體之權杖的任何呼叫端，都可以呼叫 TodoListDataAPI (資料層) API 應用程式。</span><span class="sxs-lookup"><span data-stu-id="c2899-296">Right now, any caller that can get a token for a user or service principal in your Azure AD tenant can call the TodoListDataAPI (data tier) API app.</span></span> <span data-ttu-id="c2899-297">您或許會想要確定資料層 API 應用程式只會接受 TodoListAPI (中介層) API 應用程式的呼叫，以及特定服務主體的呼叫。</span><span class="sxs-lookup"><span data-stu-id="c2899-297">You might want to make sure that the data tier API app only accepts calls from the TodoListAPI (middle tier) API app, and only from a particular service principal.</span></span> 

<span data-ttu-id="c2899-298">您可以透過新增程式碼來驗證傳入呼叫上的 `appid` 和 `objectidentifier` 宣告，以便加上這些限制。</span><span class="sxs-lookup"><span data-stu-id="c2899-298">You can add these restrictions by adding code to validate the `appid` and `objectidentifier` claims on incoming calls.</span></span>

<span data-ttu-id="c2899-299">在本教學課程中，您會將用來驗證應用程式識別碼和服務主體識別碼的程式碼直接放在控制器的動作之中。</span><span class="sxs-lookup"><span data-stu-id="c2899-299">For this tutorial you put the code that validates app ID and service principal ID directly in your controller actions.</span></span>  <span data-ttu-id="c2899-300">或者，您也可以使用自訂 `Authorize` 屬性，或是在啟動順序 (例如 OWIN 中介軟體) 中執行這項驗證。</span><span class="sxs-lookup"><span data-stu-id="c2899-300">Alternatives are to use a custom `Authorize` attribute or to do this validation in your startup sequences (e.g. OWIN middleware).</span></span> <span data-ttu-id="c2899-301">如需後者的範例，請參閱 [此範例應用程式](https://github.com/mohitsriv/EasyAuthMultiTierSample/blob/master/MyDashDataAPI/Startup.cs)。</span><span class="sxs-lookup"><span data-stu-id="c2899-301">For an example of the latter, see [this sample application](https://github.com/mohitsriv/EasyAuthMultiTierSample/blob/master/MyDashDataAPI/Startup.cs).</span></span> 

<span data-ttu-id="c2899-302">對 TodoListDataAPI 專案進行下列變更。</span><span class="sxs-lookup"><span data-stu-id="c2899-302">Make the following changes to the TodoListDataAPI project.</span></span>

1. <span data-ttu-id="c2899-303">開啟「Controllers/TodoListController.cs」  檔案。</span><span class="sxs-lookup"><span data-stu-id="c2899-303">Open the *Controllers/TodoListController.cs* file.</span></span>
2. <span data-ttu-id="c2899-304">取消註解用來設定 `trustedCallerClientId` 和 `trustedCallerServicePrincipalId` 的程式行。</span><span class="sxs-lookup"><span data-stu-id="c2899-304">Uncomment the lines that set `trustedCallerClientId` and `trustedCallerServicePrincipalId`.</span></span>
   
        private static string trustedCallerClientId = ConfigurationManager.AppSettings["todo:TrustedCallerClientId"];
        private static string trustedCallerServicePrincipalId = ConfigurationManager.AppSettings["todo:TrustedCallerServicePrincipalId"];
3. <span data-ttu-id="c2899-305">取消註解 CheckCallerId 方法中的程式碼。</span><span class="sxs-lookup"><span data-stu-id="c2899-305">Uncomment the code in the CheckCallerId method.</span></span> <span data-ttu-id="c2899-306">控制器中的每個動作方法開始時會呼叫此方法。</span><span class="sxs-lookup"><span data-stu-id="c2899-306">This method is called at the start of every action method in the controller.</span></span> 
   
        private static void CheckCallerId()
        {
            string currentCallerClientId = ClaimsPrincipal.Current.FindFirst("appid").Value;
            string currentCallerServicePrincipalId = ClaimsPrincipal.Current.FindFirst("http://schemas.microsoft.com/identity/claims/objectidentifier").Value;
            if (currentCallerClientId != trustedCallerClientId || currentCallerServicePrincipalId != trustedCallerServicePrincipalId)
            {
                throw new HttpResponseException(new HttpResponseMessage { StatusCode = HttpStatusCode.Unauthorized, ReasonPhrase = "The appID or service principal ID is not the expected value." });
            }
        }
4. <span data-ttu-id="c2899-307">將 ToDoListDataAPI 專案重新部署至 Azure App Service。</span><span class="sxs-lookup"><span data-stu-id="c2899-307">Redeploy the ToDoListDataAPI project to Azure App Service.</span></span>
5. <span data-ttu-id="c2899-308">在瀏覽器中，移至 AngularJS 前端 Web 應用程式的 HTTPS URL，然後在首頁中按一下 [待辦事項清單]  索引標籤。</span><span class="sxs-lookup"><span data-stu-id="c2899-308">In your browser, go to the AngularJS front end web app's HTTPS URL, and in the home page click the **To Do List** tab.</span></span>
   
    <span data-ttu-id="c2899-309">對後端的呼叫會失敗，因此應用程式不會運作。</span><span class="sxs-lookup"><span data-stu-id="c2899-309">The application doesn't work because calls to the back end are failing.</span></span> <span data-ttu-id="c2899-310">新的程式碼會檢查實際的 appid 和 objectidentifier，但它還沒有正確值可用來對這兩項進行檢查。</span><span class="sxs-lookup"><span data-stu-id="c2899-310">The new code is checking actual appid and objectidentifier but it doesn't yet have the correct values to check them against.</span></span> <span data-ttu-id="c2899-311">瀏覽器的開發人員工具主控台會報告伺服器傳回 HTTP 401 錯誤。</span><span class="sxs-lookup"><span data-stu-id="c2899-311">The browser Developer Tools Console reports that the server is returning an HTTP 401 error.</span></span>
   
    ![開發人員工具主控台中發生錯誤](./media/app-service-api-dotnet-service-principal-auth/webapperror.png)
   
    <span data-ttu-id="c2899-313">在下列步驟中，您將會設定預期值。</span><span class="sxs-lookup"><span data-stu-id="c2899-313">In the following steps you configure the expected values.</span></span>
6. <span data-ttu-id="c2899-314">使用 Azure AD PowerShell，為針對 TodoListWebApp 專案所建立的 Azure AD 應用程式取得服務主體的值。</span><span class="sxs-lookup"><span data-stu-id="c2899-314">Using Azure AD PowerShell, get the value of the service principal for the Azure AD application that you created for the TodoListWebApp project.</span></span>
   
    <span data-ttu-id="c2899-315">a.</span><span class="sxs-lookup"><span data-stu-id="c2899-315">a.</span></span> <span data-ttu-id="c2899-316">有關如何安裝 Azure PowerShell 和連接至訂用帳戶的指示，請參閱[搭配使用 Azure PowerShell 與 Azure Resource Manager](../powershell-azure-resource-manager.md)。</span><span class="sxs-lookup"><span data-stu-id="c2899-316">For instructions on how to install Azure PowerShell and connect to your subscription, see [Using Azure PowerShell with Azure Resource Manager](../powershell-azure-resource-manager.md).</span></span>
   
    <span data-ttu-id="c2899-317">b.這是另一個 C# 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="c2899-317">b.</span></span> <span data-ttu-id="c2899-318">若要取得服務主體清單，請依序執行 `Login-AzureRmAccount` 命令和 `Get-AzureRmADServicePrincipal` 命令。</span><span class="sxs-lookup"><span data-stu-id="c2899-318">To get a list of service principals, execute the `Login-AzureRmAccount` command and then the `Get-AzureRmADServicePrincipal` command.</span></span>
   
    <span data-ttu-id="c2899-319">c.</span><span class="sxs-lookup"><span data-stu-id="c2899-319">c.</span></span> <span data-ttu-id="c2899-320">尋找 TodoListAPI 應用程式之服務主體的 objectid，並將它儲存在您稍後可以從中複製此值的位置。</span><span class="sxs-lookup"><span data-stu-id="c2899-320">Find the objectid for the service principal of the TodoListAPI application, and save it in a location you can copy from later.</span></span>
7. <span data-ttu-id="c2899-321">在 Azure 入口網站中，瀏覽至您部署 ToDoListDataAPI 專案所在之 API 應用程式的 [API 應用程式] 刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="c2899-321">In the Azure portal, navigate to the API app blade for the API app that you deployed the ToDoListDataAPI project to.</span></span>
8. <span data-ttu-id="c2899-322">按一下 [設定] > [應用程式設定]。</span><span class="sxs-lookup"><span data-stu-id="c2899-322">Click **Settings > Application settings**.</span></span>
9. <span data-ttu-id="c2899-323">在 [應用程式設定]  區段中，新增下列金鑰和值：</span><span class="sxs-lookup"><span data-stu-id="c2899-323">In the **App settings** section, add the following keys and values:</span></span>
   
   | <span data-ttu-id="c2899-324">**金鑰**</span><span class="sxs-lookup"><span data-stu-id="c2899-324">**Key**</span></span> | <span data-ttu-id="c2899-325">todo:TrustedCallerServicePrincipalId</span><span class="sxs-lookup"><span data-stu-id="c2899-325">todo:TrustedCallerServicePrincipalId</span></span> |
   | --- | --- |
   | <span data-ttu-id="c2899-326">**值**</span><span class="sxs-lookup"><span data-stu-id="c2899-326">**Value**</span></span> |<span data-ttu-id="c2899-327">呼叫端應用程式的服務主體識別碼</span><span class="sxs-lookup"><span data-stu-id="c2899-327">Service principal id of calling application</span></span> |
   | <span data-ttu-id="c2899-328">**範例**</span><span class="sxs-lookup"><span data-stu-id="c2899-328">**Example**</span></span> |<span data-ttu-id="c2899-329">4f4a94a4-6f0d-4072-4f4a94a4-6f0d-4072</span><span class="sxs-lookup"><span data-stu-id="c2899-329">4f4a94a4-6f0d-4072-4f4a94a4-6f0d-4072</span></span> |
   
   | <span data-ttu-id="c2899-330">**金鑰**</span><span class="sxs-lookup"><span data-stu-id="c2899-330">**Key**</span></span> | <span data-ttu-id="c2899-331">todo:TrustedCallerClientId</span><span class="sxs-lookup"><span data-stu-id="c2899-331">todo:TrustedCallerClientId</span></span> |
   | --- | --- |
   | <span data-ttu-id="c2899-332">**值**</span><span class="sxs-lookup"><span data-stu-id="c2899-332">**Value**</span></span> |<span data-ttu-id="c2899-333">呼叫端應用程式的用戶端識別碼 - 從 TodoListAPI Azure AD 應用程式複製而來</span><span class="sxs-lookup"><span data-stu-id="c2899-333">Client ID of calling application - copied from the TodoListAPI Azure AD application</span></span> |
   | <span data-ttu-id="c2899-334">**範例**</span><span class="sxs-lookup"><span data-stu-id="c2899-334">**Example**</span></span> |<span data-ttu-id="c2899-335">960adec2-b74a-484a-960adec2-b74a-484a</span><span class="sxs-lookup"><span data-stu-id="c2899-335">960adec2-b74a-484a-960adec2-b74a-484a</span></span> |
10. <span data-ttu-id="c2899-336">按一下 [儲存] 。</span><span class="sxs-lookup"><span data-stu-id="c2899-336">Click **Save**.</span></span>
    
     ![按一下 [Save] (儲存)。](./media/app-service-api-dotnet-service-principal-auth/trustedcaller.png)
11. <span data-ttu-id="c2899-338">在瀏覽器中，返回 Web 應用程式的 URL，然後在首頁中按一下 [待辦事項清單]  索引標籤。</span><span class="sxs-lookup"><span data-stu-id="c2899-338">In your browser, return to the web app's URL, and in the home page click the **To Do List** tab.</span></span>
    
     <span data-ttu-id="c2899-339">受信任呼叫端的應用程式識別碼和服務主體識別碼皆為預期值，因此這次應用程式會如預期般運作。</span><span class="sxs-lookup"><span data-stu-id="c2899-339">This time the application works as expected because the trusted caller app ID and service principal ID are the expected values.</span></span>
    
     ![待辦事項清單頁面](./media/app-service-api-dotnet-service-principal-auth/mvchome.png)

## <a name="building-the-projects-from-scratch"></a><span data-ttu-id="c2899-341">從頭建置專案</span><span class="sxs-lookup"><span data-stu-id="c2899-341">Building the projects from scratch</span></span>
<span data-ttu-id="c2899-342">兩個 Web API 專案是透過使用 **Azure API 應用程式** 專案範本並以 ToDoList 控制器取代預設值控制器所建立。</span><span class="sxs-lookup"><span data-stu-id="c2899-342">The two Web API projects were created by using the **Azure API App** project template and replacing the default Values controller with a ToDoList controller.</span></span> <span data-ttu-id="c2899-343">為了在 ToDoListAPI 專案中取得 Azure AD 服務主體權杖，我們已安裝 [.NET 適用的 Active Directory 驗證程式庫 (ADAL)](https://www.nuget.org/packages/Microsoft.IdentityModel.Clients.ActiveDirectory/) NuGet 封裝。</span><span class="sxs-lookup"><span data-stu-id="c2899-343">For acquiring Azure AD service principal tokens in the ToDoListAPI project, the [Active Directory Authentication Library (ADAL) for .NET](https://www.nuget.org/packages/Microsoft.IdentityModel.Clients.ActiveDirectory/) NuGet package was installed.</span></span>

<span data-ttu-id="c2899-344">如需如何使用 ToDoListAngular 之類的 Web API 後端建立 AngularJS 單一頁面應用程式的相關資訊，請參閱[實習實驗室：使用 ASP.NET Web API 和 Angular.js 建置單一頁面應用程式 (SPA)](http://www.asp.net/web-api/overview/getting-started-with-aspnet-web-api/build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs)。</span><span class="sxs-lookup"><span data-stu-id="c2899-344">For information about how to  create an AngularJS single-page application with a Web API back end like ToDoListAngular, see  [Hands On Lab: Build a Single Page Application (SPA) with ASP.NET Web API and Angular.js](http://www.asp.net/web-api/overview/getting-started-with-aspnet-web-api/build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs).</span></span> <span data-ttu-id="c2899-345">如需如何新增 Azure AD 驗證程式碼的相關資訊，請參閱 [使用 Azure AD 保護 AngularJS 單一頁面應用程式](../active-directory/active-directory-devquickstarts-angular.md)。</span><span class="sxs-lookup"><span data-stu-id="c2899-345">For information about how to add Azure AD authentication code, see [Securing AngularJS Single Page Apps with Azure AD](../active-directory/active-directory-devquickstarts-angular.md).</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="c2899-346">疑難排解</span><span class="sxs-lookup"><span data-stu-id="c2899-346">Troubleshooting</span></span>
[!INCLUDE [troubleshooting](../../includes/app-service-api-auth-troubleshooting.md)]

* <span data-ttu-id="c2899-347">請確定不要混淆 ToDoListAPI (中介層) 和 ToDoListDataAPI (資料層)。</span><span class="sxs-lookup"><span data-stu-id="c2899-347">Make sure that you don't confuse ToDoListAPI (middle tier) and ToDoListDataAPI (data tier).</span></span> <span data-ttu-id="c2899-348">例如，您會在本教學課程中將驗證新增至資料層 API 應用程式， **但應用程式金鑰必須來自您為中介層 API 應用程式建立的 Azure AD 應用程式**。</span><span class="sxs-lookup"><span data-stu-id="c2899-348">For example, in this tutorial you add authentication to the data tier API app, **but the app key must come from the Azure AD application that you created for the middle tier API app**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="c2899-349">後續步驟</span><span class="sxs-lookup"><span data-stu-id="c2899-349">Next steps</span></span>
<span data-ttu-id="c2899-350">這是 API Apps 系列的最後一個教學課程。</span><span class="sxs-lookup"><span data-stu-id="c2899-350">This is the last tutorial in the API Apps series.</span></span> 

<span data-ttu-id="c2899-351">如需 Azure Active Directory 的詳細資訊，請參閱下列資源。</span><span class="sxs-lookup"><span data-stu-id="c2899-351">For more information about Azure Active Directory, see the following resources.</span></span>

* [<span data-ttu-id="c2899-352">Azure AD 開發人員指南</span><span class="sxs-lookup"><span data-stu-id="c2899-352">Azure AD developers' guide</span></span>](http://aka.ms/aaddev)
* [<span data-ttu-id="c2899-353">Azure AD 案例</span><span class="sxs-lookup"><span data-stu-id="c2899-353">Azure AD scenarios</span></span>](http://aka.ms/aadscenarios)
* [<span data-ttu-id="c2899-354">Azure AD 範例</span><span class="sxs-lookup"><span data-stu-id="c2899-354">Azure AD samples</span></span>](http://aka.ms/aadsamples)
  
    <span data-ttu-id="c2899-355">[WebApp-WebAPI-OAuth2-AppIdentity-DotNet](http://github.com/AzureADSamples/WebApp-WebAPI-OAuth2-AppIdentity-DotNet) 範例類似於本教學課程中顯示的項目，但是未使用 App Service 驗證。</span><span class="sxs-lookup"><span data-stu-id="c2899-355">The [WebApp-WebAPI-OAuth2-AppIdentity-DotNet](http://github.com/AzureADSamples/WebApp-WebAPI-OAuth2-AppIdentity-DotNet) sample is similar to what is shown in this tutorial, but without using App Service authentication.</span></span>

<span data-ttu-id="c2899-356">如需了解藉由使用 Visual Studio，或是藉由使用[原始檔控制系統](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/source-control)來[自動化部署](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/continuous-integration-and-continuous-delivery)，以將 Visual Studio 專案部署到 API 應用程式的其他方式相關資訊，請參閱[如何部署 Azure App Service 應用程式](../app-service-web/web-sites-deploy.md)。</span><span class="sxs-lookup"><span data-stu-id="c2899-356">For information about other ways to deploy Visual Studio projects to API apps, by using Visual Studio or by [automating deployment](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/continuous-integration-and-continuous-delivery) from a [source control system](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/source-control), see [How to deploy an Azure App Service app](../app-service-web/web-sites-deploy.md).</span></span>

