---
title: "aaaCreate 和上傳 CentOS 基礎 Linux VHD 在 Azure 中"
description: "了解 toocreate 和上傳 Azure 虛擬硬碟 (VHD)，其中包含 CentOS 為基礎的 Linux 作業系統。"
services: virtual-machines-linux
documentationcenter: 
author: szarkos
manager: timlt
editor: tysonn
tags: azure-resource-manager,azure-service-management
ms.assetid: 0e518e92-e981-43f4-b12c-9cba1064c4bb
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 02/02/2017
ms.author: szark
ms.openlocfilehash: 78f36be1d36e3d44cb836c912d143f2c9a72aab5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="prepare-a-centos-based-virtual-machine-for-azure"></a><span data-ttu-id="2bc56-103">準備適用於 Azure 的 CentOS 型虛擬機器</span><span class="sxs-lookup"><span data-stu-id="2bc56-103">Prepare a CentOS-based virtual machine for Azure</span></span>
* [<span data-ttu-id="2bc56-104">準備適用於 Azure 的 CentOS 6.x 虛擬機器</span><span class="sxs-lookup"><span data-stu-id="2bc56-104">Prepare a CentOS 6.x virtual machine for Azure</span></span>](#centos-6x)
* [<span data-ttu-id="2bc56-105">準備適用於 Azure 的 CentOS 7.0+ 虛擬機器</span><span class="sxs-lookup"><span data-stu-id="2bc56-105">Prepare a CentOS 7.0+ virtual machine for Azure</span></span>](#centos-70)

[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-both-include.md)]

## <a name="prerequisites"></a><span data-ttu-id="2bc56-106">必要條件</span><span class="sxs-lookup"><span data-stu-id="2bc56-106">Prerequisites</span></span>
<span data-ttu-id="2bc56-107">本文假設您已安裝 CentOS （或類似的衍生項目） Linux 作業系統 tooa 虛擬硬碟。</span><span class="sxs-lookup"><span data-stu-id="2bc56-107">This article assumes that you have already installed a CentOS (or similar derivative) Linux operating system tooa virtual hard disk.</span></span> <span data-ttu-id="2bc56-108">多個工具存在 toocreate.vhd 檔案，例如 HYPER-V 之類的虛擬化解決方案。</span><span class="sxs-lookup"><span data-stu-id="2bc56-108">Multiple tools exist toocreate .vhd files, for example a virtualization solution such as Hyper-V.</span></span> <span data-ttu-id="2bc56-109">如需指示，請參閱[安裝 hello HYPER-V 角色和設定虛擬機器](http://technet.microsoft.com/library/hh846766.aspx)。</span><span class="sxs-lookup"><span data-stu-id="2bc56-109">For instructions, see [Install hello Hyper-V Role and Configure a Virtual Machine](http://technet.microsoft.com/library/hh846766.aspx).</span></span>

<span data-ttu-id="2bc56-110">**CentOS 安裝注意事項**</span><span class="sxs-lookup"><span data-stu-id="2bc56-110">**CentOS installation notes**</span></span>

* <span data-ttu-id="2bc56-111">另請參閱[一般 Linux 安裝注意事項](create-upload-generic.md#general-linux-installation-notes)，了解為 Azure 準備 Linux 的更多祕訣。</span><span class="sxs-lookup"><span data-stu-id="2bc56-111">Please see also [General Linux Installation Notes](create-upload-generic.md#general-linux-installation-notes) for more tips on preparing Linux for Azure.</span></span>
* <span data-ttu-id="2bc56-112">hello VHDX 格式不支援在 Azure 中，只有**固定 VHD**。</span><span class="sxs-lookup"><span data-stu-id="2bc56-112">hello VHDX format is not supported in Azure, only **fixed VHD**.</span></span>  <span data-ttu-id="2bc56-113">您可以將使用 HYPER-V 管理員 hello 磁碟 tooVHD 格式轉換或 hello convert-vhd 指令程式。</span><span class="sxs-lookup"><span data-stu-id="2bc56-113">You can convert hello disk tooVHD format using Hyper-V Manager or hello convert-vhd cmdlet.</span></span> <span data-ttu-id="2bc56-114">如果您使用 VirtualBox 這表示選取**固定大小**為相對於 toohello 預設建立 hello 磁碟時，動態配置。</span><span class="sxs-lookup"><span data-stu-id="2bc56-114">If you are using VirtualBox this means selecting **Fixed size** as opposed toohello default dynamically allocated when creating hello disk.</span></span>
* <span data-ttu-id="2bc56-115">安裝 hello Linux 系統時*建議*您使用標準的資料分割，而非 LVM （通常 hello 預設值為許多安裝）。</span><span class="sxs-lookup"><span data-stu-id="2bc56-115">When installing hello Linux system it is *recommended* that you use standard partitions rather than LVM (often hello default for many installations).</span></span> <span data-ttu-id="2bc56-116">這樣可避免與複製 Vm，LVM 名稱衝突，特別是當作業系統磁碟需要附加 toobe tooanother 相同的 VM 進行疑難排解。</span><span class="sxs-lookup"><span data-stu-id="2bc56-116">This will avoid LVM name conflicts with cloned VMs, particularly if an OS disk ever needs toobe attached tooanother identical VM for troubleshooting.</span></span> <span data-ttu-id="2bc56-117">如果願意，您可以在資料磁碟上使用 [LVM](configure-raid.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) 或 [RAID](configure-lvm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="2bc56-117">[LVM](configure-lvm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) or [RAID](configure-raid.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) may be used on data disks.</span></span>
* <span data-ttu-id="2bc56-118">需要掛接 UDF 檔案系統的核心支援。</span><span class="sxs-lookup"><span data-stu-id="2bc56-118">Kernel support for mounting UDF file systems is required.</span></span> <span data-ttu-id="2bc56-119">在第一次開機 Azure hello 上佈建組態會透過附加的 toohello 客體的 UDF 格式化媒體傳遞 toohello Linux VM。</span><span class="sxs-lookup"><span data-stu-id="2bc56-119">At first boot on Azure hello provisioning configuration is passed toohello Linux VM via UDF-formatted media that is attached toohello guest.</span></span> <span data-ttu-id="2bc56-120">hello Azure Linux 代理程式必須要能夠 toomount hello UDF 檔案系統 tooread 其組態，並佈建 hello VM。</span><span class="sxs-lookup"><span data-stu-id="2bc56-120">hello Azure Linux agent must be able toomount hello UDF file system tooread its configuration and provision hello VM.</span></span>
* <span data-ttu-id="2bc56-121">Linux Kernel 2.6.37 以下的版本不支援較大 VM 大小 Hyper-V 上的NUMA。</span><span class="sxs-lookup"><span data-stu-id="2bc56-121">Linux kernel versions below 2.6.37 do not support NUMA on Hyper-V with larger VM sizes.</span></span> <span data-ttu-id="2bc56-122">這個問題主要會影響較舊的分佈上游使用 hello Red Hat 2.6.32 核心及已修正 RHEL 6.6 (核心-2.6.32-504) 中。</span><span class="sxs-lookup"><span data-stu-id="2bc56-122">This issue primarily impacts older distributions using hello upstream Red Hat 2.6.32 kernel, and was fixed in RHEL 6.6 (kernel-2.6.32-504).</span></span> <span data-ttu-id="2bc56-123">執行自訂的核心超過 2.6.37 或較舊 RHEL 基礎核心非 2.6.32-504 必須設定系統 hello 開機參數`numa=off`hello 核心 grub.conf 在命令列上。</span><span class="sxs-lookup"><span data-stu-id="2bc56-123">Systems running custom kernels older than 2.6.37, or RHEL-based kernels older than 2.6.32-504 must set hello boot parameter `numa=off` on hello kernel command-line in grub.conf.</span></span> <span data-ttu-id="2bc56-124">如需詳細資訊，請參閱 Red Hat [KB 436883](https://access.redhat.com/solutions/436883)。</span><span class="sxs-lookup"><span data-stu-id="2bc56-124">For more information see Red Hat [KB 436883](https://access.redhat.com/solutions/436883).</span></span>
* <span data-ttu-id="2bc56-125">請勿設定 hello OS 磁碟交換資料分割。</span><span class="sxs-lookup"><span data-stu-id="2bc56-125">Do not configure a swap partition on hello OS disk.</span></span> <span data-ttu-id="2bc56-126">hello Linux 代理程式可以設定的 toocreate 交換磁碟上的檔案 hello 暫存資源。</span><span class="sxs-lookup"><span data-stu-id="2bc56-126">hello Linux agent can be configured toocreate a swap file on hello temporary resource disk.</span></span>  <span data-ttu-id="2bc56-127">相關資訊位於下列 hello 步驟。</span><span class="sxs-lookup"><span data-stu-id="2bc56-127">More information about this can be found in hello steps below.</span></span>
* <span data-ttu-id="2bc56-128">所有 hello Vhd 必須是 1 MB 的倍數的大小。</span><span class="sxs-lookup"><span data-stu-id="2bc56-128">All of hello VHDs must have sizes that are multiples of 1 MB.</span></span>

## <a name="centos-6x"></a><span data-ttu-id="2bc56-129">CentOS 6.x</span><span class="sxs-lookup"><span data-stu-id="2bc56-129">CentOS 6.x</span></span>

1. <span data-ttu-id="2bc56-130">在 HYPER-V 管理員 中，選取 hello 虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="2bc56-130">In Hyper-V Manager, select hello virtual machine.</span></span>

2. <span data-ttu-id="2bc56-131">按一下**連接**tooopen hello 虛擬機器的主控台視窗。</span><span class="sxs-lookup"><span data-stu-id="2bc56-131">Click **Connect** tooopen a console window for hello virtual machine.</span></span>

3. <span data-ttu-id="2bc56-132">CentOS 6 NetworkManager 可能會干擾 hello Azure Linux 代理程式。</span><span class="sxs-lookup"><span data-stu-id="2bc56-132">In CentOS 6, NetworkManager can interfere with hello Azure Linux agent.</span></span> <span data-ttu-id="2bc56-133">解除安裝此套件，藉由執行下列命令的 hello:</span><span class="sxs-lookup"><span data-stu-id="2bc56-133">Uninstall this package by running hello following command:</span></span>
   
        # sudo rpm -e --nodeps NetworkManager

4. <span data-ttu-id="2bc56-134">建立或編輯 hello 檔案`/etc/sysconfig/network`並加入下列文字的 hello:</span><span class="sxs-lookup"><span data-stu-id="2bc56-134">Create or edit hello file `/etc/sysconfig/network` and add hello following text:</span></span>
   
        NETWORKING=yes
        HOSTNAME=localhost.localdomain

5. <span data-ttu-id="2bc56-135">建立或編輯 hello 檔案`/etc/sysconfig/network-scripts/ifcfg-eth0`並加入下列文字的 hello:</span><span class="sxs-lookup"><span data-stu-id="2bc56-135">Create or edit hello file `/etc/sysconfig/network-scripts/ifcfg-eth0` and add hello following text:</span></span>
   
        DEVICE=eth0
        ONBOOT=yes
        BOOTPROTO=dhcp
        TYPE=Ethernet
        USERCTL=no
        PEERDNS=yes
        IPV6INIT=no

6. <span data-ttu-id="2bc56-136">修改 udev 規則 tooavoid 產生 hello 乙太網路介面的靜態規則。</span><span class="sxs-lookup"><span data-stu-id="2bc56-136">Modify udev rules tooavoid generating static rules for hello Ethernet interface(s).</span></span> <span data-ttu-id="2bc56-137">在 Microsoft Azure 或 Hyper-V 中複製虛擬機器時，這些規則可能會造成問題：</span><span class="sxs-lookup"><span data-stu-id="2bc56-137">These rules can cause problems when cloning a virtual machine in Microsoft Azure or Hyper-V:</span></span>
   
        # sudo ln -s /dev/null /etc/udev/rules.d/75-persistent-net-generator.rules
        # sudo rm -f /etc/udev/rules.d/70-persistent-net.rules

7. <span data-ttu-id="2bc56-138">請確定 hello 網路服務將會在開機時啟動藉由執行下列命令的 hello:</span><span class="sxs-lookup"><span data-stu-id="2bc56-138">Ensure hello network service will start at boot time by running hello following command:</span></span>
   
        # sudo chkconfig network on

8. <span data-ttu-id="2bc56-139">如果您想要 toouse hello OpenLogic 鏡像 hello Azure 資料中心內裝載，然後取代 hello`/etc/yum.repos.d/CentOS-Base.repo`以 hello 下列儲存機制的檔案。</span><span class="sxs-lookup"><span data-stu-id="2bc56-139">If you would like toouse hello OpenLogic mirrors that are hosted within hello Azure datacenters, then replace hello `/etc/yum.repos.d/CentOS-Base.repo` file with hello following repositories.</span></span>  <span data-ttu-id="2bc56-140">這也會加入 hello **[openlogic]**包含例如 hello Azure Linux 代理程式的其他封裝的儲存機制：</span><span class="sxs-lookup"><span data-stu-id="2bc56-140">This will also add hello **[openlogic]** repository that includes additional packages such as hello Azure Linux agent:</span></span>

        [openlogic]
        name=CentOS-$releasever - openlogic packages for $basearch
        baseurl=http://olcentgbl.trafficmanager.net/openlogic/$releasever/openlogic/$basearch/
        enabled=1
        gpgcheck=0
        
        [base]
        name=CentOS-$releasever - Base
        #mirrorlist=http://mirrorlist.centos.org/?release=$releasever&arch=$basearch&repo=os&infra=$infra
        baseurl=http://olcentgbl.trafficmanager.net/centos/$releasever/os/$basearch/
        gpgcheck=1
        gpgkey=file:///etc/pki/rpm-gpg/RPM-GPG-KEY-CentOS-6
        
        #released updates
        [updates]
        name=CentOS-$releasever - Updates
        #mirrorlist=http://mirrorlist.centos.org/?release=$releasever&arch=$basearch&repo=updates&infra=$infra
        baseurl=http://olcentgbl.trafficmanager.net/centos/$releasever/updates/$basearch/
        gpgcheck=1
        gpgkey=file:///etc/pki/rpm-gpg/RPM-GPG-KEY-CentOS-6
        
        #additional packages that may be useful
        [extras]
        name=CentOS-$releasever - Extras
        #mirrorlist=http://mirrorlist.centos.org/?release=$releasever&arch=$basearch&repo=extras&infra=$infra
        baseurl=http://olcentgbl.trafficmanager.net/centos/$releasever/extras/$basearch/
        gpgcheck=1
        gpgkey=file:///etc/pki/rpm-gpg/RPM-GPG-KEY-CentOS-6

        #additional packages that extend functionality of existing packages
        [centosplus]
        name=CentOS-$releasever - Plus
        #mirrorlist=http://mirrorlist.centos.org/?release=$releasever&arch=$basearch&repo=centosplus&infra=$infra
        baseurl=http://olcentgbl.trafficmanager.net/centos/$releasever/centosplus/$basearch/
        gpgcheck=1
        enabled=0
        gpgkey=file:///etc/pki/rpm-gpg/RPM-GPG-KEY-CentOS-6
        
        #contrib - packages by Centos Users
        [contrib]
        name=CentOS-$releasever - Contrib
        #mirrorlist=http://mirrorlist.centos.org/?release=$releasever&arch=$basearch&repo=contrib&infra=$infra
        baseurl=http://olcentgbl.trafficmanager.net/centos/$releasever/contrib/$basearch/
        gpgcheck=1
        enabled=0
        gpgkey=file:///etc/pki/rpm-gpg/RPM-GPG-KEY-CentOS-6

    >[!Note]
    <span data-ttu-id="2bc56-141">hello 本指南的其餘部分將假設您使用至少 hello`[openlogic]`儲存機制，將會使用的 tooinstall hello Azure Linux 代理程式下方。</span><span class="sxs-lookup"><span data-stu-id="2bc56-141">hello rest of this guide will assume you are using at least hello `[openlogic]` repo, which will be used tooinstall hello Azure Linux agent below.</span></span>


9. <span data-ttu-id="2bc56-142">加入下列行 too/etc/yum.conf hello:</span><span class="sxs-lookup"><span data-stu-id="2bc56-142">Add hello following line too/etc/yum.conf:</span></span>
    
        http_caching=packages

10. <span data-ttu-id="2bc56-143">執行下列命令 tooclear hello 目前 yum 中繼資料和更新 hello 系統與 hello 最新的套件 hello:</span><span class="sxs-lookup"><span data-stu-id="2bc56-143">Run hello following command tooclear hello current yum metadata and update hello system with hello latest packages:</span></span>
    
        # yum clean all

    <span data-ttu-id="2bc56-144">除非您要建立較舊版本的 CentOS 的映像，我們建議所有 hello 的 tooupdate 封裝 toohello 最新版本：</span><span class="sxs-lookup"><span data-stu-id="2bc56-144">Unless you are creating an image for an older version of CentOS, it is recommended tooupdate all hello packages toohello latest:</span></span>

        # sudo yum -y update

    <span data-ttu-id="2bc56-145">執行此命令之後可能需要重新開機。</span><span class="sxs-lookup"><span data-stu-id="2bc56-145">A reboot may be required after running this command.</span></span>

11. <span data-ttu-id="2bc56-146">（選擇性）安裝 hello hello Linux Integration Services (LIS) 的驅動程式。</span><span class="sxs-lookup"><span data-stu-id="2bc56-146">(Optional) Install hello drivers for hello Linux Integration Services (LIS).</span></span>
   
    >[!IMPORTANT]
    <span data-ttu-id="2bc56-147">hello 步驟是**必要**CentOS 6.3 和更早版本，及更新版本的選擇性的。</span><span class="sxs-lookup"><span data-stu-id="2bc56-147">hello step is **required** for CentOS 6.3 and earlier, and optional for later releases.</span></span>

        # sudo rpm -e hypervkvpd  ## (may return error if not installed, that's OK)
        # sudo yum install microsoft-hyper-v

    <span data-ttu-id="2bc56-148">或者，您可以依照 hello 手動安裝指示，在 hello [LIS 下載頁面](https://go.microsoft.com/fwlink/?linkid=403033)tooinstall hello RPM 到您的 VM。</span><span class="sxs-lookup"><span data-stu-id="2bc56-148">Alternatively, you can follow hello manual installation instructions on hello [LIS download page](https://go.microsoft.com/fwlink/?linkid=403033) tooinstall hello RPM onto your VM.</span></span>
 
12. <span data-ttu-id="2bc56-149">安裝 hello Azure Linux 代理程式和相依性：</span><span class="sxs-lookup"><span data-stu-id="2bc56-149">Install hello Azure Linux Agent and dependencies:</span></span>
    
        # sudo yum install python-pyasn1 WALinuxAgent
    
    <span data-ttu-id="2bc56-150">如果沒有已移除步驟 3 中所述，hello NetworkManager 和 NetworkManager gnome 封裝將會移除 hello WALinuxAgent 封裝。</span><span class="sxs-lookup"><span data-stu-id="2bc56-150">hello WALinuxAgent package will remove hello NetworkManager and NetworkManager-gnome packages if they were not already removed as described in step 3.</span></span>


13. <span data-ttu-id="2bc56-151">修改 Azure hello 核心開機行幼蟲組態 tooinclude 其他核心參數中。</span><span class="sxs-lookup"><span data-stu-id="2bc56-151">Modify hello kernel boot line in your grub configuration tooinclude additional kernel parameters for Azure.</span></span> <span data-ttu-id="2bc56-152">toodo，開啟`/boot/grub/menu.lst`文字編輯器中，並確保該 hello 預設核心包含下列參數的 hello:</span><span class="sxs-lookup"><span data-stu-id="2bc56-152">toodo this, open `/boot/grub/menu.lst` in a text editor and ensure that hello default kernel includes hello following parameters:</span></span>
    
        console=ttyS0 earlyprintk=ttyS0 rootdelay=300
    
    <span data-ttu-id="2bc56-153">這也可確保所有的主控台訊息都會傳送 toohello 第一個序列連接埠，這可協助 Azure 偵錯問題的支援。</span><span class="sxs-lookup"><span data-stu-id="2bc56-153">This will also ensure all console messages are sent toohello first serial port, which can assist Azure support with debugging issues.</span></span>
    
    <span data-ttu-id="2bc56-154">除了上述 toohello 建議太*移除*hello 下列參數：</span><span class="sxs-lookup"><span data-stu-id="2bc56-154">In addition toohello above, it is recommended too*remove* hello following parameters:</span></span>
    
        rhgb quiet crashkernel=auto
    
    <span data-ttu-id="2bc56-155">沒有適用於雲端環境，我們想要傳送 toohello 序列連接埠的所有 hello 記錄 toobe 圖形和無訊息的開機。</span><span class="sxs-lookup"><span data-stu-id="2bc56-155">Graphical and quiet boot are not useful in a cloud environment where we want all hello logs toobe sent toohello serial port.</span></span>  <span data-ttu-id="2bc56-156">hello`crashkernel`選項可能會是左設定如有需要，但請注意，這個參數會減少 hello hello 128 MB 以上，VM 中可用的記憶體數量可能會造成問題 hello 較小的 VM 大小。</span><span class="sxs-lookup"><span data-stu-id="2bc56-156">hello `crashkernel` option may be left configured if desired, but note that this parameter will reduce hello amount of available memory in hello VM by 128MB or more, which may be problematic on hello smaller VM sizes.</span></span>

    >[!Important]
    <span data-ttu-id="2bc56-157">CentOS 6.5 及更早版本也必須設定 hello 核心參數`numa=off`。</span><span class="sxs-lookup"><span data-stu-id="2bc56-157">CentOS 6.5 and earlier must also set hello kernel parameter `numa=off`.</span></span> <span data-ttu-id="2bc56-158">請參閱 Red Hat [KB 436883](https://access.redhat.com/solutions/436883)。</span><span class="sxs-lookup"><span data-stu-id="2bc56-158">See Red Hat [KB 436883](https://access.redhat.com/solutions/436883).</span></span>

14. <span data-ttu-id="2bc56-159">請確定該 hello SSH 伺服器是在安裝並設定 toostart 開機時間。</span><span class="sxs-lookup"><span data-stu-id="2bc56-159">Ensure that hello SSH server is installed and configured toostart at boot time.</span></span>  <span data-ttu-id="2bc56-160">這通常是 hello 預設值。</span><span class="sxs-lookup"><span data-stu-id="2bc56-160">This is usually hello default.</span></span>

15. <span data-ttu-id="2bc56-161">不要在 hello OS 磁碟上建立的交換空間。</span><span class="sxs-lookup"><span data-stu-id="2bc56-161">Do not create swap space on hello OS disk.</span></span>
    
    <span data-ttu-id="2bc56-162">hello Azure Linux 代理程式可以自動設定使用之後附加的 toohello VM 在 Azure 上佈建的 hello 本機資源磁碟的交換空間。</span><span class="sxs-lookup"><span data-stu-id="2bc56-162">hello Azure Linux Agent can automatically configure swap space using hello local resource disk that is attached toohello VM after provisioning on Azure.</span></span> <span data-ttu-id="2bc56-163">請注意該 hello 本機資源磁碟是*暫存*磁碟，以及可能會在取消佈建 hello VM 時清空。</span><span class="sxs-lookup"><span data-stu-id="2bc56-163">Note that hello local resource disk is a *temporary* disk, and might be emptied when hello VM is deprovisioned.</span></span> <span data-ttu-id="2bc56-164">在安裝之後 hello Azure Linux 代理程式 （請參閱上一個步驟），修改下列參數中的 hello`/etc/waagent.conf`適當地：</span><span class="sxs-lookup"><span data-stu-id="2bc56-164">After installing hello Azure Linux Agent (see previous step), modify hello following parameters in `/etc/waagent.conf` appropriately:</span></span>
    
        ResourceDisk.Format=y
        ResourceDisk.Filesystem=ext4
        ResourceDisk.MountPoint=/mnt/resource
        ResourceDisk.EnableSwap=y
        ResourceDisk.SwapSizeMB=2048    ## NOTE: set this toowhatever you need it toobe.

16. <span data-ttu-id="2bc56-165">執行下列命令 toodeprovision hello 虛擬機器的 hello 並準備在 Azure 上佈建：</span><span class="sxs-lookup"><span data-stu-id="2bc56-165">Run hello following commands toodeprovision hello virtual machine and prepare it for provisioning on Azure:</span></span>
    
        # sudo waagent -force -deprovision
        # export HISTSIZE=0
        # logout

17. <span data-ttu-id="2bc56-166">在 Hyper-V 管理員中，依序按一下 [動作] -> [關閉]。</span><span class="sxs-lookup"><span data-stu-id="2bc56-166">Click **Action -> Shut Down** in Hyper-V Manager.</span></span> <span data-ttu-id="2bc56-167">Linux VHD 是現在準備好 toobe 上傳 tooAzure。</span><span class="sxs-lookup"><span data-stu-id="2bc56-167">Your Linux VHD is now ready toobe uploaded tooAzure.</span></span>


- - -
## <a name="centos-70"></a><span data-ttu-id="2bc56-168">CentOS 7.0+</span><span class="sxs-lookup"><span data-stu-id="2bc56-168">CentOS 7.0+</span></span>
<span data-ttu-id="2bc56-169">**CentOS 7 (和類似的衍生項目) 中的變更**</span><span class="sxs-lookup"><span data-stu-id="2bc56-169">**Changes in CentOS 7 (and similar derivatives)**</span></span>

<span data-ttu-id="2bc56-170">準備 Azure CentOS 7 虛擬機器是非常類似 tooCentOS 6，不過，有數個值得注意的重要差異：</span><span class="sxs-lookup"><span data-stu-id="2bc56-170">Preparing a CentOS 7 virtual machine for Azure is very similar tooCentOS 6, however there are several important differences worth noting:</span></span>

* <span data-ttu-id="2bc56-171">hello NetworkManager 封裝不會再與 hello Azure Linux 代理程式發生衝突。</span><span class="sxs-lookup"><span data-stu-id="2bc56-171">hello NetworkManager package no longer conflicts with hello Azure Linux agent.</span></span> <span data-ttu-id="2bc56-172">依預設會安裝此封裝，建議您不要將它移除。</span><span class="sxs-lookup"><span data-stu-id="2bc56-172">This package is installed by default and we recommend that it is not removed.</span></span>
* <span data-ttu-id="2bc56-173">GRUB2 現在用做 hello 預設開機載入器，因此編輯核心參數 hello 程序已變更 （請參閱下方）。</span><span class="sxs-lookup"><span data-stu-id="2bc56-173">GRUB2 is now used as hello default bootloader, so hello procedure for editing kernel parameters has changed (see below).</span></span>
* <span data-ttu-id="2bc56-174">XFS 現在是 hello 預設檔案系統。</span><span class="sxs-lookup"><span data-stu-id="2bc56-174">XFS is now hello default file system.</span></span> <span data-ttu-id="2bc56-175">如有需要，仍可以使用 hello ext4 檔案系統。</span><span class="sxs-lookup"><span data-stu-id="2bc56-175">hello ext4 file system can still be used if desired.</span></span>

<span data-ttu-id="2bc56-176">**組態步驟**</span><span class="sxs-lookup"><span data-stu-id="2bc56-176">**Configuration Steps**</span></span>

1. <span data-ttu-id="2bc56-177">在 HYPER-V 管理員 中，選取 hello 虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="2bc56-177">In Hyper-V Manager, select hello virtual machine.</span></span>

2. <span data-ttu-id="2bc56-178">按一下**連接**tooopen hello 虛擬機器的主控台視窗。</span><span class="sxs-lookup"><span data-stu-id="2bc56-178">Click **Connect** tooopen a console window for hello virtual machine.</span></span>

3. <span data-ttu-id="2bc56-179">建立或編輯 hello 檔案`/etc/sysconfig/network`並加入下列文字的 hello:</span><span class="sxs-lookup"><span data-stu-id="2bc56-179">Create or edit hello file `/etc/sysconfig/network` and add hello following text:</span></span>
   
        NETWORKING=yes
        HOSTNAME=localhost.localdomain

4. <span data-ttu-id="2bc56-180">建立或編輯 hello 檔案`/etc/sysconfig/network-scripts/ifcfg-eth0`並加入下列文字的 hello:</span><span class="sxs-lookup"><span data-stu-id="2bc56-180">Create or edit hello file `/etc/sysconfig/network-scripts/ifcfg-eth0` and add hello following text:</span></span>
   
        DEVICE=eth0
        ONBOOT=yes
        BOOTPROTO=dhcp
        TYPE=Ethernet
        USERCTL=no
        PEERDNS=yes
        IPV6INIT=no
        NM_CONTROLLED=no

5. <span data-ttu-id="2bc56-181">修改 udev 規則 tooavoid 產生 hello 乙太網路介面的靜態規則。</span><span class="sxs-lookup"><span data-stu-id="2bc56-181">Modify udev rules tooavoid generating static rules for hello Ethernet interface(s).</span></span> <span data-ttu-id="2bc56-182">在 Microsoft Azure 或 Hyper-V 中複製虛擬機器時，這些規則可能會造成問題：</span><span class="sxs-lookup"><span data-stu-id="2bc56-182">These rules can cause problems when cloning a virtual machine in Microsoft Azure or Hyper-V:</span></span>
   
        # sudo ln -s /dev/null /etc/udev/rules.d/75-persistent-net-generator.rules

6. <span data-ttu-id="2bc56-183">如果您想要 toouse hello OpenLogic 鏡像 hello Azure 資料中心內裝載，然後取代 hello`/etc/yum.repos.d/CentOS-Base.repo`以 hello 下列儲存機制的檔案。</span><span class="sxs-lookup"><span data-stu-id="2bc56-183">If you would like toouse hello OpenLogic mirrors that are hosted within hello Azure datacenters, then replace hello `/etc/yum.repos.d/CentOS-Base.repo` file with hello following repositories.</span></span>  <span data-ttu-id="2bc56-184">這也會加入 hello **[openlogic]**包含 hello Azure Linux 代理程式的封裝儲存機制：</span><span class="sxs-lookup"><span data-stu-id="2bc56-184">This will also add hello **[openlogic]** repository that includes packages for hello Azure Linux agent:</span></span>
   
        [openlogic]
        name=CentOS-$releasever - openlogic packages for $basearch
        baseurl=http://olcentgbl.trafficmanager.net/openlogic/$releasever/openlogic/$basearch/
        enabled=1
        gpgcheck=0
        
        [base]
        name=CentOS-$releasever - Base
        #mirrorlist=http://mirrorlist.centos.org/?release=$releasever&arch=$basearch&repo=os&infra=$infra
        baseurl=http://olcentgbl.trafficmanager.net/centos/$releasever/os/$basearch/
        gpgcheck=1
        gpgkey=file:///etc/pki/rpm-gpg/RPM-GPG-KEY-CentOS-7
        
        #released updates
        [updates]
        name=CentOS-$releasever - Updates
        #mirrorlist=http://mirrorlist.centos.org/?release=$releasever&arch=$basearch&repo=updates&infra=$infra
        baseurl=http://olcentgbl.trafficmanager.net/centos/$releasever/updates/$basearch/
        gpgcheck=1
        gpgkey=file:///etc/pki/rpm-gpg/RPM-GPG-KEY-CentOS-7
        
        #additional packages that may be useful
        [extras]
        name=CentOS-$releasever - Extras
        #mirrorlist=http://mirrorlist.centos.org/?release=$releasever&arch=$basearch&repo=extras&infra=$infra
        baseurl=http://olcentgbl.trafficmanager.net/centos/$releasever/extras/$basearch/
        gpgcheck=1
        gpgkey=file:///etc/pki/rpm-gpg/RPM-GPG-KEY-CentOS-7
        
        #additional packages that extend functionality of existing packages
        [centosplus]
        name=CentOS-$releasever - Plus
        #mirrorlist=http://mirrorlist.centos.org/?release=$releasever&arch=$basearch&repo=centosplus&infra=$infra
        baseurl=http://olcentgbl.trafficmanager.net/centos/$releasever/centosplus/$basearch/
        gpgcheck=1
        enabled=0
        gpgkey=file:///etc/pki/rpm-gpg/RPM-GPG-KEY-CentOS-7

    >[!Note]
    <span data-ttu-id="2bc56-185">hello 本指南的其餘部分將假設您使用至少 hello`[openlogic]`儲存機制，將會使用的 tooinstall hello Azure Linux 代理程式下方。</span><span class="sxs-lookup"><span data-stu-id="2bc56-185">hello rest of this guide will assume you are using at least hello `[openlogic]` repo, which will be used tooinstall hello Azure Linux agent below.</span></span>

7. <span data-ttu-id="2bc56-186">執行下列命令 tooclear hello 目前 yum 中繼資料的 hello 並安裝任何更新：</span><span class="sxs-lookup"><span data-stu-id="2bc56-186">Run hello following command tooclear hello current yum metadata and install any updates:</span></span>
   
        # sudo yum clean all

    <span data-ttu-id="2bc56-187">除非您要建立較舊版本的 CentOS 的映像，我們建議所有 hello 的 tooupdate 封裝 toohello 最新版本：</span><span class="sxs-lookup"><span data-stu-id="2bc56-187">Unless you are creating an image for an older version of CentOS, it is recommended tooupdate all hello packages toohello latest:</span></span>

        # sudo yum -y update

    <span data-ttu-id="2bc56-188">執行此命令之後可能需要重新開機。</span><span class="sxs-lookup"><span data-stu-id="2bc56-188">A reboot maybe required after running this command.</span></span>

8. <span data-ttu-id="2bc56-189">修改 Azure hello 核心開機行幼蟲組態 tooinclude 其他核心參數中。</span><span class="sxs-lookup"><span data-stu-id="2bc56-189">Modify hello kernel boot line in your grub configuration tooinclude additional kernel parameters for Azure.</span></span> <span data-ttu-id="2bc56-190">toodo，開啟`/etc/default/grub`在文字編輯器，編輯 hello`GRUB_CMDLINE_LINUX`參數，例如：</span><span class="sxs-lookup"><span data-stu-id="2bc56-190">toodo this, open `/etc/default/grub` in a text editor and edit hello `GRUB_CMDLINE_LINUX` parameter, for example:</span></span>
   
        GRUB_CMDLINE_LINUX="rootdelay=300 console=ttyS0 earlyprintk=ttyS0 net.ifnames=0"
   
   <span data-ttu-id="2bc56-191">這也可確保所有的主控台訊息都會傳送 toohello 第一個序列連接埠，這可協助 Azure 偵錯問題的支援。</span><span class="sxs-lookup"><span data-stu-id="2bc56-191">This will also ensure all console messages are sent toohello first serial port, which can assist Azure support with debugging issues.</span></span> <span data-ttu-id="2bc56-192">它也會關閉 hello 新 CentOS 7 命名慣例的 Nic。</span><span class="sxs-lookup"><span data-stu-id="2bc56-192">It also turns off hello new CentOS 7 naming conventions for NICs.</span></span> <span data-ttu-id="2bc56-193">除了上述 toohello 建議太*移除*hello 下列參數：</span><span class="sxs-lookup"><span data-stu-id="2bc56-193">In addition toohello above, it is recommended too*remove* hello following parameters:</span></span>
   
        rhgb quiet crashkernel=auto
   
    <span data-ttu-id="2bc56-194">沒有適用於雲端環境，我們想要傳送 toohello 序列連接埠的所有 hello 記錄 toobe 圖形和無訊息的開機。</span><span class="sxs-lookup"><span data-stu-id="2bc56-194">Graphical and quiet boot are not useful in a cloud environment where we want all hello logs toobe sent toohello serial port.</span></span> <span data-ttu-id="2bc56-195">hello`crashkernel`選項可能會是左設定如有需要，但請注意，這個參數會減少 hello hello 128 MB 以上，VM 中可用的記憶體數量可能會造成問題 hello 較小的 VM 大小。</span><span class="sxs-lookup"><span data-stu-id="2bc56-195">hello `crashkernel` option may be left configured if desired, but note that this parameter will reduce hello amount of available memory in hello VM by 128MB or more, which may be problematic on hello smaller VM sizes.</span></span>

9. <span data-ttu-id="2bc56-196">在您完成編輯`/etc/default/grub`每個以上版本，執行下列命令 toorebuild hello 幼蟲組態 hello:</span><span class="sxs-lookup"><span data-stu-id="2bc56-196">Once you are done editing `/etc/default/grub` per above, run hello following command toorebuild hello grub configuration:</span></span>
   
        # sudo grub2-mkconfig -o /boot/grub2/grub.cfg

10. <span data-ttu-id="2bc56-197">如果建置 hello 映像從**VMWare、 VirtualBox 或 KVM:**請 hello HYPER-V 驅動程式隨附的 hello initramfs:</span><span class="sxs-lookup"><span data-stu-id="2bc56-197">If building hello image from **VMWare, VirtualBox or KVM:** Ensure hello Hyper-V drivers are included in hello initramfs:</span></span>
   
   <span data-ttu-id="2bc56-198">編輯 `/etc/dracut.conf`，新增內容：</span><span class="sxs-lookup"><span data-stu-id="2bc56-198">Edit `/etc/dracut.conf`, add content:</span></span>
   
        add_drivers+=”hv_vmbus hv_netvsc hv_storvsc”
   
   <span data-ttu-id="2bc56-199">重建 hello initramfs:</span><span class="sxs-lookup"><span data-stu-id="2bc56-199">Rebuild hello initramfs:</span></span>
   
        # sudo dracut –f -v

11. <span data-ttu-id="2bc56-200">安裝 hello Azure Linux 代理程式和相依性：</span><span class="sxs-lookup"><span data-stu-id="2bc56-200">Install hello Azure Linux Agent and dependencies:</span></span>

        # sudo yum install python-pyasn1 WALinuxAgent
        # sudo systemctl enable waagent

12. <span data-ttu-id="2bc56-201">不要在 hello OS 磁碟上建立的交換空間。</span><span class="sxs-lookup"><span data-stu-id="2bc56-201">Do not create swap space on hello OS disk.</span></span>
   
   <span data-ttu-id="2bc56-202">hello Azure Linux 代理程式可以自動設定使用之後附加的 toohello VM 在 Azure 上佈建的 hello 本機資源磁碟的交換空間。</span><span class="sxs-lookup"><span data-stu-id="2bc56-202">hello Azure Linux Agent can automatically configure swap space using hello local resource disk that is attached toohello VM after provisioning on Azure.</span></span> <span data-ttu-id="2bc56-203">請注意該 hello 本機資源磁碟是*暫存*磁碟，以及可能會在取消佈建 hello VM 時清空。</span><span class="sxs-lookup"><span data-stu-id="2bc56-203">Note that hello local resource disk is a *temporary* disk, and might be emptied when hello VM is deprovisioned.</span></span> <span data-ttu-id="2bc56-204">在安裝之後 hello Azure Linux 代理程式 （請參閱上一個步驟），修改下列參數中的 hello`/etc/waagent.conf`適當地：</span><span class="sxs-lookup"><span data-stu-id="2bc56-204">After installing hello Azure Linux Agent (see previous step), modify hello following parameters in `/etc/waagent.conf` appropriately:</span></span>
   
        ResourceDisk.Format=y
        ResourceDisk.Filesystem=ext4
        ResourceDisk.MountPoint=/mnt/resource
        ResourceDisk.EnableSwap=y
        ResourceDisk.SwapSizeMB=2048    ## NOTE: set this toowhatever you need it toobe.

13. <span data-ttu-id="2bc56-205">執行下列命令 toodeprovision hello 虛擬機器的 hello 並準備在 Azure 上佈建：</span><span class="sxs-lookup"><span data-stu-id="2bc56-205">Run hello following commands toodeprovision hello virtual machine and prepare it for provisioning on Azure:</span></span>
   
        # sudo waagent -force -deprovision
        # export HISTSIZE=0
        # logout

14. <span data-ttu-id="2bc56-206">在 Hyper-V 管理員中，依序按一下 [動作] -> [關閉]。</span><span class="sxs-lookup"><span data-stu-id="2bc56-206">Click **Action -> Shut Down** in Hyper-V Manager.</span></span> <span data-ttu-id="2bc56-207">Linux VHD 是現在準備好 toobe 上傳 tooAzure。</span><span class="sxs-lookup"><span data-stu-id="2bc56-207">Your Linux VHD is now ready toobe uploaded tooAzure.</span></span>

## <a name="next-steps"></a><span data-ttu-id="2bc56-208">後續步驟</span><span class="sxs-lookup"><span data-stu-id="2bc56-208">Next steps</span></span>
<span data-ttu-id="2bc56-209">您要現在準備好 toouse CentOS Linux 虛擬硬碟 toocreate 新虛擬機器在 Azure 中。</span><span class="sxs-lookup"><span data-stu-id="2bc56-209">You're now ready toouse your CentOS Linux virtual hard disk toocreate new virtual machines in Azure.</span></span> <span data-ttu-id="2bc56-210">如果這是 hello 正在上傳 hello.vhd 檔案 tooAzure 的第一次，請參閱步驟 2 和 3 中的[建立和上傳包含 hello Linux 作業系統的虛擬硬碟](classic/create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="2bc56-210">If this is hello first time that you're uploading hello .vhd file tooAzure, see steps 2 and 3 in [Creating and uploading a virtual hard disk that contains hello Linux operating system](classic/create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).</span></span>

