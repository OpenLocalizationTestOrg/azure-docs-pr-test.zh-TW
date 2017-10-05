---
title: "Azure Active Directory PoC 腳本組成要素 | Microsoft Docs"
description: "探索並快速實作身分識別和存取管理案例"
services: active-directory
keywords: "azure active directory, 腳本, 概念證明, PoC"
documentationcenter: 
author: dstefanMSFT
manager: asuthar
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 4/12/2017
ms.author: dstefan
ms.openlocfilehash: d2a0fe280f143d390f5e4ba40e0ebe92d8a4a837
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="azure-active-directory-proof-of-concept-playbook-ingredients"></a><span data-ttu-id="f79e2-104">Azure Active Directory 概念證明腳本組成要素</span><span class="sxs-lookup"><span data-stu-id="f79e2-104">Azure Active Directory Proof of Concept Playbook Ingredients</span></span> 

## <a name="theme"></a><span data-ttu-id="f79e2-105">佈景主題</span><span class="sxs-lookup"><span data-stu-id="f79e2-105">Theme</span></span>
<span data-ttu-id="f79e2-106">Azure AD 可在企業內提供多個領域的身分識別和存取解決方案。</span><span class="sxs-lookup"><span data-stu-id="f79e2-106">Azure AD provides identity and access solutions across multiple areas in the enterprise.</span></span> <span data-ttu-id="f79e2-107">我們將這些案例分為下列領域︰</span><span class="sxs-lookup"><span data-stu-id="f79e2-107">We classify the scenarios in the following areas:</span></span> 

* [<span data-ttu-id="f79e2-108">許多應用程式、一個身分識別</span><span class="sxs-lookup"><span data-stu-id="f79e2-108">Lots of apps, one identity</span></span>](active-directory-playbook-implementation.md#theme---lots-of-apps-one-identity) 
* [<span data-ttu-id="f79e2-109">增加您的安全性</span><span class="sxs-lookup"><span data-stu-id="f79e2-109">Increase your security</span></span>](active-directory-playbook-implementation.md#theme---increase-your-security) 
* [<span data-ttu-id="f79e2-110">使用自助式縮放比例</span><span class="sxs-lookup"><span data-stu-id="f79e2-110">Scale with Self Service</span></span>](active-directory-playbook-implementation.md#theme---scale-with-self-service) 

<span data-ttu-id="f79e2-111">定義佈景主題來制定概念證明 (Proof of Concept, PoC) 可協助您將心力集中在與業務目標配合，因為您一開始之所以會對概念證明感興趣，原因往往是業務目標。</span><span class="sxs-lookup"><span data-stu-id="f79e2-111">Defining a theme to frame the PoC helps to focus the efforts that resonates with business goals, which oftentimes are the triggers of the interest in a proof of concept in the first place.</span></span> 

## <a name="environment"></a><span data-ttu-id="f79e2-112">Environment</span><span class="sxs-lookup"><span data-stu-id="f79e2-112">Environment</span></span>

<span data-ttu-id="f79e2-113">請務必確定要用來提供 PoC 之環境的詳細資料。</span><span class="sxs-lookup"><span data-stu-id="f79e2-113">It is important to determine the details of the environment where you will deliver the PoC.</span></span> <span data-ttu-id="f79e2-114">理想狀況下，您可以在 PoC 完成後以此環境為基礎來進行建置。</span><span class="sxs-lookup"><span data-stu-id="f79e2-114">Ideally you can build upon it after the PoC is completed.</span></span> <span data-ttu-id="f79e2-115">目標環境很重要，因此請在盡量呈現真實環境和條件約束的額外負荷或其他考量之間取得適當平衡。</span><span class="sxs-lookup"><span data-stu-id="f79e2-115">The target environment is crucial and you should find the right balance between making it as real as possible and the overhead of constraints or extra considerations.</span></span> <span data-ttu-id="f79e2-116">PoC 的典型環境如下︰</span><span class="sxs-lookup"><span data-stu-id="f79e2-116">The typical environments for PoCs are:</span></span>
* <span data-ttu-id="f79e2-117">**生產︰**各種案例會實作在實際環境中，並已部署 Microsoft Cloud 服務 (生產 AD、Office 365、Azure AD 租用戶/SSO 解決方案)。</span><span class="sxs-lookup"><span data-stu-id="f79e2-117">**Production:** The scenarios will be implemented in your live environment and already deployed Microsoft Cloud services (production AD, Office 365, Azure AD tenant/SSO solution).</span></span> 
* <span data-ttu-id="f79e2-118">**使用者接受度測試 (UAT)/開發環境︰**您擁有測試基礎結構 (平行 AD，並可能有 Azure AD 租用戶/SSO 解決方案) 與類似生產環境的測試資料。</span><span class="sxs-lookup"><span data-stu-id="f79e2-118">**User Acceptance Test (UAT)/Dev environment:** You have test infrastructure (parallel AD and potentially Azure AD tenant/SSO solution) with test data that resembles production.</span></span> <span data-ttu-id="f79e2-119">測試環境一般可供企業中的多個專案共用。</span><span class="sxs-lookup"><span data-stu-id="f79e2-119">Typically, the test environment is shared across multiple projects in the enterprise.</span></span>

<span data-ttu-id="f79e2-120">本指南中的大部分案例皆具有附加特質。</span><span class="sxs-lookup"><span data-stu-id="f79e2-120">Most scenarios in this guide are additive in nature.</span></span> <span data-ttu-id="f79e2-121">因此，您可以將這些案例部署在生產租用戶中，而不會影響 PoC 外的使用者。</span><span class="sxs-lookup"><span data-stu-id="f79e2-121">As a result, they can be deployed in the production tenant without affecting users outside the PoC.</span></span> <span data-ttu-id="f79e2-122">在整份文件中，我們會指出哪些案例會對整個租用戶造成影響。</span><span class="sxs-lookup"><span data-stu-id="f79e2-122">Throughout this document, we will be calling out which scenarios would have tenant-wide effect.</span></span> <span data-ttu-id="f79e2-123">在這些情況中，您可能要考慮使用非生產環境。</span><span class="sxs-lookup"><span data-stu-id="f79e2-123">In those cases, you might want to consider a non-production environment.</span></span> 


## <a name="target-users"></a><span data-ttu-id="f79e2-124">目標使用者</span><span class="sxs-lookup"><span data-stu-id="f79e2-124">Target Users</span></span>

<span data-ttu-id="f79e2-125">請務必確定將會練習這些案例的目標使用者群，尤其是當環境為生產或測試用環境時。</span><span class="sxs-lookup"><span data-stu-id="f79e2-125">It is important to determine the target set of users that will exercise the scenarios, especially when the environment is production or test.</span></span> <span data-ttu-id="f79e2-126">PoC 的目標使用者分類如下︰</span><span class="sxs-lookup"><span data-stu-id="f79e2-126">The categories of target users for PoC are:</span></span>
* <span data-ttu-id="f79e2-127">**試驗使用者︰**環境的實際使用者，他們會以進行日常工作職責時所用的帳戶來使用解決方案</span><span class="sxs-lookup"><span data-stu-id="f79e2-127">**Pilot Users:** Real users in the environment that will be using the solution with the account they use for their day to day job functions</span></span>
* <span data-ttu-id="f79e2-128">**測試使用者︰**在環境中建立的測試帳戶</span><span class="sxs-lookup"><span data-stu-id="f79e2-128">**Test Users:** Test accounts created in the environment</span></span> 

<span data-ttu-id="f79e2-129">本指南中的大部分案例均可供試驗使用者進行練習。</span><span class="sxs-lookup"><span data-stu-id="f79e2-129">Most scenarios in this guide can be exercised by pilot users.</span></span> <span data-ttu-id="f79e2-130">在整份文件中，我們會視需要指出目標使用者的考量事項。</span><span class="sxs-lookup"><span data-stu-id="f79e2-130">Throughout this document, we will be calling out target user considerations if needed.</span></span>


[!INCLUDE [active-directory-playbook-toc](../../includes/active-directory-playbook-steps.md)]