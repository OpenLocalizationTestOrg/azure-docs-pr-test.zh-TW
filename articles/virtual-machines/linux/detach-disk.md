---
title: "從 Linux VM-Azure 資料磁碟 aaaDetach |Microsoft 文件"
description: "了解 toodetach 從虛擬機器使用 CLI 2.0 或 hello Azure 入口網站在 Azure 中的資料磁碟。"
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
ms.openlocfilehash: 1c6145fc97f13179457225e93e0fb7adc261a65b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="how-toodetach-a-data-disk-from-a-linux-virtual-machine"></a><span data-ttu-id="7279b-103">Toodetach 資料從 Linux 虛擬機器的磁碟</span><span class="sxs-lookup"><span data-stu-id="7279b-103">How toodetach a data disk from a Linux virtual machine</span></span>

<span data-ttu-id="7279b-104">當您不再需要的資料磁碟附加的 tooa 虛擬機器時，您可以輕易地中斷。</span><span class="sxs-lookup"><span data-stu-id="7279b-104">When you no longer need a data disk that's attached tooa virtual machine, you can easily detach it.</span></span> <span data-ttu-id="7279b-105">這會從 hello 虛擬機器，移除 hello 磁碟，但並不會移除從儲存體。</span><span class="sxs-lookup"><span data-stu-id="7279b-105">This removes hello disk from hello virtual machine, but doesn't remove it from storage.</span></span> 

> [!WARNING]
> <span data-ttu-id="7279b-106">將磁碟中斷連結時，並不會自動將它刪除。</span><span class="sxs-lookup"><span data-stu-id="7279b-106">If you detach a disk it is not automatically deleted.</span></span> <span data-ttu-id="7279b-107">如果您已訂閱 tooPremium 儲存體，您將繼續 tooincur hello 磁碟的儲存體費用。</span><span class="sxs-lookup"><span data-stu-id="7279b-107">If you have subscribed tooPremium storage, you will continue tooincur storage charges for hello disk.</span></span> <span data-ttu-id="7279b-108">如需詳細資訊，請參閱太[定價和計費時使用進階儲存體](../../storage/common/storage-premium-storage.md#pricing-and-billing)。</span><span class="sxs-lookup"><span data-stu-id="7279b-108">For more information refer too[Pricing and Billing when using Premium Storage](../../storage/common/storage-premium-storage.md#pricing-and-billing).</span></span> 
> 
> 

<span data-ttu-id="7279b-109">若要再次 toouse hello 現有資料 hello 磁碟上的，您可以將它重新附加 toohello 相同的虛擬機器或另一個。</span><span class="sxs-lookup"><span data-stu-id="7279b-109">If you want toouse hello existing data on hello disk again, you can reattach it toohello same virtual machine, or another one.</span></span>  

## <a name="detach-a-data-disk-using-cli-20"></a><span data-ttu-id="7279b-110">使用 CLI 2.0 中斷資料磁碟連結</span><span class="sxs-lookup"><span data-stu-id="7279b-110">Detach a data disk using CLI 2.0</span></span>

```azurecli
az vm disk detach -g myResourceGroup --vm-name myVm -n myDataDisk
```

<span data-ttu-id="7279b-111">hello 磁碟留在儲存體，但已不再附加的 tooa 虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="7279b-111">hello disk remains in storage but is no longer attached tooa virtual machine.</span></span>


## <a name="detach-a-data-disk-using-hello-portal"></a><span data-ttu-id="7279b-112">卸離資料磁碟使用 hello 入口網站</span><span class="sxs-lookup"><span data-stu-id="7279b-112">Detach a data disk using hello portal</span></span>
1. <span data-ttu-id="7279b-113">在 hello 入口網站的中樞，選取 **虛擬機器**。</span><span class="sxs-lookup"><span data-stu-id="7279b-113">In hello portal hub, select **Virtual Machines**.</span></span>
2. <span data-ttu-id="7279b-114">選取 hello hello toodetach 然後按一下資料磁碟的虛擬機器**停止**toodeallocate hello VM。</span><span class="sxs-lookup"><span data-stu-id="7279b-114">Select hello virtual machine that has hello data disk you want toodetach and click **Stop** toodeallocate hello VM.</span></span>
3. <span data-ttu-id="7279b-115">在 hello 虛擬機器刀鋒視窗中，選取 **磁碟**。</span><span class="sxs-lookup"><span data-stu-id="7279b-115">In hello virtual machine blade, select **Disks**.</span></span>
4. <span data-ttu-id="7279b-116">頂端的 hello hello**磁碟**刀鋒視窗中，選取**編輯**。</span><span class="sxs-lookup"><span data-stu-id="7279b-116">At hello top of hello **Disks** blade, select **Edit**.</span></span>
5. <span data-ttu-id="7279b-117">在 [hello**磁碟**刀鋒視窗中，最右邊的 hello 資料磁碟，您想 toodetach，toohello 按一下 hello![卸離按鈕影像](./media/detach-disk/detach.png)卸離] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="7279b-117">In hello **Disks** blade, toohello far right of hello data disk that you would like toodetach, click hello ![Detach button image](./media/detach-disk/detach.png) detach button.</span></span>
5. <span data-ttu-id="7279b-118">Hello 磁碟已被移除後，按一下 [儲存] hello hello 刀鋒視窗的頂端。</span><span class="sxs-lookup"><span data-stu-id="7279b-118">After hello disk has been removed, click Save on hello top of hello blade.</span></span>
6. <span data-ttu-id="7279b-119">在 hello 虛擬機器刀鋒視窗中，按一下 **概觀**然後按一下hello**啟動**在 hello 刀鋒視窗 toorestart hello VM hello 最上方的按鈕。</span><span class="sxs-lookup"><span data-stu-id="7279b-119">In hello virtual machine blade, click **Overview** and then click hello **Start** button at hello top of hello blade toorestart hello VM.</span></span>

<span data-ttu-id="7279b-120">hello 磁碟留在儲存體，但已不再附加的 tooa 虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="7279b-120">hello disk remains in storage but is no longer attached tooa virtual machine.</span></span>








## <a name="next-steps"></a><span data-ttu-id="7279b-121">後續步驟</span><span class="sxs-lookup"><span data-stu-id="7279b-121">Next steps</span></span>
<span data-ttu-id="7279b-122">如果您想 tooreuse hello 資料磁碟時，您可以直接[將它附加 tooanother VM](add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="7279b-122">If you want tooreuse hello data disk, you can just [attach it tooanother VM](add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

