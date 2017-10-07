---
title: "aaaWhat 是 Azure 的自助註冊？ | Microsoft Docs"
description: "概觀自助式註冊 azure，toomanage hello 註冊程序，以及如何 tootake 透過 DNS 網域名稱。"
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
ms.openlocfilehash: dbf3b59e3807e98f7bf39f3d5591fcde01667323
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="what-is-self-service-signup-for-azure"></a><span data-ttu-id="5ae75-104">什麼是 Azure 的自助式註冊？</span><span class="sxs-lookup"><span data-stu-id="5ae75-104">What is Self-Service Signup for Azure?</span></span>
<span data-ttu-id="5ae75-105">本主題說明 hello 自助式註冊程序和如何 tootake 透過 DNS 網域名稱。</span><span class="sxs-lookup"><span data-stu-id="5ae75-105">This topic explains hello self-service signup process and how tootake over a DNS domain name.</span></span>  

## <a name="why-use-self-service-signup"></a><span data-ttu-id="5ae75-106">為何使用自助式註冊？</span><span class="sxs-lookup"><span data-stu-id="5ae75-106">Why use self-service signup?</span></span>
* <span data-ttu-id="5ae75-107">取得客戶 tooservices 他們想要更快。</span><span class="sxs-lookup"><span data-stu-id="5ae75-107">Get customers tooservices they want faster.</span></span>
* <span data-ttu-id="5ae75-108">建立服務的電子郵件型供應項目。</span><span class="sxs-lookup"><span data-stu-id="5ae75-108">Create email-based offers for a service.</span></span>
* <span data-ttu-id="5ae75-109">建立快速允許使用者使用其容易記住的工作電子郵件別名的 toocreate 身分識別的電子郵件型註冊流程。</span><span class="sxs-lookup"><span data-stu-id="5ae75-109">Create email-based signup flows which quickly allow users toocreate identities using their easy-to-remember work email aliases.</span></span>
* <span data-ttu-id="5ae75-110">未受管理的 Azure 目錄後來可以轉換成受管理的目錄，並重複用於其他服務。</span><span class="sxs-lookup"><span data-stu-id="5ae75-110">Unmanaged Azure directories can be made into managed directories later and be reused for other services.</span></span>

## <a name="terms-and-definitions"></a><span data-ttu-id="5ae75-111">詞彙和定義</span><span class="sxs-lookup"><span data-stu-id="5ae75-111">Terms and Definitions</span></span>
* <span data-ttu-id="5ae75-112">**自助式註冊**： 這是程式的使用者註冊的雲端服務，並將具有 Azure Active Directory (Azure AD) 中自動建立它們的身分識別根據他們的電子郵件網域的 hello 方法。</span><span class="sxs-lookup"><span data-stu-id="5ae75-112">**Self-service sign up**: This is hello method by which a user signs up for a cloud service and has an identity automatically created for them in Azure Active Directory (Azure AD) based on their email domain.</span></span>
* <span data-ttu-id="5ae75-113">**未受管理的 Azure 目錄**： 這是該身分識別建立所在的 hello 目錄。</span><span class="sxs-lookup"><span data-stu-id="5ae75-113">**Unmanaged Azure directory**: This is hello directory where that identity is created.</span></span> <span data-ttu-id="5ae75-114">未受管理的目錄是沒有全域管理員的目錄。</span><span class="sxs-lookup"><span data-stu-id="5ae75-114">An unmanaged directory is a directory that has no global administrator.</span></span>
* <span data-ttu-id="5ae75-115">**電子郵件驗證的使用者**：這是 Azure AD 中的使用者帳戶類型。</span><span class="sxs-lookup"><span data-stu-id="5ae75-115">**Email-verified user**: This is a type of user account in Azure AD.</span></span> <span data-ttu-id="5ae75-116">在註冊自助式供應項目後自動建立身分識別的使用者，就是所謂的電子郵件驗證的使用者。</span><span class="sxs-lookup"><span data-stu-id="5ae75-116">A user who has an identity created automatically after signing up for a self-service offer is known as an email-verified user.</span></span> <span data-ttu-id="5ae75-117">電子郵件驗證的使用者是加上 creationmethod=EmailVerified 標記之目錄的一般成員。</span><span class="sxs-lookup"><span data-stu-id="5ae75-117">An email-verified user is a regular member of a directory tagged with creationmethod=EmailVerified.</span></span>

## <a name="user-experience"></a><span data-ttu-id="5ae75-118">使用者體驗</span><span class="sxs-lookup"><span data-stu-id="5ae75-118">User experience</span></span>
<span data-ttu-id="5ae75-119">例如，假設電子郵件為 Dan@BellowsCollege.com 的使用者會透過電子郵件接收機密檔案。</span><span class="sxs-lookup"><span data-stu-id="5ae75-119">For example, let's say a user whose email is Dan@BellowsCollege.com receives sensitive files via email.</span></span> <span data-ttu-id="5ae75-120">hello 檔案已受 Azure Rights Management (Azure RMS)。</span><span class="sxs-lookup"><span data-stu-id="5ae75-120">hello files have been protected by Azure Rights Management (Azure RMS).</span></span> <span data-ttu-id="5ae75-121">但是 Dan 的組織 (Bellows College) 尚未註冊 Azure RMS，也未部署 Active Directory RMS。</span><span class="sxs-lookup"><span data-stu-id="5ae75-121">But Dan's organization, Bellows College, has not signed up for Azure RMS, nor has it deployed Active Directory RMS.</span></span> <span data-ttu-id="5ae75-122">在此情況下，Dan 可以申請免費訂用帳戶 tooRMS 順序 tooread hello 受保護的檔案中的個人。</span><span class="sxs-lookup"><span data-stu-id="5ae75-122">In this case, Dan can sign up for a free subscription tooRMS for individuals in order tooread hello protected files.</span></span>

<span data-ttu-id="5ae75-123">如果 Dan hello 第一位使用者與此供應項目的自助註冊 BellowsCollege.com toosign 從電子郵件地址，然後未受管理的目錄將會建立 BellowsCollege.com 在 Azure AD 中。</span><span class="sxs-lookup"><span data-stu-id="5ae75-123">If Dan is hello first user with an email address from BellowsCollege.com toosign up for this self-service offering, then an unmanaged directory will be created for BellowsCollege.com in Azure AD.</span></span> <span data-ttu-id="5ae75-124">如果來自 hello BellowsCollege.com 網域的其他使用者註冊此供應項目或類似的自助服務供應項目，它們也會具有電子郵件驗證建立的使用者帳戶在 hello 相同 unmanaged 在 Azure 中的目錄。</span><span class="sxs-lookup"><span data-stu-id="5ae75-124">If other users from hello BellowsCollege.com domain sign up for this offering or a similar self-service offering, they will also have email-verified user accounts created in hello same unmanaged directory in Azure.</span></span>

## <a name="admin-experience"></a><span data-ttu-id="5ae75-125">管理員體驗</span><span class="sxs-lookup"><span data-stu-id="5ae75-125">Admin experience</span></span>
<span data-ttu-id="5ae75-126">擁有 hello DNS 網域名稱未受管理的 Azure 目錄的系統管理員可以接管或合併 hello 目錄之後證明擁有權。</span><span class="sxs-lookup"><span data-stu-id="5ae75-126">An admin who owns hello DNS domain name of an unmanaged Azure directory can take over or merge hello directory after proving ownership.</span></span> <span data-ttu-id="5ae75-127">hello 以下幾節說明 hello 系統管理員體驗的詳細資料，但是摘要如下：</span><span class="sxs-lookup"><span data-stu-id="5ae75-127">hello next sections explain hello admin experience in more detail, but here's a summary:</span></span>

* <span data-ttu-id="5ae75-128">當您接管的未受管理的 Azure 目錄時，您只需變得 hello hello unmanaged 目錄全域管理員。</span><span class="sxs-lookup"><span data-stu-id="5ae75-128">When you take over an unmanaged Azure directory, you simply become hello global administrator of hello unmanaged directory.</span></span> <span data-ttu-id="5ae75-129">這有時候稱為內部接管。</span><span class="sxs-lookup"><span data-stu-id="5ae75-129">This is sometimes called an internal takeover.</span></span>
* <span data-ttu-id="5ae75-130">當合併未受管理的 Azure 目錄，您將 hello unmanaged 的目錄 tooyour managed Azure 目錄的 hello DNS 網域名稱和使用者資源的對應會建立讓使用者可以繼續 tooaccess 服務不中斷。</span><span class="sxs-lookup"><span data-stu-id="5ae75-130">When you merge an unmanaged Azure directory, you add hello DNS domain name of hello unmanaged directory tooyour managed Azure directory and a mapping of users-to-resources is created so users can continue tooaccess services without interruption.</span></span> <span data-ttu-id="5ae75-131">這有時候稱為外部接管。</span><span class="sxs-lookup"><span data-stu-id="5ae75-131">This is sometimes called an external takeover.</span></span>

## <a name="what-gets-created-in-azure-active-directory"></a><span data-ttu-id="5ae75-132">Azure Active Directory 中建立的項目為何？</span><span class="sxs-lookup"><span data-stu-id="5ae75-132">What gets created in Azure Active Directory?</span></span>
#### <a name="directory"></a><span data-ttu-id="5ae75-133">目錄</span><span class="sxs-lookup"><span data-stu-id="5ae75-133">directory</span></span>
* <span data-ttu-id="5ae75-134">Hello 網域的 Azure Active Directory 目錄會建立一個目錄，每個網域。</span><span class="sxs-lookup"><span data-stu-id="5ae75-134">An Azure Active Directory directory for hello domain is created, one directory per domain.</span></span>
* <span data-ttu-id="5ae75-135">hello Azure AD 目錄中有任何全域管理員。</span><span class="sxs-lookup"><span data-stu-id="5ae75-135">hello Azure AD directory has no global admin.</span></span>

#### <a name="users"></a><span data-ttu-id="5ae75-136">使用者</span><span class="sxs-lookup"><span data-stu-id="5ae75-136">Users</span></span>
* <span data-ttu-id="5ae75-137">每個使用者註冊，使用者物件建立 hello Azure AD 目錄中。</span><span class="sxs-lookup"><span data-stu-id="5ae75-137">For each user who signs up, a user object is created in hello Azure AD directory.</span></span>
* <span data-ttu-id="5ae75-138">每個使用者物件都標示為外部。</span><span class="sxs-lookup"><span data-stu-id="5ae75-138">Each user object is marked as external.</span></span>
* <span data-ttu-id="5ae75-139">每個使用者可以註冊這些簽署存取 toohello 服務。</span><span class="sxs-lookup"><span data-stu-id="5ae75-139">Each user is given access toohello service that they signed up for.</span></span>

### <a name="how-do-i-claim-a-self-service-azure-ad-directory-for-a-domain-i-own"></a><span data-ttu-id="5ae75-140">如何針對我擁有的網域宣告自助式 Azure AD 目錄？</span><span class="sxs-lookup"><span data-stu-id="5ae75-140">How do I claim a self-service Azure AD directory for a domain I own?</span></span>
<span data-ttu-id="5ae75-141">您可以執行網域驗證來宣告自助式 Azure AD 目錄。</span><span class="sxs-lookup"><span data-stu-id="5ae75-141">You can claim a self-service Azure AD directory by performing domain validation.</span></span> <span data-ttu-id="5ae75-142">網域驗證證明您自己的 hello 網域建立 DNS 記錄。</span><span class="sxs-lookup"><span data-stu-id="5ae75-142">Domain validation proves you own hello domain by creating DNS records.</span></span>

<span data-ttu-id="5ae75-143">有兩種方式 toodo DNS 接管的 Azure AD 目錄：</span><span class="sxs-lookup"><span data-stu-id="5ae75-143">There are two ways toodo a DNS takeover of an Azure AD directory:</span></span>

* <span data-ttu-id="5ae75-144">內部接管 （管理探索未受管理的 Azure 目錄，以及想 tooturn 到受管理的目錄）</span><span class="sxs-lookup"><span data-stu-id="5ae75-144">internal takeover (Admin discovers an unmanaged Azure directory, and wants tooturn into a managed directory)</span></span>
* <span data-ttu-id="5ae75-145">外部接管 （系統管理員會嘗試 tooadd 到新網域 tootheir 受管理的 Azure 目錄）</span><span class="sxs-lookup"><span data-stu-id="5ae75-145">external takeover (Admin tries tooadd a new domain tootheir managed Azure directory)</span></span>

<span data-ttu-id="5ae75-146">您可能會想要驗證您擁有網域，因為在使用者執行自助式註冊，或您可能會加入新網域 tooan 現有受管理的目錄之後，您就可以透過未受管理的目錄。</span><span class="sxs-lookup"><span data-stu-id="5ae75-146">You might be interested in validating that you own a domain because you are taking over an unmanaged directory after a user performed self-service signup, or you might be adding a new domain tooan existing managed directory.</span></span> <span data-ttu-id="5ae75-147">例如，您有名稱為 contoso.com 的網域，而且您想 tooadd contoso.co.uk 或 contoso.uk 命名新的網域。</span><span class="sxs-lookup"><span data-stu-id="5ae75-147">For example, you have a domain named contoso.com and you want tooadd a new domain named contoso.co.uk or contoso.uk.</span></span>

## <a name="what-is-domain-takeover"></a><span data-ttu-id="5ae75-148">什麼是網域接管？</span><span class="sxs-lookup"><span data-stu-id="5ae75-148">What is domain takeover?</span></span>
<span data-ttu-id="5ae75-149">本章節涵蓋如何您擁有網域 toovalidate</span><span class="sxs-lookup"><span data-stu-id="5ae75-149">This section covers how toovalidate that you own a domain</span></span>

### <a name="what-is-domain-validation-and-why-is-it-used"></a><span data-ttu-id="5ae75-150">什麼是網域驗證，以及為何使用？</span><span class="sxs-lookup"><span data-stu-id="5ae75-150">What is domain validation and why is it used?</span></span>
<span data-ttu-id="5ae75-151">在訂單 tooperform 作業在目錄中，Azure AD 會要求您驗證 hello DNS 網域的擁有權。</span><span class="sxs-lookup"><span data-stu-id="5ae75-151">In order tooperform operations on a directory, Azure AD requires that you validate ownership of hello DNS domain.</span></span>  <span data-ttu-id="5ae75-152">Hello 網域的驗證可讓您 tooclaim hello 目錄，然後升級 hello 自助目錄 tooa 管理的目錄，或合併 hello 自助服務目錄中的現有受管理的目錄。</span><span class="sxs-lookup"><span data-stu-id="5ae75-152">Validation of hello domain allows you tooclaim hello directory and either promote hello self-service directory tooa managed directory, or merge hello self-service directory into an existing managed directory.</span></span>

## <a name="examples-of-domain-validation"></a><span data-ttu-id="5ae75-153">網域驗證範例</span><span class="sxs-lookup"><span data-stu-id="5ae75-153">Examples of domain validation</span></span>
<span data-ttu-id="5ae75-154">有兩種方式 toodo DNS 接管的目錄：</span><span class="sxs-lookup"><span data-stu-id="5ae75-154">There are two ways toodo a DNS takeover of a directory:</span></span>

* <span data-ttu-id="5ae75-155">內部接管 （例如，可探索自助服務、 未受管理的目錄，而且想 tooturn 到受管理的目錄系統管理員）</span><span class="sxs-lookup"><span data-stu-id="5ae75-155">internal takeover  (For example, an admin discovers a self-service, unmanaged directory, and wants tooturn into managed directory)</span></span>
* <span data-ttu-id="5ae75-156">外部接管 （例如，系統管理員會嘗試 tooadd 新網域 tooa 受管理的目錄）</span><span class="sxs-lookup"><span data-stu-id="5ae75-156">external takeover (For example, a admin tries tooadd a new domain tooa managed directory)</span></span>

### <a name="internal-takeover---promote-a-self-service-unmanaged-directory-toobe-a-managed-directory"></a><span data-ttu-id="5ae75-157">內部接管-升級自助服務、 未受管理的目錄 toobe 受管理的目錄</span><span class="sxs-lookup"><span data-stu-id="5ae75-157">Internal Takeover - promote a self-service, unmanaged directory toobe a managed directory</span></span>
<span data-ttu-id="5ae75-158">當您進行內部接管時，取得會從 unmanaged 的目錄 tooa 管理目錄轉換 hello 目錄。</span><span class="sxs-lookup"><span data-stu-id="5ae75-158">When you do internal takeover, hello directory gets converted from an unmanaged directory tooa managed directory.</span></span> <span data-ttu-id="5ae75-159">您需要 toocomplete DNS 網域名稱驗證，其中 hello DNS 區域中建立 MX 記錄或 TXT 記錄。</span><span class="sxs-lookup"><span data-stu-id="5ae75-159">You need toocomplete DNS domain name validation, where you create an MX record or a TXT record in hello DNS zone.</span></span> <span data-ttu-id="5ae75-160">該動作：</span><span class="sxs-lookup"><span data-stu-id="5ae75-160">That action:</span></span>

* <span data-ttu-id="5ae75-161">驗證您擁有 hello 網域</span><span class="sxs-lookup"><span data-stu-id="5ae75-161">Validates that you own hello domain</span></span>
* <span data-ttu-id="5ae75-162">可讓受管理的 hello 目錄</span><span class="sxs-lookup"><span data-stu-id="5ae75-162">Makes hello directory managed</span></span>
* <span data-ttu-id="5ae75-163">可讓您 hello hello 目錄的全域管理員</span><span class="sxs-lookup"><span data-stu-id="5ae75-163">Makes you hello global admin of hello directory</span></span>

<span data-ttu-id="5ae75-164">讓我們假設您的 IT 系統管理員身分從波紋管大學探索 hello 學校的使用者已註冊為自助服務供應項目。</span><span class="sxs-lookup"><span data-stu-id="5ae75-164">Let's say an IT administrator from Bellows College discovers that users from hello school have signed up for self-service offerings.</span></span> <span data-ttu-id="5ae75-165">Hello 註冊 hello DNS 的擁有者名稱 BellowsCollege.com、 hello IT 系統管理員可以驗證在 Azure 中的 hello DNS 名稱的擁有權，並再 hello 未受管理的目錄。</span><span class="sxs-lookup"><span data-stu-id="5ae75-165">As hello registered owner of hello DNS name BellowsCollege.com, hello IT administrator can validate ownership of hello DNS name in Azure and then take over hello unmanaged directory.</span></span> <span data-ttu-id="5ae75-166">hello 目錄就會變成受管理的目錄，而且 hello IT 系統管理員指派 hello hello BellowsCollege.com 目錄的全域管理員角色。</span><span class="sxs-lookup"><span data-stu-id="5ae75-166">hello directory then becomes a managed directory, and hello IT administrator is assigned hello global administrator role for hello BellowsCollege.com directory.</span></span>

### <a name="external-takeover---merge-a-self-service-directory-into-an-existing-managed-directory"></a><span data-ttu-id="5ae75-167">外部接管 - 將自助式目錄合併到現有的受管理目錄</span><span class="sxs-lookup"><span data-stu-id="5ae75-167">External Takeover - merge a self-service directory into an existing managed directory</span></span>
<span data-ttu-id="5ae75-168">在外部的接管您已經有受管理的目錄和您想要所有使用者和群組從受管理的目錄中，未受管理的目錄 toojoin 而自己的兩個不同的目錄。</span><span class="sxs-lookup"><span data-stu-id="5ae75-168">In an external takeover, you already have a managed directory and you want all users and groups from an unmanaged directory toojoin that managed directory, rather than own two separate directories.</span></span>

<span data-ttu-id="5ae75-169">身為系統管理員的受管理的目錄中，您將加入網域，而且該網域剛好 toohave unmanaged 與它相關聯的目錄。</span><span class="sxs-lookup"><span data-stu-id="5ae75-169">As an admin of a managed directory, you add a domain, and that domain happens toohave an unmanaged directory associated with it.</span></span>

<span data-ttu-id="5ae75-170">例如，假設您是 IT 系統管理員，而且您已經擁有的受管理的目錄，對 Contoso.com 是已註冊的 tooyour 組織的網域名稱。</span><span class="sxs-lookup"><span data-stu-id="5ae75-170">For example, let's say you are an IT administrator and you already have a managed directory for Contoso.com, a domain name that is registered tooyour organization.</span></span> <span data-ttu-id="5ae75-171">您會發現貴組織的使用者已使用電子郵件網域名稱 user@contoso.co.uk (這是貴組織擁有的另一個網域名稱) 以自助方式註冊產品方案。</span><span class="sxs-lookup"><span data-stu-id="5ae75-171">You discover that users from your organization have performed self-service sign up for an offering by using email domain name user@contoso.co.uk, which is another domain name that your organization owns.</span></span> <span data-ttu-id="5ae75-172">這些使用者目前在 contoso.co.uk 的未受管理目錄中有帳戶。</span><span class="sxs-lookup"><span data-stu-id="5ae75-172">Those users currently have accounts in an unmanaged directory for contoso.co.uk.</span></span>

<span data-ttu-id="5ae75-173">您不想 toomanage 兩個個別目錄，因此 contoso.co.uk hello unmanaged 的目錄合併到現有的受管理的 IT 目錄 contoso.com。</span><span class="sxs-lookup"><span data-stu-id="5ae75-173">You don't want toomanage two separate directories, so you merge hello unmanaged directory for contoso.co.uk into your existing IT managed directory for contoso.com.</span></span>

<span data-ttu-id="5ae75-174">外部接管如下所示 hello 相同內部接管的 DNS 驗證程序。</span><span class="sxs-lookup"><span data-stu-id="5ae75-174">External takeover follows hello same DNS validation process as internal takeover.</span></span>  <span data-ttu-id="5ae75-175">正在執行的差異： 使用者和服務會重新對應的 toohello IT 管理的目錄。</span><span class="sxs-lookup"><span data-stu-id="5ae75-175">Difference being: users and services are remapped toohello IT managed directory.</span></span>

#### <a name="whats-hello-impact-of-performing-an-external-takeover"></a><span data-ttu-id="5ae75-176">執行外部接管 hello 影響為何？</span><span class="sxs-lookup"><span data-stu-id="5ae75-176">What's hello impact of performing an external takeover?</span></span>
<span data-ttu-id="5ae75-177">透過外部的接管使用者為資源的對應會建立讓使用者可以繼續 tooaccess 服務不中斷。</span><span class="sxs-lookup"><span data-stu-id="5ae75-177">With an external takeover, a mapping of users-to-resources is created so users can continue tooaccess services without interruption.</span></span> <span data-ttu-id="5ae75-178">許多應用程式，包括個人版，RMS，處理 hello 對應使用者的資源，而且使用者可以繼續 tooaccess 而不需要變更這些服務。</span><span class="sxs-lookup"><span data-stu-id="5ae75-178">Many applications, including RMS for individuals, handle hello mapping of users-to-resources well, and users can continue tooaccess those services without change.</span></span> <span data-ttu-id="5ae75-179">如果應用程式不會有效地處理 hello 對應的使用者-資源、 外部接管可能會明確封鎖的 tooprevent 使用者不佳的體驗。</span><span class="sxs-lookup"><span data-stu-id="5ae75-179">If an application does not handle hello mapping of users-to-resources effectively, external takeover may be explicitly blocked tooprevent users from a poor experience.</span></span>

#### <a name="directory-takeover-support-by-service"></a><span data-ttu-id="5ae75-180">服務支援的目錄接管</span><span class="sxs-lookup"><span data-stu-id="5ae75-180">directory takeover support by service</span></span>
<span data-ttu-id="5ae75-181">目前 hello 下列服務支援接管：</span><span class="sxs-lookup"><span data-stu-id="5ae75-181">Currently hello following services support takeover:</span></span>

* <span data-ttu-id="5ae75-182">RMS</span><span class="sxs-lookup"><span data-stu-id="5ae75-182">RMS</span></span>

<span data-ttu-id="5ae75-183">下列服務的 hello 將很快就會支援接管：</span><span class="sxs-lookup"><span data-stu-id="5ae75-183">hello following services will soon be supporting takeover:</span></span>

* <span data-ttu-id="5ae75-184">PowerBI</span><span class="sxs-lookup"><span data-stu-id="5ae75-184">PowerBI</span></span>

<span data-ttu-id="5ae75-185">hello 下列外部接管之後需要額外的管理動作 toomigrate 使用者資料，並不相符。</span><span class="sxs-lookup"><span data-stu-id="5ae75-185">hello following do not and require additional admin action toomigrate user data after an external takeover.</span></span>

* <span data-ttu-id="5ae75-186">SharePoint/OneDrive</span><span class="sxs-lookup"><span data-stu-id="5ae75-186">SharePoint/OneDrive</span></span>

## <a name="how-tooperform-a-dns-domain-name-takeover"></a><span data-ttu-id="5ae75-187">如何 tooperform DNS 網域名稱接管</span><span class="sxs-lookup"><span data-stu-id="5ae75-187">How tooperform a DNS domain name takeover</span></span>
<span data-ttu-id="5ae75-188">您有幾個選項，供 tooperform 網域驗證 （和執行接管，如果您想）：</span><span class="sxs-lookup"><span data-stu-id="5ae75-188">You have a few options for how tooperform a domain validation (and do a takeover if you wish):</span></span>

1. <span data-ttu-id="5ae75-189">Azure 管理入口網站</span><span class="sxs-lookup"><span data-stu-id="5ae75-189">Azure Management Portal</span></span>

   <span data-ttu-id="5ae75-190">接管是由執行網域新增所觸發。</span><span class="sxs-lookup"><span data-stu-id="5ae75-190">A takeover is triggered by doing a domain addition.</span></span>  <span data-ttu-id="5ae75-191">如果目錄已經存在 hello 網域，您將有 hello 選項 tooperform 外部接管。</span><span class="sxs-lookup"><span data-stu-id="5ae75-191">If a directory already exists for hello domain, you'll have hello option tooperform an external takeover.</span></span>

   <span data-ttu-id="5ae75-192">登入 toohello Azure 入口網站使用您的認證。</span><span class="sxs-lookup"><span data-stu-id="5ae75-192">Sign in toohello Azure portal using your credentials.</span></span>  <span data-ttu-id="5ae75-193">瀏覽 tooyour 現有目錄，然後太**新增網域**。</span><span class="sxs-lookup"><span data-stu-id="5ae75-193">Navigate tooyour existing directory and then too**Add domain**.</span></span>
2. <span data-ttu-id="5ae75-194">Office 365</span><span class="sxs-lookup"><span data-stu-id="5ae75-194">Office 365</span></span>

   <span data-ttu-id="5ae75-195">您可以使用 hello hello 選項[管理網域](https://support.office.com/article/Navigate-to-the-Office-365-Manage-domains-page-026af1f2-0e6d-4f2d-9b33-fd147420fac2/)Office 365 toowork 與您的網域和 DNS 記錄中的頁面。</span><span class="sxs-lookup"><span data-stu-id="5ae75-195">You can use hello options on hello [Manage domains](https://support.office.com/article/Navigate-to-the-Office-365-Manage-domains-page-026af1f2-0e6d-4f2d-9b33-fd147420fac2/) page in Office 365 toowork with your domains and DNS records.</span></span> <span data-ttu-id="5ae75-196">請參閱 [在 Office 365 中驗證您的網域](https://support.office.com/article/Verify-your-domain-in-Office-365-6383f56d-3d09-4dcb-9b41-b5f5a5efd611/)。</span><span class="sxs-lookup"><span data-stu-id="5ae75-196">See [Verify your domain in Office 365](https://support.office.com/article/Verify-your-domain-in-Office-365-6383f56d-3d09-4dcb-9b41-b5f5a5efd611/).</span></span>
3. <span data-ttu-id="5ae75-197">Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="5ae75-197">Windows PowerShell</span></span>

   <span data-ttu-id="5ae75-198">hello 步驟是必要的 tooperform 驗證，使用 Windows PowerShell。</span><span class="sxs-lookup"><span data-stu-id="5ae75-198">hello following steps are required tooperform a validation using Windows PowerShell.</span></span>

   | <span data-ttu-id="5ae75-199">步驟</span><span class="sxs-lookup"><span data-stu-id="5ae75-199">Step</span></span> | <span data-ttu-id="5ae75-200">Cmdlet toouse</span><span class="sxs-lookup"><span data-stu-id="5ae75-200">Cmdlet toouse</span></span> |
   | --- | --- |
   | <span data-ttu-id="5ae75-201">建立認證物件</span><span class="sxs-lookup"><span data-stu-id="5ae75-201">Create a credential object</span></span> |<span data-ttu-id="5ae75-202">Get-Credential</span><span class="sxs-lookup"><span data-stu-id="5ae75-202">Get-Credential</span></span> |
   | <span data-ttu-id="5ae75-203">連接 tooAzure AD</span><span class="sxs-lookup"><span data-stu-id="5ae75-203">Connect tooAzure AD</span></span> |<span data-ttu-id="5ae75-204">Connect-MsolService</span><span class="sxs-lookup"><span data-stu-id="5ae75-204">Connect-MsolService</span></span> |
   | <span data-ttu-id="5ae75-205">取得網域清單</span><span class="sxs-lookup"><span data-stu-id="5ae75-205">get a list of domains</span></span> |<span data-ttu-id="5ae75-206">Get-MsolDomain</span><span class="sxs-lookup"><span data-stu-id="5ae75-206">Get-MsolDomain</span></span> |
   | <span data-ttu-id="5ae75-207">建立挑戰</span><span class="sxs-lookup"><span data-stu-id="5ae75-207">Create a challenge</span></span> |<span data-ttu-id="5ae75-208">Get-MsolDomainVerificationDns</span><span class="sxs-lookup"><span data-stu-id="5ae75-208">Get-MsolDomainVerificationDns</span></span> |
   | <span data-ttu-id="5ae75-209">建立 DNS 記錄</span><span class="sxs-lookup"><span data-stu-id="5ae75-209">Create DNS record</span></span> |<span data-ttu-id="5ae75-210">在您的 DNS 伺服器上執行這項操作</span><span class="sxs-lookup"><span data-stu-id="5ae75-210">Do this on your DNS server</span></span> |
   | <span data-ttu-id="5ae75-211">確認 hello 挑戰</span><span class="sxs-lookup"><span data-stu-id="5ae75-211">Verify hello challenge</span></span> |<span data-ttu-id="5ae75-212">Confirm-MsolEmailVerifiedDomain</span><span class="sxs-lookup"><span data-stu-id="5ae75-212">Confirm-MsolEmailVerifiedDomain</span></span> |

<span data-ttu-id="5ae75-213">例如：</span><span class="sxs-lookup"><span data-stu-id="5ae75-213">For example:</span></span>

1. <span data-ttu-id="5ae75-214">連接 tooAzure AD 使用 hello 認證所使用的 toorespond toohello 自助服務供應項目：</span><span class="sxs-lookup"><span data-stu-id="5ae75-214">Connect tooAzure AD using hello credentials that were used toorespond toohello self-service offering:</span></span>

        import-module MSOnline
        $msolcred = get-credential
        connect-msolservice -credential $msolcred
2. <span data-ttu-id="5ae75-215">取得網域清單：</span><span class="sxs-lookup"><span data-stu-id="5ae75-215">Get a list of domains:</span></span>

    <span data-ttu-id="5ae75-216">Get-MsolDomain</span><span class="sxs-lookup"><span data-stu-id="5ae75-216">Get-MsolDomain</span></span>
3. <span data-ttu-id="5ae75-217">然後執行 hello Get-msoldomainverificationdns cmdlet toocreate 一項挑戰：</span><span class="sxs-lookup"><span data-stu-id="5ae75-217">Then run hello Get-MsolDomainVerificationDns cmdlet toocreate a challenge:</span></span>

    <span data-ttu-id="5ae75-218">Get-MsolDomainVerificationDns –DomainName *your_domain_name* –Mode DnsTxtRecord</span><span class="sxs-lookup"><span data-stu-id="5ae75-218">Get-MsolDomainVerificationDns –DomainName *your_domain_name* –Mode DnsTxtRecord</span></span>

    <span data-ttu-id="5ae75-219">例如：</span><span class="sxs-lookup"><span data-stu-id="5ae75-219">For example:</span></span>

    <span data-ttu-id="5ae75-220">Get-MsolDomainVerificationDns –DomainName contoso.com –Mode DnsTxtRecord</span><span class="sxs-lookup"><span data-stu-id="5ae75-220">Get-MsolDomainVerificationDns –DomainName contoso.com –Mode DnsTxtRecord</span></span>
4. <span data-ttu-id="5ae75-221">複製此命令會傳回 hello 值 （hello 挑戰）。</span><span class="sxs-lookup"><span data-stu-id="5ae75-221">Copy hello value (hello challenge) that is returned from this command.</span></span>

    <span data-ttu-id="5ae75-222">例如：</span><span class="sxs-lookup"><span data-stu-id="5ae75-222">For example:</span></span>

    <span data-ttu-id="5ae75-223">MS=32DD01B82C05D27151EA9AE93C5890787F0E65D9</span><span class="sxs-lookup"><span data-stu-id="5ae75-223">MS=32DD01B82C05D27151EA9AE93C5890787F0E65D9</span></span>
5. <span data-ttu-id="5ae75-224">在公用 DNS 命名空間，建立 DNS txt 記錄，其中包含您在 hello 上一個步驟中複製的 hello 值。</span><span class="sxs-lookup"><span data-stu-id="5ae75-224">In your public DNS namespace, create a DNS txt record that contains hello value that you copied in hello previous step.</span></span>

    <span data-ttu-id="5ae75-225">這個記錄的 hello 名稱是 hello hello 父系網域的名稱，因此如果您使用 Windows 伺服器 hello DNS 角色建立此資源記錄，將 hello 記錄名稱保留空白，而且只要 hello 值貼到 [hello] 文字方塊中</span><span class="sxs-lookup"><span data-stu-id="5ae75-225">hello name for this record is hello name of hello parent domain, so if you create this resource record by using hello DNS role from Windows Server, leave hello Record name blank and just paste hello value into hello Text box</span></span>
6. <span data-ttu-id="5ae75-226">執行 hello Confirm-msoldomain cmdlet tooverify hello 挑戰：</span><span class="sxs-lookup"><span data-stu-id="5ae75-226">Run hello Confirm-MsolDomain cmdlet tooverify hello challenge:</span></span>

    <span data-ttu-id="5ae75-227">Confirm-MsolEmailVerifiedDomain -DomainName *your_domain_name*</span><span class="sxs-lookup"><span data-stu-id="5ae75-227">Confirm-MsolEmailVerifiedDomain -DomainName *your_domain_name*</span></span>

    <span data-ttu-id="5ae75-228">例如：</span><span class="sxs-lookup"><span data-stu-id="5ae75-228">for example:</span></span>

    <span data-ttu-id="5ae75-229">Confirm-MsolEmailVerifiedDomain -DomainName contoso.com</span><span class="sxs-lookup"><span data-stu-id="5ae75-229">Confirm-MsolEmailVerifiedDomain -DomainName contoso.com</span></span>

<span data-ttu-id="5ae75-230">成功挑戰會傳回 toohello 提示字元，且未產生錯誤。</span><span class="sxs-lookup"><span data-stu-id="5ae75-230">A successful challenge returns you toohello prompt without an error.</span></span>

## <a name="how-do-i-control-self-service-settings"></a><span data-ttu-id="5ae75-231">如何控制自助式設定？</span><span class="sxs-lookup"><span data-stu-id="5ae75-231">How do I control self-service settings?</span></span>
<span data-ttu-id="5ae75-232">系統管理員目前有兩個自助式控制項。</span><span class="sxs-lookup"><span data-stu-id="5ae75-232">Admins have two self-service controls today.</span></span> <span data-ttu-id="5ae75-233">可以控制：</span><span class="sxs-lookup"><span data-stu-id="5ae75-233">They can control:</span></span>

* <span data-ttu-id="5ae75-234">是否使用者可以加入 hello 目錄，透過電子郵件。</span><span class="sxs-lookup"><span data-stu-id="5ae75-234">Whether or not users can join hello directory via email.</span></span>
* <span data-ttu-id="5ae75-235">使用者是否可以自行授權應用程式和服務。</span><span class="sxs-lookup"><span data-stu-id="5ae75-235">Whether or not users can license themselves for applications and services.</span></span>

### <a name="how-can-i-control-these-capabilities"></a><span data-ttu-id="5ae75-236">如何控制這些功能？</span><span class="sxs-lookup"><span data-stu-id="5ae75-236">How can I control these capabilities?</span></span>
<span data-ttu-id="5ae75-237">系統管理員可以使用下列 Azure AD Cmdlet Set-MsolCompanySettings 參數設定這些功能：</span><span class="sxs-lookup"><span data-stu-id="5ae75-237">An admin can configure these capabilities using these Azure AD cmdlet Set-MsolCompanySettings parameters:</span></span>

* <span data-ttu-id="5ae75-238">**AllowEmailVerifiedUsers** 控制使用者是否可以建立或加入未受管理的目錄。</span><span class="sxs-lookup"><span data-stu-id="5ae75-238">**AllowEmailVerifiedUsers** controls whether a user can create or join an unmanaged directory.</span></span> <span data-ttu-id="5ae75-239">如果您將該參數太 $false，則沒有電子郵件驗證的使用者可以加入 hello 目錄。</span><span class="sxs-lookup"><span data-stu-id="5ae75-239">If you set that parameter too$false, no email-verified users can join hello directory.</span></span>
* <span data-ttu-id="5ae75-240">**AllowAdHocSubscriptions**控制 hello tooperform 自助登入使用者的能力。</span><span class="sxs-lookup"><span data-stu-id="5ae75-240">**AllowAdHocSubscriptions** controls hello ability for users tooperform self-service sign up.</span></span> <span data-ttu-id="5ae75-241">如果您將該參數太 $false，沒有任何使用者可以執行自助式註冊。</span><span class="sxs-lookup"><span data-stu-id="5ae75-241">If you set that parameter too$false, no users can perform self-service signup.</span></span>

### <a name="how-do-hello-controls-work-together"></a><span data-ttu-id="5ae75-242">Hello 控制項如何一起？</span><span class="sxs-lookup"><span data-stu-id="5ae75-242">How do hello controls work together?</span></span>
<span data-ttu-id="5ae75-243">這兩個參數可以用於搭配 toodefine 更精確地控制自助登入。</span><span class="sxs-lookup"><span data-stu-id="5ae75-243">These two parameters can be used in conjunction toodefine more precise control over self-service sign up.</span></span> <span data-ttu-id="5ae75-244">比方說，下列命令的 hello 可讓使用者 tooperform 自助式註冊，但僅限於如果這些使用者已經有 Azure AD 的帳戶 （亦即，使用者必須建立電子郵件驗證帳戶 toobe 無法將自助登執行向上）：</span><span class="sxs-lookup"><span data-stu-id="5ae75-244">For example, hello following command will allow users tooperform self-service sign up, but only if those users already have an account in Azure AD (in other words, users who would need an email-verified account toobe created cannot perform self-service sign up):</span></span>

    Set-MsolCompanySettings -AllowEmailVerifiedUsers $false -AllowAdHocSubscriptions $true

<span data-ttu-id="5ae75-245">hello 以下流程圖說明對這些參數的 hello 不同組合與 hello 產生條件 hello 目錄和自助式註冊。</span><span class="sxs-lookup"><span data-stu-id="5ae75-245">hello following flowchart explains all hello different combinations for these parameters and hello resulting conditions for hello directory and self-service sign up.</span></span>

![][1]

<span data-ttu-id="5ae75-246">如需詳細資訊和範例的方式 toouse 這些參數，請參閱[Set-msolcompanysettings](/powershell/module/msonline/set-msolcompanysettings?view=azureadps-1.0)。</span><span class="sxs-lookup"><span data-stu-id="5ae75-246">For more information and examples of how toouse these parameters, see [Set-MsolCompanySettings](/powershell/module/msonline/set-msolcompanysettings?view=azureadps-1.0).</span></span>

## <a name="see-also"></a><span data-ttu-id="5ae75-247">另請參閱</span><span class="sxs-lookup"><span data-stu-id="5ae75-247">See Also</span></span>
* [<span data-ttu-id="5ae75-248">如何 tooinstall 和設定 Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="5ae75-248">How tooinstall and configure Azure PowerShell</span></span>](/powershell/azure/overview)
* [<span data-ttu-id="5ae75-249">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="5ae75-249">Azure PowerShell</span></span>](/powershell/azure/overview)
* [<span data-ttu-id="5ae75-250">Azure Cmdlet 參考</span><span class="sxs-lookup"><span data-stu-id="5ae75-250">Azure Cmdlet Reference</span></span>](/powershell/azure/get-started-azureps)
* [<span data-ttu-id="5ae75-251">Set-MsolCompanySettings</span><span class="sxs-lookup"><span data-stu-id="5ae75-251">Set-MsolCompanySettings</span></span>](/powershell/module/msonline/set-msolcompanysettings?view=azureadps-1.0)

<!--Image references-->
[1]: ./media/active-directory-self-service-signup/SelfServiceSignUpControls.png
