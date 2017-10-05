---
title: "Azure Stack 上的 Linux 客體 | Microsoft Docs"
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
ms.openlocfilehash: 935cd31c4b38262b7e42271574a8a221377a3cec
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="deploy-linux-virtual-machines-on-azure-stack"></a>在 Azure Stack 上部署 Linux 虛擬機器
您可以透過將 Linux 式映像新增到 Azure Stack Marketplace 中，在 Azure Stack 開發套件上部署 Linux 虛擬機器。 已有數個 Linux 廠商提供可新增到 Azure Stack 開發套件中的映像，您也可以建立自己的映像。

## <a name="download-an-image"></a>下載映像
1. 從下列連結下載並解壓縮與 Azure Stack 相容的映像，或準備您自己的映像：
   
   * [Bitnami](https://bitnami.com/azure-stack)
   * [CentOS](http://olstacks.cloudapp.net/latest/)
   * [CoreOS](https://stable.release.core-os.net/amd64-usr/current/coreos_production_azure_image.vhd.bz2)
   * [SuSE](https://download.suse.com/Download?buildid=VCFi7y7MsFQ~)
   * [Ubuntu 14.04 LTS](https://partner-images.canonical.com/azure/azure_stack/) / [Ubuntu 16.04 LTS](http://cloud-images.ubuntu.com/releases/xenial/release/ubuntu-16.04-server-cloudimg-amd64-disk1.vhd.zip)
2. 如有必要，請將映像 VHD 解壓縮，並[將影像新增到 Marketplace 中](azure-stack-add-vm-image.md)。 請確定已將 `OSType` 參數設定為 `Linux`。
3. 將映像新增到 Marketplace 中之後，便會建立 Marketplace 項目，而您就可以部署 Linux 虛擬機器。

## <a name="prepare-your-own-image"></a>準備您自己的映像
1. 使用下列其中一種指示，準備您自己的 Linux 映像：
   
   * [CentOS 型發行版本](../virtual-machines/linux/create-upload-centos.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
   * [Debian Linux](../virtual-machines/linux/debian-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
   * [Oracle Linux](../virtual-machines/linux/oracle-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
   * [Red Hat Enterprise Linux](../virtual-machines/linux/redhat-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
   * [SLES 和 openSUSE](../virtual-machines/linux/suse-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
   * [Ubuntu](../virtual-machines/linux/create-upload-ubuntu.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
2. 下載並安裝 [Azure Linux 代理程式](https://github.com/Azure/WALinuxAgent/)
   
    需要 Azure Linux 代理程式版本 2.1.3 或更高版本，才能在 Azure Stack 上佈建 Linux VM。 以上所列的許多發佈已在其存放庫中包含此版本的代理程式或更高版本 (通常是稱作 `WALinuxAgent` 或 `walinuxagent` 的套件)。 不過，若 Azure 代理程式套件的版本小於 2.1.3 (亦即 2.0.18 或更低)，則您必須手動安裝代理程式。 可從套件名稱或執行虛擬機器上的 `/usr/sbin/waagent -version` 來判斷已安裝的版本。
   
    請遵循下列指示，手動安裝 Azure Linux 代理程式：
   
   * 首先，從 [GitHub](https://github.com/Azure/WALinuxAgent/releases) 下載最新的 Azure Linux 代理程式，例如：
     
            # wget https://github.com/Azure/WALinuxAgent/archive/v2.2.0.tar.gz
   * 解壓縮 Azure 代理程式：
     
            # tar -vzxf v2.2.0.tar.gz
   * 安裝 python 安裝工具
     
        **Debian / Ubuntu**
     
            # sudo apt-get update
            # sudo apt-get install python-setuptools
     
        **Ubuntu 16.04+**
     
            # sudo apt-get install python3-setuptools
     
        **RHEL / CentOS / Oracle Linux**
     
            # sudo yum install python-setuptools
   * 安裝 Azure 代理程式：
     
            # cd WALinuxAgent-2.2.0
            # sudo python setup.py install --register-service
     
     已並存安裝 Python 2.x 和 Python 3.x 的系統可能會需要執行下列命令：
     
         sudo python3 setup.py install --register-service
     如需詳細資訊，請參閱 Azure Linux 代理程式[讀我檔案](https://github.com/Azure/WALinuxAgent/blob/master/README.md)。
3. [將映像新增到 Marketplace 中](azure-stack-add-vm-image.md)。 請確定已將 `OSType` 參數設定為 `Linux`。
4. 將映像新增到 Marketplace 中之後，便會建立 Marketplace 項目，而您就可以部署 Linux 虛擬機器。

## <a name="next-steps"></a>後續步驟
[Azure Stack 的常見問題集](azure-stack-faq.md)

