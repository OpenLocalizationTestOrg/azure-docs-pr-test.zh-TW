---
title: "Azure 虛擬機器的多個 IP 位址 - 入口網站 | Microsoft Docs"
description: "了解如何使用 Azure 入口網站 / Resource Manager 對虛擬機器指派多個 IP 位址。"
services: virtual-network
documentationcenter: na
author: anavinahar
manager: narayan
editor: 
tags: azure-resource-manager
ms.assetid: 3a8cae97-3bed-430d-91b3-274696d91e34
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 11/30/2016
ms.author: annahar
ms.openlocfilehash: d264bd47d76db8015a64f09248c57c94572e2693
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="assign-multiple-ip-addresses-to-virtual-machines-using-the-azure-portal"></a><span data-ttu-id="f92e3-103">使用 Azure 入口網站將多個 IP 位址指派給虛擬機器</span><span class="sxs-lookup"><span data-stu-id="f92e3-103">Assign multiple IP addresses to virtual machines using the Azure portal</span></span>

>[!INCLUDE [virtual-network-multiple-ip-addresses-intro.md](../../includes/virtual-network-multiple-ip-addresses-intro.md)]
>
<span data-ttu-id="f92e3-104">本文說明如何使用 Azure 入口網站透過 Azure Resource Manager 部署模型建立虛擬機器 (VM)。</span><span class="sxs-lookup"><span data-stu-id="f92e3-104">This article explains how to create a virtual machine (VM) through the Azure Resource Manager deployment model using the Azure portal.</span></span> <span data-ttu-id="f92e3-105">無法將多個 IP 位址指派給透過傳統部署模型建立的資源。</span><span class="sxs-lookup"><span data-stu-id="f92e3-105">Multiple IP addresses cannot be assigned to resources created through the classic deployment model.</span></span> <span data-ttu-id="f92e3-106">若要深入了解 Azure 部署模型，請參閱[了解部署模型](../resource-manager-deployment-model.md)文章。</span><span class="sxs-lookup"><span data-stu-id="f92e3-106">To learn more about Azure deployment models, read the [Understand deployment models](../resource-manager-deployment-model.md) article.</span></span>

[!INCLUDE [virtual-network-multiple-ip-addresses-template-scenario.md](../../includes/virtual-network-multiple-ip-addresses-scenario.md)]

## <span data-ttu-id="f92e3-107"><a name = "create"></a>建立有多個 IP 位址的 VM</span><span class="sxs-lookup"><span data-stu-id="f92e3-107"><a name = "create"></a>Create a VM with multiple IP addresses</span></span>

<span data-ttu-id="f92e3-108">如果您想要建立具有多個 IP 位址或一個靜態私人 IP 位址的 VM，您必須使用 PowerShell 或 Azure CLI 來建立它。</span><span class="sxs-lookup"><span data-stu-id="f92e3-108">If you want to create a VM with multiple IP addresses, or a static private IP address, you must create it using PowerShell or the Azure CLI.</span></span> <span data-ttu-id="f92e3-109">按一下本文頂端的 PowerShell 或 CLI 選項，即可了解作法。</span><span class="sxs-lookup"><span data-stu-id="f92e3-109">Click the PowerShell or CLI options at the top of this article to learn how.</span></span> <span data-ttu-id="f92e3-110">您可以依照[建立 Windows VM](../virtual-machines/virtual-machines-windows-hero-tutorial.md) 或[建立 Linux VM](../virtual-machines/linux/quick-create-portal.md)文章中的步驟，透過入口網站建立具有單一動態私人 IP 位址及 (選擇性) 單一公用 IP 位址的 VM。</span><span class="sxs-lookup"><span data-stu-id="f92e3-110">You can create a VM with a single dynamic private IP address and (optionally) a single public IP address using the portal by following the steps in the [Create a Windows VM](../virtual-machines/virtual-machines-windows-hero-tutorial.md) or [Create a Linux VM](../virtual-machines/linux/quick-create-portal.md) articles.</span></span> <span data-ttu-id="f92e3-111">建立 VM 之後，您可以依照本文的[將 IP 位址新增至 VM](#add) 一節中的步驟，透過入口網站將 IP 位址類型從動態變更為靜態，並新增其他 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="f92e3-111">After you create the VM, you can change the IP address type from dynamic to static and add additional IP addresses using the portal by following steps in the [Add IP addresses to a VM](#add) section of this article.</span></span>

## <span data-ttu-id="f92e3-112"><a name="add"></a>將 IP 位址新增至 VM</span><span class="sxs-lookup"><span data-stu-id="f92e3-112"><a name="add"></a>Add IP addresses to a VM</span></span>

<span data-ttu-id="f92e3-113">您可以完成後續步驟，將私人和公用 IP 位址新增至 NIC。</span><span class="sxs-lookup"><span data-stu-id="f92e3-113">You can add private and public IP addresses to a NIC by completing the steps that follow.</span></span> <span data-ttu-id="f92e3-114">下列各節中的範例假設您已經有一個 VM，其具有本文中的[案例](#Scenario)所述的三項 IP 組態，您不需要進行設定。</span><span class="sxs-lookup"><span data-stu-id="f92e3-114">The examples in the following sections assume that you already have a VM with the three IP configurations described in the [scenario](#Scenario) in this article, but it's not required that you do.</span></span>

### <span data-ttu-id="f92e3-115"><a name="coreadd"></a>核心步驟</span><span class="sxs-lookup"><span data-stu-id="f92e3-115"><a name="coreadd"></a>Core steps</span></span>

1. <span data-ttu-id="f92e3-116">瀏覽至 Azure 入口網站 (https://portal.azure.com) 並視需要進行登入。</span><span class="sxs-lookup"><span data-stu-id="f92e3-116">Browse to the Azure portal at https://portal.azure.com and sign into it, if necessary.</span></span>
2. <span data-ttu-id="f92e3-117">在 Azure 入口網站中，按一下 [更多服務]，接著在篩選方塊中輸入「虛擬機器」，然後按一下 [虛擬機器]。</span><span class="sxs-lookup"><span data-stu-id="f92e3-117">In the portal, click **More services** > type *virtual machines* in the filter box, and then click **Virtual machines**.</span></span>
3. <span data-ttu-id="f92e3-118">在 [虛擬機器] 刀鋒視窗中，按一下您想要新增 IP 位址的 VM。</span><span class="sxs-lookup"><span data-stu-id="f92e3-118">In the **Virtual machines** blade, click the VM you want to add IP addresses to.</span></span> <span data-ttu-id="f92e3-119">在顯示的 [虛擬機器] 刀鋒視窗中，按一下 [網路介面]，然後選取您想要新增 IP 位址的網路介面。</span><span class="sxs-lookup"><span data-stu-id="f92e3-119">Click **Network interfaces** in the virtual machine blade that appears, and then select the network interface you want to add the IP addresses to.</span></span> <span data-ttu-id="f92e3-120">在下圖顯示的範例中，已選取名為 myVM 的 VM 中名為 myNIC 的 NIC︰</span><span class="sxs-lookup"><span data-stu-id="f92e3-120">In the example shown in the following picture, the NIC named *myNIC* from the VM named *myVM* is selected:</span></span>

    ![網路介面](./media/virtual-network-multiple-ip-addresses-portal/figure1.png)

4. <span data-ttu-id="f92e3-122">在針對所選 NIC 顯示的刀鋒視窗中，按一下 [IP 組態]。</span><span class="sxs-lookup"><span data-stu-id="f92e3-122">In the blade that appears for the NIC you selected, click **IP configurations**.</span></span>

<span data-ttu-id="f92e3-123">根據您想要新增的 IP 位址類型，完成後續其中一節的步驟。</span><span class="sxs-lookup"><span data-stu-id="f92e3-123">Complete the steps in one of the sections that follow, based on the type of IP address you want to add.</span></span>

### <a name="add-a-private-ip-address"></a><span data-ttu-id="f92e3-124">**新增私人 IP 位址**</span><span class="sxs-lookup"><span data-stu-id="f92e3-124">**Add a private IP address**</span></span>

<span data-ttu-id="f92e3-125">完成下列步驟，以新增私人 IP 位址：</span><span class="sxs-lookup"><span data-stu-id="f92e3-125">Complete the following steps to add a new private IP address:</span></span>

1. <span data-ttu-id="f92e3-126">完成本文的[核心步驟](#coreadd)一節中的步驟。</span><span class="sxs-lookup"><span data-stu-id="f92e3-126">Complete the steps in the [Core steps](#coreadd) section of this article.</span></span>
2. <span data-ttu-id="f92e3-127">按一下 [新增]。</span><span class="sxs-lookup"><span data-stu-id="f92e3-127">Click **Add**.</span></span> <span data-ttu-id="f92e3-128">在所顯示的 [新增 IP 設定] 刀鋒視窗中，建立名為 *IPConfig-4* 並以 *10.0.0.7* 作為「靜態」私人 IP 位址的 IP 組態，然後按一下 [確定]。</span><span class="sxs-lookup"><span data-stu-id="f92e3-128">In the **Add IP configuration** blade that appears, create an IP configuration named *IPConfig-4* with *10.0.0.7* as a *Static* private IP address, then click **OK**.</span></span>

    > [!NOTE]
    > <span data-ttu-id="f92e3-129">新增靜態 IP 位址時，您必須在 NIC 所連接的子網路上指定未使用的有效位址。</span><span class="sxs-lookup"><span data-stu-id="f92e3-129">When adding a static IP address, you must specify an unused, valid address on the subnet the NIC is connected to.</span></span> <span data-ttu-id="f92e3-130">如果您選取的位址無法使用，入口網站會針對 IP 位址顯示 X，而您必須選取不同的位址。</span><span class="sxs-lookup"><span data-stu-id="f92e3-130">If the address you select is not available, the portal will show an X for the IP address and you'll need to select a different one.</span></span>

3. <span data-ttu-id="f92e3-131">按一下 [確定] 之後，刀鋒視窗會關閉，而您會看到新的 IP 組態列出。</span><span class="sxs-lookup"><span data-stu-id="f92e3-131">Once you click OK, the blade will close and you'll see the new IP configuration listed.</span></span> <span data-ttu-id="f92e3-132">按一下 [確定]，以關閉 [新增 IP 組態] 刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="f92e3-132">Click **OK** to close the **Add IP configuration** blade.</span></span>
4. <span data-ttu-id="f92e3-133">您可以按一下 [新增] 來新增其他 IP 組態，或關閉所有開啟的刀鋒視窗以完成 IP 位址新增。</span><span class="sxs-lookup"><span data-stu-id="f92e3-133">You can click **Add** to add additional IP configurations, or close all open blades to finish adding IP addresses.</span></span>
5. <span data-ttu-id="f92e3-134">完成本文的[將 IP 位址新增至 VM 作業系統](#os-config)一節中適用於您的作業系統的步驟，將私人 IP 位址新增至 VM 作業系統。</span><span class="sxs-lookup"><span data-stu-id="f92e3-134">Add the private IP addresses to the VM operating system by completing the steps for your operating system in the [Add IP addresses to a VM operating system](#os-config) section of this article.</span></span>

### <a name="add-a-public-ip-address"></a><span data-ttu-id="f92e3-135">新增公用 IP 位址</span><span class="sxs-lookup"><span data-stu-id="f92e3-135">Add a public IP address</span></span>

<span data-ttu-id="f92e3-136">將公用 IP 位址與新的 IP 組態或現有的 IP 組態產生關聯，便可新增公用 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="f92e3-136">A public IP address is added by associating a public IP address resource to either a new IP configuration or an existing IP configuration.</span></span>

> [!NOTE]
> <span data-ttu-id="f92e3-137">公用 IP 位址需要少許費用。</span><span class="sxs-lookup"><span data-stu-id="f92e3-137">Public IP addresses have a nominal fee.</span></span> <span data-ttu-id="f92e3-138">若要深入了解 IP 位址定價，請閱讀 [IP 位址定價](https://azure.microsoft.com/pricing/details/ip-addresses) 頁面。</span><span class="sxs-lookup"><span data-stu-id="f92e3-138">To learn more about IP address pricing, read the [IP address pricing](https://azure.microsoft.com/pricing/details/ip-addresses) page.</span></span> <span data-ttu-id="f92e3-139">訂用帳戶中可使用的公用 IP 位址數目有限制。</span><span class="sxs-lookup"><span data-stu-id="f92e3-139">There is a limit to the number of public IP addresses that can be used in a subscription.</span></span> <span data-ttu-id="f92e3-140">若要深入了解限制，請參閱 [Azure 限制](../azure-subscription-service-limits.md#networking-limits)文章。</span><span class="sxs-lookup"><span data-stu-id="f92e3-140">To learn more about the limits, read the [Azure limits](../azure-subscription-service-limits.md#networking-limits) article.</span></span>
> 

### <span data-ttu-id="f92e3-141"><a name="create-public-ip"></a>建立公用 IP 位址資源</span><span class="sxs-lookup"><span data-stu-id="f92e3-141"><a name="create-public-ip"></a>Create a public IP address resource</span></span>

<span data-ttu-id="f92e3-142">公用 IP 位址是公用 IP 位址資源的其中一項設定</span><span class="sxs-lookup"><span data-stu-id="f92e3-142">A public IP address is one setting for a public IP address resource.</span></span> <span data-ttu-id="f92e3-143">如果您的公用 IP 位址資源目前並未關聯至您想要產生關聯的 IP 組態，請略過下列步驟，並視需要完成後續其中一節的步驟。</span><span class="sxs-lookup"><span data-stu-id="f92e3-143">If you have a public IP address resource that is not currently associated to an IP configuration that you want to associate to an IP configuration, skip the following steps and complete the steps in one of the sections that follow, as you require.</span></span> <span data-ttu-id="f92e3-144">如果您沒有可用的公用 IP 位址資源，請完成下列步驟來建立一個︰</span><span class="sxs-lookup"><span data-stu-id="f92e3-144">If you don't have an available public IP address resource, complete the following steps to create one:</span></span>

1. <span data-ttu-id="f92e3-145">瀏覽至 Azure 入口網站 (https://portal.azure.com) 並視需要進行登入。</span><span class="sxs-lookup"><span data-stu-id="f92e3-145">Browse to the Azure portal at https://portal.azure.com and sign into it, if necessary.</span></span>
3. <span data-ttu-id="f92e3-146">在入口網站中，按一下 [新增] > [網路] > [公用 IP 位址]。</span><span class="sxs-lookup"><span data-stu-id="f92e3-146">In the portal, click **New** > **Networking** > **Public IP address**.</span></span>
4. <span data-ttu-id="f92e3-147">在顯示的 [建立公用 IP 位址]刀鋒視窗中，輸入 [名稱]，選取 [IP 位址指派] 類型、[訂用帳戶]、[資源群組] 和 [位置]，然後按一下 [建立]，如下圖所示︰</span><span class="sxs-lookup"><span data-stu-id="f92e3-147">In the **Create public IP address** blade that appears, enter a **Name**, select an **IP address assignment** type, a **Subscription**, a **Resource group**, and a **Location**, then click **Create**, as shown in the following picture:</span></span>

    ![建立公用 IP 位址資源](./media/virtual-network-multiple-ip-addresses-portal/figure5.png)

5. <span data-ttu-id="f92e3-149">完成後續其中一節的步驟，將公用 IP 位址資源與 IP 組態產生關聯。</span><span class="sxs-lookup"><span data-stu-id="f92e3-149">Complete the steps in one of the sections that follow to associate the public IP address resource to an IP configuration.</span></span>

#### <a name="associate-the-public-ip-address-resource-to-a-new-ip-configuration"></a><span data-ttu-id="f92e3-150">將公用 IP 位址資源與新的 IP 組態產生關聯</span><span class="sxs-lookup"><span data-stu-id="f92e3-150">Associate the public IP address resource to a new IP configuration</span></span>

1. <span data-ttu-id="f92e3-151">完成本文的[核心步驟](#coreadd)一節中的步驟。</span><span class="sxs-lookup"><span data-stu-id="f92e3-151">Complete the steps in the [Core steps](#coreadd) section of this article.</span></span>
2. <span data-ttu-id="f92e3-152">按一下 [新增] 。</span><span class="sxs-lookup"><span data-stu-id="f92e3-152">Click **Add**.</span></span> <span data-ttu-id="f92e3-153">在顯示的 [新增 IP 組態] 刀鋒視窗中，建立名為 IPConfig-4 的 IP 組態。</span><span class="sxs-lookup"><span data-stu-id="f92e3-153">In the **Add IP configuration** blade that appears, create an IP configuration named *IPConfig-4*.</span></span> <span data-ttu-id="f92e3-154">啟用 [公用 IP 位址]，然後從顯示的 [選擇公用 IP 位址] 刀鋒視窗中，選取現有的可用公用 IP 位址資源。</span><span class="sxs-lookup"><span data-stu-id="f92e3-154">Enable the **Public IP address** and select an existing, available public IP address resource from the **Choose public IP address** blade that appears.</span></span>

    <span data-ttu-id="f92e3-155">選取公用 IP 位址資源後，請按一下 [確定]，刀鋒視窗便會關閉。</span><span class="sxs-lookup"><span data-stu-id="f92e3-155">Once you've selected the public IP address resource, click **OK** and the blade will close.</span></span> <span data-ttu-id="f92e3-156">如果您沒有現有的公用 IP 位址，您可以完成[建立公用 IP 位址資源](#create-public-ip)一節中的步驟，加以建立。</span><span class="sxs-lookup"><span data-stu-id="f92e3-156">If you don't have an existing public IP address, you can create one by completing the steps in the [Create a public IP address resource](#create-public-ip) section of this article.</span></span> 

3. <span data-ttu-id="f92e3-157">檢閱新的 IP 組態。</span><span class="sxs-lookup"><span data-stu-id="f92e3-157">Review the new IP configuration.</span></span> <span data-ttu-id="f92e3-158">即使未明確指派私人 IP 位址，但已自動指派一個給 IP 組態，因為所有 IP 組態都必須有一個私人 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="f92e3-158">Even though a private IP address wasn't explicitly assigned, one was automatically assigned to the IP configuration, because all IP configurations must have a private IP address.</span></span>
4. <span data-ttu-id="f92e3-159">您可以按一下 [新增] 來新增其他 IP 組態，或關閉所有開啟的刀鋒視窗以完成 IP 位址新增。</span><span class="sxs-lookup"><span data-stu-id="f92e3-159">You can click **Add** to add additional IP configurations, or close all open blades to finish adding IP addresses.</span></span>
5. <span data-ttu-id="f92e3-160">完成本文的[將 IP 位址新增至 VM 作業系統](#os-config)一節中適用於您的作業系統的步驟，將私人 IP 位址新增至 VM 作業系統。</span><span class="sxs-lookup"><span data-stu-id="f92e3-160">Add the private IP address to the VM operating system by completing the steps for your operating system in the [Add IP addresses to a VM operating system](#os-config) section of this article.</span></span> <span data-ttu-id="f92e3-161">請勿將公用 IP 位址新增至作業系統。</span><span class="sxs-lookup"><span data-stu-id="f92e3-161">Do not add the public IP address to the operating system.</span></span>

#### <a name="associate-the-public-ip-address-resource-to-an-existing-ip-configuration"></a><span data-ttu-id="f92e3-162">將公用 IP 位址資源與現有的 IP 組態產生關聯</span><span class="sxs-lookup"><span data-stu-id="f92e3-162">Associate the public IP address resource to an existing IP configuration</span></span>

1. <span data-ttu-id="f92e3-163">完成本文的[核心步驟](#coreadd)一節中的步驟。</span><span class="sxs-lookup"><span data-stu-id="f92e3-163">Complete the steps in the [Core steps](#coreadd) section of this article.</span></span>
2. <span data-ttu-id="f92e3-164">按一下您想要新增公用 IP 位址資源的 IP 組態。</span><span class="sxs-lookup"><span data-stu-id="f92e3-164">Click the IP configuration you want to add the public IP address resource to.</span></span>
3. <span data-ttu-id="f92e3-165">在顯示的 [IPConfig] 刀鋒視窗中，按一下 [IP 位址]。</span><span class="sxs-lookup"><span data-stu-id="f92e3-165">In the IPConfig blade that appears, click **IP address**.</span></span>
4. <span data-ttu-id="f92e3-166">在顯示的 [選擇公用 IP 位址] 刀鋒視窗中，選取一個公用 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="f92e3-166">In the **Choose public IP address** blade that appears, select a public IP address.</span></span>
5. <span data-ttu-id="f92e3-167">按一下 [儲存]，這些刀鋒視窗便會關閉。</span><span class="sxs-lookup"><span data-stu-id="f92e3-167">Click **Save** and the blades will close.</span></span> <span data-ttu-id="f92e3-168">如果您沒有現有的公用 IP 位址，您可以完成[建立公用 IP 位址資源](#create-public-ip)一節中的步驟，加以建立。</span><span class="sxs-lookup"><span data-stu-id="f92e3-168">If you don't have an existing public IP address, you can create one by completing the steps in the [Create a public IP address resource](#create-public-ip) section of this article.</span></span>
3. <span data-ttu-id="f92e3-169">檢閱新的 IP 組態。</span><span class="sxs-lookup"><span data-stu-id="f92e3-169">Review the new IP configuration.</span></span>
4. <span data-ttu-id="f92e3-170">您可以按一下 [新增] 來新增其他 IP 組態，或關閉所有開啟的刀鋒視窗以完成 IP 位址新增。</span><span class="sxs-lookup"><span data-stu-id="f92e3-170">You can click **Add** to add additional IP configurations, or close all open blades to finish adding IP addresses.</span></span> <span data-ttu-id="f92e3-171">請勿將公用 IP 位址新增至作業系統。</span><span class="sxs-lookup"><span data-stu-id="f92e3-171">Do not add the public IP address to the operating system.</span></span>


[!INCLUDE [virtual-network-multiple-ip-addresses-os-config.md](../../includes/virtual-network-multiple-ip-addresses-os-config.md)]
