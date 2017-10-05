---
title: "委派 Azure Active Directory B2B 共同作業邀請 | Microsoft Docs"
description: "Azure Active Directory B2B 共同作業使用者屬性是可設定的"
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
ms.openlocfilehash: 78613cc978b585a98d235245194c02371f7f3849
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="delegate-invitations-for-azure-active-directory-b2b-collaboration"></a><span data-ttu-id="41933-103">委派 Azure Active Directory B2B 共同作業邀請</span><span class="sxs-lookup"><span data-stu-id="41933-103">Delegate invitations for Azure Active Directory B2B collaboration</span></span>

<span data-ttu-id="41933-104">使用 Azure Active Directory (Azure AD) 企業對企業 (B2B) 共同作業時，您不需要是全域系統管理員即可傳送邀請。</span><span class="sxs-lookup"><span data-stu-id="41933-104">With Azure Active Directory (Azure AD) business-to-business (B2B) collaboration, you do not have to be a global admin to send invitations.</span></span> <span data-ttu-id="41933-105">相反地，您可以使用相關原則並將邀請委派給其角色允許他們傳送邀請的使用者。</span><span class="sxs-lookup"><span data-stu-id="41933-105">Instead, you can use policies and delegate invitations to users whose roles allow them to send invitations.</span></span> <span data-ttu-id="41933-106">委派來賓使用者邀請的一個重要新方式是透過「來賓邀請者」角色。</span><span class="sxs-lookup"><span data-stu-id="41933-106">An important new way to delegate guest user invitations is through the Guest Inviter role.</span></span>

## <a name="guest-inviter-role"></a><span data-ttu-id="41933-107">來賓邀請者角色</span><span class="sxs-lookup"><span data-stu-id="41933-107">Guest Inviter role</span></span>
<span data-ttu-id="41933-108">我們可以將使用者指派到「來賓邀請者」角色以傳送邀請。</span><span class="sxs-lookup"><span data-stu-id="41933-108">We can assign the user to Guest Inviter role to send invitations.</span></span> <span data-ttu-id="41933-109">您不需要是全域系統管理員角色的成員即可傳送邀請。</span><span class="sxs-lookup"><span data-stu-id="41933-109">You don't have to be member of the global admin role to send invitations.</span></span> <span data-ttu-id="41933-110">根據預設，一般使用者也可叫用邀請 API，除非全域系統管理員已停用一般使用者的邀請功能。</span><span class="sxs-lookup"><span data-stu-id="41933-110">By default, regular users can also invoke the invite API unless a global admin disabled invitations for regular users.</span></span> <span data-ttu-id="41933-111">使用者也可以使用 Azure 入口網站或 PowerShell 來叫用 API。</span><span class="sxs-lookup"><span data-stu-id="41933-111">A user can also invoke the API using the Azure portal or PowerShell.</span></span>

<span data-ttu-id="41933-112">以下範例顯示如何使用 PowerShell 將使用者新增到「來賓邀請者」角色：</span><span class="sxs-lookup"><span data-stu-id="41933-112">Here's an example that shows how to use PowerShell to add a user to the Guest Inviter role:</span></span>

```
Add-MsolRoleMember -RoleObjectId 95e79109-95c0-4d8e-aee3-d01accf2d47b -RoleMemberEmailAddress <RoleMemberEmailAddress>
```

## <a name="control-who-can-invite"></a><span data-ttu-id="41933-113">控制誰可以邀請</span><span class="sxs-lookup"><span data-stu-id="41933-113">Control who can invite</span></span>

![控制邀請方式](media/active-directory-b2b-delegate-invitations/control-who-to-invite.png)

<span data-ttu-id="41933-115">使用 Azure AD B2B 共同作業，租用戶系統管理員可以設定下列邀請原則：</span><span class="sxs-lookup"><span data-stu-id="41933-115">With Azure AD B2B collaboration, a tenant admin can set the following invitation policies:</span></span>

- <span data-ttu-id="41933-116">關閉邀請</span><span class="sxs-lookup"><span data-stu-id="41933-116">Turn off invitations</span></span>
- <span data-ttu-id="41933-117">只有系統管理員與「來賓邀請者」角色中使用者可以邀請</span><span class="sxs-lookup"><span data-stu-id="41933-117">Only admins and users in the Guest Inviter role can invite</span></span>
- <span data-ttu-id="41933-118">系統管理員、來賓邀請者角色與成員可以邀請</span><span class="sxs-lookup"><span data-stu-id="41933-118">Admins, the Guest Inviter role, and members can invite</span></span>
- <span data-ttu-id="41933-119">所有使用者 (包括來賓) 都可以邀請</span><span class="sxs-lookup"><span data-stu-id="41933-119">All users, including guests, can invite</span></span>

<span data-ttu-id="41933-120">根據預設，租用戶會設定為 #4。</span><span class="sxs-lookup"><span data-stu-id="41933-120">By default, tenants are set to #4.</span></span> <span data-ttu-id="41933-121">(所有使用者 (包括來賓) 都可以邀請 B2B 使用者。)</span><span class="sxs-lookup"><span data-stu-id="41933-121">(All users, including guests, can invite B2B users.)</span></span>

## <a name="next-steps"></a><span data-ttu-id="41933-122">後續步驟</span><span class="sxs-lookup"><span data-stu-id="41933-122">Next steps</span></span>

<span data-ttu-id="41933-123">請瀏覽有關 Azure AD B2B 共同作業的其他文章：</span><span class="sxs-lookup"><span data-stu-id="41933-123">Browse our other articles on Azure AD B2B collaboration:</span></span>

* [<span data-ttu-id="41933-124">何謂 Azure AD B2B 共同作業？</span><span class="sxs-lookup"><span data-stu-id="41933-124">What is Azure AD B2B collaboration?</span></span>](active-directory-b2b-what-is-azure-ad-b2b.md)
* [<span data-ttu-id="41933-125">B2B 共同作業使用者屬性</span><span class="sxs-lookup"><span data-stu-id="41933-125">B2B collaboration user properties</span></span>](active-directory-b2b-user-properties.md)
* [<span data-ttu-id="41933-126">將 B2B 共同作業使用者新增至角色</span><span class="sxs-lookup"><span data-stu-id="41933-126">Adding a B2B collaboration user to a role</span></span>](active-directory-b2b-add-guest-to-role.md)
* [<span data-ttu-id="41933-127">動態群組與 B2B 共同作業</span><span class="sxs-lookup"><span data-stu-id="41933-127">Dynamic groups and B2B collaboration</span></span>](active-directory-b2b-dynamic-groups.md)
* [<span data-ttu-id="41933-128">B2B 共同作業程式碼與 PowerShell 範例</span><span class="sxs-lookup"><span data-stu-id="41933-128">B2B collaboration code and PowerShell samples</span></span>](active-directory-b2b-code-samples.md)
* [<span data-ttu-id="41933-129">設定適用於 B2B 共同作業的 SaaS 應用程式</span><span class="sxs-lookup"><span data-stu-id="41933-129">Configure SaaS apps for B2B collaboration</span></span>](active-directory-b2b-configure-saas-apps.md)
* [<span data-ttu-id="41933-130">B2B 共同作業使用者權杖</span><span class="sxs-lookup"><span data-stu-id="41933-130">B2B collaboration user tokens</span></span>](active-directory-b2b-user-token.md)
* [<span data-ttu-id="41933-131">B2B 共同作業使用者宣告對應</span><span class="sxs-lookup"><span data-stu-id="41933-131">B2B collaboration user claims mapping</span></span>](active-directory-b2b-claims-mapping.md)
* [<span data-ttu-id="41933-132">Office 365 外部共用</span><span class="sxs-lookup"><span data-stu-id="41933-132">Office 365 external sharing</span></span>](active-directory-b2b-o365-external-user.md)
* [<span data-ttu-id="41933-133">B2B 共同作業目前的限制</span><span class="sxs-lookup"><span data-stu-id="41933-133">B2B collaboration current limitations</span></span>](active-directory-b2b-current-limitations.md)
