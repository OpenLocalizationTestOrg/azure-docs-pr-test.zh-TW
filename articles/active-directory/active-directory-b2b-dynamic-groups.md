---
title: "aaaDynamic 群組和 Azure Active Directory B2B 共同作業 |Microsoft 文件"
description: "Azure Active Directory B2B 共同作業可搭配 Azure AD 動態群組使用"
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
ms.date: 06/27/2017
ms.author: curtand
ms.reviewer: sasubram
ms.openlocfilehash: b011298de5fd2c851c6d9caaf5c2b257807ef0a4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="dynamic-groups-and-azure-active-directory-b2b-collaboration"></a><span data-ttu-id="09e7d-103">動態群組與 Azure Active Directory B2B 共同作業</span><span class="sxs-lookup"><span data-stu-id="09e7d-103">Dynamic groups and Azure Active Directory B2B collaboration</span></span>

## <a name="what-are-dynamic-groups"></a><span data-ttu-id="09e7d-104">什麼是動態群組？</span><span class="sxs-lookup"><span data-stu-id="09e7d-104">What are dynamic groups?</span></span>
<span data-ttu-id="09e7d-105">Azure Active directory (Azure AD) 的動態組態的安全性群組成員資格位於[hello Azure 入口網站](https://portal.azure.com)。</span><span class="sxs-lookup"><span data-stu-id="09e7d-105">Dynamic configuration of security group membership for Azure Active Directory (Azure AD) is available in [hello Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="09e7d-106">系統管理員可以設定 Azure Active Directory 中建立的 toopopulate 群組根據使用者屬性 （例如 userType、 部門或國家/地區） 的規則。</span><span class="sxs-lookup"><span data-stu-id="09e7d-106">Administrators can set rules toopopulate groups that are created in Azure Active Directory based on user attributes (such as userType, department, or country).</span></span> <span data-ttu-id="09e7d-107">成員可以從其屬性為基礎的安全性群組移除 tooor 會自動新增。</span><span class="sxs-lookup"><span data-stu-id="09e7d-107">Members can be automatically added tooor removed from a security group based on their attributes.</span></span> <span data-ttu-id="09e7d-108">這些群組可提供存取 tooapplications 或雲端資源 （SharePoint 網站、 文件），並 tooassign 授權 toomembers。</span><span class="sxs-lookup"><span data-stu-id="09e7d-108">These groups can provide access tooapplications or cloud resources (SharePoint sites, documents) and tooassign licenses toomembers.</span></span> <span data-ttu-id="09e7d-109">若要深入了解動態群組，請參閱 [Azure Active Directory 中的專用群組](active-directory-accessmanagement-dedicated-groups.md)。</span><span class="sxs-lookup"><span data-stu-id="09e7d-109">Read more about dynamic groups in [Dedicated groups in Azure Active Directory](active-directory-accessmanagement-dedicated-groups.md).</span></span>

<span data-ttu-id="09e7d-110">hello 適當[Azure AD Premium P1 或 P2 授權](https://azure.microsoft.com/pricing/details/active-directory/)是必要的 toocreate 和使用動態群組。</span><span class="sxs-lookup"><span data-stu-id="09e7d-110">hello appropriate [Azure AD Premium P1 or P2 licensing](https://azure.microsoft.com/pricing/details/active-directory/) is required toocreate and use dynamic groups.</span></span> <span data-ttu-id="09e7d-111">進一步了解本文 hello[建立 Azure Active Directory 中的屬性為基礎的動態群組成員資格規則](active-directory-groups-dynamic-membership-azure-portal.md)。</span><span class="sxs-lookup"><span data-stu-id="09e7d-111">Learn more in hello article [Create attribute-based rules for dynamic group membership in Azure Active Directory](active-directory-groups-dynamic-membership-azure-portal.md).</span></span>

## <a name="what-are-hello-built-in-dynamic-groups"></a><span data-ttu-id="09e7d-112">Hello 內建的動態群組有哪些？</span><span class="sxs-lookup"><span data-stu-id="09e7d-112">What are hello built-in dynamic groups?</span></span>
<span data-ttu-id="09e7d-113">hello**所有使用者**動態群組可讓租用戶系統管理員 」 toocreate 按一下群組，包含具有單一 hello 租用戶中的所有使用者。</span><span class="sxs-lookup"><span data-stu-id="09e7d-113">hello **All users** dynamic group enables tenant admins toocreate a group containing all users in hello tenant with a single click.</span></span> <span data-ttu-id="09e7d-114">根據預設，hello**所有使用者**群組包含所有使用者在 hello 目錄中，包括成員和來賓。</span><span class="sxs-lookup"><span data-stu-id="09e7d-114">By default, hello **All users** group includes all users in hello directory, including Members and Guests.</span></span>
<span data-ttu-id="09e7d-115">在 [hello 新 Azure Active Directory 系統管理員入口網站中，您可以選擇 tooenable hello**所有使用者**群組 hello 群組設定] 檢視中。</span><span class="sxs-lookup"><span data-stu-id="09e7d-115">Within hello new Azure Active Directory admin portal, you can choose tooenable hello **All users** group in hello Group Settings view.</span></span>

![內建群組](media/active-directory-b2b-dynamic-groups/built-in-groups.png)

## <a name="hardening-hello-all-users-dynamic-group"></a><span data-ttu-id="09e7d-117">強化 hello 所有使用者的動態群組</span><span class="sxs-lookup"><span data-stu-id="09e7d-117">Hardening hello All users dynamic group</span></span>
<span data-ttu-id="09e7d-118">根據預設，hello**所有使用者**群組包含您 B2B 共同作業 (guest) 使用者，以及。</span><span class="sxs-lookup"><span data-stu-id="09e7d-118">By default, hello **All users** group contains your B2B collaboration (guest) users as well.</span></span> <span data-ttu-id="09e7d-119">您可以進一步保護您**所有使用者**使用規則 tooremove 來賓使用者群組。</span><span class="sxs-lookup"><span data-stu-id="09e7d-119">You can further secure your **All users** group by using a rule tooremove guest users.</span></span> <span data-ttu-id="09e7d-120">hello 如下圖所示 hello**所有使用者**修改 tooexclude guests 群組。</span><span class="sxs-lookup"><span data-stu-id="09e7d-120">hello following illustration shows hello **All users** group modified tooexclude guests.</span></span>

![啟用所有使用者群組](media/active-directory-b2b-dynamic-groups/enable-all-users-group.png)

<span data-ttu-id="09e7d-122">您可能也會很有用 toocreate 新的動態群組，其中包含只 guest 使用者，讓您可以套用原則 （例如 Azure AD 條件式存取原則） toothem。</span><span class="sxs-lookup"><span data-stu-id="09e7d-122">You might also find it useful toocreate a new dynamic group that contains only guest users, so that you can apply policies (such as Azure AD Conditional Access policies) toothem.</span></span>
<span data-ttu-id="09e7d-123">這種群組可能如下所示：</span><span class="sxs-lookup"><span data-stu-id="09e7d-123">What such a group might look like:</span></span>

![排除來賓使用者](media/active-directory-b2b-dynamic-groups/exclude-guest-users.png)

## <a name="next-steps"></a><span data-ttu-id="09e7d-125">後續步驟</span><span class="sxs-lookup"><span data-stu-id="09e7d-125">Next steps</span></span>

<span data-ttu-id="09e7d-126">請瀏覽有關 Azure AD B2B 共同作業的其他文章：</span><span class="sxs-lookup"><span data-stu-id="09e7d-126">Browse our other articles on Azure AD B2B collaboration:</span></span>

* [<span data-ttu-id="09e7d-127">何謂 Azure AD B2B 共同作業？</span><span class="sxs-lookup"><span data-stu-id="09e7d-127">What is Azure AD B2B collaboration?</span></span>](active-directory-b2b-what-is-azure-ad-b2b.md)
* [<span data-ttu-id="09e7d-128">B2B 共同作業使用者屬性</span><span class="sxs-lookup"><span data-stu-id="09e7d-128">B2B collaboration user properties</span></span>](active-directory-b2b-user-properties.md)
* [<span data-ttu-id="09e7d-129">新增 B2B 共同作業使用者 tooa 角色</span><span class="sxs-lookup"><span data-stu-id="09e7d-129">Adding a B2B collaboration user tooa role</span></span>](active-directory-b2b-add-guest-to-role.md)
* [<span data-ttu-id="09e7d-130">委派 B2B 共同作業邀請</span><span class="sxs-lookup"><span data-stu-id="09e7d-130">Delegate B2B collaboration invitations</span></span>](active-directory-b2b-delegate-invitations.md)
* [<span data-ttu-id="09e7d-131">B2B 共同作業程式碼與 PowerShell 範例</span><span class="sxs-lookup"><span data-stu-id="09e7d-131">B2B collaboration code and PowerShell samples</span></span>](active-directory-b2b-code-samples.md)
* [<span data-ttu-id="09e7d-132">設定適用於 B2B 共同作業的 SaaS 應用程式</span><span class="sxs-lookup"><span data-stu-id="09e7d-132">Configure SaaS apps for B2B collaboration</span></span>](active-directory-b2b-configure-saas-apps.md)
* [<span data-ttu-id="09e7d-133">B2B 共同作業使用者權杖</span><span class="sxs-lookup"><span data-stu-id="09e7d-133">B2B collaboration user tokens</span></span>](active-directory-b2b-user-token.md)
* [<span data-ttu-id="09e7d-134">B2B 共同作業使用者宣告對應</span><span class="sxs-lookup"><span data-stu-id="09e7d-134">B2B collaboration user claims mapping</span></span>](active-directory-b2b-claims-mapping.md)
* [<span data-ttu-id="09e7d-135">Office 365 外部共用</span><span class="sxs-lookup"><span data-stu-id="09e7d-135">Office 365 external sharing</span></span>](active-directory-b2b-o365-external-user.md)
* [<span data-ttu-id="09e7d-136">B2B 共同作業目前的限制</span><span class="sxs-lookup"><span data-stu-id="09e7d-136">B2B collaboration current limitations</span></span>](active-directory-b2b-current-limitations.md)
