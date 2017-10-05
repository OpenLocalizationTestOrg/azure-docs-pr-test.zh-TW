---
title: "Azure Active Directory B2C：QQ 設定 | Microsoft Docs"
description: "在受 Azure Active Directory B2C 保護的應用程式中，針對具有 QQ 帳戶的取用者提供註冊和登入。"
services: active-directory-b2c
documentationcenter: 
author: parakhj
manager: krassk
editor: parakhj
ms.assetid: 18c2cf94-8004-4de1-81c2-e45be65ce12d
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 3/26/2017
ms.author: parakhj
ms.openlocfilehash: b32e81494b8c84799485f154ae43ad30af394caa
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/18/2017
---
# <a name="azure-active-directory-b2c-provide-sign-up-and-sign-in-to-consumers-with-qq-accounts"></a><span data-ttu-id="c34e4-103">Azure Active Directory B2C：針對具有QQ 帳戶的取用者提供註冊和登入</span><span class="sxs-lookup"><span data-stu-id="c34e4-103">Azure Active Directory B2C: Provide sign-up and sign-in to consumers with QQ accounts</span></span>

> [!NOTE]
> <span data-ttu-id="c34e4-104">這項功能處於預覽狀態。</span><span class="sxs-lookup"><span data-stu-id="c34e4-104">This feature is in preview.</span></span>
> 

## <a name="create-a-qq-application"></a><span data-ttu-id="c34e4-105">建立 QQ 應用程式</span><span class="sxs-lookup"><span data-stu-id="c34e4-105">Create a QQ application</span></span>

<span data-ttu-id="c34e4-106">若要在 Azure Active Directory (Azure AD) B2C 中使用 QQ 做為識別提供者，您必須建立 QQ 應用程式，並對其提供正確參數。</span><span class="sxs-lookup"><span data-stu-id="c34e4-106">To use QQ as an identity provider in Azure Active Directory (Azure AD) B2C, you need to create a QQ application and supply it with the right parameters.</span></span> <span data-ttu-id="c34e4-107">您需要 QQ 帳戶才能執行此動作。</span><span class="sxs-lookup"><span data-stu-id="c34e4-107">You need a QQ account to do this.</span></span> <span data-ttu-id="c34e4-108">如果您沒有帳戶，您可以在 [https://ssl.zc.qq.com/en/index.html?type=1&ptlang=1033](https://ssl.zc.qq.com/en/index.html?type=1&ptlang=1033) 上取得一個。</span><span class="sxs-lookup"><span data-stu-id="c34e4-108">If you don’t have one, you can get one at [https://ssl.zc.qq.com/en/index.html?type=1&ptlang=1033](https://ssl.zc.qq.com/en/index.html?type=1&ptlang=1033).</span></span>

### <a name="register-for-the-qq-developer-program"></a><span data-ttu-id="c34e4-109">註冊 QQ 開發人員計劃</span><span class="sxs-lookup"><span data-stu-id="c34e4-109">Register for the QQ developer program</span></span>

1. <span data-ttu-id="c34e4-110">移至 [QQ 開發人員入口網站](http://open.qq.com)並以您的 QQ 帳戶認證登入。</span><span class="sxs-lookup"><span data-stu-id="c34e4-110">Go to the [QQ developer portal](http://open.qq.com) and sign in with your QQ account credentials.</span></span>
2. <span data-ttu-id="c34e4-111">登入之後，請移至 [http://open.qq.com/reg](http://open.qq.com/reg)，將您自己註冊為開發人員。</span><span class="sxs-lookup"><span data-stu-id="c34e4-111">After signing in, go to [http://open.qq.com/reg](http://open.qq.com/reg) to register yourself as a developer.</span></span>
3. <span data-ttu-id="c34e4-112">在功能表中，選取 [个人] \(個人開發人員)。</span><span class="sxs-lookup"><span data-stu-id="c34e4-112">In the menu, select **个人** (individual developer).</span></span>
4. <span data-ttu-id="c34e4-113">在表單中輸入所需的資訊，然後按 [下一步]。</span><span class="sxs-lookup"><span data-stu-id="c34e4-113">Enter the required information into the form and click **下一步** (next step).</span></span>
5. <span data-ttu-id="c34e4-114">完成電子郵件驗證程序。</span><span class="sxs-lookup"><span data-stu-id="c34e4-114">Complete the email verification process.</span></span>

> [!NOTE]
> <span data-ttu-id="c34e4-115">在註冊為開發人員之後，您必須等待數天以進行核准。</span><span class="sxs-lookup"><span data-stu-id="c34e4-115">You will need to wait a few days to be approved after registering as a developer.</span></span> 

### <a name="register-a-qq-application"></a><span data-ttu-id="c34e4-116">註冊 QQ 應用程式</span><span class="sxs-lookup"><span data-stu-id="c34e4-116">Register a QQ application</span></span>

1. <span data-ttu-id="c34e4-117">移至 [https://connect.qq.com/index.html](https://connect.qq.com/index.html)。</span><span class="sxs-lookup"><span data-stu-id="c34e4-117">Go to [https://connect.qq.com/index.html](https://connect.qq.com/index.html).</span></span>
2. <span data-ttu-id="c34e4-118">按一下 [应用管理] \(應用程式管理)。</span><span class="sxs-lookup"><span data-stu-id="c34e4-118">Click on **应用管理** (app management).</span></span>
3. <span data-ttu-id="c34e4-119">按一下 [创建应用] \(建立應用程式)。</span><span class="sxs-lookup"><span data-stu-id="c34e4-119">Click on **创建应用** (create app).</span></span>
4. <span data-ttu-id="c34e4-120">輸入必要的應用程式資訊。</span><span class="sxs-lookup"><span data-stu-id="c34e4-120">Enter the necessary app information.</span></span>
5. <span data-ttu-id="c34e4-121">按一下 [创建应用] \(建立應用程式)。</span><span class="sxs-lookup"><span data-stu-id="c34e4-121">Click on **创建应用** (create app).</span></span>
6. <span data-ttu-id="c34e4-122">輸入必要資訊。</span><span class="sxs-lookup"><span data-stu-id="c34e4-122">Enter the required information.</span></span>
7. <span data-ttu-id="c34e4-123">針對 [授权回调域] \(回呼 URL) 欄位，輸入 `https://login.microsoftonline.com/te/{tenant_name}/oauth2/authresp`。</span><span class="sxs-lookup"><span data-stu-id="c34e4-123">For the **授权回调域** (callback URL) field, enter `https://login.microsoftonline.com/te/{tenant_name}/oauth2/authresp`.</span></span> <span data-ttu-id="c34e4-124">例如，如果您的 `tenant_name` 是 contoso.onmicrosoft.com，請將 URL 設為 `https://login.microsoftonline.com/te/contoso.onmicrosoft.com/oauth2/authresp`。</span><span class="sxs-lookup"><span data-stu-id="c34e4-124">For example, if your `tenant_name` is contoso.onmicrosoft.com, set the URL to be `https://login.microsoftonline.com/te/contoso.onmicrosoft.com/oauth2/authresp`.</span></span>
8. <span data-ttu-id="c34e4-125">按一下 [创建应用] \(建立應用程式)。</span><span class="sxs-lookup"><span data-stu-id="c34e4-125">Click on **创建应用** (create app).</span></span>
9. <span data-ttu-id="c34e4-126">在 [確認] 頁面上，按一下 [应用管理] \(應用程式管理) 以返回應用程式管理頁面。</span><span class="sxs-lookup"><span data-stu-id="c34e4-126">On the confirmation page, click on **应用管理** (app management) to return to the app management page.</span></span>
10. <span data-ttu-id="c34e4-127">在您剛建立的應用程式旁邊，按一下 [查看] \(檢視)。</span><span class="sxs-lookup"><span data-stu-id="c34e4-127">Click on **查看** (view) next to the app you just created.</span></span>
11. <span data-ttu-id="c34e4-128">按一下 [修改] \(編輯)。</span><span class="sxs-lookup"><span data-stu-id="c34e4-128">Click on **修改** (edit).</span></span>
12. <span data-ttu-id="c34e4-129">從頁面頂端複製**應用程式識別碼**和**應用程式金鑰**。</span><span class="sxs-lookup"><span data-stu-id="c34e4-129">From the top of the page, copy the **APP ID** and **APP KEY**.</span></span>

## <a name="configure-qq-as-an-identity-provider-in-your-tenant"></a><span data-ttu-id="c34e4-130">在租用戶中將 QQ 設為識別提供者</span><span class="sxs-lookup"><span data-stu-id="c34e4-130">Configure QQ as an identity provider in your tenant</span></span>
1. <span data-ttu-id="c34e4-131">遵循下列步驟以 [瀏覽至 B2C 功能刀鋒視窗](active-directory-b2c-app-registration.md#navigate-to-b2c-settings) (位於 Azure 入口網站上)。</span><span class="sxs-lookup"><span data-stu-id="c34e4-131">Follow these steps to [navigate to the B2C features blade](active-directory-b2c-app-registration.md#navigate-to-b2c-settings) on the Azure portal.</span></span>
2. <span data-ttu-id="c34e4-132">在 B2C 功能刀鋒視窗中，按一下 [ **身分識別提供者**]。</span><span class="sxs-lookup"><span data-stu-id="c34e4-132">On the B2C features blade, click **Identity providers**.</span></span>
3. <span data-ttu-id="c34e4-133">按一下刀鋒視窗頂端的 [新增]  。</span><span class="sxs-lookup"><span data-stu-id="c34e4-133">Click **+Add** at the top of the blade.</span></span>
4. <span data-ttu-id="c34e4-134">針對身分識別提供者組態，提供容易辨識的 **名稱** 。</span><span class="sxs-lookup"><span data-stu-id="c34e4-134">Provide a friendly **Name** for the identity provider configuration.</span></span> <span data-ttu-id="c34e4-135">例如，輸入 "QQ"。</span><span class="sxs-lookup"><span data-stu-id="c34e4-135">For example, enter "QQ".</span></span>
5. <span data-ttu-id="c34e4-136">按一下 [識別提供者類型]、選取 [QQ]，然後按一下 [確定]。</span><span class="sxs-lookup"><span data-stu-id="c34e4-136">Click **Identity provider type**, select **QQ**, and click **OK**.</span></span>
6. <span data-ttu-id="c34e4-137">按一下 [設定此識別提供者]。</span><span class="sxs-lookup"><span data-stu-id="c34e4-137">Click **Set up this identity provider**</span></span>
7. <span data-ttu-id="c34e4-138">輸入您稍早複製為**用戶端識別碼**的**應用程式金鑰**。</span><span class="sxs-lookup"><span data-stu-id="c34e4-138">Enter the **App Key** that you copied earlier as the **Client ID**.</span></span>
8. <span data-ttu-id="c34e4-139">輸入您稍早複製為**用戶端密碼**的**應用程式密碼**。</span><span class="sxs-lookup"><span data-stu-id="c34e4-139">Enter the **App Secret** that you copied earlier as the **Client Secret**.</span></span>
9. <span data-ttu-id="c34e4-140">依序按一下 [確定] 和 [建立]，儲存您的 QQ 設定。</span><span class="sxs-lookup"><span data-stu-id="c34e4-140">Click **OK** and then click **Create** to save your QQ configuration.</span></span>

