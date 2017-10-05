---
title: "建立及上傳 Oracle Linux VHD | Microsoft Docs"
description: "了解如何建立及上傳包含 Oracle Linux 作業系統的 Azure 虛擬硬碟 (VHD)。"
services: virtual-machines-linux
documentationcenter: 
author: szarkos
manager: timlt
editor: tysonn
tags: azure-service-management,azure-resource-manager
ms.assetid: dd96f771-26eb-4391-9a89-8c8b6d691822
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 02/23/2017
ms.author: szark
ms.openlocfilehash: c631ddf3acf6df7364c03eb4691b78be0493e0d9
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="prepare-an-oracle-linux-virtual-machine-for-azure"></a><span data-ttu-id="bc228-103">準備用於 Azure 的 Oracle Linux 虛擬機器</span><span class="sxs-lookup"><span data-stu-id="bc228-103">Prepare an Oracle Linux virtual machine for Azure</span></span>
[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-both-include.md)]

## <a name="prerequisites"></a><span data-ttu-id="bc228-104">必要條件</span><span class="sxs-lookup"><span data-stu-id="bc228-104">Prerequisites</span></span>
<span data-ttu-id="bc228-105">本文假設您已將 Oracle Linux 作業系統安裝到虛擬硬碟。</span><span class="sxs-lookup"><span data-stu-id="bc228-105">This article assumes that you have already installed an Oracle Linux operating system to a virtual hard disk.</span></span> <span data-ttu-id="bc228-106">有多個工具可用來建立 .vhd 檔案，例如，像是 Hyper-V 的虛擬化解決方案。</span><span class="sxs-lookup"><span data-stu-id="bc228-106">Multiple tools exist to create .vhd files, for example a virtualization solution such as Hyper-V.</span></span> <span data-ttu-id="bc228-107">如需指示，請參閱 [安裝 Hyper-V 角色及設定虛擬機器](http://technet.microsoft.com/library/hh846766.aspx)。</span><span class="sxs-lookup"><span data-stu-id="bc228-107">For instructions, see [Install the Hyper-V Role and Configure a Virtual Machine](http://technet.microsoft.com/library/hh846766.aspx).</span></span>

### <a name="oracle-linux-installation-notes"></a><span data-ttu-id="bc228-108">Oracle Linux 安裝注意事項</span><span class="sxs-lookup"><span data-stu-id="bc228-108">Oracle Linux installation notes</span></span>
* <span data-ttu-id="bc228-109">如需有關準備 Azure 之 Linux 的更多秘訣，另請參閱 [一般 Linux 安裝注意事項](create-upload-generic.md#general-linux-installation-notes) 。</span><span class="sxs-lookup"><span data-stu-id="bc228-109">Please see also [General Linux Installation Notes](create-upload-generic.md#general-linux-installation-notes) for more tips on preparing Linux for Azure.</span></span>
* <span data-ttu-id="bc228-110">Hyper-V 和 Azure 都支援 Oracle 的 Red Hat 相容核心及其 UEK3 (Unbreakable Enterprise Kernel)。</span><span class="sxs-lookup"><span data-stu-id="bc228-110">Oracle's Red Hat compatible kernel and their UEK3 (Unbreakable Enterprise Kernel) are both supported on Hyper-V and Azure.</span></span> <span data-ttu-id="bc228-111">若要獲得最佳結果，請在準備執行 Oracle Linux VHD 的同時，確實更新到最新核心。</span><span class="sxs-lookup"><span data-stu-id="bc228-111">For best results, please be sure to update to the latest kernel while preparing your Oracle Linux VHD.</span></span>
* <span data-ttu-id="bc228-112">Hyper-V 和 Azure 不支援 Oracle 的 UEK2，因為它不包含必要的驅動程式。</span><span class="sxs-lookup"><span data-stu-id="bc228-112">Oracle's UEK2 is not supported on Hyper-V and Azure as it does not include the required drivers.</span></span>
* <span data-ttu-id="bc228-113">Azure 不支援 VHDX 格式，只支援 **固定 VHD**。</span><span class="sxs-lookup"><span data-stu-id="bc228-113">The VHDX format is not supported in Azure, only **fixed VHD**.</span></span>  <span data-ttu-id="bc228-114">您可以使用 Hyper-V 管理員或 convert-vhd Cmdlet，將磁碟轉換為 VHD 格式。</span><span class="sxs-lookup"><span data-stu-id="bc228-114">You can convert the disk to VHD format using Hyper-V Manager or the convert-vhd cmdlet.</span></span>
* <span data-ttu-id="bc228-115">安裝 Linux 系統時，建議您使用標準磁碟分割而不是 LVM (常是許多安裝的預設設定)。</span><span class="sxs-lookup"><span data-stu-id="bc228-115">When installing the Linux system it is recommended that you use standard partitions rather than LVM (often the default for many installations).</span></span> <span data-ttu-id="bc228-116">這可避免 LVM 與複製之虛擬機器的名稱衝突，特別是為了疑難排解而需要將作業系統磁碟連接至其他虛擬機器時。</span><span class="sxs-lookup"><span data-stu-id="bc228-116">This will avoid LVM name conflicts with cloned VMs, particularly if an OS disk ever needs to be attached to another VM for troubleshooting.</span></span> <span data-ttu-id="bc228-117">如果願意，您可以在資料磁碟上使用 [LVM](configure-lvm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) 或 [RAID](configure-raid.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="bc228-117">[LVM](configure-lvm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) or [RAID](configure-raid.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) may be used on data disks if preferred.</span></span>
* <span data-ttu-id="bc228-118">由於 2.6.37 以下的 Linux 核心版本有錯誤，因此較大的 VM 不支援 NUMA。</span><span class="sxs-lookup"><span data-stu-id="bc228-118">NUMA is not supported for larger VM sizes due to a bug in Linux kernel versions below 2.6.37.</span></span> <span data-ttu-id="bc228-119">這個問題主要會影響使用上游 Red Hat 2.6.32 kernel 的散發套件。</span><span class="sxs-lookup"><span data-stu-id="bc228-119">This issue primarily impacts distributions using the upstream Red Hat 2.6.32 kernel.</span></span> <span data-ttu-id="bc228-120">手動安裝 Azure Linux 代理程式 (waagent) 將會自動停用 Linux Kernel GRUB 組態中的 NUMA。</span><span class="sxs-lookup"><span data-stu-id="bc228-120">Manual installation of the Azure Linux agent (waagent) will automatically disable NUMA in the GRUB configuration for the Linux kernel.</span></span> <span data-ttu-id="bc228-121">您可以在以下步驟中找到與此有關的詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="bc228-121">More information about this can be found in the steps below.</span></span>
* <span data-ttu-id="bc228-122">請勿在作業系統磁碟上設定交換磁碟分割。</span><span class="sxs-lookup"><span data-stu-id="bc228-122">Do not configure a swap partition on the OS disk.</span></span> <span data-ttu-id="bc228-123">您可以設定 Linux 代理程式在暫存資源磁碟上建立交換檔。</span><span class="sxs-lookup"><span data-stu-id="bc228-123">The Linux agent can be configured to create a swap file on the temporary resource disk.</span></span>  <span data-ttu-id="bc228-124">您可以在以下步驟中找到與此有關的詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="bc228-124">More information about this can be found in the steps below.</span></span>
* <span data-ttu-id="bc228-125">所有 VHD 的大小都必須是 1 MB 的倍數。</span><span class="sxs-lookup"><span data-stu-id="bc228-125">All of the VHDs must have sizes that are multiples of 1 MB.</span></span>
* <span data-ttu-id="bc228-126">確定已啟用 `Addons` 儲存機制。</span><span class="sxs-lookup"><span data-stu-id="bc228-126">Make sure that the `Addons` repository is enabled.</span></span> <span data-ttu-id="bc228-127">編輯檔案 `/etc/yum.repo.d/public-yum-ol6.repo`(Oracle Linux 6) 或 `/etc/yum.repo.d/public-yum-ol7.repo`(Oracle Linux)，將此檔案中 **[ol6_addons]** 或 **[ol7_addons]** 底下的 `enabled=0` 一行變更為 `enabled=1`。</span><span class="sxs-lookup"><span data-stu-id="bc228-127">Edit the file `/etc/yum.repo.d/public-yum-ol6.repo`(Oracle Linux 6) or `/etc/yum.repo.d/public-yum-ol7.repo`(Oracle Linux ), and change the line `enabled=0` to `enabled=1` under **[ol6_addons]** or **[ol7_addons]** in this file.</span></span>

## <a name="oracle-linux-64"></a><span data-ttu-id="bc228-128">Oracle Linux 6.4+</span><span class="sxs-lookup"><span data-stu-id="bc228-128">Oracle Linux 6.4+</span></span>
<span data-ttu-id="bc228-129">您必須在作業系統中完成特定組態步驟，虛擬機器才能在 Azure 中執行。</span><span class="sxs-lookup"><span data-stu-id="bc228-129">You must complete specific configuration steps in the operating system for the virtual machine to run in Azure.</span></span>

1. <span data-ttu-id="bc228-130">在 Hyper-V 管理員的中央窗格中，選取虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="bc228-130">In the center pane of Hyper-V Manager, select the virtual machine.</span></span>
2. <span data-ttu-id="bc228-131">按一下 **[連接]** ，以開啟虛擬機器的視窗。</span><span class="sxs-lookup"><span data-stu-id="bc228-131">Click **Connect** to open the window for the virtual machine.</span></span>
3. <span data-ttu-id="bc228-132">執行下列命令以解除安裝 NetworkManager：</span><span class="sxs-lookup"><span data-stu-id="bc228-132">Uninstall NetworkManager by running the following command:</span></span>
   
        # sudo rpm -e --nodeps NetworkManager
   
    <span data-ttu-id="bc228-133">**注意：** 如果尚未安裝封裝，此命令將會失敗，並出現錯誤訊息。</span><span class="sxs-lookup"><span data-stu-id="bc228-133">**Note:** If the package is not already installed, this command will fail with an error message.</span></span> <span data-ttu-id="bc228-134">這是預期行為。</span><span class="sxs-lookup"><span data-stu-id="bc228-134">This is expected.</span></span>
4. <span data-ttu-id="bc228-135">在 `/etc/sysconfig/` 目錄中，建立名為 **network** 且包含下列文字的檔案：</span><span class="sxs-lookup"><span data-stu-id="bc228-135">Create a file named **network** in the `/etc/sysconfig/` directory that contains the following text:</span></span>
   
        NETWORKING=yes
        HOSTNAME=localhost.localdomain
5. <span data-ttu-id="bc228-136">在 `/etc/sysconfig/network-scripts/` 目錄中，建立名為 **ifcfg-eth0** 且包含下列文字的檔案：</span><span class="sxs-lookup"><span data-stu-id="bc228-136">Create a file named **ifcfg-eth0** in the `/etc/sysconfig/network-scripts/` directory that contains the following text:</span></span>
   
        DEVICE=eth0
        ONBOOT=yes
        BOOTPROTO=dhcp
        TYPE=Ethernet
        USERCTL=no
        PEERDNS=yes
        IPV6INIT=no
6. <span data-ttu-id="bc228-137">修改 udev 角色可防止產生乙太網路介面的靜態規則。</span><span class="sxs-lookup"><span data-stu-id="bc228-137">Modify udev rules to avoid generating static rules for the Ethernet interface(s).</span></span> <span data-ttu-id="bc228-138">在 Microsoft Azure 或 Hyper-V 中複製虛擬機器時，這些規則可能會造成問題：</span><span class="sxs-lookup"><span data-stu-id="bc228-138">These rules can cause problems when cloning a virtual machine in Microsoft Azure or Hyper-V:</span></span>
   
        # sudo ln -s /dev/null /etc/udev/rules.d/75-persistent-net-generator.rules
        # sudo rm -f /etc/udev/rules.d/70-persistent-net.rules
7. <span data-ttu-id="bc228-139">要確保開機時會啟動網路服務，可執行以下命令：</span><span class="sxs-lookup"><span data-stu-id="bc228-139">Ensure the network service will start at boot time by running the following command:</span></span>
   
        # chkconfig network on
8. <span data-ttu-id="bc228-140">執行下列命令以安裝 python-pyasn1：</span><span class="sxs-lookup"><span data-stu-id="bc228-140">Install python-pyasn1 by running the following command:</span></span>
   
        # sudo yum install python-pyasn1
9. <span data-ttu-id="bc228-141">修改 grub 組態中的核心開機那一行，使其額外包含用於 Azure 的核心參數。</span><span class="sxs-lookup"><span data-stu-id="bc228-141">Modify the kernel boot line in your grub configuration to include additional kernel parameters for Azure.</span></span> <span data-ttu-id="bc228-142">作法是，在文字編輯器中開啟 "/boot/grub/menu.lst"，並確定預設核心包含以下參數：</span><span class="sxs-lookup"><span data-stu-id="bc228-142">To do this open "/boot/grub/menu.lst" in a text editor and ensure that the default kernel includes the following parameters:</span></span>
   
        console=ttyS0 earlyprintk=ttyS0 rootdelay=300 numa=off
   
   <span data-ttu-id="bc228-143">這也將確保所有主控台訊息都會傳送給第一個序列埠，有助於 Azure 支援團隊進行問題偵錯程序。</span><span class="sxs-lookup"><span data-stu-id="bc228-143">This will also ensure all console messages are sent to the first serial port, which can assist Azure support with debugging issues.</span></span> <span data-ttu-id="bc228-144">因為 Oracle Red Hat 相容核心的一個錯誤，這將會停用 NUMA。</span><span class="sxs-lookup"><span data-stu-id="bc228-144">This will disable NUMA due to a bug in Oracle's Red Hat compatible kernel.</span></span>
   
   <span data-ttu-id="bc228-145">除了上述以外，我們還建議您 *移除* 下列參數：</span><span class="sxs-lookup"><span data-stu-id="bc228-145">In addition to the above, it is recommended to *remove* the following parameters:</span></span>
   
        rhgb quiet crashkernel=auto
   
   <span data-ttu-id="bc228-146">在雲端環境中，我們會將所有記錄傳送到序列埠，因此不適合使用圖形化和無訊息啟動。</span><span class="sxs-lookup"><span data-stu-id="bc228-146">Graphical and quiet boot are not useful in a cloud environment where we want all the logs to be sent to the serial port.</span></span>
   
   <span data-ttu-id="bc228-147">如有需要，您可以保留 `crashkernel` 選項的設定，但請注意，此參數將會減少 VM 中約 128MB 或以上的可用記憶體數量，這在較小的 VM 中可能會是個問題。</span><span class="sxs-lookup"><span data-stu-id="bc228-147">The `crashkernel` option may be left configured if desired, but note that this parameter will reduce the amount of available memory in the VM by 128MB or more, which may be problematic on the smaller VM sizes.</span></span>
10. <span data-ttu-id="bc228-148">確定您已安裝 SSH 伺服器，並已設定為在開機時啟動。</span><span class="sxs-lookup"><span data-stu-id="bc228-148">Ensure that the SSH server is installed and configured to start at boot time.</span></span>  <span data-ttu-id="bc228-149">這通常是預設值。</span><span class="sxs-lookup"><span data-stu-id="bc228-149">This is usually the default.</span></span>
11. <span data-ttu-id="bc228-150">執行以下命令來安裝 Azure Linux 代理程式。</span><span class="sxs-lookup"><span data-stu-id="bc228-150">Install the Azure Linux Agent by running the following command.</span></span> <span data-ttu-id="bc228-151">最新版為 2.0.15。</span><span class="sxs-lookup"><span data-stu-id="bc228-151">The latest version is 2.0.15.</span></span>
    
        # sudo yum install WALinuxAgent
    
    <span data-ttu-id="bc228-152">請注意，如果 NetworkManager 和 NetworkManager-gnome 套件沒有如步驟 2 所述遭到移除，則在安裝 WALinuxAgent 套件時會將這兩個套件移除。</span><span class="sxs-lookup"><span data-stu-id="bc228-152">Note that installing the WALinuxAgent package will remove the NetworkManager and NetworkManager-gnome packages if they were not already removed as described in step 2.</span></span>
12. <span data-ttu-id="bc228-153">請勿在作業系統磁碟上建立交換空間。</span><span class="sxs-lookup"><span data-stu-id="bc228-153">Do not create swap space on the OS disk.</span></span>
    
    <span data-ttu-id="bc228-154">Azure Linux 代理程式可在 VM 佈建於 Azure 後，使用附加至 VM 的本機資源磁碟自動設定交換空間。</span><span class="sxs-lookup"><span data-stu-id="bc228-154">The Azure Linux Agent can automatically configure swap space using the local resource disk that is attached to the VM after provisioning on Azure.</span></span> <span data-ttu-id="bc228-155">請注意，資源磁碟是 *暫存* 磁碟，可能會在 VM 取消佈建時清空。</span><span class="sxs-lookup"><span data-stu-id="bc228-155">Note that the local resource disk is a *temporary* disk, and might be emptied when the VM is deprovisioned.</span></span> <span data-ttu-id="bc228-156">安裝 Azure Linux 代理程式 (請參閱上一個步驟) 後，請在 /etc/waagent.conf 中適當修改下列參數：</span><span class="sxs-lookup"><span data-stu-id="bc228-156">After installing the Azure Linux Agent (see previous step), modify the following parameters in /etc/waagent.conf appropriately:</span></span>
    
        ResourceDisk.Format=y
        ResourceDisk.Filesystem=ext4
        ResourceDisk.MountPoint=/mnt/resource
        ResourceDisk.EnableSwap=y
        ResourceDisk.SwapSizeMB=2048    ## NOTE: set this to whatever you need it to be.
13. <span data-ttu-id="bc228-157">執行下列命令，以取消佈建虛擬機器，並準備將其佈建於 Azure 上：</span><span class="sxs-lookup"><span data-stu-id="bc228-157">Run the following commands to deprovision the virtual machine and prepare it for provisioning on Azure:</span></span>
    
        # sudo waagent -force -deprovision
        # export HISTSIZE=0
        # logout
14. <span data-ttu-id="bc228-158">在 Hyper-V 管理員中，依序按一下 [動作] -> [關閉]。</span><span class="sxs-lookup"><span data-stu-id="bc228-158">Click **Action -> Shut Down** in Hyper-V Manager.</span></span> <span data-ttu-id="bc228-159">您現在可以將 Linux VHD 上傳至 Azure。</span><span class="sxs-lookup"><span data-stu-id="bc228-159">Your Linux VHD is now ready to be uploaded to Azure.</span></span>

- - -
## <a name="oracle-linux-70"></a><span data-ttu-id="bc228-160">Oracle Linux 7.0+</span><span class="sxs-lookup"><span data-stu-id="bc228-160">Oracle Linux 7.0+</span></span>
<span data-ttu-id="bc228-161">**Oracle Linux 7 中的變更**</span><span class="sxs-lookup"><span data-stu-id="bc228-161">**Changes in Oracle Linux 7**</span></span>

<span data-ttu-id="bc228-162">準備適用於 Azure 的 Oracle Linux 7 虛擬機器會與 Oracle Linux 6 極為類似，不過，其中有幾個重要差異值得注意：</span><span class="sxs-lookup"><span data-stu-id="bc228-162">Preparing an Oracle Linux 7 virtual machine for Azure is very similar to Oracle Linux 6, however there are several important differences worth noting:</span></span>

* <span data-ttu-id="bc228-163">Azure 支援 Red Hat 相容核心和 Oracle 的 UEK3。</span><span class="sxs-lookup"><span data-stu-id="bc228-163">Both the Red Hat compatible kernel and Oracle's UEK3 are supported in Azure.</span></span>  <span data-ttu-id="bc228-164">建議使用 UEK3 核心。</span><span class="sxs-lookup"><span data-stu-id="bc228-164">The UEK3 kernel is recommended.</span></span>
* <span data-ttu-id="bc228-165">NetworkManager 封裝不會再與 Azure Linux 代理程式發生衝突。</span><span class="sxs-lookup"><span data-stu-id="bc228-165">The NetworkManager package no longer conflicts with the Azure Linux agent.</span></span> <span data-ttu-id="bc228-166">依預設會安裝此封裝，建議您不要將它移除。</span><span class="sxs-lookup"><span data-stu-id="bc228-166">This package is installed by default and we recommend that it is not removed.</span></span>
* <span data-ttu-id="bc228-167">GRUB2 現已作為預設的開機載入器使用，因此我們已變更編輯核心參數的程序 (如下所示)。</span><span class="sxs-lookup"><span data-stu-id="bc228-167">GRUB2 is now used as the default bootloader, so the procedure for editing kernel parameters has changed (see below).</span></span>
* <span data-ttu-id="bc228-168">XFS 現為預設的檔案系統。</span><span class="sxs-lookup"><span data-stu-id="bc228-168">XFS is now the default file system.</span></span> <span data-ttu-id="bc228-169">如有需要，您仍可使用 ext4 檔案系統。</span><span class="sxs-lookup"><span data-stu-id="bc228-169">The ext4 file system can still be used if desired.</span></span>

<span data-ttu-id="bc228-170">**組態步驟**</span><span class="sxs-lookup"><span data-stu-id="bc228-170">**Configuration steps**</span></span>

1. <span data-ttu-id="bc228-171">在 Hyper-V 管理員中，選取虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="bc228-171">In Hyper-V Manager, select the virtual machine.</span></span>
2. <span data-ttu-id="bc228-172">按一下 [連接]  ，以開啟虛擬機器的主控台視窗。</span><span class="sxs-lookup"><span data-stu-id="bc228-172">Click **Connect** to open a console window for the virtual machine.</span></span>
3. <span data-ttu-id="bc228-173">在 `/etc/sysconfig/` 目錄中，建立名為 **network** 且包含下列文字的檔案：</span><span class="sxs-lookup"><span data-stu-id="bc228-173">Create a file named **network** in the `/etc/sysconfig/` directory that contains the following text:</span></span>
   
        NETWORKING=yes
        HOSTNAME=localhost.localdomain
4. <span data-ttu-id="bc228-174">在 `/etc/sysconfig/network-scripts/` 目錄中，建立名為 **ifcfg-eth0** 且包含下列文字的檔案：</span><span class="sxs-lookup"><span data-stu-id="bc228-174">Create a file named **ifcfg-eth0** in the `/etc/sysconfig/network-scripts/` directory that contains the following text:</span></span>
   
        DEVICE=eth0
        ONBOOT=yes
        BOOTPROTO=dhcp
        TYPE=Ethernet
        USERCTL=no
        PEERDNS=yes
        IPV6INIT=no
5. <span data-ttu-id="bc228-175">修改 udev 角色可防止產生乙太網路介面的靜態規則。</span><span class="sxs-lookup"><span data-stu-id="bc228-175">Modify udev rules to avoid generating static rules for the Ethernet interface(s).</span></span> <span data-ttu-id="bc228-176">在 Microsoft Azure 或 Hyper-V 中複製虛擬機器時，這些規則可能會造成問題：</span><span class="sxs-lookup"><span data-stu-id="bc228-176">These rules can cause problems when cloning a virtual machine in Microsoft Azure or Hyper-V:</span></span>
   
        # sudo ln -s /dev/null /etc/udev/rules.d/75-persistent-net-generator.rules
6. <span data-ttu-id="bc228-177">要確保開機時會啟動網路服務，可執行以下命令：</span><span class="sxs-lookup"><span data-stu-id="bc228-177">Ensure the network service will start at boot time by running the following command:</span></span>
   
        # sudo chkconfig network on
7. <span data-ttu-id="bc228-178">執行下列命令以安裝 python-pyasn1 封裝：</span><span class="sxs-lookup"><span data-stu-id="bc228-178">Install the python-pyasn1 package by running the following command:</span></span>
   
        # sudo yum install python-pyasn1
8. <span data-ttu-id="bc228-179">執行下列命令，以清除目前的 yum 中繼資料並安裝任何更新：</span><span class="sxs-lookup"><span data-stu-id="bc228-179">Run the following command to clear the current yum metadata and install any updates:</span></span>
   
        # sudo yum clean all
        # sudo yum -y update
9. <span data-ttu-id="bc228-180">修改 grub 組態中的核心開機那一行，使其額外包含用於 Azure 的核心參數。</span><span class="sxs-lookup"><span data-stu-id="bc228-180">Modify the kernel boot line in your grub configuration to include additional kernel parameters for Azure.</span></span> <span data-ttu-id="bc228-181">若要執行這個動作，請在文字編輯器中開啟 "/etc/default/grub" 並編輯 `GRUB_CMDLINE_LINUX` 參數，例如：</span><span class="sxs-lookup"><span data-stu-id="bc228-181">To do this open "/etc/default/grub" in a text editor and edit the `GRUB_CMDLINE_LINUX` parameter, for example:</span></span>
   
        GRUB_CMDLINE_LINUX="rootdelay=300 console=ttyS0 earlyprintk=ttyS0 net.ifnames=0"
   
   <span data-ttu-id="bc228-182">這也將確保所有主控台訊息都會傳送給第一個序列埠，有助於 Azure 支援團隊進行問題偵錯程序。</span><span class="sxs-lookup"><span data-stu-id="bc228-182">This will also ensure all console messages are sent to the first serial port, which can assist Azure support with debugging issues.</span></span> <span data-ttu-id="bc228-183">也會關閉新的 OEL 7 對 NIC 的命名慣例。</span><span class="sxs-lookup"><span data-stu-id="bc228-183">It also turns off the new OEL 7 naming conventions for NICs.</span></span> <span data-ttu-id="bc228-184">除了上述以外，我們還建議您 *移除* 下列參數：</span><span class="sxs-lookup"><span data-stu-id="bc228-184">In addition to the above, it is recommended to *remove* the following parameters:</span></span>
   
       rhgb quiet crashkernel=auto
   
   <span data-ttu-id="bc228-185">在雲端環境中，我們會將所有記錄傳送到序列埠，因此不適合使用圖形化和無訊息啟動。</span><span class="sxs-lookup"><span data-stu-id="bc228-185">Graphical and quiet boot are not useful in a cloud environment where we want all the logs to be sent to the serial port.</span></span>
   
   <span data-ttu-id="bc228-186">如有需要，您可以保留 `crashkernel` 選項的設定，但請注意，此參數將會減少 VM 中約 128MB 或以上的可用記憶體數量，這在較小的 VM 中可能會是個問題。</span><span class="sxs-lookup"><span data-stu-id="bc228-186">The `crashkernel` option may be left configured if desired, but note that this parameter will reduce the amount of available memory in the VM by 128MB or more, which may be problematic on the smaller VM sizes.</span></span>
10. <span data-ttu-id="bc228-187">在您參照上述完成編輯 "/etc/default/grub" 之後，請執行下列命令以重建 grub 組態：</span><span class="sxs-lookup"><span data-stu-id="bc228-187">Once you are done editing "/etc/default/grub" per above, run the following command to rebuild the grub configuration:</span></span>
    
        # sudo grub2-mkconfig -o /boot/grub2/grub.cfg
11. <span data-ttu-id="bc228-188">確定您已安裝 SSH 伺服器，並已設定為在開機時啟動。</span><span class="sxs-lookup"><span data-stu-id="bc228-188">Ensure that the SSH server is installed and configured to start at boot time.</span></span>  <span data-ttu-id="bc228-189">這通常是預設值。</span><span class="sxs-lookup"><span data-stu-id="bc228-189">This is usually the default.</span></span>
12. <span data-ttu-id="bc228-190">執行以下命令來安裝 Azure Linux 代理程式：</span><span class="sxs-lookup"><span data-stu-id="bc228-190">Install the Azure Linux Agent by running the following command:</span></span>
    
        # sudo yum install WALinuxAgent
        # sudo systemctl enable waagent
13. <span data-ttu-id="bc228-191">請勿在作業系統磁碟上建立交換空間。</span><span class="sxs-lookup"><span data-stu-id="bc228-191">Do not create swap space on the OS disk.</span></span>
    
    <span data-ttu-id="bc228-192">Azure Linux 代理程式可在 VM 佈建於 Azure 後，使用附加至 VM 的本機資源磁碟自動設定交換空間。</span><span class="sxs-lookup"><span data-stu-id="bc228-192">The Azure Linux Agent can automatically configure swap space using the local resource disk that is attached to the VM after provisioning on Azure.</span></span> <span data-ttu-id="bc228-193">請注意，資源磁碟是 *暫存* 磁碟，可能會在 VM 取消佈建時清空。</span><span class="sxs-lookup"><span data-stu-id="bc228-193">Note that the local resource disk is a *temporary* disk, and might be emptied when the VM is deprovisioned.</span></span> <span data-ttu-id="bc228-194">安裝 Azure Linux 代理程式 (請參閱上一個步驟) 後，請在 /etc/waagent.conf 中適當修改下列參數：</span><span class="sxs-lookup"><span data-stu-id="bc228-194">After installing the Azure Linux Agent (see the previous step), modify the following parameters in /etc/waagent.conf appropriately:</span></span>
    
        ResourceDisk.Format=y
        ResourceDisk.Filesystem=ext4
        ResourceDisk.MountPoint=/mnt/resource
        ResourceDisk.EnableSwap=y
        ResourceDisk.SwapSizeMB=2048    ## NOTE: set this to whatever you need it to be.
14. <span data-ttu-id="bc228-195">執行下列命令，以取消佈建虛擬機器，並準備將其佈建於 Azure 上：</span><span class="sxs-lookup"><span data-stu-id="bc228-195">Run the following commands to deprovision the virtual machine and prepare it for provisioning on Azure:</span></span>
    
        # sudo waagent -force -deprovision
        # export HISTSIZE=0
        # logout
15. <span data-ttu-id="bc228-196">在 Hyper-V 管理員中，依序按一下 [動作] -> [關閉]。</span><span class="sxs-lookup"><span data-stu-id="bc228-196">Click **Action -> Shut Down** in Hyper-V Manager.</span></span> <span data-ttu-id="bc228-197">您現在可以將 Linux VHD 上傳至 Azure。</span><span class="sxs-lookup"><span data-stu-id="bc228-197">Your Linux VHD is now ready to be uploaded to Azure.</span></span>

## <a name="next-steps"></a><span data-ttu-id="bc228-198">後續步驟</span><span class="sxs-lookup"><span data-stu-id="bc228-198">Next steps</span></span>
<span data-ttu-id="bc228-199">您現在可以開始使用您的 Oracle Linux .vhd 在 Azure 中建立新的虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="bc228-199">You're now ready to use your Oracle Linux .vhd to create new virtual machines in Azure.</span></span> <span data-ttu-id="bc228-200">若這是您第一次將該 .vhd 檔案上傳到 Azure，請參閱 [建立及上傳包含 Linux 作業系統的虛擬硬碟](classic/create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)中的步驟 2 和步驟 3。</span><span class="sxs-lookup"><span data-stu-id="bc228-200">If this is the first time that you're uploading the .vhd file to Azure, see steps 2 and 3 in [Creating and uploading a virtual hard disk that contains the Linux operating system](classic/create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).</span></span>

