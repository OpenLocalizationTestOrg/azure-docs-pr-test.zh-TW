---
title: "aaaAzure Active Directory 混合式身分識別設計考量-判斷多因素驗證需求"
description: "條件式存取控制與 Azure Active Directory 檢查 hello 您挑選驗證 hello 使用者時，才能允許存取 toohello 應用程式特定的條件。 一旦符合這些條件，hello 使用者已驗證，而且允許存取 toohello 應用程式。"
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
ms.openlocfilehash: 49fa7b43772fb3a2d6664747477c60a34cddde2b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="determine-multi-factor-authentication-requirements-for-your-hybrid-identity-solution"></a><span data-ttu-id="32ec0-104">判斷混合式身分識別解決方案的多重要素驗證需求</span><span class="sxs-lookup"><span data-stu-id="32ec0-104">Determine multi-factor authentication requirements for your hybrid identity solution</span></span>
<span data-ttu-id="32ec0-105">在行動力，與使用者存取資料和應用程式 hello 定域機組中以及從任何裝置，此世界中保護這項資訊變得重要。</span><span class="sxs-lookup"><span data-stu-id="32ec0-105">In this world of mobility, with users accessing data and applications in hello cloud and from any device, securing this information has become paramount.</span></span>  <span data-ttu-id="32ec0-106">每天都會出現關於安全性漏洞的新標題。</span><span class="sxs-lookup"><span data-stu-id="32ec0-106">Every day there is a new headline about a security breach.</span></span>  <span data-ttu-id="32ec0-107">多因素驗證，並針對這類缺口，這不保證，但提供額外一層的安全性 toohelp 防止這些漏洞。</span><span class="sxs-lookup"><span data-stu-id="32ec0-107">Although, there is no guarantee against such breaches, multi-factor authentication, provides an additional layer of security toohelp prevent these breaches.</span></span>
<span data-ttu-id="32ec0-108">請先評估 hello 組織需求的多因素驗證。</span><span class="sxs-lookup"><span data-stu-id="32ec0-108">Start by evaluating hello organizations requirements for multi-factor authentication.</span></span> <span data-ttu-id="32ec0-109">也就是為何 hello 組織嘗試 toosecure。</span><span class="sxs-lookup"><span data-stu-id="32ec0-109">That is, what is hello organization trying toosecure.</span></span>  <span data-ttu-id="32ec0-110">這項評估是重要的 toodefine hello 技術的需求設定和啟用多因素驗證的 hello 組織使用者。</span><span class="sxs-lookup"><span data-stu-id="32ec0-110">This evaluation is important toodefine hello technical requirements for setting up and enabling hello organizations users for multi-factor authentication.</span></span>

> [!NOTE]
> <span data-ttu-id="32ec0-111">如果您不熟悉 MFA 和其用途，強烈建議您閱讀 hello 文章[什麼是 Azure Multi-factor Authentication？](../multi-factor-authentication/multi-factor-authentication.md)先前 toocontinue 閱讀本節。</span><span class="sxs-lookup"><span data-stu-id="32ec0-111">If you are not familiar with MFA and what it does, it is strongly recommended that you read hello article [What is Azure Multi-Factor Authentication?](../multi-factor-authentication/multi-factor-authentication.md) prior toocontinue reading this section.</span></span>
> 
> 

<span data-ttu-id="32ec0-112">請確定 tooanswer hello 下列：</span><span class="sxs-lookup"><span data-stu-id="32ec0-112">Make sure tooanswer hello following:</span></span>

* <span data-ttu-id="32ec0-113">您的公司正在 toosecure Microsoft 應用程式嗎？</span><span class="sxs-lookup"><span data-stu-id="32ec0-113">Is your company trying toosecure Microsoft apps?</span></span> 
* <span data-ttu-id="32ec0-114">這些 app 是如何發佈的？</span><span class="sxs-lookup"><span data-stu-id="32ec0-114">How these apps are published?</span></span>
* <span data-ttu-id="32ec0-115">您的公司提供遠端存取 tooallow 員工 tooaccess 在內部部署應用程式嗎？</span><span class="sxs-lookup"><span data-stu-id="32ec0-115">Does your company provide remote access tooallow employees tooaccess on-premises apps?</span></span>

<span data-ttu-id="32ec0-116">如果是，何種遠端存取？您也需要的 tooevaluate 即將放置 hello 使用者要存取這些應用程式。</span><span class="sxs-lookup"><span data-stu-id="32ec0-116">If yes, what type of remote access?You also need tooevaluate where hello users who are accessing these applications will be located.</span></span> <span data-ttu-id="32ec0-117">這項評估是另一個重要步驟 toodefine hello 適當的多因素驗證策略。</span><span class="sxs-lookup"><span data-stu-id="32ec0-117">This evaluation is another important step toodefine hello proper multi-factor authentication strategy.</span></span> <span data-ttu-id="32ec0-118">請確定 tooanswer hello 下列問題：</span><span class="sxs-lookup"><span data-stu-id="32ec0-118">Make sure tooanswer hello following questions:</span></span>

* <span data-ttu-id="32ec0-119">Toobe hello 使用者位於何處？</span><span class="sxs-lookup"><span data-stu-id="32ec0-119">Where are hello users going toobe located?</span></span>
* <span data-ttu-id="32ec0-120">他們將無所不在嗎？</span><span class="sxs-lookup"><span data-stu-id="32ec0-120">Can they be located anywhere?</span></span>
* <span data-ttu-id="32ec0-121">您的公司是否需要根據 toohello 使用者位置 tooestablish 限制？</span><span class="sxs-lookup"><span data-stu-id="32ec0-121">Does your company want tooestablish restrictions according toohello user’s location?</span></span>

<span data-ttu-id="32ec0-122">一旦您了解這些需求，請務必 tooalso 評估 hello 使用者的需求，進行多因素驗證。</span><span class="sxs-lookup"><span data-stu-id="32ec0-122">Once you understand these requirements, it is important tooalso evaluate hello user’s requirements for multi-factor authentication.</span></span> <span data-ttu-id="32ec0-123">這項評估很重要的因為它會定義 hello 需求推出多因素驗證。</span><span class="sxs-lookup"><span data-stu-id="32ec0-123">This evaluation is important because it will define hello requirements for rolling out multi-factor authentication.</span></span> <span data-ttu-id="32ec0-124">請確定 tooanswer hello 下列問題：</span><span class="sxs-lookup"><span data-stu-id="32ec0-124">Make sure tooanswer hello following questions:</span></span>

* <span data-ttu-id="32ec0-125">熟悉 hello 使用者使用多重要素驗證？</span><span class="sxs-lookup"><span data-stu-id="32ec0-125">Are hello users familiar with multi-factor authentication?</span></span>
* <span data-ttu-id="32ec0-126">將一些用法會需要的 tooprovide 額外的驗證？</span><span class="sxs-lookup"><span data-stu-id="32ec0-126">Will some uses be required tooprovide additional authentication?</span></span>  
  * <span data-ttu-id="32ec0-127">如果是，所有 hello 時來自外部網路或存取特定的應用程式，或在其他情況下時間？</span><span class="sxs-lookup"><span data-stu-id="32ec0-127">If yes, all hello time, when coming from external networks, or accessing specific applications, or under other conditions?</span></span>
* <span data-ttu-id="32ec0-128">Hello 使用者需要要求如何訓練 toosetup 和實作多重要素驗證？</span><span class="sxs-lookup"><span data-stu-id="32ec0-128">Will hello users require training on how toosetup and implement multi-factor authentication?</span></span>
* <span data-ttu-id="32ec0-129">Hello 貴公司想 tooenable 多因素驗證使用者的主要案例是什麼？</span><span class="sxs-lookup"><span data-stu-id="32ec0-129">What are hello key scenarios that your company wants tooenable multi-factor authentication for their users?</span></span>

<span data-ttu-id="32ec0-130">之後回應 hello 上述問題，您都無法 toounderstand 是否有已實作多因素驗證內部部署。</span><span class="sxs-lookup"><span data-stu-id="32ec0-130">After answering hello previous questions, you will be able toounderstand if there are multi-factor authentication already implemented on-premises.</span></span> <span data-ttu-id="32ec0-131">這項評估是重要的 toodefine hello 技術的需求設定和啟用多因素驗證的 hello 組織使用者。</span><span class="sxs-lookup"><span data-stu-id="32ec0-131">This evaluation is important toodefine hello technical requirements for setting up and enabling hello organizations users for multi-factor authentication.</span></span> <span data-ttu-id="32ec0-132">請確定 tooanswer hello 下列問題：</span><span class="sxs-lookup"><span data-stu-id="32ec0-132">Make sure tooanswer hello following questions:</span></span>

* <span data-ttu-id="32ec0-133">您的公司是否需要使用 MFA tooprotect 特殊權限帳戶？</span><span class="sxs-lookup"><span data-stu-id="32ec0-133">Does your company need tooprotect privileged accounts with MFA?</span></span>
* <span data-ttu-id="32ec0-134">貴公司是否需要 tooenable MFA 特定應用程式的相容性因素？</span><span class="sxs-lookup"><span data-stu-id="32ec0-134">Does your company need tooenable MFA for certain application for compliance reasons?</span></span>
* <span data-ttu-id="32ec0-135">您的公司需要 tooenable MFA 所有符合資格的使用者，這些應用程式或只有系統管理員嗎？</span><span class="sxs-lookup"><span data-stu-id="32ec0-135">Does your company need tooenable MFA for all eligible users of these application or only administrators?</span></span>
* <span data-ttu-id="32ec0-136">您需要有 MFA 永遠啟用，或只何時 hello 使用者記錄公司網路外？</span><span class="sxs-lookup"><span data-stu-id="32ec0-136">Do you need have MFA always enabled or only when hello users are logged outside of your corporate network?</span></span>

## <a name="next-steps"></a><span data-ttu-id="32ec0-137">後續步驟</span><span class="sxs-lookup"><span data-stu-id="32ec0-137">Next steps</span></span>
[<span data-ttu-id="32ec0-138">定義混合式身分識別採用策略</span><span class="sxs-lookup"><span data-stu-id="32ec0-138">Define a hybrid identity adoption strategy</span></span>](active-directory-hybrid-identity-design-considerations-identity-adoption-strategy.md)

## <a name="see-also"></a><span data-ttu-id="32ec0-139">另請參閱</span><span class="sxs-lookup"><span data-stu-id="32ec0-139">See also</span></span>
[<span data-ttu-id="32ec0-140">設計考量概觀</span><span class="sxs-lookup"><span data-stu-id="32ec0-140">Design considerations overview</span></span>](active-directory-hybrid-identity-design-considerations-overview.md)

