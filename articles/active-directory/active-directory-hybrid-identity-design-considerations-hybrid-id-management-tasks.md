---
title: "Azure Active Directory 混合式身分識別設計考量 - 判斷混合式身分識別管理工作|Microsoft Docs"
description: "透過條件式存取控制，Azure Active Directory 會在驗證使用者時以及允許存取應用程式之前，檢查您挑選的特定條件。 一旦符合這些條件，就會驗證使用者並允許存取應用程式。"
documentationcenter: 
services: active-directory
author: billmath
manager: femila
editor: 
ms.assetid: 65f80aea-0426-4072-83e1-faf5b76df034
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/18/2017
ms.author: billmath
ms.openlocfilehash: 921c8391fc18eca35d10c3ade158a98ae88df397
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="plan-for-hybrid-identity-lifecycle"></a><span data-ttu-id="a54b7-104">規劃混合式身分識別生命週期</span><span class="sxs-lookup"><span data-stu-id="a54b7-104">Plan for Hybrid Identity Lifecycle</span></span>
<span data-ttu-id="a54b7-105">身分識別是企業行動力和應用程式存取策略的基礎之一。</span><span class="sxs-lookup"><span data-stu-id="a54b7-105">Identity is one of the foundations of your enterprise mobility and application access strategy.</span></span> <span data-ttu-id="a54b7-106">無論您登入行動裝置還是 SaaS 應用程式，您的身分識別都是您能否進行存取的關鍵。</span><span class="sxs-lookup"><span data-stu-id="a54b7-106">Whether you are signing on to your mobile device or SaaS app, your identity is the key to gaining access to everything.</span></span> <span data-ttu-id="a54b7-107">在其最高層級上，身分識別管理解決方案牽涉到儲存機制的統合和同步，而其中又包含佈建資源程序的自動化和集中化。</span><span class="sxs-lookup"><span data-stu-id="a54b7-107">At its highest level, an identity management solution encompasses unifying and syncing between your identity repositories which includes automating and centralizing the process of provisioning resources.</span></span> <span data-ttu-id="a54b7-108">身分識別解決方案應為跨內部部署與雲端的集中式身分識別功能，且應使用某種形式的身分識別同盟，以維護集中式驗證，並且安全地與外部使用者和企業進行共用和共同作業。</span><span class="sxs-lookup"><span data-stu-id="a54b7-108">The identity solution should be a centralized identity across on-premises and cloud and also use some form of identity federation to maintain centralized authentication and securely share and collaborate with external users and businesses.</span></span> <span data-ttu-id="a54b7-109">資源的範圍涵蓋作業系統和應用程式，乃至於組織中或隸屬於組織的人員。</span><span class="sxs-lookup"><span data-stu-id="a54b7-109">Resources range from operating systems and applications to people in, or affiliated with, an organization.</span></span> <span data-ttu-id="a54b7-110">組織結構可以改變，以因應佈建原則和程序。</span><span class="sxs-lookup"><span data-stu-id="a54b7-110">Organizational structure can be altered to accommodate the provisioning policies and procedures.</span></span>

<span data-ttu-id="a54b7-111">為您的使用者提供身分識別解決方案，使其體驗自助式服務以提升能力進而保持生產力，是很重要的。</span><span class="sxs-lookup"><span data-stu-id="a54b7-111">It is also important to have an identity solution geared to empower your users by providing them with self-service experiences to keep them productive.</span></span> <span data-ttu-id="a54b7-112">您的身分識別解決方案若能讓使用者在其需要存取的所有資源層級上進行的所有資源層級，將會更加健全。系統管理員可在各個層級上使用標準化程序來管理使用者認證。</span><span class="sxs-lookup"><span data-stu-id="a54b7-112">Your identity solution is more robust if it enables single sign-on for users across all the resources they need access Administrators at all levels can use standardized procedures for managing user credentials.</span></span> <span data-ttu-id="a54b7-113">視佈建管理解決方案的範圍之不同，某些層級的管理可以減少或排除。</span><span class="sxs-lookup"><span data-stu-id="a54b7-113">Some levels of administration can be reduced or eliminated, depending on the breadth of the provisioning management solution.</span></span> <span data-ttu-id="a54b7-114">此外，您可以安全地在不同組織之間散發管理功能，手動或自動皆可。</span><span class="sxs-lookup"><span data-stu-id="a54b7-114">Furthermore, you can securely distribute administration capabilities, manually or automatically, among various organizations.</span></span> <span data-ttu-id="a54b7-115">例如，網域管理員只能為該網域中的人員和資源提供服務。</span><span class="sxs-lookup"><span data-stu-id="a54b7-115">For example, a domain administrator can serve only the people and resources in that domain.</span></span> <span data-ttu-id="a54b7-116">這名使用者可以執行管理和佈建工作，但無權執行組態工作，例如建立工作流程。</span><span class="sxs-lookup"><span data-stu-id="a54b7-116">This user can do administrative and provisioning tasks, but is not authorized to do configuration tasks, such as creating workflows.</span></span>

## <a name="determine-hybrid-identity-management-tasks"></a><span data-ttu-id="a54b7-117">判斷混合式身分識別管理工作</span><span class="sxs-lookup"><span data-stu-id="a54b7-117">Determine Hybrid Identity Management Tasks</span></span>
<span data-ttu-id="a54b7-118">在您的組織中散發管理工作，可以改善管理的精確度和效率，並改善組織的工作負載平衡。</span><span class="sxs-lookup"><span data-stu-id="a54b7-118">Distributing administrative tasks in your organization improves the accuracy and effectiveness of administration and improves the balance of the workload of an organization.</span></span> <span data-ttu-id="a54b7-119">以下是定義健全的身分識別管理系統的要點。</span><span class="sxs-lookup"><span data-stu-id="a54b7-119">Following are the pivots that define a robust identity management system.</span></span>

 ![](./media/hybrid-id-design-considerations/Identity_management_considerations.png)

<span data-ttu-id="a54b7-120">若要定義混合式身分識別管理工作，您必須了解將採用混合式身分識別的組織有哪些基本特性。</span><span class="sxs-lookup"><span data-stu-id="a54b7-120">To define hybrid identity management tasks, you must understand some essential characteristics of the organization that will be adopting hybrid identity.</span></span> <span data-ttu-id="a54b7-121">請務必了解目前要用於身分識別來源的儲存機制。</span><span class="sxs-lookup"><span data-stu-id="a54b7-121">It is important to understand the current repositories being used for identity sources.</span></span> <span data-ttu-id="a54b7-122">了解這些核心元素之後，將可得知您的基本需求，據此，您必須提出更細微的問題，進而為您的身分識別解決方案引導出更理想的設計決策。</span><span class="sxs-lookup"><span data-stu-id="a54b7-122">By knowing those core elements, you will have the foundational requirements and based on that you will need to ask more granular questions that will lead you to a better design decision for your Identity solution.</span></span>  

<span data-ttu-id="a54b7-123">定義這些需求時，至少要回答下列問題</span><span class="sxs-lookup"><span data-stu-id="a54b7-123">While defining those requirements, ensure that at least the following questions are answered</span></span>

* <span data-ttu-id="a54b7-124">佈建選項：</span><span class="sxs-lookup"><span data-stu-id="a54b7-124">Provisioning options:</span></span> 
  
  * <span data-ttu-id="a54b7-125">混合式身分識別解決方案是否支援健全的帳戶存取管理和佈建系統？</span><span class="sxs-lookup"><span data-stu-id="a54b7-125">Does the hybrid identity solution support a robust account access management and provisioning system?</span></span>
  * <span data-ttu-id="a54b7-126">使用者、群組和密碼將以何種方式受到管理？</span><span class="sxs-lookup"><span data-stu-id="a54b7-126">How are users, groups, and passwords going to be managed?</span></span>
  * <span data-ttu-id="a54b7-127">身分識別生命週期管理是否有因應能力？</span><span class="sxs-lookup"><span data-stu-id="a54b7-127">Is the identity lifecycle management responsive?</span></span> 
    * <span data-ttu-id="a54b7-128">密碼更新的帳戶暫止需要多久的時間？</span><span class="sxs-lookup"><span data-stu-id="a54b7-128">How long does password updates account suspension take?</span></span>
* <span data-ttu-id="a54b7-129">授權管理：</span><span class="sxs-lookup"><span data-stu-id="a54b7-129">License management:</span></span> 
  
  * <span data-ttu-id="a54b7-130">混合式身分識別解決方案是否會處理授權管理？</span><span class="sxs-lookup"><span data-stu-id="a54b7-130">Does the hybrid identity solution handles license management?</span></span>
    * <span data-ttu-id="a54b7-131">如果是，可用的功能為何？</span><span class="sxs-lookup"><span data-stu-id="a54b7-131">If yes, what capabilities are available?</span></span>
* <span data-ttu-id="a54b7-132">解決方案是否會處理以群組為基礎的授權管理？</span><span class="sxs-lookup"><span data-stu-id="a54b7-132">Does the solution handle group-based license management?</span></span> 
  
      - <span data-ttu-id="a54b7-133">如果是，是否可以將安全性群組指派給它？</span><span class="sxs-lookup"><span data-stu-id="a54b7-133">If yes, is it possible to assign a security group to it?</span></span> 
       - <span data-ttu-id="a54b7-134">如果是，雲端目錄是否會自動將授權指派給群組的所有成員？</span><span class="sxs-lookup"><span data-stu-id="a54b7-134">If yes, will the cloud directory automatically assign licenses to all the members of the group?</span></span> 
        - <span data-ttu-id="a54b7-135">如果後續在群組中新增或移除使用者，將會有何情況？會適當地自動指派或移除授權嗎？</span><span class="sxs-lookup"><span data-stu-id="a54b7-135">What happens if a user is subsequently added to, or removed from the group, will a license be automatically assigned or removed as appropriate?</span></span> 
* <span data-ttu-id="a54b7-136">與其他協力廠商身分識別提供者整合：</span><span class="sxs-lookup"><span data-stu-id="a54b7-136">Integration with other third-party identity providers:</span></span>
* <span data-ttu-id="a54b7-137">此混合式解決方案是否可與協力廠商身分識別提供者整合，以實作單一登入？</span><span class="sxs-lookup"><span data-stu-id="a54b7-137">Can this hybrid solution be integrated with third-party identity providers to implement single sign-on?</span></span>
* <span data-ttu-id="a54b7-138">是否可將所有不同的身分識別提供者統合到一致的身分識別系統中？</span><span class="sxs-lookup"><span data-stu-id="a54b7-138">Is it possible to unify all the different identity providers into a cohesive identity system?</span></span>
* <span data-ttu-id="a54b7-139">如果是，有哪些系統？如何執行？可用的功能為何？</span><span class="sxs-lookup"><span data-stu-id="a54b7-139">If yes, how and which are they and what capabilities are available?</span></span>

## <a name="synchronization-management"></a><span data-ttu-id="a54b7-140">同步處理管理</span><span class="sxs-lookup"><span data-stu-id="a54b7-140">Synchronization Management</span></span>
<span data-ttu-id="a54b7-141">身分識別管理員的目標之一，是要能夠啟用所有身分識別提供者，並保持其同步處理狀態。</span><span class="sxs-lookup"><span data-stu-id="a54b7-141">One of the goals of an identity manager, to be able to bring all the identity providers and keep them synchronized.</span></span> <span data-ttu-id="a54b7-142">您可以根據授權的主要身分識別提供者，保持資料的同步處理狀態。</span><span class="sxs-lookup"><span data-stu-id="a54b7-142">You keep the data synchronized based on an authoritative master identity provider.</span></span> <span data-ttu-id="a54b7-143">在混合式身分識別案例中，您可以透過同步處理的管理模型，在內部部署伺服器中管理所有的使用者和裝置身分識別，並將帳戶同步處理至雲端 (和選擇性地同步處理密碼)。</span><span class="sxs-lookup"><span data-stu-id="a54b7-143">In a hybrid identity scenario, with a synchronized management model, you manage all user and device identities in an on-premises server and synchronize the accounts and, optionally, passwords to the cloud.</span></span> <span data-ttu-id="a54b7-144">使用者在內部部署中輸入的密碼與雲端相同，且在登入時，身分識別解決方案會驗證密碼。</span><span class="sxs-lookup"><span data-stu-id="a54b7-144">The user enters the same password on-premises as he or she does in the cloud, and at sign-in, the password is verified by the identity solution.</span></span> <span data-ttu-id="a54b7-145">此模型會使用目錄同步處理工具。</span><span class="sxs-lookup"><span data-stu-id="a54b7-145">This model uses a directory synchronization tool.</span></span>

<span data-ttu-id="a54b7-146">![](./media/hybrid-id-design-considerations/Directory_synchronization.png) 若要適當設計混合式身分識別解決方案的同步處理，請確實回答下列問題：•    有哪些可供混合式身分識別解決方案使用的同步處理解決方案？</span><span class="sxs-lookup"><span data-stu-id="a54b7-146">![](./media/hybrid-id-design-considerations/Directory_synchronization.png) To proper design the synchronization of your hybrid identity solution ensure that the following questions are answered: •    What are the sync solutions available for the hybrid identity solution?</span></span>
<span data-ttu-id="a54b7-147">•    有哪些可用的單一登入功能？</span><span class="sxs-lookup"><span data-stu-id="a54b7-147">•    What are the single sign on capabilities available?</span></span>
<span data-ttu-id="a54b7-148">•    B2B 與 B2C 之間有哪些身分識別同盟選項？</span><span class="sxs-lookup"><span data-stu-id="a54b7-148">•    What are the options for identity federation between B2B and B2C?</span></span>

## <a name="next-steps"></a><span data-ttu-id="a54b7-149">後續步驟</span><span class="sxs-lookup"><span data-stu-id="a54b7-149">Next steps</span></span>
[<span data-ttu-id="a54b7-150">判斷混合式身分識別管理採用策略</span><span class="sxs-lookup"><span data-stu-id="a54b7-150">Determine hybrid identity management adoption strategy</span></span>](active-directory-hybrid-identity-design-considerations-lifecycle-adoption-strategy.md)

## <a name="see-also"></a><span data-ttu-id="a54b7-151">另請參閱</span><span class="sxs-lookup"><span data-stu-id="a54b7-151">See Also</span></span>
[<span data-ttu-id="a54b7-152">設計考量概觀</span><span class="sxs-lookup"><span data-stu-id="a54b7-152">Design considerations overview</span></span>](active-directory-hybrid-identity-design-considerations-overview.md)

