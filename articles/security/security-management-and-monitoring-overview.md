---
title: "aaaAzure 安全性管理和監視概觀 |Microsoft 文件"
description: " Azure 提供安全性機制 tooaid hello 管理和監視 Azure 雲端服務和虛擬機器中。  本文概述這些核心安全性功能和服務。 "
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
ms.openlocfilehash: 0026fa97bab7e15c9f8de6856b5075abe2288f61
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-security-management-and-monitoring-overview"></a><span data-ttu-id="2db7c-104">Azure 安全性管理和監視概觀</span><span class="sxs-lookup"><span data-stu-id="2db7c-104">Azure Security Management and Monitoring Overview</span></span>
<span data-ttu-id="2db7c-105">Azure 提供安全性機制 tooaid hello 管理和監視 Azure 雲端服務和虛擬機器中。</span><span class="sxs-lookup"><span data-stu-id="2db7c-105">Azure provides security mechanisms tooaid in hello management and monitoring of Azure cloud services and virtual machines.</span></span> <span data-ttu-id="2db7c-106">本文概述這些核心安全性功能和服務。</span><span class="sxs-lookup"><span data-stu-id="2db7c-106">This article provides an overview of these core security features and services.</span></span> <span data-ttu-id="2db7c-107">提供給每個詳細資料，因此，您可以深入的 tooarticles 時，會提供連結。</span><span class="sxs-lookup"><span data-stu-id="2db7c-107">Links are provided tooarticles that give details of each so you can learn more.</span></span>

<span data-ttu-id="2db7c-108">您的 Microsoft 雲端服務的 hello 安全性是合作關係與您與 Microsoft 間共用的責任。</span><span class="sxs-lookup"><span data-stu-id="2db7c-108">hello security of your Microsoft cloud services is a partnership and shared responsibility between you and Microsoft.</span></span> <span data-ttu-id="2db7c-109">共同的責任表示 Microsoft 負責 hello Microsoft Azure 和其資料中心的實體安全性 （透過使用安全性保護，例如鎖定的徽章進入的門、 柵欄和成立條件）。</span><span class="sxs-lookup"><span data-stu-id="2db7c-109">Shared responsibility means Microsoft is responsible for hello Microsoft Azure and physical security of its data centers (by using security protections such as locked badge entry doors, fences, and guards).</span></span> <span data-ttu-id="2db7c-110">此外，Azure 會提供強式符合 hello 安全性、 隱私權和相容性需求的客戶嚴苛的 hello 軟體層級的雲端安全性層級。</span><span class="sxs-lookup"><span data-stu-id="2db7c-110">In addition, Azure provides strong levels of cloud security at hello software layer that meets hello security, privacy, and compliance needs of its demanding customers.</span></span>

<span data-ttu-id="2db7c-111">您擁有您的資料和身分識別、 保護其中的 hello 您在內部部署資源安全性和雲端元件，透過它，您可以控制的安全性，hello hello 責任。</span><span class="sxs-lookup"><span data-stu-id="2db7c-111">You own your data and identities, hello responsibility for protecting them, hello security of your on-premises resources, and hello security of cloud components over which you have control.</span></span> <span data-ttu-id="2db7c-112">Microsoft 提供您與安全性控制項和功能 toohelp 保護資料和應用程式。</span><span class="sxs-lookup"><span data-stu-id="2db7c-112">Microsoft provides you with security controls and capabilities toohelp you protect your data and applications.</span></span> <span data-ttu-id="2db7c-113">維護安全性的責任的程度為基礎的雲端服務的 hello 型別。</span><span class="sxs-lookup"><span data-stu-id="2db7c-113">Your degree of responsibility for security is based on hello type of cloud service.</span></span>

<span data-ttu-id="2db7c-114">下列圖表中的 hello 摘要說明 Microsoft 和 hello 客戶責任 hello 之間取得平衡。</span><span class="sxs-lookup"><span data-stu-id="2db7c-114">hello following chart summarizes hello balance of responsibility for both Microsoft and hello customer.</span></span>

![共同責任][1]

<span data-ttu-id="2db7c-116">若要深入了解安全性管理，請參閱 [Azure 的安全性管理](azure-security-management.md)。</span><span class="sxs-lookup"><span data-stu-id="2db7c-116">For a deeper dive into security management, see [Security management in Azure](azure-security-management.md).</span></span>

<span data-ttu-id="2db7c-117">以下是本文章涵蓋 hello 核心功能 toobe:</span><span class="sxs-lookup"><span data-stu-id="2db7c-117">Here are hello core features toobe covered in this article:</span></span>

* <span data-ttu-id="2db7c-118">角色型存取控制</span><span class="sxs-lookup"><span data-stu-id="2db7c-118">Role-Based Access Control</span></span>
* <span data-ttu-id="2db7c-119">反惡意程式碼</span><span class="sxs-lookup"><span data-stu-id="2db7c-119">Antimalware</span></span>
* <span data-ttu-id="2db7c-120">Multi-Factor Authentication</span><span class="sxs-lookup"><span data-stu-id="2db7c-120">Multi-Factor Authentication</span></span>
* <span data-ttu-id="2db7c-121">ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="2db7c-121">ExpressRoute</span></span>
* <span data-ttu-id="2db7c-122">虛擬網路閘道</span><span class="sxs-lookup"><span data-stu-id="2db7c-122">Virtual network gateways</span></span>
* <span data-ttu-id="2db7c-123">Privileged Identity Management</span><span class="sxs-lookup"><span data-stu-id="2db7c-123">Privileged identity management</span></span>
* <span data-ttu-id="2db7c-124">身分識別保護</span><span class="sxs-lookup"><span data-stu-id="2db7c-124">Identity protection</span></span>
* <span data-ttu-id="2db7c-125">資訊安全中心</span><span class="sxs-lookup"><span data-stu-id="2db7c-125">Security Center</span></span>

## <a name="role-based-access-control"></a><span data-ttu-id="2db7c-126">角色型存取控制</span><span class="sxs-lookup"><span data-stu-id="2db7c-126">Role-Based Access Control</span></span>
<span data-ttu-id="2db7c-127">角色型存取控制 (RBAC) 提供 Azure 資源的更細緻存取權管理。</span><span class="sxs-lookup"><span data-stu-id="2db7c-127">Role-Based Access Control (RBAC) provides fine-grained access management for Azure resources.</span></span> <span data-ttu-id="2db7c-128">使用 RBAC 時，您可以授與人員只 hello 少量的所需 tooperform 工作的存取權。</span><span class="sxs-lookup"><span data-stu-id="2db7c-128">Using RBAC, you can grant people only hello amount of access that they need tooperform their jobs.</span></span>  <span data-ttu-id="2db7c-129">RBAC 也可協助您確保當使用者離開 hello 組織它們會失去存取 tooresources hello 雲端中。</span><span class="sxs-lookup"><span data-stu-id="2db7c-129">RBAC can also help you ensure that when people leave hello organization they lose access tooresources in hello cloud.</span></span>

<span data-ttu-id="2db7c-130">深入了解：</span><span class="sxs-lookup"><span data-stu-id="2db7c-130">Learn more:</span></span>

* [<span data-ttu-id="2db7c-131">有關 RBAC 的 Active Directory 小組部落格</span><span class="sxs-lookup"><span data-stu-id="2db7c-131">Active Directory team blog on RBAC</span></span>](http://i1.blogs.technet.com/b/ad/archive/2015/10/12/azure-rbac-is-ga.aspx)
* [<span data-ttu-id="2db7c-132">Azure 角色型存取控制</span><span class="sxs-lookup"><span data-stu-id="2db7c-132">Azure Role-Based Access Control</span></span>](../active-directory/role-based-access-control-configure.md)

## <a name="antimalware"></a><span data-ttu-id="2db7c-133">反惡意程式碼</span><span class="sxs-lookup"><span data-stu-id="2db7c-133">Antimalware</span></span>
<span data-ttu-id="2db7c-134">有了 Azure，您可以使用反惡意程式碼軟體，例如 Microsoft、 Symantec、 趨勢科技、 McAfee，主要的安全性廠商和 Kaspersky toohelp 來自惡意檔案、 廣告軟體和其他威脅保護您的虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="2db7c-134">With Azure, you can use antimalware software from major security vendors such as Microsoft, Symantec, Trend Micro, McAfee, and Kaspersky toohelp protect your virtual machines from malicious files, adware, and other threats.</span></span>

<span data-ttu-id="2db7c-135">Microsoft 反惡意程式碼提供 hello 能力 tooinstall PaaS 角色和虛擬機器的反惡意程式碼代理程式。</span><span class="sxs-lookup"><span data-stu-id="2db7c-135">Microsoft Antimalware offers you hello ability tooinstall an antimalware agent for both PaaS roles and virtual machines.</span></span> <span data-ttu-id="2db7c-136">根據 System Center Endpoint Protection，這項功能會使經過證實的內部部署安全性技術 toohello 雲端。</span><span class="sxs-lookup"><span data-stu-id="2db7c-136">Based on System Center Endpoint Protection, this feature brings proven on-premises security technology toohello cloud.</span></span>

<span data-ttu-id="2db7c-137">我們也提供深層整合趨勢的[Deep Security](http://www.trendmicro.com/us/enterprise/cloud-solutions/deep-security/)™ 和[SecureCloud](http://www.trendmicro.com/us/enterprise/cloud-solutions/secure-cloud/)™ hello Azure 平台的產品。</span><span class="sxs-lookup"><span data-stu-id="2db7c-137">We also offer deep integration for Trend’s [Deep Security](http://www.trendmicro.com/us/enterprise/cloud-solutions/deep-security/)™ and [SecureCloud](http://www.trendmicro.com/us/enterprise/cloud-solutions/secure-cloud/)™ products in hello Azure platform.</span></span> <span data-ttu-id="2db7c-138">DeepSecurity 是一種防毒解決方案，SecureCloud 則是一種加密解決方案。</span><span class="sxs-lookup"><span data-stu-id="2db7c-138">DeepSecurity is an Antivirus solution and SecureCloud is an encryption solution.</span></span> <span data-ttu-id="2db7c-139">DeepSecurity 會使用擴充功能模型部署在 VM 內。</span><span class="sxs-lookup"><span data-stu-id="2db7c-139">DeepSecurity is deployed inside VMs using an extension model.</span></span> <span data-ttu-id="2db7c-140">使用 hello 入口網站 UI 和 PowerShell，您可以選擇 toouse DeepSecurity 新的 Vm 會被調整大小或已部署的現有 Vm 內。</span><span class="sxs-lookup"><span data-stu-id="2db7c-140">Using hello portal UI and PowerShell, you can choose toouse DeepSecurity inside new VMs that are being spun up, or existing VMs that are already deployed.</span></span>

<span data-ttu-id="2db7c-141">Azure 也支援 Symantec End Point Protection (SEP)。</span><span class="sxs-lookup"><span data-stu-id="2db7c-141">Symantec End Point Protection (SEP) is also supported on Azure.</span></span> <span data-ttu-id="2db7c-142">透過入口網站整合，客戶可以指定其想 toouse 年 9 月，在 VM 內。</span><span class="sxs-lookup"><span data-stu-id="2db7c-142">Through portal integration, customers can specify that they intend toouse SEP within a VM.</span></span> <span data-ttu-id="2db7c-143">9 月可以透過 hello Azure 入口網站的新 VM 上安裝，或可以使用 PowerShell 將現有 VM 上安裝。</span><span class="sxs-lookup"><span data-stu-id="2db7c-143">SEP can be installed on a brand new VM via hello Azure portal or can be installed on an existing VM using PowerShell.</span></span>

<span data-ttu-id="2db7c-144">深入了解：</span><span class="sxs-lookup"><span data-stu-id="2db7c-144">Learn more:</span></span>

* [<span data-ttu-id="2db7c-145">在 Azure 虛擬機器上部署反惡意程式碼解決方案</span><span class="sxs-lookup"><span data-stu-id="2db7c-145">Deploying Antimalware Solutions on Azure Virtual Machines</span></span>](https://azure.microsoft.com/blog/deploying-antimalware-solutions-on-azure-virtual-machines/)
* [<span data-ttu-id="2db7c-146">適用於 Azure 雲端服務和虛擬機器的 Microsoft Antimalware</span><span class="sxs-lookup"><span data-stu-id="2db7c-146">Microsoft Antimalware for Azure Cloud Services and Virtual Machines</span></span>](azure-security-antimalware.md)
* [<span data-ttu-id="2db7c-147">如何 tooinstall 和設定 Trend Micro Deep Security 作為 Windows VM 上的服務</span><span class="sxs-lookup"><span data-stu-id="2db7c-147">How tooinstall and configure Trend Micro Deep Security as a Service on a Windows VM</span></span>](../virtual-machines/windows/classic/install-trend.md)
* [<span data-ttu-id="2db7c-148">如何 tooinstall 及 Windows VM 上設定 Symantec Endpoint Protection</span><span class="sxs-lookup"><span data-stu-id="2db7c-148">How tooinstall and configure Symantec Endpoint Protection on a Windows VM</span></span>](../virtual-machines/windows/classic/install-symantec.md)
* [<span data-ttu-id="2db7c-149">保護 Azure 虛擬機器的新反惡意程式碼選項 - McAfee Endpoint Protection</span><span class="sxs-lookup"><span data-stu-id="2db7c-149">New Antimalware Options for Protecting Azure Virtual Machines – McAfee Endpoint Protection</span></span>](https://azure.microsoft.com/blog/new-antimalware-options-for-protecting-azure-virtual-machines/)

## <a name="multi-factor-authentication"></a><span data-ttu-id="2db7c-150">Multi-Factor Authentication</span><span class="sxs-lookup"><span data-stu-id="2db7c-150">Multi-Factor Authentication</span></span>
<span data-ttu-id="2db7c-151">Azure multi-factor authentication (MFA) 是驗證的程式需要 hello 使用一個以上的驗證方法，並將重要的第二層的安全性 toouser 登入和交易方法。</span><span class="sxs-lookup"><span data-stu-id="2db7c-151">Azure Multi-factor authentication (MFA) is a method of authentication that requires hello use of more than one verification method and adds a critical second layer of security toouser sign-ins and transactions.</span></span> <span data-ttu-id="2db7c-152">MFA 有助於保護存取 toodata 和應用程式，同時滿足簡單登入程序的使用者需求。</span><span class="sxs-lookup"><span data-stu-id="2db7c-152">MFA helps safeguard access toodata and applications while meeting user demand for a simple sign-in process.</span></span> <span data-ttu-id="2db7c-153">它可以透過一些驗證選項 (例如電話、文字訊息，或行動應用程式通知或驗證代碼，以及第三方 OATH 權杖) 來提供強大的驗證功能。</span><span class="sxs-lookup"><span data-stu-id="2db7c-153">It delivers strong authentication via a range of verification options—phone call, text message, or mobile app notification or verification code and third party OATH tokens.</span></span>

<span data-ttu-id="2db7c-154">深入了解：</span><span class="sxs-lookup"><span data-stu-id="2db7c-154">Learn more:</span></span>

* [<span data-ttu-id="2db7c-155">Multi-Factor Authentication</span><span class="sxs-lookup"><span data-stu-id="2db7c-155">Multi-factor authentication</span></span>](https://azure.microsoft.com/documentation/services/multi-factor-authentication/)
* [<span data-ttu-id="2db7c-156">什麼是 Azure Multi-Factor Authentication？</span><span class="sxs-lookup"><span data-stu-id="2db7c-156">What is Azure Multi-Factor Authentication?</span></span>](../multi-factor-authentication/multi-factor-authentication.md)
* [<span data-ttu-id="2db7c-157">Azure Multi-Factor Authentication 的作用</span><span class="sxs-lookup"><span data-stu-id="2db7c-157">How Azure Multi-Factor Authentication works</span></span>](../multi-factor-authentication/multi-factor-authentication-how-it-works.md)

## <a name="expressroute"></a><span data-ttu-id="2db7c-158">ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="2db7c-158">ExpressRoute</span></span>
<span data-ttu-id="2db7c-159">Microsoft Azure ExpressRoute 可讓您將您在內部部署網路擴充至 hello Microsoft 雲端中，透過連線服務提供者所提供的專用私人連接。</span><span class="sxs-lookup"><span data-stu-id="2db7c-159">Microsoft Azure ExpressRoute lets you extend your on-premises networks into hello Microsoft cloud over a dedicated private connection facilitated by a connectivity provider.</span></span> <span data-ttu-id="2db7c-160">透過 ExpressRoute，您可以建立連線 tooMicrosoft 雲端服務，例如 Microsoft Azure、 Office 365 和 CRM Online。</span><span class="sxs-lookup"><span data-stu-id="2db7c-160">With ExpressRoute, you can establish connections tooMicrosoft cloud services, such as Microsoft Azure, Office 365, and CRM Online.</span></span> <span data-ttu-id="2db7c-161">從任意點對任意點 (IP VPN) 網路、點對點乙太網路，或在共置設施上透過連線提供者的虛擬交叉連接，都可以進行連線。</span><span class="sxs-lookup"><span data-stu-id="2db7c-161">Connectivity can be from an any-to-any (IP VPN) network, a point-to-point Ethernet network, or a virtual cross-connection through a connectivity provider at a co-location facility.</span></span> <span data-ttu-id="2db7c-162">ExpressRoute 連線不會經過 hello 公用網際網路。</span><span class="sxs-lookup"><span data-stu-id="2db7c-162">ExpressRoute connections do not go over hello public Internet.</span></span> <span data-ttu-id="2db7c-163">這可讓 ExpressRoute 連線 toooffer 詳細可靠性、 速度、 延遲更少和較高的安全性比一般連線透過網際網路 hello。</span><span class="sxs-lookup"><span data-stu-id="2db7c-163">This allows ExpressRoute connections toooffer more reliability, faster speeds, lower latencies, and higher security than typical connections over hello Internet.</span></span>

<span data-ttu-id="2db7c-164">深入了解：</span><span class="sxs-lookup"><span data-stu-id="2db7c-164">Learn more:</span></span>

* [<span data-ttu-id="2db7c-165">ExpressRoute 技術概觀</span><span class="sxs-lookup"><span data-stu-id="2db7c-165">ExpressRoute technical overview</span></span>](../expressroute/expressroute-introduction.md)

## <a name="virtual-network-gateways"></a><span data-ttu-id="2db7c-166">虛擬網路閘道</span><span class="sxs-lookup"><span data-stu-id="2db7c-166">Virtual network gateways</span></span>
<span data-ttu-id="2db7c-167">使用 VPN 閘道，也稱為 Azure 虛擬網路閘道，toosend 虛擬網路與內部部署位置之間的網路流量。</span><span class="sxs-lookup"><span data-stu-id="2db7c-167">VPN Gateways, also called Azure Virtual Network Gateways, are used toosend network traffic between virtual networks and on-premises locations.</span></span> <span data-ttu-id="2db7c-168">它們也是使用的 toosend Azure (VNet 對 VNet) 內的多個虛擬網路之間的流量。</span><span class="sxs-lookup"><span data-stu-id="2db7c-168">They are also used toosend traffic between multiple virtual networks within Azure (VNet-to-VNet).</span></span>  <span data-ttu-id="2db7c-169">VPN 閘道提供 Azure 與基礎結構之間的跨單位安全連線。</span><span class="sxs-lookup"><span data-stu-id="2db7c-169">VPN gateways provide secure cross-premises connectivity between Azure and your infrastructure.</span></span>

<span data-ttu-id="2db7c-170">深入了解：</span><span class="sxs-lookup"><span data-stu-id="2db7c-170">Learn more:</span></span>

* [<span data-ttu-id="2db7c-171">關於 VPN 閘道</span><span class="sxs-lookup"><span data-stu-id="2db7c-171">About VPN gateways</span></span>](../vpn-gateway/vpn-gateway-about-vpngateways.md)
* [<span data-ttu-id="2db7c-172">Azure 網路安全性概觀</span><span class="sxs-lookup"><span data-stu-id="2db7c-172">Azure Network Security Overview</span></span>](security-network-overview.md)

## <a name="privileged-identity-management"></a><span data-ttu-id="2db7c-173">Privileged Identity Management</span><span class="sxs-lookup"><span data-stu-id="2db7c-173">Privileged Identity Management</span></span>
<span data-ttu-id="2db7c-174">有時候使用者需要 toocarry 特殊權限的 Azure 資源或其他 SaaS 應用程式中的作業。</span><span class="sxs-lookup"><span data-stu-id="2db7c-174">Sometimes users need toocarry out privileged operations in Azure resources or other SaaS applications.</span></span> <span data-ttu-id="2db7c-175">這通常表示的組織有 toogive 它們的永久特殊權限存取 Azure Active Directory (Azure AD) 中。</span><span class="sxs-lookup"><span data-stu-id="2db7c-175">This often means organizations have toogive them permanent privileged access in Azure Active Directory (Azure AD).</span></span> <span data-ttu-id="2db7c-176">這會提高雲端資源的安全性風險，因為組織無法滴水不漏地監視這些使用者利用其特殊存取權限的所作所為。</span><span class="sxs-lookup"><span data-stu-id="2db7c-176">This is a growing security risk for cloud-hosted resources because organizations can't sufficiently monitor what those users are doing with their privileged access.</span></span>
<span data-ttu-id="2db7c-177">此外，如果擁有特殊存取權限的使用者帳戶遭到入侵，這個缺口可能會影響您的整體雲端安全性。</span><span class="sxs-lookup"><span data-stu-id="2db7c-177">Additionally, if a user account with privileged access is compromised, that one breach could impact your overall cloud security.</span></span> <span data-ttu-id="2db7c-178">Azure AD Privileged Identity Management 的十分有助於 tooresolve 這項風險降低的權限的 hello 曝光時間並增加可見性使用方式。</span><span class="sxs-lookup"><span data-stu-id="2db7c-178">Azure AD Privileged Identity Management helps tooresolve this risk by lowering hello exposure time of privileges and increasing visibility into usage.</span></span>  

<span data-ttu-id="2db7c-179">Privileged 的 Identity Management 引進了暫時的系統管理員角色或 「 及時 」 系統管理員存取權，也就是需要的 toocomplete 的啟用程序指派給角色的使用者 hello 概念。</span><span class="sxs-lookup"><span data-stu-id="2db7c-179">Privileged Identity Management introduces hello concept of a temporary admin for a role or “just in time” administrator access, which is a user who needs toocomplete an activation process for that assigned role.</span></span> <span data-ttu-id="2db7c-180">hello 啟動處理程序變更 hello 非作用中 tooactive，從指定的時間週期，例如八個小時的 Azure AD 中的 hello 使用者 tooa 角色指派。</span><span class="sxs-lookup"><span data-stu-id="2db7c-180">hello activation process changes hello assignment of hello user tooa role in Azure AD from inactive tooactive, for a specified time period such as eight hours.</span></span>

<span data-ttu-id="2db7c-181">深入了解：</span><span class="sxs-lookup"><span data-stu-id="2db7c-181">Learn more:</span></span>

* [<span data-ttu-id="2db7c-182">Azure AD 特殊權限身分識別管理</span><span class="sxs-lookup"><span data-stu-id="2db7c-182">Azure AD Privileged Identity Management</span></span>](../active-directory/active-directory-privileged-identity-management-configure.md)
* [<span data-ttu-id="2db7c-183">開始使用 Azure AD Privileged Identity Management</span><span class="sxs-lookup"><span data-stu-id="2db7c-183">Get started with Azure AD Privileged Identity Management</span></span>](../active-directory/active-directory-privileged-identity-management-getting-started.md)

## <a name="identity-protection"></a><span data-ttu-id="2db7c-184">身分識別保護</span><span class="sxs-lookup"><span data-stu-id="2db7c-184">Identity Protection</span></span>
<span data-ttu-id="2db7c-185">Azure Active Directory (AD) 的識別身分保護，提供合併的檢視可疑的登入活動和潛在弱點 toohelp 保護您的業務。</span><span class="sxs-lookup"><span data-stu-id="2db7c-185">Azure Active Directory (AD) Identity Protection provides a consolidated view of suspicious sign-in activities and potential vulnerabilities toohelp protect your business.</span></span> <span data-ttu-id="2db7c-186">Identity Protection 會依據跡象偵測使用者和特權 (系統管理員) 身分識別的可疑活動，例如暴力密碼破解攻擊、認證外洩，以及從不明位置或受感染裝置的登入。</span><span class="sxs-lookup"><span data-stu-id="2db7c-186">Identity Protection detects suspicious activities for users and privileged (admin) identities, based on signals like brute-force attacks, leaked credentials, and sign-ins from unfamiliar locations and infected devices.</span></span>

<span data-ttu-id="2db7c-187">藉由提供通知，並建議的補救，識別項保護有助於即時 toomitigate 風險。</span><span class="sxs-lookup"><span data-stu-id="2db7c-187">By providing notifications and recommended remediation, Identity Protection helps toomitigate risks in real time.</span></span> <span data-ttu-id="2db7c-188">它會計算使用者風險嚴重性，並且可以設定風險原則 tooautomatically 保護應用程式存取說明從未來的威脅。</span><span class="sxs-lookup"><span data-stu-id="2db7c-188">It calculates user risk severity, and you can configure risk-based policies tooautomatically help safeguard application access from future threats.</span></span>

<span data-ttu-id="2db7c-189">深入了解：</span><span class="sxs-lookup"><span data-stu-id="2db7c-189">Learn more:</span></span>

* [<span data-ttu-id="2db7c-190">Azure Active Directory Identity Protection</span><span class="sxs-lookup"><span data-stu-id="2db7c-190">Azure Active Directory Identity Protection</span></span>](../active-directory/active-directory-identityprotection.md)
* [<span data-ttu-id="2db7c-191">第 9 頻道：Azure AD 和身分識別展示：Identity Protection 預覽</span><span class="sxs-lookup"><span data-stu-id="2db7c-191">Channel 9: Azure AD and Identity Show: Identity Protection Preview</span></span>](https://channel9.msdn.com/Series/Azure-AD-Identity/Azure-AD-and-Identity-Show-Identity-Protection-Preview)

## <a name="security-center"></a><span data-ttu-id="2db7c-192">資訊安全中心</span><span class="sxs-lookup"><span data-stu-id="2db7c-192">Security Center</span></span>
<span data-ttu-id="2db7c-193">Azure 資訊安全中心可協助您防止、 偵測，並回應 toothreats，，並提供您增加可見性，並控制、 hello 安全性的 Azure 資源。</span><span class="sxs-lookup"><span data-stu-id="2db7c-193">Azure Security Center helps you prevent, detect, and respond toothreats, and provides you increased visibility into, and control over, hello security of your Azure resources.</span></span> <span data-ttu-id="2db7c-194">它提供您 Azure 訂用帳戶之間的整合式安全性監視和原則管理，協助您偵測可能會忽略的威脅，且適用於廣泛的安全性解決方案生態系統。</span><span class="sxs-lookup"><span data-stu-id="2db7c-194">It provides integrated security monitoring and policy management across your Azure subscriptions, helps detect threats that might otherwise go unnoticed, and works with a broad ecosystem of security solutions.</span></span>

<span data-ttu-id="2db7c-195">資訊安全中心可協助您最佳化及監視您的 Azure 資源的 hello 安全性：</span><span class="sxs-lookup"><span data-stu-id="2db7c-195">Security Center helps you optimize and monitor hello security of your Azure resources by:</span></span>

* <span data-ttu-id="2db7c-196">讓您針對您的 Azure 訂用帳戶資源，根據 tooyour toodefine 原則公司的安全性需要而且 hello 的應用程式類型或大小寫的每個訂用帳戶中的 hello 資料。</span><span class="sxs-lookup"><span data-stu-id="2db7c-196">Enabling you toodefine policies for your Azure subscription resources according tooyour company’s security needs and hello type of applications or sensitivity of hello data in each subscription.</span></span>
* <span data-ttu-id="2db7c-197">監視 Azure 虛擬機器、 網路功能和應用程式的 hello 狀態。</span><span class="sxs-lookup"><span data-stu-id="2db7c-197">Monitoring hello state of your Azure virtual machines, networking, and applications.</span></span>
* <span data-ttu-id="2db7c-198">提供一份排列安全性警示，包括從整合式的解決方案，以及您需要 tooquickly hello 資訊調查的夥伴和建議的警示 tooremediate 攻擊。</span><span class="sxs-lookup"><span data-stu-id="2db7c-198">Providing a list of prioritized security alerts, including alerts from integrated partner solutions, along with hello information you need tooquickly investigate and recommendations on how tooremediate an attack.</span></span>

<span data-ttu-id="2db7c-199">深入了解：</span><span class="sxs-lookup"><span data-stu-id="2db7c-199">Learn more:</span></span>

* [<span data-ttu-id="2db7c-200">簡介 tooAzure 資訊安全中心</span><span class="sxs-lookup"><span data-stu-id="2db7c-200">Introduction tooAzure Security Center</span></span>](../security-center/security-center-intro.md)

<!--Image references-->
[1]: ./media/security-management-and-monitoring-overview/shared-responsibility.png
