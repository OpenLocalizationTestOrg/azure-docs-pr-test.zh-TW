---
title: "Azure Active Directory 條件式存取的技術參考 | Microsoft Docs"
description: "透過條件式存取控制，Azure Active Directory 會在驗證使用者時以及允許存取應用程式之前，檢查您挑選的特定條件。 一旦符合這些條件，就會驗證使用者並允許存取應用程式。"
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
ms.openlocfilehash: ca16a5399f94fd1ab267e0798cade3fd83f75b13
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="azure-active-directory-conditional-access-technical-reference"></a><span data-ttu-id="092ff-104">Azure Active Directory 條件式存取的技術參考</span><span class="sxs-lookup"><span data-stu-id="092ff-104">Azure Active Directory Conditional Access technical reference</span></span>

## <a name="services-enabled-with-conditional-access"></a><span data-ttu-id="092ff-105">已啟用條件式存取功能的服務</span><span class="sxs-lookup"><span data-stu-id="092ff-105">Services enabled with conditional access</span></span>

<span data-ttu-id="092ff-106">各種 Azure AD 應用程式類型都支援「條件式存取」規則。</span><span class="sxs-lookup"><span data-stu-id="092ff-106">Conditional Access rules are supported across various Azure AD application types.</span></span> <span data-ttu-id="092ff-107">此清單包括：</span><span class="sxs-lookup"><span data-stu-id="092ff-107">This list includes:</span></span>


* <span data-ttu-id="092ff-108">已向 Azure 應用程式 Proxy 註冊的應用程式</span><span class="sxs-lookup"><span data-stu-id="092ff-108">Applications registered with the Azure Application Proxy</span></span>
* <span data-ttu-id="092ff-109">Azure 遠端應用程式</span><span class="sxs-lookup"><span data-stu-id="092ff-109">Azure Remote App</span></span>
* <span data-ttu-id="092ff-110">已開發並已向 Azure AD 註冊的企業營運及多租用戶應用程式</span><span class="sxs-lookup"><span data-stu-id="092ff-110">Developed line of business and multi-tenant applications registered with Azure AD</span></span>
* <span data-ttu-id="092ff-111">Dynamics CRM</span><span class="sxs-lookup"><span data-stu-id="092ff-111">Dynamics CRM</span></span>
* <span data-ttu-id="092ff-112">來自 Azure AD 應用程式庫的同盟應用程式</span><span class="sxs-lookup"><span data-stu-id="092ff-112">Federated applications from the Azure AD application gallery</span></span>
* <span data-ttu-id="092ff-113">Microsoft Office 365 Yammer</span><span class="sxs-lookup"><span data-stu-id="092ff-113">Microsoft Office 365 Yammer</span></span>
* <span data-ttu-id="092ff-114">Microsoft Office 365 Exchange Online</span><span class="sxs-lookup"><span data-stu-id="092ff-114">Microsoft Office 365 Exchange Online</span></span>
* <span data-ttu-id="092ff-115">Microsoft Office 365 SharePoint Online (包括商務用 OneDrive)</span><span class="sxs-lookup"><span data-stu-id="092ff-115">Microsoft Office 365 SharePoint Online (includes OneDrive for Business)</span></span>
* <span data-ttu-id="092ff-116">Microsoft Power BI</span><span class="sxs-lookup"><span data-stu-id="092ff-116">Microsoft Power BI</span></span> 
* <span data-ttu-id="092ff-117">來自 Azure AD 應用程式庫的密碼 SSO 應用程式</span><span class="sxs-lookup"><span data-stu-id="092ff-117">Password SSO applications from the Azure AD application gallery</span></span>
* <span data-ttu-id="092ff-118">Visual Studio Team Services</span><span class="sxs-lookup"><span data-stu-id="092ff-118">Visual Studio Team Services</span></span>
* <span data-ttu-id="092ff-119">Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="092ff-119">Microsoft Teams</span></span>









## <a name="enable-access-rules"></a><span data-ttu-id="092ff-120">啟用存取規則</span><span class="sxs-lookup"><span data-stu-id="092ff-120">Enable access rules</span></span>
<span data-ttu-id="092ff-121">您可以依據個別應用程式來啟用或停用每個規則。</span><span class="sxs-lookup"><span data-stu-id="092ff-121">Each rule can be enabled or disabled on a per application bases.</span></span> <span data-ttu-id="092ff-122">當規則為 **ON** 時，系統將會針對存取應用程式的使用者啟用並強制執行這些規則。</span><span class="sxs-lookup"><span data-stu-id="092ff-122">When rules are **ON** they will be enabled and enforced for users accessing the application.</span></span> <span data-ttu-id="092ff-123">當規則為 **OFF** 時，系統就不會使用這些規則，也就不會影響使用者的登入體驗。</span><span class="sxs-lookup"><span data-stu-id="092ff-123">When they are **OFF** they will not be used and will not impact the users sign in experience.</span></span>

## <a name="applying-rules-to-specific-users"></a><span data-ttu-id="092ff-124">將規則套用到特定的使用者</span><span class="sxs-lookup"><span data-stu-id="092ff-124">Applying rules to specific users</span></span>
<span data-ttu-id="092ff-125">您可以透過設定 [套用對象] ，根據安全性群組，將規則套用到特定的幾組使用者。</span><span class="sxs-lookup"><span data-stu-id="092ff-125">Rules can be applied to specific sets of users based on security group by setting **Apply To**.</span></span> <span data-ttu-id="092ff-126">[套用對象] 可以設定為 [所有使用者] 或 [群組]。</span><span class="sxs-lookup"><span data-stu-id="092ff-126">**Apply To** can be set to **All Users** or **Groups**.</span></span> <span data-ttu-id="092ff-127">設定為 [所有使用者]  時，會將規則套用到任何可以存取應用程式的使用者。</span><span class="sxs-lookup"><span data-stu-id="092ff-127">When set to **All Users** the rules will apply to any user with access to the application.</span></span> <span data-ttu-id="092ff-128">[群組]  選項可允許選取特定的安全性和通訊群組，系統將只會針對這些群組強制執行規則。</span><span class="sxs-lookup"><span data-stu-id="092ff-128">The **Groups** option allows specific security and distribution groups to be selected, rules will only be enforced for these groups.</span></span>

<span data-ttu-id="092ff-129">部署規則時，通常會先將它套用到一組有限的使用者，即試驗群組的成員。</span><span class="sxs-lookup"><span data-stu-id="092ff-129">When deploying a rule,  it is common to first apply it a limited set of users, that are members of a piloting groups.</span></span> <span data-ttu-id="092ff-130">完成後，規則就可以套用至 [所有使用者] 。</span><span class="sxs-lookup"><span data-stu-id="092ff-130">Once complete the rule can be applied to **All Users**.</span></span> <span data-ttu-id="092ff-131">這會造成規則對組織中的所有使用者強制執行。</span><span class="sxs-lookup"><span data-stu-id="092ff-131">This will cause the rule to be enforced for all users in the organization.</span></span>

<span data-ttu-id="092ff-132">您也可以使用 [例外]  選項來免除對選取的群組套用原則。</span><span class="sxs-lookup"><span data-stu-id="092ff-132">Select groups may also be exempted from policy using the **Except** option.</span></span> <span data-ttu-id="092ff-133">這些群組的任何成員即使出現在包含群組中，也不必套用原則。</span><span class="sxs-lookup"><span data-stu-id="092ff-133">Any members of these groups will be exempted even if they appear in an included group.</span></span>

## <a name="at-work-networks"></a><span data-ttu-id="092ff-134">「工作時」網路</span><span class="sxs-lookup"><span data-stu-id="092ff-134">“At work” networks</span></span>
<span data-ttu-id="092ff-135">使用「工作時」網路的條件式存取規則會依賴 Azure AD 中已設定的可信任 IP 位址範圍，或者從 AD FS 中使用「公司網路內部」宣告。</span><span class="sxs-lookup"><span data-stu-id="092ff-135">Conditional access rules that use an “At work” network, rely on trusted IP address ranges that have been configured in Azure AD, or use of the "inside corpnet" claim from AD FS.</span></span> <span data-ttu-id="092ff-136">這些規則包含：</span><span class="sxs-lookup"><span data-stu-id="092ff-136">These rules include:</span></span>

* <span data-ttu-id="092ff-137">不在工作時需要多重要素驗證</span><span class="sxs-lookup"><span data-stu-id="092ff-137">Require multi-factor authentication when not at work</span></span>
* <span data-ttu-id="092ff-138">不工作時封鎖存取</span><span class="sxs-lookup"><span data-stu-id="092ff-138">Block access when not at work</span></span>

<span data-ttu-id="092ff-139">用於指定「工作時」網路的選項</span><span class="sxs-lookup"><span data-stu-id="092ff-139">Options for specifiying “at work” networks</span></span>

1. <span data-ttu-id="092ff-140">在 [Multi-Factor Authentication 組態頁面](../multi-factor-authentication/multi-factor-authentication-whats-next.md)中設定可信任的 IP位址範圍。</span><span class="sxs-lookup"><span data-stu-id="092ff-140">Configure trusted IP address ranges in the [multi-factor authentication configuration page](../multi-factor-authentication/multi-factor-authentication-whats-next.md).</span></span> <span data-ttu-id="092ff-141">「條件式存取」原則會在每個驗證要求和權杖發行上使用已設定的範圍來評估規則。</span><span class="sxs-lookup"><span data-stu-id="092ff-141">Conditional Access policy will use the configured ranges on each authentication request and token issuance to evaluate rules.</span></span> 
2. <span data-ttu-id="092ff-142">設定使用公司網路內部的宣告，您可以使用 AD FS，將此選項與同盟目錄搭配使用。</span><span class="sxs-lookup"><span data-stu-id="092ff-142">Configure use of the inside corpnet claim, this option can be used with federated directories, using AD FS.</span></span> <span data-ttu-id="092ff-143">若要深入了解公司網路內部宣告，請參閱[信任的 IP](../multi-factor-authentication/multi-factor-authentication-whats-next.md#trusted-ips)。</span><span class="sxs-lookup"><span data-stu-id="092ff-143">To learn more about the inside corpnet claims, see [Tusted IPs](../multi-factor-authentication/multi-factor-authentication-whats-next.md#trusted-ips).</span></span>


## <a name="rules-based-on-application-sensitivity"></a><span data-ttu-id="092ff-144">根據應用程式敏感性的規則</span><span class="sxs-lookup"><span data-stu-id="092ff-144">Rules based on application sensitivity</span></span>
<span data-ttu-id="092ff-145">規則是依據個別應用程式來設定，以允許對高價值服務進行保護，而不影響對其他服務的存取。</span><span class="sxs-lookup"><span data-stu-id="092ff-145">Rules are configured per application allowing the high value services to be secured without impacting access to other services.</span></span> <span data-ttu-id="092ff-146">條件式存取規則可以在應用程式的 [設定]  索引標籤上設定。</span><span class="sxs-lookup"><span data-stu-id="092ff-146">Conditional access rules can be configured on the  **Configure** tab of the application.</span></span> 

<span data-ttu-id="092ff-147">目前提供的規則︰</span><span class="sxs-lookup"><span data-stu-id="092ff-147">Rules currently offered:</span></span>

* <span data-ttu-id="092ff-148">**需要多重要素驗證**</span><span class="sxs-lookup"><span data-stu-id="092ff-148">**Require multi-factor authentication**</span></span>
  
  * <span data-ttu-id="092ff-149">所有套用了這個原則的使用者都必須透過 Multi-Factor Authentication 至少驗證一次。</span><span class="sxs-lookup"><span data-stu-id="092ff-149">All users that this policy is applied to will be required to authenticate via multi-factor authentication at least once.</span></span>
* <span data-ttu-id="092ff-150">**不在工作時需要多重要素驗證**</span><span class="sxs-lookup"><span data-stu-id="092ff-150">**Require multi-factor authentication when not at work**</span></span>
  
  * <span data-ttu-id="092ff-151">如果套用了這個原則，所有使用者如果是從非工作遠端位置存取服務，都必須至少執行一次 Multi-Factor Authentication。</span><span class="sxs-lookup"><span data-stu-id="092ff-151">If this policy is applied, all users will be required to have performed multi-factor authentication at least once if they access the service from a non-work remote location.</span></span> <span data-ttu-id="092ff-152">如果他們從工作位置移到遠端位置，則在存取服務時，就必須執行 Multi-Factor Authentication。</span><span class="sxs-lookup"><span data-stu-id="092ff-152">If they move from a work to remote location, they will be required to perform multifactor authentication when accessing the service.</span></span>
* <span data-ttu-id="092ff-153">**不工作時封鎖存取**</span><span class="sxs-lookup"><span data-stu-id="092ff-153">**Block access when not at work**</span></span> 
  
  * <span data-ttu-id="092ff-154">當使用者從工作位置移至遠端位置時，如果套用了 [不工作時封鎖存取] 原則，他們就會被封鎖。</span><span class="sxs-lookup"><span data-stu-id="092ff-154">When users move from work to a remote location, they will be blocked if the "Block access when not at work" policy is applied to them.</span></span>  <span data-ttu-id="092ff-155">當他們回到工作位置時，就會再次允許他們存取。</span><span class="sxs-lookup"><span data-stu-id="092ff-155">They will be re-allowed access when at a work location.</span></span>

## <a name="related-topics"></a><span data-ttu-id="092ff-156">相關主題</span><span class="sxs-lookup"><span data-stu-id="092ff-156">Related topics</span></span>
* [<span data-ttu-id="092ff-157">保護對 Office 365 及其他連接至 Azure Active Directory 之應用程式的存取</span><span class="sxs-lookup"><span data-stu-id="092ff-157">Securing access to Office 365 and other apps connected to Azure Active Directory</span></span>](active-directory-conditional-access.md)
* [<span data-ttu-id="092ff-158">Article Index for Application Management in Azure Active Directory (Azure Active Directory 中應用程式管理的文件索引)</span><span class="sxs-lookup"><span data-stu-id="092ff-158">Article Index for Application Management in Azure Active Directory</span></span>](active-directory-apps-index.md)

