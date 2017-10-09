---
title: "aaaCreate 和 Oracle Linux VHD 上傳 |Microsoft 文件"
description: "了解 toocreate 和上傳 Azure 虛擬硬碟 (VHD)，其中包含 Oracle Linux 作業系統。"
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
ms.openlocfilehash: be9cf284d7f5e7122a106506a343e53e9f1ac56e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="prepare-an-oracle-linux-virtual-machine-for-azure"></a><span data-ttu-id="b2383-103">準備用於 Azure 的 Oracle Linux 虛擬機器</span><span class="sxs-lookup"><span data-stu-id="b2383-103">Prepare an Oracle Linux virtual machine for Azure</span></span>
[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-both-include.md)]

## <a name="prerequisites"></a><span data-ttu-id="b2383-104">必要條件</span><span class="sxs-lookup"><span data-stu-id="b2383-104">Prerequisites</span></span>
<span data-ttu-id="b2383-105">本文假設您已安裝 Oracle Linux 作業系統 tooa 虛擬硬碟。</span><span class="sxs-lookup"><span data-stu-id="b2383-105">This article assumes that you have already installed an Oracle Linux operating system tooa virtual hard disk.</span></span> <span data-ttu-id="b2383-106">多個工具存在 toocreate.vhd 檔案，例如 HYPER-V 之類的虛擬化解決方案。</span><span class="sxs-lookup"><span data-stu-id="b2383-106">Multiple tools exist toocreate .vhd files, for example a virtualization solution such as Hyper-V.</span></span> <span data-ttu-id="b2383-107">如需指示，請參閱[安裝 hello HYPER-V 角色和設定虛擬機器](http://technet.microsoft.com/library/hh846766.aspx)。</span><span class="sxs-lookup"><span data-stu-id="b2383-107">For instructions, see [Install hello Hyper-V Role and Configure a Virtual Machine](http://technet.microsoft.com/library/hh846766.aspx).</span></span>

### <a name="oracle-linux-installation-notes"></a><span data-ttu-id="b2383-108">Oracle Linux 安裝注意事項</span><span class="sxs-lookup"><span data-stu-id="b2383-108">Oracle Linux installation notes</span></span>
* <span data-ttu-id="b2383-109">如需有關準備 Azure 之 Linux 的更多秘訣，另請參閱 [一般 Linux 安裝注意事項](create-upload-generic.md#general-linux-installation-notes) 。</span><span class="sxs-lookup"><span data-stu-id="b2383-109">Please see also [General Linux Installation Notes](create-upload-generic.md#general-linux-installation-notes) for more tips on preparing Linux for Azure.</span></span>
* <span data-ttu-id="b2383-110">Hyper-V 和 Azure 都支援 Oracle 的 Red Hat 相容核心及其 UEK3 (Unbreakable Enterprise Kernel)。</span><span class="sxs-lookup"><span data-stu-id="b2383-110">Oracle's Red Hat compatible kernel and their UEK3 (Unbreakable Enterprise Kernel) are both supported on Hyper-V and Azure.</span></span> <span data-ttu-id="b2383-111">為獲得最佳結果，請確定 tooupdate toohello 最新的核心是準備 Oracle Linux VHD 時。</span><span class="sxs-lookup"><span data-stu-id="b2383-111">For best results, please be sure tooupdate toohello latest kernel while preparing your Oracle Linux VHD.</span></span>
* <span data-ttu-id="b2383-112">Oracle 的 UEK2 不會支援在 HYPER-V 和 Azure 上，因為它不包含所需的 hello 驅動程式。</span><span class="sxs-lookup"><span data-stu-id="b2383-112">Oracle's UEK2 is not supported on Hyper-V and Azure as it does not include hello required drivers.</span></span>
* <span data-ttu-id="b2383-113">hello VHDX 格式不支援在 Azure 中，只有**固定 VHD**。</span><span class="sxs-lookup"><span data-stu-id="b2383-113">hello VHDX format is not supported in Azure, only **fixed VHD**.</span></span>  <span data-ttu-id="b2383-114">您可以將使用 HYPER-V 管理員 hello 磁碟 tooVHD 格式轉換或 hello convert-vhd 指令程式。</span><span class="sxs-lookup"><span data-stu-id="b2383-114">You can convert hello disk tooVHD format using Hyper-V Manager or hello convert-vhd cmdlet.</span></span>
* <span data-ttu-id="b2383-115">當安裝 hello Linux 系統建議您使用標準的資料分割，而非 LVM （通常 hello 預設值為許多安裝）。</span><span class="sxs-lookup"><span data-stu-id="b2383-115">When installing hello Linux system it is recommended that you use standard partitions rather than LVM (often hello default for many installations).</span></span> <span data-ttu-id="b2383-116">特別是當作業系統磁碟曾經需要附加 toobe tooanother VM 進行疑難排解，這樣可避免與複製 Vm，LVM 名稱衝突。</span><span class="sxs-lookup"><span data-stu-id="b2383-116">This will avoid LVM name conflicts with cloned VMs, particularly if an OS disk ever needs toobe attached tooanother VM for troubleshooting.</span></span> <span data-ttu-id="b2383-117">如果願意，您可以在資料磁碟上使用 [LVM](configure-lvm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) 或 [RAID](configure-raid.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="b2383-117">[LVM](configure-lvm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) or [RAID](configure-raid.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) may be used on data disks if preferred.</span></span>
* <span data-ttu-id="b2383-118">較大的 VM 大小，因為 tooa bug 下方 2.6.37 Linux 核心版本中不支援 NUMA。</span><span class="sxs-lookup"><span data-stu-id="b2383-118">NUMA is not supported for larger VM sizes due tooa bug in Linux kernel versions below 2.6.37.</span></span> <span data-ttu-id="b2383-119">這個問題主要影響使用散發 hello 上游 Red Hat 2.6.32 核心。</span><span class="sxs-lookup"><span data-stu-id="b2383-119">This issue primarily impacts distributions using hello upstream Red Hat 2.6.32 kernel.</span></span> <span data-ttu-id="b2383-120">手動安裝的 hello Azure Linux 代理程式 (waagent) 會自動停用 NUMA hello Linux 核心 hello 幼蟲組態中。</span><span class="sxs-lookup"><span data-stu-id="b2383-120">Manual installation of hello Azure Linux agent (waagent) will automatically disable NUMA in hello GRUB configuration for hello Linux kernel.</span></span> <span data-ttu-id="b2383-121">相關資訊位於下列 hello 步驟。</span><span class="sxs-lookup"><span data-stu-id="b2383-121">More information about this can be found in hello steps below.</span></span>
* <span data-ttu-id="b2383-122">請勿設定 hello OS 磁碟交換資料分割。</span><span class="sxs-lookup"><span data-stu-id="b2383-122">Do not configure a swap partition on hello OS disk.</span></span> <span data-ttu-id="b2383-123">hello Linux 代理程式可以設定的 toocreate 交換磁碟上的檔案 hello 暫存資源。</span><span class="sxs-lookup"><span data-stu-id="b2383-123">hello Linux agent can be configured toocreate a swap file on hello temporary resource disk.</span></span>  <span data-ttu-id="b2383-124">相關資訊位於下列 hello 步驟。</span><span class="sxs-lookup"><span data-stu-id="b2383-124">More information about this can be found in hello steps below.</span></span>
* <span data-ttu-id="b2383-125">所有 hello Vhd 必須是 1 MB 的倍數的大小。</span><span class="sxs-lookup"><span data-stu-id="b2383-125">All of hello VHDs must have sizes that are multiples of 1 MB.</span></span>
* <span data-ttu-id="b2383-126">請確定該 hello`Addons`儲存機制已啟用。</span><span class="sxs-lookup"><span data-stu-id="b2383-126">Make sure that hello `Addons` repository is enabled.</span></span> <span data-ttu-id="b2383-127">編輯 hello 檔案`/etc/yum.repo.d/public-yum-ol6.repo`(Oracle Linux 6) 或`/etc/yum.repo.d/public-yum-ol7.repo`(Oracle Linux)，並變更 hello 行`enabled=0`太`enabled=1`下**[ol6_addons]**或**[ol7_addons]**中檔案。</span><span class="sxs-lookup"><span data-stu-id="b2383-127">Edit hello file `/etc/yum.repo.d/public-yum-ol6.repo`(Oracle Linux 6) or `/etc/yum.repo.d/public-yum-ol7.repo`(Oracle Linux ), and change hello line `enabled=0` too`enabled=1` under **[ol6_addons]** or **[ol7_addons]** in this file.</span></span>

## <a name="oracle-linux-64"></a><span data-ttu-id="b2383-128">Oracle Linux 6.4+</span><span class="sxs-lookup"><span data-stu-id="b2383-128">Oracle Linux 6.4+</span></span>
<span data-ttu-id="b2383-129">您必須完成的 hello Azure 中的虛擬機器 toorun hello 作業系統中的特定設定步驟。</span><span class="sxs-lookup"><span data-stu-id="b2383-129">You must complete specific configuration steps in hello operating system for hello virtual machine toorun in Azure.</span></span>

1. <span data-ttu-id="b2383-130">Hello 選取中間窗格內的 HYPER-V 管理員，hello 虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="b2383-130">In hello center pane of Hyper-V Manager, select hello virtual machine.</span></span>
2. <span data-ttu-id="b2383-131">按一下**連接**tooopen hello 視窗 hello 虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="b2383-131">Click **Connect** tooopen hello window for hello virtual machine.</span></span>
3. <span data-ttu-id="b2383-132">解除安裝 NetworkManager，藉由執行下列命令的 hello:</span><span class="sxs-lookup"><span data-stu-id="b2383-132">Uninstall NetworkManager by running hello following command:</span></span>
   
        # sudo rpm -e --nodeps NetworkManager
   
    <span data-ttu-id="b2383-133">**注意：**如果尚未安裝 hello 封裝，此命令將會失敗並出現錯誤訊息。</span><span class="sxs-lookup"><span data-stu-id="b2383-133">**Note:** If hello package is not already installed, this command will fail with an error message.</span></span> <span data-ttu-id="b2383-134">這是預期行為。</span><span class="sxs-lookup"><span data-stu-id="b2383-134">This is expected.</span></span>
4. <span data-ttu-id="b2383-135">建立名為**網路**在 hello`/etc/sysconfig/`目錄，包含下列文字的 hello:</span><span class="sxs-lookup"><span data-stu-id="b2383-135">Create a file named **network** in hello `/etc/sysconfig/` directory that contains hello following text:</span></span>
   
        NETWORKING=yes
        HOSTNAME=localhost.localdomain
5. <span data-ttu-id="b2383-136">建立名為**ifcfg eth0**在 hello`/etc/sysconfig/network-scripts/`目錄，包含下列文字的 hello:</span><span class="sxs-lookup"><span data-stu-id="b2383-136">Create a file named **ifcfg-eth0** in hello `/etc/sysconfig/network-scripts/` directory that contains hello following text:</span></span>
   
        DEVICE=eth0
        ONBOOT=yes
        BOOTPROTO=dhcp
        TYPE=Ethernet
        USERCTL=no
        PEERDNS=yes
        IPV6INIT=no
6. <span data-ttu-id="b2383-137">修改 udev 規則 tooavoid 產生 hello 乙太網路介面的靜態規則。</span><span class="sxs-lookup"><span data-stu-id="b2383-137">Modify udev rules tooavoid generating static rules for hello Ethernet interface(s).</span></span> <span data-ttu-id="b2383-138">在 Microsoft Azure 或 Hyper-V 中複製虛擬機器時，這些規則可能會造成問題：</span><span class="sxs-lookup"><span data-stu-id="b2383-138">These rules can cause problems when cloning a virtual machine in Microsoft Azure or Hyper-V:</span></span>
   
        # sudo ln -s /dev/null /etc/udev/rules.d/75-persistent-net-generator.rules
        # sudo rm -f /etc/udev/rules.d/70-persistent-net.rules
7. <span data-ttu-id="b2383-139">請確定 hello 網路服務將會在開機時啟動藉由執行下列命令的 hello:</span><span class="sxs-lookup"><span data-stu-id="b2383-139">Ensure hello network service will start at boot time by running hello following command:</span></span>
   
        # chkconfig network on
8. <span data-ttu-id="b2383-140">安裝 python pyasn1 藉由執行下列命令的 hello:</span><span class="sxs-lookup"><span data-stu-id="b2383-140">Install python-pyasn1 by running hello following command:</span></span>
   
        # sudo yum install python-pyasn1
9. <span data-ttu-id="b2383-141">修改 Azure hello 核心開機行幼蟲組態 tooinclude 其他核心參數中。</span><span class="sxs-lookup"><span data-stu-id="b2383-141">Modify hello kernel boot line in your grub configuration tooinclude additional kernel parameters for Azure.</span></span> <span data-ttu-id="b2383-142">此開啟 toodo"/ boot/grub/menu.lst 「 文字編輯器中並確認該 hello 預設核心中包含下列參數的 hello:</span><span class="sxs-lookup"><span data-stu-id="b2383-142">toodo this open "/boot/grub/menu.lst" in a text editor and ensure that hello default kernel includes hello following parameters:</span></span>
   
        console=ttyS0 earlyprintk=ttyS0 rootdelay=300 numa=off
   
   <span data-ttu-id="b2383-143">這也可確保所有的主控台訊息都會傳送 toohello 第一個序列連接埠，這可協助 Azure 偵錯問題的支援。</span><span class="sxs-lookup"><span data-stu-id="b2383-143">This will also ensure all console messages are sent toohello first serial port, which can assist Azure support with debugging issues.</span></span> <span data-ttu-id="b2383-144">這會停用 NUMA，因為 Oracle 的 Red Hat 相容核心 tooa bug。</span><span class="sxs-lookup"><span data-stu-id="b2383-144">This will disable NUMA due tooa bug in Oracle's Red Hat compatible kernel.</span></span>
   
   <span data-ttu-id="b2383-145">除了上述 toohello 建議太*移除*hello 下列參數：</span><span class="sxs-lookup"><span data-stu-id="b2383-145">In addition toohello above, it is recommended too*remove* hello following parameters:</span></span>
   
        rhgb quiet crashkernel=auto
   
   <span data-ttu-id="b2383-146">沒有適用於雲端環境，我們想要傳送 toohello 序列連接埠的所有 hello 記錄 toobe 圖形和無訊息的開機。</span><span class="sxs-lookup"><span data-stu-id="b2383-146">Graphical and quiet boot are not useful in a cloud environment where we want all hello logs toobe sent toohello serial port.</span></span>
   
   <span data-ttu-id="b2383-147">hello`crashkernel`選項可能會是左設定如有需要，但請注意，這個參數會減少 hello hello 128 MB 以上，VM 中可用的記憶體數量可能會造成問題 hello 較小的 VM 大小。</span><span class="sxs-lookup"><span data-stu-id="b2383-147">hello `crashkernel` option may be left configured if desired, but note that this parameter will reduce hello amount of available memory in hello VM by 128MB or more, which may be problematic on hello smaller VM sizes.</span></span>
10. <span data-ttu-id="b2383-148">請確定該 hello SSH 伺服器是在安裝並設定 toostart 開機時間。</span><span class="sxs-lookup"><span data-stu-id="b2383-148">Ensure that hello SSH server is installed and configured toostart at boot time.</span></span>  <span data-ttu-id="b2383-149">這通常是 hello 預設值。</span><span class="sxs-lookup"><span data-stu-id="b2383-149">This is usually hello default.</span></span>
11. <span data-ttu-id="b2383-150">執行下列命令的 hello 安裝 hello Azure Linux 代理程式。</span><span class="sxs-lookup"><span data-stu-id="b2383-150">Install hello Azure Linux Agent by running hello following command.</span></span> <span data-ttu-id="b2383-151">hello 最新版本是 2.0.15。</span><span class="sxs-lookup"><span data-stu-id="b2383-151">hello latest version is 2.0.15.</span></span>
    
        # sudo yum install WALinuxAgent
    
    <span data-ttu-id="b2383-152">請注意，安裝 hello WALinuxAgent 封裝將會移除 hello NetworkManager NetworkManager gnome 封裝沒有已移除所述，是否在步驟 2。</span><span class="sxs-lookup"><span data-stu-id="b2383-152">Note that installing hello WALinuxAgent package will remove hello NetworkManager and NetworkManager-gnome packages if they were not already removed as described in step 2.</span></span>
12. <span data-ttu-id="b2383-153">不要在 hello OS 磁碟上建立的交換空間。</span><span class="sxs-lookup"><span data-stu-id="b2383-153">Do not create swap space on hello OS disk.</span></span>
    
    <span data-ttu-id="b2383-154">hello Azure Linux 代理程式可以自動設定使用之後附加的 toohello VM 在 Azure 上佈建的 hello 本機資源磁碟的交換空間。</span><span class="sxs-lookup"><span data-stu-id="b2383-154">hello Azure Linux Agent can automatically configure swap space using hello local resource disk that is attached toohello VM after provisioning on Azure.</span></span> <span data-ttu-id="b2383-155">請注意該 hello 本機資源磁碟是*暫存*磁碟，以及可能會在取消佈建 hello VM 時清空。</span><span class="sxs-lookup"><span data-stu-id="b2383-155">Note that hello local resource disk is a *temporary* disk, and might be emptied when hello VM is deprovisioned.</span></span> <span data-ttu-id="b2383-156">在安裝之後 hello Azure Linux 代理程式 （請參閱上一個步驟），修改適當地遵循 /etc/waagent.conf 中的參數的 hello:</span><span class="sxs-lookup"><span data-stu-id="b2383-156">After installing hello Azure Linux Agent (see previous step), modify hello following parameters in /etc/waagent.conf appropriately:</span></span>
    
        ResourceDisk.Format=y
        ResourceDisk.Filesystem=ext4
        ResourceDisk.MountPoint=/mnt/resource
        ResourceDisk.EnableSwap=y
        ResourceDisk.SwapSizeMB=2048    ## NOTE: set this toowhatever you need it toobe.
13. <span data-ttu-id="b2383-157">執行下列命令 toodeprovision hello 虛擬機器的 hello 並準備在 Azure 上佈建：</span><span class="sxs-lookup"><span data-stu-id="b2383-157">Run hello following commands toodeprovision hello virtual machine and prepare it for provisioning on Azure:</span></span>
    
        # sudo waagent -force -deprovision
        # export HISTSIZE=0
        # logout
14. <span data-ttu-id="b2383-158">在 Hyper-V 管理員中，依序按一下 [動作] -> [關閉]。</span><span class="sxs-lookup"><span data-stu-id="b2383-158">Click **Action -> Shut Down** in Hyper-V Manager.</span></span> <span data-ttu-id="b2383-159">Linux VHD 是現在準備好 toobe 上傳 tooAzure。</span><span class="sxs-lookup"><span data-stu-id="b2383-159">Your Linux VHD is now ready toobe uploaded tooAzure.</span></span>

- - -
## <a name="oracle-linux-70"></a><span data-ttu-id="b2383-160">Oracle Linux 7.0+</span><span class="sxs-lookup"><span data-stu-id="b2383-160">Oracle Linux 7.0+</span></span>
<span data-ttu-id="b2383-161">**Oracle Linux 7 中的變更**</span><span class="sxs-lookup"><span data-stu-id="b2383-161">**Changes in Oracle Linux 7**</span></span>

<span data-ttu-id="b2383-162">準備 Azure 的 Oracle Linux 7 虛擬機器是非常類似 tooOracle Linux 6，不過，有數個值得注意的重要差異：</span><span class="sxs-lookup"><span data-stu-id="b2383-162">Preparing an Oracle Linux 7 virtual machine for Azure is very similar tooOracle Linux 6, however there are several important differences worth noting:</span></span>

* <span data-ttu-id="b2383-163">Azure 支援 hello Red Hat 相容核心和 Oracle 的 UEK3。</span><span class="sxs-lookup"><span data-stu-id="b2383-163">Both hello Red Hat compatible kernel and Oracle's UEK3 are supported in Azure.</span></span>  <span data-ttu-id="b2383-164">建議您使用 hello UEK3 核心。</span><span class="sxs-lookup"><span data-stu-id="b2383-164">hello UEK3 kernel is recommended.</span></span>
* <span data-ttu-id="b2383-165">hello NetworkManager 封裝不會再與 hello Azure Linux 代理程式發生衝突。</span><span class="sxs-lookup"><span data-stu-id="b2383-165">hello NetworkManager package no longer conflicts with hello Azure Linux agent.</span></span> <span data-ttu-id="b2383-166">依預設會安裝此封裝，建議您不要將它移除。</span><span class="sxs-lookup"><span data-stu-id="b2383-166">This package is installed by default and we recommend that it is not removed.</span></span>
* <span data-ttu-id="b2383-167">GRUB2 現在用做 hello 預設開機載入器，因此編輯核心參數 hello 程序已變更 （請參閱下方）。</span><span class="sxs-lookup"><span data-stu-id="b2383-167">GRUB2 is now used as hello default bootloader, so hello procedure for editing kernel parameters has changed (see below).</span></span>
* <span data-ttu-id="b2383-168">XFS 現在是 hello 預設檔案系統。</span><span class="sxs-lookup"><span data-stu-id="b2383-168">XFS is now hello default file system.</span></span> <span data-ttu-id="b2383-169">如有需要，仍可以使用 hello ext4 檔案系統。</span><span class="sxs-lookup"><span data-stu-id="b2383-169">hello ext4 file system can still be used if desired.</span></span>

<span data-ttu-id="b2383-170">**組態步驟**</span><span class="sxs-lookup"><span data-stu-id="b2383-170">**Configuration steps**</span></span>

1. <span data-ttu-id="b2383-171">在 HYPER-V 管理員 中，選取 hello 虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="b2383-171">In Hyper-V Manager, select hello virtual machine.</span></span>
2. <span data-ttu-id="b2383-172">按一下**連接**tooopen hello 虛擬機器的主控台視窗。</span><span class="sxs-lookup"><span data-stu-id="b2383-172">Click **Connect** tooopen a console window for hello virtual machine.</span></span>
3. <span data-ttu-id="b2383-173">建立名為**網路**在 hello`/etc/sysconfig/`目錄，包含下列文字的 hello:</span><span class="sxs-lookup"><span data-stu-id="b2383-173">Create a file named **network** in hello `/etc/sysconfig/` directory that contains hello following text:</span></span>
   
        NETWORKING=yes
        HOSTNAME=localhost.localdomain
4. <span data-ttu-id="b2383-174">建立名為**ifcfg eth0**在 hello`/etc/sysconfig/network-scripts/`目錄，包含下列文字的 hello:</span><span class="sxs-lookup"><span data-stu-id="b2383-174">Create a file named **ifcfg-eth0** in hello `/etc/sysconfig/network-scripts/` directory that contains hello following text:</span></span>
   
        DEVICE=eth0
        ONBOOT=yes
        BOOTPROTO=dhcp
        TYPE=Ethernet
        USERCTL=no
        PEERDNS=yes
        IPV6INIT=no
5. <span data-ttu-id="b2383-175">修改 udev 規則 tooavoid 產生 hello 乙太網路介面的靜態規則。</span><span class="sxs-lookup"><span data-stu-id="b2383-175">Modify udev rules tooavoid generating static rules for hello Ethernet interface(s).</span></span> <span data-ttu-id="b2383-176">在 Microsoft Azure 或 Hyper-V 中複製虛擬機器時，這些規則可能會造成問題：</span><span class="sxs-lookup"><span data-stu-id="b2383-176">These rules can cause problems when cloning a virtual machine in Microsoft Azure or Hyper-V:</span></span>
   
        # sudo ln -s /dev/null /etc/udev/rules.d/75-persistent-net-generator.rules
6. <span data-ttu-id="b2383-177">請確定 hello 網路服務將會在開機時啟動藉由執行下列命令的 hello:</span><span class="sxs-lookup"><span data-stu-id="b2383-177">Ensure hello network service will start at boot time by running hello following command:</span></span>
   
        # sudo chkconfig network on
7. <span data-ttu-id="b2383-178">執行下列命令的 hello 安裝 hello python pyasn1 封裝：</span><span class="sxs-lookup"><span data-stu-id="b2383-178">Install hello python-pyasn1 package by running hello following command:</span></span>
   
        # sudo yum install python-pyasn1
8. <span data-ttu-id="b2383-179">執行下列命令 tooclear hello 目前 yum 中繼資料的 hello 並安裝任何更新：</span><span class="sxs-lookup"><span data-stu-id="b2383-179">Run hello following command tooclear hello current yum metadata and install any updates:</span></span>
   
        # sudo yum clean all
        # sudo yum -y update
9. <span data-ttu-id="b2383-180">修改 Azure hello 核心開機行幼蟲組態 tooinclude 其他核心參數中。</span><span class="sxs-lookup"><span data-stu-id="b2383-180">Modify hello kernel boot line in your grub configuration tooinclude additional kernel parameters for Azure.</span></span> <span data-ttu-id="b2383-181">此開啟"/ 等/預設/幼蟲"toodo 在文字編輯器，編輯 hello`GRUB_CMDLINE_LINUX`參數，例如：</span><span class="sxs-lookup"><span data-stu-id="b2383-181">toodo this open "/etc/default/grub" in a text editor and edit hello `GRUB_CMDLINE_LINUX` parameter, for example:</span></span>
   
        GRUB_CMDLINE_LINUX="rootdelay=300 console=ttyS0 earlyprintk=ttyS0 net.ifnames=0"
   
   <span data-ttu-id="b2383-182">這也可確保所有的主控台訊息都會傳送 toohello 第一個序列連接埠，這可協助 Azure 偵錯問題的支援。</span><span class="sxs-lookup"><span data-stu-id="b2383-182">This will also ensure all console messages are sent toohello first serial port, which can assist Azure support with debugging issues.</span></span> <span data-ttu-id="b2383-183">它也會關閉 hello 新 OEL 7 命名慣例的 Nic。</span><span class="sxs-lookup"><span data-stu-id="b2383-183">It also turns off hello new OEL 7 naming conventions for NICs.</span></span> <span data-ttu-id="b2383-184">除了上述 toohello 建議太*移除*hello 下列參數：</span><span class="sxs-lookup"><span data-stu-id="b2383-184">In addition toohello above, it is recommended too*remove* hello following parameters:</span></span>
   
       rhgb quiet crashkernel=auto
   
   <span data-ttu-id="b2383-185">沒有適用於雲端環境，我們想要傳送 toohello 序列連接埠的所有 hello 記錄 toobe 圖形和無訊息的開機。</span><span class="sxs-lookup"><span data-stu-id="b2383-185">Graphical and quiet boot are not useful in a cloud environment where we want all hello logs toobe sent toohello serial port.</span></span>
   
   <span data-ttu-id="b2383-186">hello`crashkernel`選項可能會是左設定如有需要，但請注意，這個參數會減少 hello hello 128 MB 以上，VM 中可用的記憶體數量可能會造成問題 hello 較小的 VM 大小。</span><span class="sxs-lookup"><span data-stu-id="b2383-186">hello `crashkernel` option may be left configured if desired, but note that this parameter will reduce hello amount of available memory in hello VM by 128MB or more, which may be problematic on hello smaller VM sizes.</span></span>
10. <span data-ttu-id="b2383-187">在您完成編輯"/ 等/預設/幼蟲"每個以上版本，執行下列命令 toorebuild hello 幼蟲組態 hello:</span><span class="sxs-lookup"><span data-stu-id="b2383-187">Once you are done editing "/etc/default/grub" per above, run hello following command toorebuild hello grub configuration:</span></span>
    
        # sudo grub2-mkconfig -o /boot/grub2/grub.cfg
11. <span data-ttu-id="b2383-188">請確定該 hello SSH 伺服器是在安裝並設定 toostart 開機時間。</span><span class="sxs-lookup"><span data-stu-id="b2383-188">Ensure that hello SSH server is installed and configured toostart at boot time.</span></span>  <span data-ttu-id="b2383-189">這通常是 hello 預設值。</span><span class="sxs-lookup"><span data-stu-id="b2383-189">This is usually hello default.</span></span>
12. <span data-ttu-id="b2383-190">執行下列命令的 hello 安裝 hello Azure Linux 代理程式：</span><span class="sxs-lookup"><span data-stu-id="b2383-190">Install hello Azure Linux Agent by running hello following command:</span></span>
    
        # sudo yum install WALinuxAgent
        # sudo systemctl enable waagent
13. <span data-ttu-id="b2383-191">不要在 hello OS 磁碟上建立的交換空間。</span><span class="sxs-lookup"><span data-stu-id="b2383-191">Do not create swap space on hello OS disk.</span></span>
    
    <span data-ttu-id="b2383-192">hello Azure Linux 代理程式可以自動設定使用之後附加的 toohello VM 在 Azure 上佈建的 hello 本機資源磁碟的交換空間。</span><span class="sxs-lookup"><span data-stu-id="b2383-192">hello Azure Linux Agent can automatically configure swap space using hello local resource disk that is attached toohello VM after provisioning on Azure.</span></span> <span data-ttu-id="b2383-193">請注意該 hello 本機資源磁碟是*暫存*磁碟，以及可能會在取消佈建 hello VM 時清空。</span><span class="sxs-lookup"><span data-stu-id="b2383-193">Note that hello local resource disk is a *temporary* disk, and might be emptied when hello VM is deprovisioned.</span></span> <span data-ttu-id="b2383-194">在安裝之後 hello Azure Linux 代理程式 （請參閱 hello 上一個步驟），修改適當地遵循 /etc/waagent.conf 中的參數的 hello:</span><span class="sxs-lookup"><span data-stu-id="b2383-194">After installing hello Azure Linux Agent (see hello previous step), modify hello following parameters in /etc/waagent.conf appropriately:</span></span>
    
        ResourceDisk.Format=y
        ResourceDisk.Filesystem=ext4
        ResourceDisk.MountPoint=/mnt/resource
        ResourceDisk.EnableSwap=y
        ResourceDisk.SwapSizeMB=2048    ## NOTE: set this toowhatever you need it toobe.
14. <span data-ttu-id="b2383-195">執行下列命令 toodeprovision hello 虛擬機器的 hello 並準備在 Azure 上佈建：</span><span class="sxs-lookup"><span data-stu-id="b2383-195">Run hello following commands toodeprovision hello virtual machine and prepare it for provisioning on Azure:</span></span>
    
        # sudo waagent -force -deprovision
        # export HISTSIZE=0
        # logout
15. <span data-ttu-id="b2383-196">在 Hyper-V 管理員中，依序按一下 [動作] -> [關閉]。</span><span class="sxs-lookup"><span data-stu-id="b2383-196">Click **Action -> Shut Down** in Hyper-V Manager.</span></span> <span data-ttu-id="b2383-197">Linux VHD 是現在準備好 toobe 上傳 tooAzure。</span><span class="sxs-lookup"><span data-stu-id="b2383-197">Your Linux VHD is now ready toobe uploaded tooAzure.</span></span>

## <a name="next-steps"></a><span data-ttu-id="b2383-198">後續步驟</span><span class="sxs-lookup"><span data-stu-id="b2383-198">Next steps</span></span>
<span data-ttu-id="b2383-199">您要現在準備好 toouse Oracle Linux.vhd toocreate 新虛擬機器在 Azure 中。</span><span class="sxs-lookup"><span data-stu-id="b2383-199">You're now ready toouse your Oracle Linux .vhd toocreate new virtual machines in Azure.</span></span> <span data-ttu-id="b2383-200">如果這是 hello 正在上傳 hello.vhd 檔案 tooAzure 的第一次，請參閱步驟 2 和 3 中的[建立和上傳包含 hello Linux 作業系統的虛擬硬碟](classic/create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="b2383-200">If this is hello first time that you're uploading hello .vhd file tooAzure, see steps 2 and 3 in [Creating and uploading a virtual hard disk that contains hello Linux operating system](classic/create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).</span></span>

