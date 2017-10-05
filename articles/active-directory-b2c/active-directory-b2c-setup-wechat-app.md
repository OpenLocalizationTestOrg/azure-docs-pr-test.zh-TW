---
title: "Azure Active Directory B2C：WeChat 設定 | Microsoft Docs"
description: "在受 Azure Active Directory B2C 保護的應用程式中，針對具有 WeChat 帳戶的取用者提供註冊和登入。"
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
ms.openlocfilehash: a54aec23d951610118246e9f70cdd27752ef39a6
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/18/2017
---
# <a name="azure-active-directory-b2c-provide-sign-up-and-sign-in-to-consumers-with-wechat-accounts"></a><span data-ttu-id="38f06-103">Azure Active Directory B2C：針對具有 WeChat 帳戶的取用者提供註冊和登入</span><span class="sxs-lookup"><span data-stu-id="38f06-103">Azure Active Directory B2C: Provide sign-up and sign-in to consumers with WeChat accounts</span></span>

> [!NOTE]
> <span data-ttu-id="38f06-104">這項功能處於預覽狀態。</span><span class="sxs-lookup"><span data-stu-id="38f06-104">This feature is in preview.</span></span>
> 

## <a name="create-a-wechat-application"></a><span data-ttu-id="38f06-105">建立 WeChat 應用程式</span><span class="sxs-lookup"><span data-stu-id="38f06-105">Create a WeChat application</span></span>

<span data-ttu-id="38f06-106">若要在 Azure Active Directory (Azure AD) B2C 中使用 WeChat 做為識別提供者，您必須建立 WeChat 應用程式，並對其提供正確參數。</span><span class="sxs-lookup"><span data-stu-id="38f06-106">To use WeChat as an identity provider in Azure Active Directory (Azure AD) B2C, you need to create a WeChat application and supply it with the right parameters.</span></span> <span data-ttu-id="38f06-107">您需要 WeChat 帳戶才能執行此動作。</span><span class="sxs-lookup"><span data-stu-id="38f06-107">You need a WeChat account to do this.</span></span> <span data-ttu-id="38f06-108">如果您沒有帳戶，您可以透過它們的其中一個行動裝置應用程式來註冊，或使用您的 QQ 號碼，藉以取得一個帳戶。</span><span class="sxs-lookup"><span data-stu-id="38f06-108">If you don’t have one, you can get one by signing up through one of their mobile apps or by using your QQ number.</span></span> <span data-ttu-id="38f06-109">之後，請利用 WeChat 開發人員計劃註冊您的帳戶。</span><span class="sxs-lookup"><span data-stu-id="38f06-109">After that, get your account registered with the WeChat developer program.</span></span> <span data-ttu-id="38f06-110">您可以在 [這裡](http://kf.qq.com/faq/161220Brem2Q161220uUjERB.html)找到詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="38f06-110">You can find more information [here](http://kf.qq.com/faq/161220Brem2Q161220uUjERB.html).</span></span>

### <a name="register-a-wechat-application"></a><span data-ttu-id="38f06-111">註冊 WeChat 應用程式</span><span class="sxs-lookup"><span data-stu-id="38f06-111">Register a WeChat application</span></span>

1. <span data-ttu-id="38f06-112">移至 [https://open.weixin.qq.com/](https://open.weixin.qq.com/) 並登入。</span><span class="sxs-lookup"><span data-stu-id="38f06-112">Go to [https://open.weixin.qq.com/](https://open.weixin.qq.com/) and log in.</span></span>
2. <span data-ttu-id="38f06-113">按一下 [管理中心]。</span><span class="sxs-lookup"><span data-stu-id="38f06-113">Click on **管理中心** (management center).</span></span>
3. <span data-ttu-id="38f06-114">遵循註冊新應用程式的必要步驟。</span><span class="sxs-lookup"><span data-stu-id="38f06-114">Follow the necessary steps to register a new application.</span></span>
4. <span data-ttu-id="38f06-115">針對 [授权回调域] \(回呼 URL)，輸入 `https://login.microsoftonline.com/te/{tenant_name}/oauth2/authresp`。</span><span class="sxs-lookup"><span data-stu-id="38f06-115">For **授权回调域** (callback URL), enter `https://login.microsoftonline.com/te/{tenant_name}/oauth2/authresp`.</span></span> <span data-ttu-id="38f06-116">例如，如果您的 `tenant_name` 是 contoso.onmicrosoft.com，請將 URL 設為 `https://login.microsoftonline.com/te/contoso.onmicrosoft.com/oauth2/authresp`。</span><span class="sxs-lookup"><span data-stu-id="38f06-116">For example, if your `tenant_name` is contoso.onmicrosoft.com, set the URL to be `https://login.microsoftonline.com/te/contoso.onmicrosoft.com/oauth2/authresp`.</span></span>
5. <span data-ttu-id="38f06-117">尋找並複製**應用程式識別碼**和**應用程式金鑰**。</span><span class="sxs-lookup"><span data-stu-id="38f06-117">Find and copy the **APP ID** and **APP KEY**.</span></span> <span data-ttu-id="38f06-118">稍後您將需要這些資訊。</span><span class="sxs-lookup"><span data-stu-id="38f06-118">You will need these later.</span></span>

## <a name="configure-wechat-as-an-identity-provider-in-your-tenant"></a><span data-ttu-id="38f06-119">在租用戶中將 WeChat 設為識別提供者</span><span class="sxs-lookup"><span data-stu-id="38f06-119">Configure WeChat as an identity provider in your tenant</span></span>
1. <span data-ttu-id="38f06-120">遵循下列步驟以 [瀏覽至 B2C 功能刀鋒視窗](active-directory-b2c-app-registration.md#navigate-to-b2c-settings) (位於 Azure 入口網站上)。</span><span class="sxs-lookup"><span data-stu-id="38f06-120">Follow these steps to [navigate to the B2C features blade](active-directory-b2c-app-registration.md#navigate-to-b2c-settings) on the Azure portal.</span></span>
2. <span data-ttu-id="38f06-121">在 B2C 功能刀鋒視窗中，按一下 [ **身分識別提供者**]。</span><span class="sxs-lookup"><span data-stu-id="38f06-121">On the B2C features blade, click **Identity providers**.</span></span>
3. <span data-ttu-id="38f06-122">按一下刀鋒視窗頂端的 [新增]  。</span><span class="sxs-lookup"><span data-stu-id="38f06-122">Click **+Add** at the top of the blade.</span></span>
4. <span data-ttu-id="38f06-123">針對身分識別提供者組態，提供容易辨識的 **名稱** 。</span><span class="sxs-lookup"><span data-stu-id="38f06-123">Provide a friendly **Name** for the identity provider configuration.</span></span> <span data-ttu-id="38f06-124">例如，輸入 "WeChat"。</span><span class="sxs-lookup"><span data-stu-id="38f06-124">For example, enter "WeChat".</span></span>
5. <span data-ttu-id="38f06-125">按一下 [識別提供者類型]、選取 [WeChat]，然後按一下 [確定]。</span><span class="sxs-lookup"><span data-stu-id="38f06-125">Click **Identity provider type**, select **WeChat**, and click **OK**.</span></span>
6. <span data-ttu-id="38f06-126">按一下 [設定此識別提供者]。</span><span class="sxs-lookup"><span data-stu-id="38f06-126">Click **Set up this identity provider**</span></span>
7. <span data-ttu-id="38f06-127">輸入您稍早複製為**用戶端識別碼**的**應用程式金鑰**。</span><span class="sxs-lookup"><span data-stu-id="38f06-127">Enter the **App Key** that you copied earlier as the **Client ID**.</span></span>
8. <span data-ttu-id="38f06-128">輸入您稍早複製為**用戶端密碼**的**應用程式密碼**。</span><span class="sxs-lookup"><span data-stu-id="38f06-128">Enter the **App Secret** that you copied earlier as the **Client Secret**.</span></span>
9. <span data-ttu-id="38f06-129">依序按一下 [確定] 和 [建立]，儲存您的 WeChat 設定。</span><span class="sxs-lookup"><span data-stu-id="38f06-129">Click **OK** and then click **Create** to save your WeChat configuration.</span></span>

