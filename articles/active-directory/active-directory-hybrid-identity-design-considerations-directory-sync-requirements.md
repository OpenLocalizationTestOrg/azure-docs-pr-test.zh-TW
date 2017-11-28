---
title: "aaaAzure Active Directory 混合式身分識別設計考量-判斷目錄同步處理需求 |Microsoft 文件"
description: "識別哪些需求所需的同步處理之間的所有 hello 使用者在 = 內部部署與雲端 hello 企業版。"
documentationcenter: 
services: active-directory
author: billmath
manager: femila
editor: 
ms.assetid: 593eaa71-17eb-4c16-8c98-43cc62987e65
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/18/2017
ms.author: billmath
ms.openlocfilehash: 6646e3792c65f37c3d62eecdb6c6f3bd257f04f1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="determine-directory-synchronization-requirements"></a><span data-ttu-id="a9a99-103">判斷目錄同步處理需求</span><span class="sxs-lookup"><span data-stu-id="a9a99-103">Determine directory synchronization requirements</span></span>
<span data-ttu-id="a9a99-104">同步處理就是要為使用者提供其內部部署識別基礎 hello 雲端中的身分識別。</span><span class="sxs-lookup"><span data-stu-id="a9a99-104">Synchronization is all about providing users an identity in hello cloud based on their on-premises identity.</span></span> <span data-ttu-id="a9a99-105">它們會使用同步的帳戶進行驗證或同盟的驗證，hello 使用者仍需要 toohave hello 雲端中的身分識別。</span><span class="sxs-lookup"><span data-stu-id="a9a99-105">Whether or not they will use synchronized account for authentication or federated authentication, hello users will still need toohave an identity in hello cloud.</span></span>  <span data-ttu-id="a9a99-106">這個識別會需要 toobe 維護而定期更新。</span><span class="sxs-lookup"><span data-stu-id="a9a99-106">This identity will need toobe maintained and updated periodically.</span></span>  <span data-ttu-id="a9a99-107">hello 更新可以有許多形式，標題變更 toopassword 的變更。</span><span class="sxs-lookup"><span data-stu-id="a9a99-107">hello updates can take many forms, from title changes toopassword changes.</span></span>  

<span data-ttu-id="a9a99-108">請先評估 hello 組織在內部部署身分識別方案及使用者需求。</span><span class="sxs-lookup"><span data-stu-id="a9a99-108">Start by evaluating hello organizations on-premises identity solution and user requirements.</span></span> <span data-ttu-id="a9a99-109">這項評估是重要 toodefine hello 技術的需求會如何建立和維護 hello 雲端中使用者身分識別。</span><span class="sxs-lookup"><span data-stu-id="a9a99-109">This evaluation is important toodefine hello technical requirements for how user identities will be created and maintained in hello cloud.</span></span>  <span data-ttu-id="a9a99-110">對於大多數的組織，Active Directory 內部部署且將會透過將使用者的 hello 在內部部署目錄同步處理從，不過在某些情況下就會無法 hello 案例。</span><span class="sxs-lookup"><span data-stu-id="a9a99-110">For a majority of organizations, Active Directory is on-premises and will be hello on-premises directory that users will by synchronized from, however in some cases this will not be hello case.</span></span>  

<span data-ttu-id="a9a99-111">請確定 tooanswer hello 下列問題：</span><span class="sxs-lookup"><span data-stu-id="a9a99-111">Make sure tooanswer hello following questions:</span></span>

* <span data-ttu-id="a9a99-112">您擁有一或多個 AD 樹系，或者完全沒有嗎？</span><span class="sxs-lookup"><span data-stu-id="a9a99-112">Do you have one AD forest, multiple, or none?</span></span>
  
  * <span data-ttu-id="a9a99-113">您要進行同步處理的 Azure AD 目錄有多少個？</span><span class="sxs-lookup"><span data-stu-id="a9a99-113">How many Azure AD directories will you be synchronizing to?</span></span>
    
    1. <span data-ttu-id="a9a99-114">您會使用篩選嗎？</span><span class="sxs-lookup"><span data-stu-id="a9a99-114">Are you using filtering?</span></span>
    2. <span data-ttu-id="a9a99-115">您是否規劃了多部 Azure AD Connect 伺服器？</span><span class="sxs-lookup"><span data-stu-id="a9a99-115">Do you have multiple Azure AD Connect servers planned?</span></span>
* <span data-ttu-id="a9a99-116">您目前沒有內部部署的同步處理工具嗎？</span><span class="sxs-lookup"><span data-stu-id="a9a99-116">Do you currently have a synchronization tool on-premises?</span></span>
  
  * <span data-ttu-id="a9a99-117">如果是，您的使用者是否具有虛擬目錄/身分識別整合？</span><span class="sxs-lookup"><span data-stu-id="a9a99-117">If yes, does your users if users have a virtual directory/integration of identities?</span></span>
* <span data-ttu-id="a9a99-118">您是否有任何其他目錄內部的 toosynchronize （例如 LDAP 目錄，HR 資料庫等等）？</span><span class="sxs-lookup"><span data-stu-id="a9a99-118">Do you have any other directory on-premises that you want toosynchronize (e.g. LDAP Directory, HR database, etc)?</span></span>
  * <span data-ttu-id="a9a99-119">您會執行任何 GALSync toobe 嗎？</span><span class="sxs-lookup"><span data-stu-id="a9a99-119">Are you going toobe doing any GALSync?</span></span>
  * <span data-ttu-id="a9a99-120">Hello 目前狀態的 upn，請在您的組織為何？</span><span class="sxs-lookup"><span data-stu-id="a9a99-120">What is hello current state of UPNs in your organization?</span></span> 
  * <span data-ttu-id="a9a99-121">您擁有使用者要對其進行驗證的其他目錄嗎？</span><span class="sxs-lookup"><span data-stu-id="a9a99-121">Do you have a different directory that users authenticate against?</span></span>
  * <span data-ttu-id="a9a99-122">貴公司是否使用 Microsoft Exchange？</span><span class="sxs-lookup"><span data-stu-id="a9a99-122">Does your company use Microsoft Exchange?</span></span>
    * <span data-ttu-id="a9a99-123">他們是否規劃擁有混合式交換部署？</span><span class="sxs-lookup"><span data-stu-id="a9a99-123">Do they plan of having a hybrid exchange deployment?</span></span>

<span data-ttu-id="a9a99-124">既然您已了解關於同步處理要求時，您需要哪一種工具是 hello 正確一個 toomeet toodetermine 這些需求。</span><span class="sxs-lookup"><span data-stu-id="a9a99-124">Now that you have an idea about your synchronization requirements, you need toodetermine which tool is hello correct one toomeet these requirements.</span></span>  <span data-ttu-id="a9a99-125">Microsoft 提供數個工具 tooaccomplish 目錄整合及同步處理。</span><span class="sxs-lookup"><span data-stu-id="a9a99-125">Microsoft provides several tools tooaccomplish directory integration and synchronization.</span></span>  <span data-ttu-id="a9a99-126">請參閱 hello[混合式身分識別目錄整合工具比較資料表](active-directory-hybrid-identity-design-considerations-tools-comparison.md)如需詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="a9a99-126">See hello [Hybrid Identity directory integration tools comparison table](active-directory-hybrid-identity-design-considerations-tools-comparison.md) for more information.</span></span> 

<span data-ttu-id="a9a99-127">您已經有您的同步處理需求及 hello 工具，將會完成這項作業為您的公司，您需要使用這些目錄服務的 tooevaluate hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="a9a99-127">Now that you have your synchronization requirements and hello tool that will accomplish this for your company, you need tooevaluate hello applications that use these directory services.</span></span> <span data-ttu-id="a9a99-128">這項評估是重要 toodefine hello 技術需求 toointegrate 這些應用程式 toohello 雲端。</span><span class="sxs-lookup"><span data-stu-id="a9a99-128">This evaluation is important toodefine hello technical requirements toointegrate these applications toohello cloud.</span></span> <span data-ttu-id="a9a99-129">請確定 tooanswer hello 下列問題：</span><span class="sxs-lookup"><span data-stu-id="a9a99-129">Make sure tooanswer hello following questions:</span></span>

* <span data-ttu-id="a9a99-130">這些應用程式將會移動的 toohello 雲端，然後使用 hello 目錄嗎？</span><span class="sxs-lookup"><span data-stu-id="a9a99-130">Will these applications be moved toohello cloud and use hello directory?</span></span>
* <span data-ttu-id="a9a99-131">是否有特殊的屬性，這些應用程式可以成功地使用需要同步處理的 toobe toohello 雲端？</span><span class="sxs-lookup"><span data-stu-id="a9a99-131">Are there special attributes that need toobe synchronized toohello cloud so these applications can use them successfully?</span></span>
* <span data-ttu-id="a9a99-132">將這些應用程式需要 toobe 重寫 tootake 利用雲端驗證？</span><span class="sxs-lookup"><span data-stu-id="a9a99-132">Will these applications need toobe re-written tootake advantage of cloud auth?</span></span>
* <span data-ttu-id="a9a99-133">將這些應用程式繼續 toolive 在內部部署使用者進行存取時使用 hello 雲端識別身分嗎？</span><span class="sxs-lookup"><span data-stu-id="a9a99-133">Will these applications continue toolive on-premises while users access them using hello cloud identity?</span></span>

<span data-ttu-id="a9a99-134">您也需要 toodetermine hello 安全性需求和限制目錄同步作業。</span><span class="sxs-lookup"><span data-stu-id="a9a99-134">You also need toodetermine hello security requirements and constraints directory synchronization.</span></span> <span data-ttu-id="a9a99-135">這項評估是重要 tooget hello 需求，將會需要順序 toocreate 和維護 hello 雲端中的使用者身分識別的清單。</span><span class="sxs-lookup"><span data-stu-id="a9a99-135">This evaluation is important tooget a list of hello requirements that will be needed in order toocreate and maintain user’s identities in hello cloud.</span></span> <span data-ttu-id="a9a99-136">請確定 tooanswer hello 下列問題：</span><span class="sxs-lookup"><span data-stu-id="a9a99-136">Make sure tooanswer hello following questions:</span></span>

* <span data-ttu-id="a9a99-137">會 hello 同步伺服器是所在？</span><span class="sxs-lookup"><span data-stu-id="a9a99-137">Where will hello synchronization server be located?</span></span>
* <span data-ttu-id="a9a99-138">它將會加入網域嗎？</span><span class="sxs-lookup"><span data-stu-id="a9a99-138">Will it be domain joined?</span></span>
* <span data-ttu-id="a9a99-139">將在防火牆後面，例如 DMZ 在受限網路上找到 hello 伺服器嗎？</span><span class="sxs-lookup"><span data-stu-id="a9a99-139">Will hello server be located on a restricted network behind a firewall, such as a DMZ?</span></span>
  * <span data-ttu-id="a9a99-140">您將無法 tooopen hello 需要防火牆連接埠 toosupport 同步處理？</span><span class="sxs-lookup"><span data-stu-id="a9a99-140">Will you be able tooopen hello required firewall ports toosupport synchronization?</span></span>
* <span data-ttu-id="a9a99-141">您有 hello 同步處理伺服器的災害復原計劃嗎？</span><span class="sxs-lookup"><span data-stu-id="a9a99-141">Do you have a disaster recovery plan for hello synchronization server?</span></span>
* <span data-ttu-id="a9a99-142">您有適用於所有樹系，您想要使用 toosynch hello 正確的權限的帳戶嗎？</span><span class="sxs-lookup"><span data-stu-id="a9a99-142">Do you have an account with hello correct permissions for all forests you want toosynch with?</span></span>
  * <span data-ttu-id="a9a99-143">如果您的公司不知道 hello 解答這個問題，請檢閱 hello 文章中的 hello 節 < 密碼同步化的權限 >[安裝 hello Azure Active Directory 同步處理服務](https://msdn.microsoft.com/library/azure/dn757602.aspx#BKMK_CreateAnADAccountForTheSyncService)並判斷是否已經有與這些權限的帳戶，或如果您需要一個 toocreate。</span><span class="sxs-lookup"><span data-stu-id="a9a99-143">If your company doesn’t know hello answer for this question, review hello section “Permissions for password synchronization” in hello article [Install hello Azure Active Directory Sync Service](https://msdn.microsoft.com/library/azure/dn757602.aspx#BKMK_CreateAnADAccountForTheSyncService) and determine if you already have an account with these permissions or if you need toocreate one.</span></span>
* <span data-ttu-id="a9a99-144">如果您有多重樹系同步處理是 hello 同步伺服器可以 tooget tooeach 樹系？</span><span class="sxs-lookup"><span data-stu-id="a9a99-144">If you have mutli-forest sync is hello sync server able tooget tooeach forest?</span></span>

> [!NOTE]
> <span data-ttu-id="a9a99-145">請確定每個答案 tootake 附註，並了解 hello 回應 hello 背後的基本原理。</span><span class="sxs-lookup"><span data-stu-id="a9a99-145">Make sure tootake notes of each answer and understand hello rationale behind hello answer.</span></span> <span data-ttu-id="a9a99-146">[判斷事件回應需求](active-directory-hybrid-identity-design-considerations-incident-response-requirements.md)將介紹可用 hello 選項。</span><span class="sxs-lookup"><span data-stu-id="a9a99-146">[Determine incident response requirements](active-directory-hybrid-identity-design-considerations-incident-response-requirements.md) will go over hello options available.</span></span> <span data-ttu-id="a9a99-147">回答這些問題之後，您就能選取最適合業務需求的選項。</span><span class="sxs-lookup"><span data-stu-id="a9a99-147">By having answered those questions you will select which option best suits your business needs.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="a9a99-148">後續步驟</span><span class="sxs-lookup"><span data-stu-id="a9a99-148">Next steps</span></span>
[<span data-ttu-id="a9a99-149">判斷多重要素驗證需求</span><span class="sxs-lookup"><span data-stu-id="a9a99-149">Determine multi-factor authentication requirements</span></span>](active-directory-hybrid-identity-design-considerations-multifactor-auth-requirements.md)

## <a name="see-also"></a><span data-ttu-id="a9a99-150">另請參閱</span><span class="sxs-lookup"><span data-stu-id="a9a99-150">See also</span></span>
[<span data-ttu-id="a9a99-151">設計考量概觀</span><span class="sxs-lookup"><span data-stu-id="a9a99-151">Design considerations overview</span></span>](active-directory-hybrid-identity-design-considerations-overview.md)

