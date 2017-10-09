---
title: "aaaConfigure 私人 IP 位址的 Vm （傳統）-Azure 入口網站 |Microsoft 文件"
description: "了解如何 tooconfigure 私人 IP 位址的虛擬機器 （傳統） 使用 hello Azure 入口網站。"
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: b8ef8367-58b2-42df-9f26-3269980950b8
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/04/2016
ms.author: jdial
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: df4bfa6768fc9e66db89785b633ffdb0274dbc46
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="configure-private-ip-addresses-for-a-virtual-machine-classic-using-hello-azure-portal"></a><span data-ttu-id="9dbac-103">設定私人 IP 位址使用 hello Azure 入口網站為虛擬機器 （傳統）</span><span class="sxs-lookup"><span data-stu-id="9dbac-103">Configure private IP addresses for a virtual machine (Classic) using hello Azure portal</span></span>

[!INCLUDE [virtual-networks-static-private-ip-selectors-classic-include](../../includes/virtual-networks-static-private-ip-selectors-classic-include.md)]

[!INCLUDE [virtual-networks-static-private-ip-intro-include](../../includes/virtual-networks-static-private-ip-intro-include.md)]

[!INCLUDE [azure-arm-classic-important-include](../../includes/azure-arm-classic-important-include.md)]

<span data-ttu-id="9dbac-104">本文涵蓋 hello 傳統部署模型。</span><span class="sxs-lookup"><span data-stu-id="9dbac-104">This article covers hello classic deployment model.</span></span> <span data-ttu-id="9dbac-105">您也可以[管理 hello Resource Manager 部署模型中的靜態私人 IP 位址](virtual-networks-static-private-ip-arm-pportal.md)。</span><span class="sxs-lookup"><span data-stu-id="9dbac-105">You can also [manage a static private IP address in hello Resource Manager deployment model](virtual-networks-static-private-ip-arm-pportal.md).</span></span>

[!INCLUDE [virtual-networks-static-ip-scenario-include](../../includes/virtual-networks-static-ip-scenario-include.md)]

<span data-ttu-id="9dbac-106">下列的 hello 範例步驟預期簡單的環境中已經建立。</span><span class="sxs-lookup"><span data-stu-id="9dbac-106">hello sample steps below expect a simple environment already created.</span></span> <span data-ttu-id="9dbac-107">如果您想 toorun hello 步驟，因為它們會顯示在此文件，第一次建立 hello 測試環境中所述[建立 vnet](virtual-networks-create-vnet-classic-pportal.md)。</span><span class="sxs-lookup"><span data-stu-id="9dbac-107">If you want toorun hello steps as they are displayed in this document, first build hello test environment described in [create a vnet](virtual-networks-create-vnet-classic-pportal.md).</span></span>

## <a name="how-toospecify-a-static-private-ip-address-when-creating-a-vm"></a><span data-ttu-id="9dbac-108">如何 toospecify 靜態私人 IP 位址建立 VM 時</span><span class="sxs-lookup"><span data-stu-id="9dbac-108">How toospecify a static private IP address when creating a VM</span></span>
<span data-ttu-id="9dbac-109">名為的 VM toocreate *DNS01*在 hello*前端*名為 VNet 的子網路*TestVNet*以靜態私人 ip 位址的*192.168.1.101*，請遵循下列步驟執行 hello:</span><span class="sxs-lookup"><span data-stu-id="9dbac-109">toocreate a VM named *DNS01* in hello *FrontEnd* subnet of a VNet named *TestVNet* with a static private IP of *192.168.1.101*, follow hello steps below:</span></span>

1. <span data-ttu-id="9dbac-110">從瀏覽器，瀏覽 toohttp://portal.azure.com，並視需要登入您的 Azure 帳戶。</span><span class="sxs-lookup"><span data-stu-id="9dbac-110">From a browser, navigate toohttp://portal.azure.com and, if necessary, sign in with your Azure account.</span></span>
2. <span data-ttu-id="9dbac-111">按一下**新增** > **計算** > **Windows Server 2012 R2 Datacenter**，請注意該 hello**選取部署模型**清單已經顯示**傳統**，然後按一下**建立**。</span><span class="sxs-lookup"><span data-stu-id="9dbac-111">Click **NEW** > **Compute** > **Windows Server 2012 R2 Datacenter**, notice that hello **Select a deployment model** list already shows **Classic**, and then click **Create**.</span></span>
   
    ![在 Azure 入口網站中建立 VM](./media/virtual-networks-static-ip-classic-pportal/figure01.png)
3. <span data-ttu-id="9dbac-113">在 hello**建立 VM**刀鋒視窗中，輸入建立 hello VM toobe hello 名稱 (*DNS01*在我們的案例)，hello 本機系統管理員帳戶和密碼。</span><span class="sxs-lookup"><span data-stu-id="9dbac-113">In hello **Create VM** blade, enter hello name of hello VM toobe created (*DNS01* in our scenario), hello local administrator account, and password.</span></span>
   
    ![在 Azure 入口網站中建立 VM](./media/virtual-networks-static-ip-classic-pportal/figure02.png)
4. <span data-ttu-id="9dbac-115">按一下 選擇性組態  >  網路  >  虛擬網路，然後按一下TestVNet。</span><span class="sxs-lookup"><span data-stu-id="9dbac-115">Click **Optional Configuration** > **Network** > **Virtual Network**, and then click **TestVNet**.</span></span> <span data-ttu-id="9dbac-116">如果**TestVNet**就無法使用，請確定您使用 hello*美國中部*位置，建立 hello hello 本文開頭所述的測試環境。</span><span class="sxs-lookup"><span data-stu-id="9dbac-116">If **TestVNet** is not available, make sure you are using hello *Central US* location and have created hello test environment described at hello beginning of this article.</span></span>
   
    ![在 Azure 入口網站中建立 VM](./media/virtual-networks-static-ip-classic-pportal/figure03.png)
5. <span data-ttu-id="9dbac-118">在 hello**網路**刀鋒視窗中，目前未選取請確定 hello 子網路是*前端*，然後按一下  **IP 位址**下**IP 位址指派**按一下**靜態**，然後輸入*192.168.1.101*如**IP 位址**如下所示。</span><span class="sxs-lookup"><span data-stu-id="9dbac-118">In hello **Network** blade, make sure hello subnet currently selected is *FrontEnd*, then click **IP addresses**, under **IP address assignment** click **Static**, and then enter *192.168.1.101* for **IP Address** as seen below.</span></span>
   
    ![在 Azure 入口網站中建立 VM](./media/virtual-networks-static-ip-classic-pportal/figure04.png)    
6. <span data-ttu-id="9dbac-120">按一下**確定**在 hello **IP 位址**刀鋒視窗中，然後按一下 **確定**在 hello**網路**刀鋒視窗中，然後按一下**確定**在 hello**選用設定**刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="9dbac-120">Click **OK** in hello **IP addresses** blade, then click **OK** in hello **Network** blade, and click **OK** in hello **Optional config** blade.</span></span>
7. <span data-ttu-id="9dbac-121">在 hello**建立 VM**刀鋒視窗中，按一下 **建立**。</span><span class="sxs-lookup"><span data-stu-id="9dbac-121">In hello **Create VM** blade, click **Create**.</span></span> <span data-ttu-id="9dbac-122">請注意 hello 磚下方顯示在儀表板。</span><span class="sxs-lookup"><span data-stu-id="9dbac-122">Notice hello tile below displayed in your dashboard.</span></span>
   
    ![在 Azure 入口網站中建立 VM](./media/virtual-networks-static-ip-classic-pportal/figure05.png)

## <a name="how-tooretrieve-static-private-ip-address-information-for-a-vm"></a><span data-ttu-id="9dbac-124">如何 tooretrieve 靜態私人 IP 位址適用於 VM 的資訊</span><span class="sxs-lookup"><span data-stu-id="9dbac-124">How tooretrieve static private IP address information for a VM</span></span>
<span data-ttu-id="9dbac-125">tooview hello 靜態私人 IP 位址資訊 hello 與 hello 上述步驟，在建立 VM 執行下列步驟 hello。</span><span class="sxs-lookup"><span data-stu-id="9dbac-125">tooview hello static private IP address information for hello VM created with hello steps above, execute hello steps below.</span></span>

1. <span data-ttu-id="9dbac-126">從 hello Azure Azure 入口網站中，按一下 **瀏覽所有** > **虛擬機器 （傳統）** > **DNS01**  >  **所有設定** > **IP 位址**，並注意 hello IP 位址指派和 IP 位址，如下所示。</span><span class="sxs-lookup"><span data-stu-id="9dbac-126">From hello Azure Azure portal, click **BROWSE ALL** > **Virtual machines (classic)** > **DNS01** > **All settings** > **IP addresses** and notice hello IP address assignment and IP address as seen below.</span></span>
   
    ![在 Azure 入口網站中建立 VM](./media/virtual-networks-static-ip-classic-pportal/figure06.png)

## <a name="how-tooremove-a-static-private-ip-address-from-a-vm"></a><span data-ttu-id="9dbac-128">如何 tooremove 靜態私人 IP 位址從 VM</span><span class="sxs-lookup"><span data-stu-id="9dbac-128">How tooremove a static private IP address from a VM</span></span>
<span data-ttu-id="9dbac-129">tooremove hello 靜態私人 IP 位址從 hello 以上版本，在建立 VM，請遵循下列 hello 步驟。</span><span class="sxs-lookup"><span data-stu-id="9dbac-129">tooremove hello static private IP address from hello VM created above, follow hello steps below.</span></span>

1. <span data-ttu-id="9dbac-130">從 hello **IP 位址**按一下刀鋒視窗中，如上所示**動態**toohello 右邊**IP 位址指派**，然後按一下**儲存**，然後按一下**是**。</span><span class="sxs-lookup"><span data-stu-id="9dbac-130">From hello **IP addresses** blade shown above, click **Dynamic** toohello right of **IP address assignment**, then click **Save**, and then click **Yes**.</span></span>
   
    ![在 Azure 入口網站中建立 VM](./media/virtual-networks-static-ip-classic-pportal/figure07.png)

## <a name="how-tooadd-a-static-private-ip-address-tooan-existing-vm"></a><span data-ttu-id="9dbac-132">Tooadd 靜態私人 IP 定址 tooan 現有 VM 的方式</span><span class="sxs-lookup"><span data-stu-id="9dbac-132">How tooadd a static private IP address tooan existing VM</span></span>
<span data-ttu-id="9dbac-133">tooadd 靜態私人 IP 位址 toohello VM 建立使用 hello 上述步驟，請遵循下列 hello 步驟：</span><span class="sxs-lookup"><span data-stu-id="9dbac-133">tooadd a static private IP address toohello VM created using hello steps above, follow hello steps below:</span></span>

1. <span data-ttu-id="9dbac-134">從 hello **IP 位址**按一下刀鋒視窗中，如上所示**靜態**右邊 toohello **IP 位址指派**。</span><span class="sxs-lookup"><span data-stu-id="9dbac-134">From hello **IP addresses** blade shown above, click **Static** toohello right of **IP address assignment**.</span></span>
2. <span data-ttu-id="9dbac-135">IP 位址 輸入 192.168.1.101，然後按一下儲存，再按一下 是。</span><span class="sxs-lookup"><span data-stu-id="9dbac-135">Type *192.168.1.101* for **IP address**, then click **Save**, and then click **Yes**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="9dbac-136">後續步驟</span><span class="sxs-lookup"><span data-stu-id="9dbac-136">Next steps</span></span>
* <span data-ttu-id="9dbac-137">深入了解 [保留的公用 IP](virtual-networks-reserved-public-ip.md) 位址。</span><span class="sxs-lookup"><span data-stu-id="9dbac-137">Learn about [reserved public IP](virtual-networks-reserved-public-ip.md) addresses.</span></span>
* <span data-ttu-id="9dbac-138">深入了解 [執行個體層級公用 IP (ILPIP)](virtual-networks-instance-level-public-ip.md) 位址。</span><span class="sxs-lookup"><span data-stu-id="9dbac-138">Learn about [instance-level public IP (ILPIP)](virtual-networks-instance-level-public-ip.md) addresses.</span></span>
* <span data-ttu-id="9dbac-139">請參閱 hello[保留 IP REST Api](https://msdn.microsoft.com/library/azure/dn722420.aspx)。</span><span class="sxs-lookup"><span data-stu-id="9dbac-139">Consult hello [Reserved IP REST APIs](https://msdn.microsoft.com/library/azure/dn722420.aspx).</span></span>

