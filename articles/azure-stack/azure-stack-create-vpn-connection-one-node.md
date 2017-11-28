---
title: "aaaCreate Azure 堆疊開發套件的不同環境中的兩個虛擬網路之間的站對站 VPN 連線 |Microsoft 文件"
description: "雲端系統管理員會使用兩個單一節點 Azure 堆疊開發套件環境之間 toocreate 網站-站台 VPN 連線的逐步程序。"
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
ms.openlocfilehash: 74225a82efae7d9ca6dc08b45ff04c578fae785c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-site-to-site-vpn-connection-between-two-virtual-networks-in-different-azure-stack-development-kit-environments"></a><span data-ttu-id="b3879-103">在不同 Azure Stack 開發套件環境中的兩個虛擬網路之間建立站對站 VPN 連線</span><span class="sxs-lookup"><span data-stu-id="b3879-103">Create a site-to-site VPN connection between two virtual networks in different Azure Stack Development Kit environments</span></span>
## <a name="overview"></a><span data-ttu-id="b3879-104">概觀</span><span class="sxs-lookup"><span data-stu-id="b3879-104">Overview</span></span>
<span data-ttu-id="b3879-105">本文章將示範如何 toocreate 在兩個不同的 Azure 堆疊開發套件環境的兩個虛擬網路之間的站對站 VPN 連線。</span><span class="sxs-lookup"><span data-stu-id="b3879-105">This article shows you how toocreate a site-to-site VPN connection between two virtual networks in two separate Azure Stack Development Kit environments.</span></span> <span data-ttu-id="b3879-106">當您設定 hello 連線時，您了解 Azure 堆疊中的 VPN 閘道的運作方式。</span><span class="sxs-lookup"><span data-stu-id="b3879-106">While you configure hello connections, you learn how VPN gateways in Azure Stack work.</span></span>

### <a name="connection-diagram"></a><span data-ttu-id="b3879-107">連接圖表</span><span class="sxs-lookup"><span data-stu-id="b3879-107">Connection diagram</span></span>
<span data-ttu-id="b3879-108">hello 圖 hello 連線組態應該看起來像當您完成。</span><span class="sxs-lookup"><span data-stu-id="b3879-108">hello following diagram shows what hello connection configuration should look like when you’re done.</span></span>

![站對站 VPN 連線組態](media/azure-stack-create-vpn-connection-one-node-tp2/OneNodeS2SVPN.png)

### <a name="before-you-begin"></a><span data-ttu-id="b3879-110">開始之前</span><span class="sxs-lookup"><span data-stu-id="b3879-110">Before you begin</span></span>
<span data-ttu-id="b3879-111">toocomplete hello 連接組態中，確定您已擁有 hello 下列項目，才能開始：</span><span class="sxs-lookup"><span data-stu-id="b3879-111">toocomplete hello connection configuration, ensure that you have hello following items before you begin:</span></span>

* <span data-ttu-id="b3879-112">兩個伺服器都符合 hello Azure 堆疊開發套件的硬體需求，這會由 hello [Azure 堆疊部署必要條件](azure-stack-deploy.md)。</span><span class="sxs-lookup"><span data-stu-id="b3879-112">Two servers that meet hello Azure Stack Development Kit hardware requirements, which are defined by hello [Azure Stack deployment prerequisites](azure-stack-deploy.md).</span></span> <span data-ttu-id="b3879-113">請確定該 hello hello 中出現的其他先決條件[文章](azure-stack-deploy.md)太履行。</span><span class="sxs-lookup"><span data-stu-id="b3879-113">Ensure that hello other prerequisites that appear in hello [article](azure-stack-deploy.md) are fulfilled too.</span></span>
* <span data-ttu-id="b3879-114">hello [Azure 堆疊開發套件](https://azure.microsoft.com/en-us/overview/azure-stack/try/)部署套件。</span><span class="sxs-lookup"><span data-stu-id="b3879-114">hello [Azure Stack Development Kit](https://azure.microsoft.com/en-us/overview/azure-stack/try/) deployment package.</span></span>

## <a name="deploy-hello-azure-stack-development-kit-environments"></a><span data-ttu-id="b3879-115">部署 hello Azure 堆疊開發組件環境</span><span class="sxs-lookup"><span data-stu-id="b3879-115">Deploy hello Azure Stack Development Kit environments</span></span>
<span data-ttu-id="b3879-116">toocomplete hello 連接組態中，您必須部署兩個 Azure 堆疊開發套件的環境。</span><span class="sxs-lookup"><span data-stu-id="b3879-116">toocomplete hello connection configuration, you must deploy two Azure Stack Development Kit environments.</span></span>
> [!NOTE] 
> <span data-ttu-id="b3879-117">您部署每個 Azure 堆疊開發套件，請遵循 hello[部署指示](azure-stack-run-powershell-script.md)。</span><span class="sxs-lookup"><span data-stu-id="b3879-117">For each Azure Stack Development Kit that you deploy, follow hello [deployment instructions](azure-stack-run-powershell-script.md).</span></span> <span data-ttu-id="b3879-118">在本文中，稱為 hello Azure 堆疊開發套件環境*POC1*和*POC2*。</span><span class="sxs-lookup"><span data-stu-id="b3879-118">In this article, hello Azure Stack Development Kit environments are called *POC1* and *POC2*.</span></span>


## <a name="prepare-an-offer-on-poc1-and-poc2"></a><span data-ttu-id="b3879-119">在 POC1 和 POC2 上準備供應項目</span><span class="sxs-lookup"><span data-stu-id="b3879-119">Prepare an offer on POC1 and POC2</span></span>
<span data-ttu-id="b3879-120">POC1 和 POC2 準備提供項目，可讓使用者可以訂閱 toohello 供應項目，並部署 hello 虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="b3879-120">On both POC1 and POC2, prepare an offer so that a user can subscribe toohello offer and deploy hello virtual machines.</span></span> <span data-ttu-id="b3879-121">如需詳細資訊 toocreate 的供應項目，請參閱[讓虛擬機器可用 tooyour Azure 堆疊使用者](azure-stack-tutorial-tenant-vm.md)。</span><span class="sxs-lookup"><span data-stu-id="b3879-121">For information on how toocreate an offer, see [Make virtual machines available tooyour Azure Stack users](azure-stack-tutorial-tenant-vm.md).</span></span>

## <a name="review-and-complete-hello-network-configuration-table"></a><span data-ttu-id="b3879-122">檢閱並完成 hello 網路組態資料表</span><span class="sxs-lookup"><span data-stu-id="b3879-122">Review and complete hello network configuration table</span></span>
<span data-ttu-id="b3879-123">hello 下表摘要說明這兩種 Azure 堆疊開發套件環境的 hello 網路組態。</span><span class="sxs-lookup"><span data-stu-id="b3879-123">hello following table summarizes hello network configuration for both Azure Stack Development Kit environments.</span></span> <span data-ttu-id="b3879-124">使用 hello 資料表 tooadd hello 適合您網路的外部 BGPNAT 位址後面出現的 hello 程序。</span><span class="sxs-lookup"><span data-stu-id="b3879-124">Use hello procedure that appears after hello table tooadd hello External BGPNAT address that is specific for your network.</span></span>

<span data-ttu-id="b3879-125">**網路組態表**</span><span class="sxs-lookup"><span data-stu-id="b3879-125">**Network configuration table**</span></span>
|   |<span data-ttu-id="b3879-126">POC1</span><span class="sxs-lookup"><span data-stu-id="b3879-126">POC1</span></span>|<span data-ttu-id="b3879-127">POC2</span><span class="sxs-lookup"><span data-stu-id="b3879-127">POC2</span></span>|
|---------|---------|---------|
|<span data-ttu-id="b3879-128">虛擬網路名稱</span><span class="sxs-lookup"><span data-stu-id="b3879-128">Virtual network name</span></span>     |<span data-ttu-id="b3879-129">VNET-01</span><span class="sxs-lookup"><span data-stu-id="b3879-129">VNET-01</span></span>|<span data-ttu-id="b3879-130">VNET-02</span><span class="sxs-lookup"><span data-stu-id="b3879-130">VNET-02</span></span> |
|<span data-ttu-id="b3879-131">虛擬網路位址空間</span><span class="sxs-lookup"><span data-stu-id="b3879-131">Virtual network address space</span></span> |<span data-ttu-id="b3879-132">10.0.10.0/23</span><span class="sxs-lookup"><span data-stu-id="b3879-132">10.0.10.0/23</span></span>|<span data-ttu-id="b3879-133">10.0.20.0/23</span><span class="sxs-lookup"><span data-stu-id="b3879-133">10.0.20.0/23</span></span>|
|<span data-ttu-id="b3879-134">子網路名稱</span><span class="sxs-lookup"><span data-stu-id="b3879-134">Subnet name</span></span>     |<span data-ttu-id="b3879-135">Subnet-01</span><span class="sxs-lookup"><span data-stu-id="b3879-135">Subnet-01</span></span>|<span data-ttu-id="b3879-136">Subnet-02</span><span class="sxs-lookup"><span data-stu-id="b3879-136">Subnet-02</span></span>|
|<span data-ttu-id="b3879-137">子網路位址範圍</span><span class="sxs-lookup"><span data-stu-id="b3879-137">Subnet address range</span></span>|<span data-ttu-id="b3879-138">10.0.10.0/24</span><span class="sxs-lookup"><span data-stu-id="b3879-138">10.0.10.0/24</span></span> |<span data-ttu-id="b3879-139">10.0.20.0/24</span><span class="sxs-lookup"><span data-stu-id="b3879-139">10.0.20.0/24</span></span> |
|<span data-ttu-id="b3879-140">閘道器子網路</span><span class="sxs-lookup"><span data-stu-id="b3879-140">Gateway subnet</span></span>     |<span data-ttu-id="b3879-141">10.0.11.0/24</span><span class="sxs-lookup"><span data-stu-id="b3879-141">10.0.11.0/24</span></span>|<span data-ttu-id="b3879-142">10.0.21.0/24</span><span class="sxs-lookup"><span data-stu-id="b3879-142">10.0.21.0/24</span></span>|
|<span data-ttu-id="b3879-143">外部 BGPNAT 位址</span><span class="sxs-lookup"><span data-stu-id="b3879-143">External BGPNAT address</span></span>     |         |         |

> [!NOTE]
> <span data-ttu-id="b3879-144">在 hello 範例環境 hello 外部 BGPNAT IP 位址為 10.16.167.195 POC1，如和 POC2 的 10.16.169.131。</span><span class="sxs-lookup"><span data-stu-id="b3879-144">hello external BGPNAT IP addresses in hello example environment are 10.16.167.195 for POC1, and 10.16.169.131 for POC2.</span></span> <span data-ttu-id="b3879-145">使用 hello 您 Azure 堆疊開發套件的主機，如下列程序 toodetermine hello 外部 BGPNAT IP 位址，然後將它們加入 toohello 先前網路組態資料表。</span><span class="sxs-lookup"><span data-stu-id="b3879-145">Use hello following procedure toodetermine hello external BGPNAT IP addresses for your Azure Stack Development Kit hosts, and then add them toohello previous network configuration table.</span></span>


### <a name="get-hello-ip-address-of-hello-external-adapter-of-hello-nat-vm"></a><span data-ttu-id="b3879-146">取得 hello hello hello NAT VM 的外部介面卡的 IP 位址</span><span class="sxs-lookup"><span data-stu-id="b3879-146">Get hello IP address of hello external adapter of hello NAT VM</span></span>
1. <span data-ttu-id="b3879-147">登入 toohello Azure 堆疊實體機器 POC1。</span><span class="sxs-lookup"><span data-stu-id="b3879-147">Sign in toohello Azure Stack physical machine for POC1.</span></span>
2. <span data-ttu-id="b3879-148">編輯下列 Powershell 程式碼 tooreplace hello 您的系統管理員密碼，然後再執行 hello POC 主機上的 hello 程式碼：</span><span class="sxs-lookup"><span data-stu-id="b3879-148">Edit hello following Powershell code tooreplace your administrator password, and then run hello code on hello POC host:</span></span>

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
3. <span data-ttu-id="b3879-149">新增 hello IP 位址 toohello 網路組態中表格的 hello 上一節。</span><span class="sxs-lookup"><span data-stu-id="b3879-149">Add hello IP address toohello network configuration table that appears in hello previous section.</span></span>

4. <span data-ttu-id="b3879-150">在 POC2 上重複執行此程序。</span><span class="sxs-lookup"><span data-stu-id="b3879-150">Repeat this procedure on POC2.</span></span>

## <a name="create-hello-network-resources-in-poc1"></a><span data-ttu-id="b3879-151">建立 hello POC1 中的網路資源</span><span class="sxs-lookup"><span data-stu-id="b3879-151">Create hello network resources in POC1</span></span>
<span data-ttu-id="b3879-152">您現在建立 hello POC1 網路資源，您需要 tooset 註冊您的閘道。</span><span class="sxs-lookup"><span data-stu-id="b3879-152">Now you create hello POC1 network resources that you need tooset up your gateways.</span></span> <span data-ttu-id="b3879-153">hello 指示會告訴您如何使用 toocreate hello 資源 hello 使用者入口網站。</span><span class="sxs-lookup"><span data-stu-id="b3879-153">hello following instructions show you how toocreate hello resources by using hello user portal.</span></span> <span data-ttu-id="b3879-154">您也可以使用 PowerShell 的程式碼 toocreate hello 資源。</span><span class="sxs-lookup"><span data-stu-id="b3879-154">You can also use PowerShell code toocreate hello resources.</span></span>

![工作流程，則使用的 toocreate 資源](media/azure-stack-create-vpn-connection-one-node-tp2/image2.png)

### <a name="sign-in-as-a-tenant"></a><span data-ttu-id="b3879-156">以租用戶身分登入</span><span class="sxs-lookup"><span data-stu-id="b3879-156">Sign in as a tenant</span></span>
<span data-ttu-id="b3879-157">服務系統管理員可以登入為租用戶 tootest hello 計劃、 提供項目及可能會使用其租用戶的訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="b3879-157">A service administrator can sign in as a tenant tootest hello plans, offers, and subscriptions that their tenants might use.</span></span> <span data-ttu-id="b3879-158">如果您還沒有租用戶帳戶，請先[建立租用戶帳戶](azure-stack-add-new-user-aad.md)再登入。</span><span class="sxs-lookup"><span data-stu-id="b3879-158">If you don’t already have one, [create a tenant account](azure-stack-add-new-user-aad.md) before you sign in.</span></span>

### <a name="create-hello-virtual-network-and-vm-subnet"></a><span data-ttu-id="b3879-159">建立 hello 虛擬網路和 VM 子網路</span><span class="sxs-lookup"><span data-stu-id="b3879-159">Create hello virtual network and VM subnet</span></span>
1. <span data-ttu-id="b3879-160">使用租用戶帳戶 toosign toohello 使用者入口網站中。</span><span class="sxs-lookup"><span data-stu-id="b3879-160">Use a tenant account toosign in toohello user portal.</span></span>
2. <span data-ttu-id="b3879-161">在 hello 使用者入口網站中，選取 **新增**。</span><span class="sxs-lookup"><span data-stu-id="b3879-161">In hello user portal, select **New**.</span></span>

    ![建立新的虛擬網路](media/azure-stack-create-vpn-connection-one-node-tp2/image3.png)

3. <span data-ttu-id="b3879-163">跳過**Marketplace**，然後選取**網路**。</span><span class="sxs-lookup"><span data-stu-id="b3879-163">Go too**Marketplace**, and then select **Networking**.</span></span>
4. <span data-ttu-id="b3879-164">選取 [虛擬網路]。</span><span class="sxs-lookup"><span data-stu-id="b3879-164">Select **Virtual network**.</span></span>
5. <span data-ttu-id="b3879-165">如**名稱**，**位址空間**，**子網路名稱**，和**子網路位址範圍**，稍早出現在使用 hello 值 hello 網路組態資料表。</span><span class="sxs-lookup"><span data-stu-id="b3879-165">For **Name**, **Address space**, **Subnet name**, and **Subnet address range**, use hello values that appear earlier in hello network configuration table.</span></span>
6. <span data-ttu-id="b3879-166">在**訂用帳戶**，會出現您稍早建立的 hello 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="b3879-166">In **Subscription**, hello subscription that you created earlier appears.</span></span>
7. <span data-ttu-id="b3879-167">針對 [資源群組]，您可以建立資源群組，或選取 [使用現有的] \(如果您已經有資源群組)。</span><span class="sxs-lookup"><span data-stu-id="b3879-167">For **Resource Group**, you can either create a resource group or if you already have one, select **Use existing**.</span></span>
8. <span data-ttu-id="b3879-168">請確認 hello 預設位置。</span><span class="sxs-lookup"><span data-stu-id="b3879-168">Verify hello default location.</span></span>
9. <span data-ttu-id="b3879-169">選取**Pin toodashboard**。</span><span class="sxs-lookup"><span data-stu-id="b3879-169">Select **Pin toodashboard**.</span></span>
10. <span data-ttu-id="b3879-170">選取 [ **建立**]。</span><span class="sxs-lookup"><span data-stu-id="b3879-170">Select **Create**.</span></span>

### <a name="create-hello-gateway-subnet"></a><span data-ttu-id="b3879-171">建立 hello 閘道子網路</span><span class="sxs-lookup"><span data-stu-id="b3879-171">Create hello gateway subnet</span></span>
1. <span data-ttu-id="b3879-172">Hello 儀表板中，開啟您稍早建立的 hello VNET 01 虛擬網路資源。</span><span class="sxs-lookup"><span data-stu-id="b3879-172">On hello dashboard, open hello VNET-01 virtual network resource that you created earlier.</span></span>
2. <span data-ttu-id="b3879-173">在 hello**設定**刀鋒視窗中，選取**子網路**。</span><span class="sxs-lookup"><span data-stu-id="b3879-173">On hello **Settings** blade, select **Subnets**.</span></span>
3. <span data-ttu-id="b3879-174">tooadd hello 虛擬網路，閘道子網路選取**閘道子網路**。</span><span class="sxs-lookup"><span data-stu-id="b3879-174">tooadd a gateway subnet to hello virtual network, select **Gateway Subnet**.</span></span>
   
    ![新增閘道子網路](media/azure-stack-create-vpn-connection-one-node-tp2/image4.png)

4. <span data-ttu-id="b3879-176">根據預設，hello 子網路名稱設定太**GatewaySubnet**。</span><span class="sxs-lookup"><span data-stu-id="b3879-176">By default, hello subnet name is set too**GatewaySubnet**.</span></span>
   <span data-ttu-id="b3879-177">閘道子網路相當特殊。</span><span class="sxs-lookup"><span data-stu-id="b3879-177">Gateway subnets are special.</span></span> <span data-ttu-id="b3879-178">toofunction 正常運作，他們必須使用 hello *GatewaySubnet*名稱。</span><span class="sxs-lookup"><span data-stu-id="b3879-178">toofunction properly, they must use hello *GatewaySubnet* name.</span></span>
5. <span data-ttu-id="b3879-179">在**位址範圍**，確認 hello 位址是**10.0.11.0/24**。</span><span class="sxs-lookup"><span data-stu-id="b3879-179">In **Address range**, verify that hello address is **10.0.11.0/24**.</span></span>
6. <span data-ttu-id="b3879-180">選取**確定**toocreate hello 閘道子網路。</span><span class="sxs-lookup"><span data-stu-id="b3879-180">Select **OK** toocreate hello gateway subnet.</span></span>

### <a name="create-hello-virtual-network-gateway"></a><span data-ttu-id="b3879-181">建立 hello 虛擬網路閘道</span><span class="sxs-lookup"><span data-stu-id="b3879-181">Create hello virtual network gateway</span></span>
1. <span data-ttu-id="b3879-182">在 hello Azure 入口網站，選取 **新增**。</span><span class="sxs-lookup"><span data-stu-id="b3879-182">In hello Azure portal, select **New**.</span></span> 
2. <span data-ttu-id="b3879-183">跳過**Marketplace**，然後選取**網路**。</span><span class="sxs-lookup"><span data-stu-id="b3879-183">Go too**Marketplace**, and then select **Networking**.</span></span>
3. <span data-ttu-id="b3879-184">從網路資源的 hello 清單中選取**虛擬網路閘道**。</span><span class="sxs-lookup"><span data-stu-id="b3879-184">From hello list of network resources, select **Virtual network gateway**.</span></span>
4. <span data-ttu-id="b3879-185">在 [名稱] 中，輸入 **GW1**。</span><span class="sxs-lookup"><span data-stu-id="b3879-185">In **Name**, enter **GW1**.</span></span>
5. <span data-ttu-id="b3879-186">選取 hello**虛擬網路**項目 toochoose 虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="b3879-186">Select hello **Virtual network** item toochoose a virtual network.</span></span>
   <span data-ttu-id="b3879-187">選取**VNET 01**從 hello 清單。</span><span class="sxs-lookup"><span data-stu-id="b3879-187">Select **VNET-01** from hello list.</span></span>
6. <span data-ttu-id="b3879-188">選取 hello**公用 IP 位址**功能表項目。</span><span class="sxs-lookup"><span data-stu-id="b3879-188">Select hello **Public IP address** menu item.</span></span> <span data-ttu-id="b3879-189">當 hello**選擇公用 IP 位址**刀鋒視窗隨即開啟，選取**建立新**。</span><span class="sxs-lookup"><span data-stu-id="b3879-189">When hello **Choose public IP address** blade opens, select **Create new**.</span></span>
7. <span data-ttu-id="b3879-190">在 [名稱] 中輸入 **GW1-PiP**，然後選取 [確定]。</span><span class="sxs-lookup"><span data-stu-id="b3879-190">In **Name**, enter **GW1-PiP**, and then select **OK**.</span></span>
8.  <span data-ttu-id="b3879-191">針對 [VPN 類型]，預設會選取 [依路由]。</span><span class="sxs-lookup"><span data-stu-id="b3879-191">By default, for **VPN type**, **Route-based** is selected.</span></span>
    <span data-ttu-id="b3879-192">保留 hello**路由式**VPN 類型。</span><span class="sxs-lookup"><span data-stu-id="b3879-192">Keep hello **Route-based** VPN type.</span></span>
9. <span data-ttu-id="b3879-193">確認 [訂用帳戶] 和 [位置] 均正確無誤。</span><span class="sxs-lookup"><span data-stu-id="b3879-193">Verify that **Subscription** and **Location** are correct.</span></span> <span data-ttu-id="b3879-194">您可以釘選 hello 資源 toohello 儀表板。</span><span class="sxs-lookup"><span data-stu-id="b3879-194">You can pin hello resource toohello dashboard.</span></span> <span data-ttu-id="b3879-195">選取 [ **建立**]。</span><span class="sxs-lookup"><span data-stu-id="b3879-195">Select **Create**.</span></span>

### <a name="create-hello-local-network-gateway"></a><span data-ttu-id="b3879-196">建立 hello 區域網路閘道</span><span class="sxs-lookup"><span data-stu-id="b3879-196">Create hello local network gateway</span></span>
<span data-ttu-id="b3879-197">hello 實作*區域網路閘道*此 Azure 堆疊評估部署會比實際的 Azure 部署中有些許不同。</span><span class="sxs-lookup"><span data-stu-id="b3879-197">hello implementation of a *local network gateway* in this Azure Stack evaluation deployment is a bit different than in an actual Azure deployment.</span></span>

<span data-ttu-id="b3879-198">在 Azure 部署中，區域網路閘道代表內部 （在 hello 租用戶） 實體裝置，您在 Azure 中使用 tooconnect tooa 虛擬網路閘道。</span><span class="sxs-lookup"><span data-stu-id="b3879-198">In an Azure deployment, a local network gateway represents an on-premises (at hello tenant) physical device, that you use tooconnect tooa virtual network gateway in Azure.</span></span> <span data-ttu-id="b3879-199">此 Azure 堆疊評估部署時，在 hello 連接的兩端是虛擬網路閘道 ！</span><span class="sxs-lookup"><span data-stu-id="b3879-199">In this Azure Stack evaluation deployment, both ends of hello connection are virtual network gateways!</span></span>

<span data-ttu-id="b3879-200">關於此方式 toothink 更普遍為，hello 區域網路閘道資源一律表示 hello 遠端閘道在 hello hello 連線的另一端。</span><span class="sxs-lookup"><span data-stu-id="b3879-200">A way toothink about this more generically is that hello local network gateway resource always indicates hello remote gateway at hello other end of hello connection.</span></span> <span data-ttu-id="b3879-201">Hello 方式 hello Azure 堆疊開發套件的設計，因為您需要 tooprovide hello IP 位址的 hello 外部網路介面卡上 hello 網路位址轉譯 (NAT) 的 hello VM 其他 Azure 堆疊開發套件為 hello hello 公用 IP 位址區域網路閘道。</span><span class="sxs-lookup"><span data-stu-id="b3879-201">Because of hello way hello Azure Stack Development Kit was designed, you need tooprovide hello IP address of hello external network adapter on hello network address translation (NAT) VM of hello other Azure Stack Development Kit as hello Public IP Address of hello local network gateway.</span></span> <span data-ttu-id="b3879-202">然後，您會建立 NAT 對應上 hello NAT VM toomake 確定兩端都已正確連接。</span><span class="sxs-lookup"><span data-stu-id="b3879-202">You then create NAT mappings on hello NAT VM toomake sure that both ends are connected properly.</span></span>


### <a name="create-hello-local-network-gateway-resource"></a><span data-ttu-id="b3879-203">建立 hello 區域網路閘道資源</span><span class="sxs-lookup"><span data-stu-id="b3879-203">Create hello local network gateway resource</span></span>
1. <span data-ttu-id="b3879-204">登入 toohello Azure 堆疊實體機器 POC1。</span><span class="sxs-lookup"><span data-stu-id="b3879-204">Sign in toohello Azure Stack physical machine for POC1.</span></span>
2. <span data-ttu-id="b3879-205">在 hello 使用者入口網站中，選取 **新增**。</span><span class="sxs-lookup"><span data-stu-id="b3879-205">In hello user portal, select **New**.</span></span>
3. <span data-ttu-id="b3879-206">跳過**Marketplace**，然後選取**網路**。</span><span class="sxs-lookup"><span data-stu-id="b3879-206">Go too**Marketplace**, and then select **Networking**.</span></span>
4. <span data-ttu-id="b3879-207">從 hello 清單中的資源，選取 **區域網路閘道**。</span><span class="sxs-lookup"><span data-stu-id="b3879-207">From hello list of resources, select **local network gateway**.</span></span>
5. <span data-ttu-id="b3879-208">在 [名稱] 中，輸入 **POC2-GW**。</span><span class="sxs-lookup"><span data-stu-id="b3879-208">In **Name**, enter **POC2-GW**.</span></span>
6. <span data-ttu-id="b3879-209">在**IP 位址**，輸入 POC2 hello BGPNAT 外部位址。</span><span class="sxs-lookup"><span data-stu-id="b3879-209">In **IP address**, enter hello External BGPNAT address for POC2.</span></span> <span data-ttu-id="b3879-210">此位址在稍早 hello 網路組態資料表。</span><span class="sxs-lookup"><span data-stu-id="b3879-210">This address appears earlier in hello network configuration table.</span></span>
7. <span data-ttu-id="b3879-211">在**位址空間**，hello 的 hello 您稍後建立 POC2 VNET 位址空間，請輸入**10.0.20.0/23**。</span><span class="sxs-lookup"><span data-stu-id="b3879-211">In **Address Space**, for hello address space of hello POC2 VNET that you create later, enter **10.0.20.0/23**.</span></span>
8. <span data-ttu-id="b3879-212">確認您的 [訂用帳戶]、[資源群組] 和 [位置] 正確無誤，然後選取 [建立]。</span><span class="sxs-lookup"><span data-stu-id="b3879-212">Verify that your **Subscription**, **Resource Group**, and **location** are correct, and then select **Create**.</span></span>

### <a name="create-hello-connection"></a><span data-ttu-id="b3879-213">建立 hello 連線</span><span class="sxs-lookup"><span data-stu-id="b3879-213">Create hello connection</span></span>
1. <span data-ttu-id="b3879-214">在 hello 使用者入口網站中，選取 **新增**。</span><span class="sxs-lookup"><span data-stu-id="b3879-214">In hello user portal, select **New**.</span></span>
2. <span data-ttu-id="b3879-215">跳過**Marketplace**，然後選取**網路**。</span><span class="sxs-lookup"><span data-stu-id="b3879-215">Go too**Marketplace**, and then select **Networking**.</span></span>
3. <span data-ttu-id="b3879-216">從 hello 清單中的資源，選取 **連接**。</span><span class="sxs-lookup"><span data-stu-id="b3879-216">From hello list of resources, select **Connection**.</span></span>
4. <span data-ttu-id="b3879-217">在 hello**基本概念**設定 刀鋒視窗，hello**連線類型**，選取**站對站 (IPSec)**。</span><span class="sxs-lookup"><span data-stu-id="b3879-217">On hello **Basics** settings blade, for hello **Connection type**, select **Site-to-site (IPSec)**.</span></span>
5. <span data-ttu-id="b3879-218">選取 hello**訂用帳戶**，**資源群組**，和**位置**，然後選取**確定**。</span><span class="sxs-lookup"><span data-stu-id="b3879-218">Select hello **Subscription**, **Resource Group**, and **Location**, and then select **OK**.</span></span>
6. <span data-ttu-id="b3879-219">在 hello**設定**刀鋒視窗中，選取**虛擬網路閘道**，然後選取**GW1**。</span><span class="sxs-lookup"><span data-stu-id="b3879-219">On hello **Settings** blade,  select **Virtual network gateway**, and then select **GW1**.</span></span>
7. <span data-ttu-id="b3879-220">選取 [區域網路閘道]，然後選取 [POC2-GW]。</span><span class="sxs-lookup"><span data-stu-id="b3879-220">Select **Local network gateway**, and then select **POC2-GW**.</span></span>
8. <span data-ttu-id="b3879-221">在 [連線名稱] 中，輸入 **POC1-POC2**。</span><span class="sxs-lookup"><span data-stu-id="b3879-221">In **Connection Name**, enter **POC1-POC2**.</span></span>
9. <span data-ttu-id="b3879-222">在 [共用金鑰 (PSK)] 中輸入 **12345**，然後選取 [確定]。</span><span class="sxs-lookup"><span data-stu-id="b3879-222">In **Shared key (PSK)**, enter **12345**, and then select **OK**.</span></span>
10. <span data-ttu-id="b3879-223">在 hello**摘要**刀鋒視窗中，選取**確定**。</span><span class="sxs-lookup"><span data-stu-id="b3879-223">On hello **Summary** blade, select **OK**.</span></span>

### <a name="create-a-vm"></a><span data-ttu-id="b3879-224">建立 VM</span><span class="sxs-lookup"><span data-stu-id="b3879-224">Create a VM</span></span>
<span data-ttu-id="b3879-225">toovalidate hello 必定會行經 hello VPN 連線的資料，您需要 hello 虛擬機器 toosend 和每個 Azure 堆疊開發套件中接收資料。</span><span class="sxs-lookup"><span data-stu-id="b3879-225">toovalidate hello data that travels through hello VPN connection, you need hello virtual machines toosend and receive data in each Azure Stack Development Kit.</span></span> <span data-ttu-id="b3879-226">立即在 POC1 中建立虛擬機器，然後將它放在您虛擬網路的 VM 子網路上。</span><span class="sxs-lookup"><span data-stu-id="b3879-226">Create a virtual machine in POC1 now, and then in your virtual network, put it on your VM subnet.</span></span>

1. <span data-ttu-id="b3879-227">在 hello Azure 入口網站，選取 **新增**。</span><span class="sxs-lookup"><span data-stu-id="b3879-227">In hello Azure portal, select **New**.</span></span>
2. <span data-ttu-id="b3879-228">跳過**Marketplace**，然後選取**計算**。</span><span class="sxs-lookup"><span data-stu-id="b3879-228">Go too**Marketplace**, and then select **Compute**.</span></span>
3. <span data-ttu-id="b3879-229">在虛擬機器的映像的 hello 清單中選取 hello **Windows Server 2016 Eval Datacenter**映像。</span><span class="sxs-lookup"><span data-stu-id="b3879-229">In hello list of virtual machine images, select hello **Windows Server 2016 Datacenter Eval** image.</span></span>
4. <span data-ttu-id="b3879-230">在 hello**基本概念**刀鋒視窗，請在**名稱**，輸入**VM01**。</span><span class="sxs-lookup"><span data-stu-id="b3879-230">On hello **Basics** blade, in **Name**, enter **VM01**.</span></span>
5. <span data-ttu-id="b3879-231">輸入有效的使用者名稱和密碼。</span><span class="sxs-lookup"><span data-stu-id="b3879-231">Enter a valid username and password.</span></span> <span data-ttu-id="b3879-232">在建立後，您可以使用 toohello VM 中的這個帳戶 toosign。</span><span class="sxs-lookup"><span data-stu-id="b3879-232">You use this account toosign in toohello VM after it's created.</span></span>
6. <span data-ttu-id="b3879-233">提供 [訂用帳戶]、[資源群組] 和 [位置]，然後選取 [確定]。</span><span class="sxs-lookup"><span data-stu-id="b3879-233">Provide a **Subscription**, **Resource Group**, and **Location**, and then select **OK**.</span></span>
7. <span data-ttu-id="b3879-234">在 hello**大小**刀鋒視窗中的，這個執行個體，請選取虛擬機器大小，然後選取**選取**。</span><span class="sxs-lookup"><span data-stu-id="b3879-234">On hello **Size** blade, for this instance, select a virtual machine size, and then select **Select**.</span></span>
8. <span data-ttu-id="b3879-235">在 hello**設定**刀鋒視窗中，接受 hello 預設值。</span><span class="sxs-lookup"><span data-stu-id="b3879-235">On hello **Settings** blade, accept hello defaults.</span></span> <span data-ttu-id="b3879-236">請確定該 hello **VNET 01**已選取虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="b3879-236">Ensure that hello **VNET-01** virtual network is selected.</span></span> <span data-ttu-id="b3879-237">確認該 hello 子網路設定得**10.0.10.0/24**。</span><span class="sxs-lookup"><span data-stu-id="b3879-237">Verify that hello subnet is set too**10.0.10.0/24**.</span></span> <span data-ttu-id="b3879-238">然後選取 [確定]。</span><span class="sxs-lookup"><span data-stu-id="b3879-238">Then select **OK**.</span></span>
9. <span data-ttu-id="b3879-239">在 hello**摘要**刀鋒視窗中，檢閱 hello 設定，然後選取**確定**。</span><span class="sxs-lookup"><span data-stu-id="b3879-239">On hello **Summary** blade, review hello settings, and then select **OK**.</span></span>



## <a name="create-hello-network-resources-in-poc2"></a><span data-ttu-id="b3879-240">建立 hello POC2 中的網路資源</span><span class="sxs-lookup"><span data-stu-id="b3879-240">Create hello network resources in POC2</span></span>

<span data-ttu-id="b3879-241">hello 下一個步驟是 POC2 toocreate hello 網路資源。</span><span class="sxs-lookup"><span data-stu-id="b3879-241">hello next step is toocreate hello network resources for POC2.</span></span> <span data-ttu-id="b3879-242">下列指示的 hello 顯示如何使用 toocreate hello 資源 hello 使用者入口網站。</span><span class="sxs-lookup"><span data-stu-id="b3879-242">hello following instructions show how toocreate hello resources by using hello user portal.</span></span>

### <a name="sign-in-as-a-tenant"></a><span data-ttu-id="b3879-243">以租用戶身分登入</span><span class="sxs-lookup"><span data-stu-id="b3879-243">Sign in as a tenant</span></span>
<span data-ttu-id="b3879-244">服務系統管理員可以登入為租用戶 tootest hello 計劃、 提供項目及可能會使用其租用戶的訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="b3879-244">A service administrator can sign in as a tenant tootest hello plans, offers, and subscriptions that their tenants might use.</span></span> <span data-ttu-id="b3879-245">如果您還沒有租用戶帳戶，請先[建立租用戶帳戶](azure-stack-add-new-user-aad.md)再登入。</span><span class="sxs-lookup"><span data-stu-id="b3879-245">If you don’t already have one, [create a tenant account](azure-stack-add-new-user-aad.md) before you sign in.</span></span>

### <a name="create-hello-virtual-network-and-vm-subnet"></a><span data-ttu-id="b3879-246">建立 hello 虛擬網路和 VM 子網路</span><span class="sxs-lookup"><span data-stu-id="b3879-246">Create hello virtual network and VM subnet</span></span>

1. <span data-ttu-id="b3879-247">使用租用戶帳戶來登入。</span><span class="sxs-lookup"><span data-stu-id="b3879-247">Sign in by using a tenant account.</span></span>
2. <span data-ttu-id="b3879-248">在 hello 使用者入口網站中，選取 **新增**。</span><span class="sxs-lookup"><span data-stu-id="b3879-248">In hello user portal, select **New**.</span></span>
3. <span data-ttu-id="b3879-249">跳過**Marketplace**，然後選取**網路**。</span><span class="sxs-lookup"><span data-stu-id="b3879-249">Go too**Marketplace**, and then select **Networking**.</span></span>
4. <span data-ttu-id="b3879-250">選取 [虛擬網路]。</span><span class="sxs-lookup"><span data-stu-id="b3879-250">Select **Virtual network**.</span></span>
5. <span data-ttu-id="b3879-251">使用 hello 資訊出現稍早在 hello 網路組態資料表 tooidentify hello 值 hello POC2**名稱**，**位址空間**，**子網路名稱**，和**子網路位址範圍**。</span><span class="sxs-lookup"><span data-stu-id="b3879-251">Use hello information appearing earlier in hello network configuration table tooidentify hello values for hello POC2 **Name**, **Address space**, **Subnet name**, and **Subnet address range**.</span></span>
6. <span data-ttu-id="b3879-252">在**訂用帳戶**，會出現您稍早建立的 hello 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="b3879-252">In **Subscription**, hello subscription that you created earlier appears.</span></span>
7. <span data-ttu-id="b3879-253">針對 [資源群組]，建立資源群組，或選取 [使用現有的] (如果您已經有資源群組)。</span><span class="sxs-lookup"><span data-stu-id="b3879-253">For **Resource Group**, create a new resource group or, if you already have one, select **Use existing**.</span></span>
8. <span data-ttu-id="b3879-254">確認 hello 預設**位置**。</span><span class="sxs-lookup"><span data-stu-id="b3879-254">Verify hello default **Location**.</span></span>
9. <span data-ttu-id="b3879-255">選取**Pin toodashboard**。</span><span class="sxs-lookup"><span data-stu-id="b3879-255">Select **Pin toodashboard**.</span></span>
10. <span data-ttu-id="b3879-256">選取 [ **建立**]。</span><span class="sxs-lookup"><span data-stu-id="b3879-256">Select **Create**.</span></span>

### <a name="create-hello-gateway-subnet"></a><span data-ttu-id="b3879-257">建立 hello 閘道子網路</span><span class="sxs-lookup"><span data-stu-id="b3879-257">Create hello Gateway Subnet</span></span>
1. <span data-ttu-id="b3879-258">開啟您建立 hello 虛擬網路資源 (**VNET 02**) 從 hello 儀表板。</span><span class="sxs-lookup"><span data-stu-id="b3879-258">Open hello Virtual network resource you created (**VNET-02**) from hello dashboard.</span></span>
2. <span data-ttu-id="b3879-259">在 hello**設定**刀鋒視窗中，選取**子網路**。</span><span class="sxs-lookup"><span data-stu-id="b3879-259">On hello **Settings** blade, select **Subnets**.</span></span>
3. <span data-ttu-id="b3879-260">選取**閘道子網路**tooadd hello 虛擬網路閘道子網路。</span><span class="sxs-lookup"><span data-stu-id="b3879-260">Select  **Gateway subnet** tooadd a gateway subnet to hello virtual network.</span></span>
4. <span data-ttu-id="b3879-261">hello hello 子網路名稱設定得**GatewaySubnet**預設。</span><span class="sxs-lookup"><span data-stu-id="b3879-261">hello name of hello subnet is set too**GatewaySubnet** by default.</span></span>
   <span data-ttu-id="b3879-262">閘道子網路是特殊的且必須是此特定名稱 toofunction 正確。</span><span class="sxs-lookup"><span data-stu-id="b3879-262">Gateway subnets are special and must have this specific name toofunction properly.</span></span>
5. <span data-ttu-id="b3879-263">在 hello**位址範圍**欄位中，請確認 hello 位址**10.0.21.0/24**。</span><span class="sxs-lookup"><span data-stu-id="b3879-263">In hello **Address range** field, verify hello address is **10.0.21.0/24**.</span></span>
6. <span data-ttu-id="b3879-264">選取**確定**toocreate hello 閘道子網路。</span><span class="sxs-lookup"><span data-stu-id="b3879-264">Select **OK** toocreate hello gateway subnet.</span></span>

### <a name="create-hello-virtual-network-gateway"></a><span data-ttu-id="b3879-265">建立 hello 虛擬網路閘道</span><span class="sxs-lookup"><span data-stu-id="b3879-265">Create hello virtual network gateway</span></span>
1. <span data-ttu-id="b3879-266">在 hello Azure 入口網站，選取 **新增**。</span><span class="sxs-lookup"><span data-stu-id="b3879-266">In hello Azure portal, select **New**.</span></span>  
2. <span data-ttu-id="b3879-267">跳過**Marketplace**，然後選取**網路**。</span><span class="sxs-lookup"><span data-stu-id="b3879-267">Go too**Marketplace**, and then select **Networking**.</span></span>
3. <span data-ttu-id="b3879-268">從網路資源的 hello 清單中選取**虛擬網路閘道**。</span><span class="sxs-lookup"><span data-stu-id="b3879-268">From hello list of network resources, select **Virtual network gateway**.</span></span>
4. <span data-ttu-id="b3879-269">在 [名稱] 中，輸入 **GW2**。</span><span class="sxs-lookup"><span data-stu-id="b3879-269">In **Name**, enter **GW2**.</span></span>
5. <span data-ttu-id="b3879-270">toochoose 虛擬網路中，選取**虛擬網路**。</span><span class="sxs-lookup"><span data-stu-id="b3879-270">toochoose a virtual network, select **Virtual network**.</span></span> <span data-ttu-id="b3879-271">然後選取**VNET 02**從 hello 清單。</span><span class="sxs-lookup"><span data-stu-id="b3879-271">Then select **VNET-02** from hello list.</span></span>
6. <span data-ttu-id="b3879-272">選取 [公用 IP 位址]。</span><span class="sxs-lookup"><span data-stu-id="b3879-272">Select **Public IP address**.</span></span> <span data-ttu-id="b3879-273">當 hello**選擇公用 IP 位址**刀鋒視窗隨即開啟，選取**建立新**。</span><span class="sxs-lookup"><span data-stu-id="b3879-273">When hello **Choose public IP address** blade opens, select **Create new**.</span></span>
7. <span data-ttu-id="b3879-274">在 [名稱] 中輸入 **GW2-PiP**，然後選取 [確定]。</span><span class="sxs-lookup"><span data-stu-id="b3879-274">In **Name**, enter **GW2-PiP**, and then select **OK**.</span></span>
8. <span data-ttu-id="b3879-275">針對 [VPN 類型]，預設會選取 [依路由]。</span><span class="sxs-lookup"><span data-stu-id="b3879-275">By default, for **VPN type**, **Route-based** is selected.</span></span>
    <span data-ttu-id="b3879-276">保留 hello**路由式**VPN 類型。</span><span class="sxs-lookup"><span data-stu-id="b3879-276">Keep hello **Route-based** VPN type.</span></span>
9. <span data-ttu-id="b3879-277">確認 [訂用帳戶] 和 [位置] 均正確無誤。</span><span class="sxs-lookup"><span data-stu-id="b3879-277">Verify that **Subscription** and **Location** are correct.</span></span> <span data-ttu-id="b3879-278">您可以釘選 hello 資源 toohello 儀表板。</span><span class="sxs-lookup"><span data-stu-id="b3879-278">You can pin hello resource toohello dashboard.</span></span> <span data-ttu-id="b3879-279">選取 [ **建立**]。</span><span class="sxs-lookup"><span data-stu-id="b3879-279">Select **Create**.</span></span>

### <a name="create-hello-local-network-gateway-resource"></a><span data-ttu-id="b3879-280">建立 hello 區域網路閘道資源</span><span class="sxs-lookup"><span data-stu-id="b3879-280">Create hello local network gateway resource</span></span>

1. <span data-ttu-id="b3879-281">在 hello POC2 使用者入口網站中，選取 **新增**。</span><span class="sxs-lookup"><span data-stu-id="b3879-281">In hello POC2 user portal, select **New**.</span></span> 
4. <span data-ttu-id="b3879-282">跳過**Marketplace**，然後選取**網路**。</span><span class="sxs-lookup"><span data-stu-id="b3879-282">Go too**Marketplace**, and then select **Networking**.</span></span>
5. <span data-ttu-id="b3879-283">從 hello 清單中的資源，選取 **區域網路閘道**。</span><span class="sxs-lookup"><span data-stu-id="b3879-283">From hello list of resources, select **Local network gateway**.</span></span>
6. <span data-ttu-id="b3879-284">在 [名稱] 中，輸入 **POC1-GW**。</span><span class="sxs-lookup"><span data-stu-id="b3879-284">In **Name**, enter **POC1-GW**.</span></span>
7. <span data-ttu-id="b3879-285">在**IP 位址**，輸入稍早在 hello 網路組態資料表中列出的 POC1 hello BGPNAT 外部位址。</span><span class="sxs-lookup"><span data-stu-id="b3879-285">In **IP address**, enter hello External BGPNAT address for POC1 that is listed earlier in hello network configuration table.</span></span>
8. <span data-ttu-id="b3879-286">在**位址空間**，POC1，從輸入 hello **10.0.10.0/23**的位址空間**VNET 01**。</span><span class="sxs-lookup"><span data-stu-id="b3879-286">In **Address Space**, from POC1, enter hello **10.0.10.0/23** address space of **VNET-01**.</span></span>
9. <span data-ttu-id="b3879-287">確認您的 [訂用帳戶]、[資源群組] 和 [位置] 正確無誤，然後選取 [建立]。</span><span class="sxs-lookup"><span data-stu-id="b3879-287">Verify that your **Subscription**, **Resource Group**, and **Location** are correct, and then select **Create**.</span></span>

## <a name="create-hello-connection"></a><span data-ttu-id="b3879-288">建立 hello 連線</span><span class="sxs-lookup"><span data-stu-id="b3879-288">Create hello connection</span></span>
1. <span data-ttu-id="b3879-289">在 hello 使用者入口網站中，選取 **新增**。</span><span class="sxs-lookup"><span data-stu-id="b3879-289">In hello user portal, select **New**.</span></span> 
2. <span data-ttu-id="b3879-290">跳過**Marketplace**，然後選取**網路**。</span><span class="sxs-lookup"><span data-stu-id="b3879-290">Go too**Marketplace**, and then select **Networking**.</span></span>
3. <span data-ttu-id="b3879-291">從 hello 清單中的資源，選取 **連接**。</span><span class="sxs-lookup"><span data-stu-id="b3879-291">From hello list of resources, select **Connection**.</span></span>
4. <span data-ttu-id="b3879-292">在 [hello**基本**設定] 刀鋒視窗，hello**連線類型**，選擇**站對站 (IPSec)**。</span><span class="sxs-lookup"><span data-stu-id="b3879-292">On hello **Basic** settings blade, for hello **Connection type**, choose **Site-to-site (IPSec)**.</span></span>
5. <span data-ttu-id="b3879-293">選取 hello**訂用帳戶**，**資源群組**，和**位置**，然後選取**確定**。</span><span class="sxs-lookup"><span data-stu-id="b3879-293">Select hello **Subscription**, **Resource Group**, and **Location**, and then select **OK**.</span></span>
6. <span data-ttu-id="b3879-294">在 hello**設定**刀鋒視窗中，選取**虛擬網路閘道**，然後選取**GW2**。</span><span class="sxs-lookup"><span data-stu-id="b3879-294">On hello **Settings** blade, select **Virtual network gateway**, and then select **GW2**.</span></span>
7. <span data-ttu-id="b3879-295">選取 [區域網路閘道]，然後選取 [POC1-GW]。</span><span class="sxs-lookup"><span data-stu-id="b3879-295">Select **Local network gateway**, and then select **POC1-GW**.</span></span>
8. <span data-ttu-id="b3879-296">在 [連線名稱] 中，輸入 **POC2-POC1**。</span><span class="sxs-lookup"><span data-stu-id="b3879-296">In **Connection name**, enter **POC2-POC1**.</span></span>
9. <span data-ttu-id="b3879-297">在 [共用金鑰 (PSK)] 中，輸入 **12345**。</span><span class="sxs-lookup"><span data-stu-id="b3879-297">In **Shared key (PSK)**, enter **12345**.</span></span> <span data-ttu-id="b3879-298">如果您選擇不同的值，請記得它*必須*符合 hello hello POC1 建立的共用金鑰的值。</span><span class="sxs-lookup"><span data-stu-id="b3879-298">If you choose a different value, remember that it *must* match hello value for hello shared key that you created on POC1.</span></span> <span data-ttu-id="b3879-299">選取 [確定] 。</span><span class="sxs-lookup"><span data-stu-id="b3879-299">Select **OK**.</span></span>
10. <span data-ttu-id="b3879-300">檢閱 hello**摘要**刀鋒視窗中，然後再選取**確定**。</span><span class="sxs-lookup"><span data-stu-id="b3879-300">Review hello **Summary** blade, and then select **OK**.</span></span>

## <a name="create-a-virtual-machine"></a><span data-ttu-id="b3879-301">建立虛擬機器</span><span class="sxs-lookup"><span data-stu-id="b3879-301">Create a virtual machine</span></span>
<span data-ttu-id="b3879-302">請立即在 POC2 中建立虛擬機器，然後將它放在您虛擬網路的 VM 子網路上。</span><span class="sxs-lookup"><span data-stu-id="b3879-302">Create a virtual machine in POC2 now, and put it on your VM subnet in your virtual network.</span></span>

1. <span data-ttu-id="b3879-303">在 hello Azure 入口網站，選取 **新增**。</span><span class="sxs-lookup"><span data-stu-id="b3879-303">In hello Azure portal, select **New**.</span></span>
2. <span data-ttu-id="b3879-304">跳過**Marketplace**，然後選取**計算**。</span><span class="sxs-lookup"><span data-stu-id="b3879-304">Go too**Marketplace**, and then select **Compute**.</span></span>
3. <span data-ttu-id="b3879-305">在虛擬機器的映像的 hello 清單中選取 hello **Windows Server 2016 Eval Datacenter**映像。</span><span class="sxs-lookup"><span data-stu-id="b3879-305">In hello list of virtual machine images, select hello **Windows Server 2016 Datacenter Eval** image.</span></span>
4. <span data-ttu-id="b3879-306">在 hello**基本概念**刀鋒視窗中，針對**名稱**，輸入**VM02**。</span><span class="sxs-lookup"><span data-stu-id="b3879-306">On hello **Basics** blade, for **Name**, enter **VM02**.</span></span>
5. <span data-ttu-id="b3879-307">輸入有效的使用者名稱和密碼。</span><span class="sxs-lookup"><span data-stu-id="b3879-307">Enter a valid username and password.</span></span> <span data-ttu-id="b3879-308">在建立後，您可以使用 toohello 虛擬機器中的這個帳戶 toosign。</span><span class="sxs-lookup"><span data-stu-id="b3879-308">You use this account toosign in toohello virtual machine after it's created.</span></span>
6. <span data-ttu-id="b3879-309">提供 [訂用帳戶]、[資源群組] 和 [位置]，然後選取 [確定]。</span><span class="sxs-lookup"><span data-stu-id="b3879-309">Provide a **Subscription**, **Resource Group**, and **Location**, and then select **OK**.</span></span>
7. <span data-ttu-id="b3879-310">在 hello**大小**刀鋒視窗中，選取虛擬機器大小會針對這個執行個體，然後**選取**。</span><span class="sxs-lookup"><span data-stu-id="b3879-310">On hello **Size** blade, select a virtual machine size for this instance, and then select **Select**.</span></span>
8. <span data-ttu-id="b3879-311">在 hello**設定**刀鋒視窗中，您可以接受 hello 預設值。</span><span class="sxs-lookup"><span data-stu-id="b3879-311">On hello **Settings** blade, you can accept hello defaults.</span></span> <span data-ttu-id="b3879-312">請確定該 hello **VNET 02**虛擬網路已選取，並確認該 hello 子網路設定得**10.0.20.0/24**。</span><span class="sxs-lookup"><span data-stu-id="b3879-312">Ensure that hello **VNET-02** virtual network is selected, and verify that hello subnet is set too**10.0.20.0/24**.</span></span> <span data-ttu-id="b3879-313">選取 [確定] 。</span><span class="sxs-lookup"><span data-stu-id="b3879-313">Select **OK**.</span></span>
9. <span data-ttu-id="b3879-314">檢閱上 hello 的 hello 設定**摘要**刀鋒視窗中，然後再選取**確定**。</span><span class="sxs-lookup"><span data-stu-id="b3879-314">Review hello settings on hello **Summary** blade, and then select **OK**.</span></span>

## <a name="configure-hello-nat-virtual-machine-on-each-azure-stack-development-kit-for-gateway-traversal"></a><span data-ttu-id="b3879-315">設定 hello NAT 虛擬機器上的閘道周遊每個 Azure 堆疊開發套件</span><span class="sxs-lookup"><span data-stu-id="b3879-315">Configure hello NAT virtual machine on each Azure Stack Development Kit for gateway traversal</span></span>
<span data-ttu-id="b3879-316">因為 hello Azure 堆疊開發套件是獨立且從部署的 hello 實體主機的網路隔離，所以 hello*外部*VIP，都不會實際外部連接的 toois hello 閘道的網路。</span><span class="sxs-lookup"><span data-stu-id="b3879-316">Because hello Azure Stack Development Kit is self-contained and isolated from the network on which hello physical host is deployed, hello *external* VIP network that hello gateways are connected toois not actually external.</span></span> <span data-ttu-id="b3879-317">相反地，隱藏 hello VIP 網路執行網路位址轉譯之路由器的後面。</span><span class="sxs-lookup"><span data-stu-id="b3879-317">Instead, hello VIP network is hidden behind a router that performs network address translation.</span></span> 

<span data-ttu-id="b3879-318">路由器是 Windows Server 虛擬機器，稱為*AzS bgpnat01*、 執行路由及遠端存取服務 (RRAS) 角色中的 hello Azure 堆疊開發套件基礎結構。</span><span class="sxs-lookup"><span data-stu-id="b3879-318">The router is a Windows Server virtual machine, called *AzS-bgpnat01*, that runs the Routing and Remote Access Services (RRAS) role in hello Azure Stack Development Kit infrastructure.</span></span> <span data-ttu-id="b3879-319">您必須設定 NAT hello AzS bgpnat01 虛擬機器 tooallow hello 站對站 VPN 連線 tooconnect 兩端上。</span><span class="sxs-lookup"><span data-stu-id="b3879-319">You must configure NAT on hello AzS-bgpnat01 virtual machine tooallow hello site-to-site VPN connection tooconnect on both ends.</span></span> 

<span data-ttu-id="b3879-320">tooconfigure hello VPN 連線，您必須建立對應 hello hello BGPNAT 虛擬機器 toohello VIP 的 hello 邊緣閘道集區上的外部介面的靜態 NAT 對應路由。</span><span class="sxs-lookup"><span data-stu-id="b3879-320">tooconfigure hello VPN connection, you must create a static NAT map route that maps hello external interface on hello BGPNAT virtual machine toohello VIP of hello Edge Gateway Pool.</span></span> <span data-ttu-id="b3879-321">VPN 連線中的每個連接埠都必須要有一個靜態 NAT 對應路由。</span><span class="sxs-lookup"><span data-stu-id="b3879-321">A static NAT map route is required for each port in a VPN connection.</span></span>

> [!NOTE]
> <span data-ttu-id="b3879-322">只有「Azure Stack 開發套件」環境才需要此組態。</span><span class="sxs-lookup"><span data-stu-id="b3879-322">This configuration is required for Azure Stack Development Kit environments only.</span></span>
> 
> 

### <a name="configure-hello-nat"></a><span data-ttu-id="b3879-323">設定 NAT hello</span><span class="sxs-lookup"><span data-stu-id="b3879-323">Configure hello NAT</span></span>
> [!IMPORTANT]
> <span data-ttu-id="b3879-324">您必須為兩個「Azure Stack 開發套件」環境都完成此程序。</span><span class="sxs-lookup"><span data-stu-id="b3879-324">You must complete this procedure for *both* Azure Stack Development Kit environments.</span></span>

1. <span data-ttu-id="b3879-325">判斷 hello**內部 IP 位址**toouse hello 下列 PowerShell 指令碼中的。</span><span class="sxs-lookup"><span data-stu-id="b3879-325">Determine hello **Internal IP address** toouse in hello following PowerShell script.</span></span> <span data-ttu-id="b3879-326">開啟 hello 虛擬網路閘道 （GW1 和 GW2），然後在 hello**概觀**刀鋒視窗中的，儲存 hello hello 值**公用 IP 位址**供日後使用。</span><span class="sxs-lookup"><span data-stu-id="b3879-326">Open hello virtual network gateway (GW1 and GW2), and then on hello **Overview** blade, save hello value for hello **Public IP address** for later use.</span></span>
<span data-ttu-id="b3879-327">![內部 IP 位址](media/azure-stack-create-vpn-connection-one-node-tp2/InternalIP.PNG)</span><span class="sxs-lookup"><span data-stu-id="b3879-327">![Internal IP address](media/azure-stack-create-vpn-connection-one-node-tp2/InternalIP.PNG)</span></span>
2. <span data-ttu-id="b3879-328">登入 toohello Azure 堆疊實體機器 POC1。</span><span class="sxs-lookup"><span data-stu-id="b3879-328">Sign in toohello Azure Stack physical machine for POC1.</span></span>
3. <span data-ttu-id="b3879-329">複製並編輯 hello 下列 PowerShell 指令碼。</span><span class="sxs-lookup"><span data-stu-id="b3879-329">Copy and edit hello following PowerShell script.</span></span> <span data-ttu-id="b3879-330">tooconfigure hello NAT 上每個 Azure 堆疊開發套件，在提升權限的 Windows PowerShell ISE 中執行 hello 指令碼。</span><span class="sxs-lookup"><span data-stu-id="b3879-330">tooconfigure hello NAT on each Azure Stack Development Kit, run hello script in an elevated Windows PowerShell ISE.</span></span> <span data-ttu-id="b3879-331">Hello 的指令碼中加入值 toohello*外部 BGPNAT 位址*和*內部 IP 位址*預留位置：</span><span class="sxs-lookup"><span data-stu-id="b3879-331">In hello script, add values toohello *External BGPNAT address* and *Internal IP address* placeholders:</span></span>

   ```powershell
   # Designate hello external NAT address for hello ports that use hello IKE authentication.
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
   # create a static NAT mapping toomap hello external address toohello Gateway
   # Public IP Address toomap hello ISAKMP port 500 for PHASE 1 of hello IPSEC tunnel
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
   # successfully establish hello complete IPSEC tunnel over NAT devices
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

4. <span data-ttu-id="b3879-332">在 POC2 上重複執行此程序。</span><span class="sxs-lookup"><span data-stu-id="b3879-332">Repeat this procedure on POC2.</span></span>

## <a name="test-hello-connection"></a><span data-ttu-id="b3879-333">測試 hello 連接</span><span class="sxs-lookup"><span data-stu-id="b3879-333">Test hello connection</span></span>
<span data-ttu-id="b3879-334">現在，建立 hello 站對站連線時，您應該驗證，就可以透過它流動的流量。</span><span class="sxs-lookup"><span data-stu-id="b3879-334">Now that hello site-to-site connection is established, you should validate that you can get traffic flowing through it.</span></span> <span data-ttu-id="b3879-335">toovalidate，登入 tooone hello 您在其中一個 Azure 堆疊開發套件的環境中建立的虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="b3879-335">toovalidate, sign in tooone of hello virtual machines that you created in either Azure Stack Development Kit environment.</span></span> <span data-ttu-id="b3879-336">然後，ping hello 虛擬機器，您在建立 hello 其他環境。</span><span class="sxs-lookup"><span data-stu-id="b3879-336">Then, ping hello virtual machine that you created in hello other environment.</span></span> 

<span data-ttu-id="b3879-337">tooensure 您傳送嗨流量透過 hello 站對站連線，請確定您 ping hello hello hello 遠端子網路，不 hello VIP 上的虛擬機器的直接 IP (DIP) 位址。</span><span class="sxs-lookup"><span data-stu-id="b3879-337">tooensure that you send hello traffic through hello site-to-site connection, ensure that you ping hello Direct IP (DIP) address of hello virtual machine on hello remote subnet, not hello VIP.</span></span> <span data-ttu-id="b3879-338">在此尋找 hello DIP 位址的 toodo hello hello 連線的另一端。</span><span class="sxs-lookup"><span data-stu-id="b3879-338">toodo this, find hello DIP address on hello other end of hello connection.</span></span> <span data-ttu-id="b3879-339">儲存供稍後使用 hello 位址。</span><span class="sxs-lookup"><span data-stu-id="b3879-339">Save hello address for later use.</span></span>

### <a name="sign-in-toohello-tenant-vm-in-poc1"></a><span data-ttu-id="b3879-340">租用戶登入 toohello POC1 中的 VM</span><span class="sxs-lookup"><span data-stu-id="b3879-340">Sign in toohello tenant VM in POC1</span></span>
1. <span data-ttu-id="b3879-341">登入 toohello Azure 堆疊實體機器 POC1，，然後使用租用戶帳戶 toosign toohello 使用者入口網站中。</span><span class="sxs-lookup"><span data-stu-id="b3879-341">Sign in toohello Azure Stack physical machine for POC1, and then use a tenant account toosign in toohello user portal.</span></span>
2. <span data-ttu-id="b3879-342">在 hello 左的導覽列中，選取 **計算**。</span><span class="sxs-lookup"><span data-stu-id="b3879-342">In hello left navigation bar, select **Compute**.</span></span>
3. <span data-ttu-id="b3879-343">在 [hello] 清單中的 Vm，尋找**VM01**您先前建立並加以選取。</span><span class="sxs-lookup"><span data-stu-id="b3879-343">In hello list of VMs, find **VM01** that you created previously, and then select it.</span></span>
4. <span data-ttu-id="b3879-344">在 hello 刀鋒視窗中的 hello 虛擬機器，按一下 **連接**，然後開啟 hello VM01.rdp 檔案。</span><span class="sxs-lookup"><span data-stu-id="b3879-344">On hello blade for hello virtual machine, click **Connect**, and then open hello VM01.rdp file.</span></span>
   
     ![[連線] 按鈕](media/azure-stack-create-vpn-connection-one-node-tp2/image17.png)
5. <span data-ttu-id="b3879-346">使用建立 hello 虛擬機器時所設定的 hello 帳戶登入。</span><span class="sxs-lookup"><span data-stu-id="b3879-346">Sign in with hello account that you configured when you created hello virtual machine.</span></span>
6. <span data-ttu-id="b3879-347">開啟已提高權限的 [Windows PowerShell] 視窗。</span><span class="sxs-lookup"><span data-stu-id="b3879-347">Open an elevated **Windows PowerShell** window.</span></span>
7. <span data-ttu-id="b3879-348">輸入 **ipconfig /all**。</span><span class="sxs-lookup"><span data-stu-id="b3879-348">Enter **ipconfig /all**.</span></span>
8. <span data-ttu-id="b3879-349">Hello 輸出中尋找 hello **IPv4 位址**，然後儲存供稍後使用 hello 位址。</span><span class="sxs-lookup"><span data-stu-id="b3879-349">In hello output, find hello **IPv4 Address**, and then save hello address for later use.</span></span> <span data-ttu-id="b3879-350">這是您將 ping 從 POC2 的 hello 位址。</span><span class="sxs-lookup"><span data-stu-id="b3879-350">This is hello address that you will ping from POC2.</span></span> <span data-ttu-id="b3879-351">在 hello 範例環境，位址是**10.0.10.4**，但您的環境中可能會不同。</span><span class="sxs-lookup"><span data-stu-id="b3879-351">In hello example environment, the address is **10.0.10.4**, but in your environment it might be different.</span></span> <span data-ttu-id="b3879-352">它應該會落在 hello **10.0.10.0/24**您先前建立的子網路。</span><span class="sxs-lookup"><span data-stu-id="b3879-352">It should fall within hello **10.0.10.0/24** subnet that you created previously.</span></span>
9. <span data-ttu-id="b3879-353">toocreate 允許 hello 虛擬機器 toorespond toopings，執行下列 PowerShell 命令的 hello 的防火牆規則：</span><span class="sxs-lookup"><span data-stu-id="b3879-353">toocreate a firewall rule that allows hello virtual machine toorespond toopings, run hello following PowerShell command:</span></span>

   ```powershell
   New-NetFirewallRule `
    –DisplayName “Allow ICMPv4-In” `
    –Protocol ICMPv4
   ```

### <a name="sign-in-toohello-tenant-vm-in-poc2"></a><span data-ttu-id="b3879-354">租用戶登入 toohello POC2 中的 VM</span><span class="sxs-lookup"><span data-stu-id="b3879-354">Sign in toohello tenant VM in POC2</span></span>
1. <span data-ttu-id="b3879-355">登入 toohello Azure 堆疊實體機器 POC2，，然後使用租用戶帳戶 toosign toohello 使用者入口網站中。</span><span class="sxs-lookup"><span data-stu-id="b3879-355">Sign in toohello Azure Stack physical machine for POC2, and then use a tenant account toosign in toohello user portal.</span></span>
2. <span data-ttu-id="b3879-356">在 hello 左的導覽列中，按一下 **計算**。</span><span class="sxs-lookup"><span data-stu-id="b3879-356">In hello left navigation bar, click **Compute**.</span></span>
3. <span data-ttu-id="b3879-357">從虛擬機器的 hello 清單，尋找**VM02**您先前建立並加以選取。</span><span class="sxs-lookup"><span data-stu-id="b3879-357">From hello list of virtual machines, find **VM02** that you created previously, and then select it.</span></span>
4. <span data-ttu-id="b3879-358">在 hello 刀鋒視窗中的 hello 虛擬機器，按一下 **連接**。</span><span class="sxs-lookup"><span data-stu-id="b3879-358">On hello blade for hello virtual machine, click **Connect**.</span></span>
5. <span data-ttu-id="b3879-359">使用建立 hello 虛擬機器時所設定的 hello 帳戶登入。</span><span class="sxs-lookup"><span data-stu-id="b3879-359">Sign in with hello account that you configured when you created hello virtual machine.</span></span>
6. <span data-ttu-id="b3879-360">開啟已提高權限的 [Windows PowerShell] 視窗。</span><span class="sxs-lookup"><span data-stu-id="b3879-360">Open an elevated **Windows PowerShell** window.</span></span>
7. <span data-ttu-id="b3879-361">輸入 **ipconfig /all**。</span><span class="sxs-lookup"><span data-stu-id="b3879-361">Enter **ipconfig /all**.</span></span>
8. <span data-ttu-id="b3879-362">您應該會看到落在 **10.0.20.0/24** 內的 IPv4 位址。</span><span class="sxs-lookup"><span data-stu-id="b3879-362">You should see an IPv4 address that falls within **10.0.20.0/24**.</span></span> <span data-ttu-id="b3879-363">Hello 範例環境中，在 hello 位址是**10.0.20.4**，但您的地址可能會不同。</span><span class="sxs-lookup"><span data-stu-id="b3879-363">In hello example environment, hello address is **10.0.20.4**, but your address might be different.</span></span>
9. <span data-ttu-id="b3879-364">toocreate 允許 hello 虛擬機器 toorespond toopings，執行下列 PowerShell 命令的 hello 的防火牆規則：</span><span class="sxs-lookup"><span data-stu-id="b3879-364">toocreate a firewall rule that allows hello virtual machine toorespond toopings, run hello following PowerShell command:</span></span>

   ```powershell
   New-NetFirewallRule `
    –DisplayName “Allow ICMPv4-In” `
    –Protocol ICMPv4
   ```

10. <span data-ttu-id="b3879-365">從 hello POC2 上的虛擬機器，ping hello 虛擬機器上 POC1，透過 hello 通道。</span><span class="sxs-lookup"><span data-stu-id="b3879-365">From hello virtual machine on POC2, ping hello virtual machine on POC1, through hello tunnel.</span></span> <span data-ttu-id="b3879-366">toodo，ping hello 您記錄從 VM01 的 DIP。</span><span class="sxs-lookup"><span data-stu-id="b3879-366">toodo this, you ping hello DIP that you recorded from VM01.</span></span>
   <span data-ttu-id="b3879-367">在 hello 範例環境，這是**10.0.10.4**，但會確定您記下您的實驗室中的 tooping hello 地址。</span><span class="sxs-lookup"><span data-stu-id="b3879-367">In hello example environment, this is **10.0.10.4**, but be sure tooping hello address you noted in your lab.</span></span> <span data-ttu-id="b3879-368">您應該會看到類似下列的 hello 的結果：</span><span class="sxs-lookup"><span data-stu-id="b3879-368">You should see a result that looks like hello following:</span></span>
   
    ![成功的 Ping](media/azure-stack-create-vpn-connection-one-node-tp2/image19b.png)
11. <span data-ttu-id="b3879-370">Hello 遠端虛擬機器的回覆指出測試成功 ！</span><span class="sxs-lookup"><span data-stu-id="b3879-370">A reply from hello remote virtual machine indicates a successful test!</span></span> <span data-ttu-id="b3879-371">您可以關閉 hello 虛擬機器視窗。</span><span class="sxs-lookup"><span data-stu-id="b3879-371">You can close hello virtual machine window.</span></span> <span data-ttu-id="b3879-372">tootest 您的連線，您可以嘗試其他種類的檔案複本的資料傳輸。</span><span class="sxs-lookup"><span data-stu-id="b3879-372">tootest your connection, you can try other kinds of data transfers like a file copy.</span></span>

### <a name="viewing-data-transfer-statistics-through-hello-gateway-connection"></a><span data-ttu-id="b3879-373">檢視資料傳輸的統計資料進行 hello 閘道連線</span><span class="sxs-lookup"><span data-stu-id="b3879-373">Viewing data transfer statistics through hello gateway connection</span></span>
<span data-ttu-id="b3879-374">如果您想的 tooknow 多少資料通過站對站連線，這項資訊位於 hello**連接**刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="b3879-374">If you want tooknow how much data passes through your site-to-site connection, this information is available on hello **Connection** blade.</span></span> <span data-ttu-id="b3879-375">這項測試也是另一個 hello 剛傳送的 ping 的 tooverify 實際上八月份 hello VPN 連線的方式。</span><span class="sxs-lookup"><span data-stu-id="b3879-375">This test is also another way tooverify that hello ping you just sent actually went through hello VPN connection.</span></span>

1. <span data-ttu-id="b3879-376">您已登入中 POC2 toohello 租用戶虛擬機器，而使用您的租用戶帳戶 toosign toothe 使用者入口網站中。</span><span class="sxs-lookup"><span data-stu-id="b3879-376">While you're signed in toohello tenant virtual machine in POC2, use your tenant account toosign in toothe user portal.</span></span>
2. <span data-ttu-id="b3879-377">跳過**所有資源**，然後選取 hello **POC2 POC1**連線。</span><span class="sxs-lookup"><span data-stu-id="b3879-377">Go too**All resources**, and then select hello **POC2-POC1** connection.</span></span> <span data-ttu-id="b3879-378">[連線] 隨即顯示。</span><span class="sxs-lookup"><span data-stu-id="b3879-378">**Connections** appears.</span></span>
4. <span data-ttu-id="b3879-379">在 hello**連接**刀鋒視窗，hello 的統計資料**中的資料**和**資料輸出**出現。</span><span class="sxs-lookup"><span data-stu-id="b3879-379">On hello **Connection** blade, hello statistics for **Data in** and **Data out** appear.</span></span> <span data-ttu-id="b3879-380">在下列螢幕擷取畫面的 hello，hello 大量的屬性會設定 tooadditional 檔案傳輸。</span><span class="sxs-lookup"><span data-stu-id="b3879-380">In hello following screenshot, hello large numbers are attributed tooadditional file transfer.</span></span> <span data-ttu-id="b3879-381">您應該會在該處看到一些非零的值。</span><span class="sxs-lookup"><span data-stu-id="b3879-381">You should see some nonzero values there.</span></span>
   
    ![資料輸入和輸出](media/azure-stack-create-vpn-connection-one-node-tp2/image20.png)
