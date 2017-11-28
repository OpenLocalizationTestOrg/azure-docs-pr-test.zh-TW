---
title: "aaaCreate 並上傳 Ubuntu Linux VHD 在 Azure 中"
description: "了解 toocreate 和上傳 Azure 虛擬硬碟 (VHD)，其中包含 Ubuntu Linux 作業系統。"
services: virtual-machines-linux
documentationcenter: 
author: szarkos
manager: timlt
editor: tysonn
tags: azure-resource-manager,azure-service-management
ms.assetid: 3e097959-84fc-4f6a-8cc8-35e087fd1542
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 02/02/2017
ms.author: szark
ms.openlocfilehash: cc546a487f769b32432a7e80ddcd0f6af44e201f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="prepare-an-ubuntu-virtual-machine-for-azure"></a><span data-ttu-id="51d0e-103">準備適用於 Azure 的 Ubuntu 虛擬機器</span><span class="sxs-lookup"><span data-stu-id="51d0e-103">Prepare an Ubuntu virtual machine for Azure</span></span>
[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-both-include.md)]

## <a name="official-ubuntu-cloud-images"></a><span data-ttu-id="51d0e-104">官方 Ubuntu 雲端映像</span><span class="sxs-lookup"><span data-stu-id="51d0e-104">Official Ubuntu cloud images</span></span>
<span data-ttu-id="51d0e-105">Ubuntu 現在發佈官方 Azure VHD 提供下載 ( [http://cloud-images.ubuntu.com/](http://cloud-images.ubuntu.com/))。</span><span class="sxs-lookup"><span data-stu-id="51d0e-105">Ubuntu now publishes official Azure VHDs for download at [http://cloud-images.ubuntu.com/](http://cloud-images.ubuntu.com/).</span></span> <span data-ttu-id="51d0e-106">如果您需要 toobuild 自己特製化的 Ubuntu 映像 azure，而非使用 hello 其下的手動程序正在使用這些已知的建議的 toostart 工作 Vhd，並視需要自訂。</span><span class="sxs-lookup"><span data-stu-id="51d0e-106">If you need toobuild your own specialized Ubuntu image for Azure, rather than use hello manual procedure below it is recommended toostart with these known working VHDs and customize as needed.</span></span> <span data-ttu-id="51d0e-107">hello 最新的映像版本永遠位於下列位置的 hello:</span><span class="sxs-lookup"><span data-stu-id="51d0e-107">hello latest image releases can always be found at hello following locations:</span></span>

* <span data-ttu-id="51d0e-108">Ubuntu 12.04/Precise︰ [ubuntu-12.04-server-cloudimg-amd64-disk1.vhd.zip](https://cloud-images.ubuntu.com/precise/current/precise-server-cloudimg-amd64-disk1.vhd.zip)</span><span class="sxs-lookup"><span data-stu-id="51d0e-108">Ubuntu 12.04/Precise: [ubuntu-12.04-server-cloudimg-amd64-disk1.vhd.zip](https://cloud-images.ubuntu.com/precise/current/precise-server-cloudimg-amd64-disk1.vhd.zip)</span></span>
* <span data-ttu-id="51d0e-109">Ubuntu 14.04/Trusty︰ [ubuntu-14.04-server-cloudimg-amd64-disk1.vhd.zip](http://cloud-images.ubuntu.com/releases/trusty/release/ubuntu-14.04-server-cloudimg-amd64-disk1.vhd.zip)</span><span class="sxs-lookup"><span data-stu-id="51d0e-109">Ubuntu 14.04/Trusty: [ubuntu-14.04-server-cloudimg-amd64-disk1.vhd.zip](http://cloud-images.ubuntu.com/releases/trusty/release/ubuntu-14.04-server-cloudimg-amd64-disk1.vhd.zip)</span></span>
* <span data-ttu-id="51d0e-110">Ubuntu 16.04/Xenial︰ [ubuntu-16.04-server-cloudimg-amd64-disk1.vhd.zip](http://cloud-images.ubuntu.com/releases/xenial/release/ubuntu-16.04-server-cloudimg-amd64-disk1.vhd.zip)</span><span class="sxs-lookup"><span data-stu-id="51d0e-110">Ubuntu 16.04/Xenial: [ubuntu-16.04-server-cloudimg-amd64-disk1.vhd.zip](http://cloud-images.ubuntu.com/releases/xenial/release/ubuntu-16.04-server-cloudimg-amd64-disk1.vhd.zip)</span></span>

## <a name="prerequisites"></a><span data-ttu-id="51d0e-111">必要條件</span><span class="sxs-lookup"><span data-stu-id="51d0e-111">Prerequisites</span></span>
<span data-ttu-id="51d0e-112">本文假設您已安裝 Ubuntu Linux 作業系統 tooa 虛擬硬碟。</span><span class="sxs-lookup"><span data-stu-id="51d0e-112">This article assumes that you have already installed an Ubuntu Linux operating system tooa virtual hard disk.</span></span> <span data-ttu-id="51d0e-113">多個工具存在 toocreate.vhd 檔案，例如 HYPER-V 之類的虛擬化解決方案。</span><span class="sxs-lookup"><span data-stu-id="51d0e-113">Multiple tools exist toocreate .vhd files, for example a virtualization solution such as Hyper-V.</span></span> <span data-ttu-id="51d0e-114">如需指示，請參閱[安裝 hello HYPER-V 角色和設定虛擬機器](http://technet.microsoft.com/library/hh846766.aspx)。</span><span class="sxs-lookup"><span data-stu-id="51d0e-114">For instructions, see [Install hello Hyper-V Role and Configure a Virtual Machine](http://technet.microsoft.com/library/hh846766.aspx).</span></span>

<span data-ttu-id="51d0e-115">**Ubuntu 安裝注意事項**</span><span class="sxs-lookup"><span data-stu-id="51d0e-115">**Ubuntu installation notes**</span></span>

* <span data-ttu-id="51d0e-116">另請參閱[一般 Linux 安裝注意事項](create-upload-generic.md#general-linux-installation-notes)，了解為 Azure 準備 Linux 的更多祕訣。</span><span class="sxs-lookup"><span data-stu-id="51d0e-116">Please see also [General Linux Installation Notes](create-upload-generic.md#general-linux-installation-notes) for more tips on preparing Linux for Azure.</span></span>
* <span data-ttu-id="51d0e-117">hello VHDX 格式不支援在 Azure 中，只有**固定 VHD**。</span><span class="sxs-lookup"><span data-stu-id="51d0e-117">hello VHDX format is not supported in Azure, only **fixed VHD**.</span></span>  <span data-ttu-id="51d0e-118">您可以將使用 HYPER-V 管理員 hello 磁碟 tooVHD 格式轉換或 hello convert-vhd 指令程式。</span><span class="sxs-lookup"><span data-stu-id="51d0e-118">You can convert hello disk tooVHD format using Hyper-V Manager or hello convert-vhd cmdlet.</span></span>
* <span data-ttu-id="51d0e-119">當安裝 hello Linux 系統建議您使用標準的資料分割，而非 LVM （通常 hello 預設值為許多安裝）。</span><span class="sxs-lookup"><span data-stu-id="51d0e-119">When installing hello Linux system it is recommended that you use standard partitions rather than LVM (often hello default for many installations).</span></span> <span data-ttu-id="51d0e-120">特別是當作業系統磁碟曾經需要附加 toobe tooanother VM 進行疑難排解，這樣可避免與複製 Vm，LVM 名稱衝突。</span><span class="sxs-lookup"><span data-stu-id="51d0e-120">This will avoid LVM name conflicts with cloned VMs, particularly if an OS disk ever needs toobe attached tooanother VM for troubleshooting.</span></span> <span data-ttu-id="51d0e-121">如果願意，您可以在資料磁碟上使用 [LVM](configure-lvm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) 或 [RAID](configure-raid.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="51d0e-121">[LVM](configure-lvm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) or [RAID](configure-raid.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) may be used on data disks if preferred.</span></span>
* <span data-ttu-id="51d0e-122">請勿設定 hello OS 磁碟交換資料分割。</span><span class="sxs-lookup"><span data-stu-id="51d0e-122">Do not configure a swap partition on hello OS disk.</span></span> <span data-ttu-id="51d0e-123">hello Linux 代理程式可以設定的 toocreate 交換磁碟上的檔案 hello 暫存資源。</span><span class="sxs-lookup"><span data-stu-id="51d0e-123">hello Linux agent can be configured toocreate a swap file on hello temporary resource disk.</span></span>  <span data-ttu-id="51d0e-124">相關資訊位於下列 hello 步驟。</span><span class="sxs-lookup"><span data-stu-id="51d0e-124">More information about this can be found in hello steps below.</span></span>
* <span data-ttu-id="51d0e-125">所有 hello Vhd 必須是 1 MB 的倍數的大小。</span><span class="sxs-lookup"><span data-stu-id="51d0e-125">All of hello VHDs must have sizes that are multiples of 1 MB.</span></span>

## <a name="manual-steps"></a><span data-ttu-id="51d0e-126">手動步驟</span><span class="sxs-lookup"><span data-stu-id="51d0e-126">Manual steps</span></span>
> [!NOTE]
> <span data-ttu-id="51d0e-127">然後再嘗試 toocreate 自己自訂的 Ubuntu 映像，azure，請考慮使用 hello 預先建置和測試映像從[http://cloud-images.ubuntu.com/](http://cloud-images.ubuntu.com/)改為。</span><span class="sxs-lookup"><span data-stu-id="51d0e-127">Before attempting toocreate your own custom Ubuntu image for Azure, please consider using hello pre-built and tested images from [http://cloud-images.ubuntu.com/](http://cloud-images.ubuntu.com/) instead.</span></span>
> 
> 

1. <span data-ttu-id="51d0e-128">Hello 選取中間窗格內的 HYPER-V 管理員，hello 虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="51d0e-128">In hello center pane of Hyper-V Manager, select hello virtual machine.</span></span>

2. <span data-ttu-id="51d0e-129">按一下**連接**tooopen hello 視窗 hello 虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="51d0e-129">Click **Connect** tooopen hello window for hello virtual machine.</span></span>

3. <span data-ttu-id="51d0e-130">取代 hello hello 映像 toouse Ubuntu 的 Azure 儲存機制中的目前儲存機制。</span><span class="sxs-lookup"><span data-stu-id="51d0e-130">Replace hello current repositories in hello image toouse Ubuntu's Azure repos.</span></span> <span data-ttu-id="51d0e-131">hello 步驟會稍微不同，視 hello Ubuntu 版本而定。</span><span class="sxs-lookup"><span data-stu-id="51d0e-131">hello steps vary slightly depending on hello Ubuntu version.</span></span>
   
    <span data-ttu-id="51d0e-132">然後再編輯`/etc/apt/sources.list`，它會建議 toomake 備份：</span><span class="sxs-lookup"><span data-stu-id="51d0e-132">Before editing `/etc/apt/sources.list`, it is recommended toomake a backup:</span></span>
   
        # sudo cp /etc/apt/sources.list /etc/apt/sources.list.bak

    <span data-ttu-id="51d0e-133">Ubuntu 12.04：</span><span class="sxs-lookup"><span data-stu-id="51d0e-133">Ubuntu 12.04:</span></span>
   
        # sudo sed -i 's/[a-z][a-z].archive.ubuntu.com/azure.archive.ubuntu.com/g' /etc/apt/sources.list
        # sudo apt-get update

    <span data-ttu-id="51d0e-134">Ubuntu 14.04：</span><span class="sxs-lookup"><span data-stu-id="51d0e-134">Ubuntu 14.04:</span></span>
   
        # sudo sed -i 's/[a-z][a-z].archive.ubuntu.com/azure.archive.ubuntu.com/g' /etc/apt/sources.list
        # sudo apt-get update

    <span data-ttu-id="51d0e-135">Ubuntu 16.04：</span><span class="sxs-lookup"><span data-stu-id="51d0e-135">Ubuntu 16.04:</span></span>
   
        # sudo sed -i 's/[a-z][a-z].archive.ubuntu.com/azure.archive.ubuntu.com/g' /etc/apt/sources.list
        # sudo apt-get update

4. <span data-ttu-id="51d0e-136">hello Ubuntu Azure 映像現在下列 hello*硬體啟用*(HWE) 核心。</span><span class="sxs-lookup"><span data-stu-id="51d0e-136">hello Ubuntu Azure images are now following hello *hardware enablement* (HWE) kernel.</span></span> <span data-ttu-id="51d0e-137">藉由執行下列命令的 hello 更新 hello 作業系統 toohello 最新的核心：</span><span class="sxs-lookup"><span data-stu-id="51d0e-137">Update hello operating system toohello latest kernel by running hello following commands:</span></span>

    <span data-ttu-id="51d0e-138">Ubuntu 12.04：</span><span class="sxs-lookup"><span data-stu-id="51d0e-138">Ubuntu 12.04:</span></span>
   
        # sudo apt-get update
        # sudo apt-get install linux-image-generic-lts-trusty linux-cloud-tools-generic-lts-trusty
        # sudo apt-get install hv-kvp-daemon-init
        (recommended) sudo apt-get dist-upgrade
   
        # sudo reboot
   
    <span data-ttu-id="51d0e-139">Ubuntu 14.04：</span><span class="sxs-lookup"><span data-stu-id="51d0e-139">Ubuntu 14.04:</span></span>
   
        # sudo apt-get update
        # sudo apt-get install linux-image-virtual-lts-vivid linux-lts-vivid-tools-common
        # sudo apt-get install hv-kvp-daemon-init
        (recommended) sudo apt-get dist-upgrade
   
        # sudo reboot

    <span data-ttu-id="51d0e-140">Ubuntu 16.04：</span><span class="sxs-lookup"><span data-stu-id="51d0e-140">Ubuntu 16.04:</span></span>
   
        # sudo apt-get update
        # sudo apt-get install linux-generic-hwe-16.04 linux-cloud-tools-generic-hwe-16.04
        (recommended) sudo apt-get dist-upgrade

        # sudo reboot

    <span data-ttu-id="51d0e-141">**另請參閱：**</span><span class="sxs-lookup"><span data-stu-id="51d0e-141">**See also:**</span></span>
    - [<span data-ttu-id="51d0e-142">https://wiki.ubuntu.com/Kernel/LTSEnablementStack</span><span class="sxs-lookup"><span data-stu-id="51d0e-142">https://wiki.ubuntu.com/Kernel/LTSEnablementStack</span></span>](https://wiki.ubuntu.com/Kernel/LTSEnablementStack)
    - [<span data-ttu-id="51d0e-143">https://wiki.ubuntu.com/Kernel/RollingLTSEnablementStack</span><span class="sxs-lookup"><span data-stu-id="51d0e-143">https://wiki.ubuntu.com/Kernel/RollingLTSEnablementStack</span></span>](https://wiki.ubuntu.com/Kernel/RollingLTSEnablementStack)


5. <span data-ttu-id="51d0e-144">修改 Azure hello 核心開機行幼蟲 tooinclude 其他核心參數。</span><span class="sxs-lookup"><span data-stu-id="51d0e-144">Modify hello kernel boot line for Grub tooinclude additional kernel parameters for Azure.</span></span> <span data-ttu-id="51d0e-145">此開啟 toodo`/etc/default/grub`在文字編輯器中，尋找名 hello 變數`GRUB_CMDLINE_LINUX_DEFAULT`（或視需要新增它） 並編輯 tooinclude hello 下列參數：</span><span class="sxs-lookup"><span data-stu-id="51d0e-145">toodo this open `/etc/default/grub` in a text editor, find hello variable called `GRUB_CMDLINE_LINUX_DEFAULT` (or add it if needed) and edit it tooinclude hello following parameters:</span></span>
   
        GRUB_CMDLINE_LINUX_DEFAULT="console=tty1 console=ttyS0,115200n8 earlyprintk=ttyS0,115200 rootdelay=300"

    <span data-ttu-id="51d0e-146">儲存並關閉此檔案，然後執行 `sudo update-grub`。</span><span class="sxs-lookup"><span data-stu-id="51d0e-146">Save and close this file, and then run `sudo update-grub`.</span></span> <span data-ttu-id="51d0e-147">這可確保所有的主控台訊息都會傳送 toohello 第一個序列連接埠，這可協助 Azure 偵錯問題的技術支援。</span><span class="sxs-lookup"><span data-stu-id="51d0e-147">This will ensure all console messages are sent toohello first serial port, which can assist Azure technical support with debugging issues.</span></span>

6. <span data-ttu-id="51d0e-148">請確定該 hello SSH 伺服器是在安裝並設定 toostart 開機時間。</span><span class="sxs-lookup"><span data-stu-id="51d0e-148">Ensure that hello SSH server is installed and configured toostart at boot time.</span></span>  <span data-ttu-id="51d0e-149">這通常是 hello 預設值。</span><span class="sxs-lookup"><span data-stu-id="51d0e-149">This is usually hello default.</span></span>

7. <span data-ttu-id="51d0e-150">安裝 hello Azure Linux 代理程式：</span><span class="sxs-lookup"><span data-stu-id="51d0e-150">Install hello Azure Linux Agent:</span></span>
   
        # sudo apt-get update
        # sudo apt-get install walinuxagent

    >[!Note]
    <span data-ttu-id="51d0e-151">hello`walinuxagent`封裝可能會移除 hello`NetworkManager`和`NetworkManager-gnome`如果安裝封裝。</span><span class="sxs-lookup"><span data-stu-id="51d0e-151">hello `walinuxagent` package may remove hello `NetworkManager` and `NetworkManager-gnome` packages, if they are installed.</span></span>

8. <span data-ttu-id="51d0e-152">執行下列命令 toodeprovision hello 虛擬機器的 hello 並準備在 Azure 上佈建：</span><span class="sxs-lookup"><span data-stu-id="51d0e-152">Run hello following commands toodeprovision hello virtual machine and prepare it for provisioning on Azure:</span></span>
   
        # sudo waagent -force -deprovision
        # export HISTSIZE=0
        # logout

9. <span data-ttu-id="51d0e-153">在 Hyper-V 管理員中，依序按一下 [動作] -> [關閉]。</span><span class="sxs-lookup"><span data-stu-id="51d0e-153">Click **Action -> Shut Down** in Hyper-V Manager.</span></span> <span data-ttu-id="51d0e-154">Linux VHD 是現在準備好 toobe 上傳 tooAzure。</span><span class="sxs-lookup"><span data-stu-id="51d0e-154">Your Linux VHD is now ready toobe uploaded tooAzure.</span></span>

## <a name="next-steps"></a><span data-ttu-id="51d0e-155">後續步驟</span><span class="sxs-lookup"><span data-stu-id="51d0e-155">Next steps</span></span>
<span data-ttu-id="51d0e-156">您要現在準備好 toouse Ubuntu Linux 虛擬硬碟 toocreate 新虛擬機器在 Azure 中。</span><span class="sxs-lookup"><span data-stu-id="51d0e-156">You're now ready toouse your Ubuntu Linux virtual hard disk toocreate new virtual machines in Azure.</span></span> <span data-ttu-id="51d0e-157">如果這是 hello 正在上傳 hello.vhd 檔案 tooAzure 的第一次，請參閱步驟 2 和 3 中的[建立和上傳包含 hello Linux 作業系統的虛擬硬碟](classic/create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="51d0e-157">If this is hello first time that you're uploading hello .vhd file tooAzure, see steps 2 and 3 in [Creating and uploading a virtual hard disk that contains hello Linux operating system](classic/create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).</span></span>

## <a name="references"></a><span data-ttu-id="51d0e-158">參考</span><span class="sxs-lookup"><span data-stu-id="51d0e-158">References</span></span>
<span data-ttu-id="51d0e-159">Ubuntu 硬體啟用 (HWE) 核心：</span><span class="sxs-lookup"><span data-stu-id="51d0e-159">Ubuntu hardware enablement (HWE) kernel:</span></span>

* [<span data-ttu-id="51d0e-160">http://blog.utlemming.org/2015/01/ubuntu-1404-azure-images-now-tracking.html</span><span class="sxs-lookup"><span data-stu-id="51d0e-160">http://blog.utlemming.org/2015/01/ubuntu-1404-azure-images-now-tracking.html</span></span>](http://blog.utlemming.org/2015/01/ubuntu-1404-azure-images-now-tracking.html)
* [<span data-ttu-id="51d0e-161">http://blog.utlemming.org/2015/02/1204-azure-cloud-images-now-using-hwe.html</span><span class="sxs-lookup"><span data-stu-id="51d0e-161">http://blog.utlemming.org/2015/02/1204-azure-cloud-images-now-using-hwe.html</span></span>](http://blog.utlemming.org/2015/02/1204-azure-cloud-images-now-using-hwe.html)

