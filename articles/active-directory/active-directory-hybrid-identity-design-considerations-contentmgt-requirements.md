---
title: "Azure Active Directory 混合式身分識別設計考量 - 判斷內容管理需求|Microsoft Docs"
description: "深入了解如何判斷適合您企業的內容管理需求。 通常當使用者擁有自己的裝置時，可能也會有多個認證，將根據其使用的應用程式來替換。 請務必區分使用個人認證建立的內容以及使用公司認證建立的內容。 您的身分識別解決方案應該能夠與雲端服務互動，為使用者提供順暢的體驗，同時確保其隱私權並提高保護來防止資料外洩。"
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
ms.openlocfilehash: 840de1e1fcba74285788d51d8f544375f0affa77
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="determine-content-management-requirements-for-your-hybrid-identity-solution"></a><span data-ttu-id="d5245-106">判斷混合式身分識別解決方案的內容管理需求</span><span class="sxs-lookup"><span data-stu-id="d5245-106">Determine content management requirements for your hybrid identity solution</span></span>
<span data-ttu-id="d5245-107">了解適合您企業的內容管理需求，可能會直接影響您決定要使用哪一個混合式身分識別解決方案。</span><span class="sxs-lookup"><span data-stu-id="d5245-107">Understanding the content management requirements for your business may direct affect your decision on which hybrid identity solution to use.</span></span> <span data-ttu-id="d5245-108">由於裝置數目激增，而且可讓使用者攜帶自己的裝置 ([BYOD](http://aka.ms/byodcg))，所以公司必須保護它自己的資料，但它也必須完整保持使用者的隱私權。</span><span class="sxs-lookup"><span data-stu-id="d5245-108">With the proliferation of multiple devices and the capability of users to bring their own devices ([BYOD](http://aka.ms/byodcg)), the company must protect its own data but it also must keep user’s privacy intact.</span></span> <span data-ttu-id="d5245-109">通常當使用者擁有自己的裝置時，可能也會有多個認證，將根據其使用的應用程式來替換。</span><span class="sxs-lookup"><span data-stu-id="d5245-109">Usually when a user has his own device he might have also multiple credentials that will be alternating according to the application that he uses.</span></span> <span data-ttu-id="d5245-110">請務必區分使用個人認證建立的內容以及使用公司認證建立的內容。</span><span class="sxs-lookup"><span data-stu-id="d5245-110">It is important to differentiate what content was created using personal credentials versus the ones created using corporate credentials.</span></span> <span data-ttu-id="d5245-111">您的身分識別解決方案應該能夠與雲端服務互動，為使用者提供順暢的體驗，同時確保其隱私權並提高保護來防止資料外洩。</span><span class="sxs-lookup"><span data-stu-id="d5245-111">Your identity solution should be able to interact with cloud services to provide a seamless experience to the end user while ensure his privacy and increase the protection against data leakage.</span></span> 

<span data-ttu-id="d5245-112">您的身分識別解決方案是透過不同技術控制項來運用，以便提供內容管理，如下圖所示：</span><span class="sxs-lookup"><span data-stu-id="d5245-112">Your identity solution will be leveraged by different technical controls in order to provide content management as shown in the figure below:</span></span>

![](./media/hybrid-id-design-considerations/securitycontrols.png)

<span data-ttu-id="d5245-113">**充分運用身分識別管理系統的安全性控制項**</span><span class="sxs-lookup"><span data-stu-id="d5245-113">**Security controls that will be leveraging your identity management system**</span></span>

<span data-ttu-id="d5245-114">一般而言，內容管理需求將在下列區域中充分運用您的身分識別管理系統：</span><span class="sxs-lookup"><span data-stu-id="d5245-114">In general, content management requirements will leverage your identity management system in the following areas:</span></span>

* <span data-ttu-id="d5245-115">隱私權：識別擁有資源的使用者，並套用適當的控制項來保有完整性。</span><span class="sxs-lookup"><span data-stu-id="d5245-115">Privacy: identifying the user that owns a resource and applying the appropriate controls to maintain integrity.</span></span>
* <span data-ttu-id="d5245-116">資料分類：識別使用者或群組，以及根據物件分類來識別該物件的存取層級。</span><span class="sxs-lookup"><span data-stu-id="d5245-116">Data Classification: identify the user or group and level of access to an object according to its classification.</span></span> 
* <span data-ttu-id="d5245-117">資料外洩防護：負責保護資料以避免外洩的安全性控制項將需要與身分驗證系統互動，來驗證使用者的身分識別。</span><span class="sxs-lookup"><span data-stu-id="d5245-117">Data Leakage Protection: security controls responsible for protecting data to avoid leakage will need to interact with the identity system to validate the user’s identity.</span></span> <span data-ttu-id="d5245-118">這對於稽核記錄用途也很重要。</span><span class="sxs-lookup"><span data-stu-id="d5245-118">This is also important for auditing trail purpose.</span></span>

> [!NOTE]
> <span data-ttu-id="d5245-119">如需資料分類的最佳做法與指導方針，請參閱 [雲端整備的資料分類](http://download.microsoft.com/download/0/A/3/0A3BE969-85C5-4DD2-83B6-366AA71D1FE3/Data-Classification-for-Cloud-Readiness.pdf) 。</span><span class="sxs-lookup"><span data-stu-id="d5245-119">Read [data classification for cloud readiness](http://download.microsoft.com/download/0/A/3/0A3BE969-85C5-4DD2-83B6-366AA71D1FE3/Data-Classification-for-Cloud-Readiness.pdf) for more information about best practices and guidelines for data classification.</span></span>
> 
> 

<span data-ttu-id="d5245-120">規劃您的混合式身分識別解決方案時，請確定會根據貴組織的需求來回答下列問題：</span><span class="sxs-lookup"><span data-stu-id="d5245-120">When planning your hybrid identity solution ensure that the following questions are answered according to your organization’s requirements:</span></span>

* <span data-ttu-id="d5245-121">貴公司擁有適當的安全性控制項，可用來強制執行資料隱私權嗎？</span><span class="sxs-lookup"><span data-stu-id="d5245-121">Does your company have security controls in place to enforce data privacy?</span></span>
  * <span data-ttu-id="d5245-122">如果是，這些安全性控制項將能夠與您即將採用的混合式身分識別解決方案整合嗎？</span><span class="sxs-lookup"><span data-stu-id="d5245-122">If yes, will those security controls be able to integrate with the hybrid identity solution that you are going to adopt?</span></span>
* <span data-ttu-id="d5245-123">貴公司是否使用資料分類？</span><span class="sxs-lookup"><span data-stu-id="d5245-123">Does your company use data classification?</span></span>
  * <span data-ttu-id="d5245-124">如果是，目前的解決方案能夠與您即將採用的混合式身分識別解決方案整合嗎？</span><span class="sxs-lookup"><span data-stu-id="d5245-124">If yes, is the current solution able to integrate with the hybrid identity solution that you are going to adopt?</span></span>
* <span data-ttu-id="d5245-125">貴公司目前對於資料外洩有任何解決方案嗎？</span><span class="sxs-lookup"><span data-stu-id="d5245-125">Does your company currently have any solution for data leakage?</span></span> 
  * <span data-ttu-id="d5245-126">如果是，目前的解決方案能夠與您即將採用的混合式身分識別解決方案整合嗎？</span><span class="sxs-lookup"><span data-stu-id="d5245-126">If yes, is the current solution able to integrate with the hybrid identity solution that you are going to adopt?</span></span>
* <span data-ttu-id="d5245-127">貴公司需要稽核資源的存取嗎？</span><span class="sxs-lookup"><span data-stu-id="d5245-127">Does your company need to audit access to resources?</span></span>
  * <span data-ttu-id="d5245-128">如果是，是哪種類型的資源？</span><span class="sxs-lookup"><span data-stu-id="d5245-128">If yes, what type of resources?</span></span>
  * <span data-ttu-id="d5245-129">如果是，需要哪一個資訊層級？</span><span class="sxs-lookup"><span data-stu-id="d5245-129">If yes, what level of information is necessary?</span></span>
  * <span data-ttu-id="d5245-130">如果是，稽核記錄檔必須位於何處？</span><span class="sxs-lookup"><span data-stu-id="d5245-130">If yes, where the audit log must reside?</span></span> <span data-ttu-id="d5245-131">內部部署或在雲端中？</span><span class="sxs-lookup"><span data-stu-id="d5245-131">On-premises or in the cloud?</span></span>
* <span data-ttu-id="d5245-132">貴公司需要加密任何包含機密資料 (SSN、信用卡號碼等) 的電子郵件嗎？</span><span class="sxs-lookup"><span data-stu-id="d5245-132">Does your company need to encrypt any emails that contain sensitive data (SSNs, credit card numbers, etc)?</span></span>
* <span data-ttu-id="d5245-133">貴公司需要加密所有與外部商務合作夥伴共用的文件/內容嗎？</span><span class="sxs-lookup"><span data-stu-id="d5245-133">Does your company need to encrypt all documents/contents shared with external business partners?</span></span>
* <span data-ttu-id="d5245-134">貴公司需要強制執行有關特定電子郵件類型的公司原則 (不要全部回覆、不要轉寄) 嗎？</span><span class="sxs-lookup"><span data-stu-id="d5245-134">Does your company need to enforce corporate policies on certain kinds of emails (do no reply all, do not forward)?</span></span>

> [!NOTE]
> <span data-ttu-id="d5245-135">請確定會記下每個答案，並了解答案背後的原理。</span><span class="sxs-lookup"><span data-stu-id="d5245-135">Make sure to take notes of each answer and understand the rationale behind the answer.</span></span> <span data-ttu-id="d5245-136">[定義資料保護策略](active-directory-hybrid-identity-design-considerations-data-protection-strategy.md) 將介紹可用選項，以及每個選項的優點/缺點。</span><span class="sxs-lookup"><span data-stu-id="d5245-136">[Define Data Protection Strategy](active-directory-hybrid-identity-design-considerations-data-protection-strategy.md) will go over the options available and advantages/disadvantages of each option.</span></span>  <span data-ttu-id="d5245-137">回答這些問題之後，您就能選取最適合業務需求的選項。</span><span class="sxs-lookup"><span data-stu-id="d5245-137">By having answered those questions you will select which option best suits your business needs.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="d5245-138">後續步驟</span><span class="sxs-lookup"><span data-stu-id="d5245-138">Next steps</span></span>
[<span data-ttu-id="d5245-139">判斷存取控制需求</span><span class="sxs-lookup"><span data-stu-id="d5245-139">Determine access control requirements</span></span>](active-directory-hybrid-identity-design-considerations-accesscontrol-requirements.md)

## <a name="see-also"></a><span data-ttu-id="d5245-140">另請參閱</span><span class="sxs-lookup"><span data-stu-id="d5245-140">See Also</span></span>
[<span data-ttu-id="d5245-141">設計考量概觀</span><span class="sxs-lookup"><span data-stu-id="d5245-141">Design considerations overview</span></span>](active-directory-hybrid-identity-design-considerations-overview.md)

