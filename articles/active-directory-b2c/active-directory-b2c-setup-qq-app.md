---
title: "Azure Active Directory B2C：QQ 設定 | Microsoft Docs"
description: "提供註冊和登入 tooconsumers QQ 帳戶，在受保護的 Azure Active Directory B2C 的應用程式中使用。"
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
ms.openlocfilehash: 896d6221e01d15de1652a5717cf1f65619101e0c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2c-provide-sign-up-and-sign-in-tooconsumers-with-qq-accounts"></a><span data-ttu-id="74618-103">Azure Active Directory B2C： 註冊和登入 tooconsumers 提供 QQ 帳戶</span><span class="sxs-lookup"><span data-stu-id="74618-103">Azure Active Directory B2C: Provide sign-up and sign-in tooconsumers with QQ accounts</span></span>

> [!NOTE]
> <span data-ttu-id="74618-104">這項功能處於預覽狀態。</span><span class="sxs-lookup"><span data-stu-id="74618-104">This feature is in preview.</span></span>
> 

## <a name="create-a-qq-application"></a><span data-ttu-id="74618-105">建立 QQ 應用程式</span><span class="sxs-lookup"><span data-stu-id="74618-105">Create a QQ application</span></span>

<span data-ttu-id="74618-106">toouse QQ B2C Azure Active Directory (Azure AD) 中的身分識別提供者，您需要 toocreate QQ 應用程式和提供 hello 正確的參數。</span><span class="sxs-lookup"><span data-stu-id="74618-106">toouse QQ as an identity provider in Azure Active Directory (Azure AD) B2C, you need toocreate a QQ application and supply it with hello right parameters.</span></span> <span data-ttu-id="74618-107">您需要 QQ 帳戶 toodo 此。</span><span class="sxs-lookup"><span data-stu-id="74618-107">You need a QQ account toodo this.</span></span> <span data-ttu-id="74618-108">如果您沒有帳戶，您可以在 [https://ssl.zc.qq.com/en/index.html?type=1&ptlang=1033](https://ssl.zc.qq.com/en/index.html?type=1&ptlang=1033) 上取得一個。</span><span class="sxs-lookup"><span data-stu-id="74618-108">If you don’t have one, you can get one at [https://ssl.zc.qq.com/en/index.html?type=1&ptlang=1033](https://ssl.zc.qq.com/en/index.html?type=1&ptlang=1033).</span></span>

### <a name="register-for-hello-qq-developer-program"></a><span data-ttu-id="74618-109">註冊 hello QQ 開發人員計劃</span><span class="sxs-lookup"><span data-stu-id="74618-109">Register for hello QQ developer program</span></span>

1. <span data-ttu-id="74618-110">移 toohello [QQ 開發人員入口網站](http://open.qq.com)並以您 QQ 帳戶認證登入。</span><span class="sxs-lookup"><span data-stu-id="74618-110">Go toohello [QQ developer portal](http://open.qq.com) and sign in with your QQ account credentials.</span></span>
2. <span data-ttu-id="74618-111">登入之後，請移過[http://open.qq.com/reg](http://open.qq.com/reg) tooregister 自行身為開發人員。</span><span class="sxs-lookup"><span data-stu-id="74618-111">After signing in, go too[http://open.qq.com/reg](http://open.qq.com/reg) tooregister yourself as a developer.</span></span>
3. <span data-ttu-id="74618-112">在 [hello] 功能表中，選取 [**个人**（個別開發人員）。</span><span class="sxs-lookup"><span data-stu-id="74618-112">In hello menu, select **个人** (individual developer).</span></span>
4. <span data-ttu-id="74618-113">Hello 所需的資訊輸入 hello 表單，然後按一下**庫**（下一個步驟）。</span><span class="sxs-lookup"><span data-stu-id="74618-113">Enter hello required information into hello form and click **下一步** (next step).</span></span>
5. <span data-ttu-id="74618-114">完成 hello 電子郵件驗證程序。</span><span class="sxs-lookup"><span data-stu-id="74618-114">Complete hello email verification process.</span></span>

> [!NOTE]
> <span data-ttu-id="74618-115">您將需要核准身為開發人員註冊之後的幾天 toobe toowait。</span><span class="sxs-lookup"><span data-stu-id="74618-115">You will need toowait a few days toobe approved after registering as a developer.</span></span> 

### <a name="register-a-qq-application"></a><span data-ttu-id="74618-116">註冊 QQ 應用程式</span><span class="sxs-lookup"><span data-stu-id="74618-116">Register a QQ application</span></span>

1. <span data-ttu-id="74618-117">跳過[https://connect.qq.com/index.html](https://connect.qq.com/index.html)。</span><span class="sxs-lookup"><span data-stu-id="74618-117">Go too[https://connect.qq.com/index.html](https://connect.qq.com/index.html).</span></span>
2. <span data-ttu-id="74618-118">按一下 [应用管理] \(應用程式管理)。</span><span class="sxs-lookup"><span data-stu-id="74618-118">Click on **应用管理** (app management).</span></span>
3. <span data-ttu-id="74618-119">按一下 [创建应用] \(建立應用程式)。</span><span class="sxs-lookup"><span data-stu-id="74618-119">Click on **创建应用** (create app).</span></span>
4. <span data-ttu-id="74618-120">輸入 hello 必要的應用程式資訊。</span><span class="sxs-lookup"><span data-stu-id="74618-120">Enter hello necessary app information.</span></span>
5. <span data-ttu-id="74618-121">按一下 [创建应用] \(建立應用程式)。</span><span class="sxs-lookup"><span data-stu-id="74618-121">Click on **创建应用** (create app).</span></span>
6. <span data-ttu-id="74618-122">輸入 hello 所需的資訊。</span><span class="sxs-lookup"><span data-stu-id="74618-122">Enter hello required information.</span></span>
7. <span data-ttu-id="74618-123">Hello**授权回调域**(回呼 URL) 欄位中，輸入`https://login.microsoftonline.com/te/{tenant_name}/oauth2/authresp`。</span><span class="sxs-lookup"><span data-stu-id="74618-123">For hello **授权回调域** (callback URL) field, enter `https://login.microsoftonline.com/te/{tenant_name}/oauth2/authresp`.</span></span> <span data-ttu-id="74618-124">例如，如果您`tenant_name`是 contoso.onmicrosoft.com，集 hello URL toobe `https://login.microsoftonline.com/te/contoso.onmicrosoft.com/oauth2/authresp`。</span><span class="sxs-lookup"><span data-stu-id="74618-124">For example, if your `tenant_name` is contoso.onmicrosoft.com, set hello URL toobe `https://login.microsoftonline.com/te/contoso.onmicrosoft.com/oauth2/authresp`.</span></span>
8. <span data-ttu-id="74618-125">按一下 [创建应用] \(建立應用程式)。</span><span class="sxs-lookup"><span data-stu-id="74618-125">Click on **创建应用** (create app).</span></span>
9. <span data-ttu-id="74618-126">在 [hello] 確認頁面上，按一下**应用管理**（應用程式管理） tooreturn toohello 應用程式管理頁面。</span><span class="sxs-lookup"><span data-stu-id="74618-126">On hello confirmation page, click on **应用管理** (app management) tooreturn toohello app management page.</span></span>
10. <span data-ttu-id="74618-127">按一下**查看**您剛建立 （檢視） 下一步 toohello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="74618-127">Click on **查看** (view) next toohello app you just created.</span></span>
11. <span data-ttu-id="74618-128">按一下 [修改] \(編輯)。</span><span class="sxs-lookup"><span data-stu-id="74618-128">Click on **修改** (edit).</span></span>
12. <span data-ttu-id="74618-129">從 hello hello 頁面頂端，複製 [hello**應用程式識別碼**和**應用程式金鑰**。</span><span class="sxs-lookup"><span data-stu-id="74618-129">From hello top of hello page, copy hello **APP ID** and **APP KEY**.</span></span>

## <a name="configure-qq-as-an-identity-provider-in-your-tenant"></a><span data-ttu-id="74618-130">在租用戶中將 QQ 設為識別提供者</span><span class="sxs-lookup"><span data-stu-id="74618-130">Configure QQ as an identity provider in your tenant</span></span>
1. <span data-ttu-id="74618-131">請遵循下列步驟太[瀏覽 toohello B2C 功能刀鋒視窗](active-directory-b2c-app-registration.md#navigate-to-b2c-settings)hello Azure 入口網站上。</span><span class="sxs-lookup"><span data-stu-id="74618-131">Follow these steps too[navigate toohello B2C features blade](active-directory-b2c-app-registration.md#navigate-to-b2c-settings) on hello Azure portal.</span></span>
2. <span data-ttu-id="74618-132">在 [hello B2C 功能刀鋒視窗中，按一下 [**身分識別提供者**。</span><span class="sxs-lookup"><span data-stu-id="74618-132">On hello B2C features blade, click **Identity providers**.</span></span>
3. <span data-ttu-id="74618-133">按一下**+ 加**在 hello hello 刀鋒視窗最上方。</span><span class="sxs-lookup"><span data-stu-id="74618-133">Click **+Add** at hello top of hello blade.</span></span>
4. <span data-ttu-id="74618-134">提供方便**名稱**hello 身分識別提供者組態。</span><span class="sxs-lookup"><span data-stu-id="74618-134">Provide a friendly **Name** for hello identity provider configuration.</span></span> <span data-ttu-id="74618-135">例如，輸入 "QQ"。</span><span class="sxs-lookup"><span data-stu-id="74618-135">For example, enter "QQ".</span></span>
5. <span data-ttu-id="74618-136">按一下 [識別提供者類型]、選取 [QQ]，然後按一下 [確定]。</span><span class="sxs-lookup"><span data-stu-id="74618-136">Click **Identity provider type**, select **QQ**, and click **OK**.</span></span>
6. <span data-ttu-id="74618-137">按一下 [設定此識別提供者]。</span><span class="sxs-lookup"><span data-stu-id="74618-137">Click **Set up this identity provider**</span></span>
7. <span data-ttu-id="74618-138">輸入 hello**應用程式金鑰**您之前複製為 hello**用戶端識別碼**。</span><span class="sxs-lookup"><span data-stu-id="74618-138">Enter hello **App Key** that you copied earlier as hello **Client ID**.</span></span>
8. <span data-ttu-id="74618-139">輸入 hello**應用程式秘鑰**您之前複製為 hello**用戶端密碼**。</span><span class="sxs-lookup"><span data-stu-id="74618-139">Enter hello **App Secret** that you copied earlier as hello **Client Secret**.</span></span>
9. <span data-ttu-id="74618-140">按一下**確定**，然後按一下 [**建立**toosave QQ 組態。</span><span class="sxs-lookup"><span data-stu-id="74618-140">Click **OK** and then click **Create** toosave your QQ configuration.</span></span>

