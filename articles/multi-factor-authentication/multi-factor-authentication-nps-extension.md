---
title: "aaaUse 現有 NPS 伺服器 tooprovide Azure MFA 功能 |Microsoft 文件"
description: "hello Azure 多重要素驗證的網路原則伺服器延伸模組是簡單的解決方案 tooadd 以雲端為基礎的兩個步驟 vericiation 功能 tooyour 現有驗證基礎結構。"
services: multi-factor-authentication
documentationcenter: 
author: kgremban
manager: femila
ms.assetid: 
ms.service: multi-factor-authentication
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/14/2017
ms.author: kgremban
ms.reviewer: yossib
ms.custom: H1Hack27Feb2017; it-pro
ms.openlocfilehash: e9fc495b06873d45f06233f1aa618db9d94f8bd9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="integrate-your-existing-nps-infrastructure-with-azure-multi-factor-authentication"></a><span data-ttu-id="d9512-103">將現有的 NPS 基礎結構與 Azure Multi-Factor Authentication 整合</span><span class="sxs-lookup"><span data-stu-id="d9512-103">Integrate your existing NPS infrastructure with Azure Multi-Factor Authentication</span></span>

<span data-ttu-id="d9512-104">hello Azure MFA 的網路原則伺服器 (NPS) 擴充功能新增雲端式 MFA 功能 tooyour 驗證基礎結構使用您現有的伺服器。</span><span class="sxs-lookup"><span data-stu-id="d9512-104">hello Network Policy Server (NPS) extension for Azure MFA adds cloud-based MFA capabilities tooyour authentication infrastructure using your existing servers.</span></span> <span data-ttu-id="d9512-105">以 hello NPS 擴充功能，您可以加入通話、 簡訊或電話應用程式驗證 tooyour 現有的驗證流程，而不需要 tooinstall 設定及維護新的伺服器。</span><span class="sxs-lookup"><span data-stu-id="d9512-105">With hello NPS extension, you can add phone call, text message, or phone app verification tooyour existing authentication flow without having tooinstall, configure, and maintain new servers.</span></span> 

<span data-ttu-id="d9512-106">公司想 tooprotect VPN 連線，但不部署 hello Azure MFA Server 建立此延伸模組。</span><span class="sxs-lookup"><span data-stu-id="d9512-106">This extension was created for organizations that want tooprotect VPN connections without deploying hello Azure MFA Server.</span></span> <span data-ttu-id="d9512-107">hello NPS 擴充做為 RADIUS 和以雲端為基礎的 Azure MFA tooprovide 之間配接器的第二個因素，同盟或已同步使用者的驗證。</span><span class="sxs-lookup"><span data-stu-id="d9512-107">hello NPS extension acts as an adapter between RADIUS and cloud-based Azure MFA tooprovide a second factor of authentication for federated or synced users.</span></span>

<span data-ttu-id="d9512-108">使用 Azure MFA hello NPS 延伸模組時, hello 驗證流程包括下列元件的 hello:</span><span class="sxs-lookup"><span data-stu-id="d9512-108">When using hello NPS extension for Azure MFA, hello authentication flow includes hello following components:</span></span> 

1. <span data-ttu-id="d9512-109">**NAS/VPN 伺服器**來自 VPN 用戶端收到要求，並將它們轉換成要求 tooNPS 的 RADIUS 伺服器。</span><span class="sxs-lookup"><span data-stu-id="d9512-109">**NAS/VPN Server** receives requests from VPN clients and converts them into RADIUS requests tooNPS servers.</span></span> 
2. <span data-ttu-id="d9512-110">**NPS 伺服器**連接 tooActive 目錄 tooperform hello 的主要驗證 hello RADIUS 會要求，並成功時，會傳遞 hello 要求 tooany 安裝擴充功能。</span><span class="sxs-lookup"><span data-stu-id="d9512-110">**NPS Server** connects tooActive Directory tooperform hello primary authentication for hello RADIUS requests and, upon success, passes hello request tooany installed extensions.</span></span>  
3. <span data-ttu-id="d9512-111">**NPS 擴充**hello 次要驗證的要求 tooAzure MFA 觸發程序。</span><span class="sxs-lookup"><span data-stu-id="d9512-111">**NPS Extension** triggers a request tooAzure MFA for hello secondary authentication.</span></span> <span data-ttu-id="d9512-112">一旦 hello 延伸模組接收到 hello 回應和 hello MFA 挑戰成功，它會藉由提供包含 MFA 宣告，Azure STS 所發出的安全性權杖中的 hello NPS 伺服器完成 hello 驗證要求。</span><span class="sxs-lookup"><span data-stu-id="d9512-112">Once hello extension receives hello response, and if hello MFA challenge succeeds, it completes hello authentication request by providing hello NPS server with security tokens that include an MFA claim, issued by Azure STS.</span></span>  
4. <span data-ttu-id="d9512-113">**Azure MFA**進行通訊與 Azure Active Directory tooretrieve hello 使用者的詳細資訊，以及執行 hello 次要驗證使用的驗證方法設定 toohello 使用者。</span><span class="sxs-lookup"><span data-stu-id="d9512-113">**Azure MFA** communicates with Azure Active Directory tooretrieve hello user’s details and performs hello secondary authentication using a verification method configured toohello user.</span></span>

<span data-ttu-id="d9512-114">hello 下列圖表說明此高層級的驗證要求流程：</span><span class="sxs-lookup"><span data-stu-id="d9512-114">hello following diagram illustrates this high-level authentication request flow:</span></span> 

![驗證流程圖](./media/multi-factor-authentication-nps-extension/auth-flow.png)

## <a name="plan-your-deployment"></a><span data-ttu-id="d9512-116">規劃您的部署</span><span class="sxs-lookup"><span data-stu-id="d9512-116">Plan your deployment</span></span>

<span data-ttu-id="d9512-117">hello NPS 擴充功能會自動處理備援性，因此您不需要特殊的設定。</span><span class="sxs-lookup"><span data-stu-id="d9512-117">hello NPS extension automatically handles redundancy, so you don't need a special configuration.</span></span>

<span data-ttu-id="d9512-118">您可以視需要建立數量不拘且具有 Azure MFA 功能的 NPS 伺服器。</span><span class="sxs-lookup"><span data-stu-id="d9512-118">You can create as many Azure MFA-enabled NPS servers as you need.</span></span> <span data-ttu-id="d9512-119">如果您安裝多部伺服器，您應該為每部伺服器使用不同的用戶端憑證。</span><span class="sxs-lookup"><span data-stu-id="d9512-119">If you do install multiple servers, you should use a difference client certificate for each one of them.</span></span> <span data-ttu-id="d9512-120">建立每個伺服器的憑證，意味著您可以個別更新每個憑證，無須擔心所有的伺服器皆停機。</span><span class="sxs-lookup"><span data-stu-id="d9512-120">Creating a cert for each server means that you can update each cert individually, and not worry about downtime across all your servers.</span></span>

<span data-ttu-id="d9512-121">VPN 伺服器路由傳送驗證要求，因此需要 toobe 留意 hello 新的 Azure MFA 啟用 NPS 伺服器。</span><span class="sxs-lookup"><span data-stu-id="d9512-121">VPN servers route authentication requests, so they need toobe aware of hello new Azure MFA-enabled NPS servers.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d9512-122">必要條件</span><span class="sxs-lookup"><span data-stu-id="d9512-122">Prerequisites</span></span>

<span data-ttu-id="d9512-123">hello NPS 擴充功能的目的在於 toowork 與您現有的基礎結構。</span><span class="sxs-lookup"><span data-stu-id="d9512-123">hello NPS extension is meant toowork with your existing infrastructure.</span></span> <span data-ttu-id="d9512-124">請確定您擁有 hello 下列必要條件，才能開始。</span><span class="sxs-lookup"><span data-stu-id="d9512-124">Make sure you have hello following prerequisites before you begin.</span></span>

### <a name="licenses"></a><span data-ttu-id="d9512-125">授權</span><span class="sxs-lookup"><span data-stu-id="d9512-125">Licenses</span></span>

<span data-ttu-id="d9512-126">hello Azure MFA 的 NPS 延伸模組是與使用 toocustomers [Azure Multi-factor Authentication Server 的授權](multi-factor-authentication.md)（隨附於 Azure AD Premium、 EMS 或 MFA 訂閱）。</span><span class="sxs-lookup"><span data-stu-id="d9512-126">hello NPS Extension for Azure MFA is available toocustomers with [licenses for Azure Multi-Factor Authentication](multi-factor-authentication.md) (included with Azure AD Premium, EMS, or an MFA subscription).</span></span>

### <a name="software"></a><span data-ttu-id="d9512-127">軟體</span><span class="sxs-lookup"><span data-stu-id="d9512-127">Software</span></span>

<span data-ttu-id="d9512-128">Windows Server 2008 R2 SP1 或更新版本。</span><span class="sxs-lookup"><span data-stu-id="d9512-128">Windows Server 2008 R2 SP1 or above.</span></span>

### <a name="libraries"></a><span data-ttu-id="d9512-129">程式庫</span><span class="sxs-lookup"><span data-stu-id="d9512-129">Libraries</span></span>

<span data-ttu-id="d9512-130">這些程式庫會自動安裝 hello 副檔名。</span><span class="sxs-lookup"><span data-stu-id="d9512-130">These libraries are installed automatically with hello extension.</span></span>
-   [<span data-ttu-id="d9512-131">適用於 Visual Studio 2013 的 Visual C++ 可轉散發套件 (X64)</span><span class="sxs-lookup"><span data-stu-id="d9512-131">Visual C++ Redistributable Packages for Visual Studio 2013 (X64)</span></span>](https://www.microsoft.com/download/details.aspx?id=40784)
-   [<span data-ttu-id="d9512-132">適用於 Windows PowerShell 1.1.1660 版本的 Microsoft Azure Active Directory 模組</span><span class="sxs-lookup"><span data-stu-id="d9512-132">Microsoft Azure Active Directory Module for Windows PowerShell version 1.1.166.0</span></span>](https://connect.microsoft.com/site1164/Downloads/DownloadDetails.aspx?DownloadID=59185)

### <a name="azure-active-directory"></a><span data-ttu-id="d9512-133">Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="d9512-133">Azure Active Directory</span></span>

<span data-ttu-id="d9512-134">使用 hello NPS 延伸模組的每個人都必須是 Active Directory 的同步處理的 tooAzure 使用 Azure AD Connect，以及必須註冊 MFA。</span><span class="sxs-lookup"><span data-stu-id="d9512-134">Everyone using hello NPS extension must be synced tooAzure Active Directory using Azure AD Connect, and must be registered for MFA.</span></span>

<span data-ttu-id="d9512-135">當您安裝 hello 延伸模組時，您會需要 Azure AD 租用戶 hello 目錄識別碼和系統管理員認證。</span><span class="sxs-lookup"><span data-stu-id="d9512-135">When you install hello extension, you need hello directory ID and admin credentials for your Azure AD tenant.</span></span> <span data-ttu-id="d9512-136">您可以找到您目錄的識別碼在 hello [Azure 入口網站](https://portal.azure.com)。</span><span class="sxs-lookup"><span data-stu-id="d9512-136">You can find your directory ID in hello [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="d9512-137">身為管理員，選取 hello 登入**Azure Active Directory**圖示 hello 左邊，然後選取**屬性**。</span><span class="sxs-lookup"><span data-stu-id="d9512-137">Sign in as an administrator, select hello **Azure Active Directory** icon on hello left, then select **Properties**.</span></span> <span data-ttu-id="d9512-138">複製 hello GUID 在 hello**目錄識別碼**方塊，並將其儲存。</span><span class="sxs-lookup"><span data-stu-id="d9512-138">Copy hello GUID in hello **Directory ID** box and save it.</span></span> <span data-ttu-id="d9512-139">當您安裝 hello NPS 擴充功能時，您可以使用與 hello 租用戶識別碼的此 GUID。</span><span class="sxs-lookup"><span data-stu-id="d9512-139">You use this GUID as hello tenant ID when you install hello NPS extension.</span></span>

![在 Azure Active Directory 屬性下尋找您的目錄識別碼](./media/multi-factor-authentication-nps-extension/find-directory-id.png)

## <a name="prepare-your-environment"></a><span data-ttu-id="d9512-141">準備您的環境</span><span class="sxs-lookup"><span data-stu-id="d9512-141">Prepare your environment</span></span>

<span data-ttu-id="d9512-142">您安裝 hello NPS 擴充功能之前，您會想 tooprepare 您環境 toohandle hello 驗證流量。</span><span class="sxs-lookup"><span data-stu-id="d9512-142">Before you install hello NPS extension, you want tooprepare you environment toohandle hello authentication traffic.</span></span>

### <a name="enable-hello-nps-role-on-a-domain-joined-server"></a><span data-ttu-id="d9512-143">啟用 hello 已加入網域的伺服器上的 NPS 角色</span><span class="sxs-lookup"><span data-stu-id="d9512-143">Enable hello NPS role on a domain-joined server</span></span>

<span data-ttu-id="d9512-144">hello NPS 伺服器連接 tooAzure Active Directory，並驗證 hello MFA 要求。</span><span class="sxs-lookup"><span data-stu-id="d9512-144">hello NPS server connects tooAzure Active Directory and authenticates hello MFA requests.</span></span> <span data-ttu-id="d9512-145">為此角色選擇一部伺服器。</span><span class="sxs-lookup"><span data-stu-id="d9512-145">Choose one server for this role.</span></span> <span data-ttu-id="d9512-146">我們建議您選擇不會處理來自其他服務，要求的伺服器，因為 hello NPS 擴充功能會擲回的任何不是 RADIUS 要求的錯誤。</span><span class="sxs-lookup"><span data-stu-id="d9512-146">We recommend choosing a server that doesn't handle requests from other services, because hello NPS extension throws errors for any requests that aren't RADIUS.</span></span>

1. <span data-ttu-id="d9512-147">在您的伺服器上開啟 [hello**新增角色及功能精靈**從 hello 伺服器管理員的快速入門] 功能表。</span><span class="sxs-lookup"><span data-stu-id="d9512-147">On your server, open hello **Add Roles and Features Wizard** from hello Server Manager Quickstart menu.</span></span>
2. <span data-ttu-id="d9512-148">將您的安裝類型選為 [角色型或功能型安裝]。</span><span class="sxs-lookup"><span data-stu-id="d9512-148">Choose **Role-based or feature-based installation** for your installation type.</span></span>
3. <span data-ttu-id="d9512-149">選取 hello**網路原則與存取服務**伺服器角色。</span><span class="sxs-lookup"><span data-stu-id="d9512-149">Select hello **Network Policy and Access Services** server role.</span></span> <span data-ttu-id="d9512-150">視窗可能會快顯 tooinform 您所需的功能 toorun 此角色。</span><span class="sxs-lookup"><span data-stu-id="d9512-150">A window may pop up tooinform you of required features toorun this role.</span></span>
4. <span data-ttu-id="d9512-151">繼續透過 hello 精靈 hello 確認頁面。</span><span class="sxs-lookup"><span data-stu-id="d9512-151">Continue through hello wizard until hello Confirmation page.</span></span> <span data-ttu-id="d9512-152">選取 [安裝]。</span><span class="sxs-lookup"><span data-stu-id="d9512-152">Select **Install**.</span></span>

<span data-ttu-id="d9512-153">既然您已指定給 NPS 伺服器，您也應該設定此伺服器 toohandle hello VPN 解決方案從連入 RADIUS 要求。</span><span class="sxs-lookup"><span data-stu-id="d9512-153">Now that you have a server designated for NPS, you should also configure this server toohandle incoming RADIUS requests from hello VPN solution.</span></span>

### <a name="configure-your-vpn-solution-toocommunicate-with-hello-nps-server"></a><span data-ttu-id="d9512-154">設定您的 VPN 解決方案 toocommunicate 與 hello NPS 伺服器</span><span class="sxs-lookup"><span data-stu-id="d9512-154">Configure your VPN solution toocommunicate with hello NPS server</span></span>

<span data-ttu-id="d9512-155">根據您使用的 VPN 解決方案，hello 步驟 tooconfigure RADIUS 驗證原則而有所不同。</span><span class="sxs-lookup"><span data-stu-id="d9512-155">Depending on which VPN solution you use, hello steps tooconfigure your RADIUS authentication policy vary.</span></span> <span data-ttu-id="d9512-156">設定此原則 toopoint tooyour NPS RADIUS 伺服器。</span><span class="sxs-lookup"><span data-stu-id="d9512-156">Configure this policy toopoint tooyour RADIUS NPS server.</span></span>

### <a name="sync-domain-users-toohello-cloud"></a><span data-ttu-id="d9512-157">同步處理網域使用者 toohello 雲端</span><span class="sxs-lookup"><span data-stu-id="d9512-157">Sync domain users toohello cloud</span></span>

<span data-ttu-id="d9512-158">一定已在您的租用戶上完成此步驟，但它是，Azure AD Connect 同步處理您的資料庫最近良好 toodouble 檢查。</span><span class="sxs-lookup"><span data-stu-id="d9512-158">This step may already be complete on your tenant, but it's good toodouble-check that Azure AD Connect has synchronized your databases recently.</span></span>

1. <span data-ttu-id="d9512-159">登入 toohello [Azure 入口網站](https://portal.azure.com)身為系統管理員。</span><span class="sxs-lookup"><span data-stu-id="d9512-159">Sign in toohello [Azure portal](https://portal.azure.com) as an administrator.</span></span>
2. <span data-ttu-id="d9512-160">選取 [Azure Active Directory]  >  [Azure AD Connect]</span><span class="sxs-lookup"><span data-stu-id="d9512-160">Select **Azure Active Directory** > **Azure AD Connect**</span></span>
3. <span data-ttu-id="d9512-161">確認同步處理狀態為 [已啟用]，且上次同步處理為不到一小時前。</span><span class="sxs-lookup"><span data-stu-id="d9512-161">Verify that your sync status is **Enabled** and that your last sync was less than an hour ago.</span></span>

<span data-ttu-id="d9512-162">如果您需要關閉同步處理新回合 tookick，我們 hello 中的指示[Azure AD Connect 同步： 排程器](../active-directory/connect/active-directory-aadconnectsync-feature-scheduler.md#start-the-scheduler)。</span><span class="sxs-lookup"><span data-stu-id="d9512-162">If you need tookick off a new round of synchronization, us hello instructions in [Azure AD Connect sync: Scheduler](../active-directory/connect/active-directory-aadconnectsync-feature-scheduler.md#start-the-scheduler).</span></span>

### <a name="determine-which-authentication-methods-your-users-can-use"></a><span data-ttu-id="d9512-163">判斷您的使用者可以使用的驗證方法</span><span class="sxs-lookup"><span data-stu-id="d9512-163">Determine which authentication methods your users can use</span></span>

<span data-ttu-id="d9512-164">有兩個因素會影響與 NPS 擴充部署搭配提供的驗證方法：</span><span class="sxs-lookup"><span data-stu-id="d9512-164">There are two factors that affect which authentication methods are available with an NPS extension deployment:</span></span>

1. <span data-ttu-id="d9512-165">hello hello RADIUS 用戶端之間使用的密碼加密演算法 (VPN、 Netscaler 伺服器或其他) 與 hello NPS 伺服器。</span><span class="sxs-lookup"><span data-stu-id="d9512-165">hello password encryption algorithm used between hello RADIUS client (VPN, Netscaler server, or other) and hello NPS servers.</span></span>
   - <span data-ttu-id="d9512-166">**PAP** hello 定域機組中支援的 Azure MFA 的所有 hello 驗證方法： 通話、 單向簡訊、 行動裝置應用程式通知和行動裝置應用程式的驗證碼。</span><span class="sxs-lookup"><span data-stu-id="d9512-166">**PAP** supports all hello authentication methods of Azure MFA in hello cloud: phone call, one-way text message, mobile app notification, and mobile app verification code.</span></span>
   - <span data-ttu-id="d9512-167">**CHAPV2** 和 **EAP** 支援通話和行動裝置應用程式通知。</span><span class="sxs-lookup"><span data-stu-id="d9512-167">**CHAPV2** and **EAP** support phone call and mobile app notification.</span></span>
2. <span data-ttu-id="d9512-168">hello 輸入 hello 用戶端應用程式的方法 (VPN、 Netscaler 伺服器或其他) 可以處理。</span><span class="sxs-lookup"><span data-stu-id="d9512-168">hello input methods that hello client application (VPN, Netscaler server, or other) can handle.</span></span> <span data-ttu-id="d9512-169">Hello VPN 用戶端比方說，有一些方法 tooallow hello 使用者 tootype 文字或行動裝置應用程式的驗證程式碼中？</span><span class="sxs-lookup"><span data-stu-id="d9512-169">For example, does hello VPN client have some means tooallow hello user tootype in a verification code from a text or mobile app?</span></span>

<span data-ttu-id="d9512-170">當您部署的 hello NPS 擴充功能時，使用這些方法可供您使用者的因素 tooevaluate。</span><span class="sxs-lookup"><span data-stu-id="d9512-170">When you deploy hello NPS extension, use these factors tooevaluate which methods are available for your users.</span></span> <span data-ttu-id="d9512-171">如果您的 RADIUS 用戶端支援 PAP，但 hello 用戶端 UX 沒有驗證程式碼的輸入的欄位，然後電話和行動裝置應用程式通知 hello 兩個支援的選項。</span><span class="sxs-lookup"><span data-stu-id="d9512-171">If your RADIUS client supports PAP, but hello client UX doesn't have input fields for a verification code, then phone call and mobile app notification are hello two supported options.</span></span>

<span data-ttu-id="d9512-172">您可以在 Azure 中[停用不受支援的驗證方法](multi-factor-authentication-whats-next.md#selectable-verification-methods)。</span><span class="sxs-lookup"><span data-stu-id="d9512-172">You can [disable unsupported authentication methods](multi-factor-authentication-whats-next.md#selectable-verification-methods) in Azure.</span></span>

### <a name="enable-users-for-mfa"></a><span data-ttu-id="d9512-173">針對 MFA 啟用使用者</span><span class="sxs-lookup"><span data-stu-id="d9512-173">Enable users for MFA</span></span>

<span data-ttu-id="d9512-174">部署 hello 完整 NPS 擴充功能之前，您需要 tooenable MFA hello 想 tooperform 雙步驟驗證的使用者。</span><span class="sxs-lookup"><span data-stu-id="d9512-174">Before you deploy hello full NPS extension, you need tooenable MFA for hello users that you want tooperform two-step verification.</span></span> <span data-ttu-id="d9512-175">更立即 tootest hello 延伸模組，當您將它部署，您必須至少一個測試帳戶完全註冊多重要素驗證。</span><span class="sxs-lookup"><span data-stu-id="d9512-175">More immediately, tootest hello extension as you deploy it, you need at least one test account that is fully registered for Multi-Factor Authentication.</span></span>

<span data-ttu-id="d9512-176">使用測試帳戶啟動這些步驟 tooget:</span><span class="sxs-lookup"><span data-stu-id="d9512-176">Use these steps tooget a test account started:</span></span>
1. <span data-ttu-id="d9512-177">登入太[https://aka.ms/mfasetup](https://aka.ms/mfasetup)測試帳戶。</span><span class="sxs-lookup"><span data-stu-id="d9512-177">Sign in too[https://aka.ms/mfasetup](https://aka.ms/mfasetup) with a test account.</span></span> 
2. <span data-ttu-id="d9512-178">請遵循 hello 提示 tooset 驗證方法。</span><span class="sxs-lookup"><span data-stu-id="d9512-178">Follow hello prompts tooset up a verification method.</span></span>
3. <span data-ttu-id="d9512-179">建立條件式存取原則或[變更 hello 使用者狀態](multi-factor-authentication-get-started-user-states.md)toorequire hello 測試帳戶的雙步驟驗證。</span><span class="sxs-lookup"><span data-stu-id="d9512-179">Either create a conditional access policy or [change hello user state](multi-factor-authentication-get-started-user-states.md) toorequire two-step verification for hello test account.</span></span> 

<span data-ttu-id="d9512-180">您的使用者也需要 toofollow 這些步驟 tooenroll 之前它們向 hello NPS 擴充功能。</span><span class="sxs-lookup"><span data-stu-id="d9512-180">Your users also need toofollow these steps tooenroll before they can authenticate with hello NPS extension.</span></span>

## <a name="install-hello-nps-extension"></a><span data-ttu-id="d9512-181">安裝 hello NPS 擴充功能</span><span class="sxs-lookup"><span data-stu-id="d9512-181">Install hello NPS extension</span></span>

> [!IMPORTANT]
> <span data-ttu-id="d9512-182">不同於 hello VPN 存取點的伺服器上安裝 hello NPS 擴充功能。</span><span class="sxs-lookup"><span data-stu-id="d9512-182">Install hello NPS extension on a different server than hello VPN access point.</span></span>

### <a name="download-and-install-hello-nps-extension-for-azure-mfa"></a><span data-ttu-id="d9512-183">下載並安裝 Azure MFA hello NPS 延伸模組</span><span class="sxs-lookup"><span data-stu-id="d9512-183">Download and install hello NPS extension for Azure MFA</span></span>

1.  <span data-ttu-id="d9512-184">[下載 hello NPS 擴充](https://aka.ms/npsmfa)從 Microsoft 下載中心 hello。</span><span class="sxs-lookup"><span data-stu-id="d9512-184">[Download hello NPS Extension](https://aka.ms/npsmfa) from hello Microsoft Download Center.</span></span>
2.  <span data-ttu-id="d9512-185">將複製 hello 二進位 toohello 想 tooconfigure 網路原則伺服器。</span><span class="sxs-lookup"><span data-stu-id="d9512-185">Copy hello binary toohello Network Policy Server you want tooconfigure.</span></span>
3.  <span data-ttu-id="d9512-186">執行*setup.exe*依照 hello 安裝指示。</span><span class="sxs-lookup"><span data-stu-id="d9512-186">Run *setup.exe* and follow hello installation instructions.</span></span> <span data-ttu-id="d9512-187">如果您遇到錯誤，請仔細檢查該 hello hello 必要條件 > 一節中的兩個程式庫已成功安裝。</span><span class="sxs-lookup"><span data-stu-id="d9512-187">If you encounter errors, double-check that hello two libraries from hello prerequisite section were successfully installed.</span></span>

### <a name="run-hello-powershell-script"></a><span data-ttu-id="d9512-188">執行 hello PowerShell 指令碼</span><span class="sxs-lookup"><span data-stu-id="d9512-188">Run hello PowerShell script</span></span>

<span data-ttu-id="d9512-189">hello 安裝程式會在這個位置建立 PowerShell 指令碼： `C:\Program Files\Microsoft\AzureMfa\Config` （其中 C:\ 是安裝磁碟機）。</span><span class="sxs-lookup"><span data-stu-id="d9512-189">hello installer creates a PowerShell script in this location: `C:\Program Files\Microsoft\AzureMfa\Config` (where C:\ is your installation drive).</span></span> <span data-ttu-id="d9512-190">這個 PowerShell 指令碼會執行下列動作的 hello:</span><span class="sxs-lookup"><span data-stu-id="d9512-190">This PowerShell script performs hello following actions:</span></span>

-   <span data-ttu-id="d9512-191">建立自我簽署憑證。</span><span class="sxs-lookup"><span data-stu-id="d9512-191">Create a self-signed certificate.</span></span>
-   <span data-ttu-id="d9512-192">建立 hello 公開金鑰的 hello 憑證 toohello 服務主體上 Azure AD 的關聯。</span><span class="sxs-lookup"><span data-stu-id="d9512-192">Associate hello public key of hello certificate toohello service principal on Azure AD.</span></span>
-   <span data-ttu-id="d9512-193">存放區 hello hello 本機電腦憑證存放區中的憑證。</span><span class="sxs-lookup"><span data-stu-id="d9512-193">Store hello cert in hello local machine cert store.</span></span>
-   <span data-ttu-id="d9512-194">授與存取 toohello 憑證的私用的索引鍵 tooNetwork 使用者。</span><span class="sxs-lookup"><span data-stu-id="d9512-194">Grant access toohello certificate’s private key tooNetwork User.</span></span>
-   <span data-ttu-id="d9512-195">重新啟動 hello NPS。</span><span class="sxs-lookup"><span data-stu-id="d9512-195">Restart hello NPS.</span></span>

<span data-ttu-id="d9512-196">除非您想 toouse 自己憑證 （而不是 hello 的自我簽署憑證 hello 的 PowerShell 指令碼會產生），執行 PowerShell 指令碼 hello toocomplete hello 安裝程式。</span><span class="sxs-lookup"><span data-stu-id="d9512-196">Unless you want toouse your own certificates (instead of hello self-signed certificates that hello PowerShell script generates), run hello PowerShell Script toocomplete hello installation.</span></span> <span data-ttu-id="d9512-197">如果您在多部伺服器上安裝 hello 延伸模組，每一個應該有它自己的憑證。</span><span class="sxs-lookup"><span data-stu-id="d9512-197">If you install hello extension on multiple servers, each one should have its own certificate.</span></span>

1. <span data-ttu-id="d9512-198">以系統管理理員身分執行 Windows PowerShell。</span><span class="sxs-lookup"><span data-stu-id="d9512-198">Run Windows PowerShell as an administrator.</span></span>
2. <span data-ttu-id="d9512-199">變更目錄。</span><span class="sxs-lookup"><span data-stu-id="d9512-199">Change directories.</span></span>

   `cd "C:\Program Files\Microsoft\AzureMfa\Config"`

3. <span data-ttu-id="d9512-200">執行 hello hello 安裝程式所建立的 PowerShell 指令碼。</span><span class="sxs-lookup"><span data-stu-id="d9512-200">Run hello PowerShell script created by hello installer.</span></span>

   `.\AzureMfaNpsExtnConfigSetup.ps1`

4. <span data-ttu-id="d9512-201">PowerShell 會提示您輸入您的租用戶識別碼。</span><span class="sxs-lookup"><span data-stu-id="d9512-201">PowerShell prompts for your tenant ID.</span></span> <span data-ttu-id="d9512-202">使用 hello 從 hello hello 必要條件 > 一節中的 Azure 入口網站複製的目錄識別碼 GUID。</span><span class="sxs-lookup"><span data-stu-id="d9512-202">Use hello Directory ID GUID that you copied from hello Azure portal in hello prerequisites section.</span></span>
5. <span data-ttu-id="d9512-203">登入 tooAzure AD 系統管理員身分。</span><span class="sxs-lookup"><span data-stu-id="d9512-203">Sign in tooAzure AD as an administrator.</span></span>
6. <span data-ttu-id="d9512-204">Hello 指令碼完成時，PowerShell 會顯示成功訊息。</span><span class="sxs-lookup"><span data-stu-id="d9512-204">PowerShell shows a success message when hello script is finished.</span></span>  

<span data-ttu-id="d9512-205">重複上述步驟，在您想要進行負載平衡 tooset 任何其他 NPS 伺服器上。</span><span class="sxs-lookup"><span data-stu-id="d9512-205">Repeat these steps on any additional NPS servers that you want tooset up for load balancing.</span></span>

>[!NOTE]
><span data-ttu-id="d9512-206">如果您使用您自己的憑證，而非產生憑證以 hello PowerShell 指令碼，請確定它們對齊 toohello NPS 命名慣例。</span><span class="sxs-lookup"><span data-stu-id="d9512-206">If you use your own certificates instead of generating certificates with hello PowerShell script, make sure that they align toohello NPS naming convention.</span></span> <span data-ttu-id="d9512-207">hello 主旨名稱必須是**CN =\<TenantID\>，OU = Microsoft NPS 擴充功能**。</span><span class="sxs-lookup"><span data-stu-id="d9512-207">hello subject name must be **CN=\<TenantID\>,OU=Microsoft NPS Extension**.</span></span> 

## <a name="configure-your-nps-extension"></a><span data-ttu-id="d9512-208">設定 NPS 擴充功能</span><span class="sxs-lookup"><span data-stu-id="d9512-208">Configure your NPS extension</span></span>

<span data-ttu-id="d9512-209">本節包含成功部署 NPS 擴充功能的設計考量和建議。</span><span class="sxs-lookup"><span data-stu-id="d9512-209">This section includes design considerations and suggestions for successful NPS extension deployments.</span></span>

### <a name="configuration-limitations"></a><span data-ttu-id="d9512-210">設定限制</span><span class="sxs-lookup"><span data-stu-id="d9512-210">Configuration limitations</span></span>

- <span data-ttu-id="d9512-211">hello Azure MFA 的 NPS 擴充功能不包含工具 toomigrate 使用者和從 MFA Server toohello 雲端的設定。</span><span class="sxs-lookup"><span data-stu-id="d9512-211">hello NPS extension for Azure MFA does not include tools toomigrate users and settings from MFA Server toohello cloud.</span></span> <span data-ttu-id="d9512-212">基於這個理由，我們建議使用新的部署，而不是現有部署的 hello 延伸模組。</span><span class="sxs-lookup"><span data-stu-id="d9512-212">For this reason, we suggest using hello extension for new deployments, rather than existing deployment.</span></span> <span data-ttu-id="d9512-213">如果您使用現有部署的 hello 延伸模組，您的使用者具有 tooperform 證明總再次 toopopulate 他們 MFA 詳細說明 hello 雲端中。</span><span class="sxs-lookup"><span data-stu-id="d9512-213">If you use hello extension on an existing deployment, your users have tooperform proof-up again toopopulate their MFA details in hello cloud.</span></span>  
- <span data-ttu-id="d9512-214">hello NPS 擴充功能會使用的 hello UPN hello 從內部部署 Active directory tooidentify hello Azure MFA 上執行 hello 次要驗證 hello 延伸模組可以使用者設定的 toouse 不同的識別項，例如識別碼或自訂的 Active Directory 的替代登入UPN 以外的欄位。</span><span class="sxs-lookup"><span data-stu-id="d9512-214">hello NPS extension uses hello UPN from hello on-premises Active directory tooidentify hello user on Azure MFA for performing hello Secondary Auth. hello extension can be configured toouse a different identifier like alternate login ID or custom Active Directory field other than UPN.</span></span> <span data-ttu-id="d9512-215">請參閱[進階組態選項的 hello NPS 擴充功能的多重要素驗證](multi-factor-authentication-advanced-vpn-configurations.md)如需詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="d9512-215">See [Advanced configuration options for hello NPS extension for Multi-Factor Authentication](multi-factor-authentication-advanced-vpn-configurations.md) for more information.</span></span>
- <span data-ttu-id="d9512-216">並非所有的加密通訊協定都支援所有的驗證方法。</span><span class="sxs-lookup"><span data-stu-id="d9512-216">Not all encryption protocols support all verification methods.</span></span>
   - <span data-ttu-id="d9512-217">**PAP** 支援通話、單向簡訊、行動裝置應用程式通知和行動裝置應用程式驗證碼</span><span class="sxs-lookup"><span data-stu-id="d9512-217">**PAP** supports phone call, one-way text message, mobile app notification, and mobile app verification code</span></span>
   - <span data-ttu-id="d9512-218">**CHAPV2** 和 **EAP** 支援通話和行動裝置應用程式通知</span><span class="sxs-lookup"><span data-stu-id="d9512-218">**CHAPV2** and **EAP** support phone call and mobile app notification</span></span>

### <a name="control-radius-clients-that-require-mfa"></a><span data-ttu-id="d9512-219">控制需要 MFA 的 RADIUS 用戶端</span><span class="sxs-lookup"><span data-stu-id="d9512-219">Control RADIUS clients that require MFA</span></span>

<span data-ttu-id="d9512-220">一旦您啟用 MFA 的 RADIUS 用戶端使用 hello NPS 擴充功能時，所有的用戶端驗證是必要的 tooperform MFA。</span><span class="sxs-lookup"><span data-stu-id="d9512-220">Once you enable MFA for a RADIUS client using hello NPS Extension, all authentications for this client are required tooperform MFA.</span></span> <span data-ttu-id="d9512-221">如果您想要 tooenable MFA 某些 RADIUS 用戶端而非其他電腦，則可以設定兩部 NPS 伺服器，並在其中只有一個元件上安裝 hello 延伸模組。</span><span class="sxs-lookup"><span data-stu-id="d9512-221">If you want tooenable MFA for some RADIUS clients but not others, you can configure two NPS servers and install hello extension on only one of them.</span></span> <span data-ttu-id="d9512-222">設定您想要 toorequire MFA toosend 要求 toohello NPS 伺服器 hello 延伸模組，以設定和副檔名 hello 未設定其他 RADIUS 用戶端 toohello NPS 伺服器的 RADIUS 用戶端。</span><span class="sxs-lookup"><span data-stu-id="d9512-222">Configure RADIUS clients that you want toorequire MFA toosend requests toohello NPS server configured with hello extension, and other RADIUS clients toohello NPS server not configured with hello extension.</span></span>

### <a name="prepare-for-users-that-arent-enrolled-for-mfa"></a><span data-ttu-id="d9512-223">針對未註冊 MFA 的使用者做準備</span><span class="sxs-lookup"><span data-stu-id="d9512-223">Prepare for users that aren't enrolled for MFA</span></span>

<span data-ttu-id="d9512-224">如果您未註冊為 MFA 的使用者，您可以決定當他們嘗試 tooauthenticate 時，會發生什麼事。</span><span class="sxs-lookup"><span data-stu-id="d9512-224">If you have users that aren't enrolled for MFA, you can determine what happens when they try tooauthenticate.</span></span> <span data-ttu-id="d9512-225">使用 hello 登錄設定*REQUIRE_USER_MATCH* hello 登錄路徑中*HKLM\Software\Microsoft\AzureMFA* toocontrol hello 功能的行為。</span><span class="sxs-lookup"><span data-stu-id="d9512-225">Use hello registry setting *REQUIRE_USER_MATCH* in hello registry path *HKLM\Software\Microsoft\AzureMFA* toocontrol hello feature behavior.</span></span> <span data-ttu-id="d9512-226">此設定具有單一組態選項︰</span><span class="sxs-lookup"><span data-stu-id="d9512-226">This setting has a single configuration option:</span></span>

| <span data-ttu-id="d9512-227">索引鍵</span><span class="sxs-lookup"><span data-stu-id="d9512-227">Key</span></span> | <span data-ttu-id="d9512-228">值</span><span class="sxs-lookup"><span data-stu-id="d9512-228">Value</span></span> | <span data-ttu-id="d9512-229">預設值</span><span class="sxs-lookup"><span data-stu-id="d9512-229">Default</span></span> |
| --- | ----- | ------- |
| <span data-ttu-id="d9512-230">REQUIRE_USER_MATCH</span><span class="sxs-lookup"><span data-stu-id="d9512-230">REQUIRE_USER_MATCH</span></span> | <span data-ttu-id="d9512-231">TRUE/FALSE</span><span class="sxs-lookup"><span data-stu-id="d9512-231">TRUE/FALSE</span></span> | <span data-ttu-id="d9512-232">未設定 (對等 tooTRUE)</span><span class="sxs-lookup"><span data-stu-id="d9512-232">Not set (equivalent tooTRUE)</span></span> |

<span data-ttu-id="d9512-233">hello 此設定的目的是 toodetermine 哪些 toodo，當使用者未註冊為 MFA。</span><span class="sxs-lookup"><span data-stu-id="d9512-233">hello purpose of this setting is toodetermine what toodo when a user is not enrolled for MFA.</span></span> <span data-ttu-id="d9512-234">當 hello 索引鍵不存在、 未設定，或設 tooTRUE，hello 使用者未註冊，然後 hello 延伸失敗 hello MFA 挑戰。</span><span class="sxs-lookup"><span data-stu-id="d9512-234">When hello key does not exist, is not set, or is set tooTRUE, and hello user is not enrolled, then hello extension fails hello MFA challenge.</span></span> <span data-ttu-id="d9512-235">當 hello 機碼設定 tooFALSE hello 使用者註冊，而不需執行 MFA 就會繼續驗證。</span><span class="sxs-lookup"><span data-stu-id="d9512-235">When hello key is set tooFALSE and hello user is not enrolled, authentication proceeds without performing MFA.</span></span>

<span data-ttu-id="d9512-236">您可以選擇 toocreate 這個機碼，然後將它設定 tooFALSE，雖然您的使用者是登入，且可能不是所有註冊的 Azure MFA 尚未。</span><span class="sxs-lookup"><span data-stu-id="d9512-236">You can choose toocreate this key and set it tooFALSE while your users are onboarding, and may not all be enrolled for Azure MFA yet.</span></span> <span data-ttu-id="d9512-237">不過，因為設定 hello 索引鍵允許的 MFA toosign 中未註冊的使用者，您應該移除之前進行 tooproduction 這個機碼。</span><span class="sxs-lookup"><span data-stu-id="d9512-237">However, since setting hello key permits users that aren't enrolled for MFA toosign in, you should remove this key before going tooproduction.</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="d9512-238">疑難排解</span><span class="sxs-lookup"><span data-stu-id="d9512-238">Troubleshooting</span></span>

### <a name="how-do-i-verify-that-hello-client-cert-is-installed-as-expected"></a><span data-ttu-id="d9512-239">如何確認該 hello 用戶端憑證已安裝，如預期般？</span><span class="sxs-lookup"><span data-stu-id="d9512-239">How do I verify that hello client cert is installed as expected?</span></span>

<span data-ttu-id="d9512-240">尋找 hello hello hello 憑證存放區和 hello 私密金鑰的核取中的安裝程式所建立的自我簽署的憑證具有權限授與 toouser **NETWORK SERVICE**。</span><span class="sxs-lookup"><span data-stu-id="d9512-240">Look for hello self-signed certificate created by hello installer in hello cert store, and check that hello private key has permissions granted toouser **NETWORK SERVICE**.</span></span> <span data-ttu-id="d9512-241">hello 憑證的主體名稱的**CN \<tenantid\>，OU = Microsoft NPS 擴充功能**</span><span class="sxs-lookup"><span data-stu-id="d9512-241">hello cert has a subject name of **CN \<tenantid\>, OU = Microsoft NPS Extension**</span></span>

-------------------------------------------------------------

### <a name="how-can-i-verify-that-my-client-cert-is-associated-toomy-tenant-in-azure-active-directory"></a><span data-ttu-id="d9512-242">如何確認我的用戶端憑證是在 Azure Active Directory 中的相關聯的 toomy 租用戶？</span><span class="sxs-lookup"><span data-stu-id="d9512-242">How can I verify that my client cert is associated toomy tenant in Azure Active Directory?</span></span>

<span data-ttu-id="d9512-243">開啟 PowerShell 命令提示字元並執行下列命令的 hello:</span><span class="sxs-lookup"><span data-stu-id="d9512-243">Open PowerShell command prompt and run hello following commands:</span></span>

```
import-module MSOnline
Connect-MsolService
Get-MsolServicePrincipalCredential -AppPrincipalId "981f26a1-7f43-403b-a875-f8b09b8cd720" -ReturnKeyValues 1 
```

<span data-ttu-id="d9512-244">這些命令會列印所有租用戶關聯 hello NPS 擴充功能的執行個體，您的 PowerShell 工作階段中的 hello 憑證。</span><span class="sxs-lookup"><span data-stu-id="d9512-244">These commands print all hello certificates associating your tenant with your instance of hello NPS extension in your PowerShell session.</span></span> <span data-ttu-id="d9512-245">尋找您的憑證將用戶端憑證匯出為具 hello 私密金鑰 [Base 64 編碼 X.509(.cer)] 檔案，並與從 PowerShell hello 清單比較。</span><span class="sxs-lookup"><span data-stu-id="d9512-245">Look for your certificate by exporting your client cert as a "Base-64 encoded X.509(.cer)" file without hello private key, and compare it with hello list from PowerShell.</span></span>

<span data-ttu-id="d9512-246">有效-從且有效的時間戳記，也就是人類看得懂的格式，可以為使用的 toofilter 明顯 misfits 出，如果 hello 命令會傳回一個以上的憑證之前。</span><span class="sxs-lookup"><span data-stu-id="d9512-246">Valid-From and Valid-Until timestamps, which are in human-readable form, can be used toofilter out obvious misfits if hello command returns more than one cert.</span></span>

-------------------------------------------------------------

### <a name="why-are-my-requests-failing-with-adal-token-error"></a><span data-ttu-id="d9512-247">為何要求會失敗並出現 ADAL 權杖錯誤？</span><span class="sxs-lookup"><span data-stu-id="d9512-247">Why are my requests failing with ADAL token error?</span></span>

<span data-ttu-id="d9512-248">這個錯誤可能是因為 tooone 多種原因所造成。</span><span class="sxs-lookup"><span data-stu-id="d9512-248">This error could be due tooone of several reasons.</span></span> <span data-ttu-id="d9512-249">使用下列 toohelp 疑難排解的步驟：</span><span class="sxs-lookup"><span data-stu-id="d9512-249">Use these steps toohelp troubleshoot:</span></span>

1. <span data-ttu-id="d9512-250">重新啟動 NPS 伺服器。</span><span class="sxs-lookup"><span data-stu-id="d9512-250">Restart your NPS server.</span></span>
2. <span data-ttu-id="d9512-251">確認已如預期安裝用戶端憑證。</span><span class="sxs-lookup"><span data-stu-id="d9512-251">Verify that that client cert is installed as expected.</span></span>
3. <span data-ttu-id="d9512-252">請確認該 hello 憑證與您的租用戶相關聯的 Azure AD。</span><span class="sxs-lookup"><span data-stu-id="d9512-252">Verify that hello certificate is associated with your tenant on Azure AD.</span></span>
4. <span data-ttu-id="d9512-253">請確認該 https://login.microsoftonline.com/ 可從執行 hello 延伸模組的 hello 伺服器存取。</span><span class="sxs-lookup"><span data-stu-id="d9512-253">Verify that https://login.microsoftonline.com/ is accessible from hello server running hello extension.</span></span>

-------------------------------------------------------------

### <a name="why-does-authentication-fail-with-an-error-in-http-logs-stating-that-hello-user-is-not-found"></a><span data-ttu-id="d9512-254">驗證為何失敗，發生錯誤，指出找不到該 hello 使用者 HTTP 記錄檔中？</span><span class="sxs-lookup"><span data-stu-id="d9512-254">Why does authentication fail with an error in HTTP logs stating that hello user is not found?</span></span>

<span data-ttu-id="d9512-255">確認 AD Connect 正在執行，且該 hello 使用者存在於 Windows Active Directory 與 Azure Active Directory 中。</span><span class="sxs-lookup"><span data-stu-id="d9512-255">Verify that AD Connect is running, and that hello user is present in both Windows Active Directory and Azure Active Directory.</span></span>

------------------------------------------------------------

### <a name="why-do-i-see-http-connect-errors-in-logs-with-all-my-authentications-failing"></a><span data-ttu-id="d9512-256">為何我會在記錄中看到 HTTP 連線錯誤，且我的所有驗證都失敗？</span><span class="sxs-lookup"><span data-stu-id="d9512-256">Why do I see HTTP connect errors in logs with all my authentications failing?</span></span>

<span data-ttu-id="d9512-257">請確認該 https://adnotifications.windowsazure.com 可從執行 hello NPS 延伸模組的 hello 伺服器存取。</span><span class="sxs-lookup"><span data-stu-id="d9512-257">Verify that https://adnotifications.windowsazure.com is reachable from hello server running hello NPS extension.</span></span>


## <a name="next-steps"></a><span data-ttu-id="d9512-258">後續步驟</span><span class="sxs-lookup"><span data-stu-id="d9512-258">Next steps</span></span>

- <span data-ttu-id="d9512-259">設定替代識別碼登入，或不應該執行中的雙步驟驗證的 ip 設定的例外狀況清單[進階組態選項的 hello NPS 擴充功能的多重要素驗證](nps-extension-advanced-configuration.md)</span><span class="sxs-lookup"><span data-stu-id="d9512-259">Configure alternate IDs for login, or set up an exception list for IPs that shouldn't perform two-step verification in [Advanced configuration options for hello NPS extension for Multi-Factor Authentication](nps-extension-advanced-configuration.md)</span></span>

- [<span data-ttu-id="d9512-260">針對 Azure Multi-factor Authentication 解決 hello NPS 擴充功能中的錯誤訊息</span><span class="sxs-lookup"><span data-stu-id="d9512-260">Resolve error messages from hello NPS extension for Azure Multi-Factor Authentication</span></span>](multi-factor-authentication-nps-errors.md)
