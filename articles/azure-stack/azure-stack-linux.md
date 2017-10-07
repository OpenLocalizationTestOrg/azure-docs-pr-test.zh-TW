---
title: "Azure 堆疊上的 aaaLinux 遊客 |Microsoft 文件"
description: "了解如何在 Azure Stack 上建立 Linux 式虛擬機器。"
services: azure-stack
documentationcenter: 
author: anjayajodha
manager: byronr
editor: 
ms.assetid: d2155c59-902e-4f63-ac58-d19e6a765380
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 7/10/2017
ms.author: anajod
ms.openlocfilehash: 225bed7d630b676ca760add25731e347516b5bf7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-linux-virtual-machines-on-azure-stack"></a>在 Azure Stack 上部署 Linux 虛擬機器
您可以將以 Linux 為基礎的映像新增至 hello Marketplace</堆疊部署 Linux 虛擬機器上 hello Azure 堆疊開發套件。 已有數個 Linux 廠商提供可新增到 Azure Stack 開發套件中的映像，您也可以建立自己的映像。

## <a name="download-an-image"></a>下載映像
1. 從下列連結，hello 擷取 Azure 堆疊相容映像或準備您自己和 下載：
   
   * [Bitnami](https://bitnami.com/azure-stack)
   * [CentOS](http://olstacks.cloudapp.net/latest/)
   * [CoreOS](https://stable.release.core-os.net/amd64-usr/current/coreos_production_azure_image.vhd.bz2)
   * [SuSE](https://download.suse.com/Download?buildid=VCFi7y7MsFQ~)
   * [Ubuntu 14.04 LTS](https://partner-images.canonical.com/azure/azure_stack/) / [Ubuntu 16.04 LTS](http://cloud-images.ubuntu.com/releases/xenial/release/ubuntu-16.04-server-cloudimg-amd64-disk1.vhd.zip)
2. 如有必要，請解壓縮 hello 映像 VHD 和[新增 hello 映像 toohello Marketplace](azure-stack-add-vm-image.md)。 請確定該 hello`OSType`參數設定太`Linux`。
3. 您加入 hello 映像 toohello Marketplace 之後，建立 Marketplace 項目，而且您可以部署 Linux 虛擬機器。

## <a name="prepare-your-own-image"></a>準備您自己的映像
1. 準備您自己使用其中一種 hello 下列指示的 Linux 映像：
   
   * [CentOS 型發行版本](../virtual-machines/linux/create-upload-centos.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
   * [Debian Linux](../virtual-machines/linux/debian-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
   * [Oracle Linux](../virtual-machines/linux/oracle-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
   * [Red Hat Enterprise Linux](../virtual-machines/linux/redhat-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
   * [SLES 和 openSUSE](../virtual-machines/linux/suse-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
   * [Ubuntu](../virtual-machines/linux/create-upload-ubuntu.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
2. 下載並安裝 hello [Azure Linux 代理程式](https://github.com/Azure/WALinuxAgent/)
   
    hello Azure Linux 代理程式版本 2.1.3 或更高版本需要的 tooprovision 您 Azure 堆疊上的 Linux VM。 許多已上面所列的 hello 分佈在其儲存機制中包含或更高套件 hello 代理程式的這個版本 (通常稱為`WALinuxAgent`或`walinuxagent`)。 不過，如果 hello hello Azure 代理程式套件的版本將會小於 2.1.3 （也就是 2.0.18 或更低），則您必須手動安裝 hello 代理程式。 可以判斷安裝的 hello 版本，從 hello 封裝名稱，或是藉由執行`/usr/sbin/waagent -version`hello VM 上。
   
    手動-請遵循以下 tooinstall hello Azure Linux 代理程式的 hello 指示
   
   * 首先，下載 hello 最新 Azure Linux 代理程式從[GitHub](https://github.com/Azure/WALinuxAgent/releases)，範例：
     
            # wget https://github.com/Azure/WALinuxAgent/archive/v2.2.0.tar.gz
   * 解除封裝 hello Azure 代理程式：
     
            # tar -vzxf v2.2.0.tar.gz
   * 安裝 python 安裝工具
     
        **Debian / Ubuntu**
     
            # sudo apt-get update
            # sudo apt-get install python-setuptools
     
        **Ubuntu 16.04+**
     
            # sudo apt-get install python3-setuptools
     
        **RHEL / CentOS / Oracle Linux**
     
            # sudo yum install python-setuptools
   * 安裝 Azure 代理程式 hello:
     
            # cd WALinuxAgent-2.2.0
            # sudo python setup.py install --register-service
     
     系統使用 Python 2.x 和 Python 安裝 3.x-並存可能需要 toorun hello 下列命令：
     
         sudo python3 setup.py install --register-service
     如需詳細資訊，請參閱 hello Azure Linux 代理程式[讀我檔案](https://github.com/Azure/WALinuxAgent/blob/master/README.md)。
3. [新增 hello 映像 toohello Marketplace](azure-stack-add-vm-image.md)。 請確定該 hello`OSType`參數設定太`Linux`。
4. 您加入 hello 映像 toohello Marketplace 之後，建立 Marketplace 項目，而且您可以部署 Linux 虛擬機器。

## <a name="next-steps"></a>後續步驟
[Azure Stack 的常見問題集](azure-stack-faq.md)

