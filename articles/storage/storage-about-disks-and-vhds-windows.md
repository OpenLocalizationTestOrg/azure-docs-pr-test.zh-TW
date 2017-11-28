---
title: "關於 Microsoft Azure Windows VM 的磁碟和 VHD | Microsoft Docs"
description: "了解 Azure 中 Windows 虛擬機器的磁碟和 VHD 的基本知識。"
services: storage
documentationcenter: 
author: robinsh
manager: timlt
editor: tysonn
ms.assetid: 0142c64d-5e8c-4d62-aa6f-06d6261f485a
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/15/2017
ms.author: robinsh
ms.openlocfilehash: 34a4d8fa176484fbadb1b385d794cada5be607c8
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/18/2017
---
# <a name="about-disks-and-vhds-for-azure-windows-vms"></a><span data-ttu-id="58c17-103">關於 Azure Windows VM 的磁碟和 VHD</span><span class="sxs-lookup"><span data-stu-id="58c17-103">About disks and VHDs for Azure Windows VMs</span></span>
<span data-ttu-id="58c17-104">就像任何其他電腦，Azure 中的虛擬機器會使用磁碟做為儲存作業系統、應用程式和資料的位置。</span><span class="sxs-lookup"><span data-stu-id="58c17-104">Just like any other computer, virtual machines in Azure use disks as a place to store an operating system, applications, and data.</span></span> <span data-ttu-id="58c17-105">所有 Azure 虛擬機器都至少有兩個磁碟 - 一個 Windows 作業系統磁碟和一個暫存磁碟。</span><span class="sxs-lookup"><span data-stu-id="58c17-105">All Azure virtual machines have at least two disks – a Windows operating system disk and a temporary disk.</span></span> <span data-ttu-id="58c17-106">作業系統磁碟是從映像建立，且作業系統磁碟與該映像都是儲存在 Azure 儲存體帳戶中的虛擬硬碟 (VHD)。</span><span class="sxs-lookup"><span data-stu-id="58c17-106">The operating system disk is created from an image, and both the operating system disk and the image are virtual hard disks (VHDs) stored in an Azure storage account.</span></span> <span data-ttu-id="58c17-107">虛擬機器也可以有一或多個資料磁碟，而這些磁碟也會儲存成 VHD。</span><span class="sxs-lookup"><span data-stu-id="58c17-107">Virtual machines also can have one or more data disks, that are also stored as VHDs.</span></span> 

<span data-ttu-id="58c17-108">在本文中，我們將討論磁碟的不同用法，接著討論您可以建立和使用的不同磁碟類型。</span><span class="sxs-lookup"><span data-stu-id="58c17-108">In this article, we will talk about the different uses for the disks, and then discuss the different types of disks you can create and use.</span></span> <span data-ttu-id="58c17-109">本文也適用於 [Linux 虛擬機器](storage-about-disks-and-vhds-linux.md)。</span><span class="sxs-lookup"><span data-stu-id="58c17-109">This article is also available for [Linux virtual machines](storage-about-disks-and-vhds-linux.md).</span></span>

[!INCLUDE [learn-about-deployment-models](../../includes/learn-about-deployment-models-both-include.md)]

## <a name="disks-used-by-vms"></a><span data-ttu-id="58c17-110">VM 使用的磁碟</span><span class="sxs-lookup"><span data-stu-id="58c17-110">Disks used by VMs</span></span>

<span data-ttu-id="58c17-111">讓我們看看 VM 如何使用磁碟。</span><span class="sxs-lookup"><span data-stu-id="58c17-111">Let's take a look at how the disks are used by the VMs.</span></span>

### <a name="operating-system-disk"></a><span data-ttu-id="58c17-112">作業系統磁碟</span><span class="sxs-lookup"><span data-stu-id="58c17-112">Operating system disk</span></span>
<span data-ttu-id="58c17-113">每個虛擬機器都有一個連接的作業系統磁碟。</span><span class="sxs-lookup"><span data-stu-id="58c17-113">Every virtual machine has one attached operating system disk.</span></span> <span data-ttu-id="58c17-114">它會註冊為 SATA 磁碟機，並預設標示為 C: 磁碟機。</span><span class="sxs-lookup"><span data-stu-id="58c17-114">It's registered as a SATA drive and labeled as the C: drive by default.</span></span> <span data-ttu-id="58c17-115">此磁碟的最大容量為 2048 GB。</span><span class="sxs-lookup"><span data-stu-id="58c17-115">This disk has a maximum capacity of 2048 gigabytes (GB).</span></span> 

### <a name="temporary-disk"></a><span data-ttu-id="58c17-116">暫存磁碟</span><span class="sxs-lookup"><span data-stu-id="58c17-116">Temporary disk</span></span>
<span data-ttu-id="58c17-117">每個 VM 都包含一個暫存磁碟。</span><span class="sxs-lookup"><span data-stu-id="58c17-117">Each VM contains a temporary disk.</span></span> <span data-ttu-id="58c17-118">暫存磁碟為應用程式和處理程序提供短期的儲存空間，且僅供用來儲存分頁檔之類的資料。</span><span class="sxs-lookup"><span data-stu-id="58c17-118">The temporary disk provides short-term storage for applications and processes and is intended to only store data such as page or swap files.</span></span> <span data-ttu-id="58c17-119">暫存磁碟上的資料可能會在[維護事件](../virtual-machines/windows/manage-availability.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json#understand-vm-reboots---maintenance-vs-downtime)期間或當您[重新佈署 VM](../virtual-machines/windows/redeploy-to-new-node.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) 時遺失。</span><span class="sxs-lookup"><span data-stu-id="58c17-119">Data on the temporary disk may be lost during a [maintenance event](../virtual-machines/windows/manage-availability.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json#understand-vm-reboots---maintenance-vs-downtime) or when you [redeploy a VM](../virtual-machines/windows/redeploy-to-new-node.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> <span data-ttu-id="58c17-120">在 VM 的標準重新開機期間，暫存磁碟上的資料會保留。</span><span class="sxs-lookup"><span data-stu-id="58c17-120">During a standard reboot of the VM, the data on the temporary drive should persist.</span></span>

<span data-ttu-id="58c17-121">暫存磁碟預設會標示為 D: 磁碟機，並用於儲存 pagefile.sys。</span><span class="sxs-lookup"><span data-stu-id="58c17-121">The temporary disk is labeled as the D: drive by default and it used for storing pagefile.sys.</span></span> <span data-ttu-id="58c17-122">若要將此磁碟重新對應至不同的磁碟機代號，請參閱 [變更 Windows 暫存磁碟的磁碟機代號](../virtual-machines/windows/change-drive-letter.md)。</span><span class="sxs-lookup"><span data-stu-id="58c17-122">To remap this disk to a different drive letter, see [Change the drive letter of the Windows temporary disk](../virtual-machines/windows/change-drive-letter.md).</span></span> <span data-ttu-id="58c17-123">暫存磁碟的大小會依據虛擬機器的大小而改變。</span><span class="sxs-lookup"><span data-stu-id="58c17-123">The size of the temporary disk varies, based on the size of the virtual machine.</span></span> <span data-ttu-id="58c17-124">如需詳細資訊，請參閱 [Windows 虛擬機器的大小](../virtual-machines/windows/sizes.md)。</span><span class="sxs-lookup"><span data-stu-id="58c17-124">For more information, see [Sizes for Windows virtual machines](../virtual-machines/windows/sizes.md).</span></span>

<span data-ttu-id="58c17-125">如需有關 Azure 如何使用暫存磁碟的詳細資訊，請參閱 [Understanding the temporary drive on Microsoft Azure Virtual Machines (了解 Microsoft Azure 虛擬機器上的暫存磁碟機)](https://blogs.msdn.microsoft.com/mast/2013/12/06/understanding-the-temporary-drive-on-windows-azure-virtual-machines/)</span><span class="sxs-lookup"><span data-stu-id="58c17-125">For more information on how Azure uses the temporary disk, see [Understanding the temporary drive on Microsoft Azure Virtual Machines](https://blogs.msdn.microsoft.com/mast/2013/12/06/understanding-the-temporary-drive-on-windows-azure-virtual-machines/)</span></span>


### <a name="data-disk"></a><span data-ttu-id="58c17-126">資料磁碟</span><span class="sxs-lookup"><span data-stu-id="58c17-126">Data disk</span></span>
<span data-ttu-id="58c17-127">資料磁碟是連接至虛擬機器的 VHD，用來儲存應用程式資料或其他您需要保留的資料。</span><span class="sxs-lookup"><span data-stu-id="58c17-127">A data disk is a VHD that's attached to a virtual machine to store application data, or other data you need to keep.</span></span> <span data-ttu-id="58c17-128">資料磁碟註冊為 SCSI 磁碟機，並以您選擇的字母標示。</span><span class="sxs-lookup"><span data-stu-id="58c17-128">Data disks are registered as SCSI drives and are labeled with a letter that you choose.</span></span> <span data-ttu-id="58c17-129">每個資料磁碟具有 4095 GB 的最大容量。</span><span class="sxs-lookup"><span data-stu-id="58c17-129">Each data disk has a maximum capacity of 4095 GB.</span></span> <span data-ttu-id="58c17-130">虛擬機器的大小會決定您可以連接之磁碟的數量，以及您可以用來裝載磁碟的儲存體類型。</span><span class="sxs-lookup"><span data-stu-id="58c17-130">The size of the virtual machine determines how many data disks you can attach to it and the type of storage you can use to host the disks.</span></span>

> [!NOTE]
> <span data-ttu-id="58c17-131">如需有關虛擬機器容量的詳細資訊，請參閱 [Windows 虛擬機器的大小](../virtual-machines/windows/sizes.md)。</span><span class="sxs-lookup"><span data-stu-id="58c17-131">For more information about virtual machines capacities, see [Sizes for Windows virtual machines](../virtual-machines/windows/sizes.md).</span></span>
> 

<span data-ttu-id="58c17-132">當您從映像建立虛擬機器時，Azure 會建立作業系統磁碟。</span><span class="sxs-lookup"><span data-stu-id="58c17-132">Azure creates an operating system disk when you create a virtual machine from an image.</span></span> <span data-ttu-id="58c17-133">如果您使用包含資料磁碟映像時，Azure 建立虛擬機器時也會建立資料磁碟。</span><span class="sxs-lookup"><span data-stu-id="58c17-133">If you use an image that includes data disks, Azure also creates the data disks when it creates the virtual machine.</span></span> <span data-ttu-id="58c17-134">若沒有，則您可以建立虛擬機器後再新增資料磁碟。</span><span class="sxs-lookup"><span data-stu-id="58c17-134">Otherwise, you add data disks after you create the virtual machine.</span></span>

<span data-ttu-id="58c17-135">您可以隨時將資料磁碟「連接」  到虛擬機器來將該磁碟新增到虛擬機器中。</span><span class="sxs-lookup"><span data-stu-id="58c17-135">You can add data disks to a virtual machine at any time, by **attaching** the disk to the virtual machine.</span></span> <span data-ttu-id="58c17-136">您可以使用您已上傳或複製到儲存體帳戶的 VHD，或是 Azure 為您建立的 VHD。</span><span class="sxs-lookup"><span data-stu-id="58c17-136">You can use a VHD that you've uploaded or copied to your storage account, or one that Azure creates for you.</span></span> <span data-ttu-id="58c17-137">附加資料磁碟時，會透過在 VHD 上加上「租約」，來將 VHD 檔案與 VM 關聯，如此一來，當它仍處於附加狀態時，就無法將它從儲存體中刪除。</span><span class="sxs-lookup"><span data-stu-id="58c17-137">Attaching a data disk associates the VHD file with the VM by placing a 'lease' on the VHD so it can't be deleted from storage while it's still attached.</span></span>


[!INCLUDE [storage-about-vhds-and-disks-windows-and-linux](../../includes/storage-about-vhds-and-disks-windows-and-linux.md)]

## <a name="one-last-recommendation-use-trim-with-unmanaged-standard-disks"></a><span data-ttu-id="58c17-138">最後一個建議：對非受控標準磁碟使用 TRIM</span><span class="sxs-lookup"><span data-stu-id="58c17-138">One last recommendation: Use TRIM with unmanaged standard disks</span></span> 

<span data-ttu-id="58c17-139">如果您使用非受控標準儲存體 (HDD)，您應該啟用 TRIM。</span><span class="sxs-lookup"><span data-stu-id="58c17-139">If you use unmanaged standard disks (HDD), you should enable TRIM.</span></span> <span data-ttu-id="58c17-140">TRIM 會捨棄磁碟上未使用的區塊，因此您只需支付實際使用的儲存體。</span><span class="sxs-lookup"><span data-stu-id="58c17-140">TRIM discards unused blocks on the disk so you are only billed for storage that you are actually using.</span></span> <span data-ttu-id="58c17-141">如果您建立大型檔案，然後將它們刪除，這便可節省成本。</span><span class="sxs-lookup"><span data-stu-id="58c17-141">This can save on costs if you create large files and then delete them.</span></span> 

<span data-ttu-id="58c17-142">您可以執行此命令來檢查 TRIM 設定。</span><span class="sxs-lookup"><span data-stu-id="58c17-142">You can run this command to check the TRIM setting.</span></span> <span data-ttu-id="58c17-143">在您的 Windows VM 上開啟命令提示字元並輸入︰</span><span class="sxs-lookup"><span data-stu-id="58c17-143">Open a command prompt on your Windows VM and type:</span></span>


```
fsutil behavior query DisableDeleteNotify
```

<span data-ttu-id="58c17-144">如果命令傳回 0，則已正確啟用 TRIM。</span><span class="sxs-lookup"><span data-stu-id="58c17-144">If the command returns 0, TRIM is enabled correctly.</span></span> <span data-ttu-id="58c17-145">如果傳回 1，請執行下列命令來啟用 TRIM：</span><span class="sxs-lookup"><span data-stu-id="58c17-145">If it returns 1, run the following command to enable TRIM:</span></span>

```
fsutil behavior set DisableDeleteNotify 0
```

> [!NOTE]
> <span data-ttu-id="58c17-146">注意：Trim 支援是從 Windows Server 2012 / Windows 8 和以上版本開始，請參閱[新 API 允許應用程式將 "TRIM and Unmap" 提示傳送給儲存媒體](https://msdn.microsoft.com/windows/compatibility/new-api-allows-apps-to-send-trim-and-unmap-hints)。</span><span class="sxs-lookup"><span data-stu-id="58c17-146">Note: Trim support starts with Windows Server 2012 / Windows 8 and above, see see [New API allows apps to send "TRIM and Unmap" hints to storage media](https://msdn.microsoft.com/windows/compatibility/new-api-allows-apps-to-send-trim-and-unmap-hints).</span></span>
> 

<!-- Might want to match next-steps from overview of managed disks -->
## <a name="next-steps"></a><span data-ttu-id="58c17-147">後續步驟</span><span class="sxs-lookup"><span data-stu-id="58c17-147">Next steps</span></span>
* <span data-ttu-id="58c17-148">[連接磁碟](../virtual-machines/windows/attach-managed-disk-portal.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) 來為您的 VM 新增額外的儲存空間。</span><span class="sxs-lookup"><span data-stu-id="58c17-148">[Attach a disk](../virtual-machines/windows/attach-managed-disk-portal.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) to add additional storage for your VM.</span></span>
* <span data-ttu-id="58c17-149">[變更 Windows 暫存磁碟的磁碟機代號](../virtual-machines/windows/change-drive-letter.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json) ，讓您的應用程式可以使用 D: 磁碟機來儲存資料。</span><span class="sxs-lookup"><span data-stu-id="58c17-149">[Change the drive letter of the Windows temporary disk](../virtual-machines/windows/change-drive-letter.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json) so your application can use the D: drive for data.</span></span>

