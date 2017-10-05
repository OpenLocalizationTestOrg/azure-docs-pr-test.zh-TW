---
title: "使用點對站和憑證驗證將電腦連線至 Azure 虛擬網路︰PowerShell | Microsoft Docs"
description: "使用憑證驗證建立點對站 VPN 閘道連線，進而將電腦安全地連線到您的虛擬網路。 本文適用於 Resource Manager 部署模型並使用 PowerShell。"
services: vpn-gateway
documentationcenter: na
author: cherylmc
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 3eddadf6-2e96-48c4-87c6-52a146faeec6
ms.service: vpn-gateway
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/10/2017
ms.author: cherylmc
ms.openlocfilehash: 2e072ada13b8c742fe7f2e14737c9376f7677906
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="configure-a-point-to-site-connection-to-a-vnet-using-certificate-authentication-powershell"></a><span data-ttu-id="09466-104">使用憑證驗證設定 VNet 的點對站連線：PowerShell</span><span class="sxs-lookup"><span data-stu-id="09466-104">Configure a Point-to-Site connection to a VNet using certificate authentication: PowerShell</span></span>

<span data-ttu-id="09466-105">本文顯示如何使用 PowerShell，在 Resource Manager 部署模型中建立具有點對站連線的 VNet。</span><span class="sxs-lookup"><span data-stu-id="09466-105">This article shows you how to create a VNet with a Point-to-Site connection in the Resource Manager deployment model using PowerShell.</span></span> <span data-ttu-id="09466-106">這項設定使用憑證來驗證連線用戶端。</span><span class="sxs-lookup"><span data-stu-id="09466-106">This configuration uses certificates to authenticate the connecting client.</span></span> <span data-ttu-id="09466-107">您也可從下列清單中選取不同的選項，以使用不同的部署工具或部署模型來建立此組態：</span><span class="sxs-lookup"><span data-stu-id="09466-107">You can also create this configuration using a different deployment tool or deployment model by selecting a different option from the following list:</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="09466-108">Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="09466-108">Azure portal</span></span>](vpn-gateway-howto-point-to-site-resource-manager-portal.md)
> * [<span data-ttu-id="09466-109">PowerShell</span><span class="sxs-lookup"><span data-stu-id="09466-109">PowerShell</span></span>](vpn-gateway-howto-point-to-site-rm-ps.md)
> * [<span data-ttu-id="09466-110">Azure 入口網站 (傳統)</span><span class="sxs-lookup"><span data-stu-id="09466-110">Azure portal (classic)</span></span>](vpn-gateway-howto-point-to-site-classic-azure-portal.md)
>
>

<span data-ttu-id="09466-111">點對站 (P2S) VPN 閘道可讓您建立從個別用戶端電腦到您的虛擬網路的安全連線。</span><span class="sxs-lookup"><span data-stu-id="09466-111">A Point-to-Site (P2S) VPN gateway lets you create a secure connection to your virtual network from an individual client computer.</span></span> <span data-ttu-id="09466-112">當您想要從遠端位置 (例如當您從住家或會議進行遠距工作) 連線到您的 VNet 時，點對站 VPN 連線很實用。</span><span class="sxs-lookup"><span data-stu-id="09466-112">Point-to-Site VPN connections are useful when you want to connect to your VNet from a remote location, such when you are telecommuting from home or a conference.</span></span> <span data-ttu-id="09466-113">當您只有少數用戶端必須連線至 VNet 時，P2S VPN 也是很實用的方案 (而不是使用站對站 VPN)。</span><span class="sxs-lookup"><span data-stu-id="09466-113">A P2S VPN is also a useful solution to use instead of a Site-to-Site VPN when you have only a few clients that need to connect to a VNet.</span></span>

<span data-ttu-id="09466-114">P2S 會使用安全通訊端通道通訊協定 (SSTP)，這是以 SSL 為基礎的 VPN 通訊協定。</span><span class="sxs-lookup"><span data-stu-id="09466-114">P2S uses the Secure Socket Tunneling Protocol (SSTP), which is an SSL-based VPN protocol.</span></span> <span data-ttu-id="09466-115">P2S VPN 連線的建立方式是從用戶端電腦開始。</span><span class="sxs-lookup"><span data-stu-id="09466-115">A P2S VPN connection is established by starting it from the client computer.</span></span>

![將電腦連接至 Azure VNet - 點對站連線圖表](./media/vpn-gateway-howto-point-to-site-rm-ps/point-to-site-diagram.png)

<span data-ttu-id="09466-117">點對站連線驗證連線需要下列各項：</span><span class="sxs-lookup"><span data-stu-id="09466-117">Point-to-Site certificate authentication connections require the following:</span></span>

* <span data-ttu-id="09466-118">RouteBased VPN 閘道。</span><span class="sxs-lookup"><span data-stu-id="09466-118">A RouteBased VPN gateway.</span></span>
* <span data-ttu-id="09466-119">已上傳至 Azure 之根憑證的公開金鑰 (.cer 檔案)。</span><span class="sxs-lookup"><span data-stu-id="09466-119">The public key (.cer file) for a root certificate, which is uploaded to Azure.</span></span> <span data-ttu-id="09466-120">一旦上傳憑證，憑證就會被視為受信任的憑證並且用於驗證。</span><span class="sxs-lookup"><span data-stu-id="09466-120">Once the certificate is uploaded, it is considered a trusted certificate and is used for authentication.</span></span>
* <span data-ttu-id="09466-121">用戶端憑證是從根憑證產生，並安裝在每部即將連線到 VNet 的用戶端電腦上。</span><span class="sxs-lookup"><span data-stu-id="09466-121">A client certificate that is generated from the root certificate and installed on each client computer that will connect to the VNet.</span></span> <span data-ttu-id="09466-122">此憑證使用於用戶端憑證。</span><span class="sxs-lookup"><span data-stu-id="09466-122">This certificate is used for client authentication.</span></span>
* <span data-ttu-id="09466-123">VPN 用戶端組態套件。</span><span class="sxs-lookup"><span data-stu-id="09466-123">A VPN client configuration package.</span></span> <span data-ttu-id="09466-124">VPN 用戶端組態套件包含用戶端連線到 VNet 的必要資訊。</span><span class="sxs-lookup"><span data-stu-id="09466-124">The VPN client configuration package contains the necessary information for the client to connect to the VNet.</span></span> <span data-ttu-id="09466-125">此套件會設定 Windows 作業系統原生的現有 VPN 用戶端。</span><span class="sxs-lookup"><span data-stu-id="09466-125">The package configures the existing VPN client that is native to the Windows operating system.</span></span> <span data-ttu-id="09466-126">必須使用組態套件設定每個連線的用戶端。</span><span class="sxs-lookup"><span data-stu-id="09466-126">Each client that connects must be configured using the configuration package.</span></span>

<span data-ttu-id="09466-127">點對站連線不需要 VPN 裝置或內部部署公眾對應 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="09466-127">Point-to-Site connections do not require a VPN device or an on-premises public-facing IP address.</span></span> <span data-ttu-id="09466-128">已透過 SSTP (安全通訊端通道通訊協定) 建立 VPN 連線。</span><span class="sxs-lookup"><span data-stu-id="09466-128">The VPN connection is created over SSTP (Secure Socket Tunneling Protocol).</span></span> <span data-ttu-id="09466-129">我們在伺服器端上支援 SSTP 1.0、1.1 和 1.2 版。</span><span class="sxs-lookup"><span data-stu-id="09466-129">On the server side, we support SSTP versions 1.0, 1.1, and 1.2.</span></span> <span data-ttu-id="09466-130">用戶端會決定要使用的版本。</span><span class="sxs-lookup"><span data-stu-id="09466-130">The client decides which version to use.</span></span> <span data-ttu-id="09466-131">若為 Windows 8.1 和更新版本，SSTP 預設使用 1.2。</span><span class="sxs-lookup"><span data-stu-id="09466-131">For Windows 8.1 and above, SSTP uses 1.2 by default.</span></span> 

<span data-ttu-id="09466-132">如需有關點對站連線的詳細資訊，請參閱本文結尾的[點對站常見問題集](#faq)。</span><span class="sxs-lookup"><span data-stu-id="09466-132">For more information about Point-to-Site connections, see the [Point-to-Site FAQ](#faq) at the end of this article.</span></span>

## <a name="before-beginning"></a><span data-ttu-id="09466-133">開始之前</span><span class="sxs-lookup"><span data-stu-id="09466-133">Before beginning</span></span>

* <span data-ttu-id="09466-134">請確認您有 Azure 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="09466-134">Verify that you have an Azure subscription.</span></span> <span data-ttu-id="09466-135">如果您還沒有 Azure 訂用帳戶，則可以啟用 [MSDN 訂戶權益](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details)或註冊[免費帳戶](https://azure.microsoft.com/pricing/free-trial)。</span><span class="sxs-lookup"><span data-stu-id="09466-135">If you don't already have an Azure subscription, you can activate your [MSDN subscriber benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details) or sign up for a [free account](https://azure.microsoft.com/pricing/free-trial).</span></span>
* <span data-ttu-id="09466-136">安裝最新版的 Azure Resource Manager PowerShell Cmdlet。</span><span class="sxs-lookup"><span data-stu-id="09466-136">Install the latest version of the Azure Resource Manager PowerShell cmdlets.</span></span> <span data-ttu-id="09466-137">如需如何安裝 PowerShell Cmdlet 的詳細資訊，請參閱[如何安裝和設定 Azure PowerShell](/powershell/azure/overview)。</span><span class="sxs-lookup"><span data-stu-id="09466-137">For more information about installing PowerShell cmdlets, see [How to install and configure Azure PowerShell](/powershell/azure/overview).</span></span>

### <span data-ttu-id="09466-138"><a name="example"></a>範例值</span><span class="sxs-lookup"><span data-stu-id="09466-138"><a name="example"></a>Example values</span></span>

<span data-ttu-id="09466-139">您可以使用範例值來建立測試環境，或參考這些值來進一步了解本文中的範例。</span><span class="sxs-lookup"><span data-stu-id="09466-139">You can use the example values to create a test environment, or refer to these values to better understand the examples in this article.</span></span> <span data-ttu-id="09466-140">我們會在本文的區段 [1](#declare) 中設定變數。</span><span class="sxs-lookup"><span data-stu-id="09466-140">We set the variables in section [1](#declare) of the article.</span></span> <span data-ttu-id="09466-141">您可以使用這些步驟做為逐步解說並使用未經變更的值，或變更這些值以反映您的環境。</span><span class="sxs-lookup"><span data-stu-id="09466-141">You can either use the steps as a walk-through and use the values without changing them, or change them to reflect your environment.</span></span> 

* <span data-ttu-id="09466-142">**名稱：VNet1**</span><span class="sxs-lookup"><span data-stu-id="09466-142">**Name: VNet1**</span></span>
* <span data-ttu-id="09466-143">**位址空間：192.168.0.0/16** 和 **10.254.0.0/16**</span><span class="sxs-lookup"><span data-stu-id="09466-143">**Address space: 192.168.0.0/16** and **10.254.0.0/16**</span></span><br><span data-ttu-id="09466-144">在此範例中，我們使用一個以上的位址空間來說明此組態可以與多個位址空間搭配使用。</span><span class="sxs-lookup"><span data-stu-id="09466-144">For this example, we use more than one address space to illustrate that this configuration works with multiple address spaces.</span></span> <span data-ttu-id="09466-145">不過，此組態不需要多個位址空間。</span><span class="sxs-lookup"><span data-stu-id="09466-145">However, multiple address spaces are not required for this configuration.</span></span>
* <span data-ttu-id="09466-146">**子網路名稱：FrontEnd**</span><span class="sxs-lookup"><span data-stu-id="09466-146">**Subnet name: FrontEnd**</span></span>
  * <span data-ttu-id="09466-147">**子網路位址範圍：192.168.1.0/24**</span><span class="sxs-lookup"><span data-stu-id="09466-147">**Subnet address range: 192.168.1.0/24**</span></span>
* <span data-ttu-id="09466-148">**子網路名稱：BackEnd**</span><span class="sxs-lookup"><span data-stu-id="09466-148">**Subnet name: BackEnd**</span></span>
  * <span data-ttu-id="09466-149">**子網路位址範圍：10.254.1.0/24**</span><span class="sxs-lookup"><span data-stu-id="09466-149">**Subnet address range: 10.254.1.0/24**</span></span>
* <span data-ttu-id="09466-150">**子網路名稱：GatewaySubnet**</span><span class="sxs-lookup"><span data-stu-id="09466-150">**Subnet name: GatewaySubnet**</span></span><br><span data-ttu-id="09466-151">子網路名稱 *GatewaySubnet* 是 VPN 閘道能夠運作的必要項目。</span><span class="sxs-lookup"><span data-stu-id="09466-151">The Subnet name *GatewaySubnet* is mandatory for the VPN gateway to work.</span></span>
  * <span data-ttu-id="09466-152">**閘道子網路位址範圍：192.168.200.0/24**</span><span class="sxs-lookup"><span data-stu-id="09466-152">**GatewaySubnet address range: 192.168.200.0/24**</span></span> 
* <span data-ttu-id="09466-153">**VPN 用戶端位址集區：172.16.201.0/24**</span><span class="sxs-lookup"><span data-stu-id="09466-153">**VPN client address pool: 172.16.201.0/24**</span></span><br><span data-ttu-id="09466-154">使用這個點對站連線來連線到 VNet 的 VPN 用戶端，會收到來自 VPN 用戶端位址集區的 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="09466-154">VPN clients that connect to the VNet using this Point-to-Site connection receive an IP address from the VPN client address pool.</span></span>
* <span data-ttu-id="09466-155">**訂用帳戶：**如果您有一個以上的訂用帳戶，請確認您使用正確的訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="09466-155">**Subscription:** If you have more than one subscription, verify that you are using the correct one.</span></span>
* <span data-ttu-id="09466-156">**資源群組：TestRG**</span><span class="sxs-lookup"><span data-stu-id="09466-156">**Resource Group: TestRG**</span></span>
* <span data-ttu-id="09466-157">**位置：美國東部**</span><span class="sxs-lookup"><span data-stu-id="09466-157">**Location: East US**</span></span>
* <span data-ttu-id="09466-158">**DNS 伺服器：**您想要用於名稱解析的 DNS 伺服器的 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="09466-158">**DNS Server: IP address** of the DNS server that you want to use for name resolution.</span></span>
* <span data-ttu-id="09466-159">**GW 名稱：Vnet1GW**</span><span class="sxs-lookup"><span data-stu-id="09466-159">**GW Name: Vnet1GW**</span></span>
* <span data-ttu-id="09466-160">**公用 IP 名稱：VNet1GWPIP**</span><span class="sxs-lookup"><span data-stu-id="09466-160">**Public IP name: VNet1GWPIP**</span></span>
* <span data-ttu-id="09466-161">**VpnType：RouteBased**</span><span class="sxs-lookup"><span data-stu-id="09466-161">**VpnType: RouteBased**</span></span> 

## <span data-ttu-id="09466-162"><a name="declare"></a>1.登入和設定變數</span><span class="sxs-lookup"><span data-stu-id="09466-162"><a name="declare"></a>1. Log in and set variables</span></span>

<span data-ttu-id="09466-163">在此區段中，您可以登入並宣告用於此組態的值。</span><span class="sxs-lookup"><span data-stu-id="09466-163">In this section, you log in and declare the values used for this configuration.</span></span> <span data-ttu-id="09466-164">在範例指令碼中，會使用宣告的值。</span><span class="sxs-lookup"><span data-stu-id="09466-164">The declared values are used in the sample scripts.</span></span> <span data-ttu-id="09466-165">請變更相關值以反映自己的環境。</span><span class="sxs-lookup"><span data-stu-id="09466-165">Change the values to reflect your own environment.</span></span> <span data-ttu-id="09466-166">或者，可以使用宣告的值並執行各步驟做為練習。</span><span class="sxs-lookup"><span data-stu-id="09466-166">Or, you can use the declared values and go through the steps as an exercise.</span></span>

1. <span data-ttu-id="09466-167">以提高的權限開啟 PowerShell 主控台並登入您的 Azure 帳戶。</span><span class="sxs-lookup"><span data-stu-id="09466-167">Open your PowerShell console with elevated privileges, and log in to your Azure account.</span></span> <span data-ttu-id="09466-168">此 Cmdlet 會提示您提供登入認證。</span><span class="sxs-lookup"><span data-stu-id="09466-168">This cmdlet prompts you for the login credentials.</span></span> <span data-ttu-id="09466-169">登入之後，它會下載您的帳戶設定以供 Azure PowerShell 使用。</span><span class="sxs-lookup"><span data-stu-id="09466-169">After logging in, it downloads your account settings so that they are available to Azure PowerShell.</span></span>

  ```powershell
  Login-AzureRmAccount
  ```
2. <span data-ttu-id="09466-170">取得您的 Azure 訂用帳戶清單。</span><span class="sxs-lookup"><span data-stu-id="09466-170">Get a list of your Azure subscriptions.</span></span>

  ```powershell
  Get-AzureRmSubscription
  ```
3. <span data-ttu-id="09466-171">指定您要使用的訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="09466-171">Specify the subscription that you want to use.</span></span>

  ```powershell
  Select-AzureRmSubscription -SubscriptionName "Name of subscription"
  ```
4. <span data-ttu-id="09466-172">宣告您想要使用的變數。</span><span class="sxs-lookup"><span data-stu-id="09466-172">Declare the variables that you want to use.</span></span> <span data-ttu-id="09466-173">使用以下範例，在需要時將該值替換為您自己的值。</span><span class="sxs-lookup"><span data-stu-id="09466-173">Use the following sample, substituting the values for your own when necessary.</span></span>

  ```powershell
  $VNetName  = "VNet1"
  $FESubName = "FrontEnd"
  $BESubName = "Backend"
  $GWSubName = "GatewaySubnet"
  $VNetPrefix1 = "192.168.0.0/16"
  $VNetPrefix2 = "10.254.0.0/16"
  $FESubPrefix = "192.168.1.0/24"
  $BESubPrefix = "10.254.1.0/24"
  $GWSubPrefix = "192.168.200.0/26"
  $VPNClientAddressPool = "172.16.201.0/24"
  $RG = "TestRG"
  $Location = "East US"
  $DNS = "10.1.1.3"
  $GWName = "VNet1GW"
  $GWIPName = "VNet1GWPIP"
  $GWIPconfName = "gwipconf"
  ```

## <span data-ttu-id="09466-174"><a name="ConfigureVNet"></a>2.設定 VNet</span><span class="sxs-lookup"><span data-stu-id="09466-174"><a name="ConfigureVNet"></a>2. Configure a VNet</span></span>

1. <span data-ttu-id="09466-175">建立資源群組。</span><span class="sxs-lookup"><span data-stu-id="09466-175">Create a resource group.</span></span>

  ```powershell
  New-AzureRmResourceGroup -Name $RG -Location $Location
  ```
2. <span data-ttu-id="09466-176">為虛擬網路建立子網路組態，將其命名為 FrontEndBackEnd 和 GatewaySubnet。</span><span class="sxs-lookup"><span data-stu-id="09466-176">Create the subnet configurations for the virtual network, naming them *FrontEnd*, *BackEnd*, and *GatewaySubnet*.</span></span> <span data-ttu-id="09466-177">這些前置詞必須是您宣告的 VNet 位址空間的一部分。</span><span class="sxs-lookup"><span data-stu-id="09466-177">These prefixes must be part of the VNet address space that you declared.</span></span>

  ```powershell
  $fesub = New-AzureRmVirtualNetworkSubnetConfig -Name $FESubName -AddressPrefix $FESubPrefix
  $besub = New-AzureRmVirtualNetworkSubnetConfig -Name $BESubName -AddressPrefix $BESubPrefix
  $gwsub = New-AzureRmVirtualNetworkSubnetConfig -Name $GWSubName -AddressPrefix $GWSubPrefix
  ```
3. <span data-ttu-id="09466-178">建立虛擬網路</span><span class="sxs-lookup"><span data-stu-id="09466-178">Create the virtual network.</span></span>

  <span data-ttu-id="09466-179">在此範例中，DNS 伺服器是選擇性的。</span><span class="sxs-lookup"><span data-stu-id="09466-179">In this example, the DNS server is optional.</span></span> <span data-ttu-id="09466-180">指定一個值並不會建立新的 DNS 伺服器。</span><span class="sxs-lookup"><span data-stu-id="09466-180">Specifying a value does not create a new DNS server.</span></span> <span data-ttu-id="09466-181">您指定的 DNS 伺服器 IP 位址應該是可以解析您所連線之資源名稱的 DNS 伺服器。</span><span class="sxs-lookup"><span data-stu-id="09466-181">The DNS server IP address that you specify should be a DNS server that can resolve the names for the resources you are connecting to.</span></span> <span data-ttu-id="09466-182">在此範例中，我們使用了私人 IP 位址，但這可能不是您 DNS 伺服器的 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="09466-182">For this example, we used a private IP address, but it is likely that this is not the IP address of your DNS server.</span></span> <span data-ttu-id="09466-183">請務必使用您自己的值。</span><span class="sxs-lookup"><span data-stu-id="09466-183">Be sure to use your own values.</span></span>

  ```powershell
  New-AzureRmVirtualNetwork -Name $VNetName -ResourceGroupName $RG -Location $Location -AddressPrefix $VNetPrefix1,$VNetPrefix2 -Subnet $fesub, $besub, $gwsub -DnsServer $DNS
  ```
4. <span data-ttu-id="09466-184">指定您所建立的虛擬網路的變數。</span><span class="sxs-lookup"><span data-stu-id="09466-184">Specify the variables for the virtual network you created.</span></span>

  ```powershell
  $vnet = Get-AzureRmVirtualNetwork -Name $VNetName -ResourceGroupName $RG
  $subnet = Get-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -VirtualNetwork $vnet
  ```
5. <span data-ttu-id="09466-185">VPN 閘道必須具有公用 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="09466-185">A VPN gateway must have a Public IP address.</span></span> <span data-ttu-id="09466-186">您會先要求 IP 位址資源，然後在建立虛擬網路閘道時參考它。</span><span class="sxs-lookup"><span data-stu-id="09466-186">You first request the IP address resource, and then refer to it when creating your virtual network gateway.</span></span> <span data-ttu-id="09466-187">建立 VPN 閘道時，系統會將 IP 位址動態指派給此資源。</span><span class="sxs-lookup"><span data-stu-id="09466-187">The IP address is dynamically assigned to the resource when the VPN gateway is created.</span></span> <span data-ttu-id="09466-188">VPN 閘道目前僅支援*動態*公用 IP 位址配置。</span><span class="sxs-lookup"><span data-stu-id="09466-188">VPN Gateway currently only supports *Dynamic* Public IP address allocation.</span></span> <span data-ttu-id="09466-189">您無法要求靜態公用 IP 位址指派。</span><span class="sxs-lookup"><span data-stu-id="09466-189">You cannot request a Static Public IP address assignment.</span></span> <span data-ttu-id="09466-190">不過，這不表示之後的 IP 位址變更已指派至您的 VPN 閘道。</span><span class="sxs-lookup"><span data-stu-id="09466-190">However, it doesn't mean that the IP address changes after it has been assigned to your VPN gateway.</span></span> <span data-ttu-id="09466-191">公用 IP 位址只會在刪除或重新建立閘道時變更。</span><span class="sxs-lookup"><span data-stu-id="09466-191">The only time the Public IP address changes is when the gateway is deleted and re-created.</span></span> <span data-ttu-id="09466-192">它不會因為重新調整、重設或 VPN 閘道的其他內部維護/升級而變更。</span><span class="sxs-lookup"><span data-stu-id="09466-192">It doesn't change across resizing, resetting, or other internal maintenance/upgrades of your VPN gateway.</span></span>

  <span data-ttu-id="09466-193">要求動態指派的公用 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="09466-193">Request a dynamically assigned public IP address.</span></span>

  ```powershell
  $pip = New-AzureRmPublicIpAddress -Name $GWIPName -ResourceGroupName $RG -Location $Location -AllocationMethod Dynamic
  $ipconf = New-AzureRmVirtualNetworkGatewayIpConfig -Name $GWIPconfName -Subnet $subnet -PublicIpAddress $pip
  ```

## <span data-ttu-id="09466-194"><a name="creategateway"></a>3.建立 VPN 閘道</span><span class="sxs-lookup"><span data-stu-id="09466-194"><a name="creategateway"></a>3. Create the VPN gateway</span></span>

<span data-ttu-id="09466-195">設定和建立 VNet 的虛擬網路閘道。</span><span class="sxs-lookup"><span data-stu-id="09466-195">Configure and create the virtual network gateway for your VNet.</span></span>

* <span data-ttu-id="09466-196">-GatewayType 必須是 **Vpn**，而且 -VpnType 必須是 **RouteBased**。</span><span class="sxs-lookup"><span data-stu-id="09466-196">The *-GatewayType* must be **Vpn** and the *-VpnType* must be **RouteBased**.</span></span>
* <span data-ttu-id="09466-197">視您選取的[閘道 sku](vpn-gateway-about-vpn-gateway-settings.md) 而定，VPN 閘道可能需要 45 分鐘的時間才能完成。</span><span class="sxs-lookup"><span data-stu-id="09466-197">A VPN gateway can take up to 45 minutes to complete, depending on the [gateway sku](vpn-gateway-about-vpn-gateway-settings.md) you select.</span></span>

```powershell
New-AzureRmVirtualNetworkGateway -Name $GWName -ResourceGroupName $RG `
-Location $Location -IpConfigurations $ipconf -GatewayType Vpn `
-VpnType RouteBased -EnableBgp $false -GatewaySku VpnGw1 `
```

## <span data-ttu-id="09466-198"><a name="addresspool"></a>4.新增 VPN 用戶端位址集區</span><span class="sxs-lookup"><span data-stu-id="09466-198"><a name="addresspool"></a>4. Add the VPN client address pool</span></span>

<span data-ttu-id="09466-199">VPN 閘道完成建立之後，您可以新增 VPN 用戶端位址集區。</span><span class="sxs-lookup"><span data-stu-id="09466-199">After the VPN gateway finishes creating, you can add the VPN client address pool.</span></span> <span data-ttu-id="09466-200">VPN 用戶端位址集區是 VPN 用戶端在連線時將從其接收 IP 位址的範圍。</span><span class="sxs-lookup"><span data-stu-id="09466-200">The VPN client address pool is the range from which the VPN clients receive an IP address when connecting.</span></span> <span data-ttu-id="09466-201">使用不會重疊的私人 IP 位址範圍搭配您從其連線的內部部署位置，或搭配您要連線至的 VNet。</span><span class="sxs-lookup"><span data-stu-id="09466-201">Use a private IP address range that does not overlap with the on-premises location that you connect from, or with the VNet that you want to connect to.</span></span> <span data-ttu-id="09466-202">在此範例中，VPN 用戶端位址集區會宣告為步驟 1 中的[變數](#declare)。</span><span class="sxs-lookup"><span data-stu-id="09466-202">In this example, the VPN client address pool is declared as a [variable](#declare) in Step 1.</span></span>

```powershell
$Gateway = Get-AzureRmVirtualNetworkGateway -ResourceGroupName $RG -Name $GWName
Set-AzureRmVirtualNetworkGateway -VirtualNetworkGateway $Gateway -VpnClientAddressPool $VPNClientAddressPool
```

## <span data-ttu-id="09466-203"><a name="Certificates"></a>5.產生憑證</span><span class="sxs-lookup"><span data-stu-id="09466-203"><a name="Certificates"></a>5. Generate certificates</span></span>

<span data-ttu-id="09466-204">憑證是 Azure 用於點對站 VPN 的 VPN 用戶端驗證。</span><span class="sxs-lookup"><span data-stu-id="09466-204">Certificates are used by Azure to authenticate VPN clients for Point-to-Site VPNs.</span></span> <span data-ttu-id="09466-205">您會將根憑證的公開金鑰資訊上傳至 Azure。</span><span class="sxs-lookup"><span data-stu-id="09466-205">You upload the public key information of the root certificate to Azure.</span></span> <span data-ttu-id="09466-206">公開金鑰就會被視為「受信任」。</span><span class="sxs-lookup"><span data-stu-id="09466-206">The public key is then considered 'trusted'.</span></span> <span data-ttu-id="09466-207">用戶端憑證必須從信任的根憑證產生，然後安裝在 [憑證-目前使用者/個人憑證] 存放區中的每部用戶端電腦上。</span><span class="sxs-lookup"><span data-stu-id="09466-207">Client certificates must be generated from the trusted root certificate, and then installed on each client computer in the Certificates-Current User/Personal certificate store.</span></span> <span data-ttu-id="09466-208">在用戶端初始 VNet 連線時，此憑證用來驗證用戶端。</span><span class="sxs-lookup"><span data-stu-id="09466-208">The certificate is used to authenticate the client when it initiates a connection to the VNet.</span></span> 

<span data-ttu-id="09466-209">如果您使用自我簽署憑證，則必須使用特定參數來建立這些憑證。</span><span class="sxs-lookup"><span data-stu-id="09466-209">If you use self-signed certificates, they must be created using specific parameters.</span></span> <span data-ttu-id="09466-210">您可以依循 [PowerShell 和 Windows 10](vpn-gateway-certificates-point-to-site.md) 的指示建立自我簽署憑證；或者，如果您沒有 Windows 10，可以使用 [MakeCert](vpn-gateway-certificates-point-to-site-makecert.md)。</span><span class="sxs-lookup"><span data-stu-id="09466-210">You can create a self-signed certificate using the instructions for [PowerShell and Windows 10](vpn-gateway-certificates-point-to-site.md), or, if you don't have Windows 10, you can use [MakeCert](vpn-gateway-certificates-point-to-site-makecert.md).</span></span> <span data-ttu-id="09466-211">產生自我簽署的根憑證和用戶端憑證時，請務必遵循指示中的步驟。</span><span class="sxs-lookup"><span data-stu-id="09466-211">It's important that you follow the steps in the instructions when generating self-signed root certificates and client certificates.</span></span> <span data-ttu-id="09466-212">否則，您所產生的憑證將無法與 P2S 連線相容，而且會收到連線錯誤的訊息。</span><span class="sxs-lookup"><span data-stu-id="09466-212">Otherwise, the certificates you generate will not be compatible with P2S connections and you will receive a connection error.</span></span>

### <span data-ttu-id="09466-213"><a name="cer"></a>1.取得根憑證的 .cer 檔案</span><span class="sxs-lookup"><span data-stu-id="09466-213"><a name="cer"></a>1. Obtain the .cer file for the root certificate</span></span>

[!INCLUDE [vpn-gateway-basic-vnet-rm-portal](../../includes/vpn-gateway-p2s-rootcert-include.md)]


### <span data-ttu-id="09466-214"><a name="generate"></a>2.產生用戶端憑證 </span><span class="sxs-lookup"><span data-stu-id="09466-214"><a name="generate"></a>2. Generate a client certificate</span></span>

[!INCLUDE [vpn-gateway-basic-vnet-rm-portal](../../includes/vpn-gateway-p2s-clientcert-include.md)]

## <span data-ttu-id="09466-215"><a name="upload"></a>6.上傳根憑證公開金鑰資訊</span><span class="sxs-lookup"><span data-stu-id="09466-215"><a name="upload"></a>6. Upload the root certificate public key information</span></span>

<span data-ttu-id="09466-216">確認 VPN 閘道已完成建立。</span><span class="sxs-lookup"><span data-stu-id="09466-216">Verify that your VPN gateway has finished creating.</span></span> <span data-ttu-id="09466-217">完成之後，您可以將受信任根憑證的 .cer 檔案 (其中包含公開金鑰資訊) 上傳至 Azure。</span><span class="sxs-lookup"><span data-stu-id="09466-217">Once it has completed, you can upload the .cer file (which contains the public key information) for a trusted root certificate to Azure.</span></span> <span data-ttu-id="09466-218">一旦上傳 .cer 檔案，Azure 就可以使用它來驗證已安裝從受信任根憑證產生之用戶端憑證的用戶端。</span><span class="sxs-lookup"><span data-stu-id="09466-218">Once a.cer file is uploaded, Azure can use it to authenticate clients that have installed a client certificate generated from the trusted root certificate.</span></span> <span data-ttu-id="09466-219">如有需要，您稍後可以上傳其他受信任的根憑證檔案 (最多總計 20 個檔案)。</span><span class="sxs-lookup"><span data-stu-id="09466-219">You can upload additional trusted root certificate files - up to a total of 20 - later, if needed.</span></span>

1. <span data-ttu-id="09466-220">宣告您的憑證名稱的變數，以自己的值取代。</span><span class="sxs-lookup"><span data-stu-id="09466-220">Declare the variable for your certificate name, replacing the value with your own.</span></span>

  ```powershell
  $P2SRootCertName = "P2SRootCert.cer"
  ```
2. <span data-ttu-id="09466-221">將檔案路徑以您的路徑取代，然後執行 Cmdlet。</span><span class="sxs-lookup"><span data-stu-id="09466-221">Replace the file path with your own, and then run the cmdlets.</span></span>

  ```powershell
  $filePathForCert = "C:\cert\P2SRootCert.cer"
  $cert = new-object System.Security.Cryptography.X509Certificates.X509Certificate2($filePathForCert)
  $CertBase64 = [system.convert]::ToBase64String($cert.RawData)
  $p2srootcert = New-AzureRmVpnClientRootCertificate -Name $P2SRootCertName -PublicCertData $CertBase64
  ```
3. <span data-ttu-id="09466-222">將公開金鑰資訊上傳至 Azure。</span><span class="sxs-lookup"><span data-stu-id="09466-222">Upload the public key information to Azure.</span></span> <span data-ttu-id="09466-223">一旦上傳憑證資訊，Azure 會認為這是受信任的根憑證。</span><span class="sxs-lookup"><span data-stu-id="09466-223">Once the certificate information is uploaded, Azure considers this to be a trusted root certificate.</span></span>

   ```powershell
  Add-AzureRmVpnClientRootCertificate -VpnClientRootCertificateName $P2SRootCertName -VirtualNetworkGatewayname "VNet1GW" -ResourceGroupName "TestRG" -PublicCertData $CertBase64
  ```

## <span data-ttu-id="09466-224"><a name="clientconfig"></a>7.下載 VPN 用戶端設定套件</span><span class="sxs-lookup"><span data-stu-id="09466-224"><a name="clientconfig"></a>7. Download the VPN client configuration package</span></span>

<span data-ttu-id="09466-225">若要使用點對站 VPN 連線至 VNet，每個用戶端必須用戶端組態套件，以使用連線至虛擬網路所需的設定和檔案來設定原生 VPN 用戶端。</span><span class="sxs-lookup"><span data-stu-id="09466-225">To connect to a VNet using a Point-to-Site VPN, each client must install a client configuration package that configures the native VPN client with the settings and files that are necessary to connect to the virtual network.</span></span> <span data-ttu-id="09466-226">VPN 用戶端組態套件可設定原生 Windows VPN 用戶端，它不會安裝新的或不同的 VPN 用戶端。</span><span class="sxs-lookup"><span data-stu-id="09466-226">The VPN client configuration package configures the native Windows VPN client, it doesn't install a new or different VPN client.</span></span> 

<span data-ttu-id="09466-227">您可以在每個用戶端電腦上使用相同的 VPN 用戶端組態套件，只要版本符合用戶端的架構。</span><span class="sxs-lookup"><span data-stu-id="09466-227">You can use the same VPN client configuration package on each client computer, as long as the version matches the architecture for the client.</span></span> <span data-ttu-id="09466-228">如需支援的用戶端作業系統清單，請參閱本文結尾的[點對站連線常見問題集](#faq)。</span><span class="sxs-lookup"><span data-stu-id="09466-228">For the list of client operating systems that are supported, see the [Point-to-Site connections FAQ](#faq) at the end of this article.</span></span>

1. <span data-ttu-id="09466-229">建立閘道之後，您可以產生並下載用戶端組態套件。</span><span class="sxs-lookup"><span data-stu-id="09466-229">After the gateway has been created, you can generate and download the client configuration package.</span></span> <span data-ttu-id="09466-230">這個範例會下載 64 位元用戶端的封裝。</span><span class="sxs-lookup"><span data-stu-id="09466-230">This example downloads the package for 64-bit clients.</span></span> <span data-ttu-id="09466-231">如果您想要下載 32 位元用戶端，請將 'Amd64' 取代為 'x86'。</span><span class="sxs-lookup"><span data-stu-id="09466-231">If you want to download the 32-bit client, replace 'Amd64' with 'x86'.</span></span> <span data-ttu-id="09466-232">您也可以使用 Azure 入口網站來下載 VPN 用戶端。</span><span class="sxs-lookup"><span data-stu-id="09466-232">You can also download the VPN client by using the Azure portal.</span></span>

  ```powershell
  Get-AzureRmVpnClientPackage -ResourceGroupName $RG `
  -VirtualNetworkGatewayName $GWName -ProcessorArchitecture Amd64
  ```
2. <span data-ttu-id="09466-233">複製並貼上傳回給網頁瀏覽器的連結以下載套件，並小心移除連結周圍的引號。</span><span class="sxs-lookup"><span data-stu-id="09466-233">Copy and paste the link that is returned to a web browser to download the package, taking care to remove the quotes surrounding the link.</span></span> 
3. <span data-ttu-id="09466-234">在用戶端電腦上下載及安裝套件。</span><span class="sxs-lookup"><span data-stu-id="09466-234">Download and install the package on the client computer.</span></span> <span data-ttu-id="09466-235">如果您看到 SmartScreen 快顯視窗，請按一下 [更多資訊]，然後按一下 [仍要執行]。</span><span class="sxs-lookup"><span data-stu-id="09466-235">If you see a SmartScreen popup, click **More info**, then **Run anyway**.</span></span> <span data-ttu-id="09466-236">您也可以儲存要在其他用戶端電腦上安裝的套件。</span><span class="sxs-lookup"><span data-stu-id="09466-236">You can also save the package to install on other client computers.</span></span>
4. <span data-ttu-id="09466-237">在用戶端電腦上，瀏覽至 [網路設定]，然後按一下 [VPN]。</span><span class="sxs-lookup"><span data-stu-id="09466-237">On the client computer, navigate to **Network Settings** and click **VPN**.</span></span> <span data-ttu-id="09466-238">VPN 連線會顯示其連線的虛擬網路名稱。</span><span class="sxs-lookup"><span data-stu-id="09466-238">The VPN connection shows the name of the virtual network that it connects to.</span></span>

## <span data-ttu-id="09466-239"><a name="clientcertificate"></a>8.安裝匯出的用戶端憑證</span><span class="sxs-lookup"><span data-stu-id="09466-239"><a name="clientcertificate"></a>8. Install an exported client certificate</span></span>

<span data-ttu-id="09466-240">如果您想要從不同於用來產生用戶端憑證的用戶端電腦建立 P2S 連線，您需要安裝用戶端憑證。</span><span class="sxs-lookup"><span data-stu-id="09466-240">If you want to create a P2S connection from a client computer other than the one you used to generate the client certificates, you need to install a client certificate.</span></span> <span data-ttu-id="09466-241">安裝用戶端憑證時，您需要匯出用戶端憑證時所建立的密碼。</span><span class="sxs-lookup"><span data-stu-id="09466-241">When installing a client certificate, you need the password that was created when the client certificate was exported.</span></span> <span data-ttu-id="09466-242">一般而言，只要按兩下憑證並加以安裝。</span><span class="sxs-lookup"><span data-stu-id="09466-242">Typically, it is just a matter of double-clicking the certificate and installing it.</span></span>

<span data-ttu-id="09466-243">請確定用戶端憑證已隨著整個憑證鏈結匯出為 .pfx (這是預設值)。</span><span class="sxs-lookup"><span data-stu-id="09466-243">Make sure the client certificate was exported as a .pfx along with the entire certificate chain (which is the default).</span></span> <span data-ttu-id="09466-244">否則，根憑證資訊不存在於用戶端電腦上，而且用戶端將無法正確驗證。</span><span class="sxs-lookup"><span data-stu-id="09466-244">Otherwise, the root certificate information isn't present on the client computer and the client won't be able to authenticate properly.</span></span> <span data-ttu-id="09466-245">如需詳細資訊，請參閱[安裝匯出的用戶端憑證](vpn-gateway-certificates-point-to-site.md#install)。</span><span class="sxs-lookup"><span data-stu-id="09466-245">For more information, see [Install an exported client certificate](vpn-gateway-certificates-point-to-site.md#install).</span></span> 

## <span data-ttu-id="09466-246"><a name="connect"></a>9.連接到 Azure</span><span class="sxs-lookup"><span data-stu-id="09466-246"><a name="connect"></a>9. Connect to Azure</span></span>

1. <span data-ttu-id="09466-247">若要連接至您的 VNet，在用戶端電腦上瀏覽到 VPN 連線，然後找出所建立的 VPN 連線。</span><span class="sxs-lookup"><span data-stu-id="09466-247">To connect to your VNet, on the client computer, navigate to VPN connections and locate the VPN connection that you created.</span></span> <span data-ttu-id="09466-248">其名稱會與虛擬網路相同。</span><span class="sxs-lookup"><span data-stu-id="09466-248">It is named the same name as your virtual network.</span></span> <span data-ttu-id="09466-249">按一下 [ **連接**]。</span><span class="sxs-lookup"><span data-stu-id="09466-249">Click **Connect**.</span></span> <span data-ttu-id="09466-250">可能會出現與使用憑證有關的快顯訊息。</span><span class="sxs-lookup"><span data-stu-id="09466-250">A pop-up message may appear that refers to using the certificate.</span></span> <span data-ttu-id="09466-251">按一下 [繼續] 以使用較高的權限。</span><span class="sxs-lookup"><span data-stu-id="09466-251">Click **Continue** to use elevated privileges.</span></span> 
2. <span data-ttu-id="09466-252">在 [連線] 狀態頁面上，按一下 [連線] 以便開始連線。</span><span class="sxs-lookup"><span data-stu-id="09466-252">On the **Connection** status page, click **Connect** to start the connection.</span></span> <span data-ttu-id="09466-253">如果出現 [選取憑證]  畫面，請確認顯示的用戶端憑證是要用來連接的憑證。</span><span class="sxs-lookup"><span data-stu-id="09466-253">If you see a **Select Certificate** screen, verify that the client certificate showing is the one that you want to use to connect.</span></span> <span data-ttu-id="09466-254">如果沒有，請使用下拉箭頭來選取正確的憑證，然後按一下 [確定] 。</span><span class="sxs-lookup"><span data-stu-id="09466-254">If it is not, use the drop-down arrow to select the correct certificate, and then click **OK**.</span></span>

  ![VPN 用戶端連線至 Azure](./media/vpn-gateway-howto-point-to-site-rm-ps/clientconnect.png)
3. <span data-ttu-id="09466-256">已建立您的連線。</span><span class="sxs-lookup"><span data-stu-id="09466-256">Your connection is established.</span></span>

  ![連線已建立](./media/vpn-gateway-howto-point-to-site-rm-ps/connected.png)

#### <a name="troubleshooting-p2s-connections"></a><span data-ttu-id="09466-258">針對 P2S 連線進行疑難排解</span><span class="sxs-lookup"><span data-stu-id="09466-258">Troubleshooting P2S connections</span></span>

[!INCLUDE [client certificates](../../includes/vpn-gateway-certificates-verify-client-cert-include.md)]

## <span data-ttu-id="09466-259"><a name="verify"></a>10.確認您的連接</span><span class="sxs-lookup"><span data-stu-id="09466-259"><a name="verify"></a>10. Verify your connection</span></span>

1. <span data-ttu-id="09466-260">若要驗證您的 VPN 連線為作用中狀態，請開啟提升權限的命令提示字元，並執行 *ipconfig/all*。</span><span class="sxs-lookup"><span data-stu-id="09466-260">To verify that your VPN connection is active, open an elevated command prompt, and run *ipconfig/all*.</span></span>
2. <span data-ttu-id="09466-261">檢視結果。</span><span class="sxs-lookup"><span data-stu-id="09466-261">View the results.</span></span> <span data-ttu-id="09466-262">請注意，您接收到的 IP 位址是您在組態中指定的點對站 VPN 用戶端位址集區中的其中一個位址。</span><span class="sxs-lookup"><span data-stu-id="09466-262">Notice that the IP address you received is one of the addresses within the Point-to-Site VPN Client Address Pool that you specified in your configuration.</span></span> <span data-ttu-id="09466-263">結果類似於此範例：</span><span class="sxs-lookup"><span data-stu-id="09466-263">The results are similar to this example:</span></span>

  ```
  PPP adapter VNet1:
      Connection-specific DNS Suffix .:
      Description.....................: VNet1
      Physical Address................:
      DHCP Enabled....................: No
      Autoconfiguration Enabled.......: Yes
      IPv4 Address....................: 172.16.201.3(Preferred)
      Subnet Mask.....................: 255.255.255.255
      Default Gateway.................:
      NetBIOS over Tcpip..............: Enabled
  ```

## <span data-ttu-id="09466-264"><a name="connectVM"></a>連線至虛擬機器</span><span class="sxs-lookup"><span data-stu-id="09466-264"><a name="connectVM"></a>Connect to a virtual machine</span></span>

[!INCLUDE [Connect to a VM](../../includes/vpn-gateway-connect-vm-p2s-include.md)]

## <span data-ttu-id="09466-265"><a name="addremovecert"></a>新增或移除根憑證</span><span class="sxs-lookup"><span data-stu-id="09466-265"><a name="addremovecert"></a>Add or remove a root certificate</span></span>

<span data-ttu-id="09466-266">您可以從 Azure 新增和移除受信任的根憑證。</span><span class="sxs-lookup"><span data-stu-id="09466-266">You can add and remove trusted root certificates from Azure.</span></span> <span data-ttu-id="09466-267">當您移除根憑證時，從根憑證產生憑證的用戶端無法進行驗證，而且無法進行連線。</span><span class="sxs-lookup"><span data-stu-id="09466-267">When you remove a root certificate, clients that have a certificate generated from the root certificate can't authenticate and won't be able to connect.</span></span> <span data-ttu-id="09466-268">若希望用戶端進行驗證和連線，您需要安裝從 Azure 信任 (已上傳至 Azure) 的根憑證產生的新用戶端憑證。</span><span class="sxs-lookup"><span data-stu-id="09466-268">If you want a client to authenticate and connect, you need to install a new client certificate generated from a root certificate that is trusted (uploaded) to Azure.</span></span>

### <span data-ttu-id="09466-269"><a name="addtrustedroot"></a>新增受信任的根憑證</span><span class="sxs-lookup"><span data-stu-id="09466-269"><a name="addtrustedroot"></a>To add a trusted root certificate</span></span>

<span data-ttu-id="09466-270">您最多可將 20 個根憑證 .cer 檔案新增至 Azure。</span><span class="sxs-lookup"><span data-stu-id="09466-270">You can add up to 20 root certificate .cer files to Azure.</span></span> <span data-ttu-id="09466-271">下列步驟可協助您新增根憑證︰</span><span class="sxs-lookup"><span data-stu-id="09466-271">The following steps help you add a root certificate:</span></span>

#### <span data-ttu-id="09466-272"><a name="certmethod1"></a>方法 1</span><span class="sxs-lookup"><span data-stu-id="09466-272"><a name="certmethod1"></a>Method 1</span></span>

<span data-ttu-id="09466-273">這是上傳根憑證的最有效方法。</span><span class="sxs-lookup"><span data-stu-id="09466-273">This is the most efficient method to upload a root certificate.</span></span>

1. <span data-ttu-id="09466-274">準備要上傳的 .cer 檔案：</span><span class="sxs-lookup"><span data-stu-id="09466-274">Prepare the .cer file to upload:</span></span>

  ```powershell
  $filePathForCert = "C:\cert\P2SRootCert3.cer"
  $cert = new-object System.Security.Cryptography.X509Certificates.X509Certificate2($filePathForCert)
  $CertBase64_3 = [system.convert]::ToBase64String($cert.RawData)
  $p2srootcert = New-AzureRmVpnClientRootCertificate -Name $P2SRootCertName -PublicCertData $CertBase64_3
  ```
2. <span data-ttu-id="09466-275">上傳檔案。</span><span class="sxs-lookup"><span data-stu-id="09466-275">Upload the file.</span></span> <span data-ttu-id="09466-276">您一次只能上傳一個檔案。</span><span class="sxs-lookup"><span data-stu-id="09466-276">You can only upload one file at a time.</span></span>

  ```powershell
  Add-AzureRmVpnClientRootCertificate -VpnClientRootCertificateName $P2SRootCertName -VirtualNetworkGatewayname "VNet1GW" -ResourceGroupName "TestRG" -PublicCertData $CertBase64_3
  ```

3. <span data-ttu-id="09466-277">若要確認憑證檔案已上傳：</span><span class="sxs-lookup"><span data-stu-id="09466-277">To verify that the certificate file uploaded:</span></span>

  ```powershell
  Get-AzureRmVpnClientRootCertificate -ResourceGroupName "TestRG" `
  -VirtualNetworkGatewayName "VNet1GW"
  ```

#### <span data-ttu-id="09466-278"><a name="certmethod2"></a>方法 2</span><span class="sxs-lookup"><span data-stu-id="09466-278"><a name="certmethod2"></a>Method 2</span></span>

<span data-ttu-id="09466-279">這個方法的步驟比方法 1 多，但結果相同。</span><span class="sxs-lookup"><span data-stu-id="09466-279">This method is has more steps than Method 1, but has the same result.</span></span> <span data-ttu-id="09466-280">納入此方法，以免您需要檢視憑證資料。</span><span class="sxs-lookup"><span data-stu-id="09466-280">It is included in case you need to view the certificate data.</span></span>

1. <span data-ttu-id="09466-281">建立並準備要新增至 Azure 的新根憑證。</span><span class="sxs-lookup"><span data-stu-id="09466-281">Create and prepare the new root certificate to add to Azure.</span></span> <span data-ttu-id="09466-282">將公開金鑰匯出成 Base-64 編碼 X.509 (.CER) 並使用文字編輯器開啟。</span><span class="sxs-lookup"><span data-stu-id="09466-282">Export the public key as a Base-64 encoded X.509 (.CER) and open it with a text editor.</span></span> <span data-ttu-id="09466-283">如下列範例所示，複製相關值：</span><span class="sxs-lookup"><span data-stu-id="09466-283">Copy the values, as shown in the following example:</span></span>

  ![憑證](./media/vpn-gateway-howto-point-to-site-rm-ps/copycert.png)

  > [!NOTE]
  > <span data-ttu-id="09466-285">複製憑證資料時，請確定您是以連續一行的形式複製文字，而不含歸位字元或換行字元。</span><span class="sxs-lookup"><span data-stu-id="09466-285">When copying the certificate data, make sure that you copy the text as one continuous line without carriage returns or line feeds.</span></span> <span data-ttu-id="09466-286">您可能必須將文字編輯器中的檢視修改成 [顯示符號] 或 [顯示所有字元]，才能看到歸位字元和換行字元。</span><span class="sxs-lookup"><span data-stu-id="09466-286">You may need to modify your view in the text editor to 'Show Symbol/Show all characters' to see the carriage returns and line feeds.</span></span>
  >
  >

2. <span data-ttu-id="09466-287">指定憑證名稱和金鑰資訊做為變數。</span><span class="sxs-lookup"><span data-stu-id="09466-287">Specify the certificate name and key information as a variable.</span></span> <span data-ttu-id="09466-288">如下列範例所示，以您自己的資訊加以取代：</span><span class="sxs-lookup"><span data-stu-id="09466-288">Replace the information with your own, as shown in the following example:</span></span>

  ```powershell
  $P2SRootCertName2 = "ARMP2SRootCert2.cer"
  $MyP2SCertPubKeyBase64_2 = "MIIC/zCCAeugAwIBAgIQKazxzFjMkp9JRiX+tkTfSzAJBgUrDgMCHQUAMBgxFjAUBgNVBAMTDU15UDJTUm9vdENlcnQwHhcNMTUxMjE5MDI1MTIxWhcNMzkxMjMxMjM1OTU5WjAYMRYwFAYDVQQDEw1NeVAyU1Jvb3RDZXJ0MIIBIjANBgkqhkiG9w0BAQEFAAOCAQ8AMIIBCgKCAQEAyjIXoWy8xE/GF1OSIvUaA0bxBjZ1PJfcXkMWsHPzvhWc2esOKrVQtgFgDz4ggAnOUFEkFaszjiHdnXv3mjzE2SpmAVIZPf2/yPWqkoHwkmrp6BpOvNVOpKxaGPOuK8+dql1xcL0eCkt69g4lxy0FGRFkBcSIgVTViS9wjuuS7LPo5+OXgyFkAY3pSDiMzQCkRGNFgw5WGMHRDAiruDQF1ciLNojAQCsDdLnI3pDYsvRW73HZEhmOqRRnJQe6VekvBYKLvnKaxUTKhFIYwuymHBB96nMFdRUKCZIiWRIy8Hc8+sQEsAML2EItAjQv4+fqgYiFdSWqnQCPf/7IZbotgQIDAQABo00wSzBJBgNVHQEEQjBAgBAkuVrWvFsCJAdK5pb/eoCNoRowGDEWMBQGA1UEAxMNTXlQMlNSb290Q2VydIIQKazxzFjMkp9JRiX+tkTfSzAJBgUrDgMCHQUAA4IBAQA223veAZEIar9N12ubNH2+HwZASNzDVNqspkPKD97TXfKHlPlIcS43TaYkTz38eVrwI6E0yDk4jAuPaKnPuPYFRj9w540SvY6PdOUwDoEqpIcAVp+b4VYwxPL6oyEQ8wnOYuoAK1hhh20lCbo8h9mMy9ofU+RP6HJ7lTqupLfXdID/XevI8tW6Dm+C/wCeV3EmIlO9KUoblD/e24zlo3YzOtbyXwTIh34T0fO/zQvUuBqZMcIPfM1cDvqcqiEFLWvWKoAnxbzckye2uk1gHO52d8AVL3mGiX8wBJkjc/pMdxrEvvCzJkltBmqxTM6XjDJALuVh16qFlqgTWCIcb7ju"
  ```
3. <span data-ttu-id="09466-289">加入新的根憑證。</span><span class="sxs-lookup"><span data-stu-id="09466-289">Add the new root certificate.</span></span> <span data-ttu-id="09466-290">您一次只能新增一個憑證。</span><span class="sxs-lookup"><span data-stu-id="09466-290">You can only add one certificate at a time.</span></span>

  ```powershell
  Add-AzureRmVpnClientRootCertificate -VpnClientRootCertificateName $P2SRootCertName2 -VirtualNetworkGatewayname "VNet1GW" -ResourceGroupName "TestRG" -PublicCertData $MyP2SCertPubKeyBase64_2
  ```
4. <span data-ttu-id="09466-291">您可使用下列範例確認新憑證已正確新增：</span><span class="sxs-lookup"><span data-stu-id="09466-291">You can verify that the new certificate was added correctly by using the following example:</span></span>

  ```powershell
  Get-AzureRmVpnClientRootCertificate -ResourceGroupName "TestRG" `
  -VirtualNetworkGatewayName "VNet1GW"
  ```

### <span data-ttu-id="09466-292"><a name="removerootcert"></a>移除根憑證</span><span class="sxs-lookup"><span data-stu-id="09466-292"><a name="removerootcert"></a>To remove a root certificate</span></span>

1. <span data-ttu-id="09466-293">宣告變數。</span><span class="sxs-lookup"><span data-stu-id="09466-293">Declare the variables.</span></span>

  ```powershell
  $GWName = "Name_of_virtual_network_gateway"
  $RG = "Name_of_resource_group"
  $P2SRootCertName2 = "ARMP2SRootCert2.cer"
  $MyP2SCertPubKeyBase64_2 = "MIIC/zCCAeugAwIBAgIQKazxzFjMkp9JRiX+tkTfSzAJBgUrDgMCHQUAMBgxFjAUBgNVBAMTDU15UDJTUm9vdENlcnQwHhcNMTUxMjE5MDI1MTIxWhcNMzkxMjMxMjM1OTU5WjAYMRYwFAYDVQQDEw1NeVAyU1Jvb3RDZXJ0MIIBIjANBgkqhkiG9w0BAQEFAAOCAQ8AMIIBCgKCAQEAyjIXoWy8xE/GF1OSIvUaA0bxBjZ1PJfcXkMWsHPzvhWc2esOKrVQtgFgDz4ggAnOUFEkFaszjiHdnXv3mjzE2SpmAVIZPf2/yPWqkoHwkmrp6BpOvNVOpKxaGPOuK8+dql1xcL0eCkt69g4lxy0FGRFkBcSIgVTViS9wjuuS7LPo5+OXgyFkAY3pSDiMzQCkRGNFgw5WGMHRDAiruDQF1ciLNojAQCsDdLnI3pDYsvRW73HZEhmOqRRnJQe6VekvBYKLvnKaxUTKhFIYwuymHBB96nMFdRUKCZIiWRIy8Hc8+sQEsAML2EItAjQv4+fqgYiFdSWqnQCPf/7IZbotgQIDAQABo00wSzBJBgNVHQEEQjBAgBAkuVrWvFsCJAdK5pb/eoCNoRowGDEWMBQGA1UEAxMNTXlQMlNSb290Q2VydIIQKazxzFjMkp9JRiX+tkTfSzAJBgUrDgMCHQUAA4IBAQA223veAZEIar9N12ubNH2+HwZASNzDVNqspkPKD97TXfKHlPlIcS43TaYkTz38eVrwI6E0yDk4jAuPaKnPuPYFRj9w540SvY6PdOUwDoEqpIcAVp+b4VYwxPL6oyEQ8wnOYuoAK1hhh20lCbo8h9mMy9ofU+RP6HJ7lTqupLfXdID/XevI8tW6Dm+C/wCeV3EmIlO9KUoblD/e24zlo3YzOtbyXwTIh34T0fO/zQvUuBqZMcIPfM1cDvqcqiEFLWvWKoAnxbzckye2uk1gHO52d8AVL3mGiX8wBJkjc/pMdxrEvvCzJkltBmqxTM6XjDJALuVh16qFlqgTWCIcb7ju"
  ```
2. <span data-ttu-id="09466-294">移除憑證。</span><span class="sxs-lookup"><span data-stu-id="09466-294">Remove the certificate.</span></span>

  ```powershell
  Remove-AzureRmVpnClientRootCertificate -VpnClientRootCertificateName $P2SRootCertName2 -VirtualNetworkGatewayName $GWName -ResourceGroupName $RG -PublicCertData $MyP2SCertPubKeyBase64_2
  ```
3. <span data-ttu-id="09466-295">使用下列範例確認已成功移除憑證。</span><span class="sxs-lookup"><span data-stu-id="09466-295">Use the following example to verify that the certificate was removed successfully.</span></span>

  ```powershell
  Get-AzureRmVpnClientRootCertificate -ResourceGroupName "TestRG" `
  -VirtualNetworkGatewayName "VNet1GW"
  ```

## <span data-ttu-id="09466-296"><a name="revoke"></a>撤銷用戶端憑證</span><span class="sxs-lookup"><span data-stu-id="09466-296"><a name="revoke"></a>Revoke a client certificate</span></span>

<span data-ttu-id="09466-297">您可以撤銷用戶端憑證。</span><span class="sxs-lookup"><span data-stu-id="09466-297">You can revoke client certificates.</span></span> <span data-ttu-id="09466-298">憑證撤銷清單可讓您選擇性地拒絕以個別的用戶端憑證為基礎的點對站連線。</span><span class="sxs-lookup"><span data-stu-id="09466-298">The certificate revocation list allows you to selectively deny Point-to-Site connectivity based on individual client certificates.</span></span> <span data-ttu-id="09466-299">這與移除受信任的根憑證不同。</span><span class="sxs-lookup"><span data-stu-id="09466-299">This is different than removing a trusted root certificate.</span></span> <span data-ttu-id="09466-300">若您從 Azure 移除受信任的根憑證 .cer，就會撤銷所有由撤銷的根憑證所產生/簽署的用戶端憑證之存取權。</span><span class="sxs-lookup"><span data-stu-id="09466-300">If you remove a trusted root certificate .cer from Azure, it revokes the access for all client certificates generated/signed by the revoked root certificate.</span></span> <span data-ttu-id="09466-301">撤銷用戶端憑證，而不是根憑證，可以繼續使用從根憑證產生的憑證進行驗證。</span><span class="sxs-lookup"><span data-stu-id="09466-301">Revoking a client certificate, rather than the root certificate, allows the other certificates that were generated from the root certificate to continue to be used for authentication.</span></span>

<span data-ttu-id="09466-302">常見的做法是使用根憑證管理小組或組織層級的存取權，然後使用撤銷的用戶端憑證針對個別使用者進行細部的存取控制。</span><span class="sxs-lookup"><span data-stu-id="09466-302">The common practice is to use the root certificate to manage access at team or organization levels, while using revoked client certificates for fine-grained access control on individual users.</span></span>

### <span data-ttu-id="09466-303"><a name="revokeclientcert"></a>撤銷用戶端憑證</span><span class="sxs-lookup"><span data-stu-id="09466-303"><a name="revokeclientcert"></a>To revoke a client certificate</span></span>

1. <span data-ttu-id="09466-304">擷取用戶端憑證指紋。</span><span class="sxs-lookup"><span data-stu-id="09466-304">Retrieve the client certificate thumbprint.</span></span> <span data-ttu-id="09466-305">如需詳細資訊，請參閱[做法：擷取憑證的指紋](https://msdn.microsoft.com/library/ms734695.aspx)。</span><span class="sxs-lookup"><span data-stu-id="09466-305">For more information, see [How to retrieve the Thumbprint of a Certificate](https://msdn.microsoft.com/library/ms734695.aspx).</span></span>
2. <span data-ttu-id="09466-306">將資訊複製到文字編輯器，並移除所有的空格，讓它是連續字串。</span><span class="sxs-lookup"><span data-stu-id="09466-306">Copy the information to a text editor and remove all spaces so that it is a continuous string.</span></span> <span data-ttu-id="09466-307">這個字串在下一個步驟中會宣告為變數。</span><span class="sxs-lookup"><span data-stu-id="09466-307">This string is declared as a variable in the next step.</span></span>
3. <span data-ttu-id="09466-308">宣告變數。</span><span class="sxs-lookup"><span data-stu-id="09466-308">Declare the variables.</span></span> <span data-ttu-id="09466-309">請確定宣告您在上一個步驟中擷取的指紋。</span><span class="sxs-lookup"><span data-stu-id="09466-309">Make sure to declare the thumbprint you retrieved in the previous step.</span></span>

  ```powershell
  $RevokedClientCert1 = "NameofCertificate"
  $RevokedThumbprint1 = "‎51ab1edd8da4cfed77e20061c5eb6d2ef2f778c7"
  $GWName = "Name_of_virtual_network_gateway"
  $RG = "Name_of_resource_group"
  ```
4. <span data-ttu-id="09466-310">將指紋新增到撤銷的憑證清單。</span><span class="sxs-lookup"><span data-stu-id="09466-310">Add the thumbprint to the list of revoked certificates.</span></span> <span data-ttu-id="09466-311">指紋新增時，您會看到「成功」。</span><span class="sxs-lookup"><span data-stu-id="09466-311">You see "Succeeded" when the thumbprint has been added.</span></span>

  ```powershell
  Add-AzureRmVpnClientRevokedCertificate -VpnClientRevokedCertificateName $RevokedClientCert1 `
  -VirtualNetworkGatewayName $GWName -ResourceGroupName $RG `
  -Thumbprint $RevokedThumbprint1
  ```
5. <span data-ttu-id="09466-312">確認指紋已新增到憑證撤銷清單。</span><span class="sxs-lookup"><span data-stu-id="09466-312">Verify that the thumbprint was added to the certificate revocation list.</span></span>

  ```powershell
  Get-AzureRmVpnClientRevokedCertificate -VirtualNetworkGatewayName $GWName -ResourceGroupName $RG
  ```
6. <span data-ttu-id="09466-313">新增指紋之後，憑證無法再用於連線接。</span><span class="sxs-lookup"><span data-stu-id="09466-313">After the thumbprint has been added, the certificate can no longer be used to connect.</span></span> <span data-ttu-id="09466-314">嘗試使用此憑證進行連線的用戶端會收到訊息，指出憑證不再有效。</span><span class="sxs-lookup"><span data-stu-id="09466-314">Clients that try to connect using this certificate receive a message saying that the certificate is no longer valid.</span></span>

### <span data-ttu-id="09466-315"><a name="reinstateclientcert"></a>恢復用戶端憑證</span><span class="sxs-lookup"><span data-stu-id="09466-315"><a name="reinstateclientcert"></a>To reinstate a client certificate</span></span>

<span data-ttu-id="09466-316">您可以從撤銷的用戶端憑證清單中移除指紋來恢復用戶端憑證。</span><span class="sxs-lookup"><span data-stu-id="09466-316">You can reinstate a client certificate by removing the thumbprint from the list of revoked client certificates.</span></span>

1. <span data-ttu-id="09466-317">宣告變數。</span><span class="sxs-lookup"><span data-stu-id="09466-317">Declare the variables.</span></span> <span data-ttu-id="09466-318">請確定針對您要恢復的憑證宣告正確指紋。</span><span class="sxs-lookup"><span data-stu-id="09466-318">Make sure you declare the correct thumbprint for the certificate that you want to reinstate.</span></span>

  ```powershell
  $RevokedClientCert1 = "NameofCertificate"
  $RevokedThumbprint1 = "‎51ab1edd8da4cfed77e20061c5eb6d2ef2f778c7"
  $GWName = "Name_of_virtual_network_gateway"
  $RG = "Name_of_resource_group"
  ```
2. <span data-ttu-id="09466-319">從憑證撤銷清單中移除憑證指紋。</span><span class="sxs-lookup"><span data-stu-id="09466-319">Remove the certificate thumbprint from the certificate revocation list.</span></span>

  ```powershell
  Remove-AzureRmVpnClientRevokedCertificate -VpnClientRevokedCertificateName $RevokedClientCert1 `
  -VirtualNetworkGatewayName $GWName -ResourceGroupName $RG -Thumbprint $RevokedThumbprint1
  ```
3. <span data-ttu-id="09466-320">檢查指紋是否已從撤銷的清單中移除。</span><span class="sxs-lookup"><span data-stu-id="09466-320">Check if the thumbprint is removed from the revoked list.</span></span>

  ```powershell
  Get-AzureRmVpnClientRevokedCertificate -VirtualNetworkGatewayName $GWName -ResourceGroupName $RG
  ```

## <span data-ttu-id="09466-321"><a name="faq"></a>點對站常見問題集</span><span class="sxs-lookup"><span data-stu-id="09466-321"><a name="faq"></a>Point-to-Site FAQ</span></span>

[!INCLUDE [Point-to-Site FAQ](../../includes/vpn-gateway-point-to-site-faq-include.md)]

## <a name="next-steps"></a><span data-ttu-id="09466-322">後續步驟</span><span class="sxs-lookup"><span data-stu-id="09466-322">Next steps</span></span>
<span data-ttu-id="09466-323">一旦完成您的連接，就可以將虛擬機器加入您的虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="09466-323">Once your connection is complete, you can add virtual machines to your virtual networks.</span></span> <span data-ttu-id="09466-324">如需詳細資訊，請參閱[虛擬機器](https://docs.microsoft.com/azure/#pivot=services&panel=Compute)。</span><span class="sxs-lookup"><span data-stu-id="09466-324">For more information, see [Virtual Machines](https://docs.microsoft.com/azure/#pivot=services&panel=Compute).</span></span> <span data-ttu-id="09466-325">若要了解網路與虛擬機器的詳細資訊，請參閱 [Azure 與 Linux VM 網路概觀](../virtual-machines/linux/azure-vm-network-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="09466-325">To understand more about networking and virtual machines, see [Azure and Linux VM network overview](../virtual-machines/linux/azure-vm-network-overview.md).</span></span>