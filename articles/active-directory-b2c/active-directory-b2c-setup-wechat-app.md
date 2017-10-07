---
title: "Azure Active Directory B2C：WeChat 設定 | Microsoft Docs"
description: "提供註冊和登入 tooconsumers WeChat 帳戶，在受保護的 Azure Active Directory B2C 的應用程式中使用。"
services: active-directory-b2c
documentationcenter: 
author: parakhj
manager: krassk
editor: parakhj
ms.assetid: d2424c66-ba68-4d82-847e-d137683527b0
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 3/26/2017
ms.author: parakhj
ms.openlocfilehash: 92cc3579d818d2379a503ccc695138b33a34466d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2c-provide-sign-up-and-sign-in-tooconsumers-with-wechat-accounts"></a><span data-ttu-id="0c71c-103">Azure Active Directory B2C： 註冊和登入 tooconsumers 提供 WeChat 帳戶</span><span class="sxs-lookup"><span data-stu-id="0c71c-103">Azure Active Directory B2C: Provide sign-up and sign-in tooconsumers with WeChat accounts</span></span>

> [!NOTE]
> <span data-ttu-id="0c71c-104">這項功能處於預覽狀態。</span><span class="sxs-lookup"><span data-stu-id="0c71c-104">This feature is in preview.</span></span>
> 

## <a name="create-a-wechat-application"></a><span data-ttu-id="0c71c-105">建立 WeChat 應用程式</span><span class="sxs-lookup"><span data-stu-id="0c71c-105">Create a WeChat application</span></span>

<span data-ttu-id="0c71c-106">toouse WeChat B2C Azure Active Directory (Azure AD) 中的身分識別提供者，您需要 toocreate WeChat 應用程式和提供 hello 正確的參數。</span><span class="sxs-lookup"><span data-stu-id="0c71c-106">toouse WeChat as an identity provider in Azure Active Directory (Azure AD) B2C, you need toocreate a WeChat application and supply it with hello right parameters.</span></span> <span data-ttu-id="0c71c-107">您需要 WeChat 帳戶 toodo 此。</span><span class="sxs-lookup"><span data-stu-id="0c71c-107">You need a WeChat account toodo this.</span></span> <span data-ttu-id="0c71c-108">如果您沒有帳戶，您可以透過它們的其中一個行動裝置應用程式來註冊，或使用您的 QQ 號碼，藉以取得一個帳戶。</span><span class="sxs-lookup"><span data-stu-id="0c71c-108">If you don’t have one, you can get one by signing up through one of their mobile apps or by using your QQ number.</span></span> <span data-ttu-id="0c71c-109">在這之後，取得您的帳戶向 hello WeChat 開發人員計劃。</span><span class="sxs-lookup"><span data-stu-id="0c71c-109">After that, get your account registered with hello WeChat developer program.</span></span> <span data-ttu-id="0c71c-110">您可以在 [這裡](http://kf.qq.com/faq/161220Brem2Q161220uUjERB.html)找到詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="0c71c-110">You can find more information [here](http://kf.qq.com/faq/161220Brem2Q161220uUjERB.html).</span></span>

### <a name="register-a-wechat-application"></a><span data-ttu-id="0c71c-111">註冊 WeChat 應用程式</span><span class="sxs-lookup"><span data-stu-id="0c71c-111">Register a WeChat application</span></span>

1. <span data-ttu-id="0c71c-112">跳過[https://open.weixin.qq.com/](https://open.weixin.qq.com/)並登入。</span><span class="sxs-lookup"><span data-stu-id="0c71c-112">Go too[https://open.weixin.qq.com/](https://open.weixin.qq.com/) and log in.</span></span>
2. <span data-ttu-id="0c71c-113">按一下 [管理中心]。</span><span class="sxs-lookup"><span data-stu-id="0c71c-113">Click on **管理中心** (management center).</span></span>
3. <span data-ttu-id="0c71c-114">請遵循 hello 必要步驟 tooregister 新的應用程式。</span><span class="sxs-lookup"><span data-stu-id="0c71c-114">Follow hello necessary steps tooregister a new application.</span></span>
4. <span data-ttu-id="0c71c-115">針對 [授权回调域] \(回呼 URL)，輸入 `https://login.microsoftonline.com/te/{tenant_name}/oauth2/authresp`。</span><span class="sxs-lookup"><span data-stu-id="0c71c-115">For **授权回调域** (callback URL), enter `https://login.microsoftonline.com/te/{tenant_name}/oauth2/authresp`.</span></span> <span data-ttu-id="0c71c-116">例如，如果您`tenant_name`是 contoso.onmicrosoft.com，集 hello URL toobe `https://login.microsoftonline.com/te/contoso.onmicrosoft.com/oauth2/authresp`。</span><span class="sxs-lookup"><span data-stu-id="0c71c-116">For example, if your `tenant_name` is contoso.onmicrosoft.com, set hello URL toobe `https://login.microsoftonline.com/te/contoso.onmicrosoft.com/oauth2/authresp`.</span></span>
5. <span data-ttu-id="0c71c-117">尋找並複製 hello**應用程式識別碼**和**應用程式金鑰**。</span><span class="sxs-lookup"><span data-stu-id="0c71c-117">Find and copy hello **APP ID** and **APP KEY**.</span></span> <span data-ttu-id="0c71c-118">稍後您將需要這些資訊。</span><span class="sxs-lookup"><span data-stu-id="0c71c-118">You will need these later.</span></span>

## <a name="configure-wechat-as-an-identity-provider-in-your-tenant"></a><span data-ttu-id="0c71c-119">在租用戶中將 WeChat 設為識別提供者</span><span class="sxs-lookup"><span data-stu-id="0c71c-119">Configure WeChat as an identity provider in your tenant</span></span>
1. <span data-ttu-id="0c71c-120">請遵循下列步驟太[瀏覽 toohello B2C 功能刀鋒視窗](active-directory-b2c-app-registration.md#navigate-to-b2c-settings)hello Azure 入口網站上。</span><span class="sxs-lookup"><span data-stu-id="0c71c-120">Follow these steps too[navigate toohello B2C features blade](active-directory-b2c-app-registration.md#navigate-to-b2c-settings) on hello Azure portal.</span></span>
2. <span data-ttu-id="0c71c-121">在 hello B2C 功能刀鋒視窗中，按一下 **身分識別提供者**。</span><span class="sxs-lookup"><span data-stu-id="0c71c-121">On hello B2C features blade, click **Identity providers**.</span></span>
3. <span data-ttu-id="0c71c-122">按一下**+ 加**在 hello hello 刀鋒視窗最上方。</span><span class="sxs-lookup"><span data-stu-id="0c71c-122">Click **+Add** at hello top of hello blade.</span></span>
4. <span data-ttu-id="0c71c-123">提供方便**名稱**hello 身分識別提供者組態。</span><span class="sxs-lookup"><span data-stu-id="0c71c-123">Provide a friendly **Name** for hello identity provider configuration.</span></span> <span data-ttu-id="0c71c-124">例如，輸入 "WeChat"。</span><span class="sxs-lookup"><span data-stu-id="0c71c-124">For example, enter "WeChat".</span></span>
5. <span data-ttu-id="0c71c-125">按一下 [識別提供者類型]、選取 [WeChat]，然後按一下 [確定]。</span><span class="sxs-lookup"><span data-stu-id="0c71c-125">Click **Identity provider type**, select **WeChat**, and click **OK**.</span></span>
6. <span data-ttu-id="0c71c-126">按一下 [設定此識別提供者]。</span><span class="sxs-lookup"><span data-stu-id="0c71c-126">Click **Set up this identity provider**</span></span>
7. <span data-ttu-id="0c71c-127">輸入 hello**應用程式金鑰**您之前複製為 hello**用戶端識別碼**。</span><span class="sxs-lookup"><span data-stu-id="0c71c-127">Enter hello **App Key** that you copied earlier as hello **Client ID**.</span></span>
8. <span data-ttu-id="0c71c-128">輸入 hello**應用程式秘鑰**您之前複製為 hello**用戶端密碼**。</span><span class="sxs-lookup"><span data-stu-id="0c71c-128">Enter hello **App Secret** that you copied earlier as hello **Client Secret**.</span></span>
9. <span data-ttu-id="0c71c-129">按一下**確定**，然後按一下**建立**toosave WeChat 組態。</span><span class="sxs-lookup"><span data-stu-id="0c71c-129">Click **OK** and then click **Create** toosave your WeChat configuration.</span></span>

