---
title: "在 Azure 中建立及上傳 Linux VHD"
description: "了解如何建立及上傳包含 Linux 作業系統的 Azure 虛擬硬碟 (VHD)。"
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
ms.openlocfilehash: ccadf55c492c097ef96f25e469dbf36fc87b6102
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="information-for-non-endorsed-distributions"></a><span data-ttu-id="0f2e2-103">非背書散發套件的資訊</span><span class="sxs-lookup"><span data-stu-id="0f2e2-103">Information for Non-Endorsed Distributions</span></span>
[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-both-include.md)]

<span data-ttu-id="0f2e2-104">只有使用其中一個[背書散發套件](endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)時，Azure 平台 SLA 才適用於執行 Linux OS 的虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="0f2e2-104">The Azure platform SLA applies to virtual machines running the Linux OS only when one of the [endorsed distributions](endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) is used.</span></span> <span data-ttu-id="0f2e2-105">Azure 映像庫中提供的所有 Linux 散發套件，皆為使用必要組態的背書散發套件。</span><span class="sxs-lookup"><span data-stu-id="0f2e2-105">All Linux distributions that are provided in the Azure image gallery are endorsed distributions with the required configuration.</span></span>

* [<span data-ttu-id="0f2e2-106">Azure 背書散發套件上的 Linux</span><span class="sxs-lookup"><span data-stu-id="0f2e2-106">Linux on Azure - Endorsed Distributions</span></span>](endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [<span data-ttu-id="0f2e2-107">支援 Microsoft Azure 中的 Linux 映像</span><span class="sxs-lookup"><span data-stu-id="0f2e2-107">Support for Linux images in Microsoft Azure</span></span>](https://support.microsoft.com/kb/2941892)

<span data-ttu-id="0f2e2-108">所有執行於 Azure 的散發套件都必須符合許多必要條件，才能在平台上正確執行。</span><span class="sxs-lookup"><span data-stu-id="0f2e2-108">All distributions running on Azure will need to meet a number of prerequisites to have a chance to properly run on the platform.</span></span>  <span data-ttu-id="0f2e2-109">本文並未列出所有的必要條件，因為每個散發套件都不同；而且即使您符合下列所有條件，仍很可能需要詳加審視您的 Linux 系統，以確保它可在平台上正常運作。</span><span class="sxs-lookup"><span data-stu-id="0f2e2-109">This article is by no means comprehensive as every distribution is different; and it is quite possible that even if you meet all the criteria below you will still need to significantly tweak your Linux system to ensure that it properly runs on the platform.</span></span>

<span data-ttu-id="0f2e2-110">基於這個原因，我們建議您盡可能從其中一個 [Azure 背書散發套件上的 Linux](endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) 開始著手。</span><span class="sxs-lookup"><span data-stu-id="0f2e2-110">It is for this reason that we recommend that you start with one of our [Linux on Azure Endorsed Distributions](endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) when possible.</span></span> <span data-ttu-id="0f2e2-111">下列文章會逐步引導您如何準備 Azure 支援的各種 Linux 背書散發套件：</span><span class="sxs-lookup"><span data-stu-id="0f2e2-111">The following articles will guide you through how to prepare the various endorsed Linux distributions that are supported on Azure:</span></span>

* <span data-ttu-id="0f2e2-112">**[CentOS 型散發套件](create-upload-centos.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span><span class="sxs-lookup"><span data-stu-id="0f2e2-112">**[CentOS-based Distributions](create-upload-centos.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span></span>
* <span data-ttu-id="0f2e2-113">**[Debian Linux](debian-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span><span class="sxs-lookup"><span data-stu-id="0f2e2-113">**[Debian Linux](debian-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span></span>
* <span data-ttu-id="0f2e2-114">**[Oracle Linux](oracle-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span><span class="sxs-lookup"><span data-stu-id="0f2e2-114">**[Oracle Linux](oracle-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span></span>
* <span data-ttu-id="0f2e2-115">**[Red Hat Enterprise Linux](redhat-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span><span class="sxs-lookup"><span data-stu-id="0f2e2-115">**[Red Hat Enterprise Linux](redhat-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span></span>
* <span data-ttu-id="0f2e2-116">**[SLES 和 openSUSE](suse-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span><span class="sxs-lookup"><span data-stu-id="0f2e2-116">**[SLES & openSUSE](suse-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span></span>
* <span data-ttu-id="0f2e2-117">**[Ubuntu](create-upload-ubuntu.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span><span class="sxs-lookup"><span data-stu-id="0f2e2-117">**[Ubuntu](create-upload-ubuntu.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span></span>

<span data-ttu-id="0f2e2-118">本文接下來會將重點放在於 Azure 上執行 Linux 散發套件時的一般指引。</span><span class="sxs-lookup"><span data-stu-id="0f2e2-118">The rest of this article will focus on general guidance for running your Linux distribution on Azure.</span></span>

## <a name="general-linux-installation-notes"></a><span data-ttu-id="0f2e2-119">一般 Linux 安裝注意事項</span><span class="sxs-lookup"><span data-stu-id="0f2e2-119">General Linux Installation Notes</span></span>
* <span data-ttu-id="0f2e2-120">Azure 不支援 VHDX 格式，只支援 **固定 VHD**。</span><span class="sxs-lookup"><span data-stu-id="0f2e2-120">The VHDX format is not supported in Azure, only **fixed VHD**.</span></span>  <span data-ttu-id="0f2e2-121">您可以使用 Hyper-V 管理員或 convert-vhd Cmdlet，將磁碟轉換為 VHD 格式。</span><span class="sxs-lookup"><span data-stu-id="0f2e2-121">You can convert the disk to VHD format using Hyper-V Manager or the convert-vhd cmdlet.</span></span> <span data-ttu-id="0f2e2-122">如果您是使用 VirtualBox，即會在建立磁碟時選取 [固定大小]  而不是預設的動態配置。</span><span class="sxs-lookup"><span data-stu-id="0f2e2-122">If you are using VirtualBox this means selecting **Fixed size** as opposed to the default dynamically allocated when creating the disk.</span></span>
* <span data-ttu-id="0f2e2-123">Azure 僅支援第 1 代虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="0f2e2-123">Azure only supports generation 1 virtual machines.</span></span> <span data-ttu-id="0f2e2-124">您可以將第 1 代虛擬機器從 VHDX 轉換為 VHD 檔案格式，並從動態擴充轉換為固定大小的磁碟。</span><span class="sxs-lookup"><span data-stu-id="0f2e2-124">You can convert a generation 1 virtual machine from VHDX to the VHD file format and from dynamically expanding to a fixed sized disk.</span></span> <span data-ttu-id="0f2e2-125">但您無法變更虛擬機器的世代。</span><span class="sxs-lookup"><span data-stu-id="0f2e2-125">But you can't change a virtual machine's generation.</span></span> <span data-ttu-id="0f2e2-126">如需詳細資訊，請參閱[應該在 Hyper-V 中建立第 1 代還是第 2 代的虛擬機器？](https://technet.microsoft.com/en-us/windows-server-docs/compute/hyper-v/plan/should-i-create-a-generation-1-or-2-virtual-machine-in-hyper-v)</span><span class="sxs-lookup"><span data-stu-id="0f2e2-126">For more information, see [Should I create a generation 1 or 2 virtual machine in Hyper-V?](https://technet.microsoft.com/en-us/windows-server-docs/compute/hyper-v/plan/should-i-create-a-generation-1-or-2-virtual-machine-in-hyper-v)</span></span>
* <span data-ttu-id="0f2e2-127">允許的 VHD 大小上限為 1023 GB。</span><span class="sxs-lookup"><span data-stu-id="0f2e2-127">The maximum size allowed for the VHD is 1,023 GB.</span></span>
* <span data-ttu-id="0f2e2-128">安裝 Linux 系統時，*建議*您使用標準磁碟分割而不是 LVM (常是許多安裝的預設設定)。</span><span class="sxs-lookup"><span data-stu-id="0f2e2-128">When installing the Linux system it is *recommended* that you use standard partitions rather than LVM (often the default for many installations).</span></span> <span data-ttu-id="0f2e2-129">這可避免 LVM 與複製之 VM 的名稱衝突，特別是為了疑難排解而需要將作業系統磁碟連接至另一個相同的 VM 時。</span><span class="sxs-lookup"><span data-stu-id="0f2e2-129">This will avoid LVM name conflicts with cloned VMs, particularly if an OS disk ever needs to be attached to another identical VM for troubleshooting.</span></span> <span data-ttu-id="0f2e2-130">如果願意，您可以在資料磁碟上使用 [LVM](configure-raid.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) 或 [RAID](configure-lvm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="0f2e2-130">[LVM](configure-lvm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) or [RAID](configure-raid.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) may be used on data disks.</span></span>
* <span data-ttu-id="0f2e2-131">需要掛接 UDF 檔案系統的核心支援。</span><span class="sxs-lookup"><span data-stu-id="0f2e2-131">Kernel support for mounting UDF file systems is required.</span></span> <span data-ttu-id="0f2e2-132">在 Azure 上第一次開機時，佈建組態會透過連接客體的 UDF 格式媒體傳遞至 Linux VM。</span><span class="sxs-lookup"><span data-stu-id="0f2e2-132">At first boot on Azure the provisioning configuration is passed to the Linux VM via UDF-formatted media that is attached to the guest.</span></span> <span data-ttu-id="0f2e2-133">Azure Linux 代理程式必須能夠掛接 UDF 檔案系統讀取其組態並佈建 VM。</span><span class="sxs-lookup"><span data-stu-id="0f2e2-133">The Azure Linux agent must be able to mount the UDF file system to read its configuration and provision the VM.</span></span>
* <span data-ttu-id="0f2e2-134">Linux Kernel 2.6.37 以下的版本不支援較大 VM 大小 Hyper-V 上的NUMA。</span><span class="sxs-lookup"><span data-stu-id="0f2e2-134">Linux kernel versions below 2.6.37 do not support NUMA on Hyper-V with larger VM sizes.</span></span> <span data-ttu-id="0f2e2-135">這個問題主要會影響使用上游 Red Hat 2.6.32 kernel 的較舊散發套件，RHEL 6.6 (kernel-2.6.32-504) 已加以修正。</span><span class="sxs-lookup"><span data-stu-id="0f2e2-135">This issue primarily impacts older distributions using the upstream Red Hat 2.6.32 kernel, and was fixed in RHEL 6.6 (kernel-2.6.32-504).</span></span> <span data-ttu-id="0f2e2-136">執行的自訂核心是 2.6.37 以前版本的系統，或 2.6.32-504 以前以 RHEL 為基礎的核心必須在 grub.conf 的核心命令列上設定開機參數 `numa=off`。</span><span class="sxs-lookup"><span data-stu-id="0f2e2-136">Systems running custom kernels older than 2.6.37, or RHEL-based kernels older than 2.6.32-504 must set the boot parameter `numa=off` on the kernel command-line in grub.conf.</span></span> <span data-ttu-id="0f2e2-137">如需詳細資訊，請參閱 Red Hat [KB 436883](https://access.redhat.com/solutions/436883)。</span><span class="sxs-lookup"><span data-stu-id="0f2e2-137">For more information see Red Hat [KB 436883](https://access.redhat.com/solutions/436883).</span></span>
* <span data-ttu-id="0f2e2-138">請勿在作業系統磁碟上設定交換磁碟分割。</span><span class="sxs-lookup"><span data-stu-id="0f2e2-138">Do not configure a swap partition on the OS disk.</span></span> <span data-ttu-id="0f2e2-139">您可以設定 Linux 代理程式在暫存資源磁碟上建立交換檔。</span><span class="sxs-lookup"><span data-stu-id="0f2e2-139">The Linux agent can be configured to create a swap file on the temporary resource disk.</span></span>  <span data-ttu-id="0f2e2-140">您可以在以下步驟中找到與此有關的詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="0f2e2-140">More information about this can be found in the steps below.</span></span>
* <span data-ttu-id="0f2e2-141">所有 VHD 的大小都必須是 1 MB 的倍數。</span><span class="sxs-lookup"><span data-stu-id="0f2e2-141">All of the VHDs must have sizes that are multiples of 1 MB.</span></span>

### <a name="installing-kernel-modules-without-hyper-v"></a><span data-ttu-id="0f2e2-142">安裝不含 Hyper-V 的核心模組</span><span class="sxs-lookup"><span data-stu-id="0f2e2-142">Installing kernel modules without Hyper-V</span></span>
<span data-ttu-id="0f2e2-143">Azure 在 Hyper-V Hypervisor 上執行，因此 Linux 會要求必須安裝某些核心模組，才能在 Azure 中執行。</span><span class="sxs-lookup"><span data-stu-id="0f2e2-143">Azure runs on the Hyper-V hypervisor, so Linux requires that certain kernel modules are installed in order to run in Azure.</span></span> <span data-ttu-id="0f2e2-144">如果您的 VM 建立在 Hyper-V 外部，Linux 安裝程式在初始 Ramdisk (initrd 或 initramfs) 中可能不包含 Hyper-V 的驅動程式，除非它偵測到所執行的環境是 Hyper-V 環境。</span><span class="sxs-lookup"><span data-stu-id="0f2e2-144">If you have a VM that was created outside of Hyper-V, the Linux installers may not include the drivers for Hyper-V in the initial ramdisk (initrd or initramfs) unless it detects that it is running an a Hyper-V environment.</span></span> <span data-ttu-id="0f2e2-145">使用不同的虛擬化系統 (例如 Virtualbox、KVM 等) 來準備您的 Linux 映像時，您可能需要重新建置 initrd，以確保在初始 ramdisk 上至少有 `hv_vmbus` 和 `hv_storvsc` 核心模組可以使用。</span><span class="sxs-lookup"><span data-stu-id="0f2e2-145">When using a different virtualization system (i.e. Virtualbox, KVM, etc.) to prepare your Linux image, you may need to rebuild the initrd to ensure that at least the `hv_vmbus` and `hv_storvsc` kernel modules are available on the initial ramdisk.</span></span>  <span data-ttu-id="0f2e2-146">目前至少已知在以上游 Red Hat 散發套件為基礎的系統上有此問題。</span><span class="sxs-lookup"><span data-stu-id="0f2e2-146">This is a known issue at least on systems based on the upstream Red Hat distribution.</span></span>

<span data-ttu-id="0f2e2-147">重新建置 initrd 或 initramfs 映像的機制會根據散發套件而有所不同。</span><span class="sxs-lookup"><span data-stu-id="0f2e2-147">The mechanism for rebuilding the initrd or initramfs image may vary depending on the distribution.</span></span> <span data-ttu-id="0f2e2-148">請參閱散發套件的文件或支援人員，以了解適當程序。</span><span class="sxs-lookup"><span data-stu-id="0f2e2-148">Please consult your distribution's documentation or support for the proper procedure.</span></span>  <span data-ttu-id="0f2e2-149">以下是如何使用 `mkinitrd` 公用程式重新建置 initrd 的範例：</span><span class="sxs-lookup"><span data-stu-id="0f2e2-149">Here is one example for how to rebuild the initrd using the `mkinitrd` utility:</span></span>

<span data-ttu-id="0f2e2-150">首先，備份現有的 initrd 映像：</span><span class="sxs-lookup"><span data-stu-id="0f2e2-150">First, back up the existing initrd image:</span></span>

    # cd /boot
    # sudo cp initrd-`uname -r`.img  initrd-`uname -r`.img.bak

<span data-ttu-id="0f2e2-151">接下來，使用 `hv_vmbus` 和 `hv_storvsc` 核心模組重新建置 initrd：</span><span class="sxs-lookup"><span data-stu-id="0f2e2-151">Next, rebuild the initrd with the `hv_vmbus` and `hv_storvsc` kernel modules:</span></span>

    # sudo mkinitrd --preload=hv_storvsc --preload=hv_vmbus -v -f initrd-`uname -r`.img `uname -r`


### <a name="resizing-vhds"></a><span data-ttu-id="0f2e2-152">調整 VHD 的大小</span><span class="sxs-lookup"><span data-stu-id="0f2e2-152">Resizing VHDs</span></span>
<span data-ttu-id="0f2e2-153">Azure 上的 VHD 映像必須具有與 1 MB 對應的虛擬大小。</span><span class="sxs-lookup"><span data-stu-id="0f2e2-153">VHD images on Azure must have a virtual size aligned to 1MB.</span></span>  <span data-ttu-id="0f2e2-154">一般而言，使用 Hyper-V 建立的 VHD 應已正確對應。</span><span class="sxs-lookup"><span data-stu-id="0f2e2-154">Typically, VHDs created using Hyper-V should already be aligned correctly.</span></span>  <span data-ttu-id="0f2e2-155">如果 VHD 未正確對應，當您嘗試從 VHD 建立「映像」  時，可能會收到類似下面的錯誤訊息：</span><span class="sxs-lookup"><span data-stu-id="0f2e2-155">If the VHD is not aligned correctly then you may receive an error message similar to the following when you attempt to create an *image* from your VHD:</span></span>

    "The VHD http://<mystorageaccount>.blob.core.windows.net/vhds/MyLinuxVM.vhd has an unsupported virtual size of 21475270656 bytes. The size must be a whole number (in MBs).”

<span data-ttu-id="0f2e2-156">若要解決這個問題，您可以使用 Hyper-V 管理員主控台或 [Resize-VHD](http://technet.microsoft.com/library/hh848535.aspx) Powershell Cmdlet 調整 VM 的大小。</span><span class="sxs-lookup"><span data-stu-id="0f2e2-156">To remedy this you can resize the VM using either the Hyper-V Manager console or the [Resize-VHD](http://technet.microsoft.com/library/hh848535.aspx) Powershell cmdlet.</span></span>  <span data-ttu-id="0f2e2-157">如果您不在 Windows 環境中執行，建議使用 qemu-img 來轉換 VHD (如果需要) 及調整其大小。</span><span class="sxs-lookup"><span data-stu-id="0f2e2-157">If you are not running in a Windows environment then it is recommended to use qemu-img to convert (if needed) and resize the VHD.</span></span>

> [!NOTE]
> <span data-ttu-id="0f2e2-158">qemu-img >=2.2.1 的版本中已知有 Bug 會導致 VHD 的格式不正確。</span><span class="sxs-lookup"><span data-stu-id="0f2e2-158">There is a known bug in qemu-img versions >=2.2.1 that results in an improperly formatted VHD.</span></span> <span data-ttu-id="0f2e2-159">此問題已在 QEMU 2.6 中修正。</span><span class="sxs-lookup"><span data-stu-id="0f2e2-159">The issue has been fixed in QEMU 2.6.</span></span> <span data-ttu-id="0f2e2-160">建議使用 qemu-img 2.2.0 或更舊版本，或更新至 2.6 或更新版本。</span><span class="sxs-lookup"><span data-stu-id="0f2e2-160">It is recommended to use either qemu-img 2.2.0 or lower, or update to 2.6 or higher.</span></span> <span data-ttu-id="0f2e2-161">參考︰https://bugs.launchpad.net/qemu/+bug/1490611。</span><span class="sxs-lookup"><span data-stu-id="0f2e2-161">Reference: https://bugs.launchpad.net/qemu/+bug/1490611.</span></span>
> 
> 

1. <span data-ttu-id="0f2e2-162">直接使用工具 (例如 `qemu-img` 或 `vbox-manage`) 調整 VHD 的大小，可能會導致 VHD 無法開機。</span><span class="sxs-lookup"><span data-stu-id="0f2e2-162">Resizing the VHD directly using tools such as `qemu-img` or `vbox-manage` may result in an unbootable VHD.</span></span>  <span data-ttu-id="0f2e2-163">因此，建議先將 VHD 轉換為 RAW 磁碟映像。</span><span class="sxs-lookup"><span data-stu-id="0f2e2-163">So it is recommended to first convert the VHD to a RAW disk image.</span></span>  <span data-ttu-id="0f2e2-164">如果 VM 映像已建立為 RAW 磁碟映像 (有些 Hypervisor 的預設值，例如 KVM)，您可以省略此步驟：</span><span class="sxs-lookup"><span data-stu-id="0f2e2-164">If the VM image was already created as RAW disk image (the default for some Hypervisors such as KVM) then you may skip this step:</span></span>
   
       # qemu-img convert -f vpc -O raw MyLinuxVM.vhd MyLinuxVM.raw

2. <span data-ttu-id="0f2e2-165">計算所需的磁碟映像大小，以確保虛擬大小對應於 1 MB。</span><span class="sxs-lookup"><span data-stu-id="0f2e2-165">Calculate the required size of the disk image to ensure that the virtual size is aligned to 1MB.</span></span>  <span data-ttu-id="0f2e2-166">下列 bash 殼層指令碼有助於此作業。</span><span class="sxs-lookup"><span data-stu-id="0f2e2-166">The following bash shell script can assist with this.</span></span>  <span data-ttu-id="0f2e2-167">此指令碼會使用 "`qemu-img info`" 來判斷磁碟映像的虛擬大小，然後計算下一個 1 MB 的大小：</span><span class="sxs-lookup"><span data-stu-id="0f2e2-167">The script uses "`qemu-img info`" to determine the virtual size of the disk image and then calculates the size to the next 1MB:</span></span>
   
       rawdisk="MyLinuxVM.raw"
       vhddisk="MyLinuxVM.vhd"
   
       MB=$((1024*1024))
       size=$(qemu-img info -f raw --output json "$rawdisk" | \
              gawk 'match($0, /"virtual-size": ([0-9]+),/, val) {print val[1]}')
   
       rounded_size=$((($size/$MB + 1)*$MB))
       echo "Rounded Size = $rounded_size"

3. <span data-ttu-id="0f2e2-168">依照上述指令碼中的設定，使用 $rounded_size 調整原始磁碟的大小：</span><span class="sxs-lookup"><span data-stu-id="0f2e2-168">Resize the raw disk using $rounded_size as set in the above script:</span></span>
   
       # qemu-img resize MyLinuxVM.raw $rounded_size

4. <span data-ttu-id="0f2e2-169">現在，將 RAW 磁碟轉換回固定大小的 VHD：</span><span class="sxs-lookup"><span data-stu-id="0f2e2-169">Now, convert the RAW disk back to a fixed-size VHD:</span></span>
   
       # qemu-img convert -f raw -o subformat=fixed -O vpc MyLinuxVM.raw MyLinuxVM.vhd

   <span data-ttu-id="0f2e2-170">或者，qemu 版本 **2.6 +** 包含 `force_size` 選項︰</span><span class="sxs-lookup"><span data-stu-id="0f2e2-170">Or, with qemu version **2.6+** include the `force_size` option:</span></span>

       # qemu-img convert -f raw -o subformat=fixed,force_size -O vpc MyLinuxVM.raw MyLinuxVM.vhd

## <a name="linux-kernel-requirements"></a><span data-ttu-id="0f2e2-171">Linux Kernel 需求</span><span class="sxs-lookup"><span data-stu-id="0f2e2-171">Linux Kernel Requirements</span></span>
<span data-ttu-id="0f2e2-172">適用於 Hyper-V 和 Azure 的 Linux Integration Services (LIS) 驅動程式會直接提供給上游 Linux Kernel。</span><span class="sxs-lookup"><span data-stu-id="0f2e2-172">The Linux Integration Services (LIS) drivers for Hyper-V and Azure are contributed directly to the upstream Linux kernel.</span></span> <span data-ttu-id="0f2e2-173">許多包括最新 Linux kernel 版本 (例如 3.x) 的散發套件已經有這些驅動程式，或提供這些驅動程式及其核心的 Backport 版本。</span><span class="sxs-lookup"><span data-stu-id="0f2e2-173">Many distributions that include a recent Linux kernel version (i.e. 3.x) will have these drivers available already, or otherwise provide backported versions of these drivers with their kernels.</span></span>  <span data-ttu-id="0f2e2-174">上游核心會透過新的修正和功能來不斷更新這些驅動程式，因此若有可能的話，建議您執行將包含這些修正與更新的 [背書散發套件](endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) 。</span><span class="sxs-lookup"><span data-stu-id="0f2e2-174">These drivers are constantly being updated in the upstream kernel with new fixes and features, so when possible it is recommended to run an [endorsed distribution](endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) that will include these fixes and updates.</span></span>

<span data-ttu-id="0f2e2-175">如果您打算執行 Red Hat Enterprise Linux 版本 **6.0-6.3**的變體，則您必須安裝 Hyper-V 的最新 LIS 驅動程式。</span><span class="sxs-lookup"><span data-stu-id="0f2e2-175">If you are running a variant of Red Hat Enterprise Linux versions **6.0-6.3**, then you will need to install the latest LIS drivers for Hyper-V.</span></span> <span data-ttu-id="0f2e2-176">您可以在 [這裡](http://go.microsoft.com/fwlink/p/?LinkID=254263&clcid=0x409)找到驅動程式。</span><span class="sxs-lookup"><span data-stu-id="0f2e2-176">The drivers can be found [at this location](http://go.microsoft.com/fwlink/p/?LinkID=254263&clcid=0x409).</span></span> <span data-ttu-id="0f2e2-177">從 RHEL **6.4+** (及衍生物件) 開始，核心已隨附 LIS 驅動程式，因此無需額外的安裝套件，即可在 Azure 上執行這些系統。</span><span class="sxs-lookup"><span data-stu-id="0f2e2-177">As of RHEL **6.4+** (and derivatives) the LIS drivers are already included with the kernel and so no additional installation packages are needed to run those systems on Azure.</span></span>

<span data-ttu-id="0f2e2-178">如果需要自訂核心，建議您使用最新的核心版本 (例如 **3.8+**)。</span><span class="sxs-lookup"><span data-stu-id="0f2e2-178">If a custom kernel is required, it is recommended to use a more recent kernel version (i.e. **3.8+**).</span></span> <span data-ttu-id="0f2e2-179">針對這些散發套件或自行維護核心的廠商，需要花費一點心力，定期將 LIS 驅動程式從上游核心 Backport 到您的自訂核心。</span><span class="sxs-lookup"><span data-stu-id="0f2e2-179">For those distributions or vendors who maintain their own kernel, some effort will be required to regularly backport the LIS drivers from the upstream kernel to your custom kernel.</span></span>  <span data-ttu-id="0f2e2-180">即使您已經在執行相對較新的核心版本，還是強烈建議您持續追蹤任何 LIS 驅動程式的上游修正，並視需要 Backport 這些修正。</span><span class="sxs-lookup"><span data-stu-id="0f2e2-180">Even if you are already running a relatively recent kernel version, it is highly recommended to keep track of any upstream fixes in the LIS drivers and backport those as needed.</span></span> <span data-ttu-id="0f2e2-181">您可以在 Linux Kernel 來源樹狀目錄中的 [MAINTAINERS](https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/tree/MAINTAINERS) 檔案找到 LIS 驅動程式原始程式檔的位置。</span><span class="sxs-lookup"><span data-stu-id="0f2e2-181">The location of the LIS driver source files is available in the [MAINTAINERS](https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/tree/MAINTAINERS) file in the Linux kernel source tree:</span></span>

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

<span data-ttu-id="0f2e2-182">至少，我們已知缺少下列修補程式有可能會在 Azure 上造成問題，因此這些修補程式必須包含在核心內。</span><span class="sxs-lookup"><span data-stu-id="0f2e2-182">At a very minimum, the absence of the following patches have been known to cause problems on Azure and so these must be included in the kernel.</span></span> <span data-ttu-id="0f2e2-183">這絕對不是詳盡或完整的所有散發套件清單：</span><span class="sxs-lookup"><span data-stu-id="0f2e2-183">This list is by no means exhaustive or complete for all distributions:</span></span>

* [<span data-ttu-id="0f2e2-184">ata_piix：依預設將磁碟委託給 Hyper-V 驅動程式</span><span class="sxs-lookup"><span data-stu-id="0f2e2-184">ata_piix: defer disks to the Hyper-V drivers by default</span></span>](https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/commit/drivers/ata/ata_piix.c?id=cd006086fa5d91414d8ff9ff2b78fbb593878e3c)
* [<span data-ttu-id="0f2e2-185">storvsc：負責 RESET 路徑中的在途封包</span><span class="sxs-lookup"><span data-stu-id="0f2e2-185">storvsc: Account for in-transit packets in the RESET path</span></span>](https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/commit/drivers/scsi/storvsc_drv.c?id=5c1b10ab7f93d24f29b5630286e323d1c5802d5c)
* [<span data-ttu-id="0f2e2-186">storvsc：避免使用 WRITE_SAME</span><span class="sxs-lookup"><span data-stu-id="0f2e2-186">storvsc: avoid usage of WRITE_SAME</span></span>](https://git.kernel.org/cgit/linux/kernel/git/next/linux-next.git/commit/drivers/scsi/storvsc_drv.c?id=3e8f4f4065901c8dfc51407e1984495e1748c090)
* [<span data-ttu-id="0f2e2-187">storvsc：針對 RAID 和虛擬主機介面卡驅動程式停用 WRITE SAME</span><span class="sxs-lookup"><span data-stu-id="0f2e2-187">storvsc: Disable WRITE SAME for RAID and virtual host adapter drivers</span></span>](https://git.kernel.org/cgit/linux/kernel/git/next/linux-next.git/commit/drivers/scsi/storvsc_drv.c?id=54b2b50c20a61b51199bedb6e5d2f8ec2568fb43)
* [<span data-ttu-id="0f2e2-188">storvsc：NULL 指標取值修正</span><span class="sxs-lookup"><span data-stu-id="0f2e2-188">storvsc: NULL pointer dereference fix</span></span>](https://git.kernel.org/cgit/linux/kernel/git/next/linux-next.git/commit/drivers/scsi/storvsc_drv.c?id=b12bb60d6c350b348a4e1460cd68f97ccae9822e)
* [<span data-ttu-id="0f2e2-189">storvsc：信號緩衝區失敗可能導致 I/O 凍結</span><span class="sxs-lookup"><span data-stu-id="0f2e2-189">storvsc: ring buffer failures may result in I/O freeze</span></span>](https://git.kernel.org/cgit/linux/kernel/git/next/linux-next.git/commit/drivers/scsi/storvsc_drv.c?id=e86fb5e8ab95f10ec5f2e9430119d5d35020c951)
* [<span data-ttu-id="0f2e2-190">scsi_sysfs︰防範 __scsi_remove_device 雙重執行</span><span class="sxs-lookup"><span data-stu-id="0f2e2-190">scsi_sysfs: protect against double execution of __scsi_remove_device</span></span>](https://git.kernel.org/cgit/linux/kernel/git/next/linux-next.git/commit/drivers/scsi/scsi_sysfs.c?id=be821fd8e62765de43cc4f0e2db363d0e30a7e9b)

## <a name="the-azure-linux-agent"></a><span data-ttu-id="0f2e2-191">Azure Linux 代理程式</span><span class="sxs-lookup"><span data-stu-id="0f2e2-191">The Azure Linux Agent</span></span>
<span data-ttu-id="0f2e2-192">若要在 Azure 中正確佈建 Linux 虛擬機器， [Azure Linux 代理程式](../windows/agent-user-guide.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) (waagent) 是必要選項。</span><span class="sxs-lookup"><span data-stu-id="0f2e2-192">The [Azure Linux Agent](../windows/agent-user-guide.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) (waagent) is required to properly provision a Linux virtual machine in Azure.</span></span> <span data-ttu-id="0f2e2-193">您可以在 [Linux 代理程式 GitHub 儲存機制](https://github.com/Azure/WALinuxAgent)中取得最新的版本、檔案問題或提交提取要求。</span><span class="sxs-lookup"><span data-stu-id="0f2e2-193">You can get the latest version, file issues or submit pull requests at the [Linux Agent GitHub repo](https://github.com/Azure/WALinuxAgent).</span></span>

* <span data-ttu-id="0f2e2-194">Linux 代理程式已在 Apache 2.0 授權下發行。</span><span class="sxs-lookup"><span data-stu-id="0f2e2-194">The Linux agent is released under the Apache 2.0 license.</span></span> <span data-ttu-id="0f2e2-195">許多散發套件已提供代理程式的 RPM 或 Deb 套件，因此在某些情況下，您可以不費吹灰之力就能安裝及更新此代理程式。</span><span class="sxs-lookup"><span data-stu-id="0f2e2-195">Many distributions already provide RPM or deb packages for the agent, and so in some cases this can be installed and updated with little effort.</span></span>
* <span data-ttu-id="0f2e2-196">Azure Linux 代理程式需要 Python v2.6+。</span><span class="sxs-lookup"><span data-stu-id="0f2e2-196">The Azure Linux Agent requires Python v2.6+.</span></span>
* <span data-ttu-id="0f2e2-197">代理程式還需要 python-pyasn1 模組。</span><span class="sxs-lookup"><span data-stu-id="0f2e2-197">The agent also requires the python-pyasn1 module.</span></span> <span data-ttu-id="0f2e2-198">大多數的散發套件會以可個別安裝的套件形式提供此項目。</span><span class="sxs-lookup"><span data-stu-id="0f2e2-198">Most distributions provide this as a separate package that can be installed.</span></span>
* <span data-ttu-id="0f2e2-199">在某些情況下，Azure Linux 代理程式可能與 NetworkManager 不相容。</span><span class="sxs-lookup"><span data-stu-id="0f2e2-199">In some cases the Azure Linux Agent may not be compatible with NetworkManager.</span></span> <span data-ttu-id="0f2e2-200">散發套件提供的許多 RPM/Deb 套件會將 NetworkManager 設定為 waagent 套件的衝突，因此會在您安裝 Linux 代理程式套件時解除安裝 NetworkManager。</span><span class="sxs-lookup"><span data-stu-id="0f2e2-200">Many of the RPM/Deb packages provided by distributions configure NetworkManager as a conflict to the waagent package, and thus will uninstall NetworkManager when you install the Linux agent package.</span></span>

## <a name="general-linux-system-requirements"></a><span data-ttu-id="0f2e2-201">一般的 Linux 系統需求</span><span class="sxs-lookup"><span data-stu-id="0f2e2-201">General Linux System Requirements</span></span>

* <span data-ttu-id="0f2e2-202">在 GRUB 或 GRUB2 中修改核心開機行，以加入下列參數。</span><span class="sxs-lookup"><span data-stu-id="0f2e2-202">Modify the kernel boot line in GRUB or GRUB2 to include the following parameters.</span></span> <span data-ttu-id="0f2e2-203">這樣也可確保主控台訊息能傳送至第一個序列埠，以協助 Azure 支援偵錯問題：</span><span class="sxs-lookup"><span data-stu-id="0f2e2-203">This will also ensure all console messages are sent to the first serial port, which can assist Azure support with debugging issues:</span></span>
  
        console=ttyS0,115200n8 earlyprintk=ttyS0,115200 rootdelay=300
  
    <span data-ttu-id="0f2e2-204">這也將確保所有主控台訊息都會傳送給第一個序列埠，有助於 Azure 支援團隊進行問題偵錯程序。</span><span class="sxs-lookup"><span data-stu-id="0f2e2-204">This will also ensure all console messages are sent to the first serial port, which can assist Azure support with debugging issues.</span></span>
  
    <span data-ttu-id="0f2e2-205">除了上述以外，我們還建議您 *移除* 下列參數 (如果存在的話)：</span><span class="sxs-lookup"><span data-stu-id="0f2e2-205">In addition to the above, it is recommended to *remove* the following parameters if they exist:</span></span>
  
        rhgb quiet crashkernel=auto
  
    <span data-ttu-id="0f2e2-206">在雲端環境中，我們會將所有記錄傳送到序列埠，因此不適合使用圖形化和無訊息啟動。</span><span class="sxs-lookup"><span data-stu-id="0f2e2-206">Graphical and quiet boot are not useful in a cloud environment where we want all the logs to be sent to the serial port.</span></span> <span data-ttu-id="0f2e2-207">如有需要，您可以保留 `crashkernel` 選項的設定，但請注意，此參數將會減少 VM 中約 128MB 或以上的可用記憶體數量，這在較小的 VM 中可能會是個問題。</span><span class="sxs-lookup"><span data-stu-id="0f2e2-207">The `crashkernel` option may be left configured if desired, but note that this parameter will reduce the amount of available memory in the VM by 128MB or more, which may be problematic on the smaller VM sizes.</span></span>

* <span data-ttu-id="0f2e2-208">安裝 Azure Linux 代理程式</span><span class="sxs-lookup"><span data-stu-id="0f2e2-208">Installing the Azure Linux Agent</span></span>
  
    <span data-ttu-id="0f2e2-209">如需在 Azure 上佈建 Linux 映像，您需要 Azure Linux 代理程式。</span><span class="sxs-lookup"><span data-stu-id="0f2e2-209">The Azure Linux Agent is required for provisioning a Linux image on Azure.</span></span>  <span data-ttu-id="0f2e2-210">許多散發套件以 RPM 或 Deb 套件 (此套件通常稱為 'WALinuxAgent' 或 'walinuxagent') 的形式提供代理程式。</span><span class="sxs-lookup"><span data-stu-id="0f2e2-210">Many distributions provide the agent as an RPM or Deb package (the package is typically called 'WALinuxAgent' or 'walinuxagent').</span></span>  <span data-ttu-id="0f2e2-211">您也可以遵循 [Linux 代理程式指南](../windows/agent-user-guide.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)中的步驟來手動安裝代理程式。</span><span class="sxs-lookup"><span data-stu-id="0f2e2-211">The agent can also be installed manually by following the steps in the [Linux Agent Guide](../windows/agent-user-guide.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

* <span data-ttu-id="0f2e2-212">確定您已安裝 SSH 伺服器，並已設定為在開機時啟動。</span><span class="sxs-lookup"><span data-stu-id="0f2e2-212">Ensure that the SSH server is installed and configured to start at boot time.</span></span>  <span data-ttu-id="0f2e2-213">這通常是預設值。</span><span class="sxs-lookup"><span data-stu-id="0f2e2-213">This is usually the default.</span></span>

* <span data-ttu-id="0f2e2-214">請不要在 OS 磁碟上建立交換空間</span><span class="sxs-lookup"><span data-stu-id="0f2e2-214">Do not create swap space on the OS disk</span></span>
  
    <span data-ttu-id="0f2e2-215">Azure Linux 代理程式可在 VM 佈建於 Azure 後，使用附加至 VM 的本機資源磁碟自動設定交換空間。</span><span class="sxs-lookup"><span data-stu-id="0f2e2-215">The Azure Linux Agent can automatically configure swap space using the local resource disk that is attached to the VM after provisioning on Azure.</span></span> <span data-ttu-id="0f2e2-216">請注意，資源磁碟是 *暫存* 磁碟，可能會在 VM 取消佈建時清空。</span><span class="sxs-lookup"><span data-stu-id="0f2e2-216">Note that the local resource disk is a *temporary* disk, and might be emptied when the VM is deprovisioned.</span></span> <span data-ttu-id="0f2e2-217">安裝 Azure Linux 代理程式 (請參閱上一個步驟) 後，請在 /etc/waagent.conf 中適當修改下列參數：</span><span class="sxs-lookup"><span data-stu-id="0f2e2-217">After installing the Azure Linux Agent (see previous step), modify the following parameters in /etc/waagent.conf appropriately:</span></span>
  
        ResourceDisk.Format=y
        ResourceDisk.Filesystem=ext4
        ResourceDisk.MountPoint=/mnt/resource
        ResourceDisk.EnableSwap=y
        ResourceDisk.SwapSizeMB=2048    ## NOTE: set this to whatever you need it to be.

* <span data-ttu-id="0f2e2-218">最後一個步驟是，執行下列命令以取消佈建虛擬機器：</span><span class="sxs-lookup"><span data-stu-id="0f2e2-218">As a final step, run the following commands to deprovision the virtual machine:</span></span>
  
        # sudo waagent -force -deprovision
        # export HISTSIZE=0
        # logout
  
  > [!NOTE]
  > <span data-ttu-id="0f2e2-219">在 Virtualbox 上，執行 'waagent -force -deprovision' 之後，您可能會看到以下錯誤：`[Errno 5] Input/output error`。</span><span class="sxs-lookup"><span data-stu-id="0f2e2-219">On Virtualbox you may see the following error after running 'waagent -force -deprovision': `[Errno 5] Input/output error`.</span></span> <span data-ttu-id="0f2e2-220">此錯誤訊息並不重要，您可以忽略。</span><span class="sxs-lookup"><span data-stu-id="0f2e2-220">This error message is not critical and can be ignored.</span></span>
  > 
  > 

* <span data-ttu-id="0f2e2-221">接著，您必須關閉虛擬機器，並將 VHD 上傳至 Azure。</span><span class="sxs-lookup"><span data-stu-id="0f2e2-221">You will then need to shut down the virtual machine and upload the VHD to Azure.</span></span>

