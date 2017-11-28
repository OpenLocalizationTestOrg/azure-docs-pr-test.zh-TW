---
title: "在 Azure 中建立及上傳 CentOS 型 Linux VHD"
description: "了解如何建立及上傳包含 CentOS 型 Linux 作業系統的 Azure 虛擬硬碟 (VHD)。"
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
ms.openlocfilehash: 010f4b05b35fa1f31c14f34a5fae9298fcd831e4
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="prepare-a-centos-based-virtual-machine-for-azure"></a><span data-ttu-id="fa823-103">準備適用於 Azure 的 CentOS 型虛擬機器</span><span class="sxs-lookup"><span data-stu-id="fa823-103">Prepare a CentOS-based virtual machine for Azure</span></span>
* [<span data-ttu-id="fa823-104">準備適用於 Azure 的 CentOS 6.x 虛擬機器</span><span class="sxs-lookup"><span data-stu-id="fa823-104">Prepare a CentOS 6.x virtual machine for Azure</span></span>](#centos-6x)
* [<span data-ttu-id="fa823-105">準備適用於 Azure 的 CentOS 7.0+ 虛擬機器</span><span class="sxs-lookup"><span data-stu-id="fa823-105">Prepare a CentOS 7.0+ virtual machine for Azure</span></span>](#centos-70)

[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-both-include.md)]

## <a name="prerequisites"></a><span data-ttu-id="fa823-106">先決條件</span><span class="sxs-lookup"><span data-stu-id="fa823-106">Prerequisites</span></span>
<span data-ttu-id="fa823-107">本文假設您已將 CentOS (或類似的衍生物件) Linux 作業系統安裝到虛擬硬碟。</span><span class="sxs-lookup"><span data-stu-id="fa823-107">This article assumes that you have already installed a CentOS (or similar derivative) Linux operating system to a virtual hard disk.</span></span> <span data-ttu-id="fa823-108">有多個工具可用來建立 .vhd 檔案，例如，像是 Hyper-V 的虛擬化解決方案。</span><span class="sxs-lookup"><span data-stu-id="fa823-108">Multiple tools exist to create .vhd files, for example a virtualization solution such as Hyper-V.</span></span> <span data-ttu-id="fa823-109">如需指示，請參閱 [安裝 Hyper-V 角色及設定虛擬機器](http://technet.microsoft.com/library/hh846766.aspx)。</span><span class="sxs-lookup"><span data-stu-id="fa823-109">For instructions, see [Install the Hyper-V Role and Configure a Virtual Machine](http://technet.microsoft.com/library/hh846766.aspx).</span></span>

<span data-ttu-id="fa823-110">**CentOS 安裝注意事項**</span><span class="sxs-lookup"><span data-stu-id="fa823-110">**CentOS installation notes**</span></span>

* <span data-ttu-id="fa823-111">另請參閱[一般 Linux 安裝注意事項](create-upload-generic.md#general-linux-installation-notes)，了解為 Azure 準備 Linux 的更多祕訣。</span><span class="sxs-lookup"><span data-stu-id="fa823-111">Please see also [General Linux Installation Notes](create-upload-generic.md#general-linux-installation-notes) for more tips on preparing Linux for Azure.</span></span>
* <span data-ttu-id="fa823-112">Azure 不支援 VHDX 格式，只支援 **固定 VHD**。</span><span class="sxs-lookup"><span data-stu-id="fa823-112">The VHDX format is not supported in Azure, only **fixed VHD**.</span></span>  <span data-ttu-id="fa823-113">您可以使用 Hyper-V 管理員或 convert-vhd Cmdlet，將磁碟轉換為 VHD 格式。</span><span class="sxs-lookup"><span data-stu-id="fa823-113">You can convert the disk to VHD format using Hyper-V Manager or the convert-vhd cmdlet.</span></span> <span data-ttu-id="fa823-114">如果您是使用 VirtualBox，即會在建立磁碟時選取 [固定大小]  而不是預設的動態配置。</span><span class="sxs-lookup"><span data-stu-id="fa823-114">If you are using VirtualBox this means selecting **Fixed size** as opposed to the default dynamically allocated when creating the disk.</span></span>
* <span data-ttu-id="fa823-115">安裝 Linux 系統時，*建議*您使用標準磁碟分割而不是 LVM (常是許多安裝的預設設定)。</span><span class="sxs-lookup"><span data-stu-id="fa823-115">When installing the Linux system it is *recommended* that you use standard partitions rather than LVM (often the default for many installations).</span></span> <span data-ttu-id="fa823-116">這可避免 LVM 與複製之 VM 的名稱衝突，特別是為了疑難排解而需要將作業系統磁碟連接至另一個相同的 VM 時。</span><span class="sxs-lookup"><span data-stu-id="fa823-116">This will avoid LVM name conflicts with cloned VMs, particularly if an OS disk ever needs to be attached to another identical VM for troubleshooting.</span></span> <span data-ttu-id="fa823-117">如果願意，您可以在資料磁碟上使用 [LVM](configure-raid.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) 或 [RAID](configure-lvm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="fa823-117">[LVM](configure-lvm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) or [RAID](configure-raid.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) may be used on data disks.</span></span>
* <span data-ttu-id="fa823-118">需要掛接 UDF 檔案系統的核心支援。</span><span class="sxs-lookup"><span data-stu-id="fa823-118">Kernel support for mounting UDF file systems is required.</span></span> <span data-ttu-id="fa823-119">在 Azure 上第一次開機時，佈建組態會透過連接客體的 UDF 格式媒體傳遞至 Linux VM。</span><span class="sxs-lookup"><span data-stu-id="fa823-119">At first boot on Azure the provisioning configuration is passed to the Linux VM via UDF-formatted media that is attached to the guest.</span></span> <span data-ttu-id="fa823-120">Azure Linux 代理程式必須能夠掛接 UDF 檔案系統讀取其組態並佈建 VM。</span><span class="sxs-lookup"><span data-stu-id="fa823-120">The Azure Linux agent must be able to mount the UDF file system to read its configuration and provision the VM.</span></span>
* <span data-ttu-id="fa823-121">Linux Kernel 2.6.37 以下的版本不支援較大 VM 大小 Hyper-V 上的NUMA。</span><span class="sxs-lookup"><span data-stu-id="fa823-121">Linux kernel versions below 2.6.37 do not support NUMA on Hyper-V with larger VM sizes.</span></span> <span data-ttu-id="fa823-122">這個問題主要會影響使用上游 Red Hat 2.6.32 kernel 的較舊散發套件，RHEL 6.6 (kernel-2.6.32-504) 已加以修正。</span><span class="sxs-lookup"><span data-stu-id="fa823-122">This issue primarily impacts older distributions using the upstream Red Hat 2.6.32 kernel, and was fixed in RHEL 6.6 (kernel-2.6.32-504).</span></span> <span data-ttu-id="fa823-123">執行的自訂核心是 2.6.37 以前版本的系統，或 2.6.32-504 以前以 RHEL 為基礎的核心必須在 grub.conf 的核心命令列上設定開機參數 `numa=off`。</span><span class="sxs-lookup"><span data-stu-id="fa823-123">Systems running custom kernels older than 2.6.37, or RHEL-based kernels older than 2.6.32-504 must set the boot parameter `numa=off` on the kernel command-line in grub.conf.</span></span> <span data-ttu-id="fa823-124">如需詳細資訊，請參閱 Red Hat [KB 436883](https://access.redhat.com/solutions/436883)。</span><span class="sxs-lookup"><span data-stu-id="fa823-124">For more information see Red Hat [KB 436883](https://access.redhat.com/solutions/436883).</span></span>
* <span data-ttu-id="fa823-125">請勿在作業系統磁碟上設定交換磁碟分割。</span><span class="sxs-lookup"><span data-stu-id="fa823-125">Do not configure a swap partition on the OS disk.</span></span> <span data-ttu-id="fa823-126">您可以設定 Linux 代理程式在暫存資源磁碟上建立交換檔。</span><span class="sxs-lookup"><span data-stu-id="fa823-126">The Linux agent can be configured to create a swap file on the temporary resource disk.</span></span>  <span data-ttu-id="fa823-127">您可以在以下步驟中找到與此有關的詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="fa823-127">More information about this can be found in the steps below.</span></span>
* <span data-ttu-id="fa823-128">所有 VHD 的大小都必須是 1 MB 的倍數。</span><span class="sxs-lookup"><span data-stu-id="fa823-128">All of the VHDs must have sizes that are multiples of 1 MB.</span></span>

## <a name="centos-6x"></a><span data-ttu-id="fa823-129">CentOS 6.x</span><span class="sxs-lookup"><span data-stu-id="fa823-129">CentOS 6.x</span></span>

1. <span data-ttu-id="fa823-130">在 Hyper-V 管理員中，選取虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="fa823-130">In Hyper-V Manager, select the virtual machine.</span></span>

2. <span data-ttu-id="fa823-131">按一下 [連接] ，以開啟虛擬機器的主控台視窗。</span><span class="sxs-lookup"><span data-stu-id="fa823-131">Click **Connect** to open a console window for the virtual machine.</span></span>

3. <span data-ttu-id="fa823-132">在 CentOS 6 中，NetworkManager 可能會對 Azure Linux 代理程式造成干擾。</span><span class="sxs-lookup"><span data-stu-id="fa823-132">In CentOS 6, NetworkManager can interfere with the Azure Linux agent.</span></span> <span data-ttu-id="fa823-133">執行下列命令以將此套件解除安裝：</span><span class="sxs-lookup"><span data-stu-id="fa823-133">Uninstall this package by running the following command:</span></span>
   
        # sudo rpm -e --nodeps NetworkManager

4. <span data-ttu-id="fa823-134">建立或編輯檔案 `/etc/sysconfig/network` 並新增下列文字：</span><span class="sxs-lookup"><span data-stu-id="fa823-134">Create or edit the file `/etc/sysconfig/network` and add the following text:</span></span>
   
        NETWORKING=yes
        HOSTNAME=localhost.localdomain

5. <span data-ttu-id="fa823-135">建立或編輯檔案 `/etc/sysconfig/network-scripts/ifcfg-eth0` 並新增下列文字：</span><span class="sxs-lookup"><span data-stu-id="fa823-135">Create or edit the file `/etc/sysconfig/network-scripts/ifcfg-eth0` and add the following text:</span></span>
   
        DEVICE=eth0
        ONBOOT=yes
        BOOTPROTO=dhcp
        TYPE=Ethernet
        USERCTL=no
        PEERDNS=yes
        IPV6INIT=no

6. <span data-ttu-id="fa823-136">修改 udev 角色可防止產生乙太網路介面的靜態規則。</span><span class="sxs-lookup"><span data-stu-id="fa823-136">Modify udev rules to avoid generating static rules for the Ethernet interface(s).</span></span> <span data-ttu-id="fa823-137">在 Microsoft Azure 或 Hyper-V 中複製虛擬機器時，這些規則可能會造成問題：</span><span class="sxs-lookup"><span data-stu-id="fa823-137">These rules can cause problems when cloning a virtual machine in Microsoft Azure or Hyper-V:</span></span>
   
        # sudo ln -s /dev/null /etc/udev/rules.d/75-persistent-net-generator.rules
        # sudo rm -f /etc/udev/rules.d/70-persistent-net.rules

7. <span data-ttu-id="fa823-138">要確保開機時會啟動網路服務，可執行以下命令：</span><span class="sxs-lookup"><span data-stu-id="fa823-138">Ensure the network service will start at boot time by running the following command:</span></span>
   
        # sudo chkconfig network on

8. <span data-ttu-id="fa823-139">如果您想要使用在 Azure 資料中心內託管的 OpenLogic 鏡像，請使用下列存放庫來取代 `/etc/yum.repos.d/CentOS-Base.repo` 檔案。</span><span class="sxs-lookup"><span data-stu-id="fa823-139">If you would like to use the OpenLogic mirrors that are hosted within the Azure datacenters, then replace the `/etc/yum.repos.d/CentOS-Base.repo` file with the following repositories.</span></span>  <span data-ttu-id="fa823-140">這也會新增包括額外套件 (例如 Azure Linux 代理程式) 的 **[openlogic]** 存放庫：</span><span class="sxs-lookup"><span data-stu-id="fa823-140">This will also add the **[openlogic]** repository that includes additional packages such as the Azure Linux agent:</span></span>

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
    <span data-ttu-id="fa823-141">本指南的其他部分將假設您至少會使用 `[openlogic]` 存放庫，該存放庫稍後將可用來安裝下面的 Azure Linux 代理程式。</span><span class="sxs-lookup"><span data-stu-id="fa823-141">The rest of this guide will assume you are using at least the `[openlogic]` repo, which will be used to install the Azure Linux agent below.</span></span>


9. <span data-ttu-id="fa823-142">在 /etc/yum.conf 中加入這一行：</span><span class="sxs-lookup"><span data-stu-id="fa823-142">Add the following line to /etc/yum.conf:</span></span>
    
        http_caching=packages

10. <span data-ttu-id="fa823-143">執行下列命令，以清除目前的 yum 中繼資料並使用最新的套件來更新系統：</span><span class="sxs-lookup"><span data-stu-id="fa823-143">Run the following command to clear the current yum metadata and update the system with the latest packages:</span></span>
    
        # yum clean all

    <span data-ttu-id="fa823-144">除非您要為舊版 CentOS 建立映像，否則建議您將所有套件更新到最新版本：</span><span class="sxs-lookup"><span data-stu-id="fa823-144">Unless you are creating an image for an older version of CentOS, it is recommended to update all the packages to the latest:</span></span>

        # sudo yum -y update

    <span data-ttu-id="fa823-145">執行此命令之後可能需要重新開機。</span><span class="sxs-lookup"><span data-stu-id="fa823-145">A reboot may be required after running this command.</span></span>

11. <span data-ttu-id="fa823-146">(選擇性) 安裝 Linux 整合服務 (LIS) 的驅動程式。</span><span class="sxs-lookup"><span data-stu-id="fa823-146">(Optional) Install the drivers for the Linux Integration Services (LIS).</span></span>
   
    >[!IMPORTANT]
    <span data-ttu-id="fa823-147">此步驟對 CentOS 6.3 與更舊版本而言為**必要步驟**，但對於較新的版本而言則為選擇性步驟。</span><span class="sxs-lookup"><span data-stu-id="fa823-147">The step is **required** for CentOS 6.3 and earlier, and optional for later releases.</span></span>

        # sudo rpm -e hypervkvpd  ## (may return error if not installed, that's OK)
        # sudo yum install microsoft-hyper-v

    <span data-ttu-id="fa823-148">或者，您可以依照 [LIS 下載頁面](https://go.microsoft.com/fwlink/?linkid=403033)上的手動安裝指示執行，以在您的 VM 上安裝該 RPM。</span><span class="sxs-lookup"><span data-stu-id="fa823-148">Alternatively, you can follow the manual installation instructions on the [LIS download page](https://go.microsoft.com/fwlink/?linkid=403033) to install the RPM onto your VM.</span></span>
 
12. <span data-ttu-id="fa823-149">安裝 Azure Linux 代理程式與相依性：</span><span class="sxs-lookup"><span data-stu-id="fa823-149">Install the Azure Linux Agent and dependencies:</span></span>
    
        # sudo yum install python-pyasn1 WALinuxAgent
    
    <span data-ttu-id="fa823-150">如果未如步驟 3 所述移除 NetworkManager 和 NetworkManager-gnome 套件，則 WALinuxAgent 套件會將這兩個套件移除。</span><span class="sxs-lookup"><span data-stu-id="fa823-150">The WALinuxAgent package will remove the NetworkManager and NetworkManager-gnome packages if they were not already removed as described in step 3.</span></span>


13. <span data-ttu-id="fa823-151">修改 grub 組態中的核心開機那一行，使其額外包含用於 Azure 的核心參數。</span><span class="sxs-lookup"><span data-stu-id="fa823-151">Modify the kernel boot line in your grub configuration to include additional kernel parameters for Azure.</span></span> <span data-ttu-id="fa823-152">若要這樣做，請在文字編輯器中開啟 `/boot/grub/menu.lst`，並確定預設核心包含以下參數：</span><span class="sxs-lookup"><span data-stu-id="fa823-152">To do this, open `/boot/grub/menu.lst` in a text editor and ensure that the default kernel includes the following parameters:</span></span>
    
        console=ttyS0 earlyprintk=ttyS0 rootdelay=300
    
    <span data-ttu-id="fa823-153">這也將確保所有主控台訊息都會傳送給第一個序列埠，有助於 Azure 支援團隊進行問題偵錯程序。</span><span class="sxs-lookup"><span data-stu-id="fa823-153">This will also ensure all console messages are sent to the first serial port, which can assist Azure support with debugging issues.</span></span>
    
    <span data-ttu-id="fa823-154">除了上述以外，我們還建議您 *移除* 下列參數：</span><span class="sxs-lookup"><span data-stu-id="fa823-154">In addition to the above, it is recommended to *remove* the following parameters:</span></span>
    
        rhgb quiet crashkernel=auto
    
    <span data-ttu-id="fa823-155">在雲端環境中，我們會將所有記錄傳送到序列埠，因此不適合使用圖形化和無訊息啟動。</span><span class="sxs-lookup"><span data-stu-id="fa823-155">Graphical and quiet boot are not useful in a cloud environment where we want all the logs to be sent to the serial port.</span></span>  <span data-ttu-id="fa823-156">如有需要，您可以保留 `crashkernel` 選項的設定，但請注意，此參數將會減少 VM 中約 128MB 或以上的可用記憶體數量，這在較小的 VM 中可能會是個問題。</span><span class="sxs-lookup"><span data-stu-id="fa823-156">The `crashkernel` option may be left configured if desired, but note that this parameter will reduce the amount of available memory in the VM by 128MB or more, which may be problematic on the smaller VM sizes.</span></span>

    >[!Important]
    <span data-ttu-id="fa823-157">CentOS 6.5 與較舊版本也必須設定核心參數 `numa=off`。</span><span class="sxs-lookup"><span data-stu-id="fa823-157">CentOS 6.5 and earlier must also set the kernel parameter `numa=off`.</span></span> <span data-ttu-id="fa823-158">請參閱 Red Hat [KB 436883](https://access.redhat.com/solutions/436883)。</span><span class="sxs-lookup"><span data-stu-id="fa823-158">See Red Hat [KB 436883](https://access.redhat.com/solutions/436883).</span></span>

14. <span data-ttu-id="fa823-159">確定您已安裝 SSH 伺服器，並已設定為在開機時啟動。</span><span class="sxs-lookup"><span data-stu-id="fa823-159">Ensure that the SSH server is installed and configured to start at boot time.</span></span>  <span data-ttu-id="fa823-160">這通常是預設值。</span><span class="sxs-lookup"><span data-stu-id="fa823-160">This is usually the default.</span></span>

15. <span data-ttu-id="fa823-161">請勿在作業系統磁碟上建立交換空間。</span><span class="sxs-lookup"><span data-stu-id="fa823-161">Do not create swap space on the OS disk.</span></span>
    
    <span data-ttu-id="fa823-162">Azure Linux 代理程式可在 VM 佈建於 Azure 後，使用附加至 VM 的本機資源磁碟自動設定交換空間。</span><span class="sxs-lookup"><span data-stu-id="fa823-162">The Azure Linux Agent can automatically configure swap space using the local resource disk that is attached to the VM after provisioning on Azure.</span></span> <span data-ttu-id="fa823-163">請注意，資源磁碟是 *暫存* 磁碟，可能會在 VM 取消佈建時清空。</span><span class="sxs-lookup"><span data-stu-id="fa823-163">Note that the local resource disk is a *temporary* disk, and might be emptied when the VM is deprovisioned.</span></span> <span data-ttu-id="fa823-164">安裝 Azure Linux 代理程式 (請參閱上一個步驟) 後，請在 `/etc/waagent.conf` 中適當修改下列參數：</span><span class="sxs-lookup"><span data-stu-id="fa823-164">After installing the Azure Linux Agent (see previous step), modify the following parameters in `/etc/waagent.conf` appropriately:</span></span>
    
        ResourceDisk.Format=y
        ResourceDisk.Filesystem=ext4
        ResourceDisk.MountPoint=/mnt/resource
        ResourceDisk.EnableSwap=y
        ResourceDisk.SwapSizeMB=2048    ## NOTE: set this to whatever you need it to be.

16. <span data-ttu-id="fa823-165">執行下列命令，以取消佈建虛擬機器，並準備將它佈建於 Azure 上：</span><span class="sxs-lookup"><span data-stu-id="fa823-165">Run the following commands to deprovision the virtual machine and prepare it for provisioning on Azure:</span></span>
    
        # sudo waagent -force -deprovision
        # export HISTSIZE=0
        # logout

17. <span data-ttu-id="fa823-166">在 Hyper-V 管理員中，依序按一下 [動作] -> [關閉]。</span><span class="sxs-lookup"><span data-stu-id="fa823-166">Click **Action -> Shut Down** in Hyper-V Manager.</span></span> <span data-ttu-id="fa823-167">您現在可以將 Linux VHD 上傳至 Azure。</span><span class="sxs-lookup"><span data-stu-id="fa823-167">Your Linux VHD is now ready to be uploaded to Azure.</span></span>


- - -
## <a name="centos-70"></a><span data-ttu-id="fa823-168">CentOS 7.0+</span><span class="sxs-lookup"><span data-stu-id="fa823-168">CentOS 7.0+</span></span>
<span data-ttu-id="fa823-169">**CentOS 7 (和類似的衍生項目) 中的變更**</span><span class="sxs-lookup"><span data-stu-id="fa823-169">**Changes in CentOS 7 (and similar derivatives)**</span></span>

<span data-ttu-id="fa823-170">準備適用於 Azure 的 CentOS 7 虛擬機器會與 CentOS 6 極為類似，不過，其中有幾個重要差異值得注意：</span><span class="sxs-lookup"><span data-stu-id="fa823-170">Preparing a CentOS 7 virtual machine for Azure is very similar to CentOS 6, however there are several important differences worth noting:</span></span>

* <span data-ttu-id="fa823-171">NetworkManager 封裝不會再與 Azure Linux 代理程式發生衝突。</span><span class="sxs-lookup"><span data-stu-id="fa823-171">The NetworkManager package no longer conflicts with the Azure Linux agent.</span></span> <span data-ttu-id="fa823-172">依預設會安裝此封裝，建議您不要將它移除。</span><span class="sxs-lookup"><span data-stu-id="fa823-172">This package is installed by default and we recommend that it is not removed.</span></span>
* <span data-ttu-id="fa823-173">GRUB2 現已作為預設的開機載入器使用，因此我們已變更編輯核心參數的程序 (如下所示)。</span><span class="sxs-lookup"><span data-stu-id="fa823-173">GRUB2 is now used as the default bootloader, so the procedure for editing kernel parameters has changed (see below).</span></span>
* <span data-ttu-id="fa823-174">XFS 現為預設的檔案系統。</span><span class="sxs-lookup"><span data-stu-id="fa823-174">XFS is now the default file system.</span></span> <span data-ttu-id="fa823-175">如有需要，您仍可使用 ext4 檔案系統。</span><span class="sxs-lookup"><span data-stu-id="fa823-175">The ext4 file system can still be used if desired.</span></span>

<span data-ttu-id="fa823-176">**組態步驟**</span><span class="sxs-lookup"><span data-stu-id="fa823-176">**Configuration Steps**</span></span>

1. <span data-ttu-id="fa823-177">在 Hyper-V 管理員中，選取虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="fa823-177">In Hyper-V Manager, select the virtual machine.</span></span>

2. <span data-ttu-id="fa823-178">按一下 [連接] ，以開啟虛擬機器的主控台視窗。</span><span class="sxs-lookup"><span data-stu-id="fa823-178">Click **Connect** to open a console window for the virtual machine.</span></span>

3. <span data-ttu-id="fa823-179">建立或編輯檔案 `/etc/sysconfig/network` 並新增下列文字：</span><span class="sxs-lookup"><span data-stu-id="fa823-179">Create or edit the file `/etc/sysconfig/network` and add the following text:</span></span>
   
        NETWORKING=yes
        HOSTNAME=localhost.localdomain

4. <span data-ttu-id="fa823-180">建立或編輯檔案 `/etc/sysconfig/network-scripts/ifcfg-eth0` 並新增下列文字：</span><span class="sxs-lookup"><span data-stu-id="fa823-180">Create or edit the file `/etc/sysconfig/network-scripts/ifcfg-eth0` and add the following text:</span></span>
   
        DEVICE=eth0
        ONBOOT=yes
        BOOTPROTO=dhcp
        TYPE=Ethernet
        USERCTL=no
        PEERDNS=yes
        IPV6INIT=no
        NM_CONTROLLED=no

5. <span data-ttu-id="fa823-181">修改 udev 角色可防止產生乙太網路介面的靜態規則。</span><span class="sxs-lookup"><span data-stu-id="fa823-181">Modify udev rules to avoid generating static rules for the Ethernet interface(s).</span></span> <span data-ttu-id="fa823-182">在 Microsoft Azure 或 Hyper-V 中複製虛擬機器時，這些規則可能會造成問題：</span><span class="sxs-lookup"><span data-stu-id="fa823-182">These rules can cause problems when cloning a virtual machine in Microsoft Azure or Hyper-V:</span></span>
   
        # sudo ln -s /dev/null /etc/udev/rules.d/75-persistent-net-generator.rules

6. <span data-ttu-id="fa823-183">如果您想要使用在 Azure 資料中心內託管的 OpenLogic 鏡像，請使用下列存放庫來取代 `/etc/yum.repos.d/CentOS-Base.repo` 檔案。</span><span class="sxs-lookup"><span data-stu-id="fa823-183">If you would like to use the OpenLogic mirrors that are hosted within the Azure datacenters, then replace the `/etc/yum.repos.d/CentOS-Base.repo` file with the following repositories.</span></span>  <span data-ttu-id="fa823-184">這也會新增包含 Azure Linux 代理程式封裝的 **[openlogic]** 儲存機制：</span><span class="sxs-lookup"><span data-stu-id="fa823-184">This will also add the **[openlogic]** repository that includes packages for the Azure Linux agent:</span></span>
   
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
    <span data-ttu-id="fa823-185">本指南的其他部分將假設您至少會使用 `[openlogic]` 存放庫，該存放庫稍後將可用來安裝下面的 Azure Linux 代理程式。</span><span class="sxs-lookup"><span data-stu-id="fa823-185">The rest of this guide will assume you are using at least the `[openlogic]` repo, which will be used to install the Azure Linux agent below.</span></span>

7. <span data-ttu-id="fa823-186">執行下列命令，以清除目前的 yum 中繼資料並安裝任何更新：</span><span class="sxs-lookup"><span data-stu-id="fa823-186">Run the following command to clear the current yum metadata and install any updates:</span></span>
   
        # sudo yum clean all

    <span data-ttu-id="fa823-187">除非您要為舊版 CentOS 建立映像，否則建議您將所有套件更新到最新版本：</span><span class="sxs-lookup"><span data-stu-id="fa823-187">Unless you are creating an image for an older version of CentOS, it is recommended to update all the packages to the latest:</span></span>

        # sudo yum -y update

    <span data-ttu-id="fa823-188">執行此命令之後可能需要重新開機。</span><span class="sxs-lookup"><span data-stu-id="fa823-188">A reboot maybe required after running this command.</span></span>

8. <span data-ttu-id="fa823-189">修改 grub 組態中的核心開機那一行，使其額外包含用於 Azure 的核心參數。</span><span class="sxs-lookup"><span data-stu-id="fa823-189">Modify the kernel boot line in your grub configuration to include additional kernel parameters for Azure.</span></span> <span data-ttu-id="fa823-190">若要這樣做，請在文字編輯器中開啟 `/etc/default/grub` 並編輯 `GRUB_CMDLINE_LINUX` 參數，例如：</span><span class="sxs-lookup"><span data-stu-id="fa823-190">To do this, open `/etc/default/grub` in a text editor and edit the `GRUB_CMDLINE_LINUX` parameter, for example:</span></span>
   
        GRUB_CMDLINE_LINUX="rootdelay=300 console=ttyS0 earlyprintk=ttyS0 net.ifnames=0"
   
   <span data-ttu-id="fa823-191">這也將確保所有主控台訊息都會傳送給第一個序列埠，有助於 Azure 支援團隊進行問題偵錯程序。</span><span class="sxs-lookup"><span data-stu-id="fa823-191">This will also ensure all console messages are sent to the first serial port, which can assist Azure support with debugging issues.</span></span> <span data-ttu-id="fa823-192">也會關閉新的 CentOS 7 對 NIC 的命名慣例。</span><span class="sxs-lookup"><span data-stu-id="fa823-192">It also turns off the new CentOS 7 naming conventions for NICs.</span></span> <span data-ttu-id="fa823-193">除了上述以外，我們還建議您 *移除* 下列參數：</span><span class="sxs-lookup"><span data-stu-id="fa823-193">In addition to the above, it is recommended to *remove* the following parameters:</span></span>
   
        rhgb quiet crashkernel=auto
   
    <span data-ttu-id="fa823-194">在雲端環境中，我們會將所有記錄傳送到序列埠，因此不適合使用圖形化和無訊息啟動。</span><span class="sxs-lookup"><span data-stu-id="fa823-194">Graphical and quiet boot are not useful in a cloud environment where we want all the logs to be sent to the serial port.</span></span> <span data-ttu-id="fa823-195">如有需要，您可以保留 `crashkernel` 選項的設定，但請注意，此參數將會減少 VM 中約 128MB 或以上的可用記憶體數量，這在較小的 VM 中可能會是個問題。</span><span class="sxs-lookup"><span data-stu-id="fa823-195">The `crashkernel` option may be left configured if desired, but note that this parameter will reduce the amount of available memory in the VM by 128MB or more, which may be problematic on the smaller VM sizes.</span></span>

9. <span data-ttu-id="fa823-196">在您參照上述完成編輯 `/etc/default/grub` 之後，請執行下列命令以重建 grub 組態：</span><span class="sxs-lookup"><span data-stu-id="fa823-196">Once you are done editing `/etc/default/grub` per above, run the following command to rebuild the grub configuration:</span></span>
   
        # sudo grub2-mkconfig -o /boot/grub2/grub.cfg

10. <span data-ttu-id="fa823-197">若要從 **VMWare、VirtualBox 或 KVM 建置映像：**請確定 initramfs 中已包括 Hyper-V 驅動程式：</span><span class="sxs-lookup"><span data-stu-id="fa823-197">If building the image from **VMWare, VirtualBox or KVM:** Ensure the Hyper-V drivers are included in the initramfs:</span></span>
   
   <span data-ttu-id="fa823-198">編輯 `/etc/dracut.conf`，新增內容：</span><span class="sxs-lookup"><span data-stu-id="fa823-198">Edit `/etc/dracut.conf`, add content:</span></span>
   
        add_drivers+=”hv_vmbus hv_netvsc hv_storvsc”
   
   <span data-ttu-id="fa823-199">重建 initramfs：</span><span class="sxs-lookup"><span data-stu-id="fa823-199">Rebuild the initramfs:</span></span>
   
        # sudo dracut –f -v

11. <span data-ttu-id="fa823-200">安裝 Azure Linux 代理程式與相依性：</span><span class="sxs-lookup"><span data-stu-id="fa823-200">Install the Azure Linux Agent and dependencies:</span></span>

        # sudo yum install python-pyasn1 WALinuxAgent
        # sudo systemctl enable waagent

12. <span data-ttu-id="fa823-201">請勿在作業系統磁碟上建立交換空間。</span><span class="sxs-lookup"><span data-stu-id="fa823-201">Do not create swap space on the OS disk.</span></span>
   
   <span data-ttu-id="fa823-202">Azure Linux 代理程式可在 VM 佈建於 Azure 後，使用附加至 VM 的本機資源磁碟自動設定交換空間。</span><span class="sxs-lookup"><span data-stu-id="fa823-202">The Azure Linux Agent can automatically configure swap space using the local resource disk that is attached to the VM after provisioning on Azure.</span></span> <span data-ttu-id="fa823-203">請注意，資源磁碟是 *暫存* 磁碟，可能會在 VM 取消佈建時清空。</span><span class="sxs-lookup"><span data-stu-id="fa823-203">Note that the local resource disk is a *temporary* disk, and might be emptied when the VM is deprovisioned.</span></span> <span data-ttu-id="fa823-204">安裝 Azure Linux 代理程式 (請參閱上一個步驟) 後，請在 `/etc/waagent.conf` 中適當修改下列參數：</span><span class="sxs-lookup"><span data-stu-id="fa823-204">After installing the Azure Linux Agent (see previous step), modify the following parameters in `/etc/waagent.conf` appropriately:</span></span>
   
        ResourceDisk.Format=y
        ResourceDisk.Filesystem=ext4
        ResourceDisk.MountPoint=/mnt/resource
        ResourceDisk.EnableSwap=y
        ResourceDisk.SwapSizeMB=2048    ## NOTE: set this to whatever you need it to be.

13. <span data-ttu-id="fa823-205">執行下列命令，以取消佈建虛擬機器，並準備將它佈建於 Azure 上：</span><span class="sxs-lookup"><span data-stu-id="fa823-205">Run the following commands to deprovision the virtual machine and prepare it for provisioning on Azure:</span></span>
   
        # sudo waagent -force -deprovision
        # export HISTSIZE=0
        # logout

14. <span data-ttu-id="fa823-206">在 Hyper-V 管理員中，依序按一下 [動作] -> [關閉]。</span><span class="sxs-lookup"><span data-stu-id="fa823-206">Click **Action -> Shut Down** in Hyper-V Manager.</span></span> <span data-ttu-id="fa823-207">您現在可以將 Linux VHD 上傳至 Azure。</span><span class="sxs-lookup"><span data-stu-id="fa823-207">Your Linux VHD is now ready to be uploaded to Azure.</span></span>

## <a name="next-steps"></a><span data-ttu-id="fa823-208">後續步驟</span><span class="sxs-lookup"><span data-stu-id="fa823-208">Next steps</span></span>
<span data-ttu-id="fa823-209">您現在可以開始使用您的 CentOS Linux 虛擬硬碟在 Azure 建立新的虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="fa823-209">You're now ready to use your CentOS Linux virtual hard disk to create new virtual machines in Azure.</span></span> <span data-ttu-id="fa823-210">若這是您第一次將該 .vhd 檔案上傳到 Azure，請參閱 [建立及上傳包含 Linux 作業系統的虛擬硬碟](classic/create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)中的步驟 2 和步驟 3。</span><span class="sxs-lookup"><span data-stu-id="fa823-210">If this is the first time that you're uploading the .vhd file to Azure, see steps 2 and 3 in [Creating and uploading a virtual hard disk that contains the Linux operating system](classic/create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).</span></span>

