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
# <a name="prepare-a-centos-based-virtual-machine-for-azure"></a>準備適用於 Azure 的 CentOS 型虛擬機器
* [準備適用於 Azure 的 CentOS 6.x 虛擬機器](#centos-6x)
* [準備適用於 Azure 的 CentOS 7.0+ 虛擬機器](#centos-70)

[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-both-include.md)]

## <a name="prerequisites"></a>必要條件
本文假設您已安裝 CentOS （或類似的衍生項目） Linux 作業系統 tooa 虛擬硬碟。 多個工具存在 toocreate.vhd 檔案，例如 HYPER-V 之類的虛擬化解決方案。 如需指示，請參閱[安裝 hello HYPER-V 角色和設定虛擬機器](http://technet.microsoft.com/library/hh846766.aspx)。

**CentOS 安裝注意事項**

* 另請參閱[一般 Linux 安裝注意事項](create-upload-generic.md#general-linux-installation-notes)，了解為 Azure 準備 Linux 的更多祕訣。
* hello VHDX 格式不支援在 Azure 中，只有**固定 VHD**。  您可以將使用 HYPER-V 管理員 hello 磁碟 tooVHD 格式轉換或 hello convert-vhd 指令程式。 如果您使用 VirtualBox 這表示選取**固定大小**為相對於 toohello 預設建立 hello 磁碟時，動態配置。
* 安裝 hello Linux 系統時*建議*您使用標準的資料分割，而非 LVM （通常 hello 預設值為許多安裝）。 這樣可避免與複製 Vm，LVM 名稱衝突，特別是當作業系統磁碟需要附加 toobe tooanother 相同的 VM 進行疑難排解。 如果願意，您可以在資料磁碟上使用 [LVM](configure-raid.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) 或 [RAID](configure-lvm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)。
* 需要掛接 UDF 檔案系統的核心支援。 在第一次開機 Azure hello 上佈建組態會透過附加的 toohello 客體的 UDF 格式化媒體傳遞 toohello Linux VM。 hello Azure Linux 代理程式必須要能夠 toomount hello UDF 檔案系統 tooread 其組態，並佈建 hello VM。
* Linux Kernel 2.6.37 以下的版本不支援較大 VM 大小 Hyper-V 上的NUMA。 這個問題主要會影響較舊的分佈上游使用 hello Red Hat 2.6.32 核心及已修正 RHEL 6.6 (核心-2.6.32-504) 中。 執行自訂的核心超過 2.6.37 或較舊 RHEL 基礎核心非 2.6.32-504 必須設定系統 hello 開機參數`numa=off`hello 核心 grub.conf 在命令列上。 如需詳細資訊，請參閱 Red Hat [KB 436883](https://access.redhat.com/solutions/436883)。
* 請勿設定 hello OS 磁碟交換資料分割。 hello Linux 代理程式可以設定的 toocreate 交換磁碟上的檔案 hello 暫存資源。  相關資訊位於下列 hello 步驟。
* 所有 hello Vhd 必須是 1 MB 的倍數的大小。

## <a name="centos-6x"></a>CentOS 6.x

1. 在 HYPER-V 管理員 中，選取 hello 虛擬機器。

2. 按一下**連接**tooopen hello 虛擬機器的主控台視窗。

3. CentOS 6 NetworkManager 可能會干擾 hello Azure Linux 代理程式。 解除安裝此套件，藉由執行下列命令的 hello:
   
        # sudo rpm -e --nodeps NetworkManager

4. 建立或編輯 hello 檔案`/etc/sysconfig/network`並加入下列文字的 hello:
   
        NETWORKING=yes
        HOSTNAME=localhost.localdomain

5. 建立或編輯 hello 檔案`/etc/sysconfig/network-scripts/ifcfg-eth0`並加入下列文字的 hello:
   
        DEVICE=eth0
        ONBOOT=yes
        BOOTPROTO=dhcp
        TYPE=Ethernet
        USERCTL=no
        PEERDNS=yes
        IPV6INIT=no

6. 修改 udev 規則 tooavoid 產生 hello 乙太網路介面的靜態規則。 在 Microsoft Azure 或 Hyper-V 中複製虛擬機器時，這些規則可能會造成問題：
   
        # sudo ln -s /dev/null /etc/udev/rules.d/75-persistent-net-generator.rules
        # sudo rm -f /etc/udev/rules.d/70-persistent-net.rules

7. 請確定 hello 網路服務將會在開機時啟動藉由執行下列命令的 hello:
   
        # sudo chkconfig network on

8. 如果您想要 toouse hello OpenLogic 鏡像 hello Azure 資料中心內裝載，然後取代 hello`/etc/yum.repos.d/CentOS-Base.repo`以 hello 下列儲存機制的檔案。  這也會加入 hello **[openlogic]**包含例如 hello Azure Linux 代理程式的其他封裝的儲存機制：

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
    hello 本指南的其餘部分將假設您使用至少 hello`[openlogic]`儲存機制，將會使用的 tooinstall hello Azure Linux 代理程式下方。


9. 加入下列行 too/etc/yum.conf hello:
    
        http_caching=packages

10. 執行下列命令 tooclear hello 目前 yum 中繼資料和更新 hello 系統與 hello 最新的套件 hello:
    
        # yum clean all

    除非您要建立較舊版本的 CentOS 的映像，我們建議所有 hello 的 tooupdate 封裝 toohello 最新版本：

        # sudo yum -y update

    執行此命令之後可能需要重新開機。

11. （選擇性）安裝 hello hello Linux Integration Services (LIS) 的驅動程式。
   
    >[!IMPORTANT]
    hello 步驟是**必要**CentOS 6.3 和更早版本，及更新版本的選擇性的。

        # sudo rpm -e hypervkvpd  ## (may return error if not installed, that's OK)
        # sudo yum install microsoft-hyper-v

    或者，您可以依照 hello 手動安裝指示，在 hello [LIS 下載頁面](https://go.microsoft.com/fwlink/?linkid=403033)tooinstall hello RPM 到您的 VM。
 
12. 安裝 hello Azure Linux 代理程式和相依性：
    
        # sudo yum install python-pyasn1 WALinuxAgent
    
    如果沒有已移除步驟 3 中所述，hello NetworkManager 和 NetworkManager gnome 封裝將會移除 hello WALinuxAgent 封裝。


13. 修改 Azure hello 核心開機行幼蟲組態 tooinclude 其他核心參數中。 toodo，開啟`/boot/grub/menu.lst`文字編輯器中，並確保該 hello 預設核心包含下列參數的 hello:
    
        console=ttyS0 earlyprintk=ttyS0 rootdelay=300
    
    這也可確保所有的主控台訊息都會傳送 toohello 第一個序列連接埠，這可協助 Azure 偵錯問題的支援。
    
    除了上述 toohello 建議太*移除*hello 下列參數：
    
        rhgb quiet crashkernel=auto
    
    沒有適用於雲端環境，我們想要傳送 toohello 序列連接埠的所有 hello 記錄 toobe 圖形和無訊息的開機。  hello`crashkernel`選項可能會是左設定如有需要，但請注意，這個參數會減少 hello hello 128 MB 以上，VM 中可用的記憶體數量可能會造成問題 hello 較小的 VM 大小。

    >[!Important]
    CentOS 6.5 及更早版本也必須設定 hello 核心參數`numa=off`。 請參閱 Red Hat [KB 436883](https://access.redhat.com/solutions/436883)。

14. 請確定該 hello SSH 伺服器是在安裝並設定 toostart 開機時間。  這通常是 hello 預設值。

15. 不要在 hello OS 磁碟上建立的交換空間。
    
    hello Azure Linux 代理程式可以自動設定使用之後附加的 toohello VM 在 Azure 上佈建的 hello 本機資源磁碟的交換空間。 請注意該 hello 本機資源磁碟是*暫存*磁碟，以及可能會在取消佈建 hello VM 時清空。 在安裝之後 hello Azure Linux 代理程式 （請參閱上一個步驟），修改下列參數中的 hello`/etc/waagent.conf`適當地：
    
        ResourceDisk.Format=y
        ResourceDisk.Filesystem=ext4
        ResourceDisk.MountPoint=/mnt/resource
        ResourceDisk.EnableSwap=y
        ResourceDisk.SwapSizeMB=2048    ## NOTE: set this toowhatever you need it toobe.

16. 執行下列命令 toodeprovision hello 虛擬機器的 hello 並準備在 Azure 上佈建：
    
        # sudo waagent -force -deprovision
        # export HISTSIZE=0
        # logout

17. 在 Hyper-V 管理員中，依序按一下 [動作] -> [關閉]。 Linux VHD 是現在準備好 toobe 上傳 tooAzure。


- - -
## <a name="centos-70"></a>CentOS 7.0+
**CentOS 7 (和類似的衍生項目) 中的變更**

準備 Azure CentOS 7 虛擬機器是非常類似 tooCentOS 6，不過，有數個值得注意的重要差異：

* hello NetworkManager 封裝不會再與 hello Azure Linux 代理程式發生衝突。 依預設會安裝此封裝，建議您不要將它移除。
* GRUB2 現在用做 hello 預設開機載入器，因此編輯核心參數 hello 程序已變更 （請參閱下方）。
* XFS 現在是 hello 預設檔案系統。 如有需要，仍可以使用 hello ext4 檔案系統。

**組態步驟**

1. 在 HYPER-V 管理員 中，選取 hello 虛擬機器。

2. 按一下**連接**tooopen hello 虛擬機器的主控台視窗。

3. 建立或編輯 hello 檔案`/etc/sysconfig/network`並加入下列文字的 hello:
   
        NETWORKING=yes
        HOSTNAME=localhost.localdomain

4. 建立或編輯 hello 檔案`/etc/sysconfig/network-scripts/ifcfg-eth0`並加入下列文字的 hello:
   
        DEVICE=eth0
        ONBOOT=yes
        BOOTPROTO=dhcp
        TYPE=Ethernet
        USERCTL=no
        PEERDNS=yes
        IPV6INIT=no
        NM_CONTROLLED=no

5. 修改 udev 規則 tooavoid 產生 hello 乙太網路介面的靜態規則。 在 Microsoft Azure 或 Hyper-V 中複製虛擬機器時，這些規則可能會造成問題：
   
        # sudo ln -s /dev/null /etc/udev/rules.d/75-persistent-net-generator.rules

6. 如果您想要 toouse hello OpenLogic 鏡像 hello Azure 資料中心內裝載，然後取代 hello`/etc/yum.repos.d/CentOS-Base.repo`以 hello 下列儲存機制的檔案。  這也會加入 hello **[openlogic]**包含 hello Azure Linux 代理程式的封裝儲存機制：
   
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
    hello 本指南的其餘部分將假設您使用至少 hello`[openlogic]`儲存機制，將會使用的 tooinstall hello Azure Linux 代理程式下方。

7. 執行下列命令 tooclear hello 目前 yum 中繼資料的 hello 並安裝任何更新：
   
        # sudo yum clean all

    除非您要建立較舊版本的 CentOS 的映像，我們建議所有 hello 的 tooupdate 封裝 toohello 最新版本：

        # sudo yum -y update

    執行此命令之後可能需要重新開機。

8. 修改 Azure hello 核心開機行幼蟲組態 tooinclude 其他核心參數中。 toodo，開啟`/etc/default/grub`在文字編輯器，編輯 hello`GRUB_CMDLINE_LINUX`參數，例如：
   
        GRUB_CMDLINE_LINUX="rootdelay=300 console=ttyS0 earlyprintk=ttyS0 net.ifnames=0"
   
   這也可確保所有的主控台訊息都會傳送 toohello 第一個序列連接埠，這可協助 Azure 偵錯問題的支援。 它也會關閉 hello 新 CentOS 7 命名慣例的 Nic。 除了上述 toohello 建議太*移除*hello 下列參數：
   
        rhgb quiet crashkernel=auto
   
    沒有適用於雲端環境，我們想要傳送 toohello 序列連接埠的所有 hello 記錄 toobe 圖形和無訊息的開機。 hello`crashkernel`選項可能會是左設定如有需要，但請注意，這個參數會減少 hello hello 128 MB 以上，VM 中可用的記憶體數量可能會造成問題 hello 較小的 VM 大小。

9. 在您完成編輯`/etc/default/grub`每個以上版本，執行下列命令 toorebuild hello 幼蟲組態 hello:
   
        # sudo grub2-mkconfig -o /boot/grub2/grub.cfg

10. 如果建置 hello 映像從**VMWare、 VirtualBox 或 KVM:**請 hello HYPER-V 驅動程式隨附的 hello initramfs:
   
   編輯 `/etc/dracut.conf`，新增內容：
   
        add_drivers+=”hv_vmbus hv_netvsc hv_storvsc”
   
   重建 hello initramfs:
   
        # sudo dracut –f -v

11. 安裝 hello Azure Linux 代理程式和相依性：

        # sudo yum install python-pyasn1 WALinuxAgent
        # sudo systemctl enable waagent

12. 不要在 hello OS 磁碟上建立的交換空間。
   
   hello Azure Linux 代理程式可以自動設定使用之後附加的 toohello VM 在 Azure 上佈建的 hello 本機資源磁碟的交換空間。 請注意該 hello 本機資源磁碟是*暫存*磁碟，以及可能會在取消佈建 hello VM 時清空。 在安裝之後 hello Azure Linux 代理程式 （請參閱上一個步驟），修改下列參數中的 hello`/etc/waagent.conf`適當地：
   
        ResourceDisk.Format=y
        ResourceDisk.Filesystem=ext4
        ResourceDisk.MountPoint=/mnt/resource
        ResourceDisk.EnableSwap=y
        ResourceDisk.SwapSizeMB=2048    ## NOTE: set this toowhatever you need it toobe.

13. 執行下列命令 toodeprovision hello 虛擬機器的 hello 並準備在 Azure 上佈建：
   
        # sudo waagent -force -deprovision
        # export HISTSIZE=0
        # logout

14. 在 Hyper-V 管理員中，依序按一下 [動作] -> [關閉]。 Linux VHD 是現在準備好 toobe 上傳 tooAzure。

## <a name="next-steps"></a>後續步驟
您要現在準備好 toouse CentOS Linux 虛擬硬碟 toocreate 新虛擬機器在 Azure 中。 如果這是 hello 正在上傳 hello.vhd 檔案 tooAzure 的第一次，請參閱步驟 2 和 3 中的[建立和上傳包含 hello Linux 作業系統的虛擬硬碟](classic/create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)。

