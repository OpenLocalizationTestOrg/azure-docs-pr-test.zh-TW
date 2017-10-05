---
title: "Azure Active Directory 常見問題集 | Microsoft Docs"
description: "Azure Active Directory 常見問題集可回答如何存取 Azure 及 Azure Active Directory、密碼管理和應用程式存取權等相關問題。"
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
ms.openlocfilehash: 8d4460b3059558de2253c6f6a2d2fc8e7564d6d9
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/18/2017
---
# <a name="azure-active-directory-faq"></a><span data-ttu-id="99320-103">Azure Active Directory 常見問題集</span><span class="sxs-lookup"><span data-stu-id="99320-103">Azure Active Directory FAQ</span></span>
<span data-ttu-id="99320-104">Azure Active Directory (Azure AD) 是全方位的身分識別即服務 (IDaaS) 解決方案，其涉及範圍橫跨身分識別、存取管理和安全性的所有層面。</span><span class="sxs-lookup"><span data-stu-id="99320-104">Azure Active Directory (Azure AD) is a comprehensive identity as a service (IDaaS) solution that spans all aspects of identity, access management, and security.</span></span>

<span data-ttu-id="99320-105">如需詳細資訊，請參閱[什麼是 Azure Active Directory？](active-directory-whatis.md)。</span><span class="sxs-lookup"><span data-stu-id="99320-105">For more information, see [What is Azure Active Directory?](active-directory-whatis.md).</span></span>


## <a name="access-azure-and-azure-active-directory"></a><span data-ttu-id="99320-106">存取 Azure 和 Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="99320-106">Access Azure and Azure Active Directory</span></span>
<span data-ttu-id="99320-107">**問︰當我嘗試在 Azure 傳統入口網站中存取 Azure AD，為何會收到「找不到訂用帳戶」？**</span><span class="sxs-lookup"><span data-stu-id="99320-107">**Q: Why do I get “No subscriptions found” when I try to access Azure AD in the Azure classic portal?**</span></span>

<span data-ttu-id="99320-108">**答：**若要存取 Azure 傳統入口網站，每位使用者都必須擁有 Azure 訂用帳戶的權限。</span><span class="sxs-lookup"><span data-stu-id="99320-108">**A:** To access the Azure classic portal, each user needs permissions with an Azure subscription.</span></span> <span data-ttu-id="99320-109">如果您有付費的 Office 365 或 Azure AD 訂用帳戶，請移至 [http://aka.ms/accessAAD](http://aka.ms/accessAAD) 以進行一次性啟用步驟。</span><span class="sxs-lookup"><span data-stu-id="99320-109">If you have a paid Office 365 or Azure AD subscription, go to [http://aka.ms/accessAAD](http://aka.ms/accessAAD) for a one-time activation step.</span></span> <span data-ttu-id="99320-110">否則，您必須啟用免費 [Azure 帳戶](https://azure.microsoft.com/pricing/free-trial/)或付費的訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="99320-110">Otherwise, you will need to activate a free [Azure account](https://azure.microsoft.com/pricing/free-trial/) or a paid subscription.</span></span>

<span data-ttu-id="99320-111">如需詳細資訊，請參閱：</span><span class="sxs-lookup"><span data-stu-id="99320-111">For more information, see:</span></span>

* [<span data-ttu-id="99320-112">Azure 訂用帳戶如何與 Azure Active Directory 產生關聯</span><span class="sxs-lookup"><span data-stu-id="99320-112">How Azure subscriptions are associated with Azure Active Directory</span></span>](active-directory-how-subscriptions-associated-directory.md)
* [<span data-ttu-id="99320-113">在 Azure 中管理 Office 365 訂用帳戶的目錄</span><span class="sxs-lookup"><span data-stu-id="99320-113">Manage the directory for your Office 365 subscription in Azure</span></span>](active-directory-manage-o365-subscription.md)

- - -
<span data-ttu-id="99320-114">**問︰Azure AD、Office 365 和 Azure 之間有何關聯性？**</span><span class="sxs-lookup"><span data-stu-id="99320-114">**Q: What’s the relationship between Azure AD, Office 365, and Azure?**</span></span>

<span data-ttu-id="99320-115">**答：**Azure AD 可提供您所有 Web 服務的常見身分識別和存取功能。</span><span class="sxs-lookup"><span data-stu-id="99320-115">**A:** Azure AD provides you with common identity and access capabilities to all web services.</span></span> <span data-ttu-id="99320-116">無論您是使用 Office 365、Microsoft Azure、Intune 或其他服務，您都已是使用 Azure AD 協助上述所有服務的登入和存取管理功能。</span><span class="sxs-lookup"><span data-stu-id="99320-116">Whether you are using Office 365, Microsoft Azure, Intune, or others, you're already using Azure AD to help turn on sign-on and access management for all these services.</span></span>

<span data-ttu-id="99320-117">所有設定要使用 Web 服務的使用者都會定義為一或多個 Azure AD 執行個體中的使用者帳戶。</span><span class="sxs-lookup"><span data-stu-id="99320-117">All users who are set up to use web services are defined as user accounts in one or more Azure AD instances.</span></span> <span data-ttu-id="99320-118">您可以為這些帳戶設定免費的 Azure AD 功能，如雲端應用程式存取。</span><span class="sxs-lookup"><span data-stu-id="99320-118">You can set up these accounts for free Azure AD capabilities like cloud application access.</span></span>

<span data-ttu-id="99320-119">Azure AD 付費服務 (例如 Enterprise Mobility + Security) 可透過全方位的企業級管理和安全性解決方案來彌補其他 Web 服務 (例如 Office 365 和 Microsoft Azure) 的不足。</span><span class="sxs-lookup"><span data-stu-id="99320-119">Azure AD paid services like Enterprise Mobility + Security complement other web services like Office 365 and Microsoft Azure with comprehensive enterprise-scale management and security solutions.</span></span>
- - -
<span data-ttu-id="99320-120">**問︰我為何可以登入 Azure 入口網站，但無法登入 Azure 傳統入口網站？**</span><span class="sxs-lookup"><span data-stu-id="99320-120">**Q:  Why can I sign in to the Azure portal but not the Azure classic portal?**</span></span>

<span data-ttu-id="99320-121">**答︰**Azure 入口網站不需要有效的訂用帳戶，而傳統入口網站則需要有效的訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="99320-121">**A:**  The Azure portal does not require a valid subscription, and the classic portal does require a valid subscription.</span></span>  <span data-ttu-id="99320-122">如果您沒有訂用帳戶，您便無法登入傳統入口網站。</span><span class="sxs-lookup"><span data-stu-id="99320-122">If you do not have a subscription, you can't sign in to the classic portal.</span></span>
- - -
<span data-ttu-id="99320-123">**問︰訂用帳戶管理員和目錄管理員有何差異？**</span><span class="sxs-lookup"><span data-stu-id="99320-123">**Q:  What are the differences between Subscription Administrator and Directory Administrator?**</span></span>

<span data-ttu-id="99320-124">**問：**根據預設，當您註冊 Azure 時會指派訂用帳戶管理員角色給您。</span><span class="sxs-lookup"><span data-stu-id="99320-124">**A:** By default, you are assigned the Subscription Administrator role when you sign up for Azure.</span></span> <span data-ttu-id="99320-125">訂用帳戶管理員可以使用 Azure 訂用帳戶相關聯目錄中的 Microsoft 帳戶或是公司或學校帳戶。</span><span class="sxs-lookup"><span data-stu-id="99320-125">A subscription admin can use either a Microsoft account or a work or school account from the directory that the Azure subscription is associated with.</span></span>  <span data-ttu-id="99320-126">此角色經過授權，可管理 Azure 入口網站上的服務。</span><span class="sxs-lookup"><span data-stu-id="99320-126">This role is authorized to manage services in the Azure portal.</span></span>

<span data-ttu-id="99320-127">如果其他人必須使用相同的訂用帳戶來登入和存取服務，您可以將他們新增為共同管理員。</span><span class="sxs-lookup"><span data-stu-id="99320-127">If others need to sign in and access services by using the same subscription, you can add them as co-admins.</span></span> <span data-ttu-id="99320-128">此角色的存取權限與服務管理員相同，但無法變更訂用帳戶與 Azure 目錄的關聯。</span><span class="sxs-lookup"><span data-stu-id="99320-128">This role has the same access privileges as the service admin, but can’t change the association of subscriptions to Azure directories.</span></span>  <span data-ttu-id="99320-129">如需訂用帳戶管理員的詳細資訊，請參閱[如何新增或變更 Azure 系統管理員角色](../billing-add-change-azure-subscription-administrator.md)和 [Azure 訂用帳戶如何與 Azure Active Directory 產生關聯](active-directory-how-subscriptions-associated-directory.md)。</span><span class="sxs-lookup"><span data-stu-id="99320-129">For additional information on subscription admins, see [How to add or change Azure administrator roles](../billing-add-change-azure-subscription-administrator.md) and [How Azure subscriptions are associated with Azure Active Directory](active-directory-how-subscriptions-associated-directory.md).</span></span>


<span data-ttu-id="99320-130">Azure AD 有一組不同的系統管理角色，可用來管理目錄和識別相關功能。</span><span class="sxs-lookup"><span data-stu-id="99320-130">Azure AD has a different set of admin roles to manage the directory and identity-related features.</span></span>  <span data-ttu-id="99320-131">這些管理員將可存取 Azure 入口網站或 Azure 傳統入口網站中的各種功能。</span><span class="sxs-lookup"><span data-stu-id="99320-131">These admins will have access to various features in the Azure portal or the Azure classic portal.</span></span> <span data-ttu-id="99320-132">系統管理員的角色可決定他們可以執行的作業，例如建立或編輯使用者、將系統管理角色指派給其他人、重設使用者密碼、管理使用者授權或管理網域。</span><span class="sxs-lookup"><span data-stu-id="99320-132">The admin's role determines what they can do, like create or edit users, assign administrative roles to others, reset user passwords, manage user licenses, or manage domains.</span></span>  <span data-ttu-id="99320-133">如需有關 Azure AD 目錄管理員及其角色的詳細資訊，請參閱[在 Azure Active Directory 中指派系統管理員角色](active-directory-assign-admin-roles.md)。</span><span class="sxs-lookup"><span data-stu-id="99320-133">For additional information on Azure AD directory admins and their roles, see [Assigning administrator roles in Azure Active Directory](active-directory-assign-admin-roles.md).</span></span>

<span data-ttu-id="99320-134">此外﹐Azure AD 付費服務 (例如 Enterprise Mobility + Security) 可透過全方位的企業級管理和安全性解決方案來彌補其他 Web 服務 (例如 Office 365 和 Microsoft Azure) 的不足。</span><span class="sxs-lookup"><span data-stu-id="99320-134">Additionally, Azure AD paid services like Enterprise Mobility + Security complement other web services, such as Office 365 and Microsoft Azure, with comprehensive enterprise-scale management and security solutions.</span></span>

- - -
<span data-ttu-id="99320-135">**問︰是否有報告可顯示 Azure AD 使用者授權何時即將過期？**</span><span class="sxs-lookup"><span data-stu-id="99320-135">**Q: Is there a report that shows when my Azure AD user licenses will expire?**</span></span>

<span data-ttu-id="99320-136">**答：**否。</span><span class="sxs-lookup"><span data-stu-id="99320-136">**A:** No.</span></span>  <span data-ttu-id="99320-137">目前無法使用此功能。</span><span class="sxs-lookup"><span data-stu-id="99320-137">This is not currently available.</span></span>

- - -

## <a name="get-started-with-hybrid-azure-ad"></a><span data-ttu-id="99320-138">開始使用混合式 Azure AD</span><span class="sxs-lookup"><span data-stu-id="99320-138">Get started with Hybrid Azure AD</span></span>


<span data-ttu-id="99320-139">**問︰當我新增為共同作業人員時如何離開租用戶？**</span><span class="sxs-lookup"><span data-stu-id="99320-139">**Q: How do I leave a tenant when I am added as a collaborator?**</span></span>

<span data-ttu-id="99320-140">**答︰**當您新增為另一個組織租用戶的共同作業人員時，您可以使用右上方的「租用戶切換器」來切換租用戶。</span><span class="sxs-lookup"><span data-stu-id="99320-140">**A:** When you are added to another organization's tenant as a collaborator, you can use the "tenant switcher" in the upper right to switch between tenants.</span></span>  <span data-ttu-id="99320-141">目前沒有任何方法可離開邀請組織，Microsoft 正在努力提供此功能。</span><span class="sxs-lookup"><span data-stu-id="99320-141">Currently, there is no way to leave the inviting organization, and Microsoft is working on providing this functionality.</span></span>  <span data-ttu-id="99320-142">在這項功能可用之前，您可以要求邀請組織將您從其租用戶中移除。</span><span class="sxs-lookup"><span data-stu-id="99320-142">Until this feature is available, you can ask the inviting organization to remove you from their tenant.</span></span>
- - -
<span data-ttu-id="99320-143">**問︰如何將內部部署目錄連接至 Azure AD？**</span><span class="sxs-lookup"><span data-stu-id="99320-143">**Q: How can I connect my on-premises directory to Azure AD?**</span></span>

<span data-ttu-id="99320-144">**答︰**您可以使用 Azure AD Connect 將內部部署目錄連接至 Azure AD。</span><span class="sxs-lookup"><span data-stu-id="99320-144">**A:** You can connect your on-premises directory to Azure AD by using Azure AD Connect.</span></span>

<span data-ttu-id="99320-145">如需詳細資訊，請參閱[整合內部部署身分識別與 Azure Active Directory](active-directory-aadconnect.md)。</span><span class="sxs-lookup"><span data-stu-id="99320-145">For more information, see [Integrating your on-premises identities with Azure Active Directory](active-directory-aadconnect.md).</span></span>

- - -
<span data-ttu-id="99320-146">**問︰如何設定內部部署目錄與雲端應用程式之間的 SSO？**</span><span class="sxs-lookup"><span data-stu-id="99320-146">**Q: How do I set up SSO between my on-premises directory and my cloud applications?**</span></span>

<span data-ttu-id="99320-147">**答：**您只需要在內部部署目錄與 Azure AD 之間設定單一登入 (SSO)。</span><span class="sxs-lookup"><span data-stu-id="99320-147">**A:** You only need to set up single sign-on (SSO) between your on-premises directory and Azure AD.</span></span> <span data-ttu-id="99320-148">只要您透過 Azure AD 存取雲端應用程式，該服務就會自動讓使用者使用其內部部署認證正確地進行驗證。</span><span class="sxs-lookup"><span data-stu-id="99320-148">As long as you access your cloud applications through Azure AD, the service automatically drives your users to correctly authenticate with their on-premises credentials.</span></span>

<span data-ttu-id="99320-149">透過同盟解決方案 (例如 Active Directory Federation Services (AD FS)) 或藉由設定密碼雜湊同步處理，就能輕鬆實現從內部部署實作 SSO。您可以使用 Azure AD Connect 組態精靈輕鬆部署這兩個選項。</span><span class="sxs-lookup"><span data-stu-id="99320-149">Implementing SSO from on-premises can be easily achieved with federation solutions such as Active Directory Federation Services (AD FS), or by configuring password hash sync. You can easily deploy both options by using the Azure AD Connect configuration wizard.</span></span>

<span data-ttu-id="99320-150">如需詳細資訊，請參閱[整合內部部署身分識別與 Azure Active Directory](active-directory-aadconnect.md)。</span><span class="sxs-lookup"><span data-stu-id="99320-150">For more information, see [Integrating your on-premises identities with Azure Active Directory](active-directory-aadconnect.md).</span></span>

- - -
<span data-ttu-id="99320-151">**問︰Azure AD 是否可為組織中的使用者提供自助入口網站？**</span><span class="sxs-lookup"><span data-stu-id="99320-151">**Q: Does Azure AD provide a self-service portal for users in my organization?**</span></span>

<span data-ttu-id="99320-152">**答：** 是，Azure AD 可提供您 [Azure AD 存取面板](http://myapps.microsoft.com) ，以供使用者進行自助服務和應用程式存取。</span><span class="sxs-lookup"><span data-stu-id="99320-152">**A:** Yes, Azure AD provides you with the [Azure AD Access Panel](http://myapps.microsoft.com) for user self-service and application access.</span></span> <span data-ttu-id="99320-153">如果您是 Office 365 客戶，您可以在 Office 365 入口網站中找到許多相同的功能。</span><span class="sxs-lookup"><span data-stu-id="99320-153">If you are an Office 365 customer, you can find many of the same capabilities in the Office 365 portal.</span></span>

<span data-ttu-id="99320-154">如需詳細資訊，請參閱[存取面板簡介](active-directory-saas-access-panel-introduction.md)。</span><span class="sxs-lookup"><span data-stu-id="99320-154">For more information, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

- - -
<span data-ttu-id="99320-155">**問︰Azure AD 是否會協助我管理內部部署基礎結構？**</span><span class="sxs-lookup"><span data-stu-id="99320-155">**Q: Does Azure AD help me manage my on-premises infrastructure?**</span></span>

<span data-ttu-id="99320-156">**答：** 是。</span><span class="sxs-lookup"><span data-stu-id="99320-156">**A:** Yes.</span></span> <span data-ttu-id="99320-157">Azure AD Premium Edition 可為您提供 Azure AD Connect Health。</span><span class="sxs-lookup"><span data-stu-id="99320-157">The Azure AD Premium edition provides you with Azure AD Connect Health.</span></span> <span data-ttu-id="99320-158">Azure AD Connect Health 可協助您監視和了解內部部署身分識別基礎結構和同步處理服務。</span><span class="sxs-lookup"><span data-stu-id="99320-158">Azure AD Connect Health helps you monitor and gain insight into your on-premises identity infrastructure and the synchronization services.</span></span>  

<span data-ttu-id="99320-159">如需詳細資訊，請參閱[在雲端中監視內部部署身分識別基礎結構和同步處理服務](active-directory-aadconnect-health.md)。</span><span class="sxs-lookup"><span data-stu-id="99320-159">For more information, see [Monitor your on-premises identity infrastructure and synchronization services in the cloud](active-directory-aadconnect-health.md).</span></span>  

- - -
## <a name="password-management"></a><span data-ttu-id="99320-160">密碼管理</span><span class="sxs-lookup"><span data-stu-id="99320-160">Password management</span></span>
<span data-ttu-id="99320-161">**問︰是否可以使用 Azure AD 密碼回寫，但不使用密碼同步處理？(在此案例中，可以搭配使用 Azure AD 自助式密碼重設 (SSPR) 和密碼回寫，而不在雲端儲存密碼嗎？)**</span><span class="sxs-lookup"><span data-stu-id="99320-161">**Q: Can I use Azure AD password write-back without password sync? (In this scenario, is it possible to use Azure AD self-service password reset (SSPR) with password write-back and not store passwords in the cloud?)**</span></span>

<span data-ttu-id="99320-162">**答：**想要啟用回寫功能，並不需要將 Active Directory 密碼同步處理至 Azure AD。</span><span class="sxs-lookup"><span data-stu-id="99320-162">**A:** You do not need to synchronize your Active Directory passwords to Azure AD to enable write-back.</span></span> <span data-ttu-id="99320-163">在同盟環境中，Azure AD 單一登入 (SSO) 會依靠內部部署目錄來驗證使用者。</span><span class="sxs-lookup"><span data-stu-id="99320-163">In a federated environment, Azure AD single sign-on (SSO) relies on the on-premises directory to authenticate the user.</span></span> <span data-ttu-id="99320-164">在這種情況下，並不需要在 Azure AD 中追蹤內部部署密碼。</span><span class="sxs-lookup"><span data-stu-id="99320-164">This scenario does not require the on-premises password to be tracked in Azure AD.</span></span>

- - -
<span data-ttu-id="99320-165">**問︰需要多久時間才能將密碼回寫至 Active Directory 內部部署？**</span><span class="sxs-lookup"><span data-stu-id="99320-165">**Q: How long does it take for a password to be written back to Active Directory on-premises?**</span></span>

<span data-ttu-id="99320-166">**答：**密碼回寫會即時運作。</span><span class="sxs-lookup"><span data-stu-id="99320-166">**A:** Password write-back operates in real time.</span></span>

<span data-ttu-id="99320-167">如需詳細資訊，請參閱[開始使用密碼管理](active-directory-passwords-getting-started.md)。</span><span class="sxs-lookup"><span data-stu-id="99320-167">For more information, see [Getting started with password management](active-directory-passwords-getting-started.md).</span></span>

- - -
<span data-ttu-id="99320-168">**問︰是否可以搭配使用密碼回寫和由系統管理員管理的密碼？**</span><span class="sxs-lookup"><span data-stu-id="99320-168">**Q: Can I use password write-back with passwords that are managed by an admin?**</span></span>

<span data-ttu-id="99320-169">**答：** 是，如果您已啟用密碼回寫，系統管理員所執行的密碼作業便會回寫到內部部署環境。</span><span class="sxs-lookup"><span data-stu-id="99320-169">**A:** Yes, if you have password write-back enabled, the password operations performed by an admin are written back to your on-premises environment.</span></span>  

<span data-ttu-id="99320-170">如需密碼相關問題的詳細解答，請參閱[密碼管理常見問題集](active-directory-passwords-faq.md)。</span><span class="sxs-lookup"><span data-stu-id="99320-170">For more answers to password-related questions, see [Password management frequently asked questions](active-directory-passwords-faq.md).</span></span>
- - -
<span data-ttu-id="99320-171">**問︰如果我在嘗試變更密碼時不記得現有的 Office 365/Azure AD 密碼，我可以做什麼？**</span><span class="sxs-lookup"><span data-stu-id="99320-171">**Q:  What can I do if I can't remember my existing Office 365/Azure AD password while trying to change my password?**</span></span>

<span data-ttu-id="99320-172">**答︰**在這種情況下有幾種做法。</span><span class="sxs-lookup"><span data-stu-id="99320-172">**A:** For this type of situation, there are a couple of options.</span></span>  <span data-ttu-id="99320-173">使用自助式密碼重設 (SSPR) (如果可用的話)。</span><span class="sxs-lookup"><span data-stu-id="99320-173">Use self-service password reset (SSPR) if it's available.</span></span>  <span data-ttu-id="99320-174">SSPR 能否運作取決於其設定方式。</span><span class="sxs-lookup"><span data-stu-id="99320-174">Whether SSPR works depends on how it's configured.</span></span>  <span data-ttu-id="99320-175">如需詳細資訊，請參閱[密碼重設入口網站的運作方式](active-directory-passwords-best-practices.md)。</span><span class="sxs-lookup"><span data-stu-id="99320-175">For more information, see [How does the password reset portal work](active-directory-passwords-best-practices.md).</span></span>

<span data-ttu-id="99320-176">對於 Office 365 使用者，您的系統管理員可以使用[重設使用者密碼](https://support.office.com/en-us/article/Admins-Reset-user-passwords-7A5D073B-7FAE-4AA5-8F96-9ECD041ABA9C?ui=en-US&rs=en-US&ad=US)所述的步驟重設密碼。</span><span class="sxs-lookup"><span data-stu-id="99320-176">For Office 365 users, your admin can reset the password by using the steps outlined in [Reset user passwords](https://support.office.com/en-us/article/Admins-Reset-user-passwords-7A5D073B-7FAE-4AA5-8F96-9ECD041ABA9C?ui=en-US&rs=en-US&ad=US).</span></span>

<span data-ttu-id="99320-177">對於 Azure AD 帳戶，系統管理員可以使用下列其中一種方法重設密碼︰</span><span class="sxs-lookup"><span data-stu-id="99320-177">For Azure AD accounts, admins can reset passwords by using one of the following:</span></span>

- [<span data-ttu-id="99320-178">在 Azure 入口網站重設帳戶</span><span class="sxs-lookup"><span data-stu-id="99320-178">Reset accounts in the Azure portal</span></span>](active-directory-users-reset-password-azure-portal.md)
- [<span data-ttu-id="99320-179">在傳統入口網站重設帳戶</span><span class="sxs-lookup"><span data-stu-id="99320-179">Reset accounts in the classic portal</span></span>](active-directory-create-users-reset-password.md)
- [<span data-ttu-id="99320-180">使用 PowerShell</span><span class="sxs-lookup"><span data-stu-id="99320-180">Using PowerShell</span></span>](/powershell/module/msonline/set-msoluserpassword?view=azureadps-1.0)


- - -
## <a name="security"></a><span data-ttu-id="99320-181">安全性</span><span class="sxs-lookup"><span data-stu-id="99320-181">Security</span></span>
<span data-ttu-id="99320-182">**問︰帳戶會在特定次數的嘗試失敗之後鎖定，或者是否使用更複雜的策略？**</span><span class="sxs-lookup"><span data-stu-id="99320-182">**Q: Are accounts locked after a specific number of failed attempts or is there a more sophisticated strategy used?**</span></span></br>
<span data-ttu-id="99320-183">我們使用更複雜的策略來鎖定帳戶。</span><span class="sxs-lookup"><span data-stu-id="99320-183">We use a more sophisticated strategy to lock accounts.</span></span>  <span data-ttu-id="99320-184">此策略是以要求的 IP 和所輸入的密碼為基礎。</span><span class="sxs-lookup"><span data-stu-id="99320-184">This is based on the IP of the request and the passwords entered.</span></span> <span data-ttu-id="99320-185">鎖定持續期間也會根據它是攻擊的可能性而加長。</span><span class="sxs-lookup"><span data-stu-id="99320-185">The duration of the lockout also increases based on the likelihood that it is an attack.</span></span>  

<span data-ttu-id="99320-186">**問︰有些 (通用) 密碼遭到拒絕並出現「此密碼已使用許多次」訊息，這是指使用於目前 Active Directory 的密碼嗎？**</span><span class="sxs-lookup"><span data-stu-id="99320-186">**Q:  Certain (common) passwords get rejected with the messages ‘this password has been used to many times’, does this refer to passwords used in the current active directory?**</span></span></br>
<span data-ttu-id="99320-187">這是指全域通用的密碼，例如 “Password” 和 “123456” 的任何變體。</span><span class="sxs-lookup"><span data-stu-id="99320-187">This refers to passwords that are globally common, such as any variants of “Password” and “123456”.</span></span>

<span data-ttu-id="99320-188">**問︰來自可疑來源 (殭屍網路、Tor 端點) 的登入要求是否會在 B2C 租用戶中遭到封鎖，或者需要基本或進階版本租用戶？**</span><span class="sxs-lookup"><span data-stu-id="99320-188">**Q: Will a sign-in request from dubious sources (botnets, tor endpoint) be blocked in a B2C tenant or does this require a Basic or Premium edition tenant?**</span></span></br>
<span data-ttu-id="99320-189">我們沒有適用於所有 B2C 租用戶的閘道，可篩選要求並提供殭屍網路的一些防護功能。</span><span class="sxs-lookup"><span data-stu-id="99320-189">We do have a gateway that filters requests and provides some protection from botnets, and is applied for all B2C tenants.</span></span>

## <a name="application-access"></a><span data-ttu-id="99320-190">應用程式存取</span><span class="sxs-lookup"><span data-stu-id="99320-190">Application access</span></span>
<span data-ttu-id="99320-191">**問︰哪裡可以找到與 Azure AD 預先整合的應用程式及其功能的清單？**</span><span class="sxs-lookup"><span data-stu-id="99320-191">**Q: Where can I find a list of applications that are pre-integrated with Azure AD and their capabilities?**</span></span>

<span data-ttu-id="99320-192">**答：** Azure AD 擁有來自 Microsoft、應用程式服務提供者或協力廠商超過 2600 個預先整合的應用程式。</span><span class="sxs-lookup"><span data-stu-id="99320-192">**A:** Azure AD has more than 2,600 pre-integrated applications from Microsoft, application service providers, and partners.</span></span> <span data-ttu-id="99320-193">所有預先整合的應用程式皆支援單一登入 (SSO)。</span><span class="sxs-lookup"><span data-stu-id="99320-193">All pre-integrated applications support single sign-on (SSO).</span></span> <span data-ttu-id="99320-194">SSO 可讓您使用組織認證來存取應用程式。</span><span class="sxs-lookup"><span data-stu-id="99320-194">SSO lets you use your organizational credentials to access your apps.</span></span> <span data-ttu-id="99320-195">有些應用程式也支援自動化佈建和取消佈建。</span><span class="sxs-lookup"><span data-stu-id="99320-195">Some of the applications also support automated provisioning and de-provisioning.</span></span>

<span data-ttu-id="99320-196">如需完整的預先整合應用程式清單，請參閱 [Active Directory Marketplace](https://azure.microsoft.com/marketplace/active-directory/)。</span><span class="sxs-lookup"><span data-stu-id="99320-196">For a complete list of the pre-integrated applications, see the [Active Directory Marketplace](https://azure.microsoft.com/marketplace/active-directory/).</span></span>

- - -
<span data-ttu-id="99320-197">**問︰如果 Azure AD Marketplace 內沒有我需要的應用程式，該怎麼辦？**</span><span class="sxs-lookup"><span data-stu-id="99320-197">**Q: What if the application I need is not in the Azure AD marketplace?**</span></span>

<span data-ttu-id="99320-198">**答：**若您使用 Azure AD Premium，就可以新增及設定您想要的任何應用程式。</span><span class="sxs-lookup"><span data-stu-id="99320-198">**A:** With Azure AD Premium, you can add and configure any application that you want.</span></span> <span data-ttu-id="99320-199">視應用程式功能和您的喜好設定而定，您可以設定 SSO 和自動化佈建。</span><span class="sxs-lookup"><span data-stu-id="99320-199">Depending on your application’s capabilities and your preferences, you can configure SSO and automated provisioning.</span></span>  

<span data-ttu-id="99320-200">如需詳細資訊，請參閱：</span><span class="sxs-lookup"><span data-stu-id="99320-200">For more information, see:</span></span>

* [<span data-ttu-id="99320-201">設定對不在 Azure Active Directory 應用程式庫中的應用程式的單一登入</span><span class="sxs-lookup"><span data-stu-id="99320-201">Configuring single sign-on to applications that are not in the Azure Active Directory application gallery</span></span>](active-directory-saas-custom-apps.md)
* [<span data-ttu-id="99320-202">使用 SCIM 以啟用從 Azure Active Directory 到應用程式的使用者和群組自動佈建</span><span class="sxs-lookup"><span data-stu-id="99320-202">Using SCIM to enable automatic provisioning of users and groups from Azure Active Directory to applications</span></span>](active-directory-scim-provisioning.md)

- - -
<span data-ttu-id="99320-203">**問︰使用者如何使用 Azure AD 登入應用程式？**</span><span class="sxs-lookup"><span data-stu-id="99320-203">**Q: How do users sign in to applications by using Azure AD?**</span></span>

<span data-ttu-id="99320-204">**答：** Azure AD 提供好幾種方式來讓使用者檢視和存取其應用程式，例如︰</span><span class="sxs-lookup"><span data-stu-id="99320-204">**A:** Azure AD provides several ways for users to view and access their applications, such as:</span></span>

* <span data-ttu-id="99320-205">Azure AD 存取面板</span><span class="sxs-lookup"><span data-stu-id="99320-205">The Azure AD access panel</span></span>
* <span data-ttu-id="99320-206">Office 365 應用程式啟動程式</span><span class="sxs-lookup"><span data-stu-id="99320-206">The Office 365 application launcher</span></span>
* <span data-ttu-id="99320-207">直接登入同盟應用程式</span><span class="sxs-lookup"><span data-stu-id="99320-207">Direct sign-in to federated apps</span></span>
* <span data-ttu-id="99320-208">同盟、密碼或現有應用程式的深層連結</span><span class="sxs-lookup"><span data-stu-id="99320-208">Deep links to federated, password-based, or existing apps</span></span>

<span data-ttu-id="99320-209">如需詳細資訊，請參閱 [對使用者部署 Azure AD 整合應用程式](active-directory-appssoaccess-whatis.md#deploying-azure-ad-integrated-applications-to-users)。</span><span class="sxs-lookup"><span data-stu-id="99320-209">For more information, see [Deploying Azure AD integrated applications to users](active-directory-appssoaccess-whatis.md#deploying-azure-ad-integrated-applications-to-users).</span></span>

- - -
<span data-ttu-id="99320-210">**問︰Azure AD 可透過哪些不同方式來啟用應用程式的驗證和單一登入？**</span><span class="sxs-lookup"><span data-stu-id="99320-210">**Q: What are the different ways Azure AD enables authentication and single sign-on to applications?**</span></span>

<span data-ttu-id="99320-211">**答：**Azure AD 針對驗證和授權支援許多標準化的通訊協定，例如 SAML 2.0、OpenID Connect、OAuth 2.0 和 WS-同盟。</span><span class="sxs-lookup"><span data-stu-id="99320-211">**A:** Azure AD supports many standardized protocols for authentication and authorization, such as SAML 2.0, OpenID Connect, OAuth 2.0, and WS-Federation.</span></span> <span data-ttu-id="99320-212">Azure AD 也可針對僅支援表單型驗證的應用程式，支援密碼存放和自動化登入功能。</span><span class="sxs-lookup"><span data-stu-id="99320-212">Azure AD also supports password vaulting and automated sign-in capabilities for apps that only support forms-based authentication.</span></span>  

<span data-ttu-id="99320-213">如需詳細資訊，請參閱：</span><span class="sxs-lookup"><span data-stu-id="99320-213">For more information, see:</span></span>

* [<span data-ttu-id="99320-214">Azure AD 的驗證案例</span><span class="sxs-lookup"><span data-stu-id="99320-214">Authentication Scenarios for Azure AD</span></span>](active-directory-authentication-scenarios.md)
* [<span data-ttu-id="99320-215">Active Directory 驗證通訊協定</span><span class="sxs-lookup"><span data-stu-id="99320-215">Active Directory authentication protocols</span></span>](https://msdn.microsoft.com/library/azure/dn151124.aspx)
* [<span data-ttu-id="99320-216">單一登入如何搭配 Azure Active Directory 運作？</span><span class="sxs-lookup"><span data-stu-id="99320-216">How does single sign-on with Azure Active Directory work?</span></span>](active-directory-appssoaccess-whatis.md#how-does-single-sign-on-with-azure-active-directory-work)

- - -
<span data-ttu-id="99320-217">**問︰是否可以新增在內部部署中執行的應用程式？**</span><span class="sxs-lookup"><span data-stu-id="99320-217">**Q: Can I add applications I’m running on-premises?**</span></span>

<span data-ttu-id="99320-218">**答：** Azure AD 應用程式 Proxy 可讓您簡單又安全地存取您選擇的內部部署 Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="99320-218">**A:** Azure AD Application Proxy provides you with easy and secure access to on-premises web applications that you choose.</span></span> <span data-ttu-id="99320-219">正如同存取 Azure AD 中的軟體即服務 (SaaS) 應用程式一般，相同的方式也可以用來存取這些應用程式。</span><span class="sxs-lookup"><span data-stu-id="99320-219">You can access these applications in the same way that you access your software as a service (SaaS) apps in Azure AD.</span></span> <span data-ttu-id="99320-220">並不需要 VPN 或變更網路基礎結構。</span><span class="sxs-lookup"><span data-stu-id="99320-220">There is no need for a VPN or to change your network infrastructure.</span></span>  

<span data-ttu-id="99320-221">如需詳細資訊，請參閱[如何為內部部署應用程式提供安全的遠端存取](active-directory-application-proxy-get-started.md)。</span><span class="sxs-lookup"><span data-stu-id="99320-221">For more information, see [How to provide secure remote access to on-premises applications](active-directory-application-proxy-get-started.md).</span></span>

- - -
<span data-ttu-id="99320-222">**問︰如何對存取特定應用程式的使用者要求 Multi-Factor Authentication？**</span><span class="sxs-lookup"><span data-stu-id="99320-222">**Q: How do I require multi-factor authentication for users who access a particular application?**</span></span>

<span data-ttu-id="99320-223">**答：** Azure AD 條件式存取可讓您針對每個應用程式指派唯一的存取原則。</span><span class="sxs-lookup"><span data-stu-id="99320-223">**A:** With Azure AD conditional access, you can assign a unique access policy for each application.</span></span> <span data-ttu-id="99320-224">您可以在原則中要求一律要進行 Multi-Factor Authentication，或在使用者未連線到區域網路時才進行。</span><span class="sxs-lookup"><span data-stu-id="99320-224">In your policy, you can require multi-factor authentication always, or when users are not connected to the local network.</span></span>  

<span data-ttu-id="99320-225">如需詳細資訊，請參閱[保護對 Office 365 及其他連接至 Azure Active Directory 之應用程式的存取](active-directory-conditional-access.md)。</span><span class="sxs-lookup"><span data-stu-id="99320-225">For more information, see [Securing access to Office 365 and other apps connected to Azure Active Directory](active-directory-conditional-access.md).</span></span>

- - -
<span data-ttu-id="99320-226">**問︰SaaS 應用程式的自動化使用者佈建是什麼？**</span><span class="sxs-lookup"><span data-stu-id="99320-226">**Q: What is automated user provisioning for SaaS apps?**</span></span>

<span data-ttu-id="99320-227">**答：**使用 Azure AD 可讓您在許多熱門雲端 (SaaS) 應用程式中自動建立、維護和移除使用者身分識別。</span><span class="sxs-lookup"><span data-stu-id="99320-227">**A:** Use Azure AD to automate the creation, maintenance, and removal of user identities in many popular cloud SaaS apps.</span></span>

<span data-ttu-id="99320-228">如需詳細資訊，請參閱[使用 Azure Active Directory 自動進行 SaaS 應用程式的使用者佈建和解除佈建](active-directory-saas-app-provisioning.md)。</span><span class="sxs-lookup"><span data-stu-id="99320-228">For more information, see [Automate user provisioning and deprovisioning to SaaS applications with Azure Active Directory](active-directory-saas-app-provisioning.md).</span></span>

- - -
<span data-ttu-id="99320-229">**問︰是否可以設定與 Azure AD 之間的安全 LDAP 連線？**</span><span class="sxs-lookup"><span data-stu-id="99320-229">**Q:  Can I set up a secure LDAP connection with Azure AD?**</span></span>

<span data-ttu-id="99320-230">**答：**否。</span><span class="sxs-lookup"><span data-stu-id="99320-230">**A:**  No.</span></span> <span data-ttu-id="99320-231">Azure AD 不支援 LDAP 通訊協定。</span><span class="sxs-lookup"><span data-stu-id="99320-231">Azure AD does not support the LDAP protocol.</span></span>
