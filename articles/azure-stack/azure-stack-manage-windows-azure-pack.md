---
title: "從 Azure Stack 管理 Windows Azure 套件虛擬機器 | Microsoft Docs"
description: "了解如何從 Azure Stack 中的使用者入口網站管理 Windows Azure 套件 (WAP) VM。"
services: azure-stack
documentationcenter: 
author: walterov
manager: byronr
editor: 
ms.assetid: 213c2792-d404-4b44-8340-235adf3f8f0b
ms.service: azure-stack
ms.workload: na
pms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/10/2017
ms.author: walterov
ms.openlocfilehash: e00cf1c3f3d74b98e84b3d3f862e3a7b1b5b65f4
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="manage-windows-azure-pack-virtual-machines-from-azure-stack"></a><span data-ttu-id="00048-103">從 Azure Stack 管理 Windows Azure 套件虛擬機器</span><span class="sxs-lookup"><span data-stu-id="00048-103">Manage Windows Azure Pack virtual machines from Azure Stack</span></span>
<span data-ttu-id="00048-104">在 Azure Stack 開發套件環境中，您可以從 Azure Stack 使用者入口網站中，啟用在 Windows Azure 套件上所執行租用戶虛擬機器的存取權。</span><span class="sxs-lookup"><span data-stu-id="00048-104">In the Azure Stack Development Kit, you can enable access from the Azure Stack user portal to tenant virtual machines running on Windows Azure Pack.</span></span> <span data-ttu-id="00048-105">租用戶可以使用 Azure Stack 入口網站來管理其現有的 IaaS 虛擬機器和虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="00048-105">Tenants can use the Azure Stack portal to manage their existing IaaS virtual machines and virtual networks.</span></span> <span data-ttu-id="00048-106">這些資源都可以透過基礎的 Service Provider Foundation (SPF) 和 Virtual Machine Manager (VMM) 元件，在 Windows Azure 套件上使用。</span><span class="sxs-lookup"><span data-stu-id="00048-106">These resources are made available on Windows Azure Pack through the underlying Service Provider Foundation (SPF) and Virtual Machine Manager (VMM) components.</span></span> <span data-ttu-id="00048-107">具體而言，租用戶可以：</span><span class="sxs-lookup"><span data-stu-id="00048-107">Specifically, tenants can:</span></span>

* <span data-ttu-id="00048-108">瀏覽資源</span><span class="sxs-lookup"><span data-stu-id="00048-108">Browse resources</span></span>
* <span data-ttu-id="00048-109">檢查設定值</span><span class="sxs-lookup"><span data-stu-id="00048-109">Examine configuration values</span></span>
* <span data-ttu-id="00048-110">停止或啟動虛擬機器</span><span class="sxs-lookup"><span data-stu-id="00048-110">Stop or start a virtual machine</span></span>
* <span data-ttu-id="00048-111">透過遠端桌面通訊協定 (RDP) 連線到虛擬機器</span><span class="sxs-lookup"><span data-stu-id="00048-111">Connect to a virtual machine through Remote Desktop Protocol (RDP)</span></span>
* <span data-ttu-id="00048-112">建立和管理檢查點</span><span class="sxs-lookup"><span data-stu-id="00048-112">Create and manage checkpoints</span></span>
* <span data-ttu-id="00048-113">刪除虛擬機器和虛擬網路</span><span class="sxs-lookup"><span data-stu-id="00048-113">Delete virtual machines and virtual networks</span></span>

<span data-ttu-id="00048-114">此功能是由適用於 Azure Stack 的 Windows Azure 套件連接器所提供 (預覽)。</span><span class="sxs-lookup"><span data-stu-id="00048-114">This functionality is provided by the Windows Azure Pack Connector for Azure Stack (Preview).</span></span> <span data-ttu-id="00048-115">本文示範如何設定適用於單一節點 Azure Stack 環境的連接器。</span><span class="sxs-lookup"><span data-stu-id="00048-115">This article shows how to configure the connector for a single-node Azure Stack environment.</span></span>

<span data-ttu-id="00048-116">針對此預覽版本的連接器，請注意以下事項：</span><span class="sxs-lookup"><span data-stu-id="00048-116">For this preview release of the connector, be aware of the following:</span></span>
* <span data-ttu-id="00048-117">請僅在測試環境中使用 Windows Azure 套件連接器 (針對 Azure Stack 和 Windows Azure 套件)，而不要在生產環境部署中使用。</span><span class="sxs-lookup"><span data-stu-id="00048-117">Use the Windows Azure Pack Connector only in test environments (for both Azure Stack and Windows Azure Pack), and not in production deployments.</span></span>
* <span data-ttu-id="00048-118">您必須擁有 Windows Azure 套件更新彙總套件 (UR) 9.1 或更新版本，以及 System Center SPF 和 VMM UR 9 或更新版本。</span><span class="sxs-lookup"><span data-stu-id="00048-118">You must have Windows Azure Pack Update Rollup (UR) 9.1 or later and System Center SPF and VMM UR 9 or later.</span></span>
* <span data-ttu-id="00048-119">VMM 和 SPF 元件可以是 System Center 2012 R2 或 System Center 2016。</span><span class="sxs-lookup"><span data-stu-id="00048-119">The VMM and SPF components can be either System Center 2012 R2 or System Center 2016.</span></span>
* <span data-ttu-id="00048-120">您必須在 Azure Stack 和 Windows Azure 套件都執行設定步驟。</span><span class="sxs-lookup"><span data-stu-id="00048-120">You must perform configuration steps on both Azure Stack and on Windows Azure Pack.</span></span>
* <span data-ttu-id="00048-121">此指示適用於非雲端平台系統 (CPS) 環境。</span><span class="sxs-lookup"><span data-stu-id="00048-121">The instructions apply to non-Cloud Platform System (CPS) environments.</span></span>
* <span data-ttu-id="00048-122">若要檢閱已知的問題，請參閱 [Microsoft Azure Stack 疑難排解](azure-stack-troubleshooting.md)。</span><span class="sxs-lookup"><span data-stu-id="00048-122">To review the known issues, see [Microsoft Azure Stack troubleshooting](azure-stack-troubleshooting.md).</span></span>


## <a name="architecture"></a><span data-ttu-id="00048-123">架構</span><span class="sxs-lookup"><span data-stu-id="00048-123">Architecture</span></span>
<span data-ttu-id="00048-124">下圖顯示 Windows Azure 套件連接器的主要元件。</span><span class="sxs-lookup"><span data-stu-id="00048-124">The following diagram shows the main components of the Windows Azure Pack Connector.</span></span>

![Windows Azure 套件連接器元件](media/azure-stack-manage-wap/image1.png)

<span data-ttu-id="00048-126">請注意下列詳細資料：</span><span class="sxs-lookup"><span data-stu-id="00048-126">Notice the following details:</span></span>
* <span data-ttu-id="00048-127">Azure Stack 使用者入口網站會從這兩個雲端 (Azure Stack 和 Windows Azure 套件) 存取資源資訊。</span><span class="sxs-lookup"><span data-stu-id="00048-127">The Azure Stack user portal accesses the resource information from both clouds (Azure Stack and Windows Azure Pack).</span></span>
* <span data-ttu-id="00048-128">使用者必須具有在這兩種環境中都有效的帳戶。</span><span class="sxs-lookup"><span data-stu-id="00048-128">The user must have an account that is valid in both environments.</span></span>
* <span data-ttu-id="00048-129">Azure Stack 使用者入口網站必須具有在 Windows Azure 套件上所執行元件的網路存取權。</span><span class="sxs-lookup"><span data-stu-id="00048-129">The Azure Stack user portal must have network access to the components running on Windows Azure Pack.</span></span>
* <span data-ttu-id="00048-130">在圖表中的 **WAP** 區段，您可以看到新的 Windows Azure 套件連接器模組 (WAP 擴充功能和連接器) 以及包含 SPF 和 VMM 元件的現有 Windows Azure 套件租用戶 API。</span><span class="sxs-lookup"><span data-stu-id="00048-130">In the **WAP** section of the diagram, you can see the new Windows Azure Pack Connector modules (WAP Extension and Connector) and the existing Windows Azure Pack Tenant API with SPF and VMM components.</span></span>


## <a name="identity-management"></a><span data-ttu-id="00048-131">身分識別管理</span><span class="sxs-lookup"><span data-stu-id="00048-131">Identity management</span></span>
<span data-ttu-id="00048-132">Windows Azure 套件租用戶 API 必須信任 Azure Stack 安全性權杖服務 (STS)。</span><span class="sxs-lookup"><span data-stu-id="00048-132">The Windows Azure Pack Tenant API must trust the Azure Stack security token service (STS).</span></span>

<span data-ttu-id="00048-133">當使用者透過 Azure Stack 入口網站執行目標為 Windows Azure 套件資源的動作時，入口網站會使用 Windows Azure 套件租用戶 API。</span><span class="sxs-lookup"><span data-stu-id="00048-133">When a user performs an action through the Azure Stack portal that targets Windows Azure Pack resources, the portal uses the Windows Azure Pack Tenant API.</span></span> <span data-ttu-id="00048-134">因此，提供的使用者驗證權杖必須來自受信任的 STS。</span><span class="sxs-lookup"><span data-stu-id="00048-134">Therefore, the provided user authentication token must come from a trusted STS.</span></span> <span data-ttu-id="00048-135">請參閱下圖：</span><span class="sxs-lookup"><span data-stu-id="00048-135">See the following diagram:</span></span>

![Windows Azure 套件連接器驗證的圖表](media/azure-stack-manage-wap/image2.png)

<span data-ttu-id="00048-137">在開發套件環境中，Windows Azure 套件和 Azure Stack 具有獨立的識別提供者。</span><span class="sxs-lookup"><span data-stu-id="00048-137">In the development kit environment, Windows Azure Pack and Azure Stack have independent identity providers.</span></span> <span data-ttu-id="00048-138">從 Azure Stack 入口網站存取這兩種環境的使用者，在這兩個識別提供者中使用者主體名稱 (UPN) 的名稱必須相同。</span><span class="sxs-lookup"><span data-stu-id="00048-138">Users who access both environments from the Azure Stack portal must have the same user principal name (UPN) name in both identity providers.</span></span> <span data-ttu-id="00048-139">例如，帳戶 *azurestackadmin@azurestack.local* 在 Windows Azure 套件的 STS 中也應存在。</span><span class="sxs-lookup"><span data-stu-id="00048-139">For example, the account *azurestackadmin@azurestack.local* should also exist in the STS for Windows Azure Pack.</span></span> <span data-ttu-id="00048-140">若 AD FS 未設定為支援連出的信任關係，您會從 Windows Azure 套件元件 (租用戶 API) 建立對 AD FS Azure Stack 執行個體的信任。</span><span class="sxs-lookup"><span data-stu-id="00048-140">Where AD FS is not set up to support outbound trust relationships, you will establish trust from the Windows Azure Pack components (Tenant API) to the Azure Stack instance of AD FS.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="00048-141">必要條件</span><span class="sxs-lookup"><span data-stu-id="00048-141">Prerequisites</span></span>

### <a name="download-the-windows-azure-pack-connector"></a><span data-ttu-id="00048-142">下載 Windows Azure 套件連接器</span><span class="sxs-lookup"><span data-stu-id="00048-142">Download the Windows Azure Pack Connector</span></span>
<span data-ttu-id="00048-143">在 [Microsoft 下載中心](https://aka.ms/wapconnectorazurestackdlc)下載 .exe 檔案，並將其解壓縮到本機電腦。</span><span class="sxs-lookup"><span data-stu-id="00048-143">On the [Microsoft Download Center](https://aka.ms/wapconnectorazurestackdlc), download the .exe file and extract it to your local computer.</span></span> <span data-ttu-id="00048-144">稍後，您要將內容複製到可以存取您 Windows Azure 套件環境的電腦。</span><span class="sxs-lookup"><span data-stu-id="00048-144">Later, you copy the contents to a computer that can access your Windows Azure Pack environment.</span></span>

### <a name="deployment-option-requirement"></a><span data-ttu-id="00048-145">部署選項需求</span><span class="sxs-lookup"><span data-stu-id="00048-145">Deployment option requirement</span></span>
<span data-ttu-id="00048-146">為了與 Windows Azure 套件整合，您可以使用 AD FS 選項或 Azure Active Directory 選項來部署 Azure Stack。</span><span class="sxs-lookup"><span data-stu-id="00048-146">To integrate with Windows Azure Pack, you can deploy Azure Stack by using the AD FS option or the Azure Active Directory option.</span></span>

### <a name="connectivity-requirements"></a><span data-ttu-id="00048-147">連線能力需求</span><span class="sxs-lookup"><span data-stu-id="00048-147">Connectivity requirements</span></span>
1. <span data-ttu-id="00048-148">請從可存取 Azure Stack 使用者入口網站的電腦，確定您可以透過網頁瀏覽器來存取 Windows Azure 套件租用戶入口網站。</span><span class="sxs-lookup"><span data-stu-id="00048-148">From the computer on which you access the Azure Stack user portal, make sure that you can access the Windows Azure Pack tenant portal through the web browser.</span></span>
2. <span data-ttu-id="00048-149">Azure Stack 上的 AzS-WASP01 虛擬機器必須能夠連線到 Windows Azure 套件租用戶入口網站的電腦。</span><span class="sxs-lookup"><span data-stu-id="00048-149">The AzS-WASP01 virtual machine on Azure Stack must be able to connect to the Windows Azure Pack tenant portal computer.</span></span> <span data-ttu-id="00048-150">請使用 Ping.exe 驗證網路連線能力。</span><span class="sxs-lookup"><span data-stu-id="00048-150">Use Ping.exe to verify network connectivity.</span></span> 
3.  <span data-ttu-id="00048-151">您必須擁有新連接器服務的有效憑證。</span><span class="sxs-lookup"><span data-stu-id="00048-151">You must have valid certificates for the new Connector services.</span></span> <span data-ttu-id="00048-152">這些 SSL 憑證必須由受信任的憑證授權單位 (CA) 發行。</span><span class="sxs-lookup"><span data-stu-id="00048-152">These SSL certificates must be issued by a trusted certification authority (CA).</span></span> <span data-ttu-id="00048-153">您不得使用自我簽署的憑證。</span><span class="sxs-lookup"><span data-stu-id="00048-153">You can't use self-signed certificates.</span></span> <span data-ttu-id="00048-154">Azure Stack (尤其是 AzS-WASP01 VM) 和任何其他租用戶可用來存取 Azure Stack 使用者入口網站的電腦，都必須信任該 SSL 憑證。</span><span class="sxs-lookup"><span data-stu-id="00048-154">The SSL certificates must be trusted by Azure Stack (specifically the AzS-WASP01 VM) and any other computer that the tenant may use to access the Azure Stack user portal.</span></span>
 
    >[!NOTE]
    <span data-ttu-id="00048-155">由於 AzS-WASP01 會執行包含伺服器核心安裝選項的 Windows Server，因此您可以使用命令列工具 (例如 Certutil.ext) 來匯入憑證。</span><span class="sxs-lookup"><span data-stu-id="00048-155">Because AzS-WASP01 runs Windows Server with the Server Core installation option, you can use a command-line tool such as Certutil.ext to import the certificate.</span></span> <span data-ttu-id="00048-156">例如，您可將 .cer 檔案複製到 AzS-WASP01 的 c:\temp 上，並執行命令 **certutil -addstore "CA" "c:\temp\certname.cer"**。</span><span class="sxs-lookup"><span data-stu-id="00048-156">For example, you could copy the .cer file to c:\temp on AzS-WASP01, and then run the command **certutil -addstore "CA" "c:\temp\certname.cer"**.</span></span>

4.  <span data-ttu-id="00048-157">若要透過 Azure Stack 入口網站建立到 Windows Azure 套件租用戶虛擬機器的 RDP 連線，Windows Azure 套件環境必須允許到租用戶虛擬機器的遠端桌面流量。</span><span class="sxs-lookup"><span data-stu-id="00048-157">To establish RDP connectivity to Windows Azure Pack tenant virtual machines through the Azure Stack portal, the Windows Azure Pack environment must allow Remote Desktop traffic to the tenant VMs.</span></span>
5.  <span data-ttu-id="00048-158">針對 Azure Stack 疊租用戶虛擬機器與 Windows Azure 套件租用戶虛擬機器之間的連線，它們的外部 IP 位址必須可跨兩個環境路由傳送。</span><span class="sxs-lookup"><span data-stu-id="00048-158">For connectivity between Azure Stack tenant virtual machines and Windows Azure Pack tenant virtual machines, their external IP addresses must be routable across the two environments.</span></span> <span data-ttu-id="00048-159">這種連線能力也可能包括建立 DNS 伺服器的關聯，以解析在環境之間的虛擬機器名稱。</span><span class="sxs-lookup"><span data-stu-id="00048-159">This connectivity could also include associating a DNS server to resolve virtual machine names between the environments.</span></span>

### <a name="iis-requirements"></a><span data-ttu-id="00048-160">IIS 需求</span><span class="sxs-lookup"><span data-stu-id="00048-160">IIS requirements</span></span>
<span data-ttu-id="00048-161">裝載 Windows Azure 套件租用戶入口網站的電腦 (這可能是實體主機、一部虛擬機器或多部虛擬機器) 必須安裝 URL 重寫 IIS 擴充功能。</span><span class="sxs-lookup"><span data-stu-id="00048-161">The computer that hosts the Windows Azure Pack tenant portal (which may be a physical host, a virtual machine, or multiple virtual machines) must have the URL Rewrite IIS extension installed.</span></span> <span data-ttu-id="00048-162">如果尚未安裝，您可以從[這裡](https://www.iis.net/downloads/microsoft/url-rewrite)下載。</span><span class="sxs-lookup"><span data-stu-id="00048-162">If it is not already installed, you can download it from [here](https://www.iis.net/downloads/microsoft/url-rewrite).</span></span> <span data-ttu-id="00048-163">若有多部虛擬機器裝載租用戶入口網站，請在每部虛擬機器都上安裝擴充功能。</span><span class="sxs-lookup"><span data-stu-id="00048-163">If multiple virtual machines host the tenant portal, install the extension on each virtual machine.</span></span>

## <a name="configure-azure-stack"></a><span data-ttu-id="00048-164">設定 Azure Stack</span><span class="sxs-lookup"><span data-stu-id="00048-164">Configure Azure Stack</span></span>
<span data-ttu-id="00048-165">設定 Windows Azure 套件連接器之前，您必須先在 Azure Stack 使用者入口網站中啟用多重雲端模式。</span><span class="sxs-lookup"><span data-stu-id="00048-165">Before you configure the Windows Azure Pack Connector, you must enable multi-cloud mode in the Azure Stack user portal.</span></span> <span data-ttu-id="00048-166">此模式可讓使用者選取要存取其資源的雲端。</span><span class="sxs-lookup"><span data-stu-id="00048-166">This mode enables users to select from which cloud to access resources.</span></span>

<span data-ttu-id="00048-167">若要啟用多重雲端模式，您必須在部署 Azure Stack 後執行 Add-AzurePackConnector.ps1 指令碼。</span><span class="sxs-lookup"><span data-stu-id="00048-167">To enable multi-cloud mode, you must run the Add-AzurePackConnector.ps1 script after Azure Stack deployment.</span></span> <span data-ttu-id="00048-168">下表描述指令碼參數。</span><span class="sxs-lookup"><span data-stu-id="00048-168">The following table describes the script parameters.</span></span>


|  <span data-ttu-id="00048-169">參數</span><span class="sxs-lookup"><span data-stu-id="00048-169">Parameter</span></span> | <span data-ttu-id="00048-170">說明</span><span class="sxs-lookup"><span data-stu-id="00048-170">Description</span></span> | <span data-ttu-id="00048-171">範例</span><span class="sxs-lookup"><span data-stu-id="00048-171">Example</span></span> |   
| -------- | ------------- | ------- |  
| <span data-ttu-id="00048-172">AzurePackClouds</span><span class="sxs-lookup"><span data-stu-id="00048-172">AzurePackClouds</span></span> | <span data-ttu-id="00048-173">Windows Azure 套件連接器的 URI。</span><span class="sxs-lookup"><span data-stu-id="00048-173">URIs of the Windows Azure Pack Connectors.</span></span> <span data-ttu-id="00048-174">這些 URI 應該對應到 Windows Azure 套件租用戶入口網站。</span><span class="sxs-lookup"><span data-stu-id="00048-174">These URIs should correspond to the Windows Azure Pack tenant portals.</span></span> | <span data-ttu-id="00048-175">@{CloudName = "AzurePack1"; CloudEndpoint = "https://waptenantportal1:40005"},@{CloudName = "AzurePack2"; CloudEndpoint = "https://waptenantportal2:40005"}</span><span class="sxs-lookup"><span data-stu-id="00048-175">@{CloudName = "AzurePack1"; CloudEndpoint = "https://waptenantportal1:40005"},@{CloudName = "AzurePack2"; CloudEndpoint = "https://waptenantportal2:40005"}</span></span><br><br>  <span data-ttu-id="00048-176">(依預設，此連接埠值為 40005。)</span><span class="sxs-lookup"><span data-stu-id="00048-176">(By default, the port value is 40005.)</span></span> |  
| <span data-ttu-id="00048-177">AzureStackCloudName</span><span class="sxs-lookup"><span data-stu-id="00048-177">AzureStackCloudName</span></span> | <span data-ttu-id="00048-178">代表本機 Azure Stack 雲端的標籤。</span><span class="sxs-lookup"><span data-stu-id="00048-178">Label to represent the local Azure Stack cloud.</span></span>| <span data-ttu-id="00048-179">"AzureStack"</span><span class="sxs-lookup"><span data-stu-id="00048-179">"AzureStack"</span></span> |
| <span data-ttu-id="00048-180">DisableMultiCloud</span><span class="sxs-lookup"><span data-stu-id="00048-180">DisableMultiCloud</span></span> | <span data-ttu-id="00048-181">停用多重雲端模式的開關。</span><span class="sxs-lookup"><span data-stu-id="00048-181">A switch to disable multi-cloud mode.</span></span>| <span data-ttu-id="00048-182">N/A</span><span class="sxs-lookup"><span data-stu-id="00048-182">N/A</span></span> |
| | |

<span data-ttu-id="00048-183">您可在部署之後緊接著執行 Add-AzurePackConnector.ps1 指令碼，也可以稍後再執行。</span><span class="sxs-lookup"><span data-stu-id="00048-183">You can run the Add-AzurePackConnector.ps1 script immediately after deployment, or later.</span></span> <span data-ttu-id="00048-184">若要在部署後緊接著執行指令碼，請使用與完成 Azure Stack 部署相同的 Windows PowerShell 工作階段。</span><span class="sxs-lookup"><span data-stu-id="00048-184">To run the script immediately after deployment, use the same Windows PowerShell session where Azure Stack deployment completed.</span></span> <span data-ttu-id="00048-185">否則，您也可用系統管理員身分 (登入為 azurestackadmin 帳戶) 開啟新的 Windows PowerShell 工作階段。</span><span class="sxs-lookup"><span data-stu-id="00048-185">Otherwise, you can open a new Windows PowerShell session as an administrator (signed in as the azurestackadmin account).</span></span>

1. <span data-ttu-id="00048-186">使用下列命令 (具有您環境專屬的值) 執行 Add-AzurePackConnector.ps1 指令碼。</span><span class="sxs-lookup"><span data-stu-id="00048-186">Run the Add-AzurePackConnector.ps1 script by using the following commands (with values specific to your environment).</span></span> <span data-ttu-id="00048-187">請注意 Add-AzurePackConnector 指令碼可讓您新增多個 Windows Azure 套件連接器端點。</span><span class="sxs-lookup"><span data-stu-id="00048-187">Notice that the Add-AzurePackConnector script enables you to add more than one Windows Azure Pack Connector endpoint.</span></span>
 
 ```powershell
    $cred = New-Object System.Management.Automation.PSCredential("cloudadmin@azurestack.local", `
    (ConvertTo-SecureString -String "<password>" -AsPlainText -Force))
    $session = New-PSSession -ComputerName 'azs-ercs01' `
     -Credential $cred `
     -ConfigurationName PrivilegedEndpoint `
     -Authentication Credssp

    # Enable Multicloud
    Invoke-Command -Session $session -ScriptBlock { Add-AzurePackConnector -AzurePackClouds `
    @{CloudName = "AzurePack_1"; CloudEndpoint = "https://waptenantportal1:40005"},`
    @{CloudName = "AzurePack_2"; CloudEndpoint = "https://waptenantportal2:40005" } `
    -AzureStackCloudName "AzureStack" }

 ```
> [!NOTE]
> <span data-ttu-id="00048-188">在目前的組建中有個問題，就是 Add-AzurePackConnector 指令碼結束後，會停留在輪詢迴圈中一段很長的時間 (數分鐘)，然後才會結束。</span><span class="sxs-lookup"><span data-stu-id="00048-188">In the current build there is an issue where after the Add-AzurePackConnector script ends, it remains in a polling loop for an extended period of time (several minutes) until it ends.</span></span> <span data-ttu-id="00048-189">您看到 **VERBOSE：步驟「設定 Azure 套件連接器」狀態：「成功」**訊息後，就可以停止指令碼，或等到它自己停止。</span><span class="sxs-lookup"><span data-stu-id="00048-189">After you see the message **VERBOSE: Step 'Configure Azure Pack Connector' status: 'Success'**, you can stop the script or wait until it stops by itself.</span></span> <span data-ttu-id="00048-190">由於已設定成功，因此兩者將不會有所差別。</span><span class="sxs-lookup"><span data-stu-id="00048-190">It won’t make a difference because the configuration has already succeeded.</span></span>

2. <span data-ttu-id="00048-191">請針對您指定的每個 Windows Azure 套件環境，記下此指令碼所產生的輸出檔 (每個環境各一個)。</span><span class="sxs-lookup"><span data-stu-id="00048-191">Make note of the output files that are produced by this script, one for each Windows Azure Pack environment that you specified.</span></span> <span data-ttu-id="00048-192">檔案位於：\\\su1fileserver\SU1_Infrastructure_1\AzurePackConnectorOutput。</span><span class="sxs-lookup"><span data-stu-id="00048-192">The files are located at:  \\\su1fileserver\SU1_Infrastructure_1\AzurePackConnectorOutput.</span></span> <span data-ttu-id="00048-193">這些檔案包含設定目標 Windows Azure 套件環境所需的資訊。</span><span class="sxs-lookup"><span data-stu-id="00048-193">These files contain the information that is required to configure the target Windows Azure Pack environments.</span></span> <span data-ttu-id="00048-194">稍後在這些指示中，您會將這個檔案作為參數傳遞給指令碼。</span><span class="sxs-lookup"><span data-stu-id="00048-194">You pass this file as a parameter to a script later in these instructions.</span></span> <span data-ttu-id="00048-195">這個檔案包含下列資訊：</span><span class="sxs-lookup"><span data-stu-id="00048-195">This file contains the following information:</span></span>

    * <span data-ttu-id="00048-196">**AzurePackConnectorEndpoint**：包含 Windows Azure 套件連接器服務的端點。</span><span class="sxs-lookup"><span data-stu-id="00048-196">**AzurePackConnectorEndpoint**: Contains the endpoint to the Windows Azure Pack Connector service.</span></span>
    * <span data-ttu-id="00048-197">**AuthenticationIdentityProviderPartner**：包含下列值組：</span><span class="sxs-lookup"><span data-stu-id="00048-197">**AuthenticationIdentityProviderPartner**: Contains the following value pair:</span></span>
        * <span data-ttu-id="00048-198">Windows Azure 套件租用戶 API 需要信任的驗證權杖簽署憑證，以便接受來自 Azure Stack 入口網站擴充功能的呼叫。</span><span class="sxs-lookup"><span data-stu-id="00048-198">Authentication Token signing certificate that the Windows Azure Pack Tenant API needs to trust to accept calls from the Azure Stack portal extension.</span></span>

        * <span data-ttu-id="00048-199">與簽署憑證相關聯的「領域」。</span><span class="sxs-lookup"><span data-stu-id="00048-199">The "Realm" associated with the signing certificate.</span></span> <span data-ttu-id="00048-200">例如：https://adfs.local.azurestack.global.external/adfs/c1d72562-534e-4aa5-92aa-d65df289a107/。</span><span class="sxs-lookup"><span data-stu-id="00048-200">For example: https://adfs.local.azurestack.global.external/adfs/c1d72562-534e-4aa5-92aa-d65df289a107/.</span></span>

3.  <span data-ttu-id="00048-201">瀏覽至包含輸出檔的資料夾 (\\su1fileserver\SU1_Infrastructure_1\AzurePackConnectorOutput)，並將檔案複製到本機電腦。</span><span class="sxs-lookup"><span data-stu-id="00048-201">Browse to the folder that contains the output files (\\su1fileserver\SU1_Infrastructure_1\AzurePackConnectorOutput), and copy the files to your local computer.</span></span> <span data-ttu-id="00048-202">檔案會看起來像這樣：AzurePack-06-27-15-50.txt。</span><span class="sxs-lookup"><span data-stu-id="00048-202">The files will look similar to this: AzurePack-06-27-15-50.txt.</span></span>

4.  <span data-ttu-id="00048-203">測試設定。</span><span class="sxs-lookup"><span data-stu-id="00048-203">Test the configuration.</span></span>

    <span data-ttu-id="00048-204">a.</span><span class="sxs-lookup"><span data-stu-id="00048-204">a.</span></span> <span data-ttu-id="00048-205">開啟瀏覽器並登入 Azure Stack 使用者入口網站 (https://portal.local.azurestack.external/)。</span><span class="sxs-lookup"><span data-stu-id="00048-205">Open your browser and sign in to the Azure Stack user portal (https://portal.local.azurestack.external/).</span></span>
    
    <span data-ttu-id="00048-206">b.</span><span class="sxs-lookup"><span data-stu-id="00048-206">b.</span></span> <span data-ttu-id="00048-207">以租用戶身分登入且入口網站載入後，您將會看到無法從 Azure 套件雲端擷取訂用帳戶或擴充功能的錯誤訊息。</span><span class="sxs-lookup"><span data-stu-id="00048-207">After you sign in as a tenant and the portal loads, you'll see errors about not being able to fetch subscriptions or extensions from the Azure Pack cloud.</span></span> <span data-ttu-id="00048-208">按一下 [確定] 以關閉訊息。</span><span class="sxs-lookup"><span data-stu-id="00048-208">Click **OK** to close these messages.</span></span> <span data-ttu-id="00048-209">(在您設定 Windows Azure 套件後這些錯誤訊息就會消失。)</span><span class="sxs-lookup"><span data-stu-id="00048-209">(These error messages will go away after you configure Windows Azure Pack.)</span></span>

    <span data-ttu-id="00048-210">c.</span><span class="sxs-lookup"><span data-stu-id="00048-210">c.</span></span> <span data-ttu-id="00048-211">請注意入口網站左上角的 [雲端] 下拉式清單。</span><span class="sxs-lookup"><span data-stu-id="00048-211">Notice the **Cloud** drop-down list in the upper-left corner of the portal.</span></span>

    ![Azure Stack 使用者介面中的雲端選取器](media/azure-stack-manage-wap/image3.png)

## <a name="configure-windows-azure-pack"></a><span data-ttu-id="00048-213">設定 Windows Azure 套件</span><span class="sxs-lookup"><span data-stu-id="00048-213">Configure Windows Azure Pack</span></span>
<span data-ttu-id="00048-214">只有此預覽版本連接器需要手動設定 Windows Azure 套件。</span><span class="sxs-lookup"><span data-stu-id="00048-214">For this Connector preview release only, Windows Azure Pack requires manual configuration.</span></span>

>[!IMPORTANT]
<span data-ttu-id="00048-215">針對此預覽版本，請僅在測試環境中使用 Windows Azure 套件連接器，而不要在生產環境部署中使用。</span><span class="sxs-lookup"><span data-stu-id="00048-215">For this preview release, use the Windows Azure Pack Connector only in test environments, and not in production deployments.</span></span>

1.  <span data-ttu-id="00048-216">在 Windows Azure 套件租用戶入口網站虛擬機器上安裝連接器 MSI 檔案，並安裝憑證。</span><span class="sxs-lookup"><span data-stu-id="00048-216">Install Connector MSI files on the Windows Azure Pack tenant portal virtual machine, and install certificates.</span></span> <span data-ttu-id="00048-217">(若您有多部租用戶入口網站虛擬機器，則必須在每部虛擬機器上都完成此步驟。)</span><span class="sxs-lookup"><span data-stu-id="00048-217">(If you have multiple tenant portal virtual machines, you must complete this step on each virtual machine.)</span></span>

    <span data-ttu-id="00048-218">a.</span><span class="sxs-lookup"><span data-stu-id="00048-218">a.</span></span> <span data-ttu-id="00048-219">在 [檔案總管] 中，將 (您之前下載的) **WAPConnector** 資料夾複製到租用戶入口網站虛擬機器上名為 **c:\temp** 的資料夾中。</span><span class="sxs-lookup"><span data-stu-id="00048-219">In File Explorer, copy the **WAPConnector** folder (what you downloaded earlier) to a folder named **c:\temp** in the tenant portal virtual machine.</span></span>

    <span data-ttu-id="00048-220">b.</span><span class="sxs-lookup"><span data-stu-id="00048-220">b.</span></span> <span data-ttu-id="00048-221">開啟對租用戶入口網站虛擬機器的主控台或 RDP 連線。</span><span class="sxs-lookup"><span data-stu-id="00048-221">Open a Console or RDP connection to the tenant portal virtual machine.</span></span>

    <span data-ttu-id="00048-222">c.</span><span class="sxs-lookup"><span data-stu-id="00048-222">c.</span></span> <span data-ttu-id="00048-223">將目錄變更為 **c:\temp\wapconnector\setup\scripts**，並執行 **Install-Connector.ps1** 指令碼來安裝三個 MSI 檔案。</span><span class="sxs-lookup"><span data-stu-id="00048-223">Change directories to **c:\temp\wapconnector\setup\scripts**, and run the **Install-Connector.ps1** script to install three MSI files.</span></span> <span data-ttu-id="00048-224">不需要任何參數。</span><span class="sxs-lookup"><span data-stu-id="00048-224">No parameters are required.</span></span>

     ```powershell
    cd C:\temp\wapconnector\setup\scripts\

    .\Install-Connector.ps1
    ```
     <span data-ttu-id="00048-225">d.</span><span class="sxs-lookup"><span data-stu-id="00048-225">d.</span></span> <span data-ttu-id="00048-226">將目錄變更為 **c:\inetpub**，並確認已安裝這三個新網站：</span><span class="sxs-lookup"><span data-stu-id="00048-226">Change directories to **c:\inetpub** and verify that the three new sites are installed:</span></span>

       * <span data-ttu-id="00048-227">MgmtSvc-Connector</span><span class="sxs-lookup"><span data-stu-id="00048-227">MgmtSvc-Connector</span></span>

       * <span data-ttu-id="00048-228">MgmtSvc-ConnectorExtension</span><span class="sxs-lookup"><span data-stu-id="00048-228">MgmtSvc-ConnectorExtension</span></span>

       * <span data-ttu-id="00048-229">MgmtSvc-ConnectorController</span><span class="sxs-lookup"><span data-stu-id="00048-229">MgmtSvc-ConnectorController</span></span>

    <span data-ttu-id="00048-230">e.</span><span class="sxs-lookup"><span data-stu-id="00048-230">e.</span></span> <span data-ttu-id="00048-231">從相同的 **c:\temp\wapconnector\setup\scripts** 資料夾中，執行 **Configure-Certificates.ps1** 指令碼來安裝憑證。</span><span class="sxs-lookup"><span data-stu-id="00048-231">From the same **c:\temp\wapconnector\setup\scripts** folder, run the **Configure-Certificates.ps1** script to install certificates.</span></span> <span data-ttu-id="00048-232">依預設，會使用 Windows Azure 套件租用戶入口網站中可用的相同憑證。</span><span class="sxs-lookup"><span data-stu-id="00048-232">By default, it will use the same certificate that is available for the Tenant Portal site in Windows Azure Pack.</span></span> <span data-ttu-id="00048-233">請確定這是有效的憑證 (受到 Azure Stack AzS-WASP01 虛擬機器和任何存取 Azure Stack 入口網站的用戶端電腦信任)。</span><span class="sxs-lookup"><span data-stu-id="00048-233">Make sure this is a valid certificate (trusted by the Azure Stack AzS-WASP01 virtual machine and any client computer that accesses the Azure Stack portal).</span></span> <span data-ttu-id="00048-234">否則，通訊將無法運作。</span><span class="sxs-lookup"><span data-stu-id="00048-234">Otherwise, communication won’t work.</span></span> <span data-ttu-id="00048-235">(或者，您也可以使用 -Thumbprint 參數，明確地傳遞憑證指紋作為參數。)</span><span class="sxs-lookup"><span data-stu-id="00048-235">(Alternatively, you can explicitly pass a certificate thumbprint as a parameter by using the -Thumbprint parameter.)</span></span>

     ```powershell
        cd C:\temp\wapconnector\setup\scripts\

        .\Configure-Certificates.ps1
    ```

    <span data-ttu-id="00048-236">f.</span><span class="sxs-lookup"><span data-stu-id="00048-236">f.</span></span> <span data-ttu-id="00048-237">若要完成這三項服務的設定，請執行 **Configure-WapConnector.ps1** 指令碼以更新 Web.config 檔案參數。</span><span class="sxs-lookup"><span data-stu-id="00048-237">To finish the configuration of these three services, run the **Configure-WapConnector.ps1** script to update the Web.config file parameters.</span></span>

    |  <span data-ttu-id="00048-238">參數</span><span class="sxs-lookup"><span data-stu-id="00048-238">Parameter</span></span> | <span data-ttu-id="00048-239">說明</span><span class="sxs-lookup"><span data-stu-id="00048-239">Description</span></span> | <span data-ttu-id="00048-240">範例</span><span class="sxs-lookup"><span data-stu-id="00048-240">Example</span></span> |   
    | -------- | ------------- | ------- |  
    | <span data-ttu-id="00048-241">TenantPortalFQDN</span><span class="sxs-lookup"><span data-stu-id="00048-241">TenantPortalFQDN</span></span> | <span data-ttu-id="00048-242">Windows Azure 套件租用戶入口網站 FQDN。</span><span class="sxs-lookup"><span data-stu-id="00048-242">The Windows Azure Pack tenant portal FQDN.</span></span> | <span data-ttu-id="00048-243">tenant.contoso.com</span><span class="sxs-lookup"><span data-stu-id="00048-243">tenant.contoso.com</span></span> | 
    | <span data-ttu-id="00048-244">TenantAPIFQDN</span><span class="sxs-lookup"><span data-stu-id="00048-244">TenantAPIFQDN</span></span> | <span data-ttu-id="00048-245">Windows Azure 套件租用戶 API FQDN。</span><span class="sxs-lookup"><span data-stu-id="00048-245">The Windows Azure Pack Tenant API FQDN.</span></span> | <span data-ttu-id="00048-246">tenantapi.contoso.com</span><span class="sxs-lookup"><span data-stu-id="00048-246">tenantapi.contoso.com</span></span>  |
    | <span data-ttu-id="00048-247">AzureStackPortalFQDN</span><span class="sxs-lookup"><span data-stu-id="00048-247">AzureStackPortalFQDN</span></span> | <span data-ttu-id="00048-248">Azure Stack 使用者入口網站 FQDN。</span><span class="sxs-lookup"><span data-stu-id="00048-248">The Azure Stack user portal FQDN.</span></span> | <span data-ttu-id="00048-249">portal.local.azurestack.external</span><span class="sxs-lookup"><span data-stu-id="00048-249">portal.local.azurestack.external</span></span> |
    | | |
    
     ```powershell
    .\Configure-WapConnector.ps1 -TenantPortalFQDN "tenant.contoso.com" `
         -TenantAPIFQDN "tenantapi.contoso.com" `
         -AzureStackPortalFQDN "portal.local.azurestack.external"
    ```
    <span data-ttu-id="00048-250">g.</span><span class="sxs-lookup"><span data-stu-id="00048-250">g.</span></span> <span data-ttu-id="00048-251">若您有多部租用戶入口網站虛擬機器，請在每部虛擬機器上重複步驟 1。</span><span class="sxs-lookup"><span data-stu-id="00048-251">If you have multiple tenant portal virtual machines, repeat step 1 for each of these virtual machines.</span></span>

2. <span data-ttu-id="00048-252">在每部 Windows Azure 套件租用戶 API 虛擬機器上安裝新的租用戶 API MSI。</span><span class="sxs-lookup"><span data-stu-id="00048-252">Install the new Tenant API MSI on each Windows Azure Pack Tenant API virtual machine.</span></span>

    <span data-ttu-id="00048-253">a.</span><span class="sxs-lookup"><span data-stu-id="00048-253">a.</span></span> <span data-ttu-id="00048-254">如果負載平衡器正在使用中，您可能會想要將虛擬機器標示為離線。</span><span class="sxs-lookup"><span data-stu-id="00048-254">If a load balancer is in use, you may want to mark the virtual machine as offline.</span></span>

    <span data-ttu-id="00048-255">b.</span><span class="sxs-lookup"><span data-stu-id="00048-255">b.</span></span> <span data-ttu-id="00048-256">在 [檔案總管] 中，將 **WAPConnector** 資料夾複製到每部租用戶 API 機器上名為 **c:\temp** 的資料夾中。</span><span class="sxs-lookup"><span data-stu-id="00048-256">In File Explorer, copy the **WAPConnector** folder to a folder named **c:\temp** on each Tenant API machine.</span></span>

    <span data-ttu-id="00048-257">c.</span><span class="sxs-lookup"><span data-stu-id="00048-257">c.</span></span> <span data-ttu-id="00048-258">將您稍早儲存的 AzurePackConnectorOutput.txt 檔案複製到 **c:\temp\WAPConnector**。</span><span class="sxs-lookup"><span data-stu-id="00048-258">Copy the AzurePackConnectorOutput.txt file that you saved earlier, to **c:\temp\WAPConnector**.</span></span>

    <span data-ttu-id="00048-259">d.</span><span class="sxs-lookup"><span data-stu-id="00048-259">d.</span></span> <span data-ttu-id="00048-260">開啟對 (您將檔案複製到的) 租用戶 API VM 的主控台或 RDP 連線。</span><span class="sxs-lookup"><span data-stu-id="00048-260">Open a Console or RDP connection to the Tenant API VM you copied the files to.</span></span>
    
    <span data-ttu-id="00048-261">e.</span><span class="sxs-lookup"><span data-stu-id="00048-261">e.</span></span> <span data-ttu-id="00048-262">將目錄變更為 **c:\temp\wapconnector\setup\scripts**，並執行 **Update-TenantAPI.ps1**。</span><span class="sxs-lookup"><span data-stu-id="00048-262">Change directories to **c:\temp\wapconnector\setup\scripts**, and run **Update-TenantAPI.ps1**.</span></span> <span data-ttu-id="00048-263">這個新版本的 WAP 租用戶 API 包含變更，不只可啟用與目前 STS 間的信任關係，還可以啟用與 Azure Stack AD FS 執行個體間的信任關係。</span><span class="sxs-lookup"><span data-stu-id="00048-263">This new version of the WAP Tenant API contains a change to enable a trust relationship not only with the current STS, but also with the instance of AD FS in Azure Stack.</span></span>

     ```powershell
    cd C:\temp\wapconnector\setup\packages\

    .\Update-TenantAPI.ps1
    ```

    <span data-ttu-id="00048-264">f.</span><span class="sxs-lookup"><span data-stu-id="00048-264">f.</span></span>  <span data-ttu-id="00048-265">在每部執行租用戶 API 的虛擬機器上重複步驟 2。</span><span class="sxs-lookup"><span data-stu-id="00048-265">Repeat step 2 on any other virtual machine running the Tenant API.</span></span>
3. <span data-ttu-id="00048-266">**只從其中一部**租用戶 API VM 上，執行 Configure-TrustAzureStack.ps1 指令碼，以新增與租用戶 API 和 Azure Stack 上 AD FS 執行個體之間的信任關係。</span><span class="sxs-lookup"><span data-stu-id="00048-266">From **only one** of the Tenant API VMs, run the Configure-TrustAzureStack.ps1 script to add a trust relationship between the Tenant API and the AD FS instance on Azure Stack.</span></span> <span data-ttu-id="00048-267">您必須使用對 Microsoft.MgmtSvc.Store 資料庫具有系統管理員存取權的帳戶。</span><span class="sxs-lookup"><span data-stu-id="00048-267">You must use an account with sysadmin access to the Microsoft.MgmtSvc.Store database.</span></span> <span data-ttu-id="00048-268">此指令碼具有下列參數︰</span><span class="sxs-lookup"><span data-stu-id="00048-268">This script has the following parameters:</span></span>

    | <span data-ttu-id="00048-269">參數</span><span class="sxs-lookup"><span data-stu-id="00048-269">Parameter</span></span> | <span data-ttu-id="00048-270">說明</span><span class="sxs-lookup"><span data-stu-id="00048-270">Description</span></span> | <span data-ttu-id="00048-271">範例</span><span class="sxs-lookup"><span data-stu-id="00048-271">Example</span></span> |
    | --------- | ------------| ------- |
   | <span data-ttu-id="00048-272">SqlServer</span><span class="sxs-lookup"><span data-stu-id="00048-272">SqlServer</span></span> | <span data-ttu-id="00048-273">包含 Microsoft.MgmtSvc.Store 資料庫的 SQL Server 名稱。</span><span class="sxs-lookup"><span data-stu-id="00048-273">The name of the SQL Server that contains the Microsoft.MgmtSvc.Store database.</span></span> <span data-ttu-id="00048-274">這是必要參數。</span><span class="sxs-lookup"><span data-stu-id="00048-274">This parameter is required.</span></span> | <span data-ttu-id="00048-275">SQLServer</span><span class="sxs-lookup"><span data-stu-id="00048-275">SQLServer</span></span> | 
   | <span data-ttu-id="00048-276">DataFile</span><span class="sxs-lookup"><span data-stu-id="00048-276">DataFile</span></span> | <span data-ttu-id="00048-277">此輸出檔是稍早在設定 Azure Stack 多重雲端模式期間所產生的。</span><span class="sxs-lookup"><span data-stu-id="00048-277">The output file that was generated during the configuration of the Azure Stack multi-cloud mode earlier.</span></span> <span data-ttu-id="00048-278">這是必要參數。</span><span class="sxs-lookup"><span data-stu-id="00048-278">This parameter is required.</span></span> | <span data-ttu-id="00048-279">AzurePack-06-27-15-50.txt</span><span class="sxs-lookup"><span data-stu-id="00048-279">AzurePack-06-27-15-50.txt</span></span> | 
   | <span data-ttu-id="00048-280">PromptForSqlCredential</span><span class="sxs-lookup"><span data-stu-id="00048-280">PromptForSqlCredential</span></span> | <span data-ttu-id="00048-281">表示指令碼應該以互動方式提示您，要連線到 SQL Server 執行個體時所使用的 SQL 驗證認證。</span><span class="sxs-lookup"><span data-stu-id="00048-281">Indicates that the script should prompt you interactively for a SQL Authentication credential to use when connecting to the SQL Server instance.</span></span> <span data-ttu-id="00048-282">指定的認證必須有足夠的權限，可解除安裝資料庫、結構描述及刪除使用者登入。</span><span class="sxs-lookup"><span data-stu-id="00048-282">The given credential must have sufficient permissions to uninstall databases, schemas, and delete user logins.</span></span> <span data-ttu-id="00048-283">如果未提供，指令碼會假設目前的使用者內容具有存取權。</span><span class="sxs-lookup"><span data-stu-id="00048-283">If none is provided, the script assumes that current user context has access.</span></span> | <span data-ttu-id="00048-284">不需要任何值。</span><span class="sxs-lookup"><span data-stu-id="00048-284">No value is needed.</span></span> |
   |  |  |

    <span data-ttu-id="00048-285">如果您不知道要使用的 SQL 伺服器，可以進行探索。</span><span class="sxs-lookup"><span data-stu-id="00048-285">If you don't know the SQL Server to use, you can discover it.</span></span> <span data-ttu-id="00048-286">請連線到租用戶 API 的電腦，使用 Unprotect-MgmtSvc 命令取消保護租用戶 API Web.config 檔案，並尋找連接字串中的伺服器名稱。</span><span class="sxs-lookup"><span data-stu-id="00048-286">Connect to the Tenant API computer, use the Unprotect-MgmtSvc command to unprotect the Tenant API Web.config file, and look for the server name in the connection string.</span></span> <span data-ttu-id="00048-287">請記得再次執行 Protect-MgmtSvc 以保護租用戶 API Web.config 檔案。</span><span class="sxs-lookup"><span data-stu-id="00048-287">Remember to run Protect-MgmtSvc again to protect the Tenant API Web.config file.</span></span>

  ```powershell
  cd C:\temp\wapconnector\setup\scripts\

 .\Configure-TrustAzureStack.ps1 -SqlServer "SQLServer" `
       -DataFile "C:\temp\wapconnector\AzurePackConnectorOutput.txt"
  ```

## <a name="example"></a><span data-ttu-id="00048-288">範例</span><span class="sxs-lookup"><span data-stu-id="00048-288">Example</span></span>
<span data-ttu-id="00048-289">下列範例會示範在單一節點 Azure Stack 設定下完整的 Windows Azure 套件連接器部署，以及兩種 Windows Azure 套件快速安裝。</span><span class="sxs-lookup"><span data-stu-id="00048-289">The following example shows a complete Windows Azure Pack Connector deployment on a single-node Azure Stack configuration and two Windows Azure Pack Express installations.</span></span> <span data-ttu-id="00048-290">(每種快速安裝都是在單一電腦上，範例名稱為 *wapcomputer1* 和 *wapcomputer2*。)</span><span class="sxs-lookup"><span data-stu-id="00048-290">(Each Express installation is on a single computer, with the example names *wapcomputer1* and*wapcomputer2*.)</span></span>

```powershell
# Run the following script on the Azure Stack host
$cred = New-Object System.Management.Automation.PSCredential("cloudadmin@azurestack.local",`
     (ConvertTo-SecureString -String "p@ssw0rd" -AsPlainText -Force))
$session = New-PSSession -ComputerName 'azs-ercs01' -Credential $cred `
     -ConfigurationName PrivilegedEndpoint -Authentication Credssp
 
# Enable Multicloud
invoke-command -Session $session -ScriptBlock { Add-AzurePackConnector -AzurePackClouds `
     @{CloudName = "AzurePack_1"; CloudEndpoint = "https://wapcomputer1.contoso.com:40005"},`
     @{CloudName = "AzurePack_2"; CloudEndpoint = "https://wapcomputer2.contoso.com:40005"}`
     -AzureStackCloudName "AzureStack" }  

```
<span data-ttu-id="00048-291">從 [Microsoft 下載中心](https://aka.ms/wapconnectorazurestackdlc)下載 .exe 檔案、將其解壓縮，並將 WAPConnector 資料夾複製到 Windows Azure 套件電腦上的 **c:\temp** 資料夾中。</span><span class="sxs-lookup"><span data-stu-id="00048-291">Download the .exe file from the [Microsoft Download Center](https://aka.ms/wapconnectorazurestackdlc), extract it, and copy the WAPConnector folder to a **c:\temp** folder on the Windows Azure Pack computer.</span></span> <span data-ttu-id="00048-292">將先前指令碼中所產生的輸出檔案 (位於 \\\su1fileserver\SU1_Infrastructure_1\AzurePackConnectorOutput) 複製到 **c:\temp\WAPConnector** 資料夾中。</span><span class="sxs-lookup"><span data-stu-id="00048-292">Copy the files that were generated as output in the previous script (located at \\\su1fileserver\SU1_Infrastructure_1\AzurePackConnectorOutput) to the **c:\temp\WAPConnector** folder.</span></span> <span data-ttu-id="00048-293">(檔案會看起來像這樣：AzurePack-06-27-15-50.txt。)然後執行下列指令碼 (每次一個 Windows Azure 套件執行個體)：</span><span class="sxs-lookup"><span data-stu-id="00048-293">(The files will looks similar to this: AzurePack-06-27-15-50.txt.) Then, run the following script, once per instance of Windows Azure Pack:</span></span>

 ```powershell
# Install Connector components
cd C:\temp\WAPConnector\Setup\Scripts
.\Install-Connector.ps1

# Configure Certificates for the new Connector services
.\Configure-Certificates.ps1

# Configure the Connector services
.\Configure-WapConnector.ps1 -TenantPortalFQDN "wapcomputer1.contoso.com" `
     -TenantAPIFQDN "wapcomputer1.contoso.com" `
     -AzureStackPortalFQDN "portal.local.azurestack.external"

# Install the updated TenantAPI
.\Update-TenantAPI.ps1

# Establish trust with the Azure Stack AD FS
.\Configure-TrustAzureStack.ps1 -SqlServer "wapcomputer1" `
     -DataFile "C:\temp\wapconnector\AzurePack-06-27-15-50.txt" 

```
## <a name="troubleshooting-tips"></a><span data-ttu-id="00048-294">疑難排解秘訣</span><span class="sxs-lookup"><span data-stu-id="00048-294">Troubleshooting tips</span></span>
1.  <span data-ttu-id="00048-295">確保 Azure Stack 與 Windows Azure 套件之間有網路連線能力。</span><span class="sxs-lookup"><span data-stu-id="00048-295">Ensure there is network connectivity between Azure Stack and Windows Azure Pack.</span></span> <span data-ttu-id="00048-296">在任何存取 Azure Stack 入口網站的租用戶電腦，與執行新連接器服務的 Windows Azure 套件租用戶入口網站虛擬機器之間，都應具有連線能力。</span><span class="sxs-lookup"><span data-stu-id="00048-296">This connectivity should be between any tenant computer that accesses the Azure Stack portal and the Windows Azure Pack tenant portal virtual machine where the new Connector services are running.</span></span>
2.  <span data-ttu-id="00048-297">確保所有指定的 FQDN 都正確。</span><span class="sxs-lookup"><span data-stu-id="00048-297">Ensure that all specified FQDNs are correct.</span></span>
3.  <span data-ttu-id="00048-298">確保 Azure Stack (尤其是 AzS-WASP01 VM) 和任何其他租用戶可用來存取 Azure Stack 使用者入口網站的電腦，都必須信任用於新連接器服務上的 SSL 憑證。</span><span class="sxs-lookup"><span data-stu-id="00048-298">Ensure that the SSL certificates used in the new Connector services are trusted by Azure Stack (specifically the AzS-WASP01 VM) and any other computer the tenant may use to access the Azure Stack user portal.</span></span>
4. <span data-ttu-id="00048-299">若要檢閱已知的問題，請參閱 [Microsoft Azure Stack 疑難排解](azure-stack-troubleshooting.md)。</span><span class="sxs-lookup"><span data-stu-id="00048-299">For known issues, see [Microsoft Azure Stack troubleshooting](azure-stack-troubleshooting.md).</span></span>


## <a name="next-steps"></a><span data-ttu-id="00048-300">後續步驟</span><span class="sxs-lookup"><span data-stu-id="00048-300">Next steps</span></span>
[<span data-ttu-id="00048-301">使用 Azure Stack 中系統管理員和使用者的入口網站</span><span class="sxs-lookup"><span data-stu-id="00048-301">Using the administrator and user portals in Azure Stack</span></span>](azure-stack-manage-portals.md)
