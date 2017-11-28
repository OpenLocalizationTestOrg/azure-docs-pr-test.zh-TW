---
title: "Azure Active Directory B2C：Google+ 設定 | Microsoft Docs"
description: "提供註冊和登入 tooconsumers 與 Google + 應用程式保護 Azure Active Directory B2C 的帳戶。"
services: active-directory-b2c
documentationcenter: 
author: swkrish
manager: mbaldwin
editor: bryanla
ms.assetid: 4dcca66f-29e4-4b4d-8840-50baad736bd7
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/06/2016
ms.author: swkrish
ms.openlocfilehash: 6ef66eb17777acd95b5f4745ed6097c77e37663b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2c-provide-sign-up-and-sign-in-tooconsumers-with-google-accounts"></a><span data-ttu-id="5975e-103">Azure Active Directory B2C： 提供與 Google + 帳戶註冊和登入 tooconsumers</span><span class="sxs-lookup"><span data-stu-id="5975e-103">Azure Active Directory B2C: Provide sign-up and sign-in tooconsumers with Google+ accounts</span></span>
## <a name="create-a-google-application"></a><span data-ttu-id="5975e-104">建立 Google+ 應用程式</span><span class="sxs-lookup"><span data-stu-id="5975e-104">Create a Google+ application</span></span>
<span data-ttu-id="5975e-105">toouse Google + B2C Azure Active Directory (Azure AD) 中的身分識別提供者，您需要 toocreate Google + 應用程式和提供 hello 正確的參數。</span><span class="sxs-lookup"><span data-stu-id="5975e-105">toouse Google+ as an identity provider in Azure Active Directory (Azure AD) B2C, you need toocreate a Google+ application and supply it with hello right parameters.</span></span> <span data-ttu-id="5975e-106">您需要 Google + 帳戶 toodo 此。</span><span class="sxs-lookup"><span data-stu-id="5975e-106">You need a Google+ account toodo this.</span></span> <span data-ttu-id="5975e-107">如果您沒有該帳戶，您可以在 [https://accounts.google.com/SignUp](https://accounts.google.com/SignUp)上申請。</span><span class="sxs-lookup"><span data-stu-id="5975e-107">If you don’t have one, you can get it at [https://accounts.google.com/SignUp](https://accounts.google.com/SignUp).</span></span>

1. <span data-ttu-id="5975e-108">移 toohello [Google 開發人員主控台](https://console.developers.google.com/)並以您的 Google + 帳戶認證登入。</span><span class="sxs-lookup"><span data-stu-id="5975e-108">Go toohello [Google Developers Console](https://console.developers.google.com/) and sign in with your Google+ account credentials.</span></span>
2. <span data-ttu-id="5975e-109">按一下 [建立專案]，輸入 [專案名稱]，接著按一下 [建立]。</span><span class="sxs-lookup"><span data-stu-id="5975e-109">Click **Create project**, enter a **Project name**, and then click **Create**.</span></span>
   
    ![Google+ - 開始使用](./media/active-directory-b2c-setup-goog-app/google-get-started.png)
   
    ![Google+ - 新增專案](./media/active-directory-b2c-setup-goog-app/google-new-project.png)
3. <span data-ttu-id="5975e-112">按一下**API Manager** ，然後按一下 [**認證**在 hello 左瀏覽。</span><span class="sxs-lookup"><span data-stu-id="5975e-112">Click **API Manager** and then click **Credentials** in hello left navigation.</span></span>
4. <span data-ttu-id="5975e-113">按一下 hello **OAuth 同意畫面**hello 頂端的索引標籤。</span><span class="sxs-lookup"><span data-stu-id="5975e-113">Click hello **OAuth consent screen** tab at hello top.</span></span>
   
    ![Google+ - 認證](./media/active-directory-b2c-setup-goog-app/google-add-cred.png)
5. <span data-ttu-id="5975e-115">選取或指定有效的**電子郵件地址**、提供**產品名稱**，然後按一下 [儲存]。</span><span class="sxs-lookup"><span data-stu-id="5975e-115">Select or specify a valid **Email address**, provide a **Product name**, and click **Save**.</span></span>
   
    ![Google+ - OAuth 同意畫面](./media/active-directory-b2c-setup-goog-app/google-consent-screen.png)
6. <span data-ttu-id="5975e-117">按一下 [新增認證]，然後選擇 [OAuth 用戶端識別碼]。</span><span class="sxs-lookup"><span data-stu-id="5975e-117">Click **New credentials** and then choose **OAuth client ID**.</span></span>
   
    ![Google+ - OAuth 同意畫面](./media/active-directory-b2c-setup-goog-app/google-add-oauth2-client-id.png)
7. <span data-ttu-id="5975e-119">在 [應用程式類型] 下方，選取 [Web 應用程式]。</span><span class="sxs-lookup"><span data-stu-id="5975e-119">Under **Application type**, select **Web application**.</span></span>
   
    ![Google+ - OAuth 同意畫面](./media/active-directory-b2c-setup-goog-app/google-web-app.png)
8. <span data-ttu-id="5975e-121">提供**名稱**針對您的應用程式中，輸入`https://login.microsoftonline.com`在 hello**授權 JavaScript origins**欄位，和`https://login.microsoftonline.com/te/{tenant}/oauth2/authresp`在 hello**授權重新導向 Uri**欄位。</span><span class="sxs-lookup"><span data-stu-id="5975e-121">Provide a **Name** for your application, enter `https://login.microsoftonline.com` in hello **Authorized JavaScript origins** field, and `https://login.microsoftonline.com/te/{tenant}/oauth2/authresp` in hello **Authorized redirect URIs** field.</span></span> <span data-ttu-id="5975e-122">使用您的租用戶名稱 (例如 contosob2c.onmicrosoft.com) 來取代 **{tenant}**。</span><span class="sxs-lookup"><span data-stu-id="5975e-122">Replace **{tenant}** with your tenant's name (for example, contosob2c.onmicrosoft.com).</span></span> <span data-ttu-id="5975e-123">hello **{tenant}**值會區分大小寫。</span><span class="sxs-lookup"><span data-stu-id="5975e-123">hello **{tenant}** value is case-sensitive.</span></span> <span data-ttu-id="5975e-124">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="5975e-124">Click **Create**.</span></span>
   
    ![Google+ -  建立用戶端識別碼](./media/active-directory-b2c-setup-goog-app/google-create-client-id.png)
9. <span data-ttu-id="5975e-126">複製的 hello 值**用戶端識別碼**和**用戶端密碼**。</span><span class="sxs-lookup"><span data-stu-id="5975e-126">Copy hello values of **Client ID** and **Client secret**.</span></span> <span data-ttu-id="5975e-127">您將需要這兩種 tooconfigure Google + 身分識別提供者，在您的租用戶。</span><span class="sxs-lookup"><span data-stu-id="5975e-127">You will need both of them tooconfigure Google+ as an identity provider in your tenant.</span></span> <span data-ttu-id="5975e-128">**用戶端密碼** 是重要的安全性認證。</span><span class="sxs-lookup"><span data-stu-id="5975e-128">**Client secret** is an important security credential.</span></span>
   
    ![Google+ - 用戶端密碼](./media/active-directory-b2c-setup-goog-app/google-client-secret.png)

## <a name="configure-google-as-an-identity-provider-in-your-tenant"></a><span data-ttu-id="5975e-130">將 Google+ 帳戶於租用戶中設定為識別提供者</span><span class="sxs-lookup"><span data-stu-id="5975e-130">Configure Google+ as an identity provider in your tenant</span></span>
1. <span data-ttu-id="5975e-131">請遵循下列步驟太[瀏覽 toohello B2C 功能刀鋒視窗](active-directory-b2c-app-registration.md#navigate-to-b2c-settings)hello Azure 入口網站上。</span><span class="sxs-lookup"><span data-stu-id="5975e-131">Follow these steps too[navigate toohello B2C features blade](active-directory-b2c-app-registration.md#navigate-to-b2c-settings) on hello Azure portal.</span></span>
2. <span data-ttu-id="5975e-132">在 [hello B2C 功能刀鋒視窗中，按一下 [**身分識別提供者**。</span><span class="sxs-lookup"><span data-stu-id="5975e-132">On hello B2C features blade, click **Identity providers**.</span></span>
3. <span data-ttu-id="5975e-133">按一下**+ 加**在 hello hello 刀鋒視窗最上方。</span><span class="sxs-lookup"><span data-stu-id="5975e-133">Click **+Add** at hello top of hello blade.</span></span>
4. <span data-ttu-id="5975e-134">提供方便**名稱**hello 身分識別提供者組態。</span><span class="sxs-lookup"><span data-stu-id="5975e-134">Provide a friendly **Name** for hello identity provider configuration.</span></span> <span data-ttu-id="5975e-135">例如，輸入 "G+"。</span><span class="sxs-lookup"><span data-stu-id="5975e-135">For example, enter "G+".</span></span>
5. <span data-ttu-id="5975e-136">按一下 [識別提供者類型]、選取 [Google]，然後按一下 [確定]。</span><span class="sxs-lookup"><span data-stu-id="5975e-136">Click **Identity provider type**, select **Google**, and click **OK**.</span></span>
6. <span data-ttu-id="5975e-137">按一下**設定此身分識別提供者**，然後輸入 hello 用戶端識別碼和用戶端密碼 hello Google + 應用程式，您稍早建立。</span><span class="sxs-lookup"><span data-stu-id="5975e-137">Click **Set up this identity provider** and enter hello client ID and client secret of hello Google+ application that you created earlier.</span></span>
7. <span data-ttu-id="5975e-138">按一下**確定**，然後按一下 [**建立**toosave Google + 設定。</span><span class="sxs-lookup"><span data-stu-id="5975e-138">Click **OK** and then click **Create** toosave your Google+ configuration.</span></span>

