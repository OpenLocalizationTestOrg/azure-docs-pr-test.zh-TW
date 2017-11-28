---
title: "aaaHow tooresize Linux VM 以 hello Azure CLI 2.0 |Microsoft 文件"
description: "如何 tooscale 向上或向下 Linux 虛擬機器，藉由變更調整 hello VM 大小。"
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
ms.openlocfilehash: e8fba485b5bcc7824f546de5cf3df77624a28008
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="resize-a-linux-virtual-machine-using-cli-20"></a><span data-ttu-id="61a1c-103">使用 CLI 2.0 來調整 Linux 虛擬機器大小</span><span class="sxs-lookup"><span data-stu-id="61a1c-103">Resize a Linux virtual machine using CLI 2.0</span></span>

<span data-ttu-id="61a1c-104">佈建虛擬機器 (VM) 之後，您可以調整 hello VM 向上或向下藉由變更 hello [VM 大小][vm-sizes]。</span><span class="sxs-lookup"><span data-stu-id="61a1c-104">After you provision a virtual machine (VM), you can scale hello VM up or down by changing hello [VM size][vm-sizes].</span></span> <span data-ttu-id="61a1c-105">在某些情況下，您必須先取消配置 hello VM。</span><span class="sxs-lookup"><span data-stu-id="61a1c-105">In some cases, you must deallocate hello VM first.</span></span> <span data-ttu-id="61a1c-106">您需要 toodeallocate hello VM，視 hello 大小不是在裝載 hello VM hello 硬體叢集上使用。</span><span class="sxs-lookup"><span data-stu-id="61a1c-106">You need toodeallocate hello VM if hello desired size is not available on hello hardware cluster that is hosting hello VM.</span></span> <span data-ttu-id="61a1c-107">這篇文章說明如何使用 Linux VM 的 tooresize hello Azure CLI 2.0。</span><span class="sxs-lookup"><span data-stu-id="61a1c-107">This article details how tooresize a Linux VM with hello Azure CLI 2.0.</span></span> <span data-ttu-id="61a1c-108">您也可以執行下列步驟以 hello [Azure CLI 1.0](change-vm-size-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="61a1c-108">You can also perform these steps with hello [Azure CLI 1.0](change-vm-size-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

## <a name="resize-a-vm"></a><span data-ttu-id="61a1c-109">調整 VM 的大小</span><span class="sxs-lookup"><span data-stu-id="61a1c-109">Resize a VM</span></span>
<span data-ttu-id="61a1c-110">tooresize VM，您需要 hello 最新[Azure CLI 2.0](/cli/azure/install-az-cli2)安裝並登入 tooan Azure 帳戶使用[az 登入](/cli/azure/#login)。</span><span class="sxs-lookup"><span data-stu-id="61a1c-110">tooresize a VM, you need hello latest [Azure CLI 2.0](/cli/azure/install-az-cli2) installed and logged in tooan Azure account using [az login](/cli/azure/#login).</span></span>

1. <span data-ttu-id="61a1c-111">檢視 hello 清單可用的 VM 大小與 hello VM 裝載的 hello 硬體叢集上[az vm 清單-vm-調整大小的選項](/cli/azure/vm#list-vm-resize-options)。</span><span class="sxs-lookup"><span data-stu-id="61a1c-111">View hello list of available VM sizes on hello hardware cluster where hello VM is hosted with [az vm list-vm-resize-options](/cli/azure/vm#list-vm-resize-options).</span></span> <span data-ttu-id="61a1c-112">hello 下列範例會列出 hello 名為 VM 的 VM 大小`myVM`hello 資源群組中`myResourceGroup`區域：</span><span class="sxs-lookup"><span data-stu-id="61a1c-112">hello following example lists VM sizes for hello VM named `myVM` in hello resource group `myResourceGroup` region:</span></span>
   
    ```azurecli
    az vm list-vm-resize-options --resource-group myResourceGroup --name myVM --output table
    ```

2. <span data-ttu-id="61a1c-113">如果 hello 想要列出 VM 大小，調整大小 hello 與 VM [az vm 調整](/cli/azure/vm#resize)。</span><span class="sxs-lookup"><span data-stu-id="61a1c-113">If hello desired VM size is listed, resize hello VM with [az vm resize](/cli/azure/vm#resize).</span></span> <span data-ttu-id="61a1c-114">下列範例會調整大小的 hello hello 名為 VM `myVM` toohello`Standard_DS3_v2`大小：</span><span class="sxs-lookup"><span data-stu-id="61a1c-114">hello following example resizes hello VM named `myVM` toohello `Standard_DS3_v2` size:</span></span>
   
    ```azurecli
    az vm resize --resource-group myResourceGroup --name myVM --size Standard_DS3_v2
    ```
   
    <span data-ttu-id="61a1c-115">hello VM 重新啟動此程序期間。</span><span class="sxs-lookup"><span data-stu-id="61a1c-115">hello VM restarts during this process.</span></span> <span data-ttu-id="61a1c-116">Hello 重新啟動之後，會重新對應您現有的作業系統和資料磁碟。</span><span class="sxs-lookup"><span data-stu-id="61a1c-116">After hello restart, your existing OS and data disks are remapped.</span></span> <span data-ttu-id="61a1c-117">Hello 暫存磁碟的任何項目將會遺失。</span><span class="sxs-lookup"><span data-stu-id="61a1c-117">Anything on hello temporary disk is lost.</span></span>

3. <span data-ttu-id="61a1c-118">視 hello 未列出的 VM 大小，您需要 toofirst 解除配置 hello 與 VM [az vm 解除配置](/cli/azure/vm#deallocate)。</span><span class="sxs-lookup"><span data-stu-id="61a1c-118">If hello desired VM size is not listed, you need toofirst deallocate hello VM with [az vm deallocate](/cli/azure/vm#deallocate).</span></span> <span data-ttu-id="61a1c-119">此程序可讓 hello VM toothen 可調整大小的 tooany 可用大小 hello 區域支援，然後啟動。</span><span class="sxs-lookup"><span data-stu-id="61a1c-119">This process allows hello VM toothen be resized tooany size available that hello region supports and then started.</span></span> <span data-ttu-id="61a1c-120">hello 下列步驟解除配置、 調整大小，並再啟動 hello 名為 VM `myVM` hello 資源群組中名為`myResourceGroup`:</span><span class="sxs-lookup"><span data-stu-id="61a1c-120">hello following steps deallocate, resize, and then start hello VM named `myVM` in hello resource group named `myResourceGroup`:</span></span>
   
    ```azurecli
    az vm deallocate --resource-group myResourceGroup --name myVM
    az vm resize --resource-group myResourceGroup --name myVM --size Standard_DS3_v2
    az vm start --resource-group myResourceGroup --name myVM
    ```
   
   > [!WARNING]
   > <span data-ttu-id="61a1c-121">解除配置 hello VM 也會釋放指派 toohello VM 的任何動態 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="61a1c-121">Deallocating hello VM also releases any dynamic IP addresses assigned toohello VM.</span></span> <span data-ttu-id="61a1c-122">不會影響 hello OS 和資料磁碟。</span><span class="sxs-lookup"><span data-stu-id="61a1c-122">hello OS and data disks are not affected.</span></span>

## <a name="next-steps"></a><span data-ttu-id="61a1c-123">後續步驟</span><span class="sxs-lookup"><span data-stu-id="61a1c-123">Next steps</span></span>
<span data-ttu-id="61a1c-124">如需提高延展性，可執行多個 VM 執行個體並相應放大。如需詳細資訊，請參閱[在虛擬機器擴展集中自動調整 Linux 機器][scale-set]。</span><span class="sxs-lookup"><span data-stu-id="61a1c-124">For additional scalability, run multiple VM instances and scale out. For more information, see [Automatically scale Linux machines in a Virtual Machine Scale Set][scale-set].</span></span> 

<!-- links -->
[boot-diagnostics]: https://azure.microsoft.com/en-us/blog/boot-diagnostics-for-virtual-machines-v2/
[scale-set]: ../../virtual-machine-scale-sets/virtual-machine-scale-sets-linux-autoscale.md 
[vm-sizes]:sizes.md
