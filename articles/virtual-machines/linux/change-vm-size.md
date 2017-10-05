---
title: "如何使用 Azure CLI 2.0 來調整 Linux VM 大小 | Microsoft Docs"
description: "如何藉由變更 VM 的大小來相應增加或相應減少 Linux 虛擬機器。"
services: virtual-machines-linux
documentationcenter: na
author: mikewasson
manager: timlt
editor: 
tags: 
ms.assetid: e163f878-b919-45c5-9f5a-75a64f3b14a0
ms.service: virtual-machines-linux
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/10/2017
ms.author: mwasson
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 23fc9f7f34732079682857d4ee685fe811751698
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="resize-a-linux-virtual-machine-using-cli-20"></a><span data-ttu-id="43450-103">使用 CLI 2.0 來調整 Linux 虛擬機器大小</span><span class="sxs-lookup"><span data-stu-id="43450-103">Resize a Linux virtual machine using CLI 2.0</span></span>

<span data-ttu-id="43450-104">部屬虛擬機器 (VM) 之後，您可以藉由變更 [VM 大小][vm-sizes]來相應增加或減少 VM。</span><span class="sxs-lookup"><span data-stu-id="43450-104">After you provision a virtual machine (VM), you can scale the VM up or down by changing the [VM size][vm-sizes].</span></span> <span data-ttu-id="43450-105">在某些情況下，您必須先解除配置 VM。</span><span class="sxs-lookup"><span data-stu-id="43450-105">In some cases, you must deallocate the VM first.</span></span> <span data-ttu-id="43450-106">如果無法在裝載 VM 的硬體叢集上取得所需的大小，您可能需要解除配置 VM。</span><span class="sxs-lookup"><span data-stu-id="43450-106">You need to deallocate the VM if the desired size is not available on the hardware cluster that is hosting the VM.</span></span> <span data-ttu-id="43450-107">本文詳述如何使用 Azure CLI 2.0 來調整 Linux VM 的大小。</span><span class="sxs-lookup"><span data-stu-id="43450-107">This article details how to resize a Linux VM with the Azure CLI 2.0.</span></span> <span data-ttu-id="43450-108">您也可以使用 [Azure CLI 1.0](change-vm-size-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) 來執行這些步驟。</span><span class="sxs-lookup"><span data-stu-id="43450-108">You can also perform these steps with the [Azure CLI 1.0](change-vm-size-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

## <a name="resize-a-vm"></a><span data-ttu-id="43450-109">調整 VM 的大小</span><span class="sxs-lookup"><span data-stu-id="43450-109">Resize a VM</span></span>
<span data-ttu-id="43450-110">若要調整 VM 的大小，您需要安裝最新的 [Azure CLI 2.0](/cli/azure/install-az-cli2)，並使用 [az login](/cli/azure/#login) 來登入 Azure 帳戶。</span><span class="sxs-lookup"><span data-stu-id="43450-110">To resize a VM, you need the latest [Azure CLI 2.0](/cli/azure/install-az-cli2) installed and logged in to an Azure account using [az login](/cli/azure/#login).</span></span>

1. <span data-ttu-id="43450-111">使用 [az vm list-vm-resize-options](/cli/azure/vm#list-vm-resize-options) 檢視裝載 VM 之硬體叢集上可用的 VM 大小清單。</span><span class="sxs-lookup"><span data-stu-id="43450-111">View the list of available VM sizes on the hardware cluster where the VM is hosted with [az vm list-vm-resize-options](/cli/azure/vm#list-vm-resize-options).</span></span> <span data-ttu-id="43450-112">下列範例會針對資源群組 `myResourceGroup` 區域中名為 `myVM` 的 VM 列出 VM 大小：</span><span class="sxs-lookup"><span data-stu-id="43450-112">The following example lists VM sizes for the VM named `myVM` in the resource group `myResourceGroup` region:</span></span>
   
    ```azurecli
    az vm list-vm-resize-options --resource-group myResourceGroup --name myVM --output table
    ```

2. <span data-ttu-id="43450-113">如果已列出所需的大小，請使用 [az vm resize](/cli/azure/vm#resize) 來調整 VM 的大小。</span><span class="sxs-lookup"><span data-stu-id="43450-113">If the desired VM size is listed, resize the VM with [az vm resize](/cli/azure/vm#resize).</span></span> <span data-ttu-id="43450-114">下列範例會將名為 `myVM` 的 VM 大小調整為 `Standard_DS3_v2` 大小：</span><span class="sxs-lookup"><span data-stu-id="43450-114">The following example resizes the VM named `myVM` to the `Standard_DS3_v2` size:</span></span>
   
    ```azurecli
    az vm resize --resource-group myResourceGroup --name myVM --size Standard_DS3_v2
    ```
   
    <span data-ttu-id="43450-115">VM 會在此程序中重新啟動。</span><span class="sxs-lookup"><span data-stu-id="43450-115">The VM restarts during this process.</span></span> <span data-ttu-id="43450-116">重新啟動之後，會重新對應現有的 OS 和資料磁碟。</span><span class="sxs-lookup"><span data-stu-id="43450-116">After the restart, your existing OS and data disks are remapped.</span></span> <span data-ttu-id="43450-117">暫存磁碟的相關資料都會遺失。</span><span class="sxs-lookup"><span data-stu-id="43450-117">Anything on the temporary disk is lost.</span></span>

3. <span data-ttu-id="43450-118">如果未列出所需的 VM 大小，您需要先使用 [az vm deallocate](/cli/azure/vm#deallocate) 解除配置 VM。</span><span class="sxs-lookup"><span data-stu-id="43450-118">If the desired VM size is not listed, you need to first deallocate the VM with [az vm deallocate](/cli/azure/vm#deallocate).</span></span> <span data-ttu-id="43450-119">此程序可讓 VM 的大小調整為區域支援的任何可用大小，然後啟動。</span><span class="sxs-lookup"><span data-stu-id="43450-119">This process allows the VM to then be resized to any size available that the region supports and then started.</span></span> <span data-ttu-id="43450-120">下列步驟會解除配置、調整大小，然後啟動 `myResourceGroup` 資源群組中名為 `myVM` 的 VM：</span><span class="sxs-lookup"><span data-stu-id="43450-120">The following steps deallocate, resize, and then start the VM named `myVM` in the resource group named `myResourceGroup`:</span></span>
   
    ```azurecli
    az vm deallocate --resource-group myResourceGroup --name myVM
    az vm resize --resource-group myResourceGroup --name myVM --size Standard_DS3_v2
    az vm start --resource-group myResourceGroup --name myVM
    ```
   
   > [!WARNING]
   > <span data-ttu-id="43450-121">將 VM 解除配置也會釋出指派給該 VM 的任何動態 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="43450-121">Deallocating the VM also releases any dynamic IP addresses assigned to the VM.</span></span> <span data-ttu-id="43450-122">不會影響作業系統和資料磁碟。</span><span class="sxs-lookup"><span data-stu-id="43450-122">The OS and data disks are not affected.</span></span>

## <a name="next-steps"></a><span data-ttu-id="43450-123">後續步驟</span><span class="sxs-lookup"><span data-stu-id="43450-123">Next steps</span></span>
<span data-ttu-id="43450-124">如需提高延展性，可執行多個 VM 執行個體並相應放大。</span><span class="sxs-lookup"><span data-stu-id="43450-124">For additional scalability, run multiple VM instances and scale out.</span></span> <span data-ttu-id="43450-125">如需詳細資訊，請參閱[在虛擬機器擴展集中自動調整 Linux 機器][scale-set]。</span><span class="sxs-lookup"><span data-stu-id="43450-125">For more information, see [Automatically scale Linux machines in a Virtual Machine Scale Set][scale-set].</span></span> 

<!-- links -->
[boot-diagnostics]: https://azure.microsoft.com/en-us/blog/boot-diagnostics-for-virtual-machines-v2/
[scale-set]: ../../virtual-machine-scale-sets/virtual-machine-scale-sets-linux-autoscale.md 
[vm-sizes]:sizes.md
