---
title: "aaaAttach 磁碟 tooa 傳統 Azure VM |Microsoft 文件"
description: "連接資料磁碟 tooa 建立 Windows 虛擬機器與 hello 傳統部署模型，然後將它初始化。"
services: virtual-machines-windows, storage
documentationcenter: 
author: cynthn
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: be4e3e74-05bc-4527-969f-84f10a1d66a7
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 02/21/2017
ms.author: cynthn
ms.openlocfilehash: bfe1b0fa066277d28d3862a18da4b1023cb4452d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="attach-a-data-disk-tooa-windows-virtual-machine-created-with-hello-classic-deployment-model"></a><span data-ttu-id="8ea9e-103">附加資料磁碟 tooa 建立 Windows 虛擬機器與 hello 傳統部署模型</span><span class="sxs-lookup"><span data-stu-id="8ea9e-103">Attach a data disk tooa Windows virtual machine created with hello classic deployment model</span></span>
<!--
Refernce article:
    If you want toouse hello new portal, see [How tooattach a data disk tooa Windows VM in hello Azure portal](../../virtual-machines-windows-attach-disk-portal.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).
-->

<span data-ttu-id="8ea9e-104">本文章將示範如何 tooattach 新的和現有磁碟建立 hello 傳統部署模型 tooa Windows 虛擬機器使用 hello Azure 入口網站。</span><span class="sxs-lookup"><span data-stu-id="8ea9e-104">This article shows you how tooattach new and existing disks created with hello Classic deployment model tooa Windows virtual machine using hello Azure portal.</span></span>

<span data-ttu-id="8ea9e-105">您也可以[附加 hello Azure 入口網站中的資料磁碟 tooa Linux VM](../../linux/attach-disk-portal.md)。</span><span class="sxs-lookup"><span data-stu-id="8ea9e-105">You can also [attach a data disk tooa Linux VM in hello Azure portal](../../linux/attach-disk-portal.md).</span></span>

<span data-ttu-id="8ea9e-106">連接磁碟之前，請檢閱下列提示︰</span><span class="sxs-lookup"><span data-stu-id="8ea9e-106">Before you attach a disk, review these tips:</span></span>

* <span data-ttu-id="8ea9e-107">hello hello 虛擬機器大小會控制您可以將附加的資料磁碟數目。</span><span class="sxs-lookup"><span data-stu-id="8ea9e-107">hello size of hello virtual machine controls how many data disks you can attach.</span></span> <span data-ttu-id="8ea9e-108">如需詳細資訊，請參閱 [虛擬機器的大小](../../virtual-machines-windows-sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="8ea9e-108">For details, see [Sizes for virtual machines](../../virtual-machines-windows-sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

* <span data-ttu-id="8ea9e-109">toouse 高階儲存體，您需要將 DS 系列或 GS 系列虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="8ea9e-109">toouse Premium storage, you need a DS-series or GS-series virtual machine.</span></span> <span data-ttu-id="8ea9e-110">您可以使用進階或標準儲存體帳戶的磁碟搭配這些虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="8ea9e-110">You can use disks from both Premium and Standard storage accounts with these virtual machines.</span></span> <span data-ttu-id="8ea9e-111">僅特定地區可用進階儲存體。</span><span class="sxs-lookup"><span data-stu-id="8ea9e-111">Premium storage is available in certain regions.</span></span> <span data-ttu-id="8ea9e-112">如需詳細資訊，請參閱[進階儲存體：Azure 虛擬機器工作負載適用的高效能儲存體](../../../storage/common/storage-premium-storage.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="8ea9e-112">For details, see [Premium Storage: High-Performance Storage for Azure Virtual Machine Workloads](../../../storage/common/storage-premium-storage.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

* <span data-ttu-id="8ea9e-113">對於新的磁碟，您不需要 toocreate 它第一次因為 Azure 會建立它時將它附加。</span><span class="sxs-lookup"><span data-stu-id="8ea9e-113">For a new disk, you don't need toocreate it first because Azure creates it when you attach it.</span></span>

<span data-ttu-id="8ea9e-114">您也可以[使用 Powershell 連接資料磁碟](../../virtual-machines-windows-attach-disk-ps.md)。</span><span class="sxs-lookup"><span data-stu-id="8ea9e-114">You can also [attach a data disk using Powershell](../../virtual-machines-windows-attach-disk-ps.md).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="8ea9e-115">Azure 建立和處理資源的部署模型有二種： [資源管理員和傳統](../../../resource-manager-deployment-model.md)。</span><span class="sxs-lookup"><span data-stu-id="8ea9e-115">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../resource-manager-deployment-model.md).</span></span>

## <a name="find-hello-virtual-machine"></a><span data-ttu-id="8ea9e-116">尋找 hello 虛擬機器</span><span class="sxs-lookup"><span data-stu-id="8ea9e-116">Find hello virtual machine</span></span>
1. <span data-ttu-id="8ea9e-117">登入 toohello [Azure 入口網站](https://portal.azure.com/)。</span><span class="sxs-lookup"><span data-stu-id="8ea9e-117">Sign in toohello [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="8ea9e-118">選取 hello hello 儀表板上所列的 hello 資源從虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="8ea9e-118">Select hello virtual machine from hello resource listed on hello dashboard.</span></span>
3. <span data-ttu-id="8ea9e-119">Hello 下的左窗格中**設定**，按一下 **磁碟**。</span><span class="sxs-lookup"><span data-stu-id="8ea9e-119">In hello left pane under **Settings**, click **Disks**.</span></span>

    ![開啟磁碟設定](./media/attach-disk/virtualmachinedisks.png)

<span data-ttu-id="8ea9e-121">接著，依照指示來連接[新的磁碟](#option-1-attach-a-new-disk)或[現有的磁碟](#option-2-attach-an-existing-disk)。</span><span class="sxs-lookup"><span data-stu-id="8ea9e-121">Continue by following instructions for attaching either a [new disk](#option-1-attach-a-new-disk) or an [existing disk](#option-2-attach-an-existing-disk).</span></span>

## <a name="option-1-attach-and-initialize-a-new-disk"></a><span data-ttu-id="8ea9e-122">選項 1：連接新磁碟並進行初始化</span><span class="sxs-lookup"><span data-stu-id="8ea9e-122">Option 1: Attach and initialize a new disk</span></span>

1. <span data-ttu-id="8ea9e-123">在 hello**磁碟**刀鋒視窗中，按一下 **附加新**。</span><span class="sxs-lookup"><span data-stu-id="8ea9e-123">On hello **Disks** blade, click **Attach new**.</span></span>
2. <span data-ttu-id="8ea9e-124">檢閱 hello 預設設定，如有必要，更新，然後按一下**確定**。</span><span class="sxs-lookup"><span data-stu-id="8ea9e-124">Review hello default settings, update as necessary, and then click **OK**.</span></span>

   ![檢閱磁碟設定](./media/attach-disk/attach-new.png)

3. <span data-ttu-id="8ea9e-126">Azure 會建立 hello 磁碟，並將其附加 toohello 虛擬機器之後下, hello 虛擬機器的磁碟設定 中列為 hello 新磁碟**資料磁碟**。</span><span class="sxs-lookup"><span data-stu-id="8ea9e-126">After Azure creates hello disk and attaches it toohello virtual machine, hello new disk is listed in hello virtual machine's disk settings under **Data Disks**.</span></span>

### <a name="initialize-a-new-data-disk"></a><span data-ttu-id="8ea9e-127">初始化新的資料磁碟</span><span class="sxs-lookup"><span data-stu-id="8ea9e-127">Initialize a new data disk</span></span>

1. <span data-ttu-id="8ea9e-128">Toohello 虛擬機器連線。</span><span class="sxs-lookup"><span data-stu-id="8ea9e-128">Connect toohello virtual machine.</span></span> <span data-ttu-id="8ea9e-129">如需指示，請參閱[如何 tooconnect 和登入 tooan Azure 虛擬機器執行 Windows](../../virtual-machines-windows-connect-logon.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="8ea9e-129">For instructions, see [How tooconnect and log on tooan Azure virtual machine running Windows](../../virtual-machines-windows-connect-logon.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>
2. <span data-ttu-id="8ea9e-130">您登入 toohello 虛擬機器之後，請開啟**伺服器管理員**。</span><span class="sxs-lookup"><span data-stu-id="8ea9e-130">After you log on toohello virtual machine, open **Server Manager**.</span></span> <span data-ttu-id="8ea9e-131">Hello 左窗格中，選取**檔案和存放服務**。</span><span class="sxs-lookup"><span data-stu-id="8ea9e-131">In hello left pane, select **File and Storage Services**.</span></span>

    ![開啟伺服器管理員](../media/attach-disk-portal/fileandstorageservices.png)

3. <span data-ttu-id="8ea9e-133">選取 [磁碟]。</span><span class="sxs-lookup"><span data-stu-id="8ea9e-133">Select **Disks**.</span></span>
4. <span data-ttu-id="8ea9e-134">hello**磁碟**區段會列出 hello 磁碟。</span><span class="sxs-lookup"><span data-stu-id="8ea9e-134">hello **Disks** section lists hello disks.</span></span> <span data-ttu-id="8ea9e-135">多數情況下，虛擬機器會有磁碟 0、磁碟 1 和磁碟 2。</span><span class="sxs-lookup"><span data-stu-id="8ea9e-135">Most often, a virtual machine has disk 0, disk 1, and disk 2.</span></span> <span data-ttu-id="8ea9e-136">磁碟 0 是 hello 作業系統磁碟、 磁碟 1 是 hello 暫存磁碟，以及磁碟 2 是新 hello 資料磁碟連接的 toohello 虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="8ea9e-136">Disk 0 is hello operating system disk, disk 1 is hello temporary disk, and disk 2 is hello data disk newly attached toohello virtual machine.</span></span> <span data-ttu-id="8ea9e-137">hello 資料磁碟清單 hello 與磁碟分割**未知**。</span><span class="sxs-lookup"><span data-stu-id="8ea9e-137">hello data disk lists hello Partition as **Unknown**.</span></span>

 <span data-ttu-id="8ea9e-138">Hello 磁碟上按一下滑鼠右鍵，然後選取**初始化**。</span><span class="sxs-lookup"><span data-stu-id="8ea9e-138">Right-click hello disk and select **Initialize**.</span></span>

5. <span data-ttu-id="8ea9e-139">您收到 hello 磁碟初始化時，將被清除所有資料。</span><span class="sxs-lookup"><span data-stu-id="8ea9e-139">You're notified that all data will be erased when hello disk is initialized.</span></span> <span data-ttu-id="8ea9e-140">按一下**是**tooacknowledge hello 警告和初始化 hello 磁碟。</span><span class="sxs-lookup"><span data-stu-id="8ea9e-140">Click **Yes** tooacknowledge hello warning and initialize hello disk.</span></span> <span data-ttu-id="8ea9e-141">Hello partition 完成後，會被列為**GPT**。</span><span class="sxs-lookup"><span data-stu-id="8ea9e-141">Once complete, hello partition will be listed as **GPT**.</span></span> <span data-ttu-id="8ea9e-142">Hello 磁碟上按一下滑鼠右鍵，然後選取**新的磁碟區**。</span><span class="sxs-lookup"><span data-stu-id="8ea9e-142">Right-click hello disk again and select **New Volume**.</span></span>

6. <span data-ttu-id="8ea9e-143">完成 hello 精靈使用 hello 預設值。</span><span class="sxs-lookup"><span data-stu-id="8ea9e-143">Complete hello wizard using hello default values.</span></span> <span data-ttu-id="8ea9e-144">當 hello 精靈完成時，hello**磁碟區**區段會列出 hello 新磁碟區。</span><span class="sxs-lookup"><span data-stu-id="8ea9e-144">When hello wizard is done, hello **Volumes** section lists hello new volume.</span></span> <span data-ttu-id="8ea9e-145">hello 磁碟現在已上線並備妥 toostore 資料。</span><span class="sxs-lookup"><span data-stu-id="8ea9e-145">hello disk is now online and ready toostore data.</span></span>

    ![成功初始化磁碟區](./media/attach-disk/newdiskafterinitialization.png)

## <a name="option-2-attach-an-existing-disk"></a><span data-ttu-id="8ea9e-147">選項 2：連接現有磁碟</span><span class="sxs-lookup"><span data-stu-id="8ea9e-147">Option 2: Attach an existing disk</span></span>
1. <span data-ttu-id="8ea9e-148">在 hello**磁碟**刀鋒視窗中，按一下 **附加現有**。</span><span class="sxs-lookup"><span data-stu-id="8ea9e-148">On hello **Disks** blade, click **Attach existing**.</span></span>
2. <span data-ttu-id="8ea9e-149">在 [連接現有磁碟] 底下，按一下 [位置]。</span><span class="sxs-lookup"><span data-stu-id="8ea9e-149">Under **Attach existing disk**, click **Location**.</span></span>

   ![連接現有磁碟](./media/attach-disk/attachexistingdisksettings.png)
3. <span data-ttu-id="8ea9e-151">在下**儲存體帳戶**，選取 hello 帳戶和容器，其中含有 hello.vhd 檔案。</span><span class="sxs-lookup"><span data-stu-id="8ea9e-151">Under **Storage accounts**, select hello account and container that holds hello .vhd file.</span></span>

   ![尋找 VHD 位置](./media/attach-disk/existdiskstorageaccountandcontainer.png)

4. <span data-ttu-id="8ea9e-153">選取 hello.vhd 檔案。</span><span class="sxs-lookup"><span data-stu-id="8ea9e-153">Select hello .vhd file.</span></span>
5. <span data-ttu-id="8ea9e-154">在下**將現有磁碟**，您只選取的 hello 檔案列在**VHD 檔案**。</span><span class="sxs-lookup"><span data-stu-id="8ea9e-154">Under **Attach existing disk**, hello file you just selected is listed under **VHD File**.</span></span> <span data-ttu-id="8ea9e-155">按一下 [確定] 。</span><span class="sxs-lookup"><span data-stu-id="8ea9e-155">Click **OK**.</span></span>
6. <span data-ttu-id="8ea9e-156">Azure 將 hello 磁碟 toohello 虛擬機器之後，它會列在下方的 hello 虛擬機器的磁碟設定**資料磁碟**。</span><span class="sxs-lookup"><span data-stu-id="8ea9e-156">After Azure attaches hello disk toohello virtual machine, it's listed in hello virtual machine's disk settings under **Data Disks**.</span></span>

## <a name="use-trim-with-standard-storage"></a><span data-ttu-id="8ea9e-157">搭配使用 TRIM 與標準儲存體</span><span class="sxs-lookup"><span data-stu-id="8ea9e-157">Use TRIM with standard storage</span></span>

<span data-ttu-id="8ea9e-158">如果您使用標準儲存體 (HDD)，您應該啟用 TRIM。</span><span class="sxs-lookup"><span data-stu-id="8ea9e-158">If you use standard storage (HDD), you should enable TRIM.</span></span> <span data-ttu-id="8ea9e-159">空白位置修剪會捨棄 hello 磁碟上未使用的區塊，因此您只支付您實際使用的儲存體。</span><span class="sxs-lookup"><span data-stu-id="8ea9e-159">TRIM discards unused blocks on hello disk so you are only billed for storage that you are actually using.</span></span> <span data-ttu-id="8ea9e-160">使用 TRIM 可以節省成本，包括刪除大型檔案時所產生的未使用區塊。</span><span class="sxs-lookup"><span data-stu-id="8ea9e-160">Using TRIM can save costs, including unused blocks that result from deleting large files.</span></span>

<span data-ttu-id="8ea9e-161">您可以執行此命令 toocheck hello 修剪設定。</span><span class="sxs-lookup"><span data-stu-id="8ea9e-161">You can run this command toocheck hello TRIM setting.</span></span> <span data-ttu-id="8ea9e-162">在您的 Windows VM 上開啟命令提示字元並輸入︰</span><span class="sxs-lookup"><span data-stu-id="8ea9e-162">Open a command prompt on your Windows VM and type:</span></span>

```
fsutil behavior query DisableDeleteNotify
```

<span data-ttu-id="8ea9e-163">Hello 命令傳回 0，如果已正確啟用修剪。</span><span class="sxs-lookup"><span data-stu-id="8ea9e-163">If hello command returns 0, TRIM is enabled correctly.</span></span> <span data-ttu-id="8ea9e-164">如果它傳回 1，執行下列命令 tooenable TRIM hello:</span><span class="sxs-lookup"><span data-stu-id="8ea9e-164">If it returns 1, run hello following command tooenable TRIM:</span></span>
```
fsutil behavior set DisableDeleteNotify 0
```

## <a name="next-steps"></a><span data-ttu-id="8ea9e-165">後續步驟</span><span class="sxs-lookup"><span data-stu-id="8ea9e-165">Next steps</span></span>
<span data-ttu-id="8ea9e-166">如果您的應用程式需要 toouse hello d： 磁碟機 toostore 資料時，您可以[變更 hello hello Windows 暫存磁碟的磁碟機代號](../../virtual-machines-windows-change-drive-letter.md)。</span><span class="sxs-lookup"><span data-stu-id="8ea9e-166">If your application needs toouse hello D: drive toostore data, you can [change hello drive letter of hello Windows temporary disk](../../virtual-machines-windows-change-drive-letter.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="8ea9e-167">其他資源</span><span class="sxs-lookup"><span data-stu-id="8ea9e-167">Additional resources</span></span>
[<span data-ttu-id="8ea9e-168">有關虛擬機器的磁碟和 VHD</span><span class="sxs-lookup"><span data-stu-id="8ea9e-168">About disks and VHDs for virtual machines</span></span>](../../virtual-machines-linux-about-disks-vhds.md)
