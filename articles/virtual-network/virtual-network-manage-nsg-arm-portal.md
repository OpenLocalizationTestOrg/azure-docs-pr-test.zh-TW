---
title: "使用 Azure 入口網站 hello aaaManage Nsg |Microsoft 文件"
description: "深入了解如何 toomanage 現有 Nsg 使用 hello Azure 入口網站。"
services: virtual-network
documentationcenter: na
author: jimdial
manager: carmonm
editor: 
tags: azure-resource-manager
ms.assetid: 5d55679d-57da-457c-97dc-1e1973909ee5
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/14/2016
ms.author: jdial
ms.openlocfilehash: ad9a4060bd81bae4597ad5a4f59622e10cd214cf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="manage-nsgs-using-hello-portal"></a><span data-ttu-id="9bff6-103">管理 Nsg 使用 hello 入口網站</span><span class="sxs-lookup"><span data-stu-id="9bff6-103">Manage NSGs using hello portal</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="9bff6-104">入口網站</span><span class="sxs-lookup"><span data-stu-id="9bff6-104">Portal</span></span>](virtual-network-manage-nsg-arm-portal.md)
> * [<span data-ttu-id="9bff6-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="9bff6-105">PowerShell</span></span>](virtual-network-manage-nsg-arm-ps.md)
> * [<span data-ttu-id="9bff6-106">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="9bff6-106">Azure CLI</span></span>](virtual-network-manage-nsg-arm-cli.md)
>

[!INCLUDE [virtual-network-manage-nsg-intro-include.md](../../includes/virtual-network-manage-nsg-intro-include.md)]

> [!NOTE]
> <span data-ttu-id="9bff6-107">Azure 建立和處理資源的部署模型有二種：[Resource Manager 和傳統](../resource-manager-deployment-model.md)。</span><span class="sxs-lookup"><span data-stu-id="9bff6-107">Azure has two different deployment models for creating and working with resources:  [Resource Manager and classic](../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="9bff6-108">本文說明如何使用 hello Resource Manager 部署模型，Microsoft 建議您針對大部分新的部署，而不是 hello 傳統部署模型。</span><span class="sxs-lookup"><span data-stu-id="9bff6-108">This article covers using hello Resource Manager deployment model, which Microsoft recommends for most new deployments instead of hello classic deployment model.</span></span>
>

[!INCLUDE [virtual-network-manage-nsg-arm-scenario-include.md](../../includes/virtual-network-manage-nsg-arm-scenario-include.md)]

## <a name="retrieve-information"></a><span data-ttu-id="9bff6-109">擷取資訊</span><span class="sxs-lookup"><span data-stu-id="9bff6-109">Retrieve Information</span></span>
<span data-ttu-id="9bff6-110">您可以檢視您現有的 NSG、擷取現有 NSG 的規則，並找出與 NSG 相關聯的資源。</span><span class="sxs-lookup"><span data-stu-id="9bff6-110">You can view your existing NSGs, retrieve rules for an existing NSG, and find out what resources an NSG is associated to.</span></span>

### <a name="view-existing-nsgs"></a><span data-ttu-id="9bff6-111">檢視現有的 NSG</span><span class="sxs-lookup"><span data-stu-id="9bff6-111">View existing NSGs</span></span>

<span data-ttu-id="9bff6-112">tooview 所有現有 Nsg 中的訂閱，完成下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="9bff6-112">tooview all existing NSGs in a subscription, complete hello following steps:</span></span>

1. <span data-ttu-id="9bff6-113">從瀏覽器，瀏覽 toohttp://portal.azure.com，並視需要登入您的 Azure 帳戶。</span><span class="sxs-lookup"><span data-stu-id="9bff6-113">From a browser, navigate toohttp://portal.azure.com and, if necessary, sign in with your Azure account.</span></span>

2. <span data-ttu-id="9bff6-114">按一下 [瀏覽] >  > [網路安全性群組]。</span><span class="sxs-lookup"><span data-stu-id="9bff6-114">Click **Browse >** > **Network security groups**.</span></span>

    ![Azure 入口網站 - NSG](./media/virtual-network-manage-nsg-arm-portal/figure1.png)

3. <span data-ttu-id="9bff6-116">請檢查在 hello Nsg hello 清單**網路安全性群組**刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="9bff6-116">Check hello list of NSGs in hello **Network security groups** blade.</span></span>

    ![Azure 入口網站 - NSG](./media/virtual-network-manage-nsg-arm-portal/figure2.png)

### <a name="view-nsgs-in-a-resource-group"></a><span data-ttu-id="9bff6-118">檢視資源群組中的 NSG</span><span class="sxs-lookup"><span data-stu-id="9bff6-118">View NSGs in a resource group</span></span>

<span data-ttu-id="9bff6-119">tooview hello Nsg 中的清單 hello **RG NSG**資源群組中，完成下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="9bff6-119">tooview hello list of NSGs in hello **RG-NSG** resource group, complete hello following steps:</span></span>

1. <span data-ttu-id="9bff6-120">按一下 [資源群組] > **RG-NSG** > **...**。</span><span class="sxs-lookup"><span data-stu-id="9bff6-120">Click **Resource groups >** > **RG-NSG** > **...**.</span></span>

    ![Azure 入口網站 - NSG](./media/virtual-network-manage-nsg-arm-portal/figure3.png)

2. <span data-ttu-id="9bff6-122">在 [hello] 清單中的資源，尋找項目顯示 hello NSG 圖示，hello 中所示**資源**刀鋒視窗的下方。</span><span class="sxs-lookup"><span data-stu-id="9bff6-122">In hello list of resources, look for items displaying hello NSG icon, as shown in hello **Resources** blade below.</span></span>

    ![Azure 入口網站 - NSG](./media/virtual-network-manage-nsg-arm-portal/figure4.png)

### <a name="list-all-rules-for-an-nsg"></a><span data-ttu-id="9bff6-124">列出 NSG 的所有規則</span><span class="sxs-lookup"><span data-stu-id="9bff6-124">List all rules for an NSG</span></span>

<span data-ttu-id="9bff6-125">名為 NSG tooview hello 規則**NSG 前端**完整 hello 下列步驟：</span><span class="sxs-lookup"><span data-stu-id="9bff6-125">tooview hello rules of an NSG named **NSG-FrontEnd**, complete hello following steps:</span></span>

1. <span data-ttu-id="9bff6-126">從 hello**網路安全性群組**刀鋒視窗中或使用 hello**資源**按一下刀鋒視窗中，如上所示**NSG 前端**。</span><span class="sxs-lookup"><span data-stu-id="9bff6-126">From hello **Network security groups** blade, or hello **Resources** blade shown above, click **NSG-FrontEnd**.</span></span>

2. <span data-ttu-id="9bff6-127">在 hello**設定**索引標籤上，按一下 **輸入安全性規則**。</span><span class="sxs-lookup"><span data-stu-id="9bff6-127">In hello **Settings** tab, click **Inbound security rules**.</span></span>

    ![Azure 入口網站 - NSG](./media/virtual-network-manage-nsg-arm-portal/figure5.png)

3. <span data-ttu-id="9bff6-129">hello**輸入安全性規則**刀鋒視窗會顯示如下所示。</span><span class="sxs-lookup"><span data-stu-id="9bff6-129">hello **Inbound security rules** blade is displayed as shown below.</span></span>

    ![Azure 入口網站 - NSG](./media/virtual-network-manage-nsg-arm-portal/figure6.png)

4. <span data-ttu-id="9bff6-131">在 hello**設定**索引標籤上，按一下 **連出安全性規則**toosee hello 輸出規則。</span><span class="sxs-lookup"><span data-stu-id="9bff6-131">In hello **Settings** tab, click **Outbound security rules** toosee hello outbound rules.</span></span>

    > [!NOTE]
    > <span data-ttu-id="9bff6-132">tooview 預設規則，按一下 hello**預設規則**在 hello 顯示 hello 規則的 hello 刀鋒視窗最上方的圖示。</span><span class="sxs-lookup"><span data-stu-id="9bff6-132">tooview default rules, click hello **Default rules** icon at hello top of hello blade that displays hello rules.</span></span>
    >

### <a name="view-nsgs-associations"></a><span data-ttu-id="9bff6-133">檢視 NSG 關聯</span><span class="sxs-lookup"><span data-stu-id="9bff6-133">View NSGs associations</span></span>

<span data-ttu-id="9bff6-134">tooview 哪些資源 hello **NSG 前端**NSG 是關聯、 完整 hello 下列步驟：</span><span class="sxs-lookup"><span data-stu-id="9bff6-134">tooview what resources hello **NSG-FrontEnd** NSG is associate with, complete hello following steps:</span></span>

1. <span data-ttu-id="9bff6-135">從 hello**網路安全性群組**刀鋒視窗中或使用 hello**資源**按一下刀鋒視窗中，如上所示**NSG 前端**。</span><span class="sxs-lookup"><span data-stu-id="9bff6-135">From hello **Network security groups** blade, or hello **Resources** blade shown above, click **NSG-FrontEnd**.</span></span>

2. <span data-ttu-id="9bff6-136">在 hello**設定**索引標籤上，按一下 **子網路**tooview 哪個子網路相關聯 toohello NSG。</span><span class="sxs-lookup"><span data-stu-id="9bff6-136">In hello **Settings** tab, click **Subnets** tooview what subnets are associated toohello NSG.</span></span>

    ![Azure 入口網站 - NSG](./media/virtual-network-manage-nsg-arm-portal/figure7.png)

3. <span data-ttu-id="9bff6-138">在 hello**設定**索引標籤上，按一下 **網路介面**tooview 什麼 Nic 相關聯 toohello NSG。</span><span class="sxs-lookup"><span data-stu-id="9bff6-138">In hello **Settings** tab, click **Network interfaces** tooview what NICs are associated toohello NSG.</span></span>

## <a name="manage-rules"></a><span data-ttu-id="9bff6-139">管理規則</span><span class="sxs-lookup"><span data-stu-id="9bff6-139">Manage rules</span></span>
<span data-ttu-id="9bff6-140">您可以加入現有的 NSG 規則 tooan、 編輯現有的規則和移除規則。</span><span class="sxs-lookup"><span data-stu-id="9bff6-140">You can add rules tooan existing NSG, edit existing rules, and remove rules.</span></span>

### <a name="add-a-rule"></a><span data-ttu-id="9bff6-141">新增規則</span><span class="sxs-lookup"><span data-stu-id="9bff6-141">Add a rule</span></span>
<span data-ttu-id="9bff6-142">規則，允許 tooadd**輸入**流量 tooport **443**從任何機器 toohello **NSG 前端**NSG，完成下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="9bff6-142">tooadd a rule allowing **inbound** traffic tooport **443** from any machine toohello **NSG-FrontEnd** NSG, complete hello following steps:</span></span>

1. <span data-ttu-id="9bff6-143">從 hello**網路安全性群組**刀鋒視窗中或使用 hello**資源**按一下刀鋒視窗中，如上所示**NSG 前端**。</span><span class="sxs-lookup"><span data-stu-id="9bff6-143">From hello **Network security groups** blade, or hello **Resources** blade shown above, click **NSG-FrontEnd**.</span></span>
2. <span data-ttu-id="9bff6-144">在 hello**設定**索引標籤上，按一下 **輸入安全性規則**。</span><span class="sxs-lookup"><span data-stu-id="9bff6-144">In hello **Settings** tab, click **Inbound security rules**.</span></span>
3. <span data-ttu-id="9bff6-145">在 hello**輸入安全性規則**刀鋒視窗中，按一下 **新增**。</span><span class="sxs-lookup"><span data-stu-id="9bff6-145">In hello **Inbound security rules** blade, click **Add**.</span></span> <span data-ttu-id="9bff6-146">然後，在 hello**新增連入的安全性規則**刀鋒視窗中，填入 hello 值，如下所示，然後按一下**確定**。</span><span class="sxs-lookup"><span data-stu-id="9bff6-146">Then, in hello **Add inbound security rule** blade, fill hello values as shown below, and then click **OK**.</span></span>

    ![Azure 入口網站 - NSG](./media/virtual-network-manage-nsg-arm-portal/figure8.png)

    <span data-ttu-id="9bff6-148">幾秒之後，請注意在 hello hello 新規則**輸入安全性規則**刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="9bff6-148">After a few seconds, notice hello new rule in hello **Inbound security rules** blade.</span></span>

    ![Azure 入口網站 - NSG](./media/virtual-network-manage-nsg-arm-portal/figure9.png)

### <a name="change-a-rule"></a><span data-ttu-id="9bff6-150">變更規則</span><span class="sxs-lookup"><span data-stu-id="9bff6-150">Change a rule</span></span>
<span data-ttu-id="9bff6-151">tooallow 上面所建立的 toochange hello 規則輸入流量從 hello**網際網路**唯一、 完整 hello 下列步驟：</span><span class="sxs-lookup"><span data-stu-id="9bff6-151">toochange hello rule created above tooallow inbound traffic from hello **Internet** only, complete hello following steps:</span></span>

1. <span data-ttu-id="9bff6-152">從 hello**網路安全性群組**刀鋒視窗中或使用 hello**資源**按一下刀鋒視窗中，如上所示**NSG 前端**。</span><span class="sxs-lookup"><span data-stu-id="9bff6-152">From hello **Network security groups** blade, or hello **Resources** blade shown above, click **NSG-FrontEnd**.</span></span>
2. <span data-ttu-id="9bff6-153">在 hello**設定**索引標籤上，按一下 hello 上面所建立的規則。</span><span class="sxs-lookup"><span data-stu-id="9bff6-153">In hello **Settings** tab, click hello rule created above.</span></span>
3. <span data-ttu-id="9bff6-154">在 hello**允許 https**刀鋒視窗中，變更 hello**來源**如下所示的屬性，然後按一下**儲存**。</span><span class="sxs-lookup"><span data-stu-id="9bff6-154">In hello **allow-https** blade, change hello **Source** property as shown below, and then click **Save**.</span></span>

    ![Azure 入口網站 - NSG](./media/virtual-network-manage-nsg-arm-portal/figure10.png)

### <a name="delete-a-rule"></a><span data-ttu-id="9bff6-156">刪除規則</span><span class="sxs-lookup"><span data-stu-id="9bff6-156">Delete a rule</span></span>

<span data-ttu-id="9bff6-157">toodelete hello 規則建立上述的完整 hello 下列步驟：</span><span class="sxs-lookup"><span data-stu-id="9bff6-157">toodelete hello rule created above, complete hello following steps:</span></span>

1. <span data-ttu-id="9bff6-158">從 hello**網路安全性群組**刀鋒視窗中或使用 hello**資源**按一下刀鋒視窗中，如上所示**NSG 前端**。</span><span class="sxs-lookup"><span data-stu-id="9bff6-158">From hello **Network security groups** blade, or hello **Resources** blade shown above, click **NSG-FrontEnd**.</span></span>
2. <span data-ttu-id="9bff6-159">在 hello**設定**索引標籤上，按一下 hello 上面所建立的規則。</span><span class="sxs-lookup"><span data-stu-id="9bff6-159">In hello **Settings** tab, click hello rule created above.</span></span>
3. <span data-ttu-id="9bff6-160">在 hello**允許 https**刀鋒視窗中，按一下**刪除**，然後按一下**是**。</span><span class="sxs-lookup"><span data-stu-id="9bff6-160">In hello **allow-https** blade, click **Delete**, and then click **Yes**.</span></span>

    ![Azure 入口網站 - NSG](./media/virtual-network-manage-nsg-arm-portal/figure11.png)

## <a name="manage-associations"></a><span data-ttu-id="9bff6-162">管理關聯</span><span class="sxs-lookup"><span data-stu-id="9bff6-162">Manage associations</span></span>
<span data-ttu-id="9bff6-163">您可以將關聯 NSG toosubnets 和 Nic。</span><span class="sxs-lookup"><span data-stu-id="9bff6-163">You can associate an NSG toosubnets and NICs.</span></span> <span data-ttu-id="9bff6-164">您也可以中斷 NSG 與其相關聯的任何資源的關聯。</span><span class="sxs-lookup"><span data-stu-id="9bff6-164">You can also dissociate an NSG from any resource it's associated to.</span></span>

### <a name="associate-an-nsg-tooa-nic"></a><span data-ttu-id="9bff6-165">關聯 NSG tooa NIC</span><span class="sxs-lookup"><span data-stu-id="9bff6-165">Associate an NSG tooa NIC</span></span>
<span data-ttu-id="9bff6-166">tooassociate hello **NSG 前端**NSG toohello **TestNICWeb1** NIC，完成下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="9bff6-166">tooassociate hello **NSG-FrontEnd** NSG toohello **TestNICWeb1** NIC, complete hello following steps:</span></span>

1. <span data-ttu-id="9bff6-167">從 hello**網路安全性群組**刀鋒視窗中或使用 hello**資源**按一下刀鋒視窗中，如上所示**NSG 前端**。</span><span class="sxs-lookup"><span data-stu-id="9bff6-167">From hello **Network security groups** blade, or hello **Resources** blade shown above, click **NSG-FrontEnd**.</span></span>
2. <span data-ttu-id="9bff6-168">在 hello**設定**索引標籤上，按一下 **網路介面** > **關聯** > **TestNICWeb1**。</span><span class="sxs-lookup"><span data-stu-id="9bff6-168">In hello **Settings** tab, click **Network interfaces** > **Associate** > **TestNICWeb1**.</span></span>

    ![Azure 入口網站 - NSG](./media/virtual-network-manage-nsg-arm-portal/figure12.png)

### <a name="dissociate-an-nsg-from-a-nic"></a><span data-ttu-id="9bff6-170">中斷 NSG 與 NIC 的關聯</span><span class="sxs-lookup"><span data-stu-id="9bff6-170">Dissociate an NSG from a NIC</span></span>

<span data-ttu-id="9bff6-171">toodissociate hello **NSG 前端**hello 從 NSG **TestNICWeb1** NIC，完成下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="9bff6-171">toodissociate hello **NSG-FrontEnd** NSG from hello **TestNICWeb1** NIC, complete hello following steps:</span></span>

1. <span data-ttu-id="9bff6-172">從 hello Azure 入口網站，按一下 **資源群組 >** > **RG NSG** > **...**  >  **TestNICWeb1**。</span><span class="sxs-lookup"><span data-stu-id="9bff6-172">From hello Azure portal, click **Resource groups >** > **RG-NSG** > **...** > **TestNICWeb1**.</span></span>

2. <span data-ttu-id="9bff6-173">在 hello **TestNICWeb1**刀鋒視窗中，按一下 **變更安全性...**  > **無**。</span><span class="sxs-lookup"><span data-stu-id="9bff6-173">In hello **TestNICWeb1** blade, click **Change security...** > **None**.</span></span>

    ![Azure 入口網站 - NSG](./media/virtual-network-manage-nsg-arm-portal/figure13.png)

> [!NOTE]
> <span data-ttu-id="9bff6-175">您也可以使用現有的 NSG 此刀鋒視窗 tooassociate hello NIC tooany。</span><span class="sxs-lookup"><span data-stu-id="9bff6-175">You can also use this blade tooassociate hello NIC tooany existing NSG.</span></span>
>

### <a name="dissociate-an-nsg-from-a-subnet"></a><span data-ttu-id="9bff6-176">中斷 NSG 與子網路的關聯</span><span class="sxs-lookup"><span data-stu-id="9bff6-176">Dissociate an NSG from a subnet</span></span>

<span data-ttu-id="9bff6-177">toodissociate hello **NSG 前端**hello 從 NSG**前端**子網路、 完整 hello 下列步驟：</span><span class="sxs-lookup"><span data-stu-id="9bff6-177">toodissociate hello **NSG-FrontEnd** NSG from hello **FrontEnd** subnet, complete hello following steps:</span></span>

1. <span data-ttu-id="9bff6-178">從 hello Azure 入口網站，按一下 **資源群組 >** > **RG NSG** > **...**  >  **TestVNet**。</span><span class="sxs-lookup"><span data-stu-id="9bff6-178">From hello Azure portal, click **Resource groups >** > **RG-NSG** > **...** > **TestVNet**.</span></span>

2. <span data-ttu-id="9bff6-179">在 hello**設定**刀鋒視窗中，按一下 **子網路** > **前端** > **網路安全性群組** > **無**。</span><span class="sxs-lookup"><span data-stu-id="9bff6-179">In hello **Settings** blade, click **Subnets** > **FrontEnd** > **Network security group** > **None**.</span></span>

    ![Azure 入口網站 - NSG](./media/virtual-network-manage-nsg-arm-portal/figure14.png)

3. <span data-ttu-id="9bff6-181">在 hello**前端**刀鋒視窗中，按一下 **儲存**。</span><span class="sxs-lookup"><span data-stu-id="9bff6-181">In hello **FrontEnd** blade, click **Save**.</span></span>

    ![Azure 入口網站 - NSG](./media/virtual-network-manage-nsg-arm-portal/figure15.png)

### <a name="associate-an-nsg-tooa-subnet"></a><span data-ttu-id="9bff6-183">NSG tooa 子網路建立關聯</span><span class="sxs-lookup"><span data-stu-id="9bff6-183">Associate an NSG tooa subnet</span></span>

<span data-ttu-id="9bff6-184">tooassociate hello **NSG 前端**NSG toohello **FronEnd**一次的子網路，完成下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="9bff6-184">tooassociate hello **NSG-FrontEnd** NSG toohello **FronEnd** subnet again, complete hello following steps:</span></span>

1. <span data-ttu-id="9bff6-185">從 hello Azure 入口網站，按一下 **資源群組 >** > **RG NSG** > **...**  >  **TestVNet**。</span><span class="sxs-lookup"><span data-stu-id="9bff6-185">From hello Azure portal, click **Resource groups >** > **RG-NSG** > **...** > **TestVNet**.</span></span>
2. <span data-ttu-id="9bff6-186">在 hello**設定**刀鋒視窗中，按一下 **子網路** > **前端** > **網路安全性群組** > **NSG 前端**。</span><span class="sxs-lookup"><span data-stu-id="9bff6-186">In hello **Settings** blade, click **Subnets** > **FrontEnd** > **Network security group** > **NSG-FrontEnd**.</span></span>
3. <span data-ttu-id="9bff6-187">在 hello**前端**刀鋒視窗中，按一下 **儲存**。</span><span class="sxs-lookup"><span data-stu-id="9bff6-187">In hello **FrontEnd** blade, click **Save**.</span></span>

> [!NOTE]
> <span data-ttu-id="9bff6-188">您也可以將關聯 NSG tooa thh NSG 的子網路**設定**刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="9bff6-188">You can also associate an NSG tooa subnet from thh NSG's **Settings** blade.</span></span>
>

## <a name="delete-an-nsg"></a><span data-ttu-id="9bff6-189">刪除 NSG</span><span class="sxs-lookup"><span data-stu-id="9bff6-189">Delete an NSG</span></span>
<span data-ttu-id="9bff6-190">如果它不是相關聯 tooany 資源，您只能刪除 NSG。</span><span class="sxs-lookup"><span data-stu-id="9bff6-190">You can only delete an NSG if it's not associated tooany resource.</span></span> <span data-ttu-id="9bff6-191">toodelete NSG，完成下列步驟的 hello:。</span><span class="sxs-lookup"><span data-stu-id="9bff6-191">toodelete an NSG, complete hello following steps:.</span></span>

1. <span data-ttu-id="9bff6-192">從 hello Azure 入口網站，按一下 **資源群組 >** > **RG NSG** > **...**  >  **NSG 前端**。</span><span class="sxs-lookup"><span data-stu-id="9bff6-192">From hello Azure portal, click **Resource groups >** > **RG-NSG** > **...** > **NSG-FrontEnd**.</span></span>
2. <span data-ttu-id="9bff6-193">在 hello**設定**刀鋒視窗中，按一下 **網路介面**。</span><span class="sxs-lookup"><span data-stu-id="9bff6-193">In hello **Settings** blade, click **Network interfaces**.</span></span>
3. <span data-ttu-id="9bff6-194">如果沒有列出任何 Nic，按一下 hello NIC，並遵循步驟 2 中的[中斷 NIC 的 NSG 關聯](#Dissociate-an-NSG-from-a-NIC)。</span><span class="sxs-lookup"><span data-stu-id="9bff6-194">If there are any NICs listed, click hello NIC, and follow step 2 in [Dissociate an NSG from a NIC](#Dissociate-an-NSG-from-a-NIC).</span></span>
4. <span data-ttu-id="9bff6-195">針對每個 NIC 重複步驟 3。</span><span class="sxs-lookup"><span data-stu-id="9bff6-195">Repeat step 3 for each NIC.</span></span>
5. <span data-ttu-id="9bff6-196">在 hello**設定**刀鋒視窗中，按一下 **子網路**。</span><span class="sxs-lookup"><span data-stu-id="9bff6-196">In hello **Settings** blade, click **Subnets**.</span></span>
6. <span data-ttu-id="9bff6-197">如果沒有列出任何子網路，請按一下 hello 子網路，請依照下列步驟 2 和 3 中的[中斷關聯子網路的 NSG](#Dissociate-an-NSG-from-a-subnet)。</span><span class="sxs-lookup"><span data-stu-id="9bff6-197">If there are any subnets listed, click hello subnet and follow steps 2 and 3 in [Dissociate an NSG from a subnet](#Dissociate-an-NSG-from-a-subnet).</span></span>
7. <span data-ttu-id="9bff6-198">捲動左的 toohello **NSG 前端**刀鋒視窗中，然後按一下 **刪除** > **是**。</span><span class="sxs-lookup"><span data-stu-id="9bff6-198">Scrolls left toohello **NSG-FrontEnd** blade, then click **Delete** > **Yes**.</span></span>

    ![Azure 入口網站 - NSG](./media/virtual-network-manage-nsg-arm-portal/figure16.png)

## <a name="next-steps"></a><span data-ttu-id="9bff6-200">後續步驟</span><span class="sxs-lookup"><span data-stu-id="9bff6-200">Next steps</span></span>
* <span data-ttu-id="9bff6-201">[啟用 NSG 的記錄](virtual-network-nsg-manage-log.md) 。</span><span class="sxs-lookup"><span data-stu-id="9bff6-201">[Enable logging](virtual-network-nsg-manage-log.md) for NSGs.</span></span>
