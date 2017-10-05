---
title: "使用 Azure Active Directory 管理應用程式 | Microsoft Docs"
description: "本文章說明整合 Azure Active Directory 與您的內部部署、雲端和 SaaS 應用程式的優點。"
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
ms.assetid: 95b96f10-2d5c-4b78-8af8-d3657a24140f
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/05/2017
ms.author: markvi
ms.reviewer: asteen
ms.openlocfilehash: b8f0cfdb468094bc761d6b939ca318fcfbea3ea4
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="managing-applications-with-azure-active-directory"></a><span data-ttu-id="11ccd-103">使用 Azure Active Directory 來管理應用程式</span><span class="sxs-lookup"><span data-stu-id="11ccd-103">Managing Applications with Azure Active Directory</span></span>
<span data-ttu-id="11ccd-104">在實際工作流程或內容以外，企業對所有應用程式有兩個基本需求：</span><span class="sxs-lookup"><span data-stu-id="11ccd-104">Beyond the actual workflow or content, businesses have two basic requirements for all applications:</span></span>

1. <span data-ttu-id="11ccd-105">要增加生產力，應用程式應該易於探索及存取</span><span class="sxs-lookup"><span data-stu-id="11ccd-105">To increase productivity, applications should be easy to discover and access</span></span>
2. <span data-ttu-id="11ccd-106">要啟用安全性和控管，組織需要控制和監督可以存取與實際存取每個應用程式的對象</span><span class="sxs-lookup"><span data-stu-id="11ccd-106">To enable security and governance, the organization needs control and oversight on who can and actually is accessing each application</span></span>

<span data-ttu-id="11ccd-107">就雲端應用程式而言，使用身分識別來控制「誰有權執行什麼」最能達成此目標。</span><span class="sxs-lookup"><span data-stu-id="11ccd-107">In the world of cloud applications this can best be achieved using identity to control “*WHO is allowed to do WHAT*”.</span></span>

<span data-ttu-id="11ccd-108">在運算術語中：</span><span class="sxs-lookup"><span data-stu-id="11ccd-108">In computing terminology:</span></span>

* <span data-ttu-id="11ccd-109">*誰*被稱為*身分識別* - 用來管理使用者和群組</span><span class="sxs-lookup"><span data-stu-id="11ccd-109">*Who* is known as *identity* - the management of users and groups</span></span>
* <span data-ttu-id="11ccd-110">*什麼*被稱為*存取管理* - 用來管理對受保護資源的存取</span><span class="sxs-lookup"><span data-stu-id="11ccd-110">*What* is known as *access management* – the management of access to protected resources</span></span>

<span data-ttu-id="11ccd-111">這兩個元件結合在一起就稱為*身分識別與存取管理 (IAM)*，[Gartner](http://www.gartner.com/it-glossary/identity-and-access-management-iam) 團隊將它定義為「*可讓適當的個人以正當理由在適當時機存取適當資源的安全性規定*」。</span><span class="sxs-lookup"><span data-stu-id="11ccd-111">Both components together are known as *Identity and Access Management (IAM)*, which is defined by the [Gartner](http://www.gartner.com/it-glossary/identity-and-access-management-iam) group as “*the security discipline that enables the right individuals to access the right resources at the right times for the right reasons*”.</span></span>

<span data-ttu-id="11ccd-112">好，那麼問題是什麼？</span><span class="sxs-lookup"><span data-stu-id="11ccd-112">Okay, so what’s the problem?</span></span> <span data-ttu-id="11ccd-113">如果 IAM *未* 在一個地方使用整合解決方案加以管理：</span><span class="sxs-lookup"><span data-stu-id="11ccd-113">If IAM is *not managed* in one place with an integrated solution:</span></span>

* <span data-ttu-id="11ccd-114">身分識別系統管理員需要個別建立和個別更新所有應用程式中的使用者帳戶，這是既重複又耗時的活動。</span><span class="sxs-lookup"><span data-stu-id="11ccd-114">Identity administrators have to individually create and update user accounts in all applications separately, a redundant and time consuming activity.</span></span>
* <span data-ttu-id="11ccd-115">使用者必須記住多個認證，才能存取他們需要使用的應用程式。</span><span class="sxs-lookup"><span data-stu-id="11ccd-115">Users have to memorize multiple credentials to access the applications they need to work with.</span></span> <span data-ttu-id="11ccd-116">如此一來，使用者傾向於將密碼寫下，或使用其他密碼管理解決方案，而這會帶來其他資料安全性的風險。</span><span class="sxs-lookup"><span data-stu-id="11ccd-116">As a result, users tend to write down their passwords or use other password management solutions which introduces other data security risks.</span></span>
* <span data-ttu-id="11ccd-117">重複、耗時的活動減少了使用者和系統管理員處理可增加您的企業營收之商務活動的時間。</span><span class="sxs-lookup"><span data-stu-id="11ccd-117">Redundant, time consuming activities reduce the amount of time users and administrators are working on business activities that increase your business’s bottom line.</span></span>

<span data-ttu-id="11ccd-118">因此，通常何者會防止組織採用整合式 IAM 解決方案？</span><span class="sxs-lookup"><span data-stu-id="11ccd-118">So, what generally prevents organizations from adopting integrated IAM solutions?</span></span>

* <span data-ttu-id="11ccd-119">大多數技術解決方案是基於需由組織為自己的應用程式部署及調整的軟體平台。</span><span class="sxs-lookup"><span data-stu-id="11ccd-119">Most technical solutions are based on software platforms that need to be deployed and adapted by each organization for their own applications.</span></span>
* <span data-ttu-id="11ccd-120">採用雲端應用程式通常會比 IT 組織可以與現有的 IAM 解決方案整合需要更高的費率。</span><span class="sxs-lookup"><span data-stu-id="11ccd-120">Cloud applications are often adopted at a higher rate than IT organization can integrate with existing IAM solutions.</span></span>
* <span data-ttu-id="11ccd-121">安全性與監控工具需要其他的自訂與整合，以達到完善 E2E 案例。</span><span class="sxs-lookup"><span data-stu-id="11ccd-121">Security and monitoring tooling require additional customization and integration to achieve comprehensive E2E scenarios.</span></span>

## <a name="azure-active-directory-integrated-with-applications"></a><span data-ttu-id="11ccd-122">與應用程式整合的 Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="11ccd-122">Azure Active Directory integrated with applications</span></span>
<span data-ttu-id="11ccd-123">Azure Active Directory 是 Microsoft 的全方位「身分識別即服務」(IDaaS) 解決方案，它能夠：</span><span class="sxs-lookup"><span data-stu-id="11ccd-123">Azure Active Directory is Microsoft’s comprehensive Identity as a Service (IDaaS) solution that:</span></span>

* <span data-ttu-id="11ccd-124">讓 IAM 做為雲端服務</span><span class="sxs-lookup"><span data-stu-id="11ccd-124">Enables IAM as a cloud service</span></span> 
* <span data-ttu-id="11ccd-125">提供集中式存取管理、單一登入 (SSO) 及報告功能</span><span class="sxs-lookup"><span data-stu-id="11ccd-125">Provides central access management, single-sign on (SSO), and reporting</span></span> 
* <span data-ttu-id="11ccd-126">支援應用程式資源庫中 [數千個應用程式](https://azure.microsoft.com/marketplace/active-directory/) (包括 Salesforce、Google Apps、Box、Concur 等) 的整合式存取管理。</span><span class="sxs-lookup"><span data-stu-id="11ccd-126">Supports integrated access management for [thousands of applications](https://azure.microsoft.com/marketplace/active-directory/) in the application gallery, including Salesforce, Google Apps, Box, Concur, and more.</span></span> 

<span data-ttu-id="11ccd-127">藉由 Azure Active Directory，您為合作夥伴和客戶 (企業或消費者) 發佈的所有應用程式都可享有相同的身分識別與存取管理功能。</span><span class="sxs-lookup"><span data-stu-id="11ccd-127">With Azure Active Directory, all applications you publish for your partners and customers (business or consumer) have the same identity and access management capabilities.</span></span><br> <span data-ttu-id="11ccd-128">這可讓您大幅降低營運成本。</span><span class="sxs-lookup"><span data-stu-id="11ccd-128">This enables you to significantly reduce your operational costs.</span></span>

<span data-ttu-id="11ccd-129">如果您需要實作尚未列在應用程式資源庫的應用程式，該怎麼辦？</span><span class="sxs-lookup"><span data-stu-id="11ccd-129">What if you need to implement an application that is not yet listed in the application gallery?</span></span> <span data-ttu-id="11ccd-130">雖然這比起從應用程式資源庫的設定應用程式的 SSO 更為耗時一點，Azure AD 提供了精靈可協助您完成組態。</span><span class="sxs-lookup"><span data-stu-id="11ccd-130">While this is a bit more time-consuming than configuring SSO for applications from the application gallery, Azure AD provides you with a wizard that helps you with the configuration.</span></span>

<span data-ttu-id="11ccd-131">Azure AD 的價值不僅僅是雲端應用程式而已。</span><span class="sxs-lookup"><span data-stu-id="11ccd-131">The value of Azure AD goes beyond “just” cloud applications.</span></span> <span data-ttu-id="11ccd-132">您也可以透過提供安全的遠端存取，將它與內部部署應用程式搭配使用。</span><span class="sxs-lookup"><span data-stu-id="11ccd-132">You can also use it with on-premises applications by providing secure remote access.</span></span> <span data-ttu-id="11ccd-133">有了安全的遠端存取，您就不再需要 VPN 或其他傳統的遠端存取管理實作。</span><span class="sxs-lookup"><span data-stu-id="11ccd-133">With secure remote access, you can eliminate the the need for VPNs or other traditional remote access management implementations.</span></span>

<span data-ttu-id="11ccd-134">Azure AD 透過為您的所有應用程式提供集中式存取管理和單一登入 (SSO)，提供了主要資料安全性和生產力問題的解決方案。</span><span class="sxs-lookup"><span data-stu-id="11ccd-134">By providing central access management and single sign on (SSO) for all your applications, Azure AD provides the solution to the main data security and productivity problems.</span></span>

* <span data-ttu-id="11ccd-135">使用者透過登入一次即可存取多個應用程式，使得他們有更多時間可帶來收入或完成商務作業活動。</span><span class="sxs-lookup"><span data-stu-id="11ccd-135">Users can access multiple applications with one sign on giving more time to income generating or business operations activities done.</span></span>
* <span data-ttu-id="11ccd-136">身分識別系統管理員可以在一個位置管理對應用程式的存取。</span><span class="sxs-lookup"><span data-stu-id="11ccd-136">Identity administrators can manage access to applications in one place.</span></span>

<span data-ttu-id="11ccd-137">對使用者和貴公司的優點很明顯。</span><span class="sxs-lookup"><span data-stu-id="11ccd-137">The benefit for the user and for your company is obvious.</span></span> <span data-ttu-id="11ccd-138">讓我們仔細看看對身分識別系統管理員和組織的優點。</span><span class="sxs-lookup"><span data-stu-id="11ccd-138">Let’s take a closer look at the benefits for an identity administrator and the organization.</span></span>

## <a name="integrated-application-benefits"></a><span data-ttu-id="11ccd-139">整合式應用程式優點</span><span class="sxs-lookup"><span data-stu-id="11ccd-139">Integrated application benefits</span></span>
<span data-ttu-id="11ccd-140">SSO 程序有兩個步驟：</span><span class="sxs-lookup"><span data-stu-id="11ccd-140">The SSO process has two steps:</span></span>

* <span data-ttu-id="11ccd-141">驗證：驗證使用者身分識別的程序。</span><span class="sxs-lookup"><span data-stu-id="11ccd-141">Authentication, the process of validating the user’s identity.</span></span>
* <span data-ttu-id="11ccd-142">授權：使用存取原則決定啟用或封鎖對資源的存取。</span><span class="sxs-lookup"><span data-stu-id="11ccd-142">Authorization, the decision to enable or block access to a resource with an access policy.</span></span>

<span data-ttu-id="11ccd-143">使用 Azure AD 來管理應用程式及啟用 SSO 時：</span><span class="sxs-lookup"><span data-stu-id="11ccd-143">When using Azure AD to manage applications and enable SSO:</span></span>

* <span data-ttu-id="11ccd-144">驗證是在使用者的內部部署 (例如 AD) 或 Azure AD 帳戶中完成。</span><span class="sxs-lookup"><span data-stu-id="11ccd-144">Authentication is done on the user’s on-premises (e.g. AD) or Azure AD account.</span></span>
* <span data-ttu-id="11ccd-145">授權會基於 Azure AD 指派及保護原則執行，以確保一致的使用者體驗，並讓您在任何應用程式上加入指派、位置和 MFA 條件，而不論其內部功能為何。</span><span class="sxs-lookup"><span data-stu-id="11ccd-145">Authorization executes on the Azure AD assignment and protection policy ensuring consistent end user experience and enabling you to add assignment, locations, and MFA conditions on any application, regardless of its internal capabilities.</span></span>

<span data-ttu-id="11ccd-146">請務必了解，授權在目標應用程式上執行的方式，會根據應用程式與 Azure AD 整合的方式而有所不同。</span><span class="sxs-lookup"><span data-stu-id="11ccd-146">It important to understand that the way the authorization is enacted on the target application varies depending on how the application was integrated with Azure AD.</span></span>

* <span data-ttu-id="11ccd-147">**由服務提供者預先整合應用程式** ：如同 Office 365 和 Azure，這些應用程式都是直接在 Azure AD 上建置並仰賴其完整的身分識別和存取管理功能。</span><span class="sxs-lookup"><span data-stu-id="11ccd-147">**Applications pre-integrated by service provider** Like Office 365 and Azure, these are applications built directly on Azure AD and relying on it for their comprehensive identity and access management capabilities.</span></span> <span data-ttu-id="11ccd-148">對這些應用程式的存取是透過目錄資訊與權杖發行來啟用。</span><span class="sxs-lookup"><span data-stu-id="11ccd-148">Access to these applications is enabled through directory information and token issuance.</span></span>
* <span data-ttu-id="11ccd-149">**由 Microsoft 預先整合的應用程式和自訂應用程式** ：這些是依賴內部應用程式目錄並可獨立於 Azure AD 運作的獨立雲端應用程式。</span><span class="sxs-lookup"><span data-stu-id="11ccd-149">**Applications pre-integrated by Microsoft and custom applications** These are independent cloud applications that rely on an internal application directory and can operate independently of Azure AD.</span></span> <span data-ttu-id="11ccd-150">對這些應用程式的存取會透過發行應用程式特定認證給對應於應用程式帳戶來啟用。</span><span class="sxs-lookup"><span data-stu-id="11ccd-150">Access to these applications is enabled by issuing an application specific credential mapped to an application account.</span></span> <span data-ttu-id="11ccd-151">根據應用程式的功能，認證可以是同盟權杖或先前佈建在應用程式中帳戶的使用者名稱或密碼。</span><span class="sxs-lookup"><span data-stu-id="11ccd-151">Depending on the application capabilities, the credential may be a federation token or user-name and password for an account that was previously provisioned in the application.</span></span>
* <span data-ttu-id="11ccd-152">**內部應用程式** ：透過 Azure AD 應用程式 Proxy 發佈的應用程式，主要可啟用對內部部署應用程式的存取。</span><span class="sxs-lookup"><span data-stu-id="11ccd-152">**On-premises applications** Applications published through the Azure AD application proxy primarily enabling access to on-premises applications.</span></span> <span data-ttu-id="11ccd-153">這些應用程式依賴於 Windows Server Active Directory 之類的內部部署目錄中心。</span><span class="sxs-lookup"><span data-stu-id="11ccd-153">These applications rely on a central on-premises directory like Windows Server Active Directory.</span></span> <span data-ttu-id="11ccd-154">透過觸發 Proxy 來提供應用程式內容給一般使用者，同時接受內部部署上的登入需求，即可啟用對這些應用程式的存取。</span><span class="sxs-lookup"><span data-stu-id="11ccd-154">Access to these applications is enabled by triggering the proxy to deliver the application content to the end user while honoring the on-premises sign-on requirement.</span></span>

<span data-ttu-id="11ccd-155">例如，如果使用者加入您的組織，您需要在主要登入作業的 Azure AD 中為使用者建立帳戶。</span><span class="sxs-lookup"><span data-stu-id="11ccd-155">For example, if a user joins your organization, you need to create an account for the user in Azure AD for the primary sign-on operations.</span></span> <span data-ttu-id="11ccd-156">如果此使用者需要存取 Salesforce 之類的受管理應用程式，您也需要在 Salesforce 中為此使用者建立帳戶，並將它連結到 Azure 帳戶，SSO 才能運作。</span><span class="sxs-lookup"><span data-stu-id="11ccd-156">If this user requires access to a managed application such as Salesforce, you also need to create an account for this user in Salesforce and link it to the Azure account to make SSO work.</span></span> <span data-ttu-id="11ccd-157">當使用者離開組織時，建議您將 Azure AD 帳戶和使用者具有存取權的應用程式 IAM 存放區中的所有對應帳戶刪除。</span><span class="sxs-lookup"><span data-stu-id="11ccd-157">When the user leaves your organization, it is advisable to delete the Azure AD account and all counterpart accounts in the IAM stores of the applications the user had access to.</span></span>

## <a name="access-detection"></a><span data-ttu-id="11ccd-158">存取偵測</span><span class="sxs-lookup"><span data-stu-id="11ccd-158">Access detection</span></span>
<span data-ttu-id="11ccd-159">在現代企業中，IT 部門並通常不知道使用的所有雲端應用程式。</span><span class="sxs-lookup"><span data-stu-id="11ccd-159">In modern enterprises, IT departments are often not aware of all the cloud applications that are being used.</span></span> <span data-ttu-id="11ccd-160">結合 Cloud App Discovery，Azure AD 為您提供偵測這些應用程式的解決方案。</span><span class="sxs-lookup"><span data-stu-id="11ccd-160">In conjunction with Cloud App Discovery, Azure AD provides you with a solution to detect these applications.</span></span>

## <a name="account-management"></a><span data-ttu-id="11ccd-161">帳戶管理</span><span class="sxs-lookup"><span data-stu-id="11ccd-161">Account management</span></span>
<span data-ttu-id="11ccd-162">傳統上，管理各種應用程式中的帳戶是由組織中的 IT 或支援人員執行的手動程序。</span><span class="sxs-lookup"><span data-stu-id="11ccd-162">Traditionally, managing accounts in the various applications is a manual process performed by IT or support personal in the organization.</span></span> <span data-ttu-id="11ccd-163">Azure AD 將跨所有服務提供者整合的應用程式和由 Microsoft 預先整合的這些應用程式的帳戶管理完全自動化，可支援自動化使用者佈建或 SAML JIT。</span><span class="sxs-lookup"><span data-stu-id="11ccd-163">Azure AD fully automated account management across all service provider integrated applications and those applications pre-integrated by Microsoft supporting automated user provisioning or SAML JIT.</span></span>

## <a name="automated-user-provisioning"></a><span data-ttu-id="11ccd-164">自動的使用者佈建</span><span class="sxs-lookup"><span data-stu-id="11ccd-164">Automated user provisioning</span></span>
<span data-ttu-id="11ccd-165">某些應用程式提供自動化介面用於建立和移除 (或停用) 帳戶。</span><span class="sxs-lookup"><span data-stu-id="11ccd-165">Some applications provide automation interfaces for creation and removal (or deactivation) of accounts.</span></span> <span data-ttu-id="11ccd-166">如果有提供者提供這樣的介面，Azure AD 會加以利用。</span><span class="sxs-lookup"><span data-stu-id="11ccd-166">If a provider offers such an interface, it is leveraged by Azure AD.</span></span> <span data-ttu-id="11ccd-167">這樣可以減少您的營運成本，因為系統管理工作會自動發生，並改善您環境的安全性，因為它會減少未經授權存取的機會。</span><span class="sxs-lookup"><span data-stu-id="11ccd-167">This reduces your operational costs because administrative tasks happen automatically, and improves the security of your environment because it decreases the chance of unauthorized access.</span></span>

## <a name="access-management"></a><span data-ttu-id="11ccd-168">存取管理</span><span class="sxs-lookup"><span data-stu-id="11ccd-168">Access management</span></span>
<span data-ttu-id="11ccd-169">使用 Azure AD，您可以使用個別或規則驅動指派來管理對應用程式的存取。</span><span class="sxs-lookup"><span data-stu-id="11ccd-169">Using Azure AD you can manage access to applications using individual or rule driven assignments.</span></span> <span data-ttu-id="11ccd-170">您也可以將存取管理委派給組織中適當的人員，以獲得確保最佳的監督並減少技術服務人員的負擔。</span><span class="sxs-lookup"><span data-stu-id="11ccd-170">You can also delegate access management to the right people in the organization ensuring the best oversight and reducing the burden on helpdesk.</span></span>

## <a name="on-premises-applications"></a><span data-ttu-id="11ccd-171">內部應用程式</span><span class="sxs-lookup"><span data-stu-id="11ccd-171">On-premises applications</span></span>
<span data-ttu-id="11ccd-172">內建的應用程式 Proxy 可讓您將內部部署應用程式發佈給使用者，以獲得對現代化雲端應用程式一致的存取經驗以及 Azure AD 監視、報告和安全性功能的優點。</span><span class="sxs-lookup"><span data-stu-id="11ccd-172">The built in application proxy enables you to publish your on-premises applications to your users resulting in both consistent access experience with modern cloud application and the benefits from Azure AD monitoring, reporting, and security capabilities.</span></span>

## <a name="reporting-and-monitoring"></a><span data-ttu-id="11ccd-173">報告和監控</span><span class="sxs-lookup"><span data-stu-id="11ccd-173">Reporting and monitoring</span></span>
<span data-ttu-id="11ccd-174">Azure AD 為您提供預先整合的報告與監控功能，可讓您知道可以存取與實際存取每個應用程式的對象。</span><span class="sxs-lookup"><span data-stu-id="11ccd-174">Azure AD provides you with pre-integrated reporting and monitoring capabilities that enable you to know who has access to applications and when they actually used them.</span></span>

## <a name="related-capabilities"></a><span data-ttu-id="11ccd-175">相關功能</span><span class="sxs-lookup"><span data-stu-id="11ccd-175">Related capabilities</span></span>
<span data-ttu-id="11ccd-176">您可以使用 Azure AD 透過更細微的存取原則和預先整合的 MFA 來保護您的應用程式。</span><span class="sxs-lookup"><span data-stu-id="11ccd-176">With Azure AD you can secure your applications with granular access policies and pre-integrated MFA.</span></span> <span data-ttu-id="11ccd-177">若要深入了解 Azure MFA，請參閱 [Azure MFA](https://azure.microsoft.com/services/multi-factor-authentication/)。</span><span class="sxs-lookup"><span data-stu-id="11ccd-177">To learn more about Azure MFA see [Azure MFA](https://azure.microsoft.com/services/multi-factor-authentication/).</span></span>

## <a name="getting-started"></a><span data-ttu-id="11ccd-178">開始使用</span><span class="sxs-lookup"><span data-stu-id="11ccd-178">Getting started</span></span>
<span data-ttu-id="11ccd-179">若要開始使用 Azure AD 來整合應用程式，請查看 [整合 Azure Active Directory 與應用程式入門指南](active-directory-integrating-applications-getting-started.md)。</span><span class="sxs-lookup"><span data-stu-id="11ccd-179">To get started integrating applications with Azure AD, take a look at the [Integrating Azure Active Directory with applications getting started guide](active-directory-integrating-applications-getting-started.md).</span></span>

## <a name="see-also"></a><span data-ttu-id="11ccd-180">另請參閱</span><span class="sxs-lookup"><span data-stu-id="11ccd-180">See also</span></span>
[<span data-ttu-id="11ccd-181">Article Index for Application Management in Azure Active Directory (Azure Active Directory 中應用程式管理的文件索引)</span><span class="sxs-lookup"><span data-stu-id="11ccd-181">Article Index for Application Management in Azure Active Directory</span></span>](active-directory-apps-index.md)

