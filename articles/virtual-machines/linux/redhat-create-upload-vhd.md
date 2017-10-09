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
# <a name="prepare-a-red-hat-based-virtual-machine-for-azure"></a>準備適用於 Azure 的 Red Hat 型虛擬機器
在本文中，您將學習如何 tooprepare Red Hat Enterprise Linux (RHEL) 以用於 Azure 虛擬機器。 hello 是舊版的 RHEL 涵蓋在本文中 6.7 + 和 7.1 +。 涵蓋在本文章的 hello hypervisor 的準備為 HYPER-V、 核心為基礎的虛擬機器 (KVM) 和 VMware。 如需參加 Red Hat 雲端存取方案之資格需求的詳細資訊，請參閱 [Red Hat 雲端存取網站](http://www.redhat.com/en/technologies/cloud-computing/cloud-access)與[在 Azure 上執行 RHEL](https://access.redhat.com/ecosystem/ccsp/microsoft-azure)。

## <a name="prepare-a-red-hat-based-virtual-machine-from-hyper-v-manager"></a>從 Hyper-V 管理員準備 Red Hat 型虛擬機器

### <a name="prerequisites"></a>必要條件
本節假設您已經有取得 ISO 檔案的 hello Red Hat 網站，並已安裝的 hello RHEL 映像 tooa 虛擬硬碟 (VHD)。 如需有關如何 toouse HYPER-V 管理員 tooinstall 作業系統映像，請參閱[安裝 hello HYPER-V 角色和設定虛擬機器](http://technet.microsoft.com/library/hh846766.aspx)。

**RHEL 安裝注意事項**

* Azure 不支援 hello VHDX 格式。 Azure 只支援固定 VHD。 您可以使用 HYPER-V 管理員 tooconvert hello 磁碟 tooVHD 格式，或您可以使用 hello convert-vhd 指令程式。 如果您使用 VirtualBox，選取**固定大小**相對於的 toohello 預設建立 hello 磁碟時，動態配置選項。
* Azure 僅支援第 1 代虛擬機器。 您可以將第 1 代虛擬機器從 VHDX toohello VHD 檔案格式與動態擴充 tooa 固定大小磁碟。 您無法變更虛擬機器的世代。 如需詳細資訊，請參閱[應該在 Hyper-V 中建立第 1 代還是第 2 代的虛擬機器？](https://technet.microsoft.com/windows-server-docs/compute/hyper-v/plan/should-i-create-a-generation-1-or-2-virtual-machine-in-hyper-v)。
* hello hello VHD 允許的最大大小為 1023 GB。
* 當您安裝 Linux 作業系統 hello 時，我們建議您使用標準的資料分割，而不是邏輯磁碟區管理員 (LVM) 通常會是 hello 許多安裝的預設值。 此種做法可以避免 LVM 與複製的虛擬機器的名稱衝突，特別是如果您需要 tooattach 作業系統磁碟 tooanother 相同的虛擬機器進行疑難排解。 如果願意，您可以在資料磁碟上使用 [LVM](configure-raid.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) 或 [RAID](configure-lvm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)。
* 需要掛接通用磁碟格式 (UDF) 檔案系統的核心支援。 在 Azure，hello UDF 格式化的媒體上的第一個開機附加的 toohello 客體會將佈建組態 toohello hello Linux 虛擬機器。 hello Azure Linux 代理程式必須能夠 toomount hello UDF 檔案系統 tooread 其組態和佈建 hello 虛擬機器。
* 早於 2.6.37 hello Linux 核心版本不支援非統一記憶體存取 (NUMA) 在 HYPER-V 上具有較大的虛擬機器大小。 這個問題主要會影響用於 hello 上游的舊發佈 Red Hat 2.6.32 核心及已修正 RHEL 6.6 (核心-2.6.32-504) 中。 執行自訂的核心系統中，已經超過 2.6.37 或早於 2.6.32-504 RHEL 基礎核心必須設定 hello `numa=off` grub.conf hello 核心命令列啟動參數。 如需詳細資訊，請參閱 Red Hat [KB 436883](https://access.redhat.com/solutions/436883)。
* Hello 作業系統磁碟上未設定交換資料分割。 hello Linux 代理程式可以設定的 toocreate 交換磁碟上的檔案 hello 暫存資源。  在下列步驟的 hello 找相關資訊。
* 所有 VHD 的大小都必須是 1 MB 的倍數。

### <a name="prepare-a-rhel-6-virtual-machine-from-hyper-v-manager"></a>從 Hyper-V 管理員準備 RHEL 6 虛擬機器

1. 在 HYPER-V 管理員 中，選取 hello 虛擬機器。

2. 按一下**連接**tooopen hello 虛擬機器的主控台視窗。

3. RHEL 6 NetworkManager 可能會干擾 hello Azure Linux 代理程式。 解除安裝此套件，藉由執行下列命令的 hello:
   
        # sudo rpm -e --nodeps NetworkManager

4. 建立或編輯 hello`/etc/sysconfig/network`檔並加入下列文字的 hello:
   
        NETWORKING=yes
        HOSTNAME=localhost.localdomain

5. 建立或編輯 hello`/etc/sysconfig/network-scripts/ifcfg-eth0`檔並加入下列文字的 hello:
   
        DEVICE=eth0
        ONBOOT=yes
        BOOTPROTO=dhcp
        TYPE=Ethernet
        USERCTL=no
        PEERDNS=yes
        IPV6INIT=no

6. 移動 （或移除） hello udev 規則 tooavoid 產生 hello 乙太網路介面的靜態規則。 在 Microsoft Azure 或 Hyper-V 中複製虛擬機器時，這些規則會造成問題：

        # sudo ln -s /dev/null /etc/udev/rules.d/75-persistent-net-generator.rules
        
        # sudo rm -f /etc/udev/rules.d/70-persistent-net.rules

7. 請確定 hello 網路服務，將會執行下列命令的 hello 在開機時啟動：

        # sudo chkconfig network on

8. 藉由執行下列命令的 hello 註冊封裝 hello RHEL 儲存機制從 Red Hat 訂用帳戶 tooenable hello 的安裝：

        # sudo subscription-manager register --auto-attach --username=XXX --password=XXX

9. hello WALinuxAgent 封裝， `WALinuxAgent-<version>`，已排除 toohello Red Hat 額外項目儲存機制。 執行下列命令的 hello 啟用 hello 額外項目儲存機制：

        # subscription-manager repos --enable=rhel-6-server-extras-rpms

10. 修改 Azure hello 核心開機行幼蟲組態 tooinclude 其他核心參數中。 toodo 這項修改，開啟`/boot/grub/menu.lst`在文字編輯器中，並確認該 hello 預設核心中包含下列參數的 hello:
    
        console=ttyS0 earlyprintk=ttyS0 rootdelay=300
    
    這也可確保所有主控台會將訊息都傳送 toohello 第一個序列連接埠，這可協助 Azure 偵錯問題的支援。
    
    此外，我們建議您先移除 hello 下列參數：
    
        rhgb quiet crashkernel=auto
    
    沒有適用於雲端環境，我們想要傳送 toohello 序列連接埠的所有 hello 記錄 toobe 圖形和無訊息的開機。  您可以保留 hello`crashkernel`視設定選項。 請注意，此參數可減少 hello hello 128 MB 以上的虛擬機器中的可用記憶體數量。 此組態可能會對小型虛擬機器造成問題。

    >[!Important]
    RHEL 6.5 及更早版本也必須設定 hello`numa=off`核心參數。 請參閱 Red Hat [KB 436883](https://access.redhat.com/solutions/436883)。

11. 請確定該 hello 安全殼層 (SSH) 伺服器安裝，並在開機時，通常是 hello 預設設定 toostart。 修改下列行 /etc/ssh/sshd_config tooinclude hello:

        ClientAliveInterval 180

12. 執行下列命令的 hello 安裝 hello Azure Linux 代理程式：

        # sudo yum install WALinuxAgent

        # sudo chkconfig waagent on

    安裝 hello WALinuxAgent 套件移除 hello NetworkManager 和 NetworkManager gnome 封裝，如果在步驟 3 中沒有已移除。

13. 不要在 hello 作業系統磁碟上建立的交換空間。

    hello Azure Linux 代理程式可以自動使用 hello 本機資源磁碟附加的 toohello 虛擬機器之後，在 Azure 上佈建 hello 虛擬機器所設定交換空間。 請注意該本機資源磁碟是暫存磁碟和 hello 虛擬機器會解除佈建時，可能會清空其 hello。 Hello 上一個步驟中安裝 hello Azure Linux 代理程式之後，修改適當地遵循 /etc/waagent.conf 中的參數的 hello:

        ResourceDisk.Format=y
        ResourceDisk.Filesystem=ext4
        ResourceDisk.MountPoint=/mnt/resource
        ResourceDisk.EnableSwap=y
        ResourceDisk.SwapSizeMB=2048    ## NOTE: set this toowhatever you need it toobe.

14. 取消註冊 hello 訂用帳戶 （如有必要） 藉由執行下列命令的 hello:

        # sudo subscription-manager unregister

15. 執行下列命令 toodeprovision hello 虛擬機器的 hello 並準備在 Azure 上佈建：

        # sudo waagent -force -deprovision

        # export HISTSIZE=0

        # logout

16. 在 Hyper-V 管理員中，按一下 [動作] > [關閉]。 Linux VHD 是現在準備好 toobe 上傳 tooAzure。


### <a name="prepare-a-rhel-7-virtual-machine-from-hyper-v-manager"></a>從 Hyper-V 管理員準備 RHEL 7 虛擬機器

1. 在 HYPER-V 管理員 中，選取 hello 虛擬機器。

2. 按一下**連接**tooopen hello 虛擬機器的主控台視窗。

3. 建立或編輯 hello`/etc/sysconfig/network`檔並加入下列文字的 hello:
   
        NETWORKING=yes
        HOSTNAME=localhost.localdomain

4. 建立或編輯 hello`/etc/sysconfig/network-scripts/ifcfg-eth0`檔並加入下列文字的 hello:
   
        DEVICE=eth0
        ONBOOT=yes
        BOOTPROTO=dhcp
        TYPE=Ethernet
        USERCTL=no
        PEERDNS=yes
        IPV6INIT=no
        NM_CONTROLLED=no

5. 請確定 hello 網路服務，將會執行下列命令的 hello 在開機時啟動：

        # sudo chkconfig network on

6. 藉由執行下列命令的 hello 註冊封裝 hello RHEL 儲存機制從 Red Hat 訂用帳戶 tooenable hello 的安裝：

        # sudo subscription-manager register --auto-attach --username=XXX --password=XXX

7. 修改 Azure hello 核心開機行幼蟲組態 tooinclude 其他核心參數中。 toodo 這項修改，開啟`/etc/default/grub`在文字編輯器，編輯 hello`GRUB_CMDLINE_LINUX`參數。 例如：
   
        GRUB_CMDLINE_LINUX="rootdelay=300 console=ttyS0 earlyprintk=ttyS0 net.ifnames=0"
   
   這也可確保所有主控台會將訊息都傳送 toohello 第一個序列連接埠，這可協助 Azure 偵錯問題的支援。 這項設定也會關閉 hello 新增 RHEL 7 命名慣例的 Nic。 此外，我們建議您移除 hello 下列參數：
   
        rhgb quiet crashkernel=auto
   
    沒有適用於雲端環境，我們想要傳送 toohello 序列連接埠的所有 hello 記錄 toobe 圖形和無訊息的開機。 您可以保留 hello`crashkernel`視設定選項。 請注意，此參數減少 hello 128 MB 以上，hello 虛擬機器中的可用記憶體的數量可能較小的虛擬機器大小會造成問題。

8. 完成之後編輯`/etc/default/grub`，請執行 hello 命令 toorebuild hello 幼蟲設定下列：

        # sudo grub2-mkconfig -o /boot/grub2/grub.cfg

9. 請確定該 hello SSH 伺服器安裝，並在開機時，通常是 hello 預設設定 toostart。 修改`/etc/ssh/sshd_config`tooinclude hello 下列行：

        ClientAliveInterval 180

10. hello WALinuxAgent 封裝， `WALinuxAgent-<version>`，已排除 toohello Red Hat 額外項目儲存機制。 執行下列命令的 hello 啟用 hello 額外項目儲存機制：

        # subscription-manager repos --enable=rhel-7-server-extras-rpms

11. 執行下列命令的 hello 安裝 hello Azure Linux 代理程式：

        # sudo yum install WALinuxAgent

        # sudo systemctl enable waagent.service

12. 不要在 hello 作業系統磁碟上建立的交換空間。

    hello Azure Linux 代理程式可以自動使用 hello 本機資源磁碟附加的 toohello 虛擬機器之後，在 Azure 上佈建 hello 虛擬機器所設定交換空間。 請注意，hello 本機資源磁碟是暫存磁碟，它可能會取消佈建 hello 虛擬機器時清空。 Hello 上一個步驟中安裝 hello Azure Linux 代理程式之後，修改下列參數中的 hello`/etc/waagent.conf`適當地：

        ResourceDisk.Format=y
        ResourceDisk.Filesystem=ext4
        ResourceDisk.MountPoint=/mnt/resource
        ResourceDisk.EnableSwap=y
        ResourceDisk.SwapSizeMB=2048    ## NOTE: set this toowhatever you need it toobe.

13. 如果您想 toounregister hello 訂用帳戶，執行下列命令的 hello:

        # sudo subscription-manager unregister

14. 執行下列命令 toodeprovision hello 虛擬機器的 hello 並準備在 Azure 上佈建：

        # sudo waagent -force -deprovision

        # export HISTSIZE=0

        # logout

15. 在 Hyper-V 管理員中，按一下 [動作] > [關閉]。 Linux VHD 是現在準備好 toobe 上傳 tooAzure。


## <a name="prepare-a-red-hat-based-virtual-machine-from-kvm"></a>從 KVM 準備 Red Hat 型虛擬機器
### <a name="prepare-a-rhel-6-virtual-machine-from-kvm"></a>從 KVM 準備 RHEL 6 虛擬機器

1. Hello Red Hat 網站下載 RHEL 6 hello KVM 映的像。

2. 設定根密碼。

    產生加密的密碼，並將複製 hello hello 命令輸出：

        # openssl passwd -1 changeme

    使用 guestfish 設定根密碼：
        
        # guestfish --rw -a <image-name>
        > <fs> run
        > <fs> list-filesystems
        > <fs> mount /dev/sda1 /
        > <fs> vi /etc/shadow
        > <fs> exit

   變更 hello 第二個欄位的 hello 根使用者從 「!!" toohello 加密的密碼。

3. KVM 中建立虛擬機器，從 hello qcow2 映像。 設定得 hello 磁碟類型**qcow2**，並設定 hello 虛擬網路介面裝置型號太**virtio**。 然後，啟動 hello 虛擬機器，並為根登入。

4. 建立或編輯 hello`/etc/sysconfig/network`檔並加入下列文字的 hello:
   
        NETWORKING=yes
        HOSTNAME=localhost.localdomain

5. 建立或編輯 hello`/etc/sysconfig/network-scripts/ifcfg-eth0`檔並加入下列文字的 hello:
   
        DEVICE=eth0
        ONBOOT=yes
        BOOTPROTO=dhcp
        TYPE=Ethernet
        USERCTL=no
        PEERDNS=yes
        IPV6INIT=no

6. 移動 （或移除） hello udev 規則 tooavoid 產生 hello 乙太網路介面的靜態規則。 在 Azure 或 Hyper-V 中複製虛擬機器時，這些規則會造成問題：

        # sudo ln -s /dev/null /etc/udev/rules.d/75-persistent-net-generator.rules

        # sudo rm -f /etc/udev/rules.d/70-persistent-net.rules

7. 請確定 hello 網路服務，將會執行下列命令的 hello 在開機時啟動：

        # chkconfig network on

8. 藉由執行下列命令的 hello 註冊封裝 hello RHEL 儲存機制從 Red Hat 訂用帳戶 tooenable hello 的安裝：

        # subscription-manager register --auto-attach --username=XXX --password=XXX

9. 修改 Azure hello 核心開機行幼蟲組態 tooinclude 其他核心參數中。 toodo 此設定，請開啟`/boot/grub/menu.lst`在文字編輯器中，並確認該 hello 預設核心中包含下列參數的 hello:
    
        console=ttyS0 earlyprintk=ttyS0 rootdelay=300
    
    這也可確保所有主控台會將訊息都傳送 toohello 第一個序列連接埠，這可協助 Azure 偵錯問題的支援。
    
    此外，我們建議您移除 hello 下列參數：
    
        rhgb quiet crashkernel=auto
    
    沒有適用於雲端環境，我們想要傳送 toohello 序列連接埠的所有 hello 記錄 toobe 圖形和無訊息的開機。 您可以保留 hello`crashkernel`視設定選項。 請注意，此參數減少 hello 128 MB 以上，hello 虛擬機器中的可用記憶體的數量可能較小的虛擬機器大小會造成問題。

    >[!Important]
    RHEL 6.5 及更早版本也必須設定 hello`numa=off`核心參數。 請參閱 Red Hat [KB 436883](https://access.redhat.com/solutions/436883)。

10. 新增 HYPER-V 模組 tooinitramfs:  

    編輯`/etc/dracut.conf`，並加入下列內容的 hello:

        add_drivers+="hv_vmbus hv_netvsc hv_storvsc"

    重建 initramfs：

        # dracut -f -v

11. 解除安裝 cloud-init：

        # yum remove cloud-init

12. 請確定該 hello SSH 伺服器是在安裝並設定 toostart 開機時間：

        # chkconfig sshd on

    修改下列行 /etc/ssh/sshd_config tooinclude hello:

        PasswordAuthentication yes
        ClientAliveInterval 180

13. hello WALinuxAgent 封裝， `WALinuxAgent-<version>`，已排除 toohello Red Hat 額外項目儲存機制。 執行下列命令的 hello 啟用 hello 額外項目儲存機制：

        # subscription-manager repos --enable=rhel-6-server-extras-rpms

14. 執行下列命令的 hello 安裝 hello Azure Linux 代理程式：

        # yum install WALinuxAgent

        # chkconfig waagent on

15. hello Azure Linux 代理程式可以自動使用 hello 本機資源磁碟附加的 toohello 虛擬機器之後，在 Azure 上佈建 hello 虛擬機器所設定交換空間。 請注意，hello 本機資源磁碟是暫存磁碟，它可能會取消佈建 hello 虛擬機器時清空。 Hello 上一個步驟中安裝 hello Azure Linux 代理程式之後，修改下列參數中的 hello **/etc/waagent.conf**適當地：

        ResourceDisk.Format=y
        ResourceDisk.Filesystem=ext4
        ResourceDisk.MountPoint=/mnt/resource
        ResourceDisk.EnableSwap=y
        ResourceDisk.SwapSizeMB=2048    ## NOTE: set this toowhatever you need it toobe.

16. 取消註冊 hello 訂用帳戶 （如有必要） 藉由執行下列命令的 hello:

        # subscription-manager unregister

17. 執行下列命令 toodeprovision hello 虛擬機器的 hello 並準備在 Azure 上佈建：

        # waagent -force -deprovision

        # export HISTSIZE=0

        # logout

18. 關閉 hello KVM 中的虛擬機器。

19. 將 hello qcow2 映像 toohello VHD 格式的轉換。

    第一次轉換 hello 影像 tooraw 格式：

        # qemu-img convert -f qcow2 -O raw rhel-6.8.qcow2 rhel-6.8.raw

    請確定 hello hello 原始影像大小配合 1 MB。 否則，無條件進位 hello 與 1 MB 的大小 tooalign:

        # MB=$((1024*1024))
        # size=$(qemu-img info -f raw --output json "rhel-6.8.raw" | \
          gawk 'match($0, /"virtual-size": ([0-9]+),/, val) {print val[1]}')

        # rounded_size=$((($size/$MB + 1)*$MB))
        # qemu-img resize rhel-6.8.raw $rounded_size

    轉換 hello 原始磁碟 tooa 固定大小的 VHD:

        # qemu-img convert -f raw -o subformat=fixed -O vpc rhel-6.8.raw rhel-6.8.vhd


### <a name="prepare-a-rhel-7-virtual-machine-from-kvm"></a>從 KVM 準備 RHEL 7 虛擬機器

1. Hello Red Hat 網站下載 RHEL 7 hello KVM 映的像。 此程序使用 RHEL 7 hello 範例。

2. 設定根密碼。

    產生加密的密碼，並將複製 hello hello 命令輸出：

        # openssl passwd -1 changeme

    使用 guestfish 設定根密碼：

        # guestfish --rw -a <image-name>
        > <fs> run
        > <fs> list-filesystems
        > <fs> mount /dev/sda1 /
        > <fs> vi /etc/shadow
        > <fs> exit

   變更 hello 第二個欄位的根使用者從 「!!" toohello 加密的密碼。

3. KVM 中建立虛擬機器，從 hello qcow2 映像。 設定得 hello 磁碟類型**qcow2**，並設定 hello 虛擬網路介面裝置型號太**virtio**。 然後，啟動 hello 虛擬機器，並為根登入。

4. 建立或編輯 hello`/etc/sysconfig/network`檔並加入下列文字的 hello:
   
        NETWORKING=yes
        HOSTNAME=localhost.localdomain

5. 建立或編輯 hello`/etc/sysconfig/network-scripts/ifcfg-eth0`檔並加入下列文字的 hello:
   
        DEVICE=eth0
        ONBOOT=yes
        BOOTPROTO=dhcp
        TYPE=Ethernet
        USERCTL=no
        PEERDNS=yes
        IPV6INIT=no
        NM_CONTROLLED=no

6. 請確定 hello 網路服務，將會執行下列命令的 hello 在開機時啟動：

        # chkconfig network on

7. 藉由執行下列命令的 hello 註冊封裝從 hello RHEL 儲存機制的 Red Hat 訂用帳戶 tooenable 安裝：

        # subscription-manager register --auto-attach --username=XXX --password=XXX

8. 修改 Azure hello 核心開機行幼蟲組態 tooinclude 其他核心參數中。 toodo 此設定，請開啟`/etc/default/grub`在文字編輯器，編輯 hello`GRUB_CMDLINE_LINUX`參數。 例如：
   
        GRUB_CMDLINE_LINUX="rootdelay=300 console=ttyS0 earlyprintk=ttyS0 net.ifnames=0"
   
   此命令也可確保所有主控台會將訊息都傳送 toohello 第一個序列連接埠，這可協助 Azure 偵錯問題的支援。 hello 命令也會關閉 hello 新增 RHEL 7 命名慣例的 Nic。 此外，我們建議您移除 hello 下列參數：
   
        rhgb quiet crashkernel=auto
   
    沒有適用於雲端環境，我們想要傳送 toohello 序列連接埠的所有 hello 記錄 toobe 圖形和無訊息的開機。 您可以保留 hello`crashkernel`視設定選項。 請注意，此參數減少 hello 128 MB 以上，hello 虛擬機器中的可用記憶體的數量可能較小的虛擬機器大小會造成問題。

9. 完成之後編輯`/etc/default/grub`，請執行 hello 命令 toorebuild hello 幼蟲設定下列：

        # grub2-mkconfig -o /boot/grub2/grub.cfg

10. 將 Hyper-V 模組新增至 initramfs。

    編輯 `/etc/dracut.conf` 並加入內容：

        add_drivers+="hv_vmbus hv_netvsc hv_storvsc"

    重建 initramfs：

        # dracut -f -v

11. 解除安裝 cloud-init：

        # yum remove cloud-init

12. 請確定該 hello SSH 伺服器是在安裝並設定 toostart 開機時間：

        # systemctl enable sshd

    修改下列行 /etc/ssh/sshd_config tooinclude hello:

        PasswordAuthentication yes
        ClientAliveInterval 180

13. hello WALinuxAgent 封裝， `WALinuxAgent-<version>`，已排除 toohello Red Hat 額外項目儲存機制。 執行下列命令的 hello 啟用 hello 額外項目儲存機制：

        # subscription-manager repos --enable=rhel-7-server-extras-rpms

14. 執行下列命令的 hello 安裝 hello Azure Linux 代理程式：

        # yum install WALinuxAgent

    啟用 hello waagent 服務：

        # systemctl enable waagent.service

15. 不要在 hello 作業系統磁碟上建立的交換空間。

    hello Azure Linux 代理程式可以自動使用 hello 本機資源磁碟附加的 toohello 虛擬機器之後，在 Azure 上佈建 hello 虛擬機器所設定交換空間。 請注意，hello 本機資源磁碟是暫存磁碟，它可能會取消佈建 hello 虛擬機器時清空。 Hello 上一個步驟中安裝 hello Azure Linux 代理程式之後，修改下列參數中的 hello`/etc/waagent.conf`適當地：

        ResourceDisk.Format=y
        ResourceDisk.Filesystem=ext4
        ResourceDisk.MountPoint=/mnt/resource
        ResourceDisk.EnableSwap=y
        ResourceDisk.SwapSizeMB=2048    ## NOTE: set this toowhatever you need it toobe.

16. 取消註冊 hello 訂用帳戶 （如有必要） 藉由執行下列命令的 hello:

        # subscription-manager unregister

17. 執行下列命令 toodeprovision hello 虛擬機器的 hello 並準備在 Azure 上佈建：

        # sudo waagent -force -deprovision

        # export HISTSIZE=0

        # logout

18. 關閉 hello KVM 中的虛擬機器。

19. 將 hello qcow2 映像 toohello VHD 格式的轉換。

    第一次轉換 hello 影像 tooraw 格式：

        # qemu-img convert -f qcow2 -O raw rhel-7.3.qcow2 rhel-7.3.raw

    請確定 hello hello 原始影像大小配合 1 MB。 否則，無條件進位 hello 與 1 MB 的大小 tooalign:

        # MB=$((1024*1024))
        # size=$(qemu-img info -f raw --output json "rhel-6.8.raw" | \
          gawk 'match($0, /"virtual-size": ([0-9]+),/, val) {print val[1]}')

        # rounded_size=$((($size/$MB + 1)*$MB))
        # qemu-img resize rhel-6.8.raw $rounded_size

    轉換 hello 原始磁碟 tooa 固定大小的 VHD:

        # qemu-img convert -f raw -o subformat=fixed -O vpc rhel-7.3.raw rhel-7.3.vhd

## <a name="prepare-a-red-hat-based-virtual-machine-from-vmware"></a>從 VMware 準備 Red Hat 型虛擬機器
### <a name="prerequisites"></a>必要條件
本節假設您已在 VMware 中安裝 RHEL 虛擬機器。 如需詳細資訊，關於如何 tooinstall 作業系統在 VMware 中，請參閱[VMware 來賓作業系統安裝指南](http://partnerweb.vmware.com/GOSIG/home.html)。

* 當您安裝 Linux 作業系統 hello 時，我們建議您使用標準的資料分割，而不是 LVM，這通常是 hello 許多安裝的預設值。 這樣可避免 LVM 與複製的虛擬機器的名稱衝突，特別是當作業系統磁碟需要附加 toobe tooanother 虛擬機器進行疑難排解。 如果願意，您可以在資料磁碟上使用 LVM 或 RAID。
* Hello 作業系統磁碟上未設定交換資料分割。 您可以設定 hello Linux 代理程式 toocreate 交換磁碟上的檔案 hello 暫存資源。 您可以在 hello 面的步驟中找到相關資訊。
* 當您建立虛擬硬碟 hello 時，選取**存放區的虛擬磁碟當做單一檔案**。

### <a name="prepare-a-rhel-6-virtual-machine-from-vmware"></a>從 VMWare 準備 RHEL 6 虛擬機器
1. RHEL 6 NetworkManager 可能會干擾 hello Azure Linux 代理程式。 解除安裝此套件，藉由執行下列命令的 hello:
   
        # sudo rpm -e --nodeps NetworkManager

2. 建立名為**網路**hello /etc/sysconfig/目錄中包含 hello 下列文字：

        NETWORKING=yes
        HOSTNAME=localhost.localdomain

3. 建立或編輯 hello`/etc/sysconfig/network-scripts/ifcfg-eth0`檔並加入下列文字的 hello:
   
        DEVICE=eth0
        ONBOOT=yes
        BOOTPROTO=dhcp
        TYPE=Ethernet
        USERCTL=no
        PEERDNS=yes
        IPV6INIT=no

4. 移動 （或移除） hello udev 規則 tooavoid 產生 hello 乙太網路介面的靜態規則。 在 Azure 或 Hyper-V 中複製虛擬機器時，這些規則會造成問題：

        # sudo ln -s /dev/null /etc/udev/rules.d/75-persistent-net-generator.rules

        # sudo rm -f /etc/udev/rules.d/70-persistent-net.rules

5. 請確定 hello 網路服務，將會執行下列命令的 hello 在開機時啟動：

        # sudo chkconfig network on

6. 藉由執行下列命令的 hello 註冊封裝 hello RHEL 儲存機制從 Red Hat 訂用帳戶 tooenable hello 的安裝：

        # sudo subscription-manager register --auto-attach --username=XXX --password=XXX

7. hello WALinuxAgent 封裝， `WALinuxAgent-<version>`，已排除 toohello Red Hat 額外項目儲存機制。 執行下列命令的 hello 啟用 hello 額外項目儲存機制：

        # subscription-manager repos --enable=rhel-6-server-extras-rpms

8. 修改 Azure hello 核心開機行幼蟲組態 tooinclude 其他核心參數中。 toodo，開啟`/etc/default/grub`在文字編輯器，編輯 hello`GRUB_CMDLINE_LINUX`參數。 例如：
   
        GRUB_CMDLINE_LINUX="rootdelay=300 console=ttyS0 earlyprintk=ttyS0"
   
   這也可確保所有主控台會將訊息都傳送 toohello 第一個序列連接埠，這可協助 Azure 偵錯問題的支援。 此外，我們建議您移除 hello 下列參數：
   
        rhgb quiet crashkernel=auto
   
    沒有適用於雲端環境，我們想要傳送 toohello 序列連接埠的所有 hello 記錄 toobe 圖形和無訊息的開機。 您可以保留 hello`crashkernel`視設定選項。 請注意，此參數減少 hello 128 MB 以上，hello 虛擬機器中的可用記憶體的數量可能較小的虛擬機器大小會造成問題。

9. 新增 HYPER-V 模組 tooinitramfs:

    編輯`/etc/dracut.conf`，並加入下列內容的 hello:

        add_drivers+="hv_vmbus hv_netvsc hv_storvsc"

    重建 initramfs：

        # dracut -f -v

10. 請確定該 hello SSH 伺服器安裝，並在開機時，通常是 hello 預設設定 toostart。 修改`/etc/ssh/sshd_config`tooinclude hello 下列行：

    ClientAliveInterval 180

11. 執行下列命令的 hello 安裝 hello Azure Linux 代理程式：

        # sudo yum install WALinuxAgent

        # sudo chkconfig waagent on

12. 不要在 hello 作業系統磁碟上建立的交換空間。

    hello Azure Linux 代理程式可以自動使用 hello 本機資源磁碟附加的 toohello 虛擬機器之後，在 Azure 上佈建 hello 虛擬機器所設定交換空間。 請注意，hello 本機資源磁碟是暫存磁碟，它可能會取消佈建 hello 虛擬機器時清空。 Hello 上一個步驟中安裝 hello Azure Linux 代理程式之後，修改下列參數中的 hello`/etc/waagent.conf`適當地：

        ResourceDisk.Format=y
        ResourceDisk.Filesystem=ext4
        ResourceDisk.MountPoint=/mnt/resource
        ResourceDisk.EnableSwap=y
        ResourceDisk.SwapSizeMB=2048    ## NOTE: set this toowhatever you need it toobe.

13. 取消註冊 hello 訂用帳戶 （如有必要） 藉由執行下列命令的 hello:

        # sudo subscription-manager unregister

14. 執行下列命令 toodeprovision hello 虛擬機器的 hello 並準備在 Azure 上佈建：

        # sudo waagent -force -deprovision

        # export HISTSIZE=0

        # logout

15. 關閉 hello 虛擬機器，並將轉換 hello VMDK 檔案 tooa.vhd 檔案。

    第一次轉換 hello 影像 tooraw 格式：

        # qemu-img convert -f vmdk -O raw rhel-6.8.vmdk rhel-6.8.raw

    請確定 hello hello 原始影像大小配合 1 MB。 否則，無條件進位 hello 與 1 MB 的大小 tooalign:

        # MB=$((1024*1024))
        # size=$(qemu-img info -f raw --output json "rhel-6.8.raw" | \
          gawk 'match($0, /"virtual-size": ([0-9]+),/, val) {print val[1]}')

        # rounded_size=$((($size/$MB + 1)*$MB))
        # qemu-img resize rhel-6.8.raw $rounded_size

    轉換 hello 原始磁碟 tooa 固定大小的 VHD:

        # qemu-img convert -f raw -o subformat=fixed -O vpc rhel-6.8.raw rhel-6.8.vhd

### <a name="prepare-a-rhel-7-virtual-machine-from-vmware"></a>從 VMWare 準備 RHEL 7 虛擬機器
1. 建立或編輯 hello`/etc/sysconfig/network`檔並加入下列文字的 hello:
   
        NETWORKING=yes
        HOSTNAME=localhost.localdomain

2. 建立或編輯 hello`/etc/sysconfig/network-scripts/ifcfg-eth0`檔並加入下列文字的 hello:
   
        DEVICE=eth0
        ONBOOT=yes
        BOOTPROTO=dhcp
        TYPE=Ethernet
        USERCTL=no
        PEERDNS=yes
        IPV6INIT=no
        NM_CONTROLLED=no

3. 請確定 hello 網路服務，將會執行下列命令的 hello 在開機時啟動：

        # sudo chkconfig network on

4. 藉由執行下列命令的 hello 註冊封裝 hello RHEL 儲存機制從 Red Hat 訂用帳戶 tooenable hello 的安裝：

        # sudo subscription-manager register --auto-attach --username=XXX --password=XXX

5. 修改 Azure hello 核心開機行幼蟲組態 tooinclude 其他核心參數中。 toodo 這項修改，開啟`/etc/default/grub`在文字編輯器，編輯 hello`GRUB_CMDLINE_LINUX`參數。 例如：
   
        GRUB_CMDLINE_LINUX="rootdelay=300 console=ttyS0 earlyprintk=ttyS0 net.ifnames=0"
   
   這項設定也可確保所有主控台會將訊息都傳送 toohello 第一個序列連接埠，這可協助 Azure 偵錯問題的支援。 它也會關閉 hello 新增 RHEL 7 命名慣例的 Nic。 此外，我們建議您移除 hello 下列參數：
   
        rhgb quiet crashkernel=auto
   
    沒有適用於雲端環境，我們想要傳送 toohello 序列連接埠的所有 hello 記錄 toobe 圖形和無訊息的開機。 您可以保留 hello`crashkernel`視設定選項。 請注意，此參數減少 hello 128 MB 以上，hello 虛擬機器中的可用記憶體的數量可能較小的虛擬機器大小會造成問題。

6. 完成之後編輯`/etc/default/grub`，請執行 hello 命令 toorebuild hello 幼蟲設定下列：

        # sudo grub2-mkconfig -o /boot/grub2/grub.cfg

7. 新增 HYPER-V 模組 tooinitramfs。

    編輯 `/etc/dracut.conf`，新增內容：

        add_drivers+="hv_vmbus hv_netvsc hv_storvsc"

    重建 initramfs：

        # dracut -f -v

8. 請確定該 hello SSH 伺服器是在安裝並設定 toostart 開機時間。 這項設定通常是 hello 預設值。 修改`/etc/ssh/sshd_config`tooinclude hello 下列行：

        ClientAliveInterval 180

9. hello WALinuxAgent 封裝， `WALinuxAgent-<version>`，已排除 toohello Red Hat 額外項目儲存機制。 執行下列命令的 hello 啟用 hello 額外項目儲存機制：

        # subscription-manager repos --enable=rhel-7-server-extras-rpms

10. 執行下列命令的 hello 安裝 hello Azure Linux 代理程式：

        # sudo yum install WALinuxAgent

        # sudo systemctl enable waagent.service

11. 不要在 hello 作業系統磁碟上建立的交換空間。

    hello Azure Linux 代理程式可以自動使用 hello 本機資源磁碟附加的 toohello 虛擬機器之後，在 Azure 上佈建 hello 虛擬機器所設定交換空間。 請注意，hello 本機資源磁碟是暫存磁碟，它可能會取消佈建 hello 虛擬機器時清空。 Hello 上一個步驟中安裝 hello Azure Linux 代理程式之後，修改下列參數中的 hello`/etc/waagent.conf`適當地：

        ResourceDisk.Format=y
        ResourceDisk.Filesystem=ext4
        ResourceDisk.MountPoint=/mnt/resource
        ResourceDisk.EnableSwap=y
        ResourceDisk.SwapSizeMB=2048    ## NOTE: set this toowhatever you need it toobe.

12. 如果您想 toounregister hello 訂用帳戶，執行下列命令的 hello:

        # sudo subscription-manager unregister

13. 執行下列命令 toodeprovision hello 虛擬機器的 hello 並準備在 Azure 上佈建：

        # sudo waagent -force -deprovision

        # export HISTSIZE=0

        # logout

14. 關閉 hello 虛擬機器，並將轉換 hello VMDK 檔案 toohello VHD 格式。

    第一次轉換 hello 影像 tooraw 格式：

        # qemu-img convert -f vmdk -O raw rhel-7.3.vmdk rhel-7.3.raw

    請確定 hello hello 原始影像大小配合 1 MB。 否則，無條件進位 hello 與 1 MB 的大小 tooalign:

        # MB=$((1024*1024))
        # size=$(qemu-img info -f raw --output json "rhel-6.8.raw" | \
          gawk 'match($0, /"virtual-size": ([0-9]+),/, val) {print val[1]}')

        # rounded_size=$((($size/$MB + 1)*$MB))
        # qemu-img resize rhel-6.8.raw $rounded_size

    轉換 hello 原始磁碟 tooa 固定大小的 VHD:

        # qemu-img convert -f raw -o subformat=fixed -O vpc rhel-7.3.raw rhel-7.3.vhd

## <a name="prepare-a-red-hat-based-virtual-machine-from-an-iso-by-using-a-kickstart-file-automatically"></a>使用 kickstart 檔案自動從 ISO 準備 Red Hat 型虛擬機器
### <a name="prepare-a-rhel-7-virtual-machine-from-a-kickstart-file"></a>從 kickstart 檔案準備 RHEL 7 虛擬機器

1.  建立包含下列內容，hello 啟動檔案，並儲存 hello 檔案。 如需有關啟動安裝的詳細資訊，請參閱 hello[啟動安裝指南](https://access.redhat.com/documentation/en-US/Red_Hat_Enterprise_Linux/7/html/Installation_Guide/chap-kickstart-installations.html)。

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

2. 將 hello 安裝系統可以存取的 hello 啟動檔案。

3. 在 Hyper-V 管理員中建立新的虛擬機器。 在 hello**連接虛擬硬碟**頁面上，選取**稍後連結虛擬硬碟**，和完整 hello 新增虛擬機器精靈。

4. 開啟 hello 虛擬機器設定：

    a.  附加新的虛擬硬碟 toohello 虛擬機器。 請確定 tooselect **VHD 格式**和**固定的大小**。

    b.  附加 hello 安裝 ISO toohello DVD 光碟機。

    c.  設定 hello BIOS tooboot 從光碟片。

5. 啟動 hello 虛擬機器。 當出現 hello 安裝指南時，請按 **索引標籤**tooconfigure hello 開機選項。

6. Enter`inst.ks=<hello location of hello kickstart file>`結尾 hello hello 開機選項，然後按**Enter**。

7. 等候 hello 安裝 toofinish。 完成後，hello 虛擬機器將會自動關閉。 Linux VHD 是現在準備好 toobe 上傳 tooAzure。

## <a name="known-issues"></a>已知問題
### <a name="hello-hyper-v-driver-could-not-be-included-in-hello-initial-ram-disk-when-using-a-non-hyper-v-hypervisor"></a>hello HYPER-V 驅動程式可能不會包含在 hello 初始 RAM 磁碟使用非 HYPER-V hypervisor 時

在某些情況下，Linux 的安裝程式可能不包括 hello 驅動程式之 HYPER-V 的 hello 初始 RAM 磁碟 （initrd 或 initramfs） 除非 Linux 偵測它在 HYPER-V 環境中執行。

當您使用不同虛擬化 （亦即 Virtualbox、 Xen 等） 的系統 tooprepare Linux 映像時，您可能需要至少 hello hv_vmbus 的 toorebuild initrd tooensure 且 hv_storvsc 核心模組可 hello 初始 RAM 磁碟上。 這在至少 hello 上游 Red Hat 發佈為基礎的系統上是已知的問題。

tooresolve 這個問題，請新增 HYPER-V 模組 tooinitramfs 再重建它：

編輯`/etc/dracut.conf`，並加入下列內容的 hello:

        add_drivers+="hv_vmbus hv_netvsc hv_storvsc"

重建 initramfs：

        # dracut -f -v

如需詳細資訊，請參閱 hello 資訊[重建 initramfs](https://access.redhat.com/solutions/1958)。

## <a name="next-steps"></a>後續步驟
您要現在準備好 toouse Red Hat Enterprise Linux 虛擬硬碟 toocreate 新虛擬機器在 Azure 中。 如果這是 hello 正在上傳 hello.vhd 檔案 tooAzure 的第一次，請參閱步驟 2 和 3 中的[建立和上傳包含 hello Linux 作業系統的虛擬硬碟](classic/create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)。

如需更多詳細的 hello hypervisor 認證 toorun Red Hat Enterprise Linux，請參閱[hello Red Hat 網站](https://access.redhat.com/certified-hypervisors)。
