---
title: "aaaAzure Active Directory 常見問題集 |Microsoft 文件"
description: "Azure Active Directory 常見問題集解答疑問 tooaccess Azure 和 Azure Active Directory、 密碼管理和應用程式的存取。"
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
ms.assetid: b8207760-9714-4871-93d5-f9893de31c8f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 08/16/2017
ms.author: markvi
ms.openlocfilehash: 63c30c4aeda4551bf02c6b968f98cded5a3b2c16
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-faq"></a><span data-ttu-id="a2acc-103">Azure Active Directory 常見問題集</span><span class="sxs-lookup"><span data-stu-id="a2acc-103">Azure Active Directory FAQ</span></span>
<span data-ttu-id="a2acc-104">Azure Active Directory (Azure AD) 是全方位的身分識別即服務 (IDaaS) 解決方案，其涉及範圍橫跨身分識別、存取管理和安全性的所有層面。</span><span class="sxs-lookup"><span data-stu-id="a2acc-104">Azure Active Directory (Azure AD) is a comprehensive identity as a service (IDaaS) solution that spans all aspects of identity, access management, and security.</span></span>

<span data-ttu-id="a2acc-105">如需詳細資訊，請參閱[什麼是 Azure Active Directory？](active-directory-whatis.md)。</span><span class="sxs-lookup"><span data-stu-id="a2acc-105">For more information, see [What is Azure Active Directory?](active-directory-whatis.md).</span></span>


## <a name="access-azure-and-azure-active-directory"></a><span data-ttu-id="a2acc-106">存取 Azure 和 Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="a2acc-106">Access Azure and Azure Active Directory</span></span>
<span data-ttu-id="a2acc-107">**問： 我為什麼收到 「 找到的任何訂用帳戶 」 當我嘗試 tooaccess Azure AD 中 hello Azure 傳統入口網站？**</span><span class="sxs-lookup"><span data-stu-id="a2acc-107">**Q: Why do I get “No subscriptions found” when I try tooaccess Azure AD in hello Azure classic portal?**</span></span>

<span data-ttu-id="a2acc-108">**答：** tooaccess hello Azure 傳統入口網站，每位使用者必須具備 Azure 訂用帳戶的權限。</span><span class="sxs-lookup"><span data-stu-id="a2acc-108">**A:** tooaccess hello Azure classic portal, each user needs permissions with an Azure subscription.</span></span> <span data-ttu-id="a2acc-109">如果您有 Office 365 或 Azure AD 的付費的訂閱，請移至太[http://aka.ms/accessAAD](http://aka.ms/accessAAD)一次性的啟用步驟。</span><span class="sxs-lookup"><span data-stu-id="a2acc-109">If you have a paid Office 365 or Azure AD subscription, go too[http://aka.ms/accessAAD](http://aka.ms/accessAAD) for a one-time activation step.</span></span> <span data-ttu-id="a2acc-110">否則，您將需要可用 tooactivate [Azure 帳戶](https://azure.microsoft.com/pricing/free-trial/)或付費的訂閱。</span><span class="sxs-lookup"><span data-stu-id="a2acc-110">Otherwise, you will need tooactivate a free [Azure account](https://azure.microsoft.com/pricing/free-trial/) or a paid subscription.</span></span>

<span data-ttu-id="a2acc-111">如需詳細資訊，請參閱：</span><span class="sxs-lookup"><span data-stu-id="a2acc-111">For more information, see:</span></span>

* [<span data-ttu-id="a2acc-112">Azure 訂用帳戶如何與 Azure Active Directory 產生關聯</span><span class="sxs-lookup"><span data-stu-id="a2acc-112">How Azure subscriptions are associated with Azure Active Directory</span></span>](active-directory-how-subscriptions-associated-directory.md)
* [<span data-ttu-id="a2acc-113">管理 Office 365 訂用帳戶在 Azure 中的 hello 目錄</span><span class="sxs-lookup"><span data-stu-id="a2acc-113">Manage hello directory for your Office 365 subscription in Azure</span></span>](active-directory-manage-o365-subscription.md)

- - -
<span data-ttu-id="a2acc-114">**問： 什麼是 Azure AD 中的 hello 關聯 Office 365 和 Azure？**</span><span class="sxs-lookup"><span data-stu-id="a2acc-114">**Q: What’s hello relationship between Azure AD, Office 365, and Azure?**</span></span>

<span data-ttu-id="a2acc-115">**答：** Azure AD 為您提供常見的身分識別和存取功能 tooall web 服務。</span><span class="sxs-lookup"><span data-stu-id="a2acc-115">**A:** Azure AD provides you with common identity and access capabilities tooall web services.</span></span> <span data-ttu-id="a2acc-116">不論您使用 Office 365、 Microsoft Azure，Intune，或其他人，您是已經在使用 Azure AD toohelp 開啟登入及存取管理所有這些服務。</span><span class="sxs-lookup"><span data-stu-id="a2acc-116">Whether you are using Office 365, Microsoft Azure, Intune, or others, you're already using Azure AD toohelp turn on sign-on and access management for all these services.</span></span>

<span data-ttu-id="a2acc-117">設定 toouse web 服務的所有使用者會都定義為一或多個 Azure AD 執行個體中的使用者帳戶。</span><span class="sxs-lookup"><span data-stu-id="a2acc-117">All users who are set up toouse web services are defined as user accounts in one or more Azure AD instances.</span></span> <span data-ttu-id="a2acc-118">您可以為這些帳戶設定免費的 Azure AD 功能，如雲端應用程式存取。</span><span class="sxs-lookup"><span data-stu-id="a2acc-118">You can set up these accounts for free Azure AD capabilities like cloud application access.</span></span>

<span data-ttu-id="a2acc-119">Azure AD 付費服務 (例如 Enterprise Mobility + Security) 可透過全方位的企業級管理和安全性解決方案來彌補其他 Web 服務 (例如 Office 365 和 Microsoft Azure) 的不足。</span><span class="sxs-lookup"><span data-stu-id="a2acc-119">Azure AD paid services like Enterprise Mobility + Security complement other web services like Office 365 and Microsoft Azure with comprehensive enterprise-scale management and security solutions.</span></span>
- - -
<span data-ttu-id="a2acc-120">**問： 為什麼登入 Azure 入口網站 toohello 但不是 hello Azure 傳統入口網站？**</span><span class="sxs-lookup"><span data-stu-id="a2acc-120">**Q:  Why can I sign in toohello Azure portal but not hello Azure classic portal?**</span></span>

<span data-ttu-id="a2acc-121">**答：** hello Azure 入口網站不需要有效的訂用帳戶，且 hello 傳統入口網站需要有效的訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="a2acc-121">**A:**  hello Azure portal does not require a valid subscription, and hello classic portal does require a valid subscription.</span></span>  <span data-ttu-id="a2acc-122">如果您沒有訂用帳戶，您無法登入 toohello 傳統入口網站。</span><span class="sxs-lookup"><span data-stu-id="a2acc-122">If you do not have a subscription, you can't sign in toohello classic portal.</span></span>
- - -
<span data-ttu-id="a2acc-123">**問： hello 訂用帳戶管理員與目錄管理員之間的差異為何？**</span><span class="sxs-lookup"><span data-stu-id="a2acc-123">**Q:  What are hello differences between Subscription Administrator and Directory Administrator?**</span></span>

<span data-ttu-id="a2acc-124">**答：**根據預設，您獲指派 hello 訂用帳戶管理員角色時登入 azure。</span><span class="sxs-lookup"><span data-stu-id="a2acc-124">**A:** By default, you are assigned hello Subscription Administrator role when you sign up for Azure.</span></span> <span data-ttu-id="a2acc-125">訂用帳戶管理員可以使用 Microsoft 帳戶或是工作或學校帳戶，從 hello Azure 訂用帳戶的 hello 目錄相關聯。</span><span class="sxs-lookup"><span data-stu-id="a2acc-125">A subscription admin can use either a Microsoft account or a work or school account from hello directory that hello Azure subscription is associated with.</span></span>  <span data-ttu-id="a2acc-126">這個角色是授權的 toomanage hello Azure 入口網站中的服務。</span><span class="sxs-lookup"><span data-stu-id="a2acc-126">This role is authorized toomanage services in hello Azure portal.</span></span>

<span data-ttu-id="a2acc-127">如果其他人在 toosign 以及存取服務所使用 hello 相同訂用帳戶，您可以將它們加入為共同管理員。</span><span class="sxs-lookup"><span data-stu-id="a2acc-127">If others need toosign in and access services by using hello same subscription, you can add them as co-admins.</span></span> <span data-ttu-id="a2acc-128">這個角色有 hello 相同身 hello 服務系統管理員存取權限，但無法變更 hello 關聯的訂用帳戶 tooAzure 目錄。</span><span class="sxs-lookup"><span data-stu-id="a2acc-128">This role has hello same access privileges as hello service admin, but can’t change hello association of subscriptions tooAzure directories.</span></span>  <span data-ttu-id="a2acc-129">如需有關訂用帳戶系統管理員 」 的詳細資訊，請參閱[如何 tooadd 或變更的 Azure 系統管理員角色](../billing-add-change-azure-subscription-administrator.md)和[如何 Azure 訂用帳戶相關聯 Azure Active Directory](active-directory-how-subscriptions-associated-directory.md)。</span><span class="sxs-lookup"><span data-stu-id="a2acc-129">For additional information on subscription admins, see [How tooadd or change Azure administrator roles](../billing-add-change-azure-subscription-administrator.md) and [How Azure subscriptions are associated with Azure Active Directory](active-directory-how-subscriptions-associated-directory.md).</span></span>


<span data-ttu-id="a2acc-130">Azure AD 有一組不同的系統管理員角色 toomanage hello 目錄和身分識別相關功能。</span><span class="sxs-lookup"><span data-stu-id="a2acc-130">Azure AD has a different set of admin roles toomanage hello directory and identity-related features.</span></span>  <span data-ttu-id="a2acc-131">這些系統管理員 」 將會在 hello Azure 入口網站存取 toovarious 功能或 hello Azure 傳統入口網站。</span><span class="sxs-lookup"><span data-stu-id="a2acc-131">These admins will have access toovarious features in hello Azure portal or hello Azure classic portal.</span></span> <span data-ttu-id="a2acc-132">hello 系統管理員角色會決定其功能，例如建立或編輯使用者、 指派系統管理角色 tooothers、 重設使用者密碼、 管理使用者授權或管理的網域。</span><span class="sxs-lookup"><span data-stu-id="a2acc-132">hello admin's role determines what they can do, like create or edit users, assign administrative roles tooothers, reset user passwords, manage user licenses, or manage domains.</span></span>  <span data-ttu-id="a2acc-133">如需有關 Azure AD 目錄管理員及其角色的詳細資訊，請參閱[在 Azure Active Directory 中指派系統管理員角色](active-directory-assign-admin-roles.md)。</span><span class="sxs-lookup"><span data-stu-id="a2acc-133">For additional information on Azure AD directory admins and their roles, see [Assigning administrator roles in Azure Active Directory](active-directory-assign-admin-roles.md).</span></span>

<span data-ttu-id="a2acc-134">此外﹐Azure AD 付費服務 (例如 Enterprise Mobility + Security) 可透過全方位的企業級管理和安全性解決方案來彌補其他 Web 服務 (例如 Office 365 和 Microsoft Azure) 的不足。</span><span class="sxs-lookup"><span data-stu-id="a2acc-134">Additionally, Azure AD paid services like Enterprise Mobility + Security complement other web services, such as Office 365 and Microsoft Azure, with comprehensive enterprise-scale management and security solutions.</span></span>

- - -
<span data-ttu-id="a2acc-135">**問︰是否有報告可顯示 Azure AD 使用者授權何時即將過期？**</span><span class="sxs-lookup"><span data-stu-id="a2acc-135">**Q: Is there a report that shows when my Azure AD user licenses will expire?**</span></span>

<span data-ttu-id="a2acc-136">**答：**否。</span><span class="sxs-lookup"><span data-stu-id="a2acc-136">**A:** No.</span></span>  <span data-ttu-id="a2acc-137">目前無法使用此功能。</span><span class="sxs-lookup"><span data-stu-id="a2acc-137">This is not currently available.</span></span>

- - -

## <a name="get-started-with-hybrid-azure-ad"></a><span data-ttu-id="a2acc-138">開始使用混合式 Azure AD</span><span class="sxs-lookup"><span data-stu-id="a2acc-138">Get started with Hybrid Azure AD</span></span>


<span data-ttu-id="a2acc-139">**問︰當我新增為共同作業人員時如何離開租用戶？**</span><span class="sxs-lookup"><span data-stu-id="a2acc-139">**Q: How do I leave a tenant when I am added as a collaborator?**</span></span>

<span data-ttu-id="a2acc-140">**答：**當您加入為共同作業者 tooanother 組織的租用戶時，您可以使用 hello 「 租用戶切換器 」 中 hello 上方右 tooswitch 租用戶之間。</span><span class="sxs-lookup"><span data-stu-id="a2acc-140">**A:** When you are added tooanother organization's tenant as a collaborator, you can use hello "tenant switcher" in hello upper right tooswitch between tenants.</span></span>  <span data-ttu-id="a2acc-141">目前沒有任何方式 tooleave hello 邀請組織，Microsoft 努力提供這項功能。</span><span class="sxs-lookup"><span data-stu-id="a2acc-141">Currently, there is no way tooleave hello inviting organization, and Microsoft is working on providing this functionality.</span></span>  <span data-ttu-id="a2acc-142">這項功能可用之前，您可以詢問 hello 邀請組織 tooremove 您從其租用戶。</span><span class="sxs-lookup"><span data-stu-id="a2acc-142">Until this feature is available, you can ask hello inviting organization tooremove you from their tenant.</span></span>
- - -
<span data-ttu-id="a2acc-143">**問： 如何連線我在內部部署目錄 tooAzure AD？**</span><span class="sxs-lookup"><span data-stu-id="a2acc-143">**Q: How can I connect my on-premises directory tooAzure AD?**</span></span>

<span data-ttu-id="a2acc-144">**答：**您可以使用 Azure AD Connect 連接您在內部部署目錄 tooAzure AD。</span><span class="sxs-lookup"><span data-stu-id="a2acc-144">**A:** You can connect your on-premises directory tooAzure AD by using Azure AD Connect.</span></span>

<span data-ttu-id="a2acc-145">如需詳細資訊，請參閱[整合內部部署身分識別與 Azure Active Directory](active-directory-aadconnect.md)。</span><span class="sxs-lookup"><span data-stu-id="a2acc-145">For more information, see [Integrating your on-premises identities with Azure Active Directory](active-directory-aadconnect.md).</span></span>

- - -
<span data-ttu-id="a2acc-146">**問︰如何設定內部部署目錄與雲端應用程式之間的 SSO？**</span><span class="sxs-lookup"><span data-stu-id="a2acc-146">**Q: How do I set up SSO between my on-premises directory and my cloud applications?**</span></span>

<span data-ttu-id="a2acc-147">**答：**您只需要單一登入 (SSO) 在內部部署目錄與 Azure AD 之間的 tooset。</span><span class="sxs-lookup"><span data-stu-id="a2acc-147">**A:** You only need tooset up single sign-on (SSO) between your on-premises directory and Azure AD.</span></span> <span data-ttu-id="a2acc-148">只要您透過 Azure AD 存取雲端應用程式，則 hello 服務自動磁碟機 toocorrectly 向其內部部署認證您的使用者。</span><span class="sxs-lookup"><span data-stu-id="a2acc-148">As long as you access your cloud applications through Azure AD, hello service automatically drives your users toocorrectly authenticate with their on-premises credentials.</span></span>

<span data-ttu-id="a2acc-149">透過同盟解決方案 (例如 Active Directory Federation Services (AD FS)) 或藉由設定密碼雜湊同步處理，就能輕鬆實現從內部部署實作 SSO。您可以使用 hello Azure AD Connect 設定精靈，輕鬆部署這兩個選項。</span><span class="sxs-lookup"><span data-stu-id="a2acc-149">Implementing SSO from on-premises can be easily achieved with federation solutions such as Active Directory Federation Services (AD FS), or by configuring password hash sync. You can easily deploy both options by using hello Azure AD Connect configuration wizard.</span></span>

<span data-ttu-id="a2acc-150">如需詳細資訊，請參閱[整合內部部署身分識別與 Azure Active Directory](active-directory-aadconnect.md)。</span><span class="sxs-lookup"><span data-stu-id="a2acc-150">For more information, see [Integrating your on-premises identities with Azure Active Directory](active-directory-aadconnect.md).</span></span>

- - -
<span data-ttu-id="a2acc-151">**問︰Azure AD 是否可為組織中的使用者提供自助入口網站？**</span><span class="sxs-lookup"><span data-stu-id="a2acc-151">**Q: Does Azure AD provide a self-service portal for users in my organization?**</span></span>

<span data-ttu-id="a2acc-152">**答：**是，Azure AD 為您提供 hello [Azure AD 存取面板](http://myapps.microsoft.com)自助使用者和應用程式的存取。</span><span class="sxs-lookup"><span data-stu-id="a2acc-152">**A:** Yes, Azure AD provides you with hello [Azure AD Access Panel](http://myapps.microsoft.com) for user self-service and application access.</span></span> <span data-ttu-id="a2acc-153">如果您是 Office 365 客戶，您可以找到 hello 的許多相同的功能在 hello Office 365 入口網站。</span><span class="sxs-lookup"><span data-stu-id="a2acc-153">If you are an Office 365 customer, you can find many of hello same capabilities in hello Office 365 portal.</span></span>

<span data-ttu-id="a2acc-154">如需詳細資訊，請參閱[簡介 toohello 存取面板](active-directory-saas-access-panel-introduction.md)。</span><span class="sxs-lookup"><span data-stu-id="a2acc-154">For more information, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

- - -
<span data-ttu-id="a2acc-155">**問︰Azure AD 是否會協助我管理內部部署基礎結構？**</span><span class="sxs-lookup"><span data-stu-id="a2acc-155">**Q: Does Azure AD help me manage my on-premises infrastructure?**</span></span>

<span data-ttu-id="a2acc-156">**答：** 是。</span><span class="sxs-lookup"><span data-stu-id="a2acc-156">**A:** Yes.</span></span> <span data-ttu-id="a2acc-157">hello Azure AD Premium edition 提供 Azure AD Connect Health。</span><span class="sxs-lookup"><span data-stu-id="a2acc-157">hello Azure AD Premium edition provides you with Azure AD Connect Health.</span></span> <span data-ttu-id="a2acc-158">Azure AD Connect Health 可協助您監視及了解您的內部部署身分識別基礎結構和 hello 同步處理服務。</span><span class="sxs-lookup"><span data-stu-id="a2acc-158">Azure AD Connect Health helps you monitor and gain insight into your on-premises identity infrastructure and hello synchronization services.</span></span>  

<span data-ttu-id="a2acc-159">如需詳細資訊，請參閱[監視您內部部署識別基礎結構和同步處理雲端中的服務 hello](active-directory-aadconnect-health.md)。</span><span class="sxs-lookup"><span data-stu-id="a2acc-159">For more information, see [Monitor your on-premises identity infrastructure and synchronization services in hello cloud](active-directory-aadconnect-health.md).</span></span>  

- - -
## <a name="password-management"></a><span data-ttu-id="a2acc-160">密碼管理</span><span class="sxs-lookup"><span data-stu-id="a2acc-160">Password management</span></span>
<span data-ttu-id="a2acc-161">**問︰是否可以使用 Azure AD 密碼回寫，但不使用密碼同步處理？（在此案例中，是它可能 toouse Azure AD 自助式密碼重設 (SSPR) 與 hello 雲端中的密碼回寫並儲存密碼嗎？）**</span><span class="sxs-lookup"><span data-stu-id="a2acc-161">**Q: Can I use Azure AD password write-back without password sync? (In this scenario, is it possible toouse Azure AD self-service password reset (SSPR) with password write-back and not store passwords in hello cloud?)**</span></span>

<span data-ttu-id="a2acc-162">**答：**您不需要 toosynchronize 您 Active Directory 密碼 tooAzure AD tooenable 回寫。</span><span class="sxs-lookup"><span data-stu-id="a2acc-162">**A:** You do not need toosynchronize your Active Directory passwords tooAzure AD tooenable write-back.</span></span> <span data-ttu-id="a2acc-163">在同盟環境中，Azure AD 單一登入 (SSO) 依賴 hello 在內部部署目錄 tooauthenticate hello 使用者。</span><span class="sxs-lookup"><span data-stu-id="a2acc-163">In a federated environment, Azure AD single sign-on (SSO) relies on hello on-premises directory tooauthenticate hello user.</span></span> <span data-ttu-id="a2acc-164">這種情況下不需要在 Azure AD 中追蹤 hello 在內部部署密碼 toobe。</span><span class="sxs-lookup"><span data-stu-id="a2acc-164">This scenario does not require hello on-premises password toobe tracked in Azure AD.</span></span>

- - -
<span data-ttu-id="a2acc-165">**問： 如何花費時間的回寫 tooActive Directory 內部部署密碼 toobe？**</span><span class="sxs-lookup"><span data-stu-id="a2acc-165">**Q: How long does it take for a password toobe written back tooActive Directory on-premises?**</span></span>

<span data-ttu-id="a2acc-166">**答：**密碼回寫會即時運作。</span><span class="sxs-lookup"><span data-stu-id="a2acc-166">**A:** Password write-back operates in real time.</span></span>

<span data-ttu-id="a2acc-167">如需詳細資訊，請參閱[開始使用密碼管理](active-directory-passwords-getting-started.md)。</span><span class="sxs-lookup"><span data-stu-id="a2acc-167">For more information, see [Getting started with password management](active-directory-passwords-getting-started.md).</span></span>

- - -
<span data-ttu-id="a2acc-168">**問︰是否可以搭配使用密碼回寫和由系統管理員管理的密碼？**</span><span class="sxs-lookup"><span data-stu-id="a2acc-168">**Q: Can I use password write-back with passwords that are managed by an admin?**</span></span>

<span data-ttu-id="a2acc-169">**答：**是，如果您有密碼回寫啟用時，系統管理員所執行的 hello 密碼作業被寫回 tooyour 在內部部署環境。</span><span class="sxs-lookup"><span data-stu-id="a2acc-169">**A:** Yes, if you have password write-back enabled, hello password operations performed by an admin are written back tooyour on-premises environment.</span></span>  

<span data-ttu-id="a2acc-170">如需詳細的解答 toopassword 相關的問題，請參閱[密碼管理常見問題集](active-directory-passwords-faq.md)。</span><span class="sxs-lookup"><span data-stu-id="a2acc-170">For more answers toopassword-related questions, see [Password management frequently asked questions](active-directory-passwords-faq.md).</span></span>
- - -
<span data-ttu-id="a2acc-171">**問： 如果我不記得我現有的 Office 365/Azure AD 密碼嘗試 toochange 我的密碼時，我可以做什麼？**</span><span class="sxs-lookup"><span data-stu-id="a2acc-171">**Q:  What can I do if I can't remember my existing Office 365/Azure AD password while trying toochange my password?**</span></span>

<span data-ttu-id="a2acc-172">**答︰**在這種情況下有幾種做法。</span><span class="sxs-lookup"><span data-stu-id="a2acc-172">**A:** For this type of situation, there are a couple of options.</span></span>  <span data-ttu-id="a2acc-173">使用自助式密碼重設 (SSPR) (如果可用的話)。</span><span class="sxs-lookup"><span data-stu-id="a2acc-173">Use self-service password reset (SSPR) if it's available.</span></span>  <span data-ttu-id="a2acc-174">SSPR 能否運作取決於其設定方式。</span><span class="sxs-lookup"><span data-stu-id="a2acc-174">Whether SSPR works depends on how it's configured.</span></span>  <span data-ttu-id="a2acc-175">如需詳細資訊，請參閱[方式沒有 hello 密碼重設入口網站工作](active-directory-passwords-best-practices.md)。</span><span class="sxs-lookup"><span data-stu-id="a2acc-175">For more information, see [How does hello password reset portal work](active-directory-passwords-best-practices.md).</span></span>

<span data-ttu-id="a2acc-176">針對 Office 365 使用者，您的系統管理員可以使用重設 hello 密碼 hello 中所述的步驟[重設使用者密碼](https://support.office.com/en-us/article/Admins-Reset-user-passwords-7A5D073B-7FAE-4AA5-8F96-9ECD041ABA9C?ui=en-US&rs=en-US&ad=US)。</span><span class="sxs-lookup"><span data-stu-id="a2acc-176">For Office 365 users, your admin can reset hello password by using hello steps outlined in [Reset user passwords](https://support.office.com/en-us/article/Admins-Reset-user-passwords-7A5D073B-7FAE-4AA5-8F96-9ECD041ABA9C?ui=en-US&rs=en-US&ad=US).</span></span>

<span data-ttu-id="a2acc-177">Azure AD 帳戶管理員可以重設密碼，利用 hello 下列其中一種：</span><span class="sxs-lookup"><span data-stu-id="a2acc-177">For Azure AD accounts, admins can reset passwords by using one of hello following:</span></span>

- [<span data-ttu-id="a2acc-178">重設 hello Azure 入口網站中的帳戶</span><span class="sxs-lookup"><span data-stu-id="a2acc-178">Reset accounts in hello Azure portal</span></span>](active-directory-users-reset-password-azure-portal.md)
- [<span data-ttu-id="a2acc-179">重設 hello 傳統入口網站中的帳戶</span><span class="sxs-lookup"><span data-stu-id="a2acc-179">Reset accounts in hello classic portal</span></span>](active-directory-create-users-reset-password.md)
- [<span data-ttu-id="a2acc-180">使用 PowerShell</span><span class="sxs-lookup"><span data-stu-id="a2acc-180">Using PowerShell</span></span>](/powershell/module/msonline/set-msoluserpassword?view=azureadps-1.0)


- - -
## <a name="security"></a><span data-ttu-id="a2acc-181">安全性</span><span class="sxs-lookup"><span data-stu-id="a2acc-181">Security</span></span>
<span data-ttu-id="a2acc-182">**問︰帳戶會在特定次數的嘗試失敗之後鎖定，或者是否使用更複雜的策略？**</span><span class="sxs-lookup"><span data-stu-id="a2acc-182">**Q: Are accounts locked after a specific number of failed attempts or is there a more sophisticated strategy used?**</span></span></br>
<span data-ttu-id="a2acc-183">我們會使用更複雜的策略 toolock 帳戶。</span><span class="sxs-lookup"><span data-stu-id="a2acc-183">We use a more sophisticated strategy toolock accounts.</span></span>  <span data-ttu-id="a2acc-184">這根據 hello IP hello 要求和 hello 輸入的密碼。</span><span class="sxs-lookup"><span data-stu-id="a2acc-184">This is based on hello IP of hello request and hello passwords entered.</span></span> <span data-ttu-id="a2acc-185">hello hello 鎖定持續時間也會增加根據 hello，則攻擊的可能性。</span><span class="sxs-lookup"><span data-stu-id="a2acc-185">hello duration of hello lockout also increases based on hello likelihood that it is an attack.</span></span>  

<span data-ttu-id="a2acc-186">**問： 特定 （一般） 密碼取得拒絕以 hello 訊息 '此密碼已使用的 toomany 次'，此參考 toopasswords hello 目前的 active directory 中使用嗎？**</span><span class="sxs-lookup"><span data-stu-id="a2acc-186">**Q:  Certain (common) passwords get rejected with hello messages ‘this password has been used toomany times’, does this refer toopasswords used in hello current active directory?**</span></span></br>
<span data-ttu-id="a2acc-187">這是指 toopasswords 全域通用，例如 「 密碼 」 的任何變數和"123456"。</span><span class="sxs-lookup"><span data-stu-id="a2acc-187">This refers toopasswords that are globally common, such as any variants of “Password” and “123456”.</span></span>

<span data-ttu-id="a2acc-188">**問︰來自可疑來源 (殭屍網路、Tor 端點) 的登入要求是否會在 B2C 租用戶中遭到封鎖，或者需要基本或進階版本租用戶？**</span><span class="sxs-lookup"><span data-stu-id="a2acc-188">**Q: Will a sign-in request from dubious sources (botnets, tor endpoint) be blocked in a B2C tenant or does this require a Basic or Premium edition tenant?**</span></span></br>
<span data-ttu-id="a2acc-189">我們沒有適用於所有 B2C 租用戶的閘道，可篩選要求並提供殭屍網路的一些防護功能。</span><span class="sxs-lookup"><span data-stu-id="a2acc-189">We do have a gateway that filters requests and provides some protection from botnets, and is applied for all B2C tenants.</span></span>

## <a name="application-access"></a><span data-ttu-id="a2acc-190">應用程式存取</span><span class="sxs-lookup"><span data-stu-id="a2acc-190">Application access</span></span>
<span data-ttu-id="a2acc-191">**問︰哪裡可以找到與 Azure AD 預先整合的應用程式及其功能的清單？**</span><span class="sxs-lookup"><span data-stu-id="a2acc-191">**Q: Where can I find a list of applications that are pre-integrated with Azure AD and their capabilities?**</span></span>

<span data-ttu-id="a2acc-192">**答：** Azure AD 擁有來自 Microsoft、應用程式服務提供者或協力廠商超過 2600 個預先整合的應用程式。</span><span class="sxs-lookup"><span data-stu-id="a2acc-192">**A:** Azure AD has more than 2,600 pre-integrated applications from Microsoft, application service providers, and partners.</span></span> <span data-ttu-id="a2acc-193">所有預先整合的應用程式皆支援單一登入 (SSO)。</span><span class="sxs-lookup"><span data-stu-id="a2acc-193">All pre-integrated applications support single sign-on (SSO).</span></span> <span data-ttu-id="a2acc-194">SSO 可讓您使用您的組織認證 tooaccess 應用程式。</span><span class="sxs-lookup"><span data-stu-id="a2acc-194">SSO lets you use your organizational credentials tooaccess your apps.</span></span> <span data-ttu-id="a2acc-195">某些 hello 應用程式也支援自動佈建和解除佈建。</span><span class="sxs-lookup"><span data-stu-id="a2acc-195">Some of hello applications also support automated provisioning and de-provisioning.</span></span>

<span data-ttu-id="a2acc-196">Hello 預先整合應用程式的完整清單，請參閱 hello [Active Directory Marketplace](https://azure.microsoft.com/marketplace/active-directory/)。</span><span class="sxs-lookup"><span data-stu-id="a2acc-196">For a complete list of hello pre-integrated applications, see hello [Active Directory Marketplace](https://azure.microsoft.com/marketplace/active-directory/).</span></span>

- - -
<span data-ttu-id="a2acc-197">**問： 如果 hello 我需要的應用程式不在 hello Azure AD 服務商場嗎？**</span><span class="sxs-lookup"><span data-stu-id="a2acc-197">**Q: What if hello application I need is not in hello Azure AD marketplace?**</span></span>

<span data-ttu-id="a2acc-198">**答：**若您使用 Azure AD Premium，就可以新增及設定您想要的任何應用程式。</span><span class="sxs-lookup"><span data-stu-id="a2acc-198">**A:** With Azure AD Premium, you can add and configure any application that you want.</span></span> <span data-ttu-id="a2acc-199">視應用程式功能和您的喜好設定而定，您可以設定 SSO 和自動化佈建。</span><span class="sxs-lookup"><span data-stu-id="a2acc-199">Depending on your application’s capabilities and your preferences, you can configure SSO and automated provisioning.</span></span>  

<span data-ttu-id="a2acc-200">如需詳細資訊，請參閱：</span><span class="sxs-lookup"><span data-stu-id="a2acc-200">For more information, see:</span></span>

* [<span data-ttu-id="a2acc-201">設定單一登入 tooapplications 不在 hello Azure Active Directory 應用程式庫</span><span class="sxs-lookup"><span data-stu-id="a2acc-201">Configuring single sign-on tooapplications that are not in hello Azure Active Directory application gallery</span></span>](active-directory-saas-custom-apps.md)
* [<span data-ttu-id="a2acc-202">使用 SCIM tooenable 自動佈建的 Azure Active Directory tooapplications 來自使用者和群組</span><span class="sxs-lookup"><span data-stu-id="a2acc-202">Using SCIM tooenable automatic provisioning of users and groups from Azure Active Directory tooapplications</span></span>](active-directory-scim-provisioning.md)

- - -
<span data-ttu-id="a2acc-203">**問： 如何使用者登入 tooapplications 使用 Azure AD？**</span><span class="sxs-lookup"><span data-stu-id="a2acc-203">**Q: How do users sign in tooapplications by using Azure AD?**</span></span>

<span data-ttu-id="a2acc-204">**答：** Azure AD 使用者 tooview 提供數種方式，並存取其應用程式，例如：</span><span class="sxs-lookup"><span data-stu-id="a2acc-204">**A:** Azure AD provides several ways for users tooview and access their applications, such as:</span></span>

* <span data-ttu-id="a2acc-205">hello Azure AD 存取面板</span><span class="sxs-lookup"><span data-stu-id="a2acc-205">hello Azure AD access panel</span></span>
* <span data-ttu-id="a2acc-206">hello Office 365 應用程式啟動器</span><span class="sxs-lookup"><span data-stu-id="a2acc-206">hello Office 365 application launcher</span></span>
* <span data-ttu-id="a2acc-207">直接登入 toofederated 應用程式</span><span class="sxs-lookup"><span data-stu-id="a2acc-207">Direct sign-in toofederated apps</span></span>
* <span data-ttu-id="a2acc-208">深層連結 toofederated，密碼為基礎或現有的應用程式</span><span class="sxs-lookup"><span data-stu-id="a2acc-208">Deep links toofederated, password-based, or existing apps</span></span>

<span data-ttu-id="a2acc-209">如需詳細資訊，請參閱[部署 Azure AD 整合的應用程式 toousers](active-directory-appssoaccess-whatis.md#deploying-azure-ad-integrated-applications-to-users)。</span><span class="sxs-lookup"><span data-stu-id="a2acc-209">For more information, see [Deploying Azure AD integrated applications toousers](active-directory-appssoaccess-whatis.md#deploying-azure-ad-integrated-applications-to-users).</span></span>

- - -
<span data-ttu-id="a2acc-210">**問： 什麼是 Azure AD hello 不同方式，可讓驗證和單一登入 tooapplications 嗎？**</span><span class="sxs-lookup"><span data-stu-id="a2acc-210">**Q: What are hello different ways Azure AD enables authentication and single sign-on tooapplications?**</span></span>

<span data-ttu-id="a2acc-211">**答：**Azure AD 針對驗證和授權支援許多標準化的通訊協定，例如 SAML 2.0、OpenID Connect、OAuth 2.0 和 WS-同盟。</span><span class="sxs-lookup"><span data-stu-id="a2acc-211">**A:** Azure AD supports many standardized protocols for authentication and authorization, such as SAML 2.0, OpenID Connect, OAuth 2.0, and WS-Federation.</span></span> <span data-ttu-id="a2acc-212">Azure AD 也可針對僅支援表單型驗證的應用程式，支援密碼存放和自動化登入功能。</span><span class="sxs-lookup"><span data-stu-id="a2acc-212">Azure AD also supports password vaulting and automated sign-in capabilities for apps that only support forms-based authentication.</span></span>  

<span data-ttu-id="a2acc-213">如需詳細資訊，請參閱：</span><span class="sxs-lookup"><span data-stu-id="a2acc-213">For more information, see:</span></span>

* [<span data-ttu-id="a2acc-214">Azure AD 的驗證案例</span><span class="sxs-lookup"><span data-stu-id="a2acc-214">Authentication Scenarios for Azure AD</span></span>](active-directory-authentication-scenarios.md)
* [<span data-ttu-id="a2acc-215">Active Directory 驗證通訊協定</span><span class="sxs-lookup"><span data-stu-id="a2acc-215">Active Directory authentication protocols</span></span>](https://msdn.microsoft.com/library/azure/dn151124.aspx)
* [<span data-ttu-id="a2acc-216">單一登入如何搭配 Azure Active Directory 運作？</span><span class="sxs-lookup"><span data-stu-id="a2acc-216">How does single sign-on with Azure Active Directory work?</span></span>](active-directory-appssoaccess-whatis.md#how-does-single-sign-on-with-azure-active-directory-work)

- - -
<span data-ttu-id="a2acc-217">**問︰是否可以新增在內部部署中執行的應用程式？**</span><span class="sxs-lookup"><span data-stu-id="a2acc-217">**Q: Can I add applications I’m running on-premises?**</span></span>

<span data-ttu-id="a2acc-218">**答：** Azure AD Application Proxy 可讓您輕鬆且安全存取您選擇的 tooon 內部部署 web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="a2acc-218">**A:** Azure AD Application Proxy provides you with easy and secure access tooon-premises web applications that you choose.</span></span> <span data-ttu-id="a2acc-219">您可以存取這些應用程式在 hello 做為服務 (SaaS) 應用程式存取您的軟體，在 Azure AD 中的方式相同。</span><span class="sxs-lookup"><span data-stu-id="a2acc-219">You can access these applications in hello same way that you access your software as a service (SaaS) apps in Azure AD.</span></span> <span data-ttu-id="a2acc-220">沒有需要 VPN 或 toochange 網路基礎結構。</span><span class="sxs-lookup"><span data-stu-id="a2acc-220">There is no need for a VPN or toochange your network infrastructure.</span></span>  

<span data-ttu-id="a2acc-221">如需詳細資訊，請參閱[如何 tooprovide 安全的遠端存取 tooon 內部部署應用程式](active-directory-application-proxy-get-started.md)。</span><span class="sxs-lookup"><span data-stu-id="a2acc-221">For more information, see [How tooprovide secure remote access tooon-premises applications](active-directory-application-proxy-get-started.md).</span></span>

- - -
<span data-ttu-id="a2acc-222">**問︰如何對存取特定應用程式的使用者要求 Multi-Factor Authentication？**</span><span class="sxs-lookup"><span data-stu-id="a2acc-222">**Q: How do I require multi-factor authentication for users who access a particular application?**</span></span>

<span data-ttu-id="a2acc-223">**答：** Azure AD 條件式存取可讓您針對每個應用程式指派唯一的存取原則。</span><span class="sxs-lookup"><span data-stu-id="a2acc-223">**A:** With Azure AD conditional access, you can assign a unique access policy for each application.</span></span> <span data-ttu-id="a2acc-224">在您的原則，您可以進行多重要素驗證一律，或當使用者不屬於連接的 toohello 區域網路。</span><span class="sxs-lookup"><span data-stu-id="a2acc-224">In your policy, you can require multi-factor authentication always, or when users are not connected toohello local network.</span></span>  

<span data-ttu-id="a2acc-225">如需詳細資訊，請參閱[tooOffice 365 和其他應用程式保護的存取連接 tooAzure Active Directory](active-directory-conditional-access.md)。</span><span class="sxs-lookup"><span data-stu-id="a2acc-225">For more information, see [Securing access tooOffice 365 and other apps connected tooAzure Active Directory](active-directory-conditional-access.md).</span></span>

- - -
<span data-ttu-id="a2acc-226">**問︰SaaS 應用程式的自動化使用者佈建是什麼？**</span><span class="sxs-lookup"><span data-stu-id="a2acc-226">**Q: What is automated user provisioning for SaaS apps?**</span></span>

<span data-ttu-id="a2acc-227">**答：**使用 Azure AD tooautomate hello 建立、 維護和移除許多熱門的雲端 SaaS 應用程式中的使用者識別。</span><span class="sxs-lookup"><span data-stu-id="a2acc-227">**A:** Use Azure AD tooautomate hello creation, maintenance, and removal of user identities in many popular cloud SaaS apps.</span></span>

<span data-ttu-id="a2acc-228">如需詳細資訊，請參閱[自動化使用者佈建和解除佈建 tooSaaS 應用程式與 Azure Active Directory](active-directory-saas-app-provisioning.md)。</span><span class="sxs-lookup"><span data-stu-id="a2acc-228">For more information, see [Automate user provisioning and deprovisioning tooSaaS applications with Azure Active Directory](active-directory-saas-app-provisioning.md).</span></span>

- - -
<span data-ttu-id="a2acc-229">**問︰是否可以設定與 Azure AD 之間的安全 LDAP 連線？**</span><span class="sxs-lookup"><span data-stu-id="a2acc-229">**Q:  Can I set up a secure LDAP connection with Azure AD?**</span></span>

<span data-ttu-id="a2acc-230">**答：**否。</span><span class="sxs-lookup"><span data-stu-id="a2acc-230">**A:**  No.</span></span> <span data-ttu-id="a2acc-231">Azure AD 不支援 hello LDAP 通訊協定。</span><span class="sxs-lookup"><span data-stu-id="a2acc-231">Azure AD does not support hello LDAP protocol.</span></span>
