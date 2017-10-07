---
title: "aaaConnect tooAzure 堆疊 |Microsoft 文件"
description: "深入了解如何 tooconnect Azure 堆疊"
services: azure-stack
documentationcenter: 
author: SnehaGunda
manager: byronr
editor: 
ms.assetid: 3cebbfa6-819a-41e3-9f1b-14ca0a2aaba3
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 08/22/2017
ms.author: sngun
ms.openlocfilehash: 8a940245fbcc8795d26b694df66824f0eb1dc3ea
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="connect-tooazure-stack"></a><span data-ttu-id="86802-103">連接 tooAzure 堆疊</span><span class="sxs-lookup"><span data-stu-id="86802-103">Connect tooAzure Stack</span></span>

<span data-ttu-id="86802-104">toomanage 資源，您必須連接 toohello Azure 堆疊開發套件。</span><span class="sxs-lookup"><span data-stu-id="86802-104">toomanage resources, you must connect toohello Azure Stack Development Kit.</span></span> <span data-ttu-id="86802-105">此主題的詳細資料 hello 步驟需要 tooconnect toohello 開發套件。</span><span class="sxs-lookup"><span data-stu-id="86802-105">This topic details hello steps required tooconnect toohello development kit.</span></span> <span data-ttu-id="86802-106">您可以使用其中一個 hello 下列連接選項：</span><span class="sxs-lookup"><span data-stu-id="86802-106">You can use either of hello following connection options:</span></span>

* <span data-ttu-id="86802-107">[遠端桌面](#connect-with-remote-desktop)： 可讓單一並行使用者快速地連接從 hello 開發套件。</span><span class="sxs-lookup"><span data-stu-id="86802-107">[Remote Desktop](#connect-with-remote-desktop): lets a single concurrent user quickly connect from hello development kit.</span></span>
* <span data-ttu-id="86802-108">[虛擬私人網路 (VPN)](#connect-with-vpn)： 可讓多位使用者同時連接從用戶端以外 hello Azure 堆疊基礎結構 （需要組態）。</span><span class="sxs-lookup"><span data-stu-id="86802-108">[Virtual Private Network (VPN)](#connect-with-vpn): lets multiple concurrent users connect from clients outside of hello Azure Stack infrastructure (requires configuration).</span></span>

## <a name="connect-tooazure-stack-with-remote-desktop"></a><span data-ttu-id="86802-109">使用遠端桌面連線 tooAzure 堆疊</span><span class="sxs-lookup"><span data-stu-id="86802-109">Connect tooAzure Stack with Remote Desktop</span></span>
<span data-ttu-id="86802-110">使用遠端桌面連線，hello 入口 toomanage 資源可以處理單一的並行使用者。</span><span class="sxs-lookup"><span data-stu-id="86802-110">With a Remote Desktop connection, a single concurrent user can work with hello portal toomanage resources.</span></span>

1. <span data-ttu-id="86802-111">開啟 遠端桌面連線並連線 toohello 開發套件。</span><span class="sxs-lookup"><span data-stu-id="86802-111">Open a Remote Desktop Connection and connect toohello development kit.</span></span> <span data-ttu-id="86802-112">輸入**AzureStack\AzureStackAdmin** hello 使用者名稱，以及 hello Azure 堆疊安裝過程中提供的系統管理密碼。</span><span class="sxs-lookup"><span data-stu-id="86802-112">Enter **AzureStack\AzureStackAdmin** as hello username, and hello administrative password that you provided during Azure Stack setup.</span></span>  

2. <span data-ttu-id="86802-113">從 hello 開發套件的電腦，開啟伺服器管理員 中，按一下 **本機伺服器**，關閉 Internet Explorer 增強式安全性，，然後再關閉伺服器管理員。</span><span class="sxs-lookup"><span data-stu-id="86802-113">From hello development kit computer, open Server Manager, click **Local Server**, turn off Internet Explorer Enhanced Security, and then close Server Manager.</span></span>

3. <span data-ttu-id="86802-114">tooopen hello 使用者[入口網站](azure-stack-key-features.md#portal)，瀏覽過 (https://portal.local.azurestack.external/) 並使用使用者認證登入。</span><span class="sxs-lookup"><span data-stu-id="86802-114">tooopen hello user [portal](azure-stack-key-features.md#portal), navigate too(https://portal.local.azurestack.external/) and sign in using user credentials.</span></span> <span data-ttu-id="86802-115">tooopen hello 管理員[入口網站](azure-stack-key-features.md#portal)，瀏覽過 (https://adminportal.local.azurestack.external/) 和登入使用 hello 在安裝期間指定的 Azure Active Directory 認證。</span><span class="sxs-lookup"><span data-stu-id="86802-115">tooopen hello administrator [portal](azure-stack-key-features.md#portal), navigate too(https://adminportal.local.azurestack.external/) and sign in using hello Azure Active Directory credentials specified during installation.</span></span>

## <a name="connect-tooazure-stack-with-vpn"></a><span data-ttu-id="86802-116">使用 VPN 連線 tooAzure 堆疊</span><span class="sxs-lookup"><span data-stu-id="86802-116">Connect tooAzure Stack with VPN</span></span>

<span data-ttu-id="86802-117">您可以建立分割通道虛擬私人網路 (VPN) 連線 tooan Azure 堆疊開發套件。</span><span class="sxs-lookup"><span data-stu-id="86802-117">You can establish a split tunnel Virtual Private Network (VPN) connection tooan Azure Stack Development Kit.</span></span> <span data-ttu-id="86802-118">透過 hello VPN 連線，您可以存取 hello 管理員入口網站，使用者入口網站，及本機上安裝工具，例如 Visual Studio 和 PowerShell toomanage 堆疊 Azure 資源。</span><span class="sxs-lookup"><span data-stu-id="86802-118">Through hello VPN connection, you can access hello administrator portal, user portal, and locally installed tools such as Visual Studio and PowerShell toomanage Azure Stack resources.</span></span> <span data-ttu-id="86802-119">Azure Active Directory(AAD) 和「Active Directory 同盟服務」(AD FS) 型部署都支援 VPN 連線。</span><span class="sxs-lookup"><span data-stu-id="86802-119">VPN connectivity is supported in both Azure Active Directory(AAD) and Active Directory Federation Services(AD FS) based deployments.</span></span> <span data-ttu-id="86802-120">VPN 連線可讓在 hello 的多個用戶端 tooconnect tooAzure 堆疊相同的時間。</span><span class="sxs-lookup"><span data-stu-id="86802-120">VPN connections enable multiple clients tooconnect tooAzure Stack at hello same time.</span></span> 

> [!NOTE] 
> <span data-ttu-id="86802-121">此 VPN 連線不提供連線 tooAzure 堆疊基礎結構的 Vm。</span><span class="sxs-lookup"><span data-stu-id="86802-121">This VPN connection does not provide connectivity tooAzure Stack infrastructure VMs.</span></span> 

### <a name="prerequisites"></a><span data-ttu-id="86802-122">必要條件</span><span class="sxs-lookup"><span data-stu-id="86802-122">Prerequisites</span></span>

* <span data-ttu-id="86802-123">在您的本機電腦上安裝 [Azure Stack 相容的 Azure PowerShell](azure-stack-powershell-install.md)。</span><span class="sxs-lookup"><span data-stu-id="86802-123">Install [Azure Stack compatible Azure PowerShell](azure-stack-powershell-install.md) on your local computer.</span></span>  
* <span data-ttu-id="86802-124">下載 hello [Azure 堆疊的工具需要的 toowork](azure-stack-powershell-download.md)。</span><span class="sxs-lookup"><span data-stu-id="86802-124">Download hello [tools required toowork with Azure Stack](azure-stack-powershell-download.md).</span></span> 

### <a name="configure-vpn-connectivity"></a><span data-ttu-id="86802-125">設定 VPN 連線</span><span class="sxs-lookup"><span data-stu-id="86802-125">Configure VPN connectivity</span></span>

<span data-ttu-id="86802-126">toocreate VPN 連線 toohello 開發套件，開啟提升權限的 PowerShell 工作階段，從您的本機 Windows 為基礎的電腦和執行下列指令碼 （請確定 tooupdate hello hello IP 位址和密碼值為您的環境） 的 hello:</span><span class="sxs-lookup"><span data-stu-id="86802-126">toocreate a VPN connection toohello development kit, open an elevated PowerShell session from your local Windows-based computer and run hello following script (make sure tooupdate hello hello IP address and password values for your environment):</span></span>

```PowerShell 
# Configure winrm if it's not already configured
winrm quickconfig  

Set-ExecutionPolicy RemoteSigned

# Import hello Connect module
Import-Module .\Connect\AzureStack.Connect.psm1 

# Add hello development kit computer’s host IP address & certificate authority (CA) toohello list of trusted hosts. Make sure tooupdate hello hello IP address and password values for your environment. 

$hostIP = "<Azure Stack host IP address>"

$Password = ConvertTo-SecureString `
  "<Administrator password provided when deploying Azure Stack>" `
  -AsPlainText `
  -Force

Set-Item wsman:\localhost\Client\TrustedHosts `
  -Value $hostIP `
  -Concatenate

# Create a VPN connection entry for hello local user
Add-AzsVpnConnection `
  -ServerAddress $hostIP `
  -Password $Password

```

<span data-ttu-id="86802-127">如果 hello 設定成功，您應該會看到**azurestack**清單中的 VPN 連線。</span><span class="sxs-lookup"><span data-stu-id="86802-127">If hello set up succeeds, you should see **azurestack** in your list of VPN connections.</span></span>

![網路連線](media/azure-stack-connect-azure-stack/image3.png)  

### <a name="connect-tooazure-stack"></a><span data-ttu-id="86802-129">連接 tooAzure 堆疊</span><span class="sxs-lookup"><span data-stu-id="86802-129">Connect tooAzure Stack</span></span>

<span data-ttu-id="86802-130">使用下列兩種方法的 hello 任一連接 toohello Azure 堆疊的執行個體：</span><span class="sxs-lookup"><span data-stu-id="86802-130">Connect toohello Azure Stack instance by using either of hello following two methods:</span></span>  

* <span data-ttu-id="86802-131">使用 hello`Connect-AzsVpn `命令：</span><span class="sxs-lookup"><span data-stu-id="86802-131">By using hello `Connect-AzsVpn ` command:</span></span> 
    
  ```PowerShell
  Connect-AzsVpn `
    -Password $Password
  ```

  <span data-ttu-id="86802-132">出現提示時，信任 hello Azure 堆疊主控件，並安裝來自 hello 憑證**AzureStackCertificateAuthority**到本機電腦憑證存放區。</span><span class="sxs-lookup"><span data-stu-id="86802-132">When prompted, trust hello Azure Stack host and install hello certificate from **AzureStackCertificateAuthority** onto your local computer’s certificate store.</span></span> <span data-ttu-id="86802-133">（hello 提示可能會出現在 hello PowerShell 工作階段視窗後面）。</span><span class="sxs-lookup"><span data-stu-id="86802-133">(hello prompt might appear behind hello PowerShell session window).</span></span> 

* <span data-ttu-id="86802-134">開啟您本機電腦的 [網路設定] > [VPN] > 按一下 [azurestack] > [連線]。</span><span class="sxs-lookup"><span data-stu-id="86802-134">Open your local computer’s **Network Settings** > **VPN** > click **azurestack** > **connect**.</span></span> <span data-ttu-id="86802-135">Hello 登入提示字元之下，輸入 hello 使用者名稱 (AzureStack\AzureStackAdmin) 和 hello 密碼。</span><span class="sxs-lookup"><span data-stu-id="86802-135">At hello sign-in prompt, enter hello username (AzureStack\AzureStackAdmin) and hello password.</span></span>

### <a name="test-hello-vpn-connectivity"></a><span data-ttu-id="86802-136">測試 hello VPN 連線能力</span><span class="sxs-lookup"><span data-stu-id="86802-136">Test hello VPN connectivity</span></span>

<span data-ttu-id="86802-137">tootest hello 入口網站連線，請開啟網際網路瀏覽器和瀏覽 tooeither hello 使用者入口網站 (https://portal.local.azurestack.external/) 或 hello 管理員入口網站 (https://adminportal.local.azurestack.external/)、 登入並建立資源。</span><span class="sxs-lookup"><span data-stu-id="86802-137">tootest hello portal connection, open an Internet browser and navigate tooeither hello user portal (https://portal.local.azurestack.external/) or hello administrator portal (https://adminportal.local.azurestack.external/), sign in and create resources.</span></span>  

## <a name="next-steps"></a><span data-ttu-id="86802-138">後續步驟</span><span class="sxs-lookup"><span data-stu-id="86802-138">Next steps</span></span>

[<span data-ttu-id="86802-139">讓虛擬機器可用 tooyour Azure 堆疊使用者</span><span class="sxs-lookup"><span data-stu-id="86802-139">Make virtual machines available tooyour Azure Stack users</span></span>](azure-stack-tutorial-tenant-vm.md)

