---
title: "使用 Azure Active Directory B2C 授權開發人員帳戶 - Azure API 管理 | Microsoft Docs"
description: "了解如何在 API 管理中使用 Azure Active Directory B2C 授權使用者。"
services: api-management
documentationcenter: API Management
author: miaojiang
manager: erikre
editor: 
ms.assetid: 33a69a83-94f2-4e4e-9cef-f2a5af3c9732
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: apimpm
ms.openlocfilehash: eb7deb1a79d9db9ac5cfbea69b8d3c564eb55577
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-authorize-developer-accounts-by-using-azure-active-directory-b2c-in-azure-api-management"></a><span data-ttu-id="c84e2-103">如何在 Azure API 管理中使用 Azure Active Directory B2C 授權開發人員帳戶</span><span class="sxs-lookup"><span data-stu-id="c84e2-103">How to authorize developer accounts by using Azure Active Directory B2C in Azure API Management</span></span>
## <a name="overview"></a><span data-ttu-id="c84e2-104">概觀</span><span class="sxs-lookup"><span data-stu-id="c84e2-104">Overview</span></span>
<span data-ttu-id="c84e2-105">Azure Active Directory B2C 是適用於取用者導向 Web 與行動應用程式的雲端身分識別管理解決方案。</span><span class="sxs-lookup"><span data-stu-id="c84e2-105">Azure Active Directory B2C is a cloud identity management solution for consumer-facing web and mobile applications.</span></span> <span data-ttu-id="c84e2-106">您可以使用它來管理開發人員入口網站的存取。</span><span class="sxs-lookup"><span data-stu-id="c84e2-106">You can use it to manage access to your developer portal.</span></span> <span data-ttu-id="c84e2-107">本指南會說明要與 Azure Active Directory B2C 整合所必須在 API 管理服務中進行的設定。</span><span class="sxs-lookup"><span data-stu-id="c84e2-107">This guide shows you the configuration that's required in your API Management service to integrate with Azure Active Directory B2C.</span></span> <span data-ttu-id="c84e2-108">如需實現使用傳統 Azure Active Directory 來存取開發人員入口網站的相關資訊，請參閱[如何使用 Azure Active Directory 授權開發人員帳戶]。</span><span class="sxs-lookup"><span data-stu-id="c84e2-108">For information about enabling access to the developer portal by using classic Azure Active Directory, see [How to authorize developer accounts using Azure Active Directory].</span></span>

> [!NOTE]
> <span data-ttu-id="c84e2-109">若要完成本指南中的步驟，您必須先具備要在其中建立應用程式的 Azure Active Directory B2C 租用戶。</span><span class="sxs-lookup"><span data-stu-id="c84e2-109">To complete the steps in this guide, you must first have an Azure Active Directory B2C tenant to create an application in.</span></span> <span data-ttu-id="c84e2-110">您還必須備妥註冊和登入原則。</span><span class="sxs-lookup"><span data-stu-id="c84e2-110">Also, you need to have signup and signin policies ready.</span></span> <span data-ttu-id="c84e2-111">如需詳細資訊，請參閱 [Azure Active Directory B2C 概觀]。</span><span class="sxs-lookup"><span data-stu-id="c84e2-111">For more information, see [Azure Active Directory B2C overview].</span></span>

## <a name="authorize-developer-accounts-by-using-azure-active-directory-b2c"></a><span data-ttu-id="c84e2-112">使用 Azure Active Directory B2C 授權開發人員帳戶</span><span class="sxs-lookup"><span data-stu-id="c84e2-112">Authorize developer accounts by using Azure Active Directory B2C</span></span>

1. <span data-ttu-id="c84e2-113">若要開始，請在 API 管理服務的 Azure 入口網站中按一下 [發佈者入口網站]。</span><span class="sxs-lookup"><span data-stu-id="c84e2-113">To get started, click **Publisher portal** in the Azure portal for your API Management service.</span></span> <span data-ttu-id="c84e2-114">這會帶您前往 API 管理發行者入口網站。</span><span class="sxs-lookup"><span data-stu-id="c84e2-114">This takes you to the API Management publisher portal.</span></span>

   ![發行者入口網站][api-management-management-console]

   > [!NOTE]
   > <span data-ttu-id="c84e2-116">如果您尚未建立 API 管理服務執行個體，請參閱[開始使用 Azure API 管理教學課程][Get started with Azure API Management]中的[建立 API 管理服務執行個體][Create an API Management service instance]。</span><span class="sxs-lookup"><span data-stu-id="c84e2-116">If you haven't yet created an API Management service instance, see [Create an API Management service instance][Create an API Management service instance] in the [Get started with Azure API Management tutorial][Get started with Azure API Management].</span></span>

2. <span data-ttu-id="c84e2-117">在 [API 管理] 功能表上，按一下 [安全性]。</span><span class="sxs-lookup"><span data-stu-id="c84e2-117">On the **API Management** menu, click **Security**.</span></span> <span data-ttu-id="c84e2-118">在 [身分識別] 索引標籤上，選擇 [Azure Active Directory B2C]。</span><span class="sxs-lookup"><span data-stu-id="c84e2-118">On the **Identities** tab, choose **Azure Active Directory B2C**.</span></span>

  ![外部身分識別 1][api-management-howto-aad-b2c-security-tab]

3. <span data-ttu-id="c84e2-120">記下 [重新導向 URL]，然後切換到 Azure 入口網站中的 Azure Active Directory B2C。</span><span class="sxs-lookup"><span data-stu-id="c84e2-120">Make a note of the **Redirect URL** and switch over to Azure Active Directory B2C in the Azure portal.</span></span>

  ![外部身分識別 2][api-management-howto-aad-b2c-security-tab-reply-url]

4. <span data-ttu-id="c84e2-122">按一下 [應用程式] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="c84e2-122">Click the **Applications** button.</span></span>

  ![註冊新的應用程式 1][api-management-howto-aad-b2c-portal-menu]

5. <span data-ttu-id="c84e2-124">按一下 [新增] 按鈕以建立新的 Azure Active Directory B2C 應用程式。</span><span class="sxs-lookup"><span data-stu-id="c84e2-124">Click the **Add** button to create a new Azure Active Directory B2C application.</span></span>

  ![註冊新的應用程式 2][api-management-howto-aad-b2c-add-button]

6. <span data-ttu-id="c84e2-126">在 [新增應用程式] 刀鋒視窗中，輸入應用程式的名稱。</span><span class="sxs-lookup"><span data-stu-id="c84e2-126">In the **New application** blade, enter a name for the application.</span></span> <span data-ttu-id="c84e2-127">在 [Web 應用程式/Web API] 下選擇 [是]，然後在 [允許隱含流程] 下選擇 [是]。</span><span class="sxs-lookup"><span data-stu-id="c84e2-127">Choose **Yes** under **Web App/Web API**, and choose **Yes** under **Allow implicit flow**.</span></span> <span data-ttu-id="c84e2-128">然後，從發佈者入口網站中 [身分識別] 索引標籤的 [Azure Active Directory B2C] 區段，複製 [重新導向 URL] 並貼到 [回覆 URL] 文字方塊。</span><span class="sxs-lookup"><span data-stu-id="c84e2-128">Then copy the **Redirect URL** from the **Azure Active Directory B2C** section of the **Identities** tab in the publisher portal, and paste it into the **Reply URL** text box.</span></span>

  ![註冊新的應用程式 3][api-management-howto-aad-b2c-app-details]

7. <span data-ttu-id="c84e2-130">按一下 [ **建立** ] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="c84e2-130">Click the **Create** button.</span></span> <span data-ttu-id="c84e2-131">應用程式在建立後會出現在 [應用程式] 刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="c84e2-131">When the application is created, it appears in the **Applications** blade.</span></span> <span data-ttu-id="c84e2-132">按一下應用程式名稱可查看其詳細資料。</span><span class="sxs-lookup"><span data-stu-id="c84e2-132">Click the application name to see its details.</span></span>

  ![註冊新的應用程式 4][api-management-howto-aad-b2c-app-created]

8. <span data-ttu-id="c84e2-134">從 [屬性] 刀鋒視窗複製 [應用程式識別碼] 到剪貼簿。</span><span class="sxs-lookup"><span data-stu-id="c84e2-134">From the **Properties** blade, copy the **Application ID** to the clipboard.</span></span>

  ![應用程式識別碼 1][api-management-howto-aad-b2c-app-id]

9. <span data-ttu-id="c84e2-136">切換回發佈者入口網站，並將識別碼貼到 [用戶端識別碼] 文字方塊。</span><span class="sxs-lookup"><span data-stu-id="c84e2-136">Switch back to the publisher portal and paste the ID into the **Client Id** text box.</span></span>

  ![應用程式識別碼 2][api-management-howto-aad-b2c-client-id]

10. <span data-ttu-id="c84e2-138">切換回 Azure 入口網站，按一下 [金鑰] 按鈕，然後按一下 [產生金鑰]。</span><span class="sxs-lookup"><span data-stu-id="c84e2-138">Switch back to the Azure portal, click the **Keys** button, and then click **Generate key**.</span></span> <span data-ttu-id="c84e2-139">按一下 [儲存] 以儲存組態並顯示**應用程式金鑰**。</span><span class="sxs-lookup"><span data-stu-id="c84e2-139">Click **Save** to save the configuration and display the **App key**.</span></span> <span data-ttu-id="c84e2-140">複製金鑰至剪貼簿。</span><span class="sxs-lookup"><span data-stu-id="c84e2-140">Copy the key to the clipboard.</span></span>

  ![應用程式金鑰 1][api-management-howto-aad-b2c-app-key]

11. <span data-ttu-id="c84e2-142">切換回發行者入口網站，並將金鑰貼上至 [ **用戶端密碼** ] 文字方塊。</span><span class="sxs-lookup"><span data-stu-id="c84e2-142">Switch back to the publisher portal and paste the key into the **Client Secret** text box.</span></span>

  ![應用程式金鑰 2][api-management-howto-aad-b2c-client-secret]

12. <span data-ttu-id="c84e2-144">在 [允許的租用戶] 中，指定 Azure Active Directory B2C 租用戶的網域名稱。</span><span class="sxs-lookup"><span data-stu-id="c84e2-144">Specify the domain name of the Azure Active Directory B2C tenant in **Allowed Tenant**.</span></span>

  ![允許的租用戶][api-management-howto-aad-b2c-allowed-tenant]

13. <span data-ttu-id="c84e2-146">指定 [註冊原則] 和 [登入原則]。</span><span class="sxs-lookup"><span data-stu-id="c84e2-146">Specify the **Signup Policy** and **Signin Policy**.</span></span> <span data-ttu-id="c84e2-147">(選擇性) 您也可以提供 [設定檔編輯原則] 和 [密碼重設原則]。</span><span class="sxs-lookup"><span data-stu-id="c84e2-147">Optionally, you can also provide the **Profile Editing Policy** and **Password Reset Policy**.</span></span>

  ![原則][api-management-howto-aad-b2c-policies]

  > [!NOTE]
  > <span data-ttu-id="c84e2-149">如需原則的詳細資訊，請參閱 [Azure Active Directory B2C：可延伸的原則架構]。</span><span class="sxs-lookup"><span data-stu-id="c84e2-149">For more information on policies, see [Azure Active Directory B2C: Extensible policy framework].</span></span>

14. <span data-ttu-id="c84e2-150">指定需要的組態之後，按一下 [儲存]。</span><span class="sxs-lookup"><span data-stu-id="c84e2-150">After you've specified the desired configuration, click **Save**.</span></span>

  <span data-ttu-id="c84e2-151">儲存變更後，開發人員就可以使用 Azure Active Directory B2C 建立新帳戶和登入開發人員入口網站。</span><span class="sxs-lookup"><span data-stu-id="c84e2-151">After the changes are saved, developers will be able to create new accounts and sign in to the developer portal by using Azure Active Directory B2C.</span></span>

## <a name="sign-up-for-a-developer-account-by-using-azure-active-directory-b2c"></a><span data-ttu-id="c84e2-152">使用 Azure Active Directory B2C 註冊開發人員帳戶</span><span class="sxs-lookup"><span data-stu-id="c84e2-152">Sign up for a developer account by using Azure Active Directory B2C</span></span>

1. <span data-ttu-id="c84e2-153">若要使用 Azure Active Directory B2C 註冊開發人員帳戶，請開啟新的瀏覽器視窗並移至開發人員入口網站。</span><span class="sxs-lookup"><span data-stu-id="c84e2-153">To sign up for a developer account by using Azure Active Directory B2C, open a new browser window and go to the developer portal.</span></span> <span data-ttu-id="c84e2-154">按一下 [註冊] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="c84e2-154">Click the **Sign up** button.</span></span>

   ![開發人員入口網站 1][api-management-howto-aad-b2c-dev-portal]

2. <span data-ttu-id="c84e2-156">選擇使用 [Azure Active Directory B2C] 進行註冊。</span><span class="sxs-lookup"><span data-stu-id="c84e2-156">Choose to sign up with **Azure Active Directory B2C**.</span></span>

   ![開發人員入口網站 2][api-management-howto-aad-b2c-dev-portal-b2c-button]

3. <span data-ttu-id="c84e2-158">系統會將您重新導向至您在上一節中設定的註冊原則。</span><span class="sxs-lookup"><span data-stu-id="c84e2-158">You're redirected to the signup policy that you configured in the previous section.</span></span> <span data-ttu-id="c84e2-159">選擇使用電子郵件地址或其中一個現有的社交帳戶登入。</span><span class="sxs-lookup"><span data-stu-id="c84e2-159">Choose to sign up by using your email address or one of your existing social accounts.</span></span>

   > [!NOTE]
   > <span data-ttu-id="c84e2-160">如果 Azure Active Directory B2C 是發佈者入口網站的 [身分識別] 索引標籤上唯一啟用的選項，系統會直接將您重新導向至註冊原則。</span><span class="sxs-lookup"><span data-stu-id="c84e2-160">If Azure Active Directory B2C is the only option that's enabled on the **Identities** tab in the publisher portal, you'll be redirected to the signup policy directly.</span></span>

   ![開發人員入口網站][api-management-howto-aad-b2c-dev-portal-b2c-options]

   <span data-ttu-id="c84e2-162">註冊完成後，系統會將您重新導向回到開發人員入口網站。</span><span class="sxs-lookup"><span data-stu-id="c84e2-162">When the signup is complete, you're redirected back to the developer portal.</span></span> <span data-ttu-id="c84e2-163">您現在已登入 API 管理服務執行個體的開發人員入口網站。</span><span class="sxs-lookup"><span data-stu-id="c84e2-163">You're now signed in to the developer portal for your API Management service instance.</span></span>

    ![註冊完成][api-management-registration-complete]

## <a name="next-steps"></a><span data-ttu-id="c84e2-165">後續步驟</span><span class="sxs-lookup"><span data-stu-id="c84e2-165">Next steps</span></span>

*  <span data-ttu-id="c84e2-166">[Azure Active Directory B2C 概觀]</span><span class="sxs-lookup"><span data-stu-id="c84e2-166">[Azure Active Directory B2C overview]</span></span>
*  <span data-ttu-id="c84e2-167">[Azure Active Directory B2C：可延伸的原則架構]</span><span class="sxs-lookup"><span data-stu-id="c84e2-167">[Azure Active Directory B2C: Extensible policy framework]</span></span>
*  <span data-ttu-id="c84e2-168">[使用 Microsoft 帳戶做為 Azure Active Directory B2C 中的身分識別提供者]</span><span class="sxs-lookup"><span data-stu-id="c84e2-168">[Use a Microsoft account as an identity provider in Azure Active Directory B2C]</span></span>
*  <span data-ttu-id="c84e2-169">[使用 Google 帳戶做為 Azure Active Directory B2C 中的身分識別提供者]</span><span class="sxs-lookup"><span data-stu-id="c84e2-169">[Use a Google account as an identity provider in Azure Active Directory B2C]</span></span>
*  <span data-ttu-id="c84e2-170">[使用 Linkedin 帳戶做為 Azure Active Directory B2C 中的身分識別提供者]</span><span class="sxs-lookup"><span data-stu-id="c84e2-170">[Use a LinkedIn account as an identity provider in Azure Active Directory B2C]</span></span>
*  <span data-ttu-id="c84e2-171">[使用 Facebook 帳戶做為 Azure Active Directory B2C 中的身分識別提供者]</span><span class="sxs-lookup"><span data-stu-id="c84e2-171">[Use a Facebook account as an identity provider in Azure Active Directory B2C]</span></span>




[api-management-howto-aad-b2c-security-tab]: ./media/api-management-howto-aad-b2c/api-management-b2c-security-tab.PNG
[api-management-howto-aad-b2c-security-tab-reply-url]: ./media/api-management-howto-aad-b2c/api-management-b2c-security-tab-reply-url.PNG
[api-management-howto-aad-b2c-portal-menu]: ./media/api-management-howto-aad-b2c/api-management-b2c-portal-menu.PNG
[api-management-howto-aad-b2c-add-button]: ./media/api-management-howto-aad-b2c/api-management-b2c-add-button.PNG
[api-management-howto-aad-b2c-app-details]: ./media/api-management-howto-aad-b2c/api-management-b2c-app-details.PNG
[api-management-howto-aad-b2c-app-created]: ./media/api-management-howto-aad-b2c/api-management-b2c-app-created.PNG
[api-management-howto-aad-b2c-app-id]: ./media/api-management-howto-aad-b2c/api-management-b2c-app-id.PNG
[api-management-howto-aad-b2c-client-id]: ./media/api-management-howto-aad-b2c/api-management-b2c-client-id.PNG
[api-management-howto-aad-b2c-app-key]: ./media/api-management-howto-aad-b2c/api-management-b2c-app-key.PNG
[api-management-howto-aad-b2c-app-key-saved]: ./media/api-management-howto-aad-b2c/api-management-b2c-app-key-saved.PNG
[api-management-howto-aad-b2c-client-secret]: ./media/api-management-howto-aad-b2c/api-management-b2c-client-secret.PNG
[api-management-howto-aad-b2c-allowed-tenant]: ./media/api-management-howto-aad-b2c/api-management-b2c-allowed-tenant.PNG
[api-management-howto-aad-b2c-policies]: ./media/api-management-howto-aad-b2c/api-management-b2c-policies.PNG
[api-management-howto-aad-b2c-dev-portal]: ./media/api-management-howto-aad-b2c/api-management-b2c-dev-portal.PNG
[api-management-howto-aad-b2c-dev-portal-b2c-button]: ./media/api-management-howto-aad-b2c/api-management-b2c-dev-portal-b2c-button.PNG
[api-management-howto-aad-b2c-dev-portal-b2c-options]: ./media/api-management-howto-aad-b2c/api-management-b2c-dev-portal-b2c-options.PNG
[api-management-complete-registration]: ./media/api-management-howto-aad/api-management-complete-registration.PNG
[api-management-registration-complete]: ./media/api-management-howto-aad/api-management-registration-complete.png

[api-management-management-console]: ./media/api-management-howto-aad/api-management-management-console.png
[api-management-security-external-identities]: ./media/api-management-howto-aad/api-management-b2c-security-tab.png
[api-management-security-aad-new]: ./media/api-management-howto-aad/api-management-security-aad-new.png
[api-management-new-aad-application-menu]: ./media/api-management-howto-aad/api-management-new-aad-application-menu.png
[api-management-new-aad-application-1]: ./media/api-management-howto-aad/api-management-new-aad-application-1.png
[api-management-new-aad-application-2]: ./media/api-management-howto-aad/api-management-new-aad-application-2.png
[api-management-new-aad-app-created]: ./media/api-management-howto-aad/api-management-new-aad-app-created.png
[api-management-aad-app-permissions]: ./media/api-management-howto-aad/api-management-aad-app-permissions.png
[api-management-aad-app-client-id]: ./media/api-management-howto-aad/api-management-aad-app-client-id.png
[api-management-client-id]: ./media/api-management-howto-aad/api-management-client-id.png
[api-management-aad-key-before-save]: ./media/api-management-howto-aad/api-management-aad-key-before-save.png
[api-management-aad-key-after-save]: ./media/api-management-howto-aad/api-management-aad-key-after-save.png
[api-management-client-secret]: ./media/api-management-howto-aad/api-management-client-secret.png
[api-management-client-allowed-tenants]: ./media/api-management-howto-aad/api-management-client-allowed-tenants.png
[api-management-client-allowed-tenants-save]: ./media/api-management-howto-aad/api-management-client-allowed-tenants-save.png
[api-management-aad-delegated-permissions]: ./media/api-management-howto-aad/api-management-aad-delegated-permissions.png
[api-management-dev-portal-signin]: ./media/api-management-howto-aad/api-management-dev-portal-signin.png
[api-management-aad-signin]: ./media/api-management-howto-aad/api-management-aad-signin.png
[api-management-aad-app-multi-tenant]: ./media/api-management-howto-aad/api-management-aad-app-multi-tenant.png
[api-management-aad-reply-url]: ./media/api-management-howto-aad/api-management-aad-reply-url.png
[api-management-permissions-form]: ./media/api-management-howto-aad/api-management-permissions-form.png
[api-management-configure-product]: ./media/api-management-howto-aad/api-management-configure-product.png
[api-management-add-groups]: ./media/api-management-howto-aad/api-management-add-groups.png
[api-management-select-group]: ./media/api-management-howto-aad/api-management-select-group.png
[api-management-aad-groups-list]: ./media/api-management-howto-aad/api-management-aad-groups-list.png
[api-management-aad-group-added]: ./media/api-management-howto-aad/api-management-aad-group-added.png
[api-management-groups]: ./media/api-management-howto-aad/api-management-groups.png
[api-management-edit-group]: ./media/api-management-howto-aad/api-management-edit-group.png

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
[Accessing the Graph API]: http://msdn.microsoft.com/library/azure/dn132599.aspx#BKMK_Graph
<span data-ttu-id="c84e2-172">[Azure Active Directory B2C 概觀]: https://docs.microsoft.com/azure/active-directory-b2c/active-directory-b2c-overview</span><span class="sxs-lookup"><span data-stu-id="c84e2-172">[Azure Active Directory B2C overview]: https://docs.microsoft.com/azure/active-directory-b2c/active-directory-b2c-overview</span></span>
<span data-ttu-id="c84e2-173">[如何使用 Azure Active Directory 授權開發人員帳戶]: https://docs.microsoft.com/azure/api-management/api-management-howto-aad</span><span class="sxs-lookup"><span data-stu-id="c84e2-173">[How to authorize developer accounts using Azure Active Directory]: https://docs.microsoft.com/azure/api-management/api-management-howto-aad</span></span>
<span data-ttu-id="c84e2-174">[Azure Active Directory B2C：可延伸的原則架構]: https://docs.microsoft.com/azure/active-directory-b2c/active-directory-b2c-reference-policies</span><span class="sxs-lookup"><span data-stu-id="c84e2-174">[Azure Active Directory B2C: Extensible policy framework]: https://docs.microsoft.com/azure/active-directory-b2c/active-directory-b2c-reference-policies</span></span>
<span data-ttu-id="c84e2-175">[使用 Microsoft 帳戶做為 Azure Active Directory B2C 中的身分識別提供者]: https://docs.microsoft.com/azure/active-directory-b2c/active-directory-b2c-setup-msa-app</span><span class="sxs-lookup"><span data-stu-id="c84e2-175">[Use a Microsoft account as an identity provider in Azure Active Directory B2C]: https://docs.microsoft.com/azure/active-directory-b2c/active-directory-b2c-setup-msa-app</span></span>
<span data-ttu-id="c84e2-176">[使用 Google 帳戶做為 Azure Active Directory B2C 中的身分識別提供者]: https://docs.microsoft.com/azure/active-directory-b2c/active-directory-b2c-setup-goog-app</span><span class="sxs-lookup"><span data-stu-id="c84e2-176">[Use a Google account as an identity provider in Azure Active Directory B2C]: https://docs.microsoft.com/azure/active-directory-b2c/active-directory-b2c-setup-goog-app</span></span>
<span data-ttu-id="c84e2-177">[使用 Facebook 帳戶做為 Azure Active Directory B2C 中的身分識別提供者]: https://docs.microsoft.com/azure/active-directory-b2c/active-directory-b2c-setup-fb-app</span><span class="sxs-lookup"><span data-stu-id="c84e2-177">[Use a Facebook account as an identity provider in Azure Active Directory B2C]: https://docs.microsoft.com/azure/active-directory-b2c/active-directory-b2c-setup-fb-app</span></span>
<span data-ttu-id="c84e2-178">[使用 Linkedin 帳戶做為 Azure Active Directory B2C 中的身分識別提供者]: https://docs.microsoft.com/azure/active-directory-b2c/active-directory-b2c-setup-li-app</span><span class="sxs-lookup"><span data-stu-id="c84e2-178">[Use a LinkedIn account as an identity provider in Azure Active Directory B2C]: https://docs.microsoft.com/azure/active-directory-b2c/active-directory-b2c-setup-li-app</span></span>

[Prerequisites]: #prerequisites
[Configure an OAuth 2.0 authorization server in API Management]: #step1
[Configure an API to use OAuth 2.0 user authorization]: #step2
[Test the OAuth 2.0 user authorization in the Developer Portal]: #step3
[Next steps]: #next-steps

[Log in to the Developer portal using an Azure Active Directory account]: #Log-in-to-the-Developer-portal-using-an-Azure-Active-Directory-account
