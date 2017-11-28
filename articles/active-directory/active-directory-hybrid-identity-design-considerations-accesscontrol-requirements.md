---
title: "aaaAzure Active Directory 混合式身分識別設計考量-決定存取控制需求 |Microsoft 文件"
description: "涵蓋 hello 識別及資源的混合式環境中的使用者識別的存取需求的功能。"
documentationcenter: 
services: active-directory
author: billmath
manager: femila
editor: 
ms.assetid: e3b3b984-0d15-4654-93be-a396324b9f5e
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/18/2017
ms.author: billmath
ms.openlocfilehash: f0c22629f732a4c13ee7a24456651bec7637c387
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="determine-access-control-requirements-for-your-hybrid-identity-solution"></a><span data-ttu-id="64b2f-103">判斷混合式身分識別解決方案的存取控制需求</span><span class="sxs-lookup"><span data-stu-id="64b2f-103">Determine access control requirements for your hybrid identity solution</span></span>
<span data-ttu-id="64b2f-104">他們也可以使用這個機會 tooreview 其混合式身分識別解決方案設計的組織時存取這些計劃 toomake hello 資源的需求適用於使用者它。</span><span class="sxs-lookup"><span data-stu-id="64b2f-104">When an organization is designing their hybrid identity solution they can also use this opportunity tooreview access requirements for hello resources that they are planning toomake it available for users.</span></span> <span data-ttu-id="64b2f-105">hello 資料存取跨所有的四大身分識別，也就是：</span><span class="sxs-lookup"><span data-stu-id="64b2f-105">hello data access cross all four pillars of identity, which are:</span></span>

* <span data-ttu-id="64b2f-106">系統管理</span><span class="sxs-lookup"><span data-stu-id="64b2f-106">Administration</span></span>
* <span data-ttu-id="64b2f-107">驗證</span><span class="sxs-lookup"><span data-stu-id="64b2f-107">Authentication</span></span>
* <span data-ttu-id="64b2f-108">Authorization</span><span class="sxs-lookup"><span data-stu-id="64b2f-108">Authorization</span></span>
* <span data-ttu-id="64b2f-109">稽核</span><span class="sxs-lookup"><span data-stu-id="64b2f-109">Auditing</span></span>

<span data-ttu-id="64b2f-110">遵循的 hello 各節將說明如何驗證和授權的詳細資訊，管理和稽核 hello 混合式身分識別生命週期的一部分。</span><span class="sxs-lookup"><span data-stu-id="64b2f-110">hello sections that follows will cover authentication and authorization in more details, administration and auditing are part of hello hybrid identity lifecycle.</span></span> <span data-ttu-id="64b2f-111">如需這些功能的詳細資訊，請參閱 [判斷混合式身分識別管理工作](active-directory-hybrid-identity-design-considerations-hybrid-id-management-tasks.md) 。</span><span class="sxs-lookup"><span data-stu-id="64b2f-111">Read [Determine hybrid identity management tasks](active-directory-hybrid-identity-design-considerations-hybrid-id-management-tasks.md) for more information about these capabilities.</span></span>

> [!NOTE]
> <span data-ttu-id="64b2f-112">讀取[hello 四個核心的身分識別-hello 的混合式 IT 中的身分識別管理](http://social.technet.microsoft.com/wiki/contents/articles/15530.the-four-pillars-of-identity-identity-management-in-the-age-of-hybrid-it.aspx)如需每個這些功能的詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="64b2f-112">Read [hello Four Pillars of Identity - Identity Management in hello Age of Hybrid IT](http://social.technet.microsoft.com/wiki/contents/articles/15530.the-four-pillars-of-identity-identity-management-in-the-age-of-hybrid-it.aspx) for more information about each one of those pillars.</span></span>
> 
> 

## <a name="authentication-and-authorization"></a><span data-ttu-id="64b2f-113">驗證和授權</span><span class="sxs-lookup"><span data-stu-id="64b2f-113">Authentication and authorization</span></span>
<span data-ttu-id="64b2f-114">有不同的案例進行驗證和授權，這些案例會有必須滿足於 hello 公司是進行 tooadopt hello 混合式身分識別解決方案的特定需求。</span><span class="sxs-lookup"><span data-stu-id="64b2f-114">There are different scenarios for authentication and authorization, these scenarios will have specific requirements that must be fulfilled by hello hybrid identity solution that hello company is going tooadopt.</span></span> <span data-ttu-id="64b2f-115">案例涉及商務 tooBusiness (B2B) 通訊可以加入其他的挑戰 IT 系統管理員因為他們仍須先 tooensure hello 組織所使用的 hello 驗證和授權方法能夠與其商務合作夥伴進行通訊。</span><span class="sxs-lookup"><span data-stu-id="64b2f-115">Scenarios involving Business tooBusiness (B2B) communication can add an extra challenge for IT Admins since they will need tooensure that hello authentication and authorization method used by hello organization can communicate with their business partners.</span></span> <span data-ttu-id="64b2f-116">在 hello 設計驗證和授權需求的程序，請確定會回答下列問題的 hello:</span><span class="sxs-lookup"><span data-stu-id="64b2f-116">During hello designing process for authentication and authorization requirements, ensure that hello following questions are answered:</span></span>

* <span data-ttu-id="64b2f-117">您的組織只會驗證和授權位於其身分識別管理系統中的使用者嗎？</span><span class="sxs-lookup"><span data-stu-id="64b2f-117">Will your organization authenticate and authorize only users located at their identity management system?</span></span>
  * <span data-ttu-id="64b2f-118">是否有任何適用於 B2B 案例的方案？</span><span class="sxs-lookup"><span data-stu-id="64b2f-118">Are there any plans for B2B scenarios?</span></span>
  * <span data-ttu-id="64b2f-119">如果是，您已經知道哪些通訊協定 （SAML、 OAuth、 Kerberos、 語彙基元或憑證） 將會使用的 tooconnect 這兩個企業嗎？</span><span class="sxs-lookup"><span data-stu-id="64b2f-119">If yes, do you already know which protocols (SAML, OAuth, Kerberos, Tokens or Certificates) will be used tooconnect both businesses?</span></span>
* <span data-ttu-id="64b2f-120">您即將 tooadopt hello 混合式身分識別解決方案是否支援這些通訊協定？</span><span class="sxs-lookup"><span data-stu-id="64b2f-120">Does hello hybrid identity solution that you are going tooadopt support those protocols?</span></span>

<span data-ttu-id="64b2f-121">另一個重要的點 tooconsider 是即將放置 hello 驗證儲存機制，供使用者和合作夥伴和 hello 系統管理模型 toobe 使用。</span><span class="sxs-lookup"><span data-stu-id="64b2f-121">Another important point tooconsider is where hello authentication repository that will be used by users and partners will be located and hello administrative model toobe used.</span></span> <span data-ttu-id="64b2f-122">請考慮下列兩個核心選項 hello:</span><span class="sxs-lookup"><span data-stu-id="64b2f-122">Consider hello following two core options:</span></span>

* <span data-ttu-id="64b2f-123">集中式： 在此模型 hello 中使用者的認證、 原則和管理可集中於內部或 hello 雲端中。</span><span class="sxs-lookup"><span data-stu-id="64b2f-123">Centralized: in this model hello user’s credentials, policies and administration can be centralized on-premises or in hello cloud.</span></span>
* <span data-ttu-id="64b2f-124">混合式： 在此模型 hello 使用者的認證、 原則和管理會集中於內部，而且複寫 hello 雲端中。</span><span class="sxs-lookup"><span data-stu-id="64b2f-124">Hybrid: in this model hello user’s credentials, policies and administration will be centralized on-premises and a replicated in hello cloud.</span></span>

<span data-ttu-id="64b2f-125">您的組織將採用哪一個模型而異相應 tootheir 商務需求，要遵循問題 tooidentify hello 身分識別管理系統將會位於而 hello 系統管理模式 toouse tooanswer hello:</span><span class="sxs-lookup"><span data-stu-id="64b2f-125">Which model your organization will adopt will vary according tootheir business requirements, you want tooanswer hello following questions tooidentify where hello identity management system will reside and hello administrative mode toouse:</span></span>

* <span data-ttu-id="64b2f-126">您的組織目前具有內部部署的身分識別管理嗎？</span><span class="sxs-lookup"><span data-stu-id="64b2f-126">Does your organization currently have an identity management on-premises?</span></span>
  * <span data-ttu-id="64b2f-127">如果是，是否在計劃 tookeep 它？</span><span class="sxs-lookup"><span data-stu-id="64b2f-127">If yes, do they plan tookeep it?</span></span>
  * <span data-ttu-id="64b2f-128">是否有任何法規或規範需求，您的組織必須遵循該指定應放 hello 身分識別管理系統？</span><span class="sxs-lookup"><span data-stu-id="64b2f-128">Are there any regulation or compliance requirements that your organization must follow that dictates where hello identity management system should reside?</span></span>
* <span data-ttu-id="64b2f-129">沒有您的組織使用單一登入應用程式位於內部部署或 hello 雲端中嗎？</span><span class="sxs-lookup"><span data-stu-id="64b2f-129">Does your organization use single sign-on for apps located on-premises or in hello cloud?</span></span>
  * <span data-ttu-id="64b2f-130">如果是，並使用混合式身分識別模型的 hello 採用會影響此程序？</span><span class="sxs-lookup"><span data-stu-id="64b2f-130">If yes, does hello adoption of a hybrid identity model affect this process?</span></span>

## <a name="access-control"></a><span data-ttu-id="64b2f-131">存取控制</span><span class="sxs-lookup"><span data-stu-id="64b2f-131">Access Control</span></span>
<span data-ttu-id="64b2f-132">雖然驗證和授權的核心項目 tooenable 存取 toocorporate 資料透過使用者的驗證，也很重要的 toocontrol hello 的這些使用者將擁有而且 hello 層級的存取 」 系統管理員必須透過 hello 存取層級他們所管理的資源。</span><span class="sxs-lookup"><span data-stu-id="64b2f-132">While authentication and authorization are core elements tooenable access toocorporate data through user’s validation, it is also important toocontrol hello level of access that these users will have and hello level of access administrators will have over hello resources that they are managing.</span></span> <span data-ttu-id="64b2f-133">您的混合式身分識別解決方案必須能夠 tooprovide 細微的存取權 tooresources，委派和以角色為基礎的存取控制。</span><span class="sxs-lookup"><span data-stu-id="64b2f-133">Your hybrid identity solution must be able tooprovide granular access tooresources, delegation and role base access control.</span></span> <span data-ttu-id="64b2f-134">請確定該 hello 下列問題會回答關於存取控制：</span><span class="sxs-lookup"><span data-stu-id="64b2f-134">Ensure that hello following question are answered regarding access control:</span></span>

* <span data-ttu-id="64b2f-135">您的公司有多個使用者提高權限 toomanage 與身分識別系統嗎？</span><span class="sxs-lookup"><span data-stu-id="64b2f-135">Does your company have more than one user with elevated privilege toomanage your identity system?</span></span>
  * <span data-ttu-id="64b2f-136">如果每位使用者是，需要 hello 相同存取層級嗎？</span><span class="sxs-lookup"><span data-stu-id="64b2f-136">If yes, does each user need hello same access level?</span></span>
* <span data-ttu-id="64b2f-137">將您的公司需要 toodelegate 存取 toousers toomanage 特定的資源嗎？</span><span class="sxs-lookup"><span data-stu-id="64b2f-137">Would your company need toodelegate access toousers toomanage specific resources?</span></span>
  * <span data-ttu-id="64b2f-138">如果是，這種情況發生的頻率為何？</span><span class="sxs-lookup"><span data-stu-id="64b2f-138">If yes, how frequently this happens?</span></span>
* <span data-ttu-id="64b2f-139">您的公司需要 toointegrate 存取控制功能，在內部部署和雲端之間的資源嗎？</span><span class="sxs-lookup"><span data-stu-id="64b2f-139">Would your company need toointegrate access control capabilities between on-premises and cloud resources?</span></span>
* <span data-ttu-id="64b2f-140">您的公司需要 toolimit 存取 tooresources 根據 toosome 條件嗎？</span><span class="sxs-lookup"><span data-stu-id="64b2f-140">Would your company need toolimit access tooresources according toosome conditions?</span></span>
* <span data-ttu-id="64b2f-141">您的公司會有任何應用程式需要自訂控制項存取 toosome 資源嗎？</span><span class="sxs-lookup"><span data-stu-id="64b2f-141">Would your company have any application that needs custom control access toosome resources?</span></span>
  * <span data-ttu-id="64b2f-142">如果是，這些應用程式位置 (在內部部署或雲端 hello)？</span><span class="sxs-lookup"><span data-stu-id="64b2f-142">If yes, where are those apps located (on-premises or in hello cloud)?</span></span>
  * <span data-ttu-id="64b2f-143">如果是，其中是那些目標資源位於 (在內部部署或雲端 hello)？</span><span class="sxs-lookup"><span data-stu-id="64b2f-143">If yes, where are those target resources located (on-premises or in hello cloud)?</span></span>

> [!NOTE]
> <span data-ttu-id="64b2f-144">請確定每個答案 tootake 附註，並了解 hello 回應 hello 背後的基本原理。</span><span class="sxs-lookup"><span data-stu-id="64b2f-144">Make sure tootake notes of each answer and understand hello rationale behind hello answer.</span></span> <span data-ttu-id="64b2f-145">[定義的資料保護策略](active-directory-hybrid-identity-design-considerations-data-protection-strategy.md)將介紹可用 hello 選項以及每個選項的優點/缺點。</span><span class="sxs-lookup"><span data-stu-id="64b2f-145">[Define Data Protection Strategy](active-directory-hybrid-identity-design-considerations-data-protection-strategy.md) will go over hello options available and advantages/disadvantages of each option.</span></span>  <span data-ttu-id="64b2f-146">回答這些問題，您就能選取最適合您業務需求的選項。</span><span class="sxs-lookup"><span data-stu-id="64b2f-146">By answering those questions you will select which option best suits your business needs.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="64b2f-147">後續步驟</span><span class="sxs-lookup"><span data-stu-id="64b2f-147">Next steps</span></span>
[<span data-ttu-id="64b2f-148">判斷事件因應需求</span><span class="sxs-lookup"><span data-stu-id="64b2f-148">Determine incident response requirements</span></span>](active-directory-hybrid-identity-design-considerations-incident-response-requirements.md)

## <a name="see-also"></a><span data-ttu-id="64b2f-149">另請參閱</span><span class="sxs-lookup"><span data-stu-id="64b2f-149">See Also</span></span>
[<span data-ttu-id="64b2f-150">設計考量概觀</span><span class="sxs-lookup"><span data-stu-id="64b2f-150">Design considerations overview</span></span>](active-directory-hybrid-identity-design-considerations-overview.md)

