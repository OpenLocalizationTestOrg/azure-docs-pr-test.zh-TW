---
title: "aaaAzure AD 同盟相容性清單"
description: "此頁面具有非 Microsoft 可以使用的 tooimplement 的身分識別提供者單一登入。"
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
ms.openlocfilehash: ac2f9ad324c8ca6b587b73ea465426ad6b074b03
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-federation-compatibility-list"></a><span data-ttu-id="8d2b2-103">Azure AD 同盟相容性清單</span><span class="sxs-lookup"><span data-stu-id="8d2b2-103">Azure AD federation compatibility list</span></span>
<span data-ttu-id="8d2b2-104">Azure Active Directory 在不需要任何非 Microsoft 解決方案的情況下，針對 Office 365 和混合式與僅限雲端實作的其他 Microsoft 線上服務，提供單一登入和增強的應用程式存取安全性。</span><span class="sxs-lookup"><span data-stu-id="8d2b2-104">Azure Active Directory provides single-sign on and enhanced application access security for Office 365 and other Microsoft Online services for hybrid and cloud-only implementations without requiring any non-Microsoft solution.</span></span> <span data-ttu-id="8d2b2-105">Office 365，就像大部分 Microsoft 線上服務一樣，已經與 Azure Active Directory 整合以提供目錄服務、驗證及授權。</span><span class="sxs-lookup"><span data-stu-id="8d2b2-105">Office 365, like most of Microsoft’s Online services, is integrated with Azure Active Directory for directory services, authentication and authorization.</span></span> <span data-ttu-id="8d2b2-106">Azure Active Directory 也提供 SaaS 應用程式的單一登入 toothousands 和內部部署 web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="8d2b2-106">Azure Active Directory also provides single sign-on toothousands of SaaS applications and on-premises web applications.</span></span> <span data-ttu-id="8d2b2-107">請參閱支援的 SaaS 應用程式的 hello Azure Active Directory 應用程式庫。</span><span class="sxs-lookup"><span data-stu-id="8d2b2-107">Please see hello Azure Active Directory application gallery for supported SaaS applications.</span></span>

<span data-ttu-id="8d2b2-108">對於有投資在非 Microsoft 同盟解決方案的組織而言，本主題包含設定單一登入 Windows Server Active Directory 使用者與 Microsoft Online services 使用非 Microsoft 的身分識別提供者的指引從 hello 「 Azure Active Directory 同盟相容性清單 」 底下。</span><span class="sxs-lookup"><span data-stu-id="8d2b2-108">For organizations that have invested in non-Microsoft federation solutions, this topic contains guidance for configuring single sign-on for their Windows Server Active Directory users with Microsoft Online services by using non-Microsoft identity providers from hello “Azure Active Directory federation compatibility list” below.</span></span> 

![](./media/active-directory-aadconnect-federation-compatibility/oxford2.jpg)   
<span data-ttu-id="8d2b2-109">[Oxford Computer Group](http://oxfordcomputergroup.com/)這家代表 Microsoft 的協力廠商已使用非 Microsoft 識別提供者，針對一組常見的 Azure Active Directory 使用案例測試這些單一登入體驗。</span><span class="sxs-lookup"><span data-stu-id="8d2b2-109">[Oxford Computer Group](http://oxfordcomputergroup.com/), a third-party, on behalf of Microsoft, tested these single sign-on experiences using non-Microsoft identity providers against a set of use cases common with Azure Active Directory.</span></span>

<span data-ttu-id="8d2b2-110">如需如何取得此處所列的協力廠商識別提供者資訊，請與 Oxford Computer Group 連絡： [idp@oxfordcomputergroup.com](mailto:idp@oxfordcomputergroup.com)。</span><span class="sxs-lookup"><span data-stu-id="8d2b2-110">For information on how you can get your third-party identity provider listed here, contact Oxford Computer Group at [idp@oxfordcomputergroup.com](mailto:idp@oxfordcomputergroup.com).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="8d2b2-111">Oxford 電腦群組測試僅 hello 同盟功能這些單一登入案例。</span><span class="sxs-lookup"><span data-stu-id="8d2b2-111">Oxford Computer Group tested only hello federation functionality of these single sign-on scenarios.</span></span> <span data-ttu-id="8d2b2-112">Oxford 電腦群組並未執行任何測試 hello 同步處理、 雙因素驗證等元件的這些單一登入案例。</span><span class="sxs-lookup"><span data-stu-id="8d2b2-112">Oxford Computer Group did not perform any testing of hello synchronization, two-factor authentication, etc. components of these single sign-on scenarios.</span></span>
> 
> <span data-ttu-id="8d2b2-113">這項計畫亦未測試 tooUPN 替代識別碼登入使用。</span><span class="sxs-lookup"><span data-stu-id="8d2b2-113">Use of Sign-in by Alternate ID tooUPN is also not tested in this program.</span></span>
> 
> 

* [<span data-ttu-id="8d2b2-114">Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="8d2b2-114">Azure Active Directory</span></span>](#azure-active-directory)
* [<span data-ttu-id="8d2b2-115">AuthAnvil Single Sign On 4.5</span><span class="sxs-lookup"><span data-stu-id="8d2b2-115">AuthAnvil Single Sign On 4.5</span></span>](#authanvil-single-sign-on-45)
* [<span data-ttu-id="8d2b2-116">BIG-IP with Access Policy Manager BIG-IP ver.11.3x – 11.6x</span><span class="sxs-lookup"><span data-stu-id="8d2b2-116">BIG-IP with Access Policy Manager BIG-IP ver. 11.3x – 11.6x</span></span>](#big-ip-with-access-policy-manager-big-ip-ver-113x--116x) 
* [<span data-ttu-id="8d2b2-117">BitGlass</span><span class="sxs-lookup"><span data-stu-id="8d2b2-117">BitGlass</span></span>](#bitglass)
* [<span data-ttu-id="8d2b2-118">CA Secure Cloud</span><span class="sxs-lookup"><span data-stu-id="8d2b2-118">CA Secure Cloud</span></span>](#ca-secure-cloud) 
* [<span data-ttu-id="8d2b2-119">CA SiteMinder 12.52</span><span class="sxs-lookup"><span data-stu-id="8d2b2-119">CA SiteMinder 12.52</span></span>](#ca-siteminder-1252-sp1-cumulative-release-4) 
* [<span data-ttu-id="8d2b2-120">Centrify</span><span class="sxs-lookup"><span data-stu-id="8d2b2-120">Centrify</span></span>](#centrify) 
* [<span data-ttu-id="8d2b2-121">Dell One Identity Cloud Access Manager v7.1</span><span class="sxs-lookup"><span data-stu-id="8d2b2-121">Dell One Identity Cloud Access Manager v7.1</span></span>](#dell-one-identity-cloud-access-manager-v71) 
* [<span data-ttu-id="8d2b2-122">DigitalPersona Composite 驗證</span><span class="sxs-lookup"><span data-stu-id="8d2b2-122">DigitalPersona Composite Authentication</span></span>](#digitalpersona-composite-authentication)
* [<span data-ttu-id="8d2b2-123">IBM Tivoli Federated Identity Manager 6.2.2</span><span class="sxs-lookup"><span data-stu-id="8d2b2-123">IBM Tivoli Federated Identity Manager 6.2.2</span></span>](#ibm-tivoli-federated-identity-manager-622) 
* [<span data-ttu-id="8d2b2-124">IceWall Federation Version 3.0</span><span class="sxs-lookup"><span data-stu-id="8d2b2-124">IceWall Federation Version 3.0</span></span>](#icewall-federation-version-30) 
* [<span data-ttu-id="8d2b2-125">Memority</span><span class="sxs-lookup"><span data-stu-id="8d2b2-125">Memority</span></span>](#memority)
* [<span data-ttu-id="8d2b2-126">NetIQ Access Manager 4.x</span><span class="sxs-lookup"><span data-stu-id="8d2b2-126">NetIQ Access Manager 4.x</span></span>](#netiq-access-manager-4x) 
* [<span data-ttu-id="8d2b2-127">Okta</span><span class="sxs-lookup"><span data-stu-id="8d2b2-127">Okta</span></span>](#okta) 
* [<span data-ttu-id="8d2b2-128">OneLogin</span><span class="sxs-lookup"><span data-stu-id="8d2b2-128">OneLogin</span></span>](#onelogin) 
* [<span data-ttu-id="8d2b2-129">Optimal IDM Virtual Identity Server Federation Services</span><span class="sxs-lookup"><span data-stu-id="8d2b2-129">Optimal IDM Virtual Identity Server Federation Services</span></span>](#optimal-idm-virtual-identity-server-federation-services) 
* [<span data-ttu-id="8d2b2-130">PingFederate 6.11, 7.2, 8.x</span><span class="sxs-lookup"><span data-stu-id="8d2b2-130">PingFederate 6.11, 7.2, 8.x</span></span>](#pingfederate-611-72-8x)
* [<span data-ttu-id="8d2b2-131">RadiantOne CFS 3.0</span><span class="sxs-lookup"><span data-stu-id="8d2b2-131">RadiantOne CFS 3.0</span></span>](#radiantone-cfs-30) 
* [<span data-ttu-id="8d2b2-132">Sailpoint IdentityNow</span><span class="sxs-lookup"><span data-stu-id="8d2b2-132">Sailpoint IdentityNow</span></span>](#sailpoint-identitynow)
* [<span data-ttu-id="8d2b2-133">SecureAuth IdP 7.2.0</span><span class="sxs-lookup"><span data-stu-id="8d2b2-133">SecureAuth IdP 7.2.0</span></span>](#secureauth-idp-720) 
* [<span data-ttu-id="8d2b2-134">Sign&go 5.3</span><span class="sxs-lookup"><span data-stu-id="8d2b2-134">Sign&go 5.3</span></span>](#signgo-53) 
* [<span data-ttu-id="8d2b2-135">SoftBank Technology Online Service Gate</span><span class="sxs-lookup"><span data-stu-id="8d2b2-135">SoftBank Technology Online Service Gate</span></span>](#softbank)
* [<span data-ttu-id="8d2b2-136">VMware Workspace One</span><span class="sxs-lookup"><span data-stu-id="8d2b2-136">VMware Workspace One</span></span>](#vmware-workspace-one)



> [!IMPORTANT]
> <span data-ttu-id="8d2b2-137">因為這些是第三方產品，Microsoft 不提供支援 hello 部署、 設定、 疑難排解、 最佳作法，等問題和這些身分識別提供者有關的問題。</span><span class="sxs-lookup"><span data-stu-id="8d2b2-137">Since these are third-party products, Microsoft does not provide support for hello deployment, configuration, troubleshooting, best practices, etc. issues and questions regarding these identity providers.</span></span> <span data-ttu-id="8d2b2-138">如需支援和這些身分識別提供者有關的問題，請直接連絡 hello 支援第三方。</span><span class="sxs-lookup"><span data-stu-id="8d2b2-138">For support and questions regarding these identity providers, contact hello supported third-parties directly.</span></span>
> 
> <span data-ttu-id="8d2b2-139">這些協力廠商識別提供者僅使用 WS-同盟與 WS-Trust 通訊協定，針對與 Microsoft 雲端服務的互通性進行測試。</span><span class="sxs-lookup"><span data-stu-id="8d2b2-139">These third-party identity providers were tested for interoperability with Microsoft cloud services using WS-Federation and WS-Trust protocols only.</span></span> <span data-ttu-id="8d2b2-140">測試不包括使用 hello SAML 通訊協定。</span><span class="sxs-lookup"><span data-stu-id="8d2b2-140">Testing did not include using hello SAML protocol.</span></span>
> 


## <a name="azure-active-directory"></a><span data-ttu-id="8d2b2-141">Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="8d2b2-141">Azure Active Directory</span></span>

<span data-ttu-id="8d2b2-142">hello 下面是此登入體驗的 hello 案例支援矩陣：</span><span class="sxs-lookup"><span data-stu-id="8d2b2-142">hello following is hello scenario support matrix for this sign-on experience:</span></span> 

| <span data-ttu-id="8d2b2-143">用戶端</span><span class="sxs-lookup"><span data-stu-id="8d2b2-143">Client</span></span> | <span data-ttu-id="8d2b2-144">支援</span><span class="sxs-lookup"><span data-stu-id="8d2b2-144">Support</span></span> | <span data-ttu-id="8d2b2-145">例外狀況</span><span class="sxs-lookup"><span data-stu-id="8d2b2-145">Exceptions</span></span> |
| --- | --- | --- |
| <span data-ttu-id="8d2b2-146">Web 用戶端，例如 Exchange Web Access 和 SharePoint Online</span><span class="sxs-lookup"><span data-stu-id="8d2b2-146">Web-based clients such as Exchange Web Access and SharePoint Online</span></span> |<span data-ttu-id="8d2b2-147">支援</span><span class="sxs-lookup"><span data-stu-id="8d2b2-147">Supported</span></span> |<span data-ttu-id="8d2b2-148">None</span><span class="sxs-lookup"><span data-stu-id="8d2b2-148">None</span></span> |
| <span data-ttu-id="8d2b2-149">豐富型用戶端應用程式，例如 Lync、Office 訂閱、CRM</span><span class="sxs-lookup"><span data-stu-id="8d2b2-149">Rich client applications such as Lync, Office Subscription, CRM</span></span> |<span data-ttu-id="8d2b2-150">支援</span><span class="sxs-lookup"><span data-stu-id="8d2b2-150">Supported</span></span> |<span data-ttu-id="8d2b2-151">None</span><span class="sxs-lookup"><span data-stu-id="8d2b2-151">None</span></span> |
| <span data-ttu-id="8d2b2-152">豐富型電子郵件用戶端，例如 Outlook 和 ActiveSync</span><span class="sxs-lookup"><span data-stu-id="8d2b2-152">Email-rich clients such as Outlook and ActiveSync</span></span> |<span data-ttu-id="8d2b2-153">支援</span><span class="sxs-lookup"><span data-stu-id="8d2b2-153">Supported</span></span> |<span data-ttu-id="8d2b2-154">None</span><span class="sxs-lookup"><span data-stu-id="8d2b2-154">None</span></span> |
| <span data-ttu-id="8d2b2-155">使用 ADAL 的現代應用程式，例如 Office 2016</span><span class="sxs-lookup"><span data-stu-id="8d2b2-155">Modern Applications using ADAL such as Office 2016</span></span> |<span data-ttu-id="8d2b2-156">支援</span><span class="sxs-lookup"><span data-stu-id="8d2b2-156">Supported</span></span> |<span data-ttu-id="8d2b2-157">None</span><span class="sxs-lookup"><span data-stu-id="8d2b2-157">None</span></span> |

<span data-ttu-id="8d2b2-158">如需搭配使用 Azure Active Directory 與 AD FS 的詳細資訊，請參閱 [Active Directory 同盟服務 (ADFS)](active-directory-aadconnect-get-started-custom.md#configuring-federation-with-ad-fs)。</span><span class="sxs-lookup"><span data-stu-id="8d2b2-158">For more information about using Azure Active Directory with AD FS see [Active Directory Federation Services (ADFS)](active-directory-aadconnect-get-started-custom.md#configuring-federation-with-ad-fs).</span></span>

<span data-ttu-id="8d2b2-159">如需搭配密碼同步使用 Azure Active Directory 的相關詳細資訊，請參閱 [Azure AD Connect](active-directory-aadconnect.md)。</span><span class="sxs-lookup"><span data-stu-id="8d2b2-159">For more information about using Azure Active Directory with Password sync see [Azure AD Connect](active-directory-aadconnect.md).</span></span>

## <a name="authanvil-single-sign-on-45"></a><span data-ttu-id="8d2b2-160">AuthAnvil Single Sign On 4.5</span><span class="sxs-lookup"><span data-stu-id="8d2b2-160">AuthAnvil Single Sign On 4.5</span></span>

<span data-ttu-id="8d2b2-161">hello 下面是此單一登入體驗的 hello 案例支援矩陣：</span><span class="sxs-lookup"><span data-stu-id="8d2b2-161">hello following is hello scenario support matrix for this single sign-on experience:</span></span>

| <span data-ttu-id="8d2b2-162">用戶端</span><span class="sxs-lookup"><span data-stu-id="8d2b2-162">Client</span></span> | <span data-ttu-id="8d2b2-163">支援</span><span class="sxs-lookup"><span data-stu-id="8d2b2-163">Support</span></span> | <span data-ttu-id="8d2b2-164">例外狀況</span><span class="sxs-lookup"><span data-stu-id="8d2b2-164">Exceptions</span></span> |
| --- | --- | --- |
| <span data-ttu-id="8d2b2-165">Web 用戶端，例如 Exchange Web Access 和 SharePoint Online</span><span class="sxs-lookup"><span data-stu-id="8d2b2-165">Web-based clients such as Exchange Web Access and SharePoint Online</span></span> |<span data-ttu-id="8d2b2-166">支援</span><span class="sxs-lookup"><span data-stu-id="8d2b2-166">Supported</span></span> |<span data-ttu-id="8d2b2-167">不支援整合式 Windows 驗證</span><span class="sxs-lookup"><span data-stu-id="8d2b2-167">Integrated Windows Authentication is not supported</span></span> |
| <span data-ttu-id="8d2b2-168">豐富型用戶端應用程式，例如 Lync、Office 訂閱、CRM</span><span class="sxs-lookup"><span data-stu-id="8d2b2-168">Rich client applications such as Lync, Office Subscription, CRM</span></span> |<span data-ttu-id="8d2b2-169">支援</span><span class="sxs-lookup"><span data-stu-id="8d2b2-169">Supported</span></span> |<span data-ttu-id="8d2b2-170">不支援整合式 Windows 驗證</span><span class="sxs-lookup"><span data-stu-id="8d2b2-170">Integrated Windows Authentication is not supported</span></span> |
| <span data-ttu-id="8d2b2-171">豐富型電子郵件用戶端，例如 Outlook 和 ActiveSync</span><span class="sxs-lookup"><span data-stu-id="8d2b2-171">Email-rich clients such as Outlook and ActiveSync</span></span> |<span data-ttu-id="8d2b2-172">支援</span><span class="sxs-lookup"><span data-stu-id="8d2b2-172">Supported</span></span> |<span data-ttu-id="8d2b2-173">None</span><span class="sxs-lookup"><span data-stu-id="8d2b2-173">None</span></span> |

<span data-ttu-id="8d2b2-174">如需詳細資訊，請參閱 [AuthAnvil 單一登入](https://help.scorpionsoft.com/entries/26538603-How-can-I-Configure-Single-Sign-On-for-Office-365-)。</span><span class="sxs-lookup"><span data-stu-id="8d2b2-174">For more information, see [AuthAnvil Single Sign On.](https://help.scorpionsoft.com/entries/26538603-How-can-I-Configure-Single-Sign-On-for-Office-365-).</span></span>


## <a name="big-ip-with-access-policy-manager-big-ip-ver-113x--116x"></a><span data-ttu-id="8d2b2-175">BIG-IP with Access Policy Manager BIG-IP ver.</span><span class="sxs-lookup"><span data-stu-id="8d2b2-175">BIG-IP with Access Policy Manager BIG-IP ver.</span></span> <span data-ttu-id="8d2b2-176">11.3x – 11.6x</span><span class="sxs-lookup"><span data-stu-id="8d2b2-176">11.3x – 11.6x</span></span>

<span data-ttu-id="8d2b2-177">hello 下面是此單一登入體驗的 hello 案例支援矩陣：</span><span class="sxs-lookup"><span data-stu-id="8d2b2-177">hello following is hello scenario support matrix for this single sign-on experience:</span></span> 

| <span data-ttu-id="8d2b2-178">用戶端</span><span class="sxs-lookup"><span data-stu-id="8d2b2-178">Client</span></span> | <span data-ttu-id="8d2b2-179">支援</span><span class="sxs-lookup"><span data-stu-id="8d2b2-179">Support</span></span> | <span data-ttu-id="8d2b2-180">例外狀況</span><span class="sxs-lookup"><span data-stu-id="8d2b2-180">Exceptions</span></span> |
| --- | --- | --- |
| <span data-ttu-id="8d2b2-181">Web 用戶端，例如 Exchange Web Access 和 SharePoint Online</span><span class="sxs-lookup"><span data-stu-id="8d2b2-181">Web-based clients such as Exchange Web Access and SharePoint Online</span></span> |<span data-ttu-id="8d2b2-182">支援</span><span class="sxs-lookup"><span data-stu-id="8d2b2-182">Supported</span></span> |<span data-ttu-id="8d2b2-183">None</span><span class="sxs-lookup"><span data-stu-id="8d2b2-183">None</span></span> |
| <span data-ttu-id="8d2b2-184">豐富型用戶端應用程式，例如 Lync、Office 訂閱、CRM</span><span class="sxs-lookup"><span data-stu-id="8d2b2-184">Rich client applications such as Lync, Office Subscription, CRM</span></span> |<span data-ttu-id="8d2b2-185">不支援</span><span class="sxs-lookup"><span data-stu-id="8d2b2-185">Not Supported</span></span> |<span data-ttu-id="8d2b2-186">不支援</span><span class="sxs-lookup"><span data-stu-id="8d2b2-186">Not Supported</span></span> |
| <span data-ttu-id="8d2b2-187">豐富型電子郵件用戶端，例如 Outlook 和 ActiveSync</span><span class="sxs-lookup"><span data-stu-id="8d2b2-187">Email-rich clients such as Outlook and ActiveSync</span></span> |<span data-ttu-id="8d2b2-188">支援</span><span class="sxs-lookup"><span data-stu-id="8d2b2-188">Supported</span></span> |<span data-ttu-id="8d2b2-189">None</span><span class="sxs-lookup"><span data-stu-id="8d2b2-189">None</span></span> |

<span data-ttu-id="8d2b2-190">如需 BIG-IP Access Policy Manager 的相關詳細資訊，請參閱 [BIG-IP Access Policy Manager](https://f5.com/products/modules/access-policy-manager)</span><span class="sxs-lookup"><span data-stu-id="8d2b2-190">For more information about BIG-IP Access Policy Manager, see [BIG-IP Access Policy Manager.](https://f5.com/products/modules/access-policy-manager)</span></span> 

<span data-ttu-id="8d2b2-191">上如何 tooconfigure 此 STS tooprovide hello 單一登入體驗 tooyour Active Directory 使用者，下載 hello BIG-IP Access Policy Manager 指示 hello pdf [BIG-IP](http://www.f5.com/pdf/deployment-guides/microsoft-office-365-idp-dg.pdf)。</span><span class="sxs-lookup"><span data-stu-id="8d2b2-191">For hello BIG-IP Access Policy Manager instructions on how tooconfigure this STS tooprovide hello single sign-on experience tooyour Active Directory Users, download hello pdf [BIG-IP](http://www.f5.com/pdf/deployment-guides/microsoft-office-365-idp-dg.pdf).</span></span>

## <a name="bitglass"></a><span data-ttu-id="8d2b2-192">BitGlass</span><span class="sxs-lookup"><span data-stu-id="8d2b2-192">BitGlass</span></span>

<span data-ttu-id="8d2b2-193">hello 下面是此單一登入體驗的 hello 案例支援矩陣：</span><span class="sxs-lookup"><span data-stu-id="8d2b2-193">hello following is hello scenario support matrix for this single sign-on experience:</span></span>

| <span data-ttu-id="8d2b2-194">用戶端</span><span class="sxs-lookup"><span data-stu-id="8d2b2-194">Client</span></span> | <span data-ttu-id="8d2b2-195">支援</span><span class="sxs-lookup"><span data-stu-id="8d2b2-195">Support</span></span> | <span data-ttu-id="8d2b2-196">例外狀況</span><span class="sxs-lookup"><span data-stu-id="8d2b2-196">Exceptions</span></span> |
| --- | --- | --- |
| <span data-ttu-id="8d2b2-197">Web 用戶端，例如 Exchange Web Access 和 SharePoint Online</span><span class="sxs-lookup"><span data-stu-id="8d2b2-197">Web-based clients such as Exchange Web Access and SharePoint Online</span></span> |<span data-ttu-id="8d2b2-198">支援</span><span class="sxs-lookup"><span data-stu-id="8d2b2-198">Supported</span></span> |<span data-ttu-id="8d2b2-199">不支援整合式 Windows 驗證</span><span class="sxs-lookup"><span data-stu-id="8d2b2-199">Integrated Windows Authentication is not supported</span></span> |
| <span data-ttu-id="8d2b2-200">豐富型用戶端應用程式，例如 Lync、Office 訂閱、CRM</span><span class="sxs-lookup"><span data-stu-id="8d2b2-200">Rich client applications such as Lync, Office Subscription, CRM</span></span> |<span data-ttu-id="8d2b2-201">支援</span><span class="sxs-lookup"><span data-stu-id="8d2b2-201">Supported</span></span> |<span data-ttu-id="8d2b2-202">不支援整合式 Windows 驗證</span><span class="sxs-lookup"><span data-stu-id="8d2b2-202">Integrated Windows Authentication is not supported</span></span> |
| <span data-ttu-id="8d2b2-203">豐富型電子郵件用戶端，例如 Outlook 和 ActiveSync</span><span class="sxs-lookup"><span data-stu-id="8d2b2-203">Email-rich clients such as Outlook and ActiveSync</span></span> |<span data-ttu-id="8d2b2-204">支援</span><span class="sxs-lookup"><span data-stu-id="8d2b2-204">Supported</span></span> |<span data-ttu-id="8d2b2-205">None</span><span class="sxs-lookup"><span data-stu-id="8d2b2-205">None</span></span> |

<span data-ttu-id="8d2b2-206">如需 BitGlass 的詳細資訊，請參閱 [BitGlass](http://www.bitglass.com)。</span><span class="sxs-lookup"><span data-stu-id="8d2b2-206">For more information about BitGlass see [BitGlass](http://www.bitglass.com).</span></span>

## <a name="ca-secure-cloud"></a><span data-ttu-id="8d2b2-207">CA Secure Cloud</span><span class="sxs-lookup"><span data-stu-id="8d2b2-207">CA Secure Cloud</span></span>

<span data-ttu-id="8d2b2-208">hello 下面是此單一登入體驗的 hello 案例支援矩陣：</span><span class="sxs-lookup"><span data-stu-id="8d2b2-208">hello following is hello scenario support matrix for this single sign-on experience:</span></span>

| <span data-ttu-id="8d2b2-209">用戶端</span><span class="sxs-lookup"><span data-stu-id="8d2b2-209">Client</span></span> | <span data-ttu-id="8d2b2-210">支援</span><span class="sxs-lookup"><span data-stu-id="8d2b2-210">Support</span></span> | <span data-ttu-id="8d2b2-211">例外狀況</span><span class="sxs-lookup"><span data-stu-id="8d2b2-211">Exceptions</span></span> |
| --- | --- | --- |
| <span data-ttu-id="8d2b2-212">Web 用戶端，例如 Exchange Web Access 和 SharePoint Online</span><span class="sxs-lookup"><span data-stu-id="8d2b2-212">Web-based clients such as Exchange Web Access and SharePoint Online</span></span> |<span data-ttu-id="8d2b2-213">支援</span><span class="sxs-lookup"><span data-stu-id="8d2b2-213">Supported</span></span> |<span data-ttu-id="8d2b2-214">不支援整合式 Windows 驗證</span><span class="sxs-lookup"><span data-stu-id="8d2b2-214">Integrated Windows Authentication is not supported</span></span> |
| <span data-ttu-id="8d2b2-215">豐富型用戶端應用程式，例如 Lync、Office 訂閱、CRM</span><span class="sxs-lookup"><span data-stu-id="8d2b2-215">Rich client applications such as Lync, Office Subscription, CRM</span></span> |<span data-ttu-id="8d2b2-216">支援</span><span class="sxs-lookup"><span data-stu-id="8d2b2-216">Supported</span></span> |<span data-ttu-id="8d2b2-217">不支援整合式 Windows 驗證</span><span class="sxs-lookup"><span data-stu-id="8d2b2-217">Integrated Windows Authentication is not supported</span></span> |
| <span data-ttu-id="8d2b2-218">豐富型電子郵件用戶端，例如 Outlook 和 ActiveSync</span><span class="sxs-lookup"><span data-stu-id="8d2b2-218">Email-rich clients such as Outlook and ActiveSync</span></span> |<span data-ttu-id="8d2b2-219">支援</span><span class="sxs-lookup"><span data-stu-id="8d2b2-219">Supported</span></span> |<span data-ttu-id="8d2b2-220">None</span><span class="sxs-lookup"><span data-stu-id="8d2b2-220">None</span></span> |

<span data-ttu-id="8d2b2-221">如需 CA Secure Cloud 的詳細資訊，請參閱 [CA Secure Cloud](http://www.ca.com/us/products/security-as-a-service.aspx)。</span><span class="sxs-lookup"><span data-stu-id="8d2b2-221">For more information about CA Secure Cloud, see [CA Secure Cloud](http://www.ca.com/us/products/security-as-a-service.aspx).</span></span>

## <a name="ca-siteminder-1252-sp1-cumulative-release-4"></a><span data-ttu-id="8d2b2-222">CA SiteMinder 12.52 SP1 累計版本 4</span><span class="sxs-lookup"><span data-stu-id="8d2b2-222">CA SiteMinder 12.52 SP1 Cumulative Release 4</span></span>

<span data-ttu-id="8d2b2-223">hello 下面是此單一登入體驗的 hello 案例支援矩陣：</span><span class="sxs-lookup"><span data-stu-id="8d2b2-223">hello following is hello scenario support matrix for this single sign-on experience:</span></span> 

| <span data-ttu-id="8d2b2-224">用戶端</span><span class="sxs-lookup"><span data-stu-id="8d2b2-224">Client</span></span> | <span data-ttu-id="8d2b2-225">支援</span><span class="sxs-lookup"><span data-stu-id="8d2b2-225">Support</span></span> | <span data-ttu-id="8d2b2-226">例外狀況</span><span class="sxs-lookup"><span data-stu-id="8d2b2-226">Exceptions</span></span> |
| --- | --- | --- |
| <span data-ttu-id="8d2b2-227">Web 用戶端，例如 Exchange Web Access 和 SharePoint Online</span><span class="sxs-lookup"><span data-stu-id="8d2b2-227">Web-based clients such as Exchange Web Access and SharePoint Online</span></span> |<span data-ttu-id="8d2b2-228">支援</span><span class="sxs-lookup"><span data-stu-id="8d2b2-228">Supported</span></span> |<span data-ttu-id="8d2b2-229">None</span><span class="sxs-lookup"><span data-stu-id="8d2b2-229">None</span></span> |
| <span data-ttu-id="8d2b2-230">豐富型用戶端應用程式，例如 Lync、Office 訂閱、CRM</span><span class="sxs-lookup"><span data-stu-id="8d2b2-230">Rich client applications such as Lync, Office Subscription, CRM</span></span> |<span data-ttu-id="8d2b2-231">支援</span><span class="sxs-lookup"><span data-stu-id="8d2b2-231">Supported</span></span> |<span data-ttu-id="8d2b2-232">None</span><span class="sxs-lookup"><span data-stu-id="8d2b2-232">None</span></span> |
| <span data-ttu-id="8d2b2-233">豐富型電子郵件用戶端，例如 Outlook 和 ActiveSync</span><span class="sxs-lookup"><span data-stu-id="8d2b2-233">Email-rich clients such as Outlook and ActiveSync</span></span> |<span data-ttu-id="8d2b2-234">支援</span><span class="sxs-lookup"><span data-stu-id="8d2b2-234">Supported</span></span> |<span data-ttu-id="8d2b2-235">None</span><span class="sxs-lookup"><span data-stu-id="8d2b2-235">None</span></span> |

<span data-ttu-id="8d2b2-236">如需 CA SiteMinder 的詳細資訊，請參閱 [CA SiteMinder Federation](http://www.ca.com/us/products/ca-single-sign-on.html)。</span><span class="sxs-lookup"><span data-stu-id="8d2b2-236">For more information about CA SiteMinder, see [CA SiteMinder Federation](http://www.ca.com/us/products/ca-single-sign-on.html).</span></span> 

## <a name="centrify"></a><span data-ttu-id="8d2b2-237">Centrify</span><span class="sxs-lookup"><span data-stu-id="8d2b2-237">Centrify</span></span>

<span data-ttu-id="8d2b2-238">hello 下面是此單一登入體驗的 hello 案例支援矩陣：</span><span class="sxs-lookup"><span data-stu-id="8d2b2-238">hello following is hello scenario support matrix for this single sign-on experience:</span></span>

| <span data-ttu-id="8d2b2-239">用戶端</span><span class="sxs-lookup"><span data-stu-id="8d2b2-239">Client</span></span> | <span data-ttu-id="8d2b2-240">支援</span><span class="sxs-lookup"><span data-stu-id="8d2b2-240">Support</span></span> | <span data-ttu-id="8d2b2-241">例外狀況</span><span class="sxs-lookup"><span data-stu-id="8d2b2-241">Exceptions</span></span> |
| --- | --- | --- |
| <span data-ttu-id="8d2b2-242">Web 用戶端，例如 Exchange Web Access 和 SharePoint Online</span><span class="sxs-lookup"><span data-stu-id="8d2b2-242">Web-based clients such as Exchange Web Access and SharePoint Online</span></span> |<span data-ttu-id="8d2b2-243">支援</span><span class="sxs-lookup"><span data-stu-id="8d2b2-243">Supported</span></span> |<span data-ttu-id="8d2b2-244">None</span><span class="sxs-lookup"><span data-stu-id="8d2b2-244">None</span></span> |
| <span data-ttu-id="8d2b2-245">豐富型用戶端應用程式，例如 Lync、Office 訂閱、CRM</span><span class="sxs-lookup"><span data-stu-id="8d2b2-245">Rich client applications such as Lync, Office Subscription, CRM</span></span> |<span data-ttu-id="8d2b2-246">支援</span><span class="sxs-lookup"><span data-stu-id="8d2b2-246">Supported</span></span> |<span data-ttu-id="8d2b2-247">None</span><span class="sxs-lookup"><span data-stu-id="8d2b2-247">None</span></span> |
| <span data-ttu-id="8d2b2-248">豐富型電子郵件用戶端，例如 Outlook 和 ActiveSync</span><span class="sxs-lookup"><span data-stu-id="8d2b2-248">Email-rich clients such as Outlook and ActiveSync</span></span> |<span data-ttu-id="8d2b2-249">支援</span><span class="sxs-lookup"><span data-stu-id="8d2b2-249">Supported</span></span> |<span data-ttu-id="8d2b2-250">不支援用戶端存取控制</span><span class="sxs-lookup"><span data-stu-id="8d2b2-250">Client Access Control is not supported</span></span> |

<span data-ttu-id="8d2b2-251">如需 Centrify 的詳細資訊，請參閱 [Centrify](http://www.centrify.com/cloud/apps/single-sign-on-for-office-365.asp)。</span><span class="sxs-lookup"><span data-stu-id="8d2b2-251">For more information about Centrify, see [Centrify](http://www.centrify.com/cloud/apps/single-sign-on-for-office-365.asp).</span></span>

## <a name="dell-one-identity-cloud-access-manager-v71"></a><span data-ttu-id="8d2b2-252">Dell One Identity Cloud Access Manager v7.1</span><span class="sxs-lookup"><span data-stu-id="8d2b2-252">Dell One Identity Cloud Access Manager v7.1</span></span>

<span data-ttu-id="8d2b2-253">hello 下面是此單一登入體驗的 hello 案例支援矩陣：</span><span class="sxs-lookup"><span data-stu-id="8d2b2-253">hello following is hello scenario support matrix for this single sign-on experience:</span></span>

| <span data-ttu-id="8d2b2-254">用戶端</span><span class="sxs-lookup"><span data-stu-id="8d2b2-254">Client</span></span> | <span data-ttu-id="8d2b2-255">支援</span><span class="sxs-lookup"><span data-stu-id="8d2b2-255">Support</span></span> | <span data-ttu-id="8d2b2-256">例外狀況</span><span class="sxs-lookup"><span data-stu-id="8d2b2-256">Exceptions</span></span> |
| --- | --- | --- |
| <span data-ttu-id="8d2b2-257">Web 用戶端，例如 Exchange Web Access 和 SharePoint Online</span><span class="sxs-lookup"><span data-stu-id="8d2b2-257">Web-based clients such as Exchange Web Access and SharePoint Online</span></span> |<span data-ttu-id="8d2b2-258">支援</span><span class="sxs-lookup"><span data-stu-id="8d2b2-258">Supported</span></span> |<span data-ttu-id="8d2b2-259">None</span><span class="sxs-lookup"><span data-stu-id="8d2b2-259">None</span></span> |
| <span data-ttu-id="8d2b2-260">豐富型用戶端應用程式，例如 Lync、Office 訂閱、CRM</span><span class="sxs-lookup"><span data-stu-id="8d2b2-260">Rich client applications such as Lync, Office Subscription, CRM</span></span> |<span data-ttu-id="8d2b2-261">支援</span><span class="sxs-lookup"><span data-stu-id="8d2b2-261">Supported</span></span> |<span data-ttu-id="8d2b2-262">None</span><span class="sxs-lookup"><span data-stu-id="8d2b2-262">None</span></span> |
| <span data-ttu-id="8d2b2-263">豐富型電子郵件用戶端，例如 Outlook 和 ActiveSync</span><span class="sxs-lookup"><span data-stu-id="8d2b2-263">Email-rich clients such as Outlook and ActiveSync</span></span> |<span data-ttu-id="8d2b2-264">支援</span><span class="sxs-lookup"><span data-stu-id="8d2b2-264">Supported</span></span> |<span data-ttu-id="8d2b2-265">None</span><span class="sxs-lookup"><span data-stu-id="8d2b2-265">None</span></span> |

<span data-ttu-id="8d2b2-266">如需 Dell One Identity Cloud Access Manager 的詳細資訊，請參閱 [Dell One Identity Cloud Access Manager](http://software.dell.com/products/cloud-access-manager)。</span><span class="sxs-lookup"><span data-stu-id="8d2b2-266">For more information about Dell One Identity Cloud Access Manager, see [Dell One Identity Cloud Access Manager](http://software.dell.com/products/cloud-access-manager).</span></span>

 <span data-ttu-id="8d2b2-267">如需有關如何 tooconfigure 此 STS tooprovide hello 單一登入體驗 tooyour Office 365 使用者，請參閱的 hello 指示[設定 Office 365 使用者](http://documents.software.dell.com/dell-one-identity-cloud-access-manager/7.1/how-to-configure-microsoft-office-365)。</span><span class="sxs-lookup"><span data-stu-id="8d2b2-267">For hello instructions on how tooconfigure this STS tooprovide hello single sign-on experience tooyour Office 365 Users, see [Configure Office 365 Users](http://documents.software.dell.com/dell-one-identity-cloud-access-manager/7.1/how-to-configure-microsoft-office-365).</span></span> 

## <a name="digitalpersona-composite-authentication"></a><span data-ttu-id="8d2b2-268">DigitalPersona Composite 驗證</span><span class="sxs-lookup"><span data-stu-id="8d2b2-268">DigitalPersona Composite Authentication</span></span>  

<span data-ttu-id="8d2b2-269">hello 下面是此單一登入體驗的 hello 案例支援矩陣：</span><span class="sxs-lookup"><span data-stu-id="8d2b2-269">hello following is hello scenario support matrix for this single sign-on experience:</span></span>

| <span data-ttu-id="8d2b2-270">用戶端</span><span class="sxs-lookup"><span data-stu-id="8d2b2-270">Client</span></span> | <span data-ttu-id="8d2b2-271">支援</span><span class="sxs-lookup"><span data-stu-id="8d2b2-271">Support</span></span> | <span data-ttu-id="8d2b2-272">例外狀況</span><span class="sxs-lookup"><span data-stu-id="8d2b2-272">Exceptions</span></span> |
| --- | --- | --- |
| <span data-ttu-id="8d2b2-273">Web 用戶端，例如 Exchange Web Access 和 SharePoint Online</span><span class="sxs-lookup"><span data-stu-id="8d2b2-273">Web-based clients such as Exchange Web Access and SharePoint Online</span></span> |<span data-ttu-id="8d2b2-274">支援</span><span class="sxs-lookup"><span data-stu-id="8d2b2-274">Supported</span></span> |<span data-ttu-id="8d2b2-275">不支援整合式 Windows 驗證</span><span class="sxs-lookup"><span data-stu-id="8d2b2-275">Integrated Windows Authentication is not supported</span></span>|
| <span data-ttu-id="8d2b2-276">豐富型用戶端應用程式，例如 Lync、Office 訂閱、CRM</span><span class="sxs-lookup"><span data-stu-id="8d2b2-276">Rich client applications such as Lync, Office Subscription, CRM</span></span> |<span data-ttu-id="8d2b2-277">支援</span><span class="sxs-lookup"><span data-stu-id="8d2b2-277">Supported</span></span> |<span data-ttu-id="8d2b2-278">不支援整合式 Windows 驗證</span><span class="sxs-lookup"><span data-stu-id="8d2b2-278">Integrated Windows Authentication is not supported</span></span>|
| <span data-ttu-id="8d2b2-279">豐富型電子郵件用戶端，例如 Outlook 和 ActiveSync</span><span class="sxs-lookup"><span data-stu-id="8d2b2-279">Email-rich clients such as Outlook and ActiveSync</span></span> |<span data-ttu-id="8d2b2-280">支援</span><span class="sxs-lookup"><span data-stu-id="8d2b2-280">Supported</span></span> |<span data-ttu-id="8d2b2-281">None</span><span class="sxs-lookup"><span data-stu-id="8d2b2-281">None</span></span> |

<span data-ttu-id="8d2b2-282">如需詳細資訊，請參閱 [DigitalPersona Composite 驗證](http://www.crossmatch.com/uploadedFiles/Support/Reference_Material/DigitalPersona-Office-365-Deployment-Guide.pdf)。</span><span class="sxs-lookup"><span data-stu-id="8d2b2-282">For more information see [DigitalPersona Composite Authentication](http://www.crossmatch.com/uploadedFiles/Support/Reference_Material/DigitalPersona-Office-365-Deployment-Guide.pdf).</span></span>


## <a name="ibm-tivoli-federated-identity-manager-622"></a><span data-ttu-id="8d2b2-283">IBM Tivoli Federated Identity Manager 6.2.2</span><span class="sxs-lookup"><span data-stu-id="8d2b2-283">IBM Tivoli Federated Identity Manager 6.2.2</span></span>

<span data-ttu-id="8d2b2-284">hello 下面是此單一登入體驗的 hello 案例支援矩陣：</span><span class="sxs-lookup"><span data-stu-id="8d2b2-284">hello following is hello scenario support matrix for this single sign-on experience:</span></span> 

| <span data-ttu-id="8d2b2-285">用戶端</span><span class="sxs-lookup"><span data-stu-id="8d2b2-285">Client</span></span> | <span data-ttu-id="8d2b2-286">支援</span><span class="sxs-lookup"><span data-stu-id="8d2b2-286">Support</span></span> | <span data-ttu-id="8d2b2-287">例外狀況</span><span class="sxs-lookup"><span data-stu-id="8d2b2-287">Exceptions</span></span> |
| --- | --- | --- |
| <span data-ttu-id="8d2b2-288">Web 用戶端，例如 Exchange Web Access 和 SharePoint Online</span><span class="sxs-lookup"><span data-stu-id="8d2b2-288">Web-based clients such as Exchange Web Access and SharePoint Online</span></span> |<span data-ttu-id="8d2b2-289">支援</span><span class="sxs-lookup"><span data-stu-id="8d2b2-289">Supported</span></span> |<span data-ttu-id="8d2b2-290">None</span><span class="sxs-lookup"><span data-stu-id="8d2b2-290">None</span></span> |
| <span data-ttu-id="8d2b2-291">豐富型用戶端應用程式，例如 Lync、Office 訂閱、CRM</span><span class="sxs-lookup"><span data-stu-id="8d2b2-291">Rich client applications such as Lync, Office Subscription, CRM</span></span> |<span data-ttu-id="8d2b2-292">支援</span><span class="sxs-lookup"><span data-stu-id="8d2b2-292">Supported</span></span> |<span data-ttu-id="8d2b2-293">None</span><span class="sxs-lookup"><span data-stu-id="8d2b2-293">None</span></span> |
| <span data-ttu-id="8d2b2-294">豐富型電子郵件用戶端，例如 Outlook 和 ActiveSync</span><span class="sxs-lookup"><span data-stu-id="8d2b2-294">Email-rich clients such as Outlook and ActiveSync</span></span> |<span data-ttu-id="8d2b2-295">支援</span><span class="sxs-lookup"><span data-stu-id="8d2b2-295">Supported</span></span> |<span data-ttu-id="8d2b2-296">None</span><span class="sxs-lookup"><span data-stu-id="8d2b2-296">None</span></span> |

<span data-ttu-id="8d2b2-297">如需 IBM Tivoli Federated Identity Manager 的詳細資訊，請參閱 [IBM Security Access Manager for Microsoft Applications](http://www-01.ibm.com/support/docview.wss?uid=swg24029517)。</span><span class="sxs-lookup"><span data-stu-id="8d2b2-297">For more information about IBM Tivoli Federated Identity Manager, see [IBM Security Access Manager for Microsoft Applications](http://www-01.ibm.com/support/docview.wss?uid=swg24029517).</span></span>

## <a name="icewall-federation-version-30"></a><span data-ttu-id="8d2b2-298">IceWall Federation Version 3.0</span><span class="sxs-lookup"><span data-stu-id="8d2b2-298">IceWall Federation Version 3.0</span></span>

<span data-ttu-id="8d2b2-299">hello 下面是此單一登入體驗的 hello 案例支援矩陣：</span><span class="sxs-lookup"><span data-stu-id="8d2b2-299">hello following is hello scenario support matrix for this single sign-on experience:</span></span>

| <span data-ttu-id="8d2b2-300">用戶端</span><span class="sxs-lookup"><span data-stu-id="8d2b2-300">Client</span></span> | <span data-ttu-id="8d2b2-301">支援</span><span class="sxs-lookup"><span data-stu-id="8d2b2-301">Support</span></span> | <span data-ttu-id="8d2b2-302">例外狀況</span><span class="sxs-lookup"><span data-stu-id="8d2b2-302">Exceptions</span></span> |
| --- | --- | --- |
| <span data-ttu-id="8d2b2-303">Web 用戶端，例如 Exchange Web Access 和 SharePoint Online</span><span class="sxs-lookup"><span data-stu-id="8d2b2-303">Web-based clients such as Exchange Web Access and SharePoint Online</span></span> |<span data-ttu-id="8d2b2-304">支援</span><span class="sxs-lookup"><span data-stu-id="8d2b2-304">Supported</span></span> |<span data-ttu-id="8d2b2-305">不支援整合式 Windows 驗證</span><span class="sxs-lookup"><span data-stu-id="8d2b2-305">Integrated Windows Authentication is not supported</span></span> |
| <span data-ttu-id="8d2b2-306">豐富型用戶端應用程式，例如 Lync、Office 訂閱、CRM</span><span class="sxs-lookup"><span data-stu-id="8d2b2-306">Rich client applications such as Lync, Office Subscription, CRM</span></span> |<span data-ttu-id="8d2b2-307">支援</span><span class="sxs-lookup"><span data-stu-id="8d2b2-307">Supported</span></span> |<span data-ttu-id="8d2b2-308">不支援整合式 Windows 驗證</span><span class="sxs-lookup"><span data-stu-id="8d2b2-308">Integrated Windows Authentication is not supported</span></span> |
| <span data-ttu-id="8d2b2-309">豐富型電子郵件用戶端，例如 Outlook 和 ActiveSync</span><span class="sxs-lookup"><span data-stu-id="8d2b2-309">Email-rich clients such as Outlook and ActiveSync</span></span> |<span data-ttu-id="8d2b2-310">支援</span><span class="sxs-lookup"><span data-stu-id="8d2b2-310">Supported</span></span> |<span data-ttu-id="8d2b2-311">None</span><span class="sxs-lookup"><span data-stu-id="8d2b2-311">None</span></span> |

<span data-ttu-id="8d2b2-312">如需 IceWall Federation 的詳細資訊，請參閱 [IceWall Federation 3.0 版](http://h50146.www5.hp.com/products/software/security/icewall/eng/federation/)和 [IceWall Federation (含 Office 365)](http://h50146.www5.hp.com/products/software/security/icewall/federation/office365.html)。</span><span class="sxs-lookup"><span data-stu-id="8d2b2-312">For more information about IceWall Federation, see [IceWall Federation Version 3.0](http://h50146.www5.hp.com/products/software/security/icewall/eng/federation/) and [IceWall Federation with Office 365](http://h50146.www5.hp.com/products/software/security/icewall/federation/office365.html).</span></span>

## <a name="memority"></a><span data-ttu-id="8d2b2-313">Memority</span><span class="sxs-lookup"><span data-stu-id="8d2b2-313">Memority</span></span>

<span data-ttu-id="8d2b2-314">hello 下面是此登入體驗的 hello 案例支援矩陣：</span><span class="sxs-lookup"><span data-stu-id="8d2b2-314">hello following is hello scenario support matrix for this sign-on experience:</span></span> 

| <span data-ttu-id="8d2b2-315">用戶端</span><span class="sxs-lookup"><span data-stu-id="8d2b2-315">Client</span></span> | <span data-ttu-id="8d2b2-316">支援</span><span class="sxs-lookup"><span data-stu-id="8d2b2-316">Support</span></span> | <span data-ttu-id="8d2b2-317">例外狀況</span><span class="sxs-lookup"><span data-stu-id="8d2b2-317">Exceptions</span></span> |
| --- | --- | --- |
| <span data-ttu-id="8d2b2-318">Web 用戶端，例如 Exchange Web Access 和 SharePoint Online</span><span class="sxs-lookup"><span data-stu-id="8d2b2-318">Web-based clients such as Exchange Web Access and SharePoint Online</span></span> |<span data-ttu-id="8d2b2-319">支援</span><span class="sxs-lookup"><span data-stu-id="8d2b2-319">Supported</span></span> |<span data-ttu-id="8d2b2-320">None</span><span class="sxs-lookup"><span data-stu-id="8d2b2-320">None</span></span> |
| <span data-ttu-id="8d2b2-321">豐富型用戶端應用程式，例如 Lync、Office 訂閱、CRM</span><span class="sxs-lookup"><span data-stu-id="8d2b2-321">Rich client applications such as Lync, Office Subscription, CRM</span></span> |<span data-ttu-id="8d2b2-322">支援</span><span class="sxs-lookup"><span data-stu-id="8d2b2-322">Supported</span></span> |<span data-ttu-id="8d2b2-323">None</span><span class="sxs-lookup"><span data-stu-id="8d2b2-323">None</span></span> |
| <span data-ttu-id="8d2b2-324">豐富型電子郵件用戶端，例如 Outlook 和 ActiveSync</span><span class="sxs-lookup"><span data-stu-id="8d2b2-324">Email-rich clients such as Outlook and ActiveSync</span></span> |<span data-ttu-id="8d2b2-325">支援</span><span class="sxs-lookup"><span data-stu-id="8d2b2-325">Supported</span></span> |<span data-ttu-id="8d2b2-326">None</span><span class="sxs-lookup"><span data-stu-id="8d2b2-326">None</span></span> |

<span data-ttu-id="8d2b2-327">如需使用 Memority 的詳細資訊，請參閱 [Memority](http://www.memority.com)。</span><span class="sxs-lookup"><span data-stu-id="8d2b2-327">For more information about using Memority see [Memority](http://www.memority.com).</span></span>


## <a name="netiq-access-manager-4x"></a><span data-ttu-id="8d2b2-328">NetIQ Access Manager 4.x</span><span class="sxs-lookup"><span data-stu-id="8d2b2-328">NetIQ Access Manager 4.x</span></span>

<span data-ttu-id="8d2b2-329">hello 下面是此單一登入體驗的 hello 案例支援矩陣：</span><span class="sxs-lookup"><span data-stu-id="8d2b2-329">hello following is hello scenario support matrix for this single sign-on experience:</span></span>

| <span data-ttu-id="8d2b2-330">用戶端</span><span class="sxs-lookup"><span data-stu-id="8d2b2-330">Client</span></span> | <span data-ttu-id="8d2b2-331">支援</span><span class="sxs-lookup"><span data-stu-id="8d2b2-331">Support</span></span> | <span data-ttu-id="8d2b2-332">例外狀況</span><span class="sxs-lookup"><span data-stu-id="8d2b2-332">Exceptions</span></span> |
| --- | --- | --- |
| <span data-ttu-id="8d2b2-333">Web 用戶端，例如 Exchange Web Access 和 SharePoint Online</span><span class="sxs-lookup"><span data-stu-id="8d2b2-333">Web-based clients such as Exchange Web Access and SharePoint Online</span></span> |<span data-ttu-id="8d2b2-334">支援</span><span class="sxs-lookup"><span data-stu-id="8d2b2-334">Supported</span></span> |<span data-ttu-id="8d2b2-335">None</span><span class="sxs-lookup"><span data-stu-id="8d2b2-335">None</span></span>|
| <span data-ttu-id="8d2b2-336">豐富型用戶端應用程式，例如 Lync、Office 訂閱、CRM</span><span class="sxs-lookup"><span data-stu-id="8d2b2-336">Rich client applications such as Lync, Office Subscription, CRM</span></span> |<span data-ttu-id="8d2b2-337">支援</span><span class="sxs-lookup"><span data-stu-id="8d2b2-337">Supported</span></span> |<span data-ttu-id="8d2b2-338">None</span><span class="sxs-lookup"><span data-stu-id="8d2b2-338">None</span></span>|
| <span data-ttu-id="8d2b2-339">豐富型電子郵件用戶端，例如 Outlook 和 ActiveSync</span><span class="sxs-lookup"><span data-stu-id="8d2b2-339">Email-rich clients such as Outlook and ActiveSync</span></span> |<span data-ttu-id="8d2b2-340">支援</span><span class="sxs-lookup"><span data-stu-id="8d2b2-340">Supported</span></span> |<span data-ttu-id="8d2b2-341">None</span><span class="sxs-lookup"><span data-stu-id="8d2b2-341">None</span></span> |

<span data-ttu-id="8d2b2-342">如需詳細資訊，請參閱 [NetIQ Access Manager](https://www.netiq.com/documentation/access-manager-43/admin/data/b65ogn0.html#b12iqp0m)。</span><span class="sxs-lookup"><span data-stu-id="8d2b2-342">For more information, see [NetIQ Access Manager](https://www.netiq.com/documentation/access-manager-43/admin/data/b65ogn0.html#b12iqp0m).</span></span>

## <a name="okta"></a><span data-ttu-id="8d2b2-343">Okta</span><span class="sxs-lookup"><span data-stu-id="8d2b2-343">Okta</span></span>

<span data-ttu-id="8d2b2-344">hello 下面是此單一登入體驗的 hello 案例支援矩陣：</span><span class="sxs-lookup"><span data-stu-id="8d2b2-344">hello following is hello scenario support matrix for this single sign-on experience:</span></span> 

| <span data-ttu-id="8d2b2-345">用戶端</span><span class="sxs-lookup"><span data-stu-id="8d2b2-345">Client</span></span> | <span data-ttu-id="8d2b2-346">支援</span><span class="sxs-lookup"><span data-stu-id="8d2b2-346">Support</span></span> | <span data-ttu-id="8d2b2-347">例外狀況</span><span class="sxs-lookup"><span data-stu-id="8d2b2-347">Exceptions</span></span> |
| --- | --- | --- |
| <span data-ttu-id="8d2b2-348">Web 用戶端，例如 Exchange Web Access 和 SharePoint Online</span><span class="sxs-lookup"><span data-stu-id="8d2b2-348">Web-based clients such as Exchange Web Access and SharePoint Online</span></span> |<span data-ttu-id="8d2b2-349">支援</span><span class="sxs-lookup"><span data-stu-id="8d2b2-349">Supported</span></span> |<span data-ttu-id="8d2b2-350">整合式 Windows 認證需要設定其他 Web 伺服器與 Okta 應用程式。</span><span class="sxs-lookup"><span data-stu-id="8d2b2-350">Integrated Windows Authentication requires setup of additional web server and Okta application.</span></span> |
| <span data-ttu-id="8d2b2-351">豐富型用戶端應用程式，例如 Lync、Office 訂閱、CRM</span><span class="sxs-lookup"><span data-stu-id="8d2b2-351">Rich client applications such as Lync, Office Subscription, CRM</span></span> |<span data-ttu-id="8d2b2-352">支援</span><span class="sxs-lookup"><span data-stu-id="8d2b2-352">Supported</span></span> |<span data-ttu-id="8d2b2-353">整合式 Windows 驗證</span><span class="sxs-lookup"><span data-stu-id="8d2b2-353">Integrated Windows Authentication</span></span> |
| <span data-ttu-id="8d2b2-354">豐富型電子郵件用戶端，例如 Outlook 和 ActiveSync</span><span class="sxs-lookup"><span data-stu-id="8d2b2-354">Email-rich clients such as Outlook and ActiveSync</span></span> |<span data-ttu-id="8d2b2-355">支援</span><span class="sxs-lookup"><span data-stu-id="8d2b2-355">Supported</span></span> |<span data-ttu-id="8d2b2-356">None</span><span class="sxs-lookup"><span data-stu-id="8d2b2-356">None</span></span> |

<span data-ttu-id="8d2b2-357">如需 Okta 的詳細資訊，請參閱 [Okta](https://www.okta.com/)。</span><span class="sxs-lookup"><span data-stu-id="8d2b2-357">For more information about Okta, see [Okta](https://www.okta.com/).</span></span>

## <a name="onelogin"></a><span data-ttu-id="8d2b2-358">OneLogin</span><span class="sxs-lookup"><span data-stu-id="8d2b2-358">OneLogin</span></span>

<span data-ttu-id="8d2b2-359">hello 下面是此單一登入體驗的 hello 案例支援矩陣：</span><span class="sxs-lookup"><span data-stu-id="8d2b2-359">hello following is hello scenario support matrix for this single sign-on experience:</span></span> 

| <span data-ttu-id="8d2b2-360">用戶端</span><span class="sxs-lookup"><span data-stu-id="8d2b2-360">Client</span></span> | <span data-ttu-id="8d2b2-361">支援</span><span class="sxs-lookup"><span data-stu-id="8d2b2-361">Support</span></span> | <span data-ttu-id="8d2b2-362">例外狀況</span><span class="sxs-lookup"><span data-stu-id="8d2b2-362">Exceptions</span></span> |
| --- | --- | --- |
| <span data-ttu-id="8d2b2-363">Web 用戶端，例如 Exchange Web Access 和 SharePoint Online</span><span class="sxs-lookup"><span data-stu-id="8d2b2-363">Web-based clients such as Exchange Web Access and SharePoint Online</span></span> |<span data-ttu-id="8d2b2-364">支援</span><span class="sxs-lookup"><span data-stu-id="8d2b2-364">Supported</span></span> |<span data-ttu-id="8d2b2-365">整合式 Windows 驗證</span><span class="sxs-lookup"><span data-stu-id="8d2b2-365">Integrated Windows Authentication</span></span> |
| <span data-ttu-id="8d2b2-366">豐富型用戶端應用程式，例如 Lync、Office 訂閱、CRM</span><span class="sxs-lookup"><span data-stu-id="8d2b2-366">Rich client applications such as Lync, Office Subscription, CRM</span></span> |<span data-ttu-id="8d2b2-367">支援</span><span class="sxs-lookup"><span data-stu-id="8d2b2-367">Supported</span></span> |<span data-ttu-id="8d2b2-368">整合式 Windows 驗證</span><span class="sxs-lookup"><span data-stu-id="8d2b2-368">Integrated Windows Authentication</span></span> |
| <span data-ttu-id="8d2b2-369">豐富型電子郵件用戶端，例如 Outlook 和 ActiveSync</span><span class="sxs-lookup"><span data-stu-id="8d2b2-369">Email-rich clients such as Outlook and ActiveSync</span></span> |<span data-ttu-id="8d2b2-370">支援</span><span class="sxs-lookup"><span data-stu-id="8d2b2-370">Supported</span></span> |<span data-ttu-id="8d2b2-371">None</span><span class="sxs-lookup"><span data-stu-id="8d2b2-371">None</span></span> |

<span data-ttu-id="8d2b2-372">如需 OneLogin 的詳細資訊，請參閱 [OneLogin](https://www.onelogin.com/)。</span><span class="sxs-lookup"><span data-stu-id="8d2b2-372">For more information about OneLogin, see [OneLogin](https://www.onelogin.com/).</span></span>

## <a name="optimal-idm-virtual-identity-server-federation-services"></a><span data-ttu-id="8d2b2-373">Optimal IDM Virtual Identity Server Federation Services</span><span class="sxs-lookup"><span data-stu-id="8d2b2-373">Optimal IDM Virtual Identity Server Federation Services</span></span>

<span data-ttu-id="8d2b2-374">hello 下列是此單一登入體驗 hello 案例支援矩陣：</span><span class="sxs-lookup"><span data-stu-id="8d2b2-374">hello following is hello scenario support matrix this single sign-on experience:</span></span>

| <span data-ttu-id="8d2b2-375">用戶端</span><span class="sxs-lookup"><span data-stu-id="8d2b2-375">Client</span></span> | <span data-ttu-id="8d2b2-376">支援</span><span class="sxs-lookup"><span data-stu-id="8d2b2-376">Support</span></span> | <span data-ttu-id="8d2b2-377">例外狀況</span><span class="sxs-lookup"><span data-stu-id="8d2b2-377">Exceptions</span></span> |
| --- | --- | --- |
| <span data-ttu-id="8d2b2-378">Web 用戶端，例如 Exchange Web Access 和 SharePoint Online</span><span class="sxs-lookup"><span data-stu-id="8d2b2-378">Web-based clients such as Exchange Web Access and SharePoint Online</span></span> |<span data-ttu-id="8d2b2-379">支援</span><span class="sxs-lookup"><span data-stu-id="8d2b2-379">Supported</span></span> |<span data-ttu-id="8d2b2-380">None</span><span class="sxs-lookup"><span data-stu-id="8d2b2-380">None</span></span> |
| <span data-ttu-id="8d2b2-381">豐富型用戶端應用程式，例如 Lync、Office 訂閱、CRM</span><span class="sxs-lookup"><span data-stu-id="8d2b2-381">Rich client applications such as Lync, Office Subscription, CRM</span></span> |<span data-ttu-id="8d2b2-382">支援</span><span class="sxs-lookup"><span data-stu-id="8d2b2-382">Supported</span></span> |<span data-ttu-id="8d2b2-383">整合式 Windows 驗證</span><span class="sxs-lookup"><span data-stu-id="8d2b2-383">Integrated Windows Authentication</span></span> |
| <span data-ttu-id="8d2b2-384">豐富型電子郵件用戶端，例如 Outlook 和 ActiveSync</span><span class="sxs-lookup"><span data-stu-id="8d2b2-384">Email-rich clients such as Outlook and ActiveSync</span></span> |<span data-ttu-id="8d2b2-385">支援</span><span class="sxs-lookup"><span data-stu-id="8d2b2-385">Supported</span></span> |

<span data-ttu-id="8d2b2-386">如需有關用戶端存取原則，請參閱[限制存取 tooOffice 365 Services 根據 hello 位置的用戶端 hello](https://technet.microsoft.com/library/hh526961.aspx)。</span><span class="sxs-lookup"><span data-stu-id="8d2b2-386">For more information about client access polices see [Limiting Access tooOffice 365 Services Based on hello Location of hello Client](https://technet.microsoft.com/library/hh526961.aspx).</span></span>





## <a name="pingfederate-611-72-8x"></a><span data-ttu-id="8d2b2-387">PingFederate 6.11, 7.2, 8.x</span><span class="sxs-lookup"><span data-stu-id="8d2b2-387">PingFederate 6.11, 7.2, 8.x</span></span>

<span data-ttu-id="8d2b2-388">hello 下面是此單一登入體驗的 hello 案例支援矩陣：</span><span class="sxs-lookup"><span data-stu-id="8d2b2-388">hello following is hello scenario support matrix for this single sign-on experience:</span></span>

| <span data-ttu-id="8d2b2-389">用戶端</span><span class="sxs-lookup"><span data-stu-id="8d2b2-389">Client</span></span> | <span data-ttu-id="8d2b2-390">支援</span><span class="sxs-lookup"><span data-stu-id="8d2b2-390">Support</span></span> | <span data-ttu-id="8d2b2-391">例外狀況</span><span class="sxs-lookup"><span data-stu-id="8d2b2-391">Exceptions</span></span> |
| --- | --- | --- |
| <span data-ttu-id="8d2b2-392">Web 用戶端，例如 Exchange Web Access 和 SharePoint Online</span><span class="sxs-lookup"><span data-stu-id="8d2b2-392">Web-based clients such as Exchange Web Access and SharePoint Online</span></span> |<span data-ttu-id="8d2b2-393">支援</span><span class="sxs-lookup"><span data-stu-id="8d2b2-393">Supported</span></span> |<span data-ttu-id="8d2b2-394">None</span><span class="sxs-lookup"><span data-stu-id="8d2b2-394">None</span></span> |
| <span data-ttu-id="8d2b2-395">豐富型用戶端應用程式，例如 Lync、Office 訂閱、CRM</span><span class="sxs-lookup"><span data-stu-id="8d2b2-395">Rich client applications such as Lync, Office Subscription, CRM</span></span> |<span data-ttu-id="8d2b2-396">支援</span><span class="sxs-lookup"><span data-stu-id="8d2b2-396">Supported</span></span> |<span data-ttu-id="8d2b2-397">None</span><span class="sxs-lookup"><span data-stu-id="8d2b2-397">None</span></span> |
| <span data-ttu-id="8d2b2-398">豐富型電子郵件用戶端，例如 Outlook 和 ActiveSync</span><span class="sxs-lookup"><span data-stu-id="8d2b2-398">Email-rich clients such as Outlook and ActiveSync</span></span> |<span data-ttu-id="8d2b2-399">支援</span><span class="sxs-lookup"><span data-stu-id="8d2b2-399">Supported</span></span> |<span data-ttu-id="8d2b2-400">None</span><span class="sxs-lookup"><span data-stu-id="8d2b2-400">None</span></span> |

<span data-ttu-id="8d2b2-401">如 hello 上如何 tooconfigure 此 STS tooprovide hello 單一登入體驗的 PingFederate 指示 tooyour Active Directory 使用者，請參閱 hello 下列其中一種：</span><span class="sxs-lookup"><span data-stu-id="8d2b2-401">For hello PingFederate instructions on how tooconfigure this STS tooprovide hello single sign-on experience tooyour Active Directory users, see one of hello following:</span></span> 

- [<span data-ttu-id="8d2b2-402">PingFederate 6.11</span><span class="sxs-lookup"><span data-stu-id="8d2b2-402">PingFederate 6.11</span></span>](http://go.microsoft.com/fwlink/?LinkID=266321)
- [<span data-ttu-id="8d2b2-403">PingFederate 7.2</span><span class="sxs-lookup"><span data-stu-id="8d2b2-403">PingFederate 7.2</span></span>](http://documentation.pingidentity.com/display/PF72/PingFederate+7.2)
- [<span data-ttu-id="8d2b2-404">PingFederate 8.x</span><span class="sxs-lookup"><span data-stu-id="8d2b2-404">PingFederate 8.x</span></span>](http://documentation.pingidentity.com/display/PFS/SSO+to+Office+365+Introduction)

## <a name="radiantone-cfs-30"></a><span data-ttu-id="8d2b2-405">RadiantOne CFS 3.0</span><span class="sxs-lookup"><span data-stu-id="8d2b2-405">RadiantOne CFS 3.0</span></span>

<span data-ttu-id="8d2b2-406">hello 下面是此單一登入體驗的 hello 案例支援矩陣：</span><span class="sxs-lookup"><span data-stu-id="8d2b2-406">hello following is hello scenario support matrix for this single sign-on experience:</span></span> 

| <span data-ttu-id="8d2b2-407">用戶端</span><span class="sxs-lookup"><span data-stu-id="8d2b2-407">Client</span></span> | <span data-ttu-id="8d2b2-408">支援</span><span class="sxs-lookup"><span data-stu-id="8d2b2-408">Support</span></span> | <span data-ttu-id="8d2b2-409">例外狀況</span><span class="sxs-lookup"><span data-stu-id="8d2b2-409">Exceptions</span></span> |
| --- | --- | --- |
| <span data-ttu-id="8d2b2-410">Web 用戶端，例如 Exchange Web Access 和 SharePoint Online</span><span class="sxs-lookup"><span data-stu-id="8d2b2-410">Web-based clients such as Exchange Web Access and SharePoint Online</span></span> |<span data-ttu-id="8d2b2-411">支援</span><span class="sxs-lookup"><span data-stu-id="8d2b2-411">Supported</span></span> |<span data-ttu-id="8d2b2-412">None</span><span class="sxs-lookup"><span data-stu-id="8d2b2-412">None</span></span> |
| <span data-ttu-id="8d2b2-413">豐富型用戶端應用程式，例如 Lync、Office 訂閱、CRM</span><span class="sxs-lookup"><span data-stu-id="8d2b2-413">Rich client applications such as Lync, Office Subscription, CRM</span></span> |<span data-ttu-id="8d2b2-414">支援</span><span class="sxs-lookup"><span data-stu-id="8d2b2-414">Supported</span></span> |<span data-ttu-id="8d2b2-415">整合式 Windows 驗證</span><span class="sxs-lookup"><span data-stu-id="8d2b2-415">Integrated Windows Authentication</span></span> |
| <span data-ttu-id="8d2b2-416">豐富型電子郵件用戶端，例如 Outlook 和 ActiveSync</span><span class="sxs-lookup"><span data-stu-id="8d2b2-416">Email-rich clients such as Outlook and ActiveSync</span></span> |<span data-ttu-id="8d2b2-417">支援</span><span class="sxs-lookup"><span data-stu-id="8d2b2-417">Supported</span></span> |<span data-ttu-id="8d2b2-418">None</span><span class="sxs-lookup"><span data-stu-id="8d2b2-418">None</span></span> |

<span data-ttu-id="8d2b2-419">如需 RadiantOne CFS 的詳細資訊，請參閱 [RadiantOne CFS](http://www.radiantlogic.com/products/radiantone-cfs/)。</span><span class="sxs-lookup"><span data-stu-id="8d2b2-419">For more information about RadiantOne CFS, see [RadiantOne CFS](http://www.radiantlogic.com/products/radiantone-cfs/).</span></span>

## <a name="sailpoint-identitynow"></a><span data-ttu-id="8d2b2-420">Sailpoint IdentityNow</span><span class="sxs-lookup"><span data-stu-id="8d2b2-420">Sailpoint IdentityNow</span></span>

<span data-ttu-id="8d2b2-421">hello 下面是此單一登入體驗的 hello 案例支援矩陣：</span><span class="sxs-lookup"><span data-stu-id="8d2b2-421">hello following is hello scenario support matrix for this single sign-on experience:</span></span>

| <span data-ttu-id="8d2b2-422">用戶端</span><span class="sxs-lookup"><span data-stu-id="8d2b2-422">Client</span></span> | <span data-ttu-id="8d2b2-423">支援</span><span class="sxs-lookup"><span data-stu-id="8d2b2-423">Support</span></span> | <span data-ttu-id="8d2b2-424">例外狀況</span><span class="sxs-lookup"><span data-stu-id="8d2b2-424">Exceptions</span></span> |
| --- | --- | --- |
| <span data-ttu-id="8d2b2-425">Web 用戶端，例如 Exchange Web Access 和 SharePoint Online</span><span class="sxs-lookup"><span data-stu-id="8d2b2-425">Web-based clients such as Exchange Web Access and SharePoint Online</span></span> |<span data-ttu-id="8d2b2-426">支援</span><span class="sxs-lookup"><span data-stu-id="8d2b2-426">Supported</span></span> |<span data-ttu-id="8d2b2-427">不支援整合式 Windows 驗證</span><span class="sxs-lookup"><span data-stu-id="8d2b2-427">Integrated Windows Authentication is not supported</span></span> |
| <span data-ttu-id="8d2b2-428">豐富型用戶端應用程式，例如 Lync、Office 訂閱、CRM</span><span class="sxs-lookup"><span data-stu-id="8d2b2-428">Rich client applications such as Lync, Office Subscription, CRM</span></span> |<span data-ttu-id="8d2b2-429">支援</span><span class="sxs-lookup"><span data-stu-id="8d2b2-429">Supported</span></span> |<span data-ttu-id="8d2b2-430">不支援整合式 Windows 驗證</span><span class="sxs-lookup"><span data-stu-id="8d2b2-430">Integrated Windows Authentication is not supported</span></span> |
| <span data-ttu-id="8d2b2-431">豐富型電子郵件用戶端，例如 Outlook 和 ActiveSync</span><span class="sxs-lookup"><span data-stu-id="8d2b2-431">Email-rich clients such as Outlook and ActiveSync</span></span> |<span data-ttu-id="8d2b2-432">支援</span><span class="sxs-lookup"><span data-stu-id="8d2b2-432">Supported</span></span> |<span data-ttu-id="8d2b2-433">None</span><span class="sxs-lookup"><span data-stu-id="8d2b2-433">None</span></span> |

<span data-ttu-id="8d2b2-434">如需詳細資訊，請參閱 [Sailpoint IdentityNow](https://www.sailpoint.com/idaas-identity-as-a-service-identitynow/)。</span><span class="sxs-lookup"><span data-stu-id="8d2b2-434">For more information, see [Sailpoint IdentityNow](https://www.sailpoint.com/idaas-identity-as-a-service-identitynow/).</span></span>

## <a name="secureauth-idp-720"></a><span data-ttu-id="8d2b2-435">SecureAuth IdP 7.2.0</span><span class="sxs-lookup"><span data-stu-id="8d2b2-435">SecureAuth IdP 7.2.0</span></span>

<span data-ttu-id="8d2b2-436">hello 下面是此單一登入體驗的 hello 案例支援矩陣：</span><span class="sxs-lookup"><span data-stu-id="8d2b2-436">hello following is hello scenario support matrix for this single sign-on experience:</span></span> 

| <span data-ttu-id="8d2b2-437">用戶端</span><span class="sxs-lookup"><span data-stu-id="8d2b2-437">Client</span></span> | <span data-ttu-id="8d2b2-438">支援</span><span class="sxs-lookup"><span data-stu-id="8d2b2-438">Support</span></span> | <span data-ttu-id="8d2b2-439">例外狀況</span><span class="sxs-lookup"><span data-stu-id="8d2b2-439">Exceptions</span></span> |
| --- | --- | --- |
| <span data-ttu-id="8d2b2-440">Web 用戶端，例如 Exchange Web Access 和 SharePoint Online</span><span class="sxs-lookup"><span data-stu-id="8d2b2-440">Web-based clients such as Exchange Web Access and SharePoint Online</span></span> |<span data-ttu-id="8d2b2-441">支援</span><span class="sxs-lookup"><span data-stu-id="8d2b2-441">Supported</span></span> |<span data-ttu-id="8d2b2-442">None</span><span class="sxs-lookup"><span data-stu-id="8d2b2-442">None</span></span> |
| <span data-ttu-id="8d2b2-443">豐富型用戶端應用程式，例如 Lync、Office 訂閱、CRM</span><span class="sxs-lookup"><span data-stu-id="8d2b2-443">Rich client applications such as Lync, Office Subscription, CRM</span></span> |<span data-ttu-id="8d2b2-444">支援</span><span class="sxs-lookup"><span data-stu-id="8d2b2-444">Supported</span></span> |<span data-ttu-id="8d2b2-445">None</span><span class="sxs-lookup"><span data-stu-id="8d2b2-445">None</span></span> |
| <span data-ttu-id="8d2b2-446">豐富型電子郵件用戶端，例如 Outlook 和 ActiveSync</span><span class="sxs-lookup"><span data-stu-id="8d2b2-446">Email-rich clients such as Outlook and ActiveSync</span></span> |<span data-ttu-id="8d2b2-447">支援</span><span class="sxs-lookup"><span data-stu-id="8d2b2-447">Supported</span></span> |<span data-ttu-id="8d2b2-448">None</span><span class="sxs-lookup"><span data-stu-id="8d2b2-448">None</span></span> |

<span data-ttu-id="8d2b2-449">如需 SecureAuth 的相關詳細資訊，請參閱 [SecureAuth IdP](http://go.microsoft.com/?linkid=9845293)。</span><span class="sxs-lookup"><span data-stu-id="8d2b2-449">For more information about SecureAuth, see [SecureAuth IdP](http://go.microsoft.com/?linkid=9845293).</span></span>














## <a name="signgo-53"></a><span data-ttu-id="8d2b2-450">Sign&go 5.3</span><span class="sxs-lookup"><span data-stu-id="8d2b2-450">Sign&go 5.3</span></span>

<span data-ttu-id="8d2b2-451">hello 下面是此單一登入體驗的 hello 案例支援矩陣：</span><span class="sxs-lookup"><span data-stu-id="8d2b2-451">hello following is hello scenario support matrix for this single sign-on experience:</span></span>

| <span data-ttu-id="8d2b2-452">用戶端</span><span class="sxs-lookup"><span data-stu-id="8d2b2-452">Client</span></span> | <span data-ttu-id="8d2b2-453">支援</span><span class="sxs-lookup"><span data-stu-id="8d2b2-453">Support</span></span> | <span data-ttu-id="8d2b2-454">例外狀況</span><span class="sxs-lookup"><span data-stu-id="8d2b2-454">Exceptions</span></span> |
| --- | --- | --- |
| <span data-ttu-id="8d2b2-455">Web 用戶端，例如 Exchange Web Access 和 SharePoint Online</span><span class="sxs-lookup"><span data-stu-id="8d2b2-455">Web-based clients such as Exchange Web Access and SharePoint Online</span></span> |<span data-ttu-id="8d2b2-456">支援</span><span class="sxs-lookup"><span data-stu-id="8d2b2-456">Supported</span></span> |<span data-ttu-id="8d2b2-457">支援 Kerberos Contract</span><span class="sxs-lookup"><span data-stu-id="8d2b2-457">Kerberos Contracts supported</span></span> |
| <span data-ttu-id="8d2b2-458">豐富型用戶端應用程式，例如 Lync、Office 訂閱、CRM</span><span class="sxs-lookup"><span data-stu-id="8d2b2-458">Rich client applications such as Lync, Office Subscription, CRM</span></span> |<span data-ttu-id="8d2b2-459">支援</span><span class="sxs-lookup"><span data-stu-id="8d2b2-459">Supported</span></span> |<span data-ttu-id="8d2b2-460">None</span><span class="sxs-lookup"><span data-stu-id="8d2b2-460">None</span></span> |
| <span data-ttu-id="8d2b2-461">豐富型電子郵件用戶端，例如 Outlook 和 ActiveSync</span><span class="sxs-lookup"><span data-stu-id="8d2b2-461">Email-rich clients such as Outlook and ActiveSync</span></span> |<span data-ttu-id="8d2b2-462">支援</span><span class="sxs-lookup"><span data-stu-id="8d2b2-462">Supported</span></span> |<span data-ttu-id="8d2b2-463">None</span><span class="sxs-lookup"><span data-stu-id="8d2b2-463">None</span></span> |

<span data-ttu-id="8d2b2-464">Sign&go 5.3 透過 Kerberos Contract 的組態支援 Kerberos 驗證。</span><span class="sxs-lookup"><span data-stu-id="8d2b2-464">Sign&go 5.3 supports Kerberos authentication via configuration of a Kerberos Contract.</span></span>  <span data-ttu-id="8d2b2-465">如需使用此設定時的協助，請連絡 Ilex 或檢視表的 hello 安裝手冊 》 [sign&go](http://www.ilex-international.com/docs/sign&go_wsfederation_en.pdf)</span><span class="sxs-lookup"><span data-stu-id="8d2b2-465">For assistance with this configuration, please contact Ilex or view hello setup guide [Sign&go](http://www.ilex-international.com/docs/sign&go_wsfederation_en.pdf)</span></span>

## <a name="softbank-technology-online-service-gate"></a><span data-ttu-id="8d2b2-466">SoftBank Technology Online Service Gate</span><span class="sxs-lookup"><span data-stu-id="8d2b2-466">SoftBank Technology Online Service Gate</span></span>

<span data-ttu-id="8d2b2-467">hello 下面是此單一登入體驗的 hello 案例支援矩陣：</span><span class="sxs-lookup"><span data-stu-id="8d2b2-467">hello following is hello scenario support matrix for this single sign-on experience:</span></span>

| <span data-ttu-id="8d2b2-468">用戶端</span><span class="sxs-lookup"><span data-stu-id="8d2b2-468">Client</span></span> | <span data-ttu-id="8d2b2-469">支援</span><span class="sxs-lookup"><span data-stu-id="8d2b2-469">Support</span></span> | <span data-ttu-id="8d2b2-470">例外狀況</span><span class="sxs-lookup"><span data-stu-id="8d2b2-470">Exceptions</span></span> |
| --- | --- | --- |
| <span data-ttu-id="8d2b2-471">Web 用戶端，例如 Exchange Web Access 和 SharePoint Online</span><span class="sxs-lookup"><span data-stu-id="8d2b2-471">Web-based clients such as Exchange Web Access and SharePoint Online</span></span> |<span data-ttu-id="8d2b2-472">支援</span><span class="sxs-lookup"><span data-stu-id="8d2b2-472">Supported</span></span> |<span data-ttu-id="8d2b2-473">不支援整合式 Windows 驗證</span><span class="sxs-lookup"><span data-stu-id="8d2b2-473">Integrated Windows Authentication is not supported</span></span> |
| <span data-ttu-id="8d2b2-474">豐富型用戶端應用程式，例如 Lync、Office 訂閱、CRM</span><span class="sxs-lookup"><span data-stu-id="8d2b2-474">Rich client applications such as Lync, Office Subscription, CRM</span></span> |<span data-ttu-id="8d2b2-475">支援</span><span class="sxs-lookup"><span data-stu-id="8d2b2-475">Supported</span></span> |<span data-ttu-id="8d2b2-476">不支援整合式 Windows 驗證</span><span class="sxs-lookup"><span data-stu-id="8d2b2-476">Integrated Windows Authentication is not supported</span></span> |
| <span data-ttu-id="8d2b2-477">豐富型電子郵件用戶端，例如 Outlook 和 ActiveSync</span><span class="sxs-lookup"><span data-stu-id="8d2b2-477">Email-rich clients such as Outlook and ActiveSync</span></span> |<span data-ttu-id="8d2b2-478">支援</span><span class="sxs-lookup"><span data-stu-id="8d2b2-478">Supported</span></span> |<span data-ttu-id="8d2b2-479">None</span><span class="sxs-lookup"><span data-stu-id="8d2b2-479">None</span></span> |

<span data-ttu-id="8d2b2-480">如需 SoftBank Technology Online Service Gate 的詳細資訊，請參閱 [Softbank](https://www.softbanktech.jp/service/list/osg-pro-ent/)。</span><span class="sxs-lookup"><span data-stu-id="8d2b2-480">For more information about SoftBank Technology Online Service Gate see [Softbank](https://www.softbanktech.jp/service/list/osg-pro-ent/)</span></span>

## <a name="vmware-workspace-one"></a><span data-ttu-id="8d2b2-481">VMware Workspace One</span><span class="sxs-lookup"><span data-stu-id="8d2b2-481">VMware Workspace One</span></span>

<span data-ttu-id="8d2b2-482">hello 下面是此單一登入體驗的 hello 案例支援矩陣：</span><span class="sxs-lookup"><span data-stu-id="8d2b2-482">hello following is hello scenario support matrix for this single sign-on experience:</span></span>

| <span data-ttu-id="8d2b2-483">用戶端</span><span class="sxs-lookup"><span data-stu-id="8d2b2-483">Client</span></span> | <span data-ttu-id="8d2b2-484">支援</span><span class="sxs-lookup"><span data-stu-id="8d2b2-484">Support</span></span> | <span data-ttu-id="8d2b2-485">例外狀況</span><span class="sxs-lookup"><span data-stu-id="8d2b2-485">Exceptions</span></span> |
| --- | --- | --- |
| <span data-ttu-id="8d2b2-486">Web 用戶端，例如 Exchange Web Access 和 SharePoint Online</span><span class="sxs-lookup"><span data-stu-id="8d2b2-486">Web-based clients such as Exchange Web Access and SharePoint Online</span></span> |<span data-ttu-id="8d2b2-487">支援</span><span class="sxs-lookup"><span data-stu-id="8d2b2-487">Supported</span></span> |<span data-ttu-id="8d2b2-488">不支援整合式 Windows 驗證</span><span class="sxs-lookup"><span data-stu-id="8d2b2-488">Integrated Windows Authentication is not supported</span></span> |
| <span data-ttu-id="8d2b2-489">豐富型用戶端應用程式，例如 Lync、Office 訂閱、CRM</span><span class="sxs-lookup"><span data-stu-id="8d2b2-489">Rich client applications such as Lync, Office Subscription, CRM</span></span> |<span data-ttu-id="8d2b2-490">支援</span><span class="sxs-lookup"><span data-stu-id="8d2b2-490">Supported</span></span> |<span data-ttu-id="8d2b2-491">不支援整合式 Windows 驗證</span><span class="sxs-lookup"><span data-stu-id="8d2b2-491">Integrated Windows Authentication is not supported</span></span> |
| <span data-ttu-id="8d2b2-492">豐富型電子郵件用戶端，例如 Outlook 和 ActiveSync</span><span class="sxs-lookup"><span data-stu-id="8d2b2-492">Email-rich clients such as Outlook and ActiveSync</span></span> |<span data-ttu-id="8d2b2-493">支援</span><span class="sxs-lookup"><span data-stu-id="8d2b2-493">Supported</span></span> |<span data-ttu-id="8d2b2-494">None</span><span class="sxs-lookup"><span data-stu-id="8d2b2-494">None</span></span> |

<span data-ttu-id="8d2b2-495">如需詳細資訊，請參閱 [VMware Workspace One](http://www.vmware.com/pdf/vidm-office365-saml.pdf)。</span><span class="sxs-lookup"><span data-stu-id="8d2b2-495">For more information about see [VMware Workspace One](http://www.vmware.com/pdf/vidm-office365-saml.pdf)</span></span>

