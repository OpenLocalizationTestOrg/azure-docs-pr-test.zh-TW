---
title: "新增 Azure Active Directory B2B 共同作業使用者到角色 | Microsoft Docs"
description: "將來賓使用者新增至 Azure Active Directory 中的角色"
services: active-directory
documentationcenter: 
author: sasubram
manager: femila
editor: 
tags: 
ms.assetid: 
ms.service: active-directory
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: identity
ms.date: 03/15/2017
ms.author: sasubram
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: e816349ea971c997f655b4d51672dba666bc3e89
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="grant-permissions-to-users-from-partner-organizations-in-your-azure-active-directory-tenant"></a><span data-ttu-id="841c4-103">從 Azure Active Directory 租用戶中的合作夥伴組織授與權限給使用者</span><span class="sxs-lookup"><span data-stu-id="841c4-103">Grant permissions to users from partner organizations in your Azure Active Directory tenant</span></span>

<span data-ttu-id="841c4-104">Azure Active Directory (Azure AD) B2B 共同作業使用者是以來賓使用者身分新增到目錄中，且目錄中的來賓權限預設是有所限制的。</span><span class="sxs-lookup"><span data-stu-id="841c4-104">Azure Active Directory (Azure AD) B2B collaboration users are added as guest users to the directory, and guest permissions in the directory are restricted by default.</span></span> <span data-ttu-id="841c4-105">您的公司可能需要某些來賓使用者擁有您組織中的更高權限的角色。</span><span class="sxs-lookup"><span data-stu-id="841c4-105">Your business may need some guest users to fill higher-privilege roles in your organization.</span></span> <span data-ttu-id="841c4-106">為支援定義更高權限的角色，您可以根據您組織的需求將來賓使用者新增到您想要的任何角色。</span><span class="sxs-lookup"><span data-stu-id="841c4-106">To support defining higher-privilege roles, guest users can be added to any roles you desire, based on your organization's needs.</span></span>

## <a name="default-role"></a><span data-ttu-id="841c4-107">預設角色</span><span class="sxs-lookup"><span data-stu-id="841c4-107">Default role</span></span>

![預設角色](./media/active-directory-b2b-add-guest-to-role/default-role.png)

## <a name="global-administrator-role"></a><span data-ttu-id="841c4-109">全域系統管理員角色</span><span class="sxs-lookup"><span data-stu-id="841c4-109">Global Administrator Role</span></span>

![全域系統管理員角色](./media/active-directory-b2b-add-guest-to-role/global-admin-role.png)

## <a name="limited-administrator-role"></a><span data-ttu-id="841c4-111">受限的系統管理員角色</span><span class="sxs-lookup"><span data-stu-id="841c4-111">Limited Administrator Role</span></span>

![受限的系統管理員角色](./media/active-directory-b2b-add-guest-to-role/limited-admin-role.png)

## <a name="next-steps"></a><span data-ttu-id="841c4-113">後續步驟</span><span class="sxs-lookup"><span data-stu-id="841c4-113">Next steps</span></span>

<span data-ttu-id="841c4-114">請瀏覽有關 Azure AD B2B 共同作業的其他文章：</span><span class="sxs-lookup"><span data-stu-id="841c4-114">Browse our other articles on Azure AD B2B collaboration:</span></span>

* [<span data-ttu-id="841c4-115">何謂 Azure AD B2B 共同作業？</span><span class="sxs-lookup"><span data-stu-id="841c4-115">What is Azure AD B2B collaboration?</span></span>](active-directory-b2b-what-is-azure-ad-b2b.md)
* [<span data-ttu-id="841c4-116">B2B 共同作業使用者屬性</span><span class="sxs-lookup"><span data-stu-id="841c4-116">B2B collaboration user properties</span></span>](active-directory-b2b-user-properties.md)
* [<span data-ttu-id="841c4-117">委派 B2B 共同作業邀請</span><span class="sxs-lookup"><span data-stu-id="841c4-117">Delegate B2bB collaboration invitations</span></span>](active-directory-b2b-delegate-invitations.md)
* [<span data-ttu-id="841c4-118">動態群組與 B2B 共同作業</span><span class="sxs-lookup"><span data-stu-id="841c4-118">Dynamic groups and B2B collaboration</span></span>](active-directory-b2b-dynamic-groups.md)
* [<span data-ttu-id="841c4-119">B2B 共同作業程式碼與 PowerShell 範例</span><span class="sxs-lookup"><span data-stu-id="841c4-119">B2B collaboration code and PowerShell samples</span></span>](active-directory-b2b-code-samples.md)
* [<span data-ttu-id="841c4-120">設定適用於 B2B 共同作業的 SaaS 應用程式</span><span class="sxs-lookup"><span data-stu-id="841c4-120">Configure SaaS apps for B2B collaboration</span></span>](active-directory-b2b-configure-saas-apps.md)
* [<span data-ttu-id="841c4-121">B2B 共同作業使用者權杖</span><span class="sxs-lookup"><span data-stu-id="841c4-121">B2B collaboration user tokens</span></span>](active-directory-b2b-user-token.md)
* [<span data-ttu-id="841c4-122">B2B 共同作業使用者宣告對應</span><span class="sxs-lookup"><span data-stu-id="841c4-122">B2B collaboration user claims mapping</span></span>](active-directory-b2b-claims-mapping.md)
* [<span data-ttu-id="841c4-123">Office 365 外部共用</span><span class="sxs-lookup"><span data-stu-id="841c4-123">Office 365 external sharing</span></span>](active-directory-b2b-o365-external-user.md)
* [<span data-ttu-id="841c4-124">B2B 共同作業目前的限制</span><span class="sxs-lookup"><span data-stu-id="841c4-124">B2B collaboration current limitations</span></span>](active-directory-b2b-current-limitations.md)
