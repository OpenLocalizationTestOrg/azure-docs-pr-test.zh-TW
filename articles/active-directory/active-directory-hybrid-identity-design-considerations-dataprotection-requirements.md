---
title: "Azure Active Directory 混合式身分識別設計考量 - 判斷資料保護需求 | Microsoft Docs"
description: "在規劃混合式身分識別解決方案時，請識別您企業的資料保護需求，以及有哪些可用選項可充分因應這些需求。"
documentationcenter: 
services: active-directory
author: billmath
manager: femila
editor: 
ms.assetid: 40dc4baa-fe82-4ab6-a3e4-f36fa9dcd0df
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/18/2017
ms.author: billmath
ms.openlocfilehash: 96bf9d4c26a22f718c29804c11681199e775f589
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="plan-for-enhancing-data-security-through-strong-identity-solution"></a><span data-ttu-id="9f784-103">透過增強式身分識別解決方案規劃更高的資料安全性</span><span class="sxs-lookup"><span data-stu-id="9f784-103">Plan for enhancing data security through strong identity solution</span></span>
<span data-ttu-id="9f784-104">保護資料的第一個步驟，是識別誰可以存取該資料，而在此程序中，您必須要有可與您的系統整合以提供驗證和授權功能的身分識別解決方案。</span><span class="sxs-lookup"><span data-stu-id="9f784-104">The first step to protect the data is identify who can access that data and as part of this process you need to have an identity solution that can integrates with your system to provide authentication and authorization capabilities.</span></span> <span data-ttu-id="9f784-105">驗證和授權常被混淆，兩者角色也常被誤解。</span><span class="sxs-lookup"><span data-stu-id="9f784-105">Authentication and authorization are often confused with each other and their roles misunderstood.</span></span> <span data-ttu-id="9f784-106">這兩者其實是很不一樣的，如下圖所說明：</span><span class="sxs-lookup"><span data-stu-id="9f784-106">In reality they are quite different, as shown in the figure below:</span></span>

![](./media/hybrid-id-design-considerations/mobile-devicemgt-lifecycle.png)

<span data-ttu-id="9f784-107">**行動裝置管理生命週期階段**</span><span class="sxs-lookup"><span data-stu-id="9f784-107">**Mobile device management lifecycle stages**</span></span>

<span data-ttu-id="9f784-108">在規劃混合式身分識別解決方案時，您必須了解企業的資料保護需求，以及哪些選項最能因應這些需求。</span><span class="sxs-lookup"><span data-stu-id="9f784-108">When planning your hybrid identity solution you must understand the data protection requirements for your business and which options are available to best fulfil these requirements.</span></span>

> [!NOTE]
> <span data-ttu-id="9f784-109">完成資料安全性的規劃後，請檢閱 [判斷多因素驗證需求](active-directory-hybrid-identity-design-considerations-multifactor-auth-requirements.md) ，以確定您有關多因素驗證需求的選項不受您在這一節中所做決策的影響。</span><span class="sxs-lookup"><span data-stu-id="9f784-109">Once you finish planning for data security, review [Determine multi-factor authentication requirements](active-directory-hybrid-identity-design-considerations-multifactor-auth-requirements.md) to ensure that your selections regarding multi-factor authentication requirements were not affected by the decisions you made in this section.</span></span>
> 
> 

## <a name="determine-data-protection-requirements"></a><span data-ttu-id="9f784-110">判斷資料保護需求</span><span class="sxs-lookup"><span data-stu-id="9f784-110">Determine data protection requirements</span></span>
<span data-ttu-id="9f784-111">在行動裝置時代，大部分的公司都有共同的目標：讓使用者在行動裝置上提高生產力，無論是在內部部署，還是遠端的任何位置。</span><span class="sxs-lookup"><span data-stu-id="9f784-111">In the age of mobility, most companies have a common goal: enable their users to be productive on their mobile devices while on-premises or remotely from anywhere in order to increase productivity.</span></span> <span data-ttu-id="9f784-112">雖然可能有此共同目標，但有這類需求的公司也會顧慮必須要降低以保護公司資料安全和維護使用者隱私權的威脅數量。</span><span class="sxs-lookup"><span data-stu-id="9f784-112">While this could be a common goal, companies that have such requirement will also be concern regarding the amount of threats that must be mitigated in order to keep company’s data secure and maintain user’s privacy.</span></span> <span data-ttu-id="9f784-113">每一家公司在這方面可能會有不同的需求；會隨著公司所屬產業而異的符合性規則，會產生不同的設計決策。</span><span class="sxs-lookup"><span data-stu-id="9f784-113">Each company might have different requirements in this regard; different compliance rules that will vary according to which industry the company is acting will lead to different design decisions.</span></span> 

<span data-ttu-id="9f784-114">但無論是何種產業，都有一些安全性層面是必須探索並驗證的，這將在下一節說明。</span><span class="sxs-lookup"><span data-stu-id="9f784-114">However, there are some security aspects that should be explored and validated, regardless of the industry, which are explained in the next section.</span></span>

## <a name="data-protection-paths"></a><span data-ttu-id="9f784-115">資料保護路徑</span><span class="sxs-lookup"><span data-stu-id="9f784-115">Data protection paths</span></span>
![](./media/hybrid-id-design-considerations/data-protection-paths.png)

<span data-ttu-id="9f784-116">**資料保護路徑**</span><span class="sxs-lookup"><span data-stu-id="9f784-116">**Data protection paths**</span></span>

<span data-ttu-id="9f784-117">在上圖中，身分識別元件將是在存取資料之前最先受到驗證的。</span><span class="sxs-lookup"><span data-stu-id="9f784-117">In the above diagram, the identity component will be the first one to be verified before data is accessed.</span></span> <span data-ttu-id="9f784-118">不過，這項資料在受到存取期間可能會處於不同的狀態。</span><span class="sxs-lookup"><span data-stu-id="9f784-118">However, this data can be in different states during the time it was accessed.</span></span> <span data-ttu-id="9f784-119">此圖表上的每個數字，分別代表資料在某個時間點的所在的路徑。</span><span class="sxs-lookup"><span data-stu-id="9f784-119">Each number on this diagram represents a path in which data can be located at some point in time.</span></span> <span data-ttu-id="9f784-120">這些數字的說明如下：</span><span class="sxs-lookup"><span data-stu-id="9f784-120">These numbers are explained below:</span></span>

1. <span data-ttu-id="9f784-121">裝置層級的資料保護。</span><span class="sxs-lookup"><span data-stu-id="9f784-121">Data protection at the device level.</span></span>
2. <span data-ttu-id="9f784-122">傳輸過程中的資料保護。</span><span class="sxs-lookup"><span data-stu-id="9f784-122">Data protection while in transit.</span></span>
3. <span data-ttu-id="9f784-123">在內部部署中待用時的資料保護。</span><span class="sxs-lookup"><span data-stu-id="9f784-123">Data protection while at rest on-premises.</span></span>
4. <span data-ttu-id="9f784-124">在雲端中待用時的資料保護。</span><span class="sxs-lookup"><span data-stu-id="9f784-124">Data protection while at rest in the cloud.</span></span>

<span data-ttu-id="9f784-125">雖然混合式身分識別解決方案並未直接提供可讓 IT 人員在每一個階段保護資料本身的技術性控制，但混合式身分識別解決方案仍必須能夠運用內部部署和雲端管理資源，在授與資料的存取權之前識別使用者。</span><span class="sxs-lookup"><span data-stu-id="9f784-125">Although the technical controls that will enable IT to protect the data itself on each one of those phases are not directly offered by the hybrid identity solution, it is necessary that the hybrid identity solution is capable of leveraging both on-premises and cloud identity management resources to identify the user before grant access to the data.</span></span> <span data-ttu-id="9f784-126">規劃您的混合式身分識別解決方案時，請確定會根據貴組織的需求來回答下列問題：</span><span class="sxs-lookup"><span data-stu-id="9f784-126">When planning your hybrid identity solution ensure that the following questions are answered according to your organization’s requirements:</span></span>

## <a name="data-protection-at-rest"></a><span data-ttu-id="9f784-127">保護待用資料</span><span class="sxs-lookup"><span data-stu-id="9f784-127">Data protection at rest</span></span>
<span data-ttu-id="9f784-128">不論資料是在何處待用 (裝置、雲端或內部部署)，請務必執行評估，以了解組織在這方面的需求。</span><span class="sxs-lookup"><span data-stu-id="9f784-128">Regardless of where the data is at rest (device, cloud or on-premises), it is important to perform an assessment to understand the organization needs in this regard.</span></span> <span data-ttu-id="9f784-129">針對這個層面，請確實回答下列問題：</span><span class="sxs-lookup"><span data-stu-id="9f784-129">For this area, ensure that the following questions are asked:</span></span>

* <span data-ttu-id="9f784-130">您的公司需要保護待用資料嗎？</span><span class="sxs-lookup"><span data-stu-id="9f784-130">Does your company need to protect data at rest?</span></span>
  * <span data-ttu-id="9f784-131">如果是，混合式身分識別解決方案是否能夠與您目前的內部部署基礎結構整合？</span><span class="sxs-lookup"><span data-stu-id="9f784-131">If yes, is the hybrid identity solution able to integrate with your current on-premises infrastructure?</span></span>
  * <span data-ttu-id="9f784-132">如果是，混合式身分識別解決方案是否能夠與您在雲端中的工作負載整合？</span><span class="sxs-lookup"><span data-stu-id="9f784-132">If yes, is the hybrid identity solution able to integrate with your workloads located in the cloud?</span></span>
* <span data-ttu-id="9f784-133">雲端身分識別管理是否能夠保護使用者的認證，和其他儲存在雲端中的資料？</span><span class="sxs-lookup"><span data-stu-id="9f784-133">Is the cloud identity management able to protect the user’s credentials and other data stored in the cloud?</span></span>

## <a name="data-protection-in-transit"></a><span data-ttu-id="9f784-134">傳輸過程中的資料保護</span><span class="sxs-lookup"><span data-stu-id="9f784-134">Data protection in transit</span></span>
<span data-ttu-id="9f784-135">在裝置與資料中心之間或裝置與雲端之間傳輸的資料，必須受到保護。</span><span class="sxs-lookup"><span data-stu-id="9f784-135">Data in transit between the device and the datacenter or between the device and the cloud must be protected.</span></span> <span data-ttu-id="9f784-136">不過，所謂的傳輸中並不一定表示雲端服務外部元件的通訊程序；有時也可能在內部發生，像是兩個虛擬網路之間。</span><span class="sxs-lookup"><span data-stu-id="9f784-136">However, being in-transit does not necessarily mean a communications process with a component outside of your cloud service; it moves internally, also, such as between two virtual networks.</span></span> <span data-ttu-id="9f784-137">針對這個層面，請確實回答下列問題：</span><span class="sxs-lookup"><span data-stu-id="9f784-137">For this area, ensure that the following questions are asked:</span></span>

* <span data-ttu-id="9f784-138">您的公司需要保護傳輸中的資料嗎？</span><span class="sxs-lookup"><span data-stu-id="9f784-138">Does your company need to protect data in transit?</span></span>
  * <span data-ttu-id="9f784-139">如果是，混合式身分識別解決方案是否能夠與 SSL/TLS 之類的安全控制項整合？</span><span class="sxs-lookup"><span data-stu-id="9f784-139">If yes, is the hybrid identity solution able to integrate with secure controls such as SSL/TLS?</span></span>
* <span data-ttu-id="9f784-140">雲端身分識別管理是否可確保進入和存在於目錄的流量 (在資料中心之中和之間) 進行簽署？</span><span class="sxs-lookup"><span data-stu-id="9f784-140">Does the cloud identity management keep the traffic to and within the directory store (within and between datacenters) signed?</span></span>

## <a name="compliance"></a><span data-ttu-id="9f784-141">法規遵循</span><span class="sxs-lookup"><span data-stu-id="9f784-141">Compliance</span></span>
<span data-ttu-id="9f784-142">規定、法律和法規遵循需求會隨著您的公司所屬的產業而有所不同。</span><span class="sxs-lookup"><span data-stu-id="9f784-142">Regulations, laws and regulatory compliance requirements will vary according to the industry that your company belongs.</span></span> <span data-ttu-id="9f784-143">受到嚴格規範的公司，必須處理與法規遵循有關的身分識別管理問題。</span><span class="sxs-lookup"><span data-stu-id="9f784-143">Companies in high regulated industries must address identity-management concerns related to compliance issues.</span></span> <span data-ttu-id="9f784-144">諸如沙賓法案 (SOX)、健康保險流通與責任法案 (HIPAA)、美國金融服務法案 (GLBA) 和支付卡產業資料安全標準 (PCI DSS) 等法規，在身分識別和存取方面都有非常嚴格的規定。</span><span class="sxs-lookup"><span data-stu-id="9f784-144">Regulations such as Sarbanes-Oxley (SOX), the Health Insurance Portability and Accountability Act (HIPAA), the Gramm-Leach-Bliley Act (GLBA) and the Payment Card Industry Data Security Standard (PCI DSS) are very strict regarding identity and access.</span></span> <span data-ttu-id="9f784-145">您的公司所將採用的混合式身分識別解決方案，必須具有核心功能可因應這些法規的一或多項需求。</span><span class="sxs-lookup"><span data-stu-id="9f784-145">The hybrid identity solution that your company will adopt must have the core capabilities that will fulfill the requirements of one or more of these regulations.</span></span> <span data-ttu-id="9f784-146">針對這個層面，請確實回答下列問題：</span><span class="sxs-lookup"><span data-stu-id="9f784-146">For this area, ensure that the following questions are asked:</span></span>

* <span data-ttu-id="9f784-147">混合式身分識別解決方案是否符合貴公司的法規需求？</span><span class="sxs-lookup"><span data-stu-id="9f784-147">Is the hybrid identity solution compliant with the regulatory requirements for your business?</span></span>
* <span data-ttu-id="9f784-148">混合式身分識別解決方案是否有內建功能可讓您的公司符合法規需求？</span><span class="sxs-lookup"><span data-stu-id="9f784-148">Does the hybrid identity solution has built in capabilities that will enable your company to be compliant regulatory requirements?</span></span> 

> [!NOTE]
> <span data-ttu-id="9f784-149">請確定會記下每個答案，並了解答案背後的原理。</span><span class="sxs-lookup"><span data-stu-id="9f784-149">Make sure to take notes of each answer and understand the rationale behind the answer.</span></span> <span data-ttu-id="9f784-150">[定義資料保護策略](active-directory-hybrid-identity-design-considerations-data-protection-strategy.md) 將介紹可用選項，以及每個選項的優點/缺點。</span><span class="sxs-lookup"><span data-stu-id="9f784-150">[Define Data Protection Strategy](active-directory-hybrid-identity-design-considerations-data-protection-strategy.md) will go over the options available and advantages/disadvantages of each option.</span></span>  <span data-ttu-id="9f784-151">回答這些問題之後，您就能選取最適合業務需求的選項。</span><span class="sxs-lookup"><span data-stu-id="9f784-151">By having answered those questions you will select which option best suits your business needs.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="9f784-152">後續步驟</span><span class="sxs-lookup"><span data-stu-id="9f784-152">Next steps</span></span>
 [<span data-ttu-id="9f784-153">判斷內容管理需求</span><span class="sxs-lookup"><span data-stu-id="9f784-153">Determine content management requirements</span></span>](active-directory-hybrid-identity-design-considerations-contentmgt-requirements.md)

## <a name="see-also"></a><span data-ttu-id="9f784-154">另請參閱</span><span class="sxs-lookup"><span data-stu-id="9f784-154">See Also</span></span>
[<span data-ttu-id="9f784-155">設計考量概觀</span><span class="sxs-lookup"><span data-stu-id="9f784-155">Design considerations overview</span></span>](active-directory-hybrid-identity-design-considerations-overview.md)

