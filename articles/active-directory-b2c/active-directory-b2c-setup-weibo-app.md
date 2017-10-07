---
title: "Azure Active Directory B2C：Weibo 設定 | Microsoft Docs"
description: "提供註冊和登入 tooconsumers Weibo 帳戶，在受保護的 Azure Active Directory B2C 的應用程式中使用。"
services: active-directory-b2c
documentationcenter: 
author: parakhj
manager: krassk
editor: parakhj
ms.assetid: 1860de34-94cb-4ceb-851e-102f930f7230
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 3/26/2017
ms.author: parakhj
ms.openlocfilehash: c0648620f318046c1d9d24feb92a0c5f19c6a91a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2c-provide-sign-up-and-sign-in-tooconsumers-with-weibo-accounts"></a><span data-ttu-id="ddc82-103">Azure Active Directory B2C： 註冊和登入 tooconsumers 提供 Weibo 帳戶</span><span class="sxs-lookup"><span data-stu-id="ddc82-103">Azure Active Directory B2C: Provide sign-up and sign-in tooconsumers with Weibo accounts</span></span>

> [!NOTE]
> <span data-ttu-id="ddc82-104">這項功能處於預覽狀態。</span><span class="sxs-lookup"><span data-stu-id="ddc82-104">This feature is in preview.</span></span> <span data-ttu-id="ddc82-105">請勿在生產環境中使用此識別提供者。</span><span class="sxs-lookup"><span data-stu-id="ddc82-105">Do not use this identity provider in your production environment.</span></span>
> 

## <a name="create-a-weibo-application"></a><span data-ttu-id="ddc82-106">建立 Weibo 應用程式</span><span class="sxs-lookup"><span data-stu-id="ddc82-106">Create a Weibo application</span></span>

<span data-ttu-id="ddc82-107">toouse Weibo B2C Azure Active Directory (Azure AD) 中的身分識別提供者，您需要 toocreate Weibo 應用程式和提供 hello 正確的參數。</span><span class="sxs-lookup"><span data-stu-id="ddc82-107">toouse Weibo as an identity provider in Azure Active Directory (Azure AD) B2C, you need toocreate a Weibo application and supply it with hello right parameters.</span></span> <span data-ttu-id="ddc82-108">您需要 Weibo 帳戶 toodo 此。</span><span class="sxs-lookup"><span data-stu-id="ddc82-108">You need a Weibo account toodo this.</span></span> <span data-ttu-id="ddc82-109">如果您沒有帳戶，您可以取得在 [http://weibo.com/signup/signup.php?lang=en-us](http://weibo.com/signup/signup.php?lang=en-us) 上取得一個。</span><span class="sxs-lookup"><span data-stu-id="ddc82-109">If you don’t have one, you can get one at [http://weibo.com/signup/signup.php?lang=en-us](http://weibo.com/signup/signup.php?lang=en-us).</span></span>

### <a name="register-for-hello-weibo-developer-program"></a><span data-ttu-id="ddc82-110">註冊 hello Weibo 開發人員計劃</span><span class="sxs-lookup"><span data-stu-id="ddc82-110">Register for hello Weibo developer program</span></span>

1. <span data-ttu-id="ddc82-111">移 toohello [Weibo 開發人員入口網站](http://open.weibo.com/)並以您 Weibo 帳戶認證登入。</span><span class="sxs-lookup"><span data-stu-id="ddc82-111">Go toohello [Weibo developer portal](http://open.weibo.com/) and sign in with your Weibo account credentials.</span></span>
2. <span data-ttu-id="ddc82-112">登入之後，按一下您在 hello 右上角的顯示名稱。</span><span class="sxs-lookup"><span data-stu-id="ddc82-112">After signing in, click on your display name in hello top-right corner.</span></span>
3. <span data-ttu-id="ddc82-113">在 hello 下拉式清單中，選取 **编辑开发者信息**（編輯開發人員資訊）。</span><span class="sxs-lookup"><span data-stu-id="ddc82-113">In hello dropdown, select **编辑开发者信息** (edit developer information).</span></span>
4. <span data-ttu-id="ddc82-114">Hello 所需的資訊輸入 hello 表單，然後按一下**提交**（提交）。</span><span class="sxs-lookup"><span data-stu-id="ddc82-114">Enter hello required information into hello form and click **提交** (submit).</span></span>
5. <span data-ttu-id="ddc82-115">完成 hello 電子郵件驗證程序。</span><span class="sxs-lookup"><span data-stu-id="ddc82-115">Complete hello email verification process.</span></span>
6. <span data-ttu-id="ddc82-116">移 toohello[身分識別驗證頁面](http://open.weibo.com/developers/identity/edit)。</span><span class="sxs-lookup"><span data-stu-id="ddc82-116">Go toohello [identity verification page](http://open.weibo.com/developers/identity/edit).</span></span>
7. <span data-ttu-id="ddc82-117">Hello 所需的資訊輸入 hello 表單，然後按一下**提交**（提交）。</span><span class="sxs-lookup"><span data-stu-id="ddc82-117">Enter hello required information into hello form and click **提交** (submit).</span></span>

### <a name="register-a-weibo-application"></a><span data-ttu-id="ddc82-118">註冊 Weibo 應用程式</span><span class="sxs-lookup"><span data-stu-id="ddc82-118">Register a Weibo application</span></span>

1. <span data-ttu-id="ddc82-119">移 toohello[新 Weibo 應用程式登錄頁面](http://open.weibo.com/apps/new)。</span><span class="sxs-lookup"><span data-stu-id="ddc82-119">Go toohello [new Weibo app registration page](http://open.weibo.com/apps/new).</span></span>
2. <span data-ttu-id="ddc82-120">輸入 hello 必要的應用程式資訊。</span><span class="sxs-lookup"><span data-stu-id="ddc82-120">Enter hello necessary application information.</span></span>
3. <span data-ttu-id="ddc82-121">按一下 [创建] \(建立)。</span><span class="sxs-lookup"><span data-stu-id="ddc82-121">Click **创建** (create).</span></span>
4. <span data-ttu-id="ddc82-122">複製的 hello 值**應用程式金鑰**和**應用程式秘鑰**。</span><span class="sxs-lookup"><span data-stu-id="ddc82-122">Copy hello values of **App Key** and **App Secret**.</span></span> <span data-ttu-id="ddc82-123">稍後您將會需要此資訊。</span><span class="sxs-lookup"><span data-stu-id="ddc82-123">You will need this later.</span></span>
5. <span data-ttu-id="ddc82-124">上傳所需的 hello 相片，然後輸入 hello 所需的資訊。</span><span class="sxs-lookup"><span data-stu-id="ddc82-124">Upload hello required photos and enter hello necessary information.</span></span>
6. <span data-ttu-id="ddc82-125">按一下 [保存以上信息] \(儲存)。</span><span class="sxs-lookup"><span data-stu-id="ddc82-125">Click **保存以上信息** (save).</span></span>
7. <span data-ttu-id="ddc82-126">按一下 [高级信息] \(進階資訊)。</span><span class="sxs-lookup"><span data-stu-id="ddc82-126">Click **高级信息** (advanced information).</span></span>
8. <span data-ttu-id="ddc82-127">按一下**编辑**（編輯） 下一步 toohello 欄位 OAuth2.0**授权设置**（重新導向 URL）。</span><span class="sxs-lookup"><span data-stu-id="ddc82-127">Click **编辑** (edit) next toohello field for OAuth2.0 **授权设置** (redirect URL).</span></span>
9. <span data-ttu-id="ddc82-128">針對 OAuth2.0 [授权设置] \(重新導向 URL) 輸入 `https://login.microsoftonline.com/te/{tenant_name}/oauth2/authresp`。</span><span class="sxs-lookup"><span data-stu-id="ddc82-128">Enter `https://login.microsoftonline.com/te/{tenant_name}/oauth2/authresp` for OAuth2.0 **授权设置** (redirect URL).</span></span> <span data-ttu-id="ddc82-129">例如，如果您`tenant_name`是 contoso.onmicrosoft.com，集 hello URL toobe `https://login.microsoftonline.com/te/contoso.onmicrosoft.com/oauth2/authresp`。</span><span class="sxs-lookup"><span data-stu-id="ddc82-129">For example, if your `tenant_name` is contoso.onmicrosoft.com, set hello URL toobe `https://login.microsoftonline.com/te/contoso.onmicrosoft.com/oauth2/authresp`.</span></span>
10. <span data-ttu-id="ddc82-130">按一下 [提交]。</span><span class="sxs-lookup"><span data-stu-id="ddc82-130">Click **提交** (submit).</span></span>  

## <a name="configure-weibo-as-an-identity-provider-in-your-tenant"></a><span data-ttu-id="ddc82-131">在租用戶中將 Weibo 設為識別提供者</span><span class="sxs-lookup"><span data-stu-id="ddc82-131">Configure Weibo as an identity provider in your tenant</span></span>
1. <span data-ttu-id="ddc82-132">請遵循下列步驟太[瀏覽 toohello B2C 功能刀鋒視窗](active-directory-b2c-app-registration.md#navigate-to-b2c-settings)hello Azure 入口網站上。</span><span class="sxs-lookup"><span data-stu-id="ddc82-132">Follow these steps too[navigate toohello B2C features blade](active-directory-b2c-app-registration.md#navigate-to-b2c-settings) on hello Azure portal.</span></span>
2. <span data-ttu-id="ddc82-133">在 hello B2C 功能刀鋒視窗中，按一下 **身分識別提供者**。</span><span class="sxs-lookup"><span data-stu-id="ddc82-133">On hello B2C features blade, click **Identity providers**.</span></span>
3. <span data-ttu-id="ddc82-134">按一下**+ 加**在 hello hello 刀鋒視窗最上方。</span><span class="sxs-lookup"><span data-stu-id="ddc82-134">Click **+Add** at hello top of hello blade.</span></span>
4. <span data-ttu-id="ddc82-135">提供方便**名稱**hello 身分識別提供者組態。</span><span class="sxs-lookup"><span data-stu-id="ddc82-135">Provide a friendly **Name** for hello identity provider configuration.</span></span> <span data-ttu-id="ddc82-136">例如，輸入 "Weibo"。</span><span class="sxs-lookup"><span data-stu-id="ddc82-136">For example, enter "Weibo".</span></span>
5. <span data-ttu-id="ddc82-137">按一下 [識別提供者類型]、選取 [Weibo]，然後按一下 [確定]。</span><span class="sxs-lookup"><span data-stu-id="ddc82-137">Click **Identity provider type**, select **Weibo**, and click **OK**.</span></span>
6. <span data-ttu-id="ddc82-138">按一下 [設定此識別提供者]。</span><span class="sxs-lookup"><span data-stu-id="ddc82-138">Click **Set up this identity provider**</span></span>
7. <span data-ttu-id="ddc82-139">輸入 hello**應用程式金鑰**您之前複製為 hello**用戶端識別碼**。</span><span class="sxs-lookup"><span data-stu-id="ddc82-139">Enter hello **App Key** that you copied earlier as hello **Client ID**.</span></span>
8. <span data-ttu-id="ddc82-140">輸入 hello**應用程式秘鑰**您之前複製為 hello**用戶端密碼**。</span><span class="sxs-lookup"><span data-stu-id="ddc82-140">Enter hello **App Secret** that you copied earlier as hello **Client Secret**.</span></span>
9. <span data-ttu-id="ddc82-141">按一下**確定**，然後按一下**建立**toosave Weibo 組態。</span><span class="sxs-lookup"><span data-stu-id="ddc82-141">Click **OK** and then click **Create** toosave your Weibo configuration.</span></span>

