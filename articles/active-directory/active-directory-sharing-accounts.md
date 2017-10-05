---
title: "使用 Azure AD 共用帳戶 | Microsoft Docs"
description: "描述 Azure Active Directory 如何讓組織安全地共用內部部署應用程式和取用者雲端服務的帳戶。"
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: e2d77104-d978-46a3-bfea-03ffdf3b61e6
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/04/2017
ms.author: curtand
ms.openlocfilehash: b40335eda9dffe75e65d004837a1d67914db15b6
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="sharing-accounts-with-azure-ad"></a><span data-ttu-id="aa77a-103">使用 Azure AD 共用帳戶</span><span class="sxs-lookup"><span data-stu-id="aa77a-103">Sharing accounts with Azure AD</span></span>
## <a name="overview"></a><span data-ttu-id="aa77a-104">Overview</span><span class="sxs-lookup"><span data-stu-id="aa77a-104">Overview</span></span>
<span data-ttu-id="aa77a-105">有時候組織需要針對多人使用單一使用者名稱和密碼。</span><span class="sxs-lookup"><span data-stu-id="aa77a-105">Sometimes organizations need to use a single username and password for multiple people.</span></span> <span data-ttu-id="aa77a-106">這通常發生在兩個情況下：</span><span class="sxs-lookup"><span data-stu-id="aa77a-106">This typically happens in two cases:</span></span>

* <span data-ttu-id="aa77a-107">每個使用者必須使用唯一的登入和密碼存取應用程式時 (無論是內部部署的應用程式或取用者雲端服務，例如公司的社交媒體帳戶)。</span><span class="sxs-lookup"><span data-stu-id="aa77a-107">When accessing applications that require a unique login and password for each user, whether on-premises apps or consumer cloud services ( e.g. corporate social media accounts).</span></span>
* <span data-ttu-id="aa77a-108">建立多個使用者環境時。</span><span class="sxs-lookup"><span data-stu-id="aa77a-108">When creating multi-user environments.</span></span> <span data-ttu-id="aa77a-109">您可能有具備較高權限的單一本機帳戶可用來執行核心安裝、管理及復原活動 (例如 Office 365 的本機「全域系統管理員」帳戶或 Salesforce 中的根帳戶)。</span><span class="sxs-lookup"><span data-stu-id="aa77a-109">You may have a single, local account that has elevated privileges and can be used to do core setup, administration, and recovery activities (e.g. the local "global administrator" account for Office 365 or the root account in Salesforce).</span></span>

<span data-ttu-id="aa77a-110">傳統上，這些帳戶的共用方式是透過將認證 (使用者名稱/密碼) 散發給適當的人員，或是將認證儲存在多個受信任的代理人可以存取的共用位置。</span><span class="sxs-lookup"><span data-stu-id="aa77a-110">Traditionally, these accounts would be shared by distributing the credentials (username/password) to the right individuals or storing them in a shared location where multiple trusted agents can access them.</span></span>

<span data-ttu-id="aa77a-111">傳統共用模型有幾個缺點：</span><span class="sxs-lookup"><span data-stu-id="aa77a-111">The traditional sharing model has several drawbacks:</span></span>

* <span data-ttu-id="aa77a-112">您必須將認證散發給需要存取新應用程式的所有人，他們才能進行存取。</span><span class="sxs-lookup"><span data-stu-id="aa77a-112">Enabling access to new applications requires you to distribute credentials to everyone that needs access.</span></span>
* <span data-ttu-id="aa77a-113">每個共用的應用程式可能都需要唯一的一組共用認證，使用者必須記住許多組認證。</span><span class="sxs-lookup"><span data-stu-id="aa77a-113">Each shared application may require its own unique set of shared credentials, requiring users to remember multiple sets of credentials.</span></span> <span data-ttu-id="aa77a-114">當使用者必須記住許多認證時，他們會依靠有風險的做法，風險因此會增加。</span><span class="sxs-lookup"><span data-stu-id="aa77a-114">When users have to remember many credentials, the risk increases that they will resort to risky practices.</span></span> <span data-ttu-id="aa77a-115">(例如寫下密碼。)</span><span class="sxs-lookup"><span data-stu-id="aa77a-115">(e.g. writing down passwords).</span></span>
* <span data-ttu-id="aa77a-116">您不知道誰有權存取應用程式。</span><span class="sxs-lookup"><span data-stu-id="aa77a-116">You can't tell who has access to an application.</span></span>
* <span data-ttu-id="aa77a-117">您不知道誰 *存取* 了應用程式。</span><span class="sxs-lookup"><span data-stu-id="aa77a-117">You can't tell who has *accessed* an application.</span></span>
* <span data-ttu-id="aa77a-118">當您需要移除某個應用程式的存取權時，您必須更新認證，並將認證重新散發給需要存取該應用程式的所有人。</span><span class="sxs-lookup"><span data-stu-id="aa77a-118">When you need to remove access to an application, you have to update the credentials and re-distribute them to everyone that needs access to that application.</span></span>

## <a name="azure-active-directory-account-sharing"></a><span data-ttu-id="aa77a-119">Azure Active Directory 帳戶共用</span><span class="sxs-lookup"><span data-stu-id="aa77a-119">Azure Active Directory account sharing</span></span>
<span data-ttu-id="aa77a-120">Azure AD 提供使用共用帳戶的新方法，可以消除這些缺點。</span><span class="sxs-lookup"><span data-stu-id="aa77a-120">Azure AD provides a new approach to using shared accounts that eliminates these drawbacks.</span></span>

<span data-ttu-id="aa77a-121">透過使用「存取面板」並選擇最適合該應用程式的單一登入類型，Azure AD 系統管理員可以設定使用者可以存取的應用程式。</span><span class="sxs-lookup"><span data-stu-id="aa77a-121">The Azure AD administrator configures which applications a user can access by using the Access Panel and choosing the type of single sign-on best suited for that application.</span></span> <span data-ttu-id="aa77a-122">其中的「密碼單一登入」 類型在該應用程式的登入程序期間，可讓 Azure AD 做為一種「代理程式」。</span><span class="sxs-lookup"><span data-stu-id="aa77a-122">One of those types, *password-based single-sign on*, lets Azure AD act as a kind of "broker" during the sign-on process for that app.</span></span>

<span data-ttu-id="aa77a-123">使用者使用他們的組織帳戶登入一次。</span><span class="sxs-lookup"><span data-stu-id="aa77a-123">Users log in once with their organizational account.</span></span> <span data-ttu-id="aa77a-124">這與他們平常用來存取桌面或電子郵件的帳戶相同。</span><span class="sxs-lookup"><span data-stu-id="aa77a-124">This is the same account that they regularly use to access their desktop or email.</span></span> <span data-ttu-id="aa77a-125">他們只能探索和存取指派給他們的那些應用程式。</span><span class="sxs-lookup"><span data-stu-id="aa77a-125">They can discover and access only those applications that they are assigned to.</span></span> <span data-ttu-id="aa77a-126">使用共用帳戶，這份應用程式清單可以包含任何數目的共用認證。</span><span class="sxs-lookup"><span data-stu-id="aa77a-126">With shared accounts, this list of applications can include any number of shared credentials.</span></span> <span data-ttu-id="aa77a-127">使用者不需記住或寫下多個可能使用的帳戶。</span><span class="sxs-lookup"><span data-stu-id="aa77a-127">The end user doesn't need to remember or write down the various accounts they may be using.</span></span>

<span data-ttu-id="aa77a-128">共用帳戶不只增加監督的方便性和改善可用性，也可增強安全性。</span><span class="sxs-lookup"><span data-stu-id="aa77a-128">Shared accounts not only increase oversight and improve usability, they also enhance your security.</span></span> <span data-ttu-id="aa77a-129">具有認證使用權限的使用者看不到共用密碼，而是會在協調的驗證流程當中取得密碼的使用權限。</span><span class="sxs-lookup"><span data-stu-id="aa77a-129">Users with permissions to use the credentials don't see the shared password, but rather get permissions to use the password as part of an orchestrated authentication flow.</span></span> <span data-ttu-id="aa77a-130">此外，使用某些密碼 SSO 應用程式時，您可選擇讓 Azure AD 定期使用字元數多的複雜密碼來變換 (更新) 密碼，以提升帳戶安全性。</span><span class="sxs-lookup"><span data-stu-id="aa77a-130">Further, with some password SSO applications, you have the option to have Azure AD periodically rollover (update) the password using large, complex passwords, increasing the account security.</span></span> <span data-ttu-id="aa77a-131">系統管理員可以輕易地授與或撤銷應用程式的存取權，也可以知道誰有權存取帳戶以及誰曾經存取帳戶。</span><span class="sxs-lookup"><span data-stu-id="aa77a-131">The administrator can easily grant or revoke access to an application and also know who has access to the account and who accessed it in the past.</span></span>

<span data-ttu-id="aa77a-132">Azure AD 支援的共用帳戶適用於任何Enterprise Mobility Suite (EMS)、進階或基本型的授權使用者，含括所有類型的密碼單一登入應用程式。</span><span class="sxs-lookup"><span data-stu-id="aa77a-132">Azure AD supports shared accounts for any Enterprise Mobility Suite (EMS), Premium, or Basic licensed users, across all types of password single sign on applications.</span></span> <span data-ttu-id="aa77a-133">您可以共用應用程式庫中數千個預先整合的應用程式的帳戶，並可加入含有 [自訂 SSO 應用程式](active-directory-sso-integrate-saas-apps.md)的密碼驗證應用程式。</span><span class="sxs-lookup"><span data-stu-id="aa77a-133">You can share accounts for any of thousands of pre-integrated applications in the application gallery and can add your own password-authenticating application with [custom SSO apps](active-directory-sso-integrate-saas-apps.md).</span></span>

<span data-ttu-id="aa77a-134">啟用帳戶共用的 Azure AD 功能包括：</span><span class="sxs-lookup"><span data-stu-id="aa77a-134">Azure AD features that enable account sharing include:</span></span>

* [<span data-ttu-id="aa77a-135">密碼單一登入</span><span class="sxs-lookup"><span data-stu-id="aa77a-135">Password single sign-on</span></span>](active-directory-appssoaccess-whatis.md#password-based-single-sign-on)
* <span data-ttu-id="aa77a-136">密碼單一登入代理程式</span><span class="sxs-lookup"><span data-stu-id="aa77a-136">Password single sign-on agent</span></span>
* [<span data-ttu-id="aa77a-137">群組指派</span><span class="sxs-lookup"><span data-stu-id="aa77a-137">Group assignment</span></span>](active-directory-accessmanagement-self-service-group-management.md)
* <span data-ttu-id="aa77a-138">自訂密碼應用程式</span><span class="sxs-lookup"><span data-stu-id="aa77a-138">Custom Password apps</span></span>
* [<span data-ttu-id="aa77a-139">應用程式使用量儀表板/報告</span><span class="sxs-lookup"><span data-stu-id="aa77a-139">App usage dashboard/reports</span></span>](active-directory-passwords-get-insights.md)
* <span data-ttu-id="aa77a-140">使用者存取入口網站</span><span class="sxs-lookup"><span data-stu-id="aa77a-140">End user access portals</span></span>
* [<span data-ttu-id="aa77a-141">應用程式 proxy</span><span class="sxs-lookup"><span data-stu-id="aa77a-141">App proxy</span></span>](active-directory-application-proxy-get-started.md)
* [<span data-ttu-id="aa77a-142">Active Directory 市集</span><span class="sxs-lookup"><span data-stu-id="aa77a-142">Active Directory Marketplace</span></span>](https://azure.microsoft.com/marketplace/active-directory/all/)

## <a name="sharing-an-account"></a><span data-ttu-id="aa77a-143">共用帳戶</span><span class="sxs-lookup"><span data-stu-id="aa77a-143">Sharing an account</span></span>
<span data-ttu-id="aa77a-144">若要使用 Azure AD 來共用帳戶，您必須：</span><span class="sxs-lookup"><span data-stu-id="aa77a-144">To use Azure AD to share an account you will need to:</span></span>

* <span data-ttu-id="aa77a-145">新增應用程式[應用程式庫](https://azure.microsoft.com/marketplace/active-directory/)或[自訂應用程式](http://blogs.technet.com/b/ad/archive/2015/06/17/bring-your-own-app-with-azure-ad-self-service-saml-configuration-gt-now-in-preview.aspx)</span><span class="sxs-lookup"><span data-stu-id="aa77a-145">Add an application [app gallery](https://azure.microsoft.com/marketplace/active-directory/) or [custom application](http://blogs.technet.com/b/ad/archive/2015/06/17/bring-your-own-app-with-azure-ad-self-service-saml-configuration-gt-now-in-preview.aspx)</span></span>
* <span data-ttu-id="aa77a-146">設定應用程式使用密碼單一登入 (SSO)</span><span class="sxs-lookup"><span data-stu-id="aa77a-146">Configure the application for password Single Sign-On (SSO)</span></span>
* <span data-ttu-id="aa77a-147">使用 [以群組為基礎的指派](active-directory-accessmanagement-group-saasapps.md) ，並選取輸入共用認證的選項</span><span class="sxs-lookup"><span data-stu-id="aa77a-147">Use [group based assignment](active-directory-accessmanagement-group-saasapps.md) and select the option to enter a shared credential</span></span>
* <span data-ttu-id="aa77a-148">選擇性：在某些應用程式 (例如 Facebook、Twitter 或 LinkedIn) 中，您可以啟用 [Azure AD 自動變換密碼](http://blogs.technet.com/b/ad/archive/2015/02/20/azure-ad-automated-password-roll-over-for-facebook-twitter-and-linkedin-now-in-preview.aspx)</span><span class="sxs-lookup"><span data-stu-id="aa77a-148">Optional: in some applications, such as Facebook, Twitter, or LinkedIn, you can enable the option for [Azure AD automated password roll-over](http://blogs.technet.com/b/ad/archive/2015/02/20/azure-ad-automated-password-roll-over-for-facebook-twitter-and-linkedin-now-in-preview.aspx)</span></span>

<span data-ttu-id="aa77a-149">使用 Azure AD，可以透過 Multi-Factor Authentication (MFA) 讓您的共用帳戶更安全 (深入了解[使用 Azure AD 保護應用程式](../multi-factor-authentication/multi-factor-authentication-get-started.md))，並可使用 [Azure AD 自助式](active-directory-accessmanagement-self-service-group-management.md)群組管理來委派管理誰有權存取應用程式。</span><span class="sxs-lookup"><span data-stu-id="aa77a-149">You can also make your shared account more secure with Multi-Factor Authentication (MFA) (learn more about [securing applications with Azure AD](../multi-factor-authentication/multi-factor-authentication-get-started.md)) and you can delegate the ability to manage who has access to the application using [Azure AD Self-service](active-directory-accessmanagement-self-service-group-management.md) Group Management.</span></span>

## <a name="related-articles"></a><span data-ttu-id="aa77a-150">相關文章</span><span class="sxs-lookup"><span data-stu-id="aa77a-150">Related articles</span></span>
* [<span data-ttu-id="aa77a-151">Article Index for Application Management in Azure Active Directory (Azure Active Directory 中應用程式管理的文件索引)</span><span class="sxs-lookup"><span data-stu-id="aa77a-151">Article Index for Application Management in Azure Active Directory</span></span>](active-directory-apps-index.md)
* [<span data-ttu-id="aa77a-152">使用條件式存取來保護應用程式</span><span class="sxs-lookup"><span data-stu-id="aa77a-152">Protecting apps with conditional access</span></span>](active-directory-conditional-access.md)
* [<span data-ttu-id="aa77a-153">自助式群組管理/SSAA</span><span class="sxs-lookup"><span data-stu-id="aa77a-153">Self-service group management/SSAA</span></span>](active-directory-accessmanagement-self-service-group-management.md)

