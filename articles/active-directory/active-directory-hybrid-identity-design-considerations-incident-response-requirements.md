---
title: "aaaAzure Active Directory 混合式身分識別設計考量-判斷事件 rResponse 需求 |Microsoft 文件"
description: "決定監視和報告功能 hello 混合式身分識別解決方案，可以利用 IT tootake 動作 tooidentify 並減輕潛在威脅"
documentationcenter: 
services: active-directory
author: billmath
manager: femila
editor: 
ms.assetid: a3d2a459-599b-4b67-8e51-7369ee25082d
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/18/2017
ms.author: billmath
ms.openlocfilehash: 7084096f318ef461e8331fb6edde1b77d4108466
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="determine-incident-response-requirements-for-your-hybrid-identity-solution"></a><span data-ttu-id="e3fd5-103">判斷混合式身分識別解決方案的事件回應需求</span><span class="sxs-lookup"><span data-stu-id="e3fd5-103">Determine incident response requirements for your hybrid identity solution</span></span>
<span data-ttu-id="e3fd5-104">大型或中型組織最有可能會有[安全性事件回應](https://technet.microsoft.com/library/cc700825.aspx)位置 toohelp IT 在執行動作據以 toohello 層級的事件。</span><span class="sxs-lookup"><span data-stu-id="e3fd5-104">Large or medium organizations most likely will have a [security incident response](https://technet.microsoft.com/library/cc700825.aspx) in place toohelp IT take actions accordingly toohello level of incident.</span></span> <span data-ttu-id="e3fd5-105">hello 身分識別管理系統是 hello 事件回應程序中的重要元件，因為它可以是使用的 toohelp 識別執行特定動作對 hello 的目標人員。</span><span class="sxs-lookup"><span data-stu-id="e3fd5-105">hello identity management system is an important component in hello incident response process because it can be used toohelp identifying who performed a specific action against hello target.</span></span> <span data-ttu-id="e3fd5-106">hello 混合式身分識別解決方案必須能夠 tooprovide 監視和報告功能，可以利用 IT tootake 動作 tooidentify 並降低潛在的威脅。</span><span class="sxs-lookup"><span data-stu-id="e3fd5-106">hello hybrid identity solution must be able tooprovide monitoring and reporting capabilities that can be leveraged by IT tootake actions tooidentify and mitigate a potential threat.</span></span> <span data-ttu-id="e3fd5-107">一般事件回應計劃中，您必須遵循階段 hello 計劃的 hello:</span><span class="sxs-lookup"><span data-stu-id="e3fd5-107">In a typical incident response plan you will have hello following phases as part of hello plan:</span></span>

1. <span data-ttu-id="e3fd5-108">初步評估。</span><span class="sxs-lookup"><span data-stu-id="e3fd5-108">Initial assessment.</span></span>
2. <span data-ttu-id="e3fd5-109">事件傳達的訊息。</span><span class="sxs-lookup"><span data-stu-id="e3fd5-109">Incident communication.</span></span>
3. <span data-ttu-id="e3fd5-110">損毀控制與風險降低。</span><span class="sxs-lookup"><span data-stu-id="e3fd5-110">Damage control and risk reduction.</span></span>
4. <span data-ttu-id="e3fd5-111">識別是否遭到入侵及嚴重性。</span><span class="sxs-lookup"><span data-stu-id="e3fd5-111">Identification of what it was compromise and severity.</span></span>
5. <span data-ttu-id="e3fd5-112">保留證據。</span><span class="sxs-lookup"><span data-stu-id="e3fd5-112">Evidence preservation.</span></span>
6. <span data-ttu-id="e3fd5-113">通知 tooappropriate 合作對象。</span><span class="sxs-lookup"><span data-stu-id="e3fd5-113">Notification tooappropriate parties.</span></span>
7. <span data-ttu-id="e3fd5-114">系統修復。</span><span class="sxs-lookup"><span data-stu-id="e3fd5-114">System recovery.</span></span>
8. <span data-ttu-id="e3fd5-115">文件。</span><span class="sxs-lookup"><span data-stu-id="e3fd5-115">Documentation.</span></span>
9. <span data-ttu-id="e3fd5-116">損毀和成本評估。</span><span class="sxs-lookup"><span data-stu-id="e3fd5-116">Damage and cost assessment.</span></span>
10. <span data-ttu-id="e3fd5-117">修訂程序和計畫。</span><span class="sxs-lookup"><span data-stu-id="e3fd5-117">Process and plan revision.</span></span>

<span data-ttu-id="e3fd5-118">決定其 hello 識別期間洩露和嚴重性階段，它將會需要 tooidentify hello 系統已遭入侵，已存取，並判斷 hello 區分這些檔案的檔案。</span><span class="sxs-lookup"><span data-stu-id="e3fd5-118">During hello identification of what it was compromise and severity- phase, it will be necessary tooidentify hello systems that have been compromised, files that have been accessed and determine hello sensitivity of those files.</span></span> <span data-ttu-id="e3fd5-119">混合式身分識別系統應該能夠 toofulfill 這些需求 tooassist 您識別 hello 使用者做這些變更。</span><span class="sxs-lookup"><span data-stu-id="e3fd5-119">Your hybrid identity system should be able toofulfill these requirements tooassist you identifying hello user that made those changes.</span></span> 

## <a name="monitoring-and-reporting"></a><span data-ttu-id="e3fd5-120">監視和報告</span><span class="sxs-lookup"><span data-stu-id="e3fd5-120">Monitoring and reporting</span></span>
<span data-ttu-id="e3fd5-121">也可協助多次 hello 識別系統中初始評估階段主要如果 hello 系統具有內建稽核與報告功能。</span><span class="sxs-lookup"><span data-stu-id="e3fd5-121">Many times hello identity system can also help in initial assessment phase mainly if hello system has built in auditing and reporting capabilities.</span></span> <span data-ttu-id="e3fd5-122">在初始評估 hello，IT 系統管理員必須能夠 tooidentify 可疑的活動，或 hello 系統應該能夠 tootrigger 自動根據預先設定的工作。</span><span class="sxs-lookup"><span data-stu-id="e3fd5-122">During hello initial assessment, IT Admin must be able tooidentify a suspicious activity, or hello system should be able tootrigger it automatically based on a pre-configured task.</span></span> <span data-ttu-id="e3fd5-123">許多活動可能表示可能的攻擊，但是在其他情況下，設定不良的系統可能會導致 tooa 誤判數目入侵偵測系統中。</span><span class="sxs-lookup"><span data-stu-id="e3fd5-123">Many activities could indicate a possible attack, however in other cases, a badly configured system might lead tooa number of false positives in an intrusion detection system.</span></span> 

<span data-ttu-id="e3fd5-124">應該協助 IT 系統管理員 」 tooidentify hello 身分識別管理系統，並報告這些可疑的活動。</span><span class="sxs-lookup"><span data-stu-id="e3fd5-124">hello identity management system should assist IT admins tooidentify and report those suspicious activities.</span></span> <span data-ttu-id="e3fd5-125">通常可藉由監視所有系統並具備可強調顯示潛在威脅的報告功能，來滿足這些技術需求。</span><span class="sxs-lookup"><span data-stu-id="e3fd5-125">Usually these technical requirements can be fulfilled by monitoring all systems and having a reporting capability that can highlight potential threats.</span></span> <span data-ttu-id="e3fd5-126">使用 hello 問題下方 toohelp 設計時考量事件回應需求您混合式身分識別解決方案：</span><span class="sxs-lookup"><span data-stu-id="e3fd5-126">Use hello questions below toohelp you design your hybrid identity solution while taking into consideration incident response requirements:</span></span>

* <span data-ttu-id="e3fd5-127">貴公司擁有適當的安全性事件回應嗎？</span><span class="sxs-lookup"><span data-stu-id="e3fd5-127">Does your company has a security incident response in place?</span></span>
  * <span data-ttu-id="e3fd5-128">如果是，會 hello 目前身分識別管理系統使用 hello 程序的一部分嗎？</span><span class="sxs-lookup"><span data-stu-id="e3fd5-128">If yes, is hello current identity management system used as part of hello process?</span></span>
* <span data-ttu-id="e3fd5-129">您的公司需要 tooidentify 可疑登入嘗試從使用者跨不同裝置嗎？</span><span class="sxs-lookup"><span data-stu-id="e3fd5-129">Does your company need tooidentify suspicious sign-on attempts from users across different devices?</span></span>
* <span data-ttu-id="e3fd5-130">您的公司是否需要 toodetect 潛在盜用的使用者的認證？</span><span class="sxs-lookup"><span data-stu-id="e3fd5-130">Does your company need toodetect potential compromised user’s credentials?</span></span>
* <span data-ttu-id="e3fd5-131">您的公司是否需要 tooaudit 使用者的存取和動作？</span><span class="sxs-lookup"><span data-stu-id="e3fd5-131">Does your company need tooaudit user’s access and action?</span></span>
* <span data-ttu-id="e3fd5-132">當使用者重設其密碼時，貴公司需要 tooknow？</span><span class="sxs-lookup"><span data-stu-id="e3fd5-132">Does your company need tooknow when a user reset his password?</span></span>

## <a name="policy-enforcement"></a><span data-ttu-id="e3fd5-133">強制執行原則</span><span class="sxs-lookup"><span data-stu-id="e3fd5-133">Policy enforcement</span></span>
<span data-ttu-id="e3fd5-134">在損毀控制項和風險降低階段，請務必 tooquickly 減少受到攻擊的 hello 實際和潛在影響。</span><span class="sxs-lookup"><span data-stu-id="e3fd5-134">During damage control and risk reduction-phase, it is important tooquickly reduce hello actual and potential effects of an attack.</span></span> <span data-ttu-id="e3fd5-135">此時所採取的動作可讓 hello 次要和主要的一個宣告之間的差異。</span><span class="sxs-lookup"><span data-stu-id="e3fd5-135">That action that you will take at this point can make hello difference between a minor and a major one.</span></span> <span data-ttu-id="e3fd5-136">hello 確切的反應取決於您的組織和您所面對的 hello 攻擊的 hello 性質。</span><span class="sxs-lookup"><span data-stu-id="e3fd5-136">hello exact response will depend on your organization and hello nature of hello attack that you face.</span></span> <span data-ttu-id="e3fd5-137">如果 hello 初始評估結束帳戶已遭到洩露，您將需要 tooenforce 原則 tooblock 此帳戶。</span><span class="sxs-lookup"><span data-stu-id="e3fd5-137">If hello initial assessment concluded that an account was compromised, you will need tooenforce policy tooblock this account.</span></span> <span data-ttu-id="e3fd5-138">這是一個範例中，將內容運用 hello 身分識別管理系統。</span><span class="sxs-lookup"><span data-stu-id="e3fd5-138">That’s just one example where hello identity management system will be leveraged.</span></span> <span data-ttu-id="e3fd5-139">使用以下 toohelp 納入考量原則的會實施 tooreact tooan 進行中的事件時，設計您的混合式身分識別解決方案的 hello 問題：</span><span class="sxs-lookup"><span data-stu-id="e3fd5-139">Use hello questions below toohelp you design your hybrid identity solution while taking into consideration how policies will be enforced tooreact tooan ongoing incident:</span></span>

* <span data-ttu-id="e3fd5-140">您的公司有原則位置 tooblock 使用者從網路存取 hello 中如有必要？</span><span class="sxs-lookup"><span data-stu-id="e3fd5-140">Does your company have policies in place tooblock users from access hello network if necessary?</span></span>
  * <span data-ttu-id="e3fd5-141">如果是，不會 hello 目前方案整合 hello 混合式身分識別管理系統，必須進行 tooadopt 嗎？</span><span class="sxs-lookup"><span data-stu-id="e3fd5-141">If yes, does hello current solution integrate with hello hybrid identity management system that you are going tooadopt?</span></span>
* <span data-ttu-id="e3fd5-142">您的公司需要 tooenforce 條件式存取位於隔離的使用者嗎？</span><span class="sxs-lookup"><span data-stu-id="e3fd5-142">Does your company need tooenforce conditional access for users that are in quarantine?</span></span> 

> [!NOTE]
> <span data-ttu-id="e3fd5-143">請確定每個答案 tootake 附註，並了解 hello 回應 hello 背後的基本原理。</span><span class="sxs-lookup"><span data-stu-id="e3fd5-143">Make sure tootake notes of each answer and understand hello rationale behind hello answer.</span></span> <span data-ttu-id="e3fd5-144">[定義的資料保護策略](active-directory-hybrid-identity-design-considerations-data-protection-strategy.md)將介紹可用 hello 選項以及每個選項的優點/缺點。</span><span class="sxs-lookup"><span data-stu-id="e3fd5-144">[Define data protection strategy](active-directory-hybrid-identity-design-considerations-data-protection-strategy.md) will go over hello options available and advantages/disadvantages of each option.</span></span>  <span data-ttu-id="e3fd5-145">回答這些問題之後，您就能選取最適合業務需求的選項。</span><span class="sxs-lookup"><span data-stu-id="e3fd5-145">By having answered those questions you will select which option best suits your business needs.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="e3fd5-146">後續步驟</span><span class="sxs-lookup"><span data-stu-id="e3fd5-146">Next steps</span></span>
[<span data-ttu-id="e3fd5-147">定義資料保護策略</span><span class="sxs-lookup"><span data-stu-id="e3fd5-147">Define data protection strategy</span></span>](active-directory-hybrid-identity-design-considerations-data-protection-strategy.md)

## <a name="see-also"></a><span data-ttu-id="e3fd5-148">另請參閱</span><span class="sxs-lookup"><span data-stu-id="e3fd5-148">See Also</span></span>
[<span data-ttu-id="e3fd5-149">設計考量概觀</span><span class="sxs-lookup"><span data-stu-id="e3fd5-149">Design considerations overview</span></span>](active-directory-hybrid-identity-design-considerations-overview.md)

