---
title: "應用程式與 Azure Active Directory aaaManaging |Microsoft 文件"
description: "此文章 hello 的優點與您的內部部署、 雲端 SaaS 應用程式整合 Azure Active Directory。"
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
ms.openlocfilehash: 0016f8b433e101d8a150bc6d9be3931851578241
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="managing-applications-with-azure-active-directory"></a><span data-ttu-id="658cd-103">使用 Azure Active Directory 來管理應用程式</span><span class="sxs-lookup"><span data-stu-id="658cd-103">Managing Applications with Azure Active Directory</span></span>
<span data-ttu-id="658cd-104">超過 hello 實際工作流程或內容，企業會有兩個的所有應用程式的基本需求：</span><span class="sxs-lookup"><span data-stu-id="658cd-104">Beyond hello actual workflow or content, businesses have two basic requirements for all applications:</span></span>

1. <span data-ttu-id="658cd-105">tooincrease 產能應用程式應該簡單 toodiscover 和存取</span><span class="sxs-lookup"><span data-stu-id="658cd-105">tooincrease productivity, applications should be easy toodiscover and access</span></span>
2. <span data-ttu-id="658cd-106">hello 組織 tooenable 安全性和控管，需要控制和監督者可以與實際存取每個應用程式</span><span class="sxs-lookup"><span data-stu-id="658cd-106">tooenable security and governance, hello organization needs control and oversight on who can and actually is accessing each application</span></span>

<span data-ttu-id="658cd-107">中的雲端應用程式最適合這可以使用身分識別 toocontrol hello world"*誰是允許 toodo 什麼*"。</span><span class="sxs-lookup"><span data-stu-id="658cd-107">In hello world of cloud applications this can best be achieved using identity toocontrol “*WHO is allowed toodo WHAT*”.</span></span>

<span data-ttu-id="658cd-108">在運算術語中：</span><span class="sxs-lookup"><span data-stu-id="658cd-108">In computing terminology:</span></span>

* <span data-ttu-id="658cd-109">*誰*稱為*識別*-hello 管理使用者和群組</span><span class="sxs-lookup"><span data-stu-id="658cd-109">*Who* is known as *identity* - hello management of users and groups</span></span>
* <span data-ttu-id="658cd-110">*什麼*稱為*存取管理*– hello 存取 tooprotected 資源管理</span><span class="sxs-lookup"><span data-stu-id="658cd-110">*What* is known as *access management* – hello management of access tooprotected resources</span></span>

<span data-ttu-id="658cd-111">這兩個元件統稱為*身分識別和存取管理 (IAM)*，定義由 hello [Gartner](http://www.gartner.com/it-glossary/identity-and-access-management-iam)群組做為"*hello 安全性專業領域，可讓 hello 權限個人 tooaccess hello 正確的資源在 hello 以滑鼠右鍵 hello 右基於時間*"。</span><span class="sxs-lookup"><span data-stu-id="658cd-111">Both components together are known as *Identity and Access Management (IAM)*, which is defined by hello [Gartner](http://www.gartner.com/it-glossary/identity-and-access-management-iam) group as “*hello security discipline that enables hello right individuals tooaccess hello right resources at hello right times for hello right reasons*”.</span></span>

<span data-ttu-id="658cd-112">好，那麼是什麼 hello 問題嗎？</span><span class="sxs-lookup"><span data-stu-id="658cd-112">Okay, so what’s hello problem?</span></span> <span data-ttu-id="658cd-113">如果 IAM *未* 在一個地方使用整合解決方案加以管理：</span><span class="sxs-lookup"><span data-stu-id="658cd-113">If IAM is *not managed* in one place with an integrated solution:</span></span>

* <span data-ttu-id="658cd-114">身分識別系統管理員可以建立並分開，更新所有應用程式中的使用者帳戶的 tooindividually 多餘且耗時的活動。</span><span class="sxs-lookup"><span data-stu-id="658cd-114">Identity administrators have tooindividually create and update user accounts in all applications separately, a redundant and time consuming activity.</span></span>
* <span data-ttu-id="658cd-115">使用者擁有 toomemorize 多個認證 tooaccess hello 應用程式需要與 toowork。</span><span class="sxs-lookup"><span data-stu-id="658cd-115">Users have toomemorize multiple credentials tooaccess hello applications they need toowork with.</span></span> <span data-ttu-id="658cd-116">如此一來，使用者傾向 toowrite 向他們的密碼，或使用其他密碼管理解決方案造成其他資料安全性風險。</span><span class="sxs-lookup"><span data-stu-id="658cd-116">As a result, users tend toowrite down their passwords or use other password management solutions which introduces other data security risks.</span></span>
* <span data-ttu-id="658cd-117">備援、 耗費時間的活動減少 hello 的使用者和系統管理員正在增加您的業務營收的商務活動。</span><span class="sxs-lookup"><span data-stu-id="658cd-117">Redundant, time consuming activities reduce hello amount of time users and administrators are working on business activities that increase your business’s bottom line.</span></span>

<span data-ttu-id="658cd-118">因此，通常何者會防止組織採用整合式 IAM 解決方案？</span><span class="sxs-lookup"><span data-stu-id="658cd-118">So, what generally prevents organizations from adopting integrated IAM solutions?</span></span>

* <span data-ttu-id="658cd-119">最技術解決方案根據需要 toobe 部署，並由其自身應用程式的每個組織的軟體平台。</span><span class="sxs-lookup"><span data-stu-id="658cd-119">Most technical solutions are based on software platforms that need toobe deployed and adapted by each organization for their own applications.</span></span>
* <span data-ttu-id="658cd-120">採用雲端應用程式通常會比 IT 組織可以與現有的 IAM 解決方案整合需要更高的費率。</span><span class="sxs-lookup"><span data-stu-id="658cd-120">Cloud applications are often adopted at a higher rate than IT organization can integrate with existing IAM solutions.</span></span>
* <span data-ttu-id="658cd-121">安全性和監視工具需要額外的自訂及整合 tooachieve 完整 E2E 案例。</span><span class="sxs-lookup"><span data-stu-id="658cd-121">Security and monitoring tooling require additional customization and integration tooachieve comprehensive E2E scenarios.</span></span>

## <a name="azure-active-directory-integrated-with-applications"></a><span data-ttu-id="658cd-122">與應用程式整合的 Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="658cd-122">Azure Active Directory integrated with applications</span></span>
<span data-ttu-id="658cd-123">Azure Active Directory 是 Microsoft 的全方位「身分識別即服務」(IDaaS) 解決方案，它能夠：</span><span class="sxs-lookup"><span data-stu-id="658cd-123">Azure Active Directory is Microsoft’s comprehensive Identity as a Service (IDaaS) solution that:</span></span>

* <span data-ttu-id="658cd-124">讓 IAM 做為雲端服務</span><span class="sxs-lookup"><span data-stu-id="658cd-124">Enables IAM as a cloud service</span></span> 
* <span data-ttu-id="658cd-125">提供集中式存取管理、單一登入 (SSO) 及報告功能</span><span class="sxs-lookup"><span data-stu-id="658cd-125">Provides central access management, single-sign on (SSO), and reporting</span></span> 
* <span data-ttu-id="658cd-126">支援的整合式的存取管理[數千個應用程式](https://azure.microsoft.com/marketplace/active-directory/)在 hello 應用程式庫，包括 Salesforce、 Google Apps、 Box、 Concur、 和多個。</span><span class="sxs-lookup"><span data-stu-id="658cd-126">Supports integrated access management for [thousands of applications](https://azure.microsoft.com/marketplace/active-directory/) in hello application gallery, including Salesforce, Google Apps, Box, Concur, and more.</span></span> 

<span data-ttu-id="658cd-127">與 Azure Active Directory，所有應用程式發行您的合作夥伴，且 （商務或取用者） 的客戶有 hello 相同的身分識別和存取管理功能。</span><span class="sxs-lookup"><span data-stu-id="658cd-127">With Azure Active Directory, all applications you publish for your partners and customers (business or consumer) have hello same identity and access management capabilities.</span></span><br> <span data-ttu-id="658cd-128">這樣做可讓您 toosignificantly 縮減營運成本。</span><span class="sxs-lookup"><span data-stu-id="658cd-128">This enables you toosignificantly reduce your operational costs.</span></span>

<span data-ttu-id="658cd-129">如果您需要 tooimplement 還未列在 hello 應用程式庫的應用程式嗎？</span><span class="sxs-lookup"><span data-stu-id="658cd-129">What if you need tooimplement an application that is not yet listed in hello application gallery?</span></span> <span data-ttu-id="658cd-130">這是一個位元較費時，比從 hello 應用程式庫的應用程式設定 SSO，而 Azure AD 可讓您使用精靈，可協助您與 hello 組態。</span><span class="sxs-lookup"><span data-stu-id="658cd-130">While this is a bit more time-consuming than configuring SSO for applications from hello application gallery, Azure AD provides you with a wizard that helps you with hello configuration.</span></span>

<span data-ttu-id="658cd-131">Azure AD 的 hello 值超出 「 僅 」 雲端應用程式。</span><span class="sxs-lookup"><span data-stu-id="658cd-131">hello value of Azure AD goes beyond “just” cloud applications.</span></span> <span data-ttu-id="658cd-132">您也可以透過提供安全的遠端存取，將它與內部部署應用程式搭配使用。</span><span class="sxs-lookup"><span data-stu-id="658cd-132">You can also use it with on-premises applications by providing secure remote access.</span></span> <span data-ttu-id="658cd-133">與安全遠端存取，您可以排除 hello hello 需要 Vpn 或其他傳統的遠端存取管理實作。</span><span class="sxs-lookup"><span data-stu-id="658cd-133">With secure remote access, you can eliminate hello hello need for VPNs or other traditional remote access management implementations.</span></span>

<span data-ttu-id="658cd-134">藉由提供您的應用程式的集中存取管理和單一登入 (SSO)，Azure AD 提供 hello 解決方案 toohello 主要資料安全性和產能的問題。</span><span class="sxs-lookup"><span data-stu-id="658cd-134">By providing central access management and single sign on (SSO) for all your applications, Azure AD provides hello solution toohello main data security and productivity problems.</span></span>

* <span data-ttu-id="658cd-135">使用者可以存取一次登入，提供更多時間 tooincome 產生或商務作業活動完成的多個應用程式。</span><span class="sxs-lookup"><span data-stu-id="658cd-135">Users can access multiple applications with one sign on giving more time tooincome generating or business operations activities done.</span></span>
* <span data-ttu-id="658cd-136">身分識別的系統管理員可以管理存取 tooapplications 在同一個地方。</span><span class="sxs-lookup"><span data-stu-id="658cd-136">Identity administrators can manage access tooapplications in one place.</span></span>

<span data-ttu-id="658cd-137">hello 權益 hello 使用者並為您的公司是明顯。</span><span class="sxs-lookup"><span data-stu-id="658cd-137">hello benefit for hello user and for your company is obvious.</span></span> <span data-ttu-id="658cd-138">讓我們探討身分識別管理員 」 和 「 hello 組織 hello 優點。</span><span class="sxs-lookup"><span data-stu-id="658cd-138">Let’s take a closer look at hello benefits for an identity administrator and hello organization.</span></span>

## <a name="integrated-application-benefits"></a><span data-ttu-id="658cd-139">整合式應用程式優點</span><span class="sxs-lookup"><span data-stu-id="658cd-139">Integrated application benefits</span></span>
<span data-ttu-id="658cd-140">hello SSO 程序有兩個步驟：</span><span class="sxs-lookup"><span data-stu-id="658cd-140">hello SSO process has two steps:</span></span>

* <span data-ttu-id="658cd-141">驗證，驗證 hello 使用者的身分識別的 hello 程序。</span><span class="sxs-lookup"><span data-stu-id="658cd-141">Authentication, hello process of validating hello user’s identity.</span></span>
* <span data-ttu-id="658cd-142">授權 hello 決策 tooenable 或封鎖存取 tooa 資源的存取原則。</span><span class="sxs-lookup"><span data-stu-id="658cd-142">Authorization, hello decision tooenable or block access tooa resource with an access policy.</span></span>

<span data-ttu-id="658cd-143">當使用 Azure AD toomanage 應用程式，並啟用 SSO:</span><span class="sxs-lookup"><span data-stu-id="658cd-143">When using Azure AD toomanage applications and enable SSO:</span></span>

* <span data-ttu-id="658cd-144">在 hello 使用者在內部部署 (例如 AD) 或 Azure AD 帳戶進行驗證。</span><span class="sxs-lookup"><span data-stu-id="658cd-144">Authentication is done on hello user’s on-premises (e.g. AD) or Azure AD account.</span></span>
* <span data-ttu-id="658cd-145">上 hello Azure AD 指派和保護原則確保一致的使用者體驗及 tooadd 指派、 位置及 MFA 的條件之任何應用程式，不論其內部的功能，讓您執行授權。</span><span class="sxs-lookup"><span data-stu-id="658cd-145">Authorization executes on hello Azure AD assignment and protection policy ensuring consistent end user experience and enabling you tooadd assignment, locations, and MFA conditions on any application, regardless of its internal capabilities.</span></span>

<span data-ttu-id="658cd-146">它重要 hello 方式 hello 授權的 toounderstand 職務 hello 目標應用程式會根據 hello 應用程式已與 Azure AD 整合的方式而有所不同。</span><span class="sxs-lookup"><span data-stu-id="658cd-146">It important toounderstand that hello way hello authorization is enacted on hello target application varies depending on how hello application was integrated with Azure AD.</span></span>

* <span data-ttu-id="658cd-147">**由服務提供者預先整合應用程式** ：如同 Office 365 和 Azure，這些應用程式都是直接在 Azure AD 上建置並仰賴其完整的身分識別和存取管理功能。</span><span class="sxs-lookup"><span data-stu-id="658cd-147">**Applications pre-integrated by service provider** Like Office 365 and Azure, these are applications built directly on Azure AD and relying on it for their comprehensive identity and access management capabilities.</span></span> <span data-ttu-id="658cd-148">存取 toothese 應用程式是透過目錄資訊和語彙基元發行啟用。</span><span class="sxs-lookup"><span data-stu-id="658cd-148">Access toothese applications is enabled through directory information and token issuance.</span></span>
* <span data-ttu-id="658cd-149">**由 Microsoft 預先整合的應用程式和自訂應用程式** ：這些是依賴內部應用程式目錄並可獨立於 Azure AD 運作的獨立雲端應用程式。</span><span class="sxs-lookup"><span data-stu-id="658cd-149">**Applications pre-integrated by Microsoft and custom applications** These are independent cloud applications that rely on an internal application directory and can operate independently of Azure AD.</span></span> <span data-ttu-id="658cd-150">存取 toothese 應用程式會啟用發行應用程式特定的認證對應 tooan 應用程式帳戶。</span><span class="sxs-lookup"><span data-stu-id="658cd-150">Access toothese applications is enabled by issuing an application specific credential mapped tooan application account.</span></span> <span data-ttu-id="658cd-151">Hello 應用程式功能，依據 hello 認證可能同盟語彙基元或使用者名稱和先前在 hello 應用程式佈建的帳戶密碼。</span><span class="sxs-lookup"><span data-stu-id="658cd-151">Depending on hello application capabilities, hello credential may be a federation token or user-name and password for an account that was previously provisioned in hello application.</span></span>
* <span data-ttu-id="658cd-152">**在內部部署應用程式**透過主要讓存取 tooon 內部部署應用程式的 hello Azure AD application proxy 發行應用程式。</span><span class="sxs-lookup"><span data-stu-id="658cd-152">**On-premises applications** Applications published through hello Azure AD application proxy primarily enabling access tooon-premises applications.</span></span> <span data-ttu-id="658cd-153">這些應用程式依賴於 Windows Server Active Directory 之類的內部部署目錄中心。</span><span class="sxs-lookup"><span data-stu-id="658cd-153">These applications rely on a central on-premises directory like Windows Server Active Directory.</span></span> <span data-ttu-id="658cd-154">存取 toothese 應用程式會啟用觸發 hello proxy toodeliver hello 應用程式內容 toohello 終端使用者同時接受在內部部署的 hello 登入需求。</span><span class="sxs-lookup"><span data-stu-id="658cd-154">Access toothese applications is enabled by triggering hello proxy toodeliver hello application content toohello end user while honoring hello on-premises sign-on requirement.</span></span>

<span data-ttu-id="658cd-155">例如，如果使用者加入您的組織，您需要 toocreate 帳戶 hello 使用者 hello 主要登入作業的 Azure AD 中。</span><span class="sxs-lookup"><span data-stu-id="658cd-155">For example, if a user joins your organization, you need toocreate an account for hello user in Azure AD for hello primary sign-on operations.</span></span> <span data-ttu-id="658cd-156">如果這位使用者需要存取 tooa 受管理應用程式，例如 Salesforce，您也需要 toocreate 帳戶在 Salesforce 中的這個使用者，並連結到 toohello Azure 帳戶 toomake SSO 工作。</span><span class="sxs-lookup"><span data-stu-id="658cd-156">If this user requires access tooa managed application such as Salesforce, you also need toocreate an account for this user in Salesforce and link it toohello Azure account toomake SSO work.</span></span> <span data-ttu-id="658cd-157">當 hello 使用者離開公司時，它是建議 toodelete hello Azure AD 帳戶，而且中的所有對等項目的帳戶 hello IAM hello hello 使用者具有存取權的應用程式存放區。</span><span class="sxs-lookup"><span data-stu-id="658cd-157">When hello user leaves your organization, it is advisable toodelete hello Azure AD account and all counterpart accounts in hello IAM stores of hello applications hello user had access to.</span></span>

## <a name="access-detection"></a><span data-ttu-id="658cd-158">存取偵測</span><span class="sxs-lookup"><span data-stu-id="658cd-158">Access detection</span></span>
<span data-ttu-id="658cd-159">現代企業 IT 部門通常不會察覺所有 hello 雲端應用程式所使用的。</span><span class="sxs-lookup"><span data-stu-id="658cd-159">In modern enterprises, IT departments are often not aware of all hello cloud applications that are being used.</span></span> <span data-ttu-id="658cd-160">Cloud App Discovery 搭配，Azure AD 提供您方案 toodetect 這些應用程式。</span><span class="sxs-lookup"><span data-stu-id="658cd-160">In conjunction with Cloud App Discovery, Azure AD provides you with a solution toodetect these applications.</span></span>

## <a name="account-management"></a><span data-ttu-id="658cd-161">帳戶管理</span><span class="sxs-lookup"><span data-stu-id="658cd-161">Account management</span></span>
<span data-ttu-id="658cd-162">傳統上，管理帳戶在 hello 各種應用程式是手動程序所執行 IT 或支援 hello 組織中個人。</span><span class="sxs-lookup"><span data-stu-id="658cd-162">Traditionally, managing accounts in hello various applications is a manual process performed by IT or support personal in hello organization.</span></span> <span data-ttu-id="658cd-163">Azure AD 將跨所有服務提供者整合的應用程式和由 Microsoft 預先整合的這些應用程式的帳戶管理完全自動化，可支援自動化使用者佈建或 SAML JIT。</span><span class="sxs-lookup"><span data-stu-id="658cd-163">Azure AD fully automated account management across all service provider integrated applications and those applications pre-integrated by Microsoft supporting automated user provisioning or SAML JIT.</span></span>

## <a name="automated-user-provisioning"></a><span data-ttu-id="658cd-164">自動的使用者佈建</span><span class="sxs-lookup"><span data-stu-id="658cd-164">Automated user provisioning</span></span>
<span data-ttu-id="658cd-165">某些應用程式提供自動化介面用於建立和移除 (或停用) 帳戶。</span><span class="sxs-lookup"><span data-stu-id="658cd-165">Some applications provide automation interfaces for creation and removal (or deactivation) of accounts.</span></span> <span data-ttu-id="658cd-166">如果有提供者提供這樣的介面，Azure AD 會加以利用。</span><span class="sxs-lookup"><span data-stu-id="658cd-166">If a provider offers such an interface, it is leveraged by Azure AD.</span></span> <span data-ttu-id="658cd-167">這可減少您的營運成本，因為系統管理工作會自動發生，並改善您環境的 hello 安全性，因為它降低 hello 機率未經授權的存取。</span><span class="sxs-lookup"><span data-stu-id="658cd-167">This reduces your operational costs because administrative tasks happen automatically, and improves hello security of your environment because it decreases hello chance of unauthorized access.</span></span>

## <a name="access-management"></a><span data-ttu-id="658cd-168">存取管理</span><span class="sxs-lookup"><span data-stu-id="658cd-168">Access management</span></span>
<span data-ttu-id="658cd-169">您可以使用 Azure AD 管理存取 tooapplications 使用個別或規則驅動的指派。</span><span class="sxs-lookup"><span data-stu-id="658cd-169">Using Azure AD you can manage access tooapplications using individual or rule driven assignments.</span></span> <span data-ttu-id="658cd-170">您也可以委派存取管理 toohello 適當的人員在 hello 組織確保 hello 最佳監督和降低技術服務人員 hello 負擔。</span><span class="sxs-lookup"><span data-stu-id="658cd-170">You can also delegate access management toohello right people in hello organization ensuring hello best oversight and reducing hello burden on helpdesk.</span></span>

## <a name="on-premises-applications"></a><span data-ttu-id="658cd-171">內部應用程式</span><span class="sxs-lookup"><span data-stu-id="658cd-171">On-premises applications</span></span>
<span data-ttu-id="658cd-172">內建的應用程式 proxy 的 hello 可讓您 toopublish 兩者一致導致您在內部部署的應用程式 tooyour 使用者存取現代化雲端應用程式和 hello 優點的經驗從 Azure AD 監視、 報告和安全性功能.</span><span class="sxs-lookup"><span data-stu-id="658cd-172">hello built in application proxy enables you toopublish your on-premises applications tooyour users resulting in both consistent access experience with modern cloud application and hello benefits from Azure AD monitoring, reporting, and security capabilities.</span></span>

## <a name="reporting-and-monitoring"></a><span data-ttu-id="658cd-173">報告和監控</span><span class="sxs-lookup"><span data-stu-id="658cd-173">Reporting and monitoring</span></span>
<span data-ttu-id="658cd-174">Azure AD 提供預先整合的報告和監控功能，可讓您 tooknow 誰可以存取 tooapplications 和當他們實際使用它們。</span><span class="sxs-lookup"><span data-stu-id="658cd-174">Azure AD provides you with pre-integrated reporting and monitoring capabilities that enable you tooknow who has access tooapplications and when they actually used them.</span></span>

## <a name="related-capabilities"></a><span data-ttu-id="658cd-175">相關功能</span><span class="sxs-lookup"><span data-stu-id="658cd-175">Related capabilities</span></span>
<span data-ttu-id="658cd-176">您可以使用 Azure AD 透過更細微的存取原則和預先整合的 MFA 來保護您的應用程式。</span><span class="sxs-lookup"><span data-stu-id="658cd-176">With Azure AD you can secure your applications with granular access policies and pre-integrated MFA.</span></span> <span data-ttu-id="658cd-177">有關 Azure MFA 的詳細資訊請參閱的 toolearn [Azure MFA](https://azure.microsoft.com/services/multi-factor-authentication/)。</span><span class="sxs-lookup"><span data-stu-id="658cd-177">toolearn more about Azure MFA see [Azure MFA](https://azure.microsoft.com/services/multi-factor-authentication/).</span></span>

## <a name="getting-started"></a><span data-ttu-id="658cd-178">開始使用</span><span class="sxs-lookup"><span data-stu-id="658cd-178">Getting started</span></span>
<span data-ttu-id="658cd-179">tooget 啟動整合應用程式與 Azure AD，看看 hello[整合 Azure Active Directory 與取得的應用程式啟動指南](active-directory-integrating-applications-getting-started.md)。</span><span class="sxs-lookup"><span data-stu-id="658cd-179">tooget started integrating applications with Azure AD, take a look at hello [Integrating Azure Active Directory with applications getting started guide](active-directory-integrating-applications-getting-started.md).</span></span>

## <a name="see-also"></a><span data-ttu-id="658cd-180">另請參閱</span><span class="sxs-lookup"><span data-stu-id="658cd-180">See also</span></span>
[<span data-ttu-id="658cd-181">Article Index for Application Management in Azure Active Directory (Azure Active Directory 中應用程式管理的文件索引)</span><span class="sxs-lookup"><span data-stu-id="658cd-181">Article Index for Application Management in Azure Active Directory</span></span>](active-directory-apps-index.md)

