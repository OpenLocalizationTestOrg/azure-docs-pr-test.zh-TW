---
title: "Azure Active Directory B2C：Weibo 設定 | Microsoft Docs"
description: "在受 Azure Active Directory B2C 保護的應用程式中，針對具有 Weibo 帳戶的取用者提供註冊和登入。"
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
ms.openlocfilehash: 00c5d3781455c80b33bdbb4c872ae354531baf3e
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/18/2017
---
# <a name="azure-active-directory-b2c-provide-sign-up-and-sign-in-to-consumers-with-weibo-accounts"></a><span data-ttu-id="38166-103">Azure Active Directory B2C：針對具有 Weibo 帳戶的取用者提供註冊和登入</span><span class="sxs-lookup"><span data-stu-id="38166-103">Azure Active Directory B2C: Provide sign-up and sign-in to consumers with Weibo accounts</span></span>

> [!NOTE]
> <span data-ttu-id="38166-104">這項功能處於預覽狀態。</span><span class="sxs-lookup"><span data-stu-id="38166-104">This feature is in preview.</span></span> <span data-ttu-id="38166-105">請勿在生產環境中使用此識別提供者。</span><span class="sxs-lookup"><span data-stu-id="38166-105">Do not use this identity provider in your production environment.</span></span>
> 

## <a name="create-a-weibo-application"></a><span data-ttu-id="38166-106">建立 Weibo 應用程式</span><span class="sxs-lookup"><span data-stu-id="38166-106">Create a Weibo application</span></span>

<span data-ttu-id="38166-107">若要在 Azure Active Directory (Azure AD) B2C 中使用 Weibo 做為識別提供者，您必須建立 Weibo 應用程式，並對其提供正確參數。</span><span class="sxs-lookup"><span data-stu-id="38166-107">To use Weibo as an identity provider in Azure Active Directory (Azure AD) B2C, you need to create a Weibo application and supply it with the right parameters.</span></span> <span data-ttu-id="38166-108">您需要 Weibo 帳戶才能執行此動作。</span><span class="sxs-lookup"><span data-stu-id="38166-108">You need a Weibo account to do this.</span></span> <span data-ttu-id="38166-109">如果您沒有帳戶，您可以取得在 [http://weibo.com/signup/signup.php?lang=en-us](http://weibo.com/signup/signup.php?lang=en-us) 上取得一個。</span><span class="sxs-lookup"><span data-stu-id="38166-109">If you don’t have one, you can get one at [http://weibo.com/signup/signup.php?lang=en-us](http://weibo.com/signup/signup.php?lang=en-us).</span></span>

### <a name="register-for-the-weibo-developer-program"></a><span data-ttu-id="38166-110">註冊 Weibo 開發人員計劃</span><span class="sxs-lookup"><span data-stu-id="38166-110">Register for the Weibo developer program</span></span>

1. <span data-ttu-id="38166-111">移至 [Weibo 開發人員入口網站](http://open.weibo.com/)並以您的 Weibo 帳戶認證登入。</span><span class="sxs-lookup"><span data-stu-id="38166-111">Go to the [Weibo developer portal](http://open.weibo.com/) and sign in with your Weibo account credentials.</span></span>
2. <span data-ttu-id="38166-112">登入之後，按一下您在右上角的顯示名稱。</span><span class="sxs-lookup"><span data-stu-id="38166-112">After signing in, click on your display name in the top-right corner.</span></span>
3. <span data-ttu-id="38166-113">在下拉式清單中，選取 [编辑开发者信息] \(編輯開發人員資訊)。</span><span class="sxs-lookup"><span data-stu-id="38166-113">In the dropdown, select **编辑开发者信息** (edit developer information).</span></span>
4. <span data-ttu-id="38166-114">在表單中輸入所需的資訊，然後按一下 [提交]。</span><span class="sxs-lookup"><span data-stu-id="38166-114">Enter the required information into the form and click **提交** (submit).</span></span>
5. <span data-ttu-id="38166-115">完成電子郵件驗證程序。</span><span class="sxs-lookup"><span data-stu-id="38166-115">Complete the email verification process.</span></span>
6. <span data-ttu-id="38166-116">移至[識別驗證頁面](http://open.weibo.com/developers/identity/edit)。</span><span class="sxs-lookup"><span data-stu-id="38166-116">Go to the [identity verification page](http://open.weibo.com/developers/identity/edit).</span></span>
7. <span data-ttu-id="38166-117">在表單中輸入所需的資訊，然後按一下 [提交]。</span><span class="sxs-lookup"><span data-stu-id="38166-117">Enter the required information into the form and click **提交** (submit).</span></span>

### <a name="register-a-weibo-application"></a><span data-ttu-id="38166-118">註冊 Weibo 應用程式</span><span class="sxs-lookup"><span data-stu-id="38166-118">Register a Weibo application</span></span>

1. <span data-ttu-id="38166-119">移至[新的 Weibo 應用程式註冊頁面](http://open.weibo.com/apps/new)。</span><span class="sxs-lookup"><span data-stu-id="38166-119">Go to the [new Weibo app registration page](http://open.weibo.com/apps/new).</span></span>
2. <span data-ttu-id="38166-120">輸入必要的應用程式資訊。</span><span class="sxs-lookup"><span data-stu-id="38166-120">Enter the necessary application information.</span></span>
3. <span data-ttu-id="38166-121">按一下 [创建] \(建立)。</span><span class="sxs-lookup"><span data-stu-id="38166-121">Click **创建** (create).</span></span>
4. <span data-ttu-id="38166-122">複製**應用程式金鑰**和**應用程式密碼**的值。</span><span class="sxs-lookup"><span data-stu-id="38166-122">Copy the values of **App Key** and **App Secret**.</span></span> <span data-ttu-id="38166-123">稍後您將會需要此資訊。</span><span class="sxs-lookup"><span data-stu-id="38166-123">You will need this later.</span></span>
5. <span data-ttu-id="38166-124">上傳所需的相片，並輸入所需的資訊。</span><span class="sxs-lookup"><span data-stu-id="38166-124">Upload the required photos and enter the necessary information.</span></span>
6. <span data-ttu-id="38166-125">按一下 [保存以上信息] \(儲存)。</span><span class="sxs-lookup"><span data-stu-id="38166-125">Click **保存以上信息** (save).</span></span>
7. <span data-ttu-id="38166-126">按一下 [高级信息] \(進階資訊)。</span><span class="sxs-lookup"><span data-stu-id="38166-126">Click **高级信息** (advanced information).</span></span>
8. <span data-ttu-id="38166-127">按一下 OAuth2.0 [授权设置] \(重新導向 URL) 旁的 [编辑] \(編輯) 欄位。</span><span class="sxs-lookup"><span data-stu-id="38166-127">Click **编辑** (edit) next to the field for OAuth2.0 **授权设置** (redirect URL).</span></span>
9. <span data-ttu-id="38166-128">針對 OAuth2.0 [授权设置] \(重新導向 URL) 輸入 `https://login.microsoftonline.com/te/{tenant_name}/oauth2/authresp`。</span><span class="sxs-lookup"><span data-stu-id="38166-128">Enter `https://login.microsoftonline.com/te/{tenant_name}/oauth2/authresp` for OAuth2.0 **授权设置** (redirect URL).</span></span> <span data-ttu-id="38166-129">例如，如果您的 `tenant_name` 是 contoso.onmicrosoft.com，請將 URL 設為 `https://login.microsoftonline.com/te/contoso.onmicrosoft.com/oauth2/authresp`。</span><span class="sxs-lookup"><span data-stu-id="38166-129">For example, if your `tenant_name` is contoso.onmicrosoft.com, set the URL to be `https://login.microsoftonline.com/te/contoso.onmicrosoft.com/oauth2/authresp`.</span></span>
10. <span data-ttu-id="38166-130">按一下 [提交]。</span><span class="sxs-lookup"><span data-stu-id="38166-130">Click **提交** (submit).</span></span>  

## <a name="configure-weibo-as-an-identity-provider-in-your-tenant"></a><span data-ttu-id="38166-131">在租用戶中將 Weibo 設為識別提供者</span><span class="sxs-lookup"><span data-stu-id="38166-131">Configure Weibo as an identity provider in your tenant</span></span>
1. <span data-ttu-id="38166-132">遵循下列步驟以 [瀏覽至 B2C 功能刀鋒視窗](active-directory-b2c-app-registration.md#navigate-to-b2c-settings) (位於 Azure 入口網站上)。</span><span class="sxs-lookup"><span data-stu-id="38166-132">Follow these steps to [navigate to the B2C features blade](active-directory-b2c-app-registration.md#navigate-to-b2c-settings) on the Azure portal.</span></span>
2. <span data-ttu-id="38166-133">在 B2C 功能刀鋒視窗中，按一下 [ **身分識別提供者**]。</span><span class="sxs-lookup"><span data-stu-id="38166-133">On the B2C features blade, click **Identity providers**.</span></span>
3. <span data-ttu-id="38166-134">按一下刀鋒視窗頂端的 [新增]  。</span><span class="sxs-lookup"><span data-stu-id="38166-134">Click **+Add** at the top of the blade.</span></span>
4. <span data-ttu-id="38166-135">針對身分識別提供者組態，提供容易辨識的 **名稱** 。</span><span class="sxs-lookup"><span data-stu-id="38166-135">Provide a friendly **Name** for the identity provider configuration.</span></span> <span data-ttu-id="38166-136">例如，輸入 "Weibo"。</span><span class="sxs-lookup"><span data-stu-id="38166-136">For example, enter "Weibo".</span></span>
5. <span data-ttu-id="38166-137">按一下 [識別提供者類型]、選取 [Weibo]，然後按一下 [確定]。</span><span class="sxs-lookup"><span data-stu-id="38166-137">Click **Identity provider type**, select **Weibo**, and click **OK**.</span></span>
6. <span data-ttu-id="38166-138">按一下 [設定此識別提供者]。</span><span class="sxs-lookup"><span data-stu-id="38166-138">Click **Set up this identity provider**</span></span>
7. <span data-ttu-id="38166-139">輸入您稍早複製為**用戶端識別碼**的**應用程式金鑰**。</span><span class="sxs-lookup"><span data-stu-id="38166-139">Enter the **App Key** that you copied earlier as the **Client ID**.</span></span>
8. <span data-ttu-id="38166-140">輸入您稍早複製為**用戶端密碼**的**應用程式密碼**。</span><span class="sxs-lookup"><span data-stu-id="38166-140">Enter the **App Secret** that you copied earlier as the **Client Secret**.</span></span>
9. <span data-ttu-id="38166-141">依序按一下 [確定] 和 [建立]，儲存您的 Weibo 設定。</span><span class="sxs-lookup"><span data-stu-id="38166-141">Click **OK** and then click **Create** to save your Weibo configuration.</span></span>

