---
title: "Azure 虛擬機器-入口網站的 aaaMultiple IP 位址 |Microsoft 文件"
description: "了解如何 tooassign 多個 IP 位址 tooa 虛擬機器使用 hello Azure 入口網站 |資源管理員。"
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
ms.openlocfilehash: 34075766ac68c8de38c258a4d70e35881f28bb0b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="assign-multiple-ip-addresses-toovirtual-machines-using-hello-azure-portal"></a><span data-ttu-id="f44cd-103">指派多個 IP 位址 toovirtual 使用，在電腦 hello Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="f44cd-103">Assign multiple IP addresses toovirtual machines using hello Azure portal</span></span>

>[!INCLUDE [virtual-network-multiple-ip-addresses-intro.md](../../includes/virtual-network-multiple-ip-addresses-intro.md)]
>
<span data-ttu-id="f44cd-104">本文說明如何透過 hello Azure Resource Manager 部署模型使用的虛擬機器 (VM) toocreate hello Azure 入口網站。</span><span class="sxs-lookup"><span data-stu-id="f44cd-104">This article explains how toocreate a virtual machine (VM) through hello Azure Resource Manager deployment model using hello Azure portal.</span></span> <span data-ttu-id="f44cd-105">Tooresources 透過 hello 傳統部署模型所建立，無法指派多個 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="f44cd-105">Multiple IP addresses cannot be assigned tooresources created through hello classic deployment model.</span></span> <span data-ttu-id="f44cd-106">深入了解 Azure 的部署模型，讀取 hello toolearn[了解部署模型](../resource-manager-deployment-model.md)發行項。</span><span class="sxs-lookup"><span data-stu-id="f44cd-106">toolearn more about Azure deployment models, read hello [Understand deployment models](../resource-manager-deployment-model.md) article.</span></span>

[!INCLUDE [virtual-network-multiple-ip-addresses-template-scenario.md](../../includes/virtual-network-multiple-ip-addresses-scenario.md)]

## <span data-ttu-id="f44cd-107"><a name = "create"></a>建立有多個 IP 位址的 VM</span><span class="sxs-lookup"><span data-stu-id="f44cd-107"><a name = "create"></a>Create a VM with multiple IP addresses</span></span>

<span data-ttu-id="f44cd-108">如果您想 toocreate 具有多個 IP 位址或靜態私人 IP 位址的 VM，您必須建立使用 PowerShell 或 hello Azure CLI。</span><span class="sxs-lookup"><span data-stu-id="f44cd-108">If you want toocreate a VM with multiple IP addresses, or a static private IP address, you must create it using PowerShell or hello Azure CLI.</span></span> <span data-ttu-id="f44cd-109">如何按一下 hello PowerShell 或 CLI 選項在此發行項 toolearn hello 最上方。</span><span class="sxs-lookup"><span data-stu-id="f44cd-109">Click hello PowerShell or CLI options at hello top of this article toolearn how.</span></span> <span data-ttu-id="f44cd-110">您可以使用單一動態私人 IP 位址，以及 （選擇性） 單一公用 IP 位址使用 hello 入口網站中 hello 的 hello 步驟來建立 VM[建立 Windows VM](../virtual-machines/virtual-machines-windows-hero-tutorial.md)或[建立 Linux VM](../virtual-machines/linux/quick-create-portal.md)文件。</span><span class="sxs-lookup"><span data-stu-id="f44cd-110">You can create a VM with a single dynamic private IP address and (optionally) a single public IP address using hello portal by following hello steps in hello [Create a Windows VM](../virtual-machines/virtual-machines-windows-hero-tutorial.md) or [Create a Linux VM](../virtual-machines/linux/quick-create-portal.md) articles.</span></span> <span data-ttu-id="f44cd-111">建立 hello VM 之後，您可以從動態 toostatic 變更 hello IP 位址類型，並加入其他 IP 位址使用 hello 中的下列步驟 hello 網站[新增 IP 位址 tooa VM](#add)本文一節。</span><span class="sxs-lookup"><span data-stu-id="f44cd-111">After you create hello VM, you can change hello IP address type from dynamic toostatic and add additional IP addresses using hello portal by following steps in hello [Add IP addresses tooa VM](#add) section of this article.</span></span>

## <span data-ttu-id="f44cd-112"><a name="add"></a>新增 IP 位址 tooa VM</span><span class="sxs-lookup"><span data-stu-id="f44cd-112"><a name="add"></a>Add IP addresses tooa VM</span></span>

<span data-ttu-id="f44cd-113">您可以藉由完成 hello 遵照的步驟，新增私人和公用 IP 位址 tooa NIC。</span><span class="sxs-lookup"><span data-stu-id="f44cd-113">You can add private and public IP addresses tooa NIC by completing hello steps that follow.</span></span> <span data-ttu-id="f44cd-114">hello hello 下列各節中的範例假設您已經有含 hello 三 hello 中所述的 IP 組態的 VM[案例](#Scenario)在此文件，但它不需要您執行。</span><span class="sxs-lookup"><span data-stu-id="f44cd-114">hello examples in hello following sections assume that you already have a VM with hello three IP configurations described in hello [scenario](#Scenario) in this article, but it's not required that you do.</span></span>

### <span data-ttu-id="f44cd-115"><a name="coreadd"></a>核心步驟</span><span class="sxs-lookup"><span data-stu-id="f44cd-115"><a name="coreadd"></a>Core steps</span></span>

1. <span data-ttu-id="f44cd-116">如有必要，請到其中，瀏 toohello 在 https://portal.azure.com 並登入 Azure 入口網站。</span><span class="sxs-lookup"><span data-stu-id="f44cd-116">Browse toohello Azure portal at https://portal.azure.com and sign into it, if necessary.</span></span>
2. <span data-ttu-id="f44cd-117">在 hello 入口網站中，按一下 **更多服務**> 類型*虛擬機器*在 hello 篩選 方塊中，然後按一下**虛擬機器**。</span><span class="sxs-lookup"><span data-stu-id="f44cd-117">In hello portal, click **More services** > type *virtual machines* in hello filter box, and then click **Virtual machines**.</span></span>
3. <span data-ttu-id="f44cd-118">在 hello**虛擬機器**刀鋒視窗中，按一下的 hello VM 想 tooadd IP 位址。</span><span class="sxs-lookup"><span data-stu-id="f44cd-118">In hello **Virtual machines** blade, click hello VM you want tooadd IP addresses to.</span></span> <span data-ttu-id="f44cd-119">按一下**網路介面**中出現，hello 虛擬機器刀鋒視窗，然後再選取 hello 網路介面想 tooadd hello IP 位址。</span><span class="sxs-lookup"><span data-stu-id="f44cd-119">Click **Network interfaces** in hello virtual machine blade that appears, and then select hello network interface you want tooadd hello IP addresses to.</span></span> <span data-ttu-id="f44cd-120">在 hello 範例所示 hello 遵循圖片，hello NIC 名為*myNIC* hello 名為 VM 從*myVM*選取：</span><span class="sxs-lookup"><span data-stu-id="f44cd-120">In hello example shown in hello following picture, hello NIC named *myNIC* from hello VM named *myVM* is selected:</span></span>

    ![網路介面](./media/virtual-network-multiple-ip-addresses-portal/figure1.png)

4. <span data-ttu-id="f44cd-122">在 hello 刀鋒視窗中出現的 hello 您選取的 NIC，按一下  **IP 組態**。</span><span class="sxs-lookup"><span data-stu-id="f44cd-122">In hello blade that appears for hello NIC you selected, click **IP configurations**.</span></span>

<span data-ttu-id="f44cd-123">完整的 hello hello 以下各節的其中一個步驟，您想 tooadd 根據 hello 類型的 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="f44cd-123">Complete hello steps in one of hello sections that follow, based on hello type of IP address you want tooadd.</span></span>

### <a name="add-a-private-ip-address"></a><span data-ttu-id="f44cd-124">**新增私人 IP 位址**</span><span class="sxs-lookup"><span data-stu-id="f44cd-124">**Add a private IP address**</span></span>

<span data-ttu-id="f44cd-125">完成下列步驟 tooadd 新的私用 IP 位址的 hello:</span><span class="sxs-lookup"><span data-stu-id="f44cd-125">Complete hello following steps tooadd a new private IP address:</span></span>

1. <span data-ttu-id="f44cd-126">完整的 hello 步驟 hello[核心步驟](#coreadd)本文一節。</span><span class="sxs-lookup"><span data-stu-id="f44cd-126">Complete hello steps in hello [Core steps](#coreadd) section of this article.</span></span>
2. <span data-ttu-id="f44cd-127">按一下 [新增] 。</span><span class="sxs-lookup"><span data-stu-id="f44cd-127">Click **Add**.</span></span> <span data-ttu-id="f44cd-128">在 hello**新增 IP 組態**刀鋒視窗中，建立名為 IP 設定*IPConfig 4*與*10.0.0.7*為*靜態*私人 IP 位址，然後按一下 **確定**。</span><span class="sxs-lookup"><span data-stu-id="f44cd-128">In hello **Add IP configuration** blade that appears, create an IP configuration named *IPConfig-4* with *10.0.0.7* as a *Static* private IP address, then click **OK**.</span></span>

    > [!NOTE]
    > <span data-ttu-id="f44cd-129">時新增靜態 IP 位址，您必須上 hello 子網路 hello NIC 連線到指定的未使用且有效地址。</span><span class="sxs-lookup"><span data-stu-id="f44cd-129">When adding a static IP address, you must specify an unused, valid address on hello subnet hello NIC is connected to.</span></span> <span data-ttu-id="f44cd-130">如果您選取的 hello 位址無法使用，hello 入口網站會顯示 X 代表 hello IP 位址，而您會需要 tooselect 另一部。</span><span class="sxs-lookup"><span data-stu-id="f44cd-130">If hello address you select is not available, hello portal will show an X for hello IP address and you'll need tooselect a different one.</span></span>

3. <span data-ttu-id="f44cd-131">一旦您按一下 [確定]，hello 刀鋒視窗會關閉，而您會看到 hello 列出新 IP 組態。</span><span class="sxs-lookup"><span data-stu-id="f44cd-131">Once you click OK, hello blade will close and you'll see hello new IP configuration listed.</span></span> <span data-ttu-id="f44cd-132">按一下**確定**tooclose hello**新增 IP 組態**刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="f44cd-132">Click **OK** tooclose hello **Add IP configuration** blade.</span></span>
4. <span data-ttu-id="f44cd-133">您可以按一下**新增**tooadd 額外的 IP 設定，或關閉所有開啟刀鋒視窗 toofinish 新增 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="f44cd-133">You can click **Add** tooadd additional IP configurations, or close all open blades toofinish adding IP addresses.</span></span>
5. <span data-ttu-id="f44cd-134">新增 hello 私人 IP 位址 toohello VM 作業系統 hello hello 作業系統的步驟，以[新增 IP 位址 tooa VM 作業系統](#os-config)本文一節。</span><span class="sxs-lookup"><span data-stu-id="f44cd-134">Add hello private IP addresses toohello VM operating system by completing hello steps for your operating system in hello [Add IP addresses tooa VM operating system](#os-config) section of this article.</span></span>

### <a name="add-a-public-ip-address"></a><span data-ttu-id="f44cd-135">新增公用 IP 位址</span><span class="sxs-lookup"><span data-stu-id="f44cd-135">Add a public IP address</span></span>

<span data-ttu-id="f44cd-136">公用 IP 位址是由新的 IP 設定或現有的 IP 組態關聯公用 IP 位址資源 tooeither 加入。</span><span class="sxs-lookup"><span data-stu-id="f44cd-136">A public IP address is added by associating a public IP address resource tooeither a new IP configuration or an existing IP configuration.</span></span>

> [!NOTE]
> <span data-ttu-id="f44cd-137">公用 IP 位址需要少許費用。</span><span class="sxs-lookup"><span data-stu-id="f44cd-137">Public IP addresses have a nominal fee.</span></span> <span data-ttu-id="f44cd-138">進一步瞭解 IP 位址定價，toolearn 讀取 hello [IP 位址定價](https://azure.microsoft.com/pricing/details/ip-addresses)頁面。</span><span class="sxs-lookup"><span data-stu-id="f44cd-138">toolearn more about IP address pricing, read hello [IP address pricing](https://azure.microsoft.com/pricing/details/ip-addresses) page.</span></span> <span data-ttu-id="f44cd-139">沒有可用的訂用帳戶中的公用 IP 位址限制 toohello 數目。</span><span class="sxs-lookup"><span data-stu-id="f44cd-139">There is a limit toohello number of public IP addresses that can be used in a subscription.</span></span> <span data-ttu-id="f44cd-140">深入了解 hello 限制、 讀取 hello toolearn [Azure 限制](../azure-subscription-service-limits.md#networking-limits)發行項。</span><span class="sxs-lookup"><span data-stu-id="f44cd-140">toolearn more about hello limits, read hello [Azure limits](../azure-subscription-service-limits.md#networking-limits) article.</span></span>
> 

### <span data-ttu-id="f44cd-141"><a name="create-public-ip"></a>建立公用 IP 位址資源</span><span class="sxs-lookup"><span data-stu-id="f44cd-141"><a name="create-public-ip"></a>Create a public IP address resource</span></span>

<span data-ttu-id="f44cd-142">公用 IP 位址是公用 IP 位址資源的其中一項設定</span><span class="sxs-lookup"><span data-stu-id="f44cd-142">A public IP address is one setting for a public IP address resource.</span></span> <span data-ttu-id="f44cd-143">如果您有不是您想要的目前關聯的 tooan IP 設定公用 IP 位址資源 tooassociate tooan IP 設定，就會略過下列步驟的 hello，並視需要完成 hello 以下各節，其中的 hello 步驟。</span><span class="sxs-lookup"><span data-stu-id="f44cd-143">If you have a public IP address resource that is not currently associated tooan IP configuration that you want tooassociate tooan IP configuration, skip hello following steps and complete hello steps in one of hello sections that follow, as you require.</span></span> <span data-ttu-id="f44cd-144">如果您沒有可用的公用 IP 位址資源，請完成下列其中一個步驟 toocreate hello:</span><span class="sxs-lookup"><span data-stu-id="f44cd-144">If you don't have an available public IP address resource, complete hello following steps toocreate one:</span></span>

1. <span data-ttu-id="f44cd-145">如有必要，請到其中，瀏 toohello 在 https://portal.azure.com 並登入 Azure 入口網站。</span><span class="sxs-lookup"><span data-stu-id="f44cd-145">Browse toohello Azure portal at https://portal.azure.com and sign into it, if necessary.</span></span>
3. <span data-ttu-id="f44cd-146">在 hello 入口網站中，按一下 **新增** > **網路** > **公用 IP 位址**。</span><span class="sxs-lookup"><span data-stu-id="f44cd-146">In hello portal, click **New** > **Networking** > **Public IP address**.</span></span>
4. <span data-ttu-id="f44cd-147">在 hello**建立公用 IP 位址**刀鋒視窗中，輸入**名稱**，選取**IP 位址指派**型別，**訂用帳戶**、**資源群組**，和**位置**，然後按一下 **建立**hello 下列圖片所示：</span><span class="sxs-lookup"><span data-stu-id="f44cd-147">In hello **Create public IP address** blade that appears, enter a **Name**, select an **IP address assignment** type, a **Subscription**, a **Resource group**, and a **Location**, then click **Create**, as shown in hello following picture:</span></span>

    ![建立公用 IP 位址資源](./media/virtual-network-multiple-ip-addresses-portal/figure5.png)

5. <span data-ttu-id="f44cd-149">完整的 hello 中 hello 以下各節 tooassociate hello 公用 IP 位址資源 tooan IP 組態的其中一個步驟。</span><span class="sxs-lookup"><span data-stu-id="f44cd-149">Complete hello steps in one of hello sections that follow tooassociate hello public IP address resource tooan IP configuration.</span></span>

#### <a name="associate-hello-public-ip-address-resource-tooa-new-ip-configuration"></a><span data-ttu-id="f44cd-150">關聯的 hello 公用 IP 位址資源 tooa 新的 IP 設定</span><span class="sxs-lookup"><span data-stu-id="f44cd-150">Associate hello public IP address resource tooa new IP configuration</span></span>

1. <span data-ttu-id="f44cd-151">完整的 hello 步驟 hello[核心步驟](#coreadd)本文一節。</span><span class="sxs-lookup"><span data-stu-id="f44cd-151">Complete hello steps in hello [Core steps](#coreadd) section of this article.</span></span>
2. <span data-ttu-id="f44cd-152">按一下 [新增] 。</span><span class="sxs-lookup"><span data-stu-id="f44cd-152">Click **Add**.</span></span> <span data-ttu-id="f44cd-153">在 hello**新增 IP 組態**刀鋒視窗中，建立名為 IP 設定*IPConfig 4*。</span><span class="sxs-lookup"><span data-stu-id="f44cd-153">In hello **Add IP configuration** blade that appears, create an IP configuration named *IPConfig-4*.</span></span> <span data-ttu-id="f44cd-154">啟用 hello**公用 IP 位址**選取現有的可用公用 IP 位址資源從 hello**選擇公用 IP 位址**刀鋒視窗中出現。</span><span class="sxs-lookup"><span data-stu-id="f44cd-154">Enable hello **Public IP address** and select an existing, available public IP address resource from hello **Choose public IP address** blade that appears.</span></span>

    <span data-ttu-id="f44cd-155">一旦您已選取 hello 公用 IP 位址資源，請按一下**確定**hello 刀鋒視窗會關閉。</span><span class="sxs-lookup"><span data-stu-id="f44cd-155">Once you've selected hello public IP address resource, click **OK** and hello blade will close.</span></span> <span data-ttu-id="f44cd-156">如果您沒有現有的公用 IP 位址，您可以建立一個 hello hello 中的步驟，以[建立公用 IP 位址資源](#create-public-ip)本文一節。</span><span class="sxs-lookup"><span data-stu-id="f44cd-156">If you don't have an existing public IP address, you can create one by completing hello steps in hello [Create a public IP address resource](#create-public-ip) section of this article.</span></span> 

3. <span data-ttu-id="f44cd-157">檢閱 hello 新的 IP 設定。</span><span class="sxs-lookup"><span data-stu-id="f44cd-157">Review hello new IP configuration.</span></span> <span data-ttu-id="f44cd-158">即使未明確指派私人 IP 位址，其中一個已自動指派 toohello IP 組態，因為所有的 IP 設定必須具有私人 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="f44cd-158">Even though a private IP address wasn't explicitly assigned, one was automatically assigned toohello IP configuration, because all IP configurations must have a private IP address.</span></span>
4. <span data-ttu-id="f44cd-159">您可以按一下**新增**tooadd 額外的 IP 設定，或關閉所有開啟刀鋒視窗 toofinish 新增 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="f44cd-159">You can click **Add** tooadd additional IP configurations, or close all open blades toofinish adding IP addresses.</span></span>
5. <span data-ttu-id="f44cd-160">完成您的作業系統中 hello hello 步驟新增 hello 私用 IP 位址 toohello VM 作業系統[新增 IP 位址 tooa VM 作業系統](#os-config)本文一節。</span><span class="sxs-lookup"><span data-stu-id="f44cd-160">Add hello private IP address toohello VM operating system by completing hello steps for your operating system in hello [Add IP addresses tooa VM operating system](#os-config) section of this article.</span></span> <span data-ttu-id="f44cd-161">請勿將 hello 公用 IP 位址 toohello 作業系統。</span><span class="sxs-lookup"><span data-stu-id="f44cd-161">Do not add hello public IP address toohello operating system.</span></span>

#### <a name="associate-hello-public-ip-address-resource-tooan-existing-ip-configuration"></a><span data-ttu-id="f44cd-162">關聯的 hello 公用 IP 位址資源 tooan 現有 IP 組態</span><span class="sxs-lookup"><span data-stu-id="f44cd-162">Associate hello public IP address resource tooan existing IP configuration</span></span>

1. <span data-ttu-id="f44cd-163">完整的 hello 步驟 hello[核心步驟](#coreadd)本文一節。</span><span class="sxs-lookup"><span data-stu-id="f44cd-163">Complete hello steps in hello [Core steps](#coreadd) section of this article.</span></span>
2. <span data-ttu-id="f44cd-164">按一下 您希望 tooadd hello 公用 IP 位址資源的 hello IP 組態。</span><span class="sxs-lookup"><span data-stu-id="f44cd-164">Click hello IP configuration you want tooadd hello public IP address resource to.</span></span>
3. <span data-ttu-id="f44cd-165">在 hello IPConfig 刀鋒視窗中顯示，按一下  **IP 位址**。</span><span class="sxs-lookup"><span data-stu-id="f44cd-165">In hello IPConfig blade that appears, click **IP address**.</span></span>
4. <span data-ttu-id="f44cd-166">在 hello**選擇公用 IP 位址**刀鋒視窗中，選取的公用 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="f44cd-166">In hello **Choose public IP address** blade that appears, select a public IP address.</span></span>
5. <span data-ttu-id="f44cd-167">按一下**儲存**hello 刀鋒視窗會關閉。</span><span class="sxs-lookup"><span data-stu-id="f44cd-167">Click **Save** and hello blades will close.</span></span> <span data-ttu-id="f44cd-168">如果您沒有現有的公用 IP 位址，您可以建立一個 hello hello 中的步驟，以[建立公用 IP 位址資源](#create-public-ip)本文一節。</span><span class="sxs-lookup"><span data-stu-id="f44cd-168">If you don't have an existing public IP address, you can create one by completing hello steps in hello [Create a public IP address resource](#create-public-ip) section of this article.</span></span>
3. <span data-ttu-id="f44cd-169">檢閱 hello 新的 IP 設定。</span><span class="sxs-lookup"><span data-stu-id="f44cd-169">Review hello new IP configuration.</span></span>
4. <span data-ttu-id="f44cd-170">您可以按一下**新增**tooadd 額外的 IP 設定，或關閉所有開啟刀鋒視窗 toofinish 新增 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="f44cd-170">You can click **Add** tooadd additional IP configurations, or close all open blades toofinish adding IP addresses.</span></span> <span data-ttu-id="f44cd-171">請勿將 hello 公用 IP 位址 toohello 作業系統。</span><span class="sxs-lookup"><span data-stu-id="f44cd-171">Do not add hello public IP address toohello operating system.</span></span>


[!INCLUDE [virtual-network-multiple-ip-addresses-os-config.md](../../includes/virtual-network-multiple-ip-addresses-os-config.md)]
