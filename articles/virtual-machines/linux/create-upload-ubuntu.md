---
title: "在 Azure 中建立及上傳 Ubuntu Linux VHD"
description: "了解如何建立及上傳包含 Ubuntu Linux 作業系統的 Azure 虛擬硬碟 (VHD)。"
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
ms.openlocfilehash: 4496b34ff88ca1e08cc74788ae09d787d4399eaf
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/18/2017
---
# <a name="prepare-an-ubuntu-virtual-machine-for-azure"></a><span data-ttu-id="a779d-103">準備適用於 Azure 的 Ubuntu 虛擬機器</span><span class="sxs-lookup"><span data-stu-id="a779d-103">Prepare an Ubuntu virtual machine for Azure</span></span>
[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-both-include.md)]

## <a name="official-ubuntu-cloud-images"></a><span data-ttu-id="a779d-104">官方 Ubuntu 雲端映像</span><span class="sxs-lookup"><span data-stu-id="a779d-104">Official Ubuntu cloud images</span></span>
<span data-ttu-id="a779d-105">Ubuntu 現在發佈官方 Azure VHD 提供下載 ( [http://cloud-images.ubuntu.com/](http://cloud-images.ubuntu.com/))。</span><span class="sxs-lookup"><span data-stu-id="a779d-105">Ubuntu now publishes official Azure VHDs for download at [http://cloud-images.ubuntu.com/](http://cloud-images.ubuntu.com/).</span></span> <span data-ttu-id="a779d-106">如果您需要針對 Azure 建置您專用的 Ubuntu 映像，而不使用下面的手動程序，建議您視需要從使用這些已知可運作的 VHD 並加以自訂來開始建置。</span><span class="sxs-lookup"><span data-stu-id="a779d-106">If you need to build your own specialized Ubuntu image for Azure, rather than use the manual procedure below it is recommended to start with these known working VHDs and customize as needed.</span></span> <span data-ttu-id="a779d-107">最新的映像版本一律可以在下列位置找到︰</span><span class="sxs-lookup"><span data-stu-id="a779d-107">The latest image releases can always be found at the following locations:</span></span>

* <span data-ttu-id="a779d-108">Ubuntu 12.04/Precise︰ [ubuntu-12.04-server-cloudimg-amd64-disk1.vhd.zip](https://cloud-images.ubuntu.com/precise/current/precise-server-cloudimg-amd64-disk1.vhd.zip)</span><span class="sxs-lookup"><span data-stu-id="a779d-108">Ubuntu 12.04/Precise: [ubuntu-12.04-server-cloudimg-amd64-disk1.vhd.zip](https://cloud-images.ubuntu.com/precise/current/precise-server-cloudimg-amd64-disk1.vhd.zip)</span></span>
* <span data-ttu-id="a779d-109">Ubuntu 14.04/Trusty︰ [ubuntu-14.04-server-cloudimg-amd64-disk1.vhd.zip](http://cloud-images.ubuntu.com/releases/trusty/release/ubuntu-14.04-server-cloudimg-amd64-disk1.vhd.zip)</span><span class="sxs-lookup"><span data-stu-id="a779d-109">Ubuntu 14.04/Trusty: [ubuntu-14.04-server-cloudimg-amd64-disk1.vhd.zip](http://cloud-images.ubuntu.com/releases/trusty/release/ubuntu-14.04-server-cloudimg-amd64-disk1.vhd.zip)</span></span>
* <span data-ttu-id="a779d-110">Ubuntu 16.04/Xenial︰ [ubuntu-16.04-server-cloudimg-amd64-disk1.vhd.zip](http://cloud-images.ubuntu.com/releases/xenial/release/ubuntu-16.04-server-cloudimg-amd64-disk1.vhd.zip)</span><span class="sxs-lookup"><span data-stu-id="a779d-110">Ubuntu 16.04/Xenial: [ubuntu-16.04-server-cloudimg-amd64-disk1.vhd.zip](http://cloud-images.ubuntu.com/releases/xenial/release/ubuntu-16.04-server-cloudimg-amd64-disk1.vhd.zip)</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a779d-111">必要條件</span><span class="sxs-lookup"><span data-stu-id="a779d-111">Prerequisites</span></span>
<span data-ttu-id="a779d-112">本文假設您已將 Ubuntu Linux 作業系統安裝到虛擬硬碟。</span><span class="sxs-lookup"><span data-stu-id="a779d-112">This article assumes that you have already installed an Ubuntu Linux operating system to a virtual hard disk.</span></span> <span data-ttu-id="a779d-113">有多個工具可用來建立 .vhd 檔案，例如，像是 Hyper-V 的虛擬化解決方案。</span><span class="sxs-lookup"><span data-stu-id="a779d-113">Multiple tools exist to create .vhd files, for example a virtualization solution such as Hyper-V.</span></span> <span data-ttu-id="a779d-114">如需指示，請參閱 [安裝 Hyper-V 角色及設定虛擬機器](http://technet.microsoft.com/library/hh846766.aspx)。</span><span class="sxs-lookup"><span data-stu-id="a779d-114">For instructions, see [Install the Hyper-V Role and Configure a Virtual Machine](http://technet.microsoft.com/library/hh846766.aspx).</span></span>

<span data-ttu-id="a779d-115">**Ubuntu 安裝注意事項**</span><span class="sxs-lookup"><span data-stu-id="a779d-115">**Ubuntu installation notes**</span></span>

* <span data-ttu-id="a779d-116">另請參閱[一般 Linux 安裝注意事項](create-upload-generic.md#general-linux-installation-notes)，了解為 Azure 準備 Linux 的更多祕訣。</span><span class="sxs-lookup"><span data-stu-id="a779d-116">Please see also [General Linux Installation Notes](create-upload-generic.md#general-linux-installation-notes) for more tips on preparing Linux for Azure.</span></span>
* <span data-ttu-id="a779d-117">Azure 不支援 VHDX 格式，只支援 **固定 VHD**。</span><span class="sxs-lookup"><span data-stu-id="a779d-117">The VHDX format is not supported in Azure, only **fixed VHD**.</span></span>  <span data-ttu-id="a779d-118">您可以使用 Hyper-V 管理員或 convert-vhd Cmdlet，將磁碟轉換為 VHD 格式。</span><span class="sxs-lookup"><span data-stu-id="a779d-118">You can convert the disk to VHD format using Hyper-V Manager or the convert-vhd cmdlet.</span></span>
* <span data-ttu-id="a779d-119">安裝 Linux 系統時，建議您使用標準磁碟分割而不是 LVM (常是許多安裝的預設設定)。</span><span class="sxs-lookup"><span data-stu-id="a779d-119">When installing the Linux system it is recommended that you use standard partitions rather than LVM (often the default for many installations).</span></span> <span data-ttu-id="a779d-120">這可避免 LVM 與複製之虛擬機器的名稱衝突，特別是為了疑難排解而需要將作業系統磁碟連接至其他虛擬機器時。</span><span class="sxs-lookup"><span data-stu-id="a779d-120">This will avoid LVM name conflicts with cloned VMs, particularly if an OS disk ever needs to be attached to another VM for troubleshooting.</span></span> <span data-ttu-id="a779d-121">如果願意，您可以在資料磁碟上使用 [LVM](configure-lvm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) 或 [RAID](configure-raid.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="a779d-121">[LVM](configure-lvm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) or [RAID](configure-raid.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) may be used on data disks if preferred.</span></span>
* <span data-ttu-id="a779d-122">請勿在作業系統磁碟上設定交換磁碟分割。</span><span class="sxs-lookup"><span data-stu-id="a779d-122">Do not configure a swap partition on the OS disk.</span></span> <span data-ttu-id="a779d-123">您可以設定 Linux 代理程式在暫存資源磁碟上建立交換檔。</span><span class="sxs-lookup"><span data-stu-id="a779d-123">The Linux agent can be configured to create a swap file on the temporary resource disk.</span></span>  <span data-ttu-id="a779d-124">您可以在以下步驟中找到與此有關的詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="a779d-124">More information about this can be found in the steps below.</span></span>
* <span data-ttu-id="a779d-125">所有 VHD 的大小都必須是 1 MB 的倍數。</span><span class="sxs-lookup"><span data-stu-id="a779d-125">All of the VHDs must have sizes that are multiples of 1 MB.</span></span>

## <a name="manual-steps"></a><span data-ttu-id="a779d-126">手動步驟</span><span class="sxs-lookup"><span data-stu-id="a779d-126">Manual steps</span></span>
> [!NOTE]
> <span data-ttu-id="a779d-127">在嘗試為 Azure 建立您的自訂 Ubuntu 映像之前，請考慮改為使用來自 [http://cloud-images.ubuntu.com/](http://cloud-images.ubuntu.com/) 的已預先建置並已測試的映像。</span><span class="sxs-lookup"><span data-stu-id="a779d-127">Before attempting to create your own custom Ubuntu image for Azure, please consider using the pre-built and tested images from [http://cloud-images.ubuntu.com/](http://cloud-images.ubuntu.com/) instead.</span></span>
> 
> 

1. <span data-ttu-id="a779d-128">在 Hyper-V 管理員的中央窗格中，選取虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="a779d-128">In the center pane of Hyper-V Manager, select the virtual machine.</span></span>

2. <span data-ttu-id="a779d-129">按一下 **[連接]** ，以開啟虛擬機器的視窗。</span><span class="sxs-lookup"><span data-stu-id="a779d-129">Click **Connect** to open the window for the virtual machine.</span></span>

3. <span data-ttu-id="a779d-130">取代映像中的目前儲存機制，以使用 Ubuntu 的 Azure 儲存機制。</span><span class="sxs-lookup"><span data-stu-id="a779d-130">Replace the current repositories in the image to use Ubuntu's Azure repos.</span></span> <span data-ttu-id="a779d-131">此步驟會隨著 Ubuntu 版本而略有不同。</span><span class="sxs-lookup"><span data-stu-id="a779d-131">The steps vary slightly depending on the Ubuntu version.</span></span>
   
    <span data-ttu-id="a779d-132">建議您在編輯 `/etc/apt/sources.list` 之前先進行備份：</span><span class="sxs-lookup"><span data-stu-id="a779d-132">Before editing `/etc/apt/sources.list`, it is recommended to make a backup:</span></span>
   
        # sudo cp /etc/apt/sources.list /etc/apt/sources.list.bak

    <span data-ttu-id="a779d-133">Ubuntu 12.04：</span><span class="sxs-lookup"><span data-stu-id="a779d-133">Ubuntu 12.04:</span></span>
   
        # sudo sed -i 's/[a-z][a-z].archive.ubuntu.com/azure.archive.ubuntu.com/g' /etc/apt/sources.list
        # sudo apt-get update

    <span data-ttu-id="a779d-134">Ubuntu 14.04：</span><span class="sxs-lookup"><span data-stu-id="a779d-134">Ubuntu 14.04:</span></span>
   
        # sudo sed -i 's/[a-z][a-z].archive.ubuntu.com/azure.archive.ubuntu.com/g' /etc/apt/sources.list
        # sudo apt-get update

    <span data-ttu-id="a779d-135">Ubuntu 16.04：</span><span class="sxs-lookup"><span data-stu-id="a779d-135">Ubuntu 16.04:</span></span>
   
        # sudo sed -i 's/[a-z][a-z].archive.ubuntu.com/azure.archive.ubuntu.com/g' /etc/apt/sources.list
        # sudo apt-get update

4. <span data-ttu-id="a779d-136">Ubuntu 的 Azure 映像現在遵循「硬體啟用」  (HWE) 核心。</span><span class="sxs-lookup"><span data-stu-id="a779d-136">The Ubuntu Azure images are now following the *hardware enablement* (HWE) kernel.</span></span> <span data-ttu-id="a779d-137">執行下列命令，將作業系統更新為最新的核心：</span><span class="sxs-lookup"><span data-stu-id="a779d-137">Update the operating system to the latest kernel by running the following commands:</span></span>

    <span data-ttu-id="a779d-138">Ubuntu 12.04：</span><span class="sxs-lookup"><span data-stu-id="a779d-138">Ubuntu 12.04:</span></span>
   
        # sudo apt-get update
        # sudo apt-get install linux-image-generic-lts-trusty linux-cloud-tools-generic-lts-trusty
        # sudo apt-get install hv-kvp-daemon-init
        (recommended) sudo apt-get dist-upgrade
   
        # sudo reboot
   
    <span data-ttu-id="a779d-139">Ubuntu 14.04：</span><span class="sxs-lookup"><span data-stu-id="a779d-139">Ubuntu 14.04:</span></span>
   
        # sudo apt-get update
        # sudo apt-get install linux-image-virtual-lts-vivid linux-lts-vivid-tools-common
        # sudo apt-get install hv-kvp-daemon-init
        (recommended) sudo apt-get dist-upgrade
   
        # sudo reboot

    <span data-ttu-id="a779d-140">Ubuntu 16.04：</span><span class="sxs-lookup"><span data-stu-id="a779d-140">Ubuntu 16.04:</span></span>
   
        # sudo apt-get update
        # sudo apt-get install linux-generic-hwe-16.04 linux-cloud-tools-generic-hwe-16.04
        (recommended) sudo apt-get dist-upgrade

        # sudo reboot

    <span data-ttu-id="a779d-141">**另請參閱：**</span><span class="sxs-lookup"><span data-stu-id="a779d-141">**See also:**</span></span>
    - [<span data-ttu-id="a779d-142">https://wiki.ubuntu.com/Kernel/LTSEnablementStack</span><span class="sxs-lookup"><span data-stu-id="a779d-142">https://wiki.ubuntu.com/Kernel/LTSEnablementStack</span></span>](https://wiki.ubuntu.com/Kernel/LTSEnablementStack)
    - [<span data-ttu-id="a779d-143">https://wiki.ubuntu.com/Kernel/RollingLTSEnablementStack</span><span class="sxs-lookup"><span data-stu-id="a779d-143">https://wiki.ubuntu.com/Kernel/RollingLTSEnablementStack</span></span>](https://wiki.ubuntu.com/Kernel/RollingLTSEnablementStack)


5. <span data-ttu-id="a779d-144">修改 Grub 的核心開機程式行，使其額外包含用於 Azure 的核心參數。</span><span class="sxs-lookup"><span data-stu-id="a779d-144">Modify the kernel boot line for Grub to include additional kernel parameters for Azure.</span></span> <span data-ttu-id="a779d-145">若要這樣做，請在文字編輯器中開啟 `/etc/default/grub`，找到名為 `GRUB_CMDLINE_LINUX_DEFAULT` 的變數 (或視需要加入它)，然後進行編輯以使其包含以下參數：</span><span class="sxs-lookup"><span data-stu-id="a779d-145">To do this open `/etc/default/grub` in a text editor, find the variable called `GRUB_CMDLINE_LINUX_DEFAULT` (or add it if needed) and edit it to include the following parameters:</span></span>
   
        GRUB_CMDLINE_LINUX_DEFAULT="console=tty1 console=ttyS0,115200n8 earlyprintk=ttyS0,115200 rootdelay=300"

    <span data-ttu-id="a779d-146">儲存並關閉此檔案，然後執行 `sudo update-grub`。</span><span class="sxs-lookup"><span data-stu-id="a779d-146">Save and close this file, and then run `sudo update-grub`.</span></span> <span data-ttu-id="a779d-147">這將確保所有主控台訊息都會傳送給第一個序列埠，有助於 Azure 技術支援團隊進行問題偵錯程序。</span><span class="sxs-lookup"><span data-stu-id="a779d-147">This will ensure all console messages are sent to the first serial port, which can assist Azure technical support with debugging issues.</span></span>

6. <span data-ttu-id="a779d-148">確定您已安裝 SSH 伺服器，並已設定為在開機時啟動。</span><span class="sxs-lookup"><span data-stu-id="a779d-148">Ensure that the SSH server is installed and configured to start at boot time.</span></span>  <span data-ttu-id="a779d-149">這通常是預設值。</span><span class="sxs-lookup"><span data-stu-id="a779d-149">This is usually the default.</span></span>

7. <span data-ttu-id="a779d-150">安裝 Azure Linux 代理程式：</span><span class="sxs-lookup"><span data-stu-id="a779d-150">Install the Azure Linux Agent:</span></span>
   
        # sudo apt-get update
        # sudo apt-get install walinuxagent

    >[!Note]
    <span data-ttu-id="a779d-151">若已安裝 `NetworkManager` 和 `NetworkManager-gnome` 套件，則 `walinuxagent` 套件可能會將它們移除。</span><span class="sxs-lookup"><span data-stu-id="a779d-151">The `walinuxagent` package may remove the `NetworkManager` and `NetworkManager-gnome` packages, if they are installed.</span></span>

8. <span data-ttu-id="a779d-152">執行下列命令，以取消佈建虛擬機器，並準備將它佈建於 Azure 上：</span><span class="sxs-lookup"><span data-stu-id="a779d-152">Run the following commands to deprovision the virtual machine and prepare it for provisioning on Azure:</span></span>
   
        # sudo waagent -force -deprovision
        # export HISTSIZE=0
        # logout

9. <span data-ttu-id="a779d-153">在 Hyper-V 管理員中，依序按一下 [動作] -> [關閉]。</span><span class="sxs-lookup"><span data-stu-id="a779d-153">Click **Action -> Shut Down** in Hyper-V Manager.</span></span> <span data-ttu-id="a779d-154">您現在可以將 Linux VHD 上傳至 Azure。</span><span class="sxs-lookup"><span data-stu-id="a779d-154">Your Linux VHD is now ready to be uploaded to Azure.</span></span>

## <a name="next-steps"></a><span data-ttu-id="a779d-155">後續步驟</span><span class="sxs-lookup"><span data-stu-id="a779d-155">Next steps</span></span>
<span data-ttu-id="a779d-156">您現在可以開始使用您的 Ubuntu Linux 虛擬硬碟在 Azure 建立新的虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="a779d-156">You're now ready to use your Ubuntu Linux virtual hard disk to create new virtual machines in Azure.</span></span> <span data-ttu-id="a779d-157">若這是您第一次將該 .vhd 檔案上傳到 Azure，請參閱 [建立及上傳包含 Linux 作業系統的虛擬硬碟](classic/create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)中的步驟 2 和步驟 3。</span><span class="sxs-lookup"><span data-stu-id="a779d-157">If this is the first time that you're uploading the .vhd file to Azure, see steps 2 and 3 in [Creating and uploading a virtual hard disk that contains the Linux operating system](classic/create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).</span></span>

## <a name="references"></a><span data-ttu-id="a779d-158">參考</span><span class="sxs-lookup"><span data-stu-id="a779d-158">References</span></span>
<span data-ttu-id="a779d-159">Ubuntu 硬體啟用 (HWE) 核心：</span><span class="sxs-lookup"><span data-stu-id="a779d-159">Ubuntu hardware enablement (HWE) kernel:</span></span>

* [<span data-ttu-id="a779d-160">http://blog.utlemming.org/2015/01/ubuntu-1404-azure-images-now-tracking.html</span><span class="sxs-lookup"><span data-stu-id="a779d-160">http://blog.utlemming.org/2015/01/ubuntu-1404-azure-images-now-tracking.html</span></span>](http://blog.utlemming.org/2015/01/ubuntu-1404-azure-images-now-tracking.html)
* [<span data-ttu-id="a779d-161">http://blog.utlemming.org/2015/02/1204-azure-cloud-images-now-using-hwe.html</span><span class="sxs-lookup"><span data-stu-id="a779d-161">http://blog.utlemming.org/2015/02/1204-azure-cloud-images-now-using-hwe.html</span></span>](http://blog.utlemming.org/2015/02/1204-azure-cloud-images-now-using-hwe.html)

