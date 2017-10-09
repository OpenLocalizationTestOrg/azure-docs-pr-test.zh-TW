---
title: "aaaRemote 桌面閘道與 Azure MFA NPS 擴充功能的整合 |Microsoft 文件"
description: "這篇文章會討論與使用 Microsoft azure 的 hello 網路原則伺服器 (NPS) 延伸模組的 Azure MFA 整合您的遠端桌面閘道基礎結構。"
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
ms.openlocfilehash: ae5f6864416582bd82b787005ca787988d23a813
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
#  <a name="integrate-your-remote-desktop-gateway-infrastructure-using-hello-network-policy-server-nps-extension-and-azure-ad"></a><span data-ttu-id="42bec-104">將您的遠端桌面閘道基礎結構使用 hello 網路原則伺服器 (NPS) 延伸模組和 Azure AD 整合</span><span class="sxs-lookup"><span data-stu-id="42bec-104">Integrate your Remote Desktop Gateway infrastructure using hello Network Policy Server (NPS) extension and Azure AD</span></span>

<span data-ttu-id="42bec-105">這篇文章詳細說明如何整合您的遠端桌面閘道基礎結構與 Azure Multi-factor Authentication (MFA) 使用 Microsoft azure 的 hello 網路原則伺服器 (NPS) 延伸模組。</span><span class="sxs-lookup"><span data-stu-id="42bec-105">This article provides details for integrating your Remote Desktop Gateway infrastructure with Azure Multi-Factor Authentication (MFA) using hello Network Policy Server (NPS) extension for Microsoft Azure.</span></span> 

<span data-ttu-id="42bec-106">hello azure 網路原則服務 」 (NPS) 延伸模組可讓客戶 toosafeguard 遠端驗證撥號使用者服務 (RADIUS) 用戶端驗證使用 Azure 的雲端式[Multi-factor Authentication (MFA)](multi-factor-authentication.md)。</span><span class="sxs-lookup"><span data-stu-id="42bec-106">hello Network Policy Service (NPS) extension for Azure allows customers toosafeguard Remote Authentication Dial-In User Service (RADIUS) client authentication using Azure’s cloud-based [Multi-Factor Authentication (MFA)](multi-factor-authentication.md).</span></span> <span data-ttu-id="42bec-107">此解決方案可提供新增的第二層安全性 toouser 登入和交易的兩步驟驗證。</span><span class="sxs-lookup"><span data-stu-id="42bec-107">This solution provides two-step verification for adding a second layer of security toouser sign-ins and transactions.</span></span>

<span data-ttu-id="42bec-108">本文章提供整合 hello NPS 基礎結構使用 Azure MFA 的逐步指示，使用 Azure 的 hello NPS 擴充功能。</span><span class="sxs-lookup"><span data-stu-id="42bec-108">This article provides step-by-step instructions for integrating hello NPS infrastructure with Azure MFA using hello NPS extension for Azure.</span></span> <span data-ttu-id="42bec-109">這可讓使用者 toolog tooa 遠端桌面閘道上的安全驗證。</span><span class="sxs-lookup"><span data-stu-id="42bec-109">This enables secure verification for users attempting toolog on tooa Remote Desktop Gateway.</span></span> 

<span data-ttu-id="42bec-110">hello 網路原則與存取服務 」 (NPS) 可讓組織 hello 能力 toodo hello 下列：</span><span class="sxs-lookup"><span data-stu-id="42bec-110">hello Network Policy and Access Services (NPS) gives organizations hello ability toodo hello following:</span></span>
* <span data-ttu-id="42bec-111">藉由指定誰可以連線定義 hello 管理和控制的網路要求的中央位置，允許的連線，每天何時 hello 的連線的持續時間和 hello 層級的安全性，用戶端必須使用 tooconnect，依此類推。</span><span class="sxs-lookup"><span data-stu-id="42bec-111">Define central locations for hello management and control of network requests by specifying who can connect, what times of day connections are allowed, hello duration of connections, and hello level of security that clients must use tooconnect, and so on.</span></span> <span data-ttu-id="42bec-112">組織不必在每個 VPN 或遠端桌面 (RD) 閘道伺服器上指定這些原則，而是在中央位置一次指定這些原則。</span><span class="sxs-lookup"><span data-stu-id="42bec-112">Rather than specifying these policies on each VPN or Remote Desktop (RD) Gateway server, these policies can be specified once in a central location.</span></span> <span data-ttu-id="42bec-113">hello RADIUS 通訊協定提供 hello 集中式驗證、 授權以及帳戶處理 (AAA)。</span><span class="sxs-lookup"><span data-stu-id="42bec-113">hello RADIUS protocol provides hello centralized Authentication, Authorization, and Accounting (AAA).</span></span> 
* <span data-ttu-id="42bec-114">建立並強制執行判斷裝置是否會授與不受限制或限制存取 toonetwork 資源的網路存取保護 (NAP) 用戶端健康原則。</span><span class="sxs-lookup"><span data-stu-id="42bec-114">Establish and enforce Network Access Protection (NAP) client health policies that determine whether devices are granted unrestricted or restricted access toonetwork resources.</span></span>
* <span data-ttu-id="42bec-115">提供表示 tooenforce 驗證和授權的存取 too802.1x 無線存取點及乙太網路交換器。</span><span class="sxs-lookup"><span data-stu-id="42bec-115">Provide a means tooenforce authentication and authorization for access too802.1x-capable wireless access points and Ethernet switches.</span></span>    

<span data-ttu-id="42bec-116">一般而言，使用 NPS (RADIUS) toosimplify 組織，和集中 VPN hello 管理原則。</span><span class="sxs-lookup"><span data-stu-id="42bec-116">Typically, organizations use NPS (RADIUS) toosimplify and centralize hello management of VPN polices.</span></span> <span data-ttu-id="42bec-117">不過，許多組織也使用 NPS toosimplify，並集中管理 hello RD 桌面連線授權原則 (RD Cap)。</span><span class="sxs-lookup"><span data-stu-id="42bec-117">However, many organizations also use NPS toosimplify and centralize hello management of RD Desktop Connection Authorization Policies (RD CAPs).</span></span> 

<span data-ttu-id="42bec-118">組織也可以使用 Azure MFA tooenhance 安全性整合 NPS，並提供高層級的相容性。</span><span class="sxs-lookup"><span data-stu-id="42bec-118">Organizations can also integrate NPS with Azure MFA tooenhance security and provide a high level of compliance.</span></span> <span data-ttu-id="42bec-119">這有助於確保使用者建立雙步驟驗證 toolog toohello 遠端桌面閘道上。</span><span class="sxs-lookup"><span data-stu-id="42bec-119">This helps ensure that users establish two-step verification toolog on toohello Remote Desktop Gateway.</span></span> <span data-ttu-id="42bec-120">針對使用者 toobe 授與存取權，他們必須提供其使用者名稱/密碼組合與 hello 使用者的資訊有其控制項中。</span><span class="sxs-lookup"><span data-stu-id="42bec-120">For users toobe granted access, they must provide their username/password combination with information that hello user has in their control.</span></span> <span data-ttu-id="42bec-121">這項資訊必須能夠讓人信任且無法輕易複製，例如行動電話號碼、室內電話號碼、行動裝置上的應用程式等等。</span><span class="sxs-lookup"><span data-stu-id="42bec-121">This information must be trusted and not easily duplicated, such as a cell phone number, landline number, application on a mobile device, and so on.</span></span>

<span data-ttu-id="42bec-122">先前 toohello 可用性的 hello azure NPS 擴充功能，客戶必須承擔更多的 tooimplement 雙步驟驗證整合 NPS 和 Azure MFA 環境有 tooconfigure 和維護個別的 MFA 伺服器在 hello 與內部部署環境中記載於[遠端桌面閘道和使用 RADIUS 的 Azure Multi-factor Authentication Server](multi-factor-authentication-get-started-server-rdg.md)。</span><span class="sxs-lookup"><span data-stu-id="42bec-122">Prior toohello availability of hello NPS extension for Azure, customers who wished tooimplement two-step verification for integrated NPS and Azure MFA environments had tooconfigure and maintain a separate MFA Server in hello on-premises environment as documented in [Remote Desktop Gateway and Azure Multi-Factor Authentication Server using RADIUS](multi-factor-authentication-get-started-server-rdg.md).</span></span>

<span data-ttu-id="42bec-123">azure 的 hello NPS 擴充功能 hello 可用性現在可以讓組織 hello 選擇 toodeploy 在內部部署基礎 MFA 解決方案或以雲端為基礎 MFA 解決方案 toosecure RADIUS 用戶端驗證。</span><span class="sxs-lookup"><span data-stu-id="42bec-123">hello availability of hello NPS extension for Azure now gives organizations hello choice toodeploy either an on-premises based MFA solution or a cloud-based MFA solution toosecure RADIUS client authentication.</span></span>

## <a name="authentication-flow"></a><span data-ttu-id="42bec-124">驗證流程</span><span class="sxs-lookup"><span data-stu-id="42bec-124">Authentication Flow</span></span>

<span data-ttu-id="42bec-125">使用者 toobe 授與存取 toonetwork 資源，透過遠端桌面閘道，必須符合 hello 一個 RD 連線授權原則 (RD CAP) 和一個 RD 資源授權原則 (RD RAP) 中所指定的條件。</span><span class="sxs-lookup"><span data-stu-id="42bec-125">For users toobe granted access toonetwork resources through a Remote Desktop Gateway, they must meet hello conditions specified in one RD Connection Authorization Policy (RD CAP) and one RD Resource Authorization Policy (RD RAP).</span></span> <span data-ttu-id="42bec-126">RD Cap 指定誰是授權的 tooconnect tooRD 閘道。</span><span class="sxs-lookup"><span data-stu-id="42bec-126">RD CAPs specify who is authorized tooconnect tooRD Gateways.</span></span> <span data-ttu-id="42bec-127">RD Rap 指定 hello 網路資源，例如遠端桌面或遠端的應用程式，該 hello 允許使用者 tooconnect toothrough hello RD 閘道。</span><span class="sxs-lookup"><span data-stu-id="42bec-127">RD RAPs specify hello network resources, such as remote desktops or remote apps, that hello user is allowed tooconnect toothrough hello RD Gateway.</span></span> 

<span data-ttu-id="42bec-128">RD 閘道可以設定的 toouse RD Cap 的集中原則存放區。</span><span class="sxs-lookup"><span data-stu-id="42bec-128">An RD Gateway can be configured toouse a central policy store for RD CAPs.</span></span> <span data-ttu-id="42bec-129">RD Rap 無法使用集中原則，在處理 hello RD 閘道上。</span><span class="sxs-lookup"><span data-stu-id="42bec-129">RD RAPs cannot use a central policy, as they are processed on hello RD Gateway.</span></span> <span data-ttu-id="42bec-130">舉例來說，RD 閘道設定 toouse RD Cap 的集中原則存放區是 RADIUS 用戶端 tooanother NPS 伺服器做為 hello 中央原則存放區。</span><span class="sxs-lookup"><span data-stu-id="42bec-130">An example of an RD Gateway configured toouse a central policy store for RD CAPs is a RADIUS client tooanother NPS server that serves as hello central policy store.</span></span>

<span data-ttu-id="42bec-131">NPS 擴充 azure hello 與 hello NPS 和遠端桌面閘道整合時，hello 成功驗證流程如下所示：</span><span class="sxs-lookup"><span data-stu-id="42bec-131">When hello NPS extension for Azure is integrated with hello NPS and Remote Desktop Gateway, hello successful authentication flow is as follows:</span></span>

1. <span data-ttu-id="42bec-132">hello 遠端桌面閘道伺服器會收到的驗證要求，從遠端桌面使用者 tooconnect tooa 資源，例如遠端桌面工作階段。</span><span class="sxs-lookup"><span data-stu-id="42bec-132">hello Remote Desktop Gateway server receives an authentication request from a remote desktop user tooconnect tooa resource, such as a Remote Desktop session.</span></span> <span data-ttu-id="42bec-133">做為 RADIUS 用戶端時，hello 遠端桌面閘道伺服器 hello 要求 tooa RADIUS Access-request 訊息轉換，並將傳送 hello 訊息 toohello RADIUS (NPS) 伺服器 hello NPS 擴充功能的安裝位置。</span><span class="sxs-lookup"><span data-stu-id="42bec-133">Acting as a RADIUS client, hello Remote Desktop Gateway server converts hello request tooa RADIUS Access-Request message and sends hello message toohello RADIUS (NPS) server where hello NPS extension is installed.</span></span> 
2. <span data-ttu-id="42bec-134">hello 使用者名稱和密碼組合 Active Directory 中驗證而且 hello 使用者驗證。</span><span class="sxs-lookup"><span data-stu-id="42bec-134">hello username and password combination is verified in Active Directory and hello user is authenticated.</span></span>
3. <span data-ttu-id="42bec-135">如果所有 hello 中所指定的條件 hello NPS 連線要求，並符合 hello 網路原則 (例如，時間一天或群組的成員資格的限制)，hello NPS 擴充觸發程序使用 Azure MFA 的次要驗證的要求。</span><span class="sxs-lookup"><span data-stu-id="42bec-135">If all hello conditions as specified in hello NPS Connection Request and hello Network Policies are met (for example, time of day or group membership restrictions), hello NPS extension triggers a request for secondary authentication with Azure MFA.</span></span> 
4. <span data-ttu-id="42bec-136">Azure MFA 與 Azure AD 通訊、 擷取 hello 使用者詳細資料，然後執行 hello 次要驗證使用 hello hello 使用者 （簡訊、 行動裝置應用程式，等等） 所設定的方法。</span><span class="sxs-lookup"><span data-stu-id="42bec-136">Azure MFA communicates with Azure AD, retrieves hello user’s details, and performs hello secondary authentication using hello method configured by hello user (text message, mobile app, and so on).</span></span> 
5. <span data-ttu-id="42bec-137">成功時的 hello MFA 挑戰，Azure MFA 通訊 hello 結果 toohello NPS 擴充功能。</span><span class="sxs-lookup"><span data-stu-id="42bec-137">Upon success of hello MFA challenge, Azure MFA communicates hello result toohello NPS extension.</span></span>
6. <span data-ttu-id="42bec-138">hello 擴充功能安裝所在的 hello NPS 伺服器會傳送 hello RD CAP 原則 toohello 遠端桌面閘道伺服器的 RADIUS 存取接受訊息。</span><span class="sxs-lookup"><span data-stu-id="42bec-138">hello NPS server where hello extension is installed sends a RADIUS Access-Accept message for hello RD CAP policy toohello Remote Desktop Gateway server.</span></span>
7. <span data-ttu-id="42bec-139">hello 使用者被授與存取 toohello 要求透過 hello RD 閘道的網路資源。</span><span class="sxs-lookup"><span data-stu-id="42bec-139">hello user is granted access toohello requested network resource through hello RD Gateway.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="42bec-140">必要條件</span><span class="sxs-lookup"><span data-stu-id="42bec-140">Prerequisites</span></span>
<span data-ttu-id="42bec-141">本節詳述 hello hello 遠端桌面閘道與整合 Azure MFA 之前所需的必要條件。</span><span class="sxs-lookup"><span data-stu-id="42bec-141">This section details hello prerequisites necessary before integrating Azure MFA with hello Remote Desktop Gateway.</span></span> <span data-ttu-id="42bec-142">在開始之前，您必須擁有下列先決條件備妥的 hello。</span><span class="sxs-lookup"><span data-stu-id="42bec-142">Before you begin, you must have hello following prerequisites in place.</span></span>  

* <span data-ttu-id="42bec-143">遠端桌面服務 (RDS) 基礎結構</span><span class="sxs-lookup"><span data-stu-id="42bec-143">Remote Desktop Services (RDS) infrastructure</span></span>
* <span data-ttu-id="42bec-144">Azure MFA 授權</span><span class="sxs-lookup"><span data-stu-id="42bec-144">Azure MFA License</span></span>
* <span data-ttu-id="42bec-145">Windows Server 軟體</span><span class="sxs-lookup"><span data-stu-id="42bec-145">Windows Server software</span></span>
* <span data-ttu-id="42bec-146">網路原則與存取服務 (NPS) 角色</span><span class="sxs-lookup"><span data-stu-id="42bec-146">Network Policy and Access Services (NPS) role</span></span>
* <span data-ttu-id="42bec-147">與內部部署 AD 同步的 Azure AD</span><span class="sxs-lookup"><span data-stu-id="42bec-147">Azure AD synched with on-premises AD</span></span> 
* <span data-ttu-id="42bec-148">Azure Active Directory GUID 識別碼</span><span class="sxs-lookup"><span data-stu-id="42bec-148">Azure Active Directory GUID ID</span></span>

### <a name="remote-desktop-services-rds-infrastructure"></a><span data-ttu-id="42bec-149">遠端桌面服務 (RDS) 基礎結構</span><span class="sxs-lookup"><span data-stu-id="42bec-149">Remote Desktop Services (RDS) infrastructure</span></span>
<span data-ttu-id="42bec-150">您必須備妥中運作中的遠端桌面服務 (RDS) 基礎結構。</span><span class="sxs-lookup"><span data-stu-id="42bec-150">You must have a working Remote Desktop Services (RDS) infrastructure in place.</span></span> <span data-ttu-id="42bec-151">如果不這麼做，您可以在 Azure 中快速建立這個基礎結構，然後使用 hello 下列快速入門範本：[建立遠端桌面工作階段集合部署](https://github.com/Azure/azure-quickstart-templates/tree/ad20c78b36d8e1246f96bb0e7a8741db481f957f/rds-deployment)。</span><span class="sxs-lookup"><span data-stu-id="42bec-151">If you do not, then you can quickly create this infrastructure in Azure using hello following quick start template: [Create Remote Desktop Session Collection deployment](https://github.com/Azure/azure-quickstart-templates/tree/ad20c78b36d8e1246f96bb0e7a8741db481f957f/rds-deployment).</span></span> 

<span data-ttu-id="42bec-152">如果您想 toomanually 建立內部 RDS 基礎結構快速基於測試目的，後續 hello 步驟 toodeploy 其中一個。</span><span class="sxs-lookup"><span data-stu-id="42bec-152">If you wish toomanually create an on-premises RDS infrastructure quickly for testing purposes, follow hello steps toodeploy one.</span></span> 
<span data-ttu-id="42bec-153">**深入了解**：[使用 Azure 快速入門部署 RDS](https://docs.microsoft.com/windows-server/remote/remote-desktop-services/rds-in-azure)和[基本 RDS 基礎結構部署](https://docs.microsoft.com/windows-server/remote/remote-desktop-services/rds-deploy-infrastructure)。</span><span class="sxs-lookup"><span data-stu-id="42bec-153">**Learn more**: [Deploy RDS with Azure quick start](https://docs.microsoft.com/windows-server/remote/remote-desktop-services/rds-in-azure) and [Basic RDS infrastructure deployment](https://docs.microsoft.com/windows-server/remote/remote-desktop-services/rds-deploy-infrastructure).</span></span> 

### <a name="licenses"></a><span data-ttu-id="42bec-154">授權</span><span class="sxs-lookup"><span data-stu-id="42bec-154">Licenses</span></span>
<span data-ttu-id="42bec-155">需要 Azure MFA 的授權，此授權可透過 Azure AD Premium、Enterprise Mobility plus Security (EMS) 或 MFA 訂用帳戶來獲得。</span><span class="sxs-lookup"><span data-stu-id="42bec-155">Required is a license for Azure MFA, which is available through an Azure AD Premium, Enterprise Mobility plus Security (EMS), or an MFA subscription.</span></span> <span data-ttu-id="42bec-156">如需詳細資訊，請參閱[如何 tooget Azure Multi-factor Authentication](multi-factor-authentication-versions-plans.md)。</span><span class="sxs-lookup"><span data-stu-id="42bec-156">For more information, see [How tooget Azure Multi-Factor Authentication](multi-factor-authentication-versions-plans.md).</span></span> <span data-ttu-id="42bec-157">若要進行測試，您可以使用試用版訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="42bec-157">For testing purposes, you can use a trial subscription.</span></span>

### <a name="software"></a><span data-ttu-id="42bec-158">軟體</span><span class="sxs-lookup"><span data-stu-id="42bec-158">Software</span></span>
<span data-ttu-id="42bec-159">hello NPS 擴充功能需要 Windows Server 2008 R2 SP1 或更新版本已安裝的 hello NPS 角色服務。</span><span class="sxs-lookup"><span data-stu-id="42bec-159">hello NPS extension requires Windows Server 2008 R2 SP1 or above with hello NPS role service installed.</span></span> <span data-ttu-id="42bec-160">使用 Windows Server 2016 中未執行本節中的所有 hello 步驟。</span><span class="sxs-lookup"><span data-stu-id="42bec-160">All hello steps in this section were performed using Windows Server 2016.</span></span>

### <a name="network-policy-and-access-services-nps-role"></a><span data-ttu-id="42bec-161">網路原則與存取服務 (NPS) 角色</span><span class="sxs-lookup"><span data-stu-id="42bec-161">Network Policy and Access Services (NPS) role</span></span>
<span data-ttu-id="42bec-162">hello NPS 角色服務提供 hello RADIUS 伺服器和用戶端功能以及網路存取原則的健全狀況服務。</span><span class="sxs-lookup"><span data-stu-id="42bec-162">hello NPS role service provides hello RADIUS server and client functionality as well as Network Access Policy health service.</span></span> <span data-ttu-id="42bec-163">此角色必須安裝在您的基礎結構中的至少兩部電腦上： hello 遠端桌面閘道，而另一個成員伺服器或網域控制站。</span><span class="sxs-lookup"><span data-stu-id="42bec-163">This role must be installed on at least two computers in your infrastructure: hello Remote Desktop Gateway and another member server or domain controller.</span></span> <span data-ttu-id="42bec-164">根據預設，hello 角色已經設定為遠端桌面閘道 hello hello 電腦上。</span><span class="sxs-lookup"><span data-stu-id="42bec-164">By default, hello role is already present on hello computer configured as hello Remote Desktop Gateway.</span></span>  <span data-ttu-id="42bec-165">您必須也 hello NPS 角色上安裝至少另一部電腦，例如網域控制站或成員伺服器上。</span><span class="sxs-lookup"><span data-stu-id="42bec-165">You must also install hello NPS role on at least on another computer, such as a domain controller or member server.</span></span>

<span data-ttu-id="42bec-166">如需有關安裝 hello NPS 角色服務的 Windows Server 2012 或較舊，請參閱[安裝 NAP 健康原則伺服器](https://technet.microsoft.com/library/dd296890.aspx)。</span><span class="sxs-lookup"><span data-stu-id="42bec-166">For information on installing hello NPS role service Windows Server 2012 or older, see [Install a NAP Health Policy Server](https://technet.microsoft.com/library/dd296890.aspx).</span></span> <span data-ttu-id="42bec-167">如需 NPS，網域控制站上的包括 hello 建議 tooinstall NPS 的最佳作法的說明，請參閱[NPS 的最佳作法](https://technet.microsoft.com/library/cc771746)。</span><span class="sxs-lookup"><span data-stu-id="42bec-167">For a description of best practices for NPS, including hello recommendation tooinstall NPS on a domain controller, see [Best Practices for NPS](https://technet.microsoft.com/library/cc771746).</span></span>

### <a name="azure-active-directory-synched-with-on-premises-active-directory"></a><span data-ttu-id="42bec-168">與內部部署 Active Directory 同步的 Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="42bec-168">Azure Active Directory synched with on-premises Active Directory</span></span> 
<span data-ttu-id="42bec-169">toouse hello NPS 擴充內部必須與 Azure AD 進行同步處理並啟用 MFA 的使用者。</span><span class="sxs-lookup"><span data-stu-id="42bec-169">toouse hello NPS extension, on-premises users must be synced with Azure AD and enabled for MFA.</span></span> <span data-ttu-id="42bec-170">這一節假設內部部署使用者已使用 AD Connect 來與 Azure AD 保持同步。</span><span class="sxs-lookup"><span data-stu-id="42bec-170">This section assumes that on-premises users are synched with Azure AD using AD Connect.</span></span> <span data-ttu-id="42bec-171">如需 Azure AD Connect 的相關資訊，請參閱[整合您的內部部署目錄與 Azure Active Directory](../active-directory/connect/active-directory-aadconnect.md)。</span><span class="sxs-lookup"><span data-stu-id="42bec-171">For information on Azure AD connect, see [Integrate your on-premises directories with Azure Active Directory](../active-directory/connect/active-directory-aadconnect.md).</span></span> 

### <a name="azure-active-directory-guid-id"></a><span data-ttu-id="42bec-172">Azure Active Directory GUID 識別碼</span><span class="sxs-lookup"><span data-stu-id="42bec-172">Azure Active Directory GUID ID</span></span>
<span data-ttu-id="42bec-173">tooinstall NPS，您需要 tooknow hello hello Azure AD 的 GUID。</span><span class="sxs-lookup"><span data-stu-id="42bec-173">tooinstall NPS, you need tooknow hello GUID of hello Azure AD.</span></span> <span data-ttu-id="42bec-174">下面將提供指示來尋找 hello hello Azure AD 的 GUID。</span><span class="sxs-lookup"><span data-stu-id="42bec-174">Instructions for finding hello GUID of hello Azure AD are provided below.</span></span>

## <a name="configure-multi-factor-authentication"></a><span data-ttu-id="42bec-175">設定 Multi-Factor Authentication</span><span class="sxs-lookup"><span data-stu-id="42bec-175">Configure Multi-Factor Authentication</span></span> 
<span data-ttu-id="42bec-176">本節中的 hello 遠端桌面閘道與整合 Azure MFA 的指示。</span><span class="sxs-lookup"><span data-stu-id="42bec-176">This section provides instructions for integrating Azure MFA with hello Remote Desktop Gateway.</span></span> <span data-ttu-id="42bec-177">身為管理員，您必須設定 hello Azure MFA 服務之前，使用者可以自行註冊其多因素裝置或應用程式。</span><span class="sxs-lookup"><span data-stu-id="42bec-177">As an administrator, you must configure hello Azure MFA service before users can self-register their multi-factor devices or applications.</span></span>

<span data-ttu-id="42bec-178">中的 hello 步驟[開始使用 Azure Multi-factor Authentication hello 定域機組中](multi-factor-authentication-get-started-cloud.md)tooenable MFA 為您的 Azure AD 使用者。</span><span class="sxs-lookup"><span data-stu-id="42bec-178">Follow hello steps in [Getting started with Azure Multi-Factor Authentication in hello cloud](multi-factor-authentication-get-started-cloud.md) tooenable MFA for your Azure AD users.</span></span> 

### <a name="configure-accounts-for-two-step-verification"></a><span data-ttu-id="42bec-179">為帳戶設定雙步驟驗證</span><span class="sxs-lookup"><span data-stu-id="42bec-179">Configure accounts for two-step verification</span></span>
<span data-ttu-id="42bec-180">一旦帳戶已啟用 MFA，您無法登入 tooresources 由 hello MFA 原則之前的第二個驗證因素 hello 已通過驗證，使用兩步驟驗證，您已成功設定信任的裝置 toouse。</span><span class="sxs-lookup"><span data-stu-id="42bec-180">Once an account has been enabled for MFA, you cannot sign in tooresources governed by hello MFA policy until you have successfully configured a trusted device toouse for hello second authentication factor have authenticated using two-step verification.</span></span>

<span data-ttu-id="42bec-181">中的 hello 步驟[Azure Multi-factor Authentication 什麼適合我？](./end-user/multi-factor-authentication-end-user.md) toounderstand 並正確設定 MFA 的裝置與您的使用者帳戶。</span><span class="sxs-lookup"><span data-stu-id="42bec-181">Follow hello steps in [What does Azure Multi-Factor Authentication mean for me?](./end-user/multi-factor-authentication-end-user.md) toounderstand and properly configure your devices for MFA with your user account.</span></span>

## <a name="install-and-configure-nps-extension"></a><span data-ttu-id="42bec-182">安裝和設定 NPS 擴充功能</span><span class="sxs-lookup"><span data-stu-id="42bec-182">Install and configure NPS extension</span></span>
<span data-ttu-id="42bec-183">本節提供設定以 hello 遠端桌面閘道用戶端驗證的 RDS 基礎結構 toouse Azure MFA 的指示。</span><span class="sxs-lookup"><span data-stu-id="42bec-183">This section provides instructions for configuring RDS infrastructure toouse Azure MFA for client authentication with hello Remote Desktop Gateway.</span></span>

### <a name="acquire-azure-active-directory-guid-id"></a><span data-ttu-id="42bec-184">取得 Azure Active Directory GUID 識別碼</span><span class="sxs-lookup"><span data-stu-id="42bec-184">Acquire Azure Active Directory GUID ID</span></span>

<span data-ttu-id="42bec-185">Hello NPS 擴充功能的 hello 組態的一部分，您需要 toosupply 系統管理員認證和 hello Azure AD 識別碼的 Azure AD 租用戶。</span><span class="sxs-lookup"><span data-stu-id="42bec-185">As part of hello configuration of hello NPS extension, you need toosupply admin credentials and hello Azure AD ID for your Azure AD tenant.</span></span> <span data-ttu-id="42bec-186">下列步驟的 hello 顯示您 tooget hello 租用戶的識別碼。</span><span class="sxs-lookup"><span data-stu-id="42bec-186">hello following steps show you how tooget hello tenant ID.</span></span>

1. <span data-ttu-id="42bec-187">登入 toohello [Azure 入口網站](https://portal.azure.com)hello Azure hello 全域管理員身分租用戶。</span><span class="sxs-lookup"><span data-stu-id="42bec-187">Sign in toohello [Azure portal](https://portal.azure.com) as hello global administrator of hello Azure tenant.</span></span>
2. <span data-ttu-id="42bec-188">在左瀏覽 hello，選取 hello **Azure Active Directory**圖示。</span><span class="sxs-lookup"><span data-stu-id="42bec-188">In hello left navigation, select hello **Azure Active Directory** icon.</span></span>
3. <span data-ttu-id="42bec-189">選取 [屬性] 。</span><span class="sxs-lookup"><span data-stu-id="42bec-189">Select **Properties**.</span></span>
4. <span data-ttu-id="42bec-190">在 hello 屬性刀鋒視窗中，目錄識別碼 hello 旁邊按一下 hello**複製**圖示，如下所示 toocopy hello 識別碼 tooclipboard。</span><span class="sxs-lookup"><span data-stu-id="42bec-190">In hello Properties blade, beside hello Directory ID, click hello **Copy** icon, as shown below, toocopy hello ID tooclipboard.</span></span>

 ![屬性](./media/nps-extension-remote-desktop-gateway/image1.png)

### <a name="install-hello-nps-extension"></a><span data-ttu-id="42bec-192">安裝 hello NPS 擴充功能</span><span class="sxs-lookup"><span data-stu-id="42bec-192">Install hello NPS extension</span></span>
<span data-ttu-id="42bec-193">具有 hello 網路原則與存取服務 」 (NPS) 角色安裝在伺服器上安裝 hello NPS 擴充功能。</span><span class="sxs-lookup"><span data-stu-id="42bec-193">Install hello NPS extension on a server that has hello Network Policy and Access Services (NPS) role installed.</span></span> <span data-ttu-id="42bec-194">這項功能可以為您的設計 hello RADIUS 伺服器。</span><span class="sxs-lookup"><span data-stu-id="42bec-194">This functions as hello RADIUS server for your design.</span></span> 

>[!Important]
> <span data-ttu-id="42bec-195">請確定您沒有遠端桌面閘道伺服器上安裝 hello NPS 擴充功能。</span><span class="sxs-lookup"><span data-stu-id="42bec-195">Be sure you do not install hello NPS extension on your Remote Desktop Gateway server.</span></span>
> 

1. <span data-ttu-id="42bec-196">下載 hello [NPS 擴充](https://aka.ms/npsmfa)。</span><span class="sxs-lookup"><span data-stu-id="42bec-196">Download hello [NPS extension](https://aka.ms/npsmfa).</span></span> 
2. <span data-ttu-id="42bec-197">將複製 hello 安裝程式可執行檔 (NpsExtnForAzureMfaInstaller.exe) toohello NPS 伺服器。</span><span class="sxs-lookup"><span data-stu-id="42bec-197">Copy hello setup executable file (NpsExtnForAzureMfaInstaller.exe) toohello NPS server.</span></span>
3. <span data-ttu-id="42bec-198">在 hello NPS 伺服器上，按兩下**NpsExtnForAzureMfaInstaller.exe**。</span><span class="sxs-lookup"><span data-stu-id="42bec-198">On hello NPS server, double-click **NpsExtnForAzureMfaInstaller.exe**.</span></span> <span data-ttu-id="42bec-199">出現提示時，按一下 [執行]。</span><span class="sxs-lookup"><span data-stu-id="42bec-199">If prompted, click **Run**.</span></span>
4. <span data-ttu-id="42bec-200">在 hello NPS 擴充功能的 Azure MFA 對話方塊中，檢閱 hello 軟體授權條款，請檢查**toohello 授權條款和條件，即表示我同意**，然後按一下**安裝**。</span><span class="sxs-lookup"><span data-stu-id="42bec-200">In hello NPS Extension for Azure MFA dialog box, review hello software license terms, check **I agree toohello license terms and conditions**, and click **Install**.</span></span>
 
  ![Azure MFA 設定](./media/nps-extension-remote-desktop-gateway/image2.png)

5. <span data-ttu-id="42bec-202">在 hello NPS 擴充功能的 Azure MFA 對話方塊中，按一下 [關閉]。</span><span class="sxs-lookup"><span data-stu-id="42bec-202">In hello NPS Extension for Azure MFA dialog box, click Close.</span></span> 

  ![Azure MFA 的 NPS 擴充功能](./media/nps-extension-remote-desktop-gateway/image3.png)

### <a name="configure-certificates-for-use-with-hello-nps-extension-using-a-powershell-script"></a><span data-ttu-id="42bec-204">Hello NPS 擴充功能的 PowerShell 指令碼以設定使用的憑證</span><span class="sxs-lookup"><span data-stu-id="42bec-204">Configure certificates for use with hello NPS extension using a PowerShell script</span></span>
<span data-ttu-id="42bec-205">接下來，您需要使用 hello NPS 擴充 tooensure 安全通訊和保證的 tooconfigure 憑證。</span><span class="sxs-lookup"><span data-stu-id="42bec-205">Next, you need tooconfigure certificates for use by hello NPS extension tooensure secure communications and assurance.</span></span> <span data-ttu-id="42bec-206">hello NPS 元件包括 Windows PowerShell 指令碼，以設定 nps 使用的自我簽署的憑證。</span><span class="sxs-lookup"><span data-stu-id="42bec-206">hello NPS components include a Windows PowerShell script that configures a self-signed certificate for use with NPS.</span></span> 

<span data-ttu-id="42bec-207">hello 指令碼會執行下列動作的 hello:</span><span class="sxs-lookup"><span data-stu-id="42bec-207">hello script performs hello following actions:</span></span>

* <span data-ttu-id="42bec-208">建立自我簽署憑證</span><span class="sxs-lookup"><span data-stu-id="42bec-208">Creates a self-signed certificate</span></span>
* <span data-ttu-id="42bec-209">將公開金鑰憑證 tooservice 上 Azure AD 主體產生關聯</span><span class="sxs-lookup"><span data-stu-id="42bec-209">Associates public key of certificate tooservice principal on Azure AD</span></span>
* <span data-ttu-id="42bec-210">存放區 hello hello 本機電腦存放區中的憑證</span><span class="sxs-lookup"><span data-stu-id="42bec-210">Stores hello cert in hello local machine store</span></span>
* <span data-ttu-id="42bec-211">授與存取 toohello 憑證的私用金鑰 toohello 網路使用者</span><span class="sxs-lookup"><span data-stu-id="42bec-211">Grants access toohello certificate’s private key toohello network user</span></span>
* <span data-ttu-id="42bec-212">重新啟動網路原則伺服器服務</span><span class="sxs-lookup"><span data-stu-id="42bec-212">Restarts Network Policy Server service</span></span>

<span data-ttu-id="42bec-213">如果您想 toouse 您自己的憑證，您在 Azure AD 中，需要您憑證 toohello 服務主體的 tooassociate hello 公用等等。</span><span class="sxs-lookup"><span data-stu-id="42bec-213">If you want toouse your own certificates, you need tooassociate hello public of your certificate toohello service principle on Azure AD, and so on.</span></span>

<span data-ttu-id="42bec-214">toouse hello 指令碼會使用您的 Azure AD 系統管理員認證提供 hello 副檔名和 hello 您之前複製的 Azure AD 租用戶識別碼。</span><span class="sxs-lookup"><span data-stu-id="42bec-214">toouse hello script, provide hello extension with your Azure AD Admin credentials and hello Azure AD tenant ID that you copied earlier.</span></span> <span data-ttu-id="42bec-215">Hello NPS 擴充功能安裝在每個 NPS 伺服器上執行 hello 指令碼。</span><span class="sxs-lookup"><span data-stu-id="42bec-215">Run hello script on each NPS server where you installed hello NPS extension.</span></span> <span data-ttu-id="42bec-216">然後 hello 遵循：</span><span class="sxs-lookup"><span data-stu-id="42bec-216">Then do hello following:</span></span>

1. <span data-ttu-id="42bec-217">開啟系統管理 Windows PowerShell 提示字元。</span><span class="sxs-lookup"><span data-stu-id="42bec-217">Open an administrative Windows PowerShell prompt.</span></span>
2. <span data-ttu-id="42bec-218">在 hello PowerShell 提示字元中輸入**cd 'c:\Program Files\Microsoft\AzureMfa\Config'**，按**ENTER**。</span><span class="sxs-lookup"><span data-stu-id="42bec-218">At hello PowerShell prompt, type **cd ‘c:\Program Files\Microsoft\AzureMfa\Config’**, and press **ENTER**.</span></span>
3. <span data-ttu-id="42bec-219">輸入 _.\AzureMfsNpsExtnConfigSetup.ps1_，然後按 **ENTER**。</span><span class="sxs-lookup"><span data-stu-id="42bec-219">Type _.\AzureMfsNpsExtnConfigSetup.ps1_, and press **ENTER**.</span></span> <span data-ttu-id="42bec-220">hello 指令碼會檢查 toosee hello Azure Active Directory PowerShell 模組安裝。</span><span class="sxs-lookup"><span data-stu-id="42bec-220">hello script checks toosee if hello Azure Active Directory PowerShell module is installed.</span></span> <span data-ttu-id="42bec-221">如果未安裝，hello 指令碼會安裝 hello 模組。</span><span class="sxs-lookup"><span data-stu-id="42bec-221">If not installed, hello script installs hello module for you.</span></span>

  ![Azure AD PowerShell](./media/nps-extension-remote-desktop-gateway/image4.png)
  
4. <span data-ttu-id="42bec-223">Hello 指令碼驗證的 hello PowerShell 模組的 hello 安裝之後，它會顯示 hello Azure Active Directory PowerShell 模組對話方塊。</span><span class="sxs-lookup"><span data-stu-id="42bec-223">After hello script verifies hello installation of hello PowerShell module, it displays hello Azure Active Directory PowerShell module dialog box.</span></span> <span data-ttu-id="42bec-224">在 [hello] 對話方塊中，輸入您的 Azure AD 系統管理員認證和密碼，然後按一下**登入**。</span><span class="sxs-lookup"><span data-stu-id="42bec-224">In hello dialog box, enter your Azure AD admin credentials and password, and click **Sign In**.</span></span>

  ![開啟 Powershell 帳戶](./media/nps-extension-remote-desktop-gateway/image5.png)

5. <span data-ttu-id="42bec-226">出現提示時，貼上您先前複製 toohello 剪貼簿的 hello 租用戶識別碼，然後按**ENTER**。</span><span class="sxs-lookup"><span data-stu-id="42bec-226">When prompted, paste hello tenant ID you copied toohello clipboard earlier, and press **ENTER**.</span></span>

  ![輸入租用戶識別碼](./media/nps-extension-remote-desktop-gateway/image6.png)

6. <span data-ttu-id="42bec-228">hello 指令碼會建立自我簽署的憑證，並執行其他組態變更。</span><span class="sxs-lookup"><span data-stu-id="42bec-228">hello script creates a self-signed certificate and performs other configuration changes.</span></span> <span data-ttu-id="42bec-229">hello 輸出應類似如下所示的 hello 影像。</span><span class="sxs-lookup"><span data-stu-id="42bec-229">hello output should be like hello image shown below.</span></span>

  ![自我簽署憑證](./media/nps-extension-remote-desktop-gateway/image7.png)

## <a name="configure-nps-components-on-remote-desktop-gateway"></a><span data-ttu-id="42bec-231">設定遠端桌面閘道上的 NPS 元件</span><span class="sxs-lookup"><span data-stu-id="42bec-231">Configure NPS components on Remote Desktop Gateway</span></span>
<span data-ttu-id="42bec-232">在本節中，您可以設定 hello 遠端桌面閘道連線授權原則和其他 RADIUS 設定。</span><span class="sxs-lookup"><span data-stu-id="42bec-232">In this section, you configure hello Remote Desktop Gateway connection authorization policies and other RADIUS settings.</span></span>

<span data-ttu-id="42bec-233">hello 驗證流程要求，RADIUS 訊息交換之間 hello 遠端桌面閘道和 hello NPS 伺服器 hello NPS 伺服器的安裝位置。</span><span class="sxs-lookup"><span data-stu-id="42bec-233">hello authentication flow requires that RADIUS messages be exchanged between hello Remote Desktop Gateway and hello NPS server where hello NPS Server is installed.</span></span> <span data-ttu-id="42bec-234">這表示，您必須設定 RADIUS 用戶端 hello NPS 擴充功能安裝所在的遠端桌面閘道和 hello NPS 伺服器上。</span><span class="sxs-lookup"><span data-stu-id="42bec-234">This means that you must configure RADIUS client settings on both Remote Desktop Gateway and hello NPS server where hello NPS extension is installed.</span></span> 

### <a name="configure-remote-desktop-gateway-connection-authorization-policies-toouse-central-store"></a><span data-ttu-id="42bec-235">設定遠端桌面閘道連線授權原則 toouse 中央存放區</span><span class="sxs-lookup"><span data-stu-id="42bec-235">Configure Remote Desktop Gateway connection authorization policies toouse central store</span></span>
<span data-ttu-id="42bec-236">遠端桌面連線授權原則 (RD Cap) 指定連線 tooa 遠端桌面閘道伺服器 hello 需求。</span><span class="sxs-lookup"><span data-stu-id="42bec-236">Remote Desktop connection authorization policies (RD CAPs) specify hello requirements for connecting tooa Remote Desktop Gateway server.</span></span> <span data-ttu-id="42bec-237">RD CAP 可以儲存在本機 (預設值)，也可以儲存在執行 NPS 的中央 RD CAP 存放區中。</span><span class="sxs-lookup"><span data-stu-id="42bec-237">RD CAPs can be stored locally (default) or they can be stored in a central RD CAP store that is running NPS.</span></span> <span data-ttu-id="42bec-238">Azure MFA 與 RDS tooconfigure 整合，您需要 toospecify hello 中央存放區使用。</span><span class="sxs-lookup"><span data-stu-id="42bec-238">tooconfigure integration of Azure MFA with RDS, you need toospecify hello use of a central store.</span></span>

1. <span data-ttu-id="42bec-239">Hello RD 閘道伺服器上，開啟**伺服器管理員**。</span><span class="sxs-lookup"><span data-stu-id="42bec-239">On hello RD Gateway server, open **Server Manager**.</span></span> 
2. <span data-ttu-id="42bec-240">在 [hello] 功能表上按一下**工具**，點太**遠端桌面服務**，然後按一下**遠端桌面閘道管理員**。</span><span class="sxs-lookup"><span data-stu-id="42bec-240">On hello menu, click **Tools**, point too**Remote Desktop Services**, and then click **Remote Desktop Gateway Manager**.</span></span>

  ![遠端桌面服務問題](./media/nps-extension-remote-desktop-gateway/image8.png)

3. <span data-ttu-id="42bec-242">在 hello RD 閘道管理員，以滑鼠右鍵按一下**\[伺服器名稱\]（本機）**，按一下**屬性**。</span><span class="sxs-lookup"><span data-stu-id="42bec-242">In hello RD Gateway Manger, right-click **\[Server Name\] (Local)**, and click **Properties**.</span></span>

  ![伺服器名稱](./media/nps-extension-remote-desktop-gateway/image9.png)

4. <span data-ttu-id="42bec-244">在 hello 內容 對話方塊中，選取 hello **RD CAP**存放區索引標籤。</span><span class="sxs-lookup"><span data-stu-id="42bec-244">In hello Properties dialog box, select hello **RD CAP** Store tab.</span></span>
5. <span data-ttu-id="42bec-245">在 hello RD CAP 存放區索引標籤上，選取 **執行 NPS 的中央伺服器**。</span><span class="sxs-lookup"><span data-stu-id="42bec-245">On hello RD CAP Store tab, select **Central Server running NPS**.</span></span> 
6. <span data-ttu-id="42bec-246">在 hello**輸入 hello 執行 NPS 的伺服器名稱或 IP 位址**欄位中，輸入 hello IP 位址或伺服器名稱的 hello 伺服器 hello NPS 擴充功能的安裝位置。</span><span class="sxs-lookup"><span data-stu-id="42bec-246">In hello **Enter a name or IP address for hello server running NPS** field, type hello IP address or server name of hello server where you installed hello NPS extension.</span></span>

  ![輸入名稱或 IP 位址](./media/nps-extension-remote-desktop-gateway/image10.png)
  
7. <span data-ttu-id="42bec-248">按一下 [新增] 。</span><span class="sxs-lookup"><span data-stu-id="42bec-248">Click **Add**.</span></span>
8. <span data-ttu-id="42bec-249">在 hello**共用密碼**對話方塊中，輸入共用的密碼，然後按一下**確定**。</span><span class="sxs-lookup"><span data-stu-id="42bec-249">In hello **Shared Secret** dialog box, enter a shared secret, and then click **OK**.</span></span> <span data-ttu-id="42bec-250">請確定您記錄這個共用的密碼，並安全地儲存 hello 記錄。</span><span class="sxs-lookup"><span data-stu-id="42bec-250">Ensure you record this shared secret and store hello record securely.</span></span>

 >[!NOTE]
 ><span data-ttu-id="42bec-251">共用的密碼可用 tooestablish hello RADIUS 伺服器與用戶端之間的信任。</span><span class="sxs-lookup"><span data-stu-id="42bec-251">Shared secret is used tooestablish trust between hello RADIUS servers and clients.</span></span> <span data-ttu-id="42bec-252">建立長而複雜的密碼。</span><span class="sxs-lookup"><span data-stu-id="42bec-252">Create a long and complex password.</span></span>
 >

 ![共用祕密](./media/nps-extension-remote-desktop-gateway/image11.png)

9. <span data-ttu-id="42bec-254">按一下**確定**tooclose hello 對話方塊。</span><span class="sxs-lookup"><span data-stu-id="42bec-254">Click **OK** tooclose hello dialog box.</span></span>

### <a name="configure-radius-timeout-value-on-remote-desktop-gateway-nps"></a><span data-ttu-id="42bec-255">在遠端桌面閘道 NPS 上設定 RADIUS 逾時值</span><span class="sxs-lookup"><span data-stu-id="42bec-255">Configure RADIUS timeout value on Remote Desktop Gateway NPS</span></span>
<span data-ttu-id="42bec-256">那里的 tooensure 時間 toovalidate 使用者的認證、 執行雙步驟驗證、 接收回應，並回應 tooRADIUS 訊息，則是必要的 tooadjust hello RADIUS 逾時值。</span><span class="sxs-lookup"><span data-stu-id="42bec-256">tooensure there is time toovalidate users’ credentials, perform two-step verification, receive responses, and respond tooRADIUS messages, it is necessary tooadjust hello RADIUS timeout value.</span></span>

1. <span data-ttu-id="42bec-257">Hello RD 閘道伺服器上，在 [伺服器管理員] 中，按一下**工具**，然後按一下**網路原則伺服器**。</span><span class="sxs-lookup"><span data-stu-id="42bec-257">On hello RD Gateway server, in Server Manager, click **Tools**, and then click **Network Policy Server**.</span></span> 
2. <span data-ttu-id="42bec-258">在 hello **NPS （本機）**主控台中，展開**RADIUS 用戶端和伺服器**，然後選取**遠端 RADIUS 伺服器**。</span><span class="sxs-lookup"><span data-stu-id="42bec-258">In hello **NPS (Local)** console, expand **RADIUS Clients and Servers**, and select **Remote RADIUS Server**.</span></span>

 ![遠端 RADIUS 伺服器](./media/nps-extension-remote-desktop-gateway/image12.png)

3. <span data-ttu-id="42bec-260">在 [hello] 詳細資料窗格中，按兩下**TS GATEWAY SERVER GROUP**。</span><span class="sxs-lookup"><span data-stu-id="42bec-260">In hello details pane, double-click **TS GATEWAY SERVER GROUP**.</span></span>

 >[!NOTE]
 ><span data-ttu-id="42bec-261">當您設定 NPS 原則 hello 中央伺服器建立此 RADIUS 伺服器群組。</span><span class="sxs-lookup"><span data-stu-id="42bec-261">This RADIUS Server Group was created when you configured hello central server for NPS policies.</span></span> <span data-ttu-id="42bec-262">hello RD 閘道轉送 RADIUS 訊息 toothis 伺服器或伺服器群組，超過一個 hello 群組中。</span><span class="sxs-lookup"><span data-stu-id="42bec-262">hello RD Gateway forwards RADIUS messages toothis server or group of servers, if more than one in hello group.</span></span>
 >

4. <span data-ttu-id="42bec-263">在 [hello **TS 閘道伺服器群組內容**] 對話方塊中，選取 hello IP 位址或名稱的 hello 設定 toostore RD Cap 的 NPS 伺服器，然後按一下**編輯**。</span><span class="sxs-lookup"><span data-stu-id="42bec-263">In hello **TS GATEWAY SERVER GROUP Properties** dialog box, select hello IP address or name of hello NPS server you configured toostore RD CAPs, and then click **Edit**.</span></span> 

 ![TS Gateway Server Group](./media/nps-extension-remote-desktop-gateway/image13.png)

5. <span data-ttu-id="42bec-265">在 [hello**編輯 RADIUS 伺服器**對話方塊中，選取 hello**負載平衡**] 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="42bec-265">In hello **Edit RADIUS Server** dialog box, select hello **Load Balancing** tab.</span></span>
6. <span data-ttu-id="42bec-266">在 hello**負載平衡**索引標籤上，在 hello**卸除的要求都視為前，無回應的秒數**欄位中，變更 hello 預設 3 tooa 值介於 30 到 60 秒。</span><span class="sxs-lookup"><span data-stu-id="42bec-266">In hello **Load Balancing** tab, in hello **Number of seconds without response before request is considered dropped** field, change hello default value from 3 tooa value between 30 and 60 seconds.</span></span>
7. <span data-ttu-id="42bec-267">在 hello**伺服器被識別為無法使用時，在要求之間的秒數**欄位中，變更 hello 預設值是 30 秒 tooa 值，這個值會等於 tooor 大於 hello hello 先前步驟中所指定的值。</span><span class="sxs-lookup"><span data-stu-id="42bec-267">In hello **Number of seconds between requests when server is identified as unavailable** field, change hello default value of 30 seconds tooa value that is equal tooor greater than hello value you specified in hello previous step.</span></span>

 ![編輯 Radius 伺服器](./media/nps-extension-remote-desktop-gateway/image14.png)

8.  <span data-ttu-id="42bec-269">按一下 [確定] 兩個時間 tooclose hello 對話方塊。</span><span class="sxs-lookup"><span data-stu-id="42bec-269">Click OK two times tooclose hello dialog boxes.</span></span>

### <a name="verify-connection-request-policies"></a><span data-ttu-id="42bec-270">驗證連線要求原則</span><span class="sxs-lookup"><span data-stu-id="42bec-270">Verify Connection Request Policies</span></span> 
<span data-ttu-id="42bec-271">根據預設，當您設定 hello RD 閘道 toouse 中央原則存放區的連線授權原則，hello RD 閘道是設定的 tooforward CAP 要求 toohello NPS 伺服器。</span><span class="sxs-lookup"><span data-stu-id="42bec-271">By default, when you configure hello RD Gateway toouse a central policy store for connection authorization policies, hello RD Gateway is configured tooforward CAP requests toohello NPS server.</span></span> <span data-ttu-id="42bec-272">hello Azure MFA 副檔名 hello NPS 伺服器安裝程序 hello RADIUS 存取要求。</span><span class="sxs-lookup"><span data-stu-id="42bec-272">hello NPS server with hello Azure MFA extension installed, processes hello RADIUS access request.</span></span> <span data-ttu-id="42bec-273">hello 下列步驟顯示如何 tooverify hello 預設連線要求原則。</span><span class="sxs-lookup"><span data-stu-id="42bec-273">hello following steps show you how tooverify hello default connection request policy.</span></span> 

1. <span data-ttu-id="42bec-274">在 hello RD 閘道在 hello NPS （本機） 主控台中，展開 **原則**，然後選取**連線要求原則**。</span><span class="sxs-lookup"><span data-stu-id="42bec-274">On hello RD Gateway, in hello NPS (Local) console, expand **Policies**, and select **Connection Request Policies**.</span></span>
2. <span data-ttu-id="42bec-275">以滑鼠右鍵按一下 [連線要求原則]，然後連按兩下 [TS GATEWAY AUTHORIZATION POLICY]。</span><span class="sxs-lookup"><span data-stu-id="42bec-275">Right-click **Connect Request Policies**, and double-click **TS GATEWAY AUTHORIZATION POLICY**.</span></span>
3. <span data-ttu-id="42bec-276">在 [hello **TS GATEWAY AUTHORIZATION POLICY 屬性**對話方塊方塊中，按一下 hello**設定**] 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="42bec-276">In hello **TS GATEWAY AUTHORIZATION POLICY properties** dialog box, click hello **Settings** tab.</span></span>
4. <span data-ttu-id="42bec-277">在 [設定] 索引標籤上，按一下 [轉送連線要求] 之下的 [驗證]。</span><span class="sxs-lookup"><span data-stu-id="42bec-277">On **Settings** tab, under Forwarding Connection Request, click **Authentication**.</span></span> <span data-ttu-id="42bec-278">RADIUS 用戶端可設定的 tooforward 要求驗證。</span><span class="sxs-lookup"><span data-stu-id="42bec-278">RADIUS client is configured tooforward requests for authentication.</span></span>

 ![驗證設定](./media/nps-extension-remote-desktop-gateway/image15.png)
 
5. <span data-ttu-id="42bec-280">按一下 [取消]。</span><span class="sxs-lookup"><span data-stu-id="42bec-280">Click **Cancel**.</span></span> 

## <a name="configure-nps-on-hello-server-where-hello-nps-extension-is-installed"></a><span data-ttu-id="42bec-281">Hello hello NPS 擴充功能安裝所在的伺服器上設定 NPS</span><span class="sxs-lookup"><span data-stu-id="42bec-281">Configure NPS on hello server where hello NPS extension is installed</span></span>
<span data-ttu-id="42bec-282">hello NPS 伺服器的 hello NPS 擴充功能安裝的需求 toobe 無法 tooexchange 具有 hello hello 遠端桌面閘道上的 NPS 伺服器的 RADIUS 訊息。</span><span class="sxs-lookup"><span data-stu-id="42bec-282">hello NPS server where hello NPS extension is installed needs toobe able tooexchange RADIUS messages with hello NPS server on hello Remote Desktop Gateway.</span></span> <span data-ttu-id="42bec-283">tooenable 此訊息交換，您需要 tooconfigure hello NPS 元件 hello hello NPS 擴充服務安裝所在的伺服器上。</span><span class="sxs-lookup"><span data-stu-id="42bec-283">tooenable this message exchange, you need tooconfigure hello NPS components on hello server where hello NPS extension service is installed.</span></span> 

### <a name="register-server-in-active-directory"></a><span data-ttu-id="42bec-284">在 Active Directory 中註冊伺服器</span><span class="sxs-lookup"><span data-stu-id="42bec-284">Register Server in Active Directory</span></span>
<span data-ttu-id="42bec-285">在此案例中正常運作的 toofunction，hello NPS 伺服器需要 toobe Active Directory 中登錄。</span><span class="sxs-lookup"><span data-stu-id="42bec-285">toofunction properly in this scenario, hello NPS server needs toobe registered in Active Directory.</span></span>

1. <span data-ttu-id="42bec-286">開啟 [伺服器管理員] 。</span><span class="sxs-lookup"><span data-stu-id="42bec-286">Open **Server Manager**.</span></span>
2. <span data-ttu-id="42bec-287">在 伺服器管理員 中按一下 工具，然後按一下網路原則伺服器。</span><span class="sxs-lookup"><span data-stu-id="42bec-287">In Server Manager, click **Tools**, and then click **Network Policy Server**.</span></span> 
3. <span data-ttu-id="42bec-288">在 hello 網路原則伺服器主控台中，以滑鼠右鍵按一下**NPS （本機）**，然後按一下 **Active Directory 中的註冊伺服器**。</span><span class="sxs-lookup"><span data-stu-id="42bec-288">In hello Network Policy Server console, right-click **NPS (Local)**, and then click **Register server in Active Directory**.</span></span> 
4. <span data-ttu-id="42bec-289">按 [確定] 兩次。</span><span class="sxs-lookup"><span data-stu-id="42bec-289">Click **OK** two times.</span></span>

 ![在 AD 中註冊伺服器](./media/nps-extension-remote-desktop-gateway/image16.png)

5. <span data-ttu-id="42bec-291">將 hello 主控台保持開啟以供 hello 下一個程序。</span><span class="sxs-lookup"><span data-stu-id="42bec-291">Leave hello console open for hello next procedure.</span></span>

### <a name="create-and-configure-radius-client"></a><span data-ttu-id="42bec-292">建立及設定 RADIUS 用戶端</span><span class="sxs-lookup"><span data-stu-id="42bec-292">Create and configure RADIUS client</span></span> 
<span data-ttu-id="42bec-293">hello 遠端桌面閘道需要 toobe 設定為 RADIUS 用戶端 toohello NPS 伺服器。</span><span class="sxs-lookup"><span data-stu-id="42bec-293">hello Remote Desktop Gateway needs toobe configured as a RADIUS client toohello NPS server.</span></span> 

1. <span data-ttu-id="42bec-294">Hello NPS 擴充功能已安裝在 hello hello NPS 伺服器上**NPS （本機）**主控台中，以滑鼠右鍵按一下**RADIUS 用戶端**按一下**新增**。</span><span class="sxs-lookup"><span data-stu-id="42bec-294">On hello NPS server where hello NPS extension is installed, in hello **NPS (Local)** console, right-click **RADIUS Clients** and click **New**.</span></span>

 ![新增 RADIUS 用戶端](./media/nps-extension-remote-desktop-gateway/image17.png)

2. <span data-ttu-id="42bec-296">在 hello**新的 RADIUS 用戶端**對話方塊方塊中，提供易記的名稱，例如_閘道_，和 hello IP 位址或 hello 遠端桌面閘道伺服器的 DNS 名稱。</span><span class="sxs-lookup"><span data-stu-id="42bec-296">In hello **New RADIUS client** dialog box, provide a friendly name, such as _Gateway_, and hello IP address or DNS name of hello Remote Desktop Gateway server.</span></span> 
3. <span data-ttu-id="42bec-297">在 hello**共用密碼**和 hello**確認共用的密碼**欄位中，輸入 hello 使用之前所用的相同密碼。</span><span class="sxs-lookup"><span data-stu-id="42bec-297">In hello **Shared secret** and hello **Confirm shared secret** fields, enter hello same secret that you used before.</span></span>

 ![名稱和位址](./media/nps-extension-remote-desktop-gateway/image18.png)

4. <span data-ttu-id="42bec-299">按一下**確定**tooclose hello 新的 RADIUS 用戶端 對話方塊。</span><span class="sxs-lookup"><span data-stu-id="42bec-299">Click **OK** tooclose hello New RADIUS client dialog box.</span></span>

### <a name="configure-network-policy"></a><span data-ttu-id="42bec-300">設定網路原則</span><span class="sxs-lookup"><span data-stu-id="42bec-300">Configure Network Policy</span></span>
<span data-ttu-id="42bec-301">回收 hello NPS 伺服器 hello Azure MFA 延伸模組是 hello 連線授權原則 (CAP) 的 hello 指定集中原則存放區。</span><span class="sxs-lookup"><span data-stu-id="42bec-301">Recall hello NPS server with hello Azure MFA extension is hello designated central policy store for hello Connection Authorization Policy (CAP).</span></span> <span data-ttu-id="42bec-302">因此，您需要 tooimplement 端點上 hello NPS 伺服器 tooauthorize 有效的連接要求。</span><span class="sxs-lookup"><span data-stu-id="42bec-302">Therefore, you need tooimplement a CAP on hello NPS server tooauthorize valid connections requests.</span></span>  

1. <span data-ttu-id="42bec-303">在 hello NPS （本機） 主控台中，展開**原則**，然後按一下**網路原則**。</span><span class="sxs-lookup"><span data-stu-id="42bec-303">In hello NPS (Local) console, expand **Policies**, and click **Network Policies**.</span></span>
2. <span data-ttu-id="42bec-304">以滑鼠右鍵按一下**連線 tooother 存取伺服器**，然後按一下**重複原則**。</span><span class="sxs-lookup"><span data-stu-id="42bec-304">Right-click **Connections tooother access servers**, and click **Duplicate policy**.</span></span> 

 ![複製原則](./media/nps-extension-remote-desktop-gateway/image19.png)

3. <span data-ttu-id="42bec-306">以滑鼠右鍵按一下**複本的連接 tooother 存取伺服器**，然後按一下**屬性**。</span><span class="sxs-lookup"><span data-stu-id="42bec-306">Right-click **Copy of Connections tooother access servers**, and click **Properties**.</span></span>

 ![網路屬性](./media/nps-extension-remote-desktop-gateway/image20.png)

4. <span data-ttu-id="42bec-308">在 hello**複本的連接 tooother 存取伺服器**對話方塊中，在 原則名稱，輸入適當的名稱，例如**RDG_CAP**。</span><span class="sxs-lookup"><span data-stu-id="42bec-308">In hello **Copy of Connections tooother access servers** dialog box, in Policy Name, enter a suitable name, such as **RDG_CAP**.</span></span> <span data-ttu-id="42bec-309">勾選 [啟用原則]，然後選取 [授與存取權]。</span><span class="sxs-lookup"><span data-stu-id="42bec-309">Check **Policy Enabled**, and select **Grant access**.</span></span> <span data-ttu-id="42bec-310">(選擇性) 在 [網路存取類型] 中選取 [遠端桌面閘道]，您也可以將它保留為 [未指定]。</span><span class="sxs-lookup"><span data-stu-id="42bec-310">Optionally, in Type of network access, select **Remote Desktop Gateway**, or you can leave it as **Unspecified**.</span></span>

 ![複製連線](./media/nps-extension-remote-desktop-gateway/image21.png)

5.  <span data-ttu-id="42bec-312">按一下 hello**條件約束**索引標籤，然後檢查**沒有交涉驗證方法仍然允許用戶端 tooconnect**。</span><span class="sxs-lookup"><span data-stu-id="42bec-312">Click hello **Constraints** tab, and check **Allow clients tooconnect without negotiating an authentication method**.</span></span>

 ![允許用戶端 tooconnect](./media/nps-extension-remote-desktop-gateway/image22.png)

6. <span data-ttu-id="42bec-314">（選擇性） 按一下 hello**條件**索引標籤和加入的 hello 連接 toobe 獲授權，例如，特定的 Windows 群組成員資格，必須符合的條件。</span><span class="sxs-lookup"><span data-stu-id="42bec-314">Optionally, click hello **Conditions** tab and add conditions that must be met for hello connection toobe authorized, for example, membership in a specific Windows group.</span></span>

 ![條件](./media/nps-extension-remote-desktop-gateway/image23.png)

7. <span data-ttu-id="42bec-316">按一下 [確定] 。</span><span class="sxs-lookup"><span data-stu-id="42bec-316">Click **OK**.</span></span> <span data-ttu-id="42bec-317">當提示的 tooview hello 對應的說明主題時，按一下 **否**。</span><span class="sxs-lookup"><span data-stu-id="42bec-317">When prompted tooview hello corresponding Help topic, click **No**.</span></span>
8. <span data-ttu-id="42bec-318">請確定您的新原則 hello hello 清單頂端，確定已啟用 hello 原則，而且它會授與存取權。</span><span class="sxs-lookup"><span data-stu-id="42bec-318">Ensure that your new policy is at hello top of hello list, that hello policy is enabled, and that it grants access.</span></span>

 ![網路原則](./media/nps-extension-remote-desktop-gateway/image24.png)

## <a name="verify-configuration"></a><span data-ttu-id="42bec-320">驗證組態</span><span class="sxs-lookup"><span data-stu-id="42bec-320">Verify configuration</span></span>
<span data-ttu-id="42bec-321">tooverify hello 組態，您需要 toolog hello 遠端桌面閘道上的都有適合的 RDP 用戶端。</span><span class="sxs-lookup"><span data-stu-id="42bec-321">tooverify hello configuration, you need toolog on hello Remote Desktop Gateway with a suitable RDP client.</span></span> <span data-ttu-id="42bec-322">是確定 toouse 允許由您的連線授權原則，且已啟用 Azure MFA 的帳戶。</span><span class="sxs-lookup"><span data-stu-id="42bec-322">Be sure toouse an account that is allowed by your Connection Authorization Policies and is enabled for Azure MFA.</span></span> 

<span data-ttu-id="42bec-323">Hello 圖所顯示，您可以使用 hello**遠端桌面 Web 存取**頁面。</span><span class="sxs-lookup"><span data-stu-id="42bec-323">As show in hello image below, you can use hello **Remote Desktop Web Access** page.</span></span>

![遠端桌面 Web 存取](./media/nps-extension-remote-desktop-gateway/image25.png)

<span data-ttu-id="42bec-325">在成功地輸入您的認證進行主要驗證，hello 遠端桌面連線 對話方塊會顯示起始遠端連線，狀態，如下所示。</span><span class="sxs-lookup"><span data-stu-id="42bec-325">Upon successfully entering your credentials for primary authentication, hello Remote Desktop Connect dialog box shows a status of Initiating remote connection, as shown below.</span></span> 

<span data-ttu-id="42bec-326">如果您已成功驗證與您先前設定 Azure MFA 的 hello 次要驗證方法時，您必須連接的 toohello 資源。</span><span class="sxs-lookup"><span data-stu-id="42bec-326">If you successfully authenticate with hello secondary authentication method you previously configured in Azure MFA, you are connected toohello resource.</span></span> <span data-ttu-id="42bec-327">不過，如果 hello 次要驗證不成功，則會被拒絕存取 tooresource。</span><span class="sxs-lookup"><span data-stu-id="42bec-327">However, if hello secondary authentication is not successful, you are denied access tooresource.</span></span> 

![起始遠端連線](./media/nps-extension-remote-desktop-gateway/image26.png)

<span data-ttu-id="42bec-329">在下方 hello 驗證器 hello 範例 Windows phone 上的應用程式會是使用的 tooprovide hello 次要驗證。</span><span class="sxs-lookup"><span data-stu-id="42bec-329">In hello example below, hello Authenticator app on a Windows phone is used tooprovide hello secondary authentication.</span></span>

![帳戶](./media/nps-extension-remote-desktop-gateway/image27.png)

<span data-ttu-id="42bec-331">已成功驗證使用 hello 次要驗證方法，一旦您已登入 hello 遠端桌面閘道，像平常一樣。</span><span class="sxs-lookup"><span data-stu-id="42bec-331">Once you have successfully authenticated using hello secondary authentication method, you are logged into hello Remote Desktop Gateway as normal.</span></span> <span data-ttu-id="42bec-332">不過，因為您不需要的 toouse 行動裝置應用程式使用信任的裝置上的次要驗證方法時，會更安全，否則會比 hello 登入程序。</span><span class="sxs-lookup"><span data-stu-id="42bec-332">However, because you are required toouse a secondary authentication method using a mobile app on a trusted device, hello log-in process is more secure than it would be otherwise.</span></span>

### <a name="view-event-viewer-logs-for-successful-logon-events"></a><span data-ttu-id="42bec-333">檢視事件檢視器記錄來找到成功的登入事件</span><span class="sxs-lookup"><span data-stu-id="42bec-333">View Event Viewer logs for successful logon events</span></span>
<span data-ttu-id="42bec-334">tooview hello 成功登入事件 hello Windows 事件檢視器記錄檔中的，您可以發出下列 Windows PowerShell 命令 tooquery hello Windows 終端機服務和 Windows 安全性記錄檔的 hello。</span><span class="sxs-lookup"><span data-stu-id="42bec-334">tooview hello successful sign-in events in hello Windows Event Viewer logs, you can issue hello following Windows PowerShell command tooquery hello Windows Terminal Services and Windows Security logs.</span></span>

<span data-ttu-id="42bec-335">tooquery 成功登入事件 hello 閘道操作記錄檔中的_(事件 Viewer\Applications 和服務 Logs\Microsoft\Windows\TerminalServices Gateway\Operational_，使用下列命令的 hello:</span><span class="sxs-lookup"><span data-stu-id="42bec-335">tooquery successful sign-in events in hello Gateway operational logs _(Event Viewer\Applications and Services Logs\Microsoft\Windows\TerminalServices-Gateway\Operational_, use hello following commands:</span></span>

* <span data-ttu-id="42bec-336">_Get-WinEvent -Logname Microsoft-Windows-TerminalServices-Gateway/Operational_ | where {$_.ID -eq '300'} | FL</span><span class="sxs-lookup"><span data-stu-id="42bec-336">_Get-WinEvent -Logname Microsoft-Windows-TerminalServices-Gateway/Operational_ | where {$_.ID -eq '300'} | FL</span></span> 
* <span data-ttu-id="42bec-337">此命令會顯示顯示 hello 使用者符合資源授權原則需求 (RD RAP)，並已授與存取的 Windows 事件。</span><span class="sxs-lookup"><span data-stu-id="42bec-337">This command displays Windows events that show hello user met resource authorization policy requirements (RD RAP) and was granted access.</span></span>

![檢視事件檢視器](./media/nps-extension-remote-desktop-gateway/image28.png)

* <span data-ttu-id="42bec-339">_Get-WinEvent -Logname Microsoft-Windows-TerminalServices-Gateway/Operational_ | where {$_.ID -eq '200'} | FL</span><span class="sxs-lookup"><span data-stu-id="42bec-339">_Get-WinEvent -Logname Microsoft-Windows-TerminalServices-Gateway/Operational_ | where {$_.ID -eq '200'} | FL</span></span>
* <span data-ttu-id="42bec-340">此命令會顯示 hello 使用者遇到連線授權原則的需求時顯示的事件。</span><span class="sxs-lookup"><span data-stu-id="42bec-340">This command displays hello events that show when user met connection authorization policy requirements.</span></span>

![連線授權](./media/nps-extension-remote-desktop-gateway/image29.png)

<span data-ttu-id="42bec-342">您也可以檢視此記錄並依據事件識別碼 (300 和 200) 進行篩選。</span><span class="sxs-lookup"><span data-stu-id="42bec-342">You can also view this log and filter on event IDs, 300 and 200.</span></span> <span data-ttu-id="42bec-343">hello 安全性事件檢視器記錄檔、 tooquery 成功登入事件都會使用下列命令的 hello:</span><span class="sxs-lookup"><span data-stu-id="42bec-343">tooquery successful logon events in hello Security event viewer logs, use hello following command:</span></span>

* <span data-ttu-id="42bec-344">_Get-WinEvent -Logname Security_ | where {$_.ID -eq '6272'} | FL</span><span class="sxs-lookup"><span data-stu-id="42bec-344">_Get-WinEvent -Logname Security_ | where {$_.ID -eq '6272'} | FL</span></span> 
* <span data-ttu-id="42bec-345">此命令可以執行在 hello 中央 NPS 或 hello RD 閘道伺服器。</span><span class="sxs-lookup"><span data-stu-id="42bec-345">This command can be run on either hello central NPS or hello RD Gateway Server.</span></span> 

![成功的登入事件](./media/nps-extension-remote-desktop-gateway/image30.png)

<span data-ttu-id="42bec-347">您也可以檢視 hello 安全性記錄檔或 hello 網路原則與存取服務自訂檢視，如下所示：</span><span class="sxs-lookup"><span data-stu-id="42bec-347">You can also view hello Security log or hello Network Policy and Access Services custom view, as shown below:</span></span>

![網路原則與存取服務](./media/nps-extension-remote-desktop-gateway/image31.png)

<span data-ttu-id="42bec-349">Hello 在伺服器上安裝 hello NPS 擴充 Azure MFA 的位置，您可以找到事件檢視器應用程式記錄檔特定 toohello 延伸在_應用程式和服務 Logs\Microsoft\AzureMfa_。</span><span class="sxs-lookup"><span data-stu-id="42bec-349">On hello server where you installed hello NPS extension for Azure MFA, you can find Event Viewer application logs specific toohello extension at _Application and Services Logs\Microsoft\AzureMfa_.</span></span> 

![事件檢視器應用程式記錄](./media/nps-extension-remote-desktop-gateway/image32.png)

## <a name="troubleshoot-guide"></a><span data-ttu-id="42bec-351">疑難排解指南</span><span class="sxs-lookup"><span data-stu-id="42bec-351">Troubleshoot Guide</span></span>

<span data-ttu-id="42bec-352">Hello 組態無法如預期般運作，如果第一個位置 toostart tootroubleshoot hello 是 hello 使用者的 tooverify 設定的 toouse Azure MFA。</span><span class="sxs-lookup"><span data-stu-id="42bec-352">If hello configuration is not working as expected, hello first place toostart tootroubleshoot is tooverify that hello user is configured toouse Azure MFA.</span></span> <span data-ttu-id="42bec-353">擁有 hello 使用者連接 toohello [Azure 入口網站](https://portal.azure.com)。</span><span class="sxs-lookup"><span data-stu-id="42bec-353">Have hello user connect toohello [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="42bec-354">如果使用者收到次要驗證提示而且可以成功地完成驗證，您就可以排除 Azure MFA 設定不正確的可能性。</span><span class="sxs-lookup"><span data-stu-id="42bec-354">If users are prompted for secondary verification and can successfully authenticate, you can eliminate an incorrect configuration of Azure MFA.</span></span>

<span data-ttu-id="42bec-355">如果為 hello 使用者正在 Azure MFA，您應該檢閱 hello 相關事件記錄檔。</span><span class="sxs-lookup"><span data-stu-id="42bec-355">If Azure MFA is working for hello user(s), you should review hello relevant Event logs.</span></span> <span data-ttu-id="42bec-356">這些包括 hello 前一節中討論的 hello 安全性事件、 操作、 閘道和 Azure MFA 記錄。</span><span class="sxs-lookup"><span data-stu-id="42bec-356">These include hello Security Event, Gateway operational, and Azure MFA logs that are discussed in hello previous section.</span></span> 

<span data-ttu-id="42bec-357">以下是安全性記錄的輸出範例，其中顯示了失敗登入事件 (事件識別碼 6273)。</span><span class="sxs-lookup"><span data-stu-id="42bec-357">Below is an example output of Security log showing a failed logon event (Event ID 6273).</span></span>

![失敗的登入事件](./media/nps-extension-remote-desktop-gateway/image33.png)

<span data-ttu-id="42bec-359">以下是從 hello AzureMFA 記錄檔的相關的事件：</span><span class="sxs-lookup"><span data-stu-id="42bec-359">Below is a related event from hello AzureMFA logs:</span></span>

![Azure MFA 記錄](./media/nps-extension-remote-desktop-gateway/image34.png)

<span data-ttu-id="42bec-361">tooperform 進階疑難排解選項，請洽詢 hello NPS 資料庫格式記錄檔安裝 hello NPS 服務。</span><span class="sxs-lookup"><span data-stu-id="42bec-361">tooperform advanced troubleshoot options, consult hello NPS database format log files where hello NPS service is installed.</span></span> <span data-ttu-id="42bec-362">這些記錄檔會建立於 %SystemRoot%\System32\Logs 資料夾，並以逗號分隔文字檔的形式存在。</span><span class="sxs-lookup"><span data-stu-id="42bec-362">These log files are created in _%SystemRoot%\System32\Logs_ folder as comma-delimited text files.</span></span> 

<span data-ttu-id="42bec-363">如需這些記錄檔的說明，請參閱[解譯 NPS 資料庫格式記錄檔](https://technet.microsoft.com/library/cc771748.aspx)。</span><span class="sxs-lookup"><span data-stu-id="42bec-363">For a description of these log files, see [Interpret NPS Database Format Log Files](https://technet.microsoft.com/library/cc771748.aspx).</span></span> <span data-ttu-id="42bec-364">這些記錄檔中的 hello 項目可以是很困難 toointerpret 而不匯入至試算表或資料庫。</span><span class="sxs-lookup"><span data-stu-id="42bec-364">hello entries in these log files can be difficult toointerpret without importing them into a spreadsheet or a database.</span></span> <span data-ttu-id="42bec-365">您可以找到數個 IAS 剖析器線上 tooassist 中解譯 hello 記錄檔。</span><span class="sxs-lookup"><span data-stu-id="42bec-365">You can find several IAS parsers online tooassist you in interpreting hello log files.</span></span> 

<span data-ttu-id="42bec-366">hello 下方影像顯示 hello 輸出的其中一個這類可下載[共享軟體應用程式](http://www.deepsoftware.com/iasviewer)。</span><span class="sxs-lookup"><span data-stu-id="42bec-366">hello image below shows hello output of one such downloadable [shareware application](http://www.deepsoftware.com/iasviewer).</span></span> 

![共享軟體應用程式](./media/nps-extension-remote-desktop-gateway/image35.png)

<span data-ttu-id="42bec-368">最後，如需其他疑難排解選項，您可以使用通訊協定分析器，例如 [Microsoft Message Analyzer](https://technet.microsoft.com/library/jj649776.aspx)。</span><span class="sxs-lookup"><span data-stu-id="42bec-368">Finally, for additional troubleshoot options, you can use a protocol analyzer, such [Microsoft Message Analyzer](https://technet.microsoft.com/library/jj649776.aspx).</span></span> 

<span data-ttu-id="42bec-369">hello 從 Microsoft Message Analyzer 下的圖顯示篩選包含 hello 使用者名稱的 RADIUS 通訊協定上的網路流量**Contoso\AliceC**。</span><span class="sxs-lookup"><span data-stu-id="42bec-369">hello image below from Microsoft Message Analyzer shows network traffic filtered on RADIUS protocol that contains hello user name **Contoso\AliceC**.</span></span>

![Microsoft Message Analyzer](./media/nps-extension-remote-desktop-gateway/image36.png)

## <a name="next-steps"></a><span data-ttu-id="42bec-371">後續步驟</span><span class="sxs-lookup"><span data-stu-id="42bec-371">Next steps</span></span>
[<span data-ttu-id="42bec-372">如何 tooget Azure 多重要素驗證</span><span class="sxs-lookup"><span data-stu-id="42bec-372">How tooget Azure Multi-Factor Authentication</span></span>](multi-factor-authentication-versions-plans.md)

[<span data-ttu-id="42bec-373">使用 RADIUS 的遠端桌面閘道和 Azure Multi-Factor Authentication Server</span><span class="sxs-lookup"><span data-stu-id="42bec-373">Remote Desktop Gateway and Azure Multi-Factor Authentication Server using RADIUS</span></span>](multi-factor-authentication-get-started-server-rdg.md)

[<span data-ttu-id="42bec-374">整合您的內部部署目錄與 Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="42bec-374">Integrate your on-premises directories with Azure Active Directory</span></span>](../active-directory/connect/active-directory-aadconnect.md)
