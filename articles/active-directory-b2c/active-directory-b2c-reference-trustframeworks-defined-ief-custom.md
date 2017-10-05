---
title: "Azure Active Directory B2C：參考 - 信任架構 | Microsoft Docs"
description: "關於 Azure Active Directory B2C 自訂原則和識別體驗架構的主題"
services: active-directory-b2c
documentationcenter: 
author: rojasja
manager: krassk
editor: rojasja
ms.assetid: 
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.topic: article
ms.devlang: na
ms.date: 08/04/2017
ms.author: joroja
ms.openlocfilehash: 4e2de9c4d1c0f92970911e132fffaacbd01d9ad0
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="define-trust-frameworks-with-azure-ad-b2c-identity-experience-framework"></a><span data-ttu-id="f9dec-103">使用 Azure AD B2C 識別體驗架構定義信任架構</span><span class="sxs-lookup"><span data-stu-id="f9dec-103">Define Trust Frameworks with Azure AD B2C Identity Experience Framework</span></span>

<span data-ttu-id="f9dec-104">使用識別體驗架構的 Azure Active Directory B2C (Azure AD B2C) 自訂原則，可為貴組織提供集中式服務。</span><span class="sxs-lookup"><span data-stu-id="f9dec-104">Azure Active Directory B2C (Azure AD B2C) custom policies that use the Identity Experience Framework provide your organization with a centralized service.</span></span> <span data-ttu-id="f9dec-105">此服務會降低感興趣的大型社群中，身分識別同盟的複雜度。</span><span class="sxs-lookup"><span data-stu-id="f9dec-105">This service reduces the complexity of identity federation in a large community of interest.</span></span> <span data-ttu-id="f9dec-106">複雜度會降低為單一信任關係和單一中繼資料交換。</span><span class="sxs-lookup"><span data-stu-id="f9dec-106">The complexity is reduced to a single trust relationship and a single metadata exchange.</span></span>

<span data-ttu-id="f9dec-107">使用識別體驗架構的 Azure AD B2C 自訂原則讓您能夠回答下列問題：</span><span class="sxs-lookup"><span data-stu-id="f9dec-107">Azure AD B2C custom policies that use the Identity Experience Framework to enable you to answer the following questions:</span></span>

- <span data-ttu-id="f9dec-108">必須遵守哪些法律、安全性、隱私權和資料保護原則？</span><span class="sxs-lookup"><span data-stu-id="f9dec-108">What are the legal, security, privacy, and data protection policies that must be adhered to?</span></span>
- <span data-ttu-id="f9dec-109">連絡人是誰，要經過哪些程序才能成為合格參與者？</span><span class="sxs-lookup"><span data-stu-id="f9dec-109">Who are the contacts and what are the processes for becoming an accredited participant?</span></span>
- <span data-ttu-id="f9dec-110">誰是合格的識別資訊提供者 (亦稱為「宣告提供者」)？他們能提供哪些資訊？</span><span class="sxs-lookup"><span data-stu-id="f9dec-110">Who are the accredited identity information providers (also known as "claims providers") and what do they offer?</span></span>
- <span data-ttu-id="f9dec-111">誰是合格的信賴憑證者？其要求條件為何？(後者為選擇性問題)</span><span class="sxs-lookup"><span data-stu-id="f9dec-111">Who are the accredited relying parties (and optionally, what do they require)?</span></span>
- <span data-ttu-id="f9dec-112">在技術方面，參與者有哪些「線上」互通性需求？</span><span class="sxs-lookup"><span data-stu-id="f9dec-112">What are the technical “on the wire” interoperability requirements for participants?</span></span>
- <span data-ttu-id="f9dec-113">必須強制執行哪些作業「執行階段」規則，以便交換數位身分識別資訊？</span><span class="sxs-lookup"><span data-stu-id="f9dec-113">What are the operational “runtime” rules that must be enforced for exchanging digital identity information?</span></span>

<span data-ttu-id="f9dec-114">為了回答上述所有問題，使用識別體驗架構的 Azure AD B2C 自訂原則會使用信任架構 (TF) 結構。</span><span class="sxs-lookup"><span data-stu-id="f9dec-114">To answer all these questions, Azure AD B2C custom policies that use the Identity Experience Framework use the Trust Framework (TF) construct.</span></span> <span data-ttu-id="f9dec-115">讓我們來看一下這個結構，並想想它能提供什麼。</span><span class="sxs-lookup"><span data-stu-id="f9dec-115">Let’s consider this construct and what it provides.</span></span>

## <a name="understand-the-trust-framework-and-federation-management-foundation"></a><span data-ttu-id="f9dec-116">了解信任架構和同盟管理基礎</span><span class="sxs-lookup"><span data-stu-id="f9dec-116">Understand the Trust Framework and federation management foundation</span></span>

<span data-ttu-id="f9dec-117">信任架構是身分識別、安全性、隱私權和資料保護原則的書面規格，相關社群中的參與者都必須遵守此規格。</span><span class="sxs-lookup"><span data-stu-id="f9dec-117">The Trust Framework is a written specification of the identity, security, privacy, and data protection policies to which participants in a community of interest must conform.</span></span>

<span data-ttu-id="f9dec-118">同盟身分識別可作為基礎，來實現網際網路規模的使用者身分識別保證。</span><span class="sxs-lookup"><span data-stu-id="f9dec-118">Federated identity provides a basis for achieving end-user identity assurance at Internet scale.</span></span> <span data-ttu-id="f9dec-119">藉由將身分識別管理工作委派給第三方，使用者就能對多個信賴憑證者重複使用單一數位身分識別。</span><span class="sxs-lookup"><span data-stu-id="f9dec-119">By delegating identity management to third parties, a single digital identity for an end user can be reused with multiple relying parties.</span></span>  

<span data-ttu-id="f9dec-120">想要保證身分識別，需要識別提供者 (IdP) 和屬性提供者 (AtP) 共同遵守特定的安全性、隱私權和作業方面的原則與作法。</span><span class="sxs-lookup"><span data-stu-id="f9dec-120">Identity assurance requires that identity providers (IdPs) and attribute providers (AtPs) adhere to specific security, privacy, and operational policies and practices.</span></span>  <span data-ttu-id="f9dec-121">如果他們無法執行直接審查，信賴憑證者 (RP) 就必須對他們選擇要合作的 IdP 和 AtP 發展信任關係。</span><span class="sxs-lookup"><span data-stu-id="f9dec-121">If they can't perform direct inspections, relying parties (RPs) must develop trust relationships with the IdPs and AtPs they choose to work with.</span></span>  

<span data-ttu-id="f9dec-122">由於數位身分識別資訊的取用者和提供者數目增加，因此，很難繼續在雙方之間管理這些信任關係，或甚至在雙方之間交換所需的中繼資料以連線到網路。</span><span class="sxs-lookup"><span data-stu-id="f9dec-122">As the number of consumers and providers of digital identity information grows, it's difficult to continue pairwise management of these trust relationships, or even the pairwise exchange of the technical metadata that's required for network connectivity.</span></span>  <span data-ttu-id="f9dec-123">同盟中樞在解決這些問題上，只有些許成就。</span><span class="sxs-lookup"><span data-stu-id="f9dec-123">Federation hubs have achieved only limited success at solving these problems.</span></span>

### <a name="what-a-trust-framework-specification-defines"></a><span data-ttu-id="f9dec-124">信任架構規格定義的內容</span><span class="sxs-lookup"><span data-stu-id="f9dec-124">What a Trust Framework specification defines</span></span>
<span data-ttu-id="f9dec-125">TF 是 Open Identity Exchange (OIX) 信任架構模型的關鍵，在此模型中，每個相關社群都會受到特定 TF 規格的控管。</span><span class="sxs-lookup"><span data-stu-id="f9dec-125">TFs are the linchpins of the Open Identity Exchange (OIX) Trust Framework model, where each community of interest is governed by a particular TF specification.</span></span> <span data-ttu-id="f9dec-126">這類 TF 規範會定義︰</span><span class="sxs-lookup"><span data-stu-id="f9dec-126">Such a TF specification defines:</span></span>

- <span data-ttu-id="f9dec-127">**相關社群的安全性和隱私權計量，這些計量的定義如下︰**</span><span class="sxs-lookup"><span data-stu-id="f9dec-127">**The security and privacy metrics for the community of interest with the definition of:**</span></span>
    - <span data-ttu-id="f9dec-128">參與者所提供/要求的保證等級 (LOA)，例如，一組有先後次序的信賴評等，用以表示數位身分識別資訊的真實性。</span><span class="sxs-lookup"><span data-stu-id="f9dec-128">The levels of assurance (LOA) that are offered/required by participants; for example, an ordered set of confidence ratings for the authenticity of digital identity information.</span></span>
    - <span data-ttu-id="f9dec-129">參與者所提供/要求的保護等級 (LOP)，例如，一組有先後次序的信賴評等，用以表示相關社群參與者所處理之數位身分識別資訊的保護程度。</span><span class="sxs-lookup"><span data-stu-id="f9dec-129">The levels of protection (LOP) that are offered/required by participants; for example, an ordered set of confidence ratings for the protection of digital identity information that's handled by participants in the community of interest.</span></span>

- <span data-ttu-id="f9dec-130">**參與者所提供/要求之數位身分識別資訊的說明**。</span><span class="sxs-lookup"><span data-stu-id="f9dec-130">**The description of the digital identity information that's offered/required by participants**.</span></span>

- <span data-ttu-id="f9dec-131">**相關技術原則，適用於生產和取用數位身分識別資訊，乃至於測量 LOA 和 LOP。這些書面原則通常包含以下幾類原則：**</span><span class="sxs-lookup"><span data-stu-id="f9dec-131">**The technical policies for production and consumption of digital identity information, and thus for measuring LOA and LOP. These written policies typically include the following categories of policies:**</span></span>
    - <span data-ttu-id="f9dec-132">身分識別證明原則，例如︰個人的身分識別資訊受到多嚴格的審查？</span><span class="sxs-lookup"><span data-stu-id="f9dec-132">Identity proofing policies, for example: *How strongly is a person’s identity information vetted?*</span></span>
    - <span data-ttu-id="f9dec-133">安全性原則，例如︰資訊的完整性和機密性受到多嚴格的保護？</span><span class="sxs-lookup"><span data-stu-id="f9dec-133">Security policies, for example: *How strongly are information integrity and confidentiality protected?*</span></span>
    - <span data-ttu-id="f9dec-134">隱私權原則，例如︰使用者對於個人識別資訊 (PII) 擁有何種控制權？</span><span class="sxs-lookup"><span data-stu-id="f9dec-134">Privacy policies, for example: *What control does a user have over personal identifiable information (PII)*?</span></span>
    - <span data-ttu-id="f9dec-135">生存能力原則，例如︰若提供者停止營業，PII 功能的持續性和保護如何運作？</span><span class="sxs-lookup"><span data-stu-id="f9dec-135">Survivability policies, for example: *If a provider ceases operations, how does continuity and protection of PII function?*</span></span>

- <span data-ttu-id="f9dec-136">**適用於生產和取用數位身分識別資訊的技術設定檔。這些設定檔包括：**</span><span class="sxs-lookup"><span data-stu-id="f9dec-136">**The technical profiles for production and consumption of digital identity information. These profiles include:**</span></span>
    - <span data-ttu-id="f9dec-137">界定在指定的 LOA 下，數位身分識別資訊所適用的介面。</span><span class="sxs-lookup"><span data-stu-id="f9dec-137">Scope interfaces for which digital identity information is available at a specified LOA.</span></span>
    - <span data-ttu-id="f9dec-138">線上互通性的技術需求。</span><span class="sxs-lookup"><span data-stu-id="f9dec-138">Technical requirements for on-the-wire interoperability.</span></span>

- <span data-ttu-id="f9dec-139">**社群參與者可執行之各種角色以及要擔任這些角色所需之資格的說明。**</span><span class="sxs-lookup"><span data-stu-id="f9dec-139">**The descriptions of the various roles that participants in the community can perform and the qualifications that are required to fulfill these roles.**</span></span>

<span data-ttu-id="f9dec-140">因此，TF 規範會控管相關社群 (信賴憑證者、身分識別和屬性提供者，以及屬性驗證者) 的參與者彼此之間如何交換身分識別資訊。</span><span class="sxs-lookup"><span data-stu-id="f9dec-140">Thus a TF specification governs how identity information is exchanged between the participants of the community of interest: relying parties, identity and attribute providers, and attribute verifiers.</span></span>

<span data-ttu-id="f9dec-141">TF 規格是一或多份文件，可供您參考如何對管制社群內數位身分識別資訊之判斷提示和取用的相關社群進行控管。</span><span class="sxs-lookup"><span data-stu-id="f9dec-141">A TF specification is one or multiple documents that serve as a reference for the governance of the community of interest that regulates the assertion and consumption of digital identity information within the community.</span></span> <span data-ttu-id="f9dec-142">它是一組記載下來的原則和程序，其設計目的是為相關社群成員之間的線上交易所使用的數位身分識別建立信任。</span><span class="sxs-lookup"><span data-stu-id="f9dec-142">It's a documented set of policies and procedures designed to establish trust in the digital identities that are used for online transactions between members of a community of interest.</span></span>  

<span data-ttu-id="f9dec-143">換句話說，TF 規格會為社群定義適用於建立可行之同盟身分識別生態系統的規則。</span><span class="sxs-lookup"><span data-stu-id="f9dec-143">In other words, a TF specification defines the rules for creating a viable federated identity ecosystem for a community.</span></span>

<span data-ttu-id="f9dec-144">目前已普遍同意這類方法的好處。</span><span class="sxs-lookup"><span data-stu-id="f9dec-144">Currently there's widespread agreement on the benefit of such an approach.</span></span> <span data-ttu-id="f9dec-145">毋庸置疑地，信任架構規格會促進數位身分識別生態系統的發展，並讓此系統具有可驗證的安全性、保證和隱私權特性，這表示這些規格能夠跨多個相關社群重複使用。</span><span class="sxs-lookup"><span data-stu-id="f9dec-145">There's no doubt that trust framework specifications facilitate the development of digital identity ecosystems with verifiable security, assurance and privacy characteristics, meaning that they can be reused across multiple communities of interest.</span></span>

<span data-ttu-id="f9dec-146">基於這個理由，使用識別體驗架構的 Azure AD B2C 自訂原則會使用此規格作為其 TF 資料表現方式的基礎，以促進互通性。</span><span class="sxs-lookup"><span data-stu-id="f9dec-146">For that reason, Azure AD B2C custom policies that use the Identity Experience Framework uses the specification as the basis of its data representation for a TF to facilitate interoperability.</span></span>  

<span data-ttu-id="f9dec-147">利用識別體驗架構的 Azure AD B2C 自訂原則，會以混用人類和機器可讀取之資料的方式來表示 TF 規範。</span><span class="sxs-lookup"><span data-stu-id="f9dec-147">Azure AD B2C Custom policies that leverage the Identity Experience Framework represent a TF specification as a mixture of human and machine-readable data.</span></span> <span data-ttu-id="f9dec-148">此模型的部分小節 (通常是更控管導向的小節) 會表示為對已發行安全性和隱私權原則文件以及相關程序 (如果有的話) 的參考。</span><span class="sxs-lookup"><span data-stu-id="f9dec-148">Some sections of this model (typically sections that are more oriented toward governance) are represented as references to published security and privacy policy documentation along with the related procedures (if any).</span></span> <span data-ttu-id="f9dec-149">其他各節會詳細描述設定中繼資料和執行階段規則，以利作業自動化。</span><span class="sxs-lookup"><span data-stu-id="f9dec-149">Other sections describe in detail the configuration metadata and runtime rules that facilitate operational automation.</span></span>

## <a name="understand-trust-framework-policies"></a><span data-ttu-id="f9dec-150">了解信任架構原則</span><span class="sxs-lookup"><span data-stu-id="f9dec-150">Understand Trust Framework policies</span></span>

<span data-ttu-id="f9dec-151">在實作方面，TF 規格包含一組原則，可讓您完整控制身分識別行為和體驗。</span><span class="sxs-lookup"><span data-stu-id="f9dec-151">In terms of implementation, the TF specification consists of a set of policies that allow complete control over identity behaviors and experiences.</span></span>  <span data-ttu-id="f9dec-152">利用識別體驗架構的 Azure AD B2C 自訂原則，可讓您透過這類能定義和設定的宣告式原則來撰寫及建立自己的 TF：</span><span class="sxs-lookup"><span data-stu-id="f9dec-152">Azure AD B2C custom policies that leverage the Identity Experience Framework enable you to author and create your own TF through such declarative policies that can define and configure:</span></span>

- <span data-ttu-id="f9dec-153">文件參考，以定義與 TF 有關之社群的同盟身分識別生態系統。</span><span class="sxs-lookup"><span data-stu-id="f9dec-153">The document reference or references that define the federated identity ecosystem of the community that relates to the TF.</span></span> <span data-ttu-id="f9dec-154">文件參考是 TF 文件的連結。</span><span class="sxs-lookup"><span data-stu-id="f9dec-154">They are links to the TF documentation.</span></span> <span data-ttu-id="f9dec-155">(預先定義的) 作業「執行階段」規則或使用者旅程，後者會自動執行及/或控制宣告的交換和使用。</span><span class="sxs-lookup"><span data-stu-id="f9dec-155">The (predefined) operational “runtime” rules, or the user journeys that automate and/or control the exchange and usage of the claims.</span></span> <span data-ttu-id="f9dec-156">這些使用者旅程會與 LOA (和 LOP) 相關聯。</span><span class="sxs-lookup"><span data-stu-id="f9dec-156">These user journeys are associated with a LOA (and a LOP).</span></span> <span data-ttu-id="f9dec-157">原則所具備的使用者旅程圖因此會有不同的 LOA (和 LOP)。</span><span class="sxs-lookup"><span data-stu-id="f9dec-157">A policy can therefore have user journeys with varying LOAs (and LOPs).</span></span>

- <span data-ttu-id="f9dec-158">相關社群中的身分識別和屬性提供者或宣告提供者，以及這些提供者所支援的技術設定檔以及與他們相關的 (頻外) LOA/LOP 認證。</span><span class="sxs-lookup"><span data-stu-id="f9dec-158">The identity and attribute providers, or the claims providers, in the community of interest and the technical profiles they support along with the (out-of-band) LOA/LOP accreditation that relates to them.</span></span>

- <span data-ttu-id="f9dec-159">與屬性驗證者或宣告提供者的整合。</span><span class="sxs-lookup"><span data-stu-id="f9dec-159">The integration with attribute verifiers or  claims providers.</span></span>

- <span data-ttu-id="f9dec-160">社群中的信賴憑證者 (依推斷)。</span><span class="sxs-lookup"><span data-stu-id="f9dec-160">The relying parties in the community (by inference).</span></span>

- <span data-ttu-id="f9dec-161">用於在參與者之間建立網路通訊的中繼資料。</span><span class="sxs-lookup"><span data-stu-id="f9dec-161">The metadata for establishing network communications between participants.</span></span> <span data-ttu-id="f9dec-162">在交易過程中，此中繼資料以及技術設定檔會用來在信賴憑證者和其他社群參與者之間檢測「線上」互通性。</span><span class="sxs-lookup"><span data-stu-id="f9dec-162">This metadata, along with the technical profiles, are used during a transaction to plumb “on the wire” interoperability between the relying party and other community participants.</span></span>

- <span data-ttu-id="f9dec-163">通訊協定轉換 (例如，SAML、OAuth2、WS-同盟和 OpenID Connect)，如果有的話。</span><span class="sxs-lookup"><span data-stu-id="f9dec-163">The protocol conversion if any (for example, SAML, OAuth2, WS-Federation, and OpenID Connect).</span></span>

- <span data-ttu-id="f9dec-164">驗證需求。</span><span class="sxs-lookup"><span data-stu-id="f9dec-164">The authentication requirements.</span></span>

- <span data-ttu-id="f9dec-165">多重要素協調流程，如果有的話。</span><span class="sxs-lookup"><span data-stu-id="f9dec-165">The multifactor orchestration if any.</span></span>

- <span data-ttu-id="f9dec-166">針對相關社群參與者，適用且對應之所有宣告的共用結構描述。</span><span class="sxs-lookup"><span data-stu-id="f9dec-166">A shared schema for all the claims that are available and mappings to participants of a community of interest.</span></span>

- <span data-ttu-id="f9dec-167">所有宣告轉換 (以及此內容中可能的資料最小化)，以支撐宣告的交換和使用。</span><span class="sxs-lookup"><span data-stu-id="f9dec-167">All the claims transformations, along with the possible data minimization in this context, to sustain the exchange and usage of the claims.</span></span>

- <span data-ttu-id="f9dec-168">繫結和加密。</span><span class="sxs-lookup"><span data-stu-id="f9dec-168">The binding and encryption.</span></span>

- <span data-ttu-id="f9dec-169">宣告儲存體。</span><span class="sxs-lookup"><span data-stu-id="f9dec-169">The claims storage.</span></span>

### <a name="understand-claims"></a><span data-ttu-id="f9dec-170">了解宣告</span><span class="sxs-lookup"><span data-stu-id="f9dec-170">Understand claims</span></span>

> [!NOTE]
> <span data-ttu-id="f9dec-171">我們將所有可交換的可能身分識別資訊類型統稱為「宣告」︰有關使用者的驗證認證、身分識別審查、通訊裝置、實體位置、個人識別屬性等項目的宣告。</span><span class="sxs-lookup"><span data-stu-id="f9dec-171">We collectively refer to all the possible types of identity information that might be exchanged as "claims": claims about an end user’s authentication credential, identity vetting, communication device, physical location, personally identifying attributes, and so on.</span></span>  
>
> <span data-ttu-id="f9dec-172">我們使用「宣告」一詞，而非「屬性」，是因為在線上交易的情況下，這些資料構件並非信賴憑證者可直接驗證的事實。</span><span class="sxs-lookup"><span data-stu-id="f9dec-172">We use the term "claims"--rather than "attributes"--because in online transactions, these data artifacts are not facts that can be directly verified by the relying party.</span></span> <span data-ttu-id="f9dec-173">確切地說，它們是關於信賴憑證者必須產生足夠信心來授與使用者所要求交易之事實的判斷提示或宣告。</span><span class="sxs-lookup"><span data-stu-id="f9dec-173">Rather they're assertions, or claims, about facts for which the relying party must develop sufficient confidence to grant the end user’s requested transaction.</span></span>  
>
> <span data-ttu-id="f9dec-174">我們也會使用「宣告」一詞，因為使用識別體驗架構的 Azure AD B2C 自訂原則是針對以一致的方式簡化所有數位身分識別資訊類型的交換所設計，而不論針對驗證使用者或擷取屬性工作所定義的基礎通訊協定為何。</span><span class="sxs-lookup"><span data-stu-id="f9dec-174">We also use the term "claims" because Azure AD B2C custom policies that use the Identity Experience Framework are designed to simplify the exchange of all types of digital identity information in a consistent manner regardless of whether the underlying protocol is defined for user authentication or attribute retrieval.</span></span>  <span data-ttu-id="f9dec-175">同樣地，當我們不想區別提供者專屬的函式時，會使用「宣告提供者」一詞來統稱識別提供者、屬性提供者和屬性驗證者。</span><span class="sxs-lookup"><span data-stu-id="f9dec-175">Likewise, we use the term "claims providers" to collectively refer to identity providers, attribute providers, and attribute verifiers when we do not want to distinguish between their specific functions.</span></span>   

<span data-ttu-id="f9dec-176">因此，這些原則會控管如何在信賴憑證者、識別提供者和屬性提供者以及屬性驗證者之間交換身分識別資訊。</span><span class="sxs-lookup"><span data-stu-id="f9dec-176">Thus they govern how identity information is exchanged between a relying party, identity and attribute providers, and attribute verifiers.</span></span> <span data-ttu-id="f9dec-177">這些原則會控制信賴憑證者的驗證工作需要使用哪一個識別提供者和屬性提供者。</span><span class="sxs-lookup"><span data-stu-id="f9dec-177">They control which identity and attribute providers are required for a relying party’s authentication.</span></span> <span data-ttu-id="f9dec-178">您應將這些原則視為特定領域語言 (DSL)，也就是特定應用程式定義域專用的電腦語言，並具有繼承、*if* 陳述式、多型。</span><span class="sxs-lookup"><span data-stu-id="f9dec-178">They should be considered as a domain-specific language (DSL), that is, a computer language that's specialized for a particular application domain with inheritance, *if* statements, polymorphism.</span></span>

<span data-ttu-id="f9dec-179">這些原則會在利用識別體驗架構的 Azure AD B2C 自訂原則中，構成 TF 建構中電腦可讀取的部分。</span><span class="sxs-lookup"><span data-stu-id="f9dec-179">These policies constitute the machine-readable portion of the TF construct in Azure AD B2C Custom policies leveraging the Identity Experience Framework.</span></span> <span data-ttu-id="f9dec-180">它們包含所有作業的詳細資料，包括宣告提供者的中繼資料和技術設定檔、宣告結構描述定義、宣告轉換函式，以及可填入的使用者旅程圖，以利作業的協調流程和自動化。</span><span class="sxs-lookup"><span data-stu-id="f9dec-180">They include all the operational details, including claims providers’ metadata and technical profiles, claims schema definitions, claims transformation functions, and user journeys that are filled in to facilitate operational orchestration and automation.</span></span>  

<span data-ttu-id="f9dec-181">它們會被假設為「即時文件」，因為其關於原則中宣告之有效參與者的內容很可能會隨著時間變更。</span><span class="sxs-lookup"><span data-stu-id="f9dec-181">They are assumed to be *living documents* because there is  a good chance that their contents will change over time concerning the active participants declared in the policies.</span></span> <span data-ttu-id="f9dec-182">此外，作為參與者的條款及條件也可能會變更。</span><span class="sxs-lookup"><span data-stu-id="f9dec-182">There is also the potential that the terms and conditions for being a participant might change.</span></span>  

<span data-ttu-id="f9dec-183">藉由讓信賴憑證者不會因為不同的宣告提供者/驗證者加入或離開原則集 (所代表的社群) 而不斷重新設定信任和連線，同盟的設定和維護已大幅簡化。</span><span class="sxs-lookup"><span data-stu-id="f9dec-183">Federation setup and maintenance are vastly simplified by shielding relying parties from ongoing trust and connectivity reconfigurations as different claims providers/verifiers join or leave (the community represented by) the set of policies.</span></span>

<span data-ttu-id="f9dec-184">互通性是另一項重大挑戰。</span><span class="sxs-lookup"><span data-stu-id="f9dec-184">Interoperability is another significant challenge.</span></span> <span data-ttu-id="f9dec-185">信賴憑證者不可能支援所有必要的通訊協定，因此您必須整合其他宣告提供者/驗證者。</span><span class="sxs-lookup"><span data-stu-id="f9dec-185">Additional claims providers/verifiers must be integrated, because relying parties are unlikely to support all the necessary protocols.</span></span> <span data-ttu-id="f9dec-186">Azure AD B2C 自訂原則可解決此問題，其方法是藉由支援業界標準的通訊協定，並在信賴憑證者和屬性提供者不支援相同的通訊協定時，套用特定的使用者旅程圖來調換要求。</span><span class="sxs-lookup"><span data-stu-id="f9dec-186">Azure AD B2C custom policies solve this problem by supporting industry-standard protocols and by applying specific user journeys to transpose requests when relying parties and attribute providers do not support the same protocol.</span></span>  

<span data-ttu-id="f9dec-187">使用者旅程圖包括通訊協定設定檔和中繼資料，其可供用來在信賴憑證者和其他參與者之間檢測「線上」互通性。</span><span class="sxs-lookup"><span data-stu-id="f9dec-187">User journeys include protocol profiles and metadata that are used to plumb “on the wire” interoperability between the relying party and other participants.</span></span> <span data-ttu-id="f9dec-188">身分識別資訊交換要求/回應訊息也會有適用的作業執行階段規則，以便強制它們符合 TF 規格中已發佈原則的規範。</span><span class="sxs-lookup"><span data-stu-id="f9dec-188">There are also operational runtime rules that are applied to identity information exchange request/response messages for enforcing compliance with published policies as part of the TF specification.</span></span> <span data-ttu-id="f9dec-189">使用者旅程圖的想法是自訂客戶體驗的關鍵。</span><span class="sxs-lookup"><span data-stu-id="f9dec-189">The idea of user journeys is key to the customization of the customer experience.</span></span> <span data-ttu-id="f9dec-190">它也會闡述系統在通訊協定層級的運作方式。</span><span class="sxs-lookup"><span data-stu-id="f9dec-190">It also sheds light on how the system works at the protocol level.</span></span>

<span data-ttu-id="f9dec-191">在該基礎上，信賴憑證者應用程式和入口網站可以根據其內容，叫用利用識別體驗架構的 Azure AD B2C 自訂原則來傳遞特定原則的名稱，並精確取得其想要的行為和資訊交換，而不會有任何混亂、複雜或風險。</span><span class="sxs-lookup"><span data-stu-id="f9dec-191">On that basis, relying party applications and portals can, depending on their context, invoke Azure AD B2C custom policies that leverage the Identity Experience Framework passing the name of a specific policy and get precisely the behavior and information exchange they want without any muss, fuss, or risk.</span></span>
