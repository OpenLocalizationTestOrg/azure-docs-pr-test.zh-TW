---
title: "Azure Active Directory B2C：Microsoft 帳戶設定 | Microsoft Docs"
description: "提供在受保護的 Azure Active Directory B2C 的應用程式中的 Microsoft 帳戶註冊和登入 tooconsumers。"
services: active-directory-b2c
documentationcenter: 
author: swkrish
manager: mbaldwin
editor: bryanla
ms.assetid: 06407322-142c-4cb3-9106-a8d752c4c853
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/06/2016
ms.author: swkrish
ms.openlocfilehash: bec4777f003c459030f68c35b24f0e4bcddf84ae
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2c-provide-sign-up-and-sign-in-tooconsumers-with-microsoft-accounts"></a><span data-ttu-id="888aa-103">Azure Active Directory B2C： 提供與 Microsoft 帳戶註冊和登入 tooconsumers</span><span class="sxs-lookup"><span data-stu-id="888aa-103">Azure Active Directory B2C: Provide sign-up and sign-in tooconsumers with Microsoft accounts</span></span>
## <a name="create-a-microsoft-account-application"></a><span data-ttu-id="888aa-104">建立 Microsoft 帳戶應用程式</span><span class="sxs-lookup"><span data-stu-id="888aa-104">Create a Microsoft account application</span></span>
<span data-ttu-id="888aa-105">身分識別提供者，在 Azure Active Directory (Azure AD) B2C 的 toouse Microsoft 帳戶，您需要 toocreate Microsoft 帳戶應用程式，並提供與 hello 正確的參數。</span><span class="sxs-lookup"><span data-stu-id="888aa-105">toouse Microsoft account as an identity provider in Azure Active Directory (Azure AD) B2C, you need toocreate a Microsoft account application and supply it with hello right parameters.</span></span> <span data-ttu-id="888aa-106">您需要 Microsoft 帳戶 toodo 此。</span><span class="sxs-lookup"><span data-stu-id="888aa-106">You need a Microsoft account toodo this.</span></span> <span data-ttu-id="888aa-107">如果您沒有該帳戶，您可以在 [https://www.live.com/](https://www.live.com/)上申請。</span><span class="sxs-lookup"><span data-stu-id="888aa-107">If you don’t have one, you can get it at [https://www.live.com/](https://www.live.com/).</span></span>

1. <span data-ttu-id="888aa-108">移 toohello [Microsoft 應用程式註冊入口網站](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList)並以您的 Microsoft 帳戶認證登入。</span><span class="sxs-lookup"><span data-stu-id="888aa-108">Go toohello [Microsoft Application Registration Portal](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList) and sign in with your Microsoft account credentials.</span></span>
2. <span data-ttu-id="888aa-109">按一下 [新增應用程式] 。</span><span class="sxs-lookup"><span data-stu-id="888aa-109">Click **Add an app**.</span></span>
   
    ![Microsoft 帳戶 - 加入新的應用程式](./media/active-directory-b2c-setup-msa-app/msa-add-new-app.png)
3. <span data-ttu-id="888aa-111">為應用程式提供 [名稱]，然後按一下 [建立應用程式]。</span><span class="sxs-lookup"><span data-stu-id="888aa-111">Provide a **Name** for your application and click **Create application**.</span></span>
   
    ![Microsoft 帳戶 - 應用程式名稱](./media/active-directory-b2c-setup-msa-app/msa-app-name.png)
4. <span data-ttu-id="888aa-113">複製 hello 值**應用程式識別碼**。您需要這些 tooconfigure Microsoft 帳戶身分識別提供者租用戶中。</span><span class="sxs-lookup"><span data-stu-id="888aa-113">Copy hello value of **Application Id**. You will need it tooconfigure Microsoft account as an identity provider in your tenant.</span></span>
   
    ![Microsoft 帳戶 - 應用程式識別碼](./media/active-directory-b2c-setup-msa-app/msa-app-id.png)
5. <span data-ttu-id="888aa-115">按一下 [新增平台]，然後選擇 [Web]。</span><span class="sxs-lookup"><span data-stu-id="888aa-115">Click on **Add platform** and choose **Web**.</span></span>
   
    ![Microsoft 帳戶 - 新增平台](./media/active-directory-b2c-setup-msa-app/msa-add-platform.png)
   
    ![Microsoft 帳戶 - Web](./media/active-directory-b2c-setup-msa-app/msa-web.png)
6. <span data-ttu-id="888aa-118">輸入`https://login.microsoftonline.com/te/{tenant}/oauth2/authresp`在 hello**重新導向 Uri**欄位。</span><span class="sxs-lookup"><span data-stu-id="888aa-118">Enter `https://login.microsoftonline.com/te/{tenant}/oauth2/authresp` in hello **Redirect URIs** field.</span></span> <span data-ttu-id="888aa-119">使用您的租用戶名稱 (例如 contosob2c.onmicrosoft.com) 來取代 **{tenant}**。</span><span class="sxs-lookup"><span data-stu-id="888aa-119">Replace **{tenant}** with your tenant's name (for example, contosob2c.onmicrosoft.com).</span></span>
   
    ![Microsoft 帳戶 - 重新導向 URL](./media/active-directory-b2c-setup-msa-app/msa-redirect-url.png)
7. <span data-ttu-id="888aa-121">按一下**產生新的密碼**下 hello**應用程式密碼**> 一節。</span><span class="sxs-lookup"><span data-stu-id="888aa-121">Click on **Generate New Password** under hello **Application Secrets** section.</span></span> <span data-ttu-id="888aa-122">複製顯示在螢幕上的 hello 新密碼。</span><span class="sxs-lookup"><span data-stu-id="888aa-122">Copy hello new password displayed on screen.</span></span> <span data-ttu-id="888aa-123">您需要這些 tooconfigure Microsoft 帳戶身分識別提供者租用戶中。</span><span class="sxs-lookup"><span data-stu-id="888aa-123">You will need it tooconfigure Microsoft account as an identity provider in your tenant.</span></span> <span data-ttu-id="888aa-124">此密碼是重要的安全性認證。</span><span class="sxs-lookup"><span data-stu-id="888aa-124">This password is an important security credential.</span></span>
   
    ![Microsoft 帳戶 - 產生新密碼](./media/active-directory-b2c-setup-msa-app/msa-generate-new-password.png)
   
    ![Microsoft 帳戶 - 新密碼](./media/active-directory-b2c-setup-msa-app/msa-new-password.png)
8. <span data-ttu-id="888aa-127">指出核取 hello 方塊**Live SDK 支援**下 hello**進階選項**> 一節。</span><span class="sxs-lookup"><span data-stu-id="888aa-127">Check hello box that says **Live SDK support** under hello **Advanced Options** section.</span></span> <span data-ttu-id="888aa-128">按一下 [儲存] 。</span><span class="sxs-lookup"><span data-stu-id="888aa-128">Click **Save**.</span></span>
   
    ![Microsoft 帳戶 - Live SDK 支援](./media/active-directory-b2c-setup-msa-app/msa-live-sdk-support.png)

## <a name="configure-microsoft-account-as-an-identity-provider-in-your-tenant"></a><span data-ttu-id="888aa-130">將 Microsoft 帳戶於租用戶中設定為識別提供者</span><span class="sxs-lookup"><span data-stu-id="888aa-130">Configure Microsoft account as an identity provider in your tenant</span></span>
1. <span data-ttu-id="888aa-131">請遵循下列步驟太[瀏覽 toohello B2C 功能刀鋒視窗](active-directory-b2c-app-registration.md#navigate-to-b2c-settings)hello Azure 入口網站上。</span><span class="sxs-lookup"><span data-stu-id="888aa-131">Follow these steps too[navigate toohello B2C features blade](active-directory-b2c-app-registration.md#navigate-to-b2c-settings) on hello Azure portal.</span></span>
2. <span data-ttu-id="888aa-132">在 [hello B2C 功能刀鋒視窗中，按一下 [**身分識別提供者**。</span><span class="sxs-lookup"><span data-stu-id="888aa-132">On hello B2C features blade, click **Identity providers**.</span></span>
3. <span data-ttu-id="888aa-133">按一下**+ 加**在 hello hello 刀鋒視窗最上方。</span><span class="sxs-lookup"><span data-stu-id="888aa-133">Click **+Add** at hello top of hello blade.</span></span>
4. <span data-ttu-id="888aa-134">提供方便**名稱**hello 身分識別提供者組態。</span><span class="sxs-lookup"><span data-stu-id="888aa-134">Provide a friendly **Name** for hello identity provider configuration.</span></span> <span data-ttu-id="888aa-135">例如，輸入 "MSA"。</span><span class="sxs-lookup"><span data-stu-id="888aa-135">For example, enter "MSA".</span></span>
5. <span data-ttu-id="888aa-136">按一下 [識別提供者類型]、選取 [Microsoft 帳戶]，然後按一下 [確定]。</span><span class="sxs-lookup"><span data-stu-id="888aa-136">Click **Identity provider type**, select **Microsoft account**, and click **OK**.</span></span>
6. <span data-ttu-id="888aa-137">按一下**設定此身分識別提供者**，然後輸入 hello 應用程式識別碼和密碼的 hello 您稍早建立的 Microsoft 帳戶應用程式。</span><span class="sxs-lookup"><span data-stu-id="888aa-137">Click **Set up this identity provider** and enter hello Application Id and password of hello Microsoft account application that you created earlier.</span></span>
7. <span data-ttu-id="888aa-138">按一下**確定**，然後按一下 [**建立**toosave 您的 Microsoft 帳戶設定。</span><span class="sxs-lookup"><span data-stu-id="888aa-138">Click **OK** and then click **Create** toosave your Microsoft account configuration.</span></span>

