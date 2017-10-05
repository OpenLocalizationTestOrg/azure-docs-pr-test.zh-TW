---
title: "Azure Active Directory 混合式身分識別設計考量 - 判斷多重要素驗證需求"
description: "透過條件式存取控制，Azure Active Directory 會在驗證使用者時以及允許存取應用程式之前，檢查您挑選的特定條件。 一旦符合這些條件，使用者就會通過驗證並獲允許存取應用程式。"
documentationcenter: 
services: active-directory
author: femila
manager: billmath
editor: 
ms.assetid: 9c59fda9-47d0-4c7e-b3e7-3575c29beabe
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/18/2017
ms.author: billmath
ms.openlocfilehash: 5b3a8ce6e4203dfb3700f324e32687dd910118af
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="determine-multi-factor-authentication-requirements-for-your-hybrid-identity-solution"></a><span data-ttu-id="2787a-104">判斷混合式身分識別解決方案的多重要素驗證需求</span><span class="sxs-lookup"><span data-stu-id="2787a-104">Determine multi-factor authentication requirements for your hybrid identity solution</span></span>
<span data-ttu-id="2787a-105">在這個具備行動力的世界中，使用者可在雲端中或從任何裝置存取資料和應用程式，因此，保護此資訊就成為最重要的項目。</span><span class="sxs-lookup"><span data-stu-id="2787a-105">In this world of mobility, with users accessing data and applications in the cloud and from any device, securing this information has become paramount.</span></span>  <span data-ttu-id="2787a-106">每天都會出現關於安全性漏洞的新標題。</span><span class="sxs-lookup"><span data-stu-id="2787a-106">Every day there is a new headline about a security breach.</span></span>  <span data-ttu-id="2787a-107">雖然不會針對這類漏洞提供保證，但多重要素驗證還是可以提供額外的安全性層級來協助防止這些漏洞。</span><span class="sxs-lookup"><span data-stu-id="2787a-107">Although, there is no guarantee against such breaches, multi-factor authentication, provides an additional layer of security to help prevent these breaches.</span></span>
<span data-ttu-id="2787a-108">一開始，先評估組織對於多重要素驗證的需求。</span><span class="sxs-lookup"><span data-stu-id="2787a-108">Start by evaluating the organizations requirements for multi-factor authentication.</span></span> <span data-ttu-id="2787a-109">也就是，組織試圖保護哪些項目。</span><span class="sxs-lookup"><span data-stu-id="2787a-109">That is, what is the organization trying to secure.</span></span>  <span data-ttu-id="2787a-110">當您定義如何設定和啟用組織使用者來進行多重要素驗證的技術需求時，這項評估非常重要。</span><span class="sxs-lookup"><span data-stu-id="2787a-110">This evaluation is important to define the technical requirements for setting up and enabling the organizations users for multi-factor authentication.</span></span>

> [!NOTE]
> <span data-ttu-id="2787a-111">如果您不熟悉 MFA 和它的功用，強烈建議您先閱讀 [什麼是 Azure 多重要素驗證？](../multi-factor-authentication/multi-factor-authentication.md) 一文，然後再繼續閱讀本節。</span><span class="sxs-lookup"><span data-stu-id="2787a-111">If you are not familiar with MFA and what it does, it is strongly recommended that you read the article [What is Azure Multi-Factor Authentication?](../multi-factor-authentication/multi-factor-authentication.md) prior to continue reading this section.</span></span>
> 
> 

<span data-ttu-id="2787a-112">請確定回答下列問題：</span><span class="sxs-lookup"><span data-stu-id="2787a-112">Make sure to answer the following:</span></span>

* <span data-ttu-id="2787a-113">貴公司試圖保護 Microsoft app 嗎？</span><span class="sxs-lookup"><span data-stu-id="2787a-113">Is your company trying to secure Microsoft apps?</span></span> 
* <span data-ttu-id="2787a-114">這些 app 是如何發佈的？</span><span class="sxs-lookup"><span data-stu-id="2787a-114">How these apps are published?</span></span>
* <span data-ttu-id="2787a-115">貴公司是否提供遠端存取，讓員工可以存取內部部署 app？</span><span class="sxs-lookup"><span data-stu-id="2787a-115">Does your company provide remote access to allow employees to access on-premises apps?</span></span>

<span data-ttu-id="2787a-116">如果是，是哪種類型的遠端存取？您也需要評估存取這些應用程式的使用者所在位置。</span><span class="sxs-lookup"><span data-stu-id="2787a-116">If yes, what type of remote access?You also need to evaluate where the users who are accessing these applications will be located.</span></span> <span data-ttu-id="2787a-117">這項評估是另一個定義適當多重要素驗證策略的步驟。</span><span class="sxs-lookup"><span data-stu-id="2787a-117">This evaluation is another important step to define the proper multi-factor authentication strategy.</span></span> <span data-ttu-id="2787a-118">請確實回答下列問題：</span><span class="sxs-lookup"><span data-stu-id="2787a-118">Make sure to answer the following questions:</span></span>

* <span data-ttu-id="2787a-119">使用者即將位於何處？</span><span class="sxs-lookup"><span data-stu-id="2787a-119">Where are the users going to be located?</span></span>
* <span data-ttu-id="2787a-120">他們將無所不在嗎？</span><span class="sxs-lookup"><span data-stu-id="2787a-120">Can they be located anywhere?</span></span>
* <span data-ttu-id="2787a-121">貴公司是否想要根據使用者的位置來建立限制？</span><span class="sxs-lookup"><span data-stu-id="2787a-121">Does your company want to establish restrictions according to the user’s location?</span></span>

<span data-ttu-id="2787a-122">一旦了解這些需求之後，請務必同時評估使用者對於多重因素驗證的需求。</span><span class="sxs-lookup"><span data-stu-id="2787a-122">Once you understand these requirements, it is important to also evaluate the user’s requirements for multi-factor authentication.</span></span> <span data-ttu-id="2787a-123">這項評估很重要是因為它將定義首度發行多重要素驗證的需求。</span><span class="sxs-lookup"><span data-stu-id="2787a-123">This evaluation is important because it will define the requirements for rolling out multi-factor authentication.</span></span> <span data-ttu-id="2787a-124">請確實回答下列問題：</span><span class="sxs-lookup"><span data-stu-id="2787a-124">Make sure to answer the following questions:</span></span>

* <span data-ttu-id="2787a-125">使用者是否熟悉多重要素驗證？</span><span class="sxs-lookup"><span data-stu-id="2787a-125">Are the users familiar with multi-factor authentication?</span></span>
* <span data-ttu-id="2787a-126">需要透過有一些用法才能提供額外的驗證嗎？</span><span class="sxs-lookup"><span data-stu-id="2787a-126">Will some uses be required to provide additional authentication?</span></span>  
  * <span data-ttu-id="2787a-127">如果是，一直都是、是在來自外部網路時、存取特定應用程式時，或者是在其他情況下？</span><span class="sxs-lookup"><span data-stu-id="2787a-127">If yes, all the time, when coming from external networks, or accessing specific applications, or under other conditions?</span></span>
* <span data-ttu-id="2787a-128">使用者是否要求訓練如何設定和實作多重要素驗證？</span><span class="sxs-lookup"><span data-stu-id="2787a-128">Will the users require training on how to setup and implement multi-factor authentication?</span></span>
* <span data-ttu-id="2787a-129">哪些是貴公司想要為使用者啟用多重因素驗證的主要案例？</span><span class="sxs-lookup"><span data-stu-id="2787a-129">What are the key scenarios that your company wants to enable multi-factor authentication for their users?</span></span>

<span data-ttu-id="2787a-130">回答上述問題之後，您將能夠了解是否已經在內部部署中實作多重要素驗證。</span><span class="sxs-lookup"><span data-stu-id="2787a-130">After answering the previous questions, you will be able to understand if there are multi-factor authentication already implemented on-premises.</span></span> <span data-ttu-id="2787a-131">當您定義如何設定和啟用組織使用者來進行多重要素驗證的技術需求時，這項評估非常重要。</span><span class="sxs-lookup"><span data-stu-id="2787a-131">This evaluation is important to define the technical requirements for setting up and enabling the organizations users for multi-factor authentication.</span></span> <span data-ttu-id="2787a-132">請確實回答下列問題：</span><span class="sxs-lookup"><span data-stu-id="2787a-132">Make sure to answer the following questions:</span></span>

* <span data-ttu-id="2787a-133">貴公司需要使用 MFA 保護具備特殊權限的帳戶嗎？</span><span class="sxs-lookup"><span data-stu-id="2787a-133">Does your company need to protect privileged accounts with MFA?</span></span>
* <span data-ttu-id="2787a-134">貴公司需要基於相容性因素，針對某些應用程式啟用 MFA 嗎？</span><span class="sxs-lookup"><span data-stu-id="2787a-134">Does your company need to enable MFA for certain application for compliance reasons?</span></span>
* <span data-ttu-id="2787a-135">貴公司需要針對這些應用程式的合格使用者，或只針對系統管理員啟用 MFA？</span><span class="sxs-lookup"><span data-stu-id="2787a-135">Does your company need to enable MFA for all eligible users of these application or only administrators?</span></span>
* <span data-ttu-id="2787a-136">您需要一律啟用 MFA，或者只有在使用者於公司網路外部登入時啟用？</span><span class="sxs-lookup"><span data-stu-id="2787a-136">Do you need have MFA always enabled or only when the users are logged outside of your corporate network?</span></span>

## <a name="next-steps"></a><span data-ttu-id="2787a-137">後續步驟</span><span class="sxs-lookup"><span data-stu-id="2787a-137">Next steps</span></span>
[<span data-ttu-id="2787a-138">定義混合式身分識別採用策略</span><span class="sxs-lookup"><span data-stu-id="2787a-138">Define a hybrid identity adoption strategy</span></span>](active-directory-hybrid-identity-design-considerations-identity-adoption-strategy.md)

## <a name="see-also"></a><span data-ttu-id="2787a-139">另請參閱</span><span class="sxs-lookup"><span data-stu-id="2787a-139">See also</span></span>
[<span data-ttu-id="2787a-140">設計考量概觀</span><span class="sxs-lookup"><span data-stu-id="2787a-140">Design considerations overview</span></span>](active-directory-hybrid-identity-design-considerations-overview.md)

