---
title: "連接電腦 tooa 虛擬網路使用點對站台和憑證驗證： Azure 入口網站 |Microsoft 文件"
description: "安全地連接 Azure 虛擬網路的電腦 tooyour 藉由建立點對站 VPN 閘道連線使用憑證驗證。 本文適用於 toohello Resource Manager 部署模型，並使用 hello Azure 入口網站。"
services: vpn-gateway
documentationcenter: na
author: cherylmc
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: a15ad327-e236-461f-a18e-6dbedbf74943
ms.service: vpn-gateway
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/10/2017
ms.author: cherylmc
ms.openlocfilehash: 1419d6b4c160140b62d656b25bd02f6af7fd6655
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="configure-a-point-to-site-connection-tooa-vnet-using-certificate-authentication-azure-portal"></a><span data-ttu-id="cee38-104">設定點對站連線 tooa VNet 使用憑證驗證： Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="cee38-104">Configure a Point-to-Site connection tooa VNet using certificate authentication: Azure portal</span></span>

<span data-ttu-id="cee38-105">本文章將示範如何在 hello 資源管理員部署模型中使用的點對站連接的 VNet toocreate hello Azure 入口網站。</span><span class="sxs-lookup"><span data-stu-id="cee38-105">This article shows you how toocreate a VNet with a Point-to-Site connection in hello Resource Manager deployment model using hello Azure portal.</span></span> <span data-ttu-id="cee38-106">此組態會使用用戶端連接的憑證 tooauthenticate hello。</span><span class="sxs-lookup"><span data-stu-id="cee38-106">This configuration uses certificates tooauthenticate hello connecting client.</span></span> <span data-ttu-id="cee38-107">您也可以建立此組態使用不同的部署工具或部署模型，從下列清單中的 hello 選取不同的選項：</span><span class="sxs-lookup"><span data-stu-id="cee38-107">You can also create this configuration using a different deployment tool or deployment model by selecting a different option from hello following list:</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="cee38-108">Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="cee38-108">Azure portal</span></span>](vpn-gateway-howto-point-to-site-resource-manager-portal.md)
> * [<span data-ttu-id="cee38-109">PowerShell</span><span class="sxs-lookup"><span data-stu-id="cee38-109">PowerShell</span></span>](vpn-gateway-howto-point-to-site-rm-ps.md)
> * [<span data-ttu-id="cee38-110">Azure 入口網站 (傳統)</span><span class="sxs-lookup"><span data-stu-id="cee38-110">Azure portal (classic)</span></span>](vpn-gateway-howto-point-to-site-classic-azure-portal.md)
>
>

<span data-ttu-id="cee38-111">點對站 (P2S) VPN 閘道，可讓您建立從個別的用戶端電腦的安全連線 tooyour 虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="cee38-111">A Point-to-Site (P2S) VPN gateway lets you create a secure connection tooyour virtual network from an individual client computer.</span></span> <span data-ttu-id="cee38-112">當您想要 tooconnect tooyour 從遠端位置，例如當您從家裡或會議 telecommuting VNet，點對站 VPN 連線會很有用。</span><span class="sxs-lookup"><span data-stu-id="cee38-112">Point-to-Site VPN connections are useful when you want tooconnect tooyour VNet from a remote location, such when you are telecommuting from home or a conference.</span></span> <span data-ttu-id="cee38-113">您有只有少數的用戶端需要 tooconnect tooa VNet 時 P2S VPN 也很有用的方案 toouse，而不是站對站 VPN。</span><span class="sxs-lookup"><span data-stu-id="cee38-113">A P2S VPN is also a useful solution toouse instead of a Site-to-Site VPN when you have only a few clients that need tooconnect tooa VNet.</span></span> 

<span data-ttu-id="cee38-114">使用 P2S hello 安全通訊端通道通訊協定 (SSTP)，這是 SSL 型 VPN 通訊協定。</span><span class="sxs-lookup"><span data-stu-id="cee38-114">P2S uses hello Secure Socket Tunneling Protocol (SSTP), which is an SSL-based VPN protocol.</span></span> <span data-ttu-id="cee38-115">建立之 P2S VPN 連線從 hello 用戶端電腦。</span><span class="sxs-lookup"><span data-stu-id="cee38-115">A P2S VPN connection is established by starting it from hello client computer.</span></span>

![Point-to-Site-diagram](./media/vpn-gateway-howto-point-to-site-resource-manager-portal/point-to-site-connection-diagram.png)

<span data-ttu-id="cee38-117">點對站憑證驗證的連接需要 hello 下列：</span><span class="sxs-lookup"><span data-stu-id="cee38-117">Point-to-Site certificate authentication connections require hello following:</span></span>

* <span data-ttu-id="cee38-118">RouteBased VPN 閘道。</span><span class="sxs-lookup"><span data-stu-id="cee38-118">A RouteBased VPN gateway.</span></span>
* <span data-ttu-id="cee38-119">hello 公開金鑰 （.cer 檔案） 的根憑證，也就是上傳的 tooAzure。</span><span class="sxs-lookup"><span data-stu-id="cee38-119">hello public key (.cer file) for a root certificate, which is uploaded tooAzure.</span></span> <span data-ttu-id="cee38-120">一旦上傳 hello 憑證時，它會被視為受信任的憑證，並用於驗證。</span><span class="sxs-lookup"><span data-stu-id="cee38-120">Once hello certificate is uploaded, it is considered a trusted certificate and is used for authentication.</span></span>
* <span data-ttu-id="cee38-121">會產生從 hello 根憑證，並將連接 toohello VNet 每部用戶端電腦上安裝用戶端憑證。</span><span class="sxs-lookup"><span data-stu-id="cee38-121">A client certificate that is generated from hello root certificate and installed on each client computer that will connect toohello VNet.</span></span> <span data-ttu-id="cee38-122">此憑證使用於用戶端憑證。</span><span class="sxs-lookup"><span data-stu-id="cee38-122">This certificate is used for client authentication.</span></span>
* <span data-ttu-id="cee38-123">VPN 用戶端組態套件。</span><span class="sxs-lookup"><span data-stu-id="cee38-123">A VPN client configuration package.</span></span> <span data-ttu-id="cee38-124">hello VPN 用戶端組態封裝包含 hello 的 hello 用戶端 tooconnect toohello VNet 的必要資訊。</span><span class="sxs-lookup"><span data-stu-id="cee38-124">hello VPN client configuration package contains hello necessary information for hello client tooconnect toohello VNet.</span></span> <span data-ttu-id="cee38-125">hello 封裝設定 hello 現有 VPN 用戶端是原生 toohello Windows 作業系統。</span><span class="sxs-lookup"><span data-stu-id="cee38-125">hello package configures hello existing VPN client that is native toohello Windows operating system.</span></span> <span data-ttu-id="cee38-126">每個連接的用戶端必須使用 hello 組態封裝設定。</span><span class="sxs-lookup"><span data-stu-id="cee38-126">Each client that connects must be configured using hello configuration package.</span></span>

<span data-ttu-id="cee38-127">點對站連線不需要 VPN 裝置或內部部署公眾對應 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="cee38-127">Point-to-Site connections do not require a VPN device or an on-premises public-facing IP address.</span></span> <span data-ttu-id="cee38-128">hello VPN 連線建立透過 SSTP （安全通訊端通道通訊協定）。</span><span class="sxs-lookup"><span data-stu-id="cee38-128">hello VPN connection is created over SSTP (Secure Socket Tunneling Protocol).</span></span> <span data-ttu-id="cee38-129">在 hello 伺服器端，我們支援 SSTP 版本 1.0、 1.1 和 1.2。</span><span class="sxs-lookup"><span data-stu-id="cee38-129">On hello server side, we support SSTP versions 1.0, 1.1, and 1.2.</span></span> <span data-ttu-id="cee38-130">hello 用戶端決定哪一個版本 toouse。</span><span class="sxs-lookup"><span data-stu-id="cee38-130">hello client decides which version toouse.</span></span> <span data-ttu-id="cee38-131">若為 Windows 8.1 和更新版本，SSTP 預設使用 1.2。</span><span class="sxs-lookup"><span data-stu-id="cee38-131">For Windows 8.1 and above, SSTP uses 1.2 by default.</span></span>

<span data-ttu-id="cee38-132">如需有關點對站連線的詳細資訊，請參閱 hello[點對站常見問題集](#faq)hello 本文結尾處。</span><span class="sxs-lookup"><span data-stu-id="cee38-132">For more information about Point-to-Site connections, see hello [Point-to-Site FAQ](#faq) at hello end of this article.</span></span>

#### <span data-ttu-id="cee38-133"><a name="example"></a>範例值</span><span class="sxs-lookup"><span data-stu-id="cee38-133"><a name="example"></a>Example values</span></span>

<span data-ttu-id="cee38-134">您可以使用下列值 toocreate 測試環境的 hello 或 toothese 值，請參閱 toobetter 了解這篇文章中的 hello 範例：</span><span class="sxs-lookup"><span data-stu-id="cee38-134">You can use hello following values toocreate a test environment, or refer toothese values toobetter understand hello examples in this article:</span></span>

* <span data-ttu-id="cee38-135">**VNet 名稱︰**VNet1</span><span class="sxs-lookup"><span data-stu-id="cee38-135">**VNet Name:** VNet1</span></span>
* <span data-ttu-id="cee38-136">**位址空間：**192.168.0.0/16</span><span class="sxs-lookup"><span data-stu-id="cee38-136">**Address space:** 192.168.0.0/16</span></span><br><span data-ttu-id="cee38-137">在此範例中，我們只使用一個位址空間。</span><span class="sxs-lookup"><span data-stu-id="cee38-137">For this example, we use only one address space.</span></span> <span data-ttu-id="cee38-138">您可以針對 VNet 使用一個以上的位址空間。</span><span class="sxs-lookup"><span data-stu-id="cee38-138">You can have more than one address space for your VNet.</span></span>
* <span data-ttu-id="cee38-139">**子網路名稱：**FrontEnd</span><span class="sxs-lookup"><span data-stu-id="cee38-139">**Subnet name:** FrontEnd</span></span>
* <span data-ttu-id="cee38-140">**子網路位址範圍：**192.168.1.0/24</span><span class="sxs-lookup"><span data-stu-id="cee38-140">**Subnet address range:** 192.168.1.0/24</span></span>
* <span data-ttu-id="cee38-141">**訂用帳戶：**如果您有多個訂用帳戶，確認您是否使用 hello 正確。</span><span class="sxs-lookup"><span data-stu-id="cee38-141">**Subscription:** If you have more than one subscription, verify that you are using hello correct one.</span></span>
* <span data-ttu-id="cee38-142">**資源群組：**TestRG</span><span class="sxs-lookup"><span data-stu-id="cee38-142">**Resource Group:** TestRG</span></span>
* <span data-ttu-id="cee38-143">**位置：**美國東部</span><span class="sxs-lookup"><span data-stu-id="cee38-143">**Location:** East US</span></span>
* <span data-ttu-id="cee38-144">**GatewaySubnet：**192.168.200.0/24</span><span class="sxs-lookup"><span data-stu-id="cee38-144">**GatewaySubnet:** 192.168.200.0/24</span></span><br>
* <span data-ttu-id="cee38-145">**DNS 伺服器：** （選擇性） hello toouse 需名稱解析的 DNS 伺服器的 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="cee38-145">**DNS Server:** (optional) IP address of hello DNS server that you want toouse for name resolution.</span></span>
* <span data-ttu-id="cee38-146">**虛擬網路閘道名稱：**VNet1GW</span><span class="sxs-lookup"><span data-stu-id="cee38-146">**Virtual network gateway name:** VNet1GW</span></span>
* <span data-ttu-id="cee38-147">**閘道類型：**VPN</span><span class="sxs-lookup"><span data-stu-id="cee38-147">**Gateway type:** VPN</span></span>
* <span data-ttu-id="cee38-148">**VPN 類型：**路由式</span><span class="sxs-lookup"><span data-stu-id="cee38-148">**VPN type:** Route-based</span></span>
* <span data-ttu-id="cee38-149">**公用 IP 位址名稱：**VNet1GWpip</span><span class="sxs-lookup"><span data-stu-id="cee38-149">**Public IP address name:** VNet1GWpip</span></span>
* <span data-ttu-id="cee38-150">**連線類型：**點對站</span><span class="sxs-lookup"><span data-stu-id="cee38-150">**Connection type:** Point-to-site</span></span>
* <span data-ttu-id="cee38-151">**用戶端位址集區：**172.16.201.0/24</span><span class="sxs-lookup"><span data-stu-id="cee38-151">**Client address pool:** 172.16.201.0/24</span></span><br><span data-ttu-id="cee38-152">連接 toohello VNet 使用這個點對站連線的 VPN 用戶端收到 hello 用戶端位址集區的 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="cee38-152">VPN clients that connect toohello VNet using this Point-to-Site connection receive an IP address from hello client address pool.</span></span>

## <span data-ttu-id="cee38-153"><a name="createvnet"></a>1.建立虛擬網路</span><span class="sxs-lookup"><span data-stu-id="cee38-153"><a name="createvnet"></a>1. Create a virtual network</span></span>

<span data-ttu-id="cee38-154">在開始之前，請確認您有 Azure 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="cee38-154">Before beginning, verify that you have an Azure subscription.</span></span> <span data-ttu-id="cee38-155">如果您還沒有 Azure 訂用帳戶，則可以啟用 [MSDN 訂戶權益](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details)或註冊[免費帳戶](https://azure.microsoft.com/pricing/free-trial)。</span><span class="sxs-lookup"><span data-stu-id="cee38-155">If you don't already have an Azure subscription, you can activate your [MSDN subscriber benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details) or sign up for a [free account](https://azure.microsoft.com/pricing/free-trial).</span></span>

[!INCLUDE [Basic Point-to-Site VNet](../../includes/vpn-gateway-basic-p2s-vnet-rm-portal-include.md)]

## <span data-ttu-id="cee38-156"><a name="gatewaysubnet"></a>2.新增閘道子網路</span><span class="sxs-lookup"><span data-stu-id="cee38-156"><a name="gatewaysubnet"></a>2. Add a gateway subnet</span></span>

<span data-ttu-id="cee38-157">連接您的虛擬網路 tooa 閘道之前，您首先需要 toocreate hello 閘道子網路要為 hello 虛擬網路 toowhich tooconnect。</span><span class="sxs-lookup"><span data-stu-id="cee38-157">Before connecting your virtual network tooa gateway, you first need toocreate hello gateway subnet for hello virtual network toowhich you want tooconnect.</span></span> <span data-ttu-id="cee38-158">hello 閘道服務會使用 hello hello 閘道子網路中指定的 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="cee38-158">hello gateway services use hello IP addresses specified in hello gateway subnet.</span></span> <span data-ttu-id="cee38-159">可能的話，請建立閘道子網路使用 CIDR 區塊/28 或 /27 tooprovide 足夠的 IP 位址 tooaccommodate 額外設定需求。</span><span class="sxs-lookup"><span data-stu-id="cee38-159">If possible, create a gateway subnet using a CIDR block of /28 or /27 tooprovide enough IP addresses tooaccommodate additional future configuration requirements.</span></span>

[!INCLUDE [vpn-gateway-add-gwsubnet-rm-portal](../../includes/vpn-gateway-add-gwsubnet-p2s-rm-portal-include.md)]

## <span data-ttu-id="cee38-160"><a name="dns"></a>3.指定 DNS 伺服器 (選擇性)</span><span class="sxs-lookup"><span data-stu-id="cee38-160"><a name="dns"></a>3. Specify a DNS server (optional)</span></span>

<span data-ttu-id="cee38-161">建立虛擬網路之後，您可以加入 hello IP 位址的 DNS 伺服器 toohandle 名稱解析。</span><span class="sxs-lookup"><span data-stu-id="cee38-161">After you create your virtual network, you can add hello IP address of a DNS server toohandle name resolution.</span></span> <span data-ttu-id="cee38-162">hello DNS 伺服器是針對此設定，選擇性，但如果您想名稱解析。</span><span class="sxs-lookup"><span data-stu-id="cee38-162">hello DNS server is optional for this configuration, but required if you want name resolution.</span></span> <span data-ttu-id="cee38-163">指定一個值並不會建立新的 DNS 伺服器。</span><span class="sxs-lookup"><span data-stu-id="cee38-163">Specifying a value does not create a new DNS server.</span></span> <span data-ttu-id="cee38-164">hello 您指定的 DNS 伺服器 IP 位址應該可以解決 hello 您所連接的 hello 資源名稱的 DNS 伺服器。</span><span class="sxs-lookup"><span data-stu-id="cee38-164">hello DNS server IP address that you specify should be a DNS server that can resolve hello names for hello resources you are connecting to.</span></span> <span data-ttu-id="cee38-165">例如，我們使用私人 IP 位址，但很可能這不是您的 DNS 伺服器 hello IP 位址。</span><span class="sxs-lookup"><span data-stu-id="cee38-165">For this example, we used a private IP address, but it is likely that this is not hello IP address of your DNS server.</span></span> <span data-ttu-id="cee38-166">為確定 toouse 您自己的值。</span><span class="sxs-lookup"><span data-stu-id="cee38-166">Be sure toouse your own values.</span></span>

[!INCLUDE [vpn-gateway-add-dns-rm-portal](../../includes/vpn-gateway-add-dns-rm-portal-include.md)]

## <span data-ttu-id="cee38-167"><a name="creategw"></a>4.建立虛擬網路閘道</span><span class="sxs-lookup"><span data-stu-id="cee38-167"><a name="creategw"></a>4. Create a virtual network gateway</span></span>

[!INCLUDE [create-gateway](../../includes/vpn-gateway-add-gw-p2s-rm-portal-include.md)]

## <span data-ttu-id="cee38-168"><a name="generatecert"></a>5.產生憑證</span><span class="sxs-lookup"><span data-stu-id="cee38-168"><a name="generatecert"></a>5. Generate certificates</span></span>

<span data-ttu-id="cee38-169">Azure tooauthenticate 連接 tooa VNet 透過點對站 VPN 連線的用戶端會使用憑證。</span><span class="sxs-lookup"><span data-stu-id="cee38-169">Certificates are used by Azure tooauthenticate clients connecting tooa VNet over a Point-to-Site VPN connection.</span></span> <span data-ttu-id="cee38-170">一旦您取得根憑證，您[上傳](#uploadfile)hello tooAzure 公開金鑰資訊。</span><span class="sxs-lookup"><span data-stu-id="cee38-170">Once you obtain a root certificate, you [upload](#uploadfile) hello public key information tooAzure.</span></span> <span data-ttu-id="cee38-171">hello 根憑證便會視為 azure 的 ' trusted'，連線透過 P2S toohello 虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="cee38-171">hello root certificate is then considered 'trusted' by Azure for connection over P2S toohello virtual network.</span></span> <span data-ttu-id="cee38-172">您也會從 hello 的受信任的根憑證產生用戶端憑證，然後將它們安裝在每部用戶端電腦上。</span><span class="sxs-lookup"><span data-stu-id="cee38-172">You also generate client certificates from hello trusted root certificate, and then install them on each client computer.</span></span> <span data-ttu-id="cee38-173">hello 用戶端憑證時，使用的 tooauthenticate hello 用戶端會起始連線 toohello VNet。</span><span class="sxs-lookup"><span data-stu-id="cee38-173">hello client certificate is used tooauthenticate hello client when it initiates a connection toohello VNet.</span></span> 

### <span data-ttu-id="cee38-174"><a name="getcer"></a>1.取得 hello hello 根憑證的.cer 檔案</span><span class="sxs-lookup"><span data-stu-id="cee38-174"><a name="getcer"></a>1. Obtain hello .cer file for hello root certificate</span></span>

[!INCLUDE [root-certificate](../../includes/vpn-gateway-p2s-rootcert-include.md)]

### <span data-ttu-id="cee38-175"><a name="generateclientcert"></a>2.產生用戶端憑證 </span><span class="sxs-lookup"><span data-stu-id="cee38-175"><a name="generateclientcert"></a>2. Generate a client certificate</span></span>

[!INCLUDE [generate-client-cert](../../includes/vpn-gateway-p2s-clientcert-include.md)]

## <span data-ttu-id="cee38-176"><a name="addresspool"></a>6.新增 hello 用戶端位址集區</span><span class="sxs-lookup"><span data-stu-id="cee38-176"><a name="addresspool"></a>6. Add hello client address pool</span></span>

<span data-ttu-id="cee38-177">hello 用戶端位址集區是您指定的私人 IP 位址範圍。</span><span class="sxs-lookup"><span data-stu-id="cee38-177">hello client address pool is a range of private IP addresses that you specify.</span></span> <span data-ttu-id="cee38-178">透過點對站 VPN 連接的 hello 用戶端會接收來自這個範圍內的 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="cee38-178">hello clients that connect over a Point-to-Site VPN receive an IP address from this range.</span></span> <span data-ttu-id="cee38-179">搭配您從，連接的 hello 在內部部署位置或 hello 您想要 tooconnect 的 VNet 的私用的 IP 位址範圍不會重疊。</span><span class="sxs-lookup"><span data-stu-id="cee38-179">Use a private IP address range that does not overlap with hello on-premises location that you connect from, or hello VNet that you want tooconnect to.</span></span>

1. <span data-ttu-id="cee38-180">一旦建立 hello 虛擬網路閘道之後，瀏覽 toohello**設定**hello 虛擬網路閘道頁面區段。</span><span class="sxs-lookup"><span data-stu-id="cee38-180">Once hello virtual network gateway has been created, navigate toohello **Settings** section of hello virtual network gateway page.</span></span> <span data-ttu-id="cee38-181">在 hello**設定**區段中，按一下**點對站組態**tooopen hello**點-到-站台-設定**頁面。</span><span class="sxs-lookup"><span data-stu-id="cee38-181">In hello **Settings** section, click **Point-to-site configuration** tooopen hello **Point-to-Site-Configuration** page.</span></span>

  ![點對站頁面](./media/vpn-gateway-howto-point-to-site-resource-manager-portal/gatewayblade.png)
2. <span data-ttu-id="cee38-183">在 hello**點-到-站台-設定** 頁面上，您可以刪除 hello 自動填滿範圍，然後新增 hello 私用 IP 位址範圍的 toouse。</span><span class="sxs-lookup"><span data-stu-id="cee38-183">On hello **Point-to-Site-Configuration** page, you can delete hello auto-filled range, then add hello private IP address range that you want toouse.</span></span> <span data-ttu-id="cee38-184">按一下**儲存**toovalidate 和儲存 hello 設定。</span><span class="sxs-lookup"><span data-stu-id="cee38-184">Click **Save** toovalidate and save hello setting.</span></span>

  ![用戶端位址集區](./media/vpn-gateway-howto-point-to-site-resource-manager-portal/ipaddresspool.png)

## <span data-ttu-id="cee38-186"><a name="uploadfile"></a>7.上傳 hello 根憑證的公開憑證資料</span><span class="sxs-lookup"><span data-stu-id="cee38-186"><a name="uploadfile"></a>7. Upload hello root certificate public certificate data</span></span>

<span data-ttu-id="cee38-187">建立 hello 閘道之後，您上傳 hello 的公開金鑰資訊 hello 根憑證 tooAzure。</span><span class="sxs-lookup"><span data-stu-id="cee38-187">After hello gateway has been created, you upload hello public key information for hello root certificate tooAzure.</span></span> <span data-ttu-id="cee38-188">一旦上傳 hello 公用憑證資料時，Azure 可以使用它 tooauthenticate 安裝用戶端，已從 hello 信任的根憑證產生用戶端憑證。</span><span class="sxs-lookup"><span data-stu-id="cee38-188">Once hello public certificate data is uploaded, Azure can use it tooauthenticate clients that have installed a client certificate generated from hello trusted root certificate.</span></span> <span data-ttu-id="cee38-189">您可以上傳其他受信任的根憑證總 tooa 總共 20。</span><span class="sxs-lookup"><span data-stu-id="cee38-189">You can upload additional trusted root certificates- up tooa total of 20.</span></span>

1. <span data-ttu-id="cee38-190">憑證會加入在 hello**點對站組態**頁面 hello**根憑證**> 一節。</span><span class="sxs-lookup"><span data-stu-id="cee38-190">Certificates are added on hello **Point-to-site configuration** page in hello **Root certificate** section.</span></span>  
2. <span data-ttu-id="cee38-191">請確定您匯出 hello 根憑證，為 base-64 編碼 X.509 (.cer) 檔案。</span><span class="sxs-lookup"><span data-stu-id="cee38-191">Make sure that you exported hello root certificate as a Base-64 encoded X.509 (.cer) file.</span></span> <span data-ttu-id="cee38-192">因此您可以使用文字編輯器開啟 hello 憑證，您會需要 tooexport hello 憑證，這種格式。</span><span class="sxs-lookup"><span data-stu-id="cee38-192">You need tooexport hello certificate in this format so you can open hello certificate with text editor.</span></span>
3. <span data-ttu-id="cee38-193">使用文字編輯器，例如 [記事本] 開啟 hello 的憑證。</span><span class="sxs-lookup"><span data-stu-id="cee38-193">Open hello certificate with a text editor, such as Notepad.</span></span> <span data-ttu-id="cee38-194">複製 hello 憑證資料時，請確認您已複製的 hello 文字做為一個連續的一行，而不換行字元或換。</span><span class="sxs-lookup"><span data-stu-id="cee38-194">When copying hello certificate data, make sure that you copy hello text as one continuous line without carriage returns or line feeds.</span></span> <span data-ttu-id="cee38-195">您可能需要 toomodify 您 hello 文字編輯器 too'Show 符號/顯示所有字元 toosee hello 歸位字元傳回和行摘要中的檢視。</span><span class="sxs-lookup"><span data-stu-id="cee38-195">You may need toomodify your view in hello text editor too'Show Symbol/Show all characters' toosee hello carriage returns and line feeds.</span></span> <span data-ttu-id="cee38-196">複製下列區段以連續一行只 hello:</span><span class="sxs-lookup"><span data-stu-id="cee38-196">Copy only hello following section as one continuous line:</span></span>

  ![憑證資料](./media/vpn-gateway-howto-point-to-site-resource-manager-portal/copycert.png)
4. <span data-ttu-id="cee38-198">Hello 憑證資料貼入 hello**公用憑證資料**欄位。</span><span class="sxs-lookup"><span data-stu-id="cee38-198">Paste hello certificate data into hello **Public Certificate Data** field.</span></span> <span data-ttu-id="cee38-199">**名稱**hello 憑證，然後按一下**儲存**。</span><span class="sxs-lookup"><span data-stu-id="cee38-199">**Name** hello certificate, and then click **Save**.</span></span> <span data-ttu-id="cee38-200">您可以加入 too20 受信任的根憑證。</span><span class="sxs-lookup"><span data-stu-id="cee38-200">You can add up too20 trusted root certificates.</span></span>

  ![憑證上傳](./media/vpn-gateway-howto-point-to-site-resource-manager-portal/rootcertupload.png)

## <span data-ttu-id="cee38-202"><a name="clientconfig"></a>8.產生並安裝 hello VPN 用戶端組態封裝</span><span class="sxs-lookup"><span data-stu-id="cee38-202"><a name="clientconfig"></a>8. Generate and install hello VPN client configuration package</span></span>

<span data-ttu-id="cee38-203">tooconnect tooa 使用點對站 VPN 的 VNet，每個用戶端必須安裝以 hello 設定來設定原生 VPN 用戶端 hello 用戶端組態封裝及其必要 tooconnect toohello 虛擬網路的檔案。</span><span class="sxs-lookup"><span data-stu-id="cee38-203">tooconnect tooa VNet using a Point-to-Site VPN, each client must install a client configuration package that configures hello native VPN client with hello settings and files that are necessary tooconnect toohello virtual network.</span></span> <span data-ttu-id="cee38-204">hello VPN 用戶端組態封裝設定 hello 原生 Windows VPN 用戶端，它不會安裝新的或不同的 VPN 用戶端。</span><span class="sxs-lookup"><span data-stu-id="cee38-204">hello VPN client configuration package configures hello native Windows VPN client, it doesn't install a new or different VPN client.</span></span>

<span data-ttu-id="cee38-205">只要 hello 版本符合 hello 用戶端 hello 架構，您可以使用相同的 VPN 用戶端組態封裝每個用戶端電腦，hello。</span><span class="sxs-lookup"><span data-stu-id="cee38-205">You can use hello same VPN client configuration package on each client computer, as long as hello version matches hello architecture for hello client.</span></span> <span data-ttu-id="cee38-206">Hello 清單中的用戶端作業系統支援，請參閱 hello[點對站連線常見問題集](#faq)hello 本文結尾處。</span><span class="sxs-lookup"><span data-stu-id="cee38-206">For hello list of client operating systems that are supported, see hello [Point-to-Site connections FAQ](#faq) at hello end of this article.</span></span>

### <a name="step-1---generate-and-download-hello-client-configuration-package"></a><span data-ttu-id="cee38-207">步驟 1-產生並下載 hello 用戶端組態封裝</span><span class="sxs-lookup"><span data-stu-id="cee38-207">Step 1 - Generate and download hello client configuration package</span></span>

1. <span data-ttu-id="cee38-208">在 hello**點對站組態**頁面上，按一下**下載 VPN 用戶端**tooopen hello**下載 VPN 用戶端**頁面。</span><span class="sxs-lookup"><span data-stu-id="cee38-208">On hello **Point-to-site configuration** page, click **Download VPN client** tooopen hello **Download VPN client** page.</span></span> <span data-ttu-id="cee38-209">花一分鐘或兩個 hello 封裝 toogenerate 進行。</span><span class="sxs-lookup"><span data-stu-id="cee38-209">It takes a minute or two for hello package toogenerate.</span></span>

  ![VPN 用戶端下載 1](./media/vpn-gateway-howto-point-to-site-resource-manager-portal/downloadvpnclient1.png)
2. <span data-ttu-id="cee38-211">選取針對您的用戶端 hello 正確的封裝，然後按一下**下載**。</span><span class="sxs-lookup"><span data-stu-id="cee38-211">Select hello correct package for your client, and then click **Download**.</span></span> <span data-ttu-id="cee38-212">儲存 hello 組態封裝檔案。</span><span class="sxs-lookup"><span data-stu-id="cee38-212">Save hello configuration package file.</span></span> <span data-ttu-id="cee38-213">您在每個連線 toohello 虛擬網路的用戶端電腦上安裝 hello VPN 用戶端組態封裝。</span><span class="sxs-lookup"><span data-stu-id="cee38-213">You install hello VPN client configuration package on each client computer that connects toohello virtual network.</span></span>

  ![VPN 用戶端下載 2](./media/vpn-gateway-howto-point-to-site-resource-manager-portal/vpnclient.png)

### <a name="step-2---install-hello-client-configuration-package"></a><span data-ttu-id="cee38-215">步驟 2-安裝 hello 用戶端組態封裝</span><span class="sxs-lookup"><span data-stu-id="cee38-215">Step 2 - Install hello client configuration package</span></span>

1. <span data-ttu-id="cee38-216">複製 hello 設定檔在本機 toohello 電腦，您想 tooconnect tooyour 虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="cee38-216">Copy hello configuration file locally toohello computer that you want tooconnect tooyour virtual network.</span></span> 
2. <span data-ttu-id="cee38-217">按兩下 hello.exe 檔案 tooinstall hello 套件 hello 用戶端電腦上。</span><span class="sxs-lookup"><span data-stu-id="cee38-217">Double-click hello .exe file tooinstall hello package on hello client computer.</span></span> <span data-ttu-id="cee38-218">建立 hello 組態套件，因為未簽署，您可能會看到警告。</span><span class="sxs-lookup"><span data-stu-id="cee38-218">Because you created hello configuration package, it is not signed and you may see a warning.</span></span> <span data-ttu-id="cee38-219">如果您取得 Windows SmartScreen 快顯視窗，請按一下**進一歩**（左側 hello），然後**繼續執行**tooinstall hello 封裝。</span><span class="sxs-lookup"><span data-stu-id="cee38-219">If you get a Windows SmartScreen popup, click **More info** (on hello left), then **Run anyway** tooinstall hello package.</span></span>
3. <span data-ttu-id="cee38-220">Hello 用戶端電腦上安裝 hello 套件。</span><span class="sxs-lookup"><span data-stu-id="cee38-220">Install hello package on hello client computer.</span></span> <span data-ttu-id="cee38-221">如果您取得 Windows SmartScreen 快顯視窗，請按一下**進一歩**（左側 hello），然後**繼續執行**tooinstall hello 封裝。</span><span class="sxs-lookup"><span data-stu-id="cee38-221">If you get a Windows SmartScreen popup, click **More info** (on hello left), then **Run anyway** tooinstall hello package.</span></span>
4. <span data-ttu-id="cee38-222">Hello 用戶端電腦上，瀏覽過**網路設定**按一下**VPN**。</span><span class="sxs-lookup"><span data-stu-id="cee38-222">On hello client computer, navigate too**Network Settings** and click **VPN**.</span></span> <span data-ttu-id="cee38-223">hello VPN 連線會顯示 hello hello 連接到的虛擬網路名稱。</span><span class="sxs-lookup"><span data-stu-id="cee38-223">hello VPN connection shows hello name of hello virtual network that it connects to.</span></span>

## <span data-ttu-id="cee38-224"><a name="installclientcert"></a>9.安裝匯出的用戶端憑證</span><span class="sxs-lookup"><span data-stu-id="cee38-224"><a name="installclientcert"></a>9. Install an exported client certificate</span></span>

<span data-ttu-id="cee38-225">如果您想要 toocreate P2S 連線 hello 以外的用戶端電腦從您使用 toogenerate hello 用戶端憑證，您需要 tooinstall 用戶端憑證。</span><span class="sxs-lookup"><span data-stu-id="cee38-225">If you want toocreate a P2S connection from a client computer other than hello one you used toogenerate hello client certificates, you need tooinstall a client certificate.</span></span> <span data-ttu-id="cee38-226">安裝用戶端憑證，必須已建立 hello 用戶端憑證匯出時的 hello 密碼。</span><span class="sxs-lookup"><span data-stu-id="cee38-226">When installing a client certificate, you need hello password that was created when hello client certificate was exported.</span></span> <span data-ttu-id="cee38-227">一般而言，它是只需按兩下 hello 憑證並將其安裝。</span><span class="sxs-lookup"><span data-stu-id="cee38-227">Typically, it is just a matter of double-clicking hello certificate and installing it.</span></span>

<span data-ttu-id="cee38-228">請確定 hello 用戶端憑證匯出為.pfx 以及 hello 整個憑證鏈結 （這是 hello 預設值）。</span><span class="sxs-lookup"><span data-stu-id="cee38-228">Make sure hello client certificate was exported as a .pfx along with hello entire certificate chain (which is hello default).</span></span> <span data-ttu-id="cee38-229">否則 hello 根憑證資訊不存在 hello 用戶端電腦上，而且 hello 用戶端將不會無法 tooauthenticate 正確。</span><span class="sxs-lookup"><span data-stu-id="cee38-229">Otherwise, hello root certificate information isn't present on hello client computer and hello client won't be able tooauthenticate properly.</span></span> <span data-ttu-id="cee38-230">如需詳細資訊，請參閱[安裝匯出的用戶端憑證](vpn-gateway-certificates-point-to-site.md#install)。</span><span class="sxs-lookup"><span data-stu-id="cee38-230">For more information, see [Install an exported client certificate](vpn-gateway-certificates-point-to-site.md#install).</span></span>

## <span data-ttu-id="cee38-231"><a name="connect"></a>10.連接 tooAzure</span><span class="sxs-lookup"><span data-stu-id="cee38-231"><a name="connect"></a>10. Connect tooAzure</span></span>

1. <span data-ttu-id="cee38-232">tooconnect tooyour VNet，hello 用戶端電腦上，瀏覽 tooVPN 連線，並尋找您所建立的 hello VPN 連線。</span><span class="sxs-lookup"><span data-stu-id="cee38-232">tooconnect tooyour VNet, on hello client computer, navigate tooVPN connections and locate hello VPN connection that you created.</span></span> <span data-ttu-id="cee38-233">它會命名為與虛擬網路名稱相同的 hello。</span><span class="sxs-lookup"><span data-stu-id="cee38-233">It is named hello same name as your virtual network.</span></span> <span data-ttu-id="cee38-234">按一下 [ **連接**]。</span><span class="sxs-lookup"><span data-stu-id="cee38-234">Click **Connect**.</span></span> <span data-ttu-id="cee38-235">快顯視窗訊息可能會出現參考 toousing hello 憑證。</span><span class="sxs-lookup"><span data-stu-id="cee38-235">A pop-up message may appear that refers toousing hello certificate.</span></span> <span data-ttu-id="cee38-236">按一下**繼續**toouse 提升的權限。</span><span class="sxs-lookup"><span data-stu-id="cee38-236">Click **Continue** toouse elevated privileges.</span></span>

2. <span data-ttu-id="cee38-237">在 hello**連接**狀態] 頁面上，按一下 [**連接**toostart hello 連線。</span><span class="sxs-lookup"><span data-stu-id="cee38-237">On hello **Connection** status page, click **Connect** toostart hello connection.</span></span> <span data-ttu-id="cee38-238">如果您看到**選取憑證**畫面上，確認憑證顯示 hello 用戶端 hello 其中一個要 toouse tooconnect。</span><span class="sxs-lookup"><span data-stu-id="cee38-238">If you see a **Select Certificate** screen, verify that hello client certificate showing is hello one that you want toouse tooconnect.</span></span> <span data-ttu-id="cee38-239">如果不是，使用 hello 下拉箭號 tooselect hello 正確的憑證，，然後按一下**確定**。</span><span class="sxs-lookup"><span data-stu-id="cee38-239">If it is not, use hello drop-down arrow tooselect hello correct certificate, and then click **OK**.</span></span>

  ![VPN 用戶端連線 tooAzure](./media/vpn-gateway-howto-point-to-site-resource-manager-portal/clientconnect.png)
3. <span data-ttu-id="cee38-241">已建立您的連線。</span><span class="sxs-lookup"><span data-stu-id="cee38-241">Your connection is established.</span></span>

  ![連線已建立](./media/vpn-gateway-howto-point-to-site-resource-manager-portal/connected.png)

#### <a name="troubleshooting-p2s-connections"></a><span data-ttu-id="cee38-243">針對 P2S 連線進行疑難排解</span><span class="sxs-lookup"><span data-stu-id="cee38-243">Troubleshooting P2S connections</span></span>

[!INCLUDE [verifies client certificates](../../includes/vpn-gateway-certificates-verify-client-cert-include.md)]

## <span data-ttu-id="cee38-244"><a name="verify"></a>11.確認您的連接</span><span class="sxs-lookup"><span data-stu-id="cee38-244"><a name="verify"></a>11. Verify your connection</span></span>

1. <span data-ttu-id="cee38-245">tooverify VPN 連線為作用中，開啟提升權限的命令提示字元並執行*ipconfig/all*。</span><span class="sxs-lookup"><span data-stu-id="cee38-245">tooverify that your VPN connection is active, open an elevated command prompt, and run *ipconfig/all*.</span></span>
2. <span data-ttu-id="cee38-246">檢視 hello 結果。</span><span class="sxs-lookup"><span data-stu-id="cee38-246">View hello results.</span></span> <span data-ttu-id="cee38-247">請注意，您收到 hello IP 位址的其中一個 hello 內 hello 點對站 VPN 用戶端位址集區，您在您的組態中指定的位址。</span><span class="sxs-lookup"><span data-stu-id="cee38-247">Notice that hello IP address you received is one of hello addresses within hello Point-to-Site VPN Client Address Pool that you specified in your configuration.</span></span> <span data-ttu-id="cee38-248">hello 結果會類似 toothis 範例：</span><span class="sxs-lookup"><span data-stu-id="cee38-248">hello results are similar toothis example:</span></span>

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

## <span data-ttu-id="cee38-249"><a name="connectVM"></a>Tooa 虛擬機器連線</span><span class="sxs-lookup"><span data-stu-id="cee38-249"><a name="connectVM"></a>Connect tooa virtual machine</span></span>

[!INCLUDE [Connect tooa VM](../../includes/vpn-gateway-connect-vm-p2s-include.md)]

## <span data-ttu-id="cee38-250"><a name="add"></a>新增或移除受信任的根憑證</span><span class="sxs-lookup"><span data-stu-id="cee38-250"><a name="add"></a>Add or remove trusted root certificates</span></span>

<span data-ttu-id="cee38-251">您可以從 Azure 新增和移除受信任的根憑證。</span><span class="sxs-lookup"><span data-stu-id="cee38-251">You can add and remove trusted root certificates from Azure.</span></span> <span data-ttu-id="cee38-252">當您移除的根憑證時，產生從該根憑證的用戶端將不會無法 tooauthenticate，而且不會因此無法 tooconnect。</span><span class="sxs-lookup"><span data-stu-id="cee38-252">When you remove a root certificate, clients that have a certificate generated from that root won't be able tooauthenticate, and thus will not be able tooconnect.</span></span> <span data-ttu-id="cee38-253">如果您想用戶端 tooauthenticate 連接時，您會需要的 tooinstall 從受信任的 （上傳） tooAzure 的根憑證產生新的用戶端憑證。</span><span class="sxs-lookup"><span data-stu-id="cee38-253">If you want a client tooauthenticate and connect, you need tooinstall a new client certificate generated from a root certificate that is trusted (uploaded) tooAzure.</span></span>

### <a name="tooadd-a-trusted-root-certificate"></a><span data-ttu-id="cee38-254">tooadd 信任的根憑證</span><span class="sxs-lookup"><span data-stu-id="cee38-254">tooadd a trusted root certificate</span></span>

<span data-ttu-id="cee38-255">您可以加總 too20 受信任的根憑證.cer 檔案 tooAzure。</span><span class="sxs-lookup"><span data-stu-id="cee38-255">You can add up too20 trusted root certificate .cer files tooAzure.</span></span> <span data-ttu-id="cee38-256">如需指示，請參閱 hello 節[受信任的根憑證上傳](#uploadfile)本文中。</span><span class="sxs-lookup"><span data-stu-id="cee38-256">For instructions, see hello section [Upload a trusted root certificate](#uploadfile) in this article.</span></span>

### <a name="tooremove-a-trusted-root-certificate"></a><span data-ttu-id="cee38-257">tooremove 信任的根憑證</span><span class="sxs-lookup"><span data-stu-id="cee38-257">tooremove a trusted root certificate</span></span>

1. <span data-ttu-id="cee38-258">tooremove 信任的根憑證，瀏覽 toohello**點對站組態**虛擬網路閘道的頁面。</span><span class="sxs-lookup"><span data-stu-id="cee38-258">tooremove a trusted root certificate, navigate toohello **Point-to-site configuration** page for your virtual network gateway.</span></span>
2. <span data-ttu-id="cee38-259">在 [hello**根憑證**區段 hello] 頁面上，找出您想要 tooremove hello 憑證。</span><span class="sxs-lookup"><span data-stu-id="cee38-259">In hello **Root certificate** section of hello page, locate hello certificate that you want tooremove.</span></span>
3. <span data-ttu-id="cee38-260">按一下 hello 省略符號 下一步 toohello 憑證，然後按一下移除。</span><span class="sxs-lookup"><span data-stu-id="cee38-260">Click hello ellipsis next toohello certificate, and then click 'Remove'.</span></span>

## <span data-ttu-id="cee38-261"><a name="revokeclient"></a>撤銷用戶端憑證</span><span class="sxs-lookup"><span data-stu-id="cee38-261"><a name="revokeclient"></a>Revoke a client certificate</span></span>

<span data-ttu-id="cee38-262">您可以撤銷用戶端憑證。</span><span class="sxs-lookup"><span data-stu-id="cee38-262">You can revoke client certificates.</span></span> <span data-ttu-id="cee38-263">hello 憑證撤銷清單可讓您 tooselectively 拒絕個別用戶端憑證為基礎的點對站連線。</span><span class="sxs-lookup"><span data-stu-id="cee38-263">hello certificate revocation list allows you tooselectively deny Point-to-Site connectivity based on individual client certificates.</span></span> <span data-ttu-id="cee38-264">這與移除受信任的根憑證不同。</span><span class="sxs-lookup"><span data-stu-id="cee38-264">This is different than removing a trusted root certificate.</span></span> <span data-ttu-id="cee38-265">如果您從 Azure 移除受信任的根憑證.cer，它就會撤銷所有用戶端憑證產生/簽署由 hello 撤銷的根憑證的 hello 存取權。</span><span class="sxs-lookup"><span data-stu-id="cee38-265">If you remove a trusted root certificate .cer from Azure, it revokes hello access for all client certificates generated/signed by hello revoked root certificate.</span></span> <span data-ttu-id="cee38-266">撤銷用戶端憑證，而不是 hello 根憑證，可讓 hello 產生從 hello 根憑證 toocontinue toobe 用來驗證其他憑證。</span><span class="sxs-lookup"><span data-stu-id="cee38-266">Revoking a client certificate, rather than hello root certificate, allows hello other certificates that were generated from hello root certificate toocontinue toobe used for authentication.</span></span>

<span data-ttu-id="cee38-267">hello 常見的作法是 toouse hello 根憑證 toomanage 存取小組或組織層級時使用已撤銷用戶端憑證來進行個別使用者的更細緻的存取控制。</span><span class="sxs-lookup"><span data-stu-id="cee38-267">hello common practice is toouse hello root certificate toomanage access at team or organization levels, while using revoked client certificates for fine-grained access control on individual users.</span></span>

### <a name="toorevoke-a-client-certificate"></a><span data-ttu-id="cee38-268">toorevoke 用戶端憑證</span><span class="sxs-lookup"><span data-stu-id="cee38-268">toorevoke a client certificate</span></span>

<span data-ttu-id="cee38-269">您可以藉由新增 hello 指紋 toohello 撤銷清單來撤銷用戶端憑證。</span><span class="sxs-lookup"><span data-stu-id="cee38-269">You can revoke a client certificate by adding hello thumbprint toohello revocation list.</span></span>

1. <span data-ttu-id="cee38-270">擷取 hello 用戶端憑證指紋。</span><span class="sxs-lookup"><span data-stu-id="cee38-270">Retrieve hello client certificate thumbprint.</span></span> <span data-ttu-id="cee38-271">如需詳細資訊，請參閱[tooretrieve 如何 hello 憑證的指紋](https://msdn.microsoft.com/library/ms734695.aspx)。</span><span class="sxs-lookup"><span data-stu-id="cee38-271">For more information, see [How tooretrieve hello Thumbprint of a Certificate](https://msdn.microsoft.com/library/ms734695.aspx).</span></span>
2. <span data-ttu-id="cee38-272">複製 hello 資訊 tooa 文字編輯器，並移除所有的空間，使其連續的字串。</span><span class="sxs-lookup"><span data-stu-id="cee38-272">Copy hello information tooa text editor and remove all spaces so that it is a continuous string.</span></span>
3. <span data-ttu-id="cee38-273">瀏覽 toohello 虛擬網路閘道**點-到-站台-設定**頁面。</span><span class="sxs-lookup"><span data-stu-id="cee38-273">Navigate toohello virtual network gateway **Point-to-site-configuration** page.</span></span> <span data-ttu-id="cee38-274">這是 hello 您用過的相同頁面[受信任的根憑證上傳](#uploadfile)。</span><span class="sxs-lookup"><span data-stu-id="cee38-274">This is hello same page that you used too[upload a trusted root certificate](#uploadfile).</span></span>
4. <span data-ttu-id="cee38-275">在 hello**撤銷的憑證**區段中，輸入 hello 憑證 （不需要 toobe hello 憑證 CN） 的好記名稱。</span><span class="sxs-lookup"><span data-stu-id="cee38-275">In hello **Revoked certificates** section, input a friendly name for hello certificate (it doesn't have toobe hello certificate CN).</span></span>
5. <span data-ttu-id="cee38-276">複製並貼上 hello 指紋字串 toohello**指紋**欄位。</span><span class="sxs-lookup"><span data-stu-id="cee38-276">Copy and paste hello thumbprint string toohello **Thumbprint** field.</span></span>
6. <span data-ttu-id="cee38-277">hello 指紋驗證，並會自動加入 toohello 撤銷清單。</span><span class="sxs-lookup"><span data-stu-id="cee38-277">hello thumbprint validates and is automatically added toohello revocation list.</span></span> <span data-ttu-id="cee38-278">囉 」 畫面上出現訊息該 hello 正在更新清單。</span><span class="sxs-lookup"><span data-stu-id="cee38-278">A message appears on hello screen that hello list is updating.</span></span> 
7. <span data-ttu-id="cee38-279">更新完成後，hello 憑證不再可以使用的 tooconnect。</span><span class="sxs-lookup"><span data-stu-id="cee38-279">After updating has completed, hello certificate can no longer be used tooconnect.</span></span> <span data-ttu-id="cee38-280">使用此憑證的 tooconnect 再試一次的用戶端收到訊息，指出該 hello 憑證不再有效。</span><span class="sxs-lookup"><span data-stu-id="cee38-280">Clients that try tooconnect using this certificate receive a message saying that hello certificate is no longer valid.</span></span>

## <span data-ttu-id="cee38-281"><a name="faq"></a>點對站常見問題集</span><span class="sxs-lookup"><span data-stu-id="cee38-281"><a name="faq"></a>Point-to-Site FAQ</span></span>

[!INCLUDE [Point-to-Site FAQ](../../includes/vpn-gateway-point-to-site-faq-include.md)]

## <a name="next-steps"></a><span data-ttu-id="cee38-282">後續步驟</span><span class="sxs-lookup"><span data-stu-id="cee38-282">Next steps</span></span>
<span data-ttu-id="cee38-283">一旦完成您的連線，您可以將虛擬機器 tooyour 虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="cee38-283">Once your connection is complete, you can add virtual machines tooyour virtual networks.</span></span> <span data-ttu-id="cee38-284">如需詳細資訊，請參閱[虛擬機器](https://docs.microsoft.com/azure/#pivot=services&panel=Compute)。</span><span class="sxs-lookup"><span data-stu-id="cee38-284">For more information, see [Virtual Machines](https://docs.microsoft.com/azure/#pivot=services&panel=Compute).</span></span> <span data-ttu-id="cee38-285">toounderstand 深入了解網路和虛擬機器，請參閱[Azure 與 Linux VM 網路概觀](../virtual-machines/linux/azure-vm-network-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="cee38-285">toounderstand more about networking and virtual machines, see [Azure and Linux VM network overview](../virtual-machines/linux/azure-vm-network-overview.md).</span></span>
