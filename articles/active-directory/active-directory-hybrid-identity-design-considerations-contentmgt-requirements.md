---
title: "aaaAzure Active Directory 混合式身分識別設計考量-判斷內容管理需求 |Microsoft 文件"
description: "深入瞭解如何 toodetermine hello 內容管理您的業務需求。 通常當使用者具有自己的裝置他可能的替代方式相應 toohello 使用應用程式，他也多個的認證。 它是重要的 toodifferentiate 內容使用個人的認證與 hello 使用公司認證所建立的項目所建立。 您的身分識別解決方案應該能夠與雲端服務 tooprovide toointeract 順暢的體驗 toohello 使用者，同時確保其隱私權和增加 hello 防止資料外洩。"
documentationcenter: 
services: active-directory
author: billmath
manager: femila
editor: 
ms.assetid: dd1ef776-db4d-4ab8-9761-2adaa5a4f004
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/18/2017
ms.author: billmath
ms.openlocfilehash: 607d366633c37b65ec5cf8ae5c64d73ca1cc96b7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="determine-content-management-requirements-for-your-hybrid-identity-solution"></a><span data-ttu-id="645ab-106">判斷混合式身分識別解決方案的內容管理需求</span><span class="sxs-lookup"><span data-stu-id="645ab-106">Determine content management requirements for your hybrid identity solution</span></span>
<span data-ttu-id="645ab-107">了解 hello 內容管理的需求為您的企業可能會直接影響您決定哪一個混合式身分識別解決方案 toouse。</span><span class="sxs-lookup"><span data-stu-id="645ab-107">Understanding hello content management requirements for your business may direct affect your decision on which hybrid identity solution toouse.</span></span> <span data-ttu-id="645ab-108">與請 hello 的多個裝置和使用者 toobring hello 功能自己的裝置 ([BYOD](http://aka.ms/byodcg))、 hello 公司必須保護它自己的資料，但它也必須保留使用者的隱私權。</span><span class="sxs-lookup"><span data-stu-id="645ab-108">With hello proliferation of multiple devices and hello capability of users toobring their own devices ([BYOD](http://aka.ms/byodcg)), hello company must protect its own data but it also must keep user’s privacy intact.</span></span> <span data-ttu-id="645ab-109">通常當使用者具有自己的裝置他可能的替代方式相應 toohello 使用應用程式，他也多個的認證。</span><span class="sxs-lookup"><span data-stu-id="645ab-109">Usually when a user has his own device he might have also multiple credentials that will be alternating according toohello application that he uses.</span></span> <span data-ttu-id="645ab-110">它是重要的 toodifferentiate 內容使用個人的認證與 hello 使用公司認證所建立的項目所建立。</span><span class="sxs-lookup"><span data-stu-id="645ab-110">It is important toodifferentiate what content was created using personal credentials versus hello ones created using corporate credentials.</span></span> <span data-ttu-id="645ab-111">您的身分識別解決方案應該能夠與雲端服務 tooprovide toointeract 順暢的體驗 toohello 使用者，同時確保其隱私權和增加 hello 防止資料外洩。</span><span class="sxs-lookup"><span data-stu-id="645ab-111">Your identity solution should be able toointeract with cloud services tooprovide a seamless experience toohello end user while ensure his privacy and increase hello protection against data leakage.</span></span> 

<span data-ttu-id="645ab-112">身分識別解決方案會利用不同的技術控制項，在訂單 tooprovide 內容管理 hello 圖所示：</span><span class="sxs-lookup"><span data-stu-id="645ab-112">Your identity solution will be leveraged by different technical controls in order tooprovide content management as shown in hello figure below:</span></span>

![](./media/hybrid-id-design-considerations/securitycontrols.png)

<span data-ttu-id="645ab-113">**充分運用身分識別管理系統的安全性控制項**</span><span class="sxs-lookup"><span data-stu-id="645ab-113">**Security controls that will be leveraging your identity management system**</span></span>

<span data-ttu-id="645ab-114">一般情況下，內容管理需求將會利用您的身分識別管理系統，在下列區域的 hello:</span><span class="sxs-lookup"><span data-stu-id="645ab-114">In general, content management requirements will leverage your identity management system in hello following areas:</span></span>

* <span data-ttu-id="645ab-115">隱私權： 識別 hello 使用者擁有的資源，並套用 hello 適當的控制項 toomaintain 完整性。</span><span class="sxs-lookup"><span data-stu-id="645ab-115">Privacy: identifying hello user that owns a resource and applying hello appropriate controls toomaintain integrity.</span></span>
* <span data-ttu-id="645ab-116">資料分類： 識別 hello 使用者或群組以及根據分類 tooits 存取 tooan 物件層級。</span><span class="sxs-lookup"><span data-stu-id="645ab-116">Data Classification: identify hello user or group and level of access tooan object according tooits classification.</span></span> 
* <span data-ttu-id="645ab-117">資料外洩防護： 負責保護資料 tooavoid 外洩的安全性控制項需要 toointeract 與 hello 身分識別系統 toovalidate hello 使用者的身分識別。</span><span class="sxs-lookup"><span data-stu-id="645ab-117">Data Leakage Protection: security controls responsible for protecting data tooavoid leakage will need toointeract with hello identity system toovalidate hello user’s identity.</span></span> <span data-ttu-id="645ab-118">這對於稽核記錄用途也很重要。</span><span class="sxs-lookup"><span data-stu-id="645ab-118">This is also important for auditing trail purpose.</span></span>

> [!NOTE]
> <span data-ttu-id="645ab-119">如需資料分類的最佳做法與指導方針，請參閱 [雲端整備的資料分類](http://download.microsoft.com/download/0/A/3/0A3BE969-85C5-4DD2-83B6-366AA71D1FE3/Data-Classification-for-Cloud-Readiness.pdf) 。</span><span class="sxs-lookup"><span data-stu-id="645ab-119">Read [data classification for cloud readiness](http://download.microsoft.com/download/0/A/3/0A3BE969-85C5-4DD2-83B6-366AA71D1FE3/Data-Classification-for-Cloud-Readiness.pdf) for more information about best practices and guidelines for data classification.</span></span>
> 
> 

<span data-ttu-id="645ab-120">當您規劃混合式身分識別解決方案確定遵循該 hello 問題根據 tooyour 組織的需求：</span><span class="sxs-lookup"><span data-stu-id="645ab-120">When planning your hybrid identity solution ensure that hello following questions are answered according tooyour organization’s requirements:</span></span>

* <span data-ttu-id="645ab-121">您的公司有安全性控制項中的位置 tooenforce 資料隱私權？</span><span class="sxs-lookup"><span data-stu-id="645ab-121">Does your company have security controls in place tooenforce data privacy?</span></span>
  * <span data-ttu-id="645ab-122">如果是，這些安全性控制項將會無法與 hello 混合式身分識別解決方案，而您會進入 tooadopt toointegrate 嗎？</span><span class="sxs-lookup"><span data-stu-id="645ab-122">If yes, will those security controls be able toointegrate with hello hybrid identity solution that you are going tooadopt?</span></span>
* <span data-ttu-id="645ab-123">貴公司是否使用資料分類？</span><span class="sxs-lookup"><span data-stu-id="645ab-123">Does your company use data classification?</span></span>
  * <span data-ttu-id="645ab-124">如果是，是否 hello 目前解決方案能夠 toointegrate 與 hello 混合式身分識別解決方案，而您會進入 tooadopt？</span><span class="sxs-lookup"><span data-stu-id="645ab-124">If yes, is hello current solution able toointegrate with hello hybrid identity solution that you are going tooadopt?</span></span>
* <span data-ttu-id="645ab-125">貴公司目前對於資料外洩有任何解決方案嗎？</span><span class="sxs-lookup"><span data-stu-id="645ab-125">Does your company currently have any solution for data leakage?</span></span> 
  * <span data-ttu-id="645ab-126">如果是，是否 hello 目前解決方案能夠 toointegrate 與 hello 混合式身分識別解決方案，而您會進入 tooadopt？</span><span class="sxs-lookup"><span data-stu-id="645ab-126">If yes, is hello current solution able toointegrate with hello hybrid identity solution that you are going tooadopt?</span></span>
* <span data-ttu-id="645ab-127">您的公司是否需要 tooaudit 存取 tooresources？</span><span class="sxs-lookup"><span data-stu-id="645ab-127">Does your company need tooaudit access tooresources?</span></span>
  * <span data-ttu-id="645ab-128">如果是，是哪種類型的資源？</span><span class="sxs-lookup"><span data-stu-id="645ab-128">If yes, what type of resources?</span></span>
  * <span data-ttu-id="645ab-129">如果是，需要哪一個資訊層級？</span><span class="sxs-lookup"><span data-stu-id="645ab-129">If yes, what level of information is necessary?</span></span>
  * <span data-ttu-id="645ab-130">如果是，其中必須位於 hello 稽核記錄？</span><span class="sxs-lookup"><span data-stu-id="645ab-130">If yes, where hello audit log must reside?</span></span> <span data-ttu-id="645ab-131">在內部部署或 hello 雲端中嗎？</span><span class="sxs-lookup"><span data-stu-id="645ab-131">On-premises or in hello cloud?</span></span>
* <span data-ttu-id="645ab-132">您的公司需要 tooencrypt 包含敏感性資料 (SSNs、 信用卡號碼等) 的任何電子郵件嗎？</span><span class="sxs-lookup"><span data-stu-id="645ab-132">Does your company need tooencrypt any emails that contain sensitive data (SSNs, credit card numbers, etc)?</span></span>
* <span data-ttu-id="645ab-133">您的公司需要 tooencrypt 所有文件/內容與外部公司夥伴共用嗎？</span><span class="sxs-lookup"><span data-stu-id="645ab-133">Does your company need tooencrypt all documents/contents shared with external business partners?</span></span>
* <span data-ttu-id="645ab-134">您的公司是否需要 tooenforce 特定種類的電子郵件上的公司原則 （執行所有無回應，不會轉送）？</span><span class="sxs-lookup"><span data-stu-id="645ab-134">Does your company need tooenforce corporate policies on certain kinds of emails (do no reply all, do not forward)?</span></span>

> [!NOTE]
> <span data-ttu-id="645ab-135">請確定每個答案 tootake 附註，並了解 hello 回應 hello 背後的基本原理。</span><span class="sxs-lookup"><span data-stu-id="645ab-135">Make sure tootake notes of each answer and understand hello rationale behind hello answer.</span></span> <span data-ttu-id="645ab-136">[定義的資料保護策略](active-directory-hybrid-identity-design-considerations-data-protection-strategy.md)將介紹可用 hello 選項以及每個選項的優點/缺點。</span><span class="sxs-lookup"><span data-stu-id="645ab-136">[Define Data Protection Strategy](active-directory-hybrid-identity-design-considerations-data-protection-strategy.md) will go over hello options available and advantages/disadvantages of each option.</span></span>  <span data-ttu-id="645ab-137">回答這些問題之後，您就能選取最適合業務需求的選項。</span><span class="sxs-lookup"><span data-stu-id="645ab-137">By having answered those questions you will select which option best suits your business needs.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="645ab-138">後續步驟</span><span class="sxs-lookup"><span data-stu-id="645ab-138">Next steps</span></span>
[<span data-ttu-id="645ab-139">判斷存取控制需求</span><span class="sxs-lookup"><span data-stu-id="645ab-139">Determine access control requirements</span></span>](active-directory-hybrid-identity-design-considerations-accesscontrol-requirements.md)

## <a name="see-also"></a><span data-ttu-id="645ab-140">另請參閱</span><span class="sxs-lookup"><span data-stu-id="645ab-140">See Also</span></span>
[<span data-ttu-id="645ab-141">設計考量概觀</span><span class="sxs-lookup"><span data-stu-id="645ab-141">Design considerations overview</span></span>](active-directory-hybrid-identity-design-considerations-overview.md)

