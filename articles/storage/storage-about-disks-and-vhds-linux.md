---
title: "關於 Microsoft Azure Linux VM 的磁碟和 VHD | Microsoft Docs"
description: "了解 Azure 中 Linux 虛擬機器的磁碟和 VHD 的基本知識。"
services: storage
documentationcenter: 
author: robinsh
manager: timlt
editor: tysonn
ms.assetid: 7be8dd52-98f7-4187-9b78-55197915bc9b
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/15/2017
ms.author: robinsh
ms.openlocfilehash: 8305abeb8d943cdcc78383d678387c12cedfd1c3
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="about-disks-and-vhds-for-azure-linux-vms"></a><span data-ttu-id="671e2-103">關於 Azure Linux VM 的磁碟和 VHD</span><span class="sxs-lookup"><span data-stu-id="671e2-103">About disks and VHDs for Azure Linux VMs</span></span>
<span data-ttu-id="671e2-104">就像任何其他電腦，Azure 中的虛擬機器會使用磁碟做為儲存作業系統、應用程式和資料的位置。</span><span class="sxs-lookup"><span data-stu-id="671e2-104">Just like any other computer, virtual machines in Azure use disks as a place to store an operating system, applications, and data.</span></span> <span data-ttu-id="671e2-105">所有 Azure 虛擬機器都至少有兩個磁碟 – Linux 作業系統磁碟和暫存磁碟。</span><span class="sxs-lookup"><span data-stu-id="671e2-105">All Azure virtual machines have at least two disks – a Linux operating system disk and a temporary disk.</span></span> <span data-ttu-id="671e2-106">作業系統磁碟是由映像建立，且作業系統磁碟與該映像，實際上都是儲存在 Azure 儲存體帳戶的虛擬硬碟 (VHD)。</span><span class="sxs-lookup"><span data-stu-id="671e2-106">The operating system disk is created from an image, and both the operating system disk and the image are actually virtual hard disks (VHDs) stored in an Azure storage account.</span></span> <span data-ttu-id="671e2-107">虛擬機器也可以有一或多個資料磁碟，而這些磁碟也會儲存成 VHD。</span><span class="sxs-lookup"><span data-stu-id="671e2-107">Virtual machines also can have one or more data disks, that are also stored as VHDs.</span></span> 

<span data-ttu-id="671e2-108">在本文中，我們將討論磁碟的不同用法，接著討論您可以建立和使用的不同磁碟類型。</span><span class="sxs-lookup"><span data-stu-id="671e2-108">In this article, we will talk about the different uses for the disks, and then discuss the different types of disks you can create and use.</span></span> <span data-ttu-id="671e2-109">本文也適用於 [Windows 虛擬機器](storage-about-disks-and-vhds-windows.md)。</span><span class="sxs-lookup"><span data-stu-id="671e2-109">This article is also available for [Windows virtual machines](storage-about-disks-and-vhds-windows.md).</span></span>

[!INCLUDE [learn-about-deployment-models](../../includes/learn-about-deployment-models-both-include.md)]

## <a name="disks-used-by-vms"></a><span data-ttu-id="671e2-110">VM 使用的磁碟</span><span class="sxs-lookup"><span data-stu-id="671e2-110">Disks used by VMs</span></span>

<span data-ttu-id="671e2-111">讓我們看看 VM 如何使用磁碟。</span><span class="sxs-lookup"><span data-stu-id="671e2-111">Let's take a look at how the disks are used by the VMs.</span></span>

## <a name="operating-system-disk"></a><span data-ttu-id="671e2-112">作業系統磁碟</span><span class="sxs-lookup"><span data-stu-id="671e2-112">Operating system disk</span></span>
<span data-ttu-id="671e2-113">每個虛擬機器都有一個連接的作業系統磁碟。</span><span class="sxs-lookup"><span data-stu-id="671e2-113">Every virtual machine has one attached operating system disk.</span></span> <span data-ttu-id="671e2-114">它會註冊為 SATA 磁碟機，並預設標示為 /dev/sda。</span><span class="sxs-lookup"><span data-stu-id="671e2-114">It's registered as a SATA drive and is labeled /dev/sda by default.</span></span> <span data-ttu-id="671e2-115">此磁碟具有 2048 GB 的最大容量。</span><span class="sxs-lookup"><span data-stu-id="671e2-115">This disk has a maximum capacity of 2048 gigabytes (GB).</span></span> 

## <a name="temporary-disk"></a><span data-ttu-id="671e2-116">暫存磁碟</span><span class="sxs-lookup"><span data-stu-id="671e2-116">Temporary disk</span></span>
<span data-ttu-id="671e2-117">每個 VM 都包含一個暫存磁碟。</span><span class="sxs-lookup"><span data-stu-id="671e2-117">Each VM contains a temporary disk.</span></span> <span data-ttu-id="671e2-118">暫存磁碟為應用程式和處理程序提供短期的儲存空間，且僅供用來儲存分頁檔之類的資料。</span><span class="sxs-lookup"><span data-stu-id="671e2-118">The temporary disk provides short-term storage for applications and processes and is intended to only store data such as page or swap files.</span></span> <span data-ttu-id="671e2-119">暫存磁碟上的資料可能會在[維護事件](../virtual-machines/windows/manage-availability.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json#understand-vm-reboots---maintenance-vs-downtime)期間或當您[重新佈署 VM](../virtual-machines/linux/redeploy-to-new-node.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) 時遺失。</span><span class="sxs-lookup"><span data-stu-id="671e2-119">Data on the temporary disk may be lost during a [maintenance event](../virtual-machines/windows/manage-availability.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json#understand-vm-reboots---maintenance-vs-downtime) or when you [redeploy a VM](../virtual-machines/linux/redeploy-to-new-node.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span> <span data-ttu-id="671e2-120">在 VM 的標準重新開機期間，暫存磁碟上的資料會保留。</span><span class="sxs-lookup"><span data-stu-id="671e2-120">During a standard reboot of the VM, the data on the temporary drive should persist.</span></span>

<span data-ttu-id="671e2-121">在 Linux 虛擬機器上，這個磁碟通常是 **/dev/sdb**，並且會由「Azure Linux 代理程式」將它格式化並裝載至 **/mnt/**。</span><span class="sxs-lookup"><span data-stu-id="671e2-121">On Linux virtual machines, the disk is typically **/dev/sdb** and is formatted and mounted to **/mnt** by the Azure Linux Agent.</span></span> <span data-ttu-id="671e2-122">暫存磁碟的大小會依據虛擬機器的大小而改變。</span><span class="sxs-lookup"><span data-stu-id="671e2-122">The size of the temporary disk varies, based on the size of the virtual machine.</span></span> <span data-ttu-id="671e2-123">如需詳細資訊，請參閱 [Linux 虛擬機器的大小](../virtual-machines/linux/sizes.md)。</span><span class="sxs-lookup"><span data-stu-id="671e2-123">For more information, see [Sizes for Linux virtual machines](../virtual-machines/linux/sizes.md).</span></span>

<span data-ttu-id="671e2-124">如需有關 Azure 如何使用暫存磁碟的詳細資訊，請參閱 [Understanding the temporary drive on Microsoft Azure Virtual Machines (了解 Microsoft Azure 虛擬機器上的暫存磁碟機)](https://blogs.msdn.microsoft.com/mast/2013/12/06/understanding-the-temporary-drive-on-windows-azure-virtual-machines/)</span><span class="sxs-lookup"><span data-stu-id="671e2-124">For more information on how Azure uses the temporary disk, see [Understanding the temporary drive on Microsoft Azure Virtual Machines](https://blogs.msdn.microsoft.com/mast/2013/12/06/understanding-the-temporary-drive-on-windows-azure-virtual-machines/)</span></span>

## <a name="data-disk"></a><span data-ttu-id="671e2-125">資料磁碟</span><span class="sxs-lookup"><span data-stu-id="671e2-125">Data disk</span></span>
<span data-ttu-id="671e2-126">資料磁碟是連接至虛擬機器的 VHD，用來儲存應用程式資料或其他您需要保留的資料。</span><span class="sxs-lookup"><span data-stu-id="671e2-126">A data disk is a VHD that's attached to a virtual machine to store application data, or other data you need to keep.</span></span> <span data-ttu-id="671e2-127">資料磁碟註冊為 SCSI 磁碟機，並以您選擇的字母標示。</span><span class="sxs-lookup"><span data-stu-id="671e2-127">Data disks are registered as SCSI drives and are labeled with a letter that you choose.</span></span> <span data-ttu-id="671e2-128">每個資料磁碟具有 4095 GB 的最大容量。</span><span class="sxs-lookup"><span data-stu-id="671e2-128">Each data disk has a maximum capacity of 4095 GB.</span></span> <span data-ttu-id="671e2-129">虛擬機器的大小會決定您可以連接之磁碟的數量，以及您可以用來裝載磁碟的儲存體類型。</span><span class="sxs-lookup"><span data-stu-id="671e2-129">The size of the virtual machine determines how many data disks you can attach to it and the type of storage you can use to host the disks.</span></span>

> [!NOTE]
> <span data-ttu-id="671e2-130">如需有關虛擬機器容量的詳細資訊，請參閱 [Linux 虛擬機器的大小](../virtual-machines/linux/sizes.md)。</span><span class="sxs-lookup"><span data-stu-id="671e2-130">For more details about virtual machines capacities, see [Sizes for Linux virtual machines](../virtual-machines/linux/sizes.md).</span></span>
> 

<span data-ttu-id="671e2-131">當您從映像建立虛擬機器時，Azure 會建立作業系統磁碟。</span><span class="sxs-lookup"><span data-stu-id="671e2-131">Azure creates an operating system disk when you create a virtual machine from an image.</span></span> <span data-ttu-id="671e2-132">如果您使用包含資料磁碟映像時，Azure 建立虛擬機器時也會建立資料磁碟。</span><span class="sxs-lookup"><span data-stu-id="671e2-132">If you use an image that includes data disks, Azure also creates the data disks when it creates the virtual machine.</span></span> <span data-ttu-id="671e2-133">若沒有，則您可以建立虛擬機器後再新增資料磁碟。</span><span class="sxs-lookup"><span data-stu-id="671e2-133">Otherwise, you add data disks after you create the virtual machine.</span></span>

<span data-ttu-id="671e2-134">您可以隨時將資料磁碟「連接」  到虛擬機器來將該磁碟新增到虛擬機器中。</span><span class="sxs-lookup"><span data-stu-id="671e2-134">You can add data disks to a virtual machine at any time, by **attaching** the disk to the virtual machine.</span></span> <span data-ttu-id="671e2-135">您可以使用您已上傳或複製到儲存體帳戶的 VHD，或是 Azure 為您建立的 VHD。</span><span class="sxs-lookup"><span data-stu-id="671e2-135">You can use a VHD that you've uploaded or copied to your storage account, or one that Azure creates for you.</span></span> <span data-ttu-id="671e2-136">附加資料磁碟時，會透過在 VHD 上加上「租約」，來將 VHD 檔案與 VM 關聯，如此一來，當它仍處於附加狀態時，就無法將它從儲存體中刪除。</span><span class="sxs-lookup"><span data-stu-id="671e2-136">Attaching a data disk associates the VHD file with the VM, by placing a 'lease' on the VHD so it can't be deleted from storage while it's still attached.</span></span>

[!INCLUDE [storage-about-vhds-and-disks-windows-and-linux](../../includes/storage-about-vhds-and-disks-windows-and-linux.md)]

## <a name="troubleshooting"></a><span data-ttu-id="671e2-137">疑難排解</span><span class="sxs-lookup"><span data-stu-id="671e2-137">Troubleshooting</span></span>
[!INCLUDE [virtual-machines-linux-lunzero](../../includes/virtual-machines-linux-lunzero.md)]

## <a name="next-steps"></a><span data-ttu-id="671e2-138">後續步驟</span><span class="sxs-lookup"><span data-stu-id="671e2-138">Next steps</span></span>
* <span data-ttu-id="671e2-139">[連接磁碟](../virtual-machines/linux/add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) 來為您的 VM 新增額外的儲存空間。</span><span class="sxs-lookup"><span data-stu-id="671e2-139">[Attach a disk](../virtual-machines/linux/add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) to add additional storage for your VM.</span></span>
* <span data-ttu-id="671e2-140">[設定軟體 RAID](../virtual-machines/linux/configure-raid.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) 以提供備援。</span><span class="sxs-lookup"><span data-stu-id="671e2-140">[Configure software RAID](../virtual-machines/linux/configure-raid.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) for redundancy.</span></span>
* <span data-ttu-id="671e2-141">[擷取 Linux 虛擬機器](../virtual-machines/linux/classic/capture-image.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)以便快速部署額外的 VM。</span><span class="sxs-lookup"><span data-stu-id="671e2-141">[Capture a Linux virtual machine](../virtual-machines/linux/classic/capture-image.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json) so you can quickly deploy additional VMs.</span></span>

