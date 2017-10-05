---
title: "Azure Active Directory 混合式身分識別設計考量 - 判斷身分識別需求 | Microsoft Docs"
description: "識別公司的商務需求，以引導您定義混合式身分識別設計的需求。"
documentationcenter: 
services: active-directory
author: billmath
manager: femila
editor: 
ms.assetid: de690978-84ef-41ad-9dfe-785722d343a1
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/18/2017
ms.author: billmath
ms.openlocfilehash: 6503034b3f5a17a2a42338c73329eef0b01f2f27
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="determine-identity-requirements-for-your-hybrid-identity-solution"></a><span data-ttu-id="81eaf-103">判斷混合式身分識別解決方案的身分識別需求</span><span class="sxs-lookup"><span data-stu-id="81eaf-103">Determine identity requirements for your hybrid identity solution</span></span>
<span data-ttu-id="81eaf-104">設計混合式身分識別解決方案的第一個步驟，是判斷將運用此解決方案的企業組織有何需求。</span><span class="sxs-lookup"><span data-stu-id="81eaf-104">The first step in designing a hybrid identity solution is to determine the requirements for the business organization that will be leveraging this solution.</span></span>  <span data-ttu-id="81eaf-105">混合式身分識別一開始是支援的角色 (它可提供驗證而支援所有其他雲端解決方案)，接著會提供新奇有趣的功能，為使用者釋出新的工作負載。</span><span class="sxs-lookup"><span data-stu-id="81eaf-105">Hybrid identity starts as a supporting role (it supports all other cloud solutions by providing authentication) and goes on to provide new and interesting capabilities that unlock new workloads for users.</span></span>  <span data-ttu-id="81eaf-106">您想要為使用者採用的這些工作負載或服務，會指定混合式身分識別設計的需求。</span><span class="sxs-lookup"><span data-stu-id="81eaf-106">These workloads or services that you wish to adopt for your users will dictate the requirements for the hybrid identity design.</span></span>  <span data-ttu-id="81eaf-107">這些服務和工作負載在內部部署和雲端中都需要運用混合式身分識別。</span><span class="sxs-lookup"><span data-stu-id="81eaf-107">These services and workloads need to leverage hybrid identity both on-premises and in the cloud.</span></span>  

<span data-ttu-id="81eaf-108">我們必須通盤審視企業的各個主要層面，以了解其目前的需求，以及公司對未來的規劃。</span><span class="sxs-lookup"><span data-stu-id="81eaf-108">You need to go over these key aspects of the business to understand what it is a requirement now and what the company plans for the future.</span></span> <span data-ttu-id="81eaf-109">如果您不清楚混合式身分識別設計的長期策略，您的解決方案在未來有可能無法隨著企業的成長和變化而進行調整。</span><span class="sxs-lookup"><span data-stu-id="81eaf-109">If you don’t have the visibility of the long term strategy for hybrid identity design, chances are that your solution will not be scalable as the business needs grow and change.</span></span>   <span data-ttu-id="81eaf-110">下圖中的範例說明混合式身分識別架構和要為使用者釋出的工作負載。</span><span class="sxs-lookup"><span data-stu-id="81eaf-110">T he diagram below shows an example of a hybrid identity architecture and the workloads that are being unlocked for users.</span></span> <span data-ttu-id="81eaf-111">此範例只是為了說明所有可透過健全的整合式身分識別策略釋出及提供的新可能性。</span><span class="sxs-lookup"><span data-stu-id="81eaf-111">This is just an example of all the new possibilities that can be unlocked and delivered with a solid hybrid identity strategy.</span></span> 

<span data-ttu-id="81eaf-112">屬於混合式身分識別架構的部分元件 ![](./media/hybrid-id-design-considerations/hybrid-identity-architechture.png)</span><span class="sxs-lookup"><span data-stu-id="81eaf-112">Some components that are part of the hybrid identity architecture ![](./media/hybrid-id-design-considerations/hybrid-identity-architechture.png)</span></span>

## <a name="determine-business-needs"></a><span data-ttu-id="81eaf-113">判斷商務需求</span><span class="sxs-lookup"><span data-stu-id="81eaf-113">Determine business needs</span></span>
<span data-ttu-id="81eaf-114">每家公司都會有不同的需求，即使這些公司屬於相同產業，實際的商務需求仍可能有所不同。</span><span class="sxs-lookup"><span data-stu-id="81eaf-114">Each company will have different requirements, even if these companies are part of the same industry, the real business requirements might vary.</span></span> <span data-ttu-id="81eaf-115">您仍然可以採用業界的最佳作法，但最終引導您定義混合式身分識別設計需求的，仍將是公司的商務需求。</span><span class="sxs-lookup"><span data-stu-id="81eaf-115">You can still leverage best practices from the industry, but ultimately it is the company’s business needs that will lead you to define the requirements for the hybrid identity design.</span></span> 

<span data-ttu-id="81eaf-116">請確實回答下列問題以識別您的商務需求：</span><span class="sxs-lookup"><span data-stu-id="81eaf-116">Make sure to answer the following questions to identify your business needs:</span></span>

* <span data-ttu-id="81eaf-117">您的公司想要減少 IT 營運成本嗎？</span><span class="sxs-lookup"><span data-stu-id="81eaf-117">Is your company looking to cut IT operational cost?</span></span>
* <span data-ttu-id="81eaf-118">您的公司想要保護雲端資產 (SaaS 應用程式、基礎結構) 嗎？</span><span class="sxs-lookup"><span data-stu-id="81eaf-118">Is your company looking to secure cloud assets (SaaS apps, infrastructure)?</span></span>
* <span data-ttu-id="81eaf-119">您的公司想要將 IT 現代化嗎？</span><span class="sxs-lookup"><span data-stu-id="81eaf-119">Is your company looking to modernize your IT?</span></span>
  * <span data-ttu-id="81eaf-120">您的使用者是行動性和要求較高的 IT 人員，因而期望您的 DMZ 允許以不同類型的流量存取不同的資源嗎？</span><span class="sxs-lookup"><span data-stu-id="81eaf-120">Are your users more mobile and demanding IT to create exceptions into your DMZ to allow different type of traffic to access different resources?</span></span>
  * <span data-ttu-id="81eaf-121">您的公司是否有需要發佈給這些現代使用者、但並不容易重寫的舊型應用程式？</span><span class="sxs-lookup"><span data-stu-id="81eaf-121">Does your company have legacy apps that needed to be published to these modern users but are not easy to rewrite?</span></span>
  * <span data-ttu-id="81eaf-122">您的公司是否需要在能夠全盤掌控的情況下完成這些工作？</span><span class="sxs-lookup"><span data-stu-id="81eaf-122">Does your company need to accomplish all these tasks and bring it under control at the same time?</span></span>
* <span data-ttu-id="81eaf-123">您的公司是否想要在內部部署中導入新工具，以運用 Microsoft Azure 安全性的專業功能，保護使用者的身分識別及降低風險？</span><span class="sxs-lookup"><span data-stu-id="81eaf-123">Is your company looking to secure users’ identities and reduce risk by bringing new tools that leverage the expertise of Microsoft’s Azure security expertise on-premises?</span></span>
* <span data-ttu-id="81eaf-124">您的公司是否嘗試要在內部部署中擺脫可怕的「外部」帳戶，並將其移至雲端，使其不再是內部部署環境內的潛在威脅？</span><span class="sxs-lookup"><span data-stu-id="81eaf-124">Is your company trying to get rid of the dreaded “external” accounts on premises and move them to the cloud where they are no longer a dormant threat inside your on-premises environment?</span></span>

## <a name="analyze-on-premises-identity-infrastructure"></a><span data-ttu-id="81eaf-125">分析內部部署身分識別基礎結構</span><span class="sxs-lookup"><span data-stu-id="81eaf-125">Analyze on-premises identity infrastructure</span></span>
<span data-ttu-id="81eaf-126">現在您已對公司的商務需求有所了解，您必須評估內部部署身分識別基礎結構。</span><span class="sxs-lookup"><span data-stu-id="81eaf-126">Now that you have an idea regarding your company business requirements, you need to evaluate your on-premises identity infrastructure.</span></span> <span data-ttu-id="81eaf-127">在定義將目前的身分識別解決方案整合到雲端身分識別管理系統的技術需求時，這項評估是很重要的。</span><span class="sxs-lookup"><span data-stu-id="81eaf-127">This evaluation is important for defining the technical requirements to integrate your current identity solution to the cloud identity management system.</span></span> <span data-ttu-id="81eaf-128">請確實回答下列問題：</span><span class="sxs-lookup"><span data-stu-id="81eaf-128">Make sure to answer the following questions:</span></span>

* <span data-ttu-id="81eaf-129">您的公司在內部部署中使用何種驗證和授權解決方案？</span><span class="sxs-lookup"><span data-stu-id="81eaf-129">What authentication and authorization solution does your company use on-premises?</span></span> 
* <span data-ttu-id="81eaf-130">您的公司目前有任何內部部署同步處理服務嗎？</span><span class="sxs-lookup"><span data-stu-id="81eaf-130">Does your company currently have any on-premises synchronization services?</span></span>
* <span data-ttu-id="81eaf-131">您的貴公司是否使用任何協力廠商身分識別提供者 (IdP)？</span><span class="sxs-lookup"><span data-stu-id="81eaf-131">Does your company use any third-party Identity Providers (IdP)?</span></span>

<span data-ttu-id="81eaf-132">您也需要知道公司可能有的雲端服務。</span><span class="sxs-lookup"><span data-stu-id="81eaf-132">You also need to be aware of the cloud services that your company might have.</span></span> <span data-ttu-id="81eaf-133">執行評估以了解您的環境中目前與 SaaS、IaaS 或 PaaS 模型的整合，是非常重要的。</span><span class="sxs-lookup"><span data-stu-id="81eaf-133">Performing an assessment to understand the current integration with SaaS, IaaS or PaaS models in your environment is very important.</span></span> <span data-ttu-id="81eaf-134">請務必在這個評估期間回答下列問題︰</span><span class="sxs-lookup"><span data-stu-id="81eaf-134">Make sure to answer the following questions during this assessment:</span></span>

* <span data-ttu-id="81eaf-135">貴公司是否與任何雲端服務提供者整合？</span><span class="sxs-lookup"><span data-stu-id="81eaf-135">Does your company have any integration with a cloud service provider?</span></span>
* <span data-ttu-id="81eaf-136">如果是，請問使用了哪些服務？</span><span class="sxs-lookup"><span data-stu-id="81eaf-136">If yes, which services are being used?</span></span>
* <span data-ttu-id="81eaf-137">這項整合目前已投入使用，或只是一項試驗？</span><span class="sxs-lookup"><span data-stu-id="81eaf-137">Is this integration currently in production or is it a pilot?</span></span>

> [!NOTE]
> <span data-ttu-id="81eaf-138">如果您無法正確對應您的應用程式與雲端服務，您可以使用雲端應用程式探索工具。</span><span class="sxs-lookup"><span data-stu-id="81eaf-138">If you don’t have an accurate mapping of all your apps and cloud services, you can use the Cloud App Discovery tool.</span></span> <span data-ttu-id="81eaf-139">這項工具可讓您的 IT 部門深入了解組織的所有商業和取用者雲端應用程式。</span><span class="sxs-lookup"><span data-stu-id="81eaf-139">This tool can provide your IT department with visibility into all your organization’s business and consumer cloud apps.</span></span> <span data-ttu-id="81eaf-140">尋找組織中的「影子 IT」從未如此容易，就連使用模式的詳細資料，以及正在存取雲端應用程式的使用者都能找到。</span><span class="sxs-lookup"><span data-stu-id="81eaf-140">That makes it easier than ever to discover shadow IT in your organization, including details on usage patterns and any users accessing your cloud applications.</span></span> <span data-ttu-id="81eaf-141">若要開始使用，請參閱[雲端應用程式探索](active-directory-cloudappdiscovery-whatis.md)。</span><span class="sxs-lookup"><span data-stu-id="81eaf-141">To get started see [Cloud app discovery](active-directory-cloudappdiscovery-whatis.md).</span></span>
> 
> 

## <a name="evaluate-identity-integration-requirements"></a><span data-ttu-id="81eaf-142">評估身分識別整合需求</span><span class="sxs-lookup"><span data-stu-id="81eaf-142">Evaluate identity integration requirements</span></span>
<span data-ttu-id="81eaf-143">接下來，您必須評估身分識別整合需求。</span><span class="sxs-lookup"><span data-stu-id="81eaf-143">Next, you need to evaluate the identity integration requirements.</span></span> <span data-ttu-id="81eaf-144">要定義使用者執行驗證的方式、組織存在於雲端中的型態、組織提供授權的方式以及將會有何種使用者經驗的技術需求，這項評估是很重要的。</span><span class="sxs-lookup"><span data-stu-id="81eaf-144">This evaluation is important to define the technical requirements for how users will authenticate, how the organization’s presence will look in the cloud, how the organization will allow authorization and what the user experience is going to be.</span></span> <span data-ttu-id="81eaf-145">請確實回答下列問題：</span><span class="sxs-lookup"><span data-stu-id="81eaf-145">Make sure to answer the following questions:</span></span>

* <span data-ttu-id="81eaf-146">您的組織是否會使用同盟和 (或) 標準驗證？</span><span class="sxs-lookup"><span data-stu-id="81eaf-146">Will your organization be using federation, standard authentication or both?</span></span>
* <span data-ttu-id="81eaf-147">同盟是必要條件嗎？</span><span class="sxs-lookup"><span data-stu-id="81eaf-147">Is federation a requirement?</span></span>  <span data-ttu-id="81eaf-148">原因如下：</span><span class="sxs-lookup"><span data-stu-id="81eaf-148">Because of the following:</span></span>
  * <span data-ttu-id="81eaf-149">Kerberos 型 SSO</span><span class="sxs-lookup"><span data-stu-id="81eaf-149">Kerberos-based SSO</span></span>
  * <span data-ttu-id="81eaf-150">您的公司有使用 SAML 或類似同盟功能的內部部署應用程式 (內建或協力廠商)。</span><span class="sxs-lookup"><span data-stu-id="81eaf-150">Your company has an on-premises applications (either built in-house or 3rd party) that uses SAML or similar federation capabilities.</span></span>
  * <span data-ttu-id="81eaf-151">透過智慧卡的 MFA。</span><span class="sxs-lookup"><span data-stu-id="81eaf-151">MFA via Smart Cards.</span></span> <span data-ttu-id="81eaf-152">RSA SecurID 等等。</span><span class="sxs-lookup"><span data-stu-id="81eaf-152">RSA SecurID, etc.</span></span>
  * <span data-ttu-id="81eaf-153">可解決下列問題的用戶端存取規則：</span><span class="sxs-lookup"><span data-stu-id="81eaf-153">Client access rules that address the questions below:</span></span>
    1. <span data-ttu-id="81eaf-154">我是否可根據用戶端的 IP 位址封鎖所有對 Office 365 的外部存取？</span><span class="sxs-lookup"><span data-stu-id="81eaf-154">Can I block all external access to Office 365 based on the IP address of the client?</span></span>
    2. <span data-ttu-id="81eaf-155">我是否可封鎖所有對 Office 365 的外部存取 (Exchange ActiveSync 除外)？</span><span class="sxs-lookup"><span data-stu-id="81eaf-155">Can I block all external access to Office 365, except Exchange ActiveSync?</span></span>
    3. <span data-ttu-id="81eaf-156">我是否可封鎖所有對 Office 365 的外部存取 (瀏覽器型應用程式 (OWA、SPO) 除外)？</span><span class="sxs-lookup"><span data-stu-id="81eaf-156">Can I block all external access to Office 365, except for browser-based apps (OWA, SPO)</span></span>
    4. <span data-ttu-id="81eaf-157">我是否可針對指定的 AD 群組成員封鎖所有對 Office 365 的外部存取？</span><span class="sxs-lookup"><span data-stu-id="81eaf-157">Can I block all external access to Office 365 for members of designated AD groups</span></span>
* <span data-ttu-id="81eaf-158">安全性/稽核考量</span><span class="sxs-lookup"><span data-stu-id="81eaf-158">Security/auditing concerns</span></span>
* <span data-ttu-id="81eaf-159">對同盟驗證既有的投資</span><span class="sxs-lookup"><span data-stu-id="81eaf-159">Already existing investment in federated authentication</span></span>
* <span data-ttu-id="81eaf-160">我們的組織在雲端中的網域將使用何種名稱？</span><span class="sxs-lookup"><span data-stu-id="81eaf-160">What name will our organization use for our domain in the cloud?</span></span>
* <span data-ttu-id="81eaf-161">組織是否有自訂網域嗎？</span><span class="sxs-lookup"><span data-stu-id="81eaf-161">Does the organization have a custom domain?</span></span>
  1. <span data-ttu-id="81eaf-162">該網域是否為公用的？可透過 DNS 輕易驗證嗎？</span><span class="sxs-lookup"><span data-stu-id="81eaf-162">Is that domain public and easily verifiable via DNS?</span></span>
  2. <span data-ttu-id="81eaf-163">如果不是，您是否有公用網域可用來在 AD 中註冊替代 UPN？</span><span class="sxs-lookup"><span data-stu-id="81eaf-163">If it is not, then do you have a public domain that can be used to register an alternate UPN in AD?</span></span>
* <span data-ttu-id="81eaf-164">雲端中顯示的使用者識別碼是否一致？</span><span class="sxs-lookup"><span data-stu-id="81eaf-164">Are the user identifiers consistent for cloud representation?</span></span> 
* <span data-ttu-id="81eaf-165">組織是否有需要與雲端服務整合的應用程式？</span><span class="sxs-lookup"><span data-stu-id="81eaf-165">Does the organization have apps that require integration with cloud services?</span></span>
* <span data-ttu-id="81eaf-166">組織是否有多個網域？全都會使用標準或同盟驗證嗎？</span><span class="sxs-lookup"><span data-stu-id="81eaf-166">Does the organization have multiple domains and will they all use standard or federated authentication?</span></span>

## <a name="evaluate-applications-that-run-in-your-environment"></a><span data-ttu-id="81eaf-167">評估在您的環境中執行的應用程式</span><span class="sxs-lookup"><span data-stu-id="81eaf-167">Evaluate applications that run in your environment</span></span>
<span data-ttu-id="81eaf-168">現在您已對內部部署和雲端基礎結構有所了解，您必須評估在這些環境中執行的應用程式。</span><span class="sxs-lookup"><span data-stu-id="81eaf-168">Now that you have an idea regarding your on-premises and cloud infrastructure, you need to evaluate the applications that run in these environments.</span></span> <span data-ttu-id="81eaf-169">當您定義如何將這些應用程式整合到雲端身分識別管理系統的技術需求時，這項評估是很重要的。</span><span class="sxs-lookup"><span data-stu-id="81eaf-169">This evaluation is important to define the technical requirements to integrate these applications to the cloud identity management system.</span></span> <span data-ttu-id="81eaf-170">請確實回答下列問題：</span><span class="sxs-lookup"><span data-stu-id="81eaf-170">Make sure to answer the following questions:</span></span>

* <span data-ttu-id="81eaf-171">我們的應用程式將在何處運作？</span><span class="sxs-lookup"><span data-stu-id="81eaf-171">Where will our applications live?</span></span>
* <span data-ttu-id="81eaf-172">使用者會存取內部部署應用程式嗎？</span><span class="sxs-lookup"><span data-stu-id="81eaf-172">Will users be accessing on-premises applications?</span></span>  <span data-ttu-id="81eaf-173">還是在雲端？</span><span class="sxs-lookup"><span data-stu-id="81eaf-173">In the cloud?</span></span> <span data-ttu-id="81eaf-174">或是兩者都有？</span><span class="sxs-lookup"><span data-stu-id="81eaf-174">Or both?</span></span>
* <span data-ttu-id="81eaf-175">是否有將現有的應用程式工作負載移至雲端的計劃？</span><span class="sxs-lookup"><span data-stu-id="81eaf-175">Are there plans to take the existing application workloads and move them to the cloud?</span></span>
* <span data-ttu-id="81eaf-176">是否計劃要開發將存在於內部部署或雲端中，但會使用雲端驗證的新應用程式？</span><span class="sxs-lookup"><span data-stu-id="81eaf-176">Are there plans to develop new applications that will reside either on-premises or in the cloud that will use cloud authentication?</span></span>

## <a name="evaluate-user-requirements"></a><span data-ttu-id="81eaf-177">評估使用者需求</span><span class="sxs-lookup"><span data-stu-id="81eaf-177">Evaluate user requirements</span></span>
<span data-ttu-id="81eaf-178">您也必須評估使用者需求。</span><span class="sxs-lookup"><span data-stu-id="81eaf-178">You also have to evaluate the user requirements.</span></span> <span data-ttu-id="81eaf-179">要定義在使用者轉換至雲端時予以登入並提供協助所需的步驟，這項評估是很重要的。</span><span class="sxs-lookup"><span data-stu-id="81eaf-179">This evaluation is important to define the steps that will be needed for on-boarding and assisting users as they transition to the cloud.</span></span> <span data-ttu-id="81eaf-180">請確實回答下列問題：</span><span class="sxs-lookup"><span data-stu-id="81eaf-180">Make sure to answer the following questions:</span></span>

* <span data-ttu-id="81eaf-181">使用者會存取應用程式內部部署嗎？</span><span class="sxs-lookup"><span data-stu-id="81eaf-181">Will users be accessing applications on-premises?</span></span>
* <span data-ttu-id="81eaf-182">使用者會存取雲端中的應用程式嗎？</span><span class="sxs-lookup"><span data-stu-id="81eaf-182">Will users be accessing applications in the cloud?</span></span>
* <span data-ttu-id="81eaf-183">使用者通常會以何種方式登入其內部部署環境？</span><span class="sxs-lookup"><span data-stu-id="81eaf-183">How do users typically login to their on-premises environment?</span></span>
* <span data-ttu-id="81eaf-184">使用者將如何登入雲端？</span><span class="sxs-lookup"><span data-stu-id="81eaf-184">How will users sign-in to the cloud?</span></span>

> [!NOTE]
> <span data-ttu-id="81eaf-185">請確定會記下每個答案，並了解答案背後的原理。</span><span class="sxs-lookup"><span data-stu-id="81eaf-185">Make sure to take notes of each answer and understand the rationale behind the answer.</span></span> <span data-ttu-id="81eaf-186">[判斷事件回應需求](active-directory-hybrid-identity-design-considerations-incident-response-requirements.md) 將說明可用的選項，以及每個選項的優缺點。</span><span class="sxs-lookup"><span data-stu-id="81eaf-186">[Determine incident response requirements](active-directory-hybrid-identity-design-considerations-incident-response-requirements.md) will go over the options available and pros/cons of each option.</span></span>  <span data-ttu-id="81eaf-187">回答這些問題之後，您就能選取最適合業務需求的選項。</span><span class="sxs-lookup"><span data-stu-id="81eaf-187">By having answered those questions you will select which option best suits your business needs.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="81eaf-188">後續步驟</span><span class="sxs-lookup"><span data-stu-id="81eaf-188">Next steps</span></span>
[<span data-ttu-id="81eaf-189">判斷目錄同步處理需求</span><span class="sxs-lookup"><span data-stu-id="81eaf-189">Determine directory synchronization requirements</span></span>](active-directory-hybrid-identity-design-considerations-directory-sync-requirements.md)

## <a name="see-also"></a><span data-ttu-id="81eaf-190">另請參閱</span><span class="sxs-lookup"><span data-stu-id="81eaf-190">See also</span></span>
[<span data-ttu-id="81eaf-191">設計考量概觀</span><span class="sxs-lookup"><span data-stu-id="81eaf-191">Design considerations overview</span></span>](active-directory-hybrid-identity-design-considerations-overview.md)

