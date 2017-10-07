---
title: "aaaHow tooreset 網路介面，讓 Windows Azure VM 與 |Microsoft 文件"
description: "示範如何 tooreset Azure Windows VM 的網路介面"
services: virtual-machines-windows, azure-resource-manager
documentationcenter: 
author: genlin
manager: willchen
editor: 
tags: top-support-issue, azure-resource-manager
ms.service: virtual-machines-windows
ms.workload: na
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 06/26/2017
ms.author: genli
ms.openlocfilehash: 1b653820927ef4c3bb8f384a7e752846a8be3da9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooreset-network-interface-for-azure-windows-vm"></a><span data-ttu-id="ab7b6-103">如何 tooreset Azure Windows VM 的網路介面</span><span class="sxs-lookup"><span data-stu-id="ab7b6-103">How tooreset network interface for Azure Windows VM</span></span> 

[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-both-include.md)]

<span data-ttu-id="ab7b6-104">無法連線 tooMicrosoft Azure Windows 虛擬機器 (VM)，停用 hello 預設網路介面 (NIC) 之後，或是手動設定靜態 ip 位址的 hello nic。</span><span class="sxs-lookup"><span data-stu-id="ab7b6-104">You cannot connect tooMicrosoft Azure Windows Virtual Machine (VM) after you disable hello default Network Interface (NIC) or manually sets a static IP for hello NIC.</span></span> <span data-ttu-id="ab7b6-105">本文將說明如何 tooreset hello Azure Windows vm，將會解決 hello 遠端連線問題的網路介面。</span><span class="sxs-lookup"><span data-stu-id="ab7b6-105">This article shows how tooreset hello network interface for Azure Windows VM, which will resolve hello remote connection issue.</span></span>

[!INCLUDE [support-disclaimer](../../../includes/support-disclaimer.md)]
## <a name="reset-network-interface"></a><span data-ttu-id="ab7b6-106">重設網路介面</span><span class="sxs-lookup"><span data-stu-id="ab7b6-106">Reset network interface</span></span>

### <a name="for-classic-vms"></a><span data-ttu-id="ab7b6-107">適用於傳統 VM</span><span class="sxs-lookup"><span data-stu-id="ab7b6-107">For Classic VMs</span></span>

<span data-ttu-id="ab7b6-108">tooreset 網路介面，依照下列步驟：</span><span class="sxs-lookup"><span data-stu-id="ab7b6-108">tooreset network interface, follow these steps:</span></span>

1.  <span data-ttu-id="ab7b6-109">移 toohello [Azure 入口網站]( https://ms.portal.azure.com)。</span><span class="sxs-lookup"><span data-stu-id="ab7b6-109">Go toohello [Azure portal]( https://ms.portal.azure.com).</span></span>
2.  <span data-ttu-id="ab7b6-110">選取 [虛擬機器 (傳統)]。</span><span class="sxs-lookup"><span data-stu-id="ab7b6-110">Select **Virtual Machines (Classic)**.</span></span>
3.  <span data-ttu-id="ab7b6-111">選取 hello 影響虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="ab7b6-111">Select hello affected Virtual Machine.</span></span>
4.  <span data-ttu-id="ab7b6-112">選取 [IP 位址]。</span><span class="sxs-lookup"><span data-stu-id="ab7b6-112">Select **IP addresses**.</span></span>
5.  <span data-ttu-id="ab7b6-113">如果 hello**私用 IP 指派**不**靜態**，將它變更太**靜態**。</span><span class="sxs-lookup"><span data-stu-id="ab7b6-113">If hello **Private IP assignment**  is not  **Static**, change it too**Static**.</span></span>
6.  <span data-ttu-id="ab7b6-114">變更 hello **IP 位址**tooanother hello 子網路中可用的 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="ab7b6-114">Change hello **IP address** tooanother IP address that is available in hello Subnet.</span></span>
7.  <span data-ttu-id="ab7b6-115">選取 [儲存]。</span><span class="sxs-lookup"><span data-stu-id="ab7b6-115">Select Save.</span></span>
8.  <span data-ttu-id="ab7b6-116">hello 虛擬機器會重新啟動 tooinitialize hello 新 NIC toohello 系統。</span><span class="sxs-lookup"><span data-stu-id="ab7b6-116">hello virtual machine will restart tooinitialize hello new NIC toohello system.</span></span>
9.  <span data-ttu-id="ab7b6-117">請嘗試 tooRDP tooyour 機器。</span><span class="sxs-lookup"><span data-stu-id="ab7b6-117">Try tooRDP tooyour machine.</span></span> <span data-ttu-id="ab7b6-118">如果成功的話，您可以變更 hello 私人 IP 位址後 toohello 原始，如果您想要。</span><span class="sxs-lookup"><span data-stu-id="ab7b6-118">If successful, you can change hello Private IP address back toohello original if you would like.</span></span> <span data-ttu-id="ab7b6-119">或是維持現有設定。</span><span class="sxs-lookup"><span data-stu-id="ab7b6-119">Otherwise, you can keep it.</span></span> 

### <a name="for-vms-deployed-in-resource-group-model"></a><span data-ttu-id="ab7b6-120">適用於部署在資源群組模型中的 VM</span><span class="sxs-lookup"><span data-stu-id="ab7b6-120">For VMs deployed in Resource group model</span></span>

1.  <span data-ttu-id="ab7b6-121">移 toohello [Azure 入口網站]( https://ms.portal.azure.com)。</span><span class="sxs-lookup"><span data-stu-id="ab7b6-121">Go toohello [Azure portal]( https://ms.portal.azure.com).</span></span>
2.  <span data-ttu-id="ab7b6-122">選取 hello 影響虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="ab7b6-122">Select hello affected Virtual Machine.</span></span>
3.  <span data-ttu-id="ab7b6-123">選取 [網路介面]。</span><span class="sxs-lookup"><span data-stu-id="ab7b6-123">Select **Network Interfaces**.</span></span>
4.  <span data-ttu-id="ab7b6-124">選取與您的電腦的網路介面相關聯的 hello</span><span class="sxs-lookup"><span data-stu-id="ab7b6-124">Select hello Network Interface associated with your machine</span></span>
5.  <span data-ttu-id="ab7b6-125">選取 [IP 組態]。</span><span class="sxs-lookup"><span data-stu-id="ab7b6-125">Select **IP configurations**.</span></span>
6.  <span data-ttu-id="ab7b6-126">選取 hello IP。</span><span class="sxs-lookup"><span data-stu-id="ab7b6-126">Select hello IP.</span></span> 
7.  <span data-ttu-id="ab7b6-127">如果 hello**私用 IP 指派**不**靜態**，將它變更太**靜態**。</span><span class="sxs-lookup"><span data-stu-id="ab7b6-127">If hello **Private IP assignment**  is not  **Static**, change it too**Static**.</span></span>
8.  <span data-ttu-id="ab7b6-128">變更 hello **IP 位址**tooanother hello 子網路中可用的 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="ab7b6-128">Change hello **IP address** tooanother IP address that is available in hello Subnet.</span></span>
9. <span data-ttu-id="ab7b6-129">hello 虛擬機器會重新啟動 tooinitialize hello 新 NIC toohello 系統。</span><span class="sxs-lookup"><span data-stu-id="ab7b6-129">hello virtual machine will restart tooinitialize hello new NIC toohello system.</span></span>
10. <span data-ttu-id="ab7b6-130">請嘗試 tooRDP tooyour 機器。</span><span class="sxs-lookup"><span data-stu-id="ab7b6-130">Try tooRDP tooyour machine.</span></span> <span data-ttu-id="ab7b6-131">如果成功的話，您可以變更 hello 私人 IP 位址後 toohello 原始，如果您想要。</span><span class="sxs-lookup"><span data-stu-id="ab7b6-131">If successful, you can change hello Private IP address back toohello original if you would like.</span></span> <span data-ttu-id="ab7b6-132">或是維持現有設定。</span><span class="sxs-lookup"><span data-stu-id="ab7b6-132">Otherwise, you can keep it.</span></span> 

## <a name="delete-hello-unavailable-nics"></a><span data-ttu-id="ab7b6-133">刪除 hello 無法使用 Nic</span><span class="sxs-lookup"><span data-stu-id="ab7b6-133">Delete hello unavailable NICs</span></span>
<span data-ttu-id="ab7b6-134">您可以遠端桌面 toohello 機器之後，您必須刪除 hello 舊 Nic tooavoid hello 潛在的問題：</span><span class="sxs-lookup"><span data-stu-id="ab7b6-134">After you can remote desktop toohello machine, you must delete hello old NICs tooavoid hello potential problem:</span></span>

1.  <span data-ttu-id="ab7b6-135">開啟 [裝置管理員]。</span><span class="sxs-lookup"><span data-stu-id="ab7b6-135">Open Device Manager.</span></span>
2.  <span data-ttu-id="ab7b6-136">選取 [檢視] > [顯示隱藏的裝置]。</span><span class="sxs-lookup"><span data-stu-id="ab7b6-136">Select **View** > **Show hidden devices**.</span></span>
3.  <span data-ttu-id="ab7b6-137">選取 [網路介面卡]。</span><span class="sxs-lookup"><span data-stu-id="ab7b6-137">Select **Network Adapters**.</span></span> 
4.  <span data-ttu-id="ab7b6-138">檢查名為"Microsoft HYPER-V 網路介面卡 」 的 hello 配接器。</span><span class="sxs-lookup"><span data-stu-id="ab7b6-138">Check for hello adapters named as "Microsoft Hyper-V Network Adapter".</span></span>
5.  <span data-ttu-id="ab7b6-139">無法使用的介面卡會以灰色來顯示。以滑鼠右鍵按一下 hello 配接器，然後選取 解除安裝。</span><span class="sxs-lookup"><span data-stu-id="ab7b6-139">You might see an unavailable adapter that is grayed out. Right-click hello adapter and then select Uninstall.</span></span>

    ![hello NIC hello 映像](media/reset-network-interface/nicpage.png)

    > [!NOTE]
    > <span data-ttu-id="ab7b6-141">只解除安裝具有 hello 名稱"Microsoft HYPER-V 網路介面卡 」 的 hello 無法使用配接器。</span><span class="sxs-lookup"><span data-stu-id="ab7b6-141">Only uninstall hello unavailable adapters that have hello name "Microsoft Hyper-V Network Adapter".</span></span> <span data-ttu-id="ab7b6-142">如果您解除安裝任何 hello 其他隱藏的配接器，它可能會導致其他問題。</span><span class="sxs-lookup"><span data-stu-id="ab7b6-142">If you uninstall any of hello other hidden adapters, it could cause additional issues.</span></span>
    >
    >

6.  <span data-ttu-id="ab7b6-143">現在應該已經從系統清除所有無法使用的介面卡。</span><span class="sxs-lookup"><span data-stu-id="ab7b6-143">Now all unavailable adapter should be cleared out from your system.</span></span>