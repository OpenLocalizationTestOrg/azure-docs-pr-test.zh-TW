---
title: "在 Azure API 管理中使用 OAuth 2.0 授權開發人員帳戶 | Microsoft Docs"
description: "了解如何在 API 管理中使用 OAuth 2.0 來授權給使用者。"
services: api-management
documentationcenter: 
author: steved0x
manager: erikre
editor: 
ms.assetid: 78c48247-64f0-4708-b2d0-98b61a821283
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: apimpm
ms.openlocfilehash: a19c453bb3271374b587f3d0b35adad55863b490
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="how-to-authorize-developer-accounts-using-oauth-20-in-azure-api-management"></a><span data-ttu-id="57c7e-103">如何在 Azure API 管理中使用 OAuth 2.0 授權開發人員帳戶</span><span class="sxs-lookup"><span data-stu-id="57c7e-103">How to authorize developer accounts using OAuth 2.0 in Azure API Management</span></span>
<span data-ttu-id="57c7e-104">許多 API 都支援使用 [OAuth 2.0](http://oauth.net/2/) 來保護 API，並確保只有有效的使用者才能存取，而且他們只能存取獲授權的資源。</span><span class="sxs-lookup"><span data-stu-id="57c7e-104">Many APIs support [OAuth 2.0](http://oauth.net/2/) to secure the API and ensure that only valid users have access, and they can only access resources to which they're entitled.</span></span> <span data-ttu-id="57c7e-105">為了搭配使用 Azure API 管理的互動式開發人員主控台與這類 API，服務可讓您設定服務執行個體來使用已啟用 OAuth 2.0 的 API。</span><span class="sxs-lookup"><span data-stu-id="57c7e-105">In order to use Azure API Management's interactive Developer Console with such APIs, the service allows you to configure your service instance to work with your OAuth 2.0 enabled API.</span></span>

## <span data-ttu-id="57c7e-106"><a name="prerequisites"> </a>必要條件</span><span class="sxs-lookup"><span data-stu-id="57c7e-106"><a name="prerequisites"> </a>Prerequisites</span></span>
<span data-ttu-id="57c7e-107">本指南將示範如何設定 API 管理服務執行個體，以便使用開發人員帳戶適用的 OAuth 2.0 授權，但並未示範如何設定 OAuth 2.0 提供者。</span><span class="sxs-lookup"><span data-stu-id="57c7e-107">This guide shows you how to configure your API Management service instance to use OAuth 2.0 authorization for developer accounts, but does not show you how to configure an OAuth 2.0 provider.</span></span> <span data-ttu-id="57c7e-108">儘管步驟相似，且用來在 API 管理服務執行個體中設定 OAuth 2.0 所需的資訊也相同，但每個 OAuth 2.0 提供者的組態並不相同。</span><span class="sxs-lookup"><span data-stu-id="57c7e-108">The configuration for each OAuth 2.0 provider is different, although the steps are similar, and the required pieces of information used in configuring OAuth 2.0 in your API Management service instance are the same.</span></span> <span data-ttu-id="57c7e-109">本主題演示的範例將 Azure Active Directory 當做 OAuth 2.0 提供者。</span><span class="sxs-lookup"><span data-stu-id="57c7e-109">This topic shows examples using Azure Active Directory as an OAuth 2.0 provider.</span></span>

> [!NOTE]
> <span data-ttu-id="57c7e-110">如需使用 Azure Active Directory 設定 OAuth 2.0 的詳細資訊，請參閱 [WebApp-GraphAPI-DotNet][WebApp-GraphAPI-DotNet] (英文) 範例。</span><span class="sxs-lookup"><span data-stu-id="57c7e-110">For more information on configuring OAuth 2.0 using Azure Active Directory, see the [WebApp-GraphAPI-DotNet][WebApp-GraphAPI-DotNet] sample.</span></span>
> 
> 

## <span data-ttu-id="57c7e-111"><a name="step1"> </a>在 API 管理中設定 OAuth 2.0 授權伺服器</span><span class="sxs-lookup"><span data-stu-id="57c7e-111"><a name="step1"> </a>Configure an OAuth 2.0 authorization server in API Management</span></span>
<span data-ttu-id="57c7e-112">若要開始，請在 API 管理服務的 Azure 入口網站中按一下 [發佈者入口網站]。</span><span class="sxs-lookup"><span data-stu-id="57c7e-112">To get started, click **Publisher portal** in the Azure Portal for your API Management service.</span></span>

![發行者入口網站][api-management-management-console]

> [!NOTE]
> <span data-ttu-id="57c7e-114">如果您尚未建立 API 管理服務執行個體，請參閱[開始使用 Azure API 管理][Get started with Azure API Management]教學課程中的[建立 API 管理服務執行個體][Create an API Management service instance]。</span><span class="sxs-lookup"><span data-stu-id="57c7e-114">If you have not yet created an API Management service instance, see [Create an API Management service instance][Create an API Management service instance] in the [Get started with Azure API Management][Get started with Azure API Management] tutorial.</span></span>
> 
> 

<span data-ttu-id="57c7e-115">從左側的 [API 管理] 功能表按一下 [安全性]，然後依序按一下 [OAuth 2.0] 和 [新增授權伺服器]。</span><span class="sxs-lookup"><span data-stu-id="57c7e-115">Click **Security** from the **API Management** menu on the left, click **OAuth 2.0**, and then click **Add authorization server**.</span></span>

![OAuth 2.0][api-management-oauth2]

<span data-ttu-id="57c7e-117">按一下 [Add authorization server] 後，即會出現新的授權伺服器表單。</span><span class="sxs-lookup"><span data-stu-id="57c7e-117">After clicking **Add authorization server**, the new authorization server form is displayed.</span></span>

![New server][api-management-oauth2-server-1]

<span data-ttu-id="57c7e-119">在 [名稱] 和 [說明] 欄位中輸入名稱和選擇性的說明。</span><span class="sxs-lookup"><span data-stu-id="57c7e-119">Enter a name and an optional description in the **Name** and **Description** fields.</span></span> 

> [!NOTE]
> <span data-ttu-id="57c7e-120">這些欄位可用來在目前的 API 管理服務執行個體中識別 OAuth 2.0 授權伺服器，且欄位的值並非來自 OAuth 2.0 伺服器。</span><span class="sxs-lookup"><span data-stu-id="57c7e-120">These fields are used to identify the OAuth 2.0 authorization server within the current API Management service instance and their values do not come from the OAuth 2.0 server.</span></span>
> 
> 

<span data-ttu-id="57c7e-121">輸入 [用戶端註冊頁面 URL]。</span><span class="sxs-lookup"><span data-stu-id="57c7e-121">Enter the **Client registration page URL**.</span></span> <span data-ttu-id="57c7e-122">此頁面可供使用者建立及管理帳戶，並且會因為使用的 OAuth 2.0 提供者不同而有所差異。</span><span class="sxs-lookup"><span data-stu-id="57c7e-122">This page is where users can create and manage their accounts, and varies depending on the OAuth 2.0 provider used.</span></span> <span data-ttu-id="57c7e-123">[用戶端註冊頁面 URL] 指向使用者可用來建立和設定其對 OAuth 2.0 提供者之專屬帳戶的頁面，而提供者支援使用者帳戶管理。</span><span class="sxs-lookup"><span data-stu-id="57c7e-123">The **Client registration page URL** points to the page that users can use to create and configure their own accounts for OAuth 2.0 providers that support user management of accounts.</span></span> <span data-ttu-id="57c7e-124">即使 OAuth 2.0 提供者支援這項功能，有些組織還是未設定或未使用這項功能。</span><span class="sxs-lookup"><span data-stu-id="57c7e-124">Some organizations do not configure or use this functionality even if the OAuth 2.0 provider supports it.</span></span> <span data-ttu-id="57c7e-125">如果您的 OAuth 2.0 提供者未設定使用者帳戶管理，請在這裡輸入預留位置 URL (例如您公司的 URL) 或 `https://placeholder.contoso.com` 這類 URL。</span><span class="sxs-lookup"><span data-stu-id="57c7e-125">If your OAuth 2.0 provider does not have user management of accounts configured, enter a placeholder URL here such as the URL of your company, or a URL such as `https://placeholder.contoso.com`.</span></span>

<span data-ttu-id="57c7e-126">表單的下一個區段含有 [授權碼授與類型]、[授權端點 URL] 及 [授權要求方法] 等設定。</span><span class="sxs-lookup"><span data-stu-id="57c7e-126">The next section of the form contains the **Authorization code grant types**, **Authorization endpoint URL**, and **Authorization request method** settings.</span></span>

![New server][api-management-oauth2-server-2]

<span data-ttu-id="57c7e-128">勾選需要的類型以指定 [Authorization code grant types]  。</span><span class="sxs-lookup"><span data-stu-id="57c7e-128">Specify the **Authorization code grant types** by checking the desired types.</span></span> <span data-ttu-id="57c7e-129"> 。</span><span class="sxs-lookup"><span data-stu-id="57c7e-129">**Authorization code** is specified by default.</span></span>

<span data-ttu-id="57c7e-130">輸入 [Authorization endpoint URL] 。</span><span class="sxs-lookup"><span data-stu-id="57c7e-130">Enter the **Authorization endpoint URL**.</span></span> <span data-ttu-id="57c7e-131">對於 Azure Active Directory，此 URL 將與下列 URL 相似；其中， `<client_id>` 將取代為向 OAuth 2.0 伺服器識別應用程式的用戶端識別碼。</span><span class="sxs-lookup"><span data-stu-id="57c7e-131">For Azure Active Directory, this URL will be similar to the following URL, where `<client_id>` is replaced with the client id that identifies your application to the OAuth 2.0 server.</span></span>

`https://login.microsoftonline.com/<client_id>/oauth2/authorize`

<span data-ttu-id="57c7e-132">[授權要求方法] 能指定將授權要求傳送到 OAuth 2.0 伺服器的方法。</span><span class="sxs-lookup"><span data-stu-id="57c7e-132">The **Authorization request method** specifies how the authorization request is sent to the OAuth 2.0 server.</span></span> <span data-ttu-id="57c7e-133">預設會選取 **GET**。</span><span class="sxs-lookup"><span data-stu-id="57c7e-133">By default **GET** is selected.</span></span>

<span data-ttu-id="57c7e-134">下一個區段是指定 [權杖端點 URL]、[用戶端驗證方法]、[存取權杖傳送方法] 及 [預設範圍] 的地方。</span><span class="sxs-lookup"><span data-stu-id="57c7e-134">The next section is where the **Token endpoint URL**, **Client authentication methods**, **Access token sending method**, and **Default scope** are specified.</span></span>

![New server][api-management-oauth2-server-3]

<span data-ttu-id="57c7e-136">對於 Azure Active Directory OAuth 2.0 伺服器，[權杖端點 URL] 將具有以下格式；其中 `<APPID>` 的格式為 `yourapp.onmicrosoft.com`。</span><span class="sxs-lookup"><span data-stu-id="57c7e-136">For an Azure Active Directory OAuth 2.0 server, the **Token endpoint URL** will have the following format, where `<APPID>`  has the format of `yourapp.onmicrosoft.com`.</span></span>

`https://login.microsoftonline.com/<APPID>/oauth2/token`

<span data-ttu-id="57c7e-137">[用戶端驗證方法] 的預設設定是 [基本]，而 [存取權杖傳送方法] 則是 [授權標頭]。</span><span class="sxs-lookup"><span data-stu-id="57c7e-137">The default setting for **Client authentication methods** is **Basic**, and  **Access token sending method** is **Authorization header**.</span></span> <span data-ttu-id="57c7e-138">這些值和 [預設範圍] 均是在此表單區段設定的。</span><span class="sxs-lookup"><span data-stu-id="57c7e-138">These values are configured on this section of the form, along with the **Default scope**.</span></span>

<span data-ttu-id="57c7e-139">[用戶端認證] 區段含有 [用戶端識別碼] 和 [用戶端密碼]，這兩個項目可在 OAuth 2.0 伺服器的建立和組態程序中取得。</span><span class="sxs-lookup"><span data-stu-id="57c7e-139">The **Client credentials** section contains the **Client ID** and **Client secret**, which are obtained during the creation and configuration process of your OAuth 2.0 server.</span></span> <span data-ttu-id="57c7e-140">指定 [用戶端識別碼] 和 [用戶端密碼] 後，系統便會產生 [授權碼] 的 **redirect_uri**。</span><span class="sxs-lookup"><span data-stu-id="57c7e-140">Once the **Client ID** and **Client secret** are specified, the **redirect_uri** for the **authorization code** is generated.</span></span> <span data-ttu-id="57c7e-141">此 URI 可用來設定 OAuth 2.0 伺服器組態中的回覆 URL。</span><span class="sxs-lookup"><span data-stu-id="57c7e-141">This URI is used to configure the reply URL in your OAuth 2.0 server configuration.</span></span>

![New server][api-management-oauth2-server-4]

<span data-ttu-id="57c7e-143">如果將 [授權碼授與類型] 設定為 [資源擁有者密碼]，您便需要使用 [資源擁有者密碼認證] 區段來指定認證，若不想這麼做，則可以將授與類型保持空白。</span><span class="sxs-lookup"><span data-stu-id="57c7e-143">If **Authorization code grant types** is set to **Resource owner password**, the **Resource owner password credentials** section is used to specify those credentials; otherwise you can leave it blank.</span></span>

![New server][api-management-oauth2-server-5]

<span data-ttu-id="57c7e-145">完成表單後，按一下 [儲存]  以儲存 API 管理 OAuth 2.0 授權伺服器組態。</span><span class="sxs-lookup"><span data-stu-id="57c7e-145">Once the form is complete, click **Save** to save the API Management OAuth 2.0 authorization server configuration.</span></span> <span data-ttu-id="57c7e-146">儲存伺服器組態後，您便可以設定 API 以使用此組態，如下一個小節所述。</span><span class="sxs-lookup"><span data-stu-id="57c7e-146">Once the server configuration is saved, you can configure APIs to use this configuration, as shown in the next section.</span></span>

## <span data-ttu-id="57c7e-147"><a name="step2"> </a>設定 API 以使用 OAuth 2.0 使用者授權</span><span class="sxs-lookup"><span data-stu-id="57c7e-147"><a name="step2"> </a>Configure an API to use OAuth 2.0 user authorization</span></span>
<span data-ttu-id="57c7e-148">從左側的 [API 管理] 功能表按一下 [API]，接著依序按一下所需之 API 的名稱和 [安全性]，然後勾選 [OAuth 2.0] 的方塊。</span><span class="sxs-lookup"><span data-stu-id="57c7e-148">Click **APIs** from the **API Management** menu on the left, click the name of the desired API, click **Security**, and then check the box for **OAuth 2.0**.</span></span>

![User authorization][api-management-user-authorization]

<span data-ttu-id="57c7e-150">從下拉式清單選取需要的 [授權伺服器]，然後按一下 [儲存]。</span><span class="sxs-lookup"><span data-stu-id="57c7e-150">Select the desired **Authorization server** from the drop-down list, and click **Save**.</span></span>

![User authorization][api-management-user-authorization-save]

## <span data-ttu-id="57c7e-152"><a name="step3"> </a>在開發人員入口網站中測試 OAuth 2.0 使用者授權</span><span class="sxs-lookup"><span data-stu-id="57c7e-152"><a name="step3"> </a>Test the OAuth 2.0 user authorization in the Developer Portal</span></span>
<span data-ttu-id="57c7e-153">設定好 OAuth 2.0 授權伺服器並將 API 設定為使用該伺服器後，您可以前往開發人員入口網站並呼叫 API 來進行測試。</span><span class="sxs-lookup"><span data-stu-id="57c7e-153">Once you have configured your OAuth 2.0 authorization server and configured your API to use that server, you can test it by going to the Developer Portal and calling an API.</span></span>  <span data-ttu-id="57c7e-154">按一下右上方功能表的 [開發人員入口網站]  。</span><span class="sxs-lookup"><span data-stu-id="57c7e-154">Click **Developer portal** in the top right menu.</span></span>

![開發人員入口網站][api-management-developer-portal-menu]

<span data-ttu-id="57c7e-156">在上方功能表中按一下 [API]，然後選取 [Echo API]。</span><span class="sxs-lookup"><span data-stu-id="57c7e-156">Click **APIs** in the top menu and select **Echo API**.</span></span>

![Echo API][api-management-apis-echo-api]

> [!NOTE]
> <span data-ttu-id="57c7e-158">如果您的帳戶只設定或只看見一個 API，按一下 API 將帶您直接前往該 API 的作業。</span><span class="sxs-lookup"><span data-stu-id="57c7e-158">If you have only one API configured or visible to your account, then clicking APIs takes you directly to the operations for that API.</span></span>
> 
> 

<span data-ttu-id="57c7e-159">選取 [GET 資源] 作業、按一下 [開啟主控台]，然後從下拉式功能表選取 [授權碼]。</span><span class="sxs-lookup"><span data-stu-id="57c7e-159">Select the **GET Resource** operation, click **Open Console**, and then select **Authorization code** from the drop-down.</span></span>

![Open console][api-management-open-console]

<span data-ttu-id="57c7e-161">選取 [授權碼]  時，系統會顯示含有 OAuth 2.0 提供者之登入表單的快顯視窗。</span><span class="sxs-lookup"><span data-stu-id="57c7e-161">When **Authorization code** is selected, a pop-up window is displayed with the sign-in form of the OAuth 2.0 provider.</span></span> <span data-ttu-id="57c7e-162">在此範例中，登入表單是由 Azure Active Directory 提供。</span><span class="sxs-lookup"><span data-stu-id="57c7e-162">In this example the sign-in form is provided by Azure Active Directory.</span></span>

> [!NOTE]
> <span data-ttu-id="57c7e-163">如果已停用快顯視窗，瀏覽器會提示您加以啟用。</span><span class="sxs-lookup"><span data-stu-id="57c7e-163">If you have pop-ups disabled you will be prompted to enable them by the browser.</span></span> <span data-ttu-id="57c7e-164">啟用後，請再次選取 [授權碼]  ，系統就會顯示登入表單。</span><span class="sxs-lookup"><span data-stu-id="57c7e-164">After you enable them, select **Authorization code** again and the sign-in form will be displayed.</span></span>
> 
> 

![Sign in][api-management-oauth2-signin]

<span data-ttu-id="57c7e-166">登入後，系統會將授權要求的 `Authorization : Bearer` 標頭填入 [要求標頭]。</span><span class="sxs-lookup"><span data-stu-id="57c7e-166">Once you have signed in, the **Request headers** are populated with an `Authorization : Bearer` header that authorizes the request.</span></span>

![Request header token][api-management-request-header-token]

<span data-ttu-id="57c7e-168">此時，您可以針對剩餘的參數設定需要的值，然後再提交要求。</span><span class="sxs-lookup"><span data-stu-id="57c7e-168">At this point you can configure the desired values for the remaining parameters, and submit the request.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="57c7e-169">後續步驟</span><span class="sxs-lookup"><span data-stu-id="57c7e-169">Next steps</span></span>
<span data-ttu-id="57c7e-170">如需使用 OAuth 2.0 和 API 管理的詳細資訊，請參閱下列影片以及隨附的 [文章](api-management-howto-protect-backend-with-aad.md)。</span><span class="sxs-lookup"><span data-stu-id="57c7e-170">For more information about using OAuth 2.0 and API Management, see the following video and accompanying [article](api-management-howto-protect-backend-with-aad.md).</span></span>

> [!VIDEO https://channel9.msdn.com/Blogs/AzureApiMgmt/Protecting-Web-API-Backend-with-Azure-Active-Directory-and-API-Management/player]
> 
> 

[api-management-management-console]: ./media/api-management-howto-oauth2/api-management-management-console.png
[api-management-oauth2]: ./media/api-management-howto-oauth2/api-management-oauth2.png
[api-management-user-authorization]: ./media/api-management-howto-oauth2/api-management-user-authorization.png
[api-management-user-authorization-save]: ./media/api-management-howto-oauth2/api-management-user-authorization-save.png
[api-management-oauth2-signin]: ./media/api-management-howto-oauth2/api-management-oauth2-signin.png
[api-management-request-header-token]: ./media/api-management-howto-oauth2/api-management-request-header-token.png
[api-management-developer-portal-menu]: ./media/api-management-howto-oauth2/api-management-developer-portal-menu.png
[api-management-open-console]: ./media/api-management-howto-oauth2/api-management-open-console.png
[api-management-oauth2-server-1]: ./media/api-management-howto-oauth2/api-management-oauth2-server-1.png
[api-management-oauth2-server-2]: ./media/api-management-howto-oauth2/api-management-oauth2-server-2.png
[api-management-oauth2-server-3]: ./media/api-management-howto-oauth2/api-management-oauth2-server-3.png
[api-management-oauth2-server-4]: ./media/api-management-howto-oauth2/api-management-oauth2-server-4.png
[api-management-oauth2-server-5]: ./media/api-management-howto-oauth2/api-management-oauth2-server-5.png
[api-management-apis-echo-api]: ./media/api-management-howto-oauth2/api-management-apis-echo-api.png


[How to add operations to an API]: api-management-howto-add-operations.md
[How to add and publish a product]: api-management-howto-add-products.md
[Monitoring and analytics]: api-management-monitoring.md
[Add APIs to a product]: api-management-howto-add-products.md#add-apis
[Publish a product]: api-management-howto-add-products.md#publish-product
[Get started with Azure API Management]: api-management-get-started.md
[API Management policy reference]: api-management-policy-reference.md
[Caching policies]: api-management-policy-reference.md#caching-policies
[Create an API Management service instance]: api-management-get-started.md#create-service-instance

[http://oauth.net/2/]: http://oauth.net/2/
[WebApp-GraphAPI-DotNet]: https://github.com/AzureADSamples/WebApp-GraphAPI-DotNet

[Prerequisites]: #prerequisites
[Configure an OAuth 2.0 authorization server in API Management]: #step1
[Configure an API to use OAuth 2.0 user authorization]: #step2
[Test the OAuth 2.0 user authorization in the Developer Portal]: #step3
[Next steps]: #next-steps

