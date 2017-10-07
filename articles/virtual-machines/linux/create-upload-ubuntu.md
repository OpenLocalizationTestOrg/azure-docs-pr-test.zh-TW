---
title: "aaaCreate 並上傳 Ubuntu Linux VHD 在 Azure 中"
description: "了解 toocreate 和上傳 Azure 虛擬硬碟 (VHD)，其中包含 Ubuntu Linux 作業系統。"
services: virtual-machines-linux
documentationcenter: 
author: szarkos
manager: timlt
editor: tysonn
tags: azure-resource-manager,azure-service-management
ms.assetid: 3e097959-84fc-4f6a-8cc8-35e087fd1542
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 02/02/2017
ms.author: szark
ms.openlocfilehash: cc546a487f769b32432a7e80ddcd0f6af44e201f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="prepare-an-ubuntu-virtual-machine-for-azure"></a>準備適用於 Azure 的 Ubuntu 虛擬機器
[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-both-include.md)]

## <a name="official-ubuntu-cloud-images"></a>官方 Ubuntu 雲端映像
Ubuntu 現在發佈官方 Azure VHD 提供下載 ( [http://cloud-images.ubuntu.com/](http://cloud-images.ubuntu.com/))。 如果您需要 toobuild 自己特製化的 Ubuntu 映像 azure，而非使用 hello 其下的手動程序正在使用這些已知的建議的 toostart 工作 Vhd，並視需要自訂。 hello 最新的映像版本永遠位於下列位置的 hello:

* Ubuntu 12.04/Precise︰ [ubuntu-12.04-server-cloudimg-amd64-disk1.vhd.zip](https://cloud-images.ubuntu.com/precise/current/precise-server-cloudimg-amd64-disk1.vhd.zip)
* Ubuntu 14.04/Trusty︰ [ubuntu-14.04-server-cloudimg-amd64-disk1.vhd.zip](http://cloud-images.ubuntu.com/releases/trusty/release/ubuntu-14.04-server-cloudimg-amd64-disk1.vhd.zip)
* Ubuntu 16.04/Xenial︰ [ubuntu-16.04-server-cloudimg-amd64-disk1.vhd.zip](http://cloud-images.ubuntu.com/releases/xenial/release/ubuntu-16.04-server-cloudimg-amd64-disk1.vhd.zip)

## <a name="prerequisites"></a>必要條件
本文假設您已安裝 Ubuntu Linux 作業系統 tooa 虛擬硬碟。 多個工具存在 toocreate.vhd 檔案，例如 HYPER-V 之類的虛擬化解決方案。 如需指示，請參閱[安裝 hello HYPER-V 角色和設定虛擬機器](http://technet.microsoft.com/library/hh846766.aspx)。

**Ubuntu 安裝注意事項**

* 另請參閱[一般 Linux 安裝注意事項](create-upload-generic.md#general-linux-installation-notes)，了解為 Azure 準備 Linux 的更多祕訣。
* hello VHDX 格式不支援在 Azure 中，只有**固定 VHD**。  您可以將使用 HYPER-V 管理員 hello 磁碟 tooVHD 格式轉換或 hello convert-vhd 指令程式。
* 當安裝 hello Linux 系統建議您使用標準的資料分割，而非 LVM （通常 hello 預設值為許多安裝）。 特別是當作業系統磁碟曾經需要附加 toobe tooanother VM 進行疑難排解，這樣可避免與複製 Vm，LVM 名稱衝突。 如果願意，您可以在資料磁碟上使用 [LVM](configure-lvm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) 或 [RAID](configure-raid.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)。
* 請勿設定 hello OS 磁碟交換資料分割。 hello Linux 代理程式可以設定的 toocreate 交換磁碟上的檔案 hello 暫存資源。  相關資訊位於下列 hello 步驟。
* 所有 hello Vhd 必須是 1 MB 的倍數的大小。

## <a name="manual-steps"></a>手動步驟
> [!NOTE]
> 然後再嘗試 toocreate 自己自訂的 Ubuntu 映像，azure，請考慮使用 hello 預先建置和測試映像從[http://cloud-images.ubuntu.com/](http://cloud-images.ubuntu.com/)改為。
> 
> 

1. Hello 選取中間窗格內的 HYPER-V 管理員，hello 虛擬機器。

2. 按一下**連接**tooopen hello 視窗 hello 虛擬機器。

3. 取代 hello hello 映像 toouse Ubuntu 的 Azure 儲存機制中的目前儲存機制。 hello 步驟會稍微不同，視 hello Ubuntu 版本而定。
   
    然後再編輯`/etc/apt/sources.list`，它會建議 toomake 備份：
   
        # sudo cp /etc/apt/sources.list /etc/apt/sources.list.bak

    Ubuntu 12.04：
   
        # sudo sed -i 's/[a-z][a-z].archive.ubuntu.com/azure.archive.ubuntu.com/g' /etc/apt/sources.list
        # sudo apt-get update

    Ubuntu 14.04：
   
        # sudo sed -i 's/[a-z][a-z].archive.ubuntu.com/azure.archive.ubuntu.com/g' /etc/apt/sources.list
        # sudo apt-get update

    Ubuntu 16.04：
   
        # sudo sed -i 's/[a-z][a-z].archive.ubuntu.com/azure.archive.ubuntu.com/g' /etc/apt/sources.list
        # sudo apt-get update

4. hello Ubuntu Azure 映像現在下列 hello*硬體啟用*(HWE) 核心。 藉由執行下列命令的 hello 更新 hello 作業系統 toohello 最新的核心：

    Ubuntu 12.04：
   
        # sudo apt-get update
        # sudo apt-get install linux-image-generic-lts-trusty linux-cloud-tools-generic-lts-trusty
        # sudo apt-get install hv-kvp-daemon-init
        (recommended) sudo apt-get dist-upgrade
   
        # sudo reboot
   
    Ubuntu 14.04：
   
        # sudo apt-get update
        # sudo apt-get install linux-image-virtual-lts-vivid linux-lts-vivid-tools-common
        # sudo apt-get install hv-kvp-daemon-init
        (recommended) sudo apt-get dist-upgrade
   
        # sudo reboot

    Ubuntu 16.04：
   
        # sudo apt-get update
        # sudo apt-get install linux-generic-hwe-16.04 linux-cloud-tools-generic-hwe-16.04
        (recommended) sudo apt-get dist-upgrade

        # sudo reboot

    **另請參閱：**
    - [https://wiki.ubuntu.com/Kernel/LTSEnablementStack](https://wiki.ubuntu.com/Kernel/LTSEnablementStack)
    - [https://wiki.ubuntu.com/Kernel/RollingLTSEnablementStack](https://wiki.ubuntu.com/Kernel/RollingLTSEnablementStack)


5. 修改 Azure hello 核心開機行幼蟲 tooinclude 其他核心參數。 此開啟 toodo`/etc/default/grub`在文字編輯器中，尋找名 hello 變數`GRUB_CMDLINE_LINUX_DEFAULT`（或視需要新增它） 並編輯 tooinclude hello 下列參數：
   
        GRUB_CMDLINE_LINUX_DEFAULT="console=tty1 console=ttyS0,115200n8 earlyprintk=ttyS0,115200 rootdelay=300"

    儲存並關閉此檔案，然後執行 `sudo update-grub`。 這可確保所有的主控台訊息都會傳送 toohello 第一個序列連接埠，這可協助 Azure 偵錯問題的技術支援。

6. 請確定該 hello SSH 伺服器是在安裝並設定 toostart 開機時間。  這通常是 hello 預設值。

7. 安裝 hello Azure Linux 代理程式：
   
        # sudo apt-get update
        # sudo apt-get install walinuxagent

    >[!Note]
    hello`walinuxagent`封裝可能會移除 hello`NetworkManager`和`NetworkManager-gnome`如果安裝封裝。

8. 執行下列命令 toodeprovision hello 虛擬機器的 hello 並準備在 Azure 上佈建：
   
        # sudo waagent -force -deprovision
        # export HISTSIZE=0
        # logout

9. 在 Hyper-V 管理員中，依序按一下 [動作] -> [關閉]。 Linux VHD 是現在準備好 toobe 上傳 tooAzure。

## <a name="next-steps"></a>後續步驟
您要現在準備好 toouse Ubuntu Linux 虛擬硬碟 toocreate 新虛擬機器在 Azure 中。 如果這是 hello 正在上傳 hello.vhd 檔案 tooAzure 的第一次，請參閱步驟 2 和 3 中的[建立和上傳包含 hello Linux 作業系統的虛擬硬碟](classic/create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)。

## <a name="references"></a>參考
Ubuntu 硬體啟用 (HWE) 核心：

* [http://blog.utlemming.org/2015/01/ubuntu-1404-azure-images-now-tracking.html](http://blog.utlemming.org/2015/01/ubuntu-1404-azure-images-now-tracking.html)
* [http://blog.utlemming.org/2015/02/1204-azure-cloud-images-now-using-hwe.html](http://blog.utlemming.org/2015/02/1204-azure-cloud-images-now-using-hwe.html)

