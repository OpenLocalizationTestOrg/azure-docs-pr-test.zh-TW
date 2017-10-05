---
title: "Azure AD 同盟相容性清單"
description: "此頁面包含可用來實作單一登入的非 Microsoft 識別提供者。"
services: active-directory
documentationcenter: 
author: billmath
manager: femila
editor: curtand
ms.assetid: 22c8693e-8915-446d-b383-27e9587988ec
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/13/2017
ms.author: billmath
ms.openlocfilehash: bce5867017647764546d872d97943d5d4f01f2d2
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="azure-ad-federation-compatibility-list"></a><span data-ttu-id="88376-103">Azure AD 同盟相容性清單</span><span class="sxs-lookup"><span data-stu-id="88376-103">Azure AD federation compatibility list</span></span>
<span data-ttu-id="88376-104">Azure Active Directory 在不需要任何非 Microsoft 解決方案的情況下，針對 Office 365 和混合式與僅限雲端實作的其他 Microsoft 線上服務，提供單一登入和增強的應用程式存取安全性。</span><span class="sxs-lookup"><span data-stu-id="88376-104">Azure Active Directory provides single-sign on and enhanced application access security for Office 365 and other Microsoft Online services for hybrid and cloud-only implementations without requiring any non-Microsoft solution.</span></span> <span data-ttu-id="88376-105">Office 365，就像大部分 Microsoft 線上服務一樣，已經與 Azure Active Directory 整合以提供目錄服務、驗證及授權。</span><span class="sxs-lookup"><span data-stu-id="88376-105">Office 365, like most of Microsoft’s Online services, is integrated with Azure Active Directory for directory services, authentication and authorization.</span></span> <span data-ttu-id="88376-106">Azure Active Directory 也為數千個 SaaS 應用程式和內部部署 Web 應用程式提供單一登入。</span><span class="sxs-lookup"><span data-stu-id="88376-106">Azure Active Directory also provides single sign-on to thousands of SaaS applications and on-premises web applications.</span></span> <span data-ttu-id="88376-107">請參閱 Azure Active Directory 應用程式庫以了解支援的 SaaS 應用程式有哪些。</span><span class="sxs-lookup"><span data-stu-id="88376-107">Please see the Azure Active Directory application gallery for supported SaaS applications.</span></span>

<span data-ttu-id="88376-108">對於已經投資非 Microsoft 同盟方案的組織，此主題包含使用來自下面「Azure Active Directory 同盟相容性清單」中的非 Microsoft 識別提供者，為其 Windows Server Active Directory 使用者在 Microsoft 線上服務設定單一登入的指引。</span><span class="sxs-lookup"><span data-stu-id="88376-108">For organizations that have invested in non-Microsoft federation solutions, this topic contains guidance for configuring single sign-on for their Windows Server Active Directory users with Microsoft Online services by using non-Microsoft identity providers from the “Azure Active Directory federation compatibility list” below.</span></span> 

![](./media/active-directory-aadconnect-federation-compatibility/oxford2.jpg)   
<span data-ttu-id="88376-109">[Oxford Computer Group](http://oxfordcomputergroup.com/)這家代表 Microsoft 的協力廠商已使用非 Microsoft 識別提供者，針對一組常見的 Azure Active Directory 使用案例測試這些單一登入體驗。</span><span class="sxs-lookup"><span data-stu-id="88376-109">[Oxford Computer Group](http://oxfordcomputergroup.com/), a third-party, on behalf of Microsoft, tested these single sign-on experiences using non-Microsoft identity providers against a set of use cases common with Azure Active Directory.</span></span>

<span data-ttu-id="88376-110">如需如何取得此處所列的協力廠商識別提供者資訊，請與 Oxford Computer Group 連絡： [idp@oxfordcomputergroup.com](mailto:idp@oxfordcomputergroup.com)。</span><span class="sxs-lookup"><span data-stu-id="88376-110">For information on how you can get your third-party identity provider listed here, contact Oxford Computer Group at [idp@oxfordcomputergroup.com](mailto:idp@oxfordcomputergroup.com).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="88376-111">Oxford Computer Group 僅測試這些單一登入案例的同盟功能。</span><span class="sxs-lookup"><span data-stu-id="88376-111">Oxford Computer Group tested only the federation functionality of these single sign-on scenarios.</span></span> <span data-ttu-id="88376-112">Oxford Computer Group 並未針對這些單一登入案例的同步處理、雙因素驗證等等元件執行任何測試。</span><span class="sxs-lookup"><span data-stu-id="88376-112">Oxford Computer Group did not perform any testing of the synchronization, two-factor authentication, etc. components of these single sign-on scenarios.</span></span>
> 
> <span data-ttu-id="88376-113">此計劃中也未測試使用替代識別碼登入 UPN。</span><span class="sxs-lookup"><span data-stu-id="88376-113">Use of Sign-in by Alternate ID to UPN is also not tested in this program.</span></span>
> 
> 

* [<span data-ttu-id="88376-114">Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="88376-114">Azure Active Directory</span></span>](#azure-active-directory)
* [<span data-ttu-id="88376-115">AuthAnvil Single Sign On 4.5</span><span class="sxs-lookup"><span data-stu-id="88376-115">AuthAnvil Single Sign On 4.5</span></span>](#authanvil-single-sign-on-45)
* [<span data-ttu-id="88376-116">BIG-IP with Access Policy Manager BIG-IP ver.11.3x – 11.6x</span><span class="sxs-lookup"><span data-stu-id="88376-116">BIG-IP with Access Policy Manager BIG-IP ver. 11.3x – 11.6x</span></span>](#big-ip-with-access-policy-manager-big-ip-ver-113x--116x) 
* [<span data-ttu-id="88376-117">BitGlass</span><span class="sxs-lookup"><span data-stu-id="88376-117">BitGlass</span></span>](#bitglass)
* [<span data-ttu-id="88376-118">CA Secure Cloud</span><span class="sxs-lookup"><span data-stu-id="88376-118">CA Secure Cloud</span></span>](#ca-secure-cloud) 
* [<span data-ttu-id="88376-119">CA SiteMinder 12.52</span><span class="sxs-lookup"><span data-stu-id="88376-119">CA SiteMinder 12.52</span></span>](#ca-siteminder-1252-sp1-cumulative-release-4) 
* [<span data-ttu-id="88376-120">Centrify</span><span class="sxs-lookup"><span data-stu-id="88376-120">Centrify</span></span>](#centrify) 
* [<span data-ttu-id="88376-121">Dell One Identity Cloud Access Manager v7.1</span><span class="sxs-lookup"><span data-stu-id="88376-121">Dell One Identity Cloud Access Manager v7.1</span></span>](#dell-one-identity-cloud-access-manager-v71) 
* [<span data-ttu-id="88376-122">DigitalPersona Composite 驗證</span><span class="sxs-lookup"><span data-stu-id="88376-122">DigitalPersona Composite Authentication</span></span>](#digitalpersona-composite-authentication)
* [<span data-ttu-id="88376-123">IBM Tivoli Federated Identity Manager 6.2.2</span><span class="sxs-lookup"><span data-stu-id="88376-123">IBM Tivoli Federated Identity Manager 6.2.2</span></span>](#ibm-tivoli-federated-identity-manager-622) 
* [<span data-ttu-id="88376-124">IceWall Federation Version 3.0</span><span class="sxs-lookup"><span data-stu-id="88376-124">IceWall Federation Version 3.0</span></span>](#icewall-federation-version-30) 
* [<span data-ttu-id="88376-125">Memority</span><span class="sxs-lookup"><span data-stu-id="88376-125">Memority</span></span>](#memority)
* [<span data-ttu-id="88376-126">NetIQ Access Manager 4.x</span><span class="sxs-lookup"><span data-stu-id="88376-126">NetIQ Access Manager 4.x</span></span>](#netiq-access-manager-4x) 
* [<span data-ttu-id="88376-127">Okta</span><span class="sxs-lookup"><span data-stu-id="88376-127">Okta</span></span>](#okta) 
* [<span data-ttu-id="88376-128">OneLogin</span><span class="sxs-lookup"><span data-stu-id="88376-128">OneLogin</span></span>](#onelogin) 
* [<span data-ttu-id="88376-129">Optimal IDM Virtual Identity Server Federation Services</span><span class="sxs-lookup"><span data-stu-id="88376-129">Optimal IDM Virtual Identity Server Federation Services</span></span>](#optimal-idm-virtual-identity-server-federation-services) 
* [<span data-ttu-id="88376-130">PingFederate 6.11, 7.2, 8.x</span><span class="sxs-lookup"><span data-stu-id="88376-130">PingFederate 6.11, 7.2, 8.x</span></span>](#pingfederate-611-72-8x)
* [<span data-ttu-id="88376-131">RadiantOne CFS 3.0</span><span class="sxs-lookup"><span data-stu-id="88376-131">RadiantOne CFS 3.0</span></span>](#radiantone-cfs-30) 
* [<span data-ttu-id="88376-132">Sailpoint IdentityNow</span><span class="sxs-lookup"><span data-stu-id="88376-132">Sailpoint IdentityNow</span></span>](#sailpoint-identitynow)
* [<span data-ttu-id="88376-133">SecureAuth IdP 7.2.0</span><span class="sxs-lookup"><span data-stu-id="88376-133">SecureAuth IdP 7.2.0</span></span>](#secureauth-idp-720) 
* [<span data-ttu-id="88376-134">Sign&go 5.3</span><span class="sxs-lookup"><span data-stu-id="88376-134">Sign&go 5.3</span></span>](#signgo-53) 
* [<span data-ttu-id="88376-135">SoftBank Technology Online Service Gate</span><span class="sxs-lookup"><span data-stu-id="88376-135">SoftBank Technology Online Service Gate</span></span>](#softbank)
* [<span data-ttu-id="88376-136">VMware Workspace One</span><span class="sxs-lookup"><span data-stu-id="88376-136">VMware Workspace One</span></span>](#vmware-workspace-one)



> [!IMPORTANT]
> <span data-ttu-id="88376-137">由於這些都是協力廠商產品，因此對於與這些識別提供者有關的部署、設定、疑難排解、最佳作法等等問題，Microsoft 並沒有提供支援。</span><span class="sxs-lookup"><span data-stu-id="88376-137">Since these are third-party products, Microsoft does not provide support for the deployment, configuration, troubleshooting, best practices, etc. issues and questions regarding these identity providers.</span></span> <span data-ttu-id="88376-138">對於和這些識別提供者有關的支援與問題，請直接連絡支援的協力廠商。</span><span class="sxs-lookup"><span data-stu-id="88376-138">For support and questions regarding these identity providers, contact the supported third-parties directly.</span></span>
> 
> <span data-ttu-id="88376-139">這些協力廠商識別提供者僅使用 WS-同盟與 WS-Trust 通訊協定，針對與 Microsoft 雲端服務的互通性進行測試。</span><span class="sxs-lookup"><span data-stu-id="88376-139">These third-party identity providers were tested for interoperability with Microsoft cloud services using WS-Federation and WS-Trust protocols only.</span></span> <span data-ttu-id="88376-140">測試並不包含使用 SAML 通訊協定。</span><span class="sxs-lookup"><span data-stu-id="88376-140">Testing did not include using the SAML protocol.</span></span>
> 


## <a name="azure-active-directory"></a><span data-ttu-id="88376-141">Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="88376-141">Azure Active Directory</span></span>

<span data-ttu-id="88376-142">以下是支援此登入體驗之矩陣的案例：</span><span class="sxs-lookup"><span data-stu-id="88376-142">The following is the scenario support matrix for this sign-on experience:</span></span> 

| <span data-ttu-id="88376-143">用戶端</span><span class="sxs-lookup"><span data-stu-id="88376-143">Client</span></span> | <span data-ttu-id="88376-144">支援</span><span class="sxs-lookup"><span data-stu-id="88376-144">Support</span></span> | <span data-ttu-id="88376-145">例外狀況</span><span class="sxs-lookup"><span data-stu-id="88376-145">Exceptions</span></span> |
| --- | --- | --- |
| <span data-ttu-id="88376-146">Web 用戶端，例如 Exchange Web Access 和 SharePoint Online</span><span class="sxs-lookup"><span data-stu-id="88376-146">Web-based clients such as Exchange Web Access and SharePoint Online</span></span> |<span data-ttu-id="88376-147">支援</span><span class="sxs-lookup"><span data-stu-id="88376-147">Supported</span></span> |<span data-ttu-id="88376-148">None</span><span class="sxs-lookup"><span data-stu-id="88376-148">None</span></span> |
| <span data-ttu-id="88376-149">豐富型用戶端應用程式，例如 Lync、Office 訂閱、CRM</span><span class="sxs-lookup"><span data-stu-id="88376-149">Rich client applications such as Lync, Office Subscription, CRM</span></span> |<span data-ttu-id="88376-150">支援</span><span class="sxs-lookup"><span data-stu-id="88376-150">Supported</span></span> |<span data-ttu-id="88376-151">None</span><span class="sxs-lookup"><span data-stu-id="88376-151">None</span></span> |
| <span data-ttu-id="88376-152">豐富型電子郵件用戶端，例如 Outlook 和 ActiveSync</span><span class="sxs-lookup"><span data-stu-id="88376-152">Email-rich clients such as Outlook and ActiveSync</span></span> |<span data-ttu-id="88376-153">支援</span><span class="sxs-lookup"><span data-stu-id="88376-153">Supported</span></span> |<span data-ttu-id="88376-154">None</span><span class="sxs-lookup"><span data-stu-id="88376-154">None</span></span> |
| <span data-ttu-id="88376-155">使用 ADAL 的現代應用程式，例如 Office 2016</span><span class="sxs-lookup"><span data-stu-id="88376-155">Modern Applications using ADAL such as Office 2016</span></span> |<span data-ttu-id="88376-156">支援</span><span class="sxs-lookup"><span data-stu-id="88376-156">Supported</span></span> |<span data-ttu-id="88376-157">None</span><span class="sxs-lookup"><span data-stu-id="88376-157">None</span></span> |

<span data-ttu-id="88376-158">如需搭配使用 Azure Active Directory 與 AD FS 的詳細資訊，請參閱 [Active Directory 同盟服務 (ADFS)](active-directory-aadconnect-get-started-custom.md#configuring-federation-with-ad-fs)。</span><span class="sxs-lookup"><span data-stu-id="88376-158">For more information about using Azure Active Directory with AD FS see [Active Directory Federation Services (ADFS)](active-directory-aadconnect-get-started-custom.md#configuring-federation-with-ad-fs).</span></span>

<span data-ttu-id="88376-159">如需搭配密碼同步使用 Azure Active Directory 的相關詳細資訊，請參閱 [Azure AD Connect](active-directory-aadconnect.md)。</span><span class="sxs-lookup"><span data-stu-id="88376-159">For more information about using Azure Active Directory with Password sync see [Azure AD Connect](active-directory-aadconnect.md).</span></span>

## <a name="authanvil-single-sign-on-45"></a><span data-ttu-id="88376-160">AuthAnvil Single Sign On 4.5</span><span class="sxs-lookup"><span data-stu-id="88376-160">AuthAnvil Single Sign On 4.5</span></span>

<span data-ttu-id="88376-161">以下是支援此單一登入體驗之矩陣的案例：</span><span class="sxs-lookup"><span data-stu-id="88376-161">The following is the scenario support matrix for this single sign-on experience:</span></span>

| <span data-ttu-id="88376-162">用戶端</span><span class="sxs-lookup"><span data-stu-id="88376-162">Client</span></span> | <span data-ttu-id="88376-163">支援</span><span class="sxs-lookup"><span data-stu-id="88376-163">Support</span></span> | <span data-ttu-id="88376-164">例外狀況</span><span class="sxs-lookup"><span data-stu-id="88376-164">Exceptions</span></span> |
| --- | --- | --- |
| <span data-ttu-id="88376-165">Web 用戶端，例如 Exchange Web Access 和 SharePoint Online</span><span class="sxs-lookup"><span data-stu-id="88376-165">Web-based clients such as Exchange Web Access and SharePoint Online</span></span> |<span data-ttu-id="88376-166">支援</span><span class="sxs-lookup"><span data-stu-id="88376-166">Supported</span></span> |<span data-ttu-id="88376-167">不支援整合式 Windows 驗證</span><span class="sxs-lookup"><span data-stu-id="88376-167">Integrated Windows Authentication is not supported</span></span> |
| <span data-ttu-id="88376-168">豐富型用戶端應用程式，例如 Lync、Office 訂閱、CRM</span><span class="sxs-lookup"><span data-stu-id="88376-168">Rich client applications such as Lync, Office Subscription, CRM</span></span> |<span data-ttu-id="88376-169">支援</span><span class="sxs-lookup"><span data-stu-id="88376-169">Supported</span></span> |<span data-ttu-id="88376-170">不支援整合式 Windows 驗證</span><span class="sxs-lookup"><span data-stu-id="88376-170">Integrated Windows Authentication is not supported</span></span> |
| <span data-ttu-id="88376-171">豐富型電子郵件用戶端，例如 Outlook 和 ActiveSync</span><span class="sxs-lookup"><span data-stu-id="88376-171">Email-rich clients such as Outlook and ActiveSync</span></span> |<span data-ttu-id="88376-172">支援</span><span class="sxs-lookup"><span data-stu-id="88376-172">Supported</span></span> |<span data-ttu-id="88376-173">None</span><span class="sxs-lookup"><span data-stu-id="88376-173">None</span></span> |

<span data-ttu-id="88376-174">如需詳細資訊，請參閱 [AuthAnvil 單一登入](https://help.scorpionsoft.com/entries/26538603-How-can-I-Configure-Single-Sign-On-for-Office-365-)。</span><span class="sxs-lookup"><span data-stu-id="88376-174">For more information, see [AuthAnvil Single Sign On.](https://help.scorpionsoft.com/entries/26538603-How-can-I-Configure-Single-Sign-On-for-Office-365-).</span></span>


## <a name="big-ip-with-access-policy-manager-big-ip-ver-113x--116x"></a><span data-ttu-id="88376-175">BIG-IP with Access Policy Manager BIG-IP ver.</span><span class="sxs-lookup"><span data-stu-id="88376-175">BIG-IP with Access Policy Manager BIG-IP ver.</span></span> <span data-ttu-id="88376-176">11.3x – 11.6x</span><span class="sxs-lookup"><span data-stu-id="88376-176">11.3x – 11.6x</span></span>

<span data-ttu-id="88376-177">以下是支援此單一登入體驗之矩陣的案例：</span><span class="sxs-lookup"><span data-stu-id="88376-177">The following is the scenario support matrix for this single sign-on experience:</span></span> 

| <span data-ttu-id="88376-178">用戶端</span><span class="sxs-lookup"><span data-stu-id="88376-178">Client</span></span> | <span data-ttu-id="88376-179">支援</span><span class="sxs-lookup"><span data-stu-id="88376-179">Support</span></span> | <span data-ttu-id="88376-180">例外狀況</span><span class="sxs-lookup"><span data-stu-id="88376-180">Exceptions</span></span> |
| --- | --- | --- |
| <span data-ttu-id="88376-181">Web 用戶端，例如 Exchange Web Access 和 SharePoint Online</span><span class="sxs-lookup"><span data-stu-id="88376-181">Web-based clients such as Exchange Web Access and SharePoint Online</span></span> |<span data-ttu-id="88376-182">支援</span><span class="sxs-lookup"><span data-stu-id="88376-182">Supported</span></span> |<span data-ttu-id="88376-183">None</span><span class="sxs-lookup"><span data-stu-id="88376-183">None</span></span> |
| <span data-ttu-id="88376-184">豐富型用戶端應用程式，例如 Lync、Office 訂閱、CRM</span><span class="sxs-lookup"><span data-stu-id="88376-184">Rich client applications such as Lync, Office Subscription, CRM</span></span> |<span data-ttu-id="88376-185">不支援</span><span class="sxs-lookup"><span data-stu-id="88376-185">Not Supported</span></span> |<span data-ttu-id="88376-186">不支援</span><span class="sxs-lookup"><span data-stu-id="88376-186">Not Supported</span></span> |
| <span data-ttu-id="88376-187">豐富型電子郵件用戶端，例如 Outlook 和 ActiveSync</span><span class="sxs-lookup"><span data-stu-id="88376-187">Email-rich clients such as Outlook and ActiveSync</span></span> |<span data-ttu-id="88376-188">支援</span><span class="sxs-lookup"><span data-stu-id="88376-188">Supported</span></span> |<span data-ttu-id="88376-189">None</span><span class="sxs-lookup"><span data-stu-id="88376-189">None</span></span> |

<span data-ttu-id="88376-190">如需 BIG-IP Access Policy Manager 的相關詳細資訊，請參閱 [BIG-IP Access Policy Manager](https://f5.com/products/modules/access-policy-manager)</span><span class="sxs-lookup"><span data-stu-id="88376-190">For more information about BIG-IP Access Policy Manager, see [BIG-IP Access Policy Manager.](https://f5.com/products/modules/access-policy-manager)</span></span> 

<span data-ttu-id="88376-191">如需如何設定此 STS 來為您的 Active Directory 使用者提供單一登入體驗的 BIG-IP Access Policy Manager 指示，請下載 pdf [BIG-IP](http://www.f5.com/pdf/deployment-guides/microsoft-office-365-idp-dg.pdf)。</span><span class="sxs-lookup"><span data-stu-id="88376-191">For the BIG-IP Access Policy Manager instructions on how to configure this STS to provide the single sign-on experience to your Active Directory Users, download the pdf [BIG-IP](http://www.f5.com/pdf/deployment-guides/microsoft-office-365-idp-dg.pdf).</span></span>

## <a name="bitglass"></a><span data-ttu-id="88376-192">BitGlass</span><span class="sxs-lookup"><span data-stu-id="88376-192">BitGlass</span></span>

<span data-ttu-id="88376-193">以下是支援此單一登入體驗之矩陣的案例：</span><span class="sxs-lookup"><span data-stu-id="88376-193">The following is the scenario support matrix for this single sign-on experience:</span></span>

| <span data-ttu-id="88376-194">用戶端</span><span class="sxs-lookup"><span data-stu-id="88376-194">Client</span></span> | <span data-ttu-id="88376-195">支援</span><span class="sxs-lookup"><span data-stu-id="88376-195">Support</span></span> | <span data-ttu-id="88376-196">例外狀況</span><span class="sxs-lookup"><span data-stu-id="88376-196">Exceptions</span></span> |
| --- | --- | --- |
| <span data-ttu-id="88376-197">Web 用戶端，例如 Exchange Web Access 和 SharePoint Online</span><span class="sxs-lookup"><span data-stu-id="88376-197">Web-based clients such as Exchange Web Access and SharePoint Online</span></span> |<span data-ttu-id="88376-198">支援</span><span class="sxs-lookup"><span data-stu-id="88376-198">Supported</span></span> |<span data-ttu-id="88376-199">不支援整合式 Windows 驗證</span><span class="sxs-lookup"><span data-stu-id="88376-199">Integrated Windows Authentication is not supported</span></span> |
| <span data-ttu-id="88376-200">豐富型用戶端應用程式，例如 Lync、Office 訂閱、CRM</span><span class="sxs-lookup"><span data-stu-id="88376-200">Rich client applications such as Lync, Office Subscription, CRM</span></span> |<span data-ttu-id="88376-201">支援</span><span class="sxs-lookup"><span data-stu-id="88376-201">Supported</span></span> |<span data-ttu-id="88376-202">不支援整合式 Windows 驗證</span><span class="sxs-lookup"><span data-stu-id="88376-202">Integrated Windows Authentication is not supported</span></span> |
| <span data-ttu-id="88376-203">豐富型電子郵件用戶端，例如 Outlook 和 ActiveSync</span><span class="sxs-lookup"><span data-stu-id="88376-203">Email-rich clients such as Outlook and ActiveSync</span></span> |<span data-ttu-id="88376-204">支援</span><span class="sxs-lookup"><span data-stu-id="88376-204">Supported</span></span> |<span data-ttu-id="88376-205">None</span><span class="sxs-lookup"><span data-stu-id="88376-205">None</span></span> |

<span data-ttu-id="88376-206">如需 BitGlass 的詳細資訊，請參閱 [BitGlass](http://www.bitglass.com)。</span><span class="sxs-lookup"><span data-stu-id="88376-206">For more information about BitGlass see [BitGlass](http://www.bitglass.com).</span></span>

## <a name="ca-secure-cloud"></a><span data-ttu-id="88376-207">CA Secure Cloud</span><span class="sxs-lookup"><span data-stu-id="88376-207">CA Secure Cloud</span></span>

<span data-ttu-id="88376-208">以下是支援此單一登入體驗之矩陣的案例：</span><span class="sxs-lookup"><span data-stu-id="88376-208">The following is the scenario support matrix for this single sign-on experience:</span></span>

| <span data-ttu-id="88376-209">用戶端</span><span class="sxs-lookup"><span data-stu-id="88376-209">Client</span></span> | <span data-ttu-id="88376-210">支援</span><span class="sxs-lookup"><span data-stu-id="88376-210">Support</span></span> | <span data-ttu-id="88376-211">例外狀況</span><span class="sxs-lookup"><span data-stu-id="88376-211">Exceptions</span></span> |
| --- | --- | --- |
| <span data-ttu-id="88376-212">Web 用戶端，例如 Exchange Web Access 和 SharePoint Online</span><span class="sxs-lookup"><span data-stu-id="88376-212">Web-based clients such as Exchange Web Access and SharePoint Online</span></span> |<span data-ttu-id="88376-213">支援</span><span class="sxs-lookup"><span data-stu-id="88376-213">Supported</span></span> |<span data-ttu-id="88376-214">不支援整合式 Windows 驗證</span><span class="sxs-lookup"><span data-stu-id="88376-214">Integrated Windows Authentication is not supported</span></span> |
| <span data-ttu-id="88376-215">豐富型用戶端應用程式，例如 Lync、Office 訂閱、CRM</span><span class="sxs-lookup"><span data-stu-id="88376-215">Rich client applications such as Lync, Office Subscription, CRM</span></span> |<span data-ttu-id="88376-216">支援</span><span class="sxs-lookup"><span data-stu-id="88376-216">Supported</span></span> |<span data-ttu-id="88376-217">不支援整合式 Windows 驗證</span><span class="sxs-lookup"><span data-stu-id="88376-217">Integrated Windows Authentication is not supported</span></span> |
| <span data-ttu-id="88376-218">豐富型電子郵件用戶端，例如 Outlook 和 ActiveSync</span><span class="sxs-lookup"><span data-stu-id="88376-218">Email-rich clients such as Outlook and ActiveSync</span></span> |<span data-ttu-id="88376-219">支援</span><span class="sxs-lookup"><span data-stu-id="88376-219">Supported</span></span> |<span data-ttu-id="88376-220">None</span><span class="sxs-lookup"><span data-stu-id="88376-220">None</span></span> |

<span data-ttu-id="88376-221">如需 CA Secure Cloud 的詳細資訊，請參閱 [CA Secure Cloud](http://www.ca.com/us/products/security-as-a-service.aspx)。</span><span class="sxs-lookup"><span data-stu-id="88376-221">For more information about CA Secure Cloud, see [CA Secure Cloud](http://www.ca.com/us/products/security-as-a-service.aspx).</span></span>

## <a name="ca-siteminder-1252-sp1-cumulative-release-4"></a><span data-ttu-id="88376-222">CA SiteMinder 12.52 SP1 累計版本 4</span><span class="sxs-lookup"><span data-stu-id="88376-222">CA SiteMinder 12.52 SP1 Cumulative Release 4</span></span>

<span data-ttu-id="88376-223">以下是支援此單一登入體驗之矩陣的案例：</span><span class="sxs-lookup"><span data-stu-id="88376-223">The following is the scenario support matrix for this single sign-on experience:</span></span> 

| <span data-ttu-id="88376-224">用戶端</span><span class="sxs-lookup"><span data-stu-id="88376-224">Client</span></span> | <span data-ttu-id="88376-225">支援</span><span class="sxs-lookup"><span data-stu-id="88376-225">Support</span></span> | <span data-ttu-id="88376-226">例外狀況</span><span class="sxs-lookup"><span data-stu-id="88376-226">Exceptions</span></span> |
| --- | --- | --- |
| <span data-ttu-id="88376-227">Web 用戶端，例如 Exchange Web Access 和 SharePoint Online</span><span class="sxs-lookup"><span data-stu-id="88376-227">Web-based clients such as Exchange Web Access and SharePoint Online</span></span> |<span data-ttu-id="88376-228">支援</span><span class="sxs-lookup"><span data-stu-id="88376-228">Supported</span></span> |<span data-ttu-id="88376-229">None</span><span class="sxs-lookup"><span data-stu-id="88376-229">None</span></span> |
| <span data-ttu-id="88376-230">豐富型用戶端應用程式，例如 Lync、Office 訂閱、CRM</span><span class="sxs-lookup"><span data-stu-id="88376-230">Rich client applications such as Lync, Office Subscription, CRM</span></span> |<span data-ttu-id="88376-231">支援</span><span class="sxs-lookup"><span data-stu-id="88376-231">Supported</span></span> |<span data-ttu-id="88376-232">None</span><span class="sxs-lookup"><span data-stu-id="88376-232">None</span></span> |
| <span data-ttu-id="88376-233">豐富型電子郵件用戶端，例如 Outlook 和 ActiveSync</span><span class="sxs-lookup"><span data-stu-id="88376-233">Email-rich clients such as Outlook and ActiveSync</span></span> |<span data-ttu-id="88376-234">支援</span><span class="sxs-lookup"><span data-stu-id="88376-234">Supported</span></span> |<span data-ttu-id="88376-235">None</span><span class="sxs-lookup"><span data-stu-id="88376-235">None</span></span> |

<span data-ttu-id="88376-236">如需 CA SiteMinder 的詳細資訊，請參閱 [CA SiteMinder Federation](http://www.ca.com/us/products/ca-single-sign-on.html)。</span><span class="sxs-lookup"><span data-stu-id="88376-236">For more information about CA SiteMinder, see [CA SiteMinder Federation](http://www.ca.com/us/products/ca-single-sign-on.html).</span></span> 

## <a name="centrify"></a><span data-ttu-id="88376-237">Centrify</span><span class="sxs-lookup"><span data-stu-id="88376-237">Centrify</span></span>

<span data-ttu-id="88376-238">以下是支援此單一登入體驗之矩陣的案例：</span><span class="sxs-lookup"><span data-stu-id="88376-238">The following is the scenario support matrix for this single sign-on experience:</span></span>

| <span data-ttu-id="88376-239">用戶端</span><span class="sxs-lookup"><span data-stu-id="88376-239">Client</span></span> | <span data-ttu-id="88376-240">支援</span><span class="sxs-lookup"><span data-stu-id="88376-240">Support</span></span> | <span data-ttu-id="88376-241">例外狀況</span><span class="sxs-lookup"><span data-stu-id="88376-241">Exceptions</span></span> |
| --- | --- | --- |
| <span data-ttu-id="88376-242">Web 用戶端，例如 Exchange Web Access 和 SharePoint Online</span><span class="sxs-lookup"><span data-stu-id="88376-242">Web-based clients such as Exchange Web Access and SharePoint Online</span></span> |<span data-ttu-id="88376-243">支援</span><span class="sxs-lookup"><span data-stu-id="88376-243">Supported</span></span> |<span data-ttu-id="88376-244">None</span><span class="sxs-lookup"><span data-stu-id="88376-244">None</span></span> |
| <span data-ttu-id="88376-245">豐富型用戶端應用程式，例如 Lync、Office 訂閱、CRM</span><span class="sxs-lookup"><span data-stu-id="88376-245">Rich client applications such as Lync, Office Subscription, CRM</span></span> |<span data-ttu-id="88376-246">支援</span><span class="sxs-lookup"><span data-stu-id="88376-246">Supported</span></span> |<span data-ttu-id="88376-247">None</span><span class="sxs-lookup"><span data-stu-id="88376-247">None</span></span> |
| <span data-ttu-id="88376-248">豐富型電子郵件用戶端，例如 Outlook 和 ActiveSync</span><span class="sxs-lookup"><span data-stu-id="88376-248">Email-rich clients such as Outlook and ActiveSync</span></span> |<span data-ttu-id="88376-249">支援</span><span class="sxs-lookup"><span data-stu-id="88376-249">Supported</span></span> |<span data-ttu-id="88376-250">不支援用戶端存取控制</span><span class="sxs-lookup"><span data-stu-id="88376-250">Client Access Control is not supported</span></span> |

<span data-ttu-id="88376-251">如需 Centrify 的詳細資訊，請參閱 [Centrify](http://www.centrify.com/cloud/apps/single-sign-on-for-office-365.asp)。</span><span class="sxs-lookup"><span data-stu-id="88376-251">For more information about Centrify, see [Centrify](http://www.centrify.com/cloud/apps/single-sign-on-for-office-365.asp).</span></span>

## <a name="dell-one-identity-cloud-access-manager-v71"></a><span data-ttu-id="88376-252">Dell One Identity Cloud Access Manager v7.1</span><span class="sxs-lookup"><span data-stu-id="88376-252">Dell One Identity Cloud Access Manager v7.1</span></span>

<span data-ttu-id="88376-253">以下是支援此單一登入體驗之矩陣的案例：</span><span class="sxs-lookup"><span data-stu-id="88376-253">The following is the scenario support matrix for this single sign-on experience:</span></span>

| <span data-ttu-id="88376-254">用戶端</span><span class="sxs-lookup"><span data-stu-id="88376-254">Client</span></span> | <span data-ttu-id="88376-255">支援</span><span class="sxs-lookup"><span data-stu-id="88376-255">Support</span></span> | <span data-ttu-id="88376-256">例外狀況</span><span class="sxs-lookup"><span data-stu-id="88376-256">Exceptions</span></span> |
| --- | --- | --- |
| <span data-ttu-id="88376-257">Web 用戶端，例如 Exchange Web Access 和 SharePoint Online</span><span class="sxs-lookup"><span data-stu-id="88376-257">Web-based clients such as Exchange Web Access and SharePoint Online</span></span> |<span data-ttu-id="88376-258">支援</span><span class="sxs-lookup"><span data-stu-id="88376-258">Supported</span></span> |<span data-ttu-id="88376-259">None</span><span class="sxs-lookup"><span data-stu-id="88376-259">None</span></span> |
| <span data-ttu-id="88376-260">豐富型用戶端應用程式，例如 Lync、Office 訂閱、CRM</span><span class="sxs-lookup"><span data-stu-id="88376-260">Rich client applications such as Lync, Office Subscription, CRM</span></span> |<span data-ttu-id="88376-261">支援</span><span class="sxs-lookup"><span data-stu-id="88376-261">Supported</span></span> |<span data-ttu-id="88376-262">None</span><span class="sxs-lookup"><span data-stu-id="88376-262">None</span></span> |
| <span data-ttu-id="88376-263">豐富型電子郵件用戶端，例如 Outlook 和 ActiveSync</span><span class="sxs-lookup"><span data-stu-id="88376-263">Email-rich clients such as Outlook and ActiveSync</span></span> |<span data-ttu-id="88376-264">支援</span><span class="sxs-lookup"><span data-stu-id="88376-264">Supported</span></span> |<span data-ttu-id="88376-265">None</span><span class="sxs-lookup"><span data-stu-id="88376-265">None</span></span> |

<span data-ttu-id="88376-266">如需 Dell One Identity Cloud Access Manager 的詳細資訊，請參閱 [Dell One Identity Cloud Access Manager](http://software.dell.com/products/cloud-access-manager)。</span><span class="sxs-lookup"><span data-stu-id="88376-266">For more information about Dell One Identity Cloud Access Manager, see [Dell One Identity Cloud Access Manager](http://software.dell.com/products/cloud-access-manager).</span></span>

 <span data-ttu-id="88376-267">如需如何設定此 STS 來為您的 Office 365 使用者提供單一登入體驗的指示，請參閱[設定 Office 365 使用者](http://documents.software.dell.com/dell-one-identity-cloud-access-manager/7.1/how-to-configure-microsoft-office-365)。</span><span class="sxs-lookup"><span data-stu-id="88376-267">For the instructions on how to configure this STS to provide the single sign-on experience to your Office 365 Users, see [Configure Office 365 Users](http://documents.software.dell.com/dell-one-identity-cloud-access-manager/7.1/how-to-configure-microsoft-office-365).</span></span> 

## <a name="digitalpersona-composite-authentication"></a><span data-ttu-id="88376-268">DigitalPersona Composite 驗證</span><span class="sxs-lookup"><span data-stu-id="88376-268">DigitalPersona Composite Authentication</span></span>  

<span data-ttu-id="88376-269">以下是支援此單一登入體驗之矩陣的案例：</span><span class="sxs-lookup"><span data-stu-id="88376-269">The following is the scenario support matrix for this single sign-on experience:</span></span>

| <span data-ttu-id="88376-270">用戶端</span><span class="sxs-lookup"><span data-stu-id="88376-270">Client</span></span> | <span data-ttu-id="88376-271">支援</span><span class="sxs-lookup"><span data-stu-id="88376-271">Support</span></span> | <span data-ttu-id="88376-272">例外狀況</span><span class="sxs-lookup"><span data-stu-id="88376-272">Exceptions</span></span> |
| --- | --- | --- |
| <span data-ttu-id="88376-273">Web 用戶端，例如 Exchange Web Access 和 SharePoint Online</span><span class="sxs-lookup"><span data-stu-id="88376-273">Web-based clients such as Exchange Web Access and SharePoint Online</span></span> |<span data-ttu-id="88376-274">支援</span><span class="sxs-lookup"><span data-stu-id="88376-274">Supported</span></span> |<span data-ttu-id="88376-275">不支援整合式 Windows 驗證</span><span class="sxs-lookup"><span data-stu-id="88376-275">Integrated Windows Authentication is not supported</span></span>|
| <span data-ttu-id="88376-276">豐富型用戶端應用程式，例如 Lync、Office 訂閱、CRM</span><span class="sxs-lookup"><span data-stu-id="88376-276">Rich client applications such as Lync, Office Subscription, CRM</span></span> |<span data-ttu-id="88376-277">支援</span><span class="sxs-lookup"><span data-stu-id="88376-277">Supported</span></span> |<span data-ttu-id="88376-278">不支援整合式 Windows 驗證</span><span class="sxs-lookup"><span data-stu-id="88376-278">Integrated Windows Authentication is not supported</span></span>|
| <span data-ttu-id="88376-279">豐富型電子郵件用戶端，例如 Outlook 和 ActiveSync</span><span class="sxs-lookup"><span data-stu-id="88376-279">Email-rich clients such as Outlook and ActiveSync</span></span> |<span data-ttu-id="88376-280">支援</span><span class="sxs-lookup"><span data-stu-id="88376-280">Supported</span></span> |<span data-ttu-id="88376-281">None</span><span class="sxs-lookup"><span data-stu-id="88376-281">None</span></span> |

<span data-ttu-id="88376-282">如需詳細資訊，請參閱 [DigitalPersona Composite 驗證](http://www.crossmatch.com/uploadedFiles/Support/Reference_Material/DigitalPersona-Office-365-Deployment-Guide.pdf)。</span><span class="sxs-lookup"><span data-stu-id="88376-282">For more information see [DigitalPersona Composite Authentication](http://www.crossmatch.com/uploadedFiles/Support/Reference_Material/DigitalPersona-Office-365-Deployment-Guide.pdf).</span></span>


## <a name="ibm-tivoli-federated-identity-manager-622"></a><span data-ttu-id="88376-283">IBM Tivoli Federated Identity Manager 6.2.2</span><span class="sxs-lookup"><span data-stu-id="88376-283">IBM Tivoli Federated Identity Manager 6.2.2</span></span>

<span data-ttu-id="88376-284">以下是支援此單一登入體驗之矩陣的案例：</span><span class="sxs-lookup"><span data-stu-id="88376-284">The following is the scenario support matrix for this single sign-on experience:</span></span> 

| <span data-ttu-id="88376-285">用戶端</span><span class="sxs-lookup"><span data-stu-id="88376-285">Client</span></span> | <span data-ttu-id="88376-286">支援</span><span class="sxs-lookup"><span data-stu-id="88376-286">Support</span></span> | <span data-ttu-id="88376-287">例外狀況</span><span class="sxs-lookup"><span data-stu-id="88376-287">Exceptions</span></span> |
| --- | --- | --- |
| <span data-ttu-id="88376-288">Web 用戶端，例如 Exchange Web Access 和 SharePoint Online</span><span class="sxs-lookup"><span data-stu-id="88376-288">Web-based clients such as Exchange Web Access and SharePoint Online</span></span> |<span data-ttu-id="88376-289">支援</span><span class="sxs-lookup"><span data-stu-id="88376-289">Supported</span></span> |<span data-ttu-id="88376-290">None</span><span class="sxs-lookup"><span data-stu-id="88376-290">None</span></span> |
| <span data-ttu-id="88376-291">豐富型用戶端應用程式，例如 Lync、Office 訂閱、CRM</span><span class="sxs-lookup"><span data-stu-id="88376-291">Rich client applications such as Lync, Office Subscription, CRM</span></span> |<span data-ttu-id="88376-292">支援</span><span class="sxs-lookup"><span data-stu-id="88376-292">Supported</span></span> |<span data-ttu-id="88376-293">None</span><span class="sxs-lookup"><span data-stu-id="88376-293">None</span></span> |
| <span data-ttu-id="88376-294">豐富型電子郵件用戶端，例如 Outlook 和 ActiveSync</span><span class="sxs-lookup"><span data-stu-id="88376-294">Email-rich clients such as Outlook and ActiveSync</span></span> |<span data-ttu-id="88376-295">支援</span><span class="sxs-lookup"><span data-stu-id="88376-295">Supported</span></span> |<span data-ttu-id="88376-296">None</span><span class="sxs-lookup"><span data-stu-id="88376-296">None</span></span> |

<span data-ttu-id="88376-297">如需 IBM Tivoli Federated Identity Manager 的詳細資訊，請參閱 [IBM Security Access Manager for Microsoft Applications](http://www-01.ibm.com/support/docview.wss?uid=swg24029517)。</span><span class="sxs-lookup"><span data-stu-id="88376-297">For more information about IBM Tivoli Federated Identity Manager, see [IBM Security Access Manager for Microsoft Applications](http://www-01.ibm.com/support/docview.wss?uid=swg24029517).</span></span>

## <a name="icewall-federation-version-30"></a><span data-ttu-id="88376-298">IceWall Federation Version 3.0</span><span class="sxs-lookup"><span data-stu-id="88376-298">IceWall Federation Version 3.0</span></span>

<span data-ttu-id="88376-299">以下是支援此單一登入體驗之矩陣的案例：</span><span class="sxs-lookup"><span data-stu-id="88376-299">The following is the scenario support matrix for this single sign-on experience:</span></span>

| <span data-ttu-id="88376-300">用戶端</span><span class="sxs-lookup"><span data-stu-id="88376-300">Client</span></span> | <span data-ttu-id="88376-301">支援</span><span class="sxs-lookup"><span data-stu-id="88376-301">Support</span></span> | <span data-ttu-id="88376-302">例外狀況</span><span class="sxs-lookup"><span data-stu-id="88376-302">Exceptions</span></span> |
| --- | --- | --- |
| <span data-ttu-id="88376-303">Web 用戶端，例如 Exchange Web Access 和 SharePoint Online</span><span class="sxs-lookup"><span data-stu-id="88376-303">Web-based clients such as Exchange Web Access and SharePoint Online</span></span> |<span data-ttu-id="88376-304">支援</span><span class="sxs-lookup"><span data-stu-id="88376-304">Supported</span></span> |<span data-ttu-id="88376-305">不支援整合式 Windows 驗證</span><span class="sxs-lookup"><span data-stu-id="88376-305">Integrated Windows Authentication is not supported</span></span> |
| <span data-ttu-id="88376-306">豐富型用戶端應用程式，例如 Lync、Office 訂閱、CRM</span><span class="sxs-lookup"><span data-stu-id="88376-306">Rich client applications such as Lync, Office Subscription, CRM</span></span> |<span data-ttu-id="88376-307">支援</span><span class="sxs-lookup"><span data-stu-id="88376-307">Supported</span></span> |<span data-ttu-id="88376-308">不支援整合式 Windows 驗證</span><span class="sxs-lookup"><span data-stu-id="88376-308">Integrated Windows Authentication is not supported</span></span> |
| <span data-ttu-id="88376-309">豐富型電子郵件用戶端，例如 Outlook 和 ActiveSync</span><span class="sxs-lookup"><span data-stu-id="88376-309">Email-rich clients such as Outlook and ActiveSync</span></span> |<span data-ttu-id="88376-310">支援</span><span class="sxs-lookup"><span data-stu-id="88376-310">Supported</span></span> |<span data-ttu-id="88376-311">None</span><span class="sxs-lookup"><span data-stu-id="88376-311">None</span></span> |

<span data-ttu-id="88376-312">如需 IceWall Federation 的詳細資訊，請參閱 [IceWall Federation 3.0 版](http://h50146.www5.hp.com/products/software/security/icewall/eng/federation/)和 [IceWall Federation (含 Office 365)](http://h50146.www5.hp.com/products/software/security/icewall/federation/office365.html)。</span><span class="sxs-lookup"><span data-stu-id="88376-312">For more information about IceWall Federation, see [IceWall Federation Version 3.0](http://h50146.www5.hp.com/products/software/security/icewall/eng/federation/) and [IceWall Federation with Office 365](http://h50146.www5.hp.com/products/software/security/icewall/federation/office365.html).</span></span>

## <a name="memority"></a><span data-ttu-id="88376-313">Memority</span><span class="sxs-lookup"><span data-stu-id="88376-313">Memority</span></span>

<span data-ttu-id="88376-314">以下是支援此登入體驗之矩陣的案例：</span><span class="sxs-lookup"><span data-stu-id="88376-314">The following is the scenario support matrix for this sign-on experience:</span></span> 

| <span data-ttu-id="88376-315">用戶端</span><span class="sxs-lookup"><span data-stu-id="88376-315">Client</span></span> | <span data-ttu-id="88376-316">支援</span><span class="sxs-lookup"><span data-stu-id="88376-316">Support</span></span> | <span data-ttu-id="88376-317">例外狀況</span><span class="sxs-lookup"><span data-stu-id="88376-317">Exceptions</span></span> |
| --- | --- | --- |
| <span data-ttu-id="88376-318">Web 用戶端，例如 Exchange Web Access 和 SharePoint Online</span><span class="sxs-lookup"><span data-stu-id="88376-318">Web-based clients such as Exchange Web Access and SharePoint Online</span></span> |<span data-ttu-id="88376-319">支援</span><span class="sxs-lookup"><span data-stu-id="88376-319">Supported</span></span> |<span data-ttu-id="88376-320">None</span><span class="sxs-lookup"><span data-stu-id="88376-320">None</span></span> |
| <span data-ttu-id="88376-321">豐富型用戶端應用程式，例如 Lync、Office 訂閱、CRM</span><span class="sxs-lookup"><span data-stu-id="88376-321">Rich client applications such as Lync, Office Subscription, CRM</span></span> |<span data-ttu-id="88376-322">支援</span><span class="sxs-lookup"><span data-stu-id="88376-322">Supported</span></span> |<span data-ttu-id="88376-323">None</span><span class="sxs-lookup"><span data-stu-id="88376-323">None</span></span> |
| <span data-ttu-id="88376-324">豐富型電子郵件用戶端，例如 Outlook 和 ActiveSync</span><span class="sxs-lookup"><span data-stu-id="88376-324">Email-rich clients such as Outlook and ActiveSync</span></span> |<span data-ttu-id="88376-325">支援</span><span class="sxs-lookup"><span data-stu-id="88376-325">Supported</span></span> |<span data-ttu-id="88376-326">None</span><span class="sxs-lookup"><span data-stu-id="88376-326">None</span></span> |

<span data-ttu-id="88376-327">如需使用 Memority 的詳細資訊，請參閱 [Memority](http://www.memority.com)。</span><span class="sxs-lookup"><span data-stu-id="88376-327">For more information about using Memority see [Memority](http://www.memority.com).</span></span>


## <a name="netiq-access-manager-4x"></a><span data-ttu-id="88376-328">NetIQ Access Manager 4.x</span><span class="sxs-lookup"><span data-stu-id="88376-328">NetIQ Access Manager 4.x</span></span>

<span data-ttu-id="88376-329">以下是支援此單一登入體驗之矩陣的案例：</span><span class="sxs-lookup"><span data-stu-id="88376-329">The following is the scenario support matrix for this single sign-on experience:</span></span>

| <span data-ttu-id="88376-330">用戶端</span><span class="sxs-lookup"><span data-stu-id="88376-330">Client</span></span> | <span data-ttu-id="88376-331">支援</span><span class="sxs-lookup"><span data-stu-id="88376-331">Support</span></span> | <span data-ttu-id="88376-332">例外狀況</span><span class="sxs-lookup"><span data-stu-id="88376-332">Exceptions</span></span> |
| --- | --- | --- |
| <span data-ttu-id="88376-333">Web 用戶端，例如 Exchange Web Access 和 SharePoint Online</span><span class="sxs-lookup"><span data-stu-id="88376-333">Web-based clients such as Exchange Web Access and SharePoint Online</span></span> |<span data-ttu-id="88376-334">支援</span><span class="sxs-lookup"><span data-stu-id="88376-334">Supported</span></span> |<span data-ttu-id="88376-335">None</span><span class="sxs-lookup"><span data-stu-id="88376-335">None</span></span>|
| <span data-ttu-id="88376-336">豐富型用戶端應用程式，例如 Lync、Office 訂閱、CRM</span><span class="sxs-lookup"><span data-stu-id="88376-336">Rich client applications such as Lync, Office Subscription, CRM</span></span> |<span data-ttu-id="88376-337">支援</span><span class="sxs-lookup"><span data-stu-id="88376-337">Supported</span></span> |<span data-ttu-id="88376-338">None</span><span class="sxs-lookup"><span data-stu-id="88376-338">None</span></span>|
| <span data-ttu-id="88376-339">豐富型電子郵件用戶端，例如 Outlook 和 ActiveSync</span><span class="sxs-lookup"><span data-stu-id="88376-339">Email-rich clients such as Outlook and ActiveSync</span></span> |<span data-ttu-id="88376-340">支援</span><span class="sxs-lookup"><span data-stu-id="88376-340">Supported</span></span> |<span data-ttu-id="88376-341">None</span><span class="sxs-lookup"><span data-stu-id="88376-341">None</span></span> |

<span data-ttu-id="88376-342">如需詳細資訊，請參閱 [NetIQ Access Manager](https://www.netiq.com/documentation/access-manager-43/admin/data/b65ogn0.html#b12iqp0m)。</span><span class="sxs-lookup"><span data-stu-id="88376-342">For more information, see [NetIQ Access Manager](https://www.netiq.com/documentation/access-manager-43/admin/data/b65ogn0.html#b12iqp0m).</span></span>

## <a name="okta"></a><span data-ttu-id="88376-343">Okta</span><span class="sxs-lookup"><span data-stu-id="88376-343">Okta</span></span>

<span data-ttu-id="88376-344">以下是支援此單一登入體驗之矩陣的案例：</span><span class="sxs-lookup"><span data-stu-id="88376-344">The following is the scenario support matrix for this single sign-on experience:</span></span> 

| <span data-ttu-id="88376-345">用戶端</span><span class="sxs-lookup"><span data-stu-id="88376-345">Client</span></span> | <span data-ttu-id="88376-346">支援</span><span class="sxs-lookup"><span data-stu-id="88376-346">Support</span></span> | <span data-ttu-id="88376-347">例外狀況</span><span class="sxs-lookup"><span data-stu-id="88376-347">Exceptions</span></span> |
| --- | --- | --- |
| <span data-ttu-id="88376-348">Web 用戶端，例如 Exchange Web Access 和 SharePoint Online</span><span class="sxs-lookup"><span data-stu-id="88376-348">Web-based clients such as Exchange Web Access and SharePoint Online</span></span> |<span data-ttu-id="88376-349">支援</span><span class="sxs-lookup"><span data-stu-id="88376-349">Supported</span></span> |<span data-ttu-id="88376-350">整合式 Windows 認證需要設定其他 Web 伺服器與 Okta 應用程式。</span><span class="sxs-lookup"><span data-stu-id="88376-350">Integrated Windows Authentication requires setup of additional web server and Okta application.</span></span> |
| <span data-ttu-id="88376-351">豐富型用戶端應用程式，例如 Lync、Office 訂閱、CRM</span><span class="sxs-lookup"><span data-stu-id="88376-351">Rich client applications such as Lync, Office Subscription, CRM</span></span> |<span data-ttu-id="88376-352">支援</span><span class="sxs-lookup"><span data-stu-id="88376-352">Supported</span></span> |<span data-ttu-id="88376-353">整合式 Windows 驗證</span><span class="sxs-lookup"><span data-stu-id="88376-353">Integrated Windows Authentication</span></span> |
| <span data-ttu-id="88376-354">豐富型電子郵件用戶端，例如 Outlook 和 ActiveSync</span><span class="sxs-lookup"><span data-stu-id="88376-354">Email-rich clients such as Outlook and ActiveSync</span></span> |<span data-ttu-id="88376-355">支援</span><span class="sxs-lookup"><span data-stu-id="88376-355">Supported</span></span> |<span data-ttu-id="88376-356">None</span><span class="sxs-lookup"><span data-stu-id="88376-356">None</span></span> |

<span data-ttu-id="88376-357">如需 Okta 的詳細資訊，請參閱 [Okta](https://www.okta.com/)。</span><span class="sxs-lookup"><span data-stu-id="88376-357">For more information about Okta, see [Okta](https://www.okta.com/).</span></span>

## <a name="onelogin"></a><span data-ttu-id="88376-358">OneLogin</span><span class="sxs-lookup"><span data-stu-id="88376-358">OneLogin</span></span>

<span data-ttu-id="88376-359">以下是支援此單一登入體驗之矩陣的案例：</span><span class="sxs-lookup"><span data-stu-id="88376-359">The following is the scenario support matrix for this single sign-on experience:</span></span> 

| <span data-ttu-id="88376-360">用戶端</span><span class="sxs-lookup"><span data-stu-id="88376-360">Client</span></span> | <span data-ttu-id="88376-361">支援</span><span class="sxs-lookup"><span data-stu-id="88376-361">Support</span></span> | <span data-ttu-id="88376-362">例外狀況</span><span class="sxs-lookup"><span data-stu-id="88376-362">Exceptions</span></span> |
| --- | --- | --- |
| <span data-ttu-id="88376-363">Web 用戶端，例如 Exchange Web Access 和 SharePoint Online</span><span class="sxs-lookup"><span data-stu-id="88376-363">Web-based clients such as Exchange Web Access and SharePoint Online</span></span> |<span data-ttu-id="88376-364">支援</span><span class="sxs-lookup"><span data-stu-id="88376-364">Supported</span></span> |<span data-ttu-id="88376-365">整合式 Windows 驗證</span><span class="sxs-lookup"><span data-stu-id="88376-365">Integrated Windows Authentication</span></span> |
| <span data-ttu-id="88376-366">豐富型用戶端應用程式，例如 Lync、Office 訂閱、CRM</span><span class="sxs-lookup"><span data-stu-id="88376-366">Rich client applications such as Lync, Office Subscription, CRM</span></span> |<span data-ttu-id="88376-367">支援</span><span class="sxs-lookup"><span data-stu-id="88376-367">Supported</span></span> |<span data-ttu-id="88376-368">整合式 Windows 驗證</span><span class="sxs-lookup"><span data-stu-id="88376-368">Integrated Windows Authentication</span></span> |
| <span data-ttu-id="88376-369">豐富型電子郵件用戶端，例如 Outlook 和 ActiveSync</span><span class="sxs-lookup"><span data-stu-id="88376-369">Email-rich clients such as Outlook and ActiveSync</span></span> |<span data-ttu-id="88376-370">支援</span><span class="sxs-lookup"><span data-stu-id="88376-370">Supported</span></span> |<span data-ttu-id="88376-371">None</span><span class="sxs-lookup"><span data-stu-id="88376-371">None</span></span> |

<span data-ttu-id="88376-372">如需 OneLogin 的詳細資訊，請參閱 [OneLogin](https://www.onelogin.com/)。</span><span class="sxs-lookup"><span data-stu-id="88376-372">For more information about OneLogin, see [OneLogin](https://www.onelogin.com/).</span></span>

## <a name="optimal-idm-virtual-identity-server-federation-services"></a><span data-ttu-id="88376-373">Optimal IDM Virtual Identity Server Federation Services</span><span class="sxs-lookup"><span data-stu-id="88376-373">Optimal IDM Virtual Identity Server Federation Services</span></span>

<span data-ttu-id="88376-374">以下是支援此單一登入體驗之矩陣的案例：</span><span class="sxs-lookup"><span data-stu-id="88376-374">The following is the scenario support matrix this single sign-on experience:</span></span>

| <span data-ttu-id="88376-375">用戶端</span><span class="sxs-lookup"><span data-stu-id="88376-375">Client</span></span> | <span data-ttu-id="88376-376">支援</span><span class="sxs-lookup"><span data-stu-id="88376-376">Support</span></span> | <span data-ttu-id="88376-377">例外狀況</span><span class="sxs-lookup"><span data-stu-id="88376-377">Exceptions</span></span> |
| --- | --- | --- |
| <span data-ttu-id="88376-378">Web 用戶端，例如 Exchange Web Access 和 SharePoint Online</span><span class="sxs-lookup"><span data-stu-id="88376-378">Web-based clients such as Exchange Web Access and SharePoint Online</span></span> |<span data-ttu-id="88376-379">支援</span><span class="sxs-lookup"><span data-stu-id="88376-379">Supported</span></span> |<span data-ttu-id="88376-380">None</span><span class="sxs-lookup"><span data-stu-id="88376-380">None</span></span> |
| <span data-ttu-id="88376-381">豐富型用戶端應用程式，例如 Lync、Office 訂閱、CRM</span><span class="sxs-lookup"><span data-stu-id="88376-381">Rich client applications such as Lync, Office Subscription, CRM</span></span> |<span data-ttu-id="88376-382">支援</span><span class="sxs-lookup"><span data-stu-id="88376-382">Supported</span></span> |<span data-ttu-id="88376-383">整合式 Windows 驗證</span><span class="sxs-lookup"><span data-stu-id="88376-383">Integrated Windows Authentication</span></span> |
| <span data-ttu-id="88376-384">豐富型電子郵件用戶端，例如 Outlook 和 ActiveSync</span><span class="sxs-lookup"><span data-stu-id="88376-384">Email-rich clients such as Outlook and ActiveSync</span></span> |<span data-ttu-id="88376-385">支援</span><span class="sxs-lookup"><span data-stu-id="88376-385">Supported</span></span> |

<span data-ttu-id="88376-386">如需用戶端存取原則的詳細資訊，請參閱[依據用戶端所在位置限制存取 Office 365 服務](https://technet.microsoft.com/library/hh526961.aspx)。</span><span class="sxs-lookup"><span data-stu-id="88376-386">For more information about client access polices see [Limiting Access to Office 365 Services Based on the Location of the Client](https://technet.microsoft.com/library/hh526961.aspx).</span></span>





## <a name="pingfederate-611-72-8x"></a><span data-ttu-id="88376-387">PingFederate 6.11, 7.2, 8.x</span><span class="sxs-lookup"><span data-stu-id="88376-387">PingFederate 6.11, 7.2, 8.x</span></span>

<span data-ttu-id="88376-388">以下是支援此單一登入體驗之矩陣的案例：</span><span class="sxs-lookup"><span data-stu-id="88376-388">The following is the scenario support matrix for this single sign-on experience:</span></span>

| <span data-ttu-id="88376-389">用戶端</span><span class="sxs-lookup"><span data-stu-id="88376-389">Client</span></span> | <span data-ttu-id="88376-390">支援</span><span class="sxs-lookup"><span data-stu-id="88376-390">Support</span></span> | <span data-ttu-id="88376-391">例外狀況</span><span class="sxs-lookup"><span data-stu-id="88376-391">Exceptions</span></span> |
| --- | --- | --- |
| <span data-ttu-id="88376-392">Web 用戶端，例如 Exchange Web Access 和 SharePoint Online</span><span class="sxs-lookup"><span data-stu-id="88376-392">Web-based clients such as Exchange Web Access and SharePoint Online</span></span> |<span data-ttu-id="88376-393">支援</span><span class="sxs-lookup"><span data-stu-id="88376-393">Supported</span></span> |<span data-ttu-id="88376-394">None</span><span class="sxs-lookup"><span data-stu-id="88376-394">None</span></span> |
| <span data-ttu-id="88376-395">豐富型用戶端應用程式，例如 Lync、Office 訂閱、CRM</span><span class="sxs-lookup"><span data-stu-id="88376-395">Rich client applications such as Lync, Office Subscription, CRM</span></span> |<span data-ttu-id="88376-396">支援</span><span class="sxs-lookup"><span data-stu-id="88376-396">Supported</span></span> |<span data-ttu-id="88376-397">None</span><span class="sxs-lookup"><span data-stu-id="88376-397">None</span></span> |
| <span data-ttu-id="88376-398">豐富型電子郵件用戶端，例如 Outlook 和 ActiveSync</span><span class="sxs-lookup"><span data-stu-id="88376-398">Email-rich clients such as Outlook and ActiveSync</span></span> |<span data-ttu-id="88376-399">支援</span><span class="sxs-lookup"><span data-stu-id="88376-399">Supported</span></span> |<span data-ttu-id="88376-400">None</span><span class="sxs-lookup"><span data-stu-id="88376-400">None</span></span> |

<span data-ttu-id="88376-401">如需有關如何設定此 STS 來為您的 Active Directory 使用者提供單一登入體驗的 PingFederate 指示，請參閱下列其中一項︰</span><span class="sxs-lookup"><span data-stu-id="88376-401">For the PingFederate instructions on how to configure this STS to provide the single sign-on experience to your Active Directory users, see one of the following:</span></span> 

- [<span data-ttu-id="88376-402">PingFederate 6.11</span><span class="sxs-lookup"><span data-stu-id="88376-402">PingFederate 6.11</span></span>](http://go.microsoft.com/fwlink/?LinkID=266321)
- [<span data-ttu-id="88376-403">PingFederate 7.2</span><span class="sxs-lookup"><span data-stu-id="88376-403">PingFederate 7.2</span></span>](http://documentation.pingidentity.com/display/PF72/PingFederate+7.2)
- [<span data-ttu-id="88376-404">PingFederate 8.x</span><span class="sxs-lookup"><span data-stu-id="88376-404">PingFederate 8.x</span></span>](http://documentation.pingidentity.com/display/PFS/SSO+to+Office+365+Introduction)

## <a name="radiantone-cfs-30"></a><span data-ttu-id="88376-405">RadiantOne CFS 3.0</span><span class="sxs-lookup"><span data-stu-id="88376-405">RadiantOne CFS 3.0</span></span>

<span data-ttu-id="88376-406">以下是支援此單一登入體驗之矩陣的案例：</span><span class="sxs-lookup"><span data-stu-id="88376-406">The following is the scenario support matrix for this single sign-on experience:</span></span> 

| <span data-ttu-id="88376-407">用戶端</span><span class="sxs-lookup"><span data-stu-id="88376-407">Client</span></span> | <span data-ttu-id="88376-408">支援</span><span class="sxs-lookup"><span data-stu-id="88376-408">Support</span></span> | <span data-ttu-id="88376-409">例外狀況</span><span class="sxs-lookup"><span data-stu-id="88376-409">Exceptions</span></span> |
| --- | --- | --- |
| <span data-ttu-id="88376-410">Web 用戶端，例如 Exchange Web Access 和 SharePoint Online</span><span class="sxs-lookup"><span data-stu-id="88376-410">Web-based clients such as Exchange Web Access and SharePoint Online</span></span> |<span data-ttu-id="88376-411">支援</span><span class="sxs-lookup"><span data-stu-id="88376-411">Supported</span></span> |<span data-ttu-id="88376-412">None</span><span class="sxs-lookup"><span data-stu-id="88376-412">None</span></span> |
| <span data-ttu-id="88376-413">豐富型用戶端應用程式，例如 Lync、Office 訂閱、CRM</span><span class="sxs-lookup"><span data-stu-id="88376-413">Rich client applications such as Lync, Office Subscription, CRM</span></span> |<span data-ttu-id="88376-414">支援</span><span class="sxs-lookup"><span data-stu-id="88376-414">Supported</span></span> |<span data-ttu-id="88376-415">整合式 Windows 驗證</span><span class="sxs-lookup"><span data-stu-id="88376-415">Integrated Windows Authentication</span></span> |
| <span data-ttu-id="88376-416">豐富型電子郵件用戶端，例如 Outlook 和 ActiveSync</span><span class="sxs-lookup"><span data-stu-id="88376-416">Email-rich clients such as Outlook and ActiveSync</span></span> |<span data-ttu-id="88376-417">支援</span><span class="sxs-lookup"><span data-stu-id="88376-417">Supported</span></span> |<span data-ttu-id="88376-418">None</span><span class="sxs-lookup"><span data-stu-id="88376-418">None</span></span> |

<span data-ttu-id="88376-419">如需 RadiantOne CFS 的詳細資訊，請參閱 [RadiantOne CFS](http://www.radiantlogic.com/products/radiantone-cfs/)。</span><span class="sxs-lookup"><span data-stu-id="88376-419">For more information about RadiantOne CFS, see [RadiantOne CFS](http://www.radiantlogic.com/products/radiantone-cfs/).</span></span>

## <a name="sailpoint-identitynow"></a><span data-ttu-id="88376-420">Sailpoint IdentityNow</span><span class="sxs-lookup"><span data-stu-id="88376-420">Sailpoint IdentityNow</span></span>

<span data-ttu-id="88376-421">以下是支援此單一登入體驗之矩陣的案例：</span><span class="sxs-lookup"><span data-stu-id="88376-421">The following is the scenario support matrix for this single sign-on experience:</span></span>

| <span data-ttu-id="88376-422">用戶端</span><span class="sxs-lookup"><span data-stu-id="88376-422">Client</span></span> | <span data-ttu-id="88376-423">支援</span><span class="sxs-lookup"><span data-stu-id="88376-423">Support</span></span> | <span data-ttu-id="88376-424">例外狀況</span><span class="sxs-lookup"><span data-stu-id="88376-424">Exceptions</span></span> |
| --- | --- | --- |
| <span data-ttu-id="88376-425">Web 用戶端，例如 Exchange Web Access 和 SharePoint Online</span><span class="sxs-lookup"><span data-stu-id="88376-425">Web-based clients such as Exchange Web Access and SharePoint Online</span></span> |<span data-ttu-id="88376-426">支援</span><span class="sxs-lookup"><span data-stu-id="88376-426">Supported</span></span> |<span data-ttu-id="88376-427">不支援整合式 Windows 驗證</span><span class="sxs-lookup"><span data-stu-id="88376-427">Integrated Windows Authentication is not supported</span></span> |
| <span data-ttu-id="88376-428">豐富型用戶端應用程式，例如 Lync、Office 訂閱、CRM</span><span class="sxs-lookup"><span data-stu-id="88376-428">Rich client applications such as Lync, Office Subscription, CRM</span></span> |<span data-ttu-id="88376-429">支援</span><span class="sxs-lookup"><span data-stu-id="88376-429">Supported</span></span> |<span data-ttu-id="88376-430">不支援整合式 Windows 驗證</span><span class="sxs-lookup"><span data-stu-id="88376-430">Integrated Windows Authentication is not supported</span></span> |
| <span data-ttu-id="88376-431">豐富型電子郵件用戶端，例如 Outlook 和 ActiveSync</span><span class="sxs-lookup"><span data-stu-id="88376-431">Email-rich clients such as Outlook and ActiveSync</span></span> |<span data-ttu-id="88376-432">支援</span><span class="sxs-lookup"><span data-stu-id="88376-432">Supported</span></span> |<span data-ttu-id="88376-433">None</span><span class="sxs-lookup"><span data-stu-id="88376-433">None</span></span> |

<span data-ttu-id="88376-434">如需詳細資訊，請參閱 [Sailpoint IdentityNow](https://www.sailpoint.com/idaas-identity-as-a-service-identitynow/)。</span><span class="sxs-lookup"><span data-stu-id="88376-434">For more information, see [Sailpoint IdentityNow](https://www.sailpoint.com/idaas-identity-as-a-service-identitynow/).</span></span>

## <a name="secureauth-idp-720"></a><span data-ttu-id="88376-435">SecureAuth IdP 7.2.0</span><span class="sxs-lookup"><span data-stu-id="88376-435">SecureAuth IdP 7.2.0</span></span>

<span data-ttu-id="88376-436">以下是支援此單一登入體驗之矩陣的案例：</span><span class="sxs-lookup"><span data-stu-id="88376-436">The following is the scenario support matrix for this single sign-on experience:</span></span> 

| <span data-ttu-id="88376-437">用戶端</span><span class="sxs-lookup"><span data-stu-id="88376-437">Client</span></span> | <span data-ttu-id="88376-438">支援</span><span class="sxs-lookup"><span data-stu-id="88376-438">Support</span></span> | <span data-ttu-id="88376-439">例外狀況</span><span class="sxs-lookup"><span data-stu-id="88376-439">Exceptions</span></span> |
| --- | --- | --- |
| <span data-ttu-id="88376-440">Web 用戶端，例如 Exchange Web Access 和 SharePoint Online</span><span class="sxs-lookup"><span data-stu-id="88376-440">Web-based clients such as Exchange Web Access and SharePoint Online</span></span> |<span data-ttu-id="88376-441">支援</span><span class="sxs-lookup"><span data-stu-id="88376-441">Supported</span></span> |<span data-ttu-id="88376-442">None</span><span class="sxs-lookup"><span data-stu-id="88376-442">None</span></span> |
| <span data-ttu-id="88376-443">豐富型用戶端應用程式，例如 Lync、Office 訂閱、CRM</span><span class="sxs-lookup"><span data-stu-id="88376-443">Rich client applications such as Lync, Office Subscription, CRM</span></span> |<span data-ttu-id="88376-444">支援</span><span class="sxs-lookup"><span data-stu-id="88376-444">Supported</span></span> |<span data-ttu-id="88376-445">None</span><span class="sxs-lookup"><span data-stu-id="88376-445">None</span></span> |
| <span data-ttu-id="88376-446">豐富型電子郵件用戶端，例如 Outlook 和 ActiveSync</span><span class="sxs-lookup"><span data-stu-id="88376-446">Email-rich clients such as Outlook and ActiveSync</span></span> |<span data-ttu-id="88376-447">支援</span><span class="sxs-lookup"><span data-stu-id="88376-447">Supported</span></span> |<span data-ttu-id="88376-448">None</span><span class="sxs-lookup"><span data-stu-id="88376-448">None</span></span> |

<span data-ttu-id="88376-449">如需 SecureAuth 的相關詳細資訊，請參閱 [SecureAuth IdP](http://go.microsoft.com/?linkid=9845293)。</span><span class="sxs-lookup"><span data-stu-id="88376-449">For more information about SecureAuth, see [SecureAuth IdP](http://go.microsoft.com/?linkid=9845293).</span></span>














## <a name="signgo-53"></a><span data-ttu-id="88376-450">Sign&go 5.3</span><span class="sxs-lookup"><span data-stu-id="88376-450">Sign&go 5.3</span></span>

<span data-ttu-id="88376-451">以下是支援此單一登入體驗之矩陣的案例：</span><span class="sxs-lookup"><span data-stu-id="88376-451">The following is the scenario support matrix for this single sign-on experience:</span></span>

| <span data-ttu-id="88376-452">用戶端</span><span class="sxs-lookup"><span data-stu-id="88376-452">Client</span></span> | <span data-ttu-id="88376-453">支援</span><span class="sxs-lookup"><span data-stu-id="88376-453">Support</span></span> | <span data-ttu-id="88376-454">例外狀況</span><span class="sxs-lookup"><span data-stu-id="88376-454">Exceptions</span></span> |
| --- | --- | --- |
| <span data-ttu-id="88376-455">Web 用戶端，例如 Exchange Web Access 和 SharePoint Online</span><span class="sxs-lookup"><span data-stu-id="88376-455">Web-based clients such as Exchange Web Access and SharePoint Online</span></span> |<span data-ttu-id="88376-456">支援</span><span class="sxs-lookup"><span data-stu-id="88376-456">Supported</span></span> |<span data-ttu-id="88376-457">支援 Kerberos Contract</span><span class="sxs-lookup"><span data-stu-id="88376-457">Kerberos Contracts supported</span></span> |
| <span data-ttu-id="88376-458">豐富型用戶端應用程式，例如 Lync、Office 訂閱、CRM</span><span class="sxs-lookup"><span data-stu-id="88376-458">Rich client applications such as Lync, Office Subscription, CRM</span></span> |<span data-ttu-id="88376-459">支援</span><span class="sxs-lookup"><span data-stu-id="88376-459">Supported</span></span> |<span data-ttu-id="88376-460">None</span><span class="sxs-lookup"><span data-stu-id="88376-460">None</span></span> |
| <span data-ttu-id="88376-461">豐富型電子郵件用戶端，例如 Outlook 和 ActiveSync</span><span class="sxs-lookup"><span data-stu-id="88376-461">Email-rich clients such as Outlook and ActiveSync</span></span> |<span data-ttu-id="88376-462">支援</span><span class="sxs-lookup"><span data-stu-id="88376-462">Supported</span></span> |<span data-ttu-id="88376-463">None</span><span class="sxs-lookup"><span data-stu-id="88376-463">None</span></span> |

<span data-ttu-id="88376-464">Sign&go 5.3 透過 Kerberos Contract 的組態支援 Kerberos 驗證。</span><span class="sxs-lookup"><span data-stu-id="88376-464">Sign&go 5.3 supports Kerberos authentication via configuration of a Kerberos Contract.</span></span>  <span data-ttu-id="88376-465">如需此設定的協助，請連絡 Ilex 或檢視設定指南 [Sign&go](http://www.ilex-international.com/docs/sign&go_wsfederation_en.pdf)。</span><span class="sxs-lookup"><span data-stu-id="88376-465">For assistance with this configuration, please contact Ilex or view the setup guide [Sign&go](http://www.ilex-international.com/docs/sign&go_wsfederation_en.pdf)</span></span>

## <a name="softbank-technology-online-service-gate"></a><span data-ttu-id="88376-466">SoftBank Technology Online Service Gate</span><span class="sxs-lookup"><span data-stu-id="88376-466">SoftBank Technology Online Service Gate</span></span>

<span data-ttu-id="88376-467">以下是支援此單一登入體驗之矩陣的案例：</span><span class="sxs-lookup"><span data-stu-id="88376-467">The following is the scenario support matrix for this single sign-on experience:</span></span>

| <span data-ttu-id="88376-468">用戶端</span><span class="sxs-lookup"><span data-stu-id="88376-468">Client</span></span> | <span data-ttu-id="88376-469">支援</span><span class="sxs-lookup"><span data-stu-id="88376-469">Support</span></span> | <span data-ttu-id="88376-470">例外狀況</span><span class="sxs-lookup"><span data-stu-id="88376-470">Exceptions</span></span> |
| --- | --- | --- |
| <span data-ttu-id="88376-471">Web 用戶端，例如 Exchange Web Access 和 SharePoint Online</span><span class="sxs-lookup"><span data-stu-id="88376-471">Web-based clients such as Exchange Web Access and SharePoint Online</span></span> |<span data-ttu-id="88376-472">支援</span><span class="sxs-lookup"><span data-stu-id="88376-472">Supported</span></span> |<span data-ttu-id="88376-473">不支援整合式 Windows 驗證</span><span class="sxs-lookup"><span data-stu-id="88376-473">Integrated Windows Authentication is not supported</span></span> |
| <span data-ttu-id="88376-474">豐富型用戶端應用程式，例如 Lync、Office 訂閱、CRM</span><span class="sxs-lookup"><span data-stu-id="88376-474">Rich client applications such as Lync, Office Subscription, CRM</span></span> |<span data-ttu-id="88376-475">支援</span><span class="sxs-lookup"><span data-stu-id="88376-475">Supported</span></span> |<span data-ttu-id="88376-476">不支援整合式 Windows 驗證</span><span class="sxs-lookup"><span data-stu-id="88376-476">Integrated Windows Authentication is not supported</span></span> |
| <span data-ttu-id="88376-477">豐富型電子郵件用戶端，例如 Outlook 和 ActiveSync</span><span class="sxs-lookup"><span data-stu-id="88376-477">Email-rich clients such as Outlook and ActiveSync</span></span> |<span data-ttu-id="88376-478">支援</span><span class="sxs-lookup"><span data-stu-id="88376-478">Supported</span></span> |<span data-ttu-id="88376-479">None</span><span class="sxs-lookup"><span data-stu-id="88376-479">None</span></span> |

<span data-ttu-id="88376-480">如需 SoftBank Technology Online Service Gate 的詳細資訊，請參閱 [Softbank](https://www.softbanktech.jp/service/list/osg-pro-ent/)。</span><span class="sxs-lookup"><span data-stu-id="88376-480">For more information about SoftBank Technology Online Service Gate see [Softbank](https://www.softbanktech.jp/service/list/osg-pro-ent/)</span></span>

## <a name="vmware-workspace-one"></a><span data-ttu-id="88376-481">VMware Workspace One</span><span class="sxs-lookup"><span data-stu-id="88376-481">VMware Workspace One</span></span>

<span data-ttu-id="88376-482">以下是支援此單一登入體驗之矩陣的案例：</span><span class="sxs-lookup"><span data-stu-id="88376-482">The following is the scenario support matrix for this single sign-on experience:</span></span>

| <span data-ttu-id="88376-483">用戶端</span><span class="sxs-lookup"><span data-stu-id="88376-483">Client</span></span> | <span data-ttu-id="88376-484">支援</span><span class="sxs-lookup"><span data-stu-id="88376-484">Support</span></span> | <span data-ttu-id="88376-485">例外狀況</span><span class="sxs-lookup"><span data-stu-id="88376-485">Exceptions</span></span> |
| --- | --- | --- |
| <span data-ttu-id="88376-486">Web 用戶端，例如 Exchange Web Access 和 SharePoint Online</span><span class="sxs-lookup"><span data-stu-id="88376-486">Web-based clients such as Exchange Web Access and SharePoint Online</span></span> |<span data-ttu-id="88376-487">支援</span><span class="sxs-lookup"><span data-stu-id="88376-487">Supported</span></span> |<span data-ttu-id="88376-488">不支援整合式 Windows 驗證</span><span class="sxs-lookup"><span data-stu-id="88376-488">Integrated Windows Authentication is not supported</span></span> |
| <span data-ttu-id="88376-489">豐富型用戶端應用程式，例如 Lync、Office 訂閱、CRM</span><span class="sxs-lookup"><span data-stu-id="88376-489">Rich client applications such as Lync, Office Subscription, CRM</span></span> |<span data-ttu-id="88376-490">支援</span><span class="sxs-lookup"><span data-stu-id="88376-490">Supported</span></span> |<span data-ttu-id="88376-491">不支援整合式 Windows 驗證</span><span class="sxs-lookup"><span data-stu-id="88376-491">Integrated Windows Authentication is not supported</span></span> |
| <span data-ttu-id="88376-492">豐富型電子郵件用戶端，例如 Outlook 和 ActiveSync</span><span class="sxs-lookup"><span data-stu-id="88376-492">Email-rich clients such as Outlook and ActiveSync</span></span> |<span data-ttu-id="88376-493">支援</span><span class="sxs-lookup"><span data-stu-id="88376-493">Supported</span></span> |<span data-ttu-id="88376-494">None</span><span class="sxs-lookup"><span data-stu-id="88376-494">None</span></span> |

<span data-ttu-id="88376-495">如需詳細資訊，請參閱 [VMware Workspace One](http://www.vmware.com/pdf/vidm-office365-saml.pdf)。</span><span class="sxs-lookup"><span data-stu-id="88376-495">For more information about see [VMware Workspace One](http://www.vmware.com/pdf/vidm-office365-saml.pdf)</span></span>

