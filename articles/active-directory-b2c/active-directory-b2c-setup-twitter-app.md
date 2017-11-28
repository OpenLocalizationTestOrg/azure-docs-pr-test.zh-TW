---
title: "Azure Active Directory B2C：Twitter 設定 | Microsoft Docs"
description: "提供註冊和登入 tooconsumers Twitter 帳戶，在受保護的 Azure Active Directory B2C 的應用程式中使用。"
services: active-directory-b2c
documentationcenter: 
author: parakhj
manager: krassk
editor: parakhj
ms.assetid: 579a6841-9329-45b8-a351-da4315a6634e
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 4/06/2017
ms.author: parakhj
ms.openlocfilehash: 275c5c73fd5e8e5075e77fee942cbc1b5e1586cf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2c-provide-sign-up-and-sign-in-tooconsumers-with-twitter-accounts"></a><span data-ttu-id="c0cc1-103">Azure Active Directory B2C： 提供與 Twitter 帳戶註冊和登入 tooconsumers</span><span class="sxs-lookup"><span data-stu-id="c0cc1-103">Azure Active Directory B2C: Provide sign-up and sign-in tooconsumers with Twitter accounts</span></span>

> [!NOTE]
> <span data-ttu-id="c0cc1-104">這項功能處於預覽狀態。</span><span class="sxs-lookup"><span data-stu-id="c0cc1-104">This feature is in preview.</span></span>
> 

## <a name="create-a-twitter-application"></a><span data-ttu-id="c0cc1-105">建立 Twitter 應用程式</span><span class="sxs-lookup"><span data-stu-id="c0cc1-105">Create a Twitter application</span></span>
<span data-ttu-id="c0cc1-106">toouse Twitter 身分識別提供者，在 Azure Active Directory (Azure AD) B2C 中，您需要 toocreate Twitter 應用程式，並提供與 hello 正確的參數。</span><span class="sxs-lookup"><span data-stu-id="c0cc1-106">toouse Twitter as an identity provider in Azure Active Directory (Azure AD) B2C, you need toocreate a Twitter application and supply it with hello right parameters.</span></span> <span data-ttu-id="c0cc1-107">您需要 Twitter 開發人員帳戶 toodo 此。</span><span class="sxs-lookup"><span data-stu-id="c0cc1-107">You need a Twitter developer account toodo this.</span></span> <span data-ttu-id="c0cc1-108">如果您沒有該帳戶，您可以在 [https://dev.twitter.com/](https://dev.twitter.com/) 上申請。</span><span class="sxs-lookup"><span data-stu-id="c0cc1-108">If you don’t have one, you can get it at [https://dev.twitter.com/](https://dev.twitter.com/).</span></span>

1. <span data-ttu-id="c0cc1-109">移 toohello [Twitter 開發人員網站](https://dev.twitter.com/)並以您的認證登入。</span><span class="sxs-lookup"><span data-stu-id="c0cc1-109">Go toohello [Twitter developer's website](https://dev.twitter.com/) and sign in with your credentials.</span></span>
2. <span data-ttu-id="c0cc1-110">按一下 工具和支援 底下的 我的應用程式，然後按一下建立新的應用程式。</span><span class="sxs-lookup"><span data-stu-id="c0cc1-110">Click **My apps** under **Tools & Support** and then click **Create New App**.</span></span> 
3. <span data-ttu-id="c0cc1-111">在 hello 表單中，提供值給 hello**名稱**，**描述**，和**網站**。</span><span class="sxs-lookup"><span data-stu-id="c0cc1-111">In hello form, provide a value for hello **Name**, **Description**, and **Website**.</span></span>
4. <span data-ttu-id="c0cc1-112">Hello**回呼 URL**，輸入`https://login.microsoftonline.com/te/{tenant}/oauth2/authresp`。</span><span class="sxs-lookup"><span data-stu-id="c0cc1-112">For hello **Callback URL**, enter `https://login.microsoftonline.com/te/{tenant}/oauth2/authresp`.</span></span> <span data-ttu-id="c0cc1-113">請確定 tooreplace **{tenant}**與您的租用戶名稱 (例如，contosob2c.onmicrosoft.com)。</span><span class="sxs-lookup"><span data-stu-id="c0cc1-113">Make sure tooreplace **{tenant}** with your tenant's name (for example, contosob2c.onmicrosoft.com).</span></span>
5. <span data-ttu-id="c0cc1-114">檢查 hello 方塊 tooagree toohello**開發人員合約**按一下**建立應用程式 Twitter**。</span><span class="sxs-lookup"><span data-stu-id="c0cc1-114">Check hello box tooagree toohello **Developer Agreement** and click **Create your Twitter application**.</span></span>
6. <span data-ttu-id="c0cc1-115">Hello 應用程式建立之後，按一下**機碼和存取權杖**。</span><span class="sxs-lookup"><span data-stu-id="c0cc1-115">Once hello app is created, click **Keys and Access Tokens**.</span></span>
7. <span data-ttu-id="c0cc1-116">複製 hello 值**取用者索引鍵**和**取用者秘密**。</span><span class="sxs-lookup"><span data-stu-id="c0cc1-116">Copy hello value of **Consumer Key** and **Consumer Secret**.</span></span> <span data-ttu-id="c0cc1-117">您將需要這兩種 tooconfigure Twitter 身分識別提供者，在您的租用戶。</span><span class="sxs-lookup"><span data-stu-id="c0cc1-117">You will need both of them tooconfigure Twitter as an identity provider in your tenant.</span></span>

## <a name="configure-twitter-as-an-identity-provider-in-your-tenant"></a><span data-ttu-id="c0cc1-118">在租用戶中將 Twitter 設為識別提供者</span><span class="sxs-lookup"><span data-stu-id="c0cc1-118">Configure Twitter as an identity provider in your tenant</span></span>
1. <span data-ttu-id="c0cc1-119">請遵循下列步驟太[瀏覽 toohello B2C 功能刀鋒視窗](active-directory-b2c-app-registration.md#navigate-to-b2c-settings)hello Azure 入口網站上。</span><span class="sxs-lookup"><span data-stu-id="c0cc1-119">Follow these steps too[navigate toohello B2C features blade](active-directory-b2c-app-registration.md#navigate-to-b2c-settings) on hello Azure portal.</span></span>
2. <span data-ttu-id="c0cc1-120">在 hello B2C 功能刀鋒視窗中，按一下 **身分識別提供者**。</span><span class="sxs-lookup"><span data-stu-id="c0cc1-120">On hello B2C features blade, click **Identity providers**.</span></span>
3. <span data-ttu-id="c0cc1-121">按一下**+ 加**在 hello hello 刀鋒視窗最上方。</span><span class="sxs-lookup"><span data-stu-id="c0cc1-121">Click **+Add** at hello top of hello blade.</span></span>
4. <span data-ttu-id="c0cc1-122">提供方便**名稱**hello 身分識別提供者組態。</span><span class="sxs-lookup"><span data-stu-id="c0cc1-122">Provide a friendly **Name** for hello identity provider configuration.</span></span> <span data-ttu-id="c0cc1-123">例如，輸入「Twitter」。</span><span class="sxs-lookup"><span data-stu-id="c0cc1-123">For example, enter "Twitter".</span></span>
5. <span data-ttu-id="c0cc1-124">按一下 [識別提供者類型]、選取 [Twitter]，然後按一下 [確定]。</span><span class="sxs-lookup"><span data-stu-id="c0cc1-124">Click **Identity provider type**, select **Twitter**, and click **OK**.</span></span>
6. <span data-ttu-id="c0cc1-125">按一下**設定此身分識別提供者**，然後輸入 hello Twitter**取用者索引鍵**hello**用戶端識別碼**和 hello Twitter**取用者秘密**hello**用戶端密碼**。</span><span class="sxs-lookup"><span data-stu-id="c0cc1-125">Click **Set up this identity provider** and enter hello Twitter **Consumer Key** for hello **Client id** and hello Twitter **Consumer Secret** for hello **Client secret**.</span></span>
7. <span data-ttu-id="c0cc1-126">按一下**確定**，然後按一下**建立**toosave Twitter 組態。</span><span class="sxs-lookup"><span data-stu-id="c0cc1-126">Click **OK**, and then click **Create** toosave your Twitter configuration.</span></span>

