---
title: "使用現有的 NPS 伺服器提供 Azure MFA 功能 | Microsoft Docs"
description: "Azure Multi-Factor Authentication 的網路原則伺服器擴充功能是可將雲端式雙步驟驗證功能新增至現有驗證基礎結構的簡單解決方案。"
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
ms.openlocfilehash: fa125292ee85bd9b5329cffeff7f076d3002cbf3
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="integrate-your-existing-nps-infrastructure-with-azure-multi-factor-authentication"></a><span data-ttu-id="f834c-103">將現有的 NPS 基礎結構與 Azure Multi-Factor Authentication 整合</span><span class="sxs-lookup"><span data-stu-id="f834c-103">Integrate your existing NPS infrastructure with Azure Multi-Factor Authentication</span></span>

<span data-ttu-id="f834c-104">Azure MFA 的網路原則伺服器 (NPS) 擴充功能可使用現有伺服器將雲端式 MFA 功能新增至驗證基礎結構。</span><span class="sxs-lookup"><span data-stu-id="f834c-104">The Network Policy Server (NPS) extension for Azure MFA adds cloud-based MFA capabilities to your authentication infrastructure using your existing servers.</span></span> <span data-ttu-id="f834c-105">利用 NPS 擴充功能，您可以在現有驗證流程中新增通話、簡訊或電話應用程式驗證，而不必安裝、設定及維護新的伺服器。</span><span class="sxs-lookup"><span data-stu-id="f834c-105">With the NPS extension, you can add phone call, text message, or phone app verification to your existing authentication flow without having to install, configure, and maintain new servers.</span></span> 

<span data-ttu-id="f834c-106">這個擴充功能是針對想要保護 VPN 連線但無須部署 Azure MFA Server 的組織所建立。</span><span class="sxs-lookup"><span data-stu-id="f834c-106">This extension was created for organizations that want to protect VPN connections without deploying the Azure MFA Server.</span></span> <span data-ttu-id="f834c-107">NPS 擴充功能是用於在 RADIUS 和以雲端為基礎的 Azure MFA 之間作為配接器，為聯盟或同步處理的使用者提供第二個驗證因素。</span><span class="sxs-lookup"><span data-stu-id="f834c-107">The NPS extension acts as an adapter between RADIUS and cloud-based Azure MFA to provide a second factor of authentication for federated or synced users.</span></span>

<span data-ttu-id="f834c-108">使用 Azure MFA 的 NPS 擴充功能時，驗證流程會包含下列元件︰</span><span class="sxs-lookup"><span data-stu-id="f834c-108">When using the NPS extension for Azure MFA, the authentication flow includes the following components:</span></span> 

1. <span data-ttu-id="f834c-109">**NAS/VPN 伺服器**會從 VPN 用戶端接收要求，並將其轉換為對 NPS 伺服器的 RADIUS 要求。</span><span class="sxs-lookup"><span data-stu-id="f834c-109">**NAS/VPN Server** receives requests from VPN clients and converts them into RADIUS requests to NPS servers.</span></span> 
2. <span data-ttu-id="f834c-110">**NPS 伺服器**會連線至 Active Directory，以對 RADIUS 要求執行主要驗證，並於成功時將要求傳遞至任何已安裝的擴充功能。</span><span class="sxs-lookup"><span data-stu-id="f834c-110">**NPS Server** connects to Active Directory to perform the primary authentication for the RADIUS requests and, upon success, passes the request to any installed extensions.</span></span>  
3. <span data-ttu-id="f834c-111">**NPS 擴充功能**會觸發 Azure MFA 要求以進行第二項驗證。</span><span class="sxs-lookup"><span data-stu-id="f834c-111">**NPS Extension** triggers a request to Azure MFA for the secondary authentication.</span></span> <span data-ttu-id="f834c-112">當擴充功能收到回應後，如果 MFA 挑戰成功，擴充功能便會藉由為 NPS 伺服器提供包含 Azure STS 所發行之 MFA 宣告的安全性權杖來完成驗證要求。</span><span class="sxs-lookup"><span data-stu-id="f834c-112">Once the extension receives the response, and if the MFA challenge succeeds, it completes the authentication request by providing the NPS server with security tokens that include an MFA claim, issued by Azure STS.</span></span>  
4. <span data-ttu-id="f834c-113">**Azure MFA** 會與 Azure Active Directory 通訊以擷取使用者的詳細資料，並使用為使用者設定的驗證方法執行第二項驗證。</span><span class="sxs-lookup"><span data-stu-id="f834c-113">**Azure MFA** communicates with Azure Active Directory to retrieve the user’s details and performs the secondary authentication using a verification method configured to the user.</span></span>

<span data-ttu-id="f834c-114">下圖說明此高階驗證要求流程︰</span><span class="sxs-lookup"><span data-stu-id="f834c-114">The following diagram illustrates this high-level authentication request flow:</span></span> 

![驗證流程圖](./media/multi-factor-authentication-nps-extension/auth-flow.png)

## <a name="plan-your-deployment"></a><span data-ttu-id="f834c-116">規劃您的部署</span><span class="sxs-lookup"><span data-stu-id="f834c-116">Plan your deployment</span></span>

<span data-ttu-id="f834c-117">NPS 延伸模組會自動處理備援，因此您不需要特殊組態。</span><span class="sxs-lookup"><span data-stu-id="f834c-117">The NPS extension automatically handles redundancy, so you don't need a special configuration.</span></span>

<span data-ttu-id="f834c-118">您可以視需要建立數量不拘且具有 Azure MFA 功能的 NPS 伺服器。</span><span class="sxs-lookup"><span data-stu-id="f834c-118">You can create as many Azure MFA-enabled NPS servers as you need.</span></span> <span data-ttu-id="f834c-119">如果您安裝多部伺服器，您應該為每部伺服器使用不同的用戶端憑證。</span><span class="sxs-lookup"><span data-stu-id="f834c-119">If you do install multiple servers, you should use a difference client certificate for each one of them.</span></span> <span data-ttu-id="f834c-120">建立每個伺服器的憑證，意味著您可以個別更新每個憑證，無須擔心所有的伺服器皆停機。</span><span class="sxs-lookup"><span data-stu-id="f834c-120">Creating a cert for each server means that you can update each cert individually, and not worry about downtime across all your servers.</span></span>

<span data-ttu-id="f834c-121">VPN 伺服器會路由驗證要求，因此伺服器必須留意新的 Azure MFA 啟用 NPS 伺服器。</span><span class="sxs-lookup"><span data-stu-id="f834c-121">VPN servers route authentication requests, so they need to be aware of the new Azure MFA-enabled NPS servers.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f834c-122">必要條件</span><span class="sxs-lookup"><span data-stu-id="f834c-122">Prerequisites</span></span>

<span data-ttu-id="f834c-123">NPS 擴充功能是為了搭配現有基礎結構來運作。</span><span class="sxs-lookup"><span data-stu-id="f834c-123">The NPS extension is meant to work with your existing infrastructure.</span></span> <span data-ttu-id="f834c-124">請確定您已備妥這些必要條件，然後再開始。</span><span class="sxs-lookup"><span data-stu-id="f834c-124">Make sure you have the following prerequisites before you begin.</span></span>

### <a name="licenses"></a><span data-ttu-id="f834c-125">授權</span><span class="sxs-lookup"><span data-stu-id="f834c-125">Licenses</span></span>

<span data-ttu-id="f834c-126">Azure MFA 的 NPS 擴充功能可透過 [Azure Multi-Factor Authentication 授權](multi-factor-authentication.md) (隨附於 Azure AD Premium、EMS 或 MFA 訂用帳戶) 來提供給客戶使用。</span><span class="sxs-lookup"><span data-stu-id="f834c-126">The NPS Extension for Azure MFA is available to customers with [licenses for Azure Multi-Factor Authentication](multi-factor-authentication.md) (included with Azure AD Premium, EMS, or an MFA subscription).</span></span>

### <a name="software"></a><span data-ttu-id="f834c-127">軟體</span><span class="sxs-lookup"><span data-stu-id="f834c-127">Software</span></span>

<span data-ttu-id="f834c-128">Windows Server 2008 R2 SP1 或更新版本。</span><span class="sxs-lookup"><span data-stu-id="f834c-128">Windows Server 2008 R2 SP1 or above.</span></span>

### <a name="libraries"></a><span data-ttu-id="f834c-129">程式庫</span><span class="sxs-lookup"><span data-stu-id="f834c-129">Libraries</span></span>

<span data-ttu-id="f834c-130">這些程式庫會自動連同延伸模組一起安裝。</span><span class="sxs-lookup"><span data-stu-id="f834c-130">These libraries are installed automatically with the extension.</span></span>
-   [<span data-ttu-id="f834c-131">適用於 Visual Studio 2013 的 Visual C++ 可轉散發套件 (X64)</span><span class="sxs-lookup"><span data-stu-id="f834c-131">Visual C++ Redistributable Packages for Visual Studio 2013 (X64)</span></span>](https://www.microsoft.com/download/details.aspx?id=40784)
-   [<span data-ttu-id="f834c-132">適用於 Windows PowerShell 1.1.1660 版本的 Microsoft Azure Active Directory 模組</span><span class="sxs-lookup"><span data-stu-id="f834c-132">Microsoft Azure Active Directory Module for Windows PowerShell version 1.1.166.0</span></span>](https://connect.microsoft.com/site1164/Downloads/DownloadDetails.aspx?DownloadID=59185)

### <a name="azure-active-directory"></a><span data-ttu-id="f834c-133">Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="f834c-133">Azure Active Directory</span></span>

<span data-ttu-id="f834c-134">使用 NPS 擴充功能的每位使用者都必須使用 Azure AD Connect 同步到 Azure Active Directory ，且必須註冊 MFA。</span><span class="sxs-lookup"><span data-stu-id="f834c-134">Everyone using the NPS extension must be synced to Azure Active Directory using Azure AD Connect, and must be registered for MFA.</span></span>

<span data-ttu-id="f834c-135">當您安裝擴充功能時，您的 Azure AD 租用戶需要目錄識別碼和系統管理員認證。</span><span class="sxs-lookup"><span data-stu-id="f834c-135">When you install the extension, you need the directory ID and admin credentials for your Azure AD tenant.</span></span> <span data-ttu-id="f834c-136">您可以在 [Azure 入口網站](https://portal.azure.com)中找到您的目錄識別碼。</span><span class="sxs-lookup"><span data-stu-id="f834c-136">You can find your directory ID in the [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="f834c-137">請以系統管理員身分登入，選取左側的 [Azure Active Directory] 圖示，然後選取 [屬性]。</span><span class="sxs-lookup"><span data-stu-id="f834c-137">Sign in as an administrator, select the **Azure Active Directory** icon on the left, then select **Properties**.</span></span> <span data-ttu-id="f834c-138">複製 [目錄識別碼] 方塊中的 GUID，然後儲存。</span><span class="sxs-lookup"><span data-stu-id="f834c-138">Copy the GUID in the **Directory ID** box and save it.</span></span> <span data-ttu-id="f834c-139">當您安裝 NPS 擴充功能時，將使用此 GUID 作為租用戶識別碼。</span><span class="sxs-lookup"><span data-stu-id="f834c-139">You use this GUID as the tenant ID when you install the NPS extension.</span></span>

![在 Azure Active Directory 屬性下尋找您的目錄識別碼](./media/multi-factor-authentication-nps-extension/find-directory-id.png)

## <a name="prepare-your-environment"></a><span data-ttu-id="f834c-141">準備您的環境</span><span class="sxs-lookup"><span data-stu-id="f834c-141">Prepare your environment</span></span>

<span data-ttu-id="f834c-142">在安裝 NPS 延伸模組之前，您會想要將您的環境準備就緒，以處理驗證流量。</span><span class="sxs-lookup"><span data-stu-id="f834c-142">Before you install the NPS extension, you want to prepare you environment to handle the authentication traffic.</span></span>

### <a name="enable-the-nps-role-on-a-domain-joined-server"></a><span data-ttu-id="f834c-143">啟用已加入網域之伺服器上的 NPS 角色</span><span class="sxs-lookup"><span data-stu-id="f834c-143">Enable the NPS role on a domain-joined server</span></span>

<span data-ttu-id="f834c-144">NPS 伺服器會連線到 Azure Active Directory，並驗證 MFA 要求。</span><span class="sxs-lookup"><span data-stu-id="f834c-144">The NPS server connects to Azure Active Directory and authenticates the MFA requests.</span></span> <span data-ttu-id="f834c-145">為此角色選擇一部伺服器。</span><span class="sxs-lookup"><span data-stu-id="f834c-145">Choose one server for this role.</span></span> <span data-ttu-id="f834c-146">建議您選擇不處理來自其他服務之要求的伺服器，因為 NPS 延伸模組會對任何不是 RADIUS 的要求擲回錯誤。</span><span class="sxs-lookup"><span data-stu-id="f834c-146">We recommend choosing a server that doesn't handle requests from other services, because the NPS extension throws errors for any requests that aren't RADIUS.</span></span>

1. <span data-ttu-id="f834c-147">在伺服器上，從 [伺服器管理員快速入門] 功能表開啟 [新增角色及功能精靈]。</span><span class="sxs-lookup"><span data-stu-id="f834c-147">On your server, open the **Add Roles and Features Wizard** from the Server Manager Quickstart menu.</span></span>
2. <span data-ttu-id="f834c-148">將您的安裝類型選為 [角色型或功能型安裝]。</span><span class="sxs-lookup"><span data-stu-id="f834c-148">Choose **Role-based or feature-based installation** for your installation type.</span></span>
3. <span data-ttu-id="f834c-149">選取 [網路原則與存取服務] 伺服器角色。</span><span class="sxs-lookup"><span data-stu-id="f834c-149">Select the **Network Policy and Access Services** server role.</span></span> <span data-ttu-id="f834c-150">隨即顯示快顯視窗，通知您執行這個角色所需的功能。</span><span class="sxs-lookup"><span data-stu-id="f834c-150">A window may pop up to inform you of required features to run this role.</span></span>
4. <span data-ttu-id="f834c-151">繼續執行精靈，直到顯示 [確認] 頁面為止。</span><span class="sxs-lookup"><span data-stu-id="f834c-151">Continue through the wizard until the Confirmation page.</span></span> <span data-ttu-id="f834c-152">選取 [安裝]。</span><span class="sxs-lookup"><span data-stu-id="f834c-152">Select **Install**.</span></span>

<span data-ttu-id="f834c-153">現在您已經具備指定給 NPS 的伺服器，因此也應設定這部伺服器以處理從 VPN 解決方案傳入的 RADIUS 要求。</span><span class="sxs-lookup"><span data-stu-id="f834c-153">Now that you have a server designated for NPS, you should also configure this server to handle incoming RADIUS requests from the VPN solution.</span></span>

### <a name="configure-your-vpn-solution-to-communicate-with-the-nps-server"></a><span data-ttu-id="f834c-154">設定您的 VPN 解決方案與 NPS 伺服器通訊</span><span class="sxs-lookup"><span data-stu-id="f834c-154">Configure your VPN solution to communicate with the NPS server</span></span>

<span data-ttu-id="f834c-155">根據您所使用 VPN 解決方案的不同，設定您 RADIUS 驗證原則的步驟也有所不同。</span><span class="sxs-lookup"><span data-stu-id="f834c-155">Depending on which VPN solution you use, the steps to configure your RADIUS authentication policy vary.</span></span> <span data-ttu-id="f834c-156">設定此原則以指向 RADIUS NPS 伺服器。</span><span class="sxs-lookup"><span data-stu-id="f834c-156">Configure this policy to point to your RADIUS NPS server.</span></span>

### <a name="sync-domain-users-to-the-cloud"></a><span data-ttu-id="f834c-157">將網域使用者同步處理至雲端</span><span class="sxs-lookup"><span data-stu-id="f834c-157">Sync domain users to the cloud</span></span>

<span data-ttu-id="f834c-158">這個步驟在租用戶上可能已經完成，但建議最好再次檢查，確認 Azure AD Connect 最近已同步處理您的資料庫。</span><span class="sxs-lookup"><span data-stu-id="f834c-158">This step may already be complete on your tenant, but it's good to double-check that Azure AD Connect has synchronized your databases recently.</span></span>

1. <span data-ttu-id="f834c-159">以系統管理員身分登入 [Azure 入口網站](https://portal.azure.com)。</span><span class="sxs-lookup"><span data-stu-id="f834c-159">Sign in to the [Azure portal](https://portal.azure.com) as an administrator.</span></span>
2. <span data-ttu-id="f834c-160">選取 [Azure Active Directory]  >  [Azure AD Connect]</span><span class="sxs-lookup"><span data-stu-id="f834c-160">Select **Azure Active Directory** > **Azure AD Connect**</span></span>
3. <span data-ttu-id="f834c-161">確認同步處理狀態為 [已啟用]，且上次同步處理為不到一小時前。</span><span class="sxs-lookup"><span data-stu-id="f834c-161">Verify that your sync status is **Enabled** and that your last sync was less than an hour ago.</span></span>

<span data-ttu-id="f834c-162">如果您必須展開新一回合的同步處理，請使用 [Azure AD Connect 同步處理：排程器](../active-directory/connect/active-directory-aadconnectsync-feature-scheduler.md#start-the-scheduler)中的指示。</span><span class="sxs-lookup"><span data-stu-id="f834c-162">If you need to kick off a new round of synchronization, us the instructions in [Azure AD Connect sync: Scheduler](../active-directory/connect/active-directory-aadconnectsync-feature-scheduler.md#start-the-scheduler).</span></span>

### <a name="determine-which-authentication-methods-your-users-can-use"></a><span data-ttu-id="f834c-163">判斷您的使用者可以使用的驗證方法</span><span class="sxs-lookup"><span data-stu-id="f834c-163">Determine which authentication methods your users can use</span></span>

<span data-ttu-id="f834c-164">有兩個因素會影響與 NPS 擴充部署搭配提供的驗證方法：</span><span class="sxs-lookup"><span data-stu-id="f834c-164">There are two factors that affect which authentication methods are available with an NPS extension deployment:</span></span>

1. <span data-ttu-id="f834c-165">在 RADIUS 用戶端 (VPN、Netscaler 伺服器或其他) 與 NPS 伺服器之間使用的密碼加密演算法。</span><span class="sxs-lookup"><span data-stu-id="f834c-165">The password encryption algorithm used between the RADIUS client (VPN, Netscaler server, or other) and the NPS servers.</span></span>
   - <span data-ttu-id="f834c-166">**PAP** 支援雲端中 Azure MFA 的所有驗證方法：通話、單向簡訊、行動裝置應用程式通知，和行動裝置應用程式驗證碼。</span><span class="sxs-lookup"><span data-stu-id="f834c-166">**PAP** supports all the authentication methods of Azure MFA in the cloud: phone call, one-way text message, mobile app notification, and mobile app verification code.</span></span>
   - <span data-ttu-id="f834c-167">**CHAPV2** 和 **EAP** 支援通話和行動裝置應用程式通知。</span><span class="sxs-lookup"><span data-stu-id="f834c-167">**CHAPV2** and **EAP** support phone call and mobile app notification.</span></span>
2. <span data-ttu-id="f834c-168">用戶端應用程式 (VPN、Netscaler 伺服器或其他) 可以處理的輸入法。</span><span class="sxs-lookup"><span data-stu-id="f834c-168">The input methods that the client application (VPN, Netscaler server, or other) can handle.</span></span> <span data-ttu-id="f834c-169">例如，VPN 用戶端是否有一些方法可讓使用者從文字或行動裝置應用程式輸入驗證程式碼？</span><span class="sxs-lookup"><span data-stu-id="f834c-169">For example, does the VPN client have some means to allow the user to type in a verification code from a text or mobile app?</span></span>

<span data-ttu-id="f834c-170">當您部署 NPS 擴充時，使用這些因素來評估哪些方法可供您的使用者使用。</span><span class="sxs-lookup"><span data-stu-id="f834c-170">When you deploy the NPS extension, use these factors to evaluate which methods are available for your users.</span></span> <span data-ttu-id="f834c-171">如果您的 RADIUS 用戶端支援 PAP，但用戶端 UX 沒有驗證碼的輸入欄位，則通話和行動裝置應用程式通知是兩個支援的選項。</span><span class="sxs-lookup"><span data-stu-id="f834c-171">If your RADIUS client supports PAP, but the client UX doesn't have input fields for a verification code, then phone call and mobile app notification are the two supported options.</span></span>

<span data-ttu-id="f834c-172">您可以在 Azure 中[停用不受支援的驗證方法](multi-factor-authentication-whats-next.md#selectable-verification-methods)。</span><span class="sxs-lookup"><span data-stu-id="f834c-172">You can [disable unsupported authentication methods](multi-factor-authentication-whats-next.md#selectable-verification-methods) in Azure.</span></span>

### <a name="enable-users-for-mfa"></a><span data-ttu-id="f834c-173">針對 MFA 啟用使用者</span><span class="sxs-lookup"><span data-stu-id="f834c-173">Enable users for MFA</span></span>

<span data-ttu-id="f834c-174">在部署完整 NPS 延伸模組之前，您必須針對您想要執行雙步驟驗證的使用者啟用 MFA。</span><span class="sxs-lookup"><span data-stu-id="f834c-174">Before you deploy the full NPS extension, you need to enable MFA for the users that you want to perform two-step verification.</span></span> <span data-ttu-id="f834c-175">緊接著，若要同時部署與測試延伸模組，您必須至少有一個測試帳戶，並應已針對 Multi-Factor Authentication 完全註冊此帳戶。</span><span class="sxs-lookup"><span data-stu-id="f834c-175">More immediately, to test the extension as you deploy it, you need at least one test account that is fully registered for Multi-Factor Authentication.</span></span>

<span data-ttu-id="f834c-176">使用下列步驟啟動測試帳戶：</span><span class="sxs-lookup"><span data-stu-id="f834c-176">Use these steps to get a test account started:</span></span>
1. <span data-ttu-id="f834c-177">使用測試帳戶登入 [https://aka.ms/mfasetup](https://aka.ms/mfasetup)。</span><span class="sxs-lookup"><span data-stu-id="f834c-177">Sign in to [https://aka.ms/mfasetup](https://aka.ms/mfasetup) with a test account.</span></span> 
2. <span data-ttu-id="f834c-178">遵循提示來設定驗證方法。</span><span class="sxs-lookup"><span data-stu-id="f834c-178">Follow the prompts to set up a verification method.</span></span>
3. <span data-ttu-id="f834c-179">建立條件式存取原則或[變更使用者狀態](multi-factor-authentication-get-started-user-states.md)，以要求測試帳戶進行雙步驟驗證。</span><span class="sxs-lookup"><span data-stu-id="f834c-179">Either create a conditional access policy or [change the user state](multi-factor-authentication-get-started-user-states.md) to require two-step verification for the test account.</span></span> 

<span data-ttu-id="f834c-180">您的使用者在向 NPS 擴充功能驗證之前，也必須遵循下列步驟進行註冊。</span><span class="sxs-lookup"><span data-stu-id="f834c-180">Your users also need to follow these steps to enroll before they can authenticate with the NPS extension.</span></span>

## <a name="install-the-nps-extension"></a><span data-ttu-id="f834c-181">安裝 NPS 擴充功能</span><span class="sxs-lookup"><span data-stu-id="f834c-181">Install the NPS extension</span></span>

> [!IMPORTANT]
> <span data-ttu-id="f834c-182">在與 VPN 存取點不同的伺服器上安裝 NPS 擴充功能。</span><span class="sxs-lookup"><span data-stu-id="f834c-182">Install the NPS extension on a different server than the VPN access point.</span></span>

### <a name="download-and-install-the-nps-extension-for-azure-mfa"></a><span data-ttu-id="f834c-183">下載並安裝 Azure MFA 的 NPS 延伸模組</span><span class="sxs-lookup"><span data-stu-id="f834c-183">Download and install the NPS extension for Azure MFA</span></span>

1.  <span data-ttu-id="f834c-184">從 Microsoft 下載中心[下載 NPS 延伸模組](https://aka.ms/npsmfa)。</span><span class="sxs-lookup"><span data-stu-id="f834c-184">[Download the NPS Extension](https://aka.ms/npsmfa) from the Microsoft Download Center.</span></span>
2.  <span data-ttu-id="f834c-185">將二進位檔複製到您要設定的網路原則伺服器。</span><span class="sxs-lookup"><span data-stu-id="f834c-185">Copy the binary to the Network Policy Server you want to configure.</span></span>
3.  <span data-ttu-id="f834c-186">執行 *setup.exe* 並遵循安裝指示。</span><span class="sxs-lookup"><span data-stu-id="f834c-186">Run *setup.exe* and follow the installation instructions.</span></span> <span data-ttu-id="f834c-187">如果您遇到錯誤，請根據必要條件一節再次檢查兩個已成功安裝的程式庫。</span><span class="sxs-lookup"><span data-stu-id="f834c-187">If you encounter errors, double-check that the two libraries from the prerequisite section were successfully installed.</span></span>

### <a name="run-the-powershell-script"></a><span data-ttu-id="f834c-188">執行 PowerShell 指令碼</span><span class="sxs-lookup"><span data-stu-id="f834c-188">Run the PowerShell script</span></span>

<span data-ttu-id="f834c-189">安裝程式會在下列位置建立 PowerShell 指令碼︰`C:\Program Files\Microsoft\AzureMfa\Config` (其中 C:\ 是您的安裝磁碟機)。</span><span class="sxs-lookup"><span data-stu-id="f834c-189">The installer creates a PowerShell script in this location: `C:\Program Files\Microsoft\AzureMfa\Config` (where C:\ is your installation drive).</span></span> <span data-ttu-id="f834c-190">此 PowerShell 指令碼會執行下列動作：</span><span class="sxs-lookup"><span data-stu-id="f834c-190">This PowerShell script performs the following actions:</span></span>

-   <span data-ttu-id="f834c-191">建立自我簽署憑證。</span><span class="sxs-lookup"><span data-stu-id="f834c-191">Create a self-signed certificate.</span></span>
-   <span data-ttu-id="f834c-192">讓憑證的公開金鑰與 Azure AD 的服務主體產生關聯。</span><span class="sxs-lookup"><span data-stu-id="f834c-192">Associate the public key of the certificate to the service principal on Azure AD.</span></span>
-   <span data-ttu-id="f834c-193">將憑證儲存在本機電腦的憑證存放區。</span><span class="sxs-lookup"><span data-stu-id="f834c-193">Store the cert in the local machine cert store.</span></span>
-   <span data-ttu-id="f834c-194">將憑證的私密金鑰存取權授與給網路使用者。</span><span class="sxs-lookup"><span data-stu-id="f834c-194">Grant access to the certificate’s private key to Network User.</span></span>
-   <span data-ttu-id="f834c-195">重新啟動 NPS。</span><span class="sxs-lookup"><span data-stu-id="f834c-195">Restart the NPS.</span></span>

<span data-ttu-id="f834c-196">除非您想要使用自己的憑證 (而非 PowerShell 指令碼產生的自我簽署憑證)，否則請執行 PowerShell 指令碼來完成安裝。</span><span class="sxs-lookup"><span data-stu-id="f834c-196">Unless you want to use your own certificates (instead of the self-signed certificates that the PowerShell script generates), run the PowerShell Script to complete the installation.</span></span> <span data-ttu-id="f834c-197">如果您在多部伺服器上安裝延伸模組，每一部伺服器都應該有自己的憑證。</span><span class="sxs-lookup"><span data-stu-id="f834c-197">If you install the extension on multiple servers, each one should have its own certificate.</span></span>

1. <span data-ttu-id="f834c-198">以系統管理理員身分執行 Windows PowerShell。</span><span class="sxs-lookup"><span data-stu-id="f834c-198">Run Windows PowerShell as an administrator.</span></span>
2. <span data-ttu-id="f834c-199">變更目錄。</span><span class="sxs-lookup"><span data-stu-id="f834c-199">Change directories.</span></span>

   `cd "C:\Program Files\Microsoft\AzureMfa\Config"`

3. <span data-ttu-id="f834c-200">執行安裝程式建立的 PowerShell 指令碼。</span><span class="sxs-lookup"><span data-stu-id="f834c-200">Run the PowerShell script created by the installer.</span></span>

   `.\AzureMfaNpsExtnConfigSetup.ps1`

4. <span data-ttu-id="f834c-201">PowerShell 會提示您輸入您的租用戶識別碼。</span><span class="sxs-lookup"><span data-stu-id="f834c-201">PowerShell prompts for your tenant ID.</span></span> <span data-ttu-id="f834c-202">使用您在必要條件一節中從 Azure 入口網站複製的目錄識別碼 GUID。</span><span class="sxs-lookup"><span data-stu-id="f834c-202">Use the Directory ID GUID that you copied from the Azure portal in the prerequisites section.</span></span>
5. <span data-ttu-id="f834c-203">以系統管理員身分登入 Azure AD。</span><span class="sxs-lookup"><span data-stu-id="f834c-203">Sign in to Azure AD as an administrator.</span></span>
6. <span data-ttu-id="f834c-204">PowerShell 會在指令碼完成時顯示成功訊息。</span><span class="sxs-lookup"><span data-stu-id="f834c-204">PowerShell shows a success message when the script is finished.</span></span>  

<span data-ttu-id="f834c-205">在您想要進行設定以取得負載平衡的任何其他 NPS 伺服器上，重複上述步驟。</span><span class="sxs-lookup"><span data-stu-id="f834c-205">Repeat these steps on any additional NPS servers that you want to set up for load balancing.</span></span>

>[!NOTE]
><span data-ttu-id="f834c-206">如果您使用自己的憑證，而不是透過 PowerShell 指令碼產生憑證，請確定這些憑證遵守 NPS 命名慣例。</span><span class="sxs-lookup"><span data-stu-id="f834c-206">If you use your own certificates instead of generating certificates with the PowerShell script, make sure that they align to the NPS naming convention.</span></span> <span data-ttu-id="f834c-207">主體名稱必須是 **CN=\<租用戶識別碼\>,OU=Microsoft NPS Extension**。</span><span class="sxs-lookup"><span data-stu-id="f834c-207">The subject name must be **CN=\<TenantID\>,OU=Microsoft NPS Extension**.</span></span> 

## <a name="configure-your-nps-extension"></a><span data-ttu-id="f834c-208">設定 NPS 擴充功能</span><span class="sxs-lookup"><span data-stu-id="f834c-208">Configure your NPS extension</span></span>

<span data-ttu-id="f834c-209">本節包含成功部署 NPS 擴充功能的設計考量和建議。</span><span class="sxs-lookup"><span data-stu-id="f834c-209">This section includes design considerations and suggestions for successful NPS extension deployments.</span></span>

### <a name="configuration-limitations"></a><span data-ttu-id="f834c-210">設定限制</span><span class="sxs-lookup"><span data-stu-id="f834c-210">Configuration limitations</span></span>

- <span data-ttu-id="f834c-211">Azure MFA 的 NPS 延伸模組並未包含可將使用者與設定從 MFA Server 移轉至雲端的工具。</span><span class="sxs-lookup"><span data-stu-id="f834c-211">The NPS extension for Azure MFA does not include tools to migrate users and settings from MFA Server to the cloud.</span></span> <span data-ttu-id="f834c-212">有基於此，建議將此延伸模組用於新的部署，而非用於現有部署。</span><span class="sxs-lookup"><span data-stu-id="f834c-212">For this reason, we suggest using the extension for new deployments, rather than existing deployment.</span></span> <span data-ttu-id="f834c-213">如果您在現有部署上使用此延伸模組，您的使用者必須再次執行證明，以便在雲端中填入其 MFA 詳細資料。</span><span class="sxs-lookup"><span data-stu-id="f834c-213">If you use the extension on an existing deployment, your users have to perform proof-up again to populate their MFA details in the cloud.</span></span>  
- <span data-ttu-id="f834c-214">NPS 擴充功能會使用來自內部部署 Active Directory 的 UPN，識別 Azure MFA 上用來執行次要驗證的使用者。此延伸模組可設定為使用不同的識別碼，例如 UPN 以外的替代登入識別碼或自訂 Active Directory 欄位。</span><span class="sxs-lookup"><span data-stu-id="f834c-214">The NPS extension uses the UPN from the on-premises Active directory to identify the user on Azure MFA for performing the Secondary Auth. The extension can be configured to use a different identifier like alternate login ID or custom Active Directory field other than UPN.</span></span> <span data-ttu-id="f834c-215">如需詳細資訊，請參閱 [Multi-Factor Authentication 之 NPS 延伸模組的進階設定選項](multi-factor-authentication-advanced-vpn-configurations.md)。</span><span class="sxs-lookup"><span data-stu-id="f834c-215">See [Advanced configuration options for the NPS extension for Multi-Factor Authentication](multi-factor-authentication-advanced-vpn-configurations.md) for more information.</span></span>
- <span data-ttu-id="f834c-216">並非所有的加密通訊協定都支援所有的驗證方法。</span><span class="sxs-lookup"><span data-stu-id="f834c-216">Not all encryption protocols support all verification methods.</span></span>
   - <span data-ttu-id="f834c-217">**PAP** 支援通話、單向簡訊、行動裝置應用程式通知和行動裝置應用程式驗證碼</span><span class="sxs-lookup"><span data-stu-id="f834c-217">**PAP** supports phone call, one-way text message, mobile app notification, and mobile app verification code</span></span>
   - <span data-ttu-id="f834c-218">**CHAPV2** 和 **EAP** 支援通話和行動裝置應用程式通知</span><span class="sxs-lookup"><span data-stu-id="f834c-218">**CHAPV2** and **EAP** support phone call and mobile app notification</span></span>

### <a name="control-radius-clients-that-require-mfa"></a><span data-ttu-id="f834c-219">控制需要 MFA 的 RADIUS 用戶端</span><span class="sxs-lookup"><span data-stu-id="f834c-219">Control RADIUS clients that require MFA</span></span>

<span data-ttu-id="f834c-220">為使用 NPS 擴充功能的 RADIUS 用戶端啟用 MFA 後，便需要此用戶端的所有驗證才能執行 MFA。</span><span class="sxs-lookup"><span data-stu-id="f834c-220">Once you enable MFA for a RADIUS client using the NPS Extension, all authentications for this client are required to perform MFA.</span></span> <span data-ttu-id="f834c-221">如果您想要為一些 RADIUS 用戶端啟用 MFA，但其他的用戶端則不啟用，您可以設定兩部 NPS 伺服器，並只在其中一部上安裝擴充功能。</span><span class="sxs-lookup"><span data-stu-id="f834c-221">If you want to enable MFA for some RADIUS clients but not others, you can configure two NPS servers and install the extension on only one of them.</span></span> <span data-ttu-id="f834c-222">將您想要讓其必須使用 MFA 來傳送要求的 RADIUS 用戶端設定到設定了擴充功能的 NPS 伺服器，並將其他 RADIUS 用戶端設定到未設定擴充功能的 NPS 伺服器。</span><span class="sxs-lookup"><span data-stu-id="f834c-222">Configure RADIUS clients that you want to require MFA to send requests to the NPS server configured with the extension, and other RADIUS clients to the NPS server not configured with the extension.</span></span>

### <a name="prepare-for-users-that-arent-enrolled-for-mfa"></a><span data-ttu-id="f834c-223">針對未註冊 MFA 的使用者做準備</span><span class="sxs-lookup"><span data-stu-id="f834c-223">Prepare for users that aren't enrolled for MFA</span></span>

<span data-ttu-id="f834c-224">如果您有未註冊 MFA 的使用者，您可以決定在其嘗試驗證時會有什麼結果。</span><span class="sxs-lookup"><span data-stu-id="f834c-224">If you have users that aren't enrolled for MFA, you can determine what happens when they try to authenticate.</span></span> <span data-ttu-id="f834c-225">使用登錄路徑 HKLM\Software\Microsoft\AzureMFA 中的登錄設定 *REQUIRE_USER_MATCH* 來控制功能的行為。</span><span class="sxs-lookup"><span data-stu-id="f834c-225">Use the registry setting *REQUIRE_USER_MATCH* in the registry path *HKLM\Software\Microsoft\AzureMFA* to control the feature behavior.</span></span> <span data-ttu-id="f834c-226">此設定具有單一組態選項︰</span><span class="sxs-lookup"><span data-stu-id="f834c-226">This setting has a single configuration option:</span></span>

| <span data-ttu-id="f834c-227">索引鍵</span><span class="sxs-lookup"><span data-stu-id="f834c-227">Key</span></span> | <span data-ttu-id="f834c-228">值</span><span class="sxs-lookup"><span data-stu-id="f834c-228">Value</span></span> | <span data-ttu-id="f834c-229">預設值</span><span class="sxs-lookup"><span data-stu-id="f834c-229">Default</span></span> |
| --- | ----- | ------- |
| <span data-ttu-id="f834c-230">REQUIRE_USER_MATCH</span><span class="sxs-lookup"><span data-stu-id="f834c-230">REQUIRE_USER_MATCH</span></span> | <span data-ttu-id="f834c-231">TRUE/FALSE</span><span class="sxs-lookup"><span data-stu-id="f834c-231">TRUE/FALSE</span></span> | <span data-ttu-id="f834c-232">未設定 (相當於 TRUE)</span><span class="sxs-lookup"><span data-stu-id="f834c-232">Not set (equivalent to TRUE)</span></span> |

<span data-ttu-id="f834c-233">此設定的目的是要決定當使用者未註冊 MFA 時的行為。</span><span class="sxs-lookup"><span data-stu-id="f834c-233">The purpose of this setting is to determine what to do when a user is not enrolled for MFA.</span></span> <span data-ttu-id="f834c-234">當此索引鍵不存在、未設定或是設為 TRUE 時，若使用者未註冊，則擴充功能將無法通過 MFA 挑戰。</span><span class="sxs-lookup"><span data-stu-id="f834c-234">When the key does not exist, is not set, or is set to TRUE, and the user is not enrolled, then the extension fails the MFA challenge.</span></span> <span data-ttu-id="f834c-235">當此索引鍵設為 FALSE 時，若使用者未註冊，將會繼續驗證但不執行 MFA。</span><span class="sxs-lookup"><span data-stu-id="f834c-235">When the key is set to FALSE and the user is not enrolled, authentication proceeds without performing MFA.</span></span>

<span data-ttu-id="f834c-236">在使用者要上架但尚未全部註冊 Azure MFA 時，您可以選擇建立此金鑰，並將它設為 FALSE。</span><span class="sxs-lookup"><span data-stu-id="f834c-236">You can choose to create this key and set it to FALSE while your users are onboarding, and may not all be enrolled for Azure MFA yet.</span></span> <span data-ttu-id="f834c-237">但是，設定金鑰可讓未註冊 MFA 的使用者進行登入，因此您應該先移除此金鑰，然後再移至生產環境。</span><span class="sxs-lookup"><span data-stu-id="f834c-237">However, since setting the key permits users that aren't enrolled for MFA to sign in, you should remove this key before going to production.</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="f834c-238">疑難排解</span><span class="sxs-lookup"><span data-stu-id="f834c-238">Troubleshooting</span></span>

### <a name="how-do-i-verify-that-the-client-cert-is-installed-as-expected"></a><span data-ttu-id="f834c-239">如何確認已如預期安裝用戶端憑證？</span><span class="sxs-lookup"><span data-stu-id="f834c-239">How do I verify that the client cert is installed as expected?</span></span>

<span data-ttu-id="f834c-240">在憑證存放區中尋找安裝程式所建立的自我簽署憑證，並確認私密金鑰已將權限授與給使用者 **NETWORK SERVICE**。</span><span class="sxs-lookup"><span data-stu-id="f834c-240">Look for the self-signed certificate created by the installer in the cert store, and check that the private key has permissions granted to user **NETWORK SERVICE**.</span></span> <span data-ttu-id="f834c-241">憑證的主體名稱為 **CN \<tenantid\>, OU = Microsoft NPS Extension**</span><span class="sxs-lookup"><span data-stu-id="f834c-241">The cert has a subject name of **CN \<tenantid\>, OU = Microsoft NPS Extension**</span></span>

-------------------------------------------------------------

### <a name="how-can-i-verify-that-my-client-cert-is-associated-to-my-tenant-in-azure-active-directory"></a><span data-ttu-id="f834c-242">如何確認用戶端憑證是否已和 Azure Active Directory 中的租用戶相關聯？</span><span class="sxs-lookup"><span data-stu-id="f834c-242">How can I verify that my client cert is associated to my tenant in Azure Active Directory?</span></span>

<span data-ttu-id="f834c-243">開啟 PowerShell 命令提示字元並執行下列命令：</span><span class="sxs-lookup"><span data-stu-id="f834c-243">Open PowerShell command prompt and run the following commands:</span></span>

```
import-module MSOnline
Connect-MsolService
Get-MsolServicePrincipalCredential -AppPrincipalId "981f26a1-7f43-403b-a875-f8b09b8cd720" -ReturnKeyValues 1 
```

<span data-ttu-id="f834c-244">這些命令會列印出將租用戶與 PowerShell 工作階段中之 NPS 擴充功能執行個體相關聯的所有憑證。</span><span class="sxs-lookup"><span data-stu-id="f834c-244">These commands print all the certificates associating your tenant with your instance of the NPS extension in your PowerShell session.</span></span> <span data-ttu-id="f834c-245">將用戶端憑證匯出為不含私密金鑰的 "Base-64 encoded X.509(.cer)" 檔案，然後與 PowerShell 中的清單比較，以尋找您的憑證。</span><span class="sxs-lookup"><span data-stu-id="f834c-245">Look for your certificate by exporting your client cert as a "Base-64 encoded X.509(.cer)" file without the private key, and compare it with the list from PowerShell.</span></span>

<span data-ttu-id="f834c-246">如果命令傳回多個憑證，則可以使用採人類看得懂之格式的 Valid-From 和 Valid-Until 時間戳記來篩選出明顯不符者。</span><span class="sxs-lookup"><span data-stu-id="f834c-246">Valid-From and Valid-Until timestamps, which are in human-readable form, can be used to filter out obvious misfits if the command returns more than one cert.</span></span>

-------------------------------------------------------------

### <a name="why-are-my-requests-failing-with-adal-token-error"></a><span data-ttu-id="f834c-247">為何要求會失敗並出現 ADAL 權杖錯誤？</span><span class="sxs-lookup"><span data-stu-id="f834c-247">Why are my requests failing with ADAL token error?</span></span>

<span data-ttu-id="f834c-248">此錯誤可能來自多種原因之一。</span><span class="sxs-lookup"><span data-stu-id="f834c-248">This error could be due to one of several reasons.</span></span> <span data-ttu-id="f834c-249">請使用下列步驟來協助疑難排解︰</span><span class="sxs-lookup"><span data-stu-id="f834c-249">Use these steps to help troubleshoot:</span></span>

1. <span data-ttu-id="f834c-250">重新啟動 NPS 伺服器。</span><span class="sxs-lookup"><span data-stu-id="f834c-250">Restart your NPS server.</span></span>
2. <span data-ttu-id="f834c-251">確認已如預期安裝用戶端憑證。</span><span class="sxs-lookup"><span data-stu-id="f834c-251">Verify that that client cert is installed as expected.</span></span>
3. <span data-ttu-id="f834c-252">確認憑證已與 Azure AD 上的租用戶相關聯。</span><span class="sxs-lookup"><span data-stu-id="f834c-252">Verify that the certificate is associated with your tenant on Azure AD.</span></span>
4. <span data-ttu-id="f834c-253">確認可以從執行延伸模組的伺服器存取 https://login.microsoftonline.com/。</span><span class="sxs-lookup"><span data-stu-id="f834c-253">Verify that https://login.microsoftonline.com/ is accessible from the server running the extension.</span></span>

-------------------------------------------------------------

### <a name="why-does-authentication-fail-with-an-error-in-http-logs-stating-that-the-user-is-not-found"></a><span data-ttu-id="f834c-254">驗證為何失敗，並且 HTTP 記錄中有指出找不到使用者的錯誤？</span><span class="sxs-lookup"><span data-stu-id="f834c-254">Why does authentication fail with an error in HTTP logs stating that the user is not found?</span></span>

<span data-ttu-id="f834c-255">確認 AD Connect 正在執行，且使用者已存在於 Windows Active Directory 與 Azure Active Directory。</span><span class="sxs-lookup"><span data-stu-id="f834c-255">Verify that AD Connect is running, and that the user is present in both Windows Active Directory and Azure Active Directory.</span></span>

------------------------------------------------------------

### <a name="why-do-i-see-http-connect-errors-in-logs-with-all-my-authentications-failing"></a><span data-ttu-id="f834c-256">為何我會在記錄中看到 HTTP 連線錯誤，且我的所有驗證都失敗？</span><span class="sxs-lookup"><span data-stu-id="f834c-256">Why do I see HTTP connect errors in logs with all my authentications failing?</span></span>

<span data-ttu-id="f834c-257">確認可以從執行 NPS 擴充功能的伺服器連線到 https://adnotifications.windowsazure.com。</span><span class="sxs-lookup"><span data-stu-id="f834c-257">Verify that https://adnotifications.windowsazure.com is reachable from the server running the NPS extension.</span></span>


## <a name="next-steps"></a><span data-ttu-id="f834c-258">後續步驟</span><span class="sxs-lookup"><span data-stu-id="f834c-258">Next steps</span></span>

- <span data-ttu-id="f834c-259">在 [Multi-Factor Authentication 之 NPS 延伸模組的進階設定選項](nps-extension-advanced-configuration.md)中，設定登入的替代識別碼，或為不應該執行雙步驟驗證之 IP 設定的例外狀況清單</span><span class="sxs-lookup"><span data-stu-id="f834c-259">Configure alternate IDs for login, or set up an exception list for IPs that shouldn't perform two-step verification in [Advanced configuration options for the NPS extension for Multi-Factor Authentication](nps-extension-advanced-configuration.md)</span></span>

- [<span data-ttu-id="f834c-260">解決 Azure Multi-Factor Authentication NPS 擴充功能的錯誤訊息</span><span class="sxs-lookup"><span data-stu-id="f834c-260">Resolve error messages from the NPS extension for Azure Multi-Factor Authentication</span></span>](multi-factor-authentication-nps-errors.md)
