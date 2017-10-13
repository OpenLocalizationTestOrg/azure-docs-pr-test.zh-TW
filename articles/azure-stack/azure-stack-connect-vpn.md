---
title: "使用 VPN 將 Azure Stack 連線至 Azure"
description: "如何使用 VPN 將 Azure Stack 中的虛擬網路連線至 Azure 中的虛擬網路。"
services: azure-stack
documentationcenter: 
author: ScottNapolitan
manager: 
editor: 
ms.assetid: 
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 9/25/2017
ms.author: victorh
ms.openlocfilehash: c06eb0bb44bdfeab956e9b5051786b5bc631acf5
ms.sourcegitcommit: 90e2cced6a773b1b52f999ba73cd8877305d270b
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/13/2017
---
# <a name="connect-azure-stack-to-azure-using-vpn"></a><span data-ttu-id="77411-103">使用 VPN 將 Azure Stack 連線至 Azure</span><span class="sxs-lookup"><span data-stu-id="77411-103">Connect Azure Stack to Azure using VPN</span></span>

<span data-ttu-id="77411-104">「適用於：Azure Stack 整合系統」</span><span class="sxs-lookup"><span data-stu-id="77411-104">*Applies to: Azure Stack integrated systems*</span></span>

<span data-ttu-id="77411-105">本文示範如何建立站對站 VPN，以將 Azure Stack 中的虛擬網路連線至 Azure 中的虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="77411-105">This article shows you how to create a site-to-site VPN to connect a virtual network in Azure Stack to a virtual network in Azure.</span></span>

### <a name="connection-diagram"></a><span data-ttu-id="77411-106">連接圖表</span><span class="sxs-lookup"><span data-stu-id="77411-106">Connection diagram</span></span>
<span data-ttu-id="77411-107">下圖顯示完成時連線設定看起來的樣子：</span><span class="sxs-lookup"><span data-stu-id="77411-107">The following diagram shows what the connection configuration should look like when you’re done:</span></span>

![站對站 VPN 連線組態](media/azure-stack-connect-vpn/image2.png)

### <a name="before-you-begin"></a><span data-ttu-id="77411-109">開始之前</span><span class="sxs-lookup"><span data-stu-id="77411-109">Before you begin</span></span>
<span data-ttu-id="77411-110">若要完成連線設定，請務必在開始前備妥下列項目：</span><span class="sxs-lookup"><span data-stu-id="77411-110">To complete the connection configuration, make sure you have the following items before you begin:</span></span>

* <span data-ttu-id="77411-111">直接連線至網際網路的 Azure Stack 整合系統 (多節點) 部署。</span><span class="sxs-lookup"><span data-stu-id="77411-111">An Azure Stack integrated systems (multi-node) deployment that is directly connected to the Internet.</span></span> <span data-ttu-id="77411-112">這表示必須可從公用網際網路直接連線至您的外部公用 IP 位址範圍。</span><span class="sxs-lookup"><span data-stu-id="77411-112">This means that your External Public IP Address range must be directly reachable from the public Internet.</span></span>
* <span data-ttu-id="77411-113">有效的 Azure 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="77411-113">A valid Azure subscription.</span></span>  <span data-ttu-id="77411-114">如果您沒有 Azure 訂用帳戶，您可以建立[免費 Azure 帳戶](https://azure.microsoft.com/free/?b=17.06)。</span><span class="sxs-lookup"><span data-stu-id="77411-114">If you don’t have an Azure subscription, you can create a [free Azure account here](https://azure.microsoft.com/free/?b=17.06).</span></span>

## <a name="network-example-values-table"></a><span data-ttu-id="77411-115">網路範例值表格</span><span class="sxs-lookup"><span data-stu-id="77411-115">Network example values table</span></span>
<span data-ttu-id="77411-116">網路範例值表格顯示本文中使用的範例值。</span><span class="sxs-lookup"><span data-stu-id="77411-116">The network example values table shows the sample values that are used in this article.</span></span> <span data-ttu-id="77411-117">您可以使用這些值，也可以參考這些值，以深入了解本文中的範例。</span><span class="sxs-lookup"><span data-stu-id="77411-117">You can use these values or you can refer to them to better understand the examples in this article.</span></span>

<span data-ttu-id="77411-118">**網路範例值表格**</span><span class="sxs-lookup"><span data-stu-id="77411-118">**Network example values table**</span></span>
|   |<span data-ttu-id="77411-119">Azure Stack</span><span class="sxs-lookup"><span data-stu-id="77411-119">Azure Stack</span></span>|<span data-ttu-id="77411-120">Azure</span><span class="sxs-lookup"><span data-stu-id="77411-120">Azure</span></span>|
|---------|---------|---------|
|<span data-ttu-id="77411-121">虛擬網路名稱</span><span class="sxs-lookup"><span data-stu-id="77411-121">Virtual network name</span></span>     |<span data-ttu-id="77411-122">Azs-VNet</span><span class="sxs-lookup"><span data-stu-id="77411-122">Azs-VNet</span></span>|<span data-ttu-id="77411-123">AzureVNet</span><span class="sxs-lookup"><span data-stu-id="77411-123">AzureVNet</span></span> |
|<span data-ttu-id="77411-124">虛擬網路位址空間</span><span class="sxs-lookup"><span data-stu-id="77411-124">Virtual network address space</span></span> |<span data-ttu-id="77411-125">10.1.0.0/16</span><span class="sxs-lookup"><span data-stu-id="77411-125">10.1.0.0/16</span></span>|<span data-ttu-id="77411-126">10.100.0.0/16</span><span class="sxs-lookup"><span data-stu-id="77411-126">10.100.0.0/16</span></span>|
|<span data-ttu-id="77411-127">子網路名稱</span><span class="sxs-lookup"><span data-stu-id="77411-127">Subnet name</span></span>     |<span data-ttu-id="77411-128">FrontEnd</span><span class="sxs-lookup"><span data-stu-id="77411-128">FrontEnd</span></span>|<span data-ttu-id="77411-129">FrontEnd</span><span class="sxs-lookup"><span data-stu-id="77411-129">FrontEnd</span></span>|
|<span data-ttu-id="77411-130">子網路位址範圍</span><span class="sxs-lookup"><span data-stu-id="77411-130">Subnet address range</span></span>|<span data-ttu-id="77411-131">10.1.0.0/24</span><span class="sxs-lookup"><span data-stu-id="77411-131">10.1.0.0/24</span></span> |<span data-ttu-id="77411-132">10.100.0.0/24</span><span class="sxs-lookup"><span data-stu-id="77411-132">10.100.0.0/24</span></span> |
|<span data-ttu-id="77411-133">閘道器子網路</span><span class="sxs-lookup"><span data-stu-id="77411-133">Gateway subnet</span></span>     |<span data-ttu-id="77411-134">10.1.1.0/24</span><span class="sxs-lookup"><span data-stu-id="77411-134">10.1.1.0/24</span></span>|<span data-ttu-id="77411-135">10.100.1.0/24</span><span class="sxs-lookup"><span data-stu-id="77411-135">10.100.1.0/24</span></span>|

## <a name="create-the-network-resources-in-azure"></a><span data-ttu-id="77411-136">在 Azure 中建立網路資源</span><span class="sxs-lookup"><span data-stu-id="77411-136">Create the network resources in Azure</span></span>

<span data-ttu-id="77411-137">請先為 Azure 建立網路資源。</span><span class="sxs-lookup"><span data-stu-id="77411-137">First you create the network resources for Azure.</span></span> <span data-ttu-id="77411-138">下列指示說明如何使用 [Azure 入口網站](http://portal.azure.com/)來建立資源。</span><span class="sxs-lookup"><span data-stu-id="77411-138">The following instructions show how to create the resources by using the [Azure portal](http://portal.azure.com/).</span></span>

### <a name="create-the-virtual-network-and-vm-subnet"></a><span data-ttu-id="77411-139">建立虛擬網路和 VM 子網路</span><span class="sxs-lookup"><span data-stu-id="77411-139">Create the virtual network and VM subnet</span></span>

1. <span data-ttu-id="77411-140">使用 Azure 帳戶登入 [Azure 入口網站](http://portal.azure.com/)。</span><span class="sxs-lookup"><span data-stu-id="77411-140">Sign in to the [Azure portal](http://portal.azure.com/) using your Azure account.</span></span>
2. <span data-ttu-id="77411-141">在使用者入口網站中，選取 [新增]。</span><span class="sxs-lookup"><span data-stu-id="77411-141">In the user portal, select **New**.</span></span>
3. <span data-ttu-id="77411-142">移至 [Marketplace]，然後選取 [網路]。</span><span class="sxs-lookup"><span data-stu-id="77411-142">Go to **Marketplace**, and then select **Networking**.</span></span>
4. <span data-ttu-id="77411-143">選取 [虛擬網路]。</span><span class="sxs-lookup"><span data-stu-id="77411-143">Select **Virtual network**.</span></span>
5. <span data-ttu-id="77411-144">使用網路設定表中的資訊，以識別 Azure [名稱]、[位址空間]、[子網路名稱] 及 [子網路位址範圍] 的值。</span><span class="sxs-lookup"><span data-stu-id="77411-144">Use the information from the network configuration table to identify the values for Azure **Name**, **Address space**, **Subnet name**, and **Subnet address range**.</span></span>
6. <span data-ttu-id="77411-145">針對 [資源群組]，建立資源群組，或選取 [使用現有的] \(如果您已經有資源群組)。</span><span class="sxs-lookup"><span data-stu-id="77411-145">For **Resource Group**, create a new resource group or, if you already have one, select **Use existing**.</span></span>
7. <span data-ttu-id="77411-146">選取 VNet 的 [位置]。</span><span class="sxs-lookup"><span data-stu-id="77411-146">Select the **Location** of your VNet.</span></span>  <span data-ttu-id="77411-147">如果您使用範例值，請選取 [美國東部]，或使用您偏好的另一個位置。</span><span class="sxs-lookup"><span data-stu-id="77411-147">If you're using the example values, select **East US** or use another location if you prefer.</span></span>
8. <span data-ttu-id="77411-148">選取 [釘選到儀表板]。</span><span class="sxs-lookup"><span data-stu-id="77411-148">Select **Pin to dashboard**.</span></span>
9. <span data-ttu-id="77411-149">選取 [ **建立**]。</span><span class="sxs-lookup"><span data-stu-id="77411-149">Select **Create**.</span></span>

### <a name="create-the-gateway-subnet"></a><span data-ttu-id="77411-150">建立閘道子網路</span><span class="sxs-lookup"><span data-stu-id="77411-150">Create the Gateway Subnet</span></span>
1. <span data-ttu-id="77411-151">從儀表板開啟您建立的虛擬網路資源 (**AzureVNet**)。</span><span class="sxs-lookup"><span data-stu-id="77411-151">Open the Virtual network resource you created (**AzureVNet**) from the dashboard.</span></span>
2. <span data-ttu-id="77411-152">在 [設定] 區段上，選取 [子網路]。</span><span class="sxs-lookup"><span data-stu-id="77411-152">On the **Settings** section, select **Subnets**.</span></span>
3. <span data-ttu-id="77411-153">選取 [閘道子網路] 以將閘道子網路新增到虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="77411-153">Select  **Gateway subnet** to add a gateway subnet to the virtual network.</span></span>
4. <span data-ttu-id="77411-154">子網路名稱預設為 **GatewaySubnet**。</span><span class="sxs-lookup"><span data-stu-id="77411-154">The name of the subnet is set to **GatewaySubnet** by default.</span></span>
   <span data-ttu-id="77411-155">閘道子網路很特別﹐必須具有此特定名稱，才能正常運作。</span><span class="sxs-lookup"><span data-stu-id="77411-155">Gateway subnets are special and must have this specific name to function properly.</span></span>
5. <span data-ttu-id="77411-156">在 [位址範圍] 欄位中，確認位址是 **10.100.0.0/24**。</span><span class="sxs-lookup"><span data-stu-id="77411-156">In the **Address range** field, verify the address is **10.100.0.0/24**.</span></span>
6. <span data-ttu-id="77411-157">選取 [確定] 以建立閘道子網路。</span><span class="sxs-lookup"><span data-stu-id="77411-157">Select **OK** to create the gateway subnet.</span></span>

### <a name="create-the-virtual-network-gateway"></a><span data-ttu-id="77411-158">建立虛擬網路閘道</span><span class="sxs-lookup"><span data-stu-id="77411-158">Create the virtual network gateway</span></span>
1. <span data-ttu-id="77411-159">在 Azure 入口網站中，選取 [新增]。</span><span class="sxs-lookup"><span data-stu-id="77411-159">In the Azure portal, select **New**.</span></span>  
2. <span data-ttu-id="77411-160">移至 [Marketplace]，然後選取 [網路]。</span><span class="sxs-lookup"><span data-stu-id="77411-160">Go to **Marketplace**, and then select **Networking**.</span></span>
3. <span data-ttu-id="77411-161">從網路資源清單中，選取 [虛擬網路閘道]。</span><span class="sxs-lookup"><span data-stu-id="77411-161">From the list of network resources, select **Virtual network gateway**.</span></span>
4. <span data-ttu-id="77411-162">在 [名稱] 中輸入 **Azure-GW**。</span><span class="sxs-lookup"><span data-stu-id="77411-162">In **Name**, type **Azure-GW**.</span></span>
5. <span data-ttu-id="77411-163">若要選擇虛擬網路，請選取 [虛擬網路]。</span><span class="sxs-lookup"><span data-stu-id="77411-163">To choose a virtual network, select **Virtual network**.</span></span> <span data-ttu-id="77411-164">然後從清單中選取 [AzureVnet]。</span><span class="sxs-lookup"><span data-stu-id="77411-164">Then select **AzureVnet** from the list.</span></span>
6. <span data-ttu-id="77411-165">選取 [公用 IP 位址]。</span><span class="sxs-lookup"><span data-stu-id="77411-165">Select **Public IP address**.</span></span> <span data-ttu-id="77411-166">當 [選擇公用 IP 位址] 區段開啟時，請選取 [新建]。</span><span class="sxs-lookup"><span data-stu-id="77411-166">When the **Choose public IP address** section opens, select **Create new**.</span></span>
7. <span data-ttu-id="77411-167">在 [名稱] 中輸入 **Azure-GW-PiP**，然後選取 [確定]。</span><span class="sxs-lookup"><span data-stu-id="77411-167">In **Name**, type **Azure-GW-PiP**, and then select **OK**.</span></span>
8. <span data-ttu-id="77411-168">針對 [VPN 類型]，預設會選取 [依路由]。</span><span class="sxs-lookup"><span data-stu-id="77411-168">By default, for **VPN type**, **Route-based** is selected.</span></span>
    <span data-ttu-id="77411-169">保留 [依路由] VPN 類型。</span><span class="sxs-lookup"><span data-stu-id="77411-169">Keep the **Route-based** VPN type.</span></span>
9. <span data-ttu-id="77411-170">確認 [訂用帳戶] 和 [位置] 均正確無誤。</span><span class="sxs-lookup"><span data-stu-id="77411-170">Verify that **Subscription** and **Location** are correct.</span></span> <span data-ttu-id="77411-171">您可以將資源釘選到儀表板。</span><span class="sxs-lookup"><span data-stu-id="77411-171">You can pin the resource to the dashboard.</span></span> <span data-ttu-id="77411-172">選取 [ **建立**]。</span><span class="sxs-lookup"><span data-stu-id="77411-172">Select **Create**.</span></span>

### <a name="create-the-local-network-gateway-resource"></a><span data-ttu-id="77411-173">建立區域網路閘道資源</span><span class="sxs-lookup"><span data-stu-id="77411-173">Create the local network gateway resource</span></span>

1. <span data-ttu-id="77411-174">在 Azure 入口網站中，選取 [新增]。</span><span class="sxs-lookup"><span data-stu-id="77411-174">In the Azure portal, select **New**.</span></span> 
4. <span data-ttu-id="77411-175">移至 [Marketplace]，然後選取 [網路]。</span><span class="sxs-lookup"><span data-stu-id="77411-175">Go to **Marketplace**, and then select **Networking**.</span></span>
5. <span data-ttu-id="77411-176">從資源清單中，選取 [區域網路閘道]。</span><span class="sxs-lookup"><span data-stu-id="77411-176">From the list of resources, select **Local network gateway**.</span></span>
6. <span data-ttu-id="77411-177">在 [名稱] 中輸入 **Azs-GW**。</span><span class="sxs-lookup"><span data-stu-id="77411-177">In **Name**, type **Azs-GW**.</span></span>
7. <span data-ttu-id="77411-178">在 [IP 位址] 中，輸入稍早列在網路設定表中的 Azure Stack 虛擬網路閘道的公用 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="77411-178">In **IP address**, type the public IP address for your Azure Stack Virtual Network Gateway that is listed earlier in the network configuration table.</span></span>
8. <span data-ttu-id="77411-179">在 Azure Stack 的 [位址空間] 中，輸入 **AzureVNet**的 **10.0.10.0/23** 位址空間。</span><span class="sxs-lookup"><span data-stu-id="77411-179">In **Address Space**, from Azure Stack, type the **10.0.10.0/23** address space for **AzureVNet**.</span></span>
9. <span data-ttu-id="77411-180">確認您的 [訂用帳戶]、[資源群組] 和 [位置] 正確無誤，然後選取 [建立]。</span><span class="sxs-lookup"><span data-stu-id="77411-180">Verify that your **Subscription**, **Resource Group**, and **Location** are correct, and then select **Create**.</span></span>

## <a name="create-the-connection"></a><span data-ttu-id="77411-181">建立連線</span><span class="sxs-lookup"><span data-stu-id="77411-181">Create the connection</span></span>
1. <span data-ttu-id="77411-182">在使用者入口網站中，選取 [新增]。</span><span class="sxs-lookup"><span data-stu-id="77411-182">In the user portal, select **New**.</span></span> 
2. <span data-ttu-id="77411-183">移至 [Marketplace]，然後選取 [網路]。</span><span class="sxs-lookup"><span data-stu-id="77411-183">Go to **Marketplace**, and then select **Networking**.</span></span>
3. <span data-ttu-id="77411-184">從資源清單中，選取 [連線]。</span><span class="sxs-lookup"><span data-stu-id="77411-184">From the list of resources, select **Connection**.</span></span>
4. <span data-ttu-id="77411-185">在 [基本] 設定區段的 [連線類型] 中，選擇 [站對站 (IPSec)]。</span><span class="sxs-lookup"><span data-stu-id="77411-185">On the **Basic** settings section, for the **Connection type**, choose **Site-to-site (IPSec)**.</span></span>
5. <span data-ttu-id="77411-186">選取 [訂用帳戶]、[資源群組] 和 [位置]，然後選取 [確定]。</span><span class="sxs-lookup"><span data-stu-id="77411-186">Select the **Subscription**, **Resource Group**, and **Location**, and then select **OK**.</span></span>
6. <span data-ttu-id="77411-187">在 [設定] 區段上，選取 [虛擬網路閘道]，然後選取 [Azure-GW]。</span><span class="sxs-lookup"><span data-stu-id="77411-187">On the **Settings** section, select **Virtual network gateway**, and then select **Azure-GW**.</span></span>
7. <span data-ttu-id="77411-188">選取 [區域網路閘道]，然後選取 [Azs-GW]。</span><span class="sxs-lookup"><span data-stu-id="77411-188">Select **Local network gateway**, and then select **Azs-GW**.</span></span>
8. <span data-ttu-id="77411-189">在 [連線名稱] 中，輸入 **Azure-Azs**。</span><span class="sxs-lookup"><span data-stu-id="77411-189">In **Connection name**, type **Azure-Azs**.</span></span>
9. <span data-ttu-id="77411-190">在 [共用金鑰 (PSK)] 中，輸入 **12345**。</span><span class="sxs-lookup"><span data-stu-id="77411-190">In **Shared key (PSK)**, type **12345**.</span></span> <span data-ttu-id="77411-191">如果您選擇不同的值，請記住該值與您在連線另一端建立的共用金鑰值「必須」相符。</span><span class="sxs-lookup"><span data-stu-id="77411-191">If you choose a different value, remember that it *must* match the value for the shared key that you create on the other end of the connection.</span></span> <span data-ttu-id="77411-192">選取 [確定] 。</span><span class="sxs-lookup"><span data-stu-id="77411-192">Select **OK**.</span></span>
10. <span data-ttu-id="77411-193">檢閱 [摘要] 區段，然後選取 [確定]。</span><span class="sxs-lookup"><span data-stu-id="77411-193">Review the **Summary** section, and then select **OK**.</span></span>

## <a name="create-a-virtual-machine"></a><span data-ttu-id="77411-194">建立虛擬機器</span><span class="sxs-lookup"><span data-stu-id="77411-194">Create a virtual machine</span></span>
<span data-ttu-id="77411-195">現在，請在 Azure 中建立虛擬機器，然後放入虛擬網路中的 VM 子網路上。</span><span class="sxs-lookup"><span data-stu-id="77411-195">Create a virtual machine in Azure now, and put it on your VM subnet in your virtual network.</span></span>

1. <span data-ttu-id="77411-196">在 Azure 入口網站中，選取 [新增]。</span><span class="sxs-lookup"><span data-stu-id="77411-196">In the Azure portal, select **New**.</span></span>
2. <span data-ttu-id="77411-197">移至 [Marketplace]，然後選取 [計算]。</span><span class="sxs-lookup"><span data-stu-id="77411-197">Go to **Marketplace**, and then select **Compute**.</span></span>
3. <span data-ttu-id="77411-198">在虛擬機器映像清單中，選取 [Windows Server 2016 Datacenter 評估版] 映像。</span><span class="sxs-lookup"><span data-stu-id="77411-198">In the list of virtual machine images, select the **Windows Server 2016 Datacenter Eval** image.</span></span>
4. <span data-ttu-id="77411-199">在 [基本] 區段的 [名稱] 中，輸入 **AzureVM**。</span><span class="sxs-lookup"><span data-stu-id="77411-199">On the **Basics** section, for **Name**, type **AzureVM**.</span></span>
5. <span data-ttu-id="77411-200">輸入有效的使用者名稱和密碼。</span><span class="sxs-lookup"><span data-stu-id="77411-200">Type a valid username and password.</span></span> <span data-ttu-id="77411-201">建立虛擬機器之後，您將使用此帳戶來登入虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="77411-201">You use this account to sign in to the virtual machine after it's created.</span></span>
6. <span data-ttu-id="77411-202">提供 [訂用帳戶]、[資源群組] 和 [位置]，然後選取 [確定]。</span><span class="sxs-lookup"><span data-stu-id="77411-202">Provide a **Subscription**, **Resource Group**, and **Location**, and then select **OK**.</span></span>
7. <span data-ttu-id="77411-203">在 [大小] 區段上，選取此執行個體的虛擬機器大小，然後選取 [選取]。</span><span class="sxs-lookup"><span data-stu-id="77411-203">On the **Size** section, select a virtual machine size for this instance, and then select **Select**.</span></span>
8. <span data-ttu-id="77411-204">在 [設定] 區段上，您可以接受預設值。</span><span class="sxs-lookup"><span data-stu-id="77411-204">On the **Settings** section, you can accept the defaults.</span></span> <span data-ttu-id="77411-205">確定已選取 [AzureVnet] 虛擬網路，並確認子網路已設定為 **10.0.20.0/24**。</span><span class="sxs-lookup"><span data-stu-id="77411-205">Make sure that the **AzureVnet** virtual network is selected, and verify that the subnet is set to **10.0.20.0/24**.</span></span> <span data-ttu-id="77411-206">選取 [確定] 。</span><span class="sxs-lookup"><span data-stu-id="77411-206">Select **OK**.</span></span>
9. <span data-ttu-id="77411-207">檢閱 [摘要] 區段上的設定，然後選取 [確定]。</span><span class="sxs-lookup"><span data-stu-id="77411-207">Review the settings on the **Summary** section, and then select **OK**.</span></span>

## <a name="create-the-network-resources-in-azure-stack"></a><span data-ttu-id="77411-208">在 Azure Stack 中建立網路資源</span><span class="sxs-lookup"><span data-stu-id="77411-208">Create the network resources in Azure Stack</span></span>
<span data-ttu-id="77411-209">接下來，請在 Azure Stack 中建立網路資源。</span><span class="sxs-lookup"><span data-stu-id="77411-209">Next you create the network resources in Azure Stack.</span></span>

### <a name="sign-in-as-a-user"></a><span data-ttu-id="77411-210">以使用者身分登入</span><span class="sxs-lookup"><span data-stu-id="77411-210">Sign in as a user</span></span>
<span data-ttu-id="77411-211">服務系統管理員可以用使用者身分登入，以測試其使用者可能使用的方案、供應項目及訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="77411-211">A service administrator can sign in as a user to test the plans, offers, and subscriptions that their users might use.</span></span> <span data-ttu-id="77411-212">如果您還沒有使用者帳戶，請先[建立使用者帳戶](azure-stack-add-new-user-aad.md)再登入。</span><span class="sxs-lookup"><span data-stu-id="77411-212">If you don’t already have one, [create a user account](azure-stack-add-new-user-aad.md) before you sign in.</span></span>

### <a name="create-the-virtual-network-and-vm-subnet"></a><span data-ttu-id="77411-213">建立虛擬網路和 VM 子網路</span><span class="sxs-lookup"><span data-stu-id="77411-213">Create the virtual network and VM subnet</span></span>
1. <span data-ttu-id="77411-214">以使用者帳戶來登入使用者入口網站。</span><span class="sxs-lookup"><span data-stu-id="77411-214">Use a user account to sign in to the user portal.</span></span>
2. <span data-ttu-id="77411-215">在使用者入口網站中，選取 [新增]。</span><span class="sxs-lookup"><span data-stu-id="77411-215">In the user portal, select **New**.</span></span>

    ![建立新的虛擬網路](media/azure-stack-create-vpn-connection-one-node-tp2/image3.png)

3. <span data-ttu-id="77411-217">移至 [Marketplace]，然後選取 [網路]。</span><span class="sxs-lookup"><span data-stu-id="77411-217">Go to **Marketplace**, and then select **Networking**.</span></span>
4. <span data-ttu-id="77411-218">選取 [虛擬網路]。</span><span class="sxs-lookup"><span data-stu-id="77411-218">Select **Virtual network**.</span></span>
5. <span data-ttu-id="77411-219">在 [名稱]、[位址空間]、[子網路名稱] 及 [子網路位址範圍] 中，使用網路設定表中的值。</span><span class="sxs-lookup"><span data-stu-id="77411-219">For **Name**, **Address space**, **Subnet name**, and **Subnet address range**, use the values from the network configuration table.</span></span>
6. <span data-ttu-id="77411-220">在 [訂用帳戶] 中，會顯示您先前建立的訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="77411-220">In **Subscription**, the subscription that you created earlier appears.</span></span>
7. <span data-ttu-id="77411-221">針對 [資源群組]，您可以建立資源群組，或選取 [使用現有的] \(如果您已經有資源群組)。</span><span class="sxs-lookup"><span data-stu-id="77411-221">For **Resource Group**, you can either create a resource group or if you already have one, select **Use existing**.</span></span>
8. <span data-ttu-id="77411-222">驗證預設位置。</span><span class="sxs-lookup"><span data-stu-id="77411-222">Verify the default location.</span></span>
9. <span data-ttu-id="77411-223">選取 [釘選到儀表板]。</span><span class="sxs-lookup"><span data-stu-id="77411-223">Select **Pin to dashboard**.</span></span>
10. <span data-ttu-id="77411-224">選取 [ **建立**]。</span><span class="sxs-lookup"><span data-stu-id="77411-224">Select **Create**.</span></span>

### <a name="create-the-gateway-subnet"></a><span data-ttu-id="77411-225">建立閘道子網路</span><span class="sxs-lookup"><span data-stu-id="77411-225">Create the gateway subnet</span></span>
1. <span data-ttu-id="77411-226">在儀表板上，開啟您建立的 Azs-VNet 虛擬網路資源。</span><span class="sxs-lookup"><span data-stu-id="77411-226">On the dashboard, open the Azs-VNet virtual network resource you created.</span></span>
2. <span data-ttu-id="77411-227">在 [設定] 區段上，選取 [子網路]。</span><span class="sxs-lookup"><span data-stu-id="77411-227">On the **Settings** section, select **Subnets**.</span></span>
3. <span data-ttu-id="77411-228">若要將閘道子網路新增到虛擬網路，請選取 [閘道子網路]。</span><span class="sxs-lookup"><span data-stu-id="77411-228">To add a gateway subnet to the virtual network, select **Gateway Subnet**.</span></span>
   
    ![新增閘道子網路](media/azure-stack-create-vpn-connection-one-node-tp2/image4.png)

4. <span data-ttu-id="77411-230">子網路名稱預設為 **GatewaySubnet**。</span><span class="sxs-lookup"><span data-stu-id="77411-230">By default, the subnet name is set to **GatewaySubnet**.</span></span>
   <span data-ttu-id="77411-231">閘道子網路相當特殊。</span><span class="sxs-lookup"><span data-stu-id="77411-231">Gateway subnets are special.</span></span> <span data-ttu-id="77411-232">為了正常運作，它們必須使用 *GatewaySubnet* 名稱。</span><span class="sxs-lookup"><span data-stu-id="77411-232">To function properly, they must use the *GatewaySubnet* name.</span></span>
5. <span data-ttu-id="77411-233">在 [位址範圍] 中，確認位址是 **10.1.1.0/24**。</span><span class="sxs-lookup"><span data-stu-id="77411-233">In **Address range**, verify that the address is **10.1.1.0/24**.</span></span>
6. <span data-ttu-id="77411-234">選取 [確定] 以建立閘道子網路。</span><span class="sxs-lookup"><span data-stu-id="77411-234">Select **OK** to create the gateway subnet.</span></span>

### <a name="create-the-virtual-network-gateway"></a><span data-ttu-id="77411-235">建立虛擬網路閘道</span><span class="sxs-lookup"><span data-stu-id="77411-235">Create the virtual network gateway</span></span>
1. <span data-ttu-id="77411-236">在 Azure Stack 入口網站中，選取 [新增]。</span><span class="sxs-lookup"><span data-stu-id="77411-236">In the Azure Stack portal, select **New**.</span></span> 
2. <span data-ttu-id="77411-237">移至 [Marketplace]，然後選取 [網路]。</span><span class="sxs-lookup"><span data-stu-id="77411-237">Go to **Marketplace**, and then select **Networking**.</span></span>
3. <span data-ttu-id="77411-238">從網路資源清單中，選取 [虛擬網路閘道]。</span><span class="sxs-lookup"><span data-stu-id="77411-238">From the list of network resources, select **Virtual network gateway**.</span></span>
4. <span data-ttu-id="77411-239">在 [名稱] 中輸入 **Azs-GW**。</span><span class="sxs-lookup"><span data-stu-id="77411-239">In **Name**, type **Azs-GW**.</span></span>
5. <span data-ttu-id="77411-240">選取 [虛擬網路] 項目以選擇虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="77411-240">Select the **Virtual network** item to choose a virtual network.</span></span>
   <span data-ttu-id="77411-241">從清單中選取 [Azs-VNet]。</span><span class="sxs-lookup"><span data-stu-id="77411-241">Select **Azs-VNet** from the list.</span></span>
6. <span data-ttu-id="77411-242">選取 [公用 IP 位址] 功能表項目。</span><span class="sxs-lookup"><span data-stu-id="77411-242">Select the **Public IP address** menu item.</span></span> <span data-ttu-id="77411-243">當 [選擇公用 IP 位址] 區段開啟時，請選取 [新建]。</span><span class="sxs-lookup"><span data-stu-id="77411-243">When the **Choose public IP address** section opens, select **Create new**.</span></span>
7. <span data-ttu-id="77411-244">在 [名稱] 中輸入 **Azs-GW-PiP**，然後選取 [確定]。</span><span class="sxs-lookup"><span data-stu-id="77411-244">In **Name**, type **Azs-GW-PiP**, and then select **OK**.</span></span>
8.  <span data-ttu-id="77411-245">針對 [VPN 類型]，預設會選取 [依路由]。</span><span class="sxs-lookup"><span data-stu-id="77411-245">By default, for **VPN type**, **Route-based** is selected.</span></span>
    <span data-ttu-id="77411-246">保留 [依路由] VPN 類型。</span><span class="sxs-lookup"><span data-stu-id="77411-246">Keep the **Route-based** VPN type.</span></span>
9. <span data-ttu-id="77411-247">確認 [訂用帳戶] 和 [位置] 均正確無誤。</span><span class="sxs-lookup"><span data-stu-id="77411-247">Verify that **Subscription** and **Location** are correct.</span></span> <span data-ttu-id="77411-248">您可以將資源釘選到儀表板。</span><span class="sxs-lookup"><span data-stu-id="77411-248">You can pin the resource to the dashboard.</span></span> <span data-ttu-id="77411-249">選取 [ **建立**]。</span><span class="sxs-lookup"><span data-stu-id="77411-249">Select **Create**.</span></span>

### <a name="create-the-local-network-gateway"></a><span data-ttu-id="77411-250">建立區域網路閘道</span><span class="sxs-lookup"><span data-stu-id="77411-250">Create the local network gateway</span></span>
<span data-ttu-id="77411-251">在 Azure Stack 中，「區域網路閘道」的概念稍微不同於 Azure 部署。</span><span class="sxs-lookup"><span data-stu-id="77411-251">The notion of a *local network gateway* in Azure Stack is a bit different than in an Azure deployment.</span></span>

<span data-ttu-id="77411-252">在 Azure 部署中，區域網路閘道代表內部部署 (位於使用者位置) 實體裝置，用於連線至 Azure 中的虛擬網路閘道。</span><span class="sxs-lookup"><span data-stu-id="77411-252">In an Azure deployment, a local network gateway represents an on-premises (at the user location) physical device, that you use to connect to a virtual network gateway in Azure.</span></span> <span data-ttu-id="77411-253">在 Azure Stack 中，連線的兩端都是虛擬網路閘道！</span><span class="sxs-lookup"><span data-stu-id="77411-253">In Azure Stack, both ends of the connection are virtual network gateways!</span></span>

<span data-ttu-id="77411-254">更廣泛來說，區域網路閘道資源一律是指連線另一端的遠端閘道。</span><span class="sxs-lookup"><span data-stu-id="77411-254">A way to think about this more generically is that the local network gateway resource always indicates the remote gateway at the other end of the connection.</span></span> 

### <a name="create-the-local-network-gateway-resource"></a><span data-ttu-id="77411-255">建立區域網路閘道資源</span><span class="sxs-lookup"><span data-stu-id="77411-255">Create the local network gateway resource</span></span>
1. <span data-ttu-id="77411-256">登入 Azure Stack 入口網站。</span><span class="sxs-lookup"><span data-stu-id="77411-256">Sign in to the Azure Stack portal.</span></span>
2. <span data-ttu-id="77411-257">在使用者入口網站中，選取 [新增]。</span><span class="sxs-lookup"><span data-stu-id="77411-257">In the user portal, select **New**.</span></span>
3. <span data-ttu-id="77411-258">移至 [Marketplace]，然後選取 [網路]。</span><span class="sxs-lookup"><span data-stu-id="77411-258">Go to **Marketplace**, and then select **Networking**.</span></span>
4. <span data-ttu-id="77411-259">從資源清單中，選取 [區域網路閘道]。</span><span class="sxs-lookup"><span data-stu-id="77411-259">From the list of resources, select **local network gateway**.</span></span>
5. <span data-ttu-id="77411-260">在 [名稱] 中輸入 **Azure-GW**。</span><span class="sxs-lookup"><span data-stu-id="77411-260">In **Name**, type **Azure-GW**.</span></span>
6. <span data-ttu-id="77411-261">在 [IP 位址] 中，輸入 Azure **Azure-GW-PiP** 中的虛擬網路閘道公用 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="77411-261">In **IP address**, type the Public IP Address for the virtual network gateway in Azure **Azure-GW-PiP**.</span></span> <span data-ttu-id="77411-262">此位址先前已顯示在網路組態表中。</span><span class="sxs-lookup"><span data-stu-id="77411-262">This address appears earlier in the network configuration table.</span></span>
7. <span data-ttu-id="77411-263">在 [位址空間] 中，輸入 **10.0.20.0/23**，代表您已建立之 Azure VNET 的位址空間。</span><span class="sxs-lookup"><span data-stu-id="77411-263">In **Address Space**, for the address space of the Azure VNET that you created, type **10.0.20.0/23**.</span></span>
8. <span data-ttu-id="77411-264">確認您的 [訂用帳戶]、[資源群組] 和 [位置] 正確無誤，然後選取 [建立]。</span><span class="sxs-lookup"><span data-stu-id="77411-264">Verify that your **Subscription**, **Resource Group**, and **location** are correct, and then select **Create**.</span></span>

### <a name="create-the-connection"></a><span data-ttu-id="77411-265">建立連線</span><span class="sxs-lookup"><span data-stu-id="77411-265">Create the connection</span></span>
1. <span data-ttu-id="77411-266">在使用者入口網站中，選取 [新增]。</span><span class="sxs-lookup"><span data-stu-id="77411-266">In the user portal, select **New**.</span></span>
2. <span data-ttu-id="77411-267">移至 [Marketplace]，然後選取 [網路]。</span><span class="sxs-lookup"><span data-stu-id="77411-267">Go to **Marketplace**, and then select **Networking**.</span></span>
3. <span data-ttu-id="77411-268">從資源清單中，選取 [連線]。</span><span class="sxs-lookup"><span data-stu-id="77411-268">From the list of resources, select **Connection**.</span></span>
4. <span data-ttu-id="77411-269">在 [基本] 設定區段的 [連線類型] 中，選取 [站對站 (IPSec)]。</span><span class="sxs-lookup"><span data-stu-id="77411-269">On the **Basics** settings section, for the **Connection type**, select **Site-to-site (IPSec)**.</span></span>
5. <span data-ttu-id="77411-270">選取 [訂用帳戶]、[資源群組] 和 [位置]，然後選取 [確定]。</span><span class="sxs-lookup"><span data-stu-id="77411-270">Select the **Subscription**, **Resource Group**, and **Location**, and then select **OK**.</span></span>
6. <span data-ttu-id="77411-271">在 [設定] 區段上，選取 [虛擬網路閘道]，然後選取 [Azs-GW]。</span><span class="sxs-lookup"><span data-stu-id="77411-271">On the **Settings** section,  select **Virtual network gateway**, and then select **Azs-GW**.</span></span>
7. <span data-ttu-id="77411-272">選取 區域網路閘道，然後選取 Azure-GW。</span><span class="sxs-lookup"><span data-stu-id="77411-272">Select **Local network gateway**, and then select **Azure-GW**.</span></span>
8. <span data-ttu-id="77411-273">在 [連線名稱] 中，輸入 **Azs-Azure**。</span><span class="sxs-lookup"><span data-stu-id="77411-273">In **Connection Name**, type **Azs-Azure**.</span></span>
9. <span data-ttu-id="77411-274">在 [共用金鑰 (PSK)] 中輸入 **12345**，然後選取 [確定]。</span><span class="sxs-lookup"><span data-stu-id="77411-274">In **Shared key (PSK)**, type **12345**, and then select **OK**.</span></span>
10. <span data-ttu-id="77411-275">在 [摘要] 區段上，選取 [確定]。</span><span class="sxs-lookup"><span data-stu-id="77411-275">On the **Summary** section, select **OK**.</span></span>

### <a name="create-a-vm"></a><span data-ttu-id="77411-276">建立 VM</span><span class="sxs-lookup"><span data-stu-id="77411-276">Create a VM</span></span>
<span data-ttu-id="77411-277">若要驗證透過 VPN 連線傳輸的資料，您需要在兩端都建立虛擬機器，以透過 VPN 通道傳送和接收資料。</span><span class="sxs-lookup"><span data-stu-id="77411-277">To validate the data that travels through the VPN connection, you need to create virtual machines on each end to send and receive data through the VPN tunnel.</span></span> 

1. <span data-ttu-id="77411-278">在 Azure 入口網站中，選取 [新增]。</span><span class="sxs-lookup"><span data-stu-id="77411-278">In the Azure portal, select **New**.</span></span>
2. <span data-ttu-id="77411-279">移至 [Marketplace]，然後選取 [計算]。</span><span class="sxs-lookup"><span data-stu-id="77411-279">Go to **Marketplace**, and then select **Compute**.</span></span>
3. <span data-ttu-id="77411-280">在虛擬機器映像清單中，選取 [Windows Server 2016 Datacenter 評估版] 映像。</span><span class="sxs-lookup"><span data-stu-id="77411-280">In the list of virtual machine images, select the **Windows Server 2016 Datacenter Eval** image.</span></span>
4. <span data-ttu-id="77411-281">在 [基本] 區段的 [名稱] 中，輸入 **Azs-VM**。</span><span class="sxs-lookup"><span data-stu-id="77411-281">On the **Basics** section, in **Name**, type **Azs-VM**.</span></span>
5. <span data-ttu-id="77411-282">輸入有效的使用者名稱和密碼。</span><span class="sxs-lookup"><span data-stu-id="77411-282">Type a valid username and password.</span></span> <span data-ttu-id="77411-283">建立 VM 之後，您將使用此帳戶來登入 VM。</span><span class="sxs-lookup"><span data-stu-id="77411-283">You use this account to sign in to the VM after it's created.</span></span>
6. <span data-ttu-id="77411-284">提供 [訂用帳戶]、[資源群組] 和 [位置]，然後選取 [確定]。</span><span class="sxs-lookup"><span data-stu-id="77411-284">Provide a **Subscription**, **Resource Group**, and **Location**, and then select **OK**.</span></span>
7. <span data-ttu-id="77411-285">在 [大小] 區段，選取此執行個體的虛擬機器大小，然後選取 [選取]。</span><span class="sxs-lookup"><span data-stu-id="77411-285">On the **Size** section, for this instance, select a virtual machine size, and then select **Select**.</span></span>
8. <span data-ttu-id="77411-286">在 [設定] 區段上，接受預設值。</span><span class="sxs-lookup"><span data-stu-id="77411-286">On the **Settings** section, accept the defaults.</span></span> <span data-ttu-id="77411-287">確定已選取 [Azs-VNet] 虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="77411-287">Make sure that the **Azs-VNet** virtual network is selected.</span></span> <span data-ttu-id="77411-288">確認子網路已設定為 **10.1.0.0/24**。</span><span class="sxs-lookup"><span data-stu-id="77411-288">Verify that the subnet is set to **10.1.0.0/24**.</span></span> <span data-ttu-id="77411-289">然後選取 [確定]。</span><span class="sxs-lookup"><span data-stu-id="77411-289">Then select **OK**.</span></span>
9. <span data-ttu-id="77411-290">在 [摘要] 區段上檢視設定，然後選取 [確定]。</span><span class="sxs-lookup"><span data-stu-id="77411-290">On the **Summary** section, review the settings, and then select **OK**.</span></span>


## <a name="test-the-connection"></a><span data-ttu-id="77411-291">測試連線</span><span class="sxs-lookup"><span data-stu-id="77411-291">Test the connection</span></span>
<span data-ttu-id="77411-292">既然已建立站對站連線，您現在應驗證是否可以透過它傳送流量。</span><span class="sxs-lookup"><span data-stu-id="77411-292">Now that the site-to-site connection is established, you should validate that you can get traffic flowing through it.</span></span> <span data-ttu-id="77411-293">若要驗證，請登入您在 Azure Stack 中建立的其中一個虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="77411-293">To validate, sign in to one of the virtual machines that you created in Azure Stack.</span></span> <span data-ttu-id="77411-294">接著，偵測您在 Azure 中建立的虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="77411-294">Then, ping the virtual machine that you created in Azure.</span></span> 

<span data-ttu-id="77411-295">為了確保您是透過站對站連線傳送流量，請偵測遠端子網路上之虛擬機器的直接 IP (DIP) 位址，而非 VIP。</span><span class="sxs-lookup"><span data-stu-id="77411-295">To make sure that you send the traffic through the site-to-site connection, ping the Direct IP (DIP) address of the virtual machine on the remote subnet, not the VIP.</span></span> <span data-ttu-id="77411-296">若要這麼做，請找出連線另一端的 DIP 位址。</span><span class="sxs-lookup"><span data-stu-id="77411-296">To do this, find the DIP address on the other end of the connection.</span></span> <span data-ttu-id="77411-297">儲存位址以供稍後使用。</span><span class="sxs-lookup"><span data-stu-id="77411-297">Save the address for later use.</span></span>

### <a name="sign-in-to-the-user-vm-in-azure-stack"></a><span data-ttu-id="77411-298">登入 Azure Stack 中的使用者 VM</span><span class="sxs-lookup"><span data-stu-id="77411-298">Sign in to the user VM in Azure Stack</span></span>
1. <span data-ttu-id="77411-299">登入 Azure Stack 入口網站。</span><span class="sxs-lookup"><span data-stu-id="77411-299">Sign in to the Azure Stack portal.</span></span>
2. <span data-ttu-id="77411-300">在左側導覽列，選取 [虛擬機器]。</span><span class="sxs-lookup"><span data-stu-id="77411-300">In the left navigation bar, select **Virtual Machines**.</span></span>
3. <span data-ttu-id="77411-301">在 VM 清單中，尋找並選取您先前建立的 **Azs-VM**。</span><span class="sxs-lookup"><span data-stu-id="77411-301">In the list of VMs, find **Azs-VM** that you created previously, and then select it.</span></span>
4. <span data-ttu-id="77411-302">在虛擬機器的區段上，按一下 [連線]，然後開啟 Azs-VM.rdp 檔案。</span><span class="sxs-lookup"><span data-stu-id="77411-302">On the section for the virtual machine, click **Connect**, and then open the Azs-VM.rdp file.</span></span>
   
     ![[連線] 按鈕](media/azure-stack-create-vpn-connection-one-node-tp2/image17.png)
5. <span data-ttu-id="77411-304">使用您建立虛擬網路時所設定的帳戶來登入。</span><span class="sxs-lookup"><span data-stu-id="77411-304">Sign in with the account that you configured when you created the virtual machine.</span></span>
6. <span data-ttu-id="77411-305">開啟已提高權限的 [Windows PowerShell] 視窗。</span><span class="sxs-lookup"><span data-stu-id="77411-305">Open an elevated **Windows PowerShell** window.</span></span>
7. <span data-ttu-id="77411-306">輸入 **ipconfig /all**。</span><span class="sxs-lookup"><span data-stu-id="77411-306">Type **ipconfig /all**.</span></span>
8. <span data-ttu-id="77411-307">在輸出中，尋找「IPv4 位址」，然後儲存該位址以供稍後使用。</span><span class="sxs-lookup"><span data-stu-id="77411-307">In the output, find the **IPv4 Address**, and then save the address for later use.</span></span> <span data-ttu-id="77411-308">這是您將從 Azure 偵測的位址。</span><span class="sxs-lookup"><span data-stu-id="77411-308">This is the address that you will ping from Azure.</span></span> <span data-ttu-id="77411-309">在範例環境中，位址是 **10.0.10.4**，但在您的環境中可能會不同。</span><span class="sxs-lookup"><span data-stu-id="77411-309">In the example environment, the address is **10.0.10.4**, but in your environment it might be different.</span></span> <span data-ttu-id="77411-310">它應該落在您先前建立的 **10.0.10.0/24** 子網路內。</span><span class="sxs-lookup"><span data-stu-id="77411-310">It should fall within the **10.0.10.0/24** subnet that you created previously.</span></span>
9. <span data-ttu-id="77411-311">若要建立允許虛擬機器回應 Ping 的防火牆規則，請執行下列 PowerShell 命令：</span><span class="sxs-lookup"><span data-stu-id="77411-311">To create a firewall rule that allows the virtual machine to respond to pings, run the following PowerShell command:</span></span>

   ```powershell
   New-NetFirewallRule `
    –DisplayName “Allow ICMPv4-In” `
    –Protocol ICMPv4
   ```

### <a name="sign-in-to-the-tenant-vm-in-azure"></a><span data-ttu-id="77411-312">登入 Azure 中的租用戶 VM</span><span class="sxs-lookup"><span data-stu-id="77411-312">Sign in to the tenant VM in Azure</span></span>
1. <span data-ttu-id="77411-313">登入 Azure 入口網站。</span><span class="sxs-lookup"><span data-stu-id="77411-313">Sign in to the Azure portal.</span></span>
2. <span data-ttu-id="77411-314">在左側導覽列，按一下 [虛擬機器]。</span><span class="sxs-lookup"><span data-stu-id="77411-314">In the left navigation bar, click **Virtual Machines**.</span></span>
3. <span data-ttu-id="77411-315">從虛擬機器清單中，尋找並選取您先前建立的 **Azure-VM**。</span><span class="sxs-lookup"><span data-stu-id="77411-315">From the list of virtual machines, find **Azure-VM** that you created previously, and then select it.</span></span>
4. <span data-ttu-id="77411-316">在虛擬機器的區段上，按一下 [連線]。</span><span class="sxs-lookup"><span data-stu-id="77411-316">On the section for the virtual machine, click **Connect**.</span></span>
5. <span data-ttu-id="77411-317">使用您建立虛擬網路時所設定的帳戶來登入。</span><span class="sxs-lookup"><span data-stu-id="77411-317">Sign in with the account that you configured when you created the virtual machine.</span></span>
6. <span data-ttu-id="77411-318">開啟已提高權限的 [Windows PowerShell] 視窗。</span><span class="sxs-lookup"><span data-stu-id="77411-318">Open an elevated **Windows PowerShell** window.</span></span>
7. <span data-ttu-id="77411-319">輸入 **ipconfig /all**。</span><span class="sxs-lookup"><span data-stu-id="77411-319">Type **ipconfig /all**.</span></span>
8. <span data-ttu-id="77411-320">您應該會看到落在 **10.0.20.0/24** 內的 IPv4 位址。</span><span class="sxs-lookup"><span data-stu-id="77411-320">You should see an IPv4 address that falls within **10.0.20.0/24**.</span></span> <span data-ttu-id="77411-321">在範例環境中，該位址是 **10.0.20.4**，但您的位址可能會不同。</span><span class="sxs-lookup"><span data-stu-id="77411-321">In the example environment, the address is **10.0.20.4**, but your address might be different.</span></span>
9. <span data-ttu-id="77411-322">若要建立允許虛擬機器回應 Ping 的防火牆規則，請執行下列 PowerShell 命令：</span><span class="sxs-lookup"><span data-stu-id="77411-322">To create a firewall rule that allows the virtual machine to respond to pings, run the following PowerShell command:</span></span>

   ```powershell
   New-NetFirewallRule `
    –DisplayName “Allow ICMPv4-In” `
    –Protocol ICMPv4
   ```

10. <span data-ttu-id="77411-323">從 Azure 中的虛擬機器，透過通道偵測 Azure Stack 中的虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="77411-323">From the virtual machine in Azure, ping the virtual machine in Azure Stack, through the tunnel.</span></span> <span data-ttu-id="77411-324">若要這麼做，請偵測您從 Azs-VM 記錄的 DIP。</span><span class="sxs-lookup"><span data-stu-id="77411-324">To do this, you ping the DIP that you recorded from Azs-VM.</span></span>
   <span data-ttu-id="77411-325">在範例環境中，這是 **10.0.10.4**，但請務必 Ping 您在實驗室中記下的位址。</span><span class="sxs-lookup"><span data-stu-id="77411-325">In the example environment, this is **10.0.10.4**, but be sure to ping the address you noted in your lab.</span></span> <span data-ttu-id="77411-326">您應該會看到如下列螢幕擷取畫面的結果：</span><span class="sxs-lookup"><span data-stu-id="77411-326">You should see a result that looks like the following screenshot:</span></span>
   
    ![成功的 Ping](media/azure-stack-create-vpn-connection-one-node-tp2/image19b.png)
11. <span data-ttu-id="77411-328">來自遠端虛擬機器的回覆表示測試成功！</span><span class="sxs-lookup"><span data-stu-id="77411-328">A reply from the remote virtual machine indicates a successful test!</span></span> <span data-ttu-id="77411-329">您可以關閉虛擬機器視窗。</span><span class="sxs-lookup"><span data-stu-id="77411-329">You can close the virtual machine window.</span></span> <span data-ttu-id="77411-330">若要測試您的連線，您可以嘗試其他類型的資料傳輸，例如檔案複製。</span><span class="sxs-lookup"><span data-stu-id="77411-330">To test your connection, you can try other kinds of data transfers like a file copy.</span></span>

### <a name="viewing-data-transfer-statistics-through-the-gateway-connection"></a><span data-ttu-id="77411-331">檢視透過閘道連線的資料傳輸統計資料</span><span class="sxs-lookup"><span data-stu-id="77411-331">Viewing data transfer statistics through the gateway connection</span></span>
<span data-ttu-id="77411-332">如果想要知道有多少資料通過您的站對站連線，您可以在 [連線] 區段上取得此資訊。</span><span class="sxs-lookup"><span data-stu-id="77411-332">If you want to know how much data passes through your site-to-site connection, this information is available on the **Connection** section.</span></span> <span data-ttu-id="77411-333">此測試也是確認您剛傳送的 Ping 是否真的通過 VPN 連線的另一種方法。</span><span class="sxs-lookup"><span data-stu-id="77411-333">This test is also another way to verify that the ping you just sent actually went through the VPN connection.</span></span>

1. <span data-ttu-id="77411-334">登入 Azure Stack 中的使用者虛擬機器之後，請使用您的使用者帳戶來登入使用者入口網站。</span><span class="sxs-lookup"><span data-stu-id="77411-334">While you're signed in to the user virtual machine in Azure Stack, use your user account to sign in to the user portal.</span></span>
2. <span data-ttu-id="77411-335">移至 [所有資源]，然後選取 [Azs-Azure] 連線。</span><span class="sxs-lookup"><span data-stu-id="77411-335">Go to **All resources**, and then select the **Azs-Azure** connection.</span></span> <span data-ttu-id="77411-336">[連線] 隨即顯示。</span><span class="sxs-lookup"><span data-stu-id="77411-336">**Connections** appears.</span></span>
4. <span data-ttu-id="77411-337">[連線] 區段上會顯示 [資料輸入] 和 [資料輸出] 的統計資料。</span><span class="sxs-lookup"><span data-stu-id="77411-337">On the **Connection** section, the statistics for **Data in** and **Data out** appear.</span></span> <span data-ttu-id="77411-338">在以下的螢幕擷取畫面中，那些大的數字歸因於額外的檔案傳輸。</span><span class="sxs-lookup"><span data-stu-id="77411-338">In the following screenshot, the large numbers are attributed to additional file transfer.</span></span> <span data-ttu-id="77411-339">您應該會在該處看到一些非零的值。</span><span class="sxs-lookup"><span data-stu-id="77411-339">You should see some nonzero values there.</span></span>
   
    ![資料輸入和輸出](media/azure-stack-connect-vpn/Connection.png)

## <a name="next-steps"></a><span data-ttu-id="77411-341">後續步驟</span><span class="sxs-lookup"><span data-stu-id="77411-341">Next steps</span></span>

[<span data-ttu-id="77411-342">將應用程式部署到 Azure 和 Azure Stack</span><span class="sxs-lookup"><span data-stu-id="77411-342">Deploy apps to Azure and Azure Stack</span></span>](azure-stack-solution-pipeline.md)