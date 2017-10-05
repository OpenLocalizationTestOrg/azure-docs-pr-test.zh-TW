---
title: "使用群組來管理 Azure Active Directory 中的資源存取權 | Microsoft Docs"
description: "如何使用 Azure Active Directory 中的群組來管理內部部署、雲端應用程式與資源的使用者存取權。"
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
ms.openlocfilehash: cd8125eda7643f0b190d35cbb89edf8b7b4eca30
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="manage-access-to-resources-with-azure-active-directory-groups"></a><span data-ttu-id="500a6-103">使用 Azure Active Directory 群組來管理資源的存取權</span><span class="sxs-lookup"><span data-stu-id="500a6-103">Manage access to resources with Azure Active Directory groups</span></span>
<span data-ttu-id="500a6-104">Azure Active Directory (Azure AD) 是一個身分識別與存取管理的綜合性解決方案，提供許多強大的功能來管理內部部署和雲端應用程式和資源的存取權，包括如 Office 365 的 Microsoft 線上服務，以及非 Microsoft 的 SaaS 應用程式。</span><span class="sxs-lookup"><span data-stu-id="500a6-104">Azure Active Directory (Azure AD) is a comprehensive identity and access management solution that provides a robust set of capabilities to manage access to on-premises and cloud applications and resources including Microsoft online services like Office 365 and a world of non-Microsoft SaaS applications.</span></span> <span data-ttu-id="500a6-105">本文會提供概觀，但如果您要立即開始使用 Azure AD 群組，請遵循 [在 Azure AD 中管理安全性群組](active-directory-accessmanagement-manage-groups.md)的指示。</span><span class="sxs-lookup"><span data-stu-id="500a6-105">This article provides an overview, but if you want to start using Azure AD groups right now, follow the instructions in [Managing security groups in Azure AD](active-directory-accessmanagement-manage-groups.md).</span></span> <span data-ttu-id="500a6-106">如果您想要看看如何使用 PowerShell 管理 Azure Active directory 中的群組，則可以在 [適用於群組管理的 Azure Active Directory Cmdlet](active-directory-accessmanagement-groups-settings-v2-cmdlets.md)中深入了解。</span><span class="sxs-lookup"><span data-stu-id="500a6-106">If you want to see how you can use PowerShell to manage groups in Azure Active directory you can read more in [Azure Active Directory cmdlets for group management](active-directory-accessmanagement-groups-settings-v2-cmdlets.md).</span></span>

> [!NOTE]
> <span data-ttu-id="500a6-107">若要使用 Azure Active Directory，您需要 Azure 帳戶。</span><span class="sxs-lookup"><span data-stu-id="500a6-107">To use Azure Active Directory, you need an Azure account.</span></span> <span data-ttu-id="500a6-108">如果您沒有帳戶，您可以 [註冊免費的 Azure 帳戶](https://azure.microsoft.com/pricing/free-trial/)。</span><span class="sxs-lookup"><span data-stu-id="500a6-108">If you don't have an account, you can [sign up for a free Azure account](https://azure.microsoft.com/pricing/free-trial/).</span></span>
>
>

<span data-ttu-id="500a6-109">Azure AD 的其中一項主要功能是管理資源的存取權。</span><span class="sxs-lookup"><span data-stu-id="500a6-109">Within Azure AD, one of the major features is the ability to manage access to resources.</span></span> <span data-ttu-id="500a6-110">這些資源可以是目錄的一部分，例如透過目錄中的角色或目錄外部的資源 (例如 SaaS 應用程式、Azure 服務以及 SharePoint 網站或內部部署資源) 管理物件的權限。</span><span class="sxs-lookup"><span data-stu-id="500a6-110">These resources can be part of the directory, as in the case of permissions to manage objects through roles in the directory, or resources that are external to the directory, such as SaaS applications, Azure services, and SharePoint sites or on-premises resources.</span></span> <span data-ttu-id="500a6-111">有四種方式可以指派使用者存取資源的權限：</span><span class="sxs-lookup"><span data-stu-id="500a6-111">There are four ways a user can be assigned access rights to a resource:</span></span>

1. <span data-ttu-id="500a6-112">直接指派</span><span class="sxs-lookup"><span data-stu-id="500a6-112">Direct assignment</span></span>

    <span data-ttu-id="500a6-113">資源的擁有者可以直接指派使用者存取資源。</span><span class="sxs-lookup"><span data-stu-id="500a6-113">Users can be assigned directly to a resource by the owner of that resource.</span></span>
2. <span data-ttu-id="500a6-114">群組成員資格</span><span class="sxs-lookup"><span data-stu-id="500a6-114">Group membership</span></span>

    <span data-ttu-id="500a6-115">資源擁有者可以指派群組存取資源，透過這種方式，授與該群組成員存取資源。</span><span class="sxs-lookup"><span data-stu-id="500a6-115">A group can be assigned to a resource by the resource owner, and by doing so, granting the members of that group access to the resource.</span></span> <span data-ttu-id="500a6-116">群組的擁有者就可以管理群組的成員資格。</span><span class="sxs-lookup"><span data-stu-id="500a6-116">Membership of the group can then be managed by the owner of the group.</span></span> <span data-ttu-id="500a6-117">實際上，資源擁有者是委派權限給群組的擁有者，以指派使用者存取其資源。</span><span class="sxs-lookup"><span data-stu-id="500a6-117">Effectively, the resource owner delegates the permission to assign users to their resource to the owner of the group.</span></span>
3. <span data-ttu-id="500a6-118">以規則為基礎</span><span class="sxs-lookup"><span data-stu-id="500a6-118">Rule-based</span></span>

    <span data-ttu-id="500a6-119">資源擁有者可以使用規則來表示應指派哪些使用者存取資源。</span><span class="sxs-lookup"><span data-stu-id="500a6-119">The resource owner can use a rule to express which users should be assigned access to a resource.</span></span> <span data-ttu-id="500a6-120">規則的結果取決於該規則中使用的屬性，以及針對特定使用者的值，透過這種方式，資源擁有者實際上是根據規則中所使用的屬性，委派給授權的來源來管理其資源的存取權。</span><span class="sxs-lookup"><span data-stu-id="500a6-120">The outcome of the rule depends on the attributes used in that rule and their values for specific users, and by doing so, the resource owner effectively delegates the right to manage access to their resource to the authoritative source for the attributes that are used in the rule.</span></span> <span data-ttu-id="500a6-121">資源擁有者仍可管理規則本身，並決定哪些屬性與值提供其資源的存取權。</span><span class="sxs-lookup"><span data-stu-id="500a6-121">The resource owner still manages the rule itself and determines which attributes and values provide access to their resource.</span></span>
4. <span data-ttu-id="500a6-122">外部授權單位</span><span class="sxs-lookup"><span data-stu-id="500a6-122">External authority</span></span>

    <span data-ttu-id="500a6-123">資源的存取權從外部來源衍生而來，例如從授權來源 (例如內部部署目錄或如 WorkDay 的 SaaS 應用程式) 同步處理的群組。</span><span class="sxs-lookup"><span data-stu-id="500a6-123">The access to a resource is derived from an external source; for example, a group that is synchronized from an authoritative source such as an on-premises directory or a SaaS app such as WorkDay.</span></span> <span data-ttu-id="500a6-124">資源擁有者指派群組以提供資源存取權，外部來源管理群組的成員。</span><span class="sxs-lookup"><span data-stu-id="500a6-124">The resource owner assigns the group to provide access to the resource, and the external source manages the members of the group.</span></span>

   ![存取管理圖表的概觀](./media/active-directory-access-management-groups/access-management-overview.png)

## <a name="watch-a-video-that-explains-access-management"></a><span data-ttu-id="500a6-126">觀看說明存取管理的影片</span><span class="sxs-lookup"><span data-stu-id="500a6-126">Watch a video that explains access management</span></span>
<span data-ttu-id="500a6-127">您可以在此觀賞說明與此相關的短片：</span><span class="sxs-lookup"><span data-stu-id="500a6-127">You can watch a short video that explains more about this:</span></span>

<span data-ttu-id="500a6-128">**Azure AD：群組的動態成員資格簡介**</span><span class="sxs-lookup"><span data-stu-id="500a6-128">**Azure AD: Introduction to dynamic membership for groups**</span></span>

> [!VIDEO https://channel9.msdn.com/Series/Azure-Active-Directory-Videos-Demos/Azure-AD--Introduction-to-Dynamic-Memberships-for-Groups/player]
>
>

## <a name="how-does-access-management-in-azure-active-directory-work"></a><span data-ttu-id="500a6-129">存取管理在 Azure Active Directory 中如何運作？</span><span class="sxs-lookup"><span data-stu-id="500a6-129">How does access management in Azure Active Directory work?</span></span>
<span data-ttu-id="500a6-130">Azure AD 存取管理解決方案的重點是安全性群組。</span><span class="sxs-lookup"><span data-stu-id="500a6-130">At the center of the Azure AD access management solution is the security group.</span></span> <span data-ttu-id="500a6-131">使用安全性群組來管理資源的存取權是著名的範例，方法彈性而且容易理解，可以針對想要的使用者群組提供資源的存取權。</span><span class="sxs-lookup"><span data-stu-id="500a6-131">Using a security group to manage access to resources is a well-known paradigm, which allows for a flexible and easily understood way to provide access to a resource for the intended group of users.</span></span> <span data-ttu-id="500a6-132">資源擁有者 (或目錄的系統管理員) 可以指派群組，對所擁有的資源提供特定的存取權限。</span><span class="sxs-lookup"><span data-stu-id="500a6-132">The resource owner (or the administrator of the directory) can assign a group to provide a certain access right to the resources they own.</span></span> <span data-ttu-id="500a6-133">群組的成員會取得存取權，而資源擁有者可以委派管理群組成員清單的權限給其他人，例如部門經理或技術服務管理員。</span><span class="sxs-lookup"><span data-stu-id="500a6-133">The members of the group will be provided the access, and the resource owner can delegate the right to manage the members list of a group to someone else, such as a department manager or a helpdesk administrator.</span></span>

![Azure Active Directory 存取管理圖表](./media/active-directory-access-management-groups/active-directory-access-management-works.png)

<span data-ttu-id="500a6-135">群組的擁有者也可以讓該群組供自助式服務要求使用。</span><span class="sxs-lookup"><span data-stu-id="500a6-135">The owner of a group can also make that group available for self-service requests.</span></span> <span data-ttu-id="500a6-136">如此一來，使用者可以搜尋和尋找群組並提出要求加入，就可以尋求權限以存取透過群組所管理的資源。</span><span class="sxs-lookup"><span data-stu-id="500a6-136">In doing so, an end user can search for and find the group and make a request to join, effectively seeking permission to access the resources that are managed through the group.</span></span> <span data-ttu-id="500a6-137">群組的擁有者可以設定群組，自動核准加入的要求，或者需要經過群組的擁有者核准。</span><span class="sxs-lookup"><span data-stu-id="500a6-137">The owner of the group can set up the group so that join requests are approved automatically or require approval by the owner of the group.</span></span> <span data-ttu-id="500a6-138">當使用者提出加入群組的要求時，加入要求會轉送給群組的擁有者。</span><span class="sxs-lookup"><span data-stu-id="500a6-138">When a user makes a request to join a group, the join request is forwarded to the owners of the group.</span></span> <span data-ttu-id="500a6-139">如果其中一個擁有者核准要求，提出要求的使用者會收到通知，並且加入群組。</span><span class="sxs-lookup"><span data-stu-id="500a6-139">If one of the owners approves the request, the requesting user is notified and the user is joined to the group.</span></span> <span data-ttu-id="500a6-140">如果其中一個擁有者拒絕要求，提出要求的使用者會收到通知，但不會加入群組。</span><span class="sxs-lookup"><span data-stu-id="500a6-140">If one of the owners denies the request, the requesting user is notified but not joined to the group.</span></span>

## <a name="getting-started-with-access-management"></a><span data-ttu-id="500a6-141">開始使用存取管理</span><span class="sxs-lookup"><span data-stu-id="500a6-141">Getting started with access management</span></span>
<span data-ttu-id="500a6-142">準備好開始了嗎？</span><span class="sxs-lookup"><span data-stu-id="500a6-142">Ready to get started?</span></span> <span data-ttu-id="500a6-143">您可以嘗試一些可以使用 Azure AD 群組進行的基本工作。</span><span class="sxs-lookup"><span data-stu-id="500a6-143">You should try out some of the basic tasks you can do with Azure AD groups.</span></span> <span data-ttu-id="500a6-144">使用這些功能，針對組織中的不同資源，提供特殊存取權給不同群組的人員。</span><span class="sxs-lookup"><span data-stu-id="500a6-144">Use these capabilities to provide specialized access to different groups of people for different resources in your organization.</span></span> <span data-ttu-id="500a6-145">以下是基本的首要步驟清單。</span><span class="sxs-lookup"><span data-stu-id="500a6-145">A list of basic first steps are listed below.</span></span>

* [<span data-ttu-id="500a6-146">建立簡單的規則，設定群組的動態成員資格</span><span class="sxs-lookup"><span data-stu-id="500a6-146">Creating a simple rule to configure dynamic memberships for a group</span></span>](active-directory-accessmanagement-manage-groups.md#how-can-i-manage-the-membership-of-a-group-dynamically)
* [<span data-ttu-id="500a6-147">使用群組來管理 SaaS 應用程式的存取權</span><span class="sxs-lookup"><span data-stu-id="500a6-147">Using a group to manage access to SaaS applications</span></span>](active-directory-accessmanagement-group-saasapps.md)
* [<span data-ttu-id="500a6-148">提供可供一般使用者自助服務的群組</span><span class="sxs-lookup"><span data-stu-id="500a6-148">Making a group available for end user self-service</span></span>](active-directory-accessmanagement-self-service-group-management.md)
* [<span data-ttu-id="500a6-149">使用 Azure AD Connect 將內部部署群組同步處理至 Azure</span><span class="sxs-lookup"><span data-stu-id="500a6-149">Syncing an on-premises group to Azure using Azure AD Connect</span></span>](active-directory-aadconnect.md)
* [<span data-ttu-id="500a6-150">管理群組的擁有者</span><span class="sxs-lookup"><span data-stu-id="500a6-150">Managing owners for a group</span></span>](active-directory-accessmanagement-managing-group-owners.md)

## <a name="next-steps"></a><span data-ttu-id="500a6-151">後續步驟</span><span class="sxs-lookup"><span data-stu-id="500a6-151">Next steps</span></span>
<span data-ttu-id="500a6-152">如果您已經了解存取管理的基本概念，以下是一些 Azure Active Directory 中可用的其他進階功能，可以管理您的應用程式和資源的存取權。</span><span class="sxs-lookup"><span data-stu-id="500a6-152">Now that you have understood the basics of access management, here are some additional advanced capabilities available in Azure Active Directory for managing access to your applications and resources.</span></span>

* [<span data-ttu-id="500a6-153">使用屬性來建立進階規則</span><span class="sxs-lookup"><span data-stu-id="500a6-153">Using attributes to create advanced rules</span></span>](active-directory-accessmanagement-groups-with-advanced-rules.md)
* [<span data-ttu-id="500a6-154">在 Azure AD 中管理安全性群組</span><span class="sxs-lookup"><span data-stu-id="500a6-154">Managing security groups in Azure AD</span></span>](active-directory-accessmanagement-manage-groups.md)
* [<span data-ttu-id="500a6-155">在 Azure AD 中設定專用的群組</span><span class="sxs-lookup"><span data-stu-id="500a6-155">Setting up dedicated groups in Azure AD</span></span>](active-directory-accessmanagement-dedicated-groups.md)
* [<span data-ttu-id="500a6-156">群組的圖形 API 參考</span><span class="sxs-lookup"><span data-stu-id="500a6-156">Graph API reference for groups</span></span>](https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/groups-operations#GroupFunctions)
* [<span data-ttu-id="500a6-157">設定群組設定的 Azure Active Directory Cmdlet</span><span class="sxs-lookup"><span data-stu-id="500a6-157">Azure Active Directory cmdlets for configuring group settings</span></span>](active-directory-accessmanagement-groups-settings-cmdlets.md)
