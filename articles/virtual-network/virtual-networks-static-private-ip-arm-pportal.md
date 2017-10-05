---
title: "設定 VM 的私人 IP 位址 - Azure 入口網站 | Microsoft Docs"
description: "了解如何使用 Azure 入口網站設定虛擬機器的私人 IP 位址。"
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
ms.openlocfilehash: 672462fad715758e50680fa5bade4b1f9d50e6e5
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="configure-private-ip-addresses-for-a-virtual-machine-using-the-azure-portal"></a><span data-ttu-id="0bb5c-103">使用 Azure 入口網站設定虛擬機器的私人 IP 位址</span><span class="sxs-lookup"><span data-stu-id="0bb5c-103">Configure private IP addresses for a virtual machine using the Azure portal</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="0bb5c-104">Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="0bb5c-104">Azure portal</span></span>](virtual-networks-static-private-ip-arm-pportal.md)
> * [<span data-ttu-id="0bb5c-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="0bb5c-105">PowerShell</span></span>](virtual-networks-static-private-ip-arm-ps.md)
> * [<span data-ttu-id="0bb5c-106">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="0bb5c-106">Azure CLI</span></span>](virtual-networks-static-private-ip-arm-cli.md)
> * [<span data-ttu-id="0bb5c-107">Azure 入口網站 (傳統)</span><span class="sxs-lookup"><span data-stu-id="0bb5c-107">Azure portal (Classic)</span></span>](virtual-networks-static-private-ip-classic-pportal.md)
> * [<span data-ttu-id="0bb5c-108">PowerShell (傳統)</span><span class="sxs-lookup"><span data-stu-id="0bb5c-108">PowerShell (Classic)</span></span>](virtual-networks-static-private-ip-classic-ps.md)
> * [<span data-ttu-id="0bb5c-109">Azure CLI (傳統)</span><span class="sxs-lookup"><span data-stu-id="0bb5c-109">Azure CLI (Classic)</span></span>](virtual-networks-static-private-ip-classic-cli.md)


[!INCLUDE [virtual-networks-static-private-ip-intro-include](../../includes/virtual-networks-static-private-ip-intro-include.md)]

[!INCLUDE [azure-arm-classic-important-include](../../includes/azure-arm-classic-important-include.md)]

<span data-ttu-id="0bb5c-110">本文涵蓋之內容包括資源管理員部署模型。</span><span class="sxs-lookup"><span data-stu-id="0bb5c-110">This article covers the Resource Manager deployment model.</span></span> <span data-ttu-id="0bb5c-111">您也可以 [管理傳統部署模型中的靜態私人 IP 位址](virtual-networks-static-private-ip-classic-pportal.md)。</span><span class="sxs-lookup"><span data-stu-id="0bb5c-111">You can also [manage static private IP address in the classic deployment model](virtual-networks-static-private-ip-classic-pportal.md).</span></span>

[!INCLUDE [virtual-networks-static-ip-scenario-include](../../includes/virtual-networks-static-ip-scenario-include.md)]

<span data-ttu-id="0bb5c-112">以下的範例步驟會預期已經建立簡單的環境。</span><span class="sxs-lookup"><span data-stu-id="0bb5c-112">The sample steps below expect a simple environment already created.</span></span> <span data-ttu-id="0bb5c-113">如果您想要執行如本文件中所顯示的步驟，請先建置 [建立 vnet](virtual-networks-create-vnet-arm-pportal.md)中所說明的測試環境。</span><span class="sxs-lookup"><span data-stu-id="0bb5c-113">If you want to run the steps as they are displayed in this document, first build the test environment described in [create a vnet](virtual-networks-create-vnet-arm-pportal.md).</span></span>

## <a name="how-to-create-a-vm-for-testing-static-private-ip-addresses"></a><span data-ttu-id="0bb5c-114">如何建立用來測試靜態私人 IP 位址的 VM</span><span class="sxs-lookup"><span data-stu-id="0bb5c-114">How to create a VM for testing static private IP addresses</span></span>
<span data-ttu-id="0bb5c-115">您無法在資源管理員部署模式中建立 VM 期間，使用 Azure 入口網站設定靜態私人 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="0bb5c-115">You cannot set a static private IP address during the creation of a VM in the Resource Manager deployment mode by using the Azure portal.</span></span> <span data-ttu-id="0bb5c-116">您必須先建立 VM，才能將其私人 IP 設定為靜態。</span><span class="sxs-lookup"><span data-stu-id="0bb5c-116">You must create the VM first, tehn set its private IP to be static.</span></span>

<span data-ttu-id="0bb5c-117">若要在名為 TestVNet 之 VNet 的 FrontEnd 子網路中建立名為 DNS01 的 VM，請遵循下列步驟。</span><span class="sxs-lookup"><span data-stu-id="0bb5c-117">To create a VM named *DNS01* in the *FrontEnd* subnet of a VNet named *TestVNet*, follow the steps below.</span></span>

1. <span data-ttu-id="0bb5c-118">透過瀏覽器瀏覽至 http://portal.azure.com，並視需要使用您的 Azure 帳戶登入。</span><span class="sxs-lookup"><span data-stu-id="0bb5c-118">From a browser, navigate to http://portal.azure.com and, if necessary, sign in with your Azure account.</span></span>
2. <span data-ttu-id="0bb5c-119">按一下 [新增]  >  [計算]  >  [Windows Server 2012 R2 Datacenter]，注意 [選取部署模型] 清單已經顯示 [Resource Manager]，然後按一下 [建立]，如下圖所示。</span><span class="sxs-lookup"><span data-stu-id="0bb5c-119">Click **NEW** > **Compute** > **Windows Server 2012 R2 Datacenter**, notice that the **Select a deployment model** list already shows **Resource Manager**, and then click **Create**, as seen in the figure below.</span></span>
   
    ![在 Azure 入口網站中建立 VM](./media/virtual-networks-static-ip-arm-pportal/figure01.png)
3. <span data-ttu-id="0bb5c-121">在 [基本概念]  刀鋒視窗中，輸入要建立之 VM 的名稱 (我們的案例中為*DNS01* )、本機系統管理員帳戶和密碼，如下圖所示。</span><span class="sxs-lookup"><span data-stu-id="0bb5c-121">In the **Basics** blade, enter the name of the VM to be created (*DNS01* in our scenario), the local administrator account, and password, as seen in the figure below.</span></span>
   
    ![基本概念刀鋒視窗](./media/virtual-networks-static-ip-arm-pportal/figure02.png)
4. <span data-ttu-id="0bb5c-123">請確定選取的 [位置] 為「美國中部」，按一下 [資源群組] 底下的 [選取現有項目]，然後再按一次 [資源群組]，按一下 [TestRG]，再按一下 [確定]。</span><span class="sxs-lookup"><span data-stu-id="0bb5c-123">Make sure the **Location** selected is *Central US*, then click **Select existing** under **Resource group**, then click **Resource group** again, then click *TestRG*, and then click **OK**.</span></span>
   
    ![基本概念刀鋒視窗](./media/virtual-networks-static-ip-arm-pportal/figure03.png)
5. <span data-ttu-id="0bb5c-125">在 [大小選擇] 刀鋒視窗中，選取 [A1 標準]，再按一下 [選取]。</span><span class="sxs-lookup"><span data-stu-id="0bb5c-125">In the **Choose a size** blade, select **A1 Standard**, and then click **Select**.</span></span>
   
    ![選擇尺寸刀鋒視窗](./media/virtual-networks-static-ip-arm-pportal/figure04.png)    
6. <span data-ttu-id="0bb5c-127">在 [設定] 刀鋒視窗中，確定下列屬性都已設定為下列的值，然後按一下 [確定]。</span><span class="sxs-lookup"><span data-stu-id="0bb5c-127">In teh **Settings** blade, make sure the following properties are set are set with the values below, and then click **OK**.</span></span>
   
    <span data-ttu-id="0bb5c-128">-**儲存體帳戶**：vnetstorage</span><span class="sxs-lookup"><span data-stu-id="0bb5c-128">-**Storage account**: *vnetstorage*</span></span>
   
   * <span data-ttu-id="0bb5c-129">**網路**：TestVNet</span><span class="sxs-lookup"><span data-stu-id="0bb5c-129">**Network**: *TestVNet*</span></span>
   * <span data-ttu-id="0bb5c-130">**子網路**：FrontEnd</span><span class="sxs-lookup"><span data-stu-id="0bb5c-130">**Subnet**: *FrontEnd*</span></span>
     
     ![選擇尺寸刀鋒視窗](./media/virtual-networks-static-ip-arm-pportal/figure05.png)     
7. <span data-ttu-id="0bb5c-132">在 [摘要] 刀鋒視窗中，按一下 [確定]。</span><span class="sxs-lookup"><span data-stu-id="0bb5c-132">In the **Summary** blade, click **OK**.</span></span> <span data-ttu-id="0bb5c-133">請注意您儀表板中下方顯示的磚。</span><span class="sxs-lookup"><span data-stu-id="0bb5c-133">Notice the tile below displayed in your dashboard.</span></span>
   
    ![在 Azure 入口網站中建立 VM](./media/virtual-networks-static-ip-arm-pportal/figure06.png)

## <a name="how-to-retrieve-static-private-ip-address-information-for-a-vm"></a><span data-ttu-id="0bb5c-135">如何擷取 VM 的靜態私人 IP 位址資訊</span><span class="sxs-lookup"><span data-stu-id="0bb5c-135">How to retrieve static private IP address information for a VM</span></span>
<span data-ttu-id="0bb5c-136">若要檢視使用上述步驟建立之 VM 的靜態私人 IP 位址資訊，請執行下列步驟。</span><span class="sxs-lookup"><span data-stu-id="0bb5c-136">To view the static private IP address information for the VM created with the steps above, execute the steps below.</span></span>

1. <span data-ttu-id="0bb5c-137">從 Azure 入口網站按一下 [瀏覽全部]  >  [虛擬機器]  >  [DNS01]  >  [所有設定]  >  [網路介面]，然後按一下所列出的唯一網路介面。</span><span class="sxs-lookup"><span data-stu-id="0bb5c-137">From the Azure Azure portal, click **BROWSE ALL** > **Virtual machines** > **DNS01** > **All settings** > **Network interfaces** and then click on the only network interface listed.</span></span>
   
    ![部署 VM 磚](./media/virtual-networks-static-ip-arm-pportal/figure07.png)
2. <span data-ttu-id="0bb5c-139">在 [網路介面] 刀鋒視窗中，按一下 [所有設定]  >  [IP 位址]，注意 [指派] 與 [IP 位址] 的值。</span><span class="sxs-lookup"><span data-stu-id="0bb5c-139">In the **Network interface** blade, click **All settings** > **IP addresses** and notice the **Assignment** and **IP address** values.</span></span>
   
    ![部署 VM 磚](./media/virtual-networks-static-ip-arm-pportal/figure08.png)

## <a name="how-to-add-a-static-private-ip-address-to-an-existing-vm"></a><span data-ttu-id="0bb5c-141">如何將靜態私人 IP 位址新增至現有的 VM</span><span class="sxs-lookup"><span data-stu-id="0bb5c-141">How to add a static private IP address to an existing VM</span></span>
<span data-ttu-id="0bb5c-142">若要將靜態私人 IP 位址新增至使用上述步驟建立之 VM，請遵循下列步驟：</span><span class="sxs-lookup"><span data-stu-id="0bb5c-142">To add a static private IP address to the VM created using the steps above, follow the steps below:</span></span>

1. <span data-ttu-id="0bb5c-143">從上方顯示的 [IP 位址] 刀鋒視窗中，按一下 [指派] 底下的[靜態]。</span><span class="sxs-lookup"><span data-stu-id="0bb5c-143">From the **IP addresses** blade shown above, click **Static** under **Assignment**.</span></span>
2. <span data-ttu-id="0bb5c-144">[IP 位址] 輸入 192.168.1.101，然後按一下 [儲存]。</span><span class="sxs-lookup"><span data-stu-id="0bb5c-144">Type *192.168.1.101* for **IP address**, and then click **Save**.</span></span>
   
    ![在 Azure 入口網站中建立 VM](./media/virtual-networks-static-ip-arm-pportal/figure09.png)

> [!NOTE]
> <span data-ttu-id="0bb5c-146">如果按一下 [儲存] 之後您注意到指派仍然設定為 [動態]，這表示您輸入的 IP 位址已在使用。</span><span class="sxs-lookup"><span data-stu-id="0bb5c-146">If after clicking **Save** you notice that the assignment is still set to **Dynamic**, it means that the IP address you typed is already in use.</span></span> <span data-ttu-id="0bb5c-147">請嘗試不同的 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="0bb5c-147">Try a different IP address.</span></span>
> 
> 

## <a name="how-to-remove-a-static-private-ip-address-from-a-vm"></a><span data-ttu-id="0bb5c-148">如何移除 VM 的靜態私人 IP 位址</span><span class="sxs-lookup"><span data-stu-id="0bb5c-148">How to remove a static private IP address from a VM</span></span>
<span data-ttu-id="0bb5c-149">若要移除上述所建立 VM 的靜態私人 IP 位址，請完成下列步驟：</span><span class="sxs-lookup"><span data-stu-id="0bb5c-149">To remove the static private IP address from the VM created above, complete the following step:</span></span>

<span data-ttu-id="0bb5c-150">從上方顯示的 [IP 位址] 刀鋒視窗中，按一下 [指派] 底下的[動態]，然後按一下 [儲存]。</span><span class="sxs-lookup"><span data-stu-id="0bb5c-150">From the **IP addresses** blade shown above, click **Dynamic** under **Assignment**, and then click **Save**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="0bb5c-151">後續步驟</span><span class="sxs-lookup"><span data-stu-id="0bb5c-151">Next steps</span></span>
* <span data-ttu-id="0bb5c-152">深入了解 [保留的公用 IP](virtual-networks-reserved-public-ip.md) 位址。</span><span class="sxs-lookup"><span data-stu-id="0bb5c-152">Learn about [reserved public IP](virtual-networks-reserved-public-ip.md) addresses.</span></span>
* <span data-ttu-id="0bb5c-153">深入了解 [執行個體層級公用 IP (ILPIP)](virtual-networks-instance-level-public-ip.md) 位址。</span><span class="sxs-lookup"><span data-stu-id="0bb5c-153">Learn about [instance-level public IP (ILPIP)](virtual-networks-instance-level-public-ip.md) addresses.</span></span>
* <span data-ttu-id="0bb5c-154">請參閱 [保留 IP REST API](https://msdn.microsoft.com/library/azure/dn722420.aspx)。</span><span class="sxs-lookup"><span data-stu-id="0bb5c-154">Consult the [Reserved IP REST APIs](https://msdn.microsoft.com/library/azure/dn722420.aspx).</span></span>

