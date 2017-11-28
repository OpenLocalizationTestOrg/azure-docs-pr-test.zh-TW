---
title: "將磁碟連接到傳統 Azure VM | Microsoft Docs"
description: "將資料磁碟連接到以傳統部署模型建立的 Windows 虛擬機器，並予以初始化。"
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
ms.openlocfilehash: 087d5cda354f6e1780bddd3725859444177abd16
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="attach-a-data-disk-to-a-windows-virtual-machine-created-with-the-classic-deployment-model"></a><span data-ttu-id="944b0-103">將資料磁碟連接至以傳統部署模型建立的 Windows 虛擬機器</span><span class="sxs-lookup"><span data-stu-id="944b0-103">Attach a data disk to a Windows virtual machine created with the classic deployment model</span></span>
<!--
Refernce article:
    If you want to use the new portal, see [How to attach a data disk to a Windows VM in the Azure portal](../../virtual-machines-windows-attach-disk-portal.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).
-->

<span data-ttu-id="944b0-104">本文會示範如何使用 Azure 入口網站將傳統部署模型所建立之新的及現有的磁碟連接到 Windows 虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="944b0-104">This article shows you how to attach new and existing disks created with the Classic deployment model to a Windows virtual machine using the Azure portal.</span></span>

<span data-ttu-id="944b0-105">您也可以[在 Azure 入口網站中將資料磁碟連接到 Linux VM](../../linux/attach-disk-portal.md)。</span><span class="sxs-lookup"><span data-stu-id="944b0-105">You can also [attach a data disk to a Linux VM in the Azure portal](../../linux/attach-disk-portal.md).</span></span>

<span data-ttu-id="944b0-106">連接磁碟之前，請檢閱下列提示︰</span><span class="sxs-lookup"><span data-stu-id="944b0-106">Before you attach a disk, review these tips:</span></span>

* <span data-ttu-id="944b0-107">虛擬機器的大小會控制您可以連接的資料磁碟數目。</span><span class="sxs-lookup"><span data-stu-id="944b0-107">The size of the virtual machine controls how many data disks you can attach.</span></span> <span data-ttu-id="944b0-108">如需詳細資訊，請參閱 [虛擬機器的大小](../../virtual-machines-windows-sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="944b0-108">For details, see [Sizes for virtual machines](../../virtual-machines-windows-sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

* <span data-ttu-id="944b0-109">若要使用進階儲存體，您需要 DS 系列或 GS 系列的虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="944b0-109">To use Premium storage, you need a DS-series or GS-series virtual machine.</span></span> <span data-ttu-id="944b0-110">您可以使用進階或標準儲存體帳戶的磁碟搭配這些虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="944b0-110">You can use disks from both Premium and Standard storage accounts with these virtual machines.</span></span> <span data-ttu-id="944b0-111">僅特定地區可用進階儲存體。</span><span class="sxs-lookup"><span data-stu-id="944b0-111">Premium storage is available in certain regions.</span></span> <span data-ttu-id="944b0-112">如需詳細資訊，請參閱[進階儲存體：Azure 虛擬機器工作負載適用的高效能儲存體](../../../storage/common/storage-premium-storage.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="944b0-112">For details, see [Premium Storage: High-Performance Storage for Azure Virtual Machine Workloads](../../../storage/common/storage-premium-storage.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

* <span data-ttu-id="944b0-113">對於新的磁碟，當您連接的時候 Azure 會建立該磁碟，所以您不需要建立它。</span><span class="sxs-lookup"><span data-stu-id="944b0-113">For a new disk, you don't need to create it first because Azure creates it when you attach it.</span></span>

<span data-ttu-id="944b0-114">您也可以[使用 Powershell 連接資料磁碟](../../virtual-machines-windows-attach-disk-ps.md)。</span><span class="sxs-lookup"><span data-stu-id="944b0-114">You can also [attach a data disk using Powershell](../../virtual-machines-windows-attach-disk-ps.md).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="944b0-115">Azure 建立和處理資源的部署模型有二種： [Resource Manager 和傳統](../../../resource-manager-deployment-model.md)。</span><span class="sxs-lookup"><span data-stu-id="944b0-115">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../resource-manager-deployment-model.md).</span></span>

## <a name="find-the-virtual-machine"></a><span data-ttu-id="944b0-116">尋找虛擬機器</span><span class="sxs-lookup"><span data-stu-id="944b0-116">Find the virtual machine</span></span>
1. <span data-ttu-id="944b0-117">登入 [Azure 入口網站](https://portal.azure.com/)。</span><span class="sxs-lookup"><span data-stu-id="944b0-117">Sign in to the [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="944b0-118">從儀表板上所列資源選取虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="944b0-118">Select the virtual machine from the resource listed on the dashboard.</span></span>
3. <span data-ttu-id="944b0-119">在左窗格的 [設定] 下方，按一下 [磁碟]。</span><span class="sxs-lookup"><span data-stu-id="944b0-119">In the left pane under **Settings**, click **Disks**.</span></span>

    ![開啟磁碟設定](./media/attach-disk/virtualmachinedisks.png)

<span data-ttu-id="944b0-121">接著，依照指示來連接[新的磁碟](#option-1-attach-a-new-disk)或[現有的磁碟](#option-2-attach-an-existing-disk)。</span><span class="sxs-lookup"><span data-stu-id="944b0-121">Continue by following instructions for attaching either a [new disk](#option-1-attach-a-new-disk) or an [existing disk](#option-2-attach-an-existing-disk).</span></span>

## <a name="option-1-attach-and-initialize-a-new-disk"></a><span data-ttu-id="944b0-122">選項 1：連接新磁碟並進行初始化</span><span class="sxs-lookup"><span data-stu-id="944b0-122">Option 1: Attach and initialize a new disk</span></span>

1. <span data-ttu-id="944b0-123">在 [磁碟] 刀鋒視窗上，按一下 [連接新項目]。</span><span class="sxs-lookup"><span data-stu-id="944b0-123">On the **Disks** blade, click **Attach new**.</span></span>
2. <span data-ttu-id="944b0-124">檢閱預設設定，視需要進行更新，然後按一下 [確定] 。</span><span class="sxs-lookup"><span data-stu-id="944b0-124">Review the default settings, update as necessary, and then click **OK**.</span></span>

   ![檢閱磁碟設定](./media/attach-disk/attach-new.png)

3. <span data-ttu-id="944b0-126">在 Azure 建立磁碟並將其連接至虛擬機器之後，該新磁碟就會列在虛擬機器之磁碟設定中的 [資料磁碟] 底下。</span><span class="sxs-lookup"><span data-stu-id="944b0-126">After Azure creates the disk and attaches it to the virtual machine, the new disk is listed in the virtual machine's disk settings under **Data Disks**.</span></span>

### <a name="initialize-a-new-data-disk"></a><span data-ttu-id="944b0-127">初始化新的資料磁碟</span><span class="sxs-lookup"><span data-stu-id="944b0-127">Initialize a new data disk</span></span>

1. <span data-ttu-id="944b0-128">連接至虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="944b0-128">Connect to the virtual machine.</span></span> <span data-ttu-id="944b0-129">如需指示，請參閱[如何連接和登入執行 Windows 的 Azure 虛擬機器](../../virtual-machines-windows-connect-logon.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="944b0-129">For instructions, see [How to connect and log on to an Azure virtual machine running Windows](../../virtual-machines-windows-connect-logon.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>
2. <span data-ttu-id="944b0-130">登入虛擬機器之後，開啟 [伺服器管理員]。</span><span class="sxs-lookup"><span data-stu-id="944b0-130">After you log on to the virtual machine, open **Server Manager**.</span></span> <span data-ttu-id="944b0-131">在左窗格中，選取 [File and Storage Services] 。</span><span class="sxs-lookup"><span data-stu-id="944b0-131">In the left pane, select **File and Storage Services**.</span></span>

    ![開啟伺服器管理員](../media/attach-disk-portal/fileandstorageservices.png)

3. <span data-ttu-id="944b0-133">選取 [磁碟]。</span><span class="sxs-lookup"><span data-stu-id="944b0-133">Select **Disks**.</span></span>
4. <span data-ttu-id="944b0-134">[磁碟]  區段會列出磁碟。</span><span class="sxs-lookup"><span data-stu-id="944b0-134">The **Disks** section lists the disks.</span></span> <span data-ttu-id="944b0-135">多數情況下，虛擬機器會有磁碟 0、磁碟 1 和磁碟 2。</span><span class="sxs-lookup"><span data-stu-id="944b0-135">Most often, a virtual machine has disk 0, disk 1, and disk 2.</span></span> <span data-ttu-id="944b0-136">磁碟 0 是作業系統磁碟，磁碟 1 是暫存磁碟，磁碟 2 則是新連接至虛擬機器的資料磁碟。</span><span class="sxs-lookup"><span data-stu-id="944b0-136">Disk 0 is the operating system disk, disk 1 is the temporary disk, and disk 2 is the data disk newly attached to the virtual machine.</span></span> <span data-ttu-id="944b0-137">資料磁碟會將磁碟分割列為**未知**。</span><span class="sxs-lookup"><span data-stu-id="944b0-137">The data disk lists the Partition as **Unknown**.</span></span>

 <span data-ttu-id="944b0-138">在磁碟上按一下滑鼠右鍵，然後選取 [初始化] 。</span><span class="sxs-lookup"><span data-stu-id="944b0-138">Right-click the disk and select **Initialize**.</span></span>

5. <span data-ttu-id="944b0-139">初始化磁碟時，您會收到將清除所有資料的通知。</span><span class="sxs-lookup"><span data-stu-id="944b0-139">You're notified that all data will be erased when the disk is initialized.</span></span> <span data-ttu-id="944b0-140">按一下 [是]，認可此警告並初始化磁碟。</span><span class="sxs-lookup"><span data-stu-id="944b0-140">Click **Yes** to acknowledge the warning and initialize the disk.</span></span> <span data-ttu-id="944b0-141">完成之後，即會將磁碟分割列為 [GPT]。</span><span class="sxs-lookup"><span data-stu-id="944b0-141">Once complete, the partition will be listed as **GPT**.</span></span> <span data-ttu-id="944b0-142">再次於磁碟上按一下滑鼠右鍵，然後選取 新增磁碟區 。</span><span class="sxs-lookup"><span data-stu-id="944b0-142">Right-click the disk again and select **New Volume**.</span></span>

6. <span data-ttu-id="944b0-143">使用預設值完成精靈。</span><span class="sxs-lookup"><span data-stu-id="944b0-143">Complete the wizard using the default values.</span></span> <span data-ttu-id="944b0-144">當精靈完成時，[ **磁碟區** ] 區段會列出新的磁碟區。</span><span class="sxs-lookup"><span data-stu-id="944b0-144">When the wizard is done, the **Volumes** section lists the new volume.</span></span> <span data-ttu-id="944b0-145">磁碟此時將上線，可用來儲存資料。</span><span class="sxs-lookup"><span data-stu-id="944b0-145">The disk is now online and ready to store data.</span></span>

    ![成功初始化磁碟區](./media/attach-disk/newdiskafterinitialization.png)

## <a name="option-2-attach-an-existing-disk"></a><span data-ttu-id="944b0-147">選項 2：連接現有磁碟</span><span class="sxs-lookup"><span data-stu-id="944b0-147">Option 2: Attach an existing disk</span></span>
1. <span data-ttu-id="944b0-148">在 [磁碟] 刀鋒視窗上，按一下 [連接現有項目]。</span><span class="sxs-lookup"><span data-stu-id="944b0-148">On the **Disks** blade, click **Attach existing**.</span></span>
2. <span data-ttu-id="944b0-149">在 [連接現有磁碟] 底下，按一下 [位置]。</span><span class="sxs-lookup"><span data-stu-id="944b0-149">Under **Attach existing disk**, click **Location**.</span></span>

   ![連接現有磁碟](./media/attach-disk/attachexistingdisksettings.png)
3. <span data-ttu-id="944b0-151">在 [儲存體帳戶] 底下，選取持有該 .vhd 檔案的帳戶和容器。</span><span class="sxs-lookup"><span data-stu-id="944b0-151">Under **Storage accounts**, select the account and container that holds the .vhd file.</span></span>

   ![尋找 VHD 位置](./media/attach-disk/existdiskstorageaccountandcontainer.png)

4. <span data-ttu-id="944b0-153">選取 .vhd 檔案。</span><span class="sxs-lookup"><span data-stu-id="944b0-153">Select the .vhd file.</span></span>
5. <span data-ttu-id="944b0-154">在 [連結現有磁碟] 底下，您剛才選取的檔案會列在 [VHD 檔案] 底下。</span><span class="sxs-lookup"><span data-stu-id="944b0-154">Under **Attach existing disk**, the file you just selected is listed under **VHD File**.</span></span> <span data-ttu-id="944b0-155">按一下 [確定] 。</span><span class="sxs-lookup"><span data-stu-id="944b0-155">Click **OK**.</span></span>
6. <span data-ttu-id="944b0-156">Azure 將磁碟連接至虛擬機器之後，該磁碟會列在虛擬機器磁碟設定中的 [資料磁碟] 下面。</span><span class="sxs-lookup"><span data-stu-id="944b0-156">After Azure attaches the disk to the virtual machine, it's listed in the virtual machine's disk settings under **Data Disks**.</span></span>

## <a name="use-trim-with-standard-storage"></a><span data-ttu-id="944b0-157">搭配使用 TRIM 與標準儲存體</span><span class="sxs-lookup"><span data-stu-id="944b0-157">Use TRIM with standard storage</span></span>

<span data-ttu-id="944b0-158">如果您使用標準儲存體 (HDD)，您應該啟用 TRIM。</span><span class="sxs-lookup"><span data-stu-id="944b0-158">If you use standard storage (HDD), you should enable TRIM.</span></span> <span data-ttu-id="944b0-159">TRIM 會捨棄磁碟上未使用的區塊，因此您只需支付實際使用的儲存體。</span><span class="sxs-lookup"><span data-stu-id="944b0-159">TRIM discards unused blocks on the disk so you are only billed for storage that you are actually using.</span></span> <span data-ttu-id="944b0-160">使用 TRIM 可以節省成本，包括刪除大型檔案時所產生的未使用區塊。</span><span class="sxs-lookup"><span data-stu-id="944b0-160">Using TRIM can save costs, including unused blocks that result from deleting large files.</span></span>

<span data-ttu-id="944b0-161">您可以執行此命令來檢查 TRIM 設定。</span><span class="sxs-lookup"><span data-stu-id="944b0-161">You can run this command to check the TRIM setting.</span></span> <span data-ttu-id="944b0-162">在您的 Windows VM 上開啟命令提示字元並輸入︰</span><span class="sxs-lookup"><span data-stu-id="944b0-162">Open a command prompt on your Windows VM and type:</span></span>

```
fsutil behavior query DisableDeleteNotify
```

<span data-ttu-id="944b0-163">如果命令傳回 0，則已正確啟用 TRIM。</span><span class="sxs-lookup"><span data-stu-id="944b0-163">If the command returns 0, TRIM is enabled correctly.</span></span> <span data-ttu-id="944b0-164">如果傳回 1，請執行下列命令來啟用 TRIM：</span><span class="sxs-lookup"><span data-stu-id="944b0-164">If it returns 1, run the following command to enable TRIM:</span></span>
```
fsutil behavior set DisableDeleteNotify 0
```

## <a name="next-steps"></a><span data-ttu-id="944b0-165">後續步驟</span><span class="sxs-lookup"><span data-stu-id="944b0-165">Next steps</span></span>
<span data-ttu-id="944b0-166">如果您的應用程式需要使用 D: 磁碟機來儲存資料，您可以[變更 Windows 暫存磁碟的磁碟機代號](../../virtual-machines-windows-change-drive-letter.md)。</span><span class="sxs-lookup"><span data-stu-id="944b0-166">If your application needs to use the D: drive to store data, you can [change the drive letter of the Windows temporary disk](../../virtual-machines-windows-change-drive-letter.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="944b0-167">其他資源</span><span class="sxs-lookup"><span data-stu-id="944b0-167">Additional resources</span></span>
[<span data-ttu-id="944b0-168">有關虛擬機器的磁碟和 VHD</span><span class="sxs-lookup"><span data-stu-id="944b0-168">About disks and VHDs for virtual machines</span></span>](../../virtual-machines-linux-about-disks-vhds.md)
