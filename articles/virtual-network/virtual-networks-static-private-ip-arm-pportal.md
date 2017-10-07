---
title: "對於 Azure 入口網站的 Vm-aaaConfigure 私人 IP 位址 |Microsoft 文件"
description: "了解如何 tooconfigure 私人 IP 位址的虛擬機器使用 hello Azure 入口網站。"
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 11245645-357d-4358-9a14-dd78e367b494
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/04/2016
ms.author: jdial
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 474161303cdf8cb98e16ffd7cef6b74debdbc49a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="configure-private-ip-addresses-for-a-virtual-machine-using-hello-azure-portal"></a><span data-ttu-id="26020-103">設定使用 hello Azure 入口網站為虛擬機器的私人 IP 位址</span><span class="sxs-lookup"><span data-stu-id="26020-103">Configure private IP addresses for a virtual machine using hello Azure portal</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="26020-104">Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="26020-104">Azure portal</span></span>](virtual-networks-static-private-ip-arm-pportal.md)
> * [<span data-ttu-id="26020-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="26020-105">PowerShell</span></span>](virtual-networks-static-private-ip-arm-ps.md)
> * [<span data-ttu-id="26020-106">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="26020-106">Azure CLI</span></span>](virtual-networks-static-private-ip-arm-cli.md)
> * [<span data-ttu-id="26020-107">Azure 入口網站 (傳統)</span><span class="sxs-lookup"><span data-stu-id="26020-107">Azure portal (Classic)</span></span>](virtual-networks-static-private-ip-classic-pportal.md)
> * [<span data-ttu-id="26020-108">PowerShell (傳統)</span><span class="sxs-lookup"><span data-stu-id="26020-108">PowerShell (Classic)</span></span>](virtual-networks-static-private-ip-classic-ps.md)
> * [<span data-ttu-id="26020-109">Azure CLI (傳統)</span><span class="sxs-lookup"><span data-stu-id="26020-109">Azure CLI (Classic)</span></span>](virtual-networks-static-private-ip-classic-cli.md)


[!INCLUDE [virtual-networks-static-private-ip-intro-include](../../includes/virtual-networks-static-private-ip-intro-include.md)]

[!INCLUDE [azure-arm-classic-important-include](../../includes/azure-arm-classic-important-include.md)]

<span data-ttu-id="26020-110">本文涵蓋 hello Resource Manager 部署模型。</span><span class="sxs-lookup"><span data-stu-id="26020-110">This article covers hello Resource Manager deployment model.</span></span> <span data-ttu-id="26020-111">您也可以[管理 hello 傳統部署模型中的靜態私人 IP 位址](virtual-networks-static-private-ip-classic-pportal.md)。</span><span class="sxs-lookup"><span data-stu-id="26020-111">You can also [manage static private IP address in hello classic deployment model](virtual-networks-static-private-ip-classic-pportal.md).</span></span>

[!INCLUDE [virtual-networks-static-ip-scenario-include](../../includes/virtual-networks-static-ip-scenario-include.md)]

<span data-ttu-id="26020-112">下列的 hello 範例步驟預期簡單的環境中已經建立。</span><span class="sxs-lookup"><span data-stu-id="26020-112">hello sample steps below expect a simple environment already created.</span></span> <span data-ttu-id="26020-113">如果您想 toorun hello 步驟，因為它們會顯示在此文件，第一次建立 hello 測試環境中所述[建立 vnet](virtual-networks-create-vnet-arm-pportal.md)。</span><span class="sxs-lookup"><span data-stu-id="26020-113">If you want toorun hello steps as they are displayed in this document, first build hello test environment described in [create a vnet](virtual-networks-create-vnet-arm-pportal.md).</span></span>

## <a name="how-toocreate-a-vm-for-testing-static-private-ip-addresses"></a><span data-ttu-id="26020-114">如何 toocreate VM 進行測試靜態私人 IP 位址</span><span class="sxs-lookup"><span data-stu-id="26020-114">How toocreate a VM for testing static private IP addresses</span></span>
<span data-ttu-id="26020-115">您無法使用 hello Azure 入口網站，hello hello Resource Manager 部署模式中的 VM 建立期間設定靜態私人 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="26020-115">You cannot set a static private IP address during hello creation of a VM in hello Resource Manager deployment mode by using hello Azure portal.</span></span> <span data-ttu-id="26020-116">您必須先建立 hello VM，轉設定其私人 IP toobe 靜態。</span><span class="sxs-lookup"><span data-stu-id="26020-116">You must create hello VM first, tehn set its private IP toobe static.</span></span>

<span data-ttu-id="26020-117">名為的 VM toocreate *DNS01*在 hello*前端*名為 VNet 的子網路*TestVNet*，依照下列步驟執行 hello。</span><span class="sxs-lookup"><span data-stu-id="26020-117">toocreate a VM named *DNS01* in hello *FrontEnd* subnet of a VNet named *TestVNet*, follow hello steps below.</span></span>

1. <span data-ttu-id="26020-118">從瀏覽器，瀏覽 toohttp://portal.azure.com，並視需要登入您的 Azure 帳戶。</span><span class="sxs-lookup"><span data-stu-id="26020-118">From a browser, navigate toohttp://portal.azure.com and, if necessary, sign in with your Azure account.</span></span>
2. <span data-ttu-id="26020-119">按一下**新增** > **計算** > **Windows Server 2012 R2 Datacenter**，請注意該 hello**選取部署模型**清單已經顯示**資源管理員**，然後按一下**建立**、 hello 圖所示。</span><span class="sxs-lookup"><span data-stu-id="26020-119">Click **NEW** > **Compute** > **Windows Server 2012 R2 Datacenter**, notice that hello **Select a deployment model** list already shows **Resource Manager**, and then click **Create**, as seen in hello figure below.</span></span>
   
    ![在 Azure 入口網站中建立 VM](./media/virtual-networks-static-ip-arm-pportal/figure01.png)
3. <span data-ttu-id="26020-121">在 hello**基本概念**刀鋒視窗中，輸入 hello VM toobe 建立 hello 名稱 (*DNS01*在我們的案例)，hello 本機系統管理員帳戶和密碼，如 hello 圖所示。</span><span class="sxs-lookup"><span data-stu-id="26020-121">In hello **Basics** blade, enter hello name of hello VM toobe created (*DNS01* in our scenario), hello local administrator account, and password, as seen in hello figure below.</span></span>
   
    ![基本概念刀鋒視窗](./media/virtual-networks-static-ip-arm-pportal/figure02.png)
4. <span data-ttu-id="26020-123">請確定 hello**位置**選取*美國中部*，然後按一下**選取現有**下**資源群組**，然後按一下 **資源群組**一次，然後按一下 *TestRG*，然後按一下**確定**。</span><span class="sxs-lookup"><span data-stu-id="26020-123">Make sure hello **Location** selected is *Central US*, then click **Select existing** under **Resource group**, then click **Resource group** again, then click *TestRG*, and then click **OK**.</span></span>
   
    ![基本概念刀鋒視窗](./media/virtual-networks-static-ip-arm-pportal/figure03.png)
5. <span data-ttu-id="26020-125">在 hello**大小選擇 「**刀鋒視窗中，選取**標準 A1**，然後按一下**選取**。</span><span class="sxs-lookup"><span data-stu-id="26020-125">In hello **Choose a size** blade, select **A1 Standard**, and then click **Select**.</span></span>
   
    ![選擇尺寸刀鋒視窗](./media/virtual-networks-static-ip-arm-pportal/figure04.png)    
6. <span data-ttu-id="26020-127">在**設定**刀鋒視窗中，請確定 hello 下列屬性會設定下面的 hello 值設定，然後按一下**確定**。</span><span class="sxs-lookup"><span data-stu-id="26020-127">In teh **Settings** blade, make sure hello following properties are set are set with hello values below, and then click **OK**.</span></span>
   
    <span data-ttu-id="26020-128">-**儲存體帳戶**：vnetstorage</span><span class="sxs-lookup"><span data-stu-id="26020-128">-**Storage account**: *vnetstorage*</span></span>
   
   * <span data-ttu-id="26020-129">**網路**：TestVNet</span><span class="sxs-lookup"><span data-stu-id="26020-129">**Network**: *TestVNet*</span></span>
   * <span data-ttu-id="26020-130">**子網路**：FrontEnd</span><span class="sxs-lookup"><span data-stu-id="26020-130">**Subnet**: *FrontEnd*</span></span>
     
     ![選擇尺寸刀鋒視窗](./media/virtual-networks-static-ip-arm-pportal/figure05.png)     
7. <span data-ttu-id="26020-132">在 hello**摘要**刀鋒視窗中，按一下 **確定**。</span><span class="sxs-lookup"><span data-stu-id="26020-132">In hello **Summary** blade, click **OK**.</span></span> <span data-ttu-id="26020-133">請注意 hello 磚下方顯示在儀表板。</span><span class="sxs-lookup"><span data-stu-id="26020-133">Notice hello tile below displayed in your dashboard.</span></span>
   
    ![在 Azure 入口網站中建立 VM](./media/virtual-networks-static-ip-arm-pportal/figure06.png)

## <a name="how-tooretrieve-static-private-ip-address-information-for-a-vm"></a><span data-ttu-id="26020-135">如何 tooretrieve 靜態私人 IP 位址適用於 VM 的資訊</span><span class="sxs-lookup"><span data-stu-id="26020-135">How tooretrieve static private IP address information for a VM</span></span>
<span data-ttu-id="26020-136">tooview hello 靜態私人 IP 位址資訊 hello 與 hello 上述步驟，在建立 VM 執行下列步驟 hello。</span><span class="sxs-lookup"><span data-stu-id="26020-136">tooview hello static private IP address information for hello VM created with hello steps above, execute hello steps below.</span></span>

1. <span data-ttu-id="26020-137">從 hello Azure Azure 入口網站中，按一下 **瀏覽所有** > **虛擬機器** > **DNS01** > **所有設定** > **網路介面**，然後按一下hello 列出只有網路介面上。</span><span class="sxs-lookup"><span data-stu-id="26020-137">From hello Azure Azure portal, click **BROWSE ALL** > **Virtual machines** > **DNS01** > **All settings** > **Network interfaces** and then click on hello only network interface listed.</span></span>
   
    ![部署 VM 磚](./media/virtual-networks-static-ip-arm-pportal/figure07.png)
2. <span data-ttu-id="26020-139">在 hello**網路介面**刀鋒視窗中，按一下**所有設定** > **IP 位址**和注意事項 hello**指派**和**IP 位址**值。</span><span class="sxs-lookup"><span data-stu-id="26020-139">In hello **Network interface** blade, click **All settings** > **IP addresses** and notice hello **Assignment** and **IP address** values.</span></span>
   
    ![部署 VM 磚](./media/virtual-networks-static-ip-arm-pportal/figure08.png)

## <a name="how-tooadd-a-static-private-ip-address-tooan-existing-vm"></a><span data-ttu-id="26020-141">Tooadd 靜態私人 IP 定址 tooan 現有 VM 的方式</span><span class="sxs-lookup"><span data-stu-id="26020-141">How tooadd a static private IP address tooan existing VM</span></span>
<span data-ttu-id="26020-142">tooadd 靜態私人 IP 位址 toohello VM 建立使用 hello 上述步驟，請遵循下列 hello 步驟：</span><span class="sxs-lookup"><span data-stu-id="26020-142">tooadd a static private IP address toohello VM created using hello steps above, follow hello steps below:</span></span>

1. <span data-ttu-id="26020-143">從 hello **IP 位址**按一下刀鋒視窗中，如上所示**靜態**下**指派**。</span><span class="sxs-lookup"><span data-stu-id="26020-143">From hello **IP addresses** blade shown above, click **Static** under **Assignment**.</span></span>
2. <span data-ttu-id="26020-144">IP 位址 輸入 192.168.1.101，然後按一下儲存。</span><span class="sxs-lookup"><span data-stu-id="26020-144">Type *192.168.1.101* for **IP address**, and then click **Save**.</span></span>
   
    ![在 Azure 入口網站中建立 VM](./media/virtual-networks-static-ip-arm-pportal/figure09.png)

> [!NOTE]
> <span data-ttu-id="26020-146">如果按一下後的**儲存**您注意到 hello 分派仍然可以設定太**動態**，這表示您輸入的 hello IP 位址已在使用。</span><span class="sxs-lookup"><span data-stu-id="26020-146">If after clicking **Save** you notice that hello assignment is still set too**Dynamic**, it means that hello IP address you typed is already in use.</span></span> <span data-ttu-id="26020-147">請嘗試不同的 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="26020-147">Try a different IP address.</span></span>
> 
> 

## <a name="how-tooremove-a-static-private-ip-address-from-a-vm"></a><span data-ttu-id="26020-148">如何 tooremove 靜態私人 IP 位址從 VM</span><span class="sxs-lookup"><span data-stu-id="26020-148">How tooremove a static private IP address from a VM</span></span>
<span data-ttu-id="26020-149">tooremove hello 靜態私人 IP 位址從 VM 建立上述的 hello 完成下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="26020-149">tooremove hello static private IP address from hello VM created above, complete hello following step:</span></span>

<span data-ttu-id="26020-150">從 hello **IP 位址**按一下刀鋒視窗中，如上所示**動態**下**指派**，然後按一下**儲存**。</span><span class="sxs-lookup"><span data-stu-id="26020-150">From hello **IP addresses** blade shown above, click **Dynamic** under **Assignment**, and then click **Save**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="26020-151">後續步驟</span><span class="sxs-lookup"><span data-stu-id="26020-151">Next steps</span></span>
* <span data-ttu-id="26020-152">深入了解 [保留的公用 IP](virtual-networks-reserved-public-ip.md) 位址。</span><span class="sxs-lookup"><span data-stu-id="26020-152">Learn about [reserved public IP](virtual-networks-reserved-public-ip.md) addresses.</span></span>
* <span data-ttu-id="26020-153">深入了解 [執行個體層級公用 IP (ILPIP)](virtual-networks-instance-level-public-ip.md) 位址。</span><span class="sxs-lookup"><span data-stu-id="26020-153">Learn about [instance-level public IP (ILPIP)](virtual-networks-instance-level-public-ip.md) addresses.</span></span>
* <span data-ttu-id="26020-154">請參閱 hello[保留 IP REST Api](https://msdn.microsoft.com/library/azure/dn722420.aspx)。</span><span class="sxs-lookup"><span data-stu-id="26020-154">Consult hello [Reserved IP REST APIs](https://msdn.microsoft.com/library/azure/dn722420.aspx).</span></span>

