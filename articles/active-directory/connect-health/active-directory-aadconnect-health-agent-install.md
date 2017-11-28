---
title: "aaaAzure AD Connect Health 代理程式安裝 |Microsoft 文件"
description: "這是描述 hello 代理程式安裝 AD FS 和同步處理的 hello Azure AD Connect Health 頁面。"
services: active-directory
documentationcenter: 
author: karavar
manager: samueld
editor: curtand
ms.assetid: 1cc8ae90-607d-4925-9c30-6770a4bd1b4e
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/18/2017
ms.author: billmath
ms.openlocfilehash: 9019628ec1d4c477496e08910cfd668ed1933a62
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-connect-health-agent-installation"></a><span data-ttu-id="4e516-103">Azure AD Connect Health 代理程式安裝</span><span class="sxs-lookup"><span data-stu-id="4e516-103">Azure AD Connect Health Agent Installation</span></span>
<span data-ttu-id="4e516-104">這份文件會逐步引導您完成安裝及設定 hello Azure AD Connect Health 代理程式。</span><span class="sxs-lookup"><span data-stu-id="4e516-104">This document walks you through installing and configuring hello Azure AD Connect Health Agents.</span></span> <span data-ttu-id="4e516-105">您可以下載 hello 代理程式從[這裡](active-directory-aadconnect-health.md#download-and-install-azure-ad-connect-health-agent)。</span><span class="sxs-lookup"><span data-stu-id="4e516-105">You can download hello agents from [here](active-directory-aadconnect-health.md#download-and-install-azure-ad-connect-health-agent).</span></span>

## <a name="requirements"></a><span data-ttu-id="4e516-106">需求</span><span class="sxs-lookup"><span data-stu-id="4e516-106">Requirements</span></span>
<span data-ttu-id="4e516-107">下表中的 hello 是使用 Azure AD Connect Health 需求的清單。</span><span class="sxs-lookup"><span data-stu-id="4e516-107">hello following table is a list of requirements for using Azure AD Connect Health.</span></span>

| <span data-ttu-id="4e516-108">需求</span><span class="sxs-lookup"><span data-stu-id="4e516-108">Requirement</span></span> | <span data-ttu-id="4e516-109">說明</span><span class="sxs-lookup"><span data-stu-id="4e516-109">Description</span></span> |
| --- | --- |
| <span data-ttu-id="4e516-110">Azure AD Premium</span><span class="sxs-lookup"><span data-stu-id="4e516-110">Azure AD Premium</span></span> |<span data-ttu-id="4e516-111">Azure AD Connect Health 是 Azure AD Premium 的一個功能，而且需要 Azure AD Premium。</span><span class="sxs-lookup"><span data-stu-id="4e516-111">Azure AD Connect Health is an Azure AD Premium feature and requires Azure AD Premium.</span></span> </br></br><span data-ttu-id="4e516-112">如需詳細資訊，請參閱[開始使用 Azure AD Premium](../active-directory-get-started-premium.md)</span><span class="sxs-lookup"><span data-stu-id="4e516-112">For more information, see [Getting started with Azure AD Premium](../active-directory-get-started-premium.md)</span></span> </br><span data-ttu-id="4e516-113">toostart 免費的 30 天試用版，請參閱[開始使用試用版。](https://azure.microsoft.com/trial/get-started-active-directory/)</span><span class="sxs-lookup"><span data-stu-id="4e516-113">toostart a free 30-day trial, see [Start a trial.](https://azure.microsoft.com/trial/get-started-active-directory/)</span></span> |
| <span data-ttu-id="4e516-114">您必須是全域系統管理員的 Azure AD tooget 開始使用 Azure AD Connect Health</span><span class="sxs-lookup"><span data-stu-id="4e516-114">You must be a global administrator of your Azure AD tooget started with Azure AD Connect Health</span></span> |<span data-ttu-id="4e516-115">根據預設，只有 hello 全域系統管理員可以安裝和設定 hello 健全狀況代理程式 tooget 啟動，存取 hello 入口網站，和執行 Azure AD Connect Health 內的任何作業。</span><span class="sxs-lookup"><span data-stu-id="4e516-115">By default, only hello global administrators can install and configure hello health agents tooget started, access hello portal, and perform any operations within Azure AD Connect Health.</span></span> <span data-ttu-id="4e516-116">如需詳細資訊，請參閱[管理您的 Azure AD 目錄](../active-directory-administer.md)。</span><span class="sxs-lookup"><span data-stu-id="4e516-116">For more information, see [Administering your Azure AD directory](../active-directory-administer.md).</span></span> <br><br> <span data-ttu-id="4e516-117">使用角色型存取控制您可以允許存取 tooAzure AD Connect Health tooother 使用者在組織中。</span><span class="sxs-lookup"><span data-stu-id="4e516-117">Using Role Based Access Control you can allow access tooAzure AD Connect Health tooother users in your organization.</span></span> <span data-ttu-id="4e516-118">如需詳細資訊，請參閱[適用於 Azure AD Connect Health 的角色型存取控制](active-directory-aadconnect-health-operations.md#manage-access-with-role-based-access-control)。</span><span class="sxs-lookup"><span data-stu-id="4e516-118">For more information, see [Role Based Access Control for Azure AD Connect Health.](active-directory-aadconnect-health-operations.md#manage-access-with-role-based-access-control)</span></span> </br></br><span data-ttu-id="4e516-119">**重要事項：** hello 安裝 hello 代理程式必須是工作或學校帳戶時使用的帳戶。</span><span class="sxs-lookup"><span data-stu-id="4e516-119">**Important:** hello account used when installing hello agents must be a work or school account.</span></span> <span data-ttu-id="4e516-120">不能是 Microsoft 帳戶。</span><span class="sxs-lookup"><span data-stu-id="4e516-120">It cannot be a Microsoft account.</span></span> <span data-ttu-id="4e516-121">如需詳細資訊，請參閱[以組織身分註冊 Azure](../sign-up-organization.md)</span><span class="sxs-lookup"><span data-stu-id="4e516-121">For more information, see [Sign up for Azure as an organization](../sign-up-organization.md)</span></span> |
| <span data-ttu-id="4e516-122">Azure AD Connect Health 代理程式安裝在每部目標伺服器上</span><span class="sxs-lookup"><span data-stu-id="4e516-122">Azure AD Connect Health Agent is installed on each targeted server</span></span> | <span data-ttu-id="4e516-123">Azure AD Connect Health 需要 hello 健康狀態代理程式 toobe 安裝並設定目標的伺服器 tooreceive hello 資料，並提供 hello 的監視和分析功能</span><span class="sxs-lookup"><span data-stu-id="4e516-123">Azure AD Connect Health requires hello Health Agents toobe installed and configured on targeted servers tooreceive hello data and provide hello Monitoring and Analytics capabilities</span></span> </br></br><span data-ttu-id="4e516-124">比方說，tooget 資料從您的 AD FS 基礎結構，hello 代理程式必須安裝在 hello AD FS 和 Web 應用程式 Proxy 伺服器上。</span><span class="sxs-lookup"><span data-stu-id="4e516-124">For example, tooget data from your AD FS infrastructure, hello agent must be installed on hello AD FS and Web Application Proxy servers.</span></span> <span data-ttu-id="4e516-125">同樣地，tooget 資料在您內部部署 AD DS 基礎結構，hello 代理程式必須安裝 hello 網域控制站上。</span><span class="sxs-lookup"><span data-stu-id="4e516-125">Similarly, tooget data on your on-premises AD DS infrastructure, hello agent must be installed on hello domain controllers.</span></span> </br></br> |
| <span data-ttu-id="4e516-126">輸出連線 toohello Azure 服務端點</span><span class="sxs-lookup"><span data-stu-id="4e516-126">Outbound connectivity toohello Azure service endpoints</span></span> | <span data-ttu-id="4e516-127">在安裝和執行階段，hello 代理程式需要連接 tooAzure AD Connect Health 服務端點。</span><span class="sxs-lookup"><span data-stu-id="4e516-127">During installation and runtime, hello agent requires connectivity tooAzure AD Connect Health service endpoints.</span></span> <span data-ttu-id="4e516-128">如果使用防火牆封鎖輸出連線，請確定下列端點該 hello 加入 toohello 允許清單：</span><span class="sxs-lookup"><span data-stu-id="4e516-128">If outbound connectivity is blocked using Firewalls, ensure that hello following endpoints are added toohello allowed list:</span></span> </br></br><li><span data-ttu-id="4e516-129">&#42;.blob.core.windows.net</span><span class="sxs-lookup"><span data-stu-id="4e516-129">&#42;.blob.core.windows.net</span></span> </li><li><span data-ttu-id="4e516-130">&#42;.servicebus.windows.net - Port: 5671</span><span class="sxs-lookup"><span data-stu-id="4e516-130">&#42;.servicebus.windows.net - Port: 5671</span></span> </li><li><span data-ttu-id="4e516-131">&#42;.adhybridhealth.azure.com/</span><span class="sxs-lookup"><span data-stu-id="4e516-131">&#42;.adhybridhealth.azure.com/</span></span></li><li><span data-ttu-id="4e516-132">https://management.azure.com</span><span class="sxs-lookup"><span data-stu-id="4e516-132">https://management.azure.com</span></span> </li><li><span data-ttu-id="4e516-133">https://policykeyservice.dc.ad.msft.net/</span><span class="sxs-lookup"><span data-stu-id="4e516-133">https://policykeyservice.dc.ad.msft.net/</span></span></li><li><span data-ttu-id="4e516-134">https://login.windows.net</span><span class="sxs-lookup"><span data-stu-id="4e516-134">https://login.windows.net</span></span></li><li><span data-ttu-id="4e516-135">https://login.microsoftonline.com</span><span class="sxs-lookup"><span data-stu-id="4e516-135">https://login.microsoftonline.com</span></span></li><li><span data-ttu-id="4e516-136">https://secure.aadcdn.microsoftonline-p.com</span><span class="sxs-lookup"><span data-stu-id="4e516-136">https://secure.aadcdn.microsoftonline-p.com</span></span></li> |
|<span data-ttu-id="4e516-137">以 IP 位址為基礎的輸出連線</span><span class="sxs-lookup"><span data-stu-id="4e516-137">Outbound connectivity based on IP Addresses</span></span> | <span data-ttu-id="4e516-138">IP 位址篩選防火牆，請參閱 toohello [Azure IP 範圍](https://www.microsoft.com/en-us/download/details.aspx?id=41653)。</span><span class="sxs-lookup"><span data-stu-id="4e516-138">For IP address based filtering on firewalls, refer toohello [Azure IP Ranges](https://www.microsoft.com/en-us/download/details.aspx?id=41653).</span></span>|
| <span data-ttu-id="4e516-139">已篩選或停用輸出流量的 SSL 檢查</span><span class="sxs-lookup"><span data-stu-id="4e516-139">SSL Inspection for outbound traffic is filtered or disabled</span></span> | <span data-ttu-id="4e516-140">如果沒有 SSL 檢查或終止 hello 網路層級的輸出流量，hello 代理程式註冊步驟或資料上傳作業可能會失敗。</span><span class="sxs-lookup"><span data-stu-id="4e516-140">hello agent registration step or data upload operations may fail if there is SSL inspection or termination for outbound traffic at hello network layer.</span></span> |
| <span data-ttu-id="4e516-141">Hello 執行 hello 代理程式的伺服器上的防火牆連接埠。</span><span class="sxs-lookup"><span data-stu-id="4e516-141">Firewall ports on hello server running hello agent.</span></span> |<span data-ttu-id="4e516-142">hello 代理程式需要下列 toobe 開啟 hello 代理程式 toocommunicate hello Azure AD Health 服務端點一起使用的防火牆連接埠的 hello。</span><span class="sxs-lookup"><span data-stu-id="4e516-142">hello agent requires hello following firewall ports toobe open in order for hello agent toocommunicate with hello Azure AD Health service endpoints.</span></span></br></br><li><span data-ttu-id="4e516-143">TCP 通訊埠 443</span><span class="sxs-lookup"><span data-stu-id="4e516-143">TCP port 443</span></span></li><li><span data-ttu-id="4e516-144">TCP 通訊埠 5671</span><span class="sxs-lookup"><span data-stu-id="4e516-144">TCP port 5671</span></span></li> |
| <span data-ttu-id="4e516-145">允許下列網站，如果已啟用 IE 增強式安全性的 hello</span><span class="sxs-lookup"><span data-stu-id="4e516-145">Allow hello following websites if IE Enhanced Security is enabled</span></span> |<span data-ttu-id="4e516-146">如果已啟用 IE 增強式安全性，然後 hello 下列網站，必須允許 hello 進行 toohave hello 代理程式安裝的伺服器上。</span><span class="sxs-lookup"><span data-stu-id="4e516-146">If IE Enhanced Security is enabled, then hello following websites must be allowed on hello server that is going toohave hello agent installed.</span></span></br></br><li><span data-ttu-id="4e516-147">https://login.microsoftonline.com</span><span class="sxs-lookup"><span data-stu-id="4e516-147">https://login.microsoftonline.com</span></span></li><li><span data-ttu-id="4e516-148">https://secure.aadcdn.microsoftonline-p.com</span><span class="sxs-lookup"><span data-stu-id="4e516-148">https://secure.aadcdn.microsoftonline-p.com</span></span></li><li><span data-ttu-id="4e516-149">https://login.windows.net</span><span class="sxs-lookup"><span data-stu-id="4e516-149">https://login.windows.net</span></span></li><li><span data-ttu-id="4e516-150">hello 信任的 Azure Active Directory 組織的同盟伺服器。</span><span class="sxs-lookup"><span data-stu-id="4e516-150">hello federation server for your organization trusted by Azure Active Directory.</span></span> <span data-ttu-id="4e516-151">例如︰https://sts.contoso.com</span><span class="sxs-lookup"><span data-stu-id="4e516-151">For example: https://sts.contoso.com</span></span></li> |
|<span data-ttu-id="4e516-152">停用 FIPS</span><span class="sxs-lookup"><span data-stu-id="4e516-152">Disable FIPS</span></span>|<span data-ttu-id="4e516-153">Azure AD Connect Health 代理程式不支援 FIPS。</span><span class="sxs-lookup"><span data-stu-id="4e516-153">FIPS is not supported by Azure AD Connect Health agents.</span></span>|

## <a name="installing-hello-azure-ad-connect-health-agent-for-ad-fs"></a><span data-ttu-id="4e516-154">安裝 Azure AD Connect Health 代理程式的 AD FS hello</span><span class="sxs-lookup"><span data-stu-id="4e516-154">Installing hello Azure AD Connect Health Agent for AD FS</span></span>
<span data-ttu-id="4e516-155">toostart hello 代理程式安裝中，按兩下您下載的 hello.exe 檔案。</span><span class="sxs-lookup"><span data-stu-id="4e516-155">toostart hello agent installation, double-click hello .exe file that you downloaded.</span></span> <span data-ttu-id="4e516-156">在 hello 第一個畫面上，按一下 安裝。</span><span class="sxs-lookup"><span data-stu-id="4e516-156">On hello first screen, click Install.</span></span>

![驗證 Azure AD Connect Health](./media/active-directory-aadconnect-health-requirements/install1.png)

<span data-ttu-id="4e516-158">一旦 hello 安裝完成時，按一下 [立即設定]。</span><span class="sxs-lookup"><span data-stu-id="4e516-158">Once hello installation is finished, click Configure Now.</span></span>

![驗證 Azure AD Connect Health](./media/active-directory-aadconnect-health-requirements/install2.png)

<span data-ttu-id="4e516-160">這會啟動 PowerShell 視窗 tooinitiate hello 代理程式登錄程序。</span><span class="sxs-lookup"><span data-stu-id="4e516-160">This launches a PowerShell window tooinitiate hello agent registration process.</span></span> <span data-ttu-id="4e516-161">出現提示時，使用具有存取 tooperform 代理程式註冊的 Azure AD 帳戶登入。</span><span class="sxs-lookup"><span data-stu-id="4e516-161">When prompted, sign in with an Azure AD account that has access tooperform agent registration.</span></span> <span data-ttu-id="4e516-162">根據預設 hello 全域管理員帳戶的存取。</span><span class="sxs-lookup"><span data-stu-id="4e516-162">By default hello Global Admin account has access.</span></span>

![驗證 Azure AD Connect Health](./media/active-directory-aadconnect-health-requirements/install3.png)

<span data-ttu-id="4e516-164">登入後，PowerShell 將會繼續。</span><span class="sxs-lookup"><span data-stu-id="4e516-164">After signing in, PowerShell will continue.</span></span> <span data-ttu-id="4e516-165">在完成時，您可以關閉 PowerShell 和 hello 設定已完成。</span><span class="sxs-lookup"><span data-stu-id="4e516-165">Once it completes, you can close PowerShell and hello configuration is complete.</span></span>

<span data-ttu-id="4e516-166">此時，hello 啟動代理程式服務應該是自動允許 hello 代理程式上傳所需的 hello 資料 toohello 雲端服務以安全的方式。</span><span class="sxs-lookup"><span data-stu-id="4e516-166">At this point, hello agent services should be started automatically allowing hello agent upload hello required data toohello cloud service in a secure manner.</span></span>

<span data-ttu-id="4e516-167">如果您有不符合所有 hello 先決條件 hello 上一節所述，在 hello PowerShell 視窗中會出現警告。</span><span class="sxs-lookup"><span data-stu-id="4e516-167">If you have not met all hello pre-requisites outlined in hello previous sections, warnings appear in hello PowerShell window.</span></span> <span data-ttu-id="4e516-168">要確定 toocomplete hello[需求](active-directory-aadconnect-health-agent-install.md#requirements)之前安裝 hello 代理程式。</span><span class="sxs-lookup"><span data-stu-id="4e516-168">Be sure toocomplete hello [requirements](active-directory-aadconnect-health-agent-install.md#requirements) before installing hello agent.</span></span> <span data-ttu-id="4e516-169">下列螢幕擷取畫面的 hello 是這些錯誤的範例。</span><span class="sxs-lookup"><span data-stu-id="4e516-169">hello following screenshot is an example of these errors.</span></span>

![驗證 Azure AD Connect Health](./media/active-directory-aadconnect-health-requirements/install4.png)

<span data-ttu-id="4e516-171">已安裝 tooverify hello 代理程式、 尋找 hello 遵循 hello 伺服器上的服務。</span><span class="sxs-lookup"><span data-stu-id="4e516-171">tooverify hello agent has been installed, look for hello following services on hello server.</span></span> <span data-ttu-id="4e516-172">如果您已完成 hello 組態，它們應該已執行。</span><span class="sxs-lookup"><span data-stu-id="4e516-172">If you completed hello configuration, they should already be running.</span></span> <span data-ttu-id="4e516-173">否則，它們會停止，直到 hello 設定已完成。</span><span class="sxs-lookup"><span data-stu-id="4e516-173">Otherwise, they are stopped until hello configuration is complete.</span></span>

* <span data-ttu-id="4e516-174">Azure AD Connect Health AD FS 診斷服務</span><span class="sxs-lookup"><span data-stu-id="4e516-174">Azure AD Connect Health AD FS Diagnostics Service</span></span>
* <span data-ttu-id="4e516-175">Azure AD Connect Health AD FS Insights 服務</span><span class="sxs-lookup"><span data-stu-id="4e516-175">Azure AD Connect Health AD FS Insights Service</span></span>
* <span data-ttu-id="4e516-176">Azure AD Connect Health AD FS 監視服務</span><span class="sxs-lookup"><span data-stu-id="4e516-176">Azure AD Connect Health AD FS Monitoring Service</span></span>

![驗證 Azure AD Connect Health](./media/active-directory-aadconnect-health-requirements/install5.png)

### <a name="agent-installation-on-windows-server-2008-r2-servers"></a><span data-ttu-id="4e516-178">Windows Server 2008 R2 伺服器上的代理程式安裝</span><span class="sxs-lookup"><span data-stu-id="4e516-178">Agent installation on Windows Server 2008 R2 Servers</span></span>
<span data-ttu-id="4e516-179">適用於 Windows Server 2008 R2 伺服器的步驟：</span><span class="sxs-lookup"><span data-stu-id="4e516-179">Steps for Windows Server 2008 R2 servers:</span></span>

1. <span data-ttu-id="4e516-180">確定該 hello 伺服器正在執行 Service Pack 1 或更高版本。</span><span class="sxs-lookup"><span data-stu-id="4e516-180">Ensure that hello server is running at Service Pack 1 or higher.</span></span>
2. <span data-ttu-id="4e516-181">關閉 IE ESC 以安裝代理程式：</span><span class="sxs-lookup"><span data-stu-id="4e516-181">Turn off IE ESC for agent installation:</span></span>
3. <span data-ttu-id="4e516-182">每一個 hello 預先安裝 hello AD Health 代理程式的伺服器上安裝 Windows PowerShell 4.0。</span><span class="sxs-lookup"><span data-stu-id="4e516-182">Install Windows PowerShell 4.0 on each of hello servers ahead of installing hello AD Health agent.</span></span> <span data-ttu-id="4e516-183">tooinstall Windows PowerShell 4.0:</span><span class="sxs-lookup"><span data-stu-id="4e516-183">tooinstall Windows PowerShell 4.0:</span></span>
   * <span data-ttu-id="4e516-184">安裝[Microsoft.NET Framework 4.5](https://www.microsoft.com/download/details.aspx?id=40779)使用 hello 遵循連結 toodownload hello 離線安裝程式。</span><span class="sxs-lookup"><span data-stu-id="4e516-184">Install [Microsoft .NET Framework 4.5](https://www.microsoft.com/download/details.aspx?id=40779) using hello following link toodownload hello offline installer.</span></span>
   * <span data-ttu-id="4e516-185">安裝 PowerShell ISE (從 Windows 功能)</span><span class="sxs-lookup"><span data-stu-id="4e516-185">Install PowerShell ISE (From Windows Features)</span></span>
   * <span data-ttu-id="4e516-186">安裝 hello [Windows Management Framework 4.0。](https://www.microsoft.com/download/details.aspx?id=40855)</span><span class="sxs-lookup"><span data-stu-id="4e516-186">Install hello [Windows Management Framework 4.0.](https://www.microsoft.com/download/details.aspx?id=40855)</span></span>
   * <span data-ttu-id="4e516-187">安裝 Internet Explorer 第 10 版或更高版本 hello 伺服器上。</span><span class="sxs-lookup"><span data-stu-id="4e516-187">Install Internet Explorer version 10 or above on hello server.</span></span> <span data-ttu-id="4e516-188">（需要 hello 健全狀況服務 tooauthenticate，使用您的 Azure 系統管理員認證）。</span><span class="sxs-lookup"><span data-stu-id="4e516-188">(Required by hello Health Service tooauthenticate, using your Azure Admin credentials.)</span></span>
4. <span data-ttu-id="4e516-189">如需有關如何在 Windows Server 2008 R2 上安裝 Windows PowerShell 4.0 的詳細資訊，請參閱 hello wiki 文章[這裡](http://social.technet.microsoft.com/wiki/contents/articles/20623.step-by-step-upgrading-the-powershell-version-4-on-2008-r2.aspx)。</span><span class="sxs-lookup"><span data-stu-id="4e516-189">For more information on installing Windows PowerShell 4.0 on Windows Server 2008 R2, see hello wiki article [here](http://social.technet.microsoft.com/wiki/contents/articles/20623.step-by-step-upgrading-the-powershell-version-4-on-2008-r2.aspx).</span></span>

### <a name="enable-auditing-for-ad-fs"></a><span data-ttu-id="4e516-190">啟用 AD FS 的稽核</span><span class="sxs-lookup"><span data-stu-id="4e516-190">Enable Auditing for AD FS</span></span>
> [!NOTE]
> <span data-ttu-id="4e516-191">本節僅適用於 tooAD FS 伺服器。</span><span class="sxs-lookup"><span data-stu-id="4e516-191">This section only applies tooAD FS servers.</span></span> <span data-ttu-id="4e516-192">您沒有 toofollow hello Web 應用程式 Proxy 伺服器上的這些步驟。</span><span class="sxs-lookup"><span data-stu-id="4e516-192">You do not have toofollow these steps on hello Web Application Proxy Servers.</span></span>
>

<span data-ttu-id="4e516-193">為了讓 hello 流量分析功能 toogather 並分析資料，hello Azure AD Connect Health 代理程式需要 hello hello AD FS 稽核記錄檔中的資訊。</span><span class="sxs-lookup"><span data-stu-id="4e516-193">In order for hello Usage Analytics feature toogather and analyze data, hello Azure AD Connect Health agent needs hello information in hello AD FS Audit Logs.</span></span> <span data-ttu-id="4e516-194">預設不會啟用這些記錄檔。</span><span class="sxs-lookup"><span data-stu-id="4e516-194">These logs are not enabled by default.</span></span> <span data-ttu-id="4e516-195">使用下列程序 tooenable AD FS 稽核的 hello 和 toolocate hello AD FS 稽核記錄檔，在 AD FS 伺服器上。</span><span class="sxs-lookup"><span data-stu-id="4e516-195">Use hello following procedures tooenable AD FS auditing and toolocate hello AD FS audit logs, on your AD FS servers.</span></span>

#### <a name="tooenable-auditing-for-ad-fs-on-windows-server-2008-r2"></a><span data-ttu-id="4e516-196">Windows Server 2008 R2 上的 AD FS 的稽核 tooenable</span><span class="sxs-lookup"><span data-stu-id="4e516-196">tooenable auditing for AD FS on Windows Server 2008 R2</span></span>
1. <span data-ttu-id="4e516-197">按一下**啟動**，點太**程式**，點太**系統管理工具**，然後按一下**本機安全性原則**。</span><span class="sxs-lookup"><span data-stu-id="4e516-197">Click **Start**, point too**Programs**, point too**Administrative Tools**, and then click **Local Security Policy**.</span></span>
2. <span data-ttu-id="4e516-198">瀏覽 toohello**安全性 \ 使用者權限管理**資料夾，然後按兩下 產生安全性稽核。</span><span class="sxs-lookup"><span data-stu-id="4e516-198">Navigate toohello **Security Settings\Local Policies\User Rights Management** folder, and then double-click Generate security audits.</span></span>
3. <span data-ttu-id="4e516-199">在 hello**本機安全性設定**索引標籤上，確認已列出 hello AD FS 2.0 服務帳戶。</span><span class="sxs-lookup"><span data-stu-id="4e516-199">On hello **Local Security Setting** tab, verify that hello AD FS 2.0 service account is listed.</span></span> <span data-ttu-id="4e516-200">如果不存在，請按一下**新增使用者或群組**並將它加入 toohello 清單，然後按一下**確定**。</span><span class="sxs-lookup"><span data-stu-id="4e516-200">If it is not present, click **Add User or Group** and add it toohello list, and then click **OK**.</span></span>
4. <span data-ttu-id="4e516-201">tooenable 稽核，使用提高的權限開啟命令提示字元並執行下列命令的 hello:<code>auditpol.exe /set /subcategory:"Application Generated" /failure:enable /success:enable</code></span><span class="sxs-lookup"><span data-stu-id="4e516-201">tooenable auditing, open a command prompt with elevated privileges and run hello following command: <code>auditpol.exe /set /subcategory:"Application Generated" /failure:enable /success:enable</code></span></span>
5. <span data-ttu-id="4e516-202">關閉 [本機安全性原則]，然後開啟 hello 管理嵌入式管理單元。</span><span class="sxs-lookup"><span data-stu-id="4e516-202">Close Local Security Policy, and then open hello Management snap-in.</span></span> <span data-ttu-id="4e516-203">按一下 [管理] 嵌入式管理單元 tooopen hello**啟動**，點太**程式**，點太**系統管理工具**，然後按一下AD FS 2.0 管理。</span><span class="sxs-lookup"><span data-stu-id="4e516-203">tooopen hello Management snap-in, click **Start**, point too**Programs**, point too**Administrative Tools**, and then click AD FS 2.0 Management.</span></span>
6. <span data-ttu-id="4e516-204">Hello 動作] 窗格中按一下 [編輯同盟服務內容。</span><span class="sxs-lookup"><span data-stu-id="4e516-204">In hello Actions pane, click Edit Federation Service Properties.</span></span>
7. <span data-ttu-id="4e516-205">在 [hello **Federation Service 屬性**對話方塊方塊中，按一下 hello**事件**] 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="4e516-205">In hello **Federation Service Properties** dialog box, click hello **Events** tab.</span></span>
8. <span data-ttu-id="4e516-206">選取 hello**成功稽核**和**失敗稽核**核取方塊。</span><span class="sxs-lookup"><span data-stu-id="4e516-206">Select hello **Success audits** and **Failure audits** check boxes.</span></span>
9. <span data-ttu-id="4e516-207">按一下 [確定] 。</span><span class="sxs-lookup"><span data-stu-id="4e516-207">Click **OK**.</span></span>

#### <a name="tooenable-auditing-for-ad-fs-on-windows-server-2012-r2"></a><span data-ttu-id="4e516-208">Windows Server 2012 R2 上的 AD FS 的稽核 tooenable</span><span class="sxs-lookup"><span data-stu-id="4e516-208">tooenable auditing for AD FS on Windows Server 2012 R2</span></span>
1. <span data-ttu-id="4e516-209">開啟**本機安全性原則**開啟**伺服器管理員**hello 開始 畫面或桌面上 hello hello 工作列中的 伺服器管理員，然後按一下 **工具/本機安全性原則**.</span><span class="sxs-lookup"><span data-stu-id="4e516-209">Open **Local Security Policy** by opening **Server Manager** on hello Start screen, or Server Manager in hello taskbar on hello desktop, then click **Tools/Local Security Policy**.</span></span>
2. <span data-ttu-id="4e516-210">瀏覽 toohello**安全性本機原則 \ 使用者權限指派**資料夾，然後再按兩下**產生安全性稽核**。</span><span class="sxs-lookup"><span data-stu-id="4e516-210">Navigate toohello **Security Settings\Local Policies\User Rights Assignment** folder, and then double-click **Generate security audits**.</span></span>
3. <span data-ttu-id="4e516-211">在 hello**本機安全性設定**索引標籤上，確認已列出 hello AD FS 服務帳戶。</span><span class="sxs-lookup"><span data-stu-id="4e516-211">On hello **Local Security Setting** tab, verify that hello AD FS service account is listed.</span></span> <span data-ttu-id="4e516-212">如果不存在，請按一下**新增使用者或群組**並將它加入 toohello 清單，然後按一下**確定**。</span><span class="sxs-lookup"><span data-stu-id="4e516-212">If it is not present, click **Add User or Group** and add it toohello list, and then click **OK**.</span></span>
4. <span data-ttu-id="4e516-213">tooenable 稽核，以提高的權限開啟命令提示字元並執行下列命令的 hello: ```auditpol.exe /set /subcategory:"Application Generated" /failure:enable /success:enable```。</span><span class="sxs-lookup"><span data-stu-id="4e516-213">tooenable auditing, open a command prompt with elevated privileges and run hello following command: ```auditpol.exe /set /subcategory:"Application Generated" /failure:enable /success:enable```.</span></span>
5. <span data-ttu-id="4e516-214">關閉**本機安全性原則**，然後開啟 hello **AD FS 管理**嵌入式管理單元 （在 伺服器管理員 中，按一下工具，然後選取 AD FS 管理）。</span><span class="sxs-lookup"><span data-stu-id="4e516-214">Close **Local Security Policy**, and then open hello **AD FS Management** snap-in (in Server Manager, click Tools, and then select AD FS Management).</span></span>
6. <span data-ttu-id="4e516-215">在 hello 動作 窗格中，按一下 **編輯 Federation Service 屬性**。</span><span class="sxs-lookup"><span data-stu-id="4e516-215">In hello Actions pane, click **Edit Federation Service Properties**.</span></span>
7. <span data-ttu-id="4e516-216">在 hello Federation Service 屬性 對話方塊中，按一下 hello**事件** 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="4e516-216">In hello Federation Service Properties dialog box, click hello **Events** tab.</span></span>
8. <span data-ttu-id="4e516-217">選取 hello**成功稽核與失敗稽核**核取方塊，然後按一下**確定**。</span><span class="sxs-lookup"><span data-stu-id="4e516-217">Select hello **Success audits and Failure audits** check boxes and then click **OK**.</span></span>

#### <a name="tooenable-auditing-for-ad-fs-on-windows-server-2016"></a><span data-ttu-id="4e516-218">Windows Server 2016 上的 AD FS 的稽核 tooenable</span><span class="sxs-lookup"><span data-stu-id="4e516-218">tooenable auditing for AD FS on Windows Server 2016</span></span>
1. <span data-ttu-id="4e516-219">開啟**本機安全性原則**開啟**伺服器管理員**hello 開始 畫面或桌面上 hello hello 工作列中的 伺服器管理員，然後按一下 **工具/本機安全性原則**.</span><span class="sxs-lookup"><span data-stu-id="4e516-219">Open **Local Security Policy** by opening **Server Manager** on hello Start screen, or Server Manager in hello taskbar on hello desktop, then click **Tools/Local Security Policy**.</span></span>
2. <span data-ttu-id="4e516-220">瀏覽 toohello**安全性本機原則 \ 使用者權限指派**資料夾，然後再按兩下**產生安全性稽核**。</span><span class="sxs-lookup"><span data-stu-id="4e516-220">Navigate toohello **Security Settings\Local Policies\User Rights Assignment** folder, and then double-click **Generate security audits**.</span></span>
3. <span data-ttu-id="4e516-221">在 hello**本機安全性設定**索引標籤上，確認已列出 hello AD FS 服務帳戶。</span><span class="sxs-lookup"><span data-stu-id="4e516-221">On hello **Local Security Setting** tab, verify that hello AD FS service account is listed.</span></span> <span data-ttu-id="4e516-222">如果不存在，請按一下**新增使用者或群組**然後新增 hello AD FS 服務帳戶 toohello 清單，然後再按一下**確定**。</span><span class="sxs-lookup"><span data-stu-id="4e516-222">If it is not present, click **Add User or Group** and add hello AD FS service account toohello list, and then click **OK**.</span></span>
4. <span data-ttu-id="4e516-223">tooenable 稽核，使用提高的權限開啟命令提示字元並執行下列命令的 hello:<code>auditpol.exe /set /subcategory:"Application Generated" /failure:enable /success:enable.</code></span><span class="sxs-lookup"><span data-stu-id="4e516-223">tooenable auditing, open a command prompt with elevated privileges and run hello following command: <code>auditpol.exe /set /subcategory:"Application Generated" /failure:enable /success:enable.</code></span></span>
5. <span data-ttu-id="4e516-224">關閉**本機安全性原則**，然後開啟 hello **AD FS 管理**嵌入式管理單元 （在 伺服器管理員 中，按一下工具，然後選取 AD FS 管理）。</span><span class="sxs-lookup"><span data-stu-id="4e516-224">Close **Local Security Policy**, and then open hello **AD FS Management** snap-in (in Server Manager, click Tools, and then select AD FS Management).</span></span>
6. <span data-ttu-id="4e516-225">在 hello 動作 窗格中，按一下 **編輯 Federation Service 屬性**。</span><span class="sxs-lookup"><span data-stu-id="4e516-225">In hello Actions pane, click **Edit Federation Service Properties**.</span></span>
7. <span data-ttu-id="4e516-226">在 hello Federation Service 屬性 對話方塊中，按一下 hello**事件** 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="4e516-226">In hello Federation Service Properties dialog box, click hello **Events** tab.</span></span>
8. <span data-ttu-id="4e516-227">選取 hello**成功稽核與失敗稽核**核取方塊，然後按一下**確定**。</span><span class="sxs-lookup"><span data-stu-id="4e516-227">Select hello **Success audits and Failure audits** check boxes and then click **OK**.</span></span> <span data-ttu-id="4e516-228">預設會啟用此功能。</span><span class="sxs-lookup"><span data-stu-id="4e516-228">This should be enabled by default.</span></span>
9. <span data-ttu-id="4e516-229">開啟 PowerShell 視窗，然後執行下列命令的 hello: ```Set-AdfsProperties -AuditLevel Verbose```。</span><span class="sxs-lookup"><span data-stu-id="4e516-229">Open a PowerShell window and run hello following command: ```Set-AdfsProperties -AuditLevel Verbose```.</span></span>

<span data-ttu-id="4e516-230">請注意，預設會啟用「基本」稽核層級。</span><span class="sxs-lookup"><span data-stu-id="4e516-230">Note that "basic" audit level is enabled by default.</span></span> <span data-ttu-id="4e516-231">深入了解 hello [Windows Server 2016 中的 AD FS 稽核增強功能](https://technet.microsoft.com/en-us/windows-server-docs/identity/ad-fs/operations/auditing-enhancements-to-ad-fs-in-windows-server-2016)</span><span class="sxs-lookup"><span data-stu-id="4e516-231">Read more about hello [AD FS Audit enhancement in Windows Server 2016](https://technet.microsoft.com/en-us/windows-server-docs/identity/ad-fs/operations/auditing-enhancements-to-ad-fs-in-windows-server-2016)</span></span>


#### <a name="toolocate-hello-ad-fs-audit-logs"></a><span data-ttu-id="4e516-232">toolocate hello AD FS 稽核記錄檔</span><span class="sxs-lookup"><span data-stu-id="4e516-232">toolocate hello AD FS audit logs</span></span>
1. <span data-ttu-id="4e516-233">開啟 [事件檢視器] 。</span><span class="sxs-lookup"><span data-stu-id="4e516-233">Open **Event Viewer**.</span></span>
2. <span data-ttu-id="4e516-234">移 tooWindows 記錄檔，然後選取**安全性**。</span><span class="sxs-lookup"><span data-stu-id="4e516-234">Go tooWindows Logs and select **Security**.</span></span>
3. <span data-ttu-id="4e516-235">在 hello 右邊，按一下 **篩選目前的記錄**。</span><span class="sxs-lookup"><span data-stu-id="4e516-235">On hello right, click **Filter Current Logs**.</span></span>
4. <span data-ttu-id="4e516-236">在 [事件來源] 下，選取 [AD FS 稽核] 。</span><span class="sxs-lookup"><span data-stu-id="4e516-236">Under Event Source, select **AD FS Auditing**.</span></span>

![AD FS 稽核記錄](./media/active-directory-aadconnect-health-requirements/adfsaudit.png)

> [!WARNING]
> <span data-ttu-id="4e516-238">群組原則可以停用 AD FS 稽核。</span><span class="sxs-lookup"><span data-stu-id="4e516-238">A group policy can disable AD FS auditing.</span></span> <span data-ttu-id="4e516-239">如果已停用 AD FS 稽核，則無法使用有關登入活動的使用量分析。</span><span class="sxs-lookup"><span data-stu-id="4e516-239">If AD FS auditing is disabled, usage analytics about login activities are not available.</span></span> <span data-ttu-id="4e516-240">確定您沒有可停用 AD FS 稽核的群組原則。</span><span class="sxs-lookup"><span data-stu-id="4e516-240">Ensure that you don’t have a group policy that  disables AD FS auditing.></span></span>
>


## <a name="installing-hello-azure-ad-connect-health-agent-for-sync"></a><span data-ttu-id="4e516-241">安裝 hello Azure AD Connect Health 代理程式進行同步</span><span class="sxs-lookup"><span data-stu-id="4e516-241">Installing hello Azure AD Connect Health agent for sync</span></span>
<span data-ttu-id="4e516-242">hello Azure AD Connect Health 代理程式同步處理會自動安裝在 Azure AD Connect hello 最新組建。</span><span class="sxs-lookup"><span data-stu-id="4e516-242">hello Azure AD Connect Health agent for sync is installed automatically in hello latest build of Azure AD Connect.</span></span> <span data-ttu-id="4e516-243">toouse Azure AD Connect 同步處理，您需要 toodownload hello 最新版的 Azure AD Connect 並安裝它。</span><span class="sxs-lookup"><span data-stu-id="4e516-243">toouse Azure AD Connect for sync, you need toodownload hello latest version of Azure AD Connect and install it.</span></span> <span data-ttu-id="4e516-244">您可以下載最新版本的 hello[這裡](http://www.microsoft.com/download/details.aspx?id=47594)。</span><span class="sxs-lookup"><span data-stu-id="4e516-244">You can download hello latest version [here](http://www.microsoft.com/download/details.aspx?id=47594).</span></span>

<span data-ttu-id="4e516-245">已安裝 tooverify hello 代理程式、 尋找 hello 遵循 hello 伺服器上的服務。</span><span class="sxs-lookup"><span data-stu-id="4e516-245">tooverify hello agent has been installed, look for hello following services on hello server.</span></span> <span data-ttu-id="4e516-246">如果您已完成 hello 組態，它們應該已執行。</span><span class="sxs-lookup"><span data-stu-id="4e516-246">If you completed hello configuration, they should already be running.</span></span> <span data-ttu-id="4e516-247">否則，它們會停止，直到 hello 設定已完成。</span><span class="sxs-lookup"><span data-stu-id="4e516-247">Otherwise, they are stopped until hello configuration is complete.</span></span>

* <span data-ttu-id="4e516-248">Azure AD Connect Health Sync Insights 服務</span><span class="sxs-lookup"><span data-stu-id="4e516-248">Azure AD Connect Health Sync Insights Service</span></span>
* <span data-ttu-id="4e516-249">Azure AD Connect Health Sync Monitoring 服務</span><span class="sxs-lookup"><span data-stu-id="4e516-249">Azure AD Connect Health Sync Monitoring Service</span></span>

![驗證適用於同步處理的 Azure AD Connect Health](./media/active-directory-aadconnect-health-sync/services.png)

> [!NOTE]
> <span data-ttu-id="4e516-251">請記住，使用 Azure AD Connect Health 需要 Azure AD Premium。</span><span class="sxs-lookup"><span data-stu-id="4e516-251">Remember that using Azure AD Connect Health requires Azure AD Premium.</span></span> <span data-ttu-id="4e516-252">如果您沒有 Azure AD Premium，您便無法 toocomplete hello Azure 入口網站中的 hello 組態。</span><span class="sxs-lookup"><span data-stu-id="4e516-252">If you do not have Azure AD Premium, you are unable toocomplete hello configuration in hello Azure portal.</span></span> <span data-ttu-id="4e516-253">如需詳細資訊，請參閱 hello[需求 頁面](active-directory-aadconnect-health-agent-install.md#requirements)。</span><span class="sxs-lookup"><span data-stu-id="4e516-253">For more information, see hello [requirements page](active-directory-aadconnect-health-agent-install.md#requirements).</span></span>
>
>

## <a name="manual-azure-ad-connect-health-for-sync-registration"></a><span data-ttu-id="4e516-254">手動 Azure AD Connect Health for Sync 註冊</span><span class="sxs-lookup"><span data-stu-id="4e516-254">Manual Azure AD Connect Health for Sync registration</span></span>
<span data-ttu-id="4e516-255">如果 hello Azure AD Connect Health 進行同步處理代理程式註冊失敗之後成功安裝 Azure AD Connect，您可以使用下列 PowerShell 命令 toomanually 註冊 hello 代理程式的 hello。</span><span class="sxs-lookup"><span data-stu-id="4e516-255">If hello Azure AD Connect Health for Sync agent registration fails after successfully installing Azure AD Connect, you can use hello following PowerShell command toomanually register hello agent.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="4e516-256">使用以下 PowerShell 命令，才需要之後安裝 Azure AD Connect 如果 hello 代理程式註冊失敗。</span><span class="sxs-lookup"><span data-stu-id="4e516-256">Using this PowerShell command is only required if hello agent registration fails after installing Azure AD Connect.</span></span>
>
>

<span data-ttu-id="4e516-257">hello 下列 PowerShell 命令需要只 hello 健全狀況代理程式註冊失敗時即使成功安裝及設定 Azure AD connect。</span><span class="sxs-lookup"><span data-stu-id="4e516-257">hello following PowerShell command is required ONLY when hello health agent registration fails even after a successful installation and configuration of Azure AD Connect.</span></span> <span data-ttu-id="4e516-258">hello Azure AD Connect Health 服務都啟動之後 hello 代理程式已順利註冊。</span><span class="sxs-lookup"><span data-stu-id="4e516-258">hello Azure AD Connect Health services will start after hello agent has been successfully registered.</span></span>

<span data-ttu-id="4e516-259">您可以手動註冊 hello Azure AD Connect Health 代理程式，使用下列 PowerShell 命令的 hello 的同步處理：</span><span class="sxs-lookup"><span data-stu-id="4e516-259">You can manually register hello Azure AD Connect Health agent for sync using hello following PowerShell command:</span></span>

`Register-AzureADConnectHealthSyncAgent -AttributeFiltering $false -StagingMode $false`

<span data-ttu-id="4e516-260">hello 命令會使用下列參數：</span><span class="sxs-lookup"><span data-stu-id="4e516-260">hello command takes following parameters:</span></span>

* <span data-ttu-id="4e516-261">AttributeFiltering: $true （預設）-如果 Azure AD Connect 不同步 hello 預設屬性集，而且已自訂的 toouse 已篩選的屬性集。</span><span class="sxs-lookup"><span data-stu-id="4e516-261">AttributeFiltering: $true (default) - if Azure AD Connect is not syncing hello default attribute set and has been customized toouse a filtered attribute set.</span></span> <span data-ttu-id="4e516-262">否則為 $false。</span><span class="sxs-lookup"><span data-stu-id="4e516-262">$false otherwise.</span></span>
* <span data-ttu-id="4e516-263">StagingMode: $false （預設）-如果 hello Azure AD Connect 的伺服器不在執行模式中，$true hello 伺服器是否設定 toobe 中預備模式。</span><span class="sxs-lookup"><span data-stu-id="4e516-263">StagingMode: $false (default) - if hello Azure AD Connect server is NOT in staging mode, $true if hello server is configured toobe in staging mode.</span></span>

<span data-ttu-id="4e516-264">當系統提示您輸入驗證您應該使用 hello 相同的全域管理員帳戶 (例如admin@domain.onmicrosoft.com) 用來設定 Azure AD Connect。</span><span class="sxs-lookup"><span data-stu-id="4e516-264">When prompted for authentication you should use hello same global admin account (such as admin@domain.onmicrosoft.com) that was used for configuring Azure AD Connect.</span></span>

## <a name="installing-hello-azure-ad-connect-health-agent-for-ad-ds"></a><span data-ttu-id="4e516-265">安裝 Azure AD Connect Health 代理程式用於 AD DS hello</span><span class="sxs-lookup"><span data-stu-id="4e516-265">Installing hello Azure AD Connect Health Agent for AD DS</span></span>
<span data-ttu-id="4e516-266">toostart hello 代理程式安裝中，按兩下您下載的 hello.exe 檔案。</span><span class="sxs-lookup"><span data-stu-id="4e516-266">toostart hello agent installation, double-click hello .exe file that you downloaded.</span></span> <span data-ttu-id="4e516-267">在 hello 第一個畫面上，按一下 安裝。</span><span class="sxs-lookup"><span data-stu-id="4e516-267">On hello first screen, click Install.</span></span>

![驗證 Azure AD Connect Health](./media/active-directory-aadconnect-health/aadconnect-health-adds-agent-install1.png)

<span data-ttu-id="4e516-269">一旦 hello 安裝完成時，按一下 [立即設定]。</span><span class="sxs-lookup"><span data-stu-id="4e516-269">Once hello installation is finished, click Configure Now.</span></span>

![驗證 Azure AD Connect Health](./media/active-directory-aadconnect-health/aadconnect-health-adds-agent-install2.png)

<span data-ttu-id="4e516-271">命令提示字元隨即啟動，然後再啟動可執行 PowerShell that executes Register-AzureADConnectHealthADDSAgent 的特定 PowerShell。</span><span class="sxs-lookup"><span data-stu-id="4e516-271">A command prompt is launched, followed by some PowerShell that executes Register-AzureADConnectHealthADDSAgent.</span></span> <span data-ttu-id="4e516-272">當提示的 toosign 中 tooAzure，請繼續並登入。</span><span class="sxs-lookup"><span data-stu-id="4e516-272">When prompted toosign in tooAzure, go ahead and sign in.</span></span>

![驗證 Azure AD Connect Health](./media/active-directory-aadconnect-health/aadconnect-health-adds-agent-install3.png)

<span data-ttu-id="4e516-274">登入後，PowerShell 將會繼續。</span><span class="sxs-lookup"><span data-stu-id="4e516-274">After signing in, PowerShell will continue.</span></span> <span data-ttu-id="4e516-275">在完成時，您可以關閉 PowerShell 和 hello 設定已完成。</span><span class="sxs-lookup"><span data-stu-id="4e516-275">Once it completes, you can close PowerShell and hello configuration is complete.</span></span>

<span data-ttu-id="4e516-276">此時，hello 服務應該自動允許 hello 代理程式 toomonitor 啟動，並收集資料。</span><span class="sxs-lookup"><span data-stu-id="4e516-276">At this point, hello services should be started automatically allowing hello agent toomonitor and gather data.</span></span> <span data-ttu-id="4e516-277">如果您有不符合所有 hello 先決條件 hello 上一節所述，在 hello PowerShell 視窗中會出現警告。</span><span class="sxs-lookup"><span data-stu-id="4e516-277">If you have not met all hello pre-requisites outlined in hello previous sections, warnings appear in hello PowerShell window.</span></span> <span data-ttu-id="4e516-278">要確定 toocomplete hello[需求](active-directory-aadconnect-health-agent-install.md#requirements)之前安裝 hello 代理程式。</span><span class="sxs-lookup"><span data-stu-id="4e516-278">Be sure toocomplete hello [requirements](active-directory-aadconnect-health-agent-install.md#requirements) before installing hello agent.</span></span> <span data-ttu-id="4e516-279">下列螢幕擷取畫面的 hello 是這些錯誤的範例。</span><span class="sxs-lookup"><span data-stu-id="4e516-279">hello following screenshot is an example of these errors.</span></span>

![驗證適用於 AD DS 的 Azure AD Connect Health](./media/active-directory-aadconnect-health/aadconnect-health-adds-agent-install4.png)

<span data-ttu-id="4e516-281">已安裝 tooverify hello 代理程式、 尋找 hello 遵循 hello 網域控制站上的服務。</span><span class="sxs-lookup"><span data-stu-id="4e516-281">tooverify hello agent has been installed, look for hello following services on hello domain controller.</span></span>

* <span data-ttu-id="4e516-282">Azure AD Connect Health AD DS Insights 服務</span><span class="sxs-lookup"><span data-stu-id="4e516-282">Azure AD Connect Health AD DS Insights Service</span></span>
* <span data-ttu-id="4e516-283">Azure AD Connect Health AD DS 監視服務</span><span class="sxs-lookup"><span data-stu-id="4e516-283">Azure AD Connect Health AD DS Monitoring Service</span></span>

<span data-ttu-id="4e516-284">如果您已完成 hello 組態時，應該已經在執行這些服務。</span><span class="sxs-lookup"><span data-stu-id="4e516-284">If you completed hello configuration, these services should already be running.</span></span> <span data-ttu-id="4e516-285">否則，它們會停止，直到 hello 設定已完成。</span><span class="sxs-lookup"><span data-stu-id="4e516-285">Otherwise, they are stopped until hello configuration is complete.</span></span>

![驗證 Azure AD Connect Health](./media/active-directory-aadconnect-health/aadconnect-health-adds-agent-install5.png)


### <a name="agent-registration-using-powershell"></a><span data-ttu-id="4e516-287">使用 PowerShell 進行代理程式註冊</span><span class="sxs-lookup"><span data-stu-id="4e516-287">Agent Registration using PowerShell</span></span>
<span data-ttu-id="4e516-288">安裝之後 hello 適當的代理程式的 setup.exe，您可以執行使用下列 PowerShell 命令，視 hello 角色而定的 hello hello 代理程式註冊步驟。</span><span class="sxs-lookup"><span data-stu-id="4e516-288">After installing hello appropriate agent setup.exe, you can perform hello agent registration step using hello following PowerShell commands depending on hello role.</span></span> <span data-ttu-id="4e516-289">開啟 PowerShell 視窗，然後執行 hello 適當的命令：</span><span class="sxs-lookup"><span data-stu-id="4e516-289">Open a PowerShell Window and execute hello appropriate command:</span></span>

```
    Register-AzureADConnectHealthADFSAgent
    Register-AzureADConnectHealthADDSAgent
    Register-AzureADConnectHealthSyncAgent

```

<span data-ttu-id="4e516-290">這些命令會接受"Credential"參數 toocomplete hello 註冊為非互動方式或 Server Core 電腦上。</span><span class="sxs-lookup"><span data-stu-id="4e516-290">These commands accept "Credential" as a parameter toocomplete hello registration in a non-interactive manner or on a Server-Core machine.</span></span>
* <span data-ttu-id="4e516-291">hello 認證可以傳遞做為參數的 PowerShell 變數中擷取。</span><span class="sxs-lookup"><span data-stu-id="4e516-291">hello Credential can be captured in a PowerShell variable that is passed as a parameter.</span></span>
* <span data-ttu-id="4e516-292">您可以提供任何 Azure AD 身分識別，其中擁有存取 tooregister hello 代理程式，而且沒有啟用 MFA。</span><span class="sxs-lookup"><span data-stu-id="4e516-292">You can provide any Azure AD Identity that has access tooregister hello agents and does NOT have MFA enabled.</span></span>
* <span data-ttu-id="4e516-293">預設全域系統管理員可以存取 tooperform 代理程式註冊。</span><span class="sxs-lookup"><span data-stu-id="4e516-293">By default Global Admins have access tooperform agent registration.</span></span> <span data-ttu-id="4e516-294">您也可以讓其他特殊權限的身分識別 tooperform 小於此步驟。</span><span class="sxs-lookup"><span data-stu-id="4e516-294">You can also allow other less privileged identities tooperform this step.</span></span> <span data-ttu-id="4e516-295">深入了解[角色型存取控制](active-directory-aadconnect-health-operations.md#manage-access-with-role-based-access-control)。</span><span class="sxs-lookup"><span data-stu-id="4e516-295">Read more about [Role Based Access Control](active-directory-aadconnect-health-operations.md#manage-access-with-role-based-access-control).</span></span>

```
    $cred = Get-Credential
    Register-AzureADConnectHealthADFSAgent -Credential $cred

```

## <a name="configure-azure-ad-connect-health-agents-toouse-http-proxy"></a><span data-ttu-id="4e516-296">設定 Azure AD Connect Health 代理程式 toouse HTTP Proxy</span><span class="sxs-lookup"><span data-stu-id="4e516-296">Configure Azure AD Connect Health Agents toouse HTTP Proxy</span></span>
<span data-ttu-id="4e516-297">您可以設定 Azure AD Connect Health 代理程式 toowork 透過 HTTP Proxy。</span><span class="sxs-lookup"><span data-stu-id="4e516-297">You can configure Azure AD Connect Health Agents toowork with an HTTP Proxy.</span></span>

> [!NOTE]
> * <span data-ttu-id="4e516-298">不支援使用"Netsh WinHttp set ProxyServerAddress"，因為 hello 代理程式使用 System.Net toomake web 要求，而不是 Microsoft Windows HTTP 服務。</span><span class="sxs-lookup"><span data-stu-id="4e516-298">Using “Netsh WinHttp set ProxyServerAddress” is not supported as hello agent uses System.Net toomake web requests instead of Microsoft Windows HTTP Services.</span></span>
> * <span data-ttu-id="4e516-299">hello 設定的 Http Proxy 位址不使用的 toopass 透過加密的 Https 訊息。</span><span class="sxs-lookup"><span data-stu-id="4e516-299">hello configured Http Proxy address is used toopass-through encrypted Https messages.</span></span>
> * <span data-ttu-id="4e516-300">不支援已驗證的 Proxy (使用 HTTPBasic)。</span><span class="sxs-lookup"><span data-stu-id="4e516-300">Authenticated proxies (using HTTPBasic) are not supported.</span></span>
>
>

### <a name="change-health-agent-proxy-configuration"></a><span data-ttu-id="4e516-301">變更健康情況代理程式 Proxy 組態</span><span class="sxs-lookup"><span data-stu-id="4e516-301">Change Health Agent Proxy Configuration</span></span>
<span data-ttu-id="4e516-302">您有下列選項 tooconfigure Azure AD Connect Health 代理程式 toouse HTTP Proxy 的 hello。</span><span class="sxs-lookup"><span data-stu-id="4e516-302">You have hello following options tooconfigure Azure AD Connect Health Agent toouse an HTTP Proxy.</span></span>

> [!NOTE]
> <span data-ttu-id="4e516-303">所有的 Azure AD Connect Health 代理程式服務必須重新啟動，為了讓 hello proxy 設定 toobe 更新。</span><span class="sxs-lookup"><span data-stu-id="4e516-303">All Azure AD Connect Health Agent services must be restarted, in order for hello proxy settings toobe updated.</span></span> <span data-ttu-id="4e516-304">執行下列命令的 hello:</span><span class="sxs-lookup"><span data-stu-id="4e516-304">Run hello following command:</span></span><br>
> <span data-ttu-id="4e516-305">Restart-Service AdHealth*</span><span class="sxs-lookup"><span data-stu-id="4e516-305">Restart-Service AdHealth*</span></span>
>
>

#### <a name="import-existing-proxy-settings"></a><span data-ttu-id="4e516-306">匯入現有的 Proxy 設定</span><span class="sxs-lookup"><span data-stu-id="4e516-306">Import existing proxy Settings</span></span>
##### <a name="import-from-internet-explorer"></a><span data-ttu-id="4e516-307">從 Internet Explorer 匯入</span><span class="sxs-lookup"><span data-stu-id="4e516-307">Import from Internet Explorer</span></span>
<span data-ttu-id="4e516-308">可以匯入 Internet Explorer HTTP proxy 設定，toobe 由 hello Azure AD Connect Health 代理程式。</span><span class="sxs-lookup"><span data-stu-id="4e516-308">Internet Explorer HTTP proxy settings can be imported, toobe used by hello Azure AD Connect Health Agents.</span></span> <span data-ttu-id="4e516-309">每個執行 hello 健康情況代理程式的 hello 伺服器上執行下列 PowerShell 命令的 hello:</span><span class="sxs-lookup"><span data-stu-id="4e516-309">On each of hello servers running hello Health agent, execute hello following PowerShell command:</span></span>

    Set-AzureAdConnectHealthProxySettings -ImportFromInternetSettings

##### <a name="import-from-winhttp"></a><span data-ttu-id="4e516-310">從 WinHTTP 匯入</span><span class="sxs-lookup"><span data-stu-id="4e516-310">Import from WinHTTP</span></span>
<span data-ttu-id="4e516-311">WinHTTP proxy 設定可匯入，toobe 由 hello Azure AD Connect Health 代理程式。</span><span class="sxs-lookup"><span data-stu-id="4e516-311">WinHTTP proxy settings can be imported, toobe used by hello Azure AD Connect Health Agents.</span></span> <span data-ttu-id="4e516-312">每個執行 hello 健康情況代理程式的 hello 伺服器上執行下列 PowerShell 命令的 hello:</span><span class="sxs-lookup"><span data-stu-id="4e516-312">On each of hello servers running hello Health agent, execute hello following PowerShell command:</span></span>

    Set-AzureAdConnectHealthProxySettings -ImportFromWinHttp

#### <a name="specify-proxy-addresses-manually"></a><span data-ttu-id="4e516-313">以手動方式指定 Proxy 位址</span><span class="sxs-lookup"><span data-stu-id="4e516-313">Specify Proxy addresses manually</span></span>
<span data-ttu-id="4e516-314">您可以在每部執行 hello 健康情況代理程式，藉由執行下列 PowerShell 命令的 hello hello 伺服器上手動指定 proxy 伺服器：</span><span class="sxs-lookup"><span data-stu-id="4e516-314">You can manually specify a proxy server on each of hello servers running hello Health Agent, by executing hello following PowerShell command:</span></span>

    Set-AzureAdConnectHealthProxySettings -HttpsProxyAddress address:port

<span data-ttu-id="4e516-315">範例：*Set-AzureAdConnectHealthProxySettings -HttpsProxyAddress myproxyserver: 443*</span><span class="sxs-lookup"><span data-stu-id="4e516-315">Example: *Set-AzureAdConnectHealthProxySettings -HttpsProxyAddress myproxyserver: 443*</span></span>

* <span data-ttu-id="4e516-316">「位址」可以是可解析的 DNS 伺服器名稱或 IPv4 位址</span><span class="sxs-lookup"><span data-stu-id="4e516-316">"address" can be a DNS resolvable server name or an IPv4 address</span></span>
* <span data-ttu-id="4e516-317">「連接埠」可以省略。</span><span class="sxs-lookup"><span data-stu-id="4e516-317">"port" can be omitted.</span></span> <span data-ttu-id="4e516-318">如果省略，則會選擇 443 做為預設連接埠。</span><span class="sxs-lookup"><span data-stu-id="4e516-318">If omitted then 443 is chosen as default port.</span></span>

#### <a name="clear-existing-proxy-configuration"></a><span data-ttu-id="4e516-319">清除現有的 Proxy 設定</span><span class="sxs-lookup"><span data-stu-id="4e516-319">Clear existing proxy configuration</span></span>
<span data-ttu-id="4e516-320">您可以藉由執行下列命令的 hello 清除 hello 現有的 proxy 設定：</span><span class="sxs-lookup"><span data-stu-id="4e516-320">You can clear hello existing proxy configuration by running hello following command:</span></span>

    Set-AzureAdConnectHealthProxySettings -NoProxy


### <a name="read-current-proxy-settings"></a><span data-ttu-id="4e516-321">讀取目前的 Proxy 設定</span><span class="sxs-lookup"><span data-stu-id="4e516-321">Read current proxy settings</span></span>
<span data-ttu-id="4e516-322">您可以藉由執行下列命令的 hello 閱讀 hello 目前設定的 proxy 設定：</span><span class="sxs-lookup"><span data-stu-id="4e516-322">You can read hello currently configured proxy settings by running hello following command:</span></span>

    Get-AzureAdConnectHealthProxySettings


## <a name="test-connectivity-tooazure-ad-connect-health-service"></a><span data-ttu-id="4e516-323">測試連線 tooAzure AD Connect Health 服務</span><span class="sxs-lookup"><span data-stu-id="4e516-323">Test Connectivity tooAzure AD Connect Health Service</span></span>
<span data-ttu-id="4e516-324">有可能的問題可能會發生與 hello Azure AD Connect Health 服務 toolose 連線導致 hello Azure AD Connect Health 代理程式。</span><span class="sxs-lookup"><span data-stu-id="4e516-324">It is possible that issues may arise that cause hello Azure AD Connect Health agent toolose connectivity with hello Azure AD Connect Health service.</span></span> <span data-ttu-id="4e516-325">這些包括網路問題、權限問題或各種其他原因。</span><span class="sxs-lookup"><span data-stu-id="4e516-325">These include network issues, permission issues, or various other reasons.</span></span>

<span data-ttu-id="4e516-326">如果 hello 代理程式無法 toosend 資料 toohello Azure AD Connect Health 服務的時間超過兩小時，其中會顯示以 hello 遵循 hello 入口網站中的警示: 「 健全狀況服務的資料不是向上 toodate。 」</span><span class="sxs-lookup"><span data-stu-id="4e516-326">If hello agent is unable toosend data toohello Azure AD Connect Health service for longer than two hours, it is indicated with hello following alert in hello portal: "Health Service data is not up toodate."</span></span> <span data-ttu-id="4e516-327">您可以確認受影響的 hello Azure AD Connect Health 代理程式是否能 tooupload 資料 toohello Azure AD Connect Health 服務藉由執行下列 PowerShell 命令的 hello:</span><span class="sxs-lookup"><span data-stu-id="4e516-327">You can confirm if hello affected Azure AD Connect Health agent is able tooupload data toohello Azure AD Connect Health service by running hello following PowerShell command:</span></span>

    Test-AzureADConnectHealthConnectivity -Role ADFS

<span data-ttu-id="4e516-328">hello 角色參數目前只接受下列值的 hello:</span><span class="sxs-lookup"><span data-stu-id="4e516-328">hello role parameter currently takes hello following values:</span></span>

* <span data-ttu-id="4e516-329">ADFS</span><span class="sxs-lookup"><span data-stu-id="4e516-329">ADFS</span></span>
* <span data-ttu-id="4e516-330">Sync</span><span class="sxs-lookup"><span data-stu-id="4e516-330">Sync</span></span>
* <span data-ttu-id="4e516-331">ADDS</span><span class="sxs-lookup"><span data-stu-id="4e516-331">ADDS</span></span>

<span data-ttu-id="4e516-332">您可以在 hello 命令 tooview 使用 hello-ShowResults 旗標的詳細記錄檔。</span><span class="sxs-lookup"><span data-stu-id="4e516-332">You can use hello -ShowResults flag in hello command tooview detailed logs.</span></span> <span data-ttu-id="4e516-333">下列範例使用 hello:</span><span class="sxs-lookup"><span data-stu-id="4e516-333">Use hello following example:</span></span>

    Test-AzureADConnectHealthConnectivity -Role Sync -ShowResult

> [!NOTE]
> <span data-ttu-id="4e516-334">toouse hello 連線工具，您必須第一個完成的 hello 代理程式註冊。</span><span class="sxs-lookup"><span data-stu-id="4e516-334">toouse hello connectivity tool, you must first complete hello agent registration.</span></span> <span data-ttu-id="4e516-335">如果您不能 toocomplete hello 代理程式註冊，請確定您已符合所有 hello[需求](active-directory-aadconnect-health-agent-install.md#requirements)有關 Azure AD Connect Health。</span><span class="sxs-lookup"><span data-stu-id="4e516-335">If you are not able toocomplete hello agent registration, make sure that you have met all hello [requirements](active-directory-aadconnect-health-agent-install.md#requirements) for Azure AD Connect Health.</span></span> <span data-ttu-id="4e516-336">這項連線測試預設是在代理程式註冊期間執行。</span><span class="sxs-lookup"><span data-stu-id="4e516-336">This connectivity test is performed by default during agent registration.</span></span>
>
>

## <a name="related-links"></a><span data-ttu-id="4e516-337">相關連結</span><span class="sxs-lookup"><span data-stu-id="4e516-337">Related links</span></span>
* [<span data-ttu-id="4e516-338">Azure AD Connect Health</span><span class="sxs-lookup"><span data-stu-id="4e516-338">Azure AD Connect Health</span></span>](active-directory-aadconnect-health.md)
* [<span data-ttu-id="4e516-339">Azure AD Connect Health 操作</span><span class="sxs-lookup"><span data-stu-id="4e516-339">Azure AD Connect Health Operations</span></span>](active-directory-aadconnect-health-operations.md)
* [<span data-ttu-id="4e516-340">在 AD FS 使用 Azure AD Connect Health</span><span class="sxs-lookup"><span data-stu-id="4e516-340">Using Azure AD Connect Health with AD FS</span></span>](active-directory-aadconnect-health-adfs.md)
* [<span data-ttu-id="4e516-341">使用 Azure AD Connect Health 進行同步處理</span><span class="sxs-lookup"><span data-stu-id="4e516-341">Using Azure AD Connect Health for sync</span></span>](active-directory-aadconnect-health-sync.md)
* [<span data-ttu-id="4e516-342">在 AD DS 使用 Azure AD Connect Health</span><span class="sxs-lookup"><span data-stu-id="4e516-342">Using Azure AD Connect Health with AD DS</span></span>](active-directory-aadconnect-health-adds.md)
* [<span data-ttu-id="4e516-343">Azure AD Connect Health 常見問題集</span><span class="sxs-lookup"><span data-stu-id="4e516-343">Azure AD Connect Health FAQ</span></span>](active-directory-aadconnect-health-faq.md)
* [<span data-ttu-id="4e516-344">Azure AD Connect Health 版本歷程記錄</span><span class="sxs-lookup"><span data-stu-id="4e516-344">Azure AD Connect Health Version History</span></span>](active-directory-aadconnect-health-version-history.md)
