---
title: "Azure Active Directory B2B 共同作業 aaaLimitations |Microsoft 文件"
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
ms.openlocfilehash: 322081f32fbacfe67ee1300993c7df1870e498bd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="limitations-of-azure-ad-b2b-collaboration"></a><span data-ttu-id="cb363-103">Azure AD B2B 共同作業的限制</span><span class="sxs-lookup"><span data-stu-id="cb363-103">Limitations of Azure AD B2B collaboration</span></span>
<span data-ttu-id="cb363-104">這篇文章中所述的主旨 toohello 限制的目前 azure Active Directory (Azure AD) B2B 共同作業。</span><span class="sxs-lookup"><span data-stu-id="cb363-104">Azure Active Directory (Azure AD) B2B collaboration is currently subject toohello limitations described in this article.</span></span>

## <a name="possible-double-multi-factor-authentication"></a><span data-ttu-id="cb363-105">可能的雙重多重要素驗證</span><span class="sxs-lookup"><span data-stu-id="cb363-105">Possible double multi-factor authentication</span></span>
<span data-ttu-id="cb363-106">與 Azure AD B2B，您可以強制執行多重要素驗證在 hello 資源組織 (hello 邀請組織)。</span><span class="sxs-lookup"><span data-stu-id="cb363-106">With Azure AD B2B, you can enforce multi-factor authentication at hello resource organization (hello inviting organization).</span></span> <span data-ttu-id="cb363-107">這種方法的 hello 原因的詳細[B2B 共同作業的使用者的條件式存取](active-directory-b2b-mfa-instructions.md)。</span><span class="sxs-lookup"><span data-stu-id="cb363-107">hello reasons for this approach are detailed in [Conditional access for B2B collaboration users](active-directory-b2b-mfa-instructions.md).</span></span> <span data-ttu-id="cb363-108">如果夥伴已設定，並強制執行多重要素驗證，使用者可能已經使用 tooperform hello 驗證一次其主要組織，然後在您一次。</span><span class="sxs-lookup"><span data-stu-id="cb363-108">If a partner already has multi-factor authentication set up and enforced, their users might have tooperform hello authentication once in their home organization and then again in yours.</span></span>

## <a name="instant-on"></a><span data-ttu-id="cb363-109">即時</span><span class="sxs-lookup"><span data-stu-id="cb363-109">Instant-on</span></span>
<span data-ttu-id="cb363-110">在 hello B2B 共同作業的流量，我們會加入使用者 toohello 目錄，並動態更新期間兌換邀請、 應用程式指派和等等。</span><span class="sxs-lookup"><span data-stu-id="cb363-110">In hello B2B collaboration flows, we add users toohello directory and dynamically update them during invitation redemption, app assignment, and so on.</span></span> <span data-ttu-id="cb363-111">hello 更新寫入通常發生在一個目錄執行個體和必須在所有執行個體之間進行複寫。</span><span class="sxs-lookup"><span data-stu-id="cb363-111">hello updates and writes ordinarily happen in one directory instance and must be replicated across all instances.</span></span> <span data-ttu-id="cb363-112">在所有執行個體都更新後，複寫作業便已完成。</span><span class="sxs-lookup"><span data-stu-id="cb363-112">Replication is completed once all instances are updated.</span></span> <span data-ttu-id="cb363-113">有時當 hello 物件寫入或更新中有一個執行個體和 hello 呼叫 tooretrieve 這個物件是 tooanother 執行個體，複寫延遲可能會發生。</span><span class="sxs-lookup"><span data-stu-id="cb363-113">Sometimes when hello object is written or updated in one instance and hello call tooretrieve this object is tooanother instance, replication latencies can occur.</span></span> <span data-ttu-id="cb363-114">如果發生這種情況，請重新整理或 toohelp 重試一次。</span><span class="sxs-lookup"><span data-stu-id="cb363-114">If that happens, refresh or retry toohelp.</span></span> <span data-ttu-id="cb363-115">如果您要撰寫的應用程式，但有一些使用我們的應用程式開發介面，然後重試輪詢是防禦的好作法 tooalleviate 此問題。</span><span class="sxs-lookup"><span data-stu-id="cb363-115">If you are writing an app using our API, then retries with some back-off is a good, defensive practice tooalleviate this issue.</span></span>

## <a name="next-steps"></a><span data-ttu-id="cb363-116">後續步驟</span><span class="sxs-lookup"><span data-stu-id="cb363-116">Next steps</span></span>

<span data-ttu-id="cb363-117">請瀏覽有關 Azure AD B2B 共同作業的其他文章：</span><span class="sxs-lookup"><span data-stu-id="cb363-117">Browse our other articles on Azure AD B2B collaboration:</span></span>

* [<span data-ttu-id="cb363-118">何謂 Azure AD B2B 共同作業？</span><span class="sxs-lookup"><span data-stu-id="cb363-118">What is Azure AD B2B collaboration?</span></span>](active-directory-b2b-what-is-azure-ad-b2b.md)
* [<span data-ttu-id="cb363-119">B2B 共同作業使用者屬性</span><span class="sxs-lookup"><span data-stu-id="cb363-119">B2B collaboration user properties</span></span>](active-directory-b2b-user-properties.md)
* [<span data-ttu-id="cb363-120">新增 B2B 共同作業使用者 tooa 角色</span><span class="sxs-lookup"><span data-stu-id="cb363-120">Adding a B2B collaboration user tooa role</span></span>](active-directory-b2b-add-guest-to-role.md)
* [<span data-ttu-id="cb363-121">委派 B2B 共同作業邀請</span><span class="sxs-lookup"><span data-stu-id="cb363-121">Delegate B2bB collaboration invitations</span></span>](active-directory-b2b-delegate-invitations.md)
* [<span data-ttu-id="cb363-122">動態群組與 B2B 共同作業</span><span class="sxs-lookup"><span data-stu-id="cb363-122">Dynamic groups and B2B collaboration</span></span>](active-directory-b2b-dynamic-groups.md)
* [<span data-ttu-id="cb363-123">B2B 共同作業程式碼與 PowerShell 範例</span><span class="sxs-lookup"><span data-stu-id="cb363-123">B2B collaboration code and PowerShell samples</span></span>](active-directory-b2b-code-samples.md)
* [<span data-ttu-id="cb363-124">設定適用於 B2B 共同作業的 SaaS 應用程式</span><span class="sxs-lookup"><span data-stu-id="cb363-124">Configure SaaS apps for B2B collaboration</span></span>](active-directory-b2b-configure-saas-apps.md)
* [<span data-ttu-id="cb363-125">B2B 共同作業使用者權杖</span><span class="sxs-lookup"><span data-stu-id="cb363-125">B2B collaboration user tokens</span></span>](active-directory-b2b-user-token.md)
* [<span data-ttu-id="cb363-126">B2B 共同作業使用者宣告對應</span><span class="sxs-lookup"><span data-stu-id="cb363-126">B2B collaboration user claims mapping</span></span>](active-directory-b2b-claims-mapping.md)
* [<span data-ttu-id="cb363-127">Office 365 外部共用</span><span class="sxs-lookup"><span data-stu-id="cb363-127">Office 365 external sharing</span></span>](active-directory-b2b-o365-external-user.md)
