---
title: "在不同 Azure Stack 開發套件環境中的兩個虛擬網路之間建立站對站 VPN 連線 |Microsoft Docs"
description: "雲端系統管理員用來在兩個單節點「Azure Stack 開發套件」環境之間建立站對站 VPN 連線的逐步程序。"
services: azure-stack
documentationcenter: 
author: ScottNapolitan
manager: darmour
editor: 
ms.assetid: 3f1b4e02-dbab-46a3-8e11-a777722120ec
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 7/10/2017
ms.author: scottnap
ms.openlocfilehash: fa2a940620e06521fa110fa13dcbc3050635a502
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="create-a-site-to-site-vpn-connection-between-two-virtual-networks-in-different-azure-stack-development-kit-environments"></a><span data-ttu-id="e4cb5-103">在不同 Azure Stack 開發套件環境中的兩個虛擬網路之間建立站對站 VPN 連線</span><span class="sxs-lookup"><span data-stu-id="e4cb5-103">Create a site-to-site VPN connection between two virtual networks in different Azure Stack Development Kit environments</span></span>
## <a name="overview"></a><span data-ttu-id="e4cb5-104">概觀</span><span class="sxs-lookup"><span data-stu-id="e4cb5-104">Overview</span></span>
<span data-ttu-id="e4cb5-105">此文章說明如何在兩個個別「Azure Stack 開發套件」環境中的兩個虛擬網路之間建立站對站 VPN 連線。</span><span class="sxs-lookup"><span data-stu-id="e4cb5-105">This article shows you how to create a site-to-site VPN connection between two virtual networks in two separate Azure Stack Development Kit environments.</span></span> <span data-ttu-id="e4cb5-106">在您設定連線時，會了解 VPN 閘道在 Azure Stack 中的運作方式。</span><span class="sxs-lookup"><span data-stu-id="e4cb5-106">While you configure the connections, you learn how VPN gateways in Azure Stack work.</span></span>

### <a name="connection-diagram"></a><span data-ttu-id="e4cb5-107">連接圖表</span><span class="sxs-lookup"><span data-stu-id="e4cb5-107">Connection diagram</span></span>
<span data-ttu-id="e4cb5-108">下圖顯示當您完成時應有的連線組態。</span><span class="sxs-lookup"><span data-stu-id="e4cb5-108">The following diagram shows what the connection configuration should look like when you’re done.</span></span>

![站對站 VPN 連線組態](media/azure-stack-create-vpn-connection-one-node-tp2/OneNodeS2SVPN.png)

### <a name="before-you-begin"></a><span data-ttu-id="e4cb5-110">開始之前</span><span class="sxs-lookup"><span data-stu-id="e4cb5-110">Before you begin</span></span>
<span data-ttu-id="e4cb5-111">若要完成連線組態，請務必在開始前備妥下列項目：</span><span class="sxs-lookup"><span data-stu-id="e4cb5-111">To complete the connection configuration, ensure that you have the following items before you begin:</span></span>

* <span data-ttu-id="e4cb5-112">兩部符合 [Azure Stack 部署先決條件](azure-stack-deploy.md)所定義之「Azure Stack 開發套件」硬體需求的伺服器。</span><span class="sxs-lookup"><span data-stu-id="e4cb5-112">Two servers that meet the Azure Stack Development Kit hardware requirements, which are defined by the [Azure Stack deployment prerequisites](azure-stack-deploy.md).</span></span> <span data-ttu-id="e4cb5-113">此外，也需確定符合該[文章](azure-stack-deploy.md)中提到的其他先決條件。</span><span class="sxs-lookup"><span data-stu-id="e4cb5-113">Ensure that the other prerequisites that appear in the [article](azure-stack-deploy.md) are fulfilled too.</span></span>
* <span data-ttu-id="e4cb5-114">[Azure Stack 開發套件](https://azure.microsoft.com/en-us/overview/azure-stack/try/)部署套件。</span><span class="sxs-lookup"><span data-stu-id="e4cb5-114">The [Azure Stack Development Kit](https://azure.microsoft.com/en-us/overview/azure-stack/try/) deployment package.</span></span>

## <a name="deploy-the-azure-stack-development-kit-environments"></a><span data-ttu-id="e4cb5-115">部署 Azure Stack 開發套件環境</span><span class="sxs-lookup"><span data-stu-id="e4cb5-115">Deploy the Azure Stack Development Kit environments</span></span>
<span data-ttu-id="e4cb5-116">若要完成連線組態，您必須部署兩個「Azure Stack 開發套件」環境。</span><span class="sxs-lookup"><span data-stu-id="e4cb5-116">To complete the connection configuration, you must deploy two Azure Stack Development Kit environments.</span></span>
> [!NOTE] 
> <span data-ttu-id="e4cb5-117">針對您部署的每個「Azure Stack 開發套件」，依照[部署指示](azure-stack-run-powershell-script.md)操作。</span><span class="sxs-lookup"><span data-stu-id="e4cb5-117">For each Azure Stack Development Kit that you deploy, follow the [deployment instructions](azure-stack-run-powershell-script.md).</span></span> <span data-ttu-id="e4cb5-118">在此文章中，「Azure Stack 開發套件」環境的名稱是 *POC1* 和 *POC2*。</span><span class="sxs-lookup"><span data-stu-id="e4cb5-118">In this article, the Azure Stack Development Kit environments are called *POC1* and *POC2*.</span></span>


## <a name="prepare-an-offer-on-poc1-and-poc2"></a><span data-ttu-id="e4cb5-119">在 POC1 和 POC2 上準備供應項目</span><span class="sxs-lookup"><span data-stu-id="e4cb5-119">Prepare an offer on POC1 and POC2</span></span>
<span data-ttu-id="e4cb5-120">在 POC1 和 POC2 上都準備一個供應項目，以便讓使用者能夠訂閱該供應項目並部署虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="e4cb5-120">On both POC1 and POC2, prepare an offer so that a user can subscribe to the offer and deploy the virtual machines.</span></span> <span data-ttu-id="e4cb5-121">如需有關如何建立供應項目的資訊，請參閱[將虛擬機器提供給您的 Azure Stack 使用者](azure-stack-tutorial-tenant-vm.md)。</span><span class="sxs-lookup"><span data-stu-id="e4cb5-121">For information on how to create an offer, see [Make virtual machines available to your Azure Stack users](azure-stack-tutorial-tenant-vm.md).</span></span>

## <a name="review-and-complete-the-network-configuration-table"></a><span data-ttu-id="e4cb5-122">檢閱並完成網路組態表</span><span class="sxs-lookup"><span data-stu-id="e4cb5-122">Review and complete the network configuration table</span></span>
<span data-ttu-id="e4cb5-123">下表摘要說明這兩個「Azure Stack 開發套件」環境的網路組態。</span><span class="sxs-lookup"><span data-stu-id="e4cb5-123">The following table summarizes the network configuration for both Azure Stack Development Kit environments.</span></span> <span data-ttu-id="e4cb5-124">請使用此表格後面所列的程序來新增您網路特定的外部 BGPNAT 位址。</span><span class="sxs-lookup"><span data-stu-id="e4cb5-124">Use the procedure that appears after the table to add the External BGPNAT address that is specific for your network.</span></span>

<span data-ttu-id="e4cb5-125">**網路組態表**</span><span class="sxs-lookup"><span data-stu-id="e4cb5-125">**Network configuration table**</span></span>
|   |<span data-ttu-id="e4cb5-126">POC1</span><span class="sxs-lookup"><span data-stu-id="e4cb5-126">POC1</span></span>|<span data-ttu-id="e4cb5-127">POC2</span><span class="sxs-lookup"><span data-stu-id="e4cb5-127">POC2</span></span>|
|---------|---------|---------|
|<span data-ttu-id="e4cb5-128">虛擬網路名稱</span><span class="sxs-lookup"><span data-stu-id="e4cb5-128">Virtual network name</span></span>     |<span data-ttu-id="e4cb5-129">VNET-01</span><span class="sxs-lookup"><span data-stu-id="e4cb5-129">VNET-01</span></span>|<span data-ttu-id="e4cb5-130">VNET-02</span><span class="sxs-lookup"><span data-stu-id="e4cb5-130">VNET-02</span></span> |
|<span data-ttu-id="e4cb5-131">虛擬網路位址空間</span><span class="sxs-lookup"><span data-stu-id="e4cb5-131">Virtual network address space</span></span> |<span data-ttu-id="e4cb5-132">10.0.10.0/23</span><span class="sxs-lookup"><span data-stu-id="e4cb5-132">10.0.10.0/23</span></span>|<span data-ttu-id="e4cb5-133">10.0.20.0/23</span><span class="sxs-lookup"><span data-stu-id="e4cb5-133">10.0.20.0/23</span></span>|
|<span data-ttu-id="e4cb5-134">子網路名稱</span><span class="sxs-lookup"><span data-stu-id="e4cb5-134">Subnet name</span></span>     |<span data-ttu-id="e4cb5-135">Subnet-01</span><span class="sxs-lookup"><span data-stu-id="e4cb5-135">Subnet-01</span></span>|<span data-ttu-id="e4cb5-136">Subnet-02</span><span class="sxs-lookup"><span data-stu-id="e4cb5-136">Subnet-02</span></span>|
|<span data-ttu-id="e4cb5-137">子網路位址範圍</span><span class="sxs-lookup"><span data-stu-id="e4cb5-137">Subnet address range</span></span>|<span data-ttu-id="e4cb5-138">10.0.10.0/24</span><span class="sxs-lookup"><span data-stu-id="e4cb5-138">10.0.10.0/24</span></span> |<span data-ttu-id="e4cb5-139">10.0.20.0/24</span><span class="sxs-lookup"><span data-stu-id="e4cb5-139">10.0.20.0/24</span></span> |
|<span data-ttu-id="e4cb5-140">閘道器子網路</span><span class="sxs-lookup"><span data-stu-id="e4cb5-140">Gateway subnet</span></span>     |<span data-ttu-id="e4cb5-141">10.0.11.0/24</span><span class="sxs-lookup"><span data-stu-id="e4cb5-141">10.0.11.0/24</span></span>|<span data-ttu-id="e4cb5-142">10.0.21.0/24</span><span class="sxs-lookup"><span data-stu-id="e4cb5-142">10.0.21.0/24</span></span>|
|<span data-ttu-id="e4cb5-143">外部 BGPNAT 位址</span><span class="sxs-lookup"><span data-stu-id="e4cb5-143">External BGPNAT address</span></span>     |         |         |

> [!NOTE]
> <span data-ttu-id="e4cb5-144">範例環境中的外部 BGPNAT IP 位址是 10.16.167.195 (用於 POC1) 和 10.16.169.131 (用於 POC2)。</span><span class="sxs-lookup"><span data-stu-id="e4cb5-144">The external BGPNAT IP addresses in the example environment are 10.16.167.195 for POC1, and 10.16.169.131 for POC2.</span></span> <span data-ttu-id="e4cb5-145">使用下列程序來決定您「Azure Stack 開發套件」主機的外部 BGPNAT IP 位址，然後將這些位址新增到先前的網路組態表。</span><span class="sxs-lookup"><span data-stu-id="e4cb5-145">Use the following procedure to determine the external BGPNAT IP addresses for your Azure Stack Development Kit hosts, and then add them to the previous network configuration table.</span></span>


### <a name="get-the-ip-address-of-the-external-adapter-of-the-nat-vm"></a><span data-ttu-id="e4cb5-146">取得 NAT VM 的外部介面卡 IP 位址</span><span class="sxs-lookup"><span data-stu-id="e4cb5-146">Get the IP address of the external adapter of the NAT VM</span></span>
1. <span data-ttu-id="e4cb5-147">登入 POC1 的 Azure Stack 實體機器。</span><span class="sxs-lookup"><span data-stu-id="e4cb5-147">Sign in to the Azure Stack physical machine for POC1.</span></span>
2. <span data-ttu-id="e4cb5-148">編輯下列 Powershell 程式碼來取代您的系統管理員密碼，然後在 POC 主機上執行該程式碼：</span><span class="sxs-lookup"><span data-stu-id="e4cb5-148">Edit the following Powershell code to replace your administrator password, and then run the code on the POC host:</span></span>

   ```powershell
   cd \AzureStack-Tools-master\connect
   Import-Module .\AzureStack.Connect.psm1
   $Password = ConvertTo-SecureString "<your administrator password>" `
    -AsPlainText `
    -Force
   Get-AzureStackNatServerAddress `
    -HostComputer "AzS-bgpnat01" `
    -Password $Password
   ```
3. <span data-ttu-id="e4cb5-149">將 IP 位址新增到上一節中出現的網路組態表。</span><span class="sxs-lookup"><span data-stu-id="e4cb5-149">Add the IP address to the network configuration table that appears in the previous section.</span></span>

4. <span data-ttu-id="e4cb5-150">在 POC2 上重複執行此程序。</span><span class="sxs-lookup"><span data-stu-id="e4cb5-150">Repeat this procedure on POC2.</span></span>

## <a name="create-the-network-resources-in-poc1"></a><span data-ttu-id="e4cb5-151">在 POC 1 中建立網路資源</span><span class="sxs-lookup"><span data-stu-id="e4cb5-151">Create the network resources in POC1</span></span>
<span data-ttu-id="e4cb5-152">現在，您將建立設定閘道所需的 POC1 網路資源。</span><span class="sxs-lookup"><span data-stu-id="e4cb5-152">Now you create the POC1 network resources that you need to set up your gateways.</span></span> <span data-ttu-id="e4cb5-153">下列指示說明如何使用使用者入口網站來建立資源。</span><span class="sxs-lookup"><span data-stu-id="e4cb5-153">The following instructions show you how to create the resources by using the user portal.</span></span> <span data-ttu-id="e4cb5-154">您也可以使用 PowerShell 程式碼來建立資源。</span><span class="sxs-lookup"><span data-stu-id="e4cb5-154">You can also use PowerShell code to create the resources.</span></span>

![用來建立資源的工作流程](media/azure-stack-create-vpn-connection-one-node-tp2/image2.png)

### <a name="sign-in-as-a-tenant"></a><span data-ttu-id="e4cb5-156">以租用戶身分登入</span><span class="sxs-lookup"><span data-stu-id="e4cb5-156">Sign in as a tenant</span></span>
<span data-ttu-id="e4cb5-157">服務系統管理員可以用租用戶身分登入，以測試其租用戶可能使用的方案、供應項目及訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="e4cb5-157">A service administrator can sign in as a tenant to test the plans, offers, and subscriptions that their tenants might use.</span></span> <span data-ttu-id="e4cb5-158">如果您還沒有租用戶帳戶，請先[建立租用戶帳戶](azure-stack-add-new-user-aad.md)再登入。</span><span class="sxs-lookup"><span data-stu-id="e4cb5-158">If you don’t already have one, [create a tenant account](azure-stack-add-new-user-aad.md) before you sign in.</span></span>

### <a name="create-the-virtual-network-and-vm-subnet"></a><span data-ttu-id="e4cb5-159">建立虛擬網路和 VM 子網路</span><span class="sxs-lookup"><span data-stu-id="e4cb5-159">Create the virtual network and VM subnet</span></span>
1. <span data-ttu-id="e4cb5-160">使用租用戶帳戶來登入使用者入口網站。</span><span class="sxs-lookup"><span data-stu-id="e4cb5-160">Use a tenant account to sign in to the user portal.</span></span>
2. <span data-ttu-id="e4cb5-161">在使用者入口網站中，選取 [新增]。</span><span class="sxs-lookup"><span data-stu-id="e4cb5-161">In the user portal, select **New**.</span></span>

    ![建立新的虛擬網路](media/azure-stack-create-vpn-connection-one-node-tp2/image3.png)

3. <span data-ttu-id="e4cb5-163">移至 [Marketplace]，然後選取 [網路]。</span><span class="sxs-lookup"><span data-stu-id="e4cb5-163">Go to **Marketplace**, and then select **Networking**.</span></span>
4. <span data-ttu-id="e4cb5-164">選取 [虛擬網路]。</span><span class="sxs-lookup"><span data-stu-id="e4cb5-164">Select **Virtual network**.</span></span>
5. <span data-ttu-id="e4cb5-165">針對 [名稱]、[位址空間]、[子網路名稱] 及 [子網路位址範圍]，使用先前網路組態表中顯示的值。</span><span class="sxs-lookup"><span data-stu-id="e4cb5-165">For **Name**, **Address space**, **Subnet name**, and **Subnet address range**, use the values that appear earlier in the network configuration table.</span></span>
6. <span data-ttu-id="e4cb5-166">在 [訂用帳戶] 中，會顯示您先前建立的訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="e4cb5-166">In **Subscription**, the subscription that you created earlier appears.</span></span>
7. <span data-ttu-id="e4cb5-167">針對 [資源群組]，您可以建立資源群組，或選取 [使用現有的] \(如果您已經有資源群組)。</span><span class="sxs-lookup"><span data-stu-id="e4cb5-167">For **Resource Group**, you can either create a resource group or if you already have one, select **Use existing**.</span></span>
8. <span data-ttu-id="e4cb5-168">驗證預設位置。</span><span class="sxs-lookup"><span data-stu-id="e4cb5-168">Verify the default location.</span></span>
9. <span data-ttu-id="e4cb5-169">選取 [釘選到儀表板]。</span><span class="sxs-lookup"><span data-stu-id="e4cb5-169">Select **Pin to dashboard**.</span></span>
10. <span data-ttu-id="e4cb5-170">選取 [ **建立**]。</span><span class="sxs-lookup"><span data-stu-id="e4cb5-170">Select **Create**.</span></span>

### <a name="create-the-gateway-subnet"></a><span data-ttu-id="e4cb5-171">建立閘道子網路</span><span class="sxs-lookup"><span data-stu-id="e4cb5-171">Create the gateway subnet</span></span>
1. <span data-ttu-id="e4cb5-172">在儀表板上，開啟您先前建立的 VNET-01 虛擬網路資源。</span><span class="sxs-lookup"><span data-stu-id="e4cb5-172">On the dashboard, open the VNET-01 virtual network resource that you created earlier.</span></span>
2. <span data-ttu-id="e4cb5-173">在 [設定] 刀鋒視窗上選取 [子網路]。</span><span class="sxs-lookup"><span data-stu-id="e4cb5-173">On the **Settings** blade, select **Subnets**.</span></span>
3. <span data-ttu-id="e4cb5-174">若要將閘道子網路新增到虛擬網路，請選取 [閘道子網路]。</span><span class="sxs-lookup"><span data-stu-id="e4cb5-174">To add a gateway subnet to the virtual network, select **Gateway Subnet**.</span></span>
   
    ![新增閘道子網路](media/azure-stack-create-vpn-connection-one-node-tp2/image4.png)

4. <span data-ttu-id="e4cb5-176">子網路名稱預設為 **GatewaySubnet**。</span><span class="sxs-lookup"><span data-stu-id="e4cb5-176">By default, the subnet name is set to **GatewaySubnet**.</span></span>
   <span data-ttu-id="e4cb5-177">閘道子網路相當特殊。</span><span class="sxs-lookup"><span data-stu-id="e4cb5-177">Gateway subnets are special.</span></span> <span data-ttu-id="e4cb5-178">為了正常運作，它們必須使用 *GatewaySubnet* 名稱。</span><span class="sxs-lookup"><span data-stu-id="e4cb5-178">To function properly, they must use the *GatewaySubnet* name.</span></span>
5. <span data-ttu-id="e4cb5-179">在 [位址範圍] 中，確認位址是 **10.0.11.0/24**。</span><span class="sxs-lookup"><span data-stu-id="e4cb5-179">In **Address range**, verify that the address is **10.0.11.0/24**.</span></span>
6. <span data-ttu-id="e4cb5-180">選取 [確定] 以建立閘道子網路。</span><span class="sxs-lookup"><span data-stu-id="e4cb5-180">Select **OK** to create the gateway subnet.</span></span>

### <a name="create-the-virtual-network-gateway"></a><span data-ttu-id="e4cb5-181">建立虛擬網路閘道</span><span class="sxs-lookup"><span data-stu-id="e4cb5-181">Create the virtual network gateway</span></span>
1. <span data-ttu-id="e4cb5-182">在 Azure 入口網站中，選取 [新增]。</span><span class="sxs-lookup"><span data-stu-id="e4cb5-182">In the Azure portal, select **New**.</span></span> 
2. <span data-ttu-id="e4cb5-183">移至 [Marketplace]，然後選取 [網路]。</span><span class="sxs-lookup"><span data-stu-id="e4cb5-183">Go to **Marketplace**, and then select **Networking**.</span></span>
3. <span data-ttu-id="e4cb5-184">從網路資源清單中，選取 [虛擬網路閘道]。</span><span class="sxs-lookup"><span data-stu-id="e4cb5-184">From the list of network resources, select **Virtual network gateway**.</span></span>
4. <span data-ttu-id="e4cb5-185">在 [名稱] 中，輸入 **GW1**。</span><span class="sxs-lookup"><span data-stu-id="e4cb5-185">In **Name**, enter **GW1**.</span></span>
5. <span data-ttu-id="e4cb5-186">選取 [虛擬網路] 項目以選擇虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="e4cb5-186">Select the **Virtual network** item to choose a virtual network.</span></span>
   <span data-ttu-id="e4cb5-187">從清單中選取 [VNET-01]。</span><span class="sxs-lookup"><span data-stu-id="e4cb5-187">Select **VNET-01** from the list.</span></span>
6. <span data-ttu-id="e4cb5-188">選取 [公用 IP 位址] 功能表項目。</span><span class="sxs-lookup"><span data-stu-id="e4cb5-188">Select the **Public IP address** menu item.</span></span> <span data-ttu-id="e4cb5-189">當 [選擇公用 IP 位址] 刀鋒視窗開啟時，請選取 [新建]。</span><span class="sxs-lookup"><span data-stu-id="e4cb5-189">When the **Choose public IP address** blade opens, select **Create new**.</span></span>
7. <span data-ttu-id="e4cb5-190">在 [名稱] 中輸入 **GW1-PiP**，然後選取 [確定]。</span><span class="sxs-lookup"><span data-stu-id="e4cb5-190">In **Name**, enter **GW1-PiP**, and then select **OK**.</span></span>
8.  <span data-ttu-id="e4cb5-191">針對 [VPN 類型]，預設會選取 [依路由]。</span><span class="sxs-lookup"><span data-stu-id="e4cb5-191">By default, for **VPN type**, **Route-based** is selected.</span></span>
    <span data-ttu-id="e4cb5-192">保留 [依路由] VPN 類型。</span><span class="sxs-lookup"><span data-stu-id="e4cb5-192">Keep the **Route-based** VPN type.</span></span>
9. <span data-ttu-id="e4cb5-193">確認 [訂用帳戶] 和 [位置] 均正確無誤。</span><span class="sxs-lookup"><span data-stu-id="e4cb5-193">Verify that **Subscription** and **Location** are correct.</span></span> <span data-ttu-id="e4cb5-194">您可以將資源釘選到儀表板。</span><span class="sxs-lookup"><span data-stu-id="e4cb5-194">You can pin the resource to the dashboard.</span></span> <span data-ttu-id="e4cb5-195">選取 [ **建立**]。</span><span class="sxs-lookup"><span data-stu-id="e4cb5-195">Select **Create**.</span></span>

### <a name="create-the-local-network-gateway"></a><span data-ttu-id="e4cb5-196">建立區域網路閘道</span><span class="sxs-lookup"><span data-stu-id="e4cb5-196">Create the local network gateway</span></span>
<span data-ttu-id="e4cb5-197">在此 Azure Stack 評估部署與實際 Azure 部署中實作*區域網路閘道*的方式有點不同。</span><span class="sxs-lookup"><span data-stu-id="e4cb5-197">The implementation of a *local network gateway* in this Azure Stack evaluation deployment is a bit different than in an actual Azure deployment.</span></span>

<span data-ttu-id="e4cb5-198">在 Azure 部署中，區域網路閘道代表您用來連線到 Azure 中虛擬網路閘道的內部部署 (位於租用戶) 實體裝置。</span><span class="sxs-lookup"><span data-stu-id="e4cb5-198">In an Azure deployment, a local network gateway represents an on-premises (at the tenant) physical device, that you use to connect to a virtual network gateway in Azure.</span></span> <span data-ttu-id="e4cb5-199">在這個 Azure Stack 評估部署中，連線的兩端都是虛擬網路閘道！</span><span class="sxs-lookup"><span data-stu-id="e4cb5-199">In this Azure Stack evaluation deployment, both ends of the connection are virtual network gateways!</span></span>

<span data-ttu-id="e4cb5-200">更廣泛來說，區域網路閘道資源一律是指連線另一端的遠端閘道。</span><span class="sxs-lookup"><span data-stu-id="e4cb5-200">A way to think about this more generically is that the local network gateway resource always indicates the remote gateway at the other end of the connection.</span></span> <span data-ttu-id="e4cb5-201">由於「Azure Stack 開發套件」的設計方式緣故，因此您必須提供另一個「Azure Stack 開發套件」之網路位址轉譯 (NAT) VM 上的外部網路介面卡 IP 位址作為區域網路閘道的「公用 IP 位址」。</span><span class="sxs-lookup"><span data-stu-id="e4cb5-201">Because of the way the Azure Stack Development Kit was designed, you need to provide the IP address of the external network adapter on the network address translation (NAT) VM of the other Azure Stack Development Kit as the Public IP Address of the local network gateway.</span></span> <span data-ttu-id="e4cb5-202">您接著需在 NAT VM 上建立 NAT 對應，以確保正確連接兩端。</span><span class="sxs-lookup"><span data-stu-id="e4cb5-202">You then create NAT mappings on the NAT VM to make sure that both ends are connected properly.</span></span>


### <a name="create-the-local-network-gateway-resource"></a><span data-ttu-id="e4cb5-203">建立區域網路閘道資源</span><span class="sxs-lookup"><span data-stu-id="e4cb5-203">Create the local network gateway resource</span></span>
1. <span data-ttu-id="e4cb5-204">登入 POC1 的 Azure Stack 實體機器。</span><span class="sxs-lookup"><span data-stu-id="e4cb5-204">Sign in to the Azure Stack physical machine for POC1.</span></span>
2. <span data-ttu-id="e4cb5-205">在使用者入口網站中，選取 [新增]。</span><span class="sxs-lookup"><span data-stu-id="e4cb5-205">In the user portal, select **New**.</span></span>
3. <span data-ttu-id="e4cb5-206">移至 [Marketplace]，然後選取 [網路]。</span><span class="sxs-lookup"><span data-stu-id="e4cb5-206">Go to **Marketplace**, and then select **Networking**.</span></span>
4. <span data-ttu-id="e4cb5-207">從資源清單中，選取 [區域網路閘道]。</span><span class="sxs-lookup"><span data-stu-id="e4cb5-207">From the list of resources, select **local network gateway**.</span></span>
5. <span data-ttu-id="e4cb5-208">在 [名稱] 中，輸入 **POC2-GW**。</span><span class="sxs-lookup"><span data-stu-id="e4cb5-208">In **Name**, enter **POC2-GW**.</span></span>
6. <span data-ttu-id="e4cb5-209">在 [IP 位址] 中，輸入 POC2 的外部 BGPNAT 位址。</span><span class="sxs-lookup"><span data-stu-id="e4cb5-209">In **IP address**, enter the External BGPNAT address for POC2.</span></span> <span data-ttu-id="e4cb5-210">此位址先前已顯示在網路組態表中。</span><span class="sxs-lookup"><span data-stu-id="e4cb5-210">This address appears earlier in the network configuration table.</span></span>
7. <span data-ttu-id="e4cb5-211">在 [位址空間] 中，針對您稍後建立的 POC2 VNET 的位址空間，輸入 **10.0.20.0/23**。</span><span class="sxs-lookup"><span data-stu-id="e4cb5-211">In **Address Space**, for the address space of the POC2 VNET that you create later, enter **10.0.20.0/23**.</span></span>
8. <span data-ttu-id="e4cb5-212">確認您的 [訂用帳戶]、[資源群組] 和 [位置] 正確無誤，然後選取 [建立]。</span><span class="sxs-lookup"><span data-stu-id="e4cb5-212">Verify that your **Subscription**, **Resource Group**, and **location** are correct, and then select **Create**.</span></span>

### <a name="create-the-connection"></a><span data-ttu-id="e4cb5-213">建立連線</span><span class="sxs-lookup"><span data-stu-id="e4cb5-213">Create the connection</span></span>
1. <span data-ttu-id="e4cb5-214">在使用者入口網站中，選取 [新增]。</span><span class="sxs-lookup"><span data-stu-id="e4cb5-214">In the user portal, select **New**.</span></span>
2. <span data-ttu-id="e4cb5-215">移至 [Marketplace]，然後選取 [網路]。</span><span class="sxs-lookup"><span data-stu-id="e4cb5-215">Go to **Marketplace**, and then select **Networking**.</span></span>
3. <span data-ttu-id="e4cb5-216">從資源清單中，選取 [連線]。</span><span class="sxs-lookup"><span data-stu-id="e4cb5-216">From the list of resources, select **Connection**.</span></span>
4. <span data-ttu-id="e4cb5-217">在 [基本] 設定刀鋒視窗上，針對 [連線類型]，選取 [站對站 (IPSec)]。</span><span class="sxs-lookup"><span data-stu-id="e4cb5-217">On the **Basics** settings blade, for the **Connection type**, select **Site-to-site (IPSec)**.</span></span>
5. <span data-ttu-id="e4cb5-218">選取 [訂用帳戶]、[資源群組] 和 [位置]，然後選取 [確定]。</span><span class="sxs-lookup"><span data-stu-id="e4cb5-218">Select the **Subscription**, **Resource Group**, and **Location**, and then select **OK**.</span></span>
6. <span data-ttu-id="e4cb5-219">在 [設定] 刀鋒視窗上，選取 [虛擬網路閘道]，然後選取 [GW1]。</span><span class="sxs-lookup"><span data-stu-id="e4cb5-219">On the **Settings** blade,  select **Virtual network gateway**, and then select **GW1**.</span></span>
7. <span data-ttu-id="e4cb5-220">選取 [區域網路閘道]，然後選取 [POC2-GW]。</span><span class="sxs-lookup"><span data-stu-id="e4cb5-220">Select **Local network gateway**, and then select **POC2-GW**.</span></span>
8. <span data-ttu-id="e4cb5-221">在 [連線名稱] 中，輸入 **POC1-POC2**。</span><span class="sxs-lookup"><span data-stu-id="e4cb5-221">In **Connection Name**, enter **POC1-POC2**.</span></span>
9. <span data-ttu-id="e4cb5-222">在 [共用金鑰 (PSK)] 中輸入 **12345**，然後選取 [確定]。</span><span class="sxs-lookup"><span data-stu-id="e4cb5-222">In **Shared key (PSK)**, enter **12345**, and then select **OK**.</span></span>
10. <span data-ttu-id="e4cb5-223">在 [摘要] 刀鋒視窗上，選取 [確定]。</span><span class="sxs-lookup"><span data-stu-id="e4cb5-223">On the **Summary** blade, select **OK**.</span></span>

### <a name="create-a-vm"></a><span data-ttu-id="e4cb5-224">建立 VM</span><span class="sxs-lookup"><span data-stu-id="e4cb5-224">Create a VM</span></span>
<span data-ttu-id="e4cb5-225">若要驗證透過 VPN 連線傳輸的資料，您將需要虛擬機器，以在每個「Azure Stack 開發套件」中傳送和接收資料。</span><span class="sxs-lookup"><span data-stu-id="e4cb5-225">To validate the data that travels through the VPN connection, you need the virtual machines to send and receive data in each Azure Stack Development Kit.</span></span> <span data-ttu-id="e4cb5-226">立即在 POC1 中建立虛擬機器，然後將它放在您虛擬網路的 VM 子網路上。</span><span class="sxs-lookup"><span data-stu-id="e4cb5-226">Create a virtual machine in POC1 now, and then in your virtual network, put it on your VM subnet.</span></span>

1. <span data-ttu-id="e4cb5-227">在 Azure 入口網站中，選取 [新增]。</span><span class="sxs-lookup"><span data-stu-id="e4cb5-227">In the Azure portal, select **New**.</span></span>
2. <span data-ttu-id="e4cb5-228">移至 [Marketplace]，然後選取 [計算]。</span><span class="sxs-lookup"><span data-stu-id="e4cb5-228">Go to **Marketplace**, and then select **Compute**.</span></span>
3. <span data-ttu-id="e4cb5-229">在虛擬機器映像清單中，選取 [Windows Server 2016 Datacenter 評估版] 映像。</span><span class="sxs-lookup"><span data-stu-id="e4cb5-229">In the list of virtual machine images, select the **Windows Server 2016 Datacenter Eval** image.</span></span>
4. <span data-ttu-id="e4cb5-230">在 [基本] 刀鋒視窗的 [名稱] 中，輸入 **VM01**。</span><span class="sxs-lookup"><span data-stu-id="e4cb5-230">On the **Basics** blade, in **Name**, enter **VM01**.</span></span>
5. <span data-ttu-id="e4cb5-231">輸入有效的使用者名稱和密碼。</span><span class="sxs-lookup"><span data-stu-id="e4cb5-231">Enter a valid username and password.</span></span> <span data-ttu-id="e4cb5-232">建立 VM 之後，您將使用此帳戶來登入 VM。</span><span class="sxs-lookup"><span data-stu-id="e4cb5-232">You use this account to sign in to the VM after it's created.</span></span>
6. <span data-ttu-id="e4cb5-233">提供 [訂用帳戶]、[資源群組] 和 [位置]，然後選取 [確定]。</span><span class="sxs-lookup"><span data-stu-id="e4cb5-233">Provide a **Subscription**, **Resource Group**, and **Location**, and then select **OK**.</span></span>
7. <span data-ttu-id="e4cb5-234">在 [大小] 刀鋒視窗上，為此執行個體選取虛擬機器大小，然後選取 [選取]。</span><span class="sxs-lookup"><span data-stu-id="e4cb5-234">On the **Size** blade, for this instance, select a virtual machine size, and then select **Select**.</span></span>
8. <span data-ttu-id="e4cb5-235">在 [設定] 刀鋒視窗上，接受預設值。</span><span class="sxs-lookup"><span data-stu-id="e4cb5-235">On the **Settings** blade, accept the defaults.</span></span> <span data-ttu-id="e4cb5-236">確定選取的是 [VNET-01] 虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="e4cb5-236">Ensure that the **VNET-01** virtual network is selected.</span></span> <span data-ttu-id="e4cb5-237">確認子網路已設定為 **10.0.10.0/24**。</span><span class="sxs-lookup"><span data-stu-id="e4cb5-237">Verify that the subnet is set to **10.0.10.0/24**.</span></span> <span data-ttu-id="e4cb5-238">然後選取 [確定]。</span><span class="sxs-lookup"><span data-stu-id="e4cb5-238">Then select **OK**.</span></span>
9. <span data-ttu-id="e4cb5-239">在 [摘要] 刀鋒視窗上檢閱設定，然後選取 [確定]。</span><span class="sxs-lookup"><span data-stu-id="e4cb5-239">On the **Summary** blade, review the settings, and then select **OK**.</span></span>



## <a name="create-the-network-resources-in-poc2"></a><span data-ttu-id="e4cb5-240">在 POC 2 中建立網路資源</span><span class="sxs-lookup"><span data-stu-id="e4cb5-240">Create the network resources in POC2</span></span>

<span data-ttu-id="e4cb5-241">下一個步驟是建立 POC2 的網路資源。</span><span class="sxs-lookup"><span data-stu-id="e4cb5-241">The next step is to create the network resources for POC2.</span></span> <span data-ttu-id="e4cb5-242">下列指示說明如何使用使用者入口網站來建立資源。</span><span class="sxs-lookup"><span data-stu-id="e4cb5-242">The following instructions show how to create the resources by using the user portal.</span></span>

### <a name="sign-in-as-a-tenant"></a><span data-ttu-id="e4cb5-243">以租用戶身分登入</span><span class="sxs-lookup"><span data-stu-id="e4cb5-243">Sign in as a tenant</span></span>
<span data-ttu-id="e4cb5-244">服務系統管理員可以用租用戶身分登入，以測試其租用戶可能使用的方案、供應項目及訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="e4cb5-244">A service administrator can sign in as a tenant to test the plans, offers, and subscriptions that their tenants might use.</span></span> <span data-ttu-id="e4cb5-245">如果您還沒有租用戶帳戶，請先[建立租用戶帳戶](azure-stack-add-new-user-aad.md)再登入。</span><span class="sxs-lookup"><span data-stu-id="e4cb5-245">If you don’t already have one, [create a tenant account](azure-stack-add-new-user-aad.md) before you sign in.</span></span>

### <a name="create-the-virtual-network-and-vm-subnet"></a><span data-ttu-id="e4cb5-246">建立虛擬網路和 VM 子網路</span><span class="sxs-lookup"><span data-stu-id="e4cb5-246">Create the virtual network and VM subnet</span></span>

1. <span data-ttu-id="e4cb5-247">使用租用戶帳戶來登入。</span><span class="sxs-lookup"><span data-stu-id="e4cb5-247">Sign in by using a tenant account.</span></span>
2. <span data-ttu-id="e4cb5-248">在使用者入口網站中，選取 [新增]。</span><span class="sxs-lookup"><span data-stu-id="e4cb5-248">In the user portal, select **New**.</span></span>
3. <span data-ttu-id="e4cb5-249">移至 [Marketplace]，然後選取 [網路]。</span><span class="sxs-lookup"><span data-stu-id="e4cb5-249">Go to **Marketplace**, and then select **Networking**.</span></span>
4. <span data-ttu-id="e4cb5-250">選取 [虛擬網路]。</span><span class="sxs-lookup"><span data-stu-id="e4cb5-250">Select **Virtual network**.</span></span>
5. <span data-ttu-id="e4cb5-251">使用先前網路組態表中顯示的資訊，來指定 POC2 [名稱]、[位址空間]、[子網路名稱] 及 [子網路位址範圍] 的值。</span><span class="sxs-lookup"><span data-stu-id="e4cb5-251">Use the information appearing earlier in the network configuration table to identify the values for the POC2 **Name**, **Address space**, **Subnet name**, and **Subnet address range**.</span></span>
6. <span data-ttu-id="e4cb5-252">在 [訂用帳戶] 中，會顯示您先前建立的訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="e4cb5-252">In **Subscription**, the subscription that you created earlier appears.</span></span>
7. <span data-ttu-id="e4cb5-253">針對 [資源群組]，建立資源群組，或選取 [使用現有的] (如果您已經有資源群組)。</span><span class="sxs-lookup"><span data-stu-id="e4cb5-253">For **Resource Group**, create a new resource group or, if you already have one, select **Use existing**.</span></span>
8. <span data-ttu-id="e4cb5-254">確認預設 [位置]。</span><span class="sxs-lookup"><span data-stu-id="e4cb5-254">Verify the default **Location**.</span></span>
9. <span data-ttu-id="e4cb5-255">選取 [釘選到儀表板]。</span><span class="sxs-lookup"><span data-stu-id="e4cb5-255">Select **Pin to dashboard**.</span></span>
10. <span data-ttu-id="e4cb5-256">選取 [ **建立**]。</span><span class="sxs-lookup"><span data-stu-id="e4cb5-256">Select **Create**.</span></span>

### <a name="create-the-gateway-subnet"></a><span data-ttu-id="e4cb5-257">建立閘道子網路</span><span class="sxs-lookup"><span data-stu-id="e4cb5-257">Create the Gateway Subnet</span></span>
1. <span data-ttu-id="e4cb5-258">從儀表板開啟您建立的虛擬網路資源 (**VNET-02**)。</span><span class="sxs-lookup"><span data-stu-id="e4cb5-258">Open the Virtual network resource you created (**VNET-02**) from the dashboard.</span></span>
2. <span data-ttu-id="e4cb5-259">在 [設定] 刀鋒視窗上選取 [子網路]。</span><span class="sxs-lookup"><span data-stu-id="e4cb5-259">On the **Settings** blade, select **Subnets**.</span></span>
3. <span data-ttu-id="e4cb5-260">選取 [閘道子網路] 以將閘道子網路新增到虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="e4cb5-260">Select  **Gateway subnet** to add a gateway subnet to the virtual network.</span></span>
4. <span data-ttu-id="e4cb5-261">子網路名稱預設為 **GatewaySubnet**。</span><span class="sxs-lookup"><span data-stu-id="e4cb5-261">The name of the subnet is set to **GatewaySubnet** by default.</span></span>
   <span data-ttu-id="e4cb5-262">閘道子網路很特別﹐必須具有此特定名稱，才能正常運作。</span><span class="sxs-lookup"><span data-stu-id="e4cb5-262">Gateway subnets are special and must have this specific name to function properly.</span></span>
5. <span data-ttu-id="e4cb5-263">在 [位址範圍] 欄位中，確認位址是 **10.0.21.0/24**。</span><span class="sxs-lookup"><span data-stu-id="e4cb5-263">In the **Address range** field, verify the address is **10.0.21.0/24**.</span></span>
6. <span data-ttu-id="e4cb5-264">選取 [確定] 以建立閘道子網路。</span><span class="sxs-lookup"><span data-stu-id="e4cb5-264">Select **OK** to create the gateway subnet.</span></span>

### <a name="create-the-virtual-network-gateway"></a><span data-ttu-id="e4cb5-265">建立虛擬網路閘道</span><span class="sxs-lookup"><span data-stu-id="e4cb5-265">Create the virtual network gateway</span></span>
1. <span data-ttu-id="e4cb5-266">在 Azure 入口網站中，選取 [新增]。</span><span class="sxs-lookup"><span data-stu-id="e4cb5-266">In the Azure portal, select **New**.</span></span>  
2. <span data-ttu-id="e4cb5-267">移至 [Marketplace]，然後選取 [網路]。</span><span class="sxs-lookup"><span data-stu-id="e4cb5-267">Go to **Marketplace**, and then select **Networking**.</span></span>
3. <span data-ttu-id="e4cb5-268">從網路資源清單中，選取 [虛擬網路閘道]。</span><span class="sxs-lookup"><span data-stu-id="e4cb5-268">From the list of network resources, select **Virtual network gateway**.</span></span>
4. <span data-ttu-id="e4cb5-269">在 [名稱] 中，輸入 **GW2**。</span><span class="sxs-lookup"><span data-stu-id="e4cb5-269">In **Name**, enter **GW2**.</span></span>
5. <span data-ttu-id="e4cb5-270">若要選擇虛擬網路，請選取 [虛擬網路]。</span><span class="sxs-lookup"><span data-stu-id="e4cb5-270">To choose a virtual network, select **Virtual network**.</span></span> <span data-ttu-id="e4cb5-271">然後從清單中選取 [VNET-02]。</span><span class="sxs-lookup"><span data-stu-id="e4cb5-271">Then select **VNET-02** from the list.</span></span>
6. <span data-ttu-id="e4cb5-272">選取 [公用 IP 位址]。</span><span class="sxs-lookup"><span data-stu-id="e4cb5-272">Select **Public IP address**.</span></span> <span data-ttu-id="e4cb5-273">當 [選擇公用 IP 位址] 刀鋒視窗開啟時，請選取 [新建]。</span><span class="sxs-lookup"><span data-stu-id="e4cb5-273">When the **Choose public IP address** blade opens, select **Create new**.</span></span>
7. <span data-ttu-id="e4cb5-274">在 [名稱] 中輸入 **GW2-PiP**，然後選取 [確定]。</span><span class="sxs-lookup"><span data-stu-id="e4cb5-274">In **Name**, enter **GW2-PiP**, and then select **OK**.</span></span>
8. <span data-ttu-id="e4cb5-275">針對 [VPN 類型]，預設會選取 [依路由]。</span><span class="sxs-lookup"><span data-stu-id="e4cb5-275">By default, for **VPN type**, **Route-based** is selected.</span></span>
    <span data-ttu-id="e4cb5-276">保留 [依路由] VPN 類型。</span><span class="sxs-lookup"><span data-stu-id="e4cb5-276">Keep the **Route-based** VPN type.</span></span>
9. <span data-ttu-id="e4cb5-277">確認 [訂用帳戶] 和 [位置] 均正確無誤。</span><span class="sxs-lookup"><span data-stu-id="e4cb5-277">Verify that **Subscription** and **Location** are correct.</span></span> <span data-ttu-id="e4cb5-278">您可以將資源釘選到儀表板。</span><span class="sxs-lookup"><span data-stu-id="e4cb5-278">You can pin the resource to the dashboard.</span></span> <span data-ttu-id="e4cb5-279">選取 [ **建立**]。</span><span class="sxs-lookup"><span data-stu-id="e4cb5-279">Select **Create**.</span></span>

### <a name="create-the-local-network-gateway-resource"></a><span data-ttu-id="e4cb5-280">建立區域網路閘道資源</span><span class="sxs-lookup"><span data-stu-id="e4cb5-280">Create the local network gateway resource</span></span>

1. <span data-ttu-id="e4cb5-281">在 POC2 使用者入口網站中，選取 [新增]。</span><span class="sxs-lookup"><span data-stu-id="e4cb5-281">In the POC2 user portal, select **New**.</span></span> 
4. <span data-ttu-id="e4cb5-282">移至 [Marketplace]，然後選取 [網路]。</span><span class="sxs-lookup"><span data-stu-id="e4cb5-282">Go to **Marketplace**, and then select **Networking**.</span></span>
5. <span data-ttu-id="e4cb5-283">從資源清單中，選取 [區域網路閘道]。</span><span class="sxs-lookup"><span data-stu-id="e4cb5-283">From the list of resources, select **Local network gateway**.</span></span>
6. <span data-ttu-id="e4cb5-284">在 [名稱] 中，輸入 **POC1-GW**。</span><span class="sxs-lookup"><span data-stu-id="e4cb5-284">In **Name**, enter **POC1-GW**.</span></span>
7. <span data-ttu-id="e4cb5-285">在 [IP 位址] 中，輸入先前網路組態表中所列的 POC1 外部 BGPNAT 位址。</span><span class="sxs-lookup"><span data-stu-id="e4cb5-285">In **IP address**, enter the External BGPNAT address for POC1 that is listed earlier in the network configuration table.</span></span>
8. <span data-ttu-id="e4cb5-286">在 [位址空間] 欄位中，從 POC1，輸入 **VNET-01** 的位址空間 **10.0.10.0/23**。</span><span class="sxs-lookup"><span data-stu-id="e4cb5-286">In **Address Space**, from POC1, enter the **10.0.10.0/23** address space of **VNET-01**.</span></span>
9. <span data-ttu-id="e4cb5-287">確認您的 [訂用帳戶]、[資源群組] 和 [位置] 正確無誤，然後選取 [建立]。</span><span class="sxs-lookup"><span data-stu-id="e4cb5-287">Verify that your **Subscription**, **Resource Group**, and **Location** are correct, and then select **Create**.</span></span>

## <a name="create-the-connection"></a><span data-ttu-id="e4cb5-288">建立連線</span><span class="sxs-lookup"><span data-stu-id="e4cb5-288">Create the connection</span></span>
1. <span data-ttu-id="e4cb5-289">在使用者入口網站中，選取 [新增]。</span><span class="sxs-lookup"><span data-stu-id="e4cb5-289">In the user portal, select **New**.</span></span> 
2. <span data-ttu-id="e4cb5-290">移至 [Marketplace]，然後選取 [網路]。</span><span class="sxs-lookup"><span data-stu-id="e4cb5-290">Go to **Marketplace**, and then select **Networking**.</span></span>
3. <span data-ttu-id="e4cb5-291">從資源清單中，選取 [連線]。</span><span class="sxs-lookup"><span data-stu-id="e4cb5-291">From the list of resources, select **Connection**.</span></span>
4. <span data-ttu-id="e4cb5-292">在 [基本] 設定刀鋒視窗上，針對 [連線類型]，選擇 [站對站 (IPSec)]。</span><span class="sxs-lookup"><span data-stu-id="e4cb5-292">On the **Basic** settings blade, for the **Connection type**, choose **Site-to-site (IPSec)**.</span></span>
5. <span data-ttu-id="e4cb5-293">選取 [訂用帳戶]、[資源群組] 和 [位置]，然後選取 [確定]。</span><span class="sxs-lookup"><span data-stu-id="e4cb5-293">Select the **Subscription**, **Resource Group**, and **Location**, and then select **OK**.</span></span>
6. <span data-ttu-id="e4cb5-294">在 [設定] 刀鋒視窗上，選取 [虛擬網路閘道]，然後選取 [GW2]。</span><span class="sxs-lookup"><span data-stu-id="e4cb5-294">On the **Settings** blade, select **Virtual network gateway**, and then select **GW2**.</span></span>
7. <span data-ttu-id="e4cb5-295">選取 [區域網路閘道]，然後選取 [POC1-GW]。</span><span class="sxs-lookup"><span data-stu-id="e4cb5-295">Select **Local network gateway**, and then select **POC1-GW**.</span></span>
8. <span data-ttu-id="e4cb5-296">在 [連線名稱] 中，輸入 **POC2-POC1**。</span><span class="sxs-lookup"><span data-stu-id="e4cb5-296">In **Connection name**, enter **POC2-POC1**.</span></span>
9. <span data-ttu-id="e4cb5-297">在 [共用金鑰 (PSK)] 中，輸入 **12345**。</span><span class="sxs-lookup"><span data-stu-id="e4cb5-297">In **Shared key (PSK)**, enter **12345**.</span></span> <span data-ttu-id="e4cb5-298">如果您選擇不同的值，請記住該值「必須」與您在 POC1 上所建立共用金鑰的值相符。</span><span class="sxs-lookup"><span data-stu-id="e4cb5-298">If you choose a different value, remember that it *must* match the value for the shared key that you created on POC1.</span></span> <span data-ttu-id="e4cb5-299">選取 [確定] 。</span><span class="sxs-lookup"><span data-stu-id="e4cb5-299">Select **OK**.</span></span>
10. <span data-ttu-id="e4cb5-300">檢閱 [摘要] 刀鋒視窗，然後選取 [確定]。</span><span class="sxs-lookup"><span data-stu-id="e4cb5-300">Review the **Summary** blade, and then select **OK**.</span></span>

## <a name="create-a-virtual-machine"></a><span data-ttu-id="e4cb5-301">建立虛擬機器</span><span class="sxs-lookup"><span data-stu-id="e4cb5-301">Create a virtual machine</span></span>
<span data-ttu-id="e4cb5-302">請立即在 POC2 中建立虛擬機器，然後將它放在您虛擬網路的 VM 子網路上。</span><span class="sxs-lookup"><span data-stu-id="e4cb5-302">Create a virtual machine in POC2 now, and put it on your VM subnet in your virtual network.</span></span>

1. <span data-ttu-id="e4cb5-303">在 Azure 入口網站中，選取 [新增]。</span><span class="sxs-lookup"><span data-stu-id="e4cb5-303">In the Azure portal, select **New**.</span></span>
2. <span data-ttu-id="e4cb5-304">移至 [Marketplace]，然後選取 [計算]。</span><span class="sxs-lookup"><span data-stu-id="e4cb5-304">Go to **Marketplace**, and then select **Compute**.</span></span>
3. <span data-ttu-id="e4cb5-305">在虛擬機器映像清單中，選取 [Windows Server 2016 Datacenter 評估版] 映像。</span><span class="sxs-lookup"><span data-stu-id="e4cb5-305">In the list of virtual machine images, select the **Windows Server 2016 Datacenter Eval** image.</span></span>
4. <span data-ttu-id="e4cb5-306">在 [基本] 刀鋒視窗上，針對 [名稱]，輸入 **VM02**。</span><span class="sxs-lookup"><span data-stu-id="e4cb5-306">On the **Basics** blade, for **Name**, enter **VM02**.</span></span>
5. <span data-ttu-id="e4cb5-307">輸入有效的使用者名稱和密碼。</span><span class="sxs-lookup"><span data-stu-id="e4cb5-307">Enter a valid username and password.</span></span> <span data-ttu-id="e4cb5-308">建立虛擬機器之後，您將使用此帳戶來登入虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="e4cb5-308">You use this account to sign in to the virtual machine after it's created.</span></span>
6. <span data-ttu-id="e4cb5-309">提供 [訂用帳戶]、[資源群組] 和 [位置]，然後選取 [確定]。</span><span class="sxs-lookup"><span data-stu-id="e4cb5-309">Provide a **Subscription**, **Resource Group**, and **Location**, and then select **OK**.</span></span>
7. <span data-ttu-id="e4cb5-310">在 [大小] 刀鋒視窗上，為此執行個體選取虛擬機器大小，然後選取 [選取]。</span><span class="sxs-lookup"><span data-stu-id="e4cb5-310">On the **Size** blade, select a virtual machine size for this instance, and then select **Select**.</span></span>
8. <span data-ttu-id="e4cb5-311">在 [設定] 刀鋒視窗上，您可以接受預設值。</span><span class="sxs-lookup"><span data-stu-id="e4cb5-311">On the **Settings** blade, you can accept the defaults.</span></span> <span data-ttu-id="e4cb5-312">確定選取的是 [VNET-02] 虛擬網路，並確認子網路已設定為 **10.0.20.0/24**。</span><span class="sxs-lookup"><span data-stu-id="e4cb5-312">Ensure that the **VNET-02** virtual network is selected, and verify that the subnet is set to **10.0.20.0/24**.</span></span> <span data-ttu-id="e4cb5-313">選取 [確定] 。</span><span class="sxs-lookup"><span data-stu-id="e4cb5-313">Select **OK**.</span></span>
9. <span data-ttu-id="e4cb5-314">檢閱 [摘要] 刀鋒視窗上的設定，然後選取 [確定]。</span><span class="sxs-lookup"><span data-stu-id="e4cb5-314">Review the settings on the **Summary** blade, and then select **OK**.</span></span>

## <a name="configure-the-nat-virtual-machine-on-each-azure-stack-development-kit-for-gateway-traversal"></a><span data-ttu-id="e4cb5-315">在每個 Azure Stack 開發套件上設定 NAT 虛擬機器以進行閘道周遊</span><span class="sxs-lookup"><span data-stu-id="e4cb5-315">Configure the NAT virtual machine on each Azure Stack Development Kit for gateway traversal</span></span>
<span data-ttu-id="e4cb5-316">由於「Azure Stack 開發套件」是獨立的並與實體主機部署所在的網路隔離，因此閘道所連接的「外部」VIP 網路實際上並不在外部。</span><span class="sxs-lookup"><span data-stu-id="e4cb5-316">Because the Azure Stack Development Kit is self-contained and isolated from the network on which the physical host is deployed, the *external* VIP network that the gateways are connected to is not actually external.</span></span> <span data-ttu-id="e4cb5-317">取而代之的是，VIP 網路隱藏在執行網路位址轉譯的路由器之後。</span><span class="sxs-lookup"><span data-stu-id="e4cb5-317">Instead, the VIP network is hidden behind a router that performs network address translation.</span></span> 

<span data-ttu-id="e4cb5-318">路由器是一部名為 *AzS-bgpnat01* 的 Windows Server 虛擬機器，在「Azure Stack 開發套件」基礎結構中執行「路由及遠端存取服務」(RRAS) 角色。</span><span class="sxs-lookup"><span data-stu-id="e4cb5-318">The router is a Windows Server virtual machine, called *AzS-bgpnat01*, that runs the Routing and Remote Access Services (RRAS) role in the Azure Stack Development Kit infrastructure.</span></span> <span data-ttu-id="e4cb5-319">您必須在 AzS-bgpnat01 虛擬機器上設定 NAT，才能允許站對站 VPN 連線連接兩端。</span><span class="sxs-lookup"><span data-stu-id="e4cb5-319">You must configure NAT on the AzS-bgpnat01 virtual machine to allow the site-to-site VPN connection to connect on both ends.</span></span> 

<span data-ttu-id="e4cb5-320">若要設定 VPN 連線，您必須建立靜態 NAT 對應路由，以將 BGPNAT 虛擬機器上的外部介面對應至「邊緣閘道集區」的 VIP。</span><span class="sxs-lookup"><span data-stu-id="e4cb5-320">To configure the VPN connection, you must create a static NAT map route that maps the external interface on the BGPNAT virtual machine to the VIP of the Edge Gateway Pool.</span></span> <span data-ttu-id="e4cb5-321">VPN 連線中的每個連接埠都必須要有一個靜態 NAT 對應路由。</span><span class="sxs-lookup"><span data-stu-id="e4cb5-321">A static NAT map route is required for each port in a VPN connection.</span></span>

> [!NOTE]
> <span data-ttu-id="e4cb5-322">只有「Azure Stack 開發套件」環境才需要此組態。</span><span class="sxs-lookup"><span data-stu-id="e4cb5-322">This configuration is required for Azure Stack Development Kit environments only.</span></span>
> 
> 

### <a name="configure-the-nat"></a><span data-ttu-id="e4cb5-323">設定 NAT</span><span class="sxs-lookup"><span data-stu-id="e4cb5-323">Configure the NAT</span></span>
> [!IMPORTANT]
> <span data-ttu-id="e4cb5-324">您必須為兩個「Azure Stack 開發套件」環境都完成此程序。</span><span class="sxs-lookup"><span data-stu-id="e4cb5-324">You must complete this procedure for *both* Azure Stack Development Kit environments.</span></span>

1. <span data-ttu-id="e4cb5-325">決定要在下列 PowerShell 指令碼中使用的「內部 IP 位址」。</span><span class="sxs-lookup"><span data-stu-id="e4cb5-325">Determine the **Internal IP address** to use in the following PowerShell script.</span></span> <span data-ttu-id="e4cb5-326">開啟虛擬網路閘道 (GW1 和 GW2)，然後在 [概觀] 刀鋒視窗上，儲存 [公用 IP 位址] 的值以供稍後使用。</span><span class="sxs-lookup"><span data-stu-id="e4cb5-326">Open the virtual network gateway (GW1 and GW2), and then on the **Overview** blade, save the value for the **Public IP address** for later use.</span></span>
<span data-ttu-id="e4cb5-327">![內部 IP 位址](media/azure-stack-create-vpn-connection-one-node-tp2/InternalIP.PNG)</span><span class="sxs-lookup"><span data-stu-id="e4cb5-327">![Internal IP address](media/azure-stack-create-vpn-connection-one-node-tp2/InternalIP.PNG)</span></span>
2. <span data-ttu-id="e4cb5-328">登入 POC1 的 Azure Stack 實體機器。</span><span class="sxs-lookup"><span data-stu-id="e4cb5-328">Sign in to the Azure Stack physical machine for POC1.</span></span>
3. <span data-ttu-id="e4cb5-329">複製並編輯下列 PowerShell 指令碼。</span><span class="sxs-lookup"><span data-stu-id="e4cb5-329">Copy and edit the following PowerShell script.</span></span> <span data-ttu-id="e4cb5-330">若要在每個「Azure Stack 開發套件」上設定 NAT，請在已提高權限的 Windows PowerShell ISE 中執行該指令碼。</span><span class="sxs-lookup"><span data-stu-id="e4cb5-330">To configure the NAT on each Azure Stack Development Kit, run the script in an elevated Windows PowerShell ISE.</span></span> <span data-ttu-id="e4cb5-331">在指令碼中，將值新增到 [外部 BGPNAT 位址] 和 [內部 IP 位址] 預留位置：</span><span class="sxs-lookup"><span data-stu-id="e4cb5-331">In the script, add values to the *External BGPNAT address* and *Internal IP address* placeholders:</span></span>

   ```powershell
   # Designate the external NAT address for the ports that use the IKE authentication.
   Invoke-Command `
    -ComputerName AzS-bgpnat01 `
     {Add-NetNatExternalAddress `
      -NatName BGPNAT `
      -IPAddress <External BGPNAT address> `
      -PortStart 499 `
      -PortEnd 501}
   Invoke-Command `
    -ComputerName AzS-bgpnat01 `
     {Add-NetNatExternalAddress `
      -NatName BGPNAT `
      -IPAddress <External BGPNAT address> `
      -PortStart 4499 `
      -PortEnd 4501}
   # create a static NAT mapping to map the external address to the Gateway
   # Public IP Address to map the ISAKMP port 500 for PHASE 1 of the IPSEC tunnel
   Invoke-Command `
    -ComputerName AzS-bgpnat01 `
     {Add-NetNatStaticMapping `
      -NatName BGPNAT `
      -Protocol UDP `
      -ExternalIPAddress <External BGPNAT address> `
      -InternalIPAddress <Internal IP address> `
      -ExternalPort 500 `
      -InternalPort 500}
   # Finally, configure NAT traversal which uses port 4500 to
   # successfully establish the complete IPSEC tunnel over NAT devices
   Invoke-Command `
    -ComputerName AzS-bgpnat01 `
     {Add-NetNatStaticMapping `
      -NatName BGPNAT `
      -Protocol UDP `
      -ExternalIPAddress <External BGPNAT address> `
      -InternalIPAddress <Internal IP address> `
      -ExternalPort 4500 `
      -InternalPort 4500}
   ```

4. <span data-ttu-id="e4cb5-332">在 POC2 上重複執行此程序。</span><span class="sxs-lookup"><span data-stu-id="e4cb5-332">Repeat this procedure on POC2.</span></span>

## <a name="test-the-connection"></a><span data-ttu-id="e4cb5-333">測試連線</span><span class="sxs-lookup"><span data-stu-id="e4cb5-333">Test the connection</span></span>
<span data-ttu-id="e4cb5-334">既然已建立站對站連線，您現在應驗證是否可以透過它傳送流量。</span><span class="sxs-lookup"><span data-stu-id="e4cb5-334">Now that the site-to-site connection is established, you should validate that you can get traffic flowing through it.</span></span> <span data-ttu-id="e4cb5-335">若要驗證，請登入您在其中一個「Azure Stack 開發套件」環境中建立的其中一部虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="e4cb5-335">To validate, sign in to one of the virtual machines that you created in either Azure Stack Development Kit environment.</span></span> <span data-ttu-id="e4cb5-336">接著，Ping 您在另一個環境中建立的虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="e4cb5-336">Then, ping the virtual machine that you created in the other environment.</span></span> 

<span data-ttu-id="e4cb5-337">為了確保您是透過站對站連線傳送流量，請確定您 Ping 的是遠端子網路上虛擬機器的直接 IP (DIP) 位址，而非 VIP。</span><span class="sxs-lookup"><span data-stu-id="e4cb5-337">To ensure that you send the traffic through the site-to-site connection, ensure that you ping the Direct IP (DIP) address of the virtual machine on the remote subnet, not the VIP.</span></span> <span data-ttu-id="e4cb5-338">若要這麼做，請找出連線另一端的 DIP 位址。</span><span class="sxs-lookup"><span data-stu-id="e4cb5-338">To do this, find the DIP address on the other end of the connection.</span></span> <span data-ttu-id="e4cb5-339">儲存位址以供稍後使用。</span><span class="sxs-lookup"><span data-stu-id="e4cb5-339">Save the address for later use.</span></span>

### <a name="sign-in-to-the-tenant-vm-in-poc1"></a><span data-ttu-id="e4cb5-340">登入 POC1 中的租用戶 VM</span><span class="sxs-lookup"><span data-stu-id="e4cb5-340">Sign in to the tenant VM in POC1</span></span>
1. <span data-ttu-id="e4cb5-341">登入 POC1 的 Azure Stack 實體機器，然後使用租用戶帳戶來登入使用者入口網站。</span><span class="sxs-lookup"><span data-stu-id="e4cb5-341">Sign in to the Azure Stack physical machine for POC1, and then use a tenant account to sign in to the user portal.</span></span>
2. <span data-ttu-id="e4cb5-342">在左導覽列中，選取 [計算]。</span><span class="sxs-lookup"><span data-stu-id="e4cb5-342">In the left navigation bar, select **Compute**.</span></span>
3. <span data-ttu-id="e4cb5-343">在 VM 清單中，尋找您先前建立的 **VM01**，然後選取它。</span><span class="sxs-lookup"><span data-stu-id="e4cb5-343">In the list of VMs, find **VM01** that you created previously, and then select it.</span></span>
4. <span data-ttu-id="e4cb5-344">在虛擬機器的刀鋒視窗上，按一下 [連線]，然後開啟 VM01.rdp 檔案。</span><span class="sxs-lookup"><span data-stu-id="e4cb5-344">On the blade for the virtual machine, click **Connect**, and then open the VM01.rdp file.</span></span>
   
     ![[連線] 按鈕](media/azure-stack-create-vpn-connection-one-node-tp2/image17.png)
5. <span data-ttu-id="e4cb5-346">使用您建立虛擬網路時所設定的帳戶來登入。</span><span class="sxs-lookup"><span data-stu-id="e4cb5-346">Sign in with the account that you configured when you created the virtual machine.</span></span>
6. <span data-ttu-id="e4cb5-347">開啟已提高權限的 [Windows PowerShell] 視窗。</span><span class="sxs-lookup"><span data-stu-id="e4cb5-347">Open an elevated **Windows PowerShell** window.</span></span>
7. <span data-ttu-id="e4cb5-348">輸入 **ipconfig /all**。</span><span class="sxs-lookup"><span data-stu-id="e4cb5-348">Enter **ipconfig /all**.</span></span>
8. <span data-ttu-id="e4cb5-349">在輸出中，尋找「IPv4 位址」，然後儲存該位址以供稍後使用。</span><span class="sxs-lookup"><span data-stu-id="e4cb5-349">In the output, find the **IPv4 Address**, and then save the address for later use.</span></span> <span data-ttu-id="e4cb5-350">這是您將從 POC2 Ping 的位址。</span><span class="sxs-lookup"><span data-stu-id="e4cb5-350">This is the address that you will ping from POC2.</span></span> <span data-ttu-id="e4cb5-351">在範例環境中，位址是 **10.0.10.4**，但在您的環境中可能會不同。</span><span class="sxs-lookup"><span data-stu-id="e4cb5-351">In the example environment, the address is **10.0.10.4**, but in your environment it might be different.</span></span> <span data-ttu-id="e4cb5-352">它應該落在您先前建立的 **10.0.10.0/24** 子網路內。</span><span class="sxs-lookup"><span data-stu-id="e4cb5-352">It should fall within the **10.0.10.0/24** subnet that you created previously.</span></span>
9. <span data-ttu-id="e4cb5-353">若要建立允許虛擬機器回應 Ping 的防火牆規則，請執行下列 PowerShell 命令：</span><span class="sxs-lookup"><span data-stu-id="e4cb5-353">To create a firewall rule that allows the virtual machine to respond to pings, run the following PowerShell command:</span></span>

   ```powershell
   New-NetFirewallRule `
    –DisplayName “Allow ICMPv4-In” `
    –Protocol ICMPv4
   ```

### <a name="sign-in-to-the-tenant-vm-in-poc2"></a><span data-ttu-id="e4cb5-354">登入 POC2 中的租用戶 VM</span><span class="sxs-lookup"><span data-stu-id="e4cb5-354">Sign in to the tenant VM in POC2</span></span>
1. <span data-ttu-id="e4cb5-355">登入 POC2 的 Azure Stack 實體機器，然後使用租用戶帳戶來登入使用者入口網站。</span><span class="sxs-lookup"><span data-stu-id="e4cb5-355">Sign in to the Azure Stack physical machine for POC2, and then use a tenant account to sign in to the user portal.</span></span>
2. <span data-ttu-id="e4cb5-356">在左導覽列中，按一下 [計算]。</span><span class="sxs-lookup"><span data-stu-id="e4cb5-356">In the left navigation bar, click **Compute**.</span></span>
3. <span data-ttu-id="e4cb5-357">從虛擬機器清單中，尋找您先前建立的 **VM02**，然後選取它。</span><span class="sxs-lookup"><span data-stu-id="e4cb5-357">From the list of virtual machines, find **VM02** that you created previously, and then select it.</span></span>
4. <span data-ttu-id="e4cb5-358">在虛擬機器的刀鋒視窗中，按一下 [ **連線**]。</span><span class="sxs-lookup"><span data-stu-id="e4cb5-358">On the blade for the virtual machine, click **Connect**.</span></span>
5. <span data-ttu-id="e4cb5-359">使用您建立虛擬網路時所設定的帳戶來登入。</span><span class="sxs-lookup"><span data-stu-id="e4cb5-359">Sign in with the account that you configured when you created the virtual machine.</span></span>
6. <span data-ttu-id="e4cb5-360">開啟已提高權限的 [Windows PowerShell] 視窗。</span><span class="sxs-lookup"><span data-stu-id="e4cb5-360">Open an elevated **Windows PowerShell** window.</span></span>
7. <span data-ttu-id="e4cb5-361">輸入 **ipconfig /all**。</span><span class="sxs-lookup"><span data-stu-id="e4cb5-361">Enter **ipconfig /all**.</span></span>
8. <span data-ttu-id="e4cb5-362">您應該會看到落在 **10.0.20.0/24** 內的 IPv4 位址。</span><span class="sxs-lookup"><span data-stu-id="e4cb5-362">You should see an IPv4 address that falls within **10.0.20.0/24**.</span></span> <span data-ttu-id="e4cb5-363">在範例環境中，該位址是 **10.0.20.4**，但您的位址可能會不同。</span><span class="sxs-lookup"><span data-stu-id="e4cb5-363">In the example environment, the address is **10.0.20.4**, but your address might be different.</span></span>
9. <span data-ttu-id="e4cb5-364">若要建立允許虛擬機器回應 Ping 的防火牆規則，請執行下列 PowerShell 命令：</span><span class="sxs-lookup"><span data-stu-id="e4cb5-364">To create a firewall rule that allows the virtual machine to respond to pings, run the following PowerShell command:</span></span>

   ```powershell
   New-NetFirewallRule `
    –DisplayName “Allow ICMPv4-In” `
    –Protocol ICMPv4
   ```

10. <span data-ttu-id="e4cb5-365">從 POC2 上的虛擬機器，透過通道 Ping POC1 上的虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="e4cb5-365">From the virtual machine on POC2, ping the virtual machine on POC1, through the tunnel.</span></span> <span data-ttu-id="e4cb5-366">若要這麼做，您需 Ping 從 VM01 記錄的 DIP。</span><span class="sxs-lookup"><span data-stu-id="e4cb5-366">To do this, you ping the DIP that you recorded from VM01.</span></span>
   <span data-ttu-id="e4cb5-367">在範例環境中，這是 **10.0.10.4**，但請務必 Ping 您在實驗室中記下的位址。</span><span class="sxs-lookup"><span data-stu-id="e4cb5-367">In the example environment, this is **10.0.10.4**, but be sure to ping the address you noted in your lab.</span></span> <span data-ttu-id="e4cb5-368">您應該會看到如下所示的結果：</span><span class="sxs-lookup"><span data-stu-id="e4cb5-368">You should see a result that looks like the following:</span></span>
   
    ![成功的 Ping](media/azure-stack-create-vpn-connection-one-node-tp2/image19b.png)
11. <span data-ttu-id="e4cb5-370">來自遠端虛擬機器的回覆表示測試成功！</span><span class="sxs-lookup"><span data-stu-id="e4cb5-370">A reply from the remote virtual machine indicates a successful test!</span></span> <span data-ttu-id="e4cb5-371">您可以關閉虛擬機器視窗。</span><span class="sxs-lookup"><span data-stu-id="e4cb5-371">You can close the virtual machine window.</span></span> <span data-ttu-id="e4cb5-372">若要測試您的連線，您可以嘗試其他類型的資料傳輸，例如檔案複製。</span><span class="sxs-lookup"><span data-stu-id="e4cb5-372">To test your connection, you can try other kinds of data transfers like a file copy.</span></span>

### <a name="viewing-data-transfer-statistics-through-the-gateway-connection"></a><span data-ttu-id="e4cb5-373">檢視透過閘道連線的資料傳輸統計資料</span><span class="sxs-lookup"><span data-stu-id="e4cb5-373">Viewing data transfer statistics through the gateway connection</span></span>
<span data-ttu-id="e4cb5-374">如果您想要知道有多少資料通過您的站對站連線，可在 [連線] 刀鋒視窗中取得此資訊。</span><span class="sxs-lookup"><span data-stu-id="e4cb5-374">If you want to know how much data passes through your site-to-site connection, this information is available on the **Connection** blade.</span></span> <span data-ttu-id="e4cb5-375">此測試也是確認您剛傳送的 Ping 是否真的通過 VPN 連線的另一種方法。</span><span class="sxs-lookup"><span data-stu-id="e4cb5-375">This test is also another way to verify that the ping you just sent actually went through the VPN connection.</span></span>

1. <span data-ttu-id="e4cb5-376">在您已登入 POC2 中租用戶虛擬機器的情況下，使用您的租用戶帳戶來登入使用者入口網站。</span><span class="sxs-lookup"><span data-stu-id="e4cb5-376">While you're signed in to the tenant virtual machine in POC2, use your tenant account to sign in to the user portal.</span></span>
2. <span data-ttu-id="e4cb5-377">移至 [所有資源]，然後選取 [POC2-POC1] 連線。</span><span class="sxs-lookup"><span data-stu-id="e4cb5-377">Go to **All resources**, and then select the **POC2-POC1** connection.</span></span> <span data-ttu-id="e4cb5-378">[連線] 隨即顯示。</span><span class="sxs-lookup"><span data-stu-id="e4cb5-378">**Connections** appears.</span></span>
4. <span data-ttu-id="e4cb5-379">在 [連線] 刀鋒視窗上，會顯示 [資料輸入] 和 [資料輸出] 的統計資料。</span><span class="sxs-lookup"><span data-stu-id="e4cb5-379">On the **Connection** blade, the statistics for **Data in** and **Data out** appear.</span></span> <span data-ttu-id="e4cb5-380">在以下的螢幕擷取畫面中，那些大的數字歸因於額外的檔案傳輸。</span><span class="sxs-lookup"><span data-stu-id="e4cb5-380">In the following screenshot, the large numbers are attributed to additional file transfer.</span></span> <span data-ttu-id="e4cb5-381">您應該會在該處看到一些非零的值。</span><span class="sxs-lookup"><span data-stu-id="e4cb5-381">You should see some nonzero values there.</span></span>
   
    ![資料輸入和輸出](media/azure-stack-create-vpn-connection-one-node-tp2/image20.png)
