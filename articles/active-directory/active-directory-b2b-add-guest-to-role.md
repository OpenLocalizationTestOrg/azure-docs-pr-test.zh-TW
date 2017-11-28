---
title: "aaaAdd Azure Active Directory B2B 共同作業使用者 tooa 角色 |Microsoft 文件"
description: "Azure Active Directory 中新增來賓使用者 tooa 角色"
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
ms.openlocfilehash: ccc58a0c8ecc73f8e79a8d827efdc0ff93846a96
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="grant-permissions-toousers-from-partner-organizations-in-your-azure-active-directory-tenant"></a><span data-ttu-id="b46b7-103">從夥伴組織中建立您的 Azure Active Directory 租用戶中授與權限 toousers</span><span class="sxs-lookup"><span data-stu-id="b46b7-103">Grant permissions toousers from partner organizations in your Azure Active Directory tenant</span></span>

<span data-ttu-id="b46b7-104">Azure Active Directory (Azure AD) B2B 共同作業的使用者會新增為來賓使用者 toohello 目錄，並依預設會限制 hello 目錄中的 guest 權限。</span><span class="sxs-lookup"><span data-stu-id="b46b7-104">Azure Active Directory (Azure AD) B2B collaboration users are added as guest users toohello directory, and guest permissions in hello directory are restricted by default.</span></span> <span data-ttu-id="b46b7-105">您的企業，可能需要您組織中的有些來賓使用者 toofill 高特殊權限角色。</span><span class="sxs-lookup"><span data-stu-id="b46b7-105">Your business may need some guest users toofill higher-privilege roles in your organization.</span></span> <span data-ttu-id="b46b7-106">定義高特殊權限角色 toosupport guest 使用者可以根據組織的需求，依您想要加入的 tooany 角色。</span><span class="sxs-lookup"><span data-stu-id="b46b7-106">toosupport defining higher-privilege roles, guest users can be added tooany roles you desire, based on your organization's needs.</span></span>

## <a name="default-role"></a><span data-ttu-id="b46b7-107">預設角色</span><span class="sxs-lookup"><span data-stu-id="b46b7-107">Default role</span></span>

![預設角色](./media/active-directory-b2b-add-guest-to-role/default-role.png)

## <a name="global-administrator-role"></a><span data-ttu-id="b46b7-109">全域系統管理員角色</span><span class="sxs-lookup"><span data-stu-id="b46b7-109">Global Administrator Role</span></span>

![全域系統管理員角色](./media/active-directory-b2b-add-guest-to-role/global-admin-role.png)

## <a name="limited-administrator-role"></a><span data-ttu-id="b46b7-111">受限的系統管理員角色</span><span class="sxs-lookup"><span data-stu-id="b46b7-111">Limited Administrator Role</span></span>

![受限的系統管理員角色](./media/active-directory-b2b-add-guest-to-role/limited-admin-role.png)

## <a name="next-steps"></a><span data-ttu-id="b46b7-113">後續步驟</span><span class="sxs-lookup"><span data-stu-id="b46b7-113">Next steps</span></span>

<span data-ttu-id="b46b7-114">請瀏覽有關 Azure AD B2B 共同作業的其他文章：</span><span class="sxs-lookup"><span data-stu-id="b46b7-114">Browse our other articles on Azure AD B2B collaboration:</span></span>

* [<span data-ttu-id="b46b7-115">何謂 Azure AD B2B 共同作業？</span><span class="sxs-lookup"><span data-stu-id="b46b7-115">What is Azure AD B2B collaboration?</span></span>](active-directory-b2b-what-is-azure-ad-b2b.md)
* [<span data-ttu-id="b46b7-116">B2B 共同作業使用者屬性</span><span class="sxs-lookup"><span data-stu-id="b46b7-116">B2B collaboration user properties</span></span>](active-directory-b2b-user-properties.md)
* [<span data-ttu-id="b46b7-117">委派 B2B 共同作業邀請</span><span class="sxs-lookup"><span data-stu-id="b46b7-117">Delegate B2bB collaboration invitations</span></span>](active-directory-b2b-delegate-invitations.md)
* [<span data-ttu-id="b46b7-118">動態群組與 B2B 共同作業</span><span class="sxs-lookup"><span data-stu-id="b46b7-118">Dynamic groups and B2B collaboration</span></span>](active-directory-b2b-dynamic-groups.md)
* [<span data-ttu-id="b46b7-119">B2B 共同作業程式碼與 PowerShell 範例</span><span class="sxs-lookup"><span data-stu-id="b46b7-119">B2B collaboration code and PowerShell samples</span></span>](active-directory-b2b-code-samples.md)
* [<span data-ttu-id="b46b7-120">設定適用於 B2B 共同作業的 SaaS 應用程式</span><span class="sxs-lookup"><span data-stu-id="b46b7-120">Configure SaaS apps for B2B collaboration</span></span>](active-directory-b2b-configure-saas-apps.md)
* [<span data-ttu-id="b46b7-121">B2B 共同作業使用者權杖</span><span class="sxs-lookup"><span data-stu-id="b46b7-121">B2B collaboration user tokens</span></span>](active-directory-b2b-user-token.md)
* [<span data-ttu-id="b46b7-122">B2B 共同作業使用者宣告對應</span><span class="sxs-lookup"><span data-stu-id="b46b7-122">B2B collaboration user claims mapping</span></span>](active-directory-b2b-claims-mapping.md)
* [<span data-ttu-id="b46b7-123">Office 365 外部共用</span><span class="sxs-lookup"><span data-stu-id="b46b7-123">Office 365 external sharing</span></span>](active-directory-b2b-o365-external-user.md)
* [<span data-ttu-id="b46b7-124">B2B 共同作業目前的限制</span><span class="sxs-lookup"><span data-stu-id="b46b7-124">B2B collaboration current limitations</span></span>](active-directory-b2b-current-limitations.md)
