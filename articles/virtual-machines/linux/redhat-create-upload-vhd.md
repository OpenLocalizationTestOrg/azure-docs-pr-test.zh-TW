---
title: "aaaCreate 和在 Azure 中使用 Red Hat Enterprise Linux VHD 上傳 |Microsoft 文件"
description: "了解 toocreate 和上傳 Azure 虛擬硬碟 (VHD)，其中包含 Red Hat Linux 作業系統。"
services: virtual-machines-linux
documentationcenter: 
author: szarkos
manager: timlt
editor: tysonn
tags: azure-resource-manager,azure-service-management
ms.assetid: 6c6b8f72-32d3-47fa-be94-6cb54537c69f
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 04/28/2017
ms.author: szark
ms.openlocfilehash: bdd1bbfbee55b5cc61d69a09b06b6bd2c3de362b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="prepare-a-red-hat-based-virtual-machine-for-azure"></a><span data-ttu-id="88e3e-103">準備適用於 Azure 的 Red Hat 型虛擬機器</span><span class="sxs-lookup"><span data-stu-id="88e3e-103">Prepare a Red Hat-based virtual machine for Azure</span></span>
<span data-ttu-id="88e3e-104">在本文中，您將學習如何 tooprepare Red Hat Enterprise Linux (RHEL) 以用於 Azure 虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="88e3e-104">In this article, you will learn how tooprepare a Red Hat Enterprise Linux (RHEL) virtual machine for use in Azure.</span></span> <span data-ttu-id="88e3e-105">hello 是舊版的 RHEL 涵蓋在本文中 6.7 + 和 7.1 +。</span><span class="sxs-lookup"><span data-stu-id="88e3e-105">hello versions of RHEL that are covered in this article are 6.7+ and 7.1+.</span></span> <span data-ttu-id="88e3e-106">涵蓋在本文章的 hello hypervisor 的準備為 HYPER-V、 核心為基礎的虛擬機器 (KVM) 和 VMware。</span><span class="sxs-lookup"><span data-stu-id="88e3e-106">hello hypervisors for preparation that are covered in this article are Hyper-V, kernel-based virtual machine (KVM), and VMware.</span></span> <span data-ttu-id="88e3e-107">如需參加 Red Hat 雲端存取方案之資格需求的詳細資訊，請參閱 [Red Hat 雲端存取網站](http://www.redhat.com/en/technologies/cloud-computing/cloud-access)與[在 Azure 上執行 RHEL](https://access.redhat.com/ecosystem/ccsp/microsoft-azure)。</span><span class="sxs-lookup"><span data-stu-id="88e3e-107">For more information about eligibility requirements for participating in Red Hat's Cloud Access program, see [Red Hat's Cloud Access website](http://www.redhat.com/en/technologies/cloud-computing/cloud-access) and [Running RHEL on Azure](https://access.redhat.com/ecosystem/ccsp/microsoft-azure).</span></span>

## <a name="prepare-a-red-hat-based-virtual-machine-from-hyper-v-manager"></a><span data-ttu-id="88e3e-108">從 Hyper-V 管理員準備 Red Hat 型虛擬機器</span><span class="sxs-lookup"><span data-stu-id="88e3e-108">Prepare a Red Hat-based virtual machine from Hyper-V Manager</span></span>

### <a name="prerequisites"></a><span data-ttu-id="88e3e-109">必要條件</span><span class="sxs-lookup"><span data-stu-id="88e3e-109">Prerequisites</span></span>
<span data-ttu-id="88e3e-110">本節假設您已經有取得 ISO 檔案的 hello Red Hat 網站，並已安裝的 hello RHEL 映像 tooa 虛擬硬碟 (VHD)。</span><span class="sxs-lookup"><span data-stu-id="88e3e-110">This section assumes that you have already obtained an ISO file from hello Red Hat website and installed hello RHEL image tooa virtual hard disk (VHD).</span></span> <span data-ttu-id="88e3e-111">如需有關如何 toouse HYPER-V 管理員 tooinstall 作業系統映像，請參閱[安裝 hello HYPER-V 角色和設定虛擬機器](http://technet.microsoft.com/library/hh846766.aspx)。</span><span class="sxs-lookup"><span data-stu-id="88e3e-111">For more details about how toouse Hyper-V Manager tooinstall an operating system image, see [Install hello Hyper-V Role and Configure a Virtual Machine](http://technet.microsoft.com/library/hh846766.aspx).</span></span>

<span data-ttu-id="88e3e-112">**RHEL 安裝注意事項**</span><span class="sxs-lookup"><span data-stu-id="88e3e-112">**RHEL installation notes**</span></span>

* <span data-ttu-id="88e3e-113">Azure 不支援 hello VHDX 格式。</span><span class="sxs-lookup"><span data-stu-id="88e3e-113">Azure does not support hello VHDX format.</span></span> <span data-ttu-id="88e3e-114">Azure 只支援固定 VHD。</span><span class="sxs-lookup"><span data-stu-id="88e3e-114">Azure supports only fixed VHD.</span></span> <span data-ttu-id="88e3e-115">您可以使用 HYPER-V 管理員 tooconvert hello 磁碟 tooVHD 格式，或您可以使用 hello convert-vhd 指令程式。</span><span class="sxs-lookup"><span data-stu-id="88e3e-115">You can use Hyper-V Manager tooconvert hello disk tooVHD format, or you can use hello convert-vhd cmdlet.</span></span> <span data-ttu-id="88e3e-116">如果您使用 VirtualBox，選取**固定大小**相對於的 toohello 預設建立 hello 磁碟時，動態配置選項。</span><span class="sxs-lookup"><span data-stu-id="88e3e-116">If you use VirtualBox, select **Fixed size** as opposed toohello default dynamically allocated option when you create hello disk.</span></span>
* <span data-ttu-id="88e3e-117">Azure 僅支援第 1 代虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="88e3e-117">Azure supports only generation 1 virtual machines.</span></span> <span data-ttu-id="88e3e-118">您可以將第 1 代虛擬機器從 VHDX toohello VHD 檔案格式與動態擴充 tooa 固定大小磁碟。</span><span class="sxs-lookup"><span data-stu-id="88e3e-118">You can convert a generation 1 virtual machine from VHDX toohello VHD file format and from dynamically expanding tooa fixed-size disk.</span></span> <span data-ttu-id="88e3e-119">您無法變更虛擬機器的世代。</span><span class="sxs-lookup"><span data-stu-id="88e3e-119">You can't change a virtual machine's generation.</span></span> <span data-ttu-id="88e3e-120">如需詳細資訊，請參閱[應該在 Hyper-V 中建立第 1 代還是第 2 代的虛擬機器？](https://technet.microsoft.com/windows-server-docs/compute/hyper-v/plan/should-i-create-a-generation-1-or-2-virtual-machine-in-hyper-v)。</span><span class="sxs-lookup"><span data-stu-id="88e3e-120">For more information, see [Should I create a generation 1 or 2 virtual machine in Hyper-V?](https://technet.microsoft.com/windows-server-docs/compute/hyper-v/plan/should-i-create-a-generation-1-or-2-virtual-machine-in-hyper-v).</span></span>
* <span data-ttu-id="88e3e-121">hello hello VHD 允許的最大大小為 1023 GB。</span><span class="sxs-lookup"><span data-stu-id="88e3e-121">hello maximum size that's allowed for hello VHD is 1,023 GB.</span></span>
* <span data-ttu-id="88e3e-122">當您安裝 Linux 作業系統 hello 時，我們建議您使用標準的資料分割，而不是邏輯磁碟區管理員 (LVM) 通常會是 hello 許多安裝的預設值。</span><span class="sxs-lookup"><span data-stu-id="88e3e-122">When you install hello Linux operating system, we recommend that you use standard partitions rather than Logical Volume Manager (LVM), which is often hello default for many installations.</span></span> <span data-ttu-id="88e3e-123">此種做法可以避免 LVM 與複製的虛擬機器的名稱衝突，特別是如果您需要 tooattach 作業系統磁碟 tooanother 相同的虛擬機器進行疑難排解。</span><span class="sxs-lookup"><span data-stu-id="88e3e-123">This practice will avoid LVM name conflicts with cloned virtual machines, particularly if you ever need tooattach an operating system disk tooanother identical virtual machine for troubleshooting.</span></span> <span data-ttu-id="88e3e-124">如果願意，您可以在資料磁碟上使用 [LVM](configure-raid.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) 或 [RAID](configure-lvm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="88e3e-124">[LVM](configure-lvm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) or [RAID](configure-raid.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) may be used on data disks.</span></span>
* <span data-ttu-id="88e3e-125">需要掛接通用磁碟格式 (UDF) 檔案系統的核心支援。</span><span class="sxs-lookup"><span data-stu-id="88e3e-125">Kernel support for mounting Universal Disk Format (UDF) file systems is required.</span></span> <span data-ttu-id="88e3e-126">在 Azure，hello UDF 格式化的媒體上的第一個開機附加的 toohello 客體會將佈建組態 toohello hello Linux 虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="88e3e-126">At first boot on Azure, hello UDF-formatted media that is attached toohello guest passes hello provisioning configuration toohello Linux virtual machine.</span></span> <span data-ttu-id="88e3e-127">hello Azure Linux 代理程式必須能夠 toomount hello UDF 檔案系統 tooread 其組態和佈建 hello 虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="88e3e-127">hello Azure Linux Agent must be able toomount hello UDF file system tooread its configuration and provision hello virtual machine.</span></span>
* <span data-ttu-id="88e3e-128">早於 2.6.37 hello Linux 核心版本不支援非統一記憶體存取 (NUMA) 在 HYPER-V 上具有較大的虛擬機器大小。</span><span class="sxs-lookup"><span data-stu-id="88e3e-128">Versions of hello Linux kernel that are earlier than 2.6.37 do not support non-uniform memory access (NUMA) on Hyper-V with larger virtual machine sizes.</span></span> <span data-ttu-id="88e3e-129">這個問題主要會影響用於 hello 上游的舊發佈 Red Hat 2.6.32 核心及已修正 RHEL 6.6 (核心-2.6.32-504) 中。</span><span class="sxs-lookup"><span data-stu-id="88e3e-129">This issue primarily impacts older distributions that use hello upstream Red Hat 2.6.32 kernel and was fixed in RHEL 6.6 (kernel-2.6.32-504).</span></span> <span data-ttu-id="88e3e-130">執行自訂的核心系統中，已經超過 2.6.37 或早於 2.6.32-504 RHEL 基礎核心必須設定 hello `numa=off` grub.conf hello 核心命令列啟動參數。</span><span class="sxs-lookup"><span data-stu-id="88e3e-130">Systems that run custom kernels that are older than 2.6.37 or RHEL-based kernels that are older than 2.6.32-504 must set hello `numa=off` boot parameter on hello kernel command line in grub.conf.</span></span> <span data-ttu-id="88e3e-131">如需詳細資訊，請參閱 Red Hat [KB 436883](https://access.redhat.com/solutions/436883)。</span><span class="sxs-lookup"><span data-stu-id="88e3e-131">For more information, see Red Hat [KB 436883](https://access.redhat.com/solutions/436883).</span></span>
* <span data-ttu-id="88e3e-132">Hello 作業系統磁碟上未設定交換資料分割。</span><span class="sxs-lookup"><span data-stu-id="88e3e-132">Do not configure a swap partition on hello operating system disk.</span></span> <span data-ttu-id="88e3e-133">hello Linux 代理程式可以設定的 toocreate 交換磁碟上的檔案 hello 暫存資源。</span><span class="sxs-lookup"><span data-stu-id="88e3e-133">hello Linux Agent can be configured toocreate a swap file on hello temporary resource disk.</span></span>  <span data-ttu-id="88e3e-134">在下列步驟的 hello 找相關資訊。</span><span class="sxs-lookup"><span data-stu-id="88e3e-134">More information about this can be found in hello following steps.</span></span>
* <span data-ttu-id="88e3e-135">所有 VHD 的大小都必須是 1 MB 的倍數。</span><span class="sxs-lookup"><span data-stu-id="88e3e-135">All VHDs must have sizes that are multiples of 1 MB.</span></span>

### <a name="prepare-a-rhel-6-virtual-machine-from-hyper-v-manager"></a><span data-ttu-id="88e3e-136">從 Hyper-V 管理員準備 RHEL 6 虛擬機器</span><span class="sxs-lookup"><span data-stu-id="88e3e-136">Prepare a RHEL 6 virtual machine from Hyper-V Manager</span></span>

1. <span data-ttu-id="88e3e-137">在 HYPER-V 管理員 中，選取 hello 虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="88e3e-137">In Hyper-V Manager, select hello virtual machine.</span></span>

2. <span data-ttu-id="88e3e-138">按一下**連接**tooopen hello 虛擬機器的主控台視窗。</span><span class="sxs-lookup"><span data-stu-id="88e3e-138">Click **Connect** tooopen a console window for hello virtual machine.</span></span>

3. <span data-ttu-id="88e3e-139">RHEL 6 NetworkManager 可能會干擾 hello Azure Linux 代理程式。</span><span class="sxs-lookup"><span data-stu-id="88e3e-139">In RHEL 6, NetworkManager can interfere with hello Azure Linux agent.</span></span> <span data-ttu-id="88e3e-140">解除安裝此套件，藉由執行下列命令的 hello:</span><span class="sxs-lookup"><span data-stu-id="88e3e-140">Uninstall this package by running hello following command:</span></span>
   
        # sudo rpm -e --nodeps NetworkManager

4. <span data-ttu-id="88e3e-141">建立或編輯 hello`/etc/sysconfig/network`檔並加入下列文字的 hello:</span><span class="sxs-lookup"><span data-stu-id="88e3e-141">Create or edit hello `/etc/sysconfig/network` file, and add hello following text:</span></span>
   
        NETWORKING=yes
        HOSTNAME=localhost.localdomain

5. <span data-ttu-id="88e3e-142">建立或編輯 hello`/etc/sysconfig/network-scripts/ifcfg-eth0`檔並加入下列文字的 hello:</span><span class="sxs-lookup"><span data-stu-id="88e3e-142">Create or edit hello `/etc/sysconfig/network-scripts/ifcfg-eth0` file, and add hello following text:</span></span>
   
        DEVICE=eth0
        ONBOOT=yes
        BOOTPROTO=dhcp
        TYPE=Ethernet
        USERCTL=no
        PEERDNS=yes
        IPV6INIT=no

6. <span data-ttu-id="88e3e-143">移動 （或移除） hello udev 規則 tooavoid 產生 hello 乙太網路介面的靜態規則。</span><span class="sxs-lookup"><span data-stu-id="88e3e-143">Move (or remove) hello udev rules tooavoid generating static rules for hello Ethernet interface.</span></span> <span data-ttu-id="88e3e-144">在 Microsoft Azure 或 Hyper-V 中複製虛擬機器時，這些規則會造成問題：</span><span class="sxs-lookup"><span data-stu-id="88e3e-144">These rules cause problems when you clone a virtual machine in Microsoft Azure or Hyper-V:</span></span>

        # sudo ln -s /dev/null /etc/udev/rules.d/75-persistent-net-generator.rules
        
        # sudo rm -f /etc/udev/rules.d/70-persistent-net.rules

7. <span data-ttu-id="88e3e-145">請確定 hello 網路服務，將會執行下列命令的 hello 在開機時啟動：</span><span class="sxs-lookup"><span data-stu-id="88e3e-145">Ensure that hello network service will start at boot time by running hello following command:</span></span>

        # sudo chkconfig network on

8. <span data-ttu-id="88e3e-146">藉由執行下列命令的 hello 註冊封裝 hello RHEL 儲存機制從 Red Hat 訂用帳戶 tooenable hello 的安裝：</span><span class="sxs-lookup"><span data-stu-id="88e3e-146">Register your Red Hat subscription tooenable hello installation of packages from hello RHEL repository by running hello following command:</span></span>

        # sudo subscription-manager register --auto-attach --username=XXX --password=XXX

9. <span data-ttu-id="88e3e-147">hello WALinuxAgent 封裝， `WALinuxAgent-<version>`，已排除 toohello Red Hat 額外項目儲存機制。</span><span class="sxs-lookup"><span data-stu-id="88e3e-147">hello WALinuxAgent package, `WALinuxAgent-<version>`, has been pushed toohello Red Hat extras repository.</span></span> <span data-ttu-id="88e3e-148">執行下列命令的 hello 啟用 hello 額外項目儲存機制：</span><span class="sxs-lookup"><span data-stu-id="88e3e-148">Enable hello extras repository by running hello following command:</span></span>

        # subscription-manager repos --enable=rhel-6-server-extras-rpms

10. <span data-ttu-id="88e3e-149">修改 Azure hello 核心開機行幼蟲組態 tooinclude 其他核心參數中。</span><span class="sxs-lookup"><span data-stu-id="88e3e-149">Modify hello kernel boot line in your grub configuration tooinclude additional kernel parameters for Azure.</span></span> <span data-ttu-id="88e3e-150">toodo 這項修改，開啟`/boot/grub/menu.lst`在文字編輯器中，並確認該 hello 預設核心中包含下列參數的 hello:</span><span class="sxs-lookup"><span data-stu-id="88e3e-150">toodo this modification, open `/boot/grub/menu.lst` in a text editor, and ensure that hello default kernel includes hello following parameters:</span></span>
    
        console=ttyS0 earlyprintk=ttyS0 rootdelay=300
    
    <span data-ttu-id="88e3e-151">這也可確保所有主控台會將訊息都傳送 toohello 第一個序列連接埠，這可協助 Azure 偵錯問題的支援。</span><span class="sxs-lookup"><span data-stu-id="88e3e-151">This will also ensure that all console messages are sent toohello first serial port, which can assist Azure support with debugging issues.</span></span>
    
    <span data-ttu-id="88e3e-152">此外，我們建議您先移除 hello 下列參數：</span><span class="sxs-lookup"><span data-stu-id="88e3e-152">In addition, we recommended that you remove hello following parameters:</span></span>
    
        rhgb quiet crashkernel=auto
    
    <span data-ttu-id="88e3e-153">沒有適用於雲端環境，我們想要傳送 toohello 序列連接埠的所有 hello 記錄 toobe 圖形和無訊息的開機。</span><span class="sxs-lookup"><span data-stu-id="88e3e-153">Graphical and quiet boot are not useful in a cloud environment where we want all hello logs toobe sent toohello serial port.</span></span>  <span data-ttu-id="88e3e-154">您可以保留 hello`crashkernel`視設定選項。</span><span class="sxs-lookup"><span data-stu-id="88e3e-154">You can leave hello `crashkernel` option configured if desired.</span></span> <span data-ttu-id="88e3e-155">請注意，此參數可減少 hello hello 128 MB 以上的虛擬機器中的可用記憶體數量。</span><span class="sxs-lookup"><span data-stu-id="88e3e-155">Note that this parameter reduces hello amount of available memory in hello virtual machine by 128 MB or more.</span></span> <span data-ttu-id="88e3e-156">此組態可能會對小型虛擬機器造成問題。</span><span class="sxs-lookup"><span data-stu-id="88e3e-156">This configuration might be problematic on smaller virtual machine sizes.</span></span>

    >[!Important]
    <span data-ttu-id="88e3e-157">RHEL 6.5 及更早版本也必須設定 hello`numa=off`核心參數。</span><span class="sxs-lookup"><span data-stu-id="88e3e-157">RHEL 6.5 and earlier must also set hello `numa=off` kernel parameter.</span></span> <span data-ttu-id="88e3e-158">請參閱 Red Hat [KB 436883](https://access.redhat.com/solutions/436883)。</span><span class="sxs-lookup"><span data-stu-id="88e3e-158">See Red Hat [KB 436883](https://access.redhat.com/solutions/436883).</span></span>

11. <span data-ttu-id="88e3e-159">請確定該 hello 安全殼層 (SSH) 伺服器安裝，並在開機時，通常是 hello 預設設定 toostart。</span><span class="sxs-lookup"><span data-stu-id="88e3e-159">Ensure that hello secure shell (SSH) server is installed and configured toostart at boot time, which is usually hello default.</span></span> <span data-ttu-id="88e3e-160">修改下列行 /etc/ssh/sshd_config tooinclude hello:</span><span class="sxs-lookup"><span data-stu-id="88e3e-160">Modify /etc/ssh/sshd_config tooinclude hello following line:</span></span>

        ClientAliveInterval 180

12. <span data-ttu-id="88e3e-161">執行下列命令的 hello 安裝 hello Azure Linux 代理程式：</span><span class="sxs-lookup"><span data-stu-id="88e3e-161">Install hello Azure Linux Agent by running hello following command:</span></span>

        # sudo yum install WALinuxAgent

        # sudo chkconfig waagent on

    <span data-ttu-id="88e3e-162">安裝 hello WALinuxAgent 套件移除 hello NetworkManager 和 NetworkManager gnome 封裝，如果在步驟 3 中沒有已移除。</span><span class="sxs-lookup"><span data-stu-id="88e3e-162">Installing hello WALinuxAgent package removes hello NetworkManager and NetworkManager-gnome packages if they were not already removed in step 3.</span></span>

13. <span data-ttu-id="88e3e-163">不要在 hello 作業系統磁碟上建立的交換空間。</span><span class="sxs-lookup"><span data-stu-id="88e3e-163">Do not create swap space on hello operating system disk.</span></span>

    <span data-ttu-id="88e3e-164">hello Azure Linux 代理程式可以自動使用 hello 本機資源磁碟附加的 toohello 虛擬機器之後，在 Azure 上佈建 hello 虛擬機器所設定交換空間。</span><span class="sxs-lookup"><span data-stu-id="88e3e-164">hello Azure Linux Agent can automatically configure swap space by using hello local resource disk that is attached toohello virtual machine after hello virtual machine is provisioned on Azure.</span></span> <span data-ttu-id="88e3e-165">請注意該本機資源磁碟是暫存磁碟和 hello 虛擬機器會解除佈建時，可能會清空其 hello。</span><span class="sxs-lookup"><span data-stu-id="88e3e-165">Note that hello local resource disk is a temporary disk and that it might be emptied when hello virtual machine is deprovisioned.</span></span> <span data-ttu-id="88e3e-166">Hello 上一個步驟中安裝 hello Azure Linux 代理程式之後，修改適當地遵循 /etc/waagent.conf 中的參數的 hello:</span><span class="sxs-lookup"><span data-stu-id="88e3e-166">After you install hello Azure Linux Agent in hello previous step, modify hello following parameters in /etc/waagent.conf appropriately:</span></span>

        ResourceDisk.Format=y
        ResourceDisk.Filesystem=ext4
        ResourceDisk.MountPoint=/mnt/resource
        ResourceDisk.EnableSwap=y
        ResourceDisk.SwapSizeMB=2048    ## NOTE: set this toowhatever you need it toobe.

14. <span data-ttu-id="88e3e-167">取消註冊 hello 訂用帳戶 （如有必要） 藉由執行下列命令的 hello:</span><span class="sxs-lookup"><span data-stu-id="88e3e-167">Unregister hello subscription (if necessary) by running hello following command:</span></span>

        # sudo subscription-manager unregister

15. <span data-ttu-id="88e3e-168">執行下列命令 toodeprovision hello 虛擬機器的 hello 並準備在 Azure 上佈建：</span><span class="sxs-lookup"><span data-stu-id="88e3e-168">Run hello following commands toodeprovision hello virtual machine and prepare it for provisioning on Azure:</span></span>

        # sudo waagent -force -deprovision

        # export HISTSIZE=0

        # logout

16. <span data-ttu-id="88e3e-169">在 Hyper-V 管理員中，按一下 [動作] > [關閉]。</span><span class="sxs-lookup"><span data-stu-id="88e3e-169">Click **Action** > **Shut Down** in Hyper-V Manager.</span></span> <span data-ttu-id="88e3e-170">Linux VHD 是現在準備好 toobe 上傳 tooAzure。</span><span class="sxs-lookup"><span data-stu-id="88e3e-170">Your Linux VHD is now ready toobe uploaded tooAzure.</span></span>


### <a name="prepare-a-rhel-7-virtual-machine-from-hyper-v-manager"></a><span data-ttu-id="88e3e-171">從 Hyper-V 管理員準備 RHEL 7 虛擬機器</span><span class="sxs-lookup"><span data-stu-id="88e3e-171">Prepare a RHEL 7 virtual machine from Hyper-V Manager</span></span>

1. <span data-ttu-id="88e3e-172">在 HYPER-V 管理員 中，選取 hello 虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="88e3e-172">In Hyper-V Manager, select hello virtual machine.</span></span>

2. <span data-ttu-id="88e3e-173">按一下**連接**tooopen hello 虛擬機器的主控台視窗。</span><span class="sxs-lookup"><span data-stu-id="88e3e-173">Click **Connect** tooopen a console window for hello virtual machine.</span></span>

3. <span data-ttu-id="88e3e-174">建立或編輯 hello`/etc/sysconfig/network`檔並加入下列文字的 hello:</span><span class="sxs-lookup"><span data-stu-id="88e3e-174">Create or edit hello `/etc/sysconfig/network` file, and add hello following text:</span></span>
   
        NETWORKING=yes
        HOSTNAME=localhost.localdomain

4. <span data-ttu-id="88e3e-175">建立或編輯 hello`/etc/sysconfig/network-scripts/ifcfg-eth0`檔並加入下列文字的 hello:</span><span class="sxs-lookup"><span data-stu-id="88e3e-175">Create or edit hello `/etc/sysconfig/network-scripts/ifcfg-eth0` file, and add hello following text:</span></span>
   
        DEVICE=eth0
        ONBOOT=yes
        BOOTPROTO=dhcp
        TYPE=Ethernet
        USERCTL=no
        PEERDNS=yes
        IPV6INIT=no
        NM_CONTROLLED=no

5. <span data-ttu-id="88e3e-176">請確定 hello 網路服務，將會執行下列命令的 hello 在開機時啟動：</span><span class="sxs-lookup"><span data-stu-id="88e3e-176">Ensure that hello network service will start at boot time by running hello following command:</span></span>

        # sudo chkconfig network on

6. <span data-ttu-id="88e3e-177">藉由執行下列命令的 hello 註冊封裝 hello RHEL 儲存機制從 Red Hat 訂用帳戶 tooenable hello 的安裝：</span><span class="sxs-lookup"><span data-stu-id="88e3e-177">Register your Red Hat subscription tooenable hello installation of packages from hello RHEL repository by running hello following command:</span></span>

        # sudo subscription-manager register --auto-attach --username=XXX --password=XXX

7. <span data-ttu-id="88e3e-178">修改 Azure hello 核心開機行幼蟲組態 tooinclude 其他核心參數中。</span><span class="sxs-lookup"><span data-stu-id="88e3e-178">Modify hello kernel boot line in your grub configuration tooinclude additional kernel parameters for Azure.</span></span> <span data-ttu-id="88e3e-179">toodo 這項修改，開啟`/etc/default/grub`在文字編輯器，編輯 hello`GRUB_CMDLINE_LINUX`參數。</span><span class="sxs-lookup"><span data-stu-id="88e3e-179">toodo this modification, open `/etc/default/grub` in a text editor, and edit hello `GRUB_CMDLINE_LINUX` parameter.</span></span> <span data-ttu-id="88e3e-180">例如：</span><span class="sxs-lookup"><span data-stu-id="88e3e-180">For example:</span></span>
   
        GRUB_CMDLINE_LINUX="rootdelay=300 console=ttyS0 earlyprintk=ttyS0 net.ifnames=0"
   
   <span data-ttu-id="88e3e-181">這也可確保所有主控台會將訊息都傳送 toohello 第一個序列連接埠，這可協助 Azure 偵錯問題的支援。</span><span class="sxs-lookup"><span data-stu-id="88e3e-181">This will also ensure that all console messages are sent toohello first serial port, which can assist Azure support with debugging issues.</span></span> <span data-ttu-id="88e3e-182">這項設定也會關閉 hello 新增 RHEL 7 命名慣例的 Nic。</span><span class="sxs-lookup"><span data-stu-id="88e3e-182">This configuration also turns off hello new RHEL 7 naming conventions for NICs.</span></span> <span data-ttu-id="88e3e-183">此外，我們建議您移除 hello 下列參數：</span><span class="sxs-lookup"><span data-stu-id="88e3e-183">In addition, we recommend that you remove hello following parameters:</span></span>
   
        rhgb quiet crashkernel=auto
   
    <span data-ttu-id="88e3e-184">沒有適用於雲端環境，我們想要傳送 toohello 序列連接埠的所有 hello 記錄 toobe 圖形和無訊息的開機。</span><span class="sxs-lookup"><span data-stu-id="88e3e-184">Graphical and quiet boot are not useful in a cloud environment where we want all hello logs toobe sent toohello serial port.</span></span> <span data-ttu-id="88e3e-185">您可以保留 hello`crashkernel`視設定選項。</span><span class="sxs-lookup"><span data-stu-id="88e3e-185">You can leave hello `crashkernel` option configured if desired.</span></span> <span data-ttu-id="88e3e-186">請注意，此參數減少 hello 128 MB 以上，hello 虛擬機器中的可用記憶體的數量可能較小的虛擬機器大小會造成問題。</span><span class="sxs-lookup"><span data-stu-id="88e3e-186">Note that this parameter reduces hello amount of available memory in hello virtual machine by 128 MB or more, which might be problematic on smaller virtual machine sizes.</span></span>

8. <span data-ttu-id="88e3e-187">完成之後編輯`/etc/default/grub`，請執行 hello 命令 toorebuild hello 幼蟲設定下列：</span><span class="sxs-lookup"><span data-stu-id="88e3e-187">After you are done editing `/etc/default/grub`, run hello following command toorebuild hello grub configuration:</span></span>

        # sudo grub2-mkconfig -o /boot/grub2/grub.cfg

9. <span data-ttu-id="88e3e-188">請確定該 hello SSH 伺服器安裝，並在開機時，通常是 hello 預設設定 toostart。</span><span class="sxs-lookup"><span data-stu-id="88e3e-188">Ensure that hello SSH server is installed and configured toostart at boot time, which is usually hello default.</span></span> <span data-ttu-id="88e3e-189">修改`/etc/ssh/sshd_config`tooinclude hello 下列行：</span><span class="sxs-lookup"><span data-stu-id="88e3e-189">Modify `/etc/ssh/sshd_config` tooinclude hello following line:</span></span>

        ClientAliveInterval 180

10. <span data-ttu-id="88e3e-190">hello WALinuxAgent 封裝， `WALinuxAgent-<version>`，已排除 toohello Red Hat 額外項目儲存機制。</span><span class="sxs-lookup"><span data-stu-id="88e3e-190">hello WALinuxAgent package, `WALinuxAgent-<version>`, has been pushed toohello Red Hat extras repository.</span></span> <span data-ttu-id="88e3e-191">執行下列命令的 hello 啟用 hello 額外項目儲存機制：</span><span class="sxs-lookup"><span data-stu-id="88e3e-191">Enable hello extras repository by running hello following command:</span></span>

        # subscription-manager repos --enable=rhel-7-server-extras-rpms

11. <span data-ttu-id="88e3e-192">執行下列命令的 hello 安裝 hello Azure Linux 代理程式：</span><span class="sxs-lookup"><span data-stu-id="88e3e-192">Install hello Azure Linux Agent by running hello following command:</span></span>

        # sudo yum install WALinuxAgent

        # sudo systemctl enable waagent.service

12. <span data-ttu-id="88e3e-193">不要在 hello 作業系統磁碟上建立的交換空間。</span><span class="sxs-lookup"><span data-stu-id="88e3e-193">Do not create swap space on hello operating system disk.</span></span>

    <span data-ttu-id="88e3e-194">hello Azure Linux 代理程式可以自動使用 hello 本機資源磁碟附加的 toohello 虛擬機器之後，在 Azure 上佈建 hello 虛擬機器所設定交換空間。</span><span class="sxs-lookup"><span data-stu-id="88e3e-194">hello Azure Linux Agent can automatically configure swap space by using hello local resource disk that is attached toohello virtual machine after hello virtual machine is provisioned on Azure.</span></span> <span data-ttu-id="88e3e-195">請注意，hello 本機資源磁碟是暫存磁碟，它可能會取消佈建 hello 虛擬機器時清空。</span><span class="sxs-lookup"><span data-stu-id="88e3e-195">Note that hello local resource disk is a temporary disk, and it might be emptied when hello virtual machine is deprovisioned.</span></span> <span data-ttu-id="88e3e-196">Hello 上一個步驟中安裝 hello Azure Linux 代理程式之後，修改下列參數中的 hello`/etc/waagent.conf`適當地：</span><span class="sxs-lookup"><span data-stu-id="88e3e-196">After you install hello Azure Linux Agent in hello previous step, modify hello following parameters in `/etc/waagent.conf` appropriately:</span></span>

        ResourceDisk.Format=y
        ResourceDisk.Filesystem=ext4
        ResourceDisk.MountPoint=/mnt/resource
        ResourceDisk.EnableSwap=y
        ResourceDisk.SwapSizeMB=2048    ## NOTE: set this toowhatever you need it toobe.

13. <span data-ttu-id="88e3e-197">如果您想 toounregister hello 訂用帳戶，執行下列命令的 hello:</span><span class="sxs-lookup"><span data-stu-id="88e3e-197">If you want toounregister hello subscription, run hello following command:</span></span>

        # sudo subscription-manager unregister

14. <span data-ttu-id="88e3e-198">執行下列命令 toodeprovision hello 虛擬機器的 hello 並準備在 Azure 上佈建：</span><span class="sxs-lookup"><span data-stu-id="88e3e-198">Run hello following commands toodeprovision hello virtual machine and prepare it for provisioning on Azure:</span></span>

        # sudo waagent -force -deprovision

        # export HISTSIZE=0

        # logout

15. <span data-ttu-id="88e3e-199">在 Hyper-V 管理員中，按一下 [動作] > [關閉]。</span><span class="sxs-lookup"><span data-stu-id="88e3e-199">Click **Action** > **Shut Down** in Hyper-V Manager.</span></span> <span data-ttu-id="88e3e-200">Linux VHD 是現在準備好 toobe 上傳 tooAzure。</span><span class="sxs-lookup"><span data-stu-id="88e3e-200">Your Linux VHD is now ready toobe uploaded tooAzure.</span></span>


## <a name="prepare-a-red-hat-based-virtual-machine-from-kvm"></a><span data-ttu-id="88e3e-201">從 KVM 準備 Red Hat 型虛擬機器</span><span class="sxs-lookup"><span data-stu-id="88e3e-201">Prepare a Red Hat-based virtual machine from KVM</span></span>
### <a name="prepare-a-rhel-6-virtual-machine-from-kvm"></a><span data-ttu-id="88e3e-202">從 KVM 準備 RHEL 6 虛擬機器</span><span class="sxs-lookup"><span data-stu-id="88e3e-202">Prepare a RHEL 6 virtual machine from KVM</span></span>

1. <span data-ttu-id="88e3e-203">Hello Red Hat 網站下載 RHEL 6 hello KVM 映的像。</span><span class="sxs-lookup"><span data-stu-id="88e3e-203">Download hello KVM image of RHEL 6 from hello Red Hat website.</span></span>

2. <span data-ttu-id="88e3e-204">設定根密碼。</span><span class="sxs-lookup"><span data-stu-id="88e3e-204">Set a root password.</span></span>

    <span data-ttu-id="88e3e-205">產生加密的密碼，並將複製 hello hello 命令輸出：</span><span class="sxs-lookup"><span data-stu-id="88e3e-205">Generate an encrypted password, and copy hello output of hello command:</span></span>

        # openssl passwd -1 changeme

    <span data-ttu-id="88e3e-206">使用 guestfish 設定根密碼：</span><span class="sxs-lookup"><span data-stu-id="88e3e-206">Set a root password with guestfish:</span></span>
        
        # guestfish --rw -a <image-name>
        > <fs> run
        > <fs> list-filesystems
        > <fs> mount /dev/sda1 /
        > <fs> vi /etc/shadow
        > <fs> exit

   <span data-ttu-id="88e3e-207">變更 hello 第二個欄位的 hello 根使用者從 「!!"</span><span class="sxs-lookup"><span data-stu-id="88e3e-207">Change hello second field of hello root user from "!!"</span></span> <span data-ttu-id="88e3e-208">toohello 加密的密碼。</span><span class="sxs-lookup"><span data-stu-id="88e3e-208">toohello encrypted password.</span></span>

3. <span data-ttu-id="88e3e-209">KVM 中建立虛擬機器，從 hello qcow2 映像。</span><span class="sxs-lookup"><span data-stu-id="88e3e-209">Create a virtual machine in KVM from hello qcow2 image.</span></span> <span data-ttu-id="88e3e-210">設定得 hello 磁碟類型**qcow2**，並設定 hello 虛擬網路介面裝置型號太**virtio**。</span><span class="sxs-lookup"><span data-stu-id="88e3e-210">Set hello disk type too**qcow2**, and set hello virtual network interface device model too**virtio**.</span></span> <span data-ttu-id="88e3e-211">然後，啟動 hello 虛擬機器，並為根登入。</span><span class="sxs-lookup"><span data-stu-id="88e3e-211">Then, start hello virtual machine, and sign in as root.</span></span>

4. <span data-ttu-id="88e3e-212">建立或編輯 hello`/etc/sysconfig/network`檔並加入下列文字的 hello:</span><span class="sxs-lookup"><span data-stu-id="88e3e-212">Create or edit hello `/etc/sysconfig/network` file, and add hello following text:</span></span>
   
        NETWORKING=yes
        HOSTNAME=localhost.localdomain

5. <span data-ttu-id="88e3e-213">建立或編輯 hello`/etc/sysconfig/network-scripts/ifcfg-eth0`檔並加入下列文字的 hello:</span><span class="sxs-lookup"><span data-stu-id="88e3e-213">Create or edit hello `/etc/sysconfig/network-scripts/ifcfg-eth0` file, and add hello following text:</span></span>
   
        DEVICE=eth0
        ONBOOT=yes
        BOOTPROTO=dhcp
        TYPE=Ethernet
        USERCTL=no
        PEERDNS=yes
        IPV6INIT=no

6. <span data-ttu-id="88e3e-214">移動 （或移除） hello udev 規則 tooavoid 產生 hello 乙太網路介面的靜態規則。</span><span class="sxs-lookup"><span data-stu-id="88e3e-214">Move (or remove) hello udev rules tooavoid generating static rules for hello Ethernet interface.</span></span> <span data-ttu-id="88e3e-215">在 Azure 或 Hyper-V 中複製虛擬機器時，這些規則會造成問題：</span><span class="sxs-lookup"><span data-stu-id="88e3e-215">These rules cause problems when you clone a virtual machine in Azure or Hyper-V:</span></span>

        # sudo ln -s /dev/null /etc/udev/rules.d/75-persistent-net-generator.rules

        # sudo rm -f /etc/udev/rules.d/70-persistent-net.rules

7. <span data-ttu-id="88e3e-216">請確定 hello 網路服務，將會執行下列命令的 hello 在開機時啟動：</span><span class="sxs-lookup"><span data-stu-id="88e3e-216">Ensure that hello network service will start at boot time by running hello following command:</span></span>

        # chkconfig network on

8. <span data-ttu-id="88e3e-217">藉由執行下列命令的 hello 註冊封裝 hello RHEL 儲存機制從 Red Hat 訂用帳戶 tooenable hello 的安裝：</span><span class="sxs-lookup"><span data-stu-id="88e3e-217">Register your Red Hat subscription tooenable hello installation of packages from hello RHEL repository by running hello following command:</span></span>

        # subscription-manager register --auto-attach --username=XXX --password=XXX

9. <span data-ttu-id="88e3e-218">修改 Azure hello 核心開機行幼蟲組態 tooinclude 其他核心參數中。</span><span class="sxs-lookup"><span data-stu-id="88e3e-218">Modify hello kernel boot line in your grub configuration tooinclude additional kernel parameters for Azure.</span></span> <span data-ttu-id="88e3e-219">toodo 此設定，請開啟`/boot/grub/menu.lst`在文字編輯器中，並確認該 hello 預設核心中包含下列參數的 hello:</span><span class="sxs-lookup"><span data-stu-id="88e3e-219">toodo this configuration, open `/boot/grub/menu.lst` in a text editor, and ensure that hello default kernel includes hello following parameters:</span></span>
    
        console=ttyS0 earlyprintk=ttyS0 rootdelay=300
    
    <span data-ttu-id="88e3e-220">這也可確保所有主控台會將訊息都傳送 toohello 第一個序列連接埠，這可協助 Azure 偵錯問題的支援。</span><span class="sxs-lookup"><span data-stu-id="88e3e-220">This will also ensure that all console messages are sent toohello first serial port, which can assist Azure support with debugging issues.</span></span>
    
    <span data-ttu-id="88e3e-221">此外，我們建議您移除 hello 下列參數：</span><span class="sxs-lookup"><span data-stu-id="88e3e-221">In addition, we recommend that you remove hello following parameters:</span></span>
    
        rhgb quiet crashkernel=auto
    
    <span data-ttu-id="88e3e-222">沒有適用於雲端環境，我們想要傳送 toohello 序列連接埠的所有 hello 記錄 toobe 圖形和無訊息的開機。</span><span class="sxs-lookup"><span data-stu-id="88e3e-222">Graphical and quiet boot are not useful in a cloud environment where we want all hello logs toobe sent toohello serial port.</span></span> <span data-ttu-id="88e3e-223">您可以保留 hello`crashkernel`視設定選項。</span><span class="sxs-lookup"><span data-stu-id="88e3e-223">You can leave hello `crashkernel` option configured if desired.</span></span> <span data-ttu-id="88e3e-224">請注意，此參數減少 hello 128 MB 以上，hello 虛擬機器中的可用記憶體的數量可能較小的虛擬機器大小會造成問題。</span><span class="sxs-lookup"><span data-stu-id="88e3e-224">Note that this parameter reduces hello amount of available memory in hello virtual machine by 128 MB or more, which might be problematic on smaller virtual machine sizes.</span></span>

    >[!Important]
    <span data-ttu-id="88e3e-225">RHEL 6.5 及更早版本也必須設定 hello`numa=off`核心參數。</span><span class="sxs-lookup"><span data-stu-id="88e3e-225">RHEL 6.5 and earlier must also set hello `numa=off` kernel parameter.</span></span> <span data-ttu-id="88e3e-226">請參閱 Red Hat [KB 436883](https://access.redhat.com/solutions/436883)。</span><span class="sxs-lookup"><span data-stu-id="88e3e-226">See Red Hat [KB 436883](https://access.redhat.com/solutions/436883).</span></span>

10. <span data-ttu-id="88e3e-227">新增 HYPER-V 模組 tooinitramfs:</span><span class="sxs-lookup"><span data-stu-id="88e3e-227">Add Hyper-V modules tooinitramfs:</span></span>  

    <span data-ttu-id="88e3e-228">編輯`/etc/dracut.conf`，並加入下列內容的 hello:</span><span class="sxs-lookup"><span data-stu-id="88e3e-228">Edit `/etc/dracut.conf`, and add hello following content:</span></span>

        add_drivers+="hv_vmbus hv_netvsc hv_storvsc"

    <span data-ttu-id="88e3e-229">重建 initramfs：</span><span class="sxs-lookup"><span data-stu-id="88e3e-229">Rebuild initramfs:</span></span>

        # dracut -f -v

11. <span data-ttu-id="88e3e-230">解除安裝 cloud-init：</span><span class="sxs-lookup"><span data-stu-id="88e3e-230">Uninstall cloud-init:</span></span>

        # yum remove cloud-init

12. <span data-ttu-id="88e3e-231">請確定該 hello SSH 伺服器是在安裝並設定 toostart 開機時間：</span><span class="sxs-lookup"><span data-stu-id="88e3e-231">Ensure that hello SSH server is installed and configured toostart at boot time:</span></span>

        # chkconfig sshd on

    <span data-ttu-id="88e3e-232">修改下列行 /etc/ssh/sshd_config tooinclude hello:</span><span class="sxs-lookup"><span data-stu-id="88e3e-232">Modify /etc/ssh/sshd_config tooinclude hello following lines:</span></span>

        PasswordAuthentication yes
        ClientAliveInterval 180

13. <span data-ttu-id="88e3e-233">hello WALinuxAgent 封裝， `WALinuxAgent-<version>`，已排除 toohello Red Hat 額外項目儲存機制。</span><span class="sxs-lookup"><span data-stu-id="88e3e-233">hello WALinuxAgent package, `WALinuxAgent-<version>`, has been pushed toohello Red Hat extras repository.</span></span> <span data-ttu-id="88e3e-234">執行下列命令的 hello 啟用 hello 額外項目儲存機制：</span><span class="sxs-lookup"><span data-stu-id="88e3e-234">Enable hello extras repository by running hello following command:</span></span>

        # subscription-manager repos --enable=rhel-6-server-extras-rpms

14. <span data-ttu-id="88e3e-235">執行下列命令的 hello 安裝 hello Azure Linux 代理程式：</span><span class="sxs-lookup"><span data-stu-id="88e3e-235">Install hello Azure Linux Agent by running hello following command:</span></span>

        # yum install WALinuxAgent

        # chkconfig waagent on

15. <span data-ttu-id="88e3e-236">hello Azure Linux 代理程式可以自動使用 hello 本機資源磁碟附加的 toohello 虛擬機器之後，在 Azure 上佈建 hello 虛擬機器所設定交換空間。</span><span class="sxs-lookup"><span data-stu-id="88e3e-236">hello Azure Linux Agent can automatically configure swap space by using hello local resource disk that is attached toohello virtual machine after hello virtual machine is provisioned on Azure.</span></span> <span data-ttu-id="88e3e-237">請注意，hello 本機資源磁碟是暫存磁碟，它可能會取消佈建 hello 虛擬機器時清空。</span><span class="sxs-lookup"><span data-stu-id="88e3e-237">Note that hello local resource disk is a temporary disk, and it might be emptied when hello virtual machine is deprovisioned.</span></span> <span data-ttu-id="88e3e-238">Hello 上一個步驟中安裝 hello Azure Linux 代理程式之後，修改下列參數中的 hello **/etc/waagent.conf**適當地：</span><span class="sxs-lookup"><span data-stu-id="88e3e-238">After you install hello Azure Linux Agent in hello previous step, modify hello following parameters in **/etc/waagent.conf** appropriately:</span></span>

        ResourceDisk.Format=y
        ResourceDisk.Filesystem=ext4
        ResourceDisk.MountPoint=/mnt/resource
        ResourceDisk.EnableSwap=y
        ResourceDisk.SwapSizeMB=2048    ## NOTE: set this toowhatever you need it toobe.

16. <span data-ttu-id="88e3e-239">取消註冊 hello 訂用帳戶 （如有必要） 藉由執行下列命令的 hello:</span><span class="sxs-lookup"><span data-stu-id="88e3e-239">Unregister hello subscription (if necessary) by running hello following command:</span></span>

        # subscription-manager unregister

17. <span data-ttu-id="88e3e-240">執行下列命令 toodeprovision hello 虛擬機器的 hello 並準備在 Azure 上佈建：</span><span class="sxs-lookup"><span data-stu-id="88e3e-240">Run hello following commands toodeprovision hello virtual machine and prepare it for provisioning on Azure:</span></span>

        # waagent -force -deprovision

        # export HISTSIZE=0

        # logout

18. <span data-ttu-id="88e3e-241">關閉 hello KVM 中的虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="88e3e-241">Shut down hello virtual machine in KVM.</span></span>

19. <span data-ttu-id="88e3e-242">將 hello qcow2 映像 toohello VHD 格式的轉換。</span><span class="sxs-lookup"><span data-stu-id="88e3e-242">Convert hello qcow2 image toohello VHD format.</span></span>

    <span data-ttu-id="88e3e-243">第一次轉換 hello 影像 tooraw 格式：</span><span class="sxs-lookup"><span data-stu-id="88e3e-243">First convert hello image tooraw format:</span></span>

        # qemu-img convert -f qcow2 -O raw rhel-6.8.qcow2 rhel-6.8.raw

    <span data-ttu-id="88e3e-244">請確定 hello hello 原始影像大小配合 1 MB。</span><span class="sxs-lookup"><span data-stu-id="88e3e-244">Make sure that hello size of hello raw image is aligned with 1 MB.</span></span> <span data-ttu-id="88e3e-245">否則，無條件進位 hello 與 1 MB 的大小 tooalign:</span><span class="sxs-lookup"><span data-stu-id="88e3e-245">Otherwise, round up hello size tooalign with 1 MB:</span></span>

        # MB=$((1024*1024))
        # size=$(qemu-img info -f raw --output json "rhel-6.8.raw" | \
          gawk 'match($0, /"virtual-size": ([0-9]+),/, val) {print val[1]}')

        # rounded_size=$((($size/$MB + 1)*$MB))
        # qemu-img resize rhel-6.8.raw $rounded_size

    <span data-ttu-id="88e3e-246">轉換 hello 原始磁碟 tooa 固定大小的 VHD:</span><span class="sxs-lookup"><span data-stu-id="88e3e-246">Convert hello raw disk tooa fixed-sized VHD:</span></span>

        # qemu-img convert -f raw -o subformat=fixed -O vpc rhel-6.8.raw rhel-6.8.vhd


### <a name="prepare-a-rhel-7-virtual-machine-from-kvm"></a><span data-ttu-id="88e3e-247">從 KVM 準備 RHEL 7 虛擬機器</span><span class="sxs-lookup"><span data-stu-id="88e3e-247">Prepare a RHEL 7 virtual machine from KVM</span></span>

1. <span data-ttu-id="88e3e-248">Hello Red Hat 網站下載 RHEL 7 hello KVM 映的像。</span><span class="sxs-lookup"><span data-stu-id="88e3e-248">Download hello KVM image of RHEL 7 from hello Red Hat website.</span></span> <span data-ttu-id="88e3e-249">此程序使用 RHEL 7 hello 範例。</span><span class="sxs-lookup"><span data-stu-id="88e3e-249">This procedure uses RHEL 7 as hello example.</span></span>

2. <span data-ttu-id="88e3e-250">設定根密碼。</span><span class="sxs-lookup"><span data-stu-id="88e3e-250">Set a root password.</span></span>

    <span data-ttu-id="88e3e-251">產生加密的密碼，並將複製 hello hello 命令輸出：</span><span class="sxs-lookup"><span data-stu-id="88e3e-251">Generate an encrypted password, and copy hello output of hello command:</span></span>

        # openssl passwd -1 changeme

    <span data-ttu-id="88e3e-252">使用 guestfish 設定根密碼：</span><span class="sxs-lookup"><span data-stu-id="88e3e-252">Set a root password with guestfish:</span></span>

        # guestfish --rw -a <image-name>
        > <fs> run
        > <fs> list-filesystems
        > <fs> mount /dev/sda1 /
        > <fs> vi /etc/shadow
        > <fs> exit

   <span data-ttu-id="88e3e-253">變更 hello 第二個欄位的根使用者從 「!!"</span><span class="sxs-lookup"><span data-stu-id="88e3e-253">Change hello second field of root user from "!!"</span></span> <span data-ttu-id="88e3e-254">toohello 加密的密碼。</span><span class="sxs-lookup"><span data-stu-id="88e3e-254">toohello encrypted password.</span></span>

3. <span data-ttu-id="88e3e-255">KVM 中建立虛擬機器，從 hello qcow2 映像。</span><span class="sxs-lookup"><span data-stu-id="88e3e-255">Create a virtual machine in KVM from hello qcow2 image.</span></span> <span data-ttu-id="88e3e-256">設定得 hello 磁碟類型**qcow2**，並設定 hello 虛擬網路介面裝置型號太**virtio**。</span><span class="sxs-lookup"><span data-stu-id="88e3e-256">Set hello disk type too**qcow2**, and set hello virtual network interface device model too**virtio**.</span></span> <span data-ttu-id="88e3e-257">然後，啟動 hello 虛擬機器，並為根登入。</span><span class="sxs-lookup"><span data-stu-id="88e3e-257">Then, start hello virtual machine, and sign in as root.</span></span>

4. <span data-ttu-id="88e3e-258">建立或編輯 hello`/etc/sysconfig/network`檔並加入下列文字的 hello:</span><span class="sxs-lookup"><span data-stu-id="88e3e-258">Create or edit hello `/etc/sysconfig/network` file, and add hello following text:</span></span>
   
        NETWORKING=yes
        HOSTNAME=localhost.localdomain

5. <span data-ttu-id="88e3e-259">建立或編輯 hello`/etc/sysconfig/network-scripts/ifcfg-eth0`檔並加入下列文字的 hello:</span><span class="sxs-lookup"><span data-stu-id="88e3e-259">Create or edit hello `/etc/sysconfig/network-scripts/ifcfg-eth0` file, and add hello following text:</span></span>
   
        DEVICE=eth0
        ONBOOT=yes
        BOOTPROTO=dhcp
        TYPE=Ethernet
        USERCTL=no
        PEERDNS=yes
        IPV6INIT=no
        NM_CONTROLLED=no

6. <span data-ttu-id="88e3e-260">請確定 hello 網路服務，將會執行下列命令的 hello 在開機時啟動：</span><span class="sxs-lookup"><span data-stu-id="88e3e-260">Ensure that hello network service will start at boot time by running hello following command:</span></span>

        # chkconfig network on

7. <span data-ttu-id="88e3e-261">藉由執行下列命令的 hello 註冊封裝從 hello RHEL 儲存機制的 Red Hat 訂用帳戶 tooenable 安裝：</span><span class="sxs-lookup"><span data-stu-id="88e3e-261">Register your Red Hat subscription tooenable installation of packages from hello RHEL repository by running hello following command:</span></span>

        # subscription-manager register --auto-attach --username=XXX --password=XXX

8. <span data-ttu-id="88e3e-262">修改 Azure hello 核心開機行幼蟲組態 tooinclude 其他核心參數中。</span><span class="sxs-lookup"><span data-stu-id="88e3e-262">Modify hello kernel boot line in your grub configuration tooinclude additional kernel parameters for Azure.</span></span> <span data-ttu-id="88e3e-263">toodo 此設定，請開啟`/etc/default/grub`在文字編輯器，編輯 hello`GRUB_CMDLINE_LINUX`參數。</span><span class="sxs-lookup"><span data-stu-id="88e3e-263">toodo this configuration, open `/etc/default/grub` in a text editor, and edit hello `GRUB_CMDLINE_LINUX` parameter.</span></span> <span data-ttu-id="88e3e-264">例如：</span><span class="sxs-lookup"><span data-stu-id="88e3e-264">For example:</span></span>
   
        GRUB_CMDLINE_LINUX="rootdelay=300 console=ttyS0 earlyprintk=ttyS0 net.ifnames=0"
   
   <span data-ttu-id="88e3e-265">此命令也可確保所有主控台會將訊息都傳送 toohello 第一個序列連接埠，這可協助 Azure 偵錯問題的支援。</span><span class="sxs-lookup"><span data-stu-id="88e3e-265">This command also ensures that all console messages are sent toohello first serial port, which can assist Azure support with debugging issues.</span></span> <span data-ttu-id="88e3e-266">hello 命令也會關閉 hello 新增 RHEL 7 命名慣例的 Nic。</span><span class="sxs-lookup"><span data-stu-id="88e3e-266">hello command also turns off hello new RHEL 7 naming conventions for NICs.</span></span> <span data-ttu-id="88e3e-267">此外，我們建議您移除 hello 下列參數：</span><span class="sxs-lookup"><span data-stu-id="88e3e-267">In addition, we recommend that you remove hello following parameters:</span></span>
   
        rhgb quiet crashkernel=auto
   
    <span data-ttu-id="88e3e-268">沒有適用於雲端環境，我們想要傳送 toohello 序列連接埠的所有 hello 記錄 toobe 圖形和無訊息的開機。</span><span class="sxs-lookup"><span data-stu-id="88e3e-268">Graphical and quiet boot are not useful in a cloud environment where we want all hello logs toobe sent toohello serial port.</span></span> <span data-ttu-id="88e3e-269">您可以保留 hello`crashkernel`視設定選項。</span><span class="sxs-lookup"><span data-stu-id="88e3e-269">You can leave hello `crashkernel` option configured if desired.</span></span> <span data-ttu-id="88e3e-270">請注意，此參數減少 hello 128 MB 以上，hello 虛擬機器中的可用記憶體的數量可能較小的虛擬機器大小會造成問題。</span><span class="sxs-lookup"><span data-stu-id="88e3e-270">Note that this parameter reduces hello amount of available memory in hello virtual machine by 128 MB or more, which might be problematic on smaller virtual machine sizes.</span></span>

9. <span data-ttu-id="88e3e-271">完成之後編輯`/etc/default/grub`，請執行 hello 命令 toorebuild hello 幼蟲設定下列：</span><span class="sxs-lookup"><span data-stu-id="88e3e-271">After you are done editing `/etc/default/grub`, run hello following command toorebuild hello grub configuration:</span></span>

        # grub2-mkconfig -o /boot/grub2/grub.cfg

10. <span data-ttu-id="88e3e-272">將 Hyper-V 模組新增至 initramfs。</span><span class="sxs-lookup"><span data-stu-id="88e3e-272">Add Hyper-V modules into initramfs.</span></span>

    <span data-ttu-id="88e3e-273">編輯 `/etc/dracut.conf` 並加入內容：</span><span class="sxs-lookup"><span data-stu-id="88e3e-273">Edit `/etc/dracut.conf` and add content:</span></span>

        add_drivers+="hv_vmbus hv_netvsc hv_storvsc"

    <span data-ttu-id="88e3e-274">重建 initramfs：</span><span class="sxs-lookup"><span data-stu-id="88e3e-274">Rebuild initramfs:</span></span>

        # dracut -f -v

11. <span data-ttu-id="88e3e-275">解除安裝 cloud-init：</span><span class="sxs-lookup"><span data-stu-id="88e3e-275">Uninstall cloud-init:</span></span>

        # yum remove cloud-init

12. <span data-ttu-id="88e3e-276">請確定該 hello SSH 伺服器是在安裝並設定 toostart 開機時間：</span><span class="sxs-lookup"><span data-stu-id="88e3e-276">Ensure that hello SSH server is installed and configured toostart at boot time:</span></span>

        # systemctl enable sshd

    <span data-ttu-id="88e3e-277">修改下列行 /etc/ssh/sshd_config tooinclude hello:</span><span class="sxs-lookup"><span data-stu-id="88e3e-277">Modify /etc/ssh/sshd_config tooinclude hello following lines:</span></span>

        PasswordAuthentication yes
        ClientAliveInterval 180

13. <span data-ttu-id="88e3e-278">hello WALinuxAgent 封裝， `WALinuxAgent-<version>`，已排除 toohello Red Hat 額外項目儲存機制。</span><span class="sxs-lookup"><span data-stu-id="88e3e-278">hello WALinuxAgent package, `WALinuxAgent-<version>`, has been pushed toohello Red Hat extras repository.</span></span> <span data-ttu-id="88e3e-279">執行下列命令的 hello 啟用 hello 額外項目儲存機制：</span><span class="sxs-lookup"><span data-stu-id="88e3e-279">Enable hello extras repository by running hello following command:</span></span>

        # subscription-manager repos --enable=rhel-7-server-extras-rpms

14. <span data-ttu-id="88e3e-280">執行下列命令的 hello 安裝 hello Azure Linux 代理程式：</span><span class="sxs-lookup"><span data-stu-id="88e3e-280">Install hello Azure Linux Agent by running hello following command:</span></span>

        # yum install WALinuxAgent

    <span data-ttu-id="88e3e-281">啟用 hello waagent 服務：</span><span class="sxs-lookup"><span data-stu-id="88e3e-281">Enable hello waagent service:</span></span>

        # systemctl enable waagent.service

15. <span data-ttu-id="88e3e-282">不要在 hello 作業系統磁碟上建立的交換空間。</span><span class="sxs-lookup"><span data-stu-id="88e3e-282">Do not create swap space on hello operating system disk.</span></span>

    <span data-ttu-id="88e3e-283">hello Azure Linux 代理程式可以自動使用 hello 本機資源磁碟附加的 toohello 虛擬機器之後，在 Azure 上佈建 hello 虛擬機器所設定交換空間。</span><span class="sxs-lookup"><span data-stu-id="88e3e-283">hello Azure Linux Agent can automatically configure swap space by using hello local resource disk that is attached toohello virtual machine after hello virtual machine is provisioned on Azure.</span></span> <span data-ttu-id="88e3e-284">請注意，hello 本機資源磁碟是暫存磁碟，它可能會取消佈建 hello 虛擬機器時清空。</span><span class="sxs-lookup"><span data-stu-id="88e3e-284">Note that hello local resource disk is a temporary disk, and it might be emptied when hello virtual machine is deprovisioned.</span></span> <span data-ttu-id="88e3e-285">Hello 上一個步驟中安裝 hello Azure Linux 代理程式之後，修改下列參數中的 hello`/etc/waagent.conf`適當地：</span><span class="sxs-lookup"><span data-stu-id="88e3e-285">After you install hello Azure Linux Agent in hello previous step, modify hello following parameters in `/etc/waagent.conf` appropriately:</span></span>

        ResourceDisk.Format=y
        ResourceDisk.Filesystem=ext4
        ResourceDisk.MountPoint=/mnt/resource
        ResourceDisk.EnableSwap=y
        ResourceDisk.SwapSizeMB=2048    ## NOTE: set this toowhatever you need it toobe.

16. <span data-ttu-id="88e3e-286">取消註冊 hello 訂用帳戶 （如有必要） 藉由執行下列命令的 hello:</span><span class="sxs-lookup"><span data-stu-id="88e3e-286">Unregister hello subscription (if necessary) by running hello following command:</span></span>

        # subscription-manager unregister

17. <span data-ttu-id="88e3e-287">執行下列命令 toodeprovision hello 虛擬機器的 hello 並準備在 Azure 上佈建：</span><span class="sxs-lookup"><span data-stu-id="88e3e-287">Run hello following commands toodeprovision hello virtual machine and prepare it for provisioning on Azure:</span></span>

        # sudo waagent -force -deprovision

        # export HISTSIZE=0

        # logout

18. <span data-ttu-id="88e3e-288">關閉 hello KVM 中的虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="88e3e-288">Shut down hello virtual machine in KVM.</span></span>

19. <span data-ttu-id="88e3e-289">將 hello qcow2 映像 toohello VHD 格式的轉換。</span><span class="sxs-lookup"><span data-stu-id="88e3e-289">Convert hello qcow2 image toohello VHD format.</span></span>

    <span data-ttu-id="88e3e-290">第一次轉換 hello 影像 tooraw 格式：</span><span class="sxs-lookup"><span data-stu-id="88e3e-290">First convert hello image tooraw format:</span></span>

        # qemu-img convert -f qcow2 -O raw rhel-7.3.qcow2 rhel-7.3.raw

    <span data-ttu-id="88e3e-291">請確定 hello hello 原始影像大小配合 1 MB。</span><span class="sxs-lookup"><span data-stu-id="88e3e-291">Make sure that hello size of hello raw image is aligned with 1 MB.</span></span> <span data-ttu-id="88e3e-292">否則，無條件進位 hello 與 1 MB 的大小 tooalign:</span><span class="sxs-lookup"><span data-stu-id="88e3e-292">Otherwise, round up hello size tooalign with 1 MB:</span></span>

        # MB=$((1024*1024))
        # size=$(qemu-img info -f raw --output json "rhel-6.8.raw" | \
          gawk 'match($0, /"virtual-size": ([0-9]+),/, val) {print val[1]}')

        # rounded_size=$((($size/$MB + 1)*$MB))
        # qemu-img resize rhel-6.8.raw $rounded_size

    <span data-ttu-id="88e3e-293">轉換 hello 原始磁碟 tooa 固定大小的 VHD:</span><span class="sxs-lookup"><span data-stu-id="88e3e-293">Convert hello raw disk tooa fixed-sized VHD:</span></span>

        # qemu-img convert -f raw -o subformat=fixed -O vpc rhel-7.3.raw rhel-7.3.vhd

## <a name="prepare-a-red-hat-based-virtual-machine-from-vmware"></a><span data-ttu-id="88e3e-294">從 VMware 準備 Red Hat 型虛擬機器</span><span class="sxs-lookup"><span data-stu-id="88e3e-294">Prepare a Red Hat-based virtual machine from VMware</span></span>
### <a name="prerequisites"></a><span data-ttu-id="88e3e-295">必要條件</span><span class="sxs-lookup"><span data-stu-id="88e3e-295">Prerequisites</span></span>
<span data-ttu-id="88e3e-296">本節假設您已在 VMware 中安裝 RHEL 虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="88e3e-296">This section assumes that you have already installed a RHEL virtual machine in VMware.</span></span> <span data-ttu-id="88e3e-297">如需詳細資訊，關於如何 tooinstall 作業系統在 VMware 中，請參閱[VMware 來賓作業系統安裝指南](http://partnerweb.vmware.com/GOSIG/home.html)。</span><span class="sxs-lookup"><span data-stu-id="88e3e-297">For details about how tooinstall an operating system in VMware, see [VMware Guest Operating System Installation Guide](http://partnerweb.vmware.com/GOSIG/home.html).</span></span>

* <span data-ttu-id="88e3e-298">當您安裝 Linux 作業系統 hello 時，我們建議您使用標準的資料分割，而不是 LVM，這通常是 hello 許多安裝的預設值。</span><span class="sxs-lookup"><span data-stu-id="88e3e-298">When you install hello Linux operating system, we recommend that you use standard partitions rather than LVM, which is often hello default for many installations.</span></span> <span data-ttu-id="88e3e-299">這樣可避免 LVM 與複製的虛擬機器的名稱衝突，特別是當作業系統磁碟需要附加 toobe tooanother 虛擬機器進行疑難排解。</span><span class="sxs-lookup"><span data-stu-id="88e3e-299">This will avoid LVM name conflicts with cloned virtual machine, particularly if an operating system disk ever needs toobe attached tooanother virtual machine for troubleshooting.</span></span> <span data-ttu-id="88e3e-300">如果願意，您可以在資料磁碟上使用 LVM 或 RAID。</span><span class="sxs-lookup"><span data-stu-id="88e3e-300">LVM or RAID can be used on data disks if preferred.</span></span>
* <span data-ttu-id="88e3e-301">Hello 作業系統磁碟上未設定交換資料分割。</span><span class="sxs-lookup"><span data-stu-id="88e3e-301">Do not configure a swap partition on hello operating system disk.</span></span> <span data-ttu-id="88e3e-302">您可以設定 hello Linux 代理程式 toocreate 交換磁碟上的檔案 hello 暫存資源。</span><span class="sxs-lookup"><span data-stu-id="88e3e-302">You can configure hello Linux agent toocreate a swap file on hello temporary resource disk.</span></span> <span data-ttu-id="88e3e-303">您可以在 hello 面的步驟中找到相關資訊。</span><span class="sxs-lookup"><span data-stu-id="88e3e-303">You can find more information about this in hello steps that follow.</span></span>
* <span data-ttu-id="88e3e-304">當您建立虛擬硬碟 hello 時，選取**存放區的虛擬磁碟當做單一檔案**。</span><span class="sxs-lookup"><span data-stu-id="88e3e-304">When you create hello virtual hard disk, select **Store virtual disk as a single file**.</span></span>

### <a name="prepare-a-rhel-6-virtual-machine-from-vmware"></a><span data-ttu-id="88e3e-305">從 VMWare 準備 RHEL 6 虛擬機器</span><span class="sxs-lookup"><span data-stu-id="88e3e-305">Prepare a RHEL 6 virtual machine from VMware</span></span>
1. <span data-ttu-id="88e3e-306">RHEL 6 NetworkManager 可能會干擾 hello Azure Linux 代理程式。</span><span class="sxs-lookup"><span data-stu-id="88e3e-306">In RHEL 6, NetworkManager can interfere with hello Azure Linux agent.</span></span> <span data-ttu-id="88e3e-307">解除安裝此套件，藉由執行下列命令的 hello:</span><span class="sxs-lookup"><span data-stu-id="88e3e-307">Uninstall this package by running hello following command:</span></span>
   
        # sudo rpm -e --nodeps NetworkManager

2. <span data-ttu-id="88e3e-308">建立名為**網路**hello /etc/sysconfig/目錄中包含 hello 下列文字：</span><span class="sxs-lookup"><span data-stu-id="88e3e-308">Create a file named **network** in hello /etc/sysconfig/ directory that contains hello following text:</span></span>

        NETWORKING=yes
        HOSTNAME=localhost.localdomain

3. <span data-ttu-id="88e3e-309">建立或編輯 hello`/etc/sysconfig/network-scripts/ifcfg-eth0`檔並加入下列文字的 hello:</span><span class="sxs-lookup"><span data-stu-id="88e3e-309">Create or edit hello `/etc/sysconfig/network-scripts/ifcfg-eth0` file, and add hello following text:</span></span>
   
        DEVICE=eth0
        ONBOOT=yes
        BOOTPROTO=dhcp
        TYPE=Ethernet
        USERCTL=no
        PEERDNS=yes
        IPV6INIT=no

4. <span data-ttu-id="88e3e-310">移動 （或移除） hello udev 規則 tooavoid 產生 hello 乙太網路介面的靜態規則。</span><span class="sxs-lookup"><span data-stu-id="88e3e-310">Move (or remove) hello udev rules tooavoid generating static rules for hello Ethernet interface.</span></span> <span data-ttu-id="88e3e-311">在 Azure 或 Hyper-V 中複製虛擬機器時，這些規則會造成問題：</span><span class="sxs-lookup"><span data-stu-id="88e3e-311">These rules cause problems when you clone a virtual machine in Azure or Hyper-V:</span></span>

        # sudo ln -s /dev/null /etc/udev/rules.d/75-persistent-net-generator.rules

        # sudo rm -f /etc/udev/rules.d/70-persistent-net.rules

5. <span data-ttu-id="88e3e-312">請確定 hello 網路服務，將會執行下列命令的 hello 在開機時啟動：</span><span class="sxs-lookup"><span data-stu-id="88e3e-312">Ensure that hello network service will start at boot time by running hello following command:</span></span>

        # sudo chkconfig network on

6. <span data-ttu-id="88e3e-313">藉由執行下列命令的 hello 註冊封裝 hello RHEL 儲存機制從 Red Hat 訂用帳戶 tooenable hello 的安裝：</span><span class="sxs-lookup"><span data-stu-id="88e3e-313">Register your Red Hat subscription tooenable hello installation of packages from hello RHEL repository by running hello following command:</span></span>

        # sudo subscription-manager register --auto-attach --username=XXX --password=XXX

7. <span data-ttu-id="88e3e-314">hello WALinuxAgent 封裝， `WALinuxAgent-<version>`，已排除 toohello Red Hat 額外項目儲存機制。</span><span class="sxs-lookup"><span data-stu-id="88e3e-314">hello WALinuxAgent package, `WALinuxAgent-<version>`, has been pushed toohello Red Hat extras repository.</span></span> <span data-ttu-id="88e3e-315">執行下列命令的 hello 啟用 hello 額外項目儲存機制：</span><span class="sxs-lookup"><span data-stu-id="88e3e-315">Enable hello extras repository by running hello following command:</span></span>

        # subscription-manager repos --enable=rhel-6-server-extras-rpms

8. <span data-ttu-id="88e3e-316">修改 Azure hello 核心開機行幼蟲組態 tooinclude 其他核心參數中。</span><span class="sxs-lookup"><span data-stu-id="88e3e-316">Modify hello kernel boot line in your grub configuration tooinclude additional kernel parameters for Azure.</span></span> <span data-ttu-id="88e3e-317">toodo，開啟`/etc/default/grub`在文字編輯器，編輯 hello`GRUB_CMDLINE_LINUX`參數。</span><span class="sxs-lookup"><span data-stu-id="88e3e-317">toodo this, open `/etc/default/grub` in a text editor, and edit hello `GRUB_CMDLINE_LINUX` parameter.</span></span> <span data-ttu-id="88e3e-318">例如：</span><span class="sxs-lookup"><span data-stu-id="88e3e-318">For example:</span></span>
   
        GRUB_CMDLINE_LINUX="rootdelay=300 console=ttyS0 earlyprintk=ttyS0"
   
   <span data-ttu-id="88e3e-319">這也可確保所有主控台會將訊息都傳送 toohello 第一個序列連接埠，這可協助 Azure 偵錯問題的支援。</span><span class="sxs-lookup"><span data-stu-id="88e3e-319">This will also ensure that all console messages are sent toohello first serial port, which can assist Azure support with debugging issues.</span></span> <span data-ttu-id="88e3e-320">此外，我們建議您移除 hello 下列參數：</span><span class="sxs-lookup"><span data-stu-id="88e3e-320">In addition, we recommend that you remove hello following parameters:</span></span>
   
        rhgb quiet crashkernel=auto
   
    <span data-ttu-id="88e3e-321">沒有適用於雲端環境，我們想要傳送 toohello 序列連接埠的所有 hello 記錄 toobe 圖形和無訊息的開機。</span><span class="sxs-lookup"><span data-stu-id="88e3e-321">Graphical and quiet boot are not useful in a cloud environment where we want all hello logs toobe sent toohello serial port.</span></span> <span data-ttu-id="88e3e-322">您可以保留 hello`crashkernel`視設定選項。</span><span class="sxs-lookup"><span data-stu-id="88e3e-322">You can leave hello `crashkernel` option configured if desired.</span></span> <span data-ttu-id="88e3e-323">請注意，此參數減少 hello 128 MB 以上，hello 虛擬機器中的可用記憶體的數量可能較小的虛擬機器大小會造成問題。</span><span class="sxs-lookup"><span data-stu-id="88e3e-323">Note that this parameter reduces hello amount of available memory in hello virtual machine by 128 MB or more, which might be problematic on smaller virtual machine sizes.</span></span>

9. <span data-ttu-id="88e3e-324">新增 HYPER-V 模組 tooinitramfs:</span><span class="sxs-lookup"><span data-stu-id="88e3e-324">Add Hyper-V modules tooinitramfs:</span></span>

    <span data-ttu-id="88e3e-325">編輯`/etc/dracut.conf`，並加入下列內容的 hello:</span><span class="sxs-lookup"><span data-stu-id="88e3e-325">Edit `/etc/dracut.conf`, and add hello following content:</span></span>

        add_drivers+="hv_vmbus hv_netvsc hv_storvsc"

    <span data-ttu-id="88e3e-326">重建 initramfs：</span><span class="sxs-lookup"><span data-stu-id="88e3e-326">Rebuild initramfs:</span></span>

        # dracut -f -v

10. <span data-ttu-id="88e3e-327">請確定該 hello SSH 伺服器安裝，並在開機時，通常是 hello 預設設定 toostart。</span><span class="sxs-lookup"><span data-stu-id="88e3e-327">Ensure that hello SSH server is installed and configured toostart at boot time, which is usually hello default.</span></span> <span data-ttu-id="88e3e-328">修改`/etc/ssh/sshd_config`tooinclude hello 下列行：</span><span class="sxs-lookup"><span data-stu-id="88e3e-328">Modify `/etc/ssh/sshd_config` tooinclude hello following line:</span></span>

    <span data-ttu-id="88e3e-329">ClientAliveInterval 180</span><span class="sxs-lookup"><span data-stu-id="88e3e-329">ClientAliveInterval 180</span></span>

11. <span data-ttu-id="88e3e-330">執行下列命令的 hello 安裝 hello Azure Linux 代理程式：</span><span class="sxs-lookup"><span data-stu-id="88e3e-330">Install hello Azure Linux Agent by running hello following command:</span></span>

        # sudo yum install WALinuxAgent

        # sudo chkconfig waagent on

12. <span data-ttu-id="88e3e-331">不要在 hello 作業系統磁碟上建立的交換空間。</span><span class="sxs-lookup"><span data-stu-id="88e3e-331">Do not create swap space on hello operating system disk.</span></span>

    <span data-ttu-id="88e3e-332">hello Azure Linux 代理程式可以自動使用 hello 本機資源磁碟附加的 toohello 虛擬機器之後，在 Azure 上佈建 hello 虛擬機器所設定交換空間。</span><span class="sxs-lookup"><span data-stu-id="88e3e-332">hello Azure Linux Agent can automatically configure swap space by using hello local resource disk that is attached toohello virtual machine after hello virtual machine is provisioned on Azure.</span></span> <span data-ttu-id="88e3e-333">請注意，hello 本機資源磁碟是暫存磁碟，它可能會取消佈建 hello 虛擬機器時清空。</span><span class="sxs-lookup"><span data-stu-id="88e3e-333">Note that hello local resource disk is a temporary disk, and it might be emptied when hello virtual machine is deprovisioned.</span></span> <span data-ttu-id="88e3e-334">Hello 上一個步驟中安裝 hello Azure Linux 代理程式之後，修改下列參數中的 hello`/etc/waagent.conf`適當地：</span><span class="sxs-lookup"><span data-stu-id="88e3e-334">After you install hello Azure Linux Agent in hello previous step, modify hello following parameters in `/etc/waagent.conf` appropriately:</span></span>

        ResourceDisk.Format=y
        ResourceDisk.Filesystem=ext4
        ResourceDisk.MountPoint=/mnt/resource
        ResourceDisk.EnableSwap=y
        ResourceDisk.SwapSizeMB=2048    ## NOTE: set this toowhatever you need it toobe.

13. <span data-ttu-id="88e3e-335">取消註冊 hello 訂用帳戶 （如有必要） 藉由執行下列命令的 hello:</span><span class="sxs-lookup"><span data-stu-id="88e3e-335">Unregister hello subscription (if necessary) by running hello following command:</span></span>

        # sudo subscription-manager unregister

14. <span data-ttu-id="88e3e-336">執行下列命令 toodeprovision hello 虛擬機器的 hello 並準備在 Azure 上佈建：</span><span class="sxs-lookup"><span data-stu-id="88e3e-336">Run hello following commands toodeprovision hello virtual machine and prepare it for provisioning on Azure:</span></span>

        # sudo waagent -force -deprovision

        # export HISTSIZE=0

        # logout

15. <span data-ttu-id="88e3e-337">關閉 hello 虛擬機器，並將轉換 hello VMDK 檔案 tooa.vhd 檔案。</span><span class="sxs-lookup"><span data-stu-id="88e3e-337">Shut down hello virtual machine, and convert hello VMDK file tooa .vhd file.</span></span>

    <span data-ttu-id="88e3e-338">第一次轉換 hello 影像 tooraw 格式：</span><span class="sxs-lookup"><span data-stu-id="88e3e-338">First convert hello image tooraw format:</span></span>

        # qemu-img convert -f vmdk -O raw rhel-6.8.vmdk rhel-6.8.raw

    <span data-ttu-id="88e3e-339">請確定 hello hello 原始影像大小配合 1 MB。</span><span class="sxs-lookup"><span data-stu-id="88e3e-339">Make sure that hello size of hello raw image is aligned with 1 MB.</span></span> <span data-ttu-id="88e3e-340">否則，無條件進位 hello 與 1 MB 的大小 tooalign:</span><span class="sxs-lookup"><span data-stu-id="88e3e-340">Otherwise, round up hello size tooalign with 1 MB:</span></span>

        # MB=$((1024*1024))
        # size=$(qemu-img info -f raw --output json "rhel-6.8.raw" | \
          gawk 'match($0, /"virtual-size": ([0-9]+),/, val) {print val[1]}')

        # rounded_size=$((($size/$MB + 1)*$MB))
        # qemu-img resize rhel-6.8.raw $rounded_size

    <span data-ttu-id="88e3e-341">轉換 hello 原始磁碟 tooa 固定大小的 VHD:</span><span class="sxs-lookup"><span data-stu-id="88e3e-341">Convert hello raw disk tooa fixed-sized VHD:</span></span>

        # qemu-img convert -f raw -o subformat=fixed -O vpc rhel-6.8.raw rhel-6.8.vhd

### <a name="prepare-a-rhel-7-virtual-machine-from-vmware"></a><span data-ttu-id="88e3e-342">從 VMWare 準備 RHEL 7 虛擬機器</span><span class="sxs-lookup"><span data-stu-id="88e3e-342">Prepare a RHEL 7 virtual machine from VMware</span></span>
1. <span data-ttu-id="88e3e-343">建立或編輯 hello`/etc/sysconfig/network`檔並加入下列文字的 hello:</span><span class="sxs-lookup"><span data-stu-id="88e3e-343">Create or edit hello `/etc/sysconfig/network` file, and add hello following text:</span></span>
   
        NETWORKING=yes
        HOSTNAME=localhost.localdomain

2. <span data-ttu-id="88e3e-344">建立或編輯 hello`/etc/sysconfig/network-scripts/ifcfg-eth0`檔並加入下列文字的 hello:</span><span class="sxs-lookup"><span data-stu-id="88e3e-344">Create or edit hello `/etc/sysconfig/network-scripts/ifcfg-eth0` file, and add hello following text:</span></span>
   
        DEVICE=eth0
        ONBOOT=yes
        BOOTPROTO=dhcp
        TYPE=Ethernet
        USERCTL=no
        PEERDNS=yes
        IPV6INIT=no
        NM_CONTROLLED=no

3. <span data-ttu-id="88e3e-345">請確定 hello 網路服務，將會執行下列命令的 hello 在開機時啟動：</span><span class="sxs-lookup"><span data-stu-id="88e3e-345">Ensure that hello network service will start at boot time by running hello following command:</span></span>

        # sudo chkconfig network on

4. <span data-ttu-id="88e3e-346">藉由執行下列命令的 hello 註冊封裝 hello RHEL 儲存機制從 Red Hat 訂用帳戶 tooenable hello 的安裝：</span><span class="sxs-lookup"><span data-stu-id="88e3e-346">Register your Red Hat subscription tooenable hello installation of packages from hello RHEL repository by running hello following command:</span></span>

        # sudo subscription-manager register --auto-attach --username=XXX --password=XXX

5. <span data-ttu-id="88e3e-347">修改 Azure hello 核心開機行幼蟲組態 tooinclude 其他核心參數中。</span><span class="sxs-lookup"><span data-stu-id="88e3e-347">Modify hello kernel boot line in your grub configuration tooinclude additional kernel parameters for Azure.</span></span> <span data-ttu-id="88e3e-348">toodo 這項修改，開啟`/etc/default/grub`在文字編輯器，編輯 hello`GRUB_CMDLINE_LINUX`參數。</span><span class="sxs-lookup"><span data-stu-id="88e3e-348">toodo this modification, open `/etc/default/grub` in a text editor, and edit hello `GRUB_CMDLINE_LINUX` parameter.</span></span> <span data-ttu-id="88e3e-349">例如：</span><span class="sxs-lookup"><span data-stu-id="88e3e-349">For example:</span></span>
   
        GRUB_CMDLINE_LINUX="rootdelay=300 console=ttyS0 earlyprintk=ttyS0 net.ifnames=0"
   
   <span data-ttu-id="88e3e-350">這項設定也可確保所有主控台會將訊息都傳送 toohello 第一個序列連接埠，這可協助 Azure 偵錯問題的支援。</span><span class="sxs-lookup"><span data-stu-id="88e3e-350">This configuration also ensures that all console messages are sent toohello first serial port, which can assist Azure support with debugging issues.</span></span> <span data-ttu-id="88e3e-351">它也會關閉 hello 新增 RHEL 7 命名慣例的 Nic。</span><span class="sxs-lookup"><span data-stu-id="88e3e-351">It also turns off hello new RHEL 7 naming conventions for NICs.</span></span> <span data-ttu-id="88e3e-352">此外，我們建議您移除 hello 下列參數：</span><span class="sxs-lookup"><span data-stu-id="88e3e-352">In addition, we recommend that you remove hello following parameters:</span></span>
   
        rhgb quiet crashkernel=auto
   
    <span data-ttu-id="88e3e-353">沒有適用於雲端環境，我們想要傳送 toohello 序列連接埠的所有 hello 記錄 toobe 圖形和無訊息的開機。</span><span class="sxs-lookup"><span data-stu-id="88e3e-353">Graphical and quiet boot are not useful in a cloud environment where we want all hello logs toobe sent toohello serial port.</span></span> <span data-ttu-id="88e3e-354">您可以保留 hello`crashkernel`視設定選項。</span><span class="sxs-lookup"><span data-stu-id="88e3e-354">You can leave hello `crashkernel` option configured if desired.</span></span> <span data-ttu-id="88e3e-355">請注意，此參數減少 hello 128 MB 以上，hello 虛擬機器中的可用記憶體的數量可能較小的虛擬機器大小會造成問題。</span><span class="sxs-lookup"><span data-stu-id="88e3e-355">Note that this parameter reduces hello amount of available memory in hello virtual machine by 128 MB or more, which might be problematic on smaller virtual machine sizes.</span></span>

6. <span data-ttu-id="88e3e-356">完成之後編輯`/etc/default/grub`，請執行 hello 命令 toorebuild hello 幼蟲設定下列：</span><span class="sxs-lookup"><span data-stu-id="88e3e-356">After you are done editing `/etc/default/grub`, run hello following command toorebuild hello grub configuration:</span></span>

        # sudo grub2-mkconfig -o /boot/grub2/grub.cfg

7. <span data-ttu-id="88e3e-357">新增 HYPER-V 模組 tooinitramfs。</span><span class="sxs-lookup"><span data-stu-id="88e3e-357">Add Hyper-V modules tooinitramfs.</span></span>

    <span data-ttu-id="88e3e-358">編輯 `/etc/dracut.conf`，新增內容：</span><span class="sxs-lookup"><span data-stu-id="88e3e-358">Edit `/etc/dracut.conf`, add content:</span></span>

        add_drivers+="hv_vmbus hv_netvsc hv_storvsc"

    <span data-ttu-id="88e3e-359">重建 initramfs：</span><span class="sxs-lookup"><span data-stu-id="88e3e-359">Rebuild initramfs:</span></span>

        # dracut -f -v

8. <span data-ttu-id="88e3e-360">請確定該 hello SSH 伺服器是在安裝並設定 toostart 開機時間。</span><span class="sxs-lookup"><span data-stu-id="88e3e-360">Ensure that hello SSH server is installed and configured toostart at boot time.</span></span> <span data-ttu-id="88e3e-361">這項設定通常是 hello 預設值。</span><span class="sxs-lookup"><span data-stu-id="88e3e-361">This setting is usually hello default.</span></span> <span data-ttu-id="88e3e-362">修改`/etc/ssh/sshd_config`tooinclude hello 下列行：</span><span class="sxs-lookup"><span data-stu-id="88e3e-362">Modify `/etc/ssh/sshd_config` tooinclude hello following line:</span></span>

        ClientAliveInterval 180

9. <span data-ttu-id="88e3e-363">hello WALinuxAgent 封裝， `WALinuxAgent-<version>`，已排除 toohello Red Hat 額外項目儲存機制。</span><span class="sxs-lookup"><span data-stu-id="88e3e-363">hello WALinuxAgent package, `WALinuxAgent-<version>`, has been pushed toohello Red Hat extras repository.</span></span> <span data-ttu-id="88e3e-364">執行下列命令的 hello 啟用 hello 額外項目儲存機制：</span><span class="sxs-lookup"><span data-stu-id="88e3e-364">Enable hello extras repository by running hello following command:</span></span>

        # subscription-manager repos --enable=rhel-7-server-extras-rpms

10. <span data-ttu-id="88e3e-365">執行下列命令的 hello 安裝 hello Azure Linux 代理程式：</span><span class="sxs-lookup"><span data-stu-id="88e3e-365">Install hello Azure Linux Agent by running hello following command:</span></span>

        # sudo yum install WALinuxAgent

        # sudo systemctl enable waagent.service

11. <span data-ttu-id="88e3e-366">不要在 hello 作業系統磁碟上建立的交換空間。</span><span class="sxs-lookup"><span data-stu-id="88e3e-366">Do not create swap space on hello operating system disk.</span></span>

    <span data-ttu-id="88e3e-367">hello Azure Linux 代理程式可以自動使用 hello 本機資源磁碟附加的 toohello 虛擬機器之後，在 Azure 上佈建 hello 虛擬機器所設定交換空間。</span><span class="sxs-lookup"><span data-stu-id="88e3e-367">hello Azure Linux Agent can automatically configure swap space by using hello local resource disk that is attached toohello virtual machine after hello virtual machine is provisioned on Azure.</span></span> <span data-ttu-id="88e3e-368">請注意，hello 本機資源磁碟是暫存磁碟，它可能會取消佈建 hello 虛擬機器時清空。</span><span class="sxs-lookup"><span data-stu-id="88e3e-368">Note that hello local resource disk is a temporary disk, and it might be emptied when hello virtual machine is deprovisioned.</span></span> <span data-ttu-id="88e3e-369">Hello 上一個步驟中安裝 hello Azure Linux 代理程式之後，修改下列參數中的 hello`/etc/waagent.conf`適當地：</span><span class="sxs-lookup"><span data-stu-id="88e3e-369">After you install hello Azure Linux Agent in hello previous step, modify hello following parameters in `/etc/waagent.conf` appropriately:</span></span>

        ResourceDisk.Format=y
        ResourceDisk.Filesystem=ext4
        ResourceDisk.MountPoint=/mnt/resource
        ResourceDisk.EnableSwap=y
        ResourceDisk.SwapSizeMB=2048    ## NOTE: set this toowhatever you need it toobe.

12. <span data-ttu-id="88e3e-370">如果您想 toounregister hello 訂用帳戶，執行下列命令的 hello:</span><span class="sxs-lookup"><span data-stu-id="88e3e-370">If you want toounregister hello subscription, run hello following command:</span></span>

        # sudo subscription-manager unregister

13. <span data-ttu-id="88e3e-371">執行下列命令 toodeprovision hello 虛擬機器的 hello 並準備在 Azure 上佈建：</span><span class="sxs-lookup"><span data-stu-id="88e3e-371">Run hello following commands toodeprovision hello virtual machine and prepare it for provisioning on Azure:</span></span>

        # sudo waagent -force -deprovision

        # export HISTSIZE=0

        # logout

14. <span data-ttu-id="88e3e-372">關閉 hello 虛擬機器，並將轉換 hello VMDK 檔案 toohello VHD 格式。</span><span class="sxs-lookup"><span data-stu-id="88e3e-372">Shut down hello virtual machine, and convert hello VMDK file toohello VHD format.</span></span>

    <span data-ttu-id="88e3e-373">第一次轉換 hello 影像 tooraw 格式：</span><span class="sxs-lookup"><span data-stu-id="88e3e-373">First convert hello image tooraw format:</span></span>

        # qemu-img convert -f vmdk -O raw rhel-7.3.vmdk rhel-7.3.raw

    <span data-ttu-id="88e3e-374">請確定 hello hello 原始影像大小配合 1 MB。</span><span class="sxs-lookup"><span data-stu-id="88e3e-374">Make sure that hello size of hello raw image is aligned with 1 MB.</span></span> <span data-ttu-id="88e3e-375">否則，無條件進位 hello 與 1 MB 的大小 tooalign:</span><span class="sxs-lookup"><span data-stu-id="88e3e-375">Otherwise, round up hello size tooalign with 1 MB:</span></span>

        # MB=$((1024*1024))
        # size=$(qemu-img info -f raw --output json "rhel-6.8.raw" | \
          gawk 'match($0, /"virtual-size": ([0-9]+),/, val) {print val[1]}')

        # rounded_size=$((($size/$MB + 1)*$MB))
        # qemu-img resize rhel-6.8.raw $rounded_size

    <span data-ttu-id="88e3e-376">轉換 hello 原始磁碟 tooa 固定大小的 VHD:</span><span class="sxs-lookup"><span data-stu-id="88e3e-376">Convert hello raw disk tooa fixed-sized VHD:</span></span>

        # qemu-img convert -f raw -o subformat=fixed -O vpc rhel-7.3.raw rhel-7.3.vhd

## <a name="prepare-a-red-hat-based-virtual-machine-from-an-iso-by-using-a-kickstart-file-automatically"></a><span data-ttu-id="88e3e-377">使用 kickstart 檔案自動從 ISO 準備 Red Hat 型虛擬機器</span><span class="sxs-lookup"><span data-stu-id="88e3e-377">Prepare a Red Hat-based virtual machine from an ISO by using a kickstart file automatically</span></span>
### <a name="prepare-a-rhel-7-virtual-machine-from-a-kickstart-file"></a><span data-ttu-id="88e3e-378">從 kickstart 檔案準備 RHEL 7 虛擬機器</span><span class="sxs-lookup"><span data-stu-id="88e3e-378">Prepare a RHEL 7 virtual machine from a kickstart file</span></span>

1.  <span data-ttu-id="88e3e-379">建立包含下列內容，hello 啟動檔案，並儲存 hello 檔案。</span><span class="sxs-lookup"><span data-stu-id="88e3e-379">Create a kickstart file that includes hello following content, and save hello file.</span></span> <span data-ttu-id="88e3e-380">如需有關啟動安裝的詳細資訊，請參閱 hello[啟動安裝指南](https://access.redhat.com/documentation/en-US/Red_Hat_Enterprise_Linux/7/html/Installation_Guide/chap-kickstart-installations.html)。</span><span class="sxs-lookup"><span data-stu-id="88e3e-380">For details about kickstart installation, see hello [Kickstart Installation Guide](https://access.redhat.com/documentation/en-US/Red_Hat_Enterprise_Linux/7/html/Installation_Guide/chap-kickstart-installations.html).</span></span>

        # Kickstart for provisioning a RHEL 7 Azure VM

        # System authorization information
          auth --enableshadow --passalgo=sha512

        # Use graphical install
        text

        # Do not run hello Setup Agent on first boot
        firstboot --disable

        # Keyboard layouts
        keyboard --vckeymap=us --xlayouts='us'

        # System language
        lang en_US.UTF-8

        # Network information
        network  --bootproto=dhcp

        # Root password
        rootpw --plaintext "to_be_disabled"

        # System services
        services --enabled="sshd,waagent,NetworkManager"

        # System timezone
        timezone Etc/UTC --isUtc --ntpservers 0.rhel.pool.ntp.org,1.rhel.pool.ntp.org,2.rhel.pool.ntp.org,3.rhel.pool.ntp.org

        # Partition clearing information
        clearpart --all --initlabel

        # Clear hello MBR
        zerombr

        # Disk partitioning information
        part /boot --fstype="xfs" --size=500
        part / --fstyp="xfs" --size=1 --grow --asprimary

        # System bootloader configuration
        bootloader --location=mbr

        # Firewall configuration
        firewall --disabled

        # Enable SELinux
        selinux --enforcing

        # Don't configure X
        skipx

        # Power down hello machine after install
        poweroff

        %packages
        @base
        @console-internet
        chrony
        sudo
        parted
        -dracut-config-rescue

        %end

        %post --log=/var/log/anaconda/post-install.log

        #!/bin/bash

        # Register Red Hat Subscription
        subscription-manager register --username=XXX --password=XXX --auto-attach --force

        # Install latest repo update
        yum update -y

        # Enable extras repo
        subscription-manager repos --enable=rhel-7-server-extras-rpms

        # Install WALinuxAgent
        yum install -y WALinuxAgent

        # Unregister Red Hat subscription
        subscription-manager unregister

        # Enable waaagent at boot-up
        systemctl enable waagent

        # Disable hello root account
        usermod root -p '!!'

        # Configure swap in WALinuxAgent
        sed -i 's/^\(ResourceDisk\.EnableSwap\)=[Nn]$/\1=y/g' /etc/waagent.conf
        sed -i 's/^\(ResourceDisk\.SwapSizeMB\)=[0-9]*$/\1=2048/g' /etc/waagent.conf

        # Set hello cmdline
        sed -i 's/^\(GRUB_CMDLINE_LINUX\)=".*"$/\1="console=tty1 console=ttyS0 earlyprintk=ttyS0 rootdelay=300"/g' /etc/default/grub

        # Enable SSH keepalive
        sed -i 's/^#\(ClientAliveInterval\).*$/\1 180/g' /etc/ssh/sshd_config

        # Build hello grub cfg
        grub2-mkconfig -o /boot/grub2/grub.cfg

        # Configure network
        cat << EOF > /etc/sysconfig/network-scripts/ifcfg-eth0
        DEVICE=eth0
        ONBOOT=yes
        BOOTPROTO=dhcp
        TYPE=Ethernet
        USERCTL=no
        PEERDNS=yes
        IPV6INIT=no
        NM_CONTROLLED=no
        EOF

        # Deprovision and prepare for Azure
        waagent -force -deprovision

        %end

2. <span data-ttu-id="88e3e-381">將 hello 安裝系統可以存取的 hello 啟動檔案。</span><span class="sxs-lookup"><span data-stu-id="88e3e-381">Place hello kickstart file where hello installation system can access it.</span></span>

3. <span data-ttu-id="88e3e-382">在 Hyper-V 管理員中建立新的虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="88e3e-382">In Hyper-V Manager, create a new virtual machine.</span></span> <span data-ttu-id="88e3e-383">在 hello**連接虛擬硬碟**頁面上，選取**稍後連結虛擬硬碟**，和完整 hello 新增虛擬機器精靈。</span><span class="sxs-lookup"><span data-stu-id="88e3e-383">On hello **Connect Virtual Hard Disk** page, select **Attach a virtual hard disk later**, and complete hello New Virtual Machine Wizard.</span></span>

4. <span data-ttu-id="88e3e-384">開啟 hello 虛擬機器設定：</span><span class="sxs-lookup"><span data-stu-id="88e3e-384">Open hello virtual machine settings:</span></span>

    <span data-ttu-id="88e3e-385">a.</span><span class="sxs-lookup"><span data-stu-id="88e3e-385">a.</span></span>  <span data-ttu-id="88e3e-386">附加新的虛擬硬碟 toohello 虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="88e3e-386">Attach a new virtual hard disk toohello virtual machine.</span></span> <span data-ttu-id="88e3e-387">請確定 tooselect **VHD 格式**和**固定的大小**。</span><span class="sxs-lookup"><span data-stu-id="88e3e-387">Make sure tooselect **VHD Format** and **Fixed Size**.</span></span>

    <span data-ttu-id="88e3e-388">b.</span><span class="sxs-lookup"><span data-stu-id="88e3e-388">b.</span></span>  <span data-ttu-id="88e3e-389">附加 hello 安裝 ISO toohello DVD 光碟機。</span><span class="sxs-lookup"><span data-stu-id="88e3e-389">Attach hello installation ISO toohello DVD drive.</span></span>

    <span data-ttu-id="88e3e-390">c.</span><span class="sxs-lookup"><span data-stu-id="88e3e-390">c.</span></span>  <span data-ttu-id="88e3e-391">設定 hello BIOS tooboot 從光碟片。</span><span class="sxs-lookup"><span data-stu-id="88e3e-391">Set hello BIOS tooboot from CD.</span></span>

5. <span data-ttu-id="88e3e-392">啟動 hello 虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="88e3e-392">Start hello virtual machine.</span></span> <span data-ttu-id="88e3e-393">當出現 hello 安裝指南時，請按 **索引標籤**tooconfigure hello 開機選項。</span><span class="sxs-lookup"><span data-stu-id="88e3e-393">When hello installation guide appears, press **Tab** tooconfigure hello boot options.</span></span>

6. <span data-ttu-id="88e3e-394">Enter`inst.ks=<hello location of hello kickstart file>`結尾 hello hello 開機選項，然後按**Enter**。</span><span class="sxs-lookup"><span data-stu-id="88e3e-394">Enter `inst.ks=<hello location of hello kickstart file>` at hello end of hello boot options, and press **Enter**.</span></span>

7. <span data-ttu-id="88e3e-395">等候 hello 安裝 toofinish。</span><span class="sxs-lookup"><span data-stu-id="88e3e-395">Wait for hello installation toofinish.</span></span> <span data-ttu-id="88e3e-396">完成後，hello 虛擬機器將會自動關閉。</span><span class="sxs-lookup"><span data-stu-id="88e3e-396">When it's finished, hello virtual machine will be shut down automatically.</span></span> <span data-ttu-id="88e3e-397">Linux VHD 是現在準備好 toobe 上傳 tooAzure。</span><span class="sxs-lookup"><span data-stu-id="88e3e-397">Your Linux VHD is now ready toobe uploaded tooAzure.</span></span>

## <a name="known-issues"></a><span data-ttu-id="88e3e-398">已知問題</span><span class="sxs-lookup"><span data-stu-id="88e3e-398">Known issues</span></span>
### <a name="hello-hyper-v-driver-could-not-be-included-in-hello-initial-ram-disk-when-using-a-non-hyper-v-hypervisor"></a><span data-ttu-id="88e3e-399">hello HYPER-V 驅動程式可能不會包含在 hello 初始 RAM 磁碟使用非 HYPER-V hypervisor 時</span><span class="sxs-lookup"><span data-stu-id="88e3e-399">hello Hyper-V driver could not be included in hello initial RAM disk when using a non-Hyper-V hypervisor</span></span>

<span data-ttu-id="88e3e-400">在某些情況下，Linux 的安裝程式可能不包括 hello 驅動程式之 HYPER-V 的 hello 初始 RAM 磁碟 （initrd 或 initramfs） 除非 Linux 偵測它在 HYPER-V 環境中執行。</span><span class="sxs-lookup"><span data-stu-id="88e3e-400">In some cases, Linux installers might not include hello drivers for Hyper-V in hello initial RAM disk (initrd or initramfs) unless Linux detects that it is running in a Hyper-V environment.</span></span>

<span data-ttu-id="88e3e-401">當您使用不同虛擬化 （亦即 Virtualbox、 Xen 等） 的系統 tooprepare Linux 映像時，您可能需要至少 hello hv_vmbus 的 toorebuild initrd tooensure 且 hv_storvsc 核心模組可 hello 初始 RAM 磁碟上。</span><span class="sxs-lookup"><span data-stu-id="88e3e-401">When you're using a different virtualization system (that is, Virtualbox, Xen, etc.) tooprepare your Linux image, you might need toorebuild initrd tooensure that at least hello hv_vmbus and hv_storvsc kernel modules are available on hello initial RAM disk.</span></span> <span data-ttu-id="88e3e-402">這在至少 hello 上游 Red Hat 發佈為基礎的系統上是已知的問題。</span><span class="sxs-lookup"><span data-stu-id="88e3e-402">This is a known issue at least on systems that are based on hello upstream Red Hat distribution.</span></span>

<span data-ttu-id="88e3e-403">tooresolve 這個問題，請新增 HYPER-V 模組 tooinitramfs 再重建它：</span><span class="sxs-lookup"><span data-stu-id="88e3e-403">tooresolve this issue, add Hyper-V modules tooinitramfs and rebuild it:</span></span>

<span data-ttu-id="88e3e-404">編輯`/etc/dracut.conf`，並加入下列內容的 hello:</span><span class="sxs-lookup"><span data-stu-id="88e3e-404">Edit `/etc/dracut.conf`, and add hello following content:</span></span>

        add_drivers+="hv_vmbus hv_netvsc hv_storvsc"

<span data-ttu-id="88e3e-405">重建 initramfs：</span><span class="sxs-lookup"><span data-stu-id="88e3e-405">Rebuild initramfs:</span></span>

        # dracut -f -v

<span data-ttu-id="88e3e-406">如需詳細資訊，請參閱 hello 資訊[重建 initramfs](https://access.redhat.com/solutions/1958)。</span><span class="sxs-lookup"><span data-stu-id="88e3e-406">For more details, see hello information about [rebuilding initramfs](https://access.redhat.com/solutions/1958).</span></span>

## <a name="next-steps"></a><span data-ttu-id="88e3e-407">後續步驟</span><span class="sxs-lookup"><span data-stu-id="88e3e-407">Next steps</span></span>
<span data-ttu-id="88e3e-408">您要現在準備好 toouse Red Hat Enterprise Linux 虛擬硬碟 toocreate 新虛擬機器在 Azure 中。</span><span class="sxs-lookup"><span data-stu-id="88e3e-408">You're now ready toouse your Red Hat Enterprise Linux virtual hard disk toocreate new virtual machines in Azure.</span></span> <span data-ttu-id="88e3e-409">如果這是 hello 正在上傳 hello.vhd 檔案 tooAzure 的第一次，請參閱步驟 2 和 3 中的[建立和上傳包含 hello Linux 作業系統的虛擬硬碟](classic/create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="88e3e-409">If this is hello first time that you're uploading hello .vhd file tooAzure, see steps 2 and 3 in [Creating and uploading a virtual hard disk that contains hello Linux operating system](classic/create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).</span></span>

<span data-ttu-id="88e3e-410">如需更多詳細的 hello hypervisor 認證 toorun Red Hat Enterprise Linux，請參閱[hello Red Hat 網站](https://access.redhat.com/certified-hypervisors)。</span><span class="sxs-lookup"><span data-stu-id="88e3e-410">For more details about hello hypervisors that are certified toorun Red Hat Enterprise Linux, see [hello Red Hat website](https://access.redhat.com/certified-hypervisors).</span></span>
