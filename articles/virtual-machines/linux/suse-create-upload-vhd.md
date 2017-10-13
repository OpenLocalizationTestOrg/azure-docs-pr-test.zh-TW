---
title: "aaaCreate 和上傳在 Azure 中的 SUSE Linux VHD"
description: "了解 toocreate 和上傳 Azure 虛擬硬碟 (VHD)，其中包含 SUSE Linux 作業系統。"
services: virtual-machines-linux
documentationcenter: 
author: szarkos
manager: timlt
editor: tysonn
tags: azure-resource-manager,azure-service-management
ms.assetid: 066d01a6-2a54-4718-bcd0-90fe7a5303a1
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 08/24/2016
ms.author: szark
ms.openlocfilehash: 9185c7e67279357f00db0f43e944e96c58f0dd60
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="prepare-a-sles-or-opensuse-virtual-machine-for-azure"></a><span data-ttu-id="6cf7d-103">準備適用於 Azure 的 SLES 或 openSUSE 虛擬機器</span><span class="sxs-lookup"><span data-stu-id="6cf7d-103">Prepare a SLES or openSUSE virtual machine for Azure</span></span>
[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-both-include.md)]

## <a name="prerequisites"></a><span data-ttu-id="6cf7d-104">必要條件</span><span class="sxs-lookup"><span data-stu-id="6cf7d-104">Prerequisites</span></span>
<span data-ttu-id="6cf7d-105">本文假設您有已安裝 SUSE 或 openSUSE Linux 作業系統 tooa 虛擬硬碟。</span><span class="sxs-lookup"><span data-stu-id="6cf7d-105">This article assumes that you have already installed a SUSE or openSUSE Linux operating system tooa virtual hard disk.</span></span> <span data-ttu-id="6cf7d-106">多個工具存在 toocreate.vhd 檔案，例如 HYPER-V 之類的虛擬化解決方案。</span><span class="sxs-lookup"><span data-stu-id="6cf7d-106">Multiple tools exist toocreate .vhd files, for example a virtualization solution such as Hyper-V.</span></span> <span data-ttu-id="6cf7d-107">如需指示，請參閱[安裝 hello HYPER-V 角色和設定虛擬機器](http://technet.microsoft.com/library/hh846766.aspx)。</span><span class="sxs-lookup"><span data-stu-id="6cf7d-107">For instructions, see [Install hello Hyper-V Role and Configure a Virtual Machine](http://technet.microsoft.com/library/hh846766.aspx).</span></span>

### <a name="sles--opensuse-installation-notes"></a><span data-ttu-id="6cf7d-108">SLES / openSUSE 安裝注意事項</span><span class="sxs-lookup"><span data-stu-id="6cf7d-108">SLES / openSUSE installation notes</span></span>
* <span data-ttu-id="6cf7d-109">另請參閱[一般 Linux 安裝注意事項](create-upload-generic.md#general-linux-installation-notes)，了解為 Azure 準備 Linux 的更多祕訣。</span><span class="sxs-lookup"><span data-stu-id="6cf7d-109">Please see also [General Linux Installation Notes](create-upload-generic.md#general-linux-installation-notes) for more tips on preparing Linux for Azure.</span></span>
* <span data-ttu-id="6cf7d-110">hello VHDX 格式不支援在 Azure 中，只有**固定 VHD**。</span><span class="sxs-lookup"><span data-stu-id="6cf7d-110">hello VHDX format is not supported in Azure, only **fixed VHD**.</span></span>  <span data-ttu-id="6cf7d-111">您可以將使用 HYPER-V 管理員 hello 磁碟 tooVHD 格式轉換或 hello convert-vhd 指令程式。</span><span class="sxs-lookup"><span data-stu-id="6cf7d-111">You can convert hello disk tooVHD format using Hyper-V Manager or hello convert-vhd cmdlet.</span></span>
* <span data-ttu-id="6cf7d-112">當安裝 hello Linux 系統建議您使用標準的資料分割，而非 LVM （通常 hello 預設值為許多安裝）。</span><span class="sxs-lookup"><span data-stu-id="6cf7d-112">When installing hello Linux system it is recommended that you use standard partitions rather than LVM (often hello default for many installations).</span></span> <span data-ttu-id="6cf7d-113">特別是當作業系統磁碟曾經需要附加 toobe tooanother VM 進行疑難排解，這樣可避免與複製 Vm，LVM 名稱衝突。</span><span class="sxs-lookup"><span data-stu-id="6cf7d-113">This will avoid LVM name conflicts with cloned VMs, particularly if an OS disk ever needs toobe attached tooanother VM for troubleshooting.</span></span> <span data-ttu-id="6cf7d-114">如果願意，您可以在資料磁碟上使用 [LVM](configure-lvm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) 或 [RAID](configure-raid.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="6cf7d-114">[LVM](configure-lvm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) or [RAID](configure-raid.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) may be used on data disks if preferred.</span></span>
* <span data-ttu-id="6cf7d-115">請勿設定 hello OS 磁碟交換資料分割。</span><span class="sxs-lookup"><span data-stu-id="6cf7d-115">Do not configure a swap partition on hello OS disk.</span></span> <span data-ttu-id="6cf7d-116">hello Linux 代理程式可以設定的 toocreate 交換磁碟上的檔案 hello 暫存資源。</span><span class="sxs-lookup"><span data-stu-id="6cf7d-116">hello Linux agent can be configured toocreate a swap file on hello temporary resource disk.</span></span>  <span data-ttu-id="6cf7d-117">相關資訊位於下列 hello 步驟。</span><span class="sxs-lookup"><span data-stu-id="6cf7d-117">More information about this can be found in hello steps below.</span></span>
* <span data-ttu-id="6cf7d-118">所有 hello Vhd 必須是 1 MB 的倍數的大小。</span><span class="sxs-lookup"><span data-stu-id="6cf7d-118">All of hello VHDs must have sizes that are multiples of 1 MB.</span></span>

## <a name="use-suse-studio"></a><span data-ttu-id="6cf7d-119">使用 SUSE Studio</span><span class="sxs-lookup"><span data-stu-id="6cf7d-119">Use SUSE Studio</span></span>
<span data-ttu-id="6cf7d-120">[SUSE Studio](http://www.susestudio.com) 可讓您輕鬆建立及管理 Azure 和 Hyper-V 的 SLES 與 openSUSE 映像。</span><span class="sxs-lookup"><span data-stu-id="6cf7d-120">[SUSE Studio](http://www.susestudio.com) can easily create and manage your SLES and openSUSE images for Azure and Hyper-V.</span></span> <span data-ttu-id="6cf7d-121">這是建議的方法，自訂您自己 SLES 和 openSUSE 映像的 hello。</span><span class="sxs-lookup"><span data-stu-id="6cf7d-121">This is hello recommended approach for customizing your own SLES and openSUSE images.</span></span>

<span data-ttu-id="6cf7d-122">做為替代的 toobuilding 您自己的 VHD、 SUSE 也發行 BYOS （攜帶您自己訂閱） 映像在 sles [VMDepot](https://vmdepot.msopentech.com/User/Show?user=1007)。</span><span class="sxs-lookup"><span data-stu-id="6cf7d-122">As an alternative toobuilding your own VHD, SUSE also publishes BYOS (Bring Your Own Subscription) images for SLES at [VMDepot](https://vmdepot.msopentech.com/User/Show?user=1007).</span></span>

## <a name="prepare-suse-linux-enterprise-server-11-sp4"></a><span data-ttu-id="6cf7d-123">準備 SUSE Linux Enterprise Server 11 SP4</span><span class="sxs-lookup"><span data-stu-id="6cf7d-123">Prepare SUSE Linux Enterprise Server 11 SP4</span></span>
1. <span data-ttu-id="6cf7d-124">Hello 選取中間窗格內的 HYPER-V 管理員，hello 虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="6cf7d-124">In hello center pane of Hyper-V Manager, select hello virtual machine.</span></span>
2. <span data-ttu-id="6cf7d-125">按一下**連接**tooopen hello 視窗 hello 虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="6cf7d-125">Click **Connect** tooopen hello window for hello virtual machine.</span></span>
3. <span data-ttu-id="6cf7d-126">註冊您的 SUSE Linux Enterprise 系統 tooallow 它 toodownload 更新及安裝套件。</span><span class="sxs-lookup"><span data-stu-id="6cf7d-126">Register your SUSE Linux Enterprise system tooallow it toodownload updates and install packages.</span></span>
4. <span data-ttu-id="6cf7d-127">更新 hello 系統 hello 最新修補程式：</span><span class="sxs-lookup"><span data-stu-id="6cf7d-127">Update hello system with hello latest patches:</span></span>
   
        # sudo zypper update
5. <span data-ttu-id="6cf7d-128">從 hello SLES 儲存機制安裝 hello Azure Linux 代理程式：</span><span class="sxs-lookup"><span data-stu-id="6cf7d-128">Install hello Azure Linux Agent from hello SLES repository:</span></span>
   
        # sudo zypper install WALinuxAgent
6. <span data-ttu-id="6cf7d-129">存回是否 「 開啟 」 太設定 waagent chkconfig，而且如果沒有，請啟用自動啟動：</span><span class="sxs-lookup"><span data-stu-id="6cf7d-129">Check if waagent is set too"on" in chkconfig, and if not, enable it for autostart:</span></span>
   
        # sudo chkconfig waagent on
7. <span data-ttu-id="6cf7d-130">檢查 waagent 服務是否正在執行，若否，請加以啟動：</span><span class="sxs-lookup"><span data-stu-id="6cf7d-130">Check if waagent service is running, and if not, start it:</span></span> 
   
        # sudo service waagent start
8. <span data-ttu-id="6cf7d-131">修改 Azure hello 核心開機行幼蟲組態 tooinclude 其他核心參數中。</span><span class="sxs-lookup"><span data-stu-id="6cf7d-131">Modify hello kernel boot line in your grub configuration tooinclude additional kernel parameters for Azure.</span></span> <span data-ttu-id="6cf7d-132">此開啟 toodo"/ boot/grub/menu.lst 「 文字編輯器中並確認該 hello 預設核心中包含下列參數的 hello:</span><span class="sxs-lookup"><span data-stu-id="6cf7d-132">toodo this open "/boot/grub/menu.lst" in a text editor and ensure that hello default kernel includes hello following parameters:</span></span>
   
        console=ttyS0 earlyprintk=ttyS0 rootdelay=300
   
    <span data-ttu-id="6cf7d-133">這可確保所有的主控台訊息都會傳送 toohello 第一個序列連接埠，這可協助 Azure 偵錯問題的支援。</span><span class="sxs-lookup"><span data-stu-id="6cf7d-133">This will ensure all console messages are sent toohello first serial port, which can assist Azure support with debugging issues.</span></span>
9. <span data-ttu-id="6cf7d-134">請確認該 /boot/grub/menu.lst 和 /etc/hosts fstab 而 hello 磁碟識別碼 (由-id) 不使用其 UUID (由-uuid) 這兩個參考 hello 磁碟。</span><span class="sxs-lookup"><span data-stu-id="6cf7d-134">Confirm that /boot/grub/menu.lst and /etc/fstab both reference hello disk using its UUID (by-uuid) instead of hello disk ID (by-id).</span></span> 
   
    <span data-ttu-id="6cf7d-135">取得磁碟 UUID</span><span class="sxs-lookup"><span data-stu-id="6cf7d-135">Get disk UUID</span></span>
   
        # ls /dev/disk/by-uuid/
   
    <span data-ttu-id="6cf7d-136">如果 /dev/disk/by-id / hello 的 uuid 的適當值，更新 /boot/grub/menu.lst 和 /etc/hosts fstab</span><span class="sxs-lookup"><span data-stu-id="6cf7d-136">If /dev/disk/by-id/ is used, update both /boot/grub/menu.lst and /etc/fstab with hello proper by-uuid value</span></span>
   
    <span data-ttu-id="6cf7d-137">變更之前</span><span class="sxs-lookup"><span data-stu-id="6cf7d-137">Before change</span></span>
   
        root=/dev/disk/by-id/SCSI-xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxxx-part1
   
    <span data-ttu-id="6cf7d-138">變更之後</span><span class="sxs-lookup"><span data-stu-id="6cf7d-138">After change</span></span>
   
        root=/dev/disk/by-uuid/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx
10. <span data-ttu-id="6cf7d-139">修改 udev 規則 tooavoid 產生 hello 乙太網路介面的靜態規則。</span><span class="sxs-lookup"><span data-stu-id="6cf7d-139">Modify udev rules tooavoid generating static rules for hello Ethernet interface(s).</span></span> <span data-ttu-id="6cf7d-140">在 Microsoft Azure 或 Hyper-V 中複製虛擬機器時，這些規則可能會造成問題：</span><span class="sxs-lookup"><span data-stu-id="6cf7d-140">These rules can cause problems when cloning a virtual machine in Microsoft Azure or Hyper-V:</span></span>
    
        # sudo ln -s /dev/null /etc/udev/rules.d/75-persistent-net-generator.rules
        # sudo rm -f /etc/udev/rules.d/70-persistent-net.rules
11. <span data-ttu-id="6cf7d-141">建議 tooedit hello 檔案"/ 等/sysconfig/網路/dhcp"，並變更 hello`DHCLIENT_SET_HOSTNAME`參數 toohello 下列：</span><span class="sxs-lookup"><span data-stu-id="6cf7d-141">It is recommended tooedit hello file "/etc/sysconfig/network/dhcp" and change hello `DHCLIENT_SET_HOSTNAME` parameter toohello following:</span></span>
    
     <span data-ttu-id="6cf7d-142">DHCLIENT_SET_HOSTNAME="no"</span><span class="sxs-lookup"><span data-stu-id="6cf7d-142">DHCLIENT_SET_HOSTNAME="no"</span></span>
12. <span data-ttu-id="6cf7d-143">在"/etc/hosts sudoers"，標記為註解或移除下列行，如果它們存在 hello:</span><span class="sxs-lookup"><span data-stu-id="6cf7d-143">In "/etc/sudoers", comment out or remove hello following lines if they exist:</span></span>
    
     <span data-ttu-id="6cf7d-144">預設值 targetpw # 詢問 hello hello 也就是根所有 ALL=(ALL) 所有的目標使用者的密碼 # 警告 ！</span><span class="sxs-lookup"><span data-stu-id="6cf7d-144">Defaults targetpw   # ask for hello password of hello target user i.e. root ALL    ALL=(ALL) ALL   # WARNING!</span></span> <span data-ttu-id="6cf7d-145">僅搭配 'Defaults targetpw'! 使用這個項目</span><span class="sxs-lookup"><span data-stu-id="6cf7d-145">Only use this together with 'Defaults targetpw'!</span></span>
13. <span data-ttu-id="6cf7d-146">請確定該 hello SSH 伺服器是在安裝並設定 toostart 開機時間。</span><span class="sxs-lookup"><span data-stu-id="6cf7d-146">Ensure that hello SSH server is installed and configured toostart at boot time.</span></span>  <span data-ttu-id="6cf7d-147">這通常是 hello 預設值。</span><span class="sxs-lookup"><span data-stu-id="6cf7d-147">This is usually hello default.</span></span>
14. <span data-ttu-id="6cf7d-148">不要在 hello OS 磁碟上建立的交換空間。</span><span class="sxs-lookup"><span data-stu-id="6cf7d-148">Do not create swap space on hello OS disk.</span></span>
    
    <span data-ttu-id="6cf7d-149">hello Azure Linux 代理程式可以自動設定使用之後附加的 toohello VM 在 Azure 上佈建的 hello 本機資源磁碟的交換空間。</span><span class="sxs-lookup"><span data-stu-id="6cf7d-149">hello Azure Linux Agent can automatically configure swap space using hello local resource disk that is attached toohello VM after provisioning on Azure.</span></span> <span data-ttu-id="6cf7d-150">請注意該 hello 本機資源磁碟是*暫存*磁碟，以及可能會在取消佈建 hello VM 時清空。</span><span class="sxs-lookup"><span data-stu-id="6cf7d-150">Note that hello local resource disk is a *temporary* disk, and might be emptied when hello VM is deprovisioned.</span></span> <span data-ttu-id="6cf7d-151">在安裝之後 hello Azure Linux 代理程式 （請參閱上一個步驟），修改適當地遵循 /etc/waagent.conf 中的參數的 hello:</span><span class="sxs-lookup"><span data-stu-id="6cf7d-151">After installing hello Azure Linux Agent (see previous step), modify hello following parameters in /etc/waagent.conf appropriately:</span></span>
    
     <span data-ttu-id="6cf7d-152">ResourceDisk.Format=y ResourceDisk.Filesystem=ext4 ResourceDisk.MountPoint=/mnt/resource ResourceDisk.EnableSwap=y ResourceDisk.SwapSizeMB=&#2048; # 注意： 設定 toobe 需要此 toowhatever。</span><span class="sxs-lookup"><span data-stu-id="6cf7d-152">ResourceDisk.Format=y  ResourceDisk.Filesystem=ext4  ResourceDisk.MountPoint=/mnt/resource  ResourceDisk.EnableSwap=y  ResourceDisk.SwapSizeMB=2048    ## NOTE: set this toowhatever you need it toobe.</span></span>
15. <span data-ttu-id="6cf7d-153">執行下列命令 toodeprovision hello 虛擬機器的 hello 並準備在 Azure 上佈建：</span><span class="sxs-lookup"><span data-stu-id="6cf7d-153">Run hello following commands toodeprovision hello virtual machine and prepare it for provisioning on Azure:</span></span>
    
    # <a name="sudo-waagent--force--deprovision"></a><span data-ttu-id="6cf7d-154">sudo waagent -force -deprovision</span><span class="sxs-lookup"><span data-stu-id="6cf7d-154">sudo waagent -force -deprovision</span></span>
    # <a name="export-histsize0"></a><span data-ttu-id="6cf7d-155">export HISTSIZE=0</span><span class="sxs-lookup"><span data-stu-id="6cf7d-155">export HISTSIZE=0</span></span>
    # <a name="logout"></a><span data-ttu-id="6cf7d-156">logout</span><span class="sxs-lookup"><span data-stu-id="6cf7d-156">logout</span></span>
16. <span data-ttu-id="6cf7d-157">在 Hyper-V 管理員中，依序按一下 [動作] -> [關閉]。</span><span class="sxs-lookup"><span data-stu-id="6cf7d-157">Click **Action -> Shut Down** in Hyper-V Manager.</span></span> <span data-ttu-id="6cf7d-158">Linux VHD 是現在準備好 toobe 上傳 tooAzure。</span><span class="sxs-lookup"><span data-stu-id="6cf7d-158">Your Linux VHD is now ready toobe uploaded tooAzure.</span></span>

- - -
## <a name="prepare-opensuse-131"></a><span data-ttu-id="6cf7d-159">準備執行 openSUSE 13.1+</span><span class="sxs-lookup"><span data-stu-id="6cf7d-159">Prepare openSUSE 13.1+</span></span>
1. <span data-ttu-id="6cf7d-160">Hello 選取中間窗格內的 HYPER-V 管理員，hello 虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="6cf7d-160">In hello center pane of Hyper-V Manager, select hello virtual machine.</span></span>
2. <span data-ttu-id="6cf7d-161">按一下**連接**tooopen hello 視窗 hello 虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="6cf7d-161">Click **Connect** tooopen hello window for hello virtual machine.</span></span>
3. <span data-ttu-id="6cf7d-162">在 hello 殼層執行 hello 命令 '`zypper lr`'。</span><span class="sxs-lookup"><span data-stu-id="6cf7d-162">On hello shell, run hello command '`zypper lr`'.</span></span> <span data-ttu-id="6cf7d-163">如果此命令會傳回，輸出類似 toohello 然後 hello 儲存機制已如預期般-沒有進行調整所需遵循 （請注意，版本號碼可能不同）：</span><span class="sxs-lookup"><span data-stu-id="6cf7d-163">If this command returns output similar toohello following, then hello repositories are configured as expected--no adjustments are necessary (note that version numbers may vary):</span></span>
   
        # | Alias                 | Name                  | Enabled | Refresh
        --+-----------------------+-----------------------+---------+--------
        1 | Cloud:Tools_13.1      | Cloud:Tools_13.1      | Yes     | Yes
        2 | openSUSE_13.1_OSS     | openSUSE_13.1_OSS     | Yes     | Yes
        3 | openSUSE_13.1_Updates | openSUSE_13.1_Updates | Yes     | Yes
   
    <span data-ttu-id="6cf7d-164">如果 hello 命令會不傳回 「...定義任何儲存機制 」 請使用下列命令 tooadd hello 這些儲存機制：</span><span class="sxs-lookup"><span data-stu-id="6cf7d-164">If hello command returns "No repositories defined..." then use hello following commands tooadd these repos:</span></span>
   
        # sudo zypper ar -f http://download.opensuse.org/repositories/Cloud:Tools/openSUSE_13.1 Cloud:Tools_13.1
        # sudo zypper ar -f http://download.opensuse.org/distribution/13.1/repo/oss openSUSE_13.1_OSS
        # sudo zypper ar -f http://download.opensuse.org/update/13.1 openSUSE_13.1_Updates
   
    <span data-ttu-id="6cf7d-165">您可以確認已執行 hello 命令加入 hello 儲存機制 '`zypper lr`' 一次。</span><span class="sxs-lookup"><span data-stu-id="6cf7d-165">You can then verify hello repositories have been added by running hello command '`zypper lr`' again.</span></span> <span data-ttu-id="6cf7d-166">萬一 hello 的相關更新儲存機制的其中一個未啟用，則會啟用使用下列命令：</span><span class="sxs-lookup"><span data-stu-id="6cf7d-166">In case one of hello relevant update repositories is not enabled, enable it with following command:</span></span>
   
        # sudo zypper mr -e [NUMBER OF REPOSITORY]
4. <span data-ttu-id="6cf7d-167">更新 hello 核心 toohello 最新可用版本：</span><span class="sxs-lookup"><span data-stu-id="6cf7d-167">Update hello kernel toohello latest available version:</span></span>
   
        # sudo zypper up kernel-default
   
    <span data-ttu-id="6cf7d-168">Tooupdate hello 具備或系統的所有 hello 最新修補程式：</span><span class="sxs-lookup"><span data-stu-id="6cf7d-168">Or tooupdate hello system with all hello latest patches:</span></span>
   
        # sudo zypper update
5. <span data-ttu-id="6cf7d-169">安裝 hello Azure Linux 代理程式。</span><span class="sxs-lookup"><span data-stu-id="6cf7d-169">Install hello Azure Linux Agent.</span></span>
   
   # <a name="sudo-zypper-install-walinuxagent"></a><span data-ttu-id="6cf7d-170">sudo zypper install WALinuxAgent</span><span class="sxs-lookup"><span data-stu-id="6cf7d-170">sudo zypper install WALinuxAgent</span></span>
6. <span data-ttu-id="6cf7d-171">修改 Azure hello 核心開機行幼蟲組態 tooinclude 其他核心參數中。</span><span class="sxs-lookup"><span data-stu-id="6cf7d-171">Modify hello kernel boot line in your grub configuration tooinclude additional kernel parameters for Azure.</span></span> <span data-ttu-id="6cf7d-172">toodo，開啟 「 / boot/grub/menu.lst 「 文字編輯器中，並確保該 hello 預設核心包含下列參數的 hello:</span><span class="sxs-lookup"><span data-stu-id="6cf7d-172">toodo this, open "/boot/grub/menu.lst" in a text editor and ensure that hello default kernel includes hello following parameters:</span></span>
   
     <span data-ttu-id="6cf7d-173">console=ttyS0 earlyprintk=ttyS0 rootdelay=300</span><span class="sxs-lookup"><span data-stu-id="6cf7d-173">console=ttyS0 earlyprintk=ttyS0 rootdelay=300</span></span>
   
   <span data-ttu-id="6cf7d-174">這可確保所有的主控台訊息都會傳送 toohello 第一個序列連接埠，這可協助 Azure 偵錯問題的支援。</span><span class="sxs-lookup"><span data-stu-id="6cf7d-174">This will ensure all console messages are sent toohello first serial port, which can assist Azure support with debugging issues.</span></span> <span data-ttu-id="6cf7d-175">此外，移除 hello hello 核心開機行中的下列參數，如果它們存在：</span><span class="sxs-lookup"><span data-stu-id="6cf7d-175">In addition, remove hello following parameters from hello kernel boot line if they exist:</span></span>
   
     <span data-ttu-id="6cf7d-176">libata.atapi_enabled=0 reserve=0x1f0,0x8</span><span class="sxs-lookup"><span data-stu-id="6cf7d-176">libata.atapi_enabled=0 reserve=0x1f0,0x8</span></span>
7. <span data-ttu-id="6cf7d-177">建議 tooedit hello 檔案"/ 等/sysconfig/網路/dhcp"，並變更 hello`DHCLIENT_SET_HOSTNAME`參數 toohello 下列：</span><span class="sxs-lookup"><span data-stu-id="6cf7d-177">It is recommended tooedit hello file "/etc/sysconfig/network/dhcp" and change hello `DHCLIENT_SET_HOSTNAME` parameter toohello following:</span></span>
   
     <span data-ttu-id="6cf7d-178">DHCLIENT_SET_HOSTNAME="no"</span><span class="sxs-lookup"><span data-stu-id="6cf7d-178">DHCLIENT_SET_HOSTNAME="no"</span></span>
8. <span data-ttu-id="6cf7d-179">**重要事項：** "/etc/hosts sudoers 」，在標記為註解或移除下列行，如果它們存在 hello:</span><span class="sxs-lookup"><span data-stu-id="6cf7d-179">**Important:** In "/etc/sudoers", comment out or remove hello following lines if they exist:</span></span>
   
     <span data-ttu-id="6cf7d-180">預設值 targetpw # 詢問 hello hello 也就是根所有 ALL=(ALL) 所有的目標使用者的密碼 # 警告 ！</span><span class="sxs-lookup"><span data-stu-id="6cf7d-180">Defaults targetpw   # ask for hello password of hello target user i.e. root ALL    ALL=(ALL) ALL   # WARNING!</span></span> <span data-ttu-id="6cf7d-181">僅搭配 'Defaults targetpw'! 使用這個項目</span><span class="sxs-lookup"><span data-stu-id="6cf7d-181">Only use this together with 'Defaults targetpw'!</span></span>
9. <span data-ttu-id="6cf7d-182">請確定該 hello SSH 伺服器是在安裝並設定 toostart 開機時間。</span><span class="sxs-lookup"><span data-stu-id="6cf7d-182">Ensure that hello SSH server is installed and configured toostart at boot time.</span></span>  <span data-ttu-id="6cf7d-183">這通常是 hello 預設值。</span><span class="sxs-lookup"><span data-stu-id="6cf7d-183">This is usually hello default.</span></span>
10. <span data-ttu-id="6cf7d-184">不要在 hello OS 磁碟上建立的交換空間。</span><span class="sxs-lookup"><span data-stu-id="6cf7d-184">Do not create swap space on hello OS disk.</span></span>
    
    <span data-ttu-id="6cf7d-185">hello Azure Linux 代理程式可以自動設定使用之後附加的 toohello VM 在 Azure 上佈建的 hello 本機資源磁碟的交換空間。</span><span class="sxs-lookup"><span data-stu-id="6cf7d-185">hello Azure Linux Agent can automatically configure swap space using hello local resource disk that is attached toohello VM after provisioning on Azure.</span></span> <span data-ttu-id="6cf7d-186">請注意該 hello 本機資源磁碟是*暫存*磁碟，以及可能會在取消佈建 hello VM 時清空。</span><span class="sxs-lookup"><span data-stu-id="6cf7d-186">Note that hello local resource disk is a *temporary* disk, and might be emptied when hello VM is deprovisioned.</span></span> <span data-ttu-id="6cf7d-187">在安裝之後 hello Azure Linux 代理程式 （請參閱上一個步驟），修改適當地遵循 /etc/waagent.conf 中的參數的 hello:</span><span class="sxs-lookup"><span data-stu-id="6cf7d-187">After installing hello Azure Linux Agent (see previous step), modify hello following parameters in /etc/waagent.conf appropriately:</span></span>
    
     <span data-ttu-id="6cf7d-188">ResourceDisk.Format=y ResourceDisk.Filesystem=ext4 ResourceDisk.MountPoint=/mnt/resource ResourceDisk.EnableSwap=y ResourceDisk.SwapSizeMB=&#2048; # 注意： 設定 toobe 需要此 toowhatever。</span><span class="sxs-lookup"><span data-stu-id="6cf7d-188">ResourceDisk.Format=y  ResourceDisk.Filesystem=ext4  ResourceDisk.MountPoint=/mnt/resource  ResourceDisk.EnableSwap=y  ResourceDisk.SwapSizeMB=2048    ## NOTE: set this toowhatever you need it toobe.</span></span>
11. <span data-ttu-id="6cf7d-189">執行下列命令 toodeprovision hello 虛擬機器的 hello 並準備在 Azure 上佈建：</span><span class="sxs-lookup"><span data-stu-id="6cf7d-189">Run hello following commands toodeprovision hello virtual machine and prepare it for provisioning on Azure:</span></span>
    
    # <a name="sudo-waagent--force--deprovision"></a><span data-ttu-id="6cf7d-190">sudo waagent -force -deprovision</span><span class="sxs-lookup"><span data-stu-id="6cf7d-190">sudo waagent -force -deprovision</span></span>
    # <a name="export-histsize0"></a><span data-ttu-id="6cf7d-191">export HISTSIZE=0</span><span class="sxs-lookup"><span data-stu-id="6cf7d-191">export HISTSIZE=0</span></span>
    # <a name="logout"></a><span data-ttu-id="6cf7d-192">logout</span><span class="sxs-lookup"><span data-stu-id="6cf7d-192">logout</span></span>
12. <span data-ttu-id="6cf7d-193">請確定在啟動時執行 Azure Linux 代理程式的 hello:</span><span class="sxs-lookup"><span data-stu-id="6cf7d-193">Ensure hello Azure Linux Agent runs at startup:</span></span>
    
        # sudo systemctl enable waagent.service
13. <span data-ttu-id="6cf7d-194">在 Hyper-V 管理員中，依序按一下 [動作] -> [關閉]。</span><span class="sxs-lookup"><span data-stu-id="6cf7d-194">Click **Action -> Shut Down** in Hyper-V Manager.</span></span> <span data-ttu-id="6cf7d-195">Linux VHD 是現在準備好 toobe 上傳 tooAzure。</span><span class="sxs-lookup"><span data-stu-id="6cf7d-195">Your Linux VHD is now ready toobe uploaded tooAzure.</span></span>

## <a name="next-steps"></a><span data-ttu-id="6cf7d-196">後續步驟</span><span class="sxs-lookup"><span data-stu-id="6cf7d-196">Next steps</span></span>
<span data-ttu-id="6cf7d-197">您要現在準備好 toouse SUSE Linux 虛擬硬碟 toocreate 新虛擬機器在 Azure 中。</span><span class="sxs-lookup"><span data-stu-id="6cf7d-197">You're now ready toouse your SUSE Linux virtual hard disk toocreate new virtual machines in Azure.</span></span> <span data-ttu-id="6cf7d-198">如果這是 hello 正在上傳 hello.vhd 檔案 tooAzure 的第一次，請參閱步驟 2 和 3 中的[建立和上傳包含 hello Linux 作業系統的虛擬硬碟](classic/create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="6cf7d-198">If this is hello first time that you're uploading hello .vhd file tooAzure, see steps 2 and 3 in [Creating and uploading a virtual hard disk that contains hello Linux operating system](classic/create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).</span></span>
