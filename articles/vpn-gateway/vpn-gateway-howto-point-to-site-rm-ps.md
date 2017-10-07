---
title: "連接電腦 tooan 使用點對站 Azure 虛擬網路和憑證驗證： PowerShell |Microsoft 文件"
description: "安全地連接電腦 tooyour 虛擬網路建立點對站 VPN 閘道連線使用憑證驗證。 本文適用於 toohello Resource Manager 部署模型，並使用 PowerShell。"
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
ms.openlocfilehash: b962e4b1946a4ae17d4eb2b920ed54437bc26b61
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="configure-a-point-to-site-connection-tooa-vnet-using-certificate-authentication-powershell"></a><span data-ttu-id="d01c2-104">設定點對站連線 tooa VNet 使用憑證驗證： PowerShell</span><span class="sxs-lookup"><span data-stu-id="d01c2-104">Configure a Point-to-Site connection tooa VNet using certificate authentication: PowerShell</span></span>

<span data-ttu-id="d01c2-105">本文章將示範如何 toocreate hello 資源管理員部署中的點對站連接的 VNet 模型使用 PowerShell。</span><span class="sxs-lookup"><span data-stu-id="d01c2-105">This article shows you how toocreate a VNet with a Point-to-Site connection in hello Resource Manager deployment model using PowerShell.</span></span> <span data-ttu-id="d01c2-106">此組態會使用用戶端連接的憑證 tooauthenticate hello。</span><span class="sxs-lookup"><span data-stu-id="d01c2-106">This configuration uses certificates tooauthenticate hello connecting client.</span></span> <span data-ttu-id="d01c2-107">您也可以建立此組態使用不同的部署工具或部署模型，從下列清單中的 hello 選取不同的選項：</span><span class="sxs-lookup"><span data-stu-id="d01c2-107">You can also create this configuration using a different deployment tool or deployment model by selecting a different option from hello following list:</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="d01c2-108">Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="d01c2-108">Azure portal</span></span>](vpn-gateway-howto-point-to-site-resource-manager-portal.md)
> * [<span data-ttu-id="d01c2-109">PowerShell</span><span class="sxs-lookup"><span data-stu-id="d01c2-109">PowerShell</span></span>](vpn-gateway-howto-point-to-site-rm-ps.md)
> * [<span data-ttu-id="d01c2-110">Azure 入口網站 (傳統)</span><span class="sxs-lookup"><span data-stu-id="d01c2-110">Azure portal (classic)</span></span>](vpn-gateway-howto-point-to-site-classic-azure-portal.md)
>
>

<span data-ttu-id="d01c2-111">點對站 (P2S) VPN 閘道，可讓您建立從個別的用戶端電腦的安全連線 tooyour 虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="d01c2-111">A Point-to-Site (P2S) VPN gateway lets you create a secure connection tooyour virtual network from an individual client computer.</span></span> <span data-ttu-id="d01c2-112">當您想要 tooconnect tooyour 從遠端位置，例如當您從家裡或會議 telecommuting VNet，點對站 VPN 連線會很有用。</span><span class="sxs-lookup"><span data-stu-id="d01c2-112">Point-to-Site VPN connections are useful when you want tooconnect tooyour VNet from a remote location, such when you are telecommuting from home or a conference.</span></span> <span data-ttu-id="d01c2-113">您有只有少數的用戶端需要 tooconnect tooa VNet 時 P2S VPN 也很有用的方案 toouse，而不是站對站 VPN。</span><span class="sxs-lookup"><span data-stu-id="d01c2-113">A P2S VPN is also a useful solution toouse instead of a Site-to-Site VPN when you have only a few clients that need tooconnect tooa VNet.</span></span>

<span data-ttu-id="d01c2-114">使用 P2S hello 安全通訊端通道通訊協定 (SSTP)，這是 SSL 型 VPN 通訊協定。</span><span class="sxs-lookup"><span data-stu-id="d01c2-114">P2S uses hello Secure Socket Tunneling Protocol (SSTP), which is an SSL-based VPN protocol.</span></span> <span data-ttu-id="d01c2-115">建立之 P2S VPN 連線從 hello 用戶端電腦。</span><span class="sxs-lookup"><span data-stu-id="d01c2-115">A P2S VPN connection is established by starting it from hello client computer.</span></span>

![連接電腦 tooan Azure VNet 的點對站連接圖表](./media/vpn-gateway-howto-point-to-site-rm-ps/point-to-site-diagram.png)

<span data-ttu-id="d01c2-117">點對站憑證驗證的連接需要 hello 下列：</span><span class="sxs-lookup"><span data-stu-id="d01c2-117">Point-to-Site certificate authentication connections require hello following:</span></span>

* <span data-ttu-id="d01c2-118">RouteBased VPN 閘道。</span><span class="sxs-lookup"><span data-stu-id="d01c2-118">A RouteBased VPN gateway.</span></span>
* <span data-ttu-id="d01c2-119">hello 公開金鑰 （.cer 檔案） 的根憑證，也就是上傳的 tooAzure。</span><span class="sxs-lookup"><span data-stu-id="d01c2-119">hello public key (.cer file) for a root certificate, which is uploaded tooAzure.</span></span> <span data-ttu-id="d01c2-120">一旦上傳 hello 憑證時，它會被視為受信任的憑證，並用於驗證。</span><span class="sxs-lookup"><span data-stu-id="d01c2-120">Once hello certificate is uploaded, it is considered a trusted certificate and is used for authentication.</span></span>
* <span data-ttu-id="d01c2-121">會產生從 hello 根憑證，並將連接 toohello VNet 每部用戶端電腦上安裝用戶端憑證。</span><span class="sxs-lookup"><span data-stu-id="d01c2-121">A client certificate that is generated from hello root certificate and installed on each client computer that will connect toohello VNet.</span></span> <span data-ttu-id="d01c2-122">此憑證使用於用戶端憑證。</span><span class="sxs-lookup"><span data-stu-id="d01c2-122">This certificate is used for client authentication.</span></span>
* <span data-ttu-id="d01c2-123">VPN 用戶端組態套件。</span><span class="sxs-lookup"><span data-stu-id="d01c2-123">A VPN client configuration package.</span></span> <span data-ttu-id="d01c2-124">hello VPN 用戶端組態封裝包含 hello 的 hello 用戶端 tooconnect toohello VNet 的必要資訊。</span><span class="sxs-lookup"><span data-stu-id="d01c2-124">hello VPN client configuration package contains hello necessary information for hello client tooconnect toohello VNet.</span></span> <span data-ttu-id="d01c2-125">hello 封裝設定 hello 現有 VPN 用戶端是原生 toohello Windows 作業系統。</span><span class="sxs-lookup"><span data-stu-id="d01c2-125">hello package configures hello existing VPN client that is native toohello Windows operating system.</span></span> <span data-ttu-id="d01c2-126">每個連接的用戶端必須使用 hello 組態封裝設定。</span><span class="sxs-lookup"><span data-stu-id="d01c2-126">Each client that connects must be configured using hello configuration package.</span></span>

<span data-ttu-id="d01c2-127">點對站連線不需要 VPN 裝置或內部部署公眾對應 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="d01c2-127">Point-to-Site connections do not require a VPN device or an on-premises public-facing IP address.</span></span> <span data-ttu-id="d01c2-128">hello VPN 連線建立透過 SSTP （安全通訊端通道通訊協定）。</span><span class="sxs-lookup"><span data-stu-id="d01c2-128">hello VPN connection is created over SSTP (Secure Socket Tunneling Protocol).</span></span> <span data-ttu-id="d01c2-129">在 hello 伺服器端，我們支援 SSTP 版本 1.0、 1.1 和 1.2。</span><span class="sxs-lookup"><span data-stu-id="d01c2-129">On hello server side, we support SSTP versions 1.0, 1.1, and 1.2.</span></span> <span data-ttu-id="d01c2-130">hello 用戶端決定哪一個版本 toouse。</span><span class="sxs-lookup"><span data-stu-id="d01c2-130">hello client decides which version toouse.</span></span> <span data-ttu-id="d01c2-131">若為 Windows 8.1 和更新版本，SSTP 預設使用 1.2。</span><span class="sxs-lookup"><span data-stu-id="d01c2-131">For Windows 8.1 and above, SSTP uses 1.2 by default.</span></span> 

<span data-ttu-id="d01c2-132">如需有關點對站連線的詳細資訊，請參閱 hello[點對站常見問題集](#faq)hello 本文結尾處。</span><span class="sxs-lookup"><span data-stu-id="d01c2-132">For more information about Point-to-Site connections, see hello [Point-to-Site FAQ](#faq) at hello end of this article.</span></span>

## <a name="before-beginning"></a><span data-ttu-id="d01c2-133">開始之前</span><span class="sxs-lookup"><span data-stu-id="d01c2-133">Before beginning</span></span>

* <span data-ttu-id="d01c2-134">請確認您有 Azure 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="d01c2-134">Verify that you have an Azure subscription.</span></span> <span data-ttu-id="d01c2-135">如果您還沒有 Azure 訂用帳戶，則可以啟用 [MSDN 訂戶權益](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details)或註冊[免費帳戶](https://azure.microsoft.com/pricing/free-trial)。</span><span class="sxs-lookup"><span data-stu-id="d01c2-135">If you don't already have an Azure subscription, you can activate your [MSDN subscriber benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details) or sign up for a [free account](https://azure.microsoft.com/pricing/free-trial).</span></span>
* <span data-ttu-id="d01c2-136">安裝 hello hello Azure 資源管理員的 PowerShell 指令程式最新版本。</span><span class="sxs-lookup"><span data-stu-id="d01c2-136">Install hello latest version of hello Azure Resource Manager PowerShell cmdlets.</span></span> <span data-ttu-id="d01c2-137">如需安裝 PowerShell cmdlet 的詳細資訊，請參閱[如何 tooinstall 和設定 Azure PowerShell](/powershell/azure/overview)。</span><span class="sxs-lookup"><span data-stu-id="d01c2-137">For more information about installing PowerShell cmdlets, see [How tooinstall and configure Azure PowerShell](/powershell/azure/overview).</span></span>

### <span data-ttu-id="d01c2-138"><a name="example"></a>範例值</span><span class="sxs-lookup"><span data-stu-id="d01c2-138"><a name="example"></a>Example values</span></span>

<span data-ttu-id="d01c2-139">您可以使用 hello 範例值 toocreate 測試環境中，或參閱 toothese 值 toobetter 了解這篇文章中的 hello 範例。</span><span class="sxs-lookup"><span data-stu-id="d01c2-139">You can use hello example values toocreate a test environment, or refer toothese values toobetter understand hello examples in this article.</span></span> <span data-ttu-id="d01c2-140">我們設定一節中的 hello 變數[1](#declare) hello 發行項。</span><span class="sxs-lookup"><span data-stu-id="d01c2-140">We set hello variables in section [1](#declare) of hello article.</span></span> <span data-ttu-id="d01c2-141">您可以使用 hello 步驟逐步解說，以和使用 hello 值而不需要變更，或變更這些 tooreflect 您的環境。</span><span class="sxs-lookup"><span data-stu-id="d01c2-141">You can either use hello steps as a walk-through and use hello values without changing them, or change them tooreflect your environment.</span></span> 

* <span data-ttu-id="d01c2-142">**名稱：VNet1**</span><span class="sxs-lookup"><span data-stu-id="d01c2-142">**Name: VNet1**</span></span>
* <span data-ttu-id="d01c2-143">**位址空間：192.168.0.0/16** 和 **10.254.0.0/16**</span><span class="sxs-lookup"><span data-stu-id="d01c2-143">**Address space: 192.168.0.0/16** and **10.254.0.0/16**</span></span><br><span data-ttu-id="d01c2-144">此範例中，我們使用一個以上的位址空間 tooillustrate 這項設定適用於多個位址空間。</span><span class="sxs-lookup"><span data-stu-id="d01c2-144">For this example, we use more than one address space tooillustrate that this configuration works with multiple address spaces.</span></span> <span data-ttu-id="d01c2-145">不過，此組態不需要多個位址空間。</span><span class="sxs-lookup"><span data-stu-id="d01c2-145">However, multiple address spaces are not required for this configuration.</span></span>
* <span data-ttu-id="d01c2-146">**子網路名稱：FrontEnd**</span><span class="sxs-lookup"><span data-stu-id="d01c2-146">**Subnet name: FrontEnd**</span></span>
  * <span data-ttu-id="d01c2-147">**子網路位址範圍：192.168.1.0/24**</span><span class="sxs-lookup"><span data-stu-id="d01c2-147">**Subnet address range: 192.168.1.0/24**</span></span>
* <span data-ttu-id="d01c2-148">**子網路名稱：BackEnd**</span><span class="sxs-lookup"><span data-stu-id="d01c2-148">**Subnet name: BackEnd**</span></span>
  * <span data-ttu-id="d01c2-149">**子網路位址範圍：10.254.1.0/24**</span><span class="sxs-lookup"><span data-stu-id="d01c2-149">**Subnet address range: 10.254.1.0/24**</span></span>
* <span data-ttu-id="d01c2-150">**子網路名稱：GatewaySubnet**</span><span class="sxs-lookup"><span data-stu-id="d01c2-150">**Subnet name: GatewaySubnet**</span></span><br><span data-ttu-id="d01c2-151">hello 子網路名稱*GatewaySubnet*對於 hello VPN 閘道 toowork 是必要的。</span><span class="sxs-lookup"><span data-stu-id="d01c2-151">hello Subnet name *GatewaySubnet* is mandatory for hello VPN gateway toowork.</span></span>
  * <span data-ttu-id="d01c2-152">**閘道子網路位址範圍：192.168.200.0/24**</span><span class="sxs-lookup"><span data-stu-id="d01c2-152">**GatewaySubnet address range: 192.168.200.0/24**</span></span> 
* <span data-ttu-id="d01c2-153">**VPN 用戶端位址集區：172.16.201.0/24**</span><span class="sxs-lookup"><span data-stu-id="d01c2-153">**VPN client address pool: 172.16.201.0/24**</span></span><br><span data-ttu-id="d01c2-154">連接 toohello VNet 使用這個點對站連線的 VPN 用戶端收到 hello VPN 用戶端位址集區的 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="d01c2-154">VPN clients that connect toohello VNet using this Point-to-Site connection receive an IP address from hello VPN client address pool.</span></span>
* <span data-ttu-id="d01c2-155">**訂用帳戶：**如果您有多個訂用帳戶，確認您是否使用 hello 正確。</span><span class="sxs-lookup"><span data-stu-id="d01c2-155">**Subscription:** If you have more than one subscription, verify that you are using hello correct one.</span></span>
* <span data-ttu-id="d01c2-156">**資源群組：TestRG**</span><span class="sxs-lookup"><span data-stu-id="d01c2-156">**Resource Group: TestRG**</span></span>
* <span data-ttu-id="d01c2-157">**位置：美國東部**</span><span class="sxs-lookup"><span data-stu-id="d01c2-157">**Location: East US**</span></span>
* <span data-ttu-id="d01c2-158">**DNS 伺服器： IP 位址**hello toouse 需名稱解析的 DNS 伺服器。</span><span class="sxs-lookup"><span data-stu-id="d01c2-158">**DNS Server: IP address** of hello DNS server that you want toouse for name resolution.</span></span>
* <span data-ttu-id="d01c2-159">**GW 名稱：Vnet1GW**</span><span class="sxs-lookup"><span data-stu-id="d01c2-159">**GW Name: Vnet1GW**</span></span>
* <span data-ttu-id="d01c2-160">**公用 IP 名稱：VNet1GWPIP**</span><span class="sxs-lookup"><span data-stu-id="d01c2-160">**Public IP name: VNet1GWPIP**</span></span>
* <span data-ttu-id="d01c2-161">**VpnType：RouteBased**</span><span class="sxs-lookup"><span data-stu-id="d01c2-161">**VpnType: RouteBased**</span></span> 

## <span data-ttu-id="d01c2-162"><a name="declare"></a>1.登入和設定變數</span><span class="sxs-lookup"><span data-stu-id="d01c2-162"><a name="declare"></a>1. Log in and set variables</span></span>

<span data-ttu-id="d01c2-163">在本節中，您可以登入，並宣告 hello 值用於此設定。</span><span class="sxs-lookup"><span data-stu-id="d01c2-163">In this section, you log in and declare hello values used for this configuration.</span></span> <span data-ttu-id="d01c2-164">hello 宣告 hello 範例指令碼中使用值。</span><span class="sxs-lookup"><span data-stu-id="d01c2-164">hello declared values are used in hello sample scripts.</span></span> <span data-ttu-id="d01c2-165">變更 hello 值 tooreflect 您自己的環境。</span><span class="sxs-lookup"><span data-stu-id="d01c2-165">Change hello values tooreflect your own environment.</span></span> <span data-ttu-id="d01c2-166">或者，您可以使用 hello 宣告值，並瀏覽 hello 步驟中，當做練習。</span><span class="sxs-lookup"><span data-stu-id="d01c2-166">Or, you can use hello declared values and go through hello steps as an exercise.</span></span>

1. <span data-ttu-id="d01c2-167">使用提高的權限開啟 PowerShell 主控台，並登入 tooyour Azure 帳戶。</span><span class="sxs-lookup"><span data-stu-id="d01c2-167">Open your PowerShell console with elevated privileges, and log in tooyour Azure account.</span></span> <span data-ttu-id="d01c2-168">此 cmdlet 會提示您輸入 hello 登入認證。</span><span class="sxs-lookup"><span data-stu-id="d01c2-168">This cmdlet prompts you for hello login credentials.</span></span> <span data-ttu-id="d01c2-169">登入之後，它會下載您的帳戶設定，使其可用 tooAzure PowerShell。</span><span class="sxs-lookup"><span data-stu-id="d01c2-169">After logging in, it downloads your account settings so that they are available tooAzure PowerShell.</span></span>

  ```powershell
  Login-AzureRmAccount
  ```
2. <span data-ttu-id="d01c2-170">取得您的 Azure 訂用帳戶清單。</span><span class="sxs-lookup"><span data-stu-id="d01c2-170">Get a list of your Azure subscriptions.</span></span>

  ```powershell
  Get-AzureRmSubscription
  ```
3. <span data-ttu-id="d01c2-171">指定您想 toouse hello 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="d01c2-171">Specify hello subscription that you want toouse.</span></span>

  ```powershell
  Select-AzureRmSubscription -SubscriptionName "Name of subscription"
  ```
4. <span data-ttu-id="d01c2-172">宣告您想 toouse hello 變數。</span><span class="sxs-lookup"><span data-stu-id="d01c2-172">Declare hello variables that you want toouse.</span></span> <span data-ttu-id="d01c2-173">下列範例中，替代 hello 值供自己在必要時，就會使用 hello。</span><span class="sxs-lookup"><span data-stu-id="d01c2-173">Use hello following sample, substituting hello values for your own when necessary.</span></span>

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

## <span data-ttu-id="d01c2-174"><a name="ConfigureVNet"></a>2.設定 VNet</span><span class="sxs-lookup"><span data-stu-id="d01c2-174"><a name="ConfigureVNet"></a>2. Configure a VNet</span></span>

1. <span data-ttu-id="d01c2-175">建立資源群組。</span><span class="sxs-lookup"><span data-stu-id="d01c2-175">Create a resource group.</span></span>

  ```powershell
  New-AzureRmResourceGroup -Name $RG -Location $Location
  ```
2. <span data-ttu-id="d01c2-176">建立 hello hello 虛擬網路，請加以命名的子網路組態*前端*，*後端*，和*GatewaySubnet*。</span><span class="sxs-lookup"><span data-stu-id="d01c2-176">Create hello subnet configurations for hello virtual network, naming them *FrontEnd*, *BackEnd*, and *GatewaySubnet*.</span></span> <span data-ttu-id="d01c2-177">這些前置詞必須是 hello 您宣告的 VNet 位址空間的一部分。</span><span class="sxs-lookup"><span data-stu-id="d01c2-177">These prefixes must be part of hello VNet address space that you declared.</span></span>

  ```powershell
  $fesub = New-AzureRmVirtualNetworkSubnetConfig -Name $FESubName -AddressPrefix $FESubPrefix
  $besub = New-AzureRmVirtualNetworkSubnetConfig -Name $BESubName -AddressPrefix $BESubPrefix
  $gwsub = New-AzureRmVirtualNetworkSubnetConfig -Name $GWSubName -AddressPrefix $GWSubPrefix
  ```
3. <span data-ttu-id="d01c2-178">建立 hello 虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="d01c2-178">Create hello virtual network.</span></span>

  <span data-ttu-id="d01c2-179">在此範例中，hello DNS 伺服器是選擇性的。</span><span class="sxs-lookup"><span data-stu-id="d01c2-179">In this example, hello DNS server is optional.</span></span> <span data-ttu-id="d01c2-180">指定一個值並不會建立新的 DNS 伺服器。</span><span class="sxs-lookup"><span data-stu-id="d01c2-180">Specifying a value does not create a new DNS server.</span></span> <span data-ttu-id="d01c2-181">hello 您指定的 DNS 伺服器 IP 位址應該可以解決 hello 您所連接的 hello 資源名稱的 DNS 伺服器。</span><span class="sxs-lookup"><span data-stu-id="d01c2-181">hello DNS server IP address that you specify should be a DNS server that can resolve hello names for hello resources you are connecting to.</span></span> <span data-ttu-id="d01c2-182">例如，我們使用私人 IP 位址，但很可能這不是您的 DNS 伺服器 hello IP 位址。</span><span class="sxs-lookup"><span data-stu-id="d01c2-182">For this example, we used a private IP address, but it is likely that this is not hello IP address of your DNS server.</span></span> <span data-ttu-id="d01c2-183">為確定 toouse 您自己的值。</span><span class="sxs-lookup"><span data-stu-id="d01c2-183">Be sure toouse your own values.</span></span>

  ```powershell
  New-AzureRmVirtualNetwork -Name $VNetName -ResourceGroupName $RG -Location $Location -AddressPrefix $VNetPrefix1,$VNetPrefix2 -Subnet $fesub, $besub, $gwsub -DnsServer $DNS
  ```
4. <span data-ttu-id="d01c2-184">指定您所建立的 hello 虛擬網路的 hello 變數。</span><span class="sxs-lookup"><span data-stu-id="d01c2-184">Specify hello variables for hello virtual network you created.</span></span>

  ```powershell
  $vnet = Get-AzureRmVirtualNetwork -Name $VNetName -ResourceGroupName $RG
  $subnet = Get-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -VirtualNetwork $vnet
  ```
5. <span data-ttu-id="d01c2-185">VPN 閘道必須具有公用 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="d01c2-185">A VPN gateway must have a Public IP address.</span></span> <span data-ttu-id="d01c2-186">您第一次要求 hello IP 位址資源，並建立您的虛擬網路閘道時參考 tooit。</span><span class="sxs-lookup"><span data-stu-id="d01c2-186">You first request hello IP address resource, and then refer tooit when creating your virtual network gateway.</span></span> <span data-ttu-id="d01c2-187">hello IP 位址建立 hello VPN 閘道時，會動態指定 toohello 資源。</span><span class="sxs-lookup"><span data-stu-id="d01c2-187">hello IP address is dynamically assigned toohello resource when hello VPN gateway is created.</span></span> <span data-ttu-id="d01c2-188">VPN 閘道目前僅支援*動態*公用 IP 位址配置。</span><span class="sxs-lookup"><span data-stu-id="d01c2-188">VPN Gateway currently only supports *Dynamic* Public IP address allocation.</span></span> <span data-ttu-id="d01c2-189">您無法要求靜態公用 IP 位址指派。</span><span class="sxs-lookup"><span data-stu-id="d01c2-189">You cannot request a Static Public IP address assignment.</span></span> <span data-ttu-id="d01c2-190">不過，它並不表示 hello IP 位址變更之後已被指派 tooyour VPN 閘道。</span><span class="sxs-lookup"><span data-stu-id="d01c2-190">However, it doesn't mean that hello IP address changes after it has been assigned tooyour VPN gateway.</span></span> <span data-ttu-id="d01c2-191">hello 公用 IP 位址變更為當 hello 閘道 hello 才會刪除並重新建立。</span><span class="sxs-lookup"><span data-stu-id="d01c2-191">hello only time hello Public IP address changes is when hello gateway is deleted and re-created.</span></span> <span data-ttu-id="d01c2-192">它不會因為重新調整、重設或 VPN 閘道的其他內部維護/升級而變更。</span><span class="sxs-lookup"><span data-stu-id="d01c2-192">It doesn't change across resizing, resetting, or other internal maintenance/upgrades of your VPN gateway.</span></span>

  <span data-ttu-id="d01c2-193">要求動態指派的公用 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="d01c2-193">Request a dynamically assigned public IP address.</span></span>

  ```powershell
  $pip = New-AzureRmPublicIpAddress -Name $GWIPName -ResourceGroupName $RG -Location $Location -AllocationMethod Dynamic
  $ipconf = New-AzureRmVirtualNetworkGatewayIpConfig -Name $GWIPconfName -Subnet $subnet -PublicIpAddress $pip
  ```

## <span data-ttu-id="d01c2-194"><a name="creategateway"></a>3.建立 hello VPN 閘道</span><span class="sxs-lookup"><span data-stu-id="d01c2-194"><a name="creategateway"></a>3. Create hello VPN gateway</span></span>

<span data-ttu-id="d01c2-195">設定並建立 hello 虛擬網路閘道的 VNet。</span><span class="sxs-lookup"><span data-stu-id="d01c2-195">Configure and create hello virtual network gateway for your VNet.</span></span>

* <span data-ttu-id="d01c2-196">hello *-gatewaytype 的授權*必須**Vpn**和 hello *-VpnType*必須**RouteBased**。</span><span class="sxs-lookup"><span data-stu-id="d01c2-196">hello *-GatewayType* must be **Vpn** and hello *-VpnType* must be **RouteBased**.</span></span>
* <span data-ttu-id="d01c2-197">VPN 閘道可能會佔用 too45 分鐘 toocomplete 根據 hello[閘道 sku](vpn-gateway-about-vpn-gateway-settings.md)您選取。</span><span class="sxs-lookup"><span data-stu-id="d01c2-197">A VPN gateway can take up too45 minutes toocomplete, depending on hello [gateway sku](vpn-gateway-about-vpn-gateway-settings.md) you select.</span></span>

```powershell
New-AzureRmVirtualNetworkGateway -Name $GWName -ResourceGroupName $RG `
-Location $Location -IpConfigurations $ipconf -GatewayType Vpn `
-VpnType RouteBased -EnableBgp $false -GatewaySku VpnGw1 `
```

## <span data-ttu-id="d01c2-198"><a name="addresspool"></a>4.新增 hello VPN 用戶端位址集區</span><span class="sxs-lookup"><span data-stu-id="d01c2-198"><a name="addresspool"></a>4. Add hello VPN client address pool</span></span>

<span data-ttu-id="d01c2-199">Hello VPN 閘道完成建立之後，您可以加入 hello VPN 用戶端位址集區。</span><span class="sxs-lookup"><span data-stu-id="d01c2-199">After hello VPN gateway finishes creating, you can add hello VPN client address pool.</span></span> <span data-ttu-id="d01c2-200">hello VPN 用戶端位址集區是 hello VPN 用戶端接收的 IP 位址連接時的 hello 範圍。</span><span class="sxs-lookup"><span data-stu-id="d01c2-200">hello VPN client address pool is hello range from which hello VPN clients receive an IP address when connecting.</span></span> <span data-ttu-id="d01c2-201">搭配您從，連接的 hello 在內部部署位置或 hello 您想要 tooconnect 的 VNet，請使用私用的 IP 位址範圍不會重疊。</span><span class="sxs-lookup"><span data-stu-id="d01c2-201">Use a private IP address range that does not overlap with hello on-premises location that you connect from, or with hello VNet that you want tooconnect to.</span></span> <span data-ttu-id="d01c2-202">在此範例中，宣告 hello VPN 用戶端位址集區為[變數](#declare)在步驟 1 中。</span><span class="sxs-lookup"><span data-stu-id="d01c2-202">In this example, hello VPN client address pool is declared as a [variable](#declare) in Step 1.</span></span>

```powershell
$Gateway = Get-AzureRmVirtualNetworkGateway -ResourceGroupName $RG -Name $GWName
Set-AzureRmVirtualNetworkGateway -VirtualNetworkGateway $Gateway -VpnClientAddressPool $VPNClientAddressPool
```

## <span data-ttu-id="d01c2-203"><a name="Certificates"></a>5.產生憑證</span><span class="sxs-lookup"><span data-stu-id="d01c2-203"><a name="Certificates"></a>5. Generate certificates</span></span>

<span data-ttu-id="d01c2-204">憑證是由 Azure tooauthenticate VPN 用戶端用於點對站 Vpn。</span><span class="sxs-lookup"><span data-stu-id="d01c2-204">Certificates are used by Azure tooauthenticate VPN clients for Point-to-Site VPNs.</span></span> <span data-ttu-id="d01c2-205">您上傳 hello 的公開金鑰資訊 hello 根憑證 tooAzure。</span><span class="sxs-lookup"><span data-stu-id="d01c2-205">You upload hello public key information of hello root certificate tooAzure.</span></span> <span data-ttu-id="d01c2-206">hello 公開金鑰則被視為 'trusted'。</span><span class="sxs-lookup"><span data-stu-id="d01c2-206">hello public key is then considered 'trusted'.</span></span> <span data-ttu-id="d01c2-207">用戶端憑證必須從 hello 受信任的根憑證，所產生，並安裝 hello 憑證-目前的使用者/個人憑證存放區中每個用戶端電腦上。</span><span class="sxs-lookup"><span data-stu-id="d01c2-207">Client certificates must be generated from hello trusted root certificate, and then installed on each client computer in hello Certificates-Current User/Personal certificate store.</span></span> <span data-ttu-id="d01c2-208">hello 憑證時，使用的 tooauthenticate hello 用戶端會起始連線 toohello VNet。</span><span class="sxs-lookup"><span data-stu-id="d01c2-208">hello certificate is used tooauthenticate hello client when it initiates a connection toohello VNet.</span></span> 

<span data-ttu-id="d01c2-209">如果您使用自我簽署憑證，則必須使用特定參數來建立這些憑證。</span><span class="sxs-lookup"><span data-stu-id="d01c2-209">If you use self-signed certificates, they must be created using specific parameters.</span></span> <span data-ttu-id="d01c2-210">您可以建立自我簽署的憑證，使用 hello 指示[PowerShell 和 Windows 10](vpn-gateway-certificates-point-to-site.md)，或者，如果您沒有 Windows 10，您可以使用[MakeCert](vpn-gateway-certificates-point-to-site-makecert.md)。</span><span class="sxs-lookup"><span data-stu-id="d01c2-210">You can create a self-signed certificate using hello instructions for [PowerShell and Windows 10](vpn-gateway-certificates-point-to-site.md), or, if you don't have Windows 10, you can use [MakeCert](vpn-gateway-certificates-point-to-site-makecert.md).</span></span> <span data-ttu-id="d01c2-211">請務必產生自我簽署的根憑證和用戶端憑證時，請遵循 hello hello 指示中的步驟。</span><span class="sxs-lookup"><span data-stu-id="d01c2-211">It's important that you follow hello steps in hello instructions when generating self-signed root certificates and client certificates.</span></span> <span data-ttu-id="d01c2-212">否則，您所產生的 hello 憑證不會 P2S 連線與相容，而且您會收到連接錯誤。</span><span class="sxs-lookup"><span data-stu-id="d01c2-212">Otherwise, hello certificates you generate will not be compatible with P2S connections and you will receive a connection error.</span></span>

### <span data-ttu-id="d01c2-213"><a name="cer"></a>1.取得 hello hello 根憑證的.cer 檔案</span><span class="sxs-lookup"><span data-stu-id="d01c2-213"><a name="cer"></a>1. Obtain hello .cer file for hello root certificate</span></span>

[!INCLUDE [vpn-gateway-basic-vnet-rm-portal](../../includes/vpn-gateway-p2s-rootcert-include.md)]


### <span data-ttu-id="d01c2-214"><a name="generate"></a>2.產生用戶端憑證 </span><span class="sxs-lookup"><span data-stu-id="d01c2-214"><a name="generate"></a>2. Generate a client certificate</span></span>

[!INCLUDE [vpn-gateway-basic-vnet-rm-portal](../../includes/vpn-gateway-p2s-clientcert-include.md)]

## <span data-ttu-id="d01c2-215"><a name="upload"></a>6.上傳 hello 根憑證的公開金鑰資訊</span><span class="sxs-lookup"><span data-stu-id="d01c2-215"><a name="upload"></a>6. Upload hello root certificate public key information</span></span>

<span data-ttu-id="d01c2-216">確認 VPN 閘道已完成建立。</span><span class="sxs-lookup"><span data-stu-id="d01c2-216">Verify that your VPN gateway has finished creating.</span></span> <span data-ttu-id="d01c2-217">完成後，您可以上傳 hello.cer 檔案 （其中包含 hello 公開金鑰資訊） 的受信任的根憑證 tooAzure。</span><span class="sxs-lookup"><span data-stu-id="d01c2-217">Once it has completed, you can upload hello .cer file (which contains hello public key information) for a trusted root certificate tooAzure.</span></span> <span data-ttu-id="d01c2-218">一旦上傳 a.cer 檔案時，Azure 可以使用它 tooauthenticate 安裝用戶端，已從 hello 信任的根憑證產生用戶端憑證。</span><span class="sxs-lookup"><span data-stu-id="d01c2-218">Once a.cer file is uploaded, Azure can use it tooauthenticate clients that have installed a client certificate generated from hello trusted root certificate.</span></span> <span data-ttu-id="d01c2-219">如有需要您可以上傳其他受信任的根憑證檔-tooa 總計 20-更新版本中，設定。</span><span class="sxs-lookup"><span data-stu-id="d01c2-219">You can upload additional trusted root certificate files - up tooa total of 20 - later, if needed.</span></span>

1. <span data-ttu-id="d01c2-220">您的憑證名稱，取代 hello 值以您自己的 hello 變數宣告。</span><span class="sxs-lookup"><span data-stu-id="d01c2-220">Declare hello variable for your certificate name, replacing hello value with your own.</span></span>

  ```powershell
  $P2SRootCertName = "P2SRootCert.cer"
  ```
2. <span data-ttu-id="d01c2-221">取代您自己，hello 檔案路徑，然後執行 hello cmdlet。</span><span class="sxs-lookup"><span data-stu-id="d01c2-221">Replace hello file path with your own, and then run hello cmdlets.</span></span>

  ```powershell
  $filePathForCert = "C:\cert\P2SRootCert.cer"
  $cert = new-object System.Security.Cryptography.X509Certificates.X509Certificate2($filePathForCert)
  $CertBase64 = [system.convert]::ToBase64String($cert.RawData)
  $p2srootcert = New-AzureRmVpnClientRootCertificate -Name $P2SRootCertName -PublicCertData $CertBase64
  ```
3. <span data-ttu-id="d01c2-222">上傳 hello 公開金鑰資訊 tooAzure。</span><span class="sxs-lookup"><span data-stu-id="d01c2-222">Upload hello public key information tooAzure.</span></span> <span data-ttu-id="d01c2-223">一旦上傳 hello 憑證資訊時，Azure 會將此 toobe 視為信任的根憑證。</span><span class="sxs-lookup"><span data-stu-id="d01c2-223">Once hello certificate information is uploaded, Azure considers this toobe a trusted root certificate.</span></span>

   ```powershell
  Add-AzureRmVpnClientRootCertificate -VpnClientRootCertificateName $P2SRootCertName -VirtualNetworkGatewayname "VNet1GW" -ResourceGroupName "TestRG" -PublicCertData $CertBase64
  ```

## <span data-ttu-id="d01c2-224"><a name="clientconfig"></a>7.下載 hello VPN 用戶端組態封裝</span><span class="sxs-lookup"><span data-stu-id="d01c2-224"><a name="clientconfig"></a>7. Download hello VPN client configuration package</span></span>

<span data-ttu-id="d01c2-225">tooconnect tooa 使用點對站 VPN 的 VNet，每個用戶端必須安裝以 hello 設定來設定原生 VPN 用戶端 hello 用戶端組態封裝及其必要 tooconnect toohello 虛擬網路的檔案。</span><span class="sxs-lookup"><span data-stu-id="d01c2-225">tooconnect tooa VNet using a Point-to-Site VPN, each client must install a client configuration package that configures hello native VPN client with hello settings and files that are necessary tooconnect toohello virtual network.</span></span> <span data-ttu-id="d01c2-226">hello VPN 用戶端組態封裝設定 hello 原生 Windows VPN 用戶端，它不會安裝新的或不同的 VPN 用戶端。</span><span class="sxs-lookup"><span data-stu-id="d01c2-226">hello VPN client configuration package configures hello native Windows VPN client, it doesn't install a new or different VPN client.</span></span> 

<span data-ttu-id="d01c2-227">只要 hello 版本符合 hello 用戶端 hello 架構，您可以使用相同的 VPN 用戶端組態封裝每個用戶端電腦，hello。</span><span class="sxs-lookup"><span data-stu-id="d01c2-227">You can use hello same VPN client configuration package on each client computer, as long as hello version matches hello architecture for hello client.</span></span> <span data-ttu-id="d01c2-228">Hello 清單中的用戶端作業系統支援，請參閱 hello[點對站連線常見問題集](#faq)hello 本文結尾處。</span><span class="sxs-lookup"><span data-stu-id="d01c2-228">For hello list of client operating systems that are supported, see hello [Point-to-Site connections FAQ](#faq) at hello end of this article.</span></span>

1. <span data-ttu-id="d01c2-229">建立 hello 閘道之後，您可以產生並下載 hello 用戶端組態封裝。</span><span class="sxs-lookup"><span data-stu-id="d01c2-229">After hello gateway has been created, you can generate and download hello client configuration package.</span></span> <span data-ttu-id="d01c2-230">這個範例會將 hello 套件下載 64 位元用戶端。</span><span class="sxs-lookup"><span data-stu-id="d01c2-230">This example downloads hello package for 64-bit clients.</span></span> <span data-ttu-id="d01c2-231">如果您想 toodownload hello 32 位元用戶端，請將 'Amd64' 取代 'x86'。</span><span class="sxs-lookup"><span data-stu-id="d01c2-231">If you want toodownload hello 32-bit client, replace 'Amd64' with 'x86'.</span></span> <span data-ttu-id="d01c2-232">您也可以使用 hello Azure 入口網站下載 hello VPN 用戶端。</span><span class="sxs-lookup"><span data-stu-id="d01c2-232">You can also download hello VPN client by using hello Azure portal.</span></span>

  ```powershell
  Get-AzureRmVpnClientPackage -ResourceGroupName $RG `
  -VirtualNetworkGatewayName $GWName -ProcessorArchitecture Amd64
  ```
2. <span data-ttu-id="d01c2-233">複製並貼上傳回 tooa web 瀏覽器 toodownload hello 套件，小心 tooremove hello 引號括住 hello 連結 hello 連結。</span><span class="sxs-lookup"><span data-stu-id="d01c2-233">Copy and paste hello link that is returned tooa web browser toodownload hello package, taking care tooremove hello quotes surrounding hello link.</span></span> 
3. <span data-ttu-id="d01c2-234">下載並安裝 hello 套件 hello 用戶端電腦上。</span><span class="sxs-lookup"><span data-stu-id="d01c2-234">Download and install hello package on hello client computer.</span></span> <span data-ttu-id="d01c2-235">如果您看到 SmartScreen 快顯視窗，請按一下 [更多資訊]，然後按一下 [仍要執行]。</span><span class="sxs-lookup"><span data-stu-id="d01c2-235">If you see a SmartScreen popup, click **More info**, then **Run anyway**.</span></span> <span data-ttu-id="d01c2-236">您也可以儲存 hello 封裝 tooinstall 其他用戶端電腦上。</span><span class="sxs-lookup"><span data-stu-id="d01c2-236">You can also save hello package tooinstall on other client computers.</span></span>
4. <span data-ttu-id="d01c2-237">Hello 用戶端電腦上，瀏覽過**網路設定**按一下**VPN**。</span><span class="sxs-lookup"><span data-stu-id="d01c2-237">On hello client computer, navigate too**Network Settings** and click **VPN**.</span></span> <span data-ttu-id="d01c2-238">hello VPN 連線會顯示 hello hello 連接到的虛擬網路名稱。</span><span class="sxs-lookup"><span data-stu-id="d01c2-238">hello VPN connection shows hello name of hello virtual network that it connects to.</span></span>

## <span data-ttu-id="d01c2-239"><a name="clientcertificate"></a>8.安裝匯出的用戶端憑證</span><span class="sxs-lookup"><span data-stu-id="d01c2-239"><a name="clientcertificate"></a>8. Install an exported client certificate</span></span>

<span data-ttu-id="d01c2-240">如果您想要 toocreate P2S 連線 hello 以外的用戶端電腦從您使用 toogenerate hello 用戶端憑證，您需要 tooinstall 用戶端憑證。</span><span class="sxs-lookup"><span data-stu-id="d01c2-240">If you want toocreate a P2S connection from a client computer other than hello one you used toogenerate hello client certificates, you need tooinstall a client certificate.</span></span> <span data-ttu-id="d01c2-241">安裝用戶端憑證，必須已建立 hello 用戶端憑證匯出時的 hello 密碼。</span><span class="sxs-lookup"><span data-stu-id="d01c2-241">When installing a client certificate, you need hello password that was created when hello client certificate was exported.</span></span> <span data-ttu-id="d01c2-242">一般而言，它是只需按兩下 hello 憑證並將其安裝。</span><span class="sxs-lookup"><span data-stu-id="d01c2-242">Typically, it is just a matter of double-clicking hello certificate and installing it.</span></span>

<span data-ttu-id="d01c2-243">請確定 hello 用戶端憑證匯出為.pfx 以及 hello 整個憑證鏈結 （這是 hello 預設值）。</span><span class="sxs-lookup"><span data-stu-id="d01c2-243">Make sure hello client certificate was exported as a .pfx along with hello entire certificate chain (which is hello default).</span></span> <span data-ttu-id="d01c2-244">否則 hello 根憑證資訊不存在 hello 用戶端電腦上，而且 hello 用戶端將不會無法 tooauthenticate 正確。</span><span class="sxs-lookup"><span data-stu-id="d01c2-244">Otherwise, hello root certificate information isn't present on hello client computer and hello client won't be able tooauthenticate properly.</span></span> <span data-ttu-id="d01c2-245">如需詳細資訊，請參閱[安裝匯出的用戶端憑證](vpn-gateway-certificates-point-to-site.md#install)。</span><span class="sxs-lookup"><span data-stu-id="d01c2-245">For more information, see [Install an exported client certificate](vpn-gateway-certificates-point-to-site.md#install).</span></span> 

## <span data-ttu-id="d01c2-246"><a name="connect"></a>9.連接 tooAzure</span><span class="sxs-lookup"><span data-stu-id="d01c2-246"><a name="connect"></a>9. Connect tooAzure</span></span>

1. <span data-ttu-id="d01c2-247">tooconnect tooyour VNet，hello 用戶端電腦上，瀏覽 tooVPN 連線，並尋找您所建立的 hello VPN 連線。</span><span class="sxs-lookup"><span data-stu-id="d01c2-247">tooconnect tooyour VNet, on hello client computer, navigate tooVPN connections and locate hello VPN connection that you created.</span></span> <span data-ttu-id="d01c2-248">它會命名為與虛擬網路名稱相同的 hello。</span><span class="sxs-lookup"><span data-stu-id="d01c2-248">It is named hello same name as your virtual network.</span></span> <span data-ttu-id="d01c2-249">按一下 [ **連接**]。</span><span class="sxs-lookup"><span data-stu-id="d01c2-249">Click **Connect**.</span></span> <span data-ttu-id="d01c2-250">快顯視窗訊息可能會出現參考 toousing hello 憑證。</span><span class="sxs-lookup"><span data-stu-id="d01c2-250">A pop-up message may appear that refers toousing hello certificate.</span></span> <span data-ttu-id="d01c2-251">按一下**繼續**toouse 提升的權限。</span><span class="sxs-lookup"><span data-stu-id="d01c2-251">Click **Continue** toouse elevated privileges.</span></span> 
2. <span data-ttu-id="d01c2-252">在 hello**連接**狀態] 頁面上，按一下 [**連接**toostart hello 連線。</span><span class="sxs-lookup"><span data-stu-id="d01c2-252">On hello **Connection** status page, click **Connect** toostart hello connection.</span></span> <span data-ttu-id="d01c2-253">如果您看到**選取憑證**畫面上，確認憑證顯示 hello 用戶端 hello 其中一個要 toouse tooconnect。</span><span class="sxs-lookup"><span data-stu-id="d01c2-253">If you see a **Select Certificate** screen, verify that hello client certificate showing is hello one that you want toouse tooconnect.</span></span> <span data-ttu-id="d01c2-254">如果不是，使用 hello 下拉箭號 tooselect hello 正確的憑證，，然後按一下**確定**。</span><span class="sxs-lookup"><span data-stu-id="d01c2-254">If it is not, use hello drop-down arrow tooselect hello correct certificate, and then click **OK**.</span></span>

  ![VPN 用戶端連線 tooAzure](./media/vpn-gateway-howto-point-to-site-rm-ps/clientconnect.png)
3. <span data-ttu-id="d01c2-256">已建立您的連線。</span><span class="sxs-lookup"><span data-stu-id="d01c2-256">Your connection is established.</span></span>

  ![連線已建立](./media/vpn-gateway-howto-point-to-site-rm-ps/connected.png)

#### <a name="troubleshooting-p2s-connections"></a><span data-ttu-id="d01c2-258">針對 P2S 連線進行疑難排解</span><span class="sxs-lookup"><span data-stu-id="d01c2-258">Troubleshooting P2S connections</span></span>

[!INCLUDE [client certificates](../../includes/vpn-gateway-certificates-verify-client-cert-include.md)]

## <span data-ttu-id="d01c2-259"><a name="verify"></a>10.確認您的連接</span><span class="sxs-lookup"><span data-stu-id="d01c2-259"><a name="verify"></a>10. Verify your connection</span></span>

1. <span data-ttu-id="d01c2-260">tooverify VPN 連線為作用中，開啟提升權限的命令提示字元並執行*ipconfig/all*。</span><span class="sxs-lookup"><span data-stu-id="d01c2-260">tooverify that your VPN connection is active, open an elevated command prompt, and run *ipconfig/all*.</span></span>
2. <span data-ttu-id="d01c2-261">檢視 hello 結果。</span><span class="sxs-lookup"><span data-stu-id="d01c2-261">View hello results.</span></span> <span data-ttu-id="d01c2-262">請注意，您收到 hello IP 位址的其中一個 hello 內 hello 點對站 VPN 用戶端位址集區，您在您的組態中指定的位址。</span><span class="sxs-lookup"><span data-stu-id="d01c2-262">Notice that hello IP address you received is one of hello addresses within hello Point-to-Site VPN Client Address Pool that you specified in your configuration.</span></span> <span data-ttu-id="d01c2-263">hello 結果會類似 toothis 範例：</span><span class="sxs-lookup"><span data-stu-id="d01c2-263">hello results are similar toothis example:</span></span>

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

## <span data-ttu-id="d01c2-264"><a name="connectVM"></a>Tooa 虛擬機器連線</span><span class="sxs-lookup"><span data-stu-id="d01c2-264"><a name="connectVM"></a>Connect tooa virtual machine</span></span>

[!INCLUDE [Connect tooa VM](../../includes/vpn-gateway-connect-vm-p2s-include.md)]

## <span data-ttu-id="d01c2-265"><a name="addremovecert"></a>新增或移除根憑證</span><span class="sxs-lookup"><span data-stu-id="d01c2-265"><a name="addremovecert"></a>Add or remove a root certificate</span></span>

<span data-ttu-id="d01c2-266">您可以從 Azure 新增和移除受信任的根憑證。</span><span class="sxs-lookup"><span data-stu-id="d01c2-266">You can add and remove trusted root certificates from Azure.</span></span> <span data-ttu-id="d01c2-267">當您移除的根憑證時，產生從 hello 根憑證的憑證的用戶端會無法進行驗證，且將無法能 tooconnect。</span><span class="sxs-lookup"><span data-stu-id="d01c2-267">When you remove a root certificate, clients that have a certificate generated from hello root certificate can't authenticate and won't be able tooconnect.</span></span> <span data-ttu-id="d01c2-268">如果您想用戶端 tooauthenticate 連接時，您會需要的 tooinstall 從受信任的 （上傳） tooAzure 的根憑證產生新的用戶端憑證。</span><span class="sxs-lookup"><span data-stu-id="d01c2-268">If you want a client tooauthenticate and connect, you need tooinstall a new client certificate generated from a root certificate that is trusted (uploaded) tooAzure.</span></span>

### <span data-ttu-id="d01c2-269"><a name="addtrustedroot"></a>tooadd 信任的根憑證</span><span class="sxs-lookup"><span data-stu-id="d01c2-269"><a name="addtrustedroot"></a>tooadd a trusted root certificate</span></span>

<span data-ttu-id="d01c2-270">您可以加總 too20 根憑證.cer 檔案 tooAzure。</span><span class="sxs-lookup"><span data-stu-id="d01c2-270">You can add up too20 root certificate .cer files tooAzure.</span></span> <span data-ttu-id="d01c2-271">hello 下列步驟可幫助您加入根憑證：</span><span class="sxs-lookup"><span data-stu-id="d01c2-271">hello following steps help you add a root certificate:</span></span>

#### <span data-ttu-id="d01c2-272"><a name="certmethod1"></a>方法 1</span><span class="sxs-lookup"><span data-stu-id="d01c2-272"><a name="certmethod1"></a>Method 1</span></span>

<span data-ttu-id="d01c2-273">這是最有效方法 tooupload hello 的根憑證。</span><span class="sxs-lookup"><span data-stu-id="d01c2-273">This is hello most efficient method tooupload a root certificate.</span></span>

1. <span data-ttu-id="d01c2-274">準備 hello.cer 檔案 tooupload:</span><span class="sxs-lookup"><span data-stu-id="d01c2-274">Prepare hello .cer file tooupload:</span></span>

  ```powershell
  $filePathForCert = "C:\cert\P2SRootCert3.cer"
  $cert = new-object System.Security.Cryptography.X509Certificates.X509Certificate2($filePathForCert)
  $CertBase64_3 = [system.convert]::ToBase64String($cert.RawData)
  $p2srootcert = New-AzureRmVpnClientRootCertificate -Name $P2SRootCertName -PublicCertData $CertBase64_3
  ```
2. <span data-ttu-id="d01c2-275">Hello 檔案上傳。</span><span class="sxs-lookup"><span data-stu-id="d01c2-275">Upload hello file.</span></span> <span data-ttu-id="d01c2-276">您一次只能上傳一個檔案。</span><span class="sxs-lookup"><span data-stu-id="d01c2-276">You can only upload one file at a time.</span></span>

  ```powershell
  Add-AzureRmVpnClientRootCertificate -VpnClientRootCertificateName $P2SRootCertName -VirtualNetworkGatewayname "VNet1GW" -ResourceGroupName "TestRG" -PublicCertData $CertBase64_3
  ```

3. <span data-ttu-id="d01c2-277">hello 憑證檔案上傳的 tooverify:</span><span class="sxs-lookup"><span data-stu-id="d01c2-277">tooverify that hello certificate file uploaded:</span></span>

  ```powershell
  Get-AzureRmVpnClientRootCertificate -ResourceGroupName "TestRG" `
  -VirtualNetworkGatewayName "VNet1GW"
  ```

#### <span data-ttu-id="d01c2-278"><a name="certmethod2"></a>方法 2</span><span class="sxs-lookup"><span data-stu-id="d01c2-278"><a name="certmethod2"></a>Method 2</span></span>

<span data-ttu-id="d01c2-279">這個方法會比方法 1 的詳細步驟，但有 hello 相同的結果。</span><span class="sxs-lookup"><span data-stu-id="d01c2-279">This method is has more steps than Method 1, but has hello same result.</span></span> <span data-ttu-id="d01c2-280">它是為了，以防您需要 tooview hello 憑證資料。</span><span class="sxs-lookup"><span data-stu-id="d01c2-280">It is included in case you need tooview hello certificate data.</span></span>

1. <span data-ttu-id="d01c2-281">建立並準備 hello 新的根憑證 tooadd tooAzure。</span><span class="sxs-lookup"><span data-stu-id="d01c2-281">Create and prepare hello new root certificate tooadd tooAzure.</span></span> <span data-ttu-id="d01c2-282">Hello 公開金鑰匯出成 base-64 編碼 X.509 (。CER) 和以文字編輯器中開啟它。</span><span class="sxs-lookup"><span data-stu-id="d01c2-282">Export hello public key as a Base-64 encoded X.509 (.CER) and open it with a text editor.</span></span> <span data-ttu-id="d01c2-283">請複製 hello 值 hello 下列範例所示：</span><span class="sxs-lookup"><span data-stu-id="d01c2-283">Copy hello values, as shown in hello following example:</span></span>

  ![憑證](./media/vpn-gateway-howto-point-to-site-rm-ps/copycert.png)

  > [!NOTE]
  > <span data-ttu-id="d01c2-285">複製 hello 憑證資料時，請確認您已複製的 hello 文字做為一個連續的一行，而不換行字元或換。</span><span class="sxs-lookup"><span data-stu-id="d01c2-285">When copying hello certificate data, make sure that you copy hello text as one continuous line without carriage returns or line feeds.</span></span> <span data-ttu-id="d01c2-286">您可能需要 toomodify 您 hello 文字編輯器 too'Show 符號/顯示所有字元 toosee hello 歸位字元傳回和行摘要中的檢視。</span><span class="sxs-lookup"><span data-stu-id="d01c2-286">You may need toomodify your view in hello text editor too'Show Symbol/Show all characters' toosee hello carriage returns and line feeds.</span></span>
  >
  >

2. <span data-ttu-id="d01c2-287">為變數指定 hello 憑證名稱和金鑰資訊。</span><span class="sxs-lookup"><span data-stu-id="d01c2-287">Specify hello certificate name and key information as a variable.</span></span> <span data-ttu-id="d01c2-288">取代您自己 hello 所示的下列範例中的 hello 資訊：</span><span class="sxs-lookup"><span data-stu-id="d01c2-288">Replace hello information with your own, as shown in hello following example:</span></span>

  ```powershell
  $P2SRootCertName2 = "ARMP2SRootCert2.cer"
  $MyP2SCertPubKeyBase64_2 = "MIIC/zCCAeugAwIBAgIQKazxzFjMkp9JRiX+tkTfSzAJBgUrDgMCHQUAMBgxFjAUBgNVBAMTDU15UDJTUm9vdENlcnQwHhcNMTUxMjE5MDI1MTIxWhcNMzkxMjMxMjM1OTU5WjAYMRYwFAYDVQQDEw1NeVAyU1Jvb3RDZXJ0MIIBIjANBgkqhkiG9w0BAQEFAAOCAQ8AMIIBCgKCAQEAyjIXoWy8xE/GF1OSIvUaA0bxBjZ1PJfcXkMWsHPzvhWc2esOKrVQtgFgDz4ggAnOUFEkFaszjiHdnXv3mjzE2SpmAVIZPf2/yPWqkoHwkmrp6BpOvNVOpKxaGPOuK8+dql1xcL0eCkt69g4lxy0FGRFkBcSIgVTViS9wjuuS7LPo5+OXgyFkAY3pSDiMzQCkRGNFgw5WGMHRDAiruDQF1ciLNojAQCsDdLnI3pDYsvRW73HZEhmOqRRnJQe6VekvBYKLvnKaxUTKhFIYwuymHBB96nMFdRUKCZIiWRIy8Hc8+sQEsAML2EItAjQv4+fqgYiFdSWqnQCPf/7IZbotgQIDAQABo00wSzBJBgNVHQEEQjBAgBAkuVrWvFsCJAdK5pb/eoCNoRowGDEWMBQGA1UEAxMNTXlQMlNSb290Q2VydIIQKazxzFjMkp9JRiX+tkTfSzAJBgUrDgMCHQUAA4IBAQA223veAZEIar9N12ubNH2+HwZASNzDVNqspkPKD97TXfKHlPlIcS43TaYkTz38eVrwI6E0yDk4jAuPaKnPuPYFRj9w540SvY6PdOUwDoEqpIcAVp+b4VYwxPL6oyEQ8wnOYuoAK1hhh20lCbo8h9mMy9ofU+RP6HJ7lTqupLfXdID/XevI8tW6Dm+C/wCeV3EmIlO9KUoblD/e24zlo3YzOtbyXwTIh34T0fO/zQvUuBqZMcIPfM1cDvqcqiEFLWvWKoAnxbzckye2uk1gHO52d8AVL3mGiX8wBJkjc/pMdxrEvvCzJkltBmqxTM6XjDJALuVh16qFlqgTWCIcb7ju"
  ```
3. <span data-ttu-id="d01c2-289">新增 hello 新的根憑證。</span><span class="sxs-lookup"><span data-stu-id="d01c2-289">Add hello new root certificate.</span></span> <span data-ttu-id="d01c2-290">您一次只能新增一個憑證。</span><span class="sxs-lookup"><span data-stu-id="d01c2-290">You can only add one certificate at a time.</span></span>

  ```powershell
  Add-AzureRmVpnClientRootCertificate -VpnClientRootCertificateName $P2SRootCertName2 -VirtualNetworkGatewayname "VNet1GW" -ResourceGroupName "TestRG" -PublicCertData $MyP2SCertPubKeyBase64_2
  ```
4. <span data-ttu-id="d01c2-291">您可以確認使用下列範例中的 hello 已正確新增該 hello 新憑證：</span><span class="sxs-lookup"><span data-stu-id="d01c2-291">You can verify that hello new certificate was added correctly by using hello following example:</span></span>

  ```powershell
  Get-AzureRmVpnClientRootCertificate -ResourceGroupName "TestRG" `
  -VirtualNetworkGatewayName "VNet1GW"
  ```

### <span data-ttu-id="d01c2-292"><a name="removerootcert"></a>tooremove 根憑證</span><span class="sxs-lookup"><span data-stu-id="d01c2-292"><a name="removerootcert"></a>tooremove a root certificate</span></span>

1. <span data-ttu-id="d01c2-293">Hello 變數宣告。</span><span class="sxs-lookup"><span data-stu-id="d01c2-293">Declare hello variables.</span></span>

  ```powershell
  $GWName = "Name_of_virtual_network_gateway"
  $RG = "Name_of_resource_group"
  $P2SRootCertName2 = "ARMP2SRootCert2.cer"
  $MyP2SCertPubKeyBase64_2 = "MIIC/zCCAeugAwIBAgIQKazxzFjMkp9JRiX+tkTfSzAJBgUrDgMCHQUAMBgxFjAUBgNVBAMTDU15UDJTUm9vdENlcnQwHhcNMTUxMjE5MDI1MTIxWhcNMzkxMjMxMjM1OTU5WjAYMRYwFAYDVQQDEw1NeVAyU1Jvb3RDZXJ0MIIBIjANBgkqhkiG9w0BAQEFAAOCAQ8AMIIBCgKCAQEAyjIXoWy8xE/GF1OSIvUaA0bxBjZ1PJfcXkMWsHPzvhWc2esOKrVQtgFgDz4ggAnOUFEkFaszjiHdnXv3mjzE2SpmAVIZPf2/yPWqkoHwkmrp6BpOvNVOpKxaGPOuK8+dql1xcL0eCkt69g4lxy0FGRFkBcSIgVTViS9wjuuS7LPo5+OXgyFkAY3pSDiMzQCkRGNFgw5WGMHRDAiruDQF1ciLNojAQCsDdLnI3pDYsvRW73HZEhmOqRRnJQe6VekvBYKLvnKaxUTKhFIYwuymHBB96nMFdRUKCZIiWRIy8Hc8+sQEsAML2EItAjQv4+fqgYiFdSWqnQCPf/7IZbotgQIDAQABo00wSzBJBgNVHQEEQjBAgBAkuVrWvFsCJAdK5pb/eoCNoRowGDEWMBQGA1UEAxMNTXlQMlNSb290Q2VydIIQKazxzFjMkp9JRiX+tkTfSzAJBgUrDgMCHQUAA4IBAQA223veAZEIar9N12ubNH2+HwZASNzDVNqspkPKD97TXfKHlPlIcS43TaYkTz38eVrwI6E0yDk4jAuPaKnPuPYFRj9w540SvY6PdOUwDoEqpIcAVp+b4VYwxPL6oyEQ8wnOYuoAK1hhh20lCbo8h9mMy9ofU+RP6HJ7lTqupLfXdID/XevI8tW6Dm+C/wCeV3EmIlO9KUoblD/e24zlo3YzOtbyXwTIh34T0fO/zQvUuBqZMcIPfM1cDvqcqiEFLWvWKoAnxbzckye2uk1gHO52d8AVL3mGiX8wBJkjc/pMdxrEvvCzJkltBmqxTM6XjDJALuVh16qFlqgTWCIcb7ju"
  ```
2. <span data-ttu-id="d01c2-294">移除 hello 憑證。</span><span class="sxs-lookup"><span data-stu-id="d01c2-294">Remove hello certificate.</span></span>

  ```powershell
  Remove-AzureRmVpnClientRootCertificate -VpnClientRootCertificateName $P2SRootCertName2 -VirtualNetworkGatewayName $GWName -ResourceGroupName $RG -PublicCertData $MyP2SCertPubKeyBase64_2
  ```
3. <span data-ttu-id="d01c2-295">已成功移除下列 hello 憑證的範例 tooverify 使用 hello。</span><span class="sxs-lookup"><span data-stu-id="d01c2-295">Use hello following example tooverify that hello certificate was removed successfully.</span></span>

  ```powershell
  Get-AzureRmVpnClientRootCertificate -ResourceGroupName "TestRG" `
  -VirtualNetworkGatewayName "VNet1GW"
  ```

## <span data-ttu-id="d01c2-296"><a name="revoke"></a>撤銷用戶端憑證</span><span class="sxs-lookup"><span data-stu-id="d01c2-296"><a name="revoke"></a>Revoke a client certificate</span></span>

<span data-ttu-id="d01c2-297">您可以撤銷用戶端憑證。</span><span class="sxs-lookup"><span data-stu-id="d01c2-297">You can revoke client certificates.</span></span> <span data-ttu-id="d01c2-298">hello 憑證撤銷清單可讓您 tooselectively 拒絕個別用戶端憑證為基礎的點對站連線。</span><span class="sxs-lookup"><span data-stu-id="d01c2-298">hello certificate revocation list allows you tooselectively deny Point-to-Site connectivity based on individual client certificates.</span></span> <span data-ttu-id="d01c2-299">這與移除受信任的根憑證不同。</span><span class="sxs-lookup"><span data-stu-id="d01c2-299">This is different than removing a trusted root certificate.</span></span> <span data-ttu-id="d01c2-300">如果您從 Azure 移除受信任的根憑證.cer，它就會撤銷所有用戶端憑證產生/簽署由 hello 撤銷的根憑證的 hello 存取權。</span><span class="sxs-lookup"><span data-stu-id="d01c2-300">If you remove a trusted root certificate .cer from Azure, it revokes hello access for all client certificates generated/signed by hello revoked root certificate.</span></span> <span data-ttu-id="d01c2-301">撤銷用戶端憑證，而不是 hello 根憑證，可讓 hello 產生從 hello 根憑證 toocontinue toobe 用來驗證其他憑證。</span><span class="sxs-lookup"><span data-stu-id="d01c2-301">Revoking a client certificate, rather than hello root certificate, allows hello other certificates that were generated from hello root certificate toocontinue toobe used for authentication.</span></span>

<span data-ttu-id="d01c2-302">hello 常見的作法是 toouse hello 根憑證 toomanage 存取小組或組織層級時使用已撤銷用戶端憑證來進行個別使用者的更細緻的存取控制。</span><span class="sxs-lookup"><span data-stu-id="d01c2-302">hello common practice is toouse hello root certificate toomanage access at team or organization levels, while using revoked client certificates for fine-grained access control on individual users.</span></span>

### <span data-ttu-id="d01c2-303"><a name="revokeclientcert"></a>toorevoke 用戶端憑證</span><span class="sxs-lookup"><span data-stu-id="d01c2-303"><a name="revokeclientcert"></a>toorevoke a client certificate</span></span>

1. <span data-ttu-id="d01c2-304">擷取 hello 用戶端憑證指紋。</span><span class="sxs-lookup"><span data-stu-id="d01c2-304">Retrieve hello client certificate thumbprint.</span></span> <span data-ttu-id="d01c2-305">如需詳細資訊，請參閱[tooretrieve 如何 hello 憑證的指紋](https://msdn.microsoft.com/library/ms734695.aspx)。</span><span class="sxs-lookup"><span data-stu-id="d01c2-305">For more information, see [How tooretrieve hello Thumbprint of a Certificate](https://msdn.microsoft.com/library/ms734695.aspx).</span></span>
2. <span data-ttu-id="d01c2-306">複製 hello 資訊 tooa 文字編輯器，並移除所有的空間，使其連續的字串。</span><span class="sxs-lookup"><span data-stu-id="d01c2-306">Copy hello information tooa text editor and remove all spaces so that it is a continuous string.</span></span> <span data-ttu-id="d01c2-307">這個字串 hello 下一個步驟中宣告的變數。</span><span class="sxs-lookup"><span data-stu-id="d01c2-307">This string is declared as a variable in hello next step.</span></span>
3. <span data-ttu-id="d01c2-308">Hello 變數宣告。</span><span class="sxs-lookup"><span data-stu-id="d01c2-308">Declare hello variables.</span></span> <span data-ttu-id="d01c2-309">Hello 上一個步驟中，請確定您所擷取的 toodeclare hello 憑證指紋。</span><span class="sxs-lookup"><span data-stu-id="d01c2-309">Make sure toodeclare hello thumbprint you retrieved in hello previous step.</span></span>

  ```powershell
  $RevokedClientCert1 = "NameofCertificate"
  $RevokedThumbprint1 = "‎51ab1edd8da4cfed77e20061c5eb6d2ef2f778c7"
  $GWName = "Name_of_virtual_network_gateway"
  $RG = "Name_of_resource_group"
  ```
4. <span data-ttu-id="d01c2-310">新增 hello 撤銷憑證的指紋 toohello 清單。</span><span class="sxs-lookup"><span data-stu-id="d01c2-310">Add hello thumbprint toohello list of revoked certificates.</span></span> <span data-ttu-id="d01c2-311">已加入 hello 指紋時，您會看到 「 成功 」。</span><span class="sxs-lookup"><span data-stu-id="d01c2-311">You see "Succeeded" when hello thumbprint has been added.</span></span>

  ```powershell
  Add-AzureRmVpnClientRevokedCertificate -VpnClientRevokedCertificateName $RevokedClientCert1 `
  -VirtualNetworkGatewayName $GWName -ResourceGroupName $RG `
  -Thumbprint $RevokedThumbprint1
  ```
5. <span data-ttu-id="d01c2-312">請確認該 hello 指紋已加入 toohello 憑證撤銷清單。</span><span class="sxs-lookup"><span data-stu-id="d01c2-312">Verify that hello thumbprint was added toohello certificate revocation list.</span></span>

  ```powershell
  Get-AzureRmVpnClientRevokedCertificate -VirtualNetworkGatewayName $GWName -ResourceGroupName $RG
  ```
6. <span data-ttu-id="d01c2-313">加入 hello 指紋之後，hello 憑證不再可以使用的 tooconnect。</span><span class="sxs-lookup"><span data-stu-id="d01c2-313">After hello thumbprint has been added, hello certificate can no longer be used tooconnect.</span></span> <span data-ttu-id="d01c2-314">使用此憑證的 tooconnect 再試一次的用戶端收到訊息，指出該 hello 憑證不再有效。</span><span class="sxs-lookup"><span data-stu-id="d01c2-314">Clients that try tooconnect using this certificate receive a message saying that hello certificate is no longer valid.</span></span>

### <span data-ttu-id="d01c2-315"><a name="reinstateclientcert"></a>tooreinstate 用戶端憑證</span><span class="sxs-lookup"><span data-stu-id="d01c2-315"><a name="reinstateclientcert"></a>tooreinstate a client certificate</span></span>

<span data-ttu-id="d01c2-316">您可以從已撤銷用戶端憑證的 hello 清單移除 hello 指紋恢復用戶端憑證。</span><span class="sxs-lookup"><span data-stu-id="d01c2-316">You can reinstate a client certificate by removing hello thumbprint from hello list of revoked client certificates.</span></span>

1. <span data-ttu-id="d01c2-317">Hello 變數宣告。</span><span class="sxs-lookup"><span data-stu-id="d01c2-317">Declare hello variables.</span></span> <span data-ttu-id="d01c2-318">請確定您宣告 hello 正確的 tooreinstate hello 憑證指紋。</span><span class="sxs-lookup"><span data-stu-id="d01c2-318">Make sure you declare hello correct thumbprint for hello certificate that you want tooreinstate.</span></span>

  ```powershell
  $RevokedClientCert1 = "NameofCertificate"
  $RevokedThumbprint1 = "‎51ab1edd8da4cfed77e20061c5eb6d2ef2f778c7"
  $GWName = "Name_of_virtual_network_gateway"
  $RG = "Name_of_resource_group"
  ```
2. <span data-ttu-id="d01c2-319">移除 hello 憑證撤銷清單中的 hello 憑證指紋。</span><span class="sxs-lookup"><span data-stu-id="d01c2-319">Remove hello certificate thumbprint from hello certificate revocation list.</span></span>

  ```powershell
  Remove-AzureRmVpnClientRevokedCertificate -VpnClientRevokedCertificateName $RevokedClientCert1 `
  -VirtualNetworkGatewayName $GWName -ResourceGroupName $RG -Thumbprint $RevokedThumbprint1
  ```
3. <span data-ttu-id="d01c2-320">如果從 hello 移除 hello 指紋的核取撤銷清單。</span><span class="sxs-lookup"><span data-stu-id="d01c2-320">Check if hello thumbprint is removed from hello revoked list.</span></span>

  ```powershell
  Get-AzureRmVpnClientRevokedCertificate -VirtualNetworkGatewayName $GWName -ResourceGroupName $RG
  ```

## <span data-ttu-id="d01c2-321"><a name="faq"></a>點對站常見問題集</span><span class="sxs-lookup"><span data-stu-id="d01c2-321"><a name="faq"></a>Point-to-Site FAQ</span></span>

[!INCLUDE [Point-to-Site FAQ](../../includes/vpn-gateway-point-to-site-faq-include.md)]

## <a name="next-steps"></a><span data-ttu-id="d01c2-322">後續步驟</span><span class="sxs-lookup"><span data-stu-id="d01c2-322">Next steps</span></span>
<span data-ttu-id="d01c2-323">一旦完成您的連線，您可以將虛擬機器 tooyour 虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="d01c2-323">Once your connection is complete, you can add virtual machines tooyour virtual networks.</span></span> <span data-ttu-id="d01c2-324">如需詳細資訊，請參閱[虛擬機器](https://docs.microsoft.com/azure/#pivot=services&panel=Compute)。</span><span class="sxs-lookup"><span data-stu-id="d01c2-324">For more information, see [Virtual Machines](https://docs.microsoft.com/azure/#pivot=services&panel=Compute).</span></span> <span data-ttu-id="d01c2-325">toounderstand 深入了解網路和虛擬機器，請參閱[Azure 與 Linux VM 網路概觀](../virtual-machines/linux/azure-vm-network-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="d01c2-325">toounderstand more about networking and virtual machines, see [Azure and Linux VM network overview](../virtual-machines/linux/azure-vm-network-overview.md).</span></span>
