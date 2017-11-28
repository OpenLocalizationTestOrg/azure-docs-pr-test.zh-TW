---
title: "aaaApplications 和瀏覽器的 Azure Active Directory 中使用條件式存取規則 |Microsoft 文件"
description: "條件式存取控制與 Azure Active Directory 檢查特定條件時，它會驗證 hello 使用者及 tooallow 應用程式存取。"
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
ms.assetid: 62349fba-3cc0-4ab5-babe-372b3389eff6
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 08/22/2017
ms.author: markvi
ms.reviewer: calebb
ms.openlocfilehash: ca20853bb9f4b22d0b88ddd2f051d658e0d88cf3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="applications-and-browsers-that-use-conditional-access-rules-in-azure-active-directory"></a><span data-ttu-id="754bf-103">在 Azure Active Directory 中使用條件式存取規則的應用程式和瀏覽器</span><span class="sxs-lookup"><span data-stu-id="754bf-103">Applications and browsers that use conditional access rules in Azure Active Directory</span></span>

<span data-ttu-id="754bf-104">Azure Active Directory (Azure AD) 連線應用程式、預先整合的同盟軟體即服務 (SaaS) 應用程式、使用密碼單一登入 (SSO) 的應用程式、商務營運應用程式以及使用 Azure AD 應用程式 Proxy 的應用程式，都支援條件式存取規則。</span><span class="sxs-lookup"><span data-stu-id="754bf-104">Conditional access rules are supported in Azure Active Directory (Azure AD)-connected applications, pre-integrated federated software as a service (SaaS) applications, applications that use password single sign-on (SSO), line-of-business applications, and applications that use Azure AD Application Proxy.</span></span> <span data-ttu-id="754bf-105">如需可使用條件式存取的應用程式詳細清單，請參閱[已啟用條件式存取功能的服務](active-directory-conditional-access-technical-reference.md)。</span><span class="sxs-lookup"><span data-stu-id="754bf-105">For a detailed list of applications for which you can use conditional access, see [Services enabled with conditional access](active-directory-conditional-access-technical-reference.md).</span></span> <span data-ttu-id="754bf-106">條件式存取可以與運用新式驗證的行動和傳統型應用程式搭配使用。</span><span class="sxs-lookup"><span data-stu-id="754bf-106">Conditional access works both with mobile and desktop applications that use modern authentication.</span></span> <span data-ttu-id="754bf-107">在本文中，我們將討論條件式存取功能在行動和桌面應用程式中的運作方式。</span><span class="sxs-lookup"><span data-stu-id="754bf-107">In this article, we cover how conditional access works in mobile and desktop apps.</span></span>

<span data-ttu-id="754bf-108">您可以在使用新式驗證的應用程式中使用 Azure AD 登入頁面。</span><span class="sxs-lookup"><span data-stu-id="754bf-108">You can use Azure AD sign-in pages in applications that use modern authentication.</span></span> <span data-ttu-id="754bf-109">在登入頁面中，系統會提示您進行 Multi-Factor Authentication。</span><span class="sxs-lookup"><span data-stu-id="754bf-109">With a sign-in page, a user is prompted for multi-factor authentication.</span></span> <span data-ttu-id="754bf-110">會顯示訊息，是否將會封鎖 hello 使用者的存取權。</span><span class="sxs-lookup"><span data-stu-id="754bf-110">A message is shown if hello user's access is blocked.</span></span> <span data-ttu-id="754bf-111">以裝置型條件式存取原則評估需要使用 Azure AD，hello 裝置 tooauthenticate 新式驗證。</span><span class="sxs-lookup"><span data-stu-id="754bf-111">Modern authentication is required for hello device tooauthenticate with Azure AD, so that device-based conditional access policies are evaluated.</span></span>

<span data-ttu-id="754bf-112">它是重要 tooknow 哪些應用程式可以使用條件式存取規則，並在 hello 步驟，您可能需要 tootake toosecure 其他應用程式進入點。</span><span class="sxs-lookup"><span data-stu-id="754bf-112">It's important tooknow which applications can use conditional access rules, and hello steps that you might need tootake toosecure other application entry points.</span></span>

## <a name="applications-that-use-modern-authentication"></a><span data-ttu-id="754bf-113">使用新式驗證的應用程式</span><span class="sxs-lookup"><span data-stu-id="754bf-113">Applications that use modern authentication</span></span>
> [!NOTE]
> <span data-ttu-id="754bf-114">如果 Azure AD 中的條件式存取原則等同於 Office 365 中的條件式存取原則，請設定這兩個條件式存取原則。</span><span class="sxs-lookup"><span data-stu-id="754bf-114">If you have a conditional access policy in Azure AD that has an equivalent in Office 365, configure both conditional access policies.</span></span> <span data-ttu-id="754bf-115">這會套用，比方說，tooconditional Exchange Online 或 SharePoint Online 的存取原則。</span><span class="sxs-lookup"><span data-stu-id="754bf-115">This would apply, for example, tooconditional access policies for Exchange Online or SharePoint Online.</span></span>
>
>

<span data-ttu-id="754bf-116">hello 下列應用程式支援條件式存取 Office 365 和其他 Azure AD 連線的服務應用程式：</span><span class="sxs-lookup"><span data-stu-id="754bf-116">hello following applications support conditional access for Office 365 and other Azure AD-connected service applications:</span></span>


| <span data-ttu-id="754bf-117">目標服務</span><span class="sxs-lookup"><span data-stu-id="754bf-117">Target Service</span></span>| <span data-ttu-id="754bf-118">平台</span><span class="sxs-lookup"><span data-stu-id="754bf-118">Platform</span></span>| <span data-ttu-id="754bf-119">應用程式</span><span class="sxs-lookup"><span data-stu-id="754bf-119">Application</span></span> |
| --- | --- | --- |
| <span data-ttu-id="754bf-120">任何 My Apps 應用程式服務</span><span class="sxs-lookup"><span data-stu-id="754bf-120">Any My Apps app service</span></span>| <span data-ttu-id="754bf-121">Android 和 iOS</span><span class="sxs-lookup"><span data-stu-id="754bf-121">Android and iOS</span></span>| <span data-ttu-id="754bf-122">應用程式的 MFA 和位置原則。</span><span class="sxs-lookup"><span data-stu-id="754bf-122">MFA and location policy for apps.</span></span> <span data-ttu-id="754bf-123">不支援裝置型原則。</span><span class="sxs-lookup"><span data-stu-id="754bf-123">Device based policies are not supported.</span></span>|
| <span data-ttu-id="754bf-124">Azure 遠端應用程式服務</span><span class="sxs-lookup"><span data-stu-id="754bf-124">Azure Remote App service</span></span>| <span data-ttu-id="754bf-125">Windows 10、Windows 8.1、Windows 7、iOS、Android 和 Mac OS X</span><span class="sxs-lookup"><span data-stu-id="754bf-125">Windows 10, Windows 8.1, Windows 7, iOS, Android, and Mac OS X</span></span>| <span data-ttu-id="754bf-126">Azure 遠端應用程式</span><span class="sxs-lookup"><span data-stu-id="754bf-126">Azure Remote app</span></span>|
| <span data-ttu-id="754bf-127">Dynamics CRM</span><span class="sxs-lookup"><span data-stu-id="754bf-127">Dynamics CRM</span></span>| <span data-ttu-id="754bf-128">Windows 10、Windows 8.1、Windows 7、iOS 和 Android</span><span class="sxs-lookup"><span data-stu-id="754bf-128">Windows 10, Windows 8.1, Windows 7, iOS, and Android</span></span>| <span data-ttu-id="754bf-129">Dynamics CRM 應用程式</span><span class="sxs-lookup"><span data-stu-id="754bf-129">Dynamics CRM app</span></span>|
| <span data-ttu-id="754bf-130">Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="754bf-130">Microsoft Teams</span></span>| <span data-ttu-id="754bf-131">Windows 10、Windows 8.1、Windows 7、iOS/Android 和 MAC OSX</span><span class="sxs-lookup"><span data-stu-id="754bf-131">Windows 10, Windows 8.1, Windows 7, iOS/Android and MAC OSX</span></span>| <span data-ttu-id="754bf-132">Microsoft Teams Services - 這會控制支援 Microsoft Teams 及其所有用戶端應用程式的所有服務 - Windows 桌面、MAC OS X、iOS、Android、WP 和 Web 用戶端</span><span class="sxs-lookup"><span data-stu-id="754bf-132">Microsoft Teams Services - this controls all services that support Microsoft Teams and all its Client Apps - Windows Desktop, MAC OS X, iOS, Android, WP, and web client</span></span>|
| <span data-ttu-id="754bf-133">Office 365 Exchange Online</span><span class="sxs-lookup"><span data-stu-id="754bf-133">Office 365 Exchange Online</span></span>| <span data-ttu-id="754bf-134">Windows 10</span><span class="sxs-lookup"><span data-stu-id="754bf-134">Windows 10</span></span>| <span data-ttu-id="754bf-135">郵件/行事曆/連絡人應用程式、Outlook 2016、Outlook 2013 (已啟用新式驗證)、商務用 Skype (採用新式驗證)</span><span class="sxs-lookup"><span data-stu-id="754bf-135">Mail/Calendar/People app, Outlook 2016, Outlook 2013 (with modern authentication), Skype for Business (with modern authentication)</span></span>|
| <span data-ttu-id="754bf-136">Office 365 Exchange Online</span><span class="sxs-lookup"><span data-stu-id="754bf-136">Office 365 Exchange Online</span></span>| <span data-ttu-id="754bf-137">Windows 8.1、Windows 7</span><span class="sxs-lookup"><span data-stu-id="754bf-137">Windows 8.1, Windows 7</span></span>| <span data-ttu-id="754bf-138">Outlook 2016、Outlook 2013 (已啟用新式驗證)、商務用 Skype (採用新式驗證)</span><span class="sxs-lookup"><span data-stu-id="754bf-138">Outlook 2016, Outlook 2013 (with modern authentication), Skype for Business (with modern authentication)</span></span>|
| <span data-ttu-id="754bf-139">Office 365 Exchange Online</span><span class="sxs-lookup"><span data-stu-id="754bf-139">Office 365 Exchange Online</span></span>| <span data-ttu-id="754bf-140">iOS</span><span class="sxs-lookup"><span data-stu-id="754bf-140">iOS</span></span>| <span data-ttu-id="754bf-141">Outlook 行動應用程式</span><span class="sxs-lookup"><span data-stu-id="754bf-141">Outlook mobile app</span></span>|
| <span data-ttu-id="754bf-142">Office 365 Exchange Online</span><span class="sxs-lookup"><span data-stu-id="754bf-142">Office 365 Exchange Online</span></span>| <span data-ttu-id="754bf-143">Mac OS X</span><span class="sxs-lookup"><span data-stu-id="754bf-143">Mac OS X</span></span>| <span data-ttu-id="754bf-144">Outlook 2016 (macOS 版 Office)</span><span class="sxs-lookup"><span data-stu-id="754bf-144">Outlook 2016 (Office for macOS)</span></span>|
| <span data-ttu-id="754bf-145">Office 365 SharePoint Online</span><span class="sxs-lookup"><span data-stu-id="754bf-145">Office 365 SharePoint Online</span></span>| <span data-ttu-id="754bf-146">Windows 10</span><span class="sxs-lookup"><span data-stu-id="754bf-146">Windows 10</span></span>| <span data-ttu-id="754bf-147">Office 2016 應用程式、 通用 Office 應用程式 （使用新式驗證） 時，Office 2013 OneDrive 同步用戶端 (請參閱[備忘稿](https://support.office.com/en-US/article/Azure-Active-Directory-conditional-access-with-the-OneDrive-sync-client-on-Windows-028d73d7-4b86-4ee0-8fb7-9a209434b04e))，規劃未來的 hello Office 群組支援 SharePoint 應用程式的支援計劃未來 hello</span><span class="sxs-lookup"><span data-stu-id="754bf-147">Office 2016 apps, Universal Office apps, Office 2013 (with modern authentication), OneDrive sync client (see [notes](https://support.office.com/en-US/article/Azure-Active-Directory-conditional-access-with-the-OneDrive-sync-client-on-Windows-028d73d7-4b86-4ee0-8fb7-9a209434b04e)), Office Groups support planned for hello future, SharePoint app support planned for hello future</span></span>|
| <span data-ttu-id="754bf-148">Office 365 SharePoint Online</span><span class="sxs-lookup"><span data-stu-id="754bf-148">Office 365 SharePoint Online</span></span>| <span data-ttu-id="754bf-149">Windows 8.1、Windows 7</span><span class="sxs-lookup"><span data-stu-id="754bf-149">Windows 8.1, Windows 7</span></span>| <span data-ttu-id="754bf-150">Office 2016 應用程式、Office 2013 (具備新式驗證)、OneDrive 同步處理用戶端 (請參閱[附註](https://support.office.com/en-US/article/Azure-Active-Directory-conditional-access-with-the-OneDrive-sync-client-on-Windows-028d73d7-4b86-4ee0-8fb7-9a209434b04e))</span><span class="sxs-lookup"><span data-stu-id="754bf-150">Office 2016 apps, Office 2013 (with modern authentication), OneDrive sync client (see [notes](https://support.office.com/en-US/article/Azure-Active-Directory-conditional-access-with-the-OneDrive-sync-client-on-Windows-028d73d7-4b86-4ee0-8fb7-9a209434b04e))</span></span>|
| <span data-ttu-id="754bf-151">Office 365 SharePoint Online</span><span class="sxs-lookup"><span data-stu-id="754bf-151">Office 365 SharePoint Online</span></span>| <span data-ttu-id="754bf-152">iOS、Android</span><span class="sxs-lookup"><span data-stu-id="754bf-152">iOS, Android</span></span>| <span data-ttu-id="754bf-153">Office 行動應用程式</span><span class="sxs-lookup"><span data-stu-id="754bf-153">Office mobile apps</span></span>|
| <span data-ttu-id="754bf-154">Office 365 SharePoint Online</span><span class="sxs-lookup"><span data-stu-id="754bf-154">Office 365 SharePoint Online</span></span>| <span data-ttu-id="754bf-155">Mac OS X</span><span class="sxs-lookup"><span data-stu-id="754bf-155">Mac OS X</span></span>| <span data-ttu-id="754bf-156">macOS 版 Office 2016 (僅限 Word、Excel、PowerPoint、OneNote)。</span><span class="sxs-lookup"><span data-stu-id="754bf-156">Office 2016 for macOS (Word, Excel, PowerPoint, OneNote only).</span></span> <span data-ttu-id="754bf-157">支援商務用 OneDrive 規劃未來的 hello</span><span class="sxs-lookup"><span data-stu-id="754bf-157">OneDrive for Business support planned for hello future</span></span>|
| <span data-ttu-id="754bf-158">Office 365 Yammer</span><span class="sxs-lookup"><span data-stu-id="754bf-158">Office 365 Yammer</span></span>| <span data-ttu-id="754bf-159">Windows 10、iOS、Android</span><span class="sxs-lookup"><span data-stu-id="754bf-159">Windows 10, iOS, Android</span></span>| <span data-ttu-id="754bf-160">Office Yammer 應用程式</span><span class="sxs-lookup"><span data-stu-id="754bf-160">Office Yammer app</span></span>|
| <span data-ttu-id="754bf-161">PowerBI service</span><span class="sxs-lookup"><span data-stu-id="754bf-161">PowerBI service</span></span>| <span data-ttu-id="754bf-162">Windows 10、Windows 8.1、Windows 7 及 iOS</span><span class="sxs-lookup"><span data-stu-id="754bf-162">Windows 10, Windows 8.1, Windows 7, and iOS</span></span>| <span data-ttu-id="754bf-163">PowerBI 應用程式。</span><span class="sxs-lookup"><span data-stu-id="754bf-163">PowerBI app.</span></span> <span data-ttu-id="754bf-164">hello 適用於 Android 的 Power BI 應用程式目前不支援裝置型條件式存取。</span><span class="sxs-lookup"><span data-stu-id="754bf-164">hello Power BI app for Android does not currently support device-based conditional access.</span></span>|
| <span data-ttu-id="754bf-165">Visual Studio Team Services</span><span class="sxs-lookup"><span data-stu-id="754bf-165">Visual Studio Team Services</span></span>| <span data-ttu-id="754bf-166">Windows 10、Windows 8.1、Windows 7、iOS 和 Android</span><span class="sxs-lookup"><span data-stu-id="754bf-166">Windows 10, Windows 8.1, Windows 7, iOS, and Android</span></span>| <span data-ttu-id="754bf-167">Visual Studio Team Services 應用程式</span><span class="sxs-lookup"><span data-stu-id="754bf-167">Visual Studio Team Services app</span></span>|








## <a name="applications-that-do-not-use-modern-authentication"></a><span data-ttu-id="754bf-168">未使用新式驗證的應用程式</span><span class="sxs-lookup"><span data-stu-id="754bf-168">Applications that do not use modern authentication</span></span>
<span data-ttu-id="754bf-169">目前，您必須使用其他方法 tooblock 存取 tooapps 不使用新式驗證。</span><span class="sxs-lookup"><span data-stu-id="754bf-169">Currently, you must use other methods tooblock access tooapps that do not use modern authentication.</span></span> <span data-ttu-id="754bf-170">條件式存取不會強制執行未使用新式驗證之應用程式的存取規則。</span><span class="sxs-lookup"><span data-stu-id="754bf-170">Access rules for apps that don't use modern authentication are not enforced by conditional access.</span></span> <span data-ttu-id="754bf-171">這主要是 Exchange 和 SharePoint 存取的考量。</span><span class="sxs-lookup"><span data-stu-id="754bf-171">This primarily is a consideration for Exchange and SharePoint access.</span></span> <span data-ttu-id="754bf-172">大部分舊版應用程式使用較舊的存取控制通訊協定。</span><span class="sxs-lookup"><span data-stu-id="754bf-172">Most earlier versions of apps use older access control protocols.</span></span>

### <a name="control-access-in-office-365-sharepoint-online"></a><span data-ttu-id="754bf-173">Office 365 SharePoint Online 中的控制存取</span><span class="sxs-lookup"><span data-stu-id="754bf-173">Control access in Office 365 SharePoint Online</span></span>
<span data-ttu-id="754bf-174">您可以使用 hello 組 SPOTenant cmdlet 來停用 SharePoint 的存取權的舊版通訊協定。</span><span class="sxs-lookup"><span data-stu-id="754bf-174">You can disable legacy protocols for SharePoint access by using hello Set-SPOTenant cmdlet.</span></span> <span data-ttu-id="754bf-175">使用這個指令程式 tooprevent Office 用戶端的存取 SharePoint Online 資源的非新式驗證通訊協定。</span><span class="sxs-lookup"><span data-stu-id="754bf-175">Use this cmdlet tooprevent Office clients that use non-modern authentication protocols from accessing SharePoint Online resources.</span></span>

<span data-ttu-id="754bf-176">**範例命令**：`Set-SPOTenant -LegacyAuthProtocolsEnabled $false`</span><span class="sxs-lookup"><span data-stu-id="754bf-176">**Example command**: `Set-SPOTenant -LegacyAuthProtocolsEnabled $false`</span></span>

### <a name="control-access-in-office-365-exchange-online"></a><span data-ttu-id="754bf-177">Office 365 Exchange Online 中的控制存取</span><span class="sxs-lookup"><span data-stu-id="754bf-177">Control access in Office 365 Exchange Online</span></span>
<span data-ttu-id="754bf-178">Exchange 提供兩個主要的通訊協定類別。</span><span class="sxs-lookup"><span data-stu-id="754bf-178">Exchange offers two main categories of protocols.</span></span> <span data-ttu-id="754bf-179">檢閱 hello 下列選項，然後選取最適合貴組織的 hello 原則。</span><span class="sxs-lookup"><span data-stu-id="754bf-179">Review hello following options, and then select hello policy that is right for your organization.</span></span>

* <span data-ttu-id="754bf-180">**Exchange ActiveSync**。</span><span class="sxs-lookup"><span data-stu-id="754bf-180">**Exchange ActiveSync**.</span></span> <span data-ttu-id="754bf-181">根據預設，不會針對 Exchange ActiveSync 強制執行 Multi-Factor Authentication 和位置的條件式存取原則。</span><span class="sxs-lookup"><span data-stu-id="754bf-181">By default, conditional access policies for multi-factor authentication and location are not enforced for Exchange ActiveSync.</span></span> <span data-ttu-id="754bf-182">您可以設定 Exchange ActiveSync 原則直接管理，或是使用 Active Directory Federation Services (AD FS) 規則封鎖 Exchange ActiveSync 需要 tooprotect 存取 toothese 服務。</span><span class="sxs-lookup"><span data-stu-id="754bf-182">You need tooprotect access toothese services either by configuring Exchange ActiveSync policy directly, or by blocking Exchange ActiveSync by using Active Directory Federation Services (AD FS) rules.</span></span>
* <span data-ttu-id="754bf-183">**舊版通訊協定**。</span><span class="sxs-lookup"><span data-stu-id="754bf-183">**Legacy protocols**.</span></span> <span data-ttu-id="754bf-184">您可以使用 AD FS 來封鎖舊版通訊協定。</span><span class="sxs-lookup"><span data-stu-id="754bf-184">You can block legacy protocols with AD FS.</span></span> <span data-ttu-id="754bf-185">這會封鎖存取 tooolder Office 用戶端，例如 Office 2013 現代化驗證已啟用，而舊版 Office。</span><span class="sxs-lookup"><span data-stu-id="754bf-185">This blocks access tooolder Office clients, such as Office 2013 without modern authentication enabled, and earlier versions of Office.</span></span>

### <a name="use-ad-fs-tooblock-legacy-protocol"></a><span data-ttu-id="754bf-186">使用 AD FS tooblock 舊版通訊協定</span><span class="sxs-lookup"><span data-stu-id="754bf-186">Use AD FS tooblock legacy protocol</span></span>
<span data-ttu-id="754bf-187">您可以使用下列範例中發行授權規則 tooblock 舊版通訊協定層級的存取 hello AD FS 的 hello。</span><span class="sxs-lookup"><span data-stu-id="754bf-187">You can use hello following example issuance authorization rules tooblock legacy protocol access at hello AD FS level.</span></span> <span data-ttu-id="754bf-188">從兩個常見的組態中進行選擇。</span><span class="sxs-lookup"><span data-stu-id="754bf-188">Choose from two common configurations.</span></span>

#### <a name="option-1-allow-exchange-activesync-and-allow-legacy-apps-but-only-on-hello-intranet"></a><span data-ttu-id="754bf-189">選項 1： 讓 Exchange ActiveSync，並允許將舊版應用程式，但僅 hello 內部網路</span><span class="sxs-lookup"><span data-stu-id="754bf-189">Option 1: Allow Exchange ActiveSync, and allow legacy apps, but only on hello intranet</span></span>
<span data-ttu-id="754bf-190">AD FS 信賴憑證者信任的 Microsoft Office 365 識別平台，Exchange ActiveSync 流量套用下列三個規則 toohello hello 和瀏覽器和新式驗證的流量，可以存取。</span><span class="sxs-lookup"><span data-stu-id="754bf-190">By applying hello following three rules toohello AD FS relying party trust for Microsoft Office 365 Identity Platform, Exchange ActiveSync traffic, and browser and modern authentication traffic, have access.</span></span> <span data-ttu-id="754bf-191">將舊版應用程式會從外部網路的 hello 遭到封鎖。</span><span class="sxs-lookup"><span data-stu-id="754bf-191">Legacy apps are blocked from hello extranet.</span></span>

##### <a name="rule-1"></a><span data-ttu-id="754bf-192">規則 1</span><span class="sxs-lookup"><span data-stu-id="754bf-192">Rule 1</span></span>
    @RuleName = "Allow all intranet traffic"
    c1:[Type == "http://schemas.microsoft.com/ws/2012/01/insidecorporatenetwork", Value == "true"]
    => issue(Type = "http://schemas.microsoft.com/authorization/claims/permit", Value = "true");

##### <a name="rule-2"></a><span data-ttu-id="754bf-193">規則 2</span><span class="sxs-lookup"><span data-stu-id="754bf-193">Rule 2</span></span>
    @RuleName = "Allow Exchange ActiveSync"
    c1:[Type == "http://schemas.microsoft.com/2012/01/requestcontext/claims/x-ms-client-application", Value == "Microsoft.Exchange.ActiveSync"]
    => issue(Type = "http://schemas.microsoft.com/authorization/claims/permit", Value = "true");

##### <a name="rule-3"></a><span data-ttu-id="754bf-194">規則 3</span><span class="sxs-lookup"><span data-stu-id="754bf-194">Rule 3</span></span>
    @RuleName = "Allow extranet browser and browser dialog traffic"
    c1:[Type == "http://schemas.microsoft.com/ws/2012/01/insidecorporatenetwork", Value == "false"] &&
    c2:[Type == "http://schemas.microsoft.com/2012/01/requestcontext/claims/x-ms-endpoint-absolute-path", Value =~ "(/adfs/ls)|(/adfs/oauth2)"]
    => issue(Type = "http://schemas.microsoft.com/authorization/claims/permit", Value = "true");

#### <a name="option-2-allow-exchange-activesync-and-block-legacy-apps"></a><span data-ttu-id="754bf-195">選項 2︰允許 Exchange ActiveSync，並且封鎖舊版應用程式</span><span class="sxs-lookup"><span data-stu-id="754bf-195">Option 2: Allow Exchange ActiveSync, and block legacy apps</span></span>
<span data-ttu-id="754bf-196">AD FS 信賴憑證者信任的 Microsoft Office 365 識別平台，Exchange ActiveSync 流量套用下列三個規則 toohello hello 和瀏覽器和新式驗證的流量，可以存取。</span><span class="sxs-lookup"><span data-stu-id="754bf-196">By applying hello following three rules toohello AD FS relying party trust for Microsoft Office 365 Identity Platform, Exchange ActiveSync traffic, and browser and modern authentication traffic, have access.</span></span> <span data-ttu-id="754bf-197">來自任何位置的舊版應用程式會遭到封鎖。</span><span class="sxs-lookup"><span data-stu-id="754bf-197">Legacy apps are blocked from any location.</span></span>

##### <a name="rule-1"></a><span data-ttu-id="754bf-198">規則 1</span><span class="sxs-lookup"><span data-stu-id="754bf-198">Rule 1</span></span>
    @RuleName = "Allow all intranet traffic only for browser and modern authentication clients"
    c1:[Type == "http://schemas.microsoft.com/ws/2012/01/insidecorporatenetwork", Value == "true"] &&
    c2:[Type == "http://schemas.microsoft.com/2012/01/requestcontext/claims/x-ms-endpoint-absolute-path", Value =~ "(/adfs/ls)|(/adfs/oauth2)"]
    => issue(Type = "http://schemas.microsoft.com/authorization/claims/permit", Value = "true");


##### <a name="rule-2"></a><span data-ttu-id="754bf-199">規則 2</span><span class="sxs-lookup"><span data-stu-id="754bf-199">Rule 2</span></span>
    @RuleName = "Allow Exchange ActiveSync"
    c1:[Type == "http://schemas.microsoft.com/2012/01/requestcontext/claims/x-ms-client-application", Value == "Microsoft.Exchange.ActiveSync"]
    => issue(Type = "http://schemas.microsoft.com/authorization/claims/permit", Value = "true");


##### <a name="rule-3"></a><span data-ttu-id="754bf-200">規則 3</span><span class="sxs-lookup"><span data-stu-id="754bf-200">Rule 3</span></span>
    @RuleName = "Allow extranet browser and browser dialog traffic"
    c1:[Type == "http://schemas.microsoft.com/ws/2012/01/insidecorporatenetwork", Value == "false"] &&
    c2:[Type == "http://schemas.microsoft.com/2012/01/requestcontext/claims/x-ms-endpoint-absolute-path", Value =~ "(/adfs/ls)|(/adfs/oauth2)"]
    => issue(Type = "http://schemas.microsoft.com/authorization/claims/permit", Value = "true");


## <a name="supported-browsers-for-device-based-policies"></a><span data-ttu-id="754bf-201">裝置型原則的支援瀏覽器</span><span class="sxs-lookup"><span data-stu-id="754bf-201">Supported browsers for device based policies</span></span> 

<span data-ttu-id="754bf-202">您只能取得存取檢查的裝置原則的裝置相容性和網域加入 Azure AD 可以識別並驗證 hello 裝置時。</span><span class="sxs-lookup"><span data-stu-id="754bf-202">You can only get access for device based policies that check for device compliance and domain join when Azure AD can identify and authenticate hello device.</span></span> <span data-ttu-id="754bf-203">大部分的檢查，例如位置和 MFA 工作上大部分的裝置和瀏覽器，同時裝置原則需要 hello OS 版本與下面所列的瀏覽器。</span><span class="sxs-lookup"><span data-stu-id="754bf-203">While most checks, like location and MFA work on most devices and browsers, device policies require of hello OS version and browsers listed below.</span></span> <span data-ttu-id="754bf-204">當裝置原則已備妥，則會封鎖不受支援的瀏覽器或 hello 作業系統上的使用者存取。</span><span class="sxs-lookup"><span data-stu-id="754bf-204">Access is blocked for users on  unsupported browsers or hello operating systems when a device policy is in place.</span></span> 

| <span data-ttu-id="754bf-205">作業系統</span><span class="sxs-lookup"><span data-stu-id="754bf-205">OS</span></span>                     | <span data-ttu-id="754bf-206">瀏覽器</span><span class="sxs-lookup"><span data-stu-id="754bf-206">Browsers</span></span>                 | <span data-ttu-id="754bf-207">支援</span><span class="sxs-lookup"><span data-stu-id="754bf-207">Support</span></span>     |
| :--                    | :--                      | :-:         |
| <span data-ttu-id="754bf-208">Win 10</span><span class="sxs-lookup"><span data-stu-id="754bf-208">Win 10</span></span>                 | <span data-ttu-id="754bf-209">IE、Edge</span><span class="sxs-lookup"><span data-stu-id="754bf-209">IE, Edge</span></span>                 | ![勾選][1] |
| <span data-ttu-id="754bf-211">Win 10</span><span class="sxs-lookup"><span data-stu-id="754bf-211">Win 10</span></span>                 | <span data-ttu-id="754bf-212">Chrome</span><span class="sxs-lookup"><span data-stu-id="754bf-212">Chrome</span></span>                   | <span data-ttu-id="754bf-213">預覽</span><span class="sxs-lookup"><span data-stu-id="754bf-213">Preview</span></span>     |
| <span data-ttu-id="754bf-214">Win 8 / 8.1</span><span class="sxs-lookup"><span data-stu-id="754bf-214">Win 8 / 8.1</span></span>            | <span data-ttu-id="754bf-215">IE、Chrome</span><span class="sxs-lookup"><span data-stu-id="754bf-215">IE, Chrome</span></span>               | ![勾選][1] |
| <span data-ttu-id="754bf-217">Win 7</span><span class="sxs-lookup"><span data-stu-id="754bf-217">Win 7</span></span>                  | <span data-ttu-id="754bf-218">IE、Chrome</span><span class="sxs-lookup"><span data-stu-id="754bf-218">IE, Chrome</span></span>               | ![勾選][1] |
| <span data-ttu-id="754bf-220">iOS</span><span class="sxs-lookup"><span data-stu-id="754bf-220">iOS</span></span>                    | <span data-ttu-id="754bf-221">Safari</span><span class="sxs-lookup"><span data-stu-id="754bf-221">Safari</span></span>                   | ![勾選][1] |
| <span data-ttu-id="754bf-223">Android</span><span class="sxs-lookup"><span data-stu-id="754bf-223">Android</span></span>                | <span data-ttu-id="754bf-224">Chrome</span><span class="sxs-lookup"><span data-stu-id="754bf-224">Chrome</span></span>                   | ![勾選][1] |
| <span data-ttu-id="754bf-226">Windows Phone</span><span class="sxs-lookup"><span data-stu-id="754bf-226">Windows Phone</span></span>          | <span data-ttu-id="754bf-227">IE、Edge</span><span class="sxs-lookup"><span data-stu-id="754bf-227">IE, Edge</span></span>                 | ![勾選][1] |
| <span data-ttu-id="754bf-229">Windows Server 2016</span><span class="sxs-lookup"><span data-stu-id="754bf-229">Windows Server 2016</span></span>    | <span data-ttu-id="754bf-230">IE、Edge</span><span class="sxs-lookup"><span data-stu-id="754bf-230">IE, Edge</span></span>                 | ![勾選][1] |
| <span data-ttu-id="754bf-232">Windows Server 2016</span><span class="sxs-lookup"><span data-stu-id="754bf-232">Windows Server 2016</span></span>    | <span data-ttu-id="754bf-233">Chrome</span><span class="sxs-lookup"><span data-stu-id="754bf-233">Chrome</span></span>                   | <span data-ttu-id="754bf-234">敬請期待</span><span class="sxs-lookup"><span data-stu-id="754bf-234">Coming soon</span></span> |
| <span data-ttu-id="754bf-235">Windows Server 2012 R2</span><span class="sxs-lookup"><span data-stu-id="754bf-235">Windows Server 2012 R2</span></span> | <span data-ttu-id="754bf-236">IE、Chrome</span><span class="sxs-lookup"><span data-stu-id="754bf-236">IE, Chrome</span></span>               | ![勾選][1] |
| <span data-ttu-id="754bf-238">Windows Server 2008 R2</span><span class="sxs-lookup"><span data-stu-id="754bf-238">Windows Server 2008 R2</span></span> | <span data-ttu-id="754bf-239">IE、Chrome</span><span class="sxs-lookup"><span data-stu-id="754bf-239">IE, Chrome</span></span>               | ![勾選][1] |
| <span data-ttu-id="754bf-241">Mac OS</span><span class="sxs-lookup"><span data-stu-id="754bf-241">Mac OS</span></span>                 | <span data-ttu-id="754bf-242">Safari</span><span class="sxs-lookup"><span data-stu-id="754bf-242">Safari</span></span>                   | ![勾選][1] |
| <span data-ttu-id="754bf-244">Mac OS</span><span class="sxs-lookup"><span data-stu-id="754bf-244">Mac OS</span></span>                 | <span data-ttu-id="754bf-245">Chrome</span><span class="sxs-lookup"><span data-stu-id="754bf-245">Chrome</span></span>                   | <span data-ttu-id="754bf-246">敬請期待</span><span class="sxs-lookup"><span data-stu-id="754bf-246">Coming soon</span></span> |

> [!NOTE]
> <span data-ttu-id="754bf-247">如需 Chrome 支援，您必須使用 Windows 10 建立者更新並安裝到 hello 延伸模組[這裡](https://chrome.google.com/webstore/detail/windows-10-accounts/ppnbnpeolgkicgegkbkbjmhlideopiji)。</span><span class="sxs-lookup"><span data-stu-id="754bf-247">For Chrome support, you must be using Windows 10 Creators Update and install hello extension found [here](https://chrome.google.com/webstore/detail/windows-10-accounts/ppnbnpeolgkicgegkbkbjmhlideopiji).</span></span>
>
>

## <a name="next-steps"></a><span data-ttu-id="754bf-248">後續步驟</span><span class="sxs-lookup"><span data-stu-id="754bf-248">Next steps</span></span>

<span data-ttu-id="754bf-249">如需詳細資訊，請參閱 [Azure Active Directory 中的條件式存取](active-directory-conditional-access.md)</span><span class="sxs-lookup"><span data-stu-id="754bf-249">For more details, see [Conditional access in Azure Active Directory](active-directory-conditional-access.md)</span></span>




<!--Image references-->
[1]: ./media/active-directory-conditional-access-supported-apps/ic195031.png


