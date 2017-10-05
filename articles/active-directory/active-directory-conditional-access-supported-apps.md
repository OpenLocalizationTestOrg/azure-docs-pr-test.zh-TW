---
title: "在 Azure Active Directory 中使用條件式存取規則的應用程式和瀏覽器 | Microsoft Docs"
description: "透過條件式存取控制，Azure Active Directory 會在驗證使用者以及允許存取應用程式時，檢查特定的條件。"
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
ms.openlocfilehash: 8614660f7c98af7b4e6d50348775495c67ae1cc8
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="applications-and-browsers-that-use-conditional-access-rules-in-azure-active-directory"></a><span data-ttu-id="d4ce1-103">在 Azure Active Directory 中使用條件式存取規則的應用程式和瀏覽器</span><span class="sxs-lookup"><span data-stu-id="d4ce1-103">Applications and browsers that use conditional access rules in Azure Active Directory</span></span>

<span data-ttu-id="d4ce1-104">Azure Active Directory (Azure AD) 連線應用程式、預先整合的同盟軟體即服務 (SaaS) 應用程式、使用密碼單一登入 (SSO) 的應用程式、商務營運應用程式以及使用 Azure AD 應用程式 Proxy 的應用程式，都支援條件式存取規則。</span><span class="sxs-lookup"><span data-stu-id="d4ce1-104">Conditional access rules are supported in Azure Active Directory (Azure AD)-connected applications, pre-integrated federated software as a service (SaaS) applications, applications that use password single sign-on (SSO), line-of-business applications, and applications that use Azure AD Application Proxy.</span></span> <span data-ttu-id="d4ce1-105">如需可使用條件式存取的應用程式詳細清單，請參閱[已啟用條件式存取功能的服務](active-directory-conditional-access-technical-reference.md)。</span><span class="sxs-lookup"><span data-stu-id="d4ce1-105">For a detailed list of applications for which you can use conditional access, see [Services enabled with conditional access](active-directory-conditional-access-technical-reference.md).</span></span> <span data-ttu-id="d4ce1-106">條件式存取可以與運用新式驗證的行動和傳統型應用程式搭配使用。</span><span class="sxs-lookup"><span data-stu-id="d4ce1-106">Conditional access works both with mobile and desktop applications that use modern authentication.</span></span> <span data-ttu-id="d4ce1-107">在本文中，我們將討論條件式存取功能在行動和桌面應用程式中的運作方式。</span><span class="sxs-lookup"><span data-stu-id="d4ce1-107">In this article, we cover how conditional access works in mobile and desktop apps.</span></span>

<span data-ttu-id="d4ce1-108">您可以在使用新式驗證的應用程式中使用 Azure AD 登入頁面。</span><span class="sxs-lookup"><span data-stu-id="d4ce1-108">You can use Azure AD sign-in pages in applications that use modern authentication.</span></span> <span data-ttu-id="d4ce1-109">在登入頁面中，系統會提示您進行 Multi-Factor Authentication。</span><span class="sxs-lookup"><span data-stu-id="d4ce1-109">With a sign-in page, a user is prompted for multi-factor authentication.</span></span> <span data-ttu-id="d4ce1-110">如果使用者的存取遭到封鎖，則會顯示訊息。</span><span class="sxs-lookup"><span data-stu-id="d4ce1-110">A message is shown if the user's access is blocked.</span></span> <span data-ttu-id="d4ce1-111">需要新式驗證，裝置才能夠向 Azure AD 進行驗證，以便評估裝置型條件式存取原則。</span><span class="sxs-lookup"><span data-stu-id="d4ce1-111">Modern authentication is required for the device to authenticate with Azure AD, so that device-based conditional access policies are evaluated.</span></span>

<span data-ttu-id="d4ce1-112">請務必知道哪些應用程式可以使用條件式存取規則，以及您可能需要採取哪些步驟來保護其他應用程式進入點。</span><span class="sxs-lookup"><span data-stu-id="d4ce1-112">It's important to know which applications can use conditional access rules, and the steps that you might need to take to secure other application entry points.</span></span>

## <a name="applications-that-use-modern-authentication"></a><span data-ttu-id="d4ce1-113">使用新式驗證的應用程式</span><span class="sxs-lookup"><span data-stu-id="d4ce1-113">Applications that use modern authentication</span></span>
> [!NOTE]
> <span data-ttu-id="d4ce1-114">如果 Azure AD 中的條件式存取原則等同於 Office 365 中的條件式存取原則，請設定這兩個條件式存取原則。</span><span class="sxs-lookup"><span data-stu-id="d4ce1-114">If you have a conditional access policy in Azure AD that has an equivalent in Office 365, configure both conditional access policies.</span></span> <span data-ttu-id="d4ce1-115">這適用於 Exchange Online 或 SharePoint Online 等的條件式存取原則。</span><span class="sxs-lookup"><span data-stu-id="d4ce1-115">This would apply, for example, to conditional access policies for Exchange Online or SharePoint Online.</span></span>
>
>

<span data-ttu-id="d4ce1-116">下列應用程式支援 Office 365 和其他 Azure AD 連線服務應用程式的條件式存取︰</span><span class="sxs-lookup"><span data-stu-id="d4ce1-116">The following applications support conditional access for Office 365 and other Azure AD-connected service applications:</span></span>


| <span data-ttu-id="d4ce1-117">目標服務</span><span class="sxs-lookup"><span data-stu-id="d4ce1-117">Target Service</span></span>| <span data-ttu-id="d4ce1-118">平台</span><span class="sxs-lookup"><span data-stu-id="d4ce1-118">Platform</span></span>| <span data-ttu-id="d4ce1-119">應用程式</span><span class="sxs-lookup"><span data-stu-id="d4ce1-119">Application</span></span> |
| --- | --- | --- |
| <span data-ttu-id="d4ce1-120">任何 My Apps 應用程式服務</span><span class="sxs-lookup"><span data-stu-id="d4ce1-120">Any My Apps app service</span></span>| <span data-ttu-id="d4ce1-121">Android 和 iOS</span><span class="sxs-lookup"><span data-stu-id="d4ce1-121">Android and iOS</span></span>| <span data-ttu-id="d4ce1-122">應用程式的 MFA 和位置原則。</span><span class="sxs-lookup"><span data-stu-id="d4ce1-122">MFA and location policy for apps.</span></span> <span data-ttu-id="d4ce1-123">不支援裝置型原則。</span><span class="sxs-lookup"><span data-stu-id="d4ce1-123">Device based policies are not supported.</span></span>|
| <span data-ttu-id="d4ce1-124">Azure 遠端應用程式服務</span><span class="sxs-lookup"><span data-stu-id="d4ce1-124">Azure Remote App service</span></span>| <span data-ttu-id="d4ce1-125">Windows 10、Windows 8.1、Windows 7、iOS、Android 和 Mac OS X</span><span class="sxs-lookup"><span data-stu-id="d4ce1-125">Windows 10, Windows 8.1, Windows 7, iOS, Android, and Mac OS X</span></span>| <span data-ttu-id="d4ce1-126">Azure 遠端應用程式</span><span class="sxs-lookup"><span data-stu-id="d4ce1-126">Azure Remote app</span></span>|
| <span data-ttu-id="d4ce1-127">Dynamics CRM</span><span class="sxs-lookup"><span data-stu-id="d4ce1-127">Dynamics CRM</span></span>| <span data-ttu-id="d4ce1-128">Windows 10、Windows 8.1、Windows 7、iOS 和 Android</span><span class="sxs-lookup"><span data-stu-id="d4ce1-128">Windows 10, Windows 8.1, Windows 7, iOS, and Android</span></span>| <span data-ttu-id="d4ce1-129">Dynamics CRM 應用程式</span><span class="sxs-lookup"><span data-stu-id="d4ce1-129">Dynamics CRM app</span></span>|
| <span data-ttu-id="d4ce1-130">Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="d4ce1-130">Microsoft Teams</span></span>| <span data-ttu-id="d4ce1-131">Windows 10、Windows 8.1、Windows 7、iOS/Android 和 MAC OSX</span><span class="sxs-lookup"><span data-stu-id="d4ce1-131">Windows 10, Windows 8.1, Windows 7, iOS/Android and MAC OSX</span></span>| <span data-ttu-id="d4ce1-132">Microsoft Teams Services - 這會控制支援 Microsoft Teams 及其所有用戶端應用程式的所有服務 - Windows 桌面、MAC OS X、iOS、Android、WP 和 Web 用戶端</span><span class="sxs-lookup"><span data-stu-id="d4ce1-132">Microsoft Teams Services - this controls all services that support Microsoft Teams and all its Client Apps - Windows Desktop, MAC OS X, iOS, Android, WP, and web client</span></span>|
| <span data-ttu-id="d4ce1-133">Office 365 Exchange Online</span><span class="sxs-lookup"><span data-stu-id="d4ce1-133">Office 365 Exchange Online</span></span>| <span data-ttu-id="d4ce1-134">Windows 10</span><span class="sxs-lookup"><span data-stu-id="d4ce1-134">Windows 10</span></span>| <span data-ttu-id="d4ce1-135">郵件/行事曆/連絡人應用程式、Outlook 2016、Outlook 2013 (已啟用新式驗證)、商務用 Skype (採用新式驗證)</span><span class="sxs-lookup"><span data-stu-id="d4ce1-135">Mail/Calendar/People app, Outlook 2016, Outlook 2013 (with modern authentication), Skype for Business (with modern authentication)</span></span>|
| <span data-ttu-id="d4ce1-136">Office 365 Exchange Online</span><span class="sxs-lookup"><span data-stu-id="d4ce1-136">Office 365 Exchange Online</span></span>| <span data-ttu-id="d4ce1-137">Windows 8.1、Windows 7</span><span class="sxs-lookup"><span data-stu-id="d4ce1-137">Windows 8.1, Windows 7</span></span>| <span data-ttu-id="d4ce1-138">Outlook 2016、Outlook 2013 (已啟用新式驗證)、商務用 Skype (採用新式驗證)</span><span class="sxs-lookup"><span data-stu-id="d4ce1-138">Outlook 2016, Outlook 2013 (with modern authentication), Skype for Business (with modern authentication)</span></span>|
| <span data-ttu-id="d4ce1-139">Office 365 Exchange Online</span><span class="sxs-lookup"><span data-stu-id="d4ce1-139">Office 365 Exchange Online</span></span>| <span data-ttu-id="d4ce1-140">iOS</span><span class="sxs-lookup"><span data-stu-id="d4ce1-140">iOS</span></span>| <span data-ttu-id="d4ce1-141">Outlook 行動應用程式</span><span class="sxs-lookup"><span data-stu-id="d4ce1-141">Outlook mobile app</span></span>|
| <span data-ttu-id="d4ce1-142">Office 365 Exchange Online</span><span class="sxs-lookup"><span data-stu-id="d4ce1-142">Office 365 Exchange Online</span></span>| <span data-ttu-id="d4ce1-143">Mac OS X</span><span class="sxs-lookup"><span data-stu-id="d4ce1-143">Mac OS X</span></span>| <span data-ttu-id="d4ce1-144">Outlook 2016 (macOS 版 Office)</span><span class="sxs-lookup"><span data-stu-id="d4ce1-144">Outlook 2016 (Office for macOS)</span></span>|
| <span data-ttu-id="d4ce1-145">Office 365 SharePoint Online</span><span class="sxs-lookup"><span data-stu-id="d4ce1-145">Office 365 SharePoint Online</span></span>| <span data-ttu-id="d4ce1-146">Windows 10</span><span class="sxs-lookup"><span data-stu-id="d4ce1-146">Windows 10</span></span>| <span data-ttu-id="d4ce1-147">Office 2016 應用程式、通用 Office 應用程式、Office 2013 (具備新式驗證)、OneDrive 同步處理用戶端 (請參閱[附註](https://support.office.com/en-US/article/Azure-Active-Directory-conditional-access-with-the-OneDrive-sync-client-on-Windows-028d73d7-4b86-4ee0-8fb7-9a209434b04e))、預計未來提供的 Office Groups 支援、預計未來提供的 SharePoint 應用程式支援</span><span class="sxs-lookup"><span data-stu-id="d4ce1-147">Office 2016 apps, Universal Office apps, Office 2013 (with modern authentication), OneDrive sync client (see [notes](https://support.office.com/en-US/article/Azure-Active-Directory-conditional-access-with-the-OneDrive-sync-client-on-Windows-028d73d7-4b86-4ee0-8fb7-9a209434b04e)), Office Groups support planned for the future, SharePoint app support planned for the future</span></span>|
| <span data-ttu-id="d4ce1-148">Office 365 SharePoint Online</span><span class="sxs-lookup"><span data-stu-id="d4ce1-148">Office 365 SharePoint Online</span></span>| <span data-ttu-id="d4ce1-149">Windows 8.1、Windows 7</span><span class="sxs-lookup"><span data-stu-id="d4ce1-149">Windows 8.1, Windows 7</span></span>| <span data-ttu-id="d4ce1-150">Office 2016 應用程式、Office 2013 (具備新式驗證)、OneDrive 同步處理用戶端 (請參閱[附註](https://support.office.com/en-US/article/Azure-Active-Directory-conditional-access-with-the-OneDrive-sync-client-on-Windows-028d73d7-4b86-4ee0-8fb7-9a209434b04e))</span><span class="sxs-lookup"><span data-stu-id="d4ce1-150">Office 2016 apps, Office 2013 (with modern authentication), OneDrive sync client (see [notes](https://support.office.com/en-US/article/Azure-Active-Directory-conditional-access-with-the-OneDrive-sync-client-on-Windows-028d73d7-4b86-4ee0-8fb7-9a209434b04e))</span></span>|
| <span data-ttu-id="d4ce1-151">Office 365 SharePoint Online</span><span class="sxs-lookup"><span data-stu-id="d4ce1-151">Office 365 SharePoint Online</span></span>| <span data-ttu-id="d4ce1-152">iOS、Android</span><span class="sxs-lookup"><span data-stu-id="d4ce1-152">iOS, Android</span></span>| <span data-ttu-id="d4ce1-153">Office 行動應用程式</span><span class="sxs-lookup"><span data-stu-id="d4ce1-153">Office mobile apps</span></span>|
| <span data-ttu-id="d4ce1-154">Office 365 SharePoint Online</span><span class="sxs-lookup"><span data-stu-id="d4ce1-154">Office 365 SharePoint Online</span></span>| <span data-ttu-id="d4ce1-155">Mac OS X</span><span class="sxs-lookup"><span data-stu-id="d4ce1-155">Mac OS X</span></span>| <span data-ttu-id="d4ce1-156">macOS 版 Office 2016 (僅限 Word、Excel、PowerPoint、OneNote)。</span><span class="sxs-lookup"><span data-stu-id="d4ce1-156">Office 2016 for macOS (Word, Excel, PowerPoint, OneNote only).</span></span> <span data-ttu-id="d4ce1-157">未來規劃支援商務用 OneDrive</span><span class="sxs-lookup"><span data-stu-id="d4ce1-157">OneDrive for Business support planned for the future</span></span>|
| <span data-ttu-id="d4ce1-158">Office 365 Yammer</span><span class="sxs-lookup"><span data-stu-id="d4ce1-158">Office 365 Yammer</span></span>| <span data-ttu-id="d4ce1-159">Windows 10、iOS、Android</span><span class="sxs-lookup"><span data-stu-id="d4ce1-159">Windows 10, iOS, Android</span></span>| <span data-ttu-id="d4ce1-160">Office Yammer 應用程式</span><span class="sxs-lookup"><span data-stu-id="d4ce1-160">Office Yammer app</span></span>|
| <span data-ttu-id="d4ce1-161">PowerBI service</span><span class="sxs-lookup"><span data-stu-id="d4ce1-161">PowerBI service</span></span>| <span data-ttu-id="d4ce1-162">Windows 10、Windows 8.1、Windows 7 及 iOS</span><span class="sxs-lookup"><span data-stu-id="d4ce1-162">Windows 10, Windows 8.1, Windows 7, and iOS</span></span>| <span data-ttu-id="d4ce1-163">PowerBI 應用程式。</span><span class="sxs-lookup"><span data-stu-id="d4ce1-163">PowerBI app.</span></span> <span data-ttu-id="d4ce1-164">適用於 Android 的 Power BI 應用程式目前不支援裝置型條件式存取。</span><span class="sxs-lookup"><span data-stu-id="d4ce1-164">The Power BI app for Android does not currently support device-based conditional access.</span></span>|
| <span data-ttu-id="d4ce1-165">Visual Studio Team Services</span><span class="sxs-lookup"><span data-stu-id="d4ce1-165">Visual Studio Team Services</span></span>| <span data-ttu-id="d4ce1-166">Windows 10、Windows 8.1、Windows 7、iOS 和 Android</span><span class="sxs-lookup"><span data-stu-id="d4ce1-166">Windows 10, Windows 8.1, Windows 7, iOS, and Android</span></span>| <span data-ttu-id="d4ce1-167">Visual Studio Team Services 應用程式</span><span class="sxs-lookup"><span data-stu-id="d4ce1-167">Visual Studio Team Services app</span></span>|








## <a name="applications-that-do-not-use-modern-authentication"></a><span data-ttu-id="d4ce1-168">未使用新式驗證的應用程式</span><span class="sxs-lookup"><span data-stu-id="d4ce1-168">Applications that do not use modern authentication</span></span>
<span data-ttu-id="d4ce1-169">目前，您必須使用其他方法來阻止存取未使用新式驗證的應用程式。</span><span class="sxs-lookup"><span data-stu-id="d4ce1-169">Currently, you must use other methods to block access to apps that do not use modern authentication.</span></span> <span data-ttu-id="d4ce1-170">條件式存取不會強制執行未使用新式驗證之應用程式的存取規則。</span><span class="sxs-lookup"><span data-stu-id="d4ce1-170">Access rules for apps that don't use modern authentication are not enforced by conditional access.</span></span> <span data-ttu-id="d4ce1-171">這主要是 Exchange 和 SharePoint 存取的考量。</span><span class="sxs-lookup"><span data-stu-id="d4ce1-171">This primarily is a consideration for Exchange and SharePoint access.</span></span> <span data-ttu-id="d4ce1-172">大部分舊版應用程式使用較舊的存取控制通訊協定。</span><span class="sxs-lookup"><span data-stu-id="d4ce1-172">Most earlier versions of apps use older access control protocols.</span></span>

### <a name="control-access-in-office-365-sharepoint-online"></a><span data-ttu-id="d4ce1-173">Office 365 SharePoint Online 中的控制存取</span><span class="sxs-lookup"><span data-stu-id="d4ce1-173">Control access in Office 365 SharePoint Online</span></span>
<span data-ttu-id="d4ce1-174">您可以使用 Set-SPOTenant Cmdlet，停用 SharePoint 存取的舊版通訊協定。</span><span class="sxs-lookup"><span data-stu-id="d4ce1-174">You can disable legacy protocols for SharePoint access by using the Set-SPOTenant cmdlet.</span></span> <span data-ttu-id="d4ce1-175">利用這個 Cmdlet，阻止未使用新式驗證通訊協定的 Office 用戶端存取 SharePoint Online 資源。</span><span class="sxs-lookup"><span data-stu-id="d4ce1-175">Use this cmdlet to prevent Office clients that use non-modern authentication protocols from accessing SharePoint Online resources.</span></span>

<span data-ttu-id="d4ce1-176">**範例命令**：`Set-SPOTenant -LegacyAuthProtocolsEnabled $false`</span><span class="sxs-lookup"><span data-stu-id="d4ce1-176">**Example command**: `Set-SPOTenant -LegacyAuthProtocolsEnabled $false`</span></span>

### <a name="control-access-in-office-365-exchange-online"></a><span data-ttu-id="d4ce1-177">Office 365 Exchange Online 中的控制存取</span><span class="sxs-lookup"><span data-stu-id="d4ce1-177">Control access in Office 365 Exchange Online</span></span>
<span data-ttu-id="d4ce1-178">Exchange 提供兩個主要的通訊協定類別。</span><span class="sxs-lookup"><span data-stu-id="d4ce1-178">Exchange offers two main categories of protocols.</span></span> <span data-ttu-id="d4ce1-179">檢閱下列選項，然後選取最適合貴組織的原則。</span><span class="sxs-lookup"><span data-stu-id="d4ce1-179">Review the following options, and then select the policy that is right for your organization.</span></span>

* <span data-ttu-id="d4ce1-180">**Exchange ActiveSync**。</span><span class="sxs-lookup"><span data-stu-id="d4ce1-180">**Exchange ActiveSync**.</span></span> <span data-ttu-id="d4ce1-181">根據預設，不會針對 Exchange ActiveSync 強制執行 Multi-Factor Authentication 和位置的條件式存取原則。</span><span class="sxs-lookup"><span data-stu-id="d4ce1-181">By default, conditional access policies for multi-factor authentication and location are not enforced for Exchange ActiveSync.</span></span> <span data-ttu-id="d4ce1-182">您需要直接設定 Exchange ActiveSync 原則或使用 Active Directory Federation Services (AD FS) 規則封鎖 Exchange ActiveSync，藉此保護這些服務的存取。</span><span class="sxs-lookup"><span data-stu-id="d4ce1-182">You need to protect access to these services either by configuring Exchange ActiveSync policy directly, or by blocking Exchange ActiveSync by using Active Directory Federation Services (AD FS) rules.</span></span>
* <span data-ttu-id="d4ce1-183">**舊版通訊協定**。</span><span class="sxs-lookup"><span data-stu-id="d4ce1-183">**Legacy protocols**.</span></span> <span data-ttu-id="d4ce1-184">您可以使用 AD FS 來封鎖舊版通訊協定。</span><span class="sxs-lookup"><span data-stu-id="d4ce1-184">You can block legacy protocols with AD FS.</span></span> <span data-ttu-id="d4ce1-185">這會封鎖對於舊版 Office 用戶端的存取，例如，未啟用新式驗證的 Office 2013 及更早的 Office 版本。</span><span class="sxs-lookup"><span data-stu-id="d4ce1-185">This blocks access to older Office clients, such as Office 2013 without modern authentication enabled, and earlier versions of Office.</span></span>

### <a name="use-ad-fs-to-block-legacy-protocol"></a><span data-ttu-id="d4ce1-186">使用 AD FS 來封鎖舊版通訊協定</span><span class="sxs-lookup"><span data-stu-id="d4ce1-186">Use AD FS to block legacy protocol</span></span>
<span data-ttu-id="d4ce1-187">您可以使用下列範例發行授權規則，在 AD FS 層級封鎖舊版通訊協定存取。</span><span class="sxs-lookup"><span data-stu-id="d4ce1-187">You can use the following example issuance authorization rules to block legacy protocol access at the AD FS level.</span></span> <span data-ttu-id="d4ce1-188">從兩個常見的組態中進行選擇。</span><span class="sxs-lookup"><span data-stu-id="d4ce1-188">Choose from two common configurations.</span></span>

#### <a name="option-1-allow-exchange-activesync-and-allow-legacy-apps-but-only-on-the-intranet"></a><span data-ttu-id="d4ce1-189">選項 1︰允許 Exchange ActiveSync，並且允許舊版應用程式 (但僅限內部網路)</span><span class="sxs-lookup"><span data-stu-id="d4ce1-189">Option 1: Allow Exchange ActiveSync, and allow legacy apps, but only on the intranet</span></span>
<span data-ttu-id="d4ce1-190">將下列三個規則套用到適用於 Microsoft Office 365 身分識別平台的 AD FS 信賴憑證者信任，Exchange ActiveSync 流量以及瀏覽器和新式驗證流量就會有存取權。</span><span class="sxs-lookup"><span data-stu-id="d4ce1-190">By applying the following three rules to the AD FS relying party trust for Microsoft Office 365 Identity Platform, Exchange ActiveSync traffic, and browser and modern authentication traffic, have access.</span></span> <span data-ttu-id="d4ce1-191">來自外部網路的舊版應用程式會遭到封鎖。</span><span class="sxs-lookup"><span data-stu-id="d4ce1-191">Legacy apps are blocked from the extranet.</span></span>

##### <a name="rule-1"></a><span data-ttu-id="d4ce1-192">規則 1</span><span class="sxs-lookup"><span data-stu-id="d4ce1-192">Rule 1</span></span>
    @RuleName = "Allow all intranet traffic"
    c1:[Type == "http://schemas.microsoft.com/ws/2012/01/insidecorporatenetwork", Value == "true"]
    => issue(Type = "http://schemas.microsoft.com/authorization/claims/permit", Value = "true");

##### <a name="rule-2"></a><span data-ttu-id="d4ce1-193">規則 2</span><span class="sxs-lookup"><span data-stu-id="d4ce1-193">Rule 2</span></span>
    @RuleName = "Allow Exchange ActiveSync"
    c1:[Type == "http://schemas.microsoft.com/2012/01/requestcontext/claims/x-ms-client-application", Value == "Microsoft.Exchange.ActiveSync"]
    => issue(Type = "http://schemas.microsoft.com/authorization/claims/permit", Value = "true");

##### <a name="rule-3"></a><span data-ttu-id="d4ce1-194">規則 3</span><span class="sxs-lookup"><span data-stu-id="d4ce1-194">Rule 3</span></span>
    @RuleName = "Allow extranet browser and browser dialog traffic"
    c1:[Type == "http://schemas.microsoft.com/ws/2012/01/insidecorporatenetwork", Value == "false"] &&
    c2:[Type == "http://schemas.microsoft.com/2012/01/requestcontext/claims/x-ms-endpoint-absolute-path", Value =~ "(/adfs/ls)|(/adfs/oauth2)"]
    => issue(Type = "http://schemas.microsoft.com/authorization/claims/permit", Value = "true");

#### <a name="option-2-allow-exchange-activesync-and-block-legacy-apps"></a><span data-ttu-id="d4ce1-195">選項 2︰允許 Exchange ActiveSync，並且封鎖舊版應用程式</span><span class="sxs-lookup"><span data-stu-id="d4ce1-195">Option 2: Allow Exchange ActiveSync, and block legacy apps</span></span>
<span data-ttu-id="d4ce1-196">將下列三個規則套用到適用於 Microsoft Office 365 身分識別平台的 AD FS 信賴憑證者信任，Exchange ActiveSync 流量以及瀏覽器和新式驗證流量就會有存取權。</span><span class="sxs-lookup"><span data-stu-id="d4ce1-196">By applying the following three rules to the AD FS relying party trust for Microsoft Office 365 Identity Platform, Exchange ActiveSync traffic, and browser and modern authentication traffic, have access.</span></span> <span data-ttu-id="d4ce1-197">來自任何位置的舊版應用程式會遭到封鎖。</span><span class="sxs-lookup"><span data-stu-id="d4ce1-197">Legacy apps are blocked from any location.</span></span>

##### <a name="rule-1"></a><span data-ttu-id="d4ce1-198">規則 1</span><span class="sxs-lookup"><span data-stu-id="d4ce1-198">Rule 1</span></span>
    @RuleName = "Allow all intranet traffic only for browser and modern authentication clients"
    c1:[Type == "http://schemas.microsoft.com/ws/2012/01/insidecorporatenetwork", Value == "true"] &&
    c2:[Type == "http://schemas.microsoft.com/2012/01/requestcontext/claims/x-ms-endpoint-absolute-path", Value =~ "(/adfs/ls)|(/adfs/oauth2)"]
    => issue(Type = "http://schemas.microsoft.com/authorization/claims/permit", Value = "true");


##### <a name="rule-2"></a><span data-ttu-id="d4ce1-199">規則 2</span><span class="sxs-lookup"><span data-stu-id="d4ce1-199">Rule 2</span></span>
    @RuleName = "Allow Exchange ActiveSync"
    c1:[Type == "http://schemas.microsoft.com/2012/01/requestcontext/claims/x-ms-client-application", Value == "Microsoft.Exchange.ActiveSync"]
    => issue(Type = "http://schemas.microsoft.com/authorization/claims/permit", Value = "true");


##### <a name="rule-3"></a><span data-ttu-id="d4ce1-200">規則 3</span><span class="sxs-lookup"><span data-stu-id="d4ce1-200">Rule 3</span></span>
    @RuleName = "Allow extranet browser and browser dialog traffic"
    c1:[Type == "http://schemas.microsoft.com/ws/2012/01/insidecorporatenetwork", Value == "false"] &&
    c2:[Type == "http://schemas.microsoft.com/2012/01/requestcontext/claims/x-ms-endpoint-absolute-path", Value =~ "(/adfs/ls)|(/adfs/oauth2)"]
    => issue(Type = "http://schemas.microsoft.com/authorization/claims/permit", Value = "true");


## <a name="supported-browsers-for-device-based-policies"></a><span data-ttu-id="d4ce1-201">裝置型原則的支援瀏覽器</span><span class="sxs-lookup"><span data-stu-id="d4ce1-201">Supported browsers for device based policies</span></span> 

<span data-ttu-id="d4ce1-202">您只能取得針對 Azure AD 可以識別及驗證裝置時檢查裝置相容性和網域加入之裝置型原則的存取權。</span><span class="sxs-lookup"><span data-stu-id="d4ce1-202">You can only get access for device based policies that check for device compliance and domain join when Azure AD can identify and authenticate the device.</span></span> <span data-ttu-id="d4ce1-203">大部分的檢查 (例如位置和 MFA) 是在大部分裝置和瀏覽器上運作，所以裝置原則需要以下所列的 OS 版本和瀏覽器。</span><span class="sxs-lookup"><span data-stu-id="d4ce1-203">While most checks, like location and MFA work on most devices and browsers, device policies require of the OS version and browsers listed below.</span></span> <span data-ttu-id="d4ce1-204">當裝置原則已就緒，則會封鎖不受支援之瀏覽器或作業系統上的使用者存取。</span><span class="sxs-lookup"><span data-stu-id="d4ce1-204">Access is blocked for users on  unsupported browsers or the operating systems when a device policy is in place.</span></span> 

| <span data-ttu-id="d4ce1-205">作業系統</span><span class="sxs-lookup"><span data-stu-id="d4ce1-205">OS</span></span>                     | <span data-ttu-id="d4ce1-206">瀏覽器</span><span class="sxs-lookup"><span data-stu-id="d4ce1-206">Browsers</span></span>                 | <span data-ttu-id="d4ce1-207">支援</span><span class="sxs-lookup"><span data-stu-id="d4ce1-207">Support</span></span>     |
| :--                    | :--                      | :-:         |
| <span data-ttu-id="d4ce1-208">Win 10</span><span class="sxs-lookup"><span data-stu-id="d4ce1-208">Win 10</span></span>                 | <span data-ttu-id="d4ce1-209">IE、Edge</span><span class="sxs-lookup"><span data-stu-id="d4ce1-209">IE, Edge</span></span>                 | ![勾選][1] |
| <span data-ttu-id="d4ce1-211">Win 10</span><span class="sxs-lookup"><span data-stu-id="d4ce1-211">Win 10</span></span>                 | <span data-ttu-id="d4ce1-212">Chrome</span><span class="sxs-lookup"><span data-stu-id="d4ce1-212">Chrome</span></span>                   | <span data-ttu-id="d4ce1-213">預覽</span><span class="sxs-lookup"><span data-stu-id="d4ce1-213">Preview</span></span>     |
| <span data-ttu-id="d4ce1-214">Win 8 / 8.1</span><span class="sxs-lookup"><span data-stu-id="d4ce1-214">Win 8 / 8.1</span></span>            | <span data-ttu-id="d4ce1-215">IE、Chrome</span><span class="sxs-lookup"><span data-stu-id="d4ce1-215">IE, Chrome</span></span>               | ![勾選][1] |
| <span data-ttu-id="d4ce1-217">Win 7</span><span class="sxs-lookup"><span data-stu-id="d4ce1-217">Win 7</span></span>                  | <span data-ttu-id="d4ce1-218">IE、Chrome</span><span class="sxs-lookup"><span data-stu-id="d4ce1-218">IE, Chrome</span></span>               | ![勾選][1] |
| <span data-ttu-id="d4ce1-220">iOS</span><span class="sxs-lookup"><span data-stu-id="d4ce1-220">iOS</span></span>                    | <span data-ttu-id="d4ce1-221">Safari</span><span class="sxs-lookup"><span data-stu-id="d4ce1-221">Safari</span></span>                   | ![勾選][1] |
| <span data-ttu-id="d4ce1-223">Android</span><span class="sxs-lookup"><span data-stu-id="d4ce1-223">Android</span></span>                | <span data-ttu-id="d4ce1-224">Chrome</span><span class="sxs-lookup"><span data-stu-id="d4ce1-224">Chrome</span></span>                   | ![勾選][1] |
| <span data-ttu-id="d4ce1-226">Windows Phone</span><span class="sxs-lookup"><span data-stu-id="d4ce1-226">Windows Phone</span></span>          | <span data-ttu-id="d4ce1-227">IE、Edge</span><span class="sxs-lookup"><span data-stu-id="d4ce1-227">IE, Edge</span></span>                 | ![勾選][1] |
| <span data-ttu-id="d4ce1-229">Windows Server 2016</span><span class="sxs-lookup"><span data-stu-id="d4ce1-229">Windows Server 2016</span></span>    | <span data-ttu-id="d4ce1-230">IE、Edge</span><span class="sxs-lookup"><span data-stu-id="d4ce1-230">IE, Edge</span></span>                 | ![勾選][1] |
| <span data-ttu-id="d4ce1-232">Windows Server 2016</span><span class="sxs-lookup"><span data-stu-id="d4ce1-232">Windows Server 2016</span></span>    | <span data-ttu-id="d4ce1-233">Chrome</span><span class="sxs-lookup"><span data-stu-id="d4ce1-233">Chrome</span></span>                   | <span data-ttu-id="d4ce1-234">敬請期待</span><span class="sxs-lookup"><span data-stu-id="d4ce1-234">Coming soon</span></span> |
| <span data-ttu-id="d4ce1-235">Windows Server 2012 R2</span><span class="sxs-lookup"><span data-stu-id="d4ce1-235">Windows Server 2012 R2</span></span> | <span data-ttu-id="d4ce1-236">IE、Chrome</span><span class="sxs-lookup"><span data-stu-id="d4ce1-236">IE, Chrome</span></span>               | ![勾選][1] |
| <span data-ttu-id="d4ce1-238">Windows Server 2008 R2</span><span class="sxs-lookup"><span data-stu-id="d4ce1-238">Windows Server 2008 R2</span></span> | <span data-ttu-id="d4ce1-239">IE、Chrome</span><span class="sxs-lookup"><span data-stu-id="d4ce1-239">IE, Chrome</span></span>               | ![勾選][1] |
| <span data-ttu-id="d4ce1-241">Mac OS</span><span class="sxs-lookup"><span data-stu-id="d4ce1-241">Mac OS</span></span>                 | <span data-ttu-id="d4ce1-242">Safari</span><span class="sxs-lookup"><span data-stu-id="d4ce1-242">Safari</span></span>                   | ![勾選][1] |
| <span data-ttu-id="d4ce1-244">Mac OS</span><span class="sxs-lookup"><span data-stu-id="d4ce1-244">Mac OS</span></span>                 | <span data-ttu-id="d4ce1-245">Chrome</span><span class="sxs-lookup"><span data-stu-id="d4ce1-245">Chrome</span></span>                   | <span data-ttu-id="d4ce1-246">敬請期待</span><span class="sxs-lookup"><span data-stu-id="d4ce1-246">Coming soon</span></span> |

> [!NOTE]
> <span data-ttu-id="d4ce1-247">針對 Chrome 支援，您必須使用 Windows 10 建立者更新，而且安裝可以在[這裡](https://chrome.google.com/webstore/detail/windows-10-accounts/ppnbnpeolgkicgegkbkbjmhlideopiji)找到的擴充功能。</span><span class="sxs-lookup"><span data-stu-id="d4ce1-247">For Chrome support, you must be using Windows 10 Creators Update and install the extension found [here](https://chrome.google.com/webstore/detail/windows-10-accounts/ppnbnpeolgkicgegkbkbjmhlideopiji).</span></span>
>
>

## <a name="next-steps"></a><span data-ttu-id="d4ce1-248">後續步驟</span><span class="sxs-lookup"><span data-stu-id="d4ce1-248">Next steps</span></span>

<span data-ttu-id="d4ce1-249">如需詳細資訊，請參閱 [Azure Active Directory 中的條件式存取](active-directory-conditional-access.md)</span><span class="sxs-lookup"><span data-stu-id="d4ce1-249">For more details, see [Conditional access in Azure Active Directory](active-directory-conditional-access.md)</span></span>




<!--Image references-->
[1]: ./media/active-directory-conditional-access-supported-apps/ic195031.png


