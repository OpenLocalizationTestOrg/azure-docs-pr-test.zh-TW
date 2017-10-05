---
title: "Azure Active Directory 混合式身分識別設計考量 - 判斷存取控制需求| Microsoft Docs"
description: "說明身分識別的要件，以及針對混合式環境中的使用者識別資源的存取需求。"
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
ms.openlocfilehash: 6404940da460461632616fe49f055d50c2a7aba3
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="determine-access-control-requirements-for-your-hybrid-identity-solution"></a><span data-ttu-id="77e19-103">判斷混合式身分識別解決方案的存取控制需求</span><span class="sxs-lookup"><span data-stu-id="77e19-103">Determine access control requirements for your hybrid identity solution</span></span>
<span data-ttu-id="77e19-104">當組織正在設計他們的混合式身分識別解決方案時，也可以利用這個機會，針對他們正規劃來讓使用者使用的資源檢閱存取需求。</span><span class="sxs-lookup"><span data-stu-id="77e19-104">When an organization is designing their hybrid identity solution they can also use this opportunity to review access requirements for the resources that they are planning to make it available for users.</span></span> <span data-ttu-id="77e19-105">您可以橫跨下列這四種身分識別要件來存取資料：</span><span class="sxs-lookup"><span data-stu-id="77e19-105">The data access cross all four pillars of identity, which are:</span></span>

* <span data-ttu-id="77e19-106">系統管理</span><span class="sxs-lookup"><span data-stu-id="77e19-106">Administration</span></span>
* <span data-ttu-id="77e19-107">驗證</span><span class="sxs-lookup"><span data-stu-id="77e19-107">Authentication</span></span>
* <span data-ttu-id="77e19-108">Authorization</span><span class="sxs-lookup"><span data-stu-id="77e19-108">Authorization</span></span>
* <span data-ttu-id="77e19-109">稽核</span><span class="sxs-lookup"><span data-stu-id="77e19-109">Auditing</span></span>

<span data-ttu-id="77e19-110">後續小節將更詳細說明驗證與授權，系統管理和稽核則是混合式身分識別週期的一部分。</span><span class="sxs-lookup"><span data-stu-id="77e19-110">The sections that follows will cover authentication and authorization in more details, administration and auditing are part of the hybrid identity lifecycle.</span></span> <span data-ttu-id="77e19-111">如需這些功能的詳細資訊，請參閱 [判斷混合式身分識別管理工作](active-directory-hybrid-identity-design-considerations-hybrid-id-management-tasks.md) 。</span><span class="sxs-lookup"><span data-stu-id="77e19-111">Read [Determine hybrid identity management tasks](active-directory-hybrid-identity-design-considerations-hybrid-id-management-tasks.md) for more information about these capabilities.</span></span>

> [!NOTE]
> <span data-ttu-id="77e19-112">如需每一個要件的詳細資訊，請參閱 [身分識別的四個要件 - 混合式 IT 使用期間的身分識別管理](http://social.technet.microsoft.com/wiki/contents/articles/15530.the-four-pillars-of-identity-identity-management-in-the-age-of-hybrid-it.aspx) 。</span><span class="sxs-lookup"><span data-stu-id="77e19-112">Read [The Four Pillars of Identity - Identity Management in the Age of Hybrid IT](http://social.technet.microsoft.com/wiki/contents/articles/15530.the-four-pillars-of-identity-identity-management-in-the-age-of-hybrid-it.aspx) for more information about each one of those pillars.</span></span>
> 
> 

## <a name="authentication-and-authorization"></a><span data-ttu-id="77e19-113">驗證和授權</span><span class="sxs-lookup"><span data-stu-id="77e19-113">Authentication and authorization</span></span>
<span data-ttu-id="77e19-114">有各種適用於驗證和授權的不同案例，這些案例將具備特殊需求，必須透過公司即將採用的混合式身分識別解決方案來滿足。</span><span class="sxs-lookup"><span data-stu-id="77e19-114">There are different scenarios for authentication and authorization, these scenarios will have specific requirements that must be fulfilled by the hybrid identity solution that the company is going to adopt.</span></span> <span data-ttu-id="77e19-115">涉及企業對企業 (B2B) 通訊的案例會對 IT 系統管理員造成額外的挑戰，因為他們需要確定組織所使用的驗證和授權方法可以和他們的商務合作夥伴進行通訊。</span><span class="sxs-lookup"><span data-stu-id="77e19-115">Scenarios involving Business to Business (B2B) communication can add an extra challenge for IT Admins since they will need to ensure that the authentication and authorization method used by the organization can communicate with their business partners.</span></span> <span data-ttu-id="77e19-116">在設計驗證和授權需求的過程中，請確定會回答下列問題：</span><span class="sxs-lookup"><span data-stu-id="77e19-116">During the designing process for authentication and authorization requirements, ensure that the following questions are answered:</span></span>

* <span data-ttu-id="77e19-117">您的組織只會驗證和授權位於其身分識別管理系統中的使用者嗎？</span><span class="sxs-lookup"><span data-stu-id="77e19-117">Will your organization authenticate and authorize only users located at their identity management system?</span></span>
  * <span data-ttu-id="77e19-118">是否有任何適用於 B2B 案例的方案？</span><span class="sxs-lookup"><span data-stu-id="77e19-118">Are there any plans for B2B scenarios?</span></span>
  * <span data-ttu-id="77e19-119">如果有，您已經知道將使用哪些通訊協定 (SAML、OAuth、Kerberos、權杖或憑證) 來連接這兩個企業嗎？</span><span class="sxs-lookup"><span data-stu-id="77e19-119">If yes, do you already know which protocols (SAML, OAuth, Kerberos, Tokens or Certificates) will be used to connect both businesses?</span></span>
* <span data-ttu-id="77e19-120">您即將採用的混合式身分識別解決方案支援這些通訊協定嗎？</span><span class="sxs-lookup"><span data-stu-id="77e19-120">Does the hybrid identity solution that you are going to adopt support those protocols?</span></span>

<span data-ttu-id="77e19-121">另一個要考量的重點是使用者和合作夥伴將使用的驗證儲存機制將位於何處以及要使用哪個系統管理模型。</span><span class="sxs-lookup"><span data-stu-id="77e19-121">Another important point to consider is where the authentication repository that will be used by users and partners will be located and the administrative model to be used.</span></span> <span data-ttu-id="77e19-122">請考量下列兩個核心選項：</span><span class="sxs-lookup"><span data-stu-id="77e19-122">Consider the following two core options:</span></span>

* <span data-ttu-id="77e19-123">集中式︰在這個模型中，使用者的認證、原則和管理可以集中於內部部署或雲端中。</span><span class="sxs-lookup"><span data-stu-id="77e19-123">Centralized: in this model the user’s credentials, policies and administration can be centralized on-premises or in the cloud.</span></span>
* <span data-ttu-id="77e19-124">混合式︰在這個模型中，使用者的認證、原則和管理會集中於內部部署和雲端複寫中。</span><span class="sxs-lookup"><span data-stu-id="77e19-124">Hybrid: in this model the user’s credentials, policies and administration will be centralized on-premises and a replicated in the cloud.</span></span>

<span data-ttu-id="77e19-125">組織將採用哪一個模型，將根據其商務需求而不同，您需要回答下列問題來識別身分識別管理系統所在的位置以及要使用的系統管理模式：</span><span class="sxs-lookup"><span data-stu-id="77e19-125">Which model your organization will adopt will vary according to their business requirements, you want to answer the following questions to identify where the identity management system will reside and the administrative mode to use:</span></span>

* <span data-ttu-id="77e19-126">您的組織目前具有內部部署的身分識別管理嗎？</span><span class="sxs-lookup"><span data-stu-id="77e19-126">Does your organization currently have an identity management on-premises?</span></span>
  * <span data-ttu-id="77e19-127">如果是，他們打算如何保留它？</span><span class="sxs-lookup"><span data-stu-id="77e19-127">If yes, do they plan to keep it?</span></span>
  * <span data-ttu-id="77e19-128">您的組織是否有任何法規或規範需求必須遵循，以指出身分識別管理系統應位於的位置？</span><span class="sxs-lookup"><span data-stu-id="77e19-128">Are there any regulation or compliance requirements that your organization must follow that dictates where the identity management system should reside?</span></span>
* <span data-ttu-id="77e19-129">您的組織會針對位於內部部署或雲端中的 app 使用單一登入嗎？</span><span class="sxs-lookup"><span data-stu-id="77e19-129">Does your organization use single sign-on for apps located on-premises or in the cloud?</span></span>
  * <span data-ttu-id="77e19-130">如果是，採用混合式身分識別模型會影響此程序嗎？</span><span class="sxs-lookup"><span data-stu-id="77e19-130">If yes, does the adoption of a hybrid identity model affect this process?</span></span>

## <a name="access-control"></a><span data-ttu-id="77e19-131">存取控制</span><span class="sxs-lookup"><span data-stu-id="77e19-131">Access Control</span></span>
<span data-ttu-id="77e19-132">儘管驗證和授權是核心元素，可透過使用者的驗證來啟用對公司資料的存取權，但是控制這些使用者將具備的存取層級，以及系統管理員在其管理的資源上具備的存取層級，也同樣重要。</span><span class="sxs-lookup"><span data-stu-id="77e19-132">While authentication and authorization are core elements to enable access to corporate data through user’s validation, it is also important to control the level of access that these users will have and the level of access administrators will have over the resources that they are managing.</span></span> <span data-ttu-id="77e19-133">您的混合式身分識別解決方案必須能夠對資源、委派和角色型存取控制提供更細微的存取權。</span><span class="sxs-lookup"><span data-stu-id="77e19-133">Your hybrid identity solution must be able to provide granular access to resources, delegation and role base access control.</span></span> <span data-ttu-id="77e19-134">請確定會回答下列有關存取控制的問題：</span><span class="sxs-lookup"><span data-stu-id="77e19-134">Ensure that the following question are answered regarding access control:</span></span>

* <span data-ttu-id="77e19-135">貴公司擁有多位已提高權限來管理您身分識別系統的使用者嗎？</span><span class="sxs-lookup"><span data-stu-id="77e19-135">Does your company have more than one user with elevated privilege to manage your identity system?</span></span>
  * <span data-ttu-id="77e19-136">如果是，每位使用者都需要同一個存取層級嗎？</span><span class="sxs-lookup"><span data-stu-id="77e19-136">If yes, does each user need the same access level?</span></span>
* <span data-ttu-id="77e19-137">貴公司需要將存取權委派給使用者來管理特定資源嗎？</span><span class="sxs-lookup"><span data-stu-id="77e19-137">Would your company need to delegate access to users to manage specific resources?</span></span>
  * <span data-ttu-id="77e19-138">如果是，這種情況發生的頻率為何？</span><span class="sxs-lookup"><span data-stu-id="77e19-138">If yes, how frequently this happens?</span></span>
* <span data-ttu-id="77e19-139">貴公司需要整合內部部署與雲端資源之間的存取控制功能嗎？</span><span class="sxs-lookup"><span data-stu-id="77e19-139">Would your company need to integrate access control capabilities between on-premises and cloud resources?</span></span>
* <span data-ttu-id="77e19-140">貴公司需要根據相同情況來限制資源的存取嗎？</span><span class="sxs-lookup"><span data-stu-id="77e19-140">Would your company need to limit access to resources according to some conditions?</span></span>
* <span data-ttu-id="77e19-141">貴公司是否有任何應用程式需要某些資源的自訂控制存取權？</span><span class="sxs-lookup"><span data-stu-id="77e19-141">Would your company have any application that needs custom control access to some resources?</span></span>
  * <span data-ttu-id="77e19-142">如果是，這些 app 位於何處 (內部部署或雲端中)？</span><span class="sxs-lookup"><span data-stu-id="77e19-142">If yes, where are those apps located (on-premises or in the cloud)?</span></span>
  * <span data-ttu-id="77e19-143">如果是，這些目標資源位於何處 (內部部署或雲端中)？</span><span class="sxs-lookup"><span data-stu-id="77e19-143">If yes, where are those target resources located (on-premises or in the cloud)?</span></span>

> [!NOTE]
> <span data-ttu-id="77e19-144">請確定會記下每個答案，並了解答案背後的原理。</span><span class="sxs-lookup"><span data-stu-id="77e19-144">Make sure to take notes of each answer and understand the rationale behind the answer.</span></span> <span data-ttu-id="77e19-145">[定義資料保護策略](active-directory-hybrid-identity-design-considerations-data-protection-strategy.md) 將介紹可用選項，以及每個選項的優點/缺點。</span><span class="sxs-lookup"><span data-stu-id="77e19-145">[Define Data Protection Strategy](active-directory-hybrid-identity-design-considerations-data-protection-strategy.md) will go over the options available and advantages/disadvantages of each option.</span></span>  <span data-ttu-id="77e19-146">回答這些問題，您就能選取最適合您業務需求的選項。</span><span class="sxs-lookup"><span data-stu-id="77e19-146">By answering those questions you will select which option best suits your business needs.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="77e19-147">後續步驟</span><span class="sxs-lookup"><span data-stu-id="77e19-147">Next steps</span></span>
[<span data-ttu-id="77e19-148">判斷事件因應需求</span><span class="sxs-lookup"><span data-stu-id="77e19-148">Determine incident response requirements</span></span>](active-directory-hybrid-identity-design-considerations-incident-response-requirements.md)

## <a name="see-also"></a><span data-ttu-id="77e19-149">另請參閱</span><span class="sxs-lookup"><span data-stu-id="77e19-149">See Also</span></span>
[<span data-ttu-id="77e19-150">設計考量概觀</span><span class="sxs-lookup"><span data-stu-id="77e19-150">Design considerations overview</span></span>](active-directory-hybrid-identity-design-considerations-overview.md)

