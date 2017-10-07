---
title: "在 Azure 中的 VHD Debian Linux aaaPrepare |Microsoft 文件"
description: "了解如何 toocreate Debian 7 和 8 的 VHD 檔案部署在 Azure 中。"
services: virtual-machines-linux
documentationcenter: 
author: szarkos
manager: timlt
editor: 
tags: azure-resource-manager,azure-service-management
ms.assetid: a6de7a7c-cc70-44e7-aed0-2ae6884d401a
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 02/02/2017
ms.author: szark
ms.openlocfilehash: e67d126de3db146357a6509aedb5f478576768f0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="prepare-a-debian-vhd-for-azure"></a>準備適用於 Azure 的 Debian VHD
## <a name="prerequisites"></a>必要條件
本節假設您已經有安裝 Debian Linux 作業系統從.iso 檔案從 hello 下載[Debian 網站](https://www.debian.org/distrib/)tooa 虛擬硬碟。 多個工具存在 toocreate.vhd 檔案。HYPER-V 是一個範例。 使用 HYPER-V 的指示，請參閱[安裝 hello HYPER-V 角色和設定虛擬機器](https://technet.microsoft.com/library/hh846766.aspx)。

## <a name="installation-notes"></a>安裝注意事項
* 另請參閱[一般 Linux 安裝注意事項](create-upload-generic.md#general-linux-installation-notes)，了解為 Azure 準備 Linux 的更多祕訣。
* 在 Azure 中不支援 hello 較新的 VHDX 格式。 您可以將轉換 hello 磁碟 tooVHD 格式使用 HYPER-V 管理員] 或 [hello**轉換-vhd** cmdlet。
* 當安裝 hello Linux 系統建議您使用標準的資料分割，而非 LVM （通常 hello 預設值為許多安裝）。 特別是當作業系統磁碟曾經需要附加 toobe tooanother VM 進行疑難排解，這樣可避免與複製 Vm，LVM 名稱衝突。 如果願意，您可以在資料磁碟上使用 [LVM](configure-lvm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) 或 [RAID](configure-raid.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)。
* 請勿設定 hello OS 磁碟交換資料分割。 hello Azure Linux 代理程式可以設定的 toocreate 交換磁碟上的檔案 hello 暫存資源。 相關資訊位於下列 hello 步驟。
* 所有 hello Vhd 必須是 1 MB 的倍數的大小。

## <a name="use-azure-manage-toocreate-debian-vhds"></a>使用 Azure 管理 toocreate Debian Vhd
有工具可用於產生 Debian Vhd azure，例如 hello [azure-管理](https://github.com/credativ/azure-manage)指令碼從[credativ](http://www.credativ.com/)。 這是建議的方法與從頭開始建立映像的 hello。 例如，toocreate Debian 8 VHD 執行 hello 遵循 toodownload azure 管理的命令 （和相依性），然後執行 hello azure_build_image 指令碼：

    # sudo apt-get update
    # sudo apt-get install git qemu-utils mbr kpartx debootstrap

    # sudo apt-get install python3-pip python3-dateutil python3-cryptography
    # sudo pip3 install azure-storage azure-servicemanagement-legacy azure-common pytest pyyaml
    # git clone https://github.com/credativ/azure-manage.git
    # cd azure-manage
    # sudo pip3 install .

    # sudo azure_build_image --option release=jessie --option image_size_gb=30 --option image_prefix=debian-jessie-azure section


## <a name="manually-prepare-a-debian-vhd"></a>手動準備 Debian VHD
1. 在 HYPER-V 管理員 中，選取 hello 虛擬機器。
2. 按一下**連接**tooopen hello 虛擬機器的主控台視窗。
3. 註解 hello 列**deb cdrom**中`/etc/apt/source.list`如果您設定 hello VM 根據 ISO 檔案。
4. 編輯 hello`/etc/default/grub`檔案，並修改 hello **GRUB_CMDLINE_LINUX**如下 tooinclude 其他核心參數適用於 Azure 的參數。
   
        GRUB_CMDLINE_LINUX="console=tty0 console=ttyS0,115200 earlyprintk=ttyS0,115200 rootdelay=30"
5. 重建 hello 幼蟲並執行：
   
        # sudo update-grub
6. 新增 Debian 的 Azure 儲存機制 too/etc/apt/sources.list Debian 7 或 8:
   
    **Debian 7.x "Wheezy"**
   
        deb http://debian-archive.trafficmanager.net/debian wheezy-backports main
        deb-src http://debian-archive.trafficmanager.net/debian wheezy-backports main
        deb http://debian-archive.trafficmanager.net/debian-azure wheezy main
        deb-src http://debian-archive.trafficmanager.net/debian-azure wheezy main

    **Debian 8.x "Jessie"**

        deb http://debian-archive.trafficmanager.net/debian jessie-backports main
        deb-src http://debian-archive.trafficmanager.net/debian jessie-backports main
        deb http://debian-archive.trafficmanager.net/debian-azure jessie main
        deb-src http://debian-archive.trafficmanager.net/debian-azure jessie main


1. 安裝 hello Azure Linux 代理程式：
   
        # sudo apt-get update
        # sudo apt-get install waagent
2. Debian 7，則是必要的 toorun hello 3.16 基礎核心 hello wheezy backports 儲存機制中。 先建立檔案，稱為 /etc/apt/preferences.d/linux.pref 以 hello 下列內容：
   
        Package: linux-image-amd64 initramfs-tools
        Pin: release n=wheezy-backports
        Pin-Priority: 500
   
    然後，執行 sudo apt get 安裝 linux-映像-amd64 」 tooinstall hello 新的核心。
3. 取消佈建 hello 虛擬機器並準備在 Azure 上佈建，然後執行：
   
        # sudo waagent –force -deprovision
        # export HISTSIZE=0
        # logout
4. 在 Hyper-V 管理員中，依序按一下 [動作] -> [關閉]。 Linux VHD 是現在準備好 toobe 上傳 tooAzure。

## <a name="next-steps"></a>後續步驟
您要現在準備好 toouse Debian 虛擬硬碟 toocreate 新虛擬機器在 Azure 中。 如果這是 hello 正在上傳 hello.vhd 檔案 tooAzure 的第一次，請參閱步驟 2 和 3 中的[建立和上傳包含 hello Linux 作業系統的虛擬硬碟](classic/create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)。

