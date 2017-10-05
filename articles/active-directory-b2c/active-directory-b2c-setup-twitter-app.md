---
title: "Azure Active Directory B2C：Twitter 設定 | Microsoft Docs"
description: "在受 Azure Active Directory B2C 保護的應用程式中，針對具有 Twitter 帳戶的取用者提供註冊和登入。"
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
ms.openlocfilehash: 82a001dd53cdddcf3b360090f3250af593c96fbb
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/18/2017
---
# <a name="azure-active-directory-b2c-provide-sign-up-and-sign-in-to-consumers-with-twitter-accounts"></a><span data-ttu-id="12393-103">Azure Active Directory B2C：針對具有 Twitter 帳戶的取用者提供註冊和登入</span><span class="sxs-lookup"><span data-stu-id="12393-103">Azure Active Directory B2C: Provide sign-up and sign-in to consumers with Twitter accounts</span></span>

> [!NOTE]
> <span data-ttu-id="12393-104">這項功能處於預覽狀態。</span><span class="sxs-lookup"><span data-stu-id="12393-104">This feature is in preview.</span></span>
> 

## <a name="create-a-twitter-application"></a><span data-ttu-id="12393-105">建立 Twitter 應用程式</span><span class="sxs-lookup"><span data-stu-id="12393-105">Create a Twitter application</span></span>
<span data-ttu-id="12393-106">若要在 Azure Active Directory (Azure AD) B2C 中使用 Twitter 作為識別提供者，您必須建立 Twitter 應用程式，並對其提供正確參數。</span><span class="sxs-lookup"><span data-stu-id="12393-106">To use Twitter as an identity provider in Azure Active Directory (Azure AD) B2C, you need to create a Twitter application and supply it with the right parameters.</span></span> <span data-ttu-id="12393-107">您需要 Twitter 開發人員帳戶才能執行這項操作。</span><span class="sxs-lookup"><span data-stu-id="12393-107">You need a Twitter developer account to do this.</span></span> <span data-ttu-id="12393-108">如果您沒有該帳戶，您可以在 [https://dev.twitter.com/](https://dev.twitter.com/) 上申請。</span><span class="sxs-lookup"><span data-stu-id="12393-108">If you don’t have one, you can get it at [https://dev.twitter.com/](https://dev.twitter.com/).</span></span>

1. <span data-ttu-id="12393-109">移至 [Twitter 開發人員網站](https://dev.twitter.com/)，並以您的認證登入。</span><span class="sxs-lookup"><span data-stu-id="12393-109">Go to the [Twitter developer's website](https://dev.twitter.com/) and sign in with your credentials.</span></span>
2. <span data-ttu-id="12393-110">按一下 [工具和支援] 底下的 [我的應用程式]，然後按一下 [建立新的應用程式]。</span><span class="sxs-lookup"><span data-stu-id="12393-110">Click **My apps** under **Tools & Support** and then click **Create New App**.</span></span> 
3. <span data-ttu-id="12393-111">在表單中，提供**名稱**、**描述**和**網站**值。</span><span class="sxs-lookup"><span data-stu-id="12393-111">In the form, provide a value for the **Name**, **Description**, and **Website**.</span></span>
4. <span data-ttu-id="12393-112">在 [回呼 URL] 中輸入 `https://login.microsoftonline.com/te/{tenant}/oauth2/authresp`。</span><span class="sxs-lookup"><span data-stu-id="12393-112">For the **Callback URL**, enter `https://login.microsoftonline.com/te/{tenant}/oauth2/authresp`.</span></span> <span data-ttu-id="12393-113">務必要使用您的租用戶名稱 (例如 contosob2c.onmicrosoft.com) 來取代 **{tenant}**。</span><span class="sxs-lookup"><span data-stu-id="12393-113">Make sure to replace **{tenant}** with your tenant's name (for example, contosob2c.onmicrosoft.com).</span></span>
5. <span data-ttu-id="12393-114">勾選方塊以同意 [開發人員合約]，然後按一下 [建立 Twitter 應用程式]。</span><span class="sxs-lookup"><span data-stu-id="12393-114">Check the box to agree to the **Developer Agreement** and click **Create your Twitter application**.</span></span>
6. <span data-ttu-id="12393-115">應用程式建立完成後，按一下 [金鑰和存取權杖]。</span><span class="sxs-lookup"><span data-stu-id="12393-115">Once the app is created, click **Keys and Access Tokens**.</span></span>
7. <span data-ttu-id="12393-116">複製 [取用者金鑰] 和 [取用者祕密] 的值。</span><span class="sxs-lookup"><span data-stu-id="12393-116">Copy the value of **Consumer Key** and **Consumer Secret**.</span></span> <span data-ttu-id="12393-117">您必須使用這兩個值，將 Twitter 設為租用戶中的身分識別提供者。</span><span class="sxs-lookup"><span data-stu-id="12393-117">You will need both of them to configure Twitter as an identity provider in your tenant.</span></span>

## <a name="configure-twitter-as-an-identity-provider-in-your-tenant"></a><span data-ttu-id="12393-118">在租用戶中將 Twitter 設為識別提供者</span><span class="sxs-lookup"><span data-stu-id="12393-118">Configure Twitter as an identity provider in your tenant</span></span>
1. <span data-ttu-id="12393-119">遵循下列步驟以 [瀏覽至 B2C 功能刀鋒視窗](active-directory-b2c-app-registration.md#navigate-to-b2c-settings) (位於 Azure 入口網站上)。</span><span class="sxs-lookup"><span data-stu-id="12393-119">Follow these steps to [navigate to the B2C features blade](active-directory-b2c-app-registration.md#navigate-to-b2c-settings) on the Azure portal.</span></span>
2. <span data-ttu-id="12393-120">在 B2C 功能刀鋒視窗中，按一下 [ **身分識別提供者**]。</span><span class="sxs-lookup"><span data-stu-id="12393-120">On the B2C features blade, click **Identity providers**.</span></span>
3. <span data-ttu-id="12393-121">按一下刀鋒視窗頂端的 [新增]  。</span><span class="sxs-lookup"><span data-stu-id="12393-121">Click **+Add** at the top of the blade.</span></span>
4. <span data-ttu-id="12393-122">針對身分識別提供者組態，提供容易辨識的 **名稱** 。</span><span class="sxs-lookup"><span data-stu-id="12393-122">Provide a friendly **Name** for the identity provider configuration.</span></span> <span data-ttu-id="12393-123">例如，輸入「Twitter」。</span><span class="sxs-lookup"><span data-stu-id="12393-123">For example, enter "Twitter".</span></span>
5. <span data-ttu-id="12393-124">按一下 [識別提供者類型]、選取 [Twitter]，然後按一下 [確定]。</span><span class="sxs-lookup"><span data-stu-id="12393-124">Click **Identity provider type**, select **Twitter**, and click **OK**.</span></span>
6. <span data-ttu-id="12393-125">按一下 [設定此識別提供者]，然後輸入 Twitter 的**取用者金鑰**來作為**用戶端識別碼**，以及輸入 Twitter 的**取用者祕密**來作為**用戶端祕密**。</span><span class="sxs-lookup"><span data-stu-id="12393-125">Click **Set up this identity provider** and enter the Twitter **Consumer Key** for the **Client id** and the Twitter **Consumer Secret** for the **Client secret**.</span></span>
7. <span data-ttu-id="12393-126">依序按一下 [確定] 和 [建立]，儲存您的 Twitter 設定。</span><span class="sxs-lookup"><span data-stu-id="12393-126">Click **OK**, and then click **Create** to save your Twitter configuration.</span></span>

