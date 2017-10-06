---
title: "aaaAzure Active Directory 混合式身分識別設計考量-決定身分識別需求 |Microsoft 文件"
description: "識別導致 hello 混合式身分識別設計 toodefine hello 需求的 hello 公司的商務需求。"
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
ms.openlocfilehash: b2f1cad923b0f08ededa0d8f9a4ea8e799956e54
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="determine-identity-requirements-for-your-hybrid-identity-solution"></a><span data-ttu-id="e9085-103">判斷混合式身分識別解決方案的身分識別需求</span><span class="sxs-lookup"><span data-stu-id="e9085-103">Determine identity requirements for your hybrid identity solution</span></span>
<span data-ttu-id="e9085-104">hello 設計的混合式身分識別解決方案的第一個步驟是充分利用此解決方案的 hello 商業組織 toodetermine hello 需求。</span><span class="sxs-lookup"><span data-stu-id="e9085-104">hello first step in designing a hybrid identity solution is toodetermine hello requirements for hello business organization that will be leveraging this solution.</span></span>  <span data-ttu-id="e9085-105">混合式身分識別 （它支援所有其他雲端方案提供驗證） 支援角色會啟動，且會在解除鎖定使用者新的工作負載的 tooprovide 新的實用功能。</span><span class="sxs-lookup"><span data-stu-id="e9085-105">Hybrid identity starts as a supporting role (it supports all other cloud solutions by providing authentication) and goes on tooprovide new and interesting capabilities that unlock new workloads for users.</span></span>  <span data-ttu-id="e9085-106">這些工作負載或服務，您會希望 tooadopt 為您的使用者會指定 hello 混合式身分識別設計的 hello 需求。</span><span class="sxs-lookup"><span data-stu-id="e9085-106">These workloads or services that you wish tooadopt for your users will dictate hello requirements for hello hybrid identity design.</span></span>  <span data-ttu-id="e9085-107">這些服務和工作負載需要 tooleverage 混合式身分識別這兩個內部部署和 hello 雲端中。</span><span class="sxs-lookup"><span data-stu-id="e9085-107">These services and workloads need tooleverage hybrid identity both on-premises and in hello cloud.</span></span>  

<span data-ttu-id="e9085-108">您需要 toogo 比 hello 商務 toounderstand 的重要層面，什麼是現在的需求，以及哪些 hello 公司計劃 hello 未來。</span><span class="sxs-lookup"><span data-stu-id="e9085-108">You need toogo over these key aspects of hello business toounderstand what it is a requirement now and what hello company plans for hello future.</span></span> <span data-ttu-id="e9085-109">如果您沒有混合式身分識別設計的 hello 的長期策略 hello 可見性，有可能會是，您的方案將不會擴充在 hello 的商務需求成長及變更。</span><span class="sxs-lookup"><span data-stu-id="e9085-109">If you don’t have hello visibility of hello long term strategy for hybrid identity design, chances are that your solution will not be scalable as hello business needs grow and change.</span></span>   <span data-ttu-id="e9085-110">他圖表所示的混合式身分識別架構和 hello 的工作負載針對使用者正在取消鎖定範例 T。</span><span class="sxs-lookup"><span data-stu-id="e9085-110">T he diagram below shows an example of a hybrid identity architecture and hello workloads that are being unlocked for users.</span></span> <span data-ttu-id="e9085-111">這只是範例的所有 hello 新的可能性，可以解除鎖定，並使用純色的混合式身分識別的策略來傳遞。</span><span class="sxs-lookup"><span data-stu-id="e9085-111">This is just an example of all hello new possibilities that can be unlocked and delivered with a solid hybrid identity strategy.</span></span> 

<span data-ttu-id="e9085-112">屬於 hello 混合式身分識別架構的部分元件![](./media/hybrid-id-design-considerations/hybrid-identity-architechture.png)</span><span class="sxs-lookup"><span data-stu-id="e9085-112">Some components that are part of hello hybrid identity architecture ![](./media/hybrid-id-design-considerations/hybrid-identity-architechture.png)</span></span>

## <a name="determine-business-needs"></a><span data-ttu-id="e9085-113">判斷商務需求</span><span class="sxs-lookup"><span data-stu-id="e9085-113">Determine business needs</span></span>
<span data-ttu-id="e9085-114">每一家公司會有不同需求，即使這些公司屬於 hello 相同的業界 hello 真正的業務需求可能都不同。</span><span class="sxs-lookup"><span data-stu-id="e9085-114">Each company will have different requirements, even if these companies are part of hello same industry, hello real business requirements might vary.</span></span> <span data-ttu-id="e9085-115">您仍然可以利用從 hello 業界的最佳作法，但最終仍是導致 hello 混合式身分識別設計 toodefine hello 需求的 hello 公司的商務需求。</span><span class="sxs-lookup"><span data-stu-id="e9085-115">You can still leverage best practices from hello industry, but ultimately it is hello company’s business needs that will lead you toodefine hello requirements for hello hybrid identity design.</span></span> 

<span data-ttu-id="e9085-116">請確定 tooanswer hello 下列問題 tooidentify 業務需要：</span><span class="sxs-lookup"><span data-stu-id="e9085-116">Make sure tooanswer hello following questions tooidentify your business needs:</span></span>

* <span data-ttu-id="e9085-117">您的公司正在尋找 toocut IT 作業成本？</span><span class="sxs-lookup"><span data-stu-id="e9085-117">Is your company looking toocut IT operational cost?</span></span>
* <span data-ttu-id="e9085-118">您的公司正在尋找 toosecure 雲端資產 （[基礎結構中的 [SaaS 應用程式）？</span><span class="sxs-lookup"><span data-stu-id="e9085-118">Is your company looking toosecure cloud assets (SaaS apps, infrastructure)?</span></span>
* <span data-ttu-id="e9085-119">為您的公司正在尋找 toomodernize 您的 IT 嗎？</span><span class="sxs-lookup"><span data-stu-id="e9085-119">Is your company looking toomodernize your IT?</span></span>
  * <span data-ttu-id="e9085-120">是您的使用者更多行動裝置版和嚴苛 IT toocreate 例外狀況成您 DMZ tooallow 不同類型的流量 tooaccess 不同的資源嗎？</span><span class="sxs-lookup"><span data-stu-id="e9085-120">Are your users more mobile and demanding IT toocreate exceptions into your DMZ tooallow different type of traffic tooaccess different resources?</span></span>
  * <span data-ttu-id="e9085-121">您的公司是否有舊版的應用程式需要發行 toobe toothese 現代使用者不容易 toorewrite？</span><span class="sxs-lookup"><span data-stu-id="e9085-121">Does your company have legacy apps that needed toobe published toothese modern users but are not easy toorewrite?</span></span>
  * <span data-ttu-id="e9085-122">您的公司需要 tooaccomplish 所有這些工作並使其在 hello 控制相同的時間？</span><span class="sxs-lookup"><span data-stu-id="e9085-122">Does your company need tooaccomplish all these tasks and bring it under control at hello same time?</span></span>
* <span data-ttu-id="e9085-123">是您的公司尋找 toosecure 使用者的身分識別，並使新的工具，可利用 Microsoft Azure 安全性專業知識在內部部署的 hello 專業知識，就能降低風險？</span><span class="sxs-lookup"><span data-stu-id="e9085-123">Is your company looking toosecure users’ identities and reduce risk by bringing new tools that leverage hello expertise of Microsoft’s Azure security expertise on-premises?</span></span>
* <span data-ttu-id="e9085-124">嘗試移除 hello tooget 貴公司可怕的 「 外部 」 的帳戶，在內部部署及是將它們移 toohello 它們的位置不再休眠的潛在威脅，在內部部署環境內的雲端？</span><span class="sxs-lookup"><span data-stu-id="e9085-124">Is your company trying tooget rid of hello dreaded “external” accounts on premises and move them toohello cloud where they are no longer a dormant threat inside your on-premises environment?</span></span>

## <a name="analyze-on-premises-identity-infrastructure"></a><span data-ttu-id="e9085-125">分析內部部署身分識別基礎結構</span><span class="sxs-lookup"><span data-stu-id="e9085-125">Analyze on-premises identity infrastructure</span></span>
<span data-ttu-id="e9085-126">既然您已了解有關您公司的商務需求時，您需要 tooevaluate 您在內部部署身分識別基礎結構。</span><span class="sxs-lookup"><span data-stu-id="e9085-126">Now that you have an idea regarding your company business requirements, you need tooevaluate your on-premises identity infrastructure.</span></span> <span data-ttu-id="e9085-127">這項評估是重要的定義 hello 技術需求 toointegrate 目前身分識別解決方案 toohello 雲端身分識別管理系統。</span><span class="sxs-lookup"><span data-stu-id="e9085-127">This evaluation is important for defining hello technical requirements toointegrate your current identity solution toohello cloud identity management system.</span></span> <span data-ttu-id="e9085-128">請確定 tooanswer hello 下列問題：</span><span class="sxs-lookup"><span data-stu-id="e9085-128">Make sure tooanswer hello following questions:</span></span>

* <span data-ttu-id="e9085-129">您的公司在內部部署中使用何種驗證和授權解決方案？</span><span class="sxs-lookup"><span data-stu-id="e9085-129">What authentication and authorization solution does your company use on-premises?</span></span> 
* <span data-ttu-id="e9085-130">您的公司目前有任何內部部署同步處理服務嗎？</span><span class="sxs-lookup"><span data-stu-id="e9085-130">Does your company currently have any on-premises synchronization services?</span></span>
* <span data-ttu-id="e9085-131">您的貴公司是否使用任何協力廠商身分識別提供者 (IdP)？</span><span class="sxs-lookup"><span data-stu-id="e9085-131">Does your company use any third-party Identity Providers (IdP)?</span></span>

<span data-ttu-id="e9085-132">您也需要 toobe 知道您的公司可能會有的 hello 雲端服務。</span><span class="sxs-lookup"><span data-stu-id="e9085-132">You also need toobe aware of hello cloud services that your company might have.</span></span> <span data-ttu-id="e9085-133">執行評定 toounderstand hello 目前與整合 SaaS，您的環境中的 IaaS 或 PaaS 模型是非常重要。</span><span class="sxs-lookup"><span data-stu-id="e9085-133">Performing an assessment toounderstand hello current integration with SaaS, IaaS or PaaS models in your environment is very important.</span></span> <span data-ttu-id="e9085-134">請確定 tooanswer hello 遵循這項評估期間的問題：</span><span class="sxs-lookup"><span data-stu-id="e9085-134">Make sure tooanswer hello following questions during this assessment:</span></span>

* <span data-ttu-id="e9085-135">貴公司是否與任何雲端服務提供者整合？</span><span class="sxs-lookup"><span data-stu-id="e9085-135">Does your company have any integration with a cloud service provider?</span></span>
* <span data-ttu-id="e9085-136">如果是，請問使用了哪些服務？</span><span class="sxs-lookup"><span data-stu-id="e9085-136">If yes, which services are being used?</span></span>
* <span data-ttu-id="e9085-137">這項整合目前已投入使用，或只是一項試驗？</span><span class="sxs-lookup"><span data-stu-id="e9085-137">Is this integration currently in production or is it a pilot?</span></span>

> [!NOTE]
> <span data-ttu-id="e9085-138">如果您不要讓具有正確對應的所有應用程式和雲端服務，您可以使用 hello Cloud App Discovery 工具。</span><span class="sxs-lookup"><span data-stu-id="e9085-138">If you don’t have an accurate mapping of all your apps and cloud services, you can use hello Cloud App Discovery tool.</span></span> <span data-ttu-id="e9085-139">這項工具可讓您的 IT 部門深入了解組織的所有商業和取用者雲端應用程式。</span><span class="sxs-lookup"><span data-stu-id="e9085-139">This tool can provide your IT department with visibility into all your organization’s business and consumer cloud apps.</span></span> <span data-ttu-id="e9085-140">它較容易曾經 toodiscover 陰影 IT 組織中包括使用模式與任何使用者存取您的雲端應用程式的詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="e9085-140">That makes it easier than ever toodiscover shadow IT in your organization, including details on usage patterns and any users accessing your cloud applications.</span></span> <span data-ttu-id="e9085-141">請參閱 tooget 啟動[Cloud app discovery](active-directory-cloudappdiscovery-whatis.md)。</span><span class="sxs-lookup"><span data-stu-id="e9085-141">tooget started see [Cloud app discovery](active-directory-cloudappdiscovery-whatis.md).</span></span>
> 
> 

## <a name="evaluate-identity-integration-requirements"></a><span data-ttu-id="e9085-142">評估身分識別整合需求</span><span class="sxs-lookup"><span data-stu-id="e9085-142">Evaluate identity integration requirements</span></span>
<span data-ttu-id="e9085-143">接下來，您需要 tooevaluate hello 身分識別整合需求。</span><span class="sxs-lookup"><span data-stu-id="e9085-143">Next, you need tooevaluate hello identity integration requirements.</span></span> <span data-ttu-id="e9085-144">這項評估是使用者驗證的方式、 hello 的組織存在 hello 雲端中所呈現的樣子，hello 組織可讓授權的方式和哪些 hello 使用者體驗是進行 toobe 的重要 toodefine hello 技術需求。</span><span class="sxs-lookup"><span data-stu-id="e9085-144">This evaluation is important toodefine hello technical requirements for how users will authenticate, how hello organization’s presence will look in hello cloud, how hello organization will allow authorization and what hello user experience is going toobe.</span></span> <span data-ttu-id="e9085-145">請確定 tooanswer hello 下列問題：</span><span class="sxs-lookup"><span data-stu-id="e9085-145">Make sure tooanswer hello following questions:</span></span>

* <span data-ttu-id="e9085-146">您的組織是否會使用同盟和 (或) 標準驗證？</span><span class="sxs-lookup"><span data-stu-id="e9085-146">Will your organization be using federation, standard authentication or both?</span></span>
* <span data-ttu-id="e9085-147">同盟是必要條件嗎？</span><span class="sxs-lookup"><span data-stu-id="e9085-147">Is federation a requirement?</span></span>  <span data-ttu-id="e9085-148">因為 hello 下列內容：</span><span class="sxs-lookup"><span data-stu-id="e9085-148">Because of hello following:</span></span>
  * <span data-ttu-id="e9085-149">Kerberos 型 SSO</span><span class="sxs-lookup"><span data-stu-id="e9085-149">Kerberos-based SSO</span></span>
  * <span data-ttu-id="e9085-150">您的公司有使用 SAML 或類似同盟功能的內部部署應用程式 (內建或協力廠商)。</span><span class="sxs-lookup"><span data-stu-id="e9085-150">Your company has an on-premises applications (either built in-house or 3rd party) that uses SAML or similar federation capabilities.</span></span>
  * <span data-ttu-id="e9085-151">透過智慧卡的 MFA。</span><span class="sxs-lookup"><span data-stu-id="e9085-151">MFA via Smart Cards.</span></span> <span data-ttu-id="e9085-152">RSA SecurID 等等。</span><span class="sxs-lookup"><span data-stu-id="e9085-152">RSA SecurID, etc.</span></span>
  * <span data-ttu-id="e9085-153">用戶端存取規則解決 hello 回答以下問題：</span><span class="sxs-lookup"><span data-stu-id="e9085-153">Client access rules that address hello questions below:</span></span>
    1. <span data-ttu-id="e9085-154">我可以封鎖所有外部存取 tooOffice 365 根據 hello hello 用戶端的 IP 位址嗎？</span><span class="sxs-lookup"><span data-stu-id="e9085-154">Can I block all external access tooOffice 365 based on hello IP address of hello client?</span></span>
    2. <span data-ttu-id="e9085-155">我可以封鎖所有外部存取 tooOffice 365、 Exchange ActiveSync 以外嗎？</span><span class="sxs-lookup"><span data-stu-id="e9085-155">Can I block all external access tooOffice 365, except Exchange ActiveSync?</span></span>
    3. <span data-ttu-id="e9085-156">我可以封鎖所有外部存取 tooOffice 365，除了瀏覽器型應用程式 （OWA、 SPO） 嗎</span><span class="sxs-lookup"><span data-stu-id="e9085-156">Can I block all external access tooOffice 365, except for browser-based apps (OWA, SPO)</span></span>
    4. <span data-ttu-id="e9085-157">可以封鎖所有外部存取 tooOffice 365 指定之 AD 群組的成員嗎</span><span class="sxs-lookup"><span data-stu-id="e9085-157">Can I block all external access tooOffice 365 for members of designated AD groups</span></span>
* <span data-ttu-id="e9085-158">安全性/稽核考量</span><span class="sxs-lookup"><span data-stu-id="e9085-158">Security/auditing concerns</span></span>
* <span data-ttu-id="e9085-159">對同盟驗證既有的投資</span><span class="sxs-lookup"><span data-stu-id="e9085-159">Already existing investment in federated authentication</span></span>
* <span data-ttu-id="e9085-160">名稱將我們的組織使用我們 hello 雲端中的網域？</span><span class="sxs-lookup"><span data-stu-id="e9085-160">What name will our organization use for our domain in hello cloud?</span></span>
* <span data-ttu-id="e9085-161">Hello 的組織是否有自訂網域？</span><span class="sxs-lookup"><span data-stu-id="e9085-161">Does hello organization have a custom domain?</span></span>
  1. <span data-ttu-id="e9085-162">該網域是否為公用的？可透過 DNS 輕易驗證嗎？</span><span class="sxs-lookup"><span data-stu-id="e9085-162">Is that domain public and easily verifiable via DNS?</span></span>
  2. <span data-ttu-id="e9085-163">如果不是，要再擁有公用網域，可以在 AD 中是使用的 tooregister 替代的 UPN 嗎？</span><span class="sxs-lookup"><span data-stu-id="e9085-163">If it is not, then do you have a public domain that can be used tooregister an alternate UPN in AD?</span></span>
* <span data-ttu-id="e9085-164">Hello 使用者識別碼都是一致的雲端表示法中使用？</span><span class="sxs-lookup"><span data-stu-id="e9085-164">Are hello user identifiers consistent for cloud representation?</span></span> 
* <span data-ttu-id="e9085-165">Hello 組織有需要與雲端服務整合的應用程式嗎？</span><span class="sxs-lookup"><span data-stu-id="e9085-165">Does hello organization have apps that require integration with cloud services?</span></span>
* <span data-ttu-id="e9085-166">Hello 組織是否有多個網域，並將它們都會使用標準或同盟驗證？</span><span class="sxs-lookup"><span data-stu-id="e9085-166">Does hello organization have multiple domains and will they all use standard or federated authentication?</span></span>

## <a name="evaluate-applications-that-run-in-your-environment"></a><span data-ttu-id="e9085-167">評估在您的環境中執行的應用程式</span><span class="sxs-lookup"><span data-stu-id="e9085-167">Evaluate applications that run in your environment</span></span>
<span data-ttu-id="e9085-168">既然您已了解有關在內部和雲端基礎結構，您需要在這些環境中執行的 tooevaluate hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="e9085-168">Now that you have an idea regarding your on-premises and cloud infrastructure, you need tooevaluate hello applications that run in these environments.</span></span> <span data-ttu-id="e9085-169">這項評估是重要 toodefine hello 技術需求 toointegrate 這些應用程式 toohello 雲端身分識別管理系統。</span><span class="sxs-lookup"><span data-stu-id="e9085-169">This evaluation is important toodefine hello technical requirements toointegrate these applications toohello cloud identity management system.</span></span> <span data-ttu-id="e9085-170">請確定 tooanswer hello 下列問題：</span><span class="sxs-lookup"><span data-stu-id="e9085-170">Make sure tooanswer hello following questions:</span></span>

* <span data-ttu-id="e9085-171">我們的應用程式將在何處運作？</span><span class="sxs-lookup"><span data-stu-id="e9085-171">Where will our applications live?</span></span>
* <span data-ttu-id="e9085-172">使用者會存取內部部署應用程式嗎？</span><span class="sxs-lookup"><span data-stu-id="e9085-172">Will users be accessing on-premises applications?</span></span>  <span data-ttu-id="e9085-173">在 [hello 雲端？</span><span class="sxs-lookup"><span data-stu-id="e9085-173">In hello cloud?</span></span> <span data-ttu-id="e9085-174">或是兩者都有？</span><span class="sxs-lookup"><span data-stu-id="e9085-174">Or both?</span></span>
* <span data-ttu-id="e9085-175">是否有計畫 tootake hello 現有應用程式工作負載，並將它們移 toohello 雲端？</span><span class="sxs-lookup"><span data-stu-id="e9085-175">Are there plans tootake hello existing application workloads and move them toohello cloud?</span></span>
* <span data-ttu-id="e9085-176">有計劃將位於內部或在 hello 雲端的 toodevelop 新應用程式會使用雲端驗證嗎？</span><span class="sxs-lookup"><span data-stu-id="e9085-176">Are there plans toodevelop new applications that will reside either on-premises or in hello cloud that will use cloud authentication?</span></span>

## <a name="evaluate-user-requirements"></a><span data-ttu-id="e9085-177">評估使用者需求</span><span class="sxs-lookup"><span data-stu-id="e9085-177">Evaluate user requirements</span></span>
<span data-ttu-id="e9085-178">您也可以 tooevaluate hello 使用者需求。</span><span class="sxs-lookup"><span data-stu-id="e9085-178">You also have tooevaluate hello user requirements.</span></span> <span data-ttu-id="e9085-179">這項評估是在需要加入及協助使用者，因為這些轉換 toohello 雲端的重要 toodefine hello 步驟。</span><span class="sxs-lookup"><span data-stu-id="e9085-179">This evaluation is important toodefine hello steps that will be needed for on-boarding and assisting users as they transition toohello cloud.</span></span> <span data-ttu-id="e9085-180">請確定 tooanswer hello 下列問題：</span><span class="sxs-lookup"><span data-stu-id="e9085-180">Make sure tooanswer hello following questions:</span></span>

* <span data-ttu-id="e9085-181">使用者會存取應用程式內部部署嗎？</span><span class="sxs-lookup"><span data-stu-id="e9085-181">Will users be accessing applications on-premises?</span></span>
* <span data-ttu-id="e9085-182">使用者將用來存取 hello 雲端中的應用程式嗎？</span><span class="sxs-lookup"><span data-stu-id="e9085-182">Will users be accessing applications in hello cloud?</span></span>
* <span data-ttu-id="e9085-183">如何執行使用者通常登入 tootheir 內部部署環境嗎？</span><span class="sxs-lookup"><span data-stu-id="e9085-183">How do users typically login tootheir on-premises environment?</span></span>
* <span data-ttu-id="e9085-184">如何將雲端使用者登入 toohello？</span><span class="sxs-lookup"><span data-stu-id="e9085-184">How will users sign-in toohello cloud?</span></span>

> [!NOTE]
> <span data-ttu-id="e9085-185">請確定每個答案 tootake 附註，並了解 hello 回應 hello 背後的基本原理。</span><span class="sxs-lookup"><span data-stu-id="e9085-185">Make sure tootake notes of each answer and understand hello rationale behind hello answer.</span></span> <span data-ttu-id="e9085-186">[判斷事件回應需求](active-directory-hybrid-identity-design-considerations-incident-response-requirements.md)將介紹可用選項 hello 和專業人員/優缺點的每個選項。</span><span class="sxs-lookup"><span data-stu-id="e9085-186">[Determine incident response requirements](active-directory-hybrid-identity-design-considerations-incident-response-requirements.md) will go over hello options available and pros/cons of each option.</span></span>  <span data-ttu-id="e9085-187">回答這些問題之後，您就能選取最適合業務需求的選項。</span><span class="sxs-lookup"><span data-stu-id="e9085-187">By having answered those questions you will select which option best suits your business needs.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="e9085-188">後續步驟</span><span class="sxs-lookup"><span data-stu-id="e9085-188">Next steps</span></span>
[<span data-ttu-id="e9085-189">判斷目錄同步處理需求</span><span class="sxs-lookup"><span data-stu-id="e9085-189">Determine directory synchronization requirements</span></span>](active-directory-hybrid-identity-design-considerations-directory-sync-requirements.md)

## <a name="see-also"></a><span data-ttu-id="e9085-190">另請參閱</span><span class="sxs-lookup"><span data-stu-id="e9085-190">See also</span></span>
[<span data-ttu-id="e9085-191">設計考量概觀</span><span class="sxs-lookup"><span data-stu-id="e9085-191">Design considerations overview</span></span>](active-directory-hybrid-identity-design-considerations-overview.md)

