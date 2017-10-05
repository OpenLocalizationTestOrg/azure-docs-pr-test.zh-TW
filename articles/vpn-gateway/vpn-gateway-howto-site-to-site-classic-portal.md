---
title: "將內部部署網路連接至 Azure 虛擬網路：站對站 VPN (傳統)：入口網站 | Microsoft Docs"
description: "透過公用網際網路建立從內部部署網路至 Azure 虛擬網路之 IPsec 連線的步驟。 這些步驟可協助您使用入口網站建立跨單位的站對站 VPN 閘道連線。"
services: vpn-gateway
documentationcenter: na
author: cherylmc
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: 
ms.service: vpn-gateway
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/010/2017
ms.author: cherylmc
ms.openlocfilehash: 0be8dd6d90edb7b32b6777c76c9778cda0dcd5ea
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/18/2017
---
# <a name="create-a-site-to-site-connection-using-the-azure-portal-classic"></a><span data-ttu-id="4d6c8-104">使用 Azure 入口網站建立站對站連線 (傳統)</span><span class="sxs-lookup"><span data-stu-id="4d6c8-104">Create a Site-to-Site connection using the Azure portal (classic)</span></span>

[!INCLUDE [deployment models](../../includes/vpn-gateway-classic-deployment-model-include.md)]

<span data-ttu-id="4d6c8-105">本文說明如何使用 Azure 入口網站來建立從內部部署網路到 VNet 的站對站 VPN 閘道連線。</span><span class="sxs-lookup"><span data-stu-id="4d6c8-105">This article shows you how to use the Azure portal to create a Site-to-Site VPN gateway connection from your on-premises network to the VNet.</span></span> <span data-ttu-id="4d6c8-106">本文中的步驟適用於傳統部署模型。</span><span class="sxs-lookup"><span data-stu-id="4d6c8-106">The steps in this article apply to the classic deployment model.</span></span> <span data-ttu-id="4d6c8-107">您也可從下列清單中選取不同的選項，以使用不同的部署工具或部署模型來建立此組態：</span><span class="sxs-lookup"><span data-stu-id="4d6c8-107">You can also create this configuration using a different deployment tool or deployment model by selecting a different option from the following list:</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="4d6c8-108">Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="4d6c8-108">Azure portal</span></span>](vpn-gateway-howto-site-to-site-resource-manager-portal.md)
> * [<span data-ttu-id="4d6c8-109">PowerShell</span><span class="sxs-lookup"><span data-stu-id="4d6c8-109">PowerShell</span></span>](vpn-gateway-create-site-to-site-rm-powershell.md)
> * [<span data-ttu-id="4d6c8-110">CLI</span><span class="sxs-lookup"><span data-stu-id="4d6c8-110">CLI</span></span>](vpn-gateway-howto-site-to-site-resource-manager-cli.md)
> * [<span data-ttu-id="4d6c8-111">Azure 入口網站 (傳統)</span><span class="sxs-lookup"><span data-stu-id="4d6c8-111">Azure portal (classic)</span></span>](vpn-gateway-howto-site-to-site-classic-portal.md)
> 
>

<span data-ttu-id="4d6c8-112">站對站 VPN 閘道連線可用來透過 IPsec/IKE (IKEv1 或 IKEv2) VPN 通道，將內部部署網路連線到 Azure 虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="4d6c8-112">A Site-to-Site VPN gateway connection is used to connect your on-premises network to an Azure virtual network over an IPsec/IKE (IKEv1 or IKEv2) VPN tunnel.</span></span> <span data-ttu-id="4d6c8-113">此類型的連線需要位於內部部署的 VPN 裝置，且您已對該裝置指派對外開放的公用 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="4d6c8-113">This type of connection requires a VPN device located on-premises that has an externally facing public IP address assigned to it.</span></span> <span data-ttu-id="4d6c8-114">如需 VPN 閘道的詳細資訊，請參閱[關於 VPN 閘道](vpn-gateway-about-vpngateways.md)。</span><span class="sxs-lookup"><span data-stu-id="4d6c8-114">For more information about VPN gateways, see [About VPN gateway](vpn-gateway-about-vpngateways.md).</span></span>

![站對站 VPN 閘道跨單位連線圖表](./media/vpn-gateway-howto-site-to-site-classic-portal/site-to-site-diagram.png)

## <a name="before-you-begin"></a><span data-ttu-id="4d6c8-116">開始之前</span><span class="sxs-lookup"><span data-stu-id="4d6c8-116">Before you begin</span></span>

<span data-ttu-id="4d6c8-117">在開始設定之前，請確認您已符合下列條件：</span><span class="sxs-lookup"><span data-stu-id="4d6c8-117">Verify that you have met the following criteria before beginning configuration:</span></span>

* <span data-ttu-id="4d6c8-118">確認您想要使用傳統部署模型。</span><span class="sxs-lookup"><span data-stu-id="4d6c8-118">Verify that you want to work in the classic deployment model.</span></span> <span data-ttu-id="4d6c8-119">如果您想要使用 Resource Manager 部署模型，請參閱[建立站對站連線 (Resource Manager)](vpn-gateway-howto-site-to-site-resource-manager-portal.md)。</span><span class="sxs-lookup"><span data-stu-id="4d6c8-119">If you want to work in the Resource Manager deployment model, see [Create a Site-to-Site connection (Resource Manager)](vpn-gateway-howto-site-to-site-resource-manager-portal.md).</span></span> <span data-ttu-id="4d6c8-120">可能的話，建議使用 Azure Resource Manager 部署模型。</span><span class="sxs-lookup"><span data-stu-id="4d6c8-120">When possible, we recommend that you use the Resource Manager deployment model.</span></span>
* <span data-ttu-id="4d6c8-121">確定您有相容的 VPN 裝置以及能夠對其進行設定的人員。</span><span class="sxs-lookup"><span data-stu-id="4d6c8-121">Make sure you have a compatible VPN device and someone who is able to configure it.</span></span> <span data-ttu-id="4d6c8-122">如需相容 VPN 裝置和裝置組態的詳細資訊，請參閱[關於 VPN 裝置](vpn-gateway-about-vpn-devices.md)。</span><span class="sxs-lookup"><span data-stu-id="4d6c8-122">For more information about compatible VPN devices and device configuration, see [About VPN Devices](vpn-gateway-about-vpn-devices.md).</span></span>
* <span data-ttu-id="4d6c8-123">確認您的 VPN 裝置有對外開放的公用 IPv4 位址。</span><span class="sxs-lookup"><span data-stu-id="4d6c8-123">Verify that you have an externally facing public IPv4 address for your VPN device.</span></span> <span data-ttu-id="4d6c8-124">此 IP 位址不能位於 NAT 後方。</span><span class="sxs-lookup"><span data-stu-id="4d6c8-124">This IP address cannot be located behind a NAT.</span></span>
* <span data-ttu-id="4d6c8-125">如果您不熟悉位於內部部署網路組態的 IP 位址範圍，您需要與能夠提供那些詳細資料的人協調。</span><span class="sxs-lookup"><span data-stu-id="4d6c8-125">If you are unfamiliar with the IP address ranges located in your on-premises network configuration, you need to coordinate with someone who can provide those details for you.</span></span> <span data-ttu-id="4d6c8-126">當您建立此組態時，您必須指定 IP 位址範圍的首碼，以供 Azure 路由傳送至您的內部部署位置。</span><span class="sxs-lookup"><span data-stu-id="4d6c8-126">When you create this configuration, you must specify the IP address range prefixes that Azure will route to your on-premises location.</span></span> <span data-ttu-id="4d6c8-127">內部部署網路的子網路皆不得與您所要連線的虛擬網路子網路重疊。</span><span class="sxs-lookup"><span data-stu-id="4d6c8-127">None of the subnets of your on-premises network can over lap with the virtual network subnets that you want to connect to.</span></span>
* <span data-ttu-id="4d6c8-128">目前需要 PowerShell，才能指定共用金鑰及建立 VPN 閘道連線。</span><span class="sxs-lookup"><span data-stu-id="4d6c8-128">Currently, PowerShell is required to specify the shared key and create the VPN gateway connection.</span></span> <span data-ttu-id="4d6c8-129">安裝最新版的 Azure 服務管理 (SM) PowerShell Cmdlet。</span><span class="sxs-lookup"><span data-stu-id="4d6c8-129">Install the latest version of the Azure Service Management (SM) PowerShell cmdlets.</span></span> <span data-ttu-id="4d6c8-130">如需詳細資訊，請參閱 [如何安裝和設定 Azure PowerShell](/powershell/azure/overview)。</span><span class="sxs-lookup"><span data-stu-id="4d6c8-130">For more information, see [How to install and configure Azure PowerShell](/powershell/azure/overview).</span></span> <span data-ttu-id="4d6c8-131">使用 PowerShell 進行這項設定時，請確定您是以系統管理員身分執行。</span><span class="sxs-lookup"><span data-stu-id="4d6c8-131">When working with PowerShell for this configuration, make sure that you are running as administrator.</span></span> 

### <span data-ttu-id="4d6c8-132"><a name="values"></a>此練習的範例組態值</span><span class="sxs-lookup"><span data-stu-id="4d6c8-132"><a name="values"></a>Sample configuration values for this exercise</span></span>

<span data-ttu-id="4d6c8-133">本文的範例使用下列值。</span><span class="sxs-lookup"><span data-stu-id="4d6c8-133">The examples in this article use the following values.</span></span> <span data-ttu-id="4d6c8-134">您可以使用這些值來建立測試環境，或參考這些值，進一步了解本文中的範例。</span><span class="sxs-lookup"><span data-stu-id="4d6c8-134">You can use these values to create a test environment, or refer to them to better understand the examples in this article.</span></span>

* <span data-ttu-id="4d6c8-135">**VNet 名稱︰**TestVNet1</span><span class="sxs-lookup"><span data-stu-id="4d6c8-135">**VNet Name:** TestVNet1</span></span>
* <span data-ttu-id="4d6c8-136">**位址空間：**</span><span class="sxs-lookup"><span data-stu-id="4d6c8-136">**Address Space:**</span></span> 
  * <span data-ttu-id="4d6c8-137">10.11.0.0/16</span><span class="sxs-lookup"><span data-stu-id="4d6c8-137">10.11.0.0/16</span></span>
  * <span data-ttu-id="4d6c8-138">10.12.0.0/16 (對此練習是選擇性的)</span><span class="sxs-lookup"><span data-stu-id="4d6c8-138">10.12.0.0/16 (optional for this exercise)</span></span>
* <span data-ttu-id="4d6c8-139">**子網路：**</span><span class="sxs-lookup"><span data-stu-id="4d6c8-139">**Subnets:**</span></span>
  * <span data-ttu-id="4d6c8-140">FrontEnd：10.11.0.0/24</span><span class="sxs-lookup"><span data-stu-id="4d6c8-140">FrontEnd: 10.11.0.0/24</span></span>
  * <span data-ttu-id="4d6c8-141">BackEnd：10.12.0.0/24 (對此練習是選擇性的)</span><span class="sxs-lookup"><span data-stu-id="4d6c8-141">BackEnd: 10.12.0.0/24 (optional for this exercise)</span></span>
* <span data-ttu-id="4d6c8-142">**GatewaySubnet：**10.11.255.0/27</span><span class="sxs-lookup"><span data-stu-id="4d6c8-142">**GatewaySubnet:** 10.11.255.0/27</span></span>
* <span data-ttu-id="4d6c8-143">**資源群組︰**TestRG1</span><span class="sxs-lookup"><span data-stu-id="4d6c8-143">**Resource Group:** TestRG1</span></span>
* <span data-ttu-id="4d6c8-144">**位置：**美國東部</span><span class="sxs-lookup"><span data-stu-id="4d6c8-144">**Location:** East US</span></span>
* <span data-ttu-id="4d6c8-145">**DNS 伺服器：** 10.11.0.3 (對此練習是選擇性的)</span><span class="sxs-lookup"><span data-stu-id="4d6c8-145">**DNS Server:** 10.11.0.3 (optional for this exercise)</span></span>
* <span data-ttu-id="4d6c8-146">**本機網站名稱︰** Site2</span><span class="sxs-lookup"><span data-stu-id="4d6c8-146">**Local site name:** Site2</span></span>
* <span data-ttu-id="4d6c8-147">**用戶端位址空間：**位於內部部署網站上的位址空間。</span><span class="sxs-lookup"><span data-stu-id="4d6c8-147">**Client address space:** The address space that is located on your on-premises site.</span></span>

## <span data-ttu-id="4d6c8-148"><a name="CreatVNet"></a>1.建立虛擬網路</span><span class="sxs-lookup"><span data-stu-id="4d6c8-148"><a name="CreatVNet"></a>1. Create a virtual network</span></span>

<span data-ttu-id="4d6c8-149">當您建立要用於 S2S 連線的虛擬網路時，您必須確定您指定的位址空間，不會與您要連接之本機網站的任何用戶端位址空間重疊。</span><span class="sxs-lookup"><span data-stu-id="4d6c8-149">When you create a virtual network to use for a S2S connection, you need to make sure that the address spaces that you specify do not overlap with any of the client address spaces for the local sites that you want to connect to.</span></span> <span data-ttu-id="4d6c8-150">如果有重疊的子網路，您的連線便無法正常運作。</span><span class="sxs-lookup"><span data-stu-id="4d6c8-150">If you have overlapping subnets, your connection won't work properly.</span></span>

* <span data-ttu-id="4d6c8-151">如果您已經有 VNet，請驗證設定是否與您的 VPN 閘道設計相容。</span><span class="sxs-lookup"><span data-stu-id="4d6c8-151">If you already have a VNet, verify that the settings are compatible with your VPN gateway design.</span></span> <span data-ttu-id="4d6c8-152">請特別注意任何可能與其他網路重疊的子網路。</span><span class="sxs-lookup"><span data-stu-id="4d6c8-152">Pay particular attention to any subnets that may overlap with other networks.</span></span> 

* <span data-ttu-id="4d6c8-153">如果您還沒有虛擬網路，請建立一個。</span><span class="sxs-lookup"><span data-stu-id="4d6c8-153">If you don't already have a virtual network, create one.</span></span> <span data-ttu-id="4d6c8-154">已提供螢幕擷取畫面做為範例。</span><span class="sxs-lookup"><span data-stu-id="4d6c8-154">Screenshots are provided as examples.</span></span> <span data-ttu-id="4d6c8-155">請務必將值取代為您自己的值。</span><span class="sxs-lookup"><span data-stu-id="4d6c8-155">Be sure to replace the values with your own.</span></span>

### <a name="to-create-a-virtual-network"></a><span data-ttu-id="4d6c8-156">建立虛擬網路</span><span class="sxs-lookup"><span data-stu-id="4d6c8-156">To create a virtual network</span></span>

1. <span data-ttu-id="4d6c8-157">透過瀏覽器瀏覽至 [Azure 入口網站](http://portal.azure.com) ，並視需要使用您的 Azure 帳戶登入。</span><span class="sxs-lookup"><span data-stu-id="4d6c8-157">From a browser, navigate to the [Azure portal](http://portal.azure.com) and, if necessary, sign in with your Azure account.</span></span>
2. <span data-ttu-id="4d6c8-158">按一下頁面底部的 [新增] **+**來單一登入應用程式。</span><span class="sxs-lookup"><span data-stu-id="4d6c8-158">Click **+**.</span></span> <span data-ttu-id="4d6c8-159">在 [搜尋 Marketplace] 欄位中，輸入「虛擬網路」。</span><span class="sxs-lookup"><span data-stu-id="4d6c8-159">In the **Search the marketplace** field, type 'Virtual Network'.</span></span> <span data-ttu-id="4d6c8-160">在傳回的清單中找到 [虛擬網路]，並按一下以開啟 [虛擬網路] 頁面。</span><span class="sxs-lookup"><span data-stu-id="4d6c8-160">Locate **Virtual Network** from the returned list and click to open the **Virtual Network** page.</span></span>

  ![搜尋虛擬網路頁面](./media/vpn-gateway-howto-site-to-site-classic-portal/newvnetportal700.png)
3. <span data-ttu-id="4d6c8-162">從接近 [虛擬網路] 頁面底部的 [選取部署模型] 下拉式清單中，選取 [傳統]，然後按一下 [建立]。</span><span class="sxs-lookup"><span data-stu-id="4d6c8-162">Near the bottom of the Virtual Network page, from the **Select a deployment model** dropdown list, select **Classic**, and then click **Create**.</span></span>

  ![選取部署模型](./media/vpn-gateway-howto-site-to-site-classic-portal/selectmodel.png)
4. <span data-ttu-id="4d6c8-164">在 [建立虛擬網路 (傳統)] 頁面上進行 VNet 設定。</span><span class="sxs-lookup"><span data-stu-id="4d6c8-164">On the **Create virtual network(classic)** page, configure the VNet settings.</span></span> <span data-ttu-id="4d6c8-165">在此頁面上，您會新增您的第一個位址空間和單一子網路位址範圍。</span><span class="sxs-lookup"><span data-stu-id="4d6c8-165">On this page, you add your first address space and a single subnet address range.</span></span> <span data-ttu-id="4d6c8-166">完成 VNet 建立之後，您可以返回並新增其他子網路和位址空間。</span><span class="sxs-lookup"><span data-stu-id="4d6c8-166">After you finish creating the VNet, you can go back and add additional subnets and address spaces.</span></span>

  <span data-ttu-id="4d6c8-167">![建立虛擬網路頁面](./media/vpn-gateway-howto-site-to-site-classic-portal/createvnet.png "建立虛擬網路頁面")</span><span class="sxs-lookup"><span data-stu-id="4d6c8-167">![Create virtual network page](./media/vpn-gateway-howto-site-to-site-classic-portal/createvnet.png "Create virtual network page")</span></span>
5. <span data-ttu-id="4d6c8-168">確認 [訂用帳戶]  正確無誤。</span><span class="sxs-lookup"><span data-stu-id="4d6c8-168">Verify that the **Subscription** is the correct one.</span></span> <span data-ttu-id="4d6c8-169">您可以使用下拉式清單變更訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="4d6c8-169">You can change subscriptions by using the drop-down.</span></span>
6. <span data-ttu-id="4d6c8-170">按一下 [資源群組] 並選取現有的資源群組，或輸入名稱以建立新的資源群組。</span><span class="sxs-lookup"><span data-stu-id="4d6c8-170">Click **Resource group** and either select an existing resource group, or create a new one by typing a name.</span></span> <span data-ttu-id="4d6c8-171">如需資源群組的詳細資訊，請瀏覽 [Azure Resource Manager 概觀](../azure-resource-manager/resource-group-overview.md#resource-groups)。</span><span class="sxs-lookup"><span data-stu-id="4d6c8-171">For more information about resource groups, visit [Azure Resource Manager Overview](../azure-resource-manager/resource-group-overview.md#resource-groups).</span></span>
7. <span data-ttu-id="4d6c8-172">接著，選取 VNet 的 [位置]  設定。</span><span class="sxs-lookup"><span data-stu-id="4d6c8-172">Next, select the **Location** settings for your VNet.</span></span> <span data-ttu-id="4d6c8-173">此位置會決定您部署到此 VNet 之資源所在的位置。</span><span class="sxs-lookup"><span data-stu-id="4d6c8-173">The location determines where the resources that you deploy to this VNet will reside.</span></span>
8. <span data-ttu-id="4d6c8-174">如果想要在儀表板上輕鬆地尋找 VNet，請選取 [釘選到儀表板]。</span><span class="sxs-lookup"><span data-stu-id="4d6c8-174">If you want to be able to find your VNet easily on the dashboard, select **Pin to dashboard**.</span></span> <span data-ttu-id="4d6c8-175">按一下 [建立] 以建立 VNet。</span><span class="sxs-lookup"><span data-stu-id="4d6c8-175">Click **Create** to create your VNet.</span></span>

  <span data-ttu-id="4d6c8-176">![釘選到儀表板](./media/vpn-gateway-howto-site-to-site-classic-portal/pintodashboard150.png "釘選到儀表板")</span><span class="sxs-lookup"><span data-stu-id="4d6c8-176">![Pin to dashboard](./media/vpn-gateway-howto-site-to-site-classic-portal/pintodashboard150.png "Pin to dashboard")</span></span>
9. <span data-ttu-id="4d6c8-177">按一下 [建立] 之後，儀表板上會出現一個反映 VNet 進度的圖格。</span><span class="sxs-lookup"><span data-stu-id="4d6c8-177">After clicking 'Create', a tile appears on the dashboard that reflects the progress of your VNet.</span></span> <span data-ttu-id="4d6c8-178">建立 VNet 時，此圖格會變更。</span><span class="sxs-lookup"><span data-stu-id="4d6c8-178">The tile changes as the VNet is being created.</span></span>

  <span data-ttu-id="4d6c8-179">![建立虛擬網路圖格](./media/vpn-gateway-howto-point-to-site-classic-azure-portal/deploying150.png "建立虛擬網路")</span><span class="sxs-lookup"><span data-stu-id="4d6c8-179">![Creating virtual network tile](./media/vpn-gateway-howto-point-to-site-classic-azure-portal/deploying150.png "Creating virtual network")</span></span>

<span data-ttu-id="4d6c8-180">一旦建立虛擬網路，您可在 Azure 傳統入口網站的網路頁面上看見 [狀態] 下列出 [已建立]。</span><span class="sxs-lookup"><span data-stu-id="4d6c8-180">Once your virtual network is created, you see **Created** listed under **Status** on the networks page in the Azure classic portal.</span></span>

## <span data-ttu-id="4d6c8-181"><a name="additionaladdress"></a>2.新增其他位址空間</span><span class="sxs-lookup"><span data-stu-id="4d6c8-181"><a name="additionaladdress"></a>2. Add additional address space</span></span>

<span data-ttu-id="4d6c8-182">建立虛擬網路之後，您可以新增其他位址空間。</span><span class="sxs-lookup"><span data-stu-id="4d6c8-182">After you create your virtual network, you can add additional address space.</span></span> <span data-ttu-id="4d6c8-183">新增其他位址空間不是 S2S 組態的必要部分，但如果您需要多個位址空間，請使用下列步驟︰</span><span class="sxs-lookup"><span data-stu-id="4d6c8-183">Adding additional address space is not a required part of a S2S configuration, but if you require multiple address spaces, use the following steps:</span></span>

1. <span data-ttu-id="4d6c8-184">在入口網站中找出虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="4d6c8-184">Locate the virtual networks in the portal.</span></span>
2. <span data-ttu-id="4d6c8-185">在您的虛擬網路頁面上，按一下 [設定] 區段下的 [位址空間]。</span><span class="sxs-lookup"><span data-stu-id="4d6c8-185">On the page for your virtual network, under the **Settings** section, click **Address space**.</span></span>
3. <span data-ttu-id="4d6c8-186">在 [設定空間] 頁面上，按一下 [+新增] 並輸入其他位址空間。</span><span class="sxs-lookup"><span data-stu-id="4d6c8-186">On the Address space page, click **+Add** and enter additional address space.</span></span>

## <span data-ttu-id="4d6c8-187"><a name="dns"></a>3.指定 DNS 伺服器</span><span class="sxs-lookup"><span data-stu-id="4d6c8-187"><a name="dns"></a>3. Specify a DNS server</span></span>

<span data-ttu-id="4d6c8-188">DNS 設定不是 S2S 組態的必要部分，但如果您想要名稱解析，則需要 DNS。</span><span class="sxs-lookup"><span data-stu-id="4d6c8-188">DNS settings are not a required part of a S2S configuration, but DNS is necessary if you want name resolution.</span></span> <span data-ttu-id="4d6c8-189">指定一個值並不會建立新的 DNS 伺服器。</span><span class="sxs-lookup"><span data-stu-id="4d6c8-189">Specifying a value does not create a new DNS server.</span></span> <span data-ttu-id="4d6c8-190">您指定的 DNS 伺服器 IP 位址應該是可以解析您所連線之資源名稱的 DNS 伺服器。</span><span class="sxs-lookup"><span data-stu-id="4d6c8-190">The DNS server IP address that you specify should be a DNS server that can resolve the names for the resources you are connecting to.</span></span> <span data-ttu-id="4d6c8-191">對於範例設定，我們使用了私人 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="4d6c8-191">For the example settings, we used a private IP address.</span></span> <span data-ttu-id="4d6c8-192">我們使用的 IP 位址可能不是您 DNS 伺服器的 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="4d6c8-192">The IP address we use is probably not the IP address of your DNS server.</span></span> <span data-ttu-id="4d6c8-193">請務必使用您自己的值。</span><span class="sxs-lookup"><span data-stu-id="4d6c8-193">Be sure to use your own values.</span></span>

<span data-ttu-id="4d6c8-194">建立虛擬網路之後，您可以新增 DNS 伺服器的 IP 位址，以便處理名稱解析。</span><span class="sxs-lookup"><span data-stu-id="4d6c8-194">After you create your virtual network, you can add the IP address of a DNS server to handle name resolution.</span></span> <span data-ttu-id="4d6c8-195">開啟您的虛擬網路設定，按一下 DNS 伺服器，並新增您要用於名稱解析的 DNS 伺服器 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="4d6c8-195">Open the settings for your virtual network, click DNS servers, and add the IP address of the DNS server that you want to use for name resolution.</span></span>

1. <span data-ttu-id="4d6c8-196">在入口網站中找出虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="4d6c8-196">Locate the virtual networks in the portal.</span></span>
2. <span data-ttu-id="4d6c8-197">在您的虛擬網路頁面上，按一下 [設定] 區段下的 [DNS 伺服器]。</span><span class="sxs-lookup"><span data-stu-id="4d6c8-197">On the page for your virtual network, under the **Settings** section, click **DNS servers**.</span></span>
3. <span data-ttu-id="4d6c8-198">新增 DNS 伺服器。</span><span class="sxs-lookup"><span data-stu-id="4d6c8-198">Add a DNS server.</span></span>
4. <span data-ttu-id="4d6c8-199">若要儲存您的設定，按一下頁面頂端的 [儲存]。</span><span class="sxs-lookup"><span data-stu-id="4d6c8-199">To save your settings, click **Save** at the top of the page.</span></span>

## <span data-ttu-id="4d6c8-200"><a name="localsite"></a>4.設定本機網站</span><span class="sxs-lookup"><span data-stu-id="4d6c8-200"><a name="localsite"></a>4. Configure the local site</span></span>

<span data-ttu-id="4d6c8-201">本機網站通常是指您的內部部署位置。</span><span class="sxs-lookup"><span data-stu-id="4d6c8-201">The local site typically refers to your on-premises location.</span></span> <span data-ttu-id="4d6c8-202">它包含您要建立連線之 VPN 裝置的 IP 位址，以及將透過 VPN 閘道路由傳送至 VPN 裝置的 IP 位址範圍。</span><span class="sxs-lookup"><span data-stu-id="4d6c8-202">It contains the IP address of the VPN device to which you will create a connection, and the IP address ranges that will be routed through the VPN gateway to the VPN device.</span></span>

1. <span data-ttu-id="4d6c8-203">在入口網站中，瀏覽至要建立閘道的虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="4d6c8-203">In the portal, navigate to the virtual network for which you want to create a gateway.</span></span>
2. <span data-ttu-id="4d6c8-204">在您的虛擬網路頁面上，於 [概觀] 頁面的 [VPN 連線] 區段中，按一下 [閘道] 以開啟 [新增 VPN 連線] 頁面。</span><span class="sxs-lookup"><span data-stu-id="4d6c8-204">On the page for your virtual network, on the **Overview** page, in the VPN connections section, click **Gateway** to open the **New VPN Connection** page.</span></span>

  <span data-ttu-id="4d6c8-205">![按一下以設定閘道設定](./media/vpn-gateway-howto-site-to-site-classic-portal/beforegw125.png "按一下以設定閘道設定")</span><span class="sxs-lookup"><span data-stu-id="4d6c8-205">![Click to configure gateway settings](./media/vpn-gateway-howto-site-to-site-classic-portal/beforegw125.png "Click to configure gateway settings")</span></span>
3. <span data-ttu-id="4d6c8-206">在 [新增 VPN 連線] 頁面上，選取 [站對站]。</span><span class="sxs-lookup"><span data-stu-id="4d6c8-206">On the **New VPN Connection** page, select **Site-to-site**.</span></span>
4. <span data-ttu-id="4d6c8-207">按一下 [本機網路 - 進行必要設定] 以開啟 [本機網路] 頁面。</span><span class="sxs-lookup"><span data-stu-id="4d6c8-207">Click **Local site - Configure required settings** to open the **Local site** page.</span></span> <span data-ttu-id="4d6c8-208">進行設定，然後按一下 [確定] 以儲存設定。</span><span class="sxs-lookup"><span data-stu-id="4d6c8-208">Configure the settings, and then click **OK** to save the settings.</span></span>
  - <span data-ttu-id="4d6c8-209">**名稱︰**建立可讓您輕鬆識別您的本機網站的名稱。</span><span class="sxs-lookup"><span data-stu-id="4d6c8-209">**Name:** Create a name for your local site to make it easy for you to identify.</span></span>
  - <span data-ttu-id="4d6c8-210">**VPN 閘道 IP 位址：**這是您內部部署網路之 VPN 裝置的公用 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="4d6c8-210">**VPN gateway IP address:** This is the public IP address of the VPN device for your on-premises network.</span></span> <span data-ttu-id="4d6c8-211">VPN 裝置需要 IPv4 公用 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="4d6c8-211">The VPN device requires an IPv4 public IP address.</span></span> <span data-ttu-id="4d6c8-212">為您要連線的 VPN 裝置指定有效的公用 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="4d6c8-212">Specify a valid public IP address for the VPN device to which you want to connect.</span></span> <span data-ttu-id="4d6c8-213">它不能在 NAT 後方且必須可讓 Azure 連線。</span><span class="sxs-lookup"><span data-stu-id="4d6c8-213">It cannot be behind NAT and has to be reachable by Azure.</span></span> <span data-ttu-id="4d6c8-214">如果您不知道 VPN 裝置的 IP 位址，您可以一律放入預留位置值 (只要其為有效的公用 IP 位址格式即可)，然後稍後加以變更。</span><span class="sxs-lookup"><span data-stu-id="4d6c8-214">If you don't know the IP address of your VPN device, you can always put in a placeholder value (as long as it is in the format of a valid public IP address) and then change it later.</span></span>
  - <span data-ttu-id="4d6c8-215">**用戶端位址空間︰**列出您要透過此閘道路由傳送至本機內部部署網路的 IP 位址範圍。</span><span class="sxs-lookup"><span data-stu-id="4d6c8-215">**Client Address space:** List the IP address ranges that you want routed to the local on-premises network through this gateway.</span></span> <span data-ttu-id="4d6c8-216">您可以加入多個位址空間範圍。</span><span class="sxs-lookup"><span data-stu-id="4d6c8-216">You can add multiple address space ranges.</span></span> <span data-ttu-id="4d6c8-217">確定您在此指定的範圍，不會與虛擬網路要連接的其他網路範圍重疊，或與虛擬網路本身的位址範圍重疊。</span><span class="sxs-lookup"><span data-stu-id="4d6c8-217">Make sure that the ranges you specify here do not overlap with ranges of other networks your virtual network connects to, or with the address ranges of the virtual network itself.</span></span>

  <span data-ttu-id="4d6c8-218">![本機站台](./media/vpn-gateway-howto-site-to-site-classic-portal/localnetworksite.png "設定本機站台")</span><span class="sxs-lookup"><span data-stu-id="4d6c8-218">![Local site](./media/vpn-gateway-howto-site-to-site-classic-portal/localnetworksite.png "Configure local site")</span></span>

## <span data-ttu-id="4d6c8-219"><a name="gatewaysubnet"></a>5.設定閘道子網路</span><span class="sxs-lookup"><span data-stu-id="4d6c8-219"><a name="gatewaysubnet"></a>5. Configure the gateway subnet</span></span>

<span data-ttu-id="4d6c8-220">您必須為 VPN 閘道建立閘道子網路。</span><span class="sxs-lookup"><span data-stu-id="4d6c8-220">You must create a gateway subnet for your VPN gateway.</span></span> <span data-ttu-id="4d6c8-221">閘道子網路包含 VPN 閘道服務會使用的 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="4d6c8-221">The gateway subnet contains the IP addresses that the VPN gateway services use.</span></span>

1. <span data-ttu-id="4d6c8-222">在 [新增 VPN 連線] 頁面上，選取 [立即建立閘道] 核取方塊。</span><span class="sxs-lookup"><span data-stu-id="4d6c8-222">On the **New VPN Connection** page, select the checkbox **Create gateway immediately**.</span></span> <span data-ttu-id="4d6c8-223">[選擇性閘道組態] 頁面隨即出現。</span><span class="sxs-lookup"><span data-stu-id="4d6c8-223">The 'Optional gateway configuration' page appears.</span></span> <span data-ttu-id="4d6c8-224">如果您未選取此核取方塊，則不會看到用來設定閘道器子網路的頁面。</span><span class="sxs-lookup"><span data-stu-id="4d6c8-224">If you don't select the checkbox, you won't see the page to configure the gateway subnet.</span></span>

  <span data-ttu-id="4d6c8-225">![閘道組態 - 子網路、大小、路由類型](./media/vpn-gateway-howto-site-to-site-classic-portal/optional.png "閘道組態 - 子網路、大小、路由類型")</span><span class="sxs-lookup"><span data-stu-id="4d6c8-225">![Gateway configuration - Subnet, size, routing type](./media/vpn-gateway-howto-site-to-site-classic-portal/optional.png "Gateway configuration - Subnet, size, routing type")</span></span>
2. <span data-ttu-id="4d6c8-226">若要開啟 [閘道組態] 頁面，請按一下 [選擇性閘道組態 - 子網路、大小和路由類型]。</span><span class="sxs-lookup"><span data-stu-id="4d6c8-226">To open the **Gateway configuration** page, click **Optional gateway configuration - Subnet, size, and routing type**.</span></span>
3. <span data-ttu-id="4d6c8-227">在 [閘道組態] 頁面上，按一下 [子網路 - 進行必要設定] 以開啟 [新增子網路] 頁面。</span><span class="sxs-lookup"><span data-stu-id="4d6c8-227">On the **Gateway Configuration** page, click **Subnet - Configure required settings** to open the **Add subnet** page.</span></span>

  <span data-ttu-id="4d6c8-228">![閘道組態 - 閘道子網路](./media/vpn-gateway-howto-site-to-site-classic-portal/subnetrequired.png "閘道組態 - 閘道子網路")</span><span class="sxs-lookup"><span data-stu-id="4d6c8-228">![Gateway configuration - gateway subnet](./media/vpn-gateway-howto-site-to-site-classic-portal/subnetrequired.png "Gateway configuration - gateway subnet")</span></span>
4. <span data-ttu-id="4d6c8-229">在 [新增子網路] 頁面上，新增閘道子網路。</span><span class="sxs-lookup"><span data-stu-id="4d6c8-229">On the **Add subnet** page, add the gateway subnet.</span></span> <span data-ttu-id="4d6c8-230">您所要建立的 VPN 閘道組態會決定您需要為閘道子網路指定的大小。</span><span class="sxs-lookup"><span data-stu-id="4d6c8-230">The size of the gateway subnet that you specify depends on the VPN gateway configuration that you want to create.</span></span> <span data-ttu-id="4d6c8-231">雖然可以建立像 /29 這麼小的閘道子網路，但建議您使用 /27 或 /28。</span><span class="sxs-lookup"><span data-stu-id="4d6c8-231">While it is possible to create a gateway subnet as small as /29, we recommend that you use /27 or /28.</span></span> <span data-ttu-id="4d6c8-232">這可建立包含更多位址的較大子網路。</span><span class="sxs-lookup"><span data-stu-id="4d6c8-232">This creates a larger subnet that includes more addresses.</span></span> <span data-ttu-id="4d6c8-233">使用較大的閘道子網路可讓您擁有足夠的 IP 位址，以因應未來可能的組態。</span><span class="sxs-lookup"><span data-stu-id="4d6c8-233">Using a larger gateway subnet allows for enough IP addresses to accommodate possible future configurations.</span></span>

  <span data-ttu-id="4d6c8-234">![新增閘道子網路](./media/vpn-gateway-howto-site-to-site-classic-portal/addgwsubnet.png "新增閘道子網路")</span><span class="sxs-lookup"><span data-stu-id="4d6c8-234">![Add gateway subnet](./media/vpn-gateway-howto-site-to-site-classic-portal/addgwsubnet.png "Add gateway subnet")</span></span>

## <span data-ttu-id="4d6c8-235"><a name="sku"></a>6.指定 SKU 和 VPN 類型</span><span class="sxs-lookup"><span data-stu-id="4d6c8-235"><a name="sku"></a>6. Specify the SKU and VPN type</span></span>

1. <span data-ttu-id="4d6c8-236">選取閘道**大小**。</span><span class="sxs-lookup"><span data-stu-id="4d6c8-236">Select the gateway **Size**.</span></span> <span data-ttu-id="4d6c8-237">這是您會用來建立虛擬網路閘道的閘道 SKU。</span><span class="sxs-lookup"><span data-stu-id="4d6c8-237">This is the gateway SKU that you use to create your virtual network gateway.</span></span> <span data-ttu-id="4d6c8-238">在入口網站中，[預設 SKU] 為 [基本]。</span><span class="sxs-lookup"><span data-stu-id="4d6c8-238">In the portal, the 'Default SKU' = **Basic**.</span></span> <span data-ttu-id="4d6c8-239">傳統 VPN 閘道會使用舊式 (舊版) 閘道 SKU。</span><span class="sxs-lookup"><span data-stu-id="4d6c8-239">Classic VPN gateways use the old (legacy) gateway SKUs.</span></span> <span data-ttu-id="4d6c8-240">如需舊版閘道 SKU 的詳細資訊，請參閱[使用虛擬網路閘道 SKU (舊式 SKU)](vpn-gateway-about-skus-legacy.md)。</span><span class="sxs-lookup"><span data-stu-id="4d6c8-240">For more information about the legacy gateway SKUs, see [Working with virtual network gateway SKUs (old SKUs)](vpn-gateway-about-skus-legacy.md).</span></span>

  <span data-ttu-id="4d6c8-241">![選取 SKUL 和 VPN 類型](./media/vpn-gateway-howto-site-to-site-classic-portal/sku.png "選取 SKU 和 VPN 類型")</span><span class="sxs-lookup"><span data-stu-id="4d6c8-241">![Select SKUL and VPN type](./media/vpn-gateway-howto-site-to-site-classic-portal/sku.png "Select SKU and VPN type")</span></span>
2. <span data-ttu-id="4d6c8-242">選取閘道的 [路由類型]。</span><span class="sxs-lookup"><span data-stu-id="4d6c8-242">Select the **Routing Type** for your gateway.</span></span> <span data-ttu-id="4d6c8-243">這也稱為 VPN 類型。</span><span class="sxs-lookup"><span data-stu-id="4d6c8-243">This is also known as the VPN type.</span></span> <span data-ttu-id="4d6c8-244">請務必選取正確的閘道類型，因為您無法轉換閘道的類型。</span><span class="sxs-lookup"><span data-stu-id="4d6c8-244">It's important to select the correct gateway type because you cannot convert the gateway from one type to another.</span></span> <span data-ttu-id="4d6c8-245">您的 VPN 裝置必須與您所選取的路由類型相容。</span><span class="sxs-lookup"><span data-stu-id="4d6c8-245">Your VPN device must be compatible with the routing type you select.</span></span> <span data-ttu-id="4d6c8-246">如需 VPN 類型的詳細資訊，請參閱[關於 VPN 閘道設定](vpn-gateway-about-vpn-gateway-settings.md#vpntype)。</span><span class="sxs-lookup"><span data-stu-id="4d6c8-246">For more information about VPN type, see [About VPN Gateway Settings](vpn-gateway-about-vpn-gateway-settings.md#vpntype).</span></span> <span data-ttu-id="4d6c8-247">您可能會看到參考 'RouteBased' 和 'PolicyBased' VPN 類型的文章。</span><span class="sxs-lookup"><span data-stu-id="4d6c8-247">You may see articles referring to 'RouteBased' and 'PolicyBased' VPN types.</span></span> <span data-ttu-id="4d6c8-248">'Dynamic' 對應到 'RouteBased'，而 'Static' 對應到 'PolicyBased'。</span><span class="sxs-lookup"><span data-stu-id="4d6c8-248">'Dynamic' corresponds to 'RouteBased', and 'Static' corresponds to' PolicyBased'.</span></span>
3. <span data-ttu-id="4d6c8-249">按一下 [確定]  來儲存設定。</span><span class="sxs-lookup"><span data-stu-id="4d6c8-249">Click **OK** to save the settings.</span></span>
4. <span data-ttu-id="4d6c8-250">在 [新增 VPN 連線] 頁面上，按一下頁面底部的 [確定]，開始建立虛擬網路閘道。</span><span class="sxs-lookup"><span data-stu-id="4d6c8-250">On the **New VPN Connection** page, click **OK** at the bottom of the page to begin creating your virtual network gateway.</span></span> <span data-ttu-id="4d6c8-251">視您選取的 SKU 而定，建立虛擬網路閘道可能需要 45 分鐘的時間。</span><span class="sxs-lookup"><span data-stu-id="4d6c8-251">Depending on the SKU you select, it can take up to 45 minutes to create a virtual network gateway.</span></span>

## <span data-ttu-id="4d6c8-252"><a name="vpndevice"></a>7.設定 VPN 裝置</span><span class="sxs-lookup"><span data-stu-id="4d6c8-252"><a name="vpndevice"></a>7. Configure your VPN device</span></span>

<span data-ttu-id="4d6c8-253">內部部署網路的站對站連線需要 VPN 裝置。</span><span class="sxs-lookup"><span data-stu-id="4d6c8-253">Site-to-Site connections to an on-premises network require a VPN device.</span></span> <span data-ttu-id="4d6c8-254">在此步驟中，設定 VPN 裝置。</span><span class="sxs-lookup"><span data-stu-id="4d6c8-254">In this step, you configure your VPN device.</span></span> <span data-ttu-id="4d6c8-255">在設定 VPN 裝置時，您需要下列項目：</span><span class="sxs-lookup"><span data-stu-id="4d6c8-255">When configuring your VPN device, you need the following:</span></span>

- <span data-ttu-id="4d6c8-256">共用金鑰。</span><span class="sxs-lookup"><span data-stu-id="4d6c8-256">A shared key.</span></span> <span data-ttu-id="4d6c8-257">這個共同金鑰與您建立站對站 VPN 連線時指定的共用金鑰相同。</span><span class="sxs-lookup"><span data-stu-id="4d6c8-257">This is the same shared key that you specify when creating your Site-to-Site VPN connection.</span></span> <span data-ttu-id="4d6c8-258">在我們的範例中，我們會使用基本的共用金鑰。</span><span class="sxs-lookup"><span data-stu-id="4d6c8-258">In our examples, we use a basic shared key.</span></span> <span data-ttu-id="4d6c8-259">我們建議您產生更複雜的金鑰以供使用。</span><span class="sxs-lookup"><span data-stu-id="4d6c8-259">We recommend that you generate a more complex key to use.</span></span>
- <span data-ttu-id="4d6c8-260">虛擬網路閘道的公用 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="4d6c8-260">The Public IP address of your virtual network gateway.</span></span> <span data-ttu-id="4d6c8-261">您可以使用 Azure 入口網站、PowerShell 或 CLI 來檢視公用 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="4d6c8-261">You can view the public IP address by using the Azure portal, PowerShell, or CLI.</span></span>

[!INCLUDE [vpn-gateway-configure-vpn-device-rm](../../includes/vpn-gateway-configure-vpn-device-rm-include.md)]

## <span data-ttu-id="4d6c8-262"><a name="CreateConnection"></a>8.建立連線</span><span class="sxs-lookup"><span data-stu-id="4d6c8-262"><a name="CreateConnection"></a>8. Create the connection</span></span>
<span data-ttu-id="4d6c8-263">在此步驟中，您可以設定共用的金鑰及建立連線。</span><span class="sxs-lookup"><span data-stu-id="4d6c8-263">In this step, you set the shared key and create the connection.</span></span> <span data-ttu-id="4d6c8-264">您設定的金鑰必須是 VPN 裝置組態中使用的相同金鑰。</span><span class="sxs-lookup"><span data-stu-id="4d6c8-264">The key you set is must be the same key that was used in your VPN device configuration.</span></span>

> [!NOTE]
> <span data-ttu-id="4d6c8-265">此步驟目前無法不適用於 Azure 入口網站。</span><span class="sxs-lookup"><span data-stu-id="4d6c8-265">Currently, this step is not available in the Azure portal.</span></span> <span data-ttu-id="4d6c8-266">您必須使用 Azure PowerShell Cmdlet 的服務管理 (SM) 版本。</span><span class="sxs-lookup"><span data-stu-id="4d6c8-266">You must use the Service Management (SM) version of the Azure PowerShell cmdlets.</span></span>
>

### <a name="step-1-connect-to-your-azure-account"></a><span data-ttu-id="4d6c8-267">步驟 1.</span><span class="sxs-lookup"><span data-stu-id="4d6c8-267">Step 1.</span></span> <span data-ttu-id="4d6c8-268">連線至您的 Azure 帳戶</span><span class="sxs-lookup"><span data-stu-id="4d6c8-268">Connect to your Azure account</span></span>

1. <span data-ttu-id="4d6c8-269">以提高的權限開啟 PowerShell 主控台並連接到您的帳戶。</span><span class="sxs-lookup"><span data-stu-id="4d6c8-269">Open your PowerShell console with elevated rights and connect to your account.</span></span> <span data-ttu-id="4d6c8-270">使用下列範例來協助您連接：</span><span class="sxs-lookup"><span data-stu-id="4d6c8-270">Use the following example to help you connect:</span></span>

  ```powershell
  Add-AzureAccount
  ```
2. <span data-ttu-id="4d6c8-271">檢查帳戶的訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="4d6c8-271">Check the subscriptions for the account.</span></span>

  ```powershell
  Get-AzureSubscription
  ```
3. <span data-ttu-id="4d6c8-272">如果您有多個訂用帳戶，請選取您要使用的訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="4d6c8-272">If you have more than one subscription, select the subscription that you want to use.</span></span>

  ```powershell
  Select-AzureSubscription -SubscriptionId "Replace_with_your_subscription_ID"
  ```

### <a name="step-2-set-the-shared-key-and-create-the-connection"></a><span data-ttu-id="4d6c8-273">步驟 2.</span><span class="sxs-lookup"><span data-stu-id="4d6c8-273">Step 2.</span></span> <span data-ttu-id="4d6c8-274">設定共用金鑰及建立連線</span><span class="sxs-lookup"><span data-stu-id="4d6c8-274">Set the shared key and create the connection</span></span>

<span data-ttu-id="4d6c8-275">使用 PowerShell 和傳統部署模型時，入口網站中的資源名稱有時不是 Azure 使用 PowerShell 時預期看見的名稱。</span><span class="sxs-lookup"><span data-stu-id="4d6c8-275">When working with PowerShell and the classic deployment model, sometimes the names of resources in the portal are not the names the Azure expects to see when using PowerShell.</span></span> <span data-ttu-id="4d6c8-276">下列步驟將協助您匯出網路組態檔，以取得名稱的確切值。</span><span class="sxs-lookup"><span data-stu-id="4d6c8-276">The following steps help you export the network configuration file to obtain the exact values for the names.</span></span>

1. <span data-ttu-id="4d6c8-277">在您的電腦上建立目錄，然後將網路組態檔匯出到該目錄。</span><span class="sxs-lookup"><span data-stu-id="4d6c8-277">Create a directory on your computer and then export the network configuration file to the directory.</span></span> <span data-ttu-id="4d6c8-278">在此範例中，會將網路組態檔匯出到 C:\AzureNet。</span><span class="sxs-lookup"><span data-stu-id="4d6c8-278">In this example, the network configuration file is exported to C:\AzureNet.</span></span>

  ```powershell
  Get-AzureVNetConfig -ExportToFile C:\AzureNet\NetworkConfig.xml
  ```
2. <span data-ttu-id="4d6c8-279">使用 xml 編輯器開啟網路組態檔，並檢查 'LocalNetworkSite name' 和 'VirtualNetworkSite name' 的值。</span><span class="sxs-lookup"><span data-stu-id="4d6c8-279">Open the network configuration file with an xml editor and check the values for 'LocalNetworkSite name' and 'VirtualNetworkSite name'.</span></span> <span data-ttu-id="4d6c8-280">修改範例以反映您所需的值。</span><span class="sxs-lookup"><span data-stu-id="4d6c8-280">Modify the example to reflect the values that you need.</span></span> <span data-ttu-id="4d6c8-281">指定包含空格的名稱時，請使用單引號括住值。</span><span class="sxs-lookup"><span data-stu-id="4d6c8-281">When specifying a name that contains spaces, use single quotation marks around the value.</span></span>

3. <span data-ttu-id="4d6c8-282">設定共用金鑰及建立連線。</span><span class="sxs-lookup"><span data-stu-id="4d6c8-282">Set the shared key and create the connection.</span></span> <span data-ttu-id="4d6c8-283">'-SharedKey' 是您產生和指定的值。</span><span class="sxs-lookup"><span data-stu-id="4d6c8-283">The '-SharedKey' is a value that you generate and specify.</span></span> <span data-ttu-id="4d6c8-284">在範例中，我們使用的是 'abc123'，但是您可以產生且 (應該) 使用更為複雜的值。</span><span class="sxs-lookup"><span data-stu-id="4d6c8-284">In the example, we used 'abc123', but you can generate (and should) use something more complex.</span></span> <span data-ttu-id="4d6c8-285">重要的是，您在此指定的值必須與您在設定 VPN 裝置時指定的值相同。</span><span class="sxs-lookup"><span data-stu-id="4d6c8-285">The important thing is that the value you specify here must be the same value that you specified when configuring your VPN device.</span></span>

  ```powershell
  Set-AzureVNetGatewayKey -VNetName 'Group TestRG1 TestVNet1' `
  -LocalNetworkSiteName 'D1BFC9CB_Site2' -SharedKey abc123
  ```
<span data-ttu-id="4d6c8-286">建立連線後，結果是︰**狀態︰成功**。</span><span class="sxs-lookup"><span data-stu-id="4d6c8-286">When the connection is created, the result is: **Status: Successful**.</span></span>

## <span data-ttu-id="4d6c8-287"><a name="verify"></a>9.確認您的連接</span><span class="sxs-lookup"><span data-stu-id="4d6c8-287"><a name="verify"></a>9. Verify your connection</span></span>

[!INCLUDE [vpn-gateway-verify-connection-azureportal-classic](../../includes/vpn-gateway-verify-connection-azureportal-classic-include.md)]

<span data-ttu-id="4d6c8-288">如有連線問題，請參閱左窗格中目錄的 [疑難排解] 區段。</span><span class="sxs-lookup"><span data-stu-id="4d6c8-288">If you are having trouble connecting, see the **Troubleshoot** section of the table of contents in the left pane.</span></span>

## <span data-ttu-id="4d6c8-289"><a name="reset"></a>如何重設 VPN 閘道</span><span class="sxs-lookup"><span data-stu-id="4d6c8-289"><a name="reset"></a>How to reset a VPN gateway</span></span>

<span data-ttu-id="4d6c8-290">如果您遺失一或多個站對站 VPN 通道上的跨單位 VPN 連線，重設 Azure VPN 閘道會很有幫助。</span><span class="sxs-lookup"><span data-stu-id="4d6c8-290">Resetting an Azure VPN gateway is helpful if you lose cross-premises VPN connectivity on one or more Site-to-Site VPN tunnels.</span></span> <span data-ttu-id="4d6c8-291">在此情況下，您的所有內部部署 VPN 裝置都會運作正常，但無法使用 Azure VPN 閘道建立 IPsec 通道。</span><span class="sxs-lookup"><span data-stu-id="4d6c8-291">In this situation, your on-premises VPN devices are all working correctly, but are not able to establish IPsec tunnels with the Azure VPN gateways.</span></span> <span data-ttu-id="4d6c8-292">如需相關步驟，請參閱[重設 VPN 閘道](vpn-gateway-resetgw-classic.md)。</span><span class="sxs-lookup"><span data-stu-id="4d6c8-292">For steps, see [Reset a VPN gateway](vpn-gateway-resetgw-classic.md).</span></span>

## <span data-ttu-id="4d6c8-293"><a name="changesku"></a>如何變更閘道 SKU</span><span class="sxs-lookup"><span data-stu-id="4d6c8-293"><a name="changesku"></a>How to change a gateway SKU</span></span>

<span data-ttu-id="4d6c8-294">若需變更閘道 SKU 的步驟，請參閱[調整閘道 SKU 的大小](vpn-gateway-about-SKUS-legacy.md)。</span><span class="sxs-lookup"><span data-stu-id="4d6c8-294">For the steps to change a gateway SKU, see [Resize a gateway SKU](vpn-gateway-about-SKUS-legacy.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="4d6c8-295">後續步驟</span><span class="sxs-lookup"><span data-stu-id="4d6c8-295">Next steps</span></span>

* <span data-ttu-id="4d6c8-296">一旦完成您的連接，就可以將虛擬機器加入您的虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="4d6c8-296">Once your connection is complete, you can add virtual machines to your virtual networks.</span></span> <span data-ttu-id="4d6c8-297">如需詳細資訊，請參閱[虛擬機器](https://docs.microsoft.com/azure/#pivot=services&panel=Compute)。</span><span class="sxs-lookup"><span data-stu-id="4d6c8-297">For more information, see [Virtual Machines](https://docs.microsoft.com/azure/#pivot=services&panel=Compute).</span></span>
* <span data-ttu-id="4d6c8-298">如需強制通道的相關資訊，請參閱[關於強制通道](vpn-gateway-about-forced-tunneling.md)。</span><span class="sxs-lookup"><span data-stu-id="4d6c8-298">For information about Forced Tunneling, see [About Forced Tunneling](vpn-gateway-about-forced-tunneling.md).</span></span>