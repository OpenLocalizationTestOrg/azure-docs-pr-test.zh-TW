---
title: "aaaAzure Active Directory 混合式身分識別設計考量-決定資料保護需求 |Microsoft 文件"
description: "當您規劃混合式身分識別解決方案，識別 hello 資料保護需求的業務及哪些選項可以使用 toobest 達到這些需求。"
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
ms.openlocfilehash: 189abf9affbc2894c322f362d84222d4e33d472e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="plan-for-enhancing-data-security-through-strong-identity-solution"></a><span data-ttu-id="c82dd-103">透過增強式身分識別解決方案規劃更高的資料安全性</span><span class="sxs-lookup"><span data-stu-id="c82dd-103">Plan for enhancing data security through strong identity solution</span></span>
<span data-ttu-id="c82dd-104">hello 第一個步驟 tooprotect hello 資料會識別哪些人可以存取該資料，而且這個程序的一部分，您需要的 toohave 系統 tooprovide 驗證和授權功能與整合，可以識別解決方案。</span><span class="sxs-lookup"><span data-stu-id="c82dd-104">hello first step tooprotect hello data is identify who can access that data and as part of this process you need toohave an identity solution that can integrates with your system tooprovide authentication and authorization capabilities.</span></span> <span data-ttu-id="c82dd-105">驗證和授權常被混淆，兩者角色也常被誤解。</span><span class="sxs-lookup"><span data-stu-id="c82dd-105">Authentication and authorization are often confused with each other and their roles misunderstood.</span></span> <span data-ttu-id="c82dd-106">在現實它們是完全不同，hello 圖所示：</span><span class="sxs-lookup"><span data-stu-id="c82dd-106">In reality they are quite different, as shown in hello figure below:</span></span>

![](./media/hybrid-id-design-considerations/mobile-devicemgt-lifecycle.png)

<span data-ttu-id="c82dd-107">**行動裝置管理生命週期階段**</span><span class="sxs-lookup"><span data-stu-id="c82dd-107">**Mobile device management lifecycle stages**</span></span>

<span data-ttu-id="c82dd-108">規劃您的混合式身分識別解決方案時必須了解您的業務和哪些選項可以使用 toobest hello 資料保護需求達到這些需求。</span><span class="sxs-lookup"><span data-stu-id="c82dd-108">When planning your hybrid identity solution you must understand hello data protection requirements for your business and which options are available toobest fulfil these requirements.</span></span>

> [!NOTE]
> <span data-ttu-id="c82dd-109">完成之後提供資料安全性規劃，檢閱[判斷多因素驗證需求](active-directory-hybrid-identity-design-considerations-multifactor-auth-requirements.md)tooensure 有關多因素驗證需求選擇了不受 hello 決策您進行這一節。</span><span class="sxs-lookup"><span data-stu-id="c82dd-109">Once you finish planning for data security, review [Determine multi-factor authentication requirements](active-directory-hybrid-identity-design-considerations-multifactor-auth-requirements.md) tooensure that your selections regarding multi-factor authentication requirements were not affected by hello decisions you made in this section.</span></span>
> 
> 

## <a name="determine-data-protection-requirements"></a><span data-ttu-id="c82dd-110">判斷資料保護需求</span><span class="sxs-lookup"><span data-stu-id="c82dd-110">Determine data protection requirements</span></span>
<span data-ttu-id="c82dd-111">在行動性 hello 時代，大部分的公司有共同的目標： 啟用其使用者 toobe 提高生產力在內部部署時，或從遠端在行動裝置上從任何地方順序 tooincrease 產能。</span><span class="sxs-lookup"><span data-stu-id="c82dd-111">In hello age of mobility, most companies have a common goal: enable their users toobe productive on their mobile devices while on-premises or remotely from anywhere in order tooincrease productivity.</span></span> <span data-ttu-id="c82dd-112">雖然這可能是共同的目標，公司已經有這類需求也會考量有關 hello 數量必須降低順序 tookeep 公司資料安全，並維護使用者的隱私權威脅。</span><span class="sxs-lookup"><span data-stu-id="c82dd-112">While this could be a common goal, companies that have such requirement will also be concern regarding hello amount of threats that must be mitigated in order tookeep company’s data secure and maintain user’s privacy.</span></span> <span data-ttu-id="c82dd-113">每一家公司可能會在這方面，有不同的需求不同的符合性規則，將使變化相應 toowhich 業界 hello 公司做將會導致 toodifferent 設計決策。</span><span class="sxs-lookup"><span data-stu-id="c82dd-113">Each company might have different requirements in this regard; different compliance rules that will vary according toowhich industry hello company is acting will lead toodifferent design decisions.</span></span> 

<span data-ttu-id="c82dd-114">不過，有一些安全性層面應該瀏覽及驗證，不論 hello 業界 hello 下一節中所說明。</span><span class="sxs-lookup"><span data-stu-id="c82dd-114">However, there are some security aspects that should be explored and validated, regardless of hello industry, which are explained in hello next section.</span></span>

## <a name="data-protection-paths"></a><span data-ttu-id="c82dd-115">資料保護路徑</span><span class="sxs-lookup"><span data-stu-id="c82dd-115">Data protection paths</span></span>
![](./media/hybrid-id-design-considerations/data-protection-paths.png)

<span data-ttu-id="c82dd-116">**資料保護路徑**</span><span class="sxs-lookup"><span data-stu-id="c82dd-116">**Data protection paths**</span></span>

<span data-ttu-id="c82dd-117">在上方圖表 hello，hello 識別元件，會驗證才能存取資料的第一個 toobe hello。</span><span class="sxs-lookup"><span data-stu-id="c82dd-117">In hello above diagram, hello identity component will be hello first one toobe verified before data is accessed.</span></span> <span data-ttu-id="c82dd-118">不過，此資料可以在不同狀態期間 hello 存取它。</span><span class="sxs-lookup"><span data-stu-id="c82dd-118">However, this data can be in different states during hello time it was accessed.</span></span> <span data-ttu-id="c82dd-119">此圖表上的每個數字，分別代表資料在某個時間點的所在的路徑。</span><span class="sxs-lookup"><span data-stu-id="c82dd-119">Each number on this diagram represents a path in which data can be located at some point in time.</span></span> <span data-ttu-id="c82dd-120">這些數字的說明如下：</span><span class="sxs-lookup"><span data-stu-id="c82dd-120">These numbers are explained below:</span></span>

1. <span data-ttu-id="c82dd-121">Hello 裝置層級的資料保護。</span><span class="sxs-lookup"><span data-stu-id="c82dd-121">Data protection at hello device level.</span></span>
2. <span data-ttu-id="c82dd-122">傳輸過程中的資料保護。</span><span class="sxs-lookup"><span data-stu-id="c82dd-122">Data protection while in transit.</span></span>
3. <span data-ttu-id="c82dd-123">在內部部署中待用時的資料保護。</span><span class="sxs-lookup"><span data-stu-id="c82dd-123">Data protection while at rest on-premises.</span></span>
4. <span data-ttu-id="c82dd-124">在 hello 雲端待用時的資料保護。</span><span class="sxs-lookup"><span data-stu-id="c82dd-124">Data protection while at rest in hello cloud.</span></span>

<span data-ttu-id="c82dd-125">雖然 hello 技術控制項，將允許這些階段的每個 IT tooprotect hello 資料本身不會直接提供 hello 混合式身分識別解決方案，則需要 hello 混合式身分識別解決方案能夠利用這兩個內部部署部署和雲端身分識別管理資源 tooidentify hello 使用者授與存取 toohello 資料之前。</span><span class="sxs-lookup"><span data-stu-id="c82dd-125">Although hello technical controls that will enable IT tooprotect hello data itself on each one of those phases are not directly offered by hello hybrid identity solution, it is necessary that hello hybrid identity solution is capable of leveraging both on-premises and cloud identity management resources tooidentify hello user before grant access toohello data.</span></span> <span data-ttu-id="c82dd-126">當您規劃混合式身分識別解決方案確定遵循該 hello 問題根據 tooyour 組織的需求：</span><span class="sxs-lookup"><span data-stu-id="c82dd-126">When planning your hybrid identity solution ensure that hello following questions are answered according tooyour organization’s requirements:</span></span>

## <a name="data-protection-at-rest"></a><span data-ttu-id="c82dd-127">保護待用資料</span><span class="sxs-lookup"><span data-stu-id="c82dd-127">Data protection at rest</span></span>
<span data-ttu-id="c82dd-128">不論其中 hello 資料是在靜止 （裝置、 雲端或內部部署），請務必 tooperform 評估 toounderstand hello 組織必須在這方面。</span><span class="sxs-lookup"><span data-stu-id="c82dd-128">Regardless of where hello data is at rest (device, cloud or on-premises), it is important tooperform an assessment toounderstand hello organization needs in this regard.</span></span> <span data-ttu-id="c82dd-129">這個區域中，請確定系統會要求該 hello 下列問題：</span><span class="sxs-lookup"><span data-stu-id="c82dd-129">For this area, ensure that hello following questions are asked:</span></span>

* <span data-ttu-id="c82dd-130">您的公司是否需要 tooprotect 待用的資料？</span><span class="sxs-lookup"><span data-stu-id="c82dd-130">Does your company need tooprotect data at rest?</span></span>
  * <span data-ttu-id="c82dd-131">如果是，請與您目前的內部部署基礎結構是否 hello 混合式身分識別解決方案可以 toointegrate？</span><span class="sxs-lookup"><span data-stu-id="c82dd-131">If yes, is hello hybrid identity solution able toointegrate with your current on-premises infrastructure?</span></span>
  * <span data-ttu-id="c82dd-132">如果是，請與您在 hello 雲端中的工作負載是否 hello 混合式身分識別解決方案可以 toointegrate？</span><span class="sxs-lookup"><span data-stu-id="c82dd-132">If yes, is hello hybrid identity solution able toointegrate with your workloads located in hello cloud?</span></span>
* <span data-ttu-id="c82dd-133">是 hello 雲端身分識別管理可以 tooprotect hello 使用者的認證和其他資料儲存在 hello 雲端？</span><span class="sxs-lookup"><span data-stu-id="c82dd-133">Is hello cloud identity management able tooprotect hello user’s credentials and other data stored in hello cloud?</span></span>

## <a name="data-protection-in-transit"></a><span data-ttu-id="c82dd-134">傳輸過程中的資料保護</span><span class="sxs-lookup"><span data-stu-id="c82dd-134">Data protection in transit</span></span>
<span data-ttu-id="c82dd-135">裝置 hello 與 hello 資料中心之間或 hello 裝置與 hello 雲端之間的傳輸中的資料必須加以保護。</span><span class="sxs-lookup"><span data-stu-id="c82dd-135">Data in transit between hello device and hello datacenter or between hello device and hello cloud must be protected.</span></span> <span data-ttu-id="c82dd-136">不過，所謂的傳輸中並不一定表示雲端服務外部元件的通訊程序；有時也可能在內部發生，像是兩個虛擬網路之間。</span><span class="sxs-lookup"><span data-stu-id="c82dd-136">However, being in-transit does not necessarily mean a communications process with a component outside of your cloud service; it moves internally, also, such as between two virtual networks.</span></span> <span data-ttu-id="c82dd-137">這個區域中，請確定系統會要求該 hello 下列問題：</span><span class="sxs-lookup"><span data-stu-id="c82dd-137">For this area, ensure that hello following questions are asked:</span></span>

* <span data-ttu-id="c82dd-138">您的公司是否需要在傳輸過程中的 tooprotect 資料？</span><span class="sxs-lookup"><span data-stu-id="c82dd-138">Does your company need tooprotect data in transit?</span></span>
  * <span data-ttu-id="c82dd-139">如果是，是否 hello 混合式身分識別解決方案可以 toointegrate 與安全的控制項，例如 SSL/TLS？</span><span class="sxs-lookup"><span data-stu-id="c82dd-139">If yes, is hello hybrid identity solution able toointegrate with secure controls such as SSL/TLS?</span></span>
* <span data-ttu-id="c82dd-140">沒有 hello 雲端身分識別管理可以保留 hello 流量 tooand hello 目錄存放區中 （在且資料中心之間） 簽署嗎？</span><span class="sxs-lookup"><span data-stu-id="c82dd-140">Does hello cloud identity management keep hello traffic tooand within hello directory store (within and between datacenters) signed?</span></span>

## <a name="compliance"></a><span data-ttu-id="c82dd-141">法規遵循</span><span class="sxs-lookup"><span data-stu-id="c82dd-141">Compliance</span></span>
<span data-ttu-id="c82dd-142">規範、 法律及法規遵循需求而異公司所屬的相應 toohello 產業。</span><span class="sxs-lookup"><span data-stu-id="c82dd-142">Regulations, laws and regulatory compliance requirements will vary according toohello industry that your company belongs.</span></span> <span data-ttu-id="c82dd-143">高管制產業中的公司必須先處理身分識別管理考量相關的 toocompliance 問題。</span><span class="sxs-lookup"><span data-stu-id="c82dd-143">Companies in high regulated industries must address identity-management concerns related toocompliance issues.</span></span> <span data-ttu-id="c82dd-144">例如沙氏法案 (SOX)、 hello 健康保險流通與責任法案 (HIPAA) 規定 hello Gramm-Leach-Bliley Act (GLBA) 和 hello 付款卡產業資料安全標準 (PCI DSS) 非常嚴格有關身分識別和存取。</span><span class="sxs-lookup"><span data-stu-id="c82dd-144">Regulations such as Sarbanes-Oxley (SOX), hello Health Insurance Portability and Accountability Act (HIPAA), hello Gramm-Leach-Bliley Act (GLBA) and hello Payment Card Industry Data Security Standard (PCI DSS) are very strict regarding identity and access.</span></span> <span data-ttu-id="c82dd-145">您的公司將採用的 hello 混合式身分識別解決方案必須都滿足 hello 需求的一或多個這些規定的 hello 核心功能。</span><span class="sxs-lookup"><span data-stu-id="c82dd-145">hello hybrid identity solution that your company will adopt must have hello core capabilities that will fulfill hello requirements of one or more of these regulations.</span></span> <span data-ttu-id="c82dd-146">這個區域中，請確定系統會要求該 hello 下列問題：</span><span class="sxs-lookup"><span data-stu-id="c82dd-146">For this area, ensure that hello following questions are asked:</span></span>

* <span data-ttu-id="c82dd-147">是 hello 混合式身分識別解決方案符合您公司的 hello 法規要求？</span><span class="sxs-lookup"><span data-stu-id="c82dd-147">Is hello hybrid identity solution compliant with hello regulatory requirements for your business?</span></span>
* <span data-ttu-id="c82dd-148">沒有 hello 混合式身分識別解決方案具有內建功能可讓您公司 toobe 符合法規需求？</span><span class="sxs-lookup"><span data-stu-id="c82dd-148">Does hello hybrid identity solution has built in capabilities that will enable your company toobe compliant regulatory requirements?</span></span> 

> [!NOTE]
> <span data-ttu-id="c82dd-149">請確定每個答案 tootake 附註，並了解 hello 回應 hello 背後的基本原理。</span><span class="sxs-lookup"><span data-stu-id="c82dd-149">Make sure tootake notes of each answer and understand hello rationale behind hello answer.</span></span> <span data-ttu-id="c82dd-150">[定義的資料保護策略](active-directory-hybrid-identity-design-considerations-data-protection-strategy.md)將介紹可用 hello 選項以及每個選項的優點/缺點。</span><span class="sxs-lookup"><span data-stu-id="c82dd-150">[Define Data Protection Strategy](active-directory-hybrid-identity-design-considerations-data-protection-strategy.md) will go over hello options available and advantages/disadvantages of each option.</span></span>  <span data-ttu-id="c82dd-151">回答這些問題之後，您就能選取最適合業務需求的選項。</span><span class="sxs-lookup"><span data-stu-id="c82dd-151">By having answered those questions you will select which option best suits your business needs.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="c82dd-152">後續步驟</span><span class="sxs-lookup"><span data-stu-id="c82dd-152">Next steps</span></span>
 [<span data-ttu-id="c82dd-153">判斷內容管理需求</span><span class="sxs-lookup"><span data-stu-id="c82dd-153">Determine content management requirements</span></span>](active-directory-hybrid-identity-design-considerations-contentmgt-requirements.md)

## <a name="see-also"></a><span data-ttu-id="c82dd-154">另請參閱</span><span class="sxs-lookup"><span data-stu-id="c82dd-154">See Also</span></span>
[<span data-ttu-id="c82dd-155">設計考量概觀</span><span class="sxs-lookup"><span data-stu-id="c82dd-155">Design considerations overview</span></span>](active-directory-hybrid-identity-design-considerations-overview.md)

