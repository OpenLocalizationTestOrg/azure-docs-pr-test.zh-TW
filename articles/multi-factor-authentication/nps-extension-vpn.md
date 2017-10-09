---
title: "使用 NPS 延伸模組的 Azure mfa aaaVPN 整合 |Microsoft 文件"
description: "這篇文章會討論與使用 Microsoft azure 的 hello 網路原則伺服器 (NPS) 延伸模組的 Azure MFA 整合您的 VPN 基礎結構。"
services: active-directory
keywords: "Azure MFA, 整合 VPN, Azure Active Directory, 網路原則伺服器擴充功能"
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
ms.openlocfilehash: 5e120f7633121385d9cc5d7bec97ecaa1ec7cf19
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="integrate-your-vpn-infrastructure-with-azure-multi-factor-authentication-mfa-using-hello-network-policy-server-nps-extension-for-azure"></a><span data-ttu-id="c676a-104">整合您的 VPN 基礎結構使用 Azure 的 hello 網路原則伺服器 (NPS) 擴充 Azure Multi-factor Authentication (MFA)</span><span class="sxs-lookup"><span data-stu-id="c676a-104">Integrate your VPN infrastructure with Azure Multi-Factor Authentication (MFA) using hello Network Policy Server (NPS) extension for Azure</span></span>

## <a name="overview"></a><span data-ttu-id="c676a-105">概觀</span><span class="sxs-lookup"><span data-stu-id="c676a-105">Overview</span></span>

<span data-ttu-id="c676a-106">hello azure 網路原則服務 」 (NPS) 延伸模組可讓組織使用 toosafeguard 遠端驗證撥號使用者服務 (RADIUS) 用戶端驗證雲端架構[Azure Multi-factor Authentication (MFA)](multi-factor-authentication-get-started-server-rdg.md)，提供兩步驟驗證。</span><span class="sxs-lookup"><span data-stu-id="c676a-106">hello Network Policy Service (NPS) extension for Azure allows organizations toosafeguard Remote Authentication Dial-In User Service (RADIUS) client authentication using cloud-based [Azure Multi-Factor Authentication (MFA)](multi-factor-authentication-get-started-server-rdg.md), which provides two-step verification.</span></span>

<span data-ttu-id="c676a-107">本文章提供使用 Azure MFA 整合 hello NPS 基礎結構的指示，使用 Azure tooenable 安全的雙步驟驗證使用者使用 VPN tooconnect tooyour 網路的 hello NPS 延伸模組。</span><span class="sxs-lookup"><span data-stu-id="c676a-107">This article provides instructions for integrating hello NPS infrastructure with Azure MFA using hello NPS extension for Azure tooenable secure two-step verification for users attempting tooconnect tooyour network using a VPN.</span></span> 

<span data-ttu-id="c676a-108">hello 網路原則與存取服務 」 (NPS) 可讓組織 hello 下列能力：</span><span class="sxs-lookup"><span data-stu-id="c676a-108">hello Network Policy and Access Services (NPS) gives organizations hello following abilities:</span></span>

* <span data-ttu-id="c676a-109">指定 hello 管理和控制的網路要求 toospecify 可以連線，每天何時允許連線，連線，hello 持續時間和安全性的用戶端必須使用 tooconnect，並依此類推 hello 層級的中央的位置。</span><span class="sxs-lookup"><span data-stu-id="c676a-109">Specify central locations for hello management and control of network requests toospecify who can connect, what times of day connections are allowed, hello duration of connections, and hello level of security that clients must use tooconnect, and so on.</span></span> <span data-ttu-id="c676a-110">組織不必在每個 VPN 或遠端桌面 (RD) 閘道伺服器上指定這些原則，而是在中央位置一次指定這些原則。</span><span class="sxs-lookup"><span data-stu-id="c676a-110">Rather than specify these policies on each VPN or Remote Desktop (RD) Gateway server, these policies can be specified once in a central location.</span></span> <span data-ttu-id="c676a-111">使用 RADIUS 通訊協定 hello tooprovide hello 集中式驗證、 授權以及帳戶處理 (AAA)。</span><span class="sxs-lookup"><span data-stu-id="c676a-111">hello RADIUS protocol is used tooprovide hello centralized Authentication, Authorization, and Accounting (AAA).</span></span> 
* <span data-ttu-id="c676a-112">建立並強制執行判斷裝置是否會授與不受限制或限制存取 toonetwork 資源的網路存取保護 (NAP) 用戶端健康原則。</span><span class="sxs-lookup"><span data-stu-id="c676a-112">Establish and enforce Network Access Protection (NAP) client health policies that determine whether devices are granted unrestricted or restricted access toonetwork resources.</span></span>
* <span data-ttu-id="c676a-113">提供表示 tooenforce 驗證和授權的存取 too802.1x 無線存取點及乙太網路交換器。</span><span class="sxs-lookup"><span data-stu-id="c676a-113">Provide a means tooenforce authentication and authorization for access too802.1x-capable wireless access points and Ethernet switches.</span></span>    

<span data-ttu-id="c676a-114">如需詳細資訊，請參閱[網路原則伺服器 (NPS)](https://docs.microsoft.com/windows-server/networking/technologies/nps/nps-top)。</span><span class="sxs-lookup"><span data-stu-id="c676a-114">For more information, see [Network Policy Server (NPS)](https://docs.microsoft.com/windows-server/networking/technologies/nps/nps-top).</span></span> 

<span data-ttu-id="c676a-115">tooenhance 安全性，並提供高層級的相容性，組織可以整合 NPS 使用使用者使用雙步驟驗證的 Azure MFA tooensure toobe 無法連線 toohello hello VPN 伺服器上的虛擬通訊埠。</span><span class="sxs-lookup"><span data-stu-id="c676a-115">tooenhance security and provide high level of compliance, organizations can integrate NPS with Azure MFA tooensure that users use two-step verification toobe able connect toohello virtual port on hello VPN server.</span></span> <span data-ttu-id="c676a-116">針對使用者 toobe 授與存取權，他們必須提供其使用者名稱/密碼組合與 hello 使用者的資訊有其控制項中。</span><span class="sxs-lookup"><span data-stu-id="c676a-116">For users toobe granted access, they must provide their username/password combination with information that hello user has in their control.</span></span> <span data-ttu-id="c676a-117">這項資訊必須能夠讓人信任且無法輕易複製，例如行動電話號碼、室內電話號碼、行動裝置上的應用程式等等。</span><span class="sxs-lookup"><span data-stu-id="c676a-117">This information must be trusted and not easily duplicated, such as a cell phone number, landline number, application on a mobile device, and so on.</span></span>

<span data-ttu-id="c676a-118">先前 toohello 可用性的 hello azure NPS 擴充功能，客戶必須承擔更多的 tooimplement 雙步驟驗證整合 NPS 和 Azure MFA 環境有 tooconfigure 和維護個別的 MFA 伺服器在 hello 與內部部署環境中遠端桌面閘道和使用 RADIUS 的 Azure Multi-factor Authentication Server 中所述。</span><span class="sxs-lookup"><span data-stu-id="c676a-118">Prior toohello availability of hello NPS extension for Azure, customers who wished tooimplement two-step verification for integrated NPS and Azure MFA environments had tooconfigure and maintain a separate MFA Server in hello on-premises environment as documented in Remote Desktop Gateway and Azure Multi-Factor Authentication Server using RADIUS.</span></span>

<span data-ttu-id="c676a-119">azure 的 hello NPS 擴充功能 hello 可用性現在可以讓組織 hello 選擇 toodeploy 在內部部署基礎 MFA 解決方案或以雲端為基礎 MFA 解決方案 toosecure RADIUS 用戶端驗證。</span><span class="sxs-lookup"><span data-stu-id="c676a-119">hello availability of hello NPS extension for Azure now gives organizations hello choice toodeploy either an on-premises based MFA solution or a cloud-based MFA solution toosecure RADIUS client authentication.</span></span>
 
## <a name="authentication-flow"></a><span data-ttu-id="c676a-120">驗證流程</span><span class="sxs-lookup"><span data-stu-id="c676a-120">Authentication Flow</span></span>
<span data-ttu-id="c676a-121">當使用者連接 tooa VPN 伺服器上的虛擬通訊埠時，它們必須先通過驗證使用不同的通訊協定，允許 hello 使用使用者名稱/密碼和憑證型驗證方法的組合。</span><span class="sxs-lookup"><span data-stu-id="c676a-121">When a user connects tooa virtual port on a VPN server, they must first authenticate using a variety of protocols, which allow hello use of a combination of user name/password and certificate-based authentication methods.</span></span> 

<span data-ttu-id="c676a-122">在加法 tooauthenticating 與驗證身分識別，使用者必須擁有適當的撥入權限的 hello。</span><span class="sxs-lookup"><span data-stu-id="c676a-122">In addition tooauthenticating and verifying identity, users must have hello appropriate dial-in permissions.</span></span> <span data-ttu-id="c676a-123">在簡單的實作中，直接在 hello Active Directory 使用者物件上設定這些電話撥入權限，以允許存取。</span><span class="sxs-lookup"><span data-stu-id="c676a-123">In simple implementations, these dial-in permissions that allow access are set directly on hello Active Directory user objects.</span></span> 

 ![使用者屬性](./media/nps-extension-vpn/image1.png)

<span data-ttu-id="c676a-125">在簡單的實作中，每一部 VPN 伺服器都會根據每個本機 VPN 伺服器上所定義的原則來授與或拒絕存取權。</span><span class="sxs-lookup"><span data-stu-id="c676a-125">For simple implementations, each VPN server grants or denies access based on policies defined on each local VPN server.</span></span>

<span data-ttu-id="c676a-126">在較大且更靈活地實作 hello 原則該授與或拒絕 VPN 存取都集中在 RADIUS 伺服器上。</span><span class="sxs-lookup"><span data-stu-id="c676a-126">In larger and more scalable implementations, hello polices that grant or deny VPN access are centralized on RADIUS servers.</span></span> <span data-ttu-id="c676a-127">在此情況下，hello VPN 伺服器會做為存取伺服器 （RADIUS 用戶端），轉寄連線要求與帳戶訊息 tooa RADIUS 伺服器。</span><span class="sxs-lookup"><span data-stu-id="c676a-127">In this case, hello VPN server acts as an access server (RADIUS client) that forwards connection requests and account messages tooa RADIUS server.</span></span> <span data-ttu-id="c676a-128">tooconnect toohello 虛擬通訊埠 hello VPN 伺服器上的，使用者必須先通過驗證，並符合 hello RADIUS 伺服器上集中所定義的條件。</span><span class="sxs-lookup"><span data-stu-id="c676a-128">tooconnect toohello virtual port on hello VPN server, users must be authenticated and meet hello conditions defined centrally on RADIUS servers.</span></span> 

<span data-ttu-id="c676a-129">當以 hello NPS 整合 hello azure NPS 擴充功能時，hello 成功驗證流程如下所示：</span><span class="sxs-lookup"><span data-stu-id="c676a-129">When hello NPS extension for Azure is integrated with hello NPS, hello successful authentication flow is as follows:</span></span>

1. <span data-ttu-id="c676a-130">hello VPN 伺服器接收包含 hello 使用者名稱和密碼 tooconnect tooa 資源，例如遠端桌面工作階段的 VPN 使用者的驗證要求。</span><span class="sxs-lookup"><span data-stu-id="c676a-130">hello VPN server receives an authentication request from a VPN user that includes hello username and password tooconnect tooa resource, such as a Remote Desktop session.</span></span> 
2. <span data-ttu-id="c676a-131">做為 RADIUS 用戶端時，VPN 伺服器轉換 hello 要求 tooa RADIUS Access-request 訊息，並傳送 hello 訊息 （加密密碼） hello NPS 擴充功能安裝所在的 toohello RADIUS (NPS) 伺服器。</span><span class="sxs-lookup"><span data-stu-id="c676a-131">Acting as a RADIUS client, VPN server converts hello request tooa RADIUS Access-Request message and sends hello message (password is encrypted) toohello RADIUS (NPS) server where hello NPS extension is installed.</span></span> 
3. <span data-ttu-id="c676a-132">hello 使用者名稱和密碼組合中 Active Directory 驗證。</span><span class="sxs-lookup"><span data-stu-id="c676a-132">hello username and password combination is verified in Active Directory.</span></span> <span data-ttu-id="c676a-133">如果 hello 使用者名稱 / 密碼不正確、 hello RADIUS 伺服器會傳送 Access-reject 訊息。</span><span class="sxs-lookup"><span data-stu-id="c676a-133">If hello username / password is incorrect, hello RADIUS Server sends an Access-Reject message.</span></span> 
4. <span data-ttu-id="c676a-134">如果在指定的所有條件為 hello NPS 連線要求，並符合網路原則 (例如，時間一天或群組的成員資格的限制)，hello NPS 擴充觸發程序使用 Azure MFA 的次要驗證的要求。</span><span class="sxs-lookup"><span data-stu-id="c676a-134">If all conditions as specified in hello NPS Connection Request and Network Policies are met (for example, time of day or group membership restrictions), hello NPS extension triggers a request for secondary authentication with Azure MFA.</span></span> 
5. <span data-ttu-id="c676a-135">Azure MFA 與 Azure Active Directory 通訊、 擷取 hello 使用者詳細資料，然後執行 hello 次要驗證使用 hello hello 使用者 （簡訊、 行動裝置應用程式，等等） 所設定的方法。</span><span class="sxs-lookup"><span data-stu-id="c676a-135">Azure MFA communicates with Azure Active Directory, retrieves hello user’s details, and performs hello secondary authentication using hello method configured by hello user (text message, mobile app, and so on).</span></span> 
6. <span data-ttu-id="c676a-136">成功時的 hello MFA 挑戰，Azure MFA 通訊 hello 結果 toohello NPS 擴充功能。</span><span class="sxs-lookup"><span data-stu-id="c676a-136">Upon success of hello MFA challenge, Azure MFA communicates hello result toohello NPS extension.</span></span>
7. <span data-ttu-id="c676a-137">Hello 連線嘗試會同時驗證和授權之後，hello 擴充功能安裝所在的 hello NPS 伺服器會傳送 RADIUS Access-accept 訊息 toohello VPN 伺服器 （RADIUS 用戶端）。</span><span class="sxs-lookup"><span data-stu-id="c676a-137">After hello connection attempt is both authenticated and authorized, hello NPS server where hello extension is installed sends a RADIUS Access-Accept message toohello VPN server (RADIUS client).</span></span>
8. <span data-ttu-id="c676a-138">hello 使用者已獲得存取 toohello 虛擬通訊埠 VPN 伺服器上的，建立加密的 VPN 通道。</span><span class="sxs-lookup"><span data-stu-id="c676a-138">hello user is granted access toohello virtual port on VPN server and establishes an encrypted VPN tunnel.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c676a-139">必要條件</span><span class="sxs-lookup"><span data-stu-id="c676a-139">Prerequisites</span></span>
<span data-ttu-id="c676a-140">本節詳述 hello hello 遠端桌面閘道與整合 Azure MFA 之前所需的必要條件。</span><span class="sxs-lookup"><span data-stu-id="c676a-140">This section details hello prerequisites necessary before integrating Azure MFA with hello Remote Desktop Gateway.</span></span> <span data-ttu-id="c676a-141">在開始之前，您必須擁有下列先決條件備妥的 hello。</span><span class="sxs-lookup"><span data-stu-id="c676a-141">Before you begin, you must have hello following prerequisites in place.</span></span>

* <span data-ttu-id="c676a-142">VPN 基礎結構</span><span class="sxs-lookup"><span data-stu-id="c676a-142">VPN infrastructure</span></span>
* <span data-ttu-id="c676a-143">網路原則與存取服務 (NPS) 角色</span><span class="sxs-lookup"><span data-stu-id="c676a-143">Network Policy and Access Services (NPS) role</span></span>
* <span data-ttu-id="c676a-144">Azure MFA 授權</span><span class="sxs-lookup"><span data-stu-id="c676a-144">Azure MFA License</span></span>
* <span data-ttu-id="c676a-145">Windows Server 軟體</span><span class="sxs-lookup"><span data-stu-id="c676a-145">Windows Server software</span></span>
* <span data-ttu-id="c676a-146">程式庫</span><span class="sxs-lookup"><span data-stu-id="c676a-146">Libraries</span></span>
* <span data-ttu-id="c676a-147">與內部部署 AD 同步的 Azure AD</span><span class="sxs-lookup"><span data-stu-id="c676a-147">Azure AD synched with on-premises AD</span></span> 
* <span data-ttu-id="c676a-148">Azure Active Directory GUID 識別碼</span><span class="sxs-lookup"><span data-stu-id="c676a-148">Azure Active Directory GUID ID</span></span>

### <a name="vpn-infrastructure"></a><span data-ttu-id="c676a-149">VPN 基礎結構</span><span class="sxs-lookup"><span data-stu-id="c676a-149">VPN infrastructure</span></span>
<span data-ttu-id="c676a-150">本文假設您有使用 Microsoft Windows Server 2016 就地工作 VPN 基礎結構，而且該 hello VPN 伺服器不目前是設定的 tooforward 連線要求 tooa RADIUS 伺服器。</span><span class="sxs-lookup"><span data-stu-id="c676a-150">This article assumes that you have a working VPN infrastructure using Microsoft Windows Server 2016 in place and that hello VPN server is currently not configured tooforward connection requests tooa RADIUS server.</span></span> <span data-ttu-id="c676a-151">本指南中，您將設定 hello VPN 基礎結構 toouse 中央的 RADIUS 伺服器。</span><span class="sxs-lookup"><span data-stu-id="c676a-151">You will configure hello VPN infrastructure toouse a central RADIUS server in this guide.</span></span>

<span data-ttu-id="c676a-152">如果您沒有就地工作基礎結構，您可以快速建立這個基礎結構提供許多您可以找到 hello Microsoft 和協力廠商站台的 VPN 安裝教學課程中的下列 hello 指導方針。</span><span class="sxs-lookup"><span data-stu-id="c676a-152">If you do not have a working infrastructure in place, you can quickly create this infrastructure by following hello guidance provided in numerous VPN setup tutorials you can find on hello Microsoft and third-party sites.</span></span> 

### <a name="network-policy-and-access-services-nps-role"></a><span data-ttu-id="c676a-153">網路原則與存取服務 (NPS) 角色</span><span class="sxs-lookup"><span data-stu-id="c676a-153">Network Policy and Access Services (NPS) role</span></span>

<span data-ttu-id="c676a-154">hello NPS 角色服務提供 hello RADIUS 伺服器和用戶端功能。</span><span class="sxs-lookup"><span data-stu-id="c676a-154">hello NPS role service provides hello RADIUS server and client functionality.</span></span> <span data-ttu-id="c676a-155">本文假設您已在成員伺服器或網域控制站上安裝 hello NPS 角色，您的環境中。</span><span class="sxs-lookup"><span data-stu-id="c676a-155">This article assumes you have installed hello NPS role on a member server or domain controller in your environment.</span></span> <span data-ttu-id="c676a-156">在本指南中，您要設定 RADIUS 以進行 VPN 設定。</span><span class="sxs-lookup"><span data-stu-id="c676a-156">You will configure RADIUS for a VPN configuration in this guide.</span></span> <span data-ttu-id="c676a-157">在伺服器上安裝 hello NPS 角色_其他_比您的 VPN 伺服器。</span><span class="sxs-lookup"><span data-stu-id="c676a-157">Install hello NPS role on a server _other_ than your VPN server.</span></span>

<span data-ttu-id="c676a-158">如需有關安裝 hello NPS 角色服務的 Windows Server 2012 或更高版本，請參閱[安裝 NAP 健康原則伺服器](https://technet.microsoft.com/library/dd296890.aspx)。</span><span class="sxs-lookup"><span data-stu-id="c676a-158">For information on installing hello NPS role service Windows Server 2012 or higher, see [Install a NAP Health Policy Server](https://technet.microsoft.com/library/dd296890.aspx).</span></span> <span data-ttu-id="c676a-159">Windows Server 2016 已淘汰網路存取原則 (NAP)。</span><span class="sxs-lookup"><span data-stu-id="c676a-159">Network Access Policy (NAP) is deprecated in Windows Server 2016.</span></span> <span data-ttu-id="c676a-160">如需 NPS，網域控制站上的包括 hello 建議 tooinstall NPS 的最佳作法的說明，請參閱[NPS 的最佳作法](https://technet.microsoft.com/library/cc771746)。</span><span class="sxs-lookup"><span data-stu-id="c676a-160">For a description of best practices for NPS, including hello recommendation tooinstall NPS on a domain controller, see [Best Practices for NPS](https://technet.microsoft.com/library/cc771746).</span></span>

### <a name="licenses"></a><span data-ttu-id="c676a-161">授權</span><span class="sxs-lookup"><span data-stu-id="c676a-161">Licenses</span></span>

<span data-ttu-id="c676a-162">需要 Azure MFA 的授權，此授權可透過 Azure AD Premium、Enterprise Mobility plus Security (EMS) 或 MFA 訂用帳戶來獲得。</span><span class="sxs-lookup"><span data-stu-id="c676a-162">Required is a license for Azure MFA, which is available through an Azure AD Premium, Enterprise Mobility plus Security (EMS), or an MFA subscription.</span></span> <span data-ttu-id="c676a-163">如需詳細資訊，請參閱[如何 tooget Azure Multi-factor Authentication](multi-factor-authentication-versions-plans.md)。</span><span class="sxs-lookup"><span data-stu-id="c676a-163">For more information, see [How tooget Azure Multi-Factor Authentication](multi-factor-authentication-versions-plans.md).</span></span> <span data-ttu-id="c676a-164">若要進行測試，您可以使用試用版訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="c676a-164">For testing purposes, you can use a trial subscription.</span></span>

### <a name="software"></a><span data-ttu-id="c676a-165">軟體</span><span class="sxs-lookup"><span data-stu-id="c676a-165">Software</span></span>

<span data-ttu-id="c676a-166">hello NPS 擴充功能需要 Windows Server 2008 R2 SP1 或更新版本已安裝的 hello NPS 角色服務。</span><span class="sxs-lookup"><span data-stu-id="c676a-166">hello NPS extension requires Windows Server 2008 R2 SP1 or above with hello NPS role service installed.</span></span> <span data-ttu-id="c676a-167">使用 Windows Server 2016 中未執行本指南中的所有 hello 步驟。</span><span class="sxs-lookup"><span data-stu-id="c676a-167">All hello steps in this guide were performed using Windows Server 2016.</span></span>

### <a name="libraries"></a><span data-ttu-id="c676a-168">程式庫</span><span class="sxs-lookup"><span data-stu-id="c676a-168">Libraries</span></span>

<span data-ttu-id="c676a-169">下列兩個程式庫的 hello 是必要的：</span><span class="sxs-lookup"><span data-stu-id="c676a-169">hello following two libraries are required:</span></span>

* [<span data-ttu-id="c676a-170">適用於 Visual Studio 2013 的 Visual C++ 可轉散發套件 (X64)</span><span class="sxs-lookup"><span data-stu-id="c676a-170">Visual C++ Redistributable Packages for Visual Studio 2013 (X64)</span></span>](https://www.microsoft.com/download/details.aspx?id=40784)
* <span data-ttu-id="c676a-171">適用於 Windows PowerShell 1.1.166.0 版或更新版本的 Microsoft Azure Active Directory 模組。</span><span class="sxs-lookup"><span data-stu-id="c676a-171">_Microsoft Azure Active Directory Module for Windows PowerShell version 1.1.166.0_ or higher.</span></span> <span data-ttu-id="c676a-172">Hello 最新版本和安裝指示，請參閱[Microsoft Azure Active Directory PowerShell 模組版本發行歷程記錄](https://social.technet.microsoft.com/wiki/contents/articles/28552.microsoft-azure-active-directory-powershell-module-version-release-history.aspx)。</span><span class="sxs-lookup"><span data-stu-id="c676a-172">For hello latest release and installation instructions, see [Microsoft Azure Active Directory PowerShell Module Version Release History](https://social.technet.microsoft.com/wiki/contents/articles/28552.microsoft-azure-active-directory-powershell-module-version-release-history.aspx).</span></span>

<span data-ttu-id="c676a-173">這些程式庫不會封裝與 hello NPS 擴充功能安裝程式檔案 （版本 0.9.1.2），儘管現有文件集，否則為表示。</span><span class="sxs-lookup"><span data-stu-id="c676a-173">These libraries are not packaged with hello NPS extension setup files (version 0.9.1.2), despite existing documentation that states otherwise.</span></span> <span data-ttu-id="c676a-174">最少，您必須安裝 Visual Studio 2013 hello Visual c + + 可轉散發套件。</span><span class="sxs-lookup"><span data-stu-id="c676a-174">At a minimum, you must install hello Visual C++ Redistributable Packages for Visual Studio 2013.</span></span> <span data-ttu-id="c676a-175">如果尚不存在，透過您 hello 安裝程序的一部分執行組態指令碼，會安裝 hello Microsoft Azure Active Directory 的 Windows PowerShell 模組。</span><span class="sxs-lookup"><span data-stu-id="c676a-175">hello Microsoft Azure Active Directory Module for Windows PowerShell is installed, if it is not already present, through a configuration script you run as part of hello setup process.</span></span> <span data-ttu-id="c676a-176">沒有任何需要 tooinstall 事先本單元如果尚未安裝。</span><span class="sxs-lookup"><span data-stu-id="c676a-176">There is no need tooinstall this module ahead of time if it is not already installed.</span></span>

### <a name="azure-active-directory-synched-with-on-premises-active-directory"></a><span data-ttu-id="c676a-177">與內部部署 Active Directory 同步的 Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="c676a-177">Azure Active Directory synched with on-premises Active Directory</span></span> 

<span data-ttu-id="c676a-178">toouse hello NPS 擴充內部部署使用者必須向 Azure Active Directory 同步處理，並啟用 Multi-factor authentication。</span><span class="sxs-lookup"><span data-stu-id="c676a-178">toouse hello NPS extension, on-premises users must be synced with Azure Active Directory and enabled for Multi-Factor Authentication.</span></span> <span data-ttu-id="c676a-179">本指南假設內部部署使用者已使用 AD Connect 來與 Azure Active Directory 保持同步。</span><span class="sxs-lookup"><span data-stu-id="c676a-179">This guide assumes that on-premises users are synched with Azure Active Directory using AD Connect.</span></span> <span data-ttu-id="c676a-180">下面會提供為使用者啟用 MFA 的指示。</span><span class="sxs-lookup"><span data-stu-id="c676a-180">Instructions for enabling users for MFA are provided below.</span></span>
<span data-ttu-id="c676a-181">如需 Azure AD Connect 的相關資訊，請參閱[整合您的內部部署目錄與 Azure Active Directory](../active-directory/connect/active-directory-aadconnect.md)。</span><span class="sxs-lookup"><span data-stu-id="c676a-181">For information on Azure AD connect, see [Integrate your on-premises directories with Azure Active Directory](../active-directory/connect/active-directory-aadconnect.md).</span></span> 

### <a name="azure-active-directory-guid-id"></a><span data-ttu-id="c676a-182">Azure Active Directory GUID 識別碼</span><span class="sxs-lookup"><span data-stu-id="c676a-182">Azure Active Directory GUID ID</span></span> 
<span data-ttu-id="c676a-183">tooinstall hello NPS，您需要 tooknow hello hello Azure Active Directory 的 GUID。</span><span class="sxs-lookup"><span data-stu-id="c676a-183">tooinstall hello NPS, you need tooknow hello GUID of hello Azure Active Directory.</span></span> <span data-ttu-id="c676a-184">Hello 下一節中提供的指示尋找 hello hello Azure Active Directory 的 GUID。</span><span class="sxs-lookup"><span data-stu-id="c676a-184">Instructions for finding hello GUID of hello Azure Active Directory are provided in hello next section.</span></span>

## <a name="configure-radius-for-vpn-connections"></a><span data-ttu-id="c676a-185">設定 RADIUS 的 VPN 連線</span><span class="sxs-lookup"><span data-stu-id="c676a-185">Configure RADIUS for VPN connections</span></span>

<span data-ttu-id="c676a-186">如果您已經安裝 hello NPS 伺服器角色的成員伺服器上，您會需要 tooconfigure tooauthenticate 並授權要求 VPN 連線的 VPN 用戶端。</span><span class="sxs-lookup"><span data-stu-id="c676a-186">If you have installed hello NPS server role on a member server, you need tooconfigure tooauthenticate and authorize VPN client that request VPN connections.</span></span> 

<span data-ttu-id="c676a-187">本節假設您已經安裝 hello 網路原則伺服器角色，但不是設定它使用基礎結構中。</span><span class="sxs-lookup"><span data-stu-id="c676a-187">This section assumes that you have installed hello Network Policy Server role but have not configured it for use in your infrastructure.</span></span>

>[!NOTE]
><span data-ttu-id="c676a-188">如果您已擁有運作中的 VPN 伺服器，且使用集中式的 RADIUS 伺服器來進行驗證，則可以略過本節。</span><span class="sxs-lookup"><span data-stu-id="c676a-188">If you already have a working VPN server that uses a centralized RADIUS server for authentication, you can skip this section.</span></span>
>

### <a name="register-server-in-active-directory"></a><span data-ttu-id="c676a-189">在 Active Directory 中註冊伺服器</span><span class="sxs-lookup"><span data-stu-id="c676a-189">Register Server in Active Directory</span></span>
<span data-ttu-id="c676a-190">在此案例中正常運作的 toofunction，hello NPS 伺服器需要 toobe Active Directory 中登錄。</span><span class="sxs-lookup"><span data-stu-id="c676a-190">toofunction properly in this scenario, hello NPS server needs toobe registered in Active Directory.</span></span>

1. <span data-ttu-id="c676a-191">開啟 [伺服器管理員]。</span><span class="sxs-lookup"><span data-stu-id="c676a-191">Open Server Manager.</span></span>
2. <span data-ttu-id="c676a-192">在 伺服器管理員 中按一下 工具，然後按一下網路原則伺服器。</span><span class="sxs-lookup"><span data-stu-id="c676a-192">In Server Manager, click **Tools**, and then click **Network Policy Server**.</span></span> 
3. <span data-ttu-id="c676a-193">在 hello 網路原則伺服器主控台中，以滑鼠右鍵按一下**NPS （本機）**，然後按一下 **Active Directory 中的註冊伺服器**。</span><span class="sxs-lookup"><span data-stu-id="c676a-193">In hello Network Policy Server console, right-click **NPS (Local)**, and then click **Register server in Active Directory**.</span></span> <span data-ttu-id="c676a-194">按 [確定] 兩次。</span><span class="sxs-lookup"><span data-stu-id="c676a-194">Click **OK** two times.</span></span>

 ![網路原則伺服器](./media/nps-extension-vpn/image2.png)

4. <span data-ttu-id="c676a-196">將 hello 主控台保持開啟以供 hello 下一個程序。</span><span class="sxs-lookup"><span data-stu-id="c676a-196">Leave hello console open for hello next procedure.</span></span>

### <a name="use-wizard-tooconfigure-radius-server"></a><span data-ttu-id="c676a-197">使用精靈 tooconfigure RADIUS 伺服器</span><span class="sxs-lookup"><span data-stu-id="c676a-197">Use wizard tooconfigure RADIUS server</span></span>
<span data-ttu-id="c676a-198">您可以使用 （以精靈為基礎） 的標準或進階的組態選項 tooconfigure hello RADIUS 伺服器。</span><span class="sxs-lookup"><span data-stu-id="c676a-198">You can use a standard (wizard-based) or advanced configuration option tooconfigure hello RADIUS server.</span></span> <span data-ttu-id="c676a-199">本節假設 hello 使用 hello 精靈為基礎的標準組態選項。</span><span class="sxs-lookup"><span data-stu-id="c676a-199">This section assumes hello use of hello wizard-based standard configuration option.</span></span>

1. <span data-ttu-id="c676a-200">在 hello 網路原則伺服器主控台中，按一下  **NPS （本機）**。</span><span class="sxs-lookup"><span data-stu-id="c676a-200">In hello Network Policy Server console, click **NPS (Local)**.</span></span>
2. <span data-ttu-id="c676a-201">選取 標準設定 底下的 撥號或 VPN 連線的 RADIUS 伺服器，然後按一下設定 VPN 或撥號。</span><span class="sxs-lookup"><span data-stu-id="c676a-201">Under Standard Configuration, select **RADIUS Server for Dial-Up or VPN Connections**, and then click **Configure VPN or Dial-Up**.</span></span>

 ![設定 VPN](./media/nps-extension-vpn/image3.png)

3. <span data-ttu-id="c676a-203">在 hello 選取撥號或虛擬私人網路連線類型 頁面上，選取 **虛擬私人網路連線**，按一下**下一步**。</span><span class="sxs-lookup"><span data-stu-id="c676a-203">On hello Select Dial-up or Virtual Private Network Connections Type page, select **Virtual Private Network Connections**, and click **Next**.</span></span>

 ![虛擬私人網路](./media/nps-extension-vpn/image4.png)

4. <span data-ttu-id="c676a-205">在 hello 指定撥號或 VPN 伺服器頁面上，按一下 **新增**。</span><span class="sxs-lookup"><span data-stu-id="c676a-205">On hello Specify Dial-Up or VPN Server page, click **Add**.</span></span>
5. <span data-ttu-id="c676a-206">在 hello**新的 RADIUS 用戶端**對話方塊中，提供好記的名稱，輸入 hello 可解析名稱或 IP 位址 hello VPN 伺服器，並輸入共用密碼的密碼。</span><span class="sxs-lookup"><span data-stu-id="c676a-206">In hello **New RADIUS client** dialog box, provide a friendly name, enter hello resolvable name or IP address of hello VPN server, and enter a shared secret password.</span></span> <span data-ttu-id="c676a-207">請為此共用祕密使用較長且複雜的形式。</span><span class="sxs-lookup"><span data-stu-id="c676a-207">Make this shared secret password long and complex.</span></span> <span data-ttu-id="c676a-208">記錄此密碼，您需要 hello 下一節中的步驟。</span><span class="sxs-lookup"><span data-stu-id="c676a-208">Record this password, as you need it for steps in hello next section.</span></span>

 ![新增 RADIUS 用戶端](./media/nps-extension-vpn/image5.png)

6. <span data-ttu-id="c676a-210">按一下 [確定]，然後按 [下一步]。</span><span class="sxs-lookup"><span data-stu-id="c676a-210">Click **OK**, and then **Next**.</span></span>
7. <span data-ttu-id="c676a-211">在 hello**設定驗證方法**頁面上，接受 hello 預設選取項目 (Microsoft 加密驗證版本 2 (Ms-chapv2)，或選擇另一個選項，然後按一下 **下一步**。</span><span class="sxs-lookup"><span data-stu-id="c676a-211">On hello **Configure Authentication Methods** page, accept hello default selection (Microsoft Encrypted Authentication version 2 (MS-CHAPv2) or choose another option, and click **Next**.</span></span>

  >[!NOTE]
  ><span data-ttu-id="c676a-212">如果您設定可延伸的驗證通訊協定 (EAP)，則必須使用 MS CHAPv2 或 PEAP。</span><span class="sxs-lookup"><span data-stu-id="c676a-212">If you configure Extensible Authentication Protocol (EAP), you must use either MS CHAPv2 or PEAP.</span></span> <span data-ttu-id="c676a-213">其他 EAP 皆不受支援。</span><span class="sxs-lookup"><span data-stu-id="c676a-213">No other EAP is supported.</span></span>
 
8. <span data-ttu-id="c676a-214">在 hello 指定使用者群組 頁面上，按一下 **新增**和選取適當的群組，如果有的話。</span><span class="sxs-lookup"><span data-stu-id="c676a-214">On hello Specify User Groups page, click **Add** and select an appropriate group, if one exists.</span></span> <span data-ttu-id="c676a-215">否則，保留空白 toogrant 存取 tooall 使用者 hello 選取項目。</span><span class="sxs-lookup"><span data-stu-id="c676a-215">Otherwise, leave hello selection blank toogrant access tooall users.</span></span>

 ![指定使用者群組](./media/nps-extension-vpn/image7.png)

9. <span data-ttu-id="c676a-217">按一下 [下一步] 。</span><span class="sxs-lookup"><span data-stu-id="c676a-217">Click **Next**.</span></span>
10. <span data-ttu-id="c676a-218">在 hello 指定 IP 篩選器 頁面上，按一下 **下一步**。</span><span class="sxs-lookup"><span data-stu-id="c676a-218">On hello Specify IP Filters page, click **Next**.</span></span>
11. <span data-ttu-id="c676a-219">在 hello 指定加密設定 頁面上，接受 hello 預設設定，並按一下**下一步**。</span><span class="sxs-lookup"><span data-stu-id="c676a-219">On hello Specify Encryption Settings page, accept hello default settings, and click **Next**.</span></span>

 ![指定加密](./media/nps-extension-vpn/image8.png)

12. <span data-ttu-id="c676a-221">Hello 指定領域名稱，在 hello 名稱保留空白，接受 hello 預設設定，然後按一下**下一步**。</span><span class="sxs-lookup"><span data-stu-id="c676a-221">On hello Specify a Realm Name, leave hello name blank, accept hello default setting, and click **Next**.</span></span>

 ![指定領域名稱](./media/nps-extension-vpn/image9.png)

13. <span data-ttu-id="c676a-223">在 hello 完成新增撥號或虛擬私人網路連線和 RADIUS 用戶端頁面上，按一下 **完成**。</span><span class="sxs-lookup"><span data-stu-id="c676a-223">On hello Completing New Dial-up or Virtual Private Network Connections and RADIUS clients page, click **Finish**.</span></span>

 ![完成連線](./media/nps-extension-vpn/image10.png)

### <a name="verify-radius-configuration"></a><span data-ttu-id="c676a-225">確認 RADIUS 設定</span><span class="sxs-lookup"><span data-stu-id="c676a-225">Verify RADIUS configuration</span></span>
<span data-ttu-id="c676a-226">本節將詳細說明使用 hello 精靈所建立的 hello 組態。</span><span class="sxs-lookup"><span data-stu-id="c676a-226">This section details hello configuration you created using hello wizard.</span></span>

1. <span data-ttu-id="c676a-227">在 hello NPS 伺服器 hello NPS （本機） 主控台中，展開 RADIUS 用戶端，並選取**RADIUS 用戶端**。</span><span class="sxs-lookup"><span data-stu-id="c676a-227">On hello NPS server, in hello NPS (Local) console, expand RADIUS Clients, and select **RADIUS Clients**.</span></span>
2. <span data-ttu-id="c676a-228">在 hello 詳細資料窗格中，以滑鼠右鍵按一下您使用精靈，建立 hello RADIUS 用戶端，然後按一下**屬性**。</span><span class="sxs-lookup"><span data-stu-id="c676a-228">In hello details pane, right-click hello RADIUS client you created using wizard, and click **Properties**.</span></span> <span data-ttu-id="c676a-229">您的 RADIUS 用戶端 （hello VPN 伺服器） 的 hello 屬性應該類似 toothose 如下所示。</span><span class="sxs-lookup"><span data-stu-id="c676a-229">hello properties for your RADIUS client (hello VPN server) should be similar toothose shown below.</span></span>

 ![VPN 屬性](./media/nps-extension-vpn/image11.png)

3. <span data-ttu-id="c676a-231">按一下 [取消]。</span><span class="sxs-lookup"><span data-stu-id="c676a-231">Click **Cancel**.</span></span>
4. <span data-ttu-id="c676a-232">在 hello NPS 伺服器 hello NPS （本機） 主控台中，展開 **原則**，然後選取**連線要求原則**。</span><span class="sxs-lookup"><span data-stu-id="c676a-232">On hello NPS server, in hello NPS (Local) console, expand **Policies**, and select **Connection Request Policies**.</span></span> <span data-ttu-id="c676a-233">您應該會看到類似下面的 hello 影像的 hello VPN 連線原則。</span><span class="sxs-lookup"><span data-stu-id="c676a-233">You should see hello VPN Connections policy that resembles hello image below.</span></span>

 ![連線要求](./media/nps-extension-vpn/image12.png)

5. <span data-ttu-id="c676a-235">在 [原則] 底下選取 [網路原則]。</span><span class="sxs-lookup"><span data-stu-id="c676a-235">Under Policies, select **Network Policies**.</span></span> <span data-ttu-id="c676a-236">您應該類似下面的 hello 影像的虛擬私人網路 (VPN) 連線原則。</span><span class="sxs-lookup"><span data-stu-id="c676a-236">You should a Virtual Private Network (VPN) Connections policy that resembles hello image below.</span></span>

 ![網路屬性](./media/nps-extension-vpn/image13.png)

## <a name="configure-vpn-server-toouse-radius-authentication"></a><span data-ttu-id="c676a-238">設定 VPN 伺服器 toouse RADIUS 驗證</span><span class="sxs-lookup"><span data-stu-id="c676a-238">Configure VPN Server toouse RADIUS authentication</span></span>
<span data-ttu-id="c676a-239">在本節中，您可以設定 hello VPN 伺服器 toouse RADIUS 驗證。</span><span class="sxs-lookup"><span data-stu-id="c676a-239">In this section, you configure hello VPN server toouse RADIUS authentication.</span></span> <span data-ttu-id="c676a-240">本節假設您有工作中設定的 VPN 伺服器，但尚未設定 hello VPN 伺服器 toouse RADIUS 驗證。</span><span class="sxs-lookup"><span data-stu-id="c676a-240">This section assumes that you have a working configuration of VPN server but have not configured hello VPN server toouse RADIUS authentication.</span></span> <span data-ttu-id="c676a-241">設定後 hello VPN 伺服器，您可以確認您的組態如預期般。</span><span class="sxs-lookup"><span data-stu-id="c676a-241">After configuring hello VPN server, you confirm that your configuration is working as expected.</span></span>

>[!NOTE]
><span data-ttu-id="c676a-242">如果您已擁有運作中的 VPN 伺服器設定，且該設定使用 RADIUS 驗證，則可以略過本節。</span><span class="sxs-lookup"><span data-stu-id="c676a-242">If you already have a working VPN server configuration that uses RADIUS authentication, you can skip this section.</span></span>
>

### <a name="configure-authentication-provider"></a><span data-ttu-id="c676a-243">設定驗證提供者</span><span class="sxs-lookup"><span data-stu-id="c676a-243">Configure authentication provider</span></span>
1. <span data-ttu-id="c676a-244">在 hello VPN 伺服器上，開啟 [伺服器管理員]。</span><span class="sxs-lookup"><span data-stu-id="c676a-244">On hello VPN server, open Server Manager.</span></span>
2. <span data-ttu-id="c676a-245">在 [伺服器管理員] 中按一下 [工具]，然後按一下 [路由及遠端存取]。</span><span class="sxs-lookup"><span data-stu-id="c676a-245">In Server Manager, click **Tools**, and then **Routing and Remote Access**.</span></span>
3. <span data-ttu-id="c676a-246">在 hello 路由及遠端存取主控台中，以滑鼠右鍵按一下**\[伺服器名稱\]（本機）**，然後按一下**屬性**。</span><span class="sxs-lookup"><span data-stu-id="c676a-246">In hello Routing and Remote Access console, right-click **\[Server Name\] (local)**, and then click **Properties**.</span></span>

 ![路由及遠端存取](./media/nps-extension-vpn/image14.png)
 
4. <span data-ttu-id="c676a-248">在 hello **[伺服器名稱} （本機） 屬性**對話方塊方塊中，按一下 hello**安全性**] 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="c676a-248">In hello **[Server Name} (local) Properties** dialog box, click hello **Security** tab.</span></span> 
5. <span data-ttu-id="c676a-249">在 [hello**安全性**索引標籤的驗證提供者] 下按一下**RADIUS 驗證**，，然後**設定**。</span><span class="sxs-lookup"><span data-stu-id="c676a-249">On hello **Security** tab, under Authentication provider, click **RADIUS Authentication**, and then **Configure**.</span></span>

 ![RADIUS 驗證](./media/nps-extension-vpn/image15.png)
 
6. <span data-ttu-id="c676a-251">在 hello RADIUS 驗證 對話方塊中，按一下 **新增**。</span><span class="sxs-lookup"><span data-stu-id="c676a-251">In hello RADIUS Authentication dialog box, click **Add**.</span></span>
7. <span data-ttu-id="c676a-252">在 hello 新增 RADIUS 伺服器，在 伺服器名稱，並將您設定 hello 前一節中的 hello RADIUS 伺服器 hello 名稱或 hello IP 位址。</span><span class="sxs-lookup"><span data-stu-id="c676a-252">In hello Add RADIUS Server, in Server name, add hello name or hello IP address of hello RADIUS server you configured in hello previous section.</span></span>
8. <span data-ttu-id="c676a-253">在 共用密碼，按一下 **變更**和加入 hello 的共用密碼建立，並記錄先前的密碼。</span><span class="sxs-lookup"><span data-stu-id="c676a-253">In Shared secret, click **Change** and add hello shared secret password you created and recorded earlier.</span></span>
9. <span data-ttu-id="c676a-254">在 逾時 （秒），變更 hello tooa 值之間**30**和**60**。</span><span class="sxs-lookup"><span data-stu-id="c676a-254">In Time-out (seconds), change hello value tooa value between **30** and **60**.</span></span> <span data-ttu-id="c676a-255">這是必要的 tooallow toocomplete hello 第二個驗證因素足夠時間。</span><span class="sxs-lookup"><span data-stu-id="c676a-255">This is necessary tooallow enough time toocomplete hello second authentication factor.</span></span>
 
 ![新增 RADIUS 伺服器](./media/nps-extension-vpn/image16.png)
 
10. <span data-ttu-id="c676a-257">持續按 [確定]直到您徹底關閉所有對話方塊。</span><span class="sxs-lookup"><span data-stu-id="c676a-257">Click **OK** until you complete closing all dialog boxes.</span></span>

### <a name="test-vpn-connectivity"></a><span data-ttu-id="c676a-258">測試 VPN 連線能力</span><span class="sxs-lookup"><span data-stu-id="c676a-258">Test VPN connectivity</span></span>
<span data-ttu-id="c676a-259">在本節中，您會確認該 hello VPN 用戶端已驗證及授權 hello RADIUS 伺服器，當您嘗試 tooconnect tooVPN 虛擬通訊埠。</span><span class="sxs-lookup"><span data-stu-id="c676a-259">In this section, you confirm that hello VPN client is authenticated and authorized by hello RADIUS server when you attempt tooconnect tooVPN virtual port.</span></span> <span data-ttu-id="c676a-260">本節假設您使用 Windows 10 來作為 VPN 用戶端。</span><span class="sxs-lookup"><span data-stu-id="c676a-260">This section assumes you are using Windows 10 as a VPN client.</span></span> 

>[!NOTE]
><span data-ttu-id="c676a-261">如果您已設定 VPN 用戶端 tooconnect toohello VPN 伺服器，並已儲存的 hello 設定，您可以略過 hello 步驟相關的 tooconfiguring 並儲存 VPN 連線物件。</span><span class="sxs-lookup"><span data-stu-id="c676a-261">If you already configured a VPN client tooconnect toohello VPN server and have saved hello settings, you can skip hello steps related tooconfiguring and saving a VPN connection object.</span></span>
>

1. <span data-ttu-id="c676a-262">在 VPN 用戶端電腦上按一下 [啟動]，然後按一下 [設定] \(齒輪圖示)。</span><span class="sxs-lookup"><span data-stu-id="c676a-262">On your VPN client computer, click **Start**, and then **Settings** (gear icon).</span></span>
2. <span data-ttu-id="c676a-263">在 [視窗設定] 中按一下 [網路和網際網路]。</span><span class="sxs-lookup"><span data-stu-id="c676a-263">In Window Settings, click **Network & Internet**.</span></span>
3. <span data-ttu-id="c676a-264">按一下 [VPN]。</span><span class="sxs-lookup"><span data-stu-id="c676a-264">Click **VPN**.</span></span>
4. <span data-ttu-id="c676a-265">按一下 [新增 VPN 連線]。</span><span class="sxs-lookup"><span data-stu-id="c676a-265">Click **Add a VPN connection**.</span></span>
5. <span data-ttu-id="c676a-266">在新增 VPN 連線，因為 hello VPN 提供者，然後完成 hello 其餘欄位，視需要指定 Windows （內建），然後按一下**儲存**。</span><span class="sxs-lookup"><span data-stu-id="c676a-266">In Add a VPN connection, specify Windows (built-in) as hello VPN provider, then complete hello remaining fields, as appropriate, and click **Save**.</span></span> 

 ![新增 VPN 連線](./media/nps-extension-vpn/image17.png)
 
6. <span data-ttu-id="c676a-268">開啟 hello**網路和共用中心**控制台 中。</span><span class="sxs-lookup"><span data-stu-id="c676a-268">Open hello **Network and Sharing Center** in Control Panel.</span></span>
7. <span data-ttu-id="c676a-269">按一下 [變更介面卡設定]。</span><span class="sxs-lookup"><span data-stu-id="c676a-269">Click **Change adapter settings**.</span></span>

 ![變更介面卡設定](./media/nps-extension-vpn/image18.png)

8. <span data-ttu-id="c676a-271">以滑鼠右鍵按一下 hello VPN 網路連線，然後按一下屬性。</span><span class="sxs-lookup"><span data-stu-id="c676a-271">Right-click hello VPN network connection, and click Properties.</span></span> 

 ![VPN 網路屬性](./media/nps-extension-vpn/image19.png)

9. <span data-ttu-id="c676a-273">在 [hello VPN 內容] 對話方塊中，按一下 [hello**安全性**] 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="c676a-273">In hello VPN properties dialog box, click hello **Security** tab.</span></span> 
10. <span data-ttu-id="c676a-274">在 hello 安全性索引標籤上，確定只**Microsoft CHAP 版本 2 (MS-CHAP v2)**已選取，然後按一下 確定。</span><span class="sxs-lookup"><span data-stu-id="c676a-274">On hello Security tab, ensure that only **Microsoft CHAP Version 2 (MS-CHAP v2)** is selected, and click OK.</span></span>

 ![允許通訊協定](./media/nps-extension-vpn/image20.png)

11. <span data-ttu-id="c676a-276">以滑鼠右鍵按一下 hello VPN 連線，然後按一下**連接**。</span><span class="sxs-lookup"><span data-stu-id="c676a-276">Right-click hello VPN connection, and click **Connect**.</span></span>
12. <span data-ttu-id="c676a-277">在 hello 設定頁面上，按一下 **連接**。</span><span class="sxs-lookup"><span data-stu-id="c676a-277">On hello Settings page, click **Connect**.</span></span>

<span data-ttu-id="c676a-278">如下所示，成功的連線會出現在 hello 做為事件編號 6272，hello RADIUS 伺服器上的安全性記錄檔。</span><span class="sxs-lookup"><span data-stu-id="c676a-278">A successful connection appears in hello Security log on hello RADIUS server as Event ID 6272, as shown below.</span></span>

 ![事件屬性](./media/nps-extension-vpn/image21.png)

## <a name="troubleshoot-guide"></a><span data-ttu-id="c676a-280">疑難排解指南</span><span class="sxs-lookup"><span data-stu-id="c676a-280">Troubleshoot Guide</span></span>
<span data-ttu-id="c676a-281">假設已使用 VPN 設定，才能設定 hello VPN 伺服器 toouse 集中式的 RADIUS 伺服器進行驗證和授權。</span><span class="sxs-lookup"><span data-stu-id="c676a-281">Assume that your VPN configuration was working before you configured hello VPN server toouse a centralized RADIUS server for authentication and authorization.</span></span> <span data-ttu-id="c676a-282">在此情況下，很可能 hello 問題可能因組態 hello RADIUS 伺服器或 hello 使用的使用者名稱無效或密碼不正確。</span><span class="sxs-lookup"><span data-stu-id="c676a-282">In this case, it is likely that hello issue may be caused by a misconfiguration of hello RADIUS Server or hello use of an invalid username or password.</span></span> <span data-ttu-id="c676a-283">比方說，如果您在 hello 使用者名稱中使用 hello 替代的 UPN 尾碼，hello 登入嘗試可能會失敗 (您應該使用相同的帳戶名稱，為獲得最佳結果的 hello)。</span><span class="sxs-lookup"><span data-stu-id="c676a-283">For example, if you use hello alternate UPN suffix in hello username, hello login attempt might fail (you should use hello same Account name for best results).</span></span> 

<span data-ttu-id="c676a-284">這些問題，理想的位置 toostart 位於 tooexamine hello 安全性事件記錄檔的 tootroubleshoot hello RADIUS 伺服器。</span><span class="sxs-lookup"><span data-stu-id="c676a-284">tootroubleshoot these issues, an ideal place toostart is tooexamine hello Security event logs on hello RADIUS server.</span></span> <span data-ttu-id="c676a-285">toosave 時間搜尋事件，您可以使用 hello 以角色為基礎網路原則與存取伺服器自訂檢視在事件檢視器，如下所示。</span><span class="sxs-lookup"><span data-stu-id="c676a-285">toosave time searching for events, you can use hello role-based Network Policy and Access Server custom view in Event Viewer, as show below.</span></span> <span data-ttu-id="c676a-286">事件識別碼 6273 指出其中 hello 網路原則伺服器拒絕存取 tooa 使用者的事件。</span><span class="sxs-lookup"><span data-stu-id="c676a-286">Event ID 6273 indicates events where hello Network Policy Server denied access tooa user.</span></span> 

 ![事件檢視器](./media/nps-extension-vpn/image22.png)
 
## <a name="configure-multi-factor-authentication"></a><span data-ttu-id="c676a-288">設定 Multi-Factor Authentication</span><span class="sxs-lookup"><span data-stu-id="c676a-288">Configure Multi-Factor Authentication</span></span>
<span data-ttu-id="c676a-289">本節提供為使用者啟用 MFA 以及為帳戶設定雙步驟驗證的指示。</span><span class="sxs-lookup"><span data-stu-id="c676a-289">This section provides instructions for enabling users for MFA and for setting up accounts for two-step verification.</span></span> 

### <a name="enable-multi-factor-authentication"></a><span data-ttu-id="c676a-290">啟用 Multi-Factor Authentication</span><span class="sxs-lookup"><span data-stu-id="c676a-290">Enable multi-factor authentication</span></span>
<span data-ttu-id="c676a-291">在本節中，您將為 Azure AD 帳戶啟用 MFA。</span><span class="sxs-lookup"><span data-stu-id="c676a-291">In this section, you enable Azure AD accounts for MFA.</span></span> <span data-ttu-id="c676a-292">使用 hello**傳統入口網站**tooenable MFA 的使用者。</span><span class="sxs-lookup"><span data-stu-id="c676a-292">Use hello **classic portal** tooenable users for MFA.</span></span> 

1. <span data-ttu-id="c676a-293">開啟瀏覽器，並瀏覽過[https://manage.windowsazure.com](https://manage.windowsazure.com)。</span><span class="sxs-lookup"><span data-stu-id="c676a-293">Open a browser, and navigate too[https://manage.windowsazure.com](https://manage.windowsazure.com).</span></span> 
2. <span data-ttu-id="c676a-294">Hello 系統管理員身分登入。</span><span class="sxs-lookup"><span data-stu-id="c676a-294">Log on as hello administrator.</span></span>
3. <span data-ttu-id="c676a-295">在 hello 入口網站中 hello 左方導覽中，按一下**ACTIVE DIRECTORY**。</span><span class="sxs-lookup"><span data-stu-id="c676a-295">In hello portal, in hello left navigation, click **ACTIVE DIRECTORY**.</span></span>

 ![預設目錄](./media/nps-extension-vpn/image23.png)

4. <span data-ttu-id="c676a-297">在 hello NAME 欄位中，按一下 **預設目錄**（或另一個目錄，如果適當的話）。</span><span class="sxs-lookup"><span data-stu-id="c676a-297">In hello NAME column, click **Default Directory** (or another directory, if appropriate).</span></span>
5. <span data-ttu-id="c676a-298">在 hello 快速入門 頁面上，按一下 **設定**。</span><span class="sxs-lookup"><span data-stu-id="c676a-298">On hello Quick Start page, click **Configure**.</span></span>

 ![設定預設值](./media/nps-extension-vpn/image24.png)

6. <span data-ttu-id="c676a-300">在 hello 設定頁面上，向下捲動並在 hello 多因素驗證 區段中，按一下 **管理服務設定**。</span><span class="sxs-lookup"><span data-stu-id="c676a-300">On hello CONFIGURE page, scroll down and, in hello multi-factor authentication section, click **Manage service settings**.</span></span>

 ![管理 MFA 設定](./media/nps-extension-vpn/image25.png)
 
7. <span data-ttu-id="c676a-302">在 hello 多因素驗證頁面上，檢閱 hello 預設服務設定，然後再按一下**使用者**。</span><span class="sxs-lookup"><span data-stu-id="c676a-302">On hello multi-factor authentication page, review hello default service settings, and then click **Users**.</span></span> 

 ![MFA 使用者](./media/nps-extension-vpn/image26.png)
 
8. <span data-ttu-id="c676a-304">Hello 使用者在頁面上，選取您希望 tooenable MFA，然後按一下 hello 使用者**啟用**。</span><span class="sxs-lookup"><span data-stu-id="c676a-304">On hello Users page, select hello users that you wish tooenable for MFA, and then click **Enable**.</span></span>

 ![屬性](./media/nps-extension-vpn/image27.png)
 
9. <span data-ttu-id="c676a-306">出現提示時，按一下 [啟用多重要素驗證]。</span><span class="sxs-lookup"><span data-stu-id="c676a-306">When prompted, click **Enable multi-factor auth**.</span></span>

 ![啟用 MFA](./media/nps-extension-vpn/image28.png)
 
10. <span data-ttu-id="c676a-308">按一下 [關閉] 。</span><span class="sxs-lookup"><span data-stu-id="c676a-308">Click **Close**.</span></span> 
11. <span data-ttu-id="c676a-309">重新整理 hello 頁面。</span><span class="sxs-lookup"><span data-stu-id="c676a-309">Refresh hello page.</span></span> <span data-ttu-id="c676a-310">hello MFA 狀態是已變更的 tooEnabled。</span><span class="sxs-lookup"><span data-stu-id="c676a-310">hello MFA status is changed tooEnabled.</span></span>

<span data-ttu-id="c676a-311">如需詳細資訊 tooenable 使用者進行多重要素驗證，請參閱[開始使用 Azure Multi-factor Authentication hello 定域機組中](multi-factor-authentication-get-started-cloud.md)。</span><span class="sxs-lookup"><span data-stu-id="c676a-311">For information on how tooenable users for Multi-Factor Authentication, see [Getting started with Azure Multi-Factor Authentication in hello cloud](multi-factor-authentication-get-started-cloud.md).</span></span> 

### <a name="configure-accounts-for-two-step-verification"></a><span data-ttu-id="c676a-312">為帳戶設定雙步驟驗證</span><span class="sxs-lookup"><span data-stu-id="c676a-312">Configure accounts for two-step verification</span></span>
<span data-ttu-id="c676a-313">一旦帳戶已啟用 MFA，使用者不能 toosign 中 tooresources 由 hello MFA 原則，直到它們已經成功設定信任的裝置 toouse hello 在使用雙步驟驗證第二個驗證因素。</span><span class="sxs-lookup"><span data-stu-id="c676a-313">Once an account has been enabled for MFA, users are not able toosign in tooresources governed by hello MFA policy until they have successfully configured a trusted device toouse for hello second authentication factor having used two-step verification.</span></span>

<span data-ttu-id="c676a-314">在本節中，您要設定受信任的裝置以供雙步驟驗證使用。</span><span class="sxs-lookup"><span data-stu-id="c676a-314">In this section, you configure a trusted device for use with two-step verification.</span></span> <span data-ttu-id="c676a-315">有幾個選項供您 tooconfigure 這些包括 hello 下列：</span><span class="sxs-lookup"><span data-stu-id="c676a-315">There are several options available for you tooconfigure these, including hello following:</span></span>

* <span data-ttu-id="c676a-316">**行動裝置應用程式**。</span><span class="sxs-lookup"><span data-stu-id="c676a-316">**Mobile app**.</span></span> <span data-ttu-id="c676a-317">您在 Windows Phone、 Android 或 iOS 裝置上安裝 hello Microsoft 驗證器應用程式。</span><span class="sxs-lookup"><span data-stu-id="c676a-317">You install hello Microsoft Authenticator app on a Windows Phone, Android, or iOS device.</span></span> <span data-ttu-id="c676a-318">根據組織的原則，您會在兩種模式的其中一個必要的 toouse hello 應用程式： 接收通知的驗證 （將通知推送 tooyour 裝置），或使用的驗證碼 (需要 tooenter 驗證程式碼更新每隔 30 秒）。</span><span class="sxs-lookup"><span data-stu-id="c676a-318">Depending on your organization’s policies, you are required toouse hello app in one of two modes: Receive notifications for verifications (a notification is pushed tooyour device) or Use verification code (you are required tooenter a verification code that updates every 30 seconds).</span></span> 
* <span data-ttu-id="c676a-319">**行動電話通話或文字**。</span><span class="sxs-lookup"><span data-stu-id="c676a-319">**Mobile phone call or text**.</span></span> <span data-ttu-id="c676a-320">您會收到自動發出的來電或簡訊。</span><span class="sxs-lookup"><span data-stu-id="c676a-320">You can either receive an automated phone call or text message.</span></span> <span data-ttu-id="c676a-321">Hello 電話選項時，您可以回答 hello 呼叫，並按下 hello # 符號 tooauthenticate。</span><span class="sxs-lookup"><span data-stu-id="c676a-321">With hello phone call option, you answer hello call and press hello # sign tooauthenticate.</span></span> <span data-ttu-id="c676a-322">Hello 文字選項時，您可以回覆 toohello 文字訊息，或輸入 hello 登入介面的 hello 驗證碼。</span><span class="sxs-lookup"><span data-stu-id="c676a-322">With hello text option, you can either reply toohello text message or enter hello verification code into hello sign-in interface.</span></span>
* <span data-ttu-id="c676a-323">**辦公室電話通話**。</span><span class="sxs-lookup"><span data-stu-id="c676a-323">**Office phone call**.</span></span> <span data-ttu-id="c676a-324">此程序是 hello 與自動撥打電話上面所述相同。</span><span class="sxs-lookup"><span data-stu-id="c676a-324">This process is hello same as that described for automated phone calls above.</span></span>

<span data-ttu-id="c676a-325">遵循下列指示來設定裝置 toouse hello 行動裝置應用程式 tooreceive 推播通知進行驗證。</span><span class="sxs-lookup"><span data-stu-id="c676a-325">Follow these instructions for setting up a device toouse hello mobile app tooreceive push notification for verification.</span></span>

1. <span data-ttu-id="c676a-326">登入太[https://aka.ms/mfasetup](https://aka.ms/mfasetup)或任何站台，例如[https://portal.azure.com](https://portal.azure.com)，您必須有 tooauthenticate 使用啟用 MFA 的認證。</span><span class="sxs-lookup"><span data-stu-id="c676a-326">Log on too[https://aka.ms/mfasetup](https://aka.ms/mfasetup) or any site, such as [https://portal.azure.com](https://portal.azure.com), where you required tooauthenticate using your MFA-enabled credentials.</span></span> 
2. <span data-ttu-id="c676a-327">在登入您的使用者名稱和密碼，您會看到的畫面會提示您 tooset hello 進行額外安全性驗證的帳戶。</span><span class="sxs-lookup"><span data-stu-id="c676a-327">Upon signing in with your username and password, you are presented with a screen that prompts you tooset up hello account for additional security verification.</span></span>

 ![額外的安全性](./media/nps-extension-vpn/image29.png)

3. <span data-ttu-id="c676a-329">按一下 [立即設定]。</span><span class="sxs-lookup"><span data-stu-id="c676a-329">Click **Set it up now**.</span></span>
4. <span data-ttu-id="c676a-330">在 hello 其他安全性驗證] 頁面上，選取 [連絡人類型 （驗證電話、 辦公室電話或行動裝置應用程式）。</span><span class="sxs-lookup"><span data-stu-id="c676a-330">On hello Additional security verification page, select a contact type (authentication phone, office phone, or mobile app).</span></span> <span data-ttu-id="c676a-331">然後選取國家或地區並選取方法。</span><span class="sxs-lookup"><span data-stu-id="c676a-331">Then select a country or region, and select a method.</span></span> <span data-ttu-id="c676a-332">hello 方法會因您所選取的連絡人類型。</span><span class="sxs-lookup"><span data-stu-id="c676a-332">hello method varies by contact type you select.</span></span> <span data-ttu-id="c676a-333">例如，如果您選擇行動裝置應用程式，您可以選取是否驗證或驗證碼 toouse tooreceive 通知。</span><span class="sxs-lookup"><span data-stu-id="c676a-333">For example, if you choose Mobile app, you can select whether tooreceive notifications for verification or toouse a verification code.</span></span> <span data-ttu-id="c676a-334">hello 遵循的步驟假設您選擇**行動裝置應用程式**hello 以連絡人類型。</span><span class="sxs-lookup"><span data-stu-id="c676a-334">hello steps that follow assume you choose **Mobile app** as hello contact type.</span></span>

 ![電話驗證](./media/nps-extension-vpn/image30.png)

5. <span data-ttu-id="c676a-336">選取 [行動裝置應用程式]，按一下 [接收驗證通知]，然後按一下 [設定]。</span><span class="sxs-lookup"><span data-stu-id="c676a-336">Select Mobile app, click **Receive notifications for verification**, and then **Set up**.</span></span> 

 ![行動裝置應用程式驗證](./media/nps-extension-vpn/image31.png)
 
6. <span data-ttu-id="c676a-338">如果您尚未這樣做，請在裝置上安裝 hello authenticator 行動應用程式。</span><span class="sxs-lookup"><span data-stu-id="c676a-338">If you haven’t done so already, install hello authenticator mobile app on your device.</span></span> 
7. <span data-ttu-id="c676a-339">遵循 hello 行動裝置應用程式 tooscan hello 呈現列程式碼中的 hello 指示或手動輸入 hello 資訊，然後按一下**完成**。</span><span class="sxs-lookup"><span data-stu-id="c676a-339">Follow hello instructions in hello mobile app tooscan hello presented bar code or enter hello information manually, and then click **Done**.</span></span>

 ![設定行動裝置應用程式](./media/nps-extension-vpn/image32.png)

8. <span data-ttu-id="c676a-341">在 hello 其他安全性驗證 頁面上，按一下 **與我連絡**和回覆傳送 toonotification tooyour 裝置。</span><span class="sxs-lookup"><span data-stu-id="c676a-341">On hello Additional security verification page, click **Contact me** and reply toonotification sent tooyour device.</span></span>
9. <span data-ttu-id="c676a-342">在 hello 其他安全性驗證 頁面上，輸入萬一您遺失存取 toohello 行動裝置應用程式，然後按一下的連絡電話號碼**下一步**。</span><span class="sxs-lookup"><span data-stu-id="c676a-342">On hello Additional security verification page, enter a contact number in case you lose access toohello mobile app, and click **Next**.</span></span>

 ![行動電話號碼](./media/nps-extension-vpn/image33.png)
 
10. <span data-ttu-id="c676a-344">在 hello 其他安全性驗證，按一下 **完成**。</span><span class="sxs-lookup"><span data-stu-id="c676a-344">On hello Additional security verification, click **Done**.</span></span>

<span data-ttu-id="c676a-345">hello 的裝置已設定的 tooprovide 第二種驗證方法。</span><span class="sxs-lookup"><span data-stu-id="c676a-345">hello device is now configured tooprovide a second method of verification.</span></span> <span data-ttu-id="c676a-346">如需為帳戶設定雙步驟驗證的相關資訊，請參閱[對我的帳戶進行雙步驟驗證設定](./end-user/multi-factor-authentication-end-user-first-time.md)。</span><span class="sxs-lookup"><span data-stu-id="c676a-346">For information on setting up accounts for two-step verification, see [Set up my account for two-step verification](./end-user/multi-factor-authentication-end-user-first-time.md).</span></span>

## <a name="install-and-configure-nps-extension"></a><span data-ttu-id="c676a-347">安裝和設定 NPS 擴充功能</span><span class="sxs-lookup"><span data-stu-id="c676a-347">Install and configure NPS extension</span></span>

<span data-ttu-id="c676a-348">本節提供設定以 hello VPN 伺服器的用戶端驗證的 VPN toouse Azure MFA 的指示。</span><span class="sxs-lookup"><span data-stu-id="c676a-348">This section provides instructions for configuring VPN toouse Azure MFA for client authentication with hello VPN Server.</span></span>

<span data-ttu-id="c676a-349">一旦您安裝並設定 hello NPS 延伸模組，此伺服器所處理的所有 RADIUS 用戶端驗證都是必要的 toouse Azure MFA。</span><span class="sxs-lookup"><span data-stu-id="c676a-349">Once you install and configure hello NPS extension, all RADIUS-based client authentication that is processed by this server is required toouse Azure MFA.</span></span> <span data-ttu-id="c676a-350">若未在 Azure MFA 中註冊您的所有 VPN 使用者，您可以設定另一個 RADIUS 伺服器 tooauthenticate 不是使用者設定的 toouse MFA。</span><span class="sxs-lookup"><span data-stu-id="c676a-350">If not all your VPN users are enrolled in Azure MFA, you can set up another RADIUS server tooauthenticate users who are not configured toouse MFA.</span></span> <span data-ttu-id="c676a-351">或者，您可以建立登錄項目，第二個驗證因素，可讓挑戰使用者 tooprovide，才在 MFA 註冊。</span><span class="sxs-lookup"><span data-stu-id="c676a-351">Or you can create a registry entry that allows challenged users tooprovide a second authentication factor, only if they are enrolled in MFA.</span></span> 

<span data-ttu-id="c676a-352">建立新的字串值，名為_中 HKLM\SOFTWARE\Microsoft\AzureMfa REQUIRE_USER_MATCH_，並將設定 hello 值 tooTRUE 或 FALSE。</span><span class="sxs-lookup"><span data-stu-id="c676a-352">Create a new string value named _REQUIRE_USER_MATCH in HKLM\SOFTWARE\Microsoft\AzureMfa_, and set hello value tooTRUE or FALSE.</span></span> 

 ![需要使用者比對](./media/nps-extension-vpn/image34.png)
 
<span data-ttu-id="c676a-354">如果 hello 值組 tooTRUE 或未設定，所有驗證要求，都則主體 tooan MFA 挑戰。</span><span class="sxs-lookup"><span data-stu-id="c676a-354">If hello value is set tooTRUE or not set, all authentication requests are subject tooan MFA challenge.</span></span> <span data-ttu-id="c676a-355">為已註冊 MFA 的 toousers tooFALSE 設定 hello 值，如果發出 MFA 挑戰。</span><span class="sxs-lookup"><span data-stu-id="c676a-355">If hello value is set tooFALSE, MFA challenges are issued only toousers that are enrolled in MFA.</span></span> <span data-ttu-id="c676a-356">只使用 hello FALSE 設定在測試或實際執行環境中，在上架期間。</span><span class="sxs-lookup"><span data-stu-id="c676a-356">Only use hello FALSE setting in testing or in production environments during an onboarding period.</span></span>

### <a name="acquire-azure-active-directory-guid-id"></a><span data-ttu-id="c676a-357">取得 Azure Active Directory GUID 識別碼</span><span class="sxs-lookup"><span data-stu-id="c676a-357">Acquire Azure Active Directory GUID ID</span></span>

<span data-ttu-id="c676a-358">Hello NPS 擴充功能的 hello 組態的一部分，您需要 toosupply 系統管理員認證和 Azure Active Directory 識別碼 hello Azure AD 租用戶。</span><span class="sxs-lookup"><span data-stu-id="c676a-358">As part of hello configuration of hello NPS extension, you need toosupply admin credentials and hello Azure Active Directory ID for your Azure AD tenant.</span></span> <span data-ttu-id="c676a-359">hello 下列步驟顯示 tooget hello 租用戶的識別碼。</span><span class="sxs-lookup"><span data-stu-id="c676a-359">hello steps below show you how tooget hello tenant ID.</span></span>

1. <span data-ttu-id="c676a-360">登入 toohello 在 Azure 入口網站[https://portal.azure.com](https://portal.azure.com) hello Azure hello 全域管理員身分租用戶。</span><span class="sxs-lookup"><span data-stu-id="c676a-360">Sign in toohello Azure portal at [https://portal.azure.com](https://portal.azure.com) as hello global administrator of hello Azure tenant.</span></span>
2. <span data-ttu-id="c676a-361">在左瀏覽 hello，按一下 hello **Azure Active Directory**圖示。</span><span class="sxs-lookup"><span data-stu-id="c676a-361">In hello left navigation, click hello **Azure Active Directory** icon.</span></span>
3. <span data-ttu-id="c676a-362">按一下 [內容] 。</span><span class="sxs-lookup"><span data-stu-id="c676a-362">Click **Properties**.</span></span>
4. <span data-ttu-id="c676a-363">toocopy 您的目錄識別碼 toohello 剪貼簿、 選取 hello**複製**圖示。</span><span class="sxs-lookup"><span data-stu-id="c676a-363">toocopy your Directory ID toohello clipboard, select hello **Copy** icon.</span></span>
 
 ![目錄識別碼](./media/nps-extension-vpn/image35.png)

### <a name="install-hello-nps-extension"></a><span data-ttu-id="c676a-365">安裝 hello NPS 擴充功能</span><span class="sxs-lookup"><span data-stu-id="c676a-365">Install hello NPS extension</span></span>
<span data-ttu-id="c676a-366">hello NPS 擴充功能需要 toobe 具有 hello 網路原則伺服器上安裝和存取服務 」 (NPS) 角色安裝和該函式做 hello RADIUS 伺服器，在您的設計。</span><span class="sxs-lookup"><span data-stu-id="c676a-366">hello NPS extension needs toobe installed on a server that has hello Network Policy and Access Services (NPS) role installed and that functions as hello RADIUS server in your design.</span></span> <span data-ttu-id="c676a-367">請勿在您的遠端桌面伺服器上安裝 hello NPS 擴充功能。</span><span class="sxs-lookup"><span data-stu-id="c676a-367">Don't install hello NPS extension on your Remote Desktop Server.</span></span>

1. <span data-ttu-id="c676a-368">下載 hello NPS 擴充功能，從[https://aka.ms/npsmfa](https://aka.ms/npsmfa)。</span><span class="sxs-lookup"><span data-stu-id="c676a-368">Download hello NPS extension from [https://aka.ms/npsmfa](https://aka.ms/npsmfa).</span></span> 
2. <span data-ttu-id="c676a-369">將複製 hello 安裝程式可執行檔 (NpsExtnForAzureMfaInstaller.exe) toohello NPS 伺服器。</span><span class="sxs-lookup"><span data-stu-id="c676a-369">Copy hello setup executable file (NpsExtnForAzureMfaInstaller.exe) toohello NPS server.</span></span>
3. <span data-ttu-id="c676a-370">在 hello NPS 伺服器上，按兩下**NpsExtnForAzureMfaInstaller.exe**。</span><span class="sxs-lookup"><span data-stu-id="c676a-370">On hello NPS server, double-click **NpsExtnForAzureMfaInstaller.exe**.</span></span> <span data-ttu-id="c676a-371">出現提示時，按一下 [執行]。</span><span class="sxs-lookup"><span data-stu-id="c676a-371">If prompted, click **Run**.</span></span>
4. <span data-ttu-id="c676a-372">在 hello NPS 擴充功能的 Azure MFA 對話方塊中，檢閱 hello 軟體授權條款，請檢查**toohello 授權條款和條件，即表示我同意**，然後按一下**安裝**。</span><span class="sxs-lookup"><span data-stu-id="c676a-372">In hello NPS Extension for Azure MFA dialog box, review hello software license terms, check **I agree toohello license terms and conditions**, and click **Install**.</span></span>

 ![NPS 擴充功能](./media/nps-extension-vpn/image36.png)
 
5. <span data-ttu-id="c676a-374">在 hello NPS 擴充功能的 Azure MFA 對話方塊中，按一下 **關閉**。</span><span class="sxs-lookup"><span data-stu-id="c676a-374">In hello NPS Extension for Azure MFA dialog box, click **Close**.</span></span>  

 ![設定成功](./media/nps-extension-vpn/image37.png) 
 
### <a name="configure-certificates-for-use-with-hello-nps-extension-using-a-powershell-script"></a><span data-ttu-id="c676a-376">Hello NPS 擴充功能的 PowerShell 指令碼以設定使用的憑證</span><span class="sxs-lookup"><span data-stu-id="c676a-376">Configure certificates for use with hello NPS extension using a PowerShell script</span></span>
<span data-ttu-id="c676a-377">tooensure 安全通訊和保證，您需要 tooconfigure 憑證以供 hello NPS 延伸模組。</span><span class="sxs-lookup"><span data-stu-id="c676a-377">tooensure secure communications and assurance, you need tooconfigure certificates for use by hello NPS extension.</span></span> <span data-ttu-id="c676a-378">hello NPS 元件包括 Windows PowerShell 指令碼，以設定 nps 使用的自我簽署的憑證。</span><span class="sxs-lookup"><span data-stu-id="c676a-378">hello NPS components include a Windows PowerShell script that configures a self-signed certificate for use with NPS.</span></span> 

<span data-ttu-id="c676a-379">hello 指令碼會執行下列動作的 hello:</span><span class="sxs-lookup"><span data-stu-id="c676a-379">hello script performs hello following actions:</span></span>

* <span data-ttu-id="c676a-380">建立自我簽署憑證</span><span class="sxs-lookup"><span data-stu-id="c676a-380">Creates a self-signed certificate</span></span>
* <span data-ttu-id="c676a-381">將公開金鑰憑證 tooservice 上 Azure AD 主體產生關聯</span><span class="sxs-lookup"><span data-stu-id="c676a-381">Associates public key of certificate tooservice principal on Azure AD</span></span>
* <span data-ttu-id="c676a-382">存放區 hello hello 本機電腦存放區中的憑證</span><span class="sxs-lookup"><span data-stu-id="c676a-382">Stores hello cert in hello local machine store</span></span>
* <span data-ttu-id="c676a-383">授與存取 toohello 憑證的私用金鑰 toohello 網路使用者</span><span class="sxs-lookup"><span data-stu-id="c676a-383">Grants access toohello certificate’s private key toohello Network User</span></span>
* <span data-ttu-id="c676a-384">重新啟動網路原則伺服器服務</span><span class="sxs-lookup"><span data-stu-id="c676a-384">Restarts Network Policy Server service</span></span>

<span data-ttu-id="c676a-385">如果您想 toouse 您自己的憑證，您在 Azure AD 中，需要您憑證 toohello 服務主體的 tooassociate hello 公用等等。</span><span class="sxs-lookup"><span data-stu-id="c676a-385">If you want toouse your own certificates, you need tooassociate hello public of your certificate toohello service principle on Azure AD, and so on.</span></span>
<span data-ttu-id="c676a-386">toouse hello 指令碼提供與 Azure Active Directory 系統管理認證的 hello 副檔名和 hello 您之前複製的 Azure Active Directory 租用戶識別碼。</span><span class="sxs-lookup"><span data-stu-id="c676a-386">toouse hello script, provide hello extension with your Azure Active Directory administrative credentials and hello Azure Active Directory tenant ID you copied earlier.</span></span> <span data-ttu-id="c676a-387">您用來安裝 hello NPS 擴充每個 NPS 伺服器上執行 hello 指令碼。</span><span class="sxs-lookup"><span data-stu-id="c676a-387">Run hello script on each NPS server where you install hello NPS extension.</span></span>

1. <span data-ttu-id="c676a-388">開啟系統管理 Windows PowerShell 提示字元。</span><span class="sxs-lookup"><span data-stu-id="c676a-388">Open an administrative Windows PowerShell prompt.</span></span>
2. <span data-ttu-id="c676a-389">在 hello PowerShell 提示字元中輸入_cd 'c:\Program Files\Microsoft\AzureMfa\Config'_，按**ENTER**。</span><span class="sxs-lookup"><span data-stu-id="c676a-389">At hello PowerShell prompt, type _cd ‘c:\Program Files\Microsoft\AzureMfa\Config’_, and press **ENTER**.</span></span>
3. <span data-ttu-id="c676a-390">輸入 _.\AzureMfsNpsExtnConfigSetup.ps1_，然後按 **ENTER**。</span><span class="sxs-lookup"><span data-stu-id="c676a-390">Type _.\AzureMfsNpsExtnConfigSetup.ps1_, and press **ENTER**.</span></span> 
 * <span data-ttu-id="c676a-391">hello 指令碼會檢查 toosee hello Azure Active Directory PowerShell 模組安裝。</span><span class="sxs-lookup"><span data-stu-id="c676a-391">hello script checks toosee if hello Azure Active Directory PowerShell module is installed.</span></span> <span data-ttu-id="c676a-392">如果未安裝，hello 指令碼會安裝 hello 模組。</span><span class="sxs-lookup"><span data-stu-id="c676a-392">If it is not installed, hello script installs hello module for you.</span></span>
 
 ![PowerShell](./media/nps-extension-vpn/image38.png)
 
4. <span data-ttu-id="c676a-394">Hello 指令碼驗證的 hello PowerShell 模組的 hello 安裝之後，它會顯示 hello Azure Active Directory PowerShell 模組對話方塊。</span><span class="sxs-lookup"><span data-stu-id="c676a-394">After hello script verifies hello installation of hello PowerShell module, it displays hello Azure Active Directory PowerShell module dialog box.</span></span> <span data-ttu-id="c676a-395">在 [hello] 對話方塊中，輸入您的 Azure AD 系統管理員認證和密碼，然後按一下**登入**。</span><span class="sxs-lookup"><span data-stu-id="c676a-395">In hello dialog box, enter your Azure AD admin credentials and password, and click **Sign in**.</span></span> 
 
 ![PowerShell 登入](./media/nps-extension-vpn/image39.png)
 
5. <span data-ttu-id="c676a-397">出現提示時，貼上您先前複製 toohello 剪貼簿的 hello 租用戶識別碼，然後按**ENTER**。</span><span class="sxs-lookup"><span data-stu-id="c676a-397">When prompted, paste hello tenant ID you copied toohello clipboard earlier, and press **ENTER**.</span></span> 

 ![租用戶識別碼](./media/nps-extension-vpn/image40.png)

6. <span data-ttu-id="c676a-399">hello 指令碼會建立自我簽署的憑證，並執行其他組態變更。</span><span class="sxs-lookup"><span data-stu-id="c676a-399">hello script creates a self-signed certificate and performs other configuration changes.</span></span> <span data-ttu-id="c676a-400">hello 輸出就像是 hello 映像，如下所示。</span><span class="sxs-lookup"><span data-stu-id="c676a-400">hello output is like hello image shown below.</span></span>

 ![自我簽署憑證](./media/nps-extension-vpn/image41.png)

7. <span data-ttu-id="c676a-402">Hello 伺服器重新開機。</span><span class="sxs-lookup"><span data-stu-id="c676a-402">Reboot hello server.</span></span>
 
### <a name="verify-configuration"></a><span data-ttu-id="c676a-403">驗證組態</span><span class="sxs-lookup"><span data-stu-id="c676a-403">Verify configuration</span></span>
<span data-ttu-id="c676a-404">tooverify hello 組態中，您需要 tooestablish 與 VPN 伺服器的新 VPN 連線。</span><span class="sxs-lookup"><span data-stu-id="c676a-404">tooverify hello configuration, you need tooestablish a new VPN connection with VPN server.</span></span> <span data-ttu-id="c676a-405">在成功地輸入您的認證進行主要驗證，hello VPN 連線等候 hello 次要驗證 toosucceed 才建立 hello 連線時，如下所示。</span><span class="sxs-lookup"><span data-stu-id="c676a-405">Upon successfully entering your credentials for primary authentication, hello VPN connection waits for hello secondary authentication toosucceed before hello connection is established, as shown below.</span></span> 

 ![驗證設定](./media/nps-extension-vpn/image42.png)

<span data-ttu-id="c676a-407">如果您已成功驗證與您先前設定 Azure MFA 的 hello 次要驗證方法時，您必須連接的 toohello 資源。</span><span class="sxs-lookup"><span data-stu-id="c676a-407">If you successfully authenticate with hello secondary verification method you previously configured in Azure MFA, you are connected toohello resource.</span></span> <span data-ttu-id="c676a-408">不過，如果 hello 次要驗證不成功，則會被拒絕存取 tooresource。</span><span class="sxs-lookup"><span data-stu-id="c676a-408">However, if hello secondary authentication is not successful, you are denied access tooresource.</span></span> 

<span data-ttu-id="c676a-409">在下方 hello 驗證器 hello 範例 Windows phone 上的應用程式會是使用的 tooprovide hello 次要驗證。</span><span class="sxs-lookup"><span data-stu-id="c676a-409">In hello example below, hello Authenticator app on a Windows phone is used tooprovide hello secondary authentication.</span></span>

 ![驗證帳戶](./media/nps-extension-vpn/image43.png)

<span data-ttu-id="c676a-411">您已成功驗證之後使用 hello 第二種方法，會授與存取 toohello 虛擬通訊埠 hello VPN 伺服器上。</span><span class="sxs-lookup"><span data-stu-id="c676a-411">Once you have successfully authenticated using hello secondary method, you are granted access toohello virtual port on hello VPN server.</span></span> <span data-ttu-id="c676a-412">不過，因為您很有必要的 toouse 行動裝置應用程式使用信任的裝置上的次要驗證方法，程序中的 hello 記錄是更安全，它會使用使用者名稱 / 密碼組合。</span><span class="sxs-lookup"><span data-stu-id="c676a-412">However, because you were required toouse a secondary authentication method using a mobile app on a trusted device, hello log in process is more secure than it would be using only a username / password combination.</span></span>

### <a name="view-event-viewer-logs-for-successful-logon-events"></a><span data-ttu-id="c676a-413">檢視事件檢視器記錄來找到成功的登入事件</span><span class="sxs-lookup"><span data-stu-id="c676a-413">View Event Viewer logs for successful logon events</span></span>
<span data-ttu-id="c676a-414">tooview hello hello Windows 事件檢視器記錄檔中的成功登入事件，您可以發出下列 Windows PowerShell 命令 tooquery hello Windows 安全性記錄檔 hello NPS 伺服器上的 hello。</span><span class="sxs-lookup"><span data-stu-id="c676a-414">tooview hello successful logon events in hello Windows Event Viewer logs, you can issue hello following Windows PowerShell command tooquery hello Windows Security log on hello NPS server.</span></span>

<span data-ttu-id="c676a-415">hello 安全性事件檢視器記錄檔、 tooquery 成功登入事件都會使用下列命令 hello</span><span class="sxs-lookup"><span data-stu-id="c676a-415">tooquery successful logon events in hello Security event viewer logs, use hello following command,</span></span>
* <span data-ttu-id="c676a-416">_Get-WinEvent -Logname Security_ | where {$_.ID -eq '6272'} | FL</span><span class="sxs-lookup"><span data-stu-id="c676a-416">_Get-WinEvent -Logname Security_ | where {$_.ID -eq '6272'} | FL</span></span> 

 ![安全性事件檢視器](./media/nps-extension-vpn/image44.png)
 
<span data-ttu-id="c676a-418">您也可以檢視 hello 安全性記錄檔或 hello 網路原則與存取服務自訂檢視，如下所示：</span><span class="sxs-lookup"><span data-stu-id="c676a-418">You can also view hello Security log or hello Network Policy and Access Services custom view, as shown below:</span></span>

 ![網路原則存取](./media/nps-extension-vpn/image45.png)

<span data-ttu-id="c676a-420">Hello 在伺服器上安裝 hello NPS 擴充 Azure MFA 的位置，您可以找到事件檢視器應用程式記錄檔特定 toohello 延伸在**應用程式和服務 Logs\Microsoft\AzureMfa**。</span><span class="sxs-lookup"><span data-stu-id="c676a-420">On hello server where you installed hello NPS extension for Azure MFA, you can find Event Viewer application logs specific toohello extension at **Application and Services Logs\Microsoft\AzureMfa**.</span></span> 

* <span data-ttu-id="c676a-421">_Get-WinEvent -Logname Security_ | where {$_.ID -eq '6272'} | FL</span><span class="sxs-lookup"><span data-stu-id="c676a-421">_Get-WinEvent -Logname Security_ | where {$_.ID -eq '6272'} | FL</span></span>

 ![事件數目](./media/nps-extension-vpn/image46.png)

## <a name="troubleshoot-guide"></a><span data-ttu-id="c676a-423">疑難排解指南</span><span class="sxs-lookup"><span data-stu-id="c676a-423">Troubleshoot Guide</span></span>
<span data-ttu-id="c676a-424">如果 hello 組態無法如預期般運作，很好的起點 toostart tootroubleshoot 是 hello 使用者的 tooverify 設定的 toouse Azure MFA。</span><span class="sxs-lookup"><span data-stu-id="c676a-424">If hello configuration is not working as expected, a good place toostart tootroubleshoot is tooverify that hello user is configured toouse Azure MFA.</span></span> <span data-ttu-id="c676a-425">擁有 hello 使用者連接太[https://portal.azure.com](https://portal.azure.com)。如果他們收到次要驗證提示而且可以成功地完成驗證，您就可以排除 Azure MFA 設定不正確的可能性。</span><span class="sxs-lookup"><span data-stu-id="c676a-425">Have hello user connect too[https://portal.azure.com](https://portal.azure.com). If they are prompted for secondary authentication and can successfully authenticate, you can eliminate an incorrect configuration of Azure MFA.</span></span>

<span data-ttu-id="c676a-426">如果為 hello 使用者正在 Azure MFA，您應該檢閱 hello 相關事件記錄檔。</span><span class="sxs-lookup"><span data-stu-id="c676a-426">If Azure MFA is working for hello user(s), you should review hello relevant Event logs.</span></span> <span data-ttu-id="c676a-427">這些包括 hello 前一節中討論的 hello 安全性事件、 操作、 閘道和 Azure MFA 記錄。</span><span class="sxs-lookup"><span data-stu-id="c676a-427">These include hello Security Event, Gateway operational, and Azure MFA logs that are discussed in hello previous section.</span></span> 

<span data-ttu-id="c676a-428">以下是安全性記錄的輸出範例，其中顯示了失敗登入事件 (事件識別碼 6273)：</span><span class="sxs-lookup"><span data-stu-id="c676a-428">Below is an example output of Security log showing a failed logon event (Event ID 6273):</span></span>

 ![安全性記錄](./media/nps-extension-vpn/image47.png)

<span data-ttu-id="c676a-430">以下是從 hello AzureMFA 記錄檔的相關的事件：</span><span class="sxs-lookup"><span data-stu-id="c676a-430">Below is a related event from hello AzureMFA logs:</span></span>

 ![Azure MFA 記錄](./media/nps-extension-vpn/image48.png)

<span data-ttu-id="c676a-432">tooperform 進階疑難排解選項，請洽詢 hello NPS 資料庫格式記錄檔安裝 hello NPS 服務。</span><span class="sxs-lookup"><span data-stu-id="c676a-432">tooperform advanced troubleshoot options, consult hello NPS database format log files where hello NPS service is installed.</span></span> <span data-ttu-id="c676a-433">這些記錄檔會建立於 %SystemRoot%\System32\Logs 資料夾，並以逗號分隔文字檔的形式存在。</span><span class="sxs-lookup"><span data-stu-id="c676a-433">These log files are created in _%SystemRoot%\System32\Logs_ folder as comma-delimited text files.</span></span> <span data-ttu-id="c676a-434">如需這些記錄檔的說明，請參閱[解譯 NPS 資料庫格式記錄檔](https://technet.microsoft.com/library/cc771748.aspx)。</span><span class="sxs-lookup"><span data-stu-id="c676a-434">For a description of these log files, see [Interpret NPS Database Format Log Files](https://technet.microsoft.com/library/cc771748.aspx).</span></span> 

<span data-ttu-id="c676a-435">這些記錄檔中的 hello 項目是很困難 toointerpret 而不匯入至試算表或資料庫。</span><span class="sxs-lookup"><span data-stu-id="c676a-435">hello entries in these log files are difficult toointerpret without importing them into a spreadsheet or a database.</span></span> <span data-ttu-id="c676a-436">您可以找到數字的 IAS 剖析器線上 tooassist 中解譯 hello 記錄檔。</span><span class="sxs-lookup"><span data-stu-id="c676a-436">You can find a number of IAS parsers online tooassist you in interpreting hello log files.</span></span> <span data-ttu-id="c676a-437">以下是 hello 輸出的其中一個這類可下載[共享軟體應用程式](http://www.deepsoftware.com/iasviewer):</span><span class="sxs-lookup"><span data-stu-id="c676a-437">Below is hello output of one such downloadable [shareware application](http://www.deepsoftware.com/iasviewer):</span></span> 

 ![共享軟體應用程式](./media/nps-extension-vpn/image49.png)

<span data-ttu-id="c676a-439">最後，如需其他疑難排解選項，您可以使用通訊協定分析器，例如 Wireshark 或 [Microsoft Message Analyzer](https://technet.microsoft.com/library/jj649776.aspx)。</span><span class="sxs-lookup"><span data-stu-id="c676a-439">Finally, for additional troubleshoot options, you can use a protocol analyzer such as Wireshark or [Microsoft Message Analyzer](https://technet.microsoft.com/library/jj649776.aspx).</span></span> <span data-ttu-id="c676a-440">hello Wireshark 從下列影像顯示 hello hello VPN 伺服器與 hello NPS 伺服器之間的 RADIUS 訊息。</span><span class="sxs-lookup"><span data-stu-id="c676a-440">hello following image from Wireshark shows hello RADIUS messages between hello VPN server and hello NPS server.</span></span>

 ![Microsoft Message Analyzer](./media/nps-extension-vpn/image50.png)

<span data-ttu-id="c676a-442">如需詳細資訊，請參閱[將現有的 NPS 基礎結構與 Azure Multi-Factor Authentication 整合](multi-factor-authentication-nps-extension.md)。</span><span class="sxs-lookup"><span data-stu-id="c676a-442">For more information, see [Integrate your existing NPS infrastructure with Azure Multi-Factor Authentication](multi-factor-authentication-nps-extension.md).</span></span>  

## <a name="next-steps"></a><span data-ttu-id="c676a-443">後續步驟</span><span class="sxs-lookup"><span data-stu-id="c676a-443">Next steps</span></span>
[<span data-ttu-id="c676a-444">如何 tooget Azure 多重要素驗證</span><span class="sxs-lookup"><span data-stu-id="c676a-444">How tooget Azure Multi-Factor Authentication</span></span>](multi-factor-authentication-versions-plans.md)

[<span data-ttu-id="c676a-445">使用 RADIUS 的遠端桌面閘道和 Azure Multi-Factor Authentication Server</span><span class="sxs-lookup"><span data-stu-id="c676a-445">Remote Desktop Gateway and Azure Multi-Factor Authentication Server using RADIUS</span></span>](multi-factor-authentication-get-started-server-rdg.md)

[<span data-ttu-id="c676a-446">整合您的內部部署目錄與 Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="c676a-446">Integrate your on-premises directories with Azure Active Directory</span></span>](../active-directory/connect/active-directory-aadconnect.md)

