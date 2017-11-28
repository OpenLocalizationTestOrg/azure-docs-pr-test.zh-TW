---
title: "使用 MFA NPS 擴充功能來整合遠端桌面閘道 | Microsoft Docs"
description: "本文探討如何使用 Microsoft Azure 的網路原則伺服器 (NPS) 擴充功能來整合遠端桌面閘道基礎結構與 Azure MFA。"
services: active-directory
keywords: "Azure MFA, 整合遠端桌面閘道, Azure Active Directory, 網路原則伺服器擴充功能"
documentationcenter: 
author: kgremban
manager: femila
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/15/2017
ms.author: kgremban
ms.reviewer: jsnow
ms.custom: it-pro
ms.openlocfilehash: 6ff9a341b31e5005949dcc0ecb2591060269846e
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/18/2017
---
#  <a name="integrate-your-remote-desktop-gateway-infrastructure-using-the-network-policy-server-nps-extension-and-azure-ad"></a><span data-ttu-id="03820-104">使用網路原則伺服器 (NPS) 擴充功能和 Azure AD 整合遠端桌面閘道基礎結構</span><span class="sxs-lookup"><span data-stu-id="03820-104">Integrate your Remote Desktop Gateway infrastructure using the Network Policy Server (NPS) extension and Azure AD</span></span>

<span data-ttu-id="03820-105">本文提供使用 Microsoft Azure 的網路原則伺服器 (NPS) 擴充功能來整合遠端桌面閘道基礎結構與 Azure Multi-Factor Authentication (MFA) 的詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="03820-105">This article provides details for integrating your Remote Desktop Gateway infrastructure with Azure Multi-Factor Authentication (MFA) using the Network Policy Server (NPS) extension for Microsoft Azure.</span></span> 

<span data-ttu-id="03820-106">Azure 的網路原則服務 (NPS) 擴充功能可讓客戶使用 Azure 以雲端為基礎的 [Multi-Factor Authentication (MFA)](multi-factor-authentication.md) 來保護遠端驗證撥入使用者服務 (RADIUS) 用戶端驗證。</span><span class="sxs-lookup"><span data-stu-id="03820-106">The Network Policy Service (NPS) extension for Azure allows customers to safeguard Remote Authentication Dial-In User Service (RADIUS) client authentication using Azure’s cloud-based [Multi-Factor Authentication (MFA)](multi-factor-authentication.md).</span></span> <span data-ttu-id="03820-107">此解決方案提供雙步驟驗證，以便為使用者登入和交易增加第二層安全性。</span><span class="sxs-lookup"><span data-stu-id="03820-107">This solution provides two-step verification for adding a second layer of security to user sign-ins and transactions.</span></span>

<span data-ttu-id="03820-108">本文提供逐步指示，引導您使用 Azure 的 NPS 擴充功能來整合 NPS 基礎結構與 Azure MFA。</span><span class="sxs-lookup"><span data-stu-id="03820-108">This article provides step-by-step instructions for integrating the NPS infrastructure with Azure MFA using the NPS extension for Azure.</span></span> <span data-ttu-id="03820-109">這可為嘗試登入遠端桌面閘道的使用者能夠安全地進行驗證。</span><span class="sxs-lookup"><span data-stu-id="03820-109">This enables secure verification for users attempting to log on to a Remote Desktop Gateway.</span></span> 

<span data-ttu-id="03820-110">網路原則與存取服務 (NPS) 為組織提供執行下列作業的能力：</span><span class="sxs-lookup"><span data-stu-id="03820-110">The Network Policy and Access Services (NPS) gives organizations the ability to do the following:</span></span>
* <span data-ttu-id="03820-111">定義中央位置以供管理和控制網路要求，方法是指出誰可以連線、每天的哪些時段允許連線、連線的持續時間，以及用戶端在連線時必須使用的安全性層級等等。</span><span class="sxs-lookup"><span data-stu-id="03820-111">Define central locations for the management and control of network requests by specifying who can connect, what times of day connections are allowed, the duration of connections, and the level of security that clients must use to connect, and so on.</span></span> <span data-ttu-id="03820-112">組織不必在每個 VPN 或遠端桌面 (RD) 閘道伺服器上指定這些原則，而是在中央位置一次指定這些原則。</span><span class="sxs-lookup"><span data-stu-id="03820-112">Rather than specifying these policies on each VPN or Remote Desktop (RD) Gateway server, these policies can be specified once in a central location.</span></span> <span data-ttu-id="03820-113">RADIUS 通訊協定可提供集中式的驗證、授權和計量 (AAA)。</span><span class="sxs-lookup"><span data-stu-id="03820-113">The RADIUS protocol provides the centralized Authentication, Authorization, and Accounting (AAA).</span></span> 
* <span data-ttu-id="03820-114">建立並強制執行網路存取保護 (NAP) 用戶端健康原則，以判斷要讓裝置不受限制還是受限制地存取網路資源。</span><span class="sxs-lookup"><span data-stu-id="03820-114">Establish and enforce Network Access Protection (NAP) client health policies that determine whether devices are granted unrestricted or restricted access to network resources.</span></span>
* <span data-ttu-id="03820-115">提供強制驗證和授權的方法，以供存取具有 802.1x 功能的無線存取點及乙太網路交換器。</span><span class="sxs-lookup"><span data-stu-id="03820-115">Provide a means to enforce authentication and authorization for access to 802.1x-capable wireless access points and Ethernet switches.</span></span>    

<span data-ttu-id="03820-116">組織通常會使用 NPS (RADIUS) 來簡化和集中管理 VPN 原則。</span><span class="sxs-lookup"><span data-stu-id="03820-116">Typically, organizations use NPS (RADIUS) to simplify and centralize the management of VPN polices.</span></span> <span data-ttu-id="03820-117">不過，許多組織也會使用 NPS 來簡化和集中管理 RD 桌面連線授權原則 (RD CAP)。</span><span class="sxs-lookup"><span data-stu-id="03820-117">However, many organizations also use NPS to simplify and centralize the management of RD Desktop Connection Authorization Policies (RD CAPs).</span></span> 

<span data-ttu-id="03820-118">組織也可以整合 NPS 與 Azure MFA 來增強安全性，並提供高層級的合規性。</span><span class="sxs-lookup"><span data-stu-id="03820-118">Organizations can also integrate NPS with Azure MFA to enhance security and provide a high level of compliance.</span></span> <span data-ttu-id="03820-119">這有助於確保使用者建立雙步驟驗證來登入遠端桌面閘道。</span><span class="sxs-lookup"><span data-stu-id="03820-119">This helps ensure that users establish two-step verification to log on to the Remote Desktop Gateway.</span></span> <span data-ttu-id="03820-120">使用者若要獲得存取權，就必須提供其使用者名稱/密碼的組合以及使用者所掌握的資訊。</span><span class="sxs-lookup"><span data-stu-id="03820-120">For users to be granted access, they must provide their username/password combination with information that the user has in their control.</span></span> <span data-ttu-id="03820-121">這項資訊必須能夠讓人信任且無法輕易複製，例如行動電話號碼、室內電話號碼、行動裝置上的應用程式等等。</span><span class="sxs-lookup"><span data-stu-id="03820-121">This information must be trusted and not easily duplicated, such as a cell phone number, landline number, application on a mobile device, and so on.</span></span>

<span data-ttu-id="03820-122">在 Azure 的 NPS 擴充功能推出前，想要對整合式的 NPS 與 Azure MFA 環境實作雙步驟驗證的客戶，必須在內部部署環境中另外設定及維護一個 MFA Server，如[使用 RADIUS 的遠端桌面閘道和 Azure Multi-Factor Authentication Server](multi-factor-authentication-get-started-server-rdg.md)所述。</span><span class="sxs-lookup"><span data-stu-id="03820-122">Prior to the availability of the NPS extension for Azure, customers who wished to implement two-step verification for integrated NPS and Azure MFA environments had to configure and maintain a separate MFA Server in the on-premises environment as documented in [Remote Desktop Gateway and Azure Multi-Factor Authentication Server using RADIUS](multi-factor-authentication-get-started-server-rdg.md).</span></span>

<span data-ttu-id="03820-123">隨著 Azure 的 NPS 擴充功能推出，組織現在可以選擇要部署內部部署型 MFA 解決方案還是雲端型 MFA 解決方案，以保護 RADIUS 用戶端驗證。</span><span class="sxs-lookup"><span data-stu-id="03820-123">The availability of the NPS extension for Azure now gives organizations the choice to deploy either an on-premises based MFA solution or a cloud-based MFA solution to secure RADIUS client authentication.</span></span>

## <a name="authentication-flow"></a><span data-ttu-id="03820-124">驗證流程</span><span class="sxs-lookup"><span data-stu-id="03820-124">Authentication Flow</span></span>

<span data-ttu-id="03820-125">對於要取得透過遠端桌面閘道存取網路資源之權限的使用者，他們必須符合在一個 RD 連線授權原則 (RD CAP) 和一個 RD 資源授權原則 (RD RAP) 中所指定的條件。</span><span class="sxs-lookup"><span data-stu-id="03820-125">For users to be granted access to network resources through a Remote Desktop Gateway, they must meet the conditions specified in one RD Connection Authorization Policy (RD CAP) and one RD Resource Authorization Policy (RD RAP).</span></span> <span data-ttu-id="03820-126">RD CAP 指定誰獲得授權連線到 RD 閘道。</span><span class="sxs-lookup"><span data-stu-id="03820-126">RD CAPs specify who is authorized to connect to RD Gateways.</span></span> <span data-ttu-id="03820-127">RD RAP 指定允許使用者透過 RD 閘道連線的網路資源，例如遠端桌面或遠端應用程式。</span><span class="sxs-lookup"><span data-stu-id="03820-127">RD RAPs specify the network resources, such as remote desktops or remote apps, that the user is allowed to connect to through the RD Gateway.</span></span> 

<span data-ttu-id="03820-128">您可以將 RD 閘道設定為對 RD CAP 使用中央原則存放區。</span><span class="sxs-lookup"><span data-stu-id="03820-128">An RD Gateway can be configured to use a central policy store for RD CAPs.</span></span> <span data-ttu-id="03820-129">RD RAP 無法使用中央原則，因為它們會在 RD 閘道上進行處理。</span><span class="sxs-lookup"><span data-stu-id="03820-129">RD RAPs cannot use a central policy, as they are processed on the RD Gateway.</span></span> <span data-ttu-id="03820-130">另一部當作中央原則存放區之 NPS 伺服器的 RADIUS 用戶端，即為設定要為對 RD CAP 使用中央原則存放區的 RD 閘道範例之一。</span><span class="sxs-lookup"><span data-stu-id="03820-130">An example of an RD Gateway configured to use a central policy store for RD CAPs is a RADIUS client to another NPS server that serves as the central policy store.</span></span>

<span data-ttu-id="03820-131">當 Azure 的 NPS 擴充功能與 NPS 和遠端桌面閘道整合時，成功的驗證流程如下所示：</span><span class="sxs-lookup"><span data-stu-id="03820-131">When the NPS extension for Azure is integrated with the NPS and Remote Desktop Gateway, the successful authentication flow is as follows:</span></span>

1. <span data-ttu-id="03820-132">遠端桌面閘道伺服器會收到遠端桌面使用者要連線到某項資源 (例如遠端桌面工作階段) 的驗證要求。</span><span class="sxs-lookup"><span data-stu-id="03820-132">The Remote Desktop Gateway server receives an authentication request from a remote desktop user to connect to a resource, such as a Remote Desktop session.</span></span> <span data-ttu-id="03820-133">作為 RADIUS 用戶端的遠端桌面閘道伺服器，會將此要求轉換為 RADIUS Access-Request 訊息，並將此訊息傳送至 NPS 擴充功能安裝所在的 RADIUS (NPS) 伺服器。</span><span class="sxs-lookup"><span data-stu-id="03820-133">Acting as a RADIUS client, the Remote Desktop Gateway server converts the request to a RADIUS Access-Request message and sends the message to the RADIUS (NPS) server where the NPS extension is installed.</span></span> 
2. <span data-ttu-id="03820-134">使用者名稱和密碼組合會在 Active Directory 中進行驗證，且使用者已經過驗證。</span><span class="sxs-lookup"><span data-stu-id="03820-134">The username and password combination is verified in Active Directory and the user is authenticated.</span></span>
3. <span data-ttu-id="03820-135">如果 NPS 連線要求與網路原則中所指定的所有條件 (例如，一天當中的時間或群組成員資格限制) 皆能符合，NPS 擴充功能就會觸發要求，以便使用 Azure MFA 進行第二項驗證。</span><span class="sxs-lookup"><span data-stu-id="03820-135">If all the conditions as specified in the NPS Connection Request and the Network Policies are met (for example, time of day or group membership restrictions), the NPS extension triggers a request for secondary authentication with Azure MFA.</span></span> 
4. <span data-ttu-id="03820-136">Azure MFA 會與 Azure AD 通訊、擷取使用者的詳細資料，並使用使用者所設定的方法執行第二項驗證 (簡訊、行動裝置應用程式等等)。</span><span class="sxs-lookup"><span data-stu-id="03820-136">Azure MFA communicates with Azure AD, retrieves the user’s details, and performs the secondary authentication using the method configured by the user (text message, mobile app, and so on).</span></span> 
5. <span data-ttu-id="03820-137">成功通過 MFA 挑戰後，Azure MFA 會將結果告知 NPS 擴充功能。</span><span class="sxs-lookup"><span data-stu-id="03820-137">Upon success of the MFA challenge, Azure MFA communicates the result to the NPS extension.</span></span>
6. <span data-ttu-id="03820-138">安裝擴充功能的 NPS 伺服器會將 RD CAP 原則的 RADIUS Access-Accept 訊息傳送至遠端桌面閘道伺服器。</span><span class="sxs-lookup"><span data-stu-id="03820-138">The NPS server where the extension is installed sends a RADIUS Access-Accept message for the RD CAP policy to the Remote Desktop Gateway server.</span></span>
7. <span data-ttu-id="03820-139">使用者便取得透過 RD 閘道存取要求之網路資源的權限。</span><span class="sxs-lookup"><span data-stu-id="03820-139">The user is granted access to the requested network resource through the RD Gateway.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="03820-140">必要條件</span><span class="sxs-lookup"><span data-stu-id="03820-140">Prerequisites</span></span>
<span data-ttu-id="03820-141">本節會詳述在整合 Azure MFA 與遠端桌面閘道之前所需具備的必要條件。</span><span class="sxs-lookup"><span data-stu-id="03820-141">This section details the prerequisites necessary before integrating Azure MFA with the Remote Desktop Gateway.</span></span> <span data-ttu-id="03820-142">開始之前，您必須先具備下列必要條件。</span><span class="sxs-lookup"><span data-stu-id="03820-142">Before you begin, you must have the following prerequisites in place.</span></span>  

* <span data-ttu-id="03820-143">遠端桌面服務 (RDS) 基礎結構</span><span class="sxs-lookup"><span data-stu-id="03820-143">Remote Desktop Services (RDS) infrastructure</span></span>
* <span data-ttu-id="03820-144">Azure MFA 授權</span><span class="sxs-lookup"><span data-stu-id="03820-144">Azure MFA License</span></span>
* <span data-ttu-id="03820-145">Windows Server 軟體</span><span class="sxs-lookup"><span data-stu-id="03820-145">Windows Server software</span></span>
* <span data-ttu-id="03820-146">網路原則與存取服務 (NPS) 角色</span><span class="sxs-lookup"><span data-stu-id="03820-146">Network Policy and Access Services (NPS) role</span></span>
* <span data-ttu-id="03820-147">與內部部署 AD 同步的 Azure AD</span><span class="sxs-lookup"><span data-stu-id="03820-147">Azure AD synched with on-premises AD</span></span> 
* <span data-ttu-id="03820-148">Azure Active Directory GUID 識別碼</span><span class="sxs-lookup"><span data-stu-id="03820-148">Azure Active Directory GUID ID</span></span>

### <a name="remote-desktop-services-rds-infrastructure"></a><span data-ttu-id="03820-149">遠端桌面服務 (RDS) 基礎結構</span><span class="sxs-lookup"><span data-stu-id="03820-149">Remote Desktop Services (RDS) infrastructure</span></span>
<span data-ttu-id="03820-150">您必須備妥中運作中的遠端桌面服務 (RDS) 基礎結構。</span><span class="sxs-lookup"><span data-stu-id="03820-150">You must have a working Remote Desktop Services (RDS) infrastructure in place.</span></span> <span data-ttu-id="03820-151">如果您未這麼做，您可以使用下列快速入門範本，在 Azure 中快速建立此基礎結構：[建立遠端桌面工作階段集合部署](https://github.com/Azure/azure-quickstart-templates/tree/ad20c78b36d8e1246f96bb0e7a8741db481f957f/rds-deployment)。</span><span class="sxs-lookup"><span data-stu-id="03820-151">If you do not, then you can quickly create this infrastructure in Azure using the following quick start template: [Create Remote Desktop Session Collection deployment](https://github.com/Azure/azure-quickstart-templates/tree/ad20c78b36d8e1246f96bb0e7a8741db481f957f/rds-deployment).</span></span> 

<span data-ttu-id="03820-152">如果您想要以手動方式快速建立內部部署 RDS 基礎結構以供測試，請遵循下列步驟來部署一個。</span><span class="sxs-lookup"><span data-stu-id="03820-152">If you wish to manually create an on-premises RDS infrastructure quickly for testing purposes, follow the steps to deploy one.</span></span> 
<span data-ttu-id="03820-153">**深入了解**：[使用 Azure 快速入門部署 RDS](https://docs.microsoft.com/windows-server/remote/remote-desktop-services/rds-in-azure)和[基本 RDS 基礎結構部署](https://docs.microsoft.com/windows-server/remote/remote-desktop-services/rds-deploy-infrastructure)。</span><span class="sxs-lookup"><span data-stu-id="03820-153">**Learn more**: [Deploy RDS with Azure quick start](https://docs.microsoft.com/windows-server/remote/remote-desktop-services/rds-in-azure) and [Basic RDS infrastructure deployment](https://docs.microsoft.com/windows-server/remote/remote-desktop-services/rds-deploy-infrastructure).</span></span> 

### <a name="licenses"></a><span data-ttu-id="03820-154">授權</span><span class="sxs-lookup"><span data-stu-id="03820-154">Licenses</span></span>
<span data-ttu-id="03820-155">需要 Azure MFA 的授權，此授權可透過 Azure AD Premium、Enterprise Mobility plus Security (EMS) 或 MFA 訂用帳戶來獲得。</span><span class="sxs-lookup"><span data-stu-id="03820-155">Required is a license for Azure MFA, which is available through an Azure AD Premium, Enterprise Mobility plus Security (EMS), or an MFA subscription.</span></span> <span data-ttu-id="03820-156">如需詳細資訊，請參閱[如何取得 Azure Multi-Factor Authentication](multi-factor-authentication-versions-plans.md)。</span><span class="sxs-lookup"><span data-stu-id="03820-156">For more information, see [How to get Azure Multi-Factor Authentication](multi-factor-authentication-versions-plans.md).</span></span> <span data-ttu-id="03820-157">若要進行測試，您可以使用試用版訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="03820-157">For testing purposes, you can use a trial subscription.</span></span>

### <a name="software"></a><span data-ttu-id="03820-158">軟體</span><span class="sxs-lookup"><span data-stu-id="03820-158">Software</span></span>
<span data-ttu-id="03820-159">NPS 擴充功能需要安裝了 NPS 角色服務的 Windows Server 2008 R2 SP1 或更新版本。</span><span class="sxs-lookup"><span data-stu-id="03820-159">The NPS extension requires Windows Server 2008 R2 SP1 or above with the NPS role service installed.</span></span> <span data-ttu-id="03820-160">這一節中的所有步驟均使用 Windows Server 2016 來執行。</span><span class="sxs-lookup"><span data-stu-id="03820-160">All the steps in this section were performed using Windows Server 2016.</span></span>

### <a name="network-policy-and-access-services-nps-role"></a><span data-ttu-id="03820-161">網路原則與存取服務 (NPS) 角色</span><span class="sxs-lookup"><span data-stu-id="03820-161">Network Policy and Access Services (NPS) role</span></span>
<span data-ttu-id="03820-162">NPS 角色服務可提供 RADIUS 伺服器和用戶端功能，以及網路存取原則健康情況服務。</span><span class="sxs-lookup"><span data-stu-id="03820-162">The NPS role service provides the RADIUS server and client functionality as well as Network Access Policy health service.</span></span> <span data-ttu-id="03820-163">此角色必須安裝於您基礎結構中的至少兩部電腦上：遠端桌面閘道和另一個成員伺服器或網域控制站。</span><span class="sxs-lookup"><span data-stu-id="03820-163">This role must be installed on at least two computers in your infrastructure: The Remote Desktop Gateway and another member server or domain controller.</span></span> <span data-ttu-id="03820-164">根據預設，此角色已存在於設定為遠端桌面閘道的電腦上。</span><span class="sxs-lookup"><span data-stu-id="03820-164">By default, the role is already present on the computer configured as the Remote Desktop Gateway.</span></span>  <span data-ttu-id="03820-165">您也必須至少在另一部電腦 (例如網域控制站或成員伺服器) 上安裝 NPS 角色。</span><span class="sxs-lookup"><span data-stu-id="03820-165">You must also install the NPS role on at least on another computer, such as a domain controller or member server.</span></span>

<span data-ttu-id="03820-166">如需有關安裝 NPS 角色服務 Windows Server 2012 或更舊版本的資訊，請參閱[安裝 NAP 健康原則伺服器](https://technet.microsoft.com/library/dd296890.aspx)。</span><span class="sxs-lookup"><span data-stu-id="03820-166">For information on installing the NPS role service Windows Server 2012 or older, see [Install a NAP Health Policy Server](https://technet.microsoft.com/library/dd296890.aspx).</span></span> <span data-ttu-id="03820-167">如需 NPS 最佳做法的說明 (包括在網域控制站上安裝 NPS 的建議)，請參閱 [NPS 的最佳做法](https://technet.microsoft.com/library/cc771746)。</span><span class="sxs-lookup"><span data-stu-id="03820-167">For a description of best practices for NPS, including the recommendation to install NPS on a domain controller, see [Best Practices for NPS](https://technet.microsoft.com/library/cc771746).</span></span>

### <a name="azure-active-directory-synched-with-on-premises-active-directory"></a><span data-ttu-id="03820-168">與內部部署 Active Directory 同步的 Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="03820-168">Azure Active Directory synched with on-premises Active Directory</span></span> 
<span data-ttu-id="03820-169">若要使用 NPS 擴充功能，內部部署使用者必須與 Azure AD 保持同步並啟用 MFA。</span><span class="sxs-lookup"><span data-stu-id="03820-169">To use the NPS extension, on-premises users must be synced with Azure AD and enabled for MFA.</span></span> <span data-ttu-id="03820-170">這一節假設內部部署使用者已使用 AD Connect 來與 Azure AD 保持同步。</span><span class="sxs-lookup"><span data-stu-id="03820-170">This section assumes that on-premises users are synched with Azure AD using AD Connect.</span></span> <span data-ttu-id="03820-171">如需 Azure AD Connect 的相關資訊，請參閱[整合您的內部部署目錄與 Azure Active Directory](../active-directory/connect/active-directory-aadconnect.md)。</span><span class="sxs-lookup"><span data-stu-id="03820-171">For information on Azure AD connect, see [Integrate your on-premises directories with Azure Active Directory](../active-directory/connect/active-directory-aadconnect.md).</span></span> 

### <a name="azure-active-directory-guid-id"></a><span data-ttu-id="03820-172">Azure Active Directory GUID 識別碼</span><span class="sxs-lookup"><span data-stu-id="03820-172">Azure Active Directory GUID ID</span></span>
<span data-ttu-id="03820-173">若要安裝 NPS，您必須知道 Azure AD 的 GUID。</span><span class="sxs-lookup"><span data-stu-id="03820-173">To install NPS, you need to know the GUID of the Azure AD.</span></span> <span data-ttu-id="03820-174">下面提供尋找 Azure AD GUID 的指示。</span><span class="sxs-lookup"><span data-stu-id="03820-174">Instructions for finding the GUID of the Azure AD are provided below.</span></span>

## <a name="configure-multi-factor-authentication"></a><span data-ttu-id="03820-175">設定 Multi-Factor Authentication</span><span class="sxs-lookup"><span data-stu-id="03820-175">Configure Multi-Factor Authentication</span></span> 
<span data-ttu-id="03820-176">這一節提供用於整合 Azure MFA 與遠端桌面閘道的指示。</span><span class="sxs-lookup"><span data-stu-id="03820-176">This section provides instructions for integrating Azure MFA with the Remote Desktop Gateway.</span></span> <span data-ttu-id="03820-177">身為管理員的您必須先設定 Azure MFA 服務，使用者才能自行註冊其多因素裝置或應用程式。</span><span class="sxs-lookup"><span data-stu-id="03820-177">As an administrator, you must configure the Azure MFA service before users can self-register their multi-factor devices or applications.</span></span>

<span data-ttu-id="03820-178">請遵循[開始在雲端使用 Azure Multi-factor Authentication](multi-factor-authentication-get-started-cloud.md)中的步驟，以對 Azure AD 使用者啟用 MFA。</span><span class="sxs-lookup"><span data-stu-id="03820-178">Follow the steps in [Getting started with Azure Multi-Factor Authentication in the cloud](multi-factor-authentication-get-started-cloud.md) to enable MFA for your Azure AD users.</span></span> 

### <a name="configure-accounts-for-two-step-verification"></a><span data-ttu-id="03820-179">為帳戶設定雙步驟驗證</span><span class="sxs-lookup"><span data-stu-id="03820-179">Configure accounts for two-step verification</span></span>
<span data-ttu-id="03820-180">在帳戶啟用 MFA 之後，使用者便無法登入 MFA 原則所控管的資源，除非您成功地設定受信任的裝置來作為使用雙步驟驗證的第二個驗證要素。</span><span class="sxs-lookup"><span data-stu-id="03820-180">Once an account has been enabled for MFA, you cannot sign in to resources governed by the MFA policy until you have successfully configured a trusted device to use for the second authentication factor have authenticated using two-step verification.</span></span>

<span data-ttu-id="03820-181">遵循 [Azure Multi-factor Authentication 什麼適合我？](./end-user/multi-factor-authentication-end-user.md)中的步驟，了解及正確設定您的裝置，以便透過您的使用者帳戶進行 MFA。</span><span class="sxs-lookup"><span data-stu-id="03820-181">Follow the steps in [What does Azure Multi-Factor Authentication mean for me?](./end-user/multi-factor-authentication-end-user.md) to understand and properly configure your devices for MFA with your user account.</span></span>

## <a name="install-and-configure-nps-extension"></a><span data-ttu-id="03820-182">安裝和設定 NPS 擴充功能</span><span class="sxs-lookup"><span data-stu-id="03820-182">Install and configure NPS extension</span></span>
<span data-ttu-id="03820-183">本節會提供指示，引導您將 RDS 基礎結構設定為使用 Azure MFA 讓用戶端向遠端桌面閘道進行驗證。</span><span class="sxs-lookup"><span data-stu-id="03820-183">This section provides instructions for configuring RDS infrastructure to use Azure MFA for client authentication with the Remote Desktop Gateway.</span></span>

### <a name="acquire-azure-active-directory-guid-id"></a><span data-ttu-id="03820-184">取得 Azure Active Directory GUID 識別碼</span><span class="sxs-lookup"><span data-stu-id="03820-184">Acquire Azure Active Directory GUID ID</span></span>

<span data-ttu-id="03820-185">在設定 NPS 擴充功能期間，您必須為 Azure AD 租用戶提供管理員認證和 Azure AD 識別碼。</span><span class="sxs-lookup"><span data-stu-id="03820-185">As part of the configuration of the NPS extension, you need to supply admin credentials and the Azure AD ID for your Azure AD tenant.</span></span> <span data-ttu-id="03820-186">下列步驟說明如何取得租用戶識別碼。</span><span class="sxs-lookup"><span data-stu-id="03820-186">The following steps show you how to get the tenant ID.</span></span>

1. <span data-ttu-id="03820-187">以 Azure 租用戶的全域管理員身分登入 [Azure 入口網站](https://portal.azure.com)。</span><span class="sxs-lookup"><span data-stu-id="03820-187">Sign in to the [Azure portal](https://portal.azure.com) as the global administrator of the Azure tenant.</span></span>
2. <span data-ttu-id="03820-188">在左方瀏覽窗格中，選取 [Azure Active Directory] 圖示。</span><span class="sxs-lookup"><span data-stu-id="03820-188">In the left navigation, select the **Azure Active Directory** icon.</span></span>
3. <span data-ttu-id="03820-189">選取 [屬性] 。</span><span class="sxs-lookup"><span data-stu-id="03820-189">Select **Properties**.</span></span>
4. <span data-ttu-id="03820-190">在 [屬性] 刀鋒視窗中，按一下 [目錄識別碼] 旁邊的 [複製] 圖示 (如下所示)，將識別碼複製到剪貼簿。</span><span class="sxs-lookup"><span data-stu-id="03820-190">In the Properties blade, beside the Directory ID, click the **Copy** icon, as shown below, to copy the ID to clipboard.</span></span>

 ![屬性](./media/nps-extension-remote-desktop-gateway/image1.png)

### <a name="install-the-nps-extension"></a><span data-ttu-id="03820-192">安裝 NPS 擴充功能</span><span class="sxs-lookup"><span data-stu-id="03820-192">Install the NPS extension</span></span>
<span data-ttu-id="03820-193">在已安裝網路原則與存取服務 (NPS) 角色的伺服器上安裝 NPS 擴充功能。</span><span class="sxs-lookup"><span data-stu-id="03820-193">Install the NPS extension on a server that has the Network Policy and Access Services (NPS) role installed.</span></span> <span data-ttu-id="03820-194">這可當作您的設計的 RADIUS 伺服器。</span><span class="sxs-lookup"><span data-stu-id="03820-194">This functions as the RADIUS server for your design.</span></span> 

>[!Important]
> <span data-ttu-id="03820-195">切勿在您的遠端桌面閘道伺服器上安裝 NPS 擴充功能。</span><span class="sxs-lookup"><span data-stu-id="03820-195">Be sure you do not install the NPS extension on your Remote Desktop Gateway server.</span></span>
> 

1. <span data-ttu-id="03820-196">下載 [NPS 擴充功能](https://aka.ms/npsmfa)。</span><span class="sxs-lookup"><span data-stu-id="03820-196">Download the [NPS extension](https://aka.ms/npsmfa).</span></span> 
2. <span data-ttu-id="03820-197">將安裝程式可執行檔 (NpsExtnForAzureMfaInstaller.exe) 複製到 NPS 伺服器。</span><span class="sxs-lookup"><span data-stu-id="03820-197">Copy the setup executable file (NpsExtnForAzureMfaInstaller.exe) to the NPS server.</span></span>
3. <span data-ttu-id="03820-198">在 NPS 伺服器上按兩下 **NpsExtnForAzureMfaInstaller.exe**。</span><span class="sxs-lookup"><span data-stu-id="03820-198">On the NPS server, double-click **NpsExtnForAzureMfaInstaller.exe**.</span></span> <span data-ttu-id="03820-199">出現提示時，按一下 [執行]。</span><span class="sxs-lookup"><span data-stu-id="03820-199">If prompted, click **Run**.</span></span>
4. <span data-ttu-id="03820-200">檢閱 [Azure MFA 的 NPS 擴充功能] 對話方塊中的軟體授權條款，勾選 [我同意授權條款和條件]，然後按一下 [安裝]。</span><span class="sxs-lookup"><span data-stu-id="03820-200">In the NPS Extension for Azure MFA dialog box, review the software license terms, check **I agree to the license terms and conditions**, and click **Install**.</span></span>
 
  ![Azure MFA 設定](./media/nps-extension-remote-desktop-gateway/image2.png)

5. <span data-ttu-id="03820-202">在 [Azure MFA 的 NPS 擴充功能] 對話方塊中按一下 [關閉]。</span><span class="sxs-lookup"><span data-stu-id="03820-202">In the NPS Extension for Azure MFA dialog box, click Close.</span></span> 

  ![Azure MFA 的 NPS 擴充功能](./media/nps-extension-remote-desktop-gateway/image3.png)

### <a name="configure-certificates-for-use-with-the-nps-extension-using-a-powershell-script"></a><span data-ttu-id="03820-204">使用 PowerShell 指令碼來設定要用於 NPS 擴充功能的憑證</span><span class="sxs-lookup"><span data-stu-id="03820-204">Configure certificates for use with the NPS extension using a PowerShell script</span></span>
<span data-ttu-id="03820-205">接下來，您必須設定要供 NPS 擴充功能使用的憑證，以確保通訊安全並提供保證。</span><span class="sxs-lookup"><span data-stu-id="03820-205">Next, you need to configure certificates for use by the NPS extension to ensure secure communications and assurance.</span></span> <span data-ttu-id="03820-206">NPS 元件納入了 Windows PowerShell 指令碼，以設定要用於 NPS 的自我簽署憑證。</span><span class="sxs-lookup"><span data-stu-id="03820-206">The NPS components include a Windows PowerShell script that configures a self-signed certificate for use with NPS.</span></span> 

<span data-ttu-id="03820-207">此指令碼會執行下列動作：</span><span class="sxs-lookup"><span data-stu-id="03820-207">The script performs the following actions:</span></span>

* <span data-ttu-id="03820-208">建立自我簽署憑證</span><span class="sxs-lookup"><span data-stu-id="03820-208">Creates a self-signed certificate</span></span>
* <span data-ttu-id="03820-209">讓憑證的公開金鑰與 Azure AD 的服務主體產生關聯</span><span class="sxs-lookup"><span data-stu-id="03820-209">Associates public key of certificate to service principal on Azure AD</span></span>
* <span data-ttu-id="03820-210">將憑證儲存在本機電腦的存放區</span><span class="sxs-lookup"><span data-stu-id="03820-210">Stores the cert in the local machine store</span></span>
* <span data-ttu-id="03820-211">將憑證的私密金鑰存取權授與給網路使用者</span><span class="sxs-lookup"><span data-stu-id="03820-211">Grants access to the certificate’s private key to the network user</span></span>
* <span data-ttu-id="03820-212">重新啟動網路原則伺服器服務</span><span class="sxs-lookup"><span data-stu-id="03820-212">Restarts Network Policy Server service</span></span>

<span data-ttu-id="03820-213">如果您想要使用您自己的憑證，您必須讓該憑證的公開金鑰與 Azure AD 的服務主體產生關聯，依此類推。</span><span class="sxs-lookup"><span data-stu-id="03820-213">If you want to use your own certificates, you need to associate the public of your certificate to the service principle on Azure AD, and so on.</span></span>

<span data-ttu-id="03820-214">若要使用此指令碼，請為擴充功能提供您的 Azure AD 系統管理認證以及您之前複製的 Azure AD 租用戶識別碼。</span><span class="sxs-lookup"><span data-stu-id="03820-214">To use the script, provide the extension with your Azure AD Admin credentials and the Azure AD tenant ID that you copied earlier.</span></span> <span data-ttu-id="03820-215">在已安裝 NPS 擴充功能的每個 NPS 伺服器上執行此指令碼。</span><span class="sxs-lookup"><span data-stu-id="03820-215">Run the script on each NPS server where you installed the NPS extension.</span></span> <span data-ttu-id="03820-216">然後執行以下動作：</span><span class="sxs-lookup"><span data-stu-id="03820-216">Then do the following:</span></span>

1. <span data-ttu-id="03820-217">開啟系統管理 Windows PowerShell 提示字元。</span><span class="sxs-lookup"><span data-stu-id="03820-217">Open an administrative Windows PowerShell prompt.</span></span>
2. <span data-ttu-id="03820-218">在 PowerShell 提示字元中輸入 **cd ‘c:\Program Files\Microsoft\AzureMfa\Config’**，然後按 **ENTER**。</span><span class="sxs-lookup"><span data-stu-id="03820-218">At the PowerShell prompt, type **cd ‘c:\Program Files\Microsoft\AzureMfa\Config’**, and press **ENTER**.</span></span>
3. <span data-ttu-id="03820-219">輸入 _.\AzureMfsNpsExtnConfigSetup.ps1_，然後按 **ENTER**。</span><span class="sxs-lookup"><span data-stu-id="03820-219">Type _.\AzureMfsNpsExtnConfigSetup.ps1_, and press **ENTER**.</span></span> <span data-ttu-id="03820-220">此指令碼會檢查您是否已安裝 Azure Active Directory PowerShell 模組。</span><span class="sxs-lookup"><span data-stu-id="03820-220">The script checks to see if the Azure Active Directory PowerShell module is installed.</span></span> <span data-ttu-id="03820-221">如果尚未安裝此模組，指令碼就會為您安裝。</span><span class="sxs-lookup"><span data-stu-id="03820-221">If not installed, the script installs the module for you.</span></span>

  ![Azure AD PowerShell](./media/nps-extension-remote-desktop-gateway/image4.png)
  
4. <span data-ttu-id="03820-223">在指令碼確認您已安裝 PowerShell 模組後，它會顯示 [Azure Active Directory PowerShell 模組] 對話方塊。</span><span class="sxs-lookup"><span data-stu-id="03820-223">After the script verifies the installation of the PowerShell module, it displays the Azure Active Directory PowerShell module dialog box.</span></span> <span data-ttu-id="03820-224">在對話方塊中，輸入您的 Azure 系統管理認證和密碼，然後按一下 [登入]。</span><span class="sxs-lookup"><span data-stu-id="03820-224">In the dialog box, enter your Azure AD admin credentials and password, and click **Sign In**.</span></span>

  ![開啟 Powershell 帳戶](./media/nps-extension-remote-desktop-gateway/image5.png)

5. <span data-ttu-id="03820-226">出現提示時，貼上您之前複製到剪貼簿的租用戶識別碼，然後按 **ENTER**。</span><span class="sxs-lookup"><span data-stu-id="03820-226">When prompted, paste the tenant ID you copied to the clipboard earlier, and press **ENTER**.</span></span>

  ![輸入租用戶識別碼](./media/nps-extension-remote-desktop-gateway/image6.png)

6. <span data-ttu-id="03820-228">此指令碼會建立自我簽署憑證，並進行其他的設定變更。</span><span class="sxs-lookup"><span data-stu-id="03820-228">The script creates a self-signed certificate and performs other configuration changes.</span></span> <span data-ttu-id="03820-229">其輸出應類似下圖所示。</span><span class="sxs-lookup"><span data-stu-id="03820-229">The output should be like the image shown below.</span></span>

  ![自我簽署憑證](./media/nps-extension-remote-desktop-gateway/image7.png)

## <a name="configure-nps-components-on-remote-desktop-gateway"></a><span data-ttu-id="03820-231">設定遠端桌面閘道上的 NPS 元件</span><span class="sxs-lookup"><span data-stu-id="03820-231">Configure NPS components on Remote Desktop Gateway</span></span>
<span data-ttu-id="03820-232">在本節中，您可以設定遠端桌面閘道的連線授權原則和其他 RADIUS 設定。</span><span class="sxs-lookup"><span data-stu-id="03820-232">In this section, you configure the Remote Desktop Gateway connection authorization policies and other RADIUS settings.</span></span>

<span data-ttu-id="03820-233">驗證流程要求在遠端桌面閘道與 NPS Server 安裝所在的 NPS 伺服器之間交換 RADIUS 訊息。</span><span class="sxs-lookup"><span data-stu-id="03820-233">The authentication flow requires that RADIUS messages be exchanged between the Remote Desktop Gateway and the NPS server where the NPS Server is installed.</span></span> <span data-ttu-id="03820-234">這表示您必須在遠端桌面閘道和 NPS 擴充功能安裝所在的 NPS 伺服器上設定 RADIUS 用戶端設定。</span><span class="sxs-lookup"><span data-stu-id="03820-234">This means that you must configure RADIUS client settings on both Remote Desktop Gateway and the NPS server where the NPS extension is installed.</span></span> 

### <a name="configure-remote-desktop-gateway-connection-authorization-policies-to-use-central-store"></a><span data-ttu-id="03820-235">設定遠端桌面閘道連線授權原則以使用中央存放區</span><span class="sxs-lookup"><span data-stu-id="03820-235">Configure Remote Desktop Gateway connection authorization policies to use central store</span></span>
<span data-ttu-id="03820-236">遠端桌面連線授權原則 (RD CAP) 會指定連線至遠端桌面閘道伺服器的需求。</span><span class="sxs-lookup"><span data-stu-id="03820-236">Remote Desktop connection authorization policies (RD CAPs) specify the requirements for connecting to a Remote Desktop Gateway server.</span></span> <span data-ttu-id="03820-237">RD CAP 可以儲存在本機 (預設值)，也可以儲存在執行 NPS 的中央 RD CAP 存放區中。</span><span class="sxs-lookup"><span data-stu-id="03820-237">RD CAPs can be stored locally (default) or they can be stored in a central RD CAP store that is running NPS.</span></span> <span data-ttu-id="03820-238">若要設定 Azure MFA 與 RDS 的整合，您必須指定使用中央存放區。</span><span class="sxs-lookup"><span data-stu-id="03820-238">To configure integration of Azure MFA with RDS, you need to specify the use of a central store.</span></span>

1. <span data-ttu-id="03820-239">在 RD 閘道伺服器上，開啟 [伺服器管理員]。</span><span class="sxs-lookup"><span data-stu-id="03820-239">On the RD Gateway server, open **Server Manager**.</span></span> 
2. <span data-ttu-id="03820-240">在功能表上，按一下 [工具]，指向 [遠端桌面服務]，然後按一下 [遠端桌面閘道管理員]。</span><span class="sxs-lookup"><span data-stu-id="03820-240">On the menu, click **Tools**, point to **Remote Desktop Services**, and then click **Remote Desktop Gateway Manager**.</span></span>

  ![遠端桌面服務問題](./media/nps-extension-remote-desktop-gateway/image8.png)

3. <span data-ttu-id="03820-242">在 [RD 閘道管理員] 中，以滑鼠右鍵按一下 **\[伺服器名稱\] (本機)**，然後按一下 [屬性]。</span><span class="sxs-lookup"><span data-stu-id="03820-242">In the RD Gateway Manger, right-click **\[Server Name\] (Local)**, and click **Properties**.</span></span>

  ![伺服器名稱](./media/nps-extension-remote-desktop-gateway/image9.png)

4. <span data-ttu-id="03820-244">在 [屬性] 對話方塊中，選取 [RD CAP 存放區] 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="03820-244">In the Properties dialog box, select the **RD CAP** Store tab.</span></span>
5. <span data-ttu-id="03820-245">在 [RD CAP 存放區] 索引標籤上，選取 [執行 NPS 的中央伺服器]。</span><span class="sxs-lookup"><span data-stu-id="03820-245">On the RD CAP Store tab, select **Central Server running NPS**.</span></span> 
6. <span data-ttu-id="03820-246">在 [輸入執行 NPS 之伺服器的名稱或 IP 位址] 欄位中，輸入您安裝 NPS 擴充功能之伺服器的 IP 位址或伺服器名稱。</span><span class="sxs-lookup"><span data-stu-id="03820-246">In the **Enter a name or IP address for the server running NPS** field, type the IP address or server name of the server where you installed the NPS extension.</span></span>

  ![輸入名稱或 IP 位址](./media/nps-extension-remote-desktop-gateway/image10.png)
  
7. <span data-ttu-id="03820-248">按一下 [新增] 。</span><span class="sxs-lookup"><span data-stu-id="03820-248">Click **Add**.</span></span>
8. <span data-ttu-id="03820-249">在 [共用祕密] 對話方塊中，輸入共用祕密，然後按一下 [確定]。</span><span class="sxs-lookup"><span data-stu-id="03820-249">In the **Shared Secret** dialog box, enter a shared secret, and then click **OK**.</span></span> <span data-ttu-id="03820-250">務必記錄此共用祕密並安全地儲存記錄。</span><span class="sxs-lookup"><span data-stu-id="03820-250">Ensure you record this shared secret and store the record securely.</span></span>

 >[!NOTE]
 ><span data-ttu-id="03820-251">共用祕密用於建立 RADIUS 伺服器與用戶端之間的信任。</span><span class="sxs-lookup"><span data-stu-id="03820-251">Shared secret is used to establish trust between the RADIUS servers and clients.</span></span> <span data-ttu-id="03820-252">建立長而複雜的密碼。</span><span class="sxs-lookup"><span data-stu-id="03820-252">Create a long and complex password.</span></span>
 >

 ![共用祕密](./media/nps-extension-remote-desktop-gateway/image11.png)

9. <span data-ttu-id="03820-254">按一下 [確定] 關閉對話方塊。</span><span class="sxs-lookup"><span data-stu-id="03820-254">Click **OK** to close the dialog box.</span></span>

### <a name="configure-radius-timeout-value-on-remote-desktop-gateway-nps"></a><span data-ttu-id="03820-255">在遠端桌面閘道 NPS 上設定 RADIUS 逾時值</span><span class="sxs-lookup"><span data-stu-id="03820-255">Configure RADIUS timeout value on Remote Desktop Gateway NPS</span></span>
<span data-ttu-id="03820-256">若要確保有時間驗證使用者的認證，請執行雙步驟驗證、接收回應，然後回應 RADIUS 訊息，而且一定要調整 RADIUS 逾時值。</span><span class="sxs-lookup"><span data-stu-id="03820-256">To ensure there is time to validate users’ credentials, perform two-step verification, receive responses, and respond to RADIUS messages, it is necessary to adjust the RADIUS timeout value.</span></span>

1. <span data-ttu-id="03820-257">在 RD 閘道伺服器的 [伺服器管理員] 中，按一下 [工具]，然後按一下 [網路原則伺服器]。</span><span class="sxs-lookup"><span data-stu-id="03820-257">On the RD Gateway server, in Server Manager, click **Tools**, and then click **Network Policy Server**.</span></span> 
2. <span data-ttu-id="03820-258">在 [NPS (本機)] 主控台中，展開 [RADIUS 用戶端和伺服器]，然後選取 [遠端 RADIUS 伺服器]。</span><span class="sxs-lookup"><span data-stu-id="03820-258">In the **NPS (Local)** console, expand **RADIUS Clients and Servers**, and select **Remote RADIUS Server**.</span></span>

 ![遠端 RADIUS 伺服器](./media/nps-extension-remote-desktop-gateway/image12.png)

3. <span data-ttu-id="03820-260">在詳細資料窗格中，按兩下 [TS GATEWAY SERVER GROUP]。</span><span class="sxs-lookup"><span data-stu-id="03820-260">In the details pane, double-click **TS GATEWAY SERVER GROUP**.</span></span>

 >[!NOTE]
 ><span data-ttu-id="03820-261">設定 NPS 原則的中央伺服器時，已建立此 RADIUS 伺服器群組。</span><span class="sxs-lookup"><span data-stu-id="03820-261">This RADIUS Server Group was created when you configured the central server for NPS policies.</span></span> <span data-ttu-id="03820-262">RD 閘道會將 RADIUS 訊息轉送到此伺服器或伺服器群組 (如果群組中超過一個伺服器)。</span><span class="sxs-lookup"><span data-stu-id="03820-262">The RD Gateway forwards RADIUS messages to this server or group of servers, if more than one in the group.</span></span>
 >

4. <span data-ttu-id="03820-263">在 [TS GATEWAY SERVER GROUP 屬性] 對話方塊中，選取您設定用來儲存 RD CAP 之 NPS 伺服器的 IP 位址或名稱，然後按一下 [編輯]。</span><span class="sxs-lookup"><span data-stu-id="03820-263">In the **TS GATEWAY SERVER GROUP Properties** dialog box, select the IP address or name of the NPS server you configured to store RD CAPs, and then click **Edit**.</span></span> 

 ![TS Gateway Server Group](./media/nps-extension-remote-desktop-gateway/image13.png)

5. <span data-ttu-id="03820-265">在 [編輯 RADIUS 伺服器] 對話方塊中，選取 [負載平衡] 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="03820-265">In the **Edit RADIUS Server** dialog box, select the **Load Balancing** tab.</span></span>
6. <span data-ttu-id="03820-266">在 [負載平衡] 索引標籤的 [要求被丟棄前，無回應的秒數] 欄位中，將預設值從 3 變更為介於 30 與 60 秒之間的值。</span><span class="sxs-lookup"><span data-stu-id="03820-266">In the **Load Balancing** tab, in the **Number of seconds without response before request is considered dropped** field, change the default value from 3 to a value between 30 and 60 seconds.</span></span>
7. <span data-ttu-id="03820-267">在 [伺服器被識別為無法使用時，要求之間的間隔秒數] 欄位中，將預設值 30 秒變更為等於或大於您在上一個步驟中指定的值。</span><span class="sxs-lookup"><span data-stu-id="03820-267">In the **Number of seconds between requests when server is identified as unavailable** field, change the default value of 30 seconds to a value that is equal to or greater than the value you specified in the previous step.</span></span>

 ![編輯 Radius 伺服器](./media/nps-extension-remote-desktop-gateway/image14.png)

8.  <span data-ttu-id="03820-269">按一下 [確定] 兩次以關閉對話方塊。</span><span class="sxs-lookup"><span data-stu-id="03820-269">Click OK two times to close the dialog boxes.</span></span>

### <a name="verify-connection-request-policies"></a><span data-ttu-id="03820-270">驗證連線要求原則</span><span class="sxs-lookup"><span data-stu-id="03820-270">Verify Connection Request Policies</span></span> 
<span data-ttu-id="03820-271">根據預設，當您將 RD 閘道設定為使用連線授權原則的中央原則存放區時，則 RD 閘道會被設定為將 CAP 要求轉送到 NPS 伺服器。</span><span class="sxs-lookup"><span data-stu-id="03820-271">By default, when you configure the RD Gateway to use a central policy store for connection authorization policies, the RD Gateway is configured to forward CAP requests to the NPS server.</span></span> <span data-ttu-id="03820-272">已安裝 Azure MFA 擴充功能的 NPS 伺服器，會處理 RADIUS 存取要求。</span><span class="sxs-lookup"><span data-stu-id="03820-272">The NPS server with the Azure MFA extension installed, processes the RADIUS access request.</span></span> <span data-ttu-id="03820-273">下列步驟顯示如何確認預設連線要求原則。</span><span class="sxs-lookup"><span data-stu-id="03820-273">The following steps show you how to verify the default connection request policy.</span></span> 

1. <span data-ttu-id="03820-274">在 RD 閘道上，於 [NPS (本機)] 主控台中展開 [原則]，然後選取 [連線要求原則]。</span><span class="sxs-lookup"><span data-stu-id="03820-274">On the RD Gateway, in the NPS (Local) console, expand **Policies**, and select **Connection Request Policies**.</span></span>
2. <span data-ttu-id="03820-275">以滑鼠右鍵按一下 [連線要求原則]，然後連按兩下 [TS GATEWAY AUTHORIZATION POLICY]。</span><span class="sxs-lookup"><span data-stu-id="03820-275">Right-click **Connect Request Policies**, and double-click **TS GATEWAY AUTHORIZATION POLICY**.</span></span>
3. <span data-ttu-id="03820-276">在 [TS GATEWAY AUTHORIZATION POLICY 屬性] 對話方塊中，按一下 [設定] 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="03820-276">In the **TS GATEWAY AUTHORIZATION POLICY properties** dialog box, click the **Settings** tab.</span></span>
4. <span data-ttu-id="03820-277">在 [設定] 索引標籤上，按一下 [轉送連線要求] 之下的 [驗證]。</span><span class="sxs-lookup"><span data-stu-id="03820-277">On **Settings** tab, under Forwarding Connection Request, click **Authentication**.</span></span> <span data-ttu-id="03820-278">RADIUS 用戶端會設定為轉送要求進行驗證。</span><span class="sxs-lookup"><span data-stu-id="03820-278">RADIUS client is configured to forward requests for authentication.</span></span>

 ![驗證設定](./media/nps-extension-remote-desktop-gateway/image15.png)
 
5. <span data-ttu-id="03820-280">按一下 [取消]。</span><span class="sxs-lookup"><span data-stu-id="03820-280">Click **Cancel**.</span></span> 

## <a name="configure-nps-on-the-server-where-the-nps-extension-is-installed"></a><span data-ttu-id="03820-281">在安裝 NPS 擴充功能的伺服器上設定 NPS</span><span class="sxs-lookup"><span data-stu-id="03820-281">Configure NPS on the server where the NPS extension is installed</span></span>
<span data-ttu-id="03820-282">安裝 NPS 擴充功能的 NPS 伺服器必須能夠與遠端桌面閘道上的 NPS 伺服器交換 RADIUS 訊息。</span><span class="sxs-lookup"><span data-stu-id="03820-282">The NPS server where the NPS extension is installed needs to be able to exchange RADIUS messages with the NPS server on the Remote Desktop Gateway.</span></span> <span data-ttu-id="03820-283">若要啟用此訊息交換，您必須在安裝 NPS 擴充服務的伺服器上設定 NPS 元件。</span><span class="sxs-lookup"><span data-stu-id="03820-283">To enable this message exchange, you need to configure the NPS components on the server where the NPS extension service is installed.</span></span> 

### <a name="register-server-in-active-directory"></a><span data-ttu-id="03820-284">在 Active Directory 中註冊伺服器</span><span class="sxs-lookup"><span data-stu-id="03820-284">Register Server in Active Directory</span></span>
<span data-ttu-id="03820-285">若要讓 NPS 伺服器在本案例中正常運作，您必須在 Active Directory 中加以註冊。</span><span class="sxs-lookup"><span data-stu-id="03820-285">To function properly in this scenario, the NPS server needs to be registered in Active Directory.</span></span>

1. <span data-ttu-id="03820-286">開啟 [伺服器管理員] 。</span><span class="sxs-lookup"><span data-stu-id="03820-286">Open **Server Manager**.</span></span>
2. <span data-ttu-id="03820-287">在 [伺服器管理員] 中按一下 [工具]，然後按一下 [網路原則伺服器]。</span><span class="sxs-lookup"><span data-stu-id="03820-287">In Server Manager, click **Tools**, and then click **Network Policy Server**.</span></span> 
3. <span data-ttu-id="03820-288">在 [網路原則伺服器] 主控台中，以滑鼠右鍵按一下 [NPS (本機)]，然後按一下 [在 Active Directory 中註冊伺服器]。</span><span class="sxs-lookup"><span data-stu-id="03820-288">In the Network Policy Server console, right-click **NPS (Local)**, and then click **Register server in Active Directory**.</span></span> 
4. <span data-ttu-id="03820-289">按 [確定] 兩次。</span><span class="sxs-lookup"><span data-stu-id="03820-289">Click **OK** two times.</span></span>

 ![在 AD 中註冊伺服器](./media/nps-extension-remote-desktop-gateway/image16.png)

5. <span data-ttu-id="03820-291">讓主控台保持開啟以供下一個程序使用。</span><span class="sxs-lookup"><span data-stu-id="03820-291">Leave the console open for the next procedure.</span></span>

### <a name="create-and-configure-radius-client"></a><span data-ttu-id="03820-292">建立及設定 RADIUS 用戶端</span><span class="sxs-lookup"><span data-stu-id="03820-292">Create and configure RADIUS client</span></span> 
<span data-ttu-id="03820-293">必須將遠端桌面閘道設定為 NPS 伺服器的 RADIUS 用戶端。</span><span class="sxs-lookup"><span data-stu-id="03820-293">The Remote Desktop Gateway needs to be configured as a RADIUS client to the NPS server.</span></span> 

1. <span data-ttu-id="03820-294">在安裝 NPS 擴充功能的 NPS 伺服器上，於 [NPS (本機)] 主控台中，以滑鼠右鍵按一下 [RADIUS 用戶端] 並按一下 [新增]。</span><span class="sxs-lookup"><span data-stu-id="03820-294">On the NPS server where the NPS extension is installed, in the **NPS (Local)** console, right-click **RADIUS Clients** and click **New**.</span></span>

 ![新增 RADIUS 用戶端](./media/nps-extension-remote-desktop-gateway/image17.png)

2. <span data-ttu-id="03820-296">在 [新增 RADIUS 用戶端] 對話方塊中，提供易記的名稱 (例如 Gateway)，以及遠端桌面閘道伺服器的 IP 位址或 DNS 名稱。</span><span class="sxs-lookup"><span data-stu-id="03820-296">In the **New RADIUS client** dialog box, provide a friendly name, such as _Gateway_, and the IP address or DNS name of the Remote Desktop Gateway server.</span></span> 
3. <span data-ttu-id="03820-297">在 [共用祕密] 和 [確認共用祕密] 欄位中，輸入您之前使用的相同祕密。</span><span class="sxs-lookup"><span data-stu-id="03820-297">In the **Shared secret** and the **Confirm shared secret** fields, enter the same secret that you used before.</span></span>

 ![名稱和位址](./media/nps-extension-remote-desktop-gateway/image18.png)

4. <span data-ttu-id="03820-299">按一下 [確定] 關閉 [新增 RADIUS 用戶端] 對話方塊。</span><span class="sxs-lookup"><span data-stu-id="03820-299">Click **OK** to close the New RADIUS client dialog box.</span></span>

### <a name="configure-network-policy"></a><span data-ttu-id="03820-300">設定網路原則</span><span class="sxs-lookup"><span data-stu-id="03820-300">Configure Network Policy</span></span>
<span data-ttu-id="03820-301">請記住，具備 Azure MFA 擴充功能的 NPS 伺服器是連線授權原則 (CAP) 的指定中央原則存放區。</span><span class="sxs-lookup"><span data-stu-id="03820-301">Recall the NPS server with the Azure MFA extension is the designated central policy store for the Connection Authorization Policy (CAP).</span></span> <span data-ttu-id="03820-302">因此，您需要在 NPS 伺服器上實作 CAP，才能授權有效的連線要求。</span><span class="sxs-lookup"><span data-stu-id="03820-302">Therefore, you need to implement a CAP on the NPS server to authorize valid connections requests.</span></span>  

1. <span data-ttu-id="03820-303">在 [NPS (本機)] 主控台中，展開 [原則]，然後按一下 [網路原則]。</span><span class="sxs-lookup"><span data-stu-id="03820-303">In the NPS (Local) console, expand **Policies**, and click **Network Policies**.</span></span>
2. <span data-ttu-id="03820-304">以滑鼠右鍵按一下 [其他存取伺服器的連線]，然後按一下 [複製原則]。</span><span class="sxs-lookup"><span data-stu-id="03820-304">Right-click **Connections to other access servers**, and click **Duplicate policy**.</span></span> 

 ![複製原則](./media/nps-extension-remote-desktop-gateway/image19.png)

3. <span data-ttu-id="03820-306">以滑鼠右鍵按一下 [複製其他存取伺服器的連線]，然後按一下 [屬性]。</span><span class="sxs-lookup"><span data-stu-id="03820-306">Right-click **Copy of Connections to other access servers**, and click **Properties**.</span></span>

 ![網路屬性](./media/nps-extension-remote-desktop-gateway/image20.png)

4. <span data-ttu-id="03820-308">在 [複製其他存取伺服器的連線] 對話方塊的 [原則名稱] 中，輸入適當的名稱，例如 **RDG_CAP**。</span><span class="sxs-lookup"><span data-stu-id="03820-308">In the **Copy of Connections to other access servers** dialog box, in Policy Name, enter a suitable name, such as **RDG_CAP**.</span></span> <span data-ttu-id="03820-309">勾選 [啟用原則]，然後選取 [授與存取權]。</span><span class="sxs-lookup"><span data-stu-id="03820-309">Check **Policy Enabled**, and select **Grant access**.</span></span> <span data-ttu-id="03820-310">(選擇性) 在 [網路存取類型] 中選取 [遠端桌面閘道]，您也可以將它保留為 [未指定]。</span><span class="sxs-lookup"><span data-stu-id="03820-310">Optionally, in Type of network access, select **Remote Desktop Gateway**, or you can leave it as **Unspecified**.</span></span>

 ![複製連線](./media/nps-extension-remote-desktop-gateway/image21.png)

5.  <span data-ttu-id="03820-312">按一下 [條件約束] 索引標籤，然後勾選 [允許用戶端沒有交涉驗證方法仍然可以連線]。</span><span class="sxs-lookup"><span data-stu-id="03820-312">Click the **Constraints** tab, and check **Allow clients to connect without negotiating an authentication method**.</span></span>

 ![允許用戶端連線](./media/nps-extension-remote-desktop-gateway/image22.png)

6. <span data-ttu-id="03820-314">(選擇性) 按一下 [條件] 索引標籤，並新增必須符合才能授權連線的條件，例如，特定 Windows 群組中的成員資格。</span><span class="sxs-lookup"><span data-stu-id="03820-314">Optionally, click the **Conditions** tab and add conditions that must be met for the connection to be authorized, for example, membership in a specific Windows group.</span></span>

 ![條件](./media/nps-extension-remote-desktop-gateway/image23.png)

7. <span data-ttu-id="03820-316">按一下 [確定] 。</span><span class="sxs-lookup"><span data-stu-id="03820-316">Click **OK**.</span></span> <span data-ttu-id="03820-317">當系統提示您檢視對應的說明主題時，請按一下 [否]。</span><span class="sxs-lookup"><span data-stu-id="03820-317">When prompted to view the corresponding Help topic, click **No**.</span></span>
8. <span data-ttu-id="03820-318">請確定新原則位於清單的頂端，已啟用原則，而且它會授與存取權。</span><span class="sxs-lookup"><span data-stu-id="03820-318">Ensure that your new policy is at the top of the list, that the policy is enabled, and that it grants access.</span></span>

 ![網路原則](./media/nps-extension-remote-desktop-gateway/image24.png)

## <a name="verify-configuration"></a><span data-ttu-id="03820-320">驗證組態</span><span class="sxs-lookup"><span data-stu-id="03820-320">Verify configuration</span></span>
<span data-ttu-id="03820-321">若要驗證組態，您必須使用適當的 RDP 用戶端登入遠端桌面閘道。</span><span class="sxs-lookup"><span data-stu-id="03820-321">To verify the configuration, you need to log on the Remote Desktop Gateway with a suitable RDP client.</span></span> <span data-ttu-id="03820-322">請務必使用您的連線授權原則所允許的帳戶並已啟用 Azure MFA。</span><span class="sxs-lookup"><span data-stu-id="03820-322">Be sure to use an account that is allowed by your Connection Authorization Policies and is enabled for Azure MFA.</span></span> 

<span data-ttu-id="03820-323">如下圖所示，您可以使用 [遠端桌面 Web 存取] 頁面。</span><span class="sxs-lookup"><span data-stu-id="03820-323">As show in the image below, you can use the **Remote Desktop Web Access** page.</span></span>

![遠端桌面 Web 存取](./media/nps-extension-remote-desktop-gateway/image25.png)

<span data-ttu-id="03820-325">在成功輸入您的認證進行主要驗證時，[遠端桌面連線] 對話方塊會顯示 [起始遠端連線] 的狀態，如下所示。</span><span class="sxs-lookup"><span data-stu-id="03820-325">Upon successfully entering your credentials for primary authentication, the Remote Desktop Connect dialog box shows a status of Initiating remote connection, as shown below.</span></span> 

<span data-ttu-id="03820-326">如果您已成功地使用先前在 Azure MFA 中設定的次要驗證方法進行驗證，您就會連線到資源。</span><span class="sxs-lookup"><span data-stu-id="03820-326">If you successfully authenticate with the secondary authentication method you previously configured in Azure MFA, you are connected to the resource.</span></span> <span data-ttu-id="03820-327">不過，如果次要驗證失敗，系統就會拒絕讓您存取資源。</span><span class="sxs-lookup"><span data-stu-id="03820-327">However, if the secondary authentication is not successful, you are denied access to resource.</span></span> 

![起始遠端連線](./media/nps-extension-remote-desktop-gateway/image26.png)

<span data-ttu-id="03820-329">在下列範例中，我們使用了 Windows Phone 上的 Authenticator 應用程式來提供次要驗證。</span><span class="sxs-lookup"><span data-stu-id="03820-329">In the example below, the Authenticator app on a Windows phone is used to provide the secondary authentication.</span></span>

![帳戶](./media/nps-extension-remote-desktop-gateway/image27.png)

<span data-ttu-id="03820-331">在使用第二種驗證方法驗證成功之後，您便已如往常一樣登入遠端桌面閘道。</span><span class="sxs-lookup"><span data-stu-id="03820-331">Once you have successfully authenticated using the secondary authentication method, you are logged into the Remote Desktop Gateway as normal.</span></span> <span data-ttu-id="03820-332">不過，因為您必須使用受信任裝置上的行動裝置應用程式來使用次要驗證方法，登入程序會比使用其他方法來得更加安全。</span><span class="sxs-lookup"><span data-stu-id="03820-332">However, because you are required to use a secondary authentication method using a mobile app on a trusted device, the log-in process is more secure than it would be otherwise.</span></span>

### <a name="view-event-viewer-logs-for-successful-logon-events"></a><span data-ttu-id="03820-333">檢視事件檢視器記錄來找到成功的登入事件</span><span class="sxs-lookup"><span data-stu-id="03820-333">View Event Viewer logs for successful logon events</span></span>
<span data-ttu-id="03820-334">若要檢視 Windows 事件檢視器記錄中的成功登入事件，您可以發出下列 Windows PowerShell 命令來查詢 Windows 終端機服務和 Windows 安全性記錄。</span><span class="sxs-lookup"><span data-stu-id="03820-334">To view the successful sign-in events in the Windows Event Viewer logs, you can issue the following Windows PowerShell command to query the Windows Terminal Services and Windows Security logs.</span></span>

<span data-ttu-id="03820-335">若要查詢閘道操作記錄 (Event Viewer\Applications and Services Logs\Microsoft\Windows\TerminalServices-Gateway\Operational) 中的成功登入事件，使用下列命令：</span><span class="sxs-lookup"><span data-stu-id="03820-335">To query successful sign-in events in the Gateway operational logs _(Event Viewer\Applications and Services Logs\Microsoft\Windows\TerminalServices-Gateway\Operational_, use the following commands:</span></span>

* <span data-ttu-id="03820-336">_Get-WinEvent -Logname Microsoft-Windows-TerminalServices-Gateway/Operational_ | where {$_.ID -eq '300'} | FL</span><span class="sxs-lookup"><span data-stu-id="03820-336">_Get-WinEvent -Logname Microsoft-Windows-TerminalServices-Gateway/Operational_ | where {$_.ID -eq '300'} | FL</span></span> 
* <span data-ttu-id="03820-337">此命令顯示的 Windows 事件顯示使用者符合資源授權原則需求 (RD RAP) 並已取得存取權。</span><span class="sxs-lookup"><span data-stu-id="03820-337">This command displays Windows events that show the user met resource authorization policy requirements (RD RAP) and was granted access.</span></span>

![檢視事件檢視器](./media/nps-extension-remote-desktop-gateway/image28.png)

* <span data-ttu-id="03820-339">_Get-WinEvent -Logname Microsoft-Windows-TerminalServices-Gateway/Operational_ | where {$_.ID -eq '200'} | FL</span><span class="sxs-lookup"><span data-stu-id="03820-339">_Get-WinEvent -Logname Microsoft-Windows-TerminalServices-Gateway/Operational_ | where {$_.ID -eq '200'} | FL</span></span>
* <span data-ttu-id="03820-340">此命令會顯示使用者符合連線授權原則需求時顯示的事件。</span><span class="sxs-lookup"><span data-stu-id="03820-340">This command displays the events that show when user met connection authorization policy requirements.</span></span>

![連線授權](./media/nps-extension-remote-desktop-gateway/image29.png)

<span data-ttu-id="03820-342">您也可以檢視此記錄並依據事件識別碼 (300 和 200) 進行篩選。</span><span class="sxs-lookup"><span data-stu-id="03820-342">You can also view this log and filter on event IDs, 300 and 200.</span></span> <span data-ttu-id="03820-343">若要查詢安全性事件檢視器記錄中的成功登入事件，請使用下列命令：</span><span class="sxs-lookup"><span data-stu-id="03820-343">To query successful logon events in the Security event viewer logs, use the following command:</span></span>

* <span data-ttu-id="03820-344">_Get-WinEvent -Logname Security_ | where {$_.ID -eq '6272'} | FL</span><span class="sxs-lookup"><span data-stu-id="03820-344">_Get-WinEvent -Logname Security_ | where {$_.ID -eq '6272'} | FL</span></span> 
* <span data-ttu-id="03820-345">此命令可以在中央 NPS 或 RD 閘道伺服器上執行。</span><span class="sxs-lookup"><span data-stu-id="03820-345">This command can be run on either the central NPS or the RD Gateway Server.</span></span> 

![成功的登入事件](./media/nps-extension-remote-desktop-gateway/image30.png)

<span data-ttu-id="03820-347">您也可以檢視安全性記錄或網路原則與存取服務自訂檢視，如下所示：</span><span class="sxs-lookup"><span data-stu-id="03820-347">You can also view the Security log or the Network Policy and Access Services custom view, as shown below:</span></span>

![網路原則與存取服務](./media/nps-extension-remote-desktop-gateway/image31.png)

<span data-ttu-id="03820-349">在安裝了 Azure MFA NPS 擴充功能的伺服器上，您可以在 _Application and Services Logs\Microsoft\AzureMfa_ 找到擴充功能專屬的事件檢視器應用程式記錄。</span><span class="sxs-lookup"><span data-stu-id="03820-349">On the server where you installed the NPS extension for Azure MFA, you can find Event Viewer application logs specific to the extension at _Application and Services Logs\Microsoft\AzureMfa_.</span></span> 

![事件檢視器應用程式記錄](./media/nps-extension-remote-desktop-gateway/image32.png)

## <a name="troubleshoot-guide"></a><span data-ttu-id="03820-351">疑難排解指南</span><span class="sxs-lookup"><span data-stu-id="03820-351">Troubleshoot Guide</span></span>

<span data-ttu-id="03820-352">如果組態未如預期般運作，確認使用者是否已設為使用 Azure MFA 是疑難排解的起點。</span><span class="sxs-lookup"><span data-stu-id="03820-352">If the configuration is not working as expected, the first place to start to troubleshoot is to verify that the user is configured to use Azure MFA.</span></span> <span data-ttu-id="03820-353">讓使用者連線到 [Azure 入口網站](https://portal.azure.com)。</span><span class="sxs-lookup"><span data-stu-id="03820-353">Have the user connect to the [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="03820-354">如果使用者收到次要驗證提示而且可以成功地完成驗證，您就可以排除 Azure MFA 設定不正確的可能性。</span><span class="sxs-lookup"><span data-stu-id="03820-354">If users are prompted for secondary verification and can successfully authenticate, you can eliminate an incorrect configuration of Azure MFA.</span></span>

<span data-ttu-id="03820-355">如果 Azure MFA 對使用者有效，請檢閱相關的事件記錄。</span><span class="sxs-lookup"><span data-stu-id="03820-355">If Azure MFA is working for the user(s), you should review the relevant Event logs.</span></span> <span data-ttu-id="03820-356">這些記錄包括安全性事件記錄、閘道運作記錄，以及上一節中討論的 Azure MFA 記錄。</span><span class="sxs-lookup"><span data-stu-id="03820-356">These include the Security Event, Gateway operational, and Azure MFA logs that are discussed in the previous section.</span></span> 

<span data-ttu-id="03820-357">以下是安全性記錄的輸出範例，其中顯示了失敗登入事件 (事件識別碼 6273)。</span><span class="sxs-lookup"><span data-stu-id="03820-357">Below is an example output of Security log showing a failed logon event (Event ID 6273).</span></span>

![失敗的登入事件](./media/nps-extension-remote-desktop-gateway/image33.png)

<span data-ttu-id="03820-359">以下是來自 Azure MFA 記錄的相關事件：</span><span class="sxs-lookup"><span data-stu-id="03820-359">Below is a related event from the AzureMFA logs:</span></span>

![Azure MFA 記錄](./media/nps-extension-remote-desktop-gateway/image34.png)

<span data-ttu-id="03820-361">若要執行進階的疑難排解選項，請參閱安裝了 NPS 服務的 NPS 資料庫格式記錄檔。</span><span class="sxs-lookup"><span data-stu-id="03820-361">To perform advanced troubleshoot options, consult the NPS database format log files where the NPS service is installed.</span></span> <span data-ttu-id="03820-362">這些記錄檔會建立於 %SystemRoot%\System32\Logs 資料夾，並以逗號分隔文字檔的形式存在。</span><span class="sxs-lookup"><span data-stu-id="03820-362">These log files are created in _%SystemRoot%\System32\Logs_ folder as comma-delimited text files.</span></span> 

<span data-ttu-id="03820-363">如需這些記錄檔的說明，請參閱[解譯 NPS 資料庫格式記錄檔](https://technet.microsoft.com/library/cc771748.aspx)。</span><span class="sxs-lookup"><span data-stu-id="03820-363">For a description of these log files, see [Interpret NPS Database Format Log Files](https://technet.microsoft.com/library/cc771748.aspx).</span></span> <span data-ttu-id="03820-364">這些記錄檔中的項目若不匯入到試算表或資料庫，將難以解譯。</span><span class="sxs-lookup"><span data-stu-id="03820-364">The entries in these log files can be difficult to interpret without importing them into a spreadsheet or a database.</span></span> <span data-ttu-id="03820-365">您可以在線上找到數個 IAS 剖析器來協助您解譯記錄檔。</span><span class="sxs-lookup"><span data-stu-id="03820-365">You can find several IAS parsers online to assist you in interpreting the log files.</span></span> 

<span data-ttu-id="03820-366">下圖顯示其中一個這類可下載[共享軟體應用程式](http://www.deepsoftware.com/iasviewer)的輸出。</span><span class="sxs-lookup"><span data-stu-id="03820-366">The image below shows the output of one such downloadable [shareware application](http://www.deepsoftware.com/iasviewer).</span></span> 

![共享軟體應用程式](./media/nps-extension-remote-desktop-gateway/image35.png)

<span data-ttu-id="03820-368">最後，如需其他疑難排解選項，您可以使用通訊協定分析器，例如 [Microsoft Message Analyzer](https://technet.microsoft.com/library/jj649776.aspx)。</span><span class="sxs-lookup"><span data-stu-id="03820-368">Finally, for additional troubleshoot options, you can use a protocol analyzer, such [Microsoft Message Analyzer](https://technet.microsoft.com/library/jj649776.aspx).</span></span> 

<span data-ttu-id="03820-369">以下的 Microsoft Message Analyzer 影像顯示依據 RADIUS 通訊協定篩選並包含使用者名稱 **Contoso\AliceC** 的網路流量。</span><span class="sxs-lookup"><span data-stu-id="03820-369">The image below from Microsoft Message Analyzer shows network traffic filtered on RADIUS protocol that contains the user name **Contoso\AliceC**.</span></span>

![Microsoft Message Analyzer](./media/nps-extension-remote-desktop-gateway/image36.png)

## <a name="next-steps"></a><span data-ttu-id="03820-371">後續步驟</span><span class="sxs-lookup"><span data-stu-id="03820-371">Next steps</span></span>
[<span data-ttu-id="03820-372">如何取得 Azure Multi-Factor Authentication</span><span class="sxs-lookup"><span data-stu-id="03820-372">How to get Azure Multi-Factor Authentication</span></span>](multi-factor-authentication-versions-plans.md)

[<span data-ttu-id="03820-373">使用 RADIUS 的遠端桌面閘道和 Azure Multi-Factor Authentication Server</span><span class="sxs-lookup"><span data-stu-id="03820-373">Remote Desktop Gateway and Azure Multi-Factor Authentication Server using RADIUS</span></span>](multi-factor-authentication-get-started-server-rdg.md)

[<span data-ttu-id="03820-374">整合您的內部部署目錄與 Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="03820-374">Integrate your on-premises directories with Azure Active Directory</span></span>](../active-directory/connect/active-directory-aadconnect.md)
