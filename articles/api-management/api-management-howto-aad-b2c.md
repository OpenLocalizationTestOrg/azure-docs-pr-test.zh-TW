---
title: "使用 Azure 的 Active Directory B2C-而 Azure API 管理 aaaAuthorize 開發人員帳戶 |Microsoft 文件"
description: "深入了解如何使用 API 管理中的 Azure Active Directory B2C tooauthorize 使用者。"
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
ms.openlocfilehash: 28f7cae53138938dbbc848b4afcbf08b72690e37
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooauthorize-developer-accounts-by-using-azure-active-directory-b2c-in-azure-api-management"></a><span data-ttu-id="b86bb-103">如何在 Azure API 管理中使用 Azure Active Directory B2C tooauthorize 開發人員帳戶</span><span class="sxs-lookup"><span data-stu-id="b86bb-103">How tooauthorize developer accounts by using Azure Active Directory B2C in Azure API Management</span></span>
## <a name="overview"></a><span data-ttu-id="b86bb-104">概觀</span><span class="sxs-lookup"><span data-stu-id="b86bb-104">Overview</span></span>
<span data-ttu-id="b86bb-105">Azure Active Directory B2C 是適用於取用者導向 Web 與行動應用程式的雲端身分識別管理解決方案。</span><span class="sxs-lookup"><span data-stu-id="b86bb-105">Azure Active Directory B2C is a cloud identity management solution for consumer-facing web and mobile applications.</span></span> <span data-ttu-id="b86bb-106">您可以使用 toomanage 存取 tooyour 開發人員入口網站。</span><span class="sxs-lookup"><span data-stu-id="b86bb-106">You can use it toomanage access tooyour developer portal.</span></span> <span data-ttu-id="b86bb-107">此指南會顯示您在 Azure Active Directory B2C 與您 API 管理服務 toointegrate hello 所需的組態。</span><span class="sxs-lookup"><span data-stu-id="b86bb-107">This guide shows you hello configuration that's required in your API Management service toointegrate with Azure Active Directory B2C.</span></span> <span data-ttu-id="b86bb-108">使用傳統的 Azure Active Directory 啟用存取 toohello 開發人員入口網站的相關資訊，請參閱[如何 tooauthorize 開發人員帳戶使用 Azure Active Directory]。</span><span class="sxs-lookup"><span data-stu-id="b86bb-108">For information about enabling access toohello developer portal by using classic Azure Active Directory, see [How tooauthorize developer accounts using Azure Active Directory].</span></span>

> [!NOTE]
> <span data-ttu-id="b86bb-109">toocomplete hello 本指南中的步驟，您必須先取得 Azure Active Directory B2C 租用戶 toocreate 應用程式。</span><span class="sxs-lookup"><span data-stu-id="b86bb-109">toocomplete hello steps in this guide, you must first have an Azure Active Directory B2C tenant toocreate an application in.</span></span> <span data-ttu-id="b86bb-110">此外，您需要 toohave 註冊和登入原則準備。</span><span class="sxs-lookup"><span data-stu-id="b86bb-110">Also, you need toohave signup and signin policies ready.</span></span> <span data-ttu-id="b86bb-111">如需詳細資訊，請參閱 [Azure Active Directory B2C 概觀]。</span><span class="sxs-lookup"><span data-stu-id="b86bb-111">For more information, see [Azure Active Directory B2C overview].</span></span>

## <a name="authorize-developer-accounts-by-using-azure-active-directory-b2c"></a><span data-ttu-id="b86bb-112">使用 Azure Active Directory B2C 授權開發人員帳戶</span><span class="sxs-lookup"><span data-stu-id="b86bb-112">Authorize developer accounts by using Azure Active Directory B2C</span></span>

1. <span data-ttu-id="b86bb-113">tooget 啟動，按一下**發行者入口網站**hello API 管理服務的 Azure 入口網站中。</span><span class="sxs-lookup"><span data-stu-id="b86bb-113">tooget started, click **Publisher portal** in hello Azure portal for your API Management service.</span></span> <span data-ttu-id="b86bb-114">這會帶您 toohello API 管理發行者入口網站。</span><span class="sxs-lookup"><span data-stu-id="b86bb-114">This takes you toohello API Management publisher portal.</span></span>

   ![發行者入口網站][api-management-management-console]

   > [!NOTE]
   > <span data-ttu-id="b86bb-116">如果您尚未建立 API 管理服務執行個體，請參閱[建立 API 管理服務執行個體][ Create an API Management service instance]在 hello[開始使用 Azure API 管理教學課程][Get started with Azure API Management].</span><span class="sxs-lookup"><span data-stu-id="b86bb-116">If you haven't yet created an API Management service instance, see [Create an API Management service instance][Create an API Management service instance] in hello [Get started with Azure API Management tutorial][Get started with Azure API Management].</span></span>

2. <span data-ttu-id="b86bb-117">在 hello **API 管理**功能表上，按一下 **安全性**。</span><span class="sxs-lookup"><span data-stu-id="b86bb-117">On hello **API Management** menu, click **Security**.</span></span> <span data-ttu-id="b86bb-118">在 hello**識別**索引標籤上，選擇**Azure Active Directory B2C**。</span><span class="sxs-lookup"><span data-stu-id="b86bb-118">On hello **Identities** tab, choose **Azure Active Directory B2C**.</span></span>

  ![外部身分識別 1][api-management-howto-aad-b2c-security-tab]

3. <span data-ttu-id="b86bb-120">請記下 hello**重新導向 URL**和切換 tooAzure Active Directory B2C hello Azure 入口網站中。</span><span class="sxs-lookup"><span data-stu-id="b86bb-120">Make a note of hello **Redirect URL** and switch over tooAzure Active Directory B2C in hello Azure portal.</span></span>

  ![外部身分識別 2][api-management-howto-aad-b2c-security-tab-reply-url]

4. <span data-ttu-id="b86bb-122">按一下 hello**應用程式** 按鈕。</span><span class="sxs-lookup"><span data-stu-id="b86bb-122">Click hello **Applications** button.</span></span>

  ![註冊新的應用程式 1][api-management-howto-aad-b2c-portal-menu]

5. <span data-ttu-id="b86bb-124">按一下 hello**新增**按鈕 toocreate 新 Azure Active Directory B2C 應用程式。</span><span class="sxs-lookup"><span data-stu-id="b86bb-124">Click hello **Add** button toocreate a new Azure Active Directory B2C application.</span></span>

  ![註冊新的應用程式 2][api-management-howto-aad-b2c-add-button]

6. <span data-ttu-id="b86bb-126">在 hello**新的應用程式**刀鋒視窗中，輸入 hello 應用程式的名稱。</span><span class="sxs-lookup"><span data-stu-id="b86bb-126">In hello **New application** blade, enter a name for hello application.</span></span> <span data-ttu-id="b86bb-127">在 [Web 應用程式/Web API] 下選擇 [是]，然後在 [允許隱含流程] 下選擇 [是]。</span><span class="sxs-lookup"><span data-stu-id="b86bb-127">Choose **Yes** under **Web App/Web API**, and choose **Yes** under **Allow implicit flow**.</span></span> <span data-ttu-id="b86bb-128">然後複製 hello**重新導向 URL**從 hello **Azure Active Directory B2C**區段 hello**識別**索引標籤的 hello 發行者入口網站，並將它貼到 hello **回覆 URL**文字方塊。</span><span class="sxs-lookup"><span data-stu-id="b86bb-128">Then copy hello **Redirect URL** from hello **Azure Active Directory B2C** section of hello **Identities** tab in hello publisher portal, and paste it into hello **Reply URL** text box.</span></span>

  ![註冊新的應用程式 3][api-management-howto-aad-b2c-app-details]

7. <span data-ttu-id="b86bb-130">按一下 hello**建立** 按鈕。</span><span class="sxs-lookup"><span data-stu-id="b86bb-130">Click hello **Create** button.</span></span> <span data-ttu-id="b86bb-131">建立 hello 應用程式時，它會出現在 hello**應用程式**刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="b86bb-131">When hello application is created, it appears in hello **Applications** blade.</span></span> <span data-ttu-id="b86bb-132">按一下 hello 應用程式名稱 toosee 其詳細資料。</span><span class="sxs-lookup"><span data-stu-id="b86bb-132">Click hello application name toosee its details.</span></span>

  ![註冊新的應用程式 4][api-management-howto-aad-b2c-app-created]

8. <span data-ttu-id="b86bb-134">從 hello**屬性**刀鋒視窗，複製 hello**應用程式識別碼**toohello 剪貼簿。</span><span class="sxs-lookup"><span data-stu-id="b86bb-134">From hello **Properties** blade, copy hello **Application ID** toohello clipboard.</span></span>

  ![應用程式識別碼 1][api-management-howto-aad-b2c-app-id]

9. <span data-ttu-id="b86bb-136">切換後 toohello 發行者入口網站，然後貼入 hello hello 識別碼**用戶端識別碼**文字方塊。</span><span class="sxs-lookup"><span data-stu-id="b86bb-136">Switch back toohello publisher portal and paste hello ID into hello **Client Id** text box.</span></span>

  ![應用程式識別碼 2][api-management-howto-aad-b2c-client-id]

10. <span data-ttu-id="b86bb-138">參數後 toohello Azure 入口網站，請按一下 hello**金鑰**按鈕，然後再按一下**產生金鑰**。</span><span class="sxs-lookup"><span data-stu-id="b86bb-138">Switch back toohello Azure portal, click hello **Keys** button, and then click **Generate key**.</span></span> <span data-ttu-id="b86bb-139">按一下**儲存**toosave hello 組態並顯示 hello**應用程式金鑰**。</span><span class="sxs-lookup"><span data-stu-id="b86bb-139">Click **Save** toosave hello configuration and display hello **App key**.</span></span> <span data-ttu-id="b86bb-140">將複製 hello 金鑰 toohello 剪貼簿。</span><span class="sxs-lookup"><span data-stu-id="b86bb-140">Copy hello key toohello clipboard.</span></span>

  ![應用程式金鑰 1][api-management-howto-aad-b2c-app-key]

11. <span data-ttu-id="b86bb-142">交換器後 toohello 發行者入口網站和貼上 hello 金鑰貼入 hello**用戶端密碼**文字方塊。</span><span class="sxs-lookup"><span data-stu-id="b86bb-142">Switch back toohello publisher portal and paste hello key into hello **Client Secret** text box.</span></span>

  ![應用程式金鑰 2][api-management-howto-aad-b2c-client-secret]

12. <span data-ttu-id="b86bb-144">指定 hello 網域名稱中的 hello Azure Active Directory B2C 租用戶**允許租用戶**。</span><span class="sxs-lookup"><span data-stu-id="b86bb-144">Specify hello domain name of hello Azure Active Directory B2C tenant in **Allowed Tenant**.</span></span>

  ![允許的租用戶][api-management-howto-aad-b2c-allowed-tenant]

13. <span data-ttu-id="b86bb-146">指定 hello**註冊原則**和**簽入原則**。</span><span class="sxs-lookup"><span data-stu-id="b86bb-146">Specify hello **Signup Policy** and **Signin Policy**.</span></span> <span data-ttu-id="b86bb-147">（選擇性） 您也可以提供 hello**檔編輯原則**和**密碼重設原則**。</span><span class="sxs-lookup"><span data-stu-id="b86bb-147">Optionally, you can also provide hello **Profile Editing Policy** and **Password Reset Policy**.</span></span>

  ![原則][api-management-howto-aad-b2c-policies]

  > [!NOTE]
  > <span data-ttu-id="b86bb-149">如需原則的詳細資訊，請參閱 [Azure Active Directory B2C：可延伸的原則架構]。</span><span class="sxs-lookup"><span data-stu-id="b86bb-149">For more information on policies, see [Azure Active Directory B2C: Extensible policy framework].</span></span>

14. <span data-ttu-id="b86bb-150">您所指定 hello 所需的組態之後，請按一下**儲存**。</span><span class="sxs-lookup"><span data-stu-id="b86bb-150">After you've specified hello desired configuration, click **Save**.</span></span>

  <span data-ttu-id="b86bb-151">儲存 hello 變更之後，開發人員會是能 toocreate 新帳戶，並使用 Azure Active Directory B2C 的登入 toohello 開發人員入口網站。</span><span class="sxs-lookup"><span data-stu-id="b86bb-151">After hello changes are saved, developers will be able toocreate new accounts and sign in toohello developer portal by using Azure Active Directory B2C.</span></span>

## <a name="sign-up-for-a-developer-account-by-using-azure-active-directory-b2c"></a><span data-ttu-id="b86bb-152">使用 Azure Active Directory B2C 註冊開發人員帳戶</span><span class="sxs-lookup"><span data-stu-id="b86bb-152">Sign up for a developer account by using Azure Active Directory B2C</span></span>

1. <span data-ttu-id="b86bb-153">開發人員帳戶，使用 Azure Active Directory B2C toosign 開啟新的瀏覽器視窗，並移 toohello 開發人員入口網站。</span><span class="sxs-lookup"><span data-stu-id="b86bb-153">toosign up for a developer account by using Azure Active Directory B2C, open a new browser window and go toohello developer portal.</span></span> <span data-ttu-id="b86bb-154">按一下 hello**註冊** 按鈕。</span><span class="sxs-lookup"><span data-stu-id="b86bb-154">Click hello **Sign up** button.</span></span>

   ![開發人員入口網站 1][api-management-howto-aad-b2c-dev-portal]

2. <span data-ttu-id="b86bb-156">選擇 toosign 上與**Azure Active Directory B2C**。</span><span class="sxs-lookup"><span data-stu-id="b86bb-156">Choose toosign up with **Azure Active Directory B2C**.</span></span>

   ![開發人員入口網站 2][api-management-howto-aad-b2c-dev-portal-b2c-button]

3. <span data-ttu-id="b86bb-158">您可以設定 hello 前一節中的重新導向的 toohello 註冊原則。</span><span class="sxs-lookup"><span data-stu-id="b86bb-158">You're redirected toohello signup policy that you configured in hello previous section.</span></span> <span data-ttu-id="b86bb-159">您可以選擇 上 toosign 使用電子郵件地址，或其中一個現有的社交帳戶。</span><span class="sxs-lookup"><span data-stu-id="b86bb-159">Choose toosign up by using your email address or one of your existing social accounts.</span></span>

   > [!NOTE]
   > <span data-ttu-id="b86bb-160">如果 Azure Active Directory B2C hello hello 已啟用的唯一選項**識別** 索引標籤在 hello 發行者入口網站，您應該重新導向的 toohello 註冊原則直接。</span><span class="sxs-lookup"><span data-stu-id="b86bb-160">If Azure Active Directory B2C is hello only option that's enabled on hello **Identities** tab in hello publisher portal, you'll be redirected toohello signup policy directly.</span></span>

   ![開發人員入口網站][api-management-howto-aad-b2c-dev-portal-b2c-options]

   <span data-ttu-id="b86bb-162">Hello 註冊完成時，您已重新導向後 toohello 開發人員入口網站。</span><span class="sxs-lookup"><span data-stu-id="b86bb-162">When hello signup is complete, you're redirected back toohello developer portal.</span></span> <span data-ttu-id="b86bb-163">您現在已為您的 API 管理服務執行個體登入 toohello 開發人員入口網站。</span><span class="sxs-lookup"><span data-stu-id="b86bb-163">You're now signed in toohello developer portal for your API Management service instance.</span></span>

    ![註冊完成][api-management-registration-complete]

## <a name="next-steps"></a><span data-ttu-id="b86bb-165">後續步驟</span><span class="sxs-lookup"><span data-stu-id="b86bb-165">Next steps</span></span>

*  <span data-ttu-id="b86bb-166">[Azure Active Directory B2C 概觀]</span><span class="sxs-lookup"><span data-stu-id="b86bb-166">[Azure Active Directory B2C overview]</span></span>
*  <span data-ttu-id="b86bb-167">[Azure Active Directory B2C：可延伸的原則架構]</span><span class="sxs-lookup"><span data-stu-id="b86bb-167">[Azure Active Directory B2C: Extensible policy framework]</span></span>
*  <span data-ttu-id="b86bb-168">[使用 Microsoft 帳戶做為 Azure Active Directory B2C 中的身分識別提供者]</span><span class="sxs-lookup"><span data-stu-id="b86bb-168">[Use a Microsoft account as an identity provider in Azure Active Directory B2C]</span></span>
*  <span data-ttu-id="b86bb-169">[使用 Google 帳戶做為 Azure Active Directory B2C 中的身分識別提供者]</span><span class="sxs-lookup"><span data-stu-id="b86bb-169">[Use a Google account as an identity provider in Azure Active Directory B2C]</span></span>
*  <span data-ttu-id="b86bb-170">[使用 Linkedin 帳戶做為 Azure Active Directory B2C 中的身分識別提供者]</span><span class="sxs-lookup"><span data-stu-id="b86bb-170">[Use a LinkedIn account as an identity provider in Azure Active Directory B2C]</span></span>
*  <span data-ttu-id="b86bb-171">[使用 Facebook 帳戶做為 Azure Active Directory B2C 中的身分識別提供者]</span><span class="sxs-lookup"><span data-stu-id="b86bb-171">[Use a Facebook account as an identity provider in Azure Active Directory B2C]</span></span>




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

[How tooadd operations tooan API]: api-management-howto-add-operations.md
[How tooadd and publish a product]: api-management-howto-add-products.md
[Monitoring and analytics]: api-management-monitoring.md
[Add APIs tooa product]: api-management-howto-add-products.md#add-apis
[Publish a product]: api-management-howto-add-products.md#publish-product
[Get started with Azure API Management]: api-management-get-started.md
[API Management policy reference]: api-management-policy-reference.md
[Caching policies]: api-management-policy-reference.md#caching-policies
[Create an API Management service instance]: api-management-get-started.md#create-service-instance

[http://oauth.net/2/]: http://oauth.net/2/
[WebApp-GraphAPI-DotNet]: https://github.com/AzureADSamples/WebApp-GraphAPI-DotNet
[Accessing hello Graph API]: http://msdn.microsoft.com/library/azure/dn132599.aspx#BKMK_Graph
[Azure Active Directory B2C 概觀]: https://docs.microsoft.com/azure/active-directory-b2c/active-directory-b2c-overview
[如何 tooauthorize 開發人員帳戶使用 Azure Active Directory]: https://docs.microsoft.com/azure/api-management/api-management-howto-aad
[Azure Active Directory B2C：可延伸的原則架構]: https://docs.microsoft.com/azure/active-directory-b2c/active-directory-b2c-reference-policies
[使用 Microsoft 帳戶做為 Azure Active Directory B2C 中的身分識別提供者]: https://docs.microsoft.com/azure/active-directory-b2c/active-directory-b2c-setup-msa-app
[使用 Google 帳戶做為 Azure Active Directory B2C 中的身分識別提供者]: https://docs.microsoft.com/azure/active-directory-b2c/active-directory-b2c-setup-goog-app
[使用 Facebook 帳戶做為 Azure Active Directory B2C 中的身分識別提供者]: https://docs.microsoft.com/azure/active-directory-b2c/active-directory-b2c-setup-fb-app
[使用 Linkedin 帳戶做為 Azure Active Directory B2C 中的身分識別提供者]: https://docs.microsoft.com/azure/active-directory-b2c/active-directory-b2c-setup-li-app

[Prerequisites]: #prerequisites
[Configure an OAuth 2.0 authorization server in API Management]: #step1
[Configure an API toouse OAuth 2.0 user authorization]: #step2
[Test hello OAuth 2.0 user authorization in hello Developer Portal]: #step3
[Next steps]: #next-steps

[Log in toohello Developer portal using an Azure Active Directory account]: #Log-in-to-the-Developer-portal-using-an-Azure-Active-Directory-account
