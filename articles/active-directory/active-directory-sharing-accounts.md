---
title: "使用 Azure AD 的 aaaSharing 帳戶 |Microsoft 文件"
description: "描述 Azure Active Directory 如何讓組織 toosecurely 共用帳戶在內部部署應用程式和取用者雲端服務。"
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
ms.openlocfilehash: 9f98bfa97a6c9ba1566d3f921c1b676d5f3c2a88
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="sharing-accounts-with-azure-ad"></a><span data-ttu-id="d8778-103">使用 Azure AD 共用帳戶</span><span class="sxs-lookup"><span data-stu-id="d8778-103">Sharing accounts with Azure AD</span></span>
## <a name="overview"></a><span data-ttu-id="d8778-104">概觀</span><span class="sxs-lookup"><span data-stu-id="d8778-104">Overview</span></span>
<span data-ttu-id="d8778-105">有時候組織需要多人 toouse 單一使用者名稱和密碼。</span><span class="sxs-lookup"><span data-stu-id="d8778-105">Sometimes organizations need toouse a single username and password for multiple people.</span></span> <span data-ttu-id="d8778-106">這通常發生在兩個情況下：</span><span class="sxs-lookup"><span data-stu-id="d8778-106">This typically happens in two cases:</span></span>

* <span data-ttu-id="d8778-107">每個使用者必須使用唯一的登入和密碼存取應用程式時 (無論是內部部署的應用程式或取用者雲端服務，例如公司的社交媒體帳戶)。</span><span class="sxs-lookup"><span data-stu-id="d8778-107">When accessing applications that require a unique login and password for each user, whether on-premises apps or consumer cloud services ( e.g. corporate social media accounts).</span></span>
* <span data-ttu-id="d8778-108">建立多個使用者環境時。</span><span class="sxs-lookup"><span data-stu-id="d8778-108">When creating multi-user environments.</span></span> <span data-ttu-id="d8778-109">您可能需要一個單一的本機帳戶，具有更高的權限，而且可以是使用的 toodo 核心安裝、 管理和復原活動 （例如 hello 本機 「 全域系統管理員 」 帳戶在 Salesforce 中的 Office 365 或 hello 根帳戶）。</span><span class="sxs-lookup"><span data-stu-id="d8778-109">You may have a single, local account that has elevated privileges and can be used toodo core setup, administration, and recovery activities (e.g. hello local "global administrator" account for Office 365 or hello root account in Salesforce).</span></span>

<span data-ttu-id="d8778-110">傳統上，這些帳戶會共用由散發 hello 認證 （使用者名稱/密碼） toohello 恰當的人員或將其儲存在多個信任的代理程式可以存取它們的共用位置。</span><span class="sxs-lookup"><span data-stu-id="d8778-110">Traditionally, these accounts would be shared by distributing hello credentials (username/password) toohello right individuals or storing them in a shared location where multiple trusted agents can access them.</span></span>

<span data-ttu-id="d8778-111">hello 傳統共用模型有幾個缺點：</span><span class="sxs-lookup"><span data-stu-id="d8778-111">hello traditional sharing model has several drawbacks:</span></span>

* <span data-ttu-id="d8778-112">啟用存取 toonew 應用程式，需要在需要存取的 toodistribute 認證 tooeveryone。</span><span class="sxs-lookup"><span data-stu-id="d8778-112">Enabling access toonew applications requires you toodistribute credentials tooeveryone that needs access.</span></span>
* <span data-ttu-id="d8778-113">每個共用的應用程式可能需要它自己組唯一的共用的認證，需要使用者 tooremember 多組認證。</span><span class="sxs-lookup"><span data-stu-id="d8778-113">Each shared application may require its own unique set of shared credentials, requiring users tooremember multiple sets of credentials.</span></span> <span data-ttu-id="d8778-114">當使用者擁有 tooremember 許多的認證時，hello 風險會增加他們將採用 toorisky 作法。</span><span class="sxs-lookup"><span data-stu-id="d8778-114">When users have tooremember many credentials, hello risk increases that they will resort toorisky practices.</span></span> <span data-ttu-id="d8778-115">(例如寫下密碼。)</span><span class="sxs-lookup"><span data-stu-id="d8778-115">(e.g. writing down passwords).</span></span>
* <span data-ttu-id="d8778-116">您無法分辨誰存取 tooan 應用程式。</span><span class="sxs-lookup"><span data-stu-id="d8778-116">You can't tell who has access tooan application.</span></span>
* <span data-ttu-id="d8778-117">您不知道誰 *存取* 了應用程式。</span><span class="sxs-lookup"><span data-stu-id="d8778-117">You can't tell who has *accessed* an application.</span></span>
* <span data-ttu-id="d8778-118">當您需要 tooremove 存取 tooan 應用程式時，您擁有 tooupdate hello 認證，並且將它們重新發佈 tooeveryone 需要存取 toothat 應用程式。</span><span class="sxs-lookup"><span data-stu-id="d8778-118">When you need tooremove access tooan application, you have tooupdate hello credentials and re-distribute them tooeveryone that needs access toothat application.</span></span>

## <a name="azure-active-directory-account-sharing"></a><span data-ttu-id="d8778-119">Azure Active Directory 帳戶共用</span><span class="sxs-lookup"><span data-stu-id="d8778-119">Azure Active Directory account sharing</span></span>
<span data-ttu-id="d8778-120">Azure AD 提供的新方法可消除這些缺點 toousing 共用帳戶。</span><span class="sxs-lookup"><span data-stu-id="d8778-120">Azure AD provides a new approach toousing shared accounts that eliminates these drawbacks.</span></span>

<span data-ttu-id="d8778-121">hello Azure AD 系統管理員所設定的使用者可以存取使用 hello 存取面板，然後選擇 單一登入該應用程式最適合的 hello 類型的應用程式。</span><span class="sxs-lookup"><span data-stu-id="d8778-121">hello Azure AD administrator configures which applications a user can access by using hello Access Panel and choosing hello type of single sign-on best suited for that application.</span></span> <span data-ttu-id="d8778-122">其中一種類型，*密碼型單一登入*，可讓 Azure AD 做為類型的"broker"hello 登入程序期間，應用程式。</span><span class="sxs-lookup"><span data-stu-id="d8778-122">One of those types, *password-based single-sign on*, lets Azure AD act as a kind of "broker" during hello sign-on process for that app.</span></span>

<span data-ttu-id="d8778-123">使用者使用他們的組織帳戶登入一次。</span><span class="sxs-lookup"><span data-stu-id="d8778-123">Users log in once with their organizational account.</span></span> <span data-ttu-id="d8778-124">這是 hello 他們經常使用 tooaccess，其桌上型電腦或電子郵件的相同帳戶。</span><span class="sxs-lookup"><span data-stu-id="d8778-124">This is hello same account that they regularly use tooaccess their desktop or email.</span></span> <span data-ttu-id="d8778-125">他們只能探索和存取指派給他們的那些應用程式。</span><span class="sxs-lookup"><span data-stu-id="d8778-125">They can discover and access only those applications that they are assigned to.</span></span> <span data-ttu-id="d8778-126">使用共用帳戶，這份應用程式清單可以包含任何數目的共用認證。</span><span class="sxs-lookup"><span data-stu-id="d8778-126">With shared accounts, this list of applications can include any number of shared credentials.</span></span> <span data-ttu-id="d8778-127">hello 終端使用者不需要 tooremember 或寫下 hello 各種可能使用的帳戶。</span><span class="sxs-lookup"><span data-stu-id="d8778-127">hello end user doesn't need tooremember or write down hello various accounts they may be using.</span></span>

<span data-ttu-id="d8778-128">共用帳戶不只增加監督的方便性和改善可用性，也可增強安全性。</span><span class="sxs-lookup"><span data-stu-id="d8778-128">Shared accounts not only increase oversight and improve usability, they also enhance your security.</span></span> <span data-ttu-id="d8778-129">具有權限 toouse hello 認證的使用者看 hello 共用的密碼，但而取得的權限 toouse hello 密碼當做驗證協調的流程的一部分。</span><span class="sxs-lookup"><span data-stu-id="d8778-129">Users with permissions toouse hello credentials don't see hello shared password, but rather get permissions toouse hello password as part of an orchestrated authentication flow.</span></span> <span data-ttu-id="d8778-130">此外，某些密碼 SSO 應用程式中，您擁有 hello 選項 toohave Azure AD 定期變換 （更新） hello 密碼使用大型、 複雜密碼，增加 hello 帳戶安全性。</span><span class="sxs-lookup"><span data-stu-id="d8778-130">Further, with some password SSO applications, you have hello option toohave Azure AD periodically rollover (update) hello password using large, complex passwords, increasing hello account security.</span></span> <span data-ttu-id="d8778-131">hello 系統管理員可以輕鬆地授與或撤銷存取 tooan 應用程式，也知道誰有存取 toohello 帳戶，以及誰在存取它在過去的 hello。</span><span class="sxs-lookup"><span data-stu-id="d8778-131">hello administrator can easily grant or revoke access tooan application and also know who has access toohello account and who accessed it in hello past.</span></span>

<span data-ttu-id="d8778-132">Azure AD 支援的共用帳戶適用於任何Enterprise Mobility Suite (EMS)、進階或基本型的授權使用者，含括所有類型的密碼單一登入應用程式。</span><span class="sxs-lookup"><span data-stu-id="d8778-132">Azure AD supports shared accounts for any Enterprise Mobility Suite (EMS), Premium, or Basic licensed users, across all types of password single sign on applications.</span></span> <span data-ttu-id="d8778-133">您可以共用任何數千種預先整合的應用程式在 hello 應用程式庫中的帳戶，並可以加入自己的密碼驗證的應用程式與[自訂 SSO 應用程式](active-directory-sso-integrate-saas-apps.md)。</span><span class="sxs-lookup"><span data-stu-id="d8778-133">You can share accounts for any of thousands of pre-integrated applications in hello application gallery and can add your own password-authenticating application with [custom SSO apps](active-directory-sso-integrate-saas-apps.md).</span></span>

<span data-ttu-id="d8778-134">啟用帳戶共用的 Azure AD 功能包括：</span><span class="sxs-lookup"><span data-stu-id="d8778-134">Azure AD features that enable account sharing include:</span></span>

* [<span data-ttu-id="d8778-135">密碼單一登入</span><span class="sxs-lookup"><span data-stu-id="d8778-135">Password single sign-on</span></span>](active-directory-appssoaccess-whatis.md#password-based-single-sign-on)
* <span data-ttu-id="d8778-136">密碼單一登入代理程式</span><span class="sxs-lookup"><span data-stu-id="d8778-136">Password single sign-on agent</span></span>
* [<span data-ttu-id="d8778-137">群組指派</span><span class="sxs-lookup"><span data-stu-id="d8778-137">Group assignment</span></span>](active-directory-accessmanagement-self-service-group-management.md)
* <span data-ttu-id="d8778-138">自訂密碼應用程式</span><span class="sxs-lookup"><span data-stu-id="d8778-138">Custom Password apps</span></span>
* [<span data-ttu-id="d8778-139">應用程式使用量儀表板/報告</span><span class="sxs-lookup"><span data-stu-id="d8778-139">App usage dashboard/reports</span></span>](active-directory-passwords-get-insights.md)
* <span data-ttu-id="d8778-140">使用者存取入口網站</span><span class="sxs-lookup"><span data-stu-id="d8778-140">End user access portals</span></span>
* [<span data-ttu-id="d8778-141">應用程式 proxy</span><span class="sxs-lookup"><span data-stu-id="d8778-141">App proxy</span></span>](active-directory-application-proxy-get-started.md)
* [<span data-ttu-id="d8778-142">Active Directory 市集</span><span class="sxs-lookup"><span data-stu-id="d8778-142">Active Directory Marketplace</span></span>](https://azure.microsoft.com/marketplace/active-directory/all/)

## <a name="sharing-an-account"></a><span data-ttu-id="d8778-143">共用帳戶</span><span class="sxs-lookup"><span data-stu-id="d8778-143">Sharing an account</span></span>
<span data-ttu-id="d8778-144">Azure AD toouse tooshare 帳戶您必須：</span><span class="sxs-lookup"><span data-stu-id="d8778-144">toouse Azure AD tooshare an account you will need to:</span></span>

* <span data-ttu-id="d8778-145">新增應用程式[應用程式庫](https://azure.microsoft.com/marketplace/active-directory/)或[自訂應用程式](http://blogs.technet.com/b/ad/archive/2015/06/17/bring-your-own-app-with-azure-ad-self-service-saml-configuration-gt-now-in-preview.aspx)</span><span class="sxs-lookup"><span data-stu-id="d8778-145">Add an application [app gallery](https://azure.microsoft.com/marketplace/active-directory/) or [custom application](http://blogs.technet.com/b/ad/archive/2015/06/17/bring-your-own-app-with-azure-ad-self-service-saml-configuration-gt-now-in-preview.aspx)</span></span>
* <span data-ttu-id="d8778-146">設定密碼單一登入 (SSO) 的 hello 應用程式</span><span class="sxs-lookup"><span data-stu-id="d8778-146">Configure hello application for password Single Sign-On (SSO)</span></span>
* <span data-ttu-id="d8778-147">使用[群組為基礎的指派](active-directory-accessmanagement-group-saasapps.md)和選取 hello 選項 tooenter 共用的認證</span><span class="sxs-lookup"><span data-stu-id="d8778-147">Use [group based assignment](active-directory-accessmanagement-group-saasapps.md) and select hello option tooenter a shared credential</span></span>
* <span data-ttu-id="d8778-148">選擇性： 在某些應用程式，例如 Facebook、 Twitter 或 LinkedIn，您可以啟用 hello 選項[Azure AD 自動密碼變換](http://blogs.technet.com/b/ad/archive/2015/02/20/azure-ad-automated-password-roll-over-for-facebook-twitter-and-linkedin-now-in-preview.aspx)</span><span class="sxs-lookup"><span data-stu-id="d8778-148">Optional: in some applications, such as Facebook, Twitter, or LinkedIn, you can enable hello option for [Azure AD automated password roll-over](http://blogs.technet.com/b/ad/archive/2015/02/20/azure-ad-automated-password-roll-over-for-facebook-twitter-and-linkedin-now-in-preview.aspx)</span></span>

<span data-ttu-id="d8778-149">您也可以讓您共用的帳戶更安全的多重要素驗證 (MFA) (深入了解[保護應用程式與 Azure AD](../multi-factor-authentication/multi-factor-authentication-get-started.md))，您可以將委派 hello 能力 toomanage 擁有存取 toohello 應用程式使用[Azure AD 自助式](active-directory-accessmanagement-self-service-group-management.md)群組管理。</span><span class="sxs-lookup"><span data-stu-id="d8778-149">You can also make your shared account more secure with Multi-Factor Authentication (MFA) (learn more about [securing applications with Azure AD](../multi-factor-authentication/multi-factor-authentication-get-started.md)) and you can delegate hello ability toomanage who has access toohello application using [Azure AD Self-service](active-directory-accessmanagement-self-service-group-management.md) Group Management.</span></span>

## <a name="related-articles"></a><span data-ttu-id="d8778-150">相關文章</span><span class="sxs-lookup"><span data-stu-id="d8778-150">Related articles</span></span>
* [<span data-ttu-id="d8778-151">Article Index for Application Management in Azure Active Directory (Azure Active Directory 中應用程式管理的文件索引)</span><span class="sxs-lookup"><span data-stu-id="d8778-151">Article Index for Application Management in Azure Active Directory</span></span>](active-directory-apps-index.md)
* [<span data-ttu-id="d8778-152">使用條件式存取來保護應用程式</span><span class="sxs-lookup"><span data-stu-id="d8778-152">Protecting apps with conditional access</span></span>](active-directory-conditional-access.md)
* [<span data-ttu-id="d8778-153">自助式群組管理/SSAA</span><span class="sxs-lookup"><span data-stu-id="d8778-153">Self-service group management/SSAA</span></span>](active-directory-accessmanagement-self-service-group-management.md)

