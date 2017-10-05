---
title: "Azure 安全性管理和監視概觀 | Microsoft Docs"
description: " Azure 提供安全性機制，來協助管理與監視 Azure 雲端服務和虛擬機器。  本文概述這些核心安全性功能和服務。 "
services: security
documentationcenter: na
author: TerryLanfear
manager: StevenPo
editor: TomSh
ms.assetid: 5cf2827b-6cd3-434d-9100-d7411f7ed424
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 11/21/2016
ms.author: terrylan
ms.openlocfilehash: 6787877deabafd0b7308e190cb45b4036049b05b
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/18/2017
---
# <a name="azure-security-management-and-monitoring-overview"></a><span data-ttu-id="10d6e-104">Azure 安全性管理和監視概觀</span><span class="sxs-lookup"><span data-stu-id="10d6e-104">Azure Security Management and Monitoring Overview</span></span>
<span data-ttu-id="10d6e-105">Azure 提供安全性機制，來協助管理與監視 Azure 雲端服務和虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="10d6e-105">Azure provides security mechanisms to aid in the management and monitoring of Azure cloud services and virtual machines.</span></span> <span data-ttu-id="10d6e-106">本文概述這些核心安全性功能和服務。</span><span class="sxs-lookup"><span data-stu-id="10d6e-106">This article provides an overview of these core security features and services.</span></span> <span data-ttu-id="10d6e-107">所提供的文章連結將提供每個項目的詳細資料，以讓您深入了解。</span><span class="sxs-lookup"><span data-stu-id="10d6e-107">Links are provided to articles that give details of each so you can learn more.</span></span>

<span data-ttu-id="10d6e-108">Microsoft 雲端服務的安全性是您與 Microsoft 之間的合作關係和共同責任。</span><span class="sxs-lookup"><span data-stu-id="10d6e-108">The security of your Microsoft cloud services is a partnership and shared responsibility between you and Microsoft.</span></span> <span data-ttu-id="10d6e-109">共同責任表示 Microsoft 負責 Microsoft Azure 和其資料中心的實體安全性 (藉由使用鎖定門禁卡、圍牆和防護這類安全性保護)。</span><span class="sxs-lookup"><span data-stu-id="10d6e-109">Shared responsibility means Microsoft is responsible for the Microsoft Azure and physical security of its data centers (by using security protections such as locked badge entry doors, fences, and guards).</span></span> <span data-ttu-id="10d6e-110">此外，Azure 還提供軟體層的強式雲端安全性層級，其符合其需求客戶的安全性、隱私權和法務遵循需求。</span><span class="sxs-lookup"><span data-stu-id="10d6e-110">In addition, Azure provides strong levels of cloud security at the software layer that meets the security, privacy, and compliance needs of its demanding customers.</span></span>

<span data-ttu-id="10d6e-111">您擁有您的資料和身分識別、保護它們的責任、您內部部署資源的安全性，以及您可控制之雲端元件的安全性。</span><span class="sxs-lookup"><span data-stu-id="10d6e-111">You own your data and identities, the responsibility for protecting them, the security of your on-premises resources, and the security of cloud components over which you have control.</span></span> <span data-ttu-id="10d6e-112">Microsoft 提供安全性控制和功能，協助您保護資料和應用程式。</span><span class="sxs-lookup"><span data-stu-id="10d6e-112">Microsoft provides you with security controls and capabilities to help you protect your data and applications.</span></span> <span data-ttu-id="10d6e-113">您安全性責任的高低取決於雲端服務的類型。</span><span class="sxs-lookup"><span data-stu-id="10d6e-113">Your degree of responsibility for security is based on the type of cloud service.</span></span>

<span data-ttu-id="10d6e-114">下表摘要說明 Microsoft 與客戶責任的平衡。</span><span class="sxs-lookup"><span data-stu-id="10d6e-114">The following chart summarizes the balance of responsibility for both Microsoft and the customer.</span></span>

![共同責任][1]

<span data-ttu-id="10d6e-116">若要深入了解安全性管理，請參閱 [Azure 的安全性管理](azure-security-management.md)。</span><span class="sxs-lookup"><span data-stu-id="10d6e-116">For a deeper dive into security management, see [Security management in Azure](azure-security-management.md).</span></span>

<span data-ttu-id="10d6e-117">以下是本文所涵蓋的核心功能：</span><span class="sxs-lookup"><span data-stu-id="10d6e-117">Here are the core features to be covered in this article:</span></span>

* <span data-ttu-id="10d6e-118">角色型存取控制</span><span class="sxs-lookup"><span data-stu-id="10d6e-118">Role-Based Access Control</span></span>
* <span data-ttu-id="10d6e-119">反惡意程式碼</span><span class="sxs-lookup"><span data-stu-id="10d6e-119">Antimalware</span></span>
* <span data-ttu-id="10d6e-120">Multi-Factor Authentication</span><span class="sxs-lookup"><span data-stu-id="10d6e-120">Multi-Factor Authentication</span></span>
* <span data-ttu-id="10d6e-121">ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="10d6e-121">ExpressRoute</span></span>
* <span data-ttu-id="10d6e-122">虛擬網路閘道</span><span class="sxs-lookup"><span data-stu-id="10d6e-122">Virtual network gateways</span></span>
* <span data-ttu-id="10d6e-123">Privileged Identity Management</span><span class="sxs-lookup"><span data-stu-id="10d6e-123">Privileged identity management</span></span>
* <span data-ttu-id="10d6e-124">身分識別保護</span><span class="sxs-lookup"><span data-stu-id="10d6e-124">Identity protection</span></span>
* <span data-ttu-id="10d6e-125">資訊安全中心</span><span class="sxs-lookup"><span data-stu-id="10d6e-125">Security Center</span></span>

## <a name="role-based-access-control"></a><span data-ttu-id="10d6e-126">角色型存取控制</span><span class="sxs-lookup"><span data-stu-id="10d6e-126">Role-Based Access Control</span></span>
<span data-ttu-id="10d6e-127">角色型存取控制 (RBAC) 提供 Azure 資源的更細緻存取權管理。</span><span class="sxs-lookup"><span data-stu-id="10d6e-127">Role-Based Access Control (RBAC) provides fine-grained access management for Azure resources.</span></span> <span data-ttu-id="10d6e-128">使用 RBAC，您可以僅授與使用者執行其作業所需的存取權。</span><span class="sxs-lookup"><span data-stu-id="10d6e-128">Using RBAC, you can grant people only the amount of access that they need to perform their jobs.</span></span>  <span data-ttu-id="10d6e-129">RBAC 也可以協助您確保當使用者離開組織時，他們就無法存取雲端中的資源。</span><span class="sxs-lookup"><span data-stu-id="10d6e-129">RBAC can also help you ensure that when people leave the organization they lose access to resources in the cloud.</span></span>

<span data-ttu-id="10d6e-130">深入了解：</span><span class="sxs-lookup"><span data-stu-id="10d6e-130">Learn more:</span></span>

* [<span data-ttu-id="10d6e-131">有關 RBAC 的 Active Directory 小組部落格</span><span class="sxs-lookup"><span data-stu-id="10d6e-131">Active Directory team blog on RBAC</span></span>](http://i1.blogs.technet.com/b/ad/archive/2015/10/12/azure-rbac-is-ga.aspx)
* [<span data-ttu-id="10d6e-132">Azure 角色型存取控制</span><span class="sxs-lookup"><span data-stu-id="10d6e-132">Azure Role-Based Access Control</span></span>](../active-directory/role-based-access-control-configure.md)

## <a name="antimalware"></a><span data-ttu-id="10d6e-133">反惡意程式碼</span><span class="sxs-lookup"><span data-stu-id="10d6e-133">Antimalware</span></span>
<span data-ttu-id="10d6e-134">運用 Azure，您可以使用來自各大安全性廠商 (例如 Microsoft、Symantec、Trend Micro、McAfee 和 Kaspersky) 的反惡意程式碼軟體，以協助保護您的虛擬機器抵禦惡意檔案、廣告軟體和其他威脅。</span><span class="sxs-lookup"><span data-stu-id="10d6e-134">With Azure, you can use antimalware software from major security vendors such as Microsoft, Symantec, Trend Micro, McAfee, and Kaspersky to help protect your virtual machines from malicious files, adware, and other threats.</span></span>

<span data-ttu-id="10d6e-135">Microsoft Antimalware 可讓您安裝 PaaS 角色和虛擬機器的反惡意程式碼代理程式。</span><span class="sxs-lookup"><span data-stu-id="10d6e-135">Microsoft Antimalware offers you the ability to install an antimalware agent for both PaaS roles and virtual machines.</span></span> <span data-ttu-id="10d6e-136">根據 System Center Endpoint Protection，這項功能會將經證實的內部部署安全性技術帶入雲端。</span><span class="sxs-lookup"><span data-stu-id="10d6e-136">Based on System Center Endpoint Protection, this feature brings proven on-premises security technology to the cloud.</span></span>

<span data-ttu-id="10d6e-137">我們也提供 Azure 平台中 Trend 之 [Deep Security](http://www.trendmicro.com/us/enterprise/cloud-solutions/deep-security/)™ 和 [SecureCloud](http://www.trendmicro.com/us/enterprise/cloud-solutions/secure-cloud/)™ 產品的深入整合。</span><span class="sxs-lookup"><span data-stu-id="10d6e-137">We also offer deep integration for Trend’s [Deep Security](http://www.trendmicro.com/us/enterprise/cloud-solutions/deep-security/)™ and [SecureCloud](http://www.trendmicro.com/us/enterprise/cloud-solutions/secure-cloud/)™ products in the Azure platform.</span></span> <span data-ttu-id="10d6e-138">DeepSecurity 是一種防毒解決方案，SecureCloud 則是一種加密解決方案。</span><span class="sxs-lookup"><span data-stu-id="10d6e-138">DeepSecurity is an Antivirus solution and SecureCloud is an encryption solution.</span></span> <span data-ttu-id="10d6e-139">DeepSecurity 會使用擴充功能模型部署在 VM 內。</span><span class="sxs-lookup"><span data-stu-id="10d6e-139">DeepSecurity is deployed inside VMs using an extension model.</span></span> <span data-ttu-id="10d6e-140">使用入口網站 UI 和 PowerShell，您可以選擇在所啟動的 VM 內或已部署的現有 VM 內使用 DeepSecurity。</span><span class="sxs-lookup"><span data-stu-id="10d6e-140">Using the portal UI and PowerShell, you can choose to use DeepSecurity inside new VMs that are being spun up, or existing VMs that are already deployed.</span></span>

<span data-ttu-id="10d6e-141">Azure 也支援 Symantec End Point Protection (SEP)。</span><span class="sxs-lookup"><span data-stu-id="10d6e-141">Symantec End Point Protection (SEP) is also supported on Azure.</span></span> <span data-ttu-id="10d6e-142">透過入口網站整合，客戶可以指定他們想要在 VM 內使用 SEP。</span><span class="sxs-lookup"><span data-stu-id="10d6e-142">Through portal integration, customers can specify that they intend to use SEP within a VM.</span></span> <span data-ttu-id="10d6e-143">SEP 可以透過 Azure 入口網站安裝在全新的 VM 上，也可以使用 PowerShell 安裝在現有 VM 上。</span><span class="sxs-lookup"><span data-stu-id="10d6e-143">SEP can be installed on a brand new VM via the Azure portal or can be installed on an existing VM using PowerShell.</span></span>

<span data-ttu-id="10d6e-144">深入了解：</span><span class="sxs-lookup"><span data-stu-id="10d6e-144">Learn more:</span></span>

* [<span data-ttu-id="10d6e-145">在 Azure 虛擬機器上部署反惡意程式碼解決方案</span><span class="sxs-lookup"><span data-stu-id="10d6e-145">Deploying Antimalware Solutions on Azure Virtual Machines</span></span>](https://azure.microsoft.com/blog/deploying-antimalware-solutions-on-azure-virtual-machines/)
* [<span data-ttu-id="10d6e-146">適用於 Azure 雲端服務和虛擬機器的 Microsoft Antimalware</span><span class="sxs-lookup"><span data-stu-id="10d6e-146">Microsoft Antimalware for Azure Cloud Services and Virtual Machines</span></span>](azure-security-antimalware.md)
* [<span data-ttu-id="10d6e-147">如何在 Windows VM 上安裝和設定 Trend Micro Deep Security as a Service</span><span class="sxs-lookup"><span data-stu-id="10d6e-147">How to install and configure Trend Micro Deep Security as a Service on a Windows VM</span></span>](../virtual-machines/windows/classic/install-trend.md)
* [<span data-ttu-id="10d6e-148">如何在 Windows VM 上安裝和設定 Symantec Endpoint Protection</span><span class="sxs-lookup"><span data-stu-id="10d6e-148">How to install and configure Symantec Endpoint Protection on a Windows VM</span></span>](../virtual-machines/windows/classic/install-symantec.md)
* [<span data-ttu-id="10d6e-149">保護 Azure 虛擬機器的新反惡意程式碼選項 - McAfee Endpoint Protection</span><span class="sxs-lookup"><span data-stu-id="10d6e-149">New Antimalware Options for Protecting Azure Virtual Machines – McAfee Endpoint Protection</span></span>](https://azure.microsoft.com/blog/new-antimalware-options-for-protecting-azure-virtual-machines/)

## <a name="multi-factor-authentication"></a><span data-ttu-id="10d6e-150">Multi-Factor Authentication</span><span class="sxs-lookup"><span data-stu-id="10d6e-150">Multi-Factor Authentication</span></span>
<span data-ttu-id="10d6e-151">Azure Multi-Factor Authentication (MFA) 是需要使用多種驗證方法，並在使用者登入和交易中新增重要的第二層安全性的驗證方法。</span><span class="sxs-lookup"><span data-stu-id="10d6e-151">Azure Multi-factor authentication (MFA) is a method of authentication that requires the use of more than one verification method and adds a critical second layer of security to user sign-ins and transactions.</span></span> <span data-ttu-id="10d6e-152">MFA 有助於保護對資料與應用程式的存取，同時可以滿足使用者對簡單登入程序的需求。</span><span class="sxs-lookup"><span data-stu-id="10d6e-152">MFA helps safeguard access to data and applications while meeting user demand for a simple sign-in process.</span></span> <span data-ttu-id="10d6e-153">它可以透過一些驗證選項 (例如電話、文字訊息，或行動應用程式通知或驗證代碼，以及第三方 OATH 權杖) 來提供強大的驗證功能。</span><span class="sxs-lookup"><span data-stu-id="10d6e-153">It delivers strong authentication via a range of verification options—phone call, text message, or mobile app notification or verification code and third party OATH tokens.</span></span>

<span data-ttu-id="10d6e-154">深入了解：</span><span class="sxs-lookup"><span data-stu-id="10d6e-154">Learn more:</span></span>

* [<span data-ttu-id="10d6e-155">Multi-Factor Authentication</span><span class="sxs-lookup"><span data-stu-id="10d6e-155">Multi-factor authentication</span></span>](https://azure.microsoft.com/documentation/services/multi-factor-authentication/)
* [<span data-ttu-id="10d6e-156">什麼是 Azure Multi-Factor Authentication？</span><span class="sxs-lookup"><span data-stu-id="10d6e-156">What is Azure Multi-Factor Authentication?</span></span>](../multi-factor-authentication/multi-factor-authentication.md)
* [<span data-ttu-id="10d6e-157">Azure Multi-Factor Authentication 的作用</span><span class="sxs-lookup"><span data-stu-id="10d6e-157">How Azure Multi-Factor Authentication works</span></span>](../multi-factor-authentication/multi-factor-authentication-how-it-works.md)

## <a name="expressroute"></a><span data-ttu-id="10d6e-158">ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="10d6e-158">ExpressRoute</span></span>
<span data-ttu-id="10d6e-159">Microsoft Azure ExpressRoute 可讓您透過連線提供者所提供的專用私人連線，將內部部署網路擴充至 Microsoft 雲端。</span><span class="sxs-lookup"><span data-stu-id="10d6e-159">Microsoft Azure ExpressRoute lets you extend your on-premises networks into the Microsoft cloud over a dedicated private connection facilitated by a connectivity provider.</span></span> <span data-ttu-id="10d6e-160">透過 ExpressRoute，您可以建立 Microsoft 雲端服務的連線，例如 Microsoft Azure、Office 365 和 CRM Online。</span><span class="sxs-lookup"><span data-stu-id="10d6e-160">With ExpressRoute, you can establish connections to Microsoft cloud services, such as Microsoft Azure, Office 365, and CRM Online.</span></span> <span data-ttu-id="10d6e-161">從任意點對任意點 (IP VPN) 網路、點對點乙太網路，或在共置設施上透過連線提供者的虛擬交叉連接，都可以進行連線。</span><span class="sxs-lookup"><span data-stu-id="10d6e-161">Connectivity can be from an any-to-any (IP VPN) network, a point-to-point Ethernet network, or a virtual cross-connection through a connectivity provider at a co-location facility.</span></span> <span data-ttu-id="10d6e-162">ExpressRoute 連線不會經過公用網際網路。</span><span class="sxs-lookup"><span data-stu-id="10d6e-162">ExpressRoute connections do not go over the public Internet.</span></span> <span data-ttu-id="10d6e-163">相較於一般網際網路連線，這可讓 ExpressRoute 連線提供更可靠、更快速、延遲更短和更安全的連線。</span><span class="sxs-lookup"><span data-stu-id="10d6e-163">This allows ExpressRoute connections to offer more reliability, faster speeds, lower latencies, and higher security than typical connections over the Internet.</span></span>

<span data-ttu-id="10d6e-164">深入了解：</span><span class="sxs-lookup"><span data-stu-id="10d6e-164">Learn more:</span></span>

* [<span data-ttu-id="10d6e-165">ExpressRoute 技術概觀</span><span class="sxs-lookup"><span data-stu-id="10d6e-165">ExpressRoute technical overview</span></span>](../expressroute/expressroute-introduction.md)

## <a name="virtual-network-gateways"></a><span data-ttu-id="10d6e-166">虛擬網路閘道</span><span class="sxs-lookup"><span data-stu-id="10d6e-166">Virtual network gateways</span></span>
<span data-ttu-id="10d6e-167">VPN 閘道 (也稱為 Azure 虛擬網路閘道) 可用來傳送虛擬網路與內部部署位置之間的網路流量。</span><span class="sxs-lookup"><span data-stu-id="10d6e-167">VPN Gateways, also called Azure Virtual Network Gateways, are used to send network traffic between virtual networks and on-premises locations.</span></span> <span data-ttu-id="10d6e-168">它們也用來傳送 Azure 內多個虛擬網路之間的流量 (VNet 對 VNet)。</span><span class="sxs-lookup"><span data-stu-id="10d6e-168">They are also used to send traffic between multiple virtual networks within Azure (VNet-to-VNet).</span></span>  <span data-ttu-id="10d6e-169">VPN 閘道提供 Azure 與基礎結構之間的跨單位安全連線。</span><span class="sxs-lookup"><span data-stu-id="10d6e-169">VPN gateways provide secure cross-premises connectivity between Azure and your infrastructure.</span></span>

<span data-ttu-id="10d6e-170">深入了解：</span><span class="sxs-lookup"><span data-stu-id="10d6e-170">Learn more:</span></span>

* [<span data-ttu-id="10d6e-171">關於 VPN 閘道</span><span class="sxs-lookup"><span data-stu-id="10d6e-171">About VPN gateways</span></span>](../vpn-gateway/vpn-gateway-about-vpngateways.md)
* [<span data-ttu-id="10d6e-172">Azure 網路安全性概觀</span><span class="sxs-lookup"><span data-stu-id="10d6e-172">Azure Network Security Overview</span></span>](security-network-overview.md)

## <a name="privileged-identity-management"></a><span data-ttu-id="10d6e-173">Privileged Identity Management</span><span class="sxs-lookup"><span data-stu-id="10d6e-173">Privileged Identity Management</span></span>
<span data-ttu-id="10d6e-174">使用者有時候需要在 Azure 資源或其他 SaaS 應用程式中執行特殊權限的作業。</span><span class="sxs-lookup"><span data-stu-id="10d6e-174">Sometimes users need to carry out privileged operations in Azure resources or other SaaS applications.</span></span> <span data-ttu-id="10d6e-175">這通常表示組織必須授與他們永久的 Azure Active Directory (Azure AD) 特殊存取權限。</span><span class="sxs-lookup"><span data-stu-id="10d6e-175">This often means organizations have to give them permanent privileged access in Azure Active Directory (Azure AD).</span></span> <span data-ttu-id="10d6e-176">這會提高雲端資源的安全性風險，因為組織無法滴水不漏地監視這些使用者利用其特殊存取權限的所作所為。</span><span class="sxs-lookup"><span data-stu-id="10d6e-176">This is a growing security risk for cloud-hosted resources because organizations can't sufficiently monitor what those users are doing with their privileged access.</span></span>
<span data-ttu-id="10d6e-177">此外，如果擁有特殊存取權限的使用者帳戶遭到入侵，這個缺口可能會影響您的整體雲端安全性。</span><span class="sxs-lookup"><span data-stu-id="10d6e-177">Additionally, if a user account with privileged access is compromised, that one breach could impact your overall cloud security.</span></span> <span data-ttu-id="10d6e-178">Azure AD Privileged Identity Management 有助於解決這項風險，方法是降低權限的曝光時間，並增加使用情形的可見性。</span><span class="sxs-lookup"><span data-stu-id="10d6e-178">Azure AD Privileged Identity Management helps to resolve this risk by lowering the exposure time of privileges and increasing visibility into usage.</span></span>  

<span data-ttu-id="10d6e-179">Privileged Identity Management 引入暫時管理員的概念來進行角色或「及時」系統管理員存取，這是需要完成指派角色啟用程序的使用者。</span><span class="sxs-lookup"><span data-stu-id="10d6e-179">Privileged Identity Management introduces the concept of a temporary admin for a role or “just in time” administrator access, which is a user who needs to complete an activation process for that assigned role.</span></span> <span data-ttu-id="10d6e-180">啟用程序會在指定的時段內，將 Azure AD 中角色的使用者指派從非作用中變更為作用中，如 8 小時。</span><span class="sxs-lookup"><span data-stu-id="10d6e-180">The activation process changes the assignment of the user to a role in Azure AD from inactive to active, for a specified time period such as eight hours.</span></span>

<span data-ttu-id="10d6e-181">深入了解：</span><span class="sxs-lookup"><span data-stu-id="10d6e-181">Learn more:</span></span>

* [<span data-ttu-id="10d6e-182">Azure AD 特殊權限身分識別管理</span><span class="sxs-lookup"><span data-stu-id="10d6e-182">Azure AD Privileged Identity Management</span></span>](../active-directory/active-directory-privileged-identity-management-configure.md)
* [<span data-ttu-id="10d6e-183">開始使用 Azure AD Privileged Identity Management</span><span class="sxs-lookup"><span data-stu-id="10d6e-183">Get started with Azure AD Privileged Identity Management</span></span>](../active-directory/active-directory-privileged-identity-management-getting-started.md)

## <a name="identity-protection"></a><span data-ttu-id="10d6e-184">身分識別保護</span><span class="sxs-lookup"><span data-stu-id="10d6e-184">Identity Protection</span></span>
<span data-ttu-id="10d6e-185">Azure Active Directory (AD) Identity Protection 提供可疑登入活動和潛在弱點的整合檢視，協助保護您的業務。</span><span class="sxs-lookup"><span data-stu-id="10d6e-185">Azure Active Directory (AD) Identity Protection provides a consolidated view of suspicious sign-in activities and potential vulnerabilities to help protect your business.</span></span> <span data-ttu-id="10d6e-186">Identity Protection 會依據跡象偵測使用者和特權 (系統管理員) 身分識別的可疑活動，例如暴力密碼破解攻擊、認證外洩，以及從不明位置或受感染裝置的登入。</span><span class="sxs-lookup"><span data-stu-id="10d6e-186">Identity Protection detects suspicious activities for users and privileged (admin) identities, based on signals like brute-force attacks, leaked credentials, and sign-ins from unfamiliar locations and infected devices.</span></span>

<span data-ttu-id="10d6e-187">藉由提供通知和建議的補救，Identity Protection 有助於即時降低風險。</span><span class="sxs-lookup"><span data-stu-id="10d6e-187">By providing notifications and recommended remediation, Identity Protection helps to mitigate risks in real time.</span></span> <span data-ttu-id="10d6e-188">它會計算使用者風險嚴重性，而且您可以設定風險原則，以自動協助保護應用程式存取免於未來威脅。</span><span class="sxs-lookup"><span data-stu-id="10d6e-188">It calculates user risk severity, and you can configure risk-based policies to automatically help safeguard application access from future threats.</span></span>

<span data-ttu-id="10d6e-189">深入了解：</span><span class="sxs-lookup"><span data-stu-id="10d6e-189">Learn more:</span></span>

* [<span data-ttu-id="10d6e-190">Azure Active Directory Identity Protection</span><span class="sxs-lookup"><span data-stu-id="10d6e-190">Azure Active Directory Identity Protection</span></span>](../active-directory/active-directory-identityprotection.md)
* [<span data-ttu-id="10d6e-191">第 9 頻道：Azure AD 和身分識別展示：Identity Protection 預覽</span><span class="sxs-lookup"><span data-stu-id="10d6e-191">Channel 9: Azure AD and Identity Show: Identity Protection Preview</span></span>](https://channel9.msdn.com/Series/Azure-AD-Identity/Azure-AD-and-Identity-Show-Identity-Protection-Preview)

## <a name="security-center"></a><span data-ttu-id="10d6e-192">資訊安全中心</span><span class="sxs-lookup"><span data-stu-id="10d6e-192">Security Center</span></span>
<span data-ttu-id="10d6e-193">Azure 資訊安全中心可協助您預防、偵測和回應威脅，並加強提供對 Azure 資源安全性的能見度及控制權。</span><span class="sxs-lookup"><span data-stu-id="10d6e-193">Azure Security Center helps you prevent, detect, and respond to threats, and provides you increased visibility into, and control over, the security of your Azure resources.</span></span> <span data-ttu-id="10d6e-194">它提供您 Azure 訂用帳戶之間的整合式安全性監視和原則管理，協助您偵測可能會忽略的威脅，且適用於廣泛的安全性解決方案生態系統。</span><span class="sxs-lookup"><span data-stu-id="10d6e-194">It provides integrated security monitoring and policy management across your Azure subscriptions, helps detect threats that might otherwise go unnoticed, and works with a broad ecosystem of security solutions.</span></span>

<span data-ttu-id="10d6e-195">資訊安全中心藉由下列方式來協助您最佳化和監視 Azure 資源安全性︰</span><span class="sxs-lookup"><span data-stu-id="10d6e-195">Security Center helps you optimize and monitor the security of your Azure resources by:</span></span>

* <span data-ttu-id="10d6e-196">可讓您根據公司安全性需求，以及每個訂用帳戶中的應用程式類型或資料敏感性，為您的 Azure 訂用帳戶資源定義原則。</span><span class="sxs-lookup"><span data-stu-id="10d6e-196">Enabling you to define policies for your Azure subscription resources according to your company’s security needs and the type of applications or sensitivity of the data in each subscription.</span></span>
* <span data-ttu-id="10d6e-197">監視 Azure 虛擬機器、網路和應用程式的狀態。</span><span class="sxs-lookup"><span data-stu-id="10d6e-197">Monitoring the state of your Azure virtual machines, networking, and applications.</span></span>
* <span data-ttu-id="10d6e-198">提供包括來自整合式合作夥伴解決方案的優先安全性警示清單，以及需要您快速調查的資訊，和如何修復攻擊的建議。</span><span class="sxs-lookup"><span data-stu-id="10d6e-198">Providing a list of prioritized security alerts, including alerts from integrated partner solutions, along with the information you need to quickly investigate and recommendations on how to remediate an attack.</span></span>

<span data-ttu-id="10d6e-199">深入了解：</span><span class="sxs-lookup"><span data-stu-id="10d6e-199">Learn more:</span></span>

* [<span data-ttu-id="10d6e-200">Azure 資訊安全中心簡介</span><span class="sxs-lookup"><span data-stu-id="10d6e-200">Introduction to Azure Security Center</span></span>](../security-center/security-center-intro.md)

<!--Image references-->
[1]: ./media/security-management-and-monitoring-overview/shared-responsibility.png
