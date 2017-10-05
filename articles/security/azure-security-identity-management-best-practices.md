---
title: "Azure 身分識別和存取安全性的最佳做法 | Microsoft Docs"
description: "本文提供使用內建 Azure 功能的一些身分識別管理和存取控制最佳作法。"
services: security
documentationcenter: na
author: YuriDio
manager: swadhwa
editor: TomSh
ms.assetid: 07d8e8a8-47e8-447c-9c06-3a88d2713bc1
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 01/30/2017
ms.author: yurid
ms.openlocfilehash: 50f9073d3c35bd9dcfd826ff44e767fb69558757
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="azure-identity-management-and-access-control-security-best-practices"></a><span data-ttu-id="d97a1-103">Azure 身分識別管理和存取控制安全性最佳作法</span><span class="sxs-lookup"><span data-stu-id="d97a1-103">Azure Identity Management and access control security best practices</span></span>
<span data-ttu-id="d97a1-104">許多人認為身分識別是安全性的新界限層，並從傳統以網路為中心的觀點來接收該角色。</span><span class="sxs-lookup"><span data-stu-id="d97a1-104">Many consider identity to be the new boundary layer for security, taking over that role from the traditional network-centric perspective.</span></span> <span data-ttu-id="d97a1-105">此安全性注意和投資進展的主要關鍵是由於網路周邊的漏洞日益增加，而且周邊防禦的效果不如 [BYOD](http://aka.ms/byodcg) 裝置和雲端應用程式暴增前的效果。</span><span class="sxs-lookup"><span data-stu-id="d97a1-105">This evolution of the primary pivot for security attention and investments come from the fact that network perimeters have become increasingly porous and that perimeter defense cannot be as effective as they once were prior to the explosion of [BYOD](http://aka.ms/byodcg) devices and cloud applications.</span></span>

<span data-ttu-id="d97a1-106">本文將討論 Azure 身分識別管理和存取控制安全性最佳作法的集合。</span><span class="sxs-lookup"><span data-stu-id="d97a1-106">In this article we will discuss a collection of Azure identity management and access control security best practices.</span></span> <span data-ttu-id="d97a1-107">這些最佳作法衍生自我們的 [Azure AD](../active-directory/active-directory-whatis.md) 經驗和客戶的經驗。</span><span class="sxs-lookup"><span data-stu-id="d97a1-107">These best practices are derived from our experience with [Azure AD](../active-directory/active-directory-whatis.md) and the experiences of customers like yourself.</span></span>

<span data-ttu-id="d97a1-108">針對每個最佳作法，我們會說明︰</span><span class="sxs-lookup"><span data-stu-id="d97a1-108">For each best practice, we’ll explain:</span></span>

* <span data-ttu-id="d97a1-109">最佳作法是什麼</span><span class="sxs-lookup"><span data-stu-id="d97a1-109">What the best practice is</span></span>
* <span data-ttu-id="d97a1-110">您為何想要啟用該最佳作法</span><span class="sxs-lookup"><span data-stu-id="d97a1-110">Why you want to enable that best practice</span></span>
* <span data-ttu-id="d97a1-111">如果無法啟用最佳作法，結果可能為何</span><span class="sxs-lookup"><span data-stu-id="d97a1-111">What might be the result if you fail to enable the best practice</span></span>
* <span data-ttu-id="d97a1-112">最佳作法的可能替代方案</span><span class="sxs-lookup"><span data-stu-id="d97a1-112">Possible alternatives to the best practice</span></span>
* <span data-ttu-id="d97a1-113">如何學習啟用最佳作法</span><span class="sxs-lookup"><span data-stu-id="d97a1-113">How you can learn to enable the best practice</span></span>

<span data-ttu-id="d97a1-114">這篇「Azure 身分識別管理和存取控制安全性最佳作法」是以共識意見及 Azure 平台功能和特性集 (因為在撰寫本文時已存在) 為基礎。</span><span class="sxs-lookup"><span data-stu-id="d97a1-114">This Azure identity management and access control security best practices article is based on a consensus opinion and Azure platform capabilities and feature sets, as they exist at the time this article was written.</span></span> <span data-ttu-id="d97a1-115">意見和技術會隨著時間改變，這篇文章將會定期進行更新以反映這些變更。</span><span class="sxs-lookup"><span data-stu-id="d97a1-115">Opinions and technologies change over time and this article will be updated on a regular basis to reflect those changes.</span></span>

<span data-ttu-id="d97a1-116">本文討論的 Azure 身分識別管理和存取控制安全性最佳作法包括：</span><span class="sxs-lookup"><span data-stu-id="d97a1-116">Azure identity management and access control security best practices discussed in this article include:</span></span>

* <span data-ttu-id="d97a1-117">集中管理您的身分識別</span><span class="sxs-lookup"><span data-stu-id="d97a1-117">Centralize your identity management</span></span>
* <span data-ttu-id="d97a1-118">啟用單一登入 (SSO)</span><span class="sxs-lookup"><span data-stu-id="d97a1-118">Enable Single Sign-On (SSO)</span></span>
* <span data-ttu-id="d97a1-119">部署密碼管理</span><span class="sxs-lookup"><span data-stu-id="d97a1-119">Deploy password management</span></span>
* <span data-ttu-id="d97a1-120">對使用者強制執行 Multi-Factor Authentication (MFA)</span><span class="sxs-lookup"><span data-stu-id="d97a1-120">Enforce multi-factor authentication (MFA) for users</span></span>
* <span data-ttu-id="d97a1-121">使用角色型存取控制 (RBAC)</span><span class="sxs-lookup"><span data-stu-id="d97a1-121">Use role based access control (RBAC)</span></span>
* <span data-ttu-id="d97a1-122">使用資源管理員來控制資源的建立位置</span><span class="sxs-lookup"><span data-stu-id="d97a1-122">Control locations where resources are created using resource manager</span></span>
* <span data-ttu-id="d97a1-123">引導開發人員運用 SaaS 應用程式的身分識別功能</span><span class="sxs-lookup"><span data-stu-id="d97a1-123">Guide developers to leverage identity capabilities for SaaS apps</span></span>
* <span data-ttu-id="d97a1-124">主動監視可疑的活動</span><span class="sxs-lookup"><span data-stu-id="d97a1-124">Actively monitor for suspicious activities</span></span>

## <a name="centralize-your-identity-management"></a><span data-ttu-id="d97a1-125">集中管理您的身分識別</span><span class="sxs-lookup"><span data-stu-id="d97a1-125">Centralize your identity management</span></span>
<span data-ttu-id="d97a1-126">保護您的身分識別的一個重要步驟，就是確保 IT 可以從一個有關此帳戶建立所在的單一位置管理帳戶。</span><span class="sxs-lookup"><span data-stu-id="d97a1-126">One important step towards securing your identity is to ensure that IT can manage accounts from one single location regarding where this account was created.</span></span> <span data-ttu-id="d97a1-127">雖然大部分的企業 IT 組織會在內部部署其主要的帳戶目錄，但混合式雲端部署逐漸增加，您務必了解如何整合內部部署和雲端目錄並且為使用者提供順暢的體驗。</span><span class="sxs-lookup"><span data-stu-id="d97a1-127">While the majority of the enterprises IT organizations will have their primary account directory on-premises, hybrid cloud deployments are on the rise and it is important that you understand how to integrate on-premises and cloud directories and provide a seamless experience to the end user.</span></span>

<span data-ttu-id="d97a1-128">若要完成此[混合式身分識別](../active-directory/active-directory-hybrid-identity-design-considerations-overview.md)案例，我們建議兩個選項：</span><span class="sxs-lookup"><span data-stu-id="d97a1-128">To accomplish this [hybrid identity](../active-directory/active-directory-hybrid-identity-design-considerations-overview.md) scenario we recommend two options:</span></span>

* <span data-ttu-id="d97a1-129">使用 Azure AD Connect 同步處理內部部署目錄與雲端目錄。</span><span class="sxs-lookup"><span data-stu-id="d97a1-129">Synchronize your on-premises directory with your cloud directory using Azure AD Connect</span></span>
* <span data-ttu-id="d97a1-130">使用 [Active Directory Federation Services](https://msdn.microsoft.com/library/bb897402.aspx) (AD FS) 建立內部部署身分識別與雲端目錄的同盟</span><span class="sxs-lookup"><span data-stu-id="d97a1-130">Federate your on-premises identity with your cloud directory using [Active Directory Federation Services](https://msdn.microsoft.com/library/bb897402.aspx) (AD FS)</span></span>

<span data-ttu-id="d97a1-131">無法整合其內部部署身分識別與雲端身分識別的組織會面臨用於管理帳戶的額外管理負荷增加，這會使錯誤和安全性缺口的可能性提高。</span><span class="sxs-lookup"><span data-stu-id="d97a1-131">Organizations that fail to integrate their on-premises identity with their cloud identity will experience increased administrative overhead in managing accounts, which increases the likelihood of mistakes and security breaches.</span></span>

<span data-ttu-id="d97a1-132">如需 Azure AD 同步處理的詳細資訊，請參閱[整合內部部署身分識別與 Azure Active Directory](../active-directory/active-directory-aadconnect.md)一文。</span><span class="sxs-lookup"><span data-stu-id="d97a1-132">For more information on Azure AD synchronization, please read the article [Integrating your on-premises identities with Azure Active Directory](../active-directory/active-directory-aadconnect.md).</span></span>

## <a name="enable-single-sign-on-sso"></a><span data-ttu-id="d97a1-133">啟用單一登入 (SSO)</span><span class="sxs-lookup"><span data-stu-id="d97a1-133">Enable Single Sign-On (SSO)</span></span>
<span data-ttu-id="d97a1-134">當您有多個目錄要管理時，這不只會成為 IT 的系統管理問題，對於必須記住多組密碼的使用者而言也是個問題。</span><span class="sxs-lookup"><span data-stu-id="d97a1-134">When you have multiple directories to manage, this becomes an administrative problem not only for IT, but also for end users that will have to remember multiple passwords.</span></span> <span data-ttu-id="d97a1-135">使用 [SSO](https://azure.microsoft.com/documentation/videos/overview-of-single-sign-on/)，提供使用者使用同一組認證來登入和存取所需資源的能力，不論此資源是位於內部部署或雲端。</span><span class="sxs-lookup"><span data-stu-id="d97a1-135">By using [SSO](https://azure.microsoft.com/documentation/videos/overview-of-single-sign-on/) you will provide your users the ability of use the same set of credentials to sign-in and access the resources that they need, regardless where this resource is located on-premises or in the cloud.</span></span>

<span data-ttu-id="d97a1-136">使用 SSO 讓使用者根據其在 Azure AD 中的組織帳戶存取其 [SaaS 應用程式](../active-directory/active-directory-appssoaccess-whatis.md)。</span><span class="sxs-lookup"><span data-stu-id="d97a1-136">Use SSO to enable users to access their [SaaS applications](../active-directory/active-directory-appssoaccess-whatis.md) based on their organizational account in Azure AD.</span></span> <span data-ttu-id="d97a1-137">這不只適用於 Microsoft SaaS 應用程式，也適用於其他應用程式，例如 [Google Apps](../active-directory/active-directory-saas-google-apps-tutorial.md) 和 [Salesforce](../active-directory/active-directory-saas-salesforce-tutorial.md)。</span><span class="sxs-lookup"><span data-stu-id="d97a1-137">This is applicable not only for Microsoft SaaS apps, but also other apps, such as [Google Apps](../active-directory/active-directory-saas-google-apps-tutorial.md) and [Salesforce](../active-directory/active-directory-saas-salesforce-tutorial.md).</span></span> <span data-ttu-id="d97a1-138">您的應用程式可以設定為使用 Azure AD 作為 [SAML 型身分識別提供者](../active-directory/fundamentals-identity.md)。</span><span class="sxs-lookup"><span data-stu-id="d97a1-138">Your application can be configured to use Azure AD as a [SAML-based identity](../active-directory/fundamentals-identity.md) provider.</span></span> <span data-ttu-id="d97a1-139">為了控制安全性，Azure AD 不會核發允許他們登入應用程式的權杖，除非他們已使用 Azure AD 獲得存取存取權。</span><span class="sxs-lookup"><span data-stu-id="d97a1-139">As a security control, Azure AD will not issue a token allowing them to sign into the application unless they have been granted access using Azure AD.</span></span> <span data-ttu-id="d97a1-140">您可以直接授與存取權，或透過其所屬的群組授與。</span><span class="sxs-lookup"><span data-stu-id="d97a1-140">You may grant access directly, or through a group that they are a member of.</span></span>

> [!NOTE]
> <span data-ttu-id="d97a1-141">使用 SSO 的決策會影響您整合內部部署目錄與雲端目錄的方式。</span><span class="sxs-lookup"><span data-stu-id="d97a1-141">the decision to use SSO will impact how you integrate your on-premises directory with your cloud directory.</span></span> <span data-ttu-id="d97a1-142">如果您想要 SSO，則必須使用同盟，因為目錄同步處理只會提供[相同的登入體驗](../active-directory/active-directory-aadconnect.md)。</span><span class="sxs-lookup"><span data-stu-id="d97a1-142">If you want SSO, you will need to use federation, because directory synchronization will only provide [same sign-on experience](../active-directory/active-directory-aadconnect.md).</span></span>
>
>

<span data-ttu-id="d97a1-143">未對使用者和應用程式強制執行 SSO 的組織更容易遭遇使用者有多組密碼的情況，以致直接增加使用者重複使用密碼或使用弱式密碼的可能性。</span><span class="sxs-lookup"><span data-stu-id="d97a1-143">Organizations that do not enforce SSO for their users and applications are more exposed to scenarios where users will have multiple passwords which directly increases the likelihood of users reusing passwords or using weak passwords.</span></span>

<span data-ttu-id="d97a1-144">若要深入了解 Azure AD SSO，請閱讀[使用 Azure AD Connect 管理和自訂 AD FS](../active-directory/active-directory-aadconnect-federation-management.md) 一文。</span><span class="sxs-lookup"><span data-stu-id="d97a1-144">You can learn more about Azure AD SSO by reading the article [AD FS management and customization with Azure AD Connect](../active-directory/active-directory-aadconnect-federation-management.md).</span></span>

## <a name="deploy-password-management"></a><span data-ttu-id="d97a1-145">部署密碼管理</span><span class="sxs-lookup"><span data-stu-id="d97a1-145">Deploy password management</span></span>
<span data-ttu-id="d97a1-146">在您有多個租用戶或想要讓使用者[重設其密碼](../active-directory/active-directory-passwords-update-your-own-password.md)的案例中，請務必使用適當的安全性原則來防止不當使用。</span><span class="sxs-lookup"><span data-stu-id="d97a1-146">In scenarios where you have multiple tenants or you want to enable users to [reset their own password](../active-directory/active-directory-passwords-update-your-own-password.md), it is important that you use appropriate security policies to prevent abuse.</span></span> <span data-ttu-id="d97a1-147">在 Azure 中，您可以利用自助密碼重設功能並自訂安全性選項，以符合您的商務需求。</span><span class="sxs-lookup"><span data-stu-id="d97a1-147">In Azure you can leverage the self-service password reset capability and customize the security options to meet your business requirements.</span></span>

<span data-ttu-id="d97a1-148">向這些使用者取得意見反應，並從他們嘗試執行這些步驟時的經驗學習特別重要。</span><span class="sxs-lookup"><span data-stu-id="d97a1-148">It is particularly important to obtain feedback from these users and learn from their experiences as they try to perform these steps.</span></span> <span data-ttu-id="d97a1-149">根據這些經驗進行詳細計劃，以緩和在大型群組部署期間可能發生的潛在問題。</span><span class="sxs-lookup"><span data-stu-id="d97a1-149">Based on these experiences, elaborate a plan to mitigate potential issues that may occur during the deployment for a larger group.</span></span> <span data-ttu-id="d97a1-150">此外，也建議您使用[密碼重設登錄活動報告](../active-directory/active-directory-passwords-get-insights.md)來監視進行註冊的使用者。</span><span class="sxs-lookup"><span data-stu-id="d97a1-150">It is also recommended that you use the [Password Reset Registration Activity report](../active-directory/active-directory-passwords-get-insights.md) to monitor the users that are registering.</span></span>

<span data-ttu-id="d97a1-151">想要避免密碼變更支援電話但可讓使用者重設其密碼的組織，其服務中心比較容易接到較多有關密碼問題的電話量。</span><span class="sxs-lookup"><span data-stu-id="d97a1-151">Organizations that want to avoid password change support calls but do enable users to reset their own passwords are more susceptible to a higher call volume to the service desk due to password issues.</span></span> <span data-ttu-id="d97a1-152">在有多個租用戶的組織中，務必實作此類型的功能，並可讓使用者在安全性原則中建立的安全範圍內執行密碼重設。</span><span class="sxs-lookup"><span data-stu-id="d97a1-152">In organizations that have multiple tenants, it is imperative that you implement this type of capability and enable users to perform password reset within security boundaries that were established in the security policy.</span></span>

<span data-ttu-id="d97a1-153">您可以閱讀[部署密碼管理和訓練使用者使用密碼](../active-directory/active-directory-passwords-best-practices.md)一文，進一步了解密碼重設。</span><span class="sxs-lookup"><span data-stu-id="d97a1-153">You can learn more about password reset by reading the article [Deploying Password Management and training users to use it](../active-directory/active-directory-passwords-best-practices.md).</span></span>

## <a name="enforce-multi-factor-authentication-mfa-for-users"></a><span data-ttu-id="d97a1-154">對使用者強制執行 Multi-Factor Authentication (MFA)</span><span class="sxs-lookup"><span data-stu-id="d97a1-154">Enforce multi-factor authentication (MFA) for users</span></span>
<span data-ttu-id="d97a1-155">對於需要符合業界標準 (例如 [PCI DSS 3.2 版](http://blog.pcisecuritystandards.org/preparing-for-pci-dss-32)) 的組織，Multi-Factor Authentication 是驗證使用者的必備功能。</span><span class="sxs-lookup"><span data-stu-id="d97a1-155">For organizations that need to be compliant with industry standards, such as [PCI DSS version 3.2](http://blog.pcisecuritystandards.org/preparing-for-pci-dss-32), multi-factor authentication is a must have capability for authenticate users.</span></span> <span data-ttu-id="d97a1-156">除了符合業界標準以外，強制執行 MFA 來驗證使用者，也可協助組織緩和認證竊取攻擊類型，例如[傳遞雜湊 (Pass-the-Hash，PtH)](http://aka.ms/PtHPaper)。</span><span class="sxs-lookup"><span data-stu-id="d97a1-156">Beyond being compliant with industry standards, enforcing MFA to authenticate users can also help organizations to mitigate credential theft type of attack, such as [Pass-the-Hash (PtH)](http://aka.ms/PtHPaper).</span></span>

<span data-ttu-id="d97a1-157">為您的使用者啟用 Azure MFA，您可為使用者登入和交易增加第二層安全性。</span><span class="sxs-lookup"><span data-stu-id="d97a1-157">By enabling Azure MFA for your users, you are adding a second layer of security to user sign-ins and transactions.</span></span> <span data-ttu-id="d97a1-158">在此情況下，交易可能會存取位於檔案伺服器或 SharePoint Online 中的文件。</span><span class="sxs-lookup"><span data-stu-id="d97a1-158">In this case, a transaction might be accessing a document located in a file server or in your SharePoint Online.</span></span> <span data-ttu-id="d97a1-159">Azure MFA 也可協助 IT 降低遭入侵的認證能夠存取公司資料的可能性。</span><span class="sxs-lookup"><span data-stu-id="d97a1-159">Azure MFA also helps IT to reduce the likelihood that a compromised credential will have access to organization’s data.</span></span>

<span data-ttu-id="d97a1-160">例如︰對您的使用者強制執行 Azure MFA，並將它設定為使用電話或簡訊進行驗證。</span><span class="sxs-lookup"><span data-stu-id="d97a1-160">For example: you enforce Azure MFA for your users and configure it to use a phone call or text message as verification.</span></span> <span data-ttu-id="d97a1-161">如果使用者的認證遭到入侵，攻擊者將無法存取任何資源，因為他無法存取使用者的電話。</span><span class="sxs-lookup"><span data-stu-id="d97a1-161">If the user’s credentials are compromised, the attacker won’t be able to access any resource since he will not have access to user’s phone.</span></span> <span data-ttu-id="d97a1-162">未新增額外身分識別保護層的組織會更容易受到認證竊取攻擊，這可能會導致資料洩漏。</span><span class="sxs-lookup"><span data-stu-id="d97a1-162">Organizations that do not add extra layers of identity protection are more susceptible for credential theft attack, which may lead to data compromise.</span></span>

<span data-ttu-id="d97a1-163">想要將整個驗證控制保留於內部部署的組織有一個替代方法，就是使用 [Azure Multi-factor Authentication Server](../multi-factor-authentication/multi-factor-authentication-get-started-server.md) (也稱為 MFA 內部部署)。</span><span class="sxs-lookup"><span data-stu-id="d97a1-163">One alternative for organizations that want to keep the entire authentication control on-premises is to use [Azure Multi-Factor Authentication Server](../multi-factor-authentication/multi-factor-authentication-get-started-server.md), also called MFA on-premises.</span></span> <span data-ttu-id="d97a1-164">使用此方法，您仍可強制執行 Multi-Factor Authentication，同時保留 MFA 伺服器內部部署。</span><span class="sxs-lookup"><span data-stu-id="d97a1-164">By using this method, you will still be able to enforce multi-factor authentication, while keeping the MFA server on-premises.</span></span>

<span data-ttu-id="d97a1-165">如需 Azure MFA 的詳細資訊，請參閱[開始在雲端中使用 Azure Multi-Factor Authentication](../multi-factor-authentication/multi-factor-authentication-get-started-cloud.md)。</span><span class="sxs-lookup"><span data-stu-id="d97a1-165">For more information on Azure MFA, please read the article [Getting started with Azure Multi-Factor Authentication in the cloud](../multi-factor-authentication/multi-factor-authentication-get-started-cloud.md).</span></span>

## <a name="use-role-based-access-control-rbac"></a><span data-ttu-id="d97a1-166">使用角色型存取控制 (RBAC)</span><span class="sxs-lookup"><span data-stu-id="d97a1-166">Use role based access control (RBAC)</span></span>
<span data-ttu-id="d97a1-167">對於想要強制執行資料存取安全性原則的組織，根據[需要知道](https://en.wikipedia.org/wiki/Need_to_know)和[最低權限](https://en.wikipedia.org/wiki/Principle_of_least_privilege)安全性原則限制存取權限是必須做的事。</span><span class="sxs-lookup"><span data-stu-id="d97a1-167">Restricting access based on the [need to know](https://en.wikipedia.org/wiki/Need_to_know) and [least privilege](https://en.wikipedia.org/wiki/Principle_of_least_privilege) security principles is imperative for organizations that want to enforce security policies for data access.</span></span> <span data-ttu-id="d97a1-168">Azure 角色型存取控制 (RBAC) 可用來指派權限給特定範圍的使用者、群組和應用程式。</span><span class="sxs-lookup"><span data-stu-id="d97a1-168">Azure Role-Based Access Control (RBAC) can be used to assign permissions to users, groups, and applications at a certain scope.</span></span> <span data-ttu-id="d97a1-169">角色指派的範圍可以是訂用帳戶、資源群組或單一資源。</span><span class="sxs-lookup"><span data-stu-id="d97a1-169">The scope of a role assignment can be a subscription, a resource group, or a single resource.</span></span>

<span data-ttu-id="d97a1-170">您可以利用 Azure 中[內建的 RBAC](../active-directory/role-based-access-built-in-roles.md) 角色指派權限給使用者。</span><span class="sxs-lookup"><span data-stu-id="d97a1-170">You can leverage [built in RBAC](../active-directory/role-based-access-built-in-roles.md) roles in Azure to assign privileges to users.</span></span> <span data-ttu-id="d97a1-171">請考慮將*儲存體帳戶參與者*用於需要管理儲存體帳戶的雲端操作者，以及使用*傳統儲存體帳戶參與者*角色來管理傳統儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="d97a1-171">Consider using *Storage Account Contributor* for cloud operators that need to manage storage accounts and *Classic Storage Account Contributor* role to manage classic storage accounts.</span></span> <span data-ttu-id="d97a1-172">對於需要管理 VM 和儲存體帳戶的雲端操作者，請考慮將他們新增至*虛擬機器參與者*角色。</span><span class="sxs-lookup"><span data-stu-id="d97a1-172">For cloud operators that needs to manage VMs and storage account, consider adding them to *Virtual Machine Contributor* role.</span></span>

<span data-ttu-id="d97a1-173">未利用諸如 RBAC 等功能來強制執行資料存取控制的組織，可能會對其使用者提供超過所需的權限。</span><span class="sxs-lookup"><span data-stu-id="d97a1-173">Organizations that do not enforce data access control by leveraging capabilities such as RBAC may be giving more privileges than necessary to their users.</span></span> <span data-ttu-id="d97a1-174">一開始就讓有些使用者存取他們不應具備的資料類型 (例如，高度業務衝擊)，可能會導致資料洩漏。</span><span class="sxs-lookup"><span data-stu-id="d97a1-174">This can lead to data compromise by allow users access to certain types of types of data (e.g., high business impact) that they shouldn’t have in the first place.</span></span>

<span data-ttu-id="d97a1-175">若要深入了解 Azure RBAC，請閱讀 [Azure 角色型存取控制](../active-directory/role-based-access-control-configure.md)一文。</span><span class="sxs-lookup"><span data-stu-id="d97a1-175">You can learn more about Azure RBAC by reading the article [Azure Role-Based Access Control](../active-directory/role-based-access-control-configure.md).</span></span>

## <a name="control-locations-where-resources-are-created-using-resource-manager"></a><span data-ttu-id="d97a1-176">使用資源管理員來控制資源的建立位置</span><span class="sxs-lookup"><span data-stu-id="d97a1-176">Control locations where resources are created using resource manager</span></span>
<span data-ttu-id="d97a1-177">讓雲端操作者能夠執行工作，同時防止他們違反管理組織資源所需的慣例極為重要。</span><span class="sxs-lookup"><span data-stu-id="d97a1-177">Enabling cloud operators to perform tasks while preventing them from breaking conventions that are needed to manage your organization's resources is very important.</span></span> <span data-ttu-id="d97a1-178">想要控制資源建立位置的組織應將這些位置硬式編碼。</span><span class="sxs-lookup"><span data-stu-id="d97a1-178">Organizations that want to control the locations where resources are created should hard code these locations.</span></span>

<span data-ttu-id="d97a1-179">若要達成此目標，組織可以建立安全性原則，其定義會描述明確拒絕的動作或資源。</span><span class="sxs-lookup"><span data-stu-id="d97a1-179">To achieve this, organizations can create security policies that have definitions that describe the actions or resources that are specifically denied.</span></span> <span data-ttu-id="d97a1-180">在所需範圍內指派那些原則定義，例如訂用帳戶、資源群組或是個別的資源。</span><span class="sxs-lookup"><span data-stu-id="d97a1-180">You assign those policy definitions at the desired scope, such as the subscription, resource group, or an individual resource.</span></span>

> [!NOTE]
> <span data-ttu-id="d97a1-181">這與 RBAC 不同，其實際利用 RBAC 來驗證使用者是否有建立這些資源的權限。</span><span class="sxs-lookup"><span data-stu-id="d97a1-181">this is not the same as RBAC, it actually leverages RBAC to authenticate the users that have privilege to create those resources.</span></span>
>
>

<span data-ttu-id="d97a1-182">利用 [Azure Resource Manager](../azure-resource-manager/resource-group-overview.md) 來建立適用於以下案例的自訂原則：組織只想在有相關聯的適當成本中心時允許作業，否則將拒絕要求。</span><span class="sxs-lookup"><span data-stu-id="d97a1-182">Leverage [Azure Resource Manager](../azure-resource-manager/resource-group-overview.md) to create custom policies also for scenarios where the organization wants to allow operations only when the appropriate cost center is associated; otherwise, they will deny the request.</span></span>

<span data-ttu-id="d97a1-183">不控制資源建立方式的組織比較容易遇到使用者因建立超過所需的資源而濫用服務。</span><span class="sxs-lookup"><span data-stu-id="d97a1-183">Organizations that are not controlling how resources are created are more susceptible to users that may abuse the service by creating more resources than they need.</span></span> <span data-ttu-id="d97a1-184">強化資源建立程序是保護多租用戶案例的重要步驟。</span><span class="sxs-lookup"><span data-stu-id="d97a1-184">Hardening the resource creation process is an important step to secure a multi-tenant scenario.</span></span>

<span data-ttu-id="d97a1-185">您可以閱讀使用原則來管理資源和控制存取，進一步了解如何[使用 Azure Resource Manager 建立原則](../azure-resource-manager/resource-manager-policy.md)。</span><span class="sxs-lookup"><span data-stu-id="d97a1-185">You can learn more about creating policies with Azure Resource Manager by reading the article [Use Policy to manage resources and control access](../azure-resource-manager/resource-manager-policy.md).</span></span>

## <a name="guide-developers-to-leverage-identity-capabilities-for-saas-apps"></a><span data-ttu-id="d97a1-186">引導開發人員運用 SaaS 應用程式的身分識別功能</span><span class="sxs-lookup"><span data-stu-id="d97a1-186">Guide developers to leverage identity capabilities for SaaS apps</span></span>
<span data-ttu-id="d97a1-187">當使用者存取可與內部部署或雲端目錄整合的 [SaaS 應用程式時](https://azure.microsoft.com/marketplace/active-directory/all/)，使用者身分識別會運用在許多案例中。</span><span class="sxs-lookup"><span data-stu-id="d97a1-187">User identity will be leveraged in many scenarios when users access [SaaS apps](https://azure.microsoft.com/marketplace/active-directory/all/) that can be integrated with on-premises or cloud directory.</span></span> <span data-ttu-id="d97a1-188">最重要的是，我們建議開發人員使用安全的方法來開發這些應用程式，例如 [Microsoft 安全性開發生命週期 (SDL)](https://www.microsoft.com/sdl/default.aspx)。</span><span class="sxs-lookup"><span data-stu-id="d97a1-188">First and foremost, we recommend that developers use a secure methodology to develop these apps, such as [Microsoft Security Development Lifecycle (SDL)](https://www.microsoft.com/sdl/default.aspx).</span></span> <span data-ttu-id="d97a1-189">Azure AD 提供身分識別做為服務，支援業界標準通訊協定 (例如 [OAuth 2.0](http://oauth.net/2/) 和 [OpenID Connect](http://openid.net/connect/))，以及適用於不同平台的開放原始碼程式庫，來簡化開發人員的驗證工作。</span><span class="sxs-lookup"><span data-stu-id="d97a1-189">Azure AD simplifies authentication for developers by providing identity as a service, with support for industry-standard protocols such as [OAuth 2.0](http://oauth.net/2/) and [OpenID Connect](http://openid.net/connect/), as well as open source libraries for different platforms.</span></span>

<span data-ttu-id="d97a1-190">務必註冊將驗證外包給 Azure AD 的任何應用程式，這是必要的程序。</span><span class="sxs-lookup"><span data-stu-id="d97a1-190">Make sure to register any application that outsources authentication to Azure AD, this is a mandatory procedure.</span></span> <span data-ttu-id="d97a1-191">其背後的理由是因為 Azure AD 在處理登入 (SSO) 或交換權杖時，需要座標才能與應用程式通訊。</span><span class="sxs-lookup"><span data-stu-id="d97a1-191">The reason behind this is because Azure AD needs to coordinate the communication with the application when handling sign-on (SSO) or exchanging tokens.</span></span> <span data-ttu-id="d97a1-192">當 Azure AD 所簽發的權杖存留期到期時，使用者工作階段就過期。</span><span class="sxs-lookup"><span data-stu-id="d97a1-192">The user’s session expires when the lifetime of the token issued by Azure AD expires.</span></span> <span data-ttu-id="d97a1-193">一定要評估您的應用程式是否應該使用此時間，或者可以縮短此時間。</span><span class="sxs-lookup"><span data-stu-id="d97a1-193">Always evaluate if your application should use this time or if you can reduce this time.</span></span> <span data-ttu-id="d97a1-194">縮短存留期可做為安全措施，以根據一段閒置時間強制使用者登出。</span><span class="sxs-lookup"><span data-stu-id="d97a1-194">Reducing the lifetime can act as a security measure that will force users to sign out based on a period of inactivity.</span></span>

<span data-ttu-id="d97a1-195">未強制身分識別控制存取應用程式且不會引導其開發人員如何安全地整合應用程式與其身分識別管理系統的組織，可能更容易遭受認證竊取攻擊類型，例如 [Open Web Application Security Project (OWASP) Top 10 中所述的弱式驗證與工作階段管理](https://www.owasp.org/index.php/OWASP_Top_Ten_Cheat_Sheet)。</span><span class="sxs-lookup"><span data-stu-id="d97a1-195">Organizations that do not enforce identity control to access apps and do not guide their developers on how to securely integrate apps with their identity management system may be more susceptible to credential theft type of attack, such as [weak authentication and session management described in Open Web Application Security Project (OWASP) Top 10](https://www.owasp.org/index.php/OWASP_Top_Ten_Cheat_Sheet).</span></span>

<span data-ttu-id="d97a1-196">您可以閱讀 [Azure AD 的驗證案例](../active-directory/active-directory-authentication-scenarios.md)，進一步了解 SaaS 應用程式的驗證案例。</span><span class="sxs-lookup"><span data-stu-id="d97a1-196">You can learn more about authentication scenarios for SaaS apps by reading [Authentication Scenarios for Azure AD](../active-directory/active-directory-authentication-scenarios.md).</span></span>

## <a name="actively-monitor-for-suspicious-activities"></a><span data-ttu-id="d97a1-197">主動監視可疑的活動</span><span class="sxs-lookup"><span data-stu-id="d97a1-197">Actively monitor for suspicious activities</span></span>
<span data-ttu-id="d97a1-198">根據 [Verizon 2016 資料缺口報告](http://www.verizonenterprise.com/verizon-insights-lab/dbir/2016/)，認證洩漏仍在上升中，並成為網路罪犯的最有利潤業務之一。</span><span class="sxs-lookup"><span data-stu-id="d97a1-198">According to [Verizon 2016 Data Breach report](http://www.verizonenterprise.com/verizon-insights-lab/dbir/2016/), credential compromise is still in the rise and becoming one of the most profitable businesses for cyber criminals.</span></span> <span data-ttu-id="d97a1-199">基於這個理由，請務必備妥可快速偵測可疑行為活動並觸發警示的主動身分識別監視系統，以便進一步調查。</span><span class="sxs-lookup"><span data-stu-id="d97a1-199">For this reason, it is important to have an active identity monitor system in place that can quickly detect suspicious behavior activity and trigger an alert for further investigation.</span></span> <span data-ttu-id="d97a1-200">Azure AD 有兩項主要功能可協助組織監視其身分識別：Azure AD Premium [異常報告](../active-directory/active-directory-view-access-usage-reports.md)與 [Azure AD 身分識別保護](../active-directory/active-directory-identityprotection.md)功能。</span><span class="sxs-lookup"><span data-stu-id="d97a1-200">Azure AD has two major capabilities that can help organizations monitor their identities: Azure AD Premium [anomaly reports](../active-directory/active-directory-view-access-usage-reports.md) and Azure AD [identity protection](../active-directory/active-directory-identityprotection.md) capability.</span></span>

<span data-ttu-id="d97a1-201">務必使用異常報告來找出[不被追蹤](../active-directory/active-directory-reporting-sign-ins-from-unknown-sources.md)的登入嘗試、對特定帳戶的[暴力密碼破解攻擊](../active-directory/active-directory-reporting-sign-ins-after-multiple-failures.md)、來自多個位置的登入嘗試，以及來自[受感染裝置](../active-directory/active-directory-reporting-sign-ins-from-possibly-infected-devices.md)和可疑 IP 位址的登入嘗試。</span><span class="sxs-lookup"><span data-stu-id="d97a1-201">Make sure to use the anomaly reports to identify attempts to sign in [without being traced](../active-directory/active-directory-reporting-sign-ins-from-unknown-sources.md), [brute force](../active-directory/active-directory-reporting-sign-ins-after-multiple-failures.md) attacks against a particular account, attempts to sign in from multiple locations, sign in from [infected devices](../active-directory/active-directory-reporting-sign-ins-from-possibly-infected-devices.md) and suspicious IP addresses.</span></span> <span data-ttu-id="d97a1-202">請記住，這些都是報告。</span><span class="sxs-lookup"><span data-stu-id="d97a1-202">Keep in mind that these are reports.</span></span> <span data-ttu-id="d97a1-203">換句話說，您必須備妥相關處理和程序，以便 IT 系統管理員每天或依需求執行這些報告 (通常出現在事件回應案例)。</span><span class="sxs-lookup"><span data-stu-id="d97a1-203">In other words, you must have processes and procedures in place for IT admins to run these reports on the daily basis or on demand (usually in an incident response scenario).</span></span>

<span data-ttu-id="d97a1-204">相反地，Azure AD Identity Protection 是主動監視系統，它會在自己的儀表板上標示目前的風險。</span><span class="sxs-lookup"><span data-stu-id="d97a1-204">In contrast, Azure AD identity protection is an active monitoring system and it will flag the current risks on its own dashboard.</span></span> <span data-ttu-id="d97a1-205">除此之外，您也會透過電子郵件收到每日摘要通知。</span><span class="sxs-lookup"><span data-stu-id="d97a1-205">Besides that, you will also receive daily summary notifications via email.</span></span> <span data-ttu-id="d97a1-206">我們建議根據您的業務需求調整風險層級。</span><span class="sxs-lookup"><span data-stu-id="d97a1-206">We recommend that you adjust the risk level according to your business requirements.</span></span> <span data-ttu-id="d97a1-207">風險事件的風險層級可表示風險事件的嚴重性 (高、中或低)。</span><span class="sxs-lookup"><span data-stu-id="d97a1-207">The risk level for a risk event is an indication (High, Medium, or Low) of the severity of the risk event.</span></span> <span data-ttu-id="d97a1-208">風險層級可協助 Identity Protection 使用者排定為了降低組織風險而必須採取之行動的優先順序。</span><span class="sxs-lookup"><span data-stu-id="d97a1-208">The risk level helps Identity Protection users prioritize the actions they must take to reduce the risk to their organization.</span></span>

<span data-ttu-id="d97a1-209">未主動監視其身分識別系統的組織有洩漏使用者認證的風險。</span><span class="sxs-lookup"><span data-stu-id="d97a1-209">Organizations that do not actively monitor their identity systems are at risk of having user credentials compromised.</span></span> <span data-ttu-id="d97a1-210">若不知道有使用這些認證進行的可疑活動，組織將無法減輕這類型的威脅。</span><span class="sxs-lookup"><span data-stu-id="d97a1-210">Without knowledge that suspicious activities are taking place using these credentials, organizations won’t be able to mitigate this type of threat.</span></span>
<span data-ttu-id="d97a1-211">您可以閱讀 [Azure Active Directory 身分識別保護](../active-directory/active-directory-identityprotection.md)，進一步了解 Azure 身分識別保護。</span><span class="sxs-lookup"><span data-stu-id="d97a1-211">You can learn more about Azure Identity protection by reading [Azure Active Directory Identity Protection](../active-directory/active-directory-identityprotection.md).</span></span>