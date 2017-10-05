---
title: "連線到 Azure Stack | Microsoft Docs"
description: "了解如何連線到 Azure Stack"
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
ms.openlocfilehash: 44b167972ceffc8de48ae7560b85009a96378144
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="connect-to-azure-stack"></a><span data-ttu-id="618e3-103">連線至 Azure Stack</span><span class="sxs-lookup"><span data-stu-id="618e3-103">Connect to Azure Stack</span></span>

<span data-ttu-id="618e3-104">若要管理資源，您必須連線到「Azure Stack 開發套件」。</span><span class="sxs-lookup"><span data-stu-id="618e3-104">To manage resources, you must connect to the Azure Stack Development Kit.</span></span> <span data-ttu-id="618e3-105">此主題將詳細說明連線到開發套件所需的步驟。</span><span class="sxs-lookup"><span data-stu-id="618e3-105">This topic details the steps required to connect to the development kit.</span></span> <span data-ttu-id="618e3-106">您可以使用下列其中一個連線選項：</span><span class="sxs-lookup"><span data-stu-id="618e3-106">You can use either of the following connection options:</span></span>

* <span data-ttu-id="618e3-107">[遠端桌面](#connect-with-remote-desktop)：可讓單一並行使用者從開發套件快速連線。</span><span class="sxs-lookup"><span data-stu-id="618e3-107">[Remote Desktop](#connect-with-remote-desktop): lets a single concurrent user quickly connect from the development kit.</span></span>
* <span data-ttu-id="618e3-108">[虛擬私人網路 (VPN)](#connect-with-vpn)：可讓多個並行使用者從 Azure Stack 基礎結構外部的用戶端連線 (需要設定)。</span><span class="sxs-lookup"><span data-stu-id="618e3-108">[Virtual Private Network (VPN)](#connect-with-vpn): lets multiple concurrent users connect from clients outside of the Azure Stack infrastructure (requires configuration).</span></span>

## <a name="connect-to-azure-stack-with-remote-desktop"></a><span data-ttu-id="618e3-109">使用遠端桌面來連線到 Azure Stack</span><span class="sxs-lookup"><span data-stu-id="618e3-109">Connect to Azure Stack with Remote Desktop</span></span>
<span data-ttu-id="618e3-110">使用「遠端桌面」連線時，單一並行使用者可以使用入口網站來管理資源。</span><span class="sxs-lookup"><span data-stu-id="618e3-110">With a Remote Desktop connection, a single concurrent user can work with the portal to manage resources.</span></span>

1. <span data-ttu-id="618e3-111">開啟一個「遠端桌面連線」並連線到開發套件。</span><span class="sxs-lookup"><span data-stu-id="618e3-111">Open a Remote Desktop Connection and connect to the development kit.</span></span> <span data-ttu-id="618e3-112">輸入**AzureStack\AzureStackAdmin**做為使用者名稱，以及 Azure 堆疊安裝過程中提供的系統管理密碼。</span><span class="sxs-lookup"><span data-stu-id="618e3-112">Enter **AzureStack\AzureStackAdmin** as the username, and the administrative password that you provided during Azure Stack setup.</span></span>  

2. <span data-ttu-id="618e3-113">從開發套件電腦開啟 [伺服器管理員]，按一下 [本機伺服器]、關閉 [Internet Explorer 增強式安全性]，然後關閉 [伺服器管理員]。</span><span class="sxs-lookup"><span data-stu-id="618e3-113">From the development kit computer, open Server Manager, click **Local Server**, turn off Internet Explorer Enhanced Security, and then close Server Manager.</span></span>

3. <span data-ttu-id="618e3-114">若要開啟使用者[入口網站](azure-stack-key-features.md#portal)，請瀏覽至 (https://portal.local.azurestack.external/)，然後使用使用者認證登入。</span><span class="sxs-lookup"><span data-stu-id="618e3-114">To open the user [portal](azure-stack-key-features.md#portal), navigate to (https://portal.local.azurestack.external/) and sign in using user credentials.</span></span> <span data-ttu-id="618e3-115">若要開啟系統管理員[入口網站](azure-stack-key-features.md#portal)、 瀏覽至 (https://adminportal.local.azurestack.external/)，並使用在安裝期間指定的 Azure Active Directory 認證登入。</span><span class="sxs-lookup"><span data-stu-id="618e3-115">To open the administrator [portal](azure-stack-key-features.md#portal), navigate to (https://adminportal.local.azurestack.external/) and sign in using the Azure Active Directory credentials specified during installation.</span></span>

## <a name="connect-to-azure-stack-with-vpn"></a><span data-ttu-id="618e3-116">使用 VPN 來連線到 Azure Stack</span><span class="sxs-lookup"><span data-stu-id="618e3-116">Connect to Azure Stack with VPN</span></span>

<span data-ttu-id="618e3-117">您可以建立一個連至「Azure Stack 開發套件」的分割通道「虛擬私人網路」(VPN) 連線。</span><span class="sxs-lookup"><span data-stu-id="618e3-117">You can establish a split tunnel Virtual Private Network (VPN) connection to an Azure Stack Development Kit.</span></span> <span data-ttu-id="618e3-118">透過 VPN 連線，您可以存取系統管理員入口網站中，使用者入口網站，並在本機安裝工具，例如 Visual Studio 和 PowerShell 管理 Azure 堆疊資源。</span><span class="sxs-lookup"><span data-stu-id="618e3-118">Through the VPN connection, you can access the administrator portal, user portal, and locally installed tools such as Visual Studio and PowerShell to manage Azure Stack resources.</span></span> <span data-ttu-id="618e3-119">Azure Active Directory(AAD) 和「Active Directory 同盟服務」(AD FS) 型部署都支援 VPN 連線。</span><span class="sxs-lookup"><span data-stu-id="618e3-119">VPN connectivity is supported in both Azure Active Directory(AAD) and Active Directory Federation Services(AD FS) based deployments.</span></span> <span data-ttu-id="618e3-120">VPN 連線可讓多個用戶端同時連線到 Azure Stack。</span><span class="sxs-lookup"><span data-stu-id="618e3-120">VPN connections enable multiple clients to connect to Azure Stack at the same time.</span></span> 

> [!NOTE] 
> <span data-ttu-id="618e3-121">這個 VPN 連線並無法連線到 Azure Stack 基礎結構 VM。</span><span class="sxs-lookup"><span data-stu-id="618e3-121">This VPN connection does not provide connectivity to Azure Stack infrastructure VMs.</span></span> 

### <a name="prerequisites"></a><span data-ttu-id="618e3-122">必要條件</span><span class="sxs-lookup"><span data-stu-id="618e3-122">Prerequisites</span></span>

* <span data-ttu-id="618e3-123">在您的本機電腦上安裝 [Azure Stack 相容的 Azure PowerShell](azure-stack-powershell-install.md)。</span><span class="sxs-lookup"><span data-stu-id="618e3-123">Install [Azure Stack compatible Azure PowerShell](azure-stack-powershell-install.md) on your local computer.</span></span>  
* <span data-ttu-id="618e3-124">下載[處理 Azure Stack 所需的工具](azure-stack-powershell-download.md)。</span><span class="sxs-lookup"><span data-stu-id="618e3-124">Download the [tools required to work with Azure Stack](azure-stack-powershell-download.md).</span></span> 

### <a name="configure-vpn-connectivity"></a><span data-ttu-id="618e3-125">設定 VPN 連線</span><span class="sxs-lookup"><span data-stu-id="618e3-125">Configure VPN connectivity</span></span>

<span data-ttu-id="618e3-126">若要建立連至開發套件的 VPN 連線，請從您的本機 Windows 型電腦開啟已提高權限的 PowerShell 工作階段，然後執行下列指令碼 (請務必針對您的環境更新 IP 位址和密碼值)：</span><span class="sxs-lookup"><span data-stu-id="618e3-126">To create a VPN connection to the development kit, open an elevated PowerShell session from your local Windows-based computer and run the following script (make sure to update the the IP address and password values for your environment):</span></span>

```PowerShell 
# Configure winrm if it's not already configured
winrm quickconfig  

Set-ExecutionPolicy RemoteSigned

# Import the Connect module
Import-Module .\Connect\AzureStack.Connect.psm1 

# Add the development kit computer’s host IP address & certificate authority (CA) to the list of trusted hosts. Make sure to update the the IP address and password values for your environment. 

$hostIP = "<Azure Stack host IP address>"

$Password = ConvertTo-SecureString `
  "<Administrator password provided when deploying Azure Stack>" `
  -AsPlainText `
  -Force

Set-Item wsman:\localhost\Client\TrustedHosts `
  -Value $hostIP `
  -Concatenate

# Create a VPN connection entry for the local user
Add-AzsVpnConnection `
  -ServerAddress $hostIP `
  -Password $Password

```

<span data-ttu-id="618e3-127">如果設定成功，您應該會在 VPN 連線清單中看到 **azurestack**。</span><span class="sxs-lookup"><span data-stu-id="618e3-127">If the set up succeeds, you should see **azurestack** in your list of VPN connections.</span></span>

![網路連線](media/azure-stack-connect-azure-stack/image3.png)  

### <a name="connect-to-azure-stack"></a><span data-ttu-id="618e3-129">連線至 Azure Stack</span><span class="sxs-lookup"><span data-stu-id="618e3-129">Connect to Azure Stack</span></span>

<span data-ttu-id="618e3-130">請使用下列兩種方法之一來連線到 Azure Stack 執行個體：</span><span class="sxs-lookup"><span data-stu-id="618e3-130">Connect to the Azure Stack instance by using either of the following two methods:</span></span>  

* <span data-ttu-id="618e3-131">透過使用 `Connect-AzsVpn ` 命令：</span><span class="sxs-lookup"><span data-stu-id="618e3-131">By using the `Connect-AzsVpn ` command:</span></span> 
    
  ```PowerShell
  Connect-AzsVpn `
    -Password $Password
  ```

  <span data-ttu-id="618e3-132">出現提示時，請信任 Azure Stack 主機，然後將來自 **AzureStackCertificateAuthority** 的憑證安裝到您本機電腦的憑證存放區中。</span><span class="sxs-lookup"><span data-stu-id="618e3-132">When prompted, trust the Azure Stack host and install the certificate from **AzureStackCertificateAuthority** onto your local computer’s certificate store.</span></span> <span data-ttu-id="618e3-133">(提示可能會出現在 PowerShell 工作階段視窗後面)。</span><span class="sxs-lookup"><span data-stu-id="618e3-133">(the prompt might appear behind the PowerShell session window).</span></span> 

* <span data-ttu-id="618e3-134">開啟您本機電腦的 [網路設定] > [VPN] > 按一下 [azurestack] > [連線]。</span><span class="sxs-lookup"><span data-stu-id="618e3-134">Open your local computer’s **Network Settings** > **VPN** > click **azurestack** > **connect**.</span></span> <span data-ttu-id="618e3-135">出現登入提示時，輸入使用者名稱 (AzureStack\AzureStackAdmin) 和密碼。</span><span class="sxs-lookup"><span data-stu-id="618e3-135">At the sign-in prompt, enter the username (AzureStack\AzureStackAdmin) and the password.</span></span>

### <a name="test-the-vpn-connectivity"></a><span data-ttu-id="618e3-136">測試 VPN 連線</span><span class="sxs-lookup"><span data-stu-id="618e3-136">Test the VPN connectivity</span></span>

<span data-ttu-id="618e3-137">若要測試的入口網站的連線，開啟網際網路瀏覽器和瀏覽至使用者入口網站 (https://portal.local.azurestack.external/) 或系統管理員入口網站 (https://adminportal.local.azurestack.external/)、 登入和建立資源。</span><span class="sxs-lookup"><span data-stu-id="618e3-137">To test the portal connection, open an Internet browser and navigate to either the user portal (https://portal.local.azurestack.external/) or the administrator portal (https://adminportal.local.azurestack.external/), sign in and create resources.</span></span>  

## <a name="next-steps"></a><span data-ttu-id="618e3-138">後續步驟</span><span class="sxs-lookup"><span data-stu-id="618e3-138">Next steps</span></span>

[<span data-ttu-id="618e3-139">將虛擬機器提供給您的 Azure Stack 使用者</span><span class="sxs-lookup"><span data-stu-id="618e3-139">Make virtual machines available to your Azure Stack users</span></span>](azure-stack-tutorial-tenant-vm.md)

