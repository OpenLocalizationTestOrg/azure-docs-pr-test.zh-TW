---
title: "Azure Active Directory 混合式身分識別設計考量 - 判斷目錄同步處理需求|Microsoft Docs"
description: "識別哪些是企業在內部部署和雲端之間同步處理所有使用者所需的需求。"
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
ms.openlocfilehash: 5ef87e606f055359ca325befd6048353ce57ca2b
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="determine-directory-synchronization-requirements"></a><span data-ttu-id="56d54-103">判斷目錄同步處理需求</span><span class="sxs-lookup"><span data-stu-id="56d54-103">Determine directory synchronization requirements</span></span>
<span data-ttu-id="56d54-104">同步處理的重點是根據使用者的內部部署身分識別，為他們提供雲端中的身分識別。</span><span class="sxs-lookup"><span data-stu-id="56d54-104">Synchronization is all about providing users an identity in the cloud based on their on-premises identity.</span></span> <span data-ttu-id="56d54-105">不論使用者是否將使用同步處理的帳戶來進行驗證或同盟驗證，他們仍然需要在雲端中具備身分識別。</span><span class="sxs-lookup"><span data-stu-id="56d54-105">Whether or not they will use synchronized account for authentication or federated authentication, the users will still need to have an identity in the cloud.</span></span>  <span data-ttu-id="56d54-106">這個身分識別必須定期維護和更新。</span><span class="sxs-lookup"><span data-stu-id="56d54-106">This identity will need to be maintained and updated periodically.</span></span>  <span data-ttu-id="56d54-107">更新可以有許多形式，範圍可從標題變更到密碼變更。</span><span class="sxs-lookup"><span data-stu-id="56d54-107">The updates can take many forms, from title changes to password changes.</span></span>  

<span data-ttu-id="56d54-108">一開始，先評估組織的內部部署身分識別解決方案和使用者需求。</span><span class="sxs-lookup"><span data-stu-id="56d54-108">Start by evaluating the organizations on-premises identity solution and user requirements.</span></span> <span data-ttu-id="56d54-109">當您定義如何在雲端中建立與維護使用者身分識別的技術需求時，這項評估非常重要。</span><span class="sxs-lookup"><span data-stu-id="56d54-109">This evaluation is important to define the technical requirements for how user identities will be created and maintained in the cloud.</span></span>  <span data-ttu-id="56d54-110">對於大多數的組織，Active Directory 是內部部署，而且是從中同步處理使用者的內部部署目錄，不過，在某些情況下，這並非事實。</span><span class="sxs-lookup"><span data-stu-id="56d54-110">For a majority of organizations, Active Directory is on-premises and will be the on-premises directory that users will by synchronized from, however in some cases this will not be the case.</span></span>  

<span data-ttu-id="56d54-111">請確實回答下列問題：</span><span class="sxs-lookup"><span data-stu-id="56d54-111">Make sure to answer the following questions:</span></span>

* <span data-ttu-id="56d54-112">您擁有一或多個 AD 樹系，或者完全沒有嗎？</span><span class="sxs-lookup"><span data-stu-id="56d54-112">Do you have one AD forest, multiple, or none?</span></span>
  
  * <span data-ttu-id="56d54-113">您要進行同步處理的 Azure AD 目錄有多少個？</span><span class="sxs-lookup"><span data-stu-id="56d54-113">How many Azure AD directories will you be synchronizing to?</span></span>
    
    1. <span data-ttu-id="56d54-114">您會使用篩選嗎？</span><span class="sxs-lookup"><span data-stu-id="56d54-114">Are you using filtering?</span></span>
    2. <span data-ttu-id="56d54-115">您是否規劃了多部 Azure AD Connect 伺服器？</span><span class="sxs-lookup"><span data-stu-id="56d54-115">Do you have multiple Azure AD Connect servers planned?</span></span>
* <span data-ttu-id="56d54-116">您目前沒有內部部署的同步處理工具嗎？</span><span class="sxs-lookup"><span data-stu-id="56d54-116">Do you currently have a synchronization tool on-premises?</span></span>
  
  * <span data-ttu-id="56d54-117">如果是，您的使用者是否具有虛擬目錄/身分識別整合？</span><span class="sxs-lookup"><span data-stu-id="56d54-117">If yes, does your users if users have a virtual directory/integration of identities?</span></span>
* <span data-ttu-id="56d54-118">您擁有任何其他您想要同步處理的內部部署目錄 (例如，LDAP 目錄、HR 資料庫等) 嗎？</span><span class="sxs-lookup"><span data-stu-id="56d54-118">Do you have any other directory on-premises that you want to synchronize (e.g. LDAP Directory, HR database, etc)?</span></span>
  * <span data-ttu-id="56d54-119">您將會進行任何 GALSync 嗎？</span><span class="sxs-lookup"><span data-stu-id="56d54-119">Are you going to be doing any GALSync?</span></span>
  * <span data-ttu-id="56d54-120">在您的組織中，UPN 的目前狀態為何？</span><span class="sxs-lookup"><span data-stu-id="56d54-120">What is the current state of UPNs in your organization?</span></span> 
  * <span data-ttu-id="56d54-121">您擁有使用者要對其進行驗證的其他目錄嗎？</span><span class="sxs-lookup"><span data-stu-id="56d54-121">Do you have a different directory that users authenticate against?</span></span>
  * <span data-ttu-id="56d54-122">貴公司是否使用 Microsoft Exchange？</span><span class="sxs-lookup"><span data-stu-id="56d54-122">Does your company use Microsoft Exchange?</span></span>
    * <span data-ttu-id="56d54-123">他們是否規劃擁有混合式交換部署？</span><span class="sxs-lookup"><span data-stu-id="56d54-123">Do they plan of having a hybrid exchange deployment?</span></span>

<span data-ttu-id="56d54-124">您已經了解同步處理需求，現在您必須判斷哪一個工具符合這些需求。</span><span class="sxs-lookup"><span data-stu-id="56d54-124">Now that you have an idea about your synchronization requirements, you need to determine which tool is the correct one to meet these requirements.</span></span>  <span data-ttu-id="56d54-125">Microsoft 提供您數個工具完成目錄整合與同步處理。</span><span class="sxs-lookup"><span data-stu-id="56d54-125">Microsoft provides several tools to accomplish directory integration and synchronization.</span></span>  <span data-ttu-id="56d54-126">詳細資訊請參閱 [混合式身分識別目錄整合工具比較表](active-directory-hybrid-identity-design-considerations-tools-comparison.md) 。</span><span class="sxs-lookup"><span data-stu-id="56d54-126">See the [Hybrid Identity directory integration tools comparison table](active-directory-hybrid-identity-design-considerations-tools-comparison.md) for more information.</span></span> 

<span data-ttu-id="56d54-127">您為貴公司備妥執行此工作所需的同步處理需求項目與工具，您現在需要評估使用這些目錄服務的應用程式。</span><span class="sxs-lookup"><span data-stu-id="56d54-127">Now that you have your synchronization requirements and the tool that will accomplish this for your company, you need to evaluate the applications that use these directory services.</span></span> <span data-ttu-id="56d54-128">當您定義如何將這些應用程式整合到雲端的技術需求時，這項評估非常重要。</span><span class="sxs-lookup"><span data-stu-id="56d54-128">This evaluation is important to define the technical requirements to integrate these applications to the cloud.</span></span> <span data-ttu-id="56d54-129">請確實回答下列問題：</span><span class="sxs-lookup"><span data-stu-id="56d54-129">Make sure to answer the following questions:</span></span>

* <span data-ttu-id="56d54-130">這些應用程式將移至雲端並使用目錄嗎？</span><span class="sxs-lookup"><span data-stu-id="56d54-130">Will these applications be moved to the cloud and use the directory?</span></span>
* <span data-ttu-id="56d54-131">有任何需要同步處理到雲端的特殊屬性，讓這些應用程式可成功使用它們嗎？</span><span class="sxs-lookup"><span data-stu-id="56d54-131">Are there special attributes that need to be synchronized to the cloud so these applications can use them successfully?</span></span>
* <span data-ttu-id="56d54-132">這些應用程式將需要重新撰寫，以充分利用雲端驗證嗎？</span><span class="sxs-lookup"><span data-stu-id="56d54-132">Will these applications need to be re-written to take advantage of cloud auth?</span></span>
* <span data-ttu-id="56d54-133">當使用者使用雲端身分識別來存取這些應用程式時，它們將持續存留在內部部署中嗎？</span><span class="sxs-lookup"><span data-stu-id="56d54-133">Will these applications continue to live on-premises while users access them using the cloud identity?</span></span>

<span data-ttu-id="56d54-134">您也需要判斷目錄同步作業的安全性需求和限制。</span><span class="sxs-lookup"><span data-stu-id="56d54-134">You also need to determine the security requirements and constraints directory synchronization.</span></span> <span data-ttu-id="56d54-135">當您取得所需的需求清單以便在雲端中建立和維護使用者的身分識別時，這項評估非常重要。</span><span class="sxs-lookup"><span data-stu-id="56d54-135">This evaluation is important to get a list of the requirements that will be needed in order to create and maintain user’s identities in the cloud.</span></span> <span data-ttu-id="56d54-136">請確實回答下列問題：</span><span class="sxs-lookup"><span data-stu-id="56d54-136">Make sure to answer the following questions:</span></span>

* <span data-ttu-id="56d54-137">同步處理伺服器將位於何處？</span><span class="sxs-lookup"><span data-stu-id="56d54-137">Where will the synchronization server be located?</span></span>
* <span data-ttu-id="56d54-138">它將會加入網域嗎？</span><span class="sxs-lookup"><span data-stu-id="56d54-138">Will it be domain joined?</span></span>
* <span data-ttu-id="56d54-139">伺服器將位於防火牆後面 (例如 DMZ) 限制的網路上嗎？</span><span class="sxs-lookup"><span data-stu-id="56d54-139">Will the server be located on a restricted network behind a firewall, such as a DMZ?</span></span>
  * <span data-ttu-id="56d54-140">您能夠開啟所需的防火牆連接埠來支援同步處理嗎？</span><span class="sxs-lookup"><span data-stu-id="56d54-140">Will you be able to open the required firewall ports to support synchronization?</span></span>
* <span data-ttu-id="56d54-141">您有任何適用於同步處理伺服器的災害復原計畫嗎？</span><span class="sxs-lookup"><span data-stu-id="56d54-141">Do you have a disaster recovery plan for the synchronization server?</span></span>
* <span data-ttu-id="56d54-142">針對您想要同步處理的所有樹系，您是否擁有具備正確權限的帳戶？</span><span class="sxs-lookup"><span data-stu-id="56d54-142">Do you have an account with the correct permissions for all forests you want to synch with?</span></span>
  * <span data-ttu-id="56d54-143">如果貴公司不知道這個問題的解答，請檢閱 [安裝 Azure Active Directory 同步處理服務](https://msdn.microsoft.com/library/azure/dn757602.aspx#BKMK_CreateAnADAccountForTheSyncService) 一文中的＜密碼同步化的權限 ＞一節，並判斷您是否已經擁有具備這些權限的帳戶，或者您是否需要建立一個帳戶。</span><span class="sxs-lookup"><span data-stu-id="56d54-143">If your company doesn’t know the answer for this question, review the section “Permissions for password synchronization” in the article [Install the Azure Active Directory Sync Service](https://msdn.microsoft.com/library/azure/dn757602.aspx#BKMK_CreateAnADAccountForTheSyncService) and determine if you already have an account with these permissions or if you need to create one.</span></span>
* <span data-ttu-id="56d54-144">如果您擁有多重樹系的同步處理，則同步處理伺服器能夠送達每個樹系嗎？</span><span class="sxs-lookup"><span data-stu-id="56d54-144">If you have mutli-forest sync is the sync server able to get to each forest?</span></span>

> [!NOTE]
> <span data-ttu-id="56d54-145">請確定會記下每個答案，並了解答案背後的原理。</span><span class="sxs-lookup"><span data-stu-id="56d54-145">Make sure to take notes of each answer and understand the rationale behind the answer.</span></span> <span data-ttu-id="56d54-146">[判斷事件因應需求](active-directory-hybrid-identity-design-considerations-incident-response-requirements.md) 將介紹可用的選項。</span><span class="sxs-lookup"><span data-stu-id="56d54-146">[Determine incident response requirements](active-directory-hybrid-identity-design-considerations-incident-response-requirements.md) will go over the options available.</span></span> <span data-ttu-id="56d54-147">回答這些問題之後，您就能選取最適合業務需求的選項。</span><span class="sxs-lookup"><span data-stu-id="56d54-147">By having answered those questions you will select which option best suits your business needs.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="56d54-148">後續步驟</span><span class="sxs-lookup"><span data-stu-id="56d54-148">Next steps</span></span>
[<span data-ttu-id="56d54-149">判斷多重要素驗證需求</span><span class="sxs-lookup"><span data-stu-id="56d54-149">Determine multi-factor authentication requirements</span></span>](active-directory-hybrid-identity-design-considerations-multifactor-auth-requirements.md)

## <a name="see-also"></a><span data-ttu-id="56d54-150">另請參閱</span><span class="sxs-lookup"><span data-stu-id="56d54-150">See also</span></span>
[<span data-ttu-id="56d54-151">設計考量概觀</span><span class="sxs-lookup"><span data-stu-id="56d54-151">Design considerations overview</span></span>](active-directory-hybrid-identity-design-considerations-overview.md)

