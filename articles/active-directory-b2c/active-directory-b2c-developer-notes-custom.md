---
title: "Azure Active Directory B2C：開發人員的自訂原則使用注意事項 | Microsoft Docs"
description: "開發人員在使用自訂原則來設定和維護 Azure AD B2C 時的注意事項"
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
ms.date: 05/05/2017
ms.author: joroja
ms.openlocfilehash: a5f222e5b11e05286152a9f1cc55d2c3fc27a9dc
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="release-notes-for-azure-active-directory-b2c-custom-policy-public-preview"></a><span data-ttu-id="08779-103">Azure Active Directory B2C 自訂原則公開預覽版的版本資訊</span><span class="sxs-lookup"><span data-stu-id="08779-103">Release notes for Azure Active Directory B2C custom policy public preview</span></span>
<span data-ttu-id="08779-104">所有 Azure Active Directory B2C (Azure AD B2C) 客戶現在已可評估自訂原則功能集 (公開預覽狀態)。</span><span class="sxs-lookup"><span data-stu-id="08779-104">The custom policy feature set is now available for evaluation under public preview for all Azure Active Directory B2C (Azure AD B2C) customers.</span></span> <span data-ttu-id="08779-105">此功能集的適用對象是正在建置最複雜身分識別解決方案的進階身分識別開發人員。</span><span class="sxs-lookup"><span data-stu-id="08779-105">This feature set is targeted at advanced identity developers building the most complex identity solutions.</span></span>  

<span data-ttu-id="08779-106">目前，此功能集需要開發人員直接透過 XML 檔案編輯來設定識別體驗架構。</span><span class="sxs-lookup"><span data-stu-id="08779-106">Today, this feature set requires developers to configure the Identity Experience Framework directly via XML file editing.</span></span> <span data-ttu-id="08779-107">用這種方式進行設定的效果最好，卻也複雜。</span><span class="sxs-lookup"><span data-stu-id="08779-107">This method of configuration is powerful and complex.</span></span> <span data-ttu-id="08779-108">使用識別體驗架構的進階身分識別開發人員應該要規劃投入時間，以完成逐步解說課程和閱讀參考文件。</span><span class="sxs-lookup"><span data-stu-id="08779-108">Advanced identity developers using the Identity Experience Framework should plan to invest some time completing walk-throughs and reading reference documents.</span></span> 

## <a name="features-included-in-this-public-preview"></a><span data-ttu-id="08779-109">此公開預覽版包含的功能</span><span class="sxs-lookup"><span data-stu-id="08779-109">Features included in this public preview</span></span>
<span data-ttu-id="08779-110">透過公開預覽中所引進的新功能，開發人員可以執行下列工作：</span><span class="sxs-lookup"><span data-stu-id="08779-110">With the new features introduced in the public preview, developers can perform the following tasks:</span></span><br>

* <span data-ttu-id="08779-111">使用自訂原則來撰寫和上傳自訂驗證使用者旅程。</span><span class="sxs-lookup"><span data-stu-id="08779-111">Author and upload custom authentication user journeys by using custom policies.</span></span> 
   * <span data-ttu-id="08779-112">逐步將使用者旅程描述為宣告提供者之間的交換。</span><span class="sxs-lookup"><span data-stu-id="08779-112">Describe user journeys step-by-step as exchanges between claims providers.</span></span> 
   * <span data-ttu-id="08779-113">定義使用者旅程中的條件式分支。</span><span class="sxs-lookup"><span data-stu-id="08779-113">Define conditional branching in user journeys.</span></span> 
* <span data-ttu-id="08779-114">將啟用 REST API 功能的服務整合到您的自訂驗證使用者旅程。</span><span class="sxs-lookup"><span data-stu-id="08779-114">Integrate REST API-enabled services in your custom authentication user journeys.</span></span>  
* <span data-ttu-id="08779-115">新增符合 OpenIDConnect 標準的識別提供者同盟。</span><span class="sxs-lookup"><span data-stu-id="08779-115">Add federation with identity providers that are compliant with the OpenIDConnect standard.</span></span> <br>
* <span data-ttu-id="08779-116">新增遵守 SAML 2.0 通訊協定的識別提供者同盟。</span><span class="sxs-lookup"><span data-stu-id="08779-116">Add federation with identity providers that adhere to the SAML 2.0 protocol.</span></span> 

## <a name="terms-of-the-public-preview"></a><span data-ttu-id="08779-117">公開預覽版的條款</span><span class="sxs-lookup"><span data-stu-id="08779-117">Terms of the public preview</span></span>

* <span data-ttu-id="08779-118">建議您只有在進行評估時才使用新功能。</span><span class="sxs-lookup"><span data-stu-id="08779-118">We encourage you to use the new features for evaluation purposes only.</span></span><br>
* <span data-ttu-id="08779-119">新功能不適合在生產環境中使用。</span><span class="sxs-lookup"><span data-stu-id="08779-119">The new features are not intended for use in a production environment.</span></span><br>
* <span data-ttu-id="08779-120">服務等級協定 (SLA) 不適用於新功能。</span><span class="sxs-lookup"><span data-stu-id="08779-120">Service level agreements (SLAs) do not apply to the new features.</span></span> <br>
* <span data-ttu-id="08779-121">您可以透過標準支援管道來提出支援要求。</span><span class="sxs-lookup"><span data-stu-id="08779-121">Support requests can be filed through regular support channels.</span></span> <br>
* <span data-ttu-id="08779-122">正式運作的日期還未確定。</span><span class="sxs-lookup"><span data-stu-id="08779-122">There is no promised date for general availability.</span></span><br>
* <span data-ttu-id="08779-123">若案例和使用者旅程超過 Azure AD B2C 產品可作為客戶身分識別與存取管理 (CIAM) 平台的許可範圍，Microsoft 會自行判斷 (以及因為任何原因) 而將其加上旗標並加以拒絕或施加限制。</span><span class="sxs-lookup"><span data-stu-id="08779-123">At our discretion, and for any reason, Microsoft can flag and reject or restrict scenarios and user journeys that exceed the scope of the Azure AD B2C product charter to serve as a customer identity and access management (CIAM) platform.</span></span>

## <a name="responsibilities-of-custom-policy-feature-set-developers"></a><span data-ttu-id="08779-124">自訂原則功能集開發人員的責任</span><span class="sxs-lookup"><span data-stu-id="08779-124">Responsibilities of custom policy feature-set developers</span></span>
<span data-ttu-id="08779-125">手動設定原則會對 Azure AD B2C 基礎平台授與較低層級的存取權，並建立可完全自訂的唯一信任架構。</span><span class="sxs-lookup"><span data-stu-id="08779-125">Manual policy configuration grants lower-level access to the underlying platform of Azure AD B2C and results in the creation of a unique, fully customizable trust framework.</span></span> <span data-ttu-id="08779-126">自訂識別提供者、信任關係、與外部服務的整合以及逐步工作流程會有各種可能的排列組合，因此使用這些組合的進階開發人員會遇到更嚴格的要求。</span><span class="sxs-lookup"><span data-stu-id="08779-126">The possible permutations of custom identity providers, trust relationships, integrations with external services, and step-by-step workflows place greater demands on the advanced developers consuming them.</span></span>

<span data-ttu-id="08779-127">為了充分獲得公開預覽版的好處，建議使用自訂原則功能集的開發人員遵守下列方針：</span><span class="sxs-lookup"><span data-stu-id="08779-127">To fully benefit from the public preview, we suggest that developers consuming the custom policy feature set adhere to the following guidelines:</span></span>
* <span data-ttu-id="08779-128">熟悉識別體驗引擎 (IEEE) 的設定語言和金鑰/密碼管理。</span><span class="sxs-lookup"><span data-stu-id="08779-128">Become familiar with the configuration language of the Identity Experience Engine and key/secrets management.</span></span>
* <span data-ttu-id="08779-129">完整掌控案例和自訂整合。</span><span class="sxs-lookup"><span data-stu-id="08779-129">Take ownership of scenarios and custom integrations.</span></span>
* <span data-ttu-id="08779-130">有系統地執行案例測試。</span><span class="sxs-lookup"><span data-stu-id="08779-130">Perform methodical scenario testing.</span></span>
* <span data-ttu-id="08779-131">對至少一個開發和測試環境以及一個生產環境遵循軟體開發和分段進行的最佳做法。</span><span class="sxs-lookup"><span data-stu-id="08779-131">Follow software development and staging best practices with a minimum of one development and testing environment and one production environment.</span></span>
* <span data-ttu-id="08779-132">掌握與您整合之識別提供者和服務的最新開發資訊。</span><span class="sxs-lookup"><span data-stu-id="08779-132">Stay informed about new developments from the identity providers and services you integrate with.</span></span> <span data-ttu-id="08779-133">例如，追蹤密碼的變更，以及服務的排程和未排程變更。</span><span class="sxs-lookup"><span data-stu-id="08779-133">For example, keep track of changes in secrets and of scheduled and unscheduled changes to the service.</span></span>
* <span data-ttu-id="08779-134">設定主動式監控，並監視生產環境的回應能力。</span><span class="sxs-lookup"><span data-stu-id="08779-134">Set up active monitoring, and monitor the responsiveness of production environments.</span></span>
* <span data-ttu-id="08779-135">保有最新的連絡人電子郵件地址，並持續回應 Microsoft 即時網站小組的電子郵件。</span><span class="sxs-lookup"><span data-stu-id="08779-135">Keep contact email addresses current, and stay responsive to the Microsoft live-site team emails.</span></span>
* <span data-ttu-id="08779-136">在 Microsoft 即時網站小組的建議下及時採取動作。</span><span class="sxs-lookup"><span data-stu-id="08779-136">Take timely action when advised to do so by the Microsoft live-site team.</span></span> 


>[!NOTE]
><span data-ttu-id="08779-137">這些功能最後可能會包含在 Azure AD 的內建原則中，以方便所有開發人員存取。</span><span class="sxs-lookup"><span data-stu-id="08779-137">These features might eventually be included in Azure AD built-in policies, making them more accessible to all developers.</span></span>

## <a name="next-steps"></a><span data-ttu-id="08779-138">後續步驟</span><span class="sxs-lookup"><span data-stu-id="08779-138">Next steps</span></span>
<span data-ttu-id="08779-139">[開始使用自訂原則](active-directory-b2c-get-started-custom.md)。</span><span class="sxs-lookup"><span data-stu-id="08779-139">[Get started with custom policies](active-directory-b2c-get-started-custom.md).</span></span>
