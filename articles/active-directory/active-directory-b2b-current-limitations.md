---
title: "Azure Active Directory B2B 共同作業的限制 | Microsoft Docs"
description: "Azure Active Directory B2B 共同作業目前的限制"
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
ms.openlocfilehash: 581e5d1fb5fb08d0dc89ed2c85edcb5f0005650b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="limitations-of-azure-ad-b2b-collaboration"></a><span data-ttu-id="a2fb4-103">Azure AD B2B 共同作業的限制</span><span class="sxs-lookup"><span data-stu-id="a2fb4-103">Limitations of Azure AD B2B collaboration</span></span>
<span data-ttu-id="a2fb4-104">Azure Active Directory (Azure AD) B2B 共同作業目前受限於本文所述的限制。</span><span class="sxs-lookup"><span data-stu-id="a2fb4-104">Azure Active Directory (Azure AD) B2B collaboration is currently subject to the limitations described in this article.</span></span>

## <a name="possible-double-multi-factor-authentication"></a><span data-ttu-id="a2fb4-105">可能的雙重多重要素驗證</span><span class="sxs-lookup"><span data-stu-id="a2fb4-105">Possible double multi-factor authentication</span></span>
<span data-ttu-id="a2fb4-106">使用 Azure AD B2B，您便可以在資源組織 (邀請組織) 強制執行多重要素驗證。</span><span class="sxs-lookup"><span data-stu-id="a2fb4-106">With Azure AD B2B, you can enforce multi-factor authentication at the resource organization (the inviting organization).</span></span> <span data-ttu-id="a2fb4-107">若要了解採用此方法的詳細原因，請參閱 [B2B 共同作業使用者的條件式存取](active-directory-b2b-mfa-instructions.md)。</span><span class="sxs-lookup"><span data-stu-id="a2fb4-107">The reasons for this approach are detailed in [Conditional access for B2B collaboration users](active-directory-b2b-mfa-instructions.md).</span></span> <span data-ttu-id="a2fb4-108">如果合作夥伴已設定並強制使用 Multi-Factor Authentication，其使用者可能必須在其所屬組織執行一次驗證，然後在您的組織中再次執行驗證。</span><span class="sxs-lookup"><span data-stu-id="a2fb4-108">If a partner already has multi-factor authentication set up and enforced, their users might have to perform the authentication once in their home organization and then again in yours.</span></span>

## <a name="instant-on"></a><span data-ttu-id="a2fb4-109">即時</span><span class="sxs-lookup"><span data-stu-id="a2fb4-109">Instant-on</span></span>
<span data-ttu-id="a2fb4-110">在 B2B 共同作業流程中，我們會新增使用者到目錄中，並在邀請兌換與應用程式指派等期間動態更新它們。</span><span class="sxs-lookup"><span data-stu-id="a2fb4-110">In the B2B collaboration flows, we add users to the directory and dynamically update them during invitation redemption, app assignment, and so on.</span></span> <span data-ttu-id="a2fb4-111">更新與寫入通常會在一個目錄執行個體中進行，而且必須複寫到所有執行個體。</span><span class="sxs-lookup"><span data-stu-id="a2fb4-111">The updates and writes ordinarily happen in one directory instance and must be replicated across all instances.</span></span> <span data-ttu-id="a2fb4-112">在所有執行個體都更新後，複寫作業便已完成。</span><span class="sxs-lookup"><span data-stu-id="a2fb4-112">Replication is completed once all instances are updated.</span></span> <span data-ttu-id="a2fb4-113">有時，在某個執行個體中寫入或更新物件，但另一個執行個體呼叫擷取此物件時，就會發生複寫延遲問題。</span><span class="sxs-lookup"><span data-stu-id="a2fb4-113">Sometimes when the object is written or updated in one instance and the call to retrieve this object is to another instance, replication latencies can occur.</span></span> <span data-ttu-id="a2fb4-114">如果發生該情況，請重新整理或重試來提供幫助。</span><span class="sxs-lookup"><span data-stu-id="a2fb4-114">If that happens, refresh or retry to help.</span></span> <span data-ttu-id="a2fb4-115">如果您正在使用我們的 API 來撰寫應用程式，則採用某種讓步來重試是可減輕此問題的良好防禦性做法。</span><span class="sxs-lookup"><span data-stu-id="a2fb4-115">If you are writing an app using our API, then retries with some back-off is a good, defensive practice to alleviate this issue.</span></span>

## <a name="next-steps"></a><span data-ttu-id="a2fb4-116">後續步驟</span><span class="sxs-lookup"><span data-stu-id="a2fb4-116">Next steps</span></span>

<span data-ttu-id="a2fb4-117">請瀏覽有關 Azure AD B2B 共同作業的其他文章：</span><span class="sxs-lookup"><span data-stu-id="a2fb4-117">Browse our other articles on Azure AD B2B collaboration:</span></span>

* [<span data-ttu-id="a2fb4-118">何謂 Azure AD B2B 共同作業？</span><span class="sxs-lookup"><span data-stu-id="a2fb4-118">What is Azure AD B2B collaboration?</span></span>](active-directory-b2b-what-is-azure-ad-b2b.md)
* [<span data-ttu-id="a2fb4-119">B2B 共同作業使用者屬性</span><span class="sxs-lookup"><span data-stu-id="a2fb4-119">B2B collaboration user properties</span></span>](active-directory-b2b-user-properties.md)
* [<span data-ttu-id="a2fb4-120">將 B2B 共同作業使用者新增至角色</span><span class="sxs-lookup"><span data-stu-id="a2fb4-120">Adding a B2B collaboration user to a role</span></span>](active-directory-b2b-add-guest-to-role.md)
* [<span data-ttu-id="a2fb4-121">委派 B2B 共同作業邀請</span><span class="sxs-lookup"><span data-stu-id="a2fb4-121">Delegate B2bB collaboration invitations</span></span>](active-directory-b2b-delegate-invitations.md)
* [<span data-ttu-id="a2fb4-122">動態群組與 B2B 共同作業</span><span class="sxs-lookup"><span data-stu-id="a2fb4-122">Dynamic groups and B2B collaboration</span></span>](active-directory-b2b-dynamic-groups.md)
* [<span data-ttu-id="a2fb4-123">B2B 共同作業程式碼與 PowerShell 範例</span><span class="sxs-lookup"><span data-stu-id="a2fb4-123">B2B collaboration code and PowerShell samples</span></span>](active-directory-b2b-code-samples.md)
* [<span data-ttu-id="a2fb4-124">設定適用於 B2B 共同作業的 SaaS 應用程式</span><span class="sxs-lookup"><span data-stu-id="a2fb4-124">Configure SaaS apps for B2B collaboration</span></span>](active-directory-b2b-configure-saas-apps.md)
* [<span data-ttu-id="a2fb4-125">B2B 共同作業使用者權杖</span><span class="sxs-lookup"><span data-stu-id="a2fb4-125">B2B collaboration user tokens</span></span>](active-directory-b2b-user-token.md)
* [<span data-ttu-id="a2fb4-126">B2B 共同作業使用者宣告對應</span><span class="sxs-lookup"><span data-stu-id="a2fb4-126">B2B collaboration user claims mapping</span></span>](active-directory-b2b-claims-mapping.md)
* [<span data-ttu-id="a2fb4-127">Office 365 外部共用</span><span class="sxs-lookup"><span data-stu-id="a2fb4-127">Office 365 external sharing</span></span>](active-directory-b2b-o365-external-user.md)
