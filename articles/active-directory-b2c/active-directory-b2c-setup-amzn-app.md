---
title: "Azure Active Directory B2C：Amazon 設定 | Microsoft Docs"
description: "在受 Azure Active Directory B2C 保護的應用程式中，針對具有 Amazon 帳戶的取用者提供註冊和登入。"
services: active-directory-b2c
documentationcenter: 
author: swkrish
manager: mbaldwin
editor: bryanla
ms.assetid: 77c099bb-a005-4d75-87f9-f61e3de48725
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/06/2016
ms.author: swkrish
ms.openlocfilehash: dcc97e1b7f6287bd7692c52bf068950065a26572
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/18/2017
---
# <a name="azure-active-directory-b2c-provide-sign-up-and-sign-in-to-consumers-with-amazon-accounts"></a><span data-ttu-id="de236-103">Azure Active Directory B2C：針對具有 Amazon 帳戶的取用者提供註冊和登入</span><span class="sxs-lookup"><span data-stu-id="de236-103">Azure Active Directory B2C: Provide sign-up and sign-in to consumers with Amazon accounts</span></span>
## <a name="create-an-amazon-application"></a><span data-ttu-id="de236-104">建立 Amazon 應用程式</span><span class="sxs-lookup"><span data-stu-id="de236-104">Create an Amazon application</span></span>
<span data-ttu-id="de236-105">若要在 Azure Active Directory (Azure AD) B2C 中使用 Amazon 做為身分識別提供者，您必須建立 Amazon 應用程式，並對其提供正確的參數。</span><span class="sxs-lookup"><span data-stu-id="de236-105">To use Amazon as an identity provider in Azure Active Directory (Azure AD) B2C, you need to create an Amazon application and supply it with the right parameters.</span></span> <span data-ttu-id="de236-106">您需要 Amazon 帳戶來執行此動作。</span><span class="sxs-lookup"><span data-stu-id="de236-106">You need an Amazon account to do this.</span></span> <span data-ttu-id="de236-107">如果您沒有帳戶，您可以在 [http://www.amazon.com/](http://www.amazon.com/)上取得。</span><span class="sxs-lookup"><span data-stu-id="de236-107">If you don’t have one, you can get it at [http://www.amazon.com/](http://www.amazon.com/).</span></span>

1. <span data-ttu-id="de236-108">移至 [Amazon Developer Center (Amazon 開發人員中心)](https://login.amazon.com/) ，並以您的 Amazon 帳戶認證登入。</span><span class="sxs-lookup"><span data-stu-id="de236-108">Go to the [Amazon Developer Center](https://login.amazon.com/) and sign in with your Amazon account credentials.</span></span>
2. <span data-ttu-id="de236-109">若您尚未執行此動作，請按一下 [註冊] 、遵循開發人員註冊步驟，並接受原則。</span><span class="sxs-lookup"><span data-stu-id="de236-109">If you have not already done so, click **Sign Up**, follow the developer registration steps, and accept the policy.</span></span>
3. <span data-ttu-id="de236-110">按一下 [註冊新應用程式] 。</span><span class="sxs-lookup"><span data-stu-id="de236-110">Click **Register new application**.</span></span>
   
    ![在 Amazon 網站上註冊新的應用程式](./media/active-directory-b2c-setup-amzn-app/amzn-new-app.png)
4. <span data-ttu-id="de236-112">提供應用程式資訊 (**名稱**、**說明**和**隱私權注意事項 URL**)，然後按一下 [儲存]。</span><span class="sxs-lookup"><span data-stu-id="de236-112">Provide application information (**Name**, **Description**, and **Privacy Notice URL**) and click **Save**.</span></span>
   
    ![提供應用程式資訊以便在 Amazon 上註冊新的應用程式](./media/active-directory-b2c-setup-amzn-app/amzn-register-app.png)
5. <span data-ttu-id="de236-114">在 [Web 設定] 區段中，複製 [用戶端識別碼] 和 [用戶端密碼] 的值。</span><span class="sxs-lookup"><span data-stu-id="de236-114">In the **Web Settings** section, copy the values of **Client ID** and **Client Secret**.</span></span> <span data-ttu-id="de236-115">(您需要按一下 [顯示密碼] 按鈕，才能看到它)。您必須使用這兩個值，將 Amazon 設為租用戶中的身分識別提供者。</span><span class="sxs-lookup"><span data-stu-id="de236-115">(You need to click the **Show Secret** button to see this.) You need both of them to configure Amazon as an identity provider in your tenant.</span></span> <span data-ttu-id="de236-116">按一下位於區段底部的 [編輯]。</span><span class="sxs-lookup"><span data-stu-id="de236-116">Click **Edit** at the bottom of the section.</span></span> <span data-ttu-id="de236-117">**用戶端密碼** 是重要的安全性認證。</span><span class="sxs-lookup"><span data-stu-id="de236-117">**Client Secret** is an important security credential.</span></span>
   
    ![針對您在 Amazon 上的新應用程式提供用戶端識別碼和用戶端密碼](./media/active-directory-b2c-setup-amzn-app/amzn-client-secret.png)
6. <span data-ttu-id="de236-119">在 [允許的 JavaScript 原始來源] 欄位中輸入 `https://login.microsoftonline.com`，並在 [允許的傳回 URL] 欄位中輸入 `https://login.microsoftonline.com/te/{tenant}/oauth2/authresp`。</span><span class="sxs-lookup"><span data-stu-id="de236-119">Enter `https://login.microsoftonline.com` in the **Allowed JavaScript Origins** field and `https://login.microsoftonline.com/te/{tenant}/oauth2/authresp` in the **Allowed Return URLs** field.</span></span> <span data-ttu-id="de236-120">使用您的租用戶名稱 (例如 contoso.onmicrosoft.com) 來取代 **{tenant}**。</span><span class="sxs-lookup"><span data-stu-id="de236-120">Replace **{tenant}** with your tenant's name (for example, contoso.onmicrosoft.com).</span></span> <span data-ttu-id="de236-121">按一下 [儲存] 。</span><span class="sxs-lookup"><span data-stu-id="de236-121">Click **Save**.</span></span> <span data-ttu-id="de236-122">**{tenant}** 值會區分大小寫。</span><span class="sxs-lookup"><span data-stu-id="de236-122">The **{tenant}** value is case-sensitive.</span></span>
   
    ![針對您在 Amazon 上的新應用程式提供 JavaScript 原始來源及傳回 URL](./media/active-directory-b2c-setup-amzn-app/amzn-urls.png)

## <a name="configure-amazon-as-an-identity-provider-in-your-tenant"></a><span data-ttu-id="de236-124">將 Amazon 設為您租用戶中的身分識別提供者</span><span class="sxs-lookup"><span data-stu-id="de236-124">Configure Amazon as an identity provider in your tenant</span></span>
1. <span data-ttu-id="de236-125">遵循下列步驟以 [瀏覽至 B2C 功能刀鋒視窗](active-directory-b2c-app-registration.md#navigate-to-b2c-settings) (位於 Azure 入口網站上)。</span><span class="sxs-lookup"><span data-stu-id="de236-125">Follow these steps to [navigate to the B2C features blade](active-directory-b2c-app-registration.md#navigate-to-b2c-settings) on the Azure portal.</span></span>
2. <span data-ttu-id="de236-126">在 B2C 功能刀鋒視窗中，按一下 [ **身分識別提供者**]。</span><span class="sxs-lookup"><span data-stu-id="de236-126">On the B2C features blade, click **Identity providers**.</span></span>
3. <span data-ttu-id="de236-127">按一下刀鋒視窗頂端的 [新增]  。</span><span class="sxs-lookup"><span data-stu-id="de236-127">Click **+Add** at the top of the blade.</span></span>
4. <span data-ttu-id="de236-128">針對身分識別提供者組態，提供容易辨識的 **名稱** 。</span><span class="sxs-lookup"><span data-stu-id="de236-128">Provide a friendly **Name** for the identity provider configuration.</span></span> <span data-ttu-id="de236-129">例如，輸入 "Amzn"。</span><span class="sxs-lookup"><span data-stu-id="de236-129">For example, enter "Amzn".</span></span>
5. <span data-ttu-id="de236-130">按一下 [識別提供者類型]、選取 [Amazon]，然後按一下 [確定]。</span><span class="sxs-lookup"><span data-stu-id="de236-130">Click **Identity provider type**, select **Amazon**, and click **OK**.</span></span>
6. <span data-ttu-id="de236-131">按一下 [設定此身分識別提供者]  ，然後輸入您先前建立之 Amazon 應用程式的用戶端識別碼與用戶端密碼。</span><span class="sxs-lookup"><span data-stu-id="de236-131">Click **Set up this identity provider** and enter the client ID and client secret of the Amazon application that you created earlier.</span></span>
7. <span data-ttu-id="de236-132">依序按一下 [確定] 和 [建立]，以儲存您的 Amazon 設定。</span><span class="sxs-lookup"><span data-stu-id="de236-132">Click **OK** and then click **Create** to save your Amazon configuration.</span></span>

