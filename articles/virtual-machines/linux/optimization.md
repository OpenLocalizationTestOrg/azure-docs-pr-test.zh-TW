---
title: "aaaOptimize 您在 Azure 上的 Linux VM |Microsoft 文件"
description: "確定您已將您的 Linux VM，以獲得最佳效能，在 Azure 上設定某些最佳化提示 toomake 深入了解"
keywords: "linux 虛擬機器,虛擬機器 linux,ubuntu 虛擬機器"
services: virtual-machines-linux
documentationcenter: 
author: rickstercdn
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 8baa30c8-d40e-41ac-93d0-74e96fe18d4c
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 09/06/2016
ms.author: rclaus
ms.openlocfilehash: 89a9ac022928a2801a9a15e1c172340352745354
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="optimize-your-linux-vm-on-azure"></a><span data-ttu-id="fde00-104">在 Azure 上最佳化 Linux VM</span><span class="sxs-lookup"><span data-stu-id="fde00-104">Optimize your Linux VM on Azure</span></span>
<span data-ttu-id="fde00-105">建立 Linux 虛擬機器 (VM) 是簡單 toodo 從 hello 命令列或從 hello 入口網站。</span><span class="sxs-lookup"><span data-stu-id="fde00-105">Creating a Linux virtual machine (VM) is easy toodo from hello command line or from hello portal.</span></span> <span data-ttu-id="fde00-106">本教學課程會示範如何 tooensure 您設定它 toooptimize 其效能 hello Microsoft Azure 平台上。</span><span class="sxs-lookup"><span data-stu-id="fde00-106">This tutorial shows you how tooensure you have set it up toooptimize its performance on hello Microsoft Azure platform.</span></span> <span data-ttu-id="fde00-107">本主題會使用 Ubuntu Server VM，但您也可以使用 [自己的映像做為範本](create-upload-generic.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)來建立 Linux 虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="fde00-107">This topic uses an Ubuntu Server VM, but you can also create Linux virtual machine using [your own images as templates](create-upload-generic.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>  

## <a name="prerequisites"></a><span data-ttu-id="fde00-108">必要條件</span><span class="sxs-lookup"><span data-stu-id="fde00-108">Prerequisites</span></span>
<span data-ttu-id="fde00-109">本主題假設您已具備有效的 Azure 訂用帳戶 ([註冊免費試用版](https://azure.microsoft.com/pricing/free-trial/))，並且已在 Azure 訂用帳戶中佈建 VM。</span><span class="sxs-lookup"><span data-stu-id="fde00-109">This topic assumes you already have a working Azure subscription ([free trial signup](https://azure.microsoft.com/pricing/free-trial/)) and have already provisioned a VM into your Azure subscription.</span></span> <span data-ttu-id="fde00-110">請確定您擁有 hello 最新[Azure CLI 2.0](/cli/azure/install-az-cli2)安裝並登入 tooyour 與 Azure 訂用帳戶[az 登入](/cli/azure/#login)之前[建立 VM](quick-create-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="fde00-110">Make sure that you have hello latest [Azure CLI 2.0](/cli/azure/install-az-cli2) installed and logged in tooyour Azure subscription with [az login](/cli/azure/#login) before you [create a VM](quick-create-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

## <a name="azure-os-disk"></a><span data-ttu-id="fde00-111">Azure 作業系統磁碟</span><span class="sxs-lookup"><span data-stu-id="fde00-111">Azure OS Disk</span></span>
<span data-ttu-id="fde00-112">在 Azure 中建立 Linux VM 後，它有兩個相關聯的磁碟。</span><span class="sxs-lookup"><span data-stu-id="fde00-112">Once you create a Linux VM in Azure, it has two disks associated with it.</span></span> <span data-ttu-id="fde00-113">**/dev/sda** 是作業系統磁碟，**/dev/sdb** 是暫存磁碟。</span><span class="sxs-lookup"><span data-stu-id="fde00-113">**/dev/sda** is your OS disk, **/dev/sdb** is your temporary disk.</span></span>  <span data-ttu-id="fde00-114">請勿使用 hello 主要作業系統磁碟 (**/開發/sda**) 的 hello 作業系統，因為它以外的項目最適合用於快速 VM 開機時間，但未提供良好的效能，為您的工作負載。</span><span class="sxs-lookup"><span data-stu-id="fde00-114">Do not use hello main OS disk (**/dev/sda**) for anything except hello operating system as it is optimized for fast VM boot time and does not provide good performance for your workloads.</span></span> <span data-ttu-id="fde00-115">您想要 tooattach 其中一個或多個磁碟 tooyour VM tooget 持續性和最佳化儲存體的資料。</span><span class="sxs-lookup"><span data-stu-id="fde00-115">You want tooattach one or more disks tooyour VM tooget persistent and optimized storage for your data.</span></span> 

## <a name="adding-disks-for-size-and-performance-targets"></a><span data-ttu-id="fde00-116">加入磁碟以達成大小和效能目標</span><span class="sxs-lookup"><span data-stu-id="fde00-116">Adding Disks for Size and Performance targets</span></span>
<span data-ttu-id="fde00-117">根據 hello VM 大小，您可以附加 too16 額外的磁碟上 A 系列、 D 系列上的 32 磁碟和 G 系列電腦-每個向上 too1 TB 大小上的 64 部磁碟。</span><span class="sxs-lookup"><span data-stu-id="fde00-117">Based on hello VM size, you can attach up too16 additional disks on an A-Series, 32 disks on a D-Series and 64 disks on a G-Series machine - each up too1 TB in size.</span></span> <span data-ttu-id="fde00-118">您可以根據空間和 IOps 需求加入額外的磁碟。</span><span class="sxs-lookup"><span data-stu-id="fde00-118">You add extra disks as needed per your space and IOps requirements.</span></span> <span data-ttu-id="fde00-119">每個磁碟具有 500 IOps 效能的目標，標準儲存體及其上層 too5000 每個磁碟的 IOps Premium 儲存體。</span><span class="sxs-lookup"><span data-stu-id="fde00-119">Each disk has a performance target of 500 IOps for Standard Storage and up too5000 IOps per disk for Premium Storage.</span></span>  <span data-ttu-id="fde00-120">如需進階儲存體磁碟的詳細資訊，請參閱[進階儲存體：Azure VM 的高效能儲存體](../../storage/common/storage-premium-storage.md)</span><span class="sxs-lookup"><span data-stu-id="fde00-120">For more information about Premium Storage disks, see [Premium Storage: High-Performance Storage for Azure VMs](../../storage/common/storage-premium-storage.md)</span></span>

<span data-ttu-id="fde00-121">tooachieve hello 其快取設定具有已設定的 tooeither Premium 儲存體磁碟上的最高 IOps **ReadOnly**或**無**，您必須停用**障礙**時在 Linux 中掛接 hello 檔案系統。</span><span class="sxs-lookup"><span data-stu-id="fde00-121">tooachieve hello highest IOps on Premium Storage disks where their cache settings have been set tooeither **ReadOnly** or **None**, you must disable **barriers** while mounting hello file system in Linux.</span></span> <span data-ttu-id="fde00-122">因為 hello 寫入 tooPremium 儲存備份的磁碟是永久性的這些快取設定不需要的障礙。</span><span class="sxs-lookup"><span data-stu-id="fde00-122">You do not need barriers because hello writes tooPremium Storage backed disks are durable for these cache settings.</span></span>

* <span data-ttu-id="fde00-123">如果您使用**reiserFS**、 使用 hello 掛接選項停用障礙`barrier=none`(啟用的障礙，使用`barrier=flush`)</span><span class="sxs-lookup"><span data-stu-id="fde00-123">If you use **reiserFS**, disable barriers using hello mount option `barrier=none` (For enabling barriers, use `barrier=flush`)</span></span>
* <span data-ttu-id="fde00-124">如果您使用**ext3/ext4**、 使用 hello 掛接選項停用障礙`barrier=0`(啟用的障礙，使用`barrier=1`)</span><span class="sxs-lookup"><span data-stu-id="fde00-124">If you use **ext3/ext4**, disable barriers using hello mount option `barrier=0` (For enabling barriers, use `barrier=1`)</span></span>
* <span data-ttu-id="fde00-125">如果您使用**XFS**、 使用 hello 掛接選項停用障礙`nobarrier`(啟用的障礙，使用 hello 選項`barrier`)</span><span class="sxs-lookup"><span data-stu-id="fde00-125">If you use **XFS**, disable barriers using hello mount option `nobarrier` (For enabling barriers, use hello option `barrier`)</span></span>

## <a name="unmanaged-storage-account-considerations"></a><span data-ttu-id="fde00-126">非受控儲存體帳戶考量事項</span><span class="sxs-lookup"><span data-stu-id="fde00-126">Unmanaged storage account considerations</span></span>
<span data-ttu-id="fde00-127">當您使用 hello Azure CLI 2.0 來建立 VM 的 hello 的預設動作是 toouse Azure 受管理的磁碟。</span><span class="sxs-lookup"><span data-stu-id="fde00-127">hello default action when you create a VM with hello Azure CLI 2.0 is toouse Azure Managed Disks.</span></span>  <span data-ttu-id="fde00-128">這些磁碟都由 hello Azure 平台，而且不需要任何準備或位置 toostore 它們。</span><span class="sxs-lookup"><span data-stu-id="fde00-128">These disks are handled by hello Azure platform and do not require any preparation or location toostore them.</span></span>  <span data-ttu-id="fde00-129">非受控磁碟需要儲存體帳戶，且具有一些額外的效能注意事項。</span><span class="sxs-lookup"><span data-stu-id="fde00-129">Unmanaged disks require a storage account and have some additional performance considerations.</span></span>  <span data-ttu-id="fde00-130">如需受控磁碟的詳細資訊，請參閱 [Azure 受控磁碟概觀](../windows/managed-disks-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="fde00-130">For more information about managed disks, see [Azure Managed Disks overview](../windows/managed-disks-overview.md).</span></span>  <span data-ttu-id="fde00-131">hello 下列各節概述效能考量僅當您使用未受管理的磁碟。</span><span class="sxs-lookup"><span data-stu-id="fde00-131">hello following section outlines performance considerations only when you use unmanaged disks.</span></span>  <span data-ttu-id="fde00-132">同樣地，hello 預設和建議的儲存體解決方案是 toouse 管理磁碟。</span><span class="sxs-lookup"><span data-stu-id="fde00-132">Again, hello default and recommended storage solution is toouse managed disks.</span></span>

<span data-ttu-id="fde00-133">如果您建立未受管理磁碟 VM，請確定您將磁碟附加來自相同位於 hello 的儲存體帳戶與 VM tooensure 區域接近和網路延遲降至最低。</span><span class="sxs-lookup"><span data-stu-id="fde00-133">If you create a VM with unmanaged disks, make sure that you attach disks from storage accounts residing in hello same region as your VM tooensure close proximity and minimize network latency.</span></span>  <span data-ttu-id="fde00-134">每個標準儲存體帳戶都有最高 20k 的 IOps 和 500 TB 大小的容量。</span><span class="sxs-lookup"><span data-stu-id="fde00-134">Each Standard storage account has a maximum of 20k IOps and a 500 TB size capacity.</span></span>  <span data-ttu-id="fde00-135">這項限制適用於出 tooapproximately 40 大量使用磁碟，包括 hello OS 磁碟和任何您所建立的資料磁碟。</span><span class="sxs-lookup"><span data-stu-id="fde00-135">This  limit works out tooapproximately 40 heavily used disks including both hello OS disk and any data disks you create.</span></span> <span data-ttu-id="fde00-136">進階儲存體帳戶沒有 IOps 上限，不過有 32 TB 的大小限制。</span><span class="sxs-lookup"><span data-stu-id="fde00-136">For Premium Storage accounts, there is no Maximum IOps limit but there is a 32 TB size limit.</span></span> 

<span data-ttu-id="fde00-137">當處理高 IOps 工作負載，而且您已選擇標準儲存體的磁碟時，您可能需要 toosplit hello 磁碟跨多個儲存體帳戶 toomake 確定不叫用的 hello 20,000 IOps 限制標準儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="fde00-137">When dealing with high IOps workloads and you have chosen Standard Storage for your disks, you might need toosplit hello disks across multiple storage accounts toomake sure you have not hit hello 20,000 IOps limit for Standard Storage accounts.</span></span> <span data-ttu-id="fde00-138">您的 VM 可以包含混合的磁碟跨不同的儲存體帳戶和儲存體帳戶類型 tooachieve 最佳的設定。</span><span class="sxs-lookup"><span data-stu-id="fde00-138">Your VM can contain a mix of disks from across different storage accounts and storage account types tooachieve your optimal configuration.</span></span>
 

## <a name="your-vm-temporary-drive"></a><span data-ttu-id="fde00-139">VM 暫存磁碟機</span><span class="sxs-lookup"><span data-stu-id="fde00-139">Your VM Temporary drive</span></span>
<span data-ttu-id="fde00-140">根據預設，當您建立 VM 時，Azure 會提供作業系統磁碟 (**/dev/sda**) 和暫存磁碟 (**/dev/sdb**)。</span><span class="sxs-lookup"><span data-stu-id="fde00-140">By default when you create a VM, Azure provides you with an OS disk (**/dev/sda**) and a temporary disk (**/dev/sdb**).</span></span>  <span data-ttu-id="fde00-141">您加入的所有額外磁碟會顯示為 **/dev/sdc**、**/dev/sdd**、**/dev/sde**，依此類推。</span><span class="sxs-lookup"><span data-stu-id="fde00-141">All additional disks you add show up as **/dev/sdc**, **/dev/sdd**, **/dev/sde** and so on.</span></span> <span data-ttu-id="fde00-142">暫存磁碟 (**/dev/sdb**) 上的所有資料均不具持久性，因此當 VM 調整大小、重新部署或維護等特定事件發生迫使 VM 重新啟動時，資料可能會遺失。</span><span class="sxs-lookup"><span data-stu-id="fde00-142">All data on your temporary disk (**/dev/sdb**) is not durable, and can be lost if specific events like VM Resizing, redeployment, or maintenance forces a restart of your VM.</span></span>  <span data-ttu-id="fde00-143">hello 大小與類型的暫存磁碟是您選擇在部署階段的相關的 toohello VM 大小。</span><span class="sxs-lookup"><span data-stu-id="fde00-143">hello size and type of your temporary disk is related toohello VM size you chose at deployment time.</span></span> <span data-ttu-id="fde00-144">Hello premium 大小 Vm （DS、 G 和 DS_V2 系列） hello 暫存磁碟機的所有備份的本機 SSD 的總 too48k IOps 的其他效能。</span><span class="sxs-lookup"><span data-stu-id="fde00-144">All of hello premium size VMs (DS, G, and DS_V2 series) hello temporary drive are backed by a local SSD for additional performance of up too48k IOps.</span></span> 

## <a name="linux-swap-file"></a><span data-ttu-id="fde00-145">Linux 交換檔</span><span class="sxs-lookup"><span data-stu-id="fde00-145">Linux Swap File</span></span>
<span data-ttu-id="fde00-146">如果您的 Azure VM 從 Ubuntu 或 CoreOS 映像，您可以使用 CustomData toosend 雲端組態 toocloud init。</span><span class="sxs-lookup"><span data-stu-id="fde00-146">If your Azure VM is from an Ubuntu or CoreOS image, then you can use CustomData toosend a cloud-config toocloud-init.</span></span> <span data-ttu-id="fde00-147">如果您[上傳自訂 Linux 映像](upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)，使用 cloud-init，您也可以使用 cloud-init 設定交換資料分割。</span><span class="sxs-lookup"><span data-stu-id="fde00-147">If you [uploaded a custom Linux image](upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) that uses cloud-init, you also configure swap partitions using cloud-init.</span></span>

<span data-ttu-id="fde00-148">Ubuntu 雲端映像，您必須使用雲端 init tooconfigure hello 交換資料分割。</span><span class="sxs-lookup"><span data-stu-id="fde00-148">On Ubuntu Cloud Images, you must use cloud-init tooconfigure hello swap partition.</span></span> <span data-ttu-id="fde00-149">如需詳細資訊，請參閱 [AzureSwapPartitions](https://wiki.ubuntu.com/AzureSwapPartitions)。</span><span class="sxs-lookup"><span data-stu-id="fde00-149">For more information, see [AzureSwapPartitions](https://wiki.ubuntu.com/AzureSwapPartitions).</span></span>

<span data-ttu-id="fde00-150">沒有雲端 init 支援的映像，從 hello Azure Marketplace 部署的 VM 映像會有與 hello OS 整合的 Linux VM 代理程式。</span><span class="sxs-lookup"><span data-stu-id="fde00-150">For images without cloud-init support, VM images deployed from hello Azure Marketplace have a VM Linux Agent integrated with hello OS.</span></span> <span data-ttu-id="fde00-151">此代理程式可讓您將 VM toointeract hello 與不同 Azure 服務。</span><span class="sxs-lookup"><span data-stu-id="fde00-151">This agent allows hello VM toointeract with various Azure services.</span></span> <span data-ttu-id="fde00-152">假設您已部署的 hello Azure Marketplace 的標準映像，您就必須 toodo hello 遵循 toocorrectly 設定設定 Linux 交換檔：</span><span class="sxs-lookup"><span data-stu-id="fde00-152">Assuming you have deployed a standard image from hello Azure Marketplace, you would need toodo hello following toocorrectly configure your Linux swap file settings:</span></span>

<span data-ttu-id="fde00-153">找出和修改兩個項目在 hello **/etc/waagent.conf**檔案。</span><span class="sxs-lookup"><span data-stu-id="fde00-153">Locate and modify two entries in hello **/etc/waagent.conf** file.</span></span> <span data-ttu-id="fde00-154">它們控制 hello 存在專用的交換檔案和 hello 分頁檔大小。</span><span class="sxs-lookup"><span data-stu-id="fde00-154">They control hello existence of a dedicated swap file and size of hello swap file.</span></span> <span data-ttu-id="fde00-155">您要尋找 toomodify hello 參數`ResourceDisk.EnableSwap=N`和`ResourceDisk.SwapSizeMB=0`</span><span class="sxs-lookup"><span data-stu-id="fde00-155">hello parameters you are looking toomodify are `ResourceDisk.EnableSwap=N` and `ResourceDisk.SwapSizeMB=0`</span></span> 

<span data-ttu-id="fde00-156">變更 hello 參數 toohello 下列設定：</span><span class="sxs-lookup"><span data-stu-id="fde00-156">Change hello parameters toohello following settings:</span></span>

* <span data-ttu-id="fde00-157">ResourceDisk.EnableSwap=Y</span><span class="sxs-lookup"><span data-stu-id="fde00-157">ResourceDisk.EnableSwap=Y</span></span>
* <span data-ttu-id="fde00-158">ResourceDisk.SwapSizeMB={size MB toomeet 在您的需求。</span><span class="sxs-lookup"><span data-stu-id="fde00-158">ResourceDisk.SwapSizeMB={size in MB toomeet your needs}</span></span> 

<span data-ttu-id="fde00-159">一旦您所做變更的 hello，您需要 toorestart hello waagent 或重新啟動 Linux VM tooreflect 這些變更。</span><span class="sxs-lookup"><span data-stu-id="fde00-159">Once you have made hello change, you need toorestart hello waagent or restart your Linux VM tooreflect those changes.</span></span>  <span data-ttu-id="fde00-160">您知道實作 hello 變更，而且交換檔已經建立，當您使用 hello`free`命令 tooview 可用空間。</span><span class="sxs-lookup"><span data-stu-id="fde00-160">You know hello changes have been implemented and a swap file has been created when you use hello `free` command tooview free space.</span></span> <span data-ttu-id="fde00-161">hello 下列範例具有 512 MB 交換檔建立的結果修改 hello **waagent.conf**檔案：</span><span class="sxs-lookup"><span data-stu-id="fde00-161">hello following example has a 512MB swap file created as a result of modifying hello **waagent.conf** file:</span></span>

```bash
azuseruser@myVM:~$ free
            total       used       free     shared    buffers     cached
Mem:       3525156     804168    2720988        408       8428     633192
-/+ buffers/cache:     162548    3362608
Swap:       524284          0     524284
```

## <a name="io-scheduling-algorithm-for-premium-storage"></a><span data-ttu-id="fde00-162">進階儲存體的 I/O 排程演算法</span><span class="sxs-lookup"><span data-stu-id="fde00-162">I/O scheduling algorithm for Premium Storage</span></span>
<span data-ttu-id="fde00-163">與 hello 2.6.18 Linux 核心，hello 預設 I/O 排程演算法已經從期限 tooCFQ （完全公平佇列演算法）。</span><span class="sxs-lookup"><span data-stu-id="fde00-163">With hello 2.6.18 Linux kernel, hello default I/O scheduling algorithm was changed from Deadline tooCFQ (Completely fair queuing algorithm).</span></span> <span data-ttu-id="fde00-164">對於隨機 I/O 模式，CFQ 與期限之間的效能差異並不明顯。</span><span class="sxs-lookup"><span data-stu-id="fde00-164">For random access I/O patterns, there is negligible difference in performance differences between CFQ and Deadline.</span></span>  <span data-ttu-id="fde00-165">Ssd 磁碟 hello 磁碟 I/O 模式，主要是循序，切換回 toohello NOOP 或期限演算法可以達到較佳的 I/O 效能。</span><span class="sxs-lookup"><span data-stu-id="fde00-165">For SSD-based disks where hello disk I/O pattern is predominantly sequential, switching back toohello NOOP or Deadline algorithm can achieve better I/O performance.</span></span>

### <a name="view-hello-current-io-scheduler"></a><span data-ttu-id="fde00-166">檢視 hello 目前 I/O 排程器</span><span class="sxs-lookup"><span data-stu-id="fde00-166">View hello current I/O scheduler</span></span>
<span data-ttu-id="fde00-167">使用下列命令的 hello:</span><span class="sxs-lookup"><span data-stu-id="fde00-167">Use hello following command:</span></span>  

```bash
cat /sys/block/sda/queue/scheduler
```

<span data-ttu-id="fde00-168">您會看到下列輸出，表示 hello 目前排程器。</span><span class="sxs-lookup"><span data-stu-id="fde00-168">You see following output, which indicates hello current scheduler.</span></span>  

```bash
noop [deadline] cfq
```

### <a name="change-hello-current-device-devsda-of-io-scheduling-algorithm"></a><span data-ttu-id="fde00-169">變更 hello 目前的裝置 (/ 開發/sda) 的排程演算法的 I/O</span><span class="sxs-lookup"><span data-stu-id="fde00-169">Change hello current device (/dev/sda) of I/O scheduling algorithm</span></span>
<span data-ttu-id="fde00-170">使用下列命令的 hello:</span><span class="sxs-lookup"><span data-stu-id="fde00-170">Use hello following commands:</span></span>  

```bash
azureuser@myVM:~$ sudo su -
root@myVM:~# echo "noop" >/sys/block/sda/queue/scheduler
root@myVM:~# sed -i 's/GRUB_CMDLINE_LINUX=""/GRUB_CMDLINE_LINUX_DEFAULT="quiet splash elevator=noop"/g' /etc/default/grub
root@myVM:~# update-grub
```

> [!NOTE]
> <span data-ttu-id="fde00-171">單獨針對 **/dev/sda** 套用此設定不是很有用。</span><span class="sxs-lookup"><span data-stu-id="fde00-171">Applying this setting for **/dev/sda** alone is not useful.</span></span> <span data-ttu-id="fde00-172">所有資料磁碟上設定了該位置循序 I/O 將優先於 hello I/O 模式。</span><span class="sxs-lookup"><span data-stu-id="fde00-172">Set on all data disks where sequential I/O dominates hello I/O pattern.</span></span>  

<span data-ttu-id="fde00-173">您應該會看到下列輸出，表示 hello **grub.cfg**已成功重建，且該 hello 預設排程器已更新的 tooNOOP。</span><span class="sxs-lookup"><span data-stu-id="fde00-173">You should see hello following output, indicating that **grub.cfg** has been rebuilt successfully and that hello default scheduler has been updated tooNOOP.</span></span>  

```bash
Generating grub configuration file ...
Found linux image: /boot/vmlinuz-3.13.0-34-generic
Found initrd image: /boot/initrd.img-3.13.0-34-generic
Found linux image: /boot/vmlinuz-3.13.0-32-generic
Found initrd image: /boot/initrd.img-3.13.0-32-generic
Found memtest86+ image: /memtest86+.elf
Found memtest86+ image: /memtest86+.bin
done
```

<span data-ttu-id="fde00-174">Hello Redhat 發佈系列，您只需要 hello 下列命令：</span><span class="sxs-lookup"><span data-stu-id="fde00-174">For hello Redhat distribution family, you only need hello following command:</span></span>   

```bash
echo 'echo noop >/sys/block/sda/queue/scheduler' >> /etc/rc.local
```

## <a name="using-software-raid-tooachieve-higher-iops"></a><span data-ttu-id="fde00-175">使用較高的軟體 RAID tooachieve 我 / Ops</span><span class="sxs-lookup"><span data-stu-id="fde00-175">Using Software RAID tooachieve higher I/Ops</span></span>
<span data-ttu-id="fde00-176">如果您的工作負載需要更多的 IOps 比單一磁碟可提供，您會需要 toouse 軟體 RAID 組態的多個磁碟。</span><span class="sxs-lookup"><span data-stu-id="fde00-176">If your workloads require more IOps than a single disk can provide, you need toouse a software RAID configuration of multiple disks.</span></span> <span data-ttu-id="fde00-177">因為 Azure 已經執行 hello 本機網狀架構層級的磁碟復原，您會達成 hello 最高從 RAID 0 等量配置設定的效能層級。</span><span class="sxs-lookup"><span data-stu-id="fde00-177">Because Azure already performs disk resiliency at hello local fabric layer, you achieve hello highest level of performance from a RAID-0 striping configuration.</span></span>  <span data-ttu-id="fde00-178">佈建和 hello Azure 環境中建立磁碟，並將它們附加 tooyour Linux VM，資料分割、 格式化及裝載 hello 磁碟機之前。</span><span class="sxs-lookup"><span data-stu-id="fde00-178">Provision and create disks in hello Azure environment and attach them tooyour Linux VM before partitioning, formatting and mounting hello drives.</span></span>  <span data-ttu-id="fde00-179">需在 azure 中 Linux VM 上設定軟體 RAID 安裝程式的詳細資訊，請參閱 hello  **[Linux 上的 [設定軟體 RAID](configure-raid.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)** 文件。</span><span class="sxs-lookup"><span data-stu-id="fde00-179">More details on configuring a software RAID setup on your Linux VM in azure can be found in hello **[Configuring Software RAID on Linux](configure-raid.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)** document.</span></span>

## <a name="next-steps"></a><span data-ttu-id="fde00-180">後續步驟</span><span class="sxs-lookup"><span data-stu-id="fde00-180">Next Steps</span></span>
<span data-ttu-id="fde00-181">請記住，所有的最佳化討論中，您需要 tooperform 測試之前和之後每個變更 toomeasure hello 影響 hello 項變更有。</span><span class="sxs-lookup"><span data-stu-id="fde00-181">Remember, as with all optimization discussions, you need tooperform tests before and after each change toomeasure hello impact hello change has.</span></span>  <span data-ttu-id="fde00-182">最佳化是需要逐步進行的程序，這些程序會對環境中不同的機器產生不同的結果。</span><span class="sxs-lookup"><span data-stu-id="fde00-182">Optimization is a step by step process that has different results across different machines in your environment.</span></span>  <span data-ttu-id="fde00-183">對某項組態有用的做法不見得適用於其他組態。</span><span class="sxs-lookup"><span data-stu-id="fde00-183">What works for one configuration may not work for others.</span></span>

<span data-ttu-id="fde00-184">一些有用連結 tooadditional 的資源：</span><span class="sxs-lookup"><span data-stu-id="fde00-184">Some useful links tooadditional resources:</span></span> 

* [<span data-ttu-id="fde00-185">進階儲存體：Azure 虛擬機器工作負載適用的高效能儲存體</span><span class="sxs-lookup"><span data-stu-id="fde00-185">Premium Storage: High-Performance Storage for Azure Virtual Machine Workloads</span></span>](../../storage/common/storage-premium-storage.md)
* [<span data-ttu-id="fde00-186">Azure Linux 代理程式使用者指南</span><span class="sxs-lookup"><span data-stu-id="fde00-186">Azure Linux Agent User Guide</span></span>](../windows/agent-user-guide.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [<span data-ttu-id="fde00-187">在 Azure Linux VM 上最佳化 MySQL 效能</span><span class="sxs-lookup"><span data-stu-id="fde00-187">Optimizing MySQL Performance on Azure Linux VMs</span></span>](classic/optimize-mysql.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)
* [<span data-ttu-id="fde00-188">在 Linux 上設定軟體 RAID</span><span class="sxs-lookup"><span data-stu-id="fde00-188">Configure Software RAID on Linux</span></span>](configure-raid.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

