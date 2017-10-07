---
title: "aaaAbout 磁碟和 Microsoft Azure Linux Vm 的 Vhd |Microsoft 文件"
description: "深入了解 hello Azure 中 Linux 虛擬機器磁碟和 Vhd 的基本概念。"
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
ms.openlocfilehash: 1155d773136677553d263c17fbf8b224035d96bf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="about-disks-and-vhds-for-azure-linux-vms"></a><span data-ttu-id="664ac-103">關於 Azure Linux VM 的磁碟和 VHD</span><span class="sxs-lookup"><span data-stu-id="664ac-103">About disks and VHDs for Azure Linux VMs</span></span>
<span data-ttu-id="664ac-104">就像任何其他電腦一樣在 Azure 虛擬機器會使用磁碟進行 toostore 作業系統、 應用程式和資料。</span><span class="sxs-lookup"><span data-stu-id="664ac-104">Just like any other computer, virtual machines in Azure use disks as a place toostore an operating system, applications, and data.</span></span> <span data-ttu-id="664ac-105">所有 Azure 虛擬機器都至少有兩個磁碟 – Linux 作業系統磁碟和暫存磁碟。</span><span class="sxs-lookup"><span data-stu-id="664ac-105">All Azure virtual machines have at least two disks – a Linux operating system disk and a temporary disk.</span></span> <span data-ttu-id="664ac-106">從映像，建立 hello 作業系統磁碟和 hello 作業系統磁碟和 hello 映像會實際虛擬硬碟 (Vhd) 儲存在 Azure 儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="664ac-106">hello operating system disk is created from an image, and both hello operating system disk and hello image are actually virtual hard disks (VHDs) stored in an Azure storage account.</span></span> <span data-ttu-id="664ac-107">虛擬機器也可以有一或多個資料磁碟，而這些磁碟也會儲存成 VHD。</span><span class="sxs-lookup"><span data-stu-id="664ac-107">Virtual machines also can have one or more data disks, that are also stored as VHDs.</span></span> 

<span data-ttu-id="664ac-108">在本文中，即將討論 hello 不同用法 hello 磁碟，及再討論 hello 不同類型的磁碟，您可以建立及使用。</span><span class="sxs-lookup"><span data-stu-id="664ac-108">In this article, we will talk about hello different uses for hello disks, and then discuss hello different types of disks you can create and use.</span></span> <span data-ttu-id="664ac-109">本文也適用於 [Windows 虛擬機器](storage-about-disks-and-vhds-windows.md)。</span><span class="sxs-lookup"><span data-stu-id="664ac-109">This article is also available for [Windows virtual machines](storage-about-disks-and-vhds-windows.md).</span></span>

[!INCLUDE [learn-about-deployment-models](../../includes/learn-about-deployment-models-both-include.md)]

## <a name="disks-used-by-vms"></a><span data-ttu-id="664ac-110">VM 使用的磁碟</span><span class="sxs-lookup"><span data-stu-id="664ac-110">Disks used by VMs</span></span>

<span data-ttu-id="664ac-111">讓我們看看如何使用 hello Vm hello 磁碟。</span><span class="sxs-lookup"><span data-stu-id="664ac-111">Let's take a look at how hello disks are used by hello VMs.</span></span>

## <a name="operating-system-disk"></a><span data-ttu-id="664ac-112">作業系統磁碟</span><span class="sxs-lookup"><span data-stu-id="664ac-112">Operating system disk</span></span>
<span data-ttu-id="664ac-113">每個虛擬機器都有一個連接的作業系統磁碟。</span><span class="sxs-lookup"><span data-stu-id="664ac-113">Every virtual machine has one attached operating system disk.</span></span> <span data-ttu-id="664ac-114">它會註冊為 SATA 磁碟機，並預設標示為 /dev/sda。</span><span class="sxs-lookup"><span data-stu-id="664ac-114">It's registered as a SATA drive and is labeled /dev/sda by default.</span></span> <span data-ttu-id="664ac-115">此磁碟具有 2048 GB 的最大容量。</span><span class="sxs-lookup"><span data-stu-id="664ac-115">This disk has a maximum capacity of 2048 gigabytes (GB).</span></span> 

## <a name="temporary-disk"></a><span data-ttu-id="664ac-116">暫存磁碟</span><span class="sxs-lookup"><span data-stu-id="664ac-116">Temporary disk</span></span>
<span data-ttu-id="664ac-117">每個 VM 都包含一個暫存磁碟。</span><span class="sxs-lookup"><span data-stu-id="664ac-117">Each VM contains a temporary disk.</span></span> <span data-ttu-id="664ac-118">hello 暫存磁碟的應用程式和處理序提供短期儲存，預期的 tooonly 存放區資料，例如分頁檔。</span><span class="sxs-lookup"><span data-stu-id="664ac-118">hello temporary disk provides short-term storage for applications and processes and is intended tooonly store data such as page or swap files.</span></span> <span data-ttu-id="664ac-119">Hello 暫存磁碟上的資料可能會遺失期間[維護事件](../virtual-machines/windows/manage-availability.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json#understand-vm-reboots---maintenance-vs-downtime)或當您[重新部署 VM](../virtual-machines/linux/redeploy-to-new-node.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="664ac-119">Data on hello temporary disk may be lost during a [maintenance event](../virtual-machines/windows/manage-availability.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json#understand-vm-reboots---maintenance-vs-downtime) or when you [redeploy a VM](../virtual-machines/linux/redeploy-to-new-node.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span> <span data-ttu-id="664ac-120">Hello VM 標準重開機，應保存 hello hello 暫存磁碟機上的資料。</span><span class="sxs-lookup"><span data-stu-id="664ac-120">During a standard reboot of hello VM, hello data on hello temporary drive should persist.</span></span>

<span data-ttu-id="664ac-121">Linux 的虛擬機器上 hello 磁碟通常是**/開發/sdb** is 格式化及裝載太**/mnt**由 hello Azure Linux 代理程式。</span><span class="sxs-lookup"><span data-stu-id="664ac-121">On Linux virtual machines, hello disk is typically **/dev/sdb** and is formatted and mounted too**/mnt** by hello Azure Linux Agent.</span></span> <span data-ttu-id="664ac-122">hello hello 暫存磁碟的大小會根據 hello hello 虛擬機器大小而不同。</span><span class="sxs-lookup"><span data-stu-id="664ac-122">hello size of hello temporary disk varies, based on hello size of hello virtual machine.</span></span> <span data-ttu-id="664ac-123">如需詳細資訊，請參閱 [Linux 虛擬機器的大小](../virtual-machines/linux/sizes.md)。</span><span class="sxs-lookup"><span data-stu-id="664ac-123">For more information, see [Sizes for Linux virtual machines](../virtual-machines/linux/sizes.md).</span></span>

<span data-ttu-id="664ac-124">如需有關 Azure 的 hello 暫存磁碟的使用方式的詳細資訊，請參閱[了解 hello 暫存磁碟機上的 Microsoft Azure 虛擬機器](https://blogs.msdn.microsoft.com/mast/2013/12/06/understanding-the-temporary-drive-on-windows-azure-virtual-machines/)</span><span class="sxs-lookup"><span data-stu-id="664ac-124">For more information on how Azure uses hello temporary disk, see [Understanding hello temporary drive on Microsoft Azure Virtual Machines](https://blogs.msdn.microsoft.com/mast/2013/12/06/understanding-the-temporary-drive-on-windows-azure-virtual-machines/)</span></span>

## <a name="data-disk"></a><span data-ttu-id="664ac-125">資料磁碟</span><span class="sxs-lookup"><span data-stu-id="664ac-125">Data disk</span></span>
<span data-ttu-id="664ac-126">資料磁碟是附加的 tooa 虛擬機器 toostore 應用程式資料，或需要 tookeep 其他資料的 VHD。</span><span class="sxs-lookup"><span data-stu-id="664ac-126">A data disk is a VHD that's attached tooa virtual machine toostore application data, or other data you need tookeep.</span></span> <span data-ttu-id="664ac-127">資料磁碟註冊為 SCSI 磁碟機，並以您選擇的字母標示。</span><span class="sxs-lookup"><span data-stu-id="664ac-127">Data disks are registered as SCSI drives and are labeled with a letter that you choose.</span></span> <span data-ttu-id="664ac-128">每個資料磁碟具有 4095 GB 的最大容量。</span><span class="sxs-lookup"><span data-stu-id="664ac-128">Each data disk has a maximum capacity of 4095 GB.</span></span> <span data-ttu-id="664ac-129">hello hello 虛擬機器的大小會決定您可以將附加的儲存體，您可以使用 tooit 與 hello 類型的資料磁碟數目 toohost hello 磁碟。</span><span class="sxs-lookup"><span data-stu-id="664ac-129">hello size of hello virtual machine determines how many data disks you can attach tooit and hello type of storage you can use toohost hello disks.</span></span>

> [!NOTE]
> <span data-ttu-id="664ac-130">如需有關虛擬機器容量的詳細資訊，請參閱 [Linux 虛擬機器的大小](../virtual-machines/linux/sizes.md)。</span><span class="sxs-lookup"><span data-stu-id="664ac-130">For more details about virtual machines capacities, see [Sizes for Linux virtual machines](../virtual-machines/linux/sizes.md).</span></span>
> 

<span data-ttu-id="664ac-131">當您從映像建立虛擬機器時，Azure 會建立作業系統磁碟。</span><span class="sxs-lookup"><span data-stu-id="664ac-131">Azure creates an operating system disk when you create a virtual machine from an image.</span></span> <span data-ttu-id="664ac-132">如果您使用包含資料磁碟的映像時，Azure 也會建立 hello 資料磁碟時，它會建立 hello 虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="664ac-132">If you use an image that includes data disks, Azure also creates hello data disks when it creates hello virtual machine.</span></span> <span data-ttu-id="664ac-133">否則，您建立 hello 虛擬機器之後加入資料磁碟。</span><span class="sxs-lookup"><span data-stu-id="664ac-133">Otherwise, you add data disks after you create hello virtual machine.</span></span>

<span data-ttu-id="664ac-134">您可以新增任何時候，資料磁碟 tooa 虛擬機器由**附加**hello 磁碟 toohello 虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="664ac-134">You can add data disks tooa virtual machine at any time, by **attaching** hello disk toohello virtual machine.</span></span> <span data-ttu-id="664ac-135">您可以使用您已上傳或複製 tooyour 儲存體帳戶，或其中一個，Azure 會為您建立的 VHD。</span><span class="sxs-lookup"><span data-stu-id="664ac-135">You can use a VHD that you've uploaded or copied tooyour storage account, or one that Azure creates for you.</span></span> <span data-ttu-id="664ac-136">連接資料磁碟 hello VHD 檔案將與關聯 hello VM，將 「 租用 」 放置在 hello VHD，因此無法加以刪除仍附加時從儲存體。</span><span class="sxs-lookup"><span data-stu-id="664ac-136">Attaching a data disk associates hello VHD file with hello VM, by placing a 'lease' on hello VHD so it can't be deleted from storage while it's still attached.</span></span>

[!INCLUDE [storage-about-vhds-and-disks-windows-and-linux](../../includes/storage-about-vhds-and-disks-windows-and-linux.md)]

## <a name="troubleshooting"></a><span data-ttu-id="664ac-137">疑難排解</span><span class="sxs-lookup"><span data-stu-id="664ac-137">Troubleshooting</span></span>
[!INCLUDE [virtual-machines-linux-lunzero](../../includes/virtual-machines-linux-lunzero.md)]

## <a name="next-steps"></a><span data-ttu-id="664ac-138">後續步驟</span><span class="sxs-lookup"><span data-stu-id="664ac-138">Next steps</span></span>
* <span data-ttu-id="664ac-139">[將磁碟連接](../virtual-machines/linux/add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)vm tooadd 額外的存放裝置。</span><span class="sxs-lookup"><span data-stu-id="664ac-139">[Attach a disk](../virtual-machines/linux/add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) tooadd additional storage for your VM.</span></span>
* <span data-ttu-id="664ac-140">[設定軟體 RAID](../virtual-machines/linux/configure-raid.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) 以提供備援。</span><span class="sxs-lookup"><span data-stu-id="664ac-140">[Configure software RAID](../virtual-machines/linux/configure-raid.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) for redundancy.</span></span>
* <span data-ttu-id="664ac-141">[擷取 Linux 虛擬機器](../virtual-machines/linux/classic/capture-image.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)以便快速部署額外的 VM。</span><span class="sxs-lookup"><span data-stu-id="664ac-141">[Capture a Linux virtual machine](../virtual-machines/linux/classic/capture-image.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json) so you can quickly deploy additional VMs.</span></span>

