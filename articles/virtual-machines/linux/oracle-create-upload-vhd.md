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
# <a name="prepare-an-oracle-linux-virtual-machine-for-azure"></a>準備用於 Azure 的 Oracle Linux 虛擬機器
[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-both-include.md)]

## <a name="prerequisites"></a>必要條件
本文假設您已安裝 Oracle Linux 作業系統 tooa 虛擬硬碟。 多個工具存在 toocreate.vhd 檔案，例如 HYPER-V 之類的虛擬化解決方案。 如需指示，請參閱[安裝 hello HYPER-V 角色和設定虛擬機器](http://technet.microsoft.com/library/hh846766.aspx)。

### <a name="oracle-linux-installation-notes"></a>Oracle Linux 安裝注意事項
* 如需有關準備 Azure 之 Linux 的更多秘訣，另請參閱 [一般 Linux 安裝注意事項](create-upload-generic.md#general-linux-installation-notes) 。
* Hyper-V 和 Azure 都支援 Oracle 的 Red Hat 相容核心及其 UEK3 (Unbreakable Enterprise Kernel)。 為獲得最佳結果，請確定 tooupdate toohello 最新的核心是準備 Oracle Linux VHD 時。
* Oracle 的 UEK2 不會支援在 HYPER-V 和 Azure 上，因為它不包含所需的 hello 驅動程式。
* hello VHDX 格式不支援在 Azure 中，只有**固定 VHD**。  您可以將使用 HYPER-V 管理員 hello 磁碟 tooVHD 格式轉換或 hello convert-vhd 指令程式。
* 當安裝 hello Linux 系統建議您使用標準的資料分割，而非 LVM （通常 hello 預設值為許多安裝）。 特別是當作業系統磁碟曾經需要附加 toobe tooanother VM 進行疑難排解，這樣可避免與複製 Vm，LVM 名稱衝突。 如果願意，您可以在資料磁碟上使用 [LVM](configure-lvm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) 或 [RAID](configure-raid.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)。
* 較大的 VM 大小，因為 tooa bug 下方 2.6.37 Linux 核心版本中不支援 NUMA。 這個問題主要影響使用散發 hello 上游 Red Hat 2.6.32 核心。 手動安裝的 hello Azure Linux 代理程式 (waagent) 會自動停用 NUMA hello Linux 核心 hello 幼蟲組態中。 相關資訊位於下列 hello 步驟。
* 請勿設定 hello OS 磁碟交換資料分割。 hello Linux 代理程式可以設定的 toocreate 交換磁碟上的檔案 hello 暫存資源。  相關資訊位於下列 hello 步驟。
* 所有 hello Vhd 必須是 1 MB 的倍數的大小。
* 請確定該 hello`Addons`儲存機制已啟用。 編輯 hello 檔案`/etc/yum.repo.d/public-yum-ol6.repo`(Oracle Linux 6) 或`/etc/yum.repo.d/public-yum-ol7.repo`(Oracle Linux)，並變更 hello 行`enabled=0`太`enabled=1`下**[ol6_addons]**或**[ol7_addons]**中檔案。

## <a name="oracle-linux-64"></a>Oracle Linux 6.4+
您必須完成的 hello Azure 中的虛擬機器 toorun hello 作業系統中的特定設定步驟。

1. Hello 選取中間窗格內的 HYPER-V 管理員，hello 虛擬機器。
2. 按一下**連接**tooopen hello 視窗 hello 虛擬機器。
3. 解除安裝 NetworkManager，藉由執行下列命令的 hello:
   
        # sudo rpm -e --nodeps NetworkManager
   
    **注意：**如果尚未安裝 hello 封裝，此命令將會失敗並出現錯誤訊息。 這是預期行為。
4. 建立名為**網路**在 hello`/etc/sysconfig/`目錄，包含下列文字的 hello:
   
        NETWORKING=yes
        HOSTNAME=localhost.localdomain
5. 建立名為**ifcfg eth0**在 hello`/etc/sysconfig/network-scripts/`目錄，包含下列文字的 hello:
   
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
   
        # chkconfig network on
8. 安裝 python pyasn1 藉由執行下列命令的 hello:
   
        # sudo yum install python-pyasn1
9. 修改 Azure hello 核心開機行幼蟲組態 tooinclude 其他核心參數中。 此開啟 toodo"/ boot/grub/menu.lst 「 文字編輯器中並確認該 hello 預設核心中包含下列參數的 hello:
   
        console=ttyS0 earlyprintk=ttyS0 rootdelay=300 numa=off
   
   這也可確保所有的主控台訊息都會傳送 toohello 第一個序列連接埠，這可協助 Azure 偵錯問題的支援。 這會停用 NUMA，因為 Oracle 的 Red Hat 相容核心 tooa bug。
   
   除了上述 toohello 建議太*移除*hello 下列參數：
   
        rhgb quiet crashkernel=auto
   
   沒有適用於雲端環境，我們想要傳送 toohello 序列連接埠的所有 hello 記錄 toobe 圖形和無訊息的開機。
   
   hello`crashkernel`選項可能會是左設定如有需要，但請注意，這個參數會減少 hello hello 128 MB 以上，VM 中可用的記憶體數量可能會造成問題 hello 較小的 VM 大小。
10. 請確定該 hello SSH 伺服器是在安裝並設定 toostart 開機時間。  這通常是 hello 預設值。
11. 執行下列命令的 hello 安裝 hello Azure Linux 代理程式。 hello 最新版本是 2.0.15。
    
        # sudo yum install WALinuxAgent
    
    請注意，安裝 hello WALinuxAgent 封裝將會移除 hello NetworkManager NetworkManager gnome 封裝沒有已移除所述，是否在步驟 2。
12. 不要在 hello OS 磁碟上建立的交換空間。
    
    hello Azure Linux 代理程式可以自動設定使用之後附加的 toohello VM 在 Azure 上佈建的 hello 本機資源磁碟的交換空間。 請注意該 hello 本機資源磁碟是*暫存*磁碟，以及可能會在取消佈建 hello VM 時清空。 在安裝之後 hello Azure Linux 代理程式 （請參閱上一個步驟），修改適當地遵循 /etc/waagent.conf 中的參數的 hello:
    
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

- - -
## <a name="oracle-linux-70"></a>Oracle Linux 7.0+
**Oracle Linux 7 中的變更**

準備 Azure 的 Oracle Linux 7 虛擬機器是非常類似 tooOracle Linux 6，不過，有數個值得注意的重要差異：

* Azure 支援 hello Red Hat 相容核心和 Oracle 的 UEK3。  建議您使用 hello UEK3 核心。
* hello NetworkManager 封裝不會再與 hello Azure Linux 代理程式發生衝突。 依預設會安裝此封裝，建議您不要將它移除。
* GRUB2 現在用做 hello 預設開機載入器，因此編輯核心參數 hello 程序已變更 （請參閱下方）。
* XFS 現在是 hello 預設檔案系統。 如有需要，仍可以使用 hello ext4 檔案系統。

**組態步驟**

1. 在 HYPER-V 管理員 中，選取 hello 虛擬機器。
2. 按一下**連接**tooopen hello 虛擬機器的主控台視窗。
3. 建立名為**網路**在 hello`/etc/sysconfig/`目錄，包含下列文字的 hello:
   
        NETWORKING=yes
        HOSTNAME=localhost.localdomain
4. 建立名為**ifcfg eth0**在 hello`/etc/sysconfig/network-scripts/`目錄，包含下列文字的 hello:
   
        DEVICE=eth0
        ONBOOT=yes
        BOOTPROTO=dhcp
        TYPE=Ethernet
        USERCTL=no
        PEERDNS=yes
        IPV6INIT=no
5. 修改 udev 規則 tooavoid 產生 hello 乙太網路介面的靜態規則。 在 Microsoft Azure 或 Hyper-V 中複製虛擬機器時，這些規則可能會造成問題：
   
        # sudo ln -s /dev/null /etc/udev/rules.d/75-persistent-net-generator.rules
6. 請確定 hello 網路服務將會在開機時啟動藉由執行下列命令的 hello:
   
        # sudo chkconfig network on
7. 執行下列命令的 hello 安裝 hello python pyasn1 封裝：
   
        # sudo yum install python-pyasn1
8. 執行下列命令 tooclear hello 目前 yum 中繼資料的 hello 並安裝任何更新：
   
        # sudo yum clean all
        # sudo yum -y update
9. 修改 Azure hello 核心開機行幼蟲組態 tooinclude 其他核心參數中。 此開啟"/ 等/預設/幼蟲"toodo 在文字編輯器，編輯 hello`GRUB_CMDLINE_LINUX`參數，例如：
   
        GRUB_CMDLINE_LINUX="rootdelay=300 console=ttyS0 earlyprintk=ttyS0 net.ifnames=0"
   
   這也可確保所有的主控台訊息都會傳送 toohello 第一個序列連接埠，這可協助 Azure 偵錯問題的支援。 它也會關閉 hello 新 OEL 7 命名慣例的 Nic。 除了上述 toohello 建議太*移除*hello 下列參數：
   
       rhgb quiet crashkernel=auto
   
   沒有適用於雲端環境，我們想要傳送 toohello 序列連接埠的所有 hello 記錄 toobe 圖形和無訊息的開機。
   
   hello`crashkernel`選項可能會是左設定如有需要，但請注意，這個參數會減少 hello hello 128 MB 以上，VM 中可用的記憶體數量可能會造成問題 hello 較小的 VM 大小。
10. 在您完成編輯"/ 等/預設/幼蟲"每個以上版本，執行下列命令 toorebuild hello 幼蟲組態 hello:
    
        # sudo grub2-mkconfig -o /boot/grub2/grub.cfg
11. 請確定該 hello SSH 伺服器是在安裝並設定 toostart 開機時間。  這通常是 hello 預設值。
12. 執行下列命令的 hello 安裝 hello Azure Linux 代理程式：
    
        # sudo yum install WALinuxAgent
        # sudo systemctl enable waagent
13. 不要在 hello OS 磁碟上建立的交換空間。
    
    hello Azure Linux 代理程式可以自動設定使用之後附加的 toohello VM 在 Azure 上佈建的 hello 本機資源磁碟的交換空間。 請注意該 hello 本機資源磁碟是*暫存*磁碟，以及可能會在取消佈建 hello VM 時清空。 在安裝之後 hello Azure Linux 代理程式 （請參閱 hello 上一個步驟），修改適當地遵循 /etc/waagent.conf 中的參數的 hello:
    
        ResourceDisk.Format=y
        ResourceDisk.Filesystem=ext4
        ResourceDisk.MountPoint=/mnt/resource
        ResourceDisk.EnableSwap=y
        ResourceDisk.SwapSizeMB=2048    ## NOTE: set this toowhatever you need it toobe.
14. 執行下列命令 toodeprovision hello 虛擬機器的 hello 並準備在 Azure 上佈建：
    
        # sudo waagent -force -deprovision
        # export HISTSIZE=0
        # logout
15. 在 Hyper-V 管理員中，依序按一下 [動作] -> [關閉]。 Linux VHD 是現在準備好 toobe 上傳 tooAzure。

## <a name="next-steps"></a>後續步驟
您要現在準備好 toouse Oracle Linux.vhd toocreate 新虛擬機器在 Azure 中。 如果這是 hello 正在上傳 hello.vhd 檔案 tooAzure 的第一次，請參閱步驟 2 和 3 中的[建立和上傳包含 hello Linux 作業系統的虛擬硬碟](classic/create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)。

