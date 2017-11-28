---
title: "從 Azure 堆疊 aaaManage Windows Azure Pack 虛擬機器 |Microsoft 文件"
description: "深入了解如何 toomanage hello Azure 堆疊中的使用者入口網站中的 Windows Azure Pack (WAP) Vm。"
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
ms.openlocfilehash: 97dbe34055667a72fddc8507ae389562e885a32e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="manage-windows-azure-pack-virtual-machines-from-azure-stack"></a><span data-ttu-id="8e817-103">從 Azure Stack 管理 Windows Azure 套件虛擬機器</span><span class="sxs-lookup"><span data-stu-id="8e817-103">Manage Windows Azure Pack virtual machines from Azure Stack</span></span>
<span data-ttu-id="8e817-104">在 hello Azure 堆疊開發套件，您可以啟用從 hello Azure 堆疊使用者入口網站 tootenant 虛擬機器執行於 Windows Azure 組件的存取。</span><span class="sxs-lookup"><span data-stu-id="8e817-104">In hello Azure Stack Development Kit, you can enable access from hello Azure Stack user portal tootenant virtual machines running on Windows Azure Pack.</span></span> <span data-ttu-id="8e817-105">租用戶可使用 hello Azure 堆疊入口 toomanage 其現有的 IaaS 虛擬機器和虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="8e817-105">Tenants can use hello Azure Stack portal toomanage their existing IaaS virtual machines and virtual networks.</span></span> <span data-ttu-id="8e817-106">這些資源是透過使用在 Windows Azure 套件 hello 基礎 Service Provider Foundation (SPF) 和 Virtual Machine Manager (VMM) 元件。</span><span class="sxs-lookup"><span data-stu-id="8e817-106">These resources are made available on Windows Azure Pack through hello underlying Service Provider Foundation (SPF) and Virtual Machine Manager (VMM) components.</span></span> <span data-ttu-id="8e817-107">具體而言，租用戶可以：</span><span class="sxs-lookup"><span data-stu-id="8e817-107">Specifically, tenants can:</span></span>

* <span data-ttu-id="8e817-108">瀏覽資源</span><span class="sxs-lookup"><span data-stu-id="8e817-108">Browse resources</span></span>
* <span data-ttu-id="8e817-109">檢查設定值</span><span class="sxs-lookup"><span data-stu-id="8e817-109">Examine configuration values</span></span>
* <span data-ttu-id="8e817-110">停止或啟動虛擬機器</span><span class="sxs-lookup"><span data-stu-id="8e817-110">Stop or start a virtual machine</span></span>
* <span data-ttu-id="8e817-111">透過遠端桌面通訊協定 (RDP) 連線 tooa 虛擬機器</span><span class="sxs-lookup"><span data-stu-id="8e817-111">Connect tooa virtual machine through Remote Desktop Protocol (RDP)</span></span>
* <span data-ttu-id="8e817-112">建立和管理檢查點</span><span class="sxs-lookup"><span data-stu-id="8e817-112">Create and manage checkpoints</span></span>
* <span data-ttu-id="8e817-113">刪除虛擬機器和虛擬網路</span><span class="sxs-lookup"><span data-stu-id="8e817-113">Delete virtual machines and virtual networks</span></span>

<span data-ttu-id="8e817-114">Windows Azure Pack 連接器 hello 提供此功能的 Azure 堆疊 （預覽）。</span><span class="sxs-lookup"><span data-stu-id="8e817-114">This functionality is provided by hello Windows Azure Pack Connector for Azure Stack (Preview).</span></span> <span data-ttu-id="8e817-115">本文將說明如何 tooconfigure hello 針對單一節點的 Azure 堆疊環境的連接器。</span><span class="sxs-lookup"><span data-stu-id="8e817-115">This article shows how tooconfigure hello connector for a single-node Azure Stack environment.</span></span>

<span data-ttu-id="8e817-116">Hello 連接器此預覽版本，請注意 hello 下列各項：</span><span class="sxs-lookup"><span data-stu-id="8e817-116">For this preview release of hello connector, be aware of hello following:</span></span>
* <span data-ttu-id="8e817-117">使用 hello Windows Azure Pack Connector 只在測試環境中 （針對 Azure 堆疊與 Windows Azure Pack），而不是在生產部署。</span><span class="sxs-lookup"><span data-stu-id="8e817-117">Use hello Windows Azure Pack Connector only in test environments (for both Azure Stack and Windows Azure Pack), and not in production deployments.</span></span>
* <span data-ttu-id="8e817-118">您必須擁有 Windows Azure 套件更新彙總套件 (UR) 9.1 或更新版本，以及 System Center SPF 和 VMM UR 9 或更新版本。</span><span class="sxs-lookup"><span data-stu-id="8e817-118">You must have Windows Azure Pack Update Rollup (UR) 9.1 or later and System Center SPF and VMM UR 9 or later.</span></span>
* <span data-ttu-id="8e817-119">hello VMM 和 SPF 元件可以是 System Center 2012 R2 或 System Center 2016。</span><span class="sxs-lookup"><span data-stu-id="8e817-119">hello VMM and SPF components can be either System Center 2012 R2 or System Center 2016.</span></span>
* <span data-ttu-id="8e817-120">您必須在 Azure Stack 和 Windows Azure 套件都執行設定步驟。</span><span class="sxs-lookup"><span data-stu-id="8e817-120">You must perform configuration steps on both Azure Stack and on Windows Azure Pack.</span></span>
* <span data-ttu-id="8e817-121">hello 指示適用於 toonon 雲端平台系統 (CPS) 環境中。</span><span class="sxs-lookup"><span data-stu-id="8e817-121">hello instructions apply toonon-Cloud Platform System (CPS) environments.</span></span>
* <span data-ttu-id="8e817-122">tooreview hello 已知的問題，請參閱[疑難排解 Microsoft Azure 堆疊](azure-stack-troubleshooting.md)。</span><span class="sxs-lookup"><span data-stu-id="8e817-122">tooreview hello known issues, see [Microsoft Azure Stack troubleshooting](azure-stack-troubleshooting.md).</span></span>


## <a name="architecture"></a><span data-ttu-id="8e817-123">架構</span><span class="sxs-lookup"><span data-stu-id="8e817-123">Architecture</span></span>
<span data-ttu-id="8e817-124">hello 下列圖表顯示 hello Windows Azure Pack 連接器 hello 主要元件。</span><span class="sxs-lookup"><span data-stu-id="8e817-124">hello following diagram shows hello main components of hello Windows Azure Pack Connector.</span></span>

![hello Windows Azure Pack 連接器元件](media/azure-stack-manage-wap/image1.png)

<span data-ttu-id="8e817-126">請注意下列詳細資料的 hello:</span><span class="sxs-lookup"><span data-stu-id="8e817-126">Notice hello following details:</span></span>
* <span data-ttu-id="8e817-127">hello Azure 堆疊使用者入口網站從這兩個雲端 （Azure 堆疊和 Windows Azure Pack） 中存取 hello 資源資訊。</span><span class="sxs-lookup"><span data-stu-id="8e817-127">hello Azure Stack user portal accesses hello resource information from both clouds (Azure Stack and Windows Azure Pack).</span></span>
* <span data-ttu-id="8e817-128">hello 使用者必須具有兩個環境中有效的帳戶。</span><span class="sxs-lookup"><span data-stu-id="8e817-128">hello user must have an account that is valid in both environments.</span></span>
* <span data-ttu-id="8e817-129">hello Azure 堆疊使用者入口網站必須具有網路存取 toohello 元件在 Windows Azure 組件上執行。</span><span class="sxs-lookup"><span data-stu-id="8e817-129">hello Azure Stack user portal must have network access toohello components running on Windows Azure Pack.</span></span>
* <span data-ttu-id="8e817-130">在 hello **WAP** > 一節的 hello 圖表中，您可以查看 hello 新 Windows Azure Pack Connector 模組 （WAP 擴充功能和連接器），並 hello 現有 Windows Azure Pack 租用戶 API 與 SPF 和 VMM 元件。</span><span class="sxs-lookup"><span data-stu-id="8e817-130">In hello **WAP** section of hello diagram, you can see hello new Windows Azure Pack Connector modules (WAP Extension and Connector) and hello existing Windows Azure Pack Tenant API with SPF and VMM components.</span></span>


## <a name="identity-management"></a><span data-ttu-id="8e817-131">身分識別管理</span><span class="sxs-lookup"><span data-stu-id="8e817-131">Identity management</span></span>
<span data-ttu-id="8e817-132">Windows Azure Pack 租用戶 API hello 必須信任 hello Azure 堆疊安全性權杖服務 (STS)。</span><span class="sxs-lookup"><span data-stu-id="8e817-132">hello Windows Azure Pack Tenant API must trust hello Azure Stack security token service (STS).</span></span>

<span data-ttu-id="8e817-133">當使用者執行透過 hello Azure 堆疊入口網站的動作目標的 Windows Azure Pack 的資源時，hello 入口網站會使用 hello Windows Azure Pack 租用戶 API。</span><span class="sxs-lookup"><span data-stu-id="8e817-133">When a user performs an action through hello Azure Stack portal that targets Windows Azure Pack resources, hello portal uses hello Windows Azure Pack Tenant API.</span></span> <span data-ttu-id="8e817-134">因此，hello 提供使用者驗證語彙基元必須來自受信任的 STS。</span><span class="sxs-lookup"><span data-stu-id="8e817-134">Therefore, hello provided user authentication token must come from a trusted STS.</span></span> <span data-ttu-id="8e817-135">請參閱下列圖表中的 hello:</span><span class="sxs-lookup"><span data-stu-id="8e817-135">See hello following diagram:</span></span>

![Windows Azure 套件連接器驗證的圖表](media/azure-stack-manage-wap/image2.png)

<span data-ttu-id="8e817-137">Hello 開發套件在環境中，Windows Azure Pack and Azure 堆疊有獨立的身分識別提供者。</span><span class="sxs-lookup"><span data-stu-id="8e817-137">In hello development kit environment, Windows Azure Pack and Azure Stack have independent identity providers.</span></span> <span data-ttu-id="8e817-138">從 hello Azure 堆疊入口網站存取這兩種環境的使用者必須擁有的 hello 中這兩個身分識別提供者名稱相同的使用者主體名稱 (UPN)。</span><span class="sxs-lookup"><span data-stu-id="8e817-138">Users who access both environments from hello Azure Stack portal must have hello same user principal name (UPN) name in both identity providers.</span></span> <span data-ttu-id="8e817-139">例如，hello 帳戶 *azurestackadmin@azurestack.local* 也應該存在於 hello STS for Windows Azure Pack 中。</span><span class="sxs-lookup"><span data-stu-id="8e817-139">For example, hello account *azurestackadmin@azurestack.local* should also exist in hello STS for Windows Azure Pack.</span></span> <span data-ttu-id="8e817-140">在 AD FS 並未設定 toosupport 輸出信任關係，您會建立信任從 hello Windows Azure Pack 元件 (租用戶 API) toohello Azure 堆疊 AD FS 執行個體。</span><span class="sxs-lookup"><span data-stu-id="8e817-140">Where AD FS is not set up toosupport outbound trust relationships, you will establish trust from hello Windows Azure Pack components (Tenant API) toohello Azure Stack instance of AD FS.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="8e817-141">必要條件</span><span class="sxs-lookup"><span data-stu-id="8e817-141">Prerequisites</span></span>

### <a name="download-hello-windows-azure-pack-connector"></a><span data-ttu-id="8e817-142">下載 Windows Azure Pack 連接器 hello</span><span class="sxs-lookup"><span data-stu-id="8e817-142">Download hello Windows Azure Pack Connector</span></span>
<span data-ttu-id="8e817-143">在 hello [Microsoft Download Center](https://aka.ms/wapconnectorazurestackdlc)，請下載 hello.exe 檔案，並將它解壓縮 tooyour 本機電腦。</span><span class="sxs-lookup"><span data-stu-id="8e817-143">On hello [Microsoft Download Center](https://aka.ms/wapconnectorazurestackdlc), download hello .exe file and extract it tooyour local computer.</span></span> <span data-ttu-id="8e817-144">稍後，您可以複製可以存取 Windows Azure Pack 環境的 hello 內容 tooa 電腦。</span><span class="sxs-lookup"><span data-stu-id="8e817-144">Later, you copy hello contents tooa computer that can access your Windows Azure Pack environment.</span></span>

### <a name="deployment-option-requirement"></a><span data-ttu-id="8e817-145">部署選項需求</span><span class="sxs-lookup"><span data-stu-id="8e817-145">Deployment option requirement</span></span>
<span data-ttu-id="8e817-146">與 Windows Azure Pack toointegrate，可以使用 AD FS hello 或 hello Azure Active Directory 選項來部署 Azure 堆疊。</span><span class="sxs-lookup"><span data-stu-id="8e817-146">toointegrate with Windows Azure Pack, you can deploy Azure Stack by using hello AD FS option or hello Azure Active Directory option.</span></span>

### <a name="connectivity-requirements"></a><span data-ttu-id="8e817-147">連線能力需求</span><span class="sxs-lookup"><span data-stu-id="8e817-147">Connectivity requirements</span></span>
1. <span data-ttu-id="8e817-148">從 hello 電腦存取 hello Azure 堆疊使用者入口網站，請確定您可以透過 hello web 瀏覽器存取 hello Windows Azure Pack 租用戶入口網站。</span><span class="sxs-lookup"><span data-stu-id="8e817-148">From hello computer on which you access hello Azure Stack user portal, make sure that you can access hello Windows Azure Pack tenant portal through hello web browser.</span></span>
2. <span data-ttu-id="8e817-149">hello AzS WASP01 Azure 堆疊上的虛擬機器必須能夠 tooconnect toohello Windows Azure Pack 租用戶入口網站的電腦。</span><span class="sxs-lookup"><span data-stu-id="8e817-149">hello AzS-WASP01 virtual machine on Azure Stack must be able tooconnect toohello Windows Azure Pack tenant portal computer.</span></span> <span data-ttu-id="8e817-150">使用 Ping.exe tooverify 網路連線。</span><span class="sxs-lookup"><span data-stu-id="8e817-150">Use Ping.exe tooverify network connectivity.</span></span> 
3.  <span data-ttu-id="8e817-151">您必須擁有 hello 新連接器服務的有效憑證。</span><span class="sxs-lookup"><span data-stu-id="8e817-151">You must have valid certificates for hello new Connector services.</span></span> <span data-ttu-id="8e817-152">這些 SSL 憑證必須由受信任的憑證授權單位 (CA) 發行。</span><span class="sxs-lookup"><span data-stu-id="8e817-152">These SSL certificates must be issued by a trusted certification authority (CA).</span></span> <span data-ttu-id="8e817-153">您不得使用自我簽署的憑證。</span><span class="sxs-lookup"><span data-stu-id="8e817-153">You can't use self-signed certificates.</span></span> <span data-ttu-id="8e817-154">hello SSL 憑證必須受 Azure 堆疊 (特別是 hello AzS WASP01 VM)，而且 hello 租用戶的任何其他電腦可以使用 tooaccess hello Azure 堆疊使用者入口網站。</span><span class="sxs-lookup"><span data-stu-id="8e817-154">hello SSL certificates must be trusted by Azure Stack (specifically hello AzS-WASP01 VM) and any other computer that hello tenant may use tooaccess hello Azure Stack user portal.</span></span>
 
    >[!NOTE]
    <span data-ttu-id="8e817-155">因為 AzS WASP01 hello Server Core 安裝選項執行 Windows Server，您可以使用命令列工具，例如 Certutil.ext tooimport hello 憑證。</span><span class="sxs-lookup"><span data-stu-id="8e817-155">Because AzS-WASP01 runs Windows Server with hello Server Core installation option, you can use a command-line tool such as Certutil.ext tooimport hello certificate.</span></span> <span data-ttu-id="8e817-156">例如，您可以在其中複製 hello.cer 檔案 tooc:\temp 上 AzS WASP01，然後執行 hello 命令**certutil addstore"CA""c:\temp\certname.cer"**。</span><span class="sxs-lookup"><span data-stu-id="8e817-156">For example, you could copy hello .cer file tooc:\temp on AzS-WASP01, and then run hello command **certutil -addstore "CA" "c:\temp\certname.cer"**.</span></span>

4.  <span data-ttu-id="8e817-157">tooestablish RDP 連線 tooWindows 透過 hello Azure 堆疊入口網站的 Azure Pack 租用戶虛擬機器，hello Windows Azure Pack 環境必須允許遠端桌面流量 toohello 租用戶 Vm。</span><span class="sxs-lookup"><span data-stu-id="8e817-157">tooestablish RDP connectivity tooWindows Azure Pack tenant virtual machines through hello Azure Stack portal, hello Windows Azure Pack environment must allow Remote Desktop traffic toohello tenant VMs.</span></span>
5.  <span data-ttu-id="8e817-158">Azure 堆疊租用戶虛擬機器與 Windows Azure Pack 租用戶虛擬機器之間的連線，其外部 IP 位址必須可路由傳送 hello 兩個環境。</span><span class="sxs-lookup"><span data-stu-id="8e817-158">For connectivity between Azure Stack tenant virtual machines and Windows Azure Pack tenant virtual machines, their external IP addresses must be routable across hello two environments.</span></span> <span data-ttu-id="8e817-159">這種連線能力也可能包括建立 DNS 伺服器 tooresolve 虛擬機器名稱 hello 環境之間的關聯。</span><span class="sxs-lookup"><span data-stu-id="8e817-159">This connectivity could also include associating a DNS server tooresolve virtual machine names between hello environments.</span></span>

### <a name="iis-requirements"></a><span data-ttu-id="8e817-160">IIS 需求</span><span class="sxs-lookup"><span data-stu-id="8e817-160">IIS requirements</span></span>
<span data-ttu-id="8e817-161">裝載 hello Windows Azure Pack 租用戶入口網站 （這可能是實體的主機、 虛擬機器或多部虛擬機器） 的 hello 電腦必須有 hello URL 重寫 IIS 擴充功能安裝。</span><span class="sxs-lookup"><span data-stu-id="8e817-161">hello computer that hosts hello Windows Azure Pack tenant portal (which may be a physical host, a virtual machine, or multiple virtual machines) must have hello URL Rewrite IIS extension installed.</span></span> <span data-ttu-id="8e817-162">如果尚未安裝，您可以從[這裡](https://www.iis.net/downloads/microsoft/url-rewrite)下載。</span><span class="sxs-lookup"><span data-stu-id="8e817-162">If it is not already installed, you can download it from [here](https://www.iis.net/downloads/microsoft/url-rewrite).</span></span> <span data-ttu-id="8e817-163">如果多個虛擬機器裝載 hello 租用戶入口網站，請在每個虛擬機器上安裝 hello 擴充功能。</span><span class="sxs-lookup"><span data-stu-id="8e817-163">If multiple virtual machines host hello tenant portal, install hello extension on each virtual machine.</span></span>

## <a name="configure-azure-stack"></a><span data-ttu-id="8e817-164">設定 Azure Stack</span><span class="sxs-lookup"><span data-stu-id="8e817-164">Configure Azure Stack</span></span>
<span data-ttu-id="8e817-165">設定 Windows Azure Pack 連接器 hello 之前，您必須啟用 hello Azure 堆疊使用者入口網站中的多個雲端模式。</span><span class="sxs-lookup"><span data-stu-id="8e817-165">Before you configure hello Windows Azure Pack Connector, you must enable multi-cloud mode in hello Azure Stack user portal.</span></span> <span data-ttu-id="8e817-166">這個模式可讓使用者 tooselect 從哪些雲端 tooaccess 資源。</span><span class="sxs-lookup"><span data-stu-id="8e817-166">This mode enables users tooselect from which cloud tooaccess resources.</span></span>

<span data-ttu-id="8e817-167">tooenable 多雲端模式中，您必須 Azure 堆疊部署後執行 hello 新增 AzurePackConnector.ps1 指令碼。</span><span class="sxs-lookup"><span data-stu-id="8e817-167">tooenable multi-cloud mode, you must run hello Add-AzurePackConnector.ps1 script after Azure Stack deployment.</span></span> <span data-ttu-id="8e817-168">hello 下表描述 hello 指令碼參數。</span><span class="sxs-lookup"><span data-stu-id="8e817-168">hello following table describes hello script parameters.</span></span>


|  <span data-ttu-id="8e817-169">參數</span><span class="sxs-lookup"><span data-stu-id="8e817-169">Parameter</span></span> | <span data-ttu-id="8e817-170">說明</span><span class="sxs-lookup"><span data-stu-id="8e817-170">Description</span></span> | <span data-ttu-id="8e817-171">範例</span><span class="sxs-lookup"><span data-stu-id="8e817-171">Example</span></span> |   
| -------- | ------------- | ------- |  
| <span data-ttu-id="8e817-172">AzurePackClouds</span><span class="sxs-lookup"><span data-stu-id="8e817-172">AzurePackClouds</span></span> | <span data-ttu-id="8e817-173">Windows Azure Pack 連接器 hello 的 Uri。</span><span class="sxs-lookup"><span data-stu-id="8e817-173">URIs of hello Windows Azure Pack Connectors.</span></span> <span data-ttu-id="8e817-174">這些 Uri 應該對應 toohello Windows Azure Pack 租用戶入口網站。</span><span class="sxs-lookup"><span data-stu-id="8e817-174">These URIs should correspond toohello Windows Azure Pack tenant portals.</span></span> | <span data-ttu-id="8e817-175">@{CloudName = "AzurePack1"; CloudEndpoint = "https://waptenantportal1:40005"},@{CloudName = "AzurePack2"; CloudEndpoint = "https://waptenantportal2:40005"}</span><span class="sxs-lookup"><span data-stu-id="8e817-175">@{CloudName = "AzurePack1"; CloudEndpoint = "https://waptenantportal1:40005"},@{CloudName = "AzurePack2"; CloudEndpoint = "https://waptenantportal2:40005"}</span></span><br><br>  <span data-ttu-id="8e817-176">（根據預設，hello 連接埠值為 40005）。</span><span class="sxs-lookup"><span data-stu-id="8e817-176">(By default, hello port value is 40005.)</span></span> |  
| <span data-ttu-id="8e817-177">AzureStackCloudName</span><span class="sxs-lookup"><span data-stu-id="8e817-177">AzureStackCloudName</span></span> | <span data-ttu-id="8e817-178">標籤 toorepresent hello 本機堆疊 Azure 雲端。</span><span class="sxs-lookup"><span data-stu-id="8e817-178">Label toorepresent hello local Azure Stack cloud.</span></span>| <span data-ttu-id="8e817-179">"AzureStack"</span><span class="sxs-lookup"><span data-stu-id="8e817-179">"AzureStack"</span></span> |
| <span data-ttu-id="8e817-180">DisableMultiCloud</span><span class="sxs-lookup"><span data-stu-id="8e817-180">DisableMultiCloud</span></span> | <span data-ttu-id="8e817-181">交換器 toodisable 多雲端模式。</span><span class="sxs-lookup"><span data-stu-id="8e817-181">A switch toodisable multi-cloud mode.</span></span>| <span data-ttu-id="8e817-182">N/A</span><span class="sxs-lookup"><span data-stu-id="8e817-182">N/A</span></span> |
| | |

<span data-ttu-id="8e817-183">立即部署之後，或更新版本，您可以執行 hello 新增 AzurePackConnector.ps1 指令碼。</span><span class="sxs-lookup"><span data-stu-id="8e817-183">You can run hello Add-AzurePackConnector.ps1 script immediately after deployment, or later.</span></span> <span data-ttu-id="8e817-184">toorun hello 指令碼之後立即進行部署、 使用 hello 相同完成 Azure 堆疊部署所在的 Windows PowerShell 工作階段。</span><span class="sxs-lookup"><span data-stu-id="8e817-184">toorun hello script immediately after deployment, use hello same Windows PowerShell session where Azure Stack deployment completed.</span></span> <span data-ttu-id="8e817-185">否則，您可以開啟新的 Windows PowerShell 工作階段，以系統管理員身分 （登入為 hello azurestackadmin 帳戶）。</span><span class="sxs-lookup"><span data-stu-id="8e817-185">Otherwise, you can open a new Windows PowerShell session as an administrator (signed in as hello azurestackadmin account).</span></span>

1. <span data-ttu-id="8e817-186">使用下列命令 （具有值特定 tooyour 環境） 的 hello 執行 hello 新增 AzurePackConnector.ps1 指令碼。</span><span class="sxs-lookup"><span data-stu-id="8e817-186">Run hello Add-AzurePackConnector.ps1 script by using hello following commands (with values specific tooyour environment).</span></span> <span data-ttu-id="8e817-187">請注意，hello 新增 AzurePackConnector 指令碼可讓您 tooadd 多個 Windows Azure Pack 連接器端點。</span><span class="sxs-lookup"><span data-stu-id="8e817-187">Notice that hello Add-AzurePackConnector script enables you tooadd more than one Windows Azure Pack Connector endpoint.</span></span>
 
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
> <span data-ttu-id="8e817-188">Hello 目前組建中發生問題時的 hello 新增 AzurePackConnector 指令碼結束後，它會保留在輪詢迴圈長的時間 （幾分鐘的時間） 之前結束。</span><span class="sxs-lookup"><span data-stu-id="8e817-188">In hello current build there is an issue where after hello Add-AzurePackConnector script ends, it remains in a polling loop for an extended period of time (several minutes) until it ends.</span></span> <span data-ttu-id="8e817-189">您會看到 hello 訊息之後**VERBOSE： 步驟 「 設定 Azure Pack 連接器 」 狀態: 「 成功 」**，您可以停止 hello 指令碼，或等到它本身就會停止。</span><span class="sxs-lookup"><span data-stu-id="8e817-189">After you see hello message **VERBOSE: Step 'Configure Azure Pack Connector' status: 'Success'**, you can stop hello script or wait until it stops by itself.</span></span> <span data-ttu-id="8e817-190">因為 hello 組態已成功，它將不會有所差別。</span><span class="sxs-lookup"><span data-stu-id="8e817-190">It won’t make a difference because hello configuration has already succeeded.</span></span>

2. <span data-ttu-id="8e817-191">記下所產生的指令碼，為您指定每個 Windows Azure Pack 環境的 hello 輸出檔。</span><span class="sxs-lookup"><span data-stu-id="8e817-191">Make note of hello output files that are produced by this script, one for each Windows Azure Pack environment that you specified.</span></span> <span data-ttu-id="8e817-192">hello 檔位於： \\\su1fileserver\SU1_Infrastructure_1\AzurePackConnectorOutput。</span><span class="sxs-lookup"><span data-stu-id="8e817-192">hello files are located at:  \\\su1fileserver\SU1_Infrastructure_1\AzurePackConnectorOutput.</span></span> <span data-ttu-id="8e817-193">這些檔案包含必要的 tooconfigure hello 目標 Windows Azure Pack 環境的 hello 資訊。</span><span class="sxs-lookup"><span data-stu-id="8e817-193">These files contain hello information that is required tooconfigure hello target Windows Azure Pack environments.</span></span> <span data-ttu-id="8e817-194">您可以將此檔案當做參數 tooa 指令碼，這些指示中的更新版本。</span><span class="sxs-lookup"><span data-stu-id="8e817-194">You pass this file as a parameter tooa script later in these instructions.</span></span> <span data-ttu-id="8e817-195">這個檔案包含下列資訊的 hello:</span><span class="sxs-lookup"><span data-stu-id="8e817-195">This file contains hello following information:</span></span>

    * <span data-ttu-id="8e817-196">**AzurePackConnectorEndpoint**： 包含 hello 端點 toohello Windows Azure Pack 連接器服務。</span><span class="sxs-lookup"><span data-stu-id="8e817-196">**AzurePackConnectorEndpoint**: Contains hello endpoint toohello Windows Azure Pack Connector service.</span></span>
    * <span data-ttu-id="8e817-197">**AuthenticationIdentityProviderPartner**： 包含下列值組的 hello:</span><span class="sxs-lookup"><span data-stu-id="8e817-197">**AuthenticationIdentityProviderPartner**: Contains hello following value pair:</span></span>
        * <span data-ttu-id="8e817-198">驗證權杖簽章 hello Windows Azure Pack 租用戶 API 的憑證必須 tootrust tooaccept 呼叫從 hello Azure 堆疊入口網站擴充功能。</span><span class="sxs-lookup"><span data-stu-id="8e817-198">Authentication Token signing certificate that hello Windows Azure Pack Tenant API needs tootrust tooaccept calls from hello Azure Stack portal extension.</span></span>

        * <span data-ttu-id="8e817-199">hello"Realm"hello 簽署憑證與相關聯。</span><span class="sxs-lookup"><span data-stu-id="8e817-199">hello "Realm" associated with hello signing certificate.</span></span> <span data-ttu-id="8e817-200">例如：https://adfs.local.azurestack.global.external/adfs/c1d72562-534e-4aa5-92aa-d65df289a107/。</span><span class="sxs-lookup"><span data-stu-id="8e817-200">For example: https://adfs.local.azurestack.global.external/adfs/c1d72562-534e-4aa5-92aa-d65df289a107/.</span></span>

3.  <span data-ttu-id="8e817-201">包含 hello 輸出檔的瀏覽 toohello 資料夾 (\\su1fileserver\SU1_Infrastructure_1\AzurePackConnectorOutput)，並複製 hello 檔案 tooyour 本機電腦。</span><span class="sxs-lookup"><span data-stu-id="8e817-201">Browse toohello folder that contains hello output files (\\su1fileserver\SU1_Infrastructure_1\AzurePackConnectorOutput), and copy hello files tooyour local computer.</span></span> <span data-ttu-id="8e817-202">hello 檔案看起來類似 toothis: AzurePack-06-27-15-50.txt。</span><span class="sxs-lookup"><span data-stu-id="8e817-202">hello files will look similar toothis: AzurePack-06-27-15-50.txt.</span></span>

4.  <span data-ttu-id="8e817-203">測試 hello 組態。</span><span class="sxs-lookup"><span data-stu-id="8e817-203">Test hello configuration.</span></span>

    <span data-ttu-id="8e817-204">a.</span><span class="sxs-lookup"><span data-stu-id="8e817-204">a.</span></span> <span data-ttu-id="8e817-205">開啟瀏覽器，並登入 toohello Azure 堆疊使用者入口網站 (https://portal.local.azurestack.external/)。</span><span class="sxs-lookup"><span data-stu-id="8e817-205">Open your browser and sign in toohello Azure Stack user portal (https://portal.local.azurestack.external/).</span></span>
    
    <span data-ttu-id="8e817-206">b.</span><span class="sxs-lookup"><span data-stu-id="8e817-206">b.</span></span> <span data-ttu-id="8e817-207">為租用戶和 hello 入口網站載入登入之後，您會看到的錯誤不能 toofetch 訂閱或 hello Azure Pack 雲端擴充功能。</span><span class="sxs-lookup"><span data-stu-id="8e817-207">After you sign in as a tenant and hello portal loads, you'll see errors about not being able toofetch subscriptions or extensions from hello Azure Pack cloud.</span></span> <span data-ttu-id="8e817-208">按一下**確定**tooclose 這些訊息。</span><span class="sxs-lookup"><span data-stu-id="8e817-208">Click **OK** tooclose these messages.</span></span> <span data-ttu-id="8e817-209">(在您設定 Windows Azure 套件後這些錯誤訊息就會消失。)</span><span class="sxs-lookup"><span data-stu-id="8e817-209">(These error messages will go away after you configure Windows Azure Pack.)</span></span>

    <span data-ttu-id="8e817-210">c.</span><span class="sxs-lookup"><span data-stu-id="8e817-210">c.</span></span> <span data-ttu-id="8e817-211">請注意 hello**雲端**在 hello hello 入口網站的左上角的下拉式清單。</span><span class="sxs-lookup"><span data-stu-id="8e817-211">Notice hello **Cloud** drop-down list in hello upper-left corner of hello portal.</span></span>

    ![hello Azure 堆疊使用者介面中的 hello 雲端選取器](media/azure-stack-manage-wap/image3.png)

## <a name="configure-windows-azure-pack"></a><span data-ttu-id="8e817-213">設定 Windows Azure 套件</span><span class="sxs-lookup"><span data-stu-id="8e817-213">Configure Windows Azure Pack</span></span>
<span data-ttu-id="8e817-214">只有此預覽版本連接器需要手動設定 Windows Azure 套件。</span><span class="sxs-lookup"><span data-stu-id="8e817-214">For this Connector preview release only, Windows Azure Pack requires manual configuration.</span></span>

>[!IMPORTANT]
<span data-ttu-id="8e817-215">此預覽版本中，使用 hello Windows Azure Pack Connector 只在測試環境中，而不是在生產部署。</span><span class="sxs-lookup"><span data-stu-id="8e817-215">For this preview release, use hello Windows Azure Pack Connector only in test environments, and not in production deployments.</span></span>

1.  <span data-ttu-id="8e817-216">安裝連接器的 MSI 檔案 hello Windows Azure Pack 租用戶入口網站的虛擬機器，然後安裝憑證。</span><span class="sxs-lookup"><span data-stu-id="8e817-216">Install Connector MSI files on hello Windows Azure Pack tenant portal virtual machine, and install certificates.</span></span> <span data-ttu-id="8e817-217">(若您有多部租用戶入口網站虛擬機器，則必須在每部虛擬機器上都完成此步驟。)</span><span class="sxs-lookup"><span data-stu-id="8e817-217">(If you have multiple tenant portal virtual machines, you must complete this step on each virtual machine.)</span></span>

    <span data-ttu-id="8e817-218">a.</span><span class="sxs-lookup"><span data-stu-id="8e817-218">a.</span></span> <span data-ttu-id="8e817-219">在 檔案總管 中，複製 hello **WAPConnector** （什麼您之前下載） 的資料夾名為 tooa 資料夾**c:\temp** hello 租用戶入口網站的虛擬機器中。</span><span class="sxs-lookup"><span data-stu-id="8e817-219">In File Explorer, copy hello **WAPConnector** folder (what you downloaded earlier) tooa folder named **c:\temp** in hello tenant portal virtual machine.</span></span>

    <span data-ttu-id="8e817-220">b.</span><span class="sxs-lookup"><span data-stu-id="8e817-220">b.</span></span> <span data-ttu-id="8e817-221">開啟主控台或 RDP 連線 toohello 租用戶入口網站虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="8e817-221">Open a Console or RDP connection toohello tenant portal virtual machine.</span></span>

    <span data-ttu-id="8e817-222">c.</span><span class="sxs-lookup"><span data-stu-id="8e817-222">c.</span></span> <span data-ttu-id="8e817-223">將目錄變更太**c:\temp\wapconnector\setup\scripts**，並執行的 hello**安裝 Connector.ps1**指令碼 tooinstall 三 MSI 檔案。</span><span class="sxs-lookup"><span data-stu-id="8e817-223">Change directories too**c:\temp\wapconnector\setup\scripts**, and run hello **Install-Connector.ps1** script tooinstall three MSI files.</span></span> <span data-ttu-id="8e817-224">不需要任何參數。</span><span class="sxs-lookup"><span data-stu-id="8e817-224">No parameters are required.</span></span>

     ```powershell
    cd C:\temp\wapconnector\setup\scripts\

    .\Install-Connector.ps1
    ```
     <span data-ttu-id="8e817-225">d.</span><span class="sxs-lookup"><span data-stu-id="8e817-225">d.</span></span> <span data-ttu-id="8e817-226">將目錄變更太**c:\inetpub**並確認已安裝的 hello 三個新的站台：</span><span class="sxs-lookup"><span data-stu-id="8e817-226">Change directories too**c:\inetpub** and verify that hello three new sites are installed:</span></span>

       * <span data-ttu-id="8e817-227">MgmtSvc-Connector</span><span class="sxs-lookup"><span data-stu-id="8e817-227">MgmtSvc-Connector</span></span>

       * <span data-ttu-id="8e817-228">MgmtSvc-ConnectorExtension</span><span class="sxs-lookup"><span data-stu-id="8e817-228">MgmtSvc-ConnectorExtension</span></span>

       * <span data-ttu-id="8e817-229">MgmtSvc-ConnectorController</span><span class="sxs-lookup"><span data-stu-id="8e817-229">MgmtSvc-ConnectorController</span></span>

    <span data-ttu-id="8e817-230">e.</span><span class="sxs-lookup"><span data-stu-id="8e817-230">e.</span></span> <span data-ttu-id="8e817-231">從 hello 相同**c:\temp\wapconnector\setup\scripts**資料夾中，執行 hello**設定 Certificates.ps1** tooinstall 憑證編寫指令碼。</span><span class="sxs-lookup"><span data-stu-id="8e817-231">From hello same **c:\temp\wapconnector\setup\scripts** folder, run hello **Configure-Certificates.ps1** script tooinstall certificates.</span></span> <span data-ttu-id="8e817-232">根據預設，它會使用 hello 適用於在 Windows Azure Pack 中的 hello 租用戶入口網站的相同憑證。</span><span class="sxs-lookup"><span data-stu-id="8e817-232">By default, it will use hello same certificate that is available for hello Tenant Portal site in Windows Azure Pack.</span></span> <span data-ttu-id="8e817-233">請確定這是有效的憑證 （hello Azure 堆疊 AzS WASP01 虛擬機器和任何用戶端電腦存取 hello Azure 堆疊入口網站的信任）。</span><span class="sxs-lookup"><span data-stu-id="8e817-233">Make sure this is a valid certificate (trusted by hello Azure Stack AzS-WASP01 virtual machine and any client computer that accesses hello Azure Stack portal).</span></span> <span data-ttu-id="8e817-234">否則，通訊將無法運作。</span><span class="sxs-lookup"><span data-stu-id="8e817-234">Otherwise, communication won’t work.</span></span> <span data-ttu-id="8e817-235">(或者，您可以明確地傳遞憑證指紋做為參數使用 hello-憑證指紋參數。)</span><span class="sxs-lookup"><span data-stu-id="8e817-235">(Alternatively, you can explicitly pass a certificate thumbprint as a parameter by using hello -Thumbprint parameter.)</span></span>

     ```powershell
        cd C:\temp\wapconnector\setup\scripts\

        .\Configure-Certificates.ps1
    ```

    <span data-ttu-id="8e817-236">f.</span><span class="sxs-lookup"><span data-stu-id="8e817-236">f.</span></span> <span data-ttu-id="8e817-237">下列三種服務，執行 hello toofinish hello 組態**設定 WapConnector.ps1** tooupdate hello Web.config 檔案參數的指令碼。</span><span class="sxs-lookup"><span data-stu-id="8e817-237">toofinish hello configuration of these three services, run hello **Configure-WapConnector.ps1** script tooupdate hello Web.config file parameters.</span></span>

    |  <span data-ttu-id="8e817-238">參數</span><span class="sxs-lookup"><span data-stu-id="8e817-238">Parameter</span></span> | <span data-ttu-id="8e817-239">說明</span><span class="sxs-lookup"><span data-stu-id="8e817-239">Description</span></span> | <span data-ttu-id="8e817-240">範例</span><span class="sxs-lookup"><span data-stu-id="8e817-240">Example</span></span> |   
    | -------- | ------------- | ------- |  
    | <span data-ttu-id="8e817-241">TenantPortalFQDN</span><span class="sxs-lookup"><span data-stu-id="8e817-241">TenantPortalFQDN</span></span> | <span data-ttu-id="8e817-242">Windows Azure Pack 租用戶網站 FQDN hello。</span><span class="sxs-lookup"><span data-stu-id="8e817-242">hello Windows Azure Pack tenant portal FQDN.</span></span> | <span data-ttu-id="8e817-243">tenant.contoso.com</span><span class="sxs-lookup"><span data-stu-id="8e817-243">tenant.contoso.com</span></span> | 
    | <span data-ttu-id="8e817-244">TenantAPIFQDN</span><span class="sxs-lookup"><span data-stu-id="8e817-244">TenantAPIFQDN</span></span> | <span data-ttu-id="8e817-245">hello Windows Azure Pack 租用戶 API FQDN。</span><span class="sxs-lookup"><span data-stu-id="8e817-245">hello Windows Azure Pack Tenant API FQDN.</span></span> | <span data-ttu-id="8e817-246">tenantapi.contoso.com</span><span class="sxs-lookup"><span data-stu-id="8e817-246">tenantapi.contoso.com</span></span>  |
    | <span data-ttu-id="8e817-247">AzureStackPortalFQDN</span><span class="sxs-lookup"><span data-stu-id="8e817-247">AzureStackPortalFQDN</span></span> | <span data-ttu-id="8e817-248">hello Azure 堆疊使用者入口網站，FQDN。</span><span class="sxs-lookup"><span data-stu-id="8e817-248">hello Azure Stack user portal FQDN.</span></span> | <span data-ttu-id="8e817-249">portal.local.azurestack.external</span><span class="sxs-lookup"><span data-stu-id="8e817-249">portal.local.azurestack.external</span></span> |
    | | |
    
     ```powershell
    .\Configure-WapConnector.ps1 -TenantPortalFQDN "tenant.contoso.com" `
         -TenantAPIFQDN "tenantapi.contoso.com" `
         -AzureStackPortalFQDN "portal.local.azurestack.external"
    ```
    <span data-ttu-id="8e817-250">g.</span><span class="sxs-lookup"><span data-stu-id="8e817-250">g.</span></span> <span data-ttu-id="8e817-251">若您有多部租用戶入口網站虛擬機器，請在每部虛擬機器上重複步驟 1。</span><span class="sxs-lookup"><span data-stu-id="8e817-251">If you have multiple tenant portal virtual machines, repeat step 1 for each of these virtual machines.</span></span>

2. <span data-ttu-id="8e817-252">安裝 hello 每個 Windows Azure Pack 租用戶 API 虛擬機器上的新租用戶 API MSI。</span><span class="sxs-lookup"><span data-stu-id="8e817-252">Install hello new Tenant API MSI on each Windows Azure Pack Tenant API virtual machine.</span></span>

    <span data-ttu-id="8e817-253">a.</span><span class="sxs-lookup"><span data-stu-id="8e817-253">a.</span></span> <span data-ttu-id="8e817-254">如果負載平衡器正在使用中，您可能想 toomark hello 虛擬機器為離線狀態。</span><span class="sxs-lookup"><span data-stu-id="8e817-254">If a load balancer is in use, you may want toomark hello virtual machine as offline.</span></span>

    <span data-ttu-id="8e817-255">b.</span><span class="sxs-lookup"><span data-stu-id="8e817-255">b.</span></span> <span data-ttu-id="8e817-256">在 檔案總管 中，複製 hello **WAPConnector** tooa 資料夾名為**c:\temp**每個租用戶 API 的電腦上。</span><span class="sxs-lookup"><span data-stu-id="8e817-256">In File Explorer, copy hello **WAPConnector** folder tooa folder named **c:\temp** on each Tenant API machine.</span></span>

    <span data-ttu-id="8e817-257">c.</span><span class="sxs-lookup"><span data-stu-id="8e817-257">c.</span></span> <span data-ttu-id="8e817-258">複製 hello AzurePackConnectorOutput.txt 您稍早儲存檔案，太**c:\temp\WAPConnector**。</span><span class="sxs-lookup"><span data-stu-id="8e817-258">Copy hello AzurePackConnectorOutput.txt file that you saved earlier, too**c:\temp\WAPConnector**.</span></span>

    <span data-ttu-id="8e817-259">d.</span><span class="sxs-lookup"><span data-stu-id="8e817-259">d.</span></span> <span data-ttu-id="8e817-260">開啟主控台或 RDP 連線 toohello 租用戶 API VM 複製 hello 檔案。</span><span class="sxs-lookup"><span data-stu-id="8e817-260">Open a Console or RDP connection toohello Tenant API VM you copied hello files to.</span></span>
    
    <span data-ttu-id="8e817-261">e.</span><span class="sxs-lookup"><span data-stu-id="8e817-261">e.</span></span> <span data-ttu-id="8e817-262">將目錄變更太**c:\temp\wapconnector\setup\scripts**，並執行**更新 TenantAPI.ps1**。</span><span class="sxs-lookup"><span data-stu-id="8e817-262">Change directories too**c:\temp\wapconnector\setup\scripts**, and run **Update-TenantAPI.ps1**.</span></span> <span data-ttu-id="8e817-263">這個新版本的 hello WAP 租用戶 API 包含變更 tooenable 與 hello 目前 STS，不僅與 hello Azure 堆疊中的 AD FS 執行個體的信任關係。</span><span class="sxs-lookup"><span data-stu-id="8e817-263">This new version of hello WAP Tenant API contains a change tooenable a trust relationship not only with hello current STS, but also with hello instance of AD FS in Azure Stack.</span></span>

     ```powershell
    cd C:\temp\wapconnector\setup\packages\

    .\Update-TenantAPI.ps1
    ```

    <span data-ttu-id="8e817-264">f.</span><span class="sxs-lookup"><span data-stu-id="8e817-264">f.</span></span>  <span data-ttu-id="8e817-265">重複步驟 2 執行 hello 租用戶 API 的任何其他虛擬機器上。</span><span class="sxs-lookup"><span data-stu-id="8e817-265">Repeat step 2 on any other virtual machine running hello Tenant API.</span></span>
3. <span data-ttu-id="8e817-266">從**只有一個**的 hello 租用戶 API Vm，hello 設定 TrustAzureStack.ps1 指令碼 tooadd 信任關係之間 hello 租用戶 API 和 hello AD FS 執行個體上執行 Azure 堆疊。</span><span class="sxs-lookup"><span data-stu-id="8e817-266">From **only one** of hello Tenant API VMs, run hello Configure-TrustAzureStack.ps1 script tooadd a trust relationship between hello Tenant API and hello AD FS instance on Azure Stack.</span></span> <span data-ttu-id="8e817-267">您必須使用的帳戶具有系統管理員存取 toohello Microsoft.MgmtSvc.Store 資料庫複本。</span><span class="sxs-lookup"><span data-stu-id="8e817-267">You must use an account with sysadmin access toohello Microsoft.MgmtSvc.Store database.</span></span> <span data-ttu-id="8e817-268">此指令碼有 hello 下列參數：</span><span class="sxs-lookup"><span data-stu-id="8e817-268">This script has hello following parameters:</span></span>

    | <span data-ttu-id="8e817-269">參數</span><span class="sxs-lookup"><span data-stu-id="8e817-269">Parameter</span></span> | <span data-ttu-id="8e817-270">說明</span><span class="sxs-lookup"><span data-stu-id="8e817-270">Description</span></span> | <span data-ttu-id="8e817-271">範例</span><span class="sxs-lookup"><span data-stu-id="8e817-271">Example</span></span> |
    | --------- | ------------| ------- |
   | <span data-ttu-id="8e817-272">SqlServer</span><span class="sxs-lookup"><span data-stu-id="8e817-272">SqlServer</span></span> | <span data-ttu-id="8e817-273">hello hello 包含 hello Microsoft.MgmtSvc.Store 資料庫複本的 SQL Server 名稱。</span><span class="sxs-lookup"><span data-stu-id="8e817-273">hello name of hello SQL Server that contains hello Microsoft.MgmtSvc.Store database.</span></span> <span data-ttu-id="8e817-274">這是必要參數。</span><span class="sxs-lookup"><span data-stu-id="8e817-274">This parameter is required.</span></span> | <span data-ttu-id="8e817-275">SQLServer</span><span class="sxs-lookup"><span data-stu-id="8e817-275">SQLServer</span></span> | 
   | <span data-ttu-id="8e817-276">DataFile</span><span class="sxs-lookup"><span data-stu-id="8e817-276">DataFile</span></span> | <span data-ttu-id="8e817-277">在 hello hello Azure 堆疊多雲端之模式的組態稍早所產生的 hello 輸出檔。</span><span class="sxs-lookup"><span data-stu-id="8e817-277">hello output file that was generated during hello configuration of hello Azure Stack multi-cloud mode earlier.</span></span> <span data-ttu-id="8e817-278">這是必要參數。</span><span class="sxs-lookup"><span data-stu-id="8e817-278">This parameter is required.</span></span> | <span data-ttu-id="8e817-279">AzurePack-06-27-15-50.txt</span><span class="sxs-lookup"><span data-stu-id="8e817-279">AzurePack-06-27-15-50.txt</span></span> | 
   | <span data-ttu-id="8e817-280">PromptForSqlCredential</span><span class="sxs-lookup"><span data-stu-id="8e817-280">PromptForSqlCredential</span></span> | <span data-ttu-id="8e817-281">指出，hello 指令碼應該會提示您以互動方式的 SQL 驗證認證 toouse 連接 toohello SQL Server 執行個體時。</span><span class="sxs-lookup"><span data-stu-id="8e817-281">Indicates that hello script should prompt you interactively for a SQL Authentication credential toouse when connecting toohello SQL Server instance.</span></span> <span data-ttu-id="8e817-282">指定認證的 hello 必須有足夠的權限 toouninstall 資料庫，結構描述，並刪除使用者登入。</span><span class="sxs-lookup"><span data-stu-id="8e817-282">hello given credential must have sufficient permissions toouninstall databases, schemas, and delete user logins.</span></span> <span data-ttu-id="8e817-283">如果未提供，hello 指令碼會假設該目前使用者的內容有權存取。</span><span class="sxs-lookup"><span data-stu-id="8e817-283">If none is provided, hello script assumes that current user context has access.</span></span> | <span data-ttu-id="8e817-284">不需要任何值。</span><span class="sxs-lookup"><span data-stu-id="8e817-284">No value is needed.</span></span> |
   |  |  |

    <span data-ttu-id="8e817-285">如果您不知道 hello SQL Server toouse，您就可以進行探索。</span><span class="sxs-lookup"><span data-stu-id="8e817-285">If you don't know hello SQL Server toouse, you can discover it.</span></span> <span data-ttu-id="8e817-286">Toohello 租用戶 API 的電腦連線、 使用 hello Unprotect Mgmtsvc-adminsite 命令 toounprotect hello 租用戶 API Web.config 檔案中，並尋找 hello hello 連接字串中的伺服器名稱。</span><span class="sxs-lookup"><span data-stu-id="8e817-286">Connect toohello Tenant API computer, use hello Unprotect-MgmtSvc command toounprotect hello Tenant API Web.config file, and look for hello server name in hello connection string.</span></span> <span data-ttu-id="8e817-287">請記住 toorun 保護 Mgmtsvc-adminsite 再次 tooprotect hello 租用戶 API Web.config 檔案。</span><span class="sxs-lookup"><span data-stu-id="8e817-287">Remember toorun Protect-MgmtSvc again tooprotect hello Tenant API Web.config file.</span></span>

  ```powershell
  cd C:\temp\wapconnector\setup\scripts\

 .\Configure-TrustAzureStack.ps1 -SqlServer "SQLServer" `
       -DataFile "C:\temp\wapconnector\AzurePackConnectorOutput.txt"
  ```

## <a name="example"></a><span data-ttu-id="8e817-288">範例</span><span class="sxs-lookup"><span data-stu-id="8e817-288">Example</span></span>
<span data-ttu-id="8e817-289">hello 下列範例顯示完整的 Windows Azure Pack Connector 部署在單一節點 Azure 堆疊設定，以及兩個 Windows Azure Pack Express 安裝。</span><span class="sxs-lookup"><span data-stu-id="8e817-289">hello following example shows a complete Windows Azure Pack Connector deployment on a single-node Azure Stack configuration and two Windows Azure Pack Express installations.</span></span> <span data-ttu-id="8e817-290">(每個快速安裝位於單一電腦上，與 hello 範例名稱*wapcomputer1*和*wapcomputer2*。)</span><span class="sxs-lookup"><span data-stu-id="8e817-290">(Each Express installation is on a single computer, with hello example names *wapcomputer1* and*wapcomputer2*.)</span></span>

```powershell
# Run hello following script on hello Azure Stack host
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
<span data-ttu-id="8e817-291">從 hello 下載 hello.exe 檔案[Microsoft Download Center](https://aka.ms/wapconnectorazurestackdlc)，將它解壓縮，並將複製 hello WAPConnector 資料夾 tooa **c:\temp** hello Windows Azure Pack 的電腦上的資料夾。</span><span class="sxs-lookup"><span data-stu-id="8e817-291">Download hello .exe file from hello [Microsoft Download Center](https://aka.ms/wapconnectorazurestackdlc), extract it, and copy hello WAPConnector folder tooa **c:\temp** folder on hello Windows Azure Pack computer.</span></span> <span data-ttu-id="8e817-292">複製產生做為輸出 hello 至上一個指令碼中的 hello 檔案 (位於\\\su1fileserver\SU1_Infrastructure_1\AzurePackConnectorOutput) toohello **c:\temp\WAPConnector**資料夾。</span><span class="sxs-lookup"><span data-stu-id="8e817-292">Copy hello files that were generated as output in hello previous script (located at \\\su1fileserver\SU1_Infrastructure_1\AzurePackConnectorOutput) toohello **c:\temp\WAPConnector** folder.</span></span> <span data-ttu-id="8e817-293">(hello 檔案會看起來類似 toothis: AzurePack-06-27-15-50.txt。)然後，執行下列指令碼中，每一次的執行個體的 Windows Azure 套件 hello:</span><span class="sxs-lookup"><span data-stu-id="8e817-293">(hello files will looks similar toothis: AzurePack-06-27-15-50.txt.) Then, run hello following script, once per instance of Windows Azure Pack:</span></span>

 ```powershell
# Install Connector components
cd C:\temp\WAPConnector\Setup\Scripts
.\Install-Connector.ps1

# Configure Certificates for hello new Connector services
.\Configure-Certificates.ps1

# Configure hello Connector services
.\Configure-WapConnector.ps1 -TenantPortalFQDN "wapcomputer1.contoso.com" `
     -TenantAPIFQDN "wapcomputer1.contoso.com" `
     -AzureStackPortalFQDN "portal.local.azurestack.external"

# Install hello updated TenantAPI
.\Update-TenantAPI.ps1

# Establish trust with hello Azure Stack AD FS
.\Configure-TrustAzureStack.ps1 -SqlServer "wapcomputer1" `
     -DataFile "C:\temp\wapconnector\AzurePack-06-27-15-50.txt" 

```
## <a name="troubleshooting-tips"></a><span data-ttu-id="8e817-294">疑難排解秘訣</span><span class="sxs-lookup"><span data-stu-id="8e817-294">Troubleshooting tips</span></span>
1.  <span data-ttu-id="8e817-295">確保 Azure Stack 與 Windows Azure 套件之間有網路連線能力。</span><span class="sxs-lookup"><span data-stu-id="8e817-295">Ensure there is network connectivity between Azure Stack and Windows Azure Pack.</span></span> <span data-ttu-id="8e817-296">此連接應該是任何存取 hello Azure 堆疊入口網站的租用戶電腦與 hello Windows Azure Pack 租用戶入口網站虛擬機器之間執行 hello 新連接器服務。</span><span class="sxs-lookup"><span data-stu-id="8e817-296">This connectivity should be between any tenant computer that accesses hello Azure Stack portal and hello Windows Azure Pack tenant portal virtual machine where hello new Connector services are running.</span></span>
2.  <span data-ttu-id="8e817-297">確保所有指定的 FQDN 都正確。</span><span class="sxs-lookup"><span data-stu-id="8e817-297">Ensure that all specified FQDNs are correct.</span></span>
3.  <span data-ttu-id="8e817-298">請確定 hello hello 新連接器服務中使用的 SSL 憑證信任由 Azure 堆疊 (特別是 hello AzS WASP01 VM)，而且任何其他電腦 hello 租用戶可以使用 tooaccess hello Azure 堆疊使用者入口網站。</span><span class="sxs-lookup"><span data-stu-id="8e817-298">Ensure that hello SSL certificates used in hello new Connector services are trusted by Azure Stack (specifically hello AzS-WASP01 VM) and any other computer hello tenant may use tooaccess hello Azure Stack user portal.</span></span>
4. <span data-ttu-id="8e817-299">若要檢閱已知的問題，請參閱 [Microsoft Azure Stack 疑難排解](azure-stack-troubleshooting.md)。</span><span class="sxs-lookup"><span data-stu-id="8e817-299">For known issues, see [Microsoft Azure Stack troubleshooting](azure-stack-troubleshooting.md).</span></span>


## <a name="next-steps"></a><span data-ttu-id="8e817-300">後續步驟</span><span class="sxs-lookup"><span data-stu-id="8e817-300">Next steps</span></span>
[<span data-ttu-id="8e817-301">使用 Azure 堆疊中的 hello 系統管理員和使用者入口網站</span><span class="sxs-lookup"><span data-stu-id="8e817-301">Using hello administrator and user portals in Azure Stack</span></span>](azure-stack-manage-portals.md)
