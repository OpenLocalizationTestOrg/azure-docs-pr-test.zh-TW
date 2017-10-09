---
title: "連接電腦 tooa 虛擬網路使用點對站台和憑證驗證： Azure 入口網站的傳統 |Microsoft 文件"
description: "安全地連線 tooyour 傳統 Azure 虛擬網路建立點對站 VPN 閘道連線使用 hello Azure 入口網站。"
services: vpn-gateway
documentationcenter: na
author: cherylmc
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: 65e14579-86cf-4d29-a6ac-547ccbd743bd
ms.service: vpn-gateway
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/03/2017
ms.author: cherylmc
ms.openlocfilehash: 9b53ba43ee4dfb61defeec458905fb1f1b18c3a5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="configure-a-point-to-site-connection-tooa-vnet-using-certificate-authentication-classic-azure-portal"></a><span data-ttu-id="eb308-103">設定點對站連線 tooa VNet 使用憑證驗證 （傳統）： Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="eb308-103">Configure a Point-to-Site connection tooa VNet using certificate authentication (classic): Azure portal</span></span>

[!INCLUDE [deployment models](../../includes/vpn-gateway-classic-deployment-model-include.md)]

<span data-ttu-id="eb308-104">本文章將示範如何在 hello 傳統部署模型中使用的點對站連接的 VNet toocreate hello Azure 入口網站。</span><span class="sxs-lookup"><span data-stu-id="eb308-104">This article shows you how toocreate a VNet with a Point-to-Site connection in hello classic deployment model using hello Azure portal.</span></span> <span data-ttu-id="eb308-105">此組態會使用用戶端連接的憑證 tooauthenticate hello。</span><span class="sxs-lookup"><span data-stu-id="eb308-105">This configuration uses certificates tooauthenticate hello connecting client.</span></span> <span data-ttu-id="eb308-106">您也可以建立此組態使用不同的部署工具或部署模型，從下列清單中的 hello 選取不同的選項：</span><span class="sxs-lookup"><span data-stu-id="eb308-106">You can also create this configuration using a different deployment tool or deployment model by selecting a different option from hello following list:</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="eb308-107">Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="eb308-107">Azure portal</span></span>](vpn-gateway-howto-point-to-site-resource-manager-portal.md)
> * [<span data-ttu-id="eb308-108">PowerShell</span><span class="sxs-lookup"><span data-stu-id="eb308-108">PowerShell</span></span>](vpn-gateway-howto-point-to-site-rm-ps.md)
> * [<span data-ttu-id="eb308-109">Azure 入口網站 (傳統)</span><span class="sxs-lookup"><span data-stu-id="eb308-109">Azure portal (classic)</span></span>](vpn-gateway-howto-point-to-site-classic-azure-portal.md)
>

<span data-ttu-id="eb308-110">點對站 (P2S) VPN 閘道，可讓您建立從個別的用戶端電腦的安全連線 tooyour 虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="eb308-110">A Point-to-Site (P2S) VPN gateway lets you create a secure connection tooyour virtual network from an individual client computer.</span></span> <span data-ttu-id="eb308-111">當您想要 tooconnect tooyour 從遠端位置，例如當您從家裡或會議 telecommuting VNet，點對站 VPN 連線會很有用。</span><span class="sxs-lookup"><span data-stu-id="eb308-111">Point-to-Site VPN connections are useful when you want tooconnect tooyour VNet from a remote location, such when you are telecommuting from home or a conference.</span></span> <span data-ttu-id="eb308-112">您有只有少數的用戶端需要 tooconnect tooa VNet 時 P2S VPN 也很有用的方案 toouse，而不是站對站 VPN。</span><span class="sxs-lookup"><span data-stu-id="eb308-112">A P2S VPN is also a useful solution toouse instead of a Site-to-Site VPN when you have only a few clients that need tooconnect tooa VNet.</span></span> 

<span data-ttu-id="eb308-113">使用 P2S hello 安全通訊端通道通訊協定 (SSTP)，這是 SSL 型 VPN 通訊協定。</span><span class="sxs-lookup"><span data-stu-id="eb308-113">P2S uses hello Secure Socket Tunneling Protocol (SSTP), which is an SSL-based VPN protocol.</span></span> <span data-ttu-id="eb308-114">建立之 P2S VPN 連線從 hello 用戶端電腦。</span><span class="sxs-lookup"><span data-stu-id="eb308-114">A P2S VPN connection is established by starting it from hello client computer.</span></span>


![Point-to-Site-diagram](./media/vpn-gateway-howto-point-to-site-classic-azure-portal/point-to-site-connection-diagram.png)


<span data-ttu-id="eb308-116">點對站憑證驗證的連接需要 hello 下列：</span><span class="sxs-lookup"><span data-stu-id="eb308-116">Point-to-Site certificate authentication connections require hello following:</span></span>

* <span data-ttu-id="eb308-117">動態 VPN 閘道。</span><span class="sxs-lookup"><span data-stu-id="eb308-117">A Dynamic VPN gateway.</span></span>
* <span data-ttu-id="eb308-118">hello 公開金鑰 （.cer 檔案） 的根憑證，也就是上傳的 tooAzure。</span><span class="sxs-lookup"><span data-stu-id="eb308-118">hello public key (.cer file) for a root certificate, which is uploaded tooAzure.</span></span> <span data-ttu-id="eb308-119">這會被視為受信任的憑證並且用於驗證。</span><span class="sxs-lookup"><span data-stu-id="eb308-119">This is considered a trusted certificate and is used for authentication.</span></span>
* <span data-ttu-id="eb308-120">產生從 hello 根憑證，並會連接每個用戶端電腦上安裝用戶端憑證。</span><span class="sxs-lookup"><span data-stu-id="eb308-120">A client certificate generated from hello root certificate, and installed on each client computer that will connect.</span></span> <span data-ttu-id="eb308-121">此憑證使用於用戶端憑證。</span><span class="sxs-lookup"><span data-stu-id="eb308-121">This certificate is used for client authentication.</span></span>
* <span data-ttu-id="eb308-122">必須在每部連線的用戶端電腦上產生並安裝 VPN 用戶端組態套件。</span><span class="sxs-lookup"><span data-stu-id="eb308-122">A VPN client configuration package must be generated and installed on every client computer that connects.</span></span> <span data-ttu-id="eb308-123">hello 用戶端組態封裝設定 hello 原生 VPN 用戶端已與 hello 所需的資訊 tooconnect toohello VNet hello 作業系統上。</span><span class="sxs-lookup"><span data-stu-id="eb308-123">hello client configuration package configures hello native VPN client that is already on hello operating system with hello necessary information tooconnect toohello VNet.</span></span>

<span data-ttu-id="eb308-124">點對站連線不需要 VPN 裝置或內部部署公眾對應 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="eb308-124">Point-to-Site connections do not require a VPN device or an on-premises public-facing IP address.</span></span> <span data-ttu-id="eb308-125">hello VPN 連線建立透過 SSTP （安全通訊端通道通訊協定）。</span><span class="sxs-lookup"><span data-stu-id="eb308-125">hello VPN connection is created over SSTP (Secure Socket Tunneling Protocol).</span></span> <span data-ttu-id="eb308-126">在 hello 伺服器端，我們支援 SSTP 版本 1.0、 1.1 和 1.2。</span><span class="sxs-lookup"><span data-stu-id="eb308-126">On hello server side, we support SSTP versions 1.0, 1.1, and 1.2.</span></span> <span data-ttu-id="eb308-127">hello 用戶端決定哪一個版本 toouse。</span><span class="sxs-lookup"><span data-stu-id="eb308-127">hello client decides which version toouse.</span></span> <span data-ttu-id="eb308-128">若為 Windows 8.1 和更新版本，SSTP 預設使用 1.2。</span><span class="sxs-lookup"><span data-stu-id="eb308-128">For Windows 8.1 and above, SSTP uses 1.2 by default.</span></span> 

<span data-ttu-id="eb308-129">如需有關點對站連線的詳細資訊，請參閱 hello[點對站常見問題集](#faq)hello 本文結尾處。</span><span class="sxs-lookup"><span data-stu-id="eb308-129">For more information about Point-to-Site connections, see hello [Point-to-Site FAQ](#faq) at hello end of this article.</span></span>

### <a name="example-settings"></a><span data-ttu-id="eb308-130">範例設定</span><span class="sxs-lookup"><span data-stu-id="eb308-130">Example settings</span></span>

<span data-ttu-id="eb308-131">您可以使用下列值 toocreate 測試環境的 hello 或 toothese 值，請參閱 toobetter 了解這篇文章中的 hello 範例：</span><span class="sxs-lookup"><span data-stu-id="eb308-131">You can use hello following values toocreate a test environment, or refer toothese values toobetter understand hello examples in this article:</span></span>

* <span data-ttu-id="eb308-132">**名稱：VNet1**</span><span class="sxs-lookup"><span data-stu-id="eb308-132">**Name: VNet1**</span></span>
* <span data-ttu-id="eb308-133">**位址空間：192.168.0.0/16**</span><span class="sxs-lookup"><span data-stu-id="eb308-133">**Address space: 192.168.0.0/16**</span></span><br><span data-ttu-id="eb308-134">在此範例中，我們只使用一個位址空間。</span><span class="sxs-lookup"><span data-stu-id="eb308-134">For this example, we use only one address space.</span></span> <span data-ttu-id="eb308-135">您可以針對 VNet 使用一個以上的位址空間。</span><span class="sxs-lookup"><span data-stu-id="eb308-135">You can have more than one address space for your VNet.</span></span>
* <span data-ttu-id="eb308-136">**子網路名稱：FrontEnd**</span><span class="sxs-lookup"><span data-stu-id="eb308-136">**Subnet name: FrontEnd**</span></span>
* <span data-ttu-id="eb308-137">**子網路位址範圍：192.168.1.0/24**</span><span class="sxs-lookup"><span data-stu-id="eb308-137">**Subnet address range: 192.168.1.0/24**</span></span>
* <span data-ttu-id="eb308-138">**訂用帳戶：**如果您有多個訂用帳戶，確認您是否使用 hello 正確。</span><span class="sxs-lookup"><span data-stu-id="eb308-138">**Subscription:** If you have more than one subscription, verify that you are using hello correct one.</span></span>
* <span data-ttu-id="eb308-139">**資源群組：TestRG**</span><span class="sxs-lookup"><span data-stu-id="eb308-139">**Resource Group: TestRG**</span></span>
* <span data-ttu-id="eb308-140">**位置：美國東部**</span><span class="sxs-lookup"><span data-stu-id="eb308-140">**Location: East US**</span></span>
* <span data-ttu-id="eb308-141">**連線類型：點對站**</span><span class="sxs-lookup"><span data-stu-id="eb308-141">**Connection type: Point-to-site**</span></span>
* <span data-ttu-id="eb308-142">**用戶端位址空間：172.16.201.0/24**。</span><span class="sxs-lookup"><span data-stu-id="eb308-142">**Client Address Space: 172.16.201.0/24**.</span></span> <span data-ttu-id="eb308-143">VPN 用戶端連線使用這個點對站連接的 VNet 接收 IP 位址從 toohello hello 指定的集區。</span><span class="sxs-lookup"><span data-stu-id="eb308-143">VPN clients that connect toohello VNet using this Point-to-Site connection receive an IP address from hello specified pool.</span></span>
* <span data-ttu-id="eb308-144">**GatewaySubnet: 192.168.200.0/24**。</span><span class="sxs-lookup"><span data-stu-id="eb308-144">**GatewaySubnet: 192.168.200.0/24**.</span></span> <span data-ttu-id="eb308-145">hello 閘道子網路必須使用 hello 名稱為 'GatewaySubnet'。</span><span class="sxs-lookup"><span data-stu-id="eb308-145">hello Gateway subnet must use hello name 'GatewaySubnet'.</span></span>
* <span data-ttu-id="eb308-146">**大小：**選取 hello 閘道 SKU 的 toouse。</span><span class="sxs-lookup"><span data-stu-id="eb308-146">**Size:** Select hello gateway SKU that you want toouse.</span></span>
* <span data-ttu-id="eb308-147">**路由類型：動態**</span><span class="sxs-lookup"><span data-stu-id="eb308-147">**Routing Type: Dynamic**</span></span>

## <span data-ttu-id="eb308-148"><a name="vnetvpn"></a>1.建立虛擬網路和 VPN 閘道</span><span class="sxs-lookup"><span data-stu-id="eb308-148"><a name="vnetvpn"></a>1. Create a virtual network and a VPN gateway</span></span>

<span data-ttu-id="eb308-149">在開始之前，請確認您有 Azure 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="eb308-149">Before beginning, verify that you have an Azure subscription.</span></span> <span data-ttu-id="eb308-150">如果您還沒有 Azure 訂用帳戶，則可以啟用 [MSDN 訂戶權益](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details)或註冊[免費帳戶](https://azure.microsoft.com/pricing/free-trial)。</span><span class="sxs-lookup"><span data-stu-id="eb308-150">If you don't already have an Azure subscription, you can activate your [MSDN subscriber benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details) or sign up for a [free account](https://azure.microsoft.com/pricing/free-trial).</span></span>

### <span data-ttu-id="eb308-151"><a name="createvnet"></a>第 1 部分：建立虛擬網路</span><span class="sxs-lookup"><span data-stu-id="eb308-151"><a name="createvnet"></a>Part 1: Create a virtual network</span></span>

<span data-ttu-id="eb308-152">如果您還沒有虛擬網路，請建立一個。</span><span class="sxs-lookup"><span data-stu-id="eb308-152">If you don't already have a virtual network, create one.</span></span> <span data-ttu-id="eb308-153">已提供螢幕擷取畫面做為範例。</span><span class="sxs-lookup"><span data-stu-id="eb308-153">Screenshots are provided as examples.</span></span> <span data-ttu-id="eb308-154">是以您自己的確定 tooreplace hello 值。</span><span class="sxs-lookup"><span data-stu-id="eb308-154">Be sure tooreplace hello values with your own.</span></span> <span data-ttu-id="eb308-155">toocreate 使用 VNet hello Azure 入口網站，使用 hello 下列步驟：</span><span class="sxs-lookup"><span data-stu-id="eb308-155">toocreate a VNet by using hello Azure portal, use hello following steps:</span></span>

1. <span data-ttu-id="eb308-156">從瀏覽器中，瀏覽 toohello [Azure 入口網站](http://portal.azure.com)且如有需要，使用您的 Azure 帳戶登入。</span><span class="sxs-lookup"><span data-stu-id="eb308-156">From a browser, navigate toohello [Azure portal](http://portal.azure.com) and, if necessary, sign in with your Azure account.</span></span>
2. <span data-ttu-id="eb308-157">按一下 [新增] 。</span><span class="sxs-lookup"><span data-stu-id="eb308-157">Click **New**.</span></span> <span data-ttu-id="eb308-158">在 hello**搜尋 hello marketplace**欄位中，輸入 虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="eb308-158">In hello **Search hello marketplace** field, type 'Virtual Network'.</span></span> <span data-ttu-id="eb308-159">找出**虛擬網路**hello 傳回從清單中，按一下 tooopen hello**虛擬網路**頁面。</span><span class="sxs-lookup"><span data-stu-id="eb308-159">Locate **Virtual Network** from hello returned list and click tooopen hello **Virtual Network** page.</span></span>

  ![搜尋虛擬網路頁面](./media/vpn-gateway-howto-point-to-site-classic-azure-portal/newvnetportal700.png)
3. <span data-ttu-id="eb308-161">Hello hello 虛擬網路 頁面上，從 hello 底端附近**選取部署模型**清單中，選取**傳統**，然後按一下**建立**。</span><span class="sxs-lookup"><span data-stu-id="eb308-161">Near hello bottom of hello Virtual Network page, from hello **Select a deployment model** list, select **Classic**, and then click **Create**.</span></span>

  ![選取部署模型](./media/vpn-gateway-howto-point-to-site-classic-azure-portal/selectmodel.png)
4. <span data-ttu-id="eb308-163">在 hello**建立虛擬網路**頁面上，設定 hello VNet 設定。</span><span class="sxs-lookup"><span data-stu-id="eb308-163">On hello **Create virtual network** page, configure hello VNet settings.</span></span> <span data-ttu-id="eb308-164">在此頁面上，您會新增您的第一個位址空間和單一子網路位址範圍。</span><span class="sxs-lookup"><span data-stu-id="eb308-164">On this page, you add your first address space and a single subnet address range.</span></span> <span data-ttu-id="eb308-165">建立 hello VNet 完畢後，您可以返回並新增其他子網路和位址空間。</span><span class="sxs-lookup"><span data-stu-id="eb308-165">After you finish creating hello VNet, you can go back and add additional subnets and address spaces.</span></span>

  ![建立虛擬網路頁面](./media/vpn-gateway-howto-point-to-site-classic-azure-portal/vnet125.png)
5. <span data-ttu-id="eb308-167">請確認該 hello**訂用帳戶**為 hello 正確。</span><span class="sxs-lookup"><span data-stu-id="eb308-167">Verify that hello **Subscription** is hello correct one.</span></span> <span data-ttu-id="eb308-168">您可以使用 [hello] 下拉式清單來變更訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="eb308-168">You can change subscriptions by using hello drop-down.</span></span>
6. <span data-ttu-id="eb308-169">按一下 [資源群組]  並選取現有的資源群組，或輸入新的資源群組名稱以建立新的資源群組。</span><span class="sxs-lookup"><span data-stu-id="eb308-169">Click **Resource group** and either select an existing resource group, or create a new one by typing a name for your new resource group.</span></span> <span data-ttu-id="eb308-170">如果您要建立新的資源群組，根據 tooyour 名稱 hello 資源群組已規劃的組態值。</span><span class="sxs-lookup"><span data-stu-id="eb308-170">If you are creating a new resource group, name hello resource group according tooyour planned configuration values.</span></span> <span data-ttu-id="eb308-171">如需資源群組的詳細資訊，請瀏覽 [Azure Resource Manager 概觀](../azure-resource-manager/resource-group-overview.md#resource-groups)。</span><span class="sxs-lookup"><span data-stu-id="eb308-171">For more information about resource groups, visit [Azure Resource Manager Overview](../azure-resource-manager/resource-group-overview.md#resource-groups).</span></span>
7. <span data-ttu-id="eb308-172">接下來，選取 hello**位置**設定您的 VNet。</span><span class="sxs-lookup"><span data-stu-id="eb308-172">Next, select hello **Location** settings for your VNet.</span></span> <span data-ttu-id="eb308-173">hello 位置會決定您將部署 toothis VNet hello 資源所在的位置。</span><span class="sxs-lookup"><span data-stu-id="eb308-173">hello location determines where hello resources that you deploy toothis VNet will reside.</span></span>
8. <span data-ttu-id="eb308-174">選取**Pin toodashboard**如果您想 toobe 無法 toofind 輕鬆 hello 儀表板上，您的 VNet，然後按一下**建立**。</span><span class="sxs-lookup"><span data-stu-id="eb308-174">Select **Pin toodashboard** if you want toobe able toofind your VNet easily on hello dashboard, and then click **Create**.</span></span>

  ![Pin toodashboard](./media/vpn-gateway-howto-point-to-site-classic-azure-portal/pintodashboard150.png)
9. <span data-ttu-id="eb308-176">按一下 [建立]，圖格就會出現儀表板上，將會反映您的 VNet hello 進度。</span><span class="sxs-lookup"><span data-stu-id="eb308-176">After clicking Create, a tile appears on your dashboard that will reflect hello progress of your VNet.</span></span> <span data-ttu-id="eb308-177">hello hello 磚變更正在建立 VNet。</span><span class="sxs-lookup"><span data-stu-id="eb308-177">hello tile changes as hello VNet is being created.</span></span>

  ![建立虛擬網路圖格](./media/vpn-gateway-howto-point-to-site-classic-azure-portal/deploying150.png)
10. <span data-ttu-id="eb308-179">一旦建立您的虛擬網路之後，您會看到**Created**底下所列**狀態**hello Azure 傳統入口網站中 hello [網路] 頁面上。</span><span class="sxs-lookup"><span data-stu-id="eb308-179">Once your virtual network has been created, you see **Created** listed under **Status** on hello networks page in hello Azure classic portal.</span></span>
11. <span data-ttu-id="eb308-180">新增 DNS 伺服器 (選擇性)。</span><span class="sxs-lookup"><span data-stu-id="eb308-180">Add a DNS server (optional).</span></span> <span data-ttu-id="eb308-181">建立虛擬網路之後，您可以加入 hello 的名稱解析的 DNS 伺服器的 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="eb308-181">After you create your virtual network, you can add hello IP address of a DNS server for name resolution.</span></span> <span data-ttu-id="eb308-182">hello 您指定的 DNS 伺服器 IP 位址應該是 hello 可解析的 VNet 中的 hello 資源 hello 名稱的 DNS 伺服器位址。</span><span class="sxs-lookup"><span data-stu-id="eb308-182">hello DNS server IP address that you specify should be hello address of a DNS server that can resolve hello names for hello resources in your VNet.</span></span><br><span data-ttu-id="eb308-183">tooadd DNS 伺服器，開啟 hello 設定虛擬網路、 按一下 DNS 伺服器，並加入您想 toouse hello DNS 伺服器 hello IP 位址。</span><span class="sxs-lookup"><span data-stu-id="eb308-183">tooadd a DNS server, open hello settings for your virtual network, click DNS servers, and add hello IP address of hello DNS server that you want toouse.</span></span>

### <span data-ttu-id="eb308-184"><a name="gateway"></a>第 2 部分：建立閘道子網路和動態路由閘道</span><span class="sxs-lookup"><span data-stu-id="eb308-184"><a name="gateway"></a>Part 2: Create gateway subnet and a dynamic routing gateway</span></span>

<span data-ttu-id="eb308-185">在此步驟中，您會建立一個閘道子網路和一個動態路由閘道。</span><span class="sxs-lookup"><span data-stu-id="eb308-185">In this step, you create a gateway subnet and a Dynamic routing gateway.</span></span> <span data-ttu-id="eb308-186">在 hello hello 傳統部署模型的 Azure 入口網站，建立 hello 閘道子網路和 hello 閘道可以透過 hello 相同組態頁面。</span><span class="sxs-lookup"><span data-stu-id="eb308-186">In hello Azure portal for hello classic deployment model, creating hello gateway subnet and hello gateway can be done through hello same configuration pages.</span></span>

1. <span data-ttu-id="eb308-187">在 hello 入口網站中，瀏覽 toohello 想 toocreate 閘道的虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="eb308-187">In hello portal, navigate toohello virtual network for which you want toocreate a gateway.</span></span>
2. <span data-ttu-id="eb308-188">Hello 頁面上的虛擬網路，在 hello**概觀**hello VPN 連線一節中的頁面上，按一下**閘道**。</span><span class="sxs-lookup"><span data-stu-id="eb308-188">On hello page for your virtual network, on hello **Overview** page, in hello VPN connections section, click **Gateway**.</span></span>

  ![按一下 toocreate 閘道](./media/vpn-gateway-howto-point-to-site-classic-azure-portal/beforegw125.png)
3. <span data-ttu-id="eb308-190">在 hello**新的 VPN 連線**頁面上，選取**點對站**。</span><span class="sxs-lookup"><span data-stu-id="eb308-190">On hello **New VPN Connection** page, select **Point-to-site**.</span></span>

  ![點對站連線類型](./media/vpn-gateway-howto-point-to-site-classic-azure-portal/newvpnconnect.png)
4. <span data-ttu-id="eb308-192">如**用戶端的位址空間**，新增 hello IP 位址範圍。</span><span class="sxs-lookup"><span data-stu-id="eb308-192">For **Client Address Space**, add hello IP address range.</span></span> <span data-ttu-id="eb308-193">這是 hello VPN 用戶端接收的 IP 位址連接時的 hello 範圍。</span><span class="sxs-lookup"><span data-stu-id="eb308-193">This is hello range from which hello VPN clients receive an IP address when connecting.</span></span> <span data-ttu-id="eb308-194">搭配 hello 在內部部署位置，您將連接，或您想要 tooconnect 的 VNet hello，請使用私用的 IP 位址範圍不會重疊。</span><span class="sxs-lookup"><span data-stu-id="eb308-194">Use a private IP address range that does not overlap with hello on-premises location that you will connect from, or with hello VNet that you want tooconnect to.</span></span> <span data-ttu-id="eb308-195">您可以刪除 hello 自動填滿範圍，然後新增 hello 私用 IP 位址範圍的 toouse。</span><span class="sxs-lookup"><span data-stu-id="eb308-195">You can delete hello auto-filled range, then add hello private IP address range that you want toouse.</span></span>

  ![用戶端位址空間](./media/vpn-gateway-howto-point-to-site-classic-azure-portal/clientaddress.png)
5. <span data-ttu-id="eb308-197">選取 hello**立即建立閘道**核取方塊。</span><span class="sxs-lookup"><span data-stu-id="eb308-197">Select hello **Create gateway immediately** checkbox.</span></span>

  ![立即建立閘道](./media/vpn-gateway-howto-point-to-site-classic-azure-portal/creategwimm.png)
6. <span data-ttu-id="eb308-199">按一下**選擇性閘道組態**tooopen hello**閘道組態**頁面。</span><span class="sxs-lookup"><span data-stu-id="eb308-199">Click **Optional gateway configuration** tooopen hello **Gateway configuration** page.</span></span>

  ![按一下選擇性閘道組態](./media/vpn-gateway-howto-point-to-site-classic-azure-portal/optsubnet125.png)
7. <span data-ttu-id="eb308-201">按一下**子網路設定必要設定**tooadd hello**閘道子網路**。</span><span class="sxs-lookup"><span data-stu-id="eb308-201">Click **Subnet Configure required settings** tooadd hello **gateway subnet**.</span></span> <span data-ttu-id="eb308-202">雖然可能 toocreate 閘道子網路為/29，我們建議您建立較大的子網路選取至少是/28 或 /27 包含多個位址。</span><span class="sxs-lookup"><span data-stu-id="eb308-202">While it is possible toocreate a gateway subnet as small as /29, we recommend that you create a larger subnet that includes more addresses by selecting at least /28 or /27.</span></span> <span data-ttu-id="eb308-203">這可讓足夠位址 tooaccommodate 可能其他組態，您可能想在 hello 未來。</span><span class="sxs-lookup"><span data-stu-id="eb308-203">This will allow for enough addresses tooaccommodate possible additional configurations that you may want in hello future.</span></span> <span data-ttu-id="eb308-204">當使用閘道子網路，避免將網路安全性 (nsg) toohello 閘道子網路產生關聯。</span><span class="sxs-lookup"><span data-stu-id="eb308-204">When working with gateway subnets, avoid associating a network security group (NSG) toohello gateway subnet.</span></span> <span data-ttu-id="eb308-205">建立關聯的網路安全性群組 toothis 子網路，可能會導致您 VPN 閘道 toostop 如預期般運作。</span><span class="sxs-lookup"><span data-stu-id="eb308-205">Associating a network security group toothis subnet may cause your VPN gateway toostop functioning as expected.</span></span>

  ![新增 GatewaySubnet](./media/vpn-gateway-howto-point-to-site-classic-azure-portal/gwsubnet125.png)
8. <span data-ttu-id="eb308-207">選取 hello 閘道**大小**。</span><span class="sxs-lookup"><span data-stu-id="eb308-207">Select hello gateway **Size**.</span></span> <span data-ttu-id="eb308-208">hello 大小為您的虛擬網路閘道的 hello 閘道 SKU。</span><span class="sxs-lookup"><span data-stu-id="eb308-208">hello size is hello gateway SKU for your virtual network gateway.</span></span> <span data-ttu-id="eb308-209">在 hello 入口網站 hello 預設 SKU 是**基本**。</span><span class="sxs-lookup"><span data-stu-id="eb308-209">In hello portal, hello Default SKU is **Basic**.</span></span> <span data-ttu-id="eb308-210">如需關於閘道 SKU 的資訊，請參閱[關於 VPN 閘道設定](vpn-gateway-about-vpn-gateway-settings.md#gwsku)。</span><span class="sxs-lookup"><span data-stu-id="eb308-210">For more information about gateway SKUs, see [About VPN Gateway Settings](vpn-gateway-about-vpn-gateway-settings.md#gwsku).</span></span>

  ![閘道大小](./media/vpn-gateway-howto-point-to-site-classic-azure-portal/gwsize125.png)
9. <span data-ttu-id="eb308-212">選取 hello**路由類型**閘道。</span><span class="sxs-lookup"><span data-stu-id="eb308-212">Select hello **Routing Type** for your gateway.</span></span> <span data-ttu-id="eb308-213">P2S 組態需要**動態**路由類型。</span><span class="sxs-lookup"><span data-stu-id="eb308-213">P2S configurations require a **Dynamic** routing type.</span></span> <span data-ttu-id="eb308-214">完成此頁面的設定時，請按一下 [確定]。</span><span class="sxs-lookup"><span data-stu-id="eb308-214">Click **OK** when you have finished configuring this page.</span></span>

  ![設定路由類型](./media/vpn-gateway-howto-point-to-site-classic-azure-portal/routingtype125.png)
10. <span data-ttu-id="eb308-216">在 hello**新的 VPN 連線**頁面上，按一下**確定**底部 hello hello 頁面 toobegin 建立虛擬網路閘道。</span><span class="sxs-lookup"><span data-stu-id="eb308-216">On hello **New VPN Connection** page, click **OK** at hello bottom of hello page toobegin creating your virtual network gateway.</span></span> <span data-ttu-id="eb308-217">VPN 閘道可能佔用 too45 分鐘 toocomplete，根據您選取的 hello 閘道 sku。</span><span class="sxs-lookup"><span data-stu-id="eb308-217">A VPN gateway can take up too45 minutes toocomplete, depending on hello gateway sku that you select.</span></span>

## <span data-ttu-id="eb308-218"><a name="generatecerts"></a>2.建立憑證</span><span class="sxs-lookup"><span data-stu-id="eb308-218"><a name="generatecerts"></a>2. Create certificates</span></span>

<span data-ttu-id="eb308-219">憑證是由 Azure tooauthenticate VPN 用戶端用於點對站 Vpn。</span><span class="sxs-lookup"><span data-stu-id="eb308-219">Certificates are used by Azure tooauthenticate VPN clients for Point-to-Site VPNs.</span></span> <span data-ttu-id="eb308-220">您上傳 hello 的公開金鑰資訊 hello 根憑證 tooAzure。</span><span class="sxs-lookup"><span data-stu-id="eb308-220">You upload hello public key information of hello root certificate tooAzure.</span></span> <span data-ttu-id="eb308-221">hello 公開金鑰則被視為 'trusted'。</span><span class="sxs-lookup"><span data-stu-id="eb308-221">hello public key is then considered 'trusted'.</span></span> <span data-ttu-id="eb308-222">用戶端憑證必須從 hello 受信任的根憑證，所產生，並安裝 hello 憑證-目前的使用者/個人憑證存放區中每個用戶端電腦上。</span><span class="sxs-lookup"><span data-stu-id="eb308-222">Client certificates must be generated from hello trusted root certificate, and then installed on each client computer in hello Certificates-Current User/Personal certificate store.</span></span> <span data-ttu-id="eb308-223">hello 憑證時，使用的 tooauthenticate hello 用戶端會起始連線 toohello VNet。</span><span class="sxs-lookup"><span data-stu-id="eb308-223">hello certificate is used tooauthenticate hello client when it initiates a connection toohello VNet.</span></span> 

<span data-ttu-id="eb308-224">如果您使用自我簽署憑證，則必須使用特定參數來建立這些憑證。</span><span class="sxs-lookup"><span data-stu-id="eb308-224">If you use self-signed certificates, they must be created using specific parameters.</span></span> <span data-ttu-id="eb308-225">您可以建立自我簽署的憑證，使用 hello 指示[PowerShell 和 Windows 10](vpn-gateway-certificates-point-to-site.md)，或[MakeCert](vpn-gateway-certificates-point-to-site-makecert.md)。</span><span class="sxs-lookup"><span data-stu-id="eb308-225">You can create a self-signed certificate using hello instructions for [PowerShell and Windows 10](vpn-gateway-certificates-point-to-site.md), or [MakeCert](vpn-gateway-certificates-point-to-site-makecert.md).</span></span> <span data-ttu-id="eb308-226">請務必使用自我簽署的根憑證，並產生用戶端憑證從 hello 自我簽署的根憑證時，請遵循這些指示中的 hello 步驟。</span><span class="sxs-lookup"><span data-stu-id="eb308-226">It's important that you follow hello steps in these instructions when working with self-signed root certificates and generating client certificates from hello self-signed root certificate.</span></span> <span data-ttu-id="eb308-227">否則，您所建立的 hello 憑證不會與 P2S 連接相容，而且您會收到連接錯誤。</span><span class="sxs-lookup"><span data-stu-id="eb308-227">Otherwise, hello certificates you create will not be compatible with P2S connections and you will receive a connection error.</span></span>

### <span data-ttu-id="eb308-228"><a name="cer"></a>第 1 部分： Hello 公開金鑰 (.cer) 取得 hello 根憑證</span><span class="sxs-lookup"><span data-stu-id="eb308-228"><a name="cer"></a>Part 1: Obtain hello public key (.cer) for hello root certificate</span></span>

[!INCLUDE [vpn-gateway-basic-vnet-rm-portal](../../includes/vpn-gateway-p2s-rootcert-include.md)]

### <span data-ttu-id="eb308-229"><a name="genclientcert"></a>第 2 部分：產生用戶端憑證</span><span class="sxs-lookup"><span data-stu-id="eb308-229"><a name="genclientcert"></a>Part 2: Generate a client certificate</span></span>

[!INCLUDE [vpn-gateway-basic-vnet-rm-portal](../../includes/vpn-gateway-p2s-clientcert-include.md)]

## <span data-ttu-id="eb308-230"><a name="upload"></a>3.Hello 根憑證.cer 檔案上傳</span><span class="sxs-lookup"><span data-stu-id="eb308-230"><a name="upload"></a>3. Upload hello root certificate .cer file</span></span>

<span data-ttu-id="eb308-231">建立 hello 閘道之後，您可以上傳 hello.cer 檔案 （其中包含 hello 公開金鑰資訊） 的受信任的根憑證 tooAzure。</span><span class="sxs-lookup"><span data-stu-id="eb308-231">After hello gateway has been created, you can upload hello .cer file (which contains hello public key information) for a trusted root certificate tooAzure.</span></span> <span data-ttu-id="eb308-232">您不是私密金鑰 hello 根憑證 tooAzure hello 的上傳。</span><span class="sxs-lookup"><span data-stu-id="eb308-232">You do not upload hello private key for hello root certificate tooAzure.</span></span> <span data-ttu-id="eb308-233">一旦上傳 a.cer 檔案時，Azure 可以使用它 tooauthenticate 安裝用戶端，已從 hello 信任的根憑證產生用戶端憑證。</span><span class="sxs-lookup"><span data-stu-id="eb308-233">Once a.cer file is uploaded, Azure can use it tooauthenticate clients that have installed a client certificate generated from hello trusted root certificate.</span></span> <span data-ttu-id="eb308-234">如有需要您可以上傳其他受信任的根憑證檔-tooa 總計 20-更新版本中，設定。</span><span class="sxs-lookup"><span data-stu-id="eb308-234">You can upload additional trusted root certificate files - up tooa total of 20 - later, if needed.</span></span>  

1. <span data-ttu-id="eb308-235">在 hello **VPN 連線**> 一節的 VNet 的 hello 頁面上，按一下 hello**用戶端**圖形 tooopen hello**點對站 VPN 連線**頁面。</span><span class="sxs-lookup"><span data-stu-id="eb308-235">On hello **VPN connections** section of hello page for your VNet, click hello **clients** graphic tooopen hello **Point-to-site VPN connection** page.</span></span>

  ![用戶端](./media/vpn-gateway-howto-point-to-site-classic-azure-portal/clients125.png)
2. <span data-ttu-id="eb308-237">在 hello**點對站連線**頁面上，按一下**管理憑證**tooopen hello**憑證**頁面。</span><span class="sxs-lookup"><span data-stu-id="eb308-237">On hello **Point-to-site connection** page, click **Manage certificates** tooopen hello **Certificates** page.</span></span><br>

  ![憑證頁面](./media/vpn-gateway-howto-point-to-site-classic-azure-portal/ptsmanage.png)<br><br>
3. <span data-ttu-id="eb308-239">在 hello**憑證**頁面上，按一下**上傳**tooopen hello**將憑證上傳**頁面。</span><span class="sxs-lookup"><span data-stu-id="eb308-239">On hello **Certificates** page, click **Upload** tooopen hello **Upload certificate** page.</span></span><br>

    ![上傳憑證頁面](./media/vpn-gateway-howto-point-to-site-classic-azure-portal/uploadcerts.png)<br>
4. <span data-ttu-id="eb308-241">按一下 hello 資料夾圖形 toobrowse hello 選擇.cer 檔案。</span><span class="sxs-lookup"><span data-stu-id="eb308-241">Click hello folder graphic toobrowse for hello .cer file.</span></span> <span data-ttu-id="eb308-242">選取 hello 檔案，然後按一下 **確定**。</span><span class="sxs-lookup"><span data-stu-id="eb308-242">Select hello file, then click **OK**.</span></span> <span data-ttu-id="eb308-243">重新整理 hello 頁面 toosee hello 上傳憑證上 hello**憑證**頁面。</span><span class="sxs-lookup"><span data-stu-id="eb308-243">Refresh hello page toosee hello uploaded certificate on hello **Certificates** page.</span></span>

  ![Upload certificate](./media/vpn-gateway-howto-point-to-site-classic-azure-portal/upload.png)<br>

## <span data-ttu-id="eb308-245"><a name="vpnclientconfig"></a>4.Hello 用戶端設定</span><span class="sxs-lookup"><span data-stu-id="eb308-245"><a name="vpnclientconfig"></a>4. Configure hello client</span></span>

<span data-ttu-id="eb308-246">tooconnect tooa 使用點對站 VPN 的 VNet，每個用戶端必須安裝封裝 tooconfigure hello 原生 Windows VPN 用戶端。</span><span class="sxs-lookup"><span data-stu-id="eb308-246">tooconnect tooa VNet using a Point-to-Site VPN, each client must install a package tooconfigure hello native Windows VPN client.</span></span> <span data-ttu-id="eb308-247">hello 組態封裝設定原生 Windows VPN 用戶端 hello 與 hello 設定必要 tooconnect toohello 虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="eb308-247">hello configuration package configures hello native Windows VPN client with hello settings necessary tooconnect toohello virtual network.</span></span>

<span data-ttu-id="eb308-248">只要 hello 版本符合 hello 用戶端 hello 架構，您可以使用相同的 VPN 用戶端組態封裝每個用戶端電腦，hello。</span><span class="sxs-lookup"><span data-stu-id="eb308-248">You can use hello same VPN client configuration package on each client computer, as long as hello version matches hello architecture for hello client.</span></span> <span data-ttu-id="eb308-249">Hello 清單中的用戶端作業系統支援，請參閱 hello[點對站連線常見問題集](#faq)hello 本文結尾處。</span><span class="sxs-lookup"><span data-stu-id="eb308-249">For hello list of client operating systems that are supported, see hello [Point-to-Site connections FAQ](#faq) at hello end of this article.</span></span>

### <span data-ttu-id="eb308-250"><a name="generateconfigpackage"></a>第 1 部分： 產生並安裝 hello VPN 用戶端組態封裝</span><span class="sxs-lookup"><span data-stu-id="eb308-250"><a name="generateconfigpackage"></a>Part 1: Generate and install hello VPN client configuration package</span></span>

1. <span data-ttu-id="eb308-251">在 hello Azure 入口網站中 hello**概觀**頁面為您的 VNet， **VPN 連線**，按一下 hello 用戶端圖形 tooopen hello**點對站 VPN 連線**頁面。</span><span class="sxs-lookup"><span data-stu-id="eb308-251">In hello Azure portal, in hello **Overview** page for your VNet, in **VPN connections**, click hello client graphic tooopen hello **Point-to-site VPN connection** page.</span></span>
2. <span data-ttu-id="eb308-252">頂端的 hello hello**點對站 VPN 連線**頁面上，按一下對應 toohello 用戶端作業系統將會安裝的 hello 下載封裝：</span><span class="sxs-lookup"><span data-stu-id="eb308-252">At hello top of hello **Point-to-site VPN connection** page, click hello download package that corresponds toohello client operating system on which it will be installed:</span></span>

  * <span data-ttu-id="eb308-253">若為 64 位元用戶端，請選取 [VPN 用戶端 (64 位元)]。</span><span class="sxs-lookup"><span data-stu-id="eb308-253">For 64-bit clients, select **VPN Client (64-bit)**.</span></span>
  * <span data-ttu-id="eb308-254">若為 32 位元用戶端，請選取 [VPN 用戶端 (32 位元)]。</span><span class="sxs-lookup"><span data-stu-id="eb308-254">For 32-bit clients, select **VPN Client (32-bit)**.</span></span>

  ![下載 VPN 用戶端組態封裝](./media/vpn-gateway-howto-point-to-site-classic-azure-portal/dlclient.png)<br>
3. <span data-ttu-id="eb308-256">一旦 hello 封裝產生，下載並安裝用戶端電腦上。</span><span class="sxs-lookup"><span data-stu-id="eb308-256">Once hello packaged generates, download and install it on your client computer.</span></span> <span data-ttu-id="eb308-257">如果您看到 SmartScreen 快顯視窗，請按一下 [更多資訊]，然後按一下 [仍要執行]。</span><span class="sxs-lookup"><span data-stu-id="eb308-257">If you see a SmartScreen popup, click **More info**, then **Run anyway**.</span></span> <span data-ttu-id="eb308-258">您也可以儲存 hello 封裝 tooinstall 其他用戶端電腦上。</span><span class="sxs-lookup"><span data-stu-id="eb308-258">You can also save hello package tooinstall on other client computers.</span></span>

### <span data-ttu-id="eb308-259"><a name="installclientcert"></a>第 2 部分： 安裝 hello 用戶端憑證</span><span class="sxs-lookup"><span data-stu-id="eb308-259"><a name="installclientcert"></a>Part 2: Install hello client certificate</span></span>

<span data-ttu-id="eb308-260">如果您想要 toocreate P2S 連線 hello 以外的用戶端電腦從您使用 toogenerate hello 用戶端憑證，您需要 tooinstall 用戶端憑證。</span><span class="sxs-lookup"><span data-stu-id="eb308-260">If you want toocreate a P2S connection from a client computer other than hello one you used toogenerate hello client certificates, you need tooinstall a client certificate.</span></span> <span data-ttu-id="eb308-261">安裝用戶端憑證，必須已建立 hello 用戶端憑證匯出時的 hello 密碼。</span><span class="sxs-lookup"><span data-stu-id="eb308-261">When installing a client certificate, you need hello password that was created when hello client certificate was exported.</span></span> <span data-ttu-id="eb308-262">一般而言，這是只需按兩下 hello 憑證並將其安裝。</span><span class="sxs-lookup"><span data-stu-id="eb308-262">Typically, this is just a matter of double-clicking hello certificate and installing it.</span></span> <span data-ttu-id="eb308-263">如需詳細資訊，請參閱[安裝匯出的用戶端憑證](vpn-gateway-certificates-point-to-site.md#install)。</span><span class="sxs-lookup"><span data-stu-id="eb308-263">For more information, see [Install an exported client certificate](vpn-gateway-certificates-point-to-site.md#install).</span></span>

## <span data-ttu-id="eb308-264"><a name="connect"></a>5.連接 tooAzure</span><span class="sxs-lookup"><span data-stu-id="eb308-264"><a name="connect"></a>5. Connect tooAzure</span></span>

### <a name="connect-tooyour-vnet"></a><span data-ttu-id="eb308-265">連接 tooyour VNet</span><span class="sxs-lookup"><span data-stu-id="eb308-265">Connect tooyour VNet</span></span>

1. <span data-ttu-id="eb308-266">tooconnect tooyour VNet，hello 用戶端電腦上，瀏覽 tooVPN 連線，並尋找您所建立的 hello VPN 連線。</span><span class="sxs-lookup"><span data-stu-id="eb308-266">tooconnect tooyour VNet, on hello client computer, navigate tooVPN connections and locate hello VPN connection that you created.</span></span> <span data-ttu-id="eb308-267">它會命名為與虛擬網路名稱相同的 hello。</span><span class="sxs-lookup"><span data-stu-id="eb308-267">It is named hello same name as your virtual network.</span></span> <span data-ttu-id="eb308-268">按一下 [ **連接**]。</span><span class="sxs-lookup"><span data-stu-id="eb308-268">Click **Connect**.</span></span> <span data-ttu-id="eb308-269">快顯視窗訊息可能會出現參考 toousing hello 憑證。</span><span class="sxs-lookup"><span data-stu-id="eb308-269">A pop-up message may appear that refers toousing hello certificate.</span></span> <span data-ttu-id="eb308-270">如果發生這種情況，請按一下**繼續**toouse 提升的權限。</span><span class="sxs-lookup"><span data-stu-id="eb308-270">If this happens, click **Continue** toouse elevated privileges.</span></span>
2. <span data-ttu-id="eb308-271">在 hello**連接**狀態] 頁面上，按一下 [**連接**toostart hello 連線。</span><span class="sxs-lookup"><span data-stu-id="eb308-271">On hello **Connection** status page, click **Connect** toostart hello connection.</span></span> <span data-ttu-id="eb308-272">如果您看到**選取憑證**畫面上，確認憑證顯示 hello 用戶端 hello 其中一個要 toouse tooconnect。</span><span class="sxs-lookup"><span data-stu-id="eb308-272">If you see a **Select Certificate** screen, verify that hello client certificate showing is hello one that you want toouse tooconnect.</span></span> <span data-ttu-id="eb308-273">如果不是，使用 hello 下拉箭號 tooselect hello 正確的憑證，，然後按一下**確定**。</span><span class="sxs-lookup"><span data-stu-id="eb308-273">If it is not, use hello drop-down arrow tooselect hello correct certificate, and then click **OK**.</span></span>

  ![VPN 用戶端連線](./media/vpn-gateway-howto-point-to-site-classic-azure-portal/clientconnect.png)
3. <span data-ttu-id="eb308-275">已建立您的連線。</span><span class="sxs-lookup"><span data-stu-id="eb308-275">Your connection is established.</span></span>

  ![建立的連線](./media/vpn-gateway-howto-point-to-site-classic-azure-portal/connected.png)

#### <a name="troubleshooting-p2s-connections"></a><span data-ttu-id="eb308-277">針對 P2S 連線進行疑難排解</span><span class="sxs-lookup"><span data-stu-id="eb308-277">Troubleshooting P2S connections</span></span>

[!INCLUDE [verify-client-certificates](../../includes/vpn-gateway-certificates-verify-client-cert-include.md)]

### <span data-ttu-id="eb308-278"><a name="verifyvpnconnect"></a>確認 hello VPN 連線</span><span class="sxs-lookup"><span data-stu-id="eb308-278"><a name="verifyvpnconnect"></a>Verify hello VPN connection</span></span>

1. <span data-ttu-id="eb308-279">tooverify VPN 連線為作用中，開啟提升權限的命令提示字元並執行*ipconfig/all*。</span><span class="sxs-lookup"><span data-stu-id="eb308-279">tooverify that your VPN connection is active, open an elevated command prompt, and run *ipconfig/all*.</span></span>
2. <span data-ttu-id="eb308-280">檢視 hello 結果。</span><span class="sxs-lookup"><span data-stu-id="eb308-280">View hello results.</span></span> <span data-ttu-id="eb308-281">請注意，您收到 hello IP 位址的其中一個，指定您在建立 VNet 時 hello 點對站連線位址範圍內的 hello 位址。</span><span class="sxs-lookup"><span data-stu-id="eb308-281">Notice that hello IP address you received is one of hello addresses within hello Point-to-Site connectivity address range that you specified when you created your VNet.</span></span> <span data-ttu-id="eb308-282">hello 結果應該類似 toothis 範例：</span><span class="sxs-lookup"><span data-stu-id="eb308-282">hello results should be similar toothis example:</span></span>

  ```
    PPP adapter VNet1:
        Connection-specific DNS Suffix .:
        Description.....................: VNet1
        Physical Address................:
        DHCP Enabled....................: No
        Autoconfiguration Enabled.......: Yes
        IPv4 Address....................: 192.168.130.2(Preferred)
        Subnet Mask.....................: 255.255.255.255
        Default Gateway.................:
        NetBIOS over Tcpip..............: Enabled
  ```

## <span data-ttu-id="eb308-283"><a name="connectVM"></a>Tooa 虛擬機器連線</span><span class="sxs-lookup"><span data-stu-id="eb308-283"><a name="connectVM"></a>Connect tooa virtual machine</span></span>

[!INCLUDE [Connect tooa VM](../../includes/vpn-gateway-connect-vm-p2s-classic-include.md)]

## <span data-ttu-id="eb308-284"><a name="add"></a>新增或移除受信任的根憑證</span><span class="sxs-lookup"><span data-stu-id="eb308-284"><a name="add"></a>Add or remove trusted root certificates</span></span>

<span data-ttu-id="eb308-285">您可以從 Azure 新增和移除受信任的根憑證。</span><span class="sxs-lookup"><span data-stu-id="eb308-285">You can add and remove trusted root certificates from Azure.</span></span> <span data-ttu-id="eb308-286">當您移除的根憑證時，產生從該根憑證的用戶端將不會無法 tooauthenticate，而且不會因此無法 tooconnect。</span><span class="sxs-lookup"><span data-stu-id="eb308-286">When you remove a root certificate, clients that have a certificate generated from that root won't be able tooauthenticate, and thus will not be able tooconnect.</span></span> <span data-ttu-id="eb308-287">如果您想用戶端 tooauthenticate 連接時，您會需要的 tooinstall 從受信任的 （上傳） tooAzure 的根憑證產生新的用戶端憑證。</span><span class="sxs-lookup"><span data-stu-id="eb308-287">If you want a client tooauthenticate and connect, you need tooinstall a new client certificate generated from a root certificate that is trusted (uploaded) tooAzure.</span></span>

### <span data-ttu-id="eb308-288"><a name="addtrustedroot"></a>tooadd 信任的根憑證</span><span class="sxs-lookup"><span data-stu-id="eb308-288"><a name="addtrustedroot"></a>tooadd a trusted root certificate</span></span>

<span data-ttu-id="eb308-289">您可以加總 too20 受信任的根憑證.cer 檔案 tooAzure。</span><span class="sxs-lookup"><span data-stu-id="eb308-289">You can add up too20 trusted root certificate .cer files tooAzure.</span></span> <span data-ttu-id="eb308-290">如需指示，請參閱[區段 3-上傳 hello 根憑證.cer 檔案](#upload)。</span><span class="sxs-lookup"><span data-stu-id="eb308-290">For instructions, see [Section 3 - Upload hello root certificate .cer file](#upload).</span></span>

### <span data-ttu-id="eb308-291"><a name="removetrustedroot"></a>tooremove 信任的根憑證</span><span class="sxs-lookup"><span data-stu-id="eb308-291"><a name="removetrustedroot"></a>tooremove a trusted root certificate</span></span>

1. <span data-ttu-id="eb308-292">在 hello **VPN 連線**> 一節的 VNet 的 hello 頁面上，按一下 hello**用戶端**圖形 tooopen hello**點對站 VPN 連線**頁面。</span><span class="sxs-lookup"><span data-stu-id="eb308-292">On hello **VPN connections** section of hello page for your VNet, click hello **clients** graphic tooopen hello **Point-to-site VPN connection** page.</span></span>

  ![用戶端](./media/vpn-gateway-howto-point-to-site-classic-azure-portal/clients125.png)
2. <span data-ttu-id="eb308-294">在 hello**點對站連線**頁面上，按一下**管理憑證**tooopen hello**憑證**頁面。</span><span class="sxs-lookup"><span data-stu-id="eb308-294">On hello **Point-to-site connection** page, click **Manage certificates** tooopen hello **Certificates** page.</span></span><br>

  ![憑證頁面](./media/vpn-gateway-howto-point-to-site-classic-azure-portal/ptsmanage.png)<br><br>
3. <span data-ttu-id="eb308-296">在 hello**憑證**頁面上，按一下 hello 省略符號 下一步 toohello 憑證您想 tooremove，然後按一下**刪除**。</span><span class="sxs-lookup"><span data-stu-id="eb308-296">On hello **Certificates** page, click hello ellipsis next toohello certificate that you want tooremove, then click **Delete**.</span></span>

  ![刪除根憑證](./media/vpn-gateway-howto-point-to-site-classic-azure-portal/deleteroot.png)<br>

## <span data-ttu-id="eb308-298"><a name="revokeclient"></a>撤銷用戶端憑證</span><span class="sxs-lookup"><span data-stu-id="eb308-298"><a name="revokeclient"></a>Revoke a client certificate</span></span>

<span data-ttu-id="eb308-299">您可以撤銷用戶端憑證。</span><span class="sxs-lookup"><span data-stu-id="eb308-299">You can revoke client certificates.</span></span> <span data-ttu-id="eb308-300">hello 憑證撤銷清單可讓您 tooselectively 拒絕個別用戶端憑證為基礎的點對站連線。</span><span class="sxs-lookup"><span data-stu-id="eb308-300">hello certificate revocation list allows you tooselectively deny Point-to-Site connectivity based on individual client certificates.</span></span> <span data-ttu-id="eb308-301">這不同於移除受信任的根憑證。</span><span class="sxs-lookup"><span data-stu-id="eb308-301">This differs from removing a trusted root certificate.</span></span> <span data-ttu-id="eb308-302">如果您從 Azure 移除受信任的根憑證.cer，它就會撤銷所有用戶端憑證產生/簽署由 hello 撤銷的根憑證的 hello 存取權。</span><span class="sxs-lookup"><span data-stu-id="eb308-302">If you remove a trusted root certificate .cer from Azure, it revokes hello access for all client certificates generated/signed by hello revoked root certificate.</span></span> <span data-ttu-id="eb308-303">撤銷用戶端憑證，而不是 hello 根憑證，可讓 hello 產生從 hello 根憑證 toocontinue toobe 用於 hello 點對站連線的驗證其他憑證。</span><span class="sxs-lookup"><span data-stu-id="eb308-303">Revoking a client certificate, rather than hello root certificate, allows hello other certificates that were generated from hello root certificate toocontinue toobe used for authentication for hello Point-to-Site connection.</span></span>

<span data-ttu-id="eb308-304">hello 常見的作法是 toouse hello 根憑證 toomanage 存取小組或組織層級時使用已撤銷用戶端憑證來進行個別使用者的更細緻的存取控制。</span><span class="sxs-lookup"><span data-stu-id="eb308-304">hello common practice is toouse hello root certificate toomanage access at team or organization levels, while using revoked client certificates for fine-grained access control on individual users.</span></span>

### <span data-ttu-id="eb308-305"><a name="revokeclientcert"></a>toorevoke 用戶端憑證</span><span class="sxs-lookup"><span data-stu-id="eb308-305"><a name="revokeclientcert"></a>toorevoke a client certificate</span></span>

<span data-ttu-id="eb308-306">您可以藉由新增 hello 指紋 toohello 撤銷清單來撤銷用戶端憑證。</span><span class="sxs-lookup"><span data-stu-id="eb308-306">You can revoke a client certificate by adding hello thumbprint toohello revocation list.</span></span>

1. <span data-ttu-id="eb308-307">擷取 hello 用戶端憑證指紋。</span><span class="sxs-lookup"><span data-stu-id="eb308-307">Retrieve hello client certificate thumbprint.</span></span> <span data-ttu-id="eb308-308">如需詳細資訊，請參閱[How to： 擷取 hello 憑證的指紋](https://msdn.microsoft.com/library/ms734695.aspx)。</span><span class="sxs-lookup"><span data-stu-id="eb308-308">For more information, see [How to: Retrieve hello Thumbprint of a Certificate](https://msdn.microsoft.com/library/ms734695.aspx).</span></span>
2. <span data-ttu-id="eb308-309">複製 hello 資訊 tooa 文字編輯器，並移除所有的空間，使其連續的字串。</span><span class="sxs-lookup"><span data-stu-id="eb308-309">Copy hello information tooa text editor and remove all spaces so that it is a continuous string.</span></span>
3. <span data-ttu-id="eb308-310">瀏覽 toohello **'傳統虛擬網路名稱' > 點對站 VPN 連線 > 憑證**頁面，然後按一下**撤銷清單**tooopen hello 撤銷清單 頁面。</span><span class="sxs-lookup"><span data-stu-id="eb308-310">Navigate toohello **'classic virtual network name' > Point-to-site VPN connection > Certificates** page and then click **Revocation list** tooopen hello Revocation list page.</span></span> 
4. <span data-ttu-id="eb308-311">在 hello**撤銷清單**頁面上，按一下**+ 加入憑證**tooopen hello**新增憑證 toorevocation 清單**頁面。</span><span class="sxs-lookup"><span data-stu-id="eb308-311">On hello **Revocation list** page, click **+Add certificate** tooopen hello **Add certificate toorevocation list** page.</span></span>
5. <span data-ttu-id="eb308-312">在 hello**新增憑證 toorevocation 清單**頁面中，貼上為連續一行文字，不含空格的 hello 憑證指紋。</span><span class="sxs-lookup"><span data-stu-id="eb308-312">On hello **Add certificate toorevocation list** page, paste hello certificate thumbprint as one continuous line of text, with no spaces.</span></span> <span data-ttu-id="eb308-313">按一下**確定**hello hello 頁底端。</span><span class="sxs-lookup"><span data-stu-id="eb308-313">Click **OK** at hello bottom of hello page.</span></span>
6. <span data-ttu-id="eb308-314">更新完成後，hello 憑證不再可以使用的 tooconnect。</span><span class="sxs-lookup"><span data-stu-id="eb308-314">After updating has completed, hello certificate can no longer be used tooconnect.</span></span> <span data-ttu-id="eb308-315">使用此憑證的 tooconnect 再試一次的用戶端收到訊息，指出該 hello 憑證不再有效。</span><span class="sxs-lookup"><span data-stu-id="eb308-315">Clients that try tooconnect using this certificate receive a message saying that hello certificate is no longer valid.</span></span>

## <span data-ttu-id="eb308-316"><a name="faq"></a>點對站常見問題集</span><span class="sxs-lookup"><span data-stu-id="eb308-316"><a name="faq"></a>Point-to-Site FAQ</span></span>

[!INCLUDE [Point-to-Site FAQ](../../includes/vpn-gateway-point-to-site-faq-include.md)]

## <a name="next-steps"></a><span data-ttu-id="eb308-317">後續步驟</span><span class="sxs-lookup"><span data-stu-id="eb308-317">Next steps</span></span>
<span data-ttu-id="eb308-318">一旦完成您的連線，您可以將虛擬機器 tooyour 虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="eb308-318">Once your connection is complete, you can add virtual machines tooyour virtual networks.</span></span> <span data-ttu-id="eb308-319">如需詳細資訊，請參閱[虛擬機器](https://docs.microsoft.com/azure/#pivot=services&panel=Compute)。</span><span class="sxs-lookup"><span data-stu-id="eb308-319">For more information, see [Virtual Machines](https://docs.microsoft.com/azure/#pivot=services&panel=Compute).</span></span> <span data-ttu-id="eb308-320">toounderstand 深入了解網路和虛擬機器，請參閱[Azure 與 Linux VM 網路概觀](../virtual-machines/linux/azure-vm-network-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="eb308-320">toounderstand more about networking and virtual machines, see [Azure and Linux VM network overview](../virtual-machines/linux/azure-vm-network-overview.md).</span></span>
