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
# <a name="prepare-a-sles-or-opensuse-virtual-machine-for-azure"></a>準備適用於 Azure 的 SLES 或 openSUSE 虛擬機器
[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-both-include.md)]

## <a name="prerequisites"></a>必要條件
本文假設您有已安裝 SUSE 或 openSUSE Linux 作業系統 tooa 虛擬硬碟。 多個工具存在 toocreate.vhd 檔案，例如 HYPER-V 之類的虛擬化解決方案。 如需指示，請參閱[安裝 hello HYPER-V 角色和設定虛擬機器](http://technet.microsoft.com/library/hh846766.aspx)。

### <a name="sles--opensuse-installation-notes"></a>SLES / openSUSE 安裝注意事項
* 另請參閱[一般 Linux 安裝注意事項](create-upload-generic.md#general-linux-installation-notes)，了解為 Azure 準備 Linux 的更多祕訣。
* hello VHDX 格式不支援在 Azure 中，只有**固定 VHD**。  您可以將使用 HYPER-V 管理員 hello 磁碟 tooVHD 格式轉換或 hello convert-vhd 指令程式。
* 當安裝 hello Linux 系統建議您使用標準的資料分割，而非 LVM （通常 hello 預設值為許多安裝）。 特別是當作業系統磁碟曾經需要附加 toobe tooanother VM 進行疑難排解，這樣可避免與複製 Vm，LVM 名稱衝突。 如果願意，您可以在資料磁碟上使用 [LVM](configure-lvm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) 或 [RAID](configure-raid.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)。
* 請勿設定 hello OS 磁碟交換資料分割。 hello Linux 代理程式可以設定的 toocreate 交換磁碟上的檔案 hello 暫存資源。  相關資訊位於下列 hello 步驟。
* 所有 hello Vhd 必須是 1 MB 的倍數的大小。

## <a name="use-suse-studio"></a>使用 SUSE Studio
[SUSE Studio](http://www.susestudio.com) 可讓您輕鬆建立及管理 Azure 和 Hyper-V 的 SLES 與 openSUSE 映像。 這是建議的方法，自訂您自己 SLES 和 openSUSE 映像的 hello。

做為替代的 toobuilding 您自己的 VHD、 SUSE 也發行 BYOS （攜帶您自己訂閱） 映像在 sles [VMDepot](https://vmdepot.msopentech.com/User/Show?user=1007)。

## <a name="prepare-suse-linux-enterprise-server-11-sp4"></a>準備 SUSE Linux Enterprise Server 11 SP4
1. Hello 選取中間窗格內的 HYPER-V 管理員，hello 虛擬機器。
2. 按一下**連接**tooopen hello 視窗 hello 虛擬機器。
3. 註冊您的 SUSE Linux Enterprise 系統 tooallow 它 toodownload 更新及安裝套件。
4. 更新 hello 系統 hello 最新修補程式：
   
        # sudo zypper update
5. 從 hello SLES 儲存機制安裝 hello Azure Linux 代理程式：
   
        # sudo zypper install WALinuxAgent
6. 存回是否 「 開啟 」 太設定 waagent chkconfig，而且如果沒有，請啟用自動啟動：
   
        # sudo chkconfig waagent on
7. 檢查 waagent 服務是否正在執行，若否，請加以啟動： 
   
        # sudo service waagent start
8. 修改 Azure hello 核心開機行幼蟲組態 tooinclude 其他核心參數中。 此開啟 toodo"/ boot/grub/menu.lst 「 文字編輯器中並確認該 hello 預設核心中包含下列參數的 hello:
   
        console=ttyS0 earlyprintk=ttyS0 rootdelay=300
   
    這可確保所有的主控台訊息都會傳送 toohello 第一個序列連接埠，這可協助 Azure 偵錯問題的支援。
9. 請確認該 /boot/grub/menu.lst 和 /etc/hosts fstab 而 hello 磁碟識別碼 (由-id) 不使用其 UUID (由-uuid) 這兩個參考 hello 磁碟。 
   
    取得磁碟 UUID
   
        # ls /dev/disk/by-uuid/
   
    如果 /dev/disk/by-id / hello 的 uuid 的適當值，更新 /boot/grub/menu.lst 和 /etc/hosts fstab
   
    變更之前
   
        root=/dev/disk/by-id/SCSI-xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxxx-part1
   
    變更之後
   
        root=/dev/disk/by-uuid/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx
10. 修改 udev 規則 tooavoid 產生 hello 乙太網路介面的靜態規則。 在 Microsoft Azure 或 Hyper-V 中複製虛擬機器時，這些規則可能會造成問題：
    
        # sudo ln -s /dev/null /etc/udev/rules.d/75-persistent-net-generator.rules
        # sudo rm -f /etc/udev/rules.d/70-persistent-net.rules
11. 建議 tooedit hello 檔案"/ 等/sysconfig/網路/dhcp"，並變更 hello`DHCLIENT_SET_HOSTNAME`參數 toohello 下列：
    
     DHCLIENT_SET_HOSTNAME="no"
12. 在"/etc/hosts sudoers"，標記為註解或移除下列行，如果它們存在 hello:
    
     預設值 targetpw # 詢問 hello hello 也就是根所有 ALL=(ALL) 所有的目標使用者的密碼 # 警告 ！ 僅搭配 'Defaults targetpw'! 使用這個項目
13. 請確定該 hello SSH 伺服器是在安裝並設定 toostart 開機時間。  這通常是 hello 預設值。
14. 不要在 hello OS 磁碟上建立的交換空間。
    
    hello Azure Linux 代理程式可以自動設定使用之後附加的 toohello VM 在 Azure 上佈建的 hello 本機資源磁碟的交換空間。 請注意該 hello 本機資源磁碟是*暫存*磁碟，以及可能會在取消佈建 hello VM 時清空。 在安裝之後 hello Azure Linux 代理程式 （請參閱上一個步驟），修改適當地遵循 /etc/waagent.conf 中的參數的 hello:
    
     ResourceDisk.Format=y ResourceDisk.Filesystem=ext4 ResourceDisk.MountPoint=/mnt/resource ResourceDisk.EnableSwap=y ResourceDisk.SwapSizeMB=&#2048; # 注意： 設定 toobe 需要此 toowhatever。
15. 執行下列命令 toodeprovision hello 虛擬機器的 hello 並準備在 Azure 上佈建：
    
    # <a name="sudo-waagent--force--deprovision"></a>sudo waagent -force -deprovision
    # <a name="export-histsize0"></a>export HISTSIZE=0
    # <a name="logout"></a>logout
16. 在 Hyper-V 管理員中，依序按一下 [動作] -> [關閉]。 Linux VHD 是現在準備好 toobe 上傳 tooAzure。

- - -
## <a name="prepare-opensuse-131"></a>準備執行 openSUSE 13.1+
1. Hello 選取中間窗格內的 HYPER-V 管理員，hello 虛擬機器。
2. 按一下**連接**tooopen hello 視窗 hello 虛擬機器。
3. 在 hello 殼層執行 hello 命令 '`zypper lr`'。 如果此命令會傳回，輸出類似 toohello 然後 hello 儲存機制已如預期般-沒有進行調整所需遵循 （請注意，版本號碼可能不同）：
   
        # | Alias                 | Name                  | Enabled | Refresh
        --+-----------------------+-----------------------+---------+--------
        1 | Cloud:Tools_13.1      | Cloud:Tools_13.1      | Yes     | Yes
        2 | openSUSE_13.1_OSS     | openSUSE_13.1_OSS     | Yes     | Yes
        3 | openSUSE_13.1_Updates | openSUSE_13.1_Updates | Yes     | Yes
   
    如果 hello 命令會不傳回 「...定義任何儲存機制 」 請使用下列命令 tooadd hello 這些儲存機制：
   
        # sudo zypper ar -f http://download.opensuse.org/repositories/Cloud:Tools/openSUSE_13.1 Cloud:Tools_13.1
        # sudo zypper ar -f http://download.opensuse.org/distribution/13.1/repo/oss openSUSE_13.1_OSS
        # sudo zypper ar -f http://download.opensuse.org/update/13.1 openSUSE_13.1_Updates
   
    您可以確認已執行 hello 命令加入 hello 儲存機制 '`zypper lr`' 一次。 萬一 hello 的相關更新儲存機制的其中一個未啟用，則會啟用使用下列命令：
   
        # sudo zypper mr -e [NUMBER OF REPOSITORY]
4. 更新 hello 核心 toohello 最新可用版本：
   
        # sudo zypper up kernel-default
   
    Tooupdate hello 具備或系統的所有 hello 最新修補程式：
   
        # sudo zypper update
5. 安裝 hello Azure Linux 代理程式。
   
   # <a name="sudo-zypper-install-walinuxagent"></a>sudo zypper install WALinuxAgent
6. 修改 Azure hello 核心開機行幼蟲組態 tooinclude 其他核心參數中。 toodo，開啟 「 / boot/grub/menu.lst 「 文字編輯器中，並確保該 hello 預設核心包含下列參數的 hello:
   
     console=ttyS0 earlyprintk=ttyS0 rootdelay=300
   
   這可確保所有的主控台訊息都會傳送 toohello 第一個序列連接埠，這可協助 Azure 偵錯問題的支援。 此外，移除 hello hello 核心開機行中的下列參數，如果它們存在：
   
     libata.atapi_enabled=0 reserve=0x1f0,0x8
7. 建議 tooedit hello 檔案"/ 等/sysconfig/網路/dhcp"，並變更 hello`DHCLIENT_SET_HOSTNAME`參數 toohello 下列：
   
     DHCLIENT_SET_HOSTNAME="no"
8. **重要事項：** "/etc/hosts sudoers 」，在標記為註解或移除下列行，如果它們存在 hello:
   
     預設值 targetpw # 詢問 hello hello 也就是根所有 ALL=(ALL) 所有的目標使用者的密碼 # 警告 ！ 僅搭配 'Defaults targetpw'! 使用這個項目
9. 請確定該 hello SSH 伺服器是在安裝並設定 toostart 開機時間。  這通常是 hello 預設值。
10. 不要在 hello OS 磁碟上建立的交換空間。
    
    hello Azure Linux 代理程式可以自動設定使用之後附加的 toohello VM 在 Azure 上佈建的 hello 本機資源磁碟的交換空間。 請注意該 hello 本機資源磁碟是*暫存*磁碟，以及可能會在取消佈建 hello VM 時清空。 在安裝之後 hello Azure Linux 代理程式 （請參閱上一個步驟），修改適當地遵循 /etc/waagent.conf 中的參數的 hello:
    
     ResourceDisk.Format=y ResourceDisk.Filesystem=ext4 ResourceDisk.MountPoint=/mnt/resource ResourceDisk.EnableSwap=y ResourceDisk.SwapSizeMB=&#2048; # 注意： 設定 toobe 需要此 toowhatever。
11. 執行下列命令 toodeprovision hello 虛擬機器的 hello 並準備在 Azure 上佈建：
    
    # <a name="sudo-waagent--force--deprovision"></a>sudo waagent -force -deprovision
    # <a name="export-histsize0"></a>export HISTSIZE=0
    # <a name="logout"></a>logout
12. 請確定在啟動時執行 Azure Linux 代理程式的 hello:
    
        # sudo systemctl enable waagent.service
13. 在 Hyper-V 管理員中，依序按一下 [動作] -> [關閉]。 Linux VHD 是現在準備好 toobe 上傳 tooAzure。

## <a name="next-steps"></a>後續步驟
您要現在準備好 toouse SUSE Linux 虛擬硬碟 toocreate 新虛擬機器在 Azure 中。 如果這是 hello 正在上傳 hello.vhd 檔案 tooAzure 的第一次，請參閱步驟 2 和 3 中的[建立和上傳包含 hello Linux 作業系統的虛擬硬碟](classic/create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)。

