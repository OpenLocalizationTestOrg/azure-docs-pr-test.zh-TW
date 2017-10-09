---
title: "aaaAbout 磁碟和 Microsoft Azure Windows Vm 的 Vhd |Microsoft 文件"
description: "深入了解磁碟和 Vhd 適用於 Windows Azure 虛擬機器中的 hello 基本概念。"
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
ms.openlocfilehash: 859e564dc74240bd7c70fec33255b8d071c4acf7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="about-disks-and-vhds-for-azure-windows-vms"></a><span data-ttu-id="9a6fa-103">關於 Azure Windows VM 的磁碟和 VHD</span><span class="sxs-lookup"><span data-stu-id="9a6fa-103">About disks and VHDs for Azure Windows VMs</span></span>
<span data-ttu-id="9a6fa-104">就像任何其他電腦一樣在 Azure 虛擬機器會使用磁碟進行 toostore 作業系統、 應用程式和資料。</span><span class="sxs-lookup"><span data-stu-id="9a6fa-104">Just like any other computer, virtual machines in Azure use disks as a place toostore an operating system, applications, and data.</span></span> <span data-ttu-id="9a6fa-105">所有 Azure 虛擬機器都至少有兩個磁碟 - 一個 Windows 作業系統磁碟和一個暫存磁碟。</span><span class="sxs-lookup"><span data-stu-id="9a6fa-105">All Azure virtual machines have at least two disks – a Windows operating system disk and a temporary disk.</span></span> <span data-ttu-id="9a6fa-106">從映像，建立 hello 作業系統磁碟，而 hello 作業系統磁碟和 hello 映像的虛擬硬碟 (Vhd) 儲存在 Azure 儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="9a6fa-106">hello operating system disk is created from an image, and both hello operating system disk and hello image are virtual hard disks (VHDs) stored in an Azure storage account.</span></span> <span data-ttu-id="9a6fa-107">虛擬機器也可以有一或多個資料磁碟，而這些磁碟也會儲存成 VHD。</span><span class="sxs-lookup"><span data-stu-id="9a6fa-107">Virtual machines also can have one or more data disks, that are also stored as VHDs.</span></span> 

<span data-ttu-id="9a6fa-108">在本文中，即將討論 hello 不同用法 hello 磁碟，及再討論 hello 不同類型的磁碟，您可以建立及使用。</span><span class="sxs-lookup"><span data-stu-id="9a6fa-108">In this article, we will talk about hello different uses for hello disks, and then discuss hello different types of disks you can create and use.</span></span> <span data-ttu-id="9a6fa-109">本文也適用於 [Linux 虛擬機器](storage-about-disks-and-vhds-linux.md)。</span><span class="sxs-lookup"><span data-stu-id="9a6fa-109">This article is also available for [Linux virtual machines](storage-about-disks-and-vhds-linux.md).</span></span>

[!INCLUDE [learn-about-deployment-models](../../includes/learn-about-deployment-models-both-include.md)]

## <a name="disks-used-by-vms"></a><span data-ttu-id="9a6fa-110">VM 使用的磁碟</span><span class="sxs-lookup"><span data-stu-id="9a6fa-110">Disks used by VMs</span></span>

<span data-ttu-id="9a6fa-111">讓我們看看如何使用 hello Vm hello 磁碟。</span><span class="sxs-lookup"><span data-stu-id="9a6fa-111">Let's take a look at how hello disks are used by hello VMs.</span></span>

### <a name="operating-system-disk"></a><span data-ttu-id="9a6fa-112">作業系統磁碟</span><span class="sxs-lookup"><span data-stu-id="9a6fa-112">Operating system disk</span></span>
<span data-ttu-id="9a6fa-113">每個虛擬機器都有一個連接的作業系統磁碟。</span><span class="sxs-lookup"><span data-stu-id="9a6fa-113">Every virtual machine has one attached operating system disk.</span></span> <span data-ttu-id="9a6fa-114">它已註冊為 SATA 磁碟機，並標示為預設的 hello c： 磁碟機。</span><span class="sxs-lookup"><span data-stu-id="9a6fa-114">It's registered as a SATA drive and labeled as hello C: drive by default.</span></span> <span data-ttu-id="9a6fa-115">此磁碟的最大容量為 2048 GB。</span><span class="sxs-lookup"><span data-stu-id="9a6fa-115">This disk has a maximum capacity of 2048 gigabytes (GB).</span></span> 

### <a name="temporary-disk"></a><span data-ttu-id="9a6fa-116">暫存磁碟</span><span class="sxs-lookup"><span data-stu-id="9a6fa-116">Temporary disk</span></span>
<span data-ttu-id="9a6fa-117">每個 VM 都包含一個暫存磁碟。</span><span class="sxs-lookup"><span data-stu-id="9a6fa-117">Each VM contains a temporary disk.</span></span> <span data-ttu-id="9a6fa-118">hello 暫存磁碟的應用程式和處理序提供短期儲存，預期的 tooonly 存放區資料，例如分頁檔。</span><span class="sxs-lookup"><span data-stu-id="9a6fa-118">hello temporary disk provides short-term storage for applications and processes and is intended tooonly store data such as page or swap files.</span></span> <span data-ttu-id="9a6fa-119">Hello 暫存磁碟上的資料可能會遺失期間[維護事件](../virtual-machines/windows/manage-availability.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json#understand-vm-reboots---maintenance-vs-downtime)或當您[重新部署 VM](../virtual-machines/windows/redeploy-to-new-node.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="9a6fa-119">Data on hello temporary disk may be lost during a [maintenance event](../virtual-machines/windows/manage-availability.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json#understand-vm-reboots---maintenance-vs-downtime) or when you [redeploy a VM](../virtual-machines/windows/redeploy-to-new-node.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> <span data-ttu-id="9a6fa-120">Hello VM 標準重開機，應保存 hello hello 暫存磁碟機上的資料。</span><span class="sxs-lookup"><span data-stu-id="9a6fa-120">During a standard reboot of hello VM, hello data on hello temporary drive should persist.</span></span>

<span data-ttu-id="9a6fa-121">hello 暫存磁碟標示為 hello d： 磁碟機上，依預設，它用來儲存 pagefile.sys。</span><span class="sxs-lookup"><span data-stu-id="9a6fa-121">hello temporary disk is labeled as hello D: drive by default and it used for storing pagefile.sys.</span></span> <span data-ttu-id="9a6fa-122">tooremap 這個磁碟 tooa 不同磁碟機代號，請參閱[hello Windows 暫存磁碟的變更 hello 磁碟機代號](../virtual-machines/windows/change-drive-letter.md)。</span><span class="sxs-lookup"><span data-stu-id="9a6fa-122">tooremap this disk tooa different drive letter, see [Change hello drive letter of hello Windows temporary disk](../virtual-machines/windows/change-drive-letter.md).</span></span> <span data-ttu-id="9a6fa-123">hello hello 暫存磁碟的大小會根據 hello hello 虛擬機器大小而不同。</span><span class="sxs-lookup"><span data-stu-id="9a6fa-123">hello size of hello temporary disk varies, based on hello size of hello virtual machine.</span></span> <span data-ttu-id="9a6fa-124">如需詳細資訊，請參閱 [Windows 虛擬機器的大小](../virtual-machines/windows/sizes.md)。</span><span class="sxs-lookup"><span data-stu-id="9a6fa-124">For more information, see [Sizes for Windows virtual machines](../virtual-machines/windows/sizes.md).</span></span>

<span data-ttu-id="9a6fa-125">如需有關 Azure 的 hello 暫存磁碟的使用方式的詳細資訊，請參閱[了解 hello 暫存磁碟機上的 Microsoft Azure 虛擬機器](https://blogs.msdn.microsoft.com/mast/2013/12/06/understanding-the-temporary-drive-on-windows-azure-virtual-machines/)</span><span class="sxs-lookup"><span data-stu-id="9a6fa-125">For more information on how Azure uses hello temporary disk, see [Understanding hello temporary drive on Microsoft Azure Virtual Machines](https://blogs.msdn.microsoft.com/mast/2013/12/06/understanding-the-temporary-drive-on-windows-azure-virtual-machines/)</span></span>


### <a name="data-disk"></a><span data-ttu-id="9a6fa-126">資料磁碟</span><span class="sxs-lookup"><span data-stu-id="9a6fa-126">Data disk</span></span>
<span data-ttu-id="9a6fa-127">資料磁碟是附加的 tooa 虛擬機器 toostore 應用程式資料，或需要 tookeep 其他資料的 VHD。</span><span class="sxs-lookup"><span data-stu-id="9a6fa-127">A data disk is a VHD that's attached tooa virtual machine toostore application data, or other data you need tookeep.</span></span> <span data-ttu-id="9a6fa-128">資料磁碟註冊為 SCSI 磁碟機，並以您選擇的字母標示。</span><span class="sxs-lookup"><span data-stu-id="9a6fa-128">Data disks are registered as SCSI drives and are labeled with a letter that you choose.</span></span> <span data-ttu-id="9a6fa-129">每個資料磁碟具有 4095 GB 的最大容量。</span><span class="sxs-lookup"><span data-stu-id="9a6fa-129">Each data disk has a maximum capacity of 4095 GB.</span></span> <span data-ttu-id="9a6fa-130">hello hello 虛擬機器的大小會決定您可以將附加的儲存體，您可以使用 tooit 與 hello 類型的資料磁碟數目 toohost hello 磁碟。</span><span class="sxs-lookup"><span data-stu-id="9a6fa-130">hello size of hello virtual machine determines how many data disks you can attach tooit and hello type of storage you can use toohost hello disks.</span></span>

> [!NOTE]
> <span data-ttu-id="9a6fa-131">如需有關虛擬機器容量的詳細資訊，請參閱 [Windows 虛擬機器的大小](../virtual-machines/windows/sizes.md)。</span><span class="sxs-lookup"><span data-stu-id="9a6fa-131">For more information about virtual machines capacities, see [Sizes for Windows virtual machines](../virtual-machines/windows/sizes.md).</span></span>
> 

<span data-ttu-id="9a6fa-132">當您從映像建立虛擬機器時，Azure 會建立作業系統磁碟。</span><span class="sxs-lookup"><span data-stu-id="9a6fa-132">Azure creates an operating system disk when you create a virtual machine from an image.</span></span> <span data-ttu-id="9a6fa-133">如果您使用包含資料磁碟的映像時，Azure 也會建立 hello 資料磁碟時，它會建立 hello 虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="9a6fa-133">If you use an image that includes data disks, Azure also creates hello data disks when it creates hello virtual machine.</span></span> <span data-ttu-id="9a6fa-134">否則，您建立 hello 虛擬機器之後加入資料磁碟。</span><span class="sxs-lookup"><span data-stu-id="9a6fa-134">Otherwise, you add data disks after you create hello virtual machine.</span></span>

<span data-ttu-id="9a6fa-135">您可以新增任何時候，資料磁碟 tooa 虛擬機器由**附加**hello 磁碟 toohello 虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="9a6fa-135">You can add data disks tooa virtual machine at any time, by **attaching** hello disk toohello virtual machine.</span></span> <span data-ttu-id="9a6fa-136">您可以使用您已上傳或複製 tooyour 儲存體帳戶，或其中一個，Azure 會為您建立的 VHD。</span><span class="sxs-lookup"><span data-stu-id="9a6fa-136">You can use a VHD that you've uploaded or copied tooyour storage account, or one that Azure creates for you.</span></span> <span data-ttu-id="9a6fa-137">連接資料磁碟 hello VHD 檔案將與關聯 hello VM 「 租用 」 置於 hello VHD，因此無法加以刪除仍附加時從儲存體。</span><span class="sxs-lookup"><span data-stu-id="9a6fa-137">Attaching a data disk associates hello VHD file with hello VM by placing a 'lease' on hello VHD so it can't be deleted from storage while it's still attached.</span></span>


[!INCLUDE [storage-about-vhds-and-disks-windows-and-linux](../../includes/storage-about-vhds-and-disks-windows-and-linux.md)]

## <a name="one-last-recommendation-use-trim-with-unmanaged-standard-disks"></a><span data-ttu-id="9a6fa-138">最後一個建議：對非受控標準磁碟使用 TRIM</span><span class="sxs-lookup"><span data-stu-id="9a6fa-138">One last recommendation: Use TRIM with unmanaged standard disks</span></span> 

<span data-ttu-id="9a6fa-139">如果您使用非受控標準儲存體 (HDD)，您應該啟用 TRIM。</span><span class="sxs-lookup"><span data-stu-id="9a6fa-139">If you use unmanaged standard disks (HDD), you should enable TRIM.</span></span> <span data-ttu-id="9a6fa-140">空白位置修剪會捨棄 hello 磁碟上未使用的區塊，因此您只支付您實際使用的儲存體。</span><span class="sxs-lookup"><span data-stu-id="9a6fa-140">TRIM discards unused blocks on hello disk so you are only billed for storage that you are actually using.</span></span> <span data-ttu-id="9a6fa-141">如果您建立大型檔案，然後將它們刪除，這便可節省成本。</span><span class="sxs-lookup"><span data-stu-id="9a6fa-141">This can save on costs if you create large files and then delete them.</span></span> 

<span data-ttu-id="9a6fa-142">您可以執行此命令 toocheck hello 修剪設定。</span><span class="sxs-lookup"><span data-stu-id="9a6fa-142">You can run this command toocheck hello TRIM setting.</span></span> <span data-ttu-id="9a6fa-143">在您的 Windows VM 上開啟命令提示字元並輸入︰</span><span class="sxs-lookup"><span data-stu-id="9a6fa-143">Open a command prompt on your Windows VM and type:</span></span>


```
fsutil behavior query DisableDeleteNotify
```

<span data-ttu-id="9a6fa-144">Hello 命令傳回 0，如果已正確啟用修剪。</span><span class="sxs-lookup"><span data-stu-id="9a6fa-144">If hello command returns 0, TRIM is enabled correctly.</span></span> <span data-ttu-id="9a6fa-145">如果它傳回 1，執行下列命令 tooenable TRIM hello:</span><span class="sxs-lookup"><span data-stu-id="9a6fa-145">If it returns 1, run hello following command tooenable TRIM:</span></span>

```
fsutil behavior set DisableDeleteNotify 0
```

> [!NOTE]
> <span data-ttu-id="9a6fa-146">注意： 修剪支援啟動與 Windows Server 2012 / Windows 8 （含） 以上版本，請參閱請參閱[新 API 可讓應用程式 toosend"修剪和取消對應 」 提示 toostorage 媒體](https://msdn.microsoft.com/windows/compatibility/new-api-allows-apps-to-send-trim-and-unmap-hints)。</span><span class="sxs-lookup"><span data-stu-id="9a6fa-146">Note: Trim support starts with Windows Server 2012 / Windows 8 and above, see see [New API allows apps toosend "TRIM and Unmap" hints toostorage media](https://msdn.microsoft.com/windows/compatibility/new-api-allows-apps-to-send-trim-and-unmap-hints).</span></span>
> 

<!-- Might want toomatch next-steps from overview of managed disks -->
## <a name="next-steps"></a><span data-ttu-id="9a6fa-147">後續步驟</span><span class="sxs-lookup"><span data-stu-id="9a6fa-147">Next steps</span></span>
* <span data-ttu-id="9a6fa-148">[將磁碟連接](../virtual-machines/windows/attach-managed-disk-portal.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)vm tooadd 額外的存放裝置。</span><span class="sxs-lookup"><span data-stu-id="9a6fa-148">[Attach a disk](../virtual-machines/windows/attach-managed-disk-portal.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) tooadd additional storage for your VM.</span></span>
* <span data-ttu-id="9a6fa-149">[變更 hello 磁碟機代號 hello Windows 暫存磁碟](../virtual-machines/windows/change-drive-letter.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)讓您的應用程式的資料可以使用 hello d： 磁碟機。</span><span class="sxs-lookup"><span data-stu-id="9a6fa-149">[Change hello drive letter of hello Windows temporary disk](../virtual-machines/windows/change-drive-letter.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json) so your application can use hello D: drive for data.</span></span>

