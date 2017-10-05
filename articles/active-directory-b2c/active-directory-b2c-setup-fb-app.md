---
title: "Azure Active Directory B2C：Facebook 設定 | Microsoft Docs"
description: "在受 Azure Active Directory B2C 保護的應用程式中，針對具有 Facebook 帳戶的取用者提供註冊和登入。"
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
ms.openlocfilehash: 8c2154fcf33537358b549395d15b4ba937371cd0
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/18/2017
---
# <a name="azure-active-directory-b2c-provide-sign-up-and-sign-in-to-consumers-with-facebook-accounts"></a><span data-ttu-id="74ae6-103">Azure Active Directory B2C：針對具有 Facebook 帳戶的取用者提供註冊和登入</span><span class="sxs-lookup"><span data-stu-id="74ae6-103">Azure Active Directory B2C: Provide sign-up and sign-in to consumers with Facebook accounts</span></span>
## <a name="create-a-facebook-application"></a><span data-ttu-id="74ae6-104">建立 Facebook 應用程式</span><span class="sxs-lookup"><span data-stu-id="74ae6-104">Create a Facebook application</span></span>
<span data-ttu-id="74ae6-105">若要在 Azure Active Directory (Azure AD) B2C 中使用 Facebok 做為身分識別提供者，您必須建立 Facebook 應用程式，並對其提供正確的參數。</span><span class="sxs-lookup"><span data-stu-id="74ae6-105">To use Facebook as an identity provider in Azure Active Directory (Azure AD) B2C, you need to create a Facebook application and supply it with the right parameters.</span></span> <span data-ttu-id="74ae6-106">您需要 Facebook 帳戶來執行此動作。</span><span class="sxs-lookup"><span data-stu-id="74ae6-106">You need a Facebook account to do this.</span></span> <span data-ttu-id="74ae6-107">如果您沒有帳戶，您可以在 [https://www.facebook.com/](https://www.facebook.com/)上取得。</span><span class="sxs-lookup"><span data-stu-id="74ae6-107">If you don’t have one, you can get it at [https://www.facebook.com/](https://www.facebook.com/).</span></span>

1. <span data-ttu-id="74ae6-108">前往 [Facebook for developers (開發人員專用的 Facebook)](https://developers.facebook.com/) 網站，並以您的 Facebook 帳戶認證登入。</span><span class="sxs-lookup"><span data-stu-id="74ae6-108">Go to the [Facebook for developers](https://developers.facebook.com/) website and sign in with your Facebook account credentials.</span></span>
2. <span data-ttu-id="74ae6-109">如果您尚未這麼做，您需要註冊為 Facebook 開發人員。</span><span class="sxs-lookup"><span data-stu-id="74ae6-109">If you have not already done so, you need to register as a Facebook developer.</span></span> <span data-ttu-id="74ae6-110">若要這樣做，請按一下 **[註冊]**  \(位於頁面右上角)、接受 Facebook 的原則，然後完成註冊步驟。</span><span class="sxs-lookup"><span data-stu-id="74ae6-110">To do this, click **Register** (on the upper-right corner of the page), accept Facebook's policies, and complete the registration steps.</span></span>
3. <span data-ttu-id="74ae6-111">按一下 [我的應用程式]，然後按一下 [新增應用程式]。</span><span class="sxs-lookup"><span data-stu-id="74ae6-111">Click **My Apps** and then click **Add a New App**.</span></span> 
4. <span data-ttu-id="74ae6-112">在表單中，提供**顯示名稱**和有效的**連絡人電子郵件**。</span><span class="sxs-lookup"><span data-stu-id="74ae6-112">In the form, provide a **Display Name** and a valid **Contact Email**.</span></span>
5. <span data-ttu-id="74ae6-113">按一下 [建立應用程式識別碼]。</span><span class="sxs-lookup"><span data-stu-id="74ae6-113">Click **Create App ID**.</span></span> <span data-ttu-id="74ae6-114">這可能會要求您接受 Facebook 平台原則，並完成線上安全性檢查。</span><span class="sxs-lookup"><span data-stu-id="74ae6-114">This may require you to accept Facebook platform policies and complete an online security check.</span></span>
6. <span data-ttu-id="74ae6-115">在左欄中，按一下 [設定]，然後選取 [基本] \(如果尚未選取)。</span><span class="sxs-lookup"><span data-stu-id="74ae6-115">In the left column, click **Settings** and then select **Basic** if not selected already.</span></span>
7. <span data-ttu-id="74ae6-116">選取一個**類別**。</span><span class="sxs-lookup"><span data-stu-id="74ae6-116">Select a **Category**.</span></span> 
8. <span data-ttu-id="74ae6-117">按一下 [+ 新增平台]，然後選取 [網站]。</span><span class="sxs-lookup"><span data-stu-id="74ae6-117">Click **+ Add Platform** and select **Website**.</span></span>
   
    ![Facebook - 設定](./media/active-directory-b2c-setup-fb-app/fb-settings.png)
   
    ![Facebook - 設定 - 網站](./media/active-directory-b2c-setup-fb-app/fb-website.png)
9. <span data-ttu-id="74ae6-120">在頁面底部的 [網站 URL] 欄位中輸入 `https://login.microsoftonline.com/`，然後按一下 [儲存變更]。</span><span class="sxs-lookup"><span data-stu-id="74ae6-120">Enter `https://login.microsoftonline.com/` in the **Site URL** field and then click **Save Changes** at the bottom of the page.</span></span>
   
    ![Facebook - 網站 URL](./media/active-directory-b2c-setup-fb-app/fb-site-url.png)

10. <span data-ttu-id="74ae6-122">複製 [應用程式識別碼] 的值。</span><span class="sxs-lookup"><span data-stu-id="74ae6-122">Copy the value of **App ID**.</span></span> <span data-ttu-id="74ae6-123">按一下 [顯示]，並複製 [應用程式密碼] 的值。</span><span class="sxs-lookup"><span data-stu-id="74ae6-123">Click **Show** and copy the value of **App Secret**.</span></span> <span data-ttu-id="74ae6-124">您必須同時使用這兩個值，將 Facebook 設定為您租用戶中的身分識別提供者。</span><span class="sxs-lookup"><span data-stu-id="74ae6-124">You will need both of them to configure Facebook as an identity provider in your tenant.</span></span> <span data-ttu-id="74ae6-125">**應用程式密碼**是重要的安全性認證。</span><span class="sxs-lookup"><span data-stu-id="74ae6-125">**App Secret** is an important security credential.</span></span>
   
    ![Facebook - 應用程式識別碼和應用程式密碼](./media/active-directory-b2c-setup-fb-app/fb-app-id-app-secret.png)
11. <span data-ttu-id="74ae6-127">在左側導覽中按一下 [+ 新增產品]，然後按一下 [Facebook 登入] 的 [設定] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="74ae6-127">Click **+ Add Product** on the left navigation and then the **Set Up** button for **Facebook Login**.</span></span>
   
    ![Facebook - Facebook 登入](./media/active-directory-b2c-setup-fb-app/fb-login.png)
12. <span data-ttu-id="74ae6-129">在 [Facebook 登入] 下，按一下右側導覽中的 [設定]</span><span class="sxs-lookup"><span data-stu-id="74ae6-129">Click **Settings** on the right nav under **Facebook Login**</span></span>

    ![Facebook - Facebook 登入設定](./media/active-directory-b2c-setup-fb-app/fb-login-settings.png)
13. <span data-ttu-id="74ae6-131">在 [用戶端 OAuth 設定] 區段的 [有效的 OAuth 重新導向 URI] 欄位中輸入 `https://login.microsoftonline.com/te/{tenant}/oauth2/authresp`。</span><span class="sxs-lookup"><span data-stu-id="74ae6-131">Enter `https://login.microsoftonline.com/te/{tenant}/oauth2/authresp` in the **Valid OAuth redirect URIs** field in the **Client OAuth Settings** section.</span></span> <span data-ttu-id="74ae6-132">使用您的租用戶名稱 (例如 contosob2c.onmicrosoft.com) 來取代 **{tenant}**。</span><span class="sxs-lookup"><span data-stu-id="74ae6-132">Replace **{tenant}** with your tenant's name (for example, contosob2c.onmicrosoft.com).</span></span> <span data-ttu-id="74ae6-133">按一下頁面底部的 [儲存變更]。</span><span class="sxs-lookup"><span data-stu-id="74ae6-133">Click **Save Changes** at the bottom of the page.</span></span>
    
    ![Facebook - OAuth 重新導向 URI](./media/active-directory-b2c-setup-fb-app/fb-oauth-redirect-uri.png)
14. <span data-ttu-id="74ae6-135">若要讓您的 Facebook 應用程式可供 Azure AD B2C 使用，您必須將其設定為對外公開。</span><span class="sxs-lookup"><span data-stu-id="74ae6-135">To make your Facebook application usable by Azure AD B2C, you need to make it publicly available.</span></span> <span data-ttu-id="74ae6-136">若要執行此動作，請在左側導覽中按一下 [應用程式檢閱]，然後將頁面頂端的開關切換為 [是]，並按一下 [確認]。</span><span class="sxs-lookup"><span data-stu-id="74ae6-136">You can do this by clicking **App Review** on the left navigation and by turning the switch at the top of the page to **YES** and clicking **Confirm**.</span></span>
    
    ![Facebook - App 公開](./media/active-directory-b2c-setup-fb-app/fb-app-public.png)

## <a name="configure-facebook-as-an-identity-provider-in-your-tenant"></a><span data-ttu-id="74ae6-138">將 Facebook 設定為您租用戶中的身分識別提供者</span><span class="sxs-lookup"><span data-stu-id="74ae6-138">Configure Facebook as an identity provider in your tenant</span></span>
1. <span data-ttu-id="74ae6-139">遵循下列步驟以 [瀏覽至 B2C 功能刀鋒視窗](active-directory-b2c-app-registration.md#navigate-to-b2c-settings) (位於 Azure 入口網站上)。</span><span class="sxs-lookup"><span data-stu-id="74ae6-139">Follow these steps to [navigate to the B2C features blade](active-directory-b2c-app-registration.md#navigate-to-b2c-settings) on the Azure portal.</span></span>
2. <span data-ttu-id="74ae6-140">在 B2C 功能刀鋒視窗中，按一下 [ **身分識別提供者**]。</span><span class="sxs-lookup"><span data-stu-id="74ae6-140">On the B2C features blade, click **Identity providers**.</span></span>
3. <span data-ttu-id="74ae6-141">按一下刀鋒視窗頂端的 [新增]  。</span><span class="sxs-lookup"><span data-stu-id="74ae6-141">Click **+Add** at the top of the blade.</span></span>
4. <span data-ttu-id="74ae6-142">針對身分識別提供者組態，提供容易辨識的 **名稱** 。</span><span class="sxs-lookup"><span data-stu-id="74ae6-142">Provide a friendly **Name** for the identity provider configuration.</span></span> <span data-ttu-id="74ae6-143">例如，輸入「Facebook」。</span><span class="sxs-lookup"><span data-stu-id="74ae6-143">For example, enter "Facebook".</span></span>
5. <span data-ttu-id="74ae6-144">按一下 [識別提供者類型]、選取 [Facebook]，然後按一下 [確定]。</span><span class="sxs-lookup"><span data-stu-id="74ae6-144">Click **Identity provider type**, select **Facebook**, and click **OK**.</span></span>
6. <span data-ttu-id="74ae6-145">按一下 [設定此識別提供者]，然後在 [用戶端識別碼] 與 [用戶端密碼] 欄位中，分別輸入您先前建立之 Facebook 應用程式的應用程式識別碼和應用程式密碼。</span><span class="sxs-lookup"><span data-stu-id="74ae6-145">Click **Set up this identity provider** and enter the app ID and app secret (of the Facebook application that you created earlier) in the **Client ID** and **Client secret** fields respectively.</span></span>
7. <span data-ttu-id="74ae6-146">依序按一下 [確定] 與 [建立]，以儲存您的 Facebook 設定。</span><span class="sxs-lookup"><span data-stu-id="74ae6-146">Click **OK**, and then click **Create** to save your Facebook configuration.</span></span>

> [!NOTE]
> <span data-ttu-id="74ae6-147">將「識別提供者」新增至您的租用戶不會修改您現有的原則。</span><span class="sxs-lookup"><span data-stu-id="74ae6-147">Adding an **Identity provider** to your tenant does not modify your existing policies.</span></span> <span data-ttu-id="74ae6-148">請記得加入剛才建立的識別提供者，以更新您的原則。</span><span class="sxs-lookup"><span data-stu-id="74ae6-148">Remember to update your policies by including the identity provider you just created.</span></span>
>