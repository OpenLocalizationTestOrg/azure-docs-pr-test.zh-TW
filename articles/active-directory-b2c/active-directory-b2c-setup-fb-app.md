---
title: "Azure Active Directory B2C：Facebook 設定 | Microsoft Docs"
description: "提供在受保護的 Azure Active Directory B2C 的應用程式中的 Facebook 帳戶註冊和登入 tooconsumers。"
services: active-directory-b2c
documentationcenter: 
author: sromeroz
manager: krassk
editor: sromeroz
ms.assetid: b875f235-a1d2-4abb-b9f0-b89beac38a32
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 8/7/2017
ms.author: sromeroz
ms.openlocfilehash: 4c3b79c7248bd1e789bf33fc467abb27d0170edd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2c-provide-sign-up-and-sign-in-tooconsumers-with-facebook-accounts"></a><span data-ttu-id="76d76-103">Azure Active Directory B2C： 提供與 Facebook 帳戶註冊和登入 tooconsumers</span><span class="sxs-lookup"><span data-stu-id="76d76-103">Azure Active Directory B2C: Provide sign-up and sign-in tooconsumers with Facebook accounts</span></span>
## <a name="create-a-facebook-application"></a><span data-ttu-id="76d76-104">建立 Facebook 應用程式</span><span class="sxs-lookup"><span data-stu-id="76d76-104">Create a Facebook application</span></span>
<span data-ttu-id="76d76-105">toouse Facebook 中 Azure Active Directory (Azure AD) B2C 身分識別提供者，您需要 toocreate Facebook 應用程式和提供 hello 正確的參數。</span><span class="sxs-lookup"><span data-stu-id="76d76-105">toouse Facebook as an identity provider in Azure Active Directory (Azure AD) B2C, you need toocreate a Facebook application and supply it with hello right parameters.</span></span> <span data-ttu-id="76d76-106">您需要 Facebook 帳戶 toodo 此。</span><span class="sxs-lookup"><span data-stu-id="76d76-106">You need a Facebook account toodo this.</span></span> <span data-ttu-id="76d76-107">如果您沒有帳戶，您可以在 [https://www.facebook.com/](https://www.facebook.com/)上取得。</span><span class="sxs-lookup"><span data-stu-id="76d76-107">If you don’t have one, you can get it at [https://www.facebook.com/](https://www.facebook.com/).</span></span>

1. <span data-ttu-id="76d76-108">移 toohello [Facebook 開發人員](https://developers.facebook.com/)網站並使用您的 Facebook 登入帳戶的認證。</span><span class="sxs-lookup"><span data-stu-id="76d76-108">Go toohello [Facebook for developers](https://developers.facebook.com/) website and sign in with your Facebook account credentials.</span></span>
2. <span data-ttu-id="76d76-109">如果您尚未這樣做，您會需要 tooregister 身為 Facebook 開發人員。</span><span class="sxs-lookup"><span data-stu-id="76d76-109">If you have not already done so, you need tooregister as a Facebook developer.</span></span> <span data-ttu-id="76d76-110">toodo 此，依序按一下**註冊**（在 hello 右上角的 hello 頁面），接受 Facebook 的原則，並完成 hello 註冊步驟。</span><span class="sxs-lookup"><span data-stu-id="76d76-110">toodo this, click **Register** (on hello upper-right corner of hello page), accept Facebook's policies, and complete hello registration steps.</span></span>
3. <span data-ttu-id="76d76-111">按一下 我的應用程式，然後按一下新增應用程式。</span><span class="sxs-lookup"><span data-stu-id="76d76-111">Click **My Apps** and then click **Add a New App**.</span></span> 
4. <span data-ttu-id="76d76-112">在 hello 表單中，提供**顯示名稱**且有效**Contact Email**。</span><span class="sxs-lookup"><span data-stu-id="76d76-112">In hello form, provide a **Display Name** and a valid **Contact Email**.</span></span>
5. <span data-ttu-id="76d76-113">按一下 [建立應用程式識別碼]。</span><span class="sxs-lookup"><span data-stu-id="76d76-113">Click **Create App ID**.</span></span> <span data-ttu-id="76d76-114">這可能需要您 tooaccept Facebook 平台原則，並完成線上安全性檢查。</span><span class="sxs-lookup"><span data-stu-id="76d76-114">This may require you tooaccept Facebook platform policies and complete an online security check.</span></span>
6. <span data-ttu-id="76d76-115">Hello 左欄中按一下**設定**，然後選取 **基本**如果尚未選取的話。</span><span class="sxs-lookup"><span data-stu-id="76d76-115">In hello left column, click **Settings** and then select **Basic** if not selected already.</span></span>
7. <span data-ttu-id="76d76-116">選取一個**類別**。</span><span class="sxs-lookup"><span data-stu-id="76d76-116">Select a **Category**.</span></span> 
8. <span data-ttu-id="76d76-117">按一下 [+ 新增平台]，然後選取 [網站]。</span><span class="sxs-lookup"><span data-stu-id="76d76-117">Click **+ Add Platform** and select **Website**.</span></span>
   
    ![Facebook - 設定](./media/active-directory-b2c-setup-fb-app/fb-settings.png)
   
    ![Facebook - 設定 - 網站](./media/active-directory-b2c-setup-fb-app/fb-website.png)
9. <span data-ttu-id="76d76-120">輸入`https://login.microsoftonline.com/`在 hello**網站 URL**欄位，然後按一下**儲存變更**hello hello 頁底端。</span><span class="sxs-lookup"><span data-stu-id="76d76-120">Enter `https://login.microsoftonline.com/` in hello **Site URL** field and then click **Save Changes** at hello bottom of hello page.</span></span>
   
    ![Facebook - 網站 URL](./media/active-directory-b2c-setup-fb-app/fb-site-url.png)

10. <span data-ttu-id="76d76-122">複製 hello 值**應用程式識別碼**。</span><span class="sxs-lookup"><span data-stu-id="76d76-122">Copy hello value of **App ID**.</span></span> <span data-ttu-id="76d76-123">按一下**顯示**和複製 hello 值**應用程式秘鑰**。</span><span class="sxs-lookup"><span data-stu-id="76d76-123">Click **Show** and copy hello value of **App Secret**.</span></span> <span data-ttu-id="76d76-124">您將需要這兩種 tooconfigure Facebook 身分識別提供者，在您的租用戶。</span><span class="sxs-lookup"><span data-stu-id="76d76-124">You will need both of them tooconfigure Facebook as an identity provider in your tenant.</span></span> <span data-ttu-id="76d76-125">**應用程式密碼**是重要的安全性認證。</span><span class="sxs-lookup"><span data-stu-id="76d76-125">**App Secret** is an important security credential.</span></span>
   
    ![Facebook - 應用程式識別碼和應用程式密碼](./media/active-directory-b2c-setup-fb-app/fb-app-id-app-secret.png)
11. <span data-ttu-id="76d76-127">按一下**+ 加入產品**hello 左側瀏覽且然後 hello**設定**按鈕**Facebook 登入**。</span><span class="sxs-lookup"><span data-stu-id="76d76-127">Click **+ Add Product** on hello left navigation and then hello **Set Up** button for **Facebook Login**.</span></span>
   
    ![Facebook - Facebook 登入](./media/active-directory-b2c-setup-fb-app/fb-login.png)
12. <span data-ttu-id="76d76-129">按一下**設定**上 hello 底下的右 nav **Facebook 登入**</span><span class="sxs-lookup"><span data-stu-id="76d76-129">Click **Settings** on hello right nav under **Facebook Login**</span></span>

    ![Facebook - Facebook 登入設定](./media/active-directory-b2c-setup-fb-app/fb-login-settings.png)
13. <span data-ttu-id="76d76-131">輸入`https://login.microsoftonline.com/te/{tenant}/oauth2/authresp`在 hello**有效的 OAuth 重新導向 Uri**欄位 hello**用戶端的 OAuth 設定**> 一節。</span><span class="sxs-lookup"><span data-stu-id="76d76-131">Enter `https://login.microsoftonline.com/te/{tenant}/oauth2/authresp` in hello **Valid OAuth redirect URIs** field in hello **Client OAuth Settings** section.</span></span> <span data-ttu-id="76d76-132">使用您的租用戶名稱 (例如 contosob2c.onmicrosoft.com) 來取代 **{tenant}**。</span><span class="sxs-lookup"><span data-stu-id="76d76-132">Replace **{tenant}** with your tenant's name (for example, contosob2c.onmicrosoft.com).</span></span> <span data-ttu-id="76d76-133">按一下**儲存變更**hello hello 頁底端。</span><span class="sxs-lookup"><span data-stu-id="76d76-133">Click **Save Changes** at hello bottom of hello page.</span></span>
    
    ![Facebook - OAuth 重新導向 URI](./media/active-directory-b2c-setup-fb-app/fb-oauth-redirect-uri.png)
14. <span data-ttu-id="76d76-135">toomake Facebook 應用程式可由 Azure AD B2C，您需要 toomake 公開使用它。</span><span class="sxs-lookup"><span data-stu-id="76d76-135">toomake your Facebook application usable by Azure AD B2C, you need toomake it publicly available.</span></span> <span data-ttu-id="76d76-136">您可以按一下**應用程式檢閱**hello 左瀏覽並開啟 hello 切換 hello 頁面頂端的 hello 太**是**按一下**確認**。</span><span class="sxs-lookup"><span data-stu-id="76d76-136">You can do this by clicking **App Review** on hello left navigation and by turning hello switch at hello top of hello page too**YES** and clicking **Confirm**.</span></span>
    
    ![Facebook - App 公開](./media/active-directory-b2c-setup-fb-app/fb-app-public.png)

## <a name="configure-facebook-as-an-identity-provider-in-your-tenant"></a><span data-ttu-id="76d76-138">將 Facebook 設定為您租用戶中的身分識別提供者</span><span class="sxs-lookup"><span data-stu-id="76d76-138">Configure Facebook as an identity provider in your tenant</span></span>
1. <span data-ttu-id="76d76-139">請遵循下列步驟太[瀏覽 toohello B2C 功能刀鋒視窗](active-directory-b2c-app-registration.md#navigate-to-b2c-settings)hello Azure 入口網站上。</span><span class="sxs-lookup"><span data-stu-id="76d76-139">Follow these steps too[navigate toohello B2C features blade](active-directory-b2c-app-registration.md#navigate-to-b2c-settings) on hello Azure portal.</span></span>
2. <span data-ttu-id="76d76-140">在 hello B2C 功能刀鋒視窗中，按一下 **身分識別提供者**。</span><span class="sxs-lookup"><span data-stu-id="76d76-140">On hello B2C features blade, click **Identity providers**.</span></span>
3. <span data-ttu-id="76d76-141">按一下**+ 加**在 hello hello 刀鋒視窗最上方。</span><span class="sxs-lookup"><span data-stu-id="76d76-141">Click **+Add** at hello top of hello blade.</span></span>
4. <span data-ttu-id="76d76-142">提供方便**名稱**hello 身分識別提供者組態。</span><span class="sxs-lookup"><span data-stu-id="76d76-142">Provide a friendly **Name** for hello identity provider configuration.</span></span> <span data-ttu-id="76d76-143">例如，輸入「Facebook」。</span><span class="sxs-lookup"><span data-stu-id="76d76-143">For example, enter "Facebook".</span></span>
5. <span data-ttu-id="76d76-144">按一下 [識別提供者類型]、選取 [Facebook]，然後按一下 [確定]。</span><span class="sxs-lookup"><span data-stu-id="76d76-144">Click **Identity provider type**, select **Facebook**, and click **OK**.</span></span>
6. <span data-ttu-id="76d76-145">按一下**設定此身分識別提供者**，然後輸入 hello 應用程式識別碼和應用程式密碼 （的 hello 您稍早建立的 Facebook 應用程式) 中 hello**用戶端識別碼**和**用戶端密碼**分別欄位。</span><span class="sxs-lookup"><span data-stu-id="76d76-145">Click **Set up this identity provider** and enter hello app ID and app secret (of hello Facebook application that you created earlier) in hello **Client ID** and **Client secret** fields respectively.</span></span>
7. <span data-ttu-id="76d76-146">按一下**確定**，然後按一下**建立**toosave Facebook 組態。</span><span class="sxs-lookup"><span data-stu-id="76d76-146">Click **OK**, and then click **Create** toosave your Facebook configuration.</span></span>

> [!NOTE]
> <span data-ttu-id="76d76-147">加入**身分識別提供者**tooyour 租用戶不會修改現有的原則。</span><span class="sxs-lookup"><span data-stu-id="76d76-147">Adding an **Identity provider** tooyour tenant does not modify your existing policies.</span></span> <span data-ttu-id="76d76-148">請記住您的原則 tooupdate 包含您剛才建立的 hello 身分識別提供者。</span><span class="sxs-lookup"><span data-stu-id="76d76-148">Remember tooupdate your policies by including hello identity provider you just created.</span></span>
>