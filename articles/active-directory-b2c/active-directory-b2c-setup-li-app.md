---
title: "Azure Active Directory B2C：LinkedIn 設定 | Microsoft Docs"
description: "提供註冊和登入 tooconsumers LinkedIn 帳戶，在受保護的 Azure Active Directory B2C 的應用程式中使用"
services: active-directory-b2c
documentationcenter: 
author: swkrish
manager: mbaldwin
editor: bryanla
ms.assetid: fa51a16b-9ce9-4e27-9eff-0869b4c4f0ef
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/06/2016
ms.author: swkrish
ms.openlocfilehash: 6c5233ef48b24968fd6383f470b5d8a969a78ecf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2c-provide-sign-up-and-sign-in-tooconsumers-with-linkedin-accounts"></a><span data-ttu-id="01a92-103">Azure Active Directory B2C： 註冊和登入 tooconsumers 提供 LinkedIn 帳戶</span><span class="sxs-lookup"><span data-stu-id="01a92-103">Azure Active Directory B2C: Provide sign-up and sign-in tooconsumers with LinkedIn accounts</span></span>
## <a name="create-a-linkedin-application"></a><span data-ttu-id="01a92-104">建立 LinkedIn 應用程式</span><span class="sxs-lookup"><span data-stu-id="01a92-104">Create a LinkedIn application</span></span>
<span data-ttu-id="01a92-105">toouse LinkedIn B2C Azure Active Directory (Azure AD) 中的身分識別提供者，您需要 toocreate LinkedIn 應用程式和提供 hello 正確的參數。</span><span class="sxs-lookup"><span data-stu-id="01a92-105">toouse LinkedIn as an identity provider in Azure Active Directory (Azure AD) B2C, you need toocreate a LinkedIn application and supply it with hello right parameters.</span></span> <span data-ttu-id="01a92-106">您需要 LinkedIn 帳戶 toodo 此。</span><span class="sxs-lookup"><span data-stu-id="01a92-106">You need a LinkedIn account toodo this.</span></span> <span data-ttu-id="01a92-107">如果您沒有該帳戶，您可以在 [https://www.linkedin.com/](https://www.linkedin.com/)上申請。</span><span class="sxs-lookup"><span data-stu-id="01a92-107">If you don’t have one, you can get it at [https://www.linkedin.com/](https://www.linkedin.com/).</span></span>

1. <span data-ttu-id="01a92-108">移 toohello [LinkedIn 開發人員網站](https://www.developer.linkedin.com/)並以您 LinkedIn 的帳戶認證登入。</span><span class="sxs-lookup"><span data-stu-id="01a92-108">Go toohello [LinkedIn Developers website](https://www.developer.linkedin.com/) and sign in with your LinkedIn account credentials.</span></span>
2. <span data-ttu-id="01a92-109">按一下**我的應用程式**在 hello 頂端功能表列，然後按一下 [**建立應用程式**。</span><span class="sxs-lookup"><span data-stu-id="01a92-109">Click **My Apps** in hello top menu bar and then click **Create Application**.</span></span>
   
    ![LinkedIn - 新建應用程式](./media/active-directory-b2c-setup-li-app/linkedin-new-app.png)
3. <span data-ttu-id="01a92-111">在 [hello**建立新的應用程式**表單中，填寫 hello 相關資訊 (**公司名稱**，**名稱**，**描述**， **應用程式標誌 URL**，**應用程式使用**，**網站 URL**，**公司電子郵件**和**公司電話**).</span><span class="sxs-lookup"><span data-stu-id="01a92-111">In hello **Create a New Application** form, fill in hello relevant information (**Company Name**, **Name**, **Description**, **Application Logo URL**, **Application Use**, **Website URL**, **Business Email** and **Business Phone**).</span></span>
4. <span data-ttu-id="01a92-112">同意 toohello **LinkedIn API 的使用規定**按一下**送出**。</span><span class="sxs-lookup"><span data-stu-id="01a92-112">Agree toohello **LinkedIn API Terms of Use** and click **Submit**.</span></span>
   
    ![LinkedIn - 註冊應用程式](./media/active-directory-b2c-setup-li-app/linkedin-register-app.png)
5. <span data-ttu-id="01a92-114">複製的 hello 值**用戶端識別碼**和**用戶端密碼**。</span><span class="sxs-lookup"><span data-stu-id="01a92-114">Copy hello values of **Client ID** and **Client Secret**.</span></span> <span data-ttu-id="01a92-115">(您可以在 [驗證金鑰] 下方找到這些資訊)。您將需要這兩種 tooconfigure LinkedIn 身分識別提供者，在您的租用戶。</span><span class="sxs-lookup"><span data-stu-id="01a92-115">(You can find them under **Authentication Keys**.) You will need both of them tooconfigure LinkedIn as an identity provider in your tenant.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="01a92-116">**用戶端密碼** 是重要的安全性認證。</span><span class="sxs-lookup"><span data-stu-id="01a92-116">**Client Secret** is an important security credential.</span></span>
   > 
   > 
6. <span data-ttu-id="01a92-117">輸入`https://login.microsoftonline.com/te/{tenant}/oauth2/authresp`在 hello**授權重新導向 Url**欄位 (下**OAuth 2.0**)。</span><span class="sxs-lookup"><span data-stu-id="01a92-117">Enter `https://login.microsoftonline.com/te/{tenant}/oauth2/authresp` in hello **Authorized Redirect URLs** field (under **OAuth 2.0**).</span></span> <span data-ttu-id="01a92-118">使用您的租用戶名稱 (例如 contoso.onmicrosoft.com) 來取代 **{tenant}**。</span><span class="sxs-lookup"><span data-stu-id="01a92-118">Replace **{tenant}** with your tenant's name (for example, contoso.onmicrosoft.com).</span></span> <span data-ttu-id="01a92-119">按一下 [新增]，然後按一下 [更新]。</span><span class="sxs-lookup"><span data-stu-id="01a92-119">Click **Add**, and then click **Update**.</span></span> <span data-ttu-id="01a92-120">hello **{tenant}**值會區分大小寫。</span><span class="sxs-lookup"><span data-stu-id="01a92-120">hello **{tenant}** value is case-sensitive.</span></span>
   
    ![LinkedIn - 設定應用程式](./media/active-directory-b2c-setup-li-app/linkedin-setup.png)

## <a name="configure-linkedin-as-an-identity-provider-in-your-tenant"></a><span data-ttu-id="01a92-122">將 LinkedIn 設定為您租用戶中的識別提供者</span><span class="sxs-lookup"><span data-stu-id="01a92-122">Configure LinkedIn as an identity provider in your tenant</span></span>
1. <span data-ttu-id="01a92-123">請遵循下列步驟太[瀏覽 toohello B2C 功能刀鋒視窗](active-directory-b2c-app-registration.md#navigate-to-b2c-settings)hello Azure 入口網站上。</span><span class="sxs-lookup"><span data-stu-id="01a92-123">Follow these steps too[navigate toohello B2C features blade](active-directory-b2c-app-registration.md#navigate-to-b2c-settings) on hello Azure portal.</span></span>
2. <span data-ttu-id="01a92-124">在 [hello B2C 功能刀鋒視窗中，按一下 [**身分識別提供者**。</span><span class="sxs-lookup"><span data-stu-id="01a92-124">On hello B2C features blade, click **Identity providers**.</span></span>
3. <span data-ttu-id="01a92-125">按一下**+ 加**在 hello hello 刀鋒視窗最上方。</span><span class="sxs-lookup"><span data-stu-id="01a92-125">Click **+Add** at hello top of hello blade.</span></span>
4. <span data-ttu-id="01a92-126">提供方便**名稱**hello 身分識別提供者組態。</span><span class="sxs-lookup"><span data-stu-id="01a92-126">Provide a friendly **Name** for hello identity provider configuration.</span></span> <span data-ttu-id="01a92-127">例如，輸入「LI」。</span><span class="sxs-lookup"><span data-stu-id="01a92-127">For example, enter "LI".</span></span>
5. <span data-ttu-id="01a92-128">按一下 [識別提供者類型]、選取 [LinkedIn]，然後按一下 [確定]。</span><span class="sxs-lookup"><span data-stu-id="01a92-128">Click **Identity provider type**, select **LinkedIn**, and click **OK**.</span></span>
6. <span data-ttu-id="01a92-129">按一下**設定此身分識別提供者**，然後輸入 hello 用戶端識別碼和用戶端密碼的 hello LinkedIn 您稍早建立的應用程式。</span><span class="sxs-lookup"><span data-stu-id="01a92-129">Click **Set up this identity provider** and enter hello client ID and client secret of hello LinkedIn application that you created earlier.</span></span>
7. <span data-ttu-id="01a92-130">按一下**確定**，然後按一下 [**建立**toosave LinkedIn 組態。</span><span class="sxs-lookup"><span data-stu-id="01a92-130">Click **OK** and then click **Create** toosave your LinkedIn configuration.</span></span>

