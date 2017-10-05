---
title: "什麼是 Azure Active Directory 中的群組型授權？ | Microsoft Docs"
description: "描述 Azure Active Directory 群組型授權、如何運作以及最佳做法"
services: active-directory
keywords: "Azure AD 授權"
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: 
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 06/29/2017
ms.author: curtand
ms.reviewer: piotrci
ms.custom: H1Hack27Feb2017;it-pro
ms.openlocfilehash: 52dd48ce4e4acaf48f31edc51bbb657f8cd249cd
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="group-based-licensing-basics-in-azure-active-directory"></a><span data-ttu-id="b449c-105">Azure Active Directory 中以群組為基礎的授權基本概念</span><span class="sxs-lookup"><span data-stu-id="b449c-105">Group-based licensing basics in Azure Active Directory</span></span>

<span data-ttu-id="b449c-106">使用 Microsoft 付費雲端服務 (例如 Office 365、Enterprise Mobility + Security、Dynamics CRM 及其他類似的產品) 需要授權。</span><span class="sxs-lookup"><span data-stu-id="b449c-106">Using Microsoft paid cloud services, such as Office 365, Enterprise Mobility + Security, Dynamics CRM, and other similar products, requires licenses.</span></span> <span data-ttu-id="b449c-107">這些授權指派給每位需要存取這些服務的使用者。</span><span class="sxs-lookup"><span data-stu-id="b449c-107">These licenses are assigned to each user who needs access to these services.</span></span> <span data-ttu-id="b449c-108">若要管理授權，系統管理員需要使用其中一個管理入口網站 (Office 或 Azure) 和 PowerShell Cmdlet。</span><span class="sxs-lookup"><span data-stu-id="b449c-108">To manage licenses, administrators use one of the management portals (Office or Azure) and PowerShell cmdlets.</span></span> <span data-ttu-id="b449c-109">Azure Active Directory (Azure AD) 是支援所有 Microsoft 雲端服務身分識別管理的基礎結構。</span><span class="sxs-lookup"><span data-stu-id="b449c-109">Azure Active Directory (Azure AD) is the underlying infrastructure that supports identity management for all Microsoft cloud services.</span></span> <span data-ttu-id="b449c-110">Azure AD 會儲存使用者授權指派狀態的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="b449c-110">Azure AD stores information about license assignment states for users.</span></span>

<span data-ttu-id="b449c-111">到目前為止，只能在個別使用者等級指派授權，因此難以進行大規模的管理。</span><span class="sxs-lookup"><span data-stu-id="b449c-111">Until now, licenses could only be assigned at the individual user level, which can make large-scale management difficult.</span></span> <span data-ttu-id="b449c-112">例如，若要根據組織變更 (例如使用者加入或離開組織或部門) 來新增或移除使用者授權，系統管理員通常必須撰寫複雜的 PowerShell 指令碼。</span><span class="sxs-lookup"><span data-stu-id="b449c-112">For example, to add or remove user licenses based on organizational changes, such as users joining or leaving the organization or a department, an administrator often must write a complex PowerShell script.</span></span> <span data-ttu-id="b449c-113">此指令碼會對雲端服務進行個別的呼叫。</span><span class="sxs-lookup"><span data-stu-id="b449c-113">This script makes individual calls to the cloud service.</span></span>

<span data-ttu-id="b449c-114">為了克服這些挑戰，Azure AD 現在包含群組型授權。</span><span class="sxs-lookup"><span data-stu-id="b449c-114">To address those challenges, Azure AD now includes group-based licensing.</span></span> <span data-ttu-id="b449c-115">您可以將一或多個產品授權指派給群組。</span><span class="sxs-lookup"><span data-stu-id="b449c-115">You can assign one or more product licenses to a group.</span></span> <span data-ttu-id="b449c-116">Azure AD 會確保將授權指派給該群組的所有成員。</span><span class="sxs-lookup"><span data-stu-id="b449c-116">Azure AD ensures that the licenses are assigned to all members of the group.</span></span> <span data-ttu-id="b449c-117">任何加入群組的新成員會獲派適當的授權。</span><span class="sxs-lookup"><span data-stu-id="b449c-117">Any new members who join the group are assigned the appropriate licenses.</span></span> <span data-ttu-id="b449c-118">當他們離開群組時，就會移除這些授權。</span><span class="sxs-lookup"><span data-stu-id="b449c-118">When they leave the group, those licenses are removed.</span></span> <span data-ttu-id="b449c-119">如此一來，不需透過 PowerShell 來自動管理授權，即可依據每一使用者反映組織和部門結構中的變更。</span><span class="sxs-lookup"><span data-stu-id="b449c-119">This eliminates the need for automating license management via PowerShell to reflect changes in the organization and departmental structure on a per-user basis.</span></span>

## <a name="features"></a><span data-ttu-id="b449c-120">特性</span><span class="sxs-lookup"><span data-stu-id="b449c-120">Features</span></span>

<span data-ttu-id="b449c-121">以下是群組型授權的主要特色：</span><span class="sxs-lookup"><span data-stu-id="b449c-121">Here are the main features of group-based licensing:</span></span>

- <span data-ttu-id="b449c-122">可將授權指派給 Azure AD 中的任何安全性群組。</span><span class="sxs-lookup"><span data-stu-id="b449c-122">Licenses can be assigned to any security group in Azure AD.</span></span> <span data-ttu-id="b449c-123">內部部署可以使用 Azure AD Connect 來同步處理安全性群組。</span><span class="sxs-lookup"><span data-stu-id="b449c-123">Security groups can be synced on-premises, by using Azure AD Connect.</span></span> <span data-ttu-id="b449c-124">您也可以直接在 Azure AD 中建立安全性群組 (也稱為僅限雲端的群組)，或透過 Azure AD 動態群組功能自動建立安全性群組。</span><span class="sxs-lookup"><span data-stu-id="b449c-124">You can also create security groups directly in Azure AD (also called cloud-only groups), or automatically via the Azure AD dynamic group feature.</span></span>

- <span data-ttu-id="b449c-125">將產品授權指派給群組時，系統管理員可以停用該產品中的一或多個服務方案。</span><span class="sxs-lookup"><span data-stu-id="b449c-125">When a product license is assigned to a group, the administrator can disable one or more service plans in the product.</span></span> <span data-ttu-id="b449c-126">通常是在組織尚未準備好開始使用產品中的服務時，才會這樣做。</span><span class="sxs-lookup"><span data-stu-id="b449c-126">Typically, this is done when the organization is not yet ready to start using a service included in a product.</span></span> <span data-ttu-id="b449c-127">比方說，系統管理員可能將 Office 365 指派給某個部門，但暫時停用 Yammer 服務。</span><span class="sxs-lookup"><span data-stu-id="b449c-127">For example, the administrator might assign Office 365 to a department, but temporarily disable the Yammer service.</span></span>

- <span data-ttu-id="b449c-128">支援所有需要使用者層級授權的 Microsoft 雲端服務。</span><span class="sxs-lookup"><span data-stu-id="b449c-128">All Microsoft cloud services that require user-level licensing are supported.</span></span> <span data-ttu-id="b449c-129">這包括所有 Office 365 產品、Enterprise Mobility + Security 和 Dynamics CRM。</span><span class="sxs-lookup"><span data-stu-id="b449c-129">This includes all Office 365 products, Enterprise Mobility + Security, and Dynamics CRM.</span></span>

- <span data-ttu-id="b449c-130">群組型授權目前僅透過 [Azure 入口網站](https://portal.azure.com)提供。</span><span class="sxs-lookup"><span data-stu-id="b449c-130">Group-based licensing is currently available only through [the Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="b449c-131">如果您原本就使用其他管理入口網站來管理使用者和群組，例如 Office 365 入口網站，您可以繼續這樣做。</span><span class="sxs-lookup"><span data-stu-id="b449c-131">If you primarily use other management portals for user and group management, such as the Office 365 portal, you can continue to do so.</span></span> <span data-ttu-id="b449c-132">但是，若要在群組等級管理授權，您應該使用 Azure 入口網站。</span><span class="sxs-lookup"><span data-stu-id="b449c-132">But you should use the Azure portal to manage licenses at group level.</span></span>

- <span data-ttu-id="b449c-133">Azure AD 會自動管理因群組成員資格變更而產生的授權修改。</span><span class="sxs-lookup"><span data-stu-id="b449c-133">Azure AD automatically manages license modifications that result from group membership changes.</span></span> <span data-ttu-id="b449c-134">一般而言，在成員資格變更後的幾分鐘內，授權修改就會生效。</span><span class="sxs-lookup"><span data-stu-id="b449c-134">Typically, license modifications are effective within minutes of a membership change.</span></span>

- <span data-ttu-id="b449c-135">一個使用者可以屬於多個已指定授權原則的群組。</span><span class="sxs-lookup"><span data-stu-id="b449c-135">A user can be a member of multiple groups with license policies specified.</span></span> <span data-ttu-id="b449c-136">使用者也可以有一些直接從任何群組之外指派的授權。</span><span class="sxs-lookup"><span data-stu-id="b449c-136">A user can also have some licenses that were directly assigned, outside of any groups.</span></span> <span data-ttu-id="b449c-137">產生的使用者狀態是所有已指派之產品與服務授權的組合。</span><span class="sxs-lookup"><span data-stu-id="b449c-137">The resulting user state is a combination of all assigned product and service licenses.</span></span>

- <span data-ttu-id="b449c-138">在某些情況下，授權無法指派給使用者。</span><span class="sxs-lookup"><span data-stu-id="b449c-138">In some cases, licenses cannot be assigned to a user.</span></span> <span data-ttu-id="b449c-139">比方說，租用戶可能沒有足夠可用的授權，或可能同時指派衝突的服務。</span><span class="sxs-lookup"><span data-stu-id="b449c-139">For example, there might not be enough available licenses in the tenant, or conflicting services might have been assigned at the same time.</span></span> <span data-ttu-id="b449c-140">對於 Azure AD 無法完整處理群組授權的使用者，系統管理員可以存取這些使用者的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="b449c-140">Administrators have access to information about users for whom Azure AD could not fully process group licenses.</span></span> <span data-ttu-id="b449c-141">然後，他們可以根據該資訊採取更正動作。</span><span class="sxs-lookup"><span data-stu-id="b449c-141">They can then take corrective action based on that information.</span></span>

- <span data-ttu-id="b449c-142">在公開預覽期間，租用戶中必須要有 Azure AD Basic 或 Premium 版本的付費或試用訂用帳戶，才能使用群組型授權管理。</span><span class="sxs-lookup"><span data-stu-id="b449c-142">During public preview, a paid or trial subscription for Azure AD Basic or Premium editions is required in the tenant to use group-based license management.</span></span>

## <a name="next-steps"></a><span data-ttu-id="b449c-143">後續步驟</span><span class="sxs-lookup"><span data-stu-id="b449c-143">Next steps</span></span>

<span data-ttu-id="b449c-144">若要深入了解透過群組型授權來管理授權的其他案例，請參閱：</span><span class="sxs-lookup"><span data-stu-id="b449c-144">To learn more about other scenarios for license management through group-based licensing, see:</span></span>

* [<span data-ttu-id="b449c-145">在 Azure Active Directory 中開始使用授權</span><span class="sxs-lookup"><span data-stu-id="b449c-145">Get started with licenses in Azure Active Directory</span></span>](active-directory-licensing-get-started-azure-portal.md)
* [<span data-ttu-id="b449c-146">將授權指派給 Azure Active Directory 中的群組</span><span class="sxs-lookup"><span data-stu-id="b449c-146">Assigning licenses to a group in Azure Active Directory</span></span>](active-directory-licensing-group-assignment-azure-portal.md)
* [<span data-ttu-id="b449c-147">識別及解決 Azure Active Directory 中群組的授權問題</span><span class="sxs-lookup"><span data-stu-id="b449c-147">Identifying and resolving license problems for a group in Azure Active Directory</span></span>](active-directory-licensing-group-problem-resolution-azure-portal.md)
* [<span data-ttu-id="b449c-148">如何將個別的已授權使用者移轉成 Azure Active Directory 中的群組型授權 (英文)</span><span class="sxs-lookup"><span data-stu-id="b449c-148">How to migrate individual licensed users to group-based licensing in Azure Active Directory</span></span>](active-directory-licensing-group-migration-azure-portal.md)
* [<span data-ttu-id="b449c-149">Azure Active Directory 群組型授權其他案例 (英文)</span><span class="sxs-lookup"><span data-stu-id="b449c-149">Azure Active Directory group-based licensing additional scenarios</span></span>](active-directory-licensing-group-advanced.md)
