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
ms.openlocfilehash: 979b8a264eb819ee4a208b9171a53a5ffbf062c3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="release-notes-for-azure-active-directory-b2c-custom-policy-public-preview"></a><span data-ttu-id="b149f-103">Azure Active Directory B2C 自訂原則公開預覽版的版本資訊</span><span class="sxs-lookup"><span data-stu-id="b149f-103">Release notes for Azure Active Directory B2C custom policy public preview</span></span>
<span data-ttu-id="b149f-104">hello 自訂原則的功能集現在已可供公開預覽版供所有的 Azure Active Directory B2C 下評估 (Azure AD B2C) 客戶。</span><span class="sxs-lookup"><span data-stu-id="b149f-104">hello custom policy feature set is now available for evaluation under public preview for all Azure Active Directory B2C (Azure AD B2C) customers.</span></span> <span data-ttu-id="b149f-105">此功能集為目標的進階身分識別開發人員在建置 hello 最複雜的身分識別解決方案。</span><span class="sxs-lookup"><span data-stu-id="b149f-105">This feature set is targeted at advanced identity developers building hello most complex identity solutions.</span></span>  

<span data-ttu-id="b149f-106">現在，此功能集需要開發人員 tooconfigure hello 身分識別體驗架構透過直接編輯的 XML 檔案。</span><span class="sxs-lookup"><span data-stu-id="b149f-106">Today, this feature set requires developers tooconfigure hello Identity Experience Framework directly via XML file editing.</span></span> <span data-ttu-id="b149f-107">用這種方式進行設定的效果最好，卻也複雜。</span><span class="sxs-lookup"><span data-stu-id="b149f-107">This method of configuration is powerful and complex.</span></span> <span data-ttu-id="b149f-108">進階身分識別開發人員使用 hello 身分識別體驗架構應該規劃 tooinvest 一些時間完成逐步解說，以及讀取參考文件。</span><span class="sxs-lookup"><span data-stu-id="b149f-108">Advanced identity developers using hello Identity Experience Framework should plan tooinvest some time completing walk-throughs and reading reference documents.</span></span> 

## <a name="features-included-in-this-public-preview"></a><span data-ttu-id="b149f-109">此公開預覽版包含的功能</span><span class="sxs-lookup"><span data-stu-id="b149f-109">Features included in this public preview</span></span>
<span data-ttu-id="b149f-110">Hello hello 公開預覽版中導入了新的功能，開發人員可以執行下列工作的 hello:</span><span class="sxs-lookup"><span data-stu-id="b149f-110">With hello new features introduced in hello public preview, developers can perform hello following tasks:</span></span><br>

* <span data-ttu-id="b149f-111">使用自訂原則來撰寫和上傳自訂驗證使用者旅程。</span><span class="sxs-lookup"><span data-stu-id="b149f-111">Author and upload custom authentication user journeys by using custom policies.</span></span> 
   * <span data-ttu-id="b149f-112">逐步將使用者旅程描述為宣告提供者之間的交換。</span><span class="sxs-lookup"><span data-stu-id="b149f-112">Describe user journeys step-by-step as exchanges between claims providers.</span></span> 
   * <span data-ttu-id="b149f-113">定義使用者旅程中的條件式分支。</span><span class="sxs-lookup"><span data-stu-id="b149f-113">Define conditional branching in user journeys.</span></span> 
* <span data-ttu-id="b149f-114">將啟用 REST API 功能的服務整合到您的自訂驗證使用者旅程。</span><span class="sxs-lookup"><span data-stu-id="b149f-114">Integrate REST API-enabled services in your custom authentication user journeys.</span></span>  
* <span data-ttu-id="b149f-115">加入與 hello OpenIDConnect 標準與相容的身分識別提供者同盟。</span><span class="sxs-lookup"><span data-stu-id="b149f-115">Add federation with identity providers that are compliant with hello OpenIDConnect standard.</span></span> <br>
* <span data-ttu-id="b149f-116">加入與遵守 toohello SAML 2.0 通訊協定的身分識別提供者同盟。</span><span class="sxs-lookup"><span data-stu-id="b149f-116">Add federation with identity providers that adhere toohello SAML 2.0 protocol.</span></span> 

## <a name="terms-of-hello-public-preview"></a><span data-ttu-id="b149f-117">Hello 公用預覽中的條款</span><span class="sxs-lookup"><span data-stu-id="b149f-117">Terms of hello public preview</span></span>

* <span data-ttu-id="b149f-118">我們建議您僅為了評估目的 toouse hello 新功能。</span><span class="sxs-lookup"><span data-stu-id="b149f-118">We encourage you toouse hello new features for evaluation purposes only.</span></span><br>
* <span data-ttu-id="b149f-119">新功能不適合在生產環境中使用。</span><span class="sxs-lookup"><span data-stu-id="b149f-119">The new features are not intended for use in a production environment.</span></span><br>
* <span data-ttu-id="b149f-120">服務等級協定 (Sla) 不會套用 toohello 新功能。</span><span class="sxs-lookup"><span data-stu-id="b149f-120">Service level agreements (SLAs) do not apply toohello new features.</span></span> <br>
* <span data-ttu-id="b149f-121">您可以透過標準支援管道來提出支援要求。</span><span class="sxs-lookup"><span data-stu-id="b149f-121">Support requests can be filed through regular support channels.</span></span> <br>
* <span data-ttu-id="b149f-122">正式運作的日期還未確定。</span><span class="sxs-lookup"><span data-stu-id="b149f-122">There is no promised date for general availability.</span></span><br>
* <span data-ttu-id="b149f-123">我們決定，以及因為任何原因，Microsoft 可以加上旗標和拒絕或限制案例和使用者皆超過 hello 範圍 hello Azure AD B2C 產品教授 tooserve 做為客戶識別和存取管理 (CIAM) 平台。</span><span class="sxs-lookup"><span data-stu-id="b149f-123">At our discretion, and for any reason, Microsoft can flag and reject or restrict scenarios and user journeys that exceed hello scope of hello Azure AD B2C product charter tooserve as a customer identity and access management (CIAM) platform.</span></span>

## <a name="responsibilities-of-custom-policy-feature-set-developers"></a><span data-ttu-id="b149f-124">自訂原則功能集開發人員的責任</span><span class="sxs-lookup"><span data-stu-id="b149f-124">Responsibilities of custom policy feature-set developers</span></span>
<span data-ttu-id="b149f-125">手動原則設定會授與較低層級存取 toohello 基礎平台的 Azure AD B2C 加以 hello 建立唯一的、 可完全自訂信任架構。</span><span class="sxs-lookup"><span data-stu-id="b149f-125">Manual policy configuration grants lower-level access toohello underlying platform of Azure AD B2C and results in hello creation of a unique, fully customizable trust framework.</span></span> <span data-ttu-id="b149f-126">可能的排列方式，自訂身分識別提供者，信任關係的外部服務，與逐步工作流程整合進階開發人員使用他們的 hello 置於更高的要求。</span><span class="sxs-lookup"><span data-stu-id="b149f-126">The possible permutations of custom identity providers, trust relationships, integrations with external services, and step-by-step workflows place greater demands on hello advanced developers consuming them.</span></span>

<span data-ttu-id="b149f-127">toofully 權益從 hello 公開預覽，我們建議開發人員的耗用 hello 自訂原則的功能集遵守 toohello 指導方針：</span><span class="sxs-lookup"><span data-stu-id="b149f-127">toofully benefit from hello public preview, we suggest that developers consuming hello custom policy feature set adhere toohello following guidelines:</span></span>
* <span data-ttu-id="b149f-128">熟悉的 hello 識別經驗引擎 hello 設定語言和金鑰/密碼管理。</span><span class="sxs-lookup"><span data-stu-id="b149f-128">Become familiar with hello configuration language of hello Identity Experience Engine and key/secrets management.</span></span>
* <span data-ttu-id="b149f-129">完整掌控案例和自訂整合。</span><span class="sxs-lookup"><span data-stu-id="b149f-129">Take ownership of scenarios and custom integrations.</span></span>
* <span data-ttu-id="b149f-130">有系統地執行案例測試。</span><span class="sxs-lookup"><span data-stu-id="b149f-130">Perform methodical scenario testing.</span></span>
* <span data-ttu-id="b149f-131">對至少一個開發和測試環境以及一個生產環境遵循軟體開發和分段進行的最佳做法。</span><span class="sxs-lookup"><span data-stu-id="b149f-131">Follow software development and staging best practices with a minimum of one development and testing environment and one production environment.</span></span>
* <span data-ttu-id="b149f-132">隨時掌握有關從 hello 身分識別提供者和服務整合與新的開發。</span><span class="sxs-lookup"><span data-stu-id="b149f-132">Stay informed about new developments from hello identity providers and services you integrate with.</span></span> <span data-ttu-id="b149f-133">比方說，追蹤的機密資料中的排程和解除排程變更 toohello 服務的變更。</span><span class="sxs-lookup"><span data-stu-id="b149f-133">For example, keep track of changes in secrets and of scheduled and unscheduled changes toohello service.</span></span>
* <span data-ttu-id="b149f-134">設定使用中的監視和監視的實際執行環境的 hello 回應性。</span><span class="sxs-lookup"><span data-stu-id="b149f-134">Set up active monitoring, and monitor hello responsiveness of production environments.</span></span>
* <span data-ttu-id="b149f-135">最新的連絡人電子郵件地址，並保持回應 toohello Microsoft live 網站小組電子郵件。</span><span class="sxs-lookup"><span data-stu-id="b149f-135">Keep contact email addresses current, and stay responsive toohello Microsoft live-site team emails.</span></span>
* <span data-ttu-id="b149f-136">建議使用的 toodo 來 hello Microsoft live 網站小組時，請採取及時的動作。</span><span class="sxs-lookup"><span data-stu-id="b149f-136">Take timely action when advised toodo so by hello Microsoft live-site team.</span></span> 


>[!NOTE]
><span data-ttu-id="b149f-137">這些功能最終可能包含在 Azure AD 內建原則，使其更容易存取 tooall 開發人員。</span><span class="sxs-lookup"><span data-stu-id="b149f-137">These features might eventually be included in Azure AD built-in policies, making them more accessible tooall developers.</span></span>

## <a name="next-steps"></a><span data-ttu-id="b149f-138">後續步驟</span><span class="sxs-lookup"><span data-stu-id="b149f-138">Next steps</span></span>
<span data-ttu-id="b149f-139">[開始使用自訂原則](active-directory-b2c-get-started-custom.md)。</span><span class="sxs-lookup"><span data-stu-id="b149f-139">[Get started with custom policies](active-directory-b2c-get-started-custom.md).</span></span>
