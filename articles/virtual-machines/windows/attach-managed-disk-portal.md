---
title: "受管理的資料磁碟 tooa Windows VM-Azure aaaAttach |Microsoft 文件"
description: "如何 tooattach 新受管理的資料磁碟 tooa hello Azure 入口網站中，使用中的 Windows VM hello Resource Manager 部署模型。"
services: virtual-machines-windows
documentationcenter: 
author: cynthn
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 05/09/2017
ms.author: cynthn
ms.openlocfilehash: bacc0589ad2d93e4d3d055c8f837f8db27291ead
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooattach-a-managed-data-disk-tooa-windows-vm-in-hello-azure-portal"></a><span data-ttu-id="670eb-103">Tooattach 受管理的資料磁碟 tooa Windows VM hello Azure 入口網站中的方式</span><span class="sxs-lookup"><span data-stu-id="670eb-103">How tooattach a managed data disk tooa Windows VM in hello Azure portal</span></span>

<span data-ttu-id="670eb-104">本文章將示範如何 tooattach 新的 managed 資料磁碟 tooWindows 透過 hello Azure 入口網站的虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="670eb-104">This article shows you how tooattach a new managed data disk tooWindows virtual machines through hello Azure portal.</span></span> <span data-ttu-id="670eb-105">這麼做之前，請先檢閱下列提示：</span><span class="sxs-lookup"><span data-stu-id="670eb-105">Before you do this, review these tips:</span></span>

* <span data-ttu-id="670eb-106">hello hello 虛擬機器大小會控制您可以將附加的資料磁碟數目。</span><span class="sxs-lookup"><span data-stu-id="670eb-106">hello size of hello virtual machine controls how many data disks you can attach.</span></span> <span data-ttu-id="670eb-107">如需詳細資訊，請參閱 [虛擬機器的大小](sizes.md)。</span><span class="sxs-lookup"><span data-stu-id="670eb-107">For details, see [Sizes for virtual machines](sizes.md).</span></span>
* <span data-ttu-id="670eb-108">對於新的磁碟，您不需要 toocreate 它第一次因為 Azure 會建立它時將它附加。</span><span class="sxs-lookup"><span data-stu-id="670eb-108">For a new disk, you don't need toocreate it first because Azure creates it when you attach it.</span></span>

<span data-ttu-id="670eb-109">您也可以[使用 Powershell 連接資料磁碟](attach-disk-ps.md)。</span><span class="sxs-lookup"><span data-stu-id="670eb-109">You can also [attach a data disk using Powershell](attach-disk-ps.md).</span></span>



## <a name="add-a-data-disk"></a><span data-ttu-id="670eb-110">新增資料磁碟</span><span class="sxs-lookup"><span data-stu-id="670eb-110">Add a data disk</span></span>
1. <span data-ttu-id="670eb-111">在左側 hello hello 功能表上，按一下**虛擬機器**。</span><span class="sxs-lookup"><span data-stu-id="670eb-111">In hello menu on hello left, click **Virtual Machines**.</span></span>
2. <span data-ttu-id="670eb-112">從 [hello] 清單中選取 hello 虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="670eb-112">Select hello virtual machine from hello list.</span></span>
3. <span data-ttu-id="670eb-113">在 hello 虛擬機器刀鋒視窗中，按一下 **磁碟**。</span><span class="sxs-lookup"><span data-stu-id="670eb-113">On hello virtual machine blade, click **Disks**.</span></span>
   4. <span data-ttu-id="670eb-114">在 hello**磁碟**刀鋒視窗中，按一下  **+ 新增資料磁碟**。</span><span class="sxs-lookup"><span data-stu-id="670eb-114">On hello **Disks** blade, click **+ Add data disk**.</span></span>
5. <span data-ttu-id="670eb-115">在 hello hello 新磁碟的下拉式清單中，選取 **建立空白**。</span><span class="sxs-lookup"><span data-stu-id="670eb-115">In hello drop-down for hello new disk, select **Create empty**.</span></span>
6. <span data-ttu-id="670eb-116">在 hello**建立受管理的磁碟**刀鋒視窗中，輸入 hello 磁碟的名稱，然後調整視 hello 其他設定。</span><span class="sxs-lookup"><span data-stu-id="670eb-116">In hello **Create managed disk** blade, type in a name for hello disk and adjust hello other settings as necessary.</span></span> <span data-ttu-id="670eb-117">完成之後，請按一下 [建立]。</span><span class="sxs-lookup"><span data-stu-id="670eb-117">When you are done, click **Create**.</span></span>
7. <span data-ttu-id="670eb-118">在 hello**磁碟**刀鋒視窗中，按一下 儲存 toosave hello 新磁碟設定的 hello VM。</span><span class="sxs-lookup"><span data-stu-id="670eb-118">In hello **Disks** blade, click save toosave hello new disk configuration for hello VM.</span></span>
6. <span data-ttu-id="670eb-119">Azure 會建立 hello 磁碟，並將其附加 toohello 虛擬機器之後下, hello 虛擬機器的磁碟設定 中列為 hello 新磁碟**資料磁碟**。</span><span class="sxs-lookup"><span data-stu-id="670eb-119">After Azure creates hello disk and attaches it toohello virtual machine, hello new disk is listed in hello virtual machine's disk settings under **Data Disks**.</span></span>


## <a name="initialize-a-new-data-disk"></a><span data-ttu-id="670eb-120">初始化新的資料磁碟</span><span class="sxs-lookup"><span data-stu-id="670eb-120">Initialize a new data disk</span></span>

1. <span data-ttu-id="670eb-121">連接 toohello VM。</span><span class="sxs-lookup"><span data-stu-id="670eb-121">Connect toohello VM.</span></span>
1. <span data-ttu-id="670eb-122">按一下 hello VM 內 hello 開始 功能表及類型**diskmgmt.msc**並點擊**Enter**。</span><span class="sxs-lookup"><span data-stu-id="670eb-122">Click hello start menu inside hello VM and type **diskmgmt.msc** and hit **Enter**.</span></span> <span data-ttu-id="670eb-123">這會啟動 hello 磁碟管理嵌入式管理單元。</span><span class="sxs-lookup"><span data-stu-id="670eb-123">This will start hello Disk Management snap-in.</span></span>
2. <span data-ttu-id="670eb-124">磁碟管理會辨識您有新的、 未初始化的磁碟，並 hello 初始化磁碟 視窗會隨即快顯。</span><span class="sxs-lookup"><span data-stu-id="670eb-124">Disk Management will recognize that you have a new, un-initialized disk and hello Initialize Disk window will pop up.</span></span>
3. <span data-ttu-id="670eb-125">請確定已選取 hello 新磁碟，然後按一下**確定**tooinitialize 它。</span><span class="sxs-lookup"><span data-stu-id="670eb-125">Make sure hello new disk is selected and click **OK** tooinitialize it.</span></span>
4. <span data-ttu-id="670eb-126">hello 新磁碟現在會顯示為**未配置**。</span><span class="sxs-lookup"><span data-stu-id="670eb-126">hello new disk will now appear as **unallocated**.</span></span> <span data-ttu-id="670eb-127">Hello 磁碟上按一下滑鼠右鍵，然後選取**新增簡單磁碟區**。</span><span class="sxs-lookup"><span data-stu-id="670eb-127">Right-click anywhere on hello disk and select **New simple volume**.</span></span> <span data-ttu-id="670eb-128">hello**新增簡單磁碟區精靈**會啟動。</span><span class="sxs-lookup"><span data-stu-id="670eb-128">hello **New Simple Volume Wizard** will start.</span></span>
5. <span data-ttu-id="670eb-129">透過 hello 」 精靈，將所有 hello 預設值，當您完成選取移**完成**。</span><span class="sxs-lookup"><span data-stu-id="670eb-129">Go through hello wizard, keeping all of hello defaults, when you are done select **Finish**.</span></span>
6. <span data-ttu-id="670eb-130">關閉磁碟管理。</span><span class="sxs-lookup"><span data-stu-id="670eb-130">Close Disk Management.</span></span>
7. <span data-ttu-id="670eb-131">您將會得到快顯視窗，您可以使用它之前，需要 tooformat hello 新磁碟。</span><span class="sxs-lookup"><span data-stu-id="670eb-131">You will get a pop-up that you need tooformat hello new disk before you can use it.</span></span> <span data-ttu-id="670eb-132">按一下 [格式化磁碟]。</span><span class="sxs-lookup"><span data-stu-id="670eb-132">Click **Format disk**.</span></span>
8. <span data-ttu-id="670eb-133">在 hello**格式新磁碟**對話方塊檢查 hello 設定，然後按一下**啟動**。</span><span class="sxs-lookup"><span data-stu-id="670eb-133">In hello **Format new disk** dialog, check hello settings and then click **Start**.</span></span>
9. <span data-ttu-id="670eb-134">您會收到警告，格式化 hello 磁碟將會清除所有 hello 資料中，按一下 **確定**。</span><span class="sxs-lookup"><span data-stu-id="670eb-134">You will get a warning that formatting hello disks will erase all of hello data, click **OK**.</span></span>
10. <span data-ttu-id="670eb-135">完成 hello 格式時，按一下**確定**。</span><span class="sxs-lookup"><span data-stu-id="670eb-135">When hello format is complete, click **OK**.</span></span>

## <a name="use-trim-with-standard-storage"></a><span data-ttu-id="670eb-136">搭配使用 TRIM 與標準儲存體</span><span class="sxs-lookup"><span data-stu-id="670eb-136">Use TRIM with standard storage</span></span>

<span data-ttu-id="670eb-137">如果您使用標準儲存體 (HDD)，您應該啟用 TRIM。</span><span class="sxs-lookup"><span data-stu-id="670eb-137">If you use standard storage (HDD), you should enable TRIM.</span></span> <span data-ttu-id="670eb-138">空白位置修剪會捨棄 hello 磁碟上未使用的區塊，因此您只支付您實際使用的儲存體。</span><span class="sxs-lookup"><span data-stu-id="670eb-138">TRIM discards unused blocks on hello disk so you are only billed for storage that you are actually using.</span></span> <span data-ttu-id="670eb-139">如果您建立大型檔案，然後將它們刪除，這便可節省成本。</span><span class="sxs-lookup"><span data-stu-id="670eb-139">This can save on costs if you create large files and then delete them.</span></span> 

<span data-ttu-id="670eb-140">您可以執行此命令 toocheck hello 修剪設定。</span><span class="sxs-lookup"><span data-stu-id="670eb-140">You can run this command toocheck hello TRIM setting.</span></span> <span data-ttu-id="670eb-141">在您的 Windows VM 上開啟命令提示字元並輸入︰</span><span class="sxs-lookup"><span data-stu-id="670eb-141">Open a command prompt on your Windows VM and type:</span></span>

```
fsutil behavior query DisableDeleteNotify
```

<span data-ttu-id="670eb-142">Hello 命令傳回 0，如果已正確啟用修剪。</span><span class="sxs-lookup"><span data-stu-id="670eb-142">If hello command returns 0, TRIM is enabled correctly.</span></span> <span data-ttu-id="670eb-143">如果它傳回 1，執行下列命令 tooenable TRIM hello:</span><span class="sxs-lookup"><span data-stu-id="670eb-143">If it returns 1, run hello following command tooenable TRIM:</span></span>
```
fsutil behavior set DisableDeleteNotify 0
```

<span data-ttu-id="670eb-144">從磁碟中刪除資料之後, 您就可以確保 hello 修剪作業排清正確藉由執行磁碟重組與修剪：</span><span class="sxs-lookup"><span data-stu-id="670eb-144">After deleting data from your disk, you can ensure hello TRIM operations flush properly by running defrag with TRIM:</span></span>

```
defrag.exe <volume:> -l
```

<span data-ttu-id="670eb-145">您也可以確保修剪 hello 整個磁碟區格式化 hello 磁碟區。</span><span class="sxs-lookup"><span data-stu-id="670eb-145">You can also ensure hello entire volume is trimmed by formatting hello volume.</span></span>

## <a name="next-steps"></a><span data-ttu-id="670eb-146">後續步驟</span><span class="sxs-lookup"><span data-stu-id="670eb-146">Next steps</span></span>
<span data-ttu-id="670eb-147">如果您的應用程式需要 toouse hello d： 磁碟機 toostore 資料時，您可以[變更 hello hello Windows 暫存磁碟的磁碟機代號](change-drive-letter.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="670eb-147">If you application needs toouse hello D: drive toostore data, you can [change hello drive letter of hello Windows temporary disk](change-drive-letter.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span></span>
