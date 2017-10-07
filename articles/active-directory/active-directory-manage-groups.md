---
title: "aaaUse 群組在 Azure Active Directory toomanage 存取 tooresources |Microsoft 文件"
description: "如何在 Azure Active Directory toomanage 使用者 toouse 群組存取 tooon 內部部署和雲端應用程式和資源。"
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: 714120d0-cdf9-465d-afee-39bef591c6b3
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/04/2017
ms.author: curtand
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 876a356c8095505432e9346721f35c7943819e9d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="manage-access-tooresources-with-azure-active-directory-groups"></a><span data-ttu-id="74754-103">使用 Azure Active Directory 群組管理存取 tooresources</span><span class="sxs-lookup"><span data-stu-id="74754-103">Manage access tooresources with Azure Active Directory groups</span></span>
<span data-ttu-id="74754-104">Azure Active Directory (Azure AD) 是完整身分識別和存取管理解決方案，提供一組強固的功能 toomanage 存取 tooon 內部部署和雲端應用程式和資源包括如 Office 365 等 Microsoft online services 和許多非 Microsoft SaaS 應用程式。</span><span class="sxs-lookup"><span data-stu-id="74754-104">Azure Active Directory (Azure AD) is a comprehensive identity and access management solution that provides a robust set of capabilities toomanage access tooon-premises and cloud applications and resources including Microsoft online services like Office 365 and a world of non-Microsoft SaaS applications.</span></span> <span data-ttu-id="74754-105">本文章提供概觀，但如果您想使用 Azure AD 的 toostart 現在分組，請依照下列中的 hello 指示[在 Azure AD 中管理安全性群組](active-directory-accessmanagement-manage-groups.md)。</span><span class="sxs-lookup"><span data-stu-id="74754-105">This article provides an overview, but if you want toostart using Azure AD groups right now, follow hello instructions in [Managing security groups in Azure AD](active-directory-accessmanagement-manage-groups.md).</span></span> <span data-ttu-id="74754-106">如果您想 toosee 如何使用 PowerShell toomanage 您可以深入了解 Azure Active directory 中的群組[群組管理的 Azure Active Directory cmdlet](active-directory-accessmanagement-groups-settings-v2-cmdlets.md)。</span><span class="sxs-lookup"><span data-stu-id="74754-106">If you want toosee how you can use PowerShell toomanage groups in Azure Active directory you can read more in [Azure Active Directory cmdlets for group management](active-directory-accessmanagement-groups-settings-v2-cmdlets.md).</span></span>

> [!NOTE]
> <span data-ttu-id="74754-107">toouse Azure Active Directory，您需要 Azure 帳戶。</span><span class="sxs-lookup"><span data-stu-id="74754-107">toouse Azure Active Directory, you need an Azure account.</span></span> <span data-ttu-id="74754-108">如果您沒有帳戶，您可以 [註冊免費的 Azure 帳戶](https://azure.microsoft.com/pricing/free-trial/)。</span><span class="sxs-lookup"><span data-stu-id="74754-108">If you don't have an account, you can [sign up for a free Azure account](https://azure.microsoft.com/pricing/free-trial/).</span></span>
>
>

<span data-ttu-id="74754-109">在 Azure AD 中，其中一個 hello 主要功能是 hello 能力 toomanage 存取 tooresources。</span><span class="sxs-lookup"><span data-stu-id="74754-109">Within Azure AD, one of hello major features is hello ability toomanage access tooresources.</span></span> <span data-ttu-id="74754-110">這些資源可以是 hello 目錄中，如同透過角色在 hello 目錄或外部 toohello 目錄，例如 SaaS 應用程式、 Azure services 和 SharePoint 網站或內部部署資源的權限 toomanage 物件 hello 案例的一部分資源。</span><span class="sxs-lookup"><span data-stu-id="74754-110">These resources can be part of hello directory, as in hello case of permissions toomanage objects through roles in hello directory, or resources that are external toohello directory, such as SaaS applications, Azure services, and SharePoint sites or on-premises resources.</span></span> <span data-ttu-id="74754-111">有四種方式，可指定使用者存取權限 tooa 資源：</span><span class="sxs-lookup"><span data-stu-id="74754-111">There are four ways a user can be assigned access rights tooa resource:</span></span>

1. <span data-ttu-id="74754-112">直接指派</span><span class="sxs-lookup"><span data-stu-id="74754-112">Direct assignment</span></span>

    <span data-ttu-id="74754-113">可以將使用者指派直接 tooa 資源 hello 該資源的擁有者。</span><span class="sxs-lookup"><span data-stu-id="74754-113">Users can be assigned directly tooa resource by hello owner of that resource.</span></span>
2. <span data-ttu-id="74754-114">群組成員資格</span><span class="sxs-lookup"><span data-stu-id="74754-114">Group membership</span></span>

    <span data-ttu-id="74754-115">群組只能指派 tooa 資源 hello 資源擁有者，並透過這種方式，授與該群組存取 toohello 資源 hello 成員。</span><span class="sxs-lookup"><span data-stu-id="74754-115">A group can be assigned tooa resource by hello resource owner, and by doing so, granting hello members of that group access toohello resource.</span></span> <span data-ttu-id="74754-116">Hello 群組的成員資格然後受 hello hello 群組擁有者。</span><span class="sxs-lookup"><span data-stu-id="74754-116">Membership of hello group can then be managed by hello owner of hello group.</span></span> <span data-ttu-id="74754-117">實際上，hello 資源擁有者委派 hello 權限 tooassign 使用者 tootheir 資源 toohello 群組的擁有者 hello。</span><span class="sxs-lookup"><span data-stu-id="74754-117">Effectively, hello resource owner delegates hello permission tooassign users tootheir resource toohello owner of hello group.</span></span>
3. <span data-ttu-id="74754-118">以規則為基礎</span><span class="sxs-lookup"><span data-stu-id="74754-118">Rule-based</span></span>

    <span data-ttu-id="74754-119">hello 資源擁有者可以使用規則 tooexpress 存取 tooa 資源應該指派的使用者。</span><span class="sxs-lookup"><span data-stu-id="74754-119">hello resource owner can use a rule tooexpress which users should be assigned access tooa resource.</span></span> <span data-ttu-id="74754-120">hello 規則的 hello 結果取決於特定的使用者，該規則和它們的值中所使用的 hello 屬性和透過這種方式，hello 資源擁有者有效地委派 hello 右 toomanage 存取 tootheir 資源 toohello 授權來源 hellohello 規則中使用的屬性。</span><span class="sxs-lookup"><span data-stu-id="74754-120">hello outcome of hello rule depends on hello attributes used in that rule and their values for specific users, and by doing so, hello resource owner effectively delegates hello right toomanage access tootheir resource toohello authoritative source for hello attributes that are used in hello rule.</span></span> <span data-ttu-id="74754-121">hello 資源擁有者仍管理 hello 規則本身，並決定哪些屬性和值提供存取 tootheir 資源。</span><span class="sxs-lookup"><span data-stu-id="74754-121">hello resource owner still manages hello rule itself and determines which attributes and values provide access tootheir resource.</span></span>
4. <span data-ttu-id="74754-122">外部授權單位</span><span class="sxs-lookup"><span data-stu-id="74754-122">External authority</span></span>

    <span data-ttu-id="74754-123">hello 存取 tooa 資源被衍生自外部來源;例如，從授權的來源，例如在內部部署目錄或例如 WorkDay 的 SaaS 應用程式同步處理群組。</span><span class="sxs-lookup"><span data-stu-id="74754-123">hello access tooa resource is derived from an external source; for example, a group that is synchronized from an authoritative source such as an on-premises directory or a SaaS app such as WorkDay.</span></span> <span data-ttu-id="74754-124">hello 資源擁有者指派 hello 群組 tooprovide 存取 toohello 資源，並 hello 外部來源管理 hello hello 群組成員。</span><span class="sxs-lookup"><span data-stu-id="74754-124">hello resource owner assigns hello group tooprovide access toohello resource, and hello external source manages hello members of hello group.</span></span>

   ![存取管理圖表的概觀](./media/active-directory-access-management-groups/access-management-overview.png)

## <a name="watch-a-video-that-explains-access-management"></a><span data-ttu-id="74754-126">觀看說明存取管理的影片</span><span class="sxs-lookup"><span data-stu-id="74754-126">Watch a video that explains access management</span></span>
<span data-ttu-id="74754-127">您可以在此觀賞說明與此相關的短片：</span><span class="sxs-lookup"><span data-stu-id="74754-127">You can watch a short video that explains more about this:</span></span>

<span data-ttu-id="74754-128">**Azure AD： 群組的簡介 toodynamic 成員資格**</span><span class="sxs-lookup"><span data-stu-id="74754-128">**Azure AD: Introduction toodynamic membership for groups**</span></span>

> [!VIDEO https://channel9.msdn.com/Series/Azure-Active-Directory-Videos-Demos/Azure-AD--Introduction-to-Dynamic-Memberships-for-Groups/player]
>
>

## <a name="how-does-access-management-in-azure-active-directory-work"></a><span data-ttu-id="74754-129">存取管理在 Azure Active Directory 中如何運作？</span><span class="sxs-lookup"><span data-stu-id="74754-129">How does access management in Azure Active Directory work?</span></span>
<span data-ttu-id="74754-130">在 hello hello Azure AD 存取管理解決方案的中心是 hello 安全性群組。</span><span class="sxs-lookup"><span data-stu-id="74754-130">At hello center of hello Azure AD access management solution is hello security group.</span></span> <span data-ttu-id="74754-131">使用安全性群組 toomanage 存取 tooresources 是知名的範例，可讓 hello 適合使用者群組的彈性且易於了解的方式 tooprovide 存取 tooa 資源。</span><span class="sxs-lookup"><span data-stu-id="74754-131">Using a security group toomanage access tooresources is a well-known paradigm, which allows for a flexible and easily understood way tooprovide access tooa resource for hello intended group of users.</span></span> <span data-ttu-id="74754-132">hello 資源擁有者 （或 hello hello 目錄管理員） 可以指派群組 tooprovide 特定存取權限 toohello 資源他們所擁有。</span><span class="sxs-lookup"><span data-stu-id="74754-132">hello resource owner (or hello administrator of hello directory) can assign a group tooprovide a certain access right toohello resources they own.</span></span> <span data-ttu-id="74754-133">hello 群組成員的 hello 提供 hello 存取和 hello 資源擁有者可以將委派的 else，例如部門經理或技術支援系統管理員群組 toosomeone hello 右 toomanage hello 成員清單。</span><span class="sxs-lookup"><span data-stu-id="74754-133">hello members of hello group will be provided hello access, and hello resource owner can delegate hello right toomanage hello members list of a group toosomeone else, such as a department manager or a helpdesk administrator.</span></span>

![Azure Active Directory 存取管理圖表](./media/active-directory-access-management-groups/active-directory-access-management-works.png)

<span data-ttu-id="74754-135">hello 群組擁有者也可以讓該群組可供自助服務要求。</span><span class="sxs-lookup"><span data-stu-id="74754-135">hello owner of a group can also make that group available for self-service requests.</span></span> <span data-ttu-id="74754-136">在此情況下，使用者可以搜尋和尋找 hello 群組，以要求 toojoin，有效地搜尋透過 hello 群組所管理的權限 tooaccess hello 資源。</span><span class="sxs-lookup"><span data-stu-id="74754-136">In doing so, an end user can search for and find hello group and make a request toojoin, effectively seeking permission tooaccess hello resources that are managed through hello group.</span></span> <span data-ttu-id="74754-137">hello hello 群組擁有者可以設定 hello 群組，以便自動核准加入要求，或需要 hello 群組的 hello 擁有者核准。</span><span class="sxs-lookup"><span data-stu-id="74754-137">hello owner of hello group can set up hello group so that join requests are approved automatically or require approval by hello owner of hello group.</span></span> <span data-ttu-id="74754-138">當使用者要求 toojoin 群組，hello 聯結要求轉送 toohello hello 群組擁有者。</span><span class="sxs-lookup"><span data-stu-id="74754-138">When a user makes a request toojoin a group, hello join request is forwarded toohello owners of hello group.</span></span> <span data-ttu-id="74754-139">如果其中 hello 擁有者核准 hello 要求，hello 提出要求的使用者會收到通知，而 hello 使用者是聯結的 toohello 群組。</span><span class="sxs-lookup"><span data-stu-id="74754-139">If one of hello owners approves hello request, hello requesting user is notified and hello user is joined toohello group.</span></span> <span data-ttu-id="74754-140">如果其中 hello 擁有者拒絕 hello 要求，hello 提出要求的使用者會收到通知，但未加入 toohello 群組。</span><span class="sxs-lookup"><span data-stu-id="74754-140">If one of hello owners denies hello request, hello requesting user is notified but not joined toohello group.</span></span>

## <a name="getting-started-with-access-management"></a><span data-ttu-id="74754-141">開始使用存取管理</span><span class="sxs-lookup"><span data-stu-id="74754-141">Getting started with access management</span></span>
<span data-ttu-id="74754-142">準備好 tooget 啟動嗎？</span><span class="sxs-lookup"><span data-stu-id="74754-142">Ready tooget started?</span></span> <span data-ttu-id="74754-143">您應該嘗試一些 hello 基本的工作，您可以使用 Azure AD 群組。</span><span class="sxs-lookup"><span data-stu-id="74754-143">You should try out some of hello basic tasks you can do with Azure AD groups.</span></span> <span data-ttu-id="74754-144">使用這些功能 tooprovide 特製化存取 toodifferent 一群人的組織中不同資源。</span><span class="sxs-lookup"><span data-stu-id="74754-144">Use these capabilities tooprovide specialized access toodifferent groups of people for different resources in your organization.</span></span> <span data-ttu-id="74754-145">以下是基本的首要步驟清單。</span><span class="sxs-lookup"><span data-stu-id="74754-145">A list of basic first steps are listed below.</span></span>

* [<span data-ttu-id="74754-146">建立簡單的規則群組 tooconfigure 動態成員資格</span><span class="sxs-lookup"><span data-stu-id="74754-146">Creating a simple rule tooconfigure dynamic memberships for a group</span></span>](active-directory-accessmanagement-manage-groups.md#how-can-i-manage-the-membership-of-a-group-dynamically)
* [<span data-ttu-id="74754-147">使用群組 toomanage 存取 tooSaaS 應用程式</span><span class="sxs-lookup"><span data-stu-id="74754-147">Using a group toomanage access tooSaaS applications</span></span>](active-directory-accessmanagement-group-saasapps.md)
* [<span data-ttu-id="74754-148">提供可供一般使用者自助服務的群組</span><span class="sxs-lookup"><span data-stu-id="74754-148">Making a group available for end user self-service</span></span>](active-directory-accessmanagement-self-service-group-management.md)
* [<span data-ttu-id="74754-149">使用 Azure AD Connect 的內部群組 tooAzure 正在同步處理</span><span class="sxs-lookup"><span data-stu-id="74754-149">Syncing an on-premises group tooAzure using Azure AD Connect</span></span>](active-directory-aadconnect.md)
* [<span data-ttu-id="74754-150">管理群組的擁有者</span><span class="sxs-lookup"><span data-stu-id="74754-150">Managing owners for a group</span></span>](active-directory-accessmanagement-managing-group-owners.md)

## <a name="next-steps"></a><span data-ttu-id="74754-151">後續步驟</span><span class="sxs-lookup"><span data-stu-id="74754-151">Next steps</span></span>
<span data-ttu-id="74754-152">既然您已了解 hello 存取管理基本概念，以下是某些額外的進階的功能可用在 Azure Active Directory 中管理存取 tooyour 應用程式和資源。</span><span class="sxs-lookup"><span data-stu-id="74754-152">Now that you have understood hello basics of access management, here are some additional advanced capabilities available in Azure Active Directory for managing access tooyour applications and resources.</span></span>

* [<span data-ttu-id="74754-153">使用屬性 toocreate 進階規則</span><span class="sxs-lookup"><span data-stu-id="74754-153">Using attributes toocreate advanced rules</span></span>](active-directory-accessmanagement-groups-with-advanced-rules.md)
* [<span data-ttu-id="74754-154">在 Azure AD 中管理安全性群組</span><span class="sxs-lookup"><span data-stu-id="74754-154">Managing security groups in Azure AD</span></span>](active-directory-accessmanagement-manage-groups.md)
* [<span data-ttu-id="74754-155">在 Azure AD 中設定專用的群組</span><span class="sxs-lookup"><span data-stu-id="74754-155">Setting up dedicated groups in Azure AD</span></span>](active-directory-accessmanagement-dedicated-groups.md)
* [<span data-ttu-id="74754-156">群組的圖形 API 參考</span><span class="sxs-lookup"><span data-stu-id="74754-156">Graph API reference for groups</span></span>](https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/groups-operations#GroupFunctions)
* [<span data-ttu-id="74754-157">設定群組設定的 Azure Active Directory Cmdlet</span><span class="sxs-lookup"><span data-stu-id="74754-157">Azure Active Directory cmdlets for configuring group settings</span></span>](active-directory-accessmanagement-groups-settings-cmdlets.md)
