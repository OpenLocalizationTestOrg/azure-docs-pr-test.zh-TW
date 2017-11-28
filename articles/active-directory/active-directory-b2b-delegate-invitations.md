---
title: "Azure Active Directory B2B 共同作業的 aaaDelegate 邀請 |Microsoft 文件"
description: "Azure Active Directory B2B 共同作業的使用者屬性可進行設定"
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
ms.date: 05/23/2017
ms.author: sasubram
ms.openlocfilehash: c0122d6f60d494c6e251c41d947dc254ea887620
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="delegate-invitations-for-azure-active-directory-b2b-collaboration"></a><span data-ttu-id="d8cf0-103">委派 Azure Active Directory B2B 共同作業邀請</span><span class="sxs-lookup"><span data-stu-id="d8cf0-103">Delegate invitations for Azure Active Directory B2B collaboration</span></span>

<span data-ttu-id="d8cf0-104">Azure Active Directory (Azure AD) 企業對企業 (B2B) 共同作業，您沒有 toobe 全域管理員 toosend 邀請。</span><span class="sxs-lookup"><span data-stu-id="d8cf0-104">With Azure Active Directory (Azure AD) business-to-business (B2B) collaboration, you do not have toobe a global admin toosend invitations.</span></span> <span data-ttu-id="d8cf0-105">相反地，您可以使用原則，以及委派邀請 toousers 其角色，可讓它們 toosend 邀請。</span><span class="sxs-lookup"><span data-stu-id="d8cf0-105">Instead, you can use policies and delegate invitations toousers whose roles allow them toosend invitations.</span></span> <span data-ttu-id="d8cf0-106">重要新方式 toodelegate 來賓使用者邀請是透過 hello 來賓邀請者角色。</span><span class="sxs-lookup"><span data-stu-id="d8cf0-106">An important new way toodelegate guest user invitations is through hello Guest Inviter role.</span></span>

## <a name="guest-inviter-role"></a><span data-ttu-id="d8cf0-107">來賓邀請者角色</span><span class="sxs-lookup"><span data-stu-id="d8cf0-107">Guest Inviter role</span></span>
<span data-ttu-id="d8cf0-108">我們可以指派 hello 使用者 tooGuest 邀請者角色 toosend 邀請。</span><span class="sxs-lookup"><span data-stu-id="d8cf0-108">We can assign hello user tooGuest Inviter role toosend invitations.</span></span> <span data-ttu-id="d8cf0-109">您不需要 hello 全域管理員角色 toosend 邀請 toobe 的成員。</span><span class="sxs-lookup"><span data-stu-id="d8cf0-109">You don't have toobe member of hello global admin role toosend invitations.</span></span> <span data-ttu-id="d8cf0-110">根據預設，一般使用者也可以叫用 hello 邀請 API 全域系統管理員停用一般使用者的邀請。</span><span class="sxs-lookup"><span data-stu-id="d8cf0-110">By default, regular users can also invoke hello invite API unless a global admin disabled invitations for regular users.</span></span> <span data-ttu-id="d8cf0-111">使用者也可以叫用 hello API 使用 hello Azure 入口網站或 PowerShell。</span><span class="sxs-lookup"><span data-stu-id="d8cf0-111">A user can also invoke hello API using hello Azure portal or PowerShell.</span></span>

<span data-ttu-id="d8cf0-112">以下是範例顯示如何 toouse PowerShell tooadd 使用者 toohello 來賓邀請者角色：</span><span class="sxs-lookup"><span data-stu-id="d8cf0-112">Here's an example that shows how toouse PowerShell tooadd a user toohello Guest Inviter role:</span></span>

```
Add-MsolRoleMember -RoleObjectId 95e79109-95c0-4d8e-aee3-d01accf2d47b -RoleMemberEmailAddress <RoleMemberEmailAddress>
```

## <a name="control-who-can-invite"></a><span data-ttu-id="d8cf0-113">控制誰可以邀請</span><span class="sxs-lookup"><span data-stu-id="d8cf0-113">Control who can invite</span></span>

![控制如何 tooinvite](media/active-directory-b2b-delegate-invitations/control-who-to-invite.png)

<span data-ttu-id="d8cf0-115">Azure AD B2B 共同作業，租用戶系統管理員可以設定下列邀請原則 hello:</span><span class="sxs-lookup"><span data-stu-id="d8cf0-115">With Azure AD B2B collaboration, a tenant admin can set hello following invitation policies:</span></span>

- <span data-ttu-id="d8cf0-116">關閉邀請</span><span class="sxs-lookup"><span data-stu-id="d8cf0-116">Turn off invitations</span></span>
- <span data-ttu-id="d8cf0-117">只有系統管理員和 hello 來賓邀請者角色中的使用者可以邀請</span><span class="sxs-lookup"><span data-stu-id="d8cf0-117">Only admins and users in hello Guest Inviter role can invite</span></span>
- <span data-ttu-id="d8cf0-118">系統管理員、 hello 來賓邀請者角色和成員可以邀請</span><span class="sxs-lookup"><span data-stu-id="d8cf0-118">Admins, hello Guest Inviter role, and members can invite</span></span>
- <span data-ttu-id="d8cf0-119">所有使用者 (包括來賓) 都可以邀請</span><span class="sxs-lookup"><span data-stu-id="d8cf0-119">All users, including guests, can invite</span></span>

<span data-ttu-id="d8cf0-120">根據預設，租用戶設定太 #4。</span><span class="sxs-lookup"><span data-stu-id="d8cf0-120">By default, tenants are set too#4.</span></span> <span data-ttu-id="d8cf0-121">(所有使用者 (包括來賓) 都可以邀請 B2B 使用者。)</span><span class="sxs-lookup"><span data-stu-id="d8cf0-121">(All users, including guests, can invite B2B users.)</span></span>

## <a name="next-steps"></a><span data-ttu-id="d8cf0-122">後續步驟</span><span class="sxs-lookup"><span data-stu-id="d8cf0-122">Next steps</span></span>

<span data-ttu-id="d8cf0-123">請瀏覽有關 Azure AD B2B 共同作業的其他文章：</span><span class="sxs-lookup"><span data-stu-id="d8cf0-123">Browse our other articles on Azure AD B2B collaboration:</span></span>

* [<span data-ttu-id="d8cf0-124">何謂 Azure AD B2B 共同作業？</span><span class="sxs-lookup"><span data-stu-id="d8cf0-124">What is Azure AD B2B collaboration?</span></span>](active-directory-b2b-what-is-azure-ad-b2b.md)
* [<span data-ttu-id="d8cf0-125">B2B 共同作業使用者屬性</span><span class="sxs-lookup"><span data-stu-id="d8cf0-125">B2B collaboration user properties</span></span>](active-directory-b2b-user-properties.md)
* [<span data-ttu-id="d8cf0-126">新增 B2B 共同作業使用者 tooa 角色</span><span class="sxs-lookup"><span data-stu-id="d8cf0-126">Adding a B2B collaboration user tooa role</span></span>](active-directory-b2b-add-guest-to-role.md)
* [<span data-ttu-id="d8cf0-127">動態群組與 B2B 共同作業</span><span class="sxs-lookup"><span data-stu-id="d8cf0-127">Dynamic groups and B2B collaboration</span></span>](active-directory-b2b-dynamic-groups.md)
* [<span data-ttu-id="d8cf0-128">B2B 共同作業程式碼與 PowerShell 範例</span><span class="sxs-lookup"><span data-stu-id="d8cf0-128">B2B collaboration code and PowerShell samples</span></span>](active-directory-b2b-code-samples.md)
* [<span data-ttu-id="d8cf0-129">設定適用於 B2B 共同作業的 SaaS 應用程式</span><span class="sxs-lookup"><span data-stu-id="d8cf0-129">Configure SaaS apps for B2B collaboration</span></span>](active-directory-b2b-configure-saas-apps.md)
* [<span data-ttu-id="d8cf0-130">B2B 共同作業使用者權杖</span><span class="sxs-lookup"><span data-stu-id="d8cf0-130">B2B collaboration user tokens</span></span>](active-directory-b2b-user-token.md)
* [<span data-ttu-id="d8cf0-131">B2B 共同作業使用者宣告對應</span><span class="sxs-lookup"><span data-stu-id="d8cf0-131">B2B collaboration user claims mapping</span></span>](active-directory-b2b-claims-mapping.md)
* [<span data-ttu-id="d8cf0-132">Office 365 外部共用</span><span class="sxs-lookup"><span data-stu-id="d8cf0-132">Office 365 external sharing</span></span>](active-directory-b2b-o365-external-user.md)
* [<span data-ttu-id="d8cf0-133">B2B 共同作業目前的限制</span><span class="sxs-lookup"><span data-stu-id="d8cf0-133">B2B collaboration current limitations</span></span>](active-directory-b2b-current-limitations.md)
