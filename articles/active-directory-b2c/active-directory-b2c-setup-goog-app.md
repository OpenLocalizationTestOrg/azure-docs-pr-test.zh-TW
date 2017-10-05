---
title: "Azure Active Directory B2C：Google+ 設定 | Microsoft Docs"
description: "在受 Azure Active Directory B2C 保護的應用程式中，針對具有 Google+ 帳戶的取用者提供註冊和登入。"
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
ms.openlocfilehash: 6ab73e5c79742ab548733f5712dee1e28461db9f
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/18/2017
---
# <a name="azure-active-directory-b2c-provide-sign-up-and-sign-in-to-consumers-with-google-accounts"></a><span data-ttu-id="a4b1b-103">Azure Active Directory B2C：針對具有 Google+ 帳戶的取用者提供註冊和登入</span><span class="sxs-lookup"><span data-stu-id="a4b1b-103">Azure Active Directory B2C: Provide sign-up and sign-in to consumers with Google+ accounts</span></span>
## <a name="create-a-google-application"></a><span data-ttu-id="a4b1b-104">建立 Google+ 應用程式</span><span class="sxs-lookup"><span data-stu-id="a4b1b-104">Create a Google+ application</span></span>
<span data-ttu-id="a4b1b-105">若要在 Azure Active Directory (Azure AD) B2C 中使用 Google+ 做為身分識別提供者，您必須建立 Google+ 應用程式，並對其提供正確參數。</span><span class="sxs-lookup"><span data-stu-id="a4b1b-105">To use Google+ as an identity provider in Azure Active Directory (Azure AD) B2C, you need to create a Google+ application and supply it with the right parameters.</span></span> <span data-ttu-id="a4b1b-106">您需要 Google+ 帳戶才能執行此動作。</span><span class="sxs-lookup"><span data-stu-id="a4b1b-106">You need a Google+ account to do this.</span></span> <span data-ttu-id="a4b1b-107">如果您沒有該帳戶，您可以在 [https://accounts.google.com/SignUp](https://accounts.google.com/SignUp)上申請。</span><span class="sxs-lookup"><span data-stu-id="a4b1b-107">If you don’t have one, you can get it at [https://accounts.google.com/SignUp](https://accounts.google.com/SignUp).</span></span>

1. <span data-ttu-id="a4b1b-108">前往 [Google 開發人員主控台](https://console.developers.google.com/) ，並以您的 Google + 帳戶認證登入。</span><span class="sxs-lookup"><span data-stu-id="a4b1b-108">Go to the [Google Developers Console](https://console.developers.google.com/) and sign in with your Google+ account credentials.</span></span>
2. <span data-ttu-id="a4b1b-109">按一下 [建立專案]，輸入 [專案名稱]，接著按一下 [建立]。</span><span class="sxs-lookup"><span data-stu-id="a4b1b-109">Click **Create project**, enter a **Project name**, and then click **Create**.</span></span>
   
    ![Google+ - 開始使用](./media/active-directory-b2c-setup-goog-app/google-get-started.png)
   
    ![Google+ - 新增專案](./media/active-directory-b2c-setup-goog-app/google-new-project.png)
3. <span data-ttu-id="a4b1b-112">在左側導覽中，按一下 [API 管理員]，然後按一下 [認證]。</span><span class="sxs-lookup"><span data-stu-id="a4b1b-112">Click **API Manager** and then click **Credentials** in the left navigation.</span></span>
4. <span data-ttu-id="a4b1b-113">按一下位於頂端的 [OAuth 同意畫面]  索引標籤。</span><span class="sxs-lookup"><span data-stu-id="a4b1b-113">Click the **OAuth consent screen** tab at the top.</span></span>
   
    ![Google+ - 認證](./media/active-directory-b2c-setup-goog-app/google-add-cred.png)
5. <span data-ttu-id="a4b1b-115">選取或指定有效的**電子郵件地址**、提供**產品名稱**，然後按一下 [儲存]。</span><span class="sxs-lookup"><span data-stu-id="a4b1b-115">Select or specify a valid **Email address**, provide a **Product name**, and click **Save**.</span></span>
   
    ![Google+ - OAuth 同意畫面](./media/active-directory-b2c-setup-goog-app/google-consent-screen.png)
6. <span data-ttu-id="a4b1b-117">按一下 [新增認證]，然後選擇 [OAuth 用戶端識別碼]。</span><span class="sxs-lookup"><span data-stu-id="a4b1b-117">Click **New credentials** and then choose **OAuth client ID**.</span></span>
   
    ![Google+ - OAuth 同意畫面](./media/active-directory-b2c-setup-goog-app/google-add-oauth2-client-id.png)
7. <span data-ttu-id="a4b1b-119">在 [應用程式類型] 下方，選取 [Web 應用程式]。</span><span class="sxs-lookup"><span data-stu-id="a4b1b-119">Under **Application type**, select **Web application**.</span></span>
   
    ![Google+ - OAuth 同意畫面](./media/active-directory-b2c-setup-goog-app/google-web-app.png)
8. <span data-ttu-id="a4b1b-121">提供應用程式的**名稱**，在 [授權 JavaScript 來源] 欄位中輸入 `https://login.microsoftonline.com`，接著在 [授權重新導向 URI] 欄位中輸入 `https://login.microsoftonline.com/te/{tenant}/oauth2/authresp`。</span><span class="sxs-lookup"><span data-stu-id="a4b1b-121">Provide a **Name** for your application, enter `https://login.microsoftonline.com` in the **Authorized JavaScript origins** field, and `https://login.microsoftonline.com/te/{tenant}/oauth2/authresp` in the **Authorized redirect URIs** field.</span></span> <span data-ttu-id="a4b1b-122">使用您的租用戶名稱 (例如 contosob2c.onmicrosoft.com) 來取代 **{tenant}**。</span><span class="sxs-lookup"><span data-stu-id="a4b1b-122">Replace **{tenant}** with your tenant's name (for example, contosob2c.onmicrosoft.com).</span></span> <span data-ttu-id="a4b1b-123">**{tenant}** 值會區分大小寫。</span><span class="sxs-lookup"><span data-stu-id="a4b1b-123">The **{tenant}** value is case-sensitive.</span></span> <span data-ttu-id="a4b1b-124">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="a4b1b-124">Click **Create**.</span></span>
   
    ![Google+ -  建立用戶端識別碼](./media/active-directory-b2c-setup-goog-app/google-create-client-id.png)
9. <span data-ttu-id="a4b1b-126">複製 [用戶端識別碼] 和 [用戶端密碼] 的值。</span><span class="sxs-lookup"><span data-stu-id="a4b1b-126">Copy the values of **Client ID** and **Client secret**.</span></span> <span data-ttu-id="a4b1b-127">您必須使用這兩個值，將 Google+ 設為租用戶中的身分識別提供者。</span><span class="sxs-lookup"><span data-stu-id="a4b1b-127">You will need both of them to configure Google+ as an identity provider in your tenant.</span></span> <span data-ttu-id="a4b1b-128">**用戶端密碼** 是重要的安全性認證。</span><span class="sxs-lookup"><span data-stu-id="a4b1b-128">**Client secret** is an important security credential.</span></span>
   
    ![Google+ - 用戶端密碼](./media/active-directory-b2c-setup-goog-app/google-client-secret.png)

## <a name="configure-google-as-an-identity-provider-in-your-tenant"></a><span data-ttu-id="a4b1b-130">將 Google+ 帳戶於租用戶中設定為識別提供者</span><span class="sxs-lookup"><span data-stu-id="a4b1b-130">Configure Google+ as an identity provider in your tenant</span></span>
1. <span data-ttu-id="a4b1b-131">遵循下列步驟以 [瀏覽至 B2C 功能刀鋒視窗](active-directory-b2c-app-registration.md#navigate-to-b2c-settings) (位於 Azure 入口網站上)。</span><span class="sxs-lookup"><span data-stu-id="a4b1b-131">Follow these steps to [navigate to the B2C features blade](active-directory-b2c-app-registration.md#navigate-to-b2c-settings) on the Azure portal.</span></span>
2. <span data-ttu-id="a4b1b-132">在 B2C 功能刀鋒視窗中，按一下 [ **身分識別提供者**]。</span><span class="sxs-lookup"><span data-stu-id="a4b1b-132">On the B2C features blade, click **Identity providers**.</span></span>
3. <span data-ttu-id="a4b1b-133">按一下刀鋒視窗頂端的 [新增]  。</span><span class="sxs-lookup"><span data-stu-id="a4b1b-133">Click **+Add** at the top of the blade.</span></span>
4. <span data-ttu-id="a4b1b-134">針對身分識別提供者組態，提供容易辨識的 **名稱** 。</span><span class="sxs-lookup"><span data-stu-id="a4b1b-134">Provide a friendly **Name** for the identity provider configuration.</span></span> <span data-ttu-id="a4b1b-135">例如，輸入 "G+"。</span><span class="sxs-lookup"><span data-stu-id="a4b1b-135">For example, enter "G+".</span></span>
5. <span data-ttu-id="a4b1b-136">按一下 [識別提供者類型]、選取 [Google]，然後按一下 [確定]。</span><span class="sxs-lookup"><span data-stu-id="a4b1b-136">Click **Identity provider type**, select **Google**, and click **OK**.</span></span>
6. <span data-ttu-id="a4b1b-137">按一下 [設定此識別提供者]  ，然後輸入您先前建立的 Google+ 應用程式用戶端識別碼和用戶端密碼。</span><span class="sxs-lookup"><span data-stu-id="a4b1b-137">Click **Set up this identity provider** and enter the client ID and client secret of the Google+ application that you created earlier.</span></span>
7. <span data-ttu-id="a4b1b-138">依序按一下 [確定] 和 [建立]，儲存您的 Google+ 設定。</span><span class="sxs-lookup"><span data-stu-id="a4b1b-138">Click **OK** and then click **Create** to save your Google+ configuration.</span></span>

