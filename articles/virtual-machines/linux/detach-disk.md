---
title: "從 Linux VM 中斷資料磁碟連結 | Microsoft Docs"
description: "了解如何使用 CLI 2.0 或 Azure 入口網站，從 Azure 中的虛擬機器中斷資料磁碟連結。"
services: virtual-machines-linux
documentationcenter: 
author: cynthn
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: 
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: azurecli
ms.topic: article
ms.date: 03/21/2017
ms.author: cynthn
ms.openlocfilehash: 3f29547e1da6028b1e4b91d9e29fd3bcdfe08d50
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="how-to-detach-a-data-disk-from-a-linux-virtual-machine"></a><span data-ttu-id="c7b22-103">如何從 Linux 虛擬機器中斷資料磁碟連結</span><span class="sxs-lookup"><span data-stu-id="c7b22-103">How to detach a data disk from a Linux virtual machine</span></span>

<span data-ttu-id="c7b22-104">當不再需要某個連接至虛擬機器的資料磁碟時，卸離此資料磁碟很簡單。</span><span class="sxs-lookup"><span data-stu-id="c7b22-104">When you no longer need a data disk that's attached to a virtual machine, you can easily detach it.</span></span> <span data-ttu-id="c7b22-105">這會將磁碟從虛擬機器中卸離，但這不會將它從儲存體中移除。</span><span class="sxs-lookup"><span data-stu-id="c7b22-105">This removes the disk from the virtual machine, but doesn't remove it from storage.</span></span> 

> [!WARNING]
> <span data-ttu-id="c7b22-106">將磁碟中斷連結時，並不會自動將它刪除。</span><span class="sxs-lookup"><span data-stu-id="c7b22-106">If you detach a disk it is not automatically deleted.</span></span> <span data-ttu-id="c7b22-107">如果您已訂閱「進階」儲存體，您將會繼續因該磁碟而導致產生儲存體費用。</span><span class="sxs-lookup"><span data-stu-id="c7b22-107">If you have subscribed to Premium storage, you will continue to incur storage charges for the disk.</span></span> <span data-ttu-id="c7b22-108">如需詳細資訊，請參閱 [使用進階儲存體時的價格和計費](../../storage/common/storage-premium-storage.md#pricing-and-billing)。</span><span class="sxs-lookup"><span data-stu-id="c7b22-108">For more information refer to [Pricing and Billing when using Premium Storage](../../storage/common/storage-premium-storage.md#pricing-and-billing).</span></span> 
> 
> 

<span data-ttu-id="c7b22-109">如果您想要再次使用磁碟上現有的資料，您可以將磁碟重新連接至相同或其他虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="c7b22-109">If you want to use the existing data on the disk again, you can reattach it to the same virtual machine, or another one.</span></span>  

## <a name="detach-a-data-disk-using-cli-20"></a><span data-ttu-id="c7b22-110">使用 CLI 2.0 中斷資料磁碟連結</span><span class="sxs-lookup"><span data-stu-id="c7b22-110">Detach a data disk using CLI 2.0</span></span>

```azurecli
az vm disk detach -g myResourceGroup --vm-name myVm -n myDataDisk
```

<span data-ttu-id="c7b22-111">磁碟仍留在儲存體中，但不再連接至虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="c7b22-111">The disk remains in storage but is no longer attached to a virtual machine.</span></span>


## <a name="detach-a-data-disk-using-the-portal"></a><span data-ttu-id="c7b22-112">使用入口網站來中斷資料磁碟連結</span><span class="sxs-lookup"><span data-stu-id="c7b22-112">Detach a data disk using the portal</span></span>
1. <span data-ttu-id="c7b22-113">在入口網站中樞中，選取 [虛擬機器] 。</span><span class="sxs-lookup"><span data-stu-id="c7b22-113">In the portal hub, select **Virtual Machines**.</span></span>
2. <span data-ttu-id="c7b22-114">選取含有您想要中斷連結之資料磁碟的虛擬機器，然後按一下 [停止] 以解除配置該 VM。</span><span class="sxs-lookup"><span data-stu-id="c7b22-114">Select the virtual machine that has the data disk you want to detach and click **Stop** to deallocate the VM.</span></span>
3. <span data-ttu-id="c7b22-115">在 [虛擬機器] 刀鋒視窗中，選取 [磁碟]。</span><span class="sxs-lookup"><span data-stu-id="c7b22-115">In the virtual machine blade, select **Disks**.</span></span>
4. <span data-ttu-id="c7b22-116">在 [磁碟] 刀鋒視窗頂端，選取 [編輯]。</span><span class="sxs-lookup"><span data-stu-id="c7b22-116">At the top of the **Disks** blade, select **Edit**.</span></span>
5. <span data-ttu-id="c7b22-117">在 [磁碟] 刀鋒視窗中，在您想要中斷連結的資料磁碟最右側，按一下 ![中斷連結按鈕影像](./media/detach-disk/detach.png) 中斷連結按鈕。</span><span class="sxs-lookup"><span data-stu-id="c7b22-117">In the **Disks** blade, to the far right of the data disk that you would like to detach, click the ![Detach button image](./media/detach-disk/detach.png) detach button.</span></span>
5. <span data-ttu-id="c7b22-118">移除磁碟之後，按一下刀鋒視窗頂端的 [儲存]。</span><span class="sxs-lookup"><span data-stu-id="c7b22-118">After the disk has been removed, click Save on the top of the blade.</span></span>
6. <span data-ttu-id="c7b22-119">在 [虛擬機器] 刀鋒視窗中，按一下 [概觀]，然後按一下刀鋒視窗頂端的 [啟動] 按鈕以重新啟動 VM。</span><span class="sxs-lookup"><span data-stu-id="c7b22-119">In the virtual machine blade, click **Overview** and then click the **Start** button at the top of the blade to restart the VM.</span></span>

<span data-ttu-id="c7b22-120">磁碟仍留在儲存體中，但不再連接至虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="c7b22-120">The disk remains in storage but is no longer attached to a virtual machine.</span></span>








## <a name="next-steps"></a><span data-ttu-id="c7b22-121">後續步驟</span><span class="sxs-lookup"><span data-stu-id="c7b22-121">Next steps</span></span>
<span data-ttu-id="c7b22-122">如果您想要重複使用該資料磁碟，只要[將它連結至另一個 VM](add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="c7b22-122">If you want to reuse the data disk, you can just [attach it to another VM](add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

