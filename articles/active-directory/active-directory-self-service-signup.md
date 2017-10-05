---
title: "什麼是 Azure 的自助式註冊？ | Microsoft Docs"
description: "Azure 的自助式註冊、如何管理註冊程序及如何接管 DNS 網域名稱的概觀。"
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: b9f01876-29d1-4ab8-8b74-04d43d532f4b
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 05/08/2017
ms.author: curtand
ms.openlocfilehash: de8b55516ae7e19f2b42466fa4dc387b82495a5b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="what-is-self-service-signup-for-azure"></a><span data-ttu-id="1b4ea-104">什麼是 Azure 的自助式註冊？</span><span class="sxs-lookup"><span data-stu-id="1b4ea-104">What is Self-Service Signup for Azure?</span></span>
<span data-ttu-id="1b4ea-105">本主題說明自助式註冊程序及如何接管 DNS 網域名稱。</span><span class="sxs-lookup"><span data-stu-id="1b4ea-105">This topic explains the self-service signup process and how to take over a DNS domain name.</span></span>  

## <a name="why-use-self-service-signup"></a><span data-ttu-id="1b4ea-106">為何使用自助式註冊？</span><span class="sxs-lookup"><span data-stu-id="1b4ea-106">Why use self-service signup?</span></span>
* <span data-ttu-id="1b4ea-107">讓客戶更快取得他們想要的服務。</span><span class="sxs-lookup"><span data-stu-id="1b4ea-107">Get customers to services they want faster.</span></span>
* <span data-ttu-id="1b4ea-108">建立服務的電子郵件型供應項目。</span><span class="sxs-lookup"><span data-stu-id="1b4ea-108">Create email-based offers for a service.</span></span>
* <span data-ttu-id="1b4ea-109">建立以電子郵件為基礎的註冊流程，讓使用者使用其易記的工作電子郵件別名快速地建立身分識別。</span><span class="sxs-lookup"><span data-stu-id="1b4ea-109">Create email-based signup flows which quickly allow users to create identities using their easy-to-remember work email aliases.</span></span>
* <span data-ttu-id="1b4ea-110">未受管理的 Azure 目錄後來可以轉換成受管理的目錄，並重複用於其他服務。</span><span class="sxs-lookup"><span data-stu-id="1b4ea-110">Unmanaged Azure directories can be made into managed directories later and be reused for other services.</span></span>

## <a name="terms-and-definitions"></a><span data-ttu-id="1b4ea-111">詞彙和定義</span><span class="sxs-lookup"><span data-stu-id="1b4ea-111">Terms and Definitions</span></span>
* <span data-ttu-id="1b4ea-112">**自助式註冊**：這是使用者用以註冊雲端服務的方法，系統會根據其電子郵件網域在 Azure Active Directory (Azure AD) 中自動建立身分識別。</span><span class="sxs-lookup"><span data-stu-id="1b4ea-112">**Self-service sign up**: This is the method by which a user signs up for a cloud service and has an identity automatically created for them in Azure Active Directory (Azure AD) based on their email domain.</span></span>
* <span data-ttu-id="1b4ea-113">**未受管理的 Azure 目錄**：這是建立身分識別的目錄。</span><span class="sxs-lookup"><span data-stu-id="1b4ea-113">**Unmanaged Azure directory**: This is the directory where that identity is created.</span></span> <span data-ttu-id="1b4ea-114">未受管理的目錄是沒有全域管理員的目錄。</span><span class="sxs-lookup"><span data-stu-id="1b4ea-114">An unmanaged directory is a directory that has no global administrator.</span></span>
* <span data-ttu-id="1b4ea-115">**電子郵件驗證的使用者**：這是 Azure AD 中的使用者帳戶類型。</span><span class="sxs-lookup"><span data-stu-id="1b4ea-115">**Email-verified user**: This is a type of user account in Azure AD.</span></span> <span data-ttu-id="1b4ea-116">在註冊自助式供應項目後自動建立身分識別的使用者，就是所謂的電子郵件驗證的使用者。</span><span class="sxs-lookup"><span data-stu-id="1b4ea-116">A user who has an identity created automatically after signing up for a self-service offer is known as an email-verified user.</span></span> <span data-ttu-id="1b4ea-117">電子郵件驗證的使用者是加上 creationmethod=EmailVerified 標記之目錄的一般成員。</span><span class="sxs-lookup"><span data-stu-id="1b4ea-117">An email-verified user is a regular member of a directory tagged with creationmethod=EmailVerified.</span></span>

## <a name="user-experience"></a><span data-ttu-id="1b4ea-118">使用者體驗</span><span class="sxs-lookup"><span data-stu-id="1b4ea-118">User experience</span></span>
<span data-ttu-id="1b4ea-119">例如，假設電子郵件為 Dan@BellowsCollege.com 的使用者會透過電子郵件接收機密檔案。</span><span class="sxs-lookup"><span data-stu-id="1b4ea-119">For example, let's say a user whose email is Dan@BellowsCollege.com receives sensitive files via email.</span></span> <span data-ttu-id="1b4ea-120">檔案已受 Azure 版權管理 (Azure RMS) 保護。</span><span class="sxs-lookup"><span data-stu-id="1b4ea-120">The files have been protected by Azure Rights Management (Azure RMS).</span></span> <span data-ttu-id="1b4ea-121">但是 Dan 的組織 (Bellows College) 尚未註冊 Azure RMS，也未部署 Active Directory RMS。</span><span class="sxs-lookup"><span data-stu-id="1b4ea-121">But Dan's organization, Bellows College, has not signed up for Azure RMS, nor has it deployed Active Directory RMS.</span></span> <span data-ttu-id="1b4ea-122">在此情況下，Dan 可以註冊個人版 RMS 的免費訂閱，以便讀取受保護的檔案。</span><span class="sxs-lookup"><span data-stu-id="1b4ea-122">In this case, Dan can sign up for a free subscription to RMS for individuals in order to read the protected files.</span></span>

<span data-ttu-id="1b4ea-123">如果 Dan 是第一個使用 BellowsCollege.com 的電子郵件地址註冊此自助式供應項目的使用者，則 Azure AD 中會針對 BellowsCollege.com 建立未受管理的目錄。</span><span class="sxs-lookup"><span data-stu-id="1b4ea-123">If Dan is the first user with an email address from BellowsCollege.com to sign up for this self-service offering, then an unmanaged directory will be created for BellowsCollege.com in Azure AD.</span></span> <span data-ttu-id="1b4ea-124">如果來自 BellowsCollege.com 網域的其他使用者註冊此供應項目或類似的自助式供應項目，則在 Azure 中相同的未受管理目錄中，也會為他們建立經過電子郵件驗證的使用者帳戶。</span><span class="sxs-lookup"><span data-stu-id="1b4ea-124">If other users from the BellowsCollege.com domain sign up for this offering or a similar self-service offering, they will also have email-verified user accounts created in the same unmanaged directory in Azure.</span></span>

## <a name="admin-experience"></a><span data-ttu-id="1b4ea-125">管理員體驗</span><span class="sxs-lookup"><span data-stu-id="1b4ea-125">Admin experience</span></span>
<span data-ttu-id="1b4ea-126">擁有未受管理 Azure 目錄之 DNS 網域名稱的管理員，可以在證明擁有權後接管或合併目錄。</span><span class="sxs-lookup"><span data-stu-id="1b4ea-126">An admin who owns the DNS domain name of an unmanaged Azure directory can take over or merge the directory after proving ownership.</span></span> <span data-ttu-id="1b4ea-127">下一節會更詳細地說明管理員體驗，但其摘要如下：</span><span class="sxs-lookup"><span data-stu-id="1b4ea-127">The next sections explain the admin experience in more detail, but here's a summary:</span></span>

* <span data-ttu-id="1b4ea-128">當您接管未受管理的 Azure 目錄時，您就直接變成未受管理目錄的全域管理員。</span><span class="sxs-lookup"><span data-stu-id="1b4ea-128">When you take over an unmanaged Azure directory, you simply become the global administrator of the unmanaged directory.</span></span> <span data-ttu-id="1b4ea-129">這有時候稱為內部接管。</span><span class="sxs-lookup"><span data-stu-id="1b4ea-129">This is sometimes called an internal takeover.</span></span>
* <span data-ttu-id="1b4ea-130">當您合併未受管理的 Azure 目錄時，您會將未受管理目錄的 DNS 網域名稱新增至受管理的 Azure 目錄，而且系統會建立使用者與資源的對應，以便使用者繼續存取服務而不中斷。</span><span class="sxs-lookup"><span data-stu-id="1b4ea-130">When you merge an unmanaged Azure directory, you add the DNS domain name of the unmanaged directory to your managed Azure directory and a mapping of users-to-resources is created so users can continue to access services without interruption.</span></span> <span data-ttu-id="1b4ea-131">這有時候稱為外部接管。</span><span class="sxs-lookup"><span data-stu-id="1b4ea-131">This is sometimes called an external takeover.</span></span>

## <a name="what-gets-created-in-azure-active-directory"></a><span data-ttu-id="1b4ea-132">Azure Active Directory 中建立的項目為何？</span><span class="sxs-lookup"><span data-stu-id="1b4ea-132">What gets created in Azure Active Directory?</span></span>
#### <a name="directory"></a><span data-ttu-id="1b4ea-133">目錄</span><span class="sxs-lookup"><span data-stu-id="1b4ea-133">directory</span></span>
* <span data-ttu-id="1b4ea-134">建立網域的 Azure Active Directory 目錄 (每個網域一個目錄)。</span><span class="sxs-lookup"><span data-stu-id="1b4ea-134">An Azure Active Directory directory for the domain is created, one directory per domain.</span></span>
* <span data-ttu-id="1b4ea-135">Azure AD 目錄沒有全域管理員。</span><span class="sxs-lookup"><span data-stu-id="1b4ea-135">The Azure AD directory has no global admin.</span></span>

#### <a name="users"></a><span data-ttu-id="1b4ea-136">使用者</span><span class="sxs-lookup"><span data-stu-id="1b4ea-136">Users</span></span>
* <span data-ttu-id="1b4ea-137">針對註冊的每位使用者，Azure AD 目錄中會建立使用者物件。</span><span class="sxs-lookup"><span data-stu-id="1b4ea-137">For each user who signs up, a user object is created in the Azure AD directory.</span></span>
* <span data-ttu-id="1b4ea-138">每個使用者物件都標示為外部。</span><span class="sxs-lookup"><span data-stu-id="1b4ea-138">Each user object is marked as external.</span></span>
* <span data-ttu-id="1b4ea-139">每位使用者都獲權存取他們註冊的服務。</span><span class="sxs-lookup"><span data-stu-id="1b4ea-139">Each user is given access to the service that they signed up for.</span></span>

### <a name="how-do-i-claim-a-self-service-azure-ad-directory-for-a-domain-i-own"></a><span data-ttu-id="1b4ea-140">如何針對我擁有的網域宣告自助式 Azure AD 目錄？</span><span class="sxs-lookup"><span data-stu-id="1b4ea-140">How do I claim a self-service Azure AD directory for a domain I own?</span></span>
<span data-ttu-id="1b4ea-141">您可以執行網域驗證來宣告自助式 Azure AD 目錄。</span><span class="sxs-lookup"><span data-stu-id="1b4ea-141">You can claim a self-service Azure AD directory by performing domain validation.</span></span> <span data-ttu-id="1b4ea-142">網域驗證會藉由建立 DNS 記錄來證明您擁有該網域。</span><span class="sxs-lookup"><span data-stu-id="1b4ea-142">Domain validation proves you own the domain by creating DNS records.</span></span>

<span data-ttu-id="1b4ea-143">有兩種方式可進行 Azure AD 目錄的 DNS 接管：</span><span class="sxs-lookup"><span data-stu-id="1b4ea-143">There are two ways to do a DNS takeover of an Azure AD directory:</span></span>

* <span data-ttu-id="1b4ea-144">內部接管 (管理員會探索未受管理的 Azure 目錄，並且想要轉換成受管理的目錄)</span><span class="sxs-lookup"><span data-stu-id="1b4ea-144">internal takeover (Admin discovers an unmanaged Azure directory, and wants to turn into a managed directory)</span></span>
* <span data-ttu-id="1b4ea-145">外部接管 (管理員會嘗試將新的網域新增至他們管理的 Azure 目錄)</span><span class="sxs-lookup"><span data-stu-id="1b4ea-145">external takeover (Admin tries to add a new domain to their managed Azure directory)</span></span>

<span data-ttu-id="1b4ea-146">如果您在使用者執行自助式註冊後接管未受管理的目錄，或正在將新網域加入至現有的受管理目錄，您可能會想要驗證您擁有網域。</span><span class="sxs-lookup"><span data-stu-id="1b4ea-146">You might be interested in validating that you own a domain because you are taking over an unmanaged directory after a user performed self-service signup, or you might be adding a new domain to an existing managed directory.</span></span> <span data-ttu-id="1b4ea-147">例如，您擁有名為 contoso.com 的網域，而您想要加入名為 contoso.co.uk 或 contoso.uk 的新網域。</span><span class="sxs-lookup"><span data-stu-id="1b4ea-147">For example, you have a domain named contoso.com and you want to add a new domain named contoso.co.uk or contoso.uk.</span></span>

## <a name="what-is-domain-takeover"></a><span data-ttu-id="1b4ea-148">什麼是網域接管？</span><span class="sxs-lookup"><span data-stu-id="1b4ea-148">What is domain takeover?</span></span>
<span data-ttu-id="1b4ea-149">本節說明如何驗證您擁有的網域。</span><span class="sxs-lookup"><span data-stu-id="1b4ea-149">This section covers how to validate that you own a domain</span></span>

### <a name="what-is-domain-validation-and-why-is-it-used"></a><span data-ttu-id="1b4ea-150">什麼是網域驗證，以及為何使用？</span><span class="sxs-lookup"><span data-stu-id="1b4ea-150">What is domain validation and why is it used?</span></span>
<span data-ttu-id="1b4ea-151">為了在目錄上執行作業，Azure AD 會要求您驗證 DNS 網域的擁有權。</span><span class="sxs-lookup"><span data-stu-id="1b4ea-151">In order to perform operations on a directory, Azure AD requires that you validate ownership of the DNS domain.</span></span>  <span data-ttu-id="1b4ea-152">網域驗證可讓您宣告目錄，並且將自助式目錄提升為受管理的目錄，或將自助式目錄合併到現有的受管理目錄。</span><span class="sxs-lookup"><span data-stu-id="1b4ea-152">Validation of the domain allows you to claim the directory and either promote the self-service directory to a managed directory, or merge the self-service directory into an existing managed directory.</span></span>

## <a name="examples-of-domain-validation"></a><span data-ttu-id="1b4ea-153">網域驗證範例</span><span class="sxs-lookup"><span data-stu-id="1b4ea-153">Examples of domain validation</span></span>
<span data-ttu-id="1b4ea-154">有兩種方式可進行目錄的 DNS 接管：</span><span class="sxs-lookup"><span data-stu-id="1b4ea-154">There are two ways to do a DNS takeover of a directory:</span></span>

* <span data-ttu-id="1b4ea-155">內部接管 (例如，系統管理員會探索未受管理的自助式目錄，並且想要轉換成受管理的目錄)</span><span class="sxs-lookup"><span data-stu-id="1b4ea-155">internal takeover  (For example, an admin discovers a self-service, unmanaged directory, and wants to turn into managed directory)</span></span>
* <span data-ttu-id="1b4ea-156">外部接管 (例如，管理員會嘗試將新的網域新增至受管理的目錄)</span><span class="sxs-lookup"><span data-stu-id="1b4ea-156">external takeover (For example, a admin tries to add a new domain to a managed directory)</span></span>

### <a name="internal-takeover---promote-a-self-service-unmanaged-directory-to-be-a-managed-directory"></a><span data-ttu-id="1b4ea-157">內部接管 - 將未受管理的自助式目錄提升為受管理的目錄</span><span class="sxs-lookup"><span data-stu-id="1b4ea-157">Internal Takeover - promote a self-service, unmanaged directory to be a managed directory</span></span>
<span data-ttu-id="1b4ea-158">當您執行內部接管時，目錄會從未受管理的目錄轉換為受管理的目錄。</span><span class="sxs-lookup"><span data-stu-id="1b4ea-158">When you do internal takeover, the directory gets converted from an unmanaged directory to a managed directory.</span></span> <span data-ttu-id="1b4ea-159">您需要完成 DNS 網域名稱驗證，驗證時您會在 DNS 區域中建立 MX 記錄或 TXT 記錄。</span><span class="sxs-lookup"><span data-stu-id="1b4ea-159">You need to complete DNS domain name validation, where you create an MX record or a TXT record in the DNS zone.</span></span> <span data-ttu-id="1b4ea-160">該動作：</span><span class="sxs-lookup"><span data-stu-id="1b4ea-160">That action:</span></span>

* <span data-ttu-id="1b4ea-161">驗證您是否擁有此網域</span><span class="sxs-lookup"><span data-stu-id="1b4ea-161">Validates that you own the domain</span></span>
* <span data-ttu-id="1b4ea-162">將目錄變成受管理</span><span class="sxs-lookup"><span data-stu-id="1b4ea-162">Makes the directory managed</span></span>
* <span data-ttu-id="1b4ea-163">讓您成為目錄的全域管理員</span><span class="sxs-lookup"><span data-stu-id="1b4ea-163">Makes you the global admin of the directory</span></span>

<span data-ttu-id="1b4ea-164">假設 Bellows College 的 IT 管理員發現學校的使用者已註冊自助式供應項目。</span><span class="sxs-lookup"><span data-stu-id="1b4ea-164">Let's say an IT administrator from Bellows College discovers that users from the school have signed up for self-service offerings.</span></span> <span data-ttu-id="1b4ea-165">身為 DNS 名稱 BellowsCollege.com 的註冊擁有者，IT 管理員可以在 Azure 中驗證 DNS 名稱的擁有權，然後接管未受管理的目錄。</span><span class="sxs-lookup"><span data-stu-id="1b4ea-165">As the registered owner of the DNS name BellowsCollege.com, the IT administrator can validate ownership of the DNS name in Azure and then take over the unmanaged directory.</span></span> <span data-ttu-id="1b4ea-166">目錄接著會變成受管理的目錄，而 IT 管理員會被指派 BellowsCollege.com 目錄的全域管理員角色。</span><span class="sxs-lookup"><span data-stu-id="1b4ea-166">The directory then becomes a managed directory, and the IT administrator is assigned the global administrator role for the BellowsCollege.com directory.</span></span>

### <a name="external-takeover---merge-a-self-service-directory-into-an-existing-managed-directory"></a><span data-ttu-id="1b4ea-167">外部接管 - 將自助式目錄合併到現有的受管理目錄</span><span class="sxs-lookup"><span data-stu-id="1b4ea-167">External Takeover - merge a self-service directory into an existing managed directory</span></span>
<span data-ttu-id="1b4ea-168">在外部接管中，您已有受管理的目錄，而您希望來自未受管理目錄的所有使用者和群組都加入該受管理的目錄，而非擁有兩個不同的目錄。</span><span class="sxs-lookup"><span data-stu-id="1b4ea-168">In an external takeover, you already have a managed directory and you want all users and groups from an unmanaged directory to join that managed directory, rather than own two separate directories.</span></span>

<span data-ttu-id="1b4ea-169">身為受管理目錄的管理員，您新增網域，而該網域剛好有一個相關聯的未受管理目錄。</span><span class="sxs-lookup"><span data-stu-id="1b4ea-169">As an admin of a managed directory, you add a domain, and that domain happens to have an unmanaged directory associated with it.</span></span>

<span data-ttu-id="1b4ea-170">例如，假設您是 IT 管理員，而且已有 Contoso.com (您的組織註冊的網域名稱) 的受管理目錄。</span><span class="sxs-lookup"><span data-stu-id="1b4ea-170">For example, let's say you are an IT administrator and you already have a managed directory for Contoso.com, a domain name that is registered to your organization.</span></span> <span data-ttu-id="1b4ea-171">您會發現貴組織的使用者已使用電子郵件網域名稱 user@contoso.co.uk (這是貴組織擁有的另一個網域名稱) 以自助方式註冊產品方案。</span><span class="sxs-lookup"><span data-stu-id="1b4ea-171">You discover that users from your organization have performed self-service sign up for an offering by using email domain name user@contoso.co.uk, which is another domain name that your organization owns.</span></span> <span data-ttu-id="1b4ea-172">這些使用者目前在 contoso.co.uk 的未受管理目錄中有帳戶。</span><span class="sxs-lookup"><span data-stu-id="1b4ea-172">Those users currently have accounts in an unmanaged directory for contoso.co.uk.</span></span>

<span data-ttu-id="1b4ea-173">您不想管理兩個不同的目錄，所以將 contoso.co.uk 的未受管理目錄合併到 contoso.com 的現有 IT 受管理目錄。</span><span class="sxs-lookup"><span data-stu-id="1b4ea-173">You don't want to manage two separate directories, so you merge the unmanaged directory for contoso.co.uk into your existing IT managed directory for contoso.com.</span></span>

<span data-ttu-id="1b4ea-174">外部接管會遵循與內部接管相同的 DNS 驗證程序。</span><span class="sxs-lookup"><span data-stu-id="1b4ea-174">External takeover follows the same DNS validation process as internal takeover.</span></span>  <span data-ttu-id="1b4ea-175">差異是：使用者和服務會重新對應至 IT 受管理的目錄。</span><span class="sxs-lookup"><span data-stu-id="1b4ea-175">Difference being: users and services are remapped to the IT managed directory.</span></span>

#### <a name="whats-the-impact-of-performing-an-external-takeover"></a><span data-ttu-id="1b4ea-176">執行外部接管的影響為何？</span><span class="sxs-lookup"><span data-stu-id="1b4ea-176">What's the impact of performing an external takeover?</span></span>
<span data-ttu-id="1b4ea-177">外部接管時會建立使用者與資源的對應，以便使用者繼續存取服務而不中斷。</span><span class="sxs-lookup"><span data-stu-id="1b4ea-177">With an external takeover, a mapping of users-to-resources is created so users can continue to access services without interruption.</span></span> <span data-ttu-id="1b4ea-178">許多應用程式 (包括個人的 RMS) 會妥善處理使用者與資源的對應，而使用者不需變更即可繼續存取這些服務。</span><span class="sxs-lookup"><span data-stu-id="1b4ea-178">Many applications, including RMS for individuals, handle the mapping of users-to-resources well, and users can continue to access those services without change.</span></span> <span data-ttu-id="1b4ea-179">如果應用程式未有效地處理使用者與資源的對應，外部接管可能會明確遭到封鎖，以免使用者發生不佳的體驗。</span><span class="sxs-lookup"><span data-stu-id="1b4ea-179">If an application does not handle the mapping of users-to-resources effectively, external takeover may be explicitly blocked to prevent users from a poor experience.</span></span>

#### <a name="directory-takeover-support-by-service"></a><span data-ttu-id="1b4ea-180">服務支援的目錄接管</span><span class="sxs-lookup"><span data-stu-id="1b4ea-180">directory takeover support by service</span></span>
<span data-ttu-id="1b4ea-181">目前下列服務支援接管：</span><span class="sxs-lookup"><span data-stu-id="1b4ea-181">Currently the following services support takeover:</span></span>

* <span data-ttu-id="1b4ea-182">RMS</span><span class="sxs-lookup"><span data-stu-id="1b4ea-182">RMS</span></span>

<span data-ttu-id="1b4ea-183">下列服務很快就會支援接管：</span><span class="sxs-lookup"><span data-stu-id="1b4ea-183">The following services will soon be supporting takeover:</span></span>

* <span data-ttu-id="1b4ea-184">PowerBI</span><span class="sxs-lookup"><span data-stu-id="1b4ea-184">PowerBI</span></span>

<span data-ttu-id="1b4ea-185">在外部接管之後，下列項目不需要管理員採取行動來移轉使用者資料。</span><span class="sxs-lookup"><span data-stu-id="1b4ea-185">The following do not and require additional admin action to migrate user data after an external takeover.</span></span>

* <span data-ttu-id="1b4ea-186">SharePoint/OneDrive</span><span class="sxs-lookup"><span data-stu-id="1b4ea-186">SharePoint/OneDrive</span></span>

## <a name="how-to-perform-a-dns-domain-name-takeover"></a><span data-ttu-id="1b4ea-187">如何執行 DNS 網域名稱接管</span><span class="sxs-lookup"><span data-stu-id="1b4ea-187">How to perform a DNS domain name takeover</span></span>
<span data-ttu-id="1b4ea-188">您有幾個選項可用來執行網域驗證 (如果您想要，可執行接管)：</span><span class="sxs-lookup"><span data-stu-id="1b4ea-188">You have a few options for how to perform a domain validation (and do a takeover if you wish):</span></span>

1. <span data-ttu-id="1b4ea-189">Azure 管理入口網站</span><span class="sxs-lookup"><span data-stu-id="1b4ea-189">Azure Management Portal</span></span>

   <span data-ttu-id="1b4ea-190">接管是由執行網域新增所觸發。</span><span class="sxs-lookup"><span data-stu-id="1b4ea-190">A takeover is triggered by doing a domain addition.</span></span>  <span data-ttu-id="1b4ea-191">如果網域已有目錄，您將可選擇執行外部接管。</span><span class="sxs-lookup"><span data-stu-id="1b4ea-191">If a directory already exists for the domain, you'll have the option to perform an external takeover.</span></span>

   <span data-ttu-id="1b4ea-192">使用您的認證登入 Azure 入口網站。</span><span class="sxs-lookup"><span data-stu-id="1b4ea-192">Sign in to the Azure portal using your credentials.</span></span>  <span data-ttu-id="1b4ea-193">瀏覽至現有的目錄，再瀏覽至 [加入網域] 。</span><span class="sxs-lookup"><span data-stu-id="1b4ea-193">Navigate to your existing directory and then to **Add domain**.</span></span>
2. <span data-ttu-id="1b4ea-194">Office 365</span><span class="sxs-lookup"><span data-stu-id="1b4ea-194">Office 365</span></span>

   <span data-ttu-id="1b4ea-195">您可以在 Office 365 中使用 [管理網域](https://support.office.com/article/Navigate-to-the-Office-365-Manage-domains-page-026af1f2-0e6d-4f2d-9b33-fd147420fac2/) 頁面上的選項來處理您的網域和 DNS 記錄。</span><span class="sxs-lookup"><span data-stu-id="1b4ea-195">You can use the options on the [Manage domains](https://support.office.com/article/Navigate-to-the-Office-365-Manage-domains-page-026af1f2-0e6d-4f2d-9b33-fd147420fac2/) page in Office 365 to work with your domains and DNS records.</span></span> <span data-ttu-id="1b4ea-196">請參閱 [在 Office 365 中驗證您的網域](https://support.office.com/article/Verify-your-domain-in-Office-365-6383f56d-3d09-4dcb-9b41-b5f5a5efd611/)。</span><span class="sxs-lookup"><span data-stu-id="1b4ea-196">See [Verify your domain in Office 365](https://support.office.com/article/Verify-your-domain-in-Office-365-6383f56d-3d09-4dcb-9b41-b5f5a5efd611/).</span></span>
3. <span data-ttu-id="1b4ea-197">Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="1b4ea-197">Windows PowerShell</span></span>

   <span data-ttu-id="1b4ea-198">下列步驟是使用 Windows PowerShell 執行驗證的必要步驟。</span><span class="sxs-lookup"><span data-stu-id="1b4ea-198">The following steps are required to perform a validation using Windows PowerShell.</span></span>

   | <span data-ttu-id="1b4ea-199">步驟</span><span class="sxs-lookup"><span data-stu-id="1b4ea-199">Step</span></span> | <span data-ttu-id="1b4ea-200">要使用的 Cmdlet</span><span class="sxs-lookup"><span data-stu-id="1b4ea-200">Cmdlet to use</span></span> |
   | --- | --- |
   | <span data-ttu-id="1b4ea-201">建立認證物件</span><span class="sxs-lookup"><span data-stu-id="1b4ea-201">Create a credential object</span></span> |<span data-ttu-id="1b4ea-202">Get-Credential</span><span class="sxs-lookup"><span data-stu-id="1b4ea-202">Get-Credential</span></span> |
   | <span data-ttu-id="1b4ea-203">連接至 Azure AD</span><span class="sxs-lookup"><span data-stu-id="1b4ea-203">Connect to Azure AD</span></span> |<span data-ttu-id="1b4ea-204">Connect-MsolService</span><span class="sxs-lookup"><span data-stu-id="1b4ea-204">Connect-MsolService</span></span> |
   | <span data-ttu-id="1b4ea-205">取得網域清單</span><span class="sxs-lookup"><span data-stu-id="1b4ea-205">get a list of domains</span></span> |<span data-ttu-id="1b4ea-206">Get-MsolDomain</span><span class="sxs-lookup"><span data-stu-id="1b4ea-206">Get-MsolDomain</span></span> |
   | <span data-ttu-id="1b4ea-207">建立挑戰</span><span class="sxs-lookup"><span data-stu-id="1b4ea-207">Create a challenge</span></span> |<span data-ttu-id="1b4ea-208">Get-MsolDomainVerificationDns</span><span class="sxs-lookup"><span data-stu-id="1b4ea-208">Get-MsolDomainVerificationDns</span></span> |
   | <span data-ttu-id="1b4ea-209">建立 DNS 記錄</span><span class="sxs-lookup"><span data-stu-id="1b4ea-209">Create DNS record</span></span> |<span data-ttu-id="1b4ea-210">在您的 DNS 伺服器上執行這項操作</span><span class="sxs-lookup"><span data-stu-id="1b4ea-210">Do this on your DNS server</span></span> |
   | <span data-ttu-id="1b4ea-211">驗證挑戰</span><span class="sxs-lookup"><span data-stu-id="1b4ea-211">Verify the challenge</span></span> |<span data-ttu-id="1b4ea-212">Confirm-MsolEmailVerifiedDomain</span><span class="sxs-lookup"><span data-stu-id="1b4ea-212">Confirm-MsolEmailVerifiedDomain</span></span> |

<span data-ttu-id="1b4ea-213">例如：</span><span class="sxs-lookup"><span data-stu-id="1b4ea-213">For example:</span></span>

1. <span data-ttu-id="1b4ea-214">使用用來回應自助式產品方案的認證來連接至 Azure AD：</span><span class="sxs-lookup"><span data-stu-id="1b4ea-214">Connect to Azure AD using the credentials that were used to respond to the self-service offering:</span></span>

        import-module MSOnline
        $msolcred = get-credential
        connect-msolservice -credential $msolcred
2. <span data-ttu-id="1b4ea-215">取得網域清單：</span><span class="sxs-lookup"><span data-stu-id="1b4ea-215">Get a list of domains:</span></span>

    <span data-ttu-id="1b4ea-216">Get-MsolDomain</span><span class="sxs-lookup"><span data-stu-id="1b4ea-216">Get-MsolDomain</span></span>
3. <span data-ttu-id="1b4ea-217">然後執行 Get-MsolDomainVerificationDns Cmdlet 來建立挑戰：</span><span class="sxs-lookup"><span data-stu-id="1b4ea-217">Then run the Get-MsolDomainVerificationDns cmdlet to create a challenge:</span></span>

    <span data-ttu-id="1b4ea-218">Get-MsolDomainVerificationDns –DomainName *your_domain_name* –Mode DnsTxtRecord</span><span class="sxs-lookup"><span data-stu-id="1b4ea-218">Get-MsolDomainVerificationDns –DomainName *your_domain_name* –Mode DnsTxtRecord</span></span>

    <span data-ttu-id="1b4ea-219">例如：</span><span class="sxs-lookup"><span data-stu-id="1b4ea-219">For example:</span></span>

    <span data-ttu-id="1b4ea-220">Get-MsolDomainVerificationDns –DomainName contoso.com –Mode DnsTxtRecord</span><span class="sxs-lookup"><span data-stu-id="1b4ea-220">Get-MsolDomainVerificationDns –DomainName contoso.com –Mode DnsTxtRecord</span></span>
4. <span data-ttu-id="1b4ea-221">複製從此命令傳回的值 (挑戰)。</span><span class="sxs-lookup"><span data-stu-id="1b4ea-221">Copy the value (the challenge) that is returned from this command.</span></span>

    <span data-ttu-id="1b4ea-222">例如：</span><span class="sxs-lookup"><span data-stu-id="1b4ea-222">For example:</span></span>

    <span data-ttu-id="1b4ea-223">MS=32DD01B82C05D27151EA9AE93C5890787F0E65D9</span><span class="sxs-lookup"><span data-stu-id="1b4ea-223">MS=32DD01B82C05D27151EA9AE93C5890787F0E65D9</span></span>
5. <span data-ttu-id="1b4ea-224">在公用 DNS 命名空間中，建立 DNS txt 記錄，其中包含您在上一個步驟中複製的值。</span><span class="sxs-lookup"><span data-stu-id="1b4ea-224">In your public DNS namespace, create a DNS txt record that contains the value that you copied in the previous step.</span></span>

    <span data-ttu-id="1b4ea-225">此記錄的名稱是父系網域的名稱，所以如果您使用 Windows Server 的 DNS 角色建立此資源記錄，請將記錄名稱空白，只要將此值貼入文字方塊即可。</span><span class="sxs-lookup"><span data-stu-id="1b4ea-225">The name for this record is the name of the parent domain, so if you create this resource record by using the DNS role from Windows Server, leave the Record name blank and just paste the value into the Text box</span></span>
6. <span data-ttu-id="1b4ea-226">執行 onfirm-MsolDomain Cmdlet 來驗證挑戰：</span><span class="sxs-lookup"><span data-stu-id="1b4ea-226">Run the Confirm-MsolDomain cmdlet to verify the challenge:</span></span>

    <span data-ttu-id="1b4ea-227">Confirm-MsolEmailVerifiedDomain -DomainName *your_domain_name*</span><span class="sxs-lookup"><span data-stu-id="1b4ea-227">Confirm-MsolEmailVerifiedDomain -DomainName *your_domain_name*</span></span>

    <span data-ttu-id="1b4ea-228">例如：</span><span class="sxs-lookup"><span data-stu-id="1b4ea-228">for example:</span></span>

    <span data-ttu-id="1b4ea-229">Confirm-MsolEmailVerifiedDomain -DomainName contoso.com</span><span class="sxs-lookup"><span data-stu-id="1b4ea-229">Confirm-MsolEmailVerifiedDomain -DomainName contoso.com</span></span>

<span data-ttu-id="1b4ea-230">成功挑戰會讓您回到提示，但不會產生錯誤。</span><span class="sxs-lookup"><span data-stu-id="1b4ea-230">A successful challenge returns you to the prompt without an error.</span></span>

## <a name="how-do-i-control-self-service-settings"></a><span data-ttu-id="1b4ea-231">如何控制自助式設定？</span><span class="sxs-lookup"><span data-stu-id="1b4ea-231">How do I control self-service settings?</span></span>
<span data-ttu-id="1b4ea-232">系統管理員目前有兩個自助式控制項。</span><span class="sxs-lookup"><span data-stu-id="1b4ea-232">Admins have two self-service controls today.</span></span> <span data-ttu-id="1b4ea-233">可以控制：</span><span class="sxs-lookup"><span data-stu-id="1b4ea-233">They can control:</span></span>

* <span data-ttu-id="1b4ea-234">使用者是否可以透過電子郵件加入目錄。</span><span class="sxs-lookup"><span data-stu-id="1b4ea-234">Whether or not users can join the directory via email.</span></span>
* <span data-ttu-id="1b4ea-235">使用者是否可以自行授權應用程式和服務。</span><span class="sxs-lookup"><span data-stu-id="1b4ea-235">Whether or not users can license themselves for applications and services.</span></span>

### <a name="how-can-i-control-these-capabilities"></a><span data-ttu-id="1b4ea-236">如何控制這些功能？</span><span class="sxs-lookup"><span data-stu-id="1b4ea-236">How can I control these capabilities?</span></span>
<span data-ttu-id="1b4ea-237">系統管理員可以使用下列 Azure AD Cmdlet Set-MsolCompanySettings 參數設定這些功能：</span><span class="sxs-lookup"><span data-stu-id="1b4ea-237">An admin can configure these capabilities using these Azure AD cmdlet Set-MsolCompanySettings parameters:</span></span>

* <span data-ttu-id="1b4ea-238">**AllowEmailVerifiedUsers** 控制使用者是否可以建立或加入未受管理的目錄。</span><span class="sxs-lookup"><span data-stu-id="1b4ea-238">**AllowEmailVerifiedUsers** controls whether a user can create or join an unmanaged directory.</span></span> <span data-ttu-id="1b4ea-239">如果您將該參數設定為 $false，則經過電子郵件驗證的使用者都無法加入目錄。</span><span class="sxs-lookup"><span data-stu-id="1b4ea-239">If you set that parameter to $false, no email-verified users can join the directory.</span></span>
* <span data-ttu-id="1b4ea-240">**AllowAdHocSubscriptions** 控制使用者執行自助式註冊的能力。</span><span class="sxs-lookup"><span data-stu-id="1b4ea-240">**AllowAdHocSubscriptions** controls the ability for users to perform self-service sign up.</span></span> <span data-ttu-id="1b4ea-241">如果您將該參數為 $false，則沒有任何使用者可以執行自助式註冊。</span><span class="sxs-lookup"><span data-stu-id="1b4ea-241">If you set that parameter to $false, no users can perform self-service signup.</span></span>

### <a name="how-do-the-controls-work-together"></a><span data-ttu-id="1b4ea-242">這些控制項如何一起運作？</span><span class="sxs-lookup"><span data-stu-id="1b4ea-242">How do the controls work together?</span></span>
<span data-ttu-id="1b4ea-243">這兩個參數可合併使用，以定義更精確的自助式註冊控制項。</span><span class="sxs-lookup"><span data-stu-id="1b4ea-243">These two parameters can be used in conjunction to define more precise control over self-service sign up.</span></span> <span data-ttu-id="1b4ea-244">例如，下列命令可讓使用者執行自助式註冊，但僅限於在 Azure AD 中已有帳戶的使用者 (換句話說，需要建立電子郵件驗證帳戶的使用者無法執行自助式註冊)：</span><span class="sxs-lookup"><span data-stu-id="1b4ea-244">For example, the following command will allow users to perform self-service sign up, but only if those users already have an account in Azure AD (in other words, users who would need an email-verified account to be created cannot perform self-service sign up):</span></span>

    Set-MsolCompanySettings -AllowEmailVerifiedUsers $false -AllowAdHocSubscriptions $true

<span data-ttu-id="1b4ea-245">下列流程圖說明這些參數的所有不同組合，以及針對目錄和自助式註冊造成的情況。</span><span class="sxs-lookup"><span data-stu-id="1b4ea-245">The following flowchart explains all the different combinations for these parameters and the resulting conditions for the directory and self-service sign up.</span></span>

![][1]

<span data-ttu-id="1b4ea-246">如需如何使用這些參數的詳細資訊和相關範，請參閱 [Set-MsolCompanySettings](/powershell/module/msonline/set-msolcompanysettings?view=azureadps-1.0)。</span><span class="sxs-lookup"><span data-stu-id="1b4ea-246">For more information and examples of how to use these parameters, see [Set-MsolCompanySettings](/powershell/module/msonline/set-msolcompanysettings?view=azureadps-1.0).</span></span>

## <a name="see-also"></a><span data-ttu-id="1b4ea-247">另請參閱</span><span class="sxs-lookup"><span data-stu-id="1b4ea-247">See Also</span></span>
* [<span data-ttu-id="1b4ea-248">如何安裝和設定 Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="1b4ea-248">How to install and configure Azure PowerShell</span></span>](/powershell/azure/overview)
* [<span data-ttu-id="1b4ea-249">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="1b4ea-249">Azure PowerShell</span></span>](/powershell/azure/overview)
* [<span data-ttu-id="1b4ea-250">Azure Cmdlet 參考</span><span class="sxs-lookup"><span data-stu-id="1b4ea-250">Azure Cmdlet Reference</span></span>](/powershell/azure/get-started-azureps)
* [<span data-ttu-id="1b4ea-251">Set-MsolCompanySettings</span><span class="sxs-lookup"><span data-stu-id="1b4ea-251">Set-MsolCompanySettings</span></span>](/powershell/module/msonline/set-msolcompanysettings?view=azureadps-1.0)

<!--Image references-->
[1]: ./media/active-directory-self-service-signup/SelfServiceSignUpControls.png
