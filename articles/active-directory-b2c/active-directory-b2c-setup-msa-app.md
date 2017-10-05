---
title: "Azure Active Directory B2C：Microsoft 帳戶設定 | Microsoft Docs"
description: "在受 Azure Active Directory B2C 保護的應用程式中，針對具有 Microsoft 帳戶的取用者提供註冊和登入。"
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
ms.openlocfilehash: 59879dc0b3fc1d7af3e2a1f67f1701f451de9126
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/18/2017
---
# <a name="azure-active-directory-b2c-provide-sign-up-and-sign-in-to-consumers-with-microsoft-accounts"></a><span data-ttu-id="cb8ed-103">Azure Active Directory B2C：針對具有 Microsoft 帳戶的取用者提供註冊和登入</span><span class="sxs-lookup"><span data-stu-id="cb8ed-103">Azure Active Directory B2C: Provide sign-up and sign-in to consumers with Microsoft accounts</span></span>
## <a name="create-a-microsoft-account-application"></a><span data-ttu-id="cb8ed-104">建立 Microsoft 帳戶應用程式</span><span class="sxs-lookup"><span data-stu-id="cb8ed-104">Create a Microsoft account application</span></span>
<span data-ttu-id="cb8ed-105">若要在 Azure Active Directory (Azure AD) B2C 中使用 Microsoft 帳戶做為識別提供者，您必須建立 Microsoft 帳戶應用程式，然後對其提供正確參數。</span><span class="sxs-lookup"><span data-stu-id="cb8ed-105">To use Microsoft account as an identity provider in Azure Active Directory (Azure AD) B2C, you need to create a Microsoft account application and supply it with the right parameters.</span></span> <span data-ttu-id="cb8ed-106">您需要 Microsoft 帳戶才能執行此動作。</span><span class="sxs-lookup"><span data-stu-id="cb8ed-106">You need a Microsoft account to do this.</span></span> <span data-ttu-id="cb8ed-107">如果您沒有該帳戶，您可以在 [https://www.live.com/](https://www.live.com/)上申請。</span><span class="sxs-lookup"><span data-stu-id="cb8ed-107">If you don’t have one, you can get it at [https://www.live.com/](https://www.live.com/).</span></span>

1. <span data-ttu-id="cb8ed-108">移至 [Microsoft 應用程式註冊入口網站](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList)，並使用您的 Microsoft 帳戶認證登入。</span><span class="sxs-lookup"><span data-stu-id="cb8ed-108">Go to the [Microsoft Application Registration Portal](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList) and sign in with your Microsoft account credentials.</span></span>
2. <span data-ttu-id="cb8ed-109">按一下 [新增應用程式] 。</span><span class="sxs-lookup"><span data-stu-id="cb8ed-109">Click **Add an app**.</span></span>
   
    ![Microsoft 帳戶 - 加入新的應用程式](./media/active-directory-b2c-setup-msa-app/msa-add-new-app.png)
3. <span data-ttu-id="cb8ed-111">為應用程式提供 [名稱]，然後按一下 [建立應用程式]。</span><span class="sxs-lookup"><span data-stu-id="cb8ed-111">Provide a **Name** for your application and click **Create application**.</span></span>
   
    ![Microsoft 帳戶 - 應用程式名稱](./media/active-directory-b2c-setup-msa-app/msa-app-name.png)
4. <span data-ttu-id="cb8ed-113">複製 [應用程式識別碼] 的值。您必須使用此值，將 Microsoft 帳戶於租用戶中設定為識別提供者。</span><span class="sxs-lookup"><span data-stu-id="cb8ed-113">Copy the value of **Application Id**. You will need it to configure Microsoft account as an identity provider in your tenant.</span></span>
   
    ![Microsoft 帳戶 - 應用程式識別碼](./media/active-directory-b2c-setup-msa-app/msa-app-id.png)
5. <span data-ttu-id="cb8ed-115">按一下 [新增平台]，然後選擇 [Web]。</span><span class="sxs-lookup"><span data-stu-id="cb8ed-115">Click on **Add platform** and choose **Web**.</span></span>
   
    ![Microsoft 帳戶 - 新增平台](./media/active-directory-b2c-setup-msa-app/msa-add-platform.png)
   
    ![Microsoft 帳戶 - Web](./media/active-directory-b2c-setup-msa-app/msa-web.png)
6. <span data-ttu-id="cb8ed-118">在 [重新導向 URI] 欄位中輸入 `https://login.microsoftonline.com/te/{tenant}/oauth2/authresp`。</span><span class="sxs-lookup"><span data-stu-id="cb8ed-118">Enter `https://login.microsoftonline.com/te/{tenant}/oauth2/authresp` in the **Redirect URIs** field.</span></span> <span data-ttu-id="cb8ed-119">使用您的租用戶名稱 (例如 contosob2c.onmicrosoft.com) 來取代 **{tenant}**。</span><span class="sxs-lookup"><span data-stu-id="cb8ed-119">Replace **{tenant}** with your tenant's name (for example, contosob2c.onmicrosoft.com).</span></span>
   
    ![Microsoft 帳戶 - 重新導向 URL](./media/active-directory-b2c-setup-msa-app/msa-redirect-url.png)
7. <span data-ttu-id="cb8ed-121">按一下 [應用程式密碼] 區段底下的 [產生新密碼]。</span><span class="sxs-lookup"><span data-stu-id="cb8ed-121">Click on **Generate New Password** under the **Application Secrets** section.</span></span> <span data-ttu-id="cb8ed-122">複製螢幕上顯示的新密碼。</span><span class="sxs-lookup"><span data-stu-id="cb8ed-122">Copy the new password displayed on screen.</span></span> <span data-ttu-id="cb8ed-123">您必須使用此值，將 Microsoft 帳戶於租用戶中設定為識別提供者。</span><span class="sxs-lookup"><span data-stu-id="cb8ed-123">You will need it to configure Microsoft account as an identity provider in your tenant.</span></span> <span data-ttu-id="cb8ed-124">此密碼是重要的安全性認證。</span><span class="sxs-lookup"><span data-stu-id="cb8ed-124">This password is an important security credential.</span></span>
   
    ![Microsoft 帳戶 - 產生新密碼](./media/active-directory-b2c-setup-msa-app/msa-generate-new-password.png)
   
    ![Microsoft 帳戶 - 新密碼](./media/active-directory-b2c-setup-msa-app/msa-new-password.png)
8. <span data-ttu-id="cb8ed-127">勾選 [進階選項] 區段底下顯示 [Live SDK 支援] 的方塊。</span><span class="sxs-lookup"><span data-stu-id="cb8ed-127">Check the box that says **Live SDK support** under the **Advanced Options** section.</span></span> <span data-ttu-id="cb8ed-128">按一下 [儲存] 。</span><span class="sxs-lookup"><span data-stu-id="cb8ed-128">Click **Save**.</span></span>
   
    ![Microsoft 帳戶 - Live SDK 支援](./media/active-directory-b2c-setup-msa-app/msa-live-sdk-support.png)

## <a name="configure-microsoft-account-as-an-identity-provider-in-your-tenant"></a><span data-ttu-id="cb8ed-130">將 Microsoft 帳戶於租用戶中設定為識別提供者</span><span class="sxs-lookup"><span data-stu-id="cb8ed-130">Configure Microsoft account as an identity provider in your tenant</span></span>
1. <span data-ttu-id="cb8ed-131">遵循下列步驟以 [瀏覽至 B2C 功能刀鋒視窗](active-directory-b2c-app-registration.md#navigate-to-b2c-settings) (位於 Azure 入口網站上)。</span><span class="sxs-lookup"><span data-stu-id="cb8ed-131">Follow these steps to [navigate to the B2C features blade](active-directory-b2c-app-registration.md#navigate-to-b2c-settings) on the Azure portal.</span></span>
2. <span data-ttu-id="cb8ed-132">在 B2C 功能刀鋒視窗中，按一下 [ **身分識別提供者**]。</span><span class="sxs-lookup"><span data-stu-id="cb8ed-132">On the B2C features blade, click **Identity providers**.</span></span>
3. <span data-ttu-id="cb8ed-133">按一下刀鋒視窗頂端的 [新增]  。</span><span class="sxs-lookup"><span data-stu-id="cb8ed-133">Click **+Add** at the top of the blade.</span></span>
4. <span data-ttu-id="cb8ed-134">針對身分識別提供者組態，提供容易辨識的 **名稱** 。</span><span class="sxs-lookup"><span data-stu-id="cb8ed-134">Provide a friendly **Name** for the identity provider configuration.</span></span> <span data-ttu-id="cb8ed-135">例如，輸入 "MSA"。</span><span class="sxs-lookup"><span data-stu-id="cb8ed-135">For example, enter "MSA".</span></span>
5. <span data-ttu-id="cb8ed-136">按一下 [識別提供者類型]、選取 [Microsoft 帳戶]，然後按一下 [確定]。</span><span class="sxs-lookup"><span data-stu-id="cb8ed-136">Click **Identity provider type**, select **Microsoft account**, and click **OK**.</span></span>
6. <span data-ttu-id="cb8ed-137">按一下 [設定此身分識別提供者]  ，然後輸入您先前建立的 Microsoft 帳戶應用程式的應用程式識別碼和密碼。</span><span class="sxs-lookup"><span data-stu-id="cb8ed-137">Click **Set up this identity provider** and enter the Application Id and password of the Microsoft account application that you created earlier.</span></span>
7. <span data-ttu-id="cb8ed-138">依序按一下 [確定] 與 [建立]，以儲存您的 Microsoft 帳戶設定。</span><span class="sxs-lookup"><span data-stu-id="cb8ed-138">Click **OK** and then click **Create** to save your Microsoft account configuration.</span></span>

