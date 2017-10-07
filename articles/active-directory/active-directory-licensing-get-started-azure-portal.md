---
title: "aaaGet 開始使用 Azure Active Directory 中授權 |Microsoft 文件"
description: "Azure Active Directory 授權的運作方式 tooget 啟動方式最佳做法"
services: active-directory
keywords: "Azure AD 授權"
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: 
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/26/2017
ms.author: curtand
ms.reviewer: piotrci
ms.custom: H1Hack27Feb2017;it-pro
ms.openlocfilehash: 268dab806b8b959790341d630a0355c6a43871d0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="license-yourself-and-your-users-in-azure-active-directory"></a><span data-ttu-id="047c0-104">在 Azure Active Directory 中進行自身和使用者的授權</span><span class="sxs-lookup"><span data-stu-id="047c0-104">License yourself and your users in Azure Active Directory</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="047c0-105">Azure 入口網站指示</span><span class="sxs-lookup"><span data-stu-id="047c0-105">Azure portal instructions</span></span>](active-directory-licensing-get-started-azure-portal.md)
> * [<span data-ttu-id="047c0-106">取得 Azure 傳統入口網站的資訊</span><span class="sxs-lookup"><span data-stu-id="047c0-106">Get Azure classic portal info</span></span>](active-directory-licensing-what-is.md)
>
>

<span data-ttu-id="047c0-107">Azure Active Directory (Azure AD) 是 Microsoft 的「身分識別即服務 (IDaaS)」解決方案與平台。</span><span class="sxs-lookup"><span data-stu-id="047c0-107">Azure Active Directory (Azure AD) is an identity as a service (IDaaS) solution and platform from Microsoft.</span></span> <span data-ttu-id="047c0-108">Microsoft 在不同的服務版本中提供 Azure AD：</span><span class="sxs-lookup"><span data-stu-id="047c0-108">Azure AD is offered in different service editions:</span></span>

* <span data-ttu-id="047c0-109">Azure Active Directory Free，任何 Microsoft 服務 (例如 Office 365、Dynamics、Microsoft Intune 或 Azure) 均提供此版本。</span><span class="sxs-lookup"><span data-stu-id="047c0-109">Azure Active Directory Free, which is available with any Microsoft service such as Office 365, Dynamics, Microsoft Intune, or Azure.</span></span> <span data-ttu-id="047c0-110">在此模式中，Azure AD 不會產生任何使用費用。</span><span class="sxs-lookup"><span data-stu-id="047c0-110">Azure AD does not generate any consumption charges in this mode.</span></span>

* <span data-ttu-id="047c0-111">Azure AD 付費版本，例如：</span><span class="sxs-lookup"><span data-stu-id="047c0-111">Azure AD paid editions, such as:</span></span>
  - <span data-ttu-id="047c0-112">Enterprise Mobility + Security</span><span class="sxs-lookup"><span data-stu-id="047c0-112">Enterprise Mobility + Security</span></span> 
  - <span data-ttu-id="047c0-113">Azure AD Premium (P1 和 P2)</span><span class="sxs-lookup"><span data-stu-id="047c0-113">Azure AD Premium (P1 and P2)</span></span>
  - <span data-ttu-id="047c0-114">Azure AD Basic</span><span class="sxs-lookup"><span data-stu-id="047c0-114">Azure AD Basic</span></span>
  - <span data-ttu-id="047c0-115">Azure Multi-Factor Authentication</span><span class="sxs-lookup"><span data-stu-id="047c0-115">Azure Multi-Factor Authentication</span></span>

<span data-ttu-id="047c0-116">如同許多 Microsoft 線上服務一般，大多數 Azure AD 付費版本都是透過賦予每位使用者權利來提供，就像在 Office 365、Microsoft Intune 和 Azure AD 中一樣。</span><span class="sxs-lookup"><span data-stu-id="047c0-116">Like many of Microsoft online services, most Azure AD paid versions are delivered through per-user entitlements as they are in Office 365, Microsoft Intune, and Azure AD.</span></span> <span data-ttu-id="047c0-117">在這些情況下，購買 hello 服務由一或多個訂用帳戶，每個訂用帳戶包含您租用戶中的某些 prepurchased 的授權。</span><span class="sxs-lookup"><span data-stu-id="047c0-117">In these cases, hello service purchase is represented by one or more subscriptions, and each subscription includes some prepurchased licenses in your tenant.</span></span> <span data-ttu-id="047c0-118">您可透過下列方式來賦予每位使用者權利：</span><span class="sxs-lookup"><span data-stu-id="047c0-118">Per-user entitlements are achieved by:</span></span>

* <span data-ttu-id="047c0-119">指派授權。</span><span class="sxs-lookup"><span data-stu-id="047c0-119">Assigning a license.</span></span> 
* <span data-ttu-id="047c0-120">建立 hello 使用者與 hello 產品之間的連結。</span><span class="sxs-lookup"><span data-stu-id="047c0-120">Creating a link between hello user and hello product.</span></span>
* <span data-ttu-id="047c0-121">啟用 hello hello 使用者的服務元件。</span><span class="sxs-lookup"><span data-stu-id="047c0-121">Enabling hello service components for hello user.</span></span>
* <span data-ttu-id="047c0-122">使用一 hello 預付授權。</span><span class="sxs-lookup"><span data-stu-id="047c0-122">Consuming one of hello prepaid licenses.</span></span>

[<span data-ttu-id="047c0-123">立即試用 Azure AD Premium。</span><span class="sxs-lookup"><span data-stu-id="047c0-123">Try Azure AD Premium now.</span></span>](https://portal.office.com/Signup/Signup.aspx?OfferId=01824d11-5ad8-447f-8523-666b0848b381&ali=1#0)

<span data-ttu-id="047c0-124">如需 Azure AD 服務功能的一般概觀，請參閱[什麼是 Azure AD？](active-directory-whatis.md)。</span><span class="sxs-lookup"><span data-stu-id="047c0-124">For a broad overview of Azure AD service capabilities, see [What is Azure AD?](active-directory-whatis.md).</span></span> <span data-ttu-id="047c0-125">如需詳細資訊，請參閱[服務等級協定頁面](https://azure.microsoft.com/support/legal/sla/active-directory/v1_0/)。</span><span class="sxs-lookup"><span data-stu-id="047c0-125">For more information, see our [Service Level Agreements page](https://azure.microsoft.com/support/legal/sla/active-directory/v1_0/).</span></span>

> [!NOTE]
> <span data-ttu-id="047c0-126">Azure 隨用隨付訂用帳戶啟用 Azure 資源的建立，並再將它們對應 tooyour 付款方法。</span><span class="sxs-lookup"><span data-stu-id="047c0-126">Azure pay-as-you-go subscriptions enable creation of Azure resources and then map them tooyour payment method.</span></span> <span data-ttu-id="047c0-127">沒有任何與 hello 訂用帳戶相關聯的授權計數。</span><span class="sxs-lookup"><span data-stu-id="047c0-127">There are no license counts associated with hello subscription.</span></span> <span data-ttu-id="047c0-128">當您授與 Azure 資源上的使用者權限 toooperate 對應 toohello 訂用帳戶時，它們與 hello 訂用帳戶相關聯而且可以管理訂用帳戶的資源。</span><span class="sxs-lookup"><span data-stu-id="047c0-128">When you grant a user permission toooperate on Azure resources mapped toohello subscription, they are associated with hello subscription and can manage subscription resources.</span></span>

## <a name="how-does-azure-active-directory-licensing-work"></a><span data-ttu-id="047c0-129">Azure Active Directory 授權的運作方式為何？</span><span class="sxs-lookup"><span data-stu-id="047c0-129">How does Azure Active Directory licensing work?</span></span>

<span data-ttu-id="047c0-130">以授權為基礎的 Azure AD 服務可透過在 Azure AD 服務租用戶中啟用訂用帳戶來開始運作。</span><span class="sxs-lookup"><span data-stu-id="047c0-130">License-based Azure AD services work by activating a subscription in your Azure AD service tenant.</span></span> <span data-ttu-id="047c0-131">Hello 訂閱在作用中之後，會由 Azure AD 系統管理員管理 hello 服務功能，而且所授權的使用者使用。</span><span class="sxs-lookup"><span data-stu-id="047c0-131">After hello subscription is active, hello service capabilities are managed by Azure AD administrators and used by licensed users.</span></span>

### <a name="manage-subscription-information"></a><span data-ttu-id="047c0-132">管理訂用帳戶資訊</span><span class="sxs-lookup"><span data-stu-id="047c0-132">Manage subscription information</span></span>

<span data-ttu-id="047c0-133">當您購買企業行動力 + 安全性、 Azure AD Premium 或 Azure AD Basic，您的租用戶時，會更新與 hello 訂用帳戶，包括其有效期間內，而且預付授權。</span><span class="sxs-lookup"><span data-stu-id="047c0-133">When you purchase Enterprise Mobility + Security, Azure AD Premium, or Azure AD Basic, your tenant is updated with hello subscription, including its validity period and prepaid licenses.</span></span> <span data-ttu-id="047c0-134">您的訂用帳戶資訊，包括 hello 分派或可用授權數目是透過 Azure 入口網站 hello： 下**Azure Active Directory**，開啟 hello**授權**磚 hello特定的目錄。</span><span class="sxs-lookup"><span data-stu-id="047c0-134">Your subscription information, including hello number of assigned or available licenses, is available through hello Azure portal: Under **Azure Active Directory**, open hello **Licenses** tile for hello specific directory.</span></span> <span data-ttu-id="047c0-135">hello**授權**刀鋒視窗是也 hello 最佳地方 toomanage 授權指派。</span><span class="sxs-lookup"><span data-stu-id="047c0-135">hello **Licenses** blade is also hello best place toomanage your license assignments.</span></span>

<span data-ttu-id="047c0-136">每個訂用帳戶都包含一或多個服務方案，例如 Azure AD、Multi-Factor Authentication、Intune、Exchange Online 或 SharePoint Online。</span><span class="sxs-lookup"><span data-stu-id="047c0-136">Each subscription consists of one or more service plans, such as Azure AD, Multi-Factor Authentication, Intune, Exchange Online, or SharePoint Online.</span></span>  <span data-ttu-id="047c0-137">Azure AD 授權的管理「不」需要進行服務方案等級的管理。</span><span class="sxs-lookup"><span data-stu-id="047c0-137">Azure AD license management does *not* require service-plan-level management.</span></span> <span data-ttu-id="047c0-138">與 office 365 的不同，因為它會仰賴此進階的組態模式 toomanage 存取 tooincluded 服務。</span><span class="sxs-lookup"><span data-stu-id="047c0-138">Office 365 differs because it relies on this advanced configuration mode toomanage access tooincluded services.</span></span> <span data-ttu-id="047c0-139">Azure AD 會依賴服務中組態 tooenable 功能，並管理個別的權限。</span><span class="sxs-lookup"><span data-stu-id="047c0-139">Azure AD relies on in-service configuration tooenable features and manage individual permissions.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="047c0-140">Azure AD Premium、 Azure AD Basic 和企業行動力 + 安全性訂用帳戶會佈建的局部的 tootheir 目錄租用戶。</span><span class="sxs-lookup"><span data-stu-id="047c0-140">Azure AD Premium, Azure AD Basic, and Enterprise Mobility + Security subscriptions are confined tootheir provisioned directory/tenant.</span></span> <span data-ttu-id="047c0-141">訂用帳戶無法目錄或其他目錄中的使用的 tooentitle 使用者之間分割。</span><span class="sxs-lookup"><span data-stu-id="047c0-141">Subscriptions cannot be split between directories or used tooentitle users in other directories.</span></span> <span data-ttu-id="047c0-142">您可以在不同目錄之間移動訂用帳戶，但需要提交支援票證，或者，您也可以先取消再重新購買，來直接購買訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="047c0-142">Moving a subscription between directories is possible, but requires submitting a support ticket, or cancellation and repurchase for direct purchases.</span></span>
>
> <span data-ttu-id="047c0-143">當 Azure AD 或 Enterprise Mobility + Security 採購自大量授權的訂閱，並啟用當 hello 協議包含其他 Microsoft Online services (例如，Office 365) 時，會自動發生。</span><span class="sxs-lookup"><span data-stu-id="047c0-143">When Azure AD or Enterprise Mobility + Security is purchased through a Volume Licensing subscription, and when hello agreement includes other Microsoft Online services (for example, Office 365), activation happens automatically.</span></span> 

### <a name="assign-licenses"></a><span data-ttu-id="047c0-144">指派授權</span><span class="sxs-lookup"><span data-stu-id="047c0-144">Assign licenses</span></span>

<span data-ttu-id="047c0-145">取得訂用帳戶是所有您需要付費功能 tooconfigure，雖然您仍然必須將授權發佈的 Azure AD 的付費功能 toousers。</span><span class="sxs-lookup"><span data-stu-id="047c0-145">Although obtaining a subscription is all you need tooconfigure paid capabilities, you must still distribute licenses for Azure AD paid features toousers.</span></span> <span data-ttu-id="047c0-146">任何使用者都應該具有存取 tooor 透過 Azure AD 的付費功能管理人員必須指派授權。</span><span class="sxs-lookup"><span data-stu-id="047c0-146">Any user who should have access tooor who is managed through an Azure AD paid feature must be assigned a license.</span></span> <span data-ttu-id="047c0-147">授權指派是一種使用者與購買的服務 (例如 Azure AD Premium、Basic 或 Enterprise Mobility + Security) 之間的對應。</span><span class="sxs-lookup"><span data-stu-id="047c0-147">License assignment is a mapping between a user and a purchased service, such as Azure AD Premium, Basic, or Enterprise Mobility + Security.</span></span>


<span data-ttu-id="047c0-148">您可以透過下列方式來管理目錄中應該擁有授權的使用者：</span><span class="sxs-lookup"><span data-stu-id="047c0-148">Managing which users in your directory should have a license can be accomplished by:</span></span> 

* <span data-ttu-id="047c0-149">指派授權在 hello toogroups [Azure 入口網站](active-directory-licensing-whatis-azure-portal.md)。</span><span class="sxs-lookup"><span data-stu-id="047c0-149">Assigning licenses toogroups in hello [Azure portal](active-directory-licensing-whatis-azure-portal.md).</span></span>
* <span data-ttu-id="047c0-150">指派授權直接 toousers 透過 hello 入口網站、 PowerShell 或應用程式開發介面。</span><span class="sxs-lookup"><span data-stu-id="047c0-150">Assigning licenses directly toousers by way of hello portal, PowerShell, or APIs.</span></span> 

<span data-ttu-id="047c0-151">您指派授權 tooa 群組時，所有群組成員已都獲得授權。</span><span class="sxs-lookup"><span data-stu-id="047c0-151">When you're assigning licenses tooa group, all group members are assigned a license.</span></span> <span data-ttu-id="047c0-152">如果新增或從 hello 群組中移除使用者，hello 適當授權指派，或移除。</span><span class="sxs-lookup"><span data-stu-id="047c0-152">If users are added or removed from hello group, hello appropriate license is assigned or removed.</span></span> <span data-ttu-id="047c0-153">群組指派可以利用任何群組管理列印可用 tooyou，而且與以群組為基礎的指派 tooapplications 一致。</span><span class="sxs-lookup"><span data-stu-id="047c0-153">Group assignment can utilize any group management available tooyou, and it is consistent with group-based assignment tooapplications.</span></span>

<span data-ttu-id="047c0-154">您可以使用[群組為基礎的授權指派](active-directory-licensing-whatis-azure-portal.md)tooset hello 如下的規則：</span><span class="sxs-lookup"><span data-stu-id="047c0-154">You can use [group-based license assignment](active-directory-licensing-whatis-azure-portal.md) tooset up rules such as hello following:</span></span>
* <span data-ttu-id="047c0-155">目錄中的所有使用者都自動取得授權</span><span class="sxs-lookup"><span data-stu-id="047c0-155">All users in your directory automatically get a license</span></span>
* <span data-ttu-id="047c0-156">Everyone 具有 hello 適當職稱取得授權</span><span class="sxs-lookup"><span data-stu-id="047c0-156">Everyone with hello appropriate job title gets a license</span></span>
* <span data-ttu-id="047c0-157">您可以將委派 hello 組織中的 hello 決策 tooother 管理員 (使用[自助群組](active-directory-accessmanagement-self-service-group-management.md))</span><span class="sxs-lookup"><span data-stu-id="047c0-157">You can delegate hello decision tooother managers in hello organization (by using [self-service groups](active-directory-accessmanagement-self-service-group-management.md))</span></span>

<span data-ttu-id="047c0-158">如需授權指派 toogroups 詳細討論，包括進階的案例和 Office 365 授權的情況下，請參閱[指派授權 Azure Active Directory 中的群組成員資格 toousers](active-directory-licensing-group-assignment-azure-portal.md)。</span><span class="sxs-lookup"><span data-stu-id="047c0-158">For a detailed discussion of license assignment toogroups, including advanced scenarios and Office 365 licensing scenarios, see [Assign licenses toousers by group membership in Azure Active Directory](active-directory-licensing-group-assignment-azure-portal.md).</span></span>

## <a name="get-started-with-azure-ad-licensing"></a><span data-ttu-id="047c0-159">開始使用 Azure AD 授權</span><span class="sxs-lookup"><span data-stu-id="047c0-159">Get started with Azure AD licensing</span></span>

<span data-ttu-id="047c0-160">Azure AD 很容易就能開始使用。</span><span class="sxs-lookup"><span data-stu-id="047c0-160">Getting started with Azure AD is easy.</span></span> <span data-ttu-id="047c0-161">在註冊 [Azure 免費試用](https://azure.microsoft.com/offers/ms-azr-0044p/)的過程中，您就可以建立您的目錄。</span><span class="sxs-lookup"><span data-stu-id="047c0-161">You can always create your directory as a part of signing up for an [Azure free trial](https://azure.microsoft.com/offers/ms-azr-0044p/).</span></span>

<span data-ttu-id="047c0-162">hello 下列最佳作法可協助確保您的租用戶會對齊您可能會耗用其他 Microsoft 服務與您的目標 hello 服務：</span><span class="sxs-lookup"><span data-stu-id="047c0-162">hello following best practices can help ensure that your tenant is aligned with other Microsoft services you might be consuming and with your goals for hello service:</span></span>

- <span data-ttu-id="047c0-163">如果您已經在使用任何 Microsoft hello 組織服務，您已經有 Azure AD 租用戶。</span><span class="sxs-lookup"><span data-stu-id="047c0-163">If you are already using any of hello organizational services from Microsoft, you already have an Azure AD tenant.</span></span> <span data-ttu-id="047c0-164">有用的 toouse hello 相同租用戶的其他服務，以便核心身分識別管理，包括佈建和混合式單一登入 (SSO)，可以在 hello 服務間使用它。</span><span class="sxs-lookup"><span data-stu-id="047c0-164">It is useful toouse hello same tenant for other services so that core identity management, including provisioning and hybrid single sign-on (SSO), can be used across hello services.</span></span> <span data-ttu-id="047c0-165">搭配單一登入，您的使用者從 hello 豐富功能獲益跨 hello 服務。</span><span class="sxs-lookup"><span data-stu-id="047c0-165">With single sign-on, your users benefit from hello rich capabilities across hello services.</span></span> <span data-ttu-id="047c0-166">因此，如果您決定 toobuy 您公司的 Azure AD 的付費服務，我們建議您使用相同的一次租用戶的 hello。</span><span class="sxs-lookup"><span data-stu-id="047c0-166">Thus, if you decide toobuy an Azure AD paid service for your workforce, we recommend that you use hello same tenant again.</span></span>

- <span data-ttu-id="047c0-167">我們建議您在 hello Azure 入口網站中使用新的租用戶，如果您計劃：</span><span class="sxs-lookup"><span data-stu-id="047c0-167">We recommend that you use a new tenant in hello Azure portal if you are planning to:</span></span>
  - <span data-ttu-id="047c0-168">對一組不同的使用者 (例如夥伴或客戶) 使用 Azure AD。</span><span class="sxs-lookup"><span data-stu-id="047c0-168">Use Azure AD for a different set of users (such as partners or customers).</span></span>
  - <span data-ttu-id="047c0-169">在與生產服務隔離的環境中評估 Azure AD 服務。</span><span class="sxs-lookup"><span data-stu-id="047c0-169">Evaluate Azure AD services in isolation from your production service.</span></span>
  - <span data-ttu-id="047c0-170">為服務設置沙箱環境。</span><span class="sxs-lookup"><span data-stu-id="047c0-170">Set up a sandbox environment for your services.</span></span>

  <span data-ttu-id="047c0-171">使用您的帳戶建立 hello 新目錄全域系統管理員權限與外部使用者的身分。</span><span class="sxs-lookup"><span data-stu-id="047c0-171">hello new directory is created with your account as an external user with global administrator permissions.</span></span> <span data-ttu-id="047c0-172">當您登入 toohello 與此帳戶的 Azure 入口網站時，您可以看到此租用戶，並存取所有系統管理工作。</span><span class="sxs-lookup"><span data-stu-id="047c0-172">When you sign in toohello Azure portal with this account, you can see this tenant and access all administration tasks.</span></span>

> [!NOTE]
> <span data-ttu-id="047c0-173">Azure AD 支援「來賓使用者」，也就是 Azure AD 租用戶中的使用者帳戶，這些帳戶是透過 Microsoft 帳戶或另一個租用戶中的 Azure AD 身分識別所建立。</span><span class="sxs-lookup"><span data-stu-id="047c0-173">Azure AD supports “guest users,” which are user accounts in an Azure AD tenant that were created through either a Microsoft account or an Azure AD identity from another tenant.</span></span> <span data-ttu-id="047c0-174">hello Office 365 系統管理入口網站目前不支援這些使用者。</span><span class="sxs-lookup"><span data-stu-id="047c0-174">hello Office 365 administration portal does not currently support these users.</span></span> <span data-ttu-id="047c0-175">Microsoft 帳戶與 Guest 使用者，則無法無法 tooaccess hello Office 365 系統管理入口網站，從其他 Azure AD 租用戶的來賓使用者會被忽略。</span><span class="sxs-lookup"><span data-stu-id="047c0-175">Guest users with Microsoft accounts are not able tooaccess hello Office 365 administration portal at all, while guest users from other Azure AD tenants are ignored.</span></span> <span data-ttu-id="047c0-176">在 hello 後者的情況下，只有 hello 使用者的本機帳戶，請在 hello Azure AD 或 hello 使用者最初建立所在，Office 365 租用戶存取。</span><span class="sxs-lookup"><span data-stu-id="047c0-176">In hello latter case, only hello user’s local account, in hello Azure AD or Office 365 tenant where hello user was originally created, is accessible.</span></span>

### <a name="select-one-or-more-license-trials"></a><span data-ttu-id="047c0-177">選取一或多個授權試用版</span><span class="sxs-lookup"><span data-stu-id="047c0-177">Select one or more license trials</span></span>

<span data-ttu-id="047c0-178">您可以在 [Azure Active Directory] &gt; [快速啟動] 下啟用 Azure AD Premium 或 Enterprise Mobility + Security 試用版訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="047c0-178">You can activate an Azure AD Premium or Enterprise Mobility + Security trial subscription under **Azure Active Directory** &gt; **Quick start**.</span></span>

![選取授權試用版](media/active-directory-licensing-get-started-azure-portal/select-a-license-trial.png)

<span data-ttu-id="047c0-180">試用版授權位於 hello**授權**刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="047c0-180">Trial licenses are available on hello **Licenses** blade.</span></span>

### <a name="assign-licenses-toousers-and-groups"></a><span data-ttu-id="047c0-181">指派授權 toousers 和群組</span><span class="sxs-lookup"><span data-stu-id="047c0-181">Assign licenses toousers and groups</span></span>

<span data-ttu-id="047c0-182">Hello 訂閱為作用狀態後，您應該指派授權 tooyourself。</span><span class="sxs-lookup"><span data-stu-id="047c0-182">After hello subscription is active, you should assign a license tooyourself.</span></span> <span data-ttu-id="047c0-183">然後重新整理 hello 瀏覽器 tooensure 看到 hello 的所有功能。</span><span class="sxs-lookup"><span data-stu-id="047c0-183">Then refresh hello browser tooensure that you are seeing all hello features.</span></span> <span data-ttu-id="047c0-184">hello 下一個步驟是 tooassign 授權 toohello 使用者需要存取 toopaid Azure AD 功能。</span><span class="sxs-lookup"><span data-stu-id="047c0-184">hello next step is tooassign licenses toohello users who need access toopaid Azure AD features.</span></span> <span data-ttu-id="047c0-185">中所述[指派授權](#assign-licenses)、 tooassign 授權是代表 hello tooidentify hello 群組想要的對象與指派 hello 授權 tooit 的簡單方式。</span><span class="sxs-lookup"><span data-stu-id="047c0-185">As described in [Assign licenses](#assign-licenses), one easy way tooassign licenses is tooidentify hello group representing hello desired audience and assign hello license tooit.</span></span> <span data-ttu-id="047c0-186">如此一來，使用者加入或移除從 hello 群組在其生命週期會指派，或分別移除 hello 授權。</span><span class="sxs-lookup"><span data-stu-id="047c0-186">In this way, users who are added or removed from hello group over its lifecycle are assigned or removed from hello license, respectively.</span></span>

> [!NOTE]
> <span data-ttu-id="047c0-187">並非所有位置都可使用某些 Microsoft 服務。</span><span class="sxs-lookup"><span data-stu-id="047c0-187">Some Microsoft services are not available in all locations.</span></span> <span data-ttu-id="047c0-188">Hello 管理員 tooa 使用者可以指派授權之前，必須指定 hello**使用位置**hello 使用者的屬性。</span><span class="sxs-lookup"><span data-stu-id="047c0-188">Before a license can be assigned tooa user, hello administrator must specify hello **Usage location** property for hello user.</span></span> <span data-ttu-id="047c0-189">您可以設定此屬性在**使用者** &gt; **設定檔** &gt; **設定**hello Azure 入口網站中。</span><span class="sxs-lookup"><span data-stu-id="047c0-189">You can set this property under **User** &gt; **Profile** &gt; **Settings** in hello Azure portal.</span></span> <span data-ttu-id="047c0-190">當使用群組授權指派，其使用位置未指定任何使用者會繼承 hello hello 目錄位置。</span><span class="sxs-lookup"><span data-stu-id="047c0-190">When using group license assignment, any user whose usage location is not specified inherits hello location of hello directory.</span></span>

<span data-ttu-id="047c0-191">tooassign 授權下**Azure Active Directory** &gt; **授權** &gt; **所有產品**，選取一或多個產品，然後選取**指派**hello 命令列上。</span><span class="sxs-lookup"><span data-stu-id="047c0-191">tooassign a license, under **Azure Active Directory** &gt; **Licenses** &gt; **All Products**, select one or more products, and then select **Assign** on hello command bar.</span></span>

![選取授權 tooassign](media/active-directory-licensing-get-started-azure-portal/select-license-to-assign.png)

<span data-ttu-id="047c0-193">您可以使用 hello**使用者和群組**刀鋒視窗 toochoose hello 產品中的多個使用者或群組或 toodisable 服務計劃。</span><span class="sxs-lookup"><span data-stu-id="047c0-193">You can use hello **Users and groups** blade toochoose multiple users or groups or toodisable service plans in hello product.</span></span> <span data-ttu-id="047c0-194">使用上最上層 toosearch hello [搜尋] 方塊，使用者和群組的名稱。</span><span class="sxs-lookup"><span data-stu-id="047c0-194">Use hello search box on top toosearch for user and group names.</span></span>

![選取要指派授權的使用者或群組](media/active-directory-licensing-get-started-azure-portal/select-user-for-license-assignment.png)

<span data-ttu-id="047c0-196">您指派授權 tooa 群組時，可能需要一些時間才所有使用者都會都繼承 hello 授權，而是根據 hello hello 群組中的使用者數目。</span><span class="sxs-lookup"><span data-stu-id="047c0-196">When you're assigning a license tooa group, it can take some time before all users inherit hello license, depending on hello number of users in hello group.</span></span> <span data-ttu-id="047c0-197">您可以檢查處理狀態 hello hello**群組**刀鋒視窗中的，在 hello**授權**磚。</span><span class="sxs-lookup"><span data-stu-id="047c0-197">You can check hello processing status on hello **Group** blade, under hello **Licenses** tile.</span></span>

![授權指派狀態](media/active-directory-licensing-get-started-azure-portal/license-assignment-status.png)

<span data-ttu-id="047c0-199">在 Azure AD 授權指派期間，可能會發生指派錯誤，但在管理 Azure AD 和 Enterprise Mobility + Security 產品時則相對較少發生。</span><span class="sxs-lookup"><span data-stu-id="047c0-199">Assignment errors can occur during Azure AD license assignment but are relatively rare when managing Azure AD and Enterprise Mobility + Security products.</span></span> <span data-ttu-id="047c0-200">可能發生的指派錯誤僅限於：</span><span class="sxs-lookup"><span data-stu-id="047c0-200">Potential assignment errors are limited to:</span></span>
- <span data-ttu-id="047c0-201">指派衝突： 在使用者先前已指派與 hello 目前的授權不相容的授權。</span><span class="sxs-lookup"><span data-stu-id="047c0-201">Assignment conflict: When a user was previously assigned a license that is incompatible with hello current license.</span></span> <span data-ttu-id="047c0-202">在此情況下，hello 新授權指派，需要移除目前 hello。</span><span class="sxs-lookup"><span data-stu-id="047c0-202">In this case, assigning hello new license requires removing hello current one.</span></span>
- <span data-ttu-id="047c0-203">超過可用的授權： hello 分派群組中的使用者數目超過 hello 可用的授權，使用者的指派狀態會反映失敗 tooassign toomissing 授權到期。</span><span class="sxs-lookup"><span data-stu-id="047c0-203">Exceeded available licenses: When hello number of users in assigned groups exceeds hello available licenses, a user's assignment status reflects a failure tooassign due toomissing licenses.</span></span>

#### <a name="azure-ad-b2b-collaboration-licensing"></a><span data-ttu-id="047c0-204">Azure AD B2B 共同作業授權</span><span class="sxs-lookup"><span data-stu-id="047c0-204">Azure AD B2B collaboration licensing</span></span>

<span data-ttu-id="047c0-205">B2B 共同作業可讓您 tooinvite guest 使用者到 Azure AD 租用戶 tooprovide 存取 tooAzure AD 服務和您將提供任何 Azure 資源。</span><span class="sxs-lookup"><span data-stu-id="047c0-205">B2B collaboration allows you tooinvite guest users into your Azure AD tenant tooprovide access tooAzure AD services and any Azure resources you make available.</span></span>  

<span data-ttu-id="047c0-206">沒有邀請 B2B 使用者並指派它們 tooan 在 Azure AD 中的應用程式需付費。</span><span class="sxs-lookup"><span data-stu-id="047c0-206">There is no charge for inviting B2B users and assigning them tooan application in Azure AD.</span></span> <span data-ttu-id="047c0-207">針對每個來賓 too10 應用程式設定使用者和 3 的基本報告也是 B2B 共同作業的使用者可以免費。</span><span class="sxs-lookup"><span data-stu-id="047c0-207">Up too10 apps per guest user and 3 basic reports are also free for B2B collaboration users.</span></span> <span data-ttu-id="047c0-208">如果 guest 使用者有任何適當的授權指派 hello 夥伴的 Azure AD 租用戶中，它們將會用您以及授權。</span><span class="sxs-lookup"><span data-stu-id="047c0-208">If your guest user has any appropriate licenses assigned in hello partner's Azure AD tenant, they'll be licensed in yours as well.</span></span>

<span data-ttu-id="047c0-209">它不是必要，但如果您想 tooprovide 存取 toopaid Azure AD 功能，這些 B2B 來賓使用者必須獲得授權與適當的 Azure AD 授權。</span><span class="sxs-lookup"><span data-stu-id="047c0-209">It's not required, but if you want tooprovide access toopaid Azure AD features, those B2B guest users must be licensed with appropriate Azure AD licenses.</span></span> <span data-ttu-id="047c0-210">邀請其他租用戶與 Azure AD 的付費授權可以指派 B2B 共同作業的使用者權限受邀 tooan 額外的五個來賓使用者 toohello 租用戶。</span><span class="sxs-lookup"><span data-stu-id="047c0-210">An inviting tenant with an Azure AD paid license can assign B2B collaboration user rights tooan additional five guest users invited toohello tenant.</span></span> <span data-ttu-id="047c0-211">如需這方面的案例和資訊，請參閱 [B2B 共同作業授權指引](active-directory-b2b-licensing.md)。</span><span class="sxs-lookup"><span data-stu-id="047c0-211">For scenarios and information, see [B2B collaboration licensing guidance](active-directory-b2b-licensing.md).</span></span>

### <a name="view-assigned-licenses"></a><span data-ttu-id="047c0-212">檢視已指派的授權</span><span class="sxs-lookup"><span data-stu-id="047c0-212">View assigned licenses</span></span>

<span data-ttu-id="047c0-213">已指派授權和可用授權的摘要檢視會顯示在 [Azure Active Directory] &gt; [授權] &gt; [所有產品] 下。</span><span class="sxs-lookup"><span data-stu-id="047c0-213">A summary view of assigned and available licenses is displayed under **Azure Active Directory** &gt; **Licenses** &gt; **All products**.</span></span>

![檢視授權摘要](media/active-directory-licensing-get-started-azure-portal/view-license-summary.png)

<span data-ttu-id="047c0-215">選取特定產品時，會顯示可用的已指派使用者和群組的詳細清單。</span><span class="sxs-lookup"><span data-stu-id="047c0-215">A detailed list of assigned users and groups is available when selecting a specific product.</span></span> <span data-ttu-id="047c0-216">hello**授權使用者**清單會顯示目前耗用一個授權和是否 hello 授權已直接指派 toohello 使用者，或如果它繼承自群組的所有使用者。</span><span class="sxs-lookup"><span data-stu-id="047c0-216">hello **Licensed Users** list shows all users currently consuming a license and whether hello license was assigned directly toohello user or if it is inherited from a group.</span></span>

![檢視授權詳細資料](media/active-directory-licensing-get-started-azure-portal/view-license-detail.png)

<span data-ttu-id="047c0-218">同樣地，hello**授權群組**清單會顯示所有群組已指派給 toowhich 授權。</span><span class="sxs-lookup"><span data-stu-id="047c0-218">Similarly, hello **Licensed Groups** list shows all groups toowhich licenses have been assigned.</span></span> <span data-ttu-id="047c0-219">選取使用者或群組的 tooopen hello**授權**刀鋒視窗中，會顯示所有授權指派給 toothat 物件。</span><span class="sxs-lookup"><span data-stu-id="047c0-219">Select a user or group tooopen hello **Licenses** blade, which shows all licenses assigned toothat object.</span></span>

### <a name="remove-a-license"></a><span data-ttu-id="047c0-220">移除授權</span><span class="sxs-lookup"><span data-stu-id="047c0-220">Remove a license</span></span>

<span data-ttu-id="047c0-221">tooremove 授權，請移 toohello 使用者或群組，並開啟 hello**授權**磚。</span><span class="sxs-lookup"><span data-stu-id="047c0-221">tooremove a license, go toohello user or group, and open hello **Licenses** tile.</span></span> <span data-ttu-id="047c0-222">選取 hello 授權，然後按一下 **移除**。</span><span class="sxs-lookup"><span data-stu-id="047c0-222">Select hello license, and click **Remove**.</span></span>

![移除授權](media/active-directory-licensing-get-started-azure-portal/remove-license.png)

<span data-ttu-id="047c0-224">無法直接移除繼承自群組的 hello 使用者的授權。</span><span class="sxs-lookup"><span data-stu-id="047c0-224">Licenses inherited by hello user from a group cannot be removed directly.</span></span> <span data-ttu-id="047c0-225">相反地，移除 hello 使用者從他們從中繼承 hello 授權 hello 群組。</span><span class="sxs-lookup"><span data-stu-id="047c0-225">Instead, remove hello user from hello group from which they are inheriting hello license.</span></span>

### <a name="extend-trials"></a><span data-ttu-id="047c0-226">延長試用期</span><span class="sxs-lookup"><span data-stu-id="047c0-226">Extend trials</span></span>

<span data-ttu-id="047c0-227">客戶試用延伸模組都會提供為自助式註冊透過 hello Office 365 入口網站。</span><span class="sxs-lookup"><span data-stu-id="047c0-227">Trial extensions for customers are available as self-service sign-up through hello Office 365 portal.</span></span> <span data-ttu-id="047c0-228">客戶的系統管理員可以移 toohello Office 入口網站 （取決於 hello Office 入口網站的權限的存取），選取 hello Azure AD Premium 試用版。</span><span class="sxs-lookup"><span data-stu-id="047c0-228">A customer admin can go toohello Office portal (access depends on permissions for hello Office portal) and select hello Azure AD Premium trial.</span></span> <span data-ttu-id="047c0-229">按一下 hello**試用期延長**連結啟動 hello 延伸模組程序。</span><span class="sxs-lookup"><span data-stu-id="047c0-229">Clicking hello **Extend trial** link starts hello extension process.</span></span> <span data-ttu-id="047c0-230">您必須輸入信用卡，但不會被收費。</span><span class="sxs-lookup"><span data-stu-id="047c0-230">A credit card is required, but it is not charged.</span></span>

![在 hello Azure 入口網站中的試用期延長](media/active-directory-licensing-get-started-azure-portal/extend-trial-beginning.png)

## <a name="next-steps"></a><span data-ttu-id="047c0-232">後續步驟</span><span class="sxs-lookup"><span data-stu-id="047c0-232">Next steps</span></span>

<span data-ttu-id="047c0-233">深入了解 toolearn 進階案例的授權管理群組，透過讀取 hello 文章[指派授權 tooa 群組](active-directory-licensing-group-assignment-azure-portal.md)。</span><span class="sxs-lookup"><span data-stu-id="047c0-233">toolearn more about advanced scenarios for license management through groups, read hello article [Assigning licenses tooa group](active-directory-licensing-group-assignment-azure-portal.md).</span></span>

<span data-ttu-id="047c0-234">以下是有關 tooconfigure 並使用其他 Azure AD 的付費功能：</span><span class="sxs-lookup"><span data-stu-id="047c0-234">Here's information about how tooconfigure and use other Azure AD paid features:</span></span>

* [<span data-ttu-id="047c0-235">自助式密碼重設</span><span class="sxs-lookup"><span data-stu-id="047c0-235">Self-service password reset</span></span>](active-directory-manage-passwords.md)
* [<span data-ttu-id="047c0-236">自助式群組管理</span><span class="sxs-lookup"><span data-stu-id="047c0-236">Self-service group management</span></span>](active-directory-accessmanagement-self-service-group-management.md)
* [<span data-ttu-id="047c0-237">Azure AD Connect Health</span><span class="sxs-lookup"><span data-stu-id="047c0-237">Azure AD Connect health</span></span>](active-directory-aadconnect-health.md)
* [<span data-ttu-id="047c0-238">Azure Multi-Factor Authentication</span><span class="sxs-lookup"><span data-stu-id="047c0-238">Azure Multi-Factor Authentication</span></span>](../multi-factor-authentication/multi-factor-authentication.md)
* [<span data-ttu-id="047c0-239">直接購買 Azure AD Premium 授權</span><span class="sxs-lookup"><span data-stu-id="047c0-239">Direct purchase of Azure AD Premium licenses</span></span>](http://aka.ms/buyaadp)
