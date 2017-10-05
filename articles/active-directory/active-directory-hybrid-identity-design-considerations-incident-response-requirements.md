---
title: "Azure Active Directory 混合式身分識別設計考量 - 判斷事件回應需求 | Microsoft Docs"
description: "判斷混合式身分識別解決方案的監視和報告功能，讓 IT 可用來採取動作以識別和減緩潛在威脅。"
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
ms.openlocfilehash: 536071ec61d093af243bfd42faa6bb404172fb8e
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="determine-incident-response-requirements-for-your-hybrid-identity-solution"></a><span data-ttu-id="b3c5b-103">判斷混合式身分識別解決方案的事件回應需求</span><span class="sxs-lookup"><span data-stu-id="b3c5b-103">Determine incident response requirements for your hybrid identity solution</span></span>
<span data-ttu-id="b3c5b-104">中大型組織最可能具備適當的 [安全性事件回應](https://technet.microsoft.com/library/cc700825.aspx) ，可協助 IT 根據事件層級來採取動作。</span><span class="sxs-lookup"><span data-stu-id="b3c5b-104">Large or medium organizations most likely will have a [security incident response](https://technet.microsoft.com/library/cc700825.aspx) in place to help IT take actions accordingly to the level of incident.</span></span> <span data-ttu-id="b3c5b-105">身分識別管理系統是事件回應程序中的重要元件，因為它可以用來協助識別對目標執行特定動作的人員。</span><span class="sxs-lookup"><span data-stu-id="b3c5b-105">The identity management system is an important component in the incident response process because it can be used to help identifying who performed a specific action against the target.</span></span> <span data-ttu-id="b3c5b-106">混合式身分識別解決方案必須能夠提供監視和報告功能，讓 IT 可用來採取動作以識別和減緩潛在威脅。</span><span class="sxs-lookup"><span data-stu-id="b3c5b-106">The hybrid identity solution must be able to provide monitoring and reporting capabilities that can be leveraged by IT to take actions to identify and mitigate a potential threat.</span></span> <span data-ttu-id="b3c5b-107">在一般事件回應計畫中，您可以將計畫分為下列階段：</span><span class="sxs-lookup"><span data-stu-id="b3c5b-107">In a typical incident response plan you will have the following phases as part of the plan:</span></span>

1. <span data-ttu-id="b3c5b-108">初步評估。</span><span class="sxs-lookup"><span data-stu-id="b3c5b-108">Initial assessment.</span></span>
2. <span data-ttu-id="b3c5b-109">事件傳達的訊息。</span><span class="sxs-lookup"><span data-stu-id="b3c5b-109">Incident communication.</span></span>
3. <span data-ttu-id="b3c5b-110">損毀控制與風險降低。</span><span class="sxs-lookup"><span data-stu-id="b3c5b-110">Damage control and risk reduction.</span></span>
4. <span data-ttu-id="b3c5b-111">識別是否遭到入侵及嚴重性。</span><span class="sxs-lookup"><span data-stu-id="b3c5b-111">Identification of what it was compromise and severity.</span></span>
5. <span data-ttu-id="b3c5b-112">保留證據。</span><span class="sxs-lookup"><span data-stu-id="b3c5b-112">Evidence preservation.</span></span>
6. <span data-ttu-id="b3c5b-113">通知適當的合作對象。</span><span class="sxs-lookup"><span data-stu-id="b3c5b-113">Notification to appropriate parties.</span></span>
7. <span data-ttu-id="b3c5b-114">系統修復。</span><span class="sxs-lookup"><span data-stu-id="b3c5b-114">System recovery.</span></span>
8. <span data-ttu-id="b3c5b-115">文件。</span><span class="sxs-lookup"><span data-stu-id="b3c5b-115">Documentation.</span></span>
9. <span data-ttu-id="b3c5b-116">損毀和成本評估。</span><span class="sxs-lookup"><span data-stu-id="b3c5b-116">Damage and cost assessment.</span></span>
10. <span data-ttu-id="b3c5b-117">修訂程序和計畫。</span><span class="sxs-lookup"><span data-stu-id="b3c5b-117">Process and plan revision.</span></span>

<span data-ttu-id="b3c5b-118">在識別遭到入侵及嚴重性階段期間，必須識別已遭入侵的系統、已遭存取的檔案，並判斷這些檔案的敏感度。</span><span class="sxs-lookup"><span data-stu-id="b3c5b-118">During the identification of what it was compromise and severity- phase, it will be necessary to identify the systems that have been compromised, files that have been accessed and determine the sensitivity of those files.</span></span> <span data-ttu-id="b3c5b-119">您的混合式身分識別系統應該能夠滿足這些需求，來協助您識別進行這些變更的使用者。</span><span class="sxs-lookup"><span data-stu-id="b3c5b-119">Your hybrid identity system should be able to fulfill these requirements to assist you identifying the user that made those changes.</span></span> 

## <a name="monitoring-and-reporting"></a><span data-ttu-id="b3c5b-120">監視和報告</span><span class="sxs-lookup"><span data-stu-id="b3c5b-120">Monitoring and reporting</span></span>
<span data-ttu-id="b3c5b-121">主要是如果系統已內建稽核和報告功能，身分識別系統也可以在初步評估階段多次提供協助。</span><span class="sxs-lookup"><span data-stu-id="b3c5b-121">Many times the identity system can also help in initial assessment phase mainly if the system has built in auditing and reporting capabilities.</span></span> <span data-ttu-id="b3c5b-122">在初步評估期間，IT 系統管理員必須能夠識別可疑的活動，或者系統應該能夠根據預先設定的工作自動觸發它。</span><span class="sxs-lookup"><span data-stu-id="b3c5b-122">During the initial assessment, IT Admin must be able to identify a suspicious activity, or the system should be able to trigger it automatically based on a pre-configured task.</span></span> <span data-ttu-id="b3c5b-123">有許多活動可代表潛在的攻擊，但在其他情況下，設定不良的系統可能會在入侵偵測系統中導致誤報數目。</span><span class="sxs-lookup"><span data-stu-id="b3c5b-123">Many activities could indicate a possible attack, however in other cases, a badly configured system might lead to a number of false positives in an intrusion detection system.</span></span> 

<span data-ttu-id="b3c5b-124">身分識別管理系統應該能協助 IT 系統管理員來識別及報告這些可疑的活動。</span><span class="sxs-lookup"><span data-stu-id="b3c5b-124">The identity management system should assist IT admins to identify and report those suspicious activities.</span></span> <span data-ttu-id="b3c5b-125">通常可藉由監視所有系統並具備可強調顯示潛在威脅的報告功能，來滿足這些技術需求。</span><span class="sxs-lookup"><span data-stu-id="b3c5b-125">Usually these technical requirements can be fulfilled by monitoring all systems and having a reporting capability that can highlight potential threats.</span></span> <span data-ttu-id="b3c5b-126">在考量事件回應需求時，請使用下列問題來協助您設計混合式身分識別解決方案：</span><span class="sxs-lookup"><span data-stu-id="b3c5b-126">Use the questions below to help you design your hybrid identity solution while taking into consideration incident response requirements:</span></span>

* <span data-ttu-id="b3c5b-127">貴公司擁有適當的安全性事件回應嗎？</span><span class="sxs-lookup"><span data-stu-id="b3c5b-127">Does your company has a security incident response in place?</span></span>
  * <span data-ttu-id="b3c5b-128">如果是，目前的身分識別管理系統可用來做為程序的一部分嗎？</span><span class="sxs-lookup"><span data-stu-id="b3c5b-128">If yes, is the current identity management system used as part of the process?</span></span>
* <span data-ttu-id="b3c5b-129">貴公司需要識別使用者在不同裝置上嘗試進行的單一登入嗎？</span><span class="sxs-lookup"><span data-stu-id="b3c5b-129">Does your company need to identify suspicious sign-on attempts from users across different devices?</span></span>
* <span data-ttu-id="b3c5b-130">貴公司需要偵測可能入侵的使用者認證嗎？</span><span class="sxs-lookup"><span data-stu-id="b3c5b-130">Does your company need to detect potential compromised user’s credentials?</span></span>
* <span data-ttu-id="b3c5b-131">貴公司需要稽核使用者的存取和動作嗎？</span><span class="sxs-lookup"><span data-stu-id="b3c5b-131">Does your company need to audit user’s access and action?</span></span>
* <span data-ttu-id="b3c5b-132">貴公司需要知道使用者何時重設密碼嗎？</span><span class="sxs-lookup"><span data-stu-id="b3c5b-132">Does your company need to know when a user reset his password?</span></span>

## <a name="policy-enforcement"></a><span data-ttu-id="b3c5b-133">強制執行原則</span><span class="sxs-lookup"><span data-stu-id="b3c5b-133">Policy enforcement</span></span>
<span data-ttu-id="b3c5b-134">在損毀控制和風險降低階段期間，最重要的是快速降低攻擊的實際和潛在影響。</span><span class="sxs-lookup"><span data-stu-id="b3c5b-134">During damage control and risk reduction-phase, it is important to quickly reduce the actual and potential effects of an attack.</span></span> <span data-ttu-id="b3c5b-135">此時您所採取的動作可以在次要和主要之間產生差異。</span><span class="sxs-lookup"><span data-stu-id="b3c5b-135">That action that you will take at this point can make the difference between a minor and a major one.</span></span> <span data-ttu-id="b3c5b-136">確切的回應將取決於您的組織和您面對攻擊的性質。</span><span class="sxs-lookup"><span data-stu-id="b3c5b-136">The exact response will depend on your organization and the nature of the attack that you face.</span></span> <span data-ttu-id="b3c5b-137">如果最初評估歸納出帳戶已遭到入侵，則您必須強制執行原則來封鎖這個帳戶。</span><span class="sxs-lookup"><span data-stu-id="b3c5b-137">If the initial assessment concluded that an account was compromised, you will need to enforce policy to block this account.</span></span> <span data-ttu-id="b3c5b-138">這只是運用身分識別管理系統的其中一個範例。</span><span class="sxs-lookup"><span data-stu-id="b3c5b-138">That’s just one example where the identity management system will be leveraged.</span></span> <span data-ttu-id="b3c5b-139">在考量如何強制執行原則以回應即將發生的事件時，請使用下列問題來協助您設計混合式身分識別解決方案：</span><span class="sxs-lookup"><span data-stu-id="b3c5b-139">Use the questions below to help you design your hybrid identity solution while taking into consideration how policies will be enforced to react to an ongoing incident:</span></span>

* <span data-ttu-id="b3c5b-140">貴公司具備適當的原則，可視需要封鎖使用者存取網路嗎？</span><span class="sxs-lookup"><span data-stu-id="b3c5b-140">Does your company have policies in place to block users from access the network if necessary?</span></span>
  * <span data-ttu-id="b3c5b-141">如果是，目前的解決方案能夠與您即將採用的混合式身分識別管理系統整合嗎？</span><span class="sxs-lookup"><span data-stu-id="b3c5b-141">If yes, does the current solution integrate with the hybrid identity management system that you are going to adopt?</span></span>
* <span data-ttu-id="b3c5b-142">貴公司是否需要針對隔離的使用者強制執行條件式存取？</span><span class="sxs-lookup"><span data-stu-id="b3c5b-142">Does your company need to enforce conditional access for users that are in quarantine?</span></span> 

> [!NOTE]
> <span data-ttu-id="b3c5b-143">請確定會記下每個答案，並了解答案背後的原理。</span><span class="sxs-lookup"><span data-stu-id="b3c5b-143">Make sure to take notes of each answer and understand the rationale behind the answer.</span></span> <span data-ttu-id="b3c5b-144">[定義資料保護策略](active-directory-hybrid-identity-design-considerations-data-protection-strategy.md) 將介紹可用選項，以及每個選項的優點/缺點。</span><span class="sxs-lookup"><span data-stu-id="b3c5b-144">[Define data protection strategy](active-directory-hybrid-identity-design-considerations-data-protection-strategy.md) will go over the options available and advantages/disadvantages of each option.</span></span>  <span data-ttu-id="b3c5b-145">回答這些問題之後，您就能選取最適合業務需求的選項。</span><span class="sxs-lookup"><span data-stu-id="b3c5b-145">By having answered those questions you will select which option best suits your business needs.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="b3c5b-146">後續步驟</span><span class="sxs-lookup"><span data-stu-id="b3c5b-146">Next steps</span></span>
[<span data-ttu-id="b3c5b-147">定義資料保護策略</span><span class="sxs-lookup"><span data-stu-id="b3c5b-147">Define data protection strategy</span></span>](active-directory-hybrid-identity-design-considerations-data-protection-strategy.md)

## <a name="see-also"></a><span data-ttu-id="b3c5b-148">另請參閱</span><span class="sxs-lookup"><span data-stu-id="b3c5b-148">See Also</span></span>
[<span data-ttu-id="b3c5b-149">設計考量概觀</span><span class="sxs-lookup"><span data-stu-id="b3c5b-149">Design considerations overview</span></span>](active-directory-hybrid-identity-design-considerations-overview.md)

