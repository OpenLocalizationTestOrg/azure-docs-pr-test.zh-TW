---
title: "aaaWhat 是以群組為基礎來授權 Azure Active Directory 中？ | Microsoft Docs"
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
ms.openlocfilehash: 11647de6b76022cd2393751fcafc67ce671aeba6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="group-based-licensing-basics-in-azure-active-directory"></a><span data-ttu-id="ac498-105">Azure Active Directory 中以群組為基礎的授權基本概念</span><span class="sxs-lookup"><span data-stu-id="ac498-105">Group-based licensing basics in Azure Active Directory</span></span>

<span data-ttu-id="ac498-106">使用 Microsoft 付費雲端服務 (例如 Office 365、Enterprise Mobility + Security、Dynamics CRM 及其他類似的產品) 需要授權。</span><span class="sxs-lookup"><span data-stu-id="ac498-106">Using Microsoft paid cloud services, such as Office 365, Enterprise Mobility + Security, Dynamics CRM, and other similar products, requires licenses.</span></span> <span data-ttu-id="ac498-107">這些授權指派給需要存取 toothese 服務 tooeach 使用者。</span><span class="sxs-lookup"><span data-stu-id="ac498-107">These licenses are assigned tooeach user who needs access toothese services.</span></span> <span data-ttu-id="ac498-108">toomanage 授權，系統管理員使用其中一個 hello 管理入口網站 （Office 或 Azure） 和 PowerShell 指令程式。</span><span class="sxs-lookup"><span data-stu-id="ac498-108">toomanage licenses, administrators use one of hello management portals (Office or Azure) and PowerShell cmdlets.</span></span> <span data-ttu-id="ac498-109">Azure Active Directory (Azure AD) 是 hello 支援所有的 Microsoft 雲端服務的身分識別管理的基礎結構。</span><span class="sxs-lookup"><span data-stu-id="ac498-109">Azure Active Directory (Azure AD) is hello underlying infrastructure that supports identity management for all Microsoft cloud services.</span></span> <span data-ttu-id="ac498-110">Azure AD 會儲存使用者授權指派狀態的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="ac498-110">Azure AD stores information about license assignment states for users.</span></span>

<span data-ttu-id="ac498-111">到目前為止，授權只能在 hello 個別使用者層級，它可能會造成大規模管理困難指派。</span><span class="sxs-lookup"><span data-stu-id="ac498-111">Until now, licenses could only be assigned at hello individual user level, which can make large-scale management difficult.</span></span> <span data-ttu-id="ac498-112">例如，根據組織的變更，例如使用者加入或離開 hello 組織或部門的 tooadd 或移除使用者授權，系統管理員通常必須撰寫複雜的 PowerShell 指令碼。</span><span class="sxs-lookup"><span data-stu-id="ac498-112">For example, tooadd or remove user licenses based on organizational changes, such as users joining or leaving hello organization or a department, an administrator often must write a complex PowerShell script.</span></span> <span data-ttu-id="ac498-113">此指令碼可讓個別呼叫 toohello 雲端服務。</span><span class="sxs-lookup"><span data-stu-id="ac498-113">This script makes individual calls toohello cloud service.</span></span>

<span data-ttu-id="ac498-114">tooaddress 所面臨的挑戰，Azure AD 現在包含群組為基礎的授權。</span><span class="sxs-lookup"><span data-stu-id="ac498-114">tooaddress those challenges, Azure AD now includes group-based licensing.</span></span> <span data-ttu-id="ac498-115">您可以指派一或多個產品授權 tooa 群組。</span><span class="sxs-lookup"><span data-stu-id="ac498-115">You can assign one or more product licenses tooa group.</span></span> <span data-ttu-id="ac498-116">Azure AD 可確保 hello 授權指派 tooall hello 群組成員。</span><span class="sxs-lookup"><span data-stu-id="ac498-116">Azure AD ensures that hello licenses are assigned tooall members of hello group.</span></span> <span data-ttu-id="ac498-117">加入 hello 群組的任何新成員指派 hello 適當授權。</span><span class="sxs-lookup"><span data-stu-id="ac498-117">Any new members who join hello group are assigned hello appropriate licenses.</span></span> <span data-ttu-id="ac498-118">當它們離開 hello 群組時，會移除這些授權。</span><span class="sxs-lookup"><span data-stu-id="ac498-118">When they leave hello group, those licenses are removed.</span></span> <span data-ttu-id="ac498-119">這樣會排除 hello 需要自動化透過 PowerShell tooreflect 變更 hello 組織與部門的結構，每個使用者為基礎的授權管理。</span><span class="sxs-lookup"><span data-stu-id="ac498-119">This eliminates hello need for automating license management via PowerShell tooreflect changes in hello organization and departmental structure on a per-user basis.</span></span>

## <a name="features"></a><span data-ttu-id="ac498-120">特性</span><span class="sxs-lookup"><span data-stu-id="ac498-120">Features</span></span>

<span data-ttu-id="ac498-121">以下是以群組為基礎授權的 hello 主要功能：</span><span class="sxs-lookup"><span data-stu-id="ac498-121">Here are hello main features of group-based licensing:</span></span>

- <span data-ttu-id="ac498-122">授權可以 tooany 安全性群組指派 Azure AD 中。</span><span class="sxs-lookup"><span data-stu-id="ac498-122">Licenses can be assigned tooany security group in Azure AD.</span></span> <span data-ttu-id="ac498-123">內部部署可以使用 Azure AD Connect 來同步處理安全性群組。</span><span class="sxs-lookup"><span data-stu-id="ac498-123">Security groups can be synced on-premises, by using Azure AD Connect.</span></span> <span data-ttu-id="ac498-124">直接在 Azure AD （也稱為僅限雲端的群組），或自動透過 hello Azure AD 動態群組功能，您也可以建立安全性群組。</span><span class="sxs-lookup"><span data-stu-id="ac498-124">You can also create security groups directly in Azure AD (also called cloud-only groups), or automatically via hello Azure AD dynamic group feature.</span></span>

- <span data-ttu-id="ac498-125">當產品的授權指派 tooa 群組時，hello 系統管理員可以停用 hello 產品中的一個或多個服務方案。</span><span class="sxs-lookup"><span data-stu-id="ac498-125">When a product license is assigned tooa group, hello administrator can disable one or more service plans in hello product.</span></span> <span data-ttu-id="ac498-126">一般而言，這是當尚未使用的產品中納入服務準備好 toostart hello 組織。</span><span class="sxs-lookup"><span data-stu-id="ac498-126">Typically, this is done when hello organization is not yet ready toostart using a service included in a product.</span></span> <span data-ttu-id="ac498-127">例如，hello 系統管理員可能會指派 Office 365 tooa 部門，但暫時停用 hello Yammer 服務。</span><span class="sxs-lookup"><span data-stu-id="ac498-127">For example, hello administrator might assign Office 365 tooa department, but temporarily disable hello Yammer service.</span></span>

- <span data-ttu-id="ac498-128">支援所有需要使用者層級授權的 Microsoft 雲端服務。</span><span class="sxs-lookup"><span data-stu-id="ac498-128">All Microsoft cloud services that require user-level licensing are supported.</span></span> <span data-ttu-id="ac498-129">這包括所有 Office 365 產品、Enterprise Mobility + Security 和 Dynamics CRM。</span><span class="sxs-lookup"><span data-stu-id="ac498-129">This includes all Office 365 products, Enterprise Mobility + Security, and Dynamics CRM.</span></span>

- <span data-ttu-id="ac498-130">群組為基礎的授權其目前只能透過[hello Azure 入口網站](https://portal.azure.com)。</span><span class="sxs-lookup"><span data-stu-id="ac498-130">Group-based licensing is currently available only through [hello Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="ac498-131">如果您主要是使用其他管理入口網站為使用者與群組管理，例如 hello Office 365 入口網站中，您可以繼續 toodo 因此。</span><span class="sxs-lookup"><span data-stu-id="ac498-131">If you primarily use other management portals for user and group management, such as hello Office 365 portal, you can continue toodo so.</span></span> <span data-ttu-id="ac498-132">但是，您應該使用 hello Azure 入口網站 toomanage 授權在群組層級。</span><span class="sxs-lookup"><span data-stu-id="ac498-132">But you should use hello Azure portal toomanage licenses at group level.</span></span>

- <span data-ttu-id="ac498-133">Azure AD 會自動管理因群組成員資格變更而產生的授權修改。</span><span class="sxs-lookup"><span data-stu-id="ac498-133">Azure AD automatically manages license modifications that result from group membership changes.</span></span> <span data-ttu-id="ac498-134">一般而言，在成員資格變更後的幾分鐘內，授權修改就會生效。</span><span class="sxs-lookup"><span data-stu-id="ac498-134">Typically, license modifications are effective within minutes of a membership change.</span></span>

- <span data-ttu-id="ac498-135">一個使用者可以屬於多個已指定授權原則的群組。</span><span class="sxs-lookup"><span data-stu-id="ac498-135">A user can be a member of multiple groups with license policies specified.</span></span> <span data-ttu-id="ac498-136">使用者也可以有一些直接從任何群組之外指派的授權。</span><span class="sxs-lookup"><span data-stu-id="ac498-136">A user can also have some licenses that were directly assigned, outside of any groups.</span></span> <span data-ttu-id="ac498-137">產生使用者狀態的 hello 是所有指派的產品和服務授權的組合。</span><span class="sxs-lookup"><span data-stu-id="ac498-137">hello resulting user state is a combination of all assigned product and service licenses.</span></span>

- <span data-ttu-id="ac498-138">在某些情況下，授權不能指派 tooa 使用者。</span><span class="sxs-lookup"><span data-stu-id="ac498-138">In some cases, licenses cannot be assigned tooa user.</span></span> <span data-ttu-id="ac498-139">例如，在 hello 租用戶不可能有足夠的可用授權或衝突的服務可能已指派給 hello 在相同的時間。</span><span class="sxs-lookup"><span data-stu-id="ac498-139">For example, there might not be enough available licenses in hello tenant, or conflicting services might have been assigned at hello same time.</span></span> <span data-ttu-id="ac498-140">系統管理員具有存取 tooinformation 有關針對 Azure AD 無法完整處理群組授權的使用者。</span><span class="sxs-lookup"><span data-stu-id="ac498-140">Administrators have access tooinformation about users for whom Azure AD could not fully process group licenses.</span></span> <span data-ttu-id="ac498-141">然後，他們可以根據該資訊採取更正動作。</span><span class="sxs-lookup"><span data-stu-id="ac498-141">They can then take corrective action based on that information.</span></span>

- <span data-ttu-id="ac498-142">公用預覽期間，Azure AD Basic 或 Premium edition 的付費或試用訂用帳戶需要在 hello 租用戶 toouse 群組為基礎的授權管理。</span><span class="sxs-lookup"><span data-stu-id="ac498-142">During public preview, a paid or trial subscription for Azure AD Basic or Premium editions is required in hello tenant toouse group-based license management.</span></span>

## <a name="next-steps"></a><span data-ttu-id="ac498-143">後續步驟</span><span class="sxs-lookup"><span data-stu-id="ac498-143">Next steps</span></span>

<span data-ttu-id="ac498-144">toolearn 有關透過群組為基礎授權的授權管理的其他案例的詳細資訊，請參閱：</span><span class="sxs-lookup"><span data-stu-id="ac498-144">toolearn more about other scenarios for license management through group-based licensing, see:</span></span>

* [<span data-ttu-id="ac498-145">在 Azure Active Directory 中開始使用授權</span><span class="sxs-lookup"><span data-stu-id="ac498-145">Get started with licenses in Azure Active Directory</span></span>](active-directory-licensing-get-started-azure-portal.md)
* [<span data-ttu-id="ac498-146">Azure Active Directory 中指派的授權 tooa 群組</span><span class="sxs-lookup"><span data-stu-id="ac498-146">Assigning licenses tooa group in Azure Active Directory</span></span>](active-directory-licensing-group-assignment-azure-portal.md)
* [<span data-ttu-id="ac498-147">識別及解決 Azure Active Directory 中群組的授權問題</span><span class="sxs-lookup"><span data-stu-id="ac498-147">Identifying and resolving license problems for a group in Azure Active Directory</span></span>](active-directory-licensing-group-problem-resolution-azure-portal.md)
* [<span data-ttu-id="ac498-148">如何 toomigrate 個別授權 toogroup 型授權 Azure Active Directory 中的使用者</span><span class="sxs-lookup"><span data-stu-id="ac498-148">How toomigrate individual licensed users toogroup-based licensing in Azure Active Directory</span></span>](active-directory-licensing-group-migration-azure-portal.md)
* [<span data-ttu-id="ac498-149">Azure Active Directory 群組型授權其他案例 (英文)</span><span class="sxs-lookup"><span data-stu-id="ac498-149">Azure Active Directory group-based licensing additional scenarios</span></span>](active-directory-licensing-group-advanced.md)
