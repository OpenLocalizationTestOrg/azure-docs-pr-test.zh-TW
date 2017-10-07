---
title: "aaaAzure Active Directory 混合式身分識別設計考量-決定混合式身分識別管理工作 |Microsoft 文件"
description: "條件式存取控制與 Azure Active Directory 檢查 hello 您挑選驗證 hello 使用者時，才能允許存取 toohello 應用程式特定的條件。 一旦符合這些條件，hello 使用者已驗證，而且允許存取 toohello 應用程式。"
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
ms.openlocfilehash: d3c0e9b23f43127b3d8e0b3a4e8f03d4bc148c27
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="plan-for-hybrid-identity-lifecycle"></a><span data-ttu-id="691b2-104">規劃混合式身分識別生命週期</span><span class="sxs-lookup"><span data-stu-id="691b2-104">Plan for Hybrid Identity Lifecycle</span></span>
<span data-ttu-id="691b2-105">身分識別是其中一個 hello 基礎的企業行動性和應用程式存取策略。</span><span class="sxs-lookup"><span data-stu-id="691b2-105">Identity is one of hello foundations of your enterprise mobility and application access strategy.</span></span> <span data-ttu-id="691b2-106">您已登入 tooyour 行動裝置或 SaaS 應用程式，您的身分識別 hello 金鑰 toogaining 存取 tooeverything。</span><span class="sxs-lookup"><span data-stu-id="691b2-106">Whether you are signing on tooyour mobile device or SaaS app, your identity is hello key toogaining access tooeverything.</span></span> <span data-ttu-id="691b2-107">在其最高的層級身分識別管理解決方案包含整合和您的身分識別儲存機制包括自動化及集中 hello 的佈建資源的程序之間的同步處理。</span><span class="sxs-lookup"><span data-stu-id="691b2-107">At its highest level, an identity management solution encompasses unifying and syncing between your identity repositories which includes automating and centralizing hello process of provisioning resources.</span></span> <span data-ttu-id="691b2-108">hello 身分識別解決方案應該是跨內部部署與雲端之間的集中式身分識別也使用某種形式的識別身分同盟 toomaintain 集中式驗證和安全地共用以及與外部使用者和企業共同作業。</span><span class="sxs-lookup"><span data-stu-id="691b2-108">hello identity solution should be a centralized identity across on-premises and cloud and also use some form of identity federation toomaintain centralized authentication and securely share and collaborate with external users and businesses.</span></span> <span data-ttu-id="691b2-109">資源的範圍從作業系統和應用程式 toopeople 中，或與組織相關。</span><span class="sxs-lookup"><span data-stu-id="691b2-109">Resources range from operating systems and applications toopeople in, or affiliated with, an organization.</span></span> <span data-ttu-id="691b2-110">改變的 tooaccommodate hello 佈建原則和程序，可以是組織結構。</span><span class="sxs-lookup"><span data-stu-id="691b2-110">Organizational structure can be altered tooaccommodate hello provisioning policies and procedures.</span></span>

<span data-ttu-id="691b2-111">很重要，因為 toohave 身分識別解決方案專 tooempower 使用者藉由提供它們與自助發生 tookeep 它們生產力。</span><span class="sxs-lookup"><span data-stu-id="691b2-111">It is also important toohave an identity solution geared tooempower your users by providing them with self-service experiences tookeep them productive.</span></span> <span data-ttu-id="691b2-112">您的身分識別解決方案是更強固的層級如果單一登入的使用者可讓所有 hello 資源需要完全存取系統管理員可以使用標準化的程序來管理使用者認證。</span><span class="sxs-lookup"><span data-stu-id="691b2-112">Your identity solution is more robust if it enables single sign-on for users across all hello resources they need access Administrators at all levels can use standardized procedures for managing user credentials.</span></span> <span data-ttu-id="691b2-113">某些層級的系統管理可以減少或消除，視佈建管理解決方案的 hello hello 範圍而定。</span><span class="sxs-lookup"><span data-stu-id="691b2-113">Some levels of administration can be reduced or eliminated, depending on hello breadth of hello provisioning management solution.</span></span> <span data-ttu-id="691b2-114">此外，您可以安全地在不同組織之間散發管理功能，手動或自動皆可。</span><span class="sxs-lookup"><span data-stu-id="691b2-114">Furthermore, you can securely distribute administration capabilities, manually or automatically, among various organizations.</span></span> <span data-ttu-id="691b2-115">例如，網域系統管理員可以做只有 hello 人和該網域中的資源。</span><span class="sxs-lookup"><span data-stu-id="691b2-115">For example, a domain administrator can serve only hello people and resources in that domain.</span></span> <span data-ttu-id="691b2-116">此使用者可以執行系統管理和佈建的工作，但未獲授權的 toodo 設定工作，例如建立工作流程。</span><span class="sxs-lookup"><span data-stu-id="691b2-116">This user can do administrative and provisioning tasks, but is not authorized toodo configuration tasks, such as creating workflows.</span></span>

## <a name="determine-hybrid-identity-management-tasks"></a><span data-ttu-id="691b2-117">判斷混合式身分識別管理工作</span><span class="sxs-lookup"><span data-stu-id="691b2-117">Determine Hybrid Identity Management Tasks</span></span>
<span data-ttu-id="691b2-118">分配給組織中的系統管理工作可改善 hello 精確度和效率的系統管理，並改善 hello 組織的 hello 工作負載平衡。</span><span class="sxs-lookup"><span data-stu-id="691b2-118">Distributing administrative tasks in your organization improves hello accuracy and effectiveness of administration and improves hello balance of hello workload of an organization.</span></span> <span data-ttu-id="691b2-119">以下是 hello 樞紐分析表定義強固的身分識別管理系統。</span><span class="sxs-lookup"><span data-stu-id="691b2-119">Following are hello pivots that define a robust identity management system.</span></span>

 ![](./media/hybrid-id-design-considerations/Identity_management_considerations.png)

<span data-ttu-id="691b2-120">toodefine 混合式身分識別管理工作，您必須了解將會採用混合式身分識別的 hello 組織的一些重要特性。</span><span class="sxs-lookup"><span data-stu-id="691b2-120">toodefine hybrid identity management tasks, you must understand some essential characteristics of hello organization that will be adopting hybrid identity.</span></span> <span data-ttu-id="691b2-121">它是用於識別來源的重要 toounderstand hello 目前機制。</span><span class="sxs-lookup"><span data-stu-id="691b2-121">It is important toounderstand hello current repositories being used for identity sources.</span></span> <span data-ttu-id="691b2-122">知道的核心項目，會有 hello 基本需求，並根據您將需要 tooask 更細微問題，導致您的身分識別解決方案 tooa 更好的設計決策。</span><span class="sxs-lookup"><span data-stu-id="691b2-122">By knowing those core elements, you will have hello foundational requirements and based on that you will need tooask more granular questions that will lead you tooa better design decision for your Identity solution.</span></span>  

<span data-ttu-id="691b2-123">在定義這些需求，請確定 ，至少 hello 下列問題</span><span class="sxs-lookup"><span data-stu-id="691b2-123">While defining those requirements, ensure that at least hello following questions are answered</span></span>

* <span data-ttu-id="691b2-124">佈建選項：</span><span class="sxs-lookup"><span data-stu-id="691b2-124">Provisioning options:</span></span> 
  
  * <span data-ttu-id="691b2-125">Hello 混合式身分識別解決方案是否支援強固的帳戶存取管理和佈建的系統？</span><span class="sxs-lookup"><span data-stu-id="691b2-125">Does hello hybrid identity solution support a robust account access management and provisioning system?</span></span>
  * <span data-ttu-id="691b2-126">有使用者、 群組及移 toobe 受管理的密碼？</span><span class="sxs-lookup"><span data-stu-id="691b2-126">How are users, groups, and passwords going toobe managed?</span></span>
  * <span data-ttu-id="691b2-127">是否有回應 hello 身分識別生命週期管理？</span><span class="sxs-lookup"><span data-stu-id="691b2-127">Is hello identity lifecycle management responsive?</span></span> 
    * <span data-ttu-id="691b2-128">密碼更新的帳戶暫止需要多久的時間？</span><span class="sxs-lookup"><span data-stu-id="691b2-128">How long does password updates account suspension take?</span></span>
* <span data-ttu-id="691b2-129">授權管理：</span><span class="sxs-lookup"><span data-stu-id="691b2-129">License management:</span></span> 
  
  * <span data-ttu-id="691b2-130">沒有 hello 混合式身分識別管理解決方案，處理授權？</span><span class="sxs-lookup"><span data-stu-id="691b2-130">Does hello hybrid identity solution handles license management?</span></span>
    * <span data-ttu-id="691b2-131">如果是，可用的功能為何？</span><span class="sxs-lookup"><span data-stu-id="691b2-131">If yes, what capabilities are available?</span></span>
* <span data-ttu-id="691b2-132">沒有 hello 控點群組為基礎的授權管理解決方案嗎？</span><span class="sxs-lookup"><span data-stu-id="691b2-132">Does hello solution handle group-based license management?</span></span> 
  
      - <span data-ttu-id="691b2-133">如果是，是否有可能 tooassign 安全性群組 tooit？</span><span class="sxs-lookup"><span data-stu-id="691b2-133">If yes, is it possible tooassign a security group tooit?</span></span> 
       - <span data-ttu-id="691b2-134">如果是，將 hello 雲端目錄自動指派授權 tooall hello 群組成員的 hello？</span><span class="sxs-lookup"><span data-stu-id="691b2-134">If yes, will hello cloud directory automatically assign licenses tooall hello members of hello group?</span></span> 
        - <span data-ttu-id="691b2-135">如果隨後加入，或從 hello 群組中移除使用者，將授權會自動指派或移除依適當情況，會發生什麼事？</span><span class="sxs-lookup"><span data-stu-id="691b2-135">What happens if a user is subsequently added to, or removed from hello group, will a license be automatically assigned or removed as appropriate?</span></span> 
* <span data-ttu-id="691b2-136">與其他協力廠商身分識別提供者整合：</span><span class="sxs-lookup"><span data-stu-id="691b2-136">Integration with other third-party identity providers:</span></span>
* <span data-ttu-id="691b2-137">可與協力廠商身分識別提供者 tooimplement 單一登入整合此混合式解決方案？</span><span class="sxs-lookup"><span data-stu-id="691b2-137">Can this hybrid solution be integrated with third-party identity providers tooimplement single sign-on?</span></span>
* <span data-ttu-id="691b2-138">它是可能 toounify 所有 hello 凝聚的身分識別系統的不同的身分識別提供者嗎？</span><span class="sxs-lookup"><span data-stu-id="691b2-138">Is it possible toounify all hello different identity providers into a cohesive identity system?</span></span>
* <span data-ttu-id="691b2-139">如果是，有哪些系統？如何執行？可用的功能為何？</span><span class="sxs-lookup"><span data-stu-id="691b2-139">If yes, how and which are they and what capabilities are available?</span></span>

## <a name="synchronization-management"></a><span data-ttu-id="691b2-140">同步處理管理</span><span class="sxs-lookup"><span data-stu-id="691b2-140">Synchronization Management</span></span>
<span data-ttu-id="691b2-141">其中一個 identity manager toobe 無法 toobring hello 目標所有 hello 身分識別提供者，並讓它們保持同步。</span><span class="sxs-lookup"><span data-stu-id="691b2-141">One of hello goals of an identity manager, toobe able toobring all hello identity providers and keep them synchronized.</span></span> <span data-ttu-id="691b2-142">保留 hello 資料同步處理基礎授權的主要身分識別提供者。</span><span class="sxs-lookup"><span data-stu-id="691b2-142">You keep hello data synchronized based on an authoritative master identity provider.</span></span> <span data-ttu-id="691b2-143">在混合式身分識別案例中，使用同步處理的管理模型時，您要管理內部部署伺服器中的所有使用者和裝置身分識別，並同步處理 hello 帳戶以及 （選擇性） 密碼 toohello 雲端。</span><span class="sxs-lookup"><span data-stu-id="691b2-143">In a hybrid identity scenario, with a synchronized management model, you manage all user and device identities in an on-premises server and synchronize hello accounts and, optionally, passwords toohello cloud.</span></span> <span data-ttu-id="691b2-144">hello 使用者輸入相同的密碼在內部部署與他或她在 hello 雲端和 hello 密碼登入經過 hello 身分識別解決方案的 hello。</span><span class="sxs-lookup"><span data-stu-id="691b2-144">hello user enters hello same password on-premises as he or she does in hello cloud, and at sign-in, hello password is verified by hello identity solution.</span></span> <span data-ttu-id="691b2-145">此模型會使用目錄同步處理工具。</span><span class="sxs-lookup"><span data-stu-id="691b2-145">This model uses a directory synchronization tool.</span></span>

<span data-ttu-id="691b2-146">![](./media/hybrid-id-design-considerations/Directory_synchronization.png)tooproper 混合式身分識別解決方案的設計 hello 同步處理，確保會回答下列問題的 hello: • 供 hello 混合式身分識別解決方案的 hello 同步方案為何？</span><span class="sxs-lookup"><span data-stu-id="691b2-146">![](./media/hybrid-id-design-considerations/Directory_synchronization.png) tooproper design hello synchronization of your hybrid identity solution ensure that hello following questions are answered: •    What are hello sync solutions available for hello hybrid identity solution?</span></span>
<span data-ttu-id="691b2-147">• 為何 hello 單一登上可用的功能嗎？</span><span class="sxs-lookup"><span data-stu-id="691b2-147">•    What are hello single sign on capabilities available?</span></span>
<span data-ttu-id="691b2-148">• B2B 和 B2C 之間的識別身分同盟的 hello 選項為何？</span><span class="sxs-lookup"><span data-stu-id="691b2-148">•    What are hello options for identity federation between B2B and B2C?</span></span>

## <a name="next-steps"></a><span data-ttu-id="691b2-149">後續步驟</span><span class="sxs-lookup"><span data-stu-id="691b2-149">Next steps</span></span>
[<span data-ttu-id="691b2-150">判斷混合式身分識別管理採用策略</span><span class="sxs-lookup"><span data-stu-id="691b2-150">Determine hybrid identity management adoption strategy</span></span>](active-directory-hybrid-identity-design-considerations-lifecycle-adoption-strategy.md)

## <a name="see-also"></a><span data-ttu-id="691b2-151">另請參閱</span><span class="sxs-lookup"><span data-stu-id="691b2-151">See Also</span></span>
[<span data-ttu-id="691b2-152">設計考量概觀</span><span class="sxs-lookup"><span data-stu-id="691b2-152">Design considerations overview</span></span>](active-directory-hybrid-identity-design-considerations-overview.md)

