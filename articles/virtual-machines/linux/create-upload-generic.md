---
title: "aaaCreate 和上傳 Linux VHD 在 Azure 中"
description: "了解 toocreate 和上傳 Azure 虛擬硬碟 (VHD)，其中包含 Linux 作業系統。"
services: virtual-machines-linux
documentationcenter: 
author: szarkos
manager: timlt
editor: tysonn
tags: azure-resource-manager,azure-service-management
ms.assetid: d351396c-95a0-4092-b7bf-c6aae0bbd112
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 02/02/2017
ms.author: szark
ms.openlocfilehash: 208e15c035edb5520fc29ba8e4e71c42b041864d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="information-for-non-endorsed-distributions"></a><span data-ttu-id="7e398-103">非背書散發套件的資訊</span><span class="sxs-lookup"><span data-stu-id="7e398-103">Information for Non-Endorsed Distributions</span></span>
[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-both-include.md)]

<span data-ttu-id="7e398-104">hello Azure 平台 SLA 適用於執行 Linux 作業系統，僅當一 hello toovirtual 機器的 hello[背書分佈](endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)用。</span><span class="sxs-lookup"><span data-stu-id="7e398-104">hello Azure platform SLA applies toovirtual machines running hello Linux OS only when one of hello [endorsed distributions](endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) is used.</span></span> <span data-ttu-id="7e398-105">在 hello Azure 映像庫所提供的所有 Linux 散發都背書分佈利用 hello 必要的設定。</span><span class="sxs-lookup"><span data-stu-id="7e398-105">All Linux distributions that are provided in hello Azure image gallery are endorsed distributions with hello required configuration.</span></span>

* [<span data-ttu-id="7e398-106">Azure 背書散發套件上的 Linux</span><span class="sxs-lookup"><span data-stu-id="7e398-106">Linux on Azure - Endorsed Distributions</span></span>](endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [<span data-ttu-id="7e398-107">支援 Microsoft Azure 中的 Linux 映像</span><span class="sxs-lookup"><span data-stu-id="7e398-107">Support for Linux images in Microsoft Azure</span></span>](https://support.microsoft.com/kb/2941892)

<span data-ttu-id="7e398-108">在 Azure 上執行的所有分佈都需要 toomeet 必要條件 toohave hello 平台上執行的機率 tooproperly 數。</span><span class="sxs-lookup"><span data-stu-id="7e398-108">All distributions running on Azure will need toomeet a number of prerequisites toohave a chance tooproperly run on hello platform.</span></span>  <span data-ttu-id="7e398-109">本文並不是完整因為每個分佈是不同;然而，很可能即使您符合所有 hello 下列條件仍然需要 toosignificantly 調整您 Linux 系統 tooensure hello 平台上正常執行。</span><span class="sxs-lookup"><span data-stu-id="7e398-109">This article is by no means comprehensive as every distribution is different; and it is quite possible that even if you meet all hello criteria below you will still need toosignificantly tweak your Linux system tooensure that it properly runs on hello platform.</span></span>

<span data-ttu-id="7e398-110">基於這個原因，我們建議您盡可能從其中一個 [Azure 背書散發套件上的 Linux](endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) 開始著手。</span><span class="sxs-lookup"><span data-stu-id="7e398-110">It is for this reason that we recommend that you start with one of our [Linux on Azure Endorsed Distributions](endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) when possible.</span></span> <span data-ttu-id="7e398-111">hello 下列文件將引導您完成 tooprepare 如何 hello 各種背書在 Azure 受支援的 Linux 散發套件：</span><span class="sxs-lookup"><span data-stu-id="7e398-111">hello following articles will guide you through how tooprepare hello various endorsed Linux distributions that are supported on Azure:</span></span>

* <span data-ttu-id="7e398-112">**[CentOS 型散發套件](create-upload-centos.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span><span class="sxs-lookup"><span data-stu-id="7e398-112">**[CentOS-based Distributions](create-upload-centos.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span></span>
* <span data-ttu-id="7e398-113">**[Debian Linux](debian-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span><span class="sxs-lookup"><span data-stu-id="7e398-113">**[Debian Linux](debian-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span></span>
* <span data-ttu-id="7e398-114">**[Oracle Linux](oracle-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span><span class="sxs-lookup"><span data-stu-id="7e398-114">**[Oracle Linux](oracle-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span></span>
* <span data-ttu-id="7e398-115">**[Red Hat Enterprise Linux](redhat-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span><span class="sxs-lookup"><span data-stu-id="7e398-115">**[Red Hat Enterprise Linux](redhat-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span></span>
* <span data-ttu-id="7e398-116">**[SLES 和 openSUSE](suse-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span><span class="sxs-lookup"><span data-stu-id="7e398-116">**[SLES & openSUSE](suse-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span></span>
* <span data-ttu-id="7e398-117">**[Ubuntu](create-upload-ubuntu.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span><span class="sxs-lookup"><span data-stu-id="7e398-117">**[Ubuntu](create-upload-ubuntu.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span></span>

<span data-ttu-id="7e398-118">hello 本文其餘部分將著重在 Azure 上執行您的 Linux 散發套件的一般指引。</span><span class="sxs-lookup"><span data-stu-id="7e398-118">hello rest of this article will focus on general guidance for running your Linux distribution on Azure.</span></span>

## <a name="general-linux-installation-notes"></a><span data-ttu-id="7e398-119">一般 Linux 安裝注意事項</span><span class="sxs-lookup"><span data-stu-id="7e398-119">General Linux Installation Notes</span></span>
* <span data-ttu-id="7e398-120">hello VHDX 格式不支援在 Azure 中，只有**固定 VHD**。</span><span class="sxs-lookup"><span data-stu-id="7e398-120">hello VHDX format is not supported in Azure, only **fixed VHD**.</span></span>  <span data-ttu-id="7e398-121">您可以將使用 HYPER-V 管理員 hello 磁碟 tooVHD 格式轉換或 hello convert-vhd 指令程式。</span><span class="sxs-lookup"><span data-stu-id="7e398-121">You can convert hello disk tooVHD format using Hyper-V Manager or hello convert-vhd cmdlet.</span></span> <span data-ttu-id="7e398-122">如果您使用 VirtualBox 這表示選取**固定大小**為相對於 toohello 預設建立 hello 磁碟時，動態配置。</span><span class="sxs-lookup"><span data-stu-id="7e398-122">If you are using VirtualBox this means selecting **Fixed size** as opposed toohello default dynamically allocated when creating hello disk.</span></span>
* <span data-ttu-id="7e398-123">Azure 僅支援第 1 代虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="7e398-123">Azure only supports generation 1 virtual machines.</span></span> <span data-ttu-id="7e398-124">您可以將某個層代 1 個虛擬機器從 VHDX toohello VHD 檔案格式及動態擴充 tooa 固定大小磁碟的轉換。</span><span class="sxs-lookup"><span data-stu-id="7e398-124">You can convert a generation 1 virtual machine from VHDX toohello VHD file format and from dynamically expanding tooa fixed sized disk.</span></span> <span data-ttu-id="7e398-125">但您無法變更虛擬機器的世代。</span><span class="sxs-lookup"><span data-stu-id="7e398-125">But you can't change a virtual machine's generation.</span></span> <span data-ttu-id="7e398-126">如需詳細資訊，請參閱[應該在 Hyper-V 中建立第 1 代還是第 2 代的虛擬機器？](https://technet.microsoft.com/en-us/windows-server-docs/compute/hyper-v/plan/should-i-create-a-generation-1-or-2-virtual-machine-in-hyper-v)</span><span class="sxs-lookup"><span data-stu-id="7e398-126">For more information, see [Should I create a generation 1 or 2 virtual machine in Hyper-V?](https://technet.microsoft.com/en-us/windows-server-docs/compute/hyper-v/plan/should-i-create-a-generation-1-or-2-virtual-machine-in-hyper-v)</span></span>
* <span data-ttu-id="7e398-127">hello 最大允許 hello VHD 為 1023 GB。</span><span class="sxs-lookup"><span data-stu-id="7e398-127">hello maximum size allowed for hello VHD is 1,023 GB.</span></span>
* <span data-ttu-id="7e398-128">安裝 hello Linux 系統時*建議*您使用標準的資料分割，而非 LVM （通常 hello 預設值為許多安裝）。</span><span class="sxs-lookup"><span data-stu-id="7e398-128">When installing hello Linux system it is *recommended* that you use standard partitions rather than LVM (often hello default for many installations).</span></span> <span data-ttu-id="7e398-129">這樣可避免與複製 Vm，LVM 名稱衝突，特別是當作業系統磁碟需要附加 toobe tooanother 相同的 VM 進行疑難排解。</span><span class="sxs-lookup"><span data-stu-id="7e398-129">This will avoid LVM name conflicts with cloned VMs, particularly if an OS disk ever needs toobe attached tooanother identical VM for troubleshooting.</span></span> <span data-ttu-id="7e398-130">如果願意，您可以在資料磁碟上使用 [LVM](configure-raid.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) 或 [RAID](configure-lvm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="7e398-130">[LVM](configure-lvm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) or [RAID](configure-raid.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) may be used on data disks.</span></span>
* <span data-ttu-id="7e398-131">需要掛接 UDF 檔案系統的核心支援。</span><span class="sxs-lookup"><span data-stu-id="7e398-131">Kernel support for mounting UDF file systems is required.</span></span> <span data-ttu-id="7e398-132">在第一次開機 Azure hello 上佈建組態會透過附加的 toohello 客體的 UDF 格式化媒體傳遞 toohello Linux VM。</span><span class="sxs-lookup"><span data-stu-id="7e398-132">At first boot on Azure hello provisioning configuration is passed toohello Linux VM via UDF-formatted media that is attached toohello guest.</span></span> <span data-ttu-id="7e398-133">hello Azure Linux 代理程式必須要能夠 toomount hello UDF 檔案系統 tooread 其組態，並佈建 hello VM。</span><span class="sxs-lookup"><span data-stu-id="7e398-133">hello Azure Linux agent must be able toomount hello UDF file system tooread its configuration and provision hello VM.</span></span>
* <span data-ttu-id="7e398-134">Linux Kernel 2.6.37 以下的版本不支援較大 VM 大小 Hyper-V 上的NUMA。</span><span class="sxs-lookup"><span data-stu-id="7e398-134">Linux kernel versions below 2.6.37 do not support NUMA on Hyper-V with larger VM sizes.</span></span> <span data-ttu-id="7e398-135">這個問題主要會影響較舊的分佈上游使用 hello Red Hat 2.6.32 核心及已修正 RHEL 6.6 (核心-2.6.32-504) 中。</span><span class="sxs-lookup"><span data-stu-id="7e398-135">This issue primarily impacts older distributions using hello upstream Red Hat 2.6.32 kernel, and was fixed in RHEL 6.6 (kernel-2.6.32-504).</span></span> <span data-ttu-id="7e398-136">執行自訂的核心超過 2.6.37 或較舊 RHEL 基礎核心非 2.6.32-504 必須設定系統 hello 開機參數`numa=off`hello 核心 grub.conf 在命令列上。</span><span class="sxs-lookup"><span data-stu-id="7e398-136">Systems running custom kernels older than 2.6.37, or RHEL-based kernels older than 2.6.32-504 must set hello boot parameter `numa=off` on hello kernel command-line in grub.conf.</span></span> <span data-ttu-id="7e398-137">如需詳細資訊，請參閱 Red Hat [KB 436883](https://access.redhat.com/solutions/436883)。</span><span class="sxs-lookup"><span data-stu-id="7e398-137">For more information see Red Hat [KB 436883](https://access.redhat.com/solutions/436883).</span></span>
* <span data-ttu-id="7e398-138">請勿設定 hello OS 磁碟交換資料分割。</span><span class="sxs-lookup"><span data-stu-id="7e398-138">Do not configure a swap partition on hello OS disk.</span></span> <span data-ttu-id="7e398-139">hello Linux 代理程式可以設定的 toocreate 交換磁碟上的檔案 hello 暫存資源。</span><span class="sxs-lookup"><span data-stu-id="7e398-139">hello Linux agent can be configured toocreate a swap file on hello temporary resource disk.</span></span>  <span data-ttu-id="7e398-140">相關資訊位於下列 hello 步驟。</span><span class="sxs-lookup"><span data-stu-id="7e398-140">More information about this can be found in hello steps below.</span></span>
* <span data-ttu-id="7e398-141">所有 hello Vhd 必須是 1 MB 的倍數的大小。</span><span class="sxs-lookup"><span data-stu-id="7e398-141">All of hello VHDs must have sizes that are multiples of 1 MB.</span></span>

### <a name="installing-kernel-modules-without-hyper-v"></a><span data-ttu-id="7e398-142">安裝不含 Hyper-V 的核心模組</span><span class="sxs-lookup"><span data-stu-id="7e398-142">Installing kernel modules without Hyper-V</span></span>
<span data-ttu-id="7e398-143">因此 Linux 需要特定的核心模組會安裝在 Azure 中的順序 toorun 時，azure 會 hello HYPER-V hypervisor 上執行。</span><span class="sxs-lookup"><span data-stu-id="7e398-143">Azure runs on hello Hyper-V hypervisor, so Linux requires that certain kernel modules are installed in order toorun in Azure.</span></span> <span data-ttu-id="7e398-144">如果您有建立於 HYPER-V 之外的 VM，hello Linux 的安裝程式不能包含 hello 驅動程式的 HYPER-V 中 （initrd 或 initramfs） hello 初始 ramdisk 除非其偵測它正在執行的 HYPER-V 環境。</span><span class="sxs-lookup"><span data-stu-id="7e398-144">If you have a VM that was created outside of Hyper-V, hello Linux installers may not include hello drivers for Hyper-V in hello initial ramdisk (initrd or initramfs) unless it detects that it is running an a Hyper-V environment.</span></span> <span data-ttu-id="7e398-145">當使用不同虛擬化 （亦即 Virtualbox、 KVM 等） 的系統 tooprepare Linux 映像，您可能需要至少 hello toorebuild hello initrd tooensure`hv_vmbus`和`hv_storvsc`hello 初始 ramdisk 核心模組可用。</span><span class="sxs-lookup"><span data-stu-id="7e398-145">When using a different virtualization system (i.e. Virtualbox, KVM, etc.) tooprepare your Linux image, you may need toorebuild hello initrd tooensure that at least hello `hv_vmbus` and `hv_storvsc` kernel modules are available on hello initial ramdisk.</span></span>  <span data-ttu-id="7e398-146">這在至少 hello 上游 Red Hat 發佈為基礎的系統上是已知的問題。</span><span class="sxs-lookup"><span data-stu-id="7e398-146">This is a known issue at least on systems based on hello upstream Red Hat distribution.</span></span>

<span data-ttu-id="7e398-147">重建 hello initrd 或 initramfs 映像的 hello 機制可能有所不同 hello 發佈。</span><span class="sxs-lookup"><span data-stu-id="7e398-147">hello mechanism for rebuilding hello initrd or initramfs image may vary depending on hello distribution.</span></span> <span data-ttu-id="7e398-148">請參閱您的發佈文件，或支援 hello 適當的程序。</span><span class="sxs-lookup"><span data-stu-id="7e398-148">Please consult your distribution's documentation or support for hello proper procedure.</span></span>  <span data-ttu-id="7e398-149">以下是一個範例的方式 toorebuild hello initrd 使用 hello`mkinitrd`公用程式：</span><span class="sxs-lookup"><span data-stu-id="7e398-149">Here is one example for how toorebuild hello initrd using hello `mkinitrd` utility:</span></span>

<span data-ttu-id="7e398-150">首先，請備份 hello 現有 initrd 映像：</span><span class="sxs-lookup"><span data-stu-id="7e398-150">First, back up hello existing initrd image:</span></span>

    # cd /boot
    # sudo cp initrd-`uname -r`.img  initrd-`uname -r`.img.bak

<span data-ttu-id="7e398-151">接下來，重建以 hello hello initrd`hv_vmbus`和`hv_storvsc`核心模組：</span><span class="sxs-lookup"><span data-stu-id="7e398-151">Next, rebuild hello initrd with hello `hv_vmbus` and `hv_storvsc` kernel modules:</span></span>

    # sudo mkinitrd --preload=hv_storvsc --preload=hv_vmbus -v -f initrd-`uname -r`.img `uname -r`


### <a name="resizing-vhds"></a><span data-ttu-id="7e398-152">調整 VHD 的大小</span><span class="sxs-lookup"><span data-stu-id="7e398-152">Resizing VHDs</span></span>
<span data-ttu-id="7e398-153">在 Azure 上的 VHD 映像必須對齊的虛擬大小 too1MB。</span><span class="sxs-lookup"><span data-stu-id="7e398-153">VHD images on Azure must have a virtual size aligned too1MB.</span></span>  <span data-ttu-id="7e398-154">一般而言，使用 Hyper-V 建立的 VHD 應已正確對應。</span><span class="sxs-lookup"><span data-stu-id="7e398-154">Typically, VHDs created using Hyper-V should already be aligned correctly.</span></span>  <span data-ttu-id="7e398-155">如果可能會收到錯誤訊息類似 toohello 遵循當您嘗試 toocreate 未正確對齊 hello VHD*映像*從您的 VHD:</span><span class="sxs-lookup"><span data-stu-id="7e398-155">If hello VHD is not aligned correctly then you may receive an error message similar toohello following when you attempt toocreate an *image* from your VHD:</span></span>

    "hello VHD http://<mystorageaccount>.blob.core.windows.net/vhds/MyLinuxVM.vhd has an unsupported virtual size of 21475270656 bytes. hello size must be a whole number (in MBs).”

<span data-ttu-id="7e398-156">tooremedy 這可以調整大小 hello VM 使用 hello HYPER-V 管理員主控台或 hello [RESIZE-VHD](http://technet.microsoft.com/library/hh848535.aspx) Powershell cmdlet。</span><span class="sxs-lookup"><span data-stu-id="7e398-156">tooremedy this you can resize hello VM using either hello Hyper-V Manager console or hello [Resize-VHD](http://technet.microsoft.com/library/hh848535.aspx) Powershell cmdlet.</span></span>  <span data-ttu-id="7e398-157">如果您不在 Windows 環境中執行它，建議您使用 toouse qemu img tooconvert （如有需要），並調整 hello VHD 的大小。</span><span class="sxs-lookup"><span data-stu-id="7e398-157">If you are not running in a Windows environment then it is recommended toouse qemu-img tooconvert (if needed) and resize hello VHD.</span></span>

> [!NOTE]
> <span data-ttu-id="7e398-158">qemu-img >=2.2.1 的版本中已知有 Bug 會導致 VHD 的格式不正確。</span><span class="sxs-lookup"><span data-stu-id="7e398-158">There is a known bug in qemu-img versions >=2.2.1 that results in an improperly formatted VHD.</span></span> <span data-ttu-id="7e398-159">hello 問題已修正在 QEMU 2.6。</span><span class="sxs-lookup"><span data-stu-id="7e398-159">hello issue has been fixed in QEMU 2.6.</span></span> <span data-ttu-id="7e398-160">建議 toouse qemu img 2.2.0 或較低或更新 too2.6 或更高版本。</span><span class="sxs-lookup"><span data-stu-id="7e398-160">It is recommended toouse either qemu-img 2.2.0 or lower, or update too2.6 or higher.</span></span> <span data-ttu-id="7e398-161">參考︰https://bugs.launchpad.net/qemu/+bug/1490611。</span><span class="sxs-lookup"><span data-stu-id="7e398-161">Reference: https://bugs.launchpad.net/qemu/+bug/1490611.</span></span>
> 
> 

1. <span data-ttu-id="7e398-162">調整大小 hello 直接使用工具，例如 VHD`qemu-img`或`vbox-manage`可能會導致無法開機的 VHD。</span><span class="sxs-lookup"><span data-stu-id="7e398-162">Resizing hello VHD directly using tools such as `qemu-img` or `vbox-manage` may result in an unbootable VHD.</span></span>  <span data-ttu-id="7e398-163">因此，建議您使用 toofirst convert hello VHD tooa 原始磁碟映像。</span><span class="sxs-lookup"><span data-stu-id="7e398-163">So it is recommended toofirst convert hello VHD tooa RAW disk image.</span></span>  <span data-ttu-id="7e398-164">如果已經建立 hello VM 映像做為原始磁碟映像 （例如 KVM 有些 Hypervisor 的 hello 預設值），您可能會略過此步驟：</span><span class="sxs-lookup"><span data-stu-id="7e398-164">If hello VM image was already created as RAW disk image (hello default for some Hypervisors such as KVM) then you may skip this step:</span></span>
   
       # qemu-img convert -f vpc -O raw MyLinuxVM.vhd MyLinuxVM.raw

2. <span data-ttu-id="7e398-165">計算 hello 所需的 hello 虛擬大小的 hello 磁碟映像 tooensure 大小是對齊的 too1MB。</span><span class="sxs-lookup"><span data-stu-id="7e398-165">Calculate hello required size of hello disk image tooensure that hello virtual size is aligned too1MB.</span></span>  <span data-ttu-id="7e398-166">這可以協助 hello 遵循 bash 殼層指令碼。</span><span class="sxs-lookup"><span data-stu-id="7e398-166">hello following bash shell script can assist with this.</span></span>  <span data-ttu-id="7e398-167">hello 指令碼會使用 「`qemu-img info`"toodetermine hello hello 磁碟映像的虛擬大小，然後計算 hello 大小 toohello 下一步 1MB:</span><span class="sxs-lookup"><span data-stu-id="7e398-167">hello script uses "`qemu-img info`" toodetermine hello virtual size of hello disk image and then calculates hello size toohello next 1MB:</span></span>
   
       rawdisk="MyLinuxVM.raw"
       vhddisk="MyLinuxVM.vhd"
   
       MB=$((1024*1024))
       size=$(qemu-img info -f raw --output json "$rawdisk" | \
              gawk 'match($0, /"virtual-size": ([0-9]+),/, val) {print val[1]}')
   
       rounded_size=$((($size/$MB + 1)*$MB))
       echo "Rounded Size = $rounded_size"

3. <span data-ttu-id="7e398-168">調整在 hello 上述指令碼中使用 rounded_size hello 原始磁碟的大小：</span><span class="sxs-lookup"><span data-stu-id="7e398-168">Resize hello raw disk using $rounded_size as set in hello above script:</span></span>
   
       # qemu-img resize MyLinuxVM.raw $rounded_size

4. <span data-ttu-id="7e398-169">現在，將轉換 hello 原始磁碟回復 tooa 固定大小的 VHD:</span><span class="sxs-lookup"><span data-stu-id="7e398-169">Now, convert hello RAW disk back tooa fixed-size VHD:</span></span>
   
       # qemu-img convert -f raw -o subformat=fixed -O vpc MyLinuxVM.raw MyLinuxVM.vhd

   <span data-ttu-id="7e398-170">或 qemu 版本**2.6 +**包含 hello`force_size`選項：</span><span class="sxs-lookup"><span data-stu-id="7e398-170">Or, with qemu version **2.6+** include hello `force_size` option:</span></span>

       # qemu-img convert -f raw -o subformat=fixed,force_size -O vpc MyLinuxVM.raw MyLinuxVM.vhd

## <a name="linux-kernel-requirements"></a><span data-ttu-id="7e398-171">Linux Kernel 需求</span><span class="sxs-lookup"><span data-stu-id="7e398-171">Linux Kernel Requirements</span></span>
<span data-ttu-id="7e398-172">hello HYPER-V 和 Azure 的 Linux Integration Services (LIS) 驅動程式提供直接 toohello 上游 Linux 核心。</span><span class="sxs-lookup"><span data-stu-id="7e398-172">hello Linux Integration Services (LIS) drivers for Hyper-V and Azure are contributed directly toohello upstream Linux kernel.</span></span> <span data-ttu-id="7e398-173">許多包括最新 Linux kernel 版本 (例如 3.x) 的散發套件已經有這些驅動程式，或提供這些驅動程式及其核心的 Backport 版本。</span><span class="sxs-lookup"><span data-stu-id="7e398-173">Many distributions that include a recent Linux kernel version (i.e. 3.x) will have these drivers available already, or otherwise provide backported versions of these drivers with their kernels.</span></span>  <span data-ttu-id="7e398-174">這些驅動程式會經常更新 hello 上游核心與新的修正程式和功能，因此建議盡可能 toorun[背書發佈](endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)，將包含這些修正程式和更新。</span><span class="sxs-lookup"><span data-stu-id="7e398-174">These drivers are constantly being updated in hello upstream kernel with new fixes and features, so when possible it is recommended toorun an [endorsed distribution](endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) that will include these fixes and updates.</span></span>

<span data-ttu-id="7e398-175">如果您執行 Red Hat Enterprise Linux 版本的 variant **6.0-6.3**，則您必須針對 HYPER-V tooinstall hello 最新 LIS 驅動程式。</span><span class="sxs-lookup"><span data-stu-id="7e398-175">If you are running a variant of Red Hat Enterprise Linux versions **6.0-6.3**, then you will need tooinstall hello latest LIS drivers for Hyper-V.</span></span> <span data-ttu-id="7e398-176">您可以找到 hello 驅動程式[此位置](http://go.microsoft.com/fwlink/p/?LinkID=254263&clcid=0x409)。</span><span class="sxs-lookup"><span data-stu-id="7e398-176">hello drivers can be found [at this location](http://go.microsoft.com/fwlink/p/?LinkID=254263&clcid=0x409).</span></span> <span data-ttu-id="7e398-177">為準，RHEL **6.4 +** （與衍生項目） hello LIS 驅動程式已隨附 hello 核心，所以沒有額外的安裝封裝會需要的 toorun 這些系統在 Azure 上的。</span><span class="sxs-lookup"><span data-stu-id="7e398-177">As of RHEL **6.4+** (and derivatives) hello LIS drivers are already included with hello kernel and so no additional installation packages are needed toorun those systems on Azure.</span></span>

<span data-ttu-id="7e398-178">如果需要自訂的核心，則建議 toouse 較新的核心版本 (也就是**3.8 +**)。</span><span class="sxs-lookup"><span data-stu-id="7e398-178">If a custom kernel is required, it is recommended toouse a more recent kernel version (i.e. **3.8+**).</span></span> <span data-ttu-id="7e398-179">對於這些散發或廠商維護自己的核心，某些投入時間會需要的 tooregularly backport hello LIS 驅動程式從 hello 上游核心 tooyour 自訂的核心。</span><span class="sxs-lookup"><span data-stu-id="7e398-179">For those distributions or vendors who maintain their own kernel, some effort will be required tooregularly backport hello LIS drivers from hello upstream kernel tooyour custom kernel.</span></span>  <span data-ttu-id="7e398-180">即使您已經執行較新的核心版本，強烈建議 tookeep 追蹤任何上游的修正 hello LIS 驅動程式和 backport 那些視。</span><span class="sxs-lookup"><span data-stu-id="7e398-180">Even if you are already running a relatively recent kernel version, it is highly recommended tookeep track of any upstream fixes in hello LIS drivers and backport those as needed.</span></span> <span data-ttu-id="7e398-181">hello hello LIS 驅動程式來源檔案的位置位於 hello[維護程式](https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/tree/MAINTAINERS)hello Linux 核心來源樹狀目錄中的檔案：</span><span class="sxs-lookup"><span data-stu-id="7e398-181">hello location of hello LIS driver source files is available in hello [MAINTAINERS](https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/tree/MAINTAINERS) file in hello Linux kernel source tree:</span></span>

    F:    arch/x86/include/asm/mshyperv.h
    F:    arch/x86/include/uapi/asm/hyperv.h
    F:    arch/x86/kernel/cpu/mshyperv.c
    F:    drivers/hid/hid-hyperv.c
    F:    drivers/hv/
    F:    drivers/input/serio/hyperv-keyboard.c
    F:    drivers/net/hyperv/
    F:    drivers/scsi/storvsc_drv.c
    F:    drivers/video/fbdev/hyperv_fb.c
    F:    include/linux/hyperv.h
    F:    tools/hv/

<span data-ttu-id="7e398-182">在非常小，hello 缺乏 hello 遵循修補程式已知 toocause 在 Azure 上的問題，因此這些必須包含在 hello 核心。</span><span class="sxs-lookup"><span data-stu-id="7e398-182">At a very minimum, hello absence of hello following patches have been known toocause problems on Azure and so these must be included in hello kernel.</span></span> <span data-ttu-id="7e398-183">這絕對不是詳盡或完整的所有散發套件清單：</span><span class="sxs-lookup"><span data-stu-id="7e398-183">This list is by no means exhaustive or complete for all distributions:</span></span>

* [<span data-ttu-id="7e398-184">ata_piix： 預設延遲磁碟 toohello HYPER-V 驅動程式</span><span class="sxs-lookup"><span data-stu-id="7e398-184">ata_piix: defer disks toohello Hyper-V drivers by default</span></span>](https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/commit/drivers/ata/ata_piix.c?id=cd006086fa5d91414d8ff9ff2b78fbb593878e3c)
* [<span data-ttu-id="7e398-185">storvsc： 中傳輸封包 hello 重設路徑中的帳戶</span><span class="sxs-lookup"><span data-stu-id="7e398-185">storvsc: Account for in-transit packets in hello RESET path</span></span>](https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/commit/drivers/scsi/storvsc_drv.c?id=5c1b10ab7f93d24f29b5630286e323d1c5802d5c)
* [<span data-ttu-id="7e398-186">storvsc：避免使用 WRITE_SAME</span><span class="sxs-lookup"><span data-stu-id="7e398-186">storvsc: avoid usage of WRITE_SAME</span></span>](https://git.kernel.org/cgit/linux/kernel/git/next/linux-next.git/commit/drivers/scsi/storvsc_drv.c?id=3e8f4f4065901c8dfc51407e1984495e1748c090)
* [<span data-ttu-id="7e398-187">storvsc：針對 RAID 和虛擬主機介面卡驅動程式停用 WRITE SAME</span><span class="sxs-lookup"><span data-stu-id="7e398-187">storvsc: Disable WRITE SAME for RAID and virtual host adapter drivers</span></span>](https://git.kernel.org/cgit/linux/kernel/git/next/linux-next.git/commit/drivers/scsi/storvsc_drv.c?id=54b2b50c20a61b51199bedb6e5d2f8ec2568fb43)
* [<span data-ttu-id="7e398-188">storvsc：NULL 指標取值修正</span><span class="sxs-lookup"><span data-stu-id="7e398-188">storvsc: NULL pointer dereference fix</span></span>](https://git.kernel.org/cgit/linux/kernel/git/next/linux-next.git/commit/drivers/scsi/storvsc_drv.c?id=b12bb60d6c350b348a4e1460cd68f97ccae9822e)
* [<span data-ttu-id="7e398-189">storvsc：信號緩衝區失敗可能導致 I/O 凍結</span><span class="sxs-lookup"><span data-stu-id="7e398-189">storvsc: ring buffer failures may result in I/O freeze</span></span>](https://git.kernel.org/cgit/linux/kernel/git/next/linux-next.git/commit/drivers/scsi/storvsc_drv.c?id=e86fb5e8ab95f10ec5f2e9430119d5d35020c951)
* [<span data-ttu-id="7e398-190">scsi_sysfs︰防範 __scsi_remove_device 雙重執行</span><span class="sxs-lookup"><span data-stu-id="7e398-190">scsi_sysfs: protect against double execution of __scsi_remove_device</span></span>](https://git.kernel.org/cgit/linux/kernel/git/next/linux-next.git/commit/drivers/scsi/scsi_sysfs.c?id=be821fd8e62765de43cc4f0e2db363d0e30a7e9b)

## <a name="hello-azure-linux-agent"></a><span data-ttu-id="7e398-191">hello Azure Linux 代理程式</span><span class="sxs-lookup"><span data-stu-id="7e398-191">hello Azure Linux Agent</span></span>
<span data-ttu-id="7e398-192">hello [Azure Linux 代理程式](../windows/agent-user-guide.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)(waagent) 無須 tooproperly 佈建在 Azure 中 Linux 虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="7e398-192">hello [Azure Linux Agent](../windows/agent-user-guide.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) (waagent) is required tooproperly provision a Linux virtual machine in Azure.</span></span> <span data-ttu-id="7e398-193">您可以取得 hello 最新版本、 檔案問題或提交提取要求在 hello [Linux 代理程式 GitHub 儲存機制](https://github.com/Azure/WALinuxAgent)。</span><span class="sxs-lookup"><span data-stu-id="7e398-193">You can get hello latest version, file issues or submit pull requests at hello [Linux Agent GitHub repo](https://github.com/Azure/WALinuxAgent).</span></span>

* <span data-ttu-id="7e398-194">hello Linux 代理程式會釋放 hello Apache 2.0 授權。</span><span class="sxs-lookup"><span data-stu-id="7e398-194">hello Linux agent is released under hello Apache 2.0 license.</span></span> <span data-ttu-id="7e398-195">許多發行已提供 RPM 或 deb 套件 hello 代理程式，因此在某些情況下這也可以和安裝更新工程。</span><span class="sxs-lookup"><span data-stu-id="7e398-195">Many distributions already provide RPM or deb packages for hello agent, and so in some cases this can be installed and updated with little effort.</span></span>
* <span data-ttu-id="7e398-196">hello Azure Linux 代理程式需要 Python v2.6 +。</span><span class="sxs-lookup"><span data-stu-id="7e398-196">hello Azure Linux Agent requires Python v2.6+.</span></span>
* <span data-ttu-id="7e398-197">hello 代理程式也需要 hello python pyasn1 模組。</span><span class="sxs-lookup"><span data-stu-id="7e398-197">hello agent also requires hello python-pyasn1 module.</span></span> <span data-ttu-id="7e398-198">大多數的散發套件會以可個別安裝的套件形式提供此項目。</span><span class="sxs-lookup"><span data-stu-id="7e398-198">Most distributions provide this as a separate package that can be installed.</span></span>
* <span data-ttu-id="7e398-199">在某些情況下可能無法相容於 NetworkManager hello Azure Linux 代理程式。</span><span class="sxs-lookup"><span data-stu-id="7e398-199">In some cases hello Azure Linux Agent may not be compatible with NetworkManager.</span></span> <span data-ttu-id="7e398-200">Hello RPM/Deb 套件由分佈所提供的許多設定 NetworkManager 衝突 toohello waagent 套件，並因此將解除安裝 NetworkManager 當您安裝 hello Linux 代理程式封裝。</span><span class="sxs-lookup"><span data-stu-id="7e398-200">Many of hello RPM/Deb packages provided by distributions configure NetworkManager as a conflict toohello waagent package, and thus will uninstall NetworkManager when you install hello Linux agent package.</span></span>

## <a name="general-linux-system-requirements"></a><span data-ttu-id="7e398-201">一般的 Linux 系統需求</span><span class="sxs-lookup"><span data-stu-id="7e398-201">General Linux System Requirements</span></span>

* <span data-ttu-id="7e398-202">修改下列參數的幼蟲或 GRUB2 tooinclude hello hello 核心開機一行。</span><span class="sxs-lookup"><span data-stu-id="7e398-202">Modify hello kernel boot line in GRUB or GRUB2 tooinclude hello following parameters.</span></span> <span data-ttu-id="7e398-203">這也可確保所有的主控台訊息都會傳送 toohello 第一個序列連接埠，這可協助 Azure 偵錯問題的支援：</span><span class="sxs-lookup"><span data-stu-id="7e398-203">This will also ensure all console messages are sent toohello first serial port, which can assist Azure support with debugging issues:</span></span>
  
        console=ttyS0,115200n8 earlyprintk=ttyS0,115200 rootdelay=300
  
    <span data-ttu-id="7e398-204">這也可確保所有的主控台訊息都會傳送 toohello 第一個序列連接埠，這可協助 Azure 偵錯問題的支援。</span><span class="sxs-lookup"><span data-stu-id="7e398-204">This will also ensure all console messages are sent toohello first serial port, which can assist Azure support with debugging issues.</span></span>
  
    <span data-ttu-id="7e398-205">除了上述 toohello 建議太*移除*hello 參數之後，如果它們存在：</span><span class="sxs-lookup"><span data-stu-id="7e398-205">In addition toohello above, it is recommended too*remove* hello following parameters if they exist:</span></span>
  
        rhgb quiet crashkernel=auto
  
    <span data-ttu-id="7e398-206">沒有適用於雲端環境，我們想要傳送 toohello 序列連接埠的所有 hello 記錄 toobe 圖形和無訊息的開機。</span><span class="sxs-lookup"><span data-stu-id="7e398-206">Graphical and quiet boot are not useful in a cloud environment where we want all hello logs toobe sent toohello serial port.</span></span> <span data-ttu-id="7e398-207">hello`crashkernel`選項可能會是左設定如有需要，但請注意，這個參數會減少 hello hello 128 MB 以上，VM 中可用的記憶體數量可能會造成問題 hello 較小的 VM 大小。</span><span class="sxs-lookup"><span data-stu-id="7e398-207">hello `crashkernel` option may be left configured if desired, but note that this parameter will reduce hello amount of available memory in hello VM by 128MB or more, which may be problematic on hello smaller VM sizes.</span></span>

* <span data-ttu-id="7e398-208">安裝 hello Azure Linux 代理程式</span><span class="sxs-lookup"><span data-stu-id="7e398-208">Installing hello Azure Linux Agent</span></span>
  
    <span data-ttu-id="7e398-209">hello Azure Linux 代理程式，才能佈建在 Azure 上的 Linux 映像。</span><span class="sxs-lookup"><span data-stu-id="7e398-209">hello Azure Linux Agent is required for provisioning a Linux image on Azure.</span></span>  <span data-ttu-id="7e398-210">許多發行中提供作為 RPM 或 Deb 套件 hello 代理程式 （hello 封裝通常稱為 'WALinuxAgent' 或 'walinuxagent'）。</span><span class="sxs-lookup"><span data-stu-id="7e398-210">Many distributions provide hello agent as an RPM or Deb package (hello package is typically called 'WALinuxAgent' or 'walinuxagent').</span></span>  <span data-ttu-id="7e398-211">hello 代理程式也可以安裝以手動方式 hello 中的 hello 步驟[Linux 代理程式的指南](../windows/agent-user-guide.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="7e398-211">hello agent can also be installed manually by following hello steps in hello [Linux Agent Guide](../windows/agent-user-guide.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

* <span data-ttu-id="7e398-212">請確定該 hello SSH 伺服器是在安裝並設定 toostart 開機時間。</span><span class="sxs-lookup"><span data-stu-id="7e398-212">Ensure that hello SSH server is installed and configured toostart at boot time.</span></span>  <span data-ttu-id="7e398-213">這通常是 hello 預設值。</span><span class="sxs-lookup"><span data-stu-id="7e398-213">This is usually hello default.</span></span>

* <span data-ttu-id="7e398-214">不要在 hello OS 磁碟上建立的交換空間</span><span class="sxs-lookup"><span data-stu-id="7e398-214">Do not create swap space on hello OS disk</span></span>
  
    <span data-ttu-id="7e398-215">hello Azure Linux 代理程式可以自動設定使用之後附加的 toohello VM 在 Azure 上佈建的 hello 本機資源磁碟的交換空間。</span><span class="sxs-lookup"><span data-stu-id="7e398-215">hello Azure Linux Agent can automatically configure swap space using hello local resource disk that is attached toohello VM after provisioning on Azure.</span></span> <span data-ttu-id="7e398-216">請注意該 hello 本機資源磁碟是*暫存*磁碟，以及可能會在取消佈建 hello VM 時清空。</span><span class="sxs-lookup"><span data-stu-id="7e398-216">Note that hello local resource disk is a *temporary* disk, and might be emptied when hello VM is deprovisioned.</span></span> <span data-ttu-id="7e398-217">在安裝之後 hello Azure Linux 代理程式 （請參閱上一個步驟），修改適當地遵循 /etc/waagent.conf 中的參數的 hello:</span><span class="sxs-lookup"><span data-stu-id="7e398-217">After installing hello Azure Linux Agent (see previous step), modify hello following parameters in /etc/waagent.conf appropriately:</span></span>
  
        ResourceDisk.Format=y
        ResourceDisk.Filesystem=ext4
        ResourceDisk.MountPoint=/mnt/resource
        ResourceDisk.EnableSwap=y
        ResourceDisk.SwapSizeMB=2048    ## NOTE: set this toowhatever you need it toobe.

* <span data-ttu-id="7e398-218">最後一個步驟中，執行下列命令 toodeprovision hello 虛擬機器的 hello:</span><span class="sxs-lookup"><span data-stu-id="7e398-218">As a final step, run hello following commands toodeprovision hello virtual machine:</span></span>
  
        # sudo waagent -force -deprovision
        # export HISTSIZE=0
        # logout
  
  > [!NOTE]
  > <span data-ttu-id="7e398-219">Virtualbox 上，您可能會看到下列錯誤，開始執行之後的 hello ' waagent-force-取消佈建 ': `[Errno 5] Input/output error`。</span><span class="sxs-lookup"><span data-stu-id="7e398-219">On Virtualbox you may see hello following error after running 'waagent -force -deprovision': `[Errno 5] Input/output error`.</span></span> <span data-ttu-id="7e398-220">此錯誤訊息並不重要，您可以忽略。</span><span class="sxs-lookup"><span data-stu-id="7e398-220">This error message is not critical and can be ignored.</span></span>
  > 
  > 

* <span data-ttu-id="7e398-221">您接著需要 tooshut 關閉 hello 虛擬機器，並上傳 hello VHD tooAzure。</span><span class="sxs-lookup"><span data-stu-id="7e398-221">You will then need tooshut down hello virtual machine and upload hello VHD tooAzure.</span></span>

