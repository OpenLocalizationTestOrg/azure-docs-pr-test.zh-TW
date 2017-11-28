---
title: "Active Directory 條件式存取的技術參考 aaaAzure |Microsoft 文件"
description: "條件式存取控制與 Azure Active Directory 檢查 hello 您挑選驗證 hello 使用者時，才能允許存取 toohello 應用程式特定的條件。 一旦符合這些條件，hello 使用者已驗證，而且允許存取 toohello 應用程式。"
services: active-directory.
documentationcenter: 
author: MarkusVi
manager: femila
ms.assetid: 56a5bade-7dcc-4dcf-8092-a7d4bf5df3c1
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 08/22/2017
ms.author: markvi
ms.reviewer: calebb
ms.openlocfilehash: ee201405d1d17f130607a95bf455b60cd222dd0c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-conditional-access-technical-reference"></a><span data-ttu-id="a4265-104">Azure Active Directory 條件式存取的技術參考</span><span class="sxs-lookup"><span data-stu-id="a4265-104">Azure Active Directory Conditional Access technical reference</span></span>

## <a name="services-enabled-with-conditional-access"></a><span data-ttu-id="a4265-105">已啟用條件式存取功能的服務</span><span class="sxs-lookup"><span data-stu-id="a4265-105">Services enabled with conditional access</span></span>

<span data-ttu-id="a4265-106">各種 Azure AD 應用程式類型都支援「條件式存取」規則。</span><span class="sxs-lookup"><span data-stu-id="a4265-106">Conditional Access rules are supported across various Azure AD application types.</span></span> <span data-ttu-id="a4265-107">此清單包括：</span><span class="sxs-lookup"><span data-stu-id="a4265-107">This list includes:</span></span>


* <span data-ttu-id="a4265-108">應用程式註冊以 hello Azure 應用程式 Proxy</span><span class="sxs-lookup"><span data-stu-id="a4265-108">Applications registered with hello Azure Application Proxy</span></span>
* <span data-ttu-id="a4265-109">Azure 遠端應用程式</span><span class="sxs-lookup"><span data-stu-id="a4265-109">Azure Remote App</span></span>
* <span data-ttu-id="a4265-110">已開發並已向 Azure AD 註冊的企業營運及多租用戶應用程式</span><span class="sxs-lookup"><span data-stu-id="a4265-110">Developed line of business and multi-tenant applications registered with Azure AD</span></span>
* <span data-ttu-id="a4265-111">Dynamics CRM</span><span class="sxs-lookup"><span data-stu-id="a4265-111">Dynamics CRM</span></span>
* <span data-ttu-id="a4265-112">同盟的應用程式從 hello Azure AD 應用程式庫</span><span class="sxs-lookup"><span data-stu-id="a4265-112">Federated applications from hello Azure AD application gallery</span></span>
* <span data-ttu-id="a4265-113">Microsoft Office 365 Yammer</span><span class="sxs-lookup"><span data-stu-id="a4265-113">Microsoft Office 365 Yammer</span></span>
* <span data-ttu-id="a4265-114">Microsoft Office 365 Exchange Online</span><span class="sxs-lookup"><span data-stu-id="a4265-114">Microsoft Office 365 Exchange Online</span></span>
* <span data-ttu-id="a4265-115">Microsoft Office 365 SharePoint Online (包括商務用 OneDrive)</span><span class="sxs-lookup"><span data-stu-id="a4265-115">Microsoft Office 365 SharePoint Online (includes OneDrive for Business)</span></span>
* <span data-ttu-id="a4265-116">Microsoft Power BI</span><span class="sxs-lookup"><span data-stu-id="a4265-116">Microsoft Power BI</span></span> 
* <span data-ttu-id="a4265-117">密碼 SSO 應用程式從 hello Azure AD 應用程式庫</span><span class="sxs-lookup"><span data-stu-id="a4265-117">Password SSO applications from hello Azure AD application gallery</span></span>
* <span data-ttu-id="a4265-118">Visual Studio Team Services</span><span class="sxs-lookup"><span data-stu-id="a4265-118">Visual Studio Team Services</span></span>
* <span data-ttu-id="a4265-119">Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="a4265-119">Microsoft Teams</span></span>









## <a name="enable-access-rules"></a><span data-ttu-id="a4265-120">啟用存取規則</span><span class="sxs-lookup"><span data-stu-id="a4265-120">Enable access rules</span></span>
<span data-ttu-id="a4265-121">您可以依據個別應用程式來啟用或停用每個規則。</span><span class="sxs-lookup"><span data-stu-id="a4265-121">Each rule can be enabled or disabled on a per application bases.</span></span> <span data-ttu-id="a4265-122">當規則是**ON**會啟用並強制執行存取 hello 應用程式的使用者。</span><span class="sxs-lookup"><span data-stu-id="a4265-122">When rules are **ON** they will be enabled and enforced for users accessing hello application.</span></span> <span data-ttu-id="a4265-123">何時**OFF**它們不會使用並會影響 hello 使用者登入體驗。</span><span class="sxs-lookup"><span data-stu-id="a4265-123">When they are **OFF** they will not be used and will not impact hello users sign in experience.</span></span>

## <a name="applying-rules-toospecific-users"></a><span data-ttu-id="a4265-124">套用規則 toospecific 使用者</span><span class="sxs-lookup"><span data-stu-id="a4265-124">Applying rules toospecific users</span></span>
<span data-ttu-id="a4265-125">規則可能會藉由設定為基礎的安全性群組的使用者集合套用的 toospecific**套用到**。</span><span class="sxs-lookup"><span data-stu-id="a4265-125">Rules can be applied toospecific sets of users based on security group by setting **Apply To**.</span></span> <span data-ttu-id="a4265-126">**套用到**可以設定得**所有使用者**或**群組**。</span><span class="sxs-lookup"><span data-stu-id="a4265-126">**Apply To** can be set too**All Users** or **Groups**.</span></span> <span data-ttu-id="a4265-127">當設定太**所有使用者**hello 規則會套用與應用程式存取 toohello tooany 使用者。</span><span class="sxs-lookup"><span data-stu-id="a4265-127">When set too**All Users** hello rules will apply tooany user with access toohello application.</span></span> <span data-ttu-id="a4265-128">hello**群組**選項可讓特定的安全性以及發佈群組 toobe 選取，將只針對這些群組強制執行規則。</span><span class="sxs-lookup"><span data-stu-id="a4265-128">hello **Groups** option allows specific security and distribution groups toobe selected, rules will only be enforced for these groups.</span></span>

<span data-ttu-id="a4265-129">在部署規則時，常會 toofirst 套用一組有限的使用者，試驗群組的成員。</span><span class="sxs-lookup"><span data-stu-id="a4265-129">When deploying a rule,  it is common toofirst apply it a limited set of users, that are members of a piloting groups.</span></span> <span data-ttu-id="a4265-130">一旦完成 hello 規則套用太**所有使用者**。</span><span class="sxs-lookup"><span data-stu-id="a4265-130">Once complete hello rule can be applied too**All Users**.</span></span> <span data-ttu-id="a4265-131">這會導致 hello 規則 toobe 強制執行 hello 組織中的所有使用者。</span><span class="sxs-lookup"><span data-stu-id="a4265-131">This will cause hello rule toobe enforced for all users in hello organization.</span></span>

<span data-ttu-id="a4265-132">選取群組也可能會豁免原則使用 hello**除了**選項。</span><span class="sxs-lookup"><span data-stu-id="a4265-132">Select groups may also be exempted from policy using hello **Except** option.</span></span> <span data-ttu-id="a4265-133">這些群組的任何成員即使出現在包含群組中，也不必套用原則。</span><span class="sxs-lookup"><span data-stu-id="a4265-133">Any members of these groups will be exempted even if they appear in an included group.</span></span>

## <a name="at-work-networks"></a><span data-ttu-id="a4265-134">「工作時」網路</span><span class="sxs-lookup"><span data-stu-id="a4265-134">“At work” networks</span></span>
<span data-ttu-id="a4265-135">使用"At 工作 」 網路的條件式存取規則仰賴受信任的 IP 位址範圍已在 Azure AD 中設定或使用 「 內部公司網路 」 hello 來自 AD FS 宣告。</span><span class="sxs-lookup"><span data-stu-id="a4265-135">Conditional access rules that use an “At work” network, rely on trusted IP address ranges that have been configured in Azure AD, or use of hello "inside corpnet" claim from AD FS.</span></span> <span data-ttu-id="a4265-136">這些規則包含：</span><span class="sxs-lookup"><span data-stu-id="a4265-136">These rules include:</span></span>

* <span data-ttu-id="a4265-137">不在工作時需要多重要素驗證</span><span class="sxs-lookup"><span data-stu-id="a4265-137">Require multi-factor authentication when not at work</span></span>
* <span data-ttu-id="a4265-138">不工作時封鎖存取</span><span class="sxs-lookup"><span data-stu-id="a4265-138">Block access when not at work</span></span>

<span data-ttu-id="a4265-139">用於指定「工作時」網路的選項</span><span class="sxs-lookup"><span data-stu-id="a4265-139">Options for specifiying “at work” networks</span></span>

1. <span data-ttu-id="a4265-140">在 hello 中設定受信任的 IP 位址範圍[多因素驗證設定頁面](../multi-factor-authentication/multi-factor-authentication-whats-next.md)。</span><span class="sxs-lookup"><span data-stu-id="a4265-140">Configure trusted IP address ranges in hello [multi-factor authentication configuration page](../multi-factor-authentication/multi-factor-authentication-whats-next.md).</span></span> <span data-ttu-id="a4265-141">條件式存取原則會在每個驗證發行 tooevaluate 要求和語彙基元規則上使用 hello 設定範圍。</span><span class="sxs-lookup"><span data-stu-id="a4265-141">Conditional Access policy will use hello configured ranges on each authentication request and token issuance tooevaluate rules.</span></span> 
2. <span data-ttu-id="a4265-142">設定 hello corpnet 宣告內的使用方式，這個選項可以搭配使用 AD FS 同盟目錄。</span><span class="sxs-lookup"><span data-stu-id="a4265-142">Configure use of hello inside corpnet claim, this option can be used with federated directories, using AD FS.</span></span> <span data-ttu-id="a4265-143">toolearn 深入了解 hello 內部公司網路的宣告，請參閱[Tusted Ip](../multi-factor-authentication/multi-factor-authentication-whats-next.md#trusted-ips)。</span><span class="sxs-lookup"><span data-stu-id="a4265-143">toolearn more about hello inside corpnet claims, see [Tusted IPs](../multi-factor-authentication/multi-factor-authentication-whats-next.md#trusted-ips).</span></span>


## <a name="rules-based-on-application-sensitivity"></a><span data-ttu-id="a4265-144">根據應用程式敏感性的規則</span><span class="sxs-lookup"><span data-stu-id="a4265-144">Rules based on application sensitivity</span></span>
<span data-ttu-id="a4265-145">規則是每個允許 hello 高價值的服務 toobe 而不會影響存取 tooother 服務保護的應用程式設定。</span><span class="sxs-lookup"><span data-stu-id="a4265-145">Rules are configured per application allowing hello high value services toobe secured without impacting access tooother services.</span></span> <span data-ttu-id="a4265-146">可以設定條件式存取規則，在 hello**設定**hello 應用程式 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="a4265-146">Conditional access rules can be configured on hello  **Configure** tab of hello application.</span></span> 

<span data-ttu-id="a4265-147">目前提供的規則︰</span><span class="sxs-lookup"><span data-stu-id="a4265-147">Rules currently offered:</span></span>

* <span data-ttu-id="a4265-148">**需要多重要素驗證**</span><span class="sxs-lookup"><span data-stu-id="a4265-148">**Require multi-factor authentication**</span></span>
  
  * <span data-ttu-id="a4265-149">此原則會套用的 toowill 的所有使用者都是必要的 tooauthenticate 透過多重要素驗證至少一次。</span><span class="sxs-lookup"><span data-stu-id="a4265-149">All users that this policy is applied toowill be required tooauthenticate via multi-factor authentication at least once.</span></span>
* <span data-ttu-id="a4265-150">**不在工作時需要多重要素驗證**</span><span class="sxs-lookup"><span data-stu-id="a4265-150">**Require multi-factor authentication when not at work**</span></span>
  
  * <span data-ttu-id="a4265-151">如果套用此原則，所有使用者都都需要的 toohave 執行多重要素驗證至少一次只要從非工作遠端位置存取 hello 服務。</span><span class="sxs-lookup"><span data-stu-id="a4265-151">If this policy is applied, all users will be required toohave performed multi-factor authentication at least once if they access hello service from a non-work remote location.</span></span> <span data-ttu-id="a4265-152">如果它們從工作 tooremote 位置，就會需要的 tooperform 多重要素驗證時存取 hello 服務。</span><span class="sxs-lookup"><span data-stu-id="a4265-152">If they move from a work tooremote location, they will be required tooperform multifactor authentication when accessing hello service.</span></span>
* <span data-ttu-id="a4265-153">**不工作時封鎖存取**</span><span class="sxs-lookup"><span data-stu-id="a4265-153">**Block access when not at work**</span></span> 
  
  * <span data-ttu-id="a4265-154">當使用者移動工作 tooa 遠端位置時，請他們即將遭到封鎖時 hello 「 封鎖存取不在工作時 」 原則套用的 toothem。</span><span class="sxs-lookup"><span data-stu-id="a4265-154">When users move from work tooa remote location, they will be blocked if hello "Block access when not at work" policy is applied toothem.</span></span>  <span data-ttu-id="a4265-155">當他們回到工作位置時，就會再次允許他們存取。</span><span class="sxs-lookup"><span data-stu-id="a4265-155">They will be re-allowed access when at a work location.</span></span>

## <a name="related-topics"></a><span data-ttu-id="a4265-156">相關主題</span><span class="sxs-lookup"><span data-stu-id="a4265-156">Related topics</span></span>
* [<span data-ttu-id="a4265-157">保護存取 tooOffice 365 和其他應用程式連接 tooAzure Active Directory</span><span class="sxs-lookup"><span data-stu-id="a4265-157">Securing access tooOffice 365 and other apps connected tooAzure Active Directory</span></span>](active-directory-conditional-access.md)
* [<span data-ttu-id="a4265-158">Article Index for Application Management in Azure Active Directory (Azure Active Directory 中應用程式管理的文件索引)</span><span class="sxs-lookup"><span data-stu-id="a4265-158">Article Index for Application Management in Azure Active Directory</span></span>](active-directory-apps-index.md)

